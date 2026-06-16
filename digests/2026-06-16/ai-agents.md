# OpenClaw 生态日报 2026-06-16

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-16 03:44 UTC

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

好的，这是根据您提供的 OpenClaw GitHub 数据生成的 2026-06-16 项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-16

### 1. 今日速览

过去 24 小时，OpenClaw 项目保持了极高的社区活跃度，共发生 500 条 Issue 和 500 条 PR 更新，处于“高热”运行状态。其中新开/活跃 Issue 达 481 条，待合并 PR 413 条，反映出社区贡献热情高涨与新需求、Bug 报告的集中爆发。发布了一个新 Beta 版本，重点增强了信使通道的富文本投递能力。安全与会话稳定性是今日社区讨论的绝对焦点，大量 P1 级别的 Bug 和回归问题正在被紧急处理。尽管社区活跃度极高，但维护者的评审与决策积压（`needs-maintainer-review` / `needs-product-decision`）正在成为项目快速迭代的潜在瓶颈。

### 2. 版本发布

- **版本号**: `v2026.6.8-beta.2`
- **仓库链接**: openclaw/openclaw Releases
- **更新详情**:
    - **消息通道增强**: Telegram 和 WhatsApp 渠道的投递能力得到显著增强，现在可以发送结构化富文本（包含表格、列表、可展开的引用块），并保留了预设的换行，提升了阅读体验。
    - **CLI 后端投递**: 引入了 CLI 后端投递机制以更好地保留提示词结构。
    - **安全性与兼容性**: 退役了原生草稿迁移功能，并增强了富媒体的安全处理。
- **迁移注意事项**: 本次更新未提及明确的破坏性变更，用户可平稳升级，但需留意 Telegram/WhatsApp 渠道富文本行为的具体表现。

### 3. 项目进展

过去 24 小时，项目共合并/关闭了 **87 条** Pull Request，标志着多个功能模块取得了实质进展：

- **自动化与基础设施**:
    - **`#68936`** (Autofix pipeline + Windows daemon) 的合并是今日重大进展，该 PR 引入了 PR 审查自动修复管线，将显著加快代码质量和 CI/CD 流程。
- **核心修复与新功能合并/提交**:
    - `#93480` 修复了 Agent 在 `before_agent_finalize` Hook 请求修订时导致的首轮回答数据丢失问题。
    - `#93438` 引入了 Telegram 原生草稿支持，提升实时预览体验。
    - `#93446` 新增了 Codex 托管 Web 搜索集成，扩展了 Agent 的联网能力。
    - `#93266` 修复了飞书（Feishu）话题队列分发作用域不准确的问题。
    - `#93276` 停止了插件工具发现加载时清除活动 Provider 的严重 Bug。
    - `#93265` 极大简化了 `openclaw setup` 流程，支持智能检测现有环境并自动配置。
    - `#93282` 修复了 ClawHub 官方 NPM 目录条目安装时不被信任的问题。
- **闭环修复**: **`#43015`** 已关闭 (message.send schema 过度暴露字段导致 GPT 自动填充故障)，该问题已得到修复。

### 4. 社区热点

- **🔥 最高关注：跨平台客户端**
    - **Issue #75**: [Linux/Windows Clawdbot Apps](openclaw/openclaw Issue #75) (评论 109, 👍 79)
    - **分析**: 作为长期占据热度的 Issue，今日依旧活跃。macOS 和移动端已有客户端下，社区对桌面全平台（尤其是 Windows 和 Linux）支持的呼声从未减弱。这不仅是功能缺失，更反映了用户希望将 OpenClaw 作为日常主力工具投入生产的强烈诉求。

- **😨 安全焦虑：内部处理文本泄露**
    - **Issue #25592**: [Text between tool calls leaks to messaging channels](openclaw/openclaw Issue #25592) (评论 32, P1, Security)
    - **分析**: Agent 在执行工具调用时产生的内部日志、处理确认等文本被错误路由到用户聊天窗口，这是一个严重的 UX 和信息安全事故。社区对此反响强烈，是当前最紧迫需要修复的 P1 安全问题。

- **💡 功能共振：内部网络访问权限**
    - **Issue #39604**: [Add tools.web.fetch.allowPrivateNetwork](openclaw/openclaw Issue #39604) (评论 13, 👍 9)
    - **分析**: 获得了极高比例的支持率（9个赞/13条评论）。反映了大量的私有化部署、家庭实验室（Homelab）和企业内网用户对 Agent 访问内部服务（NAS、内网 API 等）的刚性需求。该功能极有可能被快速纳入路线图。

