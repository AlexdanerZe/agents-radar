# OpenClaw 生态日报 2026-06-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-22 03:54 UTC

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

# OpenClaw 项目动态日报 | 2026-06-22

---

## 今日速览

过去24小时，OpenClaw 项目共建活动达到峰值，共产生 **500 条 Issue 更新** 与 **500 条 PR 操作**，其中 **112 个 PR 被合并或关闭**，项目修复速率处于开源历史高位。然而，高频 Issue 涌入（特别是 P1 级回归问题）反映出 Beta 阶段稳定性仍面临严峻挑战。今日发布的 `v2026.6.10-beta.1` 针对 Session 状态持久化进行了紧急加固。项目整体处于 **「高速迭代、高频阵痛」** 的冲刺修复期，社区对“无预警破坏”的容忍度正在下降，但对未来的发布纪律改善（PR #95613）抱有期待。

---

## 版本发布

### v2026.6.10-beta.1
- **发布时间**: 2026-06-21 / 22
- **核心亮点**:
  - 修复待处理的子 Agent 完成公告的持久化问题
  - 保障聊天历史记录保证非空
  - 维护媒体索引对齐
  - 重启时恢复休眠的 Follow-up 任务
  - 统一 Compaction 模型别名解析逻辑
- **升级建议**: 所有遭遇 Session 状态不符、回复丢失或子 Agent 执行异常的 Beta 用户应升级至此版本。
- **破坏性变更**: 本次未报告重大破坏性变更或需要手动迁移的配置。

---

## 项目进展

尽管面对巨大的 Issue 压力，社区与核心团队仍在积极推进功能与治理层面的进步：

