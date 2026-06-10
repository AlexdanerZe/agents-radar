# OpenClaw 生态日报 2026-06-10

> Issues: 442 | PRs: 482 | 覆盖项目: 13 个 | 生成时间: 2026-06-10 03:26 UTC

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

好的，这是为您生成的OpenClaw项目2026年6月10日动态日报。

---

## OpenClaw 项目日报 (2026-06-10)

### 1. 今日速览

- **整体活跃度**：过去24小时项目活跃度极高，社区提交了442条Issue更新和482条PR更新，呈现在高度活跃的开发和反馈状态。
- **维护效率**：超过130个PR（约27%）和124个Issue（约28%）被关闭/合并，显示出维护团队正在积极处理社区提交，整体流转速度健康。
- **质量焦点**：当前社区反馈高度集中在消息丢失（message-loss）、会话状态错乱（session-state）和安全性（security）等严重影响用户体验的问题上，多个P1级Bug正等待维护者决策或修复。
- **新版本发布**：发布了两个新版本，主要修复了QQ机器人思维链内容泄露的安全问题，并对MCP工具结果处理进行了增强。

### 2. 版本发布

- **[v2026.6.5](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5) & [v2026.6.5-beta.6](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.6)**
    - **Highlights**: 这两个版本的亮点内容完全一致。
        1.  **QQBot 安全修复**: 现在会在将模型回复传递给渠道前，剥离模型内部的推理/思考脚手架（`<thinking>`标签），防止原始推理内容泄漏到频道回复中。这是对用户隐私和安全性的重要改进。 (PRs [#89913](https://github.com/openclaw/openclaw/pull/89913), [#90132](https://github.com/openclaw/openclaw/pull/90132))
        2.  **MCP工具结果增强**: 对MCP工具返回的结果进行了强制类型转换，以更可靠地处理`resource_link`、`resource`、`audio`、格式错误的图片等类型的数据，提高了跨模型和工具的兼容性。

    **注意**：文本中Highlights部分在此处截断，可能存在未完整列出的更新项。由于该描述同时出现在正式版和测试版中，建议用户详细查阅Release Notes以获取完整的变更列表，尤其是测试版可能包含更多实验性功能或破坏性变更。

### 3. 项目进展

过去24小时内，项目在多个关键领域取得了显著进展，多项重要修复被合并或关闭：

- **核心稳定性与问题修复**:
    - **[PR #91811 (CLOSED)](https://github.com/openclaw/openclaw/pull/91811)**: 修复了Cron定时任务在`runHeartbeatOnce()`因心跳禁用而返回`skipped: disabled`时，未能正确触发守护运行的问题。现在会优雅地回退到入队一个心跳请求，避免一次性任务被错误地标记为跳过。 (fix(cron): queue disabled wake fallback for one-shots)
    - **[PR #91785 (CLOSED)](https://github.com/openclaw/openclaw/pull/91785)**: 增强了iMessage渠道的启动诊断能力，当丢弃回显/反射消息时，会记录更详细的隐私安全日志（包括账户、原因、聊天ID等），方便排查启动问题。 (fix(imessage): surface inbound startup diagnostics)
    - **[PR #91590 (CLOSED)](https://github.com/openclaw/openclaw/pull/91590)**: 修复了Codex会话中上下文引擎（context-engine）压缩所有权的问题。现在明确了主上下文引擎的压缩职责，Codex原生压缩仅作为次要补充，解决了此前可能出现的会话状态冲突。 (Fix context-engine compaction ownership for Codex sessions)
- **用户界面与体验**:
    - **[PR #91557 (CLOSED)](https://github.com/openclaw/openclaw/pull/91557)**: 大幅改进了iPad和iPhone的控制界面，为iPad带来了类似macOS的侧边栏导航模型，并为手机端增加了对Workboard等功能的支持。 (Improve iPad and iPhone control surfaces)
- **平台与功能修复**:
    - **[PR #89251 (CLOSED)](https://github.com/openclaw/openclaw/pull/89251)**: 修复了WhatsApp渠道上TTS（文本转语音）工具音频无法送达的问题。 (fix: deliver tts tool audio on whatsapp)
    - **[PR #85669 (CLOSED)](https://github.com/openclaw/openclaw/pull/85669)**: 修复了`sessions_history`返回未过滤的`delivery-mirror`消息，导致仪表盘出现重复消息的问题，提升了会话历史的准确性。 (sessions_history returns unfiltered delivery-mirror messages)
- **配置与兼容性**:
    - **[PR #44599 (CLOSED)](https://github.com/openclaw/openclaw/pull/44599)**: 修复了`OPENCLAW_CONFIG_DIR`环境变量路径中包含空格时导致安装失败的问题，提高了对系统配置的兼容性。 ([Bug]: OPENCLAW_CONFIG_DIR cannot contain whitespace)

**总结**：项目在修复关键Bug（特别是会话状态和渠道兼容性）的同时，也积极推进了新特性（如移动端UI改进）和关键安全修复（如版本发布中的QQBot修复），整体势头良好。

### 4. 社区热点

以下是今日讨论热度最高、最能反映社区诉求的议题：

1.  **工具调用间文本泄露 (Issue #25592)**: 这是当前社区最关注的议题之一，获得29条评论。用户报告当Agent在工具调用之间产生文本（如错误处理或叙述性内容）时，这些内部处理输出会作为可见消息被发送到消息渠道（如Slack、iMessage）。这是一个显著的**UX和隐私问题**，用户希望严格区分内部处理与最终回复。该Issue已被标记为`impact:security`和`impact:message-loss`，且关联了修复PR。 [查看讨论](https://github.com/openclaw/openclaw/issues/25592)
2.  **OpenAI ChatGPT Responses传输失败 (Issue #90083)**: 这是一个影响广泛的P1级回归问题，已关闭。大量用户升级到`2026.6.1`后，尝试使用最新的`gpt-5.4`和`gpt-5.5`模型时遭遇`invalid_provider_content_type`错误。该问题迅速获得16条评论和3个👍，表明社区对最新模型支持的强烈需求和高敏感性。该Bug已被修复。 [查看讨论](https://github.com/openclaw/openclaw/issues/90083)
3.  **Agent回复错乱 (Issue #32296)**: 用户报告Agent会错误地回答上一条用户消息，导致对话上下文错乱。这个问题严重影响了对话的连贯性，被标记为`impact:session-state`和`impact:message-loss`，属于P1级Bug，但目前仍未修复，需要产品决策。 [查看讨论](https://github.com/openclaw/openclaw/issues/32296)
4.  **Codex应用服务器“停摆”回归问题 (Issue #88312)**: 用户报告在`2026.5.27`版本中，Codex应用服务器（ChatGPT Plus子服务）在执行多工具Agent轮次时，频繁出现“Codex stopped before confirming the turn was complete”的错误。这是对之前（#84076）修复的回归，影响范围大，被标记为P1级Bug。 [查看讨论](https://github.com/openclaw/openclaw/issues/88312)

**分析**：社区热点集中在消息传递的可靠性、上下文管理的准确性以及对最新模型的支持上。用户对Agent产生“噪音”消息和“答非所问”的容忍度很低，对核心功能的倒退（回归Bug）反应强烈。

### 5. Bug 与稳定性

以下为今日报告的严重Bug及回归问题，按严重程度排列：

**P1（最高优先级）**
- **[Bug]: 工具调用间文本泄露 (#25592)** `[impact:security, impact:message-loss]` - 严重UX/安全问题。**关联Fix PR，状态等待审核**。 [查看详情](https://github.com/openclaw/openclaw/issues/25592)
- **[Bug]: Agent回复错乱 (#32296)** `[impact:session-state, impact:message-loss]` - 核心对话逻辑错误。**等待产品决策**。 [查看详情](https://github.com/openclaw/openclaw/issues/32296)
- **[Bug]: [Regression] Codex app-server停摆回归 (#88312)** `[impact:session-state, impact:message-loss]` - 关键功能回归。**等待产品决策与直播复现**。 [查看详情](https://github.com/openclaw/openclaw/issues/88312)
- **[Bug]: Discord运行失败，会话文件锁定问题 (#86508)** `[impact:session-state, impact:message-loss]` - P1级回归问题。**等待直播复现**。 [查看详情](https://github.com/openclaw/openclaw/issues/86508)
- **[Bug]: 网关内存泄漏导致OOM被杀 (#89315)** `[impact:session-state, impact:crash-loop]` - P1级崩溃问题。**等待产品决策**。 [查看详情](https://github.com/openclaw/openclaw/issues/89315)
- **[Bug]: 子Agent在会话写锁超时时阻塞 (#86538)** `[impact:session-state, impact:message-loss]` - 影响会话并发处理。**有关联修复PR**。 [查看详情](https://github.com/openclaw/openclaw/issues/86538)

**P2（中优先级）**
- **[Bug]: Matrix线程回复回归 (#87307)** `[impact:session-state, impact:message-loss]` - P1级渠道功能回归。**等待用户提供信息**。 [查看详情](https://github.com/openclaw/openclaw/issues/87307)
- **[Bug]: Docker + Sandbox无法访问Workspace (#31331)** `[impact:session-state, impact:security]` - 影响Docker部署用户。**等待安全审核**。 [查看详情](https://github.com/openclaw/openclaw/issues/31331)
- **[Bug]: 会话写锁超时阻塞 (#86538)** - 影响多Agent并发。**有关联修复PR**。 [查看详情](https://github.com/openclaw/openclaw/issues/86538)

**稳定性/性能问题**
- **[Bug]: 网关堆内存无限增长 (#89315)** - 导致长时间运行的系统被OOM Killer杀死。**等待产品决策**。 [查看详情](https://github.com/openclaw/openclaw/issues/89315)

### 6. 功能请求与路线图信号

- **Persistent task-status surface (Issue #52640)**: 社区希望为长时间运行的渠道任务（如Discord）提供一个持久化的、统一的任务状态展示界面。当前的各种指示器仍显碎片化。这是一个有价值的用户体验增强，但尚无明确进展。 [查看详情](https://github.com/openclaw/openclaw/issues/52640)
- **预压缩内存刷新验证 (Issue #90354)**: 用户建议为预压缩内存刷新（pre-compaction memory flush）添加大小限制、写入后验证和静默失败处理，以防止模型写入过大或乱码内容。这反映了社区对系统鲁棒性的更高要求。 [查看详情](https://github.com/openclaw/openclaw/issues/90354)
- **按渠道/群组/DM的模型覆盖 (Issue #53638)**: 允许在`openclaw.json`中为不同对话配置不同模型，而非只能使用全局默认。这是一个呼声很高的配置灵活性需求。 **社区呼声较高**。 [查看详情](https://github.com/openclaw/openclaw/issues/53638)
- **上下文溯源 (Context Provenance) (Issue #54373)**: 用户希望系统能在提示词中标记上下文的来源（如会话启动时注入 vs. 当前轮次读取），让Agent能更好地理解信息时效性和重要性。这是一个前瞻性的功能，旨在提升Agent的智能表现。 [查看详情](https://github.com/openclaw/openclaw/issues/54373)

**信号提示**：新发布的 **[PR #91438 (feat(voice-call): Microsoft Teams provider)](https://github.com/openclaw/openclaw/pull/91438)** 展示了项目正在扩展新的渠道能力（Teams语音/视频）。此外， **[PR #91807 (feat(cli): support --file for image generate)](https://github.com/openclaw/openclaw/pull/91807)** 补齐了CLI工具的功能，体现了对命令行用户使用体验的持续优化。这些活跃的PR可能预示着下一版本的重点方向。

### 7. 用户反馈摘要

- **痛点**:
    - **消息噪声**：多位用户报告Agent将内部调试信息（如`<thinking>`标签、工具调用JSON）泄露到用户聊天界面 (#25592, #44905)，严重影响沟通体验和信息安全。
    - **上下文混乱**：`Agent回复错乱` (#32296) 和 `会话写锁阻塞` (#86538) 等问题导致对话逻辑断裂，用户需要反复纠正，体验受阻。
    - **渠道功能退化**：Matrix和Telegram等渠道的用户反馈在升级后遇到线程回复、消息送达等核心功能异常 (#87307, #84569)，影响了稳定性。
    - **配置兼容性**：Docker Sandbox环境中的Workspace挂载问题 (#31331) 和RISC-V架构上的部署问题 (#54253) 增加了特定用户群体的上手门槛。
- **满意度与需求**:
    - 用户对新模型（如`gpt-5.4`/`5.5`）的支持非常敏感，一旦出现故障，反馈会迅速且大量出现 (#90083)。
    - 社区对高级配置和精细化控制的需求持续增长，如按渠道模型覆盖 (#53638)、可配置的文件权限 (#56263) 等。
    - 用户对Agent的智能化有更高期望，希望它能感知上下文的来源和“状态”（如Issue #54373），而不仅仅是文本处理。

### 8. 待处理积压

以下为长期未获维护者响应或决策，但影响较大的重要Issue，建议维护者关注：

1.  [Issue #25592] **文本泄露问题** - `[stale, P1]` 尽管有关联PR，但状态仍停滞在`needs-maintainer-review`和`needs-product-decision`阶段，已开放逾3个月。 [查看详情](https://github.com/openclaw/openclaw/issues/25592)
2.  [Issue #32296] **Agent回复错乱** - `[P1]` 核心Bug，已开放逾3个月，等待`needs-product-decision`。 [查看详情](https://github.com/openclaw/openclaw/issues/32296)
3.  [Issue #31331] **Docker Sandbox Workspace问题** - `[P1, stale]` 严重的安全/功能Bug，等待`needs-security-review`。 [查看详情](https://github.com/openclaw/openclaw/issues/31331)
4.  [Issue #54253] **RISC-V64系统部署失败** - `[stale, P2]` 支持新硬件平台的用户诉求，等待`needs-info`和`product-decision`。 [查看详情](https://github.com/openclaw/openclaw/issues/54253)
5.  [Issue #48003] **Steer模式消息注入失败** - `[P1, stale]` 核心功能缺陷，等待`linked-pr-open`状态更新。 [查看详情](https://github.com/openclaw/openclaw/issues/48003)

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析报告

**报告日期：** 2026-06-10  
**数据源：** 12 个核心开源项目社区动态日报

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于 **高速扩张与质量巩固并行的阶段**。今日所有统计项目（除 3 个沉寂外）均保持高活跃度，社区提交了大量 Issues 与 PRs，但合并率与维护响应速度参差不齐。**安全与稳定性取代新功能成为第一优先级**：PicoClaw 一次披露 15 个安全漏洞、OpenClaw 和 Hermes Agent 多起 P1 级消息丢失 / 上下文混乱 Bug 均表明，生态正从“先跑起来”转向“跑得可靠”。同时，多模型协作、记忆进化、技能市场等平台化诉求高频出现，反映出开发者不再满足于单一 Agent 能力，而是追求可编排、可观测、可扩展的智能体基础设施。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issues 更新数 | 今日 PR 更新数 | 版本发布 | 综合健康度 |
|:---|:---:|:---:|:---:|:---|
| **OpenClaw** | 442 条 | 482 条 | ✅ v2026.6.5 / beta.6 | 极高，维护效率高（关闭率约28%） |
| **ZeroClaw** | 50 条 | 50 条 | 无 | 极高，密集攻坚期，PR 积压少 |
| **Hermes Agent** | 50 条 | 50 条 | 无 | 高，但合并瓶颈（仅1 PR 合并） |
| **IronClaw** | 45 条 | 50 条 | 无 | 高，PR 积压48个待审 |
| **CoPaw (QwenPaw)** | 42 条 | 38 条 | ✅ v1.1.11-beta.2 | 高，修复与功能并行 |
| **NanoClaw** | –（未细分） | 43 条（39 合并/关闭） | 无 | 极高，“集中清仓”式合并 |
| **PicoClaw** | 15 安全 Issue + 日常 | 11 个活跃 PR | ✅ Nightly | 极高，但安全修复压力大 |
| **NanoBot** | 6 新开 | 25 个（10 合并） | 无 | 高，响应快（GPT-5兼容当天修复） |
| **NullClaw** | 5 条（1新开/4关闭） | 7 合并/关闭 + 1 新 | 无 | 高，合并率好 |
| **LobsterAI** | 1 条 | 3 合并/关闭 | 无 | 中，功能收敛阶段 |
| **Moltis** | 1 条 | 0 | 无 | 低，维护宁静期 |
| **TinyClaw** | 0 | 0 | 无 | 沉寂 |
| **ZeptoClaw** | 0 | 0 | 无 | 沉寂 |

*注：部分项目未精确列出 Issue/PR 具体更新数，采用日报描述中的关键数字，口径尽量对齐。*

---

## 3. OpenClaw 在生态中的定位

- **社区规模与活跃度绝对领先**：Issues/PRs 数量（442/482）是第二梯队的 5~10 倍，表明其拥有最庞大的用户与贡献者基数。
- **技术路线偏“稳健核心”**：关注消息交付可靠性、会话状态严谨性、安全剥离（如 `<thinking>` 标签泄露修复），定位是**生产级通用 Agent 框架**。相比 Hermes Agent 侧重桌面自动化、PicoClaw 侧重轻量边缘部署，OpenClaw 提供的是一套完整、保守但无短板的底座。
- **竞争力优势**：
  - 维护效率高（关闭率约28%），P1 级 Bug 多数有关联修复 PR，决策路径短。
  - 渠道覆盖广（iMessage, WhatsApp, Discord, QQ, Teams 等），生态集成深度第一。
  - 版本发版节奏稳定（当日双版本），适合要求高可靠性的团队采用。
- **潜在短板**：部分高级功能（如跨模型子任务、技能市场）不如 NanoClaw 或 LobsterAI 激进，可能在创新灵活性上落后。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目及具体体现 |
|:---|:---|
| **消息丢失/上下文混乱** | OpenClaw（#25592 工具调用间文本泄露、#32296 回复错乱）、NanoBot（#4259 跨会话记忆注入）、ZeroClaw（#5808 32K上下文被系统提示耗尽、#6034 用户消息丢失）、Hermes Agent（#43175 搜索注入巨型上下文）|
| **多模型/Provider 动态切换** | NanoBot（#4253 对话级模型覆盖）、OpenClaw（#53638 按渠道模型覆盖）、ZeroClaw（#5937 Provider 架构重构）、IronClaw（#4548 DeepSeek model字段重复）|
| **安全与隐私加固** | PicoClaw（15 个 SSRF/授权绕过漏洞）、OpenClaw（#25592 工具调用文本泄露）、NanoBot（#4119 符号链接逃逸）、ZeroClaw（#5775 per-skill 权限）|
| **Agent 记忆与上下文理解** | CoPaw（#4994 记忆自进化）、Hermes Agent（#43267 避免巨型摘要回注）、LobsterAI（#2132 子任务状态同步）、ZeroClaw（#5844 记忆与当前提示平衡）|
| **平台化与开发者生态** | NanoClaw（技能市场、WebUI、直接运行模式）、CoPaw（技能批量下载、AgentHub 导入）、ZeroClaw（从 .well-known 安装 Skills）|
| **可观测性与成本控制** | NanoClaw（链路追踪 Dashboard）、ZeroClaw（#7248 缓存 token 成本核算、OTel 集成）、IronClaw（trajectory observer）、OpenClaw（#54373 上下文溯源）|

这些方向表明，**生态已从“单会话聊天”进入“多模型、可记忆、可观测、安全合规”的企业级 Agent 阶段**。

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 关键技术特征 |
|:---|:---|:---|:---|
| **OpenClaw** | 全功能生产级 Agent 框架 | 追求稳定与广泛集成的团队 | 高渠道覆盖，消息可靠性优先，维护效率高 |
| **NanoBot** | 轻快灵活的个人 AI 助手 | 个人开发者和极客 | WebUI 分支对话，快速跟进前沿模型（GPT-5 当天修复） |
| **Hermes Agent** | 桌面端+自动化任务引擎 | 重度自动化和 Cron 用户 | Kanban 看板、Cron 作业、终端 PTY，桌面客户端 |
| **PicoClaw** | 轻量嵌入式 Agent（边缘/嵌入式） | 资源受限的 IoT/嵌入式场景 | 体积小，但安全基础薄弱 |
| **NanoClaw** | 通用 Agent 中间件/平台 | 构建自定义 Agent 服务的团队 | 插件系统、技能市场、直接运行模式，多运行时抽象 |
| **NullClaw** | 精简稳定 Agent 核心 | 寻求小而精部署的用户 | 快速修复日常 Bug，跨实例记忆同步，自定义 Provider |
| **IronClaw** | 企业级生产就绪 Agent | 需要合规、多租户、审计的企业 | Reborn 平台、附件全链路、持久化审批策略、NEAR AI 集成 |
| **LobsterAI** | 异构多模型协调 | 需要混合模型工作流的高级用户 | 专注跨模型子任务（如 M3+DeepSeek），但尚未成熟 |
| **CoPaw (QwenPaw)** | 国内生态适配的 Agent 框架 | 中文用户，依赖千问/通义生态 | 后端迁移至 AgentScope 2.0，AgentHub 导入 |
| **ZeroClaw** | 自动化运维与 SOP 引擎 | DevOps/SRE 团队 | AMQP 通道、SOP 流程引擎、多租户 RBAC 规划 |
| **Molti / Tiny / Zepto** | 停滞或维护态 | – | – |

---

## 6. 社区热度与成熟度

通过 Issue/PR 数量、合并效率、版本频率及 Bug 修复质量综合评估：

- **第一梯队（极高活跃 + 较成熟治理）：**  
  **OpenClaw**（规模最大，流程完善）、**ZeroClaw**（密集开发，PR 质量高）、**IronClaw**（企业级节奏，但 PR 积压稍多）、**CoPaw**（国内最活跃，Bug 修复速度快）  
  → 适合作为现成方案或参照实现。

- **第二梯队（高活跃，但存在明显瓶颈或处于转型）：**  
  **Hermes Agent**（社区贡献多但合并率低，审核拖后腿）、**PicoClaw**（活跃但安全事件堆积）、**NanoClaw**（集中合并清除长周期积压，功效待验证）、**NanoBot**（功能更新快但规模较小）  
  → 值得关注，但采用前需评估维护响应能力。

- **第三梯队（中等活跃或低活）：**  
  **NullClaw**（精炼但规模小）、**LobsterAI**（只有特定场景亮点，整体慢）、**Moltis**（仅1 Issue，进入沉寂期）  
  → 适合特定需求，不适合作为主力框架。

- **沉寂项目：** TinyClaw、ZeptoClaw — 过去24小时零活动，可能已暂停。

---

## 7. 值得关注的趋势信号

1. **Agent 安全不再只是附加要求**：PicoClaw 15个漏洞一次性曝光、OpenClaw 工具调用文本泄露升至 P1，表明安全需要嵌入架构层面（如零信任工具调用、配置项最小权限默认值）。开发者应主动审查 Agent 框架的 SSRF、授权、隔离能力。

2. **多模型编排成为下一个“标配”**：LobsterAI 的跨模型子任务、NanoBot 的对话级覆盖、ZeroClaw 的 Provider 重构提示，都指向 Agent 不再绑定单一模型。未来评估框架时需考虑其对异构推理路由的支持能力。

3. **“记忆”需可解释、可追溯、可分离**：多个项目同时遭遇记忆污染（跨会话、搜索注入）和压缩丢失问题。单纯的 RAG 或向量存储不够，Agent 需要上下文溯源（如 OpenClaw #54373）和智能压缩策略，这将是区分 Agent 智能水平的分水岭。

4. **技能市场与插件系统推动平台化**：NanoClaw、CoPaw、ZeroClaw 均在构建标准化技能分发机制（标签、批量安装、.well-known 协议）。**中间件层**正在从 Agent 框架中分离，成为独立竞争赛道。

5. **可观测性与成本治理并行兴起**：Token 层面的调用链路、缓存核算、OTel 集成开始出现在 NanoClaw、ZeroClaw、IronClaw 路线图中。对于计划将 Agent 投入生产环境（尤其是结合公共 API）的团队，这些能力将直接影响运营效率和成本控制。

**对 AI 智能体开发者的参考价值：**
- 若追求**稳定与广泛集成**：首看 OpenClaw，治理成熟，社区支持最强。
- 若聚焦**自动化与桌面交互**：Hermes Agent 是唯一专注此场景的活跃项目，但需接受合并延迟。
- 若面向**企业级生产环境**：IronClaw、ZeroClaw 在多租户、SOP、TEE 方面更有建树。
- 若构建**个人轻量助手**：NanoBot、NanoClaw 提供了更现代的开发体验与快节奏功能迭代。
- 所有项目均**急需建立可配置的上下文预算控制、安全沙箱、及跨模型调度能力**，这些将是未来判别 Agent 框架优劣的核心维度。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-10

---

## 1. 今日速览

过去 24 小时内，NanoBot 项目呈现出极高的开发活跃度。社区共提交了 **25 个 Pull Request**，其中 **10 个已被合入或关闭**，同时新开 **6 个 Issue** 用于反馈缺陷与功能请求。尽管本轮没有正式的版本发布，但在功能迭代（WebUI 分支对话、飞书 LaTeX）、核心稳定性修复（内存游标、WebSocket 数据丢失）和生态扩展（StepFun ASR Provider）上均有显著进展。维护团队与社区贡献者的协作效率突出，特别是在 GPT-5 兼容性等紧急问题上实现了 **1 天内提交修复 PR** 的快速响应。整体而言，项目正处在功能与质量并行提升的健康高增长周期中。

---

## 2. 版本发布
本轮周期无新版本发布，该章节省略。

---

## 3. 项目进展

今日合并/关闭的 5 个 PR 为项目注入了关键功能与优化：

- **WebUI 交互增强**：PR [#4208](https://github.com/HKUDS/nanobot/pull/4208)（已合并）实现了在任意助手回复节点创建分支对话（Fork from here）的功能，用户可无风险地尝试不同对话分支路径，大幅提升了对话管理与实验的灵活性。
- **飞书渠道 LaTeX 支持**：PR [#3434](https://github.com/HKUDS/nanobot/pull/3434)（已合并）正式为飞书频道集成基于 CodeCogs 的 LaTeX 公式渲染方案，学术和教育类用户可在飞书端直接读取公式，且无需安装额外依赖。
- **智能体权限精细化**：PR [#3400](https://github.com/HKUDS/nanobot/pull/3400)（已合并）为 Dream 模块新增 `allow_edit_identity_files` 配置项，用户现可精细控制自动脚本是否能修改 `USER.md` 和 `SOUL.md`，在自动化效率与数据安全之间取得了更好的平衡。
- **文档体系重构**：PR [#4177](https://github.com/HKUDS/nanobot/pull/4177)（已合并）彻底重构了项目文档入口，针对零基础用户、CLI 用户、WebUI 用户及贡献者设计了差异化的引导路径，有效降低了新用户的上手门槛。
- **例行维护**：PR [#4265](https://github.com/HKUDS/nanobot/pull/4265)（已合并）调整了 `daily-english-read` 技能的内置 Cron 计划，将频率从每日降为每两日一次。

---

## 4. 社区热点

### 最具共鸣的功能需求：多 Provider 动态切换
Issue [#4253](https://github.com/HKUDS/nanobot/issues/4253) 获得今日最高评论数（3条）。用户 `rombert` 表达了在同一个工作流中灵活切换“高速公共 OpenRouter 模型”与“低成本私密 Llamacpp 模型”的强烈需求，直接揭示了当前全局静态模型配置模式的局限，预计将成为未来会话配置系统升级的核心驱动力。

### 最硬核的深度反馈：上下文污染数据流分析
Issue [#4259](https://github.com/HKUDS/nanobot/issues/4259) 来自用户 `chxuan`，是一份教科书级别的 Bug 报告。该 Issue 完整追溯了 `history.jsonl` 未作会话隔离而导致多会话上下文混入 System Prompt 的完整数据流路径。虽然评论数不多（2条），但其技术严谨性直接关联到正在进行的 Memory 模块大规模重构（[#4193](https://github.com/HKUDS/nanobot/pull/4193) / [#4256](https://github.com/HKUDS/nanobot/pull/4256)），是社区技术深度的直接体现。

### 最紧急的兼容性警报：GPT-5 报错
Issue [#4261](https://github.com/HKUDS/nanobot/issues/4261) 指出 `OpenAICompatProvider` 错误地向 GPT-5.x/Reasoning 模型发送了不兼容的 `max_tokens` 参数，导致调用直接失败。该问题爆发后，社区快速响应，当天即有两条修复 PR（[#4263](https://github.com/HKUDS/nanobot/pull/4263) / [#4268](https://github.com/HKUDS/nanobot/pull/4268)）被提交，展现出项目对前沿模型生态的敏锐度。

---

## 5. Bug 与稳定性

| 严重程度 | 描述 | 关联 Issue / PR | 当前状态 |
| :--- | :--- | :--- |:--- |
| **紧急** | GPT-5.x / o-series 模型因传递 `max_tokens` 而非 `max_completion_tokens` 报 400 错误 | [#4261](https://github.com/HKUDS/nanobot/issues/4261) | **已有 2 个 Fix PR**（[#4263](https://github.com/HKUDS/nanobot/pull/4263), [#4268](https://github.com/HKUDS/nanobot/pull/4268)）待合并 |
| **严重** | `history.jsonl` 跨会话注入，不同对话的记忆被无隔离地混入当前会话 System Prompt | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | 已确认，已在关联的内存模块重构（[#4193](https://github.com/HKUDS/nanobot/pull/4193), [#4256](https://github.com/HKUDS/nanobot/pull/4256)）中着手解决 |
| **严重** | `idleCompact` 机制仅保留最后 8 条消息，导致用户对模型的纠正和正确结论在压缩过程中丢失 | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | 确认存在，待讨论修复方案 |
| **中等** | WebSocket 时序竞争导致 WebUI 在渲染时静默丢弃完整的助手回复 | PR [#4267](https://github.com/HKUDS/nanobot/pull/4267) | **已提交修复**（Open 状态） |
| **中等** | `split_message` 函数在字符边界截断时破坏代码块 Fence，导致两端 HTML 渲染错乱 | PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) | **已提交修复**（Open 状态） |
| **中等** | `apply_patch` 工具在添加文本行时出现不合预期的合并与换行问题 | PR [#4266](https://github.com/HKUDS/nanobot/pull/4266) | **已提交修复**（Open 状态） |
| **低** | `MemoryStore` 历史游标在特定边缘条件下分配异常 | PR [#4256](https://github.com/HKUDS/nanobot/pull/4256) | **已提交修复**（Open 状态） |

---

## 6. 功能请求与路线图信号

- **对话级模型覆盖** ([#4253](https://github.com/HKUDS/nanobot/issues/4253))：呼声极高，要求打破全局模型配置的限制，实现单会话级别的 Provider 与模型动态切换。这可能催生未来版本中一套全新的会话配置覆盖系统。
- **Agent 系统体验打磨**：PR [#4269](https://github.com/HKUDS/nanobot/pull/4269)（改进工具箱迭代次数耗尽时的总结性回复）与 Issue [#4262](https://github.com/HKUDS/nanobot/issues/4262)（Agent 模式启动时立即加载自定义 `botIcon`）共同指向社区对 Agent 交互细节持续优化的诉求。
- **渠道与多模态拓展**：PR [#4260](https://github.com/HKUDS/nanobot/pull/4260) 新增了 StepFun ASR 语音识别 Provider，表明项目正在积极拓展语音输入前端。PR [#4255](https://github.com/HKUDS/nanobot/pull/4255) 提出的按需版本检查替代实时轮询机制，也体现了 WebUI 向轻量化性能设计演进的趋势。

---

## 7. 用户反馈摘要

- **多任务流的拥塞点**：用户 `rombert`（[#4253](https://github.com/HKUDS/nanobot/issues/4253)）典型的工作流依赖“高速公共模型”与“私密本地模型”混合使用，当前的全局静态配置是其效率提升的主要障碍。这类需求在高级用户中具有代表性。
- **长期记忆的信任危机**：用户 `chxuan`（[#4259](https://github.com/HKUDS/nanobot/issues/4259)）和 `imkuang`（[#4264](https://github.com/HKUDS/nanobot/issues/4264)）的反馈精准指向了记忆系统的两大硬伤——**会话污染**和**纠正丢失**。这类 Bug 直接动摇了用户对 Agent 长期记忆可靠性的信任，同时也展现了社区极高的技术质检水平。
- **对新模型的渴求**：用户 `mraad`（[#4261](https://github.com/HKUDS/nanobot/issues/4261)）第一时间升级到 GPT-5.4 却遭遇服务不可用，其对应的快速修复体现了社区对前沿模型兼容性的高关注度。
- **协作式共建**：上述 Bug 报告均提供了详尽的数据流分析（特别是 #4259），说明社区不仅在使用产品，更在以共建者的姿态深度参与项目演进。

---

## 8. 待处理积压

- **#3869 - DeepSeek 消息处理器修复**（开放 25 天）：该 PR 旨在解决 DeepSeek 模型对 `null content` 抛 400 错误以及 `"(empty)"` 占位符泄漏的问题。作为重要的开源模型提供商，此问题直接影响了 DeepSeek 用户的基础可用性，建议维护者尽快完成评审与合入。
- **#4119 - 符号链接工作区逃逸修复**（开放 10 天）：由核心贡献者 `yu-xin-c` 提交的沙箱安全修复，用于阻断通过相对符号链接绕过工作区路径限制的攻击向量。考虑到安全类的修复时效性很重要，建议优先合并。
- **#4061 - 部分 OpenAI 兼容 Provider 工具调用解析失效**（开放 12 天）：当上游 API 以纯文本而非标准 `tool_calls` 结构返回工具调用时，NanoBot 的执行器无法解析并直接显示原始标记。随着兼容 API 服务（如 Azure 某些场景）的普及，该问题的优先级应适当提高。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent GitHub 数据生成的 2026-06-10 项目动态日报。

---

## Hermes Agent 项目动态日报 | 2026-06-10

### 1. 今日速览

过去 24 小时，Hermes Agent 社区活跃度极高，共产生 50 条 Issue 更新和 50 条 PR 更新。尽管贡献者提交了大量的修复与功能代码（待合并 PR 达 49 条），但项目方的合并/关闭速率较低（仅 1 条），呈现出“高贡献流、低闭合率”的状态，审核与合并流程存在明显瓶颈。社区讨论焦点高度集中在**桌面客户端稳定性问题**、**终端工具（PTY）与模型对齐问题**，以及**Cron 作业的可观测性与调试体验**上。

### 2. 版本发布

无。过去 24 小时内无新版本发布。

### 3. 项目进展

尽管仅合并了 1 个 PR，但社区贡献者提交了大量针对痛点的高质量修复代码，均处于待合并状态：

- **核心稳定性修复：**
    - **PR #43269**：修复了 LLM 流式连接超时（`stale_stream_kill`）后，Agent 持续在同一个 Provider 上静默重试，而不触发 Fallback 机制的问题（关联 Issue #43211）。这是对生产环境可靠性的一次重大提升。
    - **PR #43267**：修复了 `session_search` 发现模式可能将巨大的上下文摘要（50K+ 字符）重新注入回提示词中，导致 Token 暴涨的问题（关联 Issue #43175）。
- **平台与跨端适配：**
    - **PR #43253 / PR #43252**：针对 LocalEnvironment 与 Cron Scheduler，修复了 Windows 平台下进程分离（detach）逻辑的兼容性问题。
    - **PR #43260**：优化了 macOS 26 上的 `launchctl` 启动策略，优先使用旧版 `load` 命令，防止新版 `bootstrap` 导致的启动失败。
- **配置与 CLI 修复：**
    - **PR #43266**：修复了 `config.yaml` 中 `bedrock.profile` 配置项未被传递给 boto3 客户端的问题。
    - **PR #43258 / PR #43262**：修复了 `hermes update` 等 CLI 命令无法识别 `.venv` 虚拟环境目录的问题。

**小结**：24 小时内提交了大量关键修复，修复范围覆盖 Agent 运行时、后台调度、桌面端与云端配置。项目实质性进步取决于维护团队对这批积压 PR 的合并速度。

### 4. 社区热点

1. **终端工具与模型行为的对抗问题（#43245）**
   用户 `nnnarvaez` 反映，无论怎样在配置文件或技能中按照 Hermes 意图指定使用 PTY 终端工具来处理 `sudo` 命令，大多数模型仍会“创意性地”试图通过非 Hermes 预设路径获取 sudo 权限。这暴露了当前 Agent 在**工具强制绑定与模型执行安全控制**方面的深层挑战，成为今日最受关注的 Bug 讨论（评论: 3）。

2. **指令描述国际化支持（#13107）**
   Issue #13107 是目前评论数最高的（4 条），用户 `tchivs` 请求支持通过配置文件重写机器人指令描述，以解决 Telegram 等平台上指令描述无法本地化的问题。这代表了**跨国多语言用户群体的核心诉求**。

3. **桌面端生态体验集火**
   多个关于 Hermes Desktop 的 Issue 引发了讨论链，主要集中于：
   - **数据同步缺陷**：#42962 指出 Telegram 更新会话后桌面端不会自动刷新。
   - **UI/UX 缺陷**：#42992 报告多行用户消息被视觉裁剪；#42989 报告 Gateway 会话不显示上下文占用统计。
   
   这些高频反馈表明，**桌面端作为主要交互界面，其稳定性与“最后一公里”体验是阻碍用户体验提升的最大短板。**

### 5. Bug 与稳定性

- **严重（Critical）**
    - **macOS 26.5.1 启动崩溃**：[#43242](link) - 因 V8 JIT CodeRange 无法分配虚拟内存导致 Electron 应用启动直接崩溃。高度影响所有 Apple Silicon 设备用户。**无 Fix PR。**
    - **Dashboard 进程死锁**：[#43196](link) - 作为 systemd 服务持久运行时，Dashboard 在特定路径下彻底卡死，必须 SIGKILL 才能恢复。**无 Fix PR。**
    - **Stream 静默重试无故障转移**：[#43211](link) - 流式连接断开后，系统不切换 Provider 而是不断重试相同 Provider。**已有 Fix PR #43269。**

- **高（High）**
    - **Web/Chromium 工具能力丢失**：[#43099](link) - 模型突然无法调用 Chromium 进行网页截图（P2，需复现）。**无 Fix PR。**
    - **会话搜索注入巨型上下文**：[#43175](link) - 搜索返回的 Bookend 消息包含大量压缩摘要，可能导致 Token 溢出。**已有 Fix PR #43267。**
    - **辅助配置被忽略**：[#41744](link) - `auxiliary.title.enabled` 配置项完全无效，标题生成依旧运行。**无 Fix PR。**
    - **Gemini 模型视觉能力缺失**：[#42086](link) - 代码未识别 `gemini-2.5` 和 `gemini-2.0` 模型，导致视觉功能报错。**无 Fix PR。**

- **中（Medium）**
    - **WSLg 中文输入法不兼容**：[#43247](link) - Linux GUI 环境下无法调起中文输入法。
    - **看板可复活已删除看板**：[#43243](link) - 通过读/写路径可误触复活旧的空看板。

### 6. 功能请求与路线图信号

- **企业级云厂商集成**：[#29331](link) 请求接入火山引擎作为内置 Provider，结合已有的 Bedrock Profile 修复 PR（#43266），信号指向**加速服务亚太及国内企业客户**。
- **可观测性大升级**：[#43177](link) 希望在 Cron 失败通知中附带完整诊断上下文；[#43264](link) PR 增加了 SIGUSR1 信号转储线程栈的能力。这些标志着项目正从“黑盒代理”走向**生产级可调试**。
- **原生 OS 通知（UX 追赶）**：[#43255](link) PR 增加了 Agent 完成响应时发送原生 OS 通知的功能，对标 Codex 等竞品体验。
- **看板/自动化深度增强**：[#43216](link) 建议在看板中提供“内联回复与解阻”功能，减少阻塞任务处理步骤。显示出社区正在将 Hermes 作为**任务编排引擎**使用。
- **架构层面的“转轨”**：[#36765](link) RFC 提出了将“上下文路由/选择”作为 ContextEngine 的一等公民职责，而不仅限于压缩。这为未来的智能上下文管理（RAG、角色切换等）奠定了架构基础。

### 7. 用户反馈摘要

- **痛点（摩擦点）**：
    - **“模型不听话”**（#43245）：用户设计了严格的 Sudo 执行流程，但 LLM 倾向于绕过既定路径，用户认为这是“对抗性的设计缺陷”。
    - **“配置欺骗”**（#41744, #42086）：用户设置了 `enabled: false`，但功能依旧执行，导致用户对配置文件的信任度下降。
    - **“打开即死”**（#43242, #43196）：macOS 崩溃和 Dashboard 死锁是用户遇到的最激烈的负面体验，极大阻碍了日常使用。
    - **“调试黑洞”**（#43177, #43121）：Cron 定时任务失败时，仅返回通用异常信息，用户必须 SSH 登录服务器抠日志，运维成本极高。

- **积极反馈（社区力量）**：
    - 从 PR 的提交质量（#43269, #43267, #43266 等）来看，社区贡献者不满足于提出问题，而是积极提供**经过深思熟虑的专业修复方案**，展现了强大的开发者生态。
    - 用户对 `Kanban` 看板、`Cron` 定时任务等高度自动化的功能场景粘性极强，表明在“Agentic Workflow”细分赛道上，Hermes 已经成功抓住了深度用户。

### 8. 待处理积压

- **关键性审核积压**：
    - **PR #26051**（上下文压缩失败时保留历史记录）：自 5 月 15 日提交，至今已积压 26 天。该 PR 涉及 Agent 记忆机制的核心稳定性，建议维护者优先审核。
    - **Issue #43242 & #43196**：macOS 强崩与 Dashboard 死锁为影响面极广的 P0 级 Bug，目前尚无任何关联的 Fix PR，急需维护者介入响应。

- **长期未响应的重要请求**：
    - **#7507**（Matrix 群聊引用配置，P2）：自 4 月 11 日起已开放 60 天，社区仍缺乏官方设计指引。
    - **#13107**（指令描述覆盖，P3）：作为多语言部署的前置需求，自 4 月 20 日起已悬挂 50 天。
    - **#20307**（API 消息转换插件钩子，P3）：对于构建复杂插件的开发者至关重要。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-10

## 1. 今日速览

PicoClaw 项目今日处于极高活跃度状态，核心事件是社区安全研究员 @YLChen-007 系统性披露了 **15 个安全漏洞**（[#3068](https://github.com/sipeed/picoclaw/issues/3068) - [#3082](https://github.com/sipeed/picoclaw/issues/3082)），覆盖了 SSRF 绕过、授权缺陷、配置篡改等关键攻击面，给项目带来了显著的安全修复压力，同时也体现了项目日益增长的社区影响力与审计价值。与此同时，项目日常迭代节奏依旧稳定，**Agent 协作总线**（[#2937](https://github.com/sipeed/picoclaw/pull/2937)）等重大特性已合并，另有 11 个 PR 处于活跃的 Review/待合并状态。项目健康度良好，正处于从功能扩张向 **“功能建设与安全加固并重”** 的转型期。

## 2. 版本发布

昨日发布了 **Nightly Build** 版本：`v0.2.9-nightly.20260610.b9a8fad6`
- 这是一个自动构建的测试版本，可能存在不稳定性，仅供尝鲜用户谨慎使用。
- **当前无**标注为破坏性变更或需要特别迁移注意的事项。
- 完整变更日志：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展

今日项目合并了 5 个 PR，并关闭了 3 个长期存在的 Bug，整体向前迈进了扎实的一步。

**核心架构突破：**
- **[#2937](https://github.com/sipeed/picoclaw/pull/2937) (Feat/agent collaboration)** 已合并。该 PR 引入了**智能体协作总线**，为多智能体工作流、持久化信箱及权限感知通信提供了基础架构，是项目向复杂 AI Agent 平台演进的关键里程碑。

**关键 Bug 关闭：**
- **[#2796](https://github.com/sipeed/picoclaw/issues/2796) (历史记录截断)**：修复了在 Web UI 查看历史会话时，只能看到最后一条用户消息的严重体验缺陷（已关闭）。
- **[#2472](https://github.com/sipeed/picoclaw/issues/2472) (Windows 路径兼容性)**：修复了 `list_dir` 工具因系统路径分隔符导致的 `invalid argument` 崩溃（已关闭）。
- **[#2939](https://github.com/sipeed/picoclaw/issues/2939) (Claude Opus 兼容性)**：修复了 `claude-opus-4-7` 因 `temperature` 参数被弃用导致请求失败的问题（已关闭）。

**稳定性与兼容性提升：**
- **[#3064](https://github.com/sipeed/picoclaw/pull/3064) (配置迁移健壮性)**：修复了 Config Migration 中类型断言失败可能引发 Panic 的隐患。
- **[#2942](https://github.com/sipeed/picoclaw/pull/2942) (模型 ID 修正)**：修复了默认配置中 Claude 模型 ID 格式错误（使用句点而非连字符）导致首次启动失败的问题。

## 4. 社区热点

1. **大规模安全审计（[#3068](https://github.com/sipeed/picoclaw/issues/3068) 至 [#3082](https://github.com/sipeed/picoclaw/issues/3082) 系列）**：
   - 安全研究员 @YLChen-007 一次性提交 15 个高质量安全漏洞，是今日绝对焦点。分析认为，这侧面印证了 PicoClaw 在社区中的重要性已吸引专业安全研究人员的关注，同时也暴露了 Agent 框架在 SSRF、授权校验和配置管理上的信任边界挑战。**积极信号是**，维护团队在数小时内即提交了针对性的修复 PR（[#3083](https://github.com/sipeed/picoclaw/pull/3083)、[#3085](https://github.com/sipeed/picoclaw/pull/3085)），响应速度极快。

2. **Streaming 配置呼声持续（[#2404](https://github.com/sipeed/picoclaw/issues/2404)）**：
   - 该 Issue 已获得 11 条评论。用户 @OuSatoru 的诉求非常直接：像 OpenAI 客户端一样，在配置文件中加入 `”streaming“: true`。这表明用户对实时流式交互体验有强烈且未被满足的需求，属于低投入高回报的功能。

3. **Agent 协议标准化讨论（[#2984](https://github.com/sipeed/picoclaw/issues/2984)）**：
   - 用户 @Brook-sys 提出为 Pico WebSocket 客户端添加明确的 “Turn Completion Signal”。这被视为 Agent 协作总线功能（[#2937](https://github.com/sipeed/picoclaw/pull/2937)）合并后的自然延伸，社区对 Agent 状态机通信的精细化控制抱有较高期待。

## 5. Bug 与稳定性

**严重（安全漏洞 - 15 项）：**（#3068 至 #3082）
- **SSRF 绕过**：涉及通过 ISATAP IPv6（[#3074](https://github.com/sipeed/picoclaw/issues/3074)）、特殊 IPv4 网段 198.18.0.0/15（[#3077](https://github.com/sipeed/picoclaw/issues/3077)）以及环境代理（[#3078](https://github.com/sipeed/picoclaw/issues/3078)）绕过 `web_fetch` 防护。
- **授权绕过**：涉及 MQTT 主题伪造（[#3068](https://github.com/sipeed/picoclaw/issues/3068)）、反向代理 IP 信任劫持（[#3069](https://github.com/sipeed/picoclaw/issues/3069)）、企业微信免提及触发（[#3076](https://github.com/sipeed/picoclaw/issues/3076)）。
- **配置与执行安全**：涉及 Launcher 配置重载（[#3071](https://github.com/sipeed/picoclaw/issues/3071)）、CSRF密码劫持（[#3072](https://github.com/sipeed/picoclaw/issues/3072)）、Symlink 竞争提权（[#3081](https://github.com/sipeed/picoclaw/issues/3081)）。
- **状态**：**已有缓解性 PR**： [#3085](https://github.com/sipeed/picoclaw/pull/3085) 修复了 198.18.0.0/15 的 SSRF 漏判，[#3083](https://github.com/sipeed/picoclaw/pull/3083) 加强了 Launcher 访问控制。

**高（用户体验回归）：**
- [#2796](https://github.com/sipeed/picoclaw/issues/2796) （历史会话截断）**今日已关闭**，此前严重影响用户对话回溯体验。修复 PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) 当前仍处于 Open 状态等待最终审查。

**中（生产稳定性）：**
- [#2968](https://github.com/sipeed/picoclaw/issues/2968) (Context 压缩配置不生效)：PR [#2988](https://github.com/sipeed/picoclaw/pull/2988) 待合并。
- [#2958](https://github.com/sipeed/picoclaw/issues/2958) (流式会话中 `tool_calls` 被丢弃)：PR [#2987](https://github.com/sipeed/picoclaw/pull/2987) 待合并。
- [#2472](https://github.com/sipeed/picoclaw/issues/2472) (Windows 路径错误) **今日已关闭**。

**低（其他）：**
- [#3084](https://github.com/sipeed/picoclaw/pull/3084) 修复了 `.gitignore` 编码问题。
- [#3061](https://github.com/sipeed/picoclaw/pull/3061) 修复了 Windows 子进程控制台闪烁。

## 6. 功能请求与路线图信号

- **[P0][安全] 替换 libolm 为 Vodozemac** ([#3088](https://github.com/sipeed/picoclaw/issues/3088))：鉴于已弃用的 `libolm` 存在安全隐患，此替换需求在安全审计后优先级应大幅提升。
- **[P1][网关扩展] DeltaChat 集成** ([#3063](https://github.com/sipeed/picoclaw/pull/3063))：为 PicoClaw 提供了去中心化通信网关，与当前隐私优先的社区趋势高度契合。
- **[P1][提供商扩展] NEAR AI Cloud** ([#2917](https://github.com/sipeed/picoclaw/pull/2917))：增加对 TEE 能力支持的开源模型提供商，满足特定开发者群体的需求，但推进速度较慢。
- **[P2][体验增强] Config Streaming 支持** ([#2404](https://github.com/sipeed/picoclaw/issues/2404))：从社区呼声来看，这是一个被严重低估的刚需功能。建议维护者在下一轮迭代中将其纳入 Backlog。

## 7. 用户反馈摘要

- **“历史记录中，一次对话有多次用户消息，只能查看到最后一条用户消息，先前的都看不到。”**（@EverestSnow, [#2796](https://github.com/sipeed/picoclaw/issues/2796)）——该 Bug 今日已修复关闭，此前属于颠覆用户预期的严重回归问题。
- **“Calls to `claude-opus-4-7` fail with HTTP 400 because temperature is deprecated。”**（@LegendAlessandro-Liguori, [#2939](https://github.com/sipeed/picoclaw/issues/2939)）——用户期望第一时间使用最新旗舰模型，但被 API 兼容性拦路，现已修复。
- **“要像 OpenAI 客户端一样，在配置中增加 `streaming: true`。”**（@OuSatoru, [#2404](https://github.com/sipeed/picoclaw/issues/2404)）——用户对非流式交互的延迟感受明显，认为这是基础体验的一部分。
- **安全研究员 @YLChen-007 对 15 个攻击面的详尽 PoC 披露**，侧面反映了社区愿意花费大量精力对 PicoClaw 进行深度安全审计，体现了用户对项目潜力的高度认可与对安全基线的高要求。

## 8. 待处理积压

1. **[P0] 安全漏洞快速分类与修复追踪（[#3068](https://github.com/sipeed/picoclaw/issues/3068) 至 [#3082](https://github.com/sipeed/picoclaw/issues/3082)）**：
   - 尽管数量庞大，但这些是今日**新提交**的 Issue。亟需维护团队在 24-48 小时内完成 **首次分类（Triage）**，分配 CVSS 评分，并对明显高危项（如 SSRF、CSRF、授权绕过）优先分配修复任务。避免大量安全 Issue “沉底” 形成技术债务。

2. **[P1] PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) 状态不明确**：
   - 该 PR 试图修复 [#2796](https://github.com/sipeed/picoclaw/issues/2796)（历史记录），但目前 #2796 已关闭，而 #2990 仍处于 Open 状态。维护者需明确其定位：是替代性修复、增强性补丁，还是可以废弃？避免社区困惑。

3. **[P1] Streaming 功能需求长期被忽视（[#2404](https://github.com/sipeed/picoclaw/issues/2404)）**：
   - 已开放 **2 个月**，获 11 条评论，是典型的高频请求。该功能涉及配置层和 Provider 层改动，但范围可控，建议纳入明确的里程碑（Milestone ）。

4. **[P2] NEAR AI 提供商 PR 推进停滞（[#2917](https://github.com/sipeed/picoclaw/pull/2917)）**：
   - 创建于 2026-05-21，至今未取得实质性进展。建议维护者与作者沟通，决定是继续推进还是就此截止，清理长期 Open 的 PR。

5. **[P2] 多个 Stale 高价值 Bug 修复 PR 待审**：
   - [#2983](https://github.com/sipeed/picoclaw/pull/2983) (空 LLM 响应重试)、[#2987](https://github.com/sipeed/picoclaw/pull/2987) (Tool Calls 丢弃)、[#2988](https://github.com/sipeed/picoclaw/pull/2988) (Context 压缩配置) 均为修正核心流程 Bug 的关键贡献，已存在超过一周，建议集中评审合并。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，以下是根据你提供的 GitHub 数据生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-10

## 1. 今日速览

今日项目经历了罕见的“集中清仓式”活跃期，维护者对自 2 月以来积累的大量 PR 进行了大规模合并/关闭，总计 43 条 PR 发生状态更新，其中 39 条被合并或关闭。项目核心能力在今日被极大拓展，包括 WebUI 控制面板、直接运行模式、技能市场、插件系统等多个重量级功能终于落地主干。社区方面，围绕“多运行时 Agent SDK 抽象”的讨论热度最高。整体项目健康度良好，正处于从单一 Agent 框架向通用 Agent 中间件平台转型的关键阶段。

---

## 2. 版本发布

*无新版本发布*（今日侧重代码合并与积压清理，尚未产生正式 Release）。

---

## 3. 项目进展

今日合并/关闭的 PR 数量惊人，标志着项目长周期积压贡献的集中释放。以下是按模块分类的重要进展：

### 架构与核心
- **直接运行模式 (Direct Runner Mode)** [#1285](nanocoai/nanoclaw PR #1285) (CLOSED)
  - 新增 `NANOCLAW_DIRECT_RUNNER=1` 环境变量，允许在进程内直接运行 Claude Agent SDK，无需 Docker 容器，显著降低资源开销与延迟。
- **插件系统 (Plugin System)** [#1387](nanocoai/nanoclaw PR #1387) (CLOSED)
  - 实现类似于 Channel 的通用插件机制，为后续多运行时扩展提供了基础设施。
- **Agent 运行时显式模型配置** [#1192](nanocoai/nanoclaw PR #1192) (CLOSED)
  - 在代码中显式声明已使用的 Claude 模型，避免用户通过日志文件反向查找模型。

### 用户界面与可观测性
- **WebUI 控制面板** [#212](nanocoai/nanoclaw PR #212) (CLOSED)
  - 里程碑式功能。使用 Lit + Vite 构建，Fastify 提供后端服务。包含聊天、仪表盘、操作、系统四大模块共 11 个标签页。
- **Agent 链路追踪与 Web UI** [#1202](nanocoai/nanoclaw PR #1202) (CLOSED)
  - 记录每一次 Agent 调用为 Trace（包含开始/结束时间、状态、Token 消耗），并提供 `localhost:3001` 暗色模式 Dashboard。
- **Prompt 日志追踪** [#337](nanocoai/nanoclaw PR #337) (CLOSED)
  - 支持可配置的 Prompt/Response JSONL 日志记录，支持脱敏与截断。

### 生态与技能
- **技能市场/注册系统** [#1309](nanocoai/nanoclaw PR #1309) (CLOSED)
  - 实现了完整的 CLI 命令（发现、安装、管理），从 GitHub 托管的仓库中获取技能。
- **审批门控技能 (/approve, /reject)** [#1245](nanocoai/nanoclaw PR #1245) (CLOSED)
  - 扩展了只读 `/capabilities` 命令，支持变更操作的审批流。
- **Finance 数据代理技能** [#2723](nanocoai/nanoclaw PR #2723) (CLOSED)
  - 新增金融领域 Agent 技能，展示了社区在垂直领域的落地能力。
- **本地开发环境脚本 (/setup-dev)** [#1161](nanocoai/nanoclaw PR #1161) (CLOSED)
  - 简化开发者本地环境配置，降低贡献门槛。

### 文档与设计
- **技能模型自定义文档** [#2721](nanocoai/nanoclaw PR #2721) (OPEN)
  - 建立了三级分层的技能定制文档体系，包括自定义入门、技能模型和指南。
- **容器沙盒系统设计文档** [#1084](nanocoai/nanoclaw PR #1084) (CLOSED)
  - 维护了全面的容器沙盒设计参考。
- **安全审计文档** [#214](nanocoai/nanoclaw PR #214) (CLOSED)
  - 包含了 Trivy 扫描发现、SDK 凭据隔离、Apple Container 网络出站调查等结果。

---

## 4. 社区热点

**Multi-runtime Agent SDK 抽象（Issue #1690）**
- **链接**: [nanocoai/nanoclaw Issue #1690](nanocoai/nanoclaw Issue #1690)
- **状态**: OPEN | 更新: 2026-06-10 | 评论: 5 | 👍: 3
- **诉求分析**: 该 Issue 是今日讨论度最高的话题。用户明确提出了“复用现有 Channel 模式”的核心理念，期望通过 `runtime.run()` 接口将不同 Agent SDK（Claude、Codex、本地模型）作为模块化技能无缝安装。这反映出社区对**模型无关性**和**供应商中立**的强烈追求。今日合并的插件系统 (#1387) 和直接运行模式 (#1285) 被社区视为对这一方向的有力铺垫。

---

## 5. Bug 与稳定性

| 严重程度 | 内容 | PR/Issue | 状态 |
|----------|------|----------|------|
| **高危** | **Telegram 配对码使用弱随机数 `Math.random`**，攻击者可能通过观察输出预测配对码并抢占管理权限 | [#2722](nanocoai/nanoclaw PR #2722) | **待合并**（改用 `crypto.randomInt`） |
| **高** | **飞书互动卡片清理缺陷**：Agent Runner 被 `PROCESS_TIMEOUT` 杀死后，`deleteActiveCard` 未触发，卡片永久显示“运行中” | [#2718](nanocoai/nanoclaw PR #2718) | **已修复/已合并** |
| **低** | **构建时缺乏版本元数据**：生产环境中难以快速定位运行版本和构建来源 | [#1333](nanocoai/nanoclaw PR #1333) | **已修复/已合并** |

---

## 6. 功能请求与路线图信号

### 极高优先级信号
- **Multi-runtime 支持 (#1690)**: 虽然今日无直接对应 PR 合并，但插件系统 (#1387) 的落地为其扫清了架构障碍。该功能极大概率成为下一阶段（v1.x -> v2.0）的核心开发目标。

### 路线图观察
- **平台化转型**: 从 WebUI (#212)、技能市场 (#1309)、直接运行模式 (#1285) 的同时落地可以看出，项目正在补全作为“平台”的三大要素：界面、生态、部署灵活性。
- **安全左移**: 安全审计文档 (#214) 的合并以及 Telegram 安全修复 (#2722) 的出现，表明社区和贡献者正在主动推动安全性建设。
- **文档与开发者体验 (DX)**: 大量 JSDoc、CLAUDE.md 规范、Setup Dev 脚本被合并，项目正在积极降低新贡献者的参与门槛。

---

## 7. 用户反馈摘要

- **对现有 Channel 模式的认可与扩展期望**
  - 用户表示已基于 NanoClaw 构建了多运行时抽象层，并明确强调“镜像现有的 Channel 模式”（`/add-telegram`, `/add-slack`）。这说明当前的 Channel 架构在用户心中非常成功，用户希望将其哲学推广到 Agent 运行时层面（#1690）。
- **对 Docker 环境的抱怨**
  - 直接运行模式 (#1285) 的 PR 明确指出“Docker 容器增加了显著的资源开销和延迟”。这代表了轻量级部署与开发场景下的普遍痛点。
- **对技能分享生态的期待**
  - 技能市场 (#1309) 的合并表明社区不仅希望“用技能”，更希望“发布和发现技能”。生态建设将是下一步用户活跃度的关键。

---

## 8. 待处理积压

以下为当前需要维护者重点关注的项目：

| 项目 | 类型 | 链接 | 建议行动 |
|------|------|------|----------|
| **Multi-runtime Agent SDK 抽象** | 核心功能/讨论 | [Issue #1690](nanocoai/nanoclaw Issue #1690) | 建议维护者发布**官方路线图或初步设计回应**，该 Issue 代表了项目最大的社区共识与未来方向 |
| **Telegram 配对码安全修复** | 安全修复 PR | [PR #2722](nanocoai/nanoclaw PR #2722) | 安全相关问题延迟越久风险越高，建议尽快安排 Code Review 并合并 |
| **技能模型自定义文档** | 文档 PR | [PR #2721](nanocoai/nanoclaw PR #2721) | 直接影响新用户理解“如何自定义”，建议尽快审查并入 |
| **长期积压容器技能** | 遗留 PR | 多个来自 2-3 月的社区技能 PR | 今日已清理大量历史积压，但仍需检查是否还有残留的 Pending Closure 项未被处理 |

---
*报告生成时间：2026-06-10 | 数据源：nanocoai/nanoclaw*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-06-10

## 今日速览

过去 24 小时项目保持高活跃度：共处理 **5 个 Issues**（1 个新开 / 活跃，4 个关闭），合并 / 关闭 **7 个 PR**，并新增 **1 个待审查的 PR**。大量社区贡献的修复被合并，覆盖 PII 误报、Telegram 交互缺陷、自定义 provider 回落、死配置 flag 等关键问题。同时长期开发的跨实例内存同步功能（#711）也于此期间正式关闭，标志着该特性已就绪。唯一遗留的开放 Issue #941（Agent 定时任务无法启动子进程）尚未分配修复，是需要关注的稳定性隐患。

## 项目进展

今日合并 / 关闭的 PR 在功能完善与缺陷修复上均有显著推进：

- **跨实例内存同步**（#711）关闭：为 NullClaw 增加了确定性内存事件流，使多个 Agent 实例间可以同步记忆，是实现偏好共享、上下文跟随等高级场景的基础设施。该 PR 虽在 3 月提出，经过长时间迭代后于今日合并，标志着项目在分布式 Agent 协同方向迈出一大步。
- **自定义 OpenAI-compatible 提供商**修复（#940，关闭 #936）：解决了通过 `/models` 菜单选择自定义 provider 时错误硬编码 Anthropic 模型列表的问题。现在系统会正确查询 provider 的 `/v1/models` 端点，确保模型列表真实可用。
- **Telegram 输入指示器**修复（#943，关闭 #942）：按下 inline 按钮后不再静默处理，现在会显示“typing…”指示器，提升交互反馈体验。
- **PII 误报修复**（#945，关闭 #944）：日期时间输出中的数字序列不再被错误替换为 `[PHONE_X]`，确保 Agent 执行 `date` 等命令时输出真实性。
- **`compact_context` 标志生效**（#939，关闭 #937）：此前该配置项虽被解析但运行时始终压缩上下文，现在 `autoCompactHistory()` 会读取该标志，允许用户控制上下文压缩行为。
- **工具过滤功能**（#946）：新增 `filterToolsForPromptText`，在文本系统提示中仅包含 `always` 分组的内置 / MCP 工具，动态分组工具不出现但保留于原生 API tool-calling 中，减少了提示噪音。
- **新增 Evolink 提供商**（#947）：Evolink 作为多模型网关被集成，用户可直接选择 GPT‑5、Gemini、DeepSeek 等模型，进一步扩展了可用模型生态。

另外还有一个已合并的较早 PR #711（feat/cross memory）虽未在 24 小时内创建，但更新于 2026-06-09，今日被正式关闭，因此一并计入进展。

## 社区热点

今日大部分 PR 和 Issue 评论量不大，但以下条目因涉及核心功能或仍处于开放状态而受到社区关注：

- **#941** [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens  
  这是唯一仍开放的 Issue，描述了定时任务中 `job_type: "agent"` 无法实际启动子进程的严重问题。用户期望任务执行后通过 Telegram 收到结果，但任务状态标记为完成却没有任何实际动作。虽然评论仅 1 条，但该问题的存在可能影响依赖定时触发功能的用户。  
  [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)

- **#948** [OPEN] fix cron agent delivery attribution  
  该 PR 今日刚提出，试图为 cron agent 子进程传递正确的交付来源元数据，以确保消息被正确路由到原定的 Telegram 账号。该 PR 可能与 #941 关联（若无子进程则交付自然无法发生），但目前并未标记绑定关系。社区期待审查结果。  
  [PR #948](https://github.com/nullclaw/nullclaw/pull/948)

## Bug 与稳定性

### 严重

- **#941** Agent 定时任务不启动子进程（Telegram 交付永远不发生）  
  `schedule` 设置 `job_type: "agent"` 后，任务被标记完成但 agent 子进程从未启动。目前 **无 fix PR** 指向该问题。  
  [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)

### 已修复

以下 Bug 均已通过关联 PR 于今日关闭：

- **#936** 自定义 OpenAI-compatible provider 回退到硬编码 Claude 模型 → 由 #940 修复  
- **#944** PII 过滤器将日期时间误识别为电话号码 → 由 #945 修复  
- **#942** Telegram inline 按钮无打字指示器 → 由 #943 修复  
- **#937** `compact_context` 标志存在但不生效 → 由 #939 修复

这些修复覆盖了模型选择、输出可靠性、交互反馈和配置一致性，整体上项目稳定性有显著提升。

## 功能请求与路线图信号

今日没有新开的功能请求 Issue，但从合并的 PR 可以判断出社区贡献与维护者接受的方向：

- **第三方 Provider 生态扩展**：继 #940 修复自定义 provider 后，今日合并的 #947 直接集成 Evolink 作为一等适配提供商。这暗示项目将持续接受经过验证的第三方 API 网关作为内置选项，降低用户配置门槛。
- **多 Agent 记忆同步**：#711 的合入表明项目路线图包含跨实例记忆共享，为未来 Agent 协作、长期记忆桥接提供基础。
- **更精细的提示工程**：#946 对工具列表按过滤器分组，说明开发者在平衡提示长度与动态工具调用能力之间继续优化。

## 用户反馈摘要

从今日关闭的 Issue 描述与 PR 讨论中可提炼出近期用户集中遇到的主要痛点：

- **定制化提供商配置无效**：自定义 OpenAI 兼容 provider 后在交互菜单中无法正确列出模型，使用户不得不退回固定模型（#936）。此问题已解决。
- **输出内容被异常替换**：开启 PII 过滤后，系统产生的日期时间输出（如 `2026-06-02 20:17`）被误判为电话号码，影响 Agent 任务的正常运行。用户不得不关闭过滤或接受错误输出（#944）。已修复。
- **交互反馈缺失**：Telegram 内 inline 按钮操作缺乏“typing…”状态，用户难以判断请求是否开始处理，尤其在模型响应较慢时（#942）。已修复。
- **配置项形同虚设**：`compact_context` 在配置文件中存在，但运行时始终执行压缩，让用户产生“已禁用压缩”的错觉（#937）。已修复。

整体而言，近期修复针对的都是直接影响日常体验的“隐形 bug”，用户满意度有望在更新后回升。

## 待处理积压

- **Issue #941（Agent 定时任务不启动子进程）** 自 2026-05-31 创建至今仍为 Open 状态，未分配标签或负责人。考虑到该问题可能导致定时通知类功能完全不可用，且已有部分用户复现，建议维护者尽快确认是否需要与 PR #948（cron delivery attribution）联动修复。  
  [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)

- **PR #948（fix cron agent delivery attribution）** 今日刚创建，仍等待审查。如果它能够通过测试并与 #941 的问题域对齐，或许可以一并解决定时任务不生效的根源。  
  [PR #948](https://github.com/nullclaw/nullclaw/pull/948)

以上两个条目是目前项目中唯一遗留的开放工作项，建议优先关注并推动审查。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-06-10

## 1. 今日速览

IronClaw 项目今日保持高活跃度。过去 24 小时内，共产生 **45 条 Issue 更新**（其中 40 条为新开或活跃，5 条已关闭）以及 **50 条 Pull Request 更新**（其中 48 条待合并，2 条已合并/关闭）。开发重心集中在 **Reborn 平台的生产就绪**、**WebUI v2 测试覆盖**、**通用附件处理流水线** 以及 **持久化审批策略** 等方向。尽管当日无新版本发布，大量功能特性与重构 PR 正在密集流转，显示出项目正从架构重构阶段迈向功能完善与稳定化阶段。

## 3. 项目进展

今日有 **5 个 Issue** 被关闭，标志着多个关键模块的阶段性完成：

- **Reborn WebUI v2 全栈 E2E 测试** ([#4604](https://github.com/nearai/ironclaw/issues/4604)) 已关闭，补全了浏览器驱动的端到端覆盖空白。
- **WebChat v2 认证审计** ([#4609](https://github.com/nearai/ironclaw/issues/4609)) 完成，验证了 Bearer、DB/OIDC、query-token 等多种认证途径在 v2 上的等效性。
- **操作员控制平面基础** ([#4591](https://github.com/nearai/ironclaw/issues/4591)) 关闭，为 Reborn 的 setup/config/diagnostics 等管理 API 建立了 facade 和路由骨架。
- **OpenAI 兼容 API 迁移** ([#4447](https://github.com/nearai/ironclaw/issues/4447)) 与 **流适配** ([#4446](https://github.com/nearai/ironclaw/issues/4446)) 同时关闭，意味着 Reborn 的 OpenAI 兼容层（Chat、Responses、SSE 流）已达成必经的兼容性与安全测试关。

此外，PR 列表中有 **2 个 PR 被合并/关闭**（未在前 20 活跃列中展示，推测为较小修复），整体项目正在快速推进。

## 4. 社区热点

昨日讨论最集中的 Issue 是 **Epic: Reborn production cutover readiness** ([#3026](https://github.com/nearai/ironclaw/issues/3026))，共 3 条评论，作为 `P0` 层级的工作，它定义了生产图（production graph）的构建、校验、报告和流量阻止逻辑，是项目目前最重要的一张蓝图。社区关注点集中在如何安全、零信任地推出 Reborn 生产环境。

其他获得 1 条评论的 Issue 也反映出社区的关切：
- **Strict-mode 提供者 null 值拒绝** ([#4642](https://github.com/nearai/ironclaw/issues/4642)) – 影响大多数第一方工具的调用。
- **安全加固** ([#88](https://github.com/nearai/ironclaw/issues/88)) – 长期存在的安全特性跟踪。
- **PostgreSQL 存储配置** ([#4551](https://github.com/nearai/ironclaw/issues/4551)) – 生产依赖。
- **DeepSeek 重复 model 字段** ([#4548](https://github.com/nearai/ironclaw/issues/4548)) – 第三方 API 兼容性 bug。

分析认为，社区对 **生产就绪、LLM 供给商互操作性、安全特性** 三方面的诉求最为强烈。

## 5. Bug 与稳定性

以下为今日报告的 Bug，按严重程度排列：

| 严重程度 | Issue | 描述 | Fix PR |
|----------|-------|------|--------|
| 🔴 高 | [#4642](https://github.com/nearai/ironclaw/issues/4642) | **Strict-mode LLM 提供者发送 `null` 作为未设可选参数，被 capability-port 验证拒绝**，导致大多数第一方工具调用失败。 | 未发现对应 PR |
| 🔴 高 | [#4548](https://github.com/nearai/ironclaw/issues/4548) | **Chat Completion 请求在包含 tools 时序列化出重复的顶层 `model` 字段**，DeepSeek 返回 HTTP 400。 | 未发现对应 PR |
| 🟡 中 | [#4640](https://github.com/nearai/ironclaw/issues/4640) | **google-calendar `list_events` 缺少时间下限和排序参数**，导致返回最旧事件且重复会议显示为重复主事件。 | 未发现对应 PR |
| 🟡 中 | [#4673](https://github.com/nearai/ironclaw/issues/4673) | **NEAR AI 提供者配置测试连接成功后无法保存**，点击 Save 后配置不持久化，回到欢迎页仍显示需要设置。 | 未发现对应 PR |

建议优先处理 #4642 与 #4548，这两者直接影响主流模型集成和工具使用稳定性。

## 6. 功能请求与路线图信号

从新开的 Issue 和活跃 PR 中可以清晰看到未来几个版本的功能重心：

- **附件全链路支持** ([#4644](https://github.com/nearai/ironclaw/issues/4644))：包含格式注册表 ([#4654](https://github.com/nearai/ironclaw/pull/4654))、transcript 引用 ([#4655](https://github.com/nearai/ironclaw/pull/4655))、字节落地 ([#4668](https://github.com/nearai/ironclaw/pull/4668))、上传接入 ([#4672](https://github.com/nearai/ironclaw/pull/4672)) 等多阶段 PR，预计在 Reborn 中首次实现附件持久化和模型可见。
- **持久化审批策略** ([#4613](https://github.com/nearai/ironclaw/pull/4613))：为 Reborn 提供 scoped allow/lookup/revoke 能力，并注入 AlwaysAllow 模式，为后续产品化控制铺路。
- **项目级自动化所有权** ([#4663](https://github.com/nearai/ironclaw/pull/4663), [#4664](https://github.com/nearai/ironclaw/pull/4664))：将 communication preferences 和 automations 从个人作用域扩展到项目作用域。
- **可观测性 seams** ([#4588](https://github.com/nearai/ironclaw/pull/4588), [#4671](https://github.com/nearai/ironclaw/pull/4671))：trajectory observer 和 extra-capabilities port 让外部宿主可以驱动和观察 agent 运行，对 benchmark 和集成测试很有价值。
- **NEAR 主网只读扩展** ([#4661](https://github.com/nearai/ironclaw/pull/4661))：提供 6 个只读能力（账户、余额、交易状态等），预示跨链数据访问将成为第一方能力。
- **统一搜索** ([#4647](https://github.com/nearai/ironclaw/issues/4647))、**Slack 频道路由** ([#4625](https://github.com/nearai/ironclaw/issues/4625))、**管理员共享工具** ([#4628](https://github.com/nearai/ironclaw/issues/4628)) 等增强需求也已被标记为 `suggested_P1`，很可能进入下一迭代。

以上功能信号表明项目路线图正在快速从基础设施转向用户体验和可扩展性。

## 7. 用户反馈摘要

从 Issues 描述中提炼出现实用户遇到的痛点与诉求：

- **DeepSeek API 兼容性** (#4548)：用户报告请求重复 `model` 字段导致 400 错误，拦截了通过 `deepseek` provider 的正常使用，暴露出与部分第三方模型的序列化兼容缺陷。
- **Strict-mode 提供者工具调用失败** (#4642)：用户在严格模式下使用最常见的第一方工具时遭遇验证拒绝，降低了 agent 工具使用的可靠性。
- **Google 日历事件排序异常** (#4640)：“what are my upcoming meetings?” 返回最旧的事件，与用户预期严重不符，影响日程类工作流。
- **NEAR AI 提供者配置无法保存** (#4673)：用户完成 OAuth 测试连接后，点击 Save 无反馈且不持久化，配置流程中断在最后一步，降低首次使用体验。
- **附件在 Reborn 中被静默丢弃** (#4644 背景)：用户通过频道上传的附件在 Reborn transcript 中丢失，说明当前通道与平台间存在数据鸿沟。

这些反馈集中于 **第三方集成稳定性** 与 **配置持久化**，是提升用户信任的关键优化点。

## 8. 待处理积压

以下 Issue 长期未关闭或活跃周期较长，需维护者保持关注：

| Issue | 创建时间 | 现状 | 说明 |
|-------|----------|------|------|
| [#3026](https://github.com/nearai/ironclaw/issues/3026) | 2026-04-28 | 开放中，最后更新 06-09 | **Reborn 生产 cutover 前最后几片**（#4620, #4621 为子任务）需要尽快收尾，目前仍有 5 个子 issue 在开放中。 |
| [#88](https://github.com/nearai/ironclaw/issues/88) | 2026-02-14 | 开放中，最后更新 06-09 | **安全加固** 已存在近 4 个月，覆盖配对、提权、媒体 URL 验证等，需评估是否纳入近期迭代。 |
| [#4666](https://github.com/nearai/ironclaw/issues/4666) | 2026-06-10 | 开放中（新开） | `slack_host_state.rs` 接近 2,823 行（超 1,500 门槛），需要拆分。 |
| [#4665](https://github.com/nearai/ironclaw/issues/4665) | 2026-06-10 | 开放中（新开） | `slack_host_beta.rs` 超 3,359 行，需分解。两个文件规范 issue 虽新开，但架构规则已明确，应尽早分配重构。 |

此外，PR 中 **#4521** (JSON cleaner by new contributor) 等待审核，**#4550** (full SHA branch creation) 和 **#4561, #4562** (SecurityAuditSink 记录) 等待合并，建议维护者加快 Review 节奏，降低待合并 PR 积压（当前 48 个）。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是为您生成的 LobsterAI 项目动态日报（2026-06-10）。

---

# LobsterAI 项目动态日报 — 2026年6月10日

**项目名称:** LobsterAI (github.com/netease-youdao/LobsterAI)

## 1. 今日速览

今日项目整体活跃度中等偏上，主要体现在 Pull Request 的密集处理上。**PR 合并/关闭数量显著（3个）**，显示了核心功能开发与修复正在快速推进。社区讨论集中于 **#2132** 这一核心架构议题——跨模型子任务协作，开发者提出了兼具深度与实践性的优化建议。尽管 Issue 数量不多，但 PR 活动频繁，表明项目当前处于 **“功能收敛与修复并行”** 的积极阶段，距离下一个稳定版本可能已不远。

## 2. 版本发布
*(今日无新版本发布)*

## 3. 项目进展

今日有 **3 个 PR** 被合并或关闭，标志着项目在功能和稳定性上取得了重要进展。

- **[#2136 - [CLOSED] feature: data backup and migration](https://github.com/netease-youdao/LobsterAI/pull/2136)**: 由 `fisherdaddy` 提交的**数据备份与迁移**功能。这通常是一个项目走向成熟和可靠性提升的关键步骤，为后续功能迭代提供了安全垫。
- **[#2134 - [CLOSED] Liuzhq/task complete notice](https://github.com/netease-youdao/LobsterAI/pull/2134)**: 由 `liuzhq1986` 提交，重点在于优化用户体验。该PR实现了：
    - **主窗口被关闭/销毁后，通过任务完成通知恢复应用**。
    - **等待渲染器通知处理程序就绪后**，再打开目标协作会话，提升了异步操作的稳定性。
    - **保持系统通知引用**，确保macOS通知中心点击功能可用。这是一个重要的可用性改进。
- **[#2135 - [CLOSED] chore: temporary close databackup](https://github.com/netease-youdao/LobsterAI/pull/2135)**: 同样是 `fisherdaddy` 提交，临时关闭了数据备份功能。这可能是因为在集成 `#2136` 的大功能时需要临时禁用以进行测试或调整，属正常开发流程。

**总结：** 今日合并的PR覆盖了**数据持久化、系统通知交互**等关键领域，显著提升了项目的健壮性和用户体验。

## 4. 社区热点

今日唯一的 Issue **#2132** 成为了社区讨论的焦点，虽然评论数为0，但其内容深刻，代表了高级用户对项目架构的深度思考。

- **[#2132 [OPEN] 跨模型子任务调用的问题](https://github.com/netease-youdao/LobsterAI/issues/2132)**
    - **诉求分析**：用户 `woxinsj` 提出了一个极具价值的设计构想：**M3模型作为主任务负责规划与验收，DeepSeek作为子任务负责快速执行**的跨模型协作机制。用户并非简单报告Bug，而是主动进行了根因分析（定位到 `call_function_gblu0nmqpcej_1` 是网管级函数调用而非子任务），并给出了具体的优化方案：
        1.  借鉴**同模型子任务完成时，主任务能第一时间知晓**的机制。
        2.  子任务完成或卡住时，应能**主动通知主任务**。
    - **热度分析**：尽管数据上无评论，但该Issue触及项目核心的**任务调度与多模型协作架构**，设计清晰合理，很可能吸引核心开发者的关注。这是社区从“使用者”向“贡献者/设计者”转变的信号。

## 5. Bug 与稳定性

- **[重要] 跨模型子任务调用逻辑缺陷 (#2132)**
    - **问题描述**：用户 `woxinsj` 报告了主任务无法感知跨模型子任务状态的Bug。根本原因是系统将跨模型调用识别为“网关级函数调用”，而非“子任务”，导致主任务无法获知其完成状态。
    - **严重程度**：**高**。该问题直接影响了多模型协作流程的完整性和可靠性，特别是涉及“验收监督汇报”等需要等待子任务结果的场景。
    - **修复状态**：当前 Issue 为 OPEN 状态，**尚未有对应的修复PR**，但社区用户已自行提出修复思路。

- **[中] 数据备份功能临时关闭 (#2135)**
    - **问题描述**：为推进 `#2136` 的数据备份新功能，旧的数据备份代码被临时关闭。
    - **严重程度**：**中**。这是正常的主动调整，不影响主干功能，但可能短时间内容器回滚功能受限。
    - **修复状态**：**已关闭**（临时关闭），预期新的备份功能上线后将被替代。

## 6. 功能请求与路线图信号

- **热门功能请求：跨模型子任务协作机制 (#2132)**
    - **信号强度**：**强**。社区用户不仅提出了需求，还提供了详细的技术分析和设计建议（子任务状态同步、主动通知等）。这与项目“AI智能体协作”的核心定位高度契合。
    - **纳入下版本可能性**：**高**。该请求直击当前架构痛点，结合同日合并的 `#2134`（优化任务完成通知）来看，项目团队很可能正在系统性地优化**任务状态管理和通知链路**。此功能很有可能被纳入后续版本的核心路线图。

## 7. 用户反馈摘要

- **痛点**：用户在跨模型工作流中遇到阻塞，主任务（M3）无法感知子任务（DeepSeek）的执行结果。这表明**异构模型之间的协作粒度目前仅限于函数级别，缺乏会话级别的任务管理与状态同步**，给高级用户带来了困扰。
- **需求**：用户明确需要**子任务状态反馈机制**，并希望这种机制能主动通知主任务，而非被动等待轮询。
- **使用场景**：报告显示用户在实际使用 **M3规划 + DeepSeek执行** 的混合模型Agent工作流时遇到该问题，这是一个真实且典型的复合AI应用场景。
- **评价**：用户对项目机制有较深理解，能够进行根因定位并提出建设性方案，是高质量的社区反馈。

## 8. 待处理积压

目前项目无积压的长期未响应 Issue 或 PR。新开的 Issue `#2132` 虽然内容具有战略重要性，但尚属新近提交，应立即由维护者进行响应和讨论，以确保社区贡献的方向正确。`#2133` 为待合并的Bug修复PR，积压风险较低，但仍需关注审核进度。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，以下是基于 Moltis 项目 2026-06-10 数据生成的日报。

---

# Moltis 项目动态日报 | 2026-06-10

### 1. 今日速览
Moltis 项目今日活跃度极低，处于典型的“维护宁静期”。过去24小时内无版本发布、无 Pull Request 合并或关闭。项目唯一的新增事件是用户 `vvuk` 提交的一条关于 TTS 提供者配置的 Bug 报告。整体来看，项目核心代码库稳定，但开发者运维与社区参与度在今日明显放缓，维护团队需留意是否迎来长周期的低活跃阶段。

### 2. 版本发布
今日无新版本发布。无迁移指南或破坏性变更需关注。

### 3. 项目进展
今日项目推进速度为零。**无 Pull Request 被合并或关闭**，意味着没有新功能被集成，也没有已知 Bug 的代码级修复被引入主分支。

### 4. 社区热点
- **[Bug] provider 'coqui' not configured (#1114)**
   - 作者: `vvuk`
   - 链接: https://github.com/moltis-org/moltis/issues/1114
   - **热度分析**: 尽管该 Issue 暂无评论和反应，但作为当日唯一活跃的社区交互，它集中代表了用户当前的主要诉求。用户报告在连接 Coqui 语音提供者时出现未配置错误。这暴露了用户在尝试使用第三方 TTS 模块时遇到的配置门槛。

### 5. Bug 与稳定性
- **严重程度: Minor (配置/功能受阻)**
   - **Issue #1114**: `provider 'coqui' not configured`
   - **状态**: Open（待路由）
   - **影响范围**: 仅影响使用 `coqui` 作为 TTS 后端提供者的用户，不影响核心对话或 LLM 调用逻辑。
   - **根因推测**: 可能为环境变量缺失、配置文件未正确指向、或 `coqui` 依赖包未正确安装导致。
   - **修复 PR**: 无
   - **链接**: https://github.com/moltis-org/moltis/issues/1114

### 6. 功能请求与路线图信号
今日无明确的功能请求提交（`feature request` 标签缺失）。

**路线图信号分析**：Issue #1114 揭示了用户在**语音模块的配置易用性**上存在摩擦。这暗示项目可能需要改进两个方向：
1. **文档侧**：补充一份具体的 `coqui` Provider 配置指南与环境依赖清单。
2. **代码侧**：在启动检查时提供更友好的错误提示（告诉用户是环境变量没设，还是 Python 包没装），甚至内置一个 `config-check` 诊断工具。

### 7. 用户反馈摘要
**来源**: 用户 `vvuk`
- **使用场景**: 正在尝试启用 Moltis 的 Coqui TTS 语音合成模块。
- **痛点**: 遇到“未配置”报错，导致功能不可用。用户反馈质量较高，提交前已按项目要求排查过旧 Issue 并确认使用最新版本，说明该 Bug 具有一定隐蔽性或复现门槛。
- **诉求**: 希望得到项目组的配置指引或 Bug 修复，以成功启用语音功能。

### 8. 待处理积压
- **新晋待处理项（需维护者立即关注）**：
   - **[Bug] provider 'coqui' not configured (#1114)**
      - https://github.com/moltis-org/moltis/issues/1114
      - **建议动作**: 维护团队应尽快为该 Issue 打上标签（如 `bug`、`area: TTS`、`needs-triage`），并进行初步回复，引导用户提供调试日志和配置文件样本，避免该 Issue 因长期无人回应而变为“僵尸 Issue”，影响项目对新用户的响应形象。
- **长期积压**: 今日无长期未响应的超级历史积压 Issue 或 PR。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

**CoPaw（QwenPaw）项目动态日报｜2026-06-10**

---

## 1. 今日速览

过去 24 小时项目保持**高活跃度**：共产生 42 条 Issue 更新（新开 23 条）与 38 条 PR 更新（合并/关闭 18 条）。新版本 **1.1.11-beta.2** 发布，主要增强浏览器控制能力并修复跨浏览器隔离问题。社区讨论集中在功能借鉴（Hermes Agent 学习循环）、后端架构升级（AgentScope 2.0 迁移）以及多个稳定性痛点（前端卡顿、微信推送失败）。修复类 PR 集中在 MCP 进程泄漏、JSON 损坏容错、空列表守卫等方向，整体项目推进以 **“稳定性加固 + 插件生态扩展”** 为基调。

---

## 2. 版本发布

### v1.1.11-beta.2
- **发布说明**（摘录）：
  - `feat(browser): add page coordinate click support to browser_control` – 支持页面坐标点击，提升浏览器控制精度。
  - `fix(browser): add CDP timeout param and browser profile isolation for cross-browser switching` – 增加 CDP 超时参数，实现跨浏览器切换时的 profile 隔离，修复潜在的状态污染。
- **破坏性变更**：无明确标记，通常为向前兼容。
- **迁移注意事项**：若使用旧版浏览器控制功能，建议更新后重新测试 MCP/浏览器插件行为；CDP 超时参数可能需要按环境调整。

---

## 3. 项目进展（合并/关闭的重点 PR）

以下 PR 已在 24 小时内合并或关闭，是项目实质推进的标志：

| PR 编号 | 标签 | 标题 | 影响 |
|--------|------|------|------|
| [#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014) | `fix` | fix(mcp): prevent subprocess accumulation across restarts | **关键修复**：解决 Docker 重启后 MCP 子进程不断堆积导致前端加载变慢的问题。 |
| [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) | `feat` | feat(skill): Add skill tag batch download | 实现技能按标签批量下载到工作区，**完成 Issue #2961**（技能分类功能需求）。 |
| [#5033](https://github.com/agentscope-ai/QwenPaw/pull/5033) | `feat` | feat(plugin/cloudpaw): support importing agents from AgentHub and enhance A2A capabilities | 重构 A2A 路由，支持从 AgentHub 导入 agent，增强智能体间通信能力。 |
| [#5062](https://github.com/agentscope-ai/QwenPaw/pull/5062) | `fix` | fix(e2e): handle text-based empty state in token usage test | 修复 E2E 测试在无 token 数据时对空状态的处理方式。 |
| [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) | `feat` | feat(skill): Add skill tag batch download | **社区贡献**：使技能池支持按标签过滤批量下载，满足用户文件夹式管理需求。 |

**总结**：MCP 稳定性得到显著提升；技能生态迈入分类管理阶段；AgentHub 导入与 A2A 增强为未来多 agent 协作铺路。

---

## 4. 社区热点（高评论 / 高互动 Issue & PR）

| 编号 | 标题 | 评论 | 👍 | 核心诉求 |
|------|------|------|----|----------|
| [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017)（已关闭） | 【建议】学习 Hermes Agent“学习循环”特性 | 10 | 3 | 用户建议借鉴 Hermes Agent 的**自动技能创建与迭代**机制，增强 QwenPaw 的自适应能力。 |
| [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666)（已关闭） | 新建会话后 Models 配置页面丢失且无法加载 | 7 | 0 | **严重配置 bug**：会话切换时丢失模型配置，需重启恢复。虽已关闭，但影响面大。 |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)（开放） | 【Breaking Change】后端从 AgentScope 1.x 迁移至 2.0 | 7 | 2 | 技术架构迁移计划，涉及 API 和运行时模型变更，社区高度关注。 |
| [#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)（已关闭） | 定时任务推送到微信失败 | 6 | 0 | 微信渠道 `to_handle_from_target` 返回 session_id 而非 user_id 导致投递失败。 |
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937)（已关闭） | `/compact` 命令忽略模型 `max_input_length` | 5 | 0 | 上下文压缩阈值未按模型实际限制推导，仍套用默认 128K。 |

**分析**：  
- 用户对“学习能力”的期待强烈，开放讨论反映了社区希望项目从“工具型”向“自适应 Agent”演进。  
- 配置持久化和渠道集成（微信）的 bug 是用户高频痛点，虽已修复但暴露了核心模块的边界情况。  
- AgentScope 2.0 迁移是决定项目技术走向的**关键路线图事件**，贡献者和核心用户均密切关注。

---

## 5. Bug 与稳定性

按严重程度排列，并标注是否存在修复 PR。

| 严重程度 | Issue | 标题 | 状态 | Fix PR |
|---------|-------|------|------|--------|
| **严重** | [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 新建会话后 Models 配置丢失 | 已关闭 | 未明确对应 PR（可能随版本修复） |
| **严重** | [#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878) | 微信定时任务推送失败 | 已关闭 | 疑似随版本修复；类似问题[#5060](https://github.com/agentscope-ai/QwenPaw/pull/5060) 提出相同根因 |
| **高** | [#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834) | MCP 进程积累导致前端加载慢 | 已关闭 | ✅ [#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014) |
| **高** | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | 本地千问 3.6-27B 对话无响应 | **开放** | 暂未修复 |
| **高** | [#5052](https://github.com/agentscope-ai/QwenPaw/issues/5052) | 工具调用若干次后全部报 `got an unexpected keyword argument 'arguments'` | **开放** | 暂未修复 |
| **中** | [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | Agent 生成的定时任务无法触发/编辑 | **开放** | 暂未修复 |
| **中** | [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) | 技能斜杠调用后显示为展开的 SKILL.md 内容 | **开放** | 暂未修复 |
| **中** | [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) | DeepSeek 拒绝 PAT 工具名含点号 | 已关闭（invalid） | 用户标记为模型限制，非项目 bug |
| **低** | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | 图片预览放大后拖动抖动 | **开放** | 暂未修复 |
| **低** | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | `/compact` 忽略 `max_input_length` | 已关闭 | 可能已修复 |

此外，多个**开放 Bug** 集中在**前端性能**（#5015 加载不流畅、#4917 聊天切换卡顿）和**桌面端启动慢**（#5047），表明 Tauri 版本在资源消耗和首屏体验上有优化空间。

---

## 6. 功能请求与路线图信号

| Issue / PR | 提案 | 讨论热度 | 对应 PR / 状态 | 版本纳入可能 |
|-----------|------|---------|---------------|-------------|
| [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) | 引入 Hermes Agent 风格“学习循环” | 🔥 | 无 | 可能纳入 v1.2 路线图 |
| [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) | 独立的视觉模型 fallback 配置 | 👍 1 | 无 | 社区呼声高，较容易实现 |
| [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994) | 记忆系统自进化（分层记忆） | 👍 1 | 无 | 与学习循环强相关，可能合并规划 |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | 会话栏直接切换（无需点击两次） | 评论 3 | 无 | 前端体验改进，低风险 |
| [#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751) | Windows 系统托盘图标 | 评论 3 | [PR #4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)（Tauri 更新器，相关但非直接） | 可能随 Tauri 原生功能推出 |
| [#2961](https://github.com/agentscope-ai/QwenPaw/issues/2961) | 技能分类（文件夹） | 已完成 | ✅ [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) | **已纳入 v1.1.11** |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | 后端迁移至 AgentScope 2.0 | 里程碑级 | 讨论中，等待具体 PR | **大概率 v1.2 核心变化** |

**路线图信号**：  
- “学习循环”与“记忆进化”被明确视作下一代 Agent 能力，若项目采纳，将带来架构级重构。  
- 视觉模型独立配置是社区高频诉求（典型场景：主模型纯文本，但需偶尔处理图片）。  
- 后端向 AgentScope 2.0 迁移是技术债清理的关键一步，但可能带来 Breaking Changes，需要做好兼容测试。

---

## 7. 用户反馈摘要

从 Issue 评论和描述中提炼真实用户声音：

| 反馈类型 | 内容来源 | 原话 / 摘要 |
|---------|---------|-------------|
| **满意** | [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) | “国内用起来特别舒服——本地化做得很到位，设置清晰无门槛，开箱即用。赞一个 👍” |
| **痛点** | [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | “新建会话后，模型的配置会全部丢失……只能重启”——配置持久化问题严重影响连续使用。 |
| **痛点** | [#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878) | “定时任务能正常触发、LLM 也能正常执行，但最终结果无法推送到微信”——渠道集成可靠性待加强。 |
| **痛点** | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | “升级到 1.1.9/1.1.10 后，对话提交后无响应，旧版本 1.1.5.post2 正常”——版本回退用户。 |
| **痛点** | [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) | “桌面端从 Python 打包换为 Tauri 后，启动时间从一两分钟变成十几分钟”——性能回归。 |
| **使用场景** | [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) | “主模型为纯文本模型（如 deepseek-v4-flash），但偶尔需要处理图片”——视觉 fallback 的典型需求。 |
| **不足** | [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994) | “记忆系统功能比较薄弱，不支持自进化的逻辑”——对长期记忆能力不满。 |
| **配置问题** | [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) | “DeepSeek API 要求 tool name 必须匹配 `^[a-zA-Z0-9_-]+$`，而内置 PAT 工具名含点号”——第三方 API 兼容性仍需校验。 |
| **主动模式** | [#5030](https://github.com/agentscope-ai/QwenPaw/issues/5030) | “开启主动模式后，微信频道出现一个问题两次回复”——主动模式并发控制可能存在 bug。 |

---

## 8. 待处理积压（长期未响应 / 重要开放项）

以下 Issue 或 PR 已开放较长时间或对项目健康度关键，建议维护者优先关注：

| 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|---------|---------|------|
| [#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751) | 系统托盘图标（Windows） | 2026-04-23 | 2026-06-10 | 近 2 个月无 assignee，社区有持续评论。 |
| [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) | 支持 AgentScope tracing 初始化入口 | 2026-05-06 | 2026-06-10 | 可观测性需求，长期无回复，但近期有更新。 |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | 后端迁移至 AgentScope 2.0 | 2026-05-27 | 2026-06-09 | **Breaking Change**，项目架构升级关键决策点。 |
| [#4891](https://github.com/agentscope-ai/QwenPaw/pull/4891) | 技能池多路径支持 | 2026-06-02 | 2026-06-10 | PR 已开放 8 天，未标记“Ready for Merge”，等待 review。 |
| [#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669) | Tauri 桌面端自动更新 | 2026-05-25 | 2026-06-10 | 虽被持续更新，但基础功能仍为 draft，影响桌面版用户体验。 |
| [#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917) | 聊天界面数据多时切换卡顿 | 2026-06-02 | 2026-06-10 | 与 [#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015) 类似，前端性能瓶颈，可合并跟踪。 |

**提醒**：AgentScope 2.0 迁移（#4727）的讨论已有初步结论但尚未进入开发阶段，建议尽快发布 RFC 或原型 PR，避免社区重复投入。

---

**总结**：CoPaw 项目在 24 小时内展现了旺盛的社区活力与迅速的 bug 修复节奏。稳定性修复（MCP、空列表、JSON 损坏）与技能生态落地是本次短期进展的亮点；然而，前端性能、桌面端启动速度、配置持久化等遗留问题仍影响用户信任。功能上，学习循环与记忆进化预示着项目向“自主 Agent”演进的可能性，但需平衡架构复杂性与当前维护能力。核心维护者应优先处理 AgentScope 2.0 迁移的并行工作，避免技术债堆积。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是基于 ZeroClaw 项目 2026-06-10 截止数据的项目动态日报。

---

## ZeroClaw 项目动态日报 (2026-06-10)

### 1. 今日速览

过去24小时内，ZeroClaw 项目保持极高的迭代活跃度，共计产生50条 Issue 和 50 条 PR 更新，大量 S1/P1 级别的 Bug 获得了针对性的修复 PR，社区讨论则集中在多租户安全与 Agent 自主性上。虽然今日无正式版本发布，但核心贡献者提交了多项高价值修复（如并行 SubAgent 返回、Docker 构建修复），项目整体处于密集的开发攻坚期。值得注意的是，项目治理结构（CODEOWNERS）今日也进行了调整，反映了核心团队的职责变动。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日有2个 PR 被正式合并/关闭，同时提交了多项关键修复 PR，推动项目在运行时稳定性、容器化及治理层面迈出重要一步。

- **重大功能闭环：** PR **[#7369](zeroclaw-labs/zeroclaw PR #7369)** 成功合并，实现了端到端的 AMQP 入站通道（支持 mTLS）以及驱动的确定性 SOP 运行。这标志着 ZeroClaw 在自动化运维（如监听发布源并执行 SOP 流水线）场景下具备了完全可部署的能力。
- **运行时可靠性提升：** PR **[#7442](zeroclaw-labs/zeroclaw PR #7442)** 针对性地修复了并行 `SubAgents` 和 `Delegates` 返回不可靠的核心问题，这对于依托 Agent 编排的复杂工作流至关重要。
- **容器化构建修复：** PR **[#7445](zeroclaw-labs/zeroclaw PR #7445)** 解决了因 workspace 变更导致的 Docker 预拉取依赖阶段失败的问题，恢复了 CI/CD 流水线的正常运转。
- **可观测性与配置：** PR **[#7444](zeroclaw-labs/zeroclaw PR #7444)** 修复了 Dashboard 的状态显示问题；PR **[#7441](zeroclaw-labs/zeroclaw PR #7441)** 则改进了 `zeroclaw doctor` 命令对自定义 Provider 的验证逻辑，使其不再依赖于遗留工厂方法。
- **系统上下文修复：** 针对长期被反馈的默认32K上下文被系统提示耗尽的问题（Issue [#5808](zeroclaw-labs/zeroclaw Issue #5808)），PR **[#7440](zeroclaw-labs/zeroclaw PR #7440)** 提交了修复方案，通过跳过无效的历史修剪逻辑来优化预算使用。
- **治理与组织：** PR **[#7443](zeroclaw-labs/zeroclaw PR #7443)** 更新了 CODEOWNERS，重新分配了核心维护领域并移除了离职成员，保持项目治理的清晰度。

### 4. 社区热点

过去24小时内讨论热度最高的议题反映了社区对生产级部署精细控制的强烈诉求：

- **多租户与访问控制（RBAC）：** Issue **[#5982](zeroclaw-labs/zeroclaw Issue #5982)** 获得了 9 条评论，用户强烈要求增加基于发送者的角色控制功能，以实现单实例服务多用户类别（客户、运营、开发者）的隔离。背后的核心诉求是 **从“能用”到“安全地分离使用”**。
- **Agent 自我工具认知：** Issue **[#5862](zeroclaw-labs/zeroclaw Issue #5862)** 用户反馈 Agent 不知道自己能添加 Cron 任务。这反映出社区对 Agent **元认知**能力的期待——即 Agent 应能主动识别并使用自身拥有的全部工具，而不是依赖用户的显式指令。
- **MCP 工具审批流程缺陷：** Issue **[#6721](zeroclaw-labs/zeroclaw Issue #6721)** 虽然评论数不多（4条），但它揭示了 MCP 工具 `tool_search` 在 Webhook 模式下因未纳入自动审批白名单导致挂起120秒后自动拒绝的严重 Bug，严重阻碍了自动化流程的建立。这是一个非常实际的 **阻塞用户工作流** 的热点。
- **Discord 频道隔离：** Issue **[#6378](zeroclaw-labs/zeroclaw Issue #6378)** 要求 Discord Bot 仅响应指定的频道 ID，这与 Matrix 和 Nextcloud Talk 的 `allowed_rooms` 模式保持一致，体现了社区对 **渠道功能一致性** 的追求。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在运行时核心和渠道兼容性上，其中多个严重 Bug 已有对应的修复 PR。

| 严重程度 | Issue | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **S1 - 工作流阻塞** | [#5808](zeroclaw-labs/zeroclaw Issue #5808) | 默认32K上下文预算在首次迭代即被系统提示和工具定义超过，导致持续预抢占式截断。 | **已有修复PR：[#7440](zeroclaw-labs/zeroclaw PR #7440)**
| **S1 - 工作流阻塞** | [#6034](zeroclaw-labs/zeroclaw Issue #6034) | 单轮及多轮对话中出现丢失用户消息的严重数据丢失问题。 | 待修复 |
| **S1 - 工作流阻塞** | [#6646](zeroclaw-labs/zeroclaw Issue #6646) | 通过 Telegram 频道无法触发 `web_search_tool` 和 `web_fetch` 工具。 | 待修复 |
| **S1 - 工作流阻塞** | [#6687](zeroclaw-labs/zeroclaw Issue #6687) | 单个守护进程中创建了两个独立的 `SopEngine` 实例，导致 MQTT 启动的 SOP 状态对 Agent 不可见。 | 待修复 |
| **S1 - 工作流阻塞** | [#6876](zeroclaw-labs/zeroclaw Issue #6876) | `risk_profile.allowed_tools` 无法限制 MCP 工具的调用。 | 待讨论 |
| **S2 - 功能降级** | [#6584](zeroclaw-labs/zeroclaw Issue #6584) | OpenAI 兼容提供商（如 OpenRouter、vLLM）忽略 `reasoning` 字段，仅读取 `reasoning_content`。 | **已有修复PR：[#7423](zeroclaw-labs/zeroclaw PR #7423)**
| **S2 - 功能降级** | [#7376](zeroclaw-labs/zeroclaw Issue #7376) | zerocode Dashboard 隐藏了错误状态，且错误地将历史记录标记为活跃会话。 | **已有修复PR：[#7444](zeroclaw-labs/zeroclaw PR #7444)**
| **S2 - 功能降级** | [#7377](zeroclaw-labs/zeroclaw Issue #7377) | zerocode 的深色主题继承了终端不可读的前景色，导致界面无法使用。 | 待修复 |
| **S2 - 功能降级** | [#6862](zeroclaw-labs/zeroclaw Issue #6862) | v0.8.0-beta-1 中 Gateway SPA 回退逻辑错误地为未实现的 `/api/*` 路由返回了 `index.html`，导致 Dashboard 崩溃。 | 待修复 |
| **S3 - 次要问题** | [#7378](zeroclaw-labs/zeroclaw Issue #7378) | macOS 上 Cmd-C 复制快捷键被误认为是退出快捷键。 | 待修复 |

### 6. 功能请求与路线图信号

除了紧急的 Bug 修复，社区的 Feature Request 也揭示了项目未来的演进方向：

- **Provider 架构重构（[#5937](zeroclaw-labs/zeroclaw Issue #5937)）：** 用户提议统一 `providers` 模块中的 `reqwest` 使用和模型构建参数，减少代码重复。这是 **架构层面** 的优化，有利于长期维护和扩展。
- **Skills 生态标准化（[#4853](zeroclaw-labs/zeroclaw Issue #4853)）：** 支持从 `.well-known` URI 安装技能。Cloudflare 和 Vercel 已在内部支持类似规范，ZeroClaw 的计划跟进意味着其技能市场正在向 **标准化协议** 靠拢。
- **细粒度安全权限（[#5775](zeroclaw-labs/zeroclaw Issue #5775), [#6916](zeroclaw-labs/zeroclaw Issue #6916)）：** 社区不再满足于全局的 `allow_scripts` 开关，而是要求 **per-skill** 级别的权限管理和子进程的内存限制。这反映了安全沙箱需求从测试环境向生产环境的过渡。
- **成本核算与观测性（[#7248](zeroclaw-labs/zeroclaw Issue #7248)）：** 用户要求持久化缓存的输入 Token 并将其纳入成本核算。配合 PR **[#7385](zeroclaw-labs/zeroclaw PR #7385)**（增加 Turn 元数据与 OTel 关联），可见观测性正在成为下一阶段的开发重点。

### 7. 用户反馈摘要

从近期的 Issue 评论中可以提炼出以下用户画像和痛点：

- **记忆管理的矛盾：** 用户 ([databillm](zeroclaw-labs/zeroclaw Issue #5844)) 抱怨 Agent “过度依赖记忆，忽视当前 Prompt，尤其在 Cron 任务中”。这显示了当前记忆检索算法 **无法很好地在长期背景与当前任务间取得平衡**。
- **自动化的挫败感：** 用户在 MCP 工具审批（[#6721](zeroclaw-labs/zeroclaw Issue #6721)）和 Cron 任务重入（[#6037](zeroclaw-labs/zeroclaw Issue #6037)）方面的反馈显示，**非交互式/Webhook 模式下的自动化流程充满了“陷阱”**，插件式的审批钩子和并发控制是当务之急。
- **渠道碎片化体验：** 由于不同渠道（Discord, Telegram, WhatsApp, Matrix）的功能实现进度不一，用户在不同平台上看到的表现不一致（如 Telegram 不触发搜索工具 [#6646](zeroclaw-labs/zeroclaw Issue #6646)，Matrix 线程问题 [#7349](zeroclaw-labs/zeroclaw PR #7349)）。**跨渠道功能对齐**是保持用户粘性的关键。
- **开源治理的关注：** `#7443` PR 中 CODEOWNERS 的变动，以及 `#7410` Issue 中用户提到“非维护者无法打标签”，说明社区成员对 **项目治理透明度和贡献流程** 保持着高度关注。

### 8. 待处理积压

以下为长期未解决或需维护者重点关注的重要事项：

- **Issue [#6037](zeroclaw-labs/zeroclaw Issue #6037) - [Bug] Cron 作业被反复触发：** 虽然标记为 `status:in-progress`，但至今没有明确的修复 PR，这涉及任务调度的核心稳定性。
- **Issue [#6687](zeroclaw-labs/zeroclaw Issue #6687) - [Bug] 双 SopEngine 实例：** 该 Bug 对 SOP 自动化场景影响极大，但自创建以来讨论较少（仅1条评论），可能因实现复杂而被搁置。建议维护者评估修复优先级。
- **Issue [#4853](zeroclaw-labs/zeroclaw Issue #4853) - [Feature] 从 `.well-known` 安装 Skills：** 3月27日已接受，但至今未见实质性进展。作为 Skill 生态系统的关键基础设施，应加快推动。
- **PR [#7215](zeroclaw-labs/zeroclaw PR #7215) - [Bug/Quickstart] Webhook 渠道端口配置缺失：** 该 PR 处于 `needs-author-action` 状态，代码已提交但作者未响应，导致 Quickstart 向导无法为 Webhook 渠道显示端口配置字段，阻塞了用户配置体验。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*