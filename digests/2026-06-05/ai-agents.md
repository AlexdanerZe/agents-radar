# OpenClaw 生态日报 2026-06-05

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-05 03:29 UTC

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

好的，这是根据 OpenClaw 项目 2026-06-05 的 GitHub 数据生成的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-05

### 1. 今日速览

项目过去 24 小时内展现出极高的社区活跃度，共更新 500 条 Issue 和 500 个 PR，合并/关闭 PR 达 103 个。然而，项目当前处于“高产出、高风险”的焦灼状态。新版本 2026.6.1 引入了多项严重的破坏性变更，包括 SQLite 迁移静默清空 Cron 数据、OpenAI ChatGPT 传输层完全故障等，导致用户信任度短期承压。尽管维护团队已针对部分回归问题提交了修复 PR，但整体 Bug 堆积速度依然很快，无新版本发布。

### 2. 版本发布

无新版本发布。上一个稳定版 `2026.6.1` 带来的回归问题仍是今日社区讨论的绝对焦点。

### 3. 项目进展

今日项目在修复关键 Bug 和推进功能落地方面有实质性进展，多个高优先级 PR 已进入待合并状态：

- **Provider 兼容性修复**：
  - **PR #90399** ([链接](https://github.com/openclaw/openclaw/pull/90399)) 修复了 OpenAI ChatGPT OAuth 流返回空 `content-type` 头时被误判为无效的问题，是解决 `invalid_provider_content_type` 的关键一步。
  - **PR #90138** ([链接](https://github.com/openclaw/openclaw/pull/90138)) 修复了 MiniMax-M3 模型因 `thinking` 字段注入而中断的 Bug。
- **平台渠道稳定性**：
  - **PR #90389** ([链接](https://github.com/openclaw/openclaw/pull/90389)) 通过将斜杠命令状态锚定到 `globalThis`，解决 Mattermost 长久以来的 503 回归问题（#68113）。
  - **PR #90132** ([链接](https://github.com/openclaw/openclaw/pull/90132)) 为 QQBot 输出添加了推理/思考内容的脱敏逻辑，开启自动合并。
  - **PR #89744** ([链接](https://github.com/openclaw/openclaw/pull/89744)) 修复了 Discord 多账户启动时主账户优先级不足的问题。
- **Agent 运行时优化**：
  - **PR #90060** ([链接](https://github.com/openclaw/openclaw/pull/90060)) 修复了模糊文本编辑时误改写无关行的严重 Bug（P0 级）。
  - **PR #90259** ([链接](https://github.com/openclaw/openclaw/pull/90259)) 新增会话重置序列的上下文摘要功能，防止长对话信息丢失。
  - **PR #89483** ([链接](https://github.com/openclaw/openclaw/pull/89483)) 确保 Agent 执行中的错误回复能被正确持久化到聊天历史。
- **记忆系统增强**：
  - **PR #90304** ([链接](https://github.com/openclaw/openclaw/pull/90304)) **已合并**，新增 QMD 检索模式下的重排序开关。
  - **PR #89138** ([链接](https://github.com/openclaw/openclaw/pull/89138)) 优化了 OpenAI 批量嵌入模式，提升了大型知识库的处理效率。

**影响评估**：项目正在系统性修复 2026.6.1 引入的技术债，但多个 XL 级 PR 标注了 `merge-risk: 🚨 compatibility` 和 `merge-risk: 🚨 session-state`，表明修复过程仍需警惕潜在的副作用。

### 4. 社区热点

今日社区讨论最激烈的议题直指项目当下的最大痛点：

1. **升级信任危机**：**Issue #90072** ([链接](https://github.com/openclaw/openclaw/issues/90072))“升级 2026.6.1 后 Cron 状态被静默清空”（👍 3）引发大量共鸣。用户对本应平稳的增量升级失去信任。
2. **核心 Provider 瘫痪**：**Issue #90083** ([链接](https://github.com/openclaw/openclaw/issues/90083))（👍 3）和 **#90093** ([链接](https://github.com/openclaw/openclaw/issues/90093))（👍 2）引爆了对新版本 OpenAI 适配的恐慌。大批依赖 gpt-5.4/5.5 的用户反馈完全无法使用。
3. **“静默失败”引发的焦虑**：**Issue #72808** ([链接](https://github.com/openclaw/openclaw/issues/72808))“静默丢失 Slack 连接”（20 条评论）虽非新问题，但仍是社区反馈最强烈的经典 Bug。用户呼吁增加用户可见的错误提示层。

**核心诉求**：社区强烈要求 “Stop breaking my setup on upgrade” 和 “Don't fail silently”。

### 5. Bug 与稳定性

**灾难级（数据不可逆损失）**：
- **#90072** ([链接](https://github.com/openclaw/openclaw/issues/90072)) (P1)：升级至 2026.6.1，SQLite 迁移清空 44/45 个 Cron 任务，无任何提示。**目前无 Fix PR**，风险极大。
- **#90093** ([链接](https://github.com/openclaw/openclaw/issues/90093)) (P1)：ChatGPT 原生重放携带加密推理内容，导致后续轮次直接 400 错误。**目前无 Fix PR**。

**关键级（核心功能阻塞）**：
- **#90083** ([链接](https://github.com/openclaw/openclaw/issues/90083)) (P1)：OpenAI ChatGPT Responses 传输完全不可用。`Fix PR #90399` 已提交。
- **#90082** ([链接](https://github.com/openclaw/openclaw/issues/90082)) (P1)：Active-memory 电路断路器过于激进，污染主会话提示词。**需产品决策**。
- **#90036** ([链接](https://github.com/openclaw/openclaw/issues/90036)) (P1)：Codex 运行时模型路由从 `openai/gpt-5.5` 漂移至 `openai-codex/gpt-5.5`。**无 Fix PR**。
- **#88929** ([链接](https://github.com/openclaw/openclaw/issues/88929)) (P1)：飞书流式卡片渲染异常，内容截断仅剩最后一个字符（如“？”）。**无 Fix PR**。
- **#87307** ([链接](https://github.com/openclaw/openclaw/issues/87307)) (P1)：Matrix 线程回复退化为普通回复。**无 Fix PR**。

**重要级（慢性功能异常）**：
- **#65161** ([链接](https://github.com/openclaw/openclaw/issues/65161)) (P2)：Heartbeat 孤岛模式卡顿，系统日志与执行事件错乱。
- **#67419** ([链接](https://github.com/openclaw/openclaw/issues/67419)) (P2)：会话上下文膨胀，Bootstrap 文件每轮注入浪费 20%-30% Token。

**趋势判断**：今日报告的重大 Bug 以 2026.6.1 周边的 Provider 通信和数据库迁移问题为主，新 Bug 呈现集中爆发态势，修复速度需进一步加快。

### 6. 功能请求与路线图信号

今日活跃的功能请求揭示了社区的长期期待：

- **数据安全与隐私**：**#64046** ([链接](https://github.com/openclaw/openclaw/issues/64046))“敏感数据脱敏”是呼声最高的 Feature Request。结合 PR #90132 (QQBot 输出脱敏) 来看，项目已有意识地在局部落地，但缺乏全局策略。**RFC #69066** ([链接](https://github.com/openclaw/openclaw/issues/69066)) 试图从架构上分解用户认证与服务身份，是深度治理安全的信号。
- **会话管理升级**：**PR #90259** ([链接](https://github.com/openclaw/openclaw/pull/90259)) 引入重置序列摘要，标志着项目开始解决长对话记忆丢失的痛点。
- **AI 原生能力扩展**：**#63930** ([链接](https://github.com/openclaw/openclaw/issues/63930)) 要求支持 Anthropic Advisor 工具，紧跟行业 Server-side Tool 趋势，可能成为下一版本的亮点功能。
- **可配置性提升**：**PR #89992** ([链接](https://github.com/openclaw/openclaw/pull/89992)) 提出写时生成本地编辑器的 JSON Schema，是对用户长期诟病“配置不可发现”的正面回应。

### 7. 用户反馈摘要

从 Issue 评论中提炼出以下核心声音：

- **“升级恐惧症”盛行**：用户普遍表达了“升级 = 冒风险”的心态。多位用户指出升级后遭受不可逆修改（#90072、#90083），社区呼吁引入完善的迁移前完整性检查和回滚支持。
- **“静默失败正在杀死信任”**：Slack 连接丢失（#72808）、Compaction 清空 Session（#67417）、Active-memory 注入错误提示（#90082），这些错误从不主动向用户反馈，最终表现为“机器人不工作”。
- **“配置是黑箱”**：结合 PR #89992，用户 @danhayman 的评论 “I don’t seem to be able to touch my openclaw.json without breaking something” 高度概括了新用户的挫败感。社区不仅需要 Schema，更需要官方严格的配置校验模型。

### 8. 待处理积压

以下 Issue 悬而未决多时，对用户体验构成慢性伤害，建议维护团队在下一轮 Sprint 中优先排期：

1. **#48300** ([链接](https://github.com/openclaw/openclaw/issues/48300)) (P2, 2026-03-16)：Memory_search 混合模式 FTS 不返回结果。积压 81 天，核心知识库功能受损。
2. **#63216** ([链接](https://github.com/openclaw/openclaw/issues/63216)) (P1, 2026-04-08)：同一会话键反复硬重置。积压 58 天，严重影响重度用户。
3. **#64810** ([链接](https://github.com/openclaw/openclaw/issues/64810)) (P1, 2026-04-11)：Telegram 心跳事件吞没用户回复。积压 55 天，渠道基本可用性严重受损。
4. **#64046** ([链接](https://github.com/openclaw/openclaw/issues/64046)) (P1, 2026-04-10)：敏感数据脱敏。需求强烈，但项目至今无全局方案。
5. **#60612** ([链接](https://github.com/openclaw/openclaw/issues/60612)) (P2, 2026-04-04)：“Doctor”命令警告用户使用 NVM Node 但无法修复。体验死循环，积压 62 天。

**紧急提醒**：新晋的严重 Bug **#90072** ([Cron 数据丢失](https://github.com/openclaw/openclaw/issues/90072)) 应被视作最高优先级，目前完全无 PR 认领，应立即安排维护者介入。

---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告 (2026-06-05)

## 1. 生态全景

2026 年 6 月 5 日，个人 AI 助手与自主智能体开源生态呈现出 **“核心平台承压修复，专项项目加速冲刺”** 的格局。以 OpenClaw 为代表的通用框架虽遭遇升级信任危机，但依然维持全生态最大的贡献量与反馈量；细分赛道项目（NanoBot、ZeroClaw、IronClaw 等）则利用自身架构灵活性与有限范围，在安全加固、可观测性、Agent 运行时生产化等方向取得了跨越式进展。整体生态正从“功能堆叠”转向 **“可靠、可控、可观测”** 的品质竞争：用户对静默失败、升级破坏、安全漏洞的容忍度急剧下降，而对执行控制权、工具调用兼容性、渠道稳定性的需求已成为社区共同焦点。

---

## 2. 各项目活跃度对比

| 项目 | Issues 动态（新开/关闭/更新） | PR 动态（合并/更新） | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | ~500 条更新（新开集中爆发） | 103 合并 / ~500 更新 | 无（上一版回归严重） | 高风险，信任承压 |
| **NanoBot** | 1 新开 / 5 关闭 | 60 合并 / 74 更新 | 无 | 健康，交付质量高 |
| **Hermes Agent** | 约 50 更新 / 10 关闭 | 约 50 更新（合并数未明确） | 无 | 活跃但桌面端问题积聚，P0 安全悬空 |
| **PicoClaw** | 3 新开 / 4 关闭 | 12 合并 / 22 更新 | Nightly 自动构建 | 良好，关键 Bug 快速修复 |
| **NanoClaw** | 1 新开（质量存疑） | 3 合并 / 8 更新 | 无 | 中等，渠道修复为主，PR 积压 |
| **IronClaw** | ~41 更新 | 16 合并 / ~50 更新 | 无 | 高产出，回归问题收敛快 |
| **LobsterAI** | 无新 Issue | 16 合并（全部关闭） | 无（`release/2026.5.28` 回合 main） | 极健康，低积压 |
| **Moltis** | 2 新功能请求 | 0 合并 / 3 活跃 PR | 无 | 正常推进，需加速评审 |
| **CoPaw (QwenPaw)** | ~32 更新 | ~33 更新（含 beta 发布） | v1.1.11-beta.1 | 健康但有严重 Bug（死循环） |
| **ZeroClaw** | 28 新开 / 5 关闭 | 11 合并 / 50 更新 | 无 | 高活跃，阻塞问题集中关闭 |
| NullClaw / TinyClaw / ZeptoClaw | 无活动 | 无活动 | — | 停滞 |

