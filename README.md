# Hermes Skills — 完整功能文档

> 仓库地址: https://github.com/wszz117/hermes-skills
> 共 89 个 Skills，覆盖 17 个分类

---

## 📑 目录

- [🍎 Apple — macOS 原生集成](#-apple--macos-原生集成)
- [🤖 Autonomous AI Agents — 自主 AI 编码代理](#-autonomous-ai-agents--自主-ai-编码代理)
- [🎨 Creative — 创意内容生成](#-creative--创意内容生成)
- [📊 Data Science — 数据科学](#-data-science--数据科学)
- [🔧 DevOps — 运维自动化](#-devops--运维自动化)
- [📧 Email — 邮件管理](#-email--邮件管理)
- [🎮 Gaming — 游戏服务器](#-gaming--游戏服务器)
- [🐙 GitHub — 代码仓库管理](#-github--代码仓库管理)
- [📍 Leisure — 休闲生活](#-leisure--休闲生活)
- [🔌 MCP — 模型上下文协议](#-mcp--模型上下文协议)
- [🎵 Media — 媒体处理](#-media--媒体处理)
- [🧠 MLOps — 机器学习运维](#-mlops--机器学习运维)
- [📝 Note-taking — 笔记管理](#-note-taking--笔记管理)
- [📦 OpenClaw — AI 网关部署](#-openclaw--ai-网关部署)
- [💼 Productivity — 生产力工具](#-productivity--生产力工具)
- [🔴 Red-teaming — 安全测试](#-red-teaming--安全测试)
- [🔬 Research — 学术研究](#-research--学术研究)
- [🏠 Smart Home — 智能家居](#-smart-home--智能家居)
- [📱 Social Media — 社交媒体](#-social-media--社交媒体)
- [💻 Software Development — 软件开发](#-software-development--软件开发)
- [🐛 Dogfood — Web 应用 QA 测试](#-dogfood--web-应用-qa-测试)

---

## 🍎 Apple — macOS 原生集成

> 需要 macOS 环境，通过 CLI 工具桥接 Apple 原生应用

### apple-notes — Apple 备忘录管理
**能做什么：** 通过 `memo` CLI 创建、查看、搜索、编辑 Apple Notes 备忘录
- `memo create "标题" "内容"` — 创建新备忘录
- `memo list` — 列出所有备忘录
- `memo search "关键词"` — 搜索备忘录
- `memo edit <id> "新内容"` — 编辑已有备忘录
- `memo view <id>` — 查看备忘录详情

### apple-reminders — Apple 提醒事项
**能做什么：** 通过 `remindctl` CLI 管理 Apple Reminders
- `remindctl list` — 列出所有提醒事项
- `remindctl add "买牛奶" --due "明天 9:00"` — 创建提醒
- `remindctl complete <id>` — 标记完成
- `remindctl delete <id>` — 删除提醒
- 支持日期格式：`today`、`tomorrow`、`next week`、`2026-05-01`

### findmy — 设备与 AirTag 追踪
**能做什么：** 通过 AppleScript + 截图获取 FindMy.app 中的设备位置
- 自动打开 FindMy 应用并截图
- 读取设备列表（iPhone、iPad、Mac、AirTag）
- 获取设备位置和电量信息
- 适用于"我的 iPhone 在哪"类场景

### imessage — iMessage/SMS 消息
**能做什么：** 通过 `imsg` CLI 收发 iMessage 和短信
- `imsg send "联系人" "消息内容"` — 发送消息
- `imsg list` — 查看最近对话
- `imsg read <chat-id>` — 读取对话内容
- 支持附件信息查看

---

## 🤖 Autonomous AI Agents — 自主 AI 编码代理

> 将编码任务委派给专用 AI 代理，实现自主开发

### claude-code — Claude Code 代理
**能做什么：** 委派编码任务给 Anthropic 的 Claude Code CLI 代理
- **交互式模式：** 在 tmux 中启动 Claude Code，实时监控进度
- **一次性任务：** 发送任务指令，自动完成并返回结果
- 适用场景：构建功能、重构代码、PR 审查、迭代开发
- 支持 `--acp` 模式，通过 stdio 通信
- 可指定模型（如 `claude-opus-4-6`）

### codex — OpenAI Codex 代理
**能做什么：** 委派编码任务给 OpenAI Codex CLI 代理
- **前台模式：** 短任务，即时完成
- **后台模式：** 长任务，通过 PTY 交互，可中途回答问题
- 适用场景：功能实现、重构、PR 审查、批量 issue 修复
- 需要 git 仓库环境

### hermes-agent — Hermes Agent 完整指南
**能做什么：** Hermes Agent 的使用和扩展完整手册（27KB 详细文档）
- CLI 安装和配置
- 模型/Provider 切换
- 子代理编排（delegate_task）
- Gateway 平台集成（飞书、Discord、Telegram 等）
- Skills 系统使用和创建
- 语音功能配置
- 工具系统详解
- Profile 配置
- 贡献者参考

### opencode — OpenCode 代理
**能做什么：** 委派编码任务给 OpenCode CLI 代理
- **一次性任务：** `opencode run "任务描述"`
- **交互会话：** 后台启动，通过 PTY 发送指令
- 适用场景：功能实现、重构、PR 审查、长时间自主会话
- 支持二进制路径自动解析

---

## 🎨 Creative — 创意内容生成

> AI 驱动的视觉内容创作，从图表到视频到音乐

### architecture-diagram — 软件架构图
**能做什么：** 生成深色主题 SVG 架构图（HTML + 内联 SVG）
- 软件系统架构图、云基础设施图
- 微服务拓扑、数据库 + API 层图
- 安全组、消息总线图
- **语义配色：** cyan=前端, emerald=后端, violet=数据库, amber=云/AWS, rose=安全
- 使用 JetBrains Mono 字体，网格背景
- 基于 Cocoon AI 的 architecture-diagram-generator（MIT）

### ascii-art — ASCII 艺术字
**能做什么：** 多种工具生成 ASCII 艺术
- **pyfiglet：** 571 种字体，本地生成
- **asciified API：** 远程 API，无需安装
- **cowsay：** 消息艺术（多种动物）
- **boxes/toilet：** 边框和彩色文字
- **image-to-ascii：** 图片转 ASCII
- 无需 API Key

### ascii-video — ASCII 视频制作
**能做什么：** 完整的 ASCII 艺术视频生产线（314KB 参考文档）
- **输入模式：** 视频转 ASCII、音频响应式、图片转 ASCII、生成式输入
- **输出格式：** MP4、GIF、图片序列
- **创意方向：** 音乐可视化、歌词动画、复古终端风格视频
- **参考文档：** 架构设计、合成技术、特效库、输入处理、优化指南、场景设计、着色器、故障排查
- 8 个参考文档模块，覆盖完整生产管线

### baoyu-comic — 知识漫画创作
**能做什么：** 教育漫画创作，支持多种画风和色调（116KB 资源）
- **画风：** 粉笔、水墨、清晰线条、漫画、极简、写实
- **布局：** 四格、电影、标准、密集、全页、混合、Webtoon
- **色调：** 动作、戏剧、活力、中性、浪漫、复古、温暖
- **预设：** 概念故事、四格、少女、武侠
- **工作流：** 分析 → 分镜 → 角色设计 → 逐格生成 → 合成
- 35 个参考文件，覆盖完整创作流程

### baoyu-infographic — 信息图生成
**能做什么：** 专业信息图生成，21 种布局 × 21 种视觉风格
- **布局：** Bento 网格、对比矩阵、漏斗图、冰山图、树状分支、维恩图等
- **风格：** 学术、黑板、赛博朋克、手绘教育、Kawaii、像素艺术、复古流行等
- 自动分析内容并推荐最佳布局 × 风格组合
- 生成可直接发布的信息图

### creative-ideation — 创意灵感
**能做什么：** 通过创意约束生成项目灵感
- 当你说"我想做点什么但不知道做什么"时使用
- 约束库包含：材料限制、时间限制、技术限制、主题限制等
- 输出格式：约束描述 + 示例项目 + 为什么适合你
- 适用于代码、艺术、硬件、写作等任何领域

### excalidraw — 手绘风格图表
**能做什么：** 生成 Excalidraw JSON 格式的手绘风格图表
- 架构图、流程图、序列图、概念图
- 生成 `.excalidraw` 文件，可在 excalidraw.com 打开
- 支持配色方案、暗色模式
- 包含上传脚本，可生成分享链接
- 元素格式参考：矩形、椭圆、箭头、自由绘制、文字、连线

### manim-video — 数学动画视频
**能做什么：** 3Blue1Brown 风格的数学/技术动画（98KB 参考文档）
- **内容类型：** 数学公式推导、算法可视化、架构图、数据故事
- **参考文档：** 动画设计思维、动画类型、相机和 3D、装饰元素、方程、图表、对象、论文讲解、制作质量、渲染、场景规划、故障排查、更新器和追踪器、视觉设计
- 17 个参考文件，覆盖从创意到渲染的完整管线

### p5js — 交互式生成艺术
**能做什么：** p5.js 交互式视觉艺术完整管线（161KB 资源）
- **内容类型：** 生成艺术、数据可视化、交互体验、3D 场景、音频响应视觉
- **参考文档：** 动画、色彩系统、核心 API、导出管线、交互、形状几何、故障排查、排版、视觉特效、WebGL 3D
- **脚本：** 导出帧、渲染、服务、安装
- **模板：** HTML 查看器
- 17 个文件，覆盖完整创作流程

### pixel-art — 像素艺术
**能做什么：** 图片转复古像素艺术 + 动画
- **预设：** NES、Game Boy、PICO-8、C64、街机、SNES 等 10+ 种硬件精确调色板
- **输出：** 静态图片 + 短视频动画
- **场景：** 静态、平移、缩放、脉冲、故障、粒子
- 包含 Python 脚本：`pixel_art.py`、`pixel_art_video.py`、`palettes.py`

### popular-web-designs — 网页设计模板库
**能做什么：** 54 个真实网站的设计系统提取（853KB）
- **包含网站：** Stripe、Linear、Vercel、Notion、Airbnb、Apple、BMW、Claude、Cursor、Figma、Miro、Spotify、Uber 等
- **每个模板包含：** 配色方案、排版、组件、布局规则、CSS 值
- **使用方式：** 加载模板 → 生成 HTML/CSS，匹配目标网站的视觉风格
- 适合快速原型设计、学习优秀设计

### songwriting-and-ai-music — 歌曲创作 & AI 音乐
**能做什么：** 歌曲创作指南 + Suno AI 音乐生成提示工程
- **歌曲结构：** 主歌-副歌、AABA、叙事体等
- **押韵和节奏：** 韵脚方案、音节计数、元音匹配
- **情感弧线：** 动态变化、高潮设计
- **歌词写作：** 意象、隐喻、具体细节
- **Suno 提示：** 风格标签、结构标记、音色描述
- **AI 歌手技巧：** 音素选择、发音优化

---

## 📊 Data Science — 数据科学

### jupyter-live-kernel — 实时 Jupyter 内核
**能做什么：** 通过 hamelnb 连接实时 Jupyter 内核，实现有状态的 Python 执行
- **vs execute_code：** 支持中间结果查看、迭代式开发、状态保持
- **操作：** 查看单元格、插入新单元格、替换内容、执行、查看输出
- **适用场景：** 数据探索、API 测试、迭代式代码开发、机器学习实验
- 支持单元格级别的输出查看和调试

---

## 🔧 DevOps — 运维自动化

### webhook-subscriptions — Webhook 订阅管理
**能做什么：** 创建和管理 Webhook 订阅，实现事件驱动的 Agent 激活
- **用途：** 外部服务触发 Agent 运行，或直接推送通知（零 LLM 成本）
- **支持事件：** GitHub push/PR、飞书消息、定时任务等
- **安全：** 签名验证、IP 白名单
- **模板：** 包含常见 Webhook 场景的 prompt 模板

---

## 📧 Email — 邮件管理

### himalaya — 邮件 CLI 客户端
**能做什么：** 通过 IMAP/SMTP 管理邮件，纯终端操作
- **收发邮件：** `himalaya read`、`himalaya write`、`himalaya reply`、`himalaya forward`
- **搜索：** `himalaya search "关键词"`
- **管理：** 邮件分类、标记已读/未读
- **多账户：** 支持多个邮箱配置
- **MML 格式：** MIME Meta Language 编写邮件内容
- 包含配置指南和消息组合参考

---

## 🎮 Gaming — 游戏服务器

### minecraft-modpack-server — 模组 Minecraft 服务器
**能做什么：** 从 CurseForge/Modrinth 服务器包搭建模组服务器
- **支持：** NeoForge/Forge 安装
- **配置：** Java 版本选择、JVM 调优、防火墙、局域网配置
- **运维：** 备份脚本、启动脚本
- 先收集用户偏好（玩家数、机器配置、模组包）

### pokemon-player — 自动玩 Pokemon
**能做什么：** 通过无头模拟器自动玩 Pokemon 游戏
- **启动：** 启动游戏服务器，从 RAM 读取结构化游戏状态
- **决策：** AI 根据游戏状态做出战略决策
- **输入：** 发送按钮输入控制游戏
- **战斗策略：** 自动战斗、属性克制、HP 管理
- **存档：** 自动保存和加载

---

## 🐙 GitHub — 代码仓库管理

### codebase-inspection — 代码库检查
**能做什么：** 使用 pygount 分析代码库统计信息
- LOC 行数统计、语言分布、代码/注释比例
- 支持排除常见目录（node_modules、.git、venv 等）
- 适用于 Python、JS/TS、Go、Rust 等任何项目

### github-auth — GitHub 认证设置
**能做什么：** 设置 GitHub 认证的完整指南
- **方法 1：** git-only（HTTPS token / SSH key），无需 sudo
- **方法 2：** gh CLI 认证（交互式/Token）
- **Token 管理：** 创建 PAT、配置 credential helper
- **SSH：** 密钥生成、GitHub 添加、连接测试
- **故障排查：** 密码认证失败、多账户、端口问题

### github-code-review — 代码审查
**能做什么：** 全面的代码审查，支持 PR 评论和本地预检
- **本地审查：** 分析 git diff，检查 debug 语句、TODO、安全隐患
- **PR 审查：** 在 PR 上留内联评论
- **审查清单：** 安全性、代码质量、性能、可维护性
- 支持 gh CLI 或 curl + REST API

### github-issues — Issue 管理
**能做什么：** 创建、管理、分类、关闭 GitHub Issues
- **查看：** 按标签过滤、搜索、查看详情
- **创建：** 支持 bug report 和 feature request 模板
- **管理：** 添加标签、分配人员、关联 PR
- **搜索：** 关键词搜索、状态过滤

### github-pr-workflow — PR 完整工作流
**能做什么：** Pull Request 全生命周期管理
- **分支：** 创建功能分支、同步主分支
- **提交：** 规范 commit message（Conventional Commits）
- **PR：** 创建 PR、填写模板（bugfix/feature）
- **CI：** 监控 CI 状态、自动修复失败
- **合并：** 合并 PR、清理分支
- 包含 CI 故障排查指南

### github-publish-skills — Skills 发布
**能做什么：** 将 Hermes Skills 发布到 GitHub 仓库
- 认证 → 仓库创建 → 文件推送完整流程
- 处理网络超时问题（京东云服务器经验）
- 支持 API 批量上传和 git tree API 批量提交

### github-repo-management — 仓库管理
**能做什么：** 克隆、创建、Fork、配置 GitHub 仓库
- **仓库操作：** clone、create、fork、删除
- **Remote 管理：** 添加/修改/删除 remote
- **Secrets：** 管理仓库密钥
- **Releases：** 创建和管理发布版本
- **Workflows：** 管理 GitHub Actions
- 包含 GitHub API 速查表

---

## 📍 Leisure — 休闲生活

### find-nearby — 附近地点搜索
**能做什么：** 基于 OpenStreetMap 搜索附近地点
- **类别：** 餐厅、咖啡馆、酒吧、药店、超市、银行、医院等
- **输入：** 坐标、地址、城市、邮编、Telegram 位置
- **输出：** 名称、地址、距离、评分
- 无需 API Key，免费使用
- 包含 Python 脚本 `find_nearby.py`

---

## 🔌 MCP — 模型上下文协议

### mcporter — MCP CLI 桥接
**能做什么：** 通过 mcporter CLI 直接操作 MCP 服务器
- **列出服务器：** 查看已配置的 MCP 服务器
- **列出工具：** 查看服务器提供的工具及 schema
- **调用工具：** 直接调用 MCP 工具
- **配置：** 添加/编辑 MCP 服务器配置
- 支持 HTTP 和 stdio 传输

### native-mcp — 内置 MCP 客户端
**能做什么：** Hermes 内置的 MCP 客户端，自动发现和注册工具
- **自动发现：** 连接 MCP 服务器后自动发现工具
- **工具注册：** 将 MCP 工具注册为 Hermes 原生工具
- **传输类型：** stdio（本地进程）和 HTTP（远程服务）
- **安全：** 自动重连、安全过滤
- **配置：** YAML 配置服务器列表

---

## 🎵 Media — 媒体处理

### gif-search — GIF 搜索
**能做什么：** 通过 Tenor API 搜索和下载 GIF
- `curl` + `jq` 实现，无额外依赖
- 搜索关键词 → 获取 GIF URL
- 支持预览/小尺寸版本
- 直接下载 GIF 文件
- 适合聊天表情包、内容创作

### heartmula — AI 音乐生成
**能做什么：** 开源音乐生成模型 HeartMuLa（类似 Suno）
- **输入：** 歌词 + 风格标签 → 输出完整歌曲
- **多语言：** 支持多种语言歌词
- **硬件：** 需要 GPU（有硬件要求说明）
- **安装指南：** 完整的依赖安装和模型加载
- 处理 pyarrow、transformers 等兼容性问题

### songsee — 音频可视化
**能做什么：** 从音频文件生成频谱图和音频特征可视化
- **可视化类型：** Mel 频谱、Chroma、MFCC、Tempogram 等
- **用途：** 音频分析、音乐制作调试、视觉文档
- **输入：** 音频文件路径或 stdin
- **输出：** PNG 图片，支持多面板网格
- 支持时间切片（指定起始时间和时长）

### youtube-content — YouTube 内容处理
**能做什么：** 获取 YouTube 视频字幕并转换为结构化内容
- **获取字幕：** 支持多语言、带时间戳
- **输出格式：** 章节摘要、博客文章、Twitter 线程、要点列表
- **辅助脚本：** `fetch_transcript.py` 获取原始字幕
- 适合视频内容总结、学习笔记、内容再创作

---

## 🧠 MLOps — 机器学习运维

### ☁️ Cloud — GPU 云

#### modal — Serverless GPU
**能做什么：** Modal 无服务器 GPU 平台
- **适用场景：** 按需 GPU、模型部署为 API、批量任务
- **GPU 配置：** 单 GPU、多 GPU（最多 8 卡）、指定显存
- **核心概念：** App、Function、Image、Volume、Secret
- **自动扩缩容：** 无需管理基础设施

### 📊 Evaluation — 模型评估

#### lm-evaluation-harness — 学术基准测试
**能做什么：** 评估 LLM 在 60+ 学术基准上的表现
- **基准：** MMLU（57 学科）、HumanEval、GSM8K、TruthfulQA、HellaSwag
- **适用场景：** 模型质量对比、训练进度跟踪、学术报告
- **训练循环集成：** 自动评估 checkpoint
- 行业标准，EleutherAI/HuggingFace 使用

#### weights-and-biases — 实验跟踪
**能做什么：** W&B ML 实验跟踪和 MLOps 平台
- **实验跟踪：** 自动日志、实时训练可视化
- **超参优化：** Sweeps 自动搜索最佳参数
- **模型注册：** 版本管理、部署流水线
- **Artifacts：** 数据集和模型版本管理
- **集成：** 支持 PyTorch、TensorFlow、Transformers 等

### 📦 HuggingFace Hub

#### huggingface-hub — HF Hub CLI
**能做什么：** 通过 `hf` CLI 管理 HuggingFace Hub
- **搜索：** 模型、数据集、Spaces
- **下载/上传：** 模型权重、数据集
- **仓库管理：** 创建、配置、删除 Hub 仓库
- **SQL 查询：** 对数据集执行 SQL 查询
- **推理端点：** 部署模型 API

### 🔮 Inference — 模型推理

#### gguf — GGUF 量化格式
**能做什么：** llama.cpp GGUF 量化，CPU/GPU 推理
- **量化级别：** Q2_K 到 Q8_0，2-8 bit
- **构建：** CPU、CUDA（NVIDIA）、Metal（Apple Silicon）
- **Python 绑定：** llama-cpp-python
- **适用场景：** 消费级硬件部署、本地推理
- 包含高级用法和故障排查

#### guidance — 约束生成
**能做什么：** Microsoft Guidance — 约束 LLM 输出
- **正则约束：** 保证输出匹配正则表达式
- **语法约束：** 保证 JSON/XML/代码结构正确
- **多步工作流：** 构建复杂的生成流水线
- **后端：** OpenAI、Transformers、llama.cpp
- 61KB 详细文档，含大量示例

#### llama-cpp — llama.cpp 推理
**能做什么：** llama.cpp 本地 GGUF 推理 + HF Hub 模型发现
- **模型发现：** 在 HuggingFace Hub 搜索 GGUF 模型
- **量化选择：** 根据硬件选择合适的量化级别
- **Python API：** 流式输出、批量推理
- **服务器模式：** 启动 OpenAI 兼容 API
- 43KB 参考文档

#### obliteratus — 模型去拒答
**能做什么：** 使用机械可解释性技术移除 LLM 拒答行为
- **技术：** diff-in-means、SVD、白化 SVD、LEACE、SAE 分解
- **9 种 CLI 方法：** 不同的消融策略
- **28 个分析模块：** 评估消融效果
- **116 个模型预设：** 覆盖 5 个计算层级
- **Gradio UI：** Web 界面支持
- 31KB 详细文档

#### outlines — 结构化文本生成
**能做什么：** dottxt.ai Outlines — 保证结构化输出
- **JSON 保证：** 100% 有效 JSON 输出
- **Pydantic 模型：** 类型安全的输出定义
- **正则/语法：** 任意结构化格式
- **后端：** Transformers、vLLM
- **XML/代码：** 同样支持
- 64KB 详细文档，含大量示例

#### vllm — 高性能 LLM 服务
**能做什么：** vLLM 生产级 LLM API 部署
- **PagedAttention：** 高效显存管理
- **Continuous Batching：** 高吞吐量
- **OpenAI 兼容：** 标准 API 接口
- **量化：** GPTQ/AWQ/FP8
- **张量并行：** 多 GPU 部署（30B-70B 模型）
- 包含负载测试指南

### 🧩 Models — 模型

#### audiocraft — 音频生成
**能做什么：** Meta AudioCraft — 文本生成音乐/音效
- **MusicGen：** 文本描述 → 音乐
- **AudioGen：** 文本描述 → 音效
- **旋律条件：** 基于旋律生成音乐
- **安装：** PyPI 或 GitHub 源码
- 43KB 详细文档

#### clip — 视觉语言模型
**能做什么：** OpenAI CLIP — 连接视觉和语言
- **零样本分类：** 无需训练即可分类图片
- **图文匹配：** 计算图片和文本的相似度
- **跨模态检索：** 用文本搜索图片
- **内容审核：** 检测不当内容
- 训练于 4 亿图文对

#### segment-anything — 图像分割
**能做什么：** Meta SAM — 通用图像分割
- **提示分割：** 用点、框、mask 提示分割任意对象
- **自动分割：** 自动生成图中所有对象的 mask
- **模型选择：** ViT-H（最大 2.4GB）、ViT-L（1.2GB）、ViT-B
- **零样本迁移：** 无需训练即可处理新领域
- 40KB 详细文档

#### stable-diffusion — 图像生成
**能做什么：** Stable Diffusion 文本生成图像
- **文生图：** 文本描述 → 图像
- **图生图：** 基于参考图生成
- **修复：** Inpainting 填充指定区域
- **架构：** UNet、VAE、CLIP Text Encoder
- **优化：** 显存优化、加速推理
- 42KB 详细文档

#### whisper — 语音识别
**能做什么：** OpenAI Whisper — 通用语音识别
- **99 种语言：** 多语言语音转文字
- **翻译：** 自动翻译为英文
- **语言识别：** 自动检测语言
- **模型大小：** tiny(39M) → large(1550M)
- 支持 ffmpeg 音频处理

### 🔬 Research — 研究框架

#### dspy — 声明式 AI 编程
**能做什么：** Stanford DSPy — 声明式 LLM 编程框架
- **声明式编程：** 定义"做什么"而非"怎么做"
- **自动优化：** 自动优化提示
- **模块化 RAG：** 构建检索增强系统
- **Agent 构建：** 创建复杂 AI 系统
- **优化器：** BootstrapFewShot、MIPRO、COPRO 等
- 60KB 详细文档

### 🏋️ Training — 模型训练

#### axolotl — LLM 微调
**能做什么：** Axolotl — YAML 配置的 LLM 微调框架
- **100+ 模型：** 支持主流开源模型
- **训练方式：** LoRA/QLoRA、DPO/KTO/ORPO/GRPO
- **多模态：** 支持视觉语言模型
- **配置：** YAML 文件定义所有参数
- 305KB 参考文档（含完整 API 参考）

#### grpo-rl-training — GRPO 强化学习训练
**能做什么：** TRL + GRPO — 推理和任务专项训练
- **核心概念：** GRPO 算法原理、奖励设计
- **实现流程：** 模型加载 → 奖励模型 → 训练循环
- **LoRA 支持：** 参数高效训练
- 26KB 文档，含模板代码

#### peft — 参数高效微调
**能做什么：** HuggingFace PEFT — 25+ 种参数高效方法
- **方法：** LoRA、QLoRA、AdaLoRA、IA3、Prefix Tuning 等
- **适用场景：** 7B-70B 模型、有限 GPU 显存
- **效率：** 训练 <1% 参数，质量损失最小
- **多适配器：** 支持多适配器服务
- 34KB 详细文档

#### pytorch-fsdp — 分布式训练
**能做什么：** PyTorch FSDP — 全分片数据并行训练
- **参数分片：** 模型参数跨 GPU 分片
- **混合精度：** FP16/BF16 训练
- **CPU 卸载：** 显存不足时使用 CPU
- **FSDP2：** 新一代分片策略
- 486KB 参考文档（最详细的 skill 之一）

#### trl-fine-tuning — Transformer 强化学习
**能做什么：** TRL — 强化学习微调框架
- **SFT：** 指令微调
- **DPO：** 偏好对齐
- **PPO/GRPO：** 奖励优化
- **奖励模型：** 训练自定义奖励模型
- 23KB 文档，含完整工作流

#### unsloth — 快速微调
**能做什么：** Unsloth — 2-5 倍加速、50-80% 显存节省
- **优化：** 自定义 Triton kernel 加速
- **LoRA/QLoRA：** 参数高效训练
- **兼容：** 与 HuggingFace 生态兼容
- 1.8MB 参考文档（含 LLM 完整指南）

---

## 📝 Note-taking — 笔记管理

### obsidian — Obsidian 笔记
**能做什么：** 读取、搜索、创建 Obsidian 笔记
- `obsidian read "笔记名"` — 读取笔记
- `obsidian list` — 列出笔记（支持文件夹过滤）
- `obsidian search "关键词"` — 按内容搜索
- 支持 Markdown 格式

---

## 📦 OpenClaw — AI 网关部署

### openclaw-deploy — 从零部署
**能做什么：** OpenClaw 在 Linux 服务器上的完整部署指南
- **环境准备：** nvm → Node.js v22 → npm
- **安装：** npm install openclaw
- **配置：** 模型 API、飞书集成、systemd 服务
- **验证：** 多维度验证部署成功
- 分阶段部署流程，每步有验证命令

### openclaw-upgrade-502-fix — 升级运维
**能做什么：** OpenClaw 升级和故障排查
- **升级 SOP：** 备份 → 停服 → 升级 → 配置检查 → 重启
- **502 排查：** 包丢失 / 插件不兼容 / systemd 版本不一致
- **应急回滚：** 快速恢复到上一个稳定版本
- **日常运维：** 日志查看、定期清理、配置审计
- **关键坑点：** bonjour 插件、配置校验、systemd user session

---

## 💼 Productivity — 生产力工具

### google-workspace — Google 全家桶
**能做什么：** Gmail、Calendar、Drive、Contacts、Sheets、Docs 集成
- **Gmail：** 搜索邮件、读取内容、发送邮件
- **Calendar：** 查看/创建事件
- **Drive：** 文件上传/下载/搜索
- **Sheets：** 读写表格数据
- **Docs：** 创建和编辑文档
- **OAuth2：** Hermes 管理的认证流程
- 包含 `google_api.py`、`gws_bridge.py`、`setup.py` 脚本

### linear — 项目管理
**能做什么：** Linear API 管理 Issue 和项目
- **Issue 管理：** 创建、更新、搜索、关闭
- **项目组织：** 团队、项目、里程碑
- **GraphQL API：** 完整的查询和变更
- **工作流状态：** Backlog → Todo → In Progress → Done
- API Key 认证，无需 OAuth

### maps — 地图和位置
**能做什么：** 基于 OpenStreetMap 的位置智能服务
- **地理编码：** 地址 → 坐标 / 坐标 → 地址
- **附近搜索：** 46 种 POI 类别
- **路线规划：** 驾车/步行/骑行导航
- **时区查询：** 坐标 → 时区
- **边界框：** 获取地点的边界范围
- 包含 `maps_client.py`（46KB Python 脚本）

### nano-pdf — PDF 编辑
**能做什么：** 用自然语言指令编辑 PDF
- `nano-pdf edit input.pdf "把第一页标题改成新标题"` — 修改文字
- `nano-pdf edit input.pdf "修复第 3 页的拼写错误"` — 修正错误
- `nano-pdf edit input.pdf "更新日期为 2026-05-01"` — 更新内容
- 支持页面级别的精确编辑

### notion — Notion API
**能做什么：** 通过 API 管理 Notion 页面和数据库
- **页面：** 创建、更新、查询
- **数据库：** 创建数据库、添加条目、查询过滤
- **Block：** 添加段落、列表、代码块等
- **搜索：** 全文搜索工作空间
- 2025-09-03 API 版本特性说明

### ocr-and-documents — PDF/文档提取
**能做什么：** 从 PDF 和扫描文档提取文字
- **远程 URL：** 使用 web_extract
- **本地 PDF：** pymupdf（轻量）或 marker-pdf（高质量 OCR）
- **Arxiv 论文：** 快速提取摘要或全文
- **DOCX：** python-docx
- 包含 `extract_marker.py` 和 `extract_pymupdf.py` 脚本

### opc-battle-system — OPC 超级作战系统
**能做什么：** 一人公司自动化工作流系统
- **核心架构：** 飞书 CLI + Hermes Agent 自动化
- **工作流：** 早简报、线索归档、会议转任务、每日复盘
- **系统位置：** `/root/opc-system/`
- **3 个工程原则：** 命令可重复、输出结构化、错误可追踪
- 包含命令封装脚本和 prompt 模板

### powerpoint — PPT 制作
**能做什么：** 完整的 PowerPoint 操作（1MB 资源）
- **读取：** 提取文字、视觉概览、原始 XML
- **编辑：** 修改文字、修复错别字、更新内容
- **创建：** 从零创建演示文稿
- **脚本：** `add_slide.py`（添加幻灯片）、`clean.py`（清理）
- **Office 助手：** merge_runs（合并文本）、simplify_redlines（简化红线）
- **XSD Schema：** 完整的 Office Open XML Schema（ISO-IEC 29500）
- 50 个文件，覆盖 PPT 的所有操作

### side-hustle-exploration — 副业探索
**能做什么：** 帮助用户克服分析瘫痪，从"太多想法"到"开始行动"
- **核心方法：** 低成本启动、快速验证、迭代优化
- **常见陷阱：** 过度分析、完美主义、方向选择困难
- **成功指标：** 是否有具体行动、是否验证了假设
- 适合职业转型、副业探索阶段

---

## 🔴 Red-teaming — 安全测试

### godmode — LLM 越狱测试
**能做什么：** G0DM0D3 越狱技术 — 安全测试 LLM 防护
- **Parseltongue：** 33 种输入混淆技术
- **GODMODE CLASSIC：** 系统提示模板
- **ULTRAPLINIAN：** 多模型竞赛
- **编码升级：** 编码混淆攻击
- **自动越狱：** 自动检测模型并执行越狱
- **脚本：** `auto_jailbreak.py`、`godmode_race.py`、`parseltongue.py`
- 116KB 详细文档

---

## 🔬 Research — 学术研究

### arxiv — 学术论文搜索
**能做什么：** arXiv 免费 REST API 搜索和下载
- **搜索：** 关键词、作者、分类、ID
- **语法：** AND/OR/NOT、精确短语、字段限定
- **输出：** 标题、摘要、作者、日期、PDF 链接
- 配合 `ocr-and-documents` skill 阅读论文全文
- 包含 `search_arxiv.py` 脚本

### blogwatcher — 博客/RSS 监控
**能做什么：** 监控博客和 RSS/Atom 订阅源
- **添加源：** 添加博客 URL，自动发现 RSS
- **扫描更新：** 定期检查新文章
- **跟踪状态：** 已读/未读管理
- **分类过滤：** 按类别筛选
- 通过 blogwatcher-cli Docker 容器运行

### llm-wiki — LLM 知识库
**能做什么：** Karpathy 的 LLM Wiki — 持久化 Markdown 知识库
- **三层架构：** 摄取 → 编译 → 查询
- **摄取：** 从来源提取知识
- **编译：** 构建互联的 Markdown 知识网络
- **查询：** 从知识库中检索信息
- **一致性检查：** Lint 知识库一致性
- 适合构建个人研究笔记、项目知识库

### polymarket — 预测市场数据
**能做什么：** Polymarket 预测市场数据查询
- **搜索市场：** 关键词搜索预测市场
- **价格/概率：** 获取当前市场价格
- **订单簿：** 查看买卖盘
- **价格历史：** 查看价格变化趋势
- 只读 API，无需 Key
- 包含 `polymarket.py` 脚本

### research-paper-writing — 学术论文写作
**能做什么：** ML/AI 学术论文端到端写作管线（1.3MB 资源）
- **覆盖会议：** NeurIPS、ICML、ICLR、ACL、AAAI、COLM
- **阶段：** 文献综述 → 实验设计 → 分析 → 起草 → 修改 → 提交
- **模板：** LaTeX 模板（AAAI、ACL、COLM、ICLR、ICML、NeurIPS）
- **参考文档：** 自动推理方法、检查清单、引用工作流、实验模式、人类评估、论文类型、审稿人指南、来源、写作指南
- 55 个文件，最完整的学术写作资源

---

## 🏠 Smart Home — 智能家居

### openhue — Philips Hue 灯光控制
**能做什么：** 通过 OpenHue CLI 控制 Philips Hue
- **灯光：** 开关、亮度（0-100）、颜色、色温
- **房间：** 按房间控制灯光组
- **场景：** 激活预设场景
- **发现：** 自动发现 Hue Bridge 和灯光

---

## 📱 Social Media — 社交媒体

### xitter — X/Twitter (x-cli)
**能做什么：** 通过 x-cli 操作 X/Twitter
- **发帖：** 发推、回复、引用
- **时间线：** 查看主页、用户时间线
- **搜索：** 关键词搜索推文
- **互动：** 点赞、转推、书签
- **用户：** 用户信息查询
- 需要 X API 凭证

### xurl — X/Twitter 官方 API CLI
**能做什么：** 通过 xurl（X 官方 API CLI）操作 Twitter
- **完整功能：** 发帖、回复、引用、搜索、时间线、提及、点赞、转推、书签、关注、DM、媒体上传
- **原始 API：** 直接调用 v2 端点
- **安装方式：** Shell 脚本、Homebrew、npm、Go
- 比 xitter 功能更全面

---

## 💻 Software Development — 软件开发

### plan — 计划模式
**能做什么：** Hermes 计划模式 — 只写计划不执行
- 检查项目上下文
- 生成 Markdown 计划文档
- 保存到 `.hermes/plans/` 目录
- 交互风格：只规划，不执行

### requesting-code-review — 代码审查请求
**能做什么：** 提交前代码验证流水线
- **Step 1：** 获取 diff
- **Step 2：** 静态安全扫描（密钥、Shell 注入、eval/exec、反序列化）
- **Step 3：** 代码质量检查
- **Step 4：** 独立审查子代理
- **Step 5：** 自动修复循环

### subagent-driven-development — 子代理驱动开发
**能做什么：** 使用独立子代理执行实现计划
- **流程：** 读取计划 → 创建 todo → 分派任务 → 两阶段审查 → 合并
- **审查：** 规范合规性 → 代码质量
- **并行：** 独立任务并行执行
- 适合大型功能实现

### systematic-debugging — 系统化调试
**能做什么：** 4 阶段根因调查 — 先理解问题再修复
- **铁律：** 不理解问题就不修复
- **阶段 1：** 根因调查（运行失败测试、检查日志、二分定位）
- **阶段 2：** 假设验证
- **阶段 3：** 修复实施
- **阶段 4：** 回归预防

### test-driven-development — 测试驱动开发
**能做什么：** RED-GREEN-REFACTOR 循环
- **铁律：** 先写测试再写实现
- **RED：** 写失败测试
- **GREEN：** 写最少代码通过测试
- **REFACTOR：** 重构代码保持测试通过
- 每次修改后运行全部测试检查回归

### writing-plans — 实现计划编写
**能做什么：** 多步骤任务的实现计划
- **任务粒度：** 每个任务 15-30 分钟可完成
- **计划结构：** 概述 → 任务列表 → 每个任务的详细步骤和代码
- **包含：** 确切文件路径、完整代码示例、验证步骤
- 适合有规格说明或需求文档的场景

---

## 🐛 Dogfood — Web 应用 QA 测试

### dogfood — 探索式 QA 测试
**能做什么：** 系统化的 Web 应用探索式测试
- **工作流：** 侦察 → 探索 → 深度测试 → 报告
- **工具：** 浏览器快照、点击、输入、截图
- **输出：** 结构化测试报告（Markdown）
- **分类：** Bug、UX 问题、性能问题、安全隐患
- 包含报告模板和 issue 分类参考

---

## 📦 使用方法

### 安装单个 Skill

```bash
# 克隆仓库
git clone https://github.com/wszz117/hermes-skills.git

# 复制需要的 skill 到 Hermes skills 目录
cp -r hermes-skills/dogfood ~/.hermes/skills/
cp -r hermes-skills/openclaw-deploy ~/.hermes/skills/
```

### 安装整个分类

```bash
# 安装所有 GitHub 相关 skills
cp -r hermes-skills/github/* ~/.hermes/skills/github/

# 安装所有创意工具
cp -r hermes-skills/creative/* ~/.hermes/skills/creative/
```

### Skill 目录结构

```
~/.hermes/skills/
├── skill-name/
│   ├── SKILL.md          # 主技能文档（必须）
│   ├── references/       # 参考文档
│   ├── templates/        # 模板文件
│   ├── scripts/          # 辅助脚本
│   └── assets/           # 资源文件
```

---

## 📊 统计

| 分类 | Skills 数 | 文件数 | 大小 |
|------|----------|--------|------|
| 🍎 Apple | 4 | 5 | 11KB |
| 🤖 Autonomous AI Agents | 4 | 5 | 72KB |
| 🎨 Creative | 12 | 200 | 1.7MB |
| 📊 Data Science | 1 | 2 | 6KB |
| 🔧 DevOps | 1 | 1 | 7KB |
| 📧 Email | 1 | 4 | 14KB |
| 🎮 Gaming | 2 | 3 | 15KB |
| 🐙 GitHub | 7 | 18 | 87KB |
| 📍 Leisure | 1 | 2 | 10KB |
| 🔌 MCP | 2 | 3 | 16KB |
| 🎵 Media | 4 | 7 | 20KB |
| 🧠 MLOps | 21 | 91 | 3.3MB |
| 📝 Note-taking | 1 | 2 | 1KB |
| 📦 OpenClaw | 2 | 2 | 16KB |
| 💼 Productivity | 9 | 68 | 1.1MB |
| 🔴 Red-teaming | 1 | 9 | 117KB |
| 🔬 Research | 5 | 63 | 1.4MB |
| 🏠 Smart Home | 1 | 2 | 3KB |
| 📱 Social Media | 2 | 3 | 20KB |
| 💻 Software Development | 6 | 6 | 47KB |
| 🐛 Dogfood | 1 | 3 | 11KB |
| **总计** | **89** | **502** | **~8MB** |

---

*文档生成时间: 2026-05-01*
*仓库: https://github.com/wszz117/hermes-skills*
