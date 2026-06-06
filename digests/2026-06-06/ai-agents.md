# OpenClaw 生态日报 2026-06-06

> Issues: 469 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-06 02:50 UTC

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

好的，这是基于 OpenClaw 项目 2026-06-06 日 GitHub 数据生成的动态日报。

---

## OpenClaw 项目动态日报 2026-06-06

### 1. 今日速览

过去 24 小时，OpenClaw 项目处于极度活跃状态，**共产生了 469 条 Issue 与 500 条 PR 更新**，表明社区参与度与维护响应速度均达到峰值。然而，**自 `2026.6.1` 版本发布以来，一系列严重的回归 Bug 正集中爆发**，包括核心编码智能体冻结、OpenAI 最新模型通信失败和控制面 RPC 高延迟等关键问题，社区情绪处于高期待与高焦虑并存的“压力测试”阶段。尽管故障密集，但针对 macOS 重连、会话性能优化等关键问题的修复补丁已在 24 小时内进入合并流程，**项目呈现出“边失火边灭火”的高速迭代态势**。

### 2. 版本发布

**今日无新版本发布。**

需注意，当前大多数严重回归问题均与上周发布的 `2026.6.1` 版本相关。数据表明该版本引入了多项破坏性变更（SQLite 迁移、SessionManager 重构等），用户若未升级，建议评估风险后暂缓升级。

### 3. 项目进展

今日合并/关闭了 **137 个 PR**，项目推进主要集中在故障响应与缺陷修复上，并有一批重要功能特性进入审核尾声。

*   **已合并的核心修复（ClawSweeper 自动化合并）：**
    *   `#90736` / `#90815`: **修复 macOS 节点模式健康会话的静默自重连问题。** 解决了 `wss://` 网关循环下用户体验混乱的 Bug。
    *   `#90748` / `#90816`: **修复 `memory-core` 状态检测。** 解决了 `memory status` 命令始终显示“期望模型为空”导致向量搜索不可用的假阳性报告。
    *   `#90812`: **修复语音频道 Twilio 流被错误终止。** 避免了陈旧会话回收逻辑误杀活跃的语音流。

*   **重要待合并/功能推进 PR：**
    *   `#90328`: **WebUI 模型选择器运行时标签暴露。** 提案将为模型选择器提供非默认运行时标签（如 `GPT-5.5 · OpenAI Codex`），提升模型选择透明度。
    *   `#78441`: **子代理工具权限转发。** 为 `sessions_spawn` 增加 `toolsAllow` 转发，解决子代理无法继承工具白名单的长期痛点，补齐多代理拼图。
    *   `#90819`: **`sessions.list` 并发性能修复。** 直指 `#76562` 性能问题的根源——修复并发场景下插件工作目录扫描导致的 O(行数) 级阻塞，大幅提升网关在高并发下的响应速度。

### 4. 社区热点

今日讨论最活跃的议题（按评论数排序）揭示了社区当前的两大核心诉求：**稳定性恐慌** 与 **成本控制**。

*   **🚨 [Bug]: Coding Agent never completes anything** (`#62505`，评论 14)
    *   **热度分析：** 核心功能失效。用户反馈编码智能体完全无法产生有效输出，只会给出模糊状态更新并道歉。这直接触及项目作为 **“个人 AI 助手”的核心生产力承诺**，情绪最激烈。
*   **🚨 High CPU, extreme control-plane RPC latency** (`#76562`，评论 13，👍 5)
    *   **热度分析：** 系统管理员视角的“灾难性”故障。CPU 峰值 100%、面板响应极慢，用户集体声讨此回归问题。该项目获得的 👍 数最高，表明受影响人群广泛。
*   **🚨 OpenAI ChatGPT Responses transport fails** (`#90083`，评论 12，👍 3)
    *   **热度分析：** 最新的 `gpt-5.4/5.5` 模型在 `2026.6.1` 上完全无法使用。对于依赖前沿模型的高级用户来说，这是**立即停摆**的阻断性 Bug。
*   **💡 [Feature]: Tiered bootstrap file loading** (`#22438`，评论 17)
    *   **热度分析：** 老 Issue 但生命力极强。虽然创建于 2 月，但长期占据评论榜首。它切中了所有使用大型工作区的用户的痛点——**Token 浪费**。这表明社区对精细化上下文控制有长期、稳定的需求。
*   **💡 Channel-mediated approval for MCP tool calls** (`#78308`，评论 12)
    *   **热度分析：** 企业级安全治理的呼声。MCP 工具现在可以任意修改外部状态，用户普遍不放心，要求必须像 shell-exec 一样加入 `/approve` 审批流程。这是项目从“个人玩具”向“生产级工具”进化的关键信号。

### 5. Bug 与稳定性

今日报告的 Bug 数量多且波及面广，大多数与 `2026.6.1` 的变更有关，按严重程度排列如下：

*   **🔴 严重级别：核心功能阻塞 / 数据丢失**
    *   **Coding Agent 死锁** (`#62505`)：编码智能体完全不产生输出（尚在排查，无修复 PR）。
    *   **OpenAI 传输层故障** (`#90083`)：针对 `gpt-5.4`/`5.5` 返回 `invalid_provider_content_type`（影响面巨大，已有 `#90328` 关联提案，但无直接修复）。
    *   **控制面 RPC 高延迟** (`#76562`)：CPU 满载，面板响应极慢（已有修复 PR `#90819` 待合并）。
    *   **Cron 状态静默丢失** (`#90072`)：升级后 `SQLite` 迁移导致 44/45 个 Cron 任务凭空消失（**数据完整性严重受损**）。
    *   **WebChat 会话记录被覆写** (`#77012`)：每次对话只保存最后一条消息，会话历史遭遇严重破坏（5.2 回归）。

*   **🟡 中等严重级别：特定功能/渠道异常**
    *   **MCP 工具无法注入子代理** (`#85030`)：严重限制多代理架构能力（已有关联修复 PR `#78441` 待合并）。
    *   **Matrix 频道分发崩溃** (`#90325`)：更新后 Matrix 渠道无法处理任何入站消息。
    *   **OpenAI 重放导致加密内容错误** (`#90093`)：第二轮对话即失败。
    *   **Feishu 流式卡片渲染异常** (`#88929`)：打字机效果异常，最终内容被截断。
    *   **Discord 搜索功能缺少 GuildId** (`#88796`)：模型调佣 `search` 时始终报错（已有修复 PR 待审核）。

*   **⚪ 次要/体验级别**
    *   **macOS launchd 隐藏所有 stderr 日志** (`#90711`)：导致故障排查困难（已有修复讨论）。
    *   **Telegram 反应事件无法触发 Agent 轮次** (`#64752`)：多模态交互功能退化。

### 6. 功能请求与路线图信号

从今日的 Feature Request 中，可以提炼出未来几周可能的演进方向：

*   **📐 架构重构期信号：优化与治理**
    *   **分层 Bootstrap 加载** (`#22438`)：高呼声的需求，意图解决大工作区 Token 浪费问题。预计会进入 `P1` 讨论。
    *   **MCP 工具调用审批流程** (`#78308`)：与 Shell 审批一致的安全治理。
    *   **按 Agent 隔离记忆库** (`#63829`)：多 Agent 场景下的核心需求（9 个 👍），对 `memory-wiki` 插架构性变革。
    *   **会话最大时长/Token 硬限制** (`#64463`)：成本控制意识的觉醒，用户想避免因代理死循环而产生的巨额账单。

*   **🖥️ 用户体验升级信号：透明与控制**
    *   **模型选择器运行时标签** (`#90328`)：用户希望知道具体跑在哪个运行时上。
    *   **WebChat 工作区侧栏可折叠** (`#90246`)：GUI 细节优化，表明用户量增长，进入精细化打磨阶段。
    *   **日志可操作性** (`#90797`)：要求内存压力日志包含百分比和操作建议，监控化需求增加。

### 7. 用户反馈摘要

结合 Issues 中的评论，今天能听到的社区真实声音如下：

*   **“升级恐惧症”蔓延**：大量用户反馈“在 `2026.4.X` 之前是工作的”。每次大版本升级都伴随大量回归，严重消耗了社区的信任。特别是 `2026.6.1` 的 Cron 数据静默迁移丢失（`#90072`）事件，引发了关于 **“测试覆盖率和数据迁移安全性”** 的质疑。
*   **“黑盒”行为不可接受**：用户对智能体行为不满意。
    *   智能体“只汇报，不干活” (`#62505`)。
    *   为什么选择了某个模型，系统却不使用？(`#85103`)
    *   Media 分析到底用了哪个模型？用户希望看到元数据暴露 (`#62924`)，而不是让 AI 自己猜测。
*   **对“自动解决问题”的认可**：尽管 Bug 多，但用户对于 **ClawSweeper [bot] 自动合并修复 PR** 的流程表示赞赏（如 `#90736` 的 macOS 修复）。这个自动化运维体系被认为是项目在高强度开发下仍能维持生命力的关键。

### 8. 待处理积压

以下长期未解决或处于僵局的重要条目，今天应该被再次提醒给维护者：

*   **⚡ `#14785` [工具 Schema Token 优化] (2月提出)**
    *   **状态：** 开启 4 个月，需求明确（节省约 3500 Tokens/次），方案清晰（简化参数）。**这是对所有人都有收益的优化，却迟迟没有推进决策。** 建议花 30 分钟定案。
*   **⚡ `#37446` [子代理超时导致重复 POST] (3月提出)**
    *   **状态：** **幂等性设计缺口。** 子代理超时后重试导致评论区重复回复。这是一个潜在的 **生产级可靠性灾难**，但长期未得到安全审查和解决。
*   **⚡ `#58818` [保留原始消息快照] (4月提出)**
    *   **状态：** 用户反复被“会话重置”和“压缩”破坏上下文困扰。这个 Feature 要求 **在压缩后保留关键原始消息**，是根本性的对话记忆优化，长期被标记为策略讨论中。
*   **⚡ `#64664` [审批 ID 重启丢失] (4月提出)**
    *   **状态：** 网关重启导致所有审批 ID 失效，用户收到错误的“过期或未知的审批 ID”提示。**这破坏了完整的自动化审批链路**，特别是对于 Telegram 使用场景，非常影响体验。
*   **⚡ `#61005` [Android 连接按钮灰色] (4月提出)**
    *   **状态：** 影响用户注册流程顺滑度。如果该项目依赖移动端增长，此 Bug 是 **用户转化漏斗的严重阻塞**。

---

## 横向生态对比

以下是基于 2026-06-06 数据生成的横向对比分析报告。

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“高速扩张与压力测试并存”** 的临界阶段。核心项目日处理 Issue/PR 总量维持在数百条级别，但 **2026.6.1 版回归潮**（OpenClaw、NanoBot、Hermes）与 **Yuanbao 通道兼容断层**（CoPaw）等问题表明，项目在快速迭代中普遍面临测试覆盖与数据迁移安全的挑战。社区诉求从“能否运行”升级为 **“能否可靠治理”**——MCP 工具审批、Token 消耗透明化、记忆污染隔离成为跨项目的共性痛点。同时，Provider 生态、多通道接入与多 Agent 协作网络正在快速落地，为下一阶段的标准化与互联互通奠定基础。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 今日版本发布 | 活跃度与健康度评估 |
|------|--------------|------------|--------------|-------------------|
| **OpenClaw** | 469 | 500 | 无 | **极度活跃但承压**；回归 Bug 集中爆发，修复 PR 密集，自动化合并流程高效 |
| **Hermes Agent** | 50 | 50 | v0.16.0 | **极高活跃且成熟**；大版本合并 874 commits，社区贡献者踊跃，安全性显著提升 |
| **IronClaw** | 13 | 50 | 无 | **极高活跃，架构突破**；Reborn Hook 框架完成落地，WeCom & Slack 渠道发力 |
| **ZeroClaw** | 50 | 50 | 无 | **极高活跃，生态扩张**；Schema V3 引入 7+ Provider、多通道，38 个 PR 待合并 |
| **NanoBot** | 11 | 28 | 无 | **高度活跃，响应极快**；多数 Bug 24h 内修复，子代理与 WebUI Fork 功能推进 |
| **PicoClaw** | 40+ | 20 合并 | Nightly | **高度活跃，稳定提升**；OneBot/JSONL/安全加固快速合入，Evolution Token 泄漏待解 |
| **LobsterAI** | 3 | 12 | v2026.6.5 | **高活跃，迭代集中**；cowork/语音/安全修复，社区对遗留 Bug 仍有期待 |
| **CoPaw** | 20 | 16 | 无 | **高活跃，社区贡献活跃**；4 个首贡 PR 合并，Yuanbao 通道问题集中上报 |
| **Moltis** | 4 | 5 | 无 | **中高活跃，响应良好**；Telegram 流式 Bug 72h 闭环，Docker/Podman 兼容 PR 就绪 |
| **NanoClaw** | 0 | 3 | 无 | **低活跃，稳定**；核心稳定修复，OneCLI 与 API 容错提升 |
| **NullClaw** | 0 | 1 | 无 | **低活跃**；唯一 PR 新增 Evolink 提供商，社区讨论冷淡 |
| **TinyClaw** | 0 | 0 | 无 | **无活动** |
| **ZeptoClaw** | 0 | 0 | 无 | **无活动** |

