# OpenClaw 生态日报 2026-05-30

> Issues: 330 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-30 02:47 UTC

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

# OpenClaw 项目动态日报 | 2026-05-30

## 1. 今日速览

OpenClaw 项目在过去 24 小时内呈现出极高的发版强度和社区活跃度。项目组共处理了 **330 条 Issue 更新**（其中关闭 174 条）和 **500 条 PR 更新**（其中合并/关闭 165 条），并连续发布了 4 个 Beta 热修版本。项目当前的核心节奏是 **围绕 Codex 运行时（Runtime）的稳定性进行密集攻坚**。虽然开发组响应迅速、修复推送极快，但大量 P1 级回归问题和持续爆出的内存泄漏/文件句柄泄漏表明，项目在经历了大规模架构变更（特别是 Codex 集成）后，正处于 **“高迭代、高风险”的震荡修复期**。活跃的开发态势下，项目的运行稳定性与系统性技术债务是需要高度关注的健康度指标。

## 2. 版本发布

**v2026.5.28-beta 系列（含 Beta.1—Beta.4）**

- **核心目标：** 强化 Agent 和 Codex 运行时恢复能力，修复 Beta 期间暴露的关键状态管理问题。
- **变更摘要：**
  - **子进程隔离**：子代 Agent（Subagents）保持单独的工作目录（cwd）与工作空间（workspace）分离，避免上下文污染。
  - **Hook 作用域限制**：Hook 执行上下文严格限定在 prompt-local 级别。
  - **锁机制修复**：会话在超时中止后确保释放文件锁（session locks）。
  - **重启状态安全**：避免因异常重启导致的过期延续（stale restart continuations）被意外执行。
  - **Codex 故障隔离**：Codex 应用服务器或 Helper 的故障不再连带摧毁共享运行时状态。

- **破坏性变更与迁移提醒：**
  - **⚠️ 破坏性变更：** 外部无明确 Breaking Change 声明。但根据社区大量反馈（`#84038`, `#88102`），本次更新对 `openai-codex/` 或 `openai/gpt-5.5` 路由的处理方式发生了根本变化。升级后若配置未同步更新，极易触发 **OAuth 认证失败、Token 用量暴增、模型路由被拒绝** 等问题。
  - **建议操作：** 所有持有 `openai-codex` 或 Codex 代理相关配置的用户，升级后务必执行 `openclaw doctor --fix`，并重新验证 OAuth Profile 与模型路由是否匹配。切勿在无备份的情况下直接覆盖生产环境配置。

## 3. 项目进展

- **基础设施推进**
  - `#87796 [CLOSED]` — **CI 自动化**（RomneyDa）：自动清理依赖锁文件（lockfile-only）的变更，提高供应链安全性。
  - `#65023 [CLOSED]` — **Google 统一 SDK**（zeroasterisk）：合并了 `@google/genai` SDK 集成，同时支持 Google AI Studio 和 Vertex AI，降低用户维护成本。
  - `#88200 [OPEN]` — **任务状态持久化**（steipete）：将 Task/Flow 状态迁移到共享 SQLite，提升崩溃恢复能力。
  - `#88210 [OPEN]` — **Session 写锁保护**（IYENTeam）：引入跨进程文件锁，防止并发写冲突导致数据损坏。

- **Codex 与 MCP 稳定性大修**
  - `#88206 [OPEN]` — **工具调用去重**（litang9）：为 Codex 动态工具调用添加合并器（Coalescer），防止同一工具回调被重复触发。
  - `#88207 [OPEN]` — **线程溢出旋转修复**（fuller-stack-dev）：修复原生 Codex 线程循环溢出后无法自动旋转的问题。
  - `#87879 [OPEN]` — **上下文溢出恢复**（fuller-stack-dev）：弥补了 Codex 在上下文爆满时预算跳过路径的缺口。
  - `#88172 [OPEN]` — **MCP 孤儿进程清理**（promptclickrun）：在 Session 销毁时杀死孤立的 MCP 子进程，并在传输中断时自动重连。
  - `#88177 [OPEN]` — **Codex 流式超时**（keshavbotagent）：修复 post-tool 编辑过程中因缺少进度事件导致的流式超时问题。
  - `#87981 [OPEN]` — **Cron 超时 MCP 退役**（Jerry-Xin）：在 Cron 任务超时或销毁时正确退役关联的 MCP 运行时，释放并发槽位。

- **前沿功能合并/推进**
  - `#81851 [OPEN]` — **Anthropic `claude-cli` 交互代理**（anagnorisis2peripeteia）：允许通过本地 HTTPS MITM 代理流式传输 Anthropic 推理过程。
  - `#82596 [OPEN]` — **执行拒绝列表**（JuanHuaXu）：全新的安全功能，可配置命令拒绝列表，填补“完全批准”与“完全 YOLO”之间的空白。

## 4. 社区热点

- **Codex/OpenAI 路由与 OAuth 迁移风暴**（评论高密度区）
  - `#84038 [CLOSED]`：`doctor --fix` 将 `openai-codex/` 配置**错误迁移**为 `openai/`，导致 PI+OAuth 运行时失效，Token 用量暴涨 3-4 倍。
  - `#86820 [CLOSED]`：Codex OAuth 压缩失败后回退到直连 OpenAI，因缺少 `OPENAI_API_KEY` 直接崩溃，无优雅降级。
  - `#88102 [CLOSED]`：`openai/gpt-5.5` 被 Codex 运行时拒绝，使用 `codex/gpt-5.5` 绕过又导致 `/status` 命令失效。
  - **分析：** 核心痛点在于 **“配置状态与运行时状态的同步机制过于脆弱”**，`doctor --fix` 本应是救命稻草却沦为破坏者，用户信任度受到极大打击。

- **渠道兼容性失控（跨平台体验退化）**
  - `#67035 [OPEN]`：Windows 网页 UI 输入被吞、流式回复不可见（13条评论，钻石龙虾级）。
  - `#87177 [OPEN]`：QQBot 心跳会话输出非标内容，导致消息频繁重复（11条评论）。
  - `#87646 [OPEN]`：飞书（Feishu）升级后完全无法分发消息（`read property 'run' of undefined`）（7条评论）。
  - `#77576 [OPEN]`：Telegram 群聊响应路由到 WebChat 返回，而不是 Telegram（7条评论）。

## 5. Bug 与稳定性

**致命级（Platinum Hermit / P1）**

| Issue | 标题 | 领域 | 状态 | 修复 PR |
|-------|-------|------|------|--------|
| `#86613` | `memory_search` 每次调用泄漏 N 个 FD，直至耗尽 | Memory | **Closed** | 已随 Beta 修复 |
| `#86358` | 上下文自动压缩导致 Event-loop 饥饿（17s 延迟） | Gateway | **Closed** | 已修复 |
| `#87744` | Codex Telegram 登录持续超时，`turn/completed` 永远不到达 | Codex/Telegram | **Open** | 暂无 |
| `#87646` | Feishu 升级后无法分发消息 | Feishu | **Open** | 暂无 |
| `#86948` | **Beta 阻塞器**：Codex app-server 静默丢消息 | Codex | **Closed** | `#87879` |

**严重级（Diamond Lobster / Gold Shrimp / P1-P2）**

| Issue | 标题 | 领域 | 修复 PR |
|-------|-------|------|--------|
| `#54155` | Gateway 内存泄漏 389MB → 14.7GB（持续4天） | Core | 长期开放 |
| `#87436` | Codex 自动重建 `doctor --fix` 已修复的路由状态 | Codex | 暂无 |
| `#87711` | 首轮 Telegram 对话助手回复为空（`— out`） | Telegram | 暂无 |
| `#86509` | Event-loop 饥饿在 v5.22 回归 | Core | 已关闭（待验证） |
| `#85953` | `sessions_yield` 导致父 Session 写锁未释放 | Agent | `#85953` PR |

**稳定性总结：**
- **最集中的风险领域**：Codex 运行时 ≠ 稳定。Token 用量异常、路由拒绝、流式超时、OAuth 状态丢失是压倒性的高发问题。
- **系统运行隐患**：内存泄漏、FD 泄漏、Event-loop 饥饿是服务器端长期运行的“慢性病”，虽有多次针对性的修复，但仍反复出现。
- **反馈闭环**：项目组对 Bug 的响应非常快，大量重度 Issue 在 24h 内被打上 `linked-pr-open` 标签，体现了极强的战斗力和社区重视度。

## 6. 功能请求与路线图信号

- **高概率纳入下一版本：**
  - **Slack 弹窗支持**（`#88154`）：用户请求增加 Slack Modal 原生 UI 表单输入。同期 `#87667 PR` 开放了 Slack DM 会话折叠，Slack 系列功能正在形成完整方案。
  - **执行拒绝列表**（`#82596 [OPEN]` PR）：安全功能呼声极高，PR 已进入深度审查。将直接解决 approval 审批疲劳与完全放开之间的取舍。
  - **Browser Vision 截图理解**（`#84247 [OPEN]` PR）：让纯文本模型也能理解截图内容，这项功能一旦合入将立刻激活大量 Browser-use 工作流。
  - **Telegram 交错进度通道**（`#87072 [OPEN]` PR）：将推理过程输出到单独的进度消息，提升 Chat UX。

- **长期 Waiting：**
  - **Per-Agent Dreaming**（`#67413`）：存在4个月，核心内存管理刚需，仍处于 `needs-product-decision`。
  - **ZAI/Gemini 原生 Web Search**（`#17925`）：标记为钻石龙虾级，3个月未推进，可能受限于上游 API。
  - **TUI 多行输入**（`#10118`）：评价很高但优先级低（P3），可能在 TUI 重构时顺带解决。

## 7. 用户反馈摘要

- **高频负面反馈（痛点）**
  - **“升级即失控”**：用户对 `openclaw doctor --fix` 破坏配置、升级后渠道插件失灵、Codex 路由随机拒绝感到极度沮丧。版本间的平滑度是当前的严重失分项。
  - **“长期泄漏不治本”**：尽管热修很多，但 core gateway 的内存泄漏（`#54155`）和 memory_search 的 FD 泄漏（`#86613`）让生产环境管理者对长期运维缺乏信心。
  - **“文档与事实脱节”**：部分用户反映发行说明与实际使用不符，导致升级前无法评估风险。

- **正面反馈**
  - **修复速度令人印象深刻**：多数 P1 级 Issue 在提出后 24h 内就被贴上 `linked-pr-open` 或通过热修 Beta 修复，用户能切身感受到开发组的投入。
  - **功能想象力丰富**：用户对 Anthropic CLI 代理、MCP 生态、联合搜索等功能抱有强烈期待，认为 OpenClaw 走在个人 AI 助手的正确方向上。

## 8. 待处理积压

- `#54155` **[Gateway 内存泄漏]**：P1 / 2026-03-24 / 持续4个月 / 仍然是影响长周期运行的最大定时炸弹。
- `#62328` **[FTS5 模块缺失]**：P2 / 2026-04-07 / 内置 SQLite 不支持 FTS5，导致记忆关键词检索全面失效。
- `#17925` **[ZAI/Gemini 原生 Web Search]**：P2 / 2026-02-16 / 顶级 Feature Request，长期无实质性进展。
- `#80607` **[多 Agent 启动延迟]**：P2 / 2026-05-11 / 非默认 Agent 触发 `embedded_run` 导致 10-17s 延迟，标记为 `stale`。
- `#67413` **[Per-Agent Dreaming 配置]**：P2 / 2026-04-15 / 解决记忆 spikes 引起 OOM 的刚需优化，等待产品决策。
- `#10118` **[TUI 多行输入]**：P3 / 2026-02-06 / 用户呼声高但优先级低，尚未排入迭代周期。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告 (2026-05-30)

---

## 1. 生态全景

过去 24 小时，个人 AI 助手与自主智能体开源生态呈现出 **“高并发迭代、安全与稳定性并重、架构分化加速”** 的整体态势。头部项目（OpenClaw）单日 PR 更新量突破 500，但架构变更引发的回归与内存问题使其处于震荡修复期；安全审计与加固成为普遍优先级（NanoBot、Hermes、ZeroClaw 均涉及高危漏洞修复）；MCP 工具治理、多 Agent 通信协议（A2A/ACP）和跨平台渠道兼容性是多数项目共同争夺的技术制高点。与此同时，少量分支项目（TinyClaw、ZeptoClaw）陷入停滞，整体生态正从“功能堆叠”加速迈向“生产级可靠”，但大部分项目仍处于 beta 质量波动阶段。

---

## 2. 各项目活跃度对比

