# OpenClaw 生态日报 2026-06-23

> Issues: 259 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-23 02:54 UTC

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

好的，这是根据 OpenClaw 项目 2026-06-23 的 GitHub 数据生成的日报。

---

## OpenClaw 项目动态日报 | 2026-06-23

### 1. 今日速览

OpenClaw 在 2026-06-23 展现出极高的社区活跃度和开发强度，共计更新 259 个 Issue 和 500 个 PR。项目发布了 Beta 版本 `v2026.6.10-beta.2`，重点引入了对话自动加速模式（Fast Mode）并改进了模型路由的可靠性。然而，社区焦点仍集中在平台稳定性上，P0 级 **Gateway 内存泄漏**（RSS 暴涨至 15.5GB）以及多个导致会话状态丢失和消息阻断的回归 Bug 正在严重消耗用户信任。尽管 24 小时内合并/关闭了 60 个 PR，但高达 **440 个 PR 的待合并积压**与大量等待决策的严重 Bug 表明，维护团队在产出与品控之间正面临严峻平衡挑战。

### 2. 版本发布

项目于今日发布了 **`v2026.6.10-beta.2`**。
- **主要更新内容**：
    - **对话自动加速（Automatic Fast Mode）**：在简短对话轮次中自动启用快速模式，当进入长对话时回退并恢复正常行为，优化了对话体验。感谢社区贡献者 @alexph-dev 和 @vincentkoc。
    - **更可靠的模型路由**：改进了模型路由的稳定性（特别是针对 Zai 供应商层面）。
- **破坏性变更与迁移指南**：暂无。建议用户升级体验 Fast Mode 并报告兼容性问题。

### 3. 项目进展

