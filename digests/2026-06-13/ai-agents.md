# OpenClaw 生态日报 2026-06-13

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-13 03:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

非常好，以下是根据 OpenClaw (github.com/openclaw/openclaw) 提供的 GitHub 数据生成的 2026 年 6 月 13 日项目动态日报。

---

# OpenClaw 项目动态日报 (2026-06-13)

## 1. 今日速览

过去 24 小时，OpenClaw 项目处于高度活跃状态，共更新 **500 条 Issues**（新开/活跃 410 条，关闭 90 条）和 **500 条 PR**（待合并 356 条，已合并/关闭 144 条）。社区参与度和开发工程量均处于峰值。

- **安全：** 发布了 v2026.6.6 双版本，针对 Transcript、Sandbox、MCP、Codex 等超十个模块进行了大规模安全边界加固。
- **健康度：** 尽管修复进展迅速，但项目面临显著的稳定性压力。**2 个 P0 级 Bug**（内存泄漏 #91588、记忆搜索损坏 #91778）尚未解决，多个 P1 级会话上下文混乱及消息丢失问题正在审查。

## 2. 版本发布

### v2026.6.6 (稳定版) 与 v2026.6.6-beta.2
- **核心更新：** 全面收紧安全边界。
- **详细范围：** 修复涉及 Transcripts（转录记录）、沙箱绑定 (Sandbox Binds)、宿主环境继承、MCP Stdio 协议、Codex HTTP 访问、原生搜索策略、增强的发送者检查、已删除 Agent 的 ACP 绕过、回环工具 (Loopback Tools)、Discord 审核、Teams 群组操作以及 Exec 执行环境。
- **破坏性变更：** 未明确提及破坏性变更，但安全策略的大幅收紧必然影响自定义脚本和集成方案。建议用户在升级前阅读完整更新日志。
- **迁移建议：** 强烈建议所有用户立即升级。

## 3. 项目进展

### 已合并/关闭的高价值 PR
- **🔒 `#76322` [Security]：** 修复了 Bootstrap Token 路径的 DoS 攻击风险。为启动令牌路径增加了速率限制和失败锁定机制，解决了无有效 token 时的无限串行攻击问题。
- **🤖 `#88446` [Feat]：** Codex 聊天计划控制。为 Codex 对话新增了原生 `/codex plan` 控制能力，包括规划模式偏好持久化。
- **🐛 `#71491` [Fix]：** 修复了 Kimi K2.6 模型在长对话上下文压缩后出现的 `reasoning_content is missing` 400 错误。
- **🐛 `#75378` [Fix]：** 修复了并行生成 3 个子代理导致 Gateway 事件循环饱和及 1012 服务重启的问题。
- **🐛 `#66561` [Fix]：** 修复了 OpenAI Codex SSE 流提前中止后，OpenClaw 将其错误显示为 408 超时的问题。

### 重要在途 PR (待合并)
- **🧠 `#91632` [Feat]：** 新增工具搜索目录模式 (`toolSearch.mode: "directory"`)，允许大型工具集以更紧凑的方式暴露给 LLM，并支持按需加载工具 schema。
- **🐧 `#92095` [Fix - P1]：** 修复 WhatsApp 登录状态持久化问题，防止 Docker 重建或升级后强制要求重新链接设备。
- **🔑 `#92584` [Fix - Security]：** 阻止控制 UI Token 通过 URL Query String (`?token=`) 传递，消除 Secret 泄露风险。
- **📊 `#92580` [Fix]：** 修复独立 Cron 任务的交付目标持久化问题，解决 `Channel is required` 错误。
- **🎨 `#89820-89827` [Web-UI]：** 贡献者 BunsDev 提交了一系列 UI/UX 优化，包括移动端适配、消息工具栏、设计系统文档及无障碍修复。

## 4. 社区热点

- **🔍 `#25592` [P1, Security] —— 工具调用间文本泄漏 (32 条评论)**
  目前讨论最激烈的 Issue。当 Agent 在两次工具调用之间产生中间文本（如错误处理、加工确认、旁白）时，这些文本会被错误地路由到 Slack / iMessage 等外部消息渠道，造成严重安全和 UX 问题。被标记为“钻石龙虾”级影响力。

- **📱 `#9443` [P2, Enhancement] —— 请求预构建 Android APK (25 条评论)**
  用户强烈建议官方在 GitHub Releases 中提供预编译好的 Android 配套应用 APK，而不是让用户每次自己从源码编译，以降低移动端部署门槛。

- **⚡ `#18160` [P2, Enhancement] —— Cron 任务直执行模式 (👍11)**
  获得今日赞同数最多的 Feature Request。用户期望 Cron 任务支持直接执行系统命令（`Direct Exec Mode`），而不是强制走 LLM 的 `agentTurn`，以减少 API 消耗、延迟和提高可靠性。

- **🖥️ `#32473` [P1, Regression] —— 控制 UI 强制要求 HTTPS/设备身份 (17 条评论, 👍5)**
  用户反映在 Hostinger VPS 或 Docker 环境下配置后，控制 UI 强制要求 HTTPS 或 localhost 安全上下文，导致无法正常使用，影响范围较广。

## 5. Bug 与稳定性

