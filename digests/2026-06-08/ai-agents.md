# OpenClaw 生态日报 2026-06-08

> Issues: 294 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-08 03:40 UTC

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

***

# OpenClaw 项目动态日报 — 2026-06-08

***

## 1. 今日速览

过去 24 小时，OpenClaw 项目保持了较高的社区活跃度，共产生 294 条 Issue 更新与 500 条 PR 更新，这主要受益于大规模 Bug 扫荡和社区功能的集中提交。不过，今日无新版本发布。在 PR 侧，有 167 个请求被合并或关闭，占过去 24 小时活动 PR 总量的约 33%，整体项目健康度良好，但一些核心功能（如会话状态、安全边界）相关的修复仍在等待深度评审和产品决策。值得注意的是，关于文本泄漏、认证安全性以及会话状态丢失的高优回归 Bug 仍然占据社区讨论的中心位置。

***

## 2. 版本发布

*记录：数据源中无新版本发布信息，本节跳过。*

***

## 3. 项目进展

过去 24 小时，社区持续将主要精力投入在高频问题的修复与重要功能的打磨上，虽然大部分 PR 未被直接合并，但大量“等待作者处理”或“等待维护者审查”的请求已经进入了最终验收阶段，以下是推进到关键阶段的 PR：

*   **`#90328` – 模型选择器代理运行时暴露**：为 WebUI 模型选择器添加了 `agentRuntime` 元数据展示。当模型有指定的代理运行时（如通过 OpenAI Codex 运行 GPT-5.5）时，现在会显示非默认的运行时标签。这将改善复杂配置场景下用户对模型配置的感知，避免服务调用链路的不透明性。 *(标签: `status: 👀 ready for maintainer look`)*
*   **`#90937` – 保留关闭通道的诊断信息**：修复了 Telegram 这类轮询通道在恢复停止超时后可能错误地将连接标记为 `connected=true` 的问题。此修复确保了网关在通道任务被终止后仍保留生命周期状态的所有权，从而维护了诊断信息的准确性，防止运维人员的误判。 *(标签: `status: 👀 ready for maintainer look`)*
*   **`#87504` – 对齐 Skill Workshop 钩子超时**：修复了 `agent_end` 钩子在自动捕获（Skill Research）期间延长会话关闭的问题。通过将对钩子超时的等待与审查者的最大超时时间对齐，确保了例行的会话关闭不会被“技能研究”这类辅助任务意外阻塞。
*   **`#89319` – Doctor 命令检测不被支持的钩子加载器形状**：增强了 `openclaw doctor` 命令的诊断能力。当用户配置 `hooks.internal.entries` 中含有不被当前钩子加载器消费的键（如 `handler`、`module`）时，Doctor 会发出明确警告，帮助用户在运行时提前发现无效配置。
*   **`#90089` – 使用配置解析的工作区修复沙盒同步**：修复了当没有提供显式 `workspaceDir` 时，沙盒技能同步功能会错误地读取硬编码环境变量的问题，现在会沿着用户的完整配置链正确解析工作区路径，增强了 Docker 和复杂多用户环境下的沙盒可靠性。

*总结：项目正在积极推进大量兼容性、安全性和会话边界相关的代码审核，趋势上，有多个 XL 级别的功能 PR 正进入状态，预示着未来可能有较大体量的新特性合并。*

***

## 4. 社区热点

以下 Issue / PR 在过去 24 小时内聚集了最多的社区讨论：

*   **`#25592` – 工具调用之间的文本泄漏到消息频道**（评论数：27，反应: 1 👍）
    *   *诉求分析*：这是项目内一个长期高优（Diamond Lobster 级别）的 UX 和安全问题。当 Agent 在调用工具之间产生文本（如错误处理日志、处理确认）时，这些内部处理输出被错误地路由到最终的消息通道（如 Slack、iMessage）显示为正式消息。用户强烈要求将执行轨迹与面向用户的消息进行严格剥离，这对任何生产级 AI Bot 的可用性都至关重要。

*   **`#88838` – 跟踪核心会话/记录 (Transcript) 的 SQLite 迁移**（评论数：18，反应: 1 👍）
    *   *诉求分析*：该项目试图通过“抽象分支（Branch by Abstraction）”模式，将核心运行时状态（会话/记录）迁移至 SQLite。社区围绕如何将大型重写拆分为小而可审核的 PR 进行了深度讨论。这代表项目团队正在进行显著的基础设施重构，以规避一次性大变更带来的高风险。

*   **`#88312` – 代码应用服务器回合完成停顿回归**（评论数：14，反应: 3 👍）
    *   *诉求分析*：用户 `yair` 报告了一个 P1 级别的回归，即 2026.5.27 版本的更新导致 Codex 应用服务器在多工具 Agent 回合中可靠地失败了（“Codex stopped before confirming the turn was complete”）。这引起了社区极大的关注，因为该问题影响了 ChatGPT Plus 订阅用户，且早前已被修复过一次（#84076 / #85107）。此问题严重打击了用户对稳定性的信心。

*   **`#91283` – minSecurity 安全排序逻辑反转**（今天最新 Issue）
    *   *诉求分析*：用户 `korewaChino` 报告了 `exec-approvals.js` 中 `minSecurity` 函数有一个反向的排序逻辑，它错误地将 `full` 评为了最严格模式（应当是最宽松模式），从而导致了安全配置“反转”效果。这是一个关键的安全性 Bug，因为它会导致预期采取“全量审批”模式的会话被错误降级到“名单制审批”。

*   **`#91212` – 网关重启后投递恢复机制的竞态问题**（今天最新 Issue）
    *   *诉求分析*：报告了一个严重的数据损失问题。网关重启后，`delivery-recovery` 机制在通道传输层尚未就绪前就尝试恢复消息投递（特别是飞书 WebSocket 未连接前），导致系统报告“0 recovered, N failed”并永久丢失消息。这是高可用架构中典型的并发问题。

***

## 5. Bug 与稳定性

按严重程度排列，当前社区反馈的最需关注的 Bug：

