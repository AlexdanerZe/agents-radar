# OpenClaw 生态日报 2026-06-19

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-19 03:59 UTC

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

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的 `openclaw/openclaw` 数据，生成了 **2026-06-19** 的项目动态日报。

---

## OpenClaw 项目动态日报 — 2026-06-19

### 1. 今日速览
今日项目活跃度极高：24小时内更新了 **500个 Issues** 和 **500个 PRs**，机器人自动化运维系统（`clawsweeper` 标签）运转流畅。然而，高活跃度背后暴露出严峻的稳定性挑战。今日曝出 **P0级数据丢失 Bug**（`#84882`），同时存在大量 P1 级会话状态（`session-state`）和消息丢失（`message-loss`）问题。尽管 Bug 风暴持续，社区修复响应十分迅速，今日合并/关闭了 **53个 PR**，修复了包括会话活锁、频道兼容性在内的多项严重问题。项目当前处于 **“紧急修复+高频迭代”** 的大版本前夜状态。

### 2. 版本发布
今日无新版本发布。

### 3. 项目进展
今日修复和合并的 PR 集中在 **核心稳定性** 与 **渠道兼容性** 两大战线：
- **关键会话稳定性修复（已合并）：**
  - **`fix(context-engine): resolve turn-maintenance livelock on Telegram DM sessions`** (`#86898`)：此 PR 的合并是对 Telegram 频道重度用户的一剂强心针，直接解决了高流量下的会话线程死锁问题。
  - **`fix: prevent toolDiscovery from overwriting pinned channel registry`** (`#87333`)：修复了前端调用时可能清空已固定的频道注册表的问题，保障了插件工具集的完整性。
- **渠道生态成熟度提升：**
  - **Feishu（飞书）渠道完善**：今日有多项针对飞书的更新，包括修复点对点回复失败 (`#94760`) 和支持出站消息速率限制配置 (`#94614`)，标志着该渠道正逐步走向生产可用。
  - **Telegram 优化**：修复了富文本 HTML 表格的转义 Bug (`#94777`)。
  - **LINE/WebChat 修复**：为 LINE 的媒体下载添加了超时机制 (`#86873`)；修复了 WebChat 中 TTS 语音广播未发送的问题 (`#86759`)。
- **开发者体验与代码质量：**
  - **Sandbox（沙箱）路径修复**：确保新创建的 Agent 工作区能正确识别技能目录 (`#94782`)，解决了 `#94425` 问题。
  - **Agent 工具增强**：暴露 Perplexity 搜索的上下文大小参数 (`#94757`)；增加默认工具结果截断阈值 (`#94739`)。

### 4. 社区热点
今日社区讨论的核心围绕 **“数据完整性”** 和 **“会话可靠性”** 展开：

- **P0 数据丢失引发恐慌**：`#84882` (memory-core 静默删除记忆文件) 虽然仅6条评论，但 P0 的严重级别使其成为今日社区情绪最紧绷的议题。用户对 AI 记忆体数据安全产生了信任危机。
- **长期功能需求呼声极高**：
  - `#54531` (强制回复到原始频道)：11条评论，自3月提交以来持续被顶。用户对于在 Telegram/Discord/WhatsApp 间切换时消息路由丢失的体验非常不满，这已成为多频道用户的核心阻塞点。
  - `#59330` (Control UI Raw模式)：尽管已关闭，但收获了14个 👍。用户对于 UI 表单模式限制配置的灵活性感到沮丧，社区对“完整控制权”的需求强烈。
- **插件生态摩擦**：`#85030` (MCP 工具未注入子 Agent)，8条评论。用户对复杂的配置规则感到困惑，要求更直观的跨会话工具注入机制。

### 5. Bug 与稳定性
今日 Bug 形势严峻，**P0/P1级别问题呈井喷状态**，主要集中在会话、消息和数据层：

| 严重度 | Issue | 摘要 | 状态 |
| :--- | :--- | :--- | :--- |
| **🔥 P0** | `#84882` | memory-core 梦境处理**静默删除**每日记忆文件 | ✅ 开放，**无 Fix PR** |
| **🔴 P1** | `#86538` | 会话写锁超时，阻塞所有子代理通道 | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#86519` | 2026.5.20 更新后 Telegram 消息重复 2-10 次 (回归) | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#85103` | 提供商配额耗尽后，模型回退链未触发 | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#84903` | 单个 Agent 会话阻塞整个 Gateway 事件循环 (隔离失效) | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#84516` | Codex 长回复被静默截断 (~1000字符) | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#85030` | MCP 工具未注入到子 Agent 会话 | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#84610` | WSL2 升级后 Gateway 进入 SIGTERM 无限重启循环 | 🟡 开放，**无 Fix PR** |
| **🔴 P1** | `#94750` | Discord 群组会话重置后丢失近期对话上下文 | 🟡 开放，**无 Fix PR** |

**已有 Fix PR 在途的高优 Bug：**
- **`#86900` (P2)**：为模型不可用时添加熔断器，防止 Token 无谓消耗。
- **`#86893` (P1)**：修复孤立 Cron 任务冷启动超时问题。
- **`#86764` (P1)**：修复在外部运行器失败前，用户消息未持久化的问题。
- **`#86759` (P2)**：修复 WebChat TTS 最终负载未广播问题。

### 6. 功能请求与路线图信号
今日 PR/Issues 指向了未来版本的几个关键方向：

- **平台化与插件 SDK**：`#81913` (暴露稳定插件 SDK 接口) 和 `#81061` (预路由 Hook) 的讨论热度不减，表明 OpenClaw 的定位正在从单一应用向“Agent 平台”演进。
- **Webhook 与自动化集成**：`#11665` (Webhook 会话复用) 是打通外部系统多轮对话的基石，尽管是2月提出的老 Issue，其解决优先级应随平台化战略提高。
- **安全与沙箱**：`#7722` (文件系统沙箱配置) 和 `#81185` (隐去 Exec 工具返回结果) 的推进，意味着项目开始严肃对待安全边界和权限控制，这是企业级部署的必要条件。
- **基础设备重构**：`#86237` (重命名 Cron 子系统避免与系统 Cron 冲突) 虽然等级为 P3，但这关乎长期运维和开发者体验，体现了项目团队对持续重构的投入。

### 7. 用户反馈摘要
从今日 Issue 评论中提炼出的生存用户画像和痛点：

- **“我的回忆不见了”**：P0 Bug `#84882` 的评论中充满了对数据安全的后怕。用户信任建立在绝对的数据安全之上，这类错误是致命的。
- **“升级就崩”**：用户 `w3-design1` 投诉 `2026.5.20` 更新后 Telegram 出现了严重的回复重复；用户 `orionnexor-wq` 报告 WSL2 环境升级后 Gateway 彻底不可用。**升级回归已成为当前用户满意度最大的减分项。**
- **“机器人和我，总有一个在等待”**：用户 `Sylaaaaas` 报告的一个 Agent 阻塞导致全体调度瘫痪（`#84903`），暴露了资源隔离的设计瑕疵。这反映了用户对**高并发可靠运行**的刚需。
- **“配置复杂，容易出错”**：用户 `mlaihk` 和 `jguida941` 分别报告了配置自动错误 (`authProfileOverride`) 和文档/运行时不一致 (iOS plist)。这反映了配置层在灵活性和易用性之间的平衡还有待优化。

### 8. 待处理积压
以下为长期未得到有效解决、但关乎项目健康度和核心体验的高优议题，提醒维护团队重点关注：

- **核心功能缺陷（超2个月）：**
  - `#11665` (Feb 8, P2)：Webhook 会话复用未实现，**违返文档**。这是第三方集成的硬伤。
  - `#7722` (Feb 3, P2)：文件系统沙箱配置需求，至今停留在设计讨论阶段。
- **社区呼声极高的功能缺口（超1个月）：**
  - `#54531` (Mar 25, P1)：强制回复到原始频道。这是构建跨平台无障碍交流的最后一块拼图。
  - `#81061` (May 12, P2)：预路由编辑钩子。它是插件生态实现复杂桥接与代理的基础。
- **待审查的高风险修复 PR：**
  - `#81185` (May 12, P1)：隐去 Exec 工具结果负载（安全性高，影响面大，等待 Maintainer 审查）。
  - `#86900` (May 26, P2)：为摘要器添加熔断器（防止 Token 耗尽，逻辑清晰，建议优先合入）。
  - `#86764` (May 26, P1)：持久化用户轮次消息（修复关键数据丢失路径，等待 Maintainer 审查）。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告（2026‑06‑19）

## 1. 生态全景

过去24小时，个人AI助手/自主智能体开源生态呈现**高度活跃、分化加速**的态势。以OpenClaw、IronClaw、ZeroClaw、CoPaw为代表的头部项目维持了每日数百条Issue/PR的更新量，社区贡献者和维护团队正合力将功能原型推向生产级稳定。然而高频迭代也导致**稳定性问题集中爆发**——多个项目同时出现数据丢失、会话死锁、上下文压缩崩溃等严重Bug，表明整个生态仍处于“规模扩张优先于质量巩固”的前商业化阶段。渠道适配（Telegram、飞书、Discord、微信）成为各项目的基础标配，差异化竞争点逐渐转向**成本优化、多Agent治理、安全沙箱和开发者体验**。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PRs 更新数 | 版本发布（今日） | 健康度评估 |
|------|--------------|------------|----------------|------------|
| **OpenClaw** | 500 | 500 | 否 | 🔴 极活跃但P0数据丢失；大版本前夜 |
| **NanoBot** | 3（新） | 24处理（5合并） | 否 | 🟢 良好，快速演进，待合并积压 |
| **Hermes Agent** | 50 | 50 | 否 | 🟡 活跃，网关稳定性修复，多平台对齐 |
| **PicoClaw** | 2 | 14（7合并） | nightly v0.3.0 | 🟡 中等偏高，安全修复为主 |
| **NanoClaw** | 5 | 21（6合并） | 否 | 🟡 高产但权限漏洞紧急，15个PR待合 |
| **NullClaw** | 4 | 4（0合并） | 否 | 🟡 中等，核心修复待评审，文档贡献 |
| **IronClaw** | 31 | 43（17合并） | 否 | 🟢 极高，工程化冲刺，功能落地快 |
| **LobsterAI** | 2 | 15（14合并） | **v2026.6.18** | 🟢 高，语音与Computer Use迭代密集 |
| **TinyClaw** | 0 | 0 | 否 | ⚪ 无活动 |
| **Moltis** | 1 | 0 | 否 | 🔴 极低，单Issue反馈，无维护响应 |
| **CoPaw (QwenPaw)** | 44 | 28（13合并） | **v1.1.12.post1** | 🟡 高位，上下文压缩冻结等严重Bug突出 |
| **ZeptoClaw** | 0 | 0 | 否 | ⚪ 无活动 |
| **ZeroClaw** | 50 | 50 | **v0.8.1** | 🟢 积极，密集修复，向生产环境转型 |

> 注：Issue/PR更新数为过去24小时GitHub活动计数，包含新建、评论、标签变更等；版本发布指正式版或预发布。健康度评估综合活跃度、Bug严重性、修复响应速度和社区反馈情绪。

---

## 3. OpenClaw 在生态中的定位

**核心参照地位稳固，但稳定性危机拉低信任分。** OpenClaw 以500级的日更新量稳居生态活跃度榜首，其“核心框架+插件化”的架构为整个生态提供了最灵活的实验场。与同类项目相比，优势在于：

- **社区规模最大**：Issue/PR数量远超其他项目，贡献者生态最丰富。
- **功能覆盖面广**：从记忆系统、上下文管理到多渠道、Webhook、沙箱，几乎覆盖所有前沿方向。
- **技术路线领先**：当前正从“单一聊天应用”向“Agent平台”演进（插件SDK、Webhook复用、预路由Hook），这一定位比NanoBot/Hermes更接近通用基础设施。

但短板同样显著：**P0级数据静默删除（#84882）** 和大量P1会话丢失问题直接动摇了用户信任，而Hermes Agent和ZeroClaw在相同痛点上的修复响应更快。相比之下，OpenClaw的“紧急修复+高频迭代”模式更像是在“边飞边修”，适合追逐前沿的开发者，却可能将注重稳定的用户推向专攻企业级可靠性的项目（如IronClaw、ZeroClaw的v0.8.x系列）。

---

## 4. 共同关注的技术方向

### 🔷 上下文管理与会话连续性
| 项目 | 具体诉求 |
|------|----------|
| **OpenClaw** | 会话写锁超时、消息丢失、memory-core静默删除（#84882） |
| **NanoBot** | 上下文整合清洗Agent自身消息，用户追问丢失（#4307） |
| **Hermes Agent** | 上下文压缩后/Goal状态丢失（#33618） |
| **CoPaw** | 上下文压缩导致进程冻结、上下文被清空（#5218, #5171） |
| **ZeroClaw** | 默认32k上下文被工具定义耗尽（#5808） |

会话是AI助手的“工作记忆”，当前没有一个项目能完全解决长对话下的可靠压缩与恢复，这是全生态最集中的技术债。

### 🔷 多渠道/多平台原生体验
几乎所有项目都在优化Telegram、飞书、Discord、微信等渠道的渲染一致性（表格、按钮、卡片）。例如Hermes Agent为Slack/飞书引入原生表格组件；ZeroClaw增加Discord交互组件；CoPaw修复飞书群聊回复错乱。这表明集成广度已成基线，**渠道深度体验**才是下一阶段竞争点。

### 🔷 安全沙箱与权限隔离
| 项目 | 举措 |
|------|------|
| **OpenClaw** | 文件系统沙箱配置（#7722） |
| **NanoBot** | bwrap沙箱添加额外绑定根（#4404） |
| **PicoClaw** | 修复web_fetch SSRF绕过（#3143） |
| **NanoClaw** | 非所有者创建子Agent权限漏洞（#2807） |
| **CoPaw** | 基于bubblewrap的Linux沙箱（#5310） |
| **ZeroClaw** | 工具权限逃逸修复、`execute_pipeline`安全策略（#7960） |

