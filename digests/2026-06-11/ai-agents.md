# OpenClaw 生态日报 2026-06-11

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-11 03:38 UTC

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

# OpenClaw 项目动态日报 | 2026-06-11


### 1. 今日速览

过去24小时内，OpenClaw 项目维持着极高的社区活跃度与开发强度。总计追踪到 **500 条 Issues 更新**与 **500 条 PR 更新**，其中 31 个 Issue 和 104 个 PR 已结案/合并。项目重心显著向**安全加固**倾斜——`v2026.6.6-beta.1` 的发布标志着团队对几乎整个系统进行了安全边界的大规模收紧。与此同时，社区围绕**消息投递可靠性、子智能体静默失败 和 会话状态一致性**展开了激烈讨论。一个 **P0 级维护者跟踪 Issue** (#88838) 聚焦于核心会话/Transcript 的 SQLite 迁移策略，表明项目正处于重大底层架构演进的关键节点。整体健康度良好，但大量 P1 级的 Bug 积压表明稳定性修复仍是当前的主要攻坚战。


### 2. 版本发布

**v2026.6.6-beta.1** ([Release](https://github.com/openclaw/openclaw/releases/tag/v2026.6.6-beta.1))

**核心变更：** 这是一次覆盖极广的安全审查落地，几乎涉及所有关键子系统：

- **Transcripts & 沙箱绑定**：强化内部追踪数据的隔离。
- **宿主机环境继承 & MCP stdio**：收紧子进程环境变量传递与 MCP 标准输入的权限。
- **Codex HTTP 访问 & 原生搜索策略**：限制恶意代码生成与敏感搜索。
- **Sender 检查 & ACP 绕过修复**：已删除智能体的 Agent Communication Protocol 路径已修补。
- **Discord 审查模式 & Teams 群组调用**：加强了多平台消息路径的过滤与防滥用机制。

**潜在破坏与迁移建议：**
这是自 2026 年初以来最大的一次安全收紧。安全边界变严，意味着之前一些宽松的默认配置可能失效。**强烈建议：** 升级后立即审查 `sandbox`、`mcp` 及 `gateway.auth` 配置。特别是 MCP 跨域重定向策略和宿主机环境变量继承规则的变动，可能导致已有的自动化工作流中断。请在测试环境充分验证后再投入生产环境。


### 3. 项目进展

今日合并/关闭了 104 个 PR，修复了多处关键 Bug，并对 CLI 工具链和子智能体策略进行了增强：

- **【会话修复】模型覆盖丢失 [#90128](https://github.com/openclaw/openclaw/pull/90128)** *(Merged)*：修复了用户通过 `/model` 指令覆盖模型后，在每日/空闲滚动时覆盖丢失、回退到默认配置的严重问题。
- **【兼容性修复】推理内容转发 [#84938](https://github.com/openclaw/openclaw/pull/84938)** *(Merged)*：修复了 OpenAI 兼容提供商（如 MiMo v2.5）返回的 `reasoning_content` 被网关丢弃的问题，使推理过程能被完整追踪。
- **【安全修复】MCP HTTP 重定向 SSRF [#92021](https://github.com/openclaw/openclaw/pull/92021)**：修复了跨域 30x 重定向会重放原始 POST Body 的安全漏洞（SSRF / Credential Exfil 风险）。
- **【开发者体验】Skills 语法检查与提示 [#92028](https://github.com/openclaw/openclaw/pull/92028) / [#92025](https://github.com/openclaw/openclaw/pull/92025)**：新增 `skills lint` 命令排查格式错误的 SKILL.md，并在 `skills check` 中给出具体的修复提示，降低自定义技能开发门槛。
- **【子智能体策略继承 [#78441](https://github.com/openclaw/openclaw/pull/78441)**：实现了在 `sessions_spawn` 中向下游子智能体转发 `toolsAllow` 策略，解决了子任务权限过大或过小的治理问题。
- **【后台任务唤醒修复 [#91921](https://github.com/openclaw/openclaw/pull/91921)**：修复了后台 `exec` 命令完成后，系统错误地发送 `[OpenClaw heartbeat poll]` 消息导致智能体误触心跳的问题。
- **【内存 CLI 索引修复 [#92079](https://github.com/openclaw/openclaw/pull/92079)**：修复了使用 `openclaw memory index --force` 时 `providerKey` 可能因 CLI 上下文与运行时不匹配而写入错误数据的问题。


### 4. 社区热点

今日讨论最活跃的议题集中反映了用户在使用中的核心矛盾——**信任感与可控性**：

- **“内部话语术”外泄到聊天窗口 [#25592](https://github.com/openclaw/openclaw/issues/25592)** *(31条评论, P1)*：智能体在工具调用间隙产生的内部处理文本（错误提示、处理确认）被错误地路由到用户可感知的聊天通道（Slack、iMessage）。用户普遍认为这严重影响了专业性和信任感，属于严重的 UX 问题。
- **子智能体任务“石沉大海” [#44925](https://github.com/openclaw/openclaw/issues/44925)** *(19条评论, P1)*：子智能体任务因多种原因（超时、失败、交付确认失败）静默丢失，既无重试也无通知。这是目前被诟病最多的可靠性问题。
- **“假承诺”：智能体承诺不行动 [#58450](https://github.com/openclaw/openclaw/issues/58450)** *(15条评论, P1)*：智能体回复了“我稍后检查项目记忆并跟进”之类的话，但实际并未启动任何后台任务。用户将此类行为标记为对系统可靠性的严重侵蚀。
- **内网访问能力争议 [#39604](https://github.com/openclaw/openclaw/issues/39604)** *(13条评论, 9个👍)*：要求 `web_fetch` 工具添加 `allowPrivateNetwork` 配置项。极高的 👍 数表明大量部署在内部网络环境中的用户迫切需要此功能。
- **Cron 作业的“直连执行”诉求 [#18160](https://github.com/openclaw/openclaw/issues/18160)** *(12条评论, 10个👍)*：用户强烈呼吁 Cron 作业能绕过 LLM 的 Agent Turn，直接执行系统命令（Direct Exec），以减少超时和不可预知性。这是社区呼声最高的功能点之一。


### 5. Bug 与稳定性

今日报告的 Bug 中，**数据静默丢失** 和 **安全信息泄露** 是最主要的两大威胁：

**【严重 - 安全与数据丢失】**
- **子智能体结果静默丢失** [#44925](https://github.com/openclaw/openclaw/issues/44925) *(P1)*
- **Write 工具缺少追加模式，Cron 频繁覆写文件致数据丢失** [#40001](https://github.com/openclaw/openclaw/issues/40001) *(P1)*
- **工具调用间文本泄露至消息通道** [#25592](https://github.com/openclaw/openclaw/issues/25592) *(P1)*
- **gh-issues 技能：不可信 Issue 正文直接注入子智能体 Prompt** [#45740](https://github.com/openclaw/openclaw/issues/45740) *(P2, 需安全审查)*
- **Discord 通道泄露 LLM 工具调用原始 JSON** [#44905](https://github.com/openclaw/openclaw/issues/44905) *(P1)*

**【严重 - 核心功能回归/失效】**
- **`exec` 工具不继承技能 `env` 环境变量** [#31583](https://github.com/openclaw/openclaw/issues/31583) *(P1, 回归)*
- **Agent 回复错乱：对上一条消息回应** [#32296](https://github.com/openclaw/openclaw/issues/32296) *(P1)*
- **会话压缩超时导致重复发送与死锁** [#43661](https://github.com/openclaw/openclaw/issues/43661) *(P1, 崩溃循环)*
- **多智能体编排不稳定：并发添加覆盖、会话锁定失败** [#43367](https://github.com/openclaw/openclaw/issues/43367) *(P1)*
- **A2A 双向 `sessions_send` 导致重复消息** [#39476](https://github.com/openclaw/openclaw/issues/39476) *(P1)*
- **Control UI 要求 HTTPS/localhost，VPS 用户无法使用** [#32473](https://github.com/openclaw/openclaw/issues/32473) *(P2, 回归, 4👍)*
- **Docker + Sandbox 路径不能正确绑定 workspace** [#31331](https://github.com/openclaw/openclaw/issues/31331) *(P1)*

**【其他活跃 Bug】**
- MiniMax API 503 特定时间段导致 Cron 持续失败 [#85888](https://github.com/openclaw/openclaw/issues/85888) *(P2)*
- Feishu 读取图片后媒体附件丢失 [#41744](https://github.com/openclaw/openclaw/issues/41744) *(P1)*
- 内存管理模式不规则：不同用户行为不一致 [#43747](https://github.com/openclaw/openclaw/issues/43747) *(P2, 回归)*
- Windows 上 `openclaw update` 报 EBUSY 错误 [#40540](https://github.com/openclaw/openclaw/issues/40540) *(P1)*


### 6. 功能请求与路线图信号

近期功能需求集中在 **可观测性、成本治理 和 企业级编排** 上，响应着“让智能体系统可信可控”的呼声：

| 诉求 | 相关 Issue / PR | 信号强度 |
|---|---|---|
| **Direct Exec 模式（Cron 绕过 LLM）** | [#18160](https://github.com/openclaw/openclaw/issues/18160) (10👍) | **🟢 极高** — 社区共识级 |
| **内网 Web Fetch 访问** | [#39604](https://github.com/openclaw/openclaw/issues/39604) (9👍) | **🟢 极高** |
| **Per-agent 成本预算 / 治理** | [#42475](https://github.com/openclaw/openclaw/issues/42475) / [#35203](https://github.com/openclaw/openclaw/issues/35203) | **🟢 极高** |
| **Per-skill 模型路由** | [#43260](https://github.com/openclaw/openclaw/issues/43260) | **🟡 高** |
| **会话记忆自动保存与合成（`/new` 后）** | [#40418](https://github.com/openclaw/openclaw/issues/40418) | **🟡 高** |
| **Telegram Bot-to-Bot / Guest Bot 支持** | [#79077](https://github.com/openclaw/openclaw/issues/79077) (7👍) | **🟡 高** — 紧跟平台更新 |
| **Browser 工具真实场景优化（CSS选择器等）** | [#44431](https://github.com/openclaw/openclaw/issues/44431) | **🟡 高** — 交互痛点真实反馈 |
| **写/编辑工具暴露到 HTTP /tools/invoke** | [#63919](https://github.com/openclaw/openclaw/pull/63919) | **🔵 路线图中** |

**路线图信号解读：** 仅靠被动回复已无法满足社区需求。用户需要 OpenClaw 像成熟的 PaaS 一样提供**成本控制、资源隔离、确定性执行** 和 **内网操作能力**。这些诉求指向了 **Enterprise Agent Orchestration** 这一目标。


### 7. 用户反馈摘要

**核心痛点（负面情绪集中）：**

- **“静默失败”是最大的信任杀手。** 用户反复强调：子智能体失败了没通知（#44925）、内存操作写坏了不提示（#40001）、承诺了不执行（#58450）、修改了模型配置重启后丢失（#90128）。一位用户在 #43747 中将当前记忆管理描述为 **“混乱”**，认为不同机器的行为完全不一致。
- **部署门槛居高不下。** 一位使用 Hostinger VPS 的用户（#32473）因为缺少 HTTPS 无法使用 Control UI，最终反馈说“我卡住了，找不到解决办法”。Docker 环境下的路径绑定问题（#31331）也由不止一位用户提出。
- **“Agent 自言自语”影响观感。** 内部文本泄露到 Discord/Slack 通道（#25592, #44905）被视为最不可接受的 BUG，一位用户表示“这看起来像个玩具”。

**积极信号（社区成熟度）：**

- 用户表现出极高的技术素养。大量 Issue 附带了详细的 **Root Cause Analysis** 和 **代码级定位**（如 #44925 直接指出多个失败模式 E31/E42/E45），这极大地加速了开发团队的排查效率。
- 对于`Direct Exec Cron`（#18160）和 `Private Network Access`（#39604）的强烈呼吁证明，用户已将 OpenClaw 用于严肃的生产环境，而非简单的个人玩具。用户群体正在从“尝鲜者”向“工程运维者”转变。


### 8. 待处理积压

以下为长期待响应或存在维护风险的条目，提醒维护团队关注：

**⚠️ 高危积压（需尽快响应）**

| 条目 | 状态 | 风险说明 |
|---|---|---|
| `openclaw update` 在 Windows 上 EBUSY | [#40540](https://github.com/openclaw/openclaw/issues/40540) *(P1, 9条评论)* | **更新路径阻塞**。Windows 用户在核心运维上遇到硬墙。 |
| Agent 目录 Bootstrap 文件静默忽略 | [#29387](https://github.com/openclaw/openclaw/issues/29387) *(P1, 14条评论, 5👍)* | **配置不生效**。用户精心配置的 Agent 角色文件未按预期加载。 |
| Sandbox workspace 只读导致工具失败 | [#37634](https://github.com/openclaw/openclaw/issues/37634) *(P1, 9条评论, 6👍)* | **安全策略与功能冲突**。`workspaceAccess` 设为 none 后 workspace 变成只读，使得常规文件操作失效。 |
| Exec 环境变量继承回归 | [#31583](https://github.com/openclaw/openclaw/issues/31583) *(P1, 回归, 审查中)* | 12条评论，影响范围广（密钥注入、技能隔离）。 |

**📌 长期站桩（功能请求/等待决策）**

- **Direct Exec Cron** [#18160](https://github.com/openclaw/openclaw/issues/18160) *(2月提出，10个👍)* — 社区持续关注，但从 2 月到现在仍未进入主线。
- **记忆/嵌入设置应加入初始化向导** [#16670](https://github.com/openclaw/openclaw/issues/16670) *(2月提出)* — 这直接影响到新用户的留存和核心功能的认知。
- **子智能体完成后执行钩子** [#22358](https://github.com/openclaw/openclaw/issues/22358) *(2月提出)* — 对可扩展性非常重要。

**🔄 待审 PR（风险/停滞）**

- **Coding Tools 暴露到 HTTP** [#63919](https://github.com/openclaw/openclaw/pull/63919) *(L 级 PR)* — 功能全面但风险高，安全审查与兼容性验证耗时较长，需要维护者投入专注度。
- **内存搜索优化 FTS5** [#47754](https://github.com/openclaw/openclaw/pull/47754) *(3月提交，标记为 Stale)* — 一个质量颇高的搜索体验优化 PR，内存模块的核心痛点之一，建议尽快合并。

---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告

**分析周期：** 2026-06-11  
**分析师：** AI 智能体与个人 AI 助手领域资深技术分析师

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“大爆炸”向“工程化”过渡**的关键阶段。过去 24 小时，覆盖全生态的 **13 个主要项目中有 10 个保持活跃**，总计处理超过 **800 条 Issue 和 850 个 PR**，发布 5 个新版本。生态的显著特征是：**基础能力趋同（对话/工具/记忆/多平台）已不再是差异化重心，稳定可靠、可观测、可治理成为社区共识性刚需。** 子智能体静默失败、消息重复、上下文污染、跨平台兼容问题在多个项目中集中爆发，表明行业正从“demo 可用”加速迈向“生产可用”。与此同时，**Computer Use、Direct Exec、轻量化插件系统、内网访问**等下一代能力已开始被社区主动定义，生态整体向着“Agent 基础设施平台”演进。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|------|--------------|-----------|---------|-----------|
| **OpenClaw** | 500（新开+活跃） | 500（合并104） | ✅ v2026.6.6-beta.1 | 极高活跃，安全与稳定性攻坚，P1 Bug 积压较多 |
| **NanoBot** | 4 新开 | 19 合并 + 14 待审 | ❌ | 极高活跃，社区贡献突出，核心修复节奏快 |
| **Hermes Agent** | 50（新开42/关闭8） | 50（合并11） | ❌ | 高度活跃，审查吞吐压力大，关键 Bug 修复集中 |
| **PicoClaw** | 10+10（估20） | 6 合并 | ✅ nightly | 健康高速迭代，跨平台/安全修复并行 |
| **NanoClaw** | 2 新开 | 12（4合并+8待审） | ❌ | 贡献活跃度高，Skills 生态井喷，审查积压上升 |
| **NullClaw** | 0 新开 | 4 待审 | ❌ | 低活跃，产出质量扎实，社区互动少 |
| **IronClaw** | 50（新开+活跃35/关闭15） | 50（合并22/待审28） | ❌（发布阻塞） | 高度活跃，Reborn WebUI 密集迭代，发布流程卡顿 |
| **LobsterAI** | 0 新开 | 24 合并 | ✅ v2026.6.10 | 功能扩张与偿债并行，Computer Use 里程碑落地 |
| **TinyClaw** | 0 | 0 | ❌ | 不活跃 |
| **Moltis** | 0 | 0 | ❌ | 不活跃 |
| **CoPaw** | 33 | 49（合并24） | ✅ v1.1.11 + beta | 快速迭代，Windows Bug 严重但响应迅速 |
| **ZeptoClaw** | 0 | 0 | ❌ | 不活跃 |
| **ZeroClaw** | 43（新开+活跃） | 50（合并/关闭未明确） | ❌ | 快速迭代，CI 流程优化，架构 RFC 讨论深入 |

> 注：更新数为项目日报中披露的总事件数（含新开、活跃、关闭）；部分项目以“新开”或“活跃”上报，此处统一取所披露的最大口径。

---

## 3. OpenClaw 在生态中的定位

**OpenClaw 是该生态中体量最大、能力最全面、社区最活跃的旗舰项目**，在以下维度形成显著优势：

| 维度 | OpenClaw | 同类对比 |
|------|----------|----------|
| **社区规模** | 日处理 500 Issue/500 PR，远超所有项目（第二梯队约 50 级别），社区体量为生态内第 1 梯队独一档。 | 生态内活跃度第 2 梯队的 IronClaw、CoPaw、ZeroClaw 约为其 1/10。 |
| **功能完整度** | 拥有完整的安全沙箱、MCP/ACP 协议支持、子智能体编排、多平台网关、会话质量管理、成本治理钩子等，覆盖最广。 | NanoBot 专注消息通道，Hermes 更灵活但边界松散，LobsterAI 侧重桌面原生，CoPaw 有强 OEM 平台绑定。 |
| **技术路线** | 倾向于 **“大统一 + 安全优先”**：v2026.6.6-beta.1 显示其选择对整个系统做安全收紧，走企业级管控路线。同时重度投入 SQLite 迁移（#88838）和会话治理。 | 对比之下，Hermes Agent 更倾向于多样性实验（如 Gemma 4 支持、无障碍 PR），NanoBot 倾向快速响应社区 PR，ZeroClaw 正讨论统一架构以减少碎片（#7415）。 |
| **质量挑战** | 功能膨胀导致 P1 Bug 积压最多（消息丢失、工具、环境变量继承等），稳定性修复攻坚战仍在持续。 | IronClaw 同样面临 Release 阻塞和 WebUI 早期 Bug 潮；CoPaw 新版本 Window 启动 Bug 拉低信心。 |

**结论：OpenClaw 是生态的“能力上限”和“复杂度上限”标杆**，其面临的问题（安全 vs 便利、功能 vs 稳定）也是整个行业下一阶段需要回答的命题。

---

## 4. 共同关注的技术方向

以下诉求至少出现在 3 个或以上项目中，反映行业普遍痛点：

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|---------|---------|
| **子智能体/任务的静默失败** | OpenClaw（#44925）、NanoBot（#4290）、ZeroClaw（#7263）、PicoClaw（#3094） | 子智能体未完成/超时/结果丢失，无通知无重试，社区视为“信任杀手”。 |
| **消息/上下文污染与重复** | OpenClaw（#25592 内部文本泄漏）、NanoBot（#4274 跨会话污染）、Hermes（#43835 Telegram 双重回复）、CoPaw（#5057 空卡片）、ZeroClaw（#6034 消息丢失） | 多通道场景下消息路由一致性、工具调用内部文本误暴露至用户界面。 |
| **Direct Exec / Cron 绕过 LLM** | OpenClaw（#18160 10👍）、LobsterAI（定时任务增强）、CoPaw（#5064 定时任务不可控） | 社区期望定时任务和后台作业能直接执行系统命令，减少 LLM 轮次的不可预测性。 |
| **内网/私有网络访问** | OpenClaw（#39604 9👍）、IronClaw（#2731 host.docker.internal）、NanoClaw（#2731 Egress 阻断） | 大量用户将 Agent 部署在企业或本地环境，要求 web_fetch 等工具支持私有 IP。 |
| **跨平台兼容性（尤其是 Windows）** | OpenClaw（#40540 Windows EBUSY）、Hermes（#23402 Docker 权限）、LobsterAI（#2142 NSIS 安装器）、CoPaw（#5086 OpenSSL 崩溃）、ZeroClaw（#7462 74个测试失败） | Windows 作为第二平台持续遭遇启动、更新、文件路径等严重问题。 |
| **安全敏感信息处理** | OpenClaw（MCP SSRF #92021）、Hermes（#33801 密钥编辑破坏代码、#43666 持久化边界泄露）、NanoClaw（Guardrails 技能 #2726）、PicoClaw（#3085 SSRF 绕过） | 密钥编辑、SSRF 防护、私有 Token 治理需求集中爆发。 |
| **配置即代码/声明式管理** | IronClaw（#3036 Configuration-as-Code Epic）、ZeroClaw（#7468 重命名工具）、NullClaw（#949 默认队列模式配置）、NanoClaw 多 Skill PR | 社区对“改配置靠编辑 .env 或 JSON”模式不满，期望 schema、审计、版本控制。 |
| **成本控制与可观测性** | OpenClaw（#42475 Per-agent 预算）、NanoClaw（#2727 日志持久化、#2211 工具预览）、IronClaw（Token 用量讨论）、CoPaw（#4433 Token 显示 PR） | 从“能用”到“用得起、看得清”是生产级部署的前提。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|---------|----------|----------------|
| **OpenClaw** | 全栈智能体平台：安全沙箱、MCP/ACP、多网关、企业治理 | 高级开发者/运维/企业团队 | 大单体 + 严格安全边界 + 强插件机制 |
| **NanoBot** | 轻量消息机器人（Telegram/飞书） + 快速迭代 | 个人开发者/Telegram Bot 使用者 | 极简架构，社区 PR 驱动，快速响应 |
| **Hermes Agent** | 研究级智能体框架：灵活配置、多后端、无障碍 | 研究者/技术极客 | 松散耦合，多模块可替换，强社区创新，但维护压力大 |
| **PicoClaw** | 嵌入式/轻量级开源变体 | 嵌入式/MCU 爱好者？实际是桌面级简化版 | 轻量 fork，跟随 OpenClaw 核心，精简依赖 |
| **NanoClaw** | “Skills” 为核心的最小化社区版 | 轻量用户/Skills 贡献者 | 极轻核心 + 社区贡献独立 Skills，近期生态爆发 |
| **NullClaw** | 极简 Agent 框架，强调可靠性 | 最小化主义者/测试场景 | 代码量极少，通过少量 PR 修复关键 Bug，社区冷清 |
| **IronClaw** | 生产级 Agent 自动化（Cron/Auth/WebUI） | 运维/自动化工作流用户 | Rust+WASM 架构，Reborn WebUI v2 是当前迭代焦点 |
| **LobsterAI** | 桌面原生 Agent（Windows/macOS）+ Computer Use | 桌面用户/注重隐私/本地化 | Electron + 内嵌 Computer Use，直击桌面自动化需求 |
| **CoPaw (QwenPaw)** | 多平台强绑定（小米/钉钉/微信）+ 快速 OEM 集成 | 国内用户/小米/钉钉生态 | 与 AgentScope 2.0 深度绑定，版本节奏快，但 Windows 稳定性有缺口 |
| **ZeroClaw** | 单一仓库全功能 Agent 框架 | 全栈开发者/自部署用户 | Rust 实现，正讨论统一执行引擎（#7415）和原生插件系统（#7420） |

---

## 6. 社区热度与成熟度

按今日活跃度和迭代阶段分层：

### 第一梯队：极高活跃 · 快速迭代期（日均处理 Issue/PR 接近或超过 50）

- **OpenClaw** — 生态绝对头部，但功能膨胀带来大量积压 Bug，处于“功能扩展 vs 质量修复并行”阶段。
- **IronClaw** — Reborn WebUI 密集开发，但 Release 发布阻塞（crates.io 落后）成为主要内部风险。
- **CoPaw** — 版本节奏极快（一天发 2 版），但兼容性 Bug 频发，属于“先推功能再修 Bug”模式。
- **ZeroClaw** — 同样高吞吐，架构性 RFC 讨论成熟，但 Windows 兼容拖后腿。

### 第二梯队：中等活跃 · 质量巩固 / 功能扩张期（日均处理 10–30）

- **NanoBot** — 每日约 15-25 个 PR 处理，社区贡献质量高，面向稳定可靠性集中修复，已进入 0.2.x 成熟期。
- **Hermes Agent** — 每日 50 左右 Issue/PR 但合并率低，维护瓶颈明显，处于“社区贡献旺盛但审查跟不上”的亚健康活跃。
- **LobsterAI** — 今日合并 24 个 PR，属功能爆发日，但无新 Issue，说明团队在集中合入积压。整体健康，但 Electron 依赖（#1277）严重过时。
- **NanoClaw** — Skills 生态井喷，审查积压上升，处于“社区贡献爆发 → 期待官方响应”的关键窗口期。

### 第三梯队：低活跃 / 休眠期（日均处理 0–5）

- **PicoClaw** — 仅 6 个合并，日常维护为主，无明显增长。
- **NullClaw** — 4 个 PR，无合并，社区互动为零，接近维护模式。
- **TinyClaw / Moltis / ZeptoClaw** — 24 小时无活动，实质休眠。

---

## 7. 值得关注的趋势信号

### 7.1 “静默失败”正在从 Bug 升级为信任危机

至少 5 个项目（OpenClaw #44925、NanoBot #4290、ZeroClaw #7263、CoPaw #5064、NullClaw #951）均涉及 Agent/子智能体任务不交付结果或不执行承诺。**用户已经将“承诺但不行动”等同于 Bug 而非功能缺失**。行业必须将“结果可追溯、失败可通知”作为 Agent 产品的基线能力。

### 7.2 Direct Exec 成为社区级共识，暗示“LLM-as-Judge”的边界反思

OpenClaw、CoPaw、LobsterAI 的定时任务模块中，社区反复要求“让 Cron 直接执行，不经过 LLM Turn”。这表明在确定性需求场景下，用户认为**LLM 的介入增加了不可预测性和延迟**。未来 Agent 框架可能分化出“决策层（LLM）”和“执行层（确定性系统）”的明确分层。

### 7.3 私有/内网网络访问是部署模式的关键分水岭

OpenClaw、IronClaw、NanoClaw 都出现“Agent 无法访问内网服务（host.docker.internal）或专用 IP 段”的问题。**Agent 正从纯 SaaS 工具向内部基础设施演进**，支持私有网络已成“严肃部署”的前提条件。尚未将此纳入路线图的项目将错过企业用户。

### 7.4 Computer Use / 桌面自动化成为下一轮功能高地

LobsterAI 将 Computer Use MVP 合入主线（PR #2143），OpenClaw 也有 Browser 工具优化请求（#44431），CoPaw 在讨论子代理进展可视化。**控制桌面 GUI 不再是实验性功能，而是“Agent 真正干活”的标志能力**。预计 2026 下半年此方向将成为生态竞争主战场。

### 7.5 成本预警与可观测性快速崛起

OpenClaw 有 Per-agent 成本预算（#42475），CoPaw 有 Token 用量显示（PR #4433），IronClaw 有配置即代码（#3036）。**当 Agent 能够自主调用工具、消耗 Token 时，“成本失控”就变得真实**。社区正在自发要求“预算门禁”、“用量面板”和“细粒度审计日志”。这标志着智能体从“玩具”向“生产力工具”转型的必然制度设计。

### 7.6 社区贡献爆炸与审查瓶颈的矛盾趋紧

Hermes Agent（合并率仅 22%）、NanoClaw（8 个待审 PR 持续积压）、ZeroClaw（核心 RFC 无维护者回复）都呈现 **“社区写代码速度超过核心团队 review 速度”** 的危险信号。生态的健康度不仅看提交量，更要看合并反馈周期。若长期不加干预，可能引发贡献者流失和分支碎片化。

---

*报告结束。数据来源于各项目公开 GitHub 仓库及维护团队发布的项目日报。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 NanoBot 项目动态日报。

---

### NanoBot 项目日报 | 2026-06-11

**数据周期：** 2026-06-10 ~ 2026-06-11

---

#### 1. 今日速览

过去 24 小时内项目整体呈现 **极高活跃度**，开发节奏非常快。总计有 19 个 PR 被合并/关闭，14 个新 PR 待审，同时社区报告了 4 个新 Issue。项目团队本周重点聚焦 **核心稳定性修复**（上下文污染、流中断处理）与 **平台体验优化**（WebUI 大文件处理、版本号显示）。社区力量表现突出，多位外部贡献者提交了高质量的 Bug 修复和功能增强 PR，显示了项目健康、蓬勃的社区生态。

---

#### 2. 版本发布

过去 24 小时无新版本发布。

---

#### 3. 项目进展（重大合并/关闭 PR）

昨天是项目修复和优化的关键一天，多个影响用户体验的严重 Bug 和 QoL 改进已落地：

- **（关键修复）上下文污染隔离** - 跨会话 `history.jsonl` 注入导致 AI 混淆的问题已被彻底解决。PR [#4274](HKUDS/nanobot Issue #4274) 为历史记录加入 `session_key` 过滤，确保只有当前会话的历史被注入 `system prompt`，让多会话使用体验更加可靠。
- **（关键修复）流中断 Fallback 机制** - 针对 LLM 流中断时无响应的痛点，PR [#4272](HKUDS/nanobot PR #4272) 已合并。系统现在会在流中断时自动重试并 Fallback 到备用模型，显著提升了调用稳定性。
- **（WebUI）大型聊天记录处理** - [#4247](HKUDS/nanobot PR #4247) 修复了 Transcript 文件超过 8MB 时 WebUI 历史对话完全消失的问题；[#4278](HKUDS/nanobot PR #4278) 进一步引入了分段存储，优化了大型对话的加载效率。
- **（WebUI）辅助功能** - [#4255](HKUDS/nanobot PR #4255) 实现了按需版本检查，在设置中增加了手动更新按钮，避免了后台轮询对性能的消耗。
- **（基础能力）Exec 工具增强** - [#4273](HKUDS/nanobot PR #4273) 新增了 `tools.exec.pathPrepend` 配置项，解决了虚拟环境 `PATH` 优先级被系统 Python 覆盖的问题，显著提升了 Python 脚本执行的灵活性。
- **（平台适配）生态扩展** - [#4281](HKUDS/nanobot PR #4281) 加入了对阶跃星辰 (StepFun) 语音转录的原生支持；[#4277](HKUDS/nanobot PR #4277) 优化了飞书的 SDK 懒加载，降低资源占用。

---

#### 4. 社区热点

1. **模型空回复无法触发回退** - [Issue #4287](HKUDS/nanobot Issue #4287)
   这是昨日社区最关注的问题。用户 `glebov` 报告其 Telegram Bot 在使用 DeepSeek 时，API 高峰期返回空 `choices` 导致请求硬失败。当前的错误分类机制未能将此触发 Fallback。该问题引发了社区对 **生产环境高可用性** 的热烈讨论，已有关联 PR [#4288](HKUDS/nanobot PR #4288) 紧急提交。

2. **Crontab 任务与 Subagent 冲突** - [Issue #4290](HKUDS/nanobot Issue #4290)
   用户 `tjc0726` 报告的自动化流程 Bug：当定时任务生成 Subagent 后，主 Agent 无法消费 Subagent 的返回结果导致工作流中断。这是对 **多 Agent 协作稳定性** 的强烈诉求，幸好对应的 PR [#4293](HKUDS/nanobot PR #4293) 已经提交。

3. **WebUI 显示版本号** - [Issue #4233](HKUDS/nanobot Issue #4233)
   这是一个体量虽小但获得了广泛共鸣的需求。用户 `viblo` 建议在 WebUI 显示版本号及更新提示，该诉求已被采纳并合并（PR #4255），展示了项目组对基础用户体验的关注。

---

#### 5. Bug 与稳定性

按严重程度排列：

- **（严重）Crontab 任务过早结束** - [[Issue #4290]](HKUDS/nanobot Issue #4290)
   *严重性：* 核心自动化流程受损。已有修复 PR [#4293](HKUDS/nanobot PR #4293) 待合并。
- **（严重）模型高峰期空回显无 Fallback** - [[Issue #4287]](HKUDS/nanobot Issue #4287)
  *严重性：* 导致用户在高峰时段完全不可用。已有修复 PR [#4288](HKUDS/nanobot PR #4288) 待合并。
- **（高）WebUI 大 Transcript 导致历史丢失** - [[已修复/已合并]](HKUDS/nanobot PR #4247)
  *严重性：* 曾导致长对话用户的聊天记录完全消失。已修复。
- **（高）跨会话上下文污染** - [[已修复/已合并]](HKUDS/nanobot PR #4274)
  *严重性：* 隐蔽的上下文注入问题，严重影响多会话场景。已修复。
- **（中）Bwrap 沙箱 $HOME 未隔离** - [[已修复]](HKUDS/nanobot Issue #4237)
  *严重性：* 沙箱内命令因访问宿主机 HOME 路径而失败。已由开发者 `primit1v0` 报告和验证修复。
- **（中）消息分割破坏 Markdown 代码块** - [[Issue/PR #4257]](HKUDS/nanobot Issue #4257)
  *严重性：* 影响长消息中代码渲染。暂无维护者反馈，待处理。
- **（低）OpenAI 兼容 Provider 参数名冲突** - [[已修复]](HKUDS/nanobot Issue #4261)
   *细节：* 修复了 `max_tokens` 与 `max_completion_tokens` 在 GPT-5.x 系列的兼容性问题。

---

#### 6. 功能请求与路线图信号

- **多 Agent / 子智能体能力增强**
  - *可配置模型预设：* PR [#4291](HKUDS/nanobot PR #4291) 开放。允许 Subagent 调用不同的模型 Provider，显著增强了多 Agent 调度的灵活性。
  - *聚合通知：* Issue [#4279](HKUDS/nanobot Issue #4279) 提出了一个高级功能，要求 Subagent 结果聚合后再交付给主 Agent，以防止 LLM 因并发返回而产生幻觉。
- **平台集成精细化**
  - *Slack @提及控制：* PR [#4289](HKUDS/nanobot PR #4289) 增加了 `groupRequireMention` 选项，帮助企业在频道中减少不必要的 Bot 干扰。
  - *WebUI 技能激活：* PR [#4284](HKUDS/nanobot PR #4284) 通过 `/skill` 命令激活技能，优化了 WebUI 交互流程。
  - *WebUI 文件管理：* PR [#4282](HKUDS/nanobot PR #4282) 允许用户在 WebUI 直接浏览和管理服务器文件，这是一个非常受社区欢迎的实用功能。
- **稳定性与调试**
  - *Crontab 参数严格校验：* PR [#4285](HKUDS/nanobot PR #4285) 增加了对定时任务参数的运行前校验，减少配置错误。
  - *上下文连续性优化：* PR [#4280](HKUDS/nanobot PR #4280) 尝试改进了在上下文窗口压力下的短期记忆丢失问题。

---

#### 7. 用户反馈摘要

- **正面反馈**：用户 `viblo` (Issue #4233) 和 `mxnbf` (Issue #4013) 表现出了极高的用户满意度。特别是 `mxnbf` 在抱怨新版本 Bug 的同时毫不吝啬对旧版本的赞美，说明项目在核心体验上有很强的用户黏性。
- **主要痛点**：
  - **升级回归**：`mxnbf` 从 0.1.5 升级到 0.2.0 后遭遇了流中断，这是一个大型版本升级后的典型阵痛。
  - **环境配置困扰**：`chinaliufei` (Issue #3934) 深刻描述了 Python 环境 PATH 问题，这类环境配置问题如果不解决会劝退很多开发者用户。
  - **数据/会话**：`chxuan` (Issue #4259) 发现的上下文污染 Bug 用户非常隐蔽，若不修复会长期影响用户体验。`glebov` (Issue #4287) 则代表了正在将 NanoBot 投入生产的用户群体，他们对可靠性极度敏感。

---

#### 8. 待处理积压

**紧急（需24小时内关注）**
- **修复 Crontab + Subagent 工作流**：[Issue #4290](HKUDS/nanobot Issue #4290) / [PR #4293](HKUDS/nanobot PR #4293)
  *提醒：* Crontab 功能是自动化的基石，此 Bug 严重影响核心功能。请维护者尽快 Review 并合并 #4293。
- **修复空回显 Fallback**：[Issue #4287](HKUDS/nanobot Issue #4287) / [PR #4288](HKUDS/nanobot PR #4288)
  *提醒：* 生产环境的刚需，建议优先合并。

**常规（需本周内关注）**
- **消息分割的代码块保护**：[PR #4257](HKUDS/nanobot PR #4257)
  *提醒：* 自提出后暂时没有维护者回复。这是一个影响前端渲染的 Bug，希望团队可以安排 Review。
- **上下文连续性优化方案**：[PR #4280](HKUDS/nanobot PR #4280)
  *提醒：* 针对 #4044 的长期问题进行修复，设计较为复杂，建议尽早评估以避免内存相关的长期隐患。
- **Crontab 参数校验**：[PR #4285](HKUDS/nanobot PR #4285)
  *提醒：* 虽然是改进，但能有效预防用户配置出错，值得合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我为您生成了 Hermes Agent 项目 2026年6月11日的项目动态日报。

---

## Hermes Agent 项目动态日报

**日期:** 2026-06-11
**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

- **项目高度活跃，但社区请求与Bug修复的吞吐量存在落差。** 过去24小时内有大量 Issue (50条) 和 PR (50条) 被更新，显示出极强的社区参与度和开发活动。然而，新开启的活跃 Issue 数量（42条）远超今日关闭的 Issue 数量（8条），而 PR 的合并/关闭率（11/50）也相对较低，这可能预示着维护团队在代码审查和合并方面面临一定压力，社区反馈的积压可能正在增加。
- **稳定性与安全修复是今日焦点。** 今日动态中涉及了多个 P1/P2 级别的严重 Bug，例如 Cron 任务因模型参数缺失而失败、密钥编辑功能破坏代码语法等，同时也有针对安全漏洞（如 Webhook 签名校验、常量时间比较）的修复。这表明项目正积极应对稳定性挑战。
- **项目在 Plist 管理、Cron 功能、技能系统等多个方面都有所推进。** 尽管合并比例不高，但今天关闭/合并的 PR 中包含了关键的功能修复和优化，例如解决了 macOS 上 `launchd` 管理的 Gateway 重启失败问题、明确了 Cron 任务的配置文件属主，以及完善了技能系统的文件排除和名称解析。
- **社区痛点集中在桌面体验、平台插件（Telegram, macOS）集成和配置管理上。** 从热门 Issue 来看，用户对桌面应用的功能完善（如无障碍访问、草稿持久化）、平台消息的重复处理以及 Docker/macOS 环境的配置管理有较高期待和反馈。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

在过去的24小时内，共有 **11 个 PR** 被成功合并或关闭，标志着项目在以下几个关键方向上取得了实质性的进展：

- **系统稳定性与核心功能修复:**
    - **[P1] Gateway 重连机制增强:** 合并的 PR `#18922` (by NeloReis) 修复了当 Gateway 在“脏关闭”（如未收到SIGTERM、崩溃）后，会话被错误挂起而非恢复的问题。现在系统会尝试恢复最近的活动会话，避免用户丢失对话历史。这对于基于 Telegram 等即时通讯平台的使用体验是重要的改进。
    - **[P2] 技能系统文件泄露修复:** 合并的 PR `#18897` (by SimbaKingjoe) 修复了 `_find_skill` 函数在搜索 `.git`, `.archive` 等目录时没有进行过滤的问题，与 `iter_skill_index_files` 保持了一致。
    - **[P2] 技能查找循环修复:** 合并的 PR `#18901` (by shellybotmoyer) 修复了 `skills_list` 用前端名称显示技能，但 `skill_view` 只能通过目录名查找的技能发现-加载循环问题，保证了Agent能够正确加载它发现的技能。
    - **[P2] 模型配置修复:** 合并的 PR `#18889` (by liuhao1024) 修复了 models.dev 数据中 `modalities.input` 和 `attachment` 标志不一致导致的能力误判问题。
    - **[P2] 上下文压缩修复:** 合并的 PR `#18877` (by rkt2spc) 修复了辅助压缩模型忽略 `custom_providers` 中 `context_length` 设置的问题，现在用户自定义的上下文长度限制会正确应用于所有压缩路径。
- **功能增强:** 
    - **[P3]** **UI体验优化:** 合并的 PR `#18903` (by rahulraikwar00) 在网站 UI 的安装命令旁添加了“一键复制”按钮，提升了用户易用性。
    - **[P3]** **终端输出可配置性:** 合并的 PR `#43582` (by xxxigm) 引入了 `display.terminal_code_blocks` 切换开关，允许用户在支持Markdown的平台上，选择是将终端输出渲染为紧凑的代码块还是展开的完整代码块。
    - **[P3]** **配置管理增强:** 合并的 PR `#43808` (by teknium1) 使 Dashboard 能够管理任意 Profile 的技能和工具集，修复了之前管理界面切换 Profile 后不会生效的问题。
- **其他:** 合并的 PR `#43602` (by donovan-yohan) 完善了 Baoyu 图像生成工作流的相关文档。

**小结:** 项目今日重点解决了技能系统和会话管理中的几个关键 Bug，并对 UI 和配置管理进行了增量优化，朝着更稳定、更易用的方向稳步前进。

### 4. 社区热点

- **#23402 [[Bug]: Docker with HERMES_UID; permissions issue with Dashboard chat](https://github.com/NousResearch/hermes-agent/issues/23402)**
  - **状态: OPEN**
  - **评论数: 15 (最多)**
  - **诉求分析:** 这是今日讨论最激烈的问题，涉及 Docker 环境下的权限配置。用户试图更新 Unraid 模板以适配新的 Docker 指南，但在使用 Dashboard 的 Chat 功能时遇到权限问题。这暴露了 Docker 部署文档与实战之间存在的差距，以及权限管理（UID/GID映射）的复杂性，是自部署用户头疼的典型问题。

- **#26689 [Accessibility improvements for blind VoiceOver users](https://github.com/NousResearch/hermes-agent/issues/26689)**
  - **状态: OPEN**
  - **评论数: 9 (次多)**
  - **诉求分析:** 来自视障用户的声音，指出尽管 Hermes Agent 后端强大，但当前的 TUI 和桌面端 UI 对屏幕阅读器（macOS VoiceOver）支持极差，导致他们无法使用。这不仅是功能请求，更是对项目包容性的诉求。社区对此话题的响应表明，用户群体是多元化的，且对无障碍体验有较高期待。

- **#33801 [[Bug]: Secret redaction corrupts code syntax in tool output](https://github.com/NousResearch/hermes-agent/issues/33801)**
  - **状态: OPEN**
  - **评论数: 5**
  - **诉求分析:** 这是一个相当严重的设计缺陷。安全机制（密钥编辑）在内容层（写入文件前）直接替换文本中的密钥，破坏了 Python/Shell 代码的语法，导致工具执行静默失败。用户的诉求是在保证安全的同时，不能以牺牲功能完整性为代价，社区很可能期待一个更智能的、仅在展示时进行的编辑机制。

- **#6626 [Gemma 4 tool calling support](https://github.com/NousResearch/hermes-agent/issues/6626)**
  - **状态: OPEN**
  - **评论数: 5**
  - **诉求分析:** 用户正在尝试集成最新的 Gemma 4 模型，并遇到了工具调用解析问题。这体现了社区对新模型、新语言模型后端集成的强烈需求，用户希望 Hermes Agent 能快速适配行业内的主流模型。

### 5. Bug 与稳定性

以下为今日报告的部分重要 Bug，按严重程度排列：

**P1 (严重)**
- **#43899 [Bug]: Cron jobs fail with 'Model parameter is required'** - Cron 任务在没有显式设置模型参数时失败，即使 `config.yaml` 中有默认模型。用户已提供复现步骤。已有对应 **Fix PR #43952**。
- **#24187 [Bug]: SessionDB silently skips current turn when message repair shortens conversation history** - 会话修复机制缩短消息列表后，持久化逻辑使用旧的历史长度作为偏移量，导致静默跳过当前轮次，造成对话信息丢失。

**P2 (高)**
- **#33801 [Bug]: Secret redaction corrupts code syntax in tool output** - 密钥编辑机制会破坏写入到文件中的代码语法，导致工具失败。这是一个安全性与功能性冲突的典型案例。
- **#43475 [/restart bricks a launchd-managed gateway on macOS]** - 在 macOS 上通过 `launchd` 管理的 Gateway 执行重启命令后无法自动重新启动，导致服务永久离线。
- **#43835 [Bug]: Telegram: double messages (tool output + response body) for single user message** - 用户在 Telegram 上收到两条回复（工具输出 + 文本回复），造成“重复回复”的困扰，影响信息接收体验。
- **#43915 [Bug]: Bedrock streaming transient faults abort turn non-retryably** - AWS Bedrock 临时性流式故障直接终止了本轮推理，而非重试，即使重试可以成功。这影响了服务的可用性。
- **#43666 [Redaction gaps at the persistence boundary]** - 审计发现，即使开启了密钥编辑功能，在 `state.db` 中仍有23处明文的密码。密钥编辑存在严重的边界漏洞，安全风险很高。
- **#43842 [macOS: plist refresh bootout from inside the gateway kills the CLI before bootstrap]** - 当 Agent 通过自身终端工具发起更新时，plist 刷新操作会先终止自身进程，导致更新中断。这是一个典型的自引用更新问题。

**P3 (中)**
- **#43900 [Bug] Ollama local models silently capped at 4096-token context** - 使用本地 Ollama 模型时，硬件配置支持大上下文（如131K），但 Hermes Agent 未正确将读取到的配置应用到 Ollama 请求中，导致模型被软件静默限制在 4096 上下文。这会让用户困惑，总觉得模型“太笨”或记不住东西。

### 6. 功能请求与路线图信号

- **本地化与国际化:** #40239 (Add Portuguese (pt-BR) language support) 是今天讨论度较高的功能请求，表明用户对桌面应用的本地化有明确需求。考虑到项目已存在 `locales/pt.yaml` 的翻译文件，这很可能是一个相对容易实现且呼声较高的功能。
- **无障碍支持:** #26689 (Accessibility improvements for blind VoiceOver users) 提供了用户视角的详细改进清单。这个Issue的存在本身就是一个强烈的路线图信号：社区期待项目在功能强大之外，也重视包容性设计。
- **桌面端功能完善:** 多个今日开启的 PR 直接点出了桌面端的改进方向，例如：
    - **PR #43939**: 草稿持久化与按会话隔离，这将解决用户在多个会话间切换时文字丢失的问题。
    - **PR #43507**: 提供类似 Claude.ai 的追问建议功能，增强用户引导和交互深度。
    - **PR #43411**: 新增 `/api/audio/transcribe` 端点，为语音交互铺路。
- **配置与部署灵活性:**
    - **#43473 [Feature]: Make container's .env mode/group configurable** 请求让 Docker 容器的 `.env` 文件权限可配置，这对于有主机文件访问需求的自部署用户是重要改进。
    - **PR #43956 [revert(cron): remove per-job profile support]** 这是一个关于 Cron 功能设计的撤销操作，暗示团队可能在于 Profile 关联性上简化设计，降低复杂性。

### 7. 用户反馈摘要

- **Docker 用户痛点:** 用户 `mmartial` 在尝试为其 Unraid 模板适配官方 Docker 指南时遇到权限问题，反映出现有 Docker 文档在实际部署场景（如 Unraid 这类 NAS 系统）中的指导和兼容性不足。用户原文：“Attempting to update my Unraid Template ... to reflect new guidelines ... I tried to use the `Chat` feature within a newly started container...”。这表明，Docker 的最佳实践需要更具体的环境考量。
- **无障碍需求:** 视障用户 `xiaopinpin-music` 指出 BUI 和桌面应用完全无法通过屏幕阅读器使用，这对一些核心功能（如对话、配置）构成了巨大的障碍。用户的诉求非常清晰和急切，“I am a totally blind VoiceOver user ... the current UX is very difficult for screen-reader users.” 这强烈呼吁项目组将无障碍作为一项基本特性来对待。
- **安装体验不满:** 用户 `ahillzhao-msn` 抱怨在 Windows 上执行 `hermes update` 需要约10分钟，原因是 Node.js 依赖每次都无条件重新安装。用户原文：“`hermes update` on Windows takes approximately 10 minutes. The vast majority of time is spent on Node.js dependency installation...”。这暴露了安装脚本的性能问题和资源浪费，带来了糟糕的首次使用体验。
- **消息平台体验问题:** 用户 `Jduio` 和社区成员在 Issue #43835 中报告了 Telegram 平台上的“双重回复”现象，影响了消息的可读性和用户预期。用户的直接感受是“repeating or double responses”，这是一个破坏核心交互体验的 Bug。

### 8. 待处理积压

以下为长期未响或可能被忽视的重要 Issue，提醒维护者关注：

- **#33801 [Bug]: Secret redaction corrupts code syntax in tool output** - 这是一个 P2 级别的设计缺陷，已有5条评论且被多次点赞，虽然未被分配或标记，但影响面广泛（威胁所有需要写文件或执行代码的工具），代表社区对“不加区分地进行安全编辑”模式的普遍不满。至今没有对应的 Fix PR，亟待解决。
- **#24187 [Bug]: SessionDB silently skips current turn** - 这是一个 P1 级别的数据丢失 Bug，创建于2026-05-12，至今仍为OPEN状态，且没有对应的 Fix PR。会话轮次静默丢失会严重影响用户对 Agent 的信任。这是一个非常高优先级但似乎被搁置的问题。
- **#17198 [gateway restart: race condition causes Weixin token conflict]** - 创建于2026-04-29，更新于今日，说明问题一直存在。这是一个 P2 级别且影响微信集成用户的稳定性问题，至今未见明确修复方案，可能因为微信平台的维护优先级较低。
- **#43475 [/restart bricks a launchd-managed gateway on macOS]** - 这是一个 P2 级别的问题，直接影响了 macOS 用户的核心使用。虽有 PR #43842 揭示了更深层的问题，但 #43475 本身仍处于 Open 状态。如果团队认为 #43475 是 #43842 的子问题或已解决，应明确更新状态，否则就是关键的待处理积压。
- **#43666 [Redaction gaps at the persistence boundary]:** 该问题指向了核心安全机制的严重缺陷，虽然和 #33801 属于同类问题，但性质更严重（已找到明文泄露证据）。维护者应将其与 #33801 合并处理，并优先开发更完善的编辑方案。
- **#43575 [Webhook signature validation doesn't support Fireflies V2]:** 这是一个影响与第三方服务Fireflies集成的 Bug，已有1条评论。如果目标是支持多样的Webhook生态，该请求应该被确认和规划。

---

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已经根据您提供的PicoClaw GitHub数据，为您生成了2026年6月11日的项目动态日报。

---

### PicoClaw 开源项目动态日报 (2026-06-11)

报告周期：2026-06-10 至 2026-06-11

---

### 1. 今日速览

今日项目活跃度极高，代码评审与合并节奏加快，项目整体处于健康、高速迭代状态。

- **高活跃度**：过去24小时内，共有20个（Issue + PR）讨论或贡献被更新，显示出强大的社区参与度。
- **安全与稳定性是核心**：今日重点修复了两个安全问题（SSRF绕过、未处理的panic风险）并合并了数个提升代码健壮性的PR，项目正在积极修补潜在漏洞。
- **关键遗留问题待解决**：引入了 `Agent Collaboration Bus` 这一重大功能的PR（#2937）已处于待合并状态逾两周，或将成为近期版本的重点。
- **版本迭代**：发布了一个自动化 nightly 构建版本，持续集成和交付流程正常运转。

### 2. 版本发布

- **`nightly` 频道**
    - **版本**: `v0.2.9-nightly.20260611.d955d5bb`
    - **链接**: [v0.2.9-nightly.20260611.d955d5bb](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260611.d955d5bb)
    - **说明**: 这是一个自动化构建版本，用于集成最新的代码变更。虽然是nightly版本，未被标记为稳定版，但通常包含了最新的bug修复和小型功能改进。
    - **变更内容**: 主要包含来自 `main` 分支的最新提交，具体变更可参阅 [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main) 的比较日志。

### 3. 项目进展

今日共有 **6 个 Pull Request** 被合并或关闭，项目在以下方面取得实质进展：

- **关键Bug修复**：
    - **`[CLOSED] fix os.Root api on windows issue (#3089)`**: **这是今日最重要的修复之一**。修复了长期存在的 Issue #2472，解决了 `list_dir` 等文件系统工具在Windows平台上因路径分隔符不匹配而报错的问题，显著提升了项目的跨平台兼容性。
    - **`[CLOSED] fix(tools): block 198.18.0.0/15 in SSRF guard (#3085)`**: 针对安全问题 Issue #3077 的修复。在 `web_fetch` 工具的SSRF防护中，新增了对RFC 2544定义的专用地址段 `198.18.0.0/15` 的阻拦，封堵了一个潜在的安全绕过漏洞。
- **代码质量与健壮性提升**：
    - **`[CLOSED] fix: check strconv.Atoi and json.Unmarshal errors (#3043)`**: 修复了代码中两处因忽略错误返回值导致的潜在静默失败问题，增强了代码的可靠性和可调试性。

**总结**: 今日项目进展主要集中在解决关键平台兼容性问题、修补安全漏洞以及提升代码的整体健壮性。这些合并动作增强了PicoClaw的基础稳定性和安全性，向着更成熟、更可靠的版本迈进。

### 4. 社区热点

- **PR #2937: `[stale] Feat/agent collaboration`** (待合并)
    - **链接**: [PR #2937](https://github.com/sipeed/picoclaw/pull/2937)
    - **分析**: 该PR提议为PicoClaw增加一个“Agent协作总线”功能，允许内部代理进行结构化的通信和协作。这是一个重大的架构改进提案，但自5月24日以来已处于开放状态超过两周，被标记为 `stale`。这反映了社区和核心团队对于引入此重大功能持谨慎态度，正在进行深入的代码审查和设计讨论。该PR一旦合并，将极大地拓展PicoClaw在多智能体协作领域的应用潜力。

- **Issue #3094: `[Bug] 异步子代理(spawn)任务完成时，ForUser字段被同时用于直接推送和主代理汇总...`** (新开)
    - **链接**: [Issue #3094](https://github.com/sipeed/picoclaw/pull/3094)
    - **分析**: 该issue报告了使用 `spawn` 工具时，在飞书/Telegram等IM通道上会出现消息重复的问题。这是对核心用户体验的直接Bug反馈，预计会引起使用多Agent协作功能的用户高度关注，开发者可能会在近期快速响应。

### 5. Bug 与稳定性

以下为今日报告的主要Bug，按严重程度排列：

| 严重程度 | Issue/PR | 问题描述 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **高** | `#3077` | **SSRF绕过漏洞**：`web_fetch`的SSRF防护未能拦截专用IPv4地址段 `198.18.0.0/15`。 | **已关闭** | 已通过PR #3085修复 |
| **高** | `#2472` | **Windows平台兼容性崩溃**：文件系统工具 `list_dir` 在Windows上因路径分隔符问题返回 `invalid argument`。 | **已关闭** | 已通过PR #3089修复 |
| **中** | `#3094` | **消息重复**：`spawn` 异步子代理任务完成时，导致IM通道收到两条相同的消息。 | **新开，活跃** | 尚无修复PR |
| **低** | `#3090` | **UI兼容性问题**：PicoClaw Panel在iOS 16.4以下的Safari浏览器上无法工作。 | **新开，活跃** | 暂无修复PR |

### 6. 功能请求与路线图信号

- **Issue #3093 `[Feature] I need SimpleX or tox`** (新开)
    - **链接**: [Issue #3093](https://github.com/sipeed/picoclaw/pull/3093)
    - **分析**: 用户明确提出了对端到端加密通信协议 **SimpleX** 和 **Tox** 的支持需求。这表明社区对**隐私和去中心化通讯**的兴趣在增加。虽然该项目尚未被纳入官方路线图，但结合已有的多通道支持，此请求是一个值得关注的社区信号。

- **PR #2937 `Feat/agent collaboration`** (待合并)
    - **链接**: [PR #2937](https://github.com/sipeed/picoclaw/pull/2937)
    - **分析**: 尽管目前处于 `stale` 状态，但其“Agent协作”的理念代表了智能体框架的未来方向。如果此PR被成功合并，将可能成为v0.3.0或更高版本的核心特性之一，并可能会催生更多关于子代理管理的功能请求（如Issue #3094所反映的问题）。

### 7. 用户反馈摘要

- **关于Windows兼容性（Issue #2472）**：用户指出 `list_dir` 工具在Windows上完全无法工作，这直接影响了项目在Windows平台的可用性。多位开发者在旧Issue中提及此问题，凸显了跨平台稳定性的痛点。**（已修复）**
- **关于配置UI（PR #3067）**：用户反馈“运行时会话隔离范围（DmScope）”配置项在UI上修改后无法成功保存，这损害了用户对配置系统的信任。这种“看起来能改但实际没改”的交互体验比较影响满意度。
- **关于模型参数兼容性（PR #2948, #2951）**：用户在使用较新的AI模型（如 Claude Opus 4, OpenAI 新搜索接口）时，遇到了因发送了已弃用或不支持的参数（如 `temperature`, `web_search_preview`）而导致的400错误。这反映出PicoClaw在新模型适配方面需要更快的响应速度以匹配上游API的变化。

### 8. 待处理积压

以下为长期未响应或未解决的重要项目，建议维护团队关注：

- **`[OPEN] [stale] Feat/agent collaboration (#2937)`**
    - **链接**: [PR #2937](https://github.com/sipeed/picoclaw/pull/2937)
    - **分析**: 这是当前最重量级的PR，提出了全新的内部代理协作架构。由于涉及核心架构变更，评审周期长是合理的。建议维护者尽快给出明确反馈，告知作者是否需要补充测试或进行重大调整，避免宝贵贡献被完全搁置。

- **`[OPEN] [stale] [BUG] list_dir returns "invalid argument" on Windows due to path separator mismatch with os.Root (#2472)`**
    - **分析**: 虽然该Issue已有关联的Fix PR（#3089）被合并，但Issue本身尚未被关闭。建议维护者**关闭此Issue**，以确保待办事项列表的清晰，并让受影响的用户明确知道问题已被解决。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-11

## 1. 今日速览
项目今日活跃度极高，社区贡献呈井喷态势，共有 **12 个 Pull Request** 处于活跃状态（其中 4 个已合入/关闭，8 个待处理）。核心进展体现在“Skills”生态系统的快速扩张——Guardrails、Web 搜索、工具调用预览等多项新技能同日提交，以及部署稳定性修复（环境变量加载、容器网络隔离 Bug 被迅速定位）。昨日产生 2 个新 Issue，其中 #2731 披露的“Egress 隔离阻断宿主机服务”问题已被列为严重缺陷，关联 PR #2730 已提交修复。项目整体贡献活跃度极高，但审查积压略有上升。

---

## 2. 版本发布
本日无新版本发布。

---

## 3. 项目进展
今日合并/关闭的 PR 展示了项目在工具化和文档层面的稳步推进：

- **卸载脚本合并（PR #2719）**：由 `amit-shafnir` 贡献的 `uninstall.sh` 正式合入主分支。支持确认提示、Dry-run 及 Agent 清理，大幅降低了用户的卸载和重装成本。
- **文档体系建设（PR #2721）**：`gavrielc` 提交的自定义入门文档（`docs/customizing.md`、Skills 模型等）被合并，为社区贡献标准提供了明确指引。
- **基础架构清理（PR #3）**：早期关于容器间安全通信（IPC）的架构 PR 被正式关闭，标志着该特性已通过其他机制完成或被替代方案覆盖。
- **误操作关闭（PR #2724）**：提交者误将 PR 推送到错误仓库后立即关闭，无实质内容。

**今日 4 个 PR 的合入意味着项目在工具化、文档化和遗留架构清理上取得了实质性进展，为后续社区贡献铺平了道路。**

---

## 4. 社区热点

### 🤖 Issue #1690：多运行时 Agent SDK 抽象（👍 3，评论 6）
社区核心用户 `chiptoe-svg` 提出的将 Claude、Codex、本地模型等不同 SDK 作为“运行时”（Runtime）以 Skills 形式接入的议题持续发酵。该议题已开放 2 个月，6 条深入评论反映了用户希望 NanoClaw **成为 Agent 编排基础设施而非单一 Agent 产品**的强烈愿景。
🔗 [nanocoai/nanoclaw Issue #1690](nanocoai/nanoclaw Issue #1690)

### 🐞 操作安全性 Bug 连环案（Issue #2731, PR #2730, PR #2728）
用户 `sturdy4days` 今日密集提交了多项与部署和安全相关的缺陷。其中 #2731（Egress 阻断 host.docker.internal）和 #2730（环境变量不生效）紧密关联，对于依赖本地私有模型（Ollama）的用户是致命问题。该用户同时在修复 Telegram 文档和配对逻辑，成为今日最活跃的贡献者。
🔗 [Issue #2731](nanocoai/nanoclaw Issue #2731) | [PR #2730](nanocoai/nanoclaw PR #2730)

### 🎨 Skills 生态集体井喷
今日有多个高质量 Skill PR 提交或处于活跃更新中：
- `amit-shafnir`：输入/输出护栏技能（#2726）
- `robbyczgw-cla`：Web 搜索技能（#2725）、工具调用预览技能（#2211 持续更新）
- `manojp99`：容器日志持久化（#2727）

这表明 **Skills 模型已成功激发了社区的自发贡献欲**，但同时也对官方的 Review 效率提出了挑战。

---

## 5. Bug 与稳定性

### [严重] Egress 隔离阻断内部网络（Issue #2731）
**问题**：当设置 `NANOCLAW_EGRESS_LOCKDOWN=true` 时，Agent 容器完全无法通过 `host.docker.internal` 访问宿主机上的服务（如 Ollama、本地代理等）。这使得“本地模型 + 隔离模式”的部署方案事实上不可用。
**状态**：暂无直接修复，但关联 PR #2730 正在修复环境变量加载问题，此为前置条件。
🔗 [nanocoai/nanoclaw Issue #2731](nanocoai/nanoclaw Issue #2731)

### [高] 环境变量加载失败（PR #2730）
**问题**：用户通过 `.env` 配置的 `NANOCLAW_*` 变量在 `launchd`/`systemd` 环境下无法注入 `process.env`，导致 Egress 规则即使配置了也形同虚设。
**状态**：`sturdy4days` **已提交修复 PR**，等待 Review。
🔗 [nanocoai/nanoclaw PR #2730](nanocoai/nanoclaw PR #2730)

### [高] Telegram 配对逻辑缺陷（PR #2728）
**问题**：使用 `--intent wire-to` 进行群组配对时，虽然提示成功，但未创建 `messaging_group_agents` 映射记录，导致 Agent 实际上无法在 Telegram 群中工作。
**状态**：`sturdy4days` **已提交修复 PR**，等待 Review。
🔗 [nanocoai/nanoclaw PR #2728](nanocoai/nanoclaw PR #2728)

### [中] CLI 审批上下文丢失（PR #2611）
**问题**：需要管理员审批的 `ncl` 命令在重放（replay）时丢失原始调用方上下文，影响审计追踪的完整性。
**状态**：`Hinotoi-agent` 已提交修复 PR（带安全标签），已更新至最新。
🔗 [nanocoai/nanoclaw PR #2611](nanocoai/nanoclaw PR #2611)

---

## 6. 功能请求与路线图信号

### 安全增强成为开发主线
`amit-shafnir` 提交的 **#2726（Guardrails 技能）** 为 NanoClaw 带来了原生的安全过滤能力（prompt 注入检测、凭据泄露拦截），支持 `block`/`flag` 动作和宿主端隔离审计。结合已有的 Egress Lockdown，**零信任 Agent 安全**已成为当前版本迭代的核心关键词之一。
🔗 [nanocoai/nanoclaw PR #2726](nanocoai/nanoclaw PR #2726)

### Agent“可观测性”呼声高涨
- **#2727（容器日志持久化）**：`manojp99` 提出将 Agent 容器的 stdout/stderr 持久化到磁盘，解决当前调试信息完全丢失的问题。
- **#2211（工具调用实时预览）**：在聊天界面实时显示 Agent 执行工具调用的情况。
以上功能反映用户不仅需要 Agent 运行，还需要 **“看见”Agent 运行的过程**，这是项目从实验性走向生产化的重要信号。
🔗 [PR #2727](nanocoai/nanoclaw PR #2727) | [PR #2211](nanocoai/nanoclaw PR #2211)

### 轻量不依赖 MCP 的集成策略
`robbyczgw-cla` 在 #2725（Web 搜索技能）中明确强调引擎无需 LLM 合成、**不依赖 MCP**，二进制一致。这暗示社区中存在对轻量级、直连工具集的偏好，而非全盘拥抱 MCP 协议。

### 核心架构讨论：多运行时抽象（Issue #1690）
用户 `chiptoe-svg` 在 #1690 中的架构提案虽未被官方采纳，但其高热度暗示这可能是 NanoClaw 未来从“单一 Agent 框架”演进为“Agent 操作系统”的关键路线选择。

---

## 7. 用户反馈摘要

### “新手上路”较坎坷
用户 `sturdy4days` 在一天内提交了 4 个相关的 Issue/PR，暴露了三个层面问题：
1. **文档与实际脱节**（#2729）：Telegram 文档中的状态块名称与代码实现不匹配，Advisor 固定版本号也有误。
2. **配置传播链断裂**（#2730）：.env → process.env 的链条在非终端环境下断裂。
3. **无错误反馈**（#2728）：操作提示成功但功能未生效，零错误提示。
当前版本对采用 **“容器部署 + 外部服务连接”** 模式的用户存在较高配置门槛。

### 核心用户高度投入
`robbyczgw-cla` 将其 PR #2211 从分支合并模式重构为 Skills 标准以符合项目规范；`amit-shafnir` 一次性提交了独立、完整的 Guardrails 技能。这些高级用户希望官方能加快 Review 节奏，避免分支长期分歧。

### 对“开箱即用”的期待
从 #2731 和 #2728 的反馈措辞看，用户对“配置提示成功但功能不工作”的情况容忍度极低。项目在**配置验证**和**错误反馈**上还有明显提升空间。

---

## 8. 待处理积压

### ⚠️ PR #2211【工具调用预览技能】（创建于 2026-05-03，更新于 2026-06-10）
该 PR 由 `robbyczgw-cla` 提交，期间已按项目规范从分支合并模式重写为符合 Skills 标准的独立技能。当前已 **超过 1 个月无官方 Review**。这是一个极具演示价值的技能，长期搁置容易打击核心贡献者的积极性。
🔗 [nanocoai/nanoclaw PR #2211](nanocoai/nanoclaw PR #2211)

### 📌 Issue #1690【多运行时抽象】（创建于 2026-04-07）
获得 3 个 👍 和 6 条深入讨论。这是一个决定项目架构走向的重大议题。建议维护者标记 `roadmap` 或 `discussion` 标签，并给出初步的官方态度，以引导社区预期，避免社区自行分支开发导致生态分裂。
🔗 [nanocoai/nanoclaw Issue #1690](nanocoai/nanoclaw Issue #1690)

### 📥 新提交的高质量 PR 需要排期
今日提交的 PR #2725（Web 搜索）、PR #2726（Guardrails 技能）和 PR #2727（日志持久化）逻辑完整、功能独立且无架构冲突。建议维护者优先安排 Review，以在这个贡献爆发期向社区传递强烈正向信号。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 (2026-06-11)

## 1. 今日速览
过去 24 小时内，项目未收到新 Issue 或发布新版本，但贡献者提交了 **4 个 Pull Requests**，均为待合并状态。这些 PR 集中修复了 agent 输出误污染、队列模式不可配置、cron 归属错误以及 gateway 测试资源泄漏等问题，体现出项目在稳定性和可配置性上的持续迭代。社区互动（评论、点赞）为零，整体活跃度偏低，但代码产出质量扎实。

## 2. 版本发布
无。

## 3. 项目进展
今日无 PR 被合并，但有 4 个修复性 PR 处于待合并状态，一旦合入将在以下方面推进项目：

- **Agent 输出可靠性**（[#951](https://github.com/nullclaw/nullclaw/pull/951)）：阻止 agent 子进程失败时将初始化日志（内存计划、MCP 注册等）误当作正常响应发送到 channel，避免信息污染。
- **配置灵活性**（[#949](https://github.com/nullclaw/nullclaw/pull/949)）：允许用户通过 `config.json` 的 `agent.default_queue_mode` 设置新会话的默认队列模式，并将相关枚举抽离为单一数据源，降低维护成本。
- **Cron 投递准确性**（[#948](https://github.com/nullclaw/nullclaw/pull/948)）：确保 `nullclaw cron once-agent` 子进程能正确继承触发渠道/账户的元数据，使 `agent_start` 事件的归属与实际投递渠道匹配。
- **测试健壮性**（[#950](https://github.com/nullclaw/nullclaw/pull/950)）：将 gateway 端口探测提前至资源分配之前，避免因端口占用导致的分配泄漏，增强测试环境下的隔离性。

## 4. 社区热点
今日所有 PR 均未产生评论或反应，社区讨论处于静默状态。从内容看，[#949](https://github.com/nullclaw/nullclaw/pull/949) 涉及用户可感知的配置项，可能最易引发后续讨论；[#951](https://github.com/nullclaw/nullclaw/pull/951) 则直接影响 agent 输出体验，修复价值较高。

## 5. Bug 与稳定性
全部 4 个 PR 均直接关联 Bug 或稳定性问题，按影响程度排列：

| 严重程度 | PR | 问题描述 | 已有修复 PR |
|----------|----|---------|-------------|
| **高** | [#951](https://github.com/nullclaw/nullclaw/pull/951) | Agent 失败时误将 stderr 中的初始化日志当作 agent 响应发布到 channel，造成信息混乱 | ✅ 是 |
| **高** | [#948](https://github.com/nullclaw/nullclaw/pull/948) | Cron agent 启动事件无法正确关联触发渠道/账户，影响任务归因 | ✅ 是 |
| **中** | [#950](https://github.com/nullclaw/nullclaw/pull/950) | Gateway 因 AddressInUse 失败时，已分配的 Config、SessionManager 等未被完全释放，导致测试资源泄漏 | ✅ 是 |
| **低** | [#949](https://github.com/nullclaw/nullclaw/pull/949) | 新会话队列模式无法通过配置更改，默认行为不灵活（虽不算 bug，但属配置缺失引发的体验缺陷） | ✅ 是 |

## 6. 功能请求与路线图信号
今日无用户提交的功能需求。从已提交的 PR 看：
- [#949](https://github.com/nullclaw/nullclaw/pull/949) 将 queueMode 纳入 `config.json`，表明项目正逐步暴露更多运行时参数给用户，此模式可能扩展到其他 agent 默认行为；
- 其余 PR 均为修复，未涉及新功能或路线图变动。

目前无明确的下一版本路线图信号。

## 7. 用户反馈摘要
今日无 Issues 或 PR 评论产生，因此无法提炼直接用户反馈。从 PR 修复内容反推，用户可能遇到以下痛点：Agent 输出被无关日志干扰、cron 投递归属不明确、测试环境因端口冲突反复崩溃，这些均在本次 PR 中得到解决。

## 8. 待处理积压
今日无长期未处理的 Issue 或 PR，但应注意 **4 个待合并 PR** 的审核进度。尤其是 [#951](https://github.com/nullclaw/nullclaw/pull/951) 和 [#948](https://github.com/nullclaw/nullclaw/pull/948) 修复了用户可见的错误，建议优先 review 并合并，以避免贡献者等待时间过长导致动力下降。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw 项目动态日报 · 2026‑06‑11**

---

### 1. 今日速览

过去 24 小时项目保持高度活跃：收到 50 条 Issue 更新（新开/活跃 35，关闭 15）和 50 条 PR 更新（待合并 28，合并/关闭 22）。社区注意力集中在 **Reborn WebUI v2** 的稳定性与体验打磨上，大量 Bug 报告与修复 PR 同步推进。**crates.io 发布缺口**（最新只有 0.24.0，而 GitHub 已打到 0.27.0）成为社区反馈最强烈的问题，但尚无新版本发布。整体来看，项目正处于 Reborn 功能密集落地与质量加固并行阶段，活跃度极高。

---

### 2. 版本发布

**无**（最近一次发布为 2026‑03‑31 的 0.24.0）。

---

### 3. 项目进展

今日合并/关闭了 **8 项重要 PR**，集中解决了 Reborn WebUI v2 中与认证、自动化、模型配置、文档化相关的关键缺口：

| PR | 要点 | 影响 |
|----|------|------|
| [#4746](https://github.com/nearai/ironclaw/pull/4746) | **Auth‑gate resume**：OAuth 完成后自动重新调度原 capability 调用，解决 Google Calendar 等场景“再次询问才能拿到数据”的问题 | Reborn WebUI 认证交互闭环 |
| [#4745](https://github.com/nearai/ironclaw/pull/4745) | **Automations panel 重构**：面板触发列表从 capability 路由改为直接查询 `TriggerRepository`，消除冗余的 agent‑loop 依赖 | 降低面板读取延迟与复杂度 |
| [#4743](https://github.com/nearai/ironclaw/pull/4743) | **NEAR 上下文超限分类**：将 NEAR/Anthropic 返回的 `prompt is too long` 400 错误正确归类为 `ContextLengthExceeded`，并解析 token 计数 | 改善错误诊断与模型选择 |
| [#4742](https://github.com/nearai/ironclaw/pull/4742) | **手工令牌运行时凭据选择**：`ManualToken` 模式贯穿授权义务、宿主请求、WASM 重编排等全链路，支持手工令牌满足运行时请求 | 完善非 OAuth 场景的凭据管理 |
| [#4730](https://github.com/nearai/ironclaw/pull/4730) | **Slack DM 事件推送端到端**：用户绑定 Slack 后自动获得 DM 投递目标，触发器运行结果可直接通过 Slack 消息送达 | 个人自动化通知闭环完成 |
| [#4717](https://github.com/nearai/ironclaw/pull/4717) | **始终批准（always allow）能力恢复**：为 WebUI v2 审批弹窗重新加入“始终允许”选项，持久化批准策略 | 提升高频工具重复审批体验 |
| [#4652](https://github.com/nearai/ironclaw/pull/4652) | **文档 + 启动脚本**：新增 `docs/reborn-binary.md` 和 `scripts/run-reborn-webui.sh`，简化本地 Reborn WebUI 启动与测试流程 | 降低新用户本地部署门槛 |
| [#4739](https://github.com/nearai/ironclaw/pull/4739) | **Railway QA 启用 Slack**：在 Docker 配置中集成 Slack，便于 QA 环境验证自动化推送 | 内建质量保障 |

以上合并使 Reborn 在 **认证连续性、自动化交付、错误处理、开发者体验** 四个维度上明显前进。

---

### 4. 社区热点

#### 最热 Issue：crates.io 发布缺口 [#3259](https://github.com/nearai/ironclaw/issues/3259)（14 条评论）
- **诉求**：GitHub 已打标签至 `0.27.0`，但 crates.io 最高仍是 `0.24.0`。下游（如 wasmtime 28.x CVE）被迫锁定旧版本，无法获得新功能与安全更新。
- **分析**：该 Issue 自 5 月 5 日以来持续收到 +1 和追问，是目前社区最迫切的阻塞点。**尚无官方回复或 PR 指示发布时间**，风险累积。

#### 高关注 Epic：配置即代码 [#3036](https://github.com/nearai/ironclaw/issues/3036)（6 个 👍，6 条评论）
- **诉求**：用户希望用声明式配置（tenant blueprints / harnesses）代替手工编辑 `.env`、`settings JSON` 等碎片化方式，要求有 schema、diff、审计与版本控制。
- **分析**：该 epic 被标记为 `reborn`，表明是 Reborn 体系的待规划功能，但尚未见到对应 PR 进入实现。

#### 讨论中的 PR：release PR [#3708](https://github.com/nearai/ironclaw/pull/3708)（持续更新至 2026‑06‑11）
- `ironclaw_common` 和 `ironclaw_skills` 均有 breaking changes，`ironclaw` 升到 0.29.1。该 PR 自 5 月 16 日打开，至今未合并，反映出**发布流程可能阻塞于 breaking change 的评审**。

---

### 5. Bug 与稳定性

今日报告的 Bug 集中在 **Reborn WebUI v2 的配置保存、认证、UI 交互与工具调用**，部分已附带修复 PR。严重程度排列如下：

| 严重度 | Issue | 摘要 | 状态 |
|--------|-------|------|------|
| 🔴 高 | [#4673](https://github.com/nearai/ironclaw/issues/4673) | NEAR AI provider 配置 Test connection 成功，但点击 Save 静默失败，重新进入仍显示未设置 | **已修复**（PR [#4731](https://github.com/nearai/ironclaw/pull/4731) 关闭 #4673） |
| 🔴 高 | [#4703](https://github.com/nearai/ironclaw/issues/4703) | NEAR AI provider 设置成功后，Conversation 仍无法使用该 provider | 开放中 |
| 🔴 高 | [#4729](https://github.com/nearai/ironclaw/issues/4729) | 本地/桌面构建下 NEAR AI 登录失败：`private.near.ai` 拒绝非 `private.near.ai` 的 `frontend_callback` | 开放中 |
| 🟡 中 | [#4741](https://github.com/nearai/ironclaw/issues/4741) | 本地密钥文件损坏或低熵时，错误消息为不易诊断的 `Invalid master key`，无修复提示 | 开放中 |
| 🟡 中 | [#4642](https://github.com/nearai/ironclaw/issues/4642) | 严格模式 LLM 提供者为未设可选参数发送 `null`，capability‑port 校验拒绝该调用，影响多数第一方工具 | **已关闭**（有修复） |
| 🟡 中 | [#4704](https://github.com/nearai/ironclaw/issues/4704) | `builtin.http` 工具在 `invalid_input` 后进入无限审批循环，无有效错误信息 | 开放中 |
| 🟡 中 | [#4701](https://github.com/nearai/ironclaw/issues/4701) | 审批弹窗对 `builtin.http` 请求显示的信息过少，用户无法判断批准的是什么请求 | 开放中 |
| ⚪ 低 | [#4748](https://github.com/nearai/ironclaw/issues/4748) | 代码块内 Wrap/No Wrap 切换无视觉效果 | 开放中 |
| ⚪ 低 | [#4733](https://github.com/nearai/ironclaw/issues/4733) | 点击对话中的链接（PR/Issue/差异链接）会离开当前对话，中断工作流 | 开放中 |
| ⚪ 低 | [#4708](https://github.com/nearai/ironclaw/issues/4708) | 代码块无语法高亮 | 开放中 |
| ⚪ 低 | [#4707](https://github.com/nearai/ironclaw/issues/4707) | WebUI 字体过小，阅读不舒适 | 开放中 |
| ⚪ 低 | [#4724](https://github.com/nearai/ironclaw/issues/4724) | 新对话中未发送的草稿离开页面后丢失 | 开放中 |
| ⚪ 低 | [#4725](https://github.com/nearai/ironclaw/issues/4725) | 助理响应中（Working）时 composer 仍显示交互状态，但实际不可用 | 开放中 |
| ⚪ 低 | [#4706](https://github.com/nearai/ironclaw/issues/4706) | 授权流程（NEAR AI SSO、ChatGPT 订阅）在失败/取消后不能恢复，卡死在半认证状态 | 开放中 |

**观察**：今日关闭的 15 个 Issue 中包含 #4642、#4734（avatar IC 显示）以及 #4594 / #3615 等 audit 类任务，但核心配置与认证类 Bug 仍有大量未闭合。#4673 的修复 PR [#4731](https://github.com/nearai/ironclaw/pull/4731) 尚为 `OPEN`，预计明天合并后该问题可关闭。

---

### 6. 功能请求与路线图信号

| Issue / PR | 请求 | 分析 |
|------------|------|------|
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | **Configuration‑as‑Code**：tenant blueprints + use‑case harnesses，声明式管理所有配置 | Epic，标记为 `reborn`，可预期纳入 Reborn 未来路线图 |
| [#3283](https://github.com/nearai/ironclaw/issues/3283) | **迁移 OpenAI‑compatible API** 到 Reborn 产品模型（`/v1/chat` / `/v1/responses`） | 已标记 parent #3031，说明属于 Reborn API 重构核心部分，可能伴随下一发布 |
| [#3259](https://github.com/nearai/ironclaw/issues/3259) | **发布 0.25.0–0.27.0 到 crates.io** | 本质上是一个发布操作请求，但被 blocked（如 PR [#3708](https://github.com/nearai/ironclaw/pull/3708) 未合并），目前无进展 |
| [#4632](https://github.com/nearai/ironclaw/issues/4632) | **Reborn WebUI v2 端到端浏览器测试** | 配套有已关闭的 [#4604](https://github.com/nearai/ironclaw/issues/4604) 和待合并的 [#4713](https://github.com/nearai/ironclaw/pull/4713)，质量基础设施在建设中 |
| [#4700](https://github.com/nearai/ironclaw/issues/4700) | **配置 NEAR AI 凭据后自动启用 NEAR AI MCP**，无需手动额外设置 | 强用户需求，逻辑清晰，可能随配置模块重构一起实现 |
| [#4747](https://github.com/nearai/ironclaw/issues/4747) | **agent_loop 统一挂起‑恢复记录**，将重放负载移出 checkpointed 状态 | 架构改进，今日新开，源于 [#4746](https://github.com/nearai/ironclaw/pull/4746) 的 review 发现，预计短期会有跟进 PR |

---

### 7. 用户反馈摘要

从今日活跃的评论与 Issue 描述中提炼以下真实痛点：

- **“无法获得新版功能”**（#3259）：社区重复抱怨 crates.io 版本落后，无法使用 0.25.0+ 的改进和 CVE 修复，直接阻碍了下游项目升级。这是一致的、高音量反馈。
- **“配置保存后消失，不知是否生效”**（#4673）：用户严格按照步骤添加 API key 并测试成功，但保存后回到欢迎页仍显示未设置。这种静默失败严重损害信任。
- **“包装切换没用，感觉像占位符”**（#4748）：代码块中的 Wrap/No Wrap 按钮无效果，用户怀疑功能还未实现。
- **“链接直接跳走，对话中断”**（#4733）：用户希望外部链接在新标签打开，以保持聊天上下文。当前行为对工作流干扰大。
- **“认证失败后无法恢复，只能刷新”**（#4706）：SSO 或订阅授权如果取消或出错，不能从原流程恢复，用户不得不重新开始，体验割裂。
- **“审批弹窗信息太少，我根本不知道要批准什么”**（#4701）：`builtin.http` 调用只显示“Approve / Deny”，用户无法确认工具将请求哪个 URL 或参数，感到不安全。
- **“报错信息不帮助解决问题”**（#4741、#4683）：密钥文件损坏时只显示 “Invalid master key”，而没有指出文件路径或熵要求；无效模型配置时报“driver unavailable”而不是具体原因，使用户无从着手。

这些反馈集中于 **可用性、信息透明度和流程鲁棒性**，是 Reborn WebUI 从 Beta 走向生产环境必须优先解决的问题。

---

### 8. 待处理积压

以下重要工作处于长期未合并/未回应状态，需维护者关注：

| 项目 | 标识 | 搁置时长 | 状态说明 |
|------|------|----------|----------|
| **crates.io 发布** | [#3259](https://github.com/nearai/ironclaw/issues/3259) | 自 2026‑05‑05 | 14 评论，0 官方回复；阻塞下游。相关 PR [#3708](https://github.com/nearai/ironclaw/pull/3708) 自 5月16日 搁置，包含 breaking changes 需评审 |
| **Configuration‑as‑Code Epic** | [#3036](https://github.com/nearai/ironclaw/issues/3036) | 自 2026‑04‑28 | 6 评论，1 👍；标记 reborn 但尚无实现 PR，需路线图排期 |
| **OpenAI API 迁移** | [#3283](https://github.com/nearai/ironclaw/issues/3283) | 自 2026‑05‑06 | 3 评论，依赖 #3031 等；属于 Reborn 迁移核心但进度不明确 |
| **正式发布 PR (release)** | [#3708](https://github.com/nearai/ironclaw/pull/3708) | 自 2026‑05‑16 | 持续更新但仍未合并；包含 `ironclaw_common` 和 `ironclaw_skills` breaking changes，需团队决策发布策略 |

**建议**：#3259 与 #3708 紧密关联，应尽快推动发布流程，解除下游阻塞；同时为 #3036 配置声明式功能划定 Milestone，避免社区长期等待路线图细节。

---

**数据来源**：[GitHub nearai/ironclaw](https://github.com/nearai/ironclaw) · 采集时间 2026-06-11 12:00 UTC

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 LobsterAI 项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-11

**数据来源：** GitHub (netease-youdao/LobsterAI)

## 1. 今日速览

项目今日迎来爆发式更新，活跃度**极高**。过去 24 小时内，共有 **24 个 Pull Request 被合并/关闭**，并发布了 **1 个新版本**。

今日活动的核心脉络清晰：一方面，备受瞩目的 **“Computer Use” MVP** 成功合入主分支，标志着 LobsterAI 正式迈入桌面自动化代理时代；另一方面，团队集中清偿了自 4 月以来的大量积压 PR，涉及定时任务、技能管理、会话控制等多个模块的基础能力完善。Issue 板块今日无新增，表明当前开发迭代主要集中在对社区现有贡献的吸收和内部功能的推进上。

## 2. 版本发布

项目今日发布了 **LobsterAI 2026.6.10** 版本。

- **主要更新内容：**
    - **数据迁移：** 新增了用户数据备份与恢复功能，为用户在迁移设备或重装系统时提供了安全保障。
    - **本地回调登录：** 引入了本地回调鉴权流程，提升了登录的安全性和灵活性。
    - **设置面板：** 将 OpenClaw 相关的高级配置项暴露至设置界面，方便用户自定义。
- **迁移建议：** 建议计划升级的用户，在升级前利用新增的备份功能对当前数据进行备份，以确保数据零丢失。

## 3. 项目进展

今日项目通过大规模合并 PR，在功能创新与基建补全上同步取得了显著进展：

- **🎯 里程碑功能：计算机使用（Computer Use）**
    - **PR #2143** 成功合并。该项目为 Windows x64 平台内置了完整的“计算机使用”工具包，包含技能市场元数据、运行时解析安装器及 MCP 服务器桥接。这允许 AI Agent 直接操控桌面应用和窗口，是项目走向全能型助手的关键一跃。

- **🧠 核心体验增强：长会话上下文连续性**
    - **PR #2145** 合入。针对 OpenClaw 压缩聊天历史后 Agent 上下文丢失的问题，通过增加会话作用域状态和轻量级工作空间恢复机制，极大提升了长期连续任务的可靠性。
    - **PR #1499** 合入。引入了自动会话裁剪功能，防止长对话因超出模型上下文窗口而报错。

- **🪟 Windows 平台夯实**
    - **PR #2142** 修复了 NSIS 安装程序潜在的破坏性初始化问题，并对引擎加载页面进行了重新设计，提升了首次启动的稳定性。
    - **PR #2141** 修复了 Windows 版本的应用内更新机制。
    - **PR #1497** 新增了 Windows 关闭按钮行为配置（最小化托盘/完全退出）。

- **🛠️ 技能与定时任务体系完善**
    - **修复：** 确保禁用技能后不再被注入上下文（PR #1485, #1501）。
    - **增强：** 定时任务新增“测试任务”按钮（#1486）、macOS 本地通知渠道（#1489），并修复了编辑通知渠道后 UI 未及时刷新的 Bug（#1490）。

- **🎨 UI 与交互升级**
    - **PR #2139** 优化了 Markdown 渲染、代码块语法高亮及模型选择器的样式。
    - **PR #1503** 为 Agent 引导文件编辑器引入了富文本 Markdown 编辑器，取代了原先的纯文本框。

- **🧹 技术债务清理**
    - 集中合并了来自 Dependabot 及社区提交的多个积压 PR，包括 CI/CD 依赖更新（#1491, #1492, #1493）以及其他功能增强。

## 4. 社区热点

今日无新 Issue 产生，公开评论区较为安静。社区热度主要体现在已合并 PR 所代表的用户核心诉求上：

- **焦点功能：** **PR #2143 (Computer Use MVP)**
    - **诉求分析：** 尽管缺少公开评论数据，但“计算机使用”能力是 AI Agent 领域当前最核心的探索方向。该 PR 的快速合并，反映了开发团队对该方向的坚定投入，也印证了社区对“AI 真正动手干活”的高期待。

- **长期诉求的回应：** 今日合并的多个“陈旧”PR（如会话裁剪、Windows 行为配置），印证了社区一直以来的反馈得到了积极采纳，开发者关系保持良性互动。

## 5. Bug 与稳定性

今日合并了多个关键修复，显著提升了项目整体稳定性。按严重程度排列如下：

- **🔴 严重**
    - **NSIS 安装器破坏问题** (PR #2142): 修复了 Windows 安装程序可能导致的系统初始化失败问题，直接影响用户首屏体验，已合并。

- **🟡 中等**
    - **禁用技能失效** (PR #1485, #1501): 修复了用户关闭技能后，该技能仍在后台被调用的问题，这是对用户意图控制的重大修复。
    - **定时任务渠道编辑 BUG** (PR #1490): 修复了用户修改通知渠道后页面显示未更新的 UI/数据不一致问题。

- **🟢 低危**
    - **Windows 更新问题** (PR #2141): 修复了应用内无法正常更新的逻辑。
    - **鉴权 Portal 回退 URL** (PR #2144): 更新配置以确保登录流程在不同环境下正常跳转。

## 6. 功能请求与路线图信号

结合今日合并的 PR，可以预见项目未来的演进方向：

- **优先级提升：下一代 Agent 能力**
    - 计算机使用（Computer Use）不仅是一个新功能，更是路线图的核心转向。下一阶段极有可能围绕该能力推出**自定义技能 SDK、跨平台支持、更丰富的预置市场包**。

- **已成熟模块：Scheduled Task 2.0**
    - 随着“测试按钮”、“通知渠道”等功能补齐，定时任务模块已基本成熟。未来可能向 **Workflow 自动化流** 演进。

- **用户个性化收敛**
    - 从 Markdown 编辑器到窗口行为配置，项目正从单纯的“对话工具”向“高度可定制的工作环境”发展。

## 7. 用户反馈摘要

由于今日无新 Issue 或公开评论产生，以下反馈摘要基于已合并 PR 所解决的痛点逆向推导：

- **用户痛点得到修复：** “关闭了技能，为什么对话里还能通过路由触发？” -> 已通过 PR #1485 / #1501 解决。
- **用户诉求得到满足：** “长对话一压缩就丢失上下文，需要频繁重启任务。” -> 已通过 PR #2145 / #1499 解决。
- **体验得到优化：** “我希望 AI 能直接操作我的电脑。” -> 已通过 PR #2143 实现。

## 8. 待处理积压

- **#1277 [OPEN] chore(deps-dev): bump the electron group across 1 directory with 2 updates**
    - **创建时间：** 2026-04-02 (已开启 **70 天**)
    - **风险等级：** 🔴 **极高**
    - **情况分析：** 该 PR 旨在将核心底层框架 **Electron** 从 v40 大幅升级至 v42。长期未合并意味着项目运行在过时的 Chromium 内核上，可能错过大量**安全更新**及 **API 兼容性绑定**。若该 PR 因 CI 失败而阻塞，建议维护者尽快手动调研并创建替代升级 PR，否则框架版本差距过大会导致未来升级成本剧增。
    - **链接：** [netease-youdao/LobsterAI PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)

---

**整体项目健康度评估：**

**🚀 加速冲刺期（优秀）**
项目正处于功能扩张与技术债务清偿并行的健康状态。Computer Use 的落地极具前瞻性，而大量修复 PR 的合入则稳固了底盘。主要风险点在于核心依赖（Electron）的长期滞库，建议维护团队尽快介入处理。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是基于 CoPaw 项目提供的 GitHub 数据生成的2026年6月11日项目动态日报。

---

### CoPaw 项目动态日报 | 2026-06-11

**数据周期：** 2026-06-10 - 2026-06-11
**数据来源：** AgentScope-AI/CoPaw (QwenPaw)

---

#### 1. 今日速览

项目今日极度活跃，共发布 2 个新版本，处理了大量 Issues（33条）和 PRs（49条）。**`v1.1.11` 版本的发布是今日焦点**，它引入了多项新功能，但同时也暴露了严重的 Windows 平台兼容性问题，导致紧急发布了修订版本。社区在积极反馈 Bug 的同时，也有多个重量级的架构性 PR（如 Runtime 2.0 和 Agent OS Driver）被提交，显示出项目正处于**功能快速迭代与架构升级并行**的关键阶段。整体健康度受 Bug 影响为“中等”，但开发响应速度极快。

#### 2. 版本发布

- **`v1.1.11`**：今日发布的主版本。
  - **新增功能**：引入了**Free Model OAuth**（零配置免费模型一键 OAuth 认证）、**Xiaomi MiMo Provider**（小米 MiMo Token 计划作为内置提供商）等新功能。
  - **破坏性变更**：未明确提及，但请注意其伴随的 Beta 版本特性。
  - **迁移注意**：从 Release Note 看，主要增加了新 Provider，常规升级应无大碍。但建议用户在升级后检查模型配置。

- **`v1.1.11-beta.3`**：紧跟主版本发布的 Beta 版本。
  - **新增功能**：主要特性包括**自我进化技能创建（self-evolving skill creation）**，这是一个值得关注的 AI 能力方向。
  - **其他**：移除了冗余的 CI 工作流。

- **紧急修复**：由于 `v1.1.11` 桌面版存在严重启动 Bug，团队已迅速发布修订版本 `v1.1.11.post1` (PR #5093) 进行修复。建议所有 Windows 桌面用户升级至此版本。

#### 3. 项目进展

今日项目在架构演进和功能修补上均有显著推进：

- **架构演进**：多个重量级 PR 被提交，标志着项目正迈向更高的抽象层次。
    - **`Runtime 2.0`**：PR [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) 提交了全新的模块化 Runtime 2.0 架构，旨在取代旧的 `Runner` + `stream_query` 执行路径，并以 `ToolCoordinator` 层强化工具调用生命周期控制。这是一个重要的重构信号。
    - **`Agent OS Driver`**：PR [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) 提出了统一的外部能力抽象层（Agent OS Driver），为未来轻松集成 MCP、A2A、ACP 等协议奠定了基础。
    - **治理与沙箱**：PR [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) 开启了关于治理和沙箱接口的讨论，关注 Agent 安全性。

- **功能开发**：
    - **数据插件**：PR [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) 的 `DataPaw` 数据分析插件正在开发中，内含 12 个 BI 技能。
    - **PRD 管理工具**：PR [#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902) 将 PRD 管理内建为工具，并提供了前端渲染器。

- **稳定性修复**：
    - **桌面端**：修复了桌面端端口随机分配导致用户设置丢失的问题（PR [#5051](https://github.com/agentscope-ai/QwenPaw/pull/5051)）。
    - **环境变量页面**：修复了鼠标悬停时滚动条闪烁的 UI 问题（PR [#4766](https://github.com/agentscope-ai/QwenPaw/pull/4766)）。
    - **安全设置**：修复了盾牌图标垂直未居中的 UI 问题（PR [#5094](https://github.com/agentscope-ai/QwenPaw/pull/5094), [#5097](https://github.com/agentscope-ai/QwenPaw/pull/5097)）。

#### 4. 社区热点

今日最受关注的讨论集中在 **Bug 反馈** 和 **重大架构变更** 上，反映了社区对稳定性和未来方向的同等关注。

- **#4727 [[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0](https://github.com/agentscope-ai/QwenPaw/issues/4727)**: 这个关于迁移到 AgentScope 2.0 的 Issue 获得了 8 条评论和 2 个赞，是今日讨论最热烈的话题之一。用户们显然对底层依赖的重大升级非常关注，讨论可能涉及迁移带来的影响和新特性。

- **#4878 [[Bug]: 定时任务结果无法推送到微信](https://github.com/agentscope-ai/QwenPaw/issues/4878)**: 该 Bug 报告非常详细，开发者已将根因定位在微信频道的 `to_handle_from_target` 函数。该问题严重影响了微信渠道用户的自动化体验，引发了 7 条评论，是典型的“严重影响体验”的热点。

- **#5064 [[Bug]: Agent 生成的定时任务无法正常触发](https://github.com/agentscope-ai/QwenPaw/issues/5064)**: 该问题直指 Agent 自主性的核心——生成的定时任务“不受控、不可编辑”。这触及了用户对 AI Agent 自主行为进行监督和控制的核心诉求。

**诉求分析**：社区热点清晰地表明，随着 Agent 功能（如定时任务）的复杂化，用户对**功能的可靠性**（任务能否被执行）、**可控性**（能否被修改/干预）和**渠道的连通性**（能否推送到微信）的要求变得极高。任何一环的失灵都会直接导致用户对 Agent 信任度的下降。

#### 5. Bug 与稳定性

今日报告的 Bug 主要围绕 **Windows 桌面端无法启动** 和 **定时任务失效** 这两大核心问题，严重程度很高。

- **严重：Windows 桌面端启动失败（已修复）**
    - **#5086 [[Bug]: OpenSSL 3.5 回归 bug 导致 Desktop 无法启动](https://github.com/agentscope-ai/QwenPaw/issues/5086)**: 根本原因是捆绑的 OpenSSL 3.5.7 在 Windows 上存在回归 Bug，导致 SSL 上下文创建失败。这是导致 `v1.1.11` 桌面版无法启动的根因。
    - **#5095 [[Bug]: 桌面客户端 Windows 版 v1.1.11 安装后无法启动](https://github.com/agentscope-ai/QwenPaw/issues/5095)**: 与 `#5086` 是同一个问题的不同表现。
    - **Fix PR**: 已经有多个 PR 在处理此问题，包括 `#5096`（锁定 OpenSSL 版本）、`#5082`、`#5083`、`#5084`、`#5085` 等。最终通过发布 `v1.1.11.post1` 版本（PR #5093）解决。**建议所有 Windows 用户升级。**

- **严重：Agent 相关定时任务失效**
    - **#5064 [[Bug]: Agent 生成的定时任务，无法正常触发，也无法进行手动编辑](https://github.com/agentscope-ai/QwenPaw/issues/5064)**: 该问题指向 Agent 生成的定时任务存在系统性问题，目前为 OPEN 状态，尚无明确修复 PR。
    - **#4878 [[Bug]: 定时任务结果无法推送到微信](https://github.com/agentscope-ai/QwenPaw/issues/4878)**: 该问题虽已 CLOSED，但说明定时任务在特定渠道（微信）上存在根本性的推送问题。

- **中等：其他 Bug**
    - **#5052 [工具调用若干次后报错](https://github.com/agentscope-ai/QwenPaw/issues/5052)**: 工具调用几轮后所有工具报 `got an unexpected keyword argument 'arguments'`，可能是工具调用解析或缓存问题。
    - **#5057 [DingTalk AI Card 发送空卡片](https://github.com/agentscope-ai/QwenPaw/issues/5057)**: 当 Agent 输出为空时，钉钉收到一个“处理中...”的空卡片，影响体验。
    - **#4989 & #4184 [本地模型对话无响应或中断](https://github.com/agentscope-ai/QwenPaw/issues/4989)**: 使用本地部署模型时，对话无响应或任务中断，该问题在不同版本中反复出现，值得关注。

#### 6. 功能请求与路线图信号

用户今日提出了多个有价值的功能请求，其中一些已有对应的 PR，显示出项目路线图与社区需求的高度契合。

- **高概率纳入下一版本**：
    - **独立视觉模型配置**：Issue [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) 建议为不支持多模态的主模型配置独立的“视觉模型”，实现视觉能力的“中转站”效果。这是一个非常务实和受欢迎的功能，与模块化设计的思路一致。
    - **上下文压缩**：Issue [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) 建议集成 Headroom 实现上下文压缩，可节省 60-95% Token。这在长上下文场景下极具价值，预计会受到项目组认真评估。

- **与现有 PR 呼应，可能被纳入**：
    - **Token 用量显示**：Issue 中用户对 Token 消耗的关注（如 [#4865](https://github.com/agentscope-ai/QwenPaw/issues/4865) 讨论上下文卡死与 Token 量）与 PR [#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433)（新增 Token 用量信息展示）完全吻合。该 PR 已进入 “Under Review” 状态，很可能在下一个版本中合并。
    - **子任务进展可视化**：Issue [#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923) 要求查看子代理任务的运行进展。这与项目追求更透明的 Agent 行为的诉求一致，可能通过增强前端渲染或日志系统来实现。

- **长期路线图信号**：
    - **治理与安全**：PR [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) 和 PR [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) 表明，项目已经开始为 Agent 的**管控、沙箱化和外部扩展**做顶层设计。这将是未来几个版本的焦点之一。
    - **文件与工具守卫**：Issue [#4356](https://github.com/agentscope-ai/QwenPaw/issues/4356) 提出的更细粒度的文件/工具访问控制（如只读目录）反映了用户对 Agent 安全的更高要求，是治理讨论的一部分。

#### 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出以下用户痛点和使用场景：

- **“我的 Agent 失控了”**：这是最强烈的反馈信号。用户创建的定时任务无法被触发或修改（Issue #5064），子任务的内部进展无法查看（Issue #4923），这让他们对 Agent 的行为感到焦虑和不安。
- **“卡死了”**：多个用户反映不同场景下的性能问题。
    - 工具调用生成文件时，前端无流式渲染，长时间处于“loading”状态，像“卡死”了一样（Issue #4865）。
    - 会话切换时，因数据量大导致前端卡顿超过10秒（Issue #5053）。
    - 浏览器打开一个包含大量 Token 的对话时，页面直接卡死（Issue #4213）。
- **“更新后反而坏了”**：`v1.1.11` 版本在 Windows 上无法启动（Issue #5095），导致部分用户升级后无法使用。同时，本地模型在 `v1.1.9` 和 `v1.1.10` 上无法正常工作，回退到旧版本才正常（Issue #4989）。这严重影响了用户对新版本的信任。
- **“我想要更灵活的控制”**：用户希望主模型不支持多模态时，能有一个独立的视觉模型来补位（Issue #4992）。用户希望文件访问控制能更精细，例如设置某些目录为只读（Issue #4356）。

#### 8. 待处理积压

- **#4342 [[CLOSED] [test] 单元测试覆盖率 (Phase 5)](https://github.com/agentscope-ai/QwenPaw/issues/4342)**: 虽然该 Issue 已关闭，但它反映了项目对测试覆盖率的持续投入。如其父任务所示，这是一项长期工程。后续的迁移（如 Issue #4727）和重构（PR #5078）可能会对现有测试的稳定性和覆盖率提出新的挑战。

- **#5064 [[OPEN] Agent 生成的定时任务无法正常触发](https://github.com/agentscope-ai/QwenPaw/issues/5064)**: 这是一个影响 Agent 核心价值的重要问题，且是今日新开的 Issue，目前尚无解决方案或 PR 关联。考虑到其严重性，**建议维护者优先关注并安排人手跟进**。

- **#5065 [[OPEN] MODEL_EXECUTION_FAILED 报错](https://github.com/agentscope-ai/QwenPaw/issues/5065)**: 该 Issue 提供了详细的报错日志，但问题描述不够清晰。**建议维护者与提问者进一步沟通**，促使他补充更多上下文，以定位是模型配置问题、网络问题还是代码 Bug。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 ZeroClaw 项目数据生成的日报。

---

# ZeroClaw 项目动态日报 | 2026-06-11

## 今日速览

ZeroClaw 项目继续保持极高的开发活跃度。过去 24 小时内，社区提交了 43 条 Issue 和 50 个 PR，其中包含多个高优先级（P1）的 Bug 报告和功能完善。尽管没有新版本发布，但项目在跨平台支持、用户界面体验、工具插件系统以及核心稳定性方面取得了显著进展。今日最关键的动态包括大规模修复 Windows 平台测试失败、统一核心架构（RFC）的深度讨论，以及社区对于文档和入门体验的持续完善。**项目整体处于快速迭代期，健康度良好，但高吞吐量也带来了较高的维护压力和合并积压。**

## 项目进展

今日合并/关闭的关键 PR 主要集中在优化 CI 流程和修复关键文档/配置问题，为后续开发扫清了障碍。

- **CI/测试流程优化**：PR [#7458](https://github.com/zeroclaw-labs/zeroclaw/pull/7458) 被合并，回滚了将跨平台 Clippy 检查设为必需的门禁。此举旨在平衡 CI 速度与代码质量，避免每个 PR 都运行耗时的跨平台检查，同时通过非必需工作流（Issue [#7486](https://github.com/zeroclaw-labs/zeroclaw/issues/7486)）来追踪。
- **社区入口修复**：PR [#7096](https://github.com/zeroclaw-labs/zeroclaw/pull/7096) 被合并，修复了 README 中失效的 Discord 邀请链接，使用户能够正常加入社区。
- **配置与功能完善**：与 Issues 相关的多个 PR 被创建以解决用户报告的问题，例如修复自定义编辑器路径、配置模型检查错误等，体现了项目对社区反馈的快速响应。

## 社区热点

今日讨论焦点主要集中在**跨平台兼容性**和**核心架构精简**两大方向，反映了社区用户对生产环境可用性和长期维护性的高度关注。

1.  **Windows 平台兼容性 (#7462)**：
    - **链接**: [Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
    - **热度**: 当日新开，0 评论但作为 P1 级 Bug 引起广泛关注。
    - **分析**: 该 Issue 报告了在 Windows 上运行测试套件时有 **74 个测试失败**。这揭示了项目当前以 Linux 为主的测试策略的短板，是阻碍 Windows 用户和开发者的首要障碍。社区对此表现出高敏感性，因为它直接关系到项目的跨平台承诺。

2.  **核心功能统一架构 RFC (#7415 & #7420)**：
    - **链接**: [RFC: 统一代理执行引擎 #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) | [RFC: 原生动态链接库插件系统 #7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)
    - **热度**: 尽管是新开议题，但属于高风险的架构级 RFC，评论区内有核心贡献者（如 @Nillth, @Vitaly567）的深度参与。
    - **分析**: 这两个 RFC 触及了 ZeroClaw 长期发展的核心。
        - `#7415` 指出当前存在 **三个并行且不一致** 的代理执行引擎，提议统一以减少 Bug 和维护成本。
        - `#7420` 则主张引入 **动态链接库插件系统**，以摆脱当前“单体仓库 + 内置工具”的臃肿模式。
        这些讨论表明社区正在积极思考如何让 ZeroClaw 变得更轻量、更稳定、更易于扩展。

## Bug 与稳定性

今日报告的 Bug 集中在**数据完整性**、**跨平台兼容**和**安全配置**上，其中多个问题已有对应的修复 PR。

- **[S1 - 工作流阻塞]**
    - **消息丢失 (#6034)**: 单轮/多轮对话中用户消息丢失，影响所有用户。状态为 `accepted`，暂无直接 fix PR，需要持续关注。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6034)
    - **子代理 `cwd` 继承问题 (#7263)**: 子代理未继承工作目录，导致 ACP 驱动开发模式受阻。状态为 `accepted`，暂无 fix PR。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7263)
    - **代理委托权限问题 (#7470)**: 新报告的 Bug，当目标代理的 `risk_profile.allowed_tools` 配置为空或过于严格时，代理委托失败。状态 `OPEN`，暂无 fix PR。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **[S1/S2 - 功能/性能严重降级]**
    - **工具 `tool_search` 在非交互模式下挂起 (#6721)**: 在 Webhook 模式下，由于缺乏自动批准，`tool_search` 工具会挂起 120 秒后自动拒绝。状态为 `accepted`。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6721)
    - **`image_info` 工具输出无法传递 (#7436)**: 使用相对路径或 workspace 路径时，图片信息无法正确传递给多模态模型。状态 `OPEN`。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7436)
    - **DashBoard 状态显示错误 (#7376)**: zerocode 仪表盘会隐藏错误状态，并将历史会话标记为活跃。 **已关闭**，相关修复可能已合并。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7376)

- **[Windows 兼容]**
    - **74 个 Windows 测试失败 (#7462)**: 严重阻碍了项目的跨平台可用性，已被标记为 P1。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)

## 功能请求与路线图信号

社区对功能的诉求集中在提升**易用性**和**降低入门门槛**上。
- **增强和丰富配置/编辑体验**：功能 [#7468](https://github.com/zeroclaw-labs/zeroclaw/issues/7468) 和 [#7467](https://github.com/zeroclaw-labs/zeroclaw/issues/7467) 分别提出在 TUI 中允许重命名别名和提供更灵活的字符串编辑能力（如使用方向键导航）。这表明用户正在深入使用配置功能，并期望获得更现代化的交互体验。
- **简化 Docker 部署**：功能 [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) 关于提供包含所有功能（如 WhatsApp）的“完整版” Docker 镜像，获得了较多 👍 和评论。这表明非技术用户或快速试用者对现有轻量级镜像感到不便，期望“开箱即用”。相关 PR [#7475](https://github.com/zeroclaw-labs/zeroclaw/pull/7475) 已尝试着手解决文档问题。
- **核心功能重构**：RFC #7415 和 #7420 代表着社区中资深开发者对项目架构的远期思考。这些 RFC 如果被采纳，将深刻改变 ZeroClaw 未来的发展路径，使其更具可维护性和扩展性。虽然短期内不会落地，但它们是判断项目技术走向的重要信号。

## 用户反馈摘要

从近期 Issues 和 PR 的评论中，可以归纳出以下真实用户痛点：

- **“入门门槛”是最大痛点**：多位用户（如 #3642, #6034, #7467）通过不同方式表达了现有功能“难用”或“不直观”。无论是 Docker 镜像的功能缺失、配置过程的繁琐，还是对话消息的丢失，都在打击新用户的试用积极性。
- **“兼容性问题”困扰开发者和高级用户**：Windows 平台的测试失败和 `image_info` 工具在多模态场景下的失效，直接影响了专业用户将该框架应用于实际工作的能力。
- **“容器化环境”的特定问题**：Issue [#7469](https://github.com/zeroclaw-labs/zeroclaw/issues/7469) 报告了容器内默认编辑器 `vi` 不存在的问题，虽然是一个“小毛病”，但反映了容器镜像默认配置与实际运行环境的脱节。PR [#7483](https://github.com/zeroclaw-labs/zeroclaw/pull/7483) 和 [#7476](https://github.com/zeroclaw-labs/zeroclaw/pull/7476) 正在尝试解决此问题。

## 待处理积压

- **等待维护者回应的架构级 RFC**：
    - `[RFC] Unify the three agent turn engines` [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415): 标记为 `needs-maintainer-review`，尚未有官方核心维护者表态。
    - `[RFC] Native Dynamic-Library Plugin System` [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420): 同样等待核心团队的评审。这两个 RFC 将对项目产生重大影响，需要核心维护者尽快介入组织讨论。

- **长期存在的优先特性**：
    - `[Feature]: Provide a "full" docker image` [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642): 创建已有近 3 个月，获得了 3 个 👍 和 12 条评论，但状态仍为 `blocked`。这可能是影响非技术用户增长的关键堵点。

- **高风险的阻塞 Bug**：
    - `[Bug]: 单轮对话以及多轮对话会出现丢失 user message的现象` [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034): 作为 P1 级别的数据丢失 Bug，虽然已被接受，但尚未看到分配的 fix PR，风险极高。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*