---

## 3. OpenClaw 在生态中的定位

- **社区规模第一**：日处理 Issue/PR 近千，远超其他项目（Hermes/ZeroClaw 各 100，IronClaw 63），反映出最广泛的使用基数与最多样的场景覆盖。
- **核心优势**：**“ClawSweeper”** 自动化合并机器人获得用户认可，24h 内完成 macOS 重连、内存检测等修复，形成了“边失火边灭火”的高压迭代模式。
- **技术路线差异**：相比 Hermes 的“大版本式重构”和 ZeroClaw 的“微内核+安全插拔”，OpenClaw 更倾向于**全功能整合**（WebUI、多 Provider、子代理、记忆库），但这也导致 `2026.6.1` 版因 SQLite 迁移与 SessionManager 重构引发大面积回归，测试覆盖与数据迁移安全性成为社区核心质疑点。
- **定位类比**：类比生态中的 **“旗舰项目”**，功能最全但复杂度最高，适合追求零配置与最新功能的个人用户；而 Hermes/ZeroClaw 更适合对架构安全性或定制化有更高要求的团队。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 / 症状 |
|----------|---------|----------------|
| **MCP 工具安全审批** | OpenClaw (#78308)，ZeroClaw (#7155)，CoPaw (类似需求) | 社区要求像 shell-exec 一样加入 `/approve` 流程，避免工具被滥用；ZeroClaw 提出三级确认策略 |
| **子代理权限与协作** | OpenClaw (#78441 toolsAllow 转发)，NanoBot (#3992 跨实例消息总线)，IronClaw (多 channel routing) | 解决子代理无法继承工具白名单、跨实例通信缺失的长期痛点 |
| **记忆系统污染与隔离** | NanoBot (#4212 记忆循环注入)，OpenClaw (#22438 分层 Bootstrap Token 浪费)，CoPaw (#4968 上下文管理) | 用户担忧未确认推理被固化、记忆库按 Agent 隔离需求上升 |
| **Provider 多元化与兼容性** | NullClaw (#947 Evolink)，OpenClaw (#90328 模型运行时标签)，NanoBot (#4204 Azure extra_query)，ZeroClaw (#7260 7 个新 Provider) | 社区强烈要求打破单一 Provider 依赖，标准化 OpenAI 兼容接口成为共识 |
| **成本控制与 Token 透明化** | OpenClaw (#64463 会话 Token 硬限制)，PicoClaw (#3012 Evolution 持续计费)，Hermes (时间感知注入避免无效消耗) | 用户担忧 Agent 死循环导致巨额账单，要求暴露 Token 消耗、设置硬性上限 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 个人全功能智能助手（聊天、编码、多通道、子代理、记忆） | 个人开发者、进阶用户 | **ClawSweeper 自动化运维**；以扩展（插件/工具）驱动 |
| **Hermes Agent** | Agent 核心运行时 + Web 桌面端 + 安全性 | 高级 Agent 研究者、需要端到端桌面交互的团队 | **大版本重构 + 多语言支持**；重度依赖 Anthropic 生态，安全审计严谨 |
| **NanoBot** | 轻量级个人助手，优先多 Provider 兼容与快速 Bug 响应 | 日常用户、追求低门槛和个人隐私 | **极短修复周期**；Mailbox 子代理结果管理，WebUI Fork，但 Python 版本策略激进 |
| **PicoClaw** | 嵌入式/轻量 Agent，Go 实现，支持 OneBot 等国产通道 | IoT、嵌入式场景、国内开发者 | **Crash-consistent JSONL 存储**；OneBot 优化，已针对国产 MiMo 模型优化 |
| **ZeroClaw** | 安全可插拔架构 + Provider 网关 + 多通道 | 企业/安全敏感用户，需要深度定制 | **微内核 + OIDC/可插拔安全接口**；Schema V3 统一定义 Provider 和通道 |
| **IronClaw** | Web3 + Agent Hook 框架 + Slack/WeCom 集成 | 去中心化应用开发者、企业办公集成 | **PredicateStateBackend** 三种后端（Postgres/libSQL/内存）；Reborn 架构重构 |
| **LobsterAI** | 协作办公（cowork） + Windows/macOS 桌面端 | 团队协作场景、国内用户（网易背书） | **键盘快捷键重构、付费集成 (试用限制)**；语音输入与文件预览增强 |
| **CoPaw** | 国内生态（Yuanbao 通道）+ Desktop Pet | 国内用户、桌面辅助场景 | **Yuanbao 协议深度绑定**；大量 UI 改进（会话列调整、头像） |
| **Moltis** | 容器化轻量 Agent (Docker/Podman 沙箱) | 自托管用户、对容器隔离有要求的开发者 | **沙箱逃逸机制**；Docker 更新提示缺失修复中 |

---

## 6. 社区热度与成熟度分层

### 🔥 极高度活跃 / 核心挑战期
- **OpenClaw、Hermes Agent、IronClaw、ZeroClaw**
  - 日 Issue/PR 合计 50–500+，持续有新功能和重构 PR 涌入。
  - 特征：健康度受回归 Bug 威胁但修复力量充沛；社区信任度与焦虑并存。

### ⚡ 高度活跃 / 快速迭代期
- **NanoBot、PicoClaw、LobsterAI、CoPaw**
  - 日处理 10–40+ 项活动，版本发布或 Nightly 频繁；Bug 响应多在 24h 内。
  - 虽偶有核心功能阻塞，但整体迭代效率高，贡献者生态活跃（首贡 PR 常见）。

### 🔹 中低活跃 / 稳定或瓶颈期
- **Moltis、NanoClaw、NullClaw、TinyClaw、ZeptoClaw**
  - 活动量少，Moltis 虽有小团队响应但长期积压开始出现；NanoClaw/NullClaw 依赖个别贡献者，社区规模有限。
  - 适合作为补充或特定场景选择，但作为主力风险较高。

---

## 7. 值得关注的趋势信号

1. **安全层从“附加”走向“强制插拔”**  
   - ZeroClaw 明确将安全暴露为可插拔接口（#7142），OpenClaw 社区强烈要求 MCP 审批流程（#78308），IronClaw 修复跨租户泄漏（#3931）。**AI 智能体进入生产环境的必要条件正在被开源社区补全。**

2. **Agent 行为“可视化”与“可审计”成为硬性需求**  
   - 用户不再接受黑盒：要求暴露记忆操作（NanoBot #4212）、Token 消耗（OpenClaw #64463）、模型运行时标签（#90328）以及错误日志可操作性（IronClaw #4311）。**透明度直接决定用户信任。**

3. **Provider 生态从“数量堆砌”转向“标准化兼容”**  
   - NullClaw/ZeroClaw 新增 Provider 均首选 OpenAI 兼容接口；NanoBot 为 Azure 需要 `extra_query` 参数。**未来竞争焦点不是支持多少家，而是接口兼容程度和容错能力**（如 OpenClaw #90083 的传输层故障）。

4. **多 Agent 协作网络的标准萌芽**  
   - ZeroClaw 定义 `/.well-known/agent-card.json`（#7218），NanoBot 提出跨实例消息总线（#3992），OpenClaw 推进子代理权限转发（#78441）。**A2A 协议正在浮出水面，预计 2026H2 会出现更多互操作性尝试。**

5. **桌面端与移动端成为渠道密度竞争点**  
   - Hermes 修复 Windows 中文输入法（#40146），LobsterAI 增强 macOS 语音权限（#2113），CoPaw 收到移动端多行输入请求（#1107）。**跨平台体验的细节打磨将成为留存用户的关键壁垒。**

6. **成本治理从“用户自我管理”转向“框架硬限制”**  
   - PicoClaw Evolution 模式 Token 无限制消耗（#3012），OpenClaw 请求硬性 Token 上限（#64463），CoPaw 用户希望 Cron 直接执行不经过 AI（#4963）。**框架需要内置预算控制与死循环检测**，避免 API 账单失控。

7. **自动化运维从“手动”升级为“CI/CD 与机器人”**  
   - OpenClaw 的 ClawSweeper 获得正面评价；IronClaw/ZeroClaw 积压大量待合并 PR 暴露了维护者瓶颈。**项目健康度将越来越依赖自动化合并、测试驱动的流水线**，而非单个维护者的审查速度。

---

这份横向对比基于 2026-06-06 的截面数据，建议结合项目历史趋势（如回归频率、修复时长）进行动态跟踪。当前生态尚未形成垄断格局，各项目在架构选择与社区治理上分歧明显，但**对安全、透明、成本控制与互联互通的共识正在加速凝聚**。这对 AI 智能体开发者意味着：现在参与生态贡献具有极高的话语权红利。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot 项目 2026-06-06 数据生成的动态日报。

---

### NanoBot 项目动态日报 | 2026-06-06

---

#### 1. 今日速览
过去 24 小时内，项目呈现**极高度活跃**状态（共处理 11 条 Issue 与 28 条 PR）。社区报告了多个高优先级回归 Bug（如消息丢失、SDK 退出崩溃），但维护者与贡献者反应迅速，绝大多数严重问题已在当日提交了修复 PR 或直接关闭。同时，跨代理消息总线、WebUI Fork 等重量级社区功能 PR 正在等待评审。项目整体处于高强度迭代与快速响应阶段，社区健康度与成熟度持续提升。

---

#### 2. 版本发布
*(今日无新版本发布)*

---

#### 3. 项目进展
今日合并/关闭的 Pull Requests 与 Issues 主要集中在**稳定性修复**与**基础功能补全**上，项目正从核心功能完善向架构深度优化迈进。

- **关键 Bug 修复合入：**
  - **[PR #4210]** 修复了桌面端 Engine 重启后的 Token 刷新和 WebSocket 重放间隙问题，提升了桌面客户端的鲁棒性。
  - **[PR #3968]** 合并了 `/skill` 内置命令（仅列出已启用的技能），直接解决了社区反馈的 [#3959](https://github.com/HKUDS/nanobot/issues/3959) 问题。
  - **[PR #4197]** 修复了微信和 Telegram 渠道的私信配对（DM Pairing）逻辑，并保留了早期副作用防护。

- **关闭的 Issues：**
  - 解决了多个回归 Bug：Github Copilot 登录失败 ([#2573](https://github.com/HKUDS/nanobot/issues/2573))、`/skill` 显示禁用技能 ([#3959](https://github.com/HKUDS/nanobot/issues/3959))、浏览器刷新消息丢失 ([#4200](https://github.com/HKUDS/nanobot/issues/4200))。

- **架构与功能推进：**
  - 引入了基于 **Mailbox 的子代理结果管理** ([PR #4205](https://github.com/HKUDS/nanobot/pull/4205))，改进了子代理异步任务的处理机制。
  - **WebUI 体验升级** ([PR #4208](https://github.com/HKUDS/nanobot/pull/4208))：增加了对话 Fork 功能，允许用户基于历史消息创建分支对话，同时保持了 Composer 预填充隔离。

---

#### 4. 社区热点
今日社区讨论焦点集中在 **关键服务的稳定性** 与 **深度功能的缺失** 上。

- **🔥 最高关注度：** **[Issue #2573](https://github.com/HKUDS/nanobot/issues/2573) Github Copilot 登录失败**
  - 获得 9 个 👍，4 条评论。用户 `cheanus` 反馈将底层库切换为 `openai` 后，OAuth Device Flow 返回授权头格式错误。此问题严重影响依赖 Copilot 的日常用户，已于今日被修复关闭。

- **💬 深度需求讨论：** **[Issue #4212](https://github.com/HKUDS/nanobot/issues/4212) 防止记忆系统信息污染**
  - 虽然无评论，但其描述极其详尽。用户指出了当前 Consolidator 与长期记忆循环注入中的一个根本性缺陷：未确认的推理可能被固化并污染未来对话。这反映了高级用户对 Agent 记忆系统可靠性的极高要求，可能推动长期记忆架构的重构。

- **🚀 重磅社区 PR 待审：**
  - **[PR #3992](https://github.com/HKUDS/nanobot/pull/3992) 跨实例代理消息总线**：该 PR 允许运行多个 Agent 实例并通过共享消息总线进行通信，是代理协作能力的关键一步。
  - **[PR #4208](https://github.com/HKUDS/nanobot/pull/4208) WebUI Fork-from-here 功能**：被认为是提升 Web 端会话管理灵活性的关键改进。

---

#### 5. Bug 与稳定性
今日报告的 Bug 有明显的 **回归性问题**，但整体修复速度非常快。

- **严重 (Critical) - 暂未合入：**
  - **`[#4203]`** **`find_legal_message_start` 导致全部消息丢弃**：当用户消息后跟孤立工具结果时，错误函数会返回列表长度导致后续所有消息被丢弃。**状态：** 已上报，贡献者 `bymle` 已提交修复 **[PR #4215](https://github.com/HKUDS/nanobot/pull/4215)** 等待合入。
  - **`[#4211]`** **SDK 关闭时 MCP 连接异常退出**：通过 SDK 使用 Stdio MCP 时，解释器关闭阶段会触发 `RuntimeError`。**状态：** 贡献者 `axelray-dev` 已提交修复 **[PR #4216](https://github.com/HKUDS/nanobot/pull/4216)**。

- **中等 (Medium) - 已修复：**
  - **`[#4200]`** **浏览器刷新丢失用户消息**。回归 Bug，已关闭修复。
  - **`[#3959]`** **`/skill` 命令列示禁用技能**。已通过 `#3968` 合并修复。
  - **`[#2573]`** **Github Copilot 登录失败**。已关闭，确认修复。

- **低/长期 (Low/Long-Term)：**
  - **`[#1946]`** **Matrix 测试错误**。自 3 月 13 日上报以来未分配，尚处于开放状态。

---

#### 6. 功能请求与路线图信号
结合今日动态，以下功能具备较高的路线图优先级：

- **Provider 生态扩展（强信号）：**
  - **Azure 等兼容性：** **[Issue #4204](https://github.com/HKUDS/nanobot/issues/4204)** 提出的 `extra_query` 支持（如 `?api-version=`）是连接非标准 OpenAI 兼容网关的刚需，配置改动小但收益大。
  - **新搜索/生成提供商：** **[PR #4213](https://github.com/HKUDS/nanobot/pull/4213)** (Exa 搜索) 贡献了完整代码；**[Issue #4196](https://github.com/HKUDS/nanobot/issues/4196)** (火山引擎图片生成) 需求明确。用户希望打破单一 Provider 限制。
- **代理能力深化：**
  - **子代理容错：** **[Issue #4198](https://github.com/HKUDS/nanobot/issues/4198)** 提出的子代理 `fail_on_tool_error` 可配置，允许在微错误时重试而非直接失败，提升自愈能力。
  - **工具调用严格性：** **[PR #4190](https://github.com/HKUDS/nanobot/pull/4190)** 加强工具调用的校验，拒绝模糊匹配和格式错误的参数，提升执行安全性。
- **用户体验与工程现代化：**
  - **WebUI Fork 功能：** `[PR #4208]` 已完成实现。
  - **Python 版本策略：** **[PR #4207](https://github.com/HKUDS/nanobot/pull/4207)** 提议放弃 Python 3.11/3.12 支持，与当前 CI 测试矩阵对齐，降低维护成本。

---

#### 7. 用户反馈摘要
- **痛点与负面反馈：**
  - **核心功能断裂：** 用户对 Copilot 登录失败（`[#2573]`）和浏览器刷新丢消息（`[#4200]`）这类**回归 Bug** 表达了明显的负面情绪，称“刷新消息就没了，让人崩溃”。
  - **企业兼容性差：** 使用 Azure 网关的用户遇到 404 错误（[#4204](https://github.com/HKUDS/nanobot/issues/4204)），使用火山引擎的用户遇到 Provider 不支持错误（[#4196](https://github.com/HKUDS/nanobot/issues/4196)），显示项目在非 OpenAI 标准生态的兼容性上仍需补课。
- **使用场景与期望：**
  - **企业/团队用户：** 明确提出了钉钉白名单（[#4206](https://github.com/HKUDS/nanobot/pull/4206)）和邮箱自动处理（[#4170](https://github.com/HKUDS/nanobot/pull/4170)）的需求，期待用于生产环境的精细控制。
  - **高级 Agent 用户：** 深度关注**记忆系统污染**（[#4212](https://github.com/HKUDS/nanobot/issues/4212)）、**子代理自愈**（[#4198](https://github.com/HKUDS/nanobot/issues/4198)）和**跨代理协作**（[#3992](https://github.com/HKUDS/nanobot/pull/3992)）。
- **社区满意度：**
  - 尽管 Bug 较多，但社区对**维护者的响应速度**给予了认可。多数严重 Bug 在 24 小时内即被闭环或提供了修复 PR。
  - **外部贡献质量高且活跃。** 如 Exa 搜索（[#4213](https://github.com/HKUDS/nanobot/pull/4213)）、DingTalk 白名单（[#4206](https://github.com/HKUDS/nanobot/pull/4206)）均来自社区首次贡献者，展现了良好的开源生态。

---

#### 8. 待处理积压
以下为需要维护者重点关注的老旧或紧急积压事项：

- **长期未响应的重要 Issue：**
  - **`[#1946]` Matrix 渠道测试错误**（创建 85 天）。如果 Matrix 作为正式 Channel 被支持，此测试失败可能影响其他模块的 CI/CD 稳定性。
- **长期未合入的社区 PR：**
  - **`[PR #1284]`** 和 **`[PR #1408]`** 均为 CI/CD 工作流改进（分别创建 99 天和 96 天）。功能重叠，需要维护者决策并合并，以避免社区重复劳动。
  - **`[PR #3538]` Gateway 启停命令**（创建 38 天），该功能已经完备，但迟迟未合并。
- **今日紧急待办：**
  - **高优先级修复 PR 需立即合入：** **[#4215](https://github.com/HKUDS/nanobot/pull/4215)**（修复 Session 消息丢弃）和 **[#4216](https://github.com/HKUDS/nanobot/pull/4216)**（修复 SDK 退出异常）。这两个 PR 均涉及**数据完整性**和**程序稳定性**的核心问题，建议优先审查合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，以下是根据提供的Hermes Agent项目数据生成的2026年6月6日项目动态日报。

---

# Hermes Agent 项目动态日报 (2026-06-06)

---

## 1. 今日速览

今日Hermes Agent项目活动量巨大，代码库与社区讨论空前活跃。发布了一个里程碑式的重大版本 `v2026.6.5 (v0.16.0)`，带来了海量更新。Issue和PR数量均达到50条的高点，显示出社区参与度和维护者响应效率极高。虽然有大量社区反馈的Bug（特别是在Windows桌面端和中文输入法体验上），但高产的核心团队与社区贡献者也同步提交了大量修复和新功能PR，项目整体处于高速迭代、积极响应社区诉求的健康发展状态。

- **项目活跃度评级**: 🔥🔥🔥🔥🔥 (极高)

---

## 2. 版本发布

### v2026.6.5 (v0.16.0) — The Surface Release

- **发布日期**: 2026年6月5日
- **核心亮点**: 代号为“The Surface”，这是一个体量巨大、涉及范围极广的版本。在自v0.15.2以来的短暂时间内，项目完成了惊人的工作量。
- **量化数据**:
    - 874次提交
    - 542个PR被合并
    - 1,962个文件被更改，净增20万5千多行代码
    - 399个Issue已关闭（包括2个P0紧急，62个P1高优先级，16个安全相关）
    - 170位社区贡献者参与
- **影响与分析**: 从代码变更量和Issue关闭数量来看，这是一个聚焦于**提升项目表面层（用户界面、API网关、开发者体验）稳定性、功能完整性和安全性的重大更新**。大量高优先级和安全问题的解决，表明项目成熟度有了显著提升。

---

## 3. 项目进展 (合并/关闭的重要PR摘要)

今日合并或有了明确进展的PR（包括 #32297 今日关闭），主要推动了以下方向的进展：

- **核心Bug修复**:
    - **#32297** [已关闭] `fix(vision): don't retry non-retryable 4xx image downloads` - 修复了视觉工具因重试不必要下载而导致资源浪费和延迟的问题。
    - **#39813** `fix(respect user interrupt in busy_input_mode=interrupt)` - 修复了在中断模式下，网关仍强制Agent处理旧结果，无视用户中断意图的严重逻辑错误。
- **安全与代码质量**:
    - **#40253** `fix(security): replace sys.path.insert with importlib.util for tts_normalize` - 修复了一个高风险的导入路径劫持漏洞，用更安全的`importlib`替代了不安全的路径插入方式。
- **平台适配与兼容性**:
    - **#40261** `fix: only apply dots→hyphens normalization for Claude models on Anthropic provider` - **关键修复**。解决了Anthropic提供者下对所有模型强制进行点号转连字符的问题，**恢复了对第三方兼容API（如Xiaomi MiMo）的支持**，是社区高度关注的问题。
- **新功能与增强**:
    - **#40258** `feat(desktop): browse + upload to gateway filesystem on remote backends` - 桌面端重大改进，连接远程网关时，文件交互（浏览、上传）将正确指向服务器文件系统，而非本地客户端，极大提升了远程使用体验。
    - **#40257** `feat(acp): forward authenticate() OAuth bearer to provider api_key` - 增强了ACP协议的`authenticate()`方法，支持将上游OAuth令牌透传至下游LLM提供者，打通了端到端身份验证流程。
    - **#40252** `feat(prompt): inject current wall-clock time via ephemeral_system_prompt` - 为Agent注入时间感知能力，使其能根据当前时间进行更合理的决策，同时对缓存无害。
- **开发者体验**:
    - **#40254** [已关闭] `[codex] Add profile builder web flow` - 新增了基于Web的profile构建流程，简化了Agent的配置和管理。

**总结**: 项目关键Bug（如用户中断被忽略、视觉工具无限重试）和阻塞性问题（如Anthropic兼容性）得到有效解决，同时引入了文件系统、身份验证和上下文感知等实用新功能，项目正在向着更稳定、更完善、更易用的方向稳步前进。

---

## 4. 社区热点 (高互动 Issues/PRs 分析)

今日热度最高的讨论聚焦于 **桌面端体验** 和 **多语言支持**。

1.  **#40219 [Feature]: Add Japanese language support** & **#40239 [Feature]: Add Portuguese (pt-BR) support**
    - **分析**: 这两个Feature请求虽然刚开启，但迅速获得关注，表明了社区对国际化（i18n）的强烈需求，特别是对更多语言的支持。这背后是Hermes正在从英文和中文用户群体向更广泛的全球用户社区扩展的信号。

2.  **#40146 / #40226 [Bug]: Desktop app: Chinese IME input breaks** (Windows桌面端中文输入法问题)
    - **分析**: 这是今日最集中的用户痛点。多个Issue（#40146, #40226, #40145）反馈了在Windows桌面端使用中文输入法时，出现“发送按钮不切换”、“Enter无法发送”、“文字截断”等问题。这严重影响了核心用户体验，表明桌面端应用的输入法兼容性处理存在亟待修复的短板。

---

## 5. Bug 与稳定性 (按严重程度排列)

以下为今日报告的Bug，已标注修复进展：

- **P1 (高优先级)**:
    - **#39886** `cron scheduler: profile-job context bleeds into concurrent non-profile job` - 一个**严重**的并发问题，非profile的cron任务会错误地读取其他profile的脚本，导致“脚本未找到”错误。暂无关联修复PR。
    - **#40201** `[Bug] Post-compression final synthesis can fabricate source-backed findings` - Agent在上下文压缩后可能产生**虚构的、但看似有证据支持的发现**。这是一个严重影响Agent可靠性和用户信任的幻觉问题。**已有修复PR #40260**。
- **P2 (中优先级)**:
    - **#38412** `Desktop "Remote gateway" can't connect over WebSocket — /api/ws always rejected` - 桌面端连接远程网关时WebSocket连接始终被拒，导致无法使用。影响远程办公用户。暂无关联修复PR。
    - **#38488** `MCP server permanently gives up after a transient backend outage` - MCP服务器在短暂故障后永久放弃连接，不再重试，需要重启网关。破坏了MCP服务的健壮性。暂无关联修复PR。
    - **#40139** `Secret redaction modifies actual command execution instead of only masking display` - 密码脱敏功能**错误地修改了真实的命令和输出内容**，可能导致脚本执行失败和数据损坏。这是一个设计上的Bug，影响安全性和功能性。暂无关联修复PR。
- **P3 (低优先级)**:
    - **#40101** `mnemosyne-hermes Plugin: NOT installed despite correct entry point registration` - 外部Memory插件`mnemosyne`正确注册后仍无法被Hermes发现。影响插件生态的扩展性。暂无关联修复PR。
    - **#40181** `Gateway config-bridging skips plugin platforms not in the Platform enum` - 配置桥接功能忽略插件提供的平台（如LINE），导致其配置项失效。限制了插件平台的定制能力。暂无关联修复PR。

---

## 6. 功能请求与路线图信号

今日用户提出的功能请求，结合已有PR可判断未来版本方向：

- **强需求信号 (很可能被纳入)**:
    - **多语言支持** (#40219, #40239): 请求增加日语、葡萄牙语支持。已被标记为Feature，且已有类似功能的PR `#40114` 提交（增加了日语和繁体中文支持）。这表明i18n是明确的开发方向。
    - **`/approvals` 斜杠命令** (#39425): 用户希望在对话中能方便地切换到`smart`审批模式。该功能请求获得支持（+1），且有明确的逻辑定义。
- **弱需求信号 (可能被评估)**:
    - **Telegram `clarify` 工具按钮优化** (#40259): 建议在Telegram中为选择按钮显示文字而非数字。属于特定平台UI的优化。
    - **ACP `authenticate()` 转发OAuth** (#40256): 该需求有明确的实现思路，并且**当日已有对应的实现PR #40257被提交**，将成为近期的一个亮点功能。
    - **时间感知注入** (#40252): 对应有PR实现，思路清晰，预计会被合并。
- **长期方向信号**:
    - **网关健康状态暴露** (#40199): 要求网关API能更精细地报告平台适配器的健康状态，而不仅仅是进程是否存活。这表明项目部署复杂度在增加，对可观测性提出了更高要求。

---

## 7. 用户反馈摘要

从今日的Issues中提炼出的用户声音：

- **满意与认可**: 一位中国高级用户 (#40251) 对Hermes的 `skill + memory + session_search` 设计理念表达了极高的赞赏，认为其构成了真正的“学习闭环”，并分享了自己结合`git tag`进行阶段性开发的深度使用场景。这表明**核心的“可成长性”设计思路获得了专业用户的深度认同**。
- **不满意与痛点**:
    - **桌面端体验是重灾区**: 多名用户在Windows/macOS桌面端遇到严重问题，包括**中文输入法故障**、**远程网关连接失败**、**Intel Mac不支持（#37505, #38227）**，这些是阻碍用户使用的主要壁垒。
    - **可靠性问题**: 有用户反馈了“**压缩后产生虚假证据**” (#40201) 和“**cron任务上下文泄露**” (#39886) 等破坏信任的Bug。
    - **功能可用性问题**: 报告了“**MCP服务永久失联**” (#38488) 和“**插件无法安装**” (#40101) 等问题，影响了功能的可用性。
    - **令人困惑的行为**: 有用户指出“**密码脱敏功能破坏了实际命令**” (#40139)，这是一个严重的设计缺陷。

---

## 8. 待处理积压 (重点关注)

以下为长期未关闭，或今日虽有关注但仍待解决的重大议题，提醒项目维护者给予更多关注：

1. \#22196 `Anthropic provider converts dots to hyphens for ALL models` (已有PR #40261 修复，等待合并)
    - **状态**: 【PR等待合并】这是一周前就被报告的与第三方API兼容性问题，今日终于有了修复PR。建议尽快审查并合并。
    - **链接**: [Issue #22196](https://github.com/NousResearch/hermes-agent/issues/22196), [PR #40261](https://github.com/NousResearch/hermes-agent/pull/40261)

2. \#31101 `QQ Bot adapter: _read_events() silent loop after reconnect failure`
    - **状态**: 【长期未响应】自5月23日报告以来，问题持续存在。即使在今日有相关Issue（#40199）再次强调了平台健康状态的盲区问题，该核心修复仍无进展。
    - **链接**: [Issue #31101](https://github.com/NousResearch/hermes-agent/issues/31101)

3. \#38488 `MCP server permanently gives up after a transient backend outage`
    - **状态**: 【今日更新，无修复】虽然有更新，但问题依旧。MCP服务的健壮性是开发平台的基础，此问题影响面较广。
    - **链接**: [Issue #38488](https://github.com/NousResearch/hermes-agent/issues/38488)

4. \#40176 `Pinned Python deps carry known CVEs` (已有PR #40253 解决部分问题)
    - **状态**: 【部分修复】报告了`urllib3`, `python-multipart`等库的高危CVE漏洞。虽然有PR #40253修复了一个相关问题，但整体依赖更新尚未完成。鉴于这是安全漏洞，应予以最高优先级。
    - **链接**: [Issue #40176](https://github.com/NousResearch/hermes-agent/issues/40176)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 2026-06-06 日 PicoClaw 项目动态日报。

---

# PicoClaw 项目日报 | 2026-06-06

## 1. 今日速览
PicoClaw 在过去 24 小时内维持了极高的开发活跃度。项目合计处理 **40+ 个 Issue/PR**，合并关闭了 **20 个 PR**，并发布了最新的 Nightly 构建。核心维护团队展现了极强的响应力：社区昨日报告的多个 Bug（如 OneBot 群聊路由、上下文信息展示）均在当天内完成修复并合并。此外，针对 JSONL 存储引擎崩溃一致性、回退链超时处理以及 Web 后端的全面安全加固（CSRF、路径穿越）等关键基础架构 PR 也于昨日完成合入。尽管项目健康度整体处于“优秀”水平，但当日曝出的 **Evolution 模式持续消耗 Token（#3012）** 问题，作为严重级 Bug 仍悬而未决，需保持最高关注。

## 2. 版本发布
- **Nightly Build (v0.2.9-nightly.20260606.89ee8f1b)**
  - **描述**：自动化 CI 构建的快照版本，囊括了截止 2026-06-05 的所有代码变动。官方声明为不稳定版本，仅供早期测试与验证。
  - **价值**：对于急切需要验证 OneBot 修复（#3009）或体验最新功能（如 Anthropic SDK 大版本升级）的用户，此版本是当前最佳选择。
  - **完整变更日志**：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展
昨日项目在**安全性、稳定性、渠道与开发者体验**方面均取得了显著进展，具体表现为：

- **安全架构大幅提升**：
  - **#2900** `fix: add CSRF protection, path traversal validation, and security headers`：为 Web 后端添加了 CSRF 保护、上传路径穿越校验及安全响应头，极大增强了 WebUI 管理界面的抗攻击能力。
  - **#3010 / #3011** `fix(channels/agent): add ok checks for type assertions`：在渠道配置和事件退订的热路径中增加防御性 `ok` 检查，消除了因配置异常引发服务 Panic 的潜在隐患。

- **核心稳定性修复**：
  - **#2907** `Fix JSONL store metadata drift after crash`：修复了 `pkg/memory` 模块在写入 `.jsonl` 文件后、更新 `.meta.json` 前崩溃导致的元数据漂移（Crash-Consistency Bug），保障了记忆存储的可靠性。
  - **#2905** `Fix fallback chain handling for expired contexts`：修复了 Provider 回退链在请求 `Deadline` 到达后仍尝试轮询后续供应商的问题，避免了毫无意义的无用重试。
  - **#2913** `Fix JSONL session index hot-path cloning and TTL refresh semantics`：优化了会话索引在缓存命中时的内存克隆开销与 TTL 刷新逻辑，提升了热路径性能。

- **渠道与工具链 Bug 快速响应**：
  - **#3009** `fix(onebot): use prefixed chatID for group reply routing`：迅速解决了 `#3002` 中报告的一对一机器人群聊回复使用 `send_private_msg` 的错误，致命 Bug 在 1 天内完成修复。
  - **#3013** `docs: remove missing skill-creator helper script references`：修正了 skill-creator 文档，移除了对仓库中不存在脚本的引用，降低了创建自定义技能的入门门槛。
  - **#2985** `fix(context): show both summarize and compress thresholds`：响应 `#2968` 用户反馈，让 `/context` 命令同时展示软总结与硬压缩阈值，提升了配置透明度。

- **生态与依赖更新**：
  - **#2962** `build(deps): bump anthropic-sdk-go from 1.26.0 to 1.46.0`：大幅升级了 Anthropic 官方 Go SDK，一般包含新特性支持（如工具调用扩展、流式优化等）。
  - **#2915** `feat(providers): add CommonModels for MiMo provider`：为国产模型 MiMo 添加了 Vision/Text 的标准模型列表，方便 WebUI 推荐。

## 4. 社区热点
- **热议焦点：[#1042] `exec`工具`guardCommand`方法误报路径** (已关闭)
  - **链接**: `sipeed/picoclaw Issue #1042`
  - **分析**: 该 Issue 虽为陈旧问题（已关闭），但其 **15 条评论** 揭示了用户对工具调用安全策略“智能化”的深度诉求。用户 `icyfire` 生动地举例：执行 `curl -s “wttr.in/Beijing?T”` 查天气时，`guardCommand` 通过简单正则匹配将 `Beijing?T` 误判为 `../../Beijing?T` 路径穿越。社区普遍认为安全策略不应是简单粗暴的字符串匹配，而需要理解参数语义（如 URL 参数）。该问题虽已关闭，但遗留的安全-灵活性平衡讨论值得维护者深思。

- **新晋热点：[#3012] Evolution 模式每分钟持续消耗 Token** (Open)
  - **链接**: `sipeed/picoclaw Issue #3012`
  - **分析**: 由用户 `xpader` 于昨日刚报告的问题，目前虽仅 1 条评论（无关联修复 PR），但因其直接关系到用户 API 账单，极有可能成为今日社区讨论的绝对焦点。此 Bug 严重度很高，会直接影响付费用户对 Evolution 功能的使用信心。

## 5. Bug 与稳定性
| 严重程度 | 状态 | Issue / PR | 摘要 |
| :--- | :--- | :--- | :--- |
| **Critical** | **Open** | **#3012** (Issue) | **Evolution 模式持续消耗 Token**。用户报告开启后每分钟都在计费，极可能为 Agent 循环逻辑缺陷。**暂无 Fix PR，需立即关注。** |
| **High** | **已修复** | **#3002 / #3009** | **OneBot 群聊回复错误**。群聊消息发成了私聊 API，导致 NapCat 报错。修复已合入。 |
| **Medium** | **已修复** | **#2968 / #2985** | **/context 命令展示缺失**。只显示压缩阈值，用户无法确认是否触发了总结。修复已合入。 |
| **Low** | **已修复** | **#3010 / #3011** | **类型断言 Panic 风险**。在渠道哈希计算与事件退订中，因配置不合法导致运行时 Panic。修复已合入。 |
| **Won't Fix** | **已关闭** | **#1042** | `exec` 工具路径误报。已由维护者关闭，方案可能是调整文档或判定为预期行为。 |

## 6. 功能请求与路线图信号
- **Skill 系统审计 (Issue #652)**：这是一个**长期未决**的 Task。尽管 #3013 修正了文档指引，但 Issue 本身仍开放，且 To-Do 列表中“审计所有技能”的第一步未完成。这暗示核心技能系统可能仍在重构中，短期内社区 PR 触及核心代码的复杂度可能较高。
- **渠道多实例化 (PR #2551, Stale)**：此 PR 自 4 月起停滞，旨在解耦渠道名称与 Provider 类型，允许部署多个同类型渠道（如两个 Telegram Bot）。这是从“玩具”走向“企业级部署”的关键架构，大概率是 **v0.3.0 路线的核心目标**。
- **多模态能力深化 (PR #2964, Stale)**：图片输入压缩 Feature 昨日未有进展，仍处于 Stale。但随着 MiMo 等 Provider 的 Vision 模型支持完成（#2915），为图片添加压缩策略的需求会更加迫切。此 PR 值得维护者给予更多关注，以免打击贡献者积极性。

## 7. 用户反馈摘要
- **极强的 Bug 修复满意度**：用户 `Xuan-Xuann` 在 6 月 4 日报告 OneBot 的严重 Bug，6 月 5 日即被完整修复。这种“隔夜修”的响应速度极大提升了社区对项目生命力和维护者专业度的正向评价。
- **对 Agent 行为透明度的强烈诉求**：用户 `xpader` 是反馈的典型代表。他不仅报告了严重的计费 Bug（#3012），也通过 #2968 表达了对上下文状态不透明的困惑。这反映出中重度用户希望拥有对 Agent 内存、Token 消耗和进化行为的完全可视化监控。修复 #2985 是很好的第一步，但功能层面的防损耗机制（如 #2964 的压缩）和计费暴雷修正是更好的解决方案。
- **安全功能需要更智能**：来自 #1042 的讨论表明，用户已经熟练掌握了 PicoClaw 的高级安全特性（`restrict_to_workspace`），但他们期待的是一个能区分“真实路径”和“URL参数/命令参数”的智能系统，而非简单的正则黑魔法。

## 8. 待处理积压
以下长期未更新的 Issue/PR 当前处于积压状态，建议维护者基于路线图进行明确裁决（关闭或纳入目标版本）：
- **Issue #652** `[Task] Check correction of workspace skills/ skill-creator`
  - 创建于 2026-02-22，目前仍然 Open。文档已修复，但任务本体未完成。请明确此任务的目标版本。
- **PR #2551** `refactor: standardize channel identification and decouple name from provider type`
  - 自 2026-04-16 起无新提交，处于 Stale 状态。代码改动量巨大，若难以维护，建议团队决策是否关闭或由核心成员接管重写。
- **PR #2964** `Feat/image input compression`
  - 自 2026-05-28 起无新活动。这是一项社区急需的多模态特性，若方向没问题，团队应尽快回复作者，给予合并预期或具体修改意见，避免优质贡献流失。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，遵照您的指示。作为AI智能体与个人AI助手领域的开源项目分析师，我已根据NanoClaw项目（`nanocoai/nanoclaw`）在2026年6月5日至6月6日期间的GitHub活动数据，为您生成以下项目动态日报。

---

### NanoClaw 项目动态日报 | 2026-06-06

---

#### 1. 今日速览

项目在过去24小时内保持稳定，未报告新的Issue，但通过3个Pull Request（PR）的提交与合并，在稳定性修复与开发者体验改进方面取得了实质性进展。社区活跃度中等偏低，贡献集中在少数几位核心开发者（`gavrielc`）和外部贡献者（`ddaniels`），修复了两个关键性问题：OneCLI配置引导优化和API错误处理机制的完善。项目整体状态健康，正在进行针对性的质量改进。

#### 2. 版本发布

无

#### 3. 项目进展

今天项目推进了两个重要的修复与优化，这些改动均已合并到主分支：

- **修复 OneCLI 配置与文档问题 (PR #2690, #2691)**: 这两项改动由 `gavrielc` 提交，旨在优化用户首次设置 Hugging Face token 时的体验。
    - **简化HF Token设置 (PR #2690)**: 修复了一个默认秘钥模式 `secretMode` 的文档和逻辑错误。自动创建的Agent默认使用 `all` 模式，因此无需再为每个Agent单独分配秘钥，此举简化了设置流程，降低了用户的理解成本。
    - **智能显示OneCLI设置URL (PR #2691)**: 改进了用户未登录时的错误提示。现在，当系统检测到 `credential_not_found` 错误时，会从错误体中解析出正确的 OneCLI 网关 URL，而非硬编码本地或托管地址，解决了容器化部署环境下URL显示不准确的痛点。
- **增强API调用稳定性 (PR #2692, 待合并)**: 外部贡献者 `ddaniels` 提交了一个重要的稳定性修复。当 Claude 代理 SDK 遇到临时性API错误（如`529 Overloaded`）并耗尽重试次数后，系统不再将其报告为最终错误结果，而是转为重试机制，并在尝试完全失败后发出通知。这解决了原有设计中“静默失败”的潜在风险，提升了系统在面对瞬时波动时的鲁棒性。

#### 4. 社区热点

今日社区讨论热度不高，但有一个PR因其修复的通用性值得关注：

- **PR #2692: 修复API错误重试机制** (`nanocoai/nanoclaw PR #2692`) - 虽然尚未合并，但此PR修复了一个关键的用户痛点：当上游API不稳定时，NanoClaw会错误地将临时错误作为最终结果返回，而不是重试。社区对此类问题的关注反映了对**服务端稳定性与容错能力**的普遍诉求，尤其是在依赖外部AI模型API的场景下。

#### 5. Bug 与稳定性

今日修复和报告的Bug主要集中在配置逻辑与核心API交互层面，按严重程度排列如下：

- **【中】API临时错误处理不当 (已修复PR #2692)**: 核心稳定性问题。`Claude Agent SDK`在遭遇 `5xx` 级临时错误（如过载）并重试失败后，会将此错误作为一个终端“结果”消息反馈，而非抛出异常。这导致调用方无法区分是请求完成但结果错误，还是根本未成功执行。贡献者 `ddaniels` 提交了PR，将其改为重试并通知，防止“静默错误”传播。
- **【低】OneCLI设置URL硬编码 (已修复PR #2691)**: 部署环境适应性问题。未登录时的错误提示硬编码了本地和托管URL，对于处在不同网关后的容器实例不适用。
- **【低】HF Token设置文档与逻辑不一致 (已修复PR #2690)**: 文档错误与轻微用户体验问题。文档中关于 `secretMode` 的描述与默认行为不符，导致用户执行了多余的配置步骤。

#### 6. 功能请求与路线图信号

- **增强的容错与重试机制**: PR #2692 揭示了社区对改进API错误处理的需求。此PR已被接受并准备合并，预计会纳入后续的小版本中，作为对系统稳定性的核心加强。
- **智能化的部署环境感知**: PR #2691 虽是一个bug修复，但其体现的“让程序自动发现并适应其部署环境”的思路，是提升开发者体验的重要方向。这可能预示着未来NanoClaw会加入更多环境感知的自动化配置功能。

#### 7. 用户反馈摘要

今日从PR描述中提炼的用户痛点如下：

- **部署适配**: 用户 (或开发者 `gavrielc` 代表用户) 反馈在容器化环境下，OneCLI的引导信息不准确，无法正确告知用户登录入口，造成了配置障碍。
- **误报与调试困难**: 用户 (或开发者 `ddaniels` 代表用户) 反馈API调用失败时，错误信息具有误导性（表现为正常结果消息而非错误），导致他们难以定位真正的服务不稳定问题，增加了调试成本。

#### 8. 待处理积压

- **PR #2692: API临时错误重试与通知** (`nanocoai/nanoclaw PR #2692`): 这是一个来自外部贡献者的、针对核心稳定性问题的修复。虽然已由作者标记为“准备好”，但尚未被项目维护者合并。建议项目维护者尽快审核并合并此PR，以避免该问题影响更多用户。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是根据您提供的 NullClaw 项目数据（截至 2026-06-06）生成的项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-06

## 1. 今日速览

今日项目活跃度偏低，整体状态较为平稳。过去24小时内，项目未产生新的Issue或版本发布，社区讨论热度不高。关键动态是收到了一项新的功能合并请求（PR #947），旨在增加对第三方模型网关Evolink的支持，表明项目在扩展AI供应商兼容性方面仍在持续推进。虽然无重大合并或修复，但这一新增PR为平台带来了新的集成潜力。项目当前维护重点似乎正转向生态整合，而非内部缺陷修复。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日无已合并或关闭的重要PR。项目进展主要体现在新增的待合并PR上。

- **[PR #947] feat(providers): add Evolink as an OpenAI-compatible provider**：该PR由外部贡献者提出，旨在将Evolink集成成为NullClaw原生支持的OpenAI兼容提供商。这代表项目在推动“多模型网关”集成方面迈出了一步，简化了用户通过单一端点访问多个大模型（如GPT-5, Gemini, DeepSeek等）的配置流程。虽然尚未合并，但此举拓宽了项目的提供者生态。

## 4. 社区热点

今日唯一的讨论焦点即为新开放的PR #947。该PR在当前活跃度较低的社区中成为主要话题，反映了社区以下诉求：

- **对“一站式模型访问”的强烈需求**：开发者（EvoLinkAI）提出的解决方案旨在解决用户需要管理多个模型提供商API密钥和端点的痛点。社区对此类能够简化基础设施、提供统一接口的方案兴趣浓厚。
- **对OpenAI兼容接口的偏好**：该PR强调Evolink提供与OpenAI兼容的端点，这表明社区用户普遍倾向于使用标准化的API协议，以降低学习成本和迁移难度。

## 5. Bug 与稳定性

今日未报告重大Bug、崩溃或回归问题。项目稳定性表现良好，未收到影响正常使用的严重问题反馈。

## 6. 功能请求与路线图信号

今日最主要的功能请求信号来自PR #947。该请求通过代码实现而非Issue讨论的形式提出，明确指向了路线图上的一个潜在方向：

- **信号：扩大“供应商”/“提供商”生态**：集成Evolink不仅是一个单独的功能点，更是项目提升其作为“AI网关”或“统一接口”价值的关键步骤。这表明NullClaw的路线图可能正计划对标Ollama、LiteLLM等项目，通过增加更多后端提供商来吸引用户。
- **判断**：由于该PR结构完整（已提供代码实现），且属于非破坏性的功能增强，很有可能会被项目维护者纳入下一个版本（例如 v0.x 或下一个修订版）进行合并。

## 7. 用户反馈摘要

由于今日无Issue更新和评论，直接的用户反馈数据为零。但结合PR #947的上下文，可以推测潜在用户的几点诉求：

- **痛点：配置繁多**：用户希望在单一工具中切换不同模型，而不是管理多个后台服务。
- **期望：零配置切换**：用户期望NullClaw能像Evolink这类服务一样，只需修改一个“模型名称”字段即可切换底层AI引擎，而无需改动代码或环境变量。

## 8. 待处理积压

当前无长期未响应的重要Issue或PR。PR #947是今日新增请求，等待项目维护者审核与合并。建议维护者尽快对该PR进行代码审查、测试兼容性，并给予作者反馈，以维持社区贡献者的积极性。

- **待关注链接**：[PR #947 feat(providers): add Evolink as an OpenAI-compatible provider](https://github.com/NullClaw/nullclaw/pull/947)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw 项目动态日报 · 2026-06-06**  
**数据周期：2026-06-05 ~ 2026-06-06（UTC）**

---

### 1. 今日速览

过去 24 小时项目活跃度极高：共 13 条 Issues 更新、50 条 PR 更新，核心团队集中合入了 **Reborn Hook 框架** 的整套生产级基础设施（含持久化后端与安全审计），标志着该功能的里程碑达成。WeCom 频道持续收获修复型 PR 与用户反馈，Slack 集成功能进入深度开发阶段。Nightly E2E 仍处于失败状态，新上报的 sandbox 信号量 bug（#4512）需要立即关注。整体来看，项目在基础设施重构上迈出关键一步，社区讨论集中在架构拆分与渠道完善，发布节奏受 release PR（#3708）阻塞。

---

### 2. 版本发布（无）

过去 24 小时内无新版本发布。

---

### 3. 项目进展

今日共合并/关闭 12 个 PR，其中核心团队 @zmanian 完成了 **Reborn Hook 框架** 的系列落地：

| PR | 内容 | 影响力 |
|----|------|--------|
| [#3938](https://github.com/nearai/ironclaw/pull/3938) | 在生产环境激活 Hook 框架（默认关闭），解决 #3934 | 钩子系统从潜伏变为可开关，奠定扩展基础 |
| [#3937](https://github.com/nearai/ironclaw/pull/3937) | 跨后端对抗性 parity 测试（Postgres / libSQL / 内存） | 确保三种 PredicateStateBackend 行为一致 |
| [#3933](https://github.com/nearai/ironclaw/pull/3933) | PostgresPredicateStateBackend | 提供跨主机一致的持久后端 |
| [#3936](https://github.com/nearai/ironclaw/pull/3936) | LibSqlPredicateStateBackend | 补充轻量级持久选项 |
| [#3931](https://github.com/nearai/ironclaw/pull/3931) | 修复跨租户泄露、重放、provider spoofing 三个安全漏洞 | 关键安全加固 |
| [#3922](https://github.com/nearai/ironclaw/pull/3922) | SecurityAuditSink 接入 obligation handler 和 hook deny 路径 | 审计能力增强 |
| [#3928](https://github.com/nearai/ironclaw/pull/3928) | arguments_digest snapshot 测试落到正确调用层 | 测试质量提升 |

此外，@elliotBraem 的 **[#2904](https://github.com/nearai/ironclaw/pull/2904)**（11 个 WASM 代理工具替换为基于 SKILL.md 的 HTTP 声明）与 **[#2550](https://github.com/nearai/ironclaw/pull/2550)**（新增技能框架与调查技能示例）于今日合并，显著简化了安全模型并加速新技能接入。

**项目健康度**：基础设施层完备度大幅提升；现已具备生产就绪的 Hook 框架、跨后端一致性保证、以及更安全的工具声明模型。

---

### 4. 社区热点

以下议题获得最多评论或引起广泛讨论：

- **#4488 `[Reborn] Split ProductWorkflow into explicit submit/read/subscribe doors`**（[讨论入口](https://github.com/nearai/ironclaw/issue/4488)）  
  作为父任务 #3280 的关键子问题，两位开发者先后发表设计观点，并直接催生了实现 PR #4506。社区成员正就如何对接 OpenAI 兼容 API 展开架构层面的辩论。

- **#4311 `Reborn model gateway collapses budget governance failures into context-overflow recovery`**（[讨论入口](https://github.com/nearai/ironclaw/issue/4311)）  
  持续发酵的预算治理错误映射问题，已有 2 条 review 评论指出 agent loop 的异常分类逻辑可能使运维难以定位真正原因。

- **#4502 `WeCom group chat approval reply does not work`**（[讨论入口](https://github.com/nearai/ironclaw/issue/4502)）  
  WeCom 用户的核心流程阻塞，评论集中在期待快速修复。整个 WeCom 系列（#4191、#4500、#4505）共同反映了新频道在边缘场景下的打磨需求。

- **#4491 `Use Slack AI streaming for Reborn Slack progress`**（[讨论入口](https://github.com/nearai/ironclaw/issue/4491)）  
  虽然评论数少，但关联的 stopgap PR #4490 已在 Slack 社区中引发短期 vs 长期方案的讨论，暴露用户对实时反馈的强需求。

---

### 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue/PR | 描述 | 状态 |
|----------|----------|------|------|
| 🔴 Critical | [#4512](https://github.com/nearai/ironclaw/issue/4512) | `Concurrent sandbox job_semaphore is never acquired` — 信号量从未被 acquire，可导致并发沙箱资源竞争 | 新建，无修复 PR |
| 🔴 Critical | [#4108](https://github.com/nearai/ironclaw/issue/4108) | Nightly E2E 持续失败（5/27 起，最新失败 6/5） | 持续开放，未分配 |
| 🟠 High | [#4502](https://github.com/nearai/ironclaw/issue/4502) | WeCom 群聊审批回复 `y/yes/always` 无效 | 开放 |
| 🟠 High | [#4500](https://github.com/nearai/ironclaw/issue/4500) | Onboarding 系统事件写入错误会话（WeCom & Telegram） | 开放 |
| 🟡 Medium | [#4505](https://github.com/nearai/ironclaw/issue/4505) | WeCom 群聊在 UI 侧边栏无法区分标题 | 开放 |
| 🟡 Medium | [#4191](https://github.com/nearai/ironclaw/issue/4191) | WeCom 频道总体验证结果：多个 ⚠️ 问题（附件/标签/身份等） | 持续跟踪 |
| ⚪ Low | [#4194](https://github.com/nearai/ironclaw/issue/4194)（已关闭） | 群聊和私信被合并为同一会话 | 已于今日关闭，表明修复已上线 |

**总体稳定性评价**：核心消息流在 WeCom 上基本可用，但系列 bug 显示新通道仍需密集迭代；CI 持续失败是当前最严重的阻塞项。

---

### 6. 功能请求与路线图信号

今日活跃的功能性 PR/Issue 集中反映了下一阶段的路线图方向：

- **产品架构精简**：`[Reborn] Split ProductWorkflow`（[#4488](https://github.com/nearai/ironclaw/issue/4488)，实现 PR [#4506](https://github.com/nearai/ironclaw/pull/4506)）与 `Harden ProductWorkflow boundary`（[#4483](https://github.com/nearai/ironclaw/issue/4483)），为 OpenAI 兼容 API 接口做准备。
- **多通道增强**：Slack 渠道获得两项重大功能 PR——**频道路由管理**（[#4510](https://github.com/nearai/ironclaw/pull/4510)）与 **AI streaming 反馈**（[#4491](https://github.com/nearai/ironclaw/issue/4491) + [#4490](https://github.com/nearai/ironclaw/pull/4490)）；同时 `outbound preference` 门面（[#4511](https://github.com/nearai/ironclaw/pull/4511)）为多渠道出站奠定合约基础。
- **扩展生态**：`IronHub 安装流迁移至 Reborn`（[#4479](https://github.com/nearai/ironclaw/pull/4479)）使第三方技能安装可检验签名并集成到仓库管理。
- **权限模型演进**：`Runtime profiles into approval gates`（[#4390](https://github.com/nearai/ironclaw/pull/4390)）将运行配置纳入审批决策，增强灵活性。

这些项目大部分已在开发中或拥有对应 PR，预计将随下一次版本（v0.30.0 或更晚）发布。

---

### 7. 用户反馈摘要

主要来自 @sunglow666 在 WeCom 相关问题中的叙述：

- **正面**：“核心文本消息流基本稳定”、“配对/重连/持久化/Markdown/多语言支持表现良好”。 → 对 v0.29.1 基础能力认可。
- **痛点**：群聊审批回复无效导致工具无法使用；onboarding 事件写入旧会话造成混乱；群聊标题不区分使管理困难。 → 期望迭代修复。
- **未明确需求**：在已关闭的 #4198 中，团队对于未配对用户的 owner 可见性选择保持为预期隐私行为，用户接受但表示需要文档说明。
- **其他渠道**：Telegram 同样出现 #4500 中的 onboarding 问题，暗示该 bug 为跨渠道共性。

社区整体反馈集中在 **“新渠道基本可用，但边界条件需快速跟上”**。

---

### 8. 待处理积压

以下 Issue/PR 长期未响应或阻塞关键路径：

| 类别 | 链接 | 原因 / 影响 |
|------|------|-------------|
| ⚠️ CI | [#4108](https://github.com/nearai/ironclaw/issue/4108) Nightly E2E 持续失败（>10 天） | 可能隐藏回归，需优先根因分析 |
| 🛑 阻塞 | [#3708](https://github.com/nearai/ironclaw/pull/3708) Release PR（5/16 起开放） | 已包含 API breaking 变更，可能由于测试或依赖就绪问题未被合并，阻塞发布流程 |
| 🔴 新 Bug | [#4512](https://github.com/nearai/ironclaw/issue/4512) Sandbox job_semaphore never acquired | 高风险并发缺陷，暂无回应 |
| 🔄 设计 | [#4311](https://github.com/nearai/ironclaw/issue/4311) Budget governance 错误映射 | 开放 6 天仍无进展，影响 agent loop 错误分类准确性 |
| 📋 渠道 | [#4191](https://github.com/nearai/ironclaw/issue/4191) WeCom 总体验证清单 | 多个子项未关闭，需要持续跟踪 |

维护团队应优先关注 Nightly E2E 根因与 #4512 的修复分配；release PR 的推进将有助于统一发布上述功能的版本。

---

**项目总结**：Reborn Hook 框架的完工是今日最重大的进展，为扩展性、安全性和持久化能力打下坚实基础。渠道侧进入密集修复期，整体项目健康状况良好，但需要快速解决 CI 与 sandbox 信号量问题以保持交付节奏。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-06-06

数据来源：GitHub (netease-youdao/LobsterAI)  
统计时段：2026-06-05 至 2026-06-06

---

## 今日速览

过去 24 小时，项目共处理 **3 条 Issue 更新** (均为开放状态，无关闭)、合并/关闭 **12 个 Pull Request**，并发布了 **1 个新版本** (v2026.6.5)。社区方面，3 个搁置已久的 Bug 报告获得新的评论，表明用户仍在关注数据丢失等关键问题。大量 PR 集中于 cowork、语音输入、文件预览和安全性改进，版本迭代节奏较快，项目整体活跃度高。

---

## 版本发布

### LobsterAI 2026.6.5 (2026-06-05)
- **新增特性**
  - `feat(cowork):` 改进频道会话同步与清理逻辑
  - `feat(shortcuts):` 重构键盘快捷键，扩展支持的操作并优化交互体验
- **破坏性变更** 无
- **迁移注意事项** 无特殊说明；建议用户留意快捷键变更后的默认绑定，若自定义配置可能需手动调整。

详情：[Release v2026.6.5](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.5)

---

## 项目进展

今日共有 **12 个 PR 合并/关闭**，涵盖从新功能到安全修复的多个方面：

| PR | 模块 | 摘要 |
|----|------|------|
| [#2119](https://github.com/netease-youdao/LobsterAI/pull/2119) | renderer, build, docs, main, openclaw, cowork, im, macos, artifacts | **发布 v2026.6.4**，打包了数项新特性与修复 |
| [#2118](https://github.com/netease-youdao/LobsterAI/pull/2118) | renderer, main, cowork, artifacts | 修复剪贴板复制与提交体验，引入 Electron → navigator.clipboard → textarea 降级链 |
| [#2117](https://github.com/netease-youdao/LobsterAI/pull/2117) | renderer | 修复配置迁移后被删除的 provider 模型重新出现的问题 |
| [#2116](https://github.com/netease-youdao/LobsterAI/pull/2116) | renderer, main, cowork | 改进错误 UX 与空状态引导，重复流错误去重，添加快捷键对齐入口 |
| [#2115](https://github.com/netease-youdao/LobsterAI/pull/2115) | docs, main, im | 修复 IM 模块仅从当前轮次组装回复，并改进 Windows 更新安装器 |
| [#2114](https://github.com/netease-youdao/LobsterAI/pull/2114) | renderer, cowork, artifacts | 增强文件预览与展开面板体验，支持 HTML 浏览器预览、缩放兼容修复 |
| [#2113](https://github.com/netease-youdao/LobsterAI/pull/2113) | build, main, macos | 为 macOS 语音输入添加麦克风权限申请和媒体策略注册 |
| [#2112](https://github.com/netease-youdao/LobsterAI/pull/2112) | renderer, main, openclaw | 推出付费提示界面（锁定模型点击转向登录/订阅）与 openclaw 修复流程 |
| [#1531](https://github.com/netease-youdao/LobsterAI/pull/1531) | settings | 主题色选择器由网格改为紧凑圆形选择器（4月旧PR，今日合并） |
| [#1533](https://github.com/netease-youdao/LobsterAI/pull/1533) | cowork | 设置页面新增本地会话使用统计面板（基于 SQLite 聚合查询） |
| [#1534](https://github.com/netease-youdao/LobsterAI/pull/1534) | security | API 代理日志不再打印完整 URL、Header、Body，避免凭证泄露 |
| [#1535](https://github.com/netease-youdao/LobsterAI/pull/1535) | security | 渲染进程 KV Store IPC 增加键白名单，限制敏感数据访问 |

这些更新使 cowork 交互稳定性、文件预览能力、语音输入支持以及整体安全性都得到显著提升。

---

## 社区热点

### 讨论最活跃的 Issues

| Issue | 标题 | 评论数 | 核心关注点 |
|-------|------|--------|------------|
| [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | 会话中调用python脚本出现问题 | 2 | 本地 30B 模型运行 skills 时 Python 脚本失效，其他 CLI 正常，怀疑执行环境隔离问题 |
| [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | 切换会话或视图时输入框草稿因去抖未及时持久化导致内容丢失 | 1 | 300ms debounce 导致快速切换后未发送内容丢失，影响工作流信任 |
| [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | 重新编辑历史消息时直接覆盖当前输入框未发送内容，无确认提示 | 1 | 编辑历史消息时静默覆盖当前输入内容，用户数据易丢失 |

三个 Issue 均已在 2026-04 提出，今日获得新评论，说明社区仍未得到满意解决方案。其中 **#1471** 和 **#1472** 涉及数据丢失，优先级较高。

### 讨论最少的 PR
今日所有 PR 均无评论（comment: undefined），社区对大量合并反馈平淡，可能因多数为内部开发团队驱动。

---

## Bug 与稳定性

### 今日修复的 Bug（通过合并 PR）

| 严重程度 | PR | 问题描述 |
|----------|----|----------|
| **高** | [#2118](https://github.com/netease-youdao/LobsterAI/pull/2118) | 跨平台剪贴板复制失效（降级链修复） |
| **高** | [#2117](https://github.com/netease-youdao/LobsterAI/pull/2117) | 配置迁移后用户删除的 provider 模型重新出现 |
| **高** | [#2115](https://github.com/netease-youdao/LobsterAI/pull/2115) | IM 回复从所有历史消息中组装而非当前轮次，导致上下文错误 |
| **高** | [#2113](https://github.com/netease-youdao/LobsterAI/pull/2113) | macOS 语音输入因缺少麦克风权限而无法工作 |
| **中** | [#2116](https://github.com/netease-youdao/LobsterAI/pull/2116) | 错误提示重复出现、空状态无引导 |
| **中** | [#2114](https://github.com/netease-youdao/LobsterAI/pull/2114) | 文件预览缩放重叠、展开面板布局错乱 |
| **低** | [#1534](https://github.com/netease-youdao/LobsterAI/pull/1534) | API 代理日志泄露凭证和完整响应体 |
| **低** | [#1535](https://github.com/netease-youdao/LobsterAI/pull/1535) | 渲染进程可越权读取敏感 store 键 |

### 待修复的活跃 Bug（Issue 仍 open）

- [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) Python 脚本调用问题 — 无对应 fix PR
- [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) 草稿丢失 — 无对应 fix PR
- [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) 编辑覆盖丢失内容 — 无对应 fix PR

建议维护者优先评估这三个长期未解决的数据相关 Bug。

---

## 功能请求与路线图信号

从今日合并的 PR 中可以看出项目后续发展的一些方向：

- **语音输入**：基于认证的 ASR 语音输入已落地 ([#2112](https://github.com/netease-youdao/LobsterAI/pull/2112)、[#2113](https://github.com/netease-youdao/LobsterAI/pull/2113))，未来可能扩展到更多交互场景。
- **文件协作**：文件预览支持 HTML 浏览器预览、展开面板、多种格式缩放适配 ([#2114](https://github.com/netease-youdao/LobsterAI/pull/2114))，反映对多类型文档内联预览的需求。
- **使用统计与付费集成**：设置页添加本地会话统计面板 ([#1533](https://github.com/netease-youdao/LobsterAI/pull/1533))，付费提示界面出现在锁定模型上 ([#2112](https://github.com/netease-youdao/LobsterAI/pull/2112))，暗示项目正在构建订阅/试用限制体系。
- **社区贡献吸收**：4 月提交的旧 PR（主题色选择器、统计面板、安全修复）今日统一合并，说明项目在清理积压贡献，但对快速迭代的社区预期来说响应周期稍长。

用户尚未提出明确的新功能请求（Issues 中均为 Bug 报告），但草稿持久化问题（#1471）可视为对**本地状态同步机制**的改进需求，可能影响未来输入组件设计。

---

## 用户反馈摘要

从今日更新的 Issue 描述中提炼的真实用户痛点：

| 用户 | 场景 | 反馈要点 |
|------|------|----------|
| `54huige` | 使用本地 30B 模型，在会话中执行 Python skills | 同样的技能在 Claude Code CLI 和其他客户端正常，LobsterAI 内调用却失败；怀疑执行环境隔离或路径配置问题。 |
| `MaoQianTu` | 编辑历史消息时触发覆盖 | “重新编辑”按钮无任何确认直接替换当前未发送内容，导致长篇输入瞬间丢失，期望弹出确认对话框。 |
| `MaoQianTu` | 快速切换会话/视图 | 300ms debounce 使草稿在组件卸载时未能持久化，切换后内容消失；期望卸载时强制同步或缩短延迟。 |

此外，安全贡献者 `kayo5994` 通过提交 PR 发现并修补了日志和 IPC 权限问题，体现了社区对安全性提升的积极参与。

---

## 待处理积压

以下长期开放但今日仍有更新的 Issue 应引起维护者注意：

| Issue | 创建时间 | 上次更新 | 简述 |
|-------|----------|----------|------|
| [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | 2026-04-05 | 2026-06-05 | 用户已等待超过 2 个月，Python 脚本执行问题仍未解决，仍为 open 且 stale。 |
| [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | 2026-04-04 | 2026-06-05 | 草稿丢失问题影响核心输入体验，用户除初始报告外另获一条评论支持，仍无进展。 |
| [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | 2026-04-04 | 2026-06-05 | 静默覆盖问题同样涉及数据安全，无 assignee 也无关联 PR。 |

这些 Issue 直接影响用户日常使用信心。若团队近期有其他优先级，建议至少回复用户预期时间表或标记为 accepted。

---

**今日总结**：LobsterAI 开发活跃，安全性和新功能进展迅猛，但用户侧的关键 Bug 修复存在滞后。保持迭代速度的同时，平衡社区反馈的闭环将是提升项目健康度的关键。

---
*生成时间：2026-06-06 08:00 UTC*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-06-06

---

## 1. 今日速览

过去 24 小时，Moltis 项目处于 **中高活跃度** 状态。社区提交了 4 个议题和 5 个拉取请求，关键动态包括：Telegram 流式输出的严重 Bug 已被修复并合并、沙箱（Docker/Podman）兼容性改进 PR 集中提交、Web UI 细节 Bug 与功能请求齐发。无新版本发布，但修复与开发节奏紧凑，项目健康度良好。

---

## 2. 版本发布

无新版本发布（本节省略）。

---

## 3. 项目进展

- **[已合并 / 重要修复] PR #1099 —— 分离 Telegram 进度流与最终回复**
  作者：s-salamatov

  该 PR 成功修复了 **Issue #1097** 中描述的严重问题：Telegram 渠道的流式编辑输出会将中间推理过程混入最终回复中。现在流式输出被严格限制为临时进度更新，正常最终回复独立发送，完成后删除临时消息。这一修复对依赖 Telegram 进行日常交互的用户体验提升显著。

  同时，尚在待合并队列的有：
  - **PR #1089**：限制会话恢复时持久化工具结果的大小，防止消息过长（已开放近一周）。
  - **PR #1104 / #1105 / #1106**：来自贡献者 `penso` 的三条 PR，分别涉及 Provider 模型偏好替换、Docker 沙箱文件系统回退修复、Podman 沙箱逃逸机制支持。

---

## 4. 社区热点

- **最活跃用户：@IlyaBizyaev**
  该用户在昨日集中提交了 **3 个议题（#1107, #1108, #1109）**，覆盖 Web UI 的移动端输入、时间格式展示，以及 Docker 安装场景的更新提示问题，是现阶段社区最活跃的缺陷/需求反馈者。

- **最快闭环：Bug #1097 → PR #1099**
  Telegram 流式输出混乱的问题从报告（6月3日）到修复合并（6月5日），仅用约 **72 小时** 完成闭环，体现了团队对高优通信流 Bug 的快速响应能力。

---

## 5. Bug 与稳定性

| 严重程度 | 编号 | 标题 | 状态 | 关联修复 |
|---|---|---|---|---|
| 🔴 严重 | [#1097](https://github.com/moltis-org/moltis/issues/1097) | Telegram 编辑中流式输出混淆最终回复 | ✅ 已关闭 | [#1099](https://github.com/moltis-org/moltis/pull/1099) |
| 🟡 中度 | [#1109](https://github.com/moltis-org/moltis/issues/1109) | Docker 安装不显示更新横幅 | ❌ 待处理 | 暂无 |
| 🟢 较低 | [#1108](https://github.com/moltis-org/moltis/issues/1108) | Web UI 会话列表仅显示时间不显示日期 | ❌ 待处理 | 暂无 |

**分析：**
- **#1109** 值得引起注意：若 Docker 用户无法收到更新提示，可能在无感知情况下落后于版本安全修复，建议考虑通过检测容器环境变量或额外通道推送通知。
- **#1108** 属于 UX 细节打磨，虽然影响范围小，但对日常使用习惯的干扰明显，修复成本较低。

---

## 6. 功能请求与路线图信号

- **[功能请求] [#1107](https://github.com/moltis-org/moltis/issues/1107) —— 移动端多行文本输入**
  用户希望在 Mobile Web UI 中输入多行文本（而非仅单行回车发送）。这是移动办公场景的刚性需求，考虑到 Web UI 正处于迭代窗口期，该请求有较大概率被纳入下一个版本。

- **[路线图信号] Provider 配置弹性提升**
  [#1104][PR #1104] 允许用户解除已保存的首选模型绑定，包括清空所有偏好。这表明项目正在完善多 Provider 管理的灵活性和用户控制力。

- **[路线图信号] 容器生态扩展**
  [#1105][PR #1105] 修复 Docker 沙箱写入回退逻辑；[#1106][PR #1106] 加入 Podman 沙箱逃逸机制。两条 PR 均来自 `penso` 且在同一天提交，**强烈暗示下一版本将重点提升多种容器方案的兼容性与部署鲁棒性**，对自托管用户是积极信号。

---

## 7. 用户反馈摘要

从今日议题与 PR 描述中可提炼出以下真实用户反馈：

- **“Docker 是我部署的主要方式，我需要正确的版本更新提示”** —— 用户 @IlyaBizyaev 明确指出了 Docker 安装场景下的信息缺失问题，直观反映了 **容器化部署用户群体的增长及他们对原生体验的期待**。
- **“移动端不让我换行，这限制了复杂输入的效率”** —— 同样是 @IlyaBizyaev，表明部分用户已开始将 Moltis 作为日常生产力工具在移动环境下使用，并期望获得与桌面端一致的输入体验。
- **“提交者也是修复者：痛点驱动开发”** —— @s-salamatov 同时是 Telegram 修复 PR 的作者和 Bug 报告者，这种“自驱纠错”的行为模式凸显了核心贡献团体的技术深度与对质量的坚持。

---

## 8. 待处理积压

- **[高优先 / 待合并] [#1089](https://github.com/moltis-org/moltis/pull/1089) —— 限制工具结果恢复大小**
  开启至今已近 **一周**，未收到任何评论或合并。该 PR 关乎长会话场景下的稳定性，若不及时合并，用户在大模型 Agent 循环中频繁使用工具时可能触发窗口溢出。**建议维护者尽快推进 Code Review。**

- **[高优先 / 待分类] `penso` 的三条 PR（#1104, #1105, #1106）**
  这三条 PR 在昨天集中提交，涉及 Provider 逻辑、沙箱架构等多个核心模块，影响面较广。为避免长期积压或发生合并冲突，**建议立即指定 Reviewer，并考虑将其列入下一个里程碑（Milestone）进行跟踪。**

- **[低交互 / 新 Issue] #1107, #1108, #1109**
  三项议题均为昨日新开，尚未有维护者回复或标注 label。建议项目维护者尽早给出初步回应（确认、分类或询问更多上下文），以保持社区贡献者的积极性。

---

*本日报基于 Moltis 公开仓库截至 2026-06-05 的活跃数据分析生成，所有链接均指向 GitHub 原始页面。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报　|　2026‑06‑06

> 数据统计周期：过去 24 小时（截止 2026‑06‑05 23:59 UTC）  
> 数据来源：[github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw) （当前仓库实际为 `agentscope-ai/QwenPaw`）

---

## 1. 今日速览

- 过去 24 小时共 **20 条 Issue 更新**（新开/活跃 16 条，关闭 4 条），**16 条 PR 更新**（待合并 9 条，已合并/关闭 7 条），未发布正式版本。  
- 社区活跃度维持高位：**4 个来自首次贡献者的 PR 被合并**，涵盖 LaTeX 渲染、安全加固、UI 优化等；同时用户在 Yuanbao 通道、browser_use、内存管理等方面报告了多个 Bug，项目组已快速提交修复 PR。  
- **稳定性风险集中**：Linux 子进程 `fork` 因虚拟内存耗尽失败（#4968）、Agent 死循环（#4967）、Yuanbao 通道协议兼容性缺失（#4976‑#4980）等较严重的 Bug 被报告，但相应修复已基本进入 PR 阶段。

---

## 2. 版本发布

本期无新版本发布。

---

## 3. 项目进展

今日有 **7 个 PR 被合并或关闭**，对应功能 / 修复如下：

| PR | 简述 | 类型 |
|----|------|------|
| [#4026](https://github.com/agentscope-ai/QwenPaw/pull/4026) | 安全加固：`write_file` 工具增加文件状态检测，阻止覆写非空文件 | ✨ Feature |
| [#4765](https://github.com/agentscope-ai/QwenPaw/pull/4765) | UI：安全页面 shield 图标垂直居中，调整规则列表列宽 | 🎨 Style |
| [#4766](https://github.com/agentscope-ai/QwenPaw/pull/4766) | UI：修复环境变量页面鼠标悬停时滚动条闪烁 | 🐛 Fix |
| [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) | 修复 `browser_use` CDP 超时，增加浏览器 profile 隔离（Chrome/Edge） | 🐛 Fix |
| [#4905](https://github.com/agentscope-ai/QwenPaw/pull/4905) | 浏览器控制新增 `page_x` / `page_y` 坐标点击能力 | ✨ Feature |
| [#4934](https://github.com/agentscope-ai/QwenPaw/pull/4934) | 插件：集成 OpenSandbox，Agent 可在沙箱中执行 Shell 命令 | ✨ Feature |
| [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972) | 修复 Markdown 渲染中 LaTeX 公式无法显示的问题 | 🐛 Fix |

> 前 6 个合并均来自 **社区首次贡献者**，体现项目贡献者生态良好。  
> 另外，[#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983)、[#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) 等针对 Yuanbao 通道的修复 PR 今日已提交，等待合入。

---

## 4. 社区热点

### 🔥 讨论最活跃的 Issue

| Issue | 标题 | 评论 | 热度分析 |
|-------|------|------|----------|
| [#4754](https://github.com/agentscope-ai/QwenPaw/issues/4754)（已关闭） | 打包方式（exe）及两个 Windows 版本区别 | **7** | 用户对桌面客户端打包方案高度关注，希望有官方的 PyInstaller/Tauri 指南 |
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919)（已关闭） | `browser_use` 启动失败：CDP 超时 + 浏览器闪退 | **6** | Windows 10 用户反馈最严重，最终通过切换 playwright‑cli 兜底；#4944 已修复 |
| [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770)（开放） | 左侧会话列表列顺序调整（时间列应靠左） | **5** | 多次被用户提及，已有 [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) 实现可自定义列顺序，等待合入 |
| [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967)（开放） | Agent 执行陷入死循环无法退出 | **4** | 影响核心交互流程，暂无对应修复 PR |

### 📌 其他值得关注的讨论

- [#4968](https://github.com/agentscope-ai/QwenPaw/issues/4968)（3 评论）：Linux 上的 “Cannot allocate memory” 子进程创建失败，怀疑存在虚拟内存泄漏，被标记为 Bug。  
- [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962)（3 评论）：DEEPSEEK API 的回复折叠到“思考过程”内部，需要手动展开才能看到，属于显示逻辑问题。

---

## 5. Bug 与稳定性

按严重程度排列今日（6月5日）活动中的 Bug 问题。标注是否存在关联的修复 PR。

| 严重度 | Bug | Issue | 关联 PR / 备注 |
|--------|-----|-------|----------------|
| 🔴 **严重** | 子进程 `fork` 因虚拟内存不足失败（Linux） | [#4968](https://github.com/agentscope-ai/QwenPaw/issues/4968) | 未关联 PR；作者已升级至 1.1.10 仍复现 |
| 🔴 **严重** | Agent Mission 死循环，无法退出 | [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) | 未关联 PR |
| 🟠 **高** | `loop_config.json` / `prd.json` 损坏导致整 Agent 崩溃 | [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) | 未关联 PR；建议增加异常保护 |
| 🟠 **高** | Yuanbao 通道因 proto 文件缺失无法启动 | [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976) | 无直接 PR（需 wheel 打包修复） |
| 🟠 **高** | Yuanbao `AuthBindRsp` 缺少 `connectId` 字段定义 | [#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978) | ✅ 已提交修复 [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) |
| 🟠 **高** | Yuanbao `streaming_enabled=True` 导致回复被静默丢弃 | [#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979) | ✅ 已提交修复 [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) |
| 🟡 **中** | `protobuf` 兼容性：`SerializeToString` 参数 4.x 特有 | [#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977) | 无 PR，需降低版本要求或加版本判断 |
| 🟡 **中** | DEEPSEEK 回复折叠于思考过程内（显示问题） | [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) | 无 PR |
| 🟡 **中** | Windows 下 Shell 命令调用弹出 cmd 窗口闪烁 | [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) | 无 PR（需加 `CREATE_NO_WINDOW` 标志） |
| 🟢 **低** | LaTeX 公式显示异常（已修复并关闭） | [#4959](https://github.com/agentscope-ai/QwenPaw/issues/4959) | ✅ 已合并 [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972) |
| 🟢 **低** | `browser_use` CDP 超时（已关闭） | [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | ✅ 已合并 [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) |

---

## 6. 功能请求与路线图信号

### 当前开放的功能请求

| Issue | 功能 | 状态 | 是否已有 PR |
|-------|------|------|-------------|
| [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) | 会话列表列顺序可调整 | ✅ [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) 已实现 |
| [#4974](https://github.com/agentscope-ai/QwenPaw/issues/4974) | 为每个 Agent 配置头像并在管理/列表/聊天统一显示 | 无 PR |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | 增加“会话栏”以快速切换会话 | 无 PR |
| [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963) | Cron 任务支持直接执行脚本/Shell 命令（不经过 AI） | 无 PR |
| [#4960](https://github.com/agentscope-ai/QwenPaw/issues/4960) | 局域网内手机访问桌面版控制台 | 无 PR（更偏向配置 / 文档） |
| [#4744](https://github.com/agentscope-ai/QwenPaw/issues/4744) | macOS Tauri 客户端支持 Intel 芯片 | 无 PR |
| [#2961](https://github.com/agentscope-ai/QwenPaw/issues/2961)（引用） | Skill 批量下载支持标签过滤 | ✅ [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) 已提交 |

### 路线图信号分析

- **会话与 UI 改进**（#4770、#4971、#4974）是当前社区最高频诉求，且 #4975 已将可排序列落地；
- **Cron 直接执行脚本**（#4963）代表用户希望将 CoPaw 用于纯运维自动化场景，可能推动“工具执行”与“AI 编排”的进一步解耦；
- **跨平台桌面端**（#4744）仍有一定需求缺口，尤其在非 ARM Mac 上。

---

## 7. 用户反馈摘要

从 Issue 讨论中提取的真实用户声音：

> - “我也想打包成 exe 程序使用，谢谢！”（#4754）—— 对官方 Packager 方案需求强烈，尤其希望明确 PyInstaller 与 Tauri 版本的差异。  
> - “尝试了关闭杀毒、防火墙、路由器防火墙……唯一的区别是从超时变成拒绝连接。”（#4960）—— 局域网手机访问控制台的文档和特性支持不足，用户摸索成本高。  
> - “当前仅靠名称区分多个 Agent，切换效率低、视觉上不够直观。添加头像可快速识别。”（#4974）—— 期望获得更现代化、可定制的 Agent 管理体验。  
> - “每次都要点两次才能切换会话，太麻烦了。”（#4971）—— 会话侧栏缺失是前端体验的核心痛点之一。  
> - “Three attempts all failed, finally had to fallback to npm playwright-cli.”（#4919）—— 浏览器自动化稳定性在 Windows 上表现不佳，依赖 Playwright 环境配置。  
> - “Agent 会话直接崩溃，Telegram/控制台都无法交互。”（#4970）—— JSON 文件损坏缺乏防护，属于致命稳定性问题。  
> - “希望支持直接执行脚本/命令，而不经过 AI 处理。”（#4963）—— 用户需要纯粹的自动化触发能力。  

总体来看，用户对新功能、UI 易用性、本地打包和稳定性（尤其是子进程/浏览器）最为敏感。

---

## 8. 待处理积压

以下 Issue/PR 长期开放、讨论已停止或等待维护者回应/审查：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue (Question) | [#4744](https://github.com/agentscope-ai/QwenPaw/issues/4744) | 桌面客户端 macOS Tauri 是否支持 Intel 芯片 | 2026‑05‑28 | 2026‑06‑05 | 仅 2 评论，无人给出明确答案 |
| Issue (Feature) | [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) | 左侧会话列顺序调整 | 2026‑05‑28 | 2026‑06‑05 | 已有 [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) 但未合并，需加速 review |
| Issue (Bug) | [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) | Shell 命令弹出 cmd 窗口闪烁 | 2026‑05‑31 | 2026‑06‑05 | 修复简单，但无社区或有成员响应 |
| PR (Open) | [#4822](https://github.com/agentscope-ai/QwenPaw/pull/4822) | fix(crons): 修复 share_session cron 产生空 trace | 2026‑05‑29 | 2026‑06‑05 | 已等待约 7 天，需要 reviewer 时间 |
| PR (Open) | [#4884](https://github.com/agentscope-ai/QwenPaw/pull/4884) | fix(channel): replace_channel 停止旧通道再启动新通道 | 2026‑06‑01 | 2026‑06‑05 | 等待 review |
| PR (Open) | [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) | 解耦插件加载与 Agent 启动 | 2026‑06‑02 | 2026‑06‑05 | 涉及 Desktop Pet 冻结环境，较为复杂 |

---

**分析总结**：CoPaw 项目正处于功能迭代与稳定性修复并行的密集期，社区贡献活跃（7 个 PR 被合并），但 Linux 子进程泄漏、Yuanbao 通道兼容性等严重 Bug 仍需要尽快合入修复 PR 并发布热修复版本。UI/UX 改进类需求持续增多，建议维护者及时合并 #4975、#4969 等高质量 PR，以响应社区呼声。  
*报告自动生成于 2026‑06‑06 06:00 UTC*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，请查收基于您提供的 GitHub 数据生成的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 (2026-06-06)

### 1. 今日速览

ZeroClaw 项目在 24 小时内维持了极高的开发和社区活跃度，共计 50 个 Issue 和 50 个 PR 获得更新。项目当前正处于 **架构重构与生态扩张并行的快车道**，核心工作围绕三大方向铺开：**安全层深度重构**（OIDC、可插拔安全接口）、**多通道/多 Provider 生态规模化扩张**（Schema V3 批量引入新服务）以及 **Web UI 管理能力补齐**。值得注意的是，当前有 **38 个 PR 处于待合并状态**，且多名核心贡献者（如 `singlerider`, `Audacity88`, `theonlyhennygod`, `alex-nax`）提交的代码量巨大，建议维护方规划大规模合并窗口以推进 v0.9.0 里程碑。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日虽然合并/关闭的 PR 不多（12 个），但活跃中的 PR 揭示了项目在多条主线上的巨大进展：

- **Provider 与核心架构：**
    - **Provider 生态爆发：** PR [#7260](https://github.com/zeroclaw-labs/zeroclaw/pull/7260) 一次性新增了 7 个 OpenAI 兼容的 Provider（如 GitHub Models、Morph 等），PR [#7163](https://github.com/zeroclaw-labs/zeroclaw/pull/7163) 为 Provider 新增了 `extra_body` 透传能力，PR [#7178](https://github.com/zeroclaw-labs/zeroclaw/pull/7178) 实现了按别名的模型回退机制，Provider 层的灵活性和兼容性大幅提升。
- **Web UI 功能补齐：**
    - **Dashboard 管理后台：** PR [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) 是本次迭代的“巨无霸”PR，为 MCP、Skills、Plugins 和 Providers 新增了完整的 Frontend 管理标签页。
    - **配置编辑体验：** PR [#7267](https://github.com/zeroclaw-labs/zeroclaw/pull/7267) 允许在 Web UI 中对 MCP Server 进行逐字段编辑，PR [#7235](https://github.com/zeroclaw-labs/zeroclaw/pull/7235) 新增了插件生命周期接口，极大降低了运维门槛。
- **多通道生态扩张：**
    - **SMS 通道：** PR [#7265](https://github.com/zeroclaw-labs/zeroclaw/pull/7265) 集成了 Twilio、Plivo、Telnyx、Sinch 和 Vonage 五大 SMS 通道。
    - **社交媒体/聊天通道：** PR [#7270](https://github.com/zeroclaw-labs/zeroclaw/pull/7270) 新增了 Mastodon、Rocket.Chat、Zulip 和 Lemmy 四个轮询通道。
- **可观测性重大突破：**
    - PR [#7233](https://github.com/zeroclaw-labs/zeroclaw/pull/7233) 实现了结构化的可观测性增强，填补了事件上下文稀疏、OTel 缺乏关联等关键盲区，是运维能力升级的核心提交。

### 4. 社区热点

今日讨论最为激烈的议题主要集中在工程治理与 Agent 交互控制上：

- **工程治理与流程优化：**
    - [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) **工作流、面板自动化与标签清理 RFC**（9 评论）：社区高度关注如何在不增加维护者负担的前提下，通过轻量级 PR 泳道和自动化来优化工作流。
- **输出路由与用户体验：**
    - [#6969](https://github.com/zeroclaw-labs/zeroclaw/issues/6969) **统一输出路由模型 RFC**（7 评论）：用户 `mov-xound-glitch` 提出的“控制 AI 向谁以及用什么方式发送回复”的需求引发了强烈共鸣，反映出从其他平台迁移的用户对精细控制权的强烈渴望。
- **安全与执行控制：**
    - [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) **高危险 Shell 命令确认层级 RFC**（4 评论）：社区对“允许/询问/拒绝”三级策略的讨论热度不减，这已成为 Agent 安全框架的标配诉求。

### 5. Bug 与稳定性

今日报告的 Bug 以安全性为核心，且有多项已附带修复 PR：

- **严重性高 (P1)：**
    - [#7059](https://github.com/zeroclaw-labs/zeroclaw/issues/7059) *[进行中]*：Channel Orchestrator 中的“默认 Model Provider”凭证回退机制存在设计缺陷，可能导致凭证滥用。
    - [#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) *[已阻塞]*： `allowed_tools` 仅在前端过滤但未在执行层强制拦截，这是一个严重的安全缺口。贡献者 `alex-nax` 已提交修复，但状态被阻塞，亟待维护者审阅。
    - [#6916](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) *[已接受]*： Shell/技能子进程缺乏进程级内存限制，已在生产环境造成 OOM 事故。
- **已有修复 PR 的 Bug：**
    - `PR #7281`：修复了 Shell 策略中对 heredoc 体和非路径波浪号（~）的误杀问题。
    - `PR #7123`：修复了 BlueSky 等渠道因 UTF-8 截断导致 panic 的问题，对国际化用户影响较大。
    - `PR #7254`：修复了内联 `<think>` 块污染原生工具调用输出的问题。
    - `PR #7261`：修复了配置序列化/反序列化时，嵌套数组对象中的 `#[secret]` 字段未被正确脱敏的漏洞。
    - `PR #7247`：修复了 Gateway `paired_tokens` 漂移误报的问题。

### 6. 功能请求与路线图信号

- **v0.9.0 核心信号：**
    - 从 [#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) 和 [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) 明确标记的 “Target v0.9.0” 可以看出，下个大版本的核心主题是 **安全架构升级**，目标是将安全强制层暴露为可插拔接口，并支持 OIDC 认证。
- **Multi-Agent 与互联互通：**
    - [#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218) *[已接受]*：定义了 `/.well-known/agent-card.json` 的 A2A 发现机制，为 ZeroClaw 在多人机协作网络中的互操作性奠定了基础。
- **胖核心向瘦核心演进：**
    - [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) *[已阻塞]*：提议将 Jira、GitHub 等内置集成移除，通过 Skills 进行扩展。若被接受，将是代码架构的重大转向。

### 7. 用户反馈摘要

- **痛点：**
    - *交互控制力不足：* **mov-xound-glitch**（#6969）反映从 Letta 迁移后，失去了对 AI “向谁、以何种方式”输出回复的精细控制，这是当前架构的明显短板。
    - *入门门槛改善：* 从已关闭的 #6120 和今日刚提交的修复 `PR #7240` 来看，新用户在 Provider 配置（特别是 OpenAI Codex 和多账套场景）上存在明显困惑和阻碍。
    - *终端体验差：* **shreve**（#5882）认为当前 REPL 与 Claude Code 等商业产品差距巨大（已关闭，可能已延期或放弃）。
- **期望：**
    - *深度安全与资源隔离：* 以 **alex-nax**（#6914, #6915, #6916, #6917）为代表的用户表现出了极高的安全素养，他们不仅提出问题，还直接提交了允许/拒绝列表、技能限域、进程内存限制和 Composio Action 过滤的代码。这代表了高级用户对 Agent 安全的最高期望。

### 8. 待处理积压

大量高价值工作被挂上了 `needs-maintainer-review` 或 `status:blocked` 标签，已成为项目当前最大的瓶颈：

- **安全相关阻塞项（需优先处理）：**
    - [#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914)：允许/拒绝工具执行强制检查。
    - [#6915](https://github.com/zeroclaw-labs/zeroclaw/issues/6915)：技能执行期间的临时工具权限提升。
    - [#6917](https://github.com/zeroclaw-labs/zeroclaw/issues/6917)：Composio Action 作用域过滤。
    - [#5842](https://github.com/zeroclaw-labs/zeroclaw/issues/5842)：`extra_args` 安全评估。
- **功能缺失阻塞项：**
    - [#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)：多家国内厂商的 OAuth 支持（高社区呼声）。
    - [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)：核心瘦身与外部集成迁移。
    - [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)：气隙执行模式（Unix Socket 隔离）。
    - [#5908](https://github.com/zeroclaw-labs/zeroclaw/issues/5908)：Debian 容器镜像的 CI/CD 构建与发布。
- **日常维护：**
    - [#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715)：清理主仓库中超过 200 个的陈旧分支。
    - [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)：需维护者协助审计此前因批量回滚丢失的 153 个提交（状态: 进行中）。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*