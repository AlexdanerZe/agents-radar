# OpenClaw 生态日报 2026-06-03

> Issues: 425 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-03 03:46 UTC

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

好的，这是为您生成的 OpenClaw 项目动态日报（2026-06-03）。

---

## OpenClaw 项目动态日报 | 2026-06-03

### 1. 今日速览
今日项目活跃度极高，在 **24 小时内处理了 425 条 Issue 和 500 条 PR**，社区参与异常踊跃。尽管暂无新版本发布，但团队与贡献者合力**合并/关闭了 109 个 PR**，大量修复直指近期用户反馈强烈的 “消息丢失” 与 “Codex 运行时回归” 问题。目前项目处于“存量稳定”与“增量规划”并行阶段：一方面紧急应对 Windows UI、Slack/Telegram 投递异常等致命 Bug；另一方面，关于 SQLite 统一架构迁移（`#88838`）及更智能的记忆检索系统（`#89584`）的讨论热度不减，显示出强劲的演进动力。

### 2. 版本发布
今日无新版本发布。社区讨论主要围绕 2026.5.27 及 2026.5.28 版本的回归问题展开。

### 3. 项目进展
今日项目成功推进了 **109 个 PR**，主要进展集中在会话稳定性和渠道适配性上：

- **会话与数据恢复**：
  - [PR#89065] 修复了会话文件头部因意外损坏而导致**整个对话历史被静默清空**的严重数据丢失问题。
  - [PR#67202] 强制写操作后校验，消除了“写入成功”的假阳性报告，避免 Agent 被错误状态误导。
- **渠道消息交付优化**：
  - [PR#87626] 修复了 Telegram 持久化私聊中上下文信息（chat window）重复注入的问题。
  - [PR#79176] 解决了 `github-copilot` 提供商下 GPT 系列模型因“加密推理内容”重放而导致下游请求被拒（400错误）的兼容性问题。
- **生态扩展**：
  - [PR#86169] 已合并，正式加入了对 **Xiaomi MiMo Token Plan** 提供商的原生支持，扩展了模型生态。

### 4. 社区热点
今日讨论最激烈、反馈最集中的议题凸显了用户对“基础通讯可靠性”和“架构稳定性”的极高关注：

- **核心通讯崩溃**：[Issue #52875](https://github.com/openclaw/openclaw/issues/52875)（21条评论，P2）
  - **现象**：升级后主 Agent 调用 `session_send` 返回“无会话存在”，导致智能体间通讯完全断裂。这是对项目“多 Agent 协作”核心能力的沉重打击，引发了开发者社区对会话路由机制的深度排查。
- **Codex 回归反复**：[Issue #88312](https://github.com/openclaw/openclaw/issues/88312)（10条评论，2个 👍，P1）
  - **现象**：2026.5.27 版本中 Codex 应用服务器的“回合完成”再次停滞（`Codex stopped before confirming the turn was complete`），这实际上是之前已修复问题（`#84076`）的**再次回归**。用户感叹修复回滚，社区对此表现出强烈的维稳诉求。
- **窗口聊天体验倒退**：[Issue #67035](https://github.com/openclaw/openclaw/issues/67035)（14条评论，P1）
  - **现象**：Windows 版 Web UI 输入内容被吞噬，流式回复不可见。用户 q7793527 详细描述了“输入的文字消失，需要手动刷新页面”的糟糕体验，该 Issue 直指 WebChat 前端的渲染核心逻辑。
- **基础设施关注**：[Issue #88788](https://github.com/openclaw/openclaw/issues/88788)（12条评论）
  - **现象**：GHCR 发布的 Docker 镜像中配置 Schema 过旧（与运行时文件不匹配），导致 `channels.discord.streaming.progress.commentary` 配置报错。这影响了大量基于容器部署的用户，反馈集中在**版本发布流程的严谨性**上。

### 5. Bug 与稳定性
今日报告的 Bug 呈现明显的**回归潮**，严重性等级较高的如下：

| 严重等级 | 编号 | 关键链接 | 标题 | 是否已有 Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **致命 (P1)** | `#88312` | [链接](https://github.com/openclaw/openclaw/issues/88312) | [Regression] Codex 回合完成再次停滞（二进宫） | 否 (Needs live repro) |
| | `#67035` | [链接](https://github.com/openclaw/openclaw/issues/67035) | [Regression] Windows UI 输入文本被吞，流式回复不可见 | 是 (Linked PR Open) |
| | `#86519` | [链接](https://github.com/openclaw/openclaw/issues/86519) | [Regression] Telegram 回复 2-10x 重复 | 否 (Needs info) |
| | `#80715` | [链接](https://github.com/openclaw/openclaw/issues/80715) | [Bug] Slack 回复被静默丢失（转录有，投递无） | 是 (Linked PR Open，高赞 8👍) |
| | `#86047` | [链接](https://github.com/openclaw/openclaw/issues/86047) | [Regression] Codex 插件审批超时导致对话中断 | 否 (Needs maintainer review) |
| | `#55334` | [链接](https://github.com/openclaw/openclaw/issues/55334) | [Perf] sessions.json 无限增长导致网关 OOM | 否 (Needs product decision) |
| | `#89678` | [链接](https://github.com/openclaw/openclaw/pull/89678) | [Fix] macOS LaunchAgent SIGTERM 未正确触发重启（PR） | 是 (Waiting on author) |
| **高危 (P2)** | `#88788` | [链接](https://github.com/openclaw/openclaw/issues/88788) | GHCR Docker 镜像配置 Schema 过期 | 否 (Needs maintainer review) |
| | `#63918` | [链接](https://github.com/openclaw/openclaw/issues/63918) | Cron AgentTurn 发送 `thinking=none` 导致 OpenAI 400 错误 | 否 (Open) |
| | `#84882` | [链接](https://github.com/openclaw/openclaw/issues/84882) | Memory-core 流水线静默删除用户的每日记忆文件 | 否 (Open) |
| **安全** | `#39604` | [链接](https://github.com/openclaw/openclaw/issues/39604) | [Feature] 需要 `tools.web.fetch.allowPrivateNetwork` 控制私有网络访问 | 否 (Needs security review) |
| | `#45269` | [链接](https://github.com/openclaw/openclaw/issues/45269) | [Bug] `apply_patch` 在 Agent 策略管道中被误判为插件工具（Closed） | **已解决** |

### 6. 功能请求与路线图信号
尽管修复当前 Bug 是首要任务，但从合并/活跃的 PR 和 Issue 中仍可看出清晰的路线图信号：

- **向企业级与可维护性靠拢**：
  - **[SQLite 统一存储]** `#88838` 的深入讨论表明项目计划将所有会话状态和转录数据迁移至 SQLite，以解决当前 `sessions.json` 爆炸（`#55334`）等顽疾，这是未来架构稳定性的基石。
  - **[持久化队列]** PR `#82572` 旨在持久化 Followup 队列，防止网关重启导致任务丢失，提升生产环境的可靠性。
- **智能能力增强**：
  - **[记忆检索增强]** PR `#89584` 引入可选的**交叉编码器重排序**，旨在改善 Agent 记忆检索的命中率，迈向量级提升。
- **用户体验与安全性的平衡**：
  - **[私有网络访问]** `#39604`（13条评论，9 个 👍）是目前社区呼声最高的功能，用户希望在享受 `web_fetch` 便利性的同时拥有控制**安全边界**的能力。
  - **[消息钩子系统]** `#81061` 提出的“预路由消息钩子”和 `#70990` 的“模型故障转移钩子”表明，社区正在推动 OpenClaw 成为一个更具可扩展性的**消息与 AI 编排平台**。

### 7. 用户反馈摘要
- **核心痛点：消息投递的信任危机**
  用户对“发不出去”和“重复发送”的容忍度极低。Slack 消息静默丢失（`#80715`，8个 👍）和 Telegram 信息重复（`#86519`）严重动摇了用户对 OpenClaw 作为消息总线的信任。用户 cblustein-cpu 在 `#80715` 中抱怨：“*一周内我在两个不同的对话中遇到了两次*”。
- **升级带来的“开倒车”体验**
  Windows UI（`#67035`）和 Codex 运行时（`#88312`）的回退让用户感到沮丧。用户 q7793527 详细描述了输入文字马上消失的体验，这表明**新版本的 QA 流程可能需要增加更多的回归测试覆盖**，特别是针对 UI 和核心运行时。
- **运维的复杂度反馈**
  用户期望“开箱即用”，但 Docker 镜像 Schema 过期（`#88788`）和 macOS 启动项问题（`#89678`）暴露了发布流程中对环境差异的考量不足。

### 8. 待处理积压
以下高优问题长期处于阻塞或等待决策状态，需要维护团队重点关注：

- **产品决策阻塞**：
  - `#55334` **[P1]** sessions.json 无限增长 OOM——自 3 月底报告，虽已有修复方案，仍在等待产品侧决策如何处理“旧会话优雅退役”策略。
  - `#52249` **[P1]** ACP 父会话卡死不刷新——影响多 Agent 协作体验，需明确修复 Scope。
  - `#39604` **[Feature]** 私有网络访问安全开关——呼声极高，但安全评审迟迟未下结论。
- **等待维护者响应**：
  - `#89530` **[P1]** 修复 UI 聊天流式文本可见性——**已标记为“Ready for maintainer look”**。
  - `#86036` **[P1]** 修复 CJK 输入法组成（IME）问题——影响所有东亚用户的输入体验，等待合并。
  - `#89686` **[P2]** 隔离无效的 MCP 捆绑工具——防止单一工具加载失败阻塞整个 Agent。

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析报告

**分析日期：2026-06-03 | 数据来源：各项目 GitHub 仓库当日动态**

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处在**快速迭代与深度分化并存的阶段**。头部项目在经历功能爆发后进入稳定性攻坚期，普遍面临回归潮与安全审计挑战；中等活跃项目加速补全渠道与工具生态，聚焦 MCP 稳定性与多 Agent 编排；少量新兴项目则在语言选择（Zig）、终端 TUI、轻量级 RAG 等细分方向上建立差异化优势。整体生态的共性矛盾是：**用户对“基础通信可靠性”与“开箱即用体验”的要求，正在超过项目对功能密度的追求**。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issue 更新 | 今日 PR 更新 | 合并/关闭 PR | 版本发布 | 项目健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 425 条 | 500 条 | 109 个 | 无 | ⚠️ 极高活跃但严重回归潮，消息投递信任危机 |
| **NanoBot** | 9 条 | 25 条 | 17 个 | 无 | ✅ 高活跃，核心能力双突破，健康度佳 |
| **Hermes Agent** | 50 条 | 50 条 | 7 个 | 无 | ⚠️ 活跃但 Docker 镜像阻断性 Bug 未修复，P1 堆积 |
| **PicoClaw** | 3 条 | 14 条 | 6 个 | v0.2.9-nightly | ✅ 迭代高效，维护响应敏捷，整体健康 |
| **NanoClaw** | 1 条 | 6 条 | 4 个 | 无 | 🟡 中等偏上，社区冷清，功能推进务实 |
| **NullClaw** | 1 条 | 1 条 | 0 个 | 无 | 🟡 待 Code Review，单点 Bug 修复闭环中 |
| **IronClaw** | 30 条 | 50 条 | 31 个 | 无 | ✅ 极高产出，架构审计扎实，但 CI 失败需关注 |
| **LobsterAI** | 0 条 | 6 条 | 6 个 | 无 | ✅ 内部开发驱动，MCP/Artefacts 亮点，稳定 |
| **Moltis** | 1 条 | 1 个待审 | 0 个 | 无 | 🟡 中等，单 PR 关键性增强，用户噪声需求 |
| **CoPaw** | 36 条（关闭 20） | 31 条（关闭 10） | 10 个 | 预发布 v1.1.11b1 | ⚠️ 极高活跃但严重 Bug 堆积（会话污染、压缩崩溃） |
| **ZeroClaw** | 50 条（关闭 33） | 50 条（关闭 47） | 47 个 | **v0.8.0-beta-2** | ✅ 发布日产出极高，Bug 修复循环快，健康度优秀 |

> *注：TinyClaw、ZeptoClaw 过去 24 小时无活动，未列入表格。*

---

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模与参与者活跃度远超其他项目（24 小时 425 Issue + 500 PR 是第二梯队项目的 8～10 倍）。渠道覆盖面最广（Telegram、Slack、Discord、飞书、GitHub Copilot 等），是事实上的**跨平台消息总线参照实现**。对 SQLite 统一架构、记忆检索增强的讨论表明其对长期架构投入的重视。
- **技术路线差异**：强调**多 Agent 协作核心**（`session_send` 通讯断裂被视为 P2 严重问题），并且正在推动**消息与 AI 编排平台化**（预路由钩子、模型故障转移钩子）。相比 Hermes 的子代理 RFC 和 ZeroClaw 的 TUI 侧重，OpenClaw 更偏向**无头后端 + 多渠道桥接**。
- **社区规模对比**：从 PR/Issue 量级看，OpenClaw 是**生态绝对头部**；IronClaw、ZeroClaw、CoPaw、Hermes 处于第二梯队（日 PR 50 左右）；NanoBot、PicoClaw、LobsterAI 为第三梯队。但 OpenClaw 的稳定性问题（Codex 回归二进宫、Windows UI 输入被吞）在同量级项目中最为突出，反映出**功能推新与质量验证之间的失衡**。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
|---|---|---|
| **MCP（模型上下文协议）稳定性** | NanoBot、IronClaw、PicoClaw、CoPaw、LobsterAI | 会话无故终止（NanoBot #4168）；SSRF 攻击面（NanoBot #4123）；启动卡死/重跑 npx（LobsterAI #2091）；工具名含 `.` 无法调用（CoPaw #4918） |
| **多 Agent / 子 Agent 编排** | OpenClaw、Hermes、CoPaw、ZeroClaw、NanoBot | 子 Agent 无法继承 MCP（NanoBot #4166）；任务中继 RFC（Hermes #31392）；`spawn_subagent` 运行不可见（CoPaw #4923）；委托 Agent 忽略注入控制（ZeroClaw #5155） |
| **渠道稳定性与国内 IM 接入** | OpenClaw（Slack/Telegram 丢失）、CoPaw（微信/企微/元宝）、NanoBot（QQ Napcat）、Hermes（飞书）、PicoClaw（微信图片报错） | 消息静默丢失、重复投递、定时任务无法推送、Proto 文件缺失导致无限重连 |
| **上下文窗口治理与记忆** | OpenClaw（SQLite 统一架构、记忆检索交叉编码器）、CoPaw（无损压缩 DAG、工具按需加载）、NanoBot（轻量级 RAG 合入）、IronClaw（压缩重试幂等性）、Hermes（DIKW 全息记忆展示） | 多项目一致反映上下文 Token 膨胀、压缩崩溃、静默删除历史文件 |
| **图像/多模态输入** | NanoBot（generate_image API 兼容性）、LobsterAI（MiniMax-M3 图像支持修复）、CoPaw（图片不能直接载入上下文） | 硬编码 `response_format` 导致第三方 API 失败；模型图像支持硬编码开关 |
| **安全加固** | NullClaw（PII 脱敏误杀）、NanoClaw（OS 命令注入）、CoPaw（7 个漏洞快速关闭）、OpenClaw（私有网络访问控制）、IronClaw（HTTP 凭据内存清零） | 社区安全审计角色兴起，漏洞报告与修复速度成为项目成熟度标志 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | NanoBot | Hermes Agent | IronClaw | CoPaw (QwenPaw) | ZeroClaw | LobsterAI |
|---|---|---|---|---|---|---|---|
| **功能侧重** | 多渠道消息总线 + 多 Agent 协作 | 轻量 RAG + 国内渠道优先 | 高度可定制、企业级配置与安全 | Reborn 架构、主动 Trigger、Slack 集成 | AgentScope 生态、沙箱、聊天伴侣 | 原生 TUI（zerocode）+ 技能生态 | 协作办公（cowork）+ Artefacts + MCP 优化 |
| **目标用户** | 自托管开发者，追求广泛集成 | 国内市场、低成本快速部署 | 企业/专业开发者，需要精细安全控制 | NEAR AI 生态开发者，重视架构审计 | AgentScope 用户群，国内 IM 重度使用者 | 终端爱好者和技能开发者 | 网易有道用户、跨 IM 协作团队 |
| **技术架构** | 基于网关 + 会话层，迈向 SQLite 统一 | 标准 Agent 循环 + cron 调度 + 内存嵌入 | Provider 丰富，支持 Desktop 与 ACP 模式 | Rust 底层，Engine v2，WASM 工具 | Python，AgentScope 1.x→2.0，插件钩子 | Ratatui TUI，技能白名单，多版本文档 | Electron 桌面 + MCP 解析优化 |
| **独特亮点** | 社区体量绝对领先，渠道覆盖最广 | QQ 渠道（Napcat）填补空白 | 1Password 集成、i18n 框架、飞书深度适配 | 架构审计 17 个 Issue 系统性自查 | 安全漏洞快速响应（7 个 24h 关闭） | **官方 TUI 客户端**，技能 LLM 自描述 | Artefacts 特性，npx MCP 预安装解析 |

---

## 6. 社区热度与成熟度分层

| 层级 | 项目 | 特征 |
|---|---|---|
| **第一梯队：极高活跃，快速迭代但稳定性存疑** | OpenClaw、CoPaw、IronClaw、Hermes Agent | 日 PR 更新 30～500；功能推进激进；伴随显著回归潮和高危 Bug 堆积；维护团队响应快但测试覆盖有待加强 |
| **第二梯队：高活跃，迭代稳健，健康度良好** | ZeroClaw、NanoBot、PicoClaw、LobsterAI | 日 PR 更新 6～50；修复循环快；发布节奏清晰（ZeroClaw 刚发 Beta，LobsterAI Artefacts 落地）；社区参与质量高 |
| **第三梯队：低活跃或单点突破** | NanoClaw、NullClaw、Moltis | 日 PR/Issue 在个位数；以关键 Bug 修复或单一功能增强为主；社区反馈稀缺，但代码质量扎实 |
| **静默项目** | TinyClaw、ZeptoClaw | 当日无活动 |

**成熟度评估**：ZeroClaw 因**版本化文档、预发布流程、技能白名单和 TUI 落地**在成熟度上领先；IronClaw 通过**系统架构审计**展示出生产级追求；OpenClaw 虽活跃但连续回归（Codex 二进宫、Windows UI 回退）削弱用户信任，成熟度受质疑。

---

## 7. 值得关注的趋势信号

1. **“回归常态化”催生 QA 升级需求**：OpenClaw（Codex 二进宫、Windows UI 回退）、CoPaw（v1.1.9 后系统 fallback 频升）等现象表明，**快速迭代的项目亟需引入自动化回归测试与渠道级集成测试**，否则将持续消耗社区信任。

2. **安全审计社区化**：CoPaw 一日内 7 个安全漏洞由外部研究员提交并关闭、NullClaw 社区自愈 PII 脱敏误杀，说明 **AI Agent 的安全攻防正在从项目方独立负责转向社区众包**。项目方应建立明确的漏洞报告奖励机制和响应 SLA。

3. **国内 IM 渠道成为“标配”**：QQ（NanoBot）、微信/企微（CoPaw）、飞书（Hermes）、钉钉（LobsterAI 积压 PR #1464）的集成或修复活跃，**覆盖中国用户的核心触达渠道已成为争夺国内开发者的前提条件**。

4. **多 Agent 编排从 RFC 走向落地**：Hermes 提出任务中继 RFC、ZeroClaw 发布多 Agent 运行时、OpenClaw 修复会话通讯断裂、CoPaw 改进 `spawn_subagent`，表明**跨 Agent 协作不再是概念讨论，而是各项目未来 1-2 个小版本内的交付目标**。

5. **上下文压缩成为“必须攻克”的瓶颈**：CoPaw 的上下文压缩崩溃、OpenClaw 的 SQLite 迁移讨论、NanoBot 的轻量 RAG 合入、IronClaw 的压缩重试幂等性修复，反映**随着 Agent 会话越来越长，token 治理不再是可选项。** 开发者应关注支持结构化上下文管理的框架（如 DAG 摘要，按需加载工具定义）。

6. **本地模型（Ollama）支持仍为薄弱环节**：ZeroClaw #5962 持续 40 天未根治、Moltis 的工具反馈大小限制也间接影响本地部署，**本地模型用户的工具调用体验仍是阻碍开源 Agent 替代商业产品（如 ChatGPT Codex）的关键短板**。

7. **“Agent 自治”需求萌芽**：Hermes 社区要求 Agent 拥有内部时钟、自主切换模型、自动压缩上下文；CoPaw 用户希望子任务可单独选择轻量模型。这表明用户不再满足于被动响应，**期望 Agent 具备自我管理上下文的元能力**，将成为下一代 Agent 框架的设计目标。

---

**总结**：当前生态的十字路口在于——头部项目必须解决“功能多但不可靠”的矛盾，而新锐项目正通过差异化体验（TUI、安全、渠道）争夺份额。对于技术决策者，建议优先选择**回归测试覆盖率高、渠道抽象层成熟、记忆系统稳健**的项目作为集成基础；对于开发者，参与安全审计、上下文压缩、本地模型适配等方向将获得最高的社区认可度和技术影响力。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-03

## 1. 今日速览

过去 24 小时，NanoBot 项目展现出极强的开发动能，共处理 **9 条 Issue 更新**与 **25 条 PR 动态**，其中 **17 项 PR 成功合并或关闭**。核心维护者 `chengyongru` 持续高产，主导了 Dream 重构、QQ 渠道合入及多项 WebUI 体验修复。尽管未发布新版本，但轻量级 RAG 的正式落地与 Dream 架构的演进标志着项目在 Agent 核心能力与多平台接入上实现双突破，项目整体健康度极佳。

## 2. 版本发布

（无）

---

## 3. 项目进展（今日合并/关闭的重要 PR）

### 核心能力演进
- **轻量级 RAG 正式合入主干**：[PR #4109](链接)（作者 gqcao）—— 引入基于本地 Embedding 的轻量级记忆检索，有效延长 Agent 的历史上下文利用半径，减少对窗口式上下文的完全依赖。
- **Dream 架构重构完成**：[PR #3990](链接)（作者 chengyongru）—— 抛弃旧的两阶段 Dream 类，改用标准 Agent 循环 + `cron` 调度驱动，简化了后台任务的调度逻辑与代码维护成本。

### 渠道生态拓展
- **正式支持 QQ (Napcat) 频道**：[PR #4146](链接)（作者 chengyongru）—— 基于 OneBot v11 协议实现私聊与群聊，标志性补全了国内社交渠道的空白。
- **邮件渠道支持附件发送**：[PR #4162](链接) / [PR #4160](链接)（作者 chengyongru / Pringlas）—— 允许出站邮件携带媒体文件，并含附件数量与大小限制。

### WebUI 体验大修
- 密集合入多项修复：
  - 修复页面刷新后路由丢失（[PR #4150](链接)）
  - 修复侧边栏会话列表排序错误（[PR #4151](链接)）
  - 修复启动时无限阻塞请求（[PR #4157](链接)）
  - 修复非安全上下文下复制回退（[PR #4149](链接)）

### Bug 修复
- **解决 `read_file` 结果溢出与死循环**：[PR #4155](链接)（作者 jiehaoZ）—— 阻止 `read_file` 读取自身持久化的大工具结果时陷入"落盘-读取-再落盘"的无限循环。
- **界面修复系列**：CLI App 在 `uv tool` 环境下的 pip 安装问题，已有自动修复 PR（[#4159](链接)）及更完善的修复方案（[#4164](链接)）。

---

## 4. 社区热点

- **图像生成 API 兼容性（[#4167](链接), [#4132](链接)）**：用户 gkd2323c 报告 `generate_image` 因硬编码 `response_format` 参数导致第三方 API（如 Agnes AI）调用直接报错。与 Feature Request #4132 形成强关联，社区对打破 Provider 锁定的诉求呼声极高。
- **MCP 稳定性与子 Agent 权限障碍（[#4168](链接), [#4166](链接)）**：用户 tjc0726 连续提交两项核心痛点：MCP 服务在随机时间后断连（仅重启可恢复）、`spawn()` 子 Agent 无法继承 MCP 工具。暴露了当前 MCP 集成在生产环境下的连接健壮性与多 Agent 协作能力短板。
- **WebSocket 与 MCP 安全加固（[#4134](链接), [#4123](链接)）**：社区贡献者 DreamShepherd2006 和 yu-xin-c 分别针对 WebSocket 权限错误事件和 MCP 连接的 SSRF 攻击面提交修复 PR，体现出社区对安全层面的高度参与。
- **云平台统一部署层提议（[#4139](链接)）**：DreamShepherd2006 提交 800+ 行 PR，提议为 HuggingFace Spaces / ModelScope 构建零依赖的部署层，是降低部署门槛的里程碑式提议，目前处于活跃讨论。

---

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 | 修复 PR |
|---|---|---|---|
| **严重** | MCP 会话无故终止，`McpError: Session terminated`（[#4168](链接)） | **OPEN**，无临时方案 | 无 |
| **严重** | `generate_image` 因 `response_format` 硬编码与第三方 API 不兼容（[#4167](链接)） | **OPEN** | 无 |
| **中等** | 子 Agent 无法继承 MCP 服务工具（[#4166](链接)） | **OPEN**，社区提出配置开关建议 | 无 |
| **中等** | **[已修复]** `read_file` 结果恢复死循环（[#4153](链接)） | 已关闭 | [PR #4155](链接) |
| **低危** | **[已修复]** MemoryStore 并发写入游标重复（[#4081](链接)） | 已关闭 | 已合入 |
| **低危** | **[已修复]** WebUI 刷新后路由丢失、启动挂起（[#4150](链接), [#4157](链接)） | 已关闭 | 均已合入 |

---

## 6. 功能请求与路线图信号

- **自定义图像生成 Provider（[#4132](链接)）**：用户要求 `generate_image` 适配 `config.json` 中的 Provider 配置。考虑到 Bug #4167 的高阻塞率，该功能极有可能被纳入近期小版本。
- **消息"Fork"功能（[#4163](链接)）**：允许用户在任意历史用户消息上创建分叉对话，是对对话管理粒度的极大提升，符合高级用户的 Agent 交互控制需求。
- **API 成本精细化管控（[#4142](链接)）**：用户 `hamb1y` 发起关于 DeepSeek 等模型的 Cache Miss Token 成本优化讨论。随着高端模型的普及，API 调用经济学将成为高级用户的核心关注点。
- **云平台一键部署（[#4139](链接)）**：虽仍在评审阶段，但明确传递了社区降低使用门槛、拥抱云原生生态的信号。

---

## 7. 用户反馈摘要

- **核心痛点：MCP 稳定性**：多个用户反馈 MCP 连接在运行一段时间后失联（#4168）、子 Agent 无法继承 MCP 工具（#4166）以及 Notion MCP 长期无法连接（#1168——搁置 3 月未解决），可靠性是当前 MCP 集成最大的短板。
- **功能缺口：图像生成 Provider 灵活性**：`generate_image` 工具因依赖默认 Provider 且无法兼容第三方 API（#4167），被用户吐槽无法自由选择后端模型，限制了作为通用 Agent 的能力。
- **积极反馈：WebUI 持续高频迭代**：密集的 UI 修复（复制回退、刷新路由、启动速度）让用户直观感受到项目对前端体验的重视。
- **亮点：渠道生态拓展**：QQ 频道（#4146）与邮件附件（#4160）的正式支持为用户带来了可直接落地的跨平台集成价值。

---

## 8. 待处理积压

- **[长期搁置] #1168 | Notion MCP 连接失败**（创建于 2026-02-25）—— 长达 3 个月无有效解决方案。严重阻碍重度办公用户的上手体验，**建议维护者介入排查 MCP 协议匹配或输出官方配置文档**。
- **[等待合入] #3983 | Runner 层工具调用阻断测试 PR**（创建于 2026-05-24）—— 旨在增强 LLM 拒绝响应时的稳定测试覆盖，CI/CD 应优先督导合并以防回归。
- **[审议中] #4139 | 云平台部署层 Feature**（创建于 2026-06-01）—— 851 行代码的大 PR，若被接纳将成为降低部署门槛的重大里程碑，**建议尽快推进 Review 方向或合并决策**。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是根据 Hermes Agent GitHub 仓库 2026-06-03 的实时数据生成的项目动态日报。

---

# 🗓️ Hermes Agent 项目日报 | 2026-06-03

## 1. 今日速览
今日项目活跃度达到近期峰值，**过去 24 小时内共处理了 50 条 Issue 和 50 条 PR 更新**，社区参与热情极高。尽管没有新版本发布，但 7 个主要 PR 被合并，大量高质量的 Bug 修复 PR 被集中提交。社区讨论重心主要集中在 **Docker 镜像严重回归**（Matrix 网关崩溃）以及**代理自主编排能力**（任务中继 RFC）上。这是一个典型的“高产出爆发日”，开发与社区反馈形成了紧密的联动。

## 2. 版本发布
*（今日无新版本发布）*

## 3. 项目进展 — 关键推进与合并
今日项目在稳定性与配置灵活性上迈出了坚实一步，共有 **7 个 PR 被合并/关闭**。

- **🐛 重要修复合并：**
    - **模型配置修复：** `w1ndcn` 解决了两个关键的模型配置 Bug。
        - `#34559`：自定义提供商配置中的 `discover_models: false` 现在被正确识别，不再被忽略。
        - `#35145`：修复了实时模型发现逻辑，现在会**合并** API 返回的模型与用户手动配置的模型，而非覆盖后者。
    - **远程连接修复：** `#37399`（已关闭），修复了 Desktop 远程模式下在非回环地址（如 Tailscale/LAN 绑定）上的 WebSocket 来源拒绝问题，显著提升了桌面远程连接的兼容性。
    - **ACP 模式修复：** `#37813`（已关闭），修复了 ACP 模式因硬编码 `enabled_toolsets` 而忽略 `platform_toolsets` 配置，导致记忆提供者工具被错误屏蔽的问题。

- **🆕 今日提交的重要修复 PR（待合并）：**
    - **Desktop 体验：** 提交了针对 GUI 审批提示不渲染（`#37856`）和长线程滚动回弹（`#37831`）的修复 PR。
    - **飞书（Feishu）集成：** 针对近期授权回归问题提交了多个修复 PR（`#37847`、`#37849`），确保历史用户 ID 与新事件的兼容。
    - **安全性与其他：** 新增了 MiniMax 模型内容安全过滤（`#37851`）、危险命令误报修复（`#37854`）以及 Discord 消息前缀规范化（`#37850`）的修复 PR。

## 4. 社区热点
今日社区讨论异常激烈，主要集中在基础设施断裂与未来架构的探讨上。

- **🔥 `#25495` [Bug] Matrix / Synapse 在官方 Docker 镜像中不可用 (P1)**
    - *评论：10 | 状态：未关闭*
    - **摘要：** 用户反馈 Matrix/Synapse 网关在官方 Docker 镜像的某个特定 commit 后完全崩溃，日志卡在 “fixing ownership :1000”，无法启动。这是目前威胁最大的自托管稳定性问题，吸引了最多的讨论。
    - [链接](NousResearch/hermes-agent Issue #25495)

- **💡 `#31392` [RFC] 带自动派生子代理与异步人工审批门的代理原生任务中继系统 (P3)**
    - *评论：8 | 状态：未关闭*
    - **摘要：** 该 RFC 提出了一个复杂的自主多代理编排方案。社区对其“自动分岔子代理”与“异步人工审批”的设计反响强烈，代表了社区对下一代 Agent 架构（从简单委托走向精细编排）的强烈渴望。
    - [链接](NousResearch/hermes-agent Issue #31392)

- **😟 `#27221` [Bug] entrypoint.sh 在 HERMES_UID 重映射时缺少对 ui-tui/ 和 gateway/ 目录的 chown (P2)**
    - *评论：6 | 👍：2 | 状态：未关闭*
    - **摘要：** 该问题持续影响在 Synology/Unraid 等 NAS 设备上部署的用户。每当 UID 映射发生变化，权限问题就会初选，严重影响了容器化部署的体验。
    - [链接](NousResearch/hermes-agent Issue #27221)

- **🚀 `#37447` [Show & Tell] DIKW 记忆系统 — 全息记忆的四层自愈循环 (P3)**
    - *评论：2 | 👍：2 | 状态：未关闭*
    - **摘要：** 社区成员分享了自己基于 Holographic 记忆插件构建的四层自愈记忆闭环。这展示了社区在 Agent 记忆架构上的深刻探索与创新能力，获得了项目维护者的积极反馈。
    - [链接](NousResearch/hermes-agent Issue #37447)

## 5. Bug 与稳定性 — 按严重程度排列

**P1（严重 — 功能完全不可用）**
- **Docker 镜像矩阵网关崩溃（`#25495`）：** 新用户或更新后的用户无法通过 Matrix 连接 Hermes。**尚无修复 PR。**
- **Discord 网关过早结束会话（`#27881`）：** 在自主工作流中经常只返回部分信息就中断。**尚无修复 PR。**
- **自定义提供商 API Key 丢失（`#14065`）：** 运行时配置解析时内联 API Key（`api_key: xxx`）被静默丢弃。**尚无修复 PR。**
- **Windows 设置错误（`#37827`）：** 今日新增，Bootstrap 阶段 Git checkout 失败。

**P2（高 — 影响核心体验）**
- **Docker 权限映射缺陷（`#27221`）：** 影响 NAS 用户。尚无修复 PR。
- **Desktop GUI 审批失败（`#37812`）：** 手动审批模式弹窗不显示。**已有修复 PR `#37856`。**
- **Agent 陷入无效重试循环（`#24012`）：** 工具调用失败后擅自猜测补救措施，导致大量 Token 浪费。尚无修复 PR。
- **飞书授权回归（`#37847`,`#37849`）：** 今日已提交修复 PR。

**P3（中 — 平台兼容或体验问题）**
- **macOS DMG 仅支持 Arm64（`#37505`）：** Intel Mac 用户无法启动。尚无修复 PR。
- **Desktop 聊天窗口滚动回弹（`#37527`）：** 滚轮向上滚动时被吸回底部。**已有修复 PR `#37831`。**

## 6. 功能请求与路线图信号

今日功能请求呈现出明显的 **“从工具性到自主性”** 的跃迁信号：

- **代理架构升级：**
    - **多代理编排：** `#31392`（任务中继/子代理）和 `#31388`（多配置文件共享记忆）代表了社区对 Agent 编排能力的核心诉求，很可能成为未来大版本（v1.6/v2）的路线图参考。
    - **代理内省能力：** 用户明确要求 Agent 具备“内部时钟”（`#27742`）和自主调用 `model_switch`（`#16525`）及 `compress_context`（`#12213`）的能力。这指向一个核心需求：**Agent 需要从被动响应者进化为拥有部分环境上下文感知能力的执行者。**

- **开发者体验与 DevOps：**
    - **配置统一：** `#32537` 要求编码委托技能直接继承 Hermes 的 Provider 配置。如果实现，将无缝打通 Hermes 与 OpenHands、Claude Code 等工具的壁垒。
    - **密钥管理：** PR `#36896`（1Password 集成）表明项目正在向企业级安全标准看齐。
    - **国际化：** 今日提交的 PR `#35127`（i18n 完整框架）是一个重大投入信号，为全球部署铺平道路。

- **平台深度集成：**
    - **飞书：** 今日拥有最多的 PR 活动（多应用支持、授权修复、消息 ID 注入），表明开发者生态在积极推动该平台的深度优化。
    - **Desktop 转型：** PRD `#37835`（移动优先的 Mac 聊天 Hub）预示着 Desktop 客户端可能从“管理工具”转型为“交互中心”。

## 7. 用户反馈摘要

从今日回复中提炼出的真实用户声音：

- **“容器部署让我很痛苦”：**
    - *痛点：* “Docker image 我不能用了，日志卡在 fixing ownership”（`#25495`）。
    - *痛点：* “我想在 Unraid 上跑，但 UID 映射后权限就是不对”（`#27221`）。
- **“Desktop 体验差强人意”：**
    - *痛点：* “Mac Intel 用户直接被 Arm64 安装包拒之门外”（`#37505`）。
    - *痛点：* “我设置了手动审批，但弹窗根本没有出现，这还怎么保证安全？”（`#37812`）。
- **“Agent 不够聪明”：**
    - *诉求：* “Agent 不知道现在是几点，它怎么管理我的日程？”（`#27742`）。
    - *诉求：* “我希望 Agent 觉得任务太难时能自动切到 GPT-4o，而不是我手动敲 /model switch”（`#16525`）。

## 8. 待处理积压（需维护者重点关注）

以下是为数不多的高优先级且长期未解决的遗留问题，已严重影响用户信任与功能完整性：

1.  **`#25495` [P1] Matrix Docker 崩溃** — 持续 3 周，评论 10 条，无修复 PR。这是当前影响面最广的阻断性 Bug，亟需排查。
    [链接](NousResearch/hermes-agent Issue #25495)
2.  **`#14065` [P1] 自定义配置 API Key 丢失** — 持续 6 周，对于重度自定义提供商用户来说是定时炸弹。
    [链接](NousResearch/hermes-agent Issue #14065)
3.  **`#27881` [P1] Discord 过早终止会话** — 持续 2 周，影响 Discord 平台的可靠性声誉。
    [链接](NousResearch/hermes-agent Issue #27881)
4.  **`#27221` [P2] Docker 权限映射问题** — 持续 2 周，NAS 用户部署的常见障碍。
    [链接](NousResearch/hermes-agent Issue #27221)
5.  **`#24012` [P2] Agent 失败后无限猜测重试** — 持续 3 周，直接消耗用户 Token 并降低效率。
    [链接](NousResearch/hermes-agent Issue #24012)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据提供的 GitHub 数据生成的 PicoClaw 项目动态日报。

---

### PicoClaw 项目动态日报 | 2026-06-03

**项目分析师视角：** 过去24小时项目处于高强度迭代状态，核心聚焦于稳定性修复与 Provider 兼容性增强。14 个 PR 的密集更新（6 个已合入）表明团队正加速清理技术债务，为社区新特性的引入铺平道路。

---

#### 1. 今日速览

过去 24 小时，PicoClaw 项目迎来了开发与修复的高潮，共计更新 14 个 Pull Request 和 3 个 Issue。其中 6 个 PR 被迅速合并，涵盖内存泄漏修复、LLM 端错误重试、智谱 API 兼容性等多个关键领域。同时，Nightly 版本持续滚动发布。社区侧围绕“流式 HTTP 请求”与“WebSocket 信令完善”展开深入讨论，显示出用户对构建更强大终端的迫切需求。**项目整体健康度极高，维护响应敏捷。**

#### 2. 版本发布

- **版本号**: `v0.2.9-nightly.20260603.a502aa7f` (Nightly Build)
- **更新内容**: 集成了过去 24 小时内合并的多项核心修复，包括 Agent 层错误重试机制、SessionManager goroutine 泄漏、智谱 API 错误码处理及 Docker 配置优化。
- **破坏性变更**: 此版本为自动化构建的每日测试版，未标记破坏性变更。
- **迁移注意事项**: 集成内容未经全面回归，可能不稳定。生产环境建议等待稳定版，测试环境可试用最新修复。
- **完整变更日志**: [https://github.com/sipeed/picoclaw/compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

#### 3. 项目进展

今日合并的 PR 显著提升了项目健壮性与开发者体验：
- **Agent 健壮性提升**: [PR #2991](https://github.com/sipeed/picoclaw/pull/2991) 修复了 LLM 后端返回 HTTP 5xx 瞬态错误时 Agent 直接终止的问题，启用了智能重试与备用模型切换机制。
- **资源泄漏修复**: [PR #2986](https://github.com/sipeed/picoclaw/pull/2986) 为 SessionManager 引入 `Stop()` 方法，消除了后台 ticker goroutine 在重复创建时泄漏的问题。
- **Provider 兼容性**: [PR #2989](https://github.com/sipeed/picoclaw/pull/2989) 将智谱 GLM API 错误码 1210 纳入错误分类，修复了微信渠道图片请求无法触发 fallback 的问题。
- **文档优化**: [PR #2994](https://github.com/sipeed/picoclaw/pull/2994) 与 [PR #2993](https://github.com/sipeed/picoclaw/pull/2993) 正式添加了 Picoclaw Agent 自描述 Skill 文档，降低了新用户与 AI 模型理解项目工作流的门槛。
- **基础设施**: [PR #2239](https://github.com/sipeed/picoclaw/pull/2239) 合入了 Docker Compose 的 privileged 模式支持。

#### 4. 社区热点

- **讨论最热烈**: [Issue #2404](https://github.com/sipeed/picoclaw/issues/2404) - “在配置中添加流式 HTTP 请求功能”。该 Issue 已收获 10 条评论，用户明确要求支持类似 Python OpenAI Client 的 `stream=True` 配置。这是社区对低延迟、实时交互的核心诉求。
- **最新协议探讨**: [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984) - “为 WebSocket 客户端添加显式轮次完成信号”。用户提议在 Pico 协议中增加 `turn.complete` 信号，解决外部客户端无法确定 Agent 是否处理完毕的问题。这标志着社区正基于 PicoClaw 构建严肃的交互式产品。

#### 5. Bug 与稳定性

*按严重程度排列，标注修复进展：*

- **🔴 严重 [已修复]**
  - **微信 + 智谱 GLM-5 报错 ([#2943](https://github.com/sipeed/picoclaw/issues/2943))**: 发送图片触发 `error code 1210`。已在 [PR #2989](https://github.com/sipeed/picoclaw/pull/2989) 中修复并合并。
  - **Agent 不处理 500 错误 ([PR #2991](https://github.com/sipeed/picoclaw/pull/2991) 修复)**: 瞬态服务端错误导致 Agent 直接终止。
  - **SessionManager 泄漏 ([PR #2986](https://github.com/sipeed/picoclaw/pull/2986) 修复)**: 后台 Goroutine 无法退出。
- **🟠 严重 [修复 PR 已提交，审核中]**
  - **Web UI 历史记录不全 ([#2796](https://github.com/sipeed/picoclaw/issues/2796))**: 只能看到最后一条消息。 (PR [#2990](https://github.com/sipeed/picoclaw/pull/2990))
  - **升级后 Session 错乱 ([#2972](https://github.com/sipeed/picoclaw/issues/2972))**: v0.2.9 新会话附带旧消息。 (PR [#2992](https://github.com/sipeed/picoclaw/pull/2992))
  - **流中 tool_calls 丢失 ([#2958](https://github.com/sipeed/picoclaw/issues/2958))**: 活跃流式会话中工具调用消息被过滤。 (PR [#2987](https://github.com/sipeed/picoclaw/pull/2987))
- **🟡 中低 [修复 PR 已提交]**
  - **`/context` 阈值显示不准 ([#2968](https://github.com/sipeed/picoclaw/issues/2968))**: 压缩阈值不随配置变化，且缺少汇总阈值。 ([PR #2988](https://github.com/sipeed/picoclaw/pull/2988), [PR #2985](https://github.com/sipeed/picoclaw/pull/2985))
- **🟢 待审核 (Stale PRs)**
  - Cluade Opus 4 温度参数 ([PR #2948](https://github.com/sipeed/picoclaw/pull/2948))
  - web_search 工具类型兼容 ([PR #2951](https://github.com/sipeed/picoclaw/pull/2951))

#### 6. 功能请求与路线图信号

- **短期迭代重点:**
  - **流式 HTTP 请求支持 ([#2404](https://github.com/sipeed/picoclaw/issues/2404))**: 呼声最高，预计是下一个 Minor 版本的核心特性，可能涉及 Provider 适配层的重构。
  - **WebSocket 协议补全 ([#2984](https://github.com/sipeed/picoclaw/issues/2984))**: 完善 `turn.complete` 信号，是提升前端交互 S 级体验的关键。
- **生态工具信号:**
  - **独立 Debug 工具链 ([PR #2945](https://github.com/sipeed/picoclaw/pull/2945))**: `picoclaw-tracer` 虽暂为 Stale，但其“独立 UI + JSON-Lines 日志”的架构展示了社区构建开发者工具的强大能力，值得项目方重点关注与指导，以加速合并。

#### 7. 用户反馈摘要

- **Provider 适配是最大痛点**: 用户频繁遭遇各厂商 API 的特异性问题（如：Claude 的废弃参数、OpenAI 的工具类型、智谱的错误码），对 PicoClaw 的 Provider 抽象层提出了极高的兼容性要求。
- **升级体验至关重要**: 从 [Issue #2972](https://github.com/sipeed/picoclaw/issues/2972) 的反馈来看，用户对 v0.2.9 升级后的 Session 数据混乱感到不满。社区期望数据模型变更能实现“无感迁移”。
- **前端交互细节决定成败**: 无论是 Web UI 历史记录不全 ([#2796](https://github.com/sipeed/picoclaw/issues/2796))，还是缺少流式请求和完成信号，都证明用户正从简单测试转向深度的产品化使用，对前端体验的敏感度显著提高。

#### 8. 待处理积压

**提醒维护者关注以下长期未响应的关键 PR/Issue：**

- **高优先级 (Stale PRs 待审核)**:
  - **[PR #2951](https://github.com/sipeed/picoclaw/pull/2951)**: `fix web_search` (Stale 8天)。解决 OpenAI 生态碎片化问题，建议优先合并。
  - **[PR #2948](https://github.com/sipeed/picoclaw/pull/2948)**: `fix claude-opus-4-7 temperature` (Stale 8天)。修复新模型兼容性，避免新用户报错。
  - **[PR #2945](https://github.com/sipeed/picoclaw/pull/2945)**: `feat: picoclaw-tracer` (Stale 8天)。极具潜力的开发者调试工具，需要维护者给出明确反馈（合入/要求修改/拒绝）。
- **长期社区呼声**:
  - **[Issue #2404](https://github.com/sipeed/picoclaw/issues/2404)**: 流式请求支持（开放2个月）。评论多、需求明确，建议维护者给出官方设计文档或排入 Milestone，避免社区重复讨论。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的NanoClaw项目数据，为您生成了2026年6月3日的项目动态日报。

---

## NanoClaw 项目动态日报 | 2026-06-03

**项目名称:** NanoClaw (nanocoai/nanoclaw)

---

### 1. 今日速览

过去24小时内，NanoClaw项目开发活跃度处于**中等偏上**水平。尽管没有新版本发布，但**代码合并与修复活动频繁**，共有6个Pull Request被处理，其中4个已完成合并/关闭，涵盖了安全修复、功能特性及代码重构。Issues方面仅有1条新开议题，社区讨论热度相对较低。项目整体在持续完善核心功能（尤其是Codex Provider）、修复安全漏洞（防命令注入）及标准化运行时消息方面取得了实质进展。

### 2. 版本发布

无

### 3. 项目进展

今日有4个重要PR被合并或关闭，标志着项目在稳定性、安全性和功能性上迈出了坚实步伐：
- **安全性与健壮性增强**：PR [#2538](https://nanocoai/nanoclaw/pull/2538)（[closed]）修复了容器构建过程中的命令注入漏洞（CWE-78），通过对包名进行输入验证，提升了项目的基础安全性。PR [#2187](https://nanocoai/nanoclaw/pull/2187)（[open]）的修复逻辑似乎已被采纳或其关联issue得到解决，该修复旨在为CLI通道的`platformId`增加命名空间豁免，提升了平台ID处理的一致性。
- **核心功能迭代**：PR [#2674](https://nanocoai/nanoclaw/pull/2674)（[closed]）合并了`[codex]`分支上的运行时状态消息标准化工作，使得运行时状态显示更为统一，并增加了防止自循环的内部守卫，这对项目后期进行长任务管理至关重要。
- **新功能架构落地**：PR [#1193](https://nanocoai/nanoclaw/pull/1193)（[closed]）合并了期待已久的“主机端插件钩子系统”，允许通过在`plugins/`目录下放置模块来扩展`onStartup`和`onShutdown`逻辑。这为项目构建可插拔的生态奠定了基础，是一个重要的架构里程碑。
- **新技能集成**：PR [#2069](https://nanocoai/nanoclaw/pull/2069)（[closed]）引入了“Webchat v1”技能/通道，意味着项目现在拥有了一个完整的Web聊天界面集成能力，扩展了项目的终端用户触达范围。

### 4. 社区热点

今日社区讨论和互动相对冷清，没有产生高热度或大量评论的议题。唯一新开的Issue [#2673](https://nanocoai/nanoclaw/issue/2673) 提出了一个非标的“AI视频提示词”需求，描述了一个自动学生评分系统，该议题与项目核心（AI Agent框架）关联度较低，更像是用户对AI应用场景的探讨。总体而言，今日社区热点缺失，项目团队主要精力集中在代码的集成与修复上。

### 5. Bug 与稳定性

今日共处理了2个Bug相关的PR，按严重程度排列如下：
- **高危**：PR [#2538](https://nanocoai/nanoclaw/pull/2538) \- **OS命令注入漏洞**：在构建Docker镜像时，未经过滤的包名可能导致任意命令执行。该问题已通过输入验证得到修复，并已合并入主分支。
- **中危**：PR [#2672](https://nanocoai/nanoclaw/pull/2672) ( [open] ) \- **MCP兼容性与网络传输问题**：在`providers`分支上的Codex Provider存在两个兼容性问题：1) 与新版`McpServerConfig`联合类型不兼容；2) 在代理环境下仅支持HTTP传输。目前已有修复PR处于开放等待合并状态。
- **低危**：PR [#2187](https://nanocoai/nanoclaw/pull/2187) ( [open] ) \- **CLI平台ID不一致**：CLI通道的`platformId`与其他通道（如Signal、WhatsApp）行为不一致，可能导致配置问题。

### 6. 功能请求与路线图信号

- **插件化生态**：PR [#1193](https://nanocoai/nanoclaw/pull/1193) 的合并是一个强烈的路线图信号，表明NanoClaw正在从单一核心向**插件化平台**演进。未来用户可以期待更多围绕`onStartup`和`onShutdown`钩子的社区插件出现。
- **Web交互界面**：PR [#2069](https://nanocoai/nanoclaw/pull/2069) 的合并标志着官方Webchat通道的成型。这可能是项目路线图中面向非技术用户部署Agent的关键一步，未来可能会围绕Webchat开发更多管理功能。
- **Codex Provider升级**：PR [#2672](https://nanocoai/nanoclaw/pull/2672) 和 [#2674](https://nanocoai/nanoclaw/pull/2674) 表明团队正在积极重构和优化**Codex Provider**。对MCP联合类型及代理的支持，说明下一版本将更注重企业级部署和协议兼容性。

### 7. 用户反馈摘要

今日没有来自Issues评论区的直接用户反馈。但从PR的内容可以推断出一些用户痛点：
- **安全顾虑**：PR [#2538](https://nanocoai/nanoclaw/pull/2538) 的提交表明，有用户或开发者在使用容器部署代理时遇到了潜在的安全风险，因此提出了加固建议。
- **CLI体验一致性**：PR [#2187](https://nanocoai/nanoclaw/pull/2187) 的提出反映了用户在使用CLI接口时可能遇到与图形界面或其他通道不一致的ID行为，导致自动化脚本或配置出错。

### 8. 待处理积压

- **PR #2187**: [fix(platform-id): don't namespace CLI bare platform ids](https://nanocoai/nanoclaw/pull/2187)
  - **作者**: alex-shepel
  - **创建于**: 2026-05-02 | **更新于**: 2026-06-02
  - **状态**: 已开放超过1个月，等待合并。
  - **分析**：该PR修复了一个明确的Bug，且代码量小、逻辑清晰，长期未合并可能会影响CLI用户的使用体验。建议维护者优先审查并合并此修复。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报（2026-06-03）

**数据驱动 · 开源 AI Agent 个人助手领域**

---

## 1. 今日速览

过去 24 小时，项目活跃度高度聚焦于单一核心 Bug 的闭环——**PII 脱敏系统对 Agent 自身时间戳输出的误杀问题**。社区贡献者 @vernonstinebaker 在报出 Issue #944 后，立即提交了修复性 PR #945，展现了极高的社区自愈能力。目前 Bug 与修复方案均已就位，项目正处于“发现 -> 修复提案”的关键阶段，暂无新版本发布，项目健康度中等偏上，维护者的 Code Review 响应速度是下一阶段的关键变量。

---

## 2. 版本发布

**无**（过去 24 小时无新 Releases）。

---

## 3. 项目进展

**今日无 PR 合并或关闭**，但项目取得了一项具有里程碑意义的*进展*——问题修复方案已成功由社区提出并进入待审状态。

- **核心修复提案：** [PR #945 — fix(redaction): reject ISO date/time patterns as false-positive phone matches](nullclaw/nullclaw PR #945)
- **主要逻辑：** 在 `src/redaction.zig` 的 `matchPhone` 函数中引入 `isDateLike()` 守卫逻辑，当原始文本符合 ISO 日期/时间模式（YYYY-MM-DD hh 及 DD-MM-YYYY hh）时，直接拒绝匹配。
- **技术意义：** 该方案精准定位了根因——默认启用的 PII 脱敏器缺乏对 Agent 自身结构化输出的识别能力，使用简单的正则守卫即可阻断最大误报来源。

**项目整体向前迈进一步：** 从“用户遭遇生产问题”推进到“已验证的待合并修复代码”阶段。

---

## 4. 社区热点

**今日唯二活跃项：** [Issue #944](nullclaw/nullclaw Issue #944) 与 [PR #945](nullclaw/nullclaw PR #945)，二者形成完整的技术对话闭环。

**热度分析：**
- **响应速度极快：** Bug 报告与修复代码于同一日提交，说明 @vernonstinebaker 很可能是正在使用该功能的深度用户，在发现问题后当场定位源码并完成修补。
- **背后诉求：**
  1. **功能稳定性：** 用户无法接受默认开启的安全功能破坏 Agent 执行 `date` 等基础系统命令的能力。AI Agent 的 PII 脱敏应具备对“Agent 自身输出流”的豁免能力。
  2. **可预测性：** 用户期望 PII 脱敏的匹配规则是**可推导、可预期的**，而非无差别攻击所有数字序列。
  3. **默认值哲学：** `enable_pii_redaction` 默认为 `true`，但 `date` 输出中隐含的时间数据是否需要脱敏？社区潜在地在讨论默认值的谨慎度边界。

---

## 5. Bug 与稳定性

| 严重程度 | 报告链接 | 现象 | 影响范围 | Fix PR |
|---------|---------|------|---------|--------|
| ★★★★★ 严重 | [Issue #944](nullclaw/nullclaw Issue #944) | PII 脱敏器将系统时间戳（如 `2026-06-02 20:17`）误判为手机号（`PHONE_X`）并脱敏 | 所有默认配置实例；Agent 在获取时间时可能得到脱敏后占位符，导致下游任务逻辑异常 | [PR #945](nullclaw/nullclaw PR #945) |

**崩溃 / 回归情况：** 无（以本数据源捕获范围为准）。

**临时规避方案：**
在 PR #945 合并前，维护者或用户可手动关闭 `enable_pii_redaction = false` 或将 `appendDateTimeSection` 设为 `false`，但前者会关闭整个 PII 脱敏系统，属于一刀切的操作。

---

## 6. 功能请求与路线图信号

虽然 Issue #944 是一个 Bug 报告，但它暴露的缺口具有极强的**路线图信号意义**：

1. **PII 脱敏模块需要“输出源感知”。**
   当前脱敏模块是一个全局正则匹配器，Agent 执行的不同命令输出（系统命令 / 用户邮件 / 网页抓取）共享同一套规则。这种架构在面对确定性结构化输出时将反复产生误报。
   
2. **短期路线（下一版本 大概率纳入）：**
   PR #945 的 `isDateLike()` 守卫将被合并，解决当前最迫切的误报问题。这属于“止血”手段。

3. **中期演进方向（推测）：**
   引入**输出源标签（Output Source Tag）** 系统。在执行脱敏前检查输出来源类型（`syscall_stdout` vs `user_message` vs `retrieval_result`），对不同来源应用不同粒度的脱敏规则。例如系统命令输出仅脱敏 `EMAIL`、`SSN` 等高度敏感模式，豁免 `PHONE_X` 在时间戳中的匹配。

---

## 7. 用户反馈摘要

**数据来源：** [Issue #944](nullclaw/nullclaw Issue #944)

- **使用场景：** 用户运行 AI Agent，Agent 持执行 `date` 系统调用或使用内置时间戳上下文。
- **痛点描述：** “PII redactor ... is aggressively matching digit sequences in system date/time command output as phone numbers. ... shows redacted placeholders instead of the actual timestam...”
- **满意度分析：**
  - ❌ **不满意点：** 用户对一个“本该让系统更安全”的功能感到失望，因为它直接破坏了**基础可用性**。时间戳被脱敏意味着 Agent 失去了对当前时间的基本感知，这对于 scheduling、logging、time-aware reasoning 等场景是毁灭性的。
  - ✅ **积极贡献：** @vernonstinebaker 没有停留在抱怨层面，而是直接 Fork 仓库并提交高质量修复 PR，这种“发现问题并解决问题”的模式是项目社区成熟度高的典型标志。
- **社区情绪：** 务实且富有建设性。

---

## 8. 待处理积压

**当前项目没有长期未响应的积压 Issue/PR**。所有注意力集中在以下单一项：

| 优先级 | 链接 | 类型 | 等待原因 | 提醒 |
|--------|------|------|---------|------|
| 🔴 **最高** | [PR #945](nullclaw/nullclaw PR #945) | Fix Bugfix | 等待 Code Review 与 Merge | Bug 为默认触发，每多等待一天，影响的用户就增加一批。建议维护者在 24 小时内完成审核并发布 Hotfix 版本。 |

**建议：** 鉴于 Issue #944 的严重性（默认配置即可复现，且破坏核心功能），建议维护者将 PR #945 标记为 `critical`，优先分配 reviewer，合并后尽快打一个 `0.x.y` patch 版本，或直接在 `main` 分支上 cherry-pick 修复。

---

*报告生成完毕。数据来源：NullClaw GitHub 仓库公开动态（2026-06-02 至 2026-06-03）。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是基于你提供的 IronClaw GitHub 数据生成的 2026-06-03 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-03

## 1. 今日速览

- 项目活跃度极高，过去 24 小时内共有 **30 条 Issue 更新** 和 **50 条 PR 更新**，其中 **31 个 PR 已合并/关闭**，显示出强大的交付执行力。
- 核心研发焦点锁定在 **“Reborn”架构的系统性审计与稳定性加固**。贡献者 `henrypark133` 在一天之内密集提交了 **17 个深度架构 Audit Issue**（覆盖回环 Loop 和子代理 Subagent 的 L1-C6 全部领域），这是项目健康度自查和迈向生产就绪的重要信号。
- 集成层面进展显著，`serrrfirat` 主导修复了 **Notion/Gmail OAuth 流程、ChatGPT 空响应和本地开发环境** 等关键问题。
- 质量方面，QA 团队在 Qwen3.6 和 MiniMax 模型上报告了 **8 个 P2 级别的 Bug**，主要集中在 UI 渲染和工具调用校验。
- 今日 **无新版本发布**。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日项目向前迈进了重要一步，多个涉及核心架构、安全与集成的重量级 PR 被合并/关闭。

**核心架构推进：**
- **[重要] Trigger 主动调度能力落地：** 合并了 `#4318` (`Add trigger first-party capabilities`)，标志着平台从单纯“响应式”向“主动式”任务调度的关键跨越。同时，生命周期的最后拼图 `#4375` (`wire trigger poller lifecycle`) 已处于待合并状态。
- **[重要] Slack 渠道集成闭环：** `#4321` (`Slack Reborn final reply delivery`) 完成了 Slack 异步最终回复投递，打通了 Slack 集成的核心流程。
- **Codex ChatGPT 兼容性：** 合并了 `#4371` (`Fix Codex ChatGPT Reborn empty responses`)，修复了 GPT 模型返回空响应的阻塞性问题。
- **本地开发体验：** 合并了 `#4357` (`Fix local-dev Reborn memory mount`)，确保了本地开发环境的可用性。

**安全与健壮性：**
- **纵深防御：** `#4372` (`Zeroize HTTP credential carriers`) 确保 HTTP 凭据载体在释放时进行内存清零，是一次关键的纵深防御安全改进。
- **幂等性修复：** `#4370` (`Fix compaction summary retry idempotency`) 解决了 Reborn 压缩摘要的重试幂等问题，防止数据受损。
- **契约测试加固：** 合并了 `#4369` (`Harden skill context budget contract tests`)，强化了对技能上下文预算的测试保障。

**集成与工具迭代：**
- **OAuth 流程修复：** 密集合并了 `#4345`、`#4346`、`#4347`，全面修复了 Notion 和 Gmail 的 OAuth 授权流程健壮性。
- **工具易用性：** 合并了 `#4374` (`Accept memory_search query aliases`)，允许使用 `q` 等别名进行查询，提升了内置工具的可用性。

## 4. 社区热点

今日最强烈的社区信号来自核心团队发起的系统性架构审计，而非外部用户的简单提问。

- **深度 Audit Issue 集群（研发热点）：**
    `henrypark133` 发起了 **#4358-#4368 (L1-L11)** 和 **#4348-#4353 (C1-C6)** 共 17 个架构审计与改进 Issue。这并非普通 Bug 报告，而是一次自上而下的代码质量审查，覆盖了 Reborn 循环的预算精度、取消传播、持久化、子代理完成交付等核心领域。这反映了核心团队对 **“Reborn”架构达到生产级稳定性** 的极高追求。
    - 链接：`#4358` ~ `#4368` 系列，`#4348` ~ `#4353` 系列

- **用户侧核心痛点（高共鸣热点）：**
    - **`#4334` (Claude Opus 4.7/4.8 不可用)：** 用户 `DoradoPR` 报告因代码强行发送废弃的 `temperature` 参数，导致全新的 Claude 旗舰模型完全无法使用（400 错误）。这是近期影响最深远的用户侧 Bug，直接导致了高级用户的路径阻塞。
    - **`#4377` (`/model` 显示名与切换名不符)：** 用户 `sunglow666` 指出返回的显示名无法直接用于切换模型，这是一个简单但极其影响日常操作可用性的痛点。

- **长期待办关注：**
    - **`#3548` (`DISABLE_TOOLS_LIST flag`)：** 作为一项具有安全价值且 scope 广泛的 PR（已 open 超过 3 周），其在社区中的沉默值得关注，等待最终决策。
    - **`#3669` (engine v2 thread/response ids)：** 今日与其关联的 Issue `#4355` 被关闭，表明这个 Engine v2 的关键契约功能正在持续推进中。

## 5. Bug 与稳定性

今日报告的 Bug 数量较多，严重程度不一。QA 团队发现了大量影响核心聊天体验的问题，同时 CI 流水线出现失败。

**严重/阻断性 Bug：**
- **`#4108` (Nightly E2E 持续失败)：** CI 流水线处于失败状态，需优先调查根因。影响所有后续合并的集成验证。
- **`#4334` (Claude Opus 4.7/4.8 不可用)：** 用户无法使用当前最先进的 Claude 模型。**状态：等待修复**，无直接关联 PR。
- **`#4341` (思维链泄露)：** Qwen 模型的思考过程暴露给用户，属信息泄露。**状态：等待修复**。
- **`#4343` (MCP 集成不可用)：** 驱动故障导致 MCP 功能被承认但无法使用。**关联 PR：** `#4345`, `#4354`。

**高影响 Bug (P2 - QA 报告 Qwen3.6 / MiniMax-M2.7)：**
- `#4344` (消息回显)：模型在 loading 状态时异常镜像用户消息。
- `#4339` (工具调用被拒)：MiniMax 模型的合法工具调用被校验器错误拒绝。
- `#4342` (认证弹窗卡死)：刷新页面后认证弹窗不消失，阻塞所有操作。
- `#4340` (空白字段校验错误)：正常发送消息被表单校验误报。

**待合并的修复 PR：**
- `#4373` (XL)：修复子代理安全和能力门控，阻止安全绕过。
- `#4372` (L)：实现 HTTP 凭据内存清零。
- `#4370` (L)：修复压缩摘要重试幂等性。

## 6. 功能请求与路线图信号

- **明确路线图信号（即将落地）：**
    - **Reborn Trigger 主动调度：** 随着 `#4318` 的合并和 `#4375` 的完成，Trigger 功能已处于交付前夜，这将是 IronClaw 能力边界的一次重要拓展。
    - **WASM 工具集扩展 (GitHub)：** 虽然 `#3806` 今日关闭，但它属于 Reborn Lane 6 规划的一部分，证明 GitHub WASM 能力路径仍在研发管线中。
    - **渠道集成 (Slack)：** `#4321` 的推进表明继 Web 和 CLI 后，Slack 将成为下一个得到一等公民支持的渠道。

- **架构优化信号：**
    - 今日 `henrypark133` 提交的 **17 个 Audit Issue** 实际上是在为 **Reborn 架构的 1.0 稳定版** 设定基线，解决 `debug!` 宏污染热路径、错误的 Option 类型、缺少深度限制等长期存在的架构“坏味道”。

- **用户呼声（可能需要纳入路线图）：**
    - 用户 `DoradoPR` 在 `#4334` 中实际上提出了一个功能诉求：**“不要对不支持参数的模型强行发送参数”**。这可能意味着需要建立更精细的模型能力文档或 SDK 参数协商机制。

## 7. 用户反馈摘要

从今日的 Issue 报告中可以提炼出以下典型用户声音：

- **对“开箱即用”体验的苛求：** 用户 `sunglow666` (`#4377`) 和 `DoradoPR` (`#4334`) 的反馈直接指向了基础可用性。模型显示名无法切换、新模型无法使用，这类问题会严重打击用户信心。
- **复杂场景下稳定性不足：** QA 报告的一系列 Bug (如 `#4344` 消息回显，`#4342` 弹窗卡死) 虽然处于开发测试阶段，但反映了在处理多轮、认证、流式输出等复杂状态流时，前端和后端的协调仍有缺陷。
- **核心工程师的自我高标准：** 来自 `henrypark133` 的大量重构 Issue 表明，整个开发团队对于代码质量、审计完整性、类型安全有着极其苛刻的要求。例如 `#4368` 中提到的“六个 `Option<Arc<dyn T>>` 字段本应是非可选类型”即是典型。

## 8. 待处理积压

以下为需要维护者和社区密切关注的问题与 PR：

**急需响应的系统性问题：**
- **`#4108` (Nightly E2E Failed):** [链接](https://github.com/nearai/ironclaw/issues/4108) — CI 持续显红，严重阻碍开发节奏，建议立即分配人员排查。

**长期 Open 的高价值 PR：**
- **`#3548` (DISABLE_TOOLS_LIST flag):** [链接](https://github.com/nearai/ironclaw/pull/3548) — 一个具有极高安全价值的配置功能，但 scope 较大（横跨 agent, channel, wasm 等），需要决策是否接入或分阶段实施。
- **`#3669` (engine v2 expose channel-supplied thread/response ids):** [链接](https://github.com/nearai/ironclaw/pull/3669) — Engine v2 补齐工具回调上下文的关键 PR，需要尽快 Review 并推动合并。

**架构审计 Issue 跟踪：**
- 建议将 `henrypark133` 提出的 **17 个审计 Issue** (`#4348`-`#4353`, `#4358`-`#4368`) 统一纳入一个名为 `Reborn-Audit-Milestone` 的里程碑中，以便集中跟踪修复进度，避免这些深层重构任务被日常 Bug 淹没。这直接关系项目当前的健康度评估。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-06-03

---

## 1. 今日速览

过去 24 小时内，项目**未收到新 Issue**，但 **Pull Request 活动活跃**：共 6 个 PR 被合并/关闭，3 个 PR 处于待合并状态。修复集中在 **MCP 启动优化**、**MiniMax‑M3 图像输入支持**、**子代理批量删除**及**内部插件管理**，同时 **Artefacts 特性大合并**落地。整体来看，项目在**渲染器、主进程及插件生态**多线推进，维护节奏良好；但社区反馈（Issue）层面暂无新动向，活跃度主要由内部开发驱动。

| 指标 | 数量 |
|------|------|
| 新开 Issues | 0 |
| 关闭 Issues | 0 |
| 合并/关闭 PR | 6 |
| 待合并 PR | 3 |
| 新版本发布 | 0 |

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 6 个 PR 涵盖了多项功能改进与问题修复，项目在**协作能力、MCP 健壮性、模型兼容性及 UI 细节**上均有实质推进。

### 🎯 主要合并 PR

- **`#2096` – fix(plugins): hide internal OpenClaw plugins**  
  将 OpenClaw 内部/运行时自带的隐藏插件 ID 从插件管理列表中过滤掉，避免用户误操作。同时清理 `user_plugins` 记录中的隐藏 ID。  
  [netease-youdao/LobsterAI PR #2096](https://github.com/netease-youdao/LobsterAI/pull/2096)

- **`#2095` – fix(cowork): support subagent batch deletion**  
  让子代理会话纳入侧边栏批量选择，并统一走子代理删除路径；异步清理子代理网关转录文件，限制并发与重试次数，降低网关压力。  
  [netease-youdao/LobsterAI PR #2095](https://github.com/netease-youdao/LobsterAI/pull/2095)

- **`#2094` – fix: 优化分享成功弹窗的信息层级**  
  调整分享链接与分享码的展示样式，移除成功态下冗余的状态标识，统一信息块的视觉层级。  
  [netease-youdao/LobsterAI PR #2094](https://github.com/netease-youdao/LobsterAI/pull/2094)

- **`#2093` – fix: enable image input support for MiniMax-M3**  
  MiniMax‑M3 实际支持图像输入，但提供者硬编码为 `supportsImage: false`（从 M2.5/M2.7 继承），导致用户即使开启图像开关也无法使用。该 PR 移除硬编码限制，使配置正确生效。  
  [netease-youdao/LobsterAI PR #2093](https://github.com/netease-youdao/LobsterAI/pull/2093)

- **`#2092` – Feat/2026.5.28 artifacts**  
  大型特性合并，涉及渲染器、文档、主进程、插件等多区域。分支名暗示为 **Artefacts 功能**（可能是结果工件管理、生成物展示等）。  
  [netease-youdao/LobsterAI PR #2092](https://github.com/netease-youdao/LobsterAI/pull/2092)

- **`#2091` – feat(mcp): optimize npx MCP launch resolution & add first response timing logs**  
  - 对基于 `npx -y <package>@latest` 的 stdio MCP，前置执行包解析与本地安装，将启动命令转为稳定的 `node <absolute-bin-path>`，避免每次会话都重跑 npx 慢路径。  
  - 在 OpenClaw 适配器及主进程关键路径增加首次响应计时日志。  
  - 重启或进程中断残留的 `installing` 记录在配置同步时自动重试，防止永久卡住。  
  [netease-youdao/LobsterAI PR #2091](https://github.com/netease-youdao/LobsterAI/pull/2091)

### 📈 整体进展评估

今日合并的 PR 显示项目正在 **巩固基础设施**（MCP 启动、插件隐藏）、**增强协作**（子代理批量操作）以及 **扩展模型能力**（MiniMax‑M3 图像）。特别值得关注的是 Artefacts 特性合并，这可能是本周期内的重要功能里程碑。6 个 PR 在一天内关闭，反映出较高的评审与合并效率。

---

## 4. 社区热点

今日无 Issue 更新，所有 PR 也**未产生公开评论**（数据中评论项均为 `undefined`，推测无或未记录）。因此未出现高热度讨论。以下 PR 虽无评论，但因其内容或历史值得关注：

- **`#388` – feat: upgrade MiniMax default model to M3**  
  创建于 2026-03-12，已标记 `stale`，至今未合并。涉及 MiniMax 模型切换，是长期开放的增强请求。  
  [netease-youdao/LobsterAI PR #388](https://github.com/netease-youdao/LobsterAI/pull/388)

- **`#2092` – Feat/2026.5.28 artifacts**  
  大范围变更，虽无评论，但该特性很可能引发用户关注，未来有望带动讨论。

---

## 5. Bug 与稳定性

今日无新开 Issue，但从已合并的 PR 中可以归纳出修复的缺陷：

| 严重程度 | 问题描述 | 对应 PR |
|----------|----------|---------|
| **中** | MiniMax‑M3 图像输入因硬编码 `supportsImage: false` 无法启用 | `#2093` – 已合并 |
| **中** | OpenClaw 内部插件在管理列表中暴露，可能导致用户误禁 | `#2096` – 已合并 |
| **低** | 子代理无法批量删除，且删除后网关转录清理存在异步压力 | `#2095` – 已合并 |
| **低** | 分享成功弹窗信息层级冗余，影响视觉体验 | `#2094` – 已合并 |

未发现崩溃或回归类严重问题。

---

## 6. 功能请求与路线图信号

虽无直接 Issue 提出新需求，但今日合并的 PR 反映了团队**持续投入的方向**：

- **MCP 生态优化** (`#2091`)：将 `npx` 启动改为本地静默安装解析，显著提升 MCP 插件体验。这表明 MCP 是当前优先级较高的特性领域。
- **子代理协作用户体验** (`#2095`)：支持批量删除，说明团队正在完善子代理的批量管理能力，可能是协作功能规模化的一部分。
- **Artefacts 特性** (`#2092`)：这一大型合并预示着项目即将推出工件管理或生成物展示功能，属于路线图中的重要模块。
- **模型更新** (`#388`，开放中)：将 MiniMax 默认模型升级至 M3，并清理旧模型，符合持续跟进 AI 模型迭代的策略。

这些信号显示下一版本可能重点提升 **MCP 稳定性**、**协作/子代理多会话管理**以及 **Artefacts 展示能力**。

---

## 7. 用户反馈摘要

因今日无新 Issue，无法从评论中提炼直接的用户声音。不过可以从修复内容推测潜在痛点：

- 用户在使用 MiniMax‑M3 时可能发现无法上传图片，却不知道是代码限制所致（`#2093`）。
- 插件管理列表中混入不应展示的项目，可能造成困惑（`#2096`）。
- 子代理管理缺少批量操作，删除多个子代理需要逐个操作（`#2095`）。

这些均已在今日得到修复，预期相关用户的体验将有所改善。

---

## 8. 待处理积压

以下 PR 长期未合并，建议维护者重点关注：

| PR | 创建时间 | 最后更新 | 状态 | 摘要 | 链接 |
|----|----------|----------|------|------|------|
| `#388` | 2026-03-12 | 2026-06-02 | OPEN (stale) | 升级 MiniMax 默认模型至 M3，清理旧模型 | [PR #388](https://github.com/netease-youdao/LobsterAI/pull/388) |
| `#1277` | 2026-04-02 | 2026-06-02 | OPEN | 批量更新 electron 依赖（40.2.1 → 42.3.1）及 electron-builder | [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277) |
| `#1464` | 2026-04-04 | 2026-06-02 | OPEN | 为钉钉、飞书、QQ IM 多实例添加重复名称/机器人校验 | [PR #1464](https://github.com/netease-youdao/LobsterAI/pull/1464) |

- **`#388`** 涉及模型配置和 UI 列表，与已合并的 `#2093`（图像支持）有叠加，建议评估冲突后尽快决策。
- **`#1277`** 为数周前的依赖更新，可能存在冲突或需要重新 base。
- **`#1464`** 是 IM 多实例的体验改进，功能独立，适合快速合并。

---

**重要提示**：本日报完全基于提供的 GitHub 数据生成，未包含仓库内可能存在的其他活动（如代码评论、提交记录、未关联 Issue 的更新等）。建议结合更多数据源（如 commit 历史、CI 状态、项目看板）以获取完整图景。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 Moltis 项目数据生成的 2026-06-03 项目动态日报。

---

### Moltis 项目日报 (2026-06-03)

**数据来源：** github.com/moltis-org/moltis

---

#### 1. 今日速览

今日项目活跃度属于 **中等水平**。核心工作聚焦于稳定性优化，其中一项旨在为长期存在问题（工具反馈消息过长）提供解决方案的 PR 正在进行最终评估。社区方面，用户提出了一个关于**控制界面噪音**的功能请求，要求允许禁用工具状态通知。尽管没有新版本发布或 PR 合并，但项目在关键功能的稳定性和用户体验优化上均有明确进展，整体健康度良好。

#### 2. 版本发布

无

#### 3. 项目进展

今日无 PR 被合并或关闭。然而，一项重要的待合并 PR (**#1089**) 正在积极审查中，并获得了更新。该 PR 的实施将对项目的核心稳定性和 API 消费端的可靠性产生深远影响。

- **[PR #1089]** **关键稳定性增强：** **Cap persisted tool results before rehydration**
  - **关联链接：** [moltis-org/moltis PR #1089](https://github.com/moltis-org/moltis/pull/1089)
  - **进展分析：** 该 PR 在6月1日提出，并于今日(6月3日)进行了更新，表明维护者正在认真对待此项改动。它旨在解决一个核心问题：当工具调用返回的结果内容过大时，如何安全、高效地将其重注入（rehydrate）到与AI提供商绑定的对话历史（`ChatMessage`）中。这直接关系到会话上下文的处理效率、Token消耗以及是否会导致超出提供商上下文窗口限制的错误。PR 覆盖了普通聊天、流式聊天、压缩后重试、提示词检查等多种场景，显示作者考虑得非常周全。此项一旦合并，将是项目在稳定性方面的一大步。

#### 4. 社区热点

今日讨论集中在一个核心主题：**提升用户体验，减少信息冗余**。尽管均无评论，但Issue和PR共同指向了这个明确的用户诉求。

- **[Issue #1092] 功能请求：** **Add a config option to disable channel Activity log tool-status messages**
  - **关联链接：** [moltis-org/moltis Issue #1092](https://github.com/moltis-org/moltis/issues/1092)
  - **热点分析：** 该 Issue 直接反映了用户在使用 moltis 与 Telegram 等渠道集成时的真实痛点。当 AI Agent 调用工具时，频道中会回复一个“活动日志”块。在 Telegram 上，这会表现为一个可折叠的 HTML 块或一条独立的后续消息。对于不需要或认为此信息分散注意力的用户而言，这增加了界面噪音。此诉求背后体现了社区对**可控性**和**简洁界面**的强烈需求，用户希望能自主决定哪些信息需要展示，以实现更干净、更聚焦于核心对话的体验。
- **[PR #1089] 技术讨论焦点：** **Cap persisted tool results before rehydration**
  - **关联链接：** [moltis-org/moltis PR #1089](https://github.com/moltis-org/moltis/pull/1089)
  - **热点分析：** 虽然这是一个技术PR，但它与 #1092 形成了良好呼应。如果工具返回的结果过大，不仅日志中信息会过于冗余，甚至可能导致程序错误。该 PR 通过限制（Cap）结果大小，从技术层面解决了这个问题，确保系统稳定运行。社区中关注工具扩展性和稳定性的开发者将对此高度关注。

#### 5. Bug 与稳定性

今日未报告新的崩溃或回归类 Bug。不过，**PR #1089** 可以被视为一项应对已知或潜在稳定性问题的前瞻性修复。

- **关键稳定性修复（待合并）：** **[PR #1089] Cap persisted tool results before rehydration**
  - **严重程度：** **高**。工具调用是现代 AI Agent 的核心能力，其返回内容大小不可控。如果不进行限制，极易导致 API 调用因 Token 超限而失败，或占用大量内存影响程序性能，进而导致服务不稳定。
  - **关联链接：** [moltis-org/moltis PR #1089](https://github.com/moltis-org/moltis/pull/1089)

#### 6. 功能请求与路线图信号

今日最重要的路线图信号来自对“**用户界面可控性**”的追求。

- **新增功能请求：** **[Issue #1092] Add a config option to disable channel Activity log tool-status messages**
  - **关联链接：** [moltis-org/moltis Issue #1092](https://github.com/moltis-org/moltis/issues/1092)
  - **路线图信号：** 该请求非常具体且实现路径清晰（增加配置选项）。考虑到它来源于真实用户场景并能显著提升用户体验，有较大概率被认可并纳入后续版本的开发计划。它也可能与 **PR #1089** 形成互补，前者从“**是否展示**”层面优化，后者从“**展示什么**”的源头进行控制。两项工作都指向了让工具交互更优雅的目标。

#### 7. 用户反馈摘要

今日主要收集到以下用户痛点与场景：

- **痛点：界面信息过载。** (源自 [Issue #1092](https://github.com/moltis-org/moltis/issues/1092))
  - **场景：** 用户在 Telegram 等聊天频道中与 AI Agent 交互。每当 Agent 使用工具时，都会产生一条包含详细状态的“活动日志”消息。
  - **不满意的地方：** 这种日志消息被认为是非必要的“信息噪音”，尤其是在主回复已经通过流式编辑等方式呈现后，额外的消息会破坏聊天的连贯性和简洁性。

#### 8. 待处理积压

今日最关键且待处理的事项是 **PR #1089**，需要维护者尽快审查并决定是否合并。

- **待合并 PR：** **[PR #1089] Cap persisted tool results before rehydration**
  - **重要性：** **高**。如前述，此改动影响系统核心稳定性和资源消耗。
  - **状态：** 6月1日创建，1日更新，仍处于开放待合并状态。
  - **关联链接：** [moltis-org/moltis PR #1089](https://github.com/moltis-org/moltis/pull/1089)
  - **提醒：** 请维护者重点关注此 PR。持续的悬而未决可能会导致社区中遭遇相关问题的用户产生困惑。建议尽快完成 Code Review，确认无副作用后合并，并考虑是否随之下一个 Patch 版本发布。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 | 2026-06-03

---

## 1. 今日速览

CoPaw（QwenPaw）项目在过去24小时内维持了极高的迭代强度和社区活跃度，共产生 **36 条 Issue 更新**（16 条新开/活跃，20 条已关闭）与 **31 条 PR 动态**（21 条待合并，10 条已合并/关闭）。项目团队响应迅速，社区研究者集中报告的 7 项安全漏洞已全部完成受理关闭。虽然本日无正式版本发布，但 `v1.1.11b1` 版本号已打标，预示新补丁版本即将推出。用户对于 **Windows 桌面端体验、多频道稳定性及上下文管理** 的反馈成为当前最集中的痛点信号。

---

## 2. 版本发布

**无新版本发布。**

预发布标签 `v1.1.11b1` 已发布（[PR #4907](https://github.com/agentscope-ai/QwenPaw/pull/4907)），表明项目已完成一轮密集修复，正向社区推送 Beta 版本。

---

## 3. 项目进展

**已合并/关闭的重要 PR：**

- **频道修复系列**：`fix(channel): cron messages fail to deliver to wechat/wecom`（[PR #4883](https://github.com/agentscope-ai/QwenPaw/pull/4883)）解决了定时任务无法推送至微信/企微的根源性问题，关联 Issue #4878 一并关闭。`fix(wecom): resolve session_id from authenticated sender_id`（[PR #4850](https://github.com/agentscope-ai/QwenPaw/pull/4850)）修复了企微频道的会话隔离漏洞。

- **Windows 体验优化**：`fix(coding-mode): support browsing all drives on Windows`（[PR #4906](https://github.com/agentscope-ai/QwenPaw/pull/4906)）修复了 Windows 文件浏览器锁定在 C 盘根目录的长期问题。`optimize Windows startup`（[PR #4772](https://github.com/agentscope-ai/QwenPaw/pull/4772)）通过懒加载与渐进式初始化优化了 Windows 启动性能（First-time Contributor）。

- **后端兼容性**：`feat(providers): route non-standard generate_kwargs into extra_body`（[PR #4689](https://github.com/agentscope-ai/QwenPaw/pull/4689)）解决了 DashScope 等厂商非标准参数被 OpenAI SDK 静默丢弃的问题。

**正在审查中的重大 PR：**

- **破坏性变更** `refactor: migrate agentscope from 1.x to 2.0.0`（[PR #4846](https://github.com/agentscope-ai/QwenPaw/pull/4846)）正在评审中，底层架构迁移将影响全链路。
- **插件系统扩展**：提示词注册表（[PR #4804](https://github.com/agentscope-ai/QwenPaw/pull/4804)）、卸载钩子（[PR #4794](https://github.com/agentscope-ai/QwenPaw/pull/4794)）均在推进中。
- **沙箱后端集成** E2B / AgentScope（[PR #2275](https://github.com/agentscope-ai/QwenPaw/pull/2275)）提供了跨平台的沙箱抽象。
- **技能自进化** `enhanced make-skill flow`（[PR #4857](https://github.com/agentscope-ai/QwenPaw/pull/4857)）支持后台异步技能创建。

---

## 4. 社区热点

**#1 安全审计热潮**
社区安全研究员 `@YLChen-007` 在 06-02 集中提交了 7 个安全漏洞（[#4908](https://github.com/agentscope-ai/QwenPaw/issues/4908) ~ [#4914](https://github.com/agentscope-ai/QwenPaw/issues/4914)），覆盖未授权接口访问（语言设置 API）、ToolGuard 旁路绕过、Session ID 幻象导致聊天创建不可用、MCP 验证规则 500 错误、时区别名解析 500、`system_prompt_files` 路径遍历、工作区导出泄露渠道密钥。项目组反应迅速，所有 7 个 Issue 在 24 小时内关闭。另有用户询问如何在 ASRC 上报漏洞（[#4863](https://github.com/agentscope-ai/QwenPaw/issues/4863)），社区安全意识正在形成。

**#2 频道接入稳定性**
`定时任务微信推送失败`（[#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)，5 条评论）和 `Custom channel 保存设置断连`（[#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877)，3 条评论）成为渠道开发者讨论焦点。用户对高可靠的消息投递和配置热加载有明确刚需。

**#3 元宝频道 Proto 文件缺失**
`Yuanbao channel missing proto files`（[#4898](https://github.com/agentscope-ai/QwenPaw/issues/4898)、[#4890](https://github.com/agentscope-ai/QwenPaw/issues/4890)）被多位用户报告，确认是 v1.1.10 发行包遗漏了 protobuf schema 文件，导致 WebSocket 认证陷入无限重连循环。社区用户协助排查，已确认为打包缺失而非配置问题。

---

## 5. Bug 与稳定性

### 紧急/严重 Bug（无关联修复 PR）

| Issue | 严重程度 | 问题描述 |
|---|---|---|
| [#4922](https://github.com/agentscope-ai/QwenPaw/issues/4922) | 🔴 严重 | 一次图片路径错误导致 **所有后续对话均报 `PermissionError`**，会话污染问题，用户完全无法使用 |
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | 🔴 严重 | `browser_use` 工具在 Windows 10 上完全不可用（managed CDP 超时 + Chrome/Edge 闪退），三种尝试均失败 |
| [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 🔴 严重 | 上下文压缩自动触发后因旧格式 `file block` 导致 `'str' object has no attribute 'get'`，历史消息无法正常压缩 |
| [#4837](https://github.com/agentscope-ai/QwenPaw/issues/4837) | 🟠 高 | v1.1.9 升级后频繁出现系统级 fallback 回复"无法处理您的问题"，非 Agent 真实回复，频次明显升高 |

### 高/中优先级 Bug

| Issue | 问题描述 | 关联修复 |
|---|---|---|
| [#4918](https://github.com/agentscope-ai/QwenPaw/issues/4918) | MCP 工具名含 `.` 时 `gpt-5.5` 因 `name` 校验失败无法调用 | 无 |
| [#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877) | Custom channel 保存设置时停止监听，需二次保存才能恢复 | 无 |
| [#4903](https://github.com/agentscope-ai/QwenPaw/issues/4903) | WebUI 切换聊天时 loading 状态异常，无法停止或随滚动闪烁 | 无 |
| [#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923) | `spawn_subagent` 启动的子任务执行中完全不可见，完成后内容不完整 | 无 |
| [#4920](https://github.com/agentscope-ai/QwenPaw/issues/4920) | 输入框有内容时按键盘上键返回上一条消息而非回到行首 | 无 |
| [#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917) | 聊天数据较多时从其他按钮切换回聊天界面卡顿 | 无 |

### 已确认/已修复的安全漏洞

| Issue | 漏洞类型 | 状态 |
|---|---|---|
| [#4908](https://github.com/agentscope-ai/QwenPaw/issues/4908) | 未授权修改全局语言设置 | 已关闭 |
| [#4909](https://github.com/agentscope-ai/QwenPaw/issues/4909) | ToolGuard 旁路绕过 | 已关闭 |
| [#4910](https://github.com/agentscope-ai/QwenPaw/issues/4910) | Session ID 幻象导致持久性创建失败 | 已关闭 |
| [#4911](https://github.com/agentscope-ai/QwenPaw/issues/4911) | MCP 配置 API 返回 500 而非 422 | 已关闭 |
| [#4912](https://github.com/agentscope-ai/QwenPaw/issues/4912) | Cron 时区别名解析 500 | 已关闭 |
| [#4913](https://github.com/agentscope-ai/QwenPaw/issues/4913) | `system_prompt_files` 路径遍历导致文件外泄 | 已关闭 |
| [#4914](https://github.com/agentscope-ai/QwenPaw/issues/4914) | 工作区导出泄露渠道密钥 | 已关闭 |

---

## 6. 功能请求与路线图信号

**上下文窗口治理（Core Roadmap 强信号）**
- **Lossless Context Compression**（[#4551](https://github.com/agentscope-ai/QwenPaw/issues/4551)，2026-05-20 开启，3 条评论）提出了 DAG 摘要 + CJK Token 修复方案，非常系统和深入。
- **工具定义按需加载**（[#4836](https://github.com/agentscope-ai/QwenPaw/issues/4836)）预计可减少初始上下文 55-65% 的 Token 开销。
- **图片不应直接载入上下文窗口**（[#4921](https://github.com/agentscope-ai/QwenPaw/issues/4921)）与前述问题共同指向同一核心痛点。
- 关联 PR `feat(runner): detect context length errors`（[PR #760](https://github.com/agentscope-ai/QwenPaw/pull/760)）已存在但长期待审。

**Agent 可组合性与多模型协作**
- `spawn_subagent` 多模型选择（[#4901](https://github.com/agentscope-ai/QwenPaw/issues/4901)）希望子任务可指定轻量模型以节约成本，类似 Claude Code 的 Haiku/Opus 调度模式。
- 子任务运行时可见性需求（[#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923)）是协作场景的配套诉求。

**Windows 桌面端体验**
- 文件上传大小不限制（[#4893](https://github.com/agentscope-ai/QwenPaw/issues/4893)）
- 多文件拖拽上传（[#4894](https://github.com/agentscope-ai/QwenPaw/issues/4894)）
- 侧边栏 UI 精简（[#4904](https://github.com/agentscope-ai/QwenPaw/issues/4904)）对比 Codex/Claude Desktop 提出优化思路。

---

## 7. 用户反馈摘要

**最深痛的痛点**
- "不管怎么问都报这个错"（[#4922](https://github.com/agentscope-ai/QwenPaw/issues/4922)）：一次工具调用错误 `PermissionError` 污染了整段会话，用户清空会话、AI 修复均无效，情绪表达包含明显的挫败和紧迫感。
- "侧边菜单太复杂，用户很少用到它们……但聊天会话反而需要多一次点击"（[#4904](https://github.com/agentscope-ai/QwenPaw/issues/4904)）：来自跨产品对比的深度 UI/UX 反馈，具有高参考价值。
- "最终结果无法推送到微信……日志反复出现 `ret=-3`"（[#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)）：用户完整复现了环境、日志和根因分析，技术素养扎实。

**积极反馈信号**
- 社区自发形成「安全研究员」角色（@YLChen-007），且有新人申请加入漏洞报告渠道（[#4863](https://github.com/agentscope-ai/QwenPaw/issues/4863)）。
- 大量 Issue 带有完整日志、根因代码定位和修复建议（如 #4878 给出 `channel.py` 具体行号，#4551 给出精确 Token 计算）。
- Windows 用户持续高频提出桌面端体验优化，证明桌面版激活用户比例在提升。

---

## 8. 待处理积压

### 长期未响应的重要 Feature Request

| Issue | 创建时间 | 说明 |
|---|---|---|
| [#4551](https://github.com/agentscope-ai/QwenPaw/issues/4551) | 2026-05-20 | Lossless Context Compression（DAG 摘要），高质量系统方案，无官方回复 |
| [#4836](https://github.com/agentscope-ai/QwenPaw/issues/4836) | 2026-05-31 | 工具定义按需加载，减少 55-65% Token，无官方回复 |

### 长期开放的重要 PR

| PR | 创建时间 | 说明 |
|---|---|---|
| [#2275](https://github.com/agentscope-ai/QwenPaw/pull/2275) | 2026-03-25 | E2B / AgentScope 沙箱后端抽象，影响力大，仍为 Open |
| [#760](https://github.com/agentscope-ai/QwenPaw/pull/760) | 2026-03-05 | 上下文长度错误检测 + 自动 /compact 提示，配合 #4551 治理上下文 |
| [#1086](https://github.com/agentscope-ai/QwenPaw/pull/1086) | 2026-03-09 | 修复内存压缩时缺少本地媒体文件的 TypeError，06-03 有更新 |

### 需紧急关注的严重 Bug（无关联修复 PR）

| Issue | 创建时间 | 说明 |
|---|---|---|
| [#4837](https://github.com/agentscope-ai/QwenPaw/issues/4837) | 2026-05-31 | v1.1.9 回归：频繁系统级 fallback 回复 |
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | 2026-06-02 | **browser_use 核心工具在 Windows 上完全不可用** |
| [#4922](https://github.com/agentscope-ai/QwenPaw/issues/4922) | 2026-06-03 | **会话污染 Bug 导致用户完全无法使用** |
| [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 2026-06-03 | **上下文压缩崩溃，会话无法压缩历史** |

---

**总结：** 2026-06-03 的 CoPaw 项目处于高强度的轮转维护与功能推进并行阶段。安全审计与渠道兼容性是当前处理热点，上下文窗口治理是社区呼唤最强烈的长期路线图方向。`browser_use` 不可用和会话污染 Bug 作为两个阻塞级问题，建议维护团队优先投入资源排查。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是基于您提供的 GitHub 数据生成的 ZeroClaw 项目日报。

---

# ZeroClaw 项目动态日报｜2026-06-03

### 1. 今日速览

2026年6月3日，ZeroClaw 项目迎来了里程碑式的大版本更新——**v0.8.0-beta-2** 正式发布，这是自 v0.7.5 以来规模最大的一次版本迭代。其核心亮点是全新的终端 UI **zerocode** 及多智能体运行时的发布。过去 24 小时内，项目活跃度极高，共有 50 条 Issue 更新（关闭 33 条），以及 50 条 PR 更新（合并/关闭 47 条），展现出了发布后极高的集成效率与社区响应速度。整体来看，项目健康度极佳，Bug 修复循环十分迅速。

### 2. 版本发布

- **v0.8.0-beta-2** [发布说明](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.8.0-beta-2)
    - **更新内容**：该版本是 v0.8.0 系列的第二个 Beta 版，也是截至目前功能最丰富的发布。
        - **zerocode**：基于 Ratatui 构建的全功能终端 UI，让用户无需离开终端即可对话、监控及操作 Agent。支持流式显示、工具调用、审批提示等，标志着 ZeroClaw 正式拥有了官方第一方 TUI 客户端。
        - **多智能体运行时**：伴随 zerocode 发布，提供了对多智能体协作运行时的底层支持。
    - **破坏性变更**：根据发布日志，该版本未标记明确的破坏性变更。但作为 Beta 版本，建议用户在升级后全面测试现有配置、Provider 及技能（Skill）的工作流兼容性。
    - **迁移注意事项**：由于引入了全新的 TUI 客户端和多智能体运行时，依赖此版本构建上层应用的开发者需关注 `crates/zeroclaw-tui` 迁移至 `apps/zerocode` 的路径变化。

### 3. 项目进展

过去 24 小时共有 **47 个 PR** 被合并，项目在以下方面取得了显著推进：

- **文档基建升级**：PR [#7023](https://github.com/zeroclaw-labs/zeroclaw/pull/7023) 实现了版本化文档部署及版本选择器。PR [#7124](https://github.com/zeroclaw-labs/zeroclaw/pull/7124) 修复了多版本构建时共享资源被覆写的问题，确保用户在不同版本间切换时不会出现页面错乱。
- **技能生态打磨**：
    - PR [#5874](https://github.com/zeroclaw-labs/zeroclaw/pull/5874) 合入了 Hermes 风格的 `SKILL.md` 自动生成功能（LLM Reflection）。
    - PR [#5420](https://github.com/zeroclaw-labs/zeroclaw/pull/5420) 添加了技能白名单过滤与 LLM 辅助的技能失败优化机制。
    - PR [#6072](https://github.com/zeroclaw-labs/zeroclaw/pull/6072) 优化了技能注册的日志记录，从仅报错改为正向成功日志。
- **核心稳定性修复**：
    - 修复了 Cron Agent 输出 `<tool_call>` 原始载荷的问题（[#6026](https://github.com/zeroclaw-labs/zeroclaw/pull/6026)）。
    - 修复了辅助 LLM 调用未能正确处理 `[IMAGE:]` 多模态标记的问题（[#6114](https://github.com/zeroclaw-labs/zeroclaw/pull/6114)）。
    - 修复了 `SKILL.toml` 中 `timeout_secs` 配置被静默忽略的问题（[#6054](https://github.com/zeroclaw-labs/zeroclaw/pull/6054)）。
- **观测性增强**：PR [#6009](https://github.com/zeroclaw-labs/zeroclaw/pull/6009) 丰富了 OpenTelemetry 工具调用 Span 的语义属性。

### 4. 社区热点

昨日社区讨论最活跃的议题主要围绕配置体验与第三方兼容性：

1.  **[#6123] 新用户安装配置报错（已关闭，18条评论）**：
    [Issue #6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)
    用户在 LXC 容器中全新安装后，Onboarding 流程因 `default_model` 问题失败。**这凸显了 Onboarding 流程在当前复杂网络/容器环境下存在盲区，是用户体验的第一道门槛**。尽管已关闭，但值得持续监控。

2.  **[#5722] 默认沙盒封锁 Python 技能（已关闭，6条评论）**：
    [Issue #5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722)
    知名用户 Jason Perlow 详细阐述了默认沙盒（ephemeral Alpine、无网、只读根目录）导致 Python/R/Node 技能全部失效的问题。**此 Issue 引发了关于沙盒策略与开发效率平衡的深度讨论**，最终催生出官方 Python 技能快速入门文档（PR [#6057](https://github.com/zeroclaw-labs/zeroclaw/pull/6057)），是高质量社区驱动的典范。

3.  **[#5962] Ollama Provider 工具调用崩溃（开放中，6条评论）**：
    [Issue #5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)
    用户在调用工具时 Ollama Provider 报错导致会话阻塞。**这是目前本地模型用户最核心的痛点**，评论区持续关注进展，期望尽快修复。

### 5. Bug 与稳定性

过去 24 小时大量高严重性 Bug 被快速关闭，修复效率极高。

- **高严重性（已修复/关闭）**：
    - **Bubblewrap 在 Fedora 43 上崩溃**：`sysinfo` 线程 panic 导致无法启动（[#6878](https://github.com/zeroclaw-labs/zeroclaw/issues/6878)）。风险高，已关闭。
    - **技能安装时 Reqwest panic**：`reqwest::blocking` 在 `#[tokio::main]` 上下文中被丢弃导致崩溃（[#6681](https://github.com/zeroclaw-labs/zeroclaw/issues/6681)）。风险高，已关闭。
    - **Web UI 工具审批绕过**：WebSocket 路径未经过 `ApprovalManager`，导致监管模式失效（[#6207](https://github.com/zeroclaw-labs/zeroclaw/issues/6207)）。风险高，已关闭。
    - **推理内容丢失**：上下文压缩器丢弃了 DeepSeek 等 Provider 依赖的 `reasoning_content`（[#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)）。风险高，已关闭。
    - **WhatsApp 渠道通信中断**：因 Meta 服务端协议升级导致信道不工作（[#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)）。风险中，已关闭。

- **高严重性（持续跟踪中）**：
    - **Ollama Provider 工具调用失败**（[#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)）：标记为 `P1`，`in-progress`。阻塞大量开源模型用户，是当前最关键的稳定性遗留问题。

### 6. 功能请求与路线图信号

- **已纳入当前版本或即将推进**：
    - **zerocode TUI**：核心 Tracker [#6824](https://github.com/zeroclaw-labs/zeroclaw/issues/6824) 标志着 TUI 体验已成为一等公民。对应的代码结构重构 PR [#6821](https://github.com/zeroclaw-labs/zeroclaw/pull/6821) 已合并。
    - **ACP 协议扩展**：PR [#6820](https://github.com/zeroclaw-labs/zeroclaw/issues/6820) 增加了 Diff/文件提案类型支持，增强了 TUI 和 Web 客户端在代码编辑场景下的协作能力，已在 v0.8.0-beta-2 中落地。
- **待进一步评估（路线图信号）**：
    - **`.well-known` URI 技能安装**（[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)）：该需求依赖外部行业标准（Agent Skills group）的演进，长期未闭。随着技能生态的地位提升，预计在后续版本（v0.9+）中会结合标准成熟度重启推进。
    - **Gateway 静默降级加固**（[#6127](https://github.com/zeroclaw-labs/zeroclaw/issues/6127)）：Security P1，是核心链路的安全强化项，预计会在小版本中优先解决。

### 7. 用户反馈摘要

- **配置复杂度吐槽**：新用户（[#6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)）在非标准环境（LXC 跨主机 Ollama）中遭遇 Onboarding 失败，表明当前引导流程在处理分布式/容器化环境时的鲁棒性有待加强。
- **深度用户的技术期许与贡献**：用户 **perlowja** 深入参与了沙盒、审计、Python 技能等多个议题，提供了大量技术细节。这表明 ZeroClaw 正在吸引专业开发者，他们对“开箱即用”的脚本运行环境和安全策略有着极高的要求。
- **对维护响应速度的认可**：大量严重影响使用的 Bug（如 WhatsApp 信道、Bubblewrap 崩溃、审批绕过等）均在 24 小时内关闭，虽然多数评论简短，但 Issue 快速关闭的状态本身就反映出了社区对项目维护者高效响应的满意。
- **本地模型用户的持续焦虑**：Ollama Provider 的 Bug（[#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)）长期未根治，是目前社区中最大的负面情绪点，直接限制了新 TUI 客户端在本地推理场景下的可用性。

### 8. 待处理积压

以下为长期未完全解决或优先级较高的遗留问题，提醒维护团队关注：

- **[P1, 开放中, in-progress] `#5962` Ollama Provider 工具调用失败**：
    [Issue #5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)
    自 2026-04-21 上报至今已超过 40 天，始终是本地模型用户的使用瓶颈。
- **[P1, 开放中, accepted] `#6120` Onboarding 指定 Codex 却要求 OpenAI API Key**：
    [Issue #6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120)
    影响了想要连接 Codex 订阅的用户，等待方案落地。
- **[P1, 开放中, in-progress] `#5155` 委托 Agent 忽略 Prompt 注入模式**：
    [Issue #5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155)
    自 2026-03-29 上报至今超过 2 个月。架构性缺陷，导致多智能体协作时的技能注入控制失效。
- **[Enhancement, 开放中] `#4853` 安装技能集成 `.well-known` URI**：
    [Issue #4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)
    搁置超过 70 天，依赖外部标准化进度，属于生态扩展的长期痛点。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*