随着Agent能执行代码和网络操作，沙箱已从“可选”变为“刚需”。

### 🔷 成本优化与模型路由
- **NanoBot** 合并`consolidation_model`字段，允许记忆整合使用更便宜模型。
- **ZeroClaw** 捕获调度/CLI模型成本（#5221修复）。
- **IronClaw** 将LLM使用量纳入CostGuard监控（#4989）。
- **CoPaw** 社区提议集成Headroom可逆压缩减少60-95% token消耗（#5063）。

用户不再满足于单一模型调用，开始要求“智能体根据任务重要性自动选择模型”。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 通用Agent平台、无限扩展 | 技术发烧友、集成开发者 | 原生插件SDK + Webhook + 沙箱，自下而上开放 |
| **NanoBot** | 低门槛聊天机器人、飞书生态 | 中小团队、飞书用户 | 极简配置、CLI一键接入，主打“30分钟上线” |
| **Hermes Agent** | 企业级编排、桌面端体验 | DevSecOps、专业效率用户 | 网关/REST设计优先，Doer/Reviewer双角色，Cron成熟度高 |
| **PicoClaw** | 轻量安全、嵌入式场景 | 资源受限设备（Sipeed硬件） | 偏硬件原生，依赖升级自动化，Go语言 |
| **NanoClaw** | 多Agent治理与审批 | 企业IT管理员 | 消息级审批、群组权限模型，强调安全合规 |
| **NullClaw** | 极简核心、自托管 | 边缘计算、定制化开发者 | 使用Zig语言，A2A协议，可跑在ESP32目标 |
| **IronClaw** | 工作流自动化与定时触发 | 业务运维、CI/CD场景 | Reborn引擎 + 审批流 + Projects管理，偏向“AI Cron” |
| **LobsterAI** | 桌面客户端、语音+Computer Use | 个人效率、办公场景 | Electron桌面 + 实时ASR + Windows自动化，面向C端体验 |
| **CoPaw** | 大而全的全家桶 | 深度技术用户、社区 | AgentScope 2.0原生压缩 + MCP服务池 + 视觉模型路由 |
| **ZeroClaw** | 企业生产部署（OIDC/成本监控） | 商业客户、大规模部署团队 | v0.8.x稳定化补丁 + 统一成本追踪 + 插件认证架构 |

各项目在“易用性 vs 灵活性”、“轻量 vs 全功能”光谱上的站位日趋清晰，用户选择成本正在降低。

---

## 6. 社区热度与成熟度分层

### 🔥 第一梯队：极活跃但尚未稳定
- **OpenClaw** · **IronClaw** · **ZeroClaw** · **CoPaw**
- 日更新量40+，社区讨论热烈，功能迭代密集。
- 成熟度：仍处于早期快速扩张，严重Bug频发，但修复响应也快。适合愿意尝鲜并参与反馈的核心用户。

### 🔹 第二梯队：高活跃、功能细化
- **NanoBot** · **Hermes Agent** · **NanoClaw** · **LobsterAI**
- 日更新量5-30条，团队与贡献者比例均衡，功能落地稳定。
- 成熟度：开始关注工程化（CI/CD、文档国际化、依赖升级），生产可用性有所保障。

### ✳️ 第三梯队：中等活跃、专项突破
- **PicoClaw** · **NullClaw**
- 日更新量个位数，但核心修复质量高（如SSRF、流式Tool Calls）。
- 成熟度：小而精，在特定方向（硬件、轻量核心）有独特价值。

### ⚪ 休眠/低活跃
- **TinyClaw** · **Moltis** · **ZeptoClaw**
- 24小时内几乎无活动。或项目已停滞，或处于架构重写期。建议用户谨慎选用。

---

## 7. 值得关注的趋势信号

### 📌 “数据连续性是第一生命线”
P0 Bug（静默删除记忆、上下文整合丢失）在多项目集中出现，说明当前上下文管理算法（统计式/简单压缩）已到极限。**可逆压缩（如Headroom提案）或将很快成为标配**。

### 📌 渠道集成从“能用”进入“好用”阶段
原生表格、交互组件、扫码注册（NanoBot飞书）暗示用户不再容忍生硬的消息转发。**渠道原生 SDK 的封装深度**将决定Agent在即时通讯工作流中的替换成本。

### 📌 Agent 能力碎片化下的统一治理诉求
多Agent审批（NanoClaw）、双角色编排（Hermes）、消息路由（OpenClaw #54531）共同指向一个问题：**当Agent变多，谁来决定哪个Agent做什么**？面向企业场景的权限模型和编排框架是蓝海。

### 📌 开发者体验成为留存关键
升级后配置重置（CoPaw）、CLI管道不兼容（ZeroClaw #4721）、配置文档缺失（IronClaw WeCom）等高频投诉表明：**用户愿意尝鲜，但不会忍受反复的“配置考古”**。项目需要从发布流程上内建迁移工具和兼容性测试。

### 📌 边缘/离线部署需求开始浮现
NullClaw的ESP32支持、PicoClaw的轻量定位、NanoClaw的Apple Container运行时——虽然这些需求当前用户量不大，但折射出**AI Agent“靠近数据源”**的趋势，可能会催生更轻量的运行时标准。

---

*报告基于2026-06-19 GitHub公开数据生成。所有判断均来自当日项目活动，不代表对项目长期质量的全面评估。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的NanoBot (HKUDS/nanobot) 项目数据，为您生成了2026年6月19日的项目动态日报。

---

### **NanoBot 项目动态日报 | 2026年6月19日**

---

#### **1. 今日速览**

项目今日活跃度极高，尤其是在代码贡献方面。过去24小时内，共有24条Pull Requests被处理，显示出开发社区的强劲动力。尽管有5个PR被合并或关闭，但仍有19个PR处于待合并状态，表明项目正处于密集的功能开发和迭代期。与此同时，新提交的3个Issues主要关注并发安全和工作区体验等核心稳定性问题，社区反馈集中在提升生产环境的可靠性和用户体验一致性上。总体来看，项目健康度良好，处于快速演进阶段。

#### **2. 版本发布**

无。

#### **3. 项目进展**

今日共有5个重要PR被合并或关闭，标志着项目在功能优化、通道扩展和技术债务清理方面取得了实质进展：