| 项目 | Issues 活跃数 | PR 活跃数 | 今日版本发布 | 健康度评估 |
|------|--------------|-----------|--------------|-----------|
| **OpenClaw** | 330 (更新) | 500 (更新) | v2026.5.28-beta.1~4 | 高活跃，架构震荡，稳定性风险高 |
| **Hermes Agent** | 50 (更新) | 50 (更新) | v0.15.2 | 极活跃，迭代健康，安全响应快 |
| **IronClaw** | 18 (更新) | 47 (更新) | 无 | 高质量重构，架构深水区，健康 |
| **ZeroClaw** | 19 (更新) | 46 (更新) | 无 (v0.8.0-beta-2 筹备) | 极高活跃，通道故障突出 |
| **CoPaw** | 45 (更新) | 31 (更新) | v1.1.10-beta.1 | 高活跃，社区参与积极 |
| **NanoBot** | 33 (更新) | 41 (更新) | 无 | 高活跃，安全加固积压 PR 多 |
| **NullClaw** | 3 (已关闭) | 9 (7合并) | v2026.5.29 | 较高活跃，热修复密集 |
| **LobsterAI** | 1 (新) | 14 (9合并) | 无 | 健康 (8/10)，渲染性能攻坚 |
| **NanoClaw** | 1 (新) | 7 (更新) | 无 | 中高活跃，轻量聚焦 |
| **Moltis** | 3 (更新) | 2 (更新) | 无 | 中等活跃，环境适配挑战 |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 无 | 停滞 / 无活动 |

> 注：活跃数指过去 24 小时产生更新的 Issue/PR 总量（包含关闭/合并），部分项目明确给出新开数量。

---

## 3. OpenClaw 在生态中的定位

**规模与节奏领先，稳定性代价显著。** OpenClaw 以单日 330 Issue、500 PR 的体量稳居生态社区活跃度首位，连续发布 4 个 Beta 热修，具备极强的修复执行力。但其核心挑战在于：

- **优势**：深度集成 Codex 运行时，快速跟进最新模型能力；社区反馈闭环极快（P1 级 Bug 24h 内关联 PR）；子进程隔离、Hook 作用域限制等架构探索领先。
- **劣势**：配置状态与运行时的同步机制脆弱（`doctor --fix` 引发 OAuth 失效、Token 暴涨）；内存泄漏/FD 泄漏反复出现；升级断裂感强，用户信任度受挫。

**与同类对比**：
- **Hermes Agent** 在审批体系、Docker 部署成熟度上更稳健，MCP 安全漏洞修复更彻底；
- **NanoBot** 以系统性安全审计和模型预设为特色，但 PR 积压严重；
- **CoPaw** 在渠道深度（飞书、桌面、定时任务）和插件生态上领先，beta 版本更平顺；
- **ZeroClaw** 在工具治理（MCP 过滤、Risk Profile）和成本优化上更激进。

OpenClaw 在生态中扮演 **“前沿试验场”** 角色，但生产环境用户需承受较高的迭代风险。

---

## 4. 共同关注的技术方向

以下方向至少被 3 个及以上项目涉及，是当前生态的共同痛点与机遇：

| 技术方向 | 涉及项目 | 具体诉求 / 现象 |
|----------|----------|----------------|
| **MCP 工具安全与生命周期** | OpenClaw, NanoBot, Hermes, NanoClaw, ZeroClaw, CoPaw | 孤儿进程清理、SSRF 绕过、审批绕过、供应链风险、过滤失效、配置继承缺失 |
| **对话记忆与上下文管理** | OpenClaw, NanoBot, NullClaw, CoPaw, ZeroClaw | 内存泄漏、短期记忆丢失、全局记忆不可见、向量索引膨胀、MemoryStrategy 抽象 |
| **跨平台渠道稳定性** | OpenClaw, Hermes, ZeroClaw, CoPaw, NanoClaw, NullClaw | Telegram/飞书/Slack 发信失败、流式不可见、心跳断连、配置升级后渠道失灵 |
| **成本控制与性能优化** | Hermes, ZeroClaw, LobsterAI, OpenClaw | 惰性工具加载、分类器 Provider 降成本、大输出渲染卡死、Token 用量异常 |
| **Agent 互操作协议** | Hermes (A2A), NullClaw (ACP), CoPaw (子智能体), OpenClaw (子进程隔离) | 跨 Agent 发现与通信、标准化传输（stdio/RPC）、子 Agent 生命周期管理 |
| **安全认证与配置健壮性** | OpenClaw, NanoBot, Hermes, ZeroClaw, NanoClaw | OAuth 状态丢失、API 未授权、Cron 安全注入、配置静默回退、E2EE 缺失 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 核心架构/技术栈差异 |
|------|----------|----------|-------------------|
| **OpenClaw** | Codex 运行时深度集成，全功能框架 | 追求前沿模型的开发者 | 高度插件化，OAuth+Codex 路由复杂，迭代极快 |
| **Hermes Agent** | 安全审批体系、Docker 优先、A2A 协议 | 企业级部署与多 Agent 协同 | 多层安全网关（approval.py），强调可审计与降级 |
| **IronClaw** | “Reborn”架构重构、产品级认证、可观测性 | 需要统一认证与 WebUI 的团队 | Rust 实现，认证系统全面重构，设计先于代码 |
| **ZeroClaw** | 工具治理（MCP 过滤/ Risk Profile）、成本优化、SGR 推理 | 高阶 Agent 工作流管理 | 配置驱动的工具沙箱，classifier_provider 成本分流 |
| **CoPaw** | 渠道深度集成（飞书/桌面/定时）、插件系统、类 IDE 编辑 | 重度办公与协同用户 | 丰富的 channel 适配器，对标 Trae 工作流 |
| **NanoBot** | 安全性审计、模型预设、Provider 兼容性 | 生产环境安全敏感用户 | 系统化安全修复（SSRF/并发锁），27 个待合并 PR |
| **NullClaw** | 原生 ACP 协议、高性能 Zig 实现 | 协议标准化与性能敏感场景 | Zig 语言构建，轻量级，stdio ACP 传输 |
| **LobsterAI** | 渲染性能、大输出抗阻塞、UI 防丢失 | 终端交互体验优先 | Gateway WS 心跳优化，Markdown 懒渲染 |
| **NanoClaw** | 安全工具生态（Gmail）、轻量集成、v2 安全架构 | 办公自动化与安全合规 | OneCLI 凭证注入，不存储裸 API 密钥 |
| **Moltis** | Skill 精细控制、Sandbox 环境、异构兼容 | 开发者工具与 Docker sandbox 用户 | arm64 与企业代理支持为当前瓶颈 |

注：TinyClaw/ZeptoClaw 无活跃数据，不做定位分析。

---

## 6. 社区热度与成熟度分层

### 第一梯队：快速迭代期（日 PR > 30，Issue > 30）
- **OpenClaw, Hermes Agent, IronClaw, ZeroClaw, CoPaw, NanoBot**
- 共性：社区参与度极高，大型 PR 批量合并，同时出现较多回归/安全 Bug。维护者响应速度快，但 backlog 压力大（NanoBot 27 个待合并 PR，OpenClaw 核心泄漏问题持续 4 个月）。

### 第二梯队：质量巩固 / 聚焦期（日 PR 5–20，Issue 1–10）
- **NullClaw, LobsterAI, NanoClaw, Moltis**
- 共性：迭代数量较少但针对性强，多为功能合入或专项修复（如 LobsterAI 渲染优化、NullClaw 子代理修复）。社区规模较小但贡献者质量高。

### 第三梯队：停滞期
- **TinyClaw, ZeptoClaw**：24 小时零活动，项目可能处于维护休眠状态。

**成熟度评价**：Hermes Agent 与 CoPaw 在版本平滑度、文档一致性上表现较好；OpenClaw 与 ZeroClaw 虽活跃但破坏性变更频发，属于“先发后稳”模式；IronClaw 处于大型重构但设计先行，技术债务清理较主动。

---

## 7. 值得关注的趋势信号

1. **安全左移成为标配**  
   命令拒绝列表（OpenClaw #82596）、MCP 工具过滤（ZeroClaw #6699）、SSRF 统一校验层（NanoBot #4074）等表明安全正从外围配置深入架构内核。AI Agent 权限管控即将成为落地必备条件。

2. **Agent 互操作协议从提案走向代码**  
   Hermes 社区对 A2A 的持续高赞（👍12）、NullClaw 原生 ACP stdio 合并，预示多 Agent 网格通信将在 1–2 个版本内成为主流项目的标准能力。

3. **Provider 抽象与经济性优化加速**  
   模型预设（NanoBot #3696）、分类器 Provider（ZeroClaw #6945）、惰性工具加载（Hermes #6839）表明用户对灵活路由和成本控制的诉求远高于单纯的功能堆叠。

4. **渠道体验决定用户留存**  
   跨渠道（Telegram/飞书/Slack/微信）的频繁故障成为多数项目的失分项，而 CoPaw 和 NullClaw 在渠道上下文增强上的快速合入，说明优化渠道黏性已上升为竞争优势。

5. **记忆与上下文管理走向模块化/可配置**  
   手动记忆模式（NanoBot #4050）、MemoryStrategy 特征（ZeroClaw #6907）、Per-Agent Dreaming（OpenClaw #67413）等信号显示，记忆系统正从“黑盒自动”转向“用户可干预的策略层”，长对话场景的基础设施正在成熟。

6. **可观测性从加分项变为必备项**  
   LangFuse 集成（IronClaw #2456）、推理摘要保存（IronClaw #4230）、流式进度通道（OpenClaw #87072）反映出开发者调试和信任 Agent 行为的需求急剧上升。

---

*本报告基于 2026-05-30 各项目公开 GitHub 动态生成，数据截至 UTC 时间 2026-05-30 23:59。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 开源项目日报 (2026-05-30)

## 1. 今日速览

过去 24 小时内，NanoBot 项目经历了一次罕见的“高强度压力测试”。社区产生了 **33 条 Issue** 和 **41 条 PR** 更新，极为活跃。贡献者 `hamb1y` 主导了一场系统的安全审计与稳定性修复运动，一次性提交了十余个涉及 SSRF 绕过、API 未授权、并发死锁等深层漏洞的报告及配套修复 PR。

**活跃度评估：极高 (Intense)。** 项目处于深度加固与架构稳定化阶段。虽然大量安全问题的暴露看起来令人警醒，但所有严重 Bug 几乎都有对应的修复 PR 正在排队，社区响应速度与开发效率非常亮眼。当前风险在于 27 个待合并 PR 对审查者构成了显著的 backlog 压力。

---

## 2. 版本发布

**无。** 当前未发布新版本，代码库正处于高密度的修复积累期，预计下一版本将是包含重大安全升级和架构重构的版本。

---

## 3. 项目进展

**昨日合并/关闭的重要 PR：**

