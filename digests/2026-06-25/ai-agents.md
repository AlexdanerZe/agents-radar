# OpenClaw 生态日报 2026-06-25

> Issues: 439 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-25 02:54 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是为您生成的 OpenClaw 项目 2026-06-25 动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-25

## 今日速览

OpenClaw 项目今日极度活跃，Issue 与 PR 更新数量均高达 439 条和 500 条，社区参与度与维护工作量均处高位。两个新版本的发布（v2026.6.11-beta.1, v2026.6.10）带来了强化频道控制、自动快速模式等关键改进。然而，大量关于会话状态丢失、安全与子智能体协作的 Bug 报告（如 #88838, #22676）提示核心稳定性和错误处理路径仍是当前版本的显著短板。社区对跨平台支持、安全管理细粒度的呼声依然很高。

## 版本发布

过去24小时内发布了两个新版本：

- **v2026.6.11-beta.1** (beta 版本)
  - **主要亮点：** 显著增强了频道控制能力。新增了 Slack 中继模式、原生 Mattermost 命令 (`/oc_queue`) 以及每 DM 模型覆盖功能，使得频道运维的自动化和精细调优更加便捷。
  - **链接：** openclaw/openclaw Releases (请根据实际仓库链接查找)

- **v2026.6.10**
  - **主要亮点：** 引入了对话的自动快速模式（`Automatic fast mode`），系统可针对简短对话轮次自动启用快速模式，而在长对话中回退到正常模式，并具有有界的回退和交付行为。此外，改进了模型路由的可靠性。
  - **链接：** openclaw/openclaw Releases (请根据实际仓库链接查找)

## 项目进展

- **关键 Bug 修复与功能推进：**
  - **LINE 频道文件处理：** PR #96616 (已合并) 修复了 LINE 频道中音频文件 MIME 类型检测失败的问题，增强了对文件消息的处理能力。
  - **IRQ 消息分片：** PR #96572 修复了 IRC 频道在分片长消息时可能因 UTF-16 边界导致产生“孤立代理项”（lone surrogates）的问题，提升了消息编码的健壮性。
  - **Telegram 群组/主题回复：** PR #96550 解决了 Telegram 群组主题中，因会话冲突导致回复“卡住”的故障，通过退避重试策略提高了消息传递的可靠性。
  - **子智能体生命周期管理：** PR #95996 (XL级) 旨在修复“父会话在子智能体未完成前就被视为结束”的问题，解决了 CRON 和 Discord 等场景中因事件推断不准确导致的完成丢失问题。

## 社区热点