过去 24 小时内，项目合并/关闭了 60 个 PR 和 87 个 Issue，主要进展如下：
- **基础设施与自动化**：
    - [PR #68936] 合并了基于 Claude Agent SDK 的 **PR 自动修复 Pipeline** 及 Windows 守护进程，大幅提升了 CI/CD 能力和自动化运维水平。
- **通道与连接修复**：
    - [Issue #93375] 修复了 Telegram 轮询在遇到网络超时后进入**静默崩溃循环**、健康监控无法恢复的问题。
    - [Issue #92141] 修复了 WebChat/Codex 会话中已连接的 Windows 节点未暴露 `host=node exec` 工具的问题。
- **数据安全与存储**：
    - [Issue #78396] 修复了 `--force-reset-cross-signing` 触发二次引导导致 **E2EE 加密状态彻底破坏**的严重 Bug。
    - [Issue #92302] 修复了 Windows 环境下 QMD 内存后端因 **CommonJS 路径拼接导致路径分隔符丢失**的兼容性问题。
- **核心引擎**：
    - [Issue #95248] 修复了诊断子系统 `release_lane` 在面对活跃 Worker 时无效（no-op）的问题，后者导致 Telegram 入站事件卡死。

### 4. 社区热点

- **🔥 核心重构讨论：SQLite 持久化访问器 Seam** ([Issue #88838](openclaw/openclaw Issue #88838)) — 34条评论，P1/钻石龙虾。社区深度参与了核心会话/转录 SQLite 迁移路径的讨论，这是目前最具技术深度的线程。
- **🔥 回归焦虑：Codex 服务器轮次完成停滞** ([Issue #88312](openclaw/openclaw Issue #88312)) — 17条评论，P1/铂金隐士。用户强烈反映 `2026.5.27` 版本引入的回归问题，导致多工具 Agent 轮次无法完成，严重影响 ChatGPT Plus 用户体验。
- **🔥 平台级危机：Gateway 内存泄漏** ([Issue #91588](openclaw/openclaw Issue #91588)) — 13条评论，P0/铂金隐士。RSS 从 350MB 持续增长到 15.5GB 直至被 OOM Killer 杀死，是当前最受关注的稳定性灾难。
- **🔥 架构诉求：PostgreSQL 替代 SQLite** ([Issue #90370](openclaw/openclaw Issue #90370)) — 11条评论，P3。围绕“资源浪费”、“数据孤岛”和“高并发性能”进行了深度讨论，展现了运维团队的刚需。
- **🔥 生态需求：Antigravity CLI (agy) 支持** ([Issue #84527](openclaw/openclaw Issue #84527)) — 获 9 个 👍。尽管评论少，但社区呼声极高，是应对 Google 弃用 Gemini CLI 的紧急方案。

### 5. Bug 与稳定性

按严重程度排列，高优先级 Bug 如下：

- **🔴 P0 - 铂金隐士**：
    - [Issue #91588] **Gateway 内存泄漏**：无修复 PR，急需维护者介入决策和分配资源。生产环境用户风险极高。
- **🔴 P1 - 铂金隐士**：
    - [Issue #88312] Codex 轮次完成停滞（回归）。
    - [Issue #91363] 隔离 Cron 任务 LLM 请求失败（`model-call-started` 阶段卡死）。
    - [Issue #92460] 隔离 Cron 传递丢失交付渠道信息。
    - [Issue #90288] 非 Anthropic 模型（如 MiniMax/DeepSeek）输出工具调用为纯文本（造成 Agent 功能瘫痪）。
    - [Issue #94147] macOS 端 CLLocationManager 每秒重建，导致 TCC 权限疯狂请求。
    - [Issue #94251] Ollama 远程提供者流式传输未被消费，导致模型调用卡在 `started` 阶段。
    - [Issue #95612] `cli-backend` 运行 Anthropic 返回 401（同环境手工调用正常）。
- **🔴 P1 - 钻石龙虾**：
    - [Issue #86538] 会话写锁超时阻塞 Subagent 交付。
    - [Issue #92201] Anthropic 思考签名在回放时间歇性无效。
    - [Issue #95495] `2026.6.9` 版本静默迁移内存向量库目录，导致**全量重新嵌入**且无升级警告（*已有 linked PR*）。
    - [Issue #95833] **新报告**：Subagent 中止会话时无法释放 `.jsonl.lock`，导致会话永久损坏。
- **🟡 通报新 Bug**：
    - [Issue #95760] NVIDIA Build 供应商代理流中断，导致会话陷入僵尸状态。
    - [Issue #94032] `exec` 无法访问私有局域网主机（而同一用户的 GUI/LaunchAgent 成功），疑似沙箱边界问题。

### 6. 功能请求与路线图信号

- **🚀 高概率纳入下个版本**：
    - [Issue #84527] **Antigravity CLI (agy) 支持**：受 Google I/O 2026 政策驱动（Gemini CLI 已于 6月18日停服），是硬性需求，必须优先处理。
    - [Issue #90370] **PostgreSQL 内部存储支持**：架构层呼声渐高，已有团队给出详细分析，若无架构冲突，可能会纳入长期路线图。
    - [PR #69039] **MCP Apps 支持**：已有完整实现代码，处于等待审核状态，若通过将大幅扩展 Agent 工具生态。
- **🧭 路线图信号**：
    - [Issue #95724] **按源目录索引记忆**：新提案，旨在解决多 Agent 共享工作区导致的向量库重复构建问题，设计优雅。
    - [PR #69824] **ACP 通用化**：RFC 提案，提出将所有 Agent 启动统一到 ACP 运行时 Seam 的远期架构，若实施将重构核心引擎。
    - [Issue #95279] **受信任的入站装饰契约**：旨在解决 Client（如 Slack/Telegram）主动注入不可信元数据导致的协议冲突问题。

### 7. 用户反馈摘要

- **真实痛点**：
    - “升级 `2026.6.9` 后我的 1499 个文件被静默重新索引了，没有任何警告！” — [#95495]。用户对升级体验中的**强制性破坏**非常不满。
    - “如果我的模型每次都必须回退，为什么还让我选它作为 primary？” — [#90288]。用户对**非 Anthropic 模型二等公民**的待遇感到挫败。
    - “`exit code not logged, no error output`” — [#93375]。**Telegram 通道的运维黑箱**让自部署用户非常头疼。
    - “macOS 上每秒弹出 45 次权限请求” — [#94147]。**桌面端的基本可用性**受到严重质疑。
- **使用场景与期望**：
    - **运维团队**强烈要求 PostgreSQL 支持，以消除“数据孤岛”和“资源浪费”（[#90370]）。
    - 用户对 **Fast Mode** 的上线表示认可，这是改善对话延迟的实在举措。
    - 社区对 **Antigravity CLI** 的呼声极高，表明用户对**跟上外部生态变化**有很高的期待。

### 8. 待处理积压

提醒维护者关注以下长期待响应或阻塞性 Issue/PR：

- **⏳ 高风险、长期未关闭**：
    - [Issue #91588] **P0 Gateway 内存泄漏**：自 6月9日报告，已存在 14 天，至今无 `fix PR`。项目健康度最高优先级风险项。
    - [Issue #85743] **P1 `pendingFinalDelivery` 心跳重播无限循环**：存在 31 天，对孤儿会话无任何处理机制。
    - [Issue #86538] **P1 会话写锁超时**：存在 29 天，阻碍核心子代理逻辑。
- **⏳ 需求积压**：
    - [Issue #8299] **Sub-agent announce 配置开关**：自 2 月提出（存在 141 天），用户对无法自定义抑制子代理公告感到不满。
    - [Issue #78431] **Discord `statusReactions` 生命周期**：自 5 月提出（存在 48 天），文档写了但实际只实现了 Telegram，功能不一致。
    - [Issue #54794] **Telegram Inline Query**：自 3 月提出（存在 89 天），已标记为 `stale`，若不在路线图中建议官方给出明确答复。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告（2026-06-23）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态呈现出“规模扩张与质量阵痛并存”的特征。十余个活跃项目在 **多通道集成、MCP 协议、安全权限模型** 等方向上密集迭代，社区贡献热情高涨。然而，核心维护资源瓶颈导致 **PR 积压严重**（OpenClaw 440 待合并、ZeroClaw 47 待合），回归问题频发（IronClaw 主干挂起、OpenClaw Gateway 内存泄漏），用户对稳定性和体验的诉求远高于新功能。与此同时，**移动端适配、去中心化网关、直接模型接入**等新需求明显抬头，表明生态正从“功能验证”迈向“生产环境适配”阶段。

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 259 | ~500（60 合并） | v2026.6.10-beta.2 | 极高活跃，稳定性危急（P0 内存泄漏） |
| **NanoBot** | 6（3 开/3 关） | 30（14 合并） | v0.2.2（140 PR） | 优秀，响应快，信任度高 |
| **Hermes Agent** | 50（46 新/活跃） | 50（6 合并） | 无 | 良好，跨平台兼容性短板 |
| **PicoClaw** | 数个（含关键 Bug） | 19（7 合并） | 无 | 活跃，安全加固密集推进 |
| **NanoClaw** | 0 新 | 6（1 合并） | 无 | 中等偏上，渠道扩展阶段 |
| **NullClaw** | 0 | 2 开放 | 无 | 低频维护 |
| **IronClaw** | 16（13 新/3 关） | 23（8 合并） | 无 | 高活跃，但主干回归严重 |
| **LobsterAI** | 5 存量（无新增） | 6 合并 | 无 | 中等，Bug 修复长期积压 |
| **TinyClaw** | 无活动 | 无活动 | 无 | 休眠 |
| **Moltis** | 无活动 | 无活动 | 无 | 休眠 |
| **CoPaw** | 23（21 活跃） | 50（15 合并） | 无 | 极高活跃，稳定性受质疑 |
| **ZeptoClaw** | 无活动 | 无活动 | 无 | 休眠 |
| **ZeroClaw** | 多个（含新开/关闭） | 47 待合 + 3 合并 | 无 | 高活跃，合并阻塞严重 |

> *注：更新数指过去 24 小时内的新增、更新或关闭总量。*

## 3. OpenClaw 在生态中的定位

OpenClaw 是当前生态中 **规模最大、功能最全** 的参照项目，其 Issue/PR 活跃量远超其他项目（259/500），社区广度领先。但与同类相比存在显著矛盾：

- **优势**：对话自动加速（Fast Mode）、模型路由改进、CI/CD 自动化 Pipeline 等前沿特性率先落地；核心引擎覆盖 Telegram/WebChat/Codex 等多通道，功能复杂度第一。
- **技术路线差异**：与 NanoBot 的“强韧性优先”不同，OpenClaw 偏向功能快速堆叠，导致 P0 级回归（Gateway 内存泄漏 15.5GB）长期未修复；与 IronClaw 的企业级权限体系相比，OpenClaw 的权限模型仍较薄弱。
- **社区规模**：OpenClaw 的 Issue 讨论深度和评论热度（如 SQLite 迁移、PostgreSQL 呼声）均高于其他项目，但 **440 个 PR 积压** 反映维护团队边际效率已饱和，用户信任正被稳定性问题侵蚀。
- **与生态关系**：多个项目（如 LobsterAI、NanoClaw）明确兼容 OpenClaw 插件生态，表明其已成为事实上的“插件标准”之一，但架构复杂性也让后来者有机会通过轻量、稳定等差异化策略争夺用户。

## 4. 共同关注的技术方向

以下趋势在多项目中同时出现，反映生态共性需求：

| 技术方向 | 涉及项目 | 具体体现 |
|---|---|---|
| **MCP 协议支持与稳定性** | NanoBot、Hermes、CoPaw、ZeroClaw、IronClaw | MCP 重连崩溃、资源/提示逃逸、工具在 TUI 不可见、项目级 .mcp.json 支持 |
| **通信通道稳定性** | OpenClaw、Hermes、PicoClaw、NullClaw | Telegram 静默崩溃/无限循环、WhatsApp 断连、Matrix 同步游标丢失 |
| **会话持久化与状态恢复** | OpenClaw、Hermes、NanoBot、CoPaw、ZeroClaw | session 锁超时、state.db 损坏、工具循环中间状态丢失、JSONL 竞态 |
| **安全与权限精细化** | IronClaw、PicoClaw、ZeroClaw、CoPaw | per-tool 三态权限、exec 规则绕过、CSRF、自动审批策略失效 |
| **模型供应商兼容性** | OpenClaw、Hermes、CoPaw、ZeroClaw | 非 Anthropic 模型工具调用缺陷、OpenRouter 限制、智谱/自定义 OpenAI 适配失败 |
| **资源泄漏与性能** | OpenClaw、Hermes、IronClaw | Gateway OOM 、macOS fd 耗尽、并发竞争导致卡顿 |

## 5. 差异化定位分析

| 项目 | 核心功能侧重 | 目标用户 | 技术架构特色 |
|---|---|---|---|
| **OpenClaw** | 全功能通用 Agent 平台，多通道/多模型 | 个人开发者、自部署团队 | 模块化网关，SQLite 转向 PostgreSQL，Beta 版本高速迭代 |
| **NanoBot** | 开箱即用 + 高可用，WebUI 体验优先 | 非技术用户、小团队 | Gateway 生命周期优化，对话分片存储，MCP 安全逃逸快速修复 |
| **Hermes Agent** | 多平台深度集成（Telegram/Discord） + 计算机操控 | 重度社交用户、渗透测试 | 记忆分层，reasoning effort 临时覆盖，原生 Google/Vertex AI 诉求强烈 |
| **PicoClaw** | 安全加固 + 边缘端扩展（ADB、去中心化网关） | 安全敏感用户、IoT 开发者 | 轻量 Go 实现，SimpleX/Tox 网关呼声高，exec 沙箱 |
| **NanoClaw** | 轻量集成 + 审批工作流 | 团队自动化、运维人员 | IMAP/SMTP 邮件集成，reject-with-reason 机制，Telegram 集成刚落地 |
| **NullClaw** | 极简 Matrix 机器人 | Matrix 重度用户 | 单一通道，持久化仍为内存级别 |
| **IronClaw** | 企业级权限与自动化（暂停/恢复/删除） | 企业团队、平台运维 | 并发 Turn 执行、DB 驱动 Auto-approve、Reborn 性能专项 |
| **LobsterAI** | Cowork Composer 计划模式 + OpenClaw 生态兼容 | 协同办公用户 | Plan Mode 独立交互块，NIM 插件兼容修复 |
| **CoPaw** | 移动端适配 + 测试先行 | 移动办公、质量导向团队 | 7 个移动适配 PR，~171 个新增测试用例，Qwen 生态绑定 |
| **ZeroClaw** | 极致安全与 Wasm 原生插件 | 安全架构师、高信任需求场景 | Wasm 优先运行时，硬件签名/SLSA 溯源，插件系统 RFC |

## 6. 社区热度与成熟度

生态项目可大致分为三层：

### 快速迭代层（日 PR 更新 > 20，Issues 活跃 > 15）
- **OpenClaw、Hermes、IronClaw、CoPaw、ZeroClaw** 以及今日发布正式版本的 **NanoBot**
- **特征**：功能与修复双线推进，社区讨论深度高，但均面临不同程度的 **合并瓶颈或回归风险**（OpenClaw 积压 440 PR，IronClaw 主干挂起，ZeroClaw 阻塞 47 PR）。NanoBot 依托密集发布（v0.2.2）和 3 天闭环修复在稳定性上脱颖而出。

### 质量巩固层（日 PR 5–20，侧重修复与整合）
- **PicoClaw、LobsterAI、NanoClaw**
- **特征**：开发节奏相对稳健，安全/兼容修复占主导，功能新增以增量方式引入。PicoClaw 开始涉足 Android ADB 等新领域，LobsterAI 专注 Cowork 体验。社区评论深度较浅，但 Bug 反馈质量较高。

### 维护/休眠层（日 PR < 5 或无活动）
- **NullClaw、TinyClaw、Moltis、ZeptoClaw**
- **特征**：项目或处于低频维护状态，或已事实停滞。NullClaw 仅有一个核心 PR 在审，其余无明显演进，可视为技术备选或特定场景专用（如 Matrix 通道）。

## 7. 值得关注的趋势信号

从各项目用户反馈和 PR 方向中，可提炼以下对 AI 智能体开发者具有参考价值的行业信号：

### 🔐 安全与隐私从“附加”走向“核心架构”
- PicoClaw 用户要求 SimpleX/Tox 去中心化网关；ZeroClaw 提出硬件 PGP 签名与 Wasm 沙箱插件；IronClaw 落地 per-tool 三态权限。**安全不再只是合规选项，而是差异化竞争力的关键。**

### 📱 移动端成为下一个必争战场
- CoPaw 一次性提交 7 个移动适配 PR，NanoBot 收到 PWA 支持请求，PicoClaw 新增 ADB 远程操控。**用户期望在手机端获得与桌面一致的控制体验。**

### 🧠 Agent 记忆与自我进化为长期壁垒
- Hermes 的记忆核心/扩展分层、IronClaw 的 Skill Extraction 机制（从交互中蒸馏技能）、CoPaw 的 recall-aware 记忆整合，表明 **记忆系统正从简单的向量搜索向主动学习演进**，将成为 Agent 智能度的分水岭。

### 🧩 MCP 协议加速成为标准接口，但碎片化初现
- 至少 5 个项目在 MCP 实现上出现重复 Bug（重连崩溃、安全逃逸、可见性不一致），同时 ZeroClaw 和 Hermes 开始支持项目级 `.mcp.json`。**社区急需一套共享的 MCP 实现规范或基础库，以避免重复造轮。**

### ⚡ 性能与 ROI 成为用户决断依据
- OpenClaw 的 Gateway OOM、IronClaw 的 Reborn 回归、Hermes 的 fd 泄漏、CoPaw 的进程冻结——用户对“功能丰富但吃资源”的容忍度正在下降。IronClaw 专门设立“性能专项周”，**感知性能优化已成为优先级最高的路线图投入。**

### 🔗 直接模型接入诉求挑战“中间商模式”
- Hermes 用户强烈要求原生 Google/Vertex AI 支持（避开 OpenRouter），CoPaw 用户因自定义 OpenAI 兼容失败而受阻，ZeroClaw 用户因 Kimi Code 端点回归而停摆。**项目方需重新评估“供应商抽象层”的可靠性 vs 添加中间依赖的成本**，避免因第三方瓶颈影响核心体验。

---

*本报告数据来源于各项目 2026-06-23 社区动态日报，部分数字为近似值，以各项目 GitHub 原始数据为准。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot 项目动态日报 | 2026-06-23

---

### 1. 今日速览

NanoBot 于今日发布集 140 个 PR 于一体的 **v0.2.2** 版本，项目正式进入以“**Durability（强韧高可用）**”为核心诉求的质变冲刺阶段。过去 24 小时内，项目保持极高活跃度：共 **6 个 Issue** 更新（3 开 3 关）、**30 个 PR** 更新（14 个已关闭/合并）。开发焦点全面转向 **WebUI 交互稳定性**、**Gateway 生命周期健壮性**以及 **MCP 协议层安全与崩溃修复**。核心维护者 `Re-bin` 大额投入在前端体验修复，社区贡献者 `michaelxer` 则密集清理 MCP 遗留问题。**项目健康度评级：优秀。响应速度快、发布节奏紧、社区信任度高。**

---

### 2. 版本发布

#### v0.2.2
- **发布链接**: [Release v0.2.2](https://github.com/HKUDS/nanobot/releases/tag/v0.2.2) | 对应 PR: [#4445](https://github.com/HKUDS/nanobot/pull/4445) / [#4461](https://github.com/HKUDS/nanobot/pull/4461)
- **规模**: 本次迭代合并了 **140 个 PR**，迎来了 **21 位新贡献者**。
- **核心主题**: **Agent 强韧性（Durability）**
- **主要更新**:
  - **WebUI**: 对话历史改为按段分片存储，不再依赖单个脆弱文件，大幅降低文件损坏风险；Fork 分叉对话能在历史刷新后正确保留已渲染的助手回复；修复发送后布局错位及流式跟随体验（PR #4453, #4455, #4451）。
  - **Gateway**: 彻底解决前后台网关关闭时的`SIGINT`/`SIGTERM` 竞争问题，分裂 `--enable`（控制自启动）与 `--start`（控制立即拉起）语义（PR #4454, #4456, #4447）。
  - **通用修复**: 修复 Cron Session 绑定导致心跳任务无内容也强制发消息的问题（PR #4412），解决`asyncio` on Python 3.11 兼容问题。
- **破坏性变更 (Breaking Changes)**: 
  - 未发现大规模 Breaking Changes。但后台 Gateway 的 lauchd 命令语义已变更（`--enable` 不再等于 `--start`），使用后台守护进程的用户建议关注 PR #4447 的文档细节。
  - Cron Session 行为变更：绑定后的 Cron 会经过 `evaluate_response` 门控，纯例行消息不再外发（修复 #4410），若用户依赖旧版“必须发送”行为，需调整配置。

---

### 3. 项目进展

#### 🚢 已合并/关闭的里程碑级 PR

| PR | 作者 | 描述 | 影响模块 |
|---|---|---|---|
| [#4454](https://github.com/HKUDS/nanobot/pull/4454) | Re-bin | 修复 Gateway 前台退出时信号处理，捆绑 WebUI Fork 回复丢失修复 | Gateway/WebUI |
| [#4455](https://github.com/HKUDS/nanobot/pull/4455) | Re-bin | WebUI 历史刷新时保留已渲染的 Fork 回复 | WebUI |
| [#4453](https://github.com/HKUDS/nanobot/pull/4453) | Re-bin | 改进发送后滚动跟随逻辑，区分用户主动滚动与自动滚动 | WebUI |
| [#4451](https://github.com/HKUDS/nanobot/pull/4451) | Re-bin | 修复发送后消息区域 FLEX 下沉问题，保持顶部对齐 | WebUI |
| [#4456](https://github.com/HKUDS/nanobot/pull/4456) | Re-bin | 彻底修复 Websocket Channel Stop 时 `CancelledError` 捕获失败 | Gateway |
| [#4412](https://github.com/HKUDS/nanobot/pull/4412) | HaisamAbbas | 修复 Cron 会话绑定后无操作也发消息的回弹 | Agent/Loop |
| [#4445](https://github.com/HKUDS/nanobot/pull/4445) | Re-bin | 版本升级、依赖清理、Release 准备 | 工程 |
| [#4461](https://github.com/HKUDS/nanobot/pull/4461) | Re-bin | 添加 v0.2.2 发布新闻到 README | 工程/文档 |

**总结**: 项目过去 24 小时的主要推进方向是“**扫尾与加固**”。WebUI 完成了 4 个重要前端体验修复，Gateway 完成了并发安全重写，MCP 体系完成了 3 个关键稳定性修复。v0.2.2 的发布标志着这轮加固期的成果落地。

---

### 4. 社区热点

#### 🔥 讨论最活跃 Issue
- **#1461** [Unified daemon gateway semantic layer](https://github.com/HKUDS/nanobot/issues/1461) (4 条评论)
  - **分析**: 该项目请求已存在 3 个月，用户要求 Gateway 能作为一个标准的后台守护进程运行，具备`restart/status/logs`统一管理能力。虽然今日被关闭（可能被架构吸收），但其讨论直接催生了 PR #4447 对后台生命周期的大幅优化。
  - **社区情绪**: 高级用户对工程易用性有极高期望，要求从“启动器”进化到“系统服务”。

#### ⚡ 最快响应闭环
- **#4410** -> **#4412**
  - 用户 `KennethYCK` 于 6 月 19 日报 Bug（升级后 Cron 强制发消息），6 月 23 日修复 PR #4412 合并。
  - **分析**: 这是最理想的开源互动模型。用户精准指出了 `agent/loop.py` 的嫌疑行，贡献者 `HaisamAbbas` 迅速提交了针对性的 `evaluate_response` 门控方案。**此案例是本日项目健康度的最强证明。**

#### 💡 新兴需求趋势
- **#4413** [Telegram Bot API 10.1 rich messages](https://github.com/HKUDS/nanobot/issues/4413)
  - 社区要求紧跟上游 Telegram Bot API 官方富文本特性，用户不再满足于基础收发。

---

### 5. Bug 与稳定性

#### 🔴 严重 (Critical)
| ID | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#4443](https://github.com/HKUDS/nanobot/pull/4443) | 流式 `tool_use` ID 重复导致会话永久 400 | 当 API 流式响应损坏时，重复 ID 写入历史，**所有后续消息均失败** | 已有 Fix PR |
| [#4441](https://github.com/HKUDS/nanobot/pull/4441) | MCP 重连时 `RuntimeError` 崩溃 | MCP Server 断线重连失败时，`streamable_http` Generator 在错误 Task 中退出，**导致网关 Crash** | 已有 Fix PR |

#### 🟡 较高 (High)
| ID | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#4433](https://github.com/HKUDS/nanobot/pull/4433) | Pairing Store Sender ID 类型未归一化 | 可能**静默拒绝**已授权用户的发送请求 | 已有 Fix PR |
| [#4436 / #4452](https://github.com/HKUDS/nanobot/pull/4436) | `enabledTools` 白名单未作用到 Resources/Prompts | 即使配置了拒绝，MCP 的资源与提示仍可被调用，**存在安全逃逸** | 两个 Fix PR 竞争合并中 |

#### 🟢 中低 (Medium)
| ID | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#4397](https://github.com/HKUDS/nanobot/pull/4397) | 工具链执行期间用户消息被 LLM 忽略 | LLM 在调用工具链时可能无视用户中途打断的消息 | Open，待 Review |
| [#4410](https://github.com/HKUDS/nanobot/issues/4410) | 升级 v0.1.5 后 Cron 强制外发消息 | 本无实际操作的定时任务，会强行发送 LLM 响应给用户 | ✅ **已修复** (PR #4412) |

---

### 6. 功能请求与路线图信号

根据今日提交的 Feature Request 与关联 PR，以下为明显的产品方向信号：

| 信号 | 来源 | 推测优先级 |
|---|---|---|
| **移动端体验**: PWA 支持 [#4457](https://github.com/HKUDS/nanobot/issues/4457) + 已有关联 PR [#4458](https://github.com/HKUDS/nanobot/pull/4458) | WebUI 用户 | **高** - WebUI 深度使用后，移动化是自然需求 |
| **Agent 记忆升级**: `search_history` 只读工具 [#4439](https://github.com/HKUDS/nanobot/pull/4439) | 核心 Agent | **高** - 增强模型上下文能力的基石功能 |
| **企业协作**: Mattermost 通道 [#4459](https://github.com/HKUDS/nanobot/pull/4459) | 社区贡献 | **中** - 扩展 Slack 之外的垂直市场 |
| **新平台变现**: Kimi 付费套餐集成 [#4463](https://github.com/HKUDS/nanobot/issues/4463) | 用户需求 | **中** - 与官方合作伙伴定位吻合，但需与 Kimi 确认对接方案 |
| **降低门槛**: 用户引导向导改版 [#4376](https://github.com/HKUDS/nanobot/issues/4376) | 新用户痛点 | **高** - 1个👍 + 多位贡献者讨论，是阻挡用户增长的关键点 |

---

### 7. 用户反馈摘要

收集自今日活跃 Issues 中的真实用户评论：

- **痛点 1: 升级恐惧症** (#4410)
  > “In old version... it wont message to me. after upgrade... i found out it will send the message.”
  > 用户对“升级后出现意料之外行为”极度敏感。这是开源软件升级的经典心理防线。好在项目方 3 天内闭环修复，值得信赖。

- **痛点 2: 上手门槛高** (#4376)
  > “Now, `nanobot onboard --wizard` assumes you know many technical details to complete the initialization configuration of nanobot, which is not user-friendly for new or non-technical users.”
  > 非技术用户明确指出 Wizard 目前需要太多技术性前置知识。**降低门槛** 仍是 NanoBot 吸收增量用户的首要挑战。

- **使用场景 3: 高级用户追求平台原生能力** (#4413, #1461)
  > 用户要求 Telegram 原生富文本、要求 Gateway 后台化管理。这说明项目的核心用户群体已经开始将 NanoBot 视为严肃的生产力工具，而非简单的玩具，他们对外围生态和系统集成提出了更高要求。

---

### 8. 待处理积压

以下为值得核心维护者关注的“历史遗留”或“竞争性”条目：

1. **PR #4397 - 用户中断工作流修复** (创建于 2026-06-18)
   - 该 PR 旨在插入“用户打断”HINT 消息以中断 LLM 工具链调用，已 Open 6 天，在当前 v0.2.2 极度关注稳定性的背景下，可能因改动涉及 Agent 核心循环而需更谨慎的 Review。

2. **Issue #4413 - Telegram 富消息** (创建于 2026-06-19)
   - 已 Open 4 天，但无明确开发者响应。鉴于 Telegram 是 NanoBot 主流平台之一，且上游 Bot API 一直在演进，建议项目维护者在下一版本路线（v0.2.3 或 v0.3.0）中明确优先级。

3. **Conflicting PRs (`enabledTools` 修复): #4436 vs #4452**
   - 两个 PR 解决的是同一个 MCP 配置安全逃逸问题。#4436 由 `michaelxer` 提交更早，#4452 由 `yu-xin-c` 补充提交。该重叠虽正常，但应尽快确定方案或进行组合，避免社区贡献者重复劳动和分支腐烂。

---

***分析师总结：** 今日数据表明 NanoBot 已成功挺过一个重要的“功能泡沫期”，v0.2.2 是其走向工程成熟的收网之作。若能在下一阶段快速跟进 PWA 移动化、降低 Wizard 入门门槛，并解决 Telegram 富消息的社区呼声，项目的用户增长曲线有望迎来新一轮加速。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent 项目动态日报  
**日期：2026-06-23**  
**数据来源 GitHub**: [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

### 1. 今日速览

Hermes Agent 在过去 24 小时内维持极高活跃度，共更新 **50 条 Issue**（新开/活跃 46，关闭 4）和 **50 条 Pull Request**（待合并 44，合并/关闭 6）。社区围绕原生 Google/Vertex AI 提供商、macOS Intel 兼容性、Telegram 流式消息重复循环等话题讨论热烈。多个 P1/P2 级 Bug 被报告，部分已附带修复 PR；与此同时，数个增强功能 PR（如记忆层级、项目级 MCP 配置、推理 effort 覆盖）已提交，表明项目在 **稳定性修复** 与 **功能丰富** 双线快速推进。总体健康度良好，但跨平台兼容性与核心状态持久化仍是当前主要短板。

---

### 2. 版本发布  
*暂无新版本发布。*

---

### 3. 项目进展

今日 **合并/关闭 6 个 PR**，对应以下 issue 的修复或功能已落地主干：

- **Telegram 被动历史模式（Passive History Mode）**：issue [#27912](https://github.com/NousResearch/hermes-agent/issues/27912) 关闭，标记 `implemented-on-main`。用户现在可让 Hermes 在 Telegram 群组中仅对唤醒词响应，而不干预普通聊天。
- **Telegram 富文本表格渲染修复**：issue [#45323](https://github.com/NousResearch/hermes-agent/issues/45323) 关闭，修复了流式消息中 pipe table 被错误转换为 bullet list 的问题。
- **Linux `list_windows` 空返回修复**：issue [#51033](https://github.com/NousResearch/hermes-agent/issues/51033) 关闭，解决了 Ubuntu/XFCE 环境下即使有可见窗口也返回 0 的问题。
- 其他合并的 PR 涉及配置布尔值强制转换、schema_version 空值保护等细节改进。

**社区新提交的重要 PR（OPEN 状态）**：

| PR 链接 | 类型 | 关键内容 |
|---------|------|----------|
| [#51153](https://github.com/NousResearch/hermes-agent/pull/51153) | 修复 | 修复 Discord 用户消息被调度两次（对应 issue #51057） |
| [#51088](https://github.com/NousResearch/hermes-agent/pull/51088) | 修复 | 会话持久化增强：工具循环中途与压缩后状态得以保留 |
| [#51133](https://github.com/NousResearch/hermes-agent/pull/51133) | 修复 | Honcho 内存提供者在依赖缺失时报不可用，而非静默失败 |
| [#51152](https://github.com/NousResearch/hermes-agent/pull/51152) | 功能 | 记忆核心/扩展分层：`[core]` 前缀条目标常驻 system prompt，其余按需搜索 |
| [#51158](https://github.com/NousResearch/hermes-agent/pull/51158) | 功能 | 新增 `reasoning <level> --session` 临时覆盖 reasoning effort |
| [#51135](https://github.com/NousResearch/hermes-agent/pull/51135) | 功能 | 支持加载项目本地 `.mcp.json` 中的 MCP 服务器定义 |
| [#51137](https://github.com/NousResearch/hermes-agent/pull/51137) | 修复 | 补齐 `computer_use` 中 `launch_app`/`list_apps` 动作封装 |
| [#51157](https://github.com/NousResearch/hermes-agent/pull/51157) | 修复 | 修复 `vision_temperature` 被错误传入 gpt-5.5 系列导致报错 |

整体上项目在 **消息平台稳定性**、**会话状态可靠性**、**内存与推理控制**、**MCP 生态整合** 四个方向均取得了明确进展。

---

### 4. 社区热点

当日讨论最活跃、反响最多的课题：

1. **原生 Google / Vertex AI Provider 请求**  
   [#12639](https://github.com/NousResearch/hermes-agent/issues/12639)  
   💬 11 评论 · 👍 10  
   **诉求**：用户因 OpenRouter 频繁返回 HTTP 402 及速率限制，无法稳定使用 `google/gemini-3.1-pro-preview` 等模型，强烈要求直接通过 Google / Vertex AI API 调用。此需求已持续两个月，热度极高，反映出社区对 **避开中间商、直接接入顶尖模型** 的迫切愿望。

2. **macOS DMG arm64-only 导致 Intel Mac 不可用**  
   [#37505](https://github.com/NousResearch/hermes-agent/issues/37505)  
   💬 7 评论 · 👍 1  
   **背景**：官方 DMG 仅含 arm64 二进制，Intel Mac 启动即报 `Bad CPU type`。大量存量 Intel Mac 用户被排除在桌面体验之外。

3. **Telegram 流式消息无限嵌套回复循环**  
   [#48648](https://github.com/NousResearch/hermes-agent/issues/48648)  
   💬 4 评论 · 👍 1  
   **影响**：消息超过 4096 字符限制后，网关进入无限循环反复发送同一内容，造成群组信息轰炸。此 Bug 属于使用体验上的严重问题。

4. **macOS 文件描述符限制导致网关崩溃**  
   [#30230](https://github.com/NousResearch/hermes-agent/issues/30230)  
   💬 4 评论  
   macOS 默认 `maxfiles=256`，多个 profile + MCP server 即可轻松突破，导致 `Too many open files`。该问题与 #31599、#30636 共同构成了 macOS 稳定性的主要威胁。

5. **Discord `/model` 命令阻塞事件循环 120-150s**  
   [#41289](https://github.com/NousResearch/hermes-agent/issues/41289)  
   💬 2 评论  
   同步 HTTP 调用导致 Discord 3 秒超时限制被打破，应用报错且 agent 启动延迟。

此外，[#37566](https://github.com/NousResearch/hermes-agent/issues/37566)（字体选择器，👍 4）、[#50765](https://github.com/NousResearch/hermes-agent/issues/50765)（Windows ACP 挂起）等也获得了较高关注。

---

### 5. Bug 与稳定性

当日报告的 Bug 按严重程度排列，并标注是否有修复 PR（已提交/合并）。

#### P1（严重）

| Issue | 问题描述 | 已有 Fix PR |
|-------|---------|------------|
| [#30636](https://github.com/NousResearch/hermes-agent/issues/30636) | 高负载下 SIGTERM 导致 `state.db` 损坏（单用户 48h 内损坏 3 次），对话历史丢失 | 无 |
| [#31599](https://github.com/NousResearch/hermes-agent/issues/31599) | Telegram 适配器通过 HTTP 代理后 httpx 连接泄漏，2 天后 fd 耗尽 | 无 |
| [#24100](https://github.com/NousResearch/hermes-agent/issues/24100) | Discord 命令审批提示路由到错误线程（环境变量 session key 泄露） | 无 |
| [#41289](https://github.com/NousResearch/hermes-agent/issues/41289) | Discord `/model` 命令同步调用阻塞事件循环 120-150s，导致超时 | 无 |
| [#51057](https://github.com/NousResearch/hermes-agent/issues/51057) | Discord 单条用户消息被调度两次，产生重复 agent 响应 | [#51153](https://github.com/NousResearch/hermes-agent/pull/51153) 🟢 |

#### P2（较高）

| Issue | 问题描述 | 已有 Fix PR |
|-------|---------|------------|
| [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) | macOS fd 软限制 256 导致网关打开过多文件崩溃 | 无 |
| [#48648](https://github.com/NousResearch/hermes-agent/issues/48648) | Telegram 流式消息 4096 溢出后无限嵌套回复循环 | 无（但相关机制由其他 PR 覆盖） |
| [#50765](https://github.com/NousResearch/hermes-agent/issues/50765) | 0.17.0 回归：Windows ACP `session/prompt` 在 conversation turn 后挂起 | 无 |
| [#51089](https://github.com/NousResearch/hermes-agent/issues/51089) | 会话恢复丢失工具循环中间状态或压缩后状态 | [#51088](https://github.com/NousResearch/hermes-agent/pull/51088) 🟢 |
| [#51155](https://github.com/NousResearch/hermes-agent/issues/51155) | 个性设置切换后不生效，且 `config.yaml` 被错误覆写 | 无 |
| [#51141](https://github.com/NousResearch/hermes-agent/issues/51141) | `write_file` 秘密清理过于激进，破坏 `os.getenv("SECRET")` 等有效代码 | 无 |
| [#50547](https://github.com/NousResearch/hermes-agent/issues/50547) | Kanban 插件使用浏览器原生 `confirm/alert`，未使用 in-app 对话框 | 无 |
| [#51136](https://github.com/NousResearch/hermes-agent/issues/51136) | 官方 Docker 镜像中禁用懒安装，导致 Firecrawl 等可选依赖无法使用 | 无 |

#### P3（一般）

- [#50755](https://github.com/NousResearch/hermes-agent/issues/50755) Photon iMessage 在 secret 轮换后发送失败  
- [#44183](https://github.com/NousResearch/hermes-agent/issues/44183) Desktop 睡眠唤醒后 WS 连接断开，重连窗口过短  
- [#49289](https://github.com/NousResearch/hermes-agent/issues/49289) 删除 profile 后图标仍残留在 Desktop 底部栏  
- [#51099](https://github.com/NousResearch/hermes-agent/issues/51099) Honcho 内存提供者在 `honcho-ai` 未安装时仍错误激活  
- [#51139](https://github.com/NousResearch/hermes-agent/issues/51139) `computer_use` 缺少 `page/hotkey/move_cursor` 等底层 wrapper  
  （已有 PR [#51137](https://github.com/NousResearch/hermes-agent/pull/51137) 🟢 初步补全部分动作）

**小结**：macOS 平台（fd 限制、DMG 架构、Sleep/Wake 断连）仍是稳定性薄弱环节，P1 级 issue 集中在 Discord/Telegram 网关核心路径；多日未修复的 state.db 损坏问题亟需维护组介入。

---

### 6. 功能请求与路线图信号

当日收到的特征请求及已提交的 PR 反映了项目演进方向：

| 功能请求 | 链接 | 对应 PR / 状态 | 路线图信号 |
|---------|------|---------------|-----------|
| 原生 Google/Vertex AI Provider | [#12639](https://github.com/NousResearch/hermes-agent/issues/12639) | 无 PR | 打破 OpenRouter 单一依赖，用户经济压力突出 |
| Hermes Desktop 字体选择器 | [#37566](https://github.com/NousResearch/hermes-agent/issues/37566) | 无 PR | 桌面自定义需求上升 |
| OIDC 登录支持 WebAuthn/Passkey | [#42448](https://github.com/NousResearch/hermes-agent/issues/42448) | 无 PR | 企业级身份验证需求 |
| 加载项目 `.mcp.json` | [#51069](https://github.com/NousResearch/hermes-agent/issues/51069) | PR [#51135](https://github.com/NousResearch/hermes-agent/pull/51135) 🟢 | MCP 配置复用与生态整合 |
| GLM-5 推理控制支持 | [#50696](https://github.com/NousResearch/hermes-agent/issues/50696) | 无 PR | 扩展推理模型兼容性 |
| Telegram Bot 命令 i18n | [#51046](https://github.com/NousResearch/hermes-agent/issues/51046) | 无 PR | 国际化诉求 |
| `computer_use` 完整动作封装 | [#51139](https://github.com/NousResearch/hermes-agent/issues/51139) | PR [#51137](https://github.com/NousResearch/hermes-agent/pull/51137) 🟢 | Windows/Linux 桌面操控能力深化 |
| 会话级 reasoning effort 覆盖 | — | PR [#51158](https://github.com/NousResearch/hermes-agent/pull/51158) 🟢 | 推理灵活控制 |
| 记忆核心/扩展分层 | — | PR [#51152](https://github.com/NousResearch/hermes-agent/pull/51152) 🟢 | 降低 system prompt 长度，优化成本 |
| SSH IdentitiesOnly 支持 | — | PR [#51145](https://github.com/NousResearch/hermes-agent/pull/51145) 🟢 | SSH 终端后端增强 |

综合来看，下一版本可能纳入的特性包括：**MCP 项目级配置**、**记忆分层**、**推理 effort 临时覆盖**、**Codex 图像编辑**、以及 **computer_use 跨平台动作扩展**。用户对 **原生 Google/Vertex AI** 的高呼声可能推动该特性的优先级提升。

---

### 7. 用户反馈摘要

从 Issue 评论及描述中提炼的真实用户声音：

- **OpenRouter 成本与速率限制**（#12639）：*“I frequently encounter HTTP 402 and API Rate Limits from OpenRouter… Hermes tries to charge a markup”* — 用户对被迫接受中间商加价和受限表示强烈不满，要求直连模型 API。
- **Intel Mac 被排除**（#37505）：*“On Intel Macs the app cannot launch and fails with `Bad CPU type in executable`”* — 用户认为官方应提供 universal binary。
- **Telegram 消息无限循环**（#48648）：*“the gateway enters an infinite nested reply loop, sending the same content over and over”* — 严重影响群组体验。
- **macOS 限制导致崩溃**（#30230）：用户贴出 `trade-paper gateway: 286 fds` 等数据，指出 256 软限制完全不够，建议自动提高或内置警告。
- **state.db 损坏**（#30636）：*“state.db corrupted three times over a 48h window”* — 用户对数据可靠性深感疑虑。
- **Windows ACP 在 0.17.0 回归**（#50765）：*“0.16.0 works”* — 用户明确指出是 regression，且现象清晰。
- **个性设置异常**（#51155）：*“The personality chosen at start also persists inside the config.yaml regardless”* — 用户预期会话级覆盖，实际却全局写入。
- **`write_file` 误伤**（#51141）：*“makes it impossible to write API-client scripts”* — 安全机制过度，妨碍正常使用。
- **希望复用项目已有 MCP 配置**（#51069）：*“Hermes currently only reads MCP servers from its own config file”* → 用户希望避免重复配置，已有 PR 解决。

总体用户态度：**积极贡献代码的同时，对稳定性、跨平台、供应商锁定问题表达了强烈改进诉求**。暂无负面情绪，但社区越活跃，对响应速度的期待也越高。

---

### 8. 待处理积压

以下 Issue 创建时间较长或级别较高但至今无维护者回应/无修复 PR，建议团队优先排查或给出计划。

| Issue | 创建时间 | 级别 | 问题影响 | 备注 |
|-------|---------|------|---------|------|
| [#12639](https://github.com/NousResearch/hermes-agent/issues/12639) | 2026-04-19 | Feature | 直接决定用户对顶级模型的可用性，👍10 热度最高 | 已持续 2 月，无官方计划 |
| [#30636](https://github.com/NousResearch/hermes-agent/issues/30636) | 2026-05-22 | P1 | 数据损坏，影响生产使用 | 虽有人分析根因，但无 PR |
| [#31599](https://github.com/NousResearch/hermes-agent/issues/31599) | 2026-05-24 | P1 | 持续运行 2 天后必然 fd 耗尽 | 无 PR，macOS Telegram 用户关键 |
| [#24100](https://github.com/NousResearch/hermes-agent/issues/24100) | 2026-05-12 | P1 | 命令审批路由错误，安全隐患 | 无 PR，涉及 session 隔离 |
| [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) | 2026-05-22 | P2 | 多 profile 用户 macOS 必现崩溃 | 已有讨论但未进入实施 |
| [#41289](https://github.com/NousResearch/hermes-agent/issues/41289) | 2026-06-07 | P1 | Discord slash 命令不可用 | 较新但仍无 PR，核心体验受损 |

另外 [#27912](https://github.com/NousResearch/hermes-agent/issues/27912)（Telegram passive mode）虽已关闭，但在关闭前长期未分配，类似情况需留意。

**建议**：上述积压项已严重影响部分用户的日常使用（尤其是数据损坏与连接泄漏），即使无法立即修复，也建议在 `roadmap` 或 `help wanted` 标签中表明计划，以减少社区不确定性。

---

*本日报由 AI 自动分析生成，数据截止 2026-06-23T23:59UTC。如有遗漏，请以 GitHub repository 实时状态为准。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-06-23

---

## 1. 今日速览

项目今日呈现高度活跃态势。过去 24 小时内，PicoClaw 社区和核心团队共处理 **19 条** Pull Requests，其中 **7 条已被合并/关闭**，**12 条处于待合并或审查阶段**。开发节奏明显加快，修复重点集中在**安全加固**（exec 规则绕过、跨站配置攻击）和**核心连接稳定性**（WhatsApp 断连重连、消息重复）。新功能方面，Android ADB 远程操控和 Token 用量追踪两个 PR 为项目后续拓展奠定了重要基础。Issues 方面，用户不仅反馈了模型任务重复执行等阻塞性 bug，也表达了对去中心化网关注入的强烈诉求。尽管今日无正式版本发布，但从代码库的变动密度来看，项目正稳健推进至下一个迭代阶段。

---

## 2. 版本发布

**无。** 今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 主要推进了以下关键改进：

- **关键修复合入：WhatsApp 长连接稳定性修复**
  [#3162 fix(whatsapp): add reconnection and async message processing](sipeed/picoclaw PR #3162) — **已合并。** 核心改动：将消息处理移入 goroutine 避免阻塞读循环、添加 Pong 心跳响应、设置读取超时、引入指数退避自动重连机制。解决了许多 WhatsApp 用户反馈的自动断连后无法恢复的问题，是今日最重要的稳定性贡献。

- **Bug 修复合入：Spawn 双发消息修正**
  [#3155 feat(spawn): add direct_reply parameter with SkipInboundTurn support](sipeed/picoclaw PR #3155) — **已合并。** 解决了 Issue #3094 中的重复消息问题。通过 `ToolResult.SkipInboundTurn` 机制将 spawn 回调的处理路径明确拆分为两种行为模式，彻底解决了异步回调中“用户收到消息 + 主 Agent 又被触发一次”的 bug。

- **经验修复合入：类型断言安全检查**
  [#3053 fix(evolution): add ok check for LoadOrStore type assertion](sipeed/picoclaw PR #3053) — **已合并。** 修复了 `lockStoreFile` 中未做类型断言检查可能引发的 panic 风险。
  [#3091 fix(openai_compat): add ok check for native_search type assertion](sipeed/picoclaw PR #3091) — **已合并。** 避免非 bool 值传递时静默禁用本地搜索。

- **体验优化合入：Skills 搜索结果增加安装指引**
  [#3152 add installation instructions to picoclaw skills search](sipeed/picoclaw PR #3152) — **已合并。** 现在 `picoclaw skills search` 的输出结果中会直接告知用户如何安装该 skill，大幅降低了新用户的上手门槛。

- **基础设施升级：前端依赖更新**
  [#3101 build(deps-dev): bump vite from 8.0.13 to 8.0.16](sipeed/picoclaw PR #3101) / [#3105 build(deps-dev): bump eslint from 10.2.1 to 10.4.1](sipeed/picoclaw PR #3105) — 均已合并，完成了构建工具与代码检查工具的版本同步。

---

## 4. 社区热点

- **🔥 最受期待功能：SimpleX / Tox 网关注入需求**
  [#3093 [Feature] I need SimpleX or tox](sipeed/picoclaw Issue #3093)
  作者：Damian-o2 | 👍 1 | 评论 3
  这是一个**持续发酵的功能请求**。用户明确要求 PicoClaw 支持集成 SimpleX、Wire 或 Tox 等去中心化/隐私优先的通讯协议作为消息网关。社区讨论集中在隐私安全性诉求上，反映出用户群体中存在着“避免中心化平台控制”的强烈技术思想。该 Issue 自 6 月 10 日提出，已超过 13 天无人给予官方标签或答复，建议项目组研究纳入路线图讨论。

- **💥 最尖锐 Bug 反馈：常用场景下的任务重复执行**
  [#3159 [BUG] 经常重复任务](sipeed/picoclaw Issue #3159)
  作者：okAtTjC | 创建于今日
  用户给出了精确的复现路径：先问“今天的美国新闻”，再问“今天的法国新闻”，结果第二次回答会先再执行一次美国新闻任务再做法国新闻。该问题**直接击穿了对话连续性的核心体验**，可能是 context 管理或多轮工具调用调度机制存在缺陷。目前无评论、无 assignee，修复优先级被严重低估。

- **🔄 快速响应的社区协作**
  - [#3153 Volcengine Doubao Seed 工具调用泄漏](sipeed/picoclaw Issue #3153) 于昨日报告，今日已有 [#3154 fix](sipeed/picoclaw PR #3154) 被提交修复，反馈闭环效率优秀。
  - 贡献者 danmobot 在一天之内密集提交了 4 个 PR（#3157, #3158, #3161, #3160），覆盖了 Android 扩展、沙箱兼容性、安全修复，是今日单项产出最高的 contributor。

---

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 问题 | 状态 |
|---|---|---|---|
| 🔴 **关键 (Critical)** | [#3161 fix(exec)](sipeed/picoclaw PR #3161) | **命令执行安全绕过：** 用户自定义的 allow 规则（如 `^jq\b`）会彻底禁用全局 deny 模式，攻击者可通过该规则执行 `jq` 并访问进程环境变量等敏感信息。 | **有 PR 待合** |
| 🔴 **关键 (Critical)** | [#3160 fix(auth)](sipeed/picoclaw PR #3160) | **跨站配置劫持：** `POST /api/auth/setup` 接口缺少 Origin/Referer 校验，攻击者可通过 CSRF 构造首次运行配置修改密码。 | **有 PR 待合** |
| 🟠 **高 (High)** | [#3159 [BUG] 重复任务](sipeed/picoclaw Issue #3159) | **上下文串扰：** 在连续多轮、不同主题的工具调用场景下，Agent 会重复执行上一个任务，破坏对话逻辑。 | **待修复** |
| 🟠 **高 (High)** | [#3153 Leak / #3154 Fix](sipeed/picoclaw Issue #3153 / PR #3154) | **豆包模型工具调用泄漏：** Volcengine Doubao Seed 2.0 在某些长上下文中会将 `<seed:tool_call>` 原型文本直接返回给用户而不是执行函数。 | **已提交修复 PR** |
| ⚪ **中 (Medium)** | — | 沙箱文件系统 Windows 兼容性测试（[#3158](sipeed/picoclaw PR #3158)）、Web 搜索 Body Close 错误处理（[#3128](sipeed/picoclaw PR #3128)）等多项代码质量修复已提交，尚待合并。 | **多种修复待合** |

---

## 6. 功能请求与路线图信号

- **🎯 高概率纳入下个版本：**
  - **[#3156 feat: emit per-turn LLM token usage](sipeed/picoclaw PR #3156)**：在 finalized 消息中携带 input/output token 消耗，这是**付费用户成本核算的刚需功能**。如果项目有向企业级交付演进的打算，这条 PR 会是一个非常关键的信号。
  - **[#3157 feat: Android ADB remote operations tool](sipeed/picoclaw PR #3157)**：新增 Android 设备操控能力（截图、点按、输入、唤醒等）。这标志着 PicoClaw **从桌面/服务器 Agent 向移动端与 IoT 设备操控 Agent 的跨越**。即便是实验性特性，也极具天花板价值。
  - **[#3118 feat: remote Pico WebSocket mode](sipeed/picoclaw PR #3118)**：允许通过 `picoclaw agent --remote ws://...` 作为远程客户端连接，这是实现**分布式 Agent 架构**的第一步。

- **🔄 待确认优先级：**
  - **[#3093 SimpleX/Tox 网关](sipeed/picoclaw Issue #3093)**：用户呼声很高，且属于“独立基础设施”层级的需求，落地后很难被换掉，容易形成用户粘性。但目前无任何 Project Board 或 Label 标记，建议核心团队至少回应一下总体态度。

---

## 7. 用户反馈摘要

- **深度使用场景曝光**：
  通过 Bug 描述可以推测，用户在真实场景中深度依赖多工具编排（新闻聚合、跨模型调用）。`#3159` 的复现路径显示，用户以“美国新闻 → 法国新闻”这样的非幂等、跨上下文任务测试，发现了 Agent 的工作流调度缺陷。这说明用户已从单轮对话转向**复杂的多步骤 Agent 自动化**使用阶段。

- **隐性的渠道迁移需求**：
  `#3093` 对 SimpleX/Tox 的强烈需求背后，可能隐含着用户对 Telegram/WhatsApp 等平台的审查焦虑或数据隐私担忧，尤其是在不同国家的监管环境下。PicoClaw 如果能在网关层提供去中心化选项，会显著扩大其在国际隐私敏感用户群体中的采用率。

- **对模型适配能力的高期望**：
  从 `#3153` 到 `#3154` 的快速修复来看，用户对主流国产大模型（如豆包系列）的适配非常敏感。PicoClaw 对这一生态的维护和兼容性投入，是吸引国内开发者的关键竞争优势。

---

## 8. 待处理积压

| 类型 | 条目 | 存活天数 | 风险说明 |
|---|---|---|---|
| 📦 Dependabot | [#3104 shadcn 4.7.0 → 4.11.0](sipeed/picoclaw PR #3104) | 12 天 | 长期未合并，落后 3 个大版本 |
| 📦 Dependabot | [#3100 @vitejs/plugin-react](sipeed/picoclaw PR #3100) | 12 天 | 版本落后，但风险可控 |
| 📦 Dependabot | [#3103 typescript-eslint](sipeed/picoclaw PR #3103) | 12 天 | 版本落后 |
| 🛠 代码质量 | [#3131 registry type assertion ok 检查](sipeed/picoclaw PR #3131) | 8 天 | 防止工具注册时 schema 类型不正确导致 panic |
| 🛠 代码质量 | [#3128 web search Body.Close 错误忽略](sipeed/picoclaw PR #3128) | 8 天 | 代码扫描/静态检查类修复，风险低，但长期堆积不利于 CI 清洁 |
| 🧪 功能扩展 | [#3118 远程 Pico Agent 模式](sipeed/picoclaw PR #3118) | 11 天 | 无进展，大概率还在 Code Review 中 |
| 💡 功能请求 | [#3093 SimpleX / Tox 网关](sipeed/picoclaw Issue #3093) | 13 天 | 无官方回应，未打标签 |
| 🐛 Bug | [#3159 重复任务](sipeed/picoclaw Issue #3159) | 今日 | 严重影响用户体验，强烈建议次日分配负责人 |

---

**总结：** 项目今日的代码产出量级非常大，安全与稳定修复主导了开发节奏，但部分高影响力的用户体验 Bug（`#3159`）和呼声很高的功能请求（`#3093`）存在被拖延的风险。建议维护团队释放一轮 beta 版本，将这些高频 fix 和 feat 分发给用户验证，形成正向反馈闭环。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 NanoClaw 项目动态日报（2026-06-23）。

---

# NanoClaw 项目动态日报 | 2026-06-23

## 1. 今日速览

过去 24 小时内，项目处于“增量迭代与整合成熟”阶段。尽管无新 Issue 或版本发布，但动态 PR 数量较多，且成功合并了一项重要的社区贡献（Telegram 集成）。整体健康度良好，开发侧重点从核心功能搭建转向渠道扩展与稳定性修复（如清理僵尸服务注册、修复轮询重复文本问题）。

- **活跃度评估**：中等偏上。6 条 PR 处于更新状态，1 条成功合入主分支。
- **关键信号**：渠道集成（Telegram/Email）与人工审批体验优化是当前社区最关注的方向。

## 3. 项目进展

### 已合并/关闭的 PR
- **[PR #2831] feat: add Telegram integration (verified working on v2.1.1)** — **已关闭/合并**
  - 作者：`aarchh`
  - 这是本周期最大的亮点。一条经过充分验证的 Telegram 集成方案被正式合入。它不仅丰富了 NanoClaw 的渠道生态，也证明了项目 `v2.1.1` 具有良好的扩展接口。对于希望使用 Telegram 作为 Agent 交互前端的用户而言，这是一个实质性的里程碑。
  - 链接：`nanocoai/nanoclaw PR #2831`

### 重要新 PR 进展
- **[PR #2832] feat(approvals): reject with reason** — **新提案**
  - 作者：`moshe-nanoco`
  - 改进了人工审批流程，增加了“附带原因的拒绝”按钮。之前 Agent 只能收到“已拒绝”，现在审批人可以写入一行原因并反馈给 Agent，使其能够自适应调整。这对于生产环境下的 Agent 协作是一次重要的 UX 微创新。
  - 链接：`nanocoai/nanoclaw PR #2832`

- **[PR #2830] fix(setup): reap dead peer service registrations** — **稳定性修复**
  - 作者：`amit-shafnir`
  - 修复了直接删除 NanoClaw 目录而未运行卸载程序时，`launchd` 或 `systemd` 残留僵尸服务的问题。该 PR 针对开发者和重度用户的痛点，提升了环境的整洁度和可靠性。
  - 链接：`nanocoai/nanoclaw PR #2830`

## 4. 社区热点

本周期讨论热度主要集中在合并与审批流程相关的 PR：

1.  **Telegram 集成合入（PR #2831）**
    - **热度分析**：无需多言，这是社区呼声较高的功能。合入状态激发了社区对“下一步是否支持更多渠道（如 Discord、Teams）”的期待。
    - 链接：`nanocoai/nanoclaw PR #2831`

2.  **带原因的拒绝（PR #2832）**
    - **热度分析**：虽然刚刚创立，但“拒绝时附带原因”这一功能触及了当前 Agent 反馈循环中的一个核心痛点。当一个请求被拒绝而不给原因时，Agent 往往会进行无意义的重试或给出错乱的回复。该 PR 直接回应了这一场景，预计会在设计师和运维人员中引发激烈讨论。
    - 链接：`nanocoai/nanoclaw PR #2832`

## 5. Bug 与稳定性

本周期无新 Bug 报告，但存在两项处于开放状态的修复性 PR，按严重度排列如下：

| 严重程度 | 问题描述 | 相关 PR | 作者 | 备注 |
|---|---|---|---|---|
| **高** | **轮询循环中 `send_message` 导致重复文本** | [#2531 fix(poll-loop)： suppress duplicate text](`nanocoai/nanoclaw PR #2531`) | `cfis` | 核心轮询逻辑的 Bug，直接导致特定渠道下消息重复。已开放一月有余，最近一次更新在 6 月 22 日，建议维护者尽快决策合入。 |
| **中** | **未清理的僵尸 Peer 服务** | [#2830 fix(setup)： reap dead peer service...](`nanocoai/nanoclaw PR #2830`) | `amit-shafnir` | 影响开发者切换分支或清理环境的体验，但本身不是运行时的应用程序 Bug。修复逻辑清晰，预计可顺利合入。 |

## 6. 功能请求与路线图信号

结合本周期 PR 动态，以下几个方向强烈暗示了 NanoClaw 的未来路线图：

1.  **渠道泛化（Channel Generalization）**
    - **信号**：Telegram 整合（#2831）落地 + 还在持续的 Email 集成（#1235）。
    - **判断**：“万能收件箱”是 NanoClaw 非常明确的战略目标。用户不满足于仅通过一个平台与 Agent 对话，`v2.1.1` 的渠道接口正在走向成熟。

2.  **终端可观测性（CLI Dashboard）**
    - **信号**：PR #2795 `add-clidash`。
    - **判断**：用户开始要求直接从命令行读取只读仪表盘数据，表明 Power User 群体希望在不离开终端的环境下监控 Agent 运行状态。

3.  **人机协作精细化（Human-in-the-loop 进化）**
    - **信号**：PR #2832 `reject with reason`。
    - **判断**：这表明项目正在从简单的“审批通过/否决”二元机制，迈向更复杂的“批评与反馈”机制。这将是企业级部署中提升 AI 行为可控性的关键一环，极有可能被纳入下一版本（v2.2.0）。

## 7. 用户反馈摘要

由于本周期未产生新的 Issues，我们通过活跃的 PR 内容提取出如下用户痛点与诉求：

1.  **对分支切换/开发环境清洁度的不满**
    - **来源**：PR #2830
    - **场景**：开发者在切换分支或删除项目后，操作系统持续尝试启动已不存在的 `index.js`，导致资源浪费和日志杂乱。
    - **诉求**：希望 `setup` 或 `uninstall` 脚本更“健忘”，能自动感知并清理孤立进程注册。

2.  **对 Agent 回复理解的困惑**
    - **来源**：PR #2531 与 PR #2832
    - **场景**：当 Human Approver 拒绝 Agent 操作但未给出原因时，Agent 陷入无意义的重试循环。当轮询机制触发发送消息时，又会导致消息重复。
    - **诉求**：用户不仅仅需要 AI 执行任务，更需要 AI 能“理解拒绝上下文”，以及避免“信息冗余”。这两个 PR 反映了用户对 Agent 稳定性和智能程度提出了更高要求。

## 8. 待处理积压

以下两项 PR 跨越时限较长，需维护者特别关注，防止因关注度下降而变成“遗珠”：

1.  **【PR #1235】IMAP/SMTP 邮件集成**
    - **开启时间**：2026-03-18（距今超过 3 个月）
    - **状态**：Open，作者 `aronjanosch` 于 6 月 22 日进行了最近一次更新。
    - **提醒**：这是体积最大的功能 PR，涉及 6 个 MCP tools。项目组应对作者的更新做出回应，决定是继续细化还是划定范围进行基础合入，防止作者因长期无反馈而流失。
    - 链接：`nanocoai/nanoclaw PR #1235`

2.  **【PR #2531】轮询重复文本修复**
    - **开启时间**：2026-05-18（距今超过 1 个月）
    - **状态**：Open，最近更新于 6 月 22 日。
    - **提醒**：这是一个直接影响用户体感的 Bug Fix。作为稳定性和核心通信逻辑的修正，建议维护者在路线图中将其优先级提升至“High”，尽快完成 Code Review 并合入。
    - 链接：`nanocoai/nanoclaw PR #2531`

---
**报告生成时间**：2026-06-23
**数据源**：NanoClaw GitHub Repository （qwibitai/nanoclaw / nanocoai/nanoclaw）

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是基于 NullClaw 项目今日 GitHub 数据生成的 2026-06-23 项目动态日报。

---

### NullClaw 项目动态日报 | 2026-06-23

#### 1. 今日速览
NullClaw 项目今日整体处于低频但健康的维护期。过去 24 小时内未产生新 Issue，亦无新版本发布，社区互动较少。但值得注意的是，一个针对 Matrix 通道核心稳定性的 Bug 修复 PR（#968）已正式进入开放评审阶段，标志着项目在基础设施健壮性上正在取得实质性进展。与此同时，Docker 依赖更新 PR（#956）已积压逾一周，建议维护者给予关注以避免 CI 风险累积。

#### 2. 版本发布
今日无新版本发布。

#### 3. 项目进展
今日暂无 PR 被合并或关闭。目前有 2 个开放 PR 处于待合并状态，构成项目的核心推进方向：
- **[Matrix 重启后同步游标持久化 #968](https://github.com/nullclaw/nullclaw/pull/968)**：该 PR 由 @addadi 提交，旨在解决 Matrix 模块仅将 `/sync` 游标（`next_batch`）存储于内存，导致每次重启后必须进行全量初始同步的问题。此修复若合并，将大幅提升机器人矩阵通道的长期运行可靠性。
- **[Docker 基础镜像依赖升级 #956](https://github.com/nullclaw/nullclaw/pull/956)**：由 Dependabot 自动发起，将 Docker 基础镜像从 Alpine 3.23 升级至 3.24，跟进上游安全更新与依赖维护。

#### 4. 社区热点
今日项目社区互动趋于冷淡。全部现存 Issue 与 PR 均无新增评论或表情反应。由于缺乏讨论，社区关注焦点目前完全集中在 _PR #968_ 的首轮评审反馈上，其后续的对话量将成为衡量社区对稳定性改进关注度的关键指标。

#### 5. Bug 与稳定性
今日无新增 Bug 报告，但 _一个此前报告的高严重度 Bug_ 的修复方案进入审查状态：
- **[严重：高] Matrix 同步游标丢失**：`next_batch` 未持久化，导致进程重启后触发不必要的 Homeserver 全量同步。这会增加服务器负载，并可能在恢复期造成消息处理异常。**修复 PR #968 已提交并处于开放审查中。** [查看 PR](https://github.com/nullclaw/nullclaw/pull/968)

#### 6. 功能请求与路线图信号
今日无新功能请求提交至 Issue 区。尽管 _PR #968_ 被归类为 Bug 修复，但其解决的核心问题（状态持久化与降级恢复）可视为一项未言明的强烈功能诉求。该合入请求很可能直接推动项目进入 Patch 阶段，成为下一版本最核心的变更内容。

#### 7. 用户反馈摘要
今日无用户 Issue 评论或详细反馈可供分析。项目当前处于用户反馈的静默期，维护者可能需要通过其他渠道（如 Discord 或 Matrix 群组）主动了解用户在实际使用中对重启行为的体验感受。

#### 8. 待处理积压
- **[Docker 依赖更新 PR #956](https://github.com/nullclaw/nullclaw/pull/956)**（创建于 2026-06-15，已开放 8 天）：由 Dependabot 自动提交的常规镜像升级。虽然风险较低，但长期未被合并将导致 CI 告警堆积，并可能错过上游安全修复。建议项目维护者尽快安排审查并合并。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-23

---

## 1. 今日速览

过去 24 小时内，IronClaw 保持着极高的开发活跃度，共产生 **16 条 Issue 更新**（13 条活跃/新开、3 条关闭）与 **23 条 PR 更新**（15 条待合并、8 条已关闭）。**无新版本发布**。

社区与团队正围绕 **三大战投** 密集推进：**Reborn 性能专项**（#5125 系列）、**自动化管理能力**（暂停/恢复/删除）、以及 **权限与审批模型**（#5062/#5063 已合并落地）。值得高度警惕的是，主分支在经历了 10 个 commits 的合并后暴露了 **严重回归**（#5139），导致 Web/Research 任务启动时直接挂起，0 次 LLM 调用即超时，直接影响 PinchBench 日常测评的 14% 任务。这一事件凸显了在快速迭代中对回归测试覆盖的迫切需求。

> **项目健康度评估**：🔴 🟡 🟢 **活跃 (Active)** — 功能开发推进快（权限/自动化/并发架构均已落地），但主干稳定性出现预警，CI（Nightly E2E #4108）持续飘红，性能合规仍是用户侧的突出痛点。

---

## 2. 版本发布

**无新版本发布。** 但多项关键特性已密集合并至 `main`，预计下一轮版本发布将包含：并发 Turn 执行、Per-tool 权限覆盖、DB 驱动 Auto-approve、自动化 CRUD 支持等重量级变更。

---

## 3. 项目进展

过去 24 小时内关闭/合并的 **重要 PR** 标记着项目在功能、性能与架构三条战线上的系统迈步：

### ✅ 已合并/关闭

| PR / Issue | 类别 | 关键演进 |
|---|---|---|
| [#5085](https://github.com/nearai/ironclaw/pull/5085) | **性能·并发** | 合并 `TurnRunScheduler`，Reborn 运行时从**严格串行**走向**并发执行**，是解决本地卡顿的关键一步 |
| [#5062](https://github.com/nearai/ironclaw/pull/5062) + [#4958](https://github.com/nearai/ironclaw/issues/4958) | **权限模型** | Per-tool 三态权限落地（always_allow / ask_each_time / disabled），用户终于能精细控制每一个工具的行为 |
| [#5063](https://github.com/nearai/ironclaw/pull/5063) + [#4959](https://github.com/nearai/ironclaw/issues/4959) | **审批策略** | DB 后端的全局 Auto-approve 设置 + Never-auto-approve 硬约束。**无需重启**即可实时生效，审批体验质变 |
| [#5140](https://github.com/nearai/ironclaw/pull/5140) | **稳定性** | 修复 `trigger_create` 失败时返回 opaque 错误的问题，转为结构化且可交互的修复建议 |
| [#5135](https://github.com/nearai/ironclaw/pull/5135) | **架构重构** | 启动 `ironclaw_reborn_composition` 巨型 crate（~132k 行）的解构，第一刀成功落下 |
| [#5081](https://github.com/nearai/ironclaw/pull/5081) | **基础设施** | 新增 `hosted-single-tenant` 托管 Postgres 部署 profile，为托管预览路径铺路 |

### 📌 待合并/活跃中（临近完成）

| PR / Issue | 进度 | 预期影响 |
|---|---|---|
| [#5131](https://github.com/nearai/ironclaw/pull/5131) + [#5121](https://github.com/nearai/ironclaw/issues/5121) | 活跃 | 自动化的暂停/恢复能力——完整性链条最后几块 |
| [#5133](https://github.com/nearai/ironclaw/pull/5133) + [#5122](https://github.com/nearai/ironclaw/issues/5122) | 活跃 | 自动化的删除支持 + WebUI v2 endpoint 与确认弹窗 |
| [#5137](https://github.com/nearai/ironclaw/pull/5137) | Draft | 巨型 crate 解构第二步：提取出与产品无关的 HTTP 中间件 Kit |

---

## 4. 社区热点

过去 24 小时内热度最高、讨论最集中的议题：

### 🔥 #5139 — [CRITICAL] Reborn 回归：Web/Research 任务初始化直接挂起
- **链接**：[nearai/ironclaw Issue #5139](https://github.com/nearai/ironclaw/issues/5139)
- **作者**：`pranavraja99`
- **诉求**：主分支在 `2b2ccc55` → `704fcd43` 仅 **10个 commits** 的变动后，Web/Research 任务的 turn 在初始化阶段直接超时（**0 LLM 调用、0 工具调用**），PinchBench 日常测评中 **21/147** 的任务被清零。
- **社区反应**：该问题被迅速定位至回归窗口期，但尚无关联的 fixing PR。作为直接影响主干可用性的 **P0 级事件**，它已成为社区当前最关注的焦点。

### 🔥 #5125 — Reborn 性能专项追踪周（06/22 - 06/28）
- **链接**：[nearai/ironclaw Issue #5125](https://github.com/nearai/ironclaw/issues/5125)
- **作者**：`think-in-universe`
- **诉求**：用户在本地 Dogfooding 中明确感受到 Reborn 的卡顿。该 Issue 是本周性能优化的总入口，已分解出 **延迟日志（#5126）**、**推理延迟分析（#5127）**、**减少冗余步骤（#5128）** 三条并行子议题。社区对此的持续关注显示了**感知性能**已成为当前体验的核心瓶颈。

### 🔥 #5061 — Reborn 技能提取与自我进化
- **链接**：[nearai/ironclaw PR #5061](https://github.com/nearai/ironclaw/pull/5061)
- **作者**：`krishna-505`
- **标签**：`size: XL`, `risk: medium`, `feature`
- **诉求**：为 Reborn 引入 Hermes 风格的 Skill Extraction 机制——在每个成功的 turn 后自动蒸馏交互记录为 `SKILL.md` 并安装。尽管该 PR 体量极大且处于早期 Review 阶段，但它代表了社区对于 **Agent 自我学习和进化** 的强烈技术渴望，是未来路线图的重要信号。

---

## 5. Bug 与稳定性

### 🔴 严重（影响核心功能 / CI）

| ID | 标题 | 影响 | 状态 | 对应修复 |
|---|---|---|---|---|
| [#5139](https://github.com/nearai/ironclaw/issues/5139) | Reborn 回归：Web/Research 任务启动挂起 | 丢失 PinchBench 14% 任务 (21/147)，零 LLM 调用 | **未修复，排查中** | — |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E 持续失败 | CI 持续红灯 | **未修复** | — |

### 🟡 中等（影响特定功能）

| ID | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#5129](https://github.com/nearai/ironclaw/issues/5129) | Always approve 在 `outbound_delivery_target_set` 上失效 | 自动审批工作流受阻 | **未修复，需复现定位** |
| [#4985](https://github.com/nearai/ironclaw/issues/4985) | Engine V2: admin usage API 返回空数据 | 管理员无法监控 LLM 用量 | **未修复** |

### 🟢 已修复 / 已有修复方案

| ID | 标题 | 修复状态 |
|---|---|---|
| [#5140](https://github.com/nearai/ironclaw/pull/5140) | 触发器不可见输入错误 | ✅ 已合并 |
| [#4969](https://github.com/nearai/ironclaw/pull/4969) | Google WASM 工具 401 未映射为 `auth_required` | 🔄 PR 待合并 |

---

## 6. 功能请求与路线图信号

### ✅ 已进入实施 / 即将发布的路线图特性

以下能力在过去 24 小时内已完成合并或处于临近合并状态，**大概率进入下个版本**：

| 特性 | 对应 PR / Issue | 状态 |
|---|---|---|
| Per-tool Permission Override | [#5062](https://github.com/nearai/ironclaw/pull/5062) | ✅ 已合并 |
| DB-backed Global Auto-approve | [#5063](https://github.com/nearai/ironclaw/pull/5063) | ✅ 已合并 |
| 并发 Turn 执行 | [#5085](https://github.com/nearai/ironclaw/pull/5085) | ✅ 已合并 |
| 自动化暂停/恢复 | [#5131](https://github.com/nearai/ironclaw/pull/5131) | 🔄 待合并 |
| 自动化删除 | [#5133](https://github.com/nearai/ironclaw/pull/5133) | 🔄 待合并 |
| 性能追踪与归因日志 | [#5125](https://github.com/nearai/ironclaw/issues/5125) + sub-issues | 🔄 进行中 |

### 📢 路线图信号（潜在下一阶段方向）

| 信号 | 来源 | 涵义 |
|---|---|---|
| **Telegram Channel 支持** | Issue [#5124](https://github.com/nearai/ironclaw/issues/5124) | 从 WebUI/Slack 向 **多渠道 AI 终端** 演进，Telegram 被明确指出 |
| **GitHub Bug 工作流平台用例** | PR [#5134](https://github.com/nearai/ironclaw/pull/5134) | 提出用 IronClaw 自动化处理 GitHub Bug 报告，将平台本身作为 **开发者工具（Meta-Tool）** 使用 |
| **Agent 自我进化能力** | PR [#5061](https://github.com/nearai/ironclaw/pull/5061) | Skill Extraction（技能提取与注入），虽然体量大，但代表了社区 **“让 Agent 学会学习”** 的期待 |
| **Engine V2 用量持久化** | Issue [#4985](https://github.com/nearai/ironclaw/issues/4985) | 运维可观测性的核心环节，Engine V2 部署下 admin 页面空缺直接影响了管理决策 |

---

## 7. 用户反馈摘要

从过去 24 小时的 Issue 和 PR 评论区提炼的真实用户声音：

### 🗣 感知性能是首要痛点（来源：#5125）
> “Users are seeing slowdowns during local dogfooding.”
> —— 开发者在明确提出性能专项时引用的用户反馈。功能堆叠之后，**"慢"** 已成为日常体验的瓶颈。

### 🗣 配置一致性亟待改善（来源：#5129）
> “Always approve is not working on `outbound_delivery_target_set`.”
> —— 用户对配置生效机制的困惑。尽管 #5063 已合并，但特定场景下 Auto-approve 的失效说明仍有边缘 case 未覆盖，配置逻辑的语义需要更透明。

### 🗣 主干可用性零容忍（来源：#5139）
> “reborn run failed: reborn turn timed out… having made zero LLM calls and zero tool calls.”
> —— 回归导致的完全挂起触发了用户对主线稳定性的高度警惕。14% 的任务清零是在 CI 层面才被暴露的，这暗示了用户在实际使用中暴露的概率并不低。

### 🗣 跨渠道需求明确（来源：#5124）
> “Support Telegram as a channel for IronClaw Reborn.”
> —— 用户不再满足于单一的 WebUI，明确提出 **Telegram Inbound/Outbound** 需要走 Reborn 原生通道，而不是 Legacy v1。

---

## 8. 待处理积压

以下 Issue / PR 已存在较长时间且无有效进展，可能构成技术债务或社区信任危机，**建议维护团队给予关注**：

### 🔴 高度关注

| ID | 标题 | 潜伏期 | 风险 |
|---|---|---|---|
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E 持续失败 | 2026-05-27 (25天+) | CI 基础设施绿线长期缺失，隐蔽缺陷可能流入主分支 |

### 🟡 中期关注

| ID | 标题 | 潜伏期 | 风险 |
|---|---|---|---|
| [#4712](https://github.com/nearai/ironclaw/pull/4712) | Slack WebUI 设置迁移 | 2026-06-10 (13天+) | Slack 体验长期处于半重构状态 |
| [#4969](https://github.com/nearai/ironclaw/pull/4969) | Google WASM Auth 错误修复 | 2026-06-16 (7天+) | 小修复但影响体验，积压过久可能引入更多耦合冲突 |
| [#4032](https://github.com/nearai/ironclaw/pull/4032) | wasm 依赖批量更新 | 2026-05-25 (29天+) | 长期未合并的依赖更新；WASM 工具链变动可能伴随 breaking changes，越早处理风险越低 |
| [#4787](https://github.com/nearai/ironclaw/pull/4787) | Barcelona Hackathon Fork | 2026-06-12 (11天+) | 被标记为 `[NO MERGE]`，作为 Hackathon 入口，长期不 sync 上游可能导致 fork 与主干严重偏离 |

---

**报告日期**：2026-06-23 | **数据窗口**：过去 24 小时 | **分析师**：IronClaw 开源项目分析师 Executive Agent

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是为您生成的 **LobsterAI 开源项目动态日报（2026-06-23）**，内容基于提供的数据整理，客观反映项目近期状态。

---

# LobsterAI 项目动态日报 · 2026-06-23

## 今日速览

项目在过去 24 小时内（主要覆盖 2026-06-22）整体活跃度较高。**共 6 个 Pull Request 被合并或关闭**，集中在 Cowork 计划模式功能开发、OpenClaw 插件兼容性修复以及文档/测试更新，项目核心功能有实质推进。Issue 方面无新报告，存量 5 个问题均已超过 2 个月未关闭，反映了 **Bug 修复的积压仍在持续**。无新版本发布，社区贡献以“dependabot”和内部团队为主。

## 版本发布

无

## 项目进展

今日共有 **6 个 PR 被合并/关闭**，均发生于 2026-06-22，代表了项目在以下方向的明显推进：

1. **新功能：Cowork 计划模式（Plan Mode）**  
   - PR [#2183] [CLOSED] `feat(cowork): add plan mode workflow`  
   - 在 Composer 中新增计划模式，支持将建议作为独立交互块渲染，提供复制、下载、展开/折叠操作，并防止计划过程中发生工具调用。该功能显著增强了复杂任务的协作工作流。
2. **OpenClaw 插件系统兼容性改进**  
   - PR [#2186] [CLOSED] `fix(openclaw): compile NIM plugin runtime entry`  
     - 解决 NIM 通道 TypeScript 运行时的编译与打包问题，确保 OpenClaw CLI 安装后正常运行。
   - PR [#2185] [CLOSED] `fix(openclaw): include cwd in reply options patch`  
     - 补充缺失的 `GetReplyOptions.cwd` 字段，修复插件 SDK 声明生成。
   - PR [#2182] [CLOSED] `fix(openclaw): support upgraded im plugin installs`  
     - 升级并兼容钉钉、飞书、企业微信等 IM 插件的安装布局，支持 OpenClaw 2026.6.1 的新结构。
3. **质量与文档**  
   - PR [#2187] [CLOSED] `test: align OpenClaw metadata expectations`  
     - 更新后端能力模型关于推理模型的元数据测试，提升测试覆盖准确性。
   - PR [#2184] [CLOSED] `docs(agents): update repository guidance`  
     - 更新 AGENTS.md，完善架构说明与贡献指南，降低新贡献者门槛。

这些合并表明项目 **正在同时推进功能迭代与基础设施稳定**，尤其是 OpenClaw 插件生态的正向演进。

---

## 社区热点

由于数据中注释量较少，所有 Issues 目前仅各有 1 条评论（可能为机器标记 “stale”），暂未形成热烈讨论。但以下问题具有较高关注度，代表了用户常见的痛点：

- **[#1414] 概览页“总会话数”始终显示为 0**  
  > 用户明确指出“总 API 调用数”432 次、“今日用量”444.39 积分，但总会话数始终为 0，数据逻辑明显异常。此问题严重影响用户对使用量的掌握，期待维护者回应或修复。  
  > 链接: netease-youdao/LobsterAI Issue #1414

- **[#1411] 概览页时间维度筛选器“过去30天”点击无响应**  
  > 功能触碰无反馈，用户体验直接受损，筛选器失效意味着无法切换统计时段，属于 UI 级别的功能性 Bug。  
  > 链接: netease-youdao/LobsterAI Issue #1411

- **[#1416] 切英文后 UI 布局错乱**  
  > 国际化适配不足，文本长度变化导致卡片内文字重叠，暴露前端响应式设计的短板。  
  > 链接: netease-youdao/LobsterAI Issue #1416

这些 Issues 虽已长期开放（始于 4 月 3 日），但近期（6 月 22 日）被再次更新，说明社区仍有使用诉求。

---

## Bug 与稳定性

今日未报告新 Bug，但以下存量 Bug 依然未解决，按严重程度排序：

| 严重度 | Issue | 描述 | 分析 | 状态 |
|--------|-------|------|------|------|
| 🔴 高 | [#1414] | 总会话数始终为 0，与 API 调用数和积分数据矛盾 | 大概率是会话计数逻辑缺陷或数据查询错误，直接影响用户对使用量的判断。 | 无对应 Fix PR |
| 🟠 中 | [#1411] | “使用概览”时间筛选器点击无响应 | 前端事件绑定或状态管理问题，使统计学功能失效。 | 无对应 Fix PR |
| 🟡 低 | [#1416] | 英文下 UI 文本重叠 | 国际化布局未适配，影响英文用户体验。 | 无对应 Fix PR |
| 🟡 低 | [#1409] | 跨天定时任务未生成历史记录 | 定时任务逻辑存在边界条件缺陷，可能丢失日志。 | 无对应 Fix PR |
| 🟢 提示 | [#1413] | Skills 较多时提问输入框页面显示不友好 | 排版溢出，属于易用性优化。 | 无对应 Fix PR |

**总体来看，核心 Bug 仍缺少修复 PR，需要维护者积极介入。**

---

## 功能请求与路线图信号

- **计划模式（Plan Mode）**：合并的 [#2183] 证实团队已在 Cowork 工作流中增加了计划能力，这是对用户希望更结构化协作的回应，很可能成为下一版本的核心特性。
- **OpenClaw 插件体验提升**：多个 OpenClaw 相关 PR 被合并，表明项目正在集中强化第三方插件安装与运行时的兼容性，这通常是为了支持更丰富的集成生态。
- **数据库性能与缓存**：积压 PR 中包括 Sqlite 写入防抖（[#1410]）和 Prompt 构建缓存（[#1421]），这些优化若被合并，将显著改善高频场景（如流式响应）的响应流畅度，属于潜在的路线图重点。
- **并发与容错**：[#1420] 修复 cron 重入和幽灵事件，[#1408] 处理 Promise 链未捕获错误，这些稳定性修复虽未在今日合并，但显示出社区对健壮性的持续关注。

综合来看，**下一阶段极可能侧重 Cowork 增强、OpenClaw 生态完善、以及性能/健壮性提升**。

---

## 用户反馈摘要

以下反馈来自 Issues 评论（每个 Issue 各有一条评论，内容未公开，但标题与描述已足够反映核心观点）：

- **使用概览数据可信度不足**：用户明确表示“总会话数始终为 0”，并提供了“总 API 调用数 432”等对比数据，说明统计环节存在明显逻辑错误，影响了用户对系统可用性的信任。
- **UI 交互受限**：筛选器无法点击、技能列表溢出、英文布局错乱，反映出前端在交互反馈和响应式上仍需打磨。
- **定时任务长尾问题**：跨天触发未生成历史记录，虽非高频场景，但涉及数据完整性和自动化稳定性，用户期待更严谨的边界处理。

总体而言，**用户对概览页的体验反馈最为集中，且提出时已附带复现步骤和截图，属于高质量反馈，亟待项目团队优先响应**。

---

## 待处理积压

以下为已超过 2 个月未取得实质性进展（未关闭、未分配、无最近维护者回复）的重点 Issue 与 PR，提醒维护组关注：

### Issues
- **[#1409] 定时任务已触发，未生成历史记录**（2026-04-03 创建，2026-06-22 更新）  
  链接: netease-youdao/LobsterAI Issue #1409
- **[#1411] 概览页时间维度筛选器无响应**（同上）  
  链接: netease-youdao/LobsterAI Issue #1411
- **[#1413] Skills 较多时页面展示不友好**（同上）  
  链接: netease-youdao/LobsterAI Issue #1413
- **[#1414] 概览页总会话数显示为 0**（同上）  
  链接: netease-youdao/LobsterAI Issue #1414
- **[#1416] 切换英文后 UI 布局错乱**（同上）  
  链接: netease-youdao/LobsterAI Issue #1416

### Pull Requests（长期开放、状态为 Open 且 4 月创建）
- [#1407] fix: OpenClaw Token Proxy 无请求体大小限制  
- [#1408] fix: MCP Bridge Server 的 handleRequest 处理 Promise 返回  
- [#1410] perf: SqliteStore.set() 每次写入都同步落盘  
- [#1415] fix: migration completion flag inside transaction success path  
- [#1419] fix: NIM 群组类型枚举值映射错误  
- [#1420] fix: cron 重入并发与 stopPolling 幽灵事件  
- [#1421] perf: buildUserMemoriesXml() 全量查询无缓存  

这些 PR 已长时间等待 review 或 rebase，其中部分与稳定性/性能高度相关（如 #1407 的安全限制、#1410 的写入防抖），建议团队优先安排时间处理，以避免资源浪费和社区参与度下降。

---

**报告结束**

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

**CoPaw (QwenPaw) 项目动态日报 — 2026-06-23**

---

## 1. 今日速览

- **整体活跃度极高**：过去 24 小时产生 23 条 Issue 更新（其中 21 条活跃、2 条关闭）、50 条 PR 更新（15 条合并/关闭、35 条待合并）。社区贡献者踊跃，尤其多名首次贡献者提交了移动端适配与测试代码。
- **质量与体验提升成为焦点**：大量 PR 针对前端移动适配、单元测试覆盖、以及核心 Bug 修复（会话切换锁、文件传输等）。但无新版本发布，项目正处于功能完善与稳定化阶段。
- **用户稳定性质疑集中**：多个高评论数量的 Issue 报告了进程冻结、Cron 调度停止、Dream 任务失败等严重问题，反映出对核心可靠性的紧迫需求。
- **测试基础设施加速建设**：今日新开的两组测试 PR（前端 ~120 用例、后端 crons 模块 51 用例）标志着项目开始系统性提升代码质量，是对社区“先稳定再新增”呼声的正面回应。

---

## 2. 版本发布

*今日无新版本发布。*

---

## 3. 项目进展

> 今日共有 **15 个 PR 被合并或关闭**，虽未在列表中详细显示，但从活跃 PR 与关联 Issue 可以判断项目在以下方面取得实质推进：

### 🧪 测试覆盖
- **[PR #5409] test(console): PR#1 — frontend M2 unit tests (Stores + Hooks + Control pages)**  
  新增 17 个测试文件、约 120 个用例，覆盖 Zustand 状态管理、React Hooks 及控制页面纯函数。**仅测试改动、不修改源码**，为前端稳定性打下基础。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5409)
- **[PR #5405] test(unit): add crons module unit tests — W1 sprint (51 cases)**  
  为 `crons` 模块（Cron 调度）添加单元测试，覆盖模型验证、调度逻辑等。该模块此前零测试，且已知存在调度停止 Bug。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5405)

### 📱 移动端适配（系列 PR）
多名首次贡献者（@yaozy2020）提交了 **7 个移动适配 PR**，覆盖核心页面：
- 模型选择器下拉 [PR #5355](https://github.com/agentscope-ai/CoPaw/pull/5355)
- 工作空间/文件页 [PR #5384](https://github.com/agentscope-ai/CoPaw/pull/5384)
- 频道管理页 [PR #5369](https://github.com/agentscope-ai/CoPaw/pull/5369)
- MCP、ACP、Inbox、环境配置页 [PR #5381–#5385](https://github.com/agentscope-ai/CoPaw/pulls?q=is%3Apr+is%3Aopen+5381+5382+5383+5384+5385)  
这些 PR 均遵循卡片式/单列响应布局，提升窄屏可用性。

### 🔧 关键修复与功能
- **[PR #5407] fix: cap the file size of send_file_to_user**  
  限制文件传输大小，防止超大文件导致前端/后端异常（关联 Issue #5370 文件 404 问题）。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5407)
- **[PR #5357] fix(#5354): release session switch lock on embedded mode completion**  
  修复嵌入式模式下会话切换卡死问题，此 Issue 已被关闭（#5354），PR 仍在审查中。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5357)
- **[PR #5400] feat(tui): animate logo into place on startup**  
  为 TUI 欢迎界面增加启动动画，提升用户感知。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5400)

### 🧩 其他活跃 PR
- 重构治理模块（ToolGuard 合并到 Policy 引擎）[PR #5301](https://github.com/agentscope-ai/CoPaw/pull/5301)
- 新增 Slack Channel 支持（Socket Mode + 流式）[PR #5193](https://github.com/agentscope-ai/CoPaw/pull/5193)
- 文档：Langfuse Docker 部署  [PR #5380](https://github.com/agentscope-ai/CoPaw/pull/5380)

---

## 4. 社区热点

> 以下 Issue/PR 因评论数多、涉及面广成为今日社区讨论核心：

| 编号 | 标题 | 评论 | 分析 |
|------|------|------|------|
| [#5218](https://github.com/agentscope-ai/CoPaw/issues/5218) | 子Agent触发上下文压缩时QwenPaw进程冻结无响应 | **17** | **最严重的稳定性问题**。进程完全无响应，只能重启。缺乏任何恢复机制，用户工作流被打断。已持续一周，尚未有修复 PR。 |
| [#5262](https://github.com/agentscope-ai/CoPaw/issues/5262) | 每次升级后被禁用的内置技能重新启用 | **9** | **配置持久化反复出现**。这是该 Issue 的第二次提交（第一次 #4807 未彻底修复）。用户感到挫败，期待开发者将此纳入升级流程测试。 |
| [#5345](https://github.com/agentscope-ai/CoPaw/issues/5345) | 自定义 OpenAI 兼容提供商不支持 function calling | **5** | **限制模型选型**。OMLX 等供应商完整实现了 tools API，但在 CoPaw 中失败，用户可能因此转向其他平台。 |
| [#5370](https://github.com/agentscope-ai/CoPaw/issues/5370) | send_file_to_user 产生 404（已关闭） | **5** | 文件预览 URL 构造错误，导致前端无法展示。虽已关闭，但关联的 PR #5407 尚为 open，需确保彻底解决。 |
| [#5354](https://github.com/agentscope-ai/CoPaw/issues/5354) | 消息队列串台+切换对话切不回去（已关闭） | **4** | 消息队列新功能虽好，但引入回归。用户明确赞赏队列效率提升，但批评隔离性不足。PR #5357 试图修复。 |
| [#2969](https://github.com/agentscope-ai/CoPaw/issues/2969) | [Feature] 增加个人知识库功能 | **5** 👍**2** | 长期功能请求，用户期待将 CoPaw 与个人知识结合。虽未纳入近期路线图，但点赞数高，说明需求持续存在。 |

**趋势总结**：社区对 **稳定性**（进程冻结、配置重置、Cron 停止）和 **兼容性**（自定义提供商、Shell 命令）的关注度远高于新功能。多位用户在评论中表示“希望先修好再添新”。

---

## 5. Bug 与稳定性

> 按严重程度排列（🔴 严重 / 🟠 高 / 🟡 中 / 🟢 低），标注是否已有 Fix PR。

| 严重度 | Issue | 描述 | 影响 | Fix PR 状态 |
|--------|-------|------|------|-------------|
| 🔴 | [#5218](https://github.com/agentscope-ai/CoPaw/issues/5218) | **子Agent上下文压缩导致进程冻结** | 核心功能不可用，需手动重启 | 无 |
| 🔴 | [#5402](https://github.com/agentscope-ai/CoPaw/issues/5402) | **Dream 任务执行失败**（三个 Agent 均报错） | 自动记忆/总结功能失效 | 无 |
| 🟠 | [#5398](https://github.com/agentscope-ai/CoPaw/issues/5398) | **Cron 调度停止分发已启用的 job** | 计划任务全部停摆，app 进程存活 | 测试 PR #5405 覆盖此模块 |
| 🟠 | [#5401](https://github.com/agentscope-ai/CoPaw/issues/5401) | **Console 打开大量工具调用历史时白屏崩溃** | 前端完全不可渲染，数据丢失 | 无 |
| 🟠 | [#5379](https://github.com/agentscope-ai/CoPaw/issues/5379) | **新安装启动直接显示 Internal Server Error** | 新用户无法使用，入口阻塞 | 无 |
| 🟡 | [#5373](https://github.com/agentscope-ai/CoPaw/issues/5373) | **Shell 命令无法解析重定向、管道等特殊字符** | 限制自动化脚本能力（如 `ls > file`） | 无 |
| 🟡 | [#5345](https://github.com/agentscope-ai/CoPaw/issues/5345) | **自定义 OpenAI 兼容提供商不支持 function calling** | 模型工具调用能力缺失 | 无 |
| 🟡 | [#5333](https://github.com/agentscope-ai/CoPaw/issues/5333) | **Agent 卡住无响应，文本框状态错误** | 可能在 DeepSeek 兼容上出现，影响交互 | 无 |
| 🟡 | [#5330](https://github.com/agentscope-ai/CoPaw/issues/5330) | **智谱 API 测试连接成功但模型测试全部失败** | 内置供应商无法使用 | 无 |
| 🟢 | [#5403](https://github.com/agentscope-ai/CoPaw/issues/5403) | **浏览器自动填充干扰模型配置页搜索框** | UI 混淆，不影响功能 | 无 |
| 🟢 | [#5374](https://github.com/agentscope-ai/CoPaw/issues/5374) | **Mac Chrome 下无法拖拽上传附件** | 移动/桌面端体验不一致 | 无 |
| 🟢 | [#5378](https://github.com/agentscope-ai/CoPaw/issues/5378) | **自定义模型 endpoint 写入查询框且无法删除，页面空白** | 配置页面异常，不影响运行时 | 无 |

**注意**：  
- #5370（文件 404）已关闭，关联 PR #5407（文件大小限制）仍在 open，但可能已部分修复。  
- #5354（队列串台）已关闭，PR #5357（会话切换锁）正在审查。

---

## 6. 功能请求与路线图信号

| Issue | 功能 | 潜力分析 |
|-------|------|----------|
| [#5392](https://github.com/agentscope-ai/CoPaw/issues/5392) | **解耦智能体与工作空间，支持复用与切换** | 涉及核心架构变更，符合高级用户对灵活工作流的需求，可能会在后续大版本中考虑。 |
| [#5387](https://github.com/agentscope-ai/CoPaw/issues/5387) | **为 Dream 记忆整合添加 recall-aware 信号** | 增强记忆筛选的智能性，与现有记忆系统兼容，实施成本中等，可能被纳入记忆模块优化。 |
| [#2969](https://github.com/agentscope-ai/CoPaw/issues/2969) | **个人知识库功能** | 长期需求（👍2），需要前后端及存储支持，暂无明确时间表，但社区讨论持续。 |
| [#5374](https://github.com/agentscope-ai/CoPaw/issues/5374) | **支持拖拽上传附件** | 相对较小改进，移动适配系列过后此问题可能自然解决。 |
| [#5360](https://github.com/agentscope-ai/CoPaw/issues/5360) | **先稳定核心再添加新功能** | 这不是具体功能，而是社区投票。结合今日大量测试 PR，团队已开始采纳此建议。 |

**路线图信号**：  
- 测试 PR（#5409、#5405）显示团队正在主动提升代码质量，侧面回应了 #5360 的诉求。  
- 移动适配系列 PR（7 个页面）暗示下一版本可能正式支持移动端。  
- 无新功能大 PR 被合并，当前阶段倾向于稳定与补齐短板。

---

## 7. 用户反馈摘要

> 从 Issue 评论与描述中提炼真实声音（**✓** 满意 / **✗** 痛点）。

| 反馈 | 来源 | 引用/摘要 |
|------|------|-----------|
| ✗ **升级后配置丢失** | [#5262](https://github.com/agentscope-ai/CoPaw/issues/5262) | *“每次升级，被禁用的内置技能又会重新变回启用。”* 期望升级保留禁用状态。 |
| ✗ **消息队列串台** | [#5354](https://github.com/agentscope-ai/CoPaw/issues/5354) | *“在 agent 甲这里输入了消息发送队列，然后切换到 agent 乙，结果这个消息就会发送到 agent 乙，让它莫名其妙！”* |
| ✓ **消息队列效率提升** | [#5354](https://github.com/agentscope-ai/CoPaw/issues/5354) | *“新增了消息队列，是个非常不错的进展，极大地提高了效率。”* 但同时带来回归。 |
| ✗ **进程冻结只能重启** | [#5218](https://github.com/agentscope-ai/CoPaw/issues/5218) | *“The app can only be recovered by manually restarting QwenPaw.”* 缺乏恢复机制。 |
| ✗ **自定义模型配置被破坏** | [#5378](https://github.com/agentscope-ai/CoPaw/issues/5378) | *“模型页面把新增模型的 endpoint 自动写入了查询框中，且删不掉，导致页面为空，无法使用。”* |
| ✗ **Cron 静默停止** | [#5398](https://github.com/agentscope-ai/CoPaw/issues/5398) | *“Cron scheduled jobs for one agent stopped firing even though the app process stayed alive.”* 无告警，难以排查。 |
| ✗ **Shell 特殊字符不能使用** | [#5373](https://github.com/agentscope-ai/CoPaw/issues/5373) | *“Simple commands like ls, pwd work, but any command containing shell special characters fails.”* |
| ✗ **移动端拖拽上传缺失** | [#5374](https://github.com/agentscope-ai/CoPaw/issues/5374) | *“On Chrome for Mac, drag-and-drop uploading does not work.”* 用户必须额外点击。 |
| ✗ **智能体与工作空间绑定过紧** | [#5392](https://github.com/agentscope-ai/CoPaw/issues/5392) | *“希望将智能体与工作空间解耦，使同一个智能体可以在不同工作空间中复用。”* 反映进阶用户定制需求。 |
| ✗ **切换对话卡死** | [#5354](https://github.com/agentscope-ai/CoPaw/issues/5354) | *“切换对话的时候，原对话会变灰切不回去。”* 表现为界面锁死。 |

**总体印象**：用户对基础功能（升级保留配置、消息隔离、进程稳定性）的期待值升高。对于新功能的尝试（消息队列）给予肯定，但期望更完善后再推出。管理员/重度用户越来越关注系统的可靠性和可维护性。

---

## 8. 待处理积压

> 以下 Issue/PR 长期开放且影响较大，建议维护者优先关注。

### 严重 Bug（高影响、未解决）
- **[#5218] 子Agent上下文压缩冻结**（06-16 创建，17 评论）  
  进程无响应需重启，无任何 PR 关联。建议尽快定位并修复，或至少增加 watchdog 自动恢复机制。 [→Issue](https://github.com/agentscope-ai/CoPaw/issues/5218)
- **[#5262] 升级后内置技能重置**（06-17 创建，9 评论）  
  已经是第二次报告同一类问题（首次 #4807 未完全解决）。应纳入升级测试用例。 [→Issue](https://github.com/agentscope-ai/CoPaw/issues/5262)

### 长期功能请求
- **[#2969] 个人知识库**（04-05 创建，👍2）  
  近 3 个月未有关联 PR，一直处于收集需求阶段。建议评估实现成本并列入路线图社区投票。 [→Issue](https://github.com/agentscope-ai/CoPaw/issues/2969)

### 待审查的重大 PR
- **[#4669] Tauri Auto Updater**（05-25 创建）  
  桌面端自动更新功能，已有一个月，仍为 Open 状态。该功能对桌面用户至关重要，建议加快审查。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/4669)
- **[#5193] Slack Channel 支持**（06-15 创建）  
  约 3500 行代码，大量模块新增，尚未有维护者正式 review。可能因复杂度高而延迟。 [→PR](https://github.com/agentscope-ai/CoPaw/pull/5193)

### 供应商兼容性问题
- **[#5330] 智谱 API 模型测试全部失败**（06-19 创建）  
  内置供应商无法使用，影响面大。建议优先排查模型名称路由逻辑。 [→Issue](https://github.com/agentscope-ai/CoPaw/issues/5330)
- **[#5345] 自定义 OpenAI 提供商 function calling 失效**（06-20 创建）  
  限制了用户使用 OMLX 等第三方服务，建议参考 Reasonix 的实现适配。 [→Issue](https://github.com/agentscope-ai/CoPaw/issues/5345)

---

*本期日报基于 2026-06-23 的 GitHub 活动数据自动生成。部分合并 PR 明细未公开列出，日报中的“项目进展”参考了关联 Issue 与活跃 PR 推测。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已经分析了 ZeroClaw (github.com/zeroclaw-labs/zeroclaw) 在 2026-06-23 的 GitHub 动态数据。现为您呈现项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-23

## 1. 今日速览

项目今日活跃度极高，但 PR 堆积问题进一步加剧，成为制约项目快速迭代的主要瓶颈。**今日净增 PR 积压 44 个（47 个待合并 vs 3 个已处理）**，已形成严重的“合并饥饿”现象，需引起维护团队高度重视。与此同时，社区关于安全、架构（Wasm 优先、插件系统）的深度讨论仍在进行，多个核心 Bug 的修复 PR 已排队等候。**整体评估：项目讨论活跃、开发行动密集，但交付周期面临阻塞风险。**

## 2. 版本发布

今日无新版本发布。项目自 `v0.8.1` 之后，正处于 `v0.8.3` 和 `v0.9.0` 两个重大版本的功能与修复密集开发期，无新版本发布属于预期内的开发阶段。

## 3. 项目进展

尽管合并效率不高，但社区贡献者的修复工作在持续进行，大量关键 Bug 的修复 PR 已提交并进入排队状态，预示着下一波合并浪潮将极大提升项目稳定性。

- **核心运行时稳定化**：来自 `mazhuima` 的多项修复正在排队，包括：
    - 修复工作线程并发导致会话历史 JSONL 持久化竞态条件的 PR [#7847](https://github.com/zeroclaw-labs/zeroclaw/pull/7847)。
    - 修复 Web 浏览器工具在 WebDriver 传输下快照返回空值问题的 PR [#7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908)。
    - 修复自动批准工具在非全自动模式下在频道中被错误限制的 PR [#7959](https://github.com/zeroclaw-labs/zeroclaw/pull/7959)。
    - 修复 `execute_pipeline` 子工具执行忽略代理级别 `ToolAccessPolicy` 的严重安全缺陷 PR [#7960](https://github.com/zeroclaw-labs/zeroclaw/pull/7960)。

- **会话生命周期增强**：PR [#8003](https://github.com/zeroclaw-labs/zeroclaw/pull/8003) 修复了 `session_end` Hook 从未被触发的 Bug，并增强了会话终止流程的完整性。

- **配置与实践指南加固**：PR [#8098](https://github.com/zeroclaw-labs/zeroclaw/pull/8098) 拒绝创建名为 `default` 的保留代理，防止了配置混乱。PR [#8002](https://github.com/zeroclaw-labs/zeroclaw/pull/8002) 修复了 OpenAI Codex JWT 令牌中 Account ID 的提取优先级问题。

## 4. 社区热点

今日最受关注的讨论集中在以下几个层面：

- **架构演进争议与共识**：Issue [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)（RFC: 原生动态链接库插件系统）和 [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)（RFC: Wasm 优先的插件运行时）是当前最受关注的两大 RFC。社区在“原生动态库 vs Wasm 沙箱”的默认插件路线上展开深入讨论。尽管 #7420 已关闭，但其争议性仍在发酵，这直接关系到 ZeroClaw 未来的安全模型和扩展性。

- **用户体验痛点引发共鸣**：Issue [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) 关于“默认 32k Token 上下文预算被系统提示和工具定义迅速耗尽”的严重 Bug，虽然已开启两个月，但仍在吸引新评论。用户抱怨该设计缺陷导致了“策略性预裁剪”的恶性循环，影响了核心体验。

- **MCP 工具集成受阻**：Issue [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) 报告了 MCP 工具在 TUI 会话中不可见的关键 Bug，但该 issue 在一天内被迅速标记为已关闭，彰显了项目对阻断性问题的快速响应能力，但其背后的深层原因（#7756）仍待解决。

## 5. Bug 与稳定性

今日报告的 Bug 呈现“阻断性”和“隐蔽性”并存的特点。

- **S0 - 数据丢失/安全风险**：
    - [#8013](https://github.com/zeroclaw-labs/zeroclaw/issues/8013) 禁用代理无法停止 Discord 频道响应（已关闭，表明已有修复方案）。

- **S1 - 工作流阻塞**：
    - [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) 默认 Token 预算不足导致循环裁剪（持续影响，无公开 fix PR）。
    - [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) MCP工具在 TUI 中缺失（已关闭，但可能存在根治性追踪）。
    - [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) 原生/MCP工具在特定 OpenAI/Anthropic 模型上不可用（持续影响，无 fix PR）。
    - [#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154) Kimi Code 端点 404 回归，严重阻断使用（新报告，无 fix PR）。

- **S2 - 性能退化**：
    - [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 平台 74 个测试失败（持续影响，无 fix PR，标志着跨平台兼容性短板）。

**今日新增 fix PR**：`mazhuima` 批量提交了针对工具执行策略、频道响应逻辑、浏览器工具等多项 fix PR，覆盖了多个高风险区域，一旦合并将显著改善稳定性。

## 6. 功能请求与路线图信号

用户和开发者对 ZeroClaw 的未来进化方向提出了清晰的诉求，指向更强的安全性和更好的开箱即用体验。

- **强安全与供应链**：
    - [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) 关于硬件 PGP 签名、可重现构建和 SLSA 溯源证明的 RFC，是项目安全方向的重要尝试。
    - [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135) Wasm 插件运行时 RFC 和 [#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132) 替换 React UI 为 Rust→Wasm 框架的 RFC，展现了项目决心消除 Node.js 依赖链、拥抱 Wasm 原生生态的路线图。

- **配置与体验优化**：
    - [#8134](https://github.com/zeroclaw-labs/zeroclaw/issues/8134) 请求为现有 `session_ttl_hours` 配置项补充实际实现，以自动化裁剪历史会话，这是个被频繁提及但一直缺失的功能。
    - [#8125](https://github.com/zeroclaw-labs/zeroclaw/issues/8125) 建议在 quickstart 中自动设置 `yolo` 风险配置，以匹配用户对“开箱即用”的期望，反映了新手用户与安全策略之间的冲突。
    - [#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) 支持 OpenRouter 的模型 fallback 数组，属于比较明确且实用的请求，很有可能被纳入。

- **频道集成深化**：
    - [#8046](https://github.com/zeroclaw-labs/zeroclaw/issues/8046) 请求为 Telegram 频道添加 Webhook 模式（长期轮询之外），增加部署灵活性。

## 7. 用户反馈摘要

从今日的评论和 Issue 描述中，可以透视用户的真实体验：

- **对核心机制缺陷的沮丧**：在 [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) 中，用户明确表示“the user here reported 130K tokens on iteration 0”，这表明默认 32K 的预算设计完全跟不上实际复杂场景，导致几乎所有新用户都可能立即遭遇性能瓶颈。

- **对配置生效机制的困惑**：在 [#8013](https://github.com/zeroclaw-labs/zeroclaw/issues/8013) 中，用户爆出“Even after disabling the agent in the config file, it was still answering users...”，说明配置热加载或状态管理存在严重逻辑 BUG，这严重侵蚀了用户对产品可靠性的信任。

- **对 MCP 体验割裂的抱怨**：在 [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) 中，用户反馈“gateway sees them but TUI sessions do not receive them”，这表明项目内部不同组件（Gateway vs TUI）之间的状态同步存在问题，导致用户在 UI 上看不到已经配置好并运行的工具，体验极差。

- **对平台兼容性的吐槽**：在 [#8075](https://github.com/zeroclaw-labs/zeroclaw/issues/8075) 中，MacOS 用户指出快捷键与系统全局键冲突，且过去存在终端按键被屏蔽的问题，这类细节反馈表明跨平台体验打磨仍有不小提升空间。

## 8. 待处理积压

- **关键 Bug 等待维护者确认与修复**：
    - [#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154) Kimi Code 端点回归（严重级别 S1），报告于 6 月 22 日，标注 `needs-maintainer-review`，但尚未有官方回复或指派。
    - [#8125](https://github.com/zeroclaw-labs/zeroclaw/issues/8125) 关于 quickstart 自动设置 yolo 风险的提案，同样处于 `needs-maintainer-review` 状态，等待决策。
    - 长期问题 [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 平台 74 个测试失败（严重级别 S2），从 6 月 10 日至今无可见进展，对正在拓展 Windows 用户群的项目构成隐患。

- **被阻塞的 PR 积压**：**47 个 PR 等待合并**，这是当前项目的最大风险点。大量高风险 Bug 修复（来自 `mazhuima` 和 `Nillth`）和新功能（来自 `singlerider`）均已提交，但未能进入 `master` 分支。这不仅降低了贡献者的积极性，也使得用户无法从这些修复中受益，变相延长了 Bug 的生命周期。**我们强烈建议维护者团队审视 PR 审查流程，优先处理风险评级高且已通过 CI 的修复性 PR，以快速止血。**

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*