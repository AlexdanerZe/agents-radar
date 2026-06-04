# OpenClaw 生态日报 2026-06-04

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-04 03:41 UTC

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

# OpenClaw 项目动态日报 | 2026-06-04

## 1. 今日速览
OpenClaw 项目过去 24 小时内呈现极高度活跃：**500 条 Issue** 与 **500 个 PR** 被更新，**3 个新版本**发布（v2026.6.1 正式版及两个 Beta 版）。尽管近期更新在 Codex、Mattermost、Discord 等通道引入了 P1 级回归问题，项目维护团队响应迅速，**96 个 PR 已合并/关闭**，体现出紧密的迭代节奏与较高的社区参与度。项目整体处于架构升级与稳定性攻坚并行的阶段。

## 2. 版本发布
今日共发布 3 个版本，均为 v2026.6.x 系列。

### v2026.6.2-beta.1 ⚠️
- **核心更新：** **安全与安装策略重构。** 插件和技能的安装流程从旧式的 "dangerous-code scanner" 路径全面迁移至新的 **Operator Install Policy**。配套的 `doctor` 命令、CLI、ClawHub 及故障排查界面均已重构以适配新策略。（[#89516](https://github.com/openclaw/openclaw/issues/89516)）
- **⚠️ 破坏性变更：** 如果您的组织依赖旧的自定义安全扫描钩子或 `claw-scan` 机制，需迁移至新的 Operator Policy 接口。
- **迁移注意事项：** 建议用户在 Beta 环境独立沙箱中验证新的插件安装流程，特别是涉及自建插件市场的场景。

### v2026.6.1 (正式版) / v2026.6.1-beta.3
- **核心更新：** 改善 Agent 与 CLI 运行时稳定性——中断工具调用恢复、旧会话绑定清理、压缩交接和媒体投递重试。增强 Telegram、WhatsApp、iMessage、Slack 等通道的投递可靠性。（[#88129](https://github.com/openclaw/openclaw/issues/88129) 等）

## 3. 项目进展

### 已关闭/合并的重要修复
- **Windows UI 回归（✅ 已修复）：** `#67035` 输入文本被吞、流式回复不可见问题已关闭。
- **WebChat 重复回复（✅ 已修复）：** `#71992` 控制台 WebChat 每条回复出现两次的问题已关闭。
- **队列模式修复（✅ 已修复）：** `#67793` `queue.mode "collect"` 未按 `debounceMs` 进行消息批处理的问题已关闭。
- **Auth 路由安全（✅ 已修复）：** `#67423` 修复了身份验证路由在多 Provider 配置拆分时选择了错误的 `apiKey`。
- **Windows 命令损坏（✅ 已修复）：** `#48780` `exec()` 和 `read()` 工具调用被错误追加 `</arg_value>>` 后缀的问题已关闭。
- **WebSocket 稳定性（✅ 已修复）：** `#89041` 修复 ws 8.21.0 引入的 `maxBufferedChunks` 限制导致的 Discord 断开问题。
- **WhatsApp 通道（✅ 已合并）：** `#87965` 热重载时禁用账户无法正常下线；`#90123` 自动回复中 `message_tool only` 模式的投递确认计数问题。

### 核心待合并 PR
- **多槽位记忆架构 (Multi-slot Memory，👀 Ready for maintainer look）：** `#88504` 新增 `memory.recall`、`memory.compaction`、`memory.capture`、`memory.reflect` 标准槽位，允许多个记忆插件按职能协同工作，是记忆系统架构的重大升级。
- **实时 Provider 模型目录（📣 Needs proof）：** `#90029` 支持从 Provider 实时获取 `/models` 列表，为动态模型路由提供基础设施支持。
- **数学公式渲染（📣 Needs proof）：** `#87568` 新增 KaTeX 渲染支持，社区呼声较高。

## 4. 社区热点

### 🔥 技术方案纵深讨论
- **[#88838](https://github.com/openclaw/openclaw/issues/88838)（评论 17）** 围绕如何通过 **Branch-by-Abstraction** 模式以渐进式 PR 替代一次性重写，将核心会话/转录运行时状态迁移到 SQLite。这是未来数据持久化架构的重大升级方向，社区贡献者深度参与了技术路径选型。

### 🔥 核心回归引爆讨论
- **[#88312](https://github.com/openclaw/openclaw/issues/88312)（评论 12，👍 2）** P1 级回归：Codex app-server 多工具 Agent 调用在 v2026.5.27 可靠地失败（"Codex stopped before confirming"），而 v2026.5.26 正常。该问题曾因 [#85107](https://github.com/openclaw/openclaw/pull/85107) 修复但又复现，用户 `yair` 提供了详尽对比。**当前无关联修复 PR。**
- **[#65161](https://github.com/openclaw/openclaw/issues/65161)（评论 14）** P2 级：心跳隔离模式下节奏停滞、错误事件标签、State Writer 疑似缺失。用户 `A1fred-AI` 提供了高度专业的根因分析报告。

## 5. Bug 与稳定性

### P1 级严重问题 / 回归（待修复）
| Issue | 问题描述 | 关联 Fix PR |
|-------|---------|------------|
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex 模块调用停滞（Regression of #84076） | ❌ 无 |
| [#68113](https://github.com/openclaw/openclaw/issues/68113) | Mattermost 斜杠命令返回 503（Regression） | ❌ 无 |
| [#81484](https://github.com/openclaw/openclaw/issues/81484) | Discord 频道回复负载异常、重试循环（Regression） | ❌ 无 |
| [#86214](https://github.com/openclaw/openclaw/issues/86214) | Codex 客户端大 `logs_2.sqlite` 导致中途关闭 | ❌ 无 |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新僵局，Agent 中断数小时无告警 | ❌ 无 |
| [#64810](https://github.com/openclaw/openclaw/issues/64810) | Telegram 主题会话心跳中断进行中回复 | ❌ 无 |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) | 高 `reserveTokensFloor` 下仍硬重置循环（自 04-08） | ❌ 无 |

### 已有 Fix PR 的 Bug（今日新提交）
| Issue | 问题描述 | Fix PR |
|-------|---------|--------|
| [#89473](https://github.com/openclaw/openclaw/issues/89473) | 聊天回复中未剥离 `reasoning` 标签 | [#90051](https://github.com/openclaw/openclaw/pull/90051) |
| [#90088](https://github.com/openclaw/openclaw/issues/90088) | 静态目录缺少 Claude Haiku 4.5 | [#90110](https://github.com/openclaw/openclaw/pull/90110) |
| [#89953](https://github.com/openclaw/openclaw/issues/89953) | Telegram 发送卡死后重新连接排水不当 | [#90066](https://github.com/openclaw/openclaw/pull/90066) |
| [#90015](https://github.com/openclaw/openclaw/issues/90015) | DSML 恢复缓冲区无限增长，内存溢出风险 | [#86637](https://github.com/openclaw/openclaw/pull/86637) |
| Compaction 遗留 | 旧 `thinkingSignature` 压缩后签名校验失败 | [#90137](https://github.com/openclaw/openclaw/pull/90137) |

### 长期存在的顽固 Bug（积压）
- **`#63998`** P1: Session Transcript 崩溃重启死亡螺旋，逐次膨胀直至 Gateway OOM（自 04-10）。
- **`#66561`** P1: SSE 流已开始后被 OpenClaw 本地中止，伪装成 408 超时抛给用户。
- **`#69118`** P1: Claude CLI 在群组通道每轮重置，`extraSystemPromptHash` 持续漂移。
- **`#68751`** P1/Security: `session-memory` 在 `/reset` 时将原始历史作为当前输入重放，导致自主重执行。

## 6. 功能请求与路线图信号

### 高票远景需求
| Issue | 需求 | 关联进展 |
|-------|------|---------|
| [#72741](https://github.com/openclaw/openclaw/issues/72741) | 外部安全与护栏检查标准接口 | [#90003](https://github.com/openclaw/openclaw/pull/90003) 策略引擎铺垫中 |
| [#63990](https://github.com/openclaw/openclaw/issues/63990) | 多索引 Embedding 记忆 + 模型感知故障转移 | [#88504](https://github.com/openclaw/openclaw/pull/88504) 直接呼应 |
| [#64438](https://github.com/openclaw/openclaw/issues/64438) | 远程 Reranker 端点支持 | — |
| [#76159](https://github.com/openclaw/openclaw/issues/76159) | Cron 任务 `acceptSilentStop` 标志，避免无输出误判错误 | — |

### 有望纳入下一版本的信号
- **多槽位记忆（#88504）** 已进入 Ready for maintainer look，若合并将解决当前记忆插件互斥替换的核心矛盾。
- **KaTeX 数学渲染（#87568）** 已进入待合并队列，直接提升 WebChat 学术场景的可用性。
- **实时 Model Catalog（#90029）** 基础架构已提交，为后续动态 Provider 路由铺路。

## 7. 用户反馈摘要

### 主要痛点
1. **回归地狱：** Codex 模块中断（[#88312](https://github.com/openclaw/openclaw/issues/88312)）和 Mattermost 斜杠 503（[#68113](https://github.com/openclaw/openclaw/issues/68113)）的反复出现，使用户对系统稳定性产生焦虑。
2. **Token / 上下文浪费：** 用户 `Ekko-2xko` 指出引导文件每轮重注入浪费 20–30% Token（[#67419](https://github.com/openclaw/openclaw/issues/67419)）。用户 `automata2k` 指出 "Dreaming" 深层提炼阶段将原始日志未经摘要直接写入 MEMORY.md（[#67363](https://github.com/openclaw/openclaw/issues/67363)）。
3. **MCP 集成断裂：** 用户 `reidperyam` 报告 MCP 工具无法注入子 Agent，无论怎么配置均被忽略（[#85030](https://github.com/openclaw/openclaw/issues/85030)）。
4. **Windows 及 WebChat 双端 UI 短板：** [#67035](https://github.com/openclaw/openclaw/issues/67035) 输入吞字（已修复）、[#77136](https://github.com/openclaw/openclaw/issues/77136) 部分消息无法渲染，而 TUI 正常。

### 社区韧性
- **极高参与度：** 每日 500 条 Issue/PR 讨论，用户愿意投入大量时间撰写极其专业的根因分析报告（如 [#65161](https://github.com/openclaw/openclaw/issues/65161) 用户 `A1fred-AI`）。
- **快速反馈闭环：** 多条 P1 Bug 报告后数小时内即有修复 PR 提交（如 [#90137](https://github.com/openclaw/openclaw/pull/90137)）。

## 8. 待处理积压

以下为长期未获明确回复或久拖未决的高优先级 Issue/PR，建议维护者优先关注：

| 类型 | 编号 | 等级 | 描述 | 等待时长 | 状态标签 |
|------|------|------|------|----------|----------|
| Issue | [#63216](https://github.com/openclaw/openclaw/issues/63216) | **P1** | 高 `reserveTokensFloor` 下上下文溢出硬重置循环 | 自 04-08 | `stale`, `needs-maintainer-review`, `needs-product-decision` |
| Issue | [#68751](https://github.com/openclaw/openclaw/issues/68751) | **P1/Security** | `/reset` 时代理自动重放历史输入（自主重执行风险） | 自 04-19 | `stale`, `needs-security-review` |
| Issue | [#66747](https://github.com/openclaw/openclaw/issues/66747) | **P1** | macOS CLI Gateway 探针 1006 + `EPERM` chmod 错误 | 自 04-14 | `stale`, `needs-live-repro`, `needs-maintainer-review` |
| Issue | [#63673](https://github.com/openclaw/openclaw/issues/63673) | **P1/Regression** | Keychat Bridge 更新后无法接收消息 | 自 04-09 | `stale`, `needs-maintainer-review`, `needs-info` |
| PR | [#54904](https://github.com/openclaw/openclaw/pull/54904) | P2 | 飞书 Webhook 路径校验增强修复（控制面安全加固） | 自 03-26 | `ready for maintainer look`（长期待合并） |
| Issue | [#63998](https://github.com/openclaw/openclaw/issues/63998) | **P1** | Transcript 死亡螺旋：崩溃重启→膨胀→OOM | 自 04-10 | `stale`, `needs-live-repro` |

---
*数据来源：OpenClaw GitHub (github.com/openclaw/openclaw) | 统计区间：2026-06-03 ~ 2026-06-04*

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，基于您提供的 2026 年 6 月 4 日各项目社区动态，我为您呈现以下横向对比分析报告。

---

### 横向对比分析报告：AI 智能体开源生态现状（2026-06-04）

生态目前处于一个关键的**分化与整合期**。大型旗舰项目（OpenClaw）在承受功能膨胀带来的稳定性阵痛，而快速迭代的第二梯队（NanoBot, Hermes, ZeroClaw）正通过精准解决核心痛点来迅速蚕食用户满意度。行业共识正在向**多智能体协同、安全架构前置、Token 成本控制**三大方向收敛。尽管技术路线各异，但社区对“生产级可靠性”的渴望已超过对新功能的追逐。

#### 1. 生态全景

整体生态呈现出 **“一超多强，两极分化”** 的态势。以 OpenClaw 为代表的“重型航母”正努力平衡架构升级与庞大技术债；以 IronClaw/ZeroClaw 为代表的“新生代平台”则在用更干净的架构（Rust/模块化）从安全与性能维度发起冲击。与此同时，NanoBot、Hermes Agent、Moltis 等“敏捷挑战者”凭借高响应度的社区运营和精准的 Bug 修复，正在成为注重开箱即用体验的开发者的新宠。“回归地狱”是当前生态中用户最大的痛点，而多智能体原生支持则是路线图上最强的共鸣点。

#### 2. 各项目活跃度对比

| 项目名称 | Issues (24h) | PRs (24h) | 版本发布 (24h) | 核心主题 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500+ | 500+ | 3 | 架构升级与回归控制 | 极高活跃，阵痛明显 |
| **IronClaw** | 26 | 50 | 1 (v0.29.1) | Reborn 架构成熟化、Slack 集成 | 极高活跃，密集审计期 |
| **ZeroClaw** | 29 | 50 | 0 | 安全架构 (OIDC/沙箱)、S1 Bug 修复 | 极高活跃，冲刺阶段 |
| **NanoBot** | 33 | 34 | 0 | MCP 稳定性、多 Agent 基础 | 高活跃，迭代极快 |
| **Hermes Agent** | 50 | 50 | 0 | 跨平台兼容、桌面端体验 | 高活跃，痛点明确 |
| **CoPaw** | 43 | 49 | 0 | Chromadb 崩溃、浏览器自动化 | 高活跃，稳定性攻坚 |
| **Moltis** | 9(关闭) | 4(待合) | 1 (20260603.01) | Docker 健壮性、Bug 修复速度 | 优秀，响应极快 |
| **LobsterAI** | 0 | 16(14合并) | 1 (2026.6.3) | Cowork 协作、MCP 加固 | 高活跃，团队驱动 |
| **PicoClaw** | 4 | 11(2合并) | 0 | PID 崩溃、Go 安全依赖 | 中等，稳定性维护期 |
| **NanoClaw** | 0 | 9 | 0 | 调度系统、容器运行时修复 | 中等，专注技术债 |
| **NullClaw** | 0 | 1 | 0 | 系统提示词与工具调用优化 | 低活跃，深度思考型 |
| **ZeptoClaw** | 0 | 16(机器人) | 0 | 仅 Dependabot 维护 | 休眠/低活跃 |
| **TinyClaw** | 0 | 0 | 0 | 无活动 | 停滞 |

#### 3. OpenClaw 在生态中的定位：重型旗舰 vs 回归地狱

OpenClaw 是生态中无可争议的 **“母星”与“参照系”**。

- **核心优势：最广袤的生态版图。** 其庞大的插件、技能和通道体系是其他项目短期内无法企及的护城河。它承担着在架构层面进行最前沿探索的任务（如多槽位记忆、Branch-by-Abstraction 迁移 SQLite）。
- **核心劣势：最沉重的技术债务。** 今日动态数据显示，其“回归地狱”的状况在生态中最为严重。P1 级 Blocking Issues（如 Codex 模块中断 #88312）的反复出现，直接动摇了用户对“生产级稳定”的信心。频繁的版本发布（一天三个版本）也印证了其修复压力的巨大。
- **与其他项目对比：**
    - **vs. ZeroClaw / IronClaw**：OpenClaw 是生态最成熟的“爷爷辈”项目，功能最全但负担最重。ZeroClaw（Rust 安全底座）和 IronClaw（Reborn 架构）代表了“下一代”的优化方向，架构更简洁，安全特性原生。
    - **vs. NanoBot / Hermes**：OpenClaw 追求“大而全”，而 NanoBot 和 Hermes 则是“快而准”。NanoBot 的 MCP 紧急修复和 Hermes 的快速功能合并，为用户提供了更少干扰的“轻量级替代选择”。

#### 4. 共同关注的技术方向（涌现需求）

| 技术方向 | 涉及项目 | 具体诉求 / 表现 |
| :--- | :--- | :--- |
| **多智能体协同 (A2A/Sub-Agent)** | **几乎全部活跃项目** | NanoBot 信箱系统、IronClaw `spawn_subagent` 修复、OpenClaw 子智能体管理、ZeroClaw 会话 fork。原生 A2A 协议需求成为最强共识。 |
| **MCP 协议稳定性与深化** | NanoBot, LobsterAI, Moltis, Hermes, OpenClaw | MCP Session 断连、URL 未校验、Token 传递不一致。用户对 MCP 的稳定性抱怨最多，NanoBot 的修复 (#4171) 被评为当日最成功的 Fix。 |
| **安全架构升级** | ZeroClaw, OpenClaw, Hermes, NanoBot | ZeroClaw 的 OIDC/可插拔安全层 RFC，OpenClaw 的 Operator Install Policy，Hermes 的 Slack/QQ 鉴权绕过修复，NanoBot 的沙箱逃逸漏洞。 |
| **记忆与上下文优化** | OpenClaw, CoPaw, IronClaw, NanoBot | Token 浪费（引导文件重注入）、上下文压缩失败、向量库崩溃/膨胀、记忆蒸馏与多槽位架构。从“关注能力”转向“关注 Token 效率”。 |
| **桌面端与 UI 体验** | OpenClaw, Hermes, ZeroClaw, LobsterAI | 国际化 (i18n)、数学/图表渲染、系统托盘、快捷键、窗口管理修复。纯 CLI 不再是市场的唯一标准。 |
| **跨平台兼容 (Docker/Win/Mac)** | Hermes, Moltis, CoPaw, PicoClaw | Windows 更新后崩溃、Docker 工具失效、macOS fd 限制。平台兼容性是用户满意度降级的最普遍原因。 |

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 关键架构/技术差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型 Agent 平台 | 追求极致灵活性的高级用户/管理员 | 插件生态为王，但架构沉重（Python） |
| **NanoBot** | 敏捷迭代的通用框架 | 快速尝鲜、厌恶回归的个人开发者 | 社区极强，核心维护者高产，快速解决级 Bug |
| **Hermes Agent** | 跨平台桌面 Agent 先驱 | Mac/Windows 重度桌面用户 | 桌面客户端功能丰富，社区贡献旺盛，多渠道（QQ/WeCom） |
| **IronClaw** | 下一代模块化平台 (Reborn) | 开发者与企业，注重架构演进 | Reborn 运行时，与 Near AI 生态深度集成 |
| **ZeroClaw** | 安全至上、企业级底座 (Rust) | 安全工程师、企业用户 | Rust 核心，OIDC/沙箱深度集成，RPC 原生会话 |
| **CoPaw** | 亚洲渠道与浏览器 Agent | 渠道运营、Web 自动化用户 | 深度集成飞书/QQ/Telegram，强于浏览器自动化 |
| **Moltis** | Docker 优先、Bug 修复效率 | 运维人员、Docker 重度用户 | 问题响应与修复效率极高，版节奏稳健 |
| **LobsterAI** | 协作式 Agent 工作台 | 知识工作者、小团队 | 网易背书，强 Cowork 协作功能，UI 体验最贴近产品化 |
| **PicoClaw** | 轻量化、嵌入式 Agent (Go) | IoT、边缘设备开发者 | Go 实现，资源占用极低 |

#### 6. 社区热度与成熟度分层

- **第一梯队：综合旗舰与挑战者（极高热度，快速迭代）**
    - **OpenClaw, ZeroClaw, IronClaw, NanoBot, Hermes Agent, CoPaw**
    - 特点：每日更新量均超过 30+，社区讨论激烈，有明确的架构升级路线图。这些项目占据了生态中最核心的用户注意力，但也面临着最多的稳定性挑战。它们共同定义了生态的边界。

- **第二梯队：高质量稳定派（高热度，重修复）**
    - **Moltis, LobsterAI**
    - 特点：虽然 Issue 数量不多，但 PR 合并效率极高，版本发布稳定。Moltis 关闭 Bug 的速度令人印象深刻，LobsterAI 的团队交付力极强。它们代表了一种“少即是多”的成熟发展模式。

- **第三梯队：特定领域深耕者（中低热度，维护期）**
    - **PicoClaw, NanoClaw, NullClaw**
    - 特点：社区讨论量不大，但各自在细分领域（嵌入式、调度、提示词工程）有其独特价值。团队或维护者正聚焦于技术债清理。

- **第四梯队：静默/休眠项目**
    - **ZeptoClaw, TinyClaw**
    - 特点：缺乏有效的人力活动，依赖自动化批量更新依赖。用户在选择此类项目需评估长期维护风险。

#### 7. 值得关注的趋势信号

对于 AI 智能体开发者而言，以下趋势是当前技术选型与社区投入的关键参考：

1.  **稳定性是新的性能 (Reliability is the new Performance)**：用户对回归问题的容忍度已降至冰点。谁能在保证核心功能不受损的情况下快速迭代，谁就能赢得用户的忠诚度。NanoBot 对 MCP 断连的快速修复、Moltis 日清 9 个 Bug，都是正面典范。
2.  **A2A 将引发下一轮生态洗牌**：多项目不约而同构建 Agent-to-Agent 原生基础设施，是当前最强的路线图共识。目前尚未出现主导协议，是早期开发者介入、贡献标准的最佳时机。
3.  **Token 经济学正在重塑 Agent 设计**：开发者社区开始像程序员优化代码一样优化 Token 成本（引导文件重注入、超大日志输出、未压缩的 Memory）。轻量、智能、高效的记忆与上下文管理将成为核心竞争力。
4.  **安全不再是选修课**：ZeroClaw 将 OIDC 和可插拔安全层作为 v0.9.0 核心，结合 Hermes 和 NanoBot 的安全漏洞曝光，表明安全需要从架构层面而非补丁层面加以解决，否则 Agent 的“自主性”将成为一个巨大的 liability。
5.  **去中心化渠道需求是长期刚需**：Mattermost、飞书、SMS、LINE 等非主流渠道的频繁出现，表明用户需要的是真正“私有”和“去平台化”的助手。在这个方向上深耕的项目可能在特定垂直领域建立难以逾越的壁垒。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，分析师为您呈上基于2026年06月04日数据生成的 **NanoBot 项目动态日报**。数据指标显示项目今日继续保持极高的迭代速度与社区活跃度。

---

## NanoBot 项目动态日报 | 2026-06-04

### 1. 今日速览
今日项目处于 **高强度迭代与稳定性加固并重** 的阶段。24小时内触达了33个Issue和34个PR，核心贡献者 **chengyongru** 持续输出架构级重构（事件总线、Dream流、认证系统），同时紧急修复了MCP会话中断这一严重阻塞性问题。社区对新渠道、多Agent协同和安全性表现出强烈兴趣，但也反映出大量stale问题与核心Bug积压并存的局面。

- **活跃度评估**：⭐⭐⭐⭐⭐ (极高)
- **核心基调**：高吞吐的代码合并、紧急修复响应迅速、多Agent路线图初具雏形。
- **风险提示**：长期未解决的安全逃逸漏洞(#143)和工具调用幻觉(#937)仍是磨损社区信任的关键点。

### 3. 项目进展

**稳定性与可靠性提升**
- **[MCP] 重大BUG修复：** 修复了MCP服务器随机断连（`McpError: Session terminated`， #4168）的问题。**PR [#4171](https://github.com/HKUDS/nanobot/pull/4171)** 通过自动会话重连和一次性重试机制，解决了大量用户因MCP失联被迫重启实例的致命痛处。从提报到关闭仅隔1天。
- **[Memory] 记忆模块加固：** **PR [#4183](https://github.com/HKUDS/nanobot/pull/4183)** 被合并。新增了PII/Secret擦除、原子写入机制及代码清晰度重构，提升了数据隐私与持久化可靠性。
- **[Agent] 长任务逻辑修复：** **PR [#3999](https://github.com/HKUDS/nanobot/pull/3999)** 修复了在 `/goal` 长任务模式下，Agent 因 LLM 直接返回文本而误以为任务完成并退出的回归问题。

**核心功能架构演进**
- **[Auth] 认证系统落地：** **PR [#3221](https://github.com/HKUDS/nanobot/pull/3221)** 合并，新增 `nanobot auth` 命令，支持OAuth Device Flow，用户无需手动配置API Key即可快速启动Agent，大幅降低新用户入门门槛。
- **[多Agent] 信箱通信系统：** **PR [#3461](https://github.com/HKUDS/nanobot/pull/3461)** 合并，实现了基于文件系统的信箱（Mailbox）频道插件，作为Agent间通信的纯通道层，为零侵入的多Agent协作铺平了道路。
- **[Dream] 简化为单阶段流：** **PR [#3990](https://github.com/HKUDS/nanobot/pull/3990)** 将旧的“两阶段Dream类”替换为基于定时任务 + `process_direct()` 的简单流，降低了核心循环的复杂度。
- **[WebUI] 运行时状态重构：** **PR [#4135](https://github.com/HKUDS/nanobot/pull/4135)** 将WebUI运行时状态迁移至事件总线架构，提升了状态管理的可预测性，为未来更复杂的UI交互打下基础。

**生态与用户体验**
- **[WebUI]** 新增快捷键 (`Cmd/Ctrl+Shift+O`) 快速开始新对话（[#4185](https://github.com/HKUDS/nanobot/pull/4185)）；修复了启动时请求可能陷入死循环的问题（[#4157](https://github.com/HKUDS/nanobot/pull/4157)）。
- **[Search]** 新增 **博查（Bocha）** 搜索引擎（[#4182](https://github.com/HKUDS/nanobot/pull/4182)），该API为DeepSeek官方指定搜索服务，强化了中文地区的工具链生态。
- **[Provider]** 新增对Azure AAD基于身份的认证支持（[#4126](https://github.com/HKUDS/nanobot/pull/4126)），完善企业级部署能力。
- **[Feishu]** 优化Bot提及处理逻辑（[#4184](https://github.com/HKUDS/nanobot/pull/4184)），提升飞书群聊场景下的命令解析准确率。

---

### 4. 社区热点

1.  **多Agent协同（A2A）成为最强音**
    - 新开放的 **Issue [#4179](https://github.com/HKUDS/nanobot/issues/4179)** 直接提出了原生Agent-to-Agent (A2A) 编排的诉求，与当前合并的Mailbox插件及正在讨论的Subagent控制平面形成了完整的路线图。
    - 老Issue **#222（多Agent配置）** 依旧热度不减（10评论，7👍），说明社区对“Agent团队”协作模式的期待已从“能不能用”转向了“怎么用好”。

2.  **MCP稳定性的胜利**
    - **Issue [#4168](https://github.com/HKUDS/nanobot/issues/4168)** 是目前最具代表性的用户痛点击碎案例。用户报告“After random time, the mcp server cannot be reached”，核心维护者迅速响应并修复（PR #4171），极大提振了社区对项目维护节奏的信心。

3.  **安全与细粒度配置并重**
    - **Issue [#143](https://github.com/HKUDS/nanobot/issues/143)**（文件系统沙箱逃逸）获得了4个👍，是目前最受关注的潜在安全威胁。
    - **Issue [#912](https://github.com/HKUDS/nanobot/issues/912)**（针对不同任务配置不同模型）获得了3个👍，反映出用户在不同场景下（对话/工具/浏览器）对模型能力差异化调度的强需求。

---

### 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 | 点评 |
|---|---|---|---|
| **紧急** | MCP会话随机断连 (#4168 / [#4171](https://github.com/HKUDS/nanobot/pull/4171)) | **已修复** | 可能是目前最影响生产环境的Bug，修复速度极快。 |
| **高** | `exec` 工具严重幻觉 (#937) | **未修复** | 用户反馈“已停止评估该框架”，直接影响Agent落地的可信度。 |
| **高** | 文件系统工具绕过 `restrict_to_workspace` (#143) | **未修复** | 安全风险漏洞，攻击面较大，超过3个月无进展。 |
| **中** | WebUI流式广播泄露内部工具调用 (#954) | **未修复** | 影响C端用户体验，用户界面出现`exec()`等脏数据。 |
| **中** | 媒体文件未清理致磁盘无限增长 (#896) | **未修复** | 长时间运行下的运维隐患。 |
| **中** | 重复`tool_call_id`导致API拒绝请求 (#3932) | **已修复** | 特定模型（如EnvTrustBench）下的稳定性和兼容性提升。 |

---

### 6. 功能请求与路线图信号

- **极大概率进入下个版本：**
    - **多Agent生态雏形：** 信箱Mailbox已合并，Subagent Profiles ([#1012](https://github.com/HKUDS/nanobot/issues/1012)) 和控制平面 ([#1006](https://github.com/HKUDS/nanobot/issues/1006)) 是下一步重点。
    - **企业级认证：** Azure AAD认证配合Auth命令，是面向企业私有化部署的关键拼图。
- **高潜力路线图信号：**
    - **Agent-to-Agent 原生协议：** #4179 表明社区希望Nanobot成为A2A生态的“原生公民”，而非仅仅通过插件桥接。
    - **多租户与网关：** 单实例管理多Agent的诉求频繁出现（[#936](https://github.com/HKUDS/nanobot/issues/936)， [#976](https://github.com/HKUDS/nanobot/issues/976)），是迈向平台化的必经之路。
    - **记忆检索增强：** 引入BM25/TF-IDF的轻量记忆检索（[#80](https://github.com/HKUDS/nanobot/issues/80)）仍是被低估但极具价值的优化方向，可有效抑制长记忆下的Token浪费。

---

### 7. 用户反馈摘要

- **使用场景与痛点：**
    - **“AI真的能干重活了吗？”** 用户（#1022）尝试让Agent执行“翻阅工作表 -> 抓取Facebook帖子 -> 总结”的长任务，经常遇到任务启动后无响应的回归问题，这是对Agent执行力的核心考验。虽然长任务退出问题已修复（#3999），但用户的稳定执行信心仍需维护。
    - **“AI幻觉防不胜防”** 用户（#937）因`exec`工具幻觉问题严重而放弃评估，**这是目前项目留存用户的最大障碍**。
    - **“安全是一道红线”** 用户（#143）明确指出文件工具不遵守工作区限制的问题，社区对此安全担忧获得了普遍共鸣（4👍）。
    - **“我想要的渠道你没有”** Mattermost（[#1011](https://github.com/HKUDS/nanobot/issues/1011)，4👍）是呼声最高的新增渠道，反映出用户对去中心化/非商业化的沟通平台有强烈偏好。

- **积极反馈：**
    - 大量用户对新加入Auth命令、博查搜索和多Agent架构表达兴奋，认为项目正走在正确的“产品化”道路上。
    - 核心贡献者 `chengyongru` 高强度、高质量的输出深得人心，是项目健康运转的最大保障。

---

### 8. 待处理积压

| 优先级 | 问题/PR | 标签 | 说明 |
|---|---|---|---|
| **最紧急** | [#143：文件系统工具沙箱逃逸](https://github.com/HKUDS/nanobot/issues/143) | `security`, `bug` | **潜伏超过4个月的最严重高优漏洞**，建议维护团队在下个轮次优先处理。 |
| **核心Bug** | [#937：exec工具严重幻觉](https://github.com/HKUDS/nanobot/issues/937) | `bug` | **直接影响用户体验和框架口碑**，需从Prompt优化、模型选型或工具调用策略上寻找突破口。 |
| **架构讨论** | [#97：核心架构改进RFC](https://github.com/HKUDS/nanobot/issues/97) | `enhancement` | 贡献者投入极大精力撰写的深度架构分析（6👍），建议维护者正式回复以锚定社区贡献方向。 |
| **渠道适配** | [#117：WhatsApp自身频道静默](https://github.com/HKUDS/nanobot/issues/117) | `bug`, `channel` | 影响部分自建WhatsApp用户的正常使用，等待明确方案。 |

---
**报告完毕。** 分析师认为，NanoBot 正处于从“个人玩具”向“生产力级 Agent 框架”快速演变的关键时期，解决历史积压的核心 Bug 和维持当前的 Merge 速度同样至关重要。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

**Hermes Agent 项目动态日报 — 2026-06-04**

---

### 1. 今日速览

项目在过去 24 小时内保持了极高的活跃度：共产生 50 条 Issue（新开/活跃 44 条，关闭 6 条）和 50 条 PR（待合并 46 条，关闭/合并 4 条），社区提交和反馈密集。Windows 平台兼容性问题（更新后崩溃、环境变量缺失等）以及 macOS 资源限制（文件描述符超限）仍是当前最突出的用户痛点；同时安全相关的 Slack 授权绕过与 QQ bot 鉴权默认开放问题被升级至 “High/Critical” 并进入修复流程。功能讨论方面，Per-Tool 审批、桌面端系统托盘、国际化支持等呼声较高，部分已对应 PR 推进。整体看，项目正处于高响应、快迭代的问题驱动阶段，维护团队和社区协作紧密。

---

### 2. 版本发布

*（本日无新版本发布，该项省略。）*

---

### 3. 项目进展

基础设施与核心稳定性继续改善，今日关闭/合并了以下关键 PR：

- **[Fix] Docker UID 重映射后 gateway 目录权限修复 (#38655, 闭合 #37928)**  
  `benbarclay` 在 #37928 基础上精简出最小修复集，确保 `HERMES_UID` 与宿主机 UID 不一致时 `/opt/hermes/gateway` 的运行时可写权限（`__pycache__` 生成）正确。  
  [https://github.com/NousResearch/hermes-agent/pull/38655](https://github.com/NousResearch/hermes-agent/pull/38655)

- **[Fix] Docker UID 重映射后 entrypoint 不会修复 ui-tui/ 和 gateway/ 权限 (评论最多 #27221 已关闭)**  
  社区确认该问题已通过 #37928 / #38655 闭环。此前 `usermod -u` 不会自动修复用户家目录之外的文件权限，导致非 10000 UID 运行时 gateway 启动失败。  
  [https://github.com/NousResearch/hermes-agent/pull/37928](https://github.com/NousResearch/hermes-agent/pull/37928)

- **[Feature] WeCom 原生流式消息输出 (PR #38660, OPEN)**  
  为 Hermes Gateway 接入 WeCom 平台提供了流式文本和思考动画支持，使用 `aibot_respond_msg` 协议逐步推送。  
  [https://github.com/NousResearch/hermes-agent/pull/38660](https://github.com/NousResearch/hermes-agent/pull/38660)

- **[Feature] Desktop 国际化框架 + 简体中文支持 (PR #38206, OPEN)**  
  为 Hermes Desktop 添加零依赖的 i18n 基础，并随 PR 附带完整简体中文翻译，降低中文用户使用门槛。  
  [https://github.com/NousResearch/hermes-agent/pull/38206](https://github.com/NousResearch/hermes-agent/pull/38206)

- **[Bugfix] Desktop Composer 多会话澄清指示器持久化 + UI 重绘清理 (PR #38631, OPEN)**  
  修复了后台会话陷入 `clarify` 时提示消失、多聊天间切换卡顿等问题，并同步完成图标按钮整合。  
  [https://github.com/NousResearch/hermes-agent/pull/38631](https://github.com/NousResearch/hermes-agent/pull/38631)

此外还有一批 macOS 启动恢复、cron 任务 Windows 兼容、webhook Bearer Token 鉴权等 PR 仍在开放审查中，表明项目在跨平台健壮性和新平台集成上同步发力。

---

### 4. 社区热点

#### 无障碍访问与辅助技术
- **#26689 (评论 8)**：盲人 VoiceOver 用户报告 Hermes Agent macOS 版界面无焦点、无法操作。这是近期评论数最多的 Issue，社区讨论了 Electron 中原生可访问性属性的缺失。  
  [https://github.com/NousResearch/hermes-agent/issues/26689](https://github.com/NousResearch/hermes-agent/issues/26689)

#### Windows 更新导致安装损坏（P1，评论 3）
- **#37881**：`hermes update` 在 Windows 上会重建 venv，但遗留旧目录导致 `pyvenv.cfg` 缺失，最终 `ModuleNotFoundError: hermes_cli`。  
  [https://github.com/NousResearch/hermes-agent/issues/37881](https://github.com/NousResearch/hermes-agent/issues/37881)

#### 安全议题：Slack/QQ 授权绕过（High / Critical）
- **#38068 (P2, High 8.0/8.6)**：Slack 审批与确认按钮完全忽略已配置的 Authorization 策略，导致未经授权的用户可利用按钮执行敏感操作。社区已自行提交了修复 PR（未在本次数据前 20 显示）。  
  [https://github.com/NousResearch/hermes-agent/issues/38068](https://github.com/NousResearch/hermes-agent/issues/38068)
- **#38638 (P2, Critical 9.1/9.3)**：QQ 平台的 own-policy 适配器在未设置 allowlist 时默认允许所有来源的请求，攻击者可直接调用 gateway API 而不经过鉴权。  
  [https://github.com/NousResearch/hermes-agent/issues/38638](https://github.com/NousResearch/hermes-agent/issues/38638)

#### 编辑/工具体验问题
- **#37792 (P2)**：`hermes mcp add` 用 Bearer token 添加 HTTP MCP server 时报 401，但 `hermes mcp test` 却可成功，验证了 CLI 环境中 token 传递逻辑不一致。  
  [https://github.com/NousResearch/hermes-agent/issues/37792](https://github.com/NousResearch/hermes-agent/issues/37792)

---

### 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 是否有已有 Fix PR |
|----------|------------|------|-------------------|
| **P1** | [#37881](https://github.com/NousResearch/hermes-agent/issues/37881) | Windows `hermes update` 破坏了安装，venv 重建后无 `pyvenv.cfg`，hermes_cli 无法导入。 | 无，但 [#38666](https://github.com/NousResearch/hermes-agent/pull/38666) 修复了 cron 子进程的类似 Windows 环境问题 |
| **P1** | [#38652](https://github.com/NousResearch/hermes-agent/issues/38652) | `parse_available_output_tokens_from_error()` 无法识别 OpenRouter/Nous 的 "output cap too large" 格式，导致无限自动重置循环。 | 无 |
| **P2** | [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) | macOS 默认文件描述符软限制 256，Hermes gateway 常超限，报 OSError。 | 无，但 [#35668](https://github.com/NousResearch/hermes-agent/pull/35668) 改进了 macOS launchd KeepAlive 策略 |
| **P2** | [#38068](https://github.com/NousResearch/hermes-agent/issues/38068) | Slack 审批按钮忽略 Authorization 配置（High 8.0）。 | 社区 PR 待审 |
| **P2** | [#38638](https://github.com/NousResearch/hermes-agent/issues/38638) | QQ own-policy 未设 allowlist 时任意请求放行（Critical 9.1）。 | 无 |
| **P2** | [#38407](https://github.com/NousResearch/hermes-agent/issues/38407) | Windows 更新后 git checkout 不完整 + 文件缓存不一致，桌面 GUI 无法启动。 | 无 |
| **P2** | [#38580](https://github.com/NousResearch/hermes-agent/issues/38580) | `requests==2.33.0` 在 Jetson aarch64 上缺失 `_types.py`，每次 update 后 crash。 | 无 |
| **P2** | [#38666](https://github.com/NousResearch/hermes-agent/pull/38666) | cron `_run_job_script` 在 Windows `pythonw.exe` + 非 UTF-8 区域设置下输出为空。 | **已有 PR #38666**（closes #38633） |
| **P2** | [#38662](https://github.com/NousResearch/hermes-agent/issues/38662) | `/claude` gateway 命令错误传递 `--acp --stdio` 给 Claude Code CLI 导致失败。 | 无 |
| **P2** | [#38674](https://github.com/NousResearch/hermes-agent/issues/38674) | 插件系统盲目执行 CWD 下的所有 `.py` 文件且异常捕获不完整，导致非预期代码执行。 | 无 |
| **P3** | [#38650](https://github.com/NousResearch/hermes-agent/issues/38650) | `hermes dump` 将已成功发现的 MCP 服务器报告为 "failed"，产生误导。 | 无 |
| **P3** | [#38314](https://github.com/NousResearch/hermes-agent/issues/38314) | Desktop composer 偶发无法聚焦/输入失效，需重启 App。 | PR #38631 可能修复了部分 Composer 问题 |
| **P3** | [#38669](https://github.com/NousResearch/hermes-agent/issues/38669) | Web UI 聊天滚动条向上翻页后无法滚回底部，且持续弹回顶部。 | 无 |
| **P3** | [#38683](https://github.com/NousResearch/hermes-agent/issues/38683) | Telegram 新 session 不在桌面端会话列表中刷新，直到重启 App。 | 无 |
| **P3** | [#38651](https://github.com/NousResearch/hermes-agent/issues/38651) | Desktop 斜杠命令弹出框对已安装 skills 显示 "no matches"。 | 无 |

**总结**：Windows 平台在 `update`、cron、桌面启动三方面均出现阻塞性 Bug，macOS 主要是资源限制与进程恢复问题。安全类两项达到 High/Critical 且尚未合入修复，需优先关注。

---

### 6. 功能请求与路线图信号

过去 24 小时新增了大量功能请求，与已有 PR 对照后可预判以下方向可能被纳入近期版本：

| 功能描述 | Issue link | 关联 PR / 状态 | 路线图信号 |
|----------|-----------|----------------|-----------|
| Per-Tool / Per-Toolset 审批策略 | [#33905](https://github.com/NousResearch/hermes-agent/issues/33905) | 无 | 高需求（👍1），安全审计关键能力 |
| Desktop 系统托盘后台运行 | [#38007](https://github.com/NousResearch/hermes-agent/issues/38007) | 无 | 👍1，用户期望常驻而不冷启动 |
| Desktop 远程 backend 文件浏览器 | [#38671](https://github.com/NousResearch/hermes-agent/issues/38671) | 无 | 远程工作场景刚需，与 [#37713](https://github.com/NousResearch/hermes-agent/issues/37713) profile 切换互补 |
| Desktop 离线安装 | [#38684](https://github.com/NousResearch/hermes-agent/issues/38684) | 无 | 企业内网/受限环境用户明确需求 |
| Desktop i18n / 中文支持 | 内置需求 | **有 PR #38206** | 接近合并，极大概率纳入下个版本 |
| Desktop 端项目 ID 分组 session | [#38680](https://github.com/NousResearch/hermes-agent/issues/38680) | 无 | 与 WebUI 对齐，适合运维场景 |
| Markdown Mermaid 渲染 | [#38654](https://github.com/NousResearch/hermes-agent/issues/38654) | 无 | 插件式增强，实现成本低 |
| Cron agent 内存写能力修复 | [#38647](https://github.com/NousResearch/hermes-agent/issues/38647) | 无 | 是 bug 同时也是功能缺失，cron 用户依赖 memory 回写 |
| 盲人 VoiceOver 无障碍 | [#26689](https://github.com/NousResearch/hermes-agent/issues/26689) | 无 | 长期未处理，但社区反馈强烈 |

另外，由于 `Claude Code` 网关命令失败（#38662）暴露了 ACP 子进程设计针对 Copilot CLI 而非 Claude CLI，未来可能需要对 `/claude` 做独立参数传递。

---

### 7. 用户反馈摘要

- **无障碍缺失**：盲人用户完全无法在 macOS 上使用 Hermes Agent（#26689），界面元素无法聚焦，Screen Reader 无法读出 TUI 组件。  
- **Windows 更新即损坏**：`hermes update` 后 venv 重建失败 → `ModuleNotFoundError`，依赖完全丢失（#37881），用户形容 “永久破坏了我的安装”。  
- **MCP 服务器配置困惑**：同一个 token，`mcp add` 失败而 `mcp test` 成功（#37792），用户怀疑 CLI 与 SDK 环境变量隔离不一致。  
- **桌面端体验碎片**：
  - Composer 偶发无法点击输入（#38314），用户需重启整个 App。  
  - 斜杠命令对已安装 skills 不显示（#38651），用户无法快速调用功能。  
  - `hermes dump` 报告 MCP 失败但实际可用（#38650），造成运维混淆。  
- **版本跟踪混乱**：`hermes update` 后仍提示落后 7 commits，且停留在 v0.15.1 而标签已有 v0.15.2（#38618）。  
- **Cron 内存写入静默失败**：Agent 报告成功但 memory 未持久化，用户要求至少应有明确异常（#38647）。  
- **Web UI 滚动 Bug**：向上翻阅历史后无法回到底部，每次自动弹回顶部（#38669），严重影响使用。  
- **生产环境建议**：Docker 用户希望提供通用 UID remap（#27221 已修复），macOS 用户希望放宽 fd 限制（#30230），超半数用户在小众架构（ARM64 / Jetson）上遇到依赖缺失（#38580）。

整体而言，用户对 Hermes 的 Agent 能力和生态认可度较高，但 Windows 与 macOS 桌面端的基本稳定性、更新流程的健壮性以及辅助/无障碍设施是当前满意度最低的环节。

---

### 8. 待处理积压

以下为虽已提出一段时间但尚未得到维护者明确分配或回应的项目，建议优先关注：

| 项目 | 类型 | 创建时间 | 备注 |
|------|------|----------|------|
| [#26689](https://github.com/NousResearch/hermes-agent/issues/26689) — 无障碍改进 | Issue (Feature) | 2026-05-16 | 近 20 天无 assignee，已有 8 条社区讨论但无官方标签推进 |
| [#33905](https://github.com/NousResearch/hermes-agent/issues/33905) — Per-Tool 审批 | Issue (Feature) | 2026-05-28 | 安全路线图关键项，无关联 PR |
| [#27221](https://github.com/NousResearch/hermes-agent/issues/27221) — Docker entrypoint UID remap 权限 | Bug (已关闭) | 2026-05-17 | 现已修复可关闭，但当初从提起到合并耗时 18 天，期间多处用户受影响 |
| [PR #27601](https://github.com/NousResearch/hermes-agent/pull/27601) — Webhook Bearer Token 鉴权 | PR (Feature) | 2026-05-17 | 搁置超过 18 天未合并也无 review，社区贡献的常见鉴权方式 |
| [PR #29361](https://github.com/NousResearch/hermes-agent/pull/29361) — Gemini OAuth 模型自动发现 | PR (Feature) | 2026-05-20 | 15 天未合并，无 maintainer 反馈 |
| [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) — macOS fd 上限溢出 | Bug | 2026-05-22 | 无 assignee，影响所有 macOS 高并发用户 |
| [#38314](https://github.com/NousResearch/hermes-agent/issues/38314) — Desktop Composer 无法聚焦 | Bug | 2026-06-03 | 虽新但严重打断工作流，无 assignee，PR #38631 可能部分涉及但未闭合 |
| [#38638](https://github.com/NousResearch/hermes-agent/issues/38638) — QQ own-policy fail open | Bug (Security) | 2026-06-04 | Critical 9.3，虽新但需立即响应以避免在野利用 |

**建议**：维护者可考虑为这些积压项目打上 `help wanted` 或 `needs-decision`，明确排期或合并意向，以维护社区贡献动力。

---

*数据来源：NousResearch/hermes-agent GitHub 项目 Issues/PRs 更新于 2026-06-04 UTC。本日报自动生成，仅供参考。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# 2026-06-04 PicoClaw 项目动态日报

**数据统计区间：** 2026-06-03 至 2026-06-04

---

## 1. 今日速览

过去 24 小时内，PicoClaw 项目活跃度处于**中等偏高**水平。共监测到 **4 条 Issue** 更新和 **11 条 PR** 更新，其中 **2 个 PR 成功合并关闭**（一个 Go 依赖安全升级，一个 MQTT TLS 安全加固），其余 9 个 PR 处于开放或待合并状态。项目当前明显处于 **“稳定性加固与Bug修复”** 周期，无新版本发布。**PID 单例检查冲突导致崩溃循环 (#2720)** 是全局最紧迫的技术债务，社区贡献者已提交了至少两个方向的修复方案在等待裁决。核心功能上，**Config 原生支持 Streaming 请求 (#2404)** 的呼声不减，是下阶段路线图最大看点。

---

## 2. 版本发布

无更新。

---

## 3. 项目进展

今日合并/关闭了 2 个 PR，均为安全与维护方向：

- **[[#2997] fix(deps): bump go from 1.25.10 to 1.25.11 (GO-2026-5039)](https://github.com/sipeed/picoclaw/pull/2997)（已关闭）**
  - 紧急修复 `net/textproto` 库 HTTP 头部错误信息未转义的高危漏洞，确保依赖链安全。
- **[[#2899] fix: add configurable TLS verification for MQTT channel](https://github.com/sipeed/picoclaw/pull/2899)（已关闭）**
  - 移除 MQTT 通道中硬编码的 `InsecureSkipVerify: true`（MITM 风险），新增可配置的 `TLSSkipVerify` 参数，默认开启验证。

其他活跃推进的开放 PR：

| PR | 方向 | 摘要 |
|----|------|------|
| [[#2985]](https://github.com/sipeed/picoclaw/pull/2985) | 体验优化 | `/context` 命令同时展示 summarize 与 compress 阈值 |
| [[#2992]](https://github.com/sipeed/picoclaw/pull/2992) | Bug修复 | 修复 v0.2.9 升级后 Web UI Session 继承主会话历史的问题 |
| [[#2996]](https://github.com/sipeed/picoclaw/pull/2996) | 错误处理 | 修复 shell executor 中 7 处 `json.Marshal` 错误被静默吞掉的问题 |
| [[#2995]](https://github.com/sipeed/picoclaw/pull/2995) | 社区透明 | 在 README News 补充 v0.2.5~v0.2.9 版本亮点 |

---

## 4. 社区热点

- **最活跃讨论：[[#2404] [Feature] Config 支持 Streaming HTTP 请求](https://github.com/sipeed/picoclaw/issues/2404)**
  - **数据**：11 条评论，👍 1，创建于 4 月 7 日，今日仍有更新。
  - **诉求分析**：用户希望像 OpenAI Python SDK 那样在配置文件中写入 `"streaming": true` 即可启用流式传输。当前实现需要手动拼接处理，用户强烈要求“开箱即用”的流式支持。该 Issue 代表了 LLM 调用场景下最标准化的用户体验需求。

- **最大社区工程投入：[[#2720] [BUG] 单例 PID 检查不验证进程身份](https://github.com/sipeed/picoclaw/issues/2720)**
  - **数据**：8 条评论，Priority: High。
  - **动态**：该 Bug 因引发生产环境“崩溃循环”而获高优先级，社区贡献者 `mrigangha` 和 `yuxuan-7814` 分别提交了独立的修复 PR（#2813, #2955）。今日两者均有更新但均被标记为 Stale，社区在等待维护者裁决。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重性 | Issue / PR | 摘要 | 状态 |
|--------|-----------|------|------|
| **🔴 HIGH** | [[#2720]](https://github.com/sipeed/picoclaw/issues/2720) | PID 文件僵尸导致进程反复崩溃 | 已提交修复 PR `#2813` 和 `#2955`，均 Stale |
| **🔴 HIGH** | [[#2958]](https://github.com/sipeed/picoclaw/issues/2958) | 连续请求时 `tool_calls` 消息丢失 | 已提交修复 PR `#2957`，标记 Stale |
| **🟡 MEDIUM** | [[#2954]](https://github.com/sipeed/picoclaw/issues/2954) | 不支持 32 位 Android 系统 | 开放，无进展 |
| **🟢 已修复** | [[#2899]](https://github.com/sipeed/picoclaw/pull/2899) | MQTT 硬编码跳过 TLS 验证（MITM 风险） | ✅ 已合并 |
| **🟢 已修复** | [[#2997]](https://github.com/sipeed/picoclaw/pull/2997) | `net/textproto` 注入漏洞 | ✅ 已合并 |
| **🟢 待合并** | [[#2992]](https://github.com/sipeed/picoclaw/pull/2992) | v0.2.9 升级后 Session 历史错误继承回归问题 | 开放 |
| **🟢 待合并** | [[#2996]](https://github.com/sipeed/picoclaw/pull/2996) | 工具执行时 JSON 序列化失败被静默吞掉 | 开放 |

> **风险提示**：`#2720`（PID + 崩溃循环）与 `#2958`（工具调用丢失）是影响核心 UX 体验的高频 Bug，对应的修复 PR 均已 Stale，存在被自动关闭的风险。

---

## 6. 功能请求与路线图信号

- **最强路线图信号：Streaming HTTP 配置 (`#2404`)**
  - 作为对标 OpenAI 标准 SDK 的必备体验，`streaming: true` 配置功能是社区最强烈呼声。如果项目计划进入功能开发周期（v0.3.x），此特性大概率会纳入下一版本。

- **二级信号：MCP 动态 Header (`#2696`)**
  - 该 PR 已存在较长时间且 Stale，表明当前维护重点不在 MCP 高级集成上，但该能力对于构建复杂的 Channel ↔ MCP 认证流至关重要，是未来的潜在加分项。

- **路线图趋势判断**：当前项目重心完全在 **“稳地基”**——修复残留的稳定性 Bug、安全依赖升级、增强错误处理。功能性开发（Streaming、MCP 增强）暂不是主力方向。

---

## 7. 用户反馈摘要

从 Issue 和 PR 评论中提炼的真实用户声音：

- **满意度来源于贡献体验**：社区贡献者（`chengzhichao-xydt`, `loafoe`, `yuxuan-7814` 等）持续提交高质量修复 PR，说明项目社区生态健康，贡献路径清晰。
- **最大痛点：进程管理**（来自 `#2720`）
  - 用户反馈：“Gateway fails to start when the PID file contains a PID that has been reused by an unrelated process（e.g., `systemd-resolved`）”。这导致用户在重启或 CI/CD 部署时频繁遇到**崩溃循环**，对生产环境信心打击大。
- **关键痛点：工具调用断裂**（来自 `#2958`）
  - 用户描述：“When making consecutive requests that invoke tools... subsequent `tool_calls` messages are not delivered to the UI.” 这直击 AI Agent 代理的核心逻辑——连续工具调用丢失意味着复杂的 Multi-step Reasoning 完全失效。
- **功能诉求：人性化输出**（来自 `#2985` 关联的 `#2968`）
  - 用户期待 `/context` 命令清晰显示窗口阈值，而非只有硬预算压缩提示。体现用户对“可观测性”的需求在提升。

---

## 8. 待处理积压

以下条目已长期未获有效响应或被 Stale Bot 标记，提醒维护者关注：

### 🔴 高优先级（需人工裁决）
- **`#2720` 的两个修复 PR**
  - [[#2813] (mrigangha)](https://github.com/sipeed/picoclaw/pull/2813)
  - [[#2955] (yuxuan-7814)](https://github.com/sipeed/picoclaw/pull/2955)
  - 建议：两个方案均验证进程身份（`/proc/[pid]/exe` 或其他），但实现路径不同。建议维护者尽快定夺合并方向，避免社区重复劳动。

- **`#2958` 工具调用丢失修复 PR**
  - [[#2957] (loafoe)](https://github.com/sipeed/picoclaw/pull/2957)
  - 建议：该 Bug 影响核心 Agent 工作流，PR 已存在但标记 Stale，应优先 review 合并。

### 🟡 中长期积压（功能/兼容性）
- [[#2696] MCP 动态 Headers 增强 (loafoe)](https://github.com/sipeed/picoclaw/pull/2696)
- [[#2956] Security.yml 合并导致通道状态丢失修复 (yuxuan-7814)](https://github.com/sipeed/picoclaw/pull/2956)
- [[#2954] 32 位 Android 兼容问题 (yeozhang)](https://github.com/sipeed/picoclaw/issues/2954)

> **Stale 风险提醒**：大量 PR/Issue 被打上 `[stale]` 标签。社区贡献者投入时间提交高质量修复，若因 Stale Bot 机制自动关闭，可能打击贡献积极性。建议维护者每周安排一次 Stale 检测/恢复优先级评审。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是为您生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 – 2026-06-04

## 1. 今日速览

项目今日呈现高开发活跃度，共提交了 9 条 Pull Request，主要集中在调度模块的健壮性修复和容器运行时的网络适配优化上。由一个 Bug (#2680) 引发的修复 PR (#2681) 已迅速对接，展现了良好的社区响应闭环。然而，新提交的 PR 均未合并，待审 PR 积压数量有所增加，评审效率或面临挑战。整体来看，项目在修复关键 Bug 和优化核心功能上进展显著，社区贡献踊跃。

- **活跃度**：极高（开发进度密集）
- **健康度**：良好 (Bug 修复迅速，但需关注 PR 积压)

## 2. 版本发布

无。

## 3. 项目进展

今日没有 PR 被合并。但提交的 9 个 PR 清晰地展示了项目在以下关键领域的具体进展方向：

- **调度系统健壮性增强**：社区贡献者 ``yairixStudio`` 和 ``shrwnsan`` 提交了 3 个 PR，致力于彻底解决调度任务在失败状态下的各种问题：
    - **PR #2679**：确保永久失败的任务能主动通知用户，而非仅写入日志。
    - **PR #2678**：修复了循环任务在单次运行失败后无法重新安排下一次执行的问题。
    - **PR #2677**：引入了预任务脚本失败时的一次重试机制，并附带诊断信息。
- **容器运行时优化**：``shrwnsan`` 提交的 **PR #2676** 为容器运行器添加了 `NO_PROXY` 环境变量支持，解决了使用单向代理时访问本地服务被错误代理的问题，这对企业级用户尤为重要。
- **核心 Bug 修复**：由 ``IamAdamJowett`` 提交的 **PR #2675** 直接修复了 Slack 集成中因消息块超出字符限制导致整个消息发送失败的严重问题。

## 4. 社区热点

- **核心议题：加密家目录下的服务自启动问题**
    - **Issue #2680**：该 Bug 报告了在启用 `linger` 的情况下，当用户家目录本身是加密类型（如 ecryptfs）时，NanoClaw 服务在重启后静默地无法启动。虽然评论和参与用户数为 0，但获得了 1 个 👍，表明这是特定用户场景下的痛点。
    - **PR #2681 (关联PR)**：报告者 ``glifocat`` 立即提交了相关修复 PR，提议在检测到此类加密家目录时跳过 linger 功能，这是社区自服务的优秀案例。社区对这类直接触及服务可用性的底层 Bug 的关注度极高。

## 5. Bug 与稳定性

| 严重程度 | Bug / PR 编号 | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | **Issue #2680** | 服务在加密家目录系统下（非全盘加密）启动失败。 | 已报告，**已有修复 PR #2681** |
| **高** | **PR #2675** | Slack 集成因消息块长度超限（3000字符）导致整个消息被丢弃。 | 待合并 |
| **中** | **PR #2679** | 永久失败的定时任务未被主动通知给用户。 | 待合并 |
| **中** | **PR #2678** | 循环定时任务在失败后不会重新安排下一次执行。 | 待合并 |
| **低** | **PR #2677** | 预任务脚本失败后没有重试和诊断信息。 | 待合并 |

## 6. 功能请求与路线图信号

- **新增技能（Skill）**：**PR #2683** 提交了一个新的外部容器化技能 `QMD (Query Markdown Documents)`，这是一个提供 BM25 混合搜索能力的 Markdown 文档搜索引擎。这表明项目技能生态在向更专业的知识管理和检索方向扩展。
- **权限模型改进**：**PR #2605** 旨在让子代理能够通过 OneCLI 继承父级代理的权限。虽然该 PR 是 5 月 24 日提交的，但今天被更新，可能是一个重要但复杂度较高的功能点，有可能被纳入下一个大版本。

## 7. 用户反馈摘要

由于今日无 Issues/PRs 关闭或合并，暂无新增的公开满意度反馈。但从 Issue 描述中可提炼出以下用户痛点：

- **[稳定性] 对非标准系统配置的支持不足**：用户 ``glifocat`` 明确指出了服务在 `HOME` 目录为加密文件系统时（`ecryptfs`, `fscrypt` 等）的启动失败问题。这说明在安全要求较高的个人设备（如笔记本）上，服务的部署存在已知的技术障碍。
- **[可用性] 任务失败反馈不佳**：多个关于调度系统的修复 PR 侧面反映出用户在使用过程中，对任务失败、尤其是永久失败或循环任务意外停止的情况，缺乏清晰的通知和干预手段，导致系统行为的不可预测性。

## 8. 待处理积压

- **PR #2605 (feat: inherit parent agent permissions via OneCLI)**：
    - 作者：guyb1 | 创建：2026-05-24 | 更新：2026-06-03
    - **分析**：这是一个涉及权限模型的核心功能 PR，自提交以来已超过 10 天未合并，且今天有更新。建议维护者尽快评审并给予反馈，避免因长期搁置而导致分支冲突或贡献者流失。该功能的引入与否将直接影响对代理父子结构有需求的用户。
    - **链接**: [PR #2605](https://github.com/nanocoai/nanoclaw/pull/2605)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，以下是基于您提供的 GitHub 数据生成的 NullClaw 项目动态日报。

---

## NullClaw 项目动态日报 | 2026-06-04

### 1. 今日速览
过去 24 小时内，NullClaw 项目处于相对稳定但隐藏着重要迭代的状态，活跃度停留在中等偏低水平。具体表现为：社区反馈端（Issues）保持静默，无新版本发布。然而，代码库并非停滞不前——一个关乎 Agent 核心提示词与工具调用机制的关键 Pull Request（#946）正在进行中。该 PR 专注于通过工具分组过滤来优化系统提示（System Prompt），防止动态 MCP 工具污染提示文本，体现了项目在精细化 Agent 控制与 Token 利用效率上的深度思考。

### 2. 版本发布
无

### 3. 项目进展
*   **Agent 系统提示机制优化（待合并）**：社区贡献者 `vernonstinebaker` 提交了 **PR #946**，对 Agent 的系统提示文本生成逻辑进行了微架构调整。
    *   **核心改动**：新增 `filterToolsForPromptText` 逻辑。现在，**文本型系统提示**仅会注入内置工具和隶属于 `always` 过滤器组的 MCP 工具；动态分组的 MCP 工具（根据触发关键词匹配）则不会出现在文本提示中，转而通过原生 API 的 function calling 机制下发 Schema。
    *   **项目意义**：这一改动有效地对提示词进行了“瘦身”，避免了大量难以完全在文本提示中控制的动态工具 Schema 占用宝贵的上下文窗口，从而降低了 Agent 在处理多工具时的逻辑偏离风险。
    *   **链接**: [https://github.com/nullclaw/nullclaw/pull/946](https://github.com/nullclaw/nullclaw/pull/946)

### 4. 社区热点
尽管今日没有激烈的讨论流，但 **PR #946** 本身承载了社区中最核心的技术关切。该 PR 触及了当前 AI Agent 工程中的一个经典痛点：**如何在纯文本推理与精准 API 调用之间做工具调度解耦**。传统的做法是将所有工具 Schema 平铺进系统提示，这会导致提示词臃肿且干扰模型推理。`vernonstinebaker` 提出的“文本提示仅显示固定高频工具，动态工具走 API 调用”的方案，如果被合并，将作为一项重要的 Agent 架构实践被社区关注。
*   **链接**: [https://github.com/nullclaw/nullclaw/pull/946](https://github.com/nullclaw/nullclaw/pull/946)

### 5. Bug 与稳定性
今日未报告新的运行时崩溃或客观功能性 Bug。项目当前的健康度得益于昨日的技术债务偿还：**PR #946** 被标记为 `fix`。它修正了一个潜在的逻辑 Bug：如果没有正确的分组过滤，`tool_filter_groups` 配置可能无法生效，导致动态 MCP 工具错误地以文本形式侵入系统提示，从而造成 Token 浪费或 Agent “分心”。该项目修复直接提升了大规模调用 MCP 生态时的输出稳定性。
*   **链接**: [https://github.com/nullclaw/nullclaw/pull/946](https://github.com/nullclaw/nullclaw/pull/946)

### 6. 功能请求与路线图信号
虽然没有显式的 `feature request` 标签，但 **PR #946** 所展现的修改暗示了项目的下一步路线图重点：**“智能化工具调度与显隐控制”**。
*   **信号分析**：当 `tool_filter_groups` 从单纯的权限/分组概念，进一步扩展到影响系统提示的“文本 vs 原生”双通道输出时，意味着未来的 Agent 可能支持更复杂的路由策略。这一改动为后续实现“基于上下文动态启用/禁用特定工具组”奠定了基础，是 Agent 框架走向成熟的重要一步。这表明项目正从“能跑”向“高效且定制化地跑”演进。

### 7. 用户反馈摘要
在统计周期内，社区未在 Issue 或 PR 评论区留下新的文字反馈。目前的用户池可能处于对新改动（PR #946）消化和测试前的静默等待期，这也侧面说明近期版本在满足用户核心需求（即非崩溃零反馈）方面表现稳定。没有新的痛点报告，对于开源项目而言，这是一个相对平静的积极信号。

### 8. 待处理积压
当前项目中唯一的积压事项即为 **PR #946**。虽然它处于开放状态，但截至报告生成时，尚未获得来自维护者或社区的其他评论与关注（👍: 0）。
*   **建议**：考虑到该 PR 直接修正了 Agent 核心机制，并涉及对 `tool_filter_groups` 架构的语义调整，建议项目维护者尽快安排 Review。及时响应外部高质量贡献（特别是此类涉及架构决策的贡献），对于维护开源社区的贡献者粘性和项目长期健康度至关重要。
*   **链接**: [https://github.com/nullclaw/nullclaw/pull/946](https://github.com/nullclaw/nullclaw/pull/946)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目数据生成的 2026 年 6 月 4 日项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-04

## 1. 今日速览

项目在过去 24 小时内迎来了高强度的迭代与审查周期。得益于 50 个 PR 的频繁活动和 26 个 Issue 的深度讨论，IronClaw 在 **Reborn 架构成熟度**、**Slack 集成**和 **安全加固** 三大主线取得了实质性进展。核心贡献者 `henrypark133` 发起的一系列深入审计（如 #4424-#4429）凸显了项目从“功能可用”迈向“生产级健壮性”的决心。尽管活跃度指标极佳，但新报告的多项严重 Bug 及 Nightly E2E 测试失败仍需团队优先关注。

- **活跃度评估：极高**（50 PRs / 26 Issues / 1 Release）
- **项目健康度：良好**，但处于“快速修复”与“密集审计”的阵痛期。

## 2. 版本发布

**ironclaw-v0.29.1** (发布于 2026-06-04)
- **新功能**：在 Responses API 中加入了温度参数控制（[#3641](https://github.com/nearai/ironclaw/pull/3641)）。
- **修复**：修复了频道对话中 `v1` 历史记录的作用域问题（[#4320](https://github.com/nearai/ironclaw/pull/4320)）。
- **CI/发布**：增加了对 WeCo 的支持。
- **破坏性变更 & 迁移注意事项**：根据 Release Notes，本次为小版本迭代，无重大破坏性变更说明。

## 3. 项目进展

项目在本日的核心叙事是 **“大量功能开发进入验收与合并阶段”**。

**3.1 Slack 集成整体逼近 MVP 发布**
- **核心接入完毕**：`serrrfirat` 将 Slack Beta 路由正式通过 Reborn serve 接入（[#4418](https://github.com/nearai/ironclaw/pull/4418)）。
- **身份绑定闭环**：实现了 Slack 外部 Actor 与 Reborn 用户身份的绑定（[#4421](https://github.com/nearai/ironclaw/pull/4421)），并新增了 Slack 绑定服务（[#4422](https://github.com/nearai/ironclaw/pull/4422)）。
- **OAuth 流程就绪**：WebUI 侧的 Slack OAuth 绑定流程也已提交（[#4423](https://github.com/nearai/ironclaw/pull/4423) 与 [#4430](https://github.com/nearai/ironclaw/pull/4430)）。

**3.2 Reborn 稳定性与工具链强化**
- **子智能体功能完善**：修复了子智能体完成状态投递的问题（[#4413](https://github.com/nearai/ironclaw/pull/4413)），并新增了失败时的回滚补偿机制（[#4435](https://github.com/nearai/ironclaw/pull/4435)）。
- **工具表面暴露**：`builtin.spawn_subagent` 将被暴露给模型调用（[#4434](https://github.com/nearai/ironclaw/pull/4434)），直接响应社区热点 Issue #4424。
- **安全会话路径**：类型密封了受信任的触发器入站路径（[#4406](https://github.com/nearai/ironclaw/pull/4406)）。

**3.3 功能模块迁移与社区共建**
- **WebUI 自动化**：只读的自动化 API（[#4380](https://github.com/nearai/ironclaw/pull/4380)）和前端面板（[#4433](https://github.com/nearai/ironclaw/pull/4433)）已就绪。
- **社区贡献**：来自 `denbite` 的贡献将多个只读 CLI 命令迁移到 Reborn（[#4379](https://github.com/nearai/ironclaw/pull/4379)）。

## 4. 社区热点

**4.1 开发者深度审计季**（Issue #4424 ~ #4429 系列）
由核心开发者 `henrypark133` 发起的高密度审计系列构成了今日最响亮的社区声音。这并非用户的 Bug 报告，而是专业开发者在 Dogfooding 过程中暴露的系统性问题。

- **#4424 (Critical)**: 模型无法调用 `spawn_subagent`。系统提示词“画饼”，实际工具列表里却没有。这直接打回了开发者的信任，是严重的 API 可用性问题。**已有热修复 PR #4434**。
- **#4425: `builtin.http` 是 Context 炸弹**。一次抓取产生 1.2MB 输出导致 Token 溢出。开发者呼吁增加 HTML 剔除和硬性大小限制。
- **#4426: 能力表面控制失效**。`interactive_tools` Profile 被忽略，导致聊天界面暴露了所有生命周期工具。安全面存在重大隐患。
- **#4428: `skill_list` 无限制输出**。一个命令返回 14KB JSON，缺乏分页和截断，严重浪费 Token 预算。
- **#4427, #4429**: 运维上的黑盒问题。循环退出原因不可追踪，提示词包每次都被重建导致性能浪费。

## 5. Bug 与稳定性

| 严重程度 | 编号 | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#4424](https://github.com/nearai/ironclaw/issues/4424) | (Reborn) `spawn_subagent` 无法被模型调用。 | **已有 Fix PR** |
| **严重** | [#4425](https://github.com/nearai/ironclaw/issues/4425) | (Reborn) `builtin.http` 无限制返回数据导致 Context 溢出。 | **暂无 Fix PR** |
| **严重** | [#4426](https://github.com/nearai/ironclaw/issues/4426) | (Reborn) 能力表面控制逻辑被忽略，暴露过多工具。 | **暂无 Fix PR** |
| **高** | [#4428](https://github.com/nearai/ironclaw/issues/4428) | (Reborn) `skill_list` 命令无总量控制，消耗大量 Token。 | **暂无 Fix PR** |
| **高** | [#4420](https://github.com/nearai/ironclaw/issues/4420) | (Triggers)`CompleteAfterFirstFire` 策略不生效，触发器无限执行。 | **暂无 Fix PR** |
| **中** | [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E 持续失败，全链路集成测试红灯。 | **持续监控中** |
| **中** | [#4400](https://github.com/nearai/ironclaw/issues/4400) | 旧的 PID 文件导致服务无法启动。 | **暂无 Fix PR** |

**稳定性亮点**：本日成功合并并修复了多个高优先级 Bug，包括 Context 溢出恢复问题（[#4310](https://github.com/nearai/ironclaw/issues/4310)）和检查点阻塞重试问题（[#4309](https://github.com/nearai/ironclaw/issues/4309)），以及凭证零化加固（[#4222](https://github.com/nearai/ironclaw/issues/4222)）。

## 6. 功能请求与路线图信号

- **API 迁移规划**：将 OpenAI 兼容 API 迁移到 Reborn 的长期任务（[#3283](https://github.com/nearai/ironclaw/issues/3283)）仍在开放中，随着 Reborn 日趋稳定，预计优先级将提升。
- **限制管理**：`serrrfirat` 提出了为适应 Provider 工具数量限制而设计模型可见能力选取方案（[#4407](https://github.com/nearai/ironclaw/issues/4407)），这是一个重要的 scalability 信号。
- **身份与授权深化**：
    - 提出了 Reborn 规范身份解析器（[#4381](https://github.com/nearai/ironclaw/issues/4381)），目标是实现 OAuth 用户的稳定绑定。
    - 提议为每个 OAuth Provider 设置默认账号，简化授权流程（[#4382](https://github.com/nearai/ironclaw/issues/4382)）。

## 7. 用户反馈摘要

由于项目目前处于密集开发期，反馈主要来自核心开发者的深度内部测试（Dogfooding），但代表了早期的前沿用户场景：

- **开发者生产力受挫**：最强烈的反馈集中在功能定义与实际执行的断裂上（#4424），以及 API 的资源无节制消耗（#4425, #4428）。这表明当前版本虽功能强大，但在可用性和效率上还不够“智能”。
- **运维可见性要求**：开发者明确表示需要知道“Agent 循环为什么结束了”（#4427），这反映了对运行时可观测性的迫切需求。
- **安全态度积极**：社区对安全加固（如凭证零化 #4222）的响应持肯定态度，但对能力表面控制失效（#4426）表示担忧，认为这是生产环境部署前的必选项。

## 8. 待处理积压

**需要维护者重点关注：**
- **重要 PR 缺乏 Review**：
    - `zmianian` 提交的第三方 Hook 扩展激活功能（[#3951](https://github.com/nearai/ironclaw/pull/3951)）和 Hook 参数快照测试（[#3928](https://github.com/nearai/ironclaw/pull/3928)）已等待 Review 超过 10 天，主要功能扩展被阻塞。
- **未分配的严重 Bug**：
    - 今日提交的 #4425、#4426、#4428 均没有分配 Fix PR，如果不及时排期，可能在下个版本发布时成为漏网之鱼。
- **遗留技术债务**：
    - PR #4354 合并后遗留的行为变更追踪问题（[#4389](https://github.com/nearai/ironclaw/issues/4389)）尚未开始清理。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的LobsterAI GitHub数据，我已为您生成了2026-06-04的项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-04

## 1. 今日速览

今日LobsterAI项目呈现出**高强度的迭代节奏**，核心开发团队在cowork协作、MCP协议及HTML分享等模块集中发力，展现出强劲的交付能力。过去24小时内，共有16个PR被处理，其中14个已合并/关闭，并发布了新的2026.6.3版本，修复了若干关键问题并引入了多项新功能。尽管社区公开讨论（Issues）活跃度较低，但项目内部的开发效率极高，处于快速演进期。

## 2. 版本发布

### [2026.6.3](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.3) - 已于昨日发布

**更新内容：**
- feat(mcp): 优化了npx MCP启动解析，并增加了首次响应时间日志，提升了MCP服务器的可观测性和启动稳定性。
- feat: 优化了HTML分享功能。
- feat(cowork): 新增功能（Release说明在此处截断）。
- 综合来看，此版本主要聚焦于MCP兼容性、分享体验和cowork功能的优化。

**破坏性变更 & 迁移注意事项：**
- 根据现有描述，本次更新**未提及任何破坏性变更或需要用户特别注意的迁移事项**。建议关注后续完整的Release Notes以获取完整信息。

## 3. 项目进展

今日项目核心进展体现在**cowork协作模块的功能深化**与**MCP协议的稳定性修复**上。主要里程碑包括：

- **核心功能推进：**
    - **cowork模块：** 合入了多项重要功能，包括支持从Artifact预览中**选定文本片段并添加至聊天上下文**（[#2101](https://github.com/netease-youdao/LobsterAI/pull/2101)、[#2098](https://github.com/netease-youdao/LobsterAI/pull/2098)），以及**本地对话分叉（fork）功能**（[#2085](https://github.com/netease-youdao/LobsterAI/pull/2085)），显著增强了用户的对话操作灵活性和信息利用能力。
    - **快捷键系统：** 对快捷键系统进行了**全面重构**（[#2109](https://github.com/netease-youdao/LobsterAI/pull/2109)），扩展了操作或改进了用户体验。
    - **HTML分享：** 对分享对话框和访问控制进行了**精细化打磨**（[#2099](https://github.com/netease-youdao/LobsterAI/pull/2099)），并修复了复制分享链接和代码的问题（[#2105](https://github.com/netease-youdao/LobsterAI/pull/2105)），使其更接近生产可用状态。
- **稳定性与修复：**
    - **MCP模块：** 修复了多个关键问题，包括**防止网关配置重载时的Session超时**（[#2104](https://github.com/netease-youdao/LobsterAI/pull/2104)）、对**远程服务器URL进行验证**（[#2103](https://github.com/netease-youdao/LobsterAI/pull/2103)）以及确保**托管安装能感知Node环境**（[#2100](https://github.com/netease-youdao/LobsterAI/pull/2100)），MCP的整体稳定性得到显著加强。

## 4. 社区热点

今日社区讨论热度较低，公开活动主要集中于用户议题。

- **最活跃议题：** **[#2081 [OPEN] 订阅积分清零投诉](https://github.com/netease-youdao/LobsterAI/issues/2081)**
    - **状态：** 该议题自6月1日创建以来，于昨日（6月3日）获得更新，有2条评论，是目前唯一活跃的公开议题。
    - **分析：** 用户反馈其购买的5500订阅积分在月底被清零，表达了强烈不满。这反映了用户对**订阅资产永久性**的预期与当前**月度清零规则**之间的冲突。尽管并非技术bug，但这是直接关系到用户满意度和商业模型认知的关键反馈，值得产品团队关注。

## 5. Bug 与稳定性

今日并无直接的新增Bug报告，但通过合并的PR可以观察到团队主动修复了以下重要问题：

- **严重程度：高**
    - [MCP] **MCP Session在Gateway配置重载时超时**：可能会导致服务中断或连接丢失。**状态：** 已通过PR [#2104](https://github.com/netease-youdao/LobsterAI/pull/2104) 修复并合并。
- **严重程度：中**
    - [MCP] **远程服务器URL缺失校验**：可能导致配置了无效URL而不自知。**状态：** 已通过PR [#2103](https://github.com/netease-youdao/LobsterAI/pull/2103) 修复并合并。
    - [MCP] **托管安装环境问题**：可能导致MCP服务器因Node路径问题启动失败。**状态：** 已通过PR [#2100](https://github.com/netease-youdao/LobsterAI/pull/2100) 修复并合并。
- **严重程度：低**
    - [UI] **ModelSelector悬浮卡片溢出视口**：影响交互体验。**状态：** 已通过PR [#2106](https://github.com/netease-youdao/LobsterAI/pull/2106) 修复并合并。
    - [Accessibility] **长模态标题显示不全**：影响信息可读性。**状态：** 已有修复PR [#1463](https://github.com/netease-youdao/LobsterAI/pull/1463) 待合并。

## 6. 功能请求与路线图信号

今日社区未提出新的功能请求，但从合并的PR可以清晰看出下一阶段的发展方向：

- **MCP生态成熟化**：对MCP启动、URL校验、环境注入和重载稳定性的系列修复，表明项目正在对MCP协议的支持进行**全面加固和优化**，以迎接更广泛的第三方工具集成。
- **协作能力深入**：`cowork`模块的“选定文本上下文”和“对话分叉”功能，是对协作编辑场景的深度拓展，**极有可能被纳入下一个稳定版本**，作为重头功能推出。
- **HTML分享推向用户**：分享对话框的重新设计和访问控制的完善，预示着**HTML分享功能即将正式对外开放**，而不仅仅是内部测试。

## 7. 用户反馈摘要

- **核心痛点：** 用户 [#2081](https://github.com/netease-youdao/LobsterAI/issues/2081) 对订阅积分“月底清零”的规则表达了强烈不满，认为这损害了其作为付费用户的利益。这反映了用户期望订阅制服务提供更加**灵活或可累积的积分政策**。

## 8. 待处理积压

以下议题或PR已长期未得到响应或合并，可能成为项目健康度的隐患：

- **[PR #1463] [stale] fix long modal titles**：修复长模态标题显示问题的PR已开启超过两个月，并被标记为“stale”。建议维护者及时审查并合并，这是一个提升用户体验的小而明确的改进。
    - 链接: [https://github.com/netease-youdao/LobsterAI/pull/1463](https://github.com/netease-youdao/LobsterAI/pull/1463)
- **[PR #1277] [OPEN] chore(deps-dev): bump the electron group**：由dependabot自动创建的依赖更新PR，已开启超过两个月。长期不合并可能导致依赖版本滞后，建议维护者评估后合并或关闭。
    - 链接: [https://github.com/netease-youdao/LobsterAI/pull/1277](https://github.com/netease-youdao/LobsterAI/pull/1277)
- **[Issue #2081] [OPEN] 订阅积分清零投诉**：虽然已获得评论，但尚未看到官方回复或解决方案。这是一个高敏感度的用户资产问题，长时间的沉默可能引发更负面的社区情绪。
    - 链接: [https://github.com/netease-youdao/LobsterAI/issues/2081](https://github.com/netease-youdao/LobsterAI/issues/2081)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 开源项目2026-06-04项目动态日报。

---

# Moltis 项目日报 | 2026-06-04

## 1. 今日速览
过去24小时项目处于**极高活跃度**状态。昨日集中关闭了9个 Issues，覆盖了 Docker、Vault、UI 等多个关键领域，整体修复效率显著。社区贡献方面，4个待合并 Pull Requests 展现出强劲的外部参与度。从议题反馈来看，用户使用场景正在向 Podman 兼容性和 Web 自动化深水区扩展，项目健康度评级为 **优秀**。维护团队响应迅速，社区生态活跃，迭代步调稳健。

## 2. 版本发布
### 发布版本: `20260603.01`
- **概览：** 这是一个密集的 Bug 修复累积版本，基于昨日关闭的9个 Issues 推断，该版本解决了一系列影响开箱体验和核心稳定性的问题。
- **更新内容（推测）:**
  - **修复：** Vault 初始化时密码验证失败问题 (#1046)。
  - **修复：** Docker 环境下 `send_image` 和 `send_document` 失败的问题 (#1037)。
  - **修复：** 代码块在浅色模式下无语法高亮 (#1045)。
  - **修复：** 自动会话标题生成失效 (#1053)。
  - **修复：** MCP 服务器标准输入输出配置中的环境变量暴露给 LLM 的安全隐患 (#1054)。
  - **修复：** 技能只能按类别开关、无法单独控制的问题 (#1083)。
  - **修复：** 模型选择器无法适配长版本号的问题 (#1052)。
  - **功能：** Agent 开箱即用访问 Moltis 文档 (#1028)。
  - **功能：** Web UI 支持任意文件附件上传 (#1036)。
- **迁移建议：** 无破坏性变更报告。建议所有用户升级至此版本，特别是使用 Docker 部署及 MCP 配置的用户。

## 3. 项目进展
尽管本统计窗口内无 PR 被正式合并（待合并：4），但这通常意味着维护者在集中精力进行代码评审与发版。项目实质性的进步体现在**关闭的9个 Issue**上，它们已随 `20260603.01` 版本落地。

- **社区协作亮点：** Issue #1097（Telegram 流式输出中间结果残留）发布后，贡献者 `s-salamatov` 及时提交了修复 PR #1099。这种社区驱动的快速响应是项目成熟度的有力证明。
- **Web 自动化能力增强：** 贡献者 `resumeparseeval` 提交了 PR #1100（修复 Shadow DOM 穿透问题）和 #1098（修复浏览器工具可选参数为 null 时崩溃）。这两个修复显著提升了 Moltis 在复杂单页应用（如 Salesforce）中的自动化稳定性。
- **可观察性提升：** PR #1093 引入了基于频道/用户粒度的活动日志可见性配置，这是一个面向企业级使用的关键改进。

## 4. 社区热点
- **最热 Bug/事件: Telegram 流式输出修复**：[Issue #1097](https://github.com/moltis-org/moltis/issues/1097)
  用户反馈 Telegram 编辑-替换流式输出会将中间推理步骤混入最终回复。该问题在短短一天内即得到了由 `s-salamatov` 提交的修复 PR ([PR #1099](https://github.com/moltis-org/moltis/pull/1099))。此事件反映出社区对**渠道通信质量**的高要求，以及**贡献者群体的高度活跃**。

- **高关注度 Bug：Docker 核心工具失效**：[Issue #1096](https://github.com/moltis-org/moltis/issues/1096)
  这是继昨日关闭的 #1037 后，又一个 Docker 环境下的严重 Bug。用户反馈 `Read/Write/Edit` 工具在 Docker 中完全失效。**Docker 部署的稳定性**已成为当前社区最大的痛点，连续两天的高严重性 Bug 需要维护者优先关注。

- **潜力需求：多渠道 Agent**：[Issue #1101](https://github.com/moltis-org/moltis/issues/1101)
  用户 `joeblew999` 在今日提出了增加 **SMS 和 LINE** 渠道的功能请求。这标志着社区对 Moltis 的期望已不满足于单一聊天平台，而是向**全渠道个人助手**演进。此 Feature Request 若无异议，大概率会被纳入 Roadmap 讨论。

## 5. Bug 与稳定性
| 严重程度 | Issue ID | 标题 | 状态 | 备注 |
|---|---|---|---|---|
| **严重** | [#1096](https://github.com/moltis-org/moltis/issues/1096) | Docker 下 `Read`/`Write`/`Edit` 工具失效 | 开放，无修复PR | 影响所有 Docker 用户的核心文件操作。亟待响应。 |
| **严重** | [#1095](https://github.com/moltis-org/moltis/issues/1095) | Podman 兼容性失败 | 开放，无修复PR | 影响第三方容器环境。项目拓展新用户群的障碍。 |
| **中等** | [#1094](https://github.com/moltis-org/moltis/issues/1094) | 模型“降级”优先偏好逻辑错误 | 开放，无修复PR | 用户无法有效管理模型列表与偏好。UX 优化需求。 |
| **中等** | [#1098](https://github.com/moltis-org/moltis/issues/1098) | 浏览器工具可选参数为 null 时崩溃 | **待合并PR** | PR #1098 已提交，修复与小型模型兼容性问题。 |
| **常规** | [#1097](https://github.com/moltis-org/moltis/issues/1097) | Telegram 流式输出中间数据残留 | **待合并PR** | PR #1099 已提交，方案可靠。 |

## 6. 功能请求与路线图信号
- **强烈信号：多渠道集成**
  - **请求：** SMS & LINE 渠道支持 ([#1101](https://github.com/moltis-org/moltis/issues/1101))。这表明社区试图将 Moltis 建设为统一的消息中枢。尽管目前支持 Telegram，但企业用户和深度用户对此需求迫切。
- **确认特性：可观察性**
  - **PR：** 频道活动日志可见性设置 ([PR #1093](https://github.com/moltis-org/moltis/pull/1093))。该 PR 为日志监控提供了细粒度控制，是项目从个人开发者工具向团队/企业级工具演进的重要标志。
- **现有主线：部署兼容性与浏览器 Agent**
  - 从过去24小时的高强度修复来看，**Docker 部署健壮性** 和 **Web 自动化 (Browser Agent)** 是`20260603.01`版本迭代的两大核心主线。

## 7. 用户反馈摘要
- **核心痛点：**
  - **Docker 体验是当前最大障碍：** 用户 `IlyaBizyaev` 连续提交了文件发送 (#1037) 和工具失效 (#1096) 的问题。这表明 Docker 的挂载卷和权限处理存在系统性问题，**使用 Docker 的用户目前处于高风险状态**。
  - **配置项不够灵活：** 无论是 Vault、技能开关还是模型管理，用户的反馈都指向了一个问题：**基础配置的 UX 亟待优化**，缺少针对高级用户的细粒度控制面板。
- **满意点：**
  - **响应速度极快：** 社区普遍赞赏维护者的响应速度，昨日提交的9个 Issue 在1天内全部被关闭并打包进新版。
  - **社区贡献活跃：** 外部贡献者 `s-salamatov` 和 `resumeparseeval` 正在接手关键 Bug 的修复，生态呈现出积极的正向循环。
- **用户画像：**
  - **高级用户：** `IlyaBizyaev` 和 `RokkuCode` 提交了大量深层次 Bug，属于愿意花时间测试并反馈的核心 Seed User。
  - **企业团队：** `joeblew999` 提出 LINE 和 SMS 需求，暗示可能有客服、通知等生产环境的集成诉求。

## 8. 待处理积压
项目整体无严重积压，但以下几项需要维护者重点关注：

1. **[PR #1093] 频道活动日志可见性设置** - 自2026-06-03提出后，已停留超过24小时未合并。该特性影响深远，建议尽快安排 Code Review 并决策合并，避免社区贡献者等待过久。
   [PR #1093 链接](https://github.com/moltis-org/moltis/pull/1093)

2. **[Issue #1096] Docker 环境核心工具失效** - 该项目当前最严重的稳定性 Bug，目前无人认领。建议优先分配资源，并考虑是否需要进行 `hotfix` 而不是等待下一个常规版本。
   [Issue #1096 链接](https://github.com/moltis-org/moltis/issues/1096)

3. **[Issue #1094] 模型“降级”优先偏好问题** - 这是一个中等严重性但影响用户体验的配置问题。建议至少先给出 `labels`（如 `help wanted` 或 `good first issue`）以降低用户等待的焦虑感。
   [Issue #1094 链接](https://github.com/moltis-org/moltis/issues/1094)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 2026‑06‑04

## 1. 今日速览
项目过去 24 小时活跃度较高：共处理 **43 条 Issue**（新开/活跃 22，关闭 21）及 **49 条 PR**（待合并 28，合并/关闭 21）。社区围绕 **浏览器自动化崩溃、上下文压缩失败、chromadb 致命段错误** 等稳定性问题讨论热烈；功能请求集中在 **记忆管理、智能体自我进化、自适应上下文** 等方向。无新版本发布。

## 2. 版本发布
无。

## 3. 项目进展
今日合并/关闭的 PR 推动了多渠道一致性、稳定性修复和开发者体验改善：

| PR | 说明 | 状态 |
|----|------|------|
| [#4941](https://github.com/agentscope-ai/QwenPaw/pull/4941) | **技能包下载大小限制**：修复技能市场下载 422 错误（#4928） | 合并 |
| [#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933) | **上下文压缩**：处理非字典 `source` 对象，解决 `AttributeError`，直接影响 #4811、#4924 | 合并 |
| [#4935](https://github.com/agentscope-ai/QwenPaw/pull/4935) | **依赖更新**：`reme-ai` 升至 0.3.1.10，修复文件监视器重入问题 | 合并 |
| [#4942](https://github.com/agentscope-ai/QwenPaw/pull/4942) | **路线图更新**：发布最新项目 Roadmap | 合并 |
| [#4821](https://github.com/agentscope-ai/QwenPaw/pull/4821) | **飞书渠道**：新增群组会话共享模式（`share_session_in_group`） | 合并 |
| [#4737](https://github.com/agentscope-ai/QwenPaw/pull/4737) | **Telegram 渠道**：增加内联键盘交互式工具确认卡 | 合并 |
| [#1837](https://github.com/agentscope-ai/QwenPaw/pull/1837) | **测试框架**：建立 11 个渠道的合同测试基线 | 更新（今日活跃） |

这些更新使 **渠道功能一致性**（QQ/飞书/Telegram）和 **核心稳定性**（上下文压缩、技能下载）迈出实质一步。

## 4. 社区热点
以下 Issue/PR 获得最多关注与讨论：

| 链接 | 标题 | 评论 | 核心诉求 |
|------|------|------|----------|
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | browser_use 启动失败：CDP 超时+浏览器闪退 | 6 | Windows 上三种方式均失败，用户被迫用 npm `playwright-cli` 兜底 |
| [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | chromadb Rust 绑定段错误 (SIGSEGV) 杀死进程 | 5 | 单会话崩溃 45+ 次，需安全降级 |
| [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 上下文压缩失败（旧格式 file block） | 4 | 历史消息格式不兼容导致 `'str' object has no attribute 'get'` |

**诉求分析**：用户对 **浏览器自动化可靠性** 和 **上下文压缩健壮性** 有迫切需求；chromadb 的致命崩溃已严重影响长期运行用户。

## 5. Bug 与稳定性
按严重程度排列（附修复状态）：

| 严重度 | Issue | 问题 | 修复 PR |
|--------|-------|------|---------|
| 致命 | [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | chromadb Rust 绑定段错误导致进程整死（45+ 次/会话） | 无 |
| 严重 | [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | 向量索引膨胀至 37GB，memory_search 每 30 分钟崩溃 | 无 |
| 高 | [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | browser_use 三种启动模式均失败 | 有 PR [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944)（待合并） |
| 高 | [#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889) | Tauri 桌面版插件加载器未启动 | 有 PR [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900)（待合并） |
| 高 | [#4928](https://github.com/agentscope-ai/QwenPaw/issues/4928) | 技能市场下载失败（大小限制） | ✅ 已修（[#4941](https://github.com/agentscope-ai/QwenPaw/pull/4941)） |
| 中 | [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 上下文压缩因旧格式 file block 失败 | ✅ 已修（[#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933)） |
| 中 | [#4811](https://github.com/agentscope-ai/QwenPaw/issues/4811) | 压缩遇非字典 source 字段崩溃 | ✅ 已修（[#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933)） |
| 中 | [#4916](https://github.com/agentscope-ai/QwenPaw/issues/4916) | 备份因浏览器缓存权限失败 | 无 |
| 中 | [#4888](https://github.com/agentscope-ai/QwenPaw/issues/4888) | Dream agent 相对路径覆盖其他 workspace MEMORY.md | 有 PR [#4936](https://github.com/agentscope-ai/QwenPaw/pull/4936)（待合并） |
| 低 | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | /compact 忽略模型 max_input_length | 无 |
| 低 | [#4781](https://github.com/agentscope-ai/QwenPaw/issues/4781) | tool_result_pruning 未限制单次超大输出 | 无 |
| 低 | [#4710](https://github.com/agentscope-ai/QwenPaw/issues/4710) | 向量存储时间戳时区不一致 | 无 |

**警示**：段错误和向量膨胀这两类 **进程级崩溃** 至今没有对应修复 PR，社区反复提及，风险最高。

## 6. 功能请求与路线图信号
用户近期提出的特征需求呈现清晰趋势：

| 领域 | 代表性 Issue | 期望功能 | 路线图信号 |
|------|--------------|----------|------------|
| **智能体自我进化** | [#3470](https://github.com/agentscope-ai/QwenPaw/issues/3470), [#3516](https://github.com/agentscope-ai/QwenPaw/issues/3516) | 类似 Hermes Agent 的自动进化 | 项目组已表示规划中，路线图更新（[#4942](https://github.com/agentscope-ai/QwenPaw/pull/4942)） |
| **记忆管理** | [#3944](https://github.com/agentscope-ai/QwenPaw/issues/3944), [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995), [#4640](https://github.com/agentscope-ai/QwenPaw/issues/4640), [#4171](https://github.com/agentscope-ai/QwenPaw/pull/4171) | 排除心跳/定时任务、自动归档、会话结束总结、记忆蒸馏插件 | 已有插件 PR [#4171](https://github.com/agentscope-ai/QwenPaw/pull/4171)（待合并） |
| **上下文处理** | [#4551](https://github.com/agentscope-ai/QwenPaw/issues/4551), [#4463](https://github.com/agentscope-ai/QwenPaw/issues/4463), [#3801](https://github.com/agentscope-ai/QwenPaw/issues/3801) | 无损压缩、自适应上下文 | 底层已修兼容问题，高级特性待规划 |
| **易用性** | [#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001), [#4920](https://github.com/agentscope-ai/QwenPaw/issues/4920) | 单条消息删除、上键行为改进 | 暂无 PR |
| **集成** | [#4208](https://github.com/agentscope-ai/QwenPaw/issues/4208) | 支持 mem0 记忆库 | 暂无直接动作 |

## 7. 用户反馈摘要
- **浏览器自动化**：Windows 用户尝试默认 CDP、Playwright、npm CLI 均失败，最终只能用第三方工具兜底，**核心能力不可用**。（[#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919)）
- **进程崩溃**：Linux 用户报告 chromadb SIGSEGV 在单会话内出现 45 次，整个 agent 无法正常工作，**长期运行用户受严重影响**。（[#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854)）
- **存储膨胀**：正常使用 3 个月后 ChromaDB 膨胀至 37GB，memory_search 每隔 30 分钟卡死，用户不得不删除存储目录恢复，**反馈强烈**。（[#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795)）
- **上下文压缩**：多名用户遇到压缩因格式不兼容失败（旧 file block、非字典 source），导致对话上下文过长、回复异常。（[#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924), [#4811](https://github.com/agentscope-ai/QwenPaw/issues/4811)）
- **Dream 记忆**：用户发现记忆文件变成空白模板、相对路径覆盖其他 workspace，**记忆沉淀流程未闭环**。（[#3905](https://github.com/agentscope-ai/QwenPaw/issues/3905), [#4888](https://github.com/agentscope-ai/QwenPaw/issues/4888)）
- **插件与备份**：Tauri 桌面版插件加载器不启动、备份因浏览器缓存权限报错，**桌面端体验有缺口**。（[#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889), [#4916](https://github.com/agentscope-ai/QwenPaw/issues/4916)）
- **附件膨胀**：Base64 图片直接载入上下文，消耗大量 token，用户认为应仅作为参考链接。（[#4921](https://github.com/agentscope-ai/QwenPaw/issues/4921)）

## 8. 待处理积压
以下 Issue/PR 长期未获得响应或进度停滞，建议维护者关注：

| 链接 | 创建日期 | 问题摘要 | 备注 |
|------|----------|----------|------|
| [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | 2026‑04‑27 | chromadb Rust 段错误杀死进程 | 无任何 PR，社区多次呼唤 |
| [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | 2026‑05‑29 | 向量索引膨胀至 37GB 导致周期崩溃 | 无修复 PR |
| [#3905](https://github.com/agentscope-ai/QwenPaw/issues/3905) | 2026‑04‑28 | Dream agent 记忆沉淀未闭环 | 用户反复提及，已关闭但问题可能未彻底解决 |
| [#4640](https://github.com/agentscope-ai/QwenPaw/issues/4640) | 2026‑05‑23 | 会话结束自动总结机制（RFC） | 讨论热但无人接手 PR |
| [#4208](https://github.com/agentscope-ai/QwenPaw/issues/4208) | 2026‑05‑11 | 是否支持 mem0 | 无后续 |
| [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995) | 2026‑05‑01 | 增强记忆管理（生命周期、冲突检测） | 多个子需求，待拆解 |
| [#3801](https://github.com/agentscope-ai/QwenPaw/issues/3801) | 2026‑04‑24 | 模型自适应上下文，而非手动限制 | 暂无投入 |

这些积压问题覆盖 **稳定性（段错误、存储膨胀）、记忆系统完整性、高级上下文处理** 等关键领域，建议优先分配资源。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，这是为您生成的 2026-06-04 ZeptoClaw 项目日报。

---

### ZeptoClaw 项目动态日报 | 2026-06-04

---

### 1. 今日速览

过去24小时内，ZeptoClaw 项目处于**低活跃度的维护静默期**。社区端未见任何用户互动（Issue 与 PR 均无人工创建、评论或合并），所有活动均为 Dependabot 发起的自动化依赖更新。项目虽无新功能发布或代码合入，但通过密集的依赖升级 PR 展现出良好的技术债管理习惯。整体项目健康度稳定，但缺乏社区参与信号。

---

### 2. 版本发布

**无**。今日无新版本发布。

---

### 3. 项目进展

今日**并无任何 Pull Request 被合并或关闭**，项目代码库处于零变更状态。

不过，维护者提交了 **16 条依赖更新 PR**（均为 Dependabot 自动生成），覆盖了项目的核心运行时、前端面板和 CI/CD 流水线。这些 PR 虽未落地，但已说明项目正在为下一阶段的稳定性积蓄力量：

- **Rust 后端生态**：`tokio`（#623）、`serde_json`（#627）、`scraper`（#620）、`tower-http`（#617）、`rpassword`（#625）
- **前端面板 / 文档站**：`react`（#616）、`@types/node`（#621）、`tailwindcss`（#619）、`astro`（#615、#614）
- **CI/CD 与基础设施**：`rust:1.95 -> 1.96` Docker 基础镜像（#613）、`docker/login-action`（#628）、`docker/build-push-action`（#622）、`codecov-action`（#624）等

---

### 4. 社区热点

**无**。

过去24小时内项目社区未产生任何活跃话题。16 条 PR 的评论数均为 `undefined`（无评论），点赞数均为 0。这说明当前用户群体反馈较少，或是项目尚处于功能稳定期，未触发大规模讨论。

---

### 5. Bug 与稳定性

今日未收到新的 Bug 报告。但通过 Dependabot 提交的 PR 摘要，可以发现上游修复了多个潜在的稳定性问题：

| 严重程度 | PR / 依赖 | 问题描述 | 影响范围 |
| :--- | :--- | :--- | :--- |
| **中** | [#623 tokio 1.52.3](https://github.com/qhkm/zeptoclaw/pull/623) | 修复异步运行时 `sleep` 可能导致 panic 的问题 | 核心后台任务调度 |
| **低** | [#627 serde_json 1.0.150](https://github.com/qhkm/zeptoclaw/pull/627) | 拒绝非字符串的枚举键，增强反序列化健壮性 | API 数据解析层 |
| **低** | [#625 rpassword 7.5.2](https://github.com/qhkm/zeptoclaw/pull/625) | 修复 Windows 平台 Unicode 输入问题 | 跨平台用户交互体验 |

**建议**：考虑到 `tokio` 的 panic 修复直接影响服务器稳定性，建议维护者**优先审阅并合并 #623**。

---

### 6. 功能请求与路线图信号

Issue 区无新功能请求。

底层依赖方面，[#620 `scraper 0.26 -> 0.27`](https://github.com/qhkm/zeptoclaw/pull/620) 是一个**主要版本 (Major Version)** 更新，`scraper` 库通常负责 HTML 解析与数据抓取。此次大版本升级可能带来 API 破坏性变更或新的抓取能力增强。如果 ZeptoClaw 的智能体依赖该库进行网页内容理解，这可能是底层能力拓展的信号，**需要维护者在合并前仔细评估其兼容性**。

---

### 7. 用户反馈摘要

本周期内无有效用户反馈可供分析。Issue 区和 PR 评论区均处于静默状态。

---

### 8. 待处理积压

目前存在 **16 条 Dependabot 提交的待处理 PR**，建议维护者抽空进行集中处理。具体优先级建议如下：

- **高优先级（建议立即处理）**：
  - [#613](https://github.com/qhkm/zeptoclaw/pull/613): `rust` Docker 基础镜像 `1.95 -> 1.96`。更新 CI/CD 环境，避免旧镜像漏洞。
  - [#623](https://github.com/qhkm/zeptoclaw/pull/623): `tokio 1.52.3`。修复了上游 panic 问题，直接影响生产稳定性。

- **需人工审查**：
  - [#620](https://github.com/qhkm/zeptoclaw/pull/620): `scraper 0.27.0`。大版本号变更，需确认 API 是否向后兼容。
  - [#616](https://github.com/qhkm/zeptoclaw/pull/616): `react 19.2.6`。前端核心依赖，需确保构建与运行无报错。

- **常规合并**：
  - 其余 12 条依赖更新（包括 GitHub Actions 及 npm 包）通常无风险，确认 CI 通过后即可批量合并。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw 项目动态日报 — 2026-06-04

**报告覆盖时间范围：** 2026-06-03 ~ 2026-06-04  
**数据口径：** 近24小时 Issue/PR 更新

---

### 1. 今日速览

项目在过去24小时内维持极高活跃度，共产生 **29 条 Issue 更新** 与 **50 条 PR 更新**。开发重点集中在安全架构重构（可插拔安全层、OIDC 认证）、TUI 终端界面开发以及高优先级 Bug 修复上。针对多个 S1 级阻塞 Bug（RPC 会话回收、Webhook 端口缺失），维护团队响应极为迅速，当日即完成修复合并或提交 PR。项目目前处于 v0.8.0 发布冲刺与 v0.9.0 安全特性预研并行的密集开发阶段，工程健康度与社区参与度均表现突出。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日共有 4 条 PR 完成合并/关闭，多条追踪 Issue 关闭，项目在稳定性和发布工程上取得关键进展：

- **RPC 会话持久化（[PR #7182](zeroclaw-labs/zeroclaw PR #7182) 已合并）**：直接消除因 10 分钟空闲 TTL 导致长时任务中断的 S1 级 Bug（[#7179](zeroclaw-labs/zeroclaw Issue #7179)），实现了 tmux 风格的原生持久化会话管理，对集成代理场景意义重大。
- **TUI 客户端纳入发布矩阵（[Issue #6822](zeroclaw-labs/zeroclaw Issue #6822) 已关闭）**：`zerocode` TUI 二进制正式进入官方构建流水线和包管理器分发列表，终端交互界面距离稳定版交付又近一步。
- **会话分支功能评估（[Issue #7168](zeroclaw-labs/zeroclaw Issue #7168)、[#7167](zeroclaw-labs/zeroclaw Issue #7167) 已关闭）**：关于对话岔路的 Feature Request 已完成评估关闭，为后续版本的会话管理架构提供了决策基础。
- **大量功能性 PR 排队等待合并**：当前仍有 46 条 PR 处于待合并状态，涵盖新 Provider（Kilo AI Gateway [PR #7136](zeroclaw-labs/zeroclaw PR #7136)）、Cron 调度增强（[PR #7188](zeroclaw-labs/zeroclaw PR #7188)、[#7189](zeroclaw-labs/zeroclaw PR #7189)）以及多项文档与 Web UI 修复。

### 4. 社区热点

今日讨论最为激烈的领域为 **安全与架构**，三条 RFC 级 Issue 集中受到关注：

- **[Issue #7142：可插拔安全提供者接口](zeroclaw-labs/zeroclaw Issue #7142)**（评论 3 条）  
  由核心维护者 `singlerider` 发起，计划在 v0.9.0 中将安全实施（沙箱、审计、事件响应）抽象为统一 trait。评论区围绕安全层与配置系统的解耦展开深入讨论。
- **[Issue #7141：OIDC 认证提供者支持](zeroclaw-labs/zeroclaw Issue #7141)**（评论 3 条）  
  作为 #7142 的配套提案，为 RPC/WSS 传输层引入企业级身份认证，双 Issue 共同指向 ZeroClaw 向严肃企业级应用迈进的战略意图。
- **[Issue #7155：高风险命令分级确认策略](zeroclaw-labs/zeroclaw Issue #7155)**（评论 1 条）  
  用户希望引入类似 Claude Code 的 allow/ask/deny 模式。讨论反映社区对智能体自动化与操作安全之间存在强烈的平衡诉求，可能直接影响 v0.9.0 沙箱交互范式。

**分析：** 安全基建在当前社区声量极大，三条 RFC 构成了 v0.9.0 安全特性的完整架构蓝图（提供者接口 + 身份认证 + 执行策略）。

### 5. Bug 与稳定性

按严重程度排列，标注修复进展：

#### 严重（S1）
- **RPC 会话 10 分钟强制回收（[#7179](zeroclaw-labs/zeroclaw Issue #7179)）**  
  **→ 已修复**（[PR #7182](zeroclaw-labs/zeroclaw PR #7182) 已合并）
- **Quickstart Webhook 端口配置缺失（[#7173](zeroclaw-labs/zeroclaw Issue #7173)）**  
  **→ 有修复 PR**（[PR #7193](zeroclaw-labs/zeroclaw PR #7193) 已提交）
- **Agent 重复执行 Shell 命令直至资源耗尽（[#7143](zeroclaw-labs/zeroclaw Issue #7143)）**  
  **→ 未修复**（暂无维护者回应，风险极高）

#### 中等（S2）
- **遥测数据泄露至聊天界面（[#7151](zeroclaw-labs/zeroclaw Issue #7151)）：** WebSocket 共享 Broadcaster 导致 UI 渲染永久“unknown”工具卡片。
- **安全路径策略对引号内 `~` 误报（[#7133](zeroclaw-labs/zeroclaw Issue #7133)）：** 沙箱边界防御存在检测盲区，影响 shell 命令正常使用。
- **Web UI “Clear All”仅清除前端展示（[#7126](zeroclaw-labs/zeroclaw Issue #7126)）：** 后端会话历史未清除，功能形同虚设。

#### 轻微（S3）
- Dashboard 气泡空白行累积（[#6702](zeroclaw-labs/zeroclaw Issue #6702)）
- Chat 时间戳渲染位置错误（[#7157](zeroclaw-labs/zeroclaw Issue #7157)）
- 重载横幅 `paired_tokens` 残留（[#7156](zeroclaw-labs/zeroclaw Issue #7156)）
- 工具栏 i18n 翻译缺失（[#7139](zeroclaw-labs/zeroclaw Issue #7139)）
- 废弃命令引用未清理（[#7128](zeroclaw-labs/zeroclaw Issue #7128)）

### 6. 功能请求与路线图信号

结合 Issue 请求与现有 PR 进展，以下功能具有明确的下版本纳入信号：

#### v0.8.x 方向（当前冲刺）
- **Web Chat 全面升级：** 文件上传（[#7138](zeroclaw-labs/zeroclaw Issue #7138)）、斜杠命令（[#7137](zeroclaw-labs/zeroclaw Issue #7137)）、温度参数省略（[#7145](zeroclaw-labs/zeroclaw Issue #7145)）均指向交互体验对齐主流 Chat 产品。
- **Cron 调度强化：** 相对时间支持（[PR #7188](zeroclaw-labs/zeroclaw PR #7188)）和任务安全隔离（[PR #7189](zeroclaw-labs/zeroclaw PR #7189)）正在并行推进。

#### v0.9.0 方向（安全架构重铸）
- **核心安全抽象：** 可插拔提供者（[#7142](zeroclaw-labs/zeroclaw Issue #7142)）、OIDC（[#7141](zeroclaw-labs/zeroclaw Issue #7141)）、细粒度沙箱策略 RFC（[#6996](zeroclaw-labs/zeroclaw Issue #6996)）构成三叉戟。
- **代码健壮性：** 全局 `forbid(unsafe_code)`（[#7130](zeroclaw-labs/zeroclaw Issue #7130)）、i18n 子模块化（[#7184](zeroclaw-labs/zeroclaw Issue #7184)）、OpenRPC 规范发布（[#7131](zeroclaw-labs/zeroclaw Issue #7131)）体现对工程标准的较高追求。

### 7. 用户反馈摘要

- **痛点直击且快速响应：** `tidux` 在 [#7179](zeroclaw-labs/zeroclaw Issue #7179) 中反馈 RPC 会话 10 分钟超时阻塞工作流，直接驱动 [PR #7182](zeroclaw-labs/zeroclaw PR #7182) 快速修复落地，体现了项目组对用户 blocker 的高度重视。
- **对工程性能的认可：** `sbenedetto` 在报告 [#7143](zeroclaw-labs/zeroclaw Issue #7143) 循环 Bug 时，特意提及“项目使用 Rust 构建且资源占用低”是团队选择 ZeroClaw 的主要原因，侧面验证了项目在性能层面的技术口碑与差异化优势。
- **上手入门痛点：** `eugeneb50` 在 [#7173](zeroclaw-labs/zeroclaw Issue #7173) 中抱怨 Quickstart 配置缺失端口字段，表明“开箱即用”体验在某些边缘场景仍需打磨。
- **国际化需求显现：** `xianshishan` 在 [#7139](zeroclaw-labs/zeroclaw Issue #7139) 中提出工具栏按钮缺少翻译，说明 ZeroClaw 的用户群体正在向非英语母语区域稳步扩张。

### 8. 待处理积压

以下为重要但当前关注度不足的 Issue/PR，提醒维护者关注：

- **[#7143 Agent Shell 循环 Bug](zeroclaw-labs/zeroclaw Issue #7143)**  
  用户 `sbenedetto` 报告的严重行为异常（编码 Agent 陷入死循环直至资源耗尽），直接影响 Coding Agent 场景的核心可用性。当前无维护者回复或修复 PR，建议优先跟进复现与排期。
- **[#6702 Dashboard 空白行累积](zeroclaw-labs/zeroclaw Issue #6702)**  
  开放已超两周（自 2026-05-16），虽为 P3 低优先级，但作为前端视觉瑕疵长期存在，对 Dashboard 的品质观感有持续负面影响，建议在下一个 Web UI 更新周期顺手关闭。
- **[#6996 细粒度沙箱策略 RFC](zeroclaw-labs/zeroclaw Issue #6996)**  
  自 5 月 28 日发布后无维护者正式回复或标记。虽然作为大型架构变更（涉及 Landlock、Bubblewrap、Seatbelt 三端后端）天然需要较长评审周期，但建议在 v0.9.0 正式规划前安排至少一次核心团队讨论，以免阻塞后续安全特性落地。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*