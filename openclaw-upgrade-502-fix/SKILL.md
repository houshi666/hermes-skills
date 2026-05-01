---
name: openclaw-upgrade-502-fix
description: OpenClaw 升级运维完整指南 — 502 错误排查、标准升级 SOP、应急回滚、日常运维
category: devops
---

# OpenClaw 升级与运维最佳实践

## 环境基线
- **服务器**: 京东云 117.72.204.78 (Ubuntu 22.04 LTS)
- **Node.js**: v22.x (当前 v22.22.1)
- **npm**: v10.x (当前 10.9.4)
- **OpenClaw**: v2026.4+

## 架构说明

| 组件 | 角色 | 端口 | 配置文件 |
|------|------|------|----------|
| Nginx | 前端反向代理 | 18789 (HTTP) / 8443 (HTTPS) | `/etc/nginx/sites-enabled/openclaw` |
| OpenClaw Gateway | 核心业务逻辑 | 18790 (HTTP) | `/root/.openclaw/openclaw.json` |
| Systemd | 进程守护 | N/A | `/root/.config/systemd/user/openclaw-gateway.service` |

**502 = Nginx (18789) 无法连接到 Gateway (18790)**

---

## 标准升级 SOP（零停机/最小停机）

### 步骤 1：升级前备份与停服
```bash
# 备份核心配置
cp /root/.openclaw/openclaw.json /root/.openclaw/openclaw.json.bak.$(date +%Y%m%d_%H%M%S)
cp /root/.config/systemd/user/openclaw-gateway.service /root/.config/systemd/user/openclaw-gateway.service.bak.$(date +%Y%m%d_%H%M%S)

# 优雅停止服务
export XDG_RUNTIME_DIR=/run/user/$(id -u)
systemctl --user stop openclaw-gateway.service
```

### 步骤 2：执行升级
```bash
npm install -g openclaw@latest
```

### 步骤 3：同步 Systemd 服务版本
```bash
NEW_VERSION=$(cat $(npm root -g)/openclaw/package.json | grep '"version"' | awk -F'"' '{print $4}')
sed -i "s/Description=OpenClaw Gateway (v[^)]*)/Description=OpenClaw Gateway (v${NEW_VERSION})/" /root/.config/systemd/user/openclaw-gateway.service
sed -i "s/OPENCLAW_SERVICE_VERSION=[^ ]*/OPENCLAW_SERVICE_VERSION=${NEW_VERSION}/" /root/.config/systemd/user/openclaw-gateway.service
```

### 步骤 4：配置兼容性检查（关键！）
```bash
openclaw doctor --fix
```
> ⚠️ 如果 `doctor --fix` 报错，见下方「故障排查」手动修复。

### 步骤 5：重启并验证
```bash
systemctl --user daemon-reload
systemctl --user start openclaw-gateway.service

# 多维度验证
systemctl --user status openclaw-gateway.service
ss -tlnp | grep 18790
curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:18789/
```

---

## 502 错误排查流程

### 快速诊断
```bash
ss -tlnp | grep -E '18789|18790'
XDG_RUNTIME_DIR=/run/user/0 systemctl --user status openclaw-gateway.service
tail -50 /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log
```

### 根因 A: npm 包丢失 (MODULE_NOT_FOUND)
```bash
# 验证
node /usr/lib/node_modules/openclaw/dist/index.js gateway --port 18790
# 报 MODULE_NOT_FOUND → 重新安装
npm install -g openclaw@latest
```

### 根因 B: 插件配置不兼容（最常见）
**典型错误**:
```
Config invalid
- plugins.installs.bonjour.source: Invalid input
- plugins.installs.bonjour: Unrecognized key: "enabled"
```
或:
```
Unhandled promise rejection: CIAO PROBING CANCELLED
```

**修复**:
```bash
cp /root/.openclaw/openclaw.json /root/.openclaw/openclaw.json.bak.$(date +%Y%m%d_%H%M%S)

python3 -c "
import json
config_path = '/root/.openclaw/openclaw.json'
with open(config_path, 'r') as f:
    config = json.load(f)

# 清理 installs 中的无效插件
if 'plugins' in config and 'installs' in config['plugins']:
    for plugin in ['bonjour']:
        if plugin in config['plugins']['installs']:
            del config['plugins']['installs'][plugin]
            print(f'已清理: {plugin}')

    # 通用检查：source 必须是合法值
    for key in list(config['plugins']['installs'].keys()):
        source = config['plugins']['installs'][key].get('source', '')
        if source not in ('npm', 'archive', 'path', 'clawhub', 'marketplace'):
            del config['plugins']['installs'][key]
            print(f'已清理无效 source 插件: {key}')

with open(config_path, 'w') as f:
    json.dump(config, f, indent=2, ensure_ascii=False)
print('配置清理完成')
"
```

### 根因 C: Systemd 服务文件版本不一致
```bash
CURRENT_VERSION=$(cat $(npm root -g)/openclaw/package.json | grep '"version"' | awk -F'"' '{print $4}')
sed -i "s/Description=OpenClaw Gateway (v[^)]*)/Description=OpenClaw Gateway (v${CURRENT_VERSION})/" /root/.config/systemd/user/openclaw-gateway.service
```

### 修复后重启
```bash
export XDG_RUNTIME_DIR=/run/user/$(id -u)
systemctl --user daemon-reload
systemctl --user restart openclaw-gateway.service
sleep 5
ss -tlnp | grep 18790
curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:18789/
```

---

## 应急回滚方案

升级后出现无法快速修复的故障时，立即回滚：

```bash
# 1. 停止服务
export XDG_RUNTIME_DIR=/run/user/$(id -u)
systemctl --user stop openclaw-gateway.service

# 2. 恢复配置
cp /root/.openclaw/openclaw.json.bak.YYYYMMDD_HHMMSS /root/.openclaw/openclaw.json
cp /root/.config/systemd/user/openclaw-gateway.service.bak.YYYYMMDD_HHMMSS /root/.config/systemd/user/openclaw-gateway.service

# 3. 降级 npm 包（替换为上一个稳定版本）
npm install -g openclaw@2026.3.31

# 4. 重启
systemctl --user daemon-reload
systemctl --user start openclaw-gateway.service
systemctl --user status openclaw-gateway.service
```

---

## 日常运维与监控

### 日志查看
```bash
# 实时日志
journalctl --user -u openclaw-gateway.service -f

# OpenClaw 应用日志
tail -f /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log
```

### 定期清理
```bash
# 清理超过 30 天的备份文件
find /root/.openclaw/ -name "*.bak.*" -mtime +30 -delete

# 清理旧日志
find /root/.openclaw/logs/ -name "*.json" -mtime +30 -delete
```

### 配置变更审计
任何对 `openclaw.json` 的手动修改：
1. 修改前备份
2. 修改后运行 `openclaw doctor --fix` 验证

---

## 关键坑点总结

1. **bonjour 插件**: 云服务器上 mDNS 不可用，probing 超时 → 进程崩溃 → systemd 无限重启。从 `plugins.installs` 中移除。
2. **配置校验变严格**: 新版本拒绝旧版配置格式，升级后必须先跑 `openclaw doctor --fix`。
3. **systemd user session**: 必须设置 `XDG_RUNTIME_DIR=/run/user/0` 才能操作用户服务。
4. **服务文件不自动更新**: npm 升级不会更新 systemd 服务文件，需手动同步版本号。
5. **先停服再升级**: 永远先 `systemctl --user stop` 再 `npm install`，避免文件锁定或状态不一致。