> *注：Issues/PR 数多为报告中的“更新”总量（含已关闭/合并），反映当日社区交互规模。*

---

## 3. OpenClaw 在生态中的定位

- **核心参照地位**：无论从命名体系（PicoClaw、NanoClaw、ZeroClaw 等）还是社区规模看，OpenClaw 都是生态中最广泛使用的基线项目。其日活（500+ Issue/PR 量级）远超其他项目，社区反馈和贡献密度最高。
- **技术路线差异**：OpenClaw 提供全栈 Agent 基础设施——Provider 适配、记忆系统、Agent 运行时、多通道支持，力图成为“通用底座”。相比 NanoBot（安全与生命周期优先）、ZeroClaw（Rust 轻量高性能）、IronClaw（Reborn 运行时商业级），OpenClaw 功能覆盖最广，但近期因版本破坏性变更导致信任动摇。
- **社区对比**：OpenClaw 的用户基数最大，但修复速度滞后于 Bug 爆发速度；NanoBot、LobsterAI 等则在有限范围内保持极高的合并效率和低积压，形成“高质量小循环”对比“大规模高风险”的分化。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体用户诉求 |
|---|---|---|
| **任务级模型 / 精细化路由** | NanoBot (#912)、ZeroClaw (#7100)、CoPaw (Cron 模型指定) | 不同场景（对话/工具/浏览）分别配置最优模型 |
| **Agent 执行中断与可控性** | CoPaw (#4961 / #4964)、ZeroClaw (Shell 策略 RFC)、IronClaw (子代理生命周期) | 用户可随时打断 Agent 任务，或设置阻塞/批准策略 |
| **工具调用兼容性** | OpenClaw (#90399 等)、NanoBot (#3984)、CoPaw (#4958)、PicoClaw (#3007) | 跨 Provider 工具名、参数、流式事件的一致解析 |
| **可观测性 / 监控** | ZeroClaw (#7233 OTel 重构)、NanoBot (#4176 生命周期钩子)、OpenClaw (要求更好错误提示)、LobsterAI (#2091 首次响应计时) | 生产环境需要查看 Agent 决策过程、Token 消耗、错误原因 |
| **安全与隐私加固** | NanoBot (#4119 / #4123 / #4053)、OpenClaw (#64046 脱敏)、Hermes Agent (#9560 路径遍历 P0)、ZeroClaw (#7155 命令策略) | 文件系统逃逸、SSRF、敏感信息落盘、工具调用校验 |
| **记忆 / 上下文管理增强** | OpenClaw (#90304 重排序等)、NanoBot (#4191)、CoPaw (#4781 等)、IronClaw (#4084 子代理持久化)、Moltis (#1089) | 长对话压缩/持久化/避免 OOM，防止信息丢失 |
| **多平台渠道稳定性** | NanoClaw (WhatsApp/Signal)、ZeroClaw (Web 斜杠命令)、Hermes Agent (桌面端)、Moltis (LINE/SMS 请求) | 消息投递不丢失、流式分离、跨渠道配置一致 |

这些共同方向表明生态正从“功能有无”进入 **“生产级品质”** 竞争阶段。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 / 语言 |
|---|---|---|---|
| **OpenClaw** | 全功能 Agent 框架、Provider 兼容、记忆系统 | 自部署开发者，追求全面性 | TypeScript/Node（推断），高度模块化 |
| **NanoBot** | 安全优先、生命周期钩子、CI 质量、企业集成 | 企业级开发、安全敏感用户 | 稳健型，深度依赖测试和安全 PR |
| **Hermes Agent** | 桌面 Agent、浏览器操作、任务运行 | 桌面自动化与高级用户 | Electron 桌面端 + CLI，Mac/Win/Linux |
| **PicoClaw** | 轻量级实现、核心 Bug 修复、构建兼容 | 资源敏感部署、FreeBSD 等小众平台 | Go（从 `pkg/tools/shell.go` 推断） |
| **NanoClaw** | 即时通讯渠道（WhatsApp/Signal）稳定性 | 消息优先的助手部署 | 维持 Baileys 兼容，社区贡献驱动 |
| **IronClaw** | Reborn 运行时、子代理、触发器、OpenAPI 兼容 | 复杂工作流与平台化部署 | 商业 NEAR AI 背书，架构重 |
| **LobsterAI** | 协作客户端、Kit 市场、Cowork 协同 | 团队协作、终端用户 | React/Redux 前端，集成 OpenClaw 网关 |
| **Moltis** | 语音交互、浏览器自动化、本地优先 | 语音助理、隐私敏感用户 | 个人开发者驱动，Sprint 集中 |
| **CoPaw (QwenPaw)** | 阿里生态、中国渠道（QQ/飞书）、通义模型 | 中国开发者、阿里云用户 | TypeScript，注重国内平台兼容 |
| **ZeroClaw** | Rust 轻量运行时、可观测性、微内核 | 生产部署、性能敏感环境 | Rust，资源占用低，OTel 原生支持 |

项目虽多共享相似名称，但**专业分化明显**：有的主打安全（NanoBot）、有的主打性能（ZeroClaw）、有的主打协作（LobsterAI）、有的主打语音（Moltis）、有的主打桌面（Hermes Agent）。这种分化意味着单一框架难以满足全部场景，生态正走向**互补竞争**。

---

## 6. 社区热度与成熟度分层

| 层次 | 项目特征 | 代表项目 |
|---|---|---|
| **高活跃·快速迭代** | 日 PR 合并 >10，Issue 大量涌入，有持续版本或分支推进 | OpenClaw、NanoBot、IronClaw、ZeroClaw、CoPaw、Hermes Agent |
| **中等活跃·质量巩固** | 活跃但体量较小，侧重修复与文档，无大量新 Bug 爆发 | PicoClaw、LobsterAI、Moltis、NanoClaw |
| **低活跃·停滞** | 过去 24 小时无任何活动 | NullClaw、TinyClaw、ZeptoClaw |

- **成熟度领先**：NanoBot、LobsterAI 表现出极高的代码质量与极低的积压；ZeroClaw 在 Rust 生态中的性能与可观测性设计使其生产潜力大。
- **成熟度承压**：OpenClaw 虽用户最多，但版本回归与信任危机导致健康度下滑；Hermes Agent 虽有快速社区响应，但 P0 安全漏洞长期悬空构成风险。
- **中等成熟**：PicoClaw 持续修正兼容性问题，CoPaw 系统性增强功能但需解决死循环等严重 Bug；IronClaw 合并速率高但架构 PR 量大，风险可控。

---

## 7. 值得关注的趋势信号

1. **“升级破坏”引发信任重构**：OpenClaw #90072（Cron 静默清空）、Hermes Agent 桌面端启动循环等事件表明用户对升级的畏惧已成系统性问题。未来框架必须提供 **迁移预检、回滚保障、灰度发布** 能力，否则将加速用户向更稳定的小项目分流。

2. **安全从“附加功能”变为“准入门槛”**：NanoBot 同一日提交 4 个安全 PR（SSRF、符号链接逃逸、只读隔离、工具校验），Hermes Agent 开放 P0 路径遍历漏，ZeroClaw 提出 Shell 命令策略 RFC。安全已成为项目能否进入企业场景的前置条件，不再只是锦上添花。

3. **Agent 控制权从“全自动”向“可控自主”转移**：CoPaw 连续两条 Issue 要求中断执行；ZeroClaw 要求分级命令策略；NanoBot 要求任务级模型配置。用户不再接受“Agent 自己做决定”，而是希望**随时干预、指定规则、监控过程**。这意味着交互协议需要增加中断、暂停、策略注入等接口。

4. **可观测性成为生产基础**：ZeroClaw 的 OTel 重构、NanoBot 的生命周期钩子、LobsterAI 的首次响应计时、OpenClaw 社区对错误提示层的呼吁——标志项目正从“开发者本地调试”转向“生产运维监控”。未来的 Agent 框架必须原生输出结构化事件和指标。

5. **渠道多样化与消息可靠性并重**：NanoClaw 修复 WhatsApp/Signal 消息丢失、ZeroClaw 对齐 Web 斜杠命令、Moltis 请求 SMS/LINE 接入——单纯增加渠道已不再够，用户要求**每个渠道的消息不丢失、不重复、不走样**。静默失败（Silent Failure）正成为最受反感的 Bug 类型。

6. **本地化与边缘计算趋势**：Moltis 的本地 STT（FunASR/SenseVoice）请求、ZeroClaw 的轻量 Rust 设计、PicoClaw 对 FreeBSD 的关注，表明部分用户群体正在推动 Agent 脱离纯云端依赖，向**本地或混合部署**演进。这对于离线场景和隐私敏感需求有重大意义。

---

**对 AI 智能体开发者的建议**：当前阶段应优先投资三件事——**可靠的升级/迁移体系**（避免信任崩塌）、**内置的可观测性框架**（降低运维摩擦）、**灵活的 Agent 控制接口**（中断/策略/审批）。功能速度固然重要，但生态已进入品质竞争周期，安全与可控性才是下一阶段的真正壁垒。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot 项目动态日报 | 2026-06-05

---

### 1. 今日速览

项目在 2026-06-05 显示出极高的迭代活力。过去 24 小时内 PR 更新量高达 **74 条**，其中 **60 条**被合并或关闭，社区贡献与核心团队并行推进效率极高。Issues 方面保持 `1:5` 的新开/关闭比（1 条新开活跃，5 条已关闭），问题响应和修复速度可观。当前版本无新发布，但代码库正处于安全加固（工具校验严格化、SSRF 防护、文件系统逃逸阻断）与基础设施健壮性（确定性测试、生命周期 hooks）的深度冲刺阶段，项目健康度与交付质量均处于高位。

---

### 2. 版本发布

无。

---

### 3. 项目进展

今日项目核心进展聚焦于**核心架构健壮性**、**安全可观测性**与**企业级集成**三大方向。

- **核心生命周期与管理**：
  - `#4176`（已合并）—— 引入 `run-level` Agent 生命周期钩子（`before_run/after_run/on_error/on_finally`），为后续监控、日志和扩展提供了标准化接口。
  - `#4194`（已合并）—— 重构 Capture 机制，以权威的 `run-level` 快照替代逐步累积的状态，提升上下文追踪的一致性和可靠性。

- **安全与兼容性修复**：
  - `#4126`（已合并）—— 为 Azure OpenAI Provider 增加 Azure AD（AAD）身份认证支持，打通企业级纳管流程。
  - `#3984`（已合并）—— 修复工具调用 ID 被重写导致的兼容性问题（影响 GLM-4.7, Kimi 2.6 等），确保 OpenAI 兼容 API 的端到端一致性。
  - `#4164`（已合并）—— 修复 `uv tool install` 场景下 pip 不可用的问题，解决 WebUI 安装 CLI 应用的阻断错误（fix #4158）。

- **社区生态共建**：
  - `#4186`（已合并）—— 社区重度贡献 PR，包含敏感信息落盘脱敏、Dream 双阶段重写、原子写入保障等 5 个增强模块，直接提升了数据安全和记忆质量。
  - `#4191`（已合并）—— 社区贡献，对 Memory 管理层进行了优化。
  - `#4163`（已合并）—— 实现 WebUI 用户消息的 "Fork from here" 能力，大幅提升对话编辑与衍生场景的易用性。

- **CI/测试质量提升**：
  - `#4189`（已合并）—— 替换基于定时的竞态等待为确定性时钟/事件编排，直接减少 CI 中的不稳定失败。

---

### 4. 社区热点

- **最受关注的功能诉求：任务级模型配置**
  `[Issue #912](https://github.com/HKUDS/nanobot/issues/912)`（4 条评论，3 👍，stale 状态）
  社区强烈期望能针对 **Conversational / Tool Use / Browser Use** 分别配置不同的模型，而非共用全局模型。虽然该 Issue 已标记为 stale，但其 3 个赞仍然是所有开放 Issue 中的最高值。这一诉求反映了高级用户对“场景最优模型组合”的强烈需求——他们愿意牺牲配置复杂度以换取性能和成本的最优解。

- **稳定性信任危机：回退机制未生效**
  `[Issue #1121](https://github.com/HKUDS/nanobot/issues/1121)`（3 条评论，3 👍，已关闭）
  核心 Bug：当主力模型超时（如 Gemini 503/600s），配置的 fallback 模型未被触发，Agent 直接向用户返回错误。用户最核心的反馈是：“The agent simply returns an error to the user instead of retrying with the next model”。这比功能缺失更隐蔽，但一旦用户感知到“承诺的容错机制不工作”，对项目可靠性的信任冲击很大。该 Issue 已关闭，强烈建议维护者在 Release Notes 中明确说明修复范围与验证方法。

- **潜在架构变革：子 Agent 继承 MCP 工具**
  `[PR #4192](https://github.com/HKUDS/nanobot/pull/4192)`（Open）
  开启 `tools.subagentMcpAccess` 后，子 Agent 可继承主 Agent 的 MCP 工具。这直击了下一代 Agent 架构（主管-专家模式）的核心需求，若能稳定落地，将使 NanoBot 在多级 Agent 编排上拥有差异化竞争力。

---

### 5. Bug 与稳定性

- **严重性：高**
  - `#1121`（已关闭）—— **LLM 超时时回退模型未触发**。fallback 策略配置失效是严重的可靠性 Bug，修复后应纳入回归测试专项覆盖。

- **严重性：中**
  - `#4158`（已关闭，修复于 `#4164`）—— **`uv tool install` 场景下 pip 不可用**。WebUI 调用 `CliAppManager` 安装应用失败，影响依赖 uv 的现代化部署用户。

- **严重性：低 / 防御性修复（Open PRs，亟需 Review）**
  - `[#4190](https://github.com/HKUDS/nanobot/pull/4190)` —— 工具调用校验严格化：拒绝近似工具名（near-miss）及标量/非对象参数，防止误执行。
  - `[#4119](https://github.com/HKUDS/nanobot/pull/4119)` —— 阻断通过相对符号链接逃逸工作区的路径攻击。
  - `[#4053](https://github.com/HKUDS/nanobot/pull/4053)` —— 确保只读根目录不被写入工具误写，隔离媒体文件夹的写路径。
  - `[#4123](https://github.com/HKUDS/nanobot/pull/4123)` —— 对 MCP SSE 和流式 HTTP URL 注入 SSRF 守卫，实现重定向同源安全策略。

> **分析**：团队今日在防御性安全编码上投入巨大，这是一个极其健康的信号。上述四个安全 PR 已开启数天，建议核心维护者优先投入评审，避免修复代码膨胀或产生后续冲突。

---

### 6. 功能请求与路线图信号

- **路线图级信号：桌面端形态浮出水面**
  `[#4195](https://github.com/HKUDS/nanobot/pull/4195) (Open)` —— 首次公开桌面端 Shell，并与现有 WebUI 共享 Surface。该 PR 集成了文件预览、技能页面、自动化设置等网关 API。这暗示 NanoBot 可能即将推出原生桌面应用，是产品化路径上的关键里程碑。

- **下一代 Agent 能力：MCP 工具多层继承**
  `[#4192](https://github.com/HKUDS/nanobot/pull/4192) (Open)` —— 子 Agent 继承 MCP。若配合 #912（任务级模型配置），将首次允许用户构建“主管（高推理模型）+ 专家（低成本模型 + 特定 MCP 工具集）”的复杂系统。

- **易用性填补：技能发现命令**
  `[#3968](https://github.com/HKUDS/nanobot/pull/3968) (Open)` —— `/skill` 内置命令，用于列出所有已启用的技能及其描述。回应了 `#3959` 中“用户无法知道自己有哪些技能”的痛点。该 PR 量级较小，建议尽快合并，以提振社区“提需求-被实现”的链路信心。

- **高优先级待处理：任务级模型配置**
  `[#912](https://github.com/HKUDS/nanobot/issues/912) (Open, Stale)` —— 尽管已 stale，但其 3 👍 是目前所有 Open Issue 的最高值。建议维护团队明确给出技术选型：认领进入开发，或解释未纳入 Roadmap 的原因，避免长期冷处理导致社区失望。

---

### 7. 用户反馈摘要

- **满意度信号：开发者用代码投票**
  - `#4186` 的作者一次性贡献了敏感信息脱敏、Dream 双阶段重写、原子写入等 5 个相互独立的功能模块。这表明项目代码对于高级用户是“可编程且友好”的，这是极高满意度的间接证据。

- **挫败感信号：承诺的能力与实际表现不符**
  - `#1121` 中用户明确指出回退功能未触发，表达了对 Agent “直接就报错”的失望。
  - `#4158` 中用户因运行环境（uv）与预期（系统 pip）不匹配而遭遇阻断错误，暴露了安装场景测试的盲区。

- **缺失特性阵痛：平台支持广度**
  - `#4196` 用户期望支持火山引擎的 Seedream 5.0 Lite 图片生成模型。在抢占多模态 Agent 框架市场时，对国内主流云厂商推理服务的深度适配（Volcengine/百度/阿里等）正成为差异化的竞争壁垒。

---

### 8. 待处理积压

以下 Issue/PR 长期未响应或延宕，提醒维护者关注：

| 编号 | 类型 | 描述 | 关键风险 / 建议 |
|------|------|------|----------------|
| [#912](https://github.com/HKUDS/nanobot/issues/912) | Issue | Task-Specific Model Configuration | **社区 Vot 最高**，自 2026.02 开启后 stale。建议正式认领或解释不纳入的原因，避免社区预期落空。 |
| [#4123](https://github.com/HKUDS/nanobot/pull/4123) | PR (Open) | 拒绝不安全的 MCP HTTP URLs | SSRF 安全防护，开启 5 天无变动，建议优先合并。 |
| [#4119](https://github.com/HKUDS/nanobot/pull/4119) | PR (Open) | 阻断相对符号链接工作区逃逸 | 文件系统安全隔离，开启 5 天，建议优先评审。 |
| [#4053](https://github.com/HKUDS/nanobot/pull/4053) | PR (Open) | 只读根目录防止写入工具误写 | 数据写保护隔离，开启 7 天，建议优先评审。 |
| [#3968](https://github.com/HKUDS/nanobot/pull/3968) | PR (Open) | 新增 `/skill` 内置命令 | 轻量级 PR，已开启 13 天，快速合入可有效激励社区贡献者。 |
| [#3982](https://github.com/HKUDS/nanobot/pull/3982) / <br>[#3983](https://github.com/HKUDS/nanobot/pull/3983) | PR (Open) | Agent Runner 测试框架 + 覆盖阻断 Finish Reason | 体量较大的测试基础设施 PR，对 CI 回归覆盖至关重要，需投入深度评审。 |

---
*报告基于 HKUDS/nanobot 公开数据生成，截至 2026-06-05。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-06-05

## 1. 今日速览

项目今日迎来社区活跃度的爆发，**24小时内 Issue 与 PR 双双达到 50 条更新**，呈现出密集的反馈与交付态势。维护团队响应积极，一次性关闭了 10 条长期遗留的 Issues，覆盖安全、文档与旧版 Bug，展现出良好的技术债消化节奏。**然而，桌面端稳定性报告激增（约占今日 Bug 报告总量 40%），与一条 P0 级安全补丁长周期悬空（PR #9560），构成了当前项目健康度的主要隐忧。** 总体来看，项目处于高强度迭代的“修复期”向“稳定期”冲刺的阶段。

## 2. 版本发布

**今日无新版本发布。** 尽管社区针对 v0.15.x 版本的桌面端问题（启动循环、中文输入截断、安装失败等）集中提交了大量 Bug 报告，但官方尚未释放修复版本。考虑到合并与关闭的 Issue 密度，一个包含大量稳定性修补的小版本（如 v0.15.2）或已在排期之中。

## 3. 项目进展

**今日项目维护者进行了大规模的问题清理（Closed 10条 Issues），并对核心用户体验问题提交了修复 PR。** 主要进展包括：

- **技术债清理与安全加固**：
  - **安全**：Docker 容器 Root 权限与 Capabilities 过度问题已关闭（#3969）。
  - **依赖**：Node.js 20 升级至 22 LTS 的提案关闭（#4876）。
  - **测试**：移除平台无关的 `import grp` 测试（#24531）。
  - **文档**：补齐 Docker LLM 连接指南（#7963）与 Hetzner 控制台字符乱码提示（#36279）。

- **重大 Bug 修复 PR 提交**：
  - **#39530**：针对桌面端 `uvicorn` 依赖导致启动循环的 **自修复方案**，探测并强制重装损坏的 `uvicorn`。
  - **#39533**：修复 Linux Root 用户因缺失 `--no-sandbox` 参数导致桌面端直接闪退。
  - **#39521**：升级 `react-router` 以清理 `npm audit` 报告的高危漏洞。

- **高频需求功能落地**：
  - **#39531**：**实现“禁用内置记忆工具但保留外部记忆提供者”**（Closes #39492），直接响应了社区用户对 Memory 系统灵活配置的强烈呼声。

## 4. 社区热点

- **#527 Gateway Permission Tiers — RBAC**（评论: 10, 👍: 2）
  - **核心诉求**：用户对当前二值化授权模型（全通或全封）表示强烈不满。这是企业多租户、团队协作场景的刚性需求，是当前社区诉求最强烈、讨论最持久的功能请求之一。尽管呼声极高，但目前未见明确的官方开发排期。
  - Link: NousResearch/hermes-agent Issue #527

- **#39365 误导性 OpenRouter 错误提示**（评论: 3）
  - **核心诉求**：用户愤怒地指出系统在遭遇真实故障（HTTP 401 网关授权失效）时，**返回了完全不相关的错误信息**（"OpenRouter API key missing"）。这暴露了 Gateway Auth 层极其混乱的错误映射逻辑，严重消耗用户排障时间，已对项目口碑造成负面影响。
  - Link: NousResearch/hermes-agent Issue #39365

- **#39492 → #39531 记忆功能解耦**（评论: 3）
  - **协作典范**：用户今日提出需求，团队**当天提交 PR**。这是一个完美的社区驱动案例，展示了项目对用户反馈的高度敏感和快速落地能力。这几乎可以确定会纳入下一个版本。
  - Link: NousResearch/hermes-agent Issue #39492 | PR #39531

## 5. Bug 与稳定性

**今日 Bug 呈现出“桌面端泛滥”的态势，严重影响着 v0.15.x 用户的基础使用体验。**

| 严重度 | 编号 | 描述 | 状态 / 修复进展 |
|---|---|---|---|
| **P0 (安全)** | PR #9560 | 会话管理路径遍历漏洞（CWE-22），允许恶意用户控制技能系统 | 🔴 **悬空 53 天未合并，极度危险** |
| **P2 (致命)** | #39505 | 桌面端首次启动陷入无限“引导→安装→重启”循环 | 🟡 **已有 fix PR #39530** |
| **P2 (致命)** | #39503 | 桌面端 0.15.1 启动报错：`unrecognized arguments: --tui` | 🟡 **待修复** |
| **P2 (致命)** | #39484 | macOS 桌面端安装/重建后黑屏，`electron: Failed to load` | 🟡 **待修复** |
| **P2 (阻塞)** | #39332 | macOS 安装失败（已关闭，但未发版） | ✅ **已关闭，待验证** |
| **P2 (阻塞)** | #39418 | `/reload-mcp` 命令导致 CLI 终端完全死机 | 🟡 **待修复** |
| **P2 (严重)** | #39534 | Windows 端中文输入在聊天框中被截断/吃掉 | 🟡 **待修复** |
| **P2 (严重)** | #39457 | macOS 端 CKJ 输入法中英文混输时英文部分丢失 | 🟡 **待修复** |
| **P2 (严重)** | #39525 | 合盖休眠 / 切换 WiFi 后 Gateway 持续报错，无法恢复 | 🟡 **待修复** |
| **P2 (严重)** | #39489 | `/stop` 命令不清理 Docker 沙箱环境 | 🟡 **待修复** |

## 6. 功能请求与路线图信号

**高概率纳入下个版本（已有对应 PR 或被快速认领）：**
- **禁用内置记忆工具**（#39492 → #39531）: 服务端部署场景的精细运维需求。
- **系统托盘最小化**（#39468）: Windows/Linux 用户高频请求，提升 Desktop 后台驻留体验。
- **轻量模型配置档案**（#39507 Draft）: 多模型路由 Preset 切换，面向高级用户。
- **Cron 消息历史预览**（#39344）: 自动化任务上下文追溯，提升 B 端可用性。

**需观望或长期探索：**
- **Gateway 权限分级（#527）**：发布 3 个月，评论 10+，但尚无原型 PR。项目若想进军企业 IM 集成，此为必经之路。
- **Sandbox HOME 桥接（#39523）**：提出子进程沙箱无法访问 `~/.ssh`、`~/.gitconfig` 等问题。这是安全隔离和功能完整的长期博弈，预计设计周期会很长。
- **模型路由提供商扩展**：PR #22648 （Ollama Cloud） 已悬停近 1 个月，插件式 Web Search Provider 的落地进度稍显缓慢。

## 7. 用户反馈摘要

**痛点反馈（消极）：**
1. **桌面端稳定性是最大劝退因素**：大量新用户卡死在安装、首次启动、更换网络的环节（#39532, #39484, #39505, #39525）。一个无法稳定启动的应用，无论理念多先进，都难以留住用户。
2. **国际化体验缺失**：中文输入在 Win/Mac 双平台均有截断或丢失问题（#39534, #39457）。这直接阻挡了庞大的亚洲开发者社区。
3. **错误提示质量低下**：本次#39365 的“谎言式”报错是最突出的代表，这会严重削弱系统在排障时用户给予的信任。

**满意与亮点（积极）：**
1. **架构扩展性获认可**：用户非常认可 Memory Provider 与 Session 的隔离设计，并主动要求 “Disable built-in memory tool”，说明核心架构设计严谨，给了用户足够的定制信心。
2. **社区响应速度极快**：从 Issue #39492 到 PR #39531 的快速闭环，极大增强了社区信心，激发了用户的贡献意愿。
3. **用例拓展**：用户利用 Hermes Agent 自动生成了针对土耳其市场的 AI 语音销售栈研究报告（#39504），并在报告结尾注明 “这份报告由 Hermes Agent 自己编写”，**侧面印证了其 Browser Use 和 Task Run 的强悍能力**。

## 8. 待处理积压

**⚠️ [P0 / 安全] PR #9560 — 会话管理路径遍历漏洞**
- **状态**：自 2026-04-14 至今，已悬空 **53 天**，标签为 `P0`。Hermes Agent 能够操作系统文件，路径遍历漏洞的利用后果极其严重（凭证泄露、加密文件读取）。**作为开源分析师，我们不得不强烈呼吁维护团队将该 PR 的审查优先级提至最高，甚至考虑临时冻结相关模块或发布安全警告。**
- Link: NousResearch/hermes-agent PR #9560

**⚠️ [Feature] Issue #527 — RBAC 权限分级**
- **状态**：悬空 3 个月，无官方路线图更新。如果不给出明确的设计方向或 ETA，持续的“高温低应”社区讨论热度可能会转化为负面舆情。
- Link: NousResearch/hermes-agent Issue #527

**⚠️ [Bug] Issue #39332 — Mac 安装失败**
- **状态**：已关闭，但用户报出的版本是目前官网发布的 v0.15.1。如果该 Issue 是因“无法复现”或“将在下个版本修复”关闭，强烈建议明确回复用户现状，否则会让新用户重复踩坑。
- Link: NousResearch/hermes-agent Issue #39332

**⚠️ [Infra] Issue #39529 — 受限网络环境下 ZIP 回退应为一等公民**
- **状态**：影响了大量中国、企业内部、GFW 等网络环境用户。目前的安装流程在 SSH/HTTPS 失败后才尝试 ZIP，体验较差，建议作为优先选项之一。
- Link: NousResearch/hermes-agent Issue #39529

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 | 2026-06-05

---

## 1. 今日速览

过去 24 小时内，PicoClaw 项目保持高度活跃：共产生 7 条 Issue 更新（新开 3，关闭 4）和 22 条 PR 更新（待合并 10，已合并/关闭 12），并发布了一个自动构建的 Nightly 版本。社区贡献主要集中在关键 Bug 修复（PID 身份验证、Codex 流式工具调用丢失、JSON 序列化错误处理）和依赖兼容性调整上，项目健康度与响应速度均处于良好水平。

---

## 2. 版本发布

**Nightly Build (自动构建)**  
`v0.2.9-nightly.20260605.5224b9a4`  
> 基于 main 分支的自动构建，可能包含不稳定更改，仅供测试使用。  

完整变更日志：  
[sipeed/picoclaw compare/v0.2.9…main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

## 3. 项目进展

今日合并/关闭了多个重要修复，项目在稳定性与兼容性方面取得明显进步：

- **PID 身份验证修复** ([#3000](https://github.com/sipeed/picoclaw/pull/3000))：Singleton PID 检查新增进程身份验证，防止因 PID 重用导致网关启动崩溃循环（关联 Issue [#2720](https://github.com/sipeed/picoclaw/issues/2720)）。
- **Codex OAuth 工具调用修复** ([#3007](https://github.com/sipeed/picoclaw/pull/3007))：在最终响应为空时保留流式输出的工具调用事件，解决 `gpt-5.5` 下工具使用丢失问题。
- **JSON 序列化错误处理** ([#2996](https://github.com/sipeed/picoclaw/pull/2996))：`pkg/tools/shell.go` 中 7 处被忽略的 `json.Marshal` 错误改为显式错误返回，避免静默空字符串。
- **Makefile 兼容性修复** ([#2999](https://github.com/sipeed/picoclaw/pull/2999), [#2976](https://github.com/sipeed/picoclaw/pull/2976))：处理 `go env GOVERSION` 返回值中内嵌空格导致链接器参数错误的问题。
- **Larksuite SDK 升级适配** ([#3005](https://github.com/sipeed/picoclaw/pull/3005), [#3008](https://github.com/sipeed/picoclaw/pull/3008))：将 `oapi-sdk-go` 从 v3.7.5 升级至 v3.9.4，并适配其破坏性变更（`ReceiveIdTypeChatId` 重命名）。
- **依赖例行更新**：AWS Bedrock Runtime、SQLite、Anthropic SDK 等依赖通过 Dependabot 批量更新。

这些修复共同提升了服务的可靠性、第三方集成兼容性以及构建环境的鲁棒性。

---

## 4. 社区热点

以下 Issues/PRs 获得了最多的讨论与关注：

### [#2720 – [BUG] Singleton PID check doesn't verify process identity](https://github.com/sipeed/picoclaw/issues/2720) （已关闭，8 条评论）
- **核心诉求**：PID 文件检查存在逻辑缺陷，当 PID 被系统服务（如 `systemd-resolved`）重用时，网关启动会误判并陷入崩溃循环。该问题自 4 月 30 日提出，经过近 5 周的讨论，最终通过 PR [#3000](https://github.com/sipeed/picoclaw/pull/3000) 解决，社区关注度高。

### [#2968 – [BUG] /context always show Compress at: 76800 tokens](https://github.com/sipeed/picoclaw/issues/2968) （开放中，5 条评论）
- **核心诉求**：`/context` 命令仅显示硬预算压缩阈值（`contextWindow - maxTokens`），用户期望看到基于 `summarize_token_percent` 的软触发阈值。PR [#2985](https://github.com/sipeed/picoclaw/pull/2985) 已提出增加 `SummarizeAtTokens` 显示，正待合并。

### [#3012 – [BUG] Continuous consumption of tokens every minutes when evolution is enabled](https://github.com/sipeed/picoclaw/issues/3012) （开放中，1 条评论）
- **核心诉求**：用户报告启用 Evolution 模式后每分钟持续消耗 Token，可能涉及异常循环或轮询问题，目前尚无对应修复 PR。

---

## 5. Bug 与稳定性

以下为过去 24 小时内报告的 Bug，按严重程度排列：

| Bug | 严重程度 | 状态 | 对应修复 PR |
|------|----------|------|-------------|
| **Evolution 模式下每分钟持续消耗 Token** ([#3012](https://github.com/sipeed/picoclaw/issues/3012)) | **高** – 可能导致意外费用 | 开放 | 无 |
| **OneBot 群聊回复使用了 `send_private_msg`** ([#3002](https://github.com/sipeed/picoclaw/issues/3002)) | **高** – 功能完全异常 | 开放 | [#3009](https://github.com/sipeed/picoclaw/pull/3009) (待合并) |
| **Codex OAuth GPT-5.5 工具调用丢失** ([#3006](https://github.com/sipeed/picoclaw/issues/3006)) | **中** – 特定 provider 下工具功能不可用 | 已关闭 | [#3007](https://github.com/sipeed/picoclaw/pull/3007) (已合并) |
| **/context 始终显示单一压缩阈值** ([#2968](https://github.com/sipeed/picoclaw/issues/2968)) | **低** – 信息不全，不影响运行 | 开放 | [#2985](https://github.com/sipeed/picoclaw/pull/2985) (待合并) |
| **升级 v0.2.9 后 Web UI 消息错乱** ([#2972](https://github.com/sipeed/picoclaw/issues/2972)) | **中** – 影响使用体验 | 已关闭 | 未明确关联 PR (推测已在后续修复) |
| **Singleton PID 身份验证缺失** ([#2720](https://github.com/sipeed/picoclaw/issues/2720)) | **高** – 导致网关启动崩溃 | 已关闭 | [#3000](https://github.com/sipeed/picoclaw/pull/3000) (已合并) |

**稳定性评估**：高风险 Bug 均已有关联修复（PID、Codex 已合入；OneBot 待合并），仅 Token 持续消耗问题暂无解决方案，需重点关注。

---

## 6. 功能请求与路线图信号

- **改进 `/context` 命令信息展示**：来自 Issue [#2968](https://github.com/sipeed/picoclaw/issues/2968) 的反馈，用户希望同时看到压缩与汇总阈值。PR [#2985](https://github.com/sipeed/picoclaw/pull/2985) 已实现此功能，预计很快合并，极有可能进入下一版本。
- **更新用户手册以匹配 v0.2.9 变更**：Task [#2981](https://github.com/sipeed/picoclaw/issues/2981) 要求更新文档，反映版本大量改动。虽然未直接关联功能需求，但表明社区对文档补全的期待。
- 尚无明确的新功能请求（如新 channel、新模型支持）提交，当前重心仍在稳定性修复与兼容性维护上。

---

## 7. 用户反馈摘要

从过去 24 小时的 Issue 评论中可提炼出以下典型用户痛点：

- **阈值显示不透明**：用户在 [#2968](https://github.com/sipeed/picoclaw/issues/2968) 中表示只看到 `Compress at: 76800 tokens`，无法理解压缩何时触发，期望更透明的上下文管理信息。
- **升级引发回归**：用户在 [#2972](https://github.com/sipeed/picoclaw/issues/2972) 中反馈升级到 v0.2.9 后新会话自动附加旧历史消息，严重影响正常对话。
- **平台特定问题**：FreeBSD 15.0 用户频繁上报 Bug（见 [#2968](https://github.com/sipeed/picoclaw/issues/2968)、[#2972](https://github.com/sipeed/picoclaw/issues/2972)、[#3012](https://github.com/sipeed/picoclaw/issues/3012)），暗示在非主流操作系统上的兼容性测试存在缺口。
- **Token 消耗异常**：用户在 [#3012](https://github.com/sipeed/picoclaw/issues/3012) 中反映 Evolution 功能启用后每分钟产生 Token 消耗，疑似存在无谓重复调用，影响成本和性能。

总体而言，用户对升级后的稳定性问题（消息错乱、Token 滥用）表示不满，但社区贡献者响应迅速，多数关键问题已有关联修复。

---

## 8. 待处理积压

以下为开放时间较长且尚未合并的重要 PR，建议维护者优先关注：

| PR | 创建时间 | 说明 | 阻塞原因推测 |
|----|----------|------|-------------|
| [#2813 – fix(pid): verify gateway identity before blocking startup on stale PID](https://github.com/sipeed/picoclaw/pull/2813) | 2026-05-07 | PID 身份验证（早期版本），已被 [#3000](https://github.com/sipeed/picoclaw/pull/3000) 替代并关闭？实际仍 open，需明确处理。 | 可能因冲突被搁置，需关闭或合并 |
| [#2947 – fix: correct claude-sonnet-4.6 model ID to use hyphens](https://github.com/sipeed/picoclaw/pull/2947) | 2026-05-26 | 修复默认 Anthropic 模型 ID 错误，导致 404 | 待 review，可能涉及其他模型 ID 规范讨论 |
| [#2934 – fix(channels): allow whatsapp native mode with use_native flag](https://github.com/sipeed/picoclaw/pull/2934) | 2026-05-24 | 支持 WhatsApp 原生模式 | 可能需更广泛的 Channel 配置重构 |
| [#2956 – fix: preserve channel enabled state when merging security.yml](https://github.com/sipeed/picoclaw/pull/2956) | 2026-05-27 | 合并 `.security.yml` 后禁用已启用 Channel | 安全配置合并逻辑复杂，需充分测试 |
| [#2962 – build(deps): bump github.com/anthropics/anthropic-sdk-go from 1.26.0 to 1.46.0](https://github.com/sipeed/picoclaw/pull/2962) | 2026-05-28 | 较大跨版本依赖升级，可能引入 Breaking Changes | 需适配性检查 |

这些项目若长期未合并，可能会增加后续集成成本或导致社区贡献者重复工作，建议维护者根据优先级排期处理。

---

*日报生成时间：2026-06-05 | 数据来源：GitHub (sipeed/picoclaw)*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，以下是根据您提供的 NanoClaw 项目 GitHub 数据生成的 2026-06-05 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-05

**数据时段：** 2026-06-04 至 2026-06-05
**项目仓库：** [`nanocoai/nanoclaw`](https://github.com/nanocoai/nanoclaw)

---

## 1. 今日速览

过去 24 小时项目开发活动集中于修复核心通信渠道（WhatsApp、Signal）的稳定性问题，整体活跃度较高。共处理 8 条 PR 更新，其中 3 条已合并/关闭，另有 5 条待审查，显示开发团队工作密度大，但也存在一定的审查队列积压。社区公开讨论与外部 Issue 反馈较少，唯一的新 Issue 质量存疑，当前社区参与度主要集中于功能性贡献者。项目未发布新版本。

## 2. 版本发布

无。

## 3. 项目进展

今日合并/关闭的 PR 主要围绕 **WhatsApp 稳定性修复**、**代码质量提升** 以及 **社区技能审核**。项目在强化底层基础设施方面取得了实质性进展。

- **WhatsApp 会话保持大幅增强**：合并 PR [#2633](https://github.com/nanocoai/nanoclaw/pull/2633)（maschenborn）。该修复解决了 Baileys 7.x 升级后配对会话在 Bot 重启时被自动销毁的结构性 Bug，直接改善了 WhatsApp 渠道的常驻稳定性。
- **技术债务清理**：合并 PR [#104](https://github.com/nanocoai/nanoclaw/pull/104)（Alakazam03）。替换了早期遗留的两个 `as any` 类型断言，引入严谨的 `BoomError` 类型定义，增强了类型安全与代码健壮性。
- **社区贡献技能通过审核**：处理 PR [#2687](https://github.com/nanocoai/nanoclaw/pull/2687)（dtanikella）。外部贡献者遵循贡献指南提交了“旅行代理”技能，表明插件的贡献流程对新开发者友好可用。

## 4. 社区热点

由于公开 Issue/PR 区域的评论较少，热点主要体现在高优先级的功能障碍修复请求中。

- **Signal DM 被静默丢弃（最受关注 Bug）**：PR [#2689](https://github.com/nanocoai/nanoclaw/pull/2689) 针对 Signal 私聊消息被静默吞没的问题提供了修复。这是当前 Signal 渠道最高频的痛点，直接影响新用户的首次使用体验。评论区虽安静，但背后的修复诉求十分迫切。
- **本地语音转文字功能持续受期待**：PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459)（mtichikawa）引入 Whisper 本地语音转录，虽然已开放 23 天，但作为不依赖云端 API 的核心差异化功能，长期受到社区（尤其是私有化部署用户）的高频关注。
- **平台杂音与新用户引导**：Issue [#2686](https://github.com/nanocoai/nanoclaw/issues/2686)（“I want to travel to Canada”）是唯一新开的 Issue，缺乏上下文且无有效建设性内容，极有可能是测试或误操作。建议项目方考虑关闭或引导至 Discussion 板块。

## 5. Bug 与稳定性

今日状态以显著 Bug 修复为主，但同时出现了多个阻塞性的新 Bug Fix PR。

- **[严重] 未合并 WhatsApp LID 群组消息投递失败**：PR [#2688](https://github.com/nanocoai/nanoclaw/pull/2688)（mcaldas）。WhatsApp 迁移至 LID 地址后，Bot 回复被 Baileys 报错 ack 421，用户无法感知错误。**影响范围：大量使用 WhatsApp 的部署存在消息沉默丢失问题。**
- **[严重] 未合并 Signal DM 首次消息丢失**：PR [#2689](https://github.com/nanocoai/nanoclaw/pull/2689)（klingel）。DM 中缺少 `isMention` 标志导致路由系统不创建记录。**影响范围：Signal 用户的第一条消息一定会丢失。**
- **[高] 未合并 Poll-Loop 输出格式损坏（积压 25 天）**：PR [#2405](https://github.com/nanocoai/nanoclaw/pull/2405)（matt1995ai）。Auto-compaction 后模型输出频繁丢失 XML 标签闭合，导致消息格式异常。**影响范围：长期运行的 Bot 可能间歇性产生格式错误的回复。**
- **[已修复] WhatsApp 重启后认证清除**：PR [#2633](https://github.com/nanocoai/nanoclaw/pull/2633)。已成功合并，DevOps 环境中验证有效。

## 6. 功能请求与路线图信号

目前未提出全新的功能请求，但已有 PR 强烈暗示了未来的版本路线图。

- **下一代核心候选：全平台本地语音转录**：PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459) 进展缓慢但持续跟进。该功能完全去云化（仅依赖 host 本地 Whisper），符合 AI 助手本地部署趋势，很可能是下个大版本（vNext）的核心卖点之一。
- **Signal 功能集即将释放**：由 PR [#2685](https://github.com/nanocoai/nanoclaw/pull/2685)（ira-at-work）的文档更新内容可以看出，Signal 渠道即将正式支持群组打字指示器、外发消息反应以及引用回复。这可能是继 Poll-Loop 之后项目最值得期待的功能落地点。

## 7. 用户反馈摘要

公开评论极少，反馈主要来自贡献者提交的 Bug 修正内容，投射出大量隐形用户的痛点。

- **核心痛点：消息的“静默失败”**。无论是 WhatsApp 的 LID 兼容问题，还是 Signal DM 的标记遗漏，都导致了 Bot 表现为“沉默的假死”。这是当下 Agent 开发领域最影响信任的用户体验问题——发送了消息，但无任何反馈。
- **迁移阵痛仍在持续**：近期多个 Fix 都指向 Baileys 7.x 升级后的兼容性问题（认证、消息路由、群组寻址），老用户正在经历迁移期的不稳定，建议在 Release Note 中增加该部分的提醒。
- **正面信号：技能贡献流程走通**：PR [#2687](https://github.com/nanocoai/nanoclaw/pull/2687) 的顺利合并证明项目的 Skill 系统文档清晰、reviewer 在线，开发者生态建设处于正向循环。

## 8. 待处理积压

以下项目需要维护者们重点关注，以避免贡献者流失或系统长期带病运行。

- **P0（必须立即审查）**：
  - **PR [#2405](https://github.com/nanocoai/nanoclaw/pull/2405)**（Poll-loop compaction fix）：积压 **25 天**。该 Bug 直接影响模型输出的正确性，且作者对根因分析详实。如果长期不处理，核心循环的可靠性将被持续质疑。
  - **PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459)**（Voice Transcription）：积压 **23 天**。此类功能型 PR 长期处于开放状态极耗贡献者热情，请至少给出明确的意见（合并 / 要求修改 / 纳入远期规划）。
- **P1（今日新晋阻塞项）**：
  - **PR [#2689](https://github.com/nanocoai/nanoclaw/pull/2689)**（Signal DM fix）与 **PR [#2688](https://github.com/nanocoai/nanoclaw/pull/2688)**（WhatsApp LID fix）：这两条昨日新提交，分别阻塞着 Signal 和 WhatsApp 两大渠道的可用性，建议与 Poll-loop 穿插安排审查。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的。根据您提供的 IronClaw GitHub 数据，以下是生成的项目动态日报。

---

### IronClaw 项目动态日报 — 2026-06-05

#### 1. 今日速览

过去 24 小时，IronClaw 项目进入高强度迭代冲刺阶段，共计更新 41 个 Issue 和 50 个 PR，其中 16 个 PR 完成合并。项目全部重心围绕 **Reborn 运行时**的生产化稳控展开，子代理（Subagent）生命周期持久化、触发器（Trigger）逻辑正确性以及 OpenAPI 兼容层是当前绝对核心攻关点。今日合并的 PR 扎实地解决了子代理完成通知的幂等性与持久化、触发器创建配对机制等关键可靠性问题，虽长期待合并 PR 数量（34）仍高，但整体合并效率与问题收敛速度均表现极佳，项目健康度强健。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

*   **夯实 Reborn 子代理（Subagent）完成交付基石**：针对 Background 子代理结果丢失的顽疾（`#4084`），今日合并的 `#4348`、`#4349`、`#4350` 系列 PR 完成了闭环。通过引入持久化门存储（Gate Store）、RestartReconciler 与墓碑标记，确保了 Agent 重启后完成结果依然能够恰好一次（Exactly-Once）地投递到父代理，这是 Reborn 迈向生产环境的重要质变。
*   **触发器（Trigger）生命周期全面补齐**：合并的 `#4466` 为触发器创建接入了配对生命周期钩子，避免了孤立触发器；`#4472` 和 `#4473` 则新增了激活状态管理与一次性运行支持。结合此前 `#4420` 对“一次性触发策略失效”的修复，触发器的行为逻辑现已完整。
*   **渠道与前端体验大幅进化**：Slack 通道完成了 Actor/Subject 旅程拆分（`#4476`）与认证提示链接的自动化投递（`#4478`）。WebUI v2 的设置面板经历了一场“去信息过载”的重构，将 LLM Provider 按照配置状态进行分组（`#4477`、`#4480`），显著优化了多 Provider 管理的用户心智模型。
*   **启动 Reborn 外部生态适配**：巨型 PR `#4459` 已提交，为 Reborn 原生注入了 OpenAI 兼容的 Chat Completions 和 Responses API 路由合约。配合 `#4468` 的 `previous_response_id` 暴露请求，Reborn 正在为承接外部 API 流量铺平道路。

#### 4. 社区热点

*   **#3280——P0 级 Reborn 工作流 Facade 设计（6 条评论）**：自 2026-05-06 开放至今仍备受关注，该 Issue 定义了 ProductAdapter 与 Reborn 服务层之间的统一外观模式。虽进展缓慢，但它是理解 Reborn 整体架构的核心蓝图，任何重大的接口变更都绕不开该设计。
    *   *链接：nearai/ironclaw Issue #3280*

*   **#4424——“模型被告知有工具，但不能用”引发的信任危机（4 条评论）**：该 Bug 性质极其恶劣：`builtin.spawn_subagent` 在系统提示词中被广告给模型，但结构化工具数组（Tools Array）中却未包含它，导致模型无法实际调用。社区对此类“提示词与能力不一致”的 Bug 表现出零容忍。
    *   *链接：nearai/ironclaw Issue #4424*

*   **#4427——Agent 循环退出原因“隐身”（2 条评论）**：开发者指出 Reborn Agent 循环结束的具体原因（如达到迭代上限、触发退出条件或异常失败）从未被正确追踪记录到日志中。运维人员面对一个退出 Agent 只能去翻数据库，极大降低了调试效率。
    *   *链接：nearai/ironclaw Issue #4427*

*   **#4311——预算治理错误被错误归类（1 条评论）**：一个高危逻辑漏洞。多种非上下文溢出类的预算治理失败（如 Token 总量超标）被错误地合并映射为 `ContextOverflow`，导致触发错误的恢复降级策略。
    *   *链接：nearai/ironclaw Issue #4311*

#### 5. Bug 与稳定性

*   **[严重/已修复] #4424**：Reborn 环境下的 `spawn_subagent` 在 Structured Tools 中缺失，导致模型无法调用核心内建函数。*修复已合并。*
    *   *链接：nearai/ironclaw Issue #4424*
*   **[高/追踪中] #4311**：模型网关错误地将预算治理失败映射为上下文溢出。*导致错误的恢复策略。*
    *   *链接：nearai/ironclaw Issue #4311*
*   **[高/追踪中] #4366**：Agent 循环的 Compaction 逻辑在遇到不稳定转写时直接硬错误而非推迟。*基础修复（#4440）已合并，推迟后重试的元数据问题由 #4464 追踪。*
    *   *链接：nearai/ironclaw Issue #4366*
*   **[中/已修复] #4084**：Background 子代理完成后，结果无法被通知投递给父代理。*修复已合并。*
    *   *链接：nearai/ironclaw Issue #4084*
*   **[中/已修复] #4160**：Google OAuth 刷新令牌刷新逻辑缺失，且令牌生命周期缺乏清理机制。*修复已合并。*
    *   *链接：nearai/ironclaw Issue #4160*

#### 6. 功能请求与路线图信号

*   **强信号——强攻 OpenAI 兼容层**：`#4459`（XL 规模）的提交是当前最明确的路线图信号，表明 Reborn 正式将“成为 OpenAI API 的兼容替代/增强方案”列为产品目标。`#4468` 对 `previous_response_id` 的暴露需求，则是为了完美支持外部客户端的对话延续（Conversation Continuation）。
*   **新基础生态设施——IronHub 集成**：PR `#4479` 正在将 IronHub 技能/工具市场的安全安装流程（含 Ed25519 签名验证）移植到 Reborn，这标志着 Reborn 正在从 Agent 框架进化为带有包管理能力的 Agent 应用平台。
*   **新用户引导体验优化**：PR `#4481` 为 WebUI v2 引入了首次引导流程，允许用户未配置任何 LLM 时通过点击登录 NEAR AI / ChatGPT 或粘贴 API 密钥直接开始使用，低门槛接纳新用户。
*   **泛亚洲渠道接入**：针对飞书（Feishu/Lark）长连接 WebSocket 事件接入的 PR `#4178` 仍在冷处理中，未获得合并进展。

#### 7. 用户反馈摘要

*   **“模型被虚假广告欺骗”的焦虑**：`#4424` 的体验让社区认识到，即使是最微小的“文本提示词与结构化能力不一致”，也会导致 Agent 卡死在循环幻想中。用户对工具调用可靠性的要求是**绝对刚性**的。
*   **“无法调试”的黑盒恐惧**：`#4427` 清晰地传递了运维侧用户的痛点。在没有 `LoopFailureKind` 日志的情况下，生产环境 Agent 的“非正常退出”问题几乎等同于不可排查。开发者需要的是 Exit Reason + Tracing。
*   **“硬化状态机边缘”的痛苦共识**：从一次性触发器（`#4473`）到不稳定的转写状态（`#4366`），大量 Issue 的反馈都指向了一个核心：**Agent 系统不能在非主路径上坍塌**。用户（核心开发者）正在严谨且痛苦地修补每一处状态竞争和错误处理边缘。

#### 8. 待处理积压

*   **#3280——P0 级架构设计长期静默**：定义了 Reborn Facade 的核心 Issue 已开放整月，虽然部分子任务（如 `#3283`）正在推进，但主 Issue 缺乏最终的决策或状态更新，建议维护者主动同步进展与关闭评估。
    *   *链接：nearai/ironclaw Issue #3280*
*   **Hooks 持久化后端系列 PR（#3936, #3937, #3951）**：来自贡献者 `zmanian` 的三方钩子激活与持久化后端 PR（自5月23日起）已停滞近两周。作为影响 Reborn 可扩展性的关键路径，建议核心 Reviewer 尽早安排评审，避免分支偏离主开发线。
    *   *链接：nearai/ironclaw PR #3951*
*   **飞书 WebSocket 通道 PR（#4178）**：一个大型的国际化渠道功能目前处于孤立开放状态。考虑到构建长期 WebSocket 连接可能面临的合入冲突，该项目如果仍将飞书渠道纳入路线图，应主动回应贡献者并推动合入。
    *   *链接：nearai/ironclaw PR #4178*
*   **小维护 Issue #3941 被长期搁置**：该 Issue 负责清理已合并 PR 遗留的代码腐败（死 API、空洞测试），虽工作量极小，但此类架构纪律问题挂起两周不利于保持代码库整洁。
    *   *链接：nearai/ironclaw PR #3941*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 (2026-06-05)

---

## 1. 今日速览

LobsterAI 项目今日表现出极高的开发活跃度与极佳的健康状况。过去 24 小时内，团队密集处理并关闭了 **16 个 Pull Request**，无待合并 PR，且无新 Bug Issue 上报，表明当前阶段核心工作是**消化遗留需求**与**打磨关键稳定性**。今日最大亮点是 `release/2026.5.28` 正式回合主干（#2090），正式引入 Kit 专家套件市场、Cowork 会话分叉等重磅能力；同时长期积压的 Cowork 功能请求（如系统通知、收藏、标签）在今日被集中合并，有效回应了社区期待。项目正处于功能生态建设与基础设施加固并行的快速成熟期。

---

## 2. 版本发布

**今日无新版本发布。**

> **同步关注**：PR #2090 已将 `release/2026.5.28` 分支合并回 `main` 主分支。该版本包含 73 个提交，核心增量如下：
> - **新增 Kit 专家套件市场 UI 与 Redux 集成**（获取/安装/卸载/卡片展示）
> - **Cowork 会话本地分叉能力**
> - **插件手动更新机制**
> - 多项 MCP/Gateway/Artifacts 稳定性修复

---

## 3. 项目进展

今日 16 个 PR 完成合并/关闭，集中在 **MCP 基建重构**、**Cowork 体验升级** 与 **积压 PR 清理** 三大主线上：

- **发布线与版本同步**
  - **#2090** — 将 `release/2026.5.28` 回合 `main`，标志着版本管线回归一致，Kit 市场等重量级功能已准备就绪。

- **MCP 核心深度优化**（3 PRs）
  - **#2091** — 重构 `npx` 类 MCP 服务器启动流程：前置 `npm` 解析与本地安装，将启动命令转换为稳定的本地路径，避免每次启动走慢速 npx 路径；同时在关键路径增加了首次响应计时日志，为持续性能监控提供数据支撑。
  - **#2100** — 修复受管 MCP 安装时 Node 工具链路径丢失的回归 Bug（QA 日志复现），并增加解析失败时的优雅降级（回退原始 stdio 配置而非丢弃 MCP 服务器）。
  - **#2103** — 为远程 MCP 服务器新增 URL 格式校验，同步拦截无效配置写入 OpenClaw，前端表单同步展示本地化错误提示。

- **Cowork 协同体验全面增强**（5 PRs）
  - **#2110** — 修复向 OpenClaw 网关发送超大图片负载导致 `1009` 错误的问题；精细化单图与整条消息的超载判断，新增专注的单元测试。
  - **#2095** — 支持子助手（Subagent）会话的批量选中与删除，限制网关清理并发与重试次数。
  - **#2111** — 重构语音输入模块，将 ASR IPC 注册、WAV 编码、客户端拆分至独立模块，解耦 Cowork 状态与 UI。
  - **积压功能上线**（详见社区热点）—— 系统通知、书签收藏、会话标签同步落地。

- **AI 模型修复与插件管理**
  - **#2093** — 纠正 MiniMax-M3 模型硬编码 `supportsImage: false` 的问题，正式启用图像输入能力（M2.5/M2.7 不支持但 M3 支持）。
  - **#2096** — 隐藏 OpenClaw 内置运行时插件 ID，净化插件管理列表。

---

## 4. 社区热点

- **积压特性集体上线（社区强烈共鸣）**
  今天最具标志性的事件是 6 个来自 **2026年4月7日** 的 PR 在同一日内被合并：
  - **系统通知**（#1536）：Cowork 会话完成/失败时弹出原生 OS 通知，点击可自动聚焦跳转。
  - **消息书签**（#1538）：对 AI 回复消息标记黄色星标，便于长对话中快速定位重要信息。
  - **会话标签**（#1542）：支持自定义标签、自动建议与侧边栏筛选。
  - **国际化修复 ×3**（#1540、#1543、#1544）：审批弹窗硬编码中文、编辑按钮翻译缺失、Copilot OAuth 轮询 Bug。

  > 这些 PR 代表了社区对 Cowork 日常使用场景（跨窗口感知、信息管理、全球化体验）的长期诉求，积压近两个月后同日合并，显著提振了社区对维护者响应速度的信心。

- **Issue #769 持续关注（启动稳定性焦虑）**
  唯一活跃的 Bug 跟踪仍是 **OpenClaw 网关启动失败**（3月24日创建），用户附带了全屏截图并表达困惑（"这个是什么问题啊？"）。虽评论区活跃度不高，但作为长期未解的核心接口问题，暗示项目在**配置诊断与错误提示教育**方面仍有改进空间。

---

## 5. Bug 与稳定性

**今日无新增 Bug Issue，但修复密集。**

| 严重程度 | PR/Issue | 问题描述 | 状态 |
|----------|----------|----------|------|
| 🔴 严重 | #2100 | MCP 受管安装因 Node 工具链路径缺失失败 | ✅ 已修复 |
| 🟠 较高 | #2110 | OpenClaw 超大图片负载导致 1009 网关错误 | ✅ 已修复 |
| 🟠 较高 | #1544 | 关闭 Settings 面板后 Copilot OAuth 后台轮询持续运行 15 分钟 | ✅ 已修复 |
| 🟡 一般 | #2103 | 远程 MCP 服务器 URL 格式未校验，可写入无效配置 | ✅ 已修复 |
| 🟡 一般 | #2093 | MiniMax-M3 图像输入能力被硬编码误禁用 | ✅ 已修复 |
| 🟢 轻微 | #2096 | 内部运行时插件显示在用户管理界面 | ✅ 已修复 |
| 🟢 轻微 | #1543 | 审批弹窗确定/拒绝按钮硬编码中文 | ✅ 已修复 |
| 🔴 严重 | **#769** | **OpenClaw 网关未能按时启动（3月24日至今未解）** | ⏳ **待排查** |

---

## 6. 功能请求与路线图信号

- **🚩 Kit 专家套件市场落地**：`release/2026.5.28` 发布的 Kit 市场（#2090）是明确的路线图拐点——项目正从"单一 AI 对话客户端"转向 **"插件化 AI 能力平台"**。支持获取/安装/卸载、Tabs 展示、Try-asking 跳转，生态架构初步成型。

- **🚩 MCP 进入"生产可用"阶段**：连续三天对 MCP 启动速度（#2091）、环境兼容（#2100）、输入校验（#2103）的深度打磨，表明团队已经将 MCP 从"功能实现"切换到 **"稳定性与性能优化"** 模式。这是支持外部工具生态大规模接入的前提。

- **🚩 Cowork 场景化体验闭环**：系统通知 + 书签 + 标签 + 子助手批量管理 的集中上线，构成了 Cowork "并行工作－切换感知－信息回溯－会话组织" 的完整使用闭环，符合用户从"尝鲜试用"到"日常主力工具"的需求升维路径。

---

## 7. 用户反馈摘要

- **Issue #769** 用户反馈：OpenClaw 网关启动失败，带截图表示困惑（"这个是什么问题啊？"）。核心诉求是 **"启动失败时能否告诉我确切原因"**。当前错误提示对普通用户仍不够友好，建议提供配置校验指引或诊断日志导出的入口。

- **社区情绪观察**：通过 #1536、#1538、#1542 等 PR 的合并，长期隐忍的"通知缺失"、"消息无法标记"、"会话分类混乱"等痛点得到直接回应。用户未直接发声，但 PR 本身的高频参与度（创建于4月初、积压2个月后仍被 Pull）侧面证明了需求的刚性。

---

## 8. 待处理积压

| 项目 | 链接 | 创建时间 | 状态说明 |
|------|------|----------|----------|
| **Issue #769**: OpenClaw 网关启动失败 | [链接](https://github.com/netease-youdao/LobsterAI/issues/769) | 2026-03-24 | **唯一活跃 Bug 跟踪**，自创建至今已超过 70 天。用户附带了截图但对错误原因感到困惑（"这是什么问题啊？"）。鉴于 OpenClaw 是整个 AI 请求的核心网关，该问题直接影响用户入门体验与网关稳定性信心。建议维护者优先复现并至少补充详细的错误分类和排障文档。 |

**其他提醒**：今日所有 16 个 PR 均已关闭，无新增积压 PR，代码库处于极其健康的低积压状态。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis 项目动态日报 | 2026-06-05

---

### 1. 今日速览

过去 24 小时，Moltis 项目无新版本发布，但开发活跃度较高：新增 **2 个功能请求**，**3 个活跃 PR** 获得更新。核心开发者 @s-salamatov 主导了全部活跃提交，重点攻克生产环境稳定性问题（会话记忆膨胀限制、浏览器 Shadow DOM 交互、Telegram 消息流分离）。社区侧开始涌现“超低延迟本地语音识别”和“日常通信渠道扩展”的强烈信号，项目正处于 **核心稳定性打磨与社区需求引导** 的关键过渡期。

---

### 2. 版本发布

*今日无新版本发布。*

---

### 3. 项目进展

今日虽无 PR 被正式合并，但三条核心 PR 均取得实质性推进，反映出项目正从「功能堆叠」向「生产级健壮性」跃迁：

- **Telegram 流式输出重写（[PR #1099](https://github.com/moltis-org/moltis/pull/1099)）**
  将 Agent 的思考进度流与最终回复相分离。修复了此前进度消息被当成最终答案发送的问题，极大改善 Telegram 渠道的对话层级体验。（关联 Issue #1097）

- **浏览器元素定位修复（[PR #1103](https://github.com/moltis-org/moltis/pull/1103)）**
  高效修复 Agent 在现代化 SPA 网站中无法穿透 Shadow DOM 进行节点查找的缺陷，显著提升 Browsing Agent 对复杂前端框架的兼容能力。

- **工具结果持久化限制（[PR #1089](https://github.com/moltis-org/moltis/pull/1089)）**
  在会话反序列化（rehydration）时对 `tool` 与 `tool_result` 内容进行大小截断，防止长时间 Agent 对话因 Token 膨胀导致 OOM 或性能退化，是一项重要的稳定性前瞻加固。

---

### 4. 社区热点

今日新 Issue 暂无评论互动，但提案本身指向了两个高价值社区诉求：

- **本地超低延迟语音识别（[Issue #1102](https://github.com/moltis-org/moltis/issues/1102)）**
  作者 `LauraGPT` 推崇 FunASR/SenseVoice：“10秒音频仅需 70ms 处理 + 原生流式”。这反映出部分用户对云端 STT 的延迟与隐私存在顾虑，追求完全离线的极速体验。

- **日常通信渠道扩展（[Issue #1101](https://github.com/moltis-org/moltis/issues/1101)）**
  用户 `joeblew999` 请求接入 SMS 与 LINE（日本主流社交通道）。表明 Moltis 正被探索作为“个人基础设施”融入到用户的真实社交网络中，而不仅仅是一个 Demo 应用。

**分析：** 两条请求虽无讨论，但分别代表 **Agent 感知入口的极致化（本地说）** 与 **Agent 连接范围的广泛化（多渠道）**，是社区对 AI 助手成熟度的两个核心期待。

---

### 5. Bug 与稳定性

| 严重程度 | 问题描述 | 当前状态 |
|---|---|---|
| **高** | **Browser Shadow DOM 穿透失效 (关联 [PR #1103](https://github.com/moltis-org/moltis/pull/1103))**<br>Agent 在访问现代 Web 应用时无法定位组件内部元素，导致浏览功能瘫痪。 | 已有 Fix PR |
| **中** | **会话记忆膨胀风险 (关联 [PR #1089](https://github.com/moltis-org/moltis/pull/1089))**<br>长时间对话中工具调用结果无限制堆积，重构上下文时可能引发 Token 超限或异常。 | 已有前置修复 PR（待合并） |
| **中** | **Telegram 消息流混淆 (关联 [PR #1099](https://github.com/moltis-org/moltis/pull/1099))**<br>进度流被误当最终回复发送，影响用户体验。 | 已有 Fix PR（关联 #1097） |

---

### 6. 功能请求与路线图信号

- **强烈纳入信号 — Issue #1102 (本地 STT 引擎)**
  请求集成 FunASR/SenseVoice。完全契合 Moltis “本地优先、隐私优先”的设计哲学，且性能指标诱人。若社区意向明确，预计会是下一阶段的重点功能方向。

- **广阔落地潜力 — Issue #1101 (短信与 LINE 通道)**
  当前 Moltis 主要依赖 Telegram 通道。SMS 与 LINE 的加入将极大扩展项目的用户触达面（特别是企业通知与亚洲市场）。该请求对 Connector 架构影响较小，利空不大，利好明显。

- **路线图判断**：当前 PR 主要集中在 **现有核心的修复与加固**（Session、Browser、Channel），尚未进入新功能开发阶段。但这两条 Issue 为下一版本提供了清晰的用户侧优先级参考。

---

### 7. 用户反馈摘要

由于新 Issue 尚无讨论，反馈主要提炼自提案动机与 PR 上下文：

- **用户 `LauraGPT`**：明确表示“项目很棒”（Great voice assistant project!），但对现有 STT 方案存在延迟或云依赖的不满，希望获得更快的本地实时方案。
- **用户 `joeblew999`**：认为当前仅支持单一 Telegram 信道不够，希望将 Moltis 深度嵌入短信与 LINE 的日常通信场景中，突显出“真正的 AI 助理必须无处不在”的朴素需求。
- **用户侧隐含痛点（源自 PR #1099）**：Telegram 流式进度消息与最终回复的混乱，说明早期用户体验仍有粗糙之处，核心开发者正快速响应用户反馈进行打磨。

---

### 8. 待处理积压

- **[PR #1089] Cap persisted tool results before rehydration（已开放 4 天）**
  [GitHub 链接](https://github.com/moltis-org/moltis/pull/1089)<br>
  自 6 月 1 日开启，最后更新于 6 月 4 日。作为影响会话持久化底层逻辑的关键 PR，建议 reviewer 加速审核，确保其在大量新功能涌入前合入，避免后续冲突。

- **[Issue #1102] 与 [Issue #1101] 缺少标签与里程碑**
  两条新 Issue 目前没有 `enhancement` / `feature-request` 标签，也未分配里程碑。建议维护者尽快标注并回应社区，引导后续讨论方向，提升贡献者留存率。

- **合并推进提示**：核心贡献者 @s-salamatov 正同时推动三条 PR，建议社区其他维护人员积极提供 Code Review，分担审核负担，加速 Pipeline。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，我理解您的需求。作为一名 AI 智能体与个人 AI 助手领域的开源项目分析师，我将基于您提供的 CoPaw (QwenPaw) 项目数据，生成一份结构清晰、数据驱动、客观专业的项目动态日报，日期为 2026-06-05。

---

### CoPaw (QwenPaw) 项目动态日报 | 2026-06-05

---

### 1. 今日速览

过去 24 小时内，QwenPaw 项目保持高度活跃，社区参与度与维护响应速度均处于健康水平。今日处理了 32 条 Issue 和 33 个 PR，并发布了新的 Beta 版本，体现了开发团队对问题修复和功能迭代的持续投入。尽管有部分历史 PR 被重新激活标记，但核心 Bug 修复（如 MCP 工具名兼容性、前端闪烁）和功能增强（如新增子代理工具）的合并是今日的主要进展。社区热点集中在 **Agent 执行控制**（中断/终止）和 **用户体验优化** 两个方向，反映出用户对更精细操控和更流畅交互的迫切需求。

---

### 2. 版本发布

#### v1.1.11-beta.1
- **发布链接**: [v1.1.11-beta.1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11-beta.1)
- **更新内容**:
  - **修复**: 修复了 `ProviderManager` 在获取 `get_model_max_input_length` 时的回退逻辑，提升了配置的鲁棒性。
  - **重构**: 针对 `agent` 类型的定时任务（Cron Job），禁用了其发送“气泡”提示（push bubbles），优化了推送机制，减少干扰。
- **破坏性变更**: 本次更新无破坏性变更。
- **迁移注意事项**: 无需进行特别迁移操作，常规更新即可。

---

### 3. 项目进展

今日项目核心进展体现在多个关键 Bug 的修复和功能增强的合并上，项目整体稳定性和功能性得到补强。

- **Bug 修复 (高价值)**:
    - **[PR #4958] fix(mcp): alias-rewrite tool names rejected by OpenAI-style regex**: 合并了关键 PR，解决了 MCP 工具名包含 `.` 等特殊字符时，无法调用 OpenAI 系列模型的问题（关联 [Issue #4918](https://github.com/agentscope-ai/QwenPaw/issues/4918)）。这是对多模型兼容性的重要修复。
    - **[PR #4766] fix(environments): fix scrollbar flicker**: 移除了环境变量页面 hover 时的 `transform` 属性，解决了滚动条闪烁问题，提升了 UI 稳定性。
- **功能增强**:
    - **[PR #4806] feat(agents): add spawn_subagent tool**: 新增了 `spawn_subagent` 内置工具，使 Agent 能够创建工作空间内的临时子代理，与现有的跨工作空间 `chat_with_agent` 工具形成互补，大幅增强了 Agent 执行复杂任务的灵活性和协作能力。
    - **[PR #4848] feat(channels): add QR code authorization for QQ channel**: 为 QQ 频道渠道引入了扫码授权功能，降低了用户配置门槛。
    - **[PR #4879] feat(feishu): support interactive card content extraction**: 增强了对飞书消息的支持，现在可以提取来自交互式卡片（`interactive`）的文本内容，丰富了对复杂消息格式的解析能力。
- **测试与质量**:
    - **[PR #4332] test(console): complete frontend unit test milestone**: 合并了前端单元测试的里程碑，新增 10 个测试文件和约 100 个测试用例，覆盖了常量、上下文、布局等模块，显著提升了前端代码质量。
- **待观察进展**:
    - 几个重要的历史 PR（如 [PR #476](https://github.com/agentscope-ai/QwenPaw/pull/476), [PR #710](https://github.com/agentscope-ai/QwenPaw/pull/710), [PR #1240](https://github.com/agentscope-ai/QwenPaw/pull/1240) 等）今日被标记为“已关闭”，这可能是维护者在进行代码清理或重新评估，需关注其为何长期未合并/关闭。

---

### 4. 社区热点

本周社区讨论的热点呈现出从“被动使用”到“主动控制”的转变。

- **Agent 执行中断与终止**:
    - **[Issue #4964](https://github.com/agentscope-ai/QwenPaw/issues/4964) & [Issue #4961](https://github.com/agentscope-ai/QwenPaw/issues/4961)**: 用户 `feng183043996` 连续提交了两个高度相似的 Feature Request，核心诉求是“当 Agent 正在执行任务或调用工具时，用户发送新消息能够中断或终止当前执行”。此请求获得了社区的高度共鸣，反映了用户在与 Agent 交互时，希望能够即时纠偏或下达新指令，而非被动等待当前流程结束。这代表了用户对 Agent **交互控制权** 的强烈需求。
- **工具集成与可用性**:
    - **[Issue #4918](https://github.com/agentscope-ai/QwenPaw/issues/4918)**: 关于 MCP 工具名包含点号 `.` 导致 GPT 模型调用失败的讨论。虽然问题已经通过 [PR #4958](https://github.com/agentscope-ai/QwenPaw/pull/4958) 修复，但其高达数条的评论反映出用户在集成外部工具时，对跨模型兼容性的高度关注和敏感性。用户社区对这类问题的响应速度很满意。

---

### 5. Bug 与稳定性

今日报告的 Bug 数量不多，但类型较杂，包含一些潜在的稳定性问题。

- **严重 Bug**:
    - **[Issue #4967] 执行过程陷入死循环，无法退出**: 报告时间为今天（6月5日），尚无评论。这是一个非常严重的稳定性问题，可能导致资源消耗和程序无响应。目前无关联 PR，需紧急关注和复现。
- **功能异常**:
    - **[Issue #4962] DeepSeek API回复内容折叠**: 用户反馈所有回复内容会错误地折叠到“思考过程”中，严重影响阅读体验。此问题影响所有 DeepSeek 用户，需要优先排查。
    - **[Issue #4959] Latex公式显示异常**: 用户提交了截图，展示了 Latex 公式在前端渲染混乱的问题。这是一个影响教育、科研等专业场景用户体验的 Bug。
- **修复中的 Bug**:
    - **[Issue #4937] /compact 命令忽略模型 max_input_length**: 上下文压缩功能使用了错误的默认值（128K），在引入大上下文窗口模型（如 MiniMax M3 512K）时可能导致压缩策略失效。此问题仍在开放中，未有 PR 关联。
- **历史稳定性问题**:
    - **[Issue #4781] tool_result_pruning 机制失效**: 大型输出未有效截断，社区对其造成的上下文爆炸风险讨论持续。

---

### 6. 功能请求与路线图信号

今日涌现的功能请求对产品未来演进方向有重要参考价值，部分已有相关 PR 在推进。

- **高潜力/已有关联实现**:
    - **Agent 中断/终止执行** ([Issue #4961](https://github.com/agentscope-ai/QwenPaw/issues/4961), [#4964](https://github.com/agentscope-ai/QwenPaw/issues/4964)): 社区呼声极高，应被视为 **下一版本的核心候选功能**。目前未有 PR 直接解决此问题，但 [PR #4955](https://github.com/agentscope-ai/QwenPaw/pull/4955) 中对后台子代理的生命周期管理可能为此提供了技术基础。
    - **Cron 任务支持直接执行脚本** ([Issue #4950](https://github.com/agentscope-ai/QwenPaw/issues/4950), [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963)): 用户希望 Cron 任务能直接执行 Shell 脚本，用于运维、数据处理等场景。该请求有明确的应用场景。
    - **令牌（Token）用量可视化** ([PR #4433](https://github.com/agentscope-ai/QwenPaw/pull/4433)): 旨在提供每次对话的 Token 用量和上下文窗口使用信息，直接关联多个 Feature Request ([Issue #4767](https://github.com/agentscope-ai/QwenPaw/issues/4767), [#4782](https://github.com/agentscope-ai/QwenPaw/issues/4782))。该 PR 已处于开放并在审查中，有望在下一版本落地。
- **值得关注的早期信号**:
    - **品牌 Provider 卡片合并** ([Issue #4965](https://github.com/agentscope-ai/QwenPaw/issues/4965)): 用户建议将同一品牌（如智谱）的多个 Provider 卡片合并，减少 UI 杂乱。这是一个很好的 UX 优化建议，反映了用户对更简洁管理界面的期待。
    - **会话文件快捷打开** ([Issue #4786](https://github.com/agentscope-ai/QwenPaw/issues/4786)): 用户希望生成的 Word/PPT 文件能有快捷入口一键打开，提升工作流效率。这是一个典型的“最后一公里”体验优化需求。

---

### 7. 用户反馈摘要

从今日的 Issues 和 PR 评论中，可以提炼出用户群体的几个核心反馈：

- **对“控制权”的渴望**：用户 `feng183043996` 在多次提交的涉及 Agent 执行流程、记忆机制、Cron 功能等请求中，始终贯穿着“希望系统按照我的规则执行”的诉求。无论是中断 Agent、配置 Cron 任务细节，还是让记忆系统更智能地关联，其背后都是对 **更深度、更细节的操控能力** 的期待。
- **专业用户的技术敏感度**：如 [Issue #4918](https://github.com/agentscope-ai/QwenPaw/issues/4918) 的用户 `Smalye`，能够精准指出 MCP 工具名不兼容 GPT 模型的根本原因（`tools[].name` 校验失败），并提供详细的报错信息和临时方案。这表明项目存在一批技术实力强、愿意深入贡献的专业用户。
- **中国用户的特殊场景**：多个 Issue 体现中国特色场景。例如，希望桌面版能在局域网内用手机访问控制台（[Issue #4960](https://github.com/agentscope-ai/QwenPaw/issues/4960)）、Win 环境下代码模式无法打开其他硬盘项目（[Issue #4876](https://github.com/agentscope-ai/QwenPaw/issues/4876)），以及 DeepSeek 模型前缀缓存优化（[Issue #3891](https://github.com/agentscope-ai/QwenPaw/issues/3891)）。这要求项目在网盘使用、网络配置、国产模型优化等方面给予更多关注。

---

### 8. 待处理积压

提醒维护团队关注以下长期未获官方回应的 Issue：

- **[Issue #3891] DeepSeek 前缀缓存命中率偏低（~95%），优化空间巨大**:
    - **创建时间**: 2026-04-27（已开放 40 天）
    - **用户**: LI-VIOLIENT
    - **链接**: [Issue #3891](https://github.com/agentscope-ai/QwenPaw/issues/3891)
    - **影响**: 直接影响使用 DeepSeek 模型的用户成本和延迟。该 Issue 提供了详细的分析和巨大的优化价值（将 95% 命中率提至极高），但至今无任何评论（包括维护者回复），可能被视为沟通盲区。

- **[Issue #4640] 会话结束自动总结机制（Pre-hook Memory Archiving）**:
    - **创建时间**: 2026-05-23（已开放 13 天）
    - **用户**: feng183043996
    - **链接**: [Issue #4640](https://github.com/agentscope-ai/QwenPaw/issues/4640)
    - **影响**: 该 RFC 触及社区高度关注的“记忆系统”痛点，并提出了结构化的解决方案。但未获得任何官方回复或打标签，如果开发团队对此功能有不同考虑或有内部计划，应当做出回应以避免社区创作者的热情受挫。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-06-05

---

## 1. 今日速览

ZeroClaw 过去 24 小时保持极高活跃度：处理了 **33 条 Issue**（新开 28，关闭 5）与 **50 个 PR**（待合并 39，已合并/关闭 11）。数项 S1 阻塞级 Bug 被集中关闭（Ollama 工具调用失败、Windows Shell 双引号、RPC 会话回收崩溃），稳定性显著回升。与此同时，**可观测性大重构**（#7233）、**管理面板 UI**（#7229）、**Web 斜杠命令**（#7223）等重量级 PR 集中递交，项目正为 v0.8.0 生产级发布做密集铺路。当日无新版本发布。

---

## 2. 版本发布

当日无新版本发布。项目正处于 **v0.8.0 发布队列**（#7112）与 **v0.8.1 集成队列**（#6970）并行的密集开发阶段，主要精力集中于 Bug 修复与核心功能成熟度提升。

---

## 3. 项目进展

### 🔧 高优 Bug 关闭（稳定性推进）
- **Ollama 工具调用失败**（#5962 — CLOSED）：修复了 Provider 在需要 tool-use 时阻塞会话的 S1 问题。
- **Windows Shell 双引号**（#7083 — CLOSED）：修复了 cmd.exe 参数转义导致命令执行失败的回归问题。
- **Twitter/X 编译特性遗漏**（#7069 — CLOSED）：`channel-twitter` feature 在预构建二进制中不生效的问题已修复。
- **RPC 会话空闲回收崩溃**（#7179 — CLOSED）：修复了聊天与 Code 会话在 10 分钟空闲后会被清理导致 session 丢失的 S1 问题。

### 🚀 核心 PR 递交（架构演进）
- **可观测性增强**（#7233 / @FTDGRT）：重构 ObserverEvent，增加 Channel/Agent/LLM IO 属性，打通 OTel Span 关联，是 #7232 RFC 的落地实现。对生产环境监控具有里程碑意义。
- **管理面板标签页**（#7229 / @theonlyhennygod）：为 Web UI 新增 MCP、Skills、Plugins、Providers 四个独立管理页面，大幅降低配置门槛。
- **Memory Strategy 统一**（#7234 / @fanchanghu）：将 Gateway WebSocket 与 Channel 整合至 MemoryStrategy 边界，完成 #6850 架构重构的第三阶段。
- **Web 斜杠命令**（#7223 / @NiuBlibing）：补齐 `/clear`、`/help`、`/model` 等 Web 聊天斜杠命令，实现与终端/TUI 渠道的体验对齐。
- **Web 后端历史清理**（#7222 / @NiuBlibing）：修复 "Clear all" 仅清除前端渲染而不删除后端 sqlite 历史的问题。
- **Telemetry WS 泄漏修复**（#7221 / @NiuBlibing）：阻断 SSE 监控事件误入聊天 WebSocket 的根本原因。
- **ESP32 仿真器**（#7048 / @Rhoahndur）：新增 `esp32_sim` 二进制仿真器与 Web 前端，推进硬件交互闭环。

---

## 4. 社区热点

| Issue/PR | 热度信号 | 核心诉求 |
|---|---|---|
| **#3566 — A2A 协议支持** | 5 条评论 · **👍 7** | 跨实例/跨项目智能体互操作，Linux Foundation 标准。**仍处于 blocked 状态，但社区期待极高**，是判断项目长期生态吸引力的关键。 |
| **#6909 — 计算机交互 (Computer-Use)** | 5 条评论 · `status: accepted` | 要求像 OpenAI Codex/Peekaboo 那样支持屏幕截图与键鼠事件。已被接受进入路线图，代表 ZeroClaw 向通用桌面 Agent 迈进的重要信号。 |
| **#7155 — Shell 命令策略 (Allow/Ask/Deny)** | P1 RFC · 2 条评论 | 提议参考 Claude Code 的分层命令策略，解决当前粗糙的权限控制。**反映了社区从“能用”到“安全可控”的升级诉求**。 |
| **#7143 — Slack Agent 陷入 Shell 循环** | 详细用户反馈 | 用户 `sbenedetto` 在现场部署中遇到 `max_tool_iterations` 被重复命令耗尽的问题，并称赞 ZeroClaw 资源占用优于同类系统：*"lighter on resources than many other agent systems we have tried."* |

---

## 5. Bug 与稳定性

### 🚨 严重（S1 — 流程阻塞）

| 编号 | 状态 | 摘要 | 备注 |
|---|---|---|---|
| **#7236** | 🟡 新开 | `workspace_dir` 错误传递导致 `load_skills_for_agent` 失败 | 暂无修复 |
| **#7125** | 🟡 新开 | TUI 在守护进程断开后完全冻结，需强制退出 | 暂无修复 |
| **#7227** | 🟡 新开 | zerocode Quickstart 硬编码 Provider 别名为 `default`，与已有 Provider 冲突 | 暂无修复 |
| #7083 | ✅ 已关闭 | Windows Shell 双引号参数转义失败 | 已修复 |
| #7179 | ✅ 已关闭 | RPC 空闲会话 10 分钟回收导致 session 丢失 | 已修复 |

### ⚠️ 主要（S2 — 行为降级）

| 编号 | 状态 | 摘要 |
|---|---|---|
| **#7126** | 🟡 修复中 | Web "Clear all" 未清除后端历史 ➡ **#7222** |
| **#7151** | 🟡 修复中 | Telemetry tool_call 泄漏至聊天 WS ➡ **#7221** |
| **#7225** | 🟡 新开 | WhatsApp `mention_only` 模式下忽略直接回复 |
| **#7143** | 🟡 新开 | Slack Agent 重复执行相似 Shell 命令直至迭代上限 |

### 🔍 技术债务
- **#6074** — 跟踪 2026-03-28 回滚中丢失的 **153 个提交**（Created 2026-04-24），至今无审计归结方案，对历史功能完整性仍有潜在影响。

---

## 6. 功能请求与路线图信号

| 需求 | 优先级 | 阶段 | 分析 |
|---|---|---|---|
| **#7112 — v0.8.0 发布队列** | — | 追踪器活跃 | Config 破坏性变更、Tool-Call-Parser 升 Stable 是最后拦路石 |
| **#6970 — v0.8.1 集成队列** | — | 追踪器活跃 | 渠道/Provider/Tool 集成工作有序推进 |
| **#6909 — 计算机操控** | P2 | `accepted` | 路线图已明确纳入，等待开发排期 |
| **#7155 — Shell 命令策略** | **P1** | RFC | 安全硬需求，有可能优先进入 v0.8.1 |
| **#7100 — Per-model 能力配置** | **P1** | RFC | 企业级部署对标 OpenAI 灵活度的高优先级需求 |
| **#5907 — LSP 支持** | P2 | blocked | 开发受阻，社区仍持续关注 |
| **#5797 — TLS CA 证书** | — | 已有 PR | 企业私钥 PKI 环境硬需求，PR 等待合并评审 |
| **#7138 — Web 文件上传 UI** | P2 | 已提案 | 配合 #6819 文件协议的上层体验补齐 |
| **#7228 — Azure reasoning_effort** | — | 已提案 | 生态兼容性细节，GPT-5 系列用户在等 |

---

## 7. 用户反馈摘要

### 👍 正面评价
> *“Thank you for the project. It is great to see a Rust-based agent runtime that is much lighter on resources than many other agent systems we have tried.”*
> — **sbenedetto** (#7143，Slack 集成场景)

### 💡 典型痛点
- **Windows 平台体验差距**：双引号已修复，但 TUI 断连无响应（#7125）、Quickstart 别名冲突（#7227）等问题仍在。Windows 用户增速显著，平台适配需要持续投入。
- **Agent 循环与可控性不足**：Slack 用户实际遭遇工具调用死循环（#7143），安全策略 RFC（#7155）与可观测性 PR（#7233）都指向 **"要让 Agent 行为看得见、管得住"** 的核心诉求。
- **Web UI 基础功能缺失**：Clear all 只删前端（已修）、无斜杠命令（已修）、无文件上传（待修），社区对 Web 渠道的完善期待明显高于 CLI/TUI。

### 👎 客观抱怨
- **#7211** — 抱怨仓库体积过大（虽被快速关闭，但反映了初次使用者的直观感受）

---

## 8. 待处理积压

### ⏳ 长期未响应的核心 Issue
| 编号 | 创建 | 状态 | 说明 |
|---|---|---|---|
| **#6074** | 2026-04-24 | 🟡 活跃 | 153 个提交丢失审计 — **40 天无归结方案**，建议维护者加快审查节奏 |
| **#3566 (A2A)** | 2026-03-15 | 🔴 Blocked | 高赞核心特性，超过 2 个月未推进，建议发社区更新说明预期 |
| **#5907 (LSP)** | 2026-04-19 | 🔴 Blocked | Coder Agent 关键能力，同样长期阻塞 |
| **#5797 (TLS CA)** | 2026-04-16 | 🟢 已有 PR | PR 存在但未合并，影响企业级自托管部署 |

### ⚡ PR 队列膨胀风险
当前 **39 个 PR 处于待合并状态**。虽然反映了极高的贡献热情，但容易滋生冲突并拖慢 Reviewer 反馈周期。建议近期组织 **"PR Review Day"** 集中处理低风险/文档/小型修复 PR，避免 merge hell。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*