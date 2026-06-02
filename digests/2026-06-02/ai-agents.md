# OpenClaw 生态日报 2026-06-02

> Issues: 459 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-02 03:39 UTC

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

好的，以下是根据 OpenClaw 项目 2026-06-02 的 GitHub 数据生成的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-02

### 1. 今日速览

过去 24 小时，OpenClaw 项目持续保持极高活跃度，共产生 459 条 Issue 更新和 500 条 PR 更新，显示出社区参与度和维护团队工作量的巨大规模。项目发布了两个 v2026.6.1-beta 版本，重点修复了 Codex 运行时稳定性及跨渠道消息投递问题。尽管修复工作推进迅速，但多个与 Codex 运行时相关的 P1 回归问题仍在追踪中，表明目前在代码重构和运行时切换（从 Pi 到 Codex）期间，系统稳定性面临一定挑战。社区热点集中在 Codex OAuth、会话 SQLite 迁移以及模型兼容性等领域。

### 2. 版本发布

项目在今日发布了两个小版本，均为 v2026.6.1 的 Beta 版本，修复内容高度一致。

- **v2026.6.1-beta.2** 与 **v2026.6.1-beta.1**
  - **亮点**:
    - **运行时稳定性提升**：修复了 Agent 和 CLI 后端运行时在中断的工具调用、过期会话绑定、压缩交接及媒体投递重试等情况下的恢复能力。相关的合并拉取请求（PR）包括 #88129, #88136 等。
    - **消息渠道改进**：提升了 Telegram、WhatsApp、iMe、Slack（仅 beta.1 提及）等渠道的稳定性。
  - **破坏性变更与迁移注意事项**: 发行说明中未提及明确的破坏性变更或迁移步骤。用户可直接升级。鉴于版本号为 beta，建议在非生产环境先行测试。

> **分析师观点**：本次发布的重点在于“稳定性修复”，而非新功能，表明团队正在集中精力解决系统在运行中暴露出的各类异常场景。这是项目从快速迭代转向稳定化的重要信号。

### 3. 项目进展

今日合并或关闭的 PR 主要聚焦于修复关键 Bug 和清理技术债务，项目整体向更稳定、更安全的方向迈进。

- **关键修复与功能推进**:
  - **#89305** [fix(agents): bypass stale auth for plugin harnesses]: 修复了非 Codex 插件运行时因陈旧认证信息导致的故障，确保第三方工具链能正常工作。这对于生态发展至关重要。
  - **#89308** [fix(doctor): exclude platform-incompatible skills from missing requirements count]: 修复了医生（Doctor）命令的误报问题，避免了在 Windows 上报告 macOS 专用技能为“缺失依赖”，从而使用户能聚焦于真正需要修复的错误。
  - **#89307** [fix: remove dangerouslyForceUnsafeInstall gateway override]: 移除了一个有安全风险的网关覆盖选项，收紧了插件安全扫描的防线，提升了系统安全性。

### 4. 社区热点

今日讨论最活跃的议题反映了用户对**运行时稳定性、模型兼容性和关键功能迁移**的深度关注。