| PR | 状态 | 影响 |
|---|---|---|
| **[#94478]** fix(doctor): repair legacy Codex route persistence | ✅ 已合并 | 修复旧版 Codex 配置升级后的残留，Doctor 可自动修复 |
| **[#95613]** feat: add monthly daily and stable release policy | 📋 待合并 | **元治理里程碑**，标志着 OpenClaw 走向正式发布节奏 |
| **[#95536]** fix(agents): add tool-activity heartbeat to keep subagent alive | 📋 待合并 | 精准命中了 Agent 在长耗时工具调用中被误杀的社区痛点 |
| **[#90239 / #90259]** Add session history family lookup & reset carryover summaries | 📋 待合并 | 根治长对话上下文在 Session 轮转后断裂的问题 |
| **[#78303]** feat(mcp): channel-mediated approval for MCP tool calls | 📋 待合并 | 引入 MCP 工具审批门控，补全 AI 安全边界 |

---

## 社区热点

| 排名 | Issue | 评论 | 焦点 |
|---|---|---|---|
| 1 | **#86519** [Bug]: Agent repeats identical replies 2-10x on Telegram | 10 评论 | 5.20 升级后 Telegram 回复翻倍，用户强烈情绪聚集 |
| 2 | **#90354** [Feature]: Bounded/validated append semantics for pre-compaction | 8 评论 | 深度架构讨论，揭示现代 AI Agent 的内存冲刷盲区 |
| 3 | **#92043** [Bug]: 180s compaction timeout wall clock no partial-progress reuse | 8 评论 | 慢编译被超时后彻底锁死，无任何分段进度 |
| 4 | **#95495** [Bug]: Silent memory store relocation forcing full re-embed | 7 评论 | **今日信任危机焦点**——零警告的 1499 文件重嵌入 |
| 5 | **#95623** [Bug]: tool_use.id sanitizer misses OpenAI-responses composite id | 7 评论 | 跨 Provider 故障转移中的 ID 解析漏洞，直接导致崩溃 |

**分析**: 社区讨论集中在「用户体验退化」（#86519, #95495）以及「多供应商故障转移可靠性」上（#95623）。此外，Telegram / Matrix 通道问题持续引发关注。

---

## Bug 与稳定性

按严重等级排列（Impact: 数据丢失 > 服务崩溃 > 功能异常 > 安全/隐私）

### 🔴 数据丢失 / 状态损坏（P1）
| Issue | 简述 | Fix PR |
|---|---|---|
| **#95495** | v2026.6.9 静默移动 Memory 存储，强制全量重嵌入 | ❌ 无 |
| **#92076** | 子 Agent 交付因 Session 锁定失败 | ❌ 无 |
| **#92415** | `/model` 切换后 Session 内部模型快照不刷新 | 🔗 [#92415] 有 Linked PR |
| **#91931** | 预置 BOOTSTRAP.md 被自动删除 | 🔗 [#91931] 有 Linked PR |

### 🔴 服务中断 / 进程崩溃（P1）
| Issue | 简述 | Fix PR |
|---|---|---|
| **#95623** | OpenAI 复合 ID 未被劫持，Anthropic 400 崩溃 Session | ❌ 刚提交 |
| **#93375** | Telegram 轮询网络超时后进入不可恢复的崩溃循环 | ❌ 无 |
| **#91009** | Codex PreToolUse 钩子进程占用 100%CPU，拖垮 RPC 通道 | 🔗 [#91009] 有 Linked PR |
| **#95248** | `release_lane` 在 Live Worker 下是 No-op，线程流量卡死 | 🔗 [#95248] 有 Linked PR |
| **#91804** | 内部推理思考暴露给用户（隐私 + 功能崩溃） | ❌ 无 |

### 🟠 通道 / 消息异常（P1–P2）
| Issue | 简述 | Fix PR |
|---|---|---|
| **#86519** | Telegram 回复重复（5.22 缓解但未根除） | ⚠️ 部分缓解 |
| **#90325** | Matrix 通道 TypeError，无法处理任何入站消息 | ❌ 无 |
| **#92460** | 隔离 Cron 显式设置 `delivery.channel` 后仍找不到通道 | 🔗 [#92460] 有 Linked PR |
| **#91363** | 隔离 Cron 在 `model-call-started` 阶段无限超时 | ❌ 无 |
| **#90840** | 子 Agent 裸输出推送至原始聊天而非返回主 Agent 摘要 | ❌ 无 |

### 🟠 性能 / 成本退化（P1–P2）
| Issue | 简述 | Fix PR |
|---|---|---|
| **#91223** | Active-Memory 插件导致提示缓存命中率从 99.9% → 22% | ❌ 无 |
| **#86214** | Codex 客户端在大 `logs_2.sqlite` 下关闭 / 卡死 | ❌ 无 |
| **#90639** | `safeguard` 模式允许 Session 膨胀至 200K tokens 直到崩溃 | ❌ 无 |
| **#90082** | Active-Memory 断路太敏感，Fallback 污染主 Session 上下文 | ❌ 无 |

### 🟡 平台 / 部署异常（P2）
| Issue | 简述 | Fix PR |
|---|---|---|
| **#91144** | Windows 计划任务不保持运行状态 | 🔗 [#91144] 有 Linked PR |
| **#89278** | Codex OAuth 成功但 10s 超时导致 Cron Heartbeat 失败 | ❌ 无 |
| **#90711** | macOS launchd 设置 stderr 为 `/dev/null`，吞掉所有诊断 | 🔗 [#90711] 有 Linked PR |
| **#86612** | Docker 容器在 `OPENCLAW_SANDBOX=1` 下重启循环 | ❌ 无 |

---

## 功能请求与路线图信号

### 1️⃣ 会话架构革新（短期：β · 长期：大功能）
| 特性 | 状态 |
|---|---|
| **#90354** 预编译内存冲刷的边界验证与后写校验 | 🔗 讨论中，修复核心架构盲点 |
| **#90916** 主题级会话家族（Topic-Session Family） | 📋 配合 PR #90239 / #90259 推进中 |
| **#43564** ACP Session 上下文技能注入 | ⏳ 提报三个月仍未决策，累计阻塞企业集成 |

### 2️⃣ Agent 安全与控制
| 特性 | 状态 |
|---|---|
| **#78303** MCP 工具调用审批门控（Consent Envelope） | 📋 合并在望，安全治理的标志性功能 |
| **#91804** 应对推理泄露的强制脱敏 | 🔴 紧急安全需求，或倒逼架构加密改造 |

### 3️⃣ 平台成熟度与可观测性
| 特性 | 状态 |
|---|---|
| **#95613** 月度 / 日报 / 稳定版发布策略 | 📋 **最重要的元功能**，有望在上半年缓解升级焦虑 |
| **#59414** Doctor 命令增强 Node.js 运行时诊断 | ⏳ 老 PR，社区呼声渐强 |
| **#91455** Kubernetes 部署文档改进 | 📋 有响应但未落地 |

### 4️⃣ 渠道与生态
| 特性 | 状态 |
|---|---|
| **#76020** 飞书话题提及控制 | 📋 待合并，优化群聊体验 |
| **#76296** Android APK 工作流 | ⏳ 等待维护者审查，打平移动端差距 |
| **#92479** OpenCode Zen 提供商缺少模型目录 | 🔗 有 Linked PR |

---

## 用户反馈摘要

> 基于今日 Issue 评论提取出的真实用户感知与痛点。

**🔴 【信任破裂】“无声的致命变更”**
> “After upgrading from 2026.6.8 to 2026.6.9, openclaw memory status --deep reported the memory vector store relocated from ~/.openclaw/… to … with zero migration and zero warning during upgrade.”
> —— **#95495** 评论者 fenglanhua

用户的普遍情绪：绝大多数用户愿意承受 Beta 版的不稳定，但无法接受 **“无日志、无警告”** 的操作（搬迁数据库、强制重嵌入、删除用户文件）。这不仅破坏了服务，更破坏了信任。

**🔴 【版本疲劳】“升级像开盲盒”**
> “After updating from 2026.5.12 to 2026.5.20, the agent sends duplicate identical replies on Telegram（2-10x per user message）… Upgrading to 2026.5.22 reduced severity but did not fully fix.”
> —— **#86519** 评论者 w3-design1

快速迭代虽然带来了功能增长，但每次升级都伴随着“惊喜”。`#92241` 甚至出现回滚失败，用户版本信任正在被消耗。`#95613` 的发布策略改革正是社区基于此痛点提出的自救方案。

**🔴 【成本焦虑】“一天的提示缓存命中率从 99.9% 跌到 22%”**
> —— **#91223** 评论者 Enominera

对自托管用户而言，连续多次的全量推理意味着数倍的 API 成本损耗。这个 Bug 已经开始导致部分重度用户考虑降级或退出。

**🟢 【专业认可】“社区诊断水平极高”**
> “#90354 提出的 Bounded append 和 #92043 的 Compaction 分段进度都是非常好的架构提议。”
> —— 多 Issue 共振显示，OpenClaw 拥有一批极具工程深度的社区贡献者，能给出非常精准的根治性方案代码。

---

## 待处理积压

以下 Issue / PR 长期停滞，建议维护组优先关注，避免社区贡献者流失或问题成为沉疴。

| 编号 | 时间 | 标签 / 状态 | 阻碍原因 | 建议行动 |
|---|---|---|---|---|
| **#43564** | 2026-03-12 | `P2`, `needs-product-decision` | ACP 上下文技能注入，技术复杂，缺乏产品线决策 | 列入 Q3 路线图评估或关闭 |
| **#67915** | 2026-04-17 | `P2`, `stale` | 附件权限“Outside allowed folders”反复稳定复现 | 需要一个明确的设计确认或修复 |
| **#58993** | 2026-04-01 | `P1`, `stale` | Google Chat DM 检测失效，完全阻断该渠道使用 | 活跃度低但仍为官方支持通道，需决策 |
| **[PR] #68967** | 2026-04-19 | `stale`, `waiting on author` | Google Chat 会话线程绑定 | 作者超 60 天未回复，建议另寻接手者 |
| **[PR] #75727** | 2026-05-01 | `waiting on author` | Codex 内联媒体渲染未合并 | 作者需回应审查意见，否则自动关闭 |
| **[PR] #76296** | 2026-05-02 | `needs-proof` | Android APK 构建工作流 | 基础设施缺失超过 50 天，对移动生态不友好 |
| **#86214** | 2026-05-24 | `P1`, `needs-live-repro` | Codex 客户端在大日志下中断 | 高危但缺乏现场复现，建议维护者主动介入 |

---

*数据统计窗口：2026-06-21 00:00 UTC 至 2026-06-22 00:00 UTC | 报告生成：2026-06-22*

[#86519]: openclaw/openclaw Issue #86519
[#90354]: openclaw/openclaw Issue #90354
[#92043]: openclaw/openclaw Issue #92043
[#92460]: openclaw/openclaw Issue #92460
[#95495]: openclaw/openclaw Issue #95495
[#95623]: openclaw/openclaw Issue #95623
[#93375]: openclaw/openclaw Issue #93375
[#92076]: openclaw/openclaw Issue #92076
[#92415]: openclaw/openclaw Issue #92415
[#91931]: openclaw/openclaw Issue #91931
[#91804]: openclaw/openclaw Issue #91804
[#91009]: openclaw/openclaw Issue #91009
[#95248]: openclaw/openclaw Issue #95248
[#91363]: openclaw/openclaw Issue #91363
[#90840]: openclaw/openclaw Issue #90840
[#90325]: openclaw/openclaw Issue #90325
[#91144]: openclaw/openclaw Issue #91144
[#90711]: openclaw/openclaw Issue #90711
[#91223]: openclaw/openclaw Issue #91223
[#86612]: openclaw/openclaw Issue #86612
[#86214]: openclaw/openclaw Issue #86214
[#90639]: openclaw/openclaw Issue #90639
[#90082]: openclaw/openclaw Issue #90082
[#90916]: openclaw/openclaw Issue #90916
[#43564]: openclaw/openclaw Issue #43564
[#67915]: openclaw/openclaw Issue #67915
[#58993]: openclaw/openclaw Issue #58993
[#59414]: openclaw/openclaw Issue #59414
[#91455]: openclaw/openclaw Issue #91455
[#76020]: openclaw/openclaw Issue #76020
[#76296]: openclaw/openclaw Issue #76296
[#92479]: openclaw/openclaw Issue #92479
[#68967]: openclaw/openclaw Issue #68967
[#75727]: openclaw/openclaw Issue #75727

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态横向对比分析报告

**报告日期：** 2026-06-22
**分析师角色：** 资深技术分析师（AI 智能体与个人 AI 助手开源生态）
**数据来源：** 各项目 GitHub 动态摘要（以 2026-06-22 00:00 UTC 为快照窗口）


## 1. 生态全景

个人 AI 智能体开源生态正经历**剧烈的“冰火二重天”转型**：头部项目（OpenClaw、ZeroClaw）以每日数百 PR/Issue 的节奏高速狂奔，却因 Beta 阶段的稳定性问题消耗着社区信任；整个 MCP 生态遭遇了 **“安全信任危机”**——NanoBot、NanoClaw、ZeroClaw 在同一天曝出 MCP 权限绕过或参数隐藏漏洞，凸显工具调用安全边界是当前最薄弱的环节。与此同时，**记忆/会话架构的普遍瓶颈**成为所有项目的共识性痛点，OpenClaw、NanoBot、CoPaw、ZeroClaw 均在推进“推式记忆检索”或“上下文窗口管理”创新。而开发者对“无声破坏性变更”的容忍度正在急剧下降，推动头部项目从功能竞赛转向**工程纪律与发布治理的规范化升级**。


## 2. 各项目活跃度对比

| 项目 | Issues 活动 | PR 活动 | 今日 Release | 健康度评估 | 活跃度分层 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（含更新） | 500（112合并/关闭） | v2026.6.10-beta.1 | 🟡 高频阵痛、高速修复 | 超大规模迭代 |
| **ZeroClaw** | 50（36个新开/活跃） | 50（14合并、44待合） | 无 | 🟡 高强度、风险集中 | 超大规模迭代 |
| **Hermes Agent** | 50 | 50（0合并） | 无 | 🟢 高质量 Bug 修复潮 | 大规模活跃 |
| **NanoBot** | 10 | 39（15合并/关闭） | 无（备v0.2.2） | 🟡 安全应急中、响应极快 | 大规模活跃 |
| **CoPaw** | 18 | 37（5合并） | 无 | 🟢 社区共建活跃、移动端爆发 | 高活跃 |
| **PicoClaw** | 6（2关闭） | 32（29合并/关闭） | nightly | 🟢 v0.3.0 稳定冲刺中 | 高活跃/清理周期 |
| **IronClaw** | — | 29（14合并） | 无 | 🟢 Reborn 架构与 CI 重构 | 高活跃/基础设施 |
| **LobsterAI** | 1（新）+14关闭（stale） | 0 | 无 | 🟠 代码停滞、安全新忧 | 中低维护 |
| **NanoClaw** | 2（新/安全） | 7（3合并） | 无 | 🔴 严重安全漏洞积压 | 中低/安全应激 |
| **ZeptoClaw** | 1（关闭） | 1（合并） | 无 | 🟢 极致聚焦、门禁落地 | 低流量精品 |
| **NullClaw** | 1（严重崩溃） | 0 | 无 | 🔴 开发停滞、核心故障 | 濒危 |
| **TinyClaw** | 无活动 | 无活动 | — | ⚪ 停滞 | 休眠 |
| **Moltis** | 无活动 | 无活动 | — | ⚪ 停滞 | 休眠 |


## 3. OpenClaw 在生态中的定位

**绝对生态核心 / 最宽功能面 / 最大的 Beta 阵痛承受者**

- **社区规模与治理信号引领**：OpenClaw 以每日 500+ Issue/PR 的活动量遥遥领先，远超 ZeroClaw（50/50）和 Hermes（50/50）。其社区深度的架构讨论（如 #90354 预编译冲刷边界、#92043 Compaction 分段进度）是生态中最具工程深度的辩论。更重要的是，**#95613 发布策略 PR**（月度/稳定版）正在为整个生态树立**治理标杆**——这标志着头部项目意识到“快速迭代”需要附带“破坏性变更预告”。

- **技术路线差异**：OpenClaw 的“自愈型”工具链（Codex、Doctor、Compaction）使其具备比 NanoBot/ZeroClaw 更强的**事后诊断能力**，但这也带来了更大的代码复杂度和渠道兼容压力（Telegram 回复翻倍 #86519、Matrix 通道崩溃 #90325）。相比之下，NanoBot 走“轻量安全优先”路径，ZeroClaw 走“深度模块化（WASM/MCP 隔离）”路径，Hermes 则更依赖社区贡献者的大规模修补攻势。

- **独特优势与短板**：优势在于**最大的插件/通道生态**和**最成熟的调试工具**（Doctor），短板在于**升级体验是生态中最差的**——#95495 的无声存储搬迁是今日生态中“破坏社区信任”的典型案例，直接挑战了用户对 Beta 项目的容忍底线。


## 4. 共同关注的技术方向（跨项目涌现诉求）

在多项目之间出现了高度一致的技术热点，说明行业正集体面对几个深层瓶颈：

### ① MCP 安全边界集体失守
- **涉及项目**：NanoBot、ZeroClaw、NanoClaw、OpenClaw（间接）
- **具体诉求**：
  - NanoBot P0：`enabledTools` 白名单不限制 Resources/Prompts（#4434 / #4435）
  - ZeroClaw P1：MCP 工具注册渗透到所有 Agent（#8120）、Pipeline 权限绕过（#7960）
  - NanoClaw Critical：`add_mcp_server` 审批界面隐藏危险参数（#2827）
- **分析师判断**：MCP 接入速度远超安全模型设计，未来两周将是生态的 **MCP 安全修补窗口期**。

### ② 记忆/会话架构的“推式检索”转型
- **涉及项目**：OpenClaw、NanoBot、CoPaw、ZeroClaw
- **核心共识**：被动依赖 Prompt Window 已死，行业正向**主动记忆检索**（Agent 自主调用 `search_history` 工具）、**Topic 级会话家族**、**Eager 记忆压缩**转型。
- **代表路径**：NanoBot #4440（只读 `search_history` 工具）、CoPaw `#5321`（Scroll 上下文策略）、OpenClaw `#90354`（Bounded Append + 后写校验）。

### ③ 渠道/Provider 抽象层的容错质量不一
- **涉及项目**：Hermes（Gemini 退役危机）、OpenClaw（跨 Provider ID 解析 #95623）、ZeroClaw（Gemini rate_limited 阻塞 #4879）、CoPaw（智谱模型路由失败 #5330）
- **深层信号**：多 Provider 架构不再是“加分项”，而是**基础生存能力**。无法优雅处理 Provider 故障/退役/接口变更的框架，将被用户抛弃。

### ④ 发布纪律与 CI 硬性化
- **涉及项目**：OpenClaw、ZeptoClaw、IronClaw、ZeroClaw
- **代表信号**：
  - OpenClaw `#95613`：月度 + 稳定版发布策略（元治理里程碑）
  - ZeptoClaw `#611`：7.5MB 二进制 CI 门禁（极致工程纪律）
  - IronClaw：缓存共享/E2E 门禁/依赖重试（CI 稳健性）
  - ZeroClaw：v0.8.3 拆分精细跟踪器（#8070/#8071/#8072）
- **行业意义**：项目从“能跑就行”向**“可预测的交付”**演进。

### ⑤ 移动端/多端适配正在成为“新门槛”
- **核心热点**：CoPaw 今日收到大量移动端 UI 适配 PR（#5369、#5362、#5364、#5367），Hermes 社区呼吁看板集成桌面端（#41222），ZeroClaw 增加 Quickstart 和网关 UI。
- **信号**：Agent 的交互场景正从 CLI 和专业 Web 面板，向**全端泛在化**扩展。尤其是在国内用户群，飞书/钉钉/移动浏览器成为高频接入点。


## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 架构特征 |
|---|---|---|---|
| **OpenClaw** | 通用全栈 AI 智能体平台 | 开发/重度自托管用户 | 单体化核心 + Codex/Doctor 工具链 + 广泛渠道接入 |
| **ZeroClaw** | 模块化智能体构建操作系统 | 高级开发/系统集成者 | WASM 插件沙箱 + MCP 深度绑定 + Pipeline 编排 |
| **NanoBot** | 安全优先的轻量级 Agent 框架 | 安全敏感开发者/研究者 | 轻核 + MCP 审批门控 + 记忆检索工具化 |
| **Hermes Agent** | 社区驱动的桌面 Agent 体验 | 桌面端重度用户 | 社区持续修补 + Desktop App 中心化 + 国际化（中文/泰语） |
| **PicoClaw** | 跨平台稳定 Agent 后端 | 多平台/企业集成者 | JSONL 持久化 + 消息总线背压 + 飞书/钉钉深度适配 |
| **IronClaw** | 下一代智能体架构（学习/反射） | AI 研究员/云原生部署 | Reborn 架构 + 反思服务（WS-3）+ 并发 Turn + Postgres 托管 |
| **CoPaw** | 易用性 + 移动端 Agent 管理 | 非技术用户/移动端用户 | 中核 + 移动端 Web 适配 + 技能商店雏形 |
| **ZeptoClaw** | 极致嵌入式/机器人 Agent | 嵌入式/IoT 开发者 | Rust 单体 + 7.5MB 二进制极限 + 禁用冗余特性 |
| **NanoClaw / NullClaw / LobsterAI** | 小众/防御/停滞 | 特定生态用户 | 安全性暴雷或维护乏力 |

**关键洞察**：

- **IronClaw 的 Reborn 架构**是今日数据中最具前瞻性的——WS-1 初始学习（#4937）和 WS-3 反思服务（#4975）正在将“Agent 从错误中学习”从概念推向工程实现，是所有项目中唯一在**自我改进循环**上取得实质进展的。
- **OpenClaw 与 ZeroClaw 的竞争**不是直接同层竞争。OpenClaw 提供“开箱即用但需要接受 Beta 阵痛”的体验；ZeroClaw 提供“无限组合但需要深度配置”的模块化能力。
- **CoPaw 的移动端爆发**是生态中最明确的“下沉市场”信号——Agent 不再只是技术工具，而是被社区尝试用作**日常沟通/协作入口**。


## 6. 社区热度与成熟度分层

### 🔴 快速迭代 / 高频阵痛层（Feature Sprint + Beta Pain）
- **OpenClaw**、**ZeroClaw**、**CoPaw**
- 特征：每日更新 50+ PR/Issue，功能与 Bug 同时爆发，社区情绪混合着兴奋与“升级恐惧症”。OpenClaw 的“无声变更”争议（#95495）是此层的典型风险——用户为高速迭代付出的信任成本正在升高。
- 成熟度信号：OpenClaw 开始通过治理手段（#95613）规划“有序退出 Beta”，ZeroClaw 通过精细跟踪器（v0.8.3 Triple Tracks）提升交付可预期性。

### 🟢 质量巩固 / 专项深耕层（Quality Consolidation）
- **PicoClaw**、**NanoBot**、**Hermes Agent**、**IronClaw**
- 特征：活动量中等但目标高度聚焦——PicoClaw 批量合并历史 PR 冲刺 v0.3.0，NanoBot 迅速回防 MCP 安全，Hermes 接受社区高质量修补攻势，IronClaw 大范围重构 CI。
- 社区健康度：良好。用户反馈更技术深度化，贡献者网络成熟。

### 🟠 安全应急 / 防御性维护层（Security Emergency / Defensive）
- **NanoClaw**（Critical 漏洞无修复）、**LobsterAI**（新 SSRF 风险）、**NullClaw**（核心 Bug 待响应）
- 特征：活动量低但风险敞口大。NanoClaw 两个安全漏洞（#2827 / #2828）没有今天合入的修复，在生态中处于危险位置；LobsterAI 代码停滞但安全面在扩张（SSRF 削弱）。
- 需要关注：这些项目正在用户信任流失期。如果没有快速的安全响应（如 NanoBot 的几小时内修复），将面临用户逃离风险。

### ⚪ 死亡 / 休眠层
- **TinyClaw**、**Moltis**
- 特征：零活动。基本上已停止维护或处于无人驾驶状态。


## 7. 值得关注的趋势信号（对 AI 智能体开发者的参考价值）

### 趋势一：MCP 的“安全反冲”正在发生
- **信号强度**：⚡⚡⚡⚡⚡（今日最强）
- **详情**：MCP 是当前最火热的集成协议，但 NanoBot、ZeroClaw、NanoClaw 同时暴露其安全设计缺陷。NanoBot 的 `enabledTools` 绕过（#4434）被认为是“纸糊的”；ZeroClaw 的权限渗透问题已被标记为 `risk: high`。
- **对开发者的启示**：如果你在生产环境接入了 MCP 工具，**立刻检查你的权限配置**。预计接下来 1-2 周主流框架将集中发布 MCP 安全补丁。

### 趋势二：“无声变更”正在毁掉 Beta 信任
- **信号强度**：⚡⚡⚡⚡（跨项目共鸣）
- **详情**：OpenClaw #95495 的记忆存储搬迁“零日志”，LobsterAI #2181 的 SSRF 防护削弱“默认启用”，这些**无预警的操作**成为用户情绪爆发点。ZeptoClaw 反其道而行之，通过 CI 门禁强硬固化安全边界。
- **对开发者的启示**：在 Beta 阶段，“透明沟通”与“迁移自动化”比“新功能”更重要。任何静默的侧效应（哪怕是有益的）都会消耗社区信任。确保破坏性变更拥有**日志、回滚路径和公告周期**。

### 趋势三：记忆系统是“下一代 Agent 的 CPU”
- **信号强度**：⚡⚡⚡⚡⚡（生态共识）
- **详情**：不再有项目相信“上下文窗口”是长程交互的解决方案。推式记忆检索（NanoBot #4440）、Eager 压缩（NanoBot #4402、ZeroClaw）、主题级会话家族（OpenClaw #90916）、Scroll 策略（CoPaw #5321）——行业正在积极原型化各种记忆卸载策略。
- **对开发者的启示**：如果你的 Agent 框架没有某种形式的**主动记忆检索**或**上下文窗口压缩**，它将无法支持“数字员工”级别的持续交互。这是未来半年技术分化的关键赛道。

### 趋势四：发布纪律成为核心“元功能”
- **信号强度**：⚡⚡⚡
- **详情**：OpenClaw #95613（发布纪律师）、ZeptoClaw #611（二进制门禁）、IronClaw（CI 矩阵重构）——项目正在集体意识到，“快速迭代”不等于“随意出包”。稳定的发布节奏正在成为比功能特性更受社区关注的能力。
- **对开发者的启示**：“每周无破坏性发布”可能是高信任开源项目的**新行业标准**。评估一个 Agent 框架的成熟度时，先看其发布策略和 CI 防护，再看功能清单。

### 趋势五：Provider 锁定的解药只有“多 Provider 架构 + 抽象层容错”
- **信号强度**：⚡⚡⚡（持久热点）
- **详情**：Hermes 的 Gemini 退役危机、OpenClaw/ZeroClaw 的跨 Provider ID 解析和 rate_limit 问题，表明全球 AI 模型市场正处于“Provider 洗牌期”。唯一可靠的应对策略是：**框架层提供透明的多 Provider 抽象，并具备优雅退化能力**。
- **对开发者的启示**：如果框架只能绑定单一 Provider（或 Provider 切换需要手动改配置），你离生产事故只有一次 API 策略变更的距离。

---

*结论：2026 年 6 月 22 日，AI 智能体开源生态从“功能军备竞赛”正式进入“安全性 + 确定性”的硬仗阶段。MCP 安全、记忆架构、无声变更和发布纪律，正在重新定义优秀框架的门槛。建议技术决策者在选型时，将“处理故障的能力”和“升级体验”置于“功能数量”之前。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-22

**数据来源：** [GitHub - HKUDS/nanobot](https://github.com/HKUDS/nanobot)
**统计时段：** 2026-06-21 ~ 2026-06-22

---

## 1. 今日速览

过去 24 小时，NanoBot 项目活跃度达到近期峰值，维护与社区贡献“双线高负载”运行。共处理 10 个 Issue、39 个 PR，其中 **2 个 P0 级高危安全漏洞**的曝出是今日最大事件——MCP 模块的 `enabledTools` 白名单形同虚设，资源与提示词权限完全绕过，开发团队已火速提交修复 PR #4436。同时，一个导致 Anthropic 系列模型会话“永久锁定”的流式 ID 重复 Bug (#4442) 也引发了广泛关注，社区贡献者随即提交了两个不同思路的修复方案。性能与并发方面的数个关键 Bug 已在今日合并关闭。尽管安全压力陡增，但项目正积极筹备 **v0.2.2 版本**发布（#4445），整体代码库健康度仍在高位运行。

---

## 2. 版本发布

**无新版本发布。**

最新版本：`v0.2.1`，版本发布筹备中：`v0.2.2` (PR #4445)。

---

## 3. 项目进展（今日合入/关闭的重要变更）

过去 24 小时共合入/关闭 15 个 PR，标志着项目在**渠道完善**、**性能优化**与**错误修复**上迈出坚实一步：

**渠道增强：**
- **钉钉群聊白名单 (#4206)**：[<img src="https://img.shields.io/badge/-merged-brightgreen">](https://github.com/HKUDS/nanobot/pull/4206) 新增 `group_allow_from` 配置项，支持群聊白名单与通配符 `*`，企业级部署进一步成熟。
- **Telegram 富消息 (#4422)**：[<img src="https://img.shields.io/badge/-closed-green">](https://github.com/HKUDS/nanobot/issues/4422) 合入了 `sendRichMessage` 支持，可原生渲染表格、任务列表与数学块，紧跟 Bot API 10.1 演进。

**核心稳定性 & 性能：**
- **并发安全修复 (#4408)**：[<img src="https://img.shields.io/badge/-closed-green">](https://github.com/HKUDS/nanobot/issues/4408) 修复了 `Nanobot.run()` 的 `_extra_hooks` 共享变量在多线程/异步场景下被覆写的竞态条件。
- **Token 编码性能优化 (#4420)**：[<img src="https://img.shields.io/badge/-closed-green">](https://github.com/HKUDS/nanobot/issues/4420) 解决了 `estimate_prompt_tokens` 在每轮迭代中对工具定义冗余 `tiktoken` 编码的问题，显著提升包含大量工具定义时的响应速度。

**发布准备：**
- **v0.2.2 版本编排 (#4445)**：[<img src="https://img.shields.io/badge/-open-blue">](https://github.com/HKUDS/nanobot/pull/4445) 正在进行版本号提升、README 新闻更新以及 ruff lint 清理，暗示本轮修复与功能将很快面向用户。

---

## 4. 社区热点

**① [P0] MCP 安全配置绕过（Issues #4434 / #4435）**
- **热度：** ⚠️⚠️⚠️ (当日 MVP)
- **内容：** 社区安全研究员 `YLChen-007` 披露，`enabledTools` 设为 `[]` 时仅拦截了 `list_tools()` 的注册，而 Resources 和 Prompts 仍被无条件注入 Agent。这导致配置了“零信任”策略的用户面临信息泄露风险。
- **社区反应：** 开发者 `michaelxer` 数小时内即提交修复 PR #4436。这一事件表明，随着 MCP 生态接入加速，**细粒度权限治理**已成为压倒性的社区关注焦点。

**② [P0] 流式 ID 重复导致会话中毒（Issue #4442）**
- **热度：** ⚠️⚠️⚠️
- **内容：** 用户 `tedyan` 报告，当流式响应中 `tool_use` ID 出现重复时，框架原样持久化该消息，导致该会话后续全部请求被 Anthropic API 以 `400` 拒绝，Agent 静默停机。
- **社区反应：** 立刻收到两个不同分支的修复 PR：#4443 (去重守卫)、#4444 (Provider 层去重)。这说明**会话连续性和 API 异常容错**是用户无法忍受的底线问题。

**③ [功能] 记忆检索与长程上下文进化（Issue #4440 / PR #4439）**
- **热度：** ⭐⭐⭐
- **内容：** `waelantar` 提出构建一个只读的 `search_history` 工具，使 Agent 能主动检索 `memory/history.jsonl` 中沉淀的历史摘要，而不依赖上下文窗口被动填充。这直接回应了大量“数字员工”场景下，Agent 需要长时间运行但上下文窗口有限的痛点。
- **信号：** `yu-xin-c` 提交的 Eager Memory Consolidation (PR #4402) 也在同一天更新，表明 NanoBot 正系统性地解决**长期记忆**这一 Agent 核心难题。

---

## 5. Bug 与稳定性

| 严重程度 | Bug 描述 | 状态 | 修复 PR | 链接 |
|---|---|---|---|---|
| **P0** | MCP `enabledTools` 白名单未限制 Resources/Prompts | **待合入** | #4436 | [Issue #4434](https://github.com/HKUDS/nanobot/issues/4434) [Issue #4435](https://github.com/HKUDS/nanobot/issues/4435) |
| **P0** | 流式 `tool_use` 重复 ID 永久锁定会话 | **待合入** | #4443 / #4444 | [Issue #4442](https://github.com/HKUDS/nanobot/issues/4442) |
| **P1** | MCP streamable_http 重连失败导致 RuntimeError 崩溃 | **待合入** | #4441 | [PR #4441](https://github.com/HKUDS/nanobot/pull/4441) |
| **P2** | 钉钉配对存储中 Sender ID 类型不一致导致静默拒绝 | **待合入** | #4433 | [PR #4433](https://github.com/HKUDS/nanobot/pull/4433) |
| **P2** | OpenAI 兼容接口非流式工具调用解析异常 | **长期开放** | #4092 | [PR #4092](https://github.com/HKUDS/nanobot/pull/4092) |
| **✓ 已修复** | `Nanobot.run()` 钩子并发不安全 | **已合并** | — | [Issue #4408](https://github.com/HKUDS/nanobot/issues/4408) |
| **✓ 已修复** | `estimate_prompt_tokens` 冗余编码 | **已合并** | — | [Issue #4420](https://github.com/HKUDS/nanobot/issues/4420) |

---

## 6. 功能请求与路线图信号

基于今日活跃的 PR/Issue 讨论，以下方向被认为是即将进入 `v0.2.2` 或下个大版本的核心候选：

**🔜 即将合入（极高概率）**
- **Agent 记忆主动检索**：`search_history` 只读工具 (PR #4439)，关联 Issue #4440。
- **Cron 静默模式 & 锁定接收人** (PR #4225)：支持后台监控任务不通知用户、结果定向投递。
- **工具微压缩可配置** (PR #4392)：让对 Prompt Cache 敏感的用户按需关闭压缩。
- **心跳使用独立模型** (Issue #4431)：用户呼声高，实现成本低，允许低成本模型运行健康检查。

**🛤️ 中期路线图信号**
- **只读会话 (PR #4271)**：为信息展示页面避免无效 LLM 调用，降低运营成本。
- **Eager 记忆归档 (PR #4402)**：主动压缩归档已完成对话切片，实现更智能的上下文窗口管理。
- **WebUI 引导向导 (PR #4395)** 与 **Slash 技能激活 (PR #4284)**：表明开发者体验（DX）和 Web 端用户首次接触体验正在被严肃打磨。

**⏳ 长期悬而未决**
- **统一守护进程语义层 (PR #1854)**：开放逾 3 个月，跨平台后台运行方案的架构设计仍需评审。

---

## 7. 用户反馈摘要

**核心痛点：**
1. **信任与安全透明性**：安全研究员直言 MCP 的 `enabledTools` 隔离是“纸糊的”（Bypass），这让深度信任 `enabledTools` 配置的开发者感到不安。
2. **生产级稳定性**：“会话无声死亡”（#4442）与重连崩溃（#4441）是生产环境中无法容忍的中断。用户期待框架能对 Provider 的不规范响应提供更健壮的防护层。
3. **成本敏感**：用户反映“数字员工”项目响应慢，最终定位是冗余 Token 编码（#4420）。同时要求核心流程与健康检查能用不同模型（#4431），显示出**按成本分配模型资源**是刚需。

**正面诉求与使用场景：**
- 多个用户提及将 NanoBot 改造为“数字员工”/“个人助手”，需要更强的历史记忆能力。
- 开发者社区对内存子系统的关注度极高，#4440、#4402 等提案获得了大量实质性讨论，远超简单的“+1”请求。
- 对于钉钉（#4446）和 Telegram 富文本（#4413）的支持获得了渠道开发者的积极响应，表明企业/团队协作场景正在替代传统的“泛聊天机器人”需求。

---

## 8. 待处理积压

以下 Issue/PR 长期未获得最终响应或合并，提请维护者留意：

| 类型 | 编号 | 标题 | 已开放 | 链接 | 备注 |
|---|---|---|---|---|---|
| 💬 Issue | #1011 | 请求支持 Mattermost 通信渠道 | 4 个月 | [Link](https://github.com/HKUDS/nanobot/issues/1011) | 4 👍，用户认为 Discord/Telegram/Slack 各有限制，开源私有化部署需求仍在 |
| 🛠 PR | #1854 | 统一守护进程语义层 | 3 个月 | [Link](https://github.com/HKUDS/nanobot/pull/1854) | 架构影响大的跨平台增强，需架构评审 |
| 🛠 PR | #3869 | DeepSeek 消息强化（空内容/占位符泄漏） | 1 个月 | [Link](https://github.com/HKUDS/nanobot/pull/3869) | DeepSeek 用户群体增长明显，该 PR 可解锁兼容性 |
| 🛠 PR | #4092 | 修复 OpenAI 兼容 API 工具调用解析 | 24 天 | [Link](https://github.com/HKUDS/nanobot/pull/4092) | 修复了 #4059 和 #4061 两个被确认的 Bug，但等待合入 |
| 🛠 PR | #4145 | 新增天气技能示例 | 21 天 | [Link](https://github.com/HKUDS/nanobot/pull/4145) | 基础贡献，等待 Review |

---
*Report generated by AI Agent based on GitHub activity data for public good. Data reflects snapshot as of 2026-06-22.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据 2026-06-22 的 GitHub 数据生成的 Hermes Agent 项目动态日报。

---

## Hermes Agent 项目动态日报 — 2026-06-22

### 1. 今日速览

今日项目活跃度处于 **极高** 水平，24小时内更新了 50 条 Issue 和 50 条 PR。社区贡献热情空前高涨，特别是 `trevorgordon981` 与 `AlexFucuson9` 等核心贡献者发起了一轮密集的 Bug 修复攻势，一口气提交了 9 个高质量的修复 PR，覆盖了 FTS 数据损坏、Bedrock 路由错误、配置管理等关键领域。Google Gemini CLI 下线引发的 Provider 迁移阵痛（转向 Antigravity）仍是社区讨论的焦点。整体而言，项目正经历高强度开发迭代，社区响应迅速，健康度良好。

### 2. 版本发布

> 过去 24 小时内无新版本发布。

### 3. 项目进展

今日虽无 PR 被正式合并，但提交的大量高价值修复 PR 预示着下一个次版本（很可能为 v0.17.0）的丰富内容。此外，国际化（i18n）工作取得了里程碑式进展。

- **中国区 Dashboard 翻译合并**：中文本地化 PR [#49339](NousResearch/hermes-agent PR #49339) 已合并，填补了 42+ 遗漏键值，全面支持中文配置文件、主题和看板功能。
- **大规模 Bug 修复攻势**：`trevorgordon981` 和 `AlexFucuson9` 提交了一系列针对代码健壮性的 PR：
    - **数据安全**：[#50576](NousResearch/hermes-agent PR #50576) 修复了 FTS5 写入路径损坏导致对话历史丢失的 **P1** 级严重问题。
    - **Provider 路由**：[#50578](NousResearch/hermes-agent PR #50578) 修复了 Bedrock 在非 Claude 模型下路由错误的 **P2** 级关键问题。
    - **基础设施**：[#50570](NousResearch/hermes-agent PR #50570) & [#50580](NousResearch/hermes-agent PR #50580) 替换了代码库中多处在生产环境使用 `-O` 优化时会静默失败的 `assert` 语句。
    - **配置与 Cron**：[#50574](NousResearch/hermes-agent PR #50574) 和 [#50575](NousResearch/hermes-agent PR #50575) 分别修复了 `config set` 空格分隔符失效以及定时任务会话标题生成失败的持续性 Bug。
- **Desktop 进程通信优化**：[#50582](NousResearch/hermes-agent PR #50582) 修复了 Web 终端无法正确处理本地输入法（IME）的问题，提升了亚洲语言的输入体验。

### 4. 社区热点

- **Google Provider 迁移（Gemini -> Antigravity）阵痛**：
    - **最高点赞讨论**：`#29294` (👍 8) 和 `#44943` (👍 5) 率先预报了 Gemini CLI 的退役，获得了社区高度关注。
    - **用户强烈反馈**：在 `#49701` / `#49705` 中，用户 `kzeokytj...` 尖锐地指出“核心提供商已完全不可用，但修复 PR 搁置超过 30 天未合并”，情绪上包含明显的 frustration。
    - **高质量 Bug 汇总**：`#50530` 用户提交了极其详尽的 Antigravity 集成 P2 级问题汇总，包含了复现步骤与根因分析（子代理崩溃/并发掉线/400 错误），体现了社区极高的参与度。
- **Desktop App 一体化呼声增高**：
    - **功能需求**：`#41222` 要求将看板（Kanban）集成到桌面端，获得了 6 个 👍 支持，是今日功能请求中最受欢迎的需求。
    - **兼容性 Bug**：`#37505`（Intel Mac 无法运行 arm64 版 DMG）获得了 6 条评论，反映了用户对多架构支持的基本诉求。
- **战略辩论**：`#41180` 提出了关于 Hermes 是否应该从“强力用户工具”转向“简化 GUI”的战略性辩论，引发了社区对项目核心理念的思考。

### 5. Bug 与稳定性

今日报告了较多影响核心体验的 Bug，但绝大多数已有对应的修复 PR 提交。

- **P1（严重）**
    - **FTS 数据损坏**：[#50576](NousResearch/hermes-agent PR #50576)（已有 PR）—— FTS5 索引写入损坏导致对话历史静默丢失，影响 Gateway 会话连续性。
- **P2（高）**
    - **Antigravity 遗留问题**：[#50530](NousResearch/hermes-agent Issue #50530)（P2）—— 子代理瘫痪、频繁重认证、断点无法恢复。
    - **Bedrock 路由错误**：[#50292](NousResearch/hermes-agent Issue #50292)（已有 PR #50578）—— 非 Claude 模型请求错误地通过 Anthropic SDK 路由导致崩溃。
    - **MCP OAuth 超时**：[#50485](NousResearch/hermes-agent Issue #50485)（P2）—— 添加 OAuth MCP 服务器时，40 秒超时不足于完成浏览器授权，导致集成失败。
    - **OpenRouter 免费模型 404**: [#49983](NousResearch/hermes-agent Issue #49983)（P2）—— 使用免费模型时 HTTP 404 报错。
    - **配置不生效**：[#50553](NousResearch/hermes-agent Issue #50553)（已有 PR #50574）—— 切换配置后，`memory provider` 等设置不会生效。
    - **Desktop Thinking 开关 Bug**: [#50449](NousResearch/hermes-agent Issue #50449)（P2）—— 关闭 Thinking 开关后自动弹回，且写入错误的状态键。
- **P3（中/低）**
    - **Intel Mac 不兼容**：[#37505](NousResearch/hermes-agent Issue #37505) —— 官方 DMG 仅提供 arm64 版本。
    - **Langfuse 集成中断**：[#42033](NousResearch/hermes-agent Issue #42033) —— 本地 Langfuse 实例无法接收 Hermes 的 Trace。

### 6. 功能请求与路线图信号

- **Desktop 应用功能扩展**：用户强烈要求将看板 `#41222`、系统托盘 `#50167`、图片排版优化 `#50554` 和 Windows 缩放 `#37917` 整合进桌面端。结合已有的 PR `#41756`，Desktop 正在成为功能集成的焦点平台。
- **Multi-Account / Multi-Tenancy**：`#10452`（多 Telegram Bot 路由）对应的 PR `#10455` 已存在 2 月余，且 `#18652` 亦在更新，表明社区在等待该功能合并，这将是走向企业级部署的关键信号。
- **Agent 智能进化**：`#50293` 提出了动态思维（Dynamic Thinking）切换，让模型自我检测是否需要深度推理，这是一个非常前沿的 Agent 效率优化方向。`#44672` 要求让后台自我改进的工具白名单可配置，迎合了企业级严格管控需求。
- **错误信息易用性**：`#50460` 呼吁将原始 API 错误转换为“人类可读”的友好信息（如“额度受限，将于 X 时重置”），反映了用户对正反馈和错误诊断的高要求。

### 7. 用户反馈摘要

- **核心痛点（Provider 稳定性）**：Google Gemini CLI 的突然下线让许多用户的生产环境“立竿见影”地瘫痪。尽管社区积极转向 Antigravity，修复滞后的批评声音（`#49701`）值得核心维护者高度警惕。
- **使用场景（工具互操作性）**：用户 `sleijffers` 在集成 Notion 等外部 MCP 工具时遭遇到 OAuth 超时的阻力（`#50485`），说明第三方工具链的平顺连接仍是开箱即用的瓶颈。
- **满意度信号（社区质量）**：用户对 Desktop 集成看板（`#41222`）的期待值很高。用户 `kzeokytj...` 在 `#50530` 中贡献的系统级 Bug 报告，以及 `hrmsLb3cario` 在 `#41180` 中的战略深度辩论，均体现该项目的用户画像非常偏向高阶开发者与深度使用者。
- **功能请求：** 国际化（中文、泰语）和错误信息人性化是今日呼声最高的“生活质量”改善需求。

### 8. 待处理积压

- **长期未合并的核心功能 PR**：
    - **Multi-Telegram Bot**：`#10455`（构建于 2026-04-15）和 `#18652`（构建于 2026-05-02）。两者至今已搁置超过 1-2 个月。考虑到今日有关于它的话题性 Issue `#10452` 的更新，建议尽快评估合并优先级。
    - **Desktop 看板集成**：`#41756`（构建于 2026-06-08），对应社区呼声最高的功能请求 `#41222`，等待深度 Review。
- **策略决策待定**：
    - `#41180`（Desktop 应用定位辩论）虽在今日被更新，但缺乏来自维护者的明确信号。该决策将影响未来整个桌面端的开发方向。
- **数据监控提醒**：
    - 当前 **PR 待合并池偏大**（44/50）。尽管今日提交了许多高质量修复，但若合并节奏滞后，这些分支可能迅速过时并产生大规模冲突，形成技术债。建议开展“合并周”活动来消化积压。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，以下是为您生成的 PicoClaw 项目日报。

---

# PicoClaw 项目动态日报 | 2026-06-22

---

## 今日速览

过去 24 小时项目活跃度处于**高位**。共有 32 条 Pull Request 被更新（其中 29 条已合并/关闭，3 条待合并），6 条 Issue 获得更新（4 条活跃，2 条已关闭），并发布了 1 个夜间构建版本。核心贡献者 **SiYue-ZO** 批量合并了多个历史 PR，涵盖消息总线背压、JSONL 存储崩溃一致性、回退链上下文处理、模型配置工作流、跨平台硬件支持等关键领域，项目在追求 **v0.3.0 稳定性**和**功能完整性**上迈出了坚实一步。同时，社区报出了一个关于国产模型供应商（Volcengine Doubao）工具调用泄漏的新 Bug，需重点关注。

---

## 版本发布

### nightly: Nightly Build (v0.3.0-nightly.20260622.287853ab)

项目发布了最新的自动化夜间构建版本，基于 `main` 分支。该版本为自动构建，可能包含未完全测试的变更，官方建议谨慎使用。

- **完整变更日志**: [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

**注意**: 这是开发中的快照版本，不建议在生产环境直接使用。

---

## 项目进展

今日有大量此前积累的 PR 被集中合并/关闭，标志着一系列重要的功能与修复正式进入 `main` 分支，主要进展包括：

### 核心运行时稳定性

- **消息总线背压处理** ([#2906](https://github.com/sipeed/picoclaw/pull/2906))：修复了队列饱和时无界阻塞的问题，引入了有界等待、流级别丢弃统计和专用健康指标，显著增强了系统在高负载下的健壮性。
- **JSONL 会话元数据性能与一致性**：
    - **热路径克隆修复** ([#2913](https://github.com/sipeed/picoclaw/pull/2913))：修复了缓存命中时仍深度克隆整个内存索引的性能问题。
    - **崩溃后元数据漂移修复** ([#2907](https://github.com/sipeed/picoclaw/pull/2907))：解决了进程在写入 `.jsonl` 文件与更新 `.meta.json` 之间崩溃导致的数据不一致问题。
- **回退链上下文处理修复** ([#2905](https://github.com/sipeed/picoclaw/pull/2905))：修复了当请求超时后，回退链仍会徒劳尝试后续候选 Provider 的问题，现在会立即终止。

### 平台兼容性

- **Windows 子进程控制台闪烁修复** ([#2654](https://github.com/sipeed/picoclaw/pull/2654))：修复了 `picoclaw-launcher.exe` 在 Windows 上反复弹出/关闭 PowerShell 控制台窗口的 UX 回归问题。
- **Windows 构建流程修复** ([#2487](https://github.com/sipeed/picoclaw/pull/2487))：移除了 Windows 构建中的 Unix-only 假设，确保 `make build` 流程在 Windows 上能够成功执行。
- **跨平台串口工具支持** ([#2673](https://github.com/sipeed/picoclaw/pull/2673))：新增了内置的 `serial` 硬件工具，并提供了 Linux、macOS、Windows 三平台的实现，已集成到运行时工具注册表和仪表盘配置中。

### Web UI 与交互体验

- **端到端流式支持** ([#2587](https://github.com/sipeed/picoclaw/pull/2587))：为 Pico Web 聊天体验增加了完整的流式支持，并重构了前端的聊天渲染和滚动行为。
- **思考过程可见性切换** ([#2661](https://github.com/sipeed/picoclaw/pull/2661))：在聊天 UI 中增加了切换按钮，允许用户显示或隐藏模型的思维链/推理消息，偏好设置会持久化到本地存储。
- **配置保存与重启反馈** ([#2663](https://github.com/sipeed/picoclaw/pull/2663))：改进了配置页面的保存与重启反馈，让用户在不同配置变更后能获得清晰的系统状态提示。
- **Provider Logo 回退修复** ([#2908](https://github.com/sipeed/picoclaw/pull/2908))：修复了模型配置页面在后端元数据重构后无法正确显示 Provider 图标的回归问题。

### 配置与管理

- **恢复出厂设置功能** ([#2891](https://github.com/sipeed/picoclaw/pull/2891))：新增了 "Reset to Factory Defaults" 功能，可备份当前配置、恢复默认配置并保留 API 密钥，为版本间的配置不兼容提供了恢复手段。
- **模型配置工作流大改** (三部曲 [#2831](https://github.com/sipeed/picoclaw/pull/2831), [#2832](https://github.com/sipeed/picoclaw/pull/2832), [#2833](https://github.com/sipeed/picoclaw/pull/2833))：这是当前版本升级的重头戏，统一重构了模型配置的后端 API 和前端 UI，包括 Provider 选择、模型表单 CRUD、上游模型拉取、模型目录管理以及连接性测试功能。

### Provider 与通道

- **MiMo Provider 模型支持** ([#2915](https://github.com/sipeed/picoclaw/pull/2915))：为 `mimo` Provider 新增了 `mimo-v2.5`（多模态，支持图像理解）和 `mimo-v2.5-pro`（纯文本）模型，帮助 WebUI 默认推荐正确的模型以避免用户向纯文本模型发送图片。
- **飞书通道增强** ([#2607](https://github.com/sipeed/picoclaw/pull/2607))：为飞书通道增加了 `group_trigger.mention_only` 选项，使机器人仅在群聊中被 @ 时才响应，并新增了随机 emoji 响应的前端配置。

### 文档

- **V3 配置格式文档同步** ([#2766](https://github.com/sipeed/picoclaw/pull/2766))：同步更新了 26 个文件，以匹配新的 V3 配置格式变更（如 `api_key` -> `api_keys`，`channels` -> `channel_list`）。

---

## 社区热点

### 最活跃 Issue
- **[#3012] Continuous consumption of tokens every minutes when evolution is enabled** ([链接](https://github.com/sipeed/picoclaw/issues/3012))
    - **热度**: 5 条评论，持续两周讨论
    - **分析**: 该问题报告当启用 Evolution 功能后，Token 会持续被消耗。这是用户最关注的“烧钱”类问题之一，涉及到使用成本，社区关注度高。目前仍处于开放状态，尚无明确的 Fix PR 关联，建议维护团队优先排查。

### 新报 Bug 受关注
- **[#3153] Volcengine Doubao Seed tool calls occasionally leak as text** ([链接](https://github.com/sipeed/picoclaw/issues/3153))
    - **热度**: 今日新开 Issue
    - **分析**: 问题直指国产模型（豆包）的工具调用稳定性。当工具调用结果泄漏为纯文本而非执行时，会导致自动化流程完全中断，这对依赖 Agent 能力的用户影响较大。

---

## Bug 与稳定性

按严重程度排列如下：

| 严重程度 | Issue/PR | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | [#3153](https://github.com/sipeed/picoclaw/issues/3153) | **Volcengine Doubao Seed 工具调用偶尔泄漏为 `<seed:tool_call>` 文本**，导致 Agent 无法正确执行工具。 | 🔴 新开，无 Fix |
| **高** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | **Evolution 启用后每分钟持续消耗 Token**，直接影响用户使用成本，属于严重的计费/资源浪费问题。 | 🟡 开放中，未修复 |
| **中** | [#3044](https://github.com/sipeed/picoclaw/issues/3044) | **Matrix 用户 ID 包含冒号时 `allow_from` 白名单失效**，消息被错误静默拒绝。 | 🟢 已关闭 |
| **中** | [#3041](https://github.com/sipeed/picoclaw/issues/3041) | **`mcp add` 命令错误解析全局标志为位置参数**，导致 HTTP/SSE 添加失败并错误命名 stdio 服务。 | 🟢 已关闭 |
| **低** | [#3090](https://github.com/sipeed/picoclaw/issues/3090) | **iOS 16.4 以下版本 Safari 浏览器无法打开 PicoClaw 面板**，影响旧设备用户访问。 | 🟡 开放中，未修复 |

---

## 功能请求与路线图信号

| Issue | 描述 | 分析 |
| :--- | :--- | :--- |
| [#3093](https://github.com/sipeed/picoclaw/issues/3093) | **请求增加 SimpleX、Tox 或 Wire 网关通道** | 这表明社区对**去中心化/隐私优先的通信协议**有明确需求。目前 PicoClaw 已支持 Signal、Matrix 等，加入 SimpleX/Tox 可进一步拓展其在隐私敏感用户群中的覆盖。结合当前 PR 重点在核心稳定性和配置 UI 上，此功能更可能被排入 v0.4.0 或之后的路线图。 |

---

## 用户反馈摘要

- **对 Token 消耗敏感**: 用户在 [#3012](https://github.com/sipeed/picoclaw/issues/3012) 中强烈反馈 Evolution 功能导致的持续 Token 消耗问题，这表明用户非常关注 AI 功能的实际运营成本。任何可能产生意外费用的 Bug 都会引发高度焦虑。
- **国产模型使用障碍**: 用户 `ms8great` 在 [#3153](https://github.com/sipeed/picoclaw/issues/3153) 中报告了 Volcengine（火山引擎）豆包模型的工具调用问题，说明国产大模型接入的稳定性是用户关注的痛点，同时也是 PicoClaw 扩大国内用户群的重要发力点。
- **兼容性诉求**: 用户 `Damian-o2` 在 [#3093](https://github.com/sipeed/picoclaw/issues/3093) 中直接提出对隐私通信协议的支持请求，反映出部分用户不仅将 PicoClaw 视为工具，更看中其作为一个**隐私友好的通信网关**的潜力。
- **历史遗留 Bug 修复积极**: 从今日合并的大量 PR 来看，开发团队正在系统性地清理 V3 版本过渡期间引入的各类问题（如配置格式、Logo 显示、Windows 兼容性等），这对于提升现有用户的满意度至关重要。

---

## 待处理积压

以下为开放超过 10 天且无明确 Fix PR 关联的重要 Issue，建议维护团队关注：

- **[#3012] [BUG] Continuous consumption of tokens every minutes when evolution is enabled** ([链接](https://github.com/sipeed/picoclaw/issues/3012))
    - **创建**: 2026-06-05 | **已开放**: 17 天 | **评论**: 5
    - **风险**: 高。该问题影响用户的钱包，积压时间较长，可能导致用户流失或放弃使用 Evolution 功能。
- **[#3093] [Feature] I need SimpleX or tox** ([链接](https://github.com/sipeed/picoclaw/issues/3093))
    - **创建**: 2026-06-10 | **已开放**: 12 天 | **评论**: 2
    - **风险**: 中。虽然是一个功能请求，但社区对此有明确的呼声，长期搁置可能影响项目在隐私社区中的口碑。
- **[#3090] [BUG] Panel does not work on Safari on iOS versions below 16.4** ([链接](https://github.com/sipeed/picoclaw/issues/3090))
    - **创建**: 2026-06-10 | **已开放**: 12 天 | **评论**: 2
    - **风险**: 低。影响范围较窄（旧版本 iOS Safari），但作为一个明确的兼容性 Bug，建议在下一个 Patch 版本中修复。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

过去 24 小时内，NanoClaw 收到 **2 个安全漏洞报告**（均为 OPEN 状态），**7 个 PR 有活动**（其中 3 个已合并/关闭，4 个待合并），无新版本发布。项目维护侧响应较快：两个安全 Issue 提交后已获得 triage，多项修复 PR 被合入或正在 review。社区互动方面暂无明显讨论（评论数均为 0），整体活跃度中等偏高，但安全风险的披露使项目健康度面临一定压力。

## 2. 版本发布

无

## 3. 项目进展

今日 **3 个 PR 被关闭/合并**，推进了多项稳定性与兼容性修复：

- **#2825 – fix(setup): wait for the host socket before failing the first chat**（已关闭）  
  修复了 setup 首次聊天步骤过早检测 host socket 导致的假失败问题。当 `service` 步骤完成后，host 进程可能尚未完成 socket 绑定，现在会等待 socket 就绪再继续，提升首次启动成功率。  
  [nanocoai/nanoclaw PR #2825]

- **#2168 – fix(container): pin host.docker.internal to OneCLI's bridge IP in rootless Docker**（已关闭）  
  在 rootless Docker 环境下，将 agent 容器的 `host.docker.internal` 映射固定到 OneCLI 的 bridge IP，避免依赖 `host-gateway` 在 rootless 模式下失效的问题，提升了容器网络兼容性。  
  [nanocoai/nanoclaw PR #2168]

- **#2829 – [follows-guidelines] eee**（已关闭）  
  标题与内容格式异常（仅填写模板），疑似测试或无效提交，已被关闭。建议维护者检查该提交来源，确保 CI 流程能过滤此类 PR。  
  [nanocoai/nanoclaw PR #2829]

此外，仍有 **4 个 PR 处于待合并状态**，涵盖新技能、轮询优化、卸载残留清理等功能（详见下文），项目整体在稳定性、工具生态和工程健壮度上持续推进。

## 4. 社区热点

今日暂无高互动讨论（所有 Issue/PR 评论数均为 0），但 **两个新安全 Issue 值得重点关注**：

- **#2828 – [Security] NanoClaw A2A attachment forwarding follows a symlinked inbox and writes outside the target session root**  
  报告了 A2A 附件转发机制中，被入侵的 agent 可通过替换 `inbox/` 为符号链接，使其他 agent 向任意路径写入文件。这是一个典型的 **symlink 越界写**漏洞，严重性高。目前无 fix PR，需尽快评估攻击面。  
  [nanocoai/nanoclaw Issue #2828]

- **#2827 – [Security] `add_mcp_server` approval flow hides runtime `args` and `env`, enabling approval smuggling**  
  指出 `add_mcp_server` 自修改流程在审批卡片中仅显示 MCP server 名称，隐藏了实际运行的 `args` 和 `env`，使得恶意参数可通过审批检查。属于 **approval bypass** 风险，同样暂无修复 PR。  
  [nanocoai/nanoclaw Issue #2827]

两个漏洞均由安全研究者 **YLChen-007** 提交，说明项目已进入外部安全审计视野。虽然暂无评论，但结合漏洞性质，社区内部可能已有警惕呼声，维护者宜优先处理。

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | 条目 | 说明 | 是否有 Fix PR |
|----------|------|------|---------------|
| **Critical** | #2828 – symlink 越界写 | A2A 附件转发可被引导至 session 外任意路径写入 | 无 |
| **High** | #2827 – MCP 审批参数隐藏 | `add_mcp_server` 审批界面不展示 `args`/`env`，可绕过人工审核 | 无 |
| Medium | #2825（已合并） | 首次聊天因 host socket 未就绪而失败 | 已修复 |
| Low | #2531（待合并） | 轮询循环中 `send_message` 在中间触发导致重复文本 | PR #2531 |
| Low | #2830（待合并） | 删除项目后遗留的 launchd/systemd 单元持续尝试启动已不存在的二进制 | PR #2830 |
| Low | #2826（待合并） | `/update-nanoclaw` 步骤 7 中技能更新提示可跳过，导致用户遗漏上游修复 | PR #2826 |
| Low | #2168（已合并） | rootless Docker 下 host.docker.internal 映射失效 | 已修复 |

**特别提醒**：#2828 和 #2827 暂无任何修复关联 PR，且涉及核心安全机制，应上升为项目最高优先级。

## 6. 功能请求与路线图信号

- **#2795 – feat: add /add-clidash — read-only CLI-derived dashboard skill**（OPEN）  
  提案新增一个基于 CLI 的只读仪表盘技能，属于 Utility skill，无需改动源码。该 PR 从 6 月 17 日开放，社区已有一定关注（虽然无评论）。若合入将扩展 NanoClaw 的运维工具集。  
  [nanocoai/nanoclaw PR #2795]

- **#2826 – fix(update-skills): nudge into skill updates, rebuild container on re-apply**（OPEN）  
  虽然归类为 fix，其实是对 `/update-nanoclaw` 流程的改进：不再让技能更新“可跳过”，并在重新应用时重建容器，避免用户遗漏信道/提供者的重要修复。这反映了项目正推动 **更可靠的用户升级体验**，可能为后续版本强制技能更新铺路。  
  [nanocoai/nanoclaw PR #2826]

- **#2830 – fix(setup): reap dead peer service registrations**（OPEN）  
  提出了清理僵尸注册的机制，属于基础设施健壮性增强。此类改进通常会在下一个 patch 版本中纳入。  
  [nanocoai/nanoclaw PR #2830]

整体来看，近期路线图信号偏向 **安全性修补**（因新漏洞报告）和 **生命周期管理**（升级、清理、网络兼容），功能特性方面仅有 #2795 一项新增。

## 7. 用户反馈摘要

今日所有 Issue 和 PR **评论数均为 0**，暂无来自用户的直接反馈或使用体验描述。两个安全漏洞报告虽暂无讨论，但披露形式规范、细节完整，说明报告者有较深的使用或审计背景。建议维护团队主动联系报告者以获取更多复现细节，同时鼓励社区参与讨论。

## 8. 待处理积压

以下条目虽不一定是今日热点，但因其存在时间较长或状态异常，提醒维护者关注：

- **#2531 – fix(poll-loop): suppress duplicate text when send_message fires mid-turn**（OPEN，自 2026-05-18）  
  轮询重复文本修复，已开放超过一个月且最近有更新（6 月 22 日），仍未被合入。长期积压可能导致用户持续遇到此问题，建议尽快 review 并合并。  
  [nanocoai/nanoclaw PR #2531]

- **#2795 – feat: add /add-clidash**（OPEN，自 2026-06-17）  
  新技能 PR 滞留约 5 天，无评论或更新，若无冲突应加速推进以避免分支偏离。

- **#2829 – 异常 PR（已关闭）**  
  标题仅为 “eee”，内容为模板填写，已关闭。需确认是否为恶意提交或测试遗漏，建议 CI 加入模板校验机制。

- **安全漏洞积压（#2827、#2828）**  
  两个严重漏洞无任何关联 PR，也未看到维护者回复。此类问题若长时间无人问津，会极大影响项目声誉。建议迅速响应，发布安全公告并开始修复。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是根据 2026-06-22 的 GitHub 数据生成的 NullClaw 项目动态日报。

---

### NullClaw 项目动态日报 | 2026-06-22

#### 1. 今日速览
过去24小时内，NullClaw 项目整体活跃度较低。开发侧无任何 Pull Request 合并或新版本发布，代码状态趋于平稳。社区侧仅有一条 Issue 动态，但该 Issue（#967）涉及核心功能的高频崩溃（概率 >50%），严重程度较高。当前项目处于“开发停滞、社区警觉”的状态，维护者需优先关注该稳定性问题，避免影响用户信任。

#### 2. 版本发布
*[无]*

#### 3. 项目进展
过去24小时内，无 Pull Request 被合并或关闭。项目核心主干分支未发生任何代码变更，功能推进与 Bug 修复工作暂时停滞。

#### 4. 社区热点
截至目前，社区讨论焦点全部集中在以下一个 Issue：
- **Issue [#967] [Bug] error: NoResponseContent**
  - **链接:** [https://github.com/nullclaw/nullclaw/issues/967](https://github.com/nullclaw/nullclaw/issues/967)
  - **热度分析:** 这是过去24小时内唯一的动态来源。虽然仅有1条评论，但问题性质极其严重。
  - **诉求分析:** 用户在最新稳定版（v2026.5.29）上运行核心 `agent` 命令时，错误率高达约57%（21次对话出现12次）。用户明确提到同样的模型与 API Key 在 PicoCLI 中工作正常，暗示这极有可能是 NullClaw 主程序近期更新引入的**回归性 Bug**，严重影响基础体验。

#### 5. Bug 与稳定性
当前待处理的高风险 Bug 如下：
- **Bug #967 [严重] agent 核心功能高频崩溃**
  - **环境:** Windows 11, v2026.5.29, 模型 `Agnes-2.0-Flash`。
  - **问题表现:** 执行 `nullclaw agent -m “你好！”` 后，27秒左右的响应等待后返回空内容错误 `error: NoResponseContent`。
  - **重现概率:** >50%。
  - **关联修复 PR:** 无。目前尚未有维护者或协作者回复该 Issue，也无可用的临时修复补丁。

#### 6. 功能请求与路线图信号
过去24小时内，社区未提出任何新功能请求。当前用户反馈全部聚焦于阻塞性 Bug 的修复，未产生与项目路线图相关的新信号。

#### 7. 用户反馈摘要
- **真实痛点:** 用户的核心痛点在于**高频率的随机性失败**。尽管单次响应速度尚可（27秒），但超过50%的失败率导致该工具在真实对话场景中完全不可用。错误信息 `NoResponseContent` 过于模糊，缺乏具体调试信息（如底层 HTTP 状态码、模型返回片段等），用户难以自行排查。
- **使用场景:** 用户正在进行最基础的 Agent 功能对话测试。
- **不满与对比:** 用户对最新版相比外部工具（PicoCLI）表现出的不稳定性感到困惑和失望，高频的 Bug 体验正在快速消耗用户对项目的信任。

#### 8. 待处理积压
虽然过去24小时暂无长期积压的旧 Issue，但以下 Issue 存在潜在的“维护者响应延迟”风险：
- **Issue #967**: 创建于 2026-06-20，最近更新于 2026-06-21。
  - **状态:** **严重待响应**。截至报告撰写时（06-22），该高严重性 Bug 尚未获得任何官方回复。建议维护者尽快尝试复现，或向用户索取完整日志与 API 交互的调试数据（如完整的 HTTP 请求/响应体），以便明确是 Agent 循环逻辑错误还是底层 API 兼容性变更导致的问题。该问题的紧迫性极高。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，分析师已就位。以下是基于 `nearai/ironclaw` GitHub 数据生成的 IronClaw 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

过去 24 小时，IronClaw 项目维持了极高的开发活跃度。核心聚焦于 **Reborn** 架构的稳定性与功能完善，同时大规模重构了 CI 基础设施以解决长期存在的流水线可靠性问题。数据显示，PR 更新数量达到了 **29 条**，其中合并/关闭 **14 条**，核心团队 (Core) 和自动化机器人 (Dependabot) 贡献了大量提交。尽管昨日没有版本发布，但多项关键修复（如 NEAR AI MCP 状态误报、Google OAuth 刷新）已进入主线，有效提升了用户体验。项目整体健康度良好，对新功能（如学习系统、并发执行）的探索正在加速，但 `Nightly E2E` 的长期失败依然是悬而未决的稳定性隐患。

## 2. 版本发布

昨日无新版本发布。

## 3. 项目进展

昨日项目在修复 Bug 和完善核心特性上迈出了坚实的一步，具体进展如下：

*   **Reborn 核心修复**:
    *   **修复 MCP 扩展就绪状态**：合并了 **[#4990]**，解决了 NEAR AI MCP 就绪后 UI 仍显示“需要配置”的困扰，直接关闭了社区反馈的 **[#4925]**，显著提升了 MCP 扩展的管理体验。
    *   **修复首次启动频道激活**：合并了 **[#2927]**，修复了全新安装后部分 WASM 频道无法自动激活的回归问题。
*   **Reborn 自动化功能完善**:
    *   **一次性定时触发器**：合并了 **[#5065]**，新增 `TriggerSchedule::Once` 功能，允许用户精确地设置“仅执行一次”的自动化任务，补全了定时触发器生态。
*   **CI / 基础设施重构**:
    *   **缓存优化**：合并了 **[#5118]**，将 Reborn Crate 测试矩阵从“每 crate 独立缓存”改为“共享缓存”，彻底解决了因 LRU 逐出策略导致的大规模重新下载和 CI 环境不稳定问题。
    *   **网络稳定性**：合并了 **[#5115]**，通过配置 `CARGO_NET_RETRY` 机制，增强了从 crates.io 下载依赖时的网络故障容错性。
    *   **流水线解耦**：合并了 **[#5113]**，将跨平台/兼容性测试任务从主 `test.yml` 中抽离，形成独立的 `platform-and-compat.yml` 工作流，提升了 CI 配置的可维护性。
    *   **合入门禁**：合并了 **[#4830]**，现在合入队列也会执行 Reborn E2E 测试，防止不稳定的代码突破主干。

## 4. 社区热点

昨日社区讨论热度主要集中在设计统一性、新特性推进和长期稳定性上。

*   **设计一致性讨论 (新开热点)**：**[#5120]** “统一门控拒绝语义” 是昨日新开的热门 Issue。社区正在激烈讨论如何统一 WebUI、审批、授权和 Turn 运行中各种“拒绝”状态（Declined/Deny/Canceled），这直接关系到跨模块交互的一致性和开发者的理解成本。
*   **本地体验深度追踪**：**[#5119]** “本地 Dogfooding 发现” 被设定为本周持续追踪的热点。该项目动态捕捉开发者在日常使用 IronClaw Reborn 自建版本时遇到的所有首次运行问题，是反馈最密集、最贴近真实体验的窗口。
*   **大规模功能推进**：
    *   **[#4975]** (WS-3 反思服务) 作为 Reborn 学习系统的第三部分，虽然处于开发中，但其 XL 级别的体量和设计复杂度引起了广泛内部讨论。
    *   **[#5109]** (Composio 连接器) 作为新贡献者提交的 Draft PR，旨在为 Workbench 打通外部服务商连接能力，是向开放生态迈出的重要一步，但暂无评论互动。
*   **Dependabot 集群**：大量依赖更新 PR (`#5116`, `#4002`, `#5114` 等) 占据了 PR 列表，虽然讨论热度不高，但它们是维护者需要尽快处理的技术债务。

## 5. Bug 与稳定性

*   **高风险 - 已修复**：
    *   **Google OAuth 令牌过期**：**[#5071]** 已关闭。修复了因令牌生命周期短（1小时）导致的重认证问题，通过 Refresh Token 机制实现了静默续期。
*   **中风险 - 已修复**：
    *   **MCP 配置误报**：**[#4925]** 已关闭（合并于 **#4990**）。
    *   **频道激活失败**：**[#2927]** 已关闭。
*   **持续关注中**：
    *   **Nightly E2E 测试失败**：**[#4108]** 仍处于开启状态，自 5 月 27 日以来已多次报告失败。尽管昨日合并的多个 CI 优化 PR 正是为了根治此问题，但当前 Issue 尚未关联具体的修复 PR，需持续观察后续 CI 运行结果。
    *   **语义设计缺陷**：**[#5120]** 虽然不直接导致运行时崩溃，但当前“拒绝”语义的混乱是开发者在集成 Auth/Approval 模块时感知到的设计 Bug，需要尽快统一实现。

## 6. 功能请求与路线图信号

从昨日的 PR 和 Issue 中，可以清晰看到项目向“更强智能、更高性能、更易托管”发展的路线图信号。

*   **学习能力 (Learning System)**：WS-1 (**[#4937]**) 和 WS-3 (**[#4975]**) 的更新表明，“让 Agent 从错误中学习”是下一阶段最核心的智能升级方向，Hermes 级别的反思机制即将落地。
*   **并发处理能力**：**[#5085]** “并发 Turn 执行调度器” 将打破当前的串行执行瓶颈，允许同时处理多个 LLM 推理任务。这对于提升高并发场景下的 Agent 响应速度和吞吐量至关重要。
*   **托管服务准备**：**[#5081]** “托管单租户 Postgres 配置” 的提出和推进，表明 Reborn 架构正在明确为云端托管版本做准备，增加了对 PostgreSQL 的支持配置。
*   **自动化增强**：**[#5117]** 提出的“已完成任务摘要卡”直接呼应了刚合并的一次性触发器 (**#5065**)，预计将在下一个小版本中落地，丰富自动化看板的信息密度。

## 7. 用户反馈摘要

*   **痛点改善**：
    *   **“MCP 插件已就绪，UI 却说需要配置”**：该抽象层的感知错误昨日已通过 **[#4990]** 修复，重度 MCP 用户的体验将得到极大提升。
    *   **“新安装后频道不工作”**：**[#2927]** 的合并解决了新用户首次启动时的困惑，降低了使用门槛。
*   **使用场景扩展**：
    *   用户对“一次性定时任务”的需求非常强烈，**[#5065]** 的合入精准满足了此类精细化的自动化场景（如：定期清理、一次性的通知提醒）。
    *   Google OAuth 刷新机制的改进直接提升了重度 GSuite 用户的持续使用体验，避免了日常工作流的中断。
*   **对稳定性诉求**：
    *   CI 的不稳定性是开发者最大的摩擦点。昨日的集中投入（缓存、重试、E2E门禁）表明团队已正面回应这一诉求。

## 8. 待处理积压

以下为存在较长周期未得到有效闭环的 Issue 或 PR，提醒维护团队关注：

*   **[高优先级] [#4108] Nightly E2E 测试失败**：历时近一个月，虽无直接关联的修复 PR，但昨日的 CI 基础设施优化正是以此为靶心。建议在验证优化效果后，通过该 Issue 进行闭环回复并关闭。
*   **[行动项] [#4002] Actions 依赖批量更新**：自 5 月 24 日开启，包含 16 个 Action 的重大版本跳跃（如 `actions/checkout` 从 v4 到 v7）。由于涉及 CI 核心组件，需尽快评估风险并合并，避免长期偏离主干。
*   **[行动项] [#4032] WASM 依赖更新 & [#4498] serde\_yml 依赖更新**：属于常规生态依赖升级，已分别存在 28 天和 17 天。建议在 CI 缓存问题解决后统一进行批量合并，避免版本落后带来的生态兼容性风险。

---
*数据来源：GitHub Issue 和 PR 元数据，更新截止于 2026-06-22。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，LobsterAI 项目动态日报已按您的要求生成。

---

# LobsterAI 项目动态日报 (2026-06-22)

**项目名称：** LobsterAI (netease-youdao/LobsterAI)
**报告周期：** 2026-06-21 ~ 2026-06-22
**生成时间：** 2026-06-22

---

### 1. 今日速览

过去24小时内项目主要进行了大规模的技术债务清理工作，共关闭了14个标记为 `[stale]` 的旧Issue，涉及多个未被修复的Bug和功能请求。这反映出团队正在积极进行代码库和Issue列表的维护。然而，没有新的Pull Request被合并或提交，表明新功能开发或Bug修复的代码产出暂时停滞。同时，一个涉及SSRF安全防护级别削弱的新Issue (#2181) 被提出，为项目引入了新的安全风险考量。项目整体活跃度评估为：**中等（维护清理活跃，但开发节奏放缓）**。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无 Pull Request 被合并或关闭，代码层面的功能推进处于停滞状态。

但在项目管理方面有重大进展：**14个长期未被解决的 `[stale]` Issue 被一次性关闭**。这虽然不代表这些Bug被修复或功能被实现，但有效地清理了项目积压，使得当前待处理问题的列表更具时效性。这些被关闭的Issue涵盖了从Bug（如#1500、#1502）到功能请求（如#1525、#1541）等多个方面。

- **CI/配置修复：** 一个与CI配置相关的Issue (#1518) 被关闭，该Issue本意在修复labeler工作流的权限问题并规范lint策略，虽未合并PR，但其关闭也标志着该问题已被标记。

### 4. 社区热点

本期社区讨论热度较低，大部分Issues都因标记为 `[stale]` 而缺乏活跃讨论。唯一值得关注的是新提交的Issue。

- **新增的安全风险讨论:**
    - **#2181 [Security] LobsterAI restores private-network browser access by default and weakens the bundled OpenClaw SSRF guard** (作者: YLChen-007 | 评论: 0)
    - **链接:** [netease-youdao/LobsterAI Issue #2181](https://github.com/netease-youdao/LobsterAI/issues/2181)
    - **分析:** 这是过去24小时内唯一新开的Issue，而且是**安全相关**。作者指出LobsterAI默认启用`ProxyCompatible`模式，会允许访问私有网络，并削弱了集成的OpenClaw SSRF防护。这是对项目安全模型的直接挑战，可能会成为社区后续一段时间内讨论的核心。

### 5. Bug 与稳定性

今日未发现新的Bug报告。被关闭的14个`[stale]` Issue中包含大量之前已被报告的Bug。按严重程度排列如下：

| 严重程度 | Issue ID | 问题描述 | 状态 / 备注 |
| :--- | :--- | :--- | :--- |
| **严重** | #2181 | SSRF安全防护被削弱，默认暴露私有网络访问权限。 | **[新提交]** / 无修复PR，为项目引入潜在安全风险。 |
| **高** | #1516 | 关闭Settings面板时未取消GitHub Copilot OAuth轮询，导致授权Token静默丢失。 | 已关闭 (`stale`) |
| **高** | #1506 | 定时任务选择IM通知频道后，未选择会话即可提交，导致静默失败。 | 已关闭 (`stale`) |
| **中** | #1500 | 禁用技能后，其ID仍存在于 `activeSkillIds` 中，在对话中继续被调用。 | 已关闭 (`stale`) |
| **中** | #1502 | Agent设置面板保存技能列表后，当前会话不同步，需切换Agent才能生效。 | 已关闭 (`stale`) |
| **低** | #1504 | IM机器人AES Key缺少必填校验，空值也能保存。 | 已关闭 (`stale`) |
| **低** | #1512 | QQ Bot群组白名单缺少添加输入框，无法通过UI配置。 | 已关闭 (`stale`) |

### 6. 功能请求与路线图信号

今日没有新的功能请求被提出。但值得注意的是，**一批包含明确功能诉求的Issues已被关闭**，这或许暗示着项目维护者对这些功能的当前优先级判定。

- **被关闭的功能请求（`[stale]`）：**
    - #1525 会话列表增加颜色标注功能
    - #1528 批量模式支持导出多个会话
    - #1532 设置页面增加本地会话使用统计
    - #1537 支持消息收藏/书签功能
    - #1541 会话列表增加标签分类和筛选功能

- **分析:** 这五个Issues全部是关于增强**会话（Session）管理体验**的，且均来自同一位用户。诉求涵盖了视觉区分、数据管理、使用统计和信息标记等多个维度，构成了一个相对完整的用户体验改进包。尽管目前被关闭，但若维护者未来计划提升产品在“数据管理和信息检索”方面的能力，这批Issues具有极高的参考价值，极有可能被纳入某个版本规划中。

### 7. 用户反馈摘要

从被关闭的Issues中，可以提炼出过去一段时间用户的集中反馈：

- **对AI能力一致性的关注：** #1509 的作者提出了一个核心痛点，即相同模型在LobsterAI和OpenClaw中表现不一致，且缺少中间过程展示，让用户感到困惑和不可控。
- **对操作反馈和数据同步的严格要求：** #1500、#1502、#1504、#1506 等多项报告都集中在 **“操作后未同步或未生效”** 的问题上，例如禁用技能不生效、保存后不更新、表单校验缺失导致静默失败等。这表明用户对操作的确定性和系统的反馈机制有很高要求。
- **对规范化内容和设计的期待：** #1513 指出“声明条款”页面存在序号重复、括号不完整等规范问题，反映了用户对产品质量和细节的关注。
- **对高级信息管理功能的强烈渴望：** #1525、#1528、#1532、#1537、#1541 等一连串来自同一位用户的反馈，系统地表达了对会话管理、数据统计、信息标记等进阶生产力功能的向往。这表明部分用户已不满足于基础对话，开始将LobsterAI视为知识库工具。

### 8. 待处理积压

- **安全风险提醒（急迫）：** **[OPEN]** #2181 安全漏洞报告。该Issue目前无任何回复、标签或指配。
    - **链接:** [netease-youdao/LobsterAI Issue #2181](https://github.com/netease-youdao/LobsterAI/issues/2181)
    - **提醒:** 该Issue涉及关键的安全风险，建议维护者优先关注并回应，确认漏洞有效性并制定修复计划，以避免潜在的项目使用风险。

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

好的，以下是为您生成的 CoPaw 项目动态日报（2026-06-22）。

---

# CoPaw 项目动态日报 | 2026-06-22

## 今日速览

- **高度活跃的维护状态**：过去24小时内，项目共产生55次更新（18 Issues + 37 PRs），社区与维护者互动频繁，项目处于快速迭代期。
- **关键Bug确认与紧急修复**：社区报告的多个核心Bug（如消息队列串台、会话切换卡死、图片显示异常）已被开发者确认并提交了修复PR，修复响应迅速（`#5371`, `#5357`, `#5324`）。
- **移动端适配成为社区热点**：多个用户提交了关于移动端UI优化的PR（`#5369`, `#5362`, `#5364`, `#5367`），表明社区对移动端体验有强烈诉求，项目正向多端适配迈进。
- **稳定性与测试被强调**：有社区成员明确提出“先稳定核心再添加新功能”的呼声（`#5360`），同时也有资深贡献者提交了覆盖6个模块的大规模E2E测试PR（`#5372`），表明项目健康度正在被主动维护。
- **无新版本发布**：尽管社区活跃，但昨日未发布新版本，所有修复和改进仍在待合并的分支中。

## 项目进展

今日合并/关闭了5个PR，并有多项重要修复处于待合并状态，项目在核心稳定性、测试覆盖和UI体验上均有显著推进。

| PR / Issue | 链接 | 类型 | 关键进展 |
| :--- | :--- | :--- | :--- |
| **PR #4900** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/4900) | 合并 | **修复插件加载器未初始化问题**：解决了Tauri桌面版因PyInstaller冻结环境导致插件加载器超时、无法安装或启用插件的根本原因。 |
| **PR #5270** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5270) | 合并 | **大规模集成测试**：完成了涵盖ACP运行器、插件系统、安全、跨域等四个领域的64个集成测试用例，显著增强了Sprint 3周期的功能可靠性。 |
| **PR #3831** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/3831) | 关闭 | **向量模型连接测试功能**：一项历史PR最终被处理并关闭，为模型配置模块添加了基础的连接测试能力。 |
| **PR #5324** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5324) | 待合并 | **修复图片预览回归**：通过修改文件响应头（`Content-Disposition`），直接修复了`v1.1.12`升级后`send_file_to_user`无法在聊天窗口内显示图片的Bug（`#5320`）。 |
| **PR #5371** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5371) | 待合并 | **修复消息队列串台**：通过将Agent ID绑定到队列消息中，从根源上解决了切换Agent时，消息错误发送到错误Agent的问题（`#5354`）。 |

**项目向前迈进总结：**
- **稳定根基**：插件系统初始化问题的解决和大量集成测试的加入，为项目未来功能迭代提供了更稳固的基础。
- **开发效率**：消息队列并发执行中的核心Bug得到修复，提升了用户使用时的流畅度和可靠性。
- **社区赋能**：多位首次贡献者（`yaozy2020`, `lecheng2018`）提交了移动端页面适配的PR，展示了良好的社区共建生态。

## 社区热点

今日讨论最活跃的议题集中在用户体验和核心功能回归上。

1.  **消息队列串台与会话切换卡死**
    - **Issues**: [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) (4条评论)
    - **PR**: [#5371](https://github.com/agentscope-ai/QwenPaw/pull/5371), [#5357](https://github.com/agentscope-ai/QwenPaw/pull/5357)
    - **分析**：这是今日最受关注的功能类Bug。用户`renzhong424`详细描述了`v1.1.12.post1`版本中消息队列在切换Agent时“串台”的痛点。此问题直接影响了多Agent协同工作的体验。开发者在报告后数小时内即提交了`#5371`修复PR，响应速度极快。同时，`#5357`也在修复因相同原因引起的会话切换卡死问题。这体现了社区对刚上线功能的快速反馈和开发者的敏捷响应。

2.  **升级后“内置技能”被重置为启用**
    - **Issue**: [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) (8条评论)
    - **分析**：这是一个长期困扰用户的回归Bug。用户`daigoopautoy`再次报告，每次升级后，手动禁用的内置技能（如`docx`, `xlsx`）都会被重置为启用状态。该问题已在`#4807`中被提出，但似乎尚未得到根本解决。8条评论表明许多用户都遇到了同样的问题，这是一个影响用户配置持久化体验的重要痛点，需要维护者高度关注。

3.  **移动端UI体验与功能缺失**
    - **Issue**: [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) (5条评论)
    - **PR**：多个移动端适配PR（如[#5369](https://github.com/agentscope-ai/QwenPaw/pull/5369), [#5362](https://github.com/agentscope-ai/QwenPaw/pull/5362)）
    - **分析**：用户`bob-geek11`通过手机浏览器访问后端，提出了具体的UI改进建议，例如在侧边栏简洁模式下添加“切换Agent”按钮。此需求获得了开发者和社区成员的积极回应。当前已有多个针对不同页面的移动端适配PR提交，这反映了项目社区对“随时随地使用”的强烈需求，也是项目未来发展的重要方向。

## Bug 与稳定性

过去24小时报告的Bug数量较多，按严重程度排列如下：

| 严重程度 | Issue / PR | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) | **消息队列串台**：切换Agent后，消息错误地发送给其他Agent。 | **已有修复PR** [#5371](https://github.com/agentscope-ai/QwenPaw/pull/5371) |
| **高** | [#5344](https://github.com/agentscope-ai/QwenPaw/issues/5344) | **API消息静默丢弃**：`/api/console/chat`返回200成功，但当Agent忙碌时，消息被静默丢弃，未进入处理流程。 | 待修复 |
| **高** | [#5358](https://github.com/agentscope-ai/QwenPaw/issues/5358) | **前端崩溃**：切换会话时，浏览器控制台报`TypeError`错误，导致UI无响应。 | 待修复 |
| **中** | [#5373](https://github.com/agentscope-ai/QwenPaw/issues/5373) | **Shell命令解析异常**：`execute_shell_command`工具无法解析管道符、重定向等标准Shell语法。 | 待修复 |
| **中** | [#5370](https://github.com/agentscope-ai/QwenPaw/issues/5370) | **文件预览404**：`send_file_to_user`生成的预览链接因路径解析错误导致HTTP 404。 | 待修复 |
| **中** | [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) | **智谱API模型级连接失败**：供应商级别测试成功，但所有模型测试连接均失败，疑似模型路由或名称解析问题。 | 待修复 |
| **低** | [#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889) | **Tauri桌面版插件加载器未启动**（已有关闭PR [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900)） | **已修复** (等待合并入主分支) |
| **回归** | [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) | **v1.1.12图片预览回归**：升级后`send_file_to_user`发送的图片无法在聊天窗口显示。 | **已有修复PR** [#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324) |
| **回归** | [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | **升级后内置技能被重置**：每次升级，用户禁用的技能都会恢复为启用状态。 | 待修复 (历史遗留问题) |

## 功能请求与路线图信号

社区对新功能的讨论主要集中在以下几个方面，结合已有PR可窥见可能的路线图：

1.  **多端适配与UI优化**：大量用户正在积极探索移动端使用场景。多个PR（如`#5369`, `#5362`, `#5364`, `#5367`）分别针对不同页面进行了移动端适配。这很可能会被整合进下一个版本，以解决“设备碎片化”带来的体验问题。
2.  **核心机制的增强与稳健性**：
    - **模型高可用/自动故障转移**：用户`asdfly`在`#5351`中请求实现`RoutingChatModel`的自动故障转移功能。这只是冰山一角，`#5342`请求为工具结果大小设置硬限制，`#5316`请求为记忆搜索添加时间衰减排序。这些迹象表明社区对生产环境的稳定性有更高期待。
    - **上下文管理**：PR `#5321`引入了一种名为“scroll”的上下文管理策略，利用SQLite持久化对话并支持按需召回。这是一个比较创新的功能，若被合并，将提升模型在长对话中的表现。
3.  **实时交互与API体验**：用户`xyxy`在`#5322`中请求API消息的实时UI更新和语音通知。这表明用户不仅将QwenPaw视为聊天工具，也在尝试将其嵌入到更复杂的自动化工作流中，对API体验和实时性要求更高。
4.  **插件生态与功能丰富**：PR `#4622`（datapaw数据分析插件）长期处于开放状态，表明社区在推动构建更丰富的插件生态。

## 用户反馈摘要

- **对功能回归表达不满**：用户`zjccjz869`在`#5320`中对`v1.1.12`升级后图片预览功能丢失表示无奈，原本正常的功能突然失效，且“之前发送的图片也消失了”，这种体验是令人沮丧的。开发者通过`#5324`迅速定位了根因（`FileResponse`行为变更）。
- **对消息队列功能“又爱又恨”**：用户`renzhong424`在`#5354`中肯定了新消息队列对效率的提升，但同时指出了它带来的“串台”问题，并附上了清晰的截图。这种“好但容易翻车”的反馈是典型的早期用户反馈，为开发者提供了宝贵的优化方向。
- **对配置持久化有较高期望**：用户`daigoopautoy`在`#5262`中再次强调“每次升级都要手动禁用一次”的烦恼。这暴露了软件升级流程中的一个常见痛点：忽略了用户显式的配置选择。
- **移动端用户展现探索精神**：用户`bob-geek11`在`#5329`中通过手机浏览器访问后端，展示了非凡的探索精神，并提出了具体的、符合移动端使用习惯的UI改进建议，而非简单抱怨“不好用”，这类建设性反馈对产品改进极有价值。
- **社区积极贡献移动端适配**：多位贡献者（`yaozy2020`, `lecheng2018`）主动提交了针对不同页面的移动端适配PR，表明社区不仅提出问题，也在积极动手解决。
- **对项目方向提出战略建议**：用户`Jailtonfonseca`在`#5360`中给出了一个非常成熟的建议：“在添加新功能之前，应先让核心应用完全稳定”，并指出移动端响应和Agent交互等基础问题应优先解决。这暴露了项目当前面临的一个主要矛盾：功能迭代速度与核心稳定性之间的权衡。

## 待处理积压

以下为长期未合并/响应，但对项目健康度至关重要的事项，提醒维护者关注：

1.  **技能状态持久化（`#5262`）**：这是一个自6月17日以来持续有回响的Issue，且在更早的`#4807`就有报告。虽然看似是“小”问题，但它频繁打断用户的工作流，对使用体验影响很大。
2.  **`feat/datapaw-plugin-impl` 插件PR (`#4622`)**：自5月22日创建，目前已4周有余。该PR引入了重要的数据分析插件，对扩展QwenPaw的功能边界非常有价值。建议维护者给出验收反馈或合并计划，避免打击长期贡献者的积极性。
3.  **积压的已合并PR（共32个待合并）**：虽然有5个PR被合并/关闭，但目前仍有32个PR处于待合并状态。请维护者关注是否存在因测试冲突或其他原因而停滞的关键修复，特别是涉及插件系统（`#4900`）和E2E测试（`#5372`）的PR，它们对项目稳定性的提升至关重要。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目动态日报 | 2026年6月22日

---

## 1. 今日速览

在今日的报告周期内，ZeptoClaw 项目虽然更新数量不多（1 Issue 关闭、1 PR 合并），但动作高度聚焦，呈现出典型的**“低流量、高价值信号”**特征。项目关闭了一项此前被标记为 `P1-critical`（关键优先级）的长期 Issue，并合入了直接关联的 Pull Request，成功构建了针对二进制体积的自动 CI 门禁。这一里程碑标志着项目在捍卫“机器人友好型、极致轻量化”这一核心战略护城河上，从观念倡导正式迈入了自动化强制执行阶段。维护者（qhkm）的执行效率和对核心目标（保持 6MB 量级体积）的意志力非常突出，项目整体健康度优秀。

---

## 2. 版本发布

**今日无新版本发布。**

---

## 3. 项目进展

**CI 流程硬性化：二进制体积门禁正式上线**
- **PR #611** `[chore(ci): promote binary-size to PR gate at 7.5MB]`（[查看 PR](https://github.com/qhkm/zeptoclaw/pull/611)）**已于今日合并/关闭。**

该 PR 是此前 Issue #537 的工程实现，核心修改点包括：
1. **移除执行限制：** 删除了原有 CI 中 `binary-size` 任务的 `if:` 条件，不再仅限于 `push-to-main`，而是对 **每一个 Pull Request** 都强制执行。
2. **降低并明确阈值：** 将剥离后的发布版二进制文件大小限制明确设定为 **7.5MB**（项目 `Cargo.toml` 已配置 `strip = true`），作为 PR 准入的硬性否决指标。

**影响评估：** 这一变更彻底封堵了依赖盲目增长导致体积膨胀的回归漏洞。任何新增依赖或代码若导致体积超出 7.5MB，CI 将直接拒绝 PR 合并。这是项目开发流程规范化的重要一步，确保 ZeptoClaw 始终满足嵌入式/机器人场景的物理空间约束。

---

## 4. 社区热点

尽管具体讨论的评论数显示为零，但 **Issue #537** 的关闭过程本身构成了今日社区最受关注的核心事件。

- **Issue #537** `[CLOSED] [chore, P1-critical] chore(ci): binary size budget gate`
  （[查看 Issue](https://github.com/qhkm/zeptoclaw/issues/537)）

**分析背后的诉求：**
该 Issue 原文明确阐述了项目维护者的深层思考：**“6MB 的二进制文件是项目在机器人领域的战略护城河。每次 PR 都有缓慢膨胀的风险，如果缺乏 CI 守护，这条护城河会在不知不觉中被流沙掩埋。”**

这段话已成为社区理解项目定位的经典宣言。该 Issue 从 4 月提出，到 6 月通过 PR #611 落实，历时近两个月。它传递的信号非常明确：社区（尤其是维护者）将“极致轻量”视为不可谈判的刚性约束，一切新功能扩展都必须在体积上做出妥协。这种高度的价值观统一是项目长期健康发展的强力保障。

---

## 5. Bug 与稳定性

**今日无新 Bug 报告。**

值得注意的是，今日完成的是一个**主动防御型的稳定性工程**：

- **防止体积回归：** PR #611 合入后，自动阻止一切导致二进制膨胀至 7.5MB 以上的 PR。这是一种比被动修复 Bug 更具深度的稳定性保障措施。在项目早期阶段就通过 CI 固化体积红线，可以避免后期因极端瘦身而进行大规模架构重构的风险。该项目已将此门禁置于稳定性的最高优先级。

---

## 6. 功能请求与路线图信号

今日无全新的用户功能请求。但从今日的更新行动中，可以明确捕获到项目路线图的强烈信号：

1. **极致资源约束适应能力：** 将“剥离后 7.5MB”作为硬性通过标准，暗示了 ZeptoClaw 的目标部署场景（机器人、边缘设备、嵌入式系统）对存储资源极其敏感。这可能是本项目的核心差异化优势。
2. **开发流程自动化与规范化升级：** 从设置 `P1-critical` 级别的议题到合入相应的自动化门禁，显示项目正从“个人作品”向“成熟体系”过渡，通过 DevOps 手段而非人工审查来保障代码质量和愿景。
3. **下一版本展望：** 既然体积门禁已经建立，维护者下一步很可能将精力重新投入功能性开发，但所有新增功能都必须在 7.5MB 的“紧箍咒”下寻找生存空间。

---

## 7. 用户反馈摘要

今日无新增的用户评论反馈。

不过，从 Issue #537 的动机描述中，我们可以清晰地解读出目标用户的底层痛点：

- **痛点：** 机器人/嵌入式开发者需要能稳定运行在有限 flash 空间的轻量级 AI 智能体，但很多 AI 项目随着迭代迅速变得臃肿不堪，最终被排除在实际硬件部署之外。
- **满意点：** 维护者公开明确地将“适配机器人”作为最高优先级，并主动设定了 CI 门禁，这给予用户极大的信心。这意味着他们可以信赖 ZeptoClaw 不会在未来某个版本突然变得无法塞入他们的设备。

---

## 8. 待处理积压

基于当前数据，项目待处理积压表现**非常健康**。

- **关键积压已清零：** 此前唯一跨月度、被标记为 `P1-critical` 的重要基础设施议题（#537）已在今日圆满解决并关闭。该议题自 2026年4月23日 提出，至 2026年6月21日 关闭，完美展现了维护者 **“先提案定标准，再开发做实现”** 的严谨工作流闭环。
- **无其他异常堆积：** 目前没有迹象表明存在长期未响应的严重 Bug 或处于无人维护状态的陈旧议题。项目 backlog 处于良性生态中。

*(注：如在其他渠道存在未收录的积压，可能需要维护者进行主动扫描)*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 (2026-06-22)

## 1. 今日速览
ZeroClaw 项目在 2026 年 6 月 22 日展现出极高的社区活跃度与密集的并行开发节奏。过去 24 小时内，共有 **50 个 Issue 和 50 个 PR 产生更新**，其中新开/活跃 Issue 36 个，待合并 PR 高达 44 个，显示出项目正处于高强度迭代与代码整合期。大量标记为 `risk: high` 的变更集中在 **MCP 工具隔离、WASM 插件安全、以及核心运行时稳定性**三大领域，风险可控但需密切关注。当日无新版本发布，但 v0.8.2/v0.8.3 多个版本跟踪器更新频繁，表明开发管线运行正常，整体健康状态良好。

---

## 2. 版本发布
**（本日无新版本发布）**

---

## 3. 项目进展
今日虽无大型功能合入，但多项关键 Bug 修复与安全强化 PR 正在推进，标志着项目从功能扩展期步入稳定性与安全性打磨期：

- **里程碑收尾**：`v0.8.0 发布队列` ([#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) 与 `v0.8.1 集成队列` ([#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) 两个跟踪器正式关闭，为前序版本画上句号。
- **安全与权限隔离（核心看点）**：
  - ✅ **MCP 代理级隔离**：两个 PR 同时推进——[#8120](https://github.com/zeroclaw-labs/zeroclaw/pull/8120) 修复渠道编排器将 MCP 工具注册到所有 Agent 的问题，[#7747](https://github.com/zeroclaw-labs/zeroclaw/pull/7747) 将 `mcp_bundles` 配置真正绑定到运行时。
  - ✅ **Pipeline 权限绕过修复**：[#7960](https://github.com/zeroclaw-labs/zeroclaw/pull/7960) 修复了 `execute_pipeline` 在执行子工具时跳过 `ToolAccessPolicy` 的问题。
- **运行时健壮性**：
  - ✅ [#7959](https://github.com/zeroclaw-labs/zeroclaw/pull/7959) 修复非 Full 自主级别下频道工具审批逻辑异常。
  - ✅ [#8003](https://github.com/zeroclaw-labs/zeroclaw/pull/8003) 修复 session 结束时 `session_end` 钩子从未触发的问题。
  - ✅ [#8122](https://github.com/zeroclaw-labs/zeroclaw/pull/8122) 将 `ENOBUFS` 列为守护进程的可恢复 `accept()` 错误。
  - ✅ [#7847](https://github.com/zeroclaw-labs/zeroclaw/pull/7847) 修复频道会话持久化竞态导致历史乱序。
- **平台适配与开发者体验**：
  - ✅ [#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853) 修复 Windows 自更新机制（文件锁定导致无法删除运行中进程镜像）。
  - ✅ [#7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908) 修复浏览器工具 WebDriver 传输下快照返回 Null 及 CSS 选择器转义问题。
  - ✅ [#7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946) 为 ZeroCode TUI 和网关聊天增加上下文窗口占用条。
  - ✅ [#7771](https://github.com/zeroclaw-labs/zeroclaw/pull/7771) 为观测事件补全 channel/agent_alias/turn_id 上下文字段。

---

## 4. 社区热点
- **治理讨论热浪（[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)，11 条评论）**：关于"工作列、看板自动化与标签清理"的 RFC 成为今日最热话题。核心探讨如何在不增加维护者手动负担的前提下优化工作流路由，体现了社区对项目治理流程成熟度的高度参与。
- **渠道生态缺失（[#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503)，9 条评论）**：用户 `irunmyway` 急切寻找 NaPCat / OneBot 协议通道，并截图展示配置页面没有相关选项，反映了对多样化后端接入的强烈诉求。
- **Webhook 扩展需求（[#2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467)，6 条评论）**：用户 `MexHigh` 直言 "The Webhook system is not really usable right now for generic Webhook senders"，希望增加自定义路径与载荷转换功能。
- **本地模型支持呼声（[#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)，3 条评论 / 2 个 👍）**：本地优先模式提案获得社区正面反馈，用户期望解决小模型场景下的提示词膨胀与系统提示泄露问题。

---

## 5. Bug 与稳定性

### 🔴 [S1 - 流程阻塞]
| Issue | 描述 | 状态 | 备注 |
|-------|------|------|------|
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | Gemini CLI OAuth 认证后持续报错 `rate_limited` / `All providers failed` | OPEN | 2 👍，用户 `nrpx` 确认 workflow 完全阻塞 |
| [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) | 原生/MCP 工具在 OpenAI Reasoning 与 Anthropic 模型上不可用 | OPEN | 工具注册后模型收不到，严重影响多模型生态兼容性 |
| [#8094](https://github.com/zeroclaw-labs/zeroclaw/issues/8094) | Anthropic 模型添加后在仪表盘显示但聊天窗口不可见，需重置 | OPEN | 被报告者标记为 S0 级别 |
| [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | MiniMax 上下文压缩丢弃 `tool_calls` / `tool` 消息，导致工具循环 | IN PROGRESS | OpenAI 兼容 Provider 通用问题 |

### 🟡 [S2 - 功能异常/安全隐患]
| Issue | 描述 | 严重度 |
|-------|------|--------|
| [#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360) | Telegram 频道 Prompt 缓存完全失效，每次全量重计算 | P2 |
| [#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) / [#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) | WASM 插件缺乏 SSRF 保护与环境变量读取白名单 | P1 |

### 🟢 [已关闭/已修复]
- Docker 构建失败（aardvark-sys 缺失） 🔒 [#8089](https://github.com/zeroclaw-labs/zeroclaw/issues/8089)
- `zeroclaw check` WebSocket 401 认证异常 🔒 [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038)

---

## 6. 功能请求与路线图信号
### 路线图结构化切割
v0.8.3 里程碑今日被拆分为三个精细化跟踪器，标志着项目代际规划能力的提升：
- **Operator 面** ([#8070](https://github.com/zeroclaw-labs/zeroclaw/issues/8070))：网关、Web 仪表盘、ZeroCode、Quickstart / Doctor
- **运行时面** ([#8071](https://github.com/zeroclaw-labs/zeroclaw/issues/8071))：Agent 循环、工具执行、内存、Cron
- **渠道/Provider 面** ([#8072](https://github.com/zeroclaw-labs/zeroclaw/issues/8072))：消息路由、Provider 序列化、配置行为

### 即将落地的功能
- **WASM 插件平台** ([#7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314))：架构定稿，安全边界定义冲刺中
- **Skills 平台** ([#7852](https://github.com/zeroclaw-labs/zeroclaw/issues/7852))：注册表、缺失能力提示、插件打包技能行为
- **本地优先模式** ([#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287))：in-progress，v0.8.x 走读
- **OTel 链路增强** ([#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) / [#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642))：turn 级别跨度嵌套 + 完整输入输出捕获

### 社区驱动的功能请求
- **增强配对码强度** ([#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613))：安全需求攀升，6 位数字被指太弱
- **LINE 频道功能增强** ([#7768](https://github.com/zeroclaw-labs/zeroclaw/pull/7768))：加载动画、昵称切换、回复反馈已发 PR
- **上下文窗口显示条** ([#7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946))：多界面统一落地

---

## 7. 用户反馈摘要
- **"Gemini CLI OAuth is simply not working"** ([#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879))：Google 生态用户的严重阻塞，认证成功后仍持续获限。
- **"cannot find napcat or onebot channel"** ([#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503))：国内用户群体对 OneBot 协议接入的缺失感到沮丧。
- **"The Webhook system is not really usable"** ([#2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467))：开发者集成方在使用 GitHub Webhooks 时发现通用性严重不足。
- **"forcing full prompt re-processing on Telegram"** ([#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360))：用户 `edgarkech` 明确对比 CLI 端可行而 Telegram 端不可行，反映出不同渠道间的内部行为不一致（渠道层缺失对 Provider 缓存特性的适配）。
- **"zeroclaw should log to stderr instead of stdout"** ([#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721))：用户 `mikeyhew` 明确指出命令输出被日志污染，是一个破坏 CLI 管道体验的典型细节。
- **安全焦虑**：多位用户自发报告 WASM 插件的 SSRF 攻击面 ([#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918)) 与环境变量泄露风险 ([#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919))，社区对插件安全基线的关注度在提升。
- **积极贡献生态**：`mazhuima` 成为今日修复主力，提交了线程安全、日志审计、UI 细节在内约 10 个修复 PR，项目贡献者网络日趋成熟。

---

## 8. 待处理积压（维护者关注清单）
### 🔴 安全高地（P1，搁置超 2 个月）
- **[#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) WASM 插件 SSRF 保护**：插件可攻击内网、云元数据端点、同驻服务
- **[#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) 环境变量读取白名单**：持有 `env_read` 权限的插件可读取所有环境变量
- **建议**：作为 v0.8.2 插件体系的安全生命线，建议加快推动修复 PR 落地。

### 🟡 重大审计事项（P2，已开放近 2 个月）
- **[#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) 追踪 153 个被批量回滚的 Commit**：涉及代码完整性的核心审计，目前仍处于追踪阶段，未形成具体的恢复方案与时间节点。

### 🟢 呼声较高的渠道集成（P2，开放超 3.5 个月）
- **[#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) NapCat/OneBot 渠道支持**：社区评论热度高（9 条），建议评估是否纳入 v0.8.3 渠道迭代（[#8072](https://github.com/zeroclaw-labs/zeroclaw/issues/8072)）。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*