- **模型层优化**：PR [#1391](https://github.com/HKUDS/nanobot/pull/1391) 合并，新增 `consolidation_model` 字段。该特性允许内存整合（memory consolidation）和心跳决策等成本敏感操作路由到更便宜的模型（如小模型），对于需要运行昂贵主模型（如Opus）的部署场景尤为关键，可显著降低运营成本。
- **通道与用户体验**：PR [#4391](https://github.com/HKUDS/nanobot/pull/4391) 合并，为飞书（Feishu/Lark）通道增加了**扫码创建Bot**的CLI命令。这一改进极大简化了飞书机器人的注册流程，用户无需手动创建应用和寻找凭证，显著降低了飞书通道的接入门槛。
- **第三方集成优化**：PR [#4403](https://github.com/HKUDS/nanobot/pull/4403) 合并，将 Firecrawl 数据抓取工具转换为无需API密钥的托管MCP集成。这简化了Web数据分析类应用的配置，提升了开发者体验。
- **工程效能提升**：PR [#4400](https://github.com/HKUDS/nanobot/pull/4400) 合并，优化了CI/CD流程，对仅涉及文档页面的变更跳过CI检查。此举有助于加快文档类PR的合并速度，并减少不必要的CI资源消耗。

#### **4. 社区热点**

今日社区讨论最活跃的议题是 **Issue [#4307](https://github.com/HKUDS/nanobot/issues/4307)**，标题为“Bug: Post-turn consolidation wipes the agent's own delivery message — user follow-up references are lost”。该问题获得了3条评论，是今日讨论最集中的议题。

**分析**：该Bug描述了当一个长对话轮次（multi-iteration turn）发生的上下文超过配置的 `context_window_tokens` 后，系统在回合结束时触发的上下文整合（consolidation）机制，会错误地“清洗”掉智能体自身发送的消息。这直接导致用户后续的追问丢失了上下文引用。问题的核心争议在于整合发生的时机和对象：用户认为应该在“整合发生时”而非“回合结束时”处理，且不应影响智能体自身用于维持对话历史的交付消息。此问题触及了**核心上下文管理机制**，影响了长对话和复杂任务的连续性体验，是社区高度关注的关键痛点。

#### **5. Bug 与稳定性**

今日报告的Bug严重性不一，主要集中在下游消息处理和并发安全性上：

1.  **[严重] 上下文整合错误**：**Issue [#4307](https://github.com/HKUDS/nanobot/issues/4307)** 报告了在上下文窗口被触发整合后，智能体的自我交付消息被清除，导致用户追问丢失上下文。此Bug直接影响对话的连续性和任务执行的可靠性。虽然尚无对应修复PR，但该议题讨论热度高，预计会很快得到处理。
2.  **[严重] 并发安全漏洞**：**Issue [#4408](https://github.com/HKUDS/nanobot/issues/4408)** 报告了 `Nanobot.run()` 的每运行钩子（per-run hooks）非并发安全，因为共享的 `_extra_hooks` 会被覆盖，可能导致在多任务或高并发场景下出现数据竞态和不可预测的行为。此问题直接影响生产环境的稳定性。
    - **已有修复 PR**：[#4409](https://github.com/HKUDS/nanobot/pull/4409) 已作为草案（draft）提交，试图通过将per-run hooks传递给 `process_direct` 而非修改共享状态来解决此问题。
3.  **[中等] 工作区文件读写不对称**：**Issue [#4374](https://github.com/HKUDS/nanobot/issues/4374)** 指出，项目工作区（project workspaces）功能在读取 `SOUL.md` 和 `USER.md` 时能正确指向项目根目录，但写入时却错误地写到了默认工作区，造成了读写路径的不一致。这会破坏项目工作区的私有性和配置隔离。
    - **已有修复 PR**：[#4387](https://github.com/HKUDS/nanobot/pull/4387) 正在等待合并，该PR修改了上下文管理逻辑，使其在项目工作区优先读取本地文件，并在缺失时回退到默认工作区，解决了此不对称问题。

#### **6. 功能请求与路线图信号**

从今日的Issues和PR来看，社区对项目的期望集中体现在以下方面：

- **细粒度配置与控制**：多用户提及对模型行为进行更精细的控制。PR [#1391](https://github.com/HKUDS/nanobot/pull/1391)（已合并）的 `consolidation_model` 和 PR [#4402](https://github.com/HKUDS/nanobot/pull/4402) 的“主动内存整合”（eager consolidation）都指向了**允许用户根据成本、性能需求来分配合成任务**的意向。这可能成为下一版本的一个重要特性。
- **沙箱与执行环境扩展**：PR [#4404](https://github.com/HKUDS/nanobot/pull/4404) 提出为 `bwrap` sandbox增加可配置的额外绑定根，允许在保持沙箱安全性的同时，暴露如 `~/.local/bin` 等用户级别的工具目录。这反映了用户希望在更复杂、更定制化的环境中安全运行代码的需求。
- **简化UI与配置**：PR [#4399](https://github.com/HKUDS/nanobot/pull/4399) 通过 `hidden_settings_sections` 选项允许管理员隐藏WebUI中复杂的设置项，以面向非技术用户提供“傻瓜式”界面。这暗示项目正在考虑更广泛、多元化的用户群体，而不仅仅是开发者。
- **新搜索提供商集成**：PR [#4406](https://github.com/HKUDS/nanobot/pull/4406) （Serper.dev）和 [#4405](https://github.com/HKUDS/nanobot/pull/4405)（Keenable无密钥使用）都旨在增加网络搜索后端的可选项。这表明社区希望有更多、更灵活的搜索方案来替代或作为现有选项的补充。

#### **7. 用户反馈摘要**

从今日的Issues评论中，可以提炼出以下用户反馈：

- **对核心上下文机制的稳定性表示担忧**：在 Issue [#4307](https://github.com/HKUDS/nanobot/issues/4307) 中，用户 `MARJORIESHA-pBAD` 详细描述了由于上下文整合导致的对话丢失问题，并指出当前的实现方式让人对长对话和复杂任务的可靠性产生质疑。他们的反馈充满技术细节，表明这是一个资深用户在进行深度压力测试后发现的根本性问题。
- **对设计一致性的明确批评**：在 Issue [#4374](https://github.com/HKUDS/nanobot/issues/4374) 中，用户 `maximilize` 尖锐地指出了项目工作区功能的读写不对称问题，称之为“read/write asymmetry”。这种精确的术语描述表明用户对系统设计的一致性有很高期望，这种不一致性破坏了他们对功能的基本信任。
- **对并发设计的清醒认识**：Issue [#4408](https://github.com/HKUDS/nanobot/issues/4408) 的提交者 `waelantar` 不仅报告了Bug，还直接点出了根本原因——共享状态的竞态条件，并提交了自己的修复PR [#4409](https://github.com/HKUDS/nanobot/pull/4409)。这显示社区中存在积极参与代码改进、具备高项目主人翁意识的开发者。

#### **8. 待处理积压**

在今日大量PR中，有一个值得长期关注：

- **PR [#4342](https://github.com/HKUDS/nanobot/pull/4342) (feishu WebSocket 卡片内容渲染)**：该PR于6月14日创建，旨在修复飞书通道WebSocket消息中卡片内容显示为占位符的问题。尽管提交较晚，但其累计持续时间为5天，且涉及多方协作渠道的稳定性，建议维护者关注其审核状态，避免长期积压导致该通道用户的使用体验持续受损。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent GitHub 数据生成的 2026-06-19 项目动态日报。

---

## Hermes Agent 项目动态日报 2026-06-19

**分析师备注：** 今日数据截至 2026-06-19，项目活跃度极高，社区讨论与贡献主要集中在网关稳定性、多平台适配（Slack, Feishu, Windows）以及用户体验优化上。

---

### 1. 今日速览

今日项目社区非常活跃，共产生 50 条 Issue 和 50 条 PR 更新。Issue 方面，用户集中反馈了桌面端（TUI/Dashboard）的可用性问题和令人困惑的配置行为，同时提出了诸如“Windows 原生集成”等新需求。PR 方面，项目维护者和社区贡献者并行推进了大量修复和功能增强，尤其集中在**网关稳定性**（修复重启死锁、会话丢失）和**平台适配**（Slack 表格渲染、飞书 CardKit 支持）上。虽然当天没有新版本发布，但大量 PR 的密集提交表明项目正处于快速迭代期，社区贡献活跃，项目健康度良好。

### 2. 版本发布

- **无新版本发布**

### 3. 项目进展

今日虽无新版本发布，但社区贡献的 PR 数量质量俱佳，主要集中在三个方向：**稳定性修复**、**桌面端体验增强**和**平台适配扩展**。

- **网关稳定性修复**：PR #48453 [fix(gateway): avoid self-restart deadlock](https://github.com/NousResearch/hermes-agent/pull/48453) 修复了当通过终端工具调用 `hermes gateway restart` 时可能导致的网关服务死锁问题。PR #48127 [fix(gateway): refresh runtime max_turns before agent creation](https://github.com/NousResearch/hermes-agent/pull/48127) 修复了长期运行的网关服务使用过时的 `max_turns` 配置问题。这两项修复对于保证生产环境的 gateway 可靠性至关重要。
- **桌面端体验增强**：PR #48813 [feat(desktop): Cursor-style agent edit review](https://github.com/NousResearch/hermes-agent/pull/48813) 为桌面应用引入了类似 Cursor 的编辑审核界面，用户可以逐文件接受或拒绝 Agent 的修改。PR #48805 [fix(dashboard): add usage quotas and correct model labels](https://github.com/NousResearch/hermes-agent/pull/48805) 为 Dashboard 增加了用量配额页面并修正了模型标签显示。这些更新显著提升了桌面端的功能完整性和用户控制力。
- **平台适配扩展**：PR #48737 [feat(slack): convert markdown tables to Block Kit table blocks](https://github.com/NousResearch/hermes-agent/pull/48737) 和 PR #48807 [feat(feishu): render markdown tables as CardKit v2 native table components](https://github.com/NousResearch/hermes-agent/pull/48807) 分别优化了 Slack 和飞书平台上的 Markdown 表格渲染，使其更符合平台原生体验。这体现了项目在提升多平台消息质量方面的持续投入。

项目整体正从核心功能构建向**企业级稳定性、精细化用户体验和多平台对齐**迈进。

### 4. 社区热点

今日最受关注的议题体现了用户对**高级编排能力**和**平台集成**的强烈需求。

1.  **Doer/Reviewer 双角色并行编排实践 (Issue #34592)**
    - **链接**: [NousResearch/hermes-agent Issue #34592](https://github.com/NousResearch/hermes-agent/issues/34592)
    - **热议程度**: 5条评论
    - **核心诉求**: 用户分享了一套基于 Hermes Agent 的“Doer + Reviewer”双角色并行架构，并引入了 Hindsight 共享记忆机制。这不仅是简单的需求反馈，更是一个社区贡献的高级最佳实践，展示了 Hermes Agent 在复杂任务编排和 LLM 自我纠错方面的潜力。这反映了社区高阶用户对 Agent 自主性和可靠性的探索。

2.  **MCP Tools 在 TUI 模式下不暴露 (Issue #41625)**
    - **链接**: [NousResearch/hermes-agent Issue #41625](https://github.com/NousResearch/hermes-agent/issues/41625)
    - **热议程度**: 5条评论，1个 👍
    - **核心诉求**: 这是一个典型的“发现”但“不可用”的 Bug，引发了用户的困惑和讨论。MCP 作为扩展 Hermes 能力的重要协议，其工具无法在核心的 TUI 聊天界面中被调用，严重影响了使用体验和工具生态的落地。此问题的高热度表明社区对 MCP 集成的完整性和可靠性非常关注。

3.  **WhatsApp 群发功能指南 (Issue #47477)**
    - **链接**: [NousResearch/hermes-agent Issue #47477](https://github.com/NousResearch/hermes-agent/issues/47477)
    - **热议程度**: 5条评论
    - **核心诉求**: 尽管这是一个已关闭的 Issue，但它是一份详尽的“一键式”操作指南，教用户如何在 Termux 环境下使用 Hermes Skill 发送 WhatsApp 消息。这显示了社区在扩展 Hermes Agent 实用场景（尤其是在移动端或特定环境）上的强大创造力和分享精神。

### 5. Bug 与稳定性

今日报告的 Bug 覆盖了多个组件，严重程度不一，部分已有对应的修复 PR。

| 严重程度 | Issue / PR 编号 | 标题 / 摘要 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **P1 (严重)** | [#48721](https://github.com/NousResearch/hermes-agent/issues/48721) | `hermes update` 在系统 Python 上因 PEP 668 失败 | OPEN | 影响 Homebrew Python 用户，更新功能阻塞。 |
| **P1 (严重)** | [#48746](https://github.com/NousResearch/hermes-agent/issues/48746) | macOS gateway 自重启后陷入僵尸“运行中”状态 | OPEN | 核心问题为 `exit code 75` 与 `launchd` 配置不兼容，导致服务永久挂死。 |
| **P1 (严重)** | [#48519](https://github.com/NousResearch/hermes-agent/issues/48519) | 子配置 gateway 导致会话数据完全丢失 | OPEN | `sessions.json` 有记录但 `state.db` 为空，属于严重数据丢失问题。 |
| **P2 (较高)** | [#33618](https://github.com/NousResearch/hermes-agent/issues/33618) | `/goal` 状态在上下文压缩后丢失 | OPEN | 核心功能的状态持久化问题，因 `session_id` 变更导致。 |
| **P2 (较高)** | [#48083](https://github.com/NousResearch/hermes-agent/issues/48083) | 默认 `--toolsets all` 不加载 web 工具集 | OPEN | 影响本地模型（如 Ollama）的日常使用体验。 |
| **P2 (较高)** | [#45245](https://github.com/NousResearch/hermes-agent/issues/45245) | Cron 调度器使用错误的 API 路由 | OPEN | Cron 任务执行路径错误，影响自动化任务可靠性。 |
| **P2 (较高)** | [#47868](https://github.com/NousResearch/hermes-agent/issues/47868) | 泄露 timestamp 元数据导致严格提供商拒绝 | OPEN | 兼容性问题，可能影响使用部分第三方 API 的用户。 |
| **P1 (已合并)** | [#48453](https://github.com/NousResearch/hermes-agent/pull/48453) | [Fix] 避免网关重启死锁 | **已合并/关闭** | 直接解决了 P1 级别的网关稳定性问题。 |
| **P1 (已修复)** | [#47002](https://github.com/NousResearch/hermes-agent/issues/47002) | v0.16.0 在缺少 trigram tokenizer 的 SQLite 上崩溃 | **已关闭** | 该回归问题已有解决方案。 |

**分析**: 当日报告的 Bug 触角广泛，从核心的状态管理和配置持久化，到特定平台 (macOS) 的系统级兼容性，再到 Cron 和 MCP 等高级功能。其中，**网关稳定性**和**数据持久化/丢失**是当前最突出的问题。好消息是，社区贡献者已经提交了针对网关死锁等关键 Bug 的修复 PR。

### 6. 功能请求与路线图信号

今日用户提出的功能请求呈现出鲜明的发展方向，部分需求已有相应的 PR 跟进。

- **平台兼容性扩展**: 用户 `markwang2658` 提出的 [Windows 原生集成包 (Issue #48716)](https://github.com/NousResearch/hermes-agent/issues/48716) 是一个强烈的信号，表明社区对 Windows 用户的支持有迫切需求，这与项目主要面向 Linux/Docker 的现状形成对比。若采纳，将极大拓宽用户基础。
- **项目管理与状态透明**: 用户 `tymrtn` 提出的 [Mission / Project 源真原语 (Issue #48011)](https://github.com/NousResearch/hermes-agent/issues/48011) 和用户 `byronwsmith-max` 提出的 [/status 应显示活跃模型 (Issue #48715)](https://github.com/NousResearch/hermes-agent/issues/48715) 反映出用户对 Agent 进行更复杂、有状态任务管理的渴望，以及对当前运行状态透明度的需求。这指向了构建更高级的 Agent 管理框架。
- **配置与插件标准化**: [可共享 Profile 模板 (Issue #43784)](https://github.com/NousResearch/hermes-agent/issues/43784) 和 [统一插件路由选择器 (Issue #41190)](https://github.com/NousResearch/hermes-agent/issues/41190) 表明社区希望简化复杂配置，并拥有更灵活的模型/提供商路由能力。这与项目持续优化插件系统和配置结构的路线图是吻合的。

**路线图信号**: 今日大量的 PR，特别是那些优化多平台（Slack, Feishu）体验、增强桌面端 UI 以及提升网关稳定性的 PR，强烈暗示了项目近期路线图的重心：**从核心可行性转向企业级部署的可观测性、稳定性和全平台一致性**。

### 7. 用户反馈摘要

- **痛点与不满**:
  - **配置困惑**: `#48083` 用户指出 `--toolsets all` 不完全生效，令人困惑且不符合预期。
  - **数据丢失**: `#48519` 和 `#33618` 分别报告了会话数据和 Goal 状态在不同场景下的丢失，这是最令用户沮丧的稳定性问题之一。
  - **体验割裂**: `#41625` 报告了 MCP 工具“发现”与“可用”之间的落差，以及 `#48689` 中 `hermes doctor` 给出错误建议，这些都会降低用户信任度。
  - **平台门槛**: `#48716` 的提交者明确表达了 Windows 用户因 `bootstrap.py` 限制而无法使用的挫折感。
- **满意与赞赏**:
  - 高阶用户乐于分享先进实践，如 `#34592` 的 Doer/Reviewer 架构。这表明项目底层架构的灵活性得到了核心用户的认可。
  - 用户对专为该平台定制的功能有积极反馈，如 `#47477` 的 WhatsApp 集成指南，展示了社区的自驱力和创造力。

### 8. 待处理积压

以下是一些可能被维护者忽视但值得关注的长期议题：

1.  **TUI 国际化框架 (PR #23243)**
    - **链接**: [NousResearch/hermes-agent PR #23243](https://github.com/NousResearch/hermes-agent/pull/23243)
    - **原因**: 该 PR 从 2026-05-10 开始开放，至今超过一个月未合并。它提供了一个完整的 16 语言国际化框架，是提升项目全球采用率的重要基础设施，应尽快评估与合并。

2.  **Google Gemini Grounding 与 OpenRouter 网络研究支持 (Issue #31621)**
    - **链接**: [NousResearch/hermes-agent Issue #31621](https://github.com/NousResearch/hermes-agent/issues/31621)
    - **原因**: 自 2026-05-24 开放，至今无官方回应。用户明确指出了使用 Google Grounding 和 OpenRouter 作为代理访问 Exa 的明确优势和高质量结果。这是一个能显著提升 Agent 信息获取能力的功能请求。

3.  **Profile-aware Cron Jobs (Issue #48649)**
    - **链接**: [NousResearch/hermes-agent Issue #48649](https://github.com/NousResearch/hermes-agent/issues/48649)
    - **原因**: 尽管是昨日提出的，但这是一个设计基础问题：Cron 任务在多 Profile 环境下行为不正确。随着 Profile 功能的使用增多，这个 Bug 的影响会越来越大，应尽早从架构上规划修复。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-06-19

---

## 1. 今日速览

过去24小时内，PicoClaw 项目保持了中等偏高的开发活跃度：共产生14条 PR 更新（其中7条已合并/关闭），以及2条 Issue 更新。最为引人注目的是 **1 个夜间构建版本发布**（v0.3.0-nightly.20260619），同时社区贡献者提交了 **web_fetch SSRF 防护绕过修复** 和 **web_search 诊断日志增强** 两项关键安全与稳定性补丁。依赖机器人 Dependabot 提交了大量 Go /前端依赖升级 PR，说明项目在持续追踪生态更新；但部分依赖 PR 已标记为 stale，需维护者优先审阅。整体而言，项目处于正常的开发迭代节奏中，安全性修复与依赖升级并进。

**活跃度评估**：7/10（开发活动密集，但社区参与主要来自自动化机器人，人为贡献较少）

---

## 2. 版本发布

### 🚀 nightly: Nightly Build (v0.3.0-nightly.20260619.287853ab)

- **发布类型**：预发布 / 自动化构建
- **说明**：这是基于 `main` 分支的最新自动化构建版本，标记为 `nightly`，可能包含未经充分测试的代码。
- **变更范围**：Full Changelog 覆盖从 v0.3.0 标签以来的所有变更（`compare/v0.3.0...main`）。
- **⚠️ 使用建议**：不适合生产环境部署，建议开发者在测试环境验证新功能及Bug修复效果后再决定是否跟进。
- **下载地址**：[Nightly Build 页面](https://github.com/sipeed/picoclaw/releases/tag/nightly)

---

## 3. 项目进展

今日合并/关闭的重要 PR 主要集中在 **安全修复**、**依赖升级** 和 **诊断能力增强** 三个方面，具体如下：

| PR | 类型 | 状态 | 关键内容 |
|----|------|------|----------|
| [#3143 fix(web): block private IPv4 embeds in ISATAP literals](https://github.com/sipeed/picoclaw/pull/3143) | 安全修复 | **待合并** | 修复 `web_fetch` 工具的 SSRF 防护绕过漏洞（Issue #3074），通过增强 IP 分类器识别嵌入私有 IPv4 地址的 ISATAP IPv6 字面量。这是社区贡献者 lc6464 提交的重要安全补丁。 |
| [#3141 fix(web_search): add diagnostic logging for Brave empty results](https://github.com/sipeed/picoclaw/pull/3141) | 功能增强 / 诊断 | ✅ 已合并 | 为 Brave Search API 返回空结果时添加诊断日志，解决静默失败（silent failure）问题，便于排查响应格式变化或非标准错误。由社区贡献者 jincheng-xydt 提交。 |
| [#3144 build(deps): bump actions/checkout from 6 to 7](https://github.com/sipeed/picoclaw/pull/3144) | CI 依赖升级 | ✅ 已合并 | CI 流程中的 GitHub Action 核心依赖升级。 |
| [#3146 build(deps): bump golang.org/x/term](https://github.com/sipeed/picoclaw/pull/3146) | Go 依赖升级 | ✅ 已合并 | （含 rebase） |
| [#3147 build(deps): bump Azure SDK azidentity](https://github.com/sipeed/picoclaw/pull/3147) | Go 依赖升级 | ✅ 已合并 | Azure 身份认证SDK升级。 |
| [#3148 build(deps): bump golang.org/x/sys](https://github.com/sipeed/picoclaw/pull/3148) | Go 依赖升级 | ✅ 已合并 | 引入 GPIO 常量等新功能。 |
| [#3149 build(deps): bump anthropic-sdk-go](https://github.com/sipeed/picoclaw/pull/3149) | Go 依赖升级 | ✅ 已合并 | Anthropic API SDK 升级至 1.50.2，跨越多个次要版本。 |
| [#3107 build(deps): bump copilot-sdk/go (v0.2.0→v1.0.1)](https://github.com/sipeed/picoclaw/pull/3107) | Go 依赖升级 | ✅ 已合并 | GitHub Copilot SDK 从 v0.2.0 直接升级至 v1.0.1，属于重大版本跳跃。 |

**项目整体进展**：今天项目在 **安全性**（解决 SSRF 绕过）和 **可观测性**（web_search 诊断日志）方面取得了实质推进。依赖层的持续更新表明项目保持了对上游生态的跟进。

---

## 4. 社区热点

### 🔥 最活跃讨论：Issue #3094 — 重复消息 Bug

- **链接**：[#3094 [Bug] 异步子代理(spawn)任务完成时，ForUser字段被同时用于直接推送和主代理汇总，导致重复消息](https://github.com/sipeed/picoclaw/issues/3094)
- **作者**：v2up-32mb
- **状态**：OPEN（自2026-06-10创建，持续活跃）
- **评论数**：2（当前最高）
- **背景分析**：该 Issue 描述了一个在多通道（飞书、Telegram）使用 `spawn` 派发异步子代理任务时出现的**重复消息**问题：子代理完成时，`ForUser` 字段被同时用于两条消息（子代理原始结果直接推送 + 主代理汇总后的排版输出）。用户对此有明显困扰，社区已有一定关注度，但目前尚未有 PR 关联修复。

### 📌 社区诉求分析

用户对消息推送机制的一致性和可控性有强烈需求。特别是在异步多代理场景下，消息的去重与合并策略直接影响使用体验。该 Issue 若未能及时修复，可能会影响用户对 spawn 功能的整体满意度。

---

## 5. Bug 与稳定性

今日涉及的 Bug 及稳定性问题按严重程度排列如下：

| 严重程度 | 编号 | 标题 | 状态 | 是否有 Fix PR |
|----------|------|------|------|---------------|
| 🔴 **高** | [#3074 (间接)](https://github.com/sipeed/picoclaw/issues/3074) | web_fetch SSRF 防护绕过（ISATAP 字面量） | 已解决 | ✅ [#3143](https://github.com/sipeed/picoclaw/pull/3143)（待合并） |
| 🟡 **中** | [#3094](https://github.com/sipeed/picoclaw/issues/3094) | 异步子代理消息重复推送 | OPEN | ❌ 尚未有 PR |
| 🟡 **中** | [#3125](https://github.com/sipeed/picoclaw/issues/3125) | web_search 工具使用 Brave API 时静默失败（`.security.yml` 迁移后） | **已关闭** | ✅ 推测已修复（虽未直接关联PR，但同日有 web_search 日志增强 PR #3141 被合并，有助于诊断此类问题） |
| 🟢 **低** | [#3141 (情境相关)](https://github.com/sipeed/picoclaw/pull/3141) | Brave Search API 空结果静默失败（无日志） | ✅ 已合并 | 诊断日志已增强 |

**风险提示**：
- **#3094 重复消息问题** 自6月10日上报后，至今已有8天未得到处理或分配，可能影响使用了 spawn 异步子代理功能的用户群，建议维护者优先安排修复或至少给出评论说明。
- **#3143 SSRF 修复** 虽然已提交 PR，但尚未合并，建议尽快审核合并以消除安全风险。

---

## 6. 功能请求与路线图信号

今日数据中未发现直接以 "feature request" 或 "enhancement" 标签的新建 Issue。但从已有 PR 和 Issue 中可以推断出以下路线图信号：

### 📌 潜在纳入下一版本的改进方向

1. **GitHub Copilot SDK 重大升级（v0.2.0 → v1.0.x）**
   - 涉及两条 PR：已合并的 [#3107 (v1.0.1)](https://github.com/sipeed/picoclaw/pull/3107) 和仍待合并的 [#3145 (v1.0.2)](https://github.com/sipeed/picoclaw/pull/3145)
   - SDK 从 v0.x 跳到 v1.x，可能包含破坏性变更（Breaking Changes），但 PR 描述中未提及具体适配改动，建议维护者关注向下兼容性。

2. **前端工具链升级（Vite 8.0.13→8.0.16、shadcn 4.7.0→4.11.0、eslint 10.2.1→10.4.1）**
   - 多个 Web 前端依赖 PR 处于 OPEN 且已标记 stale，显示前端工程化升级正在持续推进。

3. **web_search 的可观测性增强**
   - [#3141](https://github.com/sipeed/picoclaw/pull/3141) 的合并标志着项目在改善 API 调用诊断能力，未来可能会扩展到更多外部工具调用场景。

---

## 7. 用户反馈摘要

基于今日活跃 Issues 的评论及描述，提炼真实用户痛点与使用场景：

| 用户 | 反馈要点 | 场景 / 痛点 | 满意度 |
|------|----------|-------------|--------|
| v2up-32mb | 使用 `spawn` 工具时，子代理结果在飞书/Telegram 上重复推送（原始粗糙版 + 主代理排版版） | 异步多代理场景下的消息一致性问题，影响阅读体验 | ❌ 不满意，呼吁修复 |
| Giordano10 | API 密钥迁移至 `.security.yml` 后，Brave Search 工具静默返回空结果，无错误提示 | 配置迁移导致的回归问题，缺乏错误信息排查困难 | ❌ 不满意（提交 Issue 后已关闭，推测已处理） |

**用户痛点共性**：**配置变更后的向后兼容性** 和 **异步任务的消息控制** 是当前用户反馈最集中的两个领域。

---

## 8. 待处理积压

以下列出长期未获回应、或可能被忽视的重要 Issue / PR，建议维护者关注：

### ⚠️ 长期未响应的 Bug Issue

| 编号 | 标题 | 创建时间 | 最后更新 | 搁置天数 | 建议行动 |
|------|------|----------|----------|----------|----------|
| [#3094](https://github.com/sipeed/picoclaw/issues/3094) | [Bug] 异步子代理消息重复推送 | 2026-06-10 | 2026-06-18 | 8天（持续活跃中） | 分配标签/里程碑，确认是否纳入下个 Patch 版本 |

### ⚠️ 标记为 stale 的依赖升级 PRs（有合并价值，但审阅滞后）

这些 PR 均为 Dependabot 自动提交，涉及前端构建工具链：

| PR | 内容 | 创建时间 | 天数 |
|----|------|----------|------|
| [#3105](https://github.com/sipeed/picoclaw/pull/3105) | eslint 10.2.1 → 10.4.1 | 2026-06-11 | 7天 |
| [#3104](https://github.com/sipeed/picoclaw/pull/3104) | shadcn 4.7.0 → 4.11.0 | 2026-06-11 | 7天 |
| [#3103](https://github.com/sipeed/picoclaw/pull/3103) | typescript-eslint 8.59.3 → 8.61.0 | 2026-06-11 | 7天 |
| [#3101](https://github.com/sipeed/picoclaw/pull/3101) | vite 8.0.13 → 8.0.16 | 2026-06-11 | 7天 |
| [#3100](https://github.com/sipeed/picoclaw/pull/3100) | @vitejs/plugin-react 6.0.1 → 6.0.2 | 2026-06-11 | 7天 |

**建议**：由于这些 PR 均涉及前端的开发依赖且版本跳跃较小，若 CI 检查通过，可批量合并或批量关闭后由维护者统一升级，减少积压。

### ⚠️ 待合并的重大依赖升级

| PR | 内容 | 说明 |
|----|------|------|
| [#3145](https://github.com/sipeed/picoclaw/pull/3145) | copilot-sdk/go v0.2.0 → v1.0.2 | 继 [#3107](https://github.com/sipeed/picoclaw/pull/3107) 合并后，再次升级到 1.0.2，需关注是否与 1.0.1 有差别。 |
| [#3143](https://github.com/sipeed/picoclaw/pull/3143) | ISATAP SSRF 绕过修复 | **安全敏感**，建议优先审阅合并。 |

---

**编制日期**：2026-06-19  
**数据来源**：PicoClaw GitHub 仓库 (github.com/sipeed/picoclaw)  公开数据  
**分析师备注**：本日报基于过去 24 小时的项目活动数据生成，旨在为维护者与社区提供透明、可追溯的项目健康度视图。建议维护者重点关注 **#3094 重复消息 Bug** 与 **#3143 SSRF 安全修复 PR**。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 | 2026-06-19

**数据源:** github.com/nanocoai/nanoclaw | **统计周期:** 过去 24 小时 (截至 2026-06-18 更新)

---

## 1. 今日速览

过去 24 小时内项目活跃度极高，共计处理 5 条 Issue 和 21 条 Pull Request。安全漏洞修复是本日的绝对主旋律：一个严重的权限绕过漏洞（#2807）被披露后，社区与维护者迅速响应，连续提交多项安全加固 PR。功能开发方面，Agent 间消息审批功能已成功合并入主分支（#2793），Apple Container 运行时（#2809）等重大特性也在 PR 流程中。目前仍有 **15 个 PR 处于待合并状态**，项目呈现出高产出的积极态势，但也因多个“竞争性替代修复”方案的存在，对审核效率和外部贡献者的留存构成挑战。

**项目健康度评估:** 🟢 **活跃** (核心特性推进中，安全问题响应迅速，但待合并队列积压需警惕)

---

## 2. 版本发布

*（今日无新版本发布）*

---

## 3. 项目进展 (今日合并/关闭的 PR 亮点)

项目在 Agent 治理、开发者体验和社区覆盖上取得了实质性进展，**共有 6 个 PR 被合并/关闭**：

- **[Feature] Agent 间消息审批机制落地** ([#2793](https://github.com/nanocoai/nanoclaw/pull/2793))：合入了面向 Agent 间通信的可选消息级审批关卡。在此机制下，管理者可以为特定 Agent 间方向配置需要审批的策略，未配置时则保持现有的自由流转模式，完全向后兼容。这意味着 NanoClaw 开始具备企业级的多 Agent 通信管控能力。
- **[Refactor] 生态兼容性桥接** ([#2810](https://github.com/nanocoai/nanoclaw/pull/2810))：通过符号链接将 `.claude/skills` 与 `AGENTS.md` 映射到 `.agents/` 目录。这使得 Codex 等遵循通用 Agent 协议的 Harness 能直接读取项目技能与配置，打通了不同 Agent 框架间的技能复用。
- **[Fix] 环境配置弹性化** ([#2811](https://github.com/nanocoai/nanoclaw/pull/2811))：允许通过环境变量选择底层 AI Agent Provider，剥离了硬编码限制，提升了自托管场景的部署灵活性。
- **[Refactor] 清理 v2 遗留代码** ([#2803](https://github.com/nanocoai/nanoclaw/pull/2803))：删除了 v2 架构中已无生产调用者的 `resolveGroupIpcPath` 方法（IPC 在 v2 中已被会话 DB 替代）。
- **[Docs] 国际化进程** ([#2806](https://github.com/nanocoai/nanoclaw/pull/2806))：新增韩语版本 README 并接入语言切换器，社区贡献持续多元化。

---

## 4. 社区热点 (最活跃 Issues/PRs 分析)

- **🔥 安全漏洞引发高度关注**：[Issue #2807](https://github.com/nanocoai/nanoclaw/issues/2807) 报告了一个严重的权限管理缺陷——非所有者成员可在所有者初始化的群组中创建持久子 Agent 而无需审批。虽然该 Issue 刚创建尚未形成大量讨论，但其严重性直接驱动了后续多项安全修复 PR 的快速提交，成为今日社区最核心的关注点。
- **📦 容器化诉求尘埃落定**：[Issue #957](https://github.com/nanocoai/nanoclaw/issues/957)（建议支持 Podman 替代 Docker）在经过 10 条评论和 7 个 👍 后被关闭。这代表了用户对运行时多元化（特别是 macOS/Linux 下无守护进程方案）的长期诉求，虽然 Issue 已关闭，但这一信号值得项目组在后续路线图中考量。
- **🔀 “竞争性修复”现象**：本日多组问题出现了来自不同贡献者的“替代性 PR”（如 socket 超时、Router JSON 解析、Discord 分片）。特别是 `sturdy4days` 的 PR（#2802、#2801、#2804）与 `mksocial19-code` 的替换版本（#2813、#2815、#2816、#2818、#2814、#2817）。这种模式在提升代码质量（增加回归测试）的同时，也可能延长外部贡献者的等待周期，增加协作摩擦。

---

## 5. Bug 与稳定性

今日集中暴露了多个影响系统可用性和稳定性的 Bug，按严重程度排列如下：

| 严重程度 | Issue / PR | 问题描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **Critical** | [#2807](https://github.com/nanocoai/nanoclaw/issues/2807) | 非群组所有者成员可创建持久子 Agent，属于 **权限架构逻辑缺陷**。 | 未关闭，已有 #2814 (CLI 验证)、#2817/#2818 (send_file 沙箱) 等修复 PR |
| **Critical** | [#2804](https://github.com/nanocoai/nanoclaw/pull/2804) | `ncl messaging-groups create` **完全失效**，抛出 `NOT NULL constraint failed`。CLI 核心功能处于不可用状态。 | PR #2804 待合并 |
| **High** | [#2784](https://github.com/nanocoai/nanoclaw/issues/2784) | `container-runner`源码生成检测**仅监视 `index.ts`**，遗漏 `ipc-mcp-stdio.ts` 变更，导致运行时使用过期的 IPC 代码。 | Open，无直接 fix PR |
| **Medium** | [#2801](https://github.com/nanocoai/nanoclaw/pull/2801) / [#2815](https://github.com/nanocoai/nanoclaw/pull/2815) | Router `safeParseContent` 解析原始类型 JSON 时返回非对象，导致下游读取 `undefined` 引发崩溃。 | 待合并（竞争方案） |
| **Medium** | [#2802](https://github.com/nanocoai/nanoclaw/pull/2802) / [#2813](https://github.com/nanocoai/nanoclaw/pull/2813) | CLI Socket 客户端 `sendFrame` 无请求超时和响应缓冲区上限，存在连接永远挂起或内存泄漏风险。 | 待合并（竞争方案） |
| **Low** | [#2792](https://github.com/nanocoai/nanoclaw/pull/2792) | `add-imessage` 技能在新检出环境中因 `src/channels/` 目录不存在导致安装失败。 | PR #2792 待合并 |
| **Low** | [#2812](https://github.com/nanocoai/nanoclaw/pull/2812) / [#2816](https://github.com/nanocoai/nanoclaw/pull/2816) | Discord 适配器未设置 `maxTextLength`，长回复被截断而非按 2000 字分片发送。 | 待合并（竞争方案） |

---

## 6. 功能请求与路线图信号

- **已落地的路线图方向**：Agent 间消息审批（#2793）的合入，强烈暗示项目正朝向 **精细化 Agent 治理与安全策略** 演进，这是企业级部署的关键一环。
- **信号强劲的在途功能**：
    - [PR #2809](https://github.com/nanocoai/nanoclaw/pull/2809) 提出了 **Apple Container 原生运行时**（macOS）以及 **远程 OneCLI 网关**。这是平台层面的大跃进，如果合入，NanoClaw 将具备跨平台容器管理能力。
    - [PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795) 社区贡献了 **只读 CLI 仪表盘**技能，迎合轻量运维监控需求。
- **社区高频诉求**：
    - **v2 迁移指南**：多个 Issue（如 #2632）用户正在被迫自行考古代码进行迁移，官方急需给出 Telegram Swarm / Multi-Bot Identity 的明确替代方案。
    - **Podman 支持**（#957）：虽已关闭，但该诉求代表了非 Docker 容器用户群体的声音。

---

## 7. 用户反馈摘要

从今日更新的事件中，我们可以提炼出用户主要的情感倾向：

- **正面评价**：Issue [#957](https://github.com/nanocoai/nanoclaw/issues/957) 的作者明确评价该项目“非常有用且设计精良（It is very useful and well designed）”，这反映了项目核心架构在资深用户群体中的良好口碑。
- **核心痛点**：
    - **生产环境实战阵痛**：来自 `caburi00` 的 PR [#2808](https://github.com/nanocoai/nanoclaw/pull/2808) 日志写道“在运行生产环境时发现（found while operating a live install）”。这说明忠实用户正在尝试深度使用，但频繁遭遇核心逻辑 Bug（如 SQL 非幂等、字段丢失），项目在当前阶段的稳定性有待加强。
    - **迁移困扰**：#2632 的用户对于 v1 到 v2 的特性迁移路径感到**困惑且焦虑**，只能通过翻阅 git history 来尝试理解现状，这是一种典型的信号：官方迁移文档的缺位正在消耗社区信任。
    - **CLI 体验挫败**：`ncl messaging-groups create` 直接崩溃，对于任何尝试通过 CLI 管理群组的用户（无论是新手还是运维）都是重大负面体验。

---

## 8. 待处理积压

以下事项需要维护者团队优先关注，以避免社区信任损耗和技术债务累积：

- **⚠️ 严重安全修复积压**：漏洞 [#2807](https://github.com/nanocoai/nanoclaw/issues/2807) 对应的修复 PR（#2814、#2817、#2818）应作为当前最高优先级的合并对象，防止该权限缺陷在更多生产环境被触发。
- **⏳ v2 迁移路线图等待明确**：Issue [#2632](https://github.com/nanocoai/nanoclaw/issues/2632) 自 5 月 28 日起已悬置 3 周。维护者必须给出关于 Telegram Swarm / Multi-Bot Identity 在 v2 中的定位声明，否则将直接影响用户群体的升级决策。
- **🕸️ 竞争性 PR 决策压力**：目前有大量针对同一问题的替代性 PR 未被清理（如 #2801/2815、#2802/2813、#2812/2816）。维护者急需对这些方案做出最终决策（合并或关闭），以清理待合并队列中的 15 个 Open PR，减少贡献者的不确定性。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 | 2026-06-19

---

## 1. 今日速览

- 项目整体活跃度中等偏上，过去 24 小时共产生 **4 条 Issue 更新** 与 **4 条 PR 提交**，无代码合并及版本发布。
- 核心开发集中在 **流式请求下的 Tool Calling 缺陷修复**（`#964`、`#965`），这是直接影响用户体验的关键补丁。
- 社区贡献侧重 **文档完善**，微信个人号登录（`#963`）与原生 Anthropic 供应商（`#962`）的配置说明已进入评审队列。
- **评审积压风险凸显**：今日提交的 4 个 PR 均无维护者响应，长期 Issue（`#50`、`#190`）仍未获官方回复。
- 用户反馈集中在 **边缘端部署**（ESP32）**、多智能体编排**（Subagent）以及 **A2A 协议性能** 三大方向。

---

## 2. 版本发布

过去 24 小时无新版本发布。

---

## 3. 项目进展

**今日无已合并或关闭的 PR。** 但有 **4 个重要 PR 进入待审队列**，代表项目在核心修复与文档建设上的重要推进：

### 核心引擎修复
- **`#964`**[Enable native API-level tool calls during streaming](https://github.com/nullclaw/nullclaw/pull/964)：修复 `agent/root.zig` 在开启 Streaming 时错误地禁用原生 Tool Calls 的 Bug。这是流式场景下的核心质量修正。
- **`#965`**[Structured streaming tool-call support for SSE parser](https://github.com/nullclaw/nullclaw/pull/965)：作为 `#964` 的配套 PR，解决 SSE 解析器在处理流式工具调用时的结构化解析问题，确保端到端可用性。

### 文档生态完善
- **`#962`**[docs(providers): document native Anthropic provider](https://github.com/nullclaw/nullclaw/pull/962)：新增原生 Anthropic 供应商的详细配置文档（API Key 与 OAuth 模式），降低用户使用 Anthropic 模型的门槛。
- **`#963`**[docs(channels): document weixin personal WeChat QR code login channel](https://github.com/nullclaw/nullclaw/pull/963)：新增微信个人号二维码登录渠道文档，直接响应社区 Issue `#817` 诉求。

> **小结：** 项目处于"高产提交、等待整合"阶段。若上述 PR 落地，Streaming + Tool Calling 的体验和文档完善度将获得显著提升。

---

## 4. 社区热点

### 讨论最活跃的 Issues

- **`#817`**[Does nullclaw support WeChat QR code login?](https://github.com/nullclaw/nullclaw/issues/817)
  - 用户持续追问微信登录支持，今日获得 PR `#963` 的直接响应。体现了社区的强需求与项目组的敏捷回应能力。

- **`#50`**[Can this run on an Esp32?](https://github.com/nullclaw/nullclaw/issues/50)
  - 创建于 2 月 21 日，6 月 18 日仍有更新（累计 4 条评论）。反映出物联网/边缘端部署的持续关注度。

### 技术讨论焦点

- **`#913`**[a2a performance?](https://github.com/nullclaw/nullclaw/issues/913)
  - 用户 jacktang 直接给出对比结论：*"raw nullclaw messaging/response is faster than the a2a"*。这是一个极具建设性的性能反馈，暗示 A2A 协议可能存在额外开销，值得技术团队跟进优化。

---

## 5. Bug 与稳定性

### 严重缺陷（已有 Fix PR，待合并）

| Issue | 描述 | 严重程度 | 关联 PR |
|---|---|---|---|
| `#964` | 流式传输（Streaming）开启时，`agent/root.zig` 错误地传递 `.tools = null`，导致原生 API 级 Tool Calls 被禁用 | **严重**：影响所有流式 + 工具调用场景的用户体验 | `#964` (自述修复) |
| `#965` | SSE 解析器不支持流式结构化的 Tool Call，服务器在 `delta.content` 留下的 XML 无法被正确解析 | **高**：是 `#964` 的配套问题 | `#965` (自述修复) |

### 性能隐忧

- `#913` 用户报告的 **A2A 协议性能显著低于 Raw Messaging** 问题，虽非 Bug，但涉及协议设计或实现效率，建议官方进行基准测试并确认是否存在回归。

---

## 6. 功能请求与路线图信号

| 功能需求 | 来源 | 状态 | 路线图洞察 |
|---|---|---|---|
| **微信扫码登录** | `#817` | 已有文档 PR `#963`，待合并 | 若合并，将极大增强中国用户与微信生态的集成能力 |
| **边缘端部署 (ESP32)** | `#50` | 长期开放，无回复 | 暗示对极轻量级 Runtime 和硬件适配的需求 |
| **多智能体编排 (Subagent Spawning)** | `#190` | 用户询问跨 Provider 的 Subagent 间通信 | 指向未来 Agent 间协作、复杂工作流的架构能力 |
| **A2A 协议性能优化** | `#913` | 处于反馈阶段 | 社区正在推动 A2A 协议从"可用"走向"高效" |

---

## 7. 用户反馈摘要

- **`#913` – jacktang**：*"I find the raw nullclaw messaging/response is faster than the a2a."* 这是目前最直接、最具操作性的性能反馈，提示项目组需要审视 A2A 的协议设计或序列化开销。

- **`#190` – superhero75**：深入询问 Subagent 编排能力，暗示该用户可能正在尝试构建复杂的多智能体系统，对项目底层架构有较高期待。

- **`#50` – ngantrandev**：尝试在 ESP32 上部署，代表**极低资源、离线或边缘计算**的使用场景，目前尚无官方答复。

- **`#817` – DDGRCF**：明确需要微信生态集成，反映出项目在中国市场的潜在用户群体需求。

---

## 8. 待处理积压

### 长期未获官方回复的 Issue

| Issue | 创建时间 | 主题 | 积压天数 |
|---|---|---|---|
| `#50` | 2026-02-21 | ESP32 支持 | ~118 天 |
| `#190` | 2026-03-01 | Subagent 编排 | ~110 天 |

### 待评审 PR（均创建于 2026-06-18，无维护者评论）

| PR | 主题 | 类型 | 重要性 |
|---|---|---|---|
| `#964` | 流式 Tool Call 修复 | 核心 Bug 修复 | **紧急** |
| `#965` | SSE 解析器结构化支持 | 核心 Bug 修复 | **紧急** |
| `#963` | 微信登录文档 | 文档 | 高 |
| `#962` | Anthropic 供应商文档 | 文档 | 中 |

> **风险提示：** 今天的 4 个 PR 贡献质量较高，但目前均处于"零评论"的未评审状态。特别是 `#964` 直接影响到流式 + Tool Calling 这一核心功能组合的稳定性，建议维护团队尽快安排 Code Review 以加速项目迭代，避免贡献者因等待过久而流失。

---

*报告生成时间：2026-06-19 | 数据来源：GitHub (github.com/nullclaw/nullclaw)*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据你提供的 IronClaw 项目 2026-06-19 日期的 GitHub 数据生成的每日动态分析报告。

---

# IronClaw 项目日报 | 2026-06-19

**日报周期：** 2026-06-18 至 2026-06-19
**数据概览：** 过去 24 小时更新 **31** 条议题 / **43** 条拉取请求，无新版本发布。项目活跃度极高。

---

## 1. 今日速览

IronClaw 项目在过去 24 小时内保持了极高的工作节奏，**43 条拉取请求的更新量**表明开发团队正在全力冲刺 "Reborn" 引擎的稳定性与功能完善。核心工作围绕 **“工程化”与“可用性”** 两大主题展开：一方面推进了 **Slack 集成重构**、**并发执行调度**等底层架构优化，另一方面集中修复了 **OAuth 流程异常**、**自动化触发状态混乱**及 **WebUI 多出体验缺陷**。尽管本周无正式版本发布，但 **17 个拉取请求被合并/关闭**，标志着项目正快速向更稳定的状态迈进。社区测试者（如 `sunglow666`）提交了大量高质量的 Bug 报告，对 Agent 的弹性恢复能力提出了更高要求。

---

## 2. 版本发布
*（无）*

---

## 3. 项目进展

过去 24 小时内，以下重要功能已完成合并或进入最终评审阶段：

- **Projects 功能即将落地**：后端接口（PR #5018）已合并，前端界面（PR #5019）正在审查中。这是 IronClaw 在用户工作区组织能力上的一大步。
- **“一次性”定时触发器上线**：PR #5065 已合并，允许用户创建只执行一次的单触式自动化任务，大幅提升了定时任务场景的灵活性。
- **自动化页面体验升级**：PR #5055（合并）将自动化运行错误从红色“报错”软化为黄色“需关注”，PR #5084（开放中）则对整个自动化页面进行了密度更高的 UI 重设计。
- **核心架构解耦**：PR #5072（开放中）尝试将 Slack 集成重构为通用的宿主入口模式，为后续接入更多第三方应用铺平了架构道路。
- **性能优化前瞻**：PR #5085 引入了 **TurnRunScheduler**，旨在突破当前 LLM 推理的串行瓶颈，实现并发的回合执行，这将显著提升复杂任务的响应速度。

---

## 4. 社区热点

1.  **Agent 弹性恢复能力（Issue #4761）**
    - **关键标签：** `5 条评论`, `Reborn`, `Recovering`
    - **诉求分析：** 社区对 Agent 的自治能力有极高期望。用户反映当工具连续失败时，Agent 直接死掉而非重试或降级。这反映了 AI Agent 从“演示”走向“生产力”过程中最核心的用户痛点——**缺乏应对不确定性任务的韧性**。
    - 相关讨论：`nearai/ironclaw Issue #4761`

2.  **LLM 提供商兼容性（Issue #1520, #1012）**
    - **关键标签：** `长期未关闭`, `Alibaba`, `Qwen`, `Coding Plan`
    - **诉求分析：** 尽管是项目早期的议题（3月至今），但持续的讨论表明非 OpenAI 生态的开发者群体对“开放兼容”的强烈需求。特别是阿里云通义千问(Qwen)的 Coding Plan 在 OpenAI 兼容模式下无法使用，暴露了在兼容层上的边界问题，这一问题至今未被彻底解决。
    - 相关讨论：`nearai/ironclaw Issue #1520`, `nearai/ironclaw Issue #1012`

3.  **OAuth 认证流程的脆弱性（Issue #4907, #5070）**
    - **关键标签：** `Google OAuth`, `Flaky`, `User Experience`
    - **诉求分析：** OAuth 流程是 Agent 调用外部 API 的关键入口。用户连续报告了“认证成功但运行失败”（#4907）和“取消认证提示后陷入死循环”（#5070）的问题。这说明 OAuth 集成仍是 Reborn 引擎中最薄弱的环节之一，严重影响了 G-Suite 扩展等应用的实际体验。

---

## 5. Bug 与稳定性

**高风险项：**
- **Google OAuth 令牌过期风险（Issue #5071）：** `risk: high`。用户反馈 Google 令牌仅存活约1小时，但系统缺乏主动刷新机制。若未在短时内处理，将导致所有依赖 G-Suite 的自动化工作流瘫痪。*状态：待处理。*
- **SSO 访问不匹配导致自动化静默失败（Issue #4992）：** `risk: medium`。在多租户 Railway 环境下，本地开发的 SSO 与会话不匹配，导致计划任务在创建前就静默失败，调试极其困难。*状态：待处理。*
- **认证门控重复弹出（Issue #5070）：** 已通过 PR #5067 修复，防止 OAuth 提示在用户取消后无限重放。*状态：已关闭。*

**中/低风险项：**
- **审批弹窗内容过长（Issue #5078）：** 当前改进显示了详细命令，但对于超长 Shell 命令，弹窗被撑爆，难以操作。*状态：PR #5082 已提交修复。*
- **LLM 重试逻辑导致长时间卡死（PR #5043, #5045）：** 当配置错误（如模型名 `auto`）被 API 拒绝时，系统无限重试，导致用户长时间等待。*状态：修复中，PR 已开放。*
- **导航与 UI 状态错误（Issue #5076, #5077）：** 侧边栏高亮异常、无效 URL 直接报错而非重定向。暴露出 Reborn WebUI 在路由和状态管理上的不足。*状态：待处理。*

---

## 6. 功能请求与路线图信号

以下信号表明项目未来的短期重点方向：

- **审批流自动化（PR #5063）：** 引入“自动批准”工具列表，甚至支持基于回合的“本次运行全部允许”，旨在减少重复的交互审批。这是提升 Agent 自动驾驶级别的关键一步。
- **WeCom（企业微信）深度优化：** 从 Issue #4193（缺少引导）、#4500（写入错误会话）到 #4505（标题难以辨认），企业微信渠道集中涌现出一系列用户体验问题。这表明 **IronClaw 团队正在全力拉平多平台聊天机器人的体验差距**，而非仅限于 Slack/Telegram。
- **计费与可观测性（PR #4989）：** 将 Engine V2 的 LLM 使用量纳入 CostGuard 监控和 `llm_calls` 记录。这是一个清晰的信号：**项目正在考虑内测用户的成本管控和用量审计**，为正式商业化或大规模对外部署做准备。

---

## 7. 用户反馈摘要

- **感到满意/有改进的方面：** 用户提到审批弹窗现在能显示真实命令 (`#5078`)，这是一个明确的正面反馈。说明用户认可项目在透明化执行过程上的努力。
- **核心痛点：** “跑一半就卡死/失败了，还没有任何提示”是最大的吐槽点。用户在 `#4761`, `#4704`, `#5060` 等议题中反复描述这种糟糕的体验：工具调用通过了审批，但运行后静默失败或进入无提示的循环。
- **专业测试反馈：** 以 `sunglow666` 和 `think-in-universe` 为代表的用户，并非简单的抱怨，而是提交了非常结构化的复现步骤和测试结果。这种“先行尝鲜、积极参与”的社区文化是项目健康度的体现。

---

## 8. 待处理积压

- **长期未响应的重要 Issue：**
    - **#1012（阿里云 Qwen 兼容模式）：** 已开放超过 3 个月（2026-03-12），且仍有社区用户点赞寻求解决。此问题若不解决，可能持续扩大对阿里云生态用户的负面影响。
    - **#1520（Qwen 错误）：** 同样指向阿里云 Qwen 集成问题，与 #1012 类似，是社区呼声最高的技术债之一。
    - **WeCom 系列问题（#4193, #4500, #4502, #4505, #4612）：** 企业微信模块存在大量未关闭的子 Bug，建议维护者考虑设立一个总领的“WeCom 体验优化” Milestone，统一跟进。

- **关键开放拉取请求：**
    - **PR #5030（生产环境触发器轮询器）：** 若计划任务在生产环境正常工作，此 PR 必须尽快合并。
    - **PR #4992（SSO 访问不匹配）：** 该问题直接阻塞了多租户环境下的自动化部署，风险等级高。
    - **新贡献者拉取请求：** `abbyshekit`（PR #5045, #5043）和 `achalvs`（PR #5084）的拉取请求已开放超过24小时。及时 Review 并合入门槛较低的修复（如 LLM 故障快速失败）将极大激励社区贡献。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026‑06‑19

## 1. 今日速览

过去 24 小时，LobsterAI 完成了一次重要版本发布（2026.6.18），合并/关闭了大量 PR（14 个），展现出极高的开发活跃度。核心方向集中在 **语音输入模块的实时化改造**、**Computer Use 功能 MVP 落地** 以及 **Artifact 文件分享类型的扩展**（支持 Office、PDF、Markdown、Mermaid）。社区方面，今日新开的 Issue #2180 提出了将项目从工具集升级为“AI Collaborator”平台的长远构想，可能影响后续路线图。项目整体健康度良好，但存在一个长期未处理的 UI 小缺陷（#1422）需要留意。

| 指标 | 数量 |
|------|------|
| Issues 更新 | 2（新开/活跃 2，关闭 0） |
| PR 更新 | 15（待合并 1，已合并/关闭 14） |
| 新版本发布 | 1（2026.6.18） |

---

## 2. 版本发布

### LobsterAI 2026.6.18

📦 **发布时间**：2026‑06‑18  
🗂️ **GitHub Release**：https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.18  

**主要更新内容**

| 类别 | 说明 |
|------|------|
| **Artifact 分享能力升级** | 新增对 Word（DOCX）、PPT（PPTX）、Excel（XLSX）、PDF、CSV、TSV、Markdown、Mermaid 等文件类型的分享支持；优化预览卡片和打包逻辑。（PR #2159, #2178） |
| **语音输入（ASR）重构** | 移除旧的短 ASR 上传流程，Cowork 语音输入仅保留实时 ASR 模式；删除设置页中的 `voiceInput.recognitionMode` 配置，简化用户体验。（PR #2160, #2163, #2177） |
| **Computer Use 集成上线** | 为 Windows x64 引入内置的 Computer Use 工具包，包含运行时管理（v1.0.7）、MCP 服务器桥接（列出窗口/应用、截图、键盘鼠标控制）以及技能包完整性校验。（PR #2143, #2156） |
| **辅助改进** | 修复 macOS 麦克风权限申请（#2113）；重构语音输入模块（#2111）；修复专家套件页面样式（#2150）。 |

**⚠️ 破坏性变更与迁移说明**
- **语音输入模式配置移除**：`voiceInput.recognitionMode` 配置项不再生效，所有语音输入将自动使用实时 ASR。若用户之前在设置中切换过“一次性录制”模式，升级后无需任何操作，但自定义流程可能需要适配新的 IPC 接口（`asr:start-realtime` / `asr:stop-realtime`），旧 `asr:recognize` 已被删除。
- **Computer Use 运行时**：首次使用时会自动下载 v1.0.7 运行时，请确保网络可访问指定 CDN。已安装旧版本的用户将被自动更新。
- **依赖升级**：Electron 从 40.2.1 升到 42.4.0（伴随 #1277 待合），建议各平台全面回归测试窗口管理、权限与系统集成。

---

## 3. 项目进展

过去 24 小时共合并/关闭 14 个 PR，集中在以下三个方面：

### 🎤 语音输入实时化
- **PR #2160** `fix(voice-input): keep only realtime asr` — 彻底移除短 ASR 上传流程，所有语音输入强制走实时 ASR，简化维护路径。
- **PR #2163** `feat(voice-input): refine dictation recording UI` — 优化录音可视化、处理 ASR 配额，提升实时听写体验。
- **PR #2177** `fix(cowork): rename dictation copy to voice input` — 统一前端文案，“听写”改为“语音输入”，减少用户困惑。
- **PR #2155** `fix(voice-input): prevent duplicate realtime ASR starts` — 修复快速点击录音可能重复启动 ASR 会话的竞态问题。

### 🖥️ Computer Use MVP
- **PR #2143** `feat: add computer use MVP` — 完整引入技能包、运行时安装器、MCP 服务器桥接，使 LobsterAI 能直接操控 Windows 应用/窗口，具备基础自动化能力。
- **PR #2156** `fix(computer-use): bump runtime to 1.0.7` — 将运行时升级至 v1.0.7，修复辅助程序意外退出问题，增加 UIA 诊断日志。

### 📄 Artifact 分享扩展
- **PR #2178** `feat(artifacts): 支持 Markdown 和 Mermaid 文件分享` — 打通 Markdown 与 Mermaid 文件的分享入口，支持本地图片打包、ZIP 生成与预览。
- **PR #2179** `chore(release): merge release/2026.6.11 into main` — 将上述功能连同 office 文件分享等一起合入主分支，形成 2026.6.18 版本。

**影响**：项目正从“AI 对话工具”向“具备主动执行能力和文件协作能力的智能体平台”演进。语音交互更加流畅，计算机操控能力初具雏形，文件分享覆盖常见办公格式。

---

## 4. 社区热点

### 🆕 新功能提案：#2180 「Build "AI Collaborator" Form」
- **链接**：https://github.com/netease-youdao/LobsterAI/issues/2180
- **作者**：@woxinsj · **创建于** 2026‑06‑19
- **摘要**：提案附带详细设计文档（openclaw-ai-collaborator-proposal.pdf），建议将 OpenClaw 从低层级工具集升级为 **AI Collaborator 平台**，瞄准“懂技术的非精英程序员”。核心包括：
  - 自然语言命令栏（Natural Language Command Bar）
  - 跨模型任务调度控制台（Task Dispatch Console）
  - 项目级持久记忆（Project-Level Memory）
- **分析**：该提案反映了社区对更高层抽象、便捷多模型编排以及长程记忆的需求。若采纳，可能引导下一阶段走向“个人 AI 代理”方向。虽然暂无评论，但预计会引发维护团队与核心用户的深度讨论。

### 📌 长期搁置 Issue：#1422 UI 友好性问题
- **链接**：https://github.com/netease-youdao/LobsterAI/issues/1422
- **状态**：Open（stale）· 最后更新 2026‑06‑18
- **关注点**：MCP 自定义页面中，当服务名称较长时，删除弹框显示不友好（包含截图）。社区意见较少，但作为积压问题值得注意。

**综合热度判断**：今日无爆炸性讨论，但 #2180 提案因其战略意义，将成为近期社区关注的焦点。

---

## 5. Bug 与稳定性

过去 24 小时主要围绕语音输入模块的稳健性修复，未出现严重崩溃或数据丢失类问题。

| 严重程度 | 问题描述 | 对应修复 PR |
|----------|----------|-------------|
| ⚠️ 中等 | 语音输入在快速点击时可能重复启动实时 ASR，导致状态混乱 | ✅ #2155 `fix(voice-input): prevent duplicate realtime ASR starts` |
| 🟢 低 | macOS 上语音输入需要显式请求麦克风权限，否则 ASR 静默失败 | ✅ #2113 `fix(voice): request mac microphone permission` |
| 🟢 低 | Computer Use 辅助进程可能意外退出，影响自动化任务 | ✅ #2156 `fix(computer-use): bump runtime to 1.0.7` |
| 🟢 低 | 专家套件（Kits）页面标题与搜索栏在滚动时不固定 | ✅ #2150 `fix(kits): keep expert suite controls sticky` |
| 🟡 低 | MCP 服务名称过长时删除弹框 UI 异常（#1422） | ❌ 尚未处理 |

**稳定性总评**：得益于语音模块的全面重构，连续录音、并发处理等边界情况得到控制；Computer Use 运行时版本提升后稳定性改善。整体回归风险可控。

---

## 6. 功能请求与路线图信号

### 🚀 高潜力纳入后续版本的功能
- **AI Collaborator 平台化**（#2180）—— 自然语言命令栏、跨模型调度、项目级记忆。与当前 OpenClaw 低层级工具互补，可能成为 v2026.7 的核心主题。
- **Computer Use 扩展**（已有 MVP #2143）—— 后续可增加窗口截图 OCR、Shell 执行、更多平台支持（macOS/Linux）。从 PR 描述看，团队已在积极开发。
- **Artifact 分享持续扩展**（#2159, #2178）—— 已覆盖常用办公格式，预计很快会支持流程图、代码片段等富文本类型。

### 📌 已就绪但等待合并的依赖更新
- **PR #1277** `chore(deps-dev): bump the electron group across 1 directory with 2 updates`  
  - 链接：https://github.com/netease-youdao/LobsterAI/pull/1277  
  - Electron 版本从 40.2.1 → 42.4.0，electron-builder 同步更新。由于涉及多个 API 变更，建议维护者在下一轮发布前完成合并。

**路线图信号**：项目正在快速吸收“AI 智能体”相关功能（语音→Computer Use→平台化），从被动问答向主动执行、长期记忆的转变趋势明显。

---

## 7. 用户反馈摘要

由于今日 Issues 社区互动较少，仅能基于现有内容做有限提炼：

- **UI 易用性**（来自 #1422 截图）：用户配置了较长服务名的 MCP 自定义页面后，删除弹框不能完整显示服务名称，与周围元素重叠。推测用户希望弹框能自动调整宽度或使用省略号/提示。
- **语音输入统一化**：PR #2160 移除了“一次性录音”模式，虽然官方以简化体验为目标，但少量依赖旧模式的用户可能需要适配期。不过社区未出现反对意见。
- **Artifact 分享增强**：#2159 的作者 @liugang519 是核心开发者，说明团队对用户文件协作需求的重视。从支持类型看（Office + PDF + Markdown + Mermaid），直击办公场景高频需求。

**总体满意点**：版本发布频率快（近一月周周有 Release），功能迭代贴近实际使用场景。潜在不满点：旧 Issue 响应周期较长（如 #1422 已徘徊 2 月）。

---

## 8. 待处理积压

### 🟡 长时间未响应的 Bug
- **#1422** `[stale] MCP-自定义页面，对应的服务名称较长时，删除弹框那展示不友好`  
  - 创建于 2026‑04‑03，最后维护者评论在 2026‑06‑18（可能是机器标签更新），仍未修复。建议维护者评估 UI 组件是否需要加入文本溢出处理或调整弹框宽度策略。
  - 链接：https://github.com/netease-youdao/LobsterAI/issues/1422

### 🟡 等待手动合并的依赖 PR
- **#1277** `chore(deps-dev): bump the electron group across 1 directory with 2 updates`  
  - Dependabot 自动生成，但 Electron 42.x 的 breaking changes（如 `contextBridge` 变化）可能需要主仓库协调。该 PR 从 4 月就已创建，合并冲突风险逐渐累积。
  - 链接：https://github.com/netease-youdao/LobsterAI/pull/1277

**建议**：优先处理 #1422（低风险但影响用户体验），并在一周内完成 #1277 的回归测试与合并，避免依赖版本差距过大影响后续开发。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的。这是根据您提供的Moltis项目数据生成的2026-06-19项目动态日报。

---

## Moltis 项目日报 2026-06-19

### 1. 今日速览
今日 Moltis 项目处于极低活跃度状态。过去 24 小时内，仅新增 1 个 Bug 报告，无任何 Pull Request 提交或合并，也无新版本发布。开发节奏明显放缓，社区互动几近于零。单一新增 Issue 涉及核心会话管理功能，但尚未引发讨论，项目健康度需关注后续开发者的响应速度与修复计划。

### 2. 版本发布
*(本日无新版本发布)*

### 3. 项目进展
- **代码与功能合并：** 今日无任何 Pull Request 被合并或关闭，项目代码库与功能层面未见实质性推进。

### 4. 社区热点
- **唯一热点：** [Issue #1132 [Bug] "main" session can't be deleted/archived](https://github.com/moltis-org/moltis/issues/1132)
    - **作者：** vvuk
    - **分析：** 这是今日项目唯一的社区动态。虽然尚无评论或点赞，但其直指核心功能“会话管理”中的权限限制问题。用户期望能自主管理“main”会话，凸显了用户对数据控制权和界面清洁度的需求。该 Issue 后续的讨论方向（是设计如此还是 Bug）将直接影响用户满意度。

### 5. Bug 与稳定性
- **[Bug] 无法删除/归档“main”会话** (中等严重程度)
    - **Issue 链接：** [#1132](https://github.com/moltis-org/moltis/issues/1132)
    - **描述：** 用户报告名为 "main" 的默认会话无法被删除或归档。这可能导致用户无法清理界面或重新组织会话列表，属于功能受限问题，但不涉及程序崩溃或数据丢失。
    - **修复状态：** 无关联的修复 PR。

### 6. 功能请求与路线图信号
- **关于“会话管理”的需求信号：** [Issue #1132](https://github.com/moltis-org/moltis/issues/1132) 虽被标记为 Bug，但其内容“能否删除/归档主会话”本质上是一个功能请求。它暗示用户希望获得对所有会话的完全管理权限，而不是被强制保留一个不可删除的“main”会话。目前没有证据表明此需求会被纳入下一个版本，但开发者应将其视为改善用户体验的方向之一。

### 7. 用户反馈摘要
- **用户痛点：** 用户 `vvuk` 在 [Issue #1132](https://github.com/moltis-org/moltis/issues/1132) 中清晰地报告了一个痛点：他试图删除或归档名为“main”的会话，但操作失败。这表明用户在日常清理和管理会话时遇到了直接障碍。
- **使用场景暗示：** 用户可能拥有多个会话，并希望通过删除或归档“main”等旧会话的方式来整理工作区，或重新开始一个新周期。
- **态度评估：** 用户虽然遇到了问题，但按照规范提交了详细的预检查清单（Preflight Checklist），表明他是一个有经验的、愿意为项目质量做出贡献的正面用户。当前社区无负面情绪爆发，但开发者需尽快回应以避免其失望。

### 8. 待处理积压
- **当前无积压：** 截至今日，Moltis 项目没有超过 24 小时未回应的开放 Issue 或 PR。唯一的待处理项是新提交的 [Issue #1132](https://github.com/moltis-org/moltis/issues/1132)，状态为“待开发者响应或确认”。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw (QwenPaw) 项目动态日报 — 2026-06-19

## 1. 今日速览

过去24小时内，项目活跃度维持高位：共处理44条Issue（新开/活跃15条，关闭29条），28条PR（待合并15条，合并/关闭13条），并紧急发布修正版本v1.1.12.post1。社区围绕上下文压缩导致进程冻结、文件下载失败、升级后技能重置等痛点展开集中反馈。开发侧在MCP服务池共享、Windows环境清理、钉钉SSL适配及原生上下文压缩迁移等方向取得扎实进展，代码质量和稳定性持续提升。

## 2. 版本发布

**v1.1.12.post1**  
- **修复：** 修正`prerelease`参数扩展错误并更新版本号（PR [#5288](https://github.com/agentscope-ai/QwenPaw/pull/5288)）  
- **修复：** 将ChromaDB探测集合重命名为`probe-test`，防止与用户数据冲突（PR [#5288](https://github.com/agentscope-ai/QwenPaw/pull/5288)）  
- **影响评估：** 仅含两项小修补，无破坏性变更或迁移注意事项。

## 3. 项目进展

以下为今日合并/关闭的重要PR，推动了关键基础设施与稳定性提升：

| PR | 要点 | 影响 |
|----|------|------|
| [#4849](https://github.com/agentscope-ai/QwenPaw/pull/4849) (closed, merged) | 引入**SharedMCPPool**，跨Agent复用MCP服务器进程，解决Windows平台300+Agent启动时的进程爆炸问题 | 大幅降低资源占用，提升大规模部署稳定性 |
| [#4860](https://github.com/agentscope-ai/QwenPaw/pull/4860) (closed, merged) | 启动时自动清理Windows `pip upgrade`残留的幽灵技能目录 | 消除升级后混乱，优化用户开箱体验 |
| [#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291) (closed, merged) | 为钉钉Channel HTTP客户端显式配置SSL证书，修复`uv tool install`环境下的通信失败 | 解决Windows + uv安装场景的通道不可用问题 |
| [#5303](https://github.com/agentscope-ai/QwenPaw/pull/5303) (closed, merged) | 修复Web对话窗口上下文占用显示始终使用固定值（131072）的问题，改为读取当前模型的`max_input_length` | 消除用户对上下文满的误判 |
| [#5309](https://github.com/agentscope-ai/QwenPaw/pull/5309) (closed, merged) | 将自定义上下文管理模块迁移至**AgentScope 2.0原生压缩框架**（Offloader协议+中间件修剪） | 统一压缩管道，为后续算法替换铺设架构基础 |
| [#5270](https://github.com/agentscope-ai/QwenPaw/pull/5270) (closed, merged) | Sprint 3集成测试套件，覆盖ACP/插件/安全/横切面合计64个用例 | 显著提升回归防护能力 |

项目整体在性能（MCP复用）、跨平台兼容（Windows/uv）、核心架构（上下文管理）及质量保障方面迈出坚实一步。

## 4. 社区热点

今日讨论最活跃的Issue（按评论数排序）：

1. **#5218 [Bug] 子Agent触发上下文压缩时进程冻结无响应**  
   - 评论16条，高关注度  
   - 用户报告子Agent触发上下文压缩后整个应用卡死，必须手动重启  
   - 链接：[#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)  
   - **核心诉求：** 上下文压缩功能存在严重死锁风险，直接影响多Agent工作流可靠性

2. **#5171 [Bug] 上下文压缩保留缺少按条数保留或排除人设文件，导致信息完全丢失**  
   - 评论8条  
   - 当人设文件token超限时，压缩会将整个上下文清空，任务中断  
   - 链接：[#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)  
   - **核心诉求：** 需要更智能的保留策略（按条数/排除指定文件），防止核心设定在压缩中丢失

3. **#5140 [Bug] v1.1.11.post2附件下载docx/pdf报404**  
   - 评论8条，已关闭  
   - 纯文本可下载，但Word/PDF附件点下报404  
   - 链接：[#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140)  
   - **用户心态：** 核心文件传输功能存在回归，影响日常使用信任度

4. **#5063 [Feature] 集成Headroom作为可选压缩层，减少60-95% token消耗**  
   - 评论7条  
   - 用户提议集成可逆压缩中间件大幅降低LLM调用成本  
   - 链接：[#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)  
   - **趋势信号：** 社区对token经济性高度敏感，期待官方容量优化方案

5. **#5262 [Bug] 每次升级后被禁用的内置技能自动重置为启用**  
   - 评论7条  
   - 已曾提过类似Issue，升级后用户禁用配置被覆盖  
   - 链接：[#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262)  
   - **核心诉求：** 升级应保留用户偏好设置，减少重复配置负担

## 5. Bug 与稳定性

按严重程度排列：

| 严重性 | Issue | 描述 | Fix PR 状态 |
|--------|-------|------|-------------|
| 🔴 崩溃 | [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) | 上下文压缩导致整个进程冻结，仅能手动重启 | 无PR关联 |
| 🔴 数据丢失 | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | 压缩后上下文完全清空，人设文件被丢弃，任务中断 | 无PR关联 |
| 🟠 功能异常 | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | docx/pdf附件下载404，纯文本正常 | 已关闭，可能已修复但未标记PR |
| 🟠 功能异常 | [#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264) | 飞书群聊消息被错误回复到私聊（用户同时有私聊会话时） | 无PR关联 |
| 🟠 权限错误 | [#4922](https://github.com/agentscope-ai/QwenPaw/issues/4922) | 微信渠道读取文件后PermissionError，后续所有请求均失败 | 无PR关联 |
| 🟡 配置重置 | [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | 升级后内置技能禁用状态被重置 | 无PR关联 |
| 🟡 显示错误 | [#5300](https://github.com/agentscope-ai/QwenPaw/issues/5300) | Web上下文占用显示错误分母（已通过PR #5303修复） | [PR #5303](https://github.com/agentscope-ai/QwenPaw/pull/5303) ✅ 已合并 |
| 🟡 频道监听 | [#5253](https://github.com/agentscope-ai/QwenPaw/issues/5253) | custom_channel保存后监听宕掉，需重新保存才能启动 | 无PR关联 |

PS：ChromeDB segfault ([#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854)) 虽为历史缺陷，但仍在6月18日有更新评论，表明该问题在部分环境中仍然存在，长期未彻底解决。

## 6. 功能请求与路线图信号

| 信号强度 | Issue / PR | 说明 | 潜在纳入版本 |
|----------|------------|------|-------------|
| ⭐ 高 | [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) + [PR #5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) (open) | 集成Headroom可逆压缩，已由社区开发者提交实现PR | 下一版可能性大 |
| ⭐ 高 | [#3940](https://github.com/agentscope-ai/QwenPaw/issues/3940) | 支持独立视觉模型路由，无需手动切换模型即可解析图片 | 社区呼声高，无PR |
| ⭐ 中 | [PR #5323](https://github.com/agentscope-ai/QwenPaw/pull/5323) (open) | 添加`todo_write`原生进度面板，多步骤任务可视化 | 已提PR，可能快速合并 |
| ⭐ 中 | [PR #5321](https://github.com/agentscope-ai/QwenPaw/pull/5321) (open) | Scroll上下文管理器：持久化历史+召回式REPL | 新方案，讨论中 |
| ⭐ 中 | [PR #5310](https://github.com/agentscope-ai/QwenPaw/pull/5310) (open) | 基于bubblewrap的Linux沙箱隔离 | 提升安全，长期方向 |
| ⭐ 中 | [PR #5304](https://github.com/agentscope-ai/QwenPaw/pull/5304) (open) | `qwenpaw terminal`编码模式终端 | 增强CLI体验 |
| ⭐ 低 | [#3768](https://github.com/agentscope-ai/QwenPaw/issues/3768) | 支持正则匹配自动拒绝命令（无需审批） | 4月提出，暂无PR |

## 7. 用户反馈摘要

- **上下文压缩稳定性**：多位用户反馈压缩功能引入严重卡死或数据丢失（#5218, #5171），工作流因此中断，当前体验“不如不压缩”。
- **升级体验**：每次升级后定制配置（如禁用技能、人设文件）被重置，导致用户抵触升级，反馈“又要手动禁一遍”（#5262）。建议社区增加版本迁移脚本或保持配置持久化。
- **渠道兼容性**：钉钉在uv安装环境下SSL失败（PR #5291已修复）；飞书群聊消息回错窗口导致混淆；QQ渠道文件传输缺失（#1983）。渠道生态成熟度有待提升。
- **自定义模型配置**：用户希望为每个自定义模型独立设置`timeout`和`context_window_size`（#3929），当前全局配置难以满足多样化模型。
- **附件下载回归**：#5140中用户明确抱怨“纯文本可以，docx/pdf不行”，指出v1.1.11.post2退化，影响知识库场景。

## 8. 待处理积压

以下为长期未关闭且仍影响用户的重要Issue/PR，建议维护团队优先关注：

| 类型 | 编号 | 创建时间 | 摘要 | 最后更新 | 备注 |
|------|------|----------|------|----------|------|
| Issue | [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | 2026-04-27 | ChromaDB Rust绑定段错误导致进程直接崩溃 | 2026-06-18 | 高严重性，长期未根除 |
| Issue | [#3940](https://github.com/agentscope-ai/QwenPaw/issues/3940) | 2026-04-29 | 独立视觉模型路由需求 | 2026-06-18 | 高社区呼声，无对应PR |
| Issue | [#2245](https://github.com/agentscope-ai/QwenPaw/issues/2245) | 2026-03-25 | 多Worker时自定义Channel端口冲突导致监听停止 | 2026-06-18 | 老旧Issue，影响生产部署 |
| Issue | [#3768](https://github.com/agentscope-ai/QwenPaw/issues/3768) | 2026-04-24 | 希望新增自动拒绝功能（命令审批改进） | 2026-06-18 | 已关闭但未实现，用户期待高 |
| PR | [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) | 2026-05-22 | DataPaw数据插件（12个BI技能） | 2026-06-18 | 长时间未Review，功能价值明确 |
| PR | [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) | 2026-06-02 | 解耦插件加载器初始化，修复Tauri/PyInstaller环境插件静默超时 | 2026-06-18 | 核心稳定性修复，滞留两周 |

---

*日报基于 CoPaw (QwenPaw) GitHub 仓库公开数据自动生成，数据采集时间 2026-06-19 00:00 UTC。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是 2026 年 6 月 19 日的 ZeroClaw 项目动态日报。

---

### ZeroClaw 项目动态日报 | 2026-06-19

> 本项目动态日报由 AI 助手根据公开的 GitHub 数据结合分析生成，力求客观、专业地呈现项目实时健康度。

---

### 1. 今日速览

ZeroClaw 在 6 月 19 日保持着极高的迭代节奏，**正式发布了 v0.8.1 稳定化补丁**，同时过去 24 小时内共有 **50 个 Issue 和 50 个 PR 被更新**，标志着项目已进入 v0.8.x 系列的密集修复与优化期。

- **健康度评估**：积极。尽管大量 S1（流程阻塞）级别 Bug 仍在对用户造成困扰，但核心团队与社区贡献者响应极快，当日即提交了多项针对性修复 PR（#7959, #7960, #7961）。
- **主要矛盾**：项目正处于从“功能堆砌”向“生产环境就绪”转型的阶段。用户对企业级能力（OIDC）和消费级体验（Telegram/Local Models）的诉求都非常紧迫。
- **贡献热度**：`Audacity88`, `mazhuima`, `Nillth` 等高产贡献者在安全、工具和渠道部分提交了大批高质量代码。

---

### 2. 版本发布

#### [ZeroClaw v0.8.1 正式发布](https://github.com/zeroclaw-labs/zeroclaw/releases)
这是 v0.8.x 系列的首个补丁版本，旨在稳定化在 v0.8.0 中引入的多智能体运行时（Multi-agent Runtime）、通道（Channels）及供应商（Providers）技术栈。

- **数据量级**：共 207 次提交，45 位贡献者参与。包含 **123 个 Bug 修复** 和 **46 个新功能特性**。
- **核心优化**：重点修复了运行时的稳定性问题，并对渠道与供应商的互操作性进行了全面修补。
- **破坏性变更与迁移**：Changelog 未明确标记破坏性变更，但鉴于 v0.8.1 高度聚焦于修复 v0.8.0 的遗留问题，建议所有 v0.8.0 用户升级。若你使用了自定义的 `memory`、`runtime` 或 `provider` 配置，请留意升级后行为变化。

---

### 3. 项目进展

过去 24 小时内，项目修复了多个长期痛点，并向关键功能路径迈出了实质步伐：

- **成本追踪里程碑**：[PR #7953](https://github.com/zeroclaw-labs/zeroclaw/pull/7953) 被合并并关闭，彻底解决了 [Issue #5221](https://github.com/zeroclaw-labs/zeroclaw/issues/5221) 中报告的“调度/CLI/Web Agent 模型成本未被捕获”的问题。
- **核心权限与恢复**：
  - [PR #7959](https://github.com/zeroclaw-labs/zeroclaw/pull/7959) 修复了非 `Full` 自治级别下自动批准工具无法使用的问题。
  - [PR #7960](https://github.com/zeroclaw-labs/zeroclaw/pull/7960) 为 `execute_pipeline` 添加了基于 Agent 粒度的安全策略，防止工具权限逃逸。
  - [PR #7961](https://github.com/zeroclaw-labs/zeroclaw/pull/7961) 修复了 Anthropic provider 因 JSON Schema 包含 `$ref` 等关键字导致 API 拒绝的问题。
- **新能力注入**：
  - [PR #7965](https://github.com/zeroclaw-labs/zeroclaw/pull/7965) 提交了 Discord 渠道的完整交互组件支持（按钮、下拉框、模态框）。
  - [PR #7945](https://github.com/zeroclaw-labs/zeroclaw/pull/7945) 为 xAI/Grok 添加了第一方 OAuth 登录支持。
- **稳定与兼容性**：[PR #7956](https://github.com/zeroclaw-labs/zeroclaw/pull/7956) 对 Windows 平台的测试 fixture 进行了可移植性修复。

---

### 4. 社区热点

| 话题 | Issue/PR | 讨论量 | 核心诉求分析 |
|---|---|---|---|
| **记忆系统权重博弈** | [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | 6 条 | 用户抱怨系统提示被记忆内容“淹没”。根本诉求是**对记忆行为的精细化控制**，希望当前指令拥有更高优先级，尤其是定时任务场景。 |
| **企业级认证** | [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | 5 条 | OIDC 支持是客户部署的门槛。社区讨论聚焦于插件化架构，这也是 v0.9.0 的核心目标，体现了项目向企业级应用演进的需求。 |
| **渠道性能与成本** | [#6067](https://github.com/zeroclaw-labs/zeroclaw/issues/6067) | 5 条 | 用户希望将“渠道回复意图预判”这类频繁操作迁移至**更小、更快的模型**，并加入硬超时和日志，避免阻塞主模型调用。 |
| **MCP 功能扩展** | [#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) | 2 条 (4 👍) | 高票需求。用户不满足于仅将 MCP 作为工具执行，要求**暴露 MCP 的资源和提示能力**给 Agent，以构建更复杂的语义上下文。 |

---

### 5. Bug 与稳定性

当日处理了大量严重 Bug，部分已火速修复，但仍有关键漏洞待解。

| 严重程度 | Issue | 标题摘要 | 状态 / 修复 PR |
|---|---|---|---|
| **S1** | [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) | Shell 工具在 `full` 权限下被拒绝 | **已修复** (PR [#7959](https://github.com/zeroclaw-labs/zeroclaw/pull/7959)) |
| **S1** | [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | 默认 32k 上下文字段被工具定义耗尽 | 无直接修复 PR，严重阻塞新用户上手 |
| **S1** | [#6841](https://github.com/zeroclaw-labs/zeroclaw/issues/6841) | `vision_provider` 配置被静默忽略 | **无修复 PR**，需维护者立即关注 |
| **S1** | [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) | MCP 工具在 OpenAI/Anthropic 推理函数中丢失 | **无修复 PR**，新报告，影响范围大 |
| **S1** | [#7964](https://github.com/zeroclaw-labs/zeroclaw/issues/7964) | `context_compression` 模型配置未跨供应商隔离 | **今日新 Bug**，无修复 PR |
| **S1** | [#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) | Cron 任务被重复启动 | 无修复 PR，调度器设计缺陷 |
| **S2** | [#5221](https://github.com/zeroclaw-labs/zeroclaw/issues/5221) | 调度/CLI 模型成本未被捕获 | **已关闭** (PR [#7953](https://github.com/zeroclaw-labs/zeroclaw/pull/7953)) |
| **安全/阻塞** | [#5869](https://github.com/zeroclaw-labs/zeroclaw/issues/5869) | `rumqttc` 依赖引入多个 RustSec 漏洞 | `blocked` (等待上游依赖更新) |

---

### 6. 功能请求与路线图信号

当日的活动清晰地勾勒出了未来两个版本的重点：

- **v0.9.0（认证与安全架构）**：追踪 Issue [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) 开始聚合队列，OIDC 支持 ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) 和路由层认证中间件 ([#6250](https://github.com/zeroclaw-labs/zeroclaw/issues/6250)) 是核心。
- **v0.8.3（Web 与 MCP 管理）**：追踪 Issue [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) 表明下一个迭代重点将是 MCP 仪表盘和插件管理界面。
- **新功能注入**：
  - **Signal 渠道增强**：支持媒体附件 ([#7891](https://github.com/zeroclaw-labs/zeroclaw/issues/7891)) 和 Markdown 原生渲染 ([#7890](https://github.com/zeroclaw-labs/zeroclaw/issues/7890))。
  - **供应商熔断器**：[#7881](https://github.com/zeroclaw-labs/zeroclaw/issues/7881) 提出了按供应商进行熔断的机制，提升可靠性。
  - **RunPod/ComfyUI 图像生成**：[#7875](https://github.com/zeroclaw-labs/zeroclaw/issues/7875) 将新增独立的图像生成供应商支持。

---

### 7. 用户反馈摘要

从当日的 Issue 评论中提炼出以下关键用户场景与痛点：

1.  **对本土化/消费级渠道的高要求**：
    - 用户 `sikc231` 描述了通过 Telegram 连接本地 `llama.cpp` 的理想工作流，但遇到了“地址被错误解析”的问题 ([#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002))。
    - 用户 `aq-uua` 反馈发送多张图片时，Telegram 会错误地串行发起多次 LLM 请求 ([#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514))。

2.  **灵活性与默认配置的矛盾**：
    - `JordanTheJet` 发现默认的 32K token 预算在首次迭代就被系统提示词和工具定义耗尽，导致“永无止境的预压缩”死循环 ([#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808))。
    - `touhidurrr` 指出 Cron 任务缺乏文档，且无法指定运行模型，无法实现“简单任务跑便宜模型”的预期 ([#7762](https://github.com/zeroclaw-labs/zeroclaw/issues/7762))。

3.  **开发者体验（CLI & 日志）**：
    - `mikeyhew` 再次吐槽 ZeroClaw 将日志输出至 `stdout` 而非 `stderr`，破坏了 CLI 管道命令的使用体验 ([#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721))。该 Issue 停留在 `help wanted` 状态已久。

---

### 8. 待处理积压

以下为长期存在或关键路径上的阻塞项，提醒维护者和社区关注：

| 类型 | 编号 | 标题 | 搁置原因 / 风险提示 |
|---|---|---|---|
| **依赖阻塞** | [#5869](https://github.com/zeroclaw-labs/zeroclaw/issues/5869) | MQTT 客户端 `rumqttc` 锁定旧版 `rustls-*` 导致安全漏洞 | **外部依赖**。需升级 `rumqttc` 版本或替换 MQTT 库，P1 优先级但被外部阻塞。 |
| **核心功能缺口** | [#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) | MCP 资源与 Prompt 支持 | **缺失的重要能力**。目前仅作为工具客户端，严重限制了 MCP 生态的接入价值。 |
| **平台兼容性** | [#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721) | 日志应输出到 `stderr` | **小改动，大收益**。标签为 `help wanted`，但长期未解决，影响严肃 CLI 用户。 |
| **严重 Bug 挂起** | [#6841](https://github.com/zeroclaw-labs/zeroclaw/issues/6841) | `vision_provider` 配置被静默忽略 | **S1 严重度**，至今无关联修复 PR。图片多模态流程完全断裂，用户可能完全不知情。 |

---
*本日报由 AI 智能体生成，旨在提供数据驱动的项目洞察。具体技术决策请以官方公告和代码审核为准。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*