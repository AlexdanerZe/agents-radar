# OpenClaw 生态日报 2026-06-21

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-21 03:52 UTC

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

好的，以下是基于您提供的 GitHub 数据生成的 OpenClaw 项目动态日报（2026-06-21）。

---

## OpenClaw 项目动态日报 — 2026-06-21

---

### 1. 今日速览

OpenClaw 项目今日维持了极高的迭代强度，24小时内处理了超过 **500 条 Issue** 与 **500 条 PR** 更新，并发布了 v2026.6.9 补丁。尽管新版本加强了 Telegram 通道的富文本交付能力，项目当前正承受着巨大的稳定性压力：一个 **P0 级 Gateway 内存泄漏**（[#91588]）和多个 **P1 级会话状态/消息丢失回归**（[#88312]、[#86519]）正成为社区焦点。从大量 `clawsweeper:no-new-fix-pr` 和 `clawsweeper:needs-maintainer-review` 标签来看，项目维护团队虽在全力追赶，但修复积压已成治理挑战。项目整体在高压下仍显韧性，核心功能（Codex、Cron、Session 恢复）的重构正在密集进行中。

---

### 2. 版本发布

*   **版本号：** `v2026.6.9`
*   **更新内容：**
    *   **Richer Telegram delivery：** 电报消息交付能力显著提升。现在支持发送富 HTML、保留富 Markdown 和贴纸路径、更精确地渲染进度草稿和命令输出、安全地归一化 HTML 表格，并将提及和 Spooled Handlers 放置在正确的交付路径上。（关联 PRs [#93286] [#93164] 等）
*   **破坏性变更 / 迁移注意事项：**
    *   未明确列出破坏性变更。本次更新涉及底层渲染逻辑调整，原有消息的最终呈现样式（尤其是 Markdown 和 HTML 混合场景）可能会有变化。建议在测试通道充分验证后再进行大规模生产环境升级。

---

### 3. 项目进展

**已合并/关闭的 PR：**

*   **[PR #68936] (Merged)：** 新增了 **PR Review 自动修复流水线**（核心逻辑 ~785 行）以及 **Windows 后台守护进程**。这是重量级的基建提升，极大降低了 Windows 用户的运维门槛并加速代码评审效率。
*   **[PR #93241] (Merged)：** 修复了智谱 GLM 模型超载错误未被正确归类为 `overloaded` 的问题，使得模型的故障转移（Failover）机制能够生效，提升了特定模型在负载高峰期的可用性。

**关键推进中的 PR：**

*   **安全加固：** [PR #84738]（阻止明文写入 API Key 到 `models.json`）和 [PR #84645]（物化 `python -c` / `node -e` 等内联解释器执行前的安全审批逻辑）正在推进，体现了项目对安全边界的重视。
*   **Codex 架构重构：** [PR #93313] 正在对 Codex 集成进行深度重构，统一运行时所有权，有望从根本上解决 Codex 相关的状态混乱和交付延迟问题。
*   **核心痛点修复：** [PR #95460] 关注模型“幻觉”文档扩展名（`.docodex` → `.docx`）的自动修正，这是一个极其影响日常体验的痛点修复。

---

### 4. 社区热点

*   **[#88838] (31条评论) – 核心会话/转录 SQLite 迁移规划：** 社区主力开发者们正在激烈讨论如何以“Branch by Abstraction”模式进行路线级别的架构重写，避免超大 PR 的风险。这代表了社区对项目长期架构稳定性的深度参与。
*   **[#88312] (16条评论, 4👍) – Codex Turn-Completion 挂起回归：** 社区用户 Yair 做了教科书级的回归报告，精确 Bisect 到破坏版本（2026.5.27）。背后是 Codex 用户对实时交互稳定性的极度渴求。
*   **[#91588] (13条评论) – Gateway 内存泄漏至15.5GB：** 运维人员的头号噩梦。RSS 持续增长直至 OOM Kill，导致 `launchd-handoff` 循环重启，严重威胁生产环境。
*   **[#86519] (10条评论) – Telegram 重复消息：** 尽管在 5.22 降级，该问题仍未彻底消失。社区对此“感知度高、容忍度低”的 Bug 表达了明显不满。
*   **[#91363] (6条评论, 4👍) – Isolated Cron 彻底不可用：** 虽评论数不多，但获得了最多的关注，说明大量用户被这个隐藏较深的问题所困扰。

---

### 5. Bug 与稳定性

**P0 (Critical)：**
*   **Gateway 内存泄漏 [#91588]：** RSS 从 350MB 增长至 15.5GB，导致进程被 OS OOM Killer 杀除。*(当前无已关联 Fix PR)*

**P1 (高影响)：**
*   **Codex 回归 [#88312]：** Turn-completion 卡死，ChatGPT Plus 用户被阻塞。*(当前无已关联 Fix PR)*
*   **Anthropic Thinking 签名失效 [#94228]：** 长对话被 `Invalid signature` 错误阻塞。*(当前无已关联 Fix PR)*
*   **Isolated Cron 彻底失败 [#91363]：** 模型调用从未到达 Provider。*(当前无已关联 Fix PR)*
*   **推理逻辑泄露 [#91804]：** 隐私与 UX 的双重回归，内部思考过程暴露给用户。*(需安全审查)*
*   **投递恢复失败 [#91212]：** Gateway 重启后 WebSocket 未就绪即执行恢复，消息静默丢失。*(当前无已关联 Fix PR)*
*   **Session/Model 状态不一致 [#92415]：** `/model` 切换后快照不刷新。*(关联 PR 已打开)*
*   **Telegram 重复消息 [#86519]：** 严重用户体验问题。*(待维护者审查)*
*   **Doctor 慢 4-5x [#85333]：** 主要运维命令性能退化。*(待维护者审查)*
*   **Compaction 超时设计缺陷 [#92043]：** 180s 单次壁钟超时导致合法长任务持续失败。*(关联 PR 已打开)*
*   **内网访问失败 [#94032]：** `exec` 工具无法访问局域网资源。*(关联 PR 已打开)*

**P2 (中等影响)：**
*   **web_fetch 忽略 NO_PROXY [#93807]：** 代理安全配置失效。*(关联 PR 已打开)*
*   **launchd 屏蔽 stderr [#90711]：** 隐藏关键诊断日志。*(关联 PR 已打开)*
*   **Doctor 注入错误路径 [#85334]：** 导致启动循环警告。*(关联 PR 已打开)*

---

### 6. 功能请求与路线图信号

*   **会话与内存优化：**
    *   **[#90916] (P2)：** 提出成熟的 **“Topic-session families”** 概念，旨在让一个 Agent 拥有多个独立的上下文“话题车道”，同时共享层级记忆。该方案设计成熟，获社区讨论认可，极有可能成为下阶段的功能亮点。
    *   **[#90354] (P2)：** 请求为预压缩内存刷写增加边界校验。标签 `fix-shape-clear` 已存在，说明功能设计已获维护者认可。
*   **平台通道新特性：**
    *   **[PR #83632] (Open)：** Telegram 访客模式，允许外部用户临时调用 Bot，扩展社交场景。
    *   **[PR #83531] (Open)：** 飞书表情反应工具，增强交互性。
*   **工具链与性能：**
    *   **[#14785] (P2, 积压4个月)：** 降低工具 Schema Token 开销（~3500 tokens/会话）。虽然长期未推进，但其优化价值极高，一旦实施将惠及所有会话的冷启动。
    *   **[PR #85359] (Open)：** 本地技能路由工具，让 Agent 能自主感知并推荐可用技能。

---

### 7. 用户反馈摘要

*   **对核心稳定性下降的担忧加剧：**
    > “我的 Gateway 在运行 2-3 天后 RSS 会从 350MB 涨到 15.5GB 然后被杀死。这让我不得不编写脚本每天重启，严重影响了我们的自动化流水线。” —— 摘自 [#91588]
    > “`openclaw doctor --fix` 现在需要近 4 分钟，而在之前只需要不到 1 分钟。我用的还是 24GB 内存的服务器。” —— 摘自 [#85333]
*   **对渠道交付退化的不满：**
    > “重复消息的问题在 5.22 版本中只是变少了，并没有消失。我们的团队因为这个频繁的重复回复感到非常困惑，甚至影响了用户对 Bot 的信任。” —— 摘自 [#86519]
*   **对 Codex 集成的“零容忍”态度：**
    > “这是一个非常明确的回归。5.26 正常，5.27 就坏了。之前修过（#84076, #85107），现在又烂了。我们无法接受这种反复。” —— 摘自 [#88312]
*   **细致入微的运维发现：**
    > “我发现 `launchd` 生成的 plist 将 stderr 硬编码重定向到了 /dev/null，这导致我根本无法排查模型提示词缓存命中率为什么下降，所有 `[prompt-cache]` 警告全丢了。” —— 摘自 [#90711]

---

### 8. 待处理积压

*   **[#14785] (2026-02, P2)：** 减少工具 Schema Token 开销。长期高价值优化请求，建议项目团队尽快分配资源进入设计阶段，以压缩每次会话的固定成本。
*   **[#85333] (2026-05, P1)：** `doctor --fix` 性能衰退。作为核心维护命令，其 P1 优先级与 `clawsweeper:no-new-fix-pr` 的状态存在矛盾，急需维护者决策是否需要紧急修复通道。
*   **[#85334] (2026-05, P2)：** `doctor --fix` 注入错误路径导致循环警告。该问题影响新用户的“开箱”体验，修复 PR 已打开但长期搁置，建议优先合并。
*   **[#88870] (2026-06, P1)：** 卡顿会话恢复机制误杀长时间活跃任务。关联 PR 已打开等待审查，该问题可能导致用户长时间运行的任务结果被错误中断。
*   **[#90595] (2026-06, P2)：** Cron 失败通知在热重载时频繁误报，导致告警疲劳。这类“狼来了”式的告警会严重削弱运维监控系统的可信度，需要尽快修复源端过滤逻辑。

[#88838]: openclaw/openclaw Issue #88838
[#88312]: openclaw/openclaw Issue #88312
[#91588]: openclaw/openclaw Issue #91588
[#85333]: openclaw/openclaw Issue #85333
[#86519]: openclaw/openclaw Issue #86519
[#91363]: openclaw/openclaw Issue #91363
[#92415]: openclaw/openclaw Issue #92415
[#91804]: openclaw/openclaw Issue #91804
[#91212]: openclaw/openclaw Issue #91212
[#94228]: openclaw/openclaw Issue #94228
[#92043]: openclaw/openclaw Issue #92043
[#94032]: openclaw/openclaw Issue #94032
[#93807]: openclaw/openclaw Issue #93807
[#90711]: openclaw/openclaw Issue #90711
[#85334]: openclaw/openclaw Issue #85334
[#88870]: openclaw/openclaw Issue #88870
[#90595]: openclaw/openclaw Issue #90595
[#90916]: openclaw/openclaw Issue #90916
[#90354]: openclaw/openclaw Issue #90354
[#14785]: openclaw/openclaw Issue #14785
[#68936]: openclaw/openclaw PR #68936
[#93241]: openclaw/openclaw PR #93241
[#84738]: openclaw/openclaw PR #84738
[#84645]: openclaw/openclaw PR #84645
[#93313]: openclaw/openclaw PR #93313
[#95460]: openclaw/openclaw PR #95460
[#83632]: openclaw/openclaw PR #83632
[#83531]: openclaw/openclaw PR #83531
[#85359]: openclaw/openclaw PR #85359
[#85381]: openclaw/openclaw PR #85381
[#93286]: openclaw/openclaw PR #93286
[#93164]: openclaw/openclaw PR #93164

---

## 横向生态对比

# 个人 AI 智能体开源生态横向分析报告（2026-06-21）

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于“功能爆炸与稳定性欠账并存”的极化阶段。头部项目（OpenClaw、Hermes Agent、ZeroClaw）单日处理 500+/50+/50+ 级 Issue/PR，功能快速推进，但 P0/P1 级内存泄漏、消息静默丢失、上下文崩溃等回归问题持续消耗社区信任；腰部项目（NanoBot、CoPaw、NanoClaw）则展现出更高的修复效率和社区协作质量，往往在 Bug 报告当天即涌现多个修复方案。与此同时，Token 成本焦虑、安全左移、Agent 自我认知缺陷正从“用户抱怨”升级为架构级路线信号，驱动项目集体向精细化、可观测、低成本方向演进。

## 2. 各项目活跃度对比（过去 24h）

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| OpenClaw | 500+ | 500+ | v2026.6.9 | 高压韧性，稳定性待加强 |
| Hermes Agent | 50+ | 50+ | 无 | v0.17.0 Gateway 崩溃已修复，Token 问题仍突出 |
| ZeroClaw | 50+ | 50+（46 待合并） | 无 | 极高活跃，S0/S1 级 Bug 并存 |
| IronClaw | 未明确 | 21（9 合并） | 无 | 迭代迅猛，Nightly E2E 持续失败（25 天） |
| NanoBot | 4 | 18 | 无 | 健康高产，SDK 并发 Bug 当日修复 |
| CoPaw (QwenPaw) | 10 | 9 | 无 | 中等偏上，新人贡献质量高 |
| NanoClaw | 1 | 6（均开放） | 无 | 稳定积累，安全加固期 |
| PicoClaw | 2（已有） | 1（PR #2964 停滞） | nightly | 中等活跃，维护者决策停滞 |
| Moltis | 0 | 2（Dependabot） | 无 | 稳定维护，依赖自动更新 |
| NullClaw | 1（#967） | 0 | 无 | 低活跃，高频 Bug 待响应 |
| LobsterAI | 0 | 0 | 无 | 低活跃，5 个陈旧 Bug 自动关闭 |
| TinyClaw | — | — | 无 | 无活动 |
| ZeptoClaw | — | — | 无 | 无活动 |

## 3. OpenClaw 在生态中的定位

OpenClaw 是当前社区规模最大（单日 500+ Issue/PR）、功能覆盖最广的个人 AI 助手框架，涵盖 Codex 集成、Cron 调度、Gateway 网关、多通道交付（Telegram 增强）、PR 自动修复流水线等。其技术路线偏向“全栈式底座”，正进行底层 SQLite 迁移、Codex 架构重构、安全边界加固等大规模重构，表现出典型旗舰项目的激进迭代特征。与同类相比：

- **vs Hermes Agent**：Hermes 更侧重 Desktop 体验与 OpenAI 生态，Token 优化呼声更高；OpenClaw 在自动化和通道多样性上领先，但同样面临回归重复出现的问题。
- **vs NanoBot**：NanoBot 以轻量 Python SDK 为核心，面向快速集成，并发安全处理模式（`contextvars`）优于 OpenClaw 的钩子机制，但功能广度不及 OpenClaw。
- **vs ZeroClaw**：ZeroClaw 在自动化（Cron、Skills）和记忆（Dream Mode）上有独特设计，社区活跃度接近，但 OpenClaw 的版本发布节奏（当日补丁）和基础设施（Windows 守护进程）更为成熟。

**核心优势**：生态规模、自动化基建、安全与重构投入；**核心挑战**：回归控制、修复积压（`clawsweeper:no-new-fix-pr` 标签泛滥）。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 / 对应 Issue/PR |
|---|---|---|
| **Token 成本优化** | Hermes, NanoBot, OpenClaw | Hermes #6839 Lazy Tool Schema（13👍），NanoBot #4420 Token 缓存，OpenClaw #14785 降低 Schema 开销（积压4个月） |
| **安全与沙箱隔离** | NanoClaw, CoPaw, OpenClaw | NanoClaw CVE-2026-29611 路径穿越修复（PR #2799），CoPaw PR #5346 Docker 工具隔离（First-time），OpenClaw PR #84738 阻止 API Key 明文写入 |
| **会话 / 上下文管理** | ZeroClaw, CoPaw, Hermes | ZeroClaw #5808 32K 上下文首次超限 3.3×，CoPaw PR #5321 Scroll 持久化上下文，Hermes #43066 上下文压缩丢失 |
| **Agent 工具自认知** | ZeroClaw, Hermes, PicoClaw | ZeroClaw #5862 模型不知自身可添加 cron，Hermes #6839 可按需加载工具，PicoClaw #2984 显式 Turn 结束信号 |
| **多平台渠道覆盖** | NanoBot, OpenClaw, IronClaw | NanoBot iMessage 合并、Telegram 富文本，OpenClaw Telegram 增强，IronClaw Manifest 驱动渠道统一 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 全功能个人助手 + 自动化流程 | 高级开发者、运维 | 模块化 Gateway，Python/Rust 混合，大规模重构推进中 |
| **NanoBot** | 轻量 SDK + 多渠道覆盖 | Python 开发者、集成商 | 纯 Python asyncio，`contextvars` 并发，iMessage Node.js 侧车 |
| **Hermes Agent** | Desktop + Telegram + 商业模型 | Desktop 用户、OpenAI 用户 | 插件式 Gateway，CI 门禁，Token 高消耗 |
| **IronClaw** | 高性能 Rust Agent 框架 | 企业级部署 | Rust 实现，Reborn 架构，并发 Turn 调度 |
| **ZeroClaw** | 自动与记忆平台 | 自动化玩家、技能开发者 | v0.9.0 Auth 路线，Dream Mode 记忆整合，Skills 平台 |
| **CoPaw (QwenPaw)** | 企业级 Agent + Qwen 生态 | Qwen 模型使用者、安全要求高 | ReAct 循环可观测性（Langfuse），Docker 沙箱，Scroll 上下文 |
| **PicoClaw** | 嵌入式 / 边缘 Agent | 嵌入式开发者 | SiPEED RISC-V，极简资源占用，协议层待完善 |
| **NanoClaw** | 极致精简 + 安全 | 安全敏感场景 | 去除全局内存，CVE 修复快速，CI 持续 |

## 6. 社区热度与成熟度分层

| 层级 | 项目 | 特征 |
|---|---|---|
| **快速迭代层**（每日 50+ 更新） | OpenClaw, Hermes Agent, ZeroClaw, IronClaw | 功能快速推进，但稳定性波动大；修复多与回归并存，需用户密切关注版本兼容性 |
| **质量巩固层**（每日数～十余更新） | NanoBot, CoPaw, NanoClaw | 社区协作效率高，Bug 当日修复，代码 Review 严谨；适合生产环境逐步采用 |
| **维护静默层**（偶有更新或停滞） | PicoClaw, NullClaw, LobsterAI, Moltis | 核心贡献者资源短缺，高质量 PR 无人 Review；用户 Bug 长期未响应，存在流失风险 |
| **无活动层** | TinyClaw, ZeptoClaw | 仓库冻结或失去维护，不建议选型 |

**成熟度信号**：NanoBot 和 NanoClaw 虽然在更新量上不及头部，但修复速度和架构决策成熟度（如 `contextvars` 方案、CVE 当日处理）远超同等规模项目，是“小而精”的代表。

## 7. 值得关注的趋势信号

1. **Token 成本已从“抱怨”升级为“路线级约束”**  
   Hermes #6839（13👍）、ZeroClaw #5808（首次交互即超限）、NanoBot #4420（Token 编码成为瓶颈）共同指向：**工具 Schema 动态化、系统提示压缩、上下文预算自适应**将成为下一波 Agent 框架的核心竞争点。开发者应尽早将 Token 计量纳入架构设计，而非事后优化。

2. **Agent 安全左移成为选型硬指标**  
   NanoClaw 的 CVE 修复、CoPaw 的 Docker 沙箱、OpenClaw 的 API Key 保护，说明**一次性隔离不足以保证 Agent 运行时安全**。社区开始要求“默认安全”的沙箱策略和最小权限设计，尤其在容器化和 multi-tenant 场景下。

3. **Agent “自我能力认知”限制自动化深度**  
   ZeroClaw #5862 和 Hermes #6839 暴露了同一痛点：**模型不知道自身拥有哪些工具**。这导致用户需用自然语言“命令”模型调用工具，而非模型自主推断。未来框架需在系统提示或向量工具库中动态注入能力清单，提升 Agent 自主性。

4. **移动端与实时交互体验不再是“加分项”而是“必需品”**  
   CoPaw #5329（侧边栏被挤出屏幕）和 Hermes #49903（Desktop 升级后 Composer 不可用）表明：**Agent WebUI/Desktop 正在成为高频接触点**，响应式设计、离线能力、语音通知成为用户留存的关键。

5. **可观测性从“运维工具”演变为“调试大脑”**  
   CoPaw 合并了 Langfuse 在 ReAct 循环级的 Trace 优化（PR #5128），ZeroClaw 有待审的结构化可观测性增强（#7232）。**细粒度 Trace + 上下文快照**将是诊断 Agent 行为异常（如幻觉、工具循环）的唯一可靠手段，建议项目早期就嵌入。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是基于你提供的 GitHub 数据生成的 NanoBot 项目动态日报。

---

### 📅 NanoBot 项目动态日报 | 2026-06-21

#### 1. 今日速览
过去 24 小时内，NanoBot 项目保持极高的开发活跃度，共处理 18 个 PR 和 4 个 Issue。核心 SDK 的**并发安全 Bug (#4408)** 在报告当天即被社区贡献者定位并提交了多种修复方案（#4425，#4409），体现了高效的响应机制。同时，**性能优化**（Token 缓存）与**渠道扩展**（iMessage）是另外两大热点，多项 CR 进入待合并阶段。项目整体上处于非常健康且高产出的状态。

#### 2. 版本发布
**无**（过去24小时内无新版本发布）

#### 3. 项目进展
昨日项目在稳定性修复与功能落地方面取得了实质性的推进：

- **渠道集成突破**：**[iMessage 渠道](https://github.com/HKUDS/nanobot/pull/4426)**（#4426）已被合并，采用类似 WhatsApp 的 Node.js 侧车模式，无需 Mac 中继即可运行，扩展了 Apple 生态覆盖。
- **核心稳定性修复**：
    - **[MCP 崩溃修复](https://github.com/HKUDS/nanobot/pull/4303)**（#4303）：解决了 `streamableHttp` 会话断开时因异步上下文错位导致的 `RuntimeError` 崩溃问题。
    - **[Dream 光标修复](https://github.com/HKUDS/nanobot/pull/4321)**（#4321）：修复了禁用 Dream 时光标不推进，导致提示词无限制膨胀的 Bug。
- **WebUI 体验优化**：**[iOS 缩放修复](https://github.com/HKUDS/nanobot/pull/4427)**（#4427）已合并，通过设置基础字体大小为 16px 解决了 Safari 输入框自动缩放问题。

此外，**并发安全修复**（#4425，#4409）与**性能优化**（#4421，#4428）的 PR 正在积极评审中，有望在下一个版本中落地。

#### 4. 社区热点
昨日社区讨论的技术深度与协作效率非常高，主要聚集在以下三个焦点：

1.  **🔥 SDK 并发安全设计**（[Issue #4408](https://github.com/HKUDS/nanobot/issues/4408)，[PR #4425](https://github.com/HKUDS/nanobot/pull/4425)，[PR #4409](https://github.com/HKUDS/nanobot/pull/4409)）
    - **诉求**：`Nanobot.run()` 中通过直接修改 `self._loop._extra_hooks` 实现的钩子机制在多会话并发下会被覆盖，导致行为不可控。
    - **分析**：社区贡献者进行了深入的技术探讨。`michaelxer` 提交的 #4425 采用 `contextvars` 方案以最小化 API 破坏，而 `waelantar` 的 #4409 则倾向于修改 `process_direct` 方法签名。这展示了项目在解决核心架构问题时对兼容性与正确性的严谨考量。

2.  **🔥 Token 估算性能瓶颈**（[Issue #4420](https://github.com/HKUDS/nanobot/issues/4420)，[PR #4421](https://github.com/HKUDS/nanobot/pull/4421)，[PR #4428](https://github.com/HKUDS/nanobot/pull/4428)）
    - **诉求**：`estimate_prompt_tokens` 对不变的工具定义反复做 `json.dumps` 和 `tiktoken.encode`，成为高频调用场景下的性能瓶颈。
    - **分析**：这是典型的“社区共识型”问题。用户 `codeLong1024` 提出后，`michaelxer`（#4421）和 `yu-xin-c`（#4428）几乎同时提交了不同实现细节的优化方案，均采用缓存机制。这反映了社区在解决性能优化上的高热情与协同。

3.  **☁️ 异构 Provider 支持**（[Issue #4429](https://github.com/HKUDS/nanobot/issues/4429)）
    - **诉求**：允许 `custom` provider 配置非标准的推理参数，例如火山引擎（豆包）的 `{"thinking": {"type": "enabled"}}`，而非仅支持 OpenAI 的 `reasoning_effort`。
    - **分析**：这表明用户群体已不再局限于单一的 OpenAI 生态，对国内大模型和特色 API 的接入诉求日益增长，是项目平台化的重要信号。

#### 5. Bug 与稳定性
按严重程度排列：

- **[Critical] SDK 并发数据竞争**（[Issue #4408](https://github.com/HKUDS/nanobot/issues/4408)）：多会话 hook 列表覆盖。**已有修复 PR** (##4425, #4409)。
- **[Critical] MCP 连接崩溃**（[PR #4303](https://github.com/HKUDS/nanobot/pull/4303)，已合并）：流式 HTTP 会话断开导致 crash。
- **[High] 提示词膨胀**（[PR #4321](https://github.com/HKUDS/nanobot/pull/4321)，已合并）：Dream 禁用时光标不更新导致上下文无限增长。
- **[Medium] Token 计算性能**（[Issue #4420](https://github.com/HKUDS/nanobot/issues/4420)）：工具定义冗余编码。**已有修复 PR** (#4421，#4428）。
- **[Low] iOS Safari 自动缩放**（[PR #4427](https://github.com/HKUDS/nanobot/pull/4427)，已合并）：WebUI textarea 输入触发页面缩放。

#### 6. 功能请求与路线图信号
从昨日更新的 Issue 和 PR 来看，项目路线图信号明确，重点围绕以下方向：

- **渠道生态全平台化**：iMessage 渠道已落地，Telegram 的富文本消息支持（[Issue #4422](https://github.com/HKUDS/nanobot/issues/4422)，[PR #4423](https://github.com/HKUDS/nanobot/pull/4423)）以及 WhatsApp 的 LID 映射预加载（[PR #4407](https://github.com/HKUDS/nanobot/pull/4407)）表明目标是覆盖主流通讯软件。
- **多 Agent 协同与精细控制**：子任务聚合模式（[PR #4414](https://github.com/HKUDS/nanobot/pull/4414)）和 Cron 任务模型预设（[PR #4416](https://github.com/HKUDS/nanobot/pull/4416)）正在丰富 Agent 的编排与执行能力。
- **开发者体验与二次开发**：Python SDK 扩展（[PR #4296](https://github.com/HKUDS/nanobot/pull/4296)）和内联 TUI（[PR #4329](https://github.com/HKUDS/nanobot/pull/4329)）正在并行推进，预计将在未来版本中显著降低开发门槛。

#### 7. 用户反馈摘要
- **性能敏感**：用户 `codeLong1024` 在 [#4420](https://github.com/HKUDS/nanobot/issues/4420) 中详细描述了 Token 编码在其数字员工项目中的性能瓶颈，凸显了 Agent 高频交互场景下的痛点。
- **生产环境部署需求**：用户对并发安全（#4408）和渠道映射（#4407）的关注，说明社区正越来越多地将 NanoBot 部署到多用户、高并发的真实生产环境中，而不是简单的 Demo 场景。
- **灵活性焦虑**：对 Custom Provider 定制化的强烈需求（#4429）反映了社区不希望被绑定在任一特定 AI 厂商的共识，平台的中立性与灵活性是用户选择 NanoBot 的关键考量。

#### 8. 待处理积压
当前项目积压情况良好，维护者响应迅速。以下是需要关注提醒的、已悬停较久或涉及重大改动的 PR：

- **PR #4256** [fix(memory)](https://github.com/HKUDS/nanobot/pull/4256) (内存游标单调性，6月8日起)：内存模块核心稳定性修复，已提出2周，建议尽快安排评审。
- **PR #4296** [feat(sdk)](https://github.com/HKUDS/nanobot/pull/4296) (Python SDK 扩展，6月11日起)：涉及对外公共 API 的重大变更，需谨慎回归测试，避免影响下游用户。
- **PR #4329** [feat(cli)](https://github.com/HKUDS/nanobot/pull/4329) (内联 TUI，6月13日起)：全新的交互体验，依赖复杂，评审周期较长属正常现象，建议持续关注。
- **PR #4373** [fix(memory)](https://github.com/HKUDS/nanobot/pull/4373) (推送上下文保留，6月16日起)：确保归档时不会丢失投递上下文，防止消息错乱，对体验影响较大。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 (2026-06-21)

---

## 1. 今日速览

过去 24 小时项目保持**极高活跃度**，共涉及 50 条 Issues 与 50 个 PR 更新。开发团队集中攻坚 v0.17.0 升级引发的 Gateway P1 崩溃故障，已通过多个 PR 合并完成修复，核心稳定性回稳。社区侧关于 Token 消耗过大的讨论达到新高峰，`#6839` 延迟工具加载方案获 13 个 👍 成为当日最热议题，用户对成本效益的诉求已从 Feature 请求升级为路线级信号。Desktop 端升级后出现多项回归性 Bug（Composer 不可用、连接卡死），稳定性仍有待加固。

---

## 2. 版本发布

无。

---

## 3. 项目进展

**关键稳定修复合并，Gateway 崩溃问题终结：**
- **【P1 关键修复】`cron.scheduler_provider` 模块冲突**：v0.17.0 中，多个平台适配器（Discord、Slack、Raft 等）在 `sys.path` 中错误插入路径，导致 Python 导入 `plugins/cron/` 而非顶层 `cron/` 包，引发 Gateway 启动崩溃（`ModuleNotFoundError`）。该问题今日由 **teknium1** (#49913)、**kyssta-exe** (#49431)、**ochsec** (#49414) 三人各自提交 PR 并从不同角度修复（统一改为插入项目根路径），**均已合并**。至此，v0.17.0 最严重的阻塞性 Bug 已清除。
- **【Telegram 稳定性】**：PR #49930 为 `TelegramFallbackTransport` 补齐了 `keepalive` 限制与 TCP 保活机制，防止 `CLOSE_WAIT` 状态文件描述符泄漏，该问题此前已影响其他所有长连接适配器。
- **【CI 流水线】**：PR #49936 修复了 CI 中因 Artifact 文件重名导致的 `save-durations` 阶段 `JSONDecodeError`。
- **【社区文档清理】**：PR #49483、#49444、#49177 等多项文档 PR 合并，更新了过时链接、补充了 `context_length` 自动检测的解析链说明。

---

## 4. 社区热点

| 议题 | 热度指标 | 核心诉求 |
|---|---|---|
| **#6839 Lazy Tool Schema Loading** | 26 条评论 / 13 👍 | 两阶段工具注入，将每次调用固定 3.5K-5K Token 开销降至仅注入所需工具。社区呼声最高的单一 Feature。 |
| **#4379 Token Overhead Analysis** | 15 条评论 | 用户 Bichev 搭建 Dashboard 实测发现 73% 的 API 调用由固定开销构成（约 13.9K Tokens），要求系统性优化。 |
| **#13983 16K Tokens by default** | 5 条评论 / 1 👍 | 默认安装下简单 "who u?" 提问即消耗 16K+ Tokens，新用户表示 "难以置信"。 |
| **#41190 Unified Plugin Route** | 5 条评论 / 1 👍 | 要求提供一个统一的、插件可访问的 Hook 来覆盖所有 LLM 调用站点的 provider/model 路由。 |

**分析**：社区情绪正从 "抱怨 Token 贵" 转向 "主动提交量化分析和架构提案"。`#6839` 提出的 "两阶段注入" 架构如果落地，将从根本上改变 Hermes 的 Token 消耗模型。建议项目方在下一次 Roadmap 更新中正式回应该议题。

---

## 5. Bug 与稳定性

### P1 严重
| Issue | 状态 | 描述 |
|---|---|---|
| `#49824` / `#49768` / `#43066` | **已关闭/已修复** | Gateway 崩溃、Dashboard 100% 挂死、Context 压缩丢失消息均为 v0.17.0 回归问题，已通过合并修复 PR 或标记重复关闭。 |
| **`#49903` Composer is not available** | **待解决** | Desktop v0.17.0 升级后输入框报错不可用，影响桌面端用户日常使用。 |
| **`#49920` Desktop CONNECTING 卡死** | **待解决** | 更新后无法连接 Dashboard，根因是 Hermes 注入 `NODE_ENV=production` 导致 `npm install` 跳过 `devDependencies`。 |
| **`#48300` Feishu 飞书死锁** | **待解决** | `_session_task_is_stale` 检测逻辑在 Task 清理后未能释放锁，导致消息永久阻塞。 |

### P2 中等
| Issue | 描述 |
|---|---|
| `#13983` | 默认 Token 消耗过高 (16K+)，影响本地模型部署用户 |
| `#47867` | MCP 工具 `isError` 返回的 JSON 被双重编码，模型无法理解错误信息 |
| `#49747` | Docker 容器中 TTS Edge 懒加载因环境变量 `HERMES_DISABLE_LAZY_INSTALLS=1` 被强制关闭，v2026.6.5+ 镜像启动耗时长达 20 分钟 |
| `#49911` | NVIDIA NIM Provider 模型列表被 `max_models=50` 截断，隐藏了 GLM-5.1 和 Nemotron 等模型 |

### P3 低优
| Issue | 描述 |
|---|---|
| `#49936` | CI 中 Artifact 名称冲突导致 `JSONDecodeError`（PR 已提交） |
| `#37543` | 缺少 i18n 支持，所有 UI 字符串硬编码为英文 |

---

## 6. 功能请求与路线图信号

- **【强路线图信号】Token 体系架构重构**：`#6839`（延迟加载）+ `#4379`（量化分析）构成完整的优化证据链，已远超普通 Feature Request 范畴。建议 v0.18.0 将 "Lazy Tool Schema Loading" 列为核心目标。
- **【已提交 PR 的新功能】**
  - **Codex 联网搜索** (PR #49935)：新增基于 ChatGPT Pro OAuth 的 `openai-codex` Web Search Provider，面向 Pro/Plus 订阅用户。
  - **Venice 模型计费** (PR #49932)：将 Venice API 接入 models.dev 计价链路并支持 Langfuse 成本追踪。
- **【需求池信号】**
  - **国际化 (i18n) `#37543`**：中文社区用户提交，反映非英语用户的真实痛点。
  - **Python 3.14 兼容 `#48723`**：`<3.14` 的版本限制已影响 Homebrew 用户。
  - **自定义 Provider 辅助任务 `#37261`**：`custom:name` 解析问题若修复，将提升多 Provider 场景的可靠性。

---

## 7. 用户反馈摘要

**核心痛点——Token 焦虑**：
“默认安装下，我的 Agent 每次回复固定吃掉 16K+ Tokens，做简单问答的成本太高了。” —— `mikelemo` (#13983)
“73% 的开销是固定的，这对于运行本地模型来说几乎是不可接受的浪费。” —— `Bichev` (#4379)
“如果能在第一轮只塞入 Tool 名称，等模型决定调用时再加载完整 Schema，这将节省 70% 的 Token。” —— `jarviszomine` (#6839)

**升级体验阵痛**：
“升级到 v0.17.0 后，Gateway 直接崩溃了，系统日志显示模块找不到。我的 Telegram 机器人在 24 小时内反复崩溃重启 79 次。” —— 多位用户在 `#49824` 中反馈。
“Desktop 更新后按钮全不能用，我不得不回退到 v0.16.0。” —— `KratosLee-6` (#49903)

**积极肯定**：
“昨晚提交的 Gateway 崩溃报告，今天一早看到三个 PR 被合并了！团队反应太快了。” —— `crose0122` (#49824)
“虽然 Token 问题是老大难，但看到社区有人拿出量化 Dashboard 确实让人振奋，期待项目组的方案。” —— 社区评论反馈

**使用场景亮点**：
多位用户提及在跨平台（Telegram + CLI）长期运行 `/goal` 任务时遇到 Session 压缩导致的状态丢失，反映了高频/长周期 Agent 场景对 Context 管理的高要求。

---

## 8. 待处理积压

**高优积压——关注核心维护者资源分配**：

- **【架构级】Lazy Tool Schema Loading (`#6839`)**：自 2026-04-09 开放，已积压 **73 天**，13 👍 26 评论。该 Fabric 级别的改动需要 core team 深度参与，建议列为 v0.18.0 里程碑目标。
- **【安全】依赖版本升级 (PR #42334)**：`aiohttp` 3.14.0 + `anthropic` 0.87.0 + `cryptography` 安全版本锁定。自 2026-06-08 提交，已等待 13 天未合并。若无特殊阻塞原因，建议优先处理以防 CVE 风险。
- **【平台适配】企业 IM 平台 PR 积压**：
  - PR #39510（钉钉 Markdown 独立发送 + 飞书表格渲染修复）—— 技术确认后未合并。
  - PR #39586（Cron 投递 `wechat` 别名解析到 `weixin`）—— 等待合并。
  - 以上两 PR 均由 **WenhuaXia** 提交，自 6 月 5 日起搁置，影响企业微信/钉钉用户的完整体验。
- **【长期需求】跨平台会话上下文共享 (`#4335`)**：自 2026-03-31 开放，是 Power User 长期诉求，需架构层面介入但一直未进入开发队列。

---

*数据来源：NousResearch/hermes-agent Issues/PRs 公开数据，统计截止 2026-06-21。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClab 项目日报 | 2026-06-21

> 分析师寄语：项目进入典型的“功能累积等待决策”期，大量高质量社区贡献与严重 Bug 报告均处于 `stale` 状态，建议提高响应优先级。

---

### 1. 今日速览

PicoClaw 项目今日活跃度中等，但**核心进展趋缓**。过去 24 小时无新 Issue/PR 提出，已有的 2 个 Issue 与 1 个 PR 因长期未获响应被自动标记或最后更新提醒。新版 Nightly 构建按计划发布（`v0.3.0-nightly.20260621`），但缺乏实质性代码合并。社区关注点高度集中：**2个讨论热度最高的议题分别直指协议完备性与严重财务损失风险**。项目整体需要维护者介入打破停滞节奏。

---

### 2. 版本发布

- **版本**: `nightly` / `v0.3.0-nightly.20260621.287853ab`
- **类型**: 自动发布、可能不稳定
- **说明**: 基于 `main` 分支 at `287853ab` 的自动化构建，适合尝鲜用户验证近期改动，但不建议生产环境部署。
- **变更加载**: 可通过 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.3.0...main) 查看完整对比，本次发布未附带明确的破坏性变更说明。

---

### 3. 项目进展

- **今日合并/关闭的 PR**：**无**。过去 24 小时没有任何 PR 被合并或关闭。
- **关键待合并 PR**：
  - **#2964 — Feat/image input compression** 👈 **亟需 Code Review**
    - 作者：`afjcjsbx` | 提交于 2026-05-28 | 状态：**Open / Stale**
    - 改动：为视觉管道引入可配置的多级图像压缩策略，此前仅靠 `max_media_size` 硬限制，易导致 Token 浪费与模型 Payload 过大。
    - **进展判断**：若合并，将显著降低视觉 Agent 的 API 成本与延迟，契合当前降本增效趋势。PR 已停滞超过 3 周，是项目目前最接近入库的有价值贡献。
    - 链接：[PR #2964](https://github.com/sipeed/picoclaw/pull/2964)

---

### 4. 社区热点

| 标题 | 类型 | 热度指标 | 链接 |
|---|---|---|---|
| **Add explicit turn completion signal** | Feature Request | 👍 **2**（当日最高赞） | [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984) |
| **Continuous consumption of tokens** | Bug Report | 💬 **4** 条评论（当日最多） | [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012) |

- **#2984 — 协议完善诉求**：外部 WebSocket 客户端需要一个明确的 `turn.end` 信号，而非从 `typing.stop` 间接推断。社区对此高度认可（2 👍），反映用户正在将 PicoClaw 用于**生产级多轮对话系统**，对协议确定性有强需求。
- **#3012 — 成本流失恐慌**：用户 `xpader` 详细复现了启用 Evolution（Draft 模式）后，Token 每分钟持续消耗的 Bug。评论区共 4 条讨论，集中在复现条件与影响范围上。

---

### 5. Bug 与稳定性

> **唯一确认的 Bug 影响严重，直接涉及资金流失，应列为 P0 优先级。**

- **[P0] Issue #3012 — Token 持续消耗** 🚨
  - **版本**：v0.2.9 | **环境**：FreeBSD 15.0, MiniMax 模型
  - **现象**：开启 Evolution 功能（Evolution Mode = Draft, Code Path 触发）后，即使没有用户输入，Token 也按分钟持续被消耗。
  - **影响**：直接造成用户 API 账户资金流失，并产生无效的后台负载。
  - **当前状态**：提交于 2026-06-05，至今无维护者回复，已进入 `stale` 待关闭队列。
  - **链接**：[Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

- **稳定性检测**：无新崩溃报告或回归通报。项目整体稳定，但该 Bug 对用户信任度形成了明显冲击。

---

### 6. 功能请求与路线图信号

- **短期可落地（已有代码贡献）**：
  - **PR #2964 — 图像压缩**（见第 3 节）。如果项目组能在本周完成 Review，极大概率纳入下一版本。
- **中期基础设施（协议层）**：
  - **Issue #2984 — 显式轮次结束信号**。这是走向标准 Bot 协议（类似 Discord/Guilded 的交互模型）的关键缺失。建议打上 `design` / `protocol` 标签开启 RFC，预期纳入 v0.4.0 路线图讨论。
  - **数据提示**：⭐ 2 个赞在今日是最高的，说明该需求在社区有广泛共识。

---

### 7. 用户反馈摘要

- **成本问题是第一痛点**：用户 `xpader` 的复现步骤清晰专业，揭示了 Evolution 在特定配置下可能陷入**空转循环**。这类 Bug 会导致小微开发者直接流失，是信任危机。
- **生态集成需求旺盛**：用户 `Brook-sys` 提出协议补完需求表明，PicoClaw 正在从简单对话走向**结构化 Agent 交互**。客户端的确定性判断是落地的前提。
- **社区自我造血能力强**：用户 `afjcjsbx` 直接贡献了图像压缩的 PR 代码。说明社区开发者愿意投入时间解决实际问题，**但前提是维护者的及时认可**——该 PR 已 Stale 三周，需要响应的不仅是“合并与否”，更是对贡献者的尊重。

---

### 8. 待处理积压

以下三项若久拖不决，将对项目社区健康与用户留存构成实质威胁：

| ID | 类型 | 标题 | 已停滞 | 建议行动 |
|---|---|---|---|---|
| **#2964** | PR | Feat/image input compression | **24 天** | 本周内安排至少一位维护者 Code Review，明确合并方向或修改要求。 |
| **#3012** | Issue | [BUG] Continuous token consumption | **16 天** | **立即标记为 P0**，发布临时规避方案（如关闭 Evolution 的建议），并给出修复时间窗口。 |
| **#2984** | Issue | Explicit turn completion signal | **19 天** | 给予标签 `help-wanted` / `design`，并回复用户该功能的规划版本或在 Roadmap 中的位置。 |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，遵照您的要求。基于 `nanocoai/nanoclaw` 在 2026-06-20 的 GitHub 数据，以下是为 2026-06-21 生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-21

## 1. 今日速览

过去 24 小时内，NanoClaw 项目没有合并任何 PR 或发布新版本，整体进入 **“稳定积累与安全加固”周期**。社区活跃度保持健康，共有 **6 个开放 PR** 和 **1 个活跃 Issue** 等待维护者处理。值得注意的是，当前社区贡献的焦点高度集中：一方面在紧急修复一个已公开的 **CVE 安全漏洞（CVE-2026-29611）**，另一方面在进行大范围的技术债务清理（移除过时的全局内存机制与死代码挂载）。这标志着项目正在从快速迭代期向 **“架构收敛与安全基线提升”** 阶段过渡。

## 2. 版本发布

*   过去 24 小时内无新版本发布。

## 3. 项目进展

虽然今日没有 PR 被合并，但这并不意味着项目停滞。相反，**维护者手中积攒了一批高价值的贡献**，预计将在未来几天集中处理：

*   **安全加固（待合并）**：
    *   `sturdy4days` 提交了 **CVE-2026-29611** 的修复方案 (#2799)，对 `send_file` 函数增加了 `/workspace` 的目录限制，防止被注入的 Agent 读取容器内任意敏感文件（如凭据、外部挂载数据）。
*   **核心架构清理（待合并）**：
    *   `CutSnake01` 一口气提交了 3 个 PR，旨在彻底摘掉项目的历史包袱。包括从 Seed Prompt 中移除过时的“全局内存”指令 (#2824)，删除主机启动时自动失效的 `CLAUDE.md` 文件 (#2823)，以及丢弃无用的 `/workspace/global` 死挂载 (#2822)。这将显著减少 Agent 上下文污染并简化容器配置。
*   **技术鲁棒性（待合并）**：
    *   `sturdy4days` 修复了数据解析层的一个边缘 Bug (#2801)，防止 `JSON.parse` 对原始值（如 `"5"`、`"true"`）解析成功后导致下游调用 `undefined` 的问题。
*   **文档完善（待合并）**：
    *   `chandrameenamohan` 补充了关于 `assistant-name` 环境变量的文档 (#2821)。

## 4. 社区热点

1.  **[CVE-2026-29611] 安全漏洞修复（#2799）**：
    该 Issue/PR 是本周期社区关注度最高的话题。它触及了 Agent 安全的底线——沙箱隔离。用户 `sturdy4days` 的强烈诉求是：**绝不能让被污染的 Agent 成为任意文件读取的跳板**。
    *   链接: [PR #2799](https://github.com/nanocoai/nanoclaw/pull/2799)

2.  **Claude 提示缓存请求（#2768）**：
    用户 `galmorduku` 提出，当前 Anthropic Provider 调用时关闭了 Prompt Caching，导致每次对话都要重新发送系统提示，对于长提示或复杂 Agent 是严重的性能浪费。这是一个**呼声极高的优化需求**，改动量极小（配置默认值），但收益巨大。
    *   链接: [Issue #2768](https://github.com/nanocoai/nanoclaw/issues/2768)

3.  **清理遗留全局状态（#2822, #2823, #2824）**：
    `CutSnake01` 的系列 PR 引发了社区对 **“全局内存（Global Memory）”** 机制过于复杂且容易产生混乱的讨论。用户希望简化配置，减少认知负荷。
    *   链接: [PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824), [PR #2823](https://github.com/nanocoai/nanoclaw/pull/2823), [PR #2822](https://github.com/nanocoai/nanoclaw/pull/2822)

## 5. Bug 与稳定性

*   **严重 - 安全漏洞**：
    *   `send_file` 路径穿越 (CVE-2026-29611, #2799)。**已有修复 PR**。
*   **高 - 逻辑错误 / 可用性问题**：
    *   `safeParseContent` 解析原始值导致的 `undefined` 错误 (#2801)。**已有修复 PR**。
    *   系统提示缓存默认关闭，导致性能低下与 Token 浪费 (#2768)。**暂无修复 PR，急需维护者响应**。
*   **中 - 技术债务 / 状态异常**：
    *   种子提示中包含过时指令 (#2824)。
    *   主机启动时自动删除全局 CLAUDE.md 文件 (#2823)。
    *   容器挂载了无用的死目录 (#2822)。

## 6. 功能请求与路线图信号

*   **短期路线图信号**：
    1.  **安全优先**：CVE (#2799) 的修复预示着下一个小版本极大概率会是一个包含安全补丁的维护版。
    2.  **彻底剔除“全局内存”**：CutSnake01 的清理 PR 暗示社区希望彻底摘掉这个历史包袱，简化整体 Agent 运行时模型。
    3.  **默认开启 Prompt Caching**：Issue #2768 是一个改动极少但效用巨大的功能请求，很可能会在近期被接受。
*   **长期信号**：
    *   目前没有激进的新功能请求，社区正在 **“稳固基座”**，重点在于安全性、稳定性和清除技术债务。这对于项目的长期健康是极好的信号。

## 7. 用户反馈摘要

*   **痛点**：
    *   **安全担忧**：用户 `sturdy4days` 指出当前的安全模型存在明显的路径遍历缺陷。
    *   **效率不满**：用户 `galmorduku` 抱怨未开启缓存导致 Agent 推理效率低，成本高。
    *   **配置混乱**：用户 `CutSnake01` 认为项目中残留的大量过时配置和新手提示，对新用户极不友好。
*   **满意/贡献热情**：
    *   虽然 PR 的评论互动为 0，但连续新增 6 个高质量 PR 的行为本身说明了 **“沉默的贡献者”正在用代码投票**，项目的技术社区参与度很高。
*   **反馈真空期**：
    *   部分 PR（如 #2799， #2801）虽然已更新，但**缺乏维护者的评论**。用户可能担心反馈周期过长。

## 8. 待处理积压

目前所有 PR 均为本周提交，年龄不长，但数量较多（**6 个待审核**）。维护者需尽快安排 Code Review，确保贡献者的热情不被消耗。

*   **紧急待办（影响安全）**：
    *   [PR #2799](https://github.com/nanocoai/nanoclaw/pull/2799): CVE-2026-29611 安全修复。（等待 Review/合并）
*   **核心待办（影响体验）**：
    *   [Issue #2768](https://github.com/nanocoai/nanoclaw/issues/2768): 默认开启提示缓存。（等待维护者确认或认领）
*   **常规待办（高质量清理）**：
    *   [PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824), [PR #2823](https://github.com/nanocoai/nanoclaw/pull/2823), [PR #2822](https://github.com/nanocoai/nanoclaw/pull/2822): 全局内存清理。（等待 Review）
    *   [PR #2801](https://github.com/nanocoai/nanoclaw/pull/2801): 数据解析鲁棒性修复。（等待 Review）
    *   [PR #2821](https://github.com/nanocoai/nanoclaw/pull/2821): 环境变量文档。（等待 Review）

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

### NullClaw 项目动态日报 — 2026‑06‑21

**1. 今日速览**  
过去 24 小时内，NullClaw 仓库仅收到 1 个新 Issue（[#967](https://github.com/nullclaw/nullclaw/issues/967)），无 Pull Request 更新，无版本发布。该 Issue 报告了一个出现频率超过 50% 的 `NoResponseContent` 错误，影响核心对话功能。代码库自 v2026.5.29 以来未见新提交，项目处于低活跃间歇期，社区反馈以稳定性问题为主。

**2. 版本发布**  
（无）

**3. 项目进展**  
今日无 Pull Request 被创建、合并或关闭，未检测到任何代码提交或分支操作。项目功能与代码状态与上一版本保持一致，无明显推进。

**4. 社区热点**  
目前唯一活跃的社区讨论集中在 **[#967 [bug] error: NoResponseContent](https://github.com/nullclaw/nullclaw/issues/967)**。用户 `svier0` 提供了详细的复现环境（Win11、NullClaw v2026.5.29、Agnes‑2.0‑Flash 模型）及概率数据（21 次对话出现 12 次）。虽然尚未产生评论，但该 Bug 直指响应处理稳定性，潜在影响范围广，诉求核心是修复高频空响应问题。

**5. Bug 与稳定性**  
- **[#967](https://github.com/nullclaw/nullclaw/issues/967)**（严重程度：高）  
  用户报告 `NoResponseContent` 错误，特定模型下载体下对话失败率 > 50%，严重妨碍正常使用。当前无关联修复 PR，未分配、未标记。建议维护者优先复现定位，可能涉及 HTTP 响应解析或模型适配层缺陷。

**6. 功能请求与路线图信号**  
今日未收集到明确的新功能请求。用户反馈集中在底层稳定性不足，预期下一版本路线图应将错误处理与健壮性提升纳入优先级，尤其是对大模型返回空响应的场景进行容错优化。

**7. 用户反馈摘要**  
通过 Issue #967，用户表达出对 NullClaw 客户端可靠性的明显不满：“同样的模型同样的一个 apikey，我在 picocla...” 表明其他客户端能正常工作，而 NullClaw 却高频失败。用户提供了精确的发布 zip 包来源，体现出积极的协作态度，同时也暗示问题可能来自 NullClaw 独有的请求‑响应处理逻辑，而非后端 API 或模型本身。

**8. 待处理积压**  
- **[#967](https://github.com/nullclaw/nullclaw/issues/967)**：新提交的关键 Bug，尚未获得维护者回应或标签分配。建议尽快确认复现性并启动修复讨论，避免问题长期滞留。仓库中当前无其他长时间未响应的重要 Issue 或 PR。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 (2026-06-21)

## 1. 今日速览
今日项目活跃度极高，24小时内产生了 **21 条 Pull Request**，其中 **12 条开放待审**，**9 条已完成合并/关闭**。核心贡献者 serrrfirat 主导了 Reborn 架构下的渠道接入整合（Manifest-driven channels）、CI 现代化及多项 Bug 修复。项目功能迭代迅猛，Google OAuth 刷新、Slack 重连等用户痛点已被及时修复，但 **Nightly E2E 测试已持续失败 25 天（#4108）且无人响应**，是当前项目健康度的最大隐患。

---

## 2. 版本发布
无

---

## 3. 项目进展
今日合并/关闭了 9 个重要 PR，标志着项目在多条关键战线上取得突破：

- **渠道接入框架统一化**：serrrfirat 合并了 #5103、#5104、#5105、#5106、#5102 等系列 PR，将 Slack、Telegram 等渠道的入站鉴权、传输、凭证管理全部抽象为 Manifest 声明式配置，大幅减少了 Rust 侧的样板代码和配置矩阵。新的整合性 PR [#5107](https://github.com/nearai/ironclaw/pull/5107) 已提出，拟将前序零散修改合并为一个自包含的变更集。

- **工作区实体功能正式落地**：经过近两个月的开发和数据库迁移，PR [#2548](https://github.com/nearai/ironclaw/pull/2548)（作者 standardtoaster）完成合并。该 PR 引入了 DB 支持的工作区、成员管理和跨工作区共享，为多租户和企业级部署铺平了道路。

- **CI 基础设施强化**：
  - [#4829](https://github.com/nearai/ironclaw/pull/4829) 合并，正式将 Reborn 测试套件纳入 Nightly Deep CI，并移除已废弃的 `reborn-integration` 工作流。
  - [#5086](https://github.com/nearai/ironclaw/pull/5086) 合并，实验性地引入了 nextest 归档、mold、sccache 等构建/测试优化工具，为未来在全量门禁上运行测试进行性能摸底。

- **用户体验 Bug 修复**：
  - [#4777](https://github.com/nearai/ironclaw/pull/4777) 修复了 Slack 在 WebUI 中的断线重连循环问题。
  - [#5087](https://github.com/nearai/ironclaw/pull/5087) 修复了 Google OAuth 令牌过期需手动重连的问题，实现了条件性刷新。

---

## 4. 社区热点
虽然本次快照中互动评论数据暂未完整记录，但从 PR 的标签、规模和影响力来看，**Reborn 生态系统的全方位重构**是今日的绝对主线：

- **核心参与者**：serrrfirat 贡献了今日大部分重量级 PR（渠道、CI、测试修复、学习系统），是当前迭代的主要推手。henrypark133 则在 Reborn 运行时并发（[#5085](https://github.com/nearai/ironclaw/pull/5085)）和触发器进阶功能（[#5065](https://github.com/nearai/ironclaw/pull/5065)）上稳步推进。

- **高期待特性**：
  - [#4937](https://github.com/nearai/ironclaw/pull/4937)（Reborn 学习系统）—— WS-1 阶段记忆文档与信心评分机制，标志着 Agent 智能化能力提升的重要一步。
  - [#5085](https://github.com/nearai/ironclaw/pull/5085)（并发 Runs 执行）—— 解决 Reborn 运行时串行化瓶颈，直接关系到高并发推理场景的用户体验。

---

## 5. Bug 与稳定性

### 严重
- **[#4108](https://github.com/nearai/ironclaw/issues/4108) Nightly E2E 测试持续失败**：自 2026-05-27 起已存在 25 天，当前 0 条评论，无明确解决计划。CI 核心门禁路径处于断裂状态，严重削弱回归信心。

### 已修复
- **[#5087](https://github.com/nearai/ironclaw/pull/5087) Google OAuth 令牌条件刷新**：防止令牌过期导致 Gmail/Drive 等集成服务中断。
- **[#5108](https://github.com/nearai/ironclaw/pull/5108) 修复 Reborn 依赖闭包尾部失败**：Agent-自动修复了 GitHub 工具权限过度暴露等问题。
- **[#5105](https://github.com/nearai/ironclaw/pull/5105) 修复三个过时安全守卫测试**：因代码重构而失效的安全测试已恢复，保证 OAuth 验证逻辑闭环。
- **[#4777](https://github.com/nearai/ironclaw/pull/4777) 修复 Slack 重连循环**：彻底解决了 WebUI 中 Slack 始终处于“未连接”状态导致的前端无限重试问题。

---

## 6. 功能请求与路线图信号
路线图信号清晰，项目正在向功能完善的 **Reborn 2.0** 架构快速演进：

- **WS-1 学习系统**：[#4937](https://github.com/nearai/ironclaw/pull/4937) 引入带置信度的记忆文档（confidence 1–10）、分类（category）和 A/B 测试门控（gate），旨在实现“从错误中学习”的智能体能力提升，对标 Hermes 等级功能。
- **并发 Turn 执行**：[#5085](https://github.com/nearai/ironclaw/pull/5085) 通过 `TurnRunScheduler` 和按用户/类型限流，打破 Reborn 运行时的严格串行执行瓶颈，对 LLM 推理密集型场景带来显著吞吐提升。
- **一次性触发器**：[#5065](https://github.com/nearai/ironclaw/pull/5065) 扩展了 `TriggerSchedule`，支持 `Once { at， timezone }` 变体，丰富了规则引擎的适用场景。
- **托管单租户 Postgres 预览**：[#5081](https://github.com/nearai/ironclaw/pull/5081) 新增 `hosted-single-tenant` 配置文件，在保持本地开发界面的前提下，为 SaaS 托管版本做技术准备。

---

## 7. 用户反馈摘要
直接的用户 Issue 反馈在今日数据中较少，但通过维护者的修复动作可以反推普遍痛点：

- **连接稳定性仍是最大摩擦点**：⚠️ Slack 重连循环（#4777）和 Google OAuth 令牌过期（#5087）的快速修复，直指多模态渠道集成中的高优先级稳定性问题。这些修复应在下一轮发布中显著提升集成体验。
- **测试可观测性有待加强**：Nightly E2E 长期失败（#4108）且无人问津，可能意味着失败详情对终端用户不透明，或用户已对 CI 飘红现象产生麻木。建议增加失败通知的上下文、责任人指派以及 Dashboard 展示。

---

## 8. 待处理积压

- **[#4108](https://github.com/nearai/ironclaw/issues/4108) 【严重】Nightly E2E 失败**：积压超过 3 周，是项目的门禁红线。**亟需核心团队调查并分配资源修复**，否则长期飘红将严重削弱 CI 的信任度，并可能导致更多回归问题遗漏。

- **[#4002](https://github.com/nearai/ironclaw/pull/4002) 【依赖更新】Dependabot 批量升级**：涉及 16 个 Actions 包，包括 `actions/checkout@v4 -> v7` 等跳级升级。变更面广，存在不可预见的 CI 破坏风险，需仔细回归确保兼容性。

- **[#4765](https://github.com/nearai/ironclaw/pull/4765) 【功能修复】Codex 子代理提示预算**：自 6月11日开放，属于 Codex 边界优化，与正在推进的学习系统工作（#4937）具备天然衔接关系，建议及早合并。

- **[#5065](https://github.com/nearai/ironclaw/pull/5065) / [#5085](https://github.com/nearai/ironclaw/pull/5085) 等 XL 级特性 PR**：虽然积极更新，但均为超大级别改动，涉及文档、依赖、核心调度等多领域，建议投入足够人力加速 Code Review，避免阻塞后续工作流。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 2026-06-21

> 数据覆盖过去 24 小时（截至 2026-06-20），情报源自 GitHub 仓库 netease-youdao/LobsterAI。

---

## 1. 今日速览

过去 24 小时内项目无新 Issue、无新 Pull Request、无新版本发布。仓库自动关闭了 5 个标记为 “stale” 的陈旧 Issue（#1468, #1469, #1470, #1495, #1496），这些均为 4 月初由用户提交的 Bug，长期无维护响应后被系统关闭。整体而言，项目当前处于低活跃度维护状态：既无实质代码推进，也未见社区新讨论，仅通过自动清理积压减轻列表负担。核心的健康度信号偏弱，需关注长期未修复 Bug 对用户信心的影响。

---

## 2. 版本发布

<u>无新版本发布</u>（该部分省略）

---

## 3. 项目进展

今日没有任何 Pull Request 被打开、合并或关闭，因此项目在代码层面没有功能推进或 Bug 修复。唯一的变动是 5 个被自动关闭的 Stale Issue，但这属于仓储维护行为，不代表对应问题已解决。项目当前的开发节奏偏慢，长期贡献活跃度有待提升。

---

## 4. 社区热点

今日无新 Issue 或 PR 产生，社区讨论热度较低。但从被关闭的陈旧 Issue 中可观察到用户曾集中关注的几个方向：

- **未保存内容丢失** – #1468、#1469、#1470 均指向不同弹窗（创建 Agent、设置面板、MCP 服务器配置）在用户填写/修改后，通过 X 按钮、Cancel、Escape 或点击遮罩层关闭时，所有已填内容静默丢失。同一作者 @MaoQianTu 连报三个相似问题，反映出该行为对用户造成显著困扰。
- **任务执行异常** – #1496 报告“任务显示完成但是没有返回”，涉及核心流程可靠性。 #1495 报告“无缘无故中断进程”，并获 1 个 👍，说明部分用户同样遇到此类中断问题。

虽然这些 Issue 目前已关闭，但背后的用户诉求（数据保护、流程稳定性）仍是社区关注重点。

- [#1496: 任务显示完成，但是没有返回](https://github.com/netease-youdao/LobsterAI/issues/1496)  
- [#1468: 创建Agent弹窗关闭时无未保存确认](https://github.com/netease-youdao/LobsterAI/issues/1468)  
- [#1469: Agent设置面板关闭时无未保存确认](https://github.com/netease-youdao/LobsterAI/issues/1469)  
- [#1470: MCP服务器配置弹窗关闭或按Escape时无未保存确认](https://github.com/netease-youdao/LobsterAI/issues/1470)  
- [#1495: 无缘无故中断进程](https://github.com/netease-youdao/LobsterAI/issues/1495)

---

## 5. Bug 与稳定性

今日无新 Bug 报告。5 个此前报告的 Bug 被自动关闭，但对它们按严重程度排列如下：

| 严重性 | 编号 | 问题描述 | 影响 |
|--------|------|----------|------|
| 高 | [#1495](https://github.com/netease-youdao/LobsterAI/issues/1495) | 无缘无故中断进程 | 直接打断用户工作流，且难以区分是客户端还是模型问题 |
| 高 | [#1496](https://github.com/netease-youdao/LobsterAI/issues/1496) | 任务显示完成但无返回结果 | 核心功能输出丢失，破坏任务闭环 |
| 中 | [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468) | 创建 Agent 弹窗关闭时未保存确认 | 内容静默丢失，降低对产品的信任感 |
| 中 | [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469) | Agent 设置面板关闭时未保存确认 | 同上，涉及多个交互点位 |
| 中 | [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470) | MCP 服务器配置弹窗关闭时未保存确认 | 同上，甚至影响已配置的环境变量/API Key |

目前 **没有任何 Fix PR 关联到这些 Bug**，且它们均因 Stale 自动关闭，意味着尚未被修复。建议维护者逐一评估是否需要重新打开或标记为已知问题，避免真实用户持续受影响。

---

## 6. 功能请求与路线图信号

今日没有新的功能请求产生。但上述“未保存确认”类 Issue 虽归类为 Bug，实则隐含对交互流程的功能性期待——用户希望表单具备“是否放弃未保存更改”的判断机制。该能力在前端属于常见模式，若在后续版本中实现（例如为 Modal 增加 `useDirty` 状态与关闭拦截），将能一次性覆盖 #1468、#1469、#1470 三者场景。目前尚无 PR 或 Roadmap 文档表明该功能已排期，用户需求处于搁置状态。

---

## 7. 用户反馈摘要

综合各 Issue 内的描述与评论，提炼真实用户痛点如下：

- **数据安全感缺失**（@MaoQianTu）: 在多个关键弹窗中，用户填写大量内容后一旦误操作关闭即全部丢失，且无任何挽回手段。期待类似“有未保存更改，是否放弃？”的确认弹窗。
- **执行反馈模糊**（@xuzhiwu123）：遇到无故中断时，提示不足以定位根因（“这是客户端的问题还是大模型的问题呢？”），希望错误信息更加可解释、可诊断。
- **结果可视性**（@netease-george）: 任务显示完成却不返回结果，让用户无法信任系统反馈，需确保完成状态与输出一致。

这些反馈共同指向 **交互健壮性不足** 与 **系统透明度欠缺**，影响了用户对 Agent 功能的依赖度。

---

## 8. 待处理积压

以下 Issue 在自动关闭前长期未得到响应或修复，但其本质问题对用户影响较大，建议维护团队优先复检：

| 编号 | 标题 | 最后更新时间 | 建议行动 |
|------|------|------------|----------|
| [#1495](https://github.com/netease-youdao/LobsterAI/issues/1495) | 无缘无故中断进程 | 2026-06-20 | 重新打开并添加 “needs-reproduce” / “help-wanted” 标签，收集更多日志 |
| [#1496](https://github.com/netease-youdao/LobsterAI/issues/1496) | 任务显示完成，但是没有返回 | 2026-06-20 | 该缺陷直接关联核心功能，建议优先定位修复 |
| [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468) | 创建Agent弹窗关闭时无未保存确认 | 2026-06-20 | 三个同类 Issue 可统一作为“表单离场保护”需求跟踪，成本低且对 UX 改善明显 |
| [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469) | Agent设置面板关闭时无未保存确认 | 2026-06-20 | 同上 |
| [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470) | MCP服务器配置弹窗关闭或按Escape时无未保存确认 | 2026-06-20 | 同上，另涉及环境变量等重要配置 |

若维护者认为上述问题仍属有效，可考虑取消 stale 标签并重新激活，或将其归档至 Roadmap 的 Known Issues 列表，以免失去跟踪。

---

**日报总结：** 项目今日整体静态，唯一变化是自动清理了 5 个积压 Bug。虽然没有新的贡献流入，但清除尘封 Issue 有利于聚焦真正亟需解决的问题。当前健康度指标偏弱，建议关注搁置的高影响 Bug 并适时重启修复流程。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，以下是为您生成的 Moltis 项目 2026-06-21 动态日报。

---

# Moltis 项目日报 (2026-06-21)

**分析师视角：** 聚焦 AI 智能体与个人 AI 助手领域开源生态
**数据来源：** [Moltis GitHub](https://github.com/moltis-org/moltis)
**报告周期：** 2026-06-20 ~ 2026-06-21

---

### 1. 今日速览

Moltis 项目今日整体状态平稳，社区活跃度较低。过去 24 小时内无用户提交新的 Issue，亦无用户驱动的核心功能 PR。项目的主要动态全部由自动化依赖管理工具（Dependabot）贡献：一个依赖升级 PR (#1133) 已被合并，另一个同类 PR (#1134) 正在等待审核。这暗示项目目前处于稳定的维护周期，得益于自动化的依赖梳理，项目的供应链安全得以保障，但功能推进和社区讨论处于静默期。

### 2. 版本发布

（基于提供的数据，过去 24 小时无新版本发布，本部分省略。）

### 3. 项目进展

今日虽无新功能合入，但在“技术债务清理”与“依赖安全”方面有所推进：

- **文档构建链路升级：** **[PR #1133]** (已合并) 完成了对文档站点 (`/docs`) 核心框架 Astro 的版本升级（6.3.3 -> 6.4.8）。这将间接提升文档构建效率与安全性，降低潜在漏洞风险。
- **基础设施依赖维护：** **[PR #1134]** (待合并) 正在进行 `undici` 库在网站目录下的升级。作为 Node.js 生态中关键的 HTTP/1.1 客户端，其更新对项目可能整合的 HTTP 通信模块（如 AI 模型调用接口层）具有可靠性支撑作用。

> 总结：项目在功能维度上今日无重大进展，但在基础设施的“健康度”与“供应链安全”上完成了必要维护。

### 4. 社区热点

- **状态：** 冷清。
- **分析：** 今日所有更新的 PR 均未产生评论或互动。当前版本未引发社区显著讨论或争议，项目处于低摩擦的稳定期。

> **参与链接：** [PR #1133](https://github.com/moltis-org/moltis/pull/1133) | [PR #1134](https://github.com/moltis-org/moltis/pull/1134)

### 5. Bug 与稳定性

- **新报告 Bug：** 无。
- **崩溃/回归问题：** 未发现。
- **稳定性评估：** 稳定。无新的 Bug 修复 PR 被提出，用户在稳定性方面表现出较高的接受度。

### 6. 功能请求与路线图信号

- **新需求：** 无。
- **路线图信号解读：** 社区反馈通道较为平静，未出现新的定制化诉求。通常这种静默可能预示着项目正处于大型版本发布前的内部开发冲刺期（Feature Freeze），或当前功能已充分满足大部分用户的基本需求。

### 7. 用户反馈摘要

由于今日既无用户新开 Issue 也未在现有 PR 下发表评论，无法提炼具体的用户痛点或使用场景反馈。项目用户群处于典型的“静默使用”状态。

### 8. 待处理积压与行动提醒

- **短期积压：**
  - **[PR #1134]** 为 Dependabot 自动生成的依赖更新，非常规 Bug 或阻塞项。建议维护者尽快审核合并，以保持依赖版本的清洁度，避免后续出现冲突风险。
    > [链接至待处理 PR #1134](https://github.com/moltis-org/moltis/pull/1134)
- **长期积压：** 当前数据无显示长期未响应的关键 Issue 或 PR。项目积压情况健康。

---
**项目健康度摘要：** 绿（稳定维护期）。依赖自动更新流畅，社区无噪音，项目基础扎实。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，以下是根据您提供的 CoPaw (QwenPaw) GitHub 项目数据生成的 2026-06-21 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-06-21

## 1. 今日速览

过去 24 小时内，CoPaw 项目保持中等偏上的开发活跃度。社区层面共计产生 10 条 Issue 更新与 9 条 PR 更新，暂未有新版本发布。值得关注的是，新人贡献势头强劲，共有 4 位首次贡献者提交了涵盖 Docker 工具隔离、文件沙箱加固、KV-Cache 性能优化等核心模块的 Pull Request，表明项目生态吸引力和开发者体验良好。然而，用户的高强度使用反馈也暴露出若干稳定性隐患：Deepseek 模型思考卡死以及 API 静默丢包问题成为当前最大的信任危机，需要维护者优先响应。

## 2. 版本发布

无

## 3. 项目进展

项目在本日进展集中在“基础设施升级”与“深度防御加固”两方面。虽然合并数量不多，但待合并 PR 质量较高，展现了向企业级 Agent 平台迈进的决心。

- **可观测性优化（已合并）：** [#5128](https://github.com/agentscope-ai/QwenPaw/pull/5128) 将 Langfuse 的 Trace 粒度从单次 LLM 调用聚合为单次 Agent ReAct 循环，极大提升了对 Agent 行为的调试与监控体验。
- **内存运行时迁移（WIP）：** [#5349](https://github.com/agentscope-ai/QwenPaw/pull/5349) 将内存后端迁移至 ReMe4，在保持旧版 API 兼容的前提下，为长时记忆和大规模会话管理打下架构基础。
- **上下文管理革新（Review 中）：** [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321) 提出了基于检索的持久化上下文策略（Scroll），替代传统的压缩策略，有望在复杂任务中大幅提升 Agent 的上下文利用效率。
- **安全沙箱构建：** [#5341](https://github.com/agentscope-ai/QwenPaw/pull/5341) 限制文件工具仅能操作 Agent 工作区内文件；[#5346](https://github.com/agentscope-ai/QwenPaw/pull/5346) 则将工具执行环境置于 Docker 内，全面加固系统安全边界。
- **稳定性修复与性能优化：** [#5347](https://github.com/agentscope-ai/QwenPaw/pull/5347) 修复了因无效 Cron 任务导致启动崩溃的根因；[#5348](https://github.com/agentscope-ai/QwenPaw/pull/5348) 通过冻结 Session 内日期戳来防止跨天导致的 KV-Cache 完全失效，显著优化长会话推理性能。

## 4. 社区热点

本日社区讨论热度集中于 **“移动端可用性”**与**“模型生态兼容性”** 两大议题。

- **最活跃议题：** [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) 侧边栏 Agent 切换按钮
  - **诉求分析：** 用户通过手机浏览器访问后端，暴露出前端在低分辨率下的严重适配问题（功能按钮被挤出屏幕）。该议题 4 条评论中，用户呼声强烈，期望在“简介模式”下仍能切换 Agent、查看历史及新建聊天。这标志着 WebUI 已成为核心交互入口，移动端体验优化迫在眉睫。
- **最严重 Bug 讨论：** [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328) Deepseek 思考过程卡死
  - **诉求分析：** 这不仅是单一议题，更是用户情绪的集中爆发点。用户反馈“在 Web、Console、Tauri 端均会卡死”，需要手动“停止→继续”才能恢复。此问题严重损害了项目在主流模型下的稳定性口碑，是当前社区最大的信任负资产。
- **生态信任受损：** [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) 自定义 Provider 函数调用失效
  - **诉求分析：** 用户期望获得真正的“OpenAI 兼容”。OMLX 等高阶工具调用失效，对比 Ollama（原生支持）的工作正常，暴露了所谓“兼容 Provider”的实现可能存在请求格式或认证协议上的差异，破坏了用户对项目开放生态的期待。

## 5. Bug 与稳定性

按严重程度排列：

- **[紧急] Deepseek 思考死锁：** [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328)
  - 表现：Agent 在 `thinking` 阶段永久挂起，需手动干预。无关联修复 PR，推测问题可能涉及流式解析或 `reasoning/thinking` 字段的底层处理逻辑。
- **[紧急] API 静默丢包：** [#5344](https://github.com/agentscope-ai/QwenPaw/issues/5344) / [#5343](https://github.com/agentscope-ai/QwenPaw/issues/5343)
  - 表现：`/api/console/chat` 在 Agent 繁忙时返回 HTTP 200 但丢弃消息。这是上层自动化集成的事故隐患。其中 #5343 已关闭（可能误提或重复提交），#5344 仍在开放。
- **[严重] 自定义 Provider 函数调用残缺：** [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345)
  - 表现：手动添加的第三方 OpenAI 兼容服务无法触发 Function Calling，仅返回普通文本。预期并非所有 Provider 都应开箱即用，但项目应明确兼容性支持范围并给出清晰的排查指引。
- **[中等] 工具结果上下文爆炸：** [#5342](https://github.com/agentscope-ai/QwenPaw/issues/5342)
  - 表现：当 LLM 调用异常（如 502）时，上下文中的工具结果截断机制失效，可能导致 Token 指数级激增。贡献者已随 Issues 附带了初步防御性修复思路。
- **[低/已修复] Reasoning Block 类型兼容：** [#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208) 已关闭。解决了部分模型（如 LongCat-2.0-Preview）返回 `reasoning` 类型而非 `thinking` 导致的日志警告与计数不一致问题。

## 6. 功能请求与路线图信号

综合今日提出的需求与 PR 来看，项目正在向 **“全平台交互 Agent 与安全企业级基础设施”** 演进。

- **移动端与 UI 平权（高呼声）：**
  - [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) 侧边栏增强与 [#5327](https://github.com/agentscope-ai/QwenPaw/issues/5327) Agent 办公室对话，表明用户不再满足于桌面端操控，迫切需要在手机端获得完整的 Agent 管理体验。
  - [#5322](https://github.com/agentscope-ai/QwenPaw/issues/5322) 实时 UI 更新与语音通知，则是从“手动刷新”到“实时推送”的体验升级信号。
- **安全与隔离（强烈推进中）：**
  - [#5346](https://github.com/agentscope-ai/QwenPaw/pull/5346) (Docker 化) 与 [#5341](https://github.com/agentscope-ai/QwenPaw/pull/5341) (文件沙箱) 已进入 PR 阶段，预计将有较高优先级合并，成为下一版本的安全基座。
- **可观测性与透明度（基础设施完善）：**
  - [#5323](https://github.com/agentscope-ai/QwenPaw/pull/5323) 原生 Todo Write 面板，使得多步骤任务进度可追踪；[#5128](https://github.com/agentscope-ai/QwenPaw/pull/5128) Langfuse 优化，则增强了业务层面的调试能力。
- **性能与现代化（技术债偿还）：**
  - [#5348](https://github.com/agentscope-ai/QwenPaw/pull/5348) KV-Cache 优化与 [#5349](https://github.com/agentscope-ai/QwenPaw/pull/5349) ReMe4 迁移，表明项目组正在积极处理长期运行场景下的性能瓶颈与架构升级。

## 7. 用户反馈摘要

- **用户 A（高强度 Deepseek 用户）：** “Agent 在思考过程中经常卡死，必须手动点停止然后发送继续才能继续干活，这让人非常崩溃。我在 Windows 11 上所有前端（Web/Console/Tauri）都遇到了这个问题。”
- **用户 B（移动端先锋用户）：** “为了在手机上用，我直接访问了 backend API。但 UI 根本不行，切换 Agent 的按钮和看历史的按钮都被挤到屏幕外面去了。强烈要求在左边栏加个切换按钮。”
- **用户 C（API 集成开发者）：** “`/api/console/chat` 返回 200 但消息被静默丢弃了。这对于自动化脚本来说是致命缺陷，我们无法得知消息到底有没有被送达 Agent。”
- **用户 D（第三方模型探索者）：** “我尝试接入 OMLX（一个 OpenAI 兼容服务），但 Tool/Function Calling 完全用不了，只能返回纯文本。我的 Ollama 接入是正常的。这真的让我很困惑。”

**总结：** 用户对项目的底层 Agent 能力（适配主流模型、开放生态）有极高期望，同时对前端全平台体验（特别是移动端）提出了从“能用”到“好用”的迫切要求。当前的 Bug（如卡死、丢消息）正在严重侵蚀用户的新鲜感与信任度。

## 8. 待处理积压

| 编号 | 类型 | 标题 | 已开放时长 | 重要性 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328) | 严重 Bug | Deepseek Thinking 卡死 | 6 天 | **极高** | 无关联修复 PR，影响最大用户群之一，建议核心团队深度排查并给出临时缓解方案。 |
| [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) | 功能请求 | 侧边栏模式切换 Agent | 6 天 | **高** | 社区高频需求，决定移动端体验质量，建议排入近期 Sprint 解决。 |
| [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) | 严重 Bug | 自定义 Provider 函数调用失效 | 1 天 | **高** | 需明确项目对第三方 Vendor 的兼容性边界，并补充文档说明。 |
| [#5341](https://github.com/agentscope-ai/QwenPaw/pull/5341) | PR (First-time) | 文件工具沙箱约束 | 1 天 | **中** | 高质量安全补丁，等待 Review 合并。 |
| [#5346](https://github.com/agentscope-ai/QwenPaw/pull/5346) | PR (First-time) | Docker 化工具运行 | 1 天 | **中** | 新特性，安全架构重要一环，等待 Review。 |
| [#5348](https://github.com/agentscope-ai/QwenPaw/pull/5348) | PR (First-time) | 冻结环境上下文日期 (KV-Cache 优化) | 1 天 | **中** | 高收益低风险的性能补丁，建议快速 Review 合并。 |
| [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321) | PR (First-time) | Scroll 上下文管理器策略 | 2 天 | **中** | 复杂新功能，已进入 Review 阶段，需谨慎评估与现有机制的融合。 |

---

**免责声明：** 本报告基于 2026-06-21 提供的 GitHub 数据生成，数据源为 CoPaw（QwenPaw）仓库。项目健康度评估基于当前数据，实际情况请以仓库实时状态为准。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 · 2026-06-21

> 数据来源：GitHub `zeroclaw-labs/zeroclaw`  
> 报告覆盖时段：2026-06-20 14:00 UTC – 2026-06-21 14:00 UTC（约）

---

## 1. 今日速览

过去 24 小时项目保持极高活跃度：Issues 更新 50 条（新开+活跃 44、关闭 6），PR 更新 50 条（待合并 46、已合并/关闭 4）。无新版本发布，社区重心集中在修复长期存在的运行时稳定性问题（如上下文截断、工具调用循环、流式重复）以及推进 v0.9.0 认证与安全路线图。v0.8.2 Skills 平台与 v0.9.0 Auth 两大跟踪 Issue 均有实质性 PR 提交。值得注意的社区热点包括“Dream Mode”周期性记忆整合功能（18 条评论）以及用户对 `zeroclaw cron` 认知缺失的 bug（13 条评论）——后者已有修复 PR 提交。

---

## 2. 版本发布

**无新版本发布。**  
项目正处于 v0.8.2（Skills 平台）和 v0.9.0（Auth/安全）的并行开发阶段，两个里程碑均有多项 PR 处于评审中。

---

## 3. 项目进展

### 今日合并/关闭的重要 PR

由于数据中仅展示待合并 PR，已合并/关闭的 4 个 PR 未提供详细列表。但从 Issue 列表中可观察到 6 个已关闭 Issue（#6036、#6243、#5883、#5686、#7877、#7795），其中部分可能对应 PR 合入。以下为今日推进的关键 PR（均为待合并状态，但代表了项目的重要进展）：

| PR 编号 | 类型 | 影响域 | 摘要 |
|--------|------|--------|------|
| [#8050](https://github.com/zeroclaw-labs/zeroclaw/pull/8050) | fix | channel | 修复频道历史主动修剪时丢弃工具结果内容，提升对话连续性 |
| [#8048](https://github.com/zeroclaw-labs/zeroclaw/pull/8048) | fix | runtime | 运行时上下文压力下保留工具结果，并尊重 `history_pruning` 配置 |
| [#8014](https://github.com/zeroclaw-labs/zeroclaw/pull/8014) | fix | runtime | 修复原生工具调用前流式 narration 重复输出问题 |
| [#8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033) | feat | core | 引入对话式初始化助手，替换原有的 `zeroclaw onboard` 存根 |
| [#7945](https://github.com/zeroclaw-labs/zeroclaw/pull/7945) | feat | provider | 增加 xAI/Grok OAuth 登录支持，减少手动 API Key 操作 |
| [#8006](https://github.com/zeroclaw-labs/zeroclaw/pull/8006) | feat | zerocode TUI | 为代理提供商列表添加 Aliases/Costs 标签页，补全 Web 版已具备的功能 |
| [#7666](https://github.com/zeroclaw-labs/zeroclaw/pull/7666) | feat | gateway/cron | 添加 Cron 暂停/恢复 HTTP 接口，并限制代理更新范围 |
| [#8016](https://github.com/zeroclaw-labs/zeroclaw/pull/8016) | feat | scripts | 新增 `agent-preflight.sh` 预提交验证脚本，确保本地通过 CI 同等检查 |
| [#8004](https://github.com/zeroclaw-labs/zeroclaw/pull/8004) | fix | config | 使成本预算配置可热重载，避免启动时冻结 |
| [#8051](https://github.com/zeroclaw-labs/zeroclaw/pull/8051) | fix | channel | 禁止已禁用代理所属频道继续在线服务，修复配置透传断裂 |
| [#8032](https://github.com/zeroclaw-labs/zeroclaw/pull/8032) | fix | web | 按传输协议（命令/URL）正确标记 MCP 服务器字段的必填性 |
| [#8040](https://github.com/zeroclaw-labs/zeroclaw/pull/8040) | test | runtime | 新增 `should_execute_tools_in_parallel` 未覆盖分支的单元测试 |

**总结**：项目在**稳定性、可用性、可观测性**三个维度同时取得进展，尤其是频道历史与运行时上下文管理的修复将显著改善长对话体验。xAI OAuth 和对话式 onboard 体现了对用户上手成本的关注。

---

## 4. 社区热点

### 讨论最多的 Issues

| Issue | 标题 | 评论数 | 核心诉求 | 链接 |
|-------|------|--------|----------|------|
| #5849 | [Feature]: Dream Mode — Periodic Memory Consolidation & Reflective Learning | 18 | 提出空闲时周期性记忆整合与反思学习，增强模型长期记忆能力 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) |
| #5862 | [Bug]: zeroclaw does not know it can add cron | 13 | 用户让 zeroclaw 添加定时任务时，模型不知道自身拥有 `cron_add` 工具 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) |
| #6808 | RFC: Work Lanes, Board Automation, and Label Cleanup | 11 | 治理 RFC，讨论如何简化项目管理流程和标签清理，得到社区广泛回应 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) |

**分析**：
- **#5849** 反映出社区对“记忆”功能的持续深度需求——现有记忆机制在权重分配（#5844）和上下文溢出（#6517）上仍有痛点，Dream Mode 试图在空闲时段异步优化记忆结构，属于高价值功能请求，已有 `status:accepted` 标签。
- **#5862** 暴露了 agent 工具可见性的核心矛盾：用户自然语言表述任务，但模型无法感知自身工具集边界。该问题已由 PR #8080 提交修复，通过在 WebSocket 频道注入 cron 工具的默认交付配置来解决。
- **#6808** 是治理型 RFC，讨论工作流（Work Lanes）和标签自动化，显示项目在规模扩大后对管理效率的主动优化，契合项目从 v0.8 向 v0.9 演进的主线。

---

## 5. Bug 与稳定性

### 按严重程度排列的活跃 Bug

| 严重等级 | Issue | 标题 | 更新时间 | 关键影响 | 是否有修复 PR |
|---------|-------|------|----------|----------|--------------|
| **S0 - 数据丢失/安全风险** | [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) | `reasoning_content` 在小米思考模式工具调用循环中未回传 | 2026-06-20 | 多轮对话中思考内容断裂，可能导致信息丢失 | 无，阻塞中 |
| **S0 - 数据丢失/安全风险** | [#6558](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) | 部分自定义提供商 405 错误导致全部模型失败 | 2026-06-20 | 用户无法使用自定义 API | 无，待作者反馈 |
| **S1 - 工作流阻塞** | [#6036](https://github.com/zeroclaw-labs/zeroclaw/issues/6036) | Termux/Android 上 Agent 进入无限工具调用循环 | 2026-06-20（已关闭） | 特定环境持续死循环 | **已关闭**（待确认是否已合入修复） |
| **S1 - 工作流阻塞** | [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | 默认 32k 上下文预算被系统提示+工具定义超支 3.3 倍，导致持续截断 | 2026-06-20 | 首次交互即超限，严重影响对话质量 | 无，但 [#8048](https://github.com/zeroclaw-labs/zeroclaw/pull/8048) 通过优化修剪策略缓解 |
| **S1 - 工作流阻塞** | [#5883](https://github.com/zeroclaw-labs/zeroclaw/issues/5883) | macOS 服务启动失败 | 2026-06-20（已关闭） | 新用户无法通过 service 方式运行 | **已关闭** |
| **S2 - 行为降级** | [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | 系统提示过度强调记忆，导致当前提示被忽视 | 2026-06-20 | 特别是 cron job 中记忆权重过高 | 无，已接受 |
| **S2 - 行为降级** | [#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517) | 上下文溢出导致幻觉/主题偏移 | 2026-06-20 | 长对话后模型偏离原话题 | 无，阻塞中 |
| **S2 - 行为降级** | [#8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047) | ReadSkillTool 在 `data_dir` 而非 agent 工作目录查找技能文件 | 2026-06-20（新开） | 紧缩技能模式下模型无法读取技能 | 无，优先级 p2 |
| **S2 - 行为降级** | [#7795](https://github.com/zeroclaw-labs/zeroclaw/issues/7795) | `static_voice_peers` 缓存配置派生语音对端，存在配置偏离 | 2026-06-20（已关闭） | 单点真相违例，动态配置更新不生效 | **已关闭** |
| **S3 - 次要问题** | [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | 模型不知道自身可添加 cron | 2026-06-20 | 用户需求无法被满足 | **PR #8080 待评审** |

**稳定性评估**：今日活跃的 S0/S1 级 Bug 仍有 4-5 个未解决，但其中部分已有关联 PR（如 #5862 对应 PR #8080；#5808 的上下文压力场景被 #8048 部分修复）。Termux 无限循环和 macOS 启动失败问题已被关闭。整体上项目正在系统性地清理高优先级 Bug，但上下文管理和工具可见性仍是核心痛点。

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本的高热度功能

#### v0.9.0 认证与安全路线图

- **[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)**：OIDC 认证提供商支持（跟踪 Issue，已接受）
- **[#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)**：v0.9.0 认证、安全、网关、破坏性变更跟踪（含 131 个子项）
- **[#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076)**：本地用户名/密码 `AuthProvider`（#7141 的子任务，无 IdP 场景）

这三个 Issue 构成了 v0.9.0 的外围框架，PR #7945（xAI OAuth）是 AuthProvider 可插拔体系的实际落地。

#### v0.8.2 Skills 平台

- **[#7852](https://github.com/zeroclaw-labs/zeroclaw/issues/7852)**：v0.8.2 Skills 平台跟踪 Issue，包含注册表、技能解析、插件行为等
- **[#8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047)**：新提出的技能路径 Bug，或影响发布节奏

#### 其他高呼声功能

- **[#5849 (Dream Mode)](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)**：周期性记忆整合（已接受，但标记为 priority:p2，是否随 v0.8.2 发布仍不确定）
- **[#7950](https://github.com/zeroclaw-labs/zeroclaw/issues/7950)**：在 Docker 镜像中加入文档，使 agent 能回答自身用法问题（priority:p3，已接受）
- **[#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)**：流式卡片消息支持（QQ/企业微信/飞书等，已接受）
- **[#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)**：结构化可观测性增强（OTel 追踪关联，已接受）
- **[#6067](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)**：频道回复意图预检可配置化（使用轻量模型 + 超时）

**信号**：社区对**可观测性改进**（#7232、#6641）和**用户侧体验**（流式消息、文档内置、onboard 助手）的呼声显著高于纯功能扩展。这暗示项目在进入 v0.9 前将持续打磨运营体验和安全性。

---

## 7. 用户反馈摘要

从 Issues 评论和描述中提取的真实用户声音：

| 用户痛点/场景 | 相关 Issue | 用户原话（摘要） |
|--------------|------------|------------------|
| Agent 意识不到自己的工具能力 | [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | “I ask zeroclaw to let me do something every 8:00 PM. But zeroclaw says it does not have the tools to do this thing.” |
| 记忆权重过高，忽视当前 prompt | [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | “specially in cron jobs … gives too much value/weight to memories and less to current instructions” |
| 自定义 API 流式解码错误导致挂起 | [#6243](https://github.com/zeroclaw-labs/zeroclaw/issues/6243) | “ZeroClaw seems to hang after a streaming decode error … GPU usage stays around 50%” |
| Android/Termux 无限工具循环 | [#6036](https://github.com/zeroclaw-labs/zeroclaw/issues/6036) | “repeatedly outputting the same message without ever terminating or returning the actual result” |
| Slack 线程内首次提及消息上下文缺失 | [#6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055) | “users must re-@mention the bot for every message … would be much better to backfill thread context” |
| 长对话后幻觉偏移 | [#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517) | “When a conversation runs long enough … starts hallucinating — drifting off-topic” |
| 默认 32k 上下文首次迭代即超限 | [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | “The first LLM iteration of a fresh conversation already exceeds budget by ~3.3x” |
| 知识/技能文件路径错误 | [#8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047) | “When the agent calls read_skill(\"<name>\"), the tool returns 'Unknown skill'” |

**反馈特点**：
- **工具认知缺陷**是高频痛点——用户期望 agent 能主动利用自身工具，而非用户手动指定。
- **上下文管理**（记忆权重、预算超限、溢出）是影响稳定性的首要因素，多个 Issue 指向同一根因。
- **自定义提供商/外端代理**的兼容性仍是用户门槛，尤其在非 OpenAI 模型上更容易出错。

---

## 8. 待处理积压

以下为长期未响应或处于阻塞状态的 Issue / PR，需要维护者关注：

| 项目 | 编号 | 标题 | 标签 | 最后更新 | 备注 |
|------|------|------|------|----------|------|
| Issue | [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) | `reasoning_content` not passed back with Xiaomi thinking models | `needs-author-action`, `stale-candidate` | 2026-06-20 | 等待作者提供复现步骤，已标记为 stale |
| Issue | [#6558](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) | providers erro（自定义 API 405） | `needs-author-action`, `stale-candidate` | 2026-06-20 | 用户信息不足，无法复现 |
| Issue | [#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517) | Context Overflow Causes Hallucination / Topic Drift | `needs-author-action`, `stale-candidate` | 2026-06-20 | 同样阻塞，需作者提供更多细节 |
| Issue | [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | zeroclaw does not know it can add cron | `needs-author-action`, `r:needs-repro` | 2026-06-20 | 虽已有 PR #8080，但 Issue 本身仍标记需作者行动 |
| Issue | [#5907](https://github.com/zeroclaw-labs/zeroclaw/issues/5907) | RFC: Opt-in LSP support | `status:blocked`, `type:rfc`, `status:accepted` | 2026-06-20 | 已接受但阻塞，需要决策是否继续推进 |
| Issue | [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | Default 32k context budget exceeded on iteration 1 | `priority:p1`, `status:in-progress` | 2026-06-20 | 高优先级但修复范围未确定，需协调配置默认值 |
| PR | [#8051](https://github.com/zeroclaw-labs/zeroclaw/pull/8051) | Suppress bound channels when agent is disabled | – | 2026-06-21 | 待评审，对配置热加载修复起直接作用 |
| PR | [#8048](https://github.com/zeroclaw-labs/zeroclaw/pull/8048) | Keep tool-result content under context pressure | – | 2026-06-21 | 待评审，直接影响长对话稳定性 |

**建议**：对于标记为 `stale-candidate` 且 `needs-author-action` 的三个 Issue（#6672、#6558、#6517），如果作者未在下一个检查点响应，应予以关闭或标记为“无法复现”。同时，#5808 和 #5907 的高优先级任务需在每周治理会议中确定时间线。PR #8051 和 #8048 涉及运行时核心行为，建议优先评审。

---

**总结**：ZeroClaw 正处于功能丰富与稳定性打磨并行的关键期。社区参与活跃，修复与功能 PR 数量可观，但 Tool 可见性和上下文管理的根本性问题仍需持续投入。v0.9.0 的认证路线图已有明确交付件，整体项目健康度良好，但需警惕高严重度 Bug 的堆积。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*