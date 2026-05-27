# OpenClaw 生态日报 2026-05-27

> Issues: 379 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-27 03:30 UTC

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

# OpenClaw 项目动态日报 — 2026-05-27

## 1. 今日速览

OpenClaw 项目在 2026-05-27 呈现**极高活跃度与核心深度震荡并存**的状态。过去 24 小时内，社区提交了 **379 条 Issue**（新开/活跃 168 条，关闭 211 条）和 **500 条 PR**（待合并 251 条，已合并/关闭 249 条），并发布了两个 Beta 版本。项目正处于 v2026.5.x Beta 周期的密集迭代期：一方面架构重构取得重大进展（Pi 运行时内化、SQLite 迁移持续推进），另一方面大量 P1 回归问题（事件循环饥饿、子代理静默丢消息、Codex 运行时冲突）集中爆发。社区热情高涨但 Beta 稳定性方差较大，**整体呈现"高活力、高风险"的震荡特征**。

---

## 2. 版本发布

### v2026.5.26-beta.1

- **性能大修：** 可见回复交付与后台慢速工作流分离，减少用户等待时间；命令/模型/插件元数据在热路径上复用；Gateway 启动优化，跳过重复的插件/频道/会话/用量/文件系统扫描，显著提升启动速度。
- **迁移注意：** 无明确破坏性变更记录。建议生产环境用户在升级后运行 `openclaw doctor --fix`。
- [查看发布详情](https://github.com/openclaw/openclaw/releases/tag/v2026.5.26-beta.1)

### v2026.5.25-beta.1

- **iMessage 修复：** 将当前 Channel/Account 入站附件根路径链接到图像工具，使 `~/Library/Messages/Attachments` 下的附件能被正确读取，不会因入站策略而被拒绝。
- **影响范围：** 仅限 macOS iMessage 频道。
- [查看发布详情](https://github.com/openclaw/openclaw/releases/tag/v2026.5.25-beta.1)

---

## 3. 项目进展

### 🏗 架构突破（推进中）

- **PR [#85341](https://github.com/openclaw/openclaw/pull/85341)** `steipete` — 内化 Pi 代理运行时：移除旧 Pi 架构，将代理执行、模型/通道路由集成进 OpenClaw 自有核心/插件/SDK 体系。
- **PR [#81402](https://github.com/openclaw/openclaw/pull/81402)** `steipete` — 运行时状态迁移至 SQLite：从零散的 JSON/JSONL/文件锁/缓存存储转向统一类型化 SQLite 布局，彻底解决状态一致性问题。

### ✅ 稳定性修复合并

- **PR [#87131](https://github.com/openclaw/openclaw/pull/87131)** `steipete` — 修复本地审批解析令牌转发逻辑，确保安全性遵循 Gateway URL 来源而非仅仅是否 loopback。
- **PR [#86345](https://github.com/openclaw/openclaw/pull/86345)** `quengh` — 绑定 `memory-core` 索引缓存生命周期，防止长运行 Gateway 中 FD 耗尽。
- **PR [#86939](https://github.com/openclaw/openclaw/pull/86939)** `scotthuang` — 修复 Webchat 运行状态标签卡在 "In progress" 的 UI 竞态问题。
- **PR [#86771](https://github.com/openclaw/openclaw/pull/86771)** `fuller-stack-dev` — 收紧 Discord 审批决议权限，防止越权写入。

### 🆕 新能力/生态扩展

- **PR [#86179](https://github.com/openclaw/openclaw/pull/86179)** `NianJiuZst` — 新增小米 Token Plan 提供商一级支持（中国/欧洲/新加坡区域），完善认证/用量/配置，社区贡献突出，已进入维护者审核阶段。
- **PR [#86164](https://github.com/openclaw/openclaw/pull/86164)** `100yenadmin` — 推进 Channel Broker 第三阶段：官方频道能力矩阵，目标将 Telegram/Discord/Slack/WhatsApp/Signal 等渠道的频繁维护收敛至统一合约层。

### 📈 社区迭代速率

过去 24 小时内，PR 合并/关闭数达 **249 条**，Issue 关闭 **211 条**，说明项目保持高效的交付节奏，接近 1:1 的 Open/Close 比反映团队正在积极清理积压。

---

## 4. 社区热点

### 🏆 最广泛诉求

| # | 标题 | 评论 | 点赞 | 分析 |
|---|------|------|------|------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | **[Lin/win] Clawdbot Apps** | **109** | **77** 持续数月热度第一。社区对桌面平台覆盖的迫切需求未减，是项目扩展用户基数的关键瓶颈。 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent **silently lost** | 18 | 0 | 子代理编排的静默失败机制引发了最深度的技术讨论，被标记为 `🦞 Diamond Lobster`，反映核心架构级痛点。 |
| [#68596](https://github.com/openclaw/openclaw/issues/68596) | **Streaming watchdog** configurable timeout | 14 | 8 | DeepSeek-R1 等长思考模型频繁触发硬编码 30s 看门狗，这是一个高频且实际的体验痛点。 |
| [#81249](https://github.com/openclaw/openclaw/issues/81249) | Local Ollama + proxy (**SSRF**) | 11 | 1 | 安全机制与本地开发工作流的冲突（NO_PROXY 被清除），代表安全灵活性的敏感平衡被突破。 |

### 🔥 高活跃度讨论

- **#76562** — 升级后 CPU 100%，控制面 RPC 极高延迟，11 评论，5 点赞，直接影响升级路径。
- **#86599** — Windows Beta 本地模型阻塞事件循环，11 评论，1 点赞，平台特定稳定性问题。
- **#78016** — Matrix 语音消息不支持，11 评论，1 点赞，渠道完整性问题。
- **#80380** — 适配 Gemini 3.1 Flash-Lite 正式版，10 评论，社区紧跟上游模型更新。

---

## 5. Bug 与稳定性

### 🚨 Beta Blocker / 崩溃级别

| # | 标题 | 状态 | 标签 | 分析 |
|---|------|------|------|------|
| [#86948](https://github.com/openclaw/openclaw/issues/86948) | Codex app-server 静默丢消息 | **CLOSED** | `beta-blocker` `P1` `crash-loop` | OpenAI Responses API 事件交付后 turn 永不解析，被标记为 Beta Blocker，事件循环饱和导致。 |
| [#86509](https://github.com/openclaw/openclaw/issues/86509) | v2026.5.22 **event-loop starvation 回归** | **CLOSED** | `P1` `crash-loop` | 87s 锁阶段 + 31s 循环延迟，用户已回滚到 v2026.5.20 并加入本地禁用列表。 |
| [#86827](https://github.com/openclaw/openclaw/issues/86827) | 群聊会话 stuck `failed` 后**静默丢消息** | **OPEN** | `P1` `message-loss` | AI 回合超时后会话停留在 failed 状态，后续消息全部石沉大海，无任何错误提示。 |
| [#86508](https://github.com/openclaw/openclaw/issues/86508) | Discord `EmbeddedAttemptSessionTakeoverError` | **OPEN** | `P1` `regression` | Session 文件在嵌入式锁释放期间被更改，`doctor --fix` 无效。 |
| [#86613](https://github.com/openclaw/openclaw/issues/86613) | **`memory_search` FD 泄漏** (macOS) | **CLOSED** | `P1` `crash-loop` | 每次调用针对每个 `.md` 文件打开一个 FD 不释放，最终导致 FD 耗尽——已有确定性复现。 |
| [#86354](https://github.com/openclaw/openclaw/issues/86354) | Codex 原生代码模式在 Node.js 网关被禁用 | **CLOSED** | `P1` `session-state` | v2026.5.22 新逻辑导致孤立 session 丢失 exec/read/write/edit 能力。 |

### ⚡ 性能回归 / 异常行为 (P1/P2)

| # | 标题 | 状态 | 标签 | 分析 |
|---|------|------|------|------|
| [#86599](https://github.com/openclaw/openclaw/issues/86599) | Windows Beta 本地模型**阻塞事件循环** | **OPEN** | `P1` `Beta release blocker` | 简单推理请求需 ~4 分钟，Windows 平台首当其冲。 |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) | 升级后 CPU 100% / 控制面 RPC 极高延迟 | **OPEN** | 严重性能回归 | 从 4.24 到 4.29 及 5.2 均受影响，影响面广。 |
| [#85822](https://github.com/openclaw/openclaw/issues/85822) | Discord ~48s **静默延迟** (2026.5.20) | **OPEN** | `P1` `message-loss` | LLM 调用仅需 3-15s，但剩余 ~48s 完全无 trace 日志。 |
| [#84607](https://github.com/openclaw/openclaw/issues/84607) | 主模型 overloaded 时**无自动回退重试** | **CLOSED** | `P1` `message-loss` | Minimax 全链路中断，回退机制缺失。 |
| [#86758](https://github.com/openclaw/openclaw/issues/86758) | Codex 动态工具 RPC 超时 **30s 硬编码** | **CLOSED** | `P1` | 影响 `session_status` 等枚举型 MCP 工具。 |

### 🔒 安全 / 配置

| # | 标题 | 状态 | 标签 | 分析 |
|---|------|------|------|------|
| [#81249](https://github.com/openclaw/openclaw/issues/81249) | SSRF 防御 **忽略 NO_PROXY** | **CLOSED** | `impact:security` | 内部代理系统清空 bypass 变量，导致本地 Ollama 也被路由进代理隧道。 |
| [#83086](https://github.com/openclaw/openclaw/issues/83086) | `max_tokens` **未减已用输入**致 API 拒绝 | **CLOSED** | `regression` | 中等上下文模型（如 262K）被分配满上下文 max_tokens，导致 "too large" 错误。 |

**稳定性判断：** 项目目前处于**架构重构的阵痛期**。大量依赖 `fix-shape-clear` 和 `queueable-fix` 标签的补丁并行推进。建议关键生产环境用户暂缓升级最新 Beta，优先停留在已验证稳定的版本（如 v2026.5.20）。

---

## 6. 功能请求与路线图信号

### 📌 大概率进入下一版本（已有对应 PR 进入审核）

| 请求 | PR / Issue | 状态 | 分析 |
|------|------------|------|------|
| **小米 Token Plan 提供商支持** | [#86179](https://github.com/openclaw/openclaw/pull/86179) | `Ready for maintainer look` | 社区贡献完整，厂商生态继续扩展。 |
| **标准化 exec 审批/自动模式** | [#70543](https://github.com/openclaw/openclaw/pull/70543) | `Ready for maintainer look` | 统一原生、Codex 和 Guardian 的执行策略。 |
| **Channel Broker 官方频道能力矩阵** | [#86164](https://github.com/openclaw/openclaw/pull/86164) | `Ready for maintainer look` | 目标大幅降低多频道维护成本。 |
| **插件审批动作元数据开放** | [#82431](https://github.com/openclaw/openclaw/pull/82431) | `needs proof` | 允许外部 HITL 插件接入现有审批流程。 |

### 🗺️ 长期路线图信号

- **iOS 原生 App 新方向**
  [#85731](https://github.com/openclaw/openclaw/issues/85731) — 官方发布了**设计 UI 截图**，展示 Command/Chat/状态/审批/导航等界面。这标志着移动端体验升级已进入产品设计阶段。
- **Linux/Windows 桌面端**
  [#75](https://github.com/openclaw/openclaw/issues/75) — 虽无对应 PR，但 109 条评论和 77 点赞是社区最强共识。+PR #85341 的架构调整可能为跨平台打包铺路。
- **类型化转录投影 / 子代理可观测性**
  [#79905](https://github.com/openclaw/openclaw/issues/79905) + [#38626](https://github.com/openclaw/openclaw/issues/38626) — 架构成熟度信号，从"能跑"迈向"可观测、可维护"。

### 🔔 社区需求但被标记需产品决策

- **Gemini 3.1 Flash-Lite 适配** ([#80380](https://github.com/openclaw/openclaw/issues/80380)) — Preview 版本即将停用，需尽快切换 GA 模型。
- **Agent 缺乏可靠系统时间源** ([#82968](https://github.com/openclaw/openclaw/issues/82968)) — 限制所有涉及调度/日历的 Agent 能力，基础但长期未被解决。

---

## 7. 用户反馈摘要

### 😔 核心痛点

- **静默失败（Silent Failure）是最大的信任杀手：**
  > "Subagent task orchestration has multiple failure modes where results are silently lost."
  > "The agent gets the audio but doesn't actually hear it — it just makes up a polite reply."

  多条 P1 Issue 指向：子代理超时不告知、会话进入 failed 无声、消息顺滑丢失。用户在无感知的情况下收到虚假回应或零回应。

- **升级即冒险，回滚是常态：**
  > "Rolled back to v2026.5.20 to recover; 5.22 added to local BLOCKED_VERSIONS."

  多名用户明确表示依赖 `npm i -g openclaw@x.x` 降级求生。Beta 版本的稳定性方差严重影响信任度。

- **Windows 平台体验降级明显：**
  > "local model calls block gateway event loop on Windows beta; trivial infer run takes ~4 minutes."

  Windows 用户在这个 Beta 周期明显感觉是"二等公民"，多起严重事件循环饥饿问题集中出现在 Windows 平台。

- **MCP 工具集成困惑：**
  > "MCP tools not injected into subagent sessions — `bundle-mcp` + per-tool subagent allowlist + per-agent allowlist all ignored."

  配置文档齐全但实际行为与预期不一致，用户尝试多种配置路径全部失效，产生极大挫败感。

### 👍 积极信号

- **社区素养高，协作意识强：**
  大量 Issue 附带了 `source-repro` 标签、完整复现步骤、日志分析和 `doctor --fix` 结果。用户自发地帮助核心团队定位极复杂的竞态条件和 FD 泄漏。

- **用户群体具有前瞻性：**
  使用 DeepSeek-R1、Kimi K2.5 等长思考模型，部署大规模 Workspace（数万的 `.md` 文件），编排多层子代理网络。社区正在推动 OpenClaw 性能边界的扩展，这反过来也是项目成长的动力。

---

## 8. 待处理积压

以下 Issue/PR 已开放较长时间，或具有重要架构价值但长期缺乏维护者回应：

| # | 标题 | 创建 | 标签 | 需关注原因 |
|---|------|------|------|-----------|
| [#38626](https://github.com/openclaw/openclaw/issues/38626) | Subagent lifecycle observability + async supervision controls | 2026-03-07 | `P2` `needs-maintainer-review` `needs-product-decision` | 这是 #44925（子代理静默丢失）的根因之一。解决此 Issue 可能系统性消灭一类 Bug。 |
| [#45952](https://github.com/openclaw/openclaw/issues/45952) | Webchat 消息在 WS 重连时丢失 | 2026-03-14 | `P1` `🦞 Diamond Lobster` | 影响所有 Web 用户的核心交互通路，长时间无合并动作，可能涉及复杂前端状态管理。 |
| [#65564](https://github.com/openclaw/openclaw/issues/65564) | Heartbeat isolatedSession 换 sessionId 但重用旧 transcript | 2026-04-12 | `P2` `🦞 Diamond Lobster` | 看似矛盾的 Bug，心跳每次轮换 ID 但文件不刷新，导致无限制上下文膨胀。 |
| [#67915](https://github.com/openclaw/openclaw/issues/67915) | 本地附件 "Unavailable" 尽管配置正确 | 2026-04-17 | `P2` `🦞 Diamond Lobster` | 直接破坏 "本地媒资/图像生成" 工作流的体验。 |
| [#82968](https://github.com/openclaw/openclaw/issues/82968) | Agent 缺乏可靠的**系统时间源** | 2026-05-17 | `P2` `needs-maintainer-review` | 架构级基础缺陷，限制所有涉及定时/日历的 Agent 能力，长期积压。 |
| [#83425](https://github.com/openclaw/openclaw/issues/83425) | **xAI OAuth** `redirect_uri does not match` | 2026-05-18 | `P1`（未经正式标记但影响新增供应商接入） | 阻塞新用户的 xAI 供应商接入路径。 |

---

*报告编制时间：2026-05-27  |  数据来源：[OpenClaw / openclaw](https://github.com/openclaw/openclaw)*

---

## 横向生态对比

# AI智能体与个人AI助手开源生态横向对比分析报告

**报告时间**：2026-05-27  
**数据来源**：各项目GitHub公共活动（24小时内）  
**分析视角**：AI智能体与个人AI助手开源生态技术趋势、社区活跃度与差异化定位

---

## 1. 生态全景

2026年5月27日，个人AI助手/自主智能体开源生态整体呈现**高强度迭代与稳定性阵痛并存**的态势。OpenClaw、IronClaw、CoPaw、ZeroClaw等头部项目日PR提交量均超过20条，表明核心团队与社区均处于高速开发周期。然而，多项目同时爆发与**子代理沉默失败、流式推理超时、安全绕过**相关的高严重度Bug（如Hermes Agent Codex崩溃、CoPaw ToolGuard绕过、OpenClaw事件循环饥饿），说明普遍存在“功能先行、可靠性后补”的阶段特征。架构层面，**模块化/插件化、Agent能力边界形式化、MCP协议深度集成**成为跨项目主流演进方向。社区对**跨平台桌面端、子代理可观测性、安全合规**的诉求持续升温，生态正从单机聊天脚本向企业级自主智能体基础设施过渡。

---

## 2. 各项目活跃度对比

| 项目 | 新开/活跃 Issues | PR 活跃总数 | 版本发布 | 健康度评估 |
|------|----------------|-------------|----------|------------|
| **OpenClaw** | 168 新开/活跃，211 关闭 | 500（251待合并+249合并/关闭） | 2个Beta | 高活力、高风险震荡 |
| **NanoBot** | 4 | 19（6合并） | 无 | 快速迭代，流中断严重回归 |
| **Hermes Agent** | ~20+（Codex崩溃集中爆发） | ~10（数组合并） | 无 | 极高活跃，事故响应极快但上游依赖脆弱 |
| **PicoClaw** | 5 新开，2 关闭 | 20（13合并） | 1个Nightly | 高度活跃，功能与修复并行 |
| **NanoClaw** | 0 | 4（1合并） | 无 | 深耕基础设施，健康度良好 |
| **NullClaw** | 0 | 2（1合并） | 无 | 低活跃维护期 |
| **IronClaw** | 14 活跃，2 关闭 | 50（16合并） | v0.29.0 | 极高活跃，发布流程需补齐 |
| **LobsterAI** | 0 | 12（9合并） | 无 | 优秀，OpenClaw生态集成收尾 |
| **TinyClaw** | 0 | 0 | 无 | 完全静默 |
| **Moltis** | 2 | 2（1合并） | 无 | 稳健演进，架构里程碑完成 |
| **CoPaw** | 22 新开，11 关闭 | 29（8合并） | 无 | 极高活跃，Beta稳定性警报 |
| **ZeptoClaw** | 0 | 16（2合并，14 Dependabot） | 无 | 依赖维护，社区静默 |
| **ZeroClaw** | 6 | 34（5合并） | 无 | 极高活跃，大量积压高风险PR |

---

## 3. OpenClaw在生态中的定位

**社区规模绝对领先**：OpenClaw日活跃度（379 Issue/500 PR）是第二梯队（IronClaw 50 PR、CoPaw 29 PR）的10倍以上，反映出其作为“生态母项目”的庞大贡献者网络。

**技术路线的深度与广度**：
- **架构重构力度最大**：同时进行Pi运行时内化、SQLite统一状态存储、Channel Broker官方频道矩阵。这使OpenClaw在长期可维护性上领先，但也导致Beta稳定性方差极大。
- **子代理编排是核心差异化**：其他项目多采用单层Agent或简单工具链，OpenClaw的子代理静默丢失问题(#44925)虽未被完美解决，但表明其任务分解复杂度远超同类，社区讨论也最为深入。
- **平台生态扩展激进**：从小米Token Plan到微信多账号、Telegram Webhook，OpenClaw的渠道/供应商覆盖速度最快，但频繁变更导致大量配置兼容性Issue。

**与竞品的错位竞争**：相比Hermes Agent依赖逆向Codex（高风险）、NanoBot轻量快速但深度不足、CoPaw偏重国产平台，OpenClaw在**全平台、全模型的通用性**上无出其右，代价是复杂度最高，非专业用户难以驾驭。

---

## 4. 共同关注的技术方向

| 技术方向 | 具体诉求 | 涉及项目 |
|---------|----------|----------|
| **子代理/任务编排沉默失败** | 子代理超时不通知、结果丢失、无错误日志，严重损害信任 | OpenClaw #44925, IronClaw #4084, CoPaw #4714, ZeroClaw #6688, NanoBot #4006 |
| **流式推理稳定性与超时机制** | 可配置看门狗上限、90s死锁、Codex空输出、Streaming支持缺失 | OpenClaw #68596, NanoBot #4013, Hermes #32963, PicoClaw #2404, CoPaw #4712 |
| **安全与凭证保护** | SSRF绕过、ToolGuard逃逸、SecretString非安全类型、无自动批准回退 | OpenClaw #81249, CoPaw #4709, IronClaw #4081/#4082, PicoClaw exec路径修复 |
| **MCP工具生态标准化** | MCP超时硬编码、工具列表动态更新、Session断线重连、运行时过滤 | OpenClaw #86758, NanoBot #4014/#4012, Hermes #32877, ZeroClaw #6920 |
| **跨平台/桌面端覆盖** | Linux/Win/Mac原生App、Windows事件循环饥饿、键盘快捷键兼容、TUI多会话 | OpenClaw #75, PicoClaw #2887 (RISC-V), ZeroClaw #6950, NanoClaw #2621 (CRLF), CoPaw #4704 (macOS Tahoe) |
| **国际化与本地化** | 非英语翻译完整度、区域化模型供应商（小米Token、字节跳动） | Hermes #32994 (20语言), CoPaw #1773 (i18n笔误), OpenClaw #86179 (小米) |

---

## 5. 差异化定位分析

| 角度 | OpenClaw | NanoBot | Hermes Agent | PicoClaw | NanoClaw | NullClaw | IronClaw | LobsterAI | Moltis | CoPaw | ZeptoClaw | ZeroClaw |
|------|----------|---------|--------------|----------|----------|----------|----------|-----------|--------|-------|-----------|----------|
| **功能侧重** | 全能通用Agent | 轻量快速迭代+自省循环 | ChatGPT深度绑定 | 嵌入式/边缘渠道扩展 | 个人生产力市场 | 底层基础设施 | 企业级多链签名 | OpenClaw生态协同 | Rust高安全Agent服务器 | 全功能国产化+插件系统 | 文档/展示站 | TUI+脚本化技能系统 |
| **目标用户** | 开发者和高级用户，追求全平台全模型 | 个人用户快速部署，重视体验 | 需要与ChatGPT同步的开发者 | RISC-V/嵌入式开发者, 中文用户 | SaaS化Agent市场用户 | Nix/底层贡献者 | 安全敏感的企业用户 | OpenClaw用户/贡献者 | 多用户家庭/小团队 | 国产模型用户, 中文社区 | 项目展示/文档 | 终端高手, 自动化重度用户 |
| **技术架构** | Node.js微服务，大型PR并行 | Node.js，Nightly快速通道 | Python/Codex协议逆向 | 嵌入式C++/跨平台 | Node.js容器化 | Rust/Zig | Rust多链签名 | 同步OpenClaw核心 | Rust单二进制, Agent能力边界 | Python，插件系统Schema驱动 | Astro静态站点 | Rust? 未明，技能系统 |
| **主要趋势信号** | 架构重构，生态扩张 | 流中断修复急迫 | 逆向依赖风险高 | 渠道多实例, 模型热修复 | 市场配置热加载 | Provider观测性提升 | Attested-signing全栈 | OpenClaw技能同步 | Agent作为多租户边界 | 插件架构, Beta回归严峻 | 依赖自动化 | 技能系统积累, 任务调度RFC |

---

## 6. 社区热度与成熟度分层

**第一梯队：极高活跃，快速迭代阶段**  
OpenClaw、IronClaw、CoPaw、ZeroClaw、PicoClaw、Hermes Agent、NanoBot  
- 每日提交量巨大（PR 20+），功能与Bug并行爆发。  
- 普遍存在1-2个P1级别的回归/安全事件，社区以“边修边用”模式推进。  
- 适合愿意承担风险、需要最新特性的早期采用者。

**第二梯队：稳健演进，质量巩固阶段**  
LobsterAI、Moltis、NanoClaw  
- Issue与PR数量较少，但每个变动都聚焦核心质量或架构落地。  
- 适合对稳定性要求较高、希望长期使用的用户。

**第三梯队：低活跃/维护期**  
NullClaw、ZeptoClaw、TinyClaw  
- 长期无实质新功能，仅依赖自动化维护或完全静默。  
- 存在项目停滞或“文档项目”风险，不适合作为主力选择。

---

## 7. 值得关注的趋势信号

**① 静默失败成为第一信任杀手**  
多个项目的最高赞/最热讨论都指向Agent在无反馈状态下丢失任务、消息或错误。**可观测性（opentelemetry logs, events, errors）不再只是运维工具，而是用户判断Agent是否“活着”的基本功能**。开发者应在设计初期就将子代理生命周期追踪、超时告警、审计日志纳入架构。  

**② 子代理/多Agent协作从愿景走向工程实现**  
OpenClaw、NanoBot、ZeroClaw都在大规模讨论子代理编排的失败模式、消息总线和跨实例通信。**A2A协议（Google）和MCP已经开始从概念进入代码**（Hermes #514、NanoBot #3992），这是个人AI助手从“单工具链”迈向“Agent网络”的拐点信号。

**③ 流式推理的行业性脆弱**  
几乎所有项目都暴露了与**流式超时、空输出、模型思考格式不兼容**相关的致命Bug。DeepSeek-R1、Claude Sonnet、Gemini等长思考/多模态模型的普及，使硬编码超时和单线程事件循环成为架构瓶颈。**自适应流控和异步非阻塞I/O成为必须**。

**④ 安全合规压力随多租户/企业场景升级**  
CoPaw的ToolGuard绕过、IronClaw的凭证泄露、ZeroClaw的任务调度绕过审批——这些问题集中在同一日出现，表明用户对Agent权限控制、审计、沙箱的需求从“可选”变为“必须”。**安全不是新功能，而是基础体验**。

**⑤ MCP正成为工具集成的“USB-C”**  
项目几乎都在围绕MCP进行修改：动态工具列表、会话管理、权限过滤、超时配置。**MCP已不再是单一协议实验，而是智能体生态的事实标准线**。任何新Agent项目若不能无缝接入MCP，将迅速丧失社区兴趣。

**⑥ 跨平台桌面端是拉开差距的关键战场**  
OpenClaw #75数月热榜第一、ZeroClaw TUI快捷键改进、CoPaw macOS崩溃、PicoClaw RISC-V支持——**用户不再接受“只能命令行”或“只能Web聊天”的Agent**。原生桌面App（macOS/Linux/Windows）和嵌入式Linux部署正在成为决定用户留存的分水岭。

**⑦ 中国本土化生态加速构建**  
小米Token Plan（OpenClaw #86179）、字节跳动Coding Plan（Hermes #32990）、WeCom渠道（IronClaw #2394）、元宝/MiniMax/智谱GLM专项修复（CoPaw #4711/#4625）——国产模型和平台的主动适配在同时进行。**对中文社区和国产供应商的支持力度，正在影响生态在中国市场的竞争力**。

---

*报告基于2026-05-27各项目公开GitHub数据。指标口径受各项目日报原始统计方式影响，部分项目PR/Issue计数为更新总数而非净新增，已在表格中注明关键数据来源。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，领导。这是为您准备的 NanoBot 项目动态日报，基于 2026-05-27 的数据生成。

---

# NanoBot 项目动态日报 (2026-05-27)

**报告周期**：2026-05-26 18:00 UTC ~ 2026-05-27 18:00 UTC

---

## 1. 今日速览

NanoBot 项目在今日展现出极高的开发活跃度。24 小时内，共处理 4 个新 Issue，并有 19 个 PR 处于活跃状态，其中 6 个已成功合并/关闭。合并的 PR 主要针对 WebUI 会话稳定性、第三方 API 集成（Kagi, Codex）以及平台扩展（Telegram Webhook, Docker）。与此同时，工作区沙箱安全模型（#4007）、Agent 自省循环（#4015）以及 Dream 系统架构重构（#3990）等重大功能正在深度审查中。项目整体推进速度极快，但 v0.2.0 引入的流中断问题（#4013）已成为社区最主要的负面反馈来源，需重点关注。

---

## 2. 版本发布

**无新版本发布**。项目目前处于 `nightly` 分支的高速迭代期，短时间内未形成正式发布版本。

---

## 3. 项目进展

今日合并/关闭的 6 个 PR 涵盖了稳定性修复与平台扩展，标志着项目在多个维度的修整与基础加固：

- **稳定性与健壮性修复**：
    - **fix(webui) #3944**：修复了会话列表刷新时，新建聊天记录丢失的回归问题，解决了影响用户交互体验的直接障碍。
    - **fix(provider) #4009**：修复了 Codex Provider 返回空白传输错误的问题，使错误日志和用户提示变得有意义，改善了排查体验。
    - **fix(web) #4004**：将 Kagi 搜索集成更新至最新的 v1 API 端点，防止了因上游 API 变更导致的服务中断。
    - **chore(CI/CD) #3981**：为 WebUI 引入了 ESLint 扁平化配置，正式开启前端代码质量检查流程。

- **平台集成与功能扩展**：
    - **feat(telegram) #3996**：新增了 Telegram Webhook 模式（保留长轮询为默认），为需要固定 IP/webhook 的服务器部署提供了关键支持。
    - **feat(docker) #4008**：成功将 AgentMail CLI 挂载进 Docker 镜像，并配套新增了 AgentMail Skill，打通了基于容器的邮件处理工作流。

---

## 4. 社区热点

- **#4013 - [Bug] LLM 流中断错误（关注度最高）**：
    该 Issue 成为当日用户情绪最强烈的反馈。用户报告从 v0.1.5 升级至 v0.2.0 后，频繁遭遇“流在 90 秒内停滞”的错误。用户直言“这让任何实际工作都变得无用”，并提到 AI 代理陷入了一个需要用户不断输入“继续”的死循环。该项目揭示了新版本在流式推理超时处理上存在严重回归，且目前尚无明确的修复 PR，是当前社区最为焦虑的未决问题。

- **#4007 - [Feat] 工作区沙箱能力模型（架构信号）**：
    该 PR 详细定义了工作区沙箱的 `off`、`application` 和 `system` 三级执行策略，并将其与 `AgentLoop`、子代理工具上下文和 WebUI 设置深度绑定。这是 NanoBot 向企业级安全合规迈出的关键一步，吸引了大量关注生态安全的开发者的讨论。

- **#3992 - [Feat] 跨智能体消息总线（路线图信号）**：
    此 PR 开放了跨实例的 Agent 通信能力，打破了单个 Agent 孤岛。尽管尚未合并，但它标志着项目架构从“单一智能体”向“多智能体协作”的演进，社区对该功能的未来应用场景（如任务拆分、主从协同）抱有极大期待。

---

## 5. Bug 与稳定性

| 严重级别 | Bug 描述 | Issue / PR | 状态与影响 |
| :--- | :--- | :--- | :--- |
| **严重** | **LLM 流持续停滞（Stream Stalled）** | #4013 | **无修复 PR，用户反馈强烈**。v0.2.0 升级带来的核心功能回归，可能导致版本回退。 |
| **严重** | **会话历史中存在孤立的工具结果（Orphaned Tool Results）** | #4006 -> PR #4011 | **已有修复 PR，审核中**。违反 OpenAI/Anthropic API 规范，导致严格校验的 API 拒绝请求。 |
| **中等** | Codex Provider 空白错误 | PR #4009 | **已合并修复**。 |
| **中等** | Kagi 搜索 API 集成失效 | PR #4004 | **已合并修复**。 |
| **中等** | DeepSeek 消息清洗不彻底 | PR #3869 | **待合并**。处理 null 内容及占位符泄漏问题。 |
| **中等** | Dream 系统“饥饿”问题（缺乏实时学习） | #3973 | **架构层讨论**。长期问题，旨在改进 Dream 系统数据源。 |

---

## 6. 功能请求与路线图信号

**高概率近期合并（短周期）**：
- **Agent 自省循环（#4015）**：引入 `Observation-Reflection Prompt`（Think→Verify→Act），代价小，理论上能显著提升 Agent 输出的一致性和逻辑性。
- **MCP 通信增强（#4014, #4012）**：支持 MCP Server 工具列表变更通知和 Session 断线重连。这是深化 MCP 协议集成的最后一块拼图，一旦合入将大幅提升 MCP 生态的鲁棒性。
- **工作区沙箱（#4007）**：安全需求的第一梯队。如果项目有意进入企业/团队协同场景，此 PR 应优先级最高。

**中期路线图信号**：
- **Dream 系统单阶段重构（#3990）**：将 Dream 从两阶段合并为单阶段，并接入 AgentLoop。这标志着项目正在对核心自我提升机制进行彻底的架构简化和质量重塑。
- **跨智能体协作（#3992）**：预示项目未来可能支持 Agent Swarm 或分层协作的工作范式。
- **TTS 语音输出（#4010）**：用户对“全闭环语音对话”的呼声越来越高，这是一个明确的产品增强信号。

---

## 7. 用户反馈摘要

- **强烈的用户体验负反馈（来自 #4013）**：
    - 用户 `mxnbf` 直言 v0.2.0 的升级是“破坏性”的，并高度肯定了 v0.1.5 的稳定性。用户的核心诉求是撤回或紧急修补硬编码的 `90 秒流超时` 机制。这代表了从“可用”到“不可用”的体验断崖。
- **深度用户的架构关切（来自 #3973）**：
    - 用户 `chxuan` 专门提交了一个 Issue 详细分析了 Dream 系统的“饥饿问题”，指出其仅依赖 `history.jsonl` 导致无法从持续对话中实时学习。这显示了社区中高阶用户不仅关注功能有无，更关注系统进化的底层逻辑。
- **功能缺口反馈（来自 #4010, #4006）**：
    - 用户 `olgagaga` 指出“能听不能说”的体验割裂，认为 TTS 是“最小化新界面的闭合循环”的最佳手段。
    - 用户 `sgod39507-a11y` 报告了非常具体的 API 规范违规问题，反映了用户对与严格 API 后端（如 OpenAI/Anthropic 原生）协同的强烈需求。

---

## 8. 待处理积压

提醒维护者关注以下重要的长期未处理 PR 和 Issue，以免造成社区贡献者流失或技术债积累：

- **#2515 - [Framework] 可插拔记忆框架**（3月26日提交）
    - 这是一个标志性的社区贡献，支持 Mem0、Graphiti 和 Memobase 等多个记忆后端。该 PR 体量大，逻辑复杂，已开放超过 2 个月。长时间搁置不仅会导致巨大的合并冲突，也可能打击贡献者。建议维护者尽快给予路线图立场或直接投入精力审核。

- **#1443 - [Feat] 解耦心跳推理与通知**（3月2日提交）
    - 一个相对成熟但等待了近 3 个月的功能 PR。它允许心跳 Agent 默认静默推理，仅在必要时通过 `message` 工具联系用户。技术实现清晰，冲突风险低，建议尽快评估合并。

- **#3869 - [Fix] DeepSeek Provider 消息健壮性**（5月16日提交）
    - 针对 DeepSeek 模型的专有 Bug（null 内容导致 400 错误，占位符泄漏）提供了实用修复。作为 provider 专项维护的一部分，此类 PR 的合并周期不宜过长。

- **#3968 - [Feat] /skill 斜杠命令**（5月23日提交）
    - 一个极简的功能请求，开发成本极低，但直接解决了用户“不知道有哪些技能可用”的基础体验问题。建议作为一次小改动快速合并，以提升用户满意度。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 2026-05-27 日 GitHub 数据生成的 Hermes Agent 项目动态日报。

---

## 🔥 2026-05-27 每日项目动态：Hermes Agent

### 1. 今日速览
项目今日遭遇了 **大规模生产级事故**，`openai-codex` 提供商（ChatGPT 后端）因上游 API 变更导致 `response.output` 为 `null`，引发大面积 `TypeError: 'NoneType' object is not iterable` 崩溃（单日涌现 20+ 相关 Issue）。社区与核心维护者 **反应极快**，项目所有者 `teknium1` 在数小时内合并核心修复 PR (#32963)，展现了极强的危机应对能力。在“救火”的同时，项目在功能开发上仍有扎实进展，包括 20 种语言的国际化支持和字节跳动新平台的适配。**总体活跃度极高，健康度总体良好（虽有波动但修复极其迅速且精准）。**

### 2. 版本发布
今日无新版本发布。

### 3. 项目进展
核心故障已被歼灭，基础设施和功能开发并行推进。
- **核心崩溃修复（里程碑事件）：**
  - **#32963 - [Merged] fix(agent): recover Codex Responses streams with null output** | 由项目所有者 `teknium1` 合并。该 PR 彻底解决了今日最重大的 `openai-codex` 崩溃事件。它通过从流式事件中反填缺失的终端输出来恢复中断的流，并关闭了由该问题衍生的 #11179 及 20+ 个重复 Issue。这是今日最关键的进度。
  - **#32972 & #32979 - [Merged] handle response.output=null** | 社区贡献（arniesaha, rororoach）的辅助修复方案，进一步夯实现有的流恢复逻辑，确保在各种边缘情况下的稳健性。
- **开发者体验与基础设施：**
  - **#29025 - [Merged] Ignore local Hermes runtime files** | 更新了 `.gitignore` 和 `.dockerignore`，防止本地运行时状态、缓存和秘密被误提交。
  - **#32989 - [Open] fix(gateway): avoid systemd restart loops on replace** | 针对 #32951 提出的系统守护进程重启风暴，提供了将 `Restart=always` 改为 `Restart=on-failure` 的解决方案。
- **功能开发推进：**
  - **#32994 [Open] feat(i18n): add 20-language translations** | 一次性提交了阿拉伯语、印地语、波兰语等 20 种语言的本地化文件。
  - **#32980 [Open] feat(tui): add TUI session orchestrator** | 引入了 Ink TUI 会话编排器，允许在终端界面内列举、切换、刷新和关闭多个会话。

### 4. 社区热点
1. **Codex 提供商大规模崩溃 (#32892, #32903, #32956 等)**
   - **热度分析：** 今日绝对的讨论中心。多个相关 Issue 累计获得超 100 条评论和 100+ 个表情反应。
   - **诉求分析：** 用户的核心诉求是 **工作流的紧急恢复** 和 **对上游 API 变更的韧性**。社区在数小时内就定位到根因（ChatGPT 后端变更导致 `response.output` 为空），大量开发者直接在 Issue 里贴出 patch 并互相验证。体现了社区的高度技术导向和对核心稳定性的强烈关注。随着 #32963 的合并，该讨论已转入“验证阶段”。
   - **链接：** [Issue #32892](https://github.com/NousResearch/hermes-agent/issues/32892) | [Fix PR #32963](https://github.com/NousResearch/hermes-agent/pull/32963)

2. **A2A 跨智能体通信协议支持 (#514)**
   - **热度分析：** 长期 Feature Request 持续获得关注，今日仍有高质量讨论。
   - **诉求分析：** 用户关注点从“工具使用”（MCP）转向了“智能体协作”（A2A），这表明核心用户群体正在推动 Hermes 从“个人助手”向“智能体网络节点”进化，希望实现任务的跨智能体分包与协作。
   - **链接：** [Issue #514](https://github.com/NousResearch/hermes-agent/issues/514)

### 5. Bug 与稳定性

- **P1 严重**
  - **安全绕过：** MCP 封装的命令直接调用 `subprocess.run`，跳过了 `approval.py` 的危险命令审批系统（#32877）。风险极高。
  - **功能瘫痪：** Cron 定时任务后台线程静默停止，导致所有定时作业无限期挂起（#32895）。
  - **阻塞崩溃（已修复）：** `openai-codex` 提供商完全不可用，崩溃链锁定在 `response.output = null`。已通过 #32963 合入修复。

- **P2 高**
  - **性能退化：** Codex 超时问题仍存，#32373 表明即使用了最新的超时修复，`gpt-5.5` 模型在发出第一个字节前仍会频繁卡死。
  - **静默失败：** `MEMORY.md` 如果使用普通 Markdown 而非标准分隔符格式，系统静默忽略，无任何错误日志（#32965）。
  - **配置丢失：** 桌面版 App（v0.5.1）会话无法延续，且存在 API Key 丢失和回复重复问题（#31977）。

- **P3 低**
  - `openai-codex` 长期存在的 `response.output is empty` 问题（#5879）。
  - QQ Bot 网关断线重连陷入死循环（#31101）。
  - Matrix 网关解密失败（#13891）。

### 6. 功能请求与路线图信号

- **确定性较高（已有 PR）：**
  - **全面国际化：** #32994 引入了 20 种语言，表明项目正在积极拓展全球非英语市场。预计将在下一版本中合入。
  - **新平台提供商：** #32990 增加了字节跳动 Coding Plan 和 Xiaomi Token Plan 的原生支持，反映了项目对多元化、区域化模型支持策略。
  - **TUI 会话管理：** #32980 提供了多会话编排能力，极大提升高级用户终端操作效率。
  - **Telegram 多实例支持：** #8287 允许同一账号并行控制多个机器人，是多任务工作流的关键拼图。
  - **回合级时间感知：** #10421 的需求讨论度很高，目的是让智能体在每一轮对话中精确知道当前日期和时间。

- **路线图长期信号：**
  - **A2A 智能体协议：** #514 的持续热度表明社区迫切期望 Hermes 接入“智能体互联网”。
  - **技能自动触发：** #4589 反映了用户对“智能体自主性”的更高要求，希望系统能根据上下文自动调用合适的技能，而非手动指定。

### 7. 用户反馈摘要

- **核心痛点：**
  - **对上游依赖的脆弱性感到不安：** “Hermes stopped working with ChatGPT integration, replying only: Error...”。用户对单一反向工程后端的稳定性表示担忧，普遍希望官方提供更健壮的容错机制或原生连接通道。
  - **“静默失败”导致认知偏差：** “Memory silently ignored... No errors logged, no warnings”。用户对系统缺乏反馈极度不满，声称这导致了“聊了半天发现智能体完全不知道我设定了什么”的糟糕体验，损害了用户信任。
  - **配置与场景边缘问题：** 桌面端 Session 丢失（#31977）和 Copilot 模型列表不更新（#22990）等问题，暴露了在特定交付场景下的质量打磨不足。

- **肯定与正向反馈：**
  - **事故响应速度极受认可：** 尽管 Codex 崩溃令人沮丧，但 PR #32963 在问题爆发的同一天即被合并，社区贡献者的迅速跟进获得了高度赞扬。这种“从发现到修复的快速闭环”是社区凝聚力的强心针。

### 8. 待处理积压

- **高优先级，亟待响应：**
  - **#32877 - MCP 安全绕过：** P1 严重安全漏洞，所有使用 MCP 工具的用户都暴露在危险命令风险之下。请维护者优先关注。
  - **#32895 - Cron 任务停止：** P1 功能瘫痪，严重影响自动化依赖用户，必须有日志和告警机制。
  - **#32951 - Systemd 重启循环：** 高影响，虽然已有 PR #32989，但尚未合并。在 systemd 上部署 Gateway 的用户可能面临服务频繁无故中断。

- **长期未响应的关键功能残缺：**
  - **#9077 - Vision 工具完全失效：** 自 4 月 13 日起存在，导致 Hermes 无法处理任何图片（URL 或本地文件），这对于宣称“多模态”的应用场景是一个巨大的功能短板。
  - **#4589 - 技能自动触发：** 用户期望“智能”加载，而非手动执行，这是衡量智能体“智能”程度的核心体验之一。
  - **#31101 - QQ Bot 断线重连死循环：** 严重影响国内用户生态的稳定性体验，需专门的 WebSocket 重连逻辑修复。
  - **#22990 - Copilot 模型选择器：** 静态列表导致新模型不可见，严重影响 Pro 订阅用户的体验。

---
*报告结束。所有数据均基于 NousResearch/hermes-agent 仓库在 2026-05-27 的公开活动。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw 项目日报 – 2026-05-27**  
*数据来源：GitHub (sipeed/picoclaw) | 统计时段：过去 24 小时*

---

## 1. 今日速览

过去 24 小时内 PicoClaw 保持 **高度活跃**：共有 7 条 Issue 更新（5 条新开/活跃，2 条关闭）和 20 条 PR 更新（7 条待合并、13 条已合并/关闭），同时发布了一个 nightly 版本。社区提交集中在 **渠道功能增强**（Telegram 商业/访客模式、微信多账号）、**工具安全修复**（exec 路径解析）、以及 **模型兼容性修复**（Claude Opus/Sonnet 参数、OpenAI web_search 类型）。一批积累的 PR 被批量合并，项目正稳步向下一正式版本迈进。

---

## 2. 版本发布

**Nightly Build** – `v0.2.9-nightly.20260527.28ec5793`  
- 自动构建，可能不稳定，仅供测试。  
- 完整变更日志：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
- 本次未包含破坏性变更或迁移说明。

---

## 3. 项目进展

今日共合并/关闭 **13 个 PR**，涵盖功能、修复与文档，主要推进方向包括：

### 渠道与平台扩展
- **Telegram**：新增 `guest_mode`（[#2849](https://github.com/sipeed/picoclaw/pull/2849)）与 `business_mode`（[#2845](https://github.com/sipeed/picoclaw/pull/2845)）支持。  
- **微信**：支持多账号配置，动态识别 `weixin_*` 前缀（[#2883](https://github.com/sipeed/picoclaw/pull/2883)）。  
- **飞书**：修复多实例通道名称硬编码问题，使用动态名称（[#2846](https://github.com/sipeed/picoclaw/pull/2846)）。  
- **嵌入式 Linux**：新增 Yocto/OpenEmbedded 层文档，方便在自定义镜像中部署（[#2851](https://github.com/sipeed/picoclaw/pull/2851)）。

### 核心稳定性与安全检查
- **exec 工具**：解决相对路径被当作绝对路径的安全守卫 bug（[#2826](https://github.com/sipeed/picoclaw/pull/2826)、[#2750](https://github.com/sipeed/picoclaw/pull/2750)）。  
- **spawn 异步结果**：引入可配置的投递策略，避免子代理结果被重复注入父对话（[#2830](https://github.com/sipeed/picoclaw/pull/2830)）。  
- **Steering 链式对话**：修复最终回复被错误地编辑占位消息而非发送新消息的问题（[#2840](https://github.com/sipeed/picoclaw/pull/2840)）；并添加实验性的同代理最终轮渲染模式（[#2844](https://github.com/sipeed/picoclaw/pull/2844)）。  
- **会话历史**：修复 SeaHorse 管道中 `created_at` 字段在 bootstrap 时丢失的问题（[#2946](https://github.com/sipeed/picoclaw/pull/2946)）。

### 前端体验
- **代码块**：统一添加行号与全局换行开关，覆盖聊天、技能详情与 MQTT 示例（[#2933](https://github.com/sipeed/picoclaw/pull/2933)）。

### 配置与默认行为
- **web_search 工具**：启用 YAML 配置支持并默认开启 DuckDuckGo 提供者（[#2647](https://github.com/sipeed/picoclaw/pull/2647)）。

这些合并使项目在渠道多样性、安全审计、异步控制和前端易用性上均有实质提升。

---

## 4. 社区热点

| 编号 | 标题 | 热度指标 | 核心诉求 |
|------|------|----------|----------|
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) | [Feature] Add in config to send streaming HTTP request | 8 comments, 1 👍 | 用户希望在配置中启用 `streaming: true`，以支持流式 HTTP 请求，类似 OpenAI Python SDK。 |
| [#2674](https://github.com/sipeed/picoclaw/issues/2674) | Codex OAuth: empty assistant response when ChatGPT backend streams items | 6 comments, 4 👍 | 使用 Codex OAuth 对接 ChatGPT 后端时助手回复为空，影响大量依靠此方案的用户。 |
| [#2952](https://github.com/sipeed/picoclaw/issues/2952) | 好久没发新版本了 | 1 comment | 中文用户集中反馈 exec 默认行为、QQ 渠道重启循环、模型界面配置缺失等三个痛点，表达对稳定版发布的期待。 |

最受关注的是 **#2674**（高 👍 数）和 **#2404**（高评论数），分别指向 **OAuth 兼容性** 与 **流式传输** 两个关键缺失。

---

## 5. Bug 与稳定性

### 严重（待修复或已有临时方案）
- **#2674** (Open, 4 👍) – **Codex OAuth 空响应**：ChatGPT 后端通过 `response.output_item.done` 流式输出时，PicoClaw 无法正确解析，回退为空响应。尚无关联 PR。  
- **#2887** (Open) – **RISC-V .deb 包使用 OpenAI 模型失效**：官方 .deb 在 RISC-V 架构下运行异常，影响特定硬件用户。  
- **#2943** (Open) – **微信渠道发送图片触发智谱 GLM-5 1210 参数错误**：图片消息无法正常调用 GLM-5-Turbo 视觉 API。

### 中等（已有修复 PR 提交）
- **#2951** (Open PR) – 修复 OpenAI 端点不支持 `web_search_preview` 时返回 HTTP 400 的问题，改用 `function` 类型。  
- **#2948** (Open PR) – 修复 `claude-opus-4-7` 发送 `temperature` 参数导致 HTTP 400 的问题。  
- **#2947** (Open PR) – 修复 `claude-sonnet-4.6` 默认 Model ID 错误（点号应改为连字符）导致的 404 错误。  
- **#2949** (Open PR) – 修复 Termux 环境下 HTTPS 请求因 CA 路径未识别而失败的 X509 错误。  
- **#2826 / #2750** (已合并) – exec 工具相对路径安全守卫修复。

### 稳定性改进
- 修复 steering 链式对话中回复被错误覆盖（[#2840](https://github.com/sipeed/picoclaw/pull/2840)）  
- 修复 SeaHorse 历史数据 `created_at` 不持久化（[#2946](https://github.com/sipeed/picoclaw/pull/2946)）

整体 bug 修复节奏良好，多个模型兼容性问题已在同一天提交 PR。

---

## 6. 功能请求与路线图信号

### 用户提出但尚未实现
- **Streaming 支持**（[#2404](https://github.com/sipeed/picoclaw/issues/2404)）：呼声高，若实现可大幅提升大模型响应体验。  
- **模型界面优化**（[#2952](https://github.com/sipeed/picoclaw/issues/2952)）：建议默认显示已保存的 Key 与提供商，支持下拉选择和 API 测试。  
- **exec 默认行为改进**（[#2952](https://github.com/sipeed/picoclaw/issues/2952)）：首次调用时缺少 `actions:run` 导致错误，需自动补充。  
- **QQ 渠道重启修复**（[#2952](https://github.com/sipeed/picoclaw/issues/2952)）：重启后再次发送消息会再次触发重启，需清除历史上下文才能停止。

### 已实现/合并，预示方向
- **Telegram Business & Guest**（[#2845](https://github.com/sipeed/picoclaw/pull/2845)、[#2849](https://github.com/sipeed/picoclaw/pull/2849)）→ 消息渠道功能深化。  
- **微信多账号**（[#2883](https://github.com/sipeed/picoclaw/pull/2883)）→ 支持同一渠道多实例。  
- **FUNDING.yml**（[#2950](https://github.com/sipeed/picoclaw/pull/2950)）→ 开始接受 GitHub Sponsors，项目可持续性提升。  
- **Yocto 层**（[#2851](https://github.com/sipeed/picoclaw/pull/2851)）→ 嵌入式部署场景被官方认可。

从近期合并趋势看，下一版本很可能包含 **渠道多实例、模型热切换、exec 安全加固、前端代码块优化** 等特性。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户声音：

| 用户视角 | 具体反馈 | 出处 |
|----------|----------|------|
| **开发者** | 希望像 OpenAI Python SDK 一样提供 `stream=True` 配置，以便实现逐字输出。 | [#2404](https://github.com/sipeed/picoclaw/issues/2404) |
| **OAuth 用户** | 使用免费 ChatGPT 后端时回复为空，必须 fallback 到“模型返回空响应”，导致体验中断。 | [#2674](https://github.com/sipeed/picoclaw/issues/2674) |
| **RISC-V 用户** | 官方 .deb 在该架构上无法调用 OpenAI 模型，怀疑是编译或依赖问题。 | [#2887](https://github.com/sipeed/picoclaw/issues/2887) |
| **中文普通用户** | exec 工具首次执行总是因为缺少 `actions:run` 报错，导致模型浪费一次冗余调用；QQ 渠道重启后不清理上下文会无限重启；模型配置界面不够直观，期望复用已有 Key 并增加测试连接按钮。 | [#2952](https://github.com/sipeed/picoclaw/issues/2952) |
| **微信/智谱用户** | 发送图片触发 GLM-5 API error 1210，怀疑是消息格式或参数传递问题。 | [#2943](https://github.com/sipeed/picoclaw/issues/2943) |

用户普遍对 **API 兼容性** 与 **渠道稳定性** 敏感，中文社区对本地化体验有较高期待。

---

## 8. 待处理积压

以下 Issue / PR 长期未获得解决或回应，建议维护者优先关注：

| 编号 | 类型 | 创建时间 | 概要 | 影响 |
|------|------|----------|------|------|
| [#2551](https://github.com/sipeed/picoclaw/pull/2551) | **PR (Open)** | 2026-04-16 | 重构频道标识，将名称与提供者类型解耦以实现多实例。 | 影响渠道多实例化落地，与已合并的 [#2883](https://github.com/sipeed/picoclaw/pull/2883) 理念相通，可加速推进。 |
| [#2239](https://github.com/sipeed/picoclaw/pull/2239) | **PR (Open)** | 2026-04-01 | 修改 Docker Compose 以支持 privileged 模式。 | 场景明确但长时间未 review。 |
| [#2674](https://github.com/sipeed/picoclaw/issues/2674) | **Issue (Open, 4 👍)** | 2026-04-26 | Codex OAuth 空响应。 | 影响 OAuth 流用户，且是社区高赞问题。 |
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) | **Issue (Open)** | 2026-04-07 | 请求新增 streaming 配置。 | 功能需求讨论时间长，无明确实现计划。 |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | **Issue (Open)** | 2026-05-17 | RISC-V .deb 不可用。 | 小众但严重影响特定硬件社区。 |
| [#2951](https://github.com/sipeed/picoclaw/pull/2951) / [#2948](https://github.com/sipeed/picoclaw/pull/2948) / [#2947](https://github.com/sipeed/picoclaw/pull/2947) / [#2949](https://github.com/sipeed/picoclaw/pull/2949) | **PR (Open)** | 2026-05-26 | 四个模型兼容性修复。 | 新提交，亟待 review 与合并，以免模型用户持续遇到 HTTP 4xx 错误。 |

以上 PR/Issue 涵盖架构重构、平台兼容与用户急迫需求，建议结合 nightly 测试节奏尽快处理。

---

*本日报由 PicoClaw 项目数据自动生成，仅供参考。所有链接指向 GitHub 原始讨论。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

收到。以下是根据您提供的 NanoClaw 项目 GitHub 数据，结合 AI 智能体与个人 AI 助手领域背景分析生成的 **2026-05-27 项目动态日报**。

---

# NanoClaw 项目动态日报 | 2026-05-27

**数据源：** GitHub (`nanocoai/nanoclaw`) · **分析区间：** 2026-05-26 ~ 2026-05-27

---

### 1. 今日速览

过去 24 小时，NanoClaw 项目 **Issue 端无新增反馈**，但 **Pull Request（PR）端表现活跃，共 4 条更新**。其中 1 个核心 Bug 修复已合并，解决了 Marketplace 技能市场更新后容器不生效的体验断层问题；另外 3 个待合并 PR 则分别聚焦于**部署自愈、CI 现代化和跨平台开发体验**。今日整体状态可概括为“无噪音，深耕基础架构”，项目健康度与工程化成熟度持续提升。

---

### 2. 版本发布

**无。** 今日无新版本发布（当前最新 Release 无变更）。

---

### 3. 项目进展

今日最重要的持续推进是 **PR #2622 的成功合入**，这在功能完备性上是一个关键里程碑。

- **[已合并] PR #2622 - web: restart container after marketplace skill/persona update**
  - **作者:** sumsumai | [查看 PR](https://github.com/nanocoai/nanoclaw/pull/2622)
  - **内容：** 修复了用户在 `app.solela.ai` 市场上通过 “Use this agent” 配置新 Skill 或 Persona 后，容器未热加载新配置的问题。
  - **重要性：** 此前 `composeGroupClaudeMd` 仅在容器启动时读取 `custom_skill_md`。此次修复在 `handleProvision` 更新数据库后，主动触发了容器的重启，使得功能市场的 **“一键启用”** 即刻生效。这是提升平台 Agent 交易与订阅转化率的核心体验补完。

---

### 4. 社区热点

由于今日各项 PR 与 Issue 均**未产生公开评论或 Reactions**，讨论度较低。但从 PR 提交流程可以明显看出现阶段社区贡献者关注度的三大集中区：

1. **部署健壮性（PR #2620）：** 针对 Dokploy 等 PaaS 环境下的容器崩溃循环问题，贡献者 `matmartinez` 提交的自愈方案获得了高关注度。
   - [PR #2620](https://github.com/nanocoai/nanoclaw/pull/2620)
2. **工程债务预防（PR #2608）：** 预判 2026 年 6 月 GitHub Actions 运行时淘汰，贡献者 `IamAdamJowett` 体现了对项目长期维护的责任心。
   - [PR #2608](https://github.com/nanocoai/nanoclaw/pull/2608)
3. **开发者生态扩展（PR #2621）：** 解决 Windows 开发者的换行符痛点，降低了开源贡献门槛。
   - [PR #2621](https://github.com/nanocoai/nanoclaw/pull/2621)

---

### 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 问题描述 | 状态 | 链接 |
|---|---|---|---|
| 🔴 **严重** | **容器镜像缺失导致崩溃循环**：当 Dokploy 等运维工具执行 Daily Cleanup 清理 Docker 镜像后，`spawnContainer` 因找不到镜像直接 `docker run` 失败，导致容器无限 Crash-Loop。 | **Fix PR 已提交 (#2620)** | [PR #2620](https://github.com/nanocoai/nanoclaw/pull/2620) |
| 🟡 **中等** | **Marketplace 技能更新不生效**：用户购买或启用了新模板，配置已写入 DB，但由于缺少重启指令，业务逻辑读取的是旧配置。 | **已修复并合并 (#2622)** | [PR #2622](https://github.com/nanocoai/nanoclaw/pull/2622) |
| 🟢 **低** | **Windows 环境 Shell Script 执行失败**：Git 在 Windows 上将 Shell 脚本自动转化为 CRLF 导致语法错误，影响开发者的本地环境搭建。 | **Fix PR 已提交 (#2621)** | [PR #2621](https://github.com/nanocoai/nanoclaw/pull/2621) |

---

### 6. 功能请求与路线图信号

今日**无新增 Feature Request Issue**，但通过活跃的 PR 可以有效推断未来的迭代方向：

- **信号 1：基础设施防脆弱性（路线图可能性：高）**  
  PR #2620 的“自愈”机制表明项目正在从“假设环境完美”向“生产级容错”演进，下一版很可能内置镜像校验与自动重建逻辑。
- **信号 2：运行时现代化（路线图可能性：中高）**  
  PR #2608 主动迁移至 Node 24 运行时（Actions `@v5`），为后续可能发布的、需要新运行时特性的功能（如更快的 CLI 工具链）铺平道路。
- **信号 3：跨平台支持（路线图可能性：中）**  
  PR #2621 的 `.gitattributes` 虽是小改动，但暗示了项目正在严肃考虑吸纳非 Linux/macOS 环境下的贡献者，未来可能跟进 Windows Runner 的支持。

---

### 7. 用户反馈摘要

由于今日所有条目 **评论数均为 0**，无法直接获取在线讨论。但从 PR 提交描述中可以提取出非常清晰的 **原始用户痛点**：

- **“我没法放心部署”**：Dokploy 用户指出，在一次清理后整个集群的 NanoClaw Agent 全部崩溃，必须手动介入。这种不能自愈的状态让用户不敢在生产环境依赖项目。（源自 #2620）
- **“我点了启用按钮，但它没反应”**：市场用户在 UI 上点击配置后，系统并未响应更新，必须要求管理员去后台重启容器。这种体验伤害了 SaaS 化使用的信任度。（源自 #2622）
- **“我在 Windows 上根本跑不起来”**：潜在的开发者贡献者想本地运行 Shell 脚本，直接被换行符卡住，导致无法进入开发流程。（源自 #2621）

---

### 8. 待处理积压

目前不存在长期无人响应的僵尸 Issue 或 PR。以下 **3 个待合并 PR** 均在近 48 小时内创建，但建议维护者按照业务影响度安排审查优先级：

| 优先级 | PR编号 | 原因 |
|---|---|---|
| 🔥 **P0** | [#2620](https://github.com/nanocoai/nanoclaw/pull/2620) | 直接影响生产环境 Agent 的可用性，属于**崩溃级阻断 Bug**，建议立即审查。 |
| ⏰ **P1** | [#2608](https://github.com/nanocoai/nanoclaw/pull/2608) | 距离 GitHub 2026 年 6 月弃用 Node 20 尚有窗口期，但建议尽快合入以避免 CI 突然全红。 |
| 🛠️ **P2** | [#2621](https://github.com/nanocoai/nanoclaw/pull/2621) | 纯开发者体验优化，不阻塞任何功能，可排入常规 Sprint。 |

---

**分析师总结：** 今日 NanoClaw 项目正处于 **“修复关键体验短板”和“加固工程质量底座”** 的阶段。虽然没有大版本发布和新功能浮出水面，但解决了市场热加载这一核心逻辑，以及针对生产环境镜像崩溃的自愈方案，将显著提升项目在 **商业化部署** 场景下的口碑。建议关注 #2620 的下一个合并窗口，这将是项目迈向 **“高可用 AI Agent 基础设施”** 的重要标志。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是 **NullClaw 项目日报** (2026-05-27)。

---

## NullClaw 项目动态日报 | 2026-05-27

### 1. 今日速览
NullClaw 今日处于**低活跃度的维护期**。过去24小时内未产生新 Issue，社区反馈较为平静，项目重点集中在底层基础设施的健壮性提升与构建系统的适配修复上。一个改善 Provider 连接探测错误可观测性的重要 PR 已被合并，优化了核心网络层的调试体验。同时，存在一个阻塞 Nix 构建的 Bug，其修复 PR 目前仍在等待合并。

### 2. 版本发布
无

### 3. 项目进展
**合并/关闭：核心基础设施可观测性提升**
- **PR #891 [CLOSED]**: `fix(providers): preserve curl probe transport failures`
  - **摘要**: 该 PR 修复了 OpenAI 兼容 API 的健康探测路径中的错误处理逻辑。此前，底层的 cURL 传输层错误（如 DNS 解析失败、连接超时、TLS 握手错误等）被吞并并转换为模糊的通用错误。现在，这些具体错误类型会被保留并向上传递，极大地改善了用户在排查 Provider 连接中断时的诊断效率。
  - **影响**: 增强了 AI 智能体与上游 Provider 之间的通信可靠性观测，是基础设施层的重要改进。
  - [查看 PR #891](https://github.com/nullclaw/nullclaw/pull/891)

### 4. 社区热点
**焦点：【构建系统】Nix 构建中断问题**
- **PR #935 [OPEN]**: `fix(nix): updated lockfiles to work with zig 0.16.0`
  - **热度分析**: 尽管该 PR 暂无公开评论，但作为昨日开启且直接修复阻塞性构建失败的 PR，它代表了当前 Nix 生态用户最急迫的需求。
  - **诉求分析**: 作者明确指出了项目未完全适配 Zig 0.16.0 的构建依赖锁文件问题。这反映出社区对“声明式构建环境（Nix）”的即时生效性非常敏感，任何构建链的脱节都会严重影响核心贡献者与测试者的工作流。
  - [查看 PR #935](https://github.com/nullclaw/nullclaw/pull/935)

### 5. Bug 与稳定性
按严重程度排列：
- **[严重] Nix 构建完全中断**
  - **问题**: 由于 `flake.lock` 锁定了不兼容 Zig 0.16.0 的旧版 `zig2nix` 依赖，导致所有 Nix 路径的构建失败。
  - **状态**: **已有修复 PR (#935)**，正在等待核心维护者审批与合并。
  - [查看 PR #935](https://github.com/nullclaw/nullclaw/pull/935)

- **[中等] Provider 健康探测错误信息模糊 (已修复)**
  - **问题**: 底层网络错误（如 DNS/超时/TLS）被统一处理，导致用户难以区分是 Provider 拒绝服务还是网络链路故障。
  - **状态**: 已于 **PR #891** 中修复并合并。
  - [查看 PR #891](https://github.com/nullclaw/nullclaw/pull/891)

### 6. 功能请求与路线图信号
今日数据未显示新增的功能请求。从已有 PR 解读路线图信号：
- **观测性优先 (Observability Push)**：PR #891 的合并表明项目正在加强对 Provider 集成层的关键路径观测能力。将底层 cURL 错误暴露出来，意味着未来在 Agent 运行监控和故障排查工具链上可能会有更多投入。
- **DevEx 维护承诺**：PR #935 的存在显示出项目维护者致力于支持 Nix 作为一等开发环境，即便在 Zig 语言版本 migrate 的时期，也在积极修复构建适配问题。

### 7. 用户反馈摘要
由于今日 **Issues 与 PR 均无公开评论**，以下反馈摘要基于 PR 上下文推断：
- **痛点 (构建环境)**: “在升级至 Zig 0.16.0 后，Nix 开发环境完全断裂，无法构建项目，直到 lock 文件被更新。” —— *推断自 PR #935 描述*。
- **痛点 (错误诊断)**: “当 Provider 探测失败时，我无法判断是网络超时、DNS 错误还是 TLS 证书无效，需要更底层的错误详情。” —— *推断自 PR #891 的修复动机*。

### 8. 待处理积压
- **PR #935**: `fix(nix): updated lockfiles to work with zig 0.16.0`
  - **优先级**: **高**
  - **状态**: 已开启 1 天，待审核
  - **维护建议**: 这是一个阻塞性 Bug 修复，直接导致 Nix 用户无法构建。建议维护者尽快审阅并合并，以避免社区关键贡献者流失。
  - [查看 PR #935](https://github.com/nullclaw/nullclaw/pull/935)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

#  IronClaw 项目日报 — 2026-05-27

**数据覆盖时段**：2026-05-26 – 2026-05-27  
**趋势总览**：16 条 Issue 更新（14 条活跃 / 2 条关闭） · 50 条 PR 活动（34 条待合并 / 16 条已合并/关闭） · 1 个新版本发布

---

## 1. 今日速览

过去 24 小时 IronClaw 保持 **极高活跃度**，开发重心围绕 **Reborn 平台扩展能力**（扩展生命周期 CLI、Builtin HTTP save_to、技能列表）、**attested-signing 多链签名栈**（持续多 PR 并行提交）以及 **hooks 框架与安全加固**。新版本 v0.29.0 已于 2026-05-26 发布，增加 WeCom 渠道、外部工具支持及日志下载按钮。但 **社区核心痛点依然存在**：crates.io 发布严重滞后（最高 0.24.0），数个安全与稳定性 Bug 正待修复。整体看，项目创新节奏快，但发布流程和安全审查需补齐。

---

## 2. 版本发布

### 📦 ironclaw-v0.29.0 (2026-05-26)

**更新亮点**：
- *(channels)* 新增 **WeCom（企业微信）渠道** — [PR #2394](https://github.com/nearai/ironclaw/pull/2394)
- *(web)* **Responses API 支持外部提供的工具** — [PR #3122](https://github.com/nearai/ironclaw/pull/3122)
- *(gateway)* **Gateway 增加日志下载按钮** — [PR #3588](https://github.com/nearai/ironclaw/pull/3588)

> ⚠️ **重要提醒**：该版本目前 **仅以 GitHub tag 形式存在**，crates.io 上最新仍为 `0.24.0`（2026-03-31）。下游通过 crates.io 依赖的用户无法获取该版本，参见社区 Issue [#3259](https://github.com/nearai/ironclaw/issues/3259)。

---

## 3. 项目进展

过去 24 小时内 **16 个 PR 被合并/关闭**，主要包括以下对项目有实质性推进的变更：

| PR | 变更内容 | 状态 | 影响 |
|----|---------|------|------|
| [#4103](https://github.com/nearai/ironclaw/pull/4103) | **Reborn builtin HTTP 支持 `save_to`** | 已合并 | 内置 HTTP 工具现在可将响应体写入文件系统，并通过统一入口管理写入权限 |
| [#4099](https://github.com/nearai/ironclaw/pull/4099) | **添加 Reborn 扩展生命周期 CLI**（含数据库迁移） | 已合并 | 提供 `ironclaw-reborn extension` 命令，支持本地开发态搜索/安装/激活/移除扩展 |
| [#4095](https://github.com/nearai/ironclaw/pull/4095) | **实现 Reborn CLI skills list** | 已合并 | 替换之前存根，基于组合层技能目录展示可用 skill |
| [#3889](https://github.com/nearai/ironclaw/issues/3889) (Issue) | **审批交互服务** 对应任务关闭 | 已关闭 | 认证流程从混杂物中剥离，已有专用 Reborn 原生组件 |
| [#3886](https://github.com/nearai/ironclaw/issues/3886) (Issue) | **WebUI v2 移植到 Reborn WebChat** | 已关闭 | 静态 UI 原型已对接新一代 WebChat 入口 |

**整体进展**：Reborn 平台的可扩展性（扩展、技能、HTTP 工具）和审批/认证基础初步成型，为后续多租户与生产化奠定基础。

---

## 4. 社区热点

1. **🔥 [#3259  Publish 0.25.0–0.27.0 to crates.io](https://github.com/nearai/ironclaw/issues/3259)** — 10 条评论，持续 22 天  
   - **诉求**：crates.io 版本停留在 0.24.0，用户被 wasmtime 28.x CVE 阻挡无法升级。社区强烈要求发布已标签的 0.25.0–0.27.0（以及 v0.29.0）。**目前仍是 Open 状态，无维护者回应**，是社区最关切的阻塞项。

2. **💬 [#3857 [Reborn] Slack ProductAdapter MVP](https://github.com/nearai/ironclaw/issues/3857)** — 4 条评论  
   - 讨论如何用预配置凭证实现 Slack DM/提及路由。设计已基本定型，等待合并后添加默认启用开关。

3. **🧵 [#3281 [Reborn] EventStreamManager](https://github.com/nearai/ironclaw/issues/3281)** — 2 条评论，附大量关联 Issue  
   - 虽是技术跟踪 Issue，但关联了 9+ 个子任务（#3093、#3266 等），引起 Reborn 事件流路线的深度讨论。

PR 方面，虽然评论统计数据未展示，但 **#3931、#3937、#3965、#3995、#4015** 等 XL 级 PR 均在同一时段更新，反映出核心团队围绕 attested-signing 和 hooks 框架的密集协作。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重级别 | Issue | 问题描述 | 现状 |
|----------|-------|----------|------|
| **🔴 严重** | [#4082](https://github.com/nearai/ironclaw/issues/4082) | **凭证路径 `SecretString` 被 unwrap 为 `String`**，泄露敏感数据风险 | 已标记 security，尚无 fix PR |
| **🔴 严重** | [#4081](https://github.com/nearai/ironclaw/issues/4081) | **签名批准门字段为 `Optional`，可能绕过审批** | 已标记 security，修复方向明确 |
| **🟡 中** | [#4084](https://github.com/nearai/ironclaw/issues/4084) | **后台子代理结果从未通知父级**，父级无法主动获知结果 | 已认领，Gap 2 跟踪 PR [#4092](https://github.com/nearai/ironclaw/issues/4092) 在修复中 |
| **🟡 中** | [#4085](https://github.com/nearai/ironclaw/issues/4085) | **生产运行时构建器缺少 TenantSandboxProcessPort**，导致组合测试永久失败，CI 信号失灵 | 已提交，修复需扩展 Host builder |
| **🟢 低** | [#4106](https://github.com/nearai/ironclaw/issues/4106) | **setup wizard 忽略 `SANDBOX_IMAGE` 环境变量**，总是检测硬编码默认值 | 新提交，无 assignee |

**影响评估**：前两项安全 Bug 来自内部审查的 follow-up，若不修复可能在多租户场景下酿成漏洞。#4084 直接影响后台子代理功能，对新架构下的复杂工作流至关重要。

---

## 6. 功能请求与路线图信号

### 高概率进入下一版本 (v0.30.0) 的功能栈

- **🧾 Attested-signing 完整栈**（十余个 XL PR 在 review 中）  
  `#3995` `#3997` `#4015` `#4060` `#4054` `#3963` `#3996` `#4055` `#3965` — 涵盖多链签名、耐久存储、信任登记、回放保护等。一旦合并，将极大增强代理自主签名能力，是 Reborn 生产化的关键拼图。

- **📡 事件流管理 (EventStreamManager)**  
  `#3281` `#3809` — 为 Web SSE / WebSocket 提供耐久可重放的投影流，当前正在推进 timeline/replay 路径。

- **🔌 扩展生命周期**（今日已合并 `#4099`） — 已具备本地安装、激活能力，下一步会对接生产与多租户路由（跟踪 Issue `#4091`）。

- **⏳ 用户明确需求**：`#3259` 要求 crates.io 发布流程；`#4102` 提议 Grant 过期实施，关联 PR `#4104` 已提交。

### 路线图信号

代码仓库强烈显示 Reborn 平台正从 **“功能可用”** 走向 **“生产就绪”**——扩展动态加载、多租户隔离、安全签名均已进入实现阶段。预计 0.30.0 将是一次重要的能力整合发布。

---

## 7. 用户反馈摘要

从 Issue 评论与行为模式提取的真实用户声音：

- **“crates.io 版本停滞严重影响我们集成”**（[#3259](https://github.com/nearai/ironclaw/issues/3259)）  
  用户明确指出，因 wasmtime CVE 必须锁定 0.24.0，无法享受后续修复和新功能。期望建立自动化发布流水线，或至少手动发布 tag 版本至 crates.io。**此反馈已持续 22 天无官方回复**，是当前社区信任度的最大风险点。

- **“预配置凭证的 Slack 适配器很实用，希望尽快出台文档”**（[#3857](https://github.com/nearai/ironclaw/issues/3857)）  
  用户（可能为团队扩展开发者）对 DMs 和 app mentions 的设计表示认可，但在评论中询问何时提供配置向导与使用示例。

- **安全反馈主要来自内部审查**（[#4081](https://github.com/nearai/ironclaw/issues/4081)、[#4082](https://github.com/nearai/ironclaw/issues/4082)）  
  外部用户暂未发声，但因涉及凭证处理，一旦泄露将直接影响所有终端用户信任。宜尽快修复并发布安全公告。

---

## 8. 待处理积压

以下 Issue/PR 长期未响应或需要维护者关注，可能成为瓶颈：

| 类型 | ID | 描述 | 等待时长 | 风险 |
|------|----|------|----------|------|
| Issue | [#3259](https://github.com/nearai/ironclaw/issues/3259) | **crates.io 发布阻塞**（0.25.0–0.29.0） | 🕐 22 天 | **高** – 社区信任流失，依赖管理困难 |
| Issue | [#3281](https://github.com/nearai/ironclaw/issues/3281) | EventStreamManager 主 Issue（依赖 9 个子任务） | 🕐 21 天 | **中** – 事件流路线图的卡点 |
| Issue | [#4088](https://github.com/nearai/ironclaw/issues/4088) | **跟踪大型文件分解**（代码审查债务） | 🕐 1 天 | **低** – 若不排期可能影响后续 PR review 效率 |
| PR | [#3937](https://github.com/nearai/ironclaw/pull/3937) | 跨后端对抗测试套件（hooks 持久化后端 4/4） | 🕐 4 天 | **中** – 规模 XL，需要更多 reviewer |
| PR | [#4060](https://github.com/nearai/ironclaw/pull/4060) | 签名连续性断言 + 全栈审查 follow-up | 🕐 2 天 | **中** – 与其他签名 PR 互为依赖，阻塞整个栈 |

**建议**：
- 维护者尽快回应 [#3259](https://github.com/nearai/ironclaw/issues/3259) 并给出 crates.io 发布计划；
- 为 [#4085](https://github.com/nearai/ironclaw/issues/4085)（CI 信号掩盖）分配紧急修复，以免其它 Bug 被漏过；
- 针对 [#4081](https://github.com/nearai/ironclaw/issues/4081) 和 [#4082](https://github.com/nearai/ironclaw/issues/4082) 安全漏洞，建议在下一个补丁版本中立刻合入。

---

*报告自动生成，基于 IronClaw 公开 GitHub 数据。所有链接均为原始 Issue/PR 地址。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是基于 LobsterAI（netease-youdao/LobsterAI）GitHub 公开数据生成的 2026-05-27 项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-05-27

### 1. 今日速览
过去24小时 LobsterAI 项目开发节奏非常紧凑，共处理 **12 条 PR**，合并/关闭 **9 条**。核心团队高强度投入在 **OpenClaw 技能生态系统的集成收尾** 和 **Bug 稳定性修复** 上。今日社区 Issue 活跃度为 **0**，未产生新的用户报告，说明近期引入的 Bug 多数已被开发团队在测试时拦截并修复。整体项目健康度 **优秀**，处于大型功能合并后的快速打磨阶段。

---

### 2. 版本发布
*（暂无新版本发布）*

---

### 3. 项目进展
今日项目在 **OpenClaw 集成** 与 **核心 UX 修复** 上迈出了重要一步，共有 **9 个 PR** 被合并关闭。

#### 🎯 核心功能落地
- **[已合并] 技能同步功能最终定型（#2045 & #2054 & #2055）：**
  - **#2045** 实现了从 OpenClaw 同步技能到本地的核心能力。
  - **#2054** 紧随其后合并，修复了内部 Provider 和 Alias 插件被错误纳入同步检测的问题，避免了用户 UI 界面出现冗余插件。
  - **#2055** 则通过 Feature Flag (`ENABLE_OPENCLAW_SKILL_SYNC`) 将同步功能默认关闭，并允许用户删除市场中安装的技能，给予用户更多控制权，防止误覆盖。
    - [netease-youdao/LobsterAI PR #2045](https://github.com/netease-youdao/LobsterAI/pull/2045)
    - [netease-youdao/LobsterAI PR #2054](https://github.com/netease-youdao/LobsterAI/pull/2054)
    - [netease-youdao/LobsterAI PR #2055](https://github.com/netease-youdao/LobsterAI/pull/2055)

#### 🐛 关键缺陷修复
- **[已合并] 修复切换模型导致技能丢失（#2052）：** 修复了当用户在 Agent 设置中切换模型时，之前选定的技能被意外清空的严重问题。根因是 `syncActiveSkillsForCurrentAgent()` 被无条件调用。
- **[已合并] 修复工具调用循环/死锁（#2051 & #2058）：** 针对 LLM 在调用工具时可能陷入无限循环，以及协同模式下大工具结果后最终回复的宽限期过短问题进行了修正。
    - [netease-youdao/LobsterAI PR #2052](https://github.com/netease-youdao/LobsterAI/pull/2052)
    - [netease-youdao/LobsterAI PR #2051](https://github.com/netease-youdao/LobsterAI/pull/2051)
    - [netease-youdao/LobsterAI PR #2058](https://github.com/netease-youdao/LobsterAI/pull/2058)

#### 🛠 平台与开发体验
- **[已合并] 修复 Windows Dev 模式 OAuth 协议注册（#2059）：** 修复了开发者在 Windows 上运行时，OAuth 回调 URL 被当作文件路径而非深度链接处理的严重 Bug，对 Windows 贡献者体验至关重要。
    - [netease-youdao/LobsterAI PR #2059](https://github.com/netease-youdao/LobsterAI/pull/2059)

---

### 4. 社区热点
今日无新增 Issue 或 PR 引起大规模讨论。但有三条 **长期未合并的 PR** 在今日获得标注/更新，反映了潜在的社区关注点：

- **#1760 (Image Agent Avatars)：** 该 PR 实现了为 Agent 添加图片头像的功能，是社区呼声较高的个性化功能。目前已标记为 `stale`（已停滞），但获得了一次活动更新（2026-05-26）。背后的诉求是用户不满足于仅使用 Emoji 作为头像，需要更强的辨识度。
- **#1773 (i18n Memory Edit Translation)：** 修复一个极其简单的国际化笔误（缺少 `edit` 翻译键）。同样标记为 `stale` 已超一个月。这反映出社区对于**本地化质量**的敏感度，同时也暴露了小型贡献在合并流程上可能存在的瓶颈。
    - [netease-youdao/LobsterAI PR #1760](https://github.com/netease-youdao/LobsterAI/pull/1760)
    - [netease-youdao/LobsterAI PR #1773](https://github.com/netease-youdao/LobsterAI/pull/1773)

---

### 5. Bug 与稳定性
今日项目大幅清除了近期积压的技术债和 Bug，合并了 **7 条 Bug 修复 PR**。

| 严重程度 | 问题描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| **严重** | Windows 开发模式下 OAuth 回调无法注册，导致登录流程断裂 | ✅ **已修复 (Merged)** | [#2059](https://github.com/netease-youdao/LobsterAI/pull/2059) |
| **严重** | 切换模型后，用户手动选中的技能被清空 | ✅ **已修复 (Merged)** | [#2052](https://github.com/netease-youdao/LobsterAI/pull/2052) |
| **高** | 工具循环断路器失效，可能导致 LLM 无限调用 | ✅ **已修复 (Merged)** | [#2051](https://github.com/netease-youdao/LobsterAI/pull/2051) |
| **高** | 协同模式下大量工具结果后，最终回复的输出宽限期不足 | ✅ **已修复 (Merged)** | [#2058](https://github.com/netease-youdao/LobsterAI/pull/2058) |
| **中** | 模型选择 UI 样式/逻辑问题 | ✅ **已修复 (Merged)** | [#2053](https://github.com/netease-youdao/LobsterAI/pull/2053) |
| **中** | OpenClaw 同步检测误将内部插件暴露给用户 | ✅ **已修复 (Merged)** | [#2054](https://github.com/netease-youdao/LobsterAI/pull/2054) |
| **低** | 应用更新机制使用已废弃的 VBScript 启动器 | **⏳ 待合并 (Open)** | [#2057](https://github.com/netease-youdao/LobsterAI/pull/2057) |

---

### 6. 功能请求与路线图信号
- **OpenClaw 生态深度整合：** 今日 #2055 虽然将同步功能默认关闭（通过 Feature Flag），但这正是大型功能上线前的标准稳健做法。这表明团队正在审慎地推进 OpenClaw 集成，且删除许可的调整说明他们正在倾听用户对技能管理自主权的需求。**下一版本的核心看点仍是 OpenClaw 技能市场。**
- **HTML 分享（#2056）：** 一个已合并的新功能，增加了协同写作/聊天内容的 HTML 格式分享能力，适用于输出报告或分享对话记录。
- **图片头像（#1760）：** 该功能代码已完备，但一个月未能合并。如果它能进入下一个版本，将是 Agent 个性化体验的一次重大升级。

---

### 7. 用户反馈摘要
（基于 PR 的提交信息和测试用例描述，当日无新 Issue 评论）

- **真实痛点一：** 用户在使用多 Agent 时，频繁切换模型会破坏精细的技能配置，导致用户体验下降。这是本次 #2052 修复的根因。
- **真实痛点二：** Windows 开发者用户在本地开发调试 OAuth 功能时完全被阻塞（#2059）。
- **使用场景：** 从提交的修复内容来看，用户的典型场景包括 **“选择模型并搭配不同技能”** 的复杂工作流，以及 **“协同编程/写作后导出为 HTML”** 的内容产出需求。

---

### 8. 待处理积压
- **🔴紧急：** 无明显长期搁置的严重 Bug。但 **#2057 (App Update VBScript to PowerShell)** 虽非紧急 Bug，却是长期维护的重要基础设施，且已进入待合并状态，建议尽快合入。
- **🟡需关注：**
  - **#1760 (Image Avatars)：** 一个完整的 Feature 被标记为 `stale`。维护者需要在该 PR 上进行决策（合并、要求修改或关闭），否则会挫伤外部贡献者的积极性。
  - **#1773 (i18n fix)：** 作为一个极其轻量且无害的修复，滞留时间过长。建议维护者尽快合并，以解决非英语用户（尤其是中文用户）在设置页面的本地化体验问题。
    - [netease-youdao/LobsterAI PR #1760](https://github.com/netease-youdao/LobsterAI/pull/1760)
    - [netease-youdao/LobsterAI PR #1773](https://github.com/netease-youdao/LobsterAI/pull/1773)
    - [netease-youdao/LobsterAI PR #2057](https://github.com/netease-youdao/LobsterAI/pull/2057)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-05-27

---

## 1. 今日速览

过去 24 小时内，Moltis 保持了稳健的演进节奏：1 个里程碑式 PR 合并，1 个新 PR 提交，2 个新 Issue，无版本发布。**最值得关注的动向是架构层面的重大推进（#1049 合并）以及外部合作问询（#1076）。** 虽然 Issue/PR 评论互动为零（无社区讨论往来），但合作伙伴主动接洽及用户提交的格式化 Bug 报告均体现了项目吸引力的稳步上升。项目健康度良好，处于“核心功能深耕 + 生态影响力外溢”的阶段。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

### 核心架构演进（已合并）
- **[#1049 feat: agents as capability boundaries (MCP, sandbox, skills)](https://github.com/moltis-org/moltis/pull/1049)**
  该 PR 由 `penso` 于 5 月 23 日提交，今日正式合并关闭。**这是近期对 Moltis 架构影响最深远的一次改动。** 它将 Agent 定义为核心能力边界，Agent 预设现统一控制模型选择、MCP 服务器、沙箱策略及技能集合，并可分配到不同频道/用户上下文。这为多租户、家庭多用户等场景提供了原生架构支持，项目在此次合并后完成了从“对话机器人”向“可编排个人代理服务器”的关键跃迁。

### 记忆子系统增强（打开中）
- **[#1074 (memory): Configurable embedding dimensions with safe auto-reindex](https://github.com/moltis-org/moltis/pull/1074)**
  `soyelmismo` 提交的 PR，为兼容 OpenAI 的嵌入服务添加可配置的向量维度，并在维度变化时自动触发安全重建索引。该项目正在系统性强化长期记忆能力的灵活性与可靠性。

---

## 4. 社区热点

### #1076 合作问询 — 生态建设信号
- **链接:** [[OPEN] Partnership inquiry — MyClaw.ai × Moltis](https://github.com/moltis-org/moltis/issues/1076)
- **热度分析:** 虽然无点赞和回复，但该 Issue 是社区热点的核心。来自 MyClaw.ai 的 Leo 主动寻求合作，其正文评价 Moltis 为 *“a serious technical project”*，并具体提到了 Rust、单二进制、沙箱化等特性。这标志着 Moltis 的技术护城河已开始吸引商业侧的目光，是项目从纯开源工具走向平台化生态的重要潜在信号。

### #1075 用户 Bug 反馈 — 功能打磨需求
- **链接:** [[Bug]: "fork" forks at prompt, not response.](https://github.com/moltis-org/moltis/issues/1075)
- **热度分析:** 用户 `vvuk` 提交的格式化 Bug 报告，严格遵守了预检清单。虽然是单一用户报告，但“在 prompt 处分叉而非 response” 暴露了 fork 功能的核心判据瑕疵，预计会引发该功能使用者的后续关注。

---

## 5. Bug 与稳定性

### 今日报告的 Bug（中等严重程度）

| Issue | 标题 | 严重程度 | 分析 | Fix PR 状态 |
|---|---|---|---|---|
| [#1075](https://github.com/moltis-org/moltis/issues/1075) | [Bug]: "fork" forks at prompt, not response. | **中** | fork 操作的触发位置逻辑错误。当用户期望 fork 一个 response 分支时，错误地在 prompt 处创建了分叉，导致对话分支不符合预期。涉及对话管理核心流程。 | 无关联 PR |

**稳定性总览：** 今日无崩溃、回归或性能退化报告。项目整体稳定性良好，此 Bug 属于功能逻辑缺陷。

---

## 6. 功能请求与路线图信号

今日无传统的“Feature Request”类 Issue，但两个 PR 给出了明确的路线图信号：

| 来源 | 方向 | 纳入下一版本的可能性 |
|---|---|---|
| **#1074 (PR)** | **可配置嵌入维度 + 安全重索引** | **极高。** 该 PR 目前已处于打开状态，直接增强了记忆子系统的兼容性和可靠性。 |
| **#1049 (已合并)** | **Agent 作为能力边界** | **已纳入主线。** 这是下一版本的架构基石，预计后续会围绕多 Agent 调度、Channel-Agent 绑定推出更多功能。 |
| **#1076 (Issue)** | **外部合作/托管平台对接（MyClaw.ai）** | 该 Issue 属于生态层面，不直接对应版本功能，但若合作落地，可能催生官方托管部署文档或 API。 |

**路线图信号总结：** 当前项目重点在 **1）记忆系统深化** 和 **2）Agent 体系形式化**，整体向“多用户、可配置、持久化的 AI Agent 服务器”方向收敛。

---

## 7. 用户反馈摘要

因今日两个 Issue 均无评论互动，以下反馈基于 Issue 正文提炼：

### 外部合作伙伴反馈（来自 #1076）
- **用户画像：** 云托管服务商（MyClaw.ai）。
- **满意点：** 认可 Moltis 的技术严肃性，尤其赞赏其 Rust 实现、单二进制交付和沙箱设计。
- **期望：** 寻求商业合作机会，暗示了托管市场的需求。

### 终端用户反馈（来自 #1075）
- **用户画像：** 深度用户/开发者（`vvuk`），能够提交符合规范的 Bug 报告。
- **痛点：** fork 功能的行为与心理模型不符，影响了分支管理的工作流。
- **满意度：** 对该功能的体验不满意，但对项目本身持积极参与态度。

### 社区互动空缺
今日所有 Issue/PR 的评论数为 0，说明维护者或社区成员尚未对这两条动态做出公开响应，这是潜在的改进点。

---

## 8. 待处理积压

以下为当前需维护者关注的项目（根据今日数据，无长时间未响应的超期积压）：

| 编号 | 类型 | 状态 | 待处理问题 | 优先度 |
|---|---|---|---|---|
| #1075 | Bug | **打开 1 天** | fork 功能判据错误，影响用户的对话分支管理体验。暂无维护者确认或回复。 | **高** — 逻辑性缺陷，且是核心交互功能。 |
| #1074 | PR | **打开中** | 记忆子系统增强 PR，待 Code Review 并决定是否合并。 | **高** — 直接功能性增强，阻塞度低但价值高。 |
| #1076 | Issue | **打开不足 24h** | 合作问询，非技术问题。 | **中** — 及时回复有利于塑造项目欢迎合作的社区形象。 |

**维护提醒：** 今日数据反映出项目在“输出代码”方面效率很高（每日有 PR 合并或提交），但在“输入响应”方面（对 Issue/PR 的首次回复）存在时滞。建议对 #1075 给出初步确认或询问，以维持社区反馈闭环的流畅性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 | 2026-05-27

## 1. 今日速览

- **活跃度极高**：过去24小时，项目共处理 **33 条 Issue**（新开22，关闭11）与 **29 个 PR**（等待合并21，合并/关闭8），社区与核心团队均保持高强度参与。
- **修复动作密集**：当日虽无新版本发布，但维护者高效合入了对聊天 UI 工具显示 (`#4695`)、上下文压缩历史错乱 (`#4294`)、音频内容兼容 (`#4383`/`#1896`) 等关键修复。
- **Beta 稳定性拉响警报**：`v1.1.9-beta.1` 被连续曝出**本地 CLI 执行失败、页面切换丢历史、任务无法入队**三大回归问题，成为今日社区讨论集中点。
- **安全事件需紧急关注**：一个 ToolGuard 绕过漏洞（允许 Agent 读取进程环境变量）被完整披露 (`#4709`)，具有高危影响，建议核心团队优先排查。

---

## 2. 版本发布

当日无新版本发布。

---

## 3. 项目进展

以下为过去24小时内被合并或取得重大进展的 PR，反映了项目在核心稳健性与平台扩展性上的投入：

- **上下文压缩 Bug 修复 ✅**：PR [#4294](https://github.com/agentscope-ai/QwenPaw/pull/4294) 合入，要求压缩后的聊天历史窗口必须以用户消息开头，彻底解决了孤立 Assistant 消息导致 UI 渲染错乱的问题（Close Issue #3984）。
- **音频消息链路打通 ✅**：PR [#4383](https://github.com/agentscope-ai/QwenPaw/pull/4383) 与 [#1896](https://github.com/agentscope-ai/QwenPaw/pull/1896) 合入，增强了对使用顶层 `data` 字段的音频源（如 Telegram Voice）的处理能力。
- **聊天界面体验修复 ✅**：PR [#4695](https://github.com/agentscope-ai/QwenPaw/pull/4695) 合入，升级 `@agentscope-ai/chat` 组件，针对性修复了**停止生成按钮**和**工具调用实时显示**的异常。
- **插件架构关键拓张 🚀**：PR [#4693](https://github.com/agentscope-ai/QwenPaw/pull/4693) 提交，允许插件通过 `api.register_channel()` 注册自定义消息渠道，前端通过后端返回的 Schema 自动渲染配置表单，为无侵入式扩展体系迈出重要一步。
- **会话状态写入加固 🛡️**：PR [#4706](https://github.com/agentscope-ai/QwenPaw/pull/4706) 提交，将 `SafeJSONSession` 的写操作改为原子写入（临时文件 + `os.replace`），防止崩溃导致的会话文件数据损毁。

---

## 4. 社区热点

- **#4644：[Bug] Console UI 工具调用不刷新令人抓狂**
  - *评论*：18 | *状态*：已关闭
  - *分析*：当日评论数第一的 Issue。用户反馈除 `read_file` 外大部分工具调用无法实时显示，必须手动刷新页面。尽管已关闭，但该问题凸显了前端 WebSocket/状态同步机制的薄弱环节，是长轮询用户的持续痛点。
  - *链接*：[Issue #4644](https://github.com/agentscope-ai/QwenPaw/issues/4644)

- **#4680：[Bug] HELP，我修改了技能名，重启后我的智能体不见了！啊啊啊啊啊**
  - *评论*：7 | *状态*：已关闭
  - *分析*：极具情绪价值的报告。用户因修改自定义技能名称后遭遇解析报错并丢失 Agent，表达了强烈的恐慌与不满。此 Issue 虽已给出解决方案，但暴露了配置变更时数据迁移与错误回滚机制的缺失。
  - *链接*：[Issue #4680](https://github.com/agentscope-ai/QwenPaw/issues/4680)

- **#4662：[Feature] 增加界面上每句话的发送时间**
  - *评论*：5 | *状态*：开放（已有对应 PR）
  - *分析*：用户 `@tina0501853` 提出消息时间戳功能，用户普遍认为在排查延迟和回顾长对话时不可或缺。社区迅速响应，贡献者 `@Gmgge` 随即提交了 PR [#4699](https://github.com/agentscope-ai/QwenPaw/pull/4699) 实现了 HH:mm:ss 时间戳。
  - *链接*：[Issue #4662](https://github.com/agentscope-ai/QwenPaw/issues/4662)

---

## 5. Bug 与稳定性

### 严重 / 高危
| ID | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#4709](https://github.com/agentscope-ai/QwenPaw/issues/4709) | ToolGuard 绕过允许 Agent 读取进程环境变量 | **安全**：通过 `execute_shell_command` 可窃取宿主机凭证与密钥。 | 开放，待紧急评估 |
| [#4704](https://github.com/agentscope-ai/QwenPaw/issues/4704) | macOS Tahoe 升级后桌面版飞书渠道崩溃 (SIGSEGV) | **崩溃**：桌面版在收消息时闪退，影响全渠道使用。 | 开放 |
| [#4706](https://github.com/agentscope-ai/QwenPaw/issues/4706) | 会话状态保存非原子操作（已有 PR） | **数据**：崩溃可能导致 JSON 文件截断、会话永久丢失。 | 已有修复 PR [4706](https://github.com/agentscope-ai/QwenPaw/pull/4706) |

### 高影响
| ID | 标题 | 分析 |
|---|---|---|
| [#4712](https://github.com/agentscope-ai/QwenPaw/issues/4712) | v1.1.9-beta.1 无法运行本地 CLI 命令 | Beta 回归，WebSocket 连接中断导致子进程无法访问本地服务。 |
| [#4714](https://github.com/agentscope-ai/QwenPaw/issues/4714) | v1.1.9-beta.1 新任务无法入队 | Beta 回归，推理期间后续请求被阻塞，必须手动停止。 |
| [#4713](https://github.com/agentscope-ai/QwenPaw/issues/4713) | v1.1.9-beta.1 切换页面后历史丢失 | Beta 回归，Session 保持机制失效，页面跳转即遗忘。 |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | MiniMax M2.5 思考过程 XML 格式不兼容 | 模型返回的 XML 思考块直接被传给 Agent，导致指令解析中断。（已持续5天） |
| [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 新建会话后 Models 配置丢失 | 切换对话导致 Models 配置页面 "Load failed"，只能通过重启解决。 |
| [#4697](https://github.com/agentscope-ai/QwenPaw/issues/4697) | 微信渠道轮询线程在热加载时被杀死 | 工作区重载导致 Event Loop 关闭，且无自动恢复机制。 |
| [#4710](https://github.com/agentscope-ai/QwenPaw/issues/4710) | 向量数据库 MemoryNode 时间戳时区不一致 | Naive datetime vs UTC 元数据，潜在打乱检索排序的风险。 |

---

## 6. 功能请求与路线图信号

- **企业级平台信号强**：`#4702` 明确提出 **RBAC 多用户管理** 需求；`#4408` 与 `#4642` 共同提出**统一工作目录**。这些均是企业选型时评估 CoPaw 作为企业内部 AI 中枢的核心准入指标。
- **插件系统生态成型在即**：`#4642` 是一份厚重的路线图式建议，系统阐述了 Context/Memory/Hook/Tool/Channel 五大组件的非侵入式插件化构想。今日开放的 PR `#4693`（Schema 驱动自定义 Channel）正是该构想的落地方案，标志项目正式向“可组装 AI 引擎”演进。
- **对话交互体验精细化**：`#4703`（Fork/Rewind/Regen）和 `#4662`（时间戳）代表了用户对 Pro 级对话控制能力的追求。前者需要架构支持，后者已有社区贡献 PR 即将落地。
- **国产基础设施融合加速**：`#4711`（新增元宝频道）与 `#4715`（新增小米 MiMo Token Plan Provider）表明社区正积极将 CoPaw 嵌入更广泛的国产 AI 生态中。

---

## 7. 用户反馈摘要

- **“我的数据还安全吗？”—— 数据完整性焦虑**：用户在 `#4680`（智能体消失）和 `#4713`（历史丢失）中表现出强烈的不安与挫折感。Bug 修复之外，配置变更的**安全备份与引导式恢复**机制是提升用户信任度的关键。
- **“难道我要去改源码？”—— 高阶用户的定制化诉求**：`@zhufeizzz` 在 `#4642` 中直言“可扩展能力相比 OpenClaw 差距较大”、“需要侵入式修改源码”。这代表了社区中领先用户对**插件化 Hook 机制**的强烈渴求，他们期待 CoPaw 是一个可以被编程的 AI 引擎，而非固定功能的应用。
- **“为什么隔壁能跑，就你不能跑？”—— Beta 口碑风险**：用户 `@rescodexa` 在 `#4712` 中不满地指出“openclaw/opencode 都能正常执行”。这种横向对比带来的“口碑落差”是项目在 Beta 阶段必须高度重视的信号。
- **“能不能别忘了这种小细节？”—— 对基础 UX 的更高要求**：消息时间戳（`#4662`）、技能同步状态可视化（`#3327`）、多步工具调用一次批准（`#4701`）等高频细节需求，表明用户已不再停留在“能用”阶段，而是追求“优雅地用”。

---

## 8. 待处理积压

| ID | 创建时间 | 标题 | 积压原因 / 风险 |
|---|---|---|---|
| [#4006](https://github.com/agentscope-ai/QwenPaw/issues/4006) | 2026-05-02 | OpenAI 兼容 Provider 的 Reasoning Content 过滤问题 | 长达 25 天未关闭。关联 PR `#4689`（通过 extra_body 解决 generate_kwargs 问题）可能部分覆盖，但 Issue 标签未更新。 |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | 2026-05-22 | MiniMax M2.5 模型 XML 思考格式不兼容 | **严重度高**，影响区域广泛用户群体。已持续 5 天无官方解决方案。建议在 Provider 层增加对非法 XML 标签的过滤或回退逻辑。 |
| [#4642](https://github.com/agentscope-ai/QwenPaw/issues/4642) | 2026-05-23 | 全面插件系统及工作目录优化建议 | **路线图级建议**，无 Assignee。建议纳入项目 Milestone 讨论，系统规划非侵入式插件架构的落地时间表。 |
| [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 2026-05-25 | 新建会话 Models 配置丢失 | **严重 Bug**，操作路径极短（新建会话即可触发），但官方至今未给出正式回复或临时 Workaround。 |
| [#4704](https://github.com/agentscope-ai/QwenPaw/issues/4704) | 2026-05-26 | macOS Tahoe 飞书渠道崩溃 | 系统更新后的兼容性崩溃，桌面版用户升级新系统后有“劝退”风险。 |

---
**总结**：CoPaw 过去24小时处于高频迭代与活跃反馈并行的状态。社区对 Beta 稳定性的批评、对插件架构的期待、以及对基础 UX 细节的追求，共同勾勒出项目从“个人玩具”走向“企业级 AI 中枢”过程中的甜蜜与阵痛。建议维护者优先响应安全漏洞 (`#4709`) 与企业级 Bug (`#4666`)，同时妥善回应社区领袖贡献的路线图建议 (`#4642`)，以保持社区贡献热度。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，以下是根据 ZeptoClaw（https://github.com/qhkm/zeptoclaw）在 2026 年 5 月 26 日（对应 5 月 27 日发布日报）的数据生成的每日项目动态报告。

---

## ZeptoClaw 项目动态日报 | 2026-05-27

### 1. 今日速览
过去 24 小时，ZeptoClaw 项目处于 **“基础设施活跃但社区静默”** 的状态。自动化依赖管理工具 Dependabot 极为活跃，共计提交了 **16 个依赖更新 PR** ，其中 2 个已合并，14 个待处理。然而，社区人工互动几乎停滞，新 Issues、手动 PR 及用户评论数均为零。项目整体健康度在代码依赖层面得到自动维系，但缺乏核心功能迭代与社区热点讨论，活跃度评估为 **“平稳维护期”**。

### 2. 版本发布
过去 24 小时内无新版本发布。

### 3. 项目进展
今日项目推进主要由 Dependabot 的自动化合并构成：
- **已合并/关闭的 PR：**
    - **#578**：将 `landing/zeptoclaw/docs` 目录下的 `astro` 依赖从 `6.1.6` 升级至 `6.3.1`（[查看详情](https://github.com/qhkm/zeptoclaw/pull/578)）。
    - **#572**：将 `landing/r8r/docs` 目录下的 `@astrojs/starlight` 依赖从 `0.38.3` 升级至 `0.39.2`（[查看详情](https://github.com/qhkm/zeptoclaw/pull/572)）。
- **核心进展评估：** 今日无核心业务逻辑或架构变更。项目进展仅限于文档站点的依赖版本更新，代码核心库（如 Rust 后端）的待批 PR 仍在积压中。

### 4. 社区热点
今日社区无热点。过去 24 小时内 **0 条 Issues** 被创建，且所有 PR 均无用户评论（仅包含 Dependabot 的自动摘要）。社区讨论区处于绝对静默状态，无任何诉求表达或技术讨论。

### 5. Bug 与稳定性
今日未报告新的 Bug、崩溃或回归问题。结合当前活跃的依赖更新动作，项目近期稳定性表现良好，或处于用户深度使用磨合前的空窗期。

### 6. 功能请求与路线图信号
无。过去 24 小时未收集到任何用户提交的功能需求或路线图建议。

### 7. 用户反馈摘要
无数据可供分析。本期无人工提交的 Issues 或 PR 评论。

### 8. 待处理积压
维护者需重点关注 14 个待合并的 Dependabot PR，当前已形成一定的更新积压。按优先度排列如下：

- **高优先级（编译与安全环境）：**
    - **#596** `[docker] chore(deps): bump rust from 1.93-slim-trixie to 1.95-slim-trixie`：[查看详情](https://github.com/qhkm/zeptoclaw/pull/596)
        - *风险提示：涉及跨版本的 Rust 编译器升级，可能对 `tower-http`、`clap`、`bcrypt` 等底层库引入编译兼容性问题。*
    - **#595** `[docker] chore(deps): bump debian from ...`：[查看详情](https://github.com/qhkm/zeptoclaw/pull/595)
        - *基础镜像安全更新，建议优先合并。*

- **核心依赖积压：**
    - **#606** `tower-http 0.6.8 -> 0.6.10`（[链接](https://github.com/qhkm/zeptoclaw/pull/606)）
    - **#603** `mail-parser 0.11.2 -> 0.11.3`（[链接](https://github.com/qhkm/zeptoclaw/pull/603)）
    - **#601** `uuid 1.23.0 -> 1.23.1`（[链接](https://github.com/qhkm/zeptoclaw/pull/601)）
    - **#598** `bcrypt 0.19.0 -> 0.19.1`（[链接](https://github.com/qhkm/zeptoclaw/pull/598)）

- **CI/CD 管线维护：**
    - **#604** `taiki-e/install-action`（[链接](https://github.com/qhkm/zeptoclaw/pull/604)）
    - **#597** `EmbarkStudios/cargo-deny-action`（[链接](https://github.com/qhkm/zeptoclaw/pull/597)）

- **重复 PR 清理提醒：**
    - 当前存在重复的依赖更新场景：`#607`（[链接](https://github.com/qhkm/zeptoclaw/pull/607)）与已合并的 `#578` 内容重复；`#599`（[链接](https://github.com/qhkm/zeptoclaw/pull/599)）与已合并的 `#572` 内容重复。建议维护者关闭重复项，避免后续合并策略混乱。

---

**总结：** 依赖管理自动化运转良好，项目处于“被动维护”模式。建议维护者尽快安排一次批量合并，清理积压的 Dependabot PR，并评估 Rust 基础镜像升级可能带来的影响。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，这是根据ZeroClaw项目2026年5月27日的GitHub数据生成的动态日报。

---

## ZeroClaw 项目动态日报 | 2026-05-27

### 1. 今日速览

今日ZeroClaw项目整体活跃度极高，开发节奏显著加快。过去24小时内，项目收到34条PR更新，其中大部分（29条）处于待合并状态，显示出社区贡献者提交了大量密集的改进和修复工作。与此同时，新开问题数量有所回落（6条），且未出现新的版本发布，项目组可能正专注于消化当前大量的PR，以便进行下一次集中发布。重点关注：一个涉及DeepSeek-V4 API兼容性的高风险Bug仍在处理中，社区围绕键盘快捷键和交互模式的改进呼声很高，多个高风险的技能系统、自动化编排等工作正在等待合并。

### 2. 版本发布
无。

### 3. 项目进展

过去24小时内有5个PR被合并或关闭，主要聚焦于Bug修复和稳定性提升，涉及邮件通道、多提供者兼容性等关键模块。

-   **核心通道修复 (`#6512`)**: 邮件 (`channels/email`) 通道是今天的明星。PR `#6512` 被合并，修复了邮件通道的 **HTML正文渲染**、**邮件主题线程**和**附件路径解析**问题。这是一次针对邮件通道可用性的重大提升，解决了零字节附件和Markdown渲染为纯文本等严重可用性问题。
    - 链接: [zeroclaw-labs/zeroclaw PR #6512](https://github.com/zeroclaw-labs/zeroclaw/pull/6512)
-   **诊断能力提升 (`#6901`)**: 合并了 `#6901`，修复了提供者 (`provider`) 传输层的错误诊断信息丢失问题。现在，当API调用失败时（如超时、DNS解析失败），错误日志将保留完整的根源追踪信息，极大方便了运维和调试。
    - 链接: [zeroclaw-labs/zeroclaw PR #6901](https://github.com/zeroclaw-labs/zeroclaw/pull/6901)

### 4. 社区热点

社区的讨论焦点集中在 **键盘快捷键** 和 **DeepSeek-V4兼容性** 上。

-   **热度第一: TUI键盘快捷键** (`#6950`, `#6952`)
    围绕紧凑型键盘（如Logitech MX Keys Mini）无法使用功能键 (F-keys) 切换TUI模式的问题，引发了集中讨论。用户 `theonlyhennygod` 不仅提交了 `Issue #6950`，还连续提交了 **两个 PR (`#6950` 和 `#6952`)** 来提出解决方案，分别提议使用 `Alt+数字键` 和 `Tab/Shift+Tab` 进行切换。这表明**TUI的易用性和跨硬件兼容性**是当前社区开发者高度关注的痛点。
    - 链接: [Issue #6950](https://github.com/zeroclaw-labs/zeroclaw/issues/6950)
    - 链接: [PR #6952](https://github.com/zeroclaw-labs/zeroclaw/pull/6952)
-   **长期热点: DeepSeek-V4 API 不兼容** (`#6059`)
    尽管是历史问题，但 `Issue #6059` 仍然保持活跃，已有13条评论。用户报告在调用DeepSeek最新的V4版本API时，因为“思考模式” (`thinking mode`) 兼容性问题导致功能失效。该issue被标记为 `risk: high` 和 `status: in-progress`，说明项目团队已确认此问题并正在修复中，这是当前影响用户使用的主要瓶颈之一。
    - 链接: [Issue #6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)

### 5. Bug 与稳定性

今日报告了3个新Bug，另有1个高风险的老Bug持续受关注。

-   **高风险 (High Risk):**
    -   **DeepSeek-V4 兼容性 (`#6059`)**: 高风险Bug，S2级别，导致DeepSeek-V4 Pro和Flash版本API均告失效。状态为 `in-progress`，已开发专门修复。
        - 链接: [Issue #6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)
-   **中低风险 (Medium/Low Risk):**
    -   **TUI模式切换键绑定问题 (`#6950`)**: Bug，但已有社区PR (`#6952`) 尝试修复。
        - 链接: [Issue #6950](https://github.com/zeroclaw-labs/zeroclaw/issues/6950)
    -   **交互模式日志干扰 (`#6944`)**: S2级别，在终端交互模式下，系统的INFO/WARN日志与AI对话内容混杂，严重影响阅读体验。已有PR `#6947` 完成了修复。
        - 链接: [Issue #6944](https://github.com/zeroclaw-labs/zeroclaw/issues/6944)
        - 链接: [PR #6947](https://github.com/zeroclaw-labs/zeroclaw/pull/6947)

### 6. 功能请求与路线图信号

用户提出的新功能请求显示出对 **桌面控制能力** 和 **任务编排** 的兴趣，这与当前Agent发展的主流趋势一致。

-   **桌面控制 (computer-use) (`#6909`)**: 这是一个重要的路线图信号。用户 `NiuBlibing` 请求增加类似OpenAI Codex的“计算机使用”能力，让Agent能够控制鼠标键盘、截图，从而操作桌面GUI。这属于`enhancement`和`type:rfc`，意味着这是一个需要评审的设计性功能，很可能被纳入未来的里程碑。
    - 链接: [Issue #6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)
-   **任务调度流程优化 (`#6954`)**: 社区提出了一个系统性的RFC，建议将定时任务（Cron）的执行纳入编排器（Orchestrator）的消息管道中，而不是直接触发。这旨在解决由调度器绕过安全检查、上下文管理导致的一系列关联Bug。这显示了社区对系统鲁棒性和可观测性的更高要求。
    - 链接: [Issue #6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)
-   **代码级特性: 已纳入PR**
    - **MCP工具策略 (`#6920`)**: PR允许在运行时动态过滤MCP的工具，实现深度防御。这是对安全性和可控性的重要增强。
    - **技能内建工具 `kind` (`#6924`)**: PR允许技能声明 `kind = "builtin"` 的工具，实现技能级别的权限提升，避免授权泛滥。
    - **按Agent配置分类模型 (`#6945`)**: 提议允许为`类意图`任务配置一个更便宜的模型，以降低运营成本。

### 7. 用户反馈摘要

-   **痛点**:
    -   使用DeepSeek-V4的用户遭遇了“思考模式”兼容性错误，导致API完全不可用，这是目前最突出的用户反馈 (Issue #6059)。
    -   使用紧凑型键盘（如MacBook Pro、Keychron）的用户吐槽TUI默认的F-keys快捷键设计糟糕，完全无法使用，迫使他们需要修改键位绑定或更换键盘 (Issue #6950)。
    -   交互模式下的结构化日志输出严重干扰了正常聊天，用户反馈称“对话文字难以阅读” (Issue #6944)。
-   **满意点**:
    -   社区对PR `#6952` (Tab切换) 和 `#6947` (日志修复) 的快速响应表现出积极态度，表明社区对开发者采纳反馈的速度是满意的。
    -   邮件通道的修复 (PR #6512) 解决了用户日常使用中的文件分享和阅读体验问题，是社区普遍期待的修复。

### 8. 待处理积压

以下为已开放较长时间但仍未解决或等待作者/维护者回复的重要事项，需项目维护者关注。

-   **高风险未修复Bug**:
    - `#6059` **DeepSeek-V4 API 不兼容**: 已开放超过一个月（2026-04-24），虽标记为`in-progress`但尚未关闭，严重影响相关用户。
        - 链接: [Issue #6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)
-   **等待作者行动 (needs-author-action)**:
    - `#6684` **技能冷却修复**: 已开放12天，标记为`risk: high`，但作者长时间未回应，阻止了该问题与另一重大功能PR (`#6667`) 的集成。
        - 链接: [PR #6684](https://github.com/zeroclaw-labs/zeroclaw/pull/6684)
    - `#6667` **背景技能审查特性**: 这是一个XL级别的增强，风险高，但目前阻塞在作者行动上。
        - 链接: [PR #6667](https://github.com/zeroclaw-labs/zeroclaw/pull/6667)
    - `#6688` **委派代理技能注入模式修复**: 同样标记为`needs-author-action`，影响委派代理对系统配置的遵循。
        - 链接: [PR #6688](https://github.com/zeroclaw-labs/zeroclaw/pull/6688)

**项目健康度总结**: 项目开发活跃度极高，社区参与积极，PR提交数量巨大。当前主要风险在于大量高风险的PR和Bug处于积压状态，尤其是技能系统和DeepSeek兼容性这两个核心模块。项目组未来几天的工作重心应放在合并/处理这些积压的PR上，以释放已完成的开发成果，并解决最为紧迫的DeepSeek兼容性问题。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*