*   **Critical: 逻辑反转/安全配置 (minSecurity - #91283)**
    *   *描述*: 安全审批函数 `minSecurity` 排序逻辑反向，导致配置了高安全等级的用户被系统降级使用低安全模式。
    *   *状态*: **无修复 PR**；需立即进行安全补丁。

*   **Critical: 数据丢失/回合卡住 (Turn-Completion Stall - #88312)**
    *   *描述*: Codex 服务端在 5.27 版本回归，多轮工具调用后会话停顿并报错。这是一个影响主线交互的严重回归。
    *   *状态*: **无新修复 PR**；虽然早前有修复，但现在出现了回归，社区积极性受挫。

*   **Critical: 数据丢失/消息丢失 (Delivery Recovery Precondition - #91212)**
    *   *描述*: GATEWAY 重启后，在 WebSocket 就绪前盲目执行消息恢复，导致消息永久丢失。
    *   *状态*: **无修复 PR**；但已有清晰的 Bug 分析和竞态条件定位。

*   **High: 数据丢失/写入覆写 (Write Tool Append Mode - #40001)**
    *   *描述*: Write 工具仅支持完全覆写，不存在追加模式，导致多个 Cron 会话共享同一文件时发生数据丢失（例如日报/记忆文件被完全覆盖）。
    *   *状态*: 超过 3 个月的陈旧 Issue，**无新修复 PR**，已是长期积压。

*   **High: 会话 Terminate (WebSocket Reconnect - #38091)**
    *   *描述*: Web UI 的 WebSocket 在触发重连后，意外导致正在进行的 AI 会话被终止（terminated）。严重影响 Web 端会话体验。
    *   *状态*: 超过 3 个月的陈旧 Issue，**无新修复 PR**。

*   **High: 会话/崩溃 (Gateway 需要手动重启 - #74822)**
    *   *描述*: Telegram 通道出现 'Something went wrong' 错误后，会话无法自愈，必须手动 `openclaw gateway restart` 才能恢复。属于典型的无值守运维噩梦。
    *   *状态*: 尽管该 Issue 已 `CLOSED`，但存在短期复发的可能，需关注是否有完全测试覆盖的持久修复。

***

## 6. 功能请求与路线图信号

从过去 24 小时的议题与讨论中，可以识别出以下未来路线图的强力信号：

*   **性能与成本**：
    *   **轻量级 Slug 生成器 (`#33962`)**: **基础功能**：用户提议 slug 生成不应总使用“主模型”，应使用轻量模型。这反映了社区对降低 API 调用成本和减少请求队列拥塞的强烈需求（3个 👍）。
    *   **百分比预设分页/压缩 (`#87136`)**: **核心优化**：随着模型上下文窗口从 200K 到 1M 的变化，社区强烈要求所有压缩阈值从绝对 Token 数切换为相对百分比。

*   **开发与平台扩展**：
    *   **无 AI 的轻量网关模式 (`#86881`)**: 社区建议推出可选的、不含 AI Harness 的轻量级 “Gateway-Lite” 版本，专门用于部署通道网关、Webhook、定时任务和无状态插件。这表明了对于确定性、稳定地部署非 AI 依赖工作流的需求。
    *   **主题会话家族 (`#90916`)**: **高级功能**：提出为单一助手支持多重命名通道（Topic Lanes），以在不同的上下文隔离任务中进行切换，同时共享持久记忆。这是下一代 AI 工作台（Workspace）概念的明显蓝图信号。

*   **即用型 UX**：
    *   **补丁 & 有界 Append (`#90354`)**: **高兼容性信号**：请求在预压缩的记忆写入阶段提供硬性限制、写入后验证和静默失败处理。这反映了用户希望对 Agent 的“记忆自主权”有更强的约束，以防自我伤害。

***

## 7. 用户反馈摘要

*   **更精细的会话控制（`#25592` - 文本泄漏；`#38966` - TUI 刷新）**：
    用户 `doomclaw` 和 `yizhanzjz` 对现有 Agent 的控制粒度表达了不满。核心痛点是“我无法判断什么是 Agent 在对自己说话（内部推理/日志），什么是对我说话（终态输出）”。尤其是在多客户端（TUI + Slack）情景下，会话在某个客户端被重置，其它客户端毫无感知，这表明用户希望有一个基于状态、事件驱动的统一交互同步层。

*   **高回归容忍度的反感（`#88312`；`#68113`）**：
    多位用户对 P1 级别的频繁回归感到失望（`yair`：“same turns fails in 5.27 but fine in 5.26”；`infoanton`：“all commands return 503 in v2026.4.15”）。用户反馈表明，从开发者侧看，该阶段的版本发布似乎未能确保关键的端到端回归测试完全覆盖（特别是 Mattermost 和 Codex 通道），导致主干稳定性的信任度下降。

*   **静态 vs 动态配置的矛盾（`#91283` - minSecurity 反转；`#65201` - 静态 Doctor 警告）**：
    反馈显示，项目在向高度可配置演进时，默认值与配置合并逻辑之间的“语义反转”（如 `full` 被定义为最严格而不是最宽松）或者静态 scanner (Doctor) 无法识别 `SecretRef` 这种动态注入方式，对用户产生了明显的困扰。这表明配置定义文档与运行时实际逻辑之间需要更严谨的对齐。

*   **隐身数据丢失（`#40001` - 文件覆写；`#74586` - 搜索超时）**：
    用户 `altsoulkiller` 和 `islandpreneur007` 报告的痛点在于：错误不以崩溃的形式表现，而是以“静默的语义错误”呈现（文件内容被凭空顶替、搜索返回为空但又被判定为“正常完成”）。这通常比显式崩溃更难根除，用户呼唤更强的文件 I/O 安全语义和分析工具的精确性（`islandpreneur007`: “classifies as timeout despite model completion”）。

***

## 8. 待处理积压

随着项目推进，以下是一些长期悬而未决、严重性高且亟需维护者关注的问题：

*   **`#25592` - 文本泄漏到消息通道**（Diamond Lobster 级别，创建于 2026-02-24）
    *   *链接*: [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
    *   *分析*: 已经存在 104 天，是社区热点的长期王者。尽管它被标记了各项 Sweeper 标签，但是仍未进入修复轨道。这已经影响到生产级 SLA，是一个“已识别的头号公敌”，但未看到明确的 PR 对应。

*   **`#29387` - 引导文件被忽略 (Bootstrap silented ignored)**（Diamond Lobster，影响: 安全/会话）
    *   *链接*: [Issue #29387](https://github.com/openclaw/openclaw/issues/29387)
    *   *分析*: 用户在 2 月 28 日就报告了核心的引导系统严重 Bug，但项目至今仍未提出一个明确的修复方案或决定未来的行为（`needs-product-decision` 和 `needs-maintainer-review` 标签共存表明了内部在此问题上存在设计分歧）。

*   **`#31583` - `exec` 工具不继承技能环境变量**（Diamond Lobster，影响: 安全/Provider）
    *   *链接*: [Issue #31583](https://github.com/openclaw/openclaw/issues/31583)
    *   *分析*: 同样是 3 月初的 Issue。虽然已有链接的 PR，但尚未合并。对于任何依赖 `env` 注入密钥的场景（如 Git 操作），这是一个功能性阻断；该积压影响了对 OpenClaw 作为“平台底座”的信任。

*   **`#22358` - 子 Agent 后置完成扩展钩子 (Post-subagent hook)**（Diamond Lobster，影响: 会话/安全）
    *   *链接*: [Issue #22358](https://github.com/openclaw/openclaw/issues/22358)
    *   *分析*: 该功能请求已提出 107 天，在 Agent 的“层次化编排”中，缺少一个官方的扩展点来截获子 Agent 的完成事件以生成结构化的“事后回溯”日志。这一缺失让高级用户无法构建复杂的反思或工作流水线任务。

**备注**：如果以上积压问题不能在近期发布中（例如 2026.6.x 系列）得到充分解决，可能会继续增加社区在安全性和可控性方面对项目稳定性的质疑。

---

## 横向生态对比

好的，这是基于您提供的各项目社区动态摘要，为技术决策者和开发者撰写的横向对比分析报告。

---

## 个人 AI 助手开源生态横向对比分析报告 (2026-06-08)

**分析师：** AI 智能体与个人 AI 助手开源生态资深技术分析师
**报告日期：** 2026-06-08

### 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“高活跃度、高分化、高期待并存”** 的繁荣期。一方面，核心项目（如 OpenClaw、Hermes Agent、ZeroClaw）保持着极高的迭代速度，社区贡献者众，表明技术路径已验证，市场接受度正在快速提升。另一方面，技术路线开始出现显著分化：**多智能体协作（A2A）** 与 **轻量级、可嵌入架构** 成为两大主流发展方向，而**稳定性、会话一致性、Token 成本控制**则成为所有项目共同面临，且尚未完美解决的“必答题”。此外，企业级功能（如深度安全审计、声明式配置、多租户支持）已从“可选”变为“竞争标配”，标志着该生态正从早期探索阶段迈向生产环境落地阶段。

### 2. 各项目活跃度对比

| 项目名 | 今日 Issue 更新 | 今日 PR 更新 | 今日 Release | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 294 | 500 | 0 | **中度风险**：社区庞大，但核心回归 Bug 与长期积压问题消耗着用户信任。评审积压严重。 |
| **Hermes Agent** | 50 | 50 | 0 | **潜力极高**：A2A 落地是里程碑事件，但 46 个待合并 PR 形成严重瓶颈，若不解锁将影响士气。 |
| **ZeroClaw** | 50 | 50 | 0 | **状态良好**：正冲刺 v0.8.0，同时解决多个 S0/S1 级 Bug，快速迭代与修复并行，活跃健康。 |
| **PicoClaw** | 21 | 20 | 1 (Nightly) | **非常健康**：响应迅速、合并率高，大量低层代码质量的修复表明项目正在进入健壮性打磨阶段。 |
| **NanoBot** | 8 | 22 | 0 | **敏捷高效**：Bug 报告与修复形成高效闭环，社区协作热情高，但长期 PR 审查需加强。 |
| **CoPaw** | 22 | 10 | 0 | **中度风险**：渠道 Bug 修复迅速，但多个严重回归问题（v1.1.10）影响升级意愿，稳定性承压。 |
| **LobsterAI** | ~14 (主要 stale) | 2 | 0 | **警示状态**：活跃度偏低，7 个核心 Bug 已积压 2 个月，有陷入“低维护陷阱”的风险。 |
| **Moltis** | 1 | 0 | 0 | **低活跃**：处于迭代间歇期，唯一 Issue 是移动端输入体验，无代码变更。 |
| **NullClaw, TinyClaw, ZeptoClaw** | 0 | 0 | 0 | **停滞**：过去 24 小时无任何活动，项目或已冻结。 |
| **IronClaw** | 50 | 38 | 0 | **高强度重构**：团队内部驱动创新，但版本发布因破坏性变更阻塞，社区外部贡献者门槛较高。 |

**结论：** 生态呈 **“头部多强，长尾分化”** 格局。**PicoClaw** 和 **NanoBot** 在社区健康度和响应效率上表现最佳；**Hermes Agent** 和 **ZeroClaw** 代表了技术前沿与高活跃度，但面临增长的烦恼（审查积压）；**LobsterAI** 和 **Moltis** 则需警惕活跃度下滑风险。

### 3. OpenClaw 在生态中的定位

- **优势：**
    - **社区规模绝对领先**：以 294 Issues / 500 PRs 的单日活动量看，OpenClaw 的社区参与者数量是相邻竞品的 8-10 倍。这意味着它有更丰富的插件生态、教程和第三方集成。
    - **产品广度**：支持最多的通道（Slack, iMessage, Telegram, 飞书等），覆盖最多的 AI Provider，是“全能型”平台的代表。
    - **用户语言**：报告中的 Issue 标题和用户 ID（如 `yair`, `infoanton`）多为英文，表明其社区国际化程度极高，是目前生态的事实标准（Core Reference）。

- **技术路线差异：**
    - **更“重”的架构**：相比 NanoBot 或 PicoClaw 的轻盈，OpenClaw 功能全面但架构复杂度和耦合度更高。这导致其在进行大的基础设施重构（如核心会话迁移至 SQLite #88838）时需要采用复杂的“抽象分支”模式，验证周期长。
    - **平台而非框架**：OpenClaw 更像是“操作系统”，用户在其上运行 Agent，而非像 Hermes 那样追求 Agent 间的互联。其更新日志中普遍存在的“回归”问题（如 d #88312），从一个侧面反映了其变更的波及范围远超竞品。

- **与同类对比（Hermes Agent, ZeroClaw）：**
    - **vs Hermes Agent**：Hermes 凭借 **A2A 协议插件零侵入落地 (#41711)** 在智能体协作架构上取得了领先；而 OpenClaw 仍未解决其社区呼声最高的 A2A 相关问题（类似 #3566）。在 Agent 互操作性上，OpenClaw 暂时落后。
    - **vs ZeroClaw**：ZeroClaw 正在用 v0.8.0 证明其快速修复和交付的能力，尤其在快速解决“Web 面板不可用 (#4866)”这类阻塞性问题上优于 OpenClaw。OpenClaw 面临大量“已识别但未进入修复轨道”的积压问题（如 #25592 文本泄漏），给社区留下了“客服响应慢”的印象。

### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **多智能体/Agent 协作** | **Hermes** (落地), **OpenClaw**, **ZeroClaw**, **NanoBot** (子Agent) | 从简单的 Agent 链，进化到标准化的 **A2A 协议**、**子 Agent 模型自定义**、**Agent 间路由与任务编排**。 |
| **配置与记忆可靠性** | **OpenClaw**, **ZeroClaw**, **NanoBot**, **LobsterAI**, **CoPaw** | 核心痛点是：配置损坏导致系统崩溃、记忆/上下文意外清空或膨胀、静默覆盖文件。所有项目都在寻求**更健壮的存储、更透明的上下文管理、以及更强的 I/O 安全语义**。 |
| **对话/会话控制粒度** | **OpenClaw**, **NanoBot**, **LobsterAI** | 用户普遍要求清晰区分“内部推理轨迹”与“最终用户消息”，并要求更精细的回滚、撤回和消息编辑能力。这已成为衡量 UX 成熟度的基本标准。 |
| **沙箱与安全边界** | **NanoBot** (Bubblewrap), **PicoClaw**, **IronClaw** | 容器/沙箱的安全加固是跨项目共性问题。包括：`HOME` 未重置 (NanoBot)，`allow_from` 绕过 (PicoClaw)，TOCTOU 攻击 (IronClaw) 等。环境兼容性是最大挑战（如 Ubuntu 24.04）。 |
| **全平台稳定性** | **Hermes**, **PicoClaw**, **NanoBot**, **CoPaw** |	多个项目被跨平台 Bug 困扰，从 Windows 网关崩溃 (Hermes) 到 macOS 更新卡死，再到 Linux 桌面冻结。表明很多核心逻辑在初期开发时未充分进行全平台测试，现在正在集体“还债”。 |

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **通用生产型**：全能通道、海量集成、复杂工作流 | 技术型极客、需要“一站式”个人 AI 中枢的高级用户 | **插件中心** 架构，功能丰富但耦合紧密。是生态系统中的“大哥大”。 |
| **Hermes Agent** | **Agent 协作与生产流水线**：A2A 协议、Kanban 看板、Cron 低代码 | **AI 原生创业者**、内容创作多 Agent 团队 | **插件化、零侵入核心**，代码优雅。定位是 Agent 的“社交网络”和“工作流编排平台”。 |
| **ZeroClaw** | **开发者优先 (TUI)**：体验流畅、配置灵活、Provider 生态开放 | **CLI/PowerUser** 开发者，追求极致的终端控制与启动速度 | **TUI 优先**，架构设计上对 Provider 的兼容性（一次 PR 支持 7 个新 Provider）是其核心竞争力。 |
| **NanoBot** | **轻量极速与安全**：Bubblewrap 沙箱、社区 Bug 响应迅速、代码简洁 | **安全和性能敏感**的开发者，希望在最少依赖下快速部署 | **轻量核心 + 沙箱隔离**。架构追求简洁，Bug 修复敏捷度高。 |
| **PicoClaw** | **多场景整合与未来金融**：Kagi/Matrix 多通道，底层高频交易模块 | **边缘部署、跨平台用户**（Android）、以及对量化交易有探索欲的开发者 | **模块化明显**，ClawTrade 子项目暗示其正在向金融自动化延伸，与其他项目的“通用助手”定位显著不同。 |
| **CoPaw** | **中国企业微信集成**：深度绑定企业微信生态 | 国内企业用户，依赖企业微信办公的场景 | **渠道深度绑定**，专注于特定垂直渠道（Yuanbao/WeCom）的体验打磨，代价是通用性稍弱。 |
| **LobsterAI** | **网易云生态**：AI 协同、技能商店概念（Skill Workshop） | 网易（中国）生态内用户 | 更像是一个面向中国市场的、封装好的商业产品。UI 与 UX 层面的改进请求（如颜色标注、标签）占比高，技术深度创新较少。 |
| **Moltis** | **移动端极简** | 追求轻量、移动优先的个人用户 | 几乎无社区讨论，唯一的 Issue 聚焦于移动端输入，定位可能是最小可用模型。 |

### 6. 社区热度与成熟度

| 活跃度分层 | 项目 | 阶段特征 |
| :--- | :--- | :--- |
| **第一梯队：** <br> **快速迭代/高活跃** | Hermes Agent, ZeroClaw, OpenClaw | 日均 Issues + PRs > 100。核心功能（如 A2A, v0.8.0, 新 Release）正被大量推进。社区高度活跃，但也面临**审查阻塞、回归 Bug 频发**的成长烦恼。 |
| **第二梯队：** <br> **质量巩固/稳定增长** | PicoClaw, NanoBot, IronClaw, CoPaw | 日均活跃 20-100。项目已过了爆发式增长期，开始重点解决**架构健壮性、测试覆盖率和渠道兼容性**。Bug 修复效率高，社区健康，是生产环境部署的可靠选择。 |
| **第三梯队：** <br> **稳定维持/低活跃** | LobsterAI, Moltis | 日均活跃 < 10。Issues/PRs 更新缓慢，可能存在维护者精力不足或项目方向已定的情况。社区存在感较弱，新用户需警惕长期维护风险。 |
| **停滞/冻结** | NullClaw, TinyClaw, ZeptoClaw | 过去 24 小时零活动。大概率已不再维护，应避免将其作为技术选型的参考。 |

### 7. 值得关注的趋势信号

1.  **多Agent协作从“概念”走向“架构标配”**：Hermes Agent 的 A2A 插件化落地是本周最重磅的事件。这意味着**单一 Agent 能力不再是竞争壁垒，Agent 间的互联互通、任务编排与信息交换将成为下一阶段的核心竞争力。** ZeroClaw 和 NanoBot 对多智能体路由和子Agent的支持，也从侧面印证了这一趋势。

2.  **“上下文管理”成为系统性挑战**：用户对会话一致性、记忆可靠性的抱怨，已从“个例”变为“共同声音”。多个项目（OpenClaw, NanoBot, ZeroClaw）都在同时处理“文本泄漏”、“消息丢失”、“Prompt膨胀”等问题。这表明，**现有基于滑动窗口或简单摘要的上下文管理机制已不敷使用**，未来专为 Agent 设计的、可审计、可回溯的记忆与上下文管理系统（类似向量库+关系型数据库混合方案）将成为刚需。

3.  **架构两极分化正在形成**：生态正在演化出两大清晰流派：
    - **“大而全”的平台派（OpenClaw, IronClaw）**：提供一站式解决方案，面向高端用户和企业，但面临复杂度高、Bug多、迭代慢的挑战。
    - **“小而美”的轻量派（NanoBot, PicoClaw, Hermes Agent）**：专注于核心体验、启动快、安全、易于二次开发。他们通过插件化或模块化功能（如 A2A 插件、交易模块）实现扩展，架构更灵活。

4.  **安全与可控性成为竞争焦点**：从“静默文件写入”导致数据丢失，到“沙箱配置复杂”导致崩溃，再到“权限绕过”漏洞，安全问题正在从“隐藏风险”变为“显性问题”。**能够提供声明式安全策略、沙箱默认安全、以及可审计执行轨迹的平台，将在企业级用户中获得青睐。**

5.  **端侧部署与新协议崛起**：PicoClaw 合并 Android Termux 指南，以及社区对轻量网关模式（Gateway-Lite）的呼吁，表明**用户希望将 AI 能力下沉到更多设备**。同时，对谷歌 A2A、以及Omniroute等第三方路由协议的关注，预示着生态系统正变得日益开放和互联。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot GitHub 数据生成的 2026-06-08 项目动态日报。

---

### NanoBot 项目动态日报 (2026-06-08)

**数据采集区间：** 2026-06-07 ~ 2026-06-08

---

### 1. 今日速览

项目昨日迎来了极高强度的迭代，24小时内累计处理了8条 Issue 和22条 PR。**Bubblewrap沙箱在Ubuntu 24.04的兼容性危机**和**Dream模块禁用后的上下文不可控**成为社区讨论的双重焦点。值得注意的是，社区应对非常敏捷，针对暴露出的严重Bug几乎做到了“报告即有修复PR”的高效闭环。整体来看，项目正处在积极修复历史债、并迅速响应前沿操作系统兼容性的活跃期。

---

### 2. 版本发布

*无新版本发布。*

---

### 3. 项目进展

昨日共有5个PR被合入主分支，修复了多个影响深远的模块问题：

- **Dream模块稳定性修复**：PR [#4244](https://github.com/HKUDS/nanobot/issue/4244) 合入，修复了当 `dream.enabled=false` 时，因为游标不推进导致所有历史记录被无限注入系统提示（Prompt Bloat）的严重问题。值得一提的是，同一时段还有另一个贡献者提交了类似的修复PR [#4243](https://github.com/HKUDS/nanobot/pull/4243)，体现出社区协作的高度自发性。
- **自定义Provider兼容性增强**：PR [#4227](https://github.com/HKUDS/nanobot/pull/4227) 合入，解决了DeepSeek、Kimi等第三方模型返回空字符串 `reasoning_content` 时被错误转换为 `None` 的问题，保证了数据传递的纯净与协议合规。
- **WebUI视觉体验升级**：PR [#4240](https://github.com/HKUDS/nanobot/pull/4240) 合入，WebUI内的代码块现在支持ANSI彩色输出渲染，极大提升命令行工具返回结果的可读性。
- **通道适配遗留问题清理**：针对飞书 (PR [#2885](https://github.com/HKUDS/nanobot/pull/2885)) 和WhatsApp (PR [#2663](https://github.com/HKUDS/nanobot/pull/2663)) 的群组@提及识别修复均已合入，多平台群聊体验得到进一步夯实。

---

### 4. 社区热点

- **Bubblewrap沙箱跨平台适配**（Issues [#4236](https://github.com/HKUDS/nanobot/issue/4236)、[#4237](https://github.com/HKUDS/nanobot/issue/4237)、PR [#4239](https://github.com/HKUDS/nanobot/pull/4239)）
  - **诉求**：用户@primit1v0连续报告两个关于Bubblewrap沙箱的严重问题。一是沙箱内`$HOME`环境变量未重置导致工具写入失败（#4237），二是在Ubuntu 24.04上因内核限制非特权用户命名空间导致沙箱完全无法工作（#4236）。这暴露了沙箱模块在现代Linux发行版上开箱即用的短板。
  - **反应**：用户随即提交了修复HOME问题的PR [#4239](https://github.com/HKUDS/nanobot/pull/4239)，但内核命名空间限制问题尚无官方修复方案。

- **同一Bug的竞速修复**（Issue [#4242](https://github.com/HKUDS/nanobot/issue/4242)、PRs [#4243](https://github.com/HKUDS/nanobot/pull/4243) & [#4244](https://github.com/HKUDS/nanobot/pull/4244)）
  - **诉求**：用户@skyline75489报告关闭Dream后历史记录失控。社区两位贡献者几乎是同一时间提交了完全不同的修复方案。这种“一题多解”的现象表明该Bug触及了很多用户的日常使用痛点（Token浪费、响应变慢），社区对此容忍度极低。

---

### 5. Bug 与稳定性

按严重程度排列：

- **[严重] 会话消息意外丢弃** ([#4203](https://github.com/HKUDS/nanobot/issue/4203))：会话管理器 `find_legal_message_start` 函数在遇到“孤立工具结果”时，会错误地将之前所有用户消息丢弃。这属于严重的数据丢失Bug。已有对应修复PR [#4219](https://github.com/HKUDS/nanobot/pull/4219)（待合并）。
- **[严重] 沙箱Home目录未重置** ([#4237](https://github.com/HKUDS/nanobot/issue/4237))：Bwrap沙箱保留宿主`HOME`环境变量，导致依赖Home目录的工具（如git）执行失败。修复PR [#4239](https://github.com/HKUDS/nanobot/pull/4239) 已提交。
- **[严重] 沙箱在Ubuntu 24.04上崩溃** ([#4236](https://github.com/HKUDS/nanobot/issue/4236))：Ubuntu 24.04默认安全策略封锁用户命名空间，导致Bwrap沙箱初始化失败。**目前无直接修复PR，可能成为新用户采用的障碍。**
- **[严重] Dream禁用后Prompt膨胀** ([#4242](https://github.com/HKUDS/nanobot/issue/4242))：禁用Dream模块后历史记录无限注入，导致Token消耗激增。已通过PR [#4244](https://github.com/HKUDS/nanobot/pull/4244) 修复。
- **[中等] API空响应重试致用户消息重复** ([#4234](https://github.com/HKUDS/nanobot/issue/4234))：OpenAI兼容API的空响应重试机制会导致用户消息被重复插入。修复PR [#4234](https://github.com/HKUDS/nanobot/pull/4234) 已提交。

---

### 6. 功能请求与路线图信号

- **WebUI信息面板强化** ([#4233](https://github.com/HKUDS/nanobot/issue/4233))：用户希望在界面直接看到当前运行的NanoBot版本号，并提示是否有新版可用。PR [#4235](https://github.com/HKUDS/nanobot/pull/4235) 已提交实现。这表明官方正推动WebUI作为主要的用户交互界面，并开始注重应用生命周期管理。
- **子Agent模型定制化** ([#4231](https://github.com/HKUDS/nanobot/issue/4231))：用户要求在`spawn`工具（创建子Agent）中增加`model`参数。这反映出用户不满足于简单的单模型对话，开始探索“主Agent复杂推理 + 子Agent低成本执行”的多Agent架构。**这是一个明确的路线图信号，可能成为Agent编排能力的下一个突破口。**
- **基础设施安全加固** ([#4123](https://github.com/HKUDS/nanobot/pull/4123))：MCP服务器的SSRF防护已持续开发一周，表明社区对连接外部不可信MCP服务器的安全风险高度警惕，该PR已是MCP功能合并的强依赖。

---

### 7. 用户反馈摘要

- **“沙箱不是开箱即用的”**：用户@primit1v0在[#4236](https://github.com/HKUDS/nanobot/issue/4236)中表达了对Bubblewrap在最新Ubuntu上配置复杂度的失望。用户反映这需要同时掌握沙箱技术和系统内核参数调整，入门门槛过高。
- **“上下文莫名其妙就丢了或膨胀了”**：用户@huji820（[#4203](https://github.com/HKUDS/nanobot/issue/4203)消息丢弃）和@skyline75489（[#4242](https://github.com/HKUDS/nanobot/issue/4242)Prompt膨胀）的反馈表明，**AI Agent的历史上下文完整性是用户体验的生命线**。任何意外的增减都会严重破坏对话的连续性和可控性。
- **“请严格按协议传递我的数据”**：来自自定义Provider用户（如@tjc0726，[#4105](https://github.com/HKUDS/nanobot/issue/4105)）的反馈表明，社区对第三方模型的支持有极高要求，框架不能自作主张修改模型产生的原始数据（如将空字符串转为None），必须严格遵守协议。

---

### 8. 待处理积压

- **关键特性PR长期未Review**：
  - **工具调用验证严格化** ([#4190](https://github.com/HKUDS/nanobot/pull/4190), @chengyongru)：该PR旨在改变工具调用的错误处理模式，从“静默修复”转为“明确报错”。该改动影响所有通道，需维护者重点决策。已开放4天，无任何Review。
  - **MCP SSRF安全加固** ([#4123](https://github.com/HKUDS/nanobot/pull/4123), @yu-xin-c)：安全补丁长期积压会显著增加系统风险，建议尽快合入或给出修改意见。

- **基础设施测试框架PR**：
  - **Agent Runner测试框架** ([#3982](https://github.com/HKUDS/nanobot/pull/3982)) 与 **Memory生命周期测试** ([#4193](https://github.com/HKUDS/nanobot/pull/4193))：均来自@yu-xin-c。这两个PR对项目长期代码质量和回归测试覆盖率至关重要，但目前均处于无人审查状态。

- **严重Bug无修复计划**：
  - **Bubblewrap在Ubuntu 24.04上崩溃** ([#4236](https://github.com/HKUDS/nanobot/issue/4236))：作为当前最严重的阻塞性环境Bug，没有任何分配人和修复计划，是用户Onboarding的最大障碍。建议维护者优先评估，至少应在文档中提供适配指南（如开启`kernel.unprivileged_userns_clone`）。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent 2026-06-08 日 GitHub 数据生成的智能体与个人 AI 助手项目动态日报。

---

### Hermes Agent 项目动态日报 (2026-06-08)

**报告周期：** 2026-06-07 至 2026-06-08
**分析师：** AI 智能体与个人 AI 助手领域开源项目分析师

---

#### 1. 今日速览

*   **活跃度极高：** 项目今日迎来爆发日，24小时内累积 50 条 Issue 更新与 50 条 PR 提交。33 个新开启/活跃的 Issue 表明社区反馈和需求仍在高速增长。
*   **架构里程碑：** A2A（Agent-to-Agent）协议在社区多月翘首以盼后，以**零核心侵入的插件形态正式落地**（PR #41711），标志着 Hermes 从“个人助手”正式迈入“Agent 间互操作”时代。
*   **稳定性重构期：** 针对困扰用户已久的 Windows 网关崩溃、macOS 更新卡死、Linux 桌面冻结等全平台顽疾，团队今日集中提交了多项高优修复（#41761, #41765, #41764），平台适配正在系统性补课。
*   **健康度警示：** 当前有 **46 个待合并 PR**，形成严重审查积压，合入速率远低于提交速率。若不加快 Review，极易造成贡献者挫败感。
*   **版本静止：** 今日无新版本发布，但大量核心功能与修复已就绪，预计下一个版本将是重磅更新。

---

#### 2. 版本发布

*   无。

---

#### 3. 项目进展

今日共有 4 个 PR 被合入，17 个 Issue 被关闭。项目在 Agent 交互协议、配置管理、跨平台稳定性及用户体验上均取得关键进展：

**核心功能落地：**
*   **A2A 互操作协议插件化 ([PR #41711](NousResearch/hermes-agent PR #41711))：** 本日最重磅的架构更新。该 PR 实现了对 Google A2A 开放标准的完整双向支持，允许 Hermes Agent 发现、通信并协调异构 Agent。最关键的是，所有改动封装在单个插件中，无核心侵入，维护了代码的优雅性。直接回应了社区最核心的需求 Issue #514。
*   **Profile 配置继承 ([PR #41741](NousResearch/hermes-agent PR #41741))：** 引入配置继承机制，Profile 无需再做完整拷贝，仅需存储差异项。此举大幅优化了多 Profile 用户的配置管理体验。

**重要 Bug 修复与闭包：**
*   **对话压缩 Session 失步 ([#34089](NousResearch/hermes-agent Issue #34089), P1)：** 已关闭。曾导致 Agent 上下文与网关路由状态不一致，造成静默丢消息的严重问题已被彻底修复。
*   **KV 缓存失效 ([#13631](NousResearch/hermes-agent Issue #13631))：** 已关闭。修复了 Prompt Caching 后端中 KV Cache 被无意重建的问题，对依赖前缀缓存降本提效的生产环境用户至关重要。
*   **Delegate 工具配置失效 ([#32671](NousResearch/hermes-agent Issue #32671))：** 已关闭。修复了 `delegation.*` 设置在 v0.14.0 上被静默忽略的回归 Bug。
*   **限界记忆与归档 ([#32064](NousResearch/hermes-agent Issue #32064), [#35186](NousResearch/hermes-agent Issue #35186))：** 已关闭。引入了持久化无限用户记忆与归档路径，解决了“记忆满了只能硬删”的用户痛点。

**桌面端与稳定性修复：**
*   **看门狗与恢复机制：** 针对 Windows 网关崩溃的自动恢复看门狗 ([PR #41761](NousResearch/hermes-agent PR #41761)) 和针对网关流式生成崩溃的检查点恢复 ([PR #41765](NousResearch/hermes-agent PR #41765)) 已提交 PR。
*   **桌面端功能合并：** `send to all` 广播功能 ([PR #39474](NousResearch/hermes-agent PR #39474)) 已合并，可同时向所有 Profile 发送提示。侧边栏悬停浮出 ([PR #41670](NousResearch/hermes-agent PR #41670)) 与预览链接集成标签系统 ([PR #41762](NousResearch/hermes-agent PR #41762)) 也在今日提交。

---

#### 4. 社区热点

*   **#514 A2A Protocol Support ([Issue #514](NousResearch/hermes-agent Issue #514), 👍18, 💬20)**
    这不仅是今日，也是近几个月来社区最热的议题。用户对建立 Agent 间“社交网络”的渴望极为迫切。随着配套修复 PR #41711 的提交，讨论焦点已从“是否支持”转向“如何在生产中高效利用”。该 Issue 已开放 3 个月，圆满结局在望。

*   **#41222 Kanban Board 集成桌面端 ([Issue #41222](NousResearch/hermes-agent Issue #41222), 💬1)**
    虽然刚提交不久，但从提出者的“多Agent创意生产工作室”背景来看，这是一个高质量的需求信号。用户对在桌面端与 CLI 间切换看板感到明显摩擦，请求将看板原生集成进桌面 App。这很可能是 UX 路线图上继 A2A 之后的下一高地。

*   **多平台升级与崩溃问题**
    macOS 更新卡死 ([#38974](NousResearch/hermes-agent Issue #38974))、Linux 桌面更新冻结 ([#41737](NousResearch/hermes-agent Issue #41737))、Windows 网关崩溃 ([#41662](NousResearch/hermes-agent Issue #41662)) 等引发了大量跨平台用户的共鸣，说明全平台稳定性是社区最广泛的“集体情绪”。

---

#### 5. Bug 与稳定性

按严重程度与影响面排列，标注修复进展：

**网关与会话层（最具影响力）：**
*   **P2 [macOS] 网关健康检查失败** ([#41676](NousResearch/hermes-agent Issue #41676))：导致 Telegram 入站消息中断，**暂未修复**。
*   **P2 [Windows] 网关崩溃后无自动恢复，Cron 停止** ([#41662](NousResearch/hermes-agent Issue #41662))：**已提交修复 PR #41761**。
*   **P2 [全平台] 网关流式生成崩溃导致上下文丢失** ([#41696](NousResearch/hermes-agent Issue #41696) 关联)：**已提交修复 PR #41765**。
*   **P2 [全平台] DM 会话共享 Session 致消息错乱** ([PR #41764](NousResearch/hermes-agent PR #41764))：**已提交修复**。

**Provider 与平台层：**
*   **P2 [OpenAI] Codex GPT-5.5 上下文上限被错误判定** ([#27918](NousResearch/hermes-agent Issue #27918))：**已修复**。
*   **P2 [OpenAI] 多 Profile 切换导致反复重认证** ([#6653](NousResearch/hermes-agent Issue #6653))：**暂未修复**。
*   **P3 [Xiaomi] 视觉模型 API 返回 400 致会话中毒** ([#39685](NousResearch/hermes-agent Issue #39685))：**暂未修复**。
*   **P2 [WhatsApp] 发送消息因缺少 JID 后缀失败** ([#41660](NousResearch/hermes-agent Issue #41660))：**暂未修复**。

**桌面端/CLI：**
*   **P2 [macOS] 更新卡死** ([#38974](NousResearch/hermes-agent Issue #38974))：**已修复**。
*   **P3 [Linux] 更新至 100% 时冻结，应用不可用** ([#41737](NousResearch/hermes-agent Issue #41737))：**暂未修复**。
*   **P3 [Desktop] Gateway 模式下附件上传失败** ([#41669](NousResearch/hermes-agent Issue #41669))：**暂未修复**。
*   **P3 [Desktop] 打包时缺少 Bundle 启动黑屏** ([PR #41729](NousResearch/hermes-agent PR #41729))：**已提交修复**。

**工具与基础设施：**
*   **P3 [terminal] CWD 被删除后崩溃** ([#41686](NousResearch/hermes-agent Issue #41686))：**暂未修复**。
*   **P3 [mcp_catalog] 子进程无超时将永久挂起** ([PR #41758](NousResearch/hermes-agent PR #41758))：**已提交修复**。

---

#### 6. 功能请求与路线图信号

*   **（最高信号）A2A 多Agent协作：** PR #41711 已就绪，A2A 将成为下一个 Release 无可争议的核心特性。Signal 强度：**已确认实施**。
*   **（高优先级）Cron 配方 / 低代码自动化 ([PR #41309](NousResearch/hermes-agent PR #41309))：** “无需了解 Cron 语法，填写字段就能生成任务”的设计，信号非常明确：项目正在大步降低用户部署自动化的门槛。Signal 强度：**即将落地**。
*   **（高优先级）Kanban 看板集成桌面端 ([#41222](NousResearch/hermes-agent Issue #41222))：** 多Agent 工作流重度用户的强烈呼声，与 A2A 协议形成了完美的“世界观”闭环（通信+可视化编排）。Signal 强度：**强力候选**。
*   **（中优先级）无限记忆与 Hindsight 归档 ([#32064](NousResearch/hermes-agent Issue #32064), [#35186](NousResearch/hermes-agent Issue #35186))：** 已关闭，意味着功能已上线。用户已开始期待更智能的检索与标签化。Signal 强度：**已交付，等待下一阶段进化**。
*   **（中优先级）插件系统增强 ([PR #41752](NousResearch/hermes-agent PR #41752))：** `on_session_title` 钩子被用于 `tmux` 窗口标题同步，展现了社区对插件的创意需求，未来 SDK 扩展潜力巨大。Signal 强度：**持续积累**。

---

#### 7. 用户反馈摘要

*   **记忆与上下文可靠性是最高频痛点：**
    多位高级用户（如 `0xAlcibiades`、`zeusbotadmin`）详细报告了对话压缩导致“失忆”和 KV Cache 失效导致成本飙升等问题。用户对长期对话的可靠性要求极高，项目对此的快速响应（#34089, #13631 关闭）获得了正面评价。

*   **跨平台“三方受敌”：**
    > “macOS 更新卡死，只能靠重装”、“Windows 网关静默崩溃，Cron 任务全灭”。
    用户虽然热爱 Hermes，但全平台适配的 Bug 正在消耗信任。不过，积极提交详细日志并主动需求帮助（如 `#41662` 用户在 Issue 中详细描述了 `os.kill` 在 Windows 上的差别），也证明了用户群体的极高粘性。

*   **多Agent 协作场景的先锋用户：**
    > “My team includes Writer, Character Designer, Storyboard Artist...”
    从 `#25176` 和 `#514` 的讨论中可以看到，用户正在用 Hermes 编排真正的 **AI 内容制作生产线**。他们不仅是功能的索取者，也是项目愿景的共同塑造者。这类用户对 A2A 和看板的强烈需求，为项目提供了清晰的产品发力点。

---

#### 8. 待处理积压与维护者提醒

*   **🚨 [Critical] 审查积压：46 个待合并 PR**
    这是目前项目健康度的**最大风险**。建议 @teknium1 及核心团队优先启动“Review Sprint”，按以下水位线处理：
    1.  **高优 Bug 修复：** `#41761` (Windows 看门狗), `#41765` (流式检查点), `#41764` (DM 隔离), `#41758` (MCP 超时)。
    2.  **社区独立贡献：** `#36286` (Minimax CN OAuth), `#41757` (剪贴板工具), `#41747` (桌面缩放持久化)。新贡献者的 PR 超过 24 小时未 Review 会严重影响社区生态。
    3.  **核心架构功能：** `#41711` (A2A 插件), `#41741` (配置继承), `#41309` (Cron 配方)。

*   **🗂️ [Long-tailing] 待强回的 Feature Issue：**
    *   **#24911 Webhooks 配置选项缺失** (创建: 2026-05-13)：用户严格按文档操作却找不到 UI 入口，这个 Issue 自创建起**官方无任何回应**。可能是严重的界面逻辑 Bug 或文档未更新，需要尽快给予定性回应。
    *   **#41222 Kanban 桌面集成** (创建: 2026-06-07)：高价值特性，目前无官方表态。建议回复用户该功能的规划阶段或实现难点，管理好社区预期。

*   **🔧 [中优先级] 等待排查的开放 Bug：**
    *   **#39685 Xiaomi 视觉模型 400 错误**：对于中国区用户至关重要，目前标记为 P3。若团队有中国区 API 资源，建议安排排查。
    *   **#41676 macOS 网关 Healthcheck 失败**：影响 Telegram 等平台的入站消息，是 P2 级的核心功能缺损，亟待定位。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-08

## 1. 🚀 今日速览
过去 24 小时，PicoClaw 项目处于 **高度活跃** 状态，核心维护者和社区贡献者双线并进，项目健康度极佳。

- **响应迅速：** 共处理 21 条 Issue 更新（关闭 17 条），关闭率高达 81%，表明团队正在高效清理积压问题并推进定型。
- **开发火热：** 共 20 条 PR 更新（合并/关闭 11 条，待合并 9 条），大量低层代码质量修复（错误处理、类型安全）涌入，表明项目正在进入 **“健壮性打磨”** 阶段。
- **生态扩充：** 今日合并了原生 Kagi 搜索集成、修复了 Anthropic 模型 ID Bug，并发布了 Nightly Build，有效回应了社区对“发新版本”和“AI 提供商兼容性”的呼声。
- **架构演进：** 一批关于交易所接口 (`EX-*`)、风险引擎 (`RG-*`) 和 CLI 命令 (`EXM-*`) 的开发者任务被批量关闭，暗示 PicoClaw 架构正在向 **金融自动化/高频交易扩展** 方向演进。

## 2. 📦 版本发布
- **Nightly Build: `v0.2.9-nightly.20260608.875cf4a2`** ([查看对比](https://github.com/sipeed/picoclaw/compare/v0.2.9...main))
  - **内容：** 基于 `main` 分支的最新自动化构建。官方警告此版本可能不稳定，不建议在生产环境直接替换正式版。
  - **背景：** 回应了上月曾出现的 Issue #2952（“好久没发新版本了”），表明团队注意到了社区对版本迭代节奏的期待，采用 Nightly 自动化构建以满足尝鲜用户的需求。

## 3. 🛠️ 项目进展
- **新功能与集成：**
  - **Kagi 搜索已合并：** PR #3037 新增了原生 Kagi Web 搜索提供商，用户现在可以直接在 `tools.web` 体系中配置 Kagi。
  - **Android Termux 指南已合并：** PR #2902 上线，补齐了运行在 ARM64 Android 设备的官方文档，解决了 #286 的诉求。
- **基础设施修复与合并：**
  - **Anthropic 模型 ID 修复：** PR #3036 解决了默认配置中因点号（`claude-sonnet-4.6`）导致的 API 404 错误，用户首次启动不再必崩。
  - **消息总线 (Bus) 背压处理：** PR #2906 合并，发布操作不再无限制阻塞，增加了蓄满队列的丢弃统计和健康指标。
- **架构模块化信号：** 开发者 `jcafeitosa` 批量关闭了多个带编号的高阶任务 Issue（如 `EX-00x`, `RG-001`, `EXM-003`），这些任务聚焦于 Binance 交易所连接器、锁无关 Order Book、风险引擎接口等。这表明项目底层正在构建 **高频/量化交易模块** 的标准接口。

## 4. 🔥 社区热点
- **[已关闭] Issue #2674：Codex OAuth 空响应（4 👍 / 8 评论）**
  - **分析：** 这是持续了近两个月的“老” Bug（ChatGPT 后端流式响应导致空回复）。今日被关闭标志着这个引发大量用户困惑的诡异问题已定位并修复，对依赖 Codex OAuth 渠道的用户是绝对利好。
  - [查看 Issue](https://github.com/sipeed/picoclaw/issues/2674)

- **[已关闭] Issue #286：Android Termux 运行指南（2 👍 / 8 评论）**
  - **分析：** 热门文档请求正式完成。证明了社区对移动端/端侧部署的强烈需求，PicoClaw 正在从纯服务器端向边缘设备扩展。
  - [查看 Issue](https://github.com/sipeed/picoclaw/issues/286)

- **[Open] Issue #3044：Matrix `allow_from` 因冒号失效 (Bug)**
  - **分析：** 新爆出的问题，标准 Matrix 用户格式（`@user:domain`）导致身份验证绕过。社区用户 `weissfl` 连续提交了 3 个类似 Issue（含误提的删除请求）。这是严重的权限绕过安全问题，已有关联 PR 待合并，热度极高（需要紧急关注）。
  - [查看 Issue](https://github.com/sipeed/picoclaw/issues/3044)

## 5. 🐛 Bug 与稳定性
按严重程度排列，今日 Bug 修复频率极高：

| 严重程度 | 问题描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| ❌ 严重 | **Telegram 频道静默忽略地理位置消息 (message.location)**。无日志、无响应。 | **待确认** | [Issue #3049](https://github.com/sipeed/picoclaw/issues/3049) |
| ❌ 严重 | **Matrix `allow_from` 因 ID 含冒号失效**。标准用户格式被禁止，权限被绕过。 | **待合并 (Fix PR #3045)** | [Issue #3044](https://github.com/sipeed/picoclaw/issues/3044) |
| ⚠️ 高 | **`mcp add` 全局标志解析为位置参数**。`--no-color` 等根级 Flag 导致 HTTP/S 添加失败，服务被静默错误命名。 | **待合并 (Fix PR #3048)** | [Issue #3041](https://github.com/sipeed/picoclaw/issues/3041) |
| ✔ 已修复 | **多处 I/O 资源写入 `Close()` 错误被吞没**（影响飞书资源下载、媒体文件拷贝等）。 | **今日已合并 (PR #3033, 34, 35)** | [PR #3033](https://github.com/sipeed/picoclaw/pull/3033) |
| ✔ 已修复 | **运行时潜在 Panic**（Agent 启动类型断言、Singleflight 缓存探测、LINE 频道 Sync.Map 断言）。 | **今日已合并 (PR #3040, 46)** | [PR #3040](https://github.com/sipeed/picoclaw/pull/3040) |
| ✔ 已修复 | **默认 Anthropic 模型 ID 错误** (点号 vs 连字号) 导致 404 初始崩溃。 | **今日已合并 (PR #3036)** | [PR #3036](https://github.com/sipeed/picoclaw/pull/3036) |

**稳定性总结：** 今日贡献者 `chengzhichao-xydt` 成为绝对主角，解决了多达 **7 处** 底层代码质量问题（未检查的 Close、类型断言、Getwd 错误），极大提升了运行时健壮性。

## 6. 💡 功能请求与路线图信号
- **高可能性纳入下版本：**
  - **添加 Omniroute 提供商（Issue #2978）：** 用户请求将第三方路由工具 `Omniroute` 作为原生 Provider 加入。目前停留于询问阶段，但结合 Kagi 已并入的趋势，整合第三方路由服务是当前开发重点之一。
  - **结构化日志重构（PR #3050）：** 开发中 PR。将零散的 `log.Printf` 迁移到结构化日志系统。这是运维友好性的必备功能，符合进入生产环境的路线图。
- **路线图潜伏信号：**
  - **交易模块（CLI 与核心接口）：** 今日关闭的 `EXM-003` (Trade/Backtest/Agent CLI)，`RG-001` (Risk Manager)，`EX-001~005` (Exchange Interface, WebSocket, REST, Benchmarks) 暗示 PicoClaw 的 **ClawTrade** 子项目已从设计进入编码阶段，目标为高频、低延迟的金融交易场景。

## 7. 💬 用户反馈摘要
- **@xhynice (Issue #2952) 的痛点：**
  - **Agent 行为异常：** Agent 不遵循 `agent.md`，导致 LLM 在首次对话时自动执行多余的 `actions:run` 命令。
  - **通道自循环 Bug：** QQ 渠道重启后，再次发送信息会触发无休止的重启循环，必须清除上下文。
  - **UI 体验差：** 模型配置界面未默认展示已保存的 API Key 模型列表，添加模型时无法复用 Key。
  - *分析：* 虽然 Issue 因“发新版本”的诉求被关闭，但上述 3 个具体 Bug 可能未被完全解决或回归，建议维护者跟进这些高影响度问题。

- **@LegendAlessandro-Liguori (Issue #2941) 的痛点：**
  - **首次启动必崩：** 默认配置生成的 Anthropic 模型 ID (`claude-sonnet-4.6`) 直接导致 HTTP 404。这是新用户入门时的“第一印象”大 Bug，已被今日的 PR #3036 修复。

- **@terurium / @carlosprados (Issues #3049, #3041) 的不满：**
  - **静默失败：** 无论是 Telegram 发送位置，还是 `mcp add` 误用全局参数，系统都未给用户任何错误反馈。这表明 PicoClaw 在处理“非标准输入”时的错误通道构建有待加强。

## 8. 📌 待处理积压与提醒
- **急需合并 (Fixing New Critical Bugs)：**
  - **`#3045 - fix(identity): allow_from 修复`**：直接解决严重身份绕过 Bug（Issue #3044）。任何使用 Matrix 频道且配置了 `allow_from` 的实例均受影响，**建议优先级合并**。
  - **`#3048 - fix(mcp): 拒绝未知前置标志`**：直接解决 CLI 命令被静默破坏的 Bug（Issue #3041），影响 MCP 工具链的可靠性，**建议优先级合并**。

- **长期未合并/未响应的核心 PR (Stale)：**
  - **`#2904 - Fix agent loop reload and panic cleanup stability`**：已存在 19 天。涉及 Agent 核心循环的重载和 Panic 清理，直接影响运行时稳定性和资源泄露问题，**等待 Review**。
  - **`#2975 - feat(telegram): 回复视为提及`**：已存在 9 天。提升 Telegram 群聊交互体验 (当 `mention_only: true` 时) 的小心机功能，**等待 Review**。

- **提醒维护者关注的功能请求：**
  - **`#2978 - Add omniroute as provider`**：贡献者已询问如何集成或配置，等待社区或维护者给出集成方案或指引文档。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 (2026-06-08)

## 今日速览
过去 24 小时项目保持较高活跃度：新增 2 个 Issue、9 个 Pull Request，其中 3 个 PR 已被合并/关闭。新提交的 Issue #2711 指出现有权限机制存在安全漏洞（`create_agent` 未做角色检查），风险等级高；而困扰社区达一个多月的 Issue #2312（启动时强制删除已跟踪文件导致工作区脏）仍无修复 PR。整体上项目开发节奏快，但安全问题与长期积压仍需关注。

## 项目进展
今日共有 3 个 PR 被合并或关闭，对项目稳定性与运维规范有直接提升：

- **[#2707 – feat(upgrade): startup tripwire + upgrade marker](https://github.com/nanocoai/nanoclaw/pull/2707)**  
  引入启动绊线与升级标记机制，拒绝通过直接 `git pull` 来升级（必须走 `/setup`、`/update-nanoclaw` 等授权路径），防止因跳过迁移而静默损坏。这是部署管线规范化的重要改进。

- **[#2706 – fix(账号轮换): 限制模式并校准切换状态](https://github.com/nanocoai/nanoclaw/pull/2706)**  
  修复多账号轮换核心逻辑：限制 Codex/Gemini 模式进入 Anthropic 轮换，校准 DB 游标漂移，并在成功后即时发送切换通知，增强了多后端支持的健壮性。

- **[#2710 – docs(ollama): allow prompt caching by filtering the cache-busting hash](https://github.com/nanocoai/nanoclaw/pull/2710)**  
  补充 Ollama 文档，指导用户绕过临时生成的查询参数以启用 prompt 缓存，提升本地推理性能。

此外还有 6 个 PR 处于开放状态（详见后续章节），涵盖功能增强、关键修复与质量改进。

## 社区热点
- **[#2312 – groups/global/CLAUDE.md unconditionally deleted on startup](https://github.com/nanocoai/nanoclaw/issues/2312)**  
  该 Issue 已存在一个月（5 月 6 日提出），至今仍有 2 条评论。用户持续抱怨每次启动都会删除版本控制的 `CLAUDE.md`，导致工作区永远不干净，团队协作时每次重新拉取+重启都会产生脏树。虽已标记为 Open 且近期有更新，但尚未分配或修复，社区期待维护者回应。

- **[#2711 – create_agent MCP tool is ungated despite “admin-only” comment](https://github.com/nanocoai/nanoclaw/issues/2711)**  
  今日新提交，虽暂无评论，但内容直接触及安全信任：代码注释与文档均声称该工具仅限 admin，但实现完全未检查角色/容器权限。任何容器均可调用 `create_agent` 创建新 agent 组。一旦被恶意利用后果严重，因此很可能成为未来几日讨论焦点。

- 开放 PR 暂无用户评论，但 [#2709（DB-backed env/blocked_hosts）](https://github.com/nanocoai/nanoclaw/pull/2709) 和 [#2708（收割孤儿容器）](https://github.com/nanocoai/nanoclaw/pull/2708) 均涉及核心配置与运行安全，预计在审查阶段会获得较多关注。

## Bug 与稳定性
按严重程度排列：

1. **严重 – 权限绕过**  
   Issue [#2711](https://github.com/nanocoai/nanoclaw/issues/2711)：`create_agent` MCP 工具被标记为 admin-only，但服务端未执行任何角色/容器检查，任意容器都可创建 agent 组。当前无修复 PR，需立即由维护者介入定级并修补。

2. **中等 – 工作区污染**  
   Issue [#2312](https://github.com/nanocoai/nanoclaw/issues/2312)：`migrateGroupsToClaudeLocal()` 每次启动无条件删除已跟踪的 `groups/global/CLAUDE.md`，导致 Git 工作树永久 dirty。修复方向明确（将文件移出版本控制或更改删除逻辑），但尚无对应 PR。

3. **中等 – 轮询文本重复**  
   PR [#2531](https://github.com/nanocoai/nanoclaw/pull/2531)（Open）：`send_message` 在 mid-turn 触发时导致轮询循环输出重复文本。修复已提交但暂未合并。

4. **中等 – OneCLI 网关绕过失效**  
   PR [#2705](https://github.com/nanocoai/nanoclaw/pull/2705)（Open）：`use-native-credential-proxy` skill 原本应彻底绕过 OneCLI 网关，但因 `nativeCredentialsEnabled()` 只读取 `process.env` 而实际上一直回退到网关。提交了修复但待合并。

5. **低 – 孤儿容器残留**  
   PR [#2708](https://github.com/nanocoai/nanoclaw/pull/2708)（Open）：服务停止时 agent 容器未被动清理，可能导致资源泄漏。PR 提供了 `SIGTERM → SIGKILL` 兜底方案。

## 功能请求与路线图信号
- **[#2709 – feat(container-config): DB-backed env + blocked_hosts](https://github.com/nanocoai/nanoclaw/pull/2709)**  
  由维护者发起（对应内部 Issue #1867），将 `container_configs` 表的 `env` 和 `blocked_hosts` 交由数据库管理。这是配置存储走向持久化、可查询化的关键一步，很可能纳入下一小版本。

- **[#2704 – test(setup): add unit tests for cli-agent parseArgs](https://github.com/nanocoai/nanoclaw/pull/2704)**  
  提升 CLI 参数解析的测试覆盖率，符合项目持续改善代码质量的趋势，合并可能性大。

- **[#1626 – feat: Telegram topic isolation with auto-registration](https://github.com/nanocoai/nanoclaw/pull/1626)**  
  自 4 月 4 日起开放，提供 Telegram 话题隔离能力。虽长期未推进，但仍是社区期待的功能，可能在配置管理改进后再被激活。

- **升级规范** – 已合并的 [#2707](https://github.com/nanocoai/nanoclaw/pull/2707) 将升级路径强制绑定到官方入口，预示未来版本将更加强调部署完整性，可能推广到更多运维校验。

## 用户反馈摘要
本次周期内主要反馈来自两个 Issue 的提交与评论：

- **开发者体验**（#2312）：用户明确表示每次 `git pull` + 重启后工作区“永久 dirty”，不仅影响个人开发，还污染团队 CI/CD 流程。期望要么从仓库移除该文件，要么在删除前判断是否来自版本控制。这体现了对开发环境清洁度的刚性需求。

- **安全性质疑**（#2711）：提交者直接对比代码注释/文档与实际实现，认为这是“claim vs. reality”的矛盾。用户视角看，该问题若不修复，任何入驻的多租户容器都有可能越权创建 agent 组，构成严重信任漏洞。

其余 PR 无评论，无法获取更多定性反馈。

## 待处理积压
关注长期未合并/响应的条目，提醒维护者优先审阅：

- **Issue [#2312](https://github.com/nanocoai/nanoclaw/issues/2312)（5月6日，距今33天）** – 虽近期有更新但无修复 PR，且已被多位用户影响，建议进入里程碑规划。
- **PR [#1626](https://github.com/nanocoai/nanoclaw/pull/1626)（4月4日，距今65天）** – Telegram 主题隔离功能长期 Open，代码可能已过时，需要维护者决定是继续推进还是关闭。
- **PR [#2531](https://github.com/nanocoai/nanoclaw/pull/2531)（5月18日，距今21天）** – 文本重复 bug 修复，审查周期较长，建议尽快合并或给出修改意见。

其余 Open 的 PR（#2709、#2708、#2705、#2704）皆为今日提交，暂不列为积压，但仍需及时安排初审。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw GitHub 数据生成的 2026-06-08 项目动态日报。

---

# IronClaw 项目日报 | 2026-06-08

## 1. 今日速览

项目当前处于**高强度重构与功能冲刺阶段**，核心开发团队正全力推动 `Reborn` 架构的稳定性建设和 `Codex` 产品功能集的落地。过去 24 小时内，社区与团队共处理了 50 条 Issue 和 38 条 PR，其中成功关闭/合并了 7 个 Issue 和 16 个 PR。开发活动主要集中在 WebChat v2 基础能力补齐、Slack 主机集成、Skills 管理系统以及核心安全安全审计机制的深化上。**项目健康度极高，虽暂无新版本发布，但内部迭代速度迅猛。**

## 2. 版本发布

**无。**
当前版本发布流程因包含破坏性变更的 Release PR（[PR #3708](https://github.com/nearai/ironclaw/pull/3708)）仍在审核中而暂停，项目处于大功能开发密集期，发行节奏客观放缓。

## 3. 项目进展

今日合并/关闭了多项极具分量的 PR，项目在多个关键维度上取得了实质性进展：

- **Slack 集成就绪化：** [PR #4463](https://github.com/nearai/ironclaw/pull/4463) 打通了 Slack 主机版的后端持久化存储，[PR #4532](https://github.com/nearai/ironclaw/pull/4532) 新增了管理后台的 Slack 频道选择器，标志着 Slack 通道正式进入 Beta 就绪阶段。
- **WebChat v2 功能补齐：** [PR #4516](https://github.com/nearai/ironclaw/pull/4516) 实现了线程删除功能；[PR #4519](https://github.com/nearai/ironclaw/pull/4519) 新增了会话能力端点（Session Capabilities）用于前端动态识别用户权限；[PR #4116](https://github.com/nearai/ironclaw/pull/4116) 携带了 Google/GitHub/NEAR SSO 登录支持。
- **核心架构与可观测性：** [PR #4488](https://github.com/nearai/ironclaw/pull/4488) 将 ProductWorkflow 拆分为明确的提交/读取/订阅三个门面，为后续 OpenAI API 兼容性接入铺平道路；[PR #4530](https://github.com/nearai/ironclaw/pull/4530) 引入了类型化、结构化的模型可见工具观测数据，极大提升了 AI 执行过程的可解释性。
- **开发者体验与 CI 强化：** [PR #3298](https://github.com/nearai/ironclaw/pull/3298) 和 [PR #3565](https://github.com/nearai/ironclaw/pull/3565) 持续优化了 CI 流程，引入了隐式本地测试门禁并延长了 E2E 超时时间，确保代码库质量。

## 4. 社区热点

今日的热点讨论高度集中在 `Reborn` 架构的设计决策和代码库大规模变更上：

- **[Issue #3280](https://github.com/nearai/ironclaw/issues/3280) 产品工作流门面设计（7 条评论）：** 该 Issue 持续获得最高热度，核心争议点在于如何设计 ProductWorkflow 门面。该门面决定了 IronClaw 如何承接 ProductAdapter 的请求并分发给底层 Host 服务，直接关系未来 OpenAI 路由的接入方式。
- **[Issue #3036](https://github.com/nearai/ironclaw/issues/3036) 配置即代码（5 条评论）：** 运维人员对声明式蓝图的呼声极高，反映了当前手动混合编辑配置文件的痛点，该 Issue 代表了社区对提升多租户部署效率的迫切需求。
- **[PR #4492](https://github.com/nearai/ironclaw/pull/4492) 扩展凭证修复（XL 波及范围）：** 这条大规模改动涉及 Agent、Channel、Tool、Sandbox、Hooks 等多个模块和 DB 迁移，触发了大量 CI 检查和开发者的重点关注。它解决了本地开发中 Credential Staging 的核心痛点。
- **[PR #3708](https://github.com/nearai/ironclaw/pull/3708) 版本发布（持续观望）：** 该发布 PR 包含了 `ironclaw_common` 和 `ironclaw_skills` 的破坏性变更，由于影响下游用户升级策略，至今仍处于开放状态，等待核心维护者的最终批准。

## 5. Bug 与稳定性

今日未报告直接的用户侧崩溃或严重线上回归，稳定性工作主要集中在 `Reborn` 新架构的**安全加固**与**执行逻辑`完善**：

- **高优先级安全加固（暂未合并 Fix PR）：**
  - [Issue #4042](https://github.com/nearai/ironclaw/issues/4042)：租户沙箱进程能力尚不完善，无法安全支持工作区代码执行，需补全。
  - [Issue #3957](https://github.com/nearai/ironclaw/issues/3957)：第三方 Hook 激活固化，防止恶意外联。
  - [Issue #3956](https://github.com/nearai/ironclaw/issues/3956)：文件系统 TOCTOU 安全强化（RESOLVE_NO_XDEV），防止挂载点逃逸。
  - [Issue #3924](https://github.com/nearai/ironclaw/issues/3924)：NoExposureGuard 审计边界覆盖，确保敏感数据不泄漏给模型。
- **核心执行逻辑修复：**
  - [Issue #3423](https://github.com/nearai/ironclaw/issues/3423) 正在定义 Agent Loop 的输入恢复和取消语义，以确保分布式执行器核心的确定性行为。
- **已有 Fix 进度的 PR：**
  - [PR #4530](https://github.com/nearai/ironclaw/pull/4530) 通过结构化工具观测解决了之前错误信息传递混洗的问题。
  - [PR #4492](https://github.com/nearai/ironclaw/pull/4492) 修复了本地开发中扩展凭证未正确通过 SecretStore 提供的问题。

## 6. 功能请求与路线图信号

从 Issue 和 PR 的侧重点可以看出，项目的短期和长期路线图非常清晰：

- **近期即将纳管的功能（Beta 冲刺中）：**
  - **Skills 管理界面：** [PR #4527](https://github.com/nearai/ironclaw/pull/4527) 新增了用户可管理的技能前端和后台端 API，正在等待合并。
  - **Session 能力端点：** [PR #4519](https://github.com/nearai/ironclaw/pull/4519) 使得前端可以根据后端下发的 Capabilities 动态展示 UI（如管理员按钮），是 WebUI Beta 的关键一环。
- **中期路线图信号：**
  - **声明式配置：** [Issue #3036](https://github.com/nearai/ironclaw/issues/3036) 作为长期目标，表明项目正在为多租户 SaaS 做准备。
  - **WASM 组件化探索：** [Issue #3572](https://github.com/nearai/ironclaw/issues/3572) 提出将 ProductAdapter 构建为 WASM 组件，这将是未来插件生态的基石。
  - **OpenAI 兼容 API：** [Issue #3283](https://github.com/nearai/ironclaw/issues/3283) 的持续活跃表明保持主流协议兼容依然是产品化的硬性要求。

## 7. 用户反馈摘要

从 Issue 创建者和维护者的描述中，可以清晰窥见用户（开发者与运维人员）的痛点与诉求：

- **配置复杂性带来的挫败感：** [Issue #3036](https://github.com/nearai/ironclaw/issues/3036) 中明确指出：“用户必须手动混合编辑 `.env`、工作区文档、JSON、扩展安装和运行时标志，**无 Schema、无 Diff、无审计跟踪**，且无法进行源代码级的数据编排。” 这表明当前配置方式是运维人员最大的痛苦来源。
- **开发者体验的繁琐：** [Issue #3044](https://github.com/nearai/ironclaw/issues/3044) 提到：用户希望像 `ironclaw run` 命令一样简单，而不是“手动连接授权、挂载、进程后端、网络策略和批准”。这种对 **零配置启动** 的渴望，反映了工具化向开发工作流渗透的强烈需求。
- **极高的安全敏感性：** 从 [NoExposureGuard (#3924)](https://github.com/nearai/ironclaw/issues/3924) 到 [Hook 激活固化 (#3957)](https://github.com/nearai/ironclaw/issues/3957)，社区对 AI Agent 平台的安全基线要求非常高。用户不仅要求功能可用，更要求底层的 *数据不泄露承诺* 必须是架构级、可审计的，而非仅靠代码检查。

## 8. 待处理积压

以下为目前平台中需维护者特别关注的长期未决事项：

- **版本发布严重堵塞 [PR #3708](https://github.com/nearai/ironclaw/pull/3708)：** 该发布 PR 自 5 月 16 日开启，因包含 `ironclaw_common` 和 `ironclaw_skills` 的 API Breaking Changes 至今悬而未决。这是推进正式版本号的唯一障碍，建议维护者尽快终结评审。
- **声明式配置史诗拆解缺失 [Issue #3036](https://github.com/nearai/ironclaw/issues/3036)：** 虽然被标记为 `suggested_P2`，但该 Issue 是未来可扩展性的关键瓶颈。目前仅停留在方案讨论层面，无任何关联子任务或 PR，建议尽快召开设计会议并拆解为可执行的任务集。
- **WASM 组件化长期规划 [Issue #3572](https://github.com/nearai/ironclaw/issues/3572)：** 到目前为止，该 Issue 仍然没有与之配套的 PoC PR。如果不尽早建立里程碑进行原型验证，可能会在后期与现有 Rust Adapter 产生难以调和的技术债。
- **依赖更新积压：** Dependabot 提交的多条依赖更新 PR（如 `#4503` 38 个 Crate 大更新、`#4002` GitHub Actions 更新、`#4032` WASM 组件更新、`#4499` Tokio 生态更新）普遍处于未答复状态。长期不合并依赖更新可能会导致安全漏洞累积，建议分配周期性维护任务加以处理。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期：2026-06-08**  
**数据截止：2026-06-08 00:00 UTC（过去24小时）**

---

## 📊 今日速览

今日项目整体活跃度中等偏低。代码层面有两个修复 PR 被合并，分别增强了协同模块的负载健壮性和配置迁移的一致性，但无新版本发布。Issue 方面，14 条长期搁置的 issue 被自动标记为 stale，仅新增 1 条关于 token 浪费的疑问。社区反馈仍集中在技能管理、配置同步和 UI 体验上，部分核心 bug 已存在两个月未得到修复，项目维护节奏需要加快。

---

## 🚀 版本发布

无（过去24小时内未发布新版本）

---

## 🛠 项目进展（合并/关闭的 PR）

### #2110 [CLOSED] `fix(cowork): guard oversized OpenClaw image payloads`
- **作者**: liuzhq1986 | 创建时间: 2026-06-04 | 合并时间: 2026-06-08
- **链接**: [PR #2110](https://github.com/netease-youdao/LobsterAI/pull/2110)
- **主要改动**：
  - 在将图片负载发送到 gateway 之前检测是否过大，避免因超限导致的失败。
  - 将类型为 `1009` / 达到最大负载的网关失败归为消息大小错误。
  - 区分单张图片与整条消息的大小限制，提供更清晰的提示。
  - 新增负载估算、错误分类等针对性测试。
- **影响**: 提升协同（cowork）模块在传输图片时的稳定性，减少无提示失败。

### #2117 [CLOSED] `fix(config): preserve deleted provider models after migration`
- **作者**: liuzhq1986 | 创建时间: 2026-06-05 | 合并时间: 2026-06-08
- **链接**: [PR #2117](https://github.com/netease-youdao/LobsterAI/pull/2117)
- **主要改动**：
  - 跟踪 provider model 迁移版本，确保新增的默认模型只注入一次。
  - 保留用户在迁移后因自定义需要而删除的 provider model，避免应用重启后再次出现。
  - 新增所有受影响 provider 的回归测试。
- **影响**: 修复配置迁移时用户自定义内容被覆盖的问题，提高配置管理的可靠性和用户控制权。

**项目向前迈进**：这两个 PR 聚焦于**协同数据防护**与**配置持久化**，属于基础设施层面的改进，为后续功能迭代打下更稳定的基础。

---

## 🔥 社区热点

### #1509 — `skills文件长时间生成阻塞无法感知，中间态过程无展示`
- **作者**: jimmy-xz | 创建: 2026-04-07 | 更新: 2026-06-07 | 💬 评论: 2 | 👍: 0
- **链接**: [Issue #1509](https://github.com/netease-youdao/LobsterAI/issues/1509)
- **分析**：这是过去24小时内**评论最多的 issue**（2条）。用户的核心诉求是技能生成过程缺乏中间状态反馈，导致无法判断是否卡死；同时同一模型在不同产品（OpenClaw vs LobsterAI）中对提示的理解出现偏差，降低了信任感。该 issue 反映了用户对**透明度和一致性的强烈需求**，尤其在复杂任务如 skill 编排中。

### #2121（New） — 重复输出是否造成 token 浪费
- **作者**: nbjoe | 创建: 2026-06-07 | 更新: 2026-06-07 | 💬 评论: 0 | 👍: 0
- **链接**: [Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121)
- **分析**：作为**今日唯一新开 issue**，用户展示截图中 AI 重复输出大量文本，怀疑浪费 token。这可能是 **Claw 或策略层问题**，但尚未确认。该问题反映出用户对 token 成本的敏感度，是典型的生产力场景痛点。

---

## 🐛 Bug 与稳定性

以下为过去24小时内**处于“活跃”状态（有新活动）的 Bug issue**。其中大部分为 2026-04-07 创建、今日遭遇 stale 标记，但**仍未获得修复 PR**。

| 严重程度 | Issue # | 标题 | 影响 | 是否有 Fix PR |
|----------|---------|------|------|---------------|
| 🔴 严重 | #1500 | [禁用技能后仍保留在activeSkillIds中，对话中继续被调用](https://github.com/netease-youdao/LobsterAI/issues/1500) | 功能逻辑错误：禁用技能不生效，可能导致意外调用 | 无 |
| 🔴 严重 | #1516 | [关闭Settings面板时未取消GitHub Copilot OAuth轮询，认证成功后Token静默丢失](https://github.com/netease-youdao/LobsterAI/issues/1516) | 安全/数据丢失：用户完成授权后 token 未被正确保存 | 无 |
| 🟡 中等 | #1502 | [Agent设置面板保存后当前会话activeSkillIds未同步](https://github.com/netease-youdao/LobsterAI/issues/1502) | 配置不同步，用户需切换 Agent 才能生效，影响体验 | 无 |
| 🟡 中等 | #1504 | [设置-IM机器人，popo的AES Key没有进行必填校验](https://github.com/netease-youdao/LobsterAI/issues/1504) | 缺少输入校验，可能导致配置无效 | 无 |
| 🟡 中等 | #1506 | [定时任务选择IM通知频道后未选会话即可提交，运行时静默失败](https://github.com/netease-youdao/LobsterAI/issues/1506) | 定时任务功能可靠性不足，通知丢失无提示 | 无 |
| 🟡 中等 | #1512 | [QQ Bot群组白名单设置缺少添加输入框](https://github.com/netease-youdao/LobsterAI/issues/1512) | UI 缺陷导致白名单功能完全不可用 | 无 |
| 🟢 轻微 | #1513 | [【声明条款】内容规范不统一](https://github.com/netease-youdao/LobsterAI/issues/1513) | 展示级问题，影响合规与观感 | 无 |
| 🔵 待确认 | #2121 | [重复输出大量文字，疑似Bug](https://github.com/netease-youdao/LobsterAI/issues/2121) | 用户怀疑 token 浪费，可能需要进一步排查 | 无（新报） |

**总结**：7 个活跃 Bug 均未在今日获得修复，且大部分已积压 2 个月。其中 #1500、#1516 影响核心体验，建议优先排查。

---

## 💡 功能请求与路线图信号

以下为今日有更新的功能改进型 issue，主要来自用户 `MaoQianTu`。这些需求高度集中在**会话管理效率与信息组织**上，可能成为未来版本的重要方向。

| Issue # | 标题 | 核心价值 | 路线图信号 |
|---------|------|----------|------------|
| #1525 | [会话列表缺少颜色标注功能](https://github.com/netease-youdao/LobsterAI/issues/1525) | 通过颜色快速区分会话（如工作/个人） | 高：类似 VS Code/Notion 颜色的经典设计，提升大量会话的检索效率 |
| #1528 | [批量模式仅支持删除操作，无法导出选中的多个会话](https://github.com/netease-youdao/LobsterAI/issues/1528) | 数据备份与迁移的基本能力 | 中：用户跨设备、团队共享场景刚需 |
| #1532 | [设置页面缺少本地会话使用统计](https://github.com/netease-youdao/LobsterAI/issues/1532) | 通过统计了解自身使用模式 | 低～中：桌面应用常见功能，提升用户粘性 |
| #1537 | [长会话中无法标记重要的AI回复消息](https://github.com/netease-youdao/LobsterAI/issues/1537) | 信息回溯与知识管理 | 高：长对话场景高频需求，类似“书签” |
| #1541 | [会话列表缺少标签分类和筛选功能](https://github.com/netease-youdao/LobsterAI/issues/1541) | 多维度会话组织 | 高：标签系统是内容管理的基础，将线性列表升级为分类体系 |

**判断**：目前没有直接针对这些功能的 PR 被合并，但 #1525、#1537、#1541 在社区中呼声较高（均由同一作者系统提出），且实现思路清晰，建议在下一个里程碑中作为候选考虑。若与已有指标如 `activeSkillIds`、`AgentSettingsPanel` 的改进结合，可显著提升重度用户的生产力。

---

## 📣 用户反馈摘要

从今日活动的 Issue 评论与描述中提取真实用户声音：

> *“同样的提示词给到 Openclaw 里相同的模型，就能很好的理解和生成我想要的 skills”*  
> — [#1509](https://github.com/netease-youdao/LobsterAI/issues/1509) 用户 jimmy-xz，对模型一致性的失望

> *“禁用技能后仍然被注入到对话提示词中”*  
> — [#1500](https://github.com/netease-youdao/LobsterAI/issues/1500) 用户 MaoQianTu，配置与预期不一致

> *“会话选择器显示无可选会话……直接提交，任务创建成功，但运行时 IM 通知不送达，无任何错误提示”*  
> — [#1506](https://github.com/netease-youdao/LobsterAI/issues/1506) 用户 MaoQianTu，功能静默失败让人困惑

> *“重复输出的文字是不是在大量吃我的 token，造成 token 浪费? 是 claw 的问题吗，该如何解决？”*  
> — [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) 用户 nbjoe，对 token 消耗的担忧

**共性**：用户普遍面临**反馈不足、配置不同步、静默错误、不一致体验**等问题，这些直接影响对产品的信任感。

---

## 📋 待处理积压（长期未响应的重要 Issue/PR）

**⚠️ 重点积压（创建超过 2 个月，今被标记 stale）**  
以下 Issue 自 2026-04-07 创建至今未有进展，部分涉及核心功能，维护者可参考：

| Issue # | 标题 | 类型 | 严重度 | 积压时间 |
|---------|------|------|--------|----------|
| #1500 | [禁用技能后仍保留在activeSkillIds中](https://github.com/netease-youdao/LobsterAI/issues/1500) | Bug | 🔴 严重 | 2个月 |
| #1502 | [Agent设置面板保存后activeSkillIds未同步](https://github.com/netease-youdao/LobsterAI/issues/1502) | Bug | 🟡 中等 | 2个月 |
| #1504 | [popo的AES Key无必填校验](https://github.com/netease-youdao/LobsterAI/issues/1504) | Bug | 🟡 中等 | 2个月 |
| #1506 | [定时任务静默失败](https://github.com/netease-youdao/LobsterAI/issues/1506) | Bug | 🟡 中等 | 2个月 |
| #1516 | [GitHub Copilot OAuth Token静默丢失](https://github.com/netease-youdao/LobsterAI/issues/1516) | Bug | 🔴 严重 | 2个月 |
| #1509 | [skills生成阻塞无反馈](https://github.com/netease-youdao/LobsterAI/issues/1509) | Bug / 改进 | 🟡 中等 | 2个月 |
| #1525 | [会话颜色标注](https://github.com/netease-youdao/LobsterAI/issues/1525) | Feature | 🟢 需求 | 2个月 |
| #1537 | [消息书签功能](https://github.com/netease-youdao/LobsterAI/issues/1537) | Feature | 🟢 需求 | 2个月 |
| #1541 | [标签分类和筛选](https://github.com/netease-youdao/LobsterAI/issues/1541) | Feature | 🟢 需求 | 2个月 |

**建议**：优先处理 #1500、#1516 等影响核心逻辑和安全性的 Bug；其余功能型需求可在后续版本规划中考虑。

---

*本日报由 AI 自动生成，基于 GitHub 公开数据，仅供参考。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-06-08

**报告周期：** 2026-06-07 ~ 2026-06-08（数据来源于 GitHub 公开活动）

---

## 1. 今日速览

过去 24 小时内，Moltis 项目未合并任何 Pull Request，也没有发布新版本，整体活跃度较低。核心动态为一则功能请求（Issue #1107）的更新，反映了用户在移动端 Web UI 使用场景中的真实痛点。当前代码库保持稳定，项目可能处于迭代规划间歇期或为下一阶段开发蓄力。

## 2. 版本发布

过去 24 小时内无新版本发布。

## 3. 项目进展

过去 24 小时内无 Pull Request 被合并或关闭，代码仓库状态平稳，未引入新功能或修复。

## 4. 社区热点

- **热点议题**：移动端 Web UI 多行文本输入支持缺失
- **详情**：今日社区唯一活跃的讨论集中在 **[Issue #1107](https://github.com/moltis-org/moltis/issues/1107)**「[Feature]: Multiline text input in the mobile web UI」。该 Issue 由用户 IlyaBizyaev 创建于 6 月 5 日，于昨日（6 月 7 日）更新，目前有 1 条评论。
- **诉求分析**：该 Issue 表明用户在使用手机浏览器访问 Moltis Web 界面时，发现输入框仅支持单行输入（或回车被直接绑定为发送），无法换行输入复杂指令或粘贴多段文本。在多模态与长上下文 AI 交互日益频繁的今天，这是影响移动端核心体验的短板。虽然暂未产生大量社区反应（👍: 0），但它精准指向 UX 基本可用性，是当前社区最明确的关注焦点。

**链接**：[https://github.com/moltis-org/moltis/issues/1107](https://github.com/moltis-org/moltis/issues/1107)

## 5. Bug 与稳定性

今日无新增 Bug、崩溃或回归问题报告。项目中当前暂无严重影响核心功能的稳定性缺陷处于公开状态。

## 6. 功能请求与路线图信号

- **焦点功能**：移动端 Web UI 多行文本输入 ([Issue #1107](https://github.com/moltis-org/moltis/issues/1107))
- **路线图推断**：作为 AI 对话助手基础交互的一部分，多行输入对于信息密集型对话（如上传长文本、撰写复杂 prompt）不可或缺。考虑到暂无关联 PR，该功能尚未进入开发阶段，但其优先级在易用性维度中较高。预期维护者将在下一个小版本迭代中评估实现方案（如将 `input` 替换为可缩放的 `textarea`，或引入「回车发送/Shift+回车换行」的双快捷键逻辑）。

## 7. 用户反馈摘要

- **痛点总结**：移动端 Web 界面存在基本输入功能受限问题。用户在手机端进行长文本编辑、多段内容粘贴或复杂上下文输入时，无法有效换行组织内容，用户体验受阻。
- **提交细节**：值得留意的是，Isssue 提交者 IlyaBizyaev 在 Issue 预检清单中 **未勾选** “包含了聊天会话上下文” 的选项。这进一步佐证该反馈并非源于特定对话 Bug，而是一则独立的、普遍性的 UI/UX 诉求。
- **用户预期**：用户期待 Moltis 在移动 Web 场景下能达到与桌面端或原生 App 同等的输入交互水准。

## 8. 待处理积压

- **当前积压状况**：项目目前无长期未响应的重要积压 Issue。唯一的活跃 Issue [#1107](https://github.com/moltis-org/moltis/issues/1107) 创建于 6 月 5 日，且于 6 月 7 日刚被更新，属于正常的新需求流转周期。
- **维护建议**：建议维护者在下一个规划周期中注意回复该 Issue，通过添加 `help wanted` / `good first issue` 或指定里程碑来向社区传递明确的采纳信号，同时可安抚用户的初步期待。

---

**总结：** 今日 Moltis 项目处于低活跃维护状态，无新发布与代码合并。社区关注度唯一集中在移动端输入体验的缺口上，该需求具有切实的可用性价值，建议开发团队予以优先评估。项目整体健康度良好，无明显阻塞项与稳定性隐患。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 (2026-06-08)

## 1. 今日速览

今日项目保持高活跃度，24 小时内共产生 22 条 Issue 更新（其中新开/活跃 16 条，已关闭 6 条）和 10 条 PR 更新（待合并 7 条，已合并/关闭 3 条），无新版本发布。社区贡献积极，数个影响企业微信（Yuanbao）渠道的关键 Bug 通过 PR 得到修复并合并。同时，关于后端从 AgentScope 1.x 迁移至 2.0 的讨论热度持续，插件扩展基础设施的草案 PR 也进入初次提交阶段。项目整体处于活跃开发状态，但伴有多项回归问题，稳定性需重点关注。

## 2. 版本发布

无（截至今日未发布新版本）。

## 3. 项目进展

今日合并/关闭了 3 个 PR，均为关键修复或基础设施尝试：

- **修复 Yuanbao 流式回复丢失** — [PR #4982](https://github.com/agentscope-ai/QwenPaw/pull/4982)  
  修复企业微信渠道在启用流式回复时，回复被静默丢弃的问题。通过重写 `on_streaming_end` 和 `_on_stream_msg_end` 逻辑，确保非流式路径也能正确发送累积文本。

- **修复 AuthBindRsp 缺少 connectId 字段** — [PR #4983](https://github.com/agentscope-ai/QwenPaw/pull/4983)  
  补充 `AuthBindRsp` 的 `connectId` 字段定义，使连接追踪功能能够正常工作。

- **插件扩展基础设施（草案）** — [PR #4996](https://github.com/agentscope-ai/QwenPaw/pull/4996)  
  因与后续 PR 内容重复而关闭，但其设计思路已转移至 [#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997) 和 [#4998](https://github.com/agentscope-ai/QwenPaw/pull/4998) 继续开发。

此外，以下重要 PR 仍在开放或审查中：

- **修复配置损坏导致 Agent 崩溃** — [PR #5000](https://github.com/agentscope-ai/QwenPaw/pull/5000)  
  针对 [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) 提取 `_safe_json_loads` 至共享工具，防止 JSON 损坏时整个会话崩溃。

- **新增后端模块测试覆盖** — [PR #4973](https://github.com/agentscope-ai/QwenPaw/pull/4973)  
  首次贡献者提交 129 个测试用例，覆盖 `local_models`、`providers`、`tunnel`、`utils` 等模块。

- **渠道渲染器保留工具输出** — [PR #4995](https://github.com/agentscope-ai/QwenPaw/pull/4995)  
  修复当 `show_tool_details` 关闭时，工具输出附件和元数据丢失的问题。

总体来看，项目在企业微信渠道稳定性、测试体系建设和核心错误容忍度方面均取得实质进展。

## 4. 社区热点

今日讨论最活跃的 Issue 和 PR 集中在以下方向：

- **AgentScope 2.0 迁移讨论** — [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)  
  获得 2 个 👍 和 6 条评论。由仓库所有者发起，计划将后端依赖从 AgentScope 1.x 升级至 2.0，涉及全新架构和 API 变更。社区积极参与讨论，关注意义深远的技术栈切换。

- **自研插件在 WeCom 渠道不工作** — [#4585](https://github.com/agentscope-ai/QwenPaw/issues/4585)  
  5 条评论，持续两周仍活跃。用户反馈自研插件在桌面端正常，但企业微信渠道无法自动发现和调用，反映出跨渠道功能一致性的显著缺口。

- **Yuanbao 渠道系列 Bug 报告** — [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976)、[#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977)、[#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978)、[#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979)、[#4980](https://github.com/agentscope-ai/QwenPaw/issues/4980)  
  贡献者 ABAC-123456 在 6 月 5 日连续提交 5 个 Issue，覆盖 Proto 文件缺失、兼容性错误、字段缺失、流式回复丢失等问题。清晰的报告直接推动了 [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) 和 [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) 两个修复 PR 的快速合并，是社区协作的典型案例。

这些热点的核心诉求可归纳为：**渠道可靠性**（WeCom/Yuanbao）、**架构现代化**（AgentScope 2.0）以及**稳定的基础设施**（配置损坏防御）。

## 5. Bug 与稳定性

今日报告的 Bug 及修复状态按严重程度排列如下：

| 严重程度 | Issue | 描述 | 状态 |
|----------|-------|------|------|
| 🔴 严重 | [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) | `loop_config.json` / `prd.json` 损坏导致整个 Agent 会话崩溃，所有渠道不可用 | 已提供 fix PR [#5000](https://github.com/agentscope-ai/QwenPaw/pull/5000) |
| 🔴 严重 | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | v1.1.9/v1.1.10 使用本地部署模型（千问3.6-27B）时对话无响应（回归） | 未修复，无指派 |
| 🔴 严重 | [#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003) | 使用阿里 coding plan 模型时一直卡住 | 未修复 |
| 🟡 中等 | [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) | v1.1.10 Coding Mode 下会话切换失败（回归） | 未修复 |
| 🟡 中等 | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | Session 文件名重复拼接导致 Windows 路径超限 | 未修复 |
| 🟡 中等 | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | 图片预览放大后拖动异常抖动 | 未修复 |
| 🟡 中等 | [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) | 企业微信工具调用后信息关闭返回错误提示 | 未修复 |
| 🟡 中等 | [#4587](https://github.com/agentscope-ai/QwenPaw/issues/4587) | 退出时留下孤儿进程 | 已关闭，但修复结论不清晰 |
| 🟢 低度 | [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976)~[#4980](https://github.com/agentscope-ai/QwenPaw/issues/4980) | Yuanbao 渠道 Proto 文件缺失、兼容性等系列问题 | 已通过 [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982)、[#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) 修复 |
| 🟢 低度 | [#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977) | Protobuf 兼容性（`including_default_value_fields` 参数） | 已关闭 |

**重点关注**：配置损坏崩溃已有 PR 修复，但 #4989、#4987、#4988 等回归问题仍未得到处理，可能影响大量用户升级意愿。

## 6. 功能请求与路线图信号

今日收集到以下新功能需求：

- **独立视觉模型配置（Visual Model Fallback）** — [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992)  
  支持在主模型为纯文本时自动调用专用视觉模型处理图片，提升多模态使用灵活性。

- **记忆系统自进化** — [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994)  
  要求吸收主流 Agent 分层记忆系统框架，增强记忆能力。

- **会话按标题筛选** — [#4999](https://github.com/agentscope-ai/QwenPaw/issues/4999)  
  改善大量会话下的管理体验。

- **Shell 实时交互信息显示** — [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986)  
  参考 Cursor/Workbuddy，要求在执行 Shell 或写文件时实时反馈，避免卡住假象。

- **审批命令换行显示** — [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985)  
  删除文件等长命令需手动拖动查看，交互不友好，要求自动换行。

- **9router 网络支持** — [#5001](https://github.com/agentscope-ai/QwenPaw/issues/5001)  
  特定网络环境下无法连接模型的问题。

**路线图信号**：  
- **AgentScope 2.0 迁移** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)) 作为 Breaking Change 提案，将决定后续后端架构方向。  
- **插件扩展基础设施**已在 [#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997) 和 [#4998](https://github.com/agentscope-ai/QwenPaw/pull/4998) 以 WIP 形式提交（分别面向 main 和 dev/agentscope2.0 分支），包含菜单注册、路由、UI 插槽、聊天扩展 API 等，预示着可插拔前端框架即将成型。  
- **独立视觉模型** 和 **记忆系统进化** 等社区呼声较高的功能有可能在未来版本中优先实现。

## 7. 用户反馈摘要

从 Issue 评论与描述中提炼的真实用户声音：

- **“同一个插件，桌面端能用，企业微信就不能用，体验割裂。”** — [#4585](https://github.com/agentscope-ai/QwenPaw/issues/4585) 用户反映自研插件在渠道间行为不一致。
- **“配置文件一旦写坏，整个 Agent 就废了，Telegram 和网页都用不了。”** — [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) 用户对零容错配置设计的强烈不满。
- **“升到 1.1.10 后，本地的千问 3.6-27B 就再也不回话了，旧版本没问题。”** — [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) 用户明确指出回归，升级受阻。
- **“Windows 上文件名太长直接报路径超限，想删都没法删。”** — [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) Windows 用户受困于 Session 文件名重复拼接。
- **“Coding Mode 切换会话总是失败，只能重启。”** — [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) 代码模式下的用户工作流被阻断。
- **“企业微信里工具调用完就‘抱歉，无法回答’，用户一脸懵。”** — [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) 渠道反馈机制不透明，导致用户困惑。
- **“放大图片拖动时屏幕狂抖，根本没法用。”** — [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) 前端交互细节影响日常使用体验。
- **“执行 Shell 命令没反应，不知道是在运行还是卡死了。”** — [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) 缺乏实时反馈导致信任度下降。

这些反馈集中表明用户对 **渠道功能一致性**、**关键路径容错性** 和 **日常交互体验** 有较高期望，而当前版本在这些方面仍有明显短板。

## 8. 待处理积压

以下 Issue 和 PR 长期未获得充分响应或合并，建议维护者优先关注：

| 项目 | 创建时间 | 状态 | 备注 |
|------|----------|------|------|
| [#4585](https://github.com/agentscope-ai/QwenPaw/issues/4585) – 自研插件在 WeCom 渠道不自动发现 | 2026-05-21 | 开放，有 5 条评论 | 已持续 18 天，社区期待明确 roadmap |
| [#4587](https://github.com/agentscope-ai/QwenPaw/issues/4587) – 退出留下孤儿进程 | 2026-05-21 | 已关闭，但未说明修复版本 | 关闭结论模糊，建议补充状态 |
| [#4949](https://github.com/agentscope-ai/QwenPaw/pull/4949) – ACP 服务器扩展 | 2026-06-03 | Under Review | 等待审查和合并超过 5 天 |
| [#4973](https://github.com/agentscope-ai/QwenPaw/pull/4973) – 新增 129 个单元测试 | 2026-06-05 | Open | 显著提升测试覆盖率，应尽快 Code Review |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) – 本地模型无响应（回归） | 2026-06-06 | 开放，无指派 | 影响用户升级，建议紧急排查 |
| [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) – Coding Mode 会话切换失败（回归） | 2026-06-06 | 开放，无指派 | 阻碍代码工作流，需修复 |

其中 **#4989 和 #4987** 是 v1.1.10 引入的回归问题，用户反馈强烈，应列为下一补丁版本的最高优先级。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，请查收基于所提供数据的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 (2026-06-08)

## 1. 今日速览

ZeroClaw 项目在过去 24 小时内保持了极高的活跃度，共计有 **50 个 Issues** 和 **50 个 Pull Requests** 获得了更新。尽管今日无新版本发布，但项目在稳定性与功能开发上双线并进：多项阻塞级 Bug（如 Web 面板无法访问 #4866）已成功关闭，同时针对 **v0.8.0** 的版本发布准备工作已启动（#7364）。社区讨论热度集中在 Token 优化与多智能体架构上，整体项目健康度良好，正从密集的功能开发期向发布稳定期过渡。

## 2. 版本发布

*(今日无新版本发布)*

## 3. 项目进展

过去 24 小时共关闭 **18 个 Issues** 和 **12 个 PRs**，项目在修复关键 Bug 和推进核心功能方面取得了显著进展。

**主要关闭 Issues（稳定性胜利）：**
- **[Bug] Web dashboard is still not available** ([#4866](zeroclaw-labs/zeroclaw Issue #4866))：严重等级 S1，长期困扰用户的 Web 面板构建问题已修复。
- **[Bug] context_compression not triggered in daemon mode** ([#4880](zeroclaw-labs/zeroclaw Issue #4880))：通道模式下的上下文压缩失效问题解决。
- **[Bug] Fallback provider chain ignores [providers.X] config** ([#5803](zeroclaw-labs/zeroclaw Issue #5803))：备份 Provider 链路忽略配置文件的 Bug 已修复。
- **[Bug] Delegate agents ignore [skills].prompt_injection_mode** ([#5155](zeroclaw-labs/zeroclaw Issue #5155))：代理任务忽略注入模式的阻断性问题已解决。

**主要合并/关闭 PR（功能推进）：**
- **TUI 重大更新**：一系列提升终端用户体验的 PR 已合并，包括：
    - **出站消息队列** ([#7190](zeroclaw-labs/zeroclaw PR #7190))：支持在 Agent 响应时提前输入，提升交互流畅度。
    - **模型/Provider 实时切换器** ([#7209](zeroclaw-labs/zeroclaw PR #7209))：允许在会话中动态切换模型和 Provider。
    - **Provider 回退链** ([#7178](zeroclaw-labs/zeroclaw PR #7178))：实现了可自定义的按 Provider/别名回退机制。
    - **主题增强** ([#7249](zeroclaw-labs/zeroclaw PR #7249))：改进了颜色回退方案、预设和深度控制。
- **Quickstart 修复** ([#7360](zeroclaw-labs/zeroclaw PR #7360))：修复了快速入门面板的模态窗口尺寸计算问题。

**前瞻信号：**
- **发布分支已建立** ([#7364](zeroclaw-labs/zeroclaw PR #7364))：`v0.8.0` 的发布准备流程已启动，标志着主干开发进入锁定阶段。

## 4. 社区热点

过去 24 小时的讨论高度集中在以下议题：

1.  **Web 面板不可用（已修复）**：[#4866](zeroclaw-labs/zeroclaw Issue #4866)（28条评论）
    - 这是社区过去数月最大的痛点，用户抱怨该问题“跨越了多个版本”仍未解决。该 Issue 的关闭是今日社区最重大的利好。
2.  **Token 消耗最小化（技能编译）**：[#5146](zeroclaw-labs/zeroclaw Issue #5146)（9条评论）
    - 用户 jonsmirl 详细分析了当前全量注入 SKILL.md 带来的浪费。通过编译技能来减少 Token 消耗是当前社区功能请求的核心主题之一。
3.  **多智能体路由**：[#2767](zeroclaw-labs/zeroclaw Issue #2767)（6条评论，9个 👍）
    - 获得了最高数量的点赞，代表着社区对企业级多实例部署的强烈需求。
4.  **A2A 协议支持**：[#3566](zeroclaw-labs/zeroclaw Issue #3566)（6条评论，7个 👍）
    - 开放 Agent 间通信协议的呼声极高，社区不希望 ZeroClaw 成为信息孤岛。
5.  **Logo 设计征集**：[#4710](zeroclaw-labs/zeroclaw Issue #4710)（11条评论）
    - 表明社区成员对项目品牌形象的参与热情。

## 5. Bug 与稳定性

今日未出现新的严重崩溃，但几个已知的棘手问题仍悬而未决：

- **严重风险（S0 - 数据丢失）**：**file_write 工具静默失败** ([#4627](zeroclaw-labs/zeroclaw Issue #4627))
  - Agent 返回写入成功，但在宿主机上完全找不到文件。该问题自 2026-03-25 起开放至今，标记为 `in-progress`，但暂无关联的修复 PR。**这是当前项目面临的最严重风险。**
- **阻塞问题（S1 - 工作流阻断）**：**Gemini CLI OAuth 失效** ([#4879](zeroclaw-labs/zeroclaw Issue #4879))
  - 用户认证成功后立即遭遇限流错误。该项目自 2026-03-28 起开放，仍在处理中。
- **回归问题修复**：
    - **[#7343](zeroclaw-labs/zeroclaw PR #7343)**：修复了 Bedrock Qwen 模型对话 ID 未重置导致 Web 控制台报错的问题。
    - **[#7366](zeroclaw-labs/zeroclaw PR #7366)**：紧急修复 [#7190](zeroclaw-labs/zeroclaw PR #7190) 合入后导致的 `zerocode` TUI 输入阻塞回归问题。
    - **[#7243](zeroclaw-labs/zeroclaw PR #7243)**：修复了 Token 轮换时未撤销旧 Token 的安全漏洞。
- **次要问题**：日志写入 stdout 而非 stderr ([#4721](zeroclaw-labs/zeroclaw Issue #4721)) 仍在待办中，影响命令行管道使用。

## 6. 功能请求与路线图信号

- **架构重心：多智能体与联邦**
  - 多智能体路由 (#2767, 9👍) 和 A2A 协议支持 (#3566, 7👍) 是当前社区最渴望的功能。
  - **今日新 PR**：[#7367](zeroclaw-labs/zeroclaw PR #7367) 实现了 Webhook 的按别名路由，直接响应了用户对多实例通道路由的诉求 (#6312)。
- **成本控制：技能编译** ([#5146](zeroclaw-labs/zeroclaw Issue #5146))
  - 这是继多智能体后，社区最希望看到的功能。用户希望在保留 Agent 能力的同时，大幅降低云端 LLM 的调用成本。
- **企业级安全特性**：
  - RFC [#6293](zeroclaw-labs/zeroclaw Issue #6293) 提议的隔离执行模式（Air-gapped）、沙箱强化 (#5127) 和 Webhook 转换 (#2467) 等，标志着社区对企业部署场景的关注。
- **Provider 生态大扩展**：
  - **[#7260](zeroclaw-labs/zeroclaw PR #7260)**（开放中）引入了包括 morph, github_models, upstage 等在内的 **7 个全新 OpenAI 兼容 Provider**，大幅降低用户的 API 选择门槛。
- **Memory 架构重构**：
  - **[#7234](zeroclaw-labs/zeroclaw PR #7234)**（开放中）正在进行将网关和通道的持久化逻辑迁移至统一的 `MemoryStrategy` 接口，这是一个重要的内部架构优化。

## 7. 用户反馈摘要

- **核心痛点**：
  - **入门门槛高**：缺少“完全版” Docker 镜像 (#3642)，非技术用户配置困难。
  - **通道兼容性**：找不到期待的 OneBot/NapCat 通道 (#2503)，导致无法接入 QQ。
  - **成本与效率**：每次查询都要加载完整的、冗长的技能文件，用户形容为“昂贵且愚蠢”的设计 (#5146)。
  - **飞书集成异常**：飞书通道默认调用 LLM 而非 Agent，导致无法使用工具调用等核心功能 (#4873)。
- **质量认可**：
  - 社区对多智能体、A2A 等前瞻性功能的讨论热情高涨，表明用户群多为技术型深度用户，认可项目的技术方向。
  - 尽管面临一些 Bug，用户仍在积极提交 RFC 和完善文档（如 #7184 翻译文件结构设计，#6760 Docker 文档更新），社区自愈力强。

## 8. 待处理积压

以下 Issue/PR 长期未得到关键性推进，需维护者重点关注：

1.  **【极高风险】file_write 数据丢失** ([#4627](zeroclaw-labs/zeroclaw Issue #4627))
  - **状态**：已开放 2.5 个月（S0 级）。仅有 `in-progress` 标签，无实质性修复 PR 关联。该 Bug 摧毁用户对 Agent 文件操作的信任。
2.  **【高阻断】Gemini OAuth 无法使用** ([#4879](zeroclaw-labs/zeroclaw Issue #4879))
  - **状态**：已开放 2 个月（S1 级）。大量 Google 生态用户被拒之门外，急需排查。
3.  **【入门门槛】提供包含全部功能的 Docker 镜像** ([#3642](zeroclaw-labs/zeroclaw Issue #3642))
  - **状态**：已开放 3 个月，标记为 `blocked`。该需求是降低新用户流失率的关键。
4.  **【功能请求】Webhook 转换** ([#2467](zeroclaw-labs/zeroclaw Issue #2467))
  - **状态**：已开放 3 个月，标记为 `blocked`。缺乏针对通用 Webhook 发送者的灵活性。
5.  **【待操作】Web UI 集成类别使用英文枚举值** ([#6490](zeroclaw-labs/zeroclaw PR #6490))
  - **状态**：PR 已提交，但标记为 `needs-author-action`。作者需根据反馈完成代码以美化 Web UI 的集成页面。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*