- **功能里程碑——模型预设：** [PR #3696](https://github.com/HKUDS/nanobot/pull/3696) `feat(config): add model presets` 已合并。用户现可预设多组模型配置并实现自动故障转移，极大提升了多 Provider 切换的灵活性。
- **跨平台修复——Windows Exec：** [PR #4051](https://github.com/HKUDS/nanobot/pull/4051) `fix(exec): bypass cmd.exe for multi-line commands on Windows` 已合并。解决了 Windows 下多行 Python 命令被 `cmd.exe` 截断的问题，改用 PowerShell 执行。
- **“社区审计”修复管道已就绪：** 贡献者 `hamb1y` 提交了从 [#4088](https://github.com/HKUDS/nanobot/pull/4088) 到 [#4104](https://github.com/HKUDS/nanobot/pull/4104) 的系列修复。这批 PR 一旦合并，将系统性解决目前代码库中最棘手的并发安全与权限绕过漏洞，覆盖 Session 存储、Tool Call 协议、Provider 适配等多个核心模块。

**项目迈向：** 昨日合并的功能表明项目在通过**模型路由与模型预设**优化核心 LLM 交互体验；而大规模并发修复和权限加固表明项目正在全力提升**生产环境安全性**与**数据完整性**。

---

## 4. 社区热点

- **最活跃贡献者：`hamb1y` 安全审计风暴：** `hamb1y` 无疑是今日的社区焦点。他发起的议题覆盖了安全、并发、数据一致性等多个维度，且全部附带了详细的 Root Cause 分析和修复代码。这种“发现-分析-修补”的高质量闭环贡献模式是开源社区最良性的互动体现。相关 Issue/PR： [#4072](https://github.com/HKUDS/nanobot/issues/4072) ~ [#4104](https://github.com/HKUDS/nanobot/pull/4104)。
- **最高讨论度 Issue——短期记忆丢失：** [Issue #4044](https://github.com/HKUDS/nanobot/issues/4044) `[Bug] short term memory loss` 收到最多评论（4条）。用户 `bjoshuanoah` 详细描述了系统提示词（SOUL.md, MEMORY.md 等）膨胀挤压上下文窗口，导致模型在对话中频繁“失忆”的痛点。
- **开发者焦点——工具调用解析：** 围绕 OpenAI 兼容 Provider 的文本格式 Tool Call（[#4061](https://github.com/HKUDS/nanobot/issues/4061)）和 Anthropic Block 规范化（[#4060](https://github.com/HKUDS/nanobot/issues/4060)）的讨论表明，社区正在大量使用非标准或边缘 Provider，对协议适配的健壮性要求极高。

**趋势分析：** 社区诉求正在从“增加功能”转向“打磨稳定性和安全性”。长时间运行的聊天会话的管理策略以及第三方 Provider 的兼容性是用户目前最关心的两个问题。

---

## 5. Bug 与稳定性

以下按严重程度排列，并标注修复进度：

### 🔴 严重（安全漏洞，均已有 Fix PR）

| Issue ID | 问题描述 | 风险点 | Fix PR |
|---|---|---|---|
| [#4078](https://github.com/HKUDS/nanobot/issues/4078) | OpenAI 兼容 API 接口接受未认证请求 | 外部攻击者可无需认证直接调用 Agent | [#4103](https://github.com/HKUDS/nanobot/pull/4103) |
| [#4074](https://github.com/HKUDS/nanobot/issues/4074) | MCP HTTP/SSE 配置 SSRF 绕过 | 可对内网资源进行探测 | [#4100](https://github.com/HKUDS/nanobot/pull/4100) |
| [#4076](https://github.com/HKUDS/nanobot/issues/4076) | 消息工具缺乏外发目标授权 | 可向未授权频道发送消息/附件 | [#4102](https://github.com/HKUDS/nanobot/pull/4102) |
| [#4072](https://github.com/HKUDS/nanobot/issues/4072) | ExecTool 工作空间限制可通过相对软链接绕过 | 逃逸沙箱读取/执行外部文件 | [#4098](https://github.com/HKUDS/nanobot/pull/4098) |

### 🟠 严重（数据损坏/并发问题，均已有 Fix PR）

| Issue ID | 问题描述 | 后果 | Fix PR |
|---|---|---|---|
| [#4080](https://github.com/HKUDS/nanobot/issues/4080) | `process_direct` 绕过每会话调度锁 | 直接调用与调度队列并发运行导致历史错乱 | [#4104](https://github.com/HKUDS/nanobot/pull/4104) |
| [#4081](https://github.com/HKUDS/nanobot/issues/4081) | `MemoryStore.append_history` 并发写入分配重复游标 | JSONL 文件数据重叠或覆盖 | [#4088](https://github.com/HKUDS/nanobot/pull/4088) |
| [#4082](https://github.com/HKUDS/nanobot/issues/4082) | Cron 任务复用固定会话上下文 | 多次调度执行状态互相污染 | [#4094](https://github.com/HKUDS/nanobot/pull/4094) 关联 |

### 🟡 中等（兼容性与功能异常，包含修复或讨论中）

| Issue ID | 问题描述 | Fix PR/状态 |
|---|---|---|
| [#4061](https://github.com/HKUDS/nanobot/issues/4061) | OpenAI 兼容 Provider 的文本格式 Tool Call 未被解析 | [#4092](https://github.com/HKUDS/nanobot/pull/4092) |
| [#4060](https://github.com/HKUDS/nanobot/issues/4060) | Anthropic Provider 缺失必需的 `type` 字段 | [#4093](https://github.com/HKUDS/nanobot/pull/4093) |
| [#4067](https://github.com/HKUDS/nanobot/issues/4067) | 无效配置静默回退默认值 | [#4095](https://github.com/HKUDS/nanobot/pull/4095) |
| [#4044](https://github.com/HKUDS/nanobot/issues/4044) | 短期内存丢失（上下文窗口压力） | 待架构层面解决 |

---

## 6. 功能请求与路线图信号

- **记忆系统分裂为手动模式：** [PR #4050](https://github.com/HKUDS/nanobot/pull/4050) `feat: add manual memory mode` 在讨论中。这代表记忆系统正在走向模块化，允许用户选择“手动” vs “自动”记忆模式，解决当前自动记忆“黑盒”问题。这是对应 #4044 内存丢失问题的长线架构方案。
- **配置控制力的加强：** Issue [#4043](https://github.com/HKUDS/nanobot/issues/4043) `[Config to disable document extraction]` 已被关闭（enhancement），映射了用户对“自动文档注入”行为的控制需求。结合 PR #3696 的合并，路线图信号指向**更强的可配置性与模块化**。
- **工具生态的安全策略：** 基于 `hamb1y` 的系列修复，项目很可能将在下一版本引入**路径白名单读写分离**、**出站消息授权**以及**统一的 SSRF 校验层**，大幅强化 Agent 的沙箱边界。

---

## 7. 用户反馈摘要

- **困惑与挫败感（上下文管理）：** Issue [#4044](https://github.com/HKUDS/nanobot/issues/4044) 作者表达了对“系统提示词太大导致对话失忆”的明显困惑。用户期望模型能记住刚问过的与刚回答的上下文，这在长对话中是核心体验痛点。
- **跨平台加密体验不佳：** Issue [#4042](https://github.com/HKUDS/nanobot/issues/4042) 用户反馈在 Element X (Matrix 客户端) 中每次收到加密消息都显示“未验证设备”。这意味着 Nanobot 目前**没有处理端到端加密（E2EE）的密钥验证流**，对于隐私敏感用户来说是一个关键的体验阻塞项。
- **Edge Case 兼容性压力：** 从 #4061、#4060 等 Issue 可以看到，用户正在大量使用非 OpenAI 官方标准的 API 后端（如本地推理框架、第三方托管 API）。这些后端在 Schema 上存在细微偏差，导致稳定的“修复 Provider 层”需求非常强烈。

---

## 8. 待处理积压

- **⚠️ 紧急：安全修复 PR 审查积压**
  当前有 **27 个 PR** 处于 `OPEN` 状态并待合并。其中贡献者 `hamb1y` 提交的 [PR #4095](https://github.com/HKUDS/nanobot/pull/4095) 至 [PR #4104](https://github.com/HKUDS/nanobot/pull/4104) 直接针对高危急安全漏洞。建议维护团队在未来 24 小时内优先对这批 PR 进行审查和合入，以避免修复冲突、代码分歧或长期暴露攻击面。

- **需关注：长期遗留问题**
  - **#4044（短期记忆丢失）**：虽然目前已被新 Bug 的浪潮短暂淹没，但它是所有深度用户的共同痛点，建议纳入下一版本的路线图讨论。
  - **#4042（Matrix 加密验证）**：该议题目前只有发起者自己回复。鉴于 Matrix 是核心频道之一，E2EE 的兼容性是需要专门投入资源处理的深水区问题，不应被忽视。

- **审核建议：**
  - 优先合并 #4078、#4074 等安全问题修复。
  - 合并 #4080、#4081 的锁机制修复以保障数据稳定性。
  - 合并 #4092、#4093 的 Provider 兼容性修复以提升现有用户满意度。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent 项目数据生成的 2026-05-30 项目动态日报。

---

# Hermes Agent 项目动态日报 (2026-05-30)

## 1. 今日速览

过去 24 小时内，Hermes Agent 项目保持极高的活跃度。共计 **50 个 Issues**（新开/活跃 41，关闭 9）和 **50 个 Pull Requests**（待合并 35，已合并/关闭 15）得到更新，并发布了 **v0.15.2 补丁版本**。社区讨论热点高度集中，一方面对 A2A 跨 Agent 协议表示强烈期待，另一方面深度探讨了 Token 占用过高及惰性加载优化方案。Bug 修复方面，MCP 绕过审批系统的高危漏洞已通过今日合并的 PR 得到修补，同时修复了多个 Docker 和第三方网关的回归问题。整体来看，项目迭代极快，社区反馈敏锐，安全响应迅速，处于非常健康的高频演进状态。

## 2. 版本发布

**Hermes Agent v0.15.2 (v2026.5.29.2)**

-   **发布日期：** 2026年5月29日
-   **更新内容：** 修复了 `wheel` 和 `sdist` 安装包中未包含 `plugin.yaml` 清单文件的问题，确保插件机制在标准包管理下能正常运作。
-   **破坏性变更与迁移建议：** 无。此版本为纯 Bug 修复补丁，无需额外迁移步骤。
    -   链接：https://github.com/NousResearch/hermes-agent/releases/tag/v2026.5.29.2

## 3. 项目进展

今日项目在核心安全、Docker 部署体验和多平台兼容性上取得了实质性推进：

-   **核心安全体系加固：**
    -   **MCP 审批绕过漏洞彻底修复**：PR #33828 将 MCP (`ssh`, `docker` 等) 的 Shell 调用路由至 `approval.py` 审批系统，杜绝了 Agent 绕过安全网关执行危险命令的风险。关联 Issue #32877。
    -   **审批系统完整性修复**：PR #32705 修复了 “always_approve” 模式无法撤回以及 YOLO 模式绕过审计的问题，增强了权限审计的闭环。
-   **Docker 部署体验大幅提升：**
    -   修复了因启动脚本缺失 (`stage2-hook.sh`) 导致容器崩溃的问题 (Issue #34071)。
    -   修复了 `HERMES_UID=0` 配置无效的问题 (PR #35078)。
    -   修复了通过 `docker exec -u root` 创建文件导致权限错误的问题 (PR #35098)。
-   **平台兼容性修复：**
    -   修复了 macOS 环境下 `/private/var/` 路径前缀误伤临时目录的问题 (PR #35097)。
    -   针对 DingTalk 适配器添加了断线重连断路器，防止 SDK 故障引发无限日志风暴 (PR #24868)。
    -   修复了 Feishu (飞书) 审批卡片在 v0.15.0 升级后失效的问题 (PR #35090)。

## 4. 社区热点

-   **跨 Agent 协议 A2A 支持** (Issue #514)：以 **24 条评论、12 个 👍** 的热度持续占据榜首。用户希望 Hermes 能原生支持 Google 提出的 A2A 协议标准。这反映了社区对 Agent 间互操作性（发现、通信、协作）的核心诉求，是决定项目生态地位的关键特征。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/514
-   **惰性工具模式加载** (Issue #6839)：今日以 **20 条评论、13 个 👍** 成为评论区最活跃议题，也是 **👍 数最高的 Issue**。专业用户对每次 API 调用注入全部 50+ 工具 Schema（约 3500-5000 Token）的浪费现象表示强烈不满，提出的“两阶段注入”方案引发了深度技术讨论。这是当前性能优化的最强社区呼声。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/6839
-   **v0.15.0 升级后的副作用** (Issue #34071, #34091, #35032): 版本升级带来的 Docker 崩溃、Dashboard 断开、Feishu 审批失效等回归问题引发了大量用户关注，说明社区对升级平顺性和稳定性有着极高的要求。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/34071

## 5. Bug & 稳定性

**P1 严重等级 (Open):**

-   **Cron 安全注入检测不完善** (#35075)：运行时扫描器检测的不可见 Unicode 字符集少于安装时扫描器，存在被利用绕过安全检测的风险。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/35075
-   **微信 Cron 推送回归** (#35062)：从 v0.14 升级至 v0.15 后所有定时任务静默失败，严重影响用户依赖性。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/35062
-   **MCP 重载进程泄漏** (#34966)：每次 `/reload-mcp` 或网关重载都会衍生新进程但遗弃旧进程，可能导致服务端内存耗尽 (OOM)。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/34966
-   **Fallback 自动降级逻辑失效** (#32646)：当主模型遭遇 API 限流 (429) 时，备用模型无法按预期自动激活，影响服务连续性。
    -   链接：https://github.com/NousResearch/hermes-agent/issues/32646

**P2 中等等级 (Open):**

-   Feishu (飞书) 零管理员配置下审批按钮失效 (#35032)。
-   非默认 Profile 启动 SSH Gateway 因 HOME 目录未设导致的配置文件缺失 (#35059)。
-   Docker 环境下非默认 UID 导致的每次启动全量 Chown (#35025)。

**已关闭/修复：**

-   `MCP 绕过审批` (#32877) - 由 PR #33828 修复。
-   `v0.15.0 Docker 启动崩溃` (#34071) - 由 PR #35078/#35098 修复。
-   `Agent 空回复/截断` (#34452) 与 `静默消息循环` (#34616) 均已修复。

## 6. 功能请求与路线图信号

-   **长期路线图信号：**
    -   **A2A 协议** (#514)：呼声最高的功能，若落地将使 Hermes 从单 Agent 工具进化为多 Agent 网络节点，极有可能是下一阶段的核心方向。
    -   **原生 ACP 客户端传输** (#35063)：已有用户提交具体实现方案，希望增加纯 JSON-RPC 2.0 的 stdio 传输路径，体现了对现有 Shim 方案的不满足感。
-   **短期迭代热点（高价值）：**
    -   **惰性工具模式加载** (#6839)：基于社区高赞提案，极有可能被纳入下一个版本的核心优化项，以解决 Token 浪费痛点。
    -   **自动化推理回退** (#34786)：当模型不支持 `reasoning_effort` 参数时自动删除相关参数，提升多模型兼容性。
-   **运维与体验优化：**
    -   **Dashboard 远程访问配置** (#10567)：支持 `--host` 绑定与 CORS 白名单配置，提升家庭/企业网络部署体验。
    -   **分页记忆与关键词搜索** (#34745)：突破当前记忆系统 2200 字符上限，提供更精细的上下文管理。
    -   **macOS 终端换行支持** (#35057)：Shift+Enter 键盘映射丢失，影响多行输入体验。

## 7. 用户反馈摘要

-   **升级之痛显著：** 多条高关注度 Issue 直指 v0.15.0 大版本升级引发的兼容性断裂（Docker、Feishu、Weixin）。虽然团队修复迅速，但频繁的回归问题在一定程度上影响了用户的升级信心。
-   **安全警觉性高：** 社区对 MCP 绕过审批闸门的问题（#32877）反应强烈，用户普遍表达了在开放 Agent 权限后对“后门”行为的担忧，凸显了审批系统对 Agent 安全性的基石作用。
-   **对 Token 成本极度敏感：** 围绕惰性加载 (#6839) 的讨论中，专业用户（尤其是本地模型和 API 用户）对 Token 的浪费表现出极大焦虑，性能优化已不仅仅是锦上添花，而是影响用户留存的关键指标。
-   **跨 Agent 协作愿景强烈：** 尽管 A2A 协议 (#514) 落地复杂，但社区持续的讨论热度表明，用户期望 Hermes 能够融入更庞大的多 Agent 生态系统，而非停留在封闭的单体架构。

## 8. 待处理积压

-   **安全积压:**
    -   #35075 **Cron 安全注入扫描器字符集不完整**: 刚提交的 P1 级别安全问题，需快速响应以避免防线出现缺口。
    -   #34966 **MCP 进程泄漏**: P1 问题，严重影响长期运行的服务器稳定性，已开放两天无 fix PR。
-   **长期需求推进:**
    -   #514 **A2A 协议**: 已开放近 3 个月，社区期待维护组给出明确的路标回应或 Milestone 安排。
    -   #6839 **惰性工具模式加载**: 社区贡献度极高的提案，建议尽快纳入设计评审或提供官方态度，以指导社区贡献者。
-   **待合并 PR:**

    -   PR #24868 **DingTalk 断线重连修复**: 5月13日提交，已搁置超过 2 周，低优先级但长期存在的小痛点。
        -   链接：https://github.com/NousResearch/hermes-agent/pull/24868
    -   PR #35102 **Gateway 无限重启循环修复**: 今日提交，针对服务器稳定性问题，建议快速审核合并。
        -   链接：https://github.com/NousResearch/hermes-agent/pull/35102


</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，以下是根据 NanoClaw (github.com/qwibitai/nanoclaw) 2026-05-29 数据生成的 2026-05-30 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-05-30

## 1. 今日速览
- 项目今日保持 **高活跃度**：共产生 1 个新 Issue 和 7 个 PR 更新，社区贡献持续输出，其中 2 个重要 PR 被成功合并。
- 最值得关注的是，用户 **NoamGit** 提交了关于第三方 MCP 工具供应链安全风险的 Issue（#2641），直接引用了外部安全事件分析，敲响了 AI 自主执行代码安全性的警钟，预计将引发项目对沙箱机制的严肃讨论。
- 开发层面，**LangFuse 可观测性集成** 与 **OneCLI 原生 Gmail 工具** 的合并，标志着项目在“生产级部署能力”和“安全工具生态”上迈出了实质性的一大步。
- 社区贡献者 **yairixStudio** 今天密集提交了 3 个高质量的修复与功能 PR，覆盖了路由逻辑、Telegram 适配器及群聊上下文，体现了令人兴奋的社区共建深度。

## 2. 版本发布
- 无。项目正处于密集的功能合并期，暂无新版本发布。

## 3. 项目进展（关键进展与合并）
今日有 2 个关键 PR 被合并，显著提升了系统的可观测性与工具生态：
- **PR #1961 (已合并): skill(add-gmail-tool): OneCLI 原生 Gmail MCP 工具。**
  - **摘要：** 严格遵循 NanoClaw v2 的安全架构（容器不接收裸 API 密钥，仅通过 OneCLI 注入凭证），添加了 `/add-gmail-tool` 实用技能。
  - **意义：** 补齐了办公生态中极关键的 Gmail 集成，且是以最高安全标准实现的。这对希望在企业环境中部署 AI Agent 的用户至关重要。
  - [链接](https://github.com/nanocoai/nanoclaw/pull/1961)
- **PR #2456 (已合并): feat(langfuse): 为 Claude Provider 增加 LangFuse 可观测性。**
  - **摘要：** 在 `ClaudeProvider.query()` 中植入了 LangFuse 追踪，覆盖了 Agent 会话延迟、API 错误（重试与限流）、工具调用耗时及上下文压缩 Token 消耗。
  - **意义：** 使得开发者能够对 Agent 的性能瓶颈和错误模式进行可视化监控，距离生产级应用又近了一步。
  - [链接](https://github.com/nanocoai/nanoclaw/pull/2456)

## 4. 社区热点
- **Issue #2641 供应链安全风险 —— 今日讨论核心**
  - **概况：** 用户 NoamGit 报告名为 `@gongrzhe/server-gmail-autoauth-mcp` 的包存在供应链风险，并引用了外部分析文章（警告 AI 可能会在用户机器上安装陌生代码并索要 Gmail 密码）。
  - **分析：** 这是当前 AI Agent 领域最敏感的痛点之一。虽然目前暂无评论，但该 Issue 已经将“MCP 工具的安全审计”摆上了台面。社区潜在的诉求是希望项目方能提供官方的工具安全评分、沙箱运行机制或白名单策略。
  - [链接](https://github.com/nanocoai/nanoclaw/issues/2641)

- **yairixStudio 批量贡献 —— 贡献者标杆**
  - 贡献者 `yairixStudio` 一日内提交了 #2642、#2643、#2644、#2645 四个 PR，分别修复了 Telegram 适配器版本冲突、路由触发逻辑、回复上下文识别，并新增了群聊上下文窗口。这种深度的、系列化的贡献是项目社区健康度极高的信号。

## 5. Bug 与稳定性
- **严重安全风险 (Critical)**
  - **Issue #2641 (Open):** 第三方 MCP 工具 (`@gongrzhe/server-gmail-autoauth-mcp`) 可能存在恶意代码执行与凭证泄露风险。**目前无对应修复 PR，需维护者紧急介入评估与回应。**
  - [链接](https://github.com/nanocoai/nanoclaw/issues/2641)

- **构建与依赖问题 (High)**
  - **PR #2642 (Open / 已有Fix):** `/add-telegram` 安装脚本声明的 `@chat-adapter/telegram@4.27.0` 与项目根依赖 `chat@4.26.0` 不兼容，导致用户执行 `add-telegram` Skills 时可能失败。贡献者已提交修复 PR，将版本锁定为 `4.26.0`。
  - [链接](https://github.com/nanocoai/nanoclaw/pull/2642)

- **路由与逻辑缺陷 (Medium)**
  - **PR #2643 (Open / 已有Fix):** `evaluateEngage` 函数在 `pattern` 模式下，若消息是 `@提及` 或 `DM` 但不包含关键字，机器人会错误地保持沉默。修复后能正确响应直接寻址。
  [链接](https://github.com/nanocoai/nanoclaw/pull/2643)
  - **PR #2644 (Open / 已有Fix):** Telegram 中 `extractReplyContext` 无法区分“回复机器人的消息”与“普通回复”，导致上下文丢失。修复后增加了 `isReplyToBot` 标志。
  [链接](https://github.com/nanocoai/nanoclaw/pull/2644)

## 6. 功能请求与路线图信号
- **群聊上下文感知 (PR #2645):** 为群聊中的 Agent 组增加可选上下文窗口大小。当 Agent 被 `@提及` 时，自动携带最近 N 条未读消息作为上下文。这是实现多 Agent 群聊场景中流畅对话的关键特性，**很可能被纳入即将到来的小版本更新。**
  - [链接](https://github.com/nanocoai/nanoclaw/pull/2645)
- **应用扩展能力 (PR #2646):** 新增 `[codex]` 应用 “Street Wind & Shadow Map”，这是一个基于 OSM、Open-Meteo 和 Three.js 的完整地图可视化应用。虽然这看似是一个示例应用，但它展示了 NanoClaw 作为平台集成复杂前端应用的能力，暗示了路线图中“应用商店”或“扩展市场”的雏形。
  - [链接](https://github.com/nanocoai/nanoclaw/pull/2646)

## 7. 用户反馈摘要
- **安全焦虑（#2641）：** 用户 NoamGit 引用了真实的安全事故，警告同行不要轻易信任 AI 自动安装的代码，并直言“我的 AI 在我的机器上安装了陌生代码并索要我的 Gmail 密码”。这反映了资深开发者对 AI 安全边界的普遍担忧，以及对更强权限管控的渴望。
- **生态补全的热情（#1961反馈）：** Gmail 工具的合并获得了社区的现实需求支撑，用户期待更多标准化的、安全的生产力工具落地。
- **贡献者正面反馈（yairixStudio）：** 贡献者连续提交高质量 PR，是对项目架构、文档和贡献流程的无言认可，表明 NanoClaw 的 Onboarding 体验和代码设计非常优秀。

## 8. 待处理积压
- 目前不存在长期停滞的 Issue 或 PR。今日新开的 1 个 Issue 和 5 个待合并 PR 均处于非常新鲜的状态，说明项目维护者响应迅速，没有形成严重的积压。
- **重点关注：** **Issue #2641** 目前处于“已报告、维护者未回应”的状态。鉴于其安全严重性，维护者应尽快在 Issue 中给出初步回应（如确认问题、暂不认为高风险、或讨论解决方案），以平息社区顾虑并保持项目公信力。
  - [链接](https://github.com/nanocoai/nanoclaw/issues/2641)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 NullClaw 项目 2026-05-30 的 GitHub 动态生成的日报。

---

# NullClaw 项目动态日报 | 2026-05-30

## 1. 今日速览

今日项目活跃度**较高**，处于热修复与功能并进的密集开发期。24 小时内共处理 3 个 Issue（均已关闭）、9 个 Pull Request（合并/关闭 7 个），并正式发布了 **v2026.5.29** 版本。核心亮点包括：修复了 Telegram 子代理结果丢失、全局记忆不可见等影响面极大的关键 Bug；同时合入了 LINE 频道增强、Gateway 接口扩展及 Nix 构建修复。值得注意的是，仍有 2 个关于模型兼容性和配置一致性的 PR（#939、#940）正在等待合入，这两项直接影响用户体验与配置可靠性。

## 2. 版本发布：v2026.5.29

- **版本号**：v2026.5.29
- **发布链接**：点击查看 Release
- **主要更新内容**：
  1. **架构新增**：集成原生 **ACP（Agent Communication Protocol）stdio 适配器**，标志着项目向标准化 Agent 互操作协议迈出了第一步。
  2. **基础设施**：将 GitHub Actions 工作流迁移至 nullbuilder 组织，优化了 CI 构建流程。
  3. **Bug 修复捆绑**：该版本合入了近期的多项重要修复，包括 Telegram 频道增强、子代理投递修复和记忆工具修复（详见下文）。
- **破坏性变更/迁移注意**：暂无需要用户侧手动处理的破坏性变更。若你 Fork 了项目，建议检查并同步更新工作流文件。

## 3. 项目进展

- **频道层稳定性与功能完善**
  - **Telegram** ([PR #930](https://github.com/nullclaw/nullclaw/pull/930))：现在当用户回复 Bot 消息时，被回复消息的文本内容会被作为上下文注入，显著提升了多轮对话的语义连贯性。
  - **LINE** ([PR #934](https://github.com/nullclaw/nullclaw/pull/934))：修复了 sendMessage 的路由逻辑，并实现了 Webhook replyToken 的静态数组缓存（TTL 30s），解决了高并发下的消息乱序和丢失问题。
- **核心 Agent 机制修复**
  - **子代理（Spawn）** ([PR #928](https://github.com/nullclaw/nullclaw/pull/928))：修复了 `channel_loop.zig` 中 `SubagentManager` 初始化时导致结果投递链路中断的 Bug。现在在 Telegram 轮询模式下，子代理执行结果可以正常回传给用户。
  - **持久记忆** ([PR #929](https://github.com/nullclaw/nullclaw/pull/929))：修复了 `memory_list` 工具始终包含 `session_id` 导致全局（session_id=NULL）条目不可见的问题。现在只需将 `session_id` 默认设为 null，即可正常检索全局记忆。
- **平台构建与运维**
  - **Nix 构建** ([PR #935](https://github.com/nullclaw/nullclaw/pull/935))：更新了 flake.lock 以锁定支持 Zig 0.16.0 的 zig2nix 版本，修复了 Nix 用户的构建失败问题。
  - **Gateway 网关** ([PR #933](https://github.com/nullclaw/nullclaw/pull/933))：新增了认证后的 `POST /media/transcribe` 接口，并扩展了配置解析器对 Wizard/Gateway/A2A 等对象 JSON 的处理能力，网关功能日趋完善。

## 4. 社区热点

- **[Issue #918](https://github.com/nullclaw/nullclaw/issues/918) Spawn 子代理结果“凭空消失”**
  - 该问题在 Telegram 用户群体中引起了高度关注，被标记为生产环境的阻塞级 Bug。社区成员 `weissfl` 精准定位了 `channel_loop.zig` 中 `bus=null` 的根因，并通过 [#928](https://github.com/nullclaw/nullclaw/pull/928) 迅速修复。这反映了社区对**频道内 Agent 协作稳定性**的极高要求。
- **[Issue #917](https://github.com/nullclaw/nullclaw/issues/917) 全局记忆不可见**
  - 同样由 `weissfl` 提出，该问题暴露了依赖 `session_id` 过滤的逻辑漏洞。用户存储了全局设置或系统提示，但 `memory_list` 却无法召回，严重影响了基于记忆的智能助手体验。修复 PR [#929](https://github.com/nullclaw/nullclaw/pull/929) 得到了社区的普遍认可。
- **[PR #940](https://github.com/nullclaw/nullclaw/pull/940) 与 [#939](https://github.com/nullclaw/nullclaw/pull/939) 尚未合并**
  - **#940**：自定义 OpenAI 兼容提供商被硬编码为 Claude 模型。这暴露了社区对**本地模型（如 Ollama、vLLM）和第三方托管服务**的强烈需求，大家不希望被绑定在非原生提供商上。
  - **#939**：`compact_context` 配置项形同虚设。用户不仅期望功能能用，更期望**配置文件的每一行定义都是可执行的**，而非“僵尸代码”。

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | Issue / PR | 状态 |
| --- | --- | --- | --- |
| **严重** | `spawn` 子代理结果在 Telegram 中投递失败，Root Cause 在 `channel_loop.zig:1296` | [#918](https://github.com/nullclaw/nullclaw/issues/918) → [#928](https://github.com/nullclaw/nullclaw/pull/928) | **已修复（已合入 v2026.5.29）** |
| **严重** | `memory_list` 工具通过 `session_id` 过滤导致全局记忆条目无法被检索 | [#917](https://github.com/nullclaw/nullclaw/issues/917) → [#929](https://github.com/nullclaw/nullclaw/pull/929) | **已修复（已合入 v2026.5.29）** |
| **中等** | 自定义 OpenAI 兼容提供商配置了 `base_url` 后，`/models` 菜单依然展示硬编码的 Claude 模型列表 | [#936](https://github.com/nullclaw/nullclaw/issues/936) → [#940](https://github.com/nullclaw/nullclaw/pull/940) | **待合并** |
| **中等** | `AgentConfig.compact_context` 配置项虽已解析，但运行时从未被读取，上下文总是被压缩 | [#937](https://github.com/nullclaw/nullclaw/issues/937) → [#939](https://github.com/nullclaw/nullclaw/pull/939) | **待合并** |
| **低** | Nix 构建因 flake.lock 指向不支持 Zig 0.16.0 的 zig2nix 版本而破坏 | [#935](https://github.com/nullclaw/nullclaw/pull/935) | **已修复** |

## 6. 功能请求与路线图信号

- **路线图信号：拥抱 ACP 协议**
  - 原生 ACP stdio 适配器随 v2026.5.29 发布。这强烈暗示项目正在向 **Agent-to-Agent 通信标准**靠拢，未来可能支持 Google A2A 或类似协议，从而将 NullClaw 从一个单实例 Agent 升级为**跨 Agent 服务网格的节点**。
- **API 通用性诉求（#940）**
  - 对自定义 OpenAI 兼容 API 的支持修复表明，随着本地 LLM 和企业私有模型的普及，NullClaw 必须保证其**模型提供商中间件**的完全透明化，消除对特定模型家族的硬编码依赖。
- **配置健壮性诉求（#939）**
  - 死配置的发现和修复，体现了社区对**配置即代码**的学术严谨性追求。这通常意味着项目正在走向成熟期，用户开始关注配置的可预测性和可审计性。

## 7. 用户反馈摘要

> **明显痛点得以缓解：**
> - “我的子Agent在群里跑完了，但用户收不到结果，之前必须手动重启频道才能解决。” — 来自 #918 的用户。该问题现在已被彻底修复。
> - “我在系统指令里存了全局配置，结果 memory_list 一直返回空，我一度以为是我代码写错了。” — 来自 #917 的用户。修复后全局记忆将与局部记忆清晰分离。

> **社区贡献活跃：**
> - `raskevichai` 在本周期内密集贡献了 3 个修复 PR（Telegram 上下文、子代理投递、记忆列表），显示了极高的社区活性。
> - `supersonictw` 作为 LINE 频道的主要维护者，持续优化亚太地区用户的高频渠道体验。

## 8. 待处理积压

目前项目吞吐量很高，无长期搁置的 Issue。但有以下两个 **Pending PR** 建议维护者优先关注：

1. **PR [#940](https://github.com/nullclaw/nullclaw/pull/940) `fix(models): query base_url for custom OpenAI-compatible providers`**
   - **状态**：创建于 2026-05-29，Open 未合并。
   - **影响力**：极高。直接影响所有使用非官方 API / 本地模型 / 二次代理的用户。若该功能不修复，NullClaw 在自定义 Provider 市场上几乎不可用。
   - **建议**：尽快合并并 Cherry-pick 到 v2026.5.29 的 Hotfix 分支。

2. **PR [#939](https://github.com/nullclaw/nullclaw/pull/939) `fix(agent): honor compact_context flag instead of always compacting`**
   - **状态**：创建于 2026-05-29，Open 未合并。
   - **影响力**：中高。虽然不破坏现有功能，但修复了配置语义与实际行为不符的 “欠债”。如果不修，用户可能会在极端场景下因错误压缩上下文而丢失关键 Agent 状态。
   - **建议**：代码改动量很小，建议与 #939 一并 Review 并合入下一个 Patch 版本。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是基于你提供的 GitHub 数据生成的 IronClaw 项目动态日报。

---

## IronClaw 项目日报 — 2026-05-30

### 1. 今日速览

项目在过去 24 小时内维持高强度迭代，共产出 **47 个 PR** 与 **18 个 Issue**。核心开发任务完全围绕 **“Reborn”架构的落地**展开，尤其是在产品级认证（Product Auth）系统统一、核心 MCP 扩展移植以及引擎基础组件设计方面取得了显著进展。社区互动活跃，针对版本发布阻塞和安全设计的讨论非常深入。**暂无新版本发布**，但多个大型功能模块已完成合并，项目整体处于架构重构深水区的高质量迸发阶段。

---

### 2. 版本发布

无。

---

### 3. 项目进展

过去 24 小时内，Reborn 架构的前进步伐非常坚实，大量关键 PR 完成合并或被推进：

*   **认证系统统一（Product Auth）闭环：**
    *   史诗级 PR **[#4234](https://github.com/nearai/ironclaw/pull/4234) (durable product auth)** 完成合并，建立了可持久化的产品认证层，彻底修复了代码审查发现问题。
    *   认证消费者 **[#4231](https://github.com/nearai/ironclaw/pull/4231) (Wire Reborn auth consumers)** 和 **GitHub WASM 凭据迁移** [#4233](https://github.com/nearai/ironclaw/pull/4233) 也相继合并，标志着旧认证体系正快速向 Reborn 收敛。
    *   认证体系的最后一块拼图 **“凭据代理投影”** 通过 [#4239](https://github.com/nearai/ironclaw/pull/4239) 提出，旨在打通产品侧与运行时侧的凭据孤岛。

*   **Reborn 扩展生态成型：**
    *   两个重量级 MCP 扩展正式迁入 Reborn 架构：**Notion MCP** ([#4228](https://github.com/nearai/ironclaw/pull/4228)) 和 **NEAR AI MCP** ([#4223](https://github.com/nearai/ironclaw/pull/4223))。这表明项目在通过统一架构来承载日益丰富的 AI Agent 工具链。

*   **基础设施与设计验证：**
    *   快速响应并修复了由 `trait` 漂移导致的 CI 编译失败 ([#4243](https://github.com/nearai/ironclaw/pull/4243))。
    *   新增并完善了 **Trigger Loop** ([#4248](https://github.com/nearai/ironclaw/pull/4248))、**Delivery Resolution** ([#4240](https://github.com/nearai/ironclaw/pull/4240)) 以及 **WebUI v2 Auth E2E** ([#4247](https://github.com/nearai/ironclaw/pull/4247)) 的设计文档，保持了 Reborn 开发“设计先行”的良好习惯。

---

### 4. 社区热点

*   **🔥 发布流程争议（最受关注）**
    *   **[Issue #3259](https://github.com/nearai/ironclaw/issues/3259)：Publish 0.25.0–0.27.0 to crates.io**
    *   **评论数：11** | **状态：Open（25天）**
    *   **分析：** 这是目前社区最强烈的呼声。Git Tag 已到 0.27.0，但 crates.io 仍停留在 0.24.0，导致所有外部依赖者被锁定。这反映了项目在发布流水线与社区期望之间存在严重断层，是当前最亟待解决的 DevEx 痛点。

*   **🔒 安全设计深度思辨**
    *   **[Issue #3917](https://github.com/nearai/ironclaw/issues/3917)：RuntimeCredentialTarget::PathPlaceholder 存废**
    *   **评论数：5** | **状态：Closed**
    *   **分析：** 安全贡献者 zmanian 指出了新引入的 `PathPlaceholder` 凭据注入通道存在严重安全缺陷，引发了关于“是否保留或加固”的深度辩论。虽然 Issue 已关闭，但充分展示了社区高水平的安全共建氛围。

*   **💡 功能期待：Slack 集成**
    *   **[Issue #3857](https://github.com/nearai/ironclaw/issues/3857)：Slack ProductAdapter MVP**
    *   **评论数：5** | **状态：Open**
    *   **分析：** 关联大型 PR [#4035](https://github.com/nearai/ironclaw/pull/4035) 正在持续演进，社区对 Slack 这一高频协作工具的集成呼声很高，有望进一步增强 IronClaw 的产品落地能力。

---

### 5. Bug 与稳定性

*   **🔴 严重：Nightly E2E 持续失败**
    *   **[Issue #4108](https://github.com/nearai/ironclaw/issues/4108)** — CI 自动报告的 Nightly E2E 测试失败，目前无关联修复 PR，可能影响到新代码的合入门槛，需立即排查。
*   **🟡 中等：KV Cache 重用失效**
    *   **[Issue #4241](https://github.com/nearai/ironclaw/issues/4241)** — 用户提交的深度 Bug 报告。在 Live Workspace 场景下，由于跨对话轮次时 Prompt Inputs 变化，导致 Provider 侧的 KV Cache 完全失效，严重影响 Agent 连续对话的推理性能。
*   **🟢 已修复：产品工作流编译失败**
    *   **[Issue #4237](https://github.com/nearai/ironclaw/issues/4237)** — 由 PR [#4234](https://github.com/nearai/ironclaw/pull/4234) 引入的 trait 漂移导致的编译问题。已通过 [#4243](https://github.com/nearai/ironclaw/pull/4243) 快速修复并合并。
*   **⚪ 技术债务清扫：**
    *   **[#4209](https://github.com/nearai/ironclaw/issues/4209)**：`lib.rs` 文件膨胀至 1828 行，请求拆分。
    *   **[#4222](https://github.com/nearai/ironclaw/issues/4222)**：HTTP 凭据注入路径存在明文凭证残留在内存中的风险，需实现零化（Zeroize）。
    *   **[#4226](https://github.com/nearai/ironclaw/issues/4226)**：进程交接去重集合存在无限增长的内存泄露风险。

---

### 6. 功能请求与路线图信号

*   **认证系统全面贯通：** 随着 [#4239](https://github.com/nearai/ironclaw/pull/4239) 的提出，产品级认证账户与运行时凭据代理的投影已经完成设计。一旦实现，用户可以在 WebUI 中直接管理各类服务凭据，这将是 Reborn 用户体验的巨大飞跃。
*   **WebChat v2 SSO 全面就绪在即：** 设计文档 [#4247](https://github.com/nearai/ironclaw/pull/4247) 的发布，以及 [#4204](https://github.com/nearai/ironclaw/issues/4204) 对 GitHub、NEAR 登录的跟踪，暗示 Reborn WebUI 的多提供商单点登录功能即将大规模落地（目前谷歌 SSO 已完成）。
*   **AI Agent 链路透明度提升：** PR [#4230](https://github.com/nearai/ironclaw/pull/4230) (Preserve provider reasoning summaries) 致力于保存并展示 LLM 模型的推理摘要。这不仅是用户功能需求，更为调试和信任 Agent 行为提供了关键可观测性，是高潜力的路线图信号。

---

### 7. 用户反馈摘要

*   **强依赖阻塞：** “Downstream consumers pulling from crates.io are pinned to 0.24.0 and cannot...” (Issue #3259)——用户直指发布流程断裂，核心诉求是尽快同步 crates.io，这是开源项目健康度的基石。
*   **安全意识极高：** “This is a strictly worse channel than Header or Query injection and we should decide...” (Issue #3917)——社区成员对引入新的攻击面保持了极高的警惕，并且愿意深入讨论设计取舍，反映了用户群体的高质量和专业性。
*   **高质量 Bug 报告：** “...provider-side KV cache reuse depends on the next request starting with the same prefix as the previous request.” (Issue #4241)——用户不仅复现了问题，还直接点出了 KV Cache 失效的技术原理，为开发者提供了明确的解决路径，极大地降低了排查成本。

---

### 8. 待处理积压

*   **[P0] [Issue #3259](https://github.com/nearai/ironclaw/issues/3259) — crates.io 发布滞后：** **开启 25 天，11 条评论。** 这是项目与外部生态交互的头号障碍。强烈建议维护团队将更新 crates.io 的流程自动化或列为 P0 优先级，以避免社区信任流失。
*   **[Issue #3281](https://github.com/nearai/ironclaw/issues/3281) — EventStreamManager：** **开启 24 天。** 作为 Reborn 事件流的底层支撑组件，长期缺乏代码落地将可能阻塞下游的第三方集成与通知推送场景。
*   **[PR #4035](https://github.com/nearai/ironclaw/pull/4035) — Slack ProductAdapter：** **Size: XL，开启 5 天。** 这是一个大型跨界 PR，如果 Review 周期过长，不仅容易产生大量 Diff 冲突，也可能对贡献者的积极性造成打击。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 | 2026-05-30

**数据来源**: GitHub (netease-youdao/LobsterAI)

---

## 1. 今日速览

项目今日**活跃度极高**，共处理14个PR请求，其中**9个已合并/关闭（合并率64%）**，呈现集中交付与修复状态。代码主线核心攻坚方向为**渲染性能与连接稳定性**——针对Agent执行大输出场景下的UI阻塞与断连问题进行了集中修复（#2077, #2075）。同时，系统启动优化（#2072）、子代理生命周期完善（#2074）以及多项用户体验打磨（#2073, #2076, #2063）均有推进。**风险面**：新报告一个“执行结果窗口滚动到顶端假死”的严重Bug（#2079），暂无修复PR。

**项目健康度评估：8/10**。交付质量与响应速度积极，但新Bug的涌现说明性能优化进入深水区，需持续投入。


## 2. 版本发布

无（过去24小时内无新Release发布）。


## 3. 项目进展

本节梳理今日已合并/关闭的9个重要PR带来的实际能力提升。

### 3.1 核心渲染性能与连接稳定性攻坚
- **PR #2077 [已合并] —— Exec大输出场景渲染与连接稳定性修复**
  解决Agent执行产生超过1MB输出时的两大问题：（1）Markdown渲染阻塞UI；（2）Watchdog心跳饥饿导致WebSocket误断连。修复方案包括：对>20KB的Tool Result引入延迟渲染与摘要+展开按钮，以及让TickWatchdog将任意Gateway WS事件视为活跃信号。
  (链接: netease-youdao/LobsterAI PR #2077)

- **PR #2075 [已合并] —— 避免默认渲染超大Markdown**
  作为#2077的上游补充，对超大Markdown消息默认仅展示首尾摘要预览，完整渲染需要通过手动展开。避免在Cowork回合计算中拼接大型助手消息内容。
  (链接: netease-youdao/LobsterAI PR #2075)

### 3.2 系统架构与启动优化
- **PR #2072 [已合并] —— OpenClaw Gateway启动综合优化**
  修复启动期间多余Config同步、插件重复注册、冗余Provider解析以及Dev模式下NPM Shim路径错误的问题。同时加入Quota/Model预热缓存，减少Renderer端触发的多余同步请求。
  (链接: netease-youdao/LobsterAI PR #2072)

- **PR #2078 [已合并] —— 技能路由元数据重构**
  将内联Prompts改为发射`selected-skill`路由元数据的方式，架构向事件驱动进一步解耦。
  (链接: netease-youdao/LobsterAI PR #2078)

- **PR #2057 [已合并] —— Windows更新脚本替换**
  将废弃的VBScript启动器替换为隐藏PowerShell脚本，维护Windows平台兼容性。
  (链接: netease-youdao/LobsterAI PR #2057)

### 3.3 子代理功能补齐
- **PR #2074 [已合并] —— 支持删除子代理会话**
  新增了Subagent删除的IPC/Runtime/Store清理路径，删除子代理后从侧边栏移除并让父会话重新激活。配套增加了单元测试。
  (链接: netease-youdao/LobsterAI PR #2074)

### 3.4 用户体验细节打磨
- **PR #2073 [已合并] —— Artifact缺失文件错误提示**
  当生成的本地文件链接或Artifact文件操作失败（被移动、删除或无权限）时，Toast给出明确错误提示，避免静默失败。
  (链接: netease-youdao/LobsterAI PR #2073)

- **PR #2076 [已合并] —— 文件预览工具栏操作收纳**
  将Artifact预览工具栏中不常用的操作收纳至三点更多菜单：HTML预览仅保留分享、浏览器打开和文件列表；其他文件预览精简为系统应用打开/打开所在文件夹等。
  (链接: netease-youdao/LobsterAI PR #2076)

- **PR #2063 [已合并] —— IM回复组装范围修正与Thinking剥离**
  修复了IM回复跨Turn组装的问题，并在回复中剥离思维链（Thinking Blocks）内容。
  (链接: netease-youdao/LobsterAI PR #2063)


## 4. 社区热点

- **新Bug #2079 引发关注：执行结果窗口滚动假死**
  由用户`fcinfo`今日提交。报告“2026.5.27版本，执行结果窗口滚动到顶端会假死，现象能复现”。这是当日唯一的新Issue，恰逢核心渲染性能修改（#2077, #2075）刚刚合并，社区对该Bug的成因以及与本次渲染重构的关联性尤为关注。
  (链接: netease-youdao/LobsterAI Issue #2079)

- **陈旧UX安全PR批量“复活” (#1473 ~ #1477)**
  由开发者 `MaoQianTu` 在4月4日提交的5个防数据丢失PR（涉及Agent创建、设置面板、MCP弹窗、输入框草稿、历史覆盖等场景）在昨日（5月29日）统一进行了更新。这说明这批PR已被重新纳入Review管道，社区对于“防止未保存内容丢失”的诉求正在获得响应。
  (链接: netease-youdao/LobsterAI PR #1473, #1474, #1475, #1476, #1477)


## 5. Bug 与稳定性

| 严重程度 | Bug描述 | 修复状态 |
|---|---|---|
| **严重** | **执行结果窗口滚动到顶端会假死** — 用户 fcinfo 报告该问题在27日版本中可稳定复现，暂无根因分析与修复PR。 | 🔴未修复 (链接: Issue #2079) |
| **严重** | **Exec大输出断连/UI卡死** — Agent输出超1MB时Markdown渲染阻塞UI，Watchdog饿死导致WebSocket误断开。 | ✅已修复 (PR #2077, #2075) |
| **中等** | **Artifact缺失文件静默失败** — 本地文件被移动/删除后用户无感知。 | ✅已修复 (PR #2073) |
| **中等** | **IM回复跨Turn/含Thinking块** — 消息组装溢出当前Turn，并携带了不应展示的推理过程。 | ✅已修复 (PR #2063) |
| **低** | **Windows更新启动器废弃** — VBScript脚本被标记废弃。 | ✅已修复 (PR #2057) |


## 6. 功能请求与路线图信号

- **“Exec风暴”弹性是企业级准入信号**：PR #2077 与 #2075 的合入表明LobsterAI正在攻克复杂Agent执行环境下的数据吞吐瓶颈。高阶用户（长时间工具调用、大日志输出）的需求被明确纳入当前研发优先级。

- **UI防丢失保护走向成熟**：PR #1473~#1477（尽管尚处积压状态，但昨日更新预示将推进）涵盖弹窗未保存确认、草稿实时持久化、历史覆盖确认等场景。这是产品从“可用”进入“可靠”阶段的必备特性。

- **子代理生命周期管理闭环**：PR #2074（删除子代理）补全了子代理生命周期管理功能。继子代理创建、运行之后，删除能力的加入标志着该特性在进入生产就绪状态。

- **Gateway架构优化继续**：PR #2072 对启动阶段的配置同步和插件注册进行了减负，暗示团队正在优化冷启动体验与运行时稳定性。


## 7. 用户反馈摘要

- **Issue #2079 — 界面严重假死**: 用户 `fcinfo` 明确反馈执行结果窗口在滚动到顶端时发生假死，并强调“现象能复现”。这是具备高度可操作性的Bug报告，直接指向特定交互条件下的渲染Bug，暴露出UI渲染逻辑在边界场景仍存在缺陷。

- **隐含的“断连与卡死”痛点（从已修复PR推断）**: PR #2077 的修复说明用户在运行复杂Agent任务时，大概率持续遭遇“输出窗口不响应”以及“任务执行到一半被断开”的不良体验。今日对该问题的集中修复预计将大幅改善重度用户的使用体验。


## 8. 待处理积压

### ⚠️ 陈旧但处于活跃更新中的重要PR (作者: `MaoQianTu`)

以下5个PR均针对“用户配置/输入内容静默丢失”这一核心体验问题，均创建于2026年4月4日，标记为[stale]，但于昨日（5月29日）更新。强烈建议维护者加速合并。

- **#1473**: 创建Agent弹窗关闭时添加未保存确认
  (链接: netease-youdao/LobsterAI PR #1473)
- **#1474**: Agent设置面板关闭时添加未保存确认
  (链接: netease-youdao/LobsterAI PR #1474)
- **#1475**: MCP服务器配置弹窗关闭/按Escape时添加未保存确认
  (链接: netease-youdao/LobsterAI PR #1475)
- **#1476**: 切换会话/视图时输入框草稿立即持久化（防止去抖定时丢失）
  (链接: netease-youdao/LobsterAI PR #1476)
- **#1477**: 重新编辑历史消息时添加覆盖确认
  (链接: netease-youdao/LobsterAI PR #1477)

### 🔴 需要关注的新生Bug

- **#2079**: 执行结果窗口滚动假死。今日提交，严重程度高，目前无Assignees、无关联修复PR，需尽快分派所有者进行复现排查。
  (链接: netease-youdao/LobsterAI Issue #2079)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-05-30

**分析师评价：**
昨日项目在稳定性和兼容性上迎来了架构级别的挑战，但同时也展现了极高的核心响应速度。社区反馈质量专业，维护者修复执行力强，项目整体处于健康发展的快车道。

---

## 1. 今日速览

过去24小时，项目处于 **“高质量反馈”与“高效率修复”** 并存的阶段。共计更新 3 条 Issue 和 2 条 PR。

- **响应速度亮眼**：针对 `#1083`（技能开关逻辑错误）的 Bug 报告，维护者在当天提交修复 PR `#1084` 并完成合并，构建了优秀的用户信任闭环。
- **严峻的环境挑战**：用户 `karlmdavis` 提交了两个重量级 Issue（`#1085`, `#1086`），分别指向 arm64 架构支持和企业代理网络兼容性。这是项目从个人开发者工具走向企业级场景必须跨越的关键门槛。
- **项目健康度**：良好。尽管环境适配面临压力，但项目核心逻辑的迭代效率非常高，社区反馈质量优秀，形成了良性的开发者-用户互动循环。

---

## 2. 版本发布

昨日无新版本发布。

---

## 3. 项目进展

- **[已合并] Skill 系统后台逻辑精细化重构**
  - **PR:** [#1084 fix(skills): track bundled skill disables individually](https://github.com/moltis-org/moltis/pull/1084) by `penso`
  - **详情：** 该修复彻底解决了类别禁用与单技能禁用的状态冲突。现在用户可以完全独立地控制每一个内置技能的启停，而不再受限于类别开关。新增的回归测试保证了该逻辑在 Chat 会话、Web API 及详情页中的统一性。
  - **项目意义：** 这是技能系统精细化权限管理的基石，使 Moltis 的 Skill 生态更加灵活可控。

- **[待合并] 依赖项例行安全更新**
  - **PR:** [#1087 chore(deps): bump tar from 0.4.45 to 0.4.46](https://github.com/moltis-org/moltis/pull/1087) by `dependabot[bot]`
  - **详情：** 例行升级 Rust 后端的 `tar` 库，维护供应链安全。

---

## 4. 社区热点

尽管昨日所有 Issue 的评论数均为 0，并未形成“热烈讨论”，但从 Issue 本身的质量和深度来看，社区焦点异常明确——**企业级与异构环境兼容性**。

- **热点人物：** 用户 `karlmdavis` 成为昨日的数据亮点。他在一天内连续提交了两个极具技术深度的 Bug 报告（[#1085](https://github.com/moltis-org/moltis/issues/1085)、[#1086](https://github.com/moltis-org/moltis/issues/1086)）。
- **背后诉求：** 这说明 Moltis 的早期重度用户群体正在通过 **实际的企业级异构网络环境**（Apple Silicon + 企业代理）来验证项目。他们不仅在使用产品，更在帮助项目定义兼容性边界和架构路线图。

---

## 5. Bug 与稳定性

按严重程度排列：

- **[严重 - 环境阻塞] Apple Silicon 上 Docker 后端崩溃**
  - **Issue:** [#1085 Docker sandbox fails on arm64: /sys/class/dmi mount error](https://github.com/moltis-org/moltis/issues/1085)
  - **报告人:** `karlmdavis`
  - **状态:** 待处理
  - **根因分析:** 代码硬编码了 x86 特有的 `/sys/class/dmi` 的 tmpfs 挂载，在 Docker Desktop 的 arm64 VM 中不存在此路由，导致 runc 无法创建挂载点，完全阻止了在 Apple Silicon 上使用 Docker 后端。

- **[严重 - 环境阻塞] Apple Containers 后端在企业代理后构建失败**
  - **Issue:** [#1086 Apple Containers backend: sandbox image build fails (no DNS behind corporate proxy)](https://github.com/moltis-org/moltis/issues/1086)
  - **报告人:** `karlmdavis`
  - **状态:** 待处理
  - **根因分析:** Apple Containers 的 Builder VM 在构建沙箱镜像时无法穿透公司代理（如 Zscaler）解析 DNS。

- **[已修复] 技能开关逐项失效**
  - **Issue:** [#1083 [Bug]: Skills enabled/disabled per-category, it's unable to enable/disable one skill](https://github.com/moltis-org/moltis/issues/1083)
  - **报告人:** `bsarkisov`
  - **状态:** 已关闭（由 PR #1084 修复）

---

## 6. 功能请求与路线图信号

昨日无明确的新功能请求（如“我想要某个新后端”），但 `#1085` 和 `#1086` 本身就是最强烈的路线图信号：

- **路线图 1.0 级信号：** 增加 **arm64 完整兼容性** 以及 **企业代理网络穿透支持** 已迫在眉睫。如果项目计划下一个里程碑版本，这两个问题极大概率会被标记为 P0 级阻塞项。

---

## 7. 用户反馈摘要

- **`@karlmdavis` (高水平 DevOps 用户)**
  - **痛点：** 希望在非理想网络环境和非 x86 架构下获得原生体验。
  - **反馈质量：** 极高。他在 `#1085` 中指出 “DMI is an x86 SMBIOS feature, doesn't exist on arm64”，在 `#1086` 中指出 “DNS resolution doesn't work inside the builder VM”。这是开放源码社区最珍贵的“带根因的 Bug 报告”，能极大降低维护者的调试成本。
  - **情绪：** 略显焦急，但提供了完整的复现环境（`brew install` + Zscaler 代理），表明他是极度渴望使用 Moltis 的专业用户。

- **`@bsarkisov` (细节体验型用户)**
  - **痛点：** 追求极致的细粒度交互控制。
  - **反馈质量：** 良好。用户严格遵守了 Bug 报告模版。该 Bug 在同日被修复，相信会极大提升他的使用体验和留存率。

---

## 8. 待处理积压

以下 Issue 目前处于“0 评论、0 分配”状态，需要维护者尽快介入，避免高质量用户流失：

- **[高优先级] Issue #1085** — Docker sandbox fails on arm64
  - 链接: https://github.com/moltis-org/moltis/issues/1085
  - 建议: 即使无法立即修复，也请回复确认调研，避免专业用户感到冷落。

- **[高优先级] Issue #1086** — Apple Containers backend corporate proxy build fails
  - 链接: https://github.com/moltis-org/moltis/issues/1086
  - 建议: 同上。这两个 Issue 的作者是同一人，建议一次性回复并建立沟通渠道。

- **[中等优先级] PR #1087** — Dependabot 依赖更新
  - 链接: https://github.com/moltis-org/moltis/pull/1087
  - 建议: 常规更新，若无冲突可尽快合并以保持依赖链健康。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-05-30

## 1. 今日速览

过去 24 小时项目保持高速迭代：累计 **45 条 Issue 更新**（新开/活跃 20，已关闭 25）和 **31 条 PR 更新**（待合并 13，已合并/关闭 18），同步发布 **v1.1.10-beta.1**。  
- 大量 Bug 被快速关闭，社区反馈的工具调用挂起、Windows 桌面定时任务异常、飞书频道稳定性等核心问题均已有对应修复。  
- 功能侧聚焦**渠道增强**（飞书群共享/线程回复）、**插件系统**（卸载 hook、技能暴露、Prompt 注册）以及**开发者体验**（类 VSCode 编辑模式、项目直接导入）。  
- 用户对类似 Trae 的“对话回退与文件 Diff”呼声很高，同时向量数据库无限膨胀、流式输出卡顿等性能问题成为当前稳定性焦点。  

整体项目活跃度 **高**，维护团队响应迅速，社区参与积极。

---

## 2. 版本发布

### v1.1.10-beta.1  
- **主要变更**  
  - `chore(release)`: 完善 README 新闻板块，版本号更新至 v1.1.9 → v1.1.10-beta.1（#4726）  
  - `ci(infra)`: 移除冗余的 `unit-tests.yml` 工作流（#4748）  
- **破坏性变更/迁移注意事项**  
  无。此版本仅为 CI 优化与元数据调整的 beta 增量包，不涉及接口或行为变化。  
- **链接**：[Releases v1.1.10-beta.1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.10-beta.1)

---

## 3. 项目进展（今日合并/关闭的重要 PR）

以下 PR 已于今天或之前闭环，是项目近期功能演进和稳定性加固的关键节点：

### 智能体协作能力
- **#4806** `feat(agents): add spawn_subagent tool`  
  新增内置工具，允许智能体在同一工作区内创建**临时性子智能体**完成子任务，与已有 `chat_with_agent`（跨工作区）互补。三种协作模式现已完整覆盖。  
- **#4728** `fix(agents): preserve reasoning_content across file blocks`  
  修复 `[thinking, file]` 消息模板下推理内容被静默丢弃的问题。

### 飞书渠道深度完善
- **#4537** `feat(feishu): support group session shared mode`（首次贡献）  
  群聊会话模式统一为布尔开关 `share_session_in_group`，与企业微信对齐。  
- **#4708** `feat(feishu): feishu thread reply`（首次贡献）  
  飞书话题（Thread）内回复支持，不再发在顶层。  
- **#4742** `refactor(feishu): restructure card system`  
  飞书交互卡片重构为子包结构，修复流式模式下卡片嵌入异常。

### 插件系统扩展
- **#4794** `feat(plugins): add uninstall hooks, fix validator imports, expose skill provider API`  
  提供 `register_uninstall_hook`、技能 Provider API 等关键接口，为 DataPaw 等插件集成铺路。  
- **#4804** `Feature/prompt section registry`（OPEN 但已提交，配合插件生态）  
  插件可通过 `PluginApi.register_prompt_section()` 向 Agent 系统提示中注入自定义段落，无需猴子补丁。

### 桌面与 CLI 稳定性
- **#4779** `fix(tauri): add bundled desktop qwenpaw CLI`  
  打包版桌面不再需要额外 `pip install qwenpaw`，cron 命令直接解析内置 CLI。  
- **#4801** `fix(pet): auto-install missing dependencies`（首次贡献）  
  桌面宠物因缺失 `pyside6-essentials` 启动失败，现自动安装。  
- **#4696** `fix(coding): hide Windows git console windows`  
  消除 Coding Mode 下弹出黑框问题。

### 提供商 & 通用工具
- **#4809** `feat(providers): add OpenRouter app attribution headers`  
  增加 `X-OpenRouter-Title/Categories` 头部，确保 QwenPaw 在 OpenRouter 编程排行榜可见。  
- **#4805** `fix(console): chatcode`  
  修复 Coding Mode 切换项目时未清除旧编辑器 Tab 的问题。

> 以上 PR 合计贡献者 8 人（含 4 位 first-time-contributor），合并/关闭率 58%，项目持续吸纳外部贡献。

---

## 4. 社区热点

今日讨论最活跃的 Issue 主要集中在**可靠性**与**高级编辑体验**两方向：

| Issue | 标题 | 评论数 | 分析 |
|-------|------|--------|------|
| [#4739](https://github.com/agentscope-ai/QwenPaw/issues/4739) (CLOSED) | Tool call hangs Agent: timeout or success → waits for user input | 8 | 工具调用后 Agent 静默等待用户输入而不继续，严重影响自动化流程。已修复。 |
| [#4789](https://github.com/agentscope-ai/QwenPaw/issues/4789) (CLOSED) | [Feature] 希望像 Trae 一样可以删除/回退对话 | 7 👍1 | 用户期待“文件级回退”与“全量沙箱管理”能力，呼声极高，是当前功能路线的关键信号。 |
| [#4653](https://github.com/agentscope-ai/QwenPaw/issues/4653) (CLOSED) | 定时任务与用户消息共享 session 导致任务中断 | 7 | 多人报告 cron 任务因用户新消息被打断，涉及会话隔离设计。已修复。 |
| [#3224](https://github.com/agentscope-ai/QwenPaw/issues/3224) (OPEN) | Feature Request: CoPaw Agent Teams | 6 | 长期 request：自然语言驱动的自进化多智能体协作团队，反映对复杂协同场景的期待。 |
| [#4808](https://github.com/agentscope-ai/QwenPaw/issues/4808) (OPEN) | Agent [person_stat_skill] not exists | 5 | Skill 注册后无法调用，用户疑惑。维护者需澄清 Skill 加载机制。 |

**社区信号**：用户不再满足于简单问答，而是期待**工业级的工作流管理**（回退、Diff、定时任务隔离）和**类 IDE 的深度集成**。

---

## 5. Bug 与稳定性

按严重程度排列今日活跃 Bug，并标注已有修复 PR 的状态。

| 严重度 | Issue | 简述 | 状态 | Fix PR |
|--------|-------|------|------|--------|
| 🔴 崩溃/阻塞 | [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | ChromaDB 向量索引膨胀至 37G，`memory_search` 卡死/每30min崩溃 | OPEN | 无 (删除 `file_store` 可恢复，需根本修复) |
| 🔴 崩溃/阻塞 | [#4792](https://github.com/agentscope-ai/QwenPaw/issues/4792) | 远程 Console 流式输出长回复时本地电脑系统级卡死 | OPEN | 无 (疑似前端/渲染瓶颈) |
| 🔴 性能严重 | [#4802](https://github.com/agentscope-ai/QwenPaw/issues/4802) (CLOSED) | v1.1.9 发送消息后界面卡死无法正常问答 | 已关闭 | 可能与某次发布回归，未指定 PR |
| 🟠 功能异常 | [#4800](https://github.com/agentscope-ai/QwenPaw/issues/4800) | `/skills` 首次不触发，第二次报 YAML 解析错误 | OPEN | 疑似命令调度问题 |
| 🟠 功能异常 | [#4788](https://github.com/agentscope-ai/QwenPaw/issues/4788) (CLOSED) | OneBot 频道频繁掉线不自动重连 | 已关闭 | 需手动重保存配置，修复待验证 |
| 🟠 功能异常 | [#4819](https://github.com/agentscope-ai/QwenPaw/issues/4819) | 代码模式切换对话触发全局刷新跳回原对话 | OPEN | 无 |
| 🟠 功能异常 | [#4824](https://github.com/agentscope-ai/QwenPaw/issues/4824) | ACP 连接 Claude Code 协议版本号格式不匹配 | OPEN | 无 |
| 🟡 配置持久化 | [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807) | 每次升级已被禁用的内置技能重新启用 | OPEN | 无 |
| 🟡 子进程 | [#4636?] (列表未含但 #4773) | 桌面版定时任务总去 pip install qwenpaw | 已通过 #4779 修复 | ✅ |

### 值得关注的已关闭 Bug（暗示已修复）
- [#4739](https://github.com/agentscope-ai/QwenPaw/issues/4739) 工具调用挂起 → fix 可能随 v1.1.10-beta.1 或单独 PR。  
- [#4649](https://github.com/agentscope-ai/QwenPaw/issues/4649) 孤儿 cron 任务清理 → 修复合入。  
- [#3718](https://github.com/agentscope-ai/QwenPaw/issues/3718) Windows Defender 误报 v1.1.3 → 官方声明已修复。

---

## 6. 功能请求与路线图信号

结合 Issue 诉求与现有 PR，以下方向可能进入下个里程碑：

| 功能请求 | 票数/热度 | 当前状态 | 推测纳入可能性 |
|----------|----------|----------|----------------|
| **对话级回退与文件 Diff** (#4789, #4825) | 高 👍1 + 新开 #4825 | 社区强烈要求“writefile 变更 Diff 和审阅” | ⭐⭐⭐ 高，已在规划 |
| **Coding Mode VSCode 兼容 & 直接导入项目目录** (#4759) | 中 | 无对应 PR，但与编辑器体验重合 | ⭐⭐⭐ 高 (近一次发布增强) |
| **`/skills` Tab 自动补全** (#4796) | 中 | PR #4810 已提交 (Under Review) | ✅ 几乎确定纳入下一版 |
| **多智能体协作团队 (Agent Teams)** (#3224) | 评论6，长期 | 无正式 PR，属远景特性 | ⭐⭐ 中，需架构变更 |
| **AgentScope 2.0 后端迁移** (#4727) | 2 👍 | OPEN，Breaking Change 标记 | ⭐⭐⭐ 高，但需大量测试 |
| **插件注册自定义渠道** (#4693) | 关联 PR 已提交 | OPEN | ⭐⭐⭐ 高 (与 #4794 互补) |
| **提示词注入 Registry** (#4804 对应 feature) | 仅 PR | 已提交等待合并 | ✅ 即将合入 |
| **文件/代码位置索引引用** (#4823) | 1 评论 | 新开，具体实现参考 Trae | ⭐⭐ 中 |

项目明显向**插件化生态**、**Channels 抽象**和**类 IDE 前端体验**倾斜，与 Trae 对标的功能成为社区主要期望。

---

## 7. 用户反馈摘要

从今日 Issue/评论中提炼的真实声音：

- **“每次升级被禁用的技能又变回启用，还要手动关一次”**（#4807）— 配置持久化不足，轻微但重复的痛点。  
- **“ssh 远程访问 Console，流式输出一长，本地鼠标都动不了”**（#4792）— 前端渲染性能在长文本场景下出现灾难性退化。  
- **“用了三个月，向量数据库膨胀到 37G，memory_search 一直崩溃”**（#4795）— 重度用户的索引管理缺失，这是留存风险。  
- **“能不能像 Trae 那样每步文件更改都可以看 diff，还可以回退？”**（#4825, #4789）— 强需求，代表用户想从“对话玩具”转向“生产工具”。  
- **“飞书群共享 session 方便，现在还能在 thread 里回复了，进步很大”**（隐含在 #4708 等 PR 评论）— 渠道功能得到正面评价。  
- **“定时任务总是被用户消息打断，麻烦”**（#4653）— 会话隔离设计缺陷，现已修复，用户应感到满意。  
- **“Windows Defender 终于不报毒了，放心用了”**（#3718 closed）— 安全信任修复成功。  

整体而言，用户对**功能广度满意**（多渠道、插件等），但对**稳定性细节**（配置保持、性能、索引膨胀）和**高级内容管理**有更高期望。

---

## 8. 待处理积压

以下 Issue/PR 已开放较长时间或属于关键路径，建议维护者优先关注。

| 项目 | 类型 | 创建时间 | 重要性 | 备注 |
|------|------|----------|--------|------|
| [#3224](https://github.com/agentscope-ai/QwenPaw/issues/3224) Agent Teams 需求 | Issue (OPEN) | 2026-04-10（51 天） | 高 | 多智能体团队蓝图，虽无 PR 但长期悬而未决，社区期待。 |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) AS 2.0 迁移 | Issue (OPEN) | 2026-05-27（3 天） | ⚠️ Breaking | 影响整个后端，需尽早启动。 |
| [#4491](https://github.com/agentscope-ai/QwenPaw/issues/4491) 子代理继承 MCP/ACP 配置 | Issue (CLOSED) 但无明确结论 | 2026-05-18 | 中 | 配置语义争议，设计决策待定。 |
| [#4683](https://github.com/agentscope-ai/QwenPaw/pull/4683) 修复 Tauri 桌面外部链接 (OPEN) | PR | 2026-05-26（4 天） | 中 | 影响桌面用户体验，已标记但未合并。 |
| [#4693](https://github.com/agentscope-ai/QwenPaw/pull/4693) 插件注册自定义渠道 (OPEN) | PR | 2026-05-26（4 天） | 高 | 配合插件生态的关键 PR，待 review。 |
| [#4787](https://github.com/agentscope-ai/QwenPaw/pull/4787) 防止 shell 输出炸穿上下文 (OPEN) | PR | 2026-05-28（2 天） | 高 | 直接关系长上下文稳定性。 |
| [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) 向量索引膨胀 37G (OPEN) | Issue | 2026-05-29（1 天） | 🔴 紧急 | 阻塞重度用户使用，目前无负责人。 |
| [#4792](https://github.com/agentscope-ai/QwenPaw/issues/4792) 流式输出卡死客户端 (OPEN) | Issue | 2026-05-29（1 天） | 🔴 紧急 | 前端渲染性能衰退，影响远程使用场景。 |

**提醒**：以上列表中，#4795 和 #4792 是当前最影响用户体验的两大问题，建议优先投入资源；#3224 虽然时间久，但可作为社区讨论的锚点，适当给出 roadmap 信号。

---

*本日报基于 GitHub public events 自动生成，仅供项目健康度参考。数据时间范围：2026-05-29 ~ 2026-05-30（UTC）。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是根据 ZeroClaw 项目 2026 年 5 月 30 日的 GitHub 更新数据生成的每日项目动态报告。

---

## ZeroClaw 项目动态日报 (2026-05-30)

### 1. 今日速览

ZeroClaw 项目在过去 24 小时内保持了极高的开发活跃度，社区共提交并讨论了 19 个 Issue，同时处理了 46 个 PR。虽然 DeepSeek 多轮对话丢失 `reasoning_content` 的核心 Bug 已随 PR #6284 的合并而关闭，项目稳定性有所提升，但 Slack 与 Telegram 通道同时出现 S1 级别故障，且文档版本严重滞后，用户的开发体验受到显著影响。社区的热点讨论集中在 MCP 工具治理、即将到来的 v0.8.0-beta-2 大型功能集以及 Schema-Guided Reasoning (SGR) 范式上，体现了项目正从基础框架搭建向着高阶 Agent 能力与安全治理全面发力。

### 2. 版本发布

本日无新版本发布。然而，社区正在紧密关注大型集成 PR #6848 的进展，该 PR 将成为 **v0.8.0-beta-2** 的基础，预计将包含 ZeroCode TUI、RPC 套接字传输和对传统插件架构的初步整合。

### 3. 项目进展

今日合并/关闭的重要 PR 聚焦于修复近期引入的回归问题和增强核心基础设施：

- **Provider 稳定性修复**
    - **[DeepSeek 多轮对话修复]** PR #6284 (Closed)：修复了 `chat_messages_to_native()` 在纯文本助手轮次中丢弃 `reasoning_content` 的 Bug。此前该问题导致 **所有** 使用了思维链模型（如 DeepSeek V4）的多轮对话在第二轮必然失败。对应的追踪 Issue #6233 同步关闭。
- **网络工具增强**
    - **[IPv6 与依赖库标准化]** PR #5450 (Closed)：移除了 `http_request` 和 `web_fetch` 等工具中的自定义 URL 解析，全面转向 `reqwest::Url`。此举解决了长期存在的 IPv6 地址解析和匹配问题，增强了工具的健壮性。
- **配置与成本优化**
    - **[显式 Provider 路由]** PR #6607 (Closed)：新增了 `[providers.models.<alias>].kind` 字段，允许用户精确选择兼容层的实现，解决别名冲突和路由歧义的问题。
    - **[成本分流]** PR #6945 (Closed)：新增 `classifier_provider` 配置，允许为“回复意图预检查”分配更便宜的模型，帮助用户显著降低运营成本。
- **架构梳理**
    - **[Memory 策略抽象]** PR #6907 (Closed)：引入了 `MemoryStrategy` 特征，将高层内存生命周期策略与底层的存储逻辑分离，为未来支持多样化的记忆管理打下了基础。

### 4. 社区热点

1.  **MCP 工具过滤完全失效 (#6699)**
    - **链接**: `zeroclaw-labs/zeroclaw Issue #6699`
    - **热度**: 7 条评论，被标记为 **P1** 严重级别。
    - **分析**: 社区发现 `tool_filter_groups` 配置对于真实 MCP 工具完全不起作用，原因是标签前缀检查存在 Bug，且未集成 `deferred_loading`。这导致依赖此功能进行权限管控的用户面临安全风险。目前已经有 **PR #6920** 在排队合并，直接针对此 Bug 进行修复，是当前开发的重中之重。

2.  **v0.8.0-beta-2 整合的前哨 (#6848)**
    - **链接**: `zeroclaw-labs/zeroclaw Pull Request #6848`
    - **热度**: 该巨型 PR 涉及 116 个标签（涵盖几乎所有模块），排期长达半月，正在寻求首批反馈。
    - **分析**: 此 PR 代表了下一个版本的全景图，包括了 ZeroCode TUI、RPC 传输与全新的审批流。开发者的广泛参与和反馈将直接决定 v0.8.x 系列的最终形态。

3.  **Schema-Guided Reasoning (SGR) RFC (#6998)**
    - **链接**: `zeroclaw-labs/zeroclaw Issue #6998`
    - **热度**: 刚发布即被贴上 `needs-maintainer-review` 标签。
    - **分析**: 用户提出的该 RFC 若被接受，将彻底改变 ZeroClaw 跨 Provider 的推理输出结构，旨在实现更稳定、可控的结构化输出。这直接反映了资深用户希望将 ZeroClaw 从“聊天机器人”进化为“复杂推理 Agent”的强烈诉求。

### 5. Bug 与稳定性

本日报告的 Bug 严重分布极不均匀，通道模块出现了重大危机：

- **S1 - 流程阻塞**
    - **[Slack Socket 模式崩溃]** #6992：所有入站消息被 Slack 拒绝为“未授权用户”，严重性极高。P1 优先级。**暂无对应修复 PR**。
    - **[Telegram 语音转录失败]** #6999：语音消息被静默忽略，Agent 从未连接 `transcription_provider`。P1 优先级。**暂无对应修复 PR**。
    - **[文档版本完全脱节]** #6997：官方文档指向 v0.8.0-beta-1 的行为，但正式发布版是 v0.7.5，导致新用户上手被严重误导。

- **S2 - 行为降级**
    - **[v0.8.0-beta-1 工具序列化绕过安全策略]** #6991：`tools_to_openai_format` 忽略了 Risk Profile 和 Tool Filter 设置，属于严重的安全逻辑 Bug。P1 优先级。
    - **[多 Agent TTS 错误加载 Provider]** #7001：`TtsManager::from_config` 在解析时错误读取了顶层 Agent 的 Provider，导致语音播报异常。
    - **[GLM 历史裁剪后崩溃]** #7013：今日刚创建的修复 PR，解决了历史记录裁剪后消息格式对 GLM/Z.AI 无效的问题。

- **S3 - 轻微问题**
    - **[引导向导未本地化]** #7005：部分用户界面字符串写死，绕过 Fluent i18n 流程。对应 PR #7012 已在修复中。

### 6. 功能请求与路线图信号

用户今日提出的新请求显示出对**生产级安全**和**高阶 Agent 能力**的强烈追求：

- **[RFC] 精细化沙箱策略** (#6996)：用户提出通过配置驱动限制 Agent 的文件系统和网络访问。这是从“功能性”走向“企业级合规”的重要信号，很可能被纳入后续的 v0.8.x 路线图中。
- **[Config Secret 扩展]** (#6989)：用户在配置 MCP 和文件上传的头信息时，希望 `#[secret]` 属性能够支持 `HashMap` 以自动脱敏 Bearer Token。这表明用户对配置安全性的敏感度极高。
- **[本地优先模式 (Local-First)]** (#5287)：尽管创建已久，但今日仍有讨论热度。该请求旨在对抗提示词膨胀和防止系统指令泄露，对于吸引 Ollama 等本地模型用户至关重要，维护者应考虑在 v0.8.1 中给予支持。

### 7. 用户反馈摘要

- **满意/正面反馈**：
    - **核心修复受认可**：社区对 PR #6284（DeepSeek 修复）和 PR #6907（内存策略抽象）的合并表示积极认可，认为这是解决实际痛点的关键步骤。
    - **成本敏感**：开发者对 `classifier_provider`（PR #6945）这类能直接降低 API 调用费用的特性表现出极高兴趣。
- **痛点/负面反馈**：
    - **“为什么我配置了却没用？”**：MCP 工具过滤的静默失效（#6699）让许多依赖 RBAC 的用户感到困惑，反馈“配置看起来有效但实际是摆设”。
    - **“通道换了，助理死了”**：Slack 和 Telegram 通道的严重故障（#6992, #6999）直接影响了依赖这些平台的核心用户，造成严重的业务中断。
    - **“文档是陷阱”**：用户对新版文档与实际版本脱节（#6997）感到沮丧，认为“这增加了巨大的学习成本”。
    - **交互细节欠佳**：CJK 用户对退格键的按字节删除问题 (#6995) 提出了反馈，虽然优先级低但影响了东亚用户的日常使用体验。

### 8. 待处理积压

- **失联提交审计 (Issue #6074)**：该 Issue 跟踪的 153 个被批量回滚的提交至今缺乏系统的恢复计划。随着 v0.8.0-beta-2 的临近，维护者需尽快审计并 Cherry-pick 有价值的修复，避免版本碎片化。
- **Arm64 Docker 镜像支持 (PR #5187)**：一个潜在的高价值 PR，但陷入停滞（需作者回应）。社区对原生 Arm64 部署需求的呼声越来越高，维护者应考虑接手此 PR 或指派新的贡献者完成。
- **关键 S1 Bug 无人认领**：
    - **[Slack Socket 模式]** (#6992) 与 **[Telegram 语音]** (#6999) 是目前最紧急的漏水点，但截至发稿均**没有与之关联的 Fix PR**。这在当前活跃度极高的社区中显得尤为突出，需要项目核心维护者迅速介入或直接接管。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*