- **#80171 [CLOSED] [RFC] Codex-vs-Pi runtime parity QA harness**：作为 Codex 成为默认运行时的大规模 QA 计划追踪贴，以 15 条评论成为最热门议题。说明社区对 Codex 运行时与原有 Pi 运行时的一致性高度关注，社区用户（如`100yenadmin`）深度参与了测试和验证工作。
  - [链接](https://openclaw/openclaw Issue #80171)

- **#80380 [OPEN] [Feature]: updating openclaw to use gemini-3.1-flash-lite**：14 条评论反映了用户对及时跟进最新、更优模型的强烈需求。用户（`akessel56`）主动报告了 Google 模型的 GA 状态并建议迁移，表明社区对模型选择和 API 更新的敏感性。
  - [链接](https://openclaw/openclaw Issue #80380)

- **#88838 [OPEN] [tracker] Track core session/transcript SQLite migration via accessor seam**：12 条评论。这是一个架构层面的重大变更追踪贴。社区对该迁移的方案（分支抽象法）讨论深入，共识度高，表明开发者对以可控、可审查的方式完成数据库迁移有普遍共识。
  - [链接](https://openclaw/openclaw Issue #88838)

- **#84038 [CLOSED] [Bug]: doctor --fix silently migrates intentional openai-codex/ config**：12 条评论，获得 3 个赞。`doctor --fix` 命令“好心办坏事”，自动修复破坏了用户的主动配置，导致严重的 token 浪费。用户“danielsan1”详细记录了问题，社区对此类“破坏性自动修复”情绪强烈，认为其是“最糟糕的更新体验”。
  - [链接](https://openclaw/openclaw Issue #84038)

- **#86820 [CLOSED] [Bug]: Codex OAuth compaction falls back to direct OpenAI API**：12 条评论，获得 6 个赞。高赞说明这是很多用户的痛点。用户报告了 Codex OAuth 在压缩操作时异常回退到需要 API Key 的直接调用，导致认证失败。这暴露了认证和回退逻辑之间的边缘情况。
  - [链接](https://openclaw/openclaw Issue #86820)

### 5. Bug 与稳定性

今日 Bug 报告集中在 Codex 运行时、消息重复和特定渠道（飞书、Telegram）的稳定性上，严重程度较高。

- **P1 (Critical) 级别**:
  - **#86519 [OPEN] [Bug]: Agent repeats identical replies 2-10x on Telegram after 5.20 update**：严重的消息重复问题，影响用户体验。虽在后续版本中部分修复，但未根除。**无已关联的修复 PR**。
    - [链接](https://openclaw/openclaw Issue #86519)
  - **#88312 [OPEN] [Bug]: [Regression] Codex app-server turn-completion stall returns**：Codex 运行时“轮次未完成”的回归问题，与之前已修复的 #84076 同源，表明修复不完善。这是一个影响核心对话流畅度的严重回归。**可能存在修复**（参考 PR #89290）。
    - [链接](https://openclaw/openclaw Issue #88312)
  - **#88234 [OPEN] [Bug]: Feishu dispatch: TypeError**：飞书（Feishu）消息投递因空指针异常崩溃，导致服务不可用。**已有修复 PR**（可能为 #89172 相关）。
    - [链接](https://openclaw/openclaw Issue #88234)
  - **#88592 [OPEN] [Bug]: Control UI card settings don't persist + drag to running fails**：控制面板（Control UI）核心功能（看板）的交互问题，数据不持久化，严重影响使用。**无已关联的修复 PR**。
    - [链接](https://openclaw/openclaw Issue #88592)
  - **#89139 [OPEN] [Bug]: webchat creates new agent run per message, destroying prompt cache**：WebChat 会话未复用，导致模型 Prompt 缓存命中率从 93% 骤降至 29%。这是一个严重的性能问题，直接导致成本增加和响应变慢。**无已关联的修复 PR**。
    - [链接](https://openclaw/openclaw Issue #89139)

- **P1 (Regression) 回归问题**:
  - **#88369 [OPEN] [Bug]: isolated cron can still self-conflict on a dedicated cron agent**：Cron 任务在隔离 Agent 上仍存在资源竞争，修复不彻底。**无已关联的修复 PR**。
    - [链接](https://openclaw/openclaw Issue #88369)

### 6. 功能请求与路线图信号

今日收集到的功能请求集中在**模型提供者扩展**和**开发者体验**上。

- **#89265 [OPEN] [Feature]: More local providers**：用户明确提出希望将本地模型作为“一等公民”对待。结合近期开源模型的蓬勃发展（如 Qwen3 等），这一诉求可能推动项目路线图优先考虑对本地推理后端的更好支持。**纳入可能性：高**。
  - [链接](https://openclaw/openclaw Issue #89265)

- **#79458 [OPEN] [Feature]: Add i18n fields for slash command descriptions**：为斜杠命令描述增加国际化支持。这是一个社区呼声很高的诉求，尤其是对非英语用户。已有相关 PR 在讨论。**纳入可能性：中高**。
  - [链接](https://openclaw/openclaw Issue #79458)

- **#79077 [OPEN] [Feature]: Support for Telegram bot-to-bot and guest-bot modes**：跟进 Telegram 平台最新功能，保持渠道能力前沿。这需要对接 Facebook 新的协议，开发量不确定。**纳入可能性：中**。
  - [链接](https://openclaw/openclaw Issue #79077)

- **#35203 [OPEN] [RFC] Multi-Agent Collaboration Enhancement**：这是一个涉及多 Agent 深度协作的 RFC，提出了能力画像、共享黑板、分层内存和 Token 成本治理等概念。虽然很早就提出，但至今仍在讨论，可能预示该功能复杂度高、优先级较低，但代表了项目长期愿景。**纳入可能性：低 (远期路线图)**。
  - [链接](https://openclaw/openclaw Issue #35203)

- **#14438 [OPEN] [Feature]: Plugin hot-reload**：插件热重载功能。该 Issue 从 2026 年 2 月提出，至今仍被标记，且 PR #89307 移除了安全绕过选项，可见插件加载安全性和开发体验的平衡是个难点。**纳入可能性：低 (短期内需解决安全模型)**。
  - [链接](https://openclaw/openclaw Issue #14438)

### 7. 用户反馈摘要

从今日的 Issue 评论中，可以勾勒出用户群体的典型画像和主要痛点：

- **典型用户场景与痛点**：
  - **VPS 自部署用户**：以 `brokemac79` 和 `adamamzalag` 为代表，他们运行 live VPS，对版本升级非常敏感。升级到 2026.5.27 后立即遭遇 Codex 运行时拒绝模型（#88102）或轮次超时（#87744），迫切需要一个稳定可靠的更新渠道。
  - **跨平台用户**：`HOUHANLIN` 和 `Skeptomenos` 等用户使用 macOS，因 Node.js 版本升级（v24->v26）导致 Discord 网关和 HTTP 请求解析失败（#79752, #79794）。这要求项目在版本兼容性上做更严格的测试或提供更清晰的版本要求说明。
  - **企业或团队用户**：`lawong888` 在调试微信插件时，发现插件加载器对错误信息不够明确，导致“花费数小时”调试。这指向了插件开发者在平台上的糟糕体验，影响了生态发展（#78301）。
  - **Windows 用户**：`Alix-007` 提交的关于 `doctor` 命令误报的 PR (#89260)，反映了 Windows 用户群体虽小众但存在，且受到了不一致体验的困扰。

- **用户满意/不满意的地方**：
  - **满意**：社区对项目团队积极响应的态度表示认可。例如，`w3-design1` 在报告消息重复问题（#86519）时提到，“升级到 2026.5.22 减少了严重程度”，表明修复工作是有效的。`jalehman` 发起的 SQLite 迁移追踪贴（#88838），获得了开发者的建设性讨论，显示社区对技术方案的认可。
  - **不满意**：用户对 `doctor --fix` 这类自动化操作“破坏”他们的配置表示强烈不满（#84038），期望此类功能提供更透明的预览或更细致的控制。`yair` 在报告 Codex 回归问题（#88312）时，明确指出这是“已修复问题的回归”，这种“修了又坏”的循环极大地消耗了用户的信任。

### 8. 待处理积压

以下是从堆积的 Issue 中筛选出的，长期未获响应但可能影响重大或代表用户长期诉求的议题，提醒维护者关注。

- **#35203 【长期积压-RFC】Multi-Agent Collaboration Enhancement**：2026-03-05 提出，P2。这是一个宏大的功能RFC，但近3个月未有任何维护者回复。考虑到多 Agent 工作流是产品的核心竞争力，此 RFC 不应被忽视，至少需要维护者给出初步的反馈和规划优先级。
  - [链接](https://openclaw/openclaw Issue #35203)

- **#14438 【长期积压-功能】Plugin hot-reload**：2026-02-12 提出，P3。热重载是提升开发体验的关键，对构建强大的插件生态至关重要。虽然近期合并的 PR #89307 移除了一个危险的安全绕过，此功能仍处于“需要决策”阶段。建议将生态建设提上日程。
  - [链接](https://openclaw/openclaw Issue #14438)

- **#79752 【中等Priority】gzip decompression failure on Node v26**：2026-05-09 提出，属于 Bug。机器自动标记为 `stale`。随着 Node 26 逐渐铺开，这个兼容性问题只会越来越严重。当前仅有用户互助，缺乏官方解决方案。
  - [链接](https://openclaw/openclaw Issue #79752)

- **#78301 【中等Priority】Plugin loader silent failures**：2026-05-06 提出，P2。这是一个直接的开发者体验痛点。若项目希望吸引更多第三方插件开发者，提供清晰的错误信息是基础。
  - [链接](https://openclaw/openclaw Issue #78301)

- **#77666 【中等Priority】Feishu group messages receive replies=0**：2026-05-05 提出，P1。飞书群聊无回复的问题，从 5 月 3 日版本就存在，至今仍未解决。对于使用飞书作为主要办公协作的用户群体，这是一个很大的困扰。
  - [链接](https://openclaw/openclaw Issue #77666)

---

## 横向生态对比

# AI智能体与个人AI助手开源生态横向对比分析报告

**报告日期：2026-06-02 | 数据来源：各项目GitHub社区动态**

---

## 1. 生态全景

今日开源个人AI助手/自主智能体生态整体处于**高强度迭代与质量巩固并行**的阶段。核心项目（OpenClaw、ZeroClaw、Hermes Agent、NanoBot）均保持日均上百次Issue/PR更新的超高活跃度，焦点集中在**运行时稳定性修复、模型兼容性打磨、Token消耗优化、以及WebUI向工作台演进**。同时，社区对**多Agent协作、安全沙盒、WASI插件标准化**等前瞻方向表现出强烈兴趣。值得注意的是，多个项目不约而同地强调**本地模型与私有化部署**的支持（Ollama、RISC-V、容器化），反映出用户正从“API调用者”转向“基础设施自建者”。生态整体健康，但对稳定性的敏感度已达新高——任何“修了又坏”的回归都会引发用户信任危机。

---

## 2. 各项目活跃度对比

| 项目 | Issue动态数 | PR动态数 | 版本发布 | 健康度评估 |
|------|------------|----------|----------|------------|
| **OpenClaw** | 459项更新 | 500项更新 | v2026.6.1-beta.2 / beta.1 | 极高密度的修复与追赶，稳定挑战中积极应对 |
| **NanoBot** | 62项总更新（含Issue/PR） | 同上 | v0.2.1（WebUI工作台） | 高度活跃，版本迭代强劲 |
| **Hermes Agent** | 50项更新 | 50项更新 | 无 | 快速修复，模型选择器Bug等已落地 |
| **PicoClaw** | 7项更新 | 11项更新 | nightly | 健康，小幅修复与功能并进 |
| **NanoClaw** | 3项更新 | 6项更新 | 无 | 稳定性隐患迅速响应，生态良好 |
| **NullClaw** | 0（无新Issue） | 1（PR#943待合并） | 无 | 低活跃但维护仍在进行 |
| **IronClaw** | 数据不可用 | 数据不可用 | — | 摘要生成失败，无有效动态 |
| **LobsterAI** | 0新Issue | 50个PR合并 | 2026.6.1 | 开发吞吐高，但社区公开讨论冷清 |
| **TinyClaw** | 0 | 0 | 无 | 停滞，过去24小时无活动 |
| **Moltis** | 0新Issue | 3个PR合并 | 无 | 低活跃，但架构重构扎实落地 |
| **CoPaw** | 未明确（高活跃） | 未明确（高活跃） | v1.1.10正式版 + beta2 | 高度活跃，引入子代理等重要特性 |
| **ZeptoClaw** | 1新Issue | 18个PR处理（17合并） | 无 | 安全维护与CI基建升级，健康 |
| **ZeroClaw** | 36项更新 | 37项更新 | 无 | 高强度开发，Provider兼容性大幅改善 |

> *注：动态数指GitHub当日更新（含评论、状态变更等），非严格新增Issue/PR数。*

---

## 3. OpenClaw在生态中的定位

OpenClaw 是当前生态中**体量最大、社区最活跃**的参照级项目（Issue/PR更新数达459/500，远超其他）。其核心定位是**通用型个人AI助手平台**，技术路线从Pi运行时向Codex运行时切换，重点是系统稳定性与插件安全。它对比同类项目呈现以下优势：

- **社区规模**：从Issue评论活跃度、PR数量及用户反馈看，社区覆盖全球个人开发者、VPS自部署用户、企业团队，是生态的“流量中心”。
- **技术路线差异**：OpenClaw 当前聚焦**运行时迁移（Pi→Codex）** 和**大规模回归测试**（#80171），而 NaboBot 侧重 **WebUI工作台化**，Hermes Agent 侧重 **Skills商店与Kanban编排**，ZeroClaw 侧重 **WASI插件化与零代码TUI**。OpenClaw 是唯一在内核运行时层面进行整体替换的大项目。
- **稳定性挑战**：OpenClaw 的 P1 回归问题数量最多（如 Codex 轮次未完成、消息重复），也从侧面反映其功能前沿性——新功能先发，但也因此遇到更多边缘case。相比之下，ZeptoClaw（Rust）通过二进制审计严格控制质量，Moltis 选择在Provider层做显式策略重构以消除歧义。

---

## 4. 共同关注的技术方向

多个项目在同一时间窗口出现了高度重叠的技术议题，按热度排序：

### 4.1 运行时稳定性与切换
- **OpenClaw**：Codex vs Pi 运行时回归问题（#88312、#80171），P1级持续追踪。
- **NanoClaw**：Agent会话因损坏转录崩溃死循环（#2669），依赖 Session 自愈。
- **Hermes Agent**：模型选择器将 OpenAI 错误路由到 OpenRouter（PR #37175）。
- **ZeroClaw**：流式故障回退到非流式通道（PR #6983）。
- **CoPaw**：MCP服务器进程重启累积，Windows浏览器进程残留（#4834、#4844）。

### 4.2 模型兼容性与本地模型支持
- **OpenClaw**：#80380（Gemini 3.1），#80286（自定义模型兼容）。
- **PicoClaw**：#2939/2940（Claude Opus温度参数移除），#2941/2942（模型ID点号修复）。
- **ZeroClaw**：#5962（Ollama工具调用阻塞），#6302（Gemini历史严格模式），#7049（Kimi k2温度400错误）。
- **NanoBot**：#4124（mimo/glm XML工具调用格式错误）。
- **Hermes Agent**：#37105（Bedrock Claude上下文窗口更正为1M）。

### 4.3 Token成本优化
- **ZeroClaw**：#5146（每次对话携带完整SKILL.md，9评论高热度）。
- **Hermes Agent**：#4379（社区自建监控发现73% API调用为固定开销13.9K tokens）。
- **NanoBot**：#4142（缓存未命中时高额API成本讨论）。
- **OpenClaw**：#89139（WebChat未复用会话导致Prompt缓存命中率93%→29%）。

### 4.4 多Agent协作与编排
- **OpenClaw**：#35203（RFC 多Agent协作，长期积压但代表愿景）。
- **NanoClaw**：A2A路由Bug修复（#2331），功能上支持多频道组路由。
- **PicoClaw**：#2937（Agent协作总线PR，含mailbox、协作线程）。
- **CoPaw**：v1.1.10新增`spawn_subagent`临时子代理工具（PR #4806）。
- **Hermes Agent**：Kanban看板快速演进（多PR），成为Agent编排核心。

### 4.5 安全与沙盒
- **OpenClaw**：#89307（移除危险安全绕过），#89308（doctor误报修复）。
- **PicoClaw**：#1042（exec安全门误报合法命令，长期未修复）。
- **ZeroClaw**：#7064（渠道Agent绕过allowed_tools白名单，PR待合并）。
- **LobsterAI**：#1962（添加nsp-clawguard安全监控热开关）。
- **CoPaw**：#4835（单条无效job阻塞整个工作区）。
- **ZeptoClaw**：#594（RUSTSEC安全更新清除了6条违规）。

### 4.6 插件化与可扩展架构
- **ZeroClaw**：#7060（WASI插件接口WIT文件定义，FND-001标准）。
- **OpenClaw**：#14438（插件热重载，长期积压）。
- **LobsterAI**：#2060（Expert Kit Store，插件市场雏形）。
- **Hermes Agent**：Skills 商店从136个技能扩展到88k个（PR #37143）。

### 4.7 WebUI与用户界面
- **NanoBot**：v0.2.1 将WebUI从聊天界面进化为AI工作台（文件编辑、工具轨迹渲染）。
- **OpenClaw**：#88592（Control UI卡片设置不持久化，P1 Bug）。
- **LobsterAI**：#2022（HTML预览优化），#2025（IM Bot管理UI重构）。
- **Hermes Agent**：Kanban看板快速迭代（多PR）。
- **CoPaw**：“打开目录”标签页（v1.1.10），代码模式增强。

### 4.8 渠道扩展
- **PicoClaw**：#2893（新增Server酱³ Bot支持）。
- **CoPaw**：#4848（QQ频道二维码授权，待合并）。
- **OpenClaw**：#88234（飞书dispatch TypeError），#77666（飞书群聊无回复积压）。
- **ZeroClaw**：#7068（Telegram输出内部scratchpad问题）。
- **Hermes Agent**：#25935（Discord图片附件HTTP 400）。

### 4.9 跨平台兼容性
- **PicoClaw**：#2887（RISC-V上.deb无法使用OpenAI模型），#2890（macOS符号链接路径验证）。
- **CoPaw**：#4844（Windows浏览器进程残留），#4875（UV脚本更新重置虚拟环境）。
- **OpenClaw**：#89308（doctor误报macOS专用技能为缺失依赖）。
- **Hermes Agent**：#36208（Docker容器崩溃），#28156（Bedrock配置向导漏洞）。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 全能型AI助手，Agent/CLI/渠道全覆盖，插件生态 | 个人开发者、自部署VPS用户、企业团队 | Python为主，Pi/Codex双运行时，社区规模最大 |
| **NanoBot** | WebUI工作台 + 丰富渠道与Provider配置 | 中轻度用户、希望可视化操作者 | 模块化provider，HuggingFace集成，WebUI优先 |
| **Hermes Agent** | Skills技能商店 + Kanban看板 + 高级Agent编排 | 开发者、深度用户、需复杂工作流者 | dflash Agent，Kanban作为核心编排原语 |
| **PicoClaw** | 轻量级Agent，支持RISC-V/边缘设备 | 嵌入式、低功耗场景、中国开发者（Sipeed） | 体积小、跨架构，支持Server酱等中国特色渠道 |
| **NanoClaw** | 生产级稳定性，A2A多Agent路由，TEE支持 | 企业级用户，需要高韧性部署 | 容器化Sidecar，Provider故障恢复（PR #2666） |
| **NullClaw** | 最小维护，专注Telegram集成 | Telegram重度用户 | 运行安静，仅维护关键修复 |
| **LobsterAI** | 专家Kit商店 + 安全监控 + IM Bot管理 | 网易生态用户、企业办公场景 | Electron客户端，紧密集成cowork/openclaw，高内部开发吞吐 |
| **TinyClaw** | 处于停滞 | — | — |
| **Moltis** | Provider架构标准化，去中心化（NEAR AI TEE） | 开发者、隐私敏感用户 | 显式能力策略路由，推崇Provider回滚/重放韧性 |
| **CoPaw** | 子代理（spawn）+ 代码模式 + 微信/企微深度集成 | 腾讯AgentScope生态、国内企业用户 | 依赖AgentScope框架，Cron Job/Channel管控完善 |
| **ZeptoClaw** | 极致性能（Rust）、二进制体积门控、安全审计 | 性能敏感、安全合规场景 | Rust实现，cargo deny，7MB级二进制，自动依赖更新 |
| **ZeroClaw** | WASI插件化 + 零代码TUI + 广泛Provider兼容 | 插件开发者、跨平台用户、希望定制Agent者 | Rust + WASI标准，渠道/工具/内存插件WIT定义，安全白名单强制 |

---

## 6. 社区热度与成熟度分层

### 第一梯队——快速迭代，日更新 >30 项，社区活跃度极高
- **OpenClaw**（459/500），**ZeroClaw**（36/37），**Hermes Agent**（50/50），**NanoBot**（62总更新），**CoPaw**（高活跃，版本密集）
- 特征：每天数十个PR合并/关闭，同时出现P1回归与新功能，社区讨论热，但也伴随“修了又坏”的信任消耗。

### 第二梯队——稳定推进，日更新 5–20 项
- **PicoClaw**（7/11），**LobsterAI**（50 PR合并但缺社区反馈），**ZeptoClaw**（18 PR），**NanoClaw**（3/6）
- 特征：开发健康，但社区公开讨论偏少；部分项目如LobsterAI属于内部驱动，公开反馈不足。

### 第三梯队——低活跃或停滞
- **Moltis**（3 PR），**NullClaw**（1 PR），**TinyClaw**（0）
- 特征：项目可能处于维护模式或低密度开发阶段；Moltis虽低活跃但重构质量高。

### 成熟度信号
- **进入质量巩固阶段**：OpenClaw beta版本专注稳定性修复、LobsterAI批量合并老PR、ZeptoClaw依赖安全与二进制门控。
- **仍处快速扩散期**：CoPaw频繁发版（1.1.10正式版+beta），NanoBot v0.2.1大幅重写WebUI，ZeroClaw巨型PR #6848（零代码TUI）持续更新。

---

## 7. 值得关注的趋势信号

### 🔴 行业趋势一：Token 成本已成为社区第一性关切
从 Hermes Agent 的73%固定开销分析（#4379）、到 ZeroClaw 每次对话带400行SKILL.md的浪费（#5146）、再到 OpenClaw WebChat 缓存命中率从93%暴跌至29%（#89139）——**社区已从“能否实现功能”转向“能否经济地实现功能”**。这预示着：Agent框架必须在系统层内置上下文编译、技能惰性加载、缓存感知调度等优化。对于开发者，实现透明度高、可配置的Token预算控制将成为产品差异化关键。

### 🟡 趋势二：多Agent协作从RFC走向代码落地
两年前还停留在设计文档层面的多Agent协作，**今天已有多个项目输送可运行代码**：CoPaw 的 `spawn_subagent`、NanoClaw 的 A2A 路由、PicoClaw 的 Agent 协作总线 PR、Hermes 的 Kanban 编排系统。OpenClaw 虽长期积压 RFC #35203 但社区关注度不减。这表明**Agent内部分工与编排**不再是玩具特性，而是生产力系统的核心要求。开发者应关注跨会话上下文共享、代理间通信总线（mailbox）及权限委派设计。

### 🟢 趋势三：WASI 插件标准化起步，可能会统一Agent扩展方式
ZeroClaw 提交了 FND-001 标准的 WIT 文件（#7060），定义了 tool/channel/memory 三类插件的接口。这是行业首个**尝试在Agent框架层做WASM插件标准**的公开信号。加上 OpenClaw 插件热重载（#14438）和 LobsterAI 的 Expert Kit Store，Agent 插件市场正在从“专有API”向“可移植WASI”过渡。对于生态参与者，尽早兼容 WASI 接口可降低后续迁移成本。

### 🟣 趋势四：本地模型与私有化部署的诉求倒逼Provider兼容性
PicoClaw 出现 RISC-V 架构兼容性报告（#2887），Ollama 工具调用阻塞（ZeroClaw #5962），Claude/Bedrock/Gemini 的API差异导致每个项目都在解决参数格式、历史序列化等兼容问题。**用户已经不满足于仅支持 OpenAI，而是希望用同一套框架对接多种本地/第三方模型**。这迫使项目方要么像 Moltis 一样做显式Provider策略，要么像 ZeroClaw 一样大量修复边缘case。对开发者意味着：抽象 Provider 层、模型能力发现、自动参数清洗将是必不可少的架构投资。

### 🟠 趋势五：安全与权限管理从“可以忽略”变为“不可绕过”
ZeroClaw 今天有两个 PR（#7064、#7066）直接修复 Agent 绕过白名单的问题，PicoClaw 安全门误报（#1042）引发社区强烈反响，LobsterAI 新建安全监控热开关，OpenClaw 移除危险安全绕过选项（#89307）。**用户正在把Agent部署到团队协作、甚至生产环境中，注入攻击、数据泄露、权限绕过不再是理论风险。** 安全不再是“加分项”，而是“准入项”。未来半年我们或将看到 Agent 平台引入类似 K8s 的 RBAC 策略以及审计日志标准。

---

*本报告基于2026-06-02各项目GitHub公开数据自动分析生成。IronClaw因数据采集失败未纳入。TinyClaw连续无活动，建议关注其后续重启信号。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot 项目数据生成的 2026-06-02 项目动态日报。

---

## NanoBot 项目动态日报 | 2026-06-02

### 1. 今日速览
今日项目活跃度极高。过去24小时内，总共进行了62次 Issue/PR 更新，并发布了重要的 `v0.2.1` 版本。社区在积极提交新的功能（如QQ频道、新的搜索提供商）和修复报告的同时，维护团队也展现了高效的响应，迅速合并/关闭了17个PR和25个Issue。然而，关于对话历史数据损坏和Agent响应无法送达的 bug 讨论引人关注，显示出在 `v0.2.1` 大版本迭代后，核心稳定性是当前社区的焦点。

### 2. 版本发布
- **v0.2.1**：该版本是项目的一个重要里程碑，标题为“**WebUI becoming the place where work actually happens**”。新版本合并了84个PR，并有17位新贡献者。核心更新集中在 **WebUI** 上，使其从一个单纯的聊天界面进化为一个功能完整的工作台。改进包括：实时的文件编辑活动展示、更精细的工具调用轨迹渲染、更流畅快速的交互体验等。此版本涉及大量内部重构，建议用户在升级前仔细查阅完整的Changelog。无明确的破坏性变更说明。

### 3. 项目进展
今日合并/关闭的17个PR和25个Issue推动了项目的多个方面：

- **核心稳定性修复**：`#4124` 修复了某些模型（mimo/glm）以 XML 格式错误发出工具调用的问题。`#4143` 重构了会话保留逻辑，以解决先前版本中数据归档和丢失的 bug。
- **渠道/通信功能增强**：`#4016` 为钉钉群聊增加了“按用户隔离会话”的配置功能，提升了多用户场景下的体验。`#3723` 合并了本地 Whisper 语音转录功能，为用户提供了无需 API Key 的语音输入选项。
- **WebUI 持续优化**：对 `v0.2.1` 中的新 WebUI 进行了多项修复，包括解决路由刷新问题 (`#4150`) 和助手回复复制失败时提供 fallback 方案 (`#4149`)。
- **平台扩展**：`#4139` 新增了针对 HuggingFace Spaces & ModelScope 的云平台部署层，降低了在这些平台上的部署门槛。

项目正处于一个由新版本驱动的高速开发迭代期，方向明确，即强化 WebUI 为核心的 AI 工作台体验，并扩展渠道和部署能力。

### 4. 社区热点
- **[Issue #2880] `[BUG] 无论发什么消息都回复报错`**：虽然这是一个已经关闭的遗留问题，但18条评论表明这是用户部署初期可能遇到的重大挫折。用户反馈在特定条件下（尤其是在使用 `nanobot agent` 对话正常时）遇到此问题，引发社区广泛关注。
- **[Issue #4006] `[bug] 对话历史包含孤立的工具结果`**：这是今日讨论最热烈的新增问题。它精准地指出了 `v0.2.1` 发布后，在修复了旧 bug 的同时暴露的深层数据一致性问题。该问题会导致API请求被拒，是直接影响 Agent 功能的高优 Bug。
- **[PR #4016] `feat(dingtalk): add group_user_isolation`**：此 PR 获得了大量关注，因为它解决了钉钉用户在实际工作中的核心痛点——群聊上下文混淆。这表明企业级用户是 NanoBot 的重要用户群体。

**分析**：社区的关注点集中在两个方面：一是 **“可用性”** ，包括部署时的障碍和底层数据一致性；二是 **“实用性”** ，如针对特定IM工具（钉钉）的多用户场景优化。这反映了用户正在从“尝鲜”走向“在实际工作中依赖”的转变。

### 5. Bug 与稳定性
- **高严重性**：
  - **[#4006] `nanobot-ai 对话历史包含孤立的工具结果`**：此 bug 破坏了 OpenAI/Anthropic 的 API 规范，可能导致 API 拒绝请求。**目前无明确的 fix PR**，但问题已被社区清晰定义。
  - **[#4133] `工具调用后，Agent响应交付失败`**：Agent 能调用工具并处理结果，但最终无法将回答发送给用户（Telegram）。这是一个关键的用户体验问题，`v0.2.1`中仍有残留。
- **中严重性**：
  - **[#4128] `retain_recent_legal_suffix 导致用户消息被重复归档`**：一个由重构引入的会话管理 bug，可能导致 LLM 上下文不一致。**对应修复 PR #4136 和 #4143 正在进行/已合并。**
  - **[#4147] `append_history 并发写入导致游标重复`**：一个由并发写入导致的历史记录重复 bug，**已有 PR #4147 正在修复。**
- **低严重性**：
  - **[#4069] `Dream 定时任务缺少启用开关`**：`Dream` 功能的配置缺乏 `enabled` 标志，不符合人体工程学。
  - **[#3903] `图片生成功能硬编码 MIME 类型`**：一个关于代码可维护性和健壮性的问题。

### 6. 功能请求与路线图信号
- **新渠道扩展**：`[PR #4146]` 新增 Napcat (QQ) 频道，表明社区对非官方但更强大的 QQ 机器人接入有强烈需求。
- **新搜索/提供商**：`[PR #4141]` 增加了火山引擎搜索提供商，`[PR #4126]` 增加了 Azure AAD 认证，`[PR #4132]` 请求支持自定义图片生成提供商（如 Agnes AI），显示用户在寻求更灵活、更多样化的后端服务集成。
- **功能可控性**：`[PR #4138]` 请求为内置文件系统工具增加 `enable/disable` 开关，与 `exec` 和 `web` 工具对齐。这表明用户希望更精细地控制 Agent 的能力范围，特别是在需要限制模型权限的场景下。

**路线图信号**：管理内存模式 (`[PR #4050]`)、WebUI 语音输入 (`[PR #4122]`) 等 PR 正在开发中，代表了项目未来的重要方向。

### 7. 用户反馈摘要
- **痛点**：
  - **稳定性仍是核心痛点**：`[#4133]` 的用户反馈称 Agent 在 Telegram 上“静默失败”（`The turn ends silently. The user only sees that the last tool result was retrieved...`），这极大地破坏了用户体验。
  - **配置灵活性不足**：`[#4132]` 的用户希望自定义图片生成 API，但当前只支持内置 provider。
  - **Duplication Issues**：`[#3028]` 的用户描述了心跳机制重复创建定时任务的问题，导致问候语重复发送，显得不智能。
- **场景**：
  - **团队协作**：`[#4016]` 的提出者明确了在钉钉群聊中多用户场景下的需求，将 NanoBot 用于团队工作流。
  - **成本控制**：`[#4142]` 的用户发起讨论，关注在缓存未命中时的高额 API 成本，表明用户有在规模化和生产环境中使用，并追求更低成本。
- **满意度**：`[#2406]` 的用户虽然提出了改进建议（跳过无任务时的心跳 LLM 调用），但本质上是对 `Heartbeat` 功能的认可，并希望使其更高效。

### 8. 待处理积压
- **[Issue #4006] `nanobot-ai 对话历史包含孤立的工具结果`**：作为核心数据一致性问题，已经打开7天且无明确修复PR。该问题是 `v0.2.1` 留下的关键稳定隐患，建议维护者优先评估并分配资源。[[链接](HKUDS/nanobot Issue #4006)]
- **[Issue #1932] `技能不支持禁用，只能删除`**：虽然此 Issue 今日被关闭，但它是社区长期以来的一个基本功能诉求，影响用户配置的灵活性。确保该功能在未来版本中得以实现是回应社区期待的重要一步。[[链接](HKUDS/nanobot Issue #1932)]
- **[PR #3994] `refactor: add registry-driven provider config fields`**：这是一项大型重构，旨在通过 WebUI 动态管理提供商配置，对提升可配置性至关重要。尽管已创建一周多，但仍未合并，需要关注其进展。[[链接](HKUDS/nanobot PR #3994)]

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是基于您提供的 GitHub 数据为 Hermes Agent 生成的 2026-06-02 项目动态日报。

---

# Hermes Agent 项目日报 | 2026-06-02

## 1. 今日速览

今日项目活跃度极高，24 小时内累计处理 50 条 Issue 和 50 条 PR，显示出强劲的社区参与度和维护团队的快速响应能力。虽然无新版本发布，但团队密集合并了多项关键修复与功能，包括修复了 v0.15 中模型选择器误路由到 OpenRouter 的严重 Bug、彻底解决了 Docker 容器无法启动的问题，并在 Kanban 看板与 Skills 技能商店系统上进行了大量功能迭代。整体项目健康且正在向 **v0.16** 方向稳步推进。

## 2. 版本发布

> 本日无新版本发布。

## 3. 项目进展

今日合并/关闭了 14 个 PR，涵盖了稳定性修复、功能增强和重大架构改进，标志着项目在用户体验和 Agent 生产化方面迈出了坚实一步。

- **核心稳定性修复：**
    - **[重要]** `fix(model-picker): stop routing OpenAI selection to OpenRouter` ([PR #37175](https://github.com/NousResearch/hermes-agent/pull/37175))：修复了模型选择器将 OpenAI 选项静默路由到 OpenRouter 的问题，解决了无 OpenRouter Key 用户遭遇 401 认证错误的隐患。
    - `fix(cli): TypeError concatenating queued note onto multimodal message` ([PR #37173](https://github.com/NousResearch/hermes-agent/pull/37173) & [#37081](https://github.com/NousResearch/hermes-agent/pull/37081))：修复了在图片消息前置插入 `/model` 等命令时导致 CLI 崩溃的回归 Bug。
    - `fix(agent): allow bounded repeated stall retries` ([PR #35642](https://github.com/NousResearch/hermes-agent/pull/35642))：为 dflash Agent 引入了有限次数的卡死重试机制，替代了原来的一次性重试，大幅提升了任务执行韧性。
    - `fix(honcho): make startup fail open` ([PR #24847](https://github.com/NousResearch/hermes-agent/pull/24847))：解决了 Honcho 内存提供者导致启动阻塞的问题（解决 Issue [#5726](https://github.com/NousResearch/hermes-agent/issues/5726)）。

- **功能增强与 Kanban 看板演进：**
    - `feat(skills): fix browse cap, add source links` ([PR #37143](https://github.com/NousResearch/hermes-agent/pull/37143))：Skills 浏览功能重大升级，从仅显示 136 个技能扩展到完整展示 **88k** 社区技能，并增加了源链接和一键安装按钮。
    - `feat(kanban)` 系列 PR（如 [#37172](https://github.com/NousResearch/hermes-agent/pull/37172), [#37174](https://github.com/NousResearch/hermes-agent/pull/37174)）：修复了看板子任务工作空间继承问题，并引入了通知观察者门控机制，Kanban 系统正快速成熟。
    - `feat(browser): add AgentCookie profile support` ([PR #37154](https://github.com/NousResearch/hermes-agent/pull/37154))：为本地浏览器工具增加了 AgentCookie 配置文件支持，便于复用浏览器状态。

- **其他关键关闭：**
    - Docker 容器 v2026.5.28 启动崩溃问题已获修复 ([Issue #36208](https://github.com/NousResearch/hermes-agent/issues/36208))。
    - WebSocket 绑定 `0.0.0.0` 时被 Dashboard 拒绝的问题已解决 ([Issue #35322](https://github.com/NousResearch/hermes-agent/issues/35322))。
    - Bedrock 上 Claude 4.x 模型的上下文窗口已更正为 1M ([Issue #37105](https://github.com/NousResearch/hermes-agent/issues/37105))。

## 4. 社区热点

今日社区技术讨论和需求表达非常活跃，主要体现在以下事件：

1.  **深度 Token 消耗分析：** `Token overhead analysis` ([Issue #4379](https://github.com/NousResearch/hermes-agent/issues/4379)) 获得 9 条评论。用户自建监控面板发现 **73% 的 API 调用是固定开销**（约 13.9K tokens）。这是社区对基础设施优化的强烈呼吁，揭示了框架层面巨大的优化空间。
2.  **复杂路由场景需求旺盛：** `Multi-Role Auto-Routing` ([Issue #5143](https://github.com/NousResearch/hermes-agent/issues/5143)) 获得了 14 个 👍，并提出 v2 方案。这反映出用户对生产环境中精细化的消息路由和角色管理有极高的期待。
3.  **对新版本的不满：** `v0.15: /model command returns structured field list` ([Issue #35595](https://github.com/NousResearch/hermes-agent/issues/35595)) 成为今日最活跃的 P1 Bug 之一，用户直言 CLI 交互体验“开倒车”。
4.  **辅助 LLM 配置是普遍痛点：** `No auxiliary LLM provider configured` ([Issue #10149](https://github.com/NousResearch/hermes-agent/issues/10149)) 虽然已关闭，但获得了 **16 个 👍**，是今日获赞最多的 Issue，说明多 Provider 配置的门槛依然较高。

## 5. Bug 与稳定性

今日报告了多起 Bug，严重程度分布如下：

**P1 级（高优先级/生产阻塞）：**
- `v0.15: /model command returns structured field list` ([#35595](https://github.com/NousResearch/hermes-agent/issues/35595))：v0.15 CLI 回归，严重影响交互体验，**目前尚无修复 PR**。
- `Discord image attachments fail with HTTP 400` ([#25935](https://github.com/NousResearch/hermes-agent/issues/25935))：Discord 图片附件在混合文件或非特定格式时报错，**待修复**。

**P2 级（中等影响）：**
- `Discord mixed attachments can send non-image data URLs` ([#29711](https://github.com/NousResearch/hermes-agent/issues/29711))：Discord 混合附件图片处理逻辑缺陷。
- `Bedrock+Claude: wizard accepts Bearer-only setup, runtime fails` ([#28156](https://github.com/NousResearch/hermes-agent/issues/28156))：AWS Bedrock 配置向导存在认证方式检测漏洞。
- `Chrome CDP DOM操作在v0.15.1版本后无法正常使用` ([#36211](https://github.com/NousResearch/hermes-agent/issues/36211))：报告了 v0.15.1 升级后 Chrome CDP 自动化出现 JS 变量重复声明错误。
- `Session closed unexpectedly when use camofox as browser tool` ([#20507](https://github.com/NousResearch/hermes-agent/issues/20507))：Camofox 浏览器会话在每次任务结束后立即关闭，无法连续工作。

**今日确认修复的严重 Bug：**
- 模型选择器误路由 OpenAI 请求（[#37175](https://github.com/NousResearch/hermes-agent/pull/37175) **已合并**）
- CLI 在图片消息后执行命令崩溃（[#37173](https://github.com/NousResearch/hermes-agent/pull/37173) **已合并**）
- Docker 容器 v2026.5.28 启动崩溃（[#36208](https://github.com/NousResearch/hermes-agent/issues/36208) **已关闭**）
- Cron 子系统因 `jobs.json` 格式异常完全崩溃（[#36867](https://github.com/NousResearch/hermes-agent/issues/36867) **已关闭**）

## 6. 功能请求与路线图信号

- **Kanban 看板将成为核心编排工具：** 今日密集提交了多个 Kanban 增强 PR，包括“执行器看板” ([#37109](https://github.com/NousResearch/hermes-agent/issues/37109))、看板列状态对齐 ([#37108](https://github.com/NousResearch/hermes-agent/issues/37108)) 以及`目标节点证明门` ([PR #37177](https://github.com/NousResearch/hermes-agent/pull/37177))。这强烈暗示看板系统将在下一个版本中迎来重大升级。
- **成本优化是社区刚需：** `Gemini Flex 推理` ([#12700](https://github.com/NousResearch/hermes-agent/issues/12700)) 的用户请求以及 #4379 的分析都表明，社区对生产环境推理成本的关注度已提上日程，Flex 模式可能会被优先考虑。
- **用户身份与权限系统：** `Dashboard authenticated user identity should propagate to the agent session` ([#35408](https://github.com/NousResearch/hermes-agent/issues/35408)) 要求 Dashboard 的登录身份应下传到 Agent 会话。这是构建多用户 SaaS 平台的必经之路，预计会受到维护者重视。

## 7. 用户反馈摘要

- **强烈不满意：** v0.15 版本的 CLI 交互体验退化（`/model` 命令返回字段名而非可读文本）是今日最集中的用户抱怨。
- **典型痛点：**
    - **第三方平台集成坎坷：** 多用户反映 Discord 和 Bedrock 的配置与运行时存在大量“陷阱”，使用体验远不如 CLI 流畅。
    - **上下文割裂：** 有用户指出 Cron 任务发送的消息在后续交互中完全不可被 Agent 感知，造成了上下文孤岛 (`#37070`)。
- **满意与赞赏：**
    - 社区对 Honcho 启动慢（#5726）和 Docker 崩溃（#36208）等短期迭代 Bug 的快速响应给予正面反馈。
    - 社区的自驱力极强，有用户（Bichev）独立开发了 Token 监控面板并提供了详尽的数据分析，展现了高度技术力的用户生态。

## 8. 待处理积压

以下关键 Issue 或 PR 长时间未得到维护者有效响应或归属，提醒关注：

1.  **Token 开销高企：** `Token overhead analysis` ([#4379](https://github.com/NousResearch/hermes-agent/issues/4379))——用户提供了详尽数据（创建自 4/1），但至今未获官方路线图承诺。此为优化 Agent 成本的重大机遇。
2.  **高级消息路由：** `Multi-Role Auto-Routing` ([#5143](https://github.com/NousResearch/hermes-agent/issues/5143))——高赞功能请求（14 👍），更新了 v2 方案，仍在等待架构评审。
3.  **核心内存配置缺陷：** `Memory char limits ignored by CLI/MCP tool dispatch path` ([#11665](https://github.com/NousResearch/hermes-agent/issues/11665))——创建超过 1.5 个月，涉及核心 Agent 记忆力功能，目前无进度更新。
4.  **Discord 网关超时：** `Discord gateway connect timeout is too short` ([#19776](https://github.com/NousResearch/hermes-agent/issues/19776))——影响 Discord 用户使用，已搁置近一个月。
5.  **Windows 路径兼容：** `fix(file_operations): convert MSYS paths to Windows paths on Windows` ([PR #37180](https://github.com/NousResearch/hermes-agent/pull/37180))——该 PR 对 Windows 用户体验至关重要，今日提交，建议优先审计合并。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw 项目日报 — 2026-06-02**

---

## 1. 今日速览

过去24小时内项目保持高度活跃：共更新7条Issue、11条Pull Request，其中5个PR已被合并/关闭，同时发布了最新的nightly版本。社区围绕exec安全门误报、Claude模型兼容性以及RISC-V平台适配展开讨论。目前有6个PR处于待合并状态，涵盖Agent协作总线、新AI provider等重量级功能，整体呈现“修复与功能并进”的健康态势。

---

## 2. 版本发布

- **`nightly` (v0.2.9-nightly.20260602.426046fc)**  
  基于当前 `main` 分支的自动构建，可能包含尚未正式发布的功能和修复。官方提醒该版本不稳定，请谨慎使用。  
  🔗 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  **破坏性变更**：无明确说明。  
  **迁移注意**：若从 v0.2.9 正式版切换，建议先在测试环境验证。

---

## 3. 项目进展

今日有5个PR被合并/关闭，主要推进了以下功能与修复：

| PR | 说明 | 状态 |
|----|------|------|
| [#2982](https://github.com/sipeed/picoclaw/pull/2982) | fix(bedrock): 对弃用 `temperature` 参数的模型（Claude Opus 4.8）自动移除该字段，解决 Bedrock 调用失败。 | 已合并 |
| [#2977](https://github.com/sipeed/picoclaw/pull/2977) | feat(cron): 为 `cron` 工具新增 `get` 和 `update` 动作，允许代理查看/部分更新持久化定时任务，避免删除重建。 | 已合并 |
| [#2781](https://github.com/sipeed/picoclaw/pull/2781) | perf: 优化技能目录的token注入策略，仅在必要时发送，显著降低多轮对话及tool-call场景的token消耗。 | 已合并 |
| [#2893](https://github.com/sipeed/picoclaw/pull/2893) | feat: 新增 Server酱³ Bot 通道支持（中国流行的推送服务），支持轮询与Webhook模式。 | 已合并 |
| [#2890](https://github.com/sipeed/picoclaw/pull/2890) | fix: macOS 上 `/var` 与 `/private/var` 的符号链接导致路径验证失败，现已修复。 | 已合并 |

此外，仍有6个关键PR处于开放状态，包括 Agent 协作总线（[#2937](https://github.com/sipeed/picoclaw/pull/2937)）、NEAR AI Cloud 集成（[#2917](https://github.com/sipeed/picoclaw/pull/2917)）以及 Claude 模型ID/参数修复（[#2942](https://github.com/sipeed/picoclaw/pull/2942)、[#2940](https://github.com/sipeed/picoclaw/pull/2940)）。

---

## 4. 社区热点

| 话题 | 链接 | 互动热度 | 核心诉求 |
|------|------|----------|----------|
| `exec` 工具安全门误报合法命令 | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | 💬15 👍2 | `guardCommand` 正则过于简单，将含 `..` 但不涉及路径的命令（如 `curl -s "wttr.in/Beijing?T"`）错误拦截，影响正常技能使用。 |
| RISC-V 上 `.deb` 包无法使用 OpenAI 模型 | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | 💬8 | 在 RISC-V 架构的 Debian 上安装的版本与 OpenAI 模型（gpt-5.4）交互异常，疑似编译或依赖问题。 |
| 陈旧PID导致网关启动崩溃 | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | 💬7 | PID 文件被系统其他进程复用，单例检查仅验证 PID 存在而非进程身份，造成循环重启。已有修复PR [#2813](https://github.com/sipeed/picoclaw/pull/2813)。 |
| 历史记录只显示最后一条用户消息 | [#2796](https://github.com/sipeed/picoclaw/issues/2796) | 💬5 | 多轮对话历史中用户只能看到最近一条消息，压缩逻辑影响了前端展示。期待仅压缩LLM上下文，保留用户侧完整记录。 |

社区对安全机制的误伤和平台兼容性最为敏感，同时期望更可靠的后台进程管理。

---

## 5. Bug 与稳定性

以下为主要活跃Bug（按严重程度降序排列）：

| ID | 标题 | 影响 | 修复状态 |
|----|------|------|----------|
| [#2720](https://github.com/sipeed/picoclaw/issues/2720) | 陈旧PID导致崩溃循环 | 高——网关启动失败，影响服务可用性 | [#2813](https://github.com/sipeed/picoclaw/pull/2813) 待合并 |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | RISC-V 上 .deb 版无法使用 OpenAI 模型 | 高——特定架构功能不可用 | 无PR |
| [#2939](https://github.com/sipeed/picoclaw/issues/2939) | `claude-opus-4-7` 因 `temperature` 弃用报400 | 中——该模型调用完全失败 | [#2940](https://github.com/sipeed/picoclaw/pull/2940) 待合并 |
| [#2941](https://github.com/sipeed/picoclaw/issues/2941) | 默认 `claude-sonnet-4.6` 模型ID使用点号被API拒绝 | 中——首次使用即失败 | [#2942](https://github.com/sipeed/picoclaw/pull/2942) 待合并 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | exec安全门误报合法命令 | 中——影响技能执行，用户需关闭安全限制避开 | 暂无PR |
| [#2796](https://github.com/sipeed/picoclaw/issues/2796) | 历史记录只显示最后一条用户消息 | 低——数据呈现不完整，但模型上下文未丢 | 暂无PR |

今日合并的 [#2982](https://github.com/sipeed/picoclaw/pull/2982) 已经修复了 Bedrock 上 Opus 4.8 的温度弃用问题，相似模式可推广至其他 provider。

---

## 6. 功能请求与路线图信号

- **Agent 协作总线** ([#2937](https://github.com/sipeed/picoclaw/pull/2937))：新增代理间 mailbox、协作线程与权限感知通信，是增强多Agent场景的基础设施。若合入，将显著提升 PicoClaw 在多步骤任务编排上的能力。
- **NEAR AI Cloud 集成** ([#2917](https://github.com/sipeed/picoclaw/pull/2917))：添加新的 OpenAI 兼容 provider，支持 TEE 模型建议和动态模型列表拉取，代表对去中心化 AI 生态的扩展。
- **文档同步更新** ([#2981](https://github.com/sipeed/picoclaw/issues/2981))：用户明确要求手册与 v0.2.9 新变更对齐，属于社区呼声较高的任务类需求，但尚未关联PR。
- **exec 安全改进**（源自 #1042 讨论）：社区希望 `guardCommand` 根据命令意图而非简单正则判定路径合法性，可能催生下一代安全沙箱设计。

从当前开放PR质量判断，Agent 协作和 NEAR AI 有较大概率进入下一正式版本，而Claude模型参数修复预计会更早合并以恢复基本兼容性。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中提炼出以下真实用户痛点：

- **安全机制过于僵硬**（#1042）：用户需查询天气，却因命令中含有 `..` 模式（非真实路径）被拦截，不得不关闭 `restrict_to_workspace` 或改用其他工具。建议实现语义级别路径检查。
- **默认配置开箱即崩**（#2941、#2939）：首次启动时若使用 Claude 模型，默认写入的 model ID 和参数违反 API 规范，导致第一次对话即报错，体验极差。用户期望默认值已通过官方验证。
- **RISC-V 部署受阻**（#2887）：用户期待在低功耗平台运行 PicoClaw，但 deb 包存在编译/运行时问题，怀疑 Go 版本或依赖不匹配。该平台未被官方列为支持目标，但社区有明确需求。
- **PID 管理的可靠性焦虑**（#2720）：用户在生产环境遇到因 PID 误判导致的反复重启，缺乏进程自标识机制。已有 PR 但等待维护者合并。
- **历史记录只读不全**（#2796）：用户反馈多轮对话后查看历史只能看到最新一条，怀疑消息压缩“过度”影响前端呈现。期望展示完整用户消息，仅对 LLM 上下文做压缩。

总体而言，用户对功能扩展（Agent协作、新provider）持积极态度，但对基础稳定性（安全门、默认配置兼容性、进程管理）的抱怨较为集中。

---

## 8. 待处理积压

以下为长期未响应或未解决的高价值 Issue/PR，请维护者重点关注：

| 项目 | 类型 | 创建/最后更新 | 备注 |
|------|------|---------------|------|
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) exec安全门误报 | Issue | 2026-03-04 / 2026-06-01 | 评论多、点赞多，但无人认领修复 |
| [#2720](https://github.com/sipeed/picoclaw/issues/2720) PID崩溃循环 | Issue | 2026-04-30 / 2026-06-01 | 高优先级，已有PR [#2813](https://github.com/sipeed/picoclaw/pull/2813) 停留3周未合并 |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) RISC-V 不可用 | Issue | 2026-05-17 / 2026-06-01 | 影响特定平台用户，无进展 |
| [#2796](https://github.com/sipeed/picoclaw/issues/2796) 历史记录显示不全 | Issue | 2026-05-07 / 2026-06-01 | 影响日常使用，无修复PR |
| [#2813](https://github.com/sipeed/picoclaw/pull/2813) PID修复PR | PR | 2026-05-07 / 2026-06-01 | 对应 #2720，待review/merge |
| [#2940](https://github.com/sipeed/picoclaw/pull/2940) + [#2942](https://github.com/sipeed/picoclaw/pull/2942) Claude模型修复 | PR | 2026-05-25 / 2026-06-01 | 解决开箱即崩的配置问题，但已停滞一周 |

这些项目涉及核心稳定性和用户体验，建议尽快排入迭代计划或给出回应。

---

*数据来源：PicoClaw GitHub (github.com/sipeed/picoclaw)，采集时间 2026-06-02 00:00 UTC。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 NanoClaw 项目动态日报。

---

### NanoClaw 项目动态日报 | 2026-06-02

**分析师摘要：** 今日社区活跃度显著上升，共有 **3 个 Issue** 和 **6 个 PR** 获得更新。项目在高优 Bug 修复（A2A 路由）和关键功能开发（浏览器沙盒容器化）上稳步推进，但新提交的稳定性 Bug 值得高度警惕。社区贡献者对新出现的崩溃循环问题响应迅速（24小时内提交修复 PR），展现了良好的“发现即修复”生态。架构层级的大 PR（Provider 故障恢复）进入讨论期，表明项目正在向生产级可靠性迈进。

---

#### 1. 今日速览
今日项目活跃度较高，主要呈现“核心修复与功能推进并行，稳定性隐患显现”的态势。
- **正向进展：** 高优先级的 A2A 路由 Bug (#2331) 成功关闭；浏览器抓取沙盒已成功标准化为 v2 容器 (#2664) 并合并。
- **稳定性预警：** 用户报告了两个严重稳定性缺陷：代理会话因损坏转录硬崩溃死循环 (#2669)，以及单次 MCP 工具调用无超时导致会话长时间挂起 (#2668)。
- **快速响应：** 针对 #2669 崩溃循环的修复 PR (#2670) 已迅速提出，目前处于待合并状态。
- **架构信号：** PR #2666 的提交标志着项目开始系统性考虑 Provider 层故障恢复（回滚与重放）。

---

#### 2. 版本发布
- 今日无新版本发布。

---

#### 3. 项目进展
- **已合并/关闭（今日落地）：**
    - **[PR] 浏览器沙盒容器化：** `#2664` (whahnize) —— 将浏览器抓取 Sidecar 标准化为 v2 容器，完成了该组件的基础设施收敛。
    - **[Issue] A2A 路由 Bug 修复：** `#2331` (glifocat) —— 修复了多频道组中 `findSessionByAgentGroup` 函数按时间排序查找会话导致的回复错乱问题。
- **关键修复推进中：**
    - **[Crash 自愈] #2670：** 提交了针对 `#2669` 的修复，通过注入清空逻辑解决加载损坏背景文件时的死循环问题。
    - **[容器兼容性] #2667：** 修复了 Rootless Podman 及 LXC 环境下因用户权限导致 Claude Code 无法启动的问题，提升部署弹性。
    - **[路径挂载] #2671：** 为代理容器添加只读挂载附件目录，修复 Channel Adapters（如 Slack/Discord）发送附件时路径不存在的 Bug。

---

#### 4. 社区热点
- **最受关注的架构变革（评论潜力最大）：**
    - **`#2666`** 提交的 “Provider failure recovery: rollback, replay, in-turn ack, friendly fallback” 方案，是今日唯一的重量级功能 PR。该 PR 依赖 `#2667` 的容器修复，提出了系统性应对 Provider 故障的韧性方案，预示着未来 Agent 运行时的容错能力将大幅提升。
- **最受瞩目的稳定性修复（响应速度最快）：**
    - **`#2669`** 所描述的崩溃循环场景极为严重（日志显示无休止的 400 错误循环，只能删除会话恢复），迅速获得了 `#2670` 的修复 PR。这种“报告即修复”的节奏反映出社区核心贡献者对关键问题的高度敏感。
- **长期待办的 UX 修复（关注热度不减）：**
    - **`#2346`** (SidhayaPravda618) 关于未知 Slash Command 默认透传导致 Agent 命令被静默丢弃的修复，今日再次被更新（Updated），沉默近一月后出现转机，可能即将进入合并流程。

---

#### 5. Bug 与稳定性
按严重程度排列：

1. **[Critical] 崩溃循环 | #2669** ([链接](nanocoai/nanoclaw Issue #2669))
    - **现象：** Agent 会话因 Resume 时加载了包含损坏 `thinking` 块的 Transcript，导致 Claude API 返回 400 错误且 Runner 陷入无限 “poll-result -> error -> poll” 死循环，无法自愈。
    - **Fix PR：** ✅ 已有 (#2670)，通过注入正则清空损坏的 `thinking` 块以打破死锁。

2. **[High] 工具调用挂起 | #2668** ([链接](nanocoai/nanoclaw Issue #2668))
    - **现象：** Agent SDK 未对单次 MCP 工具调用设置独立超时，且 Runner 仅在外层 Event 循环间隙更新 Heartbeat，导致一个挂起的 MCP 调用能阻塞整个 Agent 会话长达 30 分钟（直至冷杀死锁）。
    - **Fix PR：** ❌ 暂无，该问题需要运行时心跳机制或 SDK 层面的 Per-tool 超时支持。

3. **[Closed/High] A2A 回复路由错误 | #2331** ([链接](nanocoai/nanoclaw Issue #2331))
    - **状态：** ✅ 已修复并关闭。原因为 `findSessionByAgentGroup` 仅按时间取最新活跃会话，在多频道组场景下会将 A2A 回复错误地路由至最近活跃的频道，而非发送请求的原始频道。

---

#### 6. 功能请求与路线图信号
- **P0 级路线图信号：Provider 韧性架构**
    - **证据：** PR `#2666`（依赖 `#2667`）提出了完整的 **Provider 故障恢复** 机制，包括自动回滚/重放请求、显式 ACK 确认、以及优雅降级方案。这明确表明项目下半年的重点将聚焦在 **生产环境的稳定性和自愈能力** 上。
- **部署体验持续优化：**
    - **PR #2667** 对 Rootless Podman 的支持和 **PR #2671** 对附件目录挂载的修复，以及 **PR #2664** 的浏览器容器标准化，共同指向项目正致力于简化部署模型和提升开箱即用体验。
- **可观测性需求萌芽：**
    - **Issue #2668** 要求 Per-tool 超时，这本质上是用户对 **更细粒度运行时观测与控制** 的诉求。未来 Runner 可能需要暴露更多内部状态或支持流式超时配置。

---

#### 7. 用户反馈摘要
- **强烈呼吁系统自愈：**
    - #2669 的提交者 `ddaniels` 提供了一个非常典型的崩溃日志，并明确指出“The only recovery is deleting the session.”。用户期望系统能自动检测并修复此类转录损坏问题，而不是依赖手动删除 Session。*（注：该用户随后自己提交了修复 PR #2670）*
- **对精细控制的需求：**
    - #2668 的 `mshirel` 详细描述了故障场景：“a hung MCP tool blocks the session up to 30 min”。用户对当前“要么全做完，要么全等死”的粗粒度超时机制表示不满，认为 30 分钟的等待窗口在 Agent 调用的场景下完全不可接受。
- **高质量 Bug 报告习惯：**
    - #2331 的 `glifocat` 在报告中直接定位到了具体的 SQL 代码行 `src/db/sessions.ts:56-59`，这种精准的“源码级”反馈体现了核心用户的专业度，极大缩短了维护者的调试路径。

---

#### 8. 待处理积压
- **[长期未合并 PR] `#2346` Fix 未知 Slash 命令** ([链接](nanocoai/nanoclaw PR #2346))
    - **提醒：** 该 PR 由 `SidhayaPravda618` 于 2026-05-08 提交，修复当用户输入未知斜杠命令时 Agent 回应被静默丢弃的体验问题。今天虽被更新，但已搁置 25 天。为了避免后续冲突或社区积极性受挫，建议维护者尽快安排 **Review**。
- **[被低估的稳定性 Issue] `#2668` 缺少工具调用超时** ([链接](nanocoai/nanoclaw Issue #2668))
    - **提醒：** 尽管只有 1 个 😊 表情反应，但在涉及外部资源抓取或复杂 MCP 服务器调用时，30 分钟的阻塞时间是严重的生产事故隐患。如果 #2666 的 Provider 重构进入 sprint，建议将本 Issue 中的超时诉求作为子任务一并纳入考量。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，以下是为您生成的 **NullClaw 项目动态日报（2026-06-02）**。

---

## NullClaw 项目动态日报 | 2026-06-02

### 1. 今日速览

过去24小时，NullClaw 项目保持稳定低活跃度，未产生新的 Issue 或版本发布。唯一值得关注的动态是一条修复 Telegram 集成用户体验问题的 Pull Request (PR #943)。该 PR目前处于待合并状态，表明维护者正在积极响应用户反馈的细节问题。整体来看，项目短期内无重大更新，但社区反馈的处理和代码维护仍在进行中，项目健康度良好。

### 2. 版本发布

无

### 3. 项目进展

**今日无 PR 被合并或关闭，但有一条重要的 PR 处于待合并状态：**

- **PR #943** (+0 / -0)：修复 Telegram 响应指示问题
    - **状态**：Open（待合并）
    - **摘要**：该 PR 解决了用户按下 Telegram 内联按钮（如 `nc_choices` 选项）后，由于缺乏“正在输入…”指示器，导致用户界面在模型处理期间完全静默的问题。这属于对 Agent 交互体验的重要优化。
    - **意义**：虽然尚未合并，但该 PR 通过修复一个具体的用户感知问题，显著提升了 Telegram 集成场景下的用户体验。这是项目在边际改进上迈出的扎实一步。
    - **链接**：[PR #943](https://github.com/nullclaw/nullclaw/pull/943)

### 4. 社区热点

**今日社区讨论的唯一焦点是 PR #943**。

- **链接**：[PR #943](https://github.com/nullclaw/nullclaw/pull/943)
- **分析**：尽管该 PR 只有 0 条评论和 0 个反应，但作为过去24小时内唯一的项目活动，它反映了当前社区的核心诉求。用户期望在等待 Agent 响应时有明确的视觉反馈，而非界面静止。这体现了一种对“即时反馈”和“交互流畅性”的潜在需求，尤其是在多模态或长时间推理场景下。

### 5. Bug 与稳定性

**今日报告 1 个与稳定性/用户反馈相关的 Bug，并有对应的修复 PR。**

- **[高/中] Telegram 界面响应缺失**
    - **描述**：在 Telegram 平台上，当用户通过内联按钮（Inline Button）进行选择后，Agent 在后台处理回调请求（Callback Query）期间，聊天界面没有任何状态变化，用户无法感知系统正在工作。
    - **严重程度**：中。此问题不导致崩溃，但严重影响用户体验和操作确认感。
    - **关联 Issue/PR**：该 Bug 由 #942 报告，并已通过 **PR #943** 进行修复。
    - **链接**：[PR #943](https://github.com/nullclaw/nullclaw/pull/943)

### 6. 功能请求与路线图信号

今日无新的功能请求（Feature Request）提出。

从现有的 PR #943 来看，项目当前的重点偏向于**提升现有功能的用户体验和交互稳定性**，而非引入新特性。这表明下一版本可能会侧重于解决已知的打磨问题，强化与消息平台集成的可靠性。

### 7. 用户反馈摘要

今日的反馈主要集中在 Telegram 这一特定渠道的交互体验上。

- **核心痛点**：用户在 Telegram 上使用 `callback_query` 功能（如菜单选择）时，无法获得操作是否被系统接收以及是否正在处理的即时确认。用户期望 Agent 在思考时能发送“正在输入…”等状态提示。
- **使用场景**：在 Telegram 上使用 Agent 进行任务决策时，需要等待 5-30 秒的模型调用时间。这个空窗期极易让用户产生困惑或重复操作。

### 8. 待处理积压

- **PR #943**：该修复 PR 是解决上述用户痛点的关键，目前为 Open 状态，尚未被维护者合并。提醒维护者关注并尽快审核，以改善 Telegram 用户群体的使用体验。
    - **链接**：[PR #943](https://github.com/nullclaw/nullclaw/pull/943)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**项目名称：** LobsterAI  
**日期：** 2026-06-02  
**数据来源：** GitHub (netease-youdao/LobsterAI)

---

## 今日速览

过去 24 小时内，LobsterAI 合并/关闭了 50 个 Pull Request，发布了一个小版本（2026.6.1），无新 Issue 产生。项目呈现 **高开发吞吐、低社区反馈** 的状态：大量累积的 PR 被集中处理，覆盖语音权限、安全监控、模型控制、UI 优化等多个领域，反映出内部开发节奏较快；但 Issue 端无新提交且评论数据缺失，社区公开讨论热度偏冷。整体来看，项目正处于 **功能密集合并与稳定化阶段**。

---

## 版本发布

- **版本号：** 2026.6.1  
- **发布时间：** 2026-06-01  
- **链接：** [LobsterAI 2026.6.1](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.1)  

### 主要更新内容
- **Expert Kit Store & Conversation Integration**：引入专家工具商店，并实现与对话系统的打通（PR #2060）。
- **插件更新检查**：支持从 npm 和 ClawHub 源自动检查插件更新（PR #2069）。
- **MCP 修复**：修复了 MCP 相关部分问题（原 Release 记录被截断，具体细节需查看 commit）。

### 破坏性变更与迁移注意事项
- Release notes 未标注 Breaking Changes，推测本次版本以功能新增和修复为主，不涉及重大兼容性变动。建议用户在升级后检查插件更新机制是否正常工作，尤其是使用 npm/clawhub 来源的插件。

---

## 项目进展（今日合并/关闭的重要 PR）

过去 24 小时内共有 50 个 PR 被合并/关闭，以下是从评论数最高的 20 个中筛选出的具有代表性进展：

| PR | 领域 | 性质 | 摘要 |
|----|------|------|------|
| [#1952](https://github.com/netease-youdao/LobsterAI/pull/1952) | renderer, docs, main, cowork | fix | macOS 语音输入权限拒绝后显示 toast 提示，提升权限被拒时的用户反馈体验。 |
| [#1962](https://github.com/netease-youdao/LobsterAI/pull/1962) | renderer, main, openclaw, cowork | feat | 在设置中添加 nsp-clawguard 安全监控热开关，用户可动态启用插件级安全监控。 |
| [#1985](https://github.com/netease-youdao/LobsterAI/pull/1985) | renderer, main, cowork | feat | 为聊天会话添加思考级别控制（Off/Minimal/Low/Medium/High/Adaptive），涵盖完整端到端集成。 |
| [#2022](https://github.com/netease-youdao/LobsterAI/pull/2022) | renderer, main, cowork, artifacts | fix | 优化 HTML 预览与源码展示：懒加载、明暗主题适配、预览前校验文件存在性，提升 Artifacts 体验。 |
| [#2002](https://github.com/netease-youdao/LobsterAI/pull/2002) | renderer, artifacts | fix | 修复 Markdown 预览时本地资源路径解析，支持基于 .md 文件目录解析相对引用。 |
| [#2015](https://github.com/netease-youdao/LobsterAI/pull/2015) | renderer, docs, main, openclaw, cowork | fix | 处理 OpenClaw 压缩重试与工具结果间隙问题，提升协议层健壮性。 |
| [#2023](https://github.com/netease-youdao/LobsterAI/pull/2023) | renderer, docs, main, openclaw | feat | 提升 browser 和 webfetch 稳定性和成功率。 |
| [#2025](https://github.com/netease-youdao/LobsterAI/pull/2025) | renderer, main, openclaw, im | refactor | 重新设计 IM Bot 管理 UI。 |
| [#2000](https://github.com/netease-youdao/LobsterAI/pull/2000) | docs, openclaw | fix | 修复 mimo 模型与 Anthropic 格式的兼容性问题。 |
| [#2032](https://github.com/netease-youdao/LobsterAI/pull/2032) | docs, main, openclaw | fix | 修复自定义模型切换时的错误。 |

**总体判断：** 大量 long-standing 的 PR 在此次批量合并中被关闭（最早创建于 5 月 12 日），标志着项目在 **语音交互、安全监控、Artifacts 预览、模型兼容性和浏览器工具稳定性** 方面取得了实质性进步，版本边界向前推进了约 20 天的累积工作。

---

## 社区热点

由于过去 24 小时未产生新 Issue，且已关闭 PR 的评论数与点赞数均为 undefined（或零），无法直接量化社区讨论热度。但从 PR 内容与覆盖团队看，以下 PR 可能在开发内部讨论较多：

- **[#1985 - 思考级别控制](https://github.com/netease-youdao/LobsterAI/pull/1985)**：涉及 UI 交互与完整状态管理，属于用户可感知的控制粒度提升，推测团队在设计思路上有过权衡（6 个级别的具体含义、默认值、迁移方案等）。
- **[#1952 - macOS 语音权限 toast](https://github.com/netease-youdao/LobsterAI/pull/1952)**：直接解决权限被拒后无反馈的问题，体现用户对系统权限透明度的普遍诉求。
- **[#1962 - 安全监控热开关](https://github.com/netease-youdao/LobsterAI/pull/1962)**：引入插件化安全监控，涉及 CoworkConfig 的扩展，反映用户对安全可配置性的潜在需求。

**诉求分析：** 尽管无公开评论，但上述 PR 对应三类用户核心诉求：**更好交互反馈（#1952）、更细粒度的 AI 行为控制（#1985）、以及可管理的安全性（#1962）**。

---

## Bug 与稳定性

今日无新 Bug Issue 报告，但从合并的 PR 中可归纳出以下已修复问题：

| 严重程度 | 问题描述 | 涉及 PR |
|----------|----------|---------|
| 中 | macOS 语音输入权限被拒后无任何反馈 | [#1952](https://github.com/netease-youdao/LobsterAI/pull/1952) |
| 中 | Artifacts HTML 预览显示 Not Found（文件无效）及大文件卡顿 | [#2022](https://github.com/netease-youdao/LobsterAI/pull/2022) |
| 中 | Markdown 预览中相对路径图片无法显示 | [#2002](https://github.com/netease-youdao/LobsterAI/pull/2002) |
| 中 | Browser 配置无效导致功能异常 | [#2031](https://github.com/netease-youdao/LobsterAI/pull/2031) |
| 低 | 自定义模型切换时发生错误 | [#2032](https://github.com/netease-youdao/LobsterAI/pull/2032) |
| 低 | 微信二维码网关重启问题 | [#2014](https://github.com/netease-youdao/LobsterAI/pull/2014) |
| 低 | OpenClaw 压缩重试与工具结果间隙 | [#2015](https://github.com/netease-youdao/LobsterAI/pull/2015) |

以上问题均已通过对应 PR 修复并合并，无待修复的高危崩溃类 Bug。项目稳定性处于 **渐进改善** 状态。

---

## 功能请求与路线图信号

今日无新功能请求 Issue，但已合并的功能 PR 为路线图提供了明确信号：

- **Expert Kit Store**（#2060）：标志着 LobsterAI 开始建设插件/工具集市，预计将成为后续生态扩展重点。
- **思考级别控制**（#1985）：使聊天模型具备可调推理深度，可能为未来高级推理模式（如深度思考、成本平衡）打下基础。
- **插件更新检查**（#2069）：基础架构向包管理对齐，暗示插件将更独立于核心，支持自动更新。
- **IM Bot 管理 UI 重构**（#2025）：即时通讯机器人管理迎来全新界面，可能伴随 IM 功能增强。

**下一版本展望：** 插件系统成熟化、推理控制、安全监控将成为下一迭代的核心方向。

---

## 用户反馈摘要

由于过去 24 小时未有新的 Issue 提交，且已关闭 PR 未捕获用户评论，无法直接从公开渠道提取用户反馈。

**间接推断（从 PR 修复内容看）：**
- macOS 语音输入权限问题（#1952）说明用户在使用场景中遇到过反复点击无反应的沮丧体验，修复将对这部分用户产生积极影响。
- Markdown 图片显示问题（#2002）和 Artifacts 预览问题（#2022）表明文件本地化处理是用户频繁使用的路径，优化后预期提升内容创作者的满意度。

---

## 待处理积压

- **无长期未响应的 Issue**：当前 Issue 列表为空，未发现被忽略的用户问题。
- **无阻塞性待合并 PR**：所有 50 条 PR 均已在今日关闭/合并，队列已清空。

项目维护者可以继续关注更新后的插件系统（Expert Kit Store）以及新的思考级别控制是否会在后续使用中产生用户反馈。

---

*日报自动生成于 2026-06-02，基于 GitHub 公开数据。部分字段（评论数、点赞数）在数据源中缺失，分析已尽力基于可用信息进行推断。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 Moltis 项目数据生成的 2026-06-02 项目动态日报。

---

# Moltis 项目动态日报 | 2026-06-02

## 1. 今日速览
过去24小时内，Moltis项目未产生新的Issue或版本发布，社区讨论进入静默期，整体活跃度评级为“低”。不过，项目开发层面表现扎实：共3项Pull Requests被一次性合并关闭，涵盖核心Provider架构重构、新供应商集成与重要Bug修复。这体现了开发团队在公开讨论平静期的深度打磨与线性推进能力，项目健康度良好，技术债务正在有效消化。

## 2. 版本发布
无（截至今日，项目无新版本发布）。

## 3. 项目进展
今日合并的3个PR均属于关键基础设施与功能扩展，标志着项目在架构稳健性和生态广度上迈出了实质性一步：

- **Provider架构重构（显式能力策略化）** `[#1090](https://github.com/moltis-org/moltis/pull/1090)`
  - **核心变更**：废弃了过往基于URL/Name的试探性行为判断，改为通过明确的“能力策略”来路由和注册Provider。
  - **影响**：极大提升了Provider系统的可预测性，官方Provider与自定义Provider之间的边界更清晰，为后续复杂的模型路由和特性开关铺平了道路。
  - **状态**：已合并（CLOSED）

- **NEAR AI Cloud 供应商集成** `[#1031](https://github.com/moltis-org/moltis/pull/1031)`
  - **核心变更**：新增NEAR AI Cloud作为兼容OpenAI的服务商，支持通过`NEARAI_API_KEY`及`https://cloud-api.near.ai/v1`进行模型发现和TEE感知调用。
  - **影响**：扩展了Moltis对去中心化/隐私计算领域的覆盖，为用户提供了除传统云厂商之外的新选择。
  - **状态**：已合并（CLOSED）

- **OpenAI Codex 工具调用流式修复** `[#1088](https://github.com/moltis-org/moltis/pull/1088)`
  - **核心变更**：处理了Codex Provider在流式推理中，`response.function_call_arguments.done`载荷的捕获与参数增量合成的边缘情况。
  - **影响**：修复了在特定网络条件下工具调用参数丢失的潜在Bug，增强了Agent在生产环境下的稳定性与Diagnose能力。
  - **状态**：已合并（CLOSED）

## 4. 社区热点
今日社区未产生高热度的讨论（所有PR评论数及点赞数均为0）。

虽然缺乏公开讨论，但 **[#1090：Provider显式能力策略](https://github.com/moltis-org/moltis/pull/1090)** 代表了社区核心维护者对底层设计哲学的深度思考。尽管外界感知度低，这类重构通常是项目迈向更高阶可扩展性的必要前提，反映了开发团队在“用户体验”与“底层健壮性”之间的平衡。

## 5. Bug 与稳定性
- **今日新报告 Bug**：0。
- **稳定性修复**：
  - **[#1088](https://github.com/moltis-org/moltis/pull/1088)** 的合并直接修复了OpenAI Codex流式工具调用场景下的一个隐蔽Bug（当流式片段未正常发出时，最终参数无法正确合成）。这修复属于“隐形但致命”的类型，对依赖高级Agent自动化的用户至关重要。

## 6. 功能请求与路线图信号
今日无新增的功能请求。

**路线图信号**：从已合并的PR来看，项目团队目前的战略重心清晰：
1. **去中心化/隐私（TEE）**：引入NEAR AI Cloud表明项目正在有意识地拥抱去中心化计算和隐私保护场景。
2. **架构规范化**：Provider重构是典型的“为未来买单”，暗示下一阶段可能涉及更动态的模型发现、异构计费或复杂的Provider链式调用。

## 7. 用户反馈摘要
今日无直接的用户Issue评论输入。

从间接数据（PR实现）反推，用户对于“非OpenAI”的供应商支持（如NEAR AI）存在客观需求。特别是对TEE（可信执行环境）的支持，暗示了社区中有一部分用户正在探索隐私敏感或具有合规要求的企业级Agent场景。

## 8. 待处理积压
基于提供的数据，无长期未响应的重要Issue或PR积压。近期提交的PR（如 #1031 于5月21日创建，6月1日合并）均得到了高效的处理和关闭，维护者对代码的响应速度令人满意。建议继续保持对旧有低活跃度Issue的巡查清理，保持仓库清洁度。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 CoPaw 项目数据，为您生成 2026-06-02 的项目动态日报。

---

## CoPaw 项目动态日报 | 2026 年 6 月 2 日

### 1. 今日速览

CoPaw 项目今日保持高度活跃，社区参与度强劲。**v1.1.10 版本**的发布标志着项目在 Agent 系统（如临时子代理）和开发模式（如“打开目录”功能）上取得了重要进展。社区讨论最热烈的话题集中在大版本升级（**AgentScope 2.0 迁移**）和 **Windows 平台进程残留**等关键稳定性问题上。尽管有大量 Bug 报告和修复 PR 在并行推进，社区整体对 Agent 生态的完善（如新信息源和技能特性）表现出积极的探索态度，项目健康度良好。

### 2. 版本发布

项目在 24 小时内发布了 2 个版本，其中 **v1.1.10** 为正式版，包含重要新功能。

- **v1.1.10** (正式版)
  - **发布说明**：此版本包含多项增强，重点如下：
    - **✨ Agent 系统**：
      - **临时子代理 (Spawn Subagent)**：新增 `spawn_subagent` 工具，允许在工作空间内执行临时性的子代理任务，极大地增强了 Agent 的灵活性和模块化能力。(PR [#4806](https://github.com/agentscope-ai/QwenPaw/pull/4806))
    - **✨ 代码模式 (Coding Mode)**：
      - **打开目录 (Open Directory)**：新增“打开目录”标签页，用于引用本地项目。
  - **迁移注意事项**：本次版本未提及破坏性变更。建议所有用户升级以获得上述新功能和稳定性改进。升级前请务必参考官方文档核查配置兼容性，并建议在测试环境先行验证。

- **v1.1.10-beta.2** (测试版)
  - 此版本主要集中于错误修复，包括：修复网站头部样式、修复技能（Skill）的标签保留和启用/禁用功能。

### 3. 项目进展

今日合并/关闭了多个重要 PR，推动了项目向稳定性和功能完善迈进。

- **核心稳定性与配置修复**：
  - **PR [#4827] - `fix(config)`** (已合并)：修复了因获取模型 `max_input_length` 逻辑错误导致上下文压缩阈值不正确的问题。这是一个影响广泛的重要修复，确保了长文本处理的准确性。
  - **PR [#4803] - `refactor(cron)`** (已合并)：优化了 `agent` 类型定时任务的推送逻辑，禁用了不必要的弹窗通知，改善了用户体验。
  - **PR [#4867] - `chore(release)`** (已合并)：准备并发布了 v1.1.10 版本。

- **平台适配与集成改进**：
  - **PR [#4848] - `feat(channels)`** (进行中)：为 QQ 频道增加了二维码授权功能，显著降低了用户配置门槛，该 PR 正在审查中。
  - **PR [#4883] & [#4884] - `fix(channel)`** (进行中)：分别修复了定时任务消息在微信/企微渠道的投递问题，以及频道设置保存时监听中断的逻辑问题。

- **测试覆盖**：
  - **PR [#4852] - `test(app)`** (进行中)：新增了 153 个单元测试和契约测试，覆盖 runner 和 4 个高优先级路由，是提升项目质量保障的重要一步。

### 4. 社区热点

以下议题引发了最广泛的社区讨论，反映了用户的核心关切。

- **[Breaking Change] AgentScope 2.0 迁移计划讨论 (Issue #4727)**
  - **链接**：[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)
  - **热度**：5 条评论，2 👍
  - **核心诉求**：这是社区当前最受关注的议题。维护者 `rayrayraykk` 明确提出将后端依赖从 AgentScope 1.x 升级到 2.0，这预示着一次重大的架构变革。用户和贡献者对此高度关注，积极询问规划细节和兼容性影响。同时，关联的 **WIP PR [#4846]** 已开始进行代码迁移工作，表明项目正积极拥抱这一变化。

- **Windows 平台浏览器进程与临时目录锁残留 (Issue #4844)**
  - **链接**：[#4844](https://github.com/agentscope-ai/QwenPaw/issues/4844)
  - **热度**：2 条评论
  - **核心诉求**：用户 `heidis168` 报告了一个影响 Windows 稳定性的严重问题：Agent 调用浏览器后，进程和锁定的临时目录未被清理，导致系统资源耗尽和备份失败。此问题引起了广泛共鸣，并已有 **PR [#4853]** 尝试通过杀死整个进程树来解决，反映出社区对 Windows 平台稳定性的迫切需求。

- **MCP 服务器进程随重启累积 (Issue #4834)**
  - **链接**：[#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)
  - **热度**：3 条评论
  - **核心诉求**：用户 `feng183043996` 报告 MCP 服务器进程在服务重启后未能被正确清理，导致进程堆积和系统变慢。这与 #4844 同样指向进程生命周期管理的问题，是影响高负载环境稳定性的关键 Bug。

### 5. Bug 与稳定性

以下为今日报告的 Bug，按严重程度排列。

- **严重 (Critical)**:
  1.  **对话上下文无限膨胀 (Issue [#4872] - OPEN)**
      - **现象**：新会话直接加载未压缩的原始历史对话，导致上下文无限膨胀。
      - **状态**：暂无直接修复 PR，但关联 PR [#4827] 的合入可能改善模型对上下文长度的感知。
  2.  **Windows 浏览器进程残留 (Issue [#4844] - OPEN)**
      - **现象**：Windows 上 Agent 调用浏览器后进程残留，导致系统不稳定。
      - **状态**：已有修复 PR [#4853] 在审查中。
  3.  **单条无效 job 阻塞整个工作区 (Issue [#4835] - OPEN)**
      - **现象**：`jobs.json` 文件中任何一条无效任务都会导致整个工作区服务启动失败。
      - **状态**：暂无修复 PR。

- **中等 (Major)**:
  1.  **代码模式下无法切换对话 (Issue [#4819])**
      - **现象**：开启代码模式后，切换对话会触发全局刷新。
      - **状态**：问题已关闭，表示已在特定版本修复。
  2.  **Model 配置页面丢失 (Issue [#4666] - OPEN)**
      - **现象**：新建会话后，Model 配置会丢失，页面报错“Load failed”，必须重启应用。
      - **状态**：持续开放中，暂无修复 PR，这是一个自 5 月 25 日以来持续存在的问题。
  3.  **升级后内置技能状态重置 (Issue [#4807])**
      - **现象**：每次升级后，所有被禁用的内置技能都会恢复为启用状态。
      - **状态**：问题已关闭，可能已在 v1.1.10 中修复。

- **低等 (Minor)**:
  1.  **Yuanbao 频道缺少 proto 文件 (Issue [#4890] - OPEN)**
      - **现象**：配置腾讯元宝频道时因缺少 `conn.json` 文件连接失败，疑为打包问题。
  2.  `custom channel` 保存设置时监听停止 (Issue [#4877] - OPEN)
      - **现象**：保存设置时，新 channel 启动与旧 channel 停止顺序错误导致短暂服务中断。已有修复 PR [#4884]。

### 6. 功能请求与路线图信号

以下为新的功能请求，反映了社区对项目未来的期待。

- **核心架构升级**
  - 用户明确提出将 Gen AI 后端升级至 **AgentScope 2.0** (Issues [#4727], [#4885])。这已不是简单的请求，而是由维护者发起、并由贡献者通过 **PR [#4846]** 开始实施的重大路线图项目。

- **新模型与新平台集成**
  - **Xiaomi MiMo**: **PR [#4722]** 正在审查，为平台增加小米的 `token-plan` 服务作为内置提供商。
  - **MiniMax M3**: **PR [#4881]** 正在审查，计划将 MiniMax 的最新的旗舰模型加入内置模型列表。
  - **QQ 频道二维码授权**: **PR [#4848]** 正在审查，旨在简化为频道配置认证。
  - **飞书交互卡片**: **PR [#4879]** 正在审查，以支持解析飞书消息中的交互式卡片内容。

- **用户体验与技能改进**
  - **自进化技能创建 (Self-evolving skill)**: **PR [#4857]** 正在审查，旨在让技能创建流程可以支持后台运行和自我演进。
  - **Agent 范围 Web 登录账号 (Issue [#4859])**: 用户提议在 Web 控制面板中引入更细粒度的账号体系，让用户登录后只能操作自己负责的 Agent。

### 7. 用户反馈摘要

- **正向反馈**：社区对 `spawn_subagent` 和“打开目录”等新功能表现出积极态度。对 `active_model` 配置的澄清需求 (Issue [#4871]) 得到维护者快速回应并关闭，体现了良好的支持响应。
- **痛点与投诉**：
  - **Windows 平台稳定性**：多个 Bug 报告 (如 [#4844], [#4834], [#4731]) 集中指向 Windows 平台上进程管理和清理的不完善，这是当前用户最不满意的领域之一。
  - **升级体验**：用户普遍对升级后配置、功能状态丢失感到困扰 (如 Issue [#4807])，表明升级流程的平滑性有待优化。
  - **学习曲线与配置**：用户在使用高级功能如 Cron Job 共享会话 (Issue [#4818]) 或在 MCP 环境排查问题时遇到了困难，提示相关文档和用户体验需要加强。
  - **安装脚本问题**：用户 `manjieqi` 报告使用脚本更新时，由 UV 创建的虚拟环境会被重置 (Issue [#4875])，导致所有先前安装的包需要重装。

### 8. 待处理积压

- **[Bug] Models 配置页面在新建会话后丢失 (Issue [#4666])**
  - **创建于**：2026-05-25
  - **最后更新**：2026-06-02
  - **状态**：**OPEN**，无修复 PR。
  - **影响**：这是一个严重且持续了一周以上的 Bug，严重影响新用户首次使用或切换工作空间时的体验，需要维护者高度重视并分配资源修复。

- **[Bug] 单条无效 job 阻塞整个工作区 (Issue [#4835])**
  - **创建于**：2026-05-31
  - **最后更新**：2026-06-01
  - **状态**：**OPEN**，无修复 PR。
  - **影响**：该 Bug 会导致容错能力极差，任何简单的配置错误都会导致服务完全不可用，是一个破坏性的稳定性缺陷，需要尽快处理。

- **[Enhancement] 字体大小可调节 (Issue [#4154])**
  - **创建于**：2026-05-09
  - **最后更新**：2026-06-02
  - **状态**：**OPEN**，长期未被解决。
  - **影响**：尽管不是一个 Bug，但这是一个呼声很高的用户体验改进，尤其是对于桌面版用户。过去一个月未分配任何 PR，表明团队当前高优先级仍然在核心功能建设和稳定性修复上。

- **[PR] 添加对话级别 Token 使用量显示 (PR [#4433])**
  - **创建于**：2026-05-15
  - **最后更新**：2026-06-01
  - **状态**：**OPEN**，等待审查。
  - **影响**：这是一个对开发者和管理员非常有价值的特性，能有效帮助监控成本和使用情况。其长期搁置可能消耗贡献者的积极性。

---

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，以下是根据 ZeptoClaw 2026-06-01 的 GitHub 活动数据生成的 2026-06-02 项目动态日报。

---

# ZeptoClaw 项目动态日报 | 2026-06-02

## 1. 今日速览

过去 24 小时内，ZeptoClaw 项目进入了一个高度活跃的维护与修复周期，共处理 **18 个 Pull Requests**，其中 17 个已完成合并或关闭。**核心亮点在于重大生产 Bug 的修复（Provider 路由 100% 错误率）以及大规模依赖库存的刷新（14 个自动合入 PR）。** 此外，维护者通过升级 `lettre` 与 `diesel` 依赖消除了全域 CI 阻塞，并提出了将二进制体积纳入 PR 强制门控的基础设施改造。整体项目健康度良好，短期聚焦于稳定性修复与技术债务清理。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

### 核心稳定性修复合入
- **Provider 路由 Bug 终极修复**：社区贡献者 @Sisuthros 在原 PR #592 中定位了 `infer_provider_name_for_model` 函数的逻辑缺陷（关键词回退未校验配置状态）。由于该分支 CI 复杂，维护者 @qhkm 通过 Cherry-pick 方式创建了 PR #610 并成功合入主线。该 Bug 直接导致 NIM 托管的 Photon 实例在特定模型路由时出现 **100% 错误率**，是近期的关键生产事故源头。
  - **关联链接**：[PR #592](https://github.com/qhkm/zeptoclaw/pull/592) | [PR #610](https://github.com/qhkm/zeptoclaw/pull/610)

### 大规模依赖更新与安全审计
- **RustSec 安全告警清除**：维护者 @qhkm 提交 PR #594，升级了 `lettre`（0.11.22）和 `diesel`（2.3.8）依赖，清除了 2026-05-22 安全公告更新触发的 6 条 RUSTSEC 违规，恢复了全仓库 `cargo deny` CI 的通过状态。
- **Dependabot 自动维护**：共计 14 个自动依赖更新 PR 被成功合并，覆盖：
  - **Rust 运行时**：`uuid`、`bcrypt`、`clap`、`tower-http`、`mail-parser`
  - **前端文档/面板**：`@astrojs/starlight`（两个子站点） `astro`、`eslint`
  - **Docker 基础镜像**：`rust:1.93 -> 1.95`、`debian` 滚动更新
  - **CI 工具链**：`taiki-e/install-action`、`EmbarkStudios/cargo-deny-action`
  - **关联链接**：[PR #594](https://github.com/qhkm/zeptoclaw/pull/594)

### 基础设施与 CI 改造
- **引入二进制体积门控（进行中）**：PR #611 旨在将 `binary-size` 作业从仅推送监测升级为 **PR 强制门禁**。当前 stripped 产物大小约 6.98MB，提案将临时门槛设为 7.5MB，未来目标收紧至 7MB。此改动将直接影响所有开发者的 PR 提交流程。
  - **关联链接**：[PR #611](https://github.com/qhkm/zeptoclaw/pull/611)

## 4. 社区热点

- **Provider Bug 修复流程备受关注**：虽然缺乏评论数据支撑热度，但 #592 / #610 的合入流程是今日社区协作的焦点。由外部贡献者定位根因、维护者迅速扫清合并障碍，体现了项目对外部 PR 的高效吸纳能力。该问题直接关联了真实用户 100% 错误的痛点，关注度极高。
- **二进制体积审计引发技术讨论预期**：新开的 Issue #612 提出了当前产物相对低点 6.2MB 增长了约 800KB 至 6.98MB 的现象，并建议执行审计。虽然暂无评论，但结合 #611 的门控建设，社区有较大概率就此展开关于性能退化的技术探讨。
  - **关联链接**：[Issue #612](https://github.com/qhkm/zeptoclaw/issues/612)

## 5. Bug 与稳定性

| 严重程度 | 标题与描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| **严重** | **Provider 关键词回退导致路由错误**：当模型ID包含关键词时，回退逻辑未检查用户是否实际配置了该 Provider，导致 100% 请求失败。 | **已修复** | [#592](https://github.com/qhkm/zeptoclaw/pull/592) / [#610](https://github.com/qhkm/zeptoclaw/pull/610) |
| **高** | **RUSTSEC 更新导致 CI 全局阻塞**：2026-05-22 安全数据库更新后，`deny.toml` 零容忍策略导致 `cargo deny` 作业报红，阻塞所有 PR。 | **已消除** | [#594](https://github.com/qhkm/zeptoclaw/pull/594) |
| **中** | **二进制体积无感膨胀**：从 6.2MB 的历史低点增长至 6.98MB，增量约 800KB。被标记为 `P2-high`，需排查近期回归原因。 | **追踪中** | [#612](https://github.com/qhkm/zeptoclaw/issues/612) |

## 6. 功能请求与路线图信号

- **CI 流程标准化**：PR #611 提出的二进制体积门控请求，标志着项目开始将“产物质量”纳入自动化监控体系。这通常是项目进入运维优化阶段、准备更严格发布流程的信号。
- **性能回归审计**：Issue #612 请求对二进制体积漂移进行审计。这很可能会作为下一轮小版本迭代（或性能优化 Sprint）的主题，配合 #611 的门控实现有效的体积控制。

## 7. 用户反馈摘要

从 PR #592 的修复背景中，我们可以提炼出以下真实的用户痛点与使用场景：

- **痛点**：生产环境中，用户通过 NIM 部署了自定义或第三方模型（本例为 `openai/gpt-oss-120b`），即便对应的 Provider 未在配置中激活，系统仍因关键词回退机制将请求强制路由至未就绪的 Provider，导致服务 100% 不可用。
- **依赖**：用户重度依赖自动依赖更新（Dependabot）来保持供应链安全，无需手动干预底层依赖升级是一个明显的积极点。
- **稳定性预期**：用户期望项目在处理 Provider 时严格遵循显式配置，不应因模型 ID 的命名规则产生意外路由。

## 8. 待处理积压

以下是当前需要项目维护者关注的 PR 与 Issue，提醒予以跟进：

1.  **【需要关注】** **PR #611：`promote binary-size to PR gate at 7.5MB`**
    - **状态**：Open（已创建 1 天）
    - **说明**：该 PR 将改变所有开发者的 CI 体验。建议尽快完成评审，确认 7.5MB 的临时阈值是否预留了足够的安全余量，避免误伤正常的开发者提交流程。
    - **链接**：[https://github.com/qhkm/zeptoclaw/pull/611](https://github.com/qhkm/zeptoclaw/pull/611)

2.  **【需要关注】** **Issue #612：`Audit ~800KB binary-size drift`**
    - **状态**：Open（已创建 1 天，无人指派，无评论）
    - **说明**：800KB 的净增长（~12% 的膨胀）对于 7MB 级别的二进制是显著的。建议尽快纳入迭代计划或使用专用工具（如 `cargo-bloat`）进行根源分析。
    - **链接**：[https://github.com/qhkm/zeptoclaw/issues/612](https://github.com/qhkm/zeptoclaw/issues/612)

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是为 ZeroClaw 项目生成的 **2026年6月2日** 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-02

## 1. 今日速览
项目今日保持着极高的开发活跃度，过去 24 小时内共有 **36 条 Issue** 和 **37 条 PR** 被更新。其中 **13 个 PR** 被合并或关闭。虽然无新版本发布，但开发重心明显偏向**稳定性加固**（流式回退恢复、路径权限修复）和**渠道与提供商的体验打磨**（Ollama 工具调用、Kimi 兼容性修复）。大型集成 PR（#6848，零代码 TUI & Beta-2 集成）与 WASI 插件接口定义（#7060）持续推进，表明长期架构演化并未停滞。社区反响主要聚焦于 **Token 成本控制** 与 **本地模型兼容性**，项目整体处于 **高强度开发与质量打磨并行** 的健康阶段。

## 2. 版本发布
**无。** 过去 24 小时内无新版本发布。

## 3. 项目进展
今日有 13 个 PR 完成合并，项目在安全、稳定及功能集成方面迈出了新的一步：

- **稳定性与可用性提升**
  - **恢复流式故障回滚路径** ([PR #6983](https://github.com/zeroclaw-labs/zeroclaw/pull/6983))：流式调用在未输出任何内容给客户端前失败时，将自动重试非流式通道，防止静默中断。
  - **Discord 附件失败日志脱敏** ([PR #7031](https://github.com/zeroclaw-labs/zeroclaw/pull/7031))：修复了失败日志中暴露原始文件路径的问题。
  - **邮件通道 SMTP 凭据修复** ([PR #6979](https://github.com/zeroclaw-labs/zeroclaw/pull/6979))：空白 SMTP 凭据将正确回退到 IMAP 共享凭据。
  - **Lean 默认渠道集** ([PR #6904](https://github.com/zeroclaw-labs/zeroclaw/pull/6904))：核心默认构建缩小为标准集（ACP服务 + Webhook + Email + Telegram），控制二进制包体积膨胀。
  - **渠道日期上下文优化** ([PR #6931](https://github.com/zeroclaw-labs/zeroclaw/pull/6931))：将提示词中的时间戳频率从毫秒级调整为分钟/天级，显著减少缓存搅动。

- **安全与权限增强**
  - **`web_fetch` 私有 DNS 白名单修复** ([PR #6974](https://github.com/zeroclaw-labs/zeroclaw/pull/6974))：允许明确配置的私有域名解析通过安全策略。
  - **`image_info` 路径策略强制** ([PR #6972](https://github.com/zeroclaw-labs/zeroclaw/pull/6972))：图片信息提取工具现在强制通过统一的路径守卫进行权限检查。

- **新功能与集成**
  - **新增 Jina AI 搜索提供商** ([PR #6833](https://github.com/zeroclaw-labs/zeroclaw/pull/6833))：用户可在 `web_search` 中使用 Jina AI 的免费 10M 请求额度。
  - **WASI 插件接口定义** ([PR #7060](https://github.com/zeroclaw-labs/zeroclaw/pull/7060))：提交了 FND-001 §5.2 定义的工具、渠道、内存插件的 WIT 文件，是插件化架构的关键设计文档落地。
  - **Kimi k2 系列模型兼容** ([PR #7049](https://github.com/zeroclaw-labs/zeroclaw/pull/7049))：修复因强制发送 `temperature` 参数导致 Kimi-k2 系列 400 错误的问题。

## 4. 社区热点
- **🔥 Token 消耗优化深度讨论（[#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)）**
  **9 条评论，高活跃度。** 用户 jonsmirl 指出每次对话都将完整 400+ 行 SKILL.md 送入 LLM 是巨大的 Token 浪费。社区对“技能编译”方案展开了激烈辩论。这不仅是成本问题，更触及了系统架构层面对动态子图/Skill 的 Loading 策略优化。

- **⚙️ Ollama Provider 工具调用阻塞（[#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)）**
  **6 条评论。** 用户 ufukbakan 反馈使用 Ollama 作为后端时，一旦触发工具调用，会话将完全被阻塞，无法继续。该 Issue 严重等级为 **S1（工作流阻塞）**，反映了本地部署用户对于 Provider 稳定性的极高需求。

- **📢 Gemini 历史序列化严格模式（[#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)）**
  **4 条评论。** Gemini 严格限制 `assistant` 的 `tool_call` 必须出现在 `user` 消息之后，而 ZeroClaw 构造的历史违反了该规则导致 400 错误。这触及了动态 Provider 兼容性协调机制的核心难点。

- **📱 Telegram 通道输出内部日志（[#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068)）**
  用户 sbenedetto 反馈在使用 Codex 作为后端代理时，Telegram Bot 会发回内部的 scratchpad/工具转录日志，而非正常回答。这属于严重的信息外泄和产品体验问题。

## 5. Bug 与稳定性

### 严重（待修复或修复中）
| 严重等级 | Issue / PR | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **S1** | [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | Ollama 工具调用导致会话完全阻塞 | `in-progress` |
| **S1** | [#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155) | 委托代理 (`delegate agents`) 忽略全局 `prompt_injection_mode` 配置 | `in-progress` |
| **S1** | [#7063](https://github.com/zeroclaw-labs/zeroclaw/issues/7063) | 渠道（Telegram/Webhook）智能体完全绕过 `allowed_tools` 白名单，**已提交修复** [PR #7064](https://github.com/zeroclaw-labs/zeroclaw/pull/7064) | 待合并 |
| **S2** | [#6472](https://github.com/zeroclaw-labs/zeroclaw/issues/6472) | Gateway 使用 Postgres 内存后端时因 Runtime 嵌套 Panic | `in-progress` |
| **S2** | [#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) | WhatsApp LID 格式联系人绕过 `allowed-numbers` 白名单配置 | `in-progress` |
| **S2** | [#7059](https://github.com/zeroclaw-labs/zeroclaw/issues/7059) | 渠道协调器保留“默认模型提供商”凭据降级逻辑（V3 架构违规），**已提交修复** [PR #7066](https://github.com/zeroclaw-labs/zeroclaw/pull/7066) | 待合并 |

### 已修复（今日合并）
- **Kimi 模型温度 400 错误**（[#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022)） → 由 [PR #7049](https://github.com/zeroclaw-labs/zeroclaw/pull/7049) 修复，针对 kimi-k2 系列模型已强制省略温度参数。
- **邮件通道空白 SMTP 凭据覆盖**（[#6881](https://github.com/zeroclaw-labs/zeroclaw/issues/6881)） → 由 [PR #6979](https://github.com/zeroclaw-labs/zeroclaw/pull/6979) 修复。
- **`web_fetch` 私有 DNS 白名单绕过**（[#6974](https://github.com/zeroclaw-labs/zeroclaw/pull/6974)） → 已合并。

## 6. 功能请求与路线图信号
- **🎯 高潜力功能请求**
  - **智能体评估框架 (zeroclaw eval)**（[#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065)）：mn13 提出了 Phase 0 实现，包含确定性回放模式与 LLM-as-judge。对应的 [PR #7067](https://github.com/zeroclaw-labs/zeroclaw/pull/7067) 也已提交，是提升系统发布质量的重要基建。
  - **Telegram 通道屏蔽内部 Scratchpad**（[#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068)）：用户提议增加配置，阻止 Codex 后端的内部日志被当作回复发送给用户。
  - **Dashboard 一键更新**（[#6365](https://github.com/zeroclaw-labs/zeroclaw/issues/6365)）：通过 Gateway 暴露 `zeroclaw update` 流程，已标记为 `in-progress`。
  - **TLS 自定义 CA 证书支持**（[PR #5797](https://github.com/zeroclaw-labs/zeroclaw/pull/5797)）：允许连接到使用私有/企业 PKI 的自定义推理端点，是政企部署的刚需。

- **📌 路线图信号**
  - **v0.8.0-beta-2 集成**（[PR #6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)）：XL 级巨型 PR，包含零代码 TUI、RPC Socket 传输、DenyWithEdit 审批等重大变更，仍在密集更新中。
  - **WASI 插件架构**（[PR #7060](https://github.com/zeroclaw-labs/zeroclaw/pull/7060)）：WIT 接口文件的定义提交，表明项目正认真向着模块化/插件化的方向迈进。

## 7. 用户反馈摘要
从今日的 Issue 和 PR 中，可以提炼出用户的几个核心诉求：

1. **成本敏感与效率焦虑**：用户 jonsmirl 在 ([#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)) 中一针见血地指出“每次问天气都要带 400 行 SKILL.md 是巨大的算力浪费”。社区对此反响热烈，表明用户不仅关注功能，更在意 Token 消耗带来的经济成本和延迟。
2. **本地优先布局的阵痛**：Ollama 的 Bug ([#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)) 曝光了本地 AI 场景的用户活跃度，但也反向证明了 ZeroClaw 的 Provider 兼容性在非 OpenAI 主流模型上有较大欠账。
3. **企业级配置与管理需求浮现**：用户对 WhatsApp 白名单绕过 ([#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350))、Discord 频道白名单 ([#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)) 以及渠道命令未采用当前 locale 本地化语言 ([#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)) 等问题的反馈，证明了用户场景正从个人玩具逐步过渡到多团队、多身份的正式部署。

## 8. 待处理积压
以下为长期开放、可能存在停滞风险或需要维护者介入的重要事务：

- **技能发现标准兼容（[#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)）**：自 2026-03-27 开放。需求为支持 `.well-known` URI 安装技能，是为了衔接行业 Agent Skills 标准化的重要接口。虽标为 `accepted`，但迟迟未有开发推进，可能成为生态集成的短板。
- **自定义 TLS 证书支持（[PR #5797](https://github.com/zeroclaw-labs/zeroclaw/pull/5797)）**：自 2026-04-16 起开放。由于 V3 架构的 Provider 层改造仍未定稿，该 PR 处于等待设计评审的回望状态。对于急需对接内部私有模型服务的政企用户影响较大。
- **Token 消耗最小化（[#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)）**：当前社区最热门的话题之一，但优先级仅为 P2。如果社区讨论热度不减，维护者可能需要重新审视其路线图权重。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*