- **#75 - Linux/Windows Clawdbot Apps (109 评论 | 80 👍):**
  - 持续是整个项目中最受关注的话题，用户强烈渴望跨平台桌面客户端支持，尤其是 Linux 和 Windows。
  - **链接：** [openclaw/openclaw Issue #75](https://github.com/openclaw/openclaw/issues/75)

- **#88838 - Track core session/transcript SQLite migration via accessor seam (36 评论):**
  - 围绕 SQLite 持久化层迁移的技术讨论十分热烈，属于核心架构重构。用户和开发者们正就如何在保证稳定性的前提下，通过“accessor seam”模式逐步替换核心存储进行深度讨论。
  - **链接：** [openclaw/openclaw Issue #88838](https://github.com/openclaw/openclaw/issues/88838)

- **#22676 - Signal daemon stop() race condition (17 评论):**
  - 用户报告了一个棘手的并发错误：Signal 网关重启时因未等待旧进程退出，导致进程孤儿、端口与文件锁冲突，造成消息发送失败。此问题触及核心稳定性，受到社区高度关注。
  - **链接：** [openclaw/openclaw Issue #22676](https://github.com/openclaw/openclaw/issues/22676)

## Bug 与稳定性

- **严重与紧急问题：**
  1. **#22676 (P1):** Signal 网关的竞态条件导致进程崩溃和消息发送失败。尚无直接修复 PR。
  2. **#31583 (P1, Regression):** `exec` 工具无法继承配置的环境变量，导致密码等敏感信息无法注入，影响安全和工作流可靠性。尚无直接修复 PR。
  3. **#29387 (P1):** 放置在代理目录中的引导文件（Bootstrap files）被忽略，迫使所有文件共享同一上下文窗口，浪费 Token。尚无直接修复 PR。
  4. **#32473 (P1, Regression, Security):** Docker 部署下控制 UI 因非 HTTPS/本地环境而要求“设备身份”，导致无法访问，对远程部署影响很大。
  5. **#40001 (P1):** “写入”工具无追加模式，导致隔离的 CRON 任务之间覆盖共享文件，造成数据丢失。已有大型 PR #77127 解决此问题。
  6. **#48003 (P1):** “Steer”模式无法在对话中途注入消息，严重影响了人机交互的实时性和控制感。
  7. **#95833 (P1):** 子智能体超时中止后未能释放文件锁，导致会话永久性“卡死”，这是一个严重的资源泄露与状态损坏问题。

- **关联修复 PR 的 Bug：**
  - #40001 (数据丢失) -> 已有 PR #77127 (大幅重构，待合并)。
  - #89994 (编辑工具模糊匹配) -> 已有 PR #96636 用于修复。
  - #93141 (代码使用量UI) -> 已有 PR #95317 在维护者审查中。

## 功能请求与路线图信号

- **安全与权限增强：**
  - **#6615 (Exec 黑名单):** 要求在命令行执行审批中增加黑名单功能，实现“允许一切，除 X 外”的安全策略，获得了社区 7 个 👍。
  - **#39979 (路径级权限):** 提议用基于路径的读/写/执行（RWX）权限映射替换当前的二进制级审批列表，更像 Unix DAC。
  - **#12678 (基于能力的权限):** 提议在技能/工具层面建立默认拒绝的高危操作权限模型。
  - 这些诉求表明，用户对当前安全模型感到不足，希望获得更精细、更灵活的控制。

- **跨平台与部署：**
  - **#75 (Linux/Windows 桌面端):** 持续热门，表明这仍是不可忽视的核心战略需求。
  - **#86881 (Gateway-lite 模式):** 需要一个不集成 AI 的轻量级网关，用于仅需路由、调度等确定性任务，反映了对架构解耦和部署多样性的需求。

- **扩展性与管理：**
  - **#13616 (备份/恢复工具):** 用户强烈需要标准化的配置、任务和会话历史备份恢复方案，以应对灾难恢复和环境迁移。
  - **#22438 (分级引导文件加载):** 提出根据工作区大小分层的文件加载策略以节省 Token，是提升效率和降低成本的明智建议。

## 用户反馈摘要

- **核心痛点：** 配置复杂、文档不足、内存泄漏和升级后兼容性问题。
  - 用户 `Tanklive` 报告 [#87109] Gateway 空闲时内存泄漏达到 1GB+，导致 CRON 任务静默失败，强调“**静默失败**”是最令用户愤怒的问题。
  - 用户 `fenglanhua` 报告 [#95495] 版本升级后，记忆存储被“**静默搬迁**”，导致 1499 个文件需要重新嵌入，且无任何升级警告，严重影响了用户体验和对升级的信任。
  - 用户 `richwilson-bloom` 报告 [#95833] 子智能体卡死后，恢复的唯一方法是手动重启，并批评“**Something went wrong**”这类通用错误信息缺乏诊断价值。
- **满意之处：** 新的自动快速模式 (#85104) 和更丰富的频道控制 (#94707, #95546) 普遍受到好评，展示了项目在对齐 Real-time 使用场景方面的努力。
- **典型场景：** 用户 `882soft` 描述其在拥有大量文件的工作区中使用场景，期望通过分级加载引导文件来精细控制智能体的上下文窗口（#22438）。

## 待处理积压

- **高关注度但等待维护者决策/审查的 Issues：**
  - **#75 (跨平台PC端)**: 评论最多 (109)，但状态为 `needs-product-decision` 和 `needs-maintainer-review`，维护者尚未给出明确路线图回应。
  - **#6615 (Exec 黑名单), #12678 (技能权限模型), #7722 (文件系统沙箱配置)**：这些旨在提升安全性的功能请求均已有较完善的方案讨论，但都标记为 `needs-product-decision` 或 `needs-maintainer-review`，建议维护方优先评估，以回应社区对安全控制日益增长的需求。
- **等待用户/测试人员反馈的 PR：**
  - **#44143 (序列化消息交付):** 已标记为 `⏳ waiting on author`，需要提交者补充测试验证或证据。
  - **#96316 (修复安装错误 `node-domexception`)**：同样标记为 `⏳ waiting on author`，该 PR 对上游构建阻碍很大，需尽快推动。

---

## 横向生态对比

以下是为您生成的横向对比分析报告，基于2026-06-25各项目的社区动态。

---

# AI 智能体与个人 AI 助手开源生态横向对比分析报告（2026-06-25）

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处在 **“密集功能迭代 + 安全隐患爆发 + 运营成本觉醒”** 的三期叠加阶段。核心项目日均处理数百条 Issue/PR，社区参与度极高，但大量稳定性 Bug（会话状态丢失、子智能体卡死、Token 浪费）表明工程化成熟度仍有差距。安全方面，多个项目集中披露了 SSRF、命令注入、权限绕过等漏洞（尤其 PicoClaw、NanoClaw、OpenClaw），生态正在集体补安全课。与此同时，跨平台支持、MCP 远程化、Token 优化、多租户等方向已形成多项目共识，预示着下一阶段将向企业级和广域部署演进。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issue 动态 | 今日 PR 动态 | 新版本发布 | 健康度/活跃度评估 |
|------|----------------|-------------|-----------|-------------------|
| **OpenClaw** | 更新 439 条 | 更新 500 条 | 2 个（beta + stable） | 极高活跃，但社区 Bug 集中，稳定性短板明显 |
| **NanoBot** | 11 条（3 关闭） | 41 条（12 合并） | 0 | 高活跃，社区贡献力强，响应迅速 |
| **Hermes Agent** | 更新 50 条 | 更新 50 条（10 合并/关闭） | 0 | 高活跃，Token 优化和编排讨论引领社区 |
| **PicoClaw** | 13 个历史 Issue 关闭（安全类） | 8 个新提交/更新，0 合并 | 0 | 高活跃，但处于安全修复周，功能迭代暂停 |
| **NanoClaw** | 1 新 Issue | 18 个（2 合并/关闭） | 0 | 极高活跃，密集开发与修复并行 |
| **IronClaw** | 更新 19 条（3 关闭） | 更新 45 条（18 合并/关闭） | 0 | 极高活跃，生产事故驱动紧急修复，迭代快 |
| **LobsterAI** | 近乎静默（仅 1 stale 刷新） | 43 条（41 合并/关闭） | 0 | 修复冲刺型活跃，核心开发集中处理技术债 |
| **TinyClaw** | 0 | 1 个合并 | 0 | 低活跃，仅完成跨平台兼容修复 |
| **CoPaw (QwenPaw)** | 25 条 | 50 条（7 合并/关闭） | 0 | 极高活跃但合并率低（14%），架构升级阵痛期 |
| **ZeroClaw** | 47 条（1 关闭） | 50 条（5 合并/关闭） | 0 | 极高活跃，多租户和 WASM 生态讨论密集 |
| **NullClaw / Moltis / ZeptoClaw** | 0 | 0 | 0 | 无活动，处于休眠或观察期 |

> **注**：OpenClaw、Hermes Agent 等给出的数字为“更新数量”，包含评论、状态变更等，非纯新建；其余为明确新建/关闭统计。横向对比需考虑口径差异，但量级足以反映活跃程度。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 凭借**全栈功能覆盖（多通道、子智能体、技能系统、安全管理）** 和长期迭代积累，是当前生态的 **“功能参照系”** 。其优势在于：
- **Channel 集成广度**（Slack、Mattermost、Telegram、LINE、IRC 等），远多于 NanoBot、Hermes Agent 等；
- **社区规模最大**：单日 Issues + PR 更新近千条，远超其他项目；
- **发布节奏稳定**：同时维护 Beta 和 Stable 版本。

但问题同样突出：
- **核心稳定性不足**：大量 P1 Bug（会话丢失、子智能体卡死、Token 泄漏）暴露了复杂架构下的质量代价；
- **配置复杂度高**：社区多次抱怨文档不足、升级静默迁移数据；
- **产品决策滞后**：跨平台桌面端（#75）、Exec 黑名单（#6615）等高赞请求长期悬而未决。

相比之下，**Hermes Agent 更聚焦编排抽象**、**NanoBot 主打超轻量**、**ZeroClaw 押注 WASM 插件化**，它们在某些维度上比 OpenClaw 走得更极致，但整体生态位尚未超越 OpenClaw 的“中央枢纽”角色。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 代表诉求 |
|----------|----------|----------|
| **Token / 成本优化** | OpenClaw、Hermes Agent、IronClaw、LobsterAI | 惰性工具 Schema 加载、分析 Token 开销、空闲循环终止 |
| **跨平台桌面端** | OpenClaw (#75)、Hermes Agent (Windows 乱码)、TinyClaw (Windows 原生支持)、NanoBot (PWA 呼声) | Linux/Windows 原生客户端或 PWA 支持 |
| **安全加固与权限模型** | PicoClaw (批量 CVE)、ZeroClaw (多租户 RBAC、API Key 泄漏)、OpenClaw (Exec 黑名单)、NanoClaw (CVE-2026-29611) | 细粒度权限、安全策略委托、路径级控制 |
| **MCP 生态扩展** | NanoBot (MCP 超时/资源控制)、NanoClaw (远程 MCP over HTTP)、ZeroClaw (WASM-first 插件运行时) | 远程 MCP 服务器、MCP 安全门控、WASM 组件模型 |
| **子智能体 / 委托机制** | OpenClaw (#95833、#95996)、ZeroClaw (#8285 安全隔离)、Hermes Agent (#52260 超时预算) | 生命周期管理、权限继承、超时与资源隔离 |
| **消息通道兼容性** | OpenClaw (LINE/Telegram/IRC 修复)、NanoBot (Telegram Web、钉钉)、IronClaw (Discord 网关) | 富文本兼容、群组/私聊区分、媒体组处理 |
| **模型提供商扩展** | CoPaw (自定义 OpenAI、GLM、MiniMax)、LobsterAI (Minimax M3、Mimo)、Hermes Agent (z.ai 限流) | 更多兼容接口、BYOK 配置稳定性 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|-----------------|
| **OpenClaw** | 全功能个人 AI 助手，多通道中枢 + 子智能体 + 技能系统 | 高级个人用户、团队协作 | 插件化通道、SQLite 持久化、事件驱动网关 |
| **NanoBot** | 超轻量聊天机器人，快速部署 | 个人开发者、轻量使用 | Node.js 单进程、MCP-first、极简配置 |
| **Hermes Agent** | AI 编码代理编排，IDE 集成 | 开发者、编码场景 | ACP 客户端、OAuth 认证、工具惰性加载 |
| **PicoClaw** | 嵌入式/GUI Agent，网页操控 (PageAgent) | 企业自动化、前端测试 | Rust 核心、Vue/React 适配、WebSocket 远程模式 |
| **NanoClaw** | 安全的容器化机器人分支 | 安全敏感、多实例用户 | Docker-in-Docker、CVE 快速修复、Telegram 多 Bot |
| **IronClaw** | 生产级 AI 智能体平台，记忆层可插拔 | 企业、平台团队 | Rust+WASM、Reborn 内存系统、NEAR AI 集成 |
| **LobsterAI** | 桌面 AI 助手，偏向 IDE 和办公自动化 | 个人办公用户、网易生态 | 与 OpenClaw 同源但聚焦 Windows 体验、定时任务 |
| **TinyClaw** | 极简 CLI AI 助手 | CLI 爱好者、脚本集成 | 单文件、最小依赖、Node.js |
| **CoPaw (QwenPaw)** | 模型兼容性优先，AgentScope 生态 | 多样模型用户、研究者 | AgentScope 2.0 架构、DashScope/GLM 深度适配 |
| **ZeroClaw** | 下一代安全沙箱 + WASM 插件 | 高阶用户、安全工程师 | WASM 组件模型运行时、多租户 RBAC、供应链签名 |

---

## 6. 社区热度与成熟度分层

- **快速迭代期（功能驱动）**：OpenClaw、ZeroClaw、NanoClaw、CoPaw  
  特征：每日大量新功能 PR、架构讨论活跃，但稳定性 Bug 同步积压，合并率可能偏低（CoPaw 仅 14%）。

- **修复冲刺与质量巩固期**：PicoClaw、LobsterAI、IronClaw  
  特征：近期生产事故或安全事件驱动，短期大量合入修复 PR，功能迭代暂时让位。

- **稳定增长期**：NanoBot、Hermes Agent  
  特征：既有新功能（MCP 增强、技能子目录）也有 Bug 修复，合并率较高（NanoBot 12/41 ≈ 29%），社区讨论质量高。

- **低活跃/维护期**：TinyClaw  
  特征：仅按需修复关键兼容性，无长期路线图讨论。

- **休眠**：NullClaw、Moltis、ZeptoClaw  
  特征：零活动，建议关注是否存在分支复活计划。

---

## 7. 值得关注的趋势信号

1. **Token 节俭已成为刚需，驱动架构创新**  
   Hermes Agent #6839（惰性工具 Schema）获得 14 👍；IronClaw PR #5149 同样提出逐步暴露工具（可节省 25.8K tokens/调用）。这表明 **LLM API 成本压力正迫使开发者从“功能全”转向“调用精”**。

2. **安全左移，但漏洞披露速度远超修复合并**  
   PicoClaw 批量关闭 10 个安全 Issue，但相应的修复 PR 无一合并；NanoClaw CVE 修复合并后仍有 #2800/#2802 等高危补丁等待。**社区安全贡献者积极，但维护侧审查滞后成为瓶颈。**

3. **跨平台桌面端长期缺失，用户耐心消耗**  
   OpenClaw #75（80 👍）已存在数月，仍为 `needs-product-decision`。NanoBot 用户转向请求 PWA。**桌面端已成社区核心痛点，缺乏官方原生客户端可能失去用户向 Copilot 等闭源方案迁移。**

4. **WASM 插件生态初现端倪，可能重塑扩展性**  
   ZeroClaw 围绕 WASM 组件模型提交了 5+ 个 RFC 和实现 PR（#6943、#7497、#8135 等），指向“插件 OCI 分发 + 能力门控”体系。若落地，将与其他项目的“脚本技能”体系形成代差。

5. **多租户与企业级权限管理需求信号强烈**  
   ZeroClaw #5982（Per-sender RBAC）、OpenClaw #39979/#12678（路径权限、能力模型）均获得较高关注。**随着代理从个人工具走向团队协防，权限隔离将成为必有功能。**

6. **模型提供商碎片化，适配成本持续上升**  
   CoPaw 社区报告了 GLM、MiniMax、自定义 OpenAI 接口等多起集成失败；LobsterAI 需在每次更新中维护模型配置。**一个“写一次跑多家”的 Provider 抽象层可能成为生态统一方向。**

7. **AI 自主性的边界在社区中被反复讨论**  
   审批流程断裂（IronClaw #5192、#5196）、子智能体资源耗尽（OpenClaw #95833、Hermes Agent #52260）等反馈表明：**社区正在从“让 Agent 做更多”转向“如何在可控范围内让 Agent 做更多”。**

---

*报告基于 2026-06-25 各项目 GitHub 公开数据，由 AI 自动整理生成。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，以下是为您生成的 NanoBot 项目动态日报，日期为 2026-06-25。

---

## NanoBot 项目动态日报 | 2026-06-25

### 1. 今日速览

今日项目活跃度极高，社区贡献力度强劲。过去24小时内，共处理了11条Issue和41条Pull Request，其中3个Bug被关闭，12个PR被合并。尽管没有新版本发布，但项目在渠道兼容性修复、MCP（模型上下文协议）功能增强以及新集成（如 Mattermost）方面取得了显著进展。社区围绕“超轻量”项目定位、Telegram Web兼容性等问题展开了深入讨论，开发团队响应迅速。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日多项关键修复和功能增强被合并或关闭，项目整体向前迈出了坚实一步。主要集中在渠道稳定性、AI代理核心功能优化以及MCP生态完善上。

- **Telegram Web 兼容性修复**：PR [#4505](https://github.com/HKUDS/nanobot/pull/4505) **(已合并)** 已修复因新版富消息功能导致的 Telegram Web 端消息无法显示的问题。合并关闭了 Issue [#4488](https://github.com/HKUDS/nanobot/issues/4488)。这是针对当日高优先级Bug的快速响应，解决了关键渠道的可用性问题。
- **钉钉（DingTalk）渠道优化**：针对 Issue [#4497](https://github.com/HKUDS/nanobot/issues/4497) 报告的富文本格式丢失和HTTP超时问题，修复PR [#4501](https://github.com/HKUDS/nanobot/pull/4501) 正在待合并状态，预计将提升钉钉渠道的稳定性。
- **核心代理功能增强**：来自贡献者 `yu-xin-c` 的一系列“Codex”增强PR（如 [#4416](https://github.com/HKUDS/nanobot/pull/4416), [#4415](https://github.com/HKUDS/nanobot/pull/4415), [#4424](https://github.com/HKUDS/nanobot/pull/4424)）仍在持续迭代中，加入了定时任务模型预设、子代理模型覆盖、记忆归档溯源等功能，这些能力将显著增强代理的自动化与定制化能力。
- **MCP 安全与资源管理**：PR [#4436](https://github.com/HKUDS/nanobot/pull/4436) 和 [#4452](https://github.com/HKUDS/nanobot/pull/4452) 修复了 MCP 服务器 `enabledTools` 访问控制列表未对资源（Resources）和提示（Prompts）生效的安全问题，增强了MCP调用的安全性。

### 4. 社区热点

本周社区讨论集中在两个核心议题上，反映出用户对项目透明度和渠道体验的深切关注。

- **“超轻量”项目定位的争议**: Issue [#660](https://github.com/HKUDS/nanobot/issues/660) 是长期热点，尽管创建于数月前，但仍收到了5个点赞和11条评论。用户 `besoeasy` 质疑项目自称“超轻量”却又依赖 Node.js 的矛盾之处。这反映了社区对项目技术栈透明度和明确宣传的高度重视，开发者需要就此给出更清晰的解释或优化方案。
- **Telegram Web 兼容性问题**：Issue [#4488](https://github.com/HKUDS/nanobot/issues/4488) 引发了关于“富消息”功能回退的讨论。负责修复的 PR [#4489](https://github.com/HKUDS/nanobot/pull/4489) 和 [#4505](https://github.com/HKUDS/nanobot/pull/4505)(已合并）均围绕此问题展开，显示了社区对多端一致体验的强烈诉求。

### 5. Bug 与稳定性

今日报告的Bug主要集中在iOS的WebUI界面和具体的消息渠道上。大部分已有关联的修复PR，项目维护状态良好，响应迅速。

| 严重程度 | Issue | 描述 | 状态 & 关联PR |
| :--- | :--- | :--- | :--- |
| **中** | [#4500](https://github.com/HKUDS/nanobot/issues/4500) | WebUI 首页发送不导航，自重启导致流式传输卡死，停止按钮无效 | **OPEN**，影响核心Web交互体验，需重点关注 |
| **中** | [#4465](https://github.com/HKUDS/nanobot/issues/4465) | WebUI 将 AI 模型的 `<thinking>` 标签渲染为可见文本 | **CLOSED**，已有修复 |
| **中** | [#4488](https://github.com/HKUDS/nanobot/issues/4488) | Telegram Web 收到“不支持此消息”提示（富媒体功能导致） | **FIXED**，PR [#4505](https://github.com/HKUDS/nanobot/pull/4505) 已合并 |
| **低** | [#4497](https://github.com/HKUDS/nanobot/issues/4497) | 钉钉渠道富文本丢失和HTTP超时 | **FIX PENDING**，PR [#4501](https://github.com/HKUDS/nanobot/pull/4501) 待合并 |
| **低** | [#4499](https://github.com/HKUDS/nanobot/issues/4499) | Telegram 渠道发送空消息，但Bot API 直接调用正常 | **CLOSED**，已解决或定位到根本原因 |

### 6. 功能请求与路线图信号

用户提出的新功能请求内容丰富，其中大部分已经有了对应的实现PR，显示出极强的社区贡献力。这些特性很可能被纳入下一版本，预示着 NanoBot 正从单一聊天机器人向更完善的AI工作平台演进。

- **WebUI PWA支持与手势优化**：Issue [#4479](https://github.com/HKUDS/nanobot/issues/4479) 请求添加PWA支持和移动端侧滑菜单手势。
- **MCP服务器空闲超时**：PR [#4506](https://github.com/HKUDS/nanobot/pull/4506) 实现了 MCP 服务器的空闲超时自动关闭，以防止资源泄露，此增强几乎肯定会被合并。
- **Gateway Webhook触发器**：PR [#4502](https://github.com/HKUDS/nanobot/pull/4502) 提议为 Gateway 添加 Webhook 触发功能，旨在让外部系统能够通过 HTTP 请求唤醒代理，大大扩展了 API 的集成能力。
- **Mattermost 渠道集成**：PR [#4459](https://github.com/HKUDS/nanobot/pull/4459) 为 NanoBot 增加了对 Mattermost 这一开源办公通讯平台的支持，满足了团队协作场景的需求。
- **技能子目录支持**：PR [#4504](https://github.com/HKUDS/nanobot/pull/4504) 允许用户将 `skills` 放入子目录管理，对于拥有大量自定义技能的开发者来说，这是一项重要的可用性改进。

### 7. 用户反馈摘要

- **PWA支持呼声高**：在 Issue [#4479](https://github.com/HKUDS/nanobot/issues/4479) 的评论中，用户表达了对 WebUI PWA 支持的强烈需求，希望获得“类似原生应用的体验”，这表明移动端使用场景正在快速增长。
- **“超轻量” vs “Node.js依赖”**：Issue [#660](https://github.com/HKUDS/nanobot/issues/660) 的讨论热度不减，用户普遍认为“超轻量”是一个关键卖点，支持 Node.js 虽然带来了功能扩展，但也让这一定位受到质疑。社区希望开发团队能澄清这一选择背后的技术考量。
- **用户痛并快乐着**：在 [#4488](https://github.com/HKUDS/nanobot/issues/4488) 中，用户报告了 Telegram Web 的兼容性问题，但同时也认可在 App 端体验良好。这反映了项目在积极跟随 Telegram API 更新时，对不同客户端版本的分化测试有待加强。

### 8. 待处理积压

- **项目定位矛盾**：Issue [#660](https://github.com/HKUDS/nanobot/issues/660) 已经开放超过4个月，获得大量关注（5👍）。虽然是一个“Feature Request”，但它本质是项目核心定位的争议。建议维护者在此Issue下正式回应，说明依赖 Node.js 的技术路线图，或考虑提供 Python-only 的运行模式，以消除社区疑虑。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是为您生成的 **Hermes Agent 项目动态日报**，数据基于 2026-06-24 至 2026-06-25 的 GitHub 活动。

---

# Hermes Agent 项目动态日报 | 2026-06-25

## 今日速览

过去 24 小时内，Hermes Agent 项目保持高度活跃。Issue 和 PR 的更新数量均达到 50 条，社区参与度极高，围绕性能优化（Token 开销）和平台兼容性（Windows、Discord）的讨论占据主流。虽然暂无新版本发布，但项目合并了多项关键修复，尤其是在认证、桌面端性能和网关稳定性方面取得了明显进展。值得注意的是，有大量代码重构（移除无用 f-string）的 PR 被积压，表明项目正在进行深入的代码质量清理工作。

## 版本发布

- **无**：过去 24 小时内无新版本发布。

## 项目进展

过去 24 小时共有 10 个 PR 被合并或关闭，主要集中在 Bug 修复和中期重构。

- **核心稳定性修复（PR #52270）**：修复了 `NOUS_INFERENCE_BASE_URL` 环境变量在 OAuth 会话中不生效的问题，这对于开发和预发布环境的对接至关重要。
- **桌面端性能改进（PR #52273）**：解决了 `/learn` 命令在处理大文件或目录时导致桌面应用挂起或崩溃的问题，通过限制工具结果渲染范围提升了用户体验。
- **网关与消息可靠性修复（PR #52263）**：修复了私信（DM）回复因缺少 `guild_id` 而无法解析租户导致发送失败的问题，提高了消息中继的可靠性。
- **终端工具修复（PR #50636）**：解决了在 Docker 后端环境下，`cwd` 路径因包含主机特定前缀而被错误传递的问题。
- **基础设施与代码质量（多个 PR）**：批量合并了多组旨在移除无用 `f-string` 前缀的代码重构（Batch 2-6, #52258, #52262, #52268, #52269, #52274），共清理了超过 400 处此类冗余，提高了代码的可读性和微小性能。

## 社区热点

1.  **#6839 [Lazy Tool Schema Loading]** (评论: 28, 👍: 14)
    这是过去 24 小时内讨论最热烈的议题。核心诉求是：当前系统会将所有启用工具的完整 Schema 注入到每次 API 调用中，导致巨大的 Token 浪费（约 3500-5000 tokens/ call）。社区用户`jarviszomine`提出了一种“两遍式工具注入”方案，旨在按需加载，极大优化 Token 开销，尤其利好本地模型用户。
    **诉求分析**：社区对 **降低运营成本** 和 **提升本地模型可用性** 的呼声极高。这是目前社区最希望被采纳的优化方向之一。
    [NousResearch/hermes-agent Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839)

2.  **#4379 [Token Overhead Analysis]** (评论: 16)
    作为 #6839 的配套分析，用户 `Bichev` 通过构建仪表盘详细分析了 Token 消耗，发现高达 73% 的 API 调用量为固定开销（~13.9K tokens）。这个数据为 #6839 的提案提供了强有力的数据支持。
    **诉求分析**：社区希望自动化与优化能够建立在 **量化分析** 的基础上，而非仅凭直觉。
    [NousResearch/hermes-agent Issue #4379](https://github.com/NousResearch/hermes-agent/issues/4379)

3.  **#5257 [Generalized ACP Client]** (评论: 11, 👍: 16)
    一个非常受关注的功能提议，希望将 Hermes 当前特定于 Copilot 的 ACP 客户端通用化，使其能编排所有兼容 ACP 的编码智能体，如 **Claude Code**。
    **诉求分析**：社区希望 Hermes 成为一个 **中心化的智能体编排平台**，而非仅仅是某个特定服务的客户端。
    [NousResearch/hermes-agent Issue #5257](https://github.com/NousResearch/hermes-agent/issues/5257)

## Bug 与稳定性

今日报告的 Bug 中，平台兼容性和网关稳定性问题较为突出。

- **P1 (严重) :**
    - **#52212 [非编辑平台静默丢弃消息]**：在 QQ、微信、Signal 等不支持 `edit_message` 的平台上，所有工具调用进度消息会在用户不知情的情况下被丢弃。
        - *状态：* 有 Issue 但无关联修复 PR。
        - [NousResearch/hermes-agent Issue #52212](https://github.com/NousResearch/hermes-agent/issues/52212)
    - **#19566 [OpenAI-Codex 凭据池丢失凭证]**：在凭据轮换期间，由于文件重写逻辑的竞态条件，可能导致新添加的认证凭据被意外删除。
        - *状态：* 有 Issue 但无关联修复 PR。
        - [NousResearch/hermes-agent Issue #19566](https://github.com/NousResearch/hermes-agent/issues/19566)
    - **#52197 [Discord 网关事件循环阻塞]**：网关在进行缓存清理时长时间持有锁，导致 Discord 的异步事件循环被阻塞，心跳超时，最终掉线。
        - *状态：* 有 Issue 但无关联修复 PR。这是一个高优先级回归问题。
        - [NousResearch/hermes-agent Issue #52197](https://github.com/NousResearch/hermes-agent/issues/52197)

- **P2 (中等) :**
    - **#50663 [z.ai 速率限制]**：`z.ai` 提供商会主动对 Hermes Agent 进行限流，影响正常使用。
        - *状态：* 有 Issue 但无关联修复 PR。
    - **#33801 [秘密涂改功能破坏代码语法]**：用于打码 API Key 的秘密替换系统，在替换时会破坏 Python / Shell 语法，导致工具执行失败。
        - *状态：* 有 Issue 但无关联修复 PR。
    - **#52260 [子代理终端超时预算]** (PR #52260)：已有关联 PR，旨在限制委派的子代理终端运行时不超过设定的超时预算，防止资源耗尽。该 PR 今日已提交。
    - **#52272 [推理模型超时误导性建议]** (PR #52272)：已有关联 PR，旨在改进 `reasoning model` 超时后的错误提示，避免给出不恰当的写文件建议。该 PR 今日已提交。
    - **#52160 [双次压缩后适配器错误]**：会话被压缩两次后，向 Anthropic 发送 API 请求时，第一条消息角色错误（`assistant` 而非 `user`），导致 HTTP 400 错误。
        - *状态：* 有 Issue 但无关联修复 PR。
    - **#52244 [Windows 端消息截断乱码]**：Hermes Desktop 更新后，在 Windows 上输出消息被截断、乱码，疑似 UTF-8 编码问题。
        - *状态：* 有 Issue 但无关联修复 PR。

- **P3 (较低) :**
    - **#52255 [桌面端远程模式认证失败]**：桌面客户端在连接已认证的远程网关时卡死。
    - **#36216 [Hindsight 丢数据]**：内存插件在会话结束时，如果保留轮次计数未达阈值，会静默丢失缓冲区内的对话数据。

## 功能请求与路线图信号

1.  **Token 优化已成共识**：`#6839` 和 `#4379` 的超高热度明确表明，**降低 Token 开销**是社区当前最迫切的功能需求。这是影响所有用户使用成本和体验的核心痛点，预计将在后续版本中被优先考虑。
2.  **更灵活的内存与配置系统**：`#47349`（可配置内存后端）、`#42864`（scope-recall 内存提供器）和 `#51069`（支持项目级 `.mcp.json`）等请求反映了用户期望更灵活的上下文管理和外部集成能力。`#42864` 的作者已提交了相关文档 PR (`#52257`)，这是一个强烈的信号。
3.  **智能审批模式改进**：`#46544` 指出 `smart` 审批模式会忽略用户的主动授权，导致管理员也被阻塞。这暴露了当前权限模型的缺陷，需要进行调整以平衡安全与易用性。
4.  **新平台集成**：`#3725`（Rocket Chat 支持）虽然评论不多，但有 10 个👍，表明对扩展消息通道的需求依然存在。

## 用户反馈摘要

- **痛点聚焦**：用户普遍对 **高昂的 Token 消耗** 表示关注，这被认为是当前版本最大的痛点。此外，**与 OpenAI Codex CLI 的兼容性问题**（#13834）和 **z.ai 的限流**（#50663）也造成了严重的负面体验。
- **平台体验反馈**：Windows 桌面端用户在更新后遇到了 **消息乱码**（#52244）和 **更新管理器僵死**（#44515）等问题，表明该平台在发布前的测试覆盖度可能不足。
- **开发者体验**：对于高级用户和开发者，**配置灵活度不够**（如无法禁用 memory.md）和 **外部工具整合困难**（MCP 配置不兼容）是主要吐槽点。
- **正面反馈**：社区对 `Hindsight` 等第三方插件（#42864）和 `delegate_task_stream`（#9556）等高级编排功能表现出兴趣，说明功能框架具有吸引力，但稳定性和兼容性是瓶颈。

## 待处理积压

以下 Issue 和 PR 持续未决，需要维护者关注：

1.  **#6839 [Lazy Tool Schema Loading]**：虽然讨论热烈，但状态停滞在 `needs-decision`。作为社区最期望的功能，此决策需要尽快明确以指导后续开发。
2.  **#22648 [Ollama Cloud Provider]**：该 PR（2026-05-09 创建）因架构变更导致冲突频发，虽然作者已尽力 rebase，但仍处于 `OPEN` 状态。建议分配内部人员协助审查，避免社区贡献流失。
3.  **#8427 [Vertex AI Provider]**：类似 #22648，一个重要的企业级功能（2026-04-12 创建）长期未合并，可能信号是内部优先级不同，但应主动沟通或关闭。
4.  **#4379 [Token Overhead Analysis]**：作为 #6839 的数据基础，此 Issue 提供了极具价值的量化分析。维护团队可将其标记为 `accepted` 或 `roadmap`，以回馈社区的积极贡献。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是为您生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-25

## 1. 今日速览

项目今日进入 **高风险修复周** 尾声，维护活动高度集中。过去24小时内，项目团队关闭了13个历史Issue，其中绝大多数为近期披露的安全漏洞报告，表明项目正在集中精力进行安全加固。PR方面，有8个新提交/更新的修复与功能PR正在等待合并，但暂无合并操作，显示出团队在代码审查上持谨慎态度。整体来看，项目活跃度极高，但主要体现为对安全事件的快速响应和Bug修复，而非大型功能迭代。

- **活跃度评估**：非常活跃 (High Activity)。安全事务处理是今日主旋律。
- **关键信号**：大量安全漏洞被修复关闭，但相应的修复代码（PR）尚未合并进主分支，存在一定的修复滞后窗口。

## 2. 版本发布

无。

## 3. 项目进展

今日 **无 PR 被合并**。但项目通过关闭13个Issue完成了重要的维护工作，尤其是针对近期上报的安全漏洞进行了确认和标记。这标志着项目在安全治理上迈出了关键一步。

- **安全加固（重要进展）**：批量关闭了10个安全相关Issue（#3071-#3082， #3068），涵盖了SSRF绕过、授权绕过、命令注入、CSRF等多个攻击面。这表示项目团队已评审并确认了这些漏洞的有效性，为后续的修复PR合并扫清了障碍。
- **功能增强（冻结状态）**：PR #3063 (DeltaChat网关) 和 #3118 (远程WebSocket模式) 等新功能虽已提交，但至今仍在等待审查和合并，进展停滞。

**总结**：项目今日的核心进展并非新增代码，而是完成了对项目安全风险的全面清查和确认，项目健康度在风险管理层面有所提升。

## 4. 社区热点

- **1. HTTP Streaming 功能请求尘埃落定**
  - **Issue [#2404](https://github.com/sipeed/picoclaw/issues/2404)**: 这是一个从4月延续至今的增强请求，今日被关闭。该Issue获得了13条评论和1个赞，用户 **OuSatoru** 提议在配置文件中增加 `"streaming": true` 以支持向LLM后端发送流式HTTP请求。该需求非常明确且具有普遍性。
  - **分析**：此Issue的生命周期较长，最终被关闭可能意味着内部已有其他替代方案，或者团队决定在后续版本中重新考虑。社区对此功能的期待较高，维护者有必要在关闭时给出明确理由，以避免社区困惑。

- **2. Vue.js 适配咨询**
  - **Issue [#3167](https://github.com/sipeed/picoclaw/issues/3167)**: 用户 **Wavekip** 提交了关于PageAgent在Vue 2 MVVM架构下适配方案的咨询。虽然评论数为0，但该问题触及了PicoClaw在复杂前端框架（如Vue, React）中应用的深层痛点。
  - **分析**：这反映了真实用户正在尝试将PageAgent应用于企业级后台系统，其核心诉求是期望Agent能理解并操作组件内部状态而非仅仅操作DOM。这是GUI Agent领域一个重要的技术挑战，代表了社区对更深层次网页交互能力的需求。

## 5. Bug 与稳定性

今日无新增Bug报告，但有一系列严重性极高的 **安全漏洞** 被确认并标记为已关闭 (CLOSED)，这些漏洞此前已于6月9日报告。以下是按严重程度排列的部分关键漏洞：

- **1. [严重] SSRF 与授权绕过**
  - **[#3078](https://github.com/sipeed/picoclaw/issues/3078)**：`web_fetch` SSRF保护可通过环境配置的HTTP代理绕过。
  - **[#3074](https://github.com/sipeed/picoclaw/issues/3074)**：`web_fetch` SSRF保护可通过ISATAP IPv6字面量绕过。
  - **[#3082](https://github.com/sipeed/picoclaw/issues/3082)**：飞书频道回复扩展绕过 `allow_from` 授权检查。
  - **[#3068](https://github.com/sipeed/picoclaw/issues/3068)**：MQTT `allow_from` 授权可通过伪造 `client_id` 绕过。

- **2. [高危] 命令执行与配置劫持**
  - **[#3081](https://github.com/sipeed/picoclaw/issues/3081)**：`exec` 工具的 `cwd` 存在符号链接竞争条件，可能导致在非授权目录执行命令。
  - **[#3079](https://github.com/sipeed/picoclaw/issues/3079)**：`exec` 命令白名单可通过 `jq` 绕过模式匹配，导致环境变量泄露。
  - **[#3072](https://github.com/sipeed/picoclaw/issues/3072)**：Launcher首次设置密码存在CSRF漏洞，可能导致本地控制平面被接管。

- **3. [中危] 认证与配置安全**
  - **[#3071](https://github.com/sipeed/picoclaw/issues/3071)**：已认证的WebSocket客户端可触发未经授权的配置重载(`/reload`)。

**已有修复PR**：目前，针对上述漏洞的专门修复PR **尚未被合并**。今日被关闭的PR（如 [#3165](https://github.com/sipeed/picoclaw/pull/3165), [#3166](https://github.com/sipeed/picoclaw/pull/3166), [#3168](https://github.com/sipeed/picoclaw/pull/3168), [#3169](https://github.com/sipeed/picoclaw/pull/3169)）主要处理的是OpenAI兼容性、日志和心跳包相关的Bug，并不直接解决上述安全漏洞。此外，PR [#3115](https://github.com/sipeed/picoclaw/pull/3115) 修复了内联 Data URL 导致会话历史损坏的Bug。

## 6. 功能请求与路线图信号

- **明确的功能请求**:
  - **[#2404](https://github.com/sipeed/picoclaw/issues/2404) (已关闭)**: 添加流式HTTP请求支持。虽然已关闭，但这是一个强信号，表明社区对此有普遍需求。如果关闭是由于设计决策而非已实现，团队应给出规划。
  - **[#3167](https://github.com/sipeed/picoclaw/issues/3167)**: PageAgent对Vue等MVVM框架的适配。这是一个技术挑战，若采纳将极大扩展PicoClaw的应用场景。

- **可能的路线图信号（来自待合并PR）**:
  - **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063)**: 新增DeltaChat网关。这表明项目可能计划扩展其支持的IM平台，以覆盖更多去中心化或隐私优先的用户群体。
  - **[PR #3118](https://github.com/sipeed/picoclaw/pull/3118)**: 添加远程Pico WebSocket模式。这可能是为用户提供更灵活的代理部署架构，使其可以与运行在本地的PicoClaw实例分离。

**判断**：`streaming` 支持是LLM交互的基础功能，大概率会被纳入后续版本。Vue适配则代表更长远的技术探索。DeltaChat和远程模式则暗示了项目在平台扩展性和部署灵活性上的规划。

## 7. 用户反馈摘要

- **安全研究者的贡献 (YLChen-007)**：来自安全研究员 **YLChen-007** 的批量漏洞报告 (#3071-#3082) 揭示了PicoClaw当前版本在多处安全设计上存在不足。这虽然给项目带来压力，但也极大地帮助了项目提升安全性。
- **企业级应用痛点 (Wavekip)**：用户 **Wavekip** 通过 [#3167](https://github.com/sipeed/picoclaw/issues/3167) 反映了PageAgent在真实企业后台系统（Vue + Element UI）中遇到的困难，即无法有效处理组件化状态，只能操作DOM。这指出了当前GUI Agent能力的边界。
- **基础功能需求 (OuSatoru)**：用户 **OuSatoru** 在 [#2404](https://github.com/sipeed/picoclaw/issues/2404) 中提出的Streaming请求是许多开发者开箱即用的期望功能，其长期未解决和最终关闭可能会使用户感到困惑或失望。

## 8. 待处理积压

以下为创建时间较长、状态为`stale`但尚未合并或有效回应的PR，建议维护者团队优先关注，避免社区贡献沉没：

1. **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063) (feat: add deltachat gateway)**
   - **创建**: 2026-06-08 | **状态**: OPEN, stale
   - **重要性**: 高。这是一个全新的平台集成，对扩大用户基础有吸引力，但已积压超过两周。

2. **[PR #3116](https://github.com/sipeed/picoclaw/pull/3116) (fix(pico): complete turn.done lifecycle signaling)**
   - **创建**: 2026-06-12 | **状态**: OPEN, stale
   - **重要性**: 中。修复Pico核心生命周期中的功能缺失，对依赖此功能的用户至关重要。

3. **[PR #3115](https://github.com/sipeed/picoclaw/pull/3115) (Fix inline data URL media extraction)**
   - **创建**: 2026-06-12 | **状态**: OPEN, stale
   - **重要性**: 中。修复了影响所有使用文件读取或命令执行工具用户的会话历史Bug。

4. **[Issue #3167](https://github.com/sipeed/picoclaw/issues/3167) (Vue适配咨询)**
   - **创建**: 2026-06-24 | **状态**: 新 (仅1天)，但无回复。
   - **重要性**: 中低。这是一个社群咨询，但仍建议给予初步回应，即使目前没有方案，也应肯定其价值并说明挑战。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 – 2026-06-25

---

## 1. 今日速览

过去 24 小时内，NanoClaw 项目保持了极高的活跃度：共产生 **1 个新 Issue** 和 **18 个 Pull Requests**，其中 **2 个 PR 已被合并/关闭**，其余 16 个仍在审查中。合并的 PR 包括一个已分配 CVE 的安全修复（CVE-2026-29611）和社区急需的 Telegram 多 Bot 功能。大量 Fix 型 PR 覆盖了 macOS 兼容性、Signal 消息路由、Docker-in-Docker 支持等稳定性领域，同时多个功能型 PR（Matrix 原生 E2EE、远程 MCP 服务器、`/learn` 技能）进入审查。项目整体呈现“密集开发、快速修复、积极准备新能力”的健康态势。

| 指标 | 数量 |
|------|------|
| 新 Issue | 1（1 open） |
| 新 PR | 18（16 open / 2 closed） |
| 新版本发布 | 0 |

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭了 **2 个 PR**，分别聚焦安全与功能：

- **[#2799] fix(security): confine send_file reads to /workspace (CVE-2026-29611)**  
  安全修复。`send_file` 之前仅做存在性检查，无路径限制，注入或被入侵的 Agent 可读取容器内任意文件。该 PR 增加了根目录约束和路径规范化，已分配 CVE-2026-29611。合并标志着安全基线的重要提升。  
  [PR #2799](https://github.com/nanocoai/nanoclaw/pull/2799)

- **[#2849] feat(telegram): support multiple bot instances via TELEGRAM_BOT_TOKEN_<SUFFIX>**  
  功能实现。通过读取 `TELEGRAM_BOT_TOKEN_<SUFFIX>` 环境变量，支持在同一 NanoClaw 实例中运行多个 Telegram Bot，直接回应了 #2852 的社区诉求。现已合并。  
  [PR #2849](https://github.com/nanocoai/nanoclaw/pull/2849)

两个合并 PR 分别补强了安全底线和用户呼声极高的多实例能力，体现出维护者对安全与社区需求的快速响应。

---

## 4. 社区热点

- **[Issue #2852] “telegram multi-bot”**  
  该 Issue 是今日唯一新建的 Issue，用户明确表达对 Telegram 多 Bot 功能“被移除后又未见稳定实现”的不满，并询问项目是否仍会支持。即使暂无评论，它直接催生了 #2849（已合并）和后续的 #2853（新 open PR），表明维护者已高度关注并迅速行动，是今日最值得关注的社区信号。  
  [Issue #2852](https://github.com/nanocoai/nanoclaw/issues/2852)

- **大型功能 PR 虽无激烈评论，但关注度可期**  
  如 [#2844 Matrix 原生 E2EE](https://github.com/nanocoai/nanoclaw/pull/2844)、[#2843 `/learn` 技能](https://github.com/nanocoai/nanoclaw/pull/2843) 等 PR，涉及底层通讯和安全能力，预计会随着审查推进吸引更多开发者讨论。

---

## 5. Bug 与稳定性

今日提交或更新的 Bug 修复覆盖安全、兼容性、测试等多个层面，按严重程度排列如下：

| 优先级 | PR | 摘要 | 状态 |
|--------|-----|------|------|
| **严重（已修复）** | [#2799](https://github.com/nanocoai/nanoclaw/pull/2799) | CVE-2026-29611 任意文件读取路径限制 | 已合并 |
| **高（新提交）** | [#2854](https://github.com/nanocoai/nanoclaw/pull/2854) | macOS Rancher Desktop 下自签名证书导致所有 Agent API 调用失败 | open |
| **高** | [#2850](https://github.com/nanocoai/nanoclaw/pull/2850) | Signal 群组消息丢失 `isMention`/`isGroup`，路由器无法区分提及与背景流量 | open |
| **高** | [#2846](https://github.com/nanocoai/nanoclaw/pull/2846) | 容器内 Docker Agent 无法使用 docker.sock，缺少挂载及组权限 | open |
| **中** | [#2848](https://github.com/nanocoai/nanoclaw/pull/2848) | OpenCode provider 中工作目录与 `.env` 回退失效 | open |
| **中** | [#2851](https://github.com/nanocoai/nanoclaw/pull/2851) | 测试框架中废弃轮询循环窃取后续测试消息，导致假性失败 | open |
| **中** | [#2845](https://github.com/nanocoai/nanoclaw/pull/2845) | `q.ts` 不传递位置参数，参数化查询无法使用 | open |
| **中（待合并）** | [#2800](https://github.com/nanocoai/nanoclaw/pull/2800) | `ncl groups` 文件夹路径遍历（CWE-22）及镜像标签未固定 | open |
| **中（待合并）** | [#2801](https://github.com/nanocoai/nanoclaw/pull/2801) | 路由器对原始 JSON 基元的解析缺陷，可能造成错误路由 | open |
| **中（待合并）** | [#2802](https://github.com/nanocoai/nanoclaw/pull/2802) | ncl socket 无超时与无限制缓冲区，可导致永久挂起或内存暴涨 | open |
| **中（待合并）** | [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | 容器杀死后 `outbound.db` 日志残留及轮询竞争（关联 #2516 #2640） | open |

整体而言，今日新增的修复（#2854、#2850、#2846 等）直接提升了 macOS 生产环境可用性、消息路由准确性以及容器内 Docker 支持；而等待中的安全修复（#2800 等）若合并将进一步降低攻击面。

---

## 6. 功能请求与路线图信号

除 #2852 的 multi-bot 需求（已有实现）外，以下 PR 指向了明确的功能方向：

- **[#2844] Matrix 原生 E2EE 适配器**  
  用 `matrix-bot-sdk` + Rust 加密绑定替换 Chat SDK 桥接，实现持久端到端加密。这是对 Matrix 协议“一等公民”级别支持的明确信号，为要求隐私的团队提供基础。  
  [PR #2844](https://github.com/nanocoai/nanoclaw/pull/2844)

- **[#2847] 远程 MCP 服务器（HTTP/SSE）**  
  允许 Agent 连接远程 MCP 服务器，不再局限于本地 stdio 进程，极大扩展工具链部署灵活性。  
  [PR #2847](https://github.com/nanocoai/nanoclaw/pull/2847)

- **[#2843] `/learn` 技能**  
  从目录、URL 或剪贴板自动提炼可复用 Skill，降低贡献门槛，推动技能生态增长。  
  [PR #2843](https://github.com/nanocoai/nanoclaw/pull/2843)

- **[#2842] 通用惰性扩展点**  
  在宿主与容器运行时预置 `registerX()/applyX()` 接缝，当前为无操作，但为未来插件架构奠定基础。  
  [PR #2842](https://github.com/nanocoai/nanoclaw/pull/2842)

上述 PR 共同勾勒出下一阶段的路线图：**多通道原生化（Telegram/Matrix）、远程化（MCP over HTTP）、用户可编程（`/learn`）、架构可扩展（扩展点）**。

---

## 7. 用户反馈摘要

来自 **Issue #2852** 的真实用户声音（原文）：

> “we had it, and then it got removed. its said that there is ‘instance’ support, but Claude cannot get it to work, Is it ever going to be implemented? or do we need to look elsewhere?”

**【反馈要点】**  
- 用户曾使用过 Telegram 多 Bot 功能，后该功能被移除；  
- 项目声称支持“实例”，但用户通过 Claude（NanoClaw 的 AI 助手）无法配置成功；  
- 明确表达如果该功能不能回归，将考虑迁移到替代方案。

该反馈直接驱动了 #2849 的合并与 #2853 的再度迭代，显示出维护者对用户留存的高度重视。

---

## 8. 待处理积压

以下 PR 开放时间较长或涉及关键安全/稳定性，建议维护者优先关注：

| PR | 创建时间 | 重要性 | 说明 |
|----|----------|--------|------|
| [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | 2026-06-12（13天） | **高** – 稳定性 | 修复容器 SIGKILL 后 outbound.db 日志损坏及轮询竞争，关联 #2516 #2640 |
| [#2802](https://github.com/nanocoai/nanoclaw/pull/2802) | 2026-06-17（8天） | **高** – 安全 | ncl socket 无超时/无限缓冲区，可被恶意宿主或客户端利用 |
| [#2800](https://github.com/nanocoai/nanoclaw/pull/2800) | 2026-06-17（8天） | **高** – 安全 | 文件夹遍历漏洞 + 镜像标签未固定（CWE-22） |
| [#2801](https://github.com/nanocoai/nanoclaw/pull/2801) | 2026-06-17（8天） | **中** – 稳定性 | 路由器输入 JSON 基元解析缺陷，可能造成静默错误 |
| [#2815](https://github.com/nanocoai/nanoclaw/pull/2815) | 2026-06-18（7天） | **中** – 稳定性 | 改进 safeParseContent，添加回归测试，防止非对象 JSON 引发路由器异常 |
| [#2842](https://github.com/nanocoai/nanoclaw/pull/2842) | 2026-06-23（2天） | **中** – 架构 | 通用惰性扩展点；虽时间尚短，但涉及架构变更，建议尽早评审 |

上述 PR 中，#2750 等待时间最长且影响面广，建议优先审阅合并；#2802/#2800 作为安全补丁也应加速处理。

---

*以上分析基于 2026-06-25 获取的 GitHub 项目数据，所有链接指向 nanocoai/nanoclaw 仓库。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-06-25

## 1. 今日速览

过去 24 小时项目活跃度极高：共产生 19 条 Issue 更新（16 条活跃，3 条关闭）和 45 条 PR 更新（18 条已合并/关闭）。核心团队对昨日生产环境 **Reborn meltdown**（全局 4 分钟冻结）响应迅速，提交了 #5204、#5206 等紧急修复 PR；同时记忆层重构 #5163 成功合并，完成 #3537 M2 里程碑。但 WebUI 审批流程的系列 Bug（#5196、#5192 等）集中爆出，显示该模块仍需打磨。项目总体健康度良好，迭代节奏快，但稳定性与用户体验细节是当前主要薄弱点。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

| PR/Issue | 状态 | 要点 |
|----------|------|------|
| [#5163](https://github.com/nearai/ironclaw/pull/5163) | ✅ 合并 | **记忆层 M2 提升**：将 Reborn 内存系统提取为 `ironclaw_memory`（中立接口） + `ironclaw_memory_native`（文件系统实现），后续可插拔存储提供商；严格行为保持，为 #3537 剩余工作奠定基础。 |
| [#5193](https://github.com/nearai/ironclaw/pull/5193) | ✅ 合并 | **CI 修复**：解决重复 workflow key 及 ignored 测试问题，恢复 main 分支绿色。 |
| [#5139](https://github.com/nearai/ironclaw/issues/5139) | ✅ 关闭 | **回归修复**：web/research 任务初始化挂起（零 LLM 调用）问题在 main 上修复，此前导致 21/147 任务超时。 |
| [#5190](https://github.com/nearai/ironclaw/issues/5190) | ✅ 关闭 | **无效 token 处理**：WebUI 接受无效 bearer token 后无响应的问题已修复。 |
| [#5187](https://github.com/nearai/ironclaw/issues/5187) | ✅ 关闭 | **本地化标签**：Reborn 设置与自动化过滤器标签已支持 i18n。 |
| [#5204](https://github.com/nearai/ironclaw/pull/5204) 、 [#5206](https://github.com/nearai/ironclaw/pull/5206) 、 [#5203](https://github.com/nearai/ironclaw/pull/5203) 、 [#5202](https://github.com/nearai/ironclaw/pull/5202) | 🔄 已提交/待审核 | 针对 **2026-06-24 meltdown** 的修复集：为 NEAR AI 调用添加连接超时/快速失败、WASM 执行解耦 tokio worker、降低 provider 超时对全局的影响。 |

以上合并/关闭项表明：架构重构（memory）与基础设施稳定性（CI）取得实质性进展；性能与容错方面虽暴露问题但已进入修复通道。

## 4. 社区热点

**工具权限与审批流程反馈扎堆**  
今日有多条 Issue 从 Dogfooding（#5119）中报告，指向审批机制交互问题：

- [#5196](https://github.com/nearai/ironclaw/issues/5196)：「Ask each time」批准后仍因 authorization 错误导致重复审批，流程断裂。  
- [#5192](https://github.com/nearai/ironclaw/issues/5192)：拒绝工具调用后依然继续弹出新的审批请求，无法中断。  
- [#5197](https://github.com/nearai/ironclaw/issues/5197)：禁用工具时，助手可能调用其他无关工具而非报告不可用。  
- [#5191](https://github.com/nearai/ironclaw/issues/5191)：内部 skill orchestration 调试消息暴露在对话 UI 中。

**开箱体验痛点**  
[#5169](https://github.com/nearai/ironclaw/issues/5169) 指出：干净默认环境中，内置技能包含 “Authorization/Bearer” 等 API 词汇会触发现行安全词拦截，导致良性请求被误杀并显示「temporary system issue」，误导调试方向。此问题获 2 条评论，被社区视为影响新用户上手的严重体验缺陷。

**Meltdown incident 的技术讨论**  
PR [#5204](https://github.com/nearai/ironclaw/pull/5204) 的 Problem 段落详细分析了昨日生产事故的两个根因（NEAR AI 客户端无连接超时 + WASM 执行阻塞 tokio），引发对运行时韧性的关注。

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 摘要 | 修复进展 |
|----------|------------|------|----------|
| 🔴 严重 | [#5204](https://github.com/nearai/ironclaw/pull/5204) / [#5206](https://github.com/nearai/ironclaw/pull/5206) | **生产 Meltdown**：~40 并发导致 4 分钟全进程冻结、mass lease_expired、Gateway 502。 | 已有修复 PR 待合并 |
| 🟠 高 | [#5184](https://github.com/nearai/ironclaw/issues/5184) | **启动失败**：NEAR AI MCP product-auth 不可用时 runtime build 直接报错，中断部署。 | 未分配 |
| 🟠 高 | [#5169](https://github.com/nearai/ironclaw/issues/5169) | **安全词误杀**：内置技能词汇触发 denylist，误导显示为临时系统问题。 | 无 PR |
| 🟡 中 | [#4986](https://github.com/nearai/ironclaw/issues/4986)（自 06-16） | **自动化永久阻塞**：需工具审批的循环自动化一旦等待审批可能永远无法恢复。 | 无 PR |
| 🟡 中 | [#5196](https://github.com/nearai/ironclaw/issues/5196) / [#5192](https://github.com/nearai/ironclaw/issues/5192) / [#5197](https://github.com/nearai/ironclaw/issues/5197) | **审批流程异常**：批准后 authorization 错误、拒绝后持续请求、禁用后调用无关工具。 | 无 PR，但 [#5068](https://github.com/nearai/ironclaw/pull/5068)（Tool permissions UI）待合并可能改善 |
| 🔵 低 | [#5189](https://github.com/nearai/ironclaw/issues/5189) | 成功工具调用不显示活动详情（失败却显示），UI 反馈不一致。 | 无 PR |
| 🔵 低 | [#5179](https://github.com/nearai/ironclaw/issues/5179) | 多租户用户无法通过 WebUI 查看日志。 | PR [#5199](https://github.com/nearai/ironclaw/pull/5199) 已提交 |

## 6. 功能请求与路线图信号

- [**#5182**](https://github.com/nearai/ironclaw/issues/5182)：**Reborn 可观测性增强** — 请求 CLI/Server 输出结构化诊断日志，当前须手动 scrape，开发者呼声渐高。  
- [**#5188**](https://github.com/nearai/ironclaw/issues/5188)：**响应式侧边栏** — 提升 WebUI v2 在桌面/移动端的行为一致性，属于 UI 打磨类需求，可能随下个前端迭代进入。  
- [**#5149**](https://github.com/nearai/ironclaw/pull/5149)（Open / XL）：**渐进式工具暴露** — 按需传递工具 schema，可减少每次调用 25.8k tokens，对延迟/成本优化意义重大，当前 feature-gated 。  
- [**#5068**](https://github.com/nearai/ironclaw/pull/5068)（Open / XL）：**工具权限 UI 设置** — 全局自动批准 + 每工具权限控制，若合并将直接解决 #5196 等审批流程问题。  
- [**#5201**](https://github.com/nearai/ironclaw/issues/5201)：**Memory 后续里程碑** — 跟踪 #3537 剩余任务（M3+），提示下一阶段可能支持远程 memory 提供商。

## 7. 用户反馈摘要

以下提炼自 Issue 评论中的真实声音（Dogfooding #5119 相关）：

- **#5190**：*“打开 WebUI 时用了过期 token，UI 能进去但后续操作无任何反应，也没有 clear authentication error”* → 期望快速失败并提示。  
- **#5192**：*“拒绝工具审批后，Agent 继续请求其他工具审批，根本没有停止”* → 用户期望拒绝能阻断流程。  
- **#5196**：*“点击 Approve 后出现 authorization 错误，然后又出现相同审批请求，很 confusing”* → 状态同步存在漏洞。  
- **#5191**：*“内部 skill orchestration 消息直接出现在聊天里，普通用户不应该看到这些”* → 应过滤或降级。  
- **#5169**：*“You can't even make a simple request without hitting this”* → 安全机制过度抑制，且错误提示具误导性。

整体用户情绪：积极测试并反馈，但对审批流程的一致性和错误提示的清晰度有较高期待。

## 8. 待处理积压

| ID | 类型 | 创建时间 | 摘要 | 备注 |
|----|------|----------|------|------|
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | Issue | 2026-05-27 | **Nightly E2E 持续失败**（约 30 天），每日更新但未关闭，影响主分支信心。 | 建议立即排查 root cause |
| [#4002](https://github.com/nearai/ironclaw/pull/4002) | PR | 2026-05-24 | **Dependabot actions group 16 项更新**（含 checkout v7 等），风险中等（CI），长期未合并。 | 需评估兼容性或分批合入 |
| [#4986](https://github.com/nearai/ironclaw/issues/4986) | Issue | 2026-06-16 | **Recurring automation 因审批永久阻塞**，无修复 PR，用户可能放弃此功能。 | 高影响，建议纳入近期 sprint |

以上为 IronClaw 2026-06-25 项目动态日报。项目节奏紧凑，核心功能与稳定性持续演进，用户体验细节方面需重点跟进近期 Dogfooding 反馈。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据您提供的 LobsterAI 项目数据生成的 2026-06-25 项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-06-25

---

### 1. 今日速览

过去 24 小时内，项目呈现出**极高的维护与收尾活跃度**。核心开发者在一天内处理了高达 **43 条 Pull Request**，其中 41 条被合并或关闭，表明项目正处于针对稳定性和兼容性的密集缺陷修复冲刺阶段。相比之下，社区 Issue 活动非常平静，仅有一条历史积压的 `[stale]` 标签 Issue 被刷新。整体上，项目代码库正在快速趋稳，为下一阶段的迭代（可能涉及重大版本发布）清除了诸多技术债务和功能性 Bug。

### 2. 版本发布

过去 24 小时内无新版本发布。

### 3. 项目进展

今日项目取得了显著的工程进展。维护者 `liuzhq1986` 和 `fisherdaddy` 主导了数十个 Bug 修复和配置优化的合并，项目整体稳定性大幅提升。

- **Agent 引擎 (OpenClaw) 关键修复：**
    - 统一了跨平台子进程启动逻辑（[#2195](https://github.com/netease-youdao/LobsterAI/pull/2195)），并修复了 Shell 快照场景下误启动多余应用程序的问题（[#2196](https://github.com/netease-youdao/LobsterAI/pull/2196)）。
    - 修复了 LLM 输出内容拼接时的前缀去重问题（[#2197](https://github.com/netease-youdao/LobsterAI/pull/2197)）。
    - **解决了用户反馈的“空闲时持续消耗 Token”的严重问题**，通过增加循环终止器（Loop Breaker）避免无休止的 Aborted 工具调用（[#2049](https://github.com/netease-youdao/LobsterAI/pull/2049)）。
    - 修复了网关 Session 超时导致聊天功能阻塞（[#2050](https://github.com/netease-youdao/LobsterAI/pull/2050)）。

- **核心稳定性与兼容性修复：**
    - **解决了用户会话（Session）冻结的问题**（[#2047](https://github.com/netease-youdao/LobsterAI/pull/2047)）。
    - 将 Windows 更新启动器从已弃用的 VBScript 迁移至隐藏的 PowerShell 脚本，提升了更新可靠性（[#2057](https://github.com/netease-youdao/LobsterAI/pull/2057)）。
    - 修复了微信（WeChat）在应用更新或重装后的集成 Bug（[#2086](https://github.com/netease-youdao/LobsterAI/pull/2086)）。

- **模型支持持续迭代：**
    - 新增了对 **Minimax M3** 和 **Mimo v2.5** 模型的支持，并同步更新了 BYOK（自带密钥）模型的默认上下文窗口配置（[#2089](https://github.com/netease-youdao/LobsterAI/pull/2089), [#2102](https://github.com/netease-youdao/LobsterAI/pull/2102)）。
    - **重要修复**：解决了用户配置的自定义上下文窗口在应用更新后被覆盖的问题（[#2102](https://github.com/netease-youdao/LobsterAI/pull/2102)）。

### 4. 社区热点

今日社区讨论主要围绕 **Issue #1394** 展开，这也是过去 24 小时内唯一活跃的 Issue。

- **链接**: [netease-youdao/LobsterAI Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)
- **核心诉求**：用户对“不重复执行”定时任务的自动删除逻辑表达了困惑和不满。用户希望将“不重复”理解为“仅运行一次，但保留配置以便编辑或手动再次触发”，而非系统当前执行的“运行后即永久删除”。
- **分析**：虽然该 Issue 已被机器人标记为 `[stale]`，但它在沉寂近 3 个月后因更新而重新浮出水面，且至今无官方回复或修复 PR。用户可以无法找回被自动删除的配置，这反映了项目在“配置生命周期管理”上存在设计与用户预期的偏差。

此外，PR [#2049](https://github.com/netease-youdao/LobsterAI/pull/2049) 中明确提到了“用户报告空闲期间持续消耗 Token”，说明社区对成本/资源控制的强烈需求得到了开发者的迅速响应和解决。

### 5. Bug 与稳定性

今日的 Bug 修复活动是绝对的主角。以下按严重程度汇总要点：

| 严重程度 | Bug 描述 | Issue/PR | 修复状态 |
|---|---|---|---|
| **严重** | Agent 在空闲时因工具循环中断失败导致持续消耗 LLM API Token | PR #2049 | ✅ 已合并 |
| **严重** | 用户会话（Session）无响应/冻结，无法继续对话 | PR #2047 | ✅ 已合并 |
| **高** | 用户配置的自定义上下文窗口在应用更新后丢失 | PR #2102 | ✅ 已合并 |
| **高** | 定时任务（非重复模式）执行一次后配置被永久删除 | Issue #1394 | ❌ 待处理 |
| **中** | GitHub Copilot Token 刷新导致 Gateway 意外重启 | PR #2043 | ✅ 已合并 |
| **中** | Shell 快照执行时产生多余的 Dock 应用 | PR #2196 | ✅ 已合并 |
| **中** | WeChat 在应用升级或重装后出现 Bug | PR #2086 | ✅ 已合并 |
| **低** | 应用更新器使用已弃用的 VBScript 作为启动器 | PR #2057 | ✅ 已合并 |

### 6. 功能请求与路线图信号

尽管没有新增的功能请求 Issue，但从今日合并的 PR 中可以清晰看到项目的路线图信号：

- **Agent 架构趋于成熟**：今天大量针对 OpenClaw 的修复（Spawn、Docker、Tool Loop 终止）表明，开发者正在花费巨大精力打磨 Agent 的执行层。这为后续高可靠性的 CoWorker（协作者）协作奠定了坚实基础。
- **模型接入战略优先级高**：项目在第一时间跟进并适配了 **Minimax M3** 和 **Mimo v2.5** 等新模型。代码中频繁出现的 `chore` 和 `fix` 涉及模型配置，暗示了一个“零摩擦模型接入”的架构正在成型。
- **CoWorker 协作层 Signal**：PR [#2078](https://github.com/netease-youdao/LobsterAI/pull/2078) 将技能选择的逻辑从内联提示词改为了元数据路由。这通常是为未来构建复杂的“技能路由系统”或“技能市场”所做的准备。

### 7. 用户反馈摘要

近期用户反馈主要集中在以下两点：

1. **任务配置的数据安全**（Issue #1394）：用户对一次性任务（`不重复执行`）的删除逻辑不满。用户的典型使用场景是：创建任务 -> 手动测试 -> 结果不符合预期 -> 需要修改配置再次运行。当前的自动删除机制完全打破了这一工作流，导致用户需要重新创建整个任务，体验不佳。
2. **资源消耗透明度**（PR #2049 上下文）：用户在空闲状态或无任务执行时，被无节制的 Token 消耗触达了成本焦虑。这表明用户不仅关注功能的可用性，也非常在意 Agent 在后台运行的资源开销和成本控制。该 Bug 已通过修复解决。

### 8. 待处理积压

目前项目最主要的积压/待处理问题是 **Issue #1394**。

- **标题**: [stale] 定时任务选择不重复执行时，执行一次后会自动被永久删除（预期不自动删除）
- **创建时间**: 2026-04-03
- **最后更新**: 2026-06-24
- **链接**: [netease-youdao/LobsterAI Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)
- **风险评估**: 这是一个长期未解决的 **数据完整性/配置丢失** 问题。虽然当前被认为是“预期行为”，但该行为与主流任务调度软件（如 Cron 的一次性任务）的用户思维定势相悖。建议项目维护者尽快评估，明确这是设计如此还是需要标记为 Bug 并安排修复。如果继续沉默，该 Issue 会日复一日地被 `stale` 机器人刷新，降低 Issue Tracker 的信噪比。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

好的，请查收基于您提供的 GitHub 数据生成的 TinyClaw 项目动态日报。

---

# TinyClaw (TinyAGI/tinyagi) 项目动态日报 | 2026-06-25

## 1. 今日速览
- **活跃度评估**：🔴 **低**。过去 24 小时项目未收到新的 Issue 或版本 Release，处于静默迭代阶段。
- **核心动态**：唯一的变更是一份关于 Windows 兼容性的重要 Pull Request (#281) 被合并关闭。
- **项目健康度**：总体稳定。项目团队正集中精力解决历史遗留的跨平台兼容性问题，而非引入新功能。积压数量为零，响应效率较高。
- **小结**：今日无用户侧新反馈或 Bug 报告，项目热度虽低，但底层工具链的稳定性得到了一次实质性提升。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
**唯一更新：Windows 平台兼容性 Bug 修复（已合并）**
- **PR**: [#281 fix: Windows cross-platform support in CLI](https://github.com/TinyAGI/tinyagi/pull/281)
- **贡献者**: mperkins0155
- **动作**: 今日已将 PR 合并入主分支并关闭（从创建到合并历时约 9 天）。
- **问题分析**：该 PR 旨在解决 `tinyagi` CLI 在原生 Windows 环境（非 WSL）下的启动失败问题。根据描述，项目主要存在三个 Windows 专属 Bug：
    1. **路径解析错误**：`new URL('.', import.meta.url).pathname` 在 Windows 下会返回带有盘符的路径（如 `/C:/...`），直接传递给 `path.resolve` 会导致模块查找路径异常，从而引发 `MODULE_NOT_FOUND` 错误。
    2. **驱动器号重复**：修复了路径拼接时可能出现的盘符重复（如 `C:/C:/...`）问题。
    3. 其他文件路径兼容性调整。
- **推进意义**：此修复**彻底移除了 Windows 用户使用 TinyClaw CLI 的门槛**。此前 Windows 用户必须借助 WSL 环境，这会显著影响 CI/CD 集成以及部分 Windows 原生开发者的体验。

## 4. 社区热点
- **当前状态**：过去 24 小时社区无高讨论度或高评论量的议题。PR #281 虽为今日焦点，但评论数为 0，无公开讨论。
- **背后诉求分析**：尽管缺乏公开辩论，**“原生 Windows 支持”** 是很多开源 CLI 工具在早期被忽略的高频需求。此次静默合并表明贡献者与维护者之间的沟通可能已通过其他渠道（如内部讨论或明确的 Bug Fix 需求）完成，而非需要在 Issue 区公开辩论。这反映出社区目前主要由效率驱动的**问题解决型贡献**主导，而非功能讨论型。

## 5. Bug 与稳定性
- **今日新增 Bug**：0 条。
- **近期高严重性 Bug 修复（今日合入）**：
    - **[严重][CLI 无法启动] Windows 原生环境下的模块查找失败**
        - **关联修复**：[PR #281](https://github.com/TinyAGI/tinyagi/pull/281)
        - **表现**：在原生 Windows 系统（命令提示符/PowerShell）中执行 `tinyagi` 命令或相关 CLI 指令时，Node.js 因路径解析异常而抛出 `MODULE_NOT_FOUND` 错误，导致工具完全不可用。
        - **严重程度**：阻塞级。直接导致平台不可用，此 Bug 已通过今日合并的 PR 修复。

## 6. 功能请求与路线图信号
- **今日无新功能请求**。
- **路线图信号**：由于 PR #281 专注于基础架构层面的**兼容性**而非新功能，可以判断项目团队当前优先级的重点是 “**稳定跨平台基础设施**” ，可能会在核心 CLI 对所有主流平台（Win/macOS/Linux）的稳定支持达成后，才大规模铺开新功能开发。

## 7. 用户反馈摘要
- 今日无公开用户反馈或评论。

## 8. 待处理积压
- **Issues 积压**：0 条
- **待 Merge PR**：0 条
- **维护者提醒**：当前无长期未响应的重要议题。项目维护状态良好，无需特别提醒。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的CoPaw (QwenPaw) 项目数据，为您生成了以下项目动态日报。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-06-25

## 1. 今日速览

项目在24小时内保持极高的活跃度（25条 Issues, 50条 PR），但观察发现 **PR 的合并/关闭率较低（14%），大量代码变更正等待审查**。社区反馈主要集中在两个方面：一是 **AgentScope 2.0 架构升级后引发的兼容性与功能回归问题**（如流式传输、Token 显示、工具调用渲染），二是 **特定模型/提供商的集成适配问题**（如 GLM, MiniMax, Kimi Coding）。此外，与前端渲染、性能及移动端体验相关的 Bug 报告也较为集中。项目正处于关键架构升级的阵痛期与快速迭代期。

## 2. 版本发布

| 版本 | 更新时间 | 备注 |
| :--- | :--- | :--- |
| 今日无新版本发布 | - | 暂无 |

## 3. 项目进展

今日核心工作集中在 **AgentScope 2.0 迁移后的修复** 与 **特定模型兼容性** 上，并已关闭或提交了多项关键修复。具体进展如下：

- **修复 DashScope (阿里云灵积) 提供商兼容性**：修复了旧版 `generate_kwargs` 参数在新架构下未正确处理的 Bug，特别是 `extra_body` 和 `enable_thinking` 参数。([PR #5491](https://github.com/agentscope-ai/QwenPaw/pull/5491))
- **解决会话时间信息固定问题**：通过合并多个相关 PR，将 `Current date` 从静态环境上下文移至每条用户消息的动态前缀中，确保长时间会话中的时间信息准确，并改善 Prompt 缓存效率。([PR #5498](https://github.com/agentscope-ai/QwenPaw/pull/5498), [PR #5499](https://github.com/agentscope-ai/QwenPaw/pull/5499))
- **修复 GLM 模型工具调用兼容性**：提交了针对 GLM-5.x 通过 OpenCode Go 服务调用时 `json_schema_converter` 失败的问题，通过在工具 schema 中内联所有 `$ref/$defs` 引用来解决。([PR #5496](https://github.com/agentscope-ai/QwenPaw/pull/5496))
- **消息通道流式输出修复**：针对所有即时通讯（IM）通道，修复了因 AgentScope 2.0 迁移导致的后端流式传输路径断裂、多段回复无法正确分开发送的问题。([PR #5487](https://github.com/agentscope-ai/QwenPaw/pull/5487))
- **修复移动端 Agent 切换问题**：已关闭移动端无法切换智能体的 Bug。([Issue #5476](https://github.com/agentscope-ai/QwenPaw/issues/5476))
- **关闭 Shell 命令解析错误**：修复了 `execute_shell_command` 工具无法正确解析管道、重定向等特殊字符的问题。([Issue #5373](https://github.com/agentscope-ai/QwenPaw/issues/5373))
- **优化内存占用讨论**：关于1.4G高内存占用的 Feature Request 已被关闭，推测已通过其他方式解决或有后续规划。([Issue #5441](https://github.com/agentscope-ai/QwenPaw/issues/5441))

## 4. 社区热点

- **自定义 OpenAI 提供商无法 Function Calling (Issue #5345)**：该问题获得8条评论，是讨论最密集的议题。用户 `qiyuanlicn` 报告了在使用 OMLX 等非标准 OpenAI 兼容提供商时，模型仅返回文本而无法触发工具调用。Ollama 则工作正常。**这反映了社区对支持更多样化、非主流模型后端的核心诉求。** ([Issue #5345](https://github.com/agentscope-ai/QwenPaw/issues/5345))
- **群聊消息回复目标错乱 (Issue #5264)**：该 Bug 报告了在飞书/Lark 场景下，若用户同时存在私聊和群聊会话，群内消息的回复会错误地发送到私聊窗口，严重影响用户体验。**凸显了多会话管理逻辑的复杂性以及对即时通讯体验的高要求。** ([Issue #5264](https://github.com/agentscope-ai/QwenPaw/issues/5264))

## 5. Bug 与稳定性

- **严重 (Core/Model Interaction)**:
  - **自定义 OpenAI 提供商无法 Function Calling**：核心功能缺失，限制了 AI 能力的发挥。无关联修复 PR。 ([#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345))
  - **AgentScope 2.0 工具调用渲染问题**：Console 前端在包含大量工具调用的会话中崩溃（白屏），原因是前端组件无法识别新的消息格式。 ([#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401))
  - **MiniMax-M3 模型错误缓存 `rejects_media=True`**：一次安全审核失败导致模型被错误标记为不支持图片，后续所有图片请求被剥离。这是严重的模型路由逻辑 Bug。 ([#5505](https://github.com/agentscope-ai/QwenPaw/issues/5505))

- **中度 (UI/UX & Compatibility)**:
  - **浏览器自动填充劫持搜索框**：在模型配置页面，浏览器的密码自动填充干扰了搜索功能。 ([#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403))
  - **GLM-5.x 模型工具调用报错**：特定模型因 JSON Schema 解析失败而无法使用。已有关联修复 PR。 ([#5472](https://github.com/agentscope-ai/QwenPaw/issues/5472), [PR #5496](https://github.com/agentscope-ai/QwenPaw/pull/5496))
  - **大会话文件加载崩溃**：前端在加载超过 500KB 的会话文件时崩溃，影响深度用户。 ([#5479](https://github.com/agentscope-ai/QwenPaw/issues/5479))
  - **长消息渲染和排版错误**：前端在接收长消息时排版错乱，需切换标签页才能恢复。 ([#5480](https://github.com/agentscope-ai/QwenPaw/issues/5480))

- **轻微 (Other)**:
  - **宽屏模式下发送按钮对齐问题**：页面样式细节问题，已有关联修复 PR。 ([#5501](https://github.com/agentscope-ai/QwenPaw/issues/5501), [PR #5502](https://github.com/agentscope-ai/QwenPaw/pull/5502))
  - **内网安装后页面白屏**：特定网络环境下的部署问题。 ([#5497](https://github.com/agentscope-ai/QwenPaw/issues/5497))

## 6. 功能请求与路线图信号

- **更强的模型提供商扩展性**：
  - **支持 Anthropic 兼容接口**：社区请求增加对 Kimi K2 Code 的 `Anthropic-compatible` 原生 API 支持。 ([#5427](https://github.com/agentscope-ai/QwenPaw/issues/5427))
  - **支持 OpenAI response format**：核心功能请求，使消息流支持 OpenAI 标准的响应格式。 ([#5489](https://github.com/agentscope-ai/QwenPaw/issues/5489))

- **插件/Skill 生态建设**：
  - **支持从 PyPI 通过 pip 安装插件**：这是一项重要的基础设施提议，旨在简化插件的分发与安装，接近 Python 生态标准。([#5484](https://github.com/agentscope-ai/QwenPaw/issues/5484))

- **核心交互体验优化**：
  - **MCP 工具名称优化**：请求在 UI 界面显示人类可读的工具名称，而非模型使用的内部名称。([#5231](https://github.com/agentscope-ai/QwenPaw/issues/5231))
  - **删除/修改单轮对话功能**：用户希望能在本回合删除或修改自己的提问，以便上下文逻辑更连贯。([#5503](https://github.com/agentscope-ai/QwenPaw/issues/5503))

这些功能请求普遍集中在 **“易用性”** 和 **“兼容性”** 上，预示着项目下一阶段需在支持更广泛的模型和提供更流畅的用户交互上发力。特别是 PyPI 插件机制，若被采纳将是项目生态建设的重要里程碑。

## 7. 用户反馈摘要

- **痛点与问题**：
  - **“刚启动，还没做什么，内存占用已经 1.4g 了。”** — `w409401768` 反映了对桌面版资源占用的担忧。([#5441](https://github.com/agentscope-ai/QwenPaw/issues/5441))
  - **“通过Python命令安装后启动，直接报错 Internal Server Error”** — `luo201227` 的安装体验不佳，影响了新用户上手。([#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379))
  - **“大会话文件...打开报错...只能删除该会话才能继续使用”** — `samluoabc` 描述了严重的功能障碍，给重度用户带来数据丢失风险。([#5479](https://github.com/agentscope-ai/QwenPaw/issues/5479))
  - **“群消息的回复会错误地发送到私聊窗口”** — `feng183043996` 反映了多场景协同下的严重干扰。([#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264))
- **使用场景**：
  - **多样化后端集成**：用户`qiyuanlicn` 尝试通过自定义OpanAI兼容接口集成 OMLX 等新兴推理服务，表明社区用户正积极寻求使用更丰富、更便宜或更专业的模型后端。([#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345))
  - **企业级信息通道集成**：关于飞书和钉钉通道的反馈（如[#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264), [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177)）表明项目正被用于实际的生产和办公协作用户场景。

## 8. 待处理积压

- **Desktop 自动更新功能 (PR #4669)**：此 PR 自2026年5月25日起已开放超过一个月，旨在为 Tauri 桌面端加入自动更新功能。长时间未合并可能影响桌面端用户的更新体验，需要维护者评估其优先级并推动审查。([PR #4669](https://github.com/agentscope-ai/QwenPaw/pull/4669))
- **MCP 工具名称显示优化 (Issue #5231)**：自2026年6月16日提出的功能请求，虽只有一个评论，但它涉及到后端和前端两个核心组件，且对用户体验提升明显。该 Issue 缺乏关键标签或来自维护者的明确回复，可能是一个容易被忽视但有效的改进点。([Issue #5231](https://github.com/agentscope-ai/QwenPaw/issues/5231))

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

**ZeroClaw 项目动态日报 · 2026‑06‑25**  
*数据来源：[GitHub](https://github.com/zeroclaw-labs/zeroclaw) | 统计周期：2026‑06‑24 ~ 2026‑06‑25*

---

## 1️⃣ 今日速览

过去 24 小时项目共产生 **47 条 Issue**（新开/活跃 46，关闭 1）和 **50 条 PR**（待合并 45，已合并/关闭 5），未发布新版本。整体活跃度维持高位，社区围绕**多租户安全**、**WASM 插件生态**以及**认证基础设施**展开了密集讨论。多项高风险特性进入 RFC 或实现阶段，同时两个稳定性修复 PR 已合并，项目健康度良好，维护响应及时。

---

## 2️⃣ 版本发布

无。

---

## 3️⃣ 项目进展

今日共 **5 个 PR 被合并或关闭**，其中两个关键合入：

- **🔀 [#8101](https://github.com/zeroclaw-labs/zeroclaw/pull/8101) (fix: fill-translations 修复)**  
  `OmkumarSolanki` 修复了 `fill-translations` 在泄露修复后未清理残留续行（continuation line）的问题，避免重新解析后仍包含脏数据。

- **🔀 [#8285](https://github.com/zeroclaw-labs/zeroclaw/pull/8285) (fix: delegate 工具边界门控)**  
  `wangmiao0668000666` 在 delegate 边界处交集校验调用方与目标方 `SecurityPolicy`，阻止子智能体调用父级明确禁止的工具，**增强了跨委托的安全隔离**。

此外，多个社区 PR 正在等待合并，例如自定义模型提供者验证（[#7485](https://github.com/zeroclaw-labs/zeroclaw/pull/7485)、[#8084](https://github.com/zeroclaw-labs/zeroclaw/pull/8084)）、Telegram 回复绕过 `mention_only`（[#7723](https://github.com/zeroclaw-labs/zeroclaw/pull/7723)、[#7958](https://github.com/zeroclaw-labs/zeroclaw/pull/7958)）等，表明项目在工具安全、渠道体验和配置诊断方面正稳步前进。

---

## 4️⃣ 社区热点

评论最活跃的 Issue 反映了社区对**安全隔离**、**认证集成**和**可发现性**的强烈需求：

- **[#5982 – Per‑sender RBAC for multi‑tenant](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) 💬 9 条**  
  用户期望单一实例能根据 sender 身份提供隔离的工作空间、工具集和速率限制。该诉求与 [#8044](https://github.com/zeroclaw-labs/zeroclaw/issues/8044)（`/model --agent` 授权）形成互补，是多租户部署的核心阻塞项。

- **[#7141 – OIDC Authentication Provider](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) 💬 6 条**  
  作为身份验证基础设施的基石，该 RFC 被标记为 P1，社区关注如何插拔式支持 OIDC/SSH/本地账户，是 v0.9.0 的目标之一。

- **[#6289 – Prompt‑triggered install suggestions](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) 💬 5 条**  
  用户抱怨技能发现困难，希望当提到未安装的能力时自动提示安装。该需求直接提升新用户体验。

- **[#8177 – Supply chain signing & SLSA provenance](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) 💬 5 条**  
  社区安全贡献者提出硬件 PGP、暂离签名和 SLSA 证明，反映出对发布完整性已达企业级要求。

---

## 5️⃣ Bug 与稳定性

今日跟踪的 Bug 覆盖消息处理、资源泄漏、配置静默失败等方面，按严重程度排列：

| 严重性 | Issue | 简述 | 修复 PR |
|--------|-------|------|---------|
| **S1**（工作流阻塞） | [#8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151) | 延迟处理的图片在缓存中丢失引用，后续对话机器人声称未收到图片 | ✅ 已关闭（今日合入修复） |
| **S2**（行为降级） | [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) | MCP stdio 子进程随心跳持续累积，产生 ≈48 个孤儿进程/天 | ❌ 无关联 PR |
| | [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) | `mcp_bundles` per‑agent 配置仅解析不执行，安全隔离形同虚设 | ❌ 无关联 PR |
| | [#7737](https://github.com/zeroclaw-labs/zeroclaw/issues/7737) | 审批归属依赖全局侧信道，并发时状态可能被覆盖 | ❌ 无关联 PR |
| | [#7623](https://github.com/zeroclaw-labs/zeroclaw/issues/7623) | delegate 至 Codex/OAuth 子智能体时转发父协调器 API Key（#7266 仍未完全修复） | ❌ 无关联 PR |
| | [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) | `fill-translations` 修复引入遗留 translations‑map 项，导致数据重发 | ❌ 新增，待处理 |
| **S3**（次要） | [#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) | Telegram 多图发送时每张图片触发独立请求，导致重复输出 | ❌ 无关联 PR |

**重点提醒**：`#5903`、`#7733`、`#7623` 与 `#8312` 尚未有关联修复，维护者需优先评估风险。

---

## 6️⃣ 功能请求与路线图信号

社区提交的功能请求显著集中在**安全基础设施**、**WASM 原生化**和**智能体编排**领域，与项目路线图高度吻合：

- **多租户与认证**
  - [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) per‑sender RBAC → 与 [#8044](https://github.com/zeroclaw-labs/zeroclaw/issues/8044)、[#7743](https://github.com/zeroclaw-labs/zeroclaw/issues/7743)、[#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238) 共同构成委托/授权体系。
  - [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) OIDC + [#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076) 本地密码认证 → 可插拔 `AuthProvider` 已成型。

- **插件与运行时**
  - [#6943](https://github.com/zeroclaw-labs/zeroclaw/issues/6943) / [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) / [#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135) / [#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822) 系列推动 **WASM‑first 插件运行时**，涉及组件模型、OCI 分发、签名与生命周期钩子。
  - [#6140](https://github.com/zeroclaw-labs/zeroclaw/issues/6140) 混合技能+WASM 工具 → 将技能指令与 WASM 二进制捆绑交付。
  - [#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187) 能力门控 WASI 硬件访问。

- **智能体能力**
  - [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) 提示触发安装 → UX 改进。
  - [#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226) per‑agent 自定义环境变量。
  - [#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) OpenRouter 多模型回退 → 已有 **双 PR**（[#8141](https://github.com/zeroclaw-labs/zeroclaw/pull/8141)、[#8207](https://github.com/zeroclaw-labs/zeroclaw/pull/8207)）实现，有望合入 v0.9.0。
  - [#8310](https://github.com/zeroclaw-labs/zeroclaw/issues/8310) 移除废弃 `prompt_injection_mode` → 对应 PR [#8313](https://github.com/zeroclaw-labs/zeroclaw/pull/8313) 已提交。

- **架构方向**
  - [#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489) “一切皆插件”长期路线。
  - [#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309) 决定 SkillForge 去留。

这些请求大多已获 `status:accepted` 或有对应实现 PR，表明维护团队正积极向 **v0.9.0** 推进。

---

## 7️⃣ 用户反馈摘要

从 Issue 描述和讨论中提炼的普遍痛点与使用场景：

- **📸 媒体消息处理混乱**  
  用户在 Telegram 发送多张图片时收到多次智能体回复（[#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)）；媒体组（media group）也未合并为一个请求（[#7873](https://github.com/zeroclaw-labs/zeroclaw/issues/7873)）。

- **🔄 MCP 子进程泄漏**  
  “运行一天后系统提示达到进程上限” —— `heartbeat.enabled` 默认开启导致 stdio MCP 进程不断累积（[#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)）。

- **🔒 安全配置形同虚设**  
  管理员配置了 per‑agent `mcp_bundles`，但运行时不生效，所有 MCP 工具仍全局可见（[#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733)）。

- **🔑 API Key 跨委托泄露**  
  Codex/OAuth 子智能体使用的是父协调器的 Key，而非自身的凭据（[#7623](https://github.com/zeroclaw-labs/zeroclaw/issues/7623)）。

- **🖼️ 附件引用丢失**  
  在 Matrix 等渠道中，用户先发图片指示“等待”，后续询问时机器人无法识别该图片（[#8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151)，已修复）。

- **👤 缺乏无 IdP 登录**  
  社区成员希望在没有外部身份提供者的情况下，仅使用用户名+密码从浏览器登录管理面板（[#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076)）。

- **🔧 技能/插件发现困难**  
  “我知道 ZeroClaw 有技能插件，但要自己翻阅文档才知道有哪些可用” —— 用户期望按需提示安装（[#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)）。

---

## 8️⃣ 待处理积压

以下 Issue 和 PR 长期处于打开状态，或缺少维护者响应，建议重点关注：

| 类型 | 编号 | 创建时间 | 简述 | 等待原因 |
|------|------|----------|------|----------|
| Issue | [#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) | 2026‑04‑08 | Telegram 多图独立请求 (S3, accepted) | 已有初步调查，但无 PR |
| Issue | [#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) | 2026‑04‑10 | Cron pre‑hook 跳过门控 (accepted, blocked) | 依赖基础架构，无进展 |
| Issue | [#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) | 2026‑04‑19 | MCP 子进程泄漏 (risk: high) | 严重性高但尚未分配 |
| Issue | [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | 2026‑04‑22 | Per‑sender RBAC (accepted, p2) | 设计复杂，尚无实现 PR |
| Issue | [#6250](https://github.com/zeroclaw-labs/zeroclaw/issues/6250) | 2026‑05‑01 | `require_auth` 抽取为路由中间件 (p1, accepted) | 是 #7141 的前置，未开始 |
| Issue | [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) | 2026‑06‑15 | `mcp_bundles` 运行时忽略 (S2, risk: high) | 近两周无响应 |
| PR | [#7928](https://github.com/zeroclaw-labs/zeroclaw/pull/7928) | 2026‑06‑18 | WASM 组件模型插件宿主代码 (XL, risk: high) | 等待 maintainer review |
| Issue | [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) | 2026‑06‑22 | 供应链签名 RFC (needs‑maintainer‑review) | 等待架构决策 |
| Issue | [#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226) | 2026‑06‑23 | per‑agent 环境变量 (needs‑author‑action) | 作者未回复 |

---

*以上为截至 2026‑06‑25 的 ZeroClaw 项目动态。项目正处在安全硬化与 WASM 生态建设的关键时期，社区参与积极，维护者应把握当前 momentum，优先处理 S2/S1 级别的 Bug 及阻塞性的安全 RFC。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*