| 严重程度 | ID | 标题摘要 | 当前状态 | 关联修复 PR |
|---|---|---|---|---|
| 🔴 **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏：RSS 从 350MB 涨至 15.5GB 导致 OOM 崩溃 | 待维护者审查 | 无 |
| 🔴 **P0** | [#91778](https://github.com/openclaw/openclaw/issues/91778) | `memory_search` 索引元数据丢失 (v2026.6.1 起) | 等待实机复现 | 无 |
| 🟠 **P1** | [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用间文本泄漏到外部消息频道 (安全/消息丢失) | 待安全/产品决策 | 链接 PR 开启 |
| 🟠 **P1** | [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal Daemon 重启竞态条件导致孤儿进程和发送失败 | 待链接 PR | 链接 PR 开启 |
| 🟠 **P1** | [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent 回复上一条消息 (会话上下文混乱) | 待产品决策/复现 | 无 |
| 🟠 **P1** | [#29387](https://github.com/openclaw/openclaw/issues/29387) | agentDir 中的 Bootstrap 文件被静默忽略 | 待维护者审查 | 无 |
| 🟠 **P1** | [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` 工具不继承技能环境变量 (回归) | 待产品/安全决策 | 无 |
| 🟠 **P1** | [#74484](https://github.com/openclaw/openclaw/issues/74484) | Gateway 配对作用域死锁 (CLI 无法 approve/reject) | 待讨论 | 无 |
| 🟠 **P1** | [#88951](https://github.com/openclaw/openclaw/issues/88951) | 升级后消息内容重复 2-4 次 | 待维护者审查 | 无 |
| 🟠 **P1** | [#38327](https://github.com/openclaw/openclaw/issues/38327) | `google-vertex/gemini` 报 `Cannot convert undefined or null to object` | 等待实机复现 | 无 |

## 6. 功能请求与路线图信号

### 高热度功能需求
- **Cron 直执行模式 (`#18160`)：** 社区强烈呼吁改变 Cron 强制走 LLM 的设计，以节省 Token 和提高可靠性，但卡在 `needs-product-decision`。
- **Exec Approvals 黑名单 (`#6615`)：** 用户希望实施“允许一切，仅阻止特定命令”的精细化安全策略（👍7）。
- **Slack Block Kit 支持 (`#12602`)：** 提升 Agent 在 Slack 中的消息交互丰富度和结构化能力。
- **Telegram 商业版支持 (`#20786`)：** 扩展 Telegram 渠道对企业功能的支持（👍6）。
- **记忆 / 会话自动保留 (`#40418`)：** 执行 `/new` 时自动保留并合成对话历史，实现跨会话学习。

### 路线图信号
- 大量高赞功能请求处于 `needs-product-decision` 的积压状态，显示项目团队当前重心在稳定性和安全性。
- **新 PR `#91632` (工具搜索目录模式) 与 `#92499` (QMD mcporter 隔离)** 暗示未来可能在「工具管理» 和 «记忆架构» 上实施重大重构。

## 7. 用户反馈摘要

- **稳定性痛点：** “Gateway 运行 2-3 天后 RSS 从 350 MB 暴涨到 15.5 GB，直接被 OOM killer 杀掉然后无限重启。” (#91588) “升级到 5.27 后消息重复问题依旧存在，严重影响使用。” (#88951)
- **配置与兼容性抱怨：** “在 VPS 上用 Docker 部署，配置完 Brave 密钥后始终报 `control ui requires device identity`，完全无解。” (#32473) “在 Agent 目录下放 SOUL.md 完全没效果，最后发现它根本不读这个目录。” (#29387)
- **安全焦虑：** “Agent 处理请求时内部日志居然发到了 Slack 频道里，这个信息泄漏风险太大了。” (#25592)
- **功能遗憾：** “Cron 任务单纯跑个脚本也要走 LLM，既浪费又容易超时，能不能有直接执行模式？” (#18160) “为什么官方不发一个编译好的 APK，自己折腾安卓环境太累了。” (#9443)

## 8. 待处理积压

### 产品决策阻塞 (`needs-product-decision`)
- **分层引导文件加载 (`#22438`)**：17 条评论，用户期望渐进式加载 Bootstrap 文件以节省 Token。
- **预响应强制执行钩子 (`#13583`)**：11 条评论，高频交易/安全场景的硬性需求。
- **子代理完成扩展钩子 (`#22358`)**：12 条评论，用于生成 Trajectory 文件。

### 安全审查阻塞 (`needs-security-review`)
- **原生密钥管理集成 (`#13610`)**：7 条评论，解决将 API 密钥明文存储在配置文件中的风险。
- **暴露 Tool Call 前后钩子 (`#13364`)**：7 条评论，希望能在 Managed Hook 中拦截/审核 Tool 调用。

### 等待维护者介入的关键 Bug (`needs-maintainer-review`)
- **`#91588` 严重内存泄漏 (P0)：** 应是当前最高优先级的维护任务。
- **`#57326` CLI 分发绕过 (P1)：** 部分辅助路径仍绕过 CLI 代理走向嵌入式 API。
- **`#37634` 沙箱工作区只读 (P1)：** 在开启隔离模式后，工具无法在沙箱内写入文件。

---

## 横向生态对比

好的，以下是根据您提供的各项目社区动态摘要生成的横向对比分析报告。

---

## 横向对比分析报告：个人 AI 助手与自主智能体开源生态（2026-06-13）

### 1. 生态全景

今日，个人 AI 助手/自主智能体开源生态呈现出 **高度活跃但分化加剧** 的态势。以 OpenClaw、IronClaw 为代表的头部项目每天处理数百个协作项，正承受功能快速膨胀与稳定性债务的双重压力；中等规模项目（NanoBot、PicoClaw、CoPaw）则以架构重构与安全加固为重心，迈向工程成熟期。社区关注点从“能否对话”全面转向 **生产级可靠性**：上下文记忆一致、沙箱隔离、可观测性、成本透明成为跨项目共同议题。总体而言，生态正处于从“原型验证”向“企业就绪”跨越的关键阶段，领先项目之间在稳定性上的差异正逐渐成为核心竞争力分水岭。

### 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.6.6 / beta | 高度活跃，稳定性承压（P0 Bug 未解） |
| **NanoBot** | 3（新增） | 29 | 无 | 良好，审查带宽紧张 |
| **Hermes Agent** | 50 | 50 | 无 | 密集迭代，PR 积压严重 |
| **PicoClaw** | 6 | 14 | Nightly v0.2.9-nightly | 极佳，架构重构交付 |
| **NanoClaw** | 5 | 18 | 无 | 良好，从扩展步入稳定深水区 |
| **NullClaw** | 1 | 3（开放） | 无 | 良好，进展缓慢 |
| **IronClaw** | 50 | 50 | 无 | 极高，界面稳定化+核心攻坚 |
| **LobsterAI** | 1 | 17 | 无（发版分支合并） | 优，MVP 功能集成 |
| **TinyClaw** | 0 | 0 | 无 | 停滞 |
| **Moltis** | 3 | 0 | 无 | 中低，需求驱动但开发暂缓 |
| **CoPaw (QwenPaw)** | 21 | 23 | 无（版本号 1.1.12b1） | 向好，架构升级进行中 |
| **ZeptoClaw** | 0 | 0 | 无 | 停滞 |
| **ZeroClaw** | 12 | 36 | 无 | 良好，RFC 驱动迭代快 |

### 3. OpenClaw 在生态中的定位

OpenClaw 在社区规模与功能广度上 **占据绝对主导地位**：单日 500 Issues/PR 的吞吐量（第二梯队约 50）体现了其最大用户基数和贡献者网络。优势在于安全响应速度（同日发布双版本修复超十个模块）和功能覆盖的完备性（MCP、Sandbox、Codex、多渠道等）。但其 **技术路线正承受复杂度反噬**：同一日存在 2 个 P0 级 Bug（内存泄漏 #91588、记忆搜索损坏 #91778）以及 8 个 P1 级严重问题，社区安全感与信心面临考验。相比之下，NanoBot 通过审计模块强化可观测性，PicoClaw 以极简架构维持低缺陷率，CoPaw 通过 Runtime 2.0 解耦工具协调。OpenClaw 的定位是 **“功能最全的个人 AI 中心”**，但若稳健性不能及时跟上，可能为中等规模但更专注的项目提供赶超窗口。

### 4. 共同关注的技术方向

**① 上下文窗口与记忆管理**  
跨项目高频出现，是当前生态最大瓶颈。涉及：  
- **OpenClaw**：记忆搜索索引损坏（#91778）、消息内容重复 2-4 次（#88951）  
- **NanoBot**：短期记忆因系统 prompt 占用上下文而丢失（#4044）、压缩误删助手自身回答（#4307）  
- **Hermes Agent**：输出 token 预算预留机制（#45351，对应长期截断问题 #7237）  
- **CoPaw**：长对话后 Agent 完全无响应（#5161）  
**共性诉求**：提高压缩决策的可控性、保留关键上下文、引入更细粒度的工具输出压缩（如 Hermes #39691 提出的 headroom-ai）。

**② 安全边界与权限最小化**  
- **PicoClaw**：频道级危险操作限制（#3109）及 Telegram 分级控制（#3114）  
- **NanoClaw**：容器 runtime 默认移除 Capability（#2748）、npm 包发布年龄检查（#2749）  
- **OpenClaw**：v2026.6.6 大规模收紧 MCP/Exec/沙箱等安全边界  
- **Moltis**：提案要求 K8s Pod + Kata/gVisor 虚拟机级隔离（#1118）  
- **LobsterAI**：技能停用后仍注入提示词（#1453）  
**共性诉求**：从“默认开放”转向“默认最小权限”，并在渠道、工具调用、代码执行等维度统一策略。

**③ Agent 运行时架构统一**  
- **ZeroClaw**：RFC #7415 计划将三个独立 turn 引擎统一为单一合并 PR（#7540）  
- **CoPaw**：Runtime 2.0 模块化，引入 ToolCoordinator 层（#5078，Breaking Change）  
- **Hermes Agent**：引入输出 token 预留机制来避免截断，实为运行时调度改进（#45351）  
- **NanoClaw**：持久化内存脚手架与能力定义缝（#2745-#2747）  
**共性诉求**：标准化 Agent 内部调度逻辑，分离工具协调与模型交互，为多 provider 及复杂工作流铺路。

### 5. 差异化定位分析

| 项目 | 核心侧重 | 目标用户 | 关键架构特征 |
|---|---|---|---|
| **OpenClaw** | 全栈个人 AI 平台 | 高级用户/社区 | 功能最全，安全加固密集，但复杂度高 |
| **NanoBot** | 开发者工具链 | 应用开发者 | 审计模块、SDK 扩展、TTS 框架，强调可观测性 |
| **Hermes Agent** | 社区驱动快速迭代 | 激进尝鲜用户 | 修复响应极快（同 Bug 多 PR 竞争），但 PR 积压多 |
| **PicoClaw** | 轻量单实例助手 | 个人/家庭用户 | 架构简洁，渠道标识标准化，安全边界刚落地 |
| **NanoClaw** | 后起之秀，安全先行 | 安全敏感用户 | 容器加固、供应链检查，通道生态快速补齐 |
| **NullClaw** | 稳字当头 | 低维护需求用户 | Zig 实现，更新缓慢，但基础可用 |
| **IronClaw** | 界面重写 + 核心攻坚 | 高端生产用户 | Reborn 界面修复批量关闭，附件系统管道构建中 |
| **LobsterAI** | 商业支持 + 前沿功能 | 企业/创新用户 | Computer Use MVP、实时 ASR，发版集中 |
| **CoPaw** | 模块化运行时 | 插件/二次开发用户 | Runtime 2.0 模块化、Agent OS Driver 统一抽象 |
| **ZeroClaw** | RFC 驱动架构演进 | 架构爱好者 | 统一 turn 引擎、CI 门禁，注重设计一致性 |
| **Moltis** | 企业级沙箱探索 | 企业安全团队 | K8s 原生执行提案、本地 STT 需求 |
| **TinyClaw / ZeptoClaw** | 停滞/休眠 | – | 无活动 |

### 6. 社区热度与成熟度

- **第一梯队（极高活跃，>40 协作项）**：**OpenClaw**、**Hermes Agent**、**IronClaw**、**ZeroClaw**。这些项目每日处理事务数十至五百项，但步态迥异：OpenClaw 处于“维护性活跃”，Bug 修复与新功能并行但压力巨大；IronClaw 处在 **界面冲刺期**，同时批量关闭积压 UX 问题；ZeroClaw 以 **架构讨论驱动**，快速响应 RFC 和 S1 Bug 并提交 PR。
- **第二梯队（较高活跃，10-40 项）**：**NanoBot**、**PicoClaw**、**NanoClaw**、**LobsterAI**、**CoPaw**。处于 **质量巩固或功能闭环阶段**：NanoBot 侧重可观测性与 SDK；PicoClaw 与 NanoClaw 在渠道生态和安全上补齐差距；LobsterAI 正在完成重大功能集成；CoPaw 围绕 Runtime 2.0 迁移重整架构。
- **第三梯队（低活跃，<10 项）**：**NullClaw**、**Moltis**。前者开发节奏缓慢但稳定，后者需求讨论超前于代码产出。
- **停滞**：**TinyClaw**、**ZeptoClaw** 无任何活动，可能已暂停维护。

### 7. 值得关注的趋势信号

1. **桌面自动化（Computer Use）成为新爆发点**：LobsterAI 合并了 Computer Use MVP，标志着 AI 智能体从“聊天”向“操作电脑”跨越。预计将拉动更多项目跟进（OpenClaw 已有相关安全加固），并催生对抗性沙箱与 UI grounding 技术需求。

2. **本地模型兼容性仍是广泛痛点**：NullClaw #952（Ollama 输出截断）、ZeroClaw #6723（本地模型超时硬编码）、CoPaw #5163（Gemini 回归）显示，项目对非 OpenAI API 的适配依然脆弱。支持本地部署已成为用户留存的关键杠杆。

3. **成本透明与计量呼声高涨**：NanoBot #4309（Token 用量恒为 0）、OpenClaw #18160（Cron 直执行省 Token）、CoPaw 飞书卡片刷新慢（流式消耗）。随着 AI 调用成本深入人心，内置用量统计、预算控制和“轻量执行模式”将从加分项变为必备项。

4. **渠道统一体验受质疑**：Hermes Agent #45275 要求跨平台会话统一；OpenClaw #32473 控制 UI HTTPS 强制要求；PicoClaw #3114 渠道分级。用户对 **多端割裂感** 容忍度降低，项目需要建立一致的认证、路由和权限框架。

5. **供应链安全成为社区自觉**：NanoClaw #2749（npm 年龄检查）由社区贡献，OpenClaw #92584（阻止 UI Token 通过 URL 传递），ZeroClaw #7537（安装配置脆弱）。开发者已经开始主动填补安全盲区，项目组应顺势制定安全基线文档。

---

*本报告基于各项目 2026-06-13 的 GitHub 公开活动数据，旨在为技术决策者提供生态全景与定位参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目日报（2026-06-13）

## 1. 今日速览
过去 24 小时项目活跃度极高，共 29 个 PR 发生变更（9 个合并/关闭），新增 3 个 Issue。项目重心显著倾斜于 **Agent 基础设施成熟化**（审计模块、TTS 框架、Python SDK 扩展）与 **系统健壮性防御**（上下文窗口修复、MCP 崩溃修复、多项输入校验）。测试体系建设（`yu-xin-c` 主导的多个 test harness）持续积累，显示团队在高频迭代的同时保有对长期工程质量的投入。整体健康度良好，但功能迭代可能正对代码审查带宽造成挤压。

## 2. 版本发布
无。

## 3. 项目进展
昨日共有 **9 个 PR 被合并/关闭**，项目在以下方向取得实质性推进：

- **Agent 可观测性（Audit 模块落地）** —— `bjoshuanoah` 提交的 `feat(audit)` PR 系列（[#4318](https://github.com/HKUDS/nanobot/pulls/4318)、[#4319](https://github.com/HKUDS/nanobot/pulls/4319)）正式合入主分支。该模块为 Agent 工具调用提供完整可观测框架，支持 Loguru、Webhook、JSONL 四种传输层，是 NanoBot 走向企业级部署的关键一步。
- **后台任务可靠性修复** —— `michaelxer` 修复了 Cron 任务通过 `spawn_tool` 孵化子 Agent 后过早标记完成的 Bug（[#4304](https://github.com/HKUDS/nanobot/pulls/4304)），确保异步业务流程完整性。
- **上下文安全与合规** —— 针对 OpenAI/Anthropic 工具调用规范的合规性修复（[#4006](https://github.com/HKUDS/nanobot/issues/4006)、[#4203](https://github.com/HKUDS/nanobot/issues/4203)）已关闭，同时合入了多条防御性编程修复（消息附件校验 [#4312](https://github.com/HKUDS/nanobot/pulls/4312)、文件分页限制 [#4311](https://github.com/HKUDS/nanobot/pulls/4311)、记忆游标单调性 [#4256](https://github.com/HKUDS/nanobot/pulls/4256)）。
- **架构解耦** —— `chengyongru` 将配置模式与工具运行时解耦（[#4314](https://github.com/HKUDS/nanobot/pulls/4314)），对模块化编译与依赖优化意义积极。

## 4. 社区热点

- **短期记忆丢失（[#4044](https://github.com/HKUDS/nanobot/issues/4044)）** —— 获 5 条评论，是目前社区最聚焦的议题。用户 `bjoshuanoah` 并非单纯报 Bug，而是给出深度根因分析：系统 prompt（SOUL.md、USER.md、MEMORY.md）占用大量上下文窗口空间（Context Window Pressure），导致 Agent 在单轮交互中丢失即时记忆。已超出单一修复范畴，进入架构设计层面。
- **API 用量透明性（[#4309](https://github.com/HKUDS/nanobot/issues/4309)）** —— 昨日新提 Issue，指出 `/v1/chat/completions` 端点 `usage` 字段始终返回 0 Token。直接触及 API 重度用户对计量、限流的底层依赖，预期将引发快速跟进。
- **功能兴趣点** —— TTS 功能（[#4316](https://github.com/HKUDS/nanobot/pulls/4316)）、WhatsApp 提及能力（[#4317](https://github.com/HKUDS/nanobot/pulls/4317)）等 PR 热度较高，反映出社区已从基础对话走向多模态与渠道增强。

## 5. Bug 与稳定性

按严重程度排列：

- **严重 - API 行为异常**：[#4309](https://github.com/HKUDS/nanobot/issues/4309) Token 用量恒为 0。已确认社区核心功能存在计量回归，当前无关联修复 PR，需维护者优先定位。
- **严重 - 上下文压缩导致消息丢失**：[#4307](https://github.com/HKUDS/nanobot/issues/4307) 当 `context_window_tokens` 设置过低时，长轮次压缩（Consolidation）会误删 Agent 自身的回答消息，导致用户后续引用断裂。
- **高 - 短期记忆系统性衰退**：[#4044](https://github.com/HKUDS/nanobot/issues/4044) 持续开放，社区深度分析指向上下文窗口管理架构性瓶颈。
- **中 - MCP 协议崩溃**：[#4303](https://github.com/HKUDS/nanobot/pulls/4303) 修复了 `streamableHttp` 模式下服务器重连时的异步取消作用域崩溃（`RuntimeError`），目前仍为开放审查状态。
- **安全性 - 符号链接逃逸**：[#4119](https://github.com/HKUDS/nanobot/pulls/4119)（5 月 31 日提交）限制受限 exec 通过相对路径符号链接逃离工作区。长期未合入，但属于防御纵深的关键一环。

整体看，项目防御性编程正在快速做强，但功能性回归（#4309）和架构性 Bug（#4044）仍是隐患。

## 6. 功能请求与路线图信号

- **多模态扩展信号（TTS）**：[#4316](https://github.com/HKUDS/nanobot/pulls/4316) 引入官方 TTS 配置系统（OpenAI、Groq/Orpheus、ElevenLabs），配合 agent-facing 文档说明，暗示 Agent 将具备主动语音输出能力。此功能一旦合入，将显著扩展 NanoBot 在语音助手领域的应用面。
- **WebUI 与 Config 同步**：[#4313](https://github.com/HKUDS/nanobot/pulls/4313) 大幅弥合了 WebUI 设置面板与 `config.json` 之间的双向写入差距（temperature、tool limits、memory fields 等），强化了非命令行操作体验，降低使用门槛。
- **SDK 开发者体验升级**：[#4296](https://github.com/HKUDS/nanobot/pulls/4296) 从单行的 `bot.run()` 扩展到完整的 `RunResult`、session/memory/runtime 控制，暗示项目正在布局应用层生态。
- **路线图空白地带**：用户 `smurfix` 在 [#4305](https://github.com/HKUDS/nanobot/issues/4305)（已关闭）中请求多自定义 Provider。虽关闭但反映社区对 Provider 灵活性的潜在期待，可考虑纳入未来路线图评估。

## 7. 用户反馈摘要

- **深度诊断型贡献**：`bjoshuanoah` 在 #4044 中提供完整的内存丢失场景再现与根因分析（Context Window Pressure），属高价值社区技术分析。
- **代码级贡献**：`huji820` 在 #4203 中精确锁定 `find_legal_message_start` 在孤立工具结果场景下的逻辑缺陷（返回列表长度而非正确索引），极大降低了维护者的排查成本。
- **透明计量诉求**：`alx1379` 在 #4309 中反映 Token 用量恒为零，代表了通过 API 做计费、监控的 B 端用户的声音。
- **情绪基调**：随着 TTS、WebUI 同步等新功能贡献涌入，社区正向情绪上升；但 #4047 / #4044 等上下文相关问题的长期未决，可能在重度用户群体中积累失望。

## 8. 待处理积压

- **核心测试与安全 PR 积压严重**：社区核心贡献者 `yu-xin-c` 自 **5 月 24 日**起连续提交的大批测试与安全修复 PR（[#3982](https://github.com/HKUDS/nanobot/pulls/3982)、[#3983](https://github.com/HKUDS/nanobot/pulls/3983)、[#4053](https://github.com/HKUDS/nanobot/pulls/4053)、[#4119](https://github.com/HKUDS/nanobot/pulls/4119)、[#4193](https://github.com/HKUDS/nanobot/pulls/4193)、[#4256](https://github.com/HKUDS/nanobot/pulls/4256)）至今仍为开放状态。这批 PR 覆盖了 Runner 线束、Agent 生命周期、文件系统安全、记忆游标等关键子系统的长期测试保障。**近期功能（TTS、Audit、WebUI）的密集开发严重占用了审查资源，建议维护者在下周协调专项 Review 时间窗口，优先消化这批积压，避免质量债务累积到不可收拾的程度。**
- **架构性 Issue 悬置**：[#4044](https://github.com/HKUDS/nanobot/issues/4044)（短期记忆）自 5 月 28 日提出以来已逾半月，社区期望看到团队是否将其纳入迭代路线图，并评估是否需要引入 Prompt Compression 或改进滑动窗口机制。当前沉默本身也是一种风险信号。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent GitHub 数据生成的 2026-06-13 项目动态日报。

---

## Hermes Agent 项目日报 | 2026-06-13

### 1. 今日速览

Hermes Agent 项目今日保持高度活跃，24小时内共产生/更新 **50 个 Issue** 和 **50 个 PR**，其中 **3 个 PR 被合并/关闭**、**2 个 Issue 关闭**、**47 个 PR** 仍在待审核/合并状态。社区贡献者响应极其迅速，针对 `notify_on_complete` 刷屏问题（#45352）甚至涌现了 **3 个并行的修复方案**。经典 Bug “输出长度限制截断”（#7237）终于关闭，项目在上下文管理上迈出重要一步。整体来看，项目处于密集的迭代修复期，社区参与度极高，但 PR 积压数量（47）与部分旧 Issue 无人认领的情况需警惕。

### 2. 版本发布

*暂无新版本发布。*

### 3. 项目进展

今日无重大版本发布，但项目在 Bug 修复与稳定性的推进上非常扎实。主要进展体现在以下集群：

- **Bug 修复集群（notify_on_complete）**：针对 Issue #45352（`[IMPORTANT: ...]` 消息在后台进程失败时仍推送到对话），社区在几小时内提交了 3 个不同的修复 PR（[#45366](https://github.com/NousResearch/hermes-agent/pull/45366)、[#45359](https://github.com/NousResearch/hermes-agent/pull/45359)、[#45357](https://github.com/NousResearch/hermes-agent/pull/45357)），体现了极高的社区治理效率。
- **Cron 子系统修复**：PR [#45350](https://github.com/NousResearch/hermes-agent/pull/45350) 为所有 cron 子命令添加了 `--profile` 标志，修复了 `cron edit --profile` 返回 "Job not found" 的 Bug（#45335）。
- **Docker 网关权限修复**：PR [#45346](https://github.com/NousResearch/hermes-agent/pull/45346) 修复了 Issue #45258 中 `mkdir -p` 创建父目录权限为 root 导致后续容器无法写入日志的 Bug。
- **长输出稳定性修复**：PR [#45351](https://github.com/NousResearch/hermes-agent/pull/45351) 引入了“输出 token 预算预留”机制，在压缩上下文时主动保留响应所需的 token 空间，从根源上缓解了类 #7237 的长度截断问题。
- **其他修复**：PR [#45364](https://github.com/NousResearch/hermes-agent/pull/45364) 修复了某些第三方 Provider 因接收 `reasoning_content` 字段而报错的问题；PR [#45345](https://github.com/NousResearch/hermes-agent/pull/45345) 修复了会话消息计数字段为 NULL 时引发的异常；PR [#45353](https://github.com/NousResearch/hermes-agent/pull/45353) 修复了微信网关断开时的消息确认问题；PR [#45349](https://github.com/NousResearch/hermes-agent/pull/45349) 恢复了 Dashboard 启动时自动显示上一次聊天的功能。

### 4. 社区热点

1.  **Issue #7237（已关闭） - 输出长度截断**：
    - 以 **41 条评论**成为本日评论数最高的议题，并被用户投票 **5 个 👍**。
    - [分析]：该 Bug 在社区中存在已久，被标记为 P3 严重度但影响面极广。本次关闭伴随着上下文管理修复方案的出现，是项目在 Agent 稳定性上的重大胜利。
    - [链接](https://github.com/NousResearch/hermes-agent/issues/7237)

2.  **Issue #45352（P2） - notify_on_complete 误报**：
    - 尽管只产生了 1 条评论，但在几小时内引发了 **3 个修复 PR** 的竞争性提交（这在该项目历史上非常罕见）。
    - [分析]：这表明运行自动化工作流的用户对“后台进程失败/被杀仍通知”的行为模式有强烈抵触。社区对“只通知成功”还是“同时通知成功与失败”的讨论达成了高度共识。
    - [链接](https://github.com/NousResearch/hermes-agent/issues/45352)

3.  **Issue #39691（Feature, P3, 6👍） - 集成 headroom-ai 进行工具输出压缩**：
    - 截至目前获得 **6 个点赞**，是所有展示 Issue 中点赞数最高的功能请求。
    - [分析]：社区用户对当前基于 LLM 的粗放式上下文压缩方式不满意，希望引入更细粒度的工具调用输出压缩方案，以节省 token 并提升 Agent 决策质量。
    - [链接](https://github.com/NousResearch/hermes-agent/issues/39691)

### 5. Bug 与稳定性

**高风险（P2）且已有修复 PR 跟进：**
- [#45352](https://github.com/NousResearch/hermes-agent/issues/45352) 后台进程退出通知刷屏 -> 修复 PR： [#45366](https://github.com/NousResearch/hermes-agent/pull/45366) / [#45359](https://github.com/NousResearch/hermes-agent/pull/45359) / [#45357](https://github.com/NousResearch/hermes-agent/pull/45357)
- [#45335](https://github.com/NousResearch/hermes-agent/issues/45335) Cron 编辑 Profile 不生效 -> 修复 PR： [#45350](https://github.com/NousResearch/hermes-agent/pull/45350)
- [#45258](https://github.com/NousResearch/hermes-agent/issues/45258) Docker 日志目录权限问题 -> 修复 PR： [#45346](https://github.com/NousResearch/hermes-agent/pull/45346)

**高风险（P2）且暂未出现修复 PR：**
- **Provider 兼容性**：
  - [#17199](https://github.com/NousResearch/hermes-agent/issues/17199) DeepSeek Provider 模型名归一化错误，导致 Volcengine ARK 等自定义端点不可用。
  - [#44976](https://github.com/NousResearch/hermes-agent/issues/44976) MiniMax Provider 嵌套数组传参坍塌（MiniMax-M3）。
  - [#45250](https://github.com/NousResearch/hermes-agent/issues/45250) Anthropic OAuth 登录流程因 Token 端点过期导致 404 错误。
- **网关平台**：
  - [#18646](https://github.com/NousResearch/hermes-agent/issues/18646) WhatsApp 群组目标路由错误，消息发送到私聊而非群组。
  - [#45323](https://github.com/NousResearch/hermes-agent/issues/45323) Telegram 富文本表格被统一格式化器改写为列表。
  - [#45308](https://github.com/NousResearch/hermes-agent/issues/45308) BlueBubbles Webhook 在 IPv6 环境下发送异常。
- **桌面端/CLI**：
  - [#26264](https://github.com/NousResearch/hermes-agent/issues/26264) Dashboard Resume 在显式网络绑定时显示 Session 已结束。
  - [#45226](https://github.com/NousResearch/hermes-agent/issues/45226) Windows 桌面端因 GPU 进程崩溃导致反复闪退。
- **工具**：
  - [#44763](https://github.com/NousResearch/hermes-agent/issues/44763) macOS 下 Computer Use 工具的 AX/SOM 元素边界始终为零，导致空间定位失效。

**中等风险（P3）Bug：**
- [#45328](https://github.com/NousResearch/hermes-agent/issues/45328) 异步客户端关闭未 await 产生警告。
- [#45307](https://github.com/NousResearch/hermes-agent/issues/45307) Skill 管理工具中 `_find_skill()` 路径解析错误。
- [#45303](https://github.com/NousResearch/hermes-agent/issues/45303) `monitor` 和 `session_search` 辅助模型未出现在 `hermes model` 选择器中。
- [#45279](https://github.com/NousResearch/hermes-agent/issues/45279) macOS 用户安装场景下 Node Shims 覆盖 Homebrew/nvm。
- [#45272](https://github.com/NousResearch/hermes-agent/issues/45272) CLI 流式输出在终端软换行时断词。
- [#45264](https://github.com/NousResearch/hermes-agent/issues/45264) macOS 桌面端全屏模式侧边栏布局偏移。

### 6. 功能请求与路线图信号

- **高可能纳入下一版**：[#39691](https://github.com/NousResearch/hermes-agent/issues/39691) (headroom-ai 压缩) 因备受社区期待（6👍）且与“输出长度截断”（#7237）强相关，可能是 Agent 模块下一阶段的重点。
- **桌面端体验大更新**：多个 Feature 指向桌面端进化，包括 [看板墙集成](https://github.com/NousResearch/hermes-agent/issues/41222)、[UI/UX 改进（自动滚动/分组）](https://github.com/NousResearch/hermes-agent/issues/44140)、[`.gitignore` 文件显示开关](https://github.com/NousResearch/hermes-agent/pull/45355)、[远程网关分离](https://github.com/NousResearch/hermes-agent/pull/45358)。桌面端正在从聊天工具进化为全功能操作台。
- **Agent 智能增强**：[#45369](https://github.com/NousResearch/hermes-agent/pull/45369)（模糊指代委派防护）和 [#45331](https://github.com/NousResearch/hermes-agent/issues/45331)（YAML+Git 多端同步 Memory Provider）将提升 Agent 在多 Agent 协作和跨设备场景下的可靠性。
- **国际化**：[#45348](https://github.com/NousResearch/hermes-agent/pull/45348) 提交了法语本地化，标志着项目正在积极拓展非英语用户市场。

### 7. 用户反馈摘要

- **核心痛点**：配置自定义 Provider（DeepSeek/Anthropic/MiniMax）的体验极差，归一化、认证、参数结构等问题频发。Docker 部署的用户普遍反映文件句柄和目录权限问题较多。
- **满意点**：社区贡献者修复速度极快（如 #45352 的 3 个并行 Fix PR）。用户对 #7237 的最终关闭感到欣慰，对能解决长输出问题的 #45351 表示“避免了信息丢失”。
- **明确诉求**：
    - 强烈希望 **跨平台会话统一**（[#45275](https://github.com/NousResearch/hermes-agent/issues/45275)），Telegram/Discord/Desktop 的割裂感影响了日常使用体验。
    - 用户需要更 **可靠的 Cron 任务反馈机制** 和 **更智能的上下文管理**，而不是简单的全量总结。
    - 需要 **澄清文档**，例如 Telegram 用户创建的 DM 主题存在读取状态限制但未被文档提及（[#45295](https://github.com/NousResearch/hermes-agent/issues/45295)）。

### 8. 待处理积压

- **最古老的高影响 Issue（无修复 PR 追踪）：**
    - [#18646](https://github.com/NousResearch/hermes-agent/issues/18646) WhatsApp 群组路由（P2，5月2日创建）—— 已超 6 周无人认领，严重影响 WhatsApp 网关的核心功能。
    - [#17199](https://github.com/NousResearch/hermes-agent/issues/17199) DeepSeek Provider 端点重写（P2，4月29日创建）—— 已超 6 周，严重影响使用第三方兼容端点的用户。
- **高赞功能请求：**
    - [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) headroom-ai 压缩（6👍，P3）—— 暂无关联 PR 或指派负责人，建议维护者关注社区诉求。
- **依赖健康/技术债：**
    - [#45375](https://github.com/NousResearch/hermes-agent/issues/45375) electron-builder @ 26.8.1 拉取弃用依赖（inflight/rimap@2/glob@7）。
    - [#45374](https://github.com/NousResearch/hermes-agent/issues/45374) 捆绑 Node 版本停留在 22，未跟进 LTS 24。
    - *以上两项虽标记为 P3，但每次安装都会弹出警告，建议尽快升级以避免阻碍新用户。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw 项目动态日报 | 2026年6月13日
**分析师摘要**：项目进入高密度迭代期，24 小时内处理 20 个协作项（6 Issues / 14 PRs），渠道架构重构（#2551）与权限体系（#3109）两大基础设施合并落地，项目健康度极佳。社区注意力集中在**生产环境安全**与**新版 LLM 兼容性**。

---

### 1. 今日速览
今日项目活跃度极高，14 个 PR 与 6 个 Issue 正在流动，并发布了一个 Nightly 构建。核心进展集中在三方面：**架构层**完成渠道标识标准化（#2551），为多实例部署扫清障碍；**协议层**补全 Pico WebSocket 的生命周期信号（#3116 对应 #2984）；**稳定性层**集中修复了 Gemini 3.5 Flash 兼容性崩溃（#3111）和会话历史状态损坏（#3115）。整体看来，项目正从单实例个人工具向多租户、协议完整的智能体后端加速演进。

### 2. 版本发布
**Nightly Build: v0.2.9-nightly.20260613.c362114c**
- **内容**：自动化日常构建，包含自 v0.2.9 以来所有 main 分支变更。
- **说明**：官方标注 “may be unstable”，仅建议测试与集成验证使用。CI 流水线运行正常。
- **变更日志**：[compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

### 3. 项目进展（今日合并/关闭项）
今日共有 **3 个 PR 被合并/关闭**，包含一项重大基础设施重构：

- **#2551 [CLOSED] 渠道标识标准化重构 （作者: cytown）**
  渠道名（配置 Key）与 Provider 类型解耦，消息总线与 Agent 分发逻辑现在可以正确识别同一 Provider 的多个实例。
  ➜ 这是多实例、多渠道架构的**基石性合并**。
  [PR链接](https://github.com/sipeed/picoclaw/pull/2551)

- **#3109 [CLOSED] 频道级权限范围控制**
  引入 “safe/unsafe” 边界概念，在群组/频道中可限制 `exec`、`write_file` 等危险操作。
  ➜ 弥补了团队协作场景的核心安全缺口。
  [Issue链接](https://github.com/sipeed/picoclaw/issues/3109)

- **#3112 / #3113 [CLOSED] 静默错误清理**
  `chengzhichao-xydt` 持续修复 `json.Marshal` / `json.Unmarshal` 被 `_` 忽略的问题，提升可观测性。
  [PR #3112](https://github.com/sipeed/picoclaw/pull/3112) | [PR #3113](https://github.com/sipeed/picoclaw/pull/3113)

### 4. 社区热点（讨论最活跃 / 诉求最强烈）
- **#3114  Telegram 渠道按对话类型分级控制** (作者: v2up-32mb)
  #3109 刚合并，社区立刻跟进要求在 Telegram 上区分**私聊/群组/频道**分别赋予不同能力。反映出用户将 PicoClaw 部署到公共群组时**极强的安全敏感度**。
  [Issue链接](https://github.com/sipeed/picoclaw/issues/3114)

- **#2984  Pico WebSocket 显式 Turn 完成信号（2 👍）**
  外部客户端开发者 `Brook-sys` 强调缺少确定性信号导致客户端状态管理复杂化。对应修复 PR #3116 已迅速提交，说明核心团队高度重视外部集成体验。
  [Issue链接](https://github.com/sipeed/picoclaw/issues/2984)

### 5. Bug 与稳定性（按严重程度排列）
| 严重程度 | 问题 | Fix PR |
|---|---|---|
| 🔴 **严重** | **#3111**: Gemini 3.5 Flash 工具调用 400 Bad Request。Google API 要求 `thought_signature`，当前 Schema 不兼容。**尚无修复**。 | 无 |
| 🟡 **高** | **#3110**: Telegram Forum 话题回复错发至 #General。影响升级了超级群的用户。**尚无修复**。 | 无 |
| 🟡 **高** | **#3012** (stale): Evolution 模式每分钟持续消耗 Token。资源浪费严重，标记为 stale 需尽快评估。 | 无 |
| 🟢 **中** | **#3115**: `data:image` 内联 URL 被错误当作媒体附件，导致会话历史状态损坏。 | ✅ [PR #3115](https://github.com/sipeed/picoclaw/pull/3115) |
| ⚪ **低** | 运行时代码类型断言（`ok` check）缺失 (#3053, #3045, #3091)，`chengzhichao-xydt` 正在批量修复中。 | 进行中 |

### 6. 功能请求与路线图信号
- **Agent 远程模式（#3118）**：新增 `--remote` 参数，通过 WebSocket 连接远程 PicoClaw Agent。标志 PicoClaw 开始支持分布式 Agent 架构。
- **视觉管线优化（#2964 / #3117）**：图像压缩策略与路由逻辑，自动将媒体请求分配给配置的图像模型。对使用多模态模型（如 Gemini / GPT-4V）的用户至关重要。
- **DeltaChat 渠道（#3063）**：正在建设的去中心化通信渠道，符合隐私优先趋势。
- **安全边界（#3109 / #3114）**：下一个里程碑大概率围绕**生产级多租户安全**与**渠道粒度权限**展开。

### 7. 用户反馈摘要
- **🔴 痛点 - 资源浪费**：`xpader` 在 #3012 中报告 Evolution 模式下“每一分钟”都在消耗 Token，已严重影响长时间运行体验。
- **🔴 痛点 - 安全焦虑**：`v2up-32mb` 的多次反馈（#3109, #3114）直指 PicoClaw 在群组中的“防呆”机制缺失：“如果配置宽松，任何人都可以让机器人执行 shell 命令”。
- **🟡 使用场景 - 前沿模型尝鲜**：`Giordano10` 同日报了两个 Bug（Gemini 3.5 Flash 与 Telegram Forum），属于积极尝试新功能的**高价值开发者**，其反馈应优先处理。
- **🟢 集成者之声**：`Brook-sys` 的反馈（#2984）代表外部开发者的对接诉求：**需要确定的 Agent 完成事件**来正确控制 UI 状态。

### 8. 待处理积压（存量风险提醒）
以下 Issue/PR 已停滞较久或标记为 [stale]，建议维护者安排 review 或决策是否搁置：

- **#3012** [stale] Evolution 模式持续 token 消耗 — 6 天无进展。
  [Issue链接](https://github.com/sipeed/picoclaw/issues/3012)
- **#2964** [stale] 图像输入压缩 PR — 16 天无 Review。
  [PR链接](https://github.com/sipeed/picoclaw/pull/2964)
- **#2917** [stale] NEAR AI Cloud Provider 集成 — 23 天无 Review。
  [PR链接](https://github.com/sipeed/picoclaw/pull/2917)

> **总结**：今日代码合并量可观，架构重构完成第一轮交付；但 Gemini 3.5 Flash 兼容性 Bug 和 Telegram Forum 问题叠加出现，提示社区正以较高标准要求项目的**前沿模型适配**与**复杂平台兼容性**，这两点将是近期稳定性口碑的关键。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw 项目动态日报 | 2026-06-13**

**分析范围：** nanocoai/nanoclaw (GitHub)

---

### 1. 今日速览

过去24小时项目活跃度极高，累计5条Issues与18条PR更新。项目成功合并了Signal通道的完整支持（文件、反应）及多项核心稳定性修复（崩溃自愈、路由刷新、API重试），标志着通道生态基本成型。同时，社区贡献者密集提交了8个高质量的Open PR，重点攻向安全加固（容器权限最小化、npm包年龄检查）和Provider生态抽象（持久化内存、能力注册）。整体来看，NanoClaw正从功能快速扩展期步入稳定性深水区与生态建设期，社区技术成熟度与参与度显著提升。

---

### 2. 版本发布
今日无新版本发布。

---

### 3. 项目进展

今日共有10个PR完成合并，项目在以下几个维度取得关键进展：

*   **Signal通道生态成熟**
    *   [PR #2040](https://github.com/nanocoai/nanoclaw/pull/2040) - 支持出站附件（文件、图片）。
    *   [PR #2071](https://github.com/nanocoai/nanoclaw/pull/2071) - 路由所有非音频附件至收件箱路径。
    *   [PR #2203](https://github.com/nanocoai/nanoclaw/pull/2203) - 支持入站与出站双向反应用。
    *   [PR #2070](https://github.com/nanocoai/nanoclaw/pull/2070) - 重构附件解析器以接受宿主机文件路径，为更多原生通道适配铺平道路。

*   **核心运行时稳定性修复**
    *   [PR #2670](https://github.com/nanocoai/nanoclaw/pull/2670) - 实现“毒化断点续传”崩溃循环的自愈。此前对话记录损坏会导致无限崩溃，现可自动恢复。
    *   [PR #2277](https://github.com/nanocoai/nanoclaw/pull/2277) - 修复`follow-up`消息路由冻结问题，确保在流式输出中动态刷新路由上下文。
    *   [PR #2267](https://github.com/nanocoai/nanoclaw/pull/2267) - 修复Agent-to-Agent回复总是路由到最新Session的“分脑”问题，确保返回正确会话。
    *   [PR #2692](https://github.com/nanocoai/nanoclaw/pull/2692) - 为5xx瞬时API错误（如529）添加轮询重试与通知机制，避免静默失败。

*   **基础设施与能力扩展**
    *   [PR #2084](https://github.com/nanocoai/nanoclaw/pull/2084) - 新增每日项目备份与CLI恢复能力，支持全量或单Agent恢复，提供生产级灾备保障。
    *   [PR #2072](https://github.com/nanocoai/nanoclaw/pull/2072) - Ollama生成现支持通过收件箱路径传入图片，扩展多模态能力。

---

### 4. 社区热点

今日社区讨论与技术贡献集中在两大方向：

1.  **安全合规深化**
    由 `boazdori` 提交的两项PR引发了广泛关注。容器运行时安全（[PR #2748](https://github.com/nanocoai/nanoclaw/pull/2748) - 默认移除Capability、禁止权限提升）与供应链安全（[PR #2749](https://github.com/nanocoai/nanoclaw/pull/2749) - 对Agent请求安装的npm包执行3天最小发布年龄检查）均有高质量建议。这代表高级社区用户对运行安全基线已有明确共识。

2.  **Provider生态蓝图**
    由 `omri-maya` 提交的三个关联PR（[PR #2745](https://github.com/nanocoai/nanoclaw/pull/2745) - 持久化内存脚手架，[PR #2746](https://github.com/nanocoai/nanoclaw/pull/2746) - 能力定义缝隙，[PR #2747](https://github.com/nanocoai/nanoclaw/pull/2747) - SDK升级与凭证桩）标志着NanoClaw架构正在向通用的、标准化的多Provider框架演进。

*   **讨论度最高：** Issue [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) 以3条评论成为今日讨论最多的问题，开发者`mshirel`报告了并发场景下的消息丢失，引发了关于去重逻辑和Event Loop的深入讨论。

---

### 5. Bug 与稳定性

| 严重程度 | 问题/PR | 状态 | 分析与影响 |
|---|---|---|---|
| **严重** | Issue [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) - 无Tool级超时 | **Open，无Fix PR** | 挂起的MCP调用会阻塞会话长达30分钟，是Agent“假死”的核心根因之一。生产环境关键隐患。 |
| **严重** | Issue [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) - 并发丢消息 | **Open，无Fix PR** | `send_message`去重与`poll-loop`在并发场景下静默丢弃响应，导致客户端超时。创建近30天，属长期积压Bug。 |
| **中危** | Issue [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) - MCP工具越权 | **Open** | `create_agent`工具未校验管理员身份，任何容器都可创建Agent组。 |
| **中危** | PR [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) - DB WAL竞态 | **Open Fix PR** | 容器强制杀死后`outbound.db`陷入恢复状态，通过完善WAL恢复逻辑修复。 |
| **已修复** | Issue [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) - 预算耗尽静默丢失 | **Closed** | 预算超额时的合成200响应被识别并处理。 |
| **已修复** | PR [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) - 5xx API重试 | **Merged** | 为API瞬时错误添加了弹性重试机制。 |

---

### 6. 功能请求与路线图信号

1.  **Provider能力抽象（高优路线图信号）**
    [PR #2746](https://github.com/nanocoai/nanoclaw/pull/2746) 提出的`agent-surfaces capability seam`与[PR #2745](https://github.com/nanocoai/nanoclaw/pull/2745)的持久化内存脚手架，明确指向下一阶段将构建标准的Provider能力注册与感知层。未来的第三方集成将基于此框架进行。

2.  **容器与供应链安全硬性约束（极大概率纳入下一版本）**
    [PR #2748](https://github.com/nanocoai/nanoclaw/pull/2748) 与 [PR #2749](https://github.com/nanocoai/nanoclaw/pull/2749) 逻辑严密且与主流安全实践（如Kubernetes Pod Security Standards）高度一致，预计无需大改即可合并。

3.  **用户迁移路径请求（Issue [#2632](https://github.com/nanocoai/nanoclaw/issues/2632)）**
    用户详细梳理了v1的Telegram Swarm功能在v2中的实现状态，请求官方明确此功能的现状及迁移路径。这提示维护者需要补充清晰的v1→v2 `CHANGELOG` 或迁移 FAQ。

---

### 7. 用户反馈摘要

*   **可靠性痛点 `mshirel` (Issue #2506, #2668)：** 报告了两起严重稳定性事件（并发丢消息、Tool无超时）。反馈直指生产环境痛点，对消息交付健壮性及会话管理兜底机制有较高期望。
*   **迁移路径困惑 `arthurkrupa` (Issue #2632)：** 详细对比了新旧代码寻求功能确认。反映了重度用户在规划v2迁移时，因特性状态不明确产生的决策困难。
*   **安全意识 `jonazri` (Issue #2711)：** 精准定位了`create_agent`工具的权限漏洞，并追溯到具体Commit。体现了社区对API边界的警觉性。
*   **成本透明性 `assapin` (Issue #2751)：** 遭遇预算耗尽后Agent静默无响应，表达了成本管控与操作透明性的需求。

---

### 8. 待处理积压

以下为长期未解决或等待响应的关键Issue，建议维护者关注：

1.  **Issue [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) (创建于2026-05-16)：** 并发消息去重静默丢消息。已积压 **28天**，影响高并发场景下的通讯可靠性，建议纳入Sprint排期。
2.  **Issue [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) (创建于2026-06-01)：** 缺乏Tool级超时。已积压 **12天**，是Agent运行时“无响应”的核心根因，解决方案（如通用`Promise.race`）可参考社区讨论。
3.  **Issue [#2632](https://github.com/nanocoai/nanoclaw/issues/2632) (创建于2026-05-28)：** 请求明确Telegram v2迁移路径。已积压 **16天**，存在v1用户因迁移路径不明确而放弃升级的风险，建议官方人员给出明确答复或文档更新计划。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是依据您提供的 NullClaw 项目实时数据生成的 2026-06-13 项目动态日报。

---

### NullClaw 项目日报 | 2026-06-13

---

#### 1. 今日速览

过去 24 小时，NullClaw 项目进入平稳的“开发期”但“低交互”状态：**无新版本发布**，**无 PR 合并/关闭**，仅新增 1 条用户侧 Bug 报告。尽管合入动作停滞，但开发者的活跃度保持良好，共有 3 个待合并的修复与功能增强型 PR（#949, #951, #953）正在推进，覆盖了 Discord 网关恢复、Agent 错误处理及配置灵活性。社区侧注意力高度集中在 **#952**（Ollama 本地模型输出截断）问题上，目前尚无官方回应。项目健康度评分可评估为 **良好（待处理机制较缓慢）**。

---

#### 2. 版本发布

**无**

---

#### 3. 项目进展

**今日无任何 PR 被合并或关闭**，但以下三个待合入的 PR 代表了项目当前的主要开发方向：

- **#953 [待合并] fix(discord): recover closed gateway sockets**
  - 作者：vernonstinebaker
  - 重要性：**极高**
  - 描述：修复了 Discord 网关套接字关闭后的主动恢复机制。涉及心跳线程清理、预 HELLO 状态的超时保护以及回归测试。这是保证 Discord Bot 模式长久稳定运行的关键修复。
  - 链接：`nullclaw/nullclaw Pull Request #953`

- **#951 [待合并] fix(agent_runner): suppress stderr initialization logs**
  - 作者：vernonstinebaker
  - 重要性：**高（用户体验）**
  - 描述：修复 Agent 子进程失败时，将内部初始化日志（内存规划、MCP 注册等）错误输出到频道的 Bug。避免了向用户暴露不必要的技术噪音。
  - 链接：`nullclaw/nullclaw Pull Request #951`

- **#949 [待合并] fix: make queue_mode configurable from config.json**
  - 作者：vernonstinebaker
  - 重要性：**中（功能增强）**
  - 描述：将 `QueueMode` 枚举重构到 `config_types.zig` 作为唯一数据源，并允许用户在 `config.json` 中通过 `agent.default_queue_mode` 配置默认队列模式。这一变化为后续会话策略的个性化定制打下了基础。
  - 链接：`nullclaw/nullclaw Pull Request #949`

---

#### 4. 社区热点

**Issue #952：[Bug] Local model using ollama returns incomplete answers**
- **作者**：bloodgroup-cplusplus
- **状态**：Open，0 评论，0 👍
- **链接**：`nullclaw/nullclaw Issue #952`
- **分析**：这是今日最高（也是唯一）的热点 Issue。用户使用 Ollama 加载 Gemma 模型后，Agent 无法输出完整的句子（incomplete sentences）。由于没有评论，目前无法判断是模型上下文长度限制、Ollama 流式缓冲问题、还是 Agent 输出解析器的截断逻辑所致。此问题直接击中 **“本地部署 + 开箱即用”** 的核心体验，是当前社区反馈最大的压力点。

---

#### 5. Bug 与稳定性

| 严重程度 | Issue / PR ID | 描述 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | **#952** | 使用 Ollama 加载 Gemma 模型，Agent 回答不完整。 | **未修复** | 影响所有本地模型用户，无开发者响应。 |
| **中等** | **#953** | Discord 网关断开可能导致 Bot 永久失联。 | **待合并** | 已有完整修复方案，等待 Code Review。 |
| **中等** | **#951** | Agent 子系统崩溃时向用户弹出一堆初始化日志。 | **待合并** | 纯体验向修复，等待 Code Review。 |

---

#### 6. 功能请求与路线图信号

今天没有正式的功能请求 Issue 提交，但从 PR #949 可以看出项目组的主动规划：
- **信号**：`QueueMode` 的配置化（PR #949）。这暗示项目不仅仅满足于“启动即用”的单模式，正在规划针对不同场景（如实时聊天 vs. 异步批处理）的会话策略。这很有可能会进入下一个 Minor 版本的路线图中。

---

#### 7. 用户反馈摘要

本次报告周期内的用户反馈仅限于 **Issue #952**，提炼如下：
- **痛点**：用户尝试本地化部署（Ollama + Gemma），但模型推理结果未能被正确输出，导致对话体验严重受损（Agent “说着说着就断了”）。
- **使用场景**：隐私敏感型用户、离线用户、希望通过本地模型节省 API 成本的用户。
- **满意度**：**低（存在严重体验阻碍）**。用户感到困惑，并求助社区（附带了截图）。这说明在“本地模型兼容性”方面，NullClaw 的用户预期与实际表现存在明显差距。

---

#### 8. 待处理积压

**需维护者紧急关注：**

1. **Issue #952 （本地模型输出截断问题）**
   - **风险**：短期内无响应的 Bug 是社区口碑的重大隐患。建议立即向用户请求 `config.json` 和 Ollama 日志以复现，并排查 Agent 输出的 Token 限制 / 流式处理逻辑。
   - **链接**：`nullclaw/nullclaw Issue #952`

2. **PR #949, #951, #953 （开发者积压）**
   - **风险**：来自同一位开发者（vernonstinebaker）的三个 PR 目前均处于待审查状态。长期积压容易导致代码分支过时并挫伤贡献者积极性。建议本周内安排至少一次集中 Review，优先合并 **#953**（稳定性）和 **#951**（体验优化）。
   - **链接**：`nullclaw/nullclaw Pull Requests`

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目数据生成的 2026-06-13 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-13

### 1. 今日速览

项目过去24小时保持极高活跃度，共处理了50条Issue与50条PR，成功关闭/合并了37项。项目处于 **Reborn 界面稳定化冲刺** 与 **核心架构攻坚** 双线并行的状态：大量长期存在的 UX Bug 被批量根除，安全审计与线程排空机制完成阶段性交付。同时，附件系统与 Slack 深度集成的 PR 栈仍在积极汇集。需要注意的是，`cargo-deny` 因新安全公告阻塞了全仓库 CI（#4824），且积压近一个月的 Release PR #3708 仍未合并，Breaking Changes 存在被阻塞的风险。

### 2. 版本发布

无。

### 3. 项目进展

- **Reborn 交互体验显著提升**：贡献者 `sunglow666` 批量关闭了合计 14 个 UX 问题。包括：模型选择器保存错误 ID（#4703）、SSO 流程无法恢复（#4706）、PINNED 区域逻辑错误（#4721）、对话内容闪烁（#4719）、草稿丢失（#4724）及正在工作状态下的编辑器交互异常（#4725）等。这标志着 Reborn 的基础交互质量达到了一个新的节点。

- **安全审计与资源限量框架落地**：`zmanian` 贡献的三项 Hooks 相关核心 PR 成功合并：
    - **认证分发失败埋点**（#4562）：为安全性审计提供了关键的可观测性。
    - **BeforeCapability 分发上限**（#4568）：Fail-close 机制防止能力边界被滥用。
    - **Tenant 谓词 Key 上限**（#4569）：统一了调用与存储侧的配额控制，增强了多租户健壮性。

- **线程排空机制完成闭环**：PR #4812 (DeferredBusy Drain) 的合并解决了线程被 Gate 阻塞时消息可能丢失的问题。随后的架构复盘（#4831, #4832, #4833）已在 Issue 中完成讨论并关闭，为未来的批处理化与索引优化奠定了理论蓝图。

- **新功能开发预览**：
    - **附件系统管道**：`ilblackdragon` 的附件注册表 PR #4654 与后端存储管道（#4655, #4668, #4670）形成了连贯的开发链，前端 WebUI 通道 #4738 也同步在推进，附件全流程支持即将成型。
    - **运行时上下文注入**：为解决 Agent 对当前连接状态和交付目标的“盲区”，PR #4836 实现了 `msg:runtime.*` 上下文切片，显著提升了模型在交互环境中的决策能力。

### 4. 社区热点

- **#4825 - 权限持久化作用域争议**：用户发现“Always Allow”权限在新线程后重置引发热议。社区与开发者深入讨论了 `thread_id` 是否应被纳入持久化作用域，最终促成了修复 PR #4835 的迅速提交。
    `链接: nearai/ironclaw Issue #4825`
- **#4817 - Drain 架构的未来走向**：虽为技术追踪 Issue，但核心开发者通过 3 条评论深入探讨了“可信重交 seam”、“过期策略”与“启动清扫”三大前瞻性设计方向，展现了深厚的工程规划文化。
    `链接: nearai/ironclaw Issue #4817`
- **#4777 - Slack 重连循环修复**：作为 Use Case 3 的瓶颈，如何让 WebUI 正确反映 Slack 连接状态是用户最迫切的痛点。该 PR 的分析与修复思路获得了高度关注。
    `链接: nearai/ironclaw PR #4777`

### 5. Bug 与稳定性

- **【紧急/阻塞级】**
    - **全仓库 CI 阻断 (#4824)**：Postgres 相关 crate 出现新 RUSTSEC 公告，导致 `cargo-deny` 在 main 分支及所有 PR 上失败。这是当前最高优先级的技术债务，可能直接影响所有贡献的合并节奏。
        `链接: nearai/ironclaw Issue #4824`
- **【高影响级】**
    - **Ollama 测试连接假阳性 (#4696)**：Ollama 未运行仍报告连接成功，严重误导用户。已提出 3 天仍无配套修复 PR。
        `链接: nearai/ironclaw Issue #4696`
    - **Provider 状态显示不一致 (#4697)**：Inference 页面显示的“Active” Provider 与实际执行时使用的 Provider 不匹配，影响所有 Provider 用户。
        `链接: nearai/ironclaw Issue #4697`
    - **工具工作流失败导致消息混乱 (#4762)**：在本地 Reborn 中，工具工作流失败后发送简单的后续消息会导致活动排序错误，影响 Agent 交互可靠性。
        `链接: nearai/ironclaw Issue #4762`
- **【修复确认级】**
    - 昨日批量修复的 PR 已确认关闭了大批 Bug，如：SSO 登录失败未恢复 (#4706)、模型选择器错误 (#4703)、附件警告跨对话残留 (#4720) 等，修复效率极高。

### 6. 功能请求与路线图信号

- **附件系统是下阶段绝对焦点**：由 #4644 衍生出的 5 个活跃 PR 揭示了团队正在积极补齐 Reborn 的文件上传与处理流程。这将是 Agent 从“文本聊天”向“多模态工作台”演进的关键一步。
- **Agent 环境感知能力补全**：
    - **时间感知**：Issue #4796 请求让模型感知当前时间，解决日历与规划类任务的错误。
    - **通道/交付状态感知**：Issue #4828 要求提供运行时上下文切片（PR #4836 已实现），让模型自身理解当前连接状态，而不是依赖硬编码提示。
- **运维与观测性需求凸显**：Engine V2 用量统计 (#4822)、CI 分片加速 (#4813)、大文件重构 (#4818) 等需求的出现，表明项目正在从“能用”向“可运维/高质量”阶段过渡。

### 7. 用户反馈摘要

- **用户画像**：高阶开发者为主，期望通过自然语言编排复杂工作流（如文件创建 API 调用 #4762, #4759）。
- **满意之处**：团队对 Bug 的响应速度极快。昨日 14 个关键 UX 问题的批量关闭体现了极强的迭代执行力。
- **主要痛点**：
    - **信任与透明度**：Provider 状态不一致（#4697）与 Ollama 假阳性（#4696）严重损害了用户对系统状态的信任。
    - **交互一致性**：SSO 流程脆弱（#4706）、草稿丢失（#4724）、删除无反馈（#4823）等细节体验仍有较大优化空间。
    - **能力落差**：WebChat v2 目前不支持附件，但 Agent 会返回附件相关内容（#4720），导致体验割裂。

### 8. 待处理积压

- **命悬一线的 Release (PR #3708)**：自 5 月 16 日开启，内含 `ironclaw_common` 和 `ironclaw_skills` 的重大 Breaking Changes。阻塞原因不明，导致所有依赖新 API 的 PR 只能采用栈式策略暂存，合并风险日益增高。
    `链接: nearai/ironclaw PR #3708`
- **失联的核心 Bug**：
    - #4696 (Ollama 假阳性) - 无跟进回复
    - #4697 (Provider 状态错乱) - 无跟进回复
    - #4759 (路径重复) - 无跟进回复
- **搁置的架构改进**：
    - #4796 (AI 时间感知) - 虽是用户痛点，但当前无配套 PR 跟进。
    - #4588 (观测轨迹提供者) - 已等待 4 天，是实现可对比基准测试的关键依赖，关系到 `nearai-bench` 的集成。
        `链接: nearai/ironclaw PR #4588`

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据你提供的 LobsterAI GitHub 数据生成的 2026-06-13 项目动态日报。

---

### LobsterAI 项目动态日报 — 2026-06-13

**数据观测周期：** 2026-06-12 ～ 2026-06-13

---

#### 1. 今日速览
过去 24 小时，LobsterAI 项目共更新 **17 个 Pull Requests**（11 个合并/关闭，6 个待处理），展现了极高的开发活跃度。主线合并了发版分支 `release/2026.6.11`（#2158），标志**Computer Use MVP** 和 **Realtime ASR 语音输入**等重磅功能正式进入主代码库。团队同时批量清理了 5 个关于“未保存内容丢失”的积压 UI 修复 PR，显著改善了用户体验。尽管 Issue 侧仅有 1 个更新（项目首个 Issue 被关闭），但 PR 侧的活跃度表明项目正处于新版本发布前的快速冲刺阶段。**整体项目健康度：优。**

#### 2. 版本发布
*（本条无内容）*
今日无新版本发布（0 releases）。但 PR #2158 完成了 `release/2026.6.11` 分支向 `main` 的合并，预示着 `v2026.6.12` 乃至更大版本的 Release 已呼之欲出。

#### 3. 项目进展
今日合并/关闭的 PR 清晰展示了项目的双重焦点：**大功能收尾**与**小修复细补**，同时兼顾**历史积案清理**。

- **🚀 重大功能集成：**
    - **[PR #2158](netease-youdao/LobsterAI PR #2158) - 发版分支合并：** 这是今日最高优先级的合并。
        - **Computer Use MVP：** 引入计算机使用模式的初步版本及内置工具包，标志着项目正式迈入桌面自动化智能体领域。
        - **Realtime ASR：** 在协作者（Cowork）模式下新增实时语音输入，大幅度提升语音交互的流畅度。
        - **Artifact 共享增强：** 增加了 HTML 内容的公开分享模式选择，并支持图片和 SVG 格式的 Artifact 分享。
    - 该合并意味着以上特性已进入发布倒计时。

- **🛠️ 稳定性与 Bug 修复深化：**
    - **[PR #2156](netease-youdao/LobsterAI PR #2156) 运行时升级：** Computer Use 运行时升级至 1.0.7。
    - **[PR #2154](netease-youdao/LobsterAI PR #2154) 流式响应修复：** 修复了手动停止流式回复后模型元数据丢失的问题。
    - **[PR #2153](netease-youdao/LobsterAI PR #2153) 模型选择修复：** 修复了同名包名下的模型选择状态混乱问题。
    - **[PR #2155](netease-youdao/LobsterAI PR #2155) 语音输入修复：** 阻止了实时语音输入的重复启动问题。
    - **[PR #2157](netease-youdao/LobsterAI PR #2157) 文件格式修复：** 修复了文生图保存时字节流格式与文件后缀名不匹配的“名实不符”问题。

- **🛡️ 用户体验全面加固（积案清理）：**
    - 批处理关闭了 5 个针对“未保存内容丢失”的 PR（[#1473](netease-youdao/LobsterAI PR #1473)、[#1474](netease-youdao/LobsterAI PR #1474)、[#1475](netease-youdao/LobsterAI PR #1475)、[#1476](netease-youdao/LobsterAI PR #1476)、[#1477](netease-youdao/LobsterAI PR #1477)），全面覆盖了 Agent 创建、设置、MCP 配置、草稿持久化、历史重编等核心场景。

#### 4. 社区热点
- **🎉 里程碑事件：项目首个 Issue 关闭**
    - **[Issue #1](netease-youdao/LobsterAI Issue #1) - `hit API error with OpenAI API Type`** 于今日关闭。该 Issue 由用户 **simson2010** 于半年多前（2026-02-19）提出，记录了在 Mac 平台下配置不同类型 API Keys 时遇到的兼容性问题。
    - **分析：** 虽然该 Issue 在近期没有激烈的讨论，但作为开源项目的“第一个 Issue”，它的关闭具有强烈的象征意义。这说明团队未曾遗忘早期用户遇到的深层技术债务，并在这次发版前后对其进行了彻底的根因排查和修补。这能大大增强长期贡献者和早期用户的信心。

#### 5. Bug 与稳定性
- **严重（待修复）：**
    1. **[#1446](netease-youdao/LobsterAI PR #1446) - OpenClaw 网关崩溃循环：** 应用陷入无限重启，严重影响正常使用。这是最严重的积压 Bug。
    2. **[#1453](netease-youdao/LobsterAI PR #1453) - 技能停用失效：** 已停用的技能仍会在后台注入提示词，存在逻辑安全隐患。

- **中等（待修复）：**
    1. **[#1454](netease-youdao/LobsterAI PR #1454) - 定时任务创建无响应：** 特定操作下按钮无任何反馈，造成操作流程阻塞。
    2. **[#1456](netease-youdao/LobsterAI PR #1456) - 快捷键冲突：** 系统缺乏冲突检测，导致用户自定义的快捷键被静默覆盖而失效。
    3. **[#1448](netease-youdao/LobsterAI PR #1448) - 本地化缺失：** Agent 设置等核心界面部分内容仅显示英文，影响非英语用户。

- **已修复项目：**
    - 文生图扩展名错误（#2157）。
    - 语音输入重复启动（#2155）。
    - Agent 创建/设置/MCP 弹窗未保存弹窗提示（#1473-#1475）。
    - API 兼容性错误（Issue #1 已关闭）。

#### 6. 功能请求与路线图信号
- **明确路线图（来自 #2158 合并）：**
    - **Computer Use / 桌面代理：** 这是本月项目释放的最重磅信号，LobsterAI 正在向“让 AI 直接操作电脑”的高级 Agent 形态演进。
    - **实时音频交互（Realtime ASR）：** 语音交互方式从“按下-说话”升级为更自然的流式对话，提升了协同工作的效率。
    - **成果物公开展示（Public Artifact Sharing）：** 允许用户公开分享 AI 生成的 HTML 和图片/SVG 成果，这是提升项目曝光度和社交裂变的重要功能。

- **高潜力纳入（来自开放 PR）：**
    - **[#1449](netease-youdao/LobsterAI PR #1449) - 定时任务记录折叠：** 这是一个呼声很高的需求。随着用户使用定时任务的频率增加，侧边栏被刷屏是必然痛点。该 PR 提供了优雅的解决方案，预计很快会被提上合并日程。

#### 7. 用户反馈摘要
- **痛点：多 API 模型配置复杂。**
    - **反馈来源：** Issue #1。用户 `simson2010` 反映在配置 MiniMaxi API key 并测试通过后，切换至 OpenAI 消息类型进行对话时遭遇 `400 invalid params` 错误。这表明底层 Provider 的类型判断和参数映射逻辑仍存在易出错的灰色地带。
- **痛点：生成文件可靠性。**
    - **反馈来源：** PR #2157 对应的用户报告。用户指出程序会将 PNG 内容保存为 `.jpg` 或 `.webp` 后缀的文件，这可能在跨平台或特定应用场景下导致文件识别错误。
- **满意：反馈响应及时。**
    - **反馈来源：** 用户对数据丢失的担忧。今天批量合入了多个关于“未保存内容丢失”的修复。这说明社区关于表单内容意外丢失的反馈被开发团队高度重视，并一次性完成了对所有核心弹窗的补强。

#### 8. 待处理积压
**⚠️ 提醒维护者注意：** 目前项目中有 **6 个** 标有 `[stale]` 标签的 PR 仍未合并，创建已超过 2 个月（2026-04-03 创建）。其中包含影响较为严重的修复：
- **🔴 优先级 P0：**
    - **[#1446](netease-youdao/LobsterAI PR #1446) - OpenClaw 网关无限重启：** 影响应用可用性的阻断性故障。
    - **[#1453](netease-youdao/LobsterAI PR #1453) - 技能停用失效：** 影响系统逻辑可靠性的 Bug。
- **🟠 优先级 P1：**
    - **[#1454](netease-youdao/LobsterAI PR #1454)** - 定时任务创建无响应（流程死锁）。
    - **[#1456](netease-youdao/LobsterAI PR #1456)** - 快捷键冲突（功能缺陷）。
- **🟡 优先级 P2：**
    - **[#1448](netease-youdao/LobsterAI PR #1448)** - 本地化问题（体验）。
    - **[#1449](netease-youdao/LobsterAI PR #1449)** - 定时任务记录折叠（功能特性）。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据 Moltis 项目 2026 年 6 月 12 日全天 GitHub 活动数据生成的 2026-06-13 项目动态日报。

---

## Moltis 项目日报 | 2026-06-13

### 1. 今日速览

过去 24 小时内，项目动态以社区讨论为主，**代码层无实质性推进**。共产生 3 条 Issue 更新，但无任何 Pull Request 被合并或关闭，亦无新版本发布。当前项目处于 **“需求驱动、开发蓄力”** 阶段：一方面社区提出了极具战略价值的增强提议（企业级沙箱隔离与超低延迟本地语音识别），另一方面核心开发组的代码公开贡献动作暂时放缓，整体活跃度评估为 **中低水平**。

### 2. 版本发布

本日无新版本发布。

### 3. 项目进展

今日无任何 Pull Request 提交或合并，项目在代码层面暂无可见的新功能落地或 Bug 修复。这可能暗示核心维护者正在进行高难度的底层大型重构，或在集中精力评估 [#1118](https://github.com/moltis-org/moltis/issues/1118) 类需要改动的重大特性可行性。

### 4. 社区热点

今日讨论热度分化明显，三个活跃的 Issue 分别代表了三种不同的社区诉求：

- **最具争议/活跃的讨论：** **[Bug] Fastmail MCP 授权问题 ([#1115](https://github.com/moltis-org/moltis/issues/1115))**  
  获得 2 条评论，是目前互动最多的议题。用户配置 Fastmail 服务时遭遇授权失败，社区正在围绕该问题是环境配置歧义还是核心协议处理 Bug 进行排查。这暴露出第三方 MCP 服务集成的稳定性与易用性是当前使用中的显性痛点。

- **最具战略价值：** **Kubernetes 原生沙箱后端 ([#1118](https://github.com/moltis-org/moltis/issues/1118))**  
  该提案要求引入基于 Kubernetes 短暂 Pod 的执行后端，并支持 Kata Containers / gVisor 等 VM 级运行时。这标志着社区中**高安全需求用户**（如企业 DevOps）正在尝试将 Moltis 推向生产环境，对 Agent 执行环境的隔离性要求已从进程级跃升至虚拟化级。

- **最具用户基础：** **FunASR/SenseVoice 本地 STT 引擎 ([#1102](https://github.com/moltis-org/moltis/issues/1102))**  
  虽创建已久但在今日重新获得关注。用户明确对比了当前 STT 的体验瓶颈，并指名道姓要求引入开源最强方案，反映了用户对 **“本地优先、超低延迟”** 语音交互的刚性需求。

### 5. Bug 与稳定性

- **中等严重程度 | 待排查：** **Fastmail MCP 授权失败 ([#1115](https://github.com/moltis-org/moltis/issues/1115))**  
  作者已按模板提交预检清单，但未提供完整的会话上下文日志。该 Bug 目前优先级较高（因其正在被社区实时讨论），但在无更多日志辅助时难以定位。建议维护者尽快介入，要求用户补充通信日志，以区分是 Fastmail API 变更还是 Moltis MCP 实现缺陷。**当前暂无关联修复 PR。**

### 6. 功能请求与路线图信号

今日提出的两个 Feature 均极具分量，释放了清晰的未来演进信号：

- **🚀 高优先级 / 路线图核心候选：** **Kubernetes 沙箱 ([#1118](https://github.com/moltis-org/moltis/issues/1118))**  
  若被采纳，这将是一次**架构级的变革**。该特性将直接塑造 Moltis 在“企业级 AI Agent 安全执行”领域的竞争力。考虑到“AI 安全性”是当前业界焦点，此需求有极大概率被纳入 **v1.x 的里程碑规划**，甚至可能成为下一个版本的核心宣传点。

- **🚀 中优先级 / 快速落地候选：** **FunASR/SenseVoice 本地 STT ([#1102](https://github.com/moltis-org/moltis/issues/1102))**  
  相较于 K8s 后端，集成本地 STT 引擎的技术路径相对明确（通常通过封装 FFI 或模型调用实现）。SenseVoice 70ms 处理 10s 音频的性能指标对于提升“个人 AI 助手”的体验极具杀伤力。该提案极可能作为**下一个迭代版本中的语音模块增强**予以实施。

### 7. 用户反馈摘要

- **安全焦虑**：用户在 [#1118](https://github.com/moltis-org/moltis/issues/1118) 中明确表达了对 LLM 生成命令执行的安全担忧（`untrusted LLM-generated...`），认为目前的沙箱模型不足以应对恶意代码，希望达到“虚拟机级”隔离。这反映出社区高级用户对项目安全上限的极大关切。
- **生态兼容性**：用户在 [#1115](https://github.com/moltis-org/moltis/issues/1115) 的诉求很直接——希望第三方 MCP 服务能开箱即用。目前的授权失败阻碍了 Fastmail 用户的使用，甚至可能暗示 Moltis 自身的 MCP 认证握手存在短板。
- **性能痛点**：用户在 [#1102](https://github.com/moltis-org/moltis/issues/1102) 对项目当前语音助手功能表示肯定（`Great voice assistant project!`），但随即指出了延迟和云依赖两大硬伤，并给出了具体的量化指标和开源替代方案，诉求非常务实。

### 8. 待处理积压

- **长期未响应的有价值的提案：** **本地 STT 引擎 ([#1102](https://github.com/moltis-org/moltis/issues/1102))**  
  该 Issue 创建于 6 月 4 日，直到今天（6 月 12 日）才有一条评论回复，经历了长达 8 天的搁置期。作为一条高质量且符合产品定位的功能请求，维护者长期的沉默可能会挫伤社区贡献者的积极性。建议项目维护者尽快进行技术可行性评估，并在 Issue 中给出明确的阶段回复（例如“已列入路线图”或解释当前技术阻碍）。

- **潜在的动力不足信号：** **PR 数量长期为零**  
  连续 24 小时无任何 PR 更新，结合项目整体进展节奏来看，是一个需要关注的健康度指标。可能的原因包括：核心开发者精力分散、PR 审核标准/流程不透明、或缺乏“Good First Issue”等低门槛入口。建议活跃社区渠道，适度降低贡献门槛，向外部贡献者释放更友好的信号。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# QwenPaw（CoPaw 项目）项目动态日报 | 2026-06-13

## 今日速览

过去 24 小时项目保持高活跃度：共更新 21 条 Issue（新开/活跃 14，已关闭 7）和 23 条 PR（待合并 13，已合并/关闭 10）。社区围绕定时任务异常、AgentScope 2.0 后端迁移、附件下载 404 等关键问题展开讨论；同时多项 Bug 修复 PR 被合并，包括运行时 2.0 模块化架构（Breaking Change）、控制台记忆配置丢失、Session 重定向等。版本方面未发布正式版，但已进行 1.1.12b1 的版本号更新（PR #5159 / #5157），预示新一轮迭代即将开始。

---

## 版本发布

**无**（新版本发布数为 0）。

---

## 项目进展

今日合并/关闭的重要 PR 聚焦于架构演进、核心 Bug 修复与 CI 质量门禁：

| PR | 描述 | 类型 | 状态 |
|----|------|------|------|
| #5078 | **Runtime 2.0 模块化架构**：将单体 Runner 拆分为可组合单元，并引入 `ToolCoordinator` 层实现细粒度工具调用控制，属于破坏性变更。 | Breaking Change / 新架构 | 已关闭（合并） |
| #5144 | **修复记忆配置丢失**：强制渲染 Collapse 面板，确保未展开时也能获取表单值，解决保存后配置丢失问题。 | Bug 修复 | 已合并 |
| #5147 | **修复 Coding Mode Session 重定向**：调整路由以支持 `/coding/*`，统一 Session 路径处理工具函数。 | Bug 修复 | 已合并 |
| #5154 | **重构记忆搜索结果样式**：修复 UI 中表格显示未知内容的问题。 | Bug 修复 | 已合并 |
| #5121 | **CI 增加发布验证门**：在构建生成后执行端到端安装/启动/健康检查，通过后才发布 PyPI/DockerHub。 | CI 改进 | 已合并 |
| #4144 | **修复桌面通配符地址准备检查**：绑定 `0.0.0.0` 时使用回环地址探测，解决 Windows 下桌面命令卡住。 | Bug 修复 | 已合并 |
| #5022 | **Guard 工作区还原路径**：防止备份恢复时将工作区写入受管理目录。 | 安全性 / 改进 | 已合并 |
| #5157 / #5159 | **版本号更新到 1.1.12b1**：为下一个测试版做准备。 | 发布工程 | 已合并 |

这些变更使项目在架构（Runtime 2.0）、CI 可靠性、以及多个用户报告的严重 Bug 方面取得实质进展，整体健康度向好。

---

## 社区热点

今日讨论最活跃、参与度最高的议题：

1. **#5064 – 定时任务无法触发**（评论 11，👍 0）  
   [agentscope-ai/QwenPaw Issue #5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)  
   **摘要**：Agent 创建的定时任务无报错但无法自动触发，且不能手动编辑。这是影响自动化的关键 Bug，用户反馈使用 v1.1.10 复现，开发团队在评论中要求提供更多日志。目前仍为 OPEN 状态。

2. **#4727 – 迁移后端至 AgentScope 2.0**（评论 10，👍 2）  
   [agentscope-ai/QwenPaw Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)  
   **摘要**：正式提出将 QwenPaw 的后端从 AgentScope 1.x 升级到 2.0，涉及新架构、API 和运行时模型。该议题获得最高赞数，社区呼声强烈，已有关联 PR #5078（Runtime 2.0）为此迈出第一步。

3. **#5140 – 附件下载 404（post2 版本未修复）**（评论 6）  
   [agentscope-ai/QwenPaw Issue #5140](https://github.com/agentscope-ai/QwenPaw/issues/5140)  
   **摘要**：纯文本可下载，但 docx/pdf 等类型返回 404。用户在早期版本报告过，修复后再次出现，表明回归。该 Issue 目前已 CLOSED，但仍有评论讨论。

**分析**：社区主要关注两类诉求：**稳定性和可靠性**（定时任务、附件下载、配置丢失）和 **技术演进**（AgentScope 2.0 迁移）。定时任务和附件下载是高频使用场景，当前问题直接影响用户体验，维护者应优先响应。

---

## Bug 与稳定性

今日报告的 Bug 按严重程度排列（严重→轻微），标注是否已有 Fix PR：

| 严重程度 | Issue | 描述 | 状态 | 关联 Fix |
|----------|-------|------|------|----------|
| 🔴 严重 | #5064 | Agent 定时任务无法自动触发 | OPEN | 无 |
| 🔴 严重 | #5155 | 升级 v1.1.11 后 Docker 环境自动宕机重启 | OPEN | 无 |
| 🔴 严重 | #5161 | 长对话后 QwenPaw 无响应 / 卡死 | OPEN | 无 |
| 🔴 严重 | #5163 | Gemini tool calling 在 v1.1.11.post2 回归（v1.1.10 正常） | OPEN | 无 |
| 🟡 中等 | #5140 | 附件下载 404（除纯文本外） | CLOSED | 已在 post2 尝试修复，但仍有用户报告问题，可能需重新打开 |
| 🟡 中等 | #5137 | 向量模型记忆搜索配置保存后丢失 | CLOSED (已合并 #5144) | ✅ #5144 |
| 🟡 中等 | #5142 | Coding Mode 刷新页面后 Session 回退到第一个 | CLOSED (已合并 #5147) | ✅ #5147 |
| 🟡 中等 | #5098 | 记忆搜索工具在 UI 显示结果异常（unknown等） | CLOSED (已合并 #5154) | ✅ #5154 |
| 🟡 中等 | #5148 / #5143 | 网页 UI 显示根号错误/数学公式渲染问题 | CLOSED | 可能是同一问题已关闭 |
| 🟢 轻微 | #5145 | 执行详情始终展开，干扰输出 | OPEN | 无 |
| 🟢 轻微 | #5162 | 对话思考逻辑进入死循环 | OPEN | 无 |
| 🟢 轻微 | #5166 | Python 3.13 安装 TeamChat 插件因缺失 `imghdr` 失败 | OPEN | 无 |
| 🟢 轻微 | #5165 | 打包后白屏（脚本引用不存在的模块） | OPEN | 无 |

**小结**：定时任务宕机、长对话卡死、回归问题（Gemini）是最高风险项，目前尚无合并的修复 PR；记忆配置丢失、Session 回退、搜索结果显示异常均已通过 #5144 #5147 #5154 得到修复。

---

## 功能请求与路线图信号

用户提出的新功能需求及潜在纳入版本的可能判断：

| Issue | 描述 | 热度 | 关联 PR / 路线图信号 |
|-------|------|------|----------------------|
| #5156 | 支持 `kimi-for-coding` / 加入 `uv` 白名单 | 3 评论 | 无直接关联 |
| #5139 | 增加 Agent Team / 群组协作能力（类似 WorkBuddy 专家团队） | 3 评论 | Agent OS Driver (#5067) 已提出统一外部能力抽象（MCP/A2A/ACP），可能作为基础 |
| #5167 | 优化飞书 CardKit 流式卡片长回复刷新慢 | 1 评论 | 无直接关联 |
| #5164 | 桌面版系统托盘、开机自启、后台常驻与管理 | 2 评论 | 与 Tauri/ pywebview 客户端优化相关，近期有 #5153 优化 pywebview 启动速度 |
| #5152 | Slack 频道支持 | 1 评论 | 项目已有多个频道（DingTalk、Feishu、QQ 等），新增 Slack 属于频道拓展，技术难度中等 |
| #5088（PR） | 初始治理与沙箱接口讨论 | Under Review | 偏向底层基础设施，可能推进更安全的插件/代码执行 |
| #5067（PR） | Agent OS Driver 统一抽象（MCP/A2A/ACP） | Under Review | 路线图级特性，与 Agent 生态系统互操作性相关 |
| #4622（PR） | DataPaw 数据分析插件 | Under Review | 扩展插件生态 |
| #5069（PR） | 文本模型回退视觉模型（图片转文字） | OPEN | 增强多模态支持 |

**判断**：短期内最有可能下个版本（1.1.12）纳入的包括 **Agent OS Driver** 和 **DataPaw 插件**（均已处于 Review 状态），以及 **视觉模型回退**。用户呼声较高的 **Agent 协作** 可能依赖 Runtime 2.0 的 ToolCoordinator 进一步演化。飞书卡片优化和桌面增强属于持续改进项。

---

## 用户反馈摘要

从 Issues 评论及描述中提取的真实用户声音：

- **定时任务不可用**：“流程执行无异常……但任务到达设定时间点后，无法自动触发执行……不支持手动编辑操作” —— #5064，说明该功能在用户工作流中不可或缺。
- **附件下载反复异常**：“最早 v1.1.11 版本纯文本点击不会弹出下载对话框……后续版本修复了。但是纯文本以外的文件，点击下载会报错 404！” —— #5140，用户对修复的递进和回退感到困扰。
- **配置丢失迷惑**：“如果修改了此界面设置，且未展开自动记忆搜索和向量模型配置卡片，点击保存自动搜索记忆配置丢失” —— #5137，UI/UX 设计导致隐藏字段无法保存，已修复。
- **升级后稳定性下降**：“docker 环境部署，时不时会自动宕机重启” —— #5155；还有用户报告长对话后无响应 #5161。
- **Gemini 回归**：“On v1.1.10, Gemini tool calling works correctly. After upgrading to .post2, it does not work.” —— #5163，显示回归测试不足。
- **飞书卡片反馈**：“短回复还好，回复一长就会明显变慢，看起来像一个字一个字往外吐……影响可用性” —— #5167，用户对流式体验要求高。
- **打包构建问题**：“qwenpaw.spec 中引用了两个不存在的模块……打包出来 exe 安装启动后就白屏” —— #5165，影响桌面版部署。
- **死循环**：“对话思考逻辑进入死循环” —— #5162，严重影响交互。
- **积极建议**：“希望增加 Agent Team / Swarm 协作能力”、“希望支持 kimi-for-coding”、“希望完善桌面版系统托盘、开机自启” —— 用户期待项目向平台化发展。

---

## 待处理积压

以下为长期未响应或重要但未合并的 Issue/PR，提醒维护者关注：

| 编号 | 标题 | 当前状态 | 持续时间 | 建议 |
|------|------|----------|----------|------|
| #4727 | [Breaking Change] 迁移后端至 AgentScope 2.0 | OPEN，已有 #5078 PR | 创建 2026-05-27（已 17 天） | 与 #5078 Runtime 2.0 合并后需整体规划迁移步骤 |
| #4900 | Decouple plugin loader initialization from agent startup | OPEN（Under Review） | 创建 2026-06-02（已 11 天） | 解决 PyInstaller/Tauri 环境下插件加载失败的关键修复 |
| #4622 | plugin(datapaw): add data-analysis plugin | OPEN（Under Review） | 创建 2026-05-22（已 22 天） | 新插件贡献，Review 周期较长，建议加速 |
| #5067 | Agent OS Driver 统一抽象 | OPEN（Under Review） | 创建 2026-06-10（已 3 天） | 路线图级设计，需广泛讨论，但应避免无限期搁置 |
| #5064 | Agent 定时任务无法触发 | OPEN，评论数多 | 创建 2026-06-10（已 3 天） | 用户高频遭遇，开发团队已在评论中要求日志，建议优先安排开发 |
| #5155 | 升级 v1.1.11 后自动宕机重启 | OPEN，无回复 | 创建 2026-06-12（1 天） | 可能性严重，需迅速排查 |
| #5163 | Gemini tool calling 回归 | OPEN，用户已定位 | 创建 2026-06-12（1 天） | 明确回归范围，建议立即回滚或 hotfix |

> **说明**：所有 Issue/PR 链接均基于数据源 `agentscope-ai/QwenPaw`。部分 PR 的评论数未显示视为正常。

---

*本报告由 AI 根据 GitHub 公开数据自动生成，旨在辅助决策。具体细节请参阅对应 GitHub 链接。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是为您生成的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 — 2026-06-13

## 1. 今日速览

过去 24 小时内，项目保持了高度活跃的状态，共产生 **12 条 Issue 更新** 和 **36 条 PR 更新**。尽管无新版本发布，但待合并 PR 高达 **32 条**，反映出社区贡献者参与热情持续高涨，项目正处于密集的合并冲刺期。维护团队响应迅速，针对几个 **S1 级阻塞性 Bug** 均已快速提交了修复 PR。架构层面，关于统一 Agent turn 引擎的 **RFC #7415** 已获得维护者明确指导并进入具体实施阶段，标志着核心运行时的重大统一迈出关键一步。总体来看，项目健康度良好，迭代节奏快，但在新手入门体验和特定平台（macOS）的稳定性上仍需加强。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日有 **2 个 PR 被合并/关闭**，1 个重要功能 Issue 正式关闭，推进了项目在多方面的实质性进展：

-   **PR #7447 (已合并)**：**修复 OpenAI 及兼容端点超时问题**。该 PR 解决了原生 OpenAI Provider 硬编码 120 秒超时的问题，使其正确读取用户配置的 `timeout_secs` 字段。这对于连接慢速本地模型（如 llama.cpp, vLLM）的用户至关重要，避免了请求无声中断。 关联 Issue: [#6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723)
-   **PR #7548 (已合并)**：**依赖清理与代码优化**。这是一次大规模的 Chore 操作，涉及 Cargo 依赖和代码清理，有助于减少维护成本并提升编译效率。
-   **Issue #6443 (已关闭)**：**Twitch 聊天频道功能已被正式接受并关闭**。该功能通过 IRC 适配器集成 Twitch 聊天，是项目在直播和社区场景上的重要拓展。

此外，今日还有多个关键的修复类 PR 被提交，极大地改善了项目的稳定性和体验，包括修复 Docker 构建失败 (`#7534`)、修复 Windows 自更新失败 (`#7528`, `#7530`)、修复 `ask_user` 工具错误 (`#7551`)、以及对 MCP 工具自动发现 (`#7547`) 和插件安装路径 (`#7549`) 的修复。

## 4. 社区热点

-   **🔥 最受关注：RFC #7415 — 统一 Agent Turn 引擎**
    -   **链接**: [Issue #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)
    -   **分析**: 该 RFC 提议将 `run_tool_call_loop`、`turn_streamed` 和 `Agent::turn` 三个独立引擎统一为一个。此提案获得了 **3 条评论**，成为过去一天讨论最集中的议题。维护者在评论中明确指示放弃分阶段迁移的原计划，直接通过一个 **单一合并 PR (#7540)** 完成统一。这反映了项目组对简化核心架构、降低技术债务的决心，对未来开发者和内部逻辑的演进影响深远。社区对这一架构变更表现出积极关注。

## 5. Bug 与稳定性

在过去 24 小时内，共有 **6 个 Bug 被报告**，其中 **5 个为 S1 级（工作流阻塞）**，严重程度较高。维护团队响应迅速，已为其中 **3 个 Bug** 提交了修复 PR。

| 严重程度 | Issue | 问题描述 | 相关 Fix PR |
| :--- | :--- | :--- | :--- |
| **S1 (阻塞)** | [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | Web Dashboard 不可用 | 暂无 |
| **S1 (阻塞)** | [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | `zeroclaw quickstart` 命令安装失败 | 暂无 |
| **S1 (阻塞)** | [#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) | Docker 构建失败，缺少 C++ 编译器 | [PR #7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534) (Open) |
| **S1 (阻塞)** | [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS 应用无响应、窗口消失 | 暂无 |
| **S1 (阻塞)** | [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | `ask_user` 工具在 WebSocket 会话中失败 | [PR #7551](https://github.com/zeroclaw-labs/zeroclaw/pull/7551) (Open) |
| **S2 (降级)** | [#7541](https://github.com/zeroclaw-labs/zeroclaw/issues/7541) | V3 路径重命名后，仍错误使用 `data_dir` 作为工作区目录 | 暂无 |

**要点**：`ask_user` (#7542) 和 Docker 构建 (#7533) 问题已在报告后数小时内得到修复 PR，展示了极高的响应率。但 Dashboard (#7523)、macOS 应用 (#7527) 和安装体验 (#7537) 是当前亟待解决的用户体验痛点。

## 6. 功能请求与路线图信号

今日收到 **3 个新增强请求**，反映了用户对扩展使用场景的强烈需求：

-   **Multi-session 支持 (Issue #7543)**：用户 `NiuBlibing` 提出了在 Web Chat UI 中增加多会话管理（新建/切换/重命名/删除）。这被视作当前单一会话模式的重大改进，有望提升聊天界面的可用性。
-   **llama.cpp 模型路由 (Issue #7539)**：用户希望在运行时能够快速切换不同的本地模型。这直接解决了本地推理时一个模型无法满足所有任务的痛点，对本地部署场景是重要补充。
-   **流式卡片消息 (Issue #7531)**：针对 QQ/DingTalk/WeChat/Feishu 等渠道，提出增加流式卡片消息以降低用户等待焦虑。这表明用户正在深度使用这些渠道的高级特性，对交互体验要求更高。

**路线图信号**：结合已存在的 `v0.8.1` 集成追踪器 (Issue #6970) 来看，下一个版本的重点仍在集成扩展和外挂能力上，而 `#7543` 和 `#7539` 等请求则指向前端 UI 和本地体验的优化，可能成为后续版本的重要方向。

## 7. 用户反馈摘要

从今日的 Issue 评论和摘要中，可以提炼出以下用户声音：

-   **新手入门受挫**: 用户 `hejiangda` (#7537) 在尝试 `zeroclaw quickstart` 时遇到配置报错 `no map-keyed/list section at peer-groups`，反馈称“新用户无法创建 Agent”，这表明初始化流程的容错性和引导信息有待优化。
-   **macOS 平台兼容性堪忧**: 用户 `swellee` (#7527) 详细描述了 macOS app 在权限授权、页面加载和窗口重显上的全面失效问题，该报告严重影响了 macOS 用户群的信心和采纳度。
-   **Dashboard 引导存在误导**: 用户 `luckbyte` (#7523) 指出通过 brew 安装后，Web Dashboard 不可用，但 `cargo web build` 的入口并不直观，且启动日志中打印的 URL 缺乏实际验证，形成了体验落差。
-   **错误信息导致信任危机**: 用户 `NiuBlibing` 在提交 Bug (#7542) 的同时，特别指出 `ask_user` 失败时返回的 `“Channel closed before receiving a response”` 错误信息具有误导性，并非真实问题，这降低了用户对工具可靠性的信任。

## 8. 待处理积压

以下为需要维护者和社区重点关注、推动解决的问题：

-   **等待作者响应的 PR（有搁浅风险）**：
    -   [PR #7351](https://github.com/zeroclaw-labs/zeroclaw/pull/7351): MCP 重连功能，标签为 `needs-author-action`。
    -   [PR #7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245): 修复 `read_skill` 无法加载插件捆绑技能，同样等待作者操作。
-   **S1 严重 Bug 尚无关联 Fix**：
    -   [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523): Dashboard 不可用问题。
    -   [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537): quickstart 安装失败问题。
    -   [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527): macOS 应用崩溃问题。
-   **高风险/大规模 PR，需谨慎审查**：
    -   [PR #7429](https://github.com/zeroclaw-labs/zeroclaw/pull/7429): 引入 wasmtime 依赖和 feature flags，作为未来取代 Extism 的铺垫。该变更风险高、范围大，可能影响整个插件系统架构，需要社区核心成员进行深入的架构评审。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*