- **另有讨论激烈的议题:**
    - `#9443` [Prebuilt Android APK releases](openclaw/openclaw Issue #9443) (25 条评论) - 社区对降低使用门槛的呼声。
    - `#32296` [Bug: Agent replies to previous message](openclaw/openclaw Issue #32296) (15 条评论, P1) - 会话混乱是当前最大的体验降级点。

### 5. Bug 与稳定性

过去 24 小时是 Bug 汇报的高发期，以下按严重程度排列：

- **P1（严重）**:
    - **会话混乱**: `#32296` Agent 回复上一条消息（会话上下文错乱）。*Linked PR Open*
    - **消息泄漏**: `#25592` 工具调用间文本泄漏到信使。*Linked PR Open*
    - **数据丢失/覆盖**: `#22676` Signal 守护进程重启竞态 (crash-loop)。*Linked PR Open*
    - **环境变量回归**: `#31583` `exec` 工具不继承技能配置的环境变量（Regression）。*Linked PR Open*
    - **数据覆盖**: `#40001` Write 工具无追加模式，隔离 Cron 会话覆盖共享文件。*Linked PR Open*
    - **消息阻塞**: `#40611` Heartbeat 漂移修复导致攻击性重试阻塞 Telegram。*Linked PR Open*
    - **Bootstrap 失效**: `#29387` Agent 目录下的 Bootstrap 文件被静默忽略。*Needs Maintainer Review*

- **P2（高）**:
    - **UI 回归**: `#32473` 控制 UI 要求 HTTPS/本地安全上下文。*Linked PR Open*
    - **头像断层**: `#38439` / `#41201` Webchat 和控制 UI 头像 404 回归。*Needs Maintainer Review*
    - **平台兼容性**: `#40540` `openclaw update` 在 Windows 上因 EBUSY 失败。*Needs Maintainer Review*
    - **渠道路由**: `#41165` Telegram DM 仍错误路由到主会话。*Needs Maintainer Review*
    - **飞书媒体**: `#41744` 飞书读取图片后最终出站 payload 丢失附件。*Linked PR Open*
    - **其他**: `#41545` 编辑 WebSocket URL 导致 Gateway Token 被清除；`#38327` 在 google-vertex 模型下报 `Cannot convert undefined or null to object`。

### 6. 功能请求与路线图信号

从今日的 Issue 中可以提炼出清晰的社区期待方向：

- **全面安全性增强（架构级）**：用户不只是在报告 Bug，而是在主动设计解决方案。
    - `#10659` (Masked Secrets: 防止 Agent 看见原始 API key)
    - `#7707` (Memory Trust Tagging: 按来源标记记忆可信度)
    - `#7722` (Filesystem Sandboxing Config: 配置文件访问白名单)
    - `#6615` (Denylist for exec-approvals: 命令黑名单)
    - `#6731` (Rewrite in Rust: 从语言层面保证内存安全)
    - `#92086` (Security Matrix runtime-fact audit model: 形式化安全审计)

- **Agent 协作与可编程性**：
    - `#22438` (Tiered bootstrap：分级加载节省 Token)
    - `#27445` (`announceTarget`: 子 Agent 完成通知可配置路由)
    - `#22358` (Post-subagent hooks：子任务结束后自动生成复盘报告)

- **用户体验打磨**：
    - `#12602` (Slack Block Kit 支持)
    - `#11665` (Webhook 复用 Session 支持多轮对话)
    - `#14785` (减少工具 Schema 固定开销 ~3500 Token/次)
    - `#33413` (Slack 显示步骤级运行状态)

### 7. 用户反馈摘要

- **肯定与期待**:
    - 用户对 `v2026.6.8-beta.2` 在 Telegram/WhatsApp 方向的改进表示欢迎，特别是富文本格式的正式支持解决了长期以来的痛点。
    - 新增的安全审计模型和 Markdown 注入扫描虽尚未合并，但社区对其“从架构层面治理安全”的思路给予积极评价。

- **痛点与抱怨**:
    - **平台缺失（Windows/Linux）**: `#75` 的持久高热度表明桌面用户感到被边缘化，部分用户表示因此暂未深度使用。
    - **配置复杂度过高**: `#16670` 指出 Memory/Embedding 配置在初始化向导中完全缺失，导致新手用户无法体验核心的跨会话记忆能力。
    - **Docker 环境体验差**: `#31331` Docker + Sandbox 工作区无法挂载的问题让容器化用户感到沮丧。
    - **回归破坏性强**: 多名用户在 `#31583` 和 `#32473` 中反馈“之前还能用”的回归问题，对使用了稳定版本的团队打击较大。

### 8. 待处理积压

- **长期愿望清单**:
    - `#75` Linux/Windows 客户端 (109 条评论，创建于 1 月). 项目方目前无明确官方回应，积压严重。
    - `#6731` Rust 重写提议 (P1, 仅讨论无明确实施方案)。

- **评审队列阻塞**:
    - 大量用户期待的 Issue（如 `#9443` APK 发布, `#12602` Slack Block Kit, `#7707` 内存信任）均处于 `clawsweeper:needs-maintainer-review` 或 `clawsweeper:needs-product-decision` 状态。维护者需尽快做出决策，以免挫伤社区贡献者提交 PR 的积极性。

- **功能 PR 审核停滞**:
    - `#89596` [Fix policy allowlists] - 状态 `re-review loop` (P3)，推进缓慢。
    - `#43656` [Cross-gateway sessions] - 已标记为 stale，功能价值极高但维护者无暇推进。
    - `#44143` [Serialize outbound deliveries] - 等待作者回复环节已超过 72 小时。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告（2026-06-16）

## 1. 生态全景

2026年6月16日，个人 AI 助手与自主智能体开源生态呈现出**空前繁荣与高度竞争**的态势。核心参照项目 **OpenClaw** 维持着单日近 500 条 Issue/PR 的超高强度迭代，其衍生产品（PicoClaw、NanoClaw）与独立项目（Hermes Agent、ZeroClaw、IronClaw、CoPaw）在功能深度与落地场景上各展所长。社区贡献热情极高，但**评审积压、稳定性回退**成为多个项目的共性瓶颈。安全隔离、多智能体编排、上下文成本控制及全平台客户端覆盖已成为决定项目下一阶段竞争力的关键战役。

## 2. 各项目活跃度对比

| 项目 | 当日Issues更新 | 当日PR更新 | 新版本 | 健康度评估 |
|------|----------------|------------|--------|------------|
| **OpenClaw** | ~500条（新开481） | ~500条（合并87，待合并413） | v2026.6.8-beta.2 | 🔥 高热运行，评审瓶颈显著 |
| **NanoBot** | 5条（3新开，2关闭） | 26条（合并5，待合并21） | 无 | ✅ 高活跃，迭代健康 |
| **Hermes Agent** | 50条 | 50条（合并4） | 无 | ✅ 极高活跃，功能与修复并行 |
| **PicoClaw** | 3条（2关闭，1开放） | 13条（合并3） | nightly自动构建 | ✅ 高活跃，安全诊断增强 |
| **NanoClaw** | 0条（无新增） | 12条（合并3） | 无 | ✅ 低报告高产出，稳定性导向 |
| **NullClaw** | 2条活跃 | 1条（基本依赖更新） | 无 | ⚠️ 维护低潮，核心Bug待响应 |
| **IronClaw** | 46条 | 50条（合并18） | 无 | ✅ 极高活跃，授权/WebUI修复冲刺 |
| **LobsterAI** | 2条（均为旧Issue更新） | 11条（合并5） | 无 | 🔶 中等活跃，聚焦语音重构 |
| **TinyClaw** | 0 | 0 | - | ❌ 无活动 |
| **Moltis** | 0 | 2条（新提交，未合并） | 无 | 🔶 低活跃，外部Agent集成起步 |
| **CoPaw (QwenPaw)** | 50条 | 50条 | 无 | ✅ 高活跃，严重Bug与功能上线并存 |
| **ZeptoClaw** | 0 | 0 | - | ❌ 无活动 |
| **ZeroClaw** | 50条 | 50条 | 无 | ✅ 极高活跃，RFC密集，技术冲刺 |

## 3. OpenClaw 在生态中的定位

OpenClaw 仍是该生态的 **“基础设施级”核心参照**，其社区规模（单日 500+ 动态）、功能广度（信使增强、CLI后端、自动修复管线）和衍生项目数量（PicoClaw、NanoClaw 等均直接基于其代码库）均领先于同类。今日合并的自动修复管线（#68936）与 Telegram 富文本支持标志着其持续推进工程效能与用户体验。

但 OpenClaw 也暴露出 **评审效率严重滞后**的问题：待合并 PR 超 400 条，大量长期愿望清单（如 Linux/Windows 客户端 #75）无官方回应。如果维持此状态，可能将活跃贡献者推向更敏捷的衍生项目或竞品。其技术路线仍以信使优先、通用智能体为主，而零一Claw、Hermes 等已开始在 **多智能体路由和 Rust/WASM** 方向拉开差距。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
|----------|----------|----------------|
| **安全与隔离** | OpenClaw, Hermes Agent, ZeroClaw, PicoClaw, IronClaw | 内部文本泄漏（OpenClaw #25592）、MCP隔离失效（ZeroClaw #7733）、凭据作用域重构（IronClaw #4935）、反向代理绕过（PicoClaw #3069） |
| **多智能体编排与路由** | Hermes Agent, ZeroClaw, CoPaw | DAG任务图引擎（Hermes #47016）、多智能体路由（ZeroClaw #2767）、Agent OS Driver（CoPaw #5067） |
| **上下文/Token优化** | CoPaw, NanoBot, Hermes Agent, OpenClaw | Token可视化（CoPaw #4310/5130）、历史压缩改用Token计数（NanoBot #4352）、分级bootstrap（OpenClaw #22438）、上下文窗口优化（Hermes #22620） |
| **跨平台客户端** | OpenClaw, CoPaw, Hermes Agent | Linux/Windows桌面客户端（OpenClaw #75）、macOS崩溃（CoPaw #5209）、桌面端字体/UI调节（Hermes #46097） |
| **MCP协议集成** | NanoClaw, CoPaw, ZeroClaw, Hermes Agent | 远程MCP（NanoClaw #2776）、MCP技能标准化（CoPaw）、MCP安全修复（ZeroClaw #7733） |
| **CI/供应链安全** | ZeroClaw, IronClaw, PicoClaw | 硬化CI与SBOM（ZeroClaw #7675）、Wasmtime漏洞（IronClaw #4949）、依赖更新统一管理 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 通用智能体运行时，信使通道最丰富 | 开发者、社区用户，自部署 | 插件生态最广，社区驱动评审重 |
| **NanoBot** | 快速部署、WebUI驱动、Provider兼容 | 个人开发者，快速体验 | 轻量，强调WebUI与config同步 |
| **Hermes Agent** | 多智能体DAG编排、桌面端深度优化 | 复杂工作流用户，企业 | DAG引擎 + 桌面全功能客户端，内存隔离弱 |
| **PicoClaw** | 嵌入/RISC-V、安全诊断 | 边缘设备用户 | 基于OpenClaw但极度精简，nightly构建 |
| **NanoClaw** | 低运维、容器化、MCP技能生态 | DevOps，快速搭建自用Agent | 自动化更新，容器优化，OneCLI网关 |
| **IronClaw** | 企业级授权与凭据、Reborn WebUI | 安全敏感的企业团队 | 强OAuth、凭据作用域、可观测性管线 |
| **LobsterAI** | 语音输入、文档Artifact分享 | 办公场景（网易生态） | 短ASR转实时，文档协同，Electron桌面 |
| **CoPaw (QwenPaw)** | 国内渠道（小艺/飞书）、阿里云生态 | 国内用户、鸿蒙用户 | 大厂维护，快速迭代但稳定性回退较多 |
| **ZeroClaw** | 多Agent路由、Rust/WASM演进 | 技术先锋、架构探索者 | 多份架构RFC，计划摆脱Node.js依赖 |
| **Moltis** | 外部代理聚合、模型/effort选择 | 多模型编排用户 | 作为中间层对接多家Provider，功能起步 |

## 6. 社区热度与成熟度分层

- **第一梯队：极高活跃，功能迭代冲刺期**  
  OpenClaw、Hermes Agent、ZeroClaw、IronClaw、CoPaw。日均Issue/PR更新均在50+甚至500+，PR合并频繁，但同时面临回归Bug频发、评审挤压压力。成熟度方面，OpenClaw在功能广度领先，Hermes在架构深度领先，ZeroClaw在技术前瞻性领先，但稳定性均未达到“生产无忧”等级。

- **第二梯队：高活跃，健康迭代**  
  NanoBot、PicoClaw、NanoClaw。更新量适中（10-30条PR），合并节奏好，Issues管理较轻。项目处于“功能增量发布+持续修复”的良性循环，适合普通开发者快速上手。

- **第三梯队：中等活跃，局部重构期**  
  LobsterAI。当前聚焦语音模块重构，Issues长期积压但PR活跃，属于产品方向调整中的正常收敛。

- **第四梯队：低活跃或停滞**  
  NullClaw（核心Bug未解决）、Moltis（功能起步缺迭代）、TinyClaw与ZeptoClaw（无活动）。这些项目存在社区关注度流失的风险，除非有重大更新或维护者回归。

## 7. 值得关注的趋势信号

1. **安全架构从前置修补转向体系化设计**  
   ZeroClaw的Rust/WASM计划（#7674）、IronClaw的凭据作用域（#4935）、OpenClaw的安全审计模型（#92086）表明，项目方不再满足于打补丁，而是从语言层面和架构层面治理安全。这对未来企业级采用至关重要。

2. **多智能体路由成为“标配级”功能**  
   Hermes DAG与ZeroClaw多Agent同时发力，OpenClaw也在讨论Post-subagent hooks（#22358）。2026下半年，单一Agent将不再是智能体项目的主打，“Agent网络”将是竞争焦点。

3. **Token消耗控制从优化走向可视化**  
   CoPaw合并Token用量卡片获得社区点赞，NanoBot改用Token计数字节，OpenClaw呼吁分级加载（#22438）。用户对成本敏感度显著上升，下一阶段上下文压缩将集成至运行时内部。

4. **国内势力深度渗透开源智能体生态**  
   CoPaw（阿里/Huawei）、LobsterAI（网易）以及多项目对飞书/企业微信的支持（OpenClaw、NanoBot、CoPaw）显示国内厂商正以开源形式抢占入口。对国际开发者来说，这既是生态补充也意味着标准分化。

5. **MCP工具协议走向事实标准**  
   几乎每个活跃项目都在增强MCP支持。MCP正在取代私有工具定义，成为Agent连接外部世界的“USB接口”。未来工具的跨项目复用将变得更加容易。

6. **评审机制成为项目发展的最大制约**  
   OpenClaw 400+待合并PR、ZeroClaw大量needs-author-action PR、CoPaw严重Bug因评审滞后持续数周。社区贡献热情需要维护者及时响应，否则有分裂风险。**CI自动合并、分级review**或成为头部项目下一阶段必须引入的流程改进。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot 项目动态日报 | 2026‑06‑16**  

---

## 1. 今日速览  
过去 24 小时内，项目保持了极高的迭代活力：  
- **Issues**：5 条（3 条新开 / 活跃，2 条已关闭）  
- **Pull Requests**：26 条（待合并 21 条，已合并 / 关闭 5 条）  
- **新版本**：0 个  

社区贡献者提交了覆盖 WebUI、Provider、Bridge 等多个模块的新功能与修复，其中两项会话管理相关的修复已合并。整体来看，项目处于“大量功能开发并行 + 快速响应 Bug”的健康节奏。  

---

## 2. 版本发布  
今日无新版本发布。  

---

## 3. 项目进展  
今日合并 / 关闭的 **5 个 PR** 中，重要的两项功能 / 修复如下：  

| PR | 标题 | 关键影响 |
|----|------|----------|
| [#4359](https://github.com/HKUDS/nanobot/pull/4359) | fix(agent): refresh goal continuation context | 持续目标（sustained goal）现在延迟解析，确保长任务工具在 runner 调用期间创建的新目标能被后续提示真实引用，修复了目标上下文“快照”问题。 |
| [#4348](https://github.com/HKUDS/nanobot/pull/4348) | fix(session): keep auto compact suffix on user turn | 空闲自动压缩时，至少保留最近后缀并向后延伸到包含的用户 Turn，避免压缩后出现不完整的工具消息片段，提升多轮会话底纹质量。 |

这两项修复直接增强了 Agent 长对话的稳定性和上下文一致性，是本次迭代的重要质量提升。  

---

## 4. 社区热点  

### 最活跃 Issue  
- **[#4360](https://github.com/HKUDS/nanobot/issues/4360)** – `[bug] "end of file unexpected" during installer`（4 条评论）  
  在官方 `debian:13` Docker 容器中安装时，pip 脚本报语法错误，疑似与所依赖的 shell 环境有关。该问题直接影响新用户首次部署，讨论热度最高。  

### 其他高关注度的讨论  
- **[#4287](https://github.com/HKUDS/nanobot/issues/4287)** – 空响应未触发 fallback（2 条评论）  
  用户反映 DeepSeek 在高负载时返回空 completion，但 Nanobot 将其分类为 “non‑fallbackable”，导致无备用模型接管。  
- **[#4322](https://github.com/HKUDS/nanobot/issues/4322)**（`question, stale`）– `NameError: session_key`（1 条评论）  
  合并主干后出现的崩溃问题，社区正在确认根因与修复方向。  

### 热议 PR  
功能型 PR 虽然评论数未显式给出，但以下 PR 因其功能范围或重要性在社区中被反复引用：  
- [#4320](https://github.com/HKUDS/nanobot/pull/4320) – 新增审计模块  
- [#4351](https://github.com/HKUDS/nanobot/pull/4351) – 增强 Mistral 支持  
- [#4350](https://github.com/HKUDS/nanobot/pull/4350) – 集成 Keenable 搜索  

---

## 5. Bug 与稳定性  

按严重程度排列今日报告的问题：  

| 问题 | 严重程度 | 状态 | 说明 | 是否有 Fix PR |
|------|----------|------|------|---------------|
| [#4360](https://github.com/HKUDS/nanobot/issues/4360) – Docker 安装语法错误 | **高** | Open | 完全阻塞新用户在 `debian:13` 环境部署。 | 暂无 |
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) – 空响应不 fallback | **中** | Open | 影响高负载时段的服务连续性。 | 未直接 fix；但 [#4358](https://github.com/HKUDS/nanobot/pull/4358) 解决了空响应重试时重复记录用户消息的问题，属于同类改进。 |
| [#4322](https://github.com/HKUDS/nanobot/issues/4322) – merger 后 `session_key` NameError | **中** | Open | 导致 agent 启动时崩溃，影响 `fix/prompt-caching` 分支用户。 | 暂无 |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) – 丢失 "sustained goal" context | **低** | Closed | 用户反映文章创作中反复提示缺失上下文，已随 [#4359](https://github.com/HKUDS/nanobot/pull/4359) 合并修复。 | 已合并 |
| [#4309](https://github.com/HKUDS/nanobot/issues/4309) – API 返回零 usage tokens | **低** | Closed | 违反 OpenAI API 行为预期，已修复并关闭。 | 已合并 |

此外，今天提交了 **大量稳定性修复 PR**（尚待合并），涵盖：  
- 图片剥离后路径泄露（[#4346](https://github.com/HKUDS/nanobot/pull/4346)）  
- Replay‑window 截断导致历史丢失（[#4349](https://github.com/HKUDS/nanobot/pull/4349)）  
- History digest 改用 token 计数而非字符（[#4352](https://github.com/HKUDS/nanobot/pull/4352)）  
- Anthropic 工具 ID 格式校验（[#4356](https://github.com/HKUDS/nanobot/pull/4356)）  
- 音频转码后 STT 空结果（[#4353](https://github.com/HKUDS/nanobot/pull/4353)）  

这些 PR 反映了社区对运行可靠性的高度重视。  

---

## 6. 功能请求与路线图信号  

今日提交的 **20+ 条新 PR** 体现出强烈的功能扩展趋势，以下功能最可能被纳入下一版本：  

| 功能 | PR | 信号强度 |
|------|----|----------|
| **WebUI 自动化管理视图** – 列表、过滤、启停自动化 | [#4330](https://github.com/HKUDS/nanobot/pull/4330) | 高（chengyongru 主导，UI 层关键补充） |
| **WebUI 设置面板与 config.json 同步** – 缩小两者差距 | [#4313](https://github.com/HKUDS/nanobot/pull/4313) | 高（长期用户诉求） |
| **Agent 审计模块** – 可观测 action 日志 | [#4320](https://github.com/HKUDS/nanobot/pull/4320) | 中高（企业级需求） |
| **Mistral 专属适配器** – 修复参数兼容性 | [#4351](https://github.com/HKUDS/nanobot/pull/4351) | 中高（增加主要供应商支持） |
| **Keenable 搜索提供者** – 新增 Web Search 后端 | [#4350](https://github.com/HKUDS/nanobot/pull/4350) | 中（丰富搜索选择） |
| **Cron “静默”作业** – 只在有报告产出时发送消息 | [#4357](https://github.com/HKUDS/nanobot/pull/4357) | 中（减少噪音） |
| **飞书 WebSocket 卡片** – 支持实时消息格式 | [#4342](https://github.com/HKUDS/nanobot/pull/4342) | 中（飞书用户刚需） |
| **WhatsApp 已读回执** – 蓝勾功能 | [#4354](https://github.com/HKUDS/nanobot/pull/4354) | 低（体验增强） |

上述高信号特性表明项目正在向全功能 AI 助手基础设施演进，尤其在 WebUI、Provider 兼容性、可观测性三个方向发力。  

---

## 7. 用户反馈摘要  

| Issue | 用户场景 / 痛点 | 反馈倾向 |
|-------|----------------|----------|
| [#4360](https://github.com/HKUDS/nanobot/issues/4360) | 在 `debian:13` 纯净容器中安装失败，SHELL 语法错误。 | **不满**，期待快速修复。 |
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | 生产环境用 DeepSeek v4，高峰时空响应，agent 不 fallback。 | **功能缺失感**，希望增加 fallback 条件。 |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | 创建文章时 agent 反复提示缺少“sustained goal”上下文。 | **困惑**，已确认是上下文未刷新导致，已修复。 |
| [#4322](https://github.com/HKUDS/nanobot/issues/4322) | 合并分支后 agent 启动即 crash，`session_key` 未定义。 | **困扰**，影响开发测试。 |
| [#4309](https://github.com/HKUDS/nanobot/issues/4309) | `nanobot serve` 的 OpenAI 兼容接口总返回 0 token 用量。 | **不符预期**，已修复。 |

从评论看，用户对 **安装顺畅度** 和 **高负载下的稳定性** 有较高期望，同时对 WebUI 与 config.json 的一致性持续关注。  

---

## 8. 待处理积压  

以下问题 / PR 停留时间较长或已标记为 `stale`，建议维护者优先关注：  

| 项目 | 类型 | 创建 | 最后更新 | 备注 |
|------|------|------|-----------|------|
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) – 空响应 fallback | Issue (Bug) | 2026‑06‑10 | 2026‑06‑15 | 已一周，影响生产环境。 |
| [#4322](https://github.com/HKUDS/nanobot/issues/4322) – `session_key` NameError | Issue (Bug/Stale) | 2026‑06‑13 | 2026‑06‑15 | 标记 `stale`，但会导致崩溃。 |
| [#4303](https://github.com/HKUDS/nanobot/pull/4303) – MCP streamableHttp crash | PR (Fix) | 2026‑06‑11 | 2026‑06‑15 | 有复现步骤，待 Review。 |
| [#4320](https://github.com/HKUDS/nanobot/pull/4320) – 审计模块 | PR (Feat) | 2026‑06‑12 | 2026‑06‑15 | 标记 `release-TCH-486-audit`，讨论中。 |
| [#4313](https://github.com/HKUDS/nanobot/pull/4313) – WebUI / config.json 同步 | PR (Feat) | 2026‑06‑12 | 2026‑06‑15 | 改动量大，需仔细审查。 |

**特别提醒**：`#4360`（installer bug）虽刚提交，但因其阻碍新用户准入，建议本周内分配修复。  

---

*数据来源：HKUDS/nanobot GitHub 仓库，统计时间窗口 2026‑06‑15 ~ 2026‑06‑16。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，根据您提供的 Hermes Agent 项目数据，以下是为您生成的 2026-06-16 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-16

## 1. 今日速览

Hermes Agent 在过去24小时内保持了极高的社区活跃度，共产生 **50 条 Issue 更新**和 **50 条 PR 更新**。尽管无新版本发布，但项目在核心架构（DAG多智能体编排 PR #47016）和桌面端体验（合成器模型选择器 PR #46959）上均有重大代码推进。值得注意的是，v0.16.0 版本引入了多个回归性 Bug（如 SQLite 崩溃 #47002 及桌面端运行历史为空 #46979），当前修复工作正在密集进行中。社区对“远程 Agent + 本地工具执行”（#18715）和“上下文窗口优化”（#22620）等功能诉求强烈，整体项目健康度良好，处于高强度的“功能迭代与稳定性修复并行”阶段。

## 2. 版本发布

**无新版本发布。** 最新版本仍为 v0.16.0 (2026.6.5)，当前社区反馈主要集中在修复该版本的回归问题。

## 3. 项目进展

今日虽仅有 **4 个 PR/Issue 被合并/关闭**，但项目在关键架构上取得了突破性进展：

**合并/关闭：**
- **PR [#46958]**: 修复了在容器化环境中仪表盘显示不必要的更新控制按钮的问题，提升了部署兼容性。
- **Issue [#46593]** (已关闭): 修复了 Kanban Worker 因未调用 `kanban_complete` 而显示无意义的 “protocol violation” 错误，关联的修复 PR [#46985] 已提交。

**推进中的重磅 PR（待合并）：**
- **PR [#47016]** (DAG 任务图引擎): 这是社区贡献的又一重大架构更新。引入了基于 DAG 的任务图执行引擎，支持 DFS 循环检测和并行 Wave 执行，为复杂的多智能体工作流编排奠定了基础。该 PR 与早期的 #12436 形成互补。
- **PR [#46959]** (桌面端合成器/模型选择器): 大幅改写了桌面端聊天体验，包括可单击切换的模型选择器、模型级预设，以及断开外部 Provider 连接的 UI 支持。
- **PR [#47011] & [#47015]** (网关 & 后端修复): 修复了桌面端全局远程 Profile 切换时 REST 调用失效的问题，以及 Microsoft Teams 平台图片附件的 Bearer 认证问题。
- **PR [#47013]** (Windows MCP 体验优化): 修复了 Windows 平台下启动 MCP 服务器时频繁弹出无法关闭的黑色控制台窗口的恼人问题。

> 链接：[PR #47016](https://github.com/NousResearch/hermes-agent/pull/47016), [PR #46959](https://github.com/NousResearch/hermes-agent/pull/46959)

## 4. 社区热点

1.  **#7237 [CLOSED] “输出长度限制导致响应截断”**
    - **热度**: 评论数 **50 条**（全时段最高），👍 6。
    - **分析**: 这是社区在过去24小时最关注的 Issue。用户在使用 CLI 或 Telegram/Discord 网关进行长文本交互时频繁遭遇截断。该 Bug 现已关闭，但如此高的讨论量凸显了“长上下文输出完整性”是当前 Agent 落地场景中的核心痛点。用户对中间流式输出的丢失容忍度极低。

2.  **#18715 [OPEN] “支持远程 Hermes Agent + 本地工具执行”**
    - **热度**: 👍 **15 个**（全时段最高赞）。
    - **分析**: 该 Feature Request 获得了压倒性的支持。典型场景是让重型 LLM 推理在远端机器（MaaS）进行，而将代码执行、文件操作等敏感工具保留在本地。这不仅是功能请求，更指明了**企业级部署的架构方向**——拆分计算力与安全边界。

3.  **#46975 [OPEN] “桌面端 Profile 切换导致僵尸进程”**
    - **热度**: 今日热议。
    - **分析**: 用户反馈在切换 Profile 后，后台会积压大量未清理的 `hermes dashboard` 进程，消耗数百 MB 内存。这直接影响了长周期运行稳定性，是阻碍用户将 Agent 作为常驻应用使用的关键因素。用户对该问题的描述非常详细（80+ 进程，700MB 内存占用），说明其影响严重。

> 链接：[Issue #7237](https://github.com/NousResearch/hermes-agent/issues/7237), [Issue #18715](https://github.com/NousResearch/hermes-agent/issues/18715), [Issue #46975](https://github.com/NousResearch/hermes-agent/issues/46975)

## 5. Bug 与稳定性

今日报告的 Bug 量较大，按严重程度排列如下：

**严重（P1 - 关键路径阻塞）：**
- **#46675**: Max OAuth 令牌因 `mcp_` 工具名前缀被 Anthropic 拒绝（HTTP 400）。影响所有使用 Anthropic Max OAuth 用户的工具调用功能。
- **#47002**: **v0.16.0 回归** — `SessionDB` 在缺少 `trigram` 分词器的 SQLite 构建下初始化崩溃，导致会话数据库完全不可用。修复 PR [#47007] 已针对 Windows WAL 模式损坏提交。
- **#40691**: Telegram 网关在轮询冲突恢复后完全“冻结”，停止处理所有消息（**P1 Bug，已开放 10 天，尚未关联修复 PR**）。

**高（P2 - 功能严重受损）：**
- **#46303**: 并发 Session 发生严重的记忆/上下文污染（共享 Memory Injection 和工作树），无隔离机制。
- **#46979**: **v0.16.0 回归** — 桌面端 Cron Job 的“运行历史”面板显示空白。
- **#46934**: 网关重启后，卡住的 `resume_pending` Session 绕过空闲重置，导致上下文泄漏。
- **#46897**: 后台“自我改进”审查误报“技能已创建”，但技能实际无法加载。
- **#46917**: “角色”指令要求保持沉默时，Agent 仍被强制输出占位符 `'(silence)'`。

**中（P3 - 体验与兼容性问题）：**
- **#46975**: 桌面端 Profile 切换产生僵尸进程（如上）。
- **#46941**: 在飞书等平台中，终端命令代码块被截断。
- **#47006**: 自定义端点配置向导因无法请求 `/v1/models` 而硬失败。

> 链接：[Issue #46675](https://github.com/NousResearch/hermes-agent/issues/46675), [Issue #47002](https://github.com/NousResearch/hermes-agent/issues/47002), [PR #47007](https://github.com/NousResearch/hermes-agent/pull/47007)

## 6. 功能请求与路线图信号

今日涌现的功能请求集中在**架构灵活性与用户体验精细化**：

**核心架构：**
- **#22620** (P3): “技能列表膨胀导致上下文窗口爆炸”。提出了基于向量的技能路由或懒加载方案。这是解决复杂 Agent 上下文中 Skill 数量增长的核心设计思路，具有极高的技术前瞻性。
- **#47014** (P3): 允许 `delegate_task` 进行“每次调用模型覆盖”。这与当前正在推进的 DAG 编排（#47016）相呼应，是实现子任务级模型路由的基础。

**用户体验平台化：**
- **#46097** (P3): 桌面端字体大小调节。这是从“发烧友工具”向“消费级应用”转型的标志性需求。
- **#46839** (P3): 中国用户反馈 Docker 安装因 GFW 受阻，建议优化中国用户的安装体验。
- **#46094 & #46081** (PR P3): 将 OpenRouter Fusion 和 Mixture of Agents (MoA) 作为“虚拟 Provider”暴露为标准模型选择。这表明**Hermes Agent 正在从“单一模型客户端”进化为“模型编排与聚合平台”**。

> 链接：[Issue #22620](https://github.com/NousResearch/hermes-agent/issues/22620), [Issue #47014](https://github.com/NousResearch/hermes-agent/issues/47014)

## 7. 用户反馈摘要

- **长文本生成体验差（#7237）**: 用户依赖 Agent 生成完整报告或代码，但 `output length limit` 错误粗暴截断回复。这说明流式输出架构在应对不确定输出长度时缺乏优雅降级策略，影响了 Agent 在“创作”场景下的可用性。
- **自定义 Provider 兼容性不足（#40480, #47006）**: 用户配置了非标准 OpenAI 兼容端点（如 SenseNova、Cohere）后，桌面端模型选择器不显示、配置向导卡死。底层假设了标准的 `/v1/models` 接口，对私有化/兼容性部署场景支持不够友好。
- **桌面端生产环境稳定性存疑（#46975, #46303, #46934）**: 连续的稳定性报告（僵尸进程、内存污染、会话泄漏）表明，当前架构在设计之初未充分考虑长时间多 Session 并行运行的生产环境要求，进程模型和内存隔离机制有待加强。
- **Agent 自主性与可控性的拉扯（#46917, #27178）**: 用户既希望 Agent 能自主执行，又苦恼于其过度遵循协议（强制沉默回应、Kanban 严格协议违规）。这反映了 Agent 系统设计中的经典矛盾：如何平衡“灵活自主”与“严格预期”。

## 8. 待处理积压

以下为长期未响应或积压的重要议题，可能成为项目健康度的隐患：

- **PR [#12436]** (DAG 编排，自 2026-04-19): 早期的多智能体编排基础设施 PR，已超过两个月未合并，当前被更新更全的 #47016 接替。需要维护者明确 Ops 方向并处理旧 PR 的关闭/引用。
- **PR [#10707]** (OpenRouter Base URL 配置被忽略，自 2026-04-16): 一个基础的配置 Bug 修复（允许用户指定自定义镜像/代理），积压已超两个月，可能影响特定地区用户的使用。
- **PR [#32663]** (OpenViking 内存输入净化，自 2026-05-26): 安全相关的修复（防止 Prompt 污染泄露），无人审阅合并。
- **Issue [#31246]** (MCP 配置静默失效，自 2026-05-24): 用户配置 MCP 服务器后，如果 SDK 缺失或连接失败，系统毫无反馈，仅在 DEBUG 日志中体现。这会严重打击初次接触 MCP 用户的信心。
- **Issue [#40691]** (Telegram 网关 P1 Bug，自 2026-06-06): 作为 P1 级严重 Bug，已开放 **10 天**且无关联修复 PR，是当前最大的稳定性风险敞口。

> 链接：[PR #12436](https://github.com/NousResearch/hermes-agent/pull/12436), [Issue #31246](https://github.com/NousResearch/hermes-agent/issues/31246), [Issue #40691](https://github.com/NousResearch/hermes-agent/issues/40691)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 —— 2026-06-16

## 今日速览
过去 24 小时内，PicoClaw 共产生 **13 个 PR 更新**（其中 3 个已合并/关闭）、**3 个 Issue 更新**（2 个已关闭，1 个保持开放）以及 **1 个 nightly 构建版本**。项目核心贡献者集中于错误处理规范化、安全诊断增强和代码健壮性改进，社区侧则围绕 RISC‑V 兼容性、QQ 频道连接问题和允许列表绕过漏洞展开讨论。整体呈现高活跃度，代码质量与安全性是今日重点。

## 版本发布
### 🆕 `nightly` 自动构建
- **版本**: `v0.2.9-nightly.20260616.c1ff5aa6`
- **类型**: 每日自动构建，可能不稳定
- **完整变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **破坏性变更**: 未注明，请勿在生产环境使用
- **迁移注意**: 此版本为开发主线快照，建议仅用于测试

## 项目进展
### 今日合并/关闭的 PR
| PR | 类型 | 摘要 |
|----|------|------|
| [#3096](https://github.com/sipeed/picoclaw/pull/3096) | 文档 | 向 README 添加 PicoPaw 横幅，提升品牌一致性 |
| [#3126](https://github.com/sipeed/picoclaw/pull/3126) | 安全/诊断 | 改进启动器允许列表绕过诊断，新增 `allow_localhost_bypass` 配置的显式日志 |
| [#3097](https://github.com/sipeed/picoclaw/pull/3097) | 功能 | 在 Web 聊天输入框下方添加 Shift+Enter 换行提示，优化用户交互 |

**整体推进**: 2 个修复/优化 + 1 个小功能落地，安全诊断能力得到增强，文档和 UI 细节同步改善。

## 社区热点
### 评论最活跃的 Issue
- **[#2887 [CLOSED] .deb version on RISC-V is not functional with OpenAI model](https://github.com/sipeed/picoclaw/issues/2887)**  
  10 条评论，讨论在 RISC‑V 平台下 OpenAI 模型不可用的问题，虽已关闭但仍引起跨架构兼容性关注。

- **[#3015 [OPEN] QQ channel connection failed on Windows after build](https://github.com/sipeed/picoclaw/issues/3015)**  
  3 条评论，用户报告 Windows 上 QQ 频道启动时 token 获取超时，仅涉及 QQ 频道，Pico 频道正常。该 issue 因标记为 `stale` 但至今未关闭，社区期待处理。

### 高安全性关注
- **[#3069 [CLOSED] allowed_cidrs bypass via same-host reverse proxy](https://github.com/sipeed/picoclaw/issues/3069)**  
  零评论但严重性高：同一主机上的反向代理可通过 `RemoteAddr` 绕过访问白名单。已被关闭，对应的 PR [#3126](https://github.com/sipeed/picoclaw/pull/3126) 已合并以增强诊断。

## Bug 与稳定性
按严重程度排列：

| 严重程度 | Issue/PR | 状态 | 说明 |
|----------|----------|------|------|
| **严重** | [#3069](https://github.com/sipeed/picoclaw/issues/3069) | 已关闭 | 安全绕过漏洞：同机反向代理可突破 `allowed_cidrs` |
| **中等** | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | 开放 | Windows 上 QQ 频道 token 获取超时 |
| **低** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | 已关闭 | RISC‑V .deb 无法用 OpenAI 模型（可能跟架构依赖有关） |
| **代码质量** | 多个 PR（如 #3059, #3054, #3047, #3132 等） | 开放/待合并 | 显式忽略 Close 错误、类型断言安全检查、panic recovery 等，共 10 个开放 PR 专注于错误处理和稳定性 |

**已有 fix PR**: 安全漏洞诊断 (#3126) 已合并；其他稳定性 PR 仍待 review 或合并。

## 功能请求与路线图信号
今日无新增功能请求 Issue，但以下 PR 反映了社区期望的功能：

- **[#2975 [OPEN] Telegram: treat reply to bot message as mention](https://github.com/sipeed/picoclaw/pull/2975)**  
  在群组中回复机器人消息视为 @提及，提升用户体验，已开放超过 15 天，可能纳入下一版本。

- **[#3097 [CLOSED] Shift+Enter hint](https://github.com/sipeed/picoclaw/pull/3097)**  
  已于今天合并，属于一个轻量 UI 功能。

## 用户反馈摘要
从 Issues 评论中提炼的典型用户声音：

- **RISC‑V 用户**: “官方提供的 `.deb` 包在 RISC‑V 上无法与 OpenAI 模型正常工作，需用源码编译。” (#2887)
- **Windows 用户**: “每次构建后 QQ 频道都会超时，必须手动配置 token。” (#3015)
- **安全关注者**: “同一主机上的反向代理可以绕过 IP 白名单，期望更严格的检查。” (#3069 → 已通过 #3126 部分解决)

## 待处理积压
以下 Issue 或 PR 长期未获得维护者响应或停滞过久，建议优先关注：

| 序号 | 链接 | 类型 | 停滞原因 |
|------|------|------|----------|
| 1 | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | Issue (BUG) | 标记为 `stale` 但已开放 10 天，无维护者回复 |
| 2 | [#3059](https://github.com/sipeed/picoclaw/pull/3059) | PR (fix) | 关闭错误处理优化，等待 review 超过 7 天 |
| 3 | [#3054](https://github.com/sipeed/picoclaw/pull/3054) | PR (fix) | 类型断言安全性修复，等待 review 超过 7 天 |
| 4 | [#3047](https://github.com/sipeed/picoclaw/pull/3047) | PR (fix) | 恢复 JSONL 历史记录细节展示，等待 review 超过 8 天 |
| 5 | [#2975](https://github.com/sipeed/picoclaw/pull/2975) | PR (feature) | 功能请求已实现但停滞超过 16 天，建议决定合并方向 |

**健康度提示**: 项目整体活跃度高，但部分 `stale` 标记的 PR 和 Issue 已超一周未处理，可能影响贡献者积极性，建议维护者安排批量 review。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 NanoClaw 项目动态日报（2026-06-16）。

---

### NanoClaw 项目动态日报 | 2026-06-16

**项目状态总览：** `优` | **活跃度：** `高`

---

### 1. 今日速览

本日 NanoClaw 项目呈现典型的“低报告、高产出”健康状态。24小时内**无新增Issue提交**，表明现有版本的主体稳定性较好，未出现大规模Regression或用户恐慌。开发活动极为密集，**共12个Pull Request被更新**，其中**3个已被合并/关闭**，**9个处于活跃开发/待审阶段**。合并内容主要集中在基础设施可靠性（OneCLI网关升级同步）和核心数据持久化修复（Codex对话归档碎片化）。开放PR的管线极为丰富，涵盖高优Bug修复（WhatsApp媒体流、预算静默错误）和架构级新功能（远程MCP服务支持），显示了项目强大的迭代动能。

---

### 2. 版本发布

**本日无新版本发布。** 项目自上次 Release 以来已积累了9个待合并PR，预计近期可能发布集中更新。

---

### 3. 项目进展

今日共有 **3 个 PR** 完成合并/关闭，项目在可靠性和可维护性上稳步推进：

*   **[已合并] #2774 - 更新时自动升级 OneCLI 网关：**
    *   **内容：** 解决了 `update-nanoclaw` 在更新依赖版本后，未能同步升级运行中 OneCLI 网关的问题。
    *   **影响：** 避免了因代码与网关版本不匹配导致的潜在运行时故障，提升了更新过程的健壮性。
    *   (https://github.com/nanocoai/nanoclaw/pull/2774)

*   **[已合并] #2772 - 修复 Codex 对话归档（CDX-004）：**
    *   **内容：** 解决了系统默认仅为每个 Exchange 创建独立文件的碎片化问题。现在系统会以线程/续线ID为键进行追加写入。
    *   **影响：** 恢复了历史对话的连续性和可读性，对依赖 Codex 回放上下文的用户行为追踪至关重要。
    *   (https://github.com/nanocoai/nanoclaw/pull/2772)

*   **[已合并] #2773 - 精简 `add-codex` 文档：**
    *   **内容：** 移除了认证说明中冗余的 TTY 警告提示。
    *   **影响：** 降低了新手因信息过载而产生的困惑，提升了文档清晰度。
    *   (https://github.com/nanocoai/nanoclaw/pull/2773)

---

### 4. 社区热点

尽管本日 Issue/PR 中无公开评论的详细计数，但从 PR 的标签、关联 Issue 及核心内容可以清晰看到社区的讨论热点和背后诉求：

*   **外部集成生态是“第一优先”：** `#2776`（远程 MCP 服务器）和 `#2777`（Strava MCP 技能）代表了社区对打破生态围墙、接入更广泛外部工具的强烈渴望。用户不再满足于本地 Stdio 连接的 MCP，对于 HTTP/SSE 远程 MCP 的支持呼声极高，这直接关系到大模型 Agent 调用云 API 和第三方服务的核心能力。
*   **多模态与渠道“最后一公里”问题：** `#2778`（WhatsApp 入站媒体）和 `#2627`（跨平台 Reations 短码/Unicode 对齐）暴露了用户在实际运营中的“一致性”焦虑。用户期望 NanoClaw 不仅仅是一个“文本聊天机器人”，还能无缝处理图片、视频，并确保在任何渠道上的“表情回应”都能生效。
*   **长期等待的 CLI 体验：** `#2628`（自定义 Group ID）自 5 月 27 日提交后，已积压 20 天。用户对 `--id` 参数被静默忽略表示失望，本日该 PR 被更新引发了社区对管理员体验的再讨论。
    *   [#2776](https://github.com/nanocoai/nanoclaw/pull/2776)
    *   [#2777](https://github.com/nanocoai/nanoclaw/pull/2777)

---

### 5. Bug 与稳定性

本日修复清单深度聚焦于“静默失败”和“数据路由”两类高危问题：

*   **[严重] 预算/Token 耗尽错误被静默丢弃：**
    *   **表现：** `agent-runner` 在 LLM 调用遭遇预算限制时，错误被丢弃并不留日志，Agent 无响应且用户无法排查。
    *   **状态：** PR `#2759` 已提交修复，正在开放评审中。
    *   (https://github.com/nanocoai/nanoclaw/pull/2759)

*   **[严重] WhatsApp 入站媒体传输失败：**
    *   **表现：** `/add-whatsapp` 将下载的媒体文件写入了宿主机 `data/attachments/`，但 Agent 容器只挂载了会话目录，导致 Agent 无法读取收到的图片、视频和文档。
    *   **状态：** PR `#2778` 已提交修复。
    *   (https://github.com/nanocoai/nanoclaw/pull/2778)

*   **[中等] Signal 渠道启动静默失败：**
    *   **表现：** `restartService` 在未加载 plist 时进行空操作，导致渠道启动向导报告假性成功。
    *   **状态：** PR `#2626` 已提交，待合并。
    *   (https://github.com/nanocoai/nanoclaw/pull/2626)

*   **[中等] MCP Reactions 跨平台失效：**
    *   **表现：** 部分渠道（WhatsApp/Telegram）接受 Unicode 表情，但传递了 Shortcode 名，导致 Slack 外渠道静默失败。
    *   **状态：** PR `#2627` 已提交，待合并。
    *   (https://github.com/nanocoai/nanoclaw/pull/2627)

---

### 6. 功能请求与路线图信号

*   **[架构级信号] 远程 HTTP/SSE MCP 服务器支持：**
    *   PR `#2776` 扩展了 `McpServerConfig`，允许对接远程 MCP 服务。这是 NanoClaw 从纯本地运行走向混合架构的关键信号，极大概率会被纳入下一里程碑。
    *   (https://github.com/nanocoai/nanoclaw/pull/2776)

*   **[垂直集成信号] 官方 Strava MCP 技能：**
    *   PR `#2777` 提供了`/add-strava`一键集成命令。这暗示项目组开始封装主流服务的 MCP 技能，未来可能形成类似“技能市场”的生态入口。
    *   (https://github.com/nanocoai/nanoclaw/pull/2777)

*   **[容器优化信号] 调节 Agent 容器运行时：**
    *   PR `#2771` 为 Agent 容器增加 `--shm-size=1g` 和 `--init`。这解决了 Headless Chromium 在 Docker 下的内存和僵尸进程问题，信号意味着浏览器自动化已被完全纳入 Agent 标准套件，并进入了深度优化阶段。
    *   (https://github.com/nanocoai/nanoclaw/pull/2771)

*   **[UX 赋权信号] 允许自定义 Group ID：**
    *   PR `#2628` 虽然定位为 Bug 修复，实则是对管理员用户精细化配置权的承认，契合 DevOps 用户的标准化创建需求。
    *   (https://github.com/nanocoai/nanoclaw/pull/2628)

---

### 7. 用户反馈摘要

从近期 PR 关联的 Issues 中，可以提炼出当前用户群体的三大核心诉求：

1.  **拒绝静默失败，要求可观测性：**
    *   用户在 Signal 安装成功（实则空操作）(`#2583`) 和 Agent 预算耗尽无响应 (`#2751`) 后感到极度困惑。用户明确要求“看见失败”比“规避失败”更重要，这是对系统透明度的底线要求。
2.  **文档与实现的严格一致性：**
    *   对于 `--id` 功能 (`#2390`)，用户不满的不仅是功能缺失，更是“帮助文档写明 `(auto)` 但实际行为是 `(UUID)` 的误导”。用户对 API 诚实度要求极高。
3.  **极致的一致性桥接要求：**
    *   用户将 NanoClaw 定位为统一通信 Hub，因此对 WhatsApp 媒体不可见 (`#2778`)、跨平台表情失效 (`#2569`) 表现出高度敏感。平台间的”体验割裂“是导致用户流失的关键因素。

---

### 8. 待处理积压

以下三个 `eldar702` 提交的 PR 于 5 月 27 日创建，昨日（6 月 15 日）被集中更新。它们构成了一个高质量的功能/修复包，已等待评审超过 **20 天**，建议维护团队尽快安排下一批合并窗口：

*   **#2628 - CLI `--id` 修复：** 等待 20 天。解决用户输入被忽略的基础 UX 恶化问题，影响所有 CLI 用户。
    *   (https://github.com/nanocoai/nanoclaw/pull/2628)

*   **#2626 - Signal 错误显式化：** 等待 20 天。将静默空操作转为显式报错，直接提升渠道配置阶段的开发运维体验。
    *   (https://github.com/nanocoai/nanoclaw/pull/2626)

*   **#2627 - 跨平台 Reactions 对齐：** 等待 20 天。深度修复 MCP 协议层与多平台 API 的编码兼容性，是完善 Agent 交互拼图的核心修复。
    *   (https://github.com/nanocoai/nanoclaw/pull/2627)

---
*报告结束。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

```markdown
# NullClaw 项目动态日报
**日期：** 2026-06-16
**项目主页：** [github.com/nullclaw/nullclaw](https://github.com/nullclaw/nullclaw)

---

### 1. 今日速览

在过去 24 小时内，NullClaw 项目处于显著的**维护低潮期**。代码库无任何新代码合并，亦无版本发布，唯一活跃的 PR 是 Dependabot 提交的基础环境依赖更新（[#956](#)）。社区方面，两个未解决的 Issue 构成了用户关注的核心：Ollama 本地模型回答截断的严重 Bug（[#952](#)）与新用户遭遇的配置限流问题（[#957](#)）。项目维护者今日未就这些关键问题做出公开的技术回复或推送修复，项目核心功能的稳定性和社区支持响应性需提升。

### 2. 版本发布

（今日无新版本发布，本模块省略。）

### 3. 项目进展

今日无任何 Pull Request 被合并或关闭，项目核心功能没有向前推进。

- **CI/CD & 依赖更新：** `dependabot[bot]` 提出了依赖更新 PR [#956](https://github.com/nullclaw/nullclaw/pull/956)，计划将 Docker 基础镜像 Alpine 从 3.23 升级至 3.24。这是一个常规的安全维护更新，目前处于待合并状态。这反映了项目在自动化基础设施维护上的持续性，但核心代码的开发节奏明显放缓。

### 4. 社区热点

今日社区讨论主要围绕两个核心 Issue，它们揭示了用户群体的不同痛点：

1. **[#952] [bug] Local model using ollama returns incomplete answers** | [链接](https://github.com/nullclaw/nullclaw/issues/952)
   - **热度分析：** 该 Issue 已存在 5 天，昨日有新的反馈更新。这是当前社区**最稳定且严重**的关注点。
   - **诉求分析：** 用户通过 Ollama 运行 Gemma 模型时，Agent 无法提供完整回答。这直接冲击了 NullClaw 作为本地 Agent 运行时的核心价值主张。虽然 Issue 下有 1 条评论，但尚未见维护者提出明确的重现或修复方案。

2. **[#957] Rate limit issue** | [链接](https://github.com/nullclaw/nullclaw/issues/957)
   - **热度分析：** 最新创建的 Issue，反映了新用户入门的即时代价。
   - **诉求分析：** 用户在“无记忆模式”并设置 JSON 输出时，触发了内部 “config reader” 的限流机制。这暴露了当前硬编码配置与用户实际场景之间的摩擦。用户迫切需要文档说明以及可自定义的阈值配置。

### 5. Bug 与稳定性

今日聚焦 2 个活跃 Bug，按严重程度排列如下：

- **严重（High）：[#952] Ollama 本地模型返回不完整回答**
  - **影响范围：** 所有使用 Ollama 集成本地大语言模型（如 Gemma）的用户。此问题导致 Agent 对话逻辑彻底失效。
  - **当前状态：** 待确认根因。**无关联修复 PR。** 这是当前项目健康度的最大风险点。

- **中等（Medium）：[#957] Config reader 限流阻塞**
  - **影响范围：** 特定配置场景（启用 JSON 输出、无记忆模式）。
  - **当前状态：** 配置设计问题。用户遭遇了文档未覆盖的硬限制，属于配置可用性缺陷。**无关联修复 PR。**

### 6. 功能请求与路线图信号

今日虽无全新的 Feature Request Issue 提交，但从已有 Issue 中可以提炼出明确的路线图改进方向：

- **配置可观测性与灵活性（来自 #957）：** 用户明确要求将内部的 `config reader` 限流阈值（rate limit threshold）开放为可自定义的参数。这表明随着用户部署场景多样化，系统内硬编码的限制正成为采用瓶颈。下一版本应考虑将业务级限流纳入配置体系。
- **本地模型兼容性强化（来自 #952）：** 修复与 Ollama 接口的兼容性问题，确保模型输出不被截断，是维持项目“本地 AI Agent 运行时”定位的基石。这不仅是 Bug 修复，更是核心路线的紧急捍卫。

### 7. 用户反馈摘要

从今日活跃的 Issue 评论中，可以梳理出用户的真实场景与核心不满：

- **痛点：核心功能障碍**
  - *用户 bloodgroup-cplusplus*（#952）：“通过 Ollama 拉取 Gemma 模型并启动 Agent，Agent 无法用完整句子回答。” —— 这直接摧毁了该用户的使用场景。
- **痛点：配置黑箱与学习成本**
  - *用户 jacktang*（#957）：“我用 NullClaw 做无记忆的 Agent 运行时，设置了 JSON 输出，但总是遇到 rate limit 问题。这个 config 是什么？阈值怎么改？” —— 这表明文档的缺失正在消耗用户对新工具的好感度。

### 8. 待处理积压

当前项目没有跨周或月的超高龄 Issue，但存在较高的**滑入积压风险**：

- **高优先级风险项：** Issue [#952](https://github.com/nullclaw/nullclaw/issues/952) 自 2026-06-11 开启，已持续 5 天。鉴于其对核心功能的破坏性，若未来 48 小时内没有维护者介入（提供重现步骤、临时 workaround 或确认修复），该项目将面临严重的社区信任度滑坡。
- **建议权重：** 维护者应优先回复 [#952] 和 [#957]，至少提供明确的进展说明或临时的配置规避方案。同时，依赖更新 PR [#956](https://github.com/nullclaw/nullclaw/pull/956) 也应尽快合并，以维持项目基础环境的稳健性。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 IronClaw 项目动态日报。

---

# IronClaw 项目动态日报 (2026-06-16)

### 1. 今日速览
今日项目活跃度极高，过去24小时处理了46条Issue和50条PR，核心团队与社区均投入大量精力。当前项目重心集中在 **Reborn WebUI 的稳定性与用户体验修复** 上，尤其是 OAuth 授权流程中断、授权状态不一致和工具调用失败后无法恢复的严重问题。与此同时，底层依赖安全补丁（Wasmtime）、凭据作用域重构等架构级修复也在并行推进。虽然今日无新版本发布，但多项关键修复已进入待合并阶段，项目整体健康度正处于高强度迭代的“状态修复冲刺期”。

### 2. 版本发布
无。

### 3. 项目进展
今日共有 **18 个 PR 被合并或关闭**，标志着以下几个重要功能与修复的落地：

- **重大功能推进：视觉图像附件支持 (#4871) 合并：** 这是通用附件全程 (#4644) 的关键里程碑。合并后，支持视觉能力的模型（如Claude）现在能接收真正的多模态图像内容，而非单纯的文件指针。
- **基础管线打通：Trace Commons 集成 (#4929) 与例行任务路由 (#4780) 合并：** 前者解决了可观测性数据的轨迹管线问题，后者强化了例行任务（Routine）投递至外部队道的流程引导。
- **安全/CI修复：** 基准测试CI验证工具 (#4947) 合并，确保了基准测试的准确性。
- **活跃开发中的关键修复：**
    - **终结授权死循环 (PR #4944, XL)：** 针对模型授权被拒绝后无限重试的死循环问题提出修复方案。
    - **凭据作用域重构 (PR #4939, XL)：** 对应 Issue #4935，将凭据从“线程作用域”修正为“所有者（用户/项目）作用域”，根治跨对话授权丢失问题。
    - **消除 Run "Borking" 崩溃 (PR #4841, XL)：** 致力于消除因后端不可用或模型故障导致的无法恢复的终端错误。
    - **依赖安全: Wasmtime 漏洞修复 (PR #4949, #4950, M)：** 针对 RUSTSEC-2026-0182 安全漏洞进行补丁升级。

### 4. 社区热点
今日讨论最活跃的 Issues 高度集中在 **Reborn 授权流程与错误感知** 方面，反映出用户在 Agent 交互过程中的核心痛点。

- **#4764 [拒绝Shell审批后无反馈]**：评论数 2，最新更新时间 2026-06-16。用户点击“拒绝”后，界面操作卡死，没有任何恢复或提示。这是工具调用中最直接的交互障碍，社区讨论度高，亟待解决。
- **#4908 [Google Calendar 激活状态矛盾]**：评论数 3。扩展页显示“ACTIVE”，配置页仍显示“Activate”，这种状态不一致让用户极度困惑于自己是否已完成设置。
- **#4907 [Google OAuth 成功但执行失败]**：评论数 2。OAuth 认证成功后，原始任务未恢复运行，违反了用户对“标准 OAuth 流程结束后自动恢复执行”的预期。
- **#4825 ["始终允许"未跨线程持久化 (已关闭)]**：评论数 3。该 Issue 已于昨日被关闭，说明团队已经针对用户“希望一次性批准在全局生效”的诉求做出了响应并完成了修复方案。

### 5. Bug 与稳定性
今日报告的 Bug 主要围绕 Reborn 的流程断裂与状态欺骗，按严重程度排列如下：

- **[严重] 流程中断/无法恢复执行：**
    - **OAuth 执行成功但 Run 不恢复 (#4907)**：用户完成 Google OAuth 后，原 Agent 任务报错而非继续执行。(无修复 PR)
    - **拒绝授权后交互无反馈 (#4764)**：用户点击 Deny 后，工具调用永久挂起。(无修复 PR)
    - **凭据未跨对话复用 (#4913)**：用户授权后，在同一个项目的不同对话中仍需重复授权。（关联修复 PR #4939）
    - **自动化任务永久不运行 (#4917)**：创建定时任务后，状态永远停留在“SCHEDULED”，从未真正触发。(无修复 PR)
    - **MCP 工具批准后因 `stale input_ref` 失败 (#4887)**：用户在 WebUI 中批准工具后，恢复执行会话时因引用失效报错。(无修复 PR)
- **[中等] 状态显示不一致与误导：**
    - **扩展状态矛盾 (#4908)**：描述同上。
    - **LLM 提供商状态错误 (#4857, #4697)**：在未配置或 Ollama 未运行时，UI 仍显示为 ACTIVE 的用户状态。
    - **工具调用失败不刷新不显示 (#4942)**：用户需手动刷新页面才能看到工具调用失败的错误信息。
- **[低] UI/UX 引导缺失：**
    - 扩展安装后无明确下一步引导 (#4886)，安装流程分割于多个页面 (#4890)。
    - NEAR AI MCP 错误显示需要额外设置 (#4925)。
- **[安全] 底层依赖安全：**
    - **Wasmtime `fd_renumber` 内存泄漏漏洞 (RUSTSEC-2026-0182)**：此漏洞影响 `main` 分支及所有基于它的 PR 的 CI 检查。修复补丁已提交 (PR #4949, #4950)。

### 6. 功能请求与路线图信号
- **Coding Agent / 开发工作流自动化 (#4880, #4882)：** 社区贡献者提出构建云端编码代理和自动化代码审查功能，目标是让 IronClaw 能够通过 Assign Issue 或提及 Bot 自动生成 PR。这表明项目正在向 AI 驱动的全栈开发平台演进。
- **通用附件系统持续深化 (#4644)：** 作为当前最大的特性 Epic，其衍生的子任务正在稳步推进。**OpenAI 兼容接口的视觉输入支持 (#4902)** 和 **Reborn 端可下载项目文件支持 (#4933)** 均处于活跃开发状态，预计将随下一版本推出。
- **凭据模型架构变更 (#4935)：** 提出的“凭据所有者作用域化”是对早期线程级方案的修正，这是一个信号，表明开发者正在从架构层面解决授权状态的持久性问题。
- **Slack 用户级令牌工具 (#4941)：** 新贡献者为 Slack 集成增加了用户级别（User Token）的支持，可实现搜索跨频道消息等 Bot Token 无法实现的功能，丰富了 Slack 集成的潜力。

### 7. 用户反馈摘要
从今日 Issue 的评论与描述中可以提炼出用户的明确诉求：

- **对“授权-执行”链路的强依赖与不满：** 用户最大的共识是 **“授权流程必须顺滑且可预测”** 。大量 Issue 描述了在安装、激活、允许、拒绝等步骤后，系统未能按照用户预期做出响应（如 #4907, #4764, #4921）。用户不希望在一个操作步骤完成后需要手动检查是否“真的成功了”。
- **“所见即所得”的状态信任危机：** 用户对 UI 提供的信息产生了不信任感。多个报告指出组件显示“ACTIVE”但功能未就绪（#4908, #4697）。这种用户体验的割裂感严重影响了用户对新功能的尝试意愿。
- **对自动化功能的核心期待被辜负：** #4917 暴露出的“定时任务不执行”问题，对于尝鲜自动化的用户来说是一种沉痛的“信任危机”，说明功能虽然上线但缺乏基础的质量保障。

### 8. 待处理积压
- **依赖更新休眠 (PR #3705)：** 针对 `channels-src/wechat` 的依赖更新 PR 已搁置一个多月（2026-05-16），虽然风险较低，但长期未合并是维护的隐患。
- **关键 Bug 缺乏修复关联：**
    - **#4764 (拒绝 Shell 后挂起)**：此类直接阻断用户操作的 Bug 已报 5 天，严重程度高，但暂无已提交的修复 PR。
    - **#4917 (自动化不运行)**：昨日新报，属于核心功能缺失，社区暂无回应。
    - **#4913 (授权不跨对话复用)**：依赖于底层的凭据重构（PR #4939），需等待该大 PR 的合入。
- **通用附件全程 (#4644)：** 虽然进展快，但主 Issue 开了一周，Re-born WebUI 端的全链路整合还未完成，仍有大量工作积压。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-06-16

## 今日速览
- 过去 24 小时内 Issue 更新 2 条，均为已存在两月余的 **技能管理** 相关 bug，无新 Issue 提交；Issue 活跃度偏低。
- PR 活跃度较高，共 11 条更新，其中 **5 个 PR 被合并/关闭**，集中在对 **语音输入** 功能的重构与优化，以及 **文档 Artifact 分享** 新特性的合入。
- 另有 **6 个 PR 处于开放状态**，其中 4 个为 Dependabot 发起的 CI 依赖更新，1 个为长期搁置的依赖升级，1 个为功能特性（会话系统通知）。
- 无新版本发布，项目当前处于 **功能迭代与技术债务清理并行** 的阶段。

## 项目进展

今日主要合并/关闭了 5 个 PR，显著推进了语音输入模块的简化和文档预览能力的扩展：

### 🎤 语音输入重构与稳定化
- **[#2160] fix(voice-input): keep only realtime asr**  
  移除短 ASR 上传流程及相关 IPC 接口，使语音输入始终使用实时 ASR，并删除了设置中的识别模式切换开关。这是一个 **破坏性变更**，旧版配置项 `voiceInput.recognitionMode` 不再生效。  
  [netease-youdao/LobsterAI PR #2160](https://github.com/netease-youdao/LobsterAI/pull/2160)

- **[#2162] fix(cowork): preserve voice input cancel guard after merge**  
  解决合并冲突时保留取消守卫、草稿所有权、会话切换取消等逻辑，提升稳定性。  
  [netease-youdao/LobsterAI PR #2162](https://github.com/netease-youdao/LobsterAI/pull/2162)

- **[#2163] feat(voice-input): refine dictation recording UI**  
  优化听写录音界面，新增内存级 ASR 配额切片与共享常量，改善每日可用性提示与配额状态重置。  
  [netease-youdao/LobsterAI PR #2163](https://github.com/netease-youdao/LobsterAI/pull/2163)

### 📄 文档 Artifact 分享与预览
- **[#2159] feat(artifacts): 支持文档 Artifact 分享与预览优化**  
  新增 DOCX/PPTX/XLSX/PDF/CSV/TSV 等文档类型的分享来源，完善类型校验、大小限制、分页渲染及原生预览兜底，并补齐 pdfjs 字体与 cMap 资源，调整 CSP 以支持 Blob 预览。  
  [netease-youdao/LobsterAI PR #2159](https://github.com/netease-youdao/LobsterAI/pull/2159)

### 🧹 其他
- **[#2161] chore: update about**  
  更新“关于”页面内容。  
  [netease-youdao/LobsterAI PR #2161](https://github.com/netease-youdao/LobsterAI/pull/2161)

> 项目整体在 **语音交互体验** 和 **文档协同能力** 两个方向上迈出了实质性的一步，同时主动清理技术债务（去除短 ASR 冗余逻辑），代码库更加精简。

## 社区热点

今日讨论相对分散，评论最多的条目为 **[#1426]** 和 **[#1427]**，各有 1 条评论，均来自技能上传相关的同类缺陷：

- **[#1426] [OPEN] 通过上传本地添加技能后无成功提示，技能列表未刷新**  
  用户期望上传后有明确反馈，列表能自动刷新。  
  [Issue #1426](https://github.com/netease-youdao/LobsterAI/issues/1426)

- **[#1427] [OPEN] 通过本地添加，能重复添加技能，导致多个同名技能**  
  缺少去重校验，允许重复上传同一技能。  
  [Issue #1427](https://github.com/netease-youdao/LobsterAI/issues/1427)

**诉求分析**：这两条 Issue 反映了 **技能管理基础交互的缺失**——既无操作成功/失败的状态反馈，也未对同名校验进行限制。用户对日常使用的“确定性”有较高要求，此类细节虽小却直接影响信任感。

> 值得注意的是，这两条 Issue 创建于 4 月初，昨日（6-15）被标记或更新为 `stale`，但未关闭，说明维护者仍未忽视，但修复尚未排入日程。

## Bug 与稳定性

| 严重程度 | Issue / Bug 描述 | 状态 | 是否有关联 Fix PR |
|----------|------------------|------|------------------|
| 中 | **[#1426]** 添加上传技能后无成功提示、列表未刷新 | Open / stale | 无 |
| 中 | **[#1427]** 可重复添加同名技能，缺少去重 | Open / stale | 无 |

未见崩溃、数据丢失等 P0/P1 级别 Bug。语音输入重构（#2160）虽为破坏性变更，但已通过测试（`npm run test:ui`），且附带更新了单测，未报告新的回归。

## 功能请求与路线图信号

- **[#2159] 文档 Artifact 分享** 已合并，将成为 2026.6.11 版本后的新能力，预期提升办公文档协作体验。
- **[#2160] 语音输入实时化** 移除了短 ASR 模式，意味着产品方向更聚焦实时语音场景，**用户若依赖旧版非实时上传需关注升级影响**。
- **[#1428] feat(cowork): 会话完成/报错推送系统通知** 仍为 Open / stale，但该特性可显著改善后台会话的感知，与 #2160、#2163 等语音优化形成互补，建议维护者评估其纳入下一版本的可能。  
  [PR #1428](https://github.com/netease-youdao/LobsterAI/pull/1428)

## 用户反馈摘要

基于 Issue 摘要及评论（截至今日可获取的数据），提炼出以下真实用户场景痛点：

1. **操作无反馈**：上传技能后界面无任何成功/失败提示，用户不确定是否生效。
2. **数据一致性问题**：重复上传同一技能可创建多个同名条目，缺乏前端或后端去重校验，可能污染技能列表。
3. **后台会话感知不足**（由 #1428 推断）：用户希望当主窗口未聚焦时，自动接收到会话完成或报错的通知，避免频繁切换窗口检查状态。

## 待处理积压

以下为长期未响应或未合并的重要条目，建议维护团队优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 最近更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue | [#1426](https://github.com/netease-youdao/LobsterAI/issues/1426) | 技能上传无提示/列表不刷新 | 2026-04-03 | 2026-06-15 | 已被标记 stale，无 fix PR |
| Issue | [#1427](https://github.com/netease-youdao/LobsterAI/issues/1427) | 可重复添加同名技能 | 2026-04-03 | 2026-06-15 | 同上，两问题相近，可考虑统一修复 |
| PR | [#1428](https://github.com/netease-youdao/LobsterAI/pull/1428) | feat: 会话完成/报错推送通知 | 2026-04-03 | 2026-06-15 | 与近期语音/体验优化方向契合，需决策是否合入 |
| PR | [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | chore(deps-dev): bump electron group | 2026-04-02 | 2026-06-15 | 依赖升级（Electron 40→42），长期搁置，可能影响安全/稳定性 |
| PR | [#2164–2167](https://github.com/netease-youdao/LobsterAI/pulls?q=is%3Apr+is%3Aopen+created%3A2026-06-15) | 多个 CI 依赖更新 | 2026-06-15 | 2026-06-15 | 虽新提交，但应尽早 review，避免重蹈 #1277 积压覆辙 |

> **建议**：针对技能上传的 #1426 / #1427，可考虑在下次迭代中安排一个小型 UI 改进（提示条 + 按钮 loading + 名称去重），以较低成本解决两个积压痛点。

---

*生成时间：2026-06-16 · 数据截止 2026-06-15 24:00 UTC*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-06-16

## 今日速览

过去 24 小时内项目主要围绕两项新功能推进，共计提交 2 个 Pull Request，均为开放状态，无 Issues 更新或新版本发布。整体活跃度中等偏低，开发集中于 **外部代理的模型与 effort 选择** 以及 **聊天回合上下文命令** 两大方向，表明项目正在积极增强多模型集成和会话自动化能力。这两项变更尚未合并，需等待代码审查与后续测试。

---

## 项目进展

### 新提交 PR（未合并）

1. **Support model and effort selection for external agents**（[#1125](https://github.com/moltis-org/moltis/pull/1125)）  
   - 为外部代理提供商增加了 `models = [...]` 和 `efforts = [...]` 配置，并在 `/model` 命令中添加 `external-agent/<kind>` 分组展示。  
   - 使开发者能够在不同外部代理间灵活切换模型与算力级别，扩展了 Moltis 作为多代理聚合器的能力。

2. **Add context command support for chat turns**（[#1124](https://github.com/moltis-org/moltis/pull/1124)）  
   - 引入可选的 `chat.context_command` 配置项，在每次聊天回合前执行并追加 stdout 到 prompt 上下文中。  
   - 有助于部署场景自动注入运行时上下文，减少手动粘贴，提升交互连续性。

两个 PR 分别触及 **模型管理** 与 **会话上下文** 两个关键模块，项目在上述方向迈出了实质性的一步，但当前进度仍处于提案阶段，尚未合并到主分支。

---

## 社区热点

> 今日无 Issues 创建/更新，所有讨论集中在提交的 PR 上。

- [#1125 Support model and effort selection for external agents](https://github.com/moltis-org/moltis/pull/1125)  
- [#1124 Add context command support for chat turns](https://github.com/moltis-org/moltis/pull/1124)

两项 PR 的作者均为 `gptme-thomas`，目前无评论或点赞，但作为唯一的活动条目，代表了社区最近关注的两个方向：  
- 通过标准化接口对接多种外部代理（如 OpenAI、Anthropic 等）并在同一界面切换模型；  
- 自动为每次对话注入预生成的上下文，提升复杂工作流中的可用性。

背后的诉求指向 **更灵活的模型编排** 与 **更少的手动状态维护**，这与当前 AI 智能体平台追求多模型支持、自动化 prompt 管理的趋势一致。

---

## Bug 与稳定性

**无**。过去 24 小时内未报告新的 Bug、崩溃或回归问题，也没有相关修复 PR。

---

## 功能请求与路线图信号

- **多外部代理模型/effort 选择**（[#1125](https://github.com/moltis-org/moltis/pull/1125)）：该功能如果合并，将使 Moltis 成为更通用的智能体中间层，兼容不同提供商的模型与定价等级，符合“模型路由”的路线图信号。  
- **聊天回合自动上下文命令**（[#1124](https://github.com/moltis-org/moltis/pull/1124)）：提供了一种轻量级脚本注入能力，可被用于动态注入系统指令、工具输出或用户信息。若合入，有望在未来版本中发展成更完善的“会话前置钩子”机制。

两项功能均属于基础设施增强，未涉及破坏性变更，可能纳入下一 minor 版本（如 `v0.x`）。

---

## 用户反馈摘要

**无直接用户反馈。** 但从 PR 摘要推断，以下场景可能被用户期待：  
- 开发者在同一项目中使用多个外部代理（如 GPT-4 与 Claude 3），希望无缝切换模型和 effort 等级；  
- 部署者需要自动在每轮对话前插入环境变量、文件内容或工具调用结果，减少粘贴操作。

---

## 待处理积压

| 项目 | 描述 | 状态 | 提醒 |
|------|------|------|------|
| [#1125](https://github.com/moltis-org/moltis/pull/1125) | 外部代理模型与 effort 选择 | 开放 1 天，无评论 | 建议尽快安排审查，避免与后续 PR 冲突 |
| [#1124](https://github.com/moltis-org/moltis/pull/1124) | 聊天回合上下文命令 | 开放 1 天，无评论 | 功能涉及配置和行为变更，需明确默认值及安全性 |

两个 PR 均为刚提交的新增功能，尚未得到维护者的响应。建议尽快触发 CI、邀请 reviewers，以避免较长的不活跃期。

---

*数据来源：GitHub (moltis-org/moltis)，更新时间 2026-06-16 00:00 UTC。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

```
好的，以下是为您生成的 CoPaw (QwenPaw) 项目动态日报（2026-06-16）。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-06-16

## 1. 今日速览

项目在过去24小时内持续保持着**极高的活跃度**。社区提交与开发修复并行，共产生50条Issue和50条PR更新，净新增/活跃33条Issue。Bug修复与功能开发“双线冲刺”：一方面严重崩溃（macOS Tauri、Windows内存泄漏）与高频Bug（附件下载、上下文清空）频繁上报；另一方面，社区呼声极高的**上下文/Token用量可视化功能正式落地合并**，多项基础体验（模型设置页、技能市场UI）也迎来重构。项目健康度呈现 **“高活跃、高关注、高修复压力”** 的态势。

## 2. 版本发布

*过去24小时内无新版本发布。项目当前最新稳定版本为 v1.1.11.post2。*

## 3. 项目进展

多个人期待已久的功能PR在今日取得重大进展或正式合并：

- **Token及上下文可视化功能正式上线：** PR [#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310) 与 [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) 相继合并。后端记录每轮上下文用量，前端在聊天头部和回复卡片中提供直观指示器。标志着 #4284、#3366、#4647、#4782 等多个被反复提及的长期需求正式落地。
- **Agent外部能力统一抽象层构建：** PR [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) 合并。该PR引入的“Agent OS Driver”为后续无缝集成 MCP、A2A、ACP 等异构协议奠定了坚实基础。
- **技能显示交互优化：** PR [#5146](https://github.com/agentscope-ai/QwenPaw/pull/5146) 合并，修复了在控制台通过斜杠命令调用技能时，错误展示完整 `SKILL.md` 内容的问题，正式关闭 [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031)。
- **插件市场 UI 迭代：** PR [#5123](https://github.com/agentscope-ai/QwenPaw/pull/5123) 合并，为技能市场新增分类、预览功能，提升了插件发现和安装体验。
- **桌面端启动性能优化推进：** PR [#5153](https://github.com/agentscope-ai/QwenPaw/pull/5153)（开放中）致力于将 Tauri 客户端的“瞬时窗口（Instant-Window）”启动优化移植到 pywebview 客户端。
- **模型管理页面大重构提案：** PR [#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203) 提交，采用玻璃态卡片设计和供应商聚合分组，集成阿里云国际站Token方案，暗示模型配置UI即将换代。

## 4. 社区热点

- **#1911 “小艺”频道适配疑难帖 (22条评论)**
  [https://github.com/agentscope-ai/QwenPaw/issues/1911](https://github.com/agentscope-ai/QwenPaw/issues/1911)
  用户深入测试了小艺频道，发现手机端小艺返回“开小差”错误，且无法在CoPaw端找到手机侧的对话记录。该Issue因涉及华为生态的联调难题，连续多日成为社区讨论焦点。

- **#5140 / #5199 附件下载功能反复“失灵” (6条 / 2条评论)**
  [https://github.com/agentscope-ai/QwenPaw/issues/5140](https://github.com/agentscope-ai/QwenPaw/issues/5140)
  [https://github.com/agentscope-ai/QwenPaw/issues/5199](https://github.com/agentscope-ai/QwenPaw/issues/5199)
  从v1.1.11起持续跨版本存在的回归问题。用户反馈纯文本（TXT/MD/PY）下载有时正常，但docx/pdf等二进制文件报404，偶尔全部正常。频繁的反复已让该问题成为影响日常生产力的头号痛点。

- **#5167 关于飞书CardKit流式卡片长回复性能的专业反馈 (4条评论)**
  [https://github.com/agentscope-ai/QwenPaw/issues/5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)
  用户给出了非常深入的技术分析，指出当前逐字推送机制在面对飞书卡片刷新API时的性能瓶颈，引发了关于SSE与消息整合策略的高质量技术讨论。

## 5. Bug 与稳定性

### 🔴 严重崩溃与数据丢失
- **macOS Tauri 端崩溃循环 (SIGSEGV)** [#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209)：QwenPaw Desktop 在 Apple Silicon (ARM64) 上进程平均1分钟崩溃一次并反复重启，无法正常使用。**暂无Fix PR。**
- **Windows 客户端进程/内存泄漏** [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138)：进程数持续增加，内存占用超过90%，严重拖慢系统。**暂无Fix PR。**
- **插件依赖安装导致 cmd 窗口疯狂弹窗** [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)：当 PyPI 连接不稳定时，pip 安装失败陷入无限重试并弹出大量黑窗口，用户体验灾难。**暂无Fix PR。**
- **上下文压缩导致 Agent 完全失忆** [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)：当单条人设文件 Token 大于压缩保留阈值时，压缩逻辑将上下文压缩至0条，导致对话任务完全中断。

### 🟡 高影响功能回归与受限
- **Minimax 模型 XML 输出不兼容** [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)：遗留超过三周，严重影响使用 M2.5 模型用户的指令与技能执行。
- **本地模型提供者在 v1.1.11.post2 中消失** [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184)：v1.1.11 新增的本地提供商功能在 post2 中无法正常显示，属于严重回归。
- **工作区工具路径解析不一致** [#5207](https://github.com/agentscope-ai/QwenPaw/issues/5207)：`read_file` 与 `execute_shell_command` 对同一路径字符串解析结果不同，导致自动化任务不可靠。

### 🟢 中低影响
- 企业微信私聊审批入口不可见 [#5190](https://github.com/agentscope-ai/QwenPaw/issues/5190)
- 上下文压缩统计值与实际输入偏差 [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122)

## 6. 功能请求与路线图信号

- **上下文极致优化诉求强烈：** 用户提议集成第三方压缩层 Headroom（[#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)），声称可减少60-95% Token消耗。结合 [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) 对技能/MCP元数据膨胀的质疑，表明社区已开始探索超越当前内置压缩器的方案。
- **Agent 自主性呼声初显：** [#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205) 提出了“Agent自我进化”概念，要求Agent从静态规则执行转向基于错误的动态行为修正，代表了核心用户对智能体的长期期待。
- **交互体验持续迭代：** [#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158)（输入队列）和 [#5211](https://github.com/agentscope-ai/QwenPaw/issues/5211)（桌面UI布局优化）的提交，直接反映了社区对工作流顺畅度和界面效率的具体要求。PR [#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158) 有望成为下一版本的核心交互改进。

## 7. 用户反馈摘要

- **赞赏：** Token统计功能的多PR合并赢得了用户的广泛肯定，用户评论称“终于能主动管理上下文了”。
- **疲惫：** 对于“附件下载”等Bug跨多个小版本反复出现，用户明显表现出疲劳和不满情绪（“之前的版本修复了，现在又不正常了”）。Post2引入的回归Bug加深了用户对发布质量的疑虑。
- **抱怨：** macOS用户对桌面端崩溃感到强烈不满；插件弹窗问题被冠以“灾难级体验”。
- **期望：** 用户期望向 OpenClaw 看齐，补齐对话队列和时间戳功能。这一需求已直接驱动了相关PR的提交。

## 8. 待处理积压

以下为长期未响应或亟需维护者关注的重要 Issue 与 PR：

- **#4625 Minimax 模型严重不兼容（5月22日至今）**：[https://github.com/agentscope-ai/QwenPaw/issues/4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)
  *严重度极高的功能Bug，持续20余天未给出修复时间表，用户已从“求修复”转为高频质疑。*
- **#4900 插件加载器解耦（6月2日至今）**：[https://github.com/agentscope-ai/QwenPaw/pull/4900](https://github.com/agentscope-ai/QwenPaw/pull/4900)
  *修复了桌面端（PyInstaller/Tauri）环境下插件系统静默超时不生效的严重问题，长期处于Open状态，影响所有打包版用户。*
- **#5041 备份跳过不可读文件（6月9日更新）**：[https://github.com/agentscope-ai/QwenPaw/pull/5041](https://github.com/agentscope-ai/QwenPaw/pull/5041)
  *提升备份鲁棒性的社区贡献，处于Under Review状态，若能合并将显著降低用户数据备份失败的风险。*
```

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是为您生成的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 (2026-06-16)

## 1. 今日速览
零一爪 (ZeroClaw) 项目在 2026-06-16 保持了极高的迭代热度，24 小时内共发生 **50 条 Issue 更新** 与 **50 条 PR 更新**。虽然当日无新版本发布，但项目活跃度处于峰值状态。开发重心显著转向 **运行稳定性修复**（MCP 配置静默失效、锁竞争崩溃）与 **安全架构加固**（CI 供应链安全、委托授权、WASM 栈演进）。社区对多智能体路由 (Multi-Agent Routing) 的深度讨论与多份架构级 RFC 的涌现，预示着项目正为 v0.8.1/v0.9.0 里程碑进行密集的技术冲刺。

## 2. 版本发布
无

## 3. 项目进展
- **Issue 关单推动项目成熟度**：
  - [#1458](https://github.com/zeroclaw-labs/zeroclaw/issues/1458) **[CLOSED]**: 新增本地 CA 证书支持，解决了企业级用户使用自签名推理端点时的连接阻塞。
  - [#6683](https://github.com/zeroclaw-labs/zeroclaw/issues/6683) **[CLOSED]**: 修复 `skill_manage` 补丁无视冷却时间的严重 Bug，规避了潜在的无限资源消耗。
  - [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) **[CLOSED]**: 修复 Web 仪表盘中 `ask_user` 功能阻断，恢复了关键的人机交互工作流。
- **核心功能 PR 在途**：
  - **Web 体验**： [#7223](https://github.com/zeroclaw-labs/zeroclaw/pull/7223) 为网页聊天引入斜杠命令 (`/clear`, `/model` 等)。
  - **通道功能对齐**： [#7535](https://github.com/zeroclaw-labs/zeroclaw/pull/7535) (WhatsApp 表情回复) 和 [#7671](https://github.com/zeroclaw-labs/zeroclaw/pull/7671) (Telegram `/clear` 命令) 处于审查中。
  - **稳定性提升**： [#7755](https://github.com/zeroclaw-labs/zeroclaw/pull/7755) 修复了运行时毒化锁导致的进程崩溃；[#7727](https://github.com/zeroclaw-labs/zeroclaw/pull/7727) 与 [#7485](https://github.com/zeroclaw-labs/zeroclaw/pull/7485) 则显著增强了 `zeroclaw doctor` 的诊断能力与自定义 Provider 验证。

## 4. 社区热点
- **呼声最高的功能：多智能体路由 (Multi-Agent Routing)**：
  Issue [#2767](https://github.com/zeroclaw-labs/zeroclaw/issues/2767) 以 **9 个 👍 和 6 条评论** 成为过去 24 小时互动度最高的议题。用户详细讨论了在单一 Gateway 内部署互相隔离的智能体与账户的架构设计。与之紧密关联的 RFC [#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)（讨论 A2A 发现协议）也获得不少关注，社区正在深入探讨 ZeroClaw 作为多智能体宿主机的系统边界。
- **架构级 RFC 引领技术风向**：
  高级用户 `ConYel` 连续提交三份重量级 RFC，引发社区对技术债务的反思。
  - [#7673](https://github.com/zeroclaw-labs/zeroclaw/issues/7673): 原生上下文压缩，旨在降低每一次 LLM 调用的 Token 消耗。
  - [#7675](https://github.com/zeroclaw-labs/zeroclaw/issues/7675): 硬化 CI 管道，引入供应链扫描与 SBOM 生成。
  - [#7674](https://github.com/zeroclaw-labs/zeroclaw/issues/7674): 极具雄心的“纯 Rust / WASM First”计划，建议彻底斩断对 Node.js 的构建与运行时依赖。

## 5. Bug 与稳定性
- **P1 (严重)**:
  - **#7733 [MCP 隔离静默失效]**：`mcp_bundles` 安全隔离字段在配置后解析正常，但运行时完全未生效，构成严重的安全隔离漏洞。当前**无 PR 关联**，亟待维护者响应。
  - **#7542 [已修复]**：WebSocket 下 `ask_user` 阻断 Bug 已关闭。
- **P2 (高危)**:
  - **#7756 [工具注册后未发送]**：针对 `responses API` 和 Anthropic 模型，工具注册后模型端收到空列表，导致回复“无可用工具”。
  - **#7757 [Web 面板技能列表缺失]**：UI 仅显示 `skill_bundles`，遗漏了 `workspace` 和 `open-skills` 技能。
  - **#7753 [会话持久化竞态]**：并发消息处理导致历史顺序出错，可能引发数据丢失。
  - **#7741 [多模态缓存问题]**：响应缓存未能跳过图片标识符，缓存命中逻辑存在缺陷。
  - **#7739 [Email OAuth 缺乏重试]**：Email 通道的 OAuth 刷新缺少背退与重试机制，防脆弱性不足。
- **稳定性修复管线**：
  当前 **49 个 OPEN PR** 多数为修复性补丁。核心修复包括锁崩溃 (`#7755`)、全局凭据 fallback 危胁 (`#7640`)、Windows 更新 (`#7530`)、Lark 表情配置 (`#7495`)、以及自检认证 (`#7732`)。

## 6. 功能请求与路线图信号
- **确定为下一阶段重点 (v0.8.1 / v0.9.0)**:
  - 多智能体路由 ([#2767](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)) 与 A2A 发现 ([#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)) 无疑是当前路线图的最强信号。
  - 安全重构追踪器 ([#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)) 与显式智能体委托 ([#7743](https://github.com/zeroclaw-labs/zeroclaw/issues/7743)) 表明 v0.9.0 将对权限与安全模型进行较大变更。
- **用户期望的配置优化 (短期高频需求)**:
  - 别名重命名 ([#7468](https://github.com/zeroclaw-labs/zeroclaw/issues/7468))、字符串内编辑增强 ([#7467](https://github.com/zeroclaw-labs/zeroclaw/issues/7467))、Channel 意图预检模型可配置化 ([#6067](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)) 等用户呼声极高，反映了社区对基础配置灵活性的迫切需求。

## 7. 用户反馈摘要
- **信任危机**：用户 `metalmon` 遭遇配置隔离不生效 (`#7733`)，用户 `perlowja` 遭遇工具注册无效 (`#7756`)。这类“静默失效”严重动摇了用户对系统的信任，是当前最需要被关注的负面体验。
- **企业级部署痛点**：用户 `BlueskyFR` 持续数月的对自签名证书支持的诉求（`#551`）已通过 `#1458` 获得解决方案。此外，Email 通道防脆弱性缺失是另一个突出的企业级部署槽点 (`#7739`)。
- **开发体验反馈**：用户 `damajor` 抱怨 TUI 中编辑字符串时无法使用方向键导航 (`#7467`)，体现了当前终端交互细节仍有较大打磨空间。
- **正向贡献关系**：社区对贡献者 `Audacity88`（项目追踪/审计）和 `ConYel`（架构 RFC）给予了高度评价，社区自组织与自驱力非常健康。

## 8. 待处理积压
- **[高风险 / 积压] 代码恢复审计 [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)**：追踪 3 月底批量 Revert 丢失的 153 个提交。该问题已悬置近 2 个月，如不尽快通过 Cherry-pick 或审查恢复，将导致大量已合并功能与修复的重复劳动，并增加后续合并冲突的风险。
- **[阻塞风险] WebSocket 认证问题 [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038)**：该 Issue 因“需作者提供更多信息”而被搁置。鉴于其影响首批用户体验（新手引导直接失败），维护者不应被动等待，建议主动协助用户 `dgreffrath` 重现问题。
- **[失活风险] 待作者响应 PR 列表**：以下 PR 均被打上了 `needs-author-action` 标签，处于“濒死”状态，维护者需联系作者或重新分配给其他贡献者：
  - [#7094](https://github.com/zeroclaw-labs/zeroclaw/pull/7094) (CLI 设置模型)
  - [#7340](https://github.com/zeroclaw-labs/zeroclaw/pull/7340) (URL 验证解耦)
  - [#7098](https://github.com/zeroclaw-labs/zeroclaw/pull/7098) (Mattermost WebSocket)
  - [#7215](https://github.com/zeroclaw-labs/zeroclaw/pull/7215) (Quickstart Port 字段)
  - [#7532](https://github.com/zeroclaw-labs/zeroclaw/pull/7532) (配置序列化丢失)
- **[持续债务] 国际化滞后 [#6698](https://github.com/zeroclaw-labs/zeroclaw/issues/6698)**：Fluent 本地化文件持续落后英文源文件（尤其是 `zh-CN` 地区）。随着项目受众全球化扩展，此技术债务日积月累，或将成为用户采纳的隐形障碍。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*