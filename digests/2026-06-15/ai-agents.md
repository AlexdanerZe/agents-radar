# OpenClaw 生态日报 2026-06-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-15 03:56 UTC

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

# OpenClaw 项目动态日报 — 2026-06-15

**数据来源：** [OpenClaw / openclaw](https://github.com/openclaw/openclaw) GitHub 仓库  
**统计时段：** 2026-06-14 至 2026-06-15（过去 24 小时）

---

## 今日速览

过去 24 小时内项目保持极高活跃度：共有 **500 条 Issue 更新**（其中新开 / 活跃 428 条，关闭 72 条）及 **500 条 PR 更新**（待合并 416 条，已合并 / 关闭 84 条），社区参与热情持续高涨。昨日发布了一个新的 Beta 版本（v2026.6.8-beta.1），重点强化了 Telegram 与 WhatsApp 渠道的消息投递健壮性。与此同时，大量 **P1 级别的稳定性 Bug**（消息截断、会话冲突、重复回复等）仍处于开放状态，项目团队正在通过 `clawsweeper` 标签体系分类追踪，整体健康度呈 **高活跃、高压力** 态势。

---

## 版本发布

### v2026.6.8-beta.1
- **发布日期：** 2026-06-08 前后（今日仍可见）  
- **标签：** [v2026.6.8-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.1)

#### 主要亮点
- **Telegram 渠道**：支持结构化富文本（表格、列表、可折叠引用块），CLI 后端投递更可靠，旧 draft 迁移已废弃，富媒体边界处理更安全。
- **WhatsApp 渠道**：投递边界检查增强，减少因媒体格式引发的异常。

#### 已知问题 / 迁移注意
- 部分用户升级至前序版本（2026.5.20 → 2026.6.1）后报告 DeepSeek Prompt Cache 失效、消息重复等问题（参见 [#91016](https://github.com/openclaw/openclaw/issues/91016)、[#86519](https://github.com/openclaw/openclaw/issues/86519)）。本 Beta 版本是否已完全修复尚未明确，建议升级前关注对应 Issue 的进展。
- `v2026.6.8-beta.1` 对底层会话锁机制进行了一定调整，如使用 `@openclaw/codex` 等扩展，建议先在测试环境验证。

---

## 项目进展

过去 24 小时内 **84 个 PR 被合并或关闭**，以下为归类列举的代表性合并 / 推进：

### 渠道修复与增强
| PR | 摘要 | 状态 |
| :--- | :--- | :--- |
| [#93148](https://github.com/openclaw/openclaw/pull/93148) | `fix(telegram):` 恢复发送消息的 SQLite 持久化记录 | 已合并 |
| [#93014](https://github.com/openclaw/openclaw/pull/93014) | `fix(telegram):` 将 `ERR_MODULE_NOT_FOUND` 归类为不可重试的死信 | 已合并 |
| [#93137](https://github.com/openclaw/openclaw/pull/93137) | `fix(imessage):` 正确解析 `channels.imessage.actions.reply === false` | 已合并 |

### 会话管理与核心引擎
- [#85643](https://github.com/openclaw/openclaw/pull/85643) — `fix(sessions):` 明确持久化用户选择的默认模型 pin（防止模型被自动切换）
- [#85402](https://github.com/openclaw/openclaw/pull/85402) — `fix(agents):` 在提示锁释放期间锁定会话事件写操作，减少错误的 `EmbeddedAttemptSessionTakeoverError`
- [#85651](https://github.com/openclaw/openclaw/pull/85651) — `feat(continuation):` **大型特性**，引入上下文压力感知的 Agent 延续信号（`continue_work / continue_delegate / request_compaction`），当前开放评审中

### 代码执行安全
- [#84172](https://github.com/openclaw/openclaw/pull/84172) / [#84118](https://github.com/openclaw/openclaw/pull/84118) — 将命令授权迁移至 Tree-sitter 命令行规划器，提升安全边界

### 持续集成与测试
- [#93114](https://github.com/openclaw/openclaw/pull/93114) — 将脚本测试用例归入 QA Lab 执行，提高测试覆盖的可维护性

> 整体来看，项目正在 **系统性修补会话并发、消息投递与渠道集成** 方面的长尾 Bug，同时稳步推进 continuation 这样的重要架构特性。

---

## 社区热点

以下为过去 24 小时内评论数最多的 Issue（反映社区最高关注度），均集中在 **会话可靠性与消息丢失** 问题上：

| Issue | 标题标签 | 评论 | 关键诉求 |
| :--- | :--- | :--- | :--- |
| [#85888](https://github.com/openclaw/openclaw/issues/85888) | Cron jobs fail with MiniMax 503 (05:00-07:30 CST) | **12** | 定时任务与手动触发表现不一致，怀疑调度层而非 API |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex app-server: 回复被静默截断 ~1000-1100 字符 | **11** | `stop=null` 但文本中断，多个用户复现，严重影响 headless 使用 |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex 导致长延迟、超时、Gateway 事件循环堵塞 | **9** | 复杂配置下简单消息也变成几十秒延迟，诊断路径不清晰 |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | 5.20 更新后 Agent 在 Telegram 上重复回复 2–10 次 | **9** | 5.22 减轻但未完全解决，用户强烈要求回滚或紧急修复 |
| [#86508](https://github.com/openclaw/openclaw/issues/86508) | `EmbeddedAttemptSessionTakeoverError` 在 Discord 运行中 | **9** | 会话文件在锁释放后被修改，影响多个用户 |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | 模型 fallback 链在提供方配额耗尽时不触发 | **9** | fallback 机制形同虚设，导致任务卡死 |

**分析：** 社区最关切的仍然是 **消息的完整交付与对话的连续性**。多个热门 Issue 都指向 Agent 在特定条件下（凌晨定时、长回复、复杂配置）不响应或输出错误。用户对 regressions（5.20/5.22 更新引入）反应激烈，希望团队在追求新功能前先稳住核心体验。

---

## Bug 与稳定性

过去 24 小时内有大量 Bug 报告，按严重程度排列如下（含 P0/P1 及影响范围）：

### P0 – 数据丢失
- [#84882](https://github.com/openclaw/openclaw/issues/84882) **memory-core `normalized recall artifacts` 静默删除每日记忆文件**  
  标签：`impact:data-loss`, `P0`  
  状态：无修复 PR，等待维护者评审  
  影响：用户 memory/YYYY-MM-DD.md 被无提示删除

### P1 – 核心功能受损 / 回归
| Issue | 问题 | 是否有修复 PR |
| :--- | :--- | :--- |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex 回复截断（~1100 字符） | 无 |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory → 延迟、超时、事件循环 stall | 无 |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | 升级后 Telegram 重复回复（5.20 引入） | 无（5.22 缓解但未根除） |
| [#86508](https://github.com/openclaw/openclaw/issues/86508) | EmbeddedAttemptSessionTakeoverError | 无 |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | 模型 fallback 链不触发 + 同一错误 | 无 |
| [#86047](https://github.com/openclaw/openclaw/issues/86047) | Codex app-server 插件审批 stall（Nextcloud Talk） | 无 |
| [#84882](https://github.com/openclaw/openclaw/issues/84882) | 记忆文件静默删除（P0） | 无 |
| [#85251](https://github.com/openclaw/openclaw/issues/85251) | Codex 发出 `turn/started` 后静默，会话卡死 | 无 |
| [#83184](https://github.com/openclaw/openclaw/issues/83184) | `pendingFinalDelivery` 卡住后续心跳 | 有 linked PR |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP 工具不注入子会话 | 无 |
| [#84536](https://github.com/openclaw/openclaw/issues/84536) | 上下文溢出静默终结会话 | 无 |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) | Gateway 内存泄漏（MacOS 空闲 1GB+） | 无 |
| [#91016](https://github.com/openclaw/openclaw/issues/91016) | DeepSeek Prompt Cache 失效，费用飙升（今日已关闭，原因待确认） | 已关闭 |

### 值得注意的闭环
- [#91016](https://github.com/openclaw/openclaw/issues/91016) 在今日被关闭，但关闭理由未明示，社区仍有疑问。
- [#85192](https://github.com/openclaw/openclaw/issues/85192) DeepSeek V4 reasoning-only 重试失败——已 closed。
- [#83425](https://github.com/openclaw/openclaw/issues/83425) xAI OAuth redirect_uri 不匹配——已 closed。

**稳定性总结：** 尽管发布频繁，但近几个版本（5.20 → 6.1）的回归未能及时收敛，特别是会话锁与消息投递路径仍存在多个并发缺陷，建议项目组优先投入 **session isolation** 与 **可靠反馈机制**。

---

## 功能请求与路线图信号

以下新功能请求获得较多关注，结合已有 PR 可判断可能进入下一版本：

### 高潜力 / 已有实施或设计
| Issue/PR | 描述 | 信号 |
| :--- | :--- | :--- |
| [#85651](https://github.com/openclaw/openclaw/pull/85651) | **context-pressure-aware continuation**（Agent 主动请求延续/压缩） | 大型 PR，附设计文档，已标记 `ready for maintainer look` |
| [#86881](https://github.com/openclaw/openclaw/issues/86881) | **Gateway-lite 模式**：不带 AI harness 的轻量部署 | 7 评论，多位用户表示需要纯网关场景 |
| [#44395](https://github.com/openclaw/openclaw/issues/44395) | **heading-aware chunking + 实体提取**（改进记忆搜索） | 长期开放（3 月），仍无实现，但需求稳定 |
| [#74077](https://github.com/openclaw/openclaw/issues/74077) | **会话内 streaming 模式切换（/stream 命令）** | P3，有清晰 UX 设计，社区讨论 5 条 |

### 值得关注的中等信号
- [#85461](https://github.com/openclaw/openclaw/issues/85461) 捕获图片生成 API 的使用量/成本元数据（P2）
- [#86381](https://github.com/openclaw/openclaw/issues/86381) 提高系统资源利用率（中文用户提出，分析了 event loop 延迟）
- [#79818](https://github.com/openclaw/openclaw/pull/79818) Slack 消息操作扩展（automerger 状态，即将合并）
- [#82303](https://github.com/openclaw/openclaw/pull/82303) Telegram 渐进式助手预览（progress assistantPreview）

**路线图判断：** Continuation、Gateway-lite、记忆改进是三大方向，其中 continuation 已有实现，最可能进入下一大版本（v2026.7）。

---

## 用户反馈摘要

从 Issue 评论中提炼的真实用户痛点与场景：

- **升级恐惧**：“After updating from 2026.5.12 to 2026.5.20, the agent sends duplicate replies.”（#86519）—— 用户期望点发布而不是大跳升级。
- **费用意外**：“Prompt Cache 完全失效，一小时烧掉约 $6”（#91016）—— 用户对成本敏感，要求 cache 机制可观测。
- **静默失败**：“returned `replies=0` … no error logged”（#85692 等）—— 多个渠道（Feishu、WhatsApp）存在无日志丢消息，让用户无从排查。
- **配置陡峭**：“MCP tools not injected into subagent” (#85030) —— 功能有文档但实际不生效，用户投入时间调试无果。
- **对轻量部署的需求**：“I like OpenClaw with AI, but I need gateway-only deterministic deployment”（#86881）—— 部分用户只需要 cron + webhook，不需要 LLM 层。
- **社区反馈积极**：尽管有 Bug，用户仍认真提供日志、根因分析（如 #86047 由 AI 代理代填 Issue），社区自组织 debug 氛围良好。

---

## 待处理积压

以下为创建时间较早或长时间未获得实质性进展的重要 Issue / PR，提醒维护者关注：

| # | 类型 | 标题 | 创建时间 | 最后更新 | 标签 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | Bug(P1) | Cron jobs silently time out during LLM outage（不快速失败） | 2026-03-13 | 2026-06-15 | `regression`, `impact:auth-provider` |
| [#44395](https://github.com/openclaw/openclaw/issues/44395) | Feature(P2) | heading-aware chunking + entity extraction | 2026-03-12 | 2026-06-15 | 需要产品决策 |
| [#74077](https://github.com/openclaw/openclaw/issues/74077) | Feature(P3) | 会话内 streaming 模式切换 | 2026-04-29 | 2026-06-15 | `needs-product-decision` |
| [#77467](https://github.com/openclaw/openclaw/issues/77467) | Bug(P1) | MiniMax OAuth 无法自动刷新（无 refreshOAuth） | 2026-05-04 | 2026-06-15 | `impact:auth-provider` |
| [#83184](https://github.com/openclaw/openclaw/issues/83184) | Bug(P1) | `pendingFinalDelivery` 阻塞心跳 | 2026-05-17 | 2026-06-15 | 有 linked PR 但未合并 |
| [#81382](https://github.com/openclaw/openclaw/pull/81382) | PR(P2) | Link heartbeat commitment to replies | 2026-05-13 | 2026-06-15 | `waiting on author`，长期 stale |
| [#83964](https://github.com/openclaw/openclaw/issues/83964) | Bug(P1) | `@openclaw/codex` 报 `ERR_MODULE_NOT_FOUND` | 2026-05-19 | 2026-06-15 | 需要产品决策 |

> **特别提醒：** [#45494](https://github.com/openclaw/openclaw/issues/45494) 与 [#44395](https://github.com/openclaw/openclaw/issues/44395) 已悬置近三个月，前者影响 cron 用户的核心可靠性，后者是记忆系统的重要提升，建议排期处理。

---

*本日报由 AI 自动生成，数据基于 OpenClaw 公开 GitHub 指标，部分分析结论仅供参考。*

---

## 横向生态对比

# 个人AI助手与自主智能体开源生态横向对比分析报告（2026-06-15）

---

## 1. 生态全景

当前个人AI助手/自主智能体开源生态处于 **“高活跃、高碎片、高质量博弈”** 阶段：头部项目日均处理数百条Issue/PR，迭代速度极快，但普遍面临回归频发、安全边界薄弱与用户信任波动的问题。社区对**消息投递可靠性、会话连续性、成本透明化**的诉求跨越所有项目成为共同痛点；同时，**架构解耦（插件化/Operator化）、轻量边缘部署、AI原生开发自举**正从少数项目的前沿探索扩散为行业共识。整体上看，生态正从“功能竞赛”进入“稳定性+安全+可观测性”的深水区。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 PR | 版本发布 | 健康度评估 |
|------|-------------|---------|--------------|----------|------------|
| **OpenClaw** | 500（含新开428，关闭72） | 500（待合并416，已合并84） | 84 | v2026.6.8-beta.1 | 极高活跃，P0/P1回归积压，高压力 |
| **ZeroClaw** | 42（关闭28） | 50（待合并46） | 少量合并 | 无 | 高热，审查瓶颈明显，治理转型期 |
| **IronClaw** | 42 | 45（15合并/关闭） | 15 | 无 | 高强度迭代+安全审计并进，发布受阻 |
| **Hermes Agent** | 50 | 50（4合并，8关闭） | 4 | 无 | 高活跃，安全漏洞集中涌现 |
| **NanoBot** | 51总更新 | 27合并 | 27 | 无 | 快速闭环，API兼容性遗留问题 |
| **CoPaw** | 24 | 16（5合并） | 5 | 无 | 极高活跃但回归严重，社区贡献积极 |
| **NanoClaw** | 7 | 10（合并多个大型PR） | 多个 | 无 | 高速迭代+安全审计并行，亟需加固 |
| **PicoClaw** | 5 | 9（5合并） | 5 | v0.2.9-nightly | 稳定修复，插件生态起步 |
| **LobsterAI** | 2 stale | 5（2合并） | 2 | 无 | 中等活跃，PR积压73天需关注 |
| **NullClaw** | 1 | 0 | 0 | 无 | 低活跃，需避免需求冷却 |
| **Moltis** | 1 | 0 | 0 | 无 | 静默期，边缘部署方向明确 |
| **TinyClaw** | 0 | 0 | 0 | — | 无活动 |
| **ZeptoClaw** | 0 | 0 | 0 | — | 无活动 |

---

## 3. OpenClaw 在生态中的定位

**社区规模**: OpenClaw 以每日 500+ Issue/PR 的体量稳居生态第一梯队，远超第二集团（IronClaw、ZeroClaw 约 40-50 级别）。其多消息渠道（Telegram/WhatsApp/iMessage 等）和会话持久化能力是核心差异化优势。

**技术路线差异**:
- 相比 **NanoBot/ZeroClaw** 的 API 优先和集成优先，OpenClaw 更强调 **端到端会话建模**（记忆、延续、锁机制），但代价是架构复杂度导致回归难以收敛。
- 相比 **Hermes Agent** 的多 Profile 隔离和 **NanoClaw** 的 Operator 驱动，OpenClaw 的配置体系更偏“单体全功能”，社区对“升级即破坏”的抱怨集中（v5.20/5.22 引入重复回复等问题）。
- 与 **CoPaw**（中国桌面+移动优先）相比，OpenClaw 的渠道更全球化，但缺少本地化（企业微信、飞书）支撑。

**竞争风险**: 若 OpenClaw 无法在未来 2-3 个版本内系统解决会话锁、消息截断等 P0/P1 回归，将面临高阶用户向 **NanoBot（API 稳定）** 或 **IronClaw（强安全审计）** 迁移的压力。不过其“continuation”等大型架构特性（PR #85651）若成功落地，将继续保持技术领先。

---

## 4. 共同关注的技术方向（横跨多项目）

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **安全边界加固** | NanoClaw, Hermes, IronClaw, PicoClaw, CoPaw | 审批流参数隐藏、文件路径泄露、凭证跨Profile访问、shell命令前缀匹配绕过、CMD弹窗风险等。漏洞报告方呈现“研究员主动提交”趋势。 |
| **消息投递可靠性** | OpenClaw, NanoBot, Hermes, CoPaw, ZeroClaw | 重复回复、截断、无日志静默丢包、长消息渲染异常、Cron任务孤儿等。用户对“静默失败”容忍度已降至最低。 |
| **Token/成本可观测性** | OpenClaw, NanoBot, NanoClaw, Hermes | Prompt Cache 失效致费用飙升、API token统计为零、预算耗尽无反馈。社区要求成本告警与配额控制的呼声强烈。 |
| **多Provider灵活切换** | 几乎所有活跃项目 | 移除硬编码依赖（OpenClaw DeepSeek、NanoBot Anthropic、Hermes Claude、NullClaw Azure、ZeroClaw Inception Labs），用户渴望按任务自动路由 Provider。 |
| **边缘/轻量部署** | OpenClaw(Gateway-lite), ZeroClaw(气隙), Moltis(turbovec), PicoClaw(远程Agent), CoPaw(Computer Use) | 产业界向端侧下沉趋势明显，纯网关/离线模式/低内存后端成为下一波差异点。 |
| **会话上下文连续性** | OpenClaw(会话锁/continuation), NanoBot(会话隔离), Hermes(Cron Profile孤儿), CoPaw(上下文压缩0保留) | 长期对话的安全恢复、Agent间上下文不污染仍是工程难点。 |

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构亮点 | 社区驱动特征 |
|------|----------|----------|--------------|--------------|
| **OpenClaw** | 全能型个人AI助手 | 个人极客/泛AI用户 | 渠道丰富、记忆与延续系统 | 高贡献高抱怨，用户希望“先稳定再功能” |
| **NanoBot** | API兼容的Agent运行时 | 开发者/企业API集成 | OpenAI API兼容、WebUI配置对齐、微服务走向 | 品质迭代快，社区贡献PR质量高 |
| **Hermes Agent** | Profile隔离的安全Agent | 多场景隔离的进阶用户 | Docker优先、Multi-Profile、OAuth集成 | 安全议题主导，Claude订阅需求强 |
| **NanoClaw** | Operator驱动的模块化Agent | 高级Agent开发者/安全敏感 | Operator显式Provider切换、Codex v2集成、容器工具链数据化 | 安全审计密集，用户期待“可信自治” |
| **IronClaw** | AI-Native工程组织自举 | 企业/团队AI落地 | Reborn新架构、Dogfooding、Slack等业务通道 | 自开发计划吸引注意，发布阻塞影响社区信心 |
| **CoPaw** | 桌面+企业IM原生AI助手 | 中国市场企业/桌面用户 | 计算机操控(GUI)、插件SDK、企业微信/飞书/钉钉 | 回归影响显著但社区协作氛围好，国际化萌芽 |
| **PicoClaw** | 轻量模块化Agent框架 | 嵌入式/插件开发者 | 插件频道Hook、远程Agent、新版错误处理 | 小而精，强调KISS和贡献者安全素养 |
| **ZeroClaw** | 万能AI连接器 | 集成商/全栈开发者 | 海量第三方服务集成、SMS网关/智能家居 | 贡献者吞吐瓶颈，治理自动化RFC提上日程 |
| **LobsterAI** | 办公文档协作Agent | 办公场景用户 | Artifact分享(DOCX/PDF等)、Schedule Task幽灵修复 | 技术债务积累，社区反馈弱 |
| **Moltis** | 极致轻量边缘Agent运行时 | MCU/传感器开发者 | 纯Rust、no_std兼容、turbovec内存后端 | 前瞻性架构社区，目前讨论深度有限 |
| **NullClaw** | Azure生态首选Agent | 微软企业栈用户 | Azure托管身份认证 | 活跃度低，单点需求 |

---

## 6. 社区热度与成熟度分层

| 阶段 | 项目 | 判断依据 |
|------|------|----------|
| **快速迭代扩张期（极高活跃，功能与bug并行）** | OpenClaw, ZeroClaw, IronClaw, Hermes Agent, NanoBot, CoPaw | 每日 Issue/PR 合计40+，新功能与安全修复同时涌现，社区关注度高但不稳定。 |
| **稳步推进期（功能增加，开始治理技术债）** | NanoClaw, PicoClaw | 每日更新在10-20件，安全审计集中，核心功能合入后倾向于打磨稳定性。 |
| **质量巩固/瓶颈期（活跃下降，积压显现）** | LobsterAI, NullClaw | PR/Issue新增量少，存在长期未review的贡献，社区沟通频率低。 |
| **概念孵化期（静默但方向清晰）** | Moltis, TinyClaw, ZeptoClaw | 几乎无日常更新，偶尔出现架构级提议，项目仍处早期探索阶段。 |

---

## 7. 值得关注的趋势信号（对AI智能体开发者的参考）

1. **安全已成为社区的“第一性原理”**  
   三家独立研究员（YLChen-007 等）同日向 NanoClaw、Hermes、IronClaw 提交9个高危漏洞。所有AI Agent开发者应尽早引入**文件沙箱、审批流参数审查、本地网关认证**等基础防护，否则会快速流失敏感用户。

2. **用户对“成本不可知”的容忍度接近零**  
   OpenClaw（Prompt Cache失效烧$6）、NanoBot（Token统计为零）、NanoClaw（预算耗尽静默丢包）三条不同路径指向同一结论：**没有成本反馈机制的Agent不可信任**。开发者应在第一版就内置配额告警和Token审计日志。

3. **“边缘离线”不是未来，而是正在发生的需求**  
   Moltis 的 turbovec、ZeroClaw 的气隙模式、OpenClaw 的 Gateway-lite 在一天内同时出现，表明用户场景已从“连网可用”进化到“受限环境可靠运行”。端侧Agent部署将成为差异化的关键战场。

4. **插件化生态决定长期留存**  
   CoPaw（Computer Use/DataPaw）、PicoClaw（RegisterChannelSettings Hook）、ZeroClaw（第三方集成闭环）验证了**能自我扩展的项目才具备平台潜力**。开发者应设计插件系统而非硬编码功能。

5. **AI原生工程自举代表下一阶段组织能力**  
   IronClaw 的 #4878 系列（用 IronClaw 开发 IronClaw）并非噱头——当项目开始Dogfooding自己的Agent做CI/代码审查/发布时，才真正具备**商业级可靠性**。社区会视此为成熟度分水岭。

6. **企业级渠道是最强的锁客入口**  
   CoPaw 对企业微信/飞书/钉钉的支持、ZeroClaw 的 SMS 网关、Hermes 的 Matrix E2EE 表明，掌握特定垂直渠道的Agent项目更容易建立护城河。下一阶段竞争将从模型能力转向渠道体验与合规。

---

**数据源**: 各项目 GitHub 社区动态日报（2026-06-15）  
**分析师**: AI 智能体与个人 AI 助手开源生态资深分析师  
**报告时间**: 2026-06-15

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 每日项目动态日报 | 2026-06-15

*数据来源：HKUDS/nanobot GitHub 仓库*

---

## 1. 今日速览

项目在 **2026-06-15** 维持了极高强度的开发节奏。过去24小时内，项目累计发生 **51 次 Issue/PR 更新**，其中合并/关闭了 **27 个 Pull Requests**，另有 **19 个 PR** 处于待合并状态。尽管没有正式版本发布，但代码库在**架构解耦**（打破循环导入）、**WebUI 功能大幅对齐**、**Agent 循环稳定性**以及**多 Provider 兼容性**方面取得了显著进展。社区参与度同样处于高位，多个关键 Bug 由社区发现并同步提交了修复 PR。项目维护者 **@chengyongru** 主导了绝大多数合并，体现了健康的快速迭代闭环。

---

## 2. 版本发布

无。项目过去24小时未发布新版本。

---

## 3. 项目进展

过去24小时内 **合并了 27 个 PR**，覆盖了核心架构、应用功能和文档体验优化。

**核心架构与稳定性（Core Architecture & Stability）**
- **打破循环依赖**：[#4314](https://github.com/HKUDS/nanobot/pull/4314) 将工具配置模型从核心模式中解耦，消除导入循环，为工具系统的模块化扩展扫清障碍。
- **执行工具增强**：[#4273](https://github.com/HKUDS/nanobot/pull/4273) 新增 `tools.exec.pathPrepend` 配置，赋予用户在系统 `PATH` 之上优先定义自定义工具路径的能力。
- **文件系统开关**：[#4138](https://github.com/HKUDS/nanobot/pull/4138) 增加 `tools.file.enable` 开关，允许管理员完全禁用内置文件工具，提升沙箱部署场景的安全性。
- **会话边界优化**：[#4274](https://github.com/HKUDS/nanobot/pull/4274) 和 [#4299](https://github.com/HKUDS/nanobot/pull/4299) 强化会话上下文管理：Cron 任务绑定到触发的会话，历史摘要写入带会话标识，避免上下文污染。
- **Agent 循环增强**：[#4269](https://github.com/HKUDS/nanobot/pull/4269) 修复 Agent 在耗尽工具迭代次数时无法给出最终结论的交互缺陷。
- **配置健壮性**：[#4275](https://github.com/HKUDS/nanobot/pull/4275) 让系统在遇到无效配置文件时快速失败而非静默使用默认值。

**WebUI 与用户体验**
- **移动端响应式**：[#4339](https://github.com/HKUDS/nanobot/pull/4339) 大幅优化移动端排版布局、侧边栏和热力图显示。
- **桌面端稳定性**：[#4210](https://github.com/HKUDS/nanobot/pull/4210) 修复了桌面端引擎重启后 Token 刷新及 WebSocket 回放断流问题。

**多平台与 Provider 修复**
- **Feishu 启动加速**：[#4277](https://github.com/HKUDS/nanobot/pull/4277) 对飞书 SDK 进行懒加载，避免不必要的启动开销。
- **Anthropic 兼容性**：[#4333](https://github.com/HKUDS/nanobot/issues/4333)（已关闭）紧急修复 Opus-4-8 / Fable 模型因发送已弃用参数而报 400 错误的问题。
- **Telegram 消息修复**：[#4250](https://github.com/HKUDS/nanobot/issues/4250)（已关闭）修复消息分割导致代码块渲染异常的问题。

**文档改进**
- **[#4177](https://github.com/HKUDS/nanobot/pull/4177)** 大规模重写入门指南，提供新手友好型 Setup 路径。
- **[#4245](https://github.com/HKUDS/nanobot/pull/4245)** 清理旧版开发文档，简化贡献流程。

---

## 4. 社区热点

过去24小时社区讨论高度集中，主要围绕功能补全和关键错误修复。

- **🔥 WebUI 配置全面对接**：[#4313](https://github.com/HKUDS/nanobot/pull/4313) 是近期体量最大、讨论度最高的 PR，旨在消除 WebUI 设置面板与 `config.json` 之间的功能鸿沟。新增了对 Temperature、Tool Limits、Dream 等核心参数的写接口。这表明社区对「可视化配置」与「配置文件」深度并行的需求非常迫切，是项目向平台化演进的关键步骤。

- **⚠️ 图像回退安全漏洞**：[#4345](https://github.com/HKUDS/nanobot/issues/4345) 的报告迅速成为焦点。贡献者 **@BearMett** 发现当模型处理图像出错时，回退机制不仅让模型「幻觉」自己看到了图像，还泄露了绝对文件路径。更值得关注的是，该作者几乎在提交 Issue 的同时就提交了修复 PR [#4346](https://github.com/HKUDS/nanobot/pull/4346)，展现了社区极高的协作素养和对安全问题的敏感度。

- **🧪 API 统计异常**：[#4309](https://github.com/HKUDS/nanobot/issues/4309) 提出的 `/v1/chat/completions` 接口返回零 Token 用量问题，直接影响了依赖 API 进行计费或监控的用户。目前该 Issue 尚无修复 PR 分配，是当前社区最关切的待办事项。

- **自动化管理界面**：[#4330](https://github.com/HKUDS/nanobot/pull/4330) 提出的自动化管理视图（Automation Management View）获得了大量关注，用户希望能够更直观地在 WebUI 中管理 Cron 定时任务。

---

## 5. Bug 与稳定性

| 严重度 | Issue/PR | 描述 | 状态 | 补救 |
|---|---|---|---|---|
| **极高** | [#4309](https://github.com/HKUDS/nanobot/issues/4309) | `nanobot serve` 的 Token 统计始终返回硬编码零值 | 待修复 | **尚无修复 PR**，需要维护者优先关注 |
| **高** | [#4345](https://github.com/HKUDS/nanobot/issues/4345) | 图片回退机制导致模型「幻觉」和本地路径泄漏 | **已有修复** | 用户 @BearMett 已提交 PR [#4346](https://github.com/HKUDS/nanobot/pull/4346) |
| **高** | [#4333](https://github.com/HKUDS/nanobot/issues/4333) | Anthropic Opus-4-8 / Fable 因已弃用参数全部请求失败 | **已修复** | 已合入修复并关闭 Issue |
| **中** | [#4343](https://github.com/HKUDS/nanobot/pull/4343) | 内置工具参数校验宽松，可能静默忽略未知参数 | 审查中 | PR 已提交，提议严格化 JSON Schema 校验 |
| **中** | [#4293](https://github.com/HKUDS/nanobot/pull/4293) | 子代理（Subagent）在 Cron 等直接调用场景无法注入结果 | 审查中 | PR 已提交，@yorkhellen 贡献 |
| **低** | [#4337](https://github.com/HKUDS/nanobot/pull/4337) | Runner 空负载注入导致出现空白用户消息 | 审查中 | PR 已提交，@yu-xin-c 贡献 |
| **低** | [#4250](https://github.com/HKUDS/nanobot/issues/4250) | Telegram 长消息分割破坏代码块渲染 | **已修复** | 已合入并关闭 |
| **低** | [#4262](https://github.com/HKUDS/nanobot/issues/4262) | Agent 模式启动时未立即展示自定义 Bot 图标 | **已修复** | 已合入并关闭 |

---

## 6. 功能请求与路线图信号

从今日的数据中可以捕捉到项目明确的演进方向：

1. **配置平台化**：[#4313](https://github.com/HKUDS/nanobot/pull/4313)（WebUI 与 config.json 对齐）和 [#4330](https://github.com/HKUDS/nanobot/pull/4330)（自动化管理视图）共同表明，项目正在将核心配置和管理能力从纯文件编辑向 Web 图形界面迁移。这将是下一版本最显著的特性升级。
2. **生产级稳定性**：针对 Provider 兼容性（#4333）、会话隔离（#4274、#4299）、工具参数校验（#4343）的密集修复，表明项目已经从「0到1可用」阶段过渡到「复杂生产环境下是否可靠」的打磨阶段。
3. **安全管控增强**：[#4138](https://github.com/HKUDS/nanobot/pull/4138)（内置工具开关）和 [#4346](https://github.com/HKUDS/nanobot/pull/4346)（路径泄漏修复）反映出社区对 Agent 安全边界管控的持续关注。预计未来版本会引入更多细粒度的安全配置（如白名单、路径拦截）。

---

## 7. 用户反馈摘要

- **API 用户痛点**：@alx1379 在 [#4309](https://github.com/HKUDS/nanobot/issues/4309) 中明确指出 API 兼容性测试的遗漏问题，反映出正式应用对接方对 OpenAI API 协议合规性的要求十分严苛。
- **高级工作流需求**：@yorkhellen 提交的 PR [#4293](https://github.com/HKUDS/nanobot/pull/4293) 表明，部分用户正在构建复杂的多层 Agent 工作流（Cron 触发子代理），任何中间环节的阻断（如 pending_queue 缺失）都会造成整个自动化链路的崩溃。
- **安全意识提升**：@BearMett 对 [#4345](https://github.com/HKUDS/nanobot/issues/4345) 的报告极其专业，不仅指出错误，还深入剖析了 Impact（模型幻觉 + 隐私泄露），证明社区用户已具备较高的安全审慎意识。
- **细节体验关注**：@mraad 提出的 Bot 图标启动显示问题（[#4262](https://github.com/HKUDS/nanobot/issues/4262)）虽是小细节，但反映了用户对「第一印象」和产品润色度的追求。

---

## 8. 待处理积压

当前 Backlog 管理整体较好，主要积压情况如下：

**🔴 高风险未处理：**
- **[#4309](https://github.com/HKUDS/nanobot/issues/4309) — `nanobot serve` Token 统计为零**。已敞开 **3 天**，目前无修复 PR。影响 OpenAI API 兼容端点的核心功能，建议维护者优先介入评估和修复。

**需要推动审查的社区 PR：**
- **[#4293](https://github.com/HKUDS/nanobot/pull/4293)** — 子代理直接调用修复（@yorkhellen 贡献）。解决的是 Cron 工作流的关键失能问题，已经停留数日，建议优先 Review。
- **[#4343](https://github.com/HKUDS/nanobot/pull/4343)** 和 **[#4337](https://github.com/HKUDS/nanobot/pull/4337)** — 均为提升代码健壮性的优质 PR，来自社区贡献者 @yu-xin-c，可以安排合并。

**大型特性跟踪：**
- **[#4313](https://github.com/HKUDS/nanobot/pull/4313) — WebUI 配置对齐**。代码体量巨大，当前为 Open 状态且持续更新。需要关注其 Code Review 进度，防止因迭代时间过长导致与主线产生严重冲突或功能碎片化。

---
*报告生成时间：2026-06-15 | 数据统计周期：过去 24 小时*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-15

## 今日速览

项目今日保持高活跃度，24小时内共处理 **50 条 Issue** 和 **50 条 PR**，社区参与度极高。前期三大热点问题均在本日获得重大进展：长期困扰用户的 **输出截断 Bug（#7237）** 在经历2个月后终于关闭，**数据路由透明度（#45058）** 议题也已关闭，而呼声极高的 **Claude 订阅集成（#25267）** 讨论持续升温。然而，值得警惕的是，今日集中报告了 **3 个安全相关漏洞（#46411、#46413、#46422）**，涉及凭证跨 Profile 泄露和 CI/CD 权限配置。整体而言，项目进入密集的 Bug 修复与功能开发并行期，稳定性与安全性修复是今日的攻坚重点。

## 项目进展

今日共合并了 **4 个 PR**，并关闭了 **8 个 Issue**，主要内容聚焦于 Docker 环境稳定性、平台兼容性和测试覆盖：

- **Docker 环境与 s6 服务管理优化：**
  - **[PR #46291]** (已合并): 修复了延迟添加的 Profile 网关因日志父目录权限问题导致 `s6-log` 陷入 `mkdir`/`lock` 死循环的 Bug，提升了 Docker 部署的健壮性。
  - **[PR #46289]** (开放): 清理 `s6-log` 陈旧锁文件，防止在 virtiofs-backed 容器中启动卡死。
  - **[PR #46292]** (开放): 在容器重启后持久化 Profile 网关的期望状态，确保操作意图不会丢失。

- **平台兼容性与功能修复：**
  - **[PR #46399]** (已合并): 修复了本地后端 `terminal.env_passthrough` 无法从 `~/.hermes/.env` 文件读取变量的问题，与 Docker 后端行为对齐。
  - **[PR #46438]** (已合并): 为 `send_message` 工具添加了 Telegram `sendRichMessage` 快速通道，使 Markdown 格式的表格、任务列表等能原生渲染。
  - **[PR #39840]** (已合并): 修复了 TUI 仪表盘在嵌入式网关传输未就绪时的 `/chat` 崩溃问题。

- **安全性加固：**
  - **[PR #46422]** (开放): 着手加固 GitHub Actions 工作流，限制默认 Token 权限，防止凭证泄露。

- **测试与代码质量：**
  - **[Issue #36515]** (已关闭): 完成了 `plugins/web/parallel/provider.py` 模块的测试覆盖率提升工作，从 22.52% 提升至目标线以上。

## 社区热点

今日社区讨论高度集中，三大热门议题反映了用户最核心的诉求：

1.  **#7237 - 输出截断错误（46条评论，6👍，已关闭）**
    - **链接**: [NousResearch/hermes-agent Issue #7237](https://github.com/NousResearch/hermes-agent/issues/7237)
    - **分析**: 这是存在逾2个月的长期 Bug 首次得到解决，是今日最大的社区关注点。用户在 CLI 和 Telegram/Discord/Slack 网关上生成长篇回答时，频繁遭遇输出被截断的问题。该问题的关闭标志着项目在长文本处理稳定性上的重要进步，极大地缓解了高频用户的痛点。

2.  **#25267 - Claude 订阅 OAuth 集成（7条评论，21👍，开放）**
    - **链接**: [NousResearch/hermes-agent Issue #25267](https://github.com/NousResearch/hermes-agent/issues/25267)
    - **分析**: 获得了今日最高点赞数，反映出社区对与 Claude 订阅生态整合的强烈渴望。用户希望使用自己的 Claude 订阅而非需要额外付费的 API Key。如果该功能被采纳，将是吸引更广泛用户群体的关键举措，具有重要的商业和生态价值。

3.  **#45058 - Web 搜索/提取默认路由到 Parallel.ai（7条评论，15👍，已关闭）**
    - **链接**: [NousResearch/hermes-agent Issue #45058](https://github.com/NousResearch/hermes-agent/issues/45058)
    - **分析**: 用户对 `web_search` 和 `web_extract` 工具在没有明确用户同意的情况下，默认后端从 Firecrawl 静默切换为 Parallel.ai 表达了强烈的不满。这体现了社区对数据路由透明度和用户自主选择权的高度敏感。虽然 Issue 已关闭，但后续的默认行为设计需更加审慎。

## Bug 与稳定性

今日报告的 Bug 中，安全性问题是最大焦点，同时存在多个需优先处理的严重 Bug。

### P1（严重级）
- **#32091 - Cron Job Profile 作用域孤儿问题** (开放，无PR)
  - **链接**: [NousResearch/hermes-agent Issue #32091](https://github.com/NousResearch/hermes-agent/issues/32091)
  - **摘要**: 非默认 Profile 下创建的 Cron Job 写入本地文件，但网关读取全局配置，导致任务被"遗忘"。影响所有多 Profile 用户。
- **#46310 - Matrix E2EE 密钥在媒体消息爆发时耗尽** (开放，无PR)
  - **链接**: [NousResearch/hermes-agent Issue #46310](https://github.com/NousResearch/hermes-agent/issues/46310)
  - **摘要**: 每次发送媒体消息都进行完整的 E2EE 初始化，高频场景下可能导致密钥耗尽并静默丢消息。

### P2（中等级）
- **#46411 - 安全漏洞：read_file 可跨 Profile 窃取凭证** (开放， P2)
  - **链接**: [NousResearch/hermes-agent Issue #46411](https://github.com/NousResearch/hermes-agent/issues/46411)
  - **摘要**: 文件安全检查未能覆盖兄弟 Profile 的凭证文件，存在权限提升风险。
- **#46413 - 安全漏洞：桌面版文件预览可读取 Hermes 凭证** (开放， P2)
  - **链接**: [NousResearch/hermes-agent Issue #46413](https://github.com/NousResearch/hermes-agent/issues/46413)
  - **摘要**: Electron 文件预览 IPC 守卫未屏蔽 Hermes 自身的 Token 存储文件。
- **#44560 - model.options 处理同步 HTTP 阻塞** (开放， P2)
  - **链接**: [NousResearch/hermes-agent Issue #44560](https://github.com/NousResearch/hermes-agent/issues/44560)
  - **摘要**: 慢速模型提供商响应会导致 WebSocket 超时，影响配置过程。
- **#46303 - 并发会话记忆交叉污染** (开放， P2)
  - **链接**: [NousResearch/hermes-agent Issue #46303](https://github.com/NousResearch/hermes-agent/issues/46303)
  - **摘要**: 共享记忆和 git 工作树导致多个并发会话互相干扰。

### P3（较低级）
- **#46090 - 基础任务执行变得异常缓慢** (开放，需复现)
- **#46265 - SimpleX 适配器 DM 回复静默丢失** (开放，无PR)
- **#46332 - Windows 平台 Cron 作业 Bash 脚本路径混乱** (开放，无PR)

## 功能请求与路线图信号

社区对集成的渴望和核心架构的改进建议构成了今日功能请求的主旋律。

1.  **#25267 - Claude 订阅 OAuth 集成 (23👍)**
    - **信号**: 获得超高社区认可度。这不仅是技术需求，更是战略方向。项目应评估与 Anthropic 合作提供 OAuth 流程的可行性，有望大幅降低用户准入门槛。

2.  **#31584 - 记忆上下文作为背景信息 (6条评论)**
    - **信号**: 用户敏锐地指出了当前记忆注入机制可能带来的安全威胁和混淆风险。该建议涉及 Agent 对话核心架构的调整，若纳入路线图，将提升 Agent 对语境的理解准确性和安全性。

3.  **#42199 - x86_64 macOS 桌面版构建 (4条评论)**
    - **信号**: 这是一个明确的用户盲区。当前仅提供 ARM64 二进制文件，将大量 Intel Mac 用户排除在外。发布 Intel 版本是扩大用户基数的直接手段。

4.  **#13490 - 可配置 TUI 状态栏 (1条评论)**
    - **信号**: 用户对终端 UI 个性化需求的具体体现。虽然讨论度不高，但类似追求简洁、可定制的 UI 反馈是长期存在的需求。

## 用户反馈摘要

从今日活跃的回复中，可以窥见用户的一些核心感受和诉求：

- **对自动化变更的警惕**: #45058 的讨论显示，用户对后端服务的静默替换反应强烈。他们希望即使是"更好的默认选项"，也应当在变更前给予明确的提示和选择权。这要求项目在推动体验优化时，必须将透明度和用户控制权放在首位。

- **对复杂架构的困惑**: #32091、#46303、#46411 等问题的根源都指向了日渐复杂但文档和默认行为未能完全跟上的多 Profile 架构。用户在实际使用中面临较高的理解和操作成本。

- **对"付费墙"的沮丧**: #25267 的高赞表明，用户认为无法复用 Claude 订阅是一种 "双重付费" 的负担。这不仅是技术问题，更是影响用户情感和品牌忠诚度的关键点。

- **对 Bug 修复周期的关注**: #7237 虽然已关闭，但长达 2 个月的解决周期暴露出项目在处理这类复现困难或影响面广的 Bug 时，资源分配和优先级判断可能需要优化。

## 待处理积压

以下为长期未作业或进展缓慢，但影响较大的议题，建议维护者重点关注：

1.  **#12020 - 工具进度事件输出控制 (2026-04-18创建， 58天)**
    - **链接**: [NousResearch/hermes-agent Issue #12020](https://github.com/NousResearch/hermes-agent/issues/12020)
    - **风险**: 因 `hermes.tool.progress` 事件导致前端与 OpenAI 接口不兼容，存在 2 个月无进展，限制了部分用户的前端工具链集成。

2.  **#26051 - 修复压缩失败时保留上下文 (2026-05-15创建， PR状态)**
    - **链接**: [NousResearch/hermes-agent PR #26051](https://github.com/NousResearch/hermes-agent/pull/26051)
    - **风险**: 这是一个重要的可靠性修复 PR，在上下文压缩失败时不应丢失对话历史，等待合并已一个月。建议尽快完成 Code Review 并合并。

3.  **#32091 - Cron Job Profile 作用域孤儿问题 (2026-05-25创建， 21天)**
    - **链接**: [NousResearch/hermes-agent Issue #32091](https://github.com/NousResearch/hermes-agent/issues/32091)
    - **风险**: 影响多 Profile 用户的核心 P1 Bug，目前无任何关联 PR，需尽快定级并分配修复。

4.  **#23094 - 可配置回滚粘性机制 (2026-05-10创建， 36天)**
    - **链接**: [NousResearch/hermes-agent Issue #23094](https://github.com/NousResearch/hermes-agent/issues/23094)
    - **风险**: 提供了对回滚/降级行为的精细控制，是提升配置灵活性的重要需求，长期未有维护者回复。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 **PicoClaw 项目动态日报**。

---

# PicoClaw 项目动态日报 | 2026-06-15

*数据来源：GitHub Issues & Pull Requests (sipeed/picoclaw)*

---

## 1. 今日速览

今日项目活跃度较高，样本期内共处理 **5 个 Issue** 与 **9 个 Pull Request**，并发布了最新的夜间构建版本。核心贡献集中爆发，合并了 **5 个 PR**，主要涉及错误处理增强、结构化日志重构以及 Agent 模块稳定性修复。社区提交的 **1 个回归 Bug**（Brave 搜索在配置迁移后静默失效）需要团队立即介入。整体而言，项目在插件化生态（第三方频道 Hook）与分布式部署（Agent 远程模式）的探索上加速推进，代码健康度稳步提升。

---

## 2. 版本发布

- **版本**: `v0.2.9-nightly.20260615.13a38bd1` (Nightly Build)
- **说明**: 自动构建的每日快照，集成了截至今日的低频主分支变更。可能存在未完全验证的改动，请谨慎在生产环境中使用。
- **变更对比**: [View Diff](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

## 3. 项目进展

昨日至今共有 **5 个 PR** 被合入主分支，主要集中在**稳定性增强**与**代码现代化**：

- **核心架构稳定性修复**：
  - [#2904](https://github.com/sipeed/picoclaw/pull/2904) 重构了 Agent 的重载与 Panic 恢复机制。使用同步 `defer/recover` 替换了异步 Goroutine，彻底消除了 Agent 模块在重载时潜在的协程泄漏与 Panic 残留风险，是近期内核对可靠性的重要提升。

- **错误处理与健壮性**（贡献者：`chengzhichao-xydt`）：
  - [#3124](https://github.com/sipeed/picoclaw/pull/3124) 修复 TTS 模块在 API 非 200 响应时可能静默忽略 `ReadAll` 错误的问题。
  - [#3123](https://github.com/sipeed/picoclaw/pull/3123) 显式处理文件系统模块中目录描述符 `Close()` 错误，消除静默失败路径。
  - [#3122](https://github.com/sipeed/picoclaw/pull/3122) 捕获 Evolution 功能中写文件的 `Close()` 错误，防止磁盘满或 NFS 错误导致的数据未写入。

- **可观测性提升**：
  - [#3121](https://github.com/sipeed/picoclaw/pull/3121) 将 OpenAI 兼容适配器中残留的 `log.Printf` 替换为 `logger.WarnCF`，日志系统全面完成结构化转型。

---

## 4. 社区热点

- **🔴 紧急回归报告**：[#3125](https://github.com/sipeed/picoclaw/issues/3125) `web_search` (Brave) 静默失效
  - **背景**：用户报告在架构升级将 API 密钥迁移至 `.security.yml` 后，核心搜索工具静默返回“无结果”。LLM 调用正常，但后端直接返回空数据，且无错误日志。
  - **分析**：这是近期重构带来的严重回归，且错误不具备可观测性，修复难度较高，已引起社区广泛担忧。

- **💬 安全增强主动提交**：[#3126](https://github.com/sipeed/picoclaw/pull/3126) 改进启动器允许列表绕过诊断
  - **背景**：贡献者主动提交 PR，通过追踪配置的三种状态（省略/显式设置/空值），在存在公共 IP 绑定可能绕过 CIDR 限制时发出清晰日志。
  - **分析**：反映了社区极高的安全意识以及自驱动的防御性编程文化。

- **🛠️ 分布式 Agent 呼声**：[#3118](https://github.com/sipeed/picoclaw/pull/3118) 引入远程 WebSocket Agent 模式
  - **背景**：该 PR 支持将 Agent 作为独立守护进程运行，通过 `--remote ws://...` 地址连接，实现了 Agent 与主进程的解耦。
  - **分析**：该 PR 获得了大量关注，标志着社区对分布式、高可用部署架构的强烈需求。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue / PR | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| 🔴 **严重** | [#3125](https://github.com/sipeed/picoclaw/issues/3125) | **Brave 搜索在 `.security.yml` 迁移后静默失效**。<br>功能完全不可用，且无错误提示，严重影响用户体验与项目可信度。 | 新报，无修复 PR |
| 🟡 **中等** | [#3041](https://github.com/sipeed/picoclaw/issues/3041) | **`mcp add` 全局标志解析错误**。破坏 HTTP/SSE 类型 MCP 的添加流程，并可能导致 Stdio 类型命名错误。 | 已 stale 8 天，无修复 PR |
| 🟡 **中等** | [#3044](https://github.com/sipeed/picoclaw/issues/3044) | **Matrix `allow_from` 配置对标准用户名格式失效**。含有冒号的用户 ID (`@user:domain.com`) 无法通过授权检查。 | 已 stale 8 天，无修复 PR |
| 🟡 **中等** | [#3090](https://github.com/sipeed/picoclaw/issues/3090) | **Web 面板在 iOS < 16.4 的 Safari 上无法工作**。限制了旧款苹果设备用户的移动端访问。 | 已 stale 5 天，无修复 PR |
| 🟢 **低 (已修复)** | [#3122](https://github.com/sipeed/picoclaw/pull/3122) #3123 #3124 | 社区批量修复了 TTS、Evolution、FileSystem 模块中潜在的静默失败路径（`Close()` 和 `ReadAll()` 错误处理）。 | **已合并** |

---

## 6. 功能请求与路线图信号

- **强力纳入 v0.3.0 候选**：
  - [#3120](https://github.com/sipeed/picoclaw/pull/3120) **`RegisterChannelSettings` Hook**：允许第三方模块注册配置项。这打破了“只能通过 Fork 添加频道”的限制，是 PicoClaw 走向插件生态系统的**关键里程碑**。
  - [#3118](https://github.com/sipeed/picoclaw/pull/3118) **Agent 远程 WebSocket 模式**符合将 AI Agent 作为独立后端服务部署的潮流。

- **用户呼声较高的需求**：
  - **Telegram 群聊交互优化**：[#2975](https://github.com/sipeed/picoclaw/pull/2975) 提议在 `mention_only` 模式下，回复 Bot 消息等同于 @提及。该 PR 已开放 16 天等待审核。
  - **更多 Provider 支持**：尽管 [#2978](https://github.com/sipeed/picoclaw/issues/2978)（添加 OmniRoute）因长期搁置被 Bot 关闭，但扩展上下文提供商的需求仍是社区高频请求。

---

## 7. 用户反馈摘要

- **痛点与流失风险**：
  - **迁移阵痛**：`Giordano10` 在 [#3125](https://github.com/sipeed/picoclaw/issues/3125) 中表现出明显的挫败感，指出自信地声称“无结果”比明确的错误更令用户困惑。这表明架构变更需要配合更完善的迁移指南或 Beta 发布通道。
  - **协议兼容性 Gap**：`weissfl` 在 [#3044](https://github.com/sipeed/picoclaw/issues/3044) 中提及“使用标准格式的 Matrix 账号却无法通过 Allow List”，这暴露了 PicoClaw 在遵循主流平台协议标准上的短板。

- **亮点与社区力量**：
  - **专家级贡献**：`carlosprados` 同时提交了高质量的 Bug 报告 ([#3041](https://github.com/sipeed/picoclaw/issues/3041)) 和基础设施级框架代码 ([#3120](https://github.com/sipeed/picoclaw/pull/3120))；`lc6464` 展现了卓越的安全思维 ([#3126](https://github.com/sipeed/picoclaw/pull/3126))。项目核心贡献者群体质量非常高。

---

## 8. 待处理积压

- **需维护者紧急响应**：
  - [#3125](https://github.com/sipeed/picoclaw/issues/3125) **Brave 搜索失效**（新报，严重，影响面广）。
  - [#3041](https://github.com/sipeed/picoclaw/issues/3041) **`mcp add` 解析错误**（严重，已停滞 8 天）。

- **待审核的成熟功能 PR**：
  - [#2975](https://github.com/sipeed/picoclaw/pull/2975) **Telegram 回复提及**（功能完整，合并冲突风险随时间增加）。
  - [#3118](https://github.com/sipeed/picoclaw/pull/3118) **Agent 远程模式**（路线图价值极高，建议积极 Review）。

- **未激活的模块缺陷**：
  - [#3090](https://github.com/sipeed/picoclaw/issues/3090) **Safari 面板兼容**（移动端关键体验）。
  - [#3044](https://github.com/sipeed/picoclaw/issues/3044) **Matrix 用户 ID 过滤失效**（协议合规性缺陷）。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-15

**数据源**: GitHub (github.com/qwibitai/nanoclaw)  
**分析时段**: 过去 24 小时 (2026-06-14 至 2026-06-15)  
**分析师**: AI 智能体与个人 AI 助手领域开源项目分析师

---

## 1. 今日速览

项目当前处于**高速迭代与安全审计并行的关键阶段**。过去 24 小时活跃度极高：共处理 7 条 Issue 与 10 个 PR，无新版本发布。外部安全研究员 YLChen-007 连续提交 3 个严重安全漏洞（#2760、#2761、#2762），直指 NanoClaw 的审批流、文件读写与本地网关认证机制，对项目安全模型构成直接挑战。与此同时，核心团队保持高输出节奏，完成了 Operator 驱动的 Provider 选择、Codex v2 集成、容器工具链数据化三大架构级功能合入，并提交了预算耗尽静默丢包的修复补丁（#2759）。整体而言，项目健康度呈"双轨并行"态势——功能成熟度快速提升，安全面亟需快速加固。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合入的重大功能与修复：

- **PR #2756** — `feat(providers): operator-driven provider selection, switching, and memory migration`（omri-maya，已合并）  
  将提供商（Provider）从隐式绑定变为 Operator 可显式选择、切换的顶层属性，同时构建了 Provider 注册表、安装器、Vault 认证引导与内存迁移技能。这是 NanoClaw 架构的重要里程碑，为后续多 Provider 协作与故障切换奠定基础。

- **PR #2757** — `feat(codex): Codex agent-provider payload v2`（omri-maya，已合并）  
  Codex 正式成为完整的 Agent Provider，运行在宿主能力切面上，并通过 OneCLI 进行保险库限定认证。Codex 集成的技术债务就此结清。

- **PR #2758** — `feat(container): data-drive global CLI installs from cli-tools.json`（gavrielc，已合并）  
  将 Dockerfile 中硬编码的 `claude-code`、`agent-browser`、`vercel` 等 CLI 工具安装迁移至数据驱动的清单文件 `cli-tools.json`。Skill 开发者仅需向 JSON 添加一行即可声明依赖，大幅降低容器维护成本。

- **PR #2764** — `docs(CLAUDE.md): fix two relocated Key Files paths`（glifocat，已合并）  
  修复了文档中两个因文件迁移失效的路径引用，提升 AI 编码辅助工具的扫描准确性。

- **PR #2769** — `docs(add-codex): flag interactive auth step + add host-restart step`（Koshkoshinsk，已合并）  
  补充了 `/add-codex` 技能交互式认证步骤与重启提示，防止 Agent 在无 TTY 环境下执行操作时挂起。

---

## 4. 社区热点

今日社区讨论的核心议题围绕**安全性**与**自治 Agent 可靠性**展开：

| 议题 | 作者 | 类型 | 热度信号 |
|------|------|------|----------|
| **#2760、#2761、#2762** 安全漏洞三连击 | YLChen-007 | Issue | 零评论但有极高潜在影响，暴露审批流与文件处理根本缺陷 |
| **#2751** 预算耗尽无响应 | assapin | Issue | 引起广泛共鸣（用户得不到回复），PR #2759 已快速响应 |
| **#2768** Claude Prompt Caching 默认关闭 | galmorduku | Issue | 指向长期成本效率痛点，对大 prompt Agent 用户影响显著 |

**分析**：YLChen-007 提交的三个安全 Issue 精准命中了 AI Agent 自治场景下的信任根基——审批流可见性（#2762）、回环链路认证（#2761）、文件读取作用域（#2760）。结合 assapin 报告的"静默丢包"问题，社区当前的深层诉求是：**Agent 在执行敏感操作和遭遇资源边界时，必须向用户提供完整、可信、不遗漏的回显与确认机制。**

---

## 5. Bug 与稳定性

### ⚠️ 严重 — 安全漏洞

| ID | 标题 | 影响 | 修复状态 |
|----|------|------|----------|
| #2762 | `add_mcp_server` 审批流隐藏 `args` 和 `env` | 恶意 Agent 可在用户不知情的情况下配置受控 MCP 工具参数与环境变量，绕过审批意图 | 待处理（零评论） |
| #2761 | 本地网关审批绕过（未认证 loopback webhook） | 本机无认证攻击者可伪造事件绕过审批流直接提交 | 待处理（零评论） |
| #2760 | `send_file` 绝对路径任意文件读取 | Agent 可读取系统任意文件并通过出站发件箱外泄 | 待处理（零评论） |

### 🔴 高 — 功能缺陷

| ID | 标题 | 影响 | 修复状态 |
|----|------|------|----------|
| #2751 | 预算耗尽静默丢包 | 用户请求被静默丢弃，无任何反馈，自治体验断裂 | **PR #2759 已提交，待合入** |
| #2770 | Codex 图片文件未传递到聊天 | 图片生成完成但卡在 ProviderEvent 中，用户不可见 | **PR #2770 已提交，待合入** |

### 🟡 中 — 效率与兼容性

| ID | 标题 | 影响 | 修复状态 |
|----|------|------|----------|
| #2768 | Claude Provider 默认关闭 Prompt Caching | 每次轮次系统提示完整发送，Token 消耗超预期 | 待处理 |
| #2767 | Telegram Markdown 解析适配 | 老版 sanitizer 与上游 `@chat-adapter/telegram@4.30.0` 原生 MarkdownV2 支持冲突 | 待处理 |

### 🟢 低 — 文档/配置

| ID | 标题 | 影响 | 修复状态 |
|----|------|------|----------|
| #2763 | CLAUDE.md Key Files 路径失效 | AI 编码助手或开发者跳转至不存在的路径 | **PR #2764 已合入修复** |

---

## 6. 功能请求与路线图信号

- **🔮 多 Provider 策略成为路线图核心方向**  
  PR #2756 的合入是社区对于"自由选择与切换 AI Provider"的长期呼声的正式落地。未来路线图将围绕该能力延伸出 Provider 智能路由、故障切换和按任务成本优化策略。根据 `feat(providers)` 系列 PR 的密度，该能力可能成为 v2.0 的旗舰功能。

- **🔮 格式/风格控制的显式化需求浮现**  
  PR #2765（providers）与 #2766（channels）相继提交 `.format-lint-off` 支持请求，反映出在自动代码生成场景下，高阶用户对 Provider 和 Channel 端代码格式输出有严格的个性化控制需求。该项目有可能在下一版本引入细粒度的格式化配置项。

- **🔮 安全审计与加固将常态化**  
  本期连续出现多份安全审计结果（#2732 健康审计、#2760-#2762 安全漏洞），且报告方来自不同贡献者。预计项目组将加快推动安全最佳实践文档编写、审批流 UI 强化，并可能引入沙箱化文件访问机制。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 与 PR 评论中可提炼出以下核心用户声音：

### 核心痛点：静默失败

> "When an LLM turn exhausts its token / spend budget … the agent-runner currently drops it silently: the user gets no reply."  
> — **assapin** (#2751)

用户对自治 Agent 的"静默失败"容忍度最低。无论是预算耗尽、文件传递失败还是认证挂起，没有反馈的失败比失败本身更破坏信任。PR #2759（传递预算错误回显）与 PR #2770（修复 Codex 图片传递）均直接响应了这类诉求。

### 成本敏感度持续走高

> "The Anthropic Agent SDK defaults this to false for agent sessions, so every turn re-sends the full system prompt uncached."  
> — **galmorduku** (#2768)

对于运行大 System Prompt Agent 的用户，Prompt Caching 默认关闭意味着显著的超额 Token 消耗。社区开始关注基建层默认配置对运营成本的连带影响。

### 文档即产品

> "A reader (or an AI coding assistant) following the table opens a nonexistent path and has to go hunting."  
> — **glifocat** (#2763)

用户将 CLAUDE.md 文档视为 AI 编码助手的知识入口，文档路径的准确性直接影响开发效率。该 Issue 当日提交、当日修复，说明了项目组在这方面的高响应度。

---

## 8. 待处理积压

以下为需维护者优先关注的长期未响应或潜在阻塞的 Issue/PR：

| ID | 标题 | 积压天数 | 风险等级 | 原因 |
|----|------|----------|----------|------|
| #2732 | Harden host + agent-runner from health audit findings | 4 天（创建 06-11） | 🔴 高 | 大规模核心加固 PR（1 commit，19 files），与新提交的 #2760-#2762 安全漏洞在修复域上可能重叠或冲突，需尽快拉齐评审基线 |
| #2760 | 任意文件读取（`send_file` 绝对路径） | <1 天 | 🔴 高 | 零评论、零 Assignee，攻击向量明确 |
| #2761 | 本地网关审批绕过 | <1 天 | 🔴 高 | 零评论，直接影响权限模型 |
| #2762 | `add_mcp_server` 隐藏参数绕过 | <1 天 | 🔴 高 | 零评论，涉及 MCP 审批可信根基 |
| #2751 | 预算耗尽丢包 | 3 天（创建 06-12） | 🟡 中 | PR #2759 已提交，待 Reviewer 终审合入 |
| #2767 | Telegram Markdown 兼容性 | <1 天 | 🟡 中 | 涉及上游依赖更新，需确认是否阻塞 channels 分支 PR |

**维护者行动建议**：
1. 立即对 #2760、#2761、#2762 进行漏洞确认、分配标签与 Assignee，并考虑启动临时安全公告流程。
2. 将 #2732 的修正域与 #2760-#2762 进行冲突扫描，避免两路修复产生回归。
3. 优先合入 #2759（预算回显），这是当前用户感知最直接的可靠性缺口。

---

*报告生成时间: 2026-06-15 | 数据截止: 2026-06-15 00:00 UTC*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw 项目动态日报 (2026-06-15)**

---

### 1. 今日速览

过去 24 小时内，项目仅收到 1 个新的功能请求 Issue，无 Pull Request 合并或更新，无新版本发布。整体活跃度较低，社区贡献节奏平缓。唯一动态展示了用户对 Azure OpenAI 集成能力的持续需求，但尚未引发讨论或维护者响应。项目代码库保持稳定，未见功能推进或修复活动，健康度处于“稳定但需关注”状态。

---

### 2. 版本发布

无（今日未发布新版本）。

---

### 3. 项目进展

- 今日无 PR 被合并或关闭，代码库未引入新变更，核心功能无可见推进。

---

### 4. 社区热点

- **#955 [enhancement] Identity based authentication support for Azure OpenAI LLM Provider**  
  这是今日唯一新开 Issue，虽然暂无评论，但其内容反映了用户在企业级 Azure 场景下的迫切需求：由于订阅安全策略禁止使用 API 密钥，用户希望支持基于 Azure 托管标识（`DefaultTokenCredential`）的认证方式。该请求可能吸引更多受同类限制的用户关注，成为社区近期讨论的潜在焦点。  
  [查看 Issue](https://github.com/nullclaw/nullclaw/issues/955)

---

### 5. Bug 与稳定性

- 今日未报告任何 Bug、崩溃或回归问题。项目稳定性未受新挑战，但可能因活动较少而缺乏充分验证。

---

### 6. 功能请求与路线图信号

- **#955** 提出了明确的增强需求：为 Azure OpenAI LLM Provider 增加“基于身份的认证”支持，允许使用 `az login` 产生的开发人员凭据 (`DefaultTokenCredential`)。  
  这属于安全性与合规性相关的关键特性，若被采纳，将直接影响使用 Azure OpenAI 的企业用户体验。目前无维护者回复，需结合项目路线图判断是否纳入下一版本。  
  [查看 Issue](https://github.com/nullclaw/nullclaw/issues/955)

---

### 7. 用户反馈摘要

- 由于今日无 Issue 评论或 PR 讨论，无法提炼真实用户反馈。但从 Issue #955 的描述可知，用户正在受到 Azure 订阅安全策略的限制（无法使用 API 密钥），从而提出托管认证的方案——这是典型的企业级使用痛点，表明 NullClaw 的用户群体中存在生产环境部署需求。

---

### 8. 待处理积压

- 今日无长期未响应的历史 Issue 或 PR。新建 Issue #955 尚处于未分配、未标注状态，建议维护者尽快添加标签（如 `enhancement`、`question`）并初步回应，以避免需求冷却。  
  [查看 Issue](https://github.com/nullclaw/nullclaw/issues/955)

---

*本日报基于 2026-06-15 UTC 数据自动生成，仅反映当日公开活动。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-15

## 1. 今日速览
过去 24 小时，IronClaw 项目处于高强度迭代状态，共计 **42 条 Issues** 与 **45 条 PRs** 发生更新（其中 15 条 PR 已完成合入/关闭）。核心战场明确聚焦于 **Reborn 新架构的安全加固** 与 **用户体验精细化**：附件上传管道正式合入 SPA（#4738），同时社区研究员一次性批量提交了 4 个 shell 工具审批绕过漏洞。项目组同步启动了"用 IronClaw 开发 IronClaw"的 AI 原生效能提升计划（#4878）。整体来看，功能推进、安全审计、基础设施自举三条线并行，**项目健康度优秀**。

## 3. 项目进展

### 🚀 里程碑合并 / 关闭
- **附件管道落库**：PR #4738 (`feat(reborn): attachment web UX on the WebChat v2 SPA`) 正式合入，填补了 Reborn 前端附件上传-组装的核心空白。
- **运行时上下文增强**：PR #4836 (`feat(runtime-context): surface connected channels, delivery state, and run origin`) 合入，模型现可感知已连接频道与下发目标。
- **测试基座修复**：PR #4873 (`test(slack): re-home approval→auth→final-reply delivery e2e`) 关闭，修复了 Slack 审批-认证-回复全链路 E2E 测试。

### 🔧 当前积极推进的修复 / 功能
- **审批边界优化**：PR #4835（移除 thread_id 作用域，跨线程持久化）、#4840（凭据缺失前置检测）、#4838（忙碌线程显式拒绝代替暗等）。
- **模型应答增强**：PR #4837（空转/预算耗尽时 Gated 提示）、PR #4871（图片附件多模态支持，紧接 #4644）。
- **日常修复**：PR #4889（取消运行后关闭工具 Activity）、PR #4888（GitHub Issue 列表过滤 PR）。

---

## 4. 社区热点

### 🔥 Shell 工具审批绕过（Critical，4 条）
研究员 `YLChen-007` 集中提交四份详细安全公告：
- `sort --compress-program` 代理执行（#4862）
- `env /bin/sh -c` 透明包装（#4863）
- 继承先前自动批准的高危命令（#4864）
- 包装器绕过审批下限（#4865）

**深层诉求**：说明当前 shell 工具的权限分类完全依赖前缀匹配，社区正在推动更严格的沙箱或指令拦截层。

### 🔥 Reborn 扩展安装引导碎片化
`sunglow666` 发布了系列用户体验反馈：
- 安装后提示 "AUTH NEEDED" 但无下一步引导（#4886）
- 扩展安装-配置-授权流程断裂，用户需手动摸索（#4890）
- Google Calendar 对话中直接弹出 access token 而非 OAuth 流程（#4884）

**深层诉求**：扩展生态是 Reborn 的命脉，社区强烈要求一个统一的"安装 → 授权 → 可用"引导管线。

### 🔥 工程效能自举计划
`think-in-universe` 提交 #4878 系列，意图用 IronClaw 自身完成：
- AI 代码审查与评论闭环（#4880）
- 预热部署 Vercel 体验（#4881）
- Cloud Coding Agent 自动产出 PR（#4882）
- 测试覆盖率防退化（#4883）

**深层诉求**：团队试图从单一"模型 Agent 开源项目"进化为 **AI-Native 工程组织**。

---

## 5. Bug 与稳定性

### 🔴 严重（Critical）
| Issue | 摘要 | 修复 PR |
|---|---|---|
| #4862–#4865 | Shell 工具审批绕过（前缀匹配盲区） | 暂无关联 PR |
| #4887 | MCP 能力批准后 `input_ref` 跨作用域失败 | 暂无，待 CodeRabbit 鉴别 |

### 🟠 高（High）
| Issue | 摘要 | 修复 PR |
|---|---|---|
| #4872 | 外部频道标签渲染为指令文本（Prompt 注入风险） | 无 |
| #4870 | WebSocket 鉴权冲突（query-token 被后端拒绝） | 无 |
| #4874 | 非 localhost HTTP 访问报 `Illegal invocation` | 无 |
| #4751 | 大响应请求触发 Provider 参数超限（已关闭） | 无 |

### 🟡 中（Medium）
| Issue | 摘要 | 修复 PR |
|---|---|---|
| #4868 | 移动端配置 Action 按钮被截断 | 无 |
| #4867 | GitHub 分析任务降级为原生 HTTP 工具 | 无 |
| #4852 | Shell 命令在审批弹窗/Activity 中完全不可见 | 无 |
| #4848 (closed) | 认证恢复路径匹配修复 | 已在 `crates/ironclaw_agent_loop` 修复 |

---

## 6. 功能请求与路线图信号

### 🧠 自举开发（Strong Signal）
#4878 系列（AI Review / Preview Deployments / Cloud Agent）是迄今为止最强的**路线图信号**——IronClaw 要将自身变为 AI 原生开发的最佳实践案例。

### 🔗 外设统一化
- **PR #4778**：将 Slack 重构为标准 ProductAdapter Extension。预示所有 Channel 连接器（WeChat、Discord）都将被插件化。
- **#4875**：计划拆分 1025 行的 `runtime_context.rs`。大规模模块化重构迫在眉睫。

### 🧪 可观测性 & 基准测试
- **PR #4588**（Trajectory Observer + LLM Provider Injection）持续推进，大量代码注释和设计文档表明 **nearai-bench** 的外部驱动需求是下一阶段重点。

### 📦 版本发布（Blocked）
**PR #3708**（`chore: release`）已从 5 月 16 日悬而未决至今，涉及 `ironclaw_common 0.5.0` 和 `ironclaw 0.29.1` 的 Breaking Changes。社区期待解封。

---

## 7. 用户反馈摘要

| 反馈维度 | 原文 / 场景提炼 | 来源 |
|---|---|---|
| **引导缺失（痛点）** | "Installed extensions provide limited guidance for required post-install setup" | #4886 |
| **对话透明性（信任）** | "Shell command is not visible in approval dialog. User sees 'Capability: builtin.shell' but not the actual command." | #4852 |
| **能力路由（困惑）** | "GitHub analysis may bypass GitHub Extension and fall back to builtin.http" | #4867 |
| **环境兼容性（短板）** | "WebChat v2 fails with 'Illegal invocation' over plain HTTP from non-localhost" | #4874 |
| **安全信任（积极信号）** | 研究员按漏洞标准格式详细提交 4 个 shell bypass，社区反馈质量极高 | #4862-4865 |
| **Dogfooding（内部压力）** | "Local startup, config, provider setup usability problems" | #4879, #4692 |

---

## 8. 待处理积压

### ⏳ 长周期悬停
- **PR #3708**（`chore: release`）：**最关键的阻塞项**。5 月 16 日开启，已超 30 天未合入。断崖式拖延会阻止下游用户锁定版本。
- **PR #4002**（Actions deps 16 项更新）：5 月 24 日开启，CI 安全风险累积。
- **PR #4499**（tokio-ecosystem 更新）：6 月 5 日开启，存在语义冲突预警。

### ⏳ 待办结构性问题
- **Issue #4644**（通用附件）：虽已推进，但原 Issue 提出的"格式注册表"和四倍重复逻辑尚未落地。
- **PR #4584**（系统 Sentinel ID 重构）：6 月 9 日开启，可能阻塞后续的租户/身份系统变更。

### 👥 备注维护者
- **Issue #4878 / #4879**：这两个源自 `think-in-universe` 的 Dogfooding 自省计划包含了大量可操作的 task 拆分，建议管理层关注资源分配。
- **Issue #4692**（6/08-6/14 的 Dogfooding 报告）：承载的前一周 Local Reborn 纸漏等待正式归类并 assign。

---

*生成时间：2026-06-15 | 数据源：nearai/ironclaw GitHub Datafeed*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报（2026-06-15）

## 今日速览

过去 24 小时项目整体活跃度 **中等**，共 2 个历史 Issues 被更新（均被标记 stale），5 个 PR 中有 2 个被合并/关闭。功能方面，Doc/Office 文档 Artifact 分享与预览优化（#2159）已合入主分支，同时一个长期存在的“幽灵会话” Bug 得到修复（#1465）。其余 3 个功能型 PR（会话内搜索、防休眠、运行计时器）仍处于停滞状态，已沦为 stale，需维护者推进 review 或更新。项目在持续迭代新功能的同时，技术债务清理（stale 标记）也在进行中，社区沟通活跃度偏低。

## 版本发布

无新版本发布。

## 项目进展

今日合并/关闭的重要 PR 涉及功能增强与可靠性修复：

- **#2159 (merged) – feat(artifacts): 支持文档 Artifact 分享与预览优化**  
  作者 liugang519，今日提交并合并。新增对 DOCX、PPTX、XLSX、PDF、CSV、TSV 等文档类型的 Artifact 分享与预览能力；优化了 DOCX 分页、PDF 原生预览兜底、表格自动列宽/换行渲染；补充 pdfjs 字体与 cMap 资源，调整 CSP 策略以支持 blob 预览。标志着 LobsterAI 在文档协作预览能力上迈出了实质性一步。  
  https://github.com/netease-youdao/LobsterAI/pull/2159

- **#1465 (closed) – fix(scheduled-tasks): 已删除定时任务重启后作为幽灵会话重新出现**  
  作者 linlihua，关联 Issue #1359。根因是删除定时任务时未清理本地 SQLite 中的关联会话记录。修复后彻底消除了“删除后重启又出现”的幽灵会话问题，提升了定时任务模块的可靠性。  
  https://github.com/netease-youdao/LobsterAI/pull/1465

## 社区热点

目前 Issues 和 PR 评论区均未产生高热度讨论（评论数 0–1，所有反应 👍 均为 0）。相对值得关注的为用户 xuzx-code 反馈的两个 UI 体验问题：

- **#1434**：在 Agent 技能页搜索无数据时，系统语言设置为中文但仍展示英文提示及英文按钮，本地化不完备。  
- **#1435**：新建自定义 Agent 时，名称过长导致超出弹框边界，展示不友好。

这两个 Issue 虽然创建于 4 月初，但于昨日被自动标记为 **stale**，可能因长期无更新。它们反映了新手用户在本地化与 UI 适配上的典型痛点，但维护者尚未给出明确回应。  
https://github.com/netease-youdao/LobsterAI/issues/1434  
https://github.com/netease-youdao/LobsterAI/issues/1435

## Bug 与稳定性

| 严重程度 | Bug 描述 | 状态 |
|----------|----------|------|
| 中 | **定时任务删除后幽灵会话重现** | **已修复**（#1465 已合并） |
| 低 | **Agent 技能页搜索无数据显示英文** | 未修复，Issue #1434，stale |
| 低 | **Agent 名称过长导致 UI 溢出** | 未修复，Issue #1435，stale |

无新增 Bug 报告。幽灵会话的修复消除了一个影响定时任务可靠性的中等严重度问题。其余两项 UI 问题虽不严重，但影响国际化和基础交互体验，建议在后续版本中优先解决。

## 功能请求与路线图信号

三个社区提交的功能 PR 目前均处于 **open + stale** 状态（自 4 月 3 日以来未获有效 review 或更新），具体包括：

- **#1429 – feat(cowork): 会话内消息搜索（mark.js 高亮）**  
  提供 `Cmd/Ctrl+F` 搜索、实时高亮与跳转，提升长会话的信息检索效率。  
- **#1430 – feat(cowork): 会话运行期间自动阻止系统休眠**  
  利用 Electron `powerSaveBlocker` 防止长时间任务因系统挂起中断，对可靠性有明确价值。  
- **#1431 – feat(cowork): StreamingActivityBar 右侧显示运行计时器**  
  增加实时运行时长显示，帮助用户感知进度，功能成熟度较高。

这三个功能涵盖了 AI Agent 会话体验的重要增强方向，代码改动清晰，如果纳入下一版本，将显著提升用户对长时间任务的掌控感与可靠性。建议维护团队尽快评估并推进合入。

## 用户反馈摘要

从现有 Issue 评论中可归纳出较为集中的用户诉求：

- **本地化不全**：用户在中文界面下仍看到英文提示和按钮，表明系统国际化覆盖不足，对非英文用户造成困扰（#1434）。
- **UI 细节缺乏打磨**：弹框输入框未对超长文本做截断或换行处理，直接破坏布局（#1435），反映出前端边界情况处理不够严格。

未发现对已发布功能的“满意”或积极评论，整体用户反馈信号偏弱。

## 待处理积压

以下高价值但长期未获响应的 PR/Issue 值得维护者重点关注：

| 编号 | 类型 | 说明 | 停滞时间 |
|------|------|------|----------|
| #1429 | PR | 会话内搜索功能，至今未 review | 73 天（stale） |
| #1430 | PR | 阻止系统休眠，提升任务可靠性 | 73 天（stale） |
| #1431 | PR | 会话运行计时器，体验提升 | 73 天（stale） |
| #1434 | Issue | 本地化文案错误，新手易感知 | 73 天（stale） |
| #1435 | Issue | 输入框溢出，UI 错误 | 73 天（stale） |

建议维护者在下一次迭代前集中评估这批 PR 的可合并性，并对上述两个 Issue 给出至少初步回应（确认 / 分配 / 关闭），以避免社区贡献者的积极性下降。

---

*报告生成时间：2026-06-15 · 数据来源：LobsterAI (netease-youdao/LobsterAI) GitHub*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-06-15

---

## 1. 今日速览
过去 24 小时内，Moltis 项目进入了短暂的静默期。未发布新版本，无 Pull Request 合并或关闭，仅产生 1 条新的功能请求 Issue。整体活跃度较低，但核心维护稳定。唯一的新动态聚焦于极端边缘场景下的压缩后端优化，这反映了社区对 Moltis 轻量化部署路径的关注仍在延续。项目健康度保持稳定，开发节奏暂时放缓。

---

## 2. 版本发布
无新版本发布。

---

## 3. 项目进展
今日无 Pull Request 被合并或关闭，主线代码未发生任何变更。无新功能落地或重要修复整合进入主分支，项目开发进度处于暂停状态。

---

## 4. 社区热点
### [Issue #1123] 提议添加纯 Rust 的 turbovec 内存后端
- **链接**：[moltis-org/moltis Issue #1123](https://github.com/moltis-org/moltis/issues/1123)
- **分析**：这是今日社区唯一的活跃信号。尽管该 Issue 尚未收到评论或表态（0 评论、0 表情），但其议题定位十分明确——为“极端边缘压缩”场景提供一个纯 Rust 的内存后端替代方案。提出者希望通过引入 `turbovec` 来：
  1. 彻底消除对 C 语言链接库的编译依赖。
  2. 在极低内存的设备上实现更高效的向量压缩。
  
  这强烈暗示着一部分 Moltis 用户正在尝试将其智能体运行时推向嵌入式 MCU 或传感器级的硬件平台。

---

## 5. Bug 与稳定性
今日未报告任何新的 Bug、崩溃或回归问题。项目目前暂无明显稳定性风险，无需紧急修复介入。

---

## 6. 功能请求与路线图信号
### 核心信号：向“极致边缘”迈进的诉求
- **依据**：Issue #1123 是目前唯一的路线图信号。它明确要求 Moltis 提供针对资源受限设备的专用内存后端。
- **研判**：`turbovec` 作为新兴的纯 Rust 压缩库，如果被采纳，将显著降低 Moltis 在无标准库环境（`no_std`）或极小内存设备上的适配门槛。该提案目前虽独立，但与当前 AI Agent 向端侧下沉的行业浪潮高度契合，具备被纳入下一版本规划的潜力。建议维护者关注该方向是否有原型代码或 PoC 跟进。

---

## 7. 用户反馈摘要
今日几乎没有来自社区评论区的深度用户讨论。无日常使用吐槽，也无新 Bug 确认反馈。唯一的新 Input 来自 Issue #1123 的创建者（`joeblew999`），其诉求风格偏向于**前瞻性的架构提议**，而非对现有问题的抱怨。项目用户群体当前整体情绪安静，缺少围绕具体功能的使用交流。

---

## 8. 待处理积压
今日未关闭任何旧 Issue，净积压量 **+1**（新增 1 条）。
- **提醒维护者关注**：虽然根据提供的数据无法定位具体哪些旧 Issue 长期未响应，但 **Issue #1123** 具备较高的架构讨论价值。此类涉及引入新后端的大提案，如果长时间无人回复，容易快速冷却并积压。建议核心维护者尽早给予初步反馈（例如初步技术评估或标记为 `under-discussion`），以维持社区的提案积极性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我为您生成了 2026-06-15 的 CoPaw 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-06-15

## 1. 今日速览
`v1.1.11.post2` 版本的回归问题成为今日社区焦点，Windows 桌面端 CMD 弹窗循环、本地模型提供商消失及 Gemini 工具调用故障引发了大量用户反馈。项目在 24 小时内处理了 24 条 Issue 和 16 个 PR，尽管合并率表现稳健，但待合并 PR （11 个）积压表明核心维护工作量压力巨大。值得肯定的是，首次贡献者活跃度很高，多位社区成员提交了越南语翻译及多项 Bug 修复，呈现出社区共建的健康生态。**整体活跃度：极高，项目处于高强度迭代与碎片化 Bug 修复的并行期。**

## 2. 版本发布
- **无新版本发布**。当前最新版本为 `v1.1.11.post2`，该版本在社区中反馈的回归问题较多。

## 3. 项目进展
今日共有 **5 个 PR** 被合并/关闭，主要聚焦于桌面端遗留问题修复与插件扩展能力的增强。

- **关键修复落地：** PR [#5051](agentscope-ai/QwenPaw/pull/5051)（桌面端端口持久化）被合并，解决了 Windows 桌面版重启后无法记住上次使用的智能体及会话的长期痛点。这是对 Issue [#4733](agentscope-ai/QwenPaw/issues/4733) 迟来的修复。
- **插件 SDK 扩展：** PR [#5188](agentscope-ai/QwenPaw/pull/5188)（请求负载转换钩子）被合并，向宿主 SDK 中注入了请求载荷转换能力（`window.QwenPaw.chat.requestPayload.add`），允许插件在消息发送前拦截并修改请求，极大增强了中间件生态的扩展性。
- **稳定性维护：** PR [#5035](agentscope-ai/QwenPaw/pull/5035) 修复了 llama.cpp 版本号解析的固定宽度切片 Bug；PR [#5038](agentscope-ai/QwenPaw/pull/5038) 修复了 `LightContextManager` 在空消息列表下的崩溃问题。
- **回滚操作：** PR [#5092](agentscope-ai/QwenPaw/pull/5092) 被关闭，回退了此前关于 Discord 打包编译的修复（#5084）。

## 4. 社区热点
- **🔥 Gemini 工具调用回归（#5163）：** 用户确认 `v1.1.11.post2` 版本破坏了 Gemini 模型的工具调用能力，这在 `v1.1.10` 版本中是正常的。截至本报告发布尚无修复 PR。
- **🔥 CMD 弹窗无限循环（#5181）：** `v1.1.11.post2` 版本中，由于插件依赖安装失败时未隐藏 CMD 窗口，导致 PyPI 连接异常时会弹出无限循环的 cmd 窗口，严重影响了 Windows 用户的使用体验。
- **🔥 企业微信审批不可见（#5190）：** 开启私聊访问控制后，用户端只能看到无权限提示，但在 Web 控制台和企业微信端均找不到审批入口，这对企业级用户是严重的阻断性 Bug。
- **🔥 飞书流式卡片长回复卡顿（#5167）：** 用户反馈长回复场景下，飞书 CardKit 流式卡片刷新极慢，体验甚至不如非流式分段更新，影响了该功能在飞书生态中的可用性。

## 5. Bug 与稳定性
| 严重程度 | Issue | 描述 | 状态/修复 PR |
|---|---|---|---|
| **紧急** | [#5181](agentscope-ai/QwenPaw/issues/5181) | `v1.1.11.post2` 插件依赖安装失败引发 CMD 窗口循环弹窗 | 暂无修复 |
| **紧急** | [#5184](agentscope-ai/QwenPaw/issues/5184) | `v1.1.11.post2` 本地模型提供商在前端不可见 | 暂无修复 |
| **紧急** | [#5163](agentscope-ai/QwenPaw/issues/5163) | `v1.1.11.post2` Gemini 工具调用回归，首次观察到较严重的跨版本兼容性倒退 | 暂无修复 |
| **高** | [#5190](agentscope-ai/QwenPaw/issues/5190) | 企业微信私聊审批界面缺失 | 暂无修复 |
| **高** | [#5161](agentscope-ai/QwenPaw/issues/5161) | 长对话后 QwenPaw 无响应，上下文过长导致服务卡顿 | 暂无修复 |
| **高** | [#5162](agentscope-ai/QwenPaw/issues/5162) | 对话思考逻辑进入死循环 | 暂无修复 |
| **中** | [#5171](agentscope-ai/QwenPaw/issues/5171) | 上下文压缩有时会将保留阈值设为 0，导致信息完全丢失 | 暂无修复 |
| **中** | [#5177](agentscope-ai/QwenPaw/issues/5177) | 钉钉 Channel 消息无法在前端 Console 会话列表中显示 | 暂无修复 |
| **低** | [#5145](agentscope-ai/QwenPaw/issues/5145) | 执行详情应折叠但持续展开，干扰用户阅读 | 已关闭 |

## 6. 功能请求与路线图信号
- **即将到来的重磅功能：**
    - **计算机操控（Computer Use）：** PR [#5187](agentscope-ai/QwenPaw/pull/5187) 为 Windows 桌面端添加了 UIA + Tauri 控制模式的 GUI 自动化能力，是朝着 Agent 智能化操作迈出的重要一步。
    - **数据分析插件（DataPaw）：** PR [#4622](agentscope-ai/QwenPaw/pull/4622) 带来包含 12 种 BI 技能的深度数据分析插件，已在审查中 24 天。
    - **PRD 管理工具：** PR [#4902](agentscope-ai/QwenPaw/pull/4902) 将插件化的 PRD 管理能力内建化。
- **社区呼声较高的需求：**
    - **代码高亮（#5191）：** Coding 重度用户的核心诉求，认为当前代码区无高亮、无补全非常影响效率。
    - **国际化支持（#5168, #5186）：** 越南语完整翻译（#5186）和 Zalo Bot 频道支持（#5168）标志着 CoPaw 正在向东南亚市场渗透。
    - **统一模型配置（#5182）：** 社区希望向量模型、文本模型、音视频模型在配置端实现统一，降低使用门槛。
- **自动化增强：** 针对 Cron/心跳 Agent 的超时和上下文缺失问题，PR [#5180](agentscope-ai/QwenPaw/pull/5180) 和 PR [#5179](agentscope-ai/QwenPaw/pull/5179) 正在尝试增强，表明 Agent 自主协作与自动化是当前路线图的重点。

## 7. 用户反馈摘要
- **[抱怨] 版本质量波动：** 多位用户对 `v1.1.11.post2` 版本的稳定性表达了失望。“自从升级到 `post2` 之后什么都不能用了” (CMD 弹窗回滚，Gemini 回退)；
- **[企业场景痛点] 渠道体验不成熟：** 企业微信用户反馈“申请审批工单无处可见”是极其困惑的体验。飞书用户表示“长回复场景下刷新较慢，体感上已经影响可用性”。钉钉用户则无法在后台看到私聊会话；
- **[肯定与期待] 生态建设受认可：** 用户对 CoPaw 的插件生态抱有高度期待，在建议中多次表达“感谢你们一直在维护这个项目”，并希望尽快接入 kimi-for-coding 和 uv 等工具链；
- **[高级 Agent 用户困境] 上下文管理问题：** 上下文压缩导致 0 保留、长对话卡死等 Bug，使得复杂的 Agent 任务无法安全完成，重度用户表达了“任务中断”的严重沮丧感。

## 8. 待处理积压
以下 Issue 或 PR 长期未得到充分响应或修复，建议维护团队重点关注：

- **无修复的回归 Bug：**
    - [#5163](agentscope-ai/QwenPaw/issues/5163) - Gemini 工具调用回归（断档 3 天，无 PR 关联）
    - [#5184](agentscope-ai/QwenPaw/issues/5184) - 本地模型提供商消失（断档 1 天）
    - [#5181](agentscope-ai/QwenPaw/issues/5181) - CMD 弹窗循环（断档 1 天）
- **长时间待合并或审查的 PR：**
    - [#4622](agentscope-ai/QwenPaw/pull/4622) - DataPaw 数据分析插件（审查中 24 天）
    - [#4902](agentscope-ai/QwenPaw/pull/4902) - 内置 PRD CRUD 工具及前端渲染器（审查中 13 天）
    - [#5141](agentscope-ai/QwenPaw/pull/5141) - Tool Card 加载 Spinner 修复（审查中 3 天，登录口状态逻辑优化）
    - [#5187](agentscope-ai/QwenPaw/pull/5187) - Windows 桌面端 Computer Use 功能（功能量大，需严格 Code Review）

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-06-15

**项目分析师**：AI 智能体与个人 AI 助手领域
**数据窗口**：2026-06-14 ~ 2026-06-15

---

## 1. 今日速览

今日 ZeroClaw 项目处于 **"高热"** 活跃状态，社区提交和讨论密度极高，但维护团队的审批吞吐量面临压力。过去 24 小时 **42 条 Issue 更新**中有 28 条被关闭（关闭率 66%），修复效率尚可；然而 **50 条 PR 更新**中高达 **46 条处于打开待合并状态**，形成了显著积压。本周无新版本发布，社区讨论焦点集中在委托代理安全模型、企业级离线和架构治理上。项目正处于 **"功能快速扩张 vs. 稳定化需求迫切"** 的交叉路口。

---

## 2. 版本发布

本日无新版本发布。上一次正式版动态请查阅日前日报。

---

## 3. 项目进展

尽管合并数字不大，但背后积累的大量功能正在推进中，项目整体生态显著扩展。

### 关键修复/功能合并

- **高强度 Bug 修复：** **PR #7664** 已合并/关闭，修复了一个严重阻塞问题——Gateway Web UI 中 `ask_user` 功能提示 "Channel closed before receiving a response" 导致用户审批流程直接中断。关联 Issue #7542 已解决。
- **定时任务管理增强：** **PR #7384** 为 Scheduled Tasks 加入了暂停/恢复（Pause/Resume）功能，基于已有 `enabled` 字段打通了从 Dashboard 到 API 的全链路控制。
- **配置系统重构奠基：** **PR #7594**（类型驱动 alias 选择器）虽然标有 `needs-author-action` 但已关闭，其引入的枚举声明式设计模型将降低未来配置扩展的维护成本。

### 今日新提交的高质量 PR

- **运行时性能优化：** **PR #7667** 重构了 `before_llm_call` Hook，改为传递可变借用，避免了每次 LLM 请求时对完整消息历史的全量克隆——对长对话场景降延迟意义重大。
- **矩阵频道深度集成：** **PR #7661** 恢复了 Matrix 的房间创建和管理能力（创建房间、邀请用户、开关加密），强化了去中心化通讯协议的原生支持。
- **Cron 远程控制扩展：** **PR #7666** 在合并的 #7384 基础上，向 Gateway 的 REST API `CronPatchBody` 增加了 `enabled` 字段，允许通过 HTTP 远程暂停/恢复定时任务。

### 集成生态里程碑

由贡献者 **@theonlyhennygod** 提交的大规模集成工作（Vonage/Sinch/Plivo/Telnyx 四路 SMS 网关、Sonos/Spotify/Shazam/8Sleep/Philips Hue 等智能家居工具、Arcee AI/Inception Labs/Lambda AI 等多家模型提供商）对应的跟踪 Issue 在本日窗口内集中关闭，表明代码已趋稳或已合入主线。**ZeroClaw 作为 "万能 AI 连接器" 的生态版图正在快速变为现实。**

---

## 4. 社区热点

### 🏆 评论最多 Issue

| # | 标题 | 评论 | 热度分析 |
|---|---|---|---|
| **#3642** (CLOSED) | [Feature]: Provide a "full" docker image | **13** | **降低部署门槛**是社区最普遍的显性诉求。多个 Feature 默认关闭以降低内存消耗，但增加了新用户和/or 非技术用户的使用障碍。社区希望有一个开箱即用、内置 WhatsApp 等全部功能的 `full` 标签镜像。 |
| **#6808** (OPEN, RFC) | RFC: Work Lanes, Board Automation, and Label Cleanup | **11** | **治理改革迫在眉睫**。随着贡献量激增，@Audacity88 发起的这份 RFC 提议用自动化泳道和看板维度消化维护压力，标志着社区从"高速增长"向"规范治理"的转型讨论已全面展开。 |
| **#7470** (OPEN, P1) | [Bug]: delegate agentic mode rejects empty allowed_tools | **7** | **多代理协作的边界困境**。用户 vrurg 在搭建"多 Agent 审核/研究"场景时被当前委托权限模型阻塞。这是当下最热门的 Bug，直接关系到 Agent 间编排能力的可靠性。 |
| **#6293** (OPEN, RFC) | RFC: Air-gapped execution mode | **5** | **企业级安全的北极星功能**。提议将项目拆分为"在线 Proxy"和"离线 Agent"双进程，通过 Unix Socket 通信。一旦实现，ZeroClaw 将在端侧安全 Agent 领域建立显著差异化优势。 |
| **#6074** (OPEN) | audit: track 153 commits lost in bulk revert | **2** | **代码完整性警示**。3月份的 153 个提交批量回滚，至今清理工作标记为 `help wanted` 但进展缓慢，是项目健康度的一处暗礁。 |

---

## 5. Bug 与稳定性

### 🔴 S1 - 工作流阻塞 / 严重

| Issue | 严重程度 | 当前状态 | 关联修复 |
|---|---|---|---|
| **#7470**：Delegate agentic mode rejects empty `allowed_tools` 和 same-profile gate blocking | S1 / P1 | `in-progress` | 关联 **PR #7592**（文档说明）和 **PR #7608**（运行时修复，暴露 Deferred MCP 工具给 Delegate）。修复后多 Agent 编排能力即将解锁。 |
| **#5528** (CLOSED) | Email 通道配置逻辑缺陷导致数据丢失 | S0 / P1 | **已关闭/修复** |

### 🟡 S2 - 行为异常 / 退化

| Issue | 问题描述 | 状态 |
|---|---|---|
| **#6856** | v3 架构下频道响应中缺少 `show_tool_calls` 字段， Agent 行为对用户不可见 | `in-progress` |
| **#7549** (PR 已提交) | CLI 安装插件写入 `config.data_dir/plugins`，但运行时扫描 `config.plugins.plugins_dir`，导致 WASM 插件"静默失踪" | 等待合并 |
| **#5662** | QQ 频道语音消息被处理 20+ 次，数据库大量重复 | 失联超 2 月 |

### 🟢 S3 - 边界 / 体验修复（近期大量合并/提交）

项目在 **开发者体验（DX）和国际化（i18n）** 的精细化打磨上力度显著：

- **#7610**：Quickstart 流程遗漏 Webhook 端口设置
- **#7609**：Quickstart 中 Alias 输入未做实时校验
- **#7614**：安装脚本未检测 musl vs gnu libc，aarch64 Linux 用户可能安装错误目标
- **#7612**：zh-CN 语言包滞后源码 28 个 key，已同步
- **#7617**：冗余 TOML 嵌套导致 Provider 配置静默丢失，已增加检测警告

---

## 6. 功能请求与路线图信号

### 🔮 极可能纳入下一版本

| 功能 | 当前状态 | 理由 |
|---|---|---|
| **记忆 "梦境" 模式**（PR #6693） | `size: XL`，`needs-author-action` | 5 阶段记忆巩固引擎（收集→反思→精简→剪枝→报告），是 Agent 长期记忆能力的核心进化，一旦作者回归即可推进。 |
| **Cron 远程暂停/恢复**（PR #7666） | 新提交，延续 #7384 | 从 Dashboard 到 REST API 的 pause/resume 通道打通，补全了定时任务的远程管理能力。 |
| **Deferred MCP 暴露给 Delegate**（PR #7608） | `in-progress` | 与 #7470 + #6136 联动，解禁后 Agent 间可灵活共享延迟加载的 MCP 工具集，是专业多 Agent 系统的关键工程。 |

### 🧭 中期架构愿景信号

- **气隙执行模式（#6293）**：虽然无代码贡献，但被评为 RFC 级别。一旦进入实现阶段，将与 Air-gapped 环境深度绑定，成为企业级 LLM 操作的黄金标准。
- **治理自动化（#6808）**：RFC 本身定义了未来看板、标签和工作流的协作规则，是社区能否持续健康扩容的基础设施级决定。

### 📦 集成生态扩展（用户高频请求）

- 大量新的 SMS 网关、智能家居工具和第三方模型提供商（Inception Labs、Arcee AI、Lambda AI）的 Issue 已关闭，社区对 **"零切换成本接入各种后端"** 的期望正在被兑现。
- **@singlerider** 提出的 **Zerocode ACP Bridge**（#6823）和 **Companion Daemon**（#6293）构成了 ZeroClaw 向平台级 Agent 运行时进化的两大支柱。

---

## 7. 用户反馈摘要

### 👍 正面反馈
> "Best tool out there. Wishing way more stars. Greatly appreciated."
> —— u/MushiTheMoshi (于 #6847，虽遭遇 WhatsApp QR 不显示的 Bug，仍对项目表达了高度认可)

### 👎 核心痛点
1.  **入门体验 vs. 高级功能：** 用户普遍希望官方提供一个 "Full Feature" 的 Docker 镜像，而非依赖编译时 Feature Flag。默认关闭高频功能（WhatsApp、私有 CA 等）给非技术用户设置了门槛（#3642）。
2.  **配置 / 环境复杂：** 邮件通道配置逻辑存在数据丢失风险（#5528）；Nix Flake 输出的是工具链而非 `zeroclaw` 包（#6906），与用户预期差距大；Musl 安装脚本检测缺失（#7614）。
3.  **多 Agent 高级场景受限：** 用户 vrurg 尝试搭建专业化多 Agent 审核流程，但委托权限模型匹配度不足（#7470），反映出当前安全体系尚需针对复杂生产场景做针对性优化。

### 💡 场景落地趋势
- **多 Agent 研究与协同**（#7470）：用户明确希望 AI 智能体之间能灵活委托和共享工具栈。
- **成本控制型推理**：用户社区积极推动小参数、专业化、开源模型的支持（如 Arcee AI 的 Conductor 路由模型、Inception Labs 的扩散式语言模型），体现了对"非 GPT 替代"的需求。

---

## 8. 待处理积压

以下事项建议维护团队优先关注：

### 🔴 积压优先级 1

| 条目 | 类型 | 搁置时长 | 风险 |
|---|---|---|---|
| **PR #5892**：修复 `tool_choice` 与孤立的 `tool_use` | bug / 核心运行时 | 自 4-19 起，标记 `needs-author-action` | 作用于 OpenAI、Bedrock、Azure、OpenRouter 等多 Provider，是**生产中最大的稳定性隐患**。如作者无法继续，建议 Maintainer 接手。 |
| **Issue #6074**：追踪 153 个被回滚的提交 | bug / 代码完整性 | 自 4-24 起，标记 `help wanted` | 涉及丢失的 Bug fix 和 Feature，每周都会增加分化合并的风险。 |

### 🟡 积压优先级 2

| 条目 | 类型 | 建议行动 |
|---|---|---|
| **Issue #5662**：QQ 语音消息重复处理 | 通道稳定性 | 超过 2 个月无进展，影响特定地区用户群体。 |
| **Issue #5842**：`extra_args` 安全白名单验证 | 安全增强 | 尽管 PR #5361 引入了该能力，但针对命令注入的安全验证需尽快完整。 |
| **@theonlyhennygod** 的集成系列 PR 收尾 | 功能版图 | 多个 Provider/Channel Issue 已关闭，对应的代码 PR 应尽快完成最终合并，避免长期挫伤高产能贡献者的积极性。 |

---

> 总结：ZeroClaw 当前处于功能高速扩张期，Docker 开箱体验、多 Agent 委托和安全架构正在成为社区的核心关注点。大量小型修复 PR 展示了项目对工程精品的追求，而 #5892 和 #6074 代表了历史和技术债务的必要清理窗口。整体项目健康度**良好但审查瓶颈显著**。

*数据来源：GitHub zeroclaw-labs/zeroclaw  |  报告生成时间：2026-06-15*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*