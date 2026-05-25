# OpenClaw 生态日报 2026-05-25

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-25 09:58 UTC

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

好的，以下是基于您提供的 GitHub 数据生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-05-25

## 1. 今日速览

OpenClaw 项目今日处于**极端高活跃**状态，社区开发与反馈节奏空前密集。24小时内总计发生 **500 条 Issue 更新**（新开/活跃 297 条，关闭 203 条）及 **500 条 PR 更新**（待合并 315 条，已合入/关闭 185 条）。项目发布了 2 个 Beta 版本。值得高度关注的是，项目在处理大量功能请求和日常 Bug 的同时，成功快速响应并修复了一起 **P0 级跨用户隐私泄露漏洞**（#85240），展现出较强的安全响应能力。此外，一项**将底层 Agent 运行时从 Pi 完全内化**的架构级重型 PR（#85341）正在推进中，标志着项目走向更高程度的自主可控。

## 2. 版本发布

- **v2026.5.24-beta.2**
  - **核心更新**：新增 iMessage 手势反馈（Tapback）支持。用户发送 `👍` 可将审批解析为 `allow-once`（一次性授权），发送 `👎` 则解析为 `deny`（拒绝）。显式审批人白名单通过 `channels.imessage.allowFrom` 配置读取。`allow-always` 功能仍需通过手动输入文本命令执行。
  - **影响**：极大增强了 iMessage 渠道的操作直观性，将日常交互中的点赞/踩直接映射为安全审批动作。
- **v2026.5.24-beta.1**
  - **核心更新**：网关性能优化。重用进程稳定的频道目录读取，避免重复的捆绑频道边界检查；轮换网关 CPU 性能分析文件以防止长期运行导致磁盘膨胀。
  - **影响**：提升了多频道运行环境下的吞吐量和稳定性，并优化了开发/运维过程中的磁盘空间管理。

## 3. 项目进展

过去 24 小时，开源社区贡献了大量高质量的代码和修复，项目整体稳步向前迈进了一大步：

- **重大架构重构**：PR [#85341](https://github.com/openclaw/openclaw/issues/85341)（**内化 OpenClaw Agent 运行时**）取得关键进展。该 PR 移除了对旧版 Pi 运行时的依赖，将 Agent 执行、模型/提供商路由等功能完全重写为 OpenClaw 自有核心。这是项目走向成熟化和独立化的重要里程碑。
- **安全防线紧急加固**：
  - Issue [#85240](https://github.com/openclaw/openclaw/issues/85240) **P0 跨用户隐私泄露** 被成功修复并关闭，回应速度极快。
  - PR [#84338](https://github.com/openclaw/openclaw/issues/84338)（修复 Hook 令牌可绕过密码模式网关认证）已进入自动合并准备阶段，这是一项关键的认证安全修补。
- **稳定性修复成果显著**：
  - Issue [#68944](https://github.com/openclaw/openclaw/issues/68944)（CLI 命令在 WebSocket 握手时挂起）已被关闭。
  - Issue [#84945](https://github.com/openclaw/openclaw/issues/84945)（LLM 空闲超时错误被静默丢弃）已被关闭。
  - Issue [#85048](https://github.com/openclaw/openclaw/issues/85048)（启动时大量内置插件 manifest-id 不匹配警告）已被关闭。
- **代码质量与测试覆盖**：
  - PR [#86419](https://github.com/openclaw/openclaw/issues/86419) 重构了共享的强制转换/提取辅助函数，提升了跨模块的代码复用度。
  - PR [#86429](https://github.com/openclaw/openclaw/issues/86429) 增加了对 `node-cli` 守护进程安装和生命周期路径的测试覆盖。

## 4. 社区热点

今日社区讨论异常激烈，主要聚焦于提升用户体验和增强平台能力：

- **🔥 呼声最高：桌面客户端与基础体验**
  - [#75](https://github.com/openclaw/openclaw/issues/75) **Linux/Windows Clawdbot Apps**：以 **106 条评论和 77 个 👍 高居榜首**。社区对完善桌面端（特别是非 macOS 系统）体验的渴望已经到了极致，这是项目拓展用户基数的核心卡点。
  - [#9443](https://github.com/openclaw/openclaw/issues/9443) **请求提供预构建 APK**：拥有 25 条评论。用户对直接从源代码构建感到不便，强烈要求在 Release 中提供开箱即用的 Android 伴侣应用。

- **✍️ 功能设计激烈讨论**
  - [#68596](https://github.com/openclaw/openclaw/issues/68596) **可配置流看门狗超时阈值**：13条评论，8 👍。用户普遍反映使用 DeepSeek-R1、Kimi 等擅长长思考的模型时，看门狗频繁误报，急需灵活的配置项。
  - [#18160](https://github.com/openclaw/openclaw/issues/18160) **Direct Exec 模式**：12条评论，9 👍。高级用户对 Cron 任务依赖 LLM 解释执行的方式感到不满，要求能直接执行脚本以降低延迟、提高可靠性。

- **🔒 安全意识空前高涨**
  - [#10659](https://github.com/openclaw/openclaw/issues/10659) **Masked Secrets**：13条评论，4 👍。社区对 API 密钥能被 Agent 直接读取感到不安，屏蔽密钥功能被认为是防止 Prompt 注入和数据泄露的关键。

## 5. Bug 与稳定性

今日 Bug 主要集中在会话管理、消息投递和回归问题上，但大部分均有修复 PR 跟进：

| 严重程度 | Issue 编号 | 问题摘要 | 状态 | 关联修复 PR |
|---|---|---|---|---|
| P0 | [#85240](https://github.com/openclaw/openclaw/issues/85240) | 跨用户隐私泄露（语义记忆召回未隔离 sender_id） | ✅ 已关闭 | - |
| P1 | [#85913](https://github.com/openclaw/openclaw/issues/85913) | EmbeddedAttemptSessionTakeoverError 竞态条件，锁未正确释放 | 🔴 开放中 | [#86427](https://github.com/openclaw/openclaw/issues/86427) |
| P1 | [#80520](https://github.com/openclaw/openclaw/issues/80520) | Telegram 消息静默丢失，无 sendMessage 日志 | 🔴 开放中 | - |
| P1 | [#85953](https://github.com/openclaw/openclaw/issues/85953) | sessions_yield 导致父会话锁未释放，子代理回调超时 | 🔴 开放中 | - |
| P1 | [#86214](https://github.com/openclaw/openclaw/issues/86214) | Codex 服务器处理大日志时关闭，UI 卡死 | 🔴 开放中 | [#86233](https://github.com/openclaw/openclaw/issues/86233) |
| P1 | [#86184](https://github.com/openclaw/openclaw/issues/86184) | 2026.5.22 Telegram 工具调用成功后返回通用错误回退 | 🔴 开放中 | - |
| P2 | [#58479](https://github.com/openclaw/openclaw/issues/58479) | [回归] 审批对话框成功，但 Exec 未消费，生成新审批 ID | ✅ 已关闭 | - |
| P2 | [#68944](https://github.com/openclaw/openclaw/issues/68944) | CLI 命令卡在 WebSocket 握手 | ✅ 已关闭 | - |
| 安全 | [#84338](https://github.com/openclaw/openclaw/issues/84338) | Hook 入口令牌可升级为网关密码模式认证权限 | 🚀 待自动合并 | [#84338](https://github.com/openclaw/openclaw/issues/84338) |

**稳定性分析**：项目当前遭遇了一波严重的会话模型竞态问题（#85913, #85953），好在核心团队已经提交了修复 PR（#86427）。在快速迭代的背景下，需要警惕此类并发锁问题的蔓延。

## 6. 功能请求与路线图信号

结合今日最热门的 Issue 和新提出的 PR，我们可以推测项目的下一步优先级：

- **✅ 高概率进入下一版本的功能**：
  - **MCP 工具调用审批门**：PR [#78303](https://github.com/openclaw/openclaw/issues/78303)（XL， P2）为 MCP 工具引入了类似 `exec-approvals` 的安全审批机制，预示着 MCP 生态安全将成为下一阶段的重点。
  - **可配置流看门狗**：Issue [#68596](https://github.com/openclaw/openclaw/issues/68596) 呼声极高，涉及代码改动量小，针对大模型新特性（长思考）的适配将成为必要。
  - **Masked Secrets**：Issue [#10659](https://github.com/openclaw/openclaw/issues/10659) 与当前的强化安全方向（#85240, #84338）一致，预计会被采纳以构建更完善的安全架构。

- **🔄 长期规划与关注信号**：
  - **渠道适配**：Issue [#12602](https://github.com/openclaw/openclaw/issues/12602)（Slack Block Kit）、[#86169](https://github.com/openclaw/openclaw/issues/86169)（小米 MiMo Token Plan）展示了社区对更丰富渠道的渴望。
  - **运维与可观测性**：Issue [#13616](https://github.com/openclaw/openclaw/issues/13616)（备份/恢复）、PR [#86415](https://github.com/openclaw/openclaw/issues/86415)（Cron 写入修复）表明项目在运维健壮性上仍有提升空间。

## 7. 用户反馈摘要

以下是从热门 Issue 中提炼的真实用户声音：

- **“看门狗能不能别叫了？”**：用户 `Yaemikoreal` 在 [#68596](https://github.com/openclaw/openclaw/issues/68596) 中明确表示，使用 Kimi-k2.5、DeepSeek-R1 等模型时，`streaming watchdog` 频繁警告不仅干扰日志，还重置状态，非常影响使用。
- **“我的 Telegram Bot 哑巴了。”**：用户 `kyle20026` 在 [#80520](https://github.com/openclaw/openclaw/issues/80520) 中详细举证了 Telegram 消息被静默丢弃的过程，直言网关处理了消息但没调用 `sendMessage API`，这严重破坏了用户对 Bot 的信任。
- **“说好的多轮对话呢？”**：用户 `marieejesus12` 在 [#11665](https://github.com/openclaw/openclaw/issues/11665) 中指控文档中宣传的 Webhook `sessionKey` 持续会话功能实际上是无效的，`resolveCronSession` 每次都生成新 ID，功能承诺落空。
- **“能不能直接给我 APK，别让我自己编译？”**：用户 `AstridQing-AI` 在 [#9443](https://github.com/openclaw/openclaw/issues/9443) 中强烈建议发布预编译的 Android APK，暴露出当前的构建流程对普通用户不友好，是采用率的阻碍。
- **“给残障用户留条路吧。”**：用户 `robin24` 在 [#9637](https://github.com/openclaw/openclaw/issues/9637) 中要求提供禁用 Emoji 的选项，指出填充大量 Emoji 的 TUI 对于屏幕阅读器用户来说是灾难性的噪音，体现了对无障碍设计的关注。

## 8. 待处理积压

以下为需要维护者或作者重点关注的问题与 PR：

- **⚠️ 重大产品决策待定**：
  - [#75](https://github.com/openclaw/openclaw/issues/75) **Linux/Windows Apps（106条评论）**：自 1 月 1 日提出至今，社区已围绕此问题讨论了半年，项目进行了多次大版本更新却未回应此核心诉求，极需一个明确的产品决策或时间表。
  - [#6731](https://github.com/openclaw/openclaw/issues/6731) Safe/Unsafe ClawdBot 模式讨论。
  - [#6615](https://github.com/openclaw/openclaw/issues/6615) Exec-approvals 拒绝名单支持。

- **👀 P1 修复等待维护者审查**：
  - PR [#86427](https://github.com/openclaw/openclaw/issues/86427) **fix(agents): 释放嵌入式会话锁（P1）**：直接解决当前最头疼的并发锁问题，应优先审查合入。
  - PR [#86416](https://github.com/openclaw/openclaw/issues/86233) **fix(codex): 限制应用服务器日志（P1）**：直接修复 [#86214](https://github.com/openclaw/openclaw/issues/86214) 导致的 UI 卡死问题，建议尽快合入。

- **⏳ 大型/关键 PR 等待作者修改**：
  - [#86415](https://github.com/openclaw/openclaw/issues/86415)（Cron 写入修复）、[#86286](https://github.com/openclaw/openclaw/issues/86286)（Ollama 推理泄露）、[#78303](https://github.com/openclaw/openclaw/issues/78303)（MCP 审批门）、[#85941](https://github.com/openclaw/openclaw/issues/85941)（回复性能提升）均处于“等待作者”状态。这些 PR 的进度直接影响后续版本的质量和功能完备性。

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态横向对比分析报告

**报告日期**：2026-05-25  
**数据来源**：github.com/openclaw/openclaw 等 13 个仓库当日公开活动  
**分析师**：资深 AI 智能体开源生态分析师

---

## 1. 生态全景

个人 AI 助手/自主智能体开源赛道正处于“爆发式迭代与安全焦虑并存”的阶段。项目普遍保持极高提交密度，头部的 OpenClaw 单日产出 500+ Issue/PR，NanoBot、Hermes Agent、IronClaw、ZeroClaw 等紧随其后，社区贡献热情空前。然而，合并率普遍偏低（多数项目低于 20%），维护者审核带宽成为主要瓶颈；同时，跨用户隐私泄露、MCP 子系统进程泄漏、Agent 循环调用等安全与可靠性问题开始集中暴露，推动社区加速构建安全护栏。整体生态正从“能用”向“可信、可控、可生产”快速演进，桌面客户端、记忆系统、多渠道成熟度成为下一阶段竞争力焦点。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|------|-------------|-----------|----------|------------|
| **OpenClaw** | 500（新开/活跃 297，关闭 203） | 500（待合并 315，已合并/关闭 185） | 2 个 Beta | ✦✦✦✦✧ 极活跃但合并压力大，安全响应及时，架构重构推进中 |
| **NanoBot** | 6（关闭 3） | 114（待合并 106，合并/关闭 8） | 无 | ✦✦✦✧✧ 合并率极低（7%），积压严重，但核心功能修复有效率 |
| **Hermes Agent** | 50（新开/活跃 40，关闭 10） | 50（待合并 45，合并/关闭 5） | 无 | ✦✦✦✧✧ 合并率 10%，严重 Bug 多但关闭速度可，维护瓶颈明显 |
| **PicoClaw** | 8 | 9 | 1 Nightly | ✦✦✦✦✧ 快速响应模型兼容危机，架构 PR 进入审查，部分修复积压 18 天 |
| **NanoClaw** | 2 | 10（待合并 6，合并/关闭 4） | 无 | ✦✦✦✦✧ 核心功能 per-agent 配置落地，新 Bug 静默丢消息需高度关注 |
| **NullClaw** | 0 | 1（Dependabot） | 无 | ✦✧✧✧✧ 静默维护期，仅自动化依赖更新，无人工贡献 |
| **IronClaw** | 27（活跃 20，关闭 7） | 50（待处理 42，合并/关闭 8） | 无 | ✦✦✦✧✧ 架构重构（Reborn）推进快，但版本发布阻塞，Discord 渠道崩溃 |
| **LobsterAI** | 0 | 22（开放 8，合并/关闭 14） | 无 | ✦✦✦✦✧ 核心功能与修复密集合入，无新 Bug 报告，但 8 个 PR 长期积压 |
| **TinyClaw** | 0 | 0 | 无 | ✦✧✧✧✧ 当日无活动，休眠状态 |
| **Moltis** | 8（全部关闭） | 10（全部合并/关闭） | 无 | ✦✦✦✦✦ 零积压，维护者秒修，架构关键革新，健康度最佳 |
| **CoPaw (QwenPaw)** | 27（关闭 13） | 37（合并/关闭 24） | 无 | ✦✦✦✦✧ 密集修复与测试补全，大型功能蓄力，开放 Bug 数量仍多 |
| **ZeptoClaw** | 0 | 0 | 无 | ✦✧✧✧✧ 当日无活动，休眠状态 |
| **ZeroClaw** | 50（关闭 4） | 50（合并/关闭 8，待合并 42） | 无 | ✦✦✦✦✧ 飞书渠道完工，但 MCP 可靠性危机集中爆发，治理 RFC 获热议 |

> 健康度评估综合考虑合并率、Bug 响应速度、积压严重度、社区反馈与版本节奏，满分五颗星。

---

## 3. OpenClaw 在生态中的定位

**生态核心参照，规模一骑绝尘。** OpenClaw 当日 500 条 Issue 与 500 条 PR 的量级是第二名（NanoBot、Hermes、ZeroClaw 均为 50 条量级）的 10 倍，社区活跃度遥遥领先。其核心优势在于：

- **全功能覆盖**：从多渠道（Telegram、Slack、iMessage、微信、飞书）、审批门（exec-approvals、MCP 审批）、记忆系统、Cron 调度到 Agent 运行时内化，功能栈最深最全。
- **安全先行**：P0 隐私泄露 24h 内修复、Hook 令牌认证修复、Masked Secrets 呼声高涨，安全能力建设明显领先于其他项目。
- **技术路线激进**：将底层 Agent 运行时从 Pi 完全内化（PR #85341），实现自主可控；而多数项目（如 NanoBot、Hermes）仍依赖回调或转发模式。

与同类对比：
- **Hermes Agent** 更侧重轻量 TUI 与插件生态，规模小但社区质量高，合并率同样偏低。
- **NanoBot** 聚焦 Agent 循环检测与 Dream 记忆系统，规模虽大但合并瓶颈最严重。
- **IronClaw** 采用 Rust 重写并启动 Reborn 重构，架构现代化，但版本发布被 CVE 阻塞，社区协作尚在爬坡。
- **ZeroClaw** 在 Rust 领域与 IronClaw 竞争，MCP 集成是其差异化优势，但稳定性问题较多。

**社区规模：** OpenClaw 的 Issue 评论数（如 Linux/Windows Apps #75 达 106 条）远超其他项目，用户基础最广，但桌面端缺失也是其最大槽点。

---

## 4. 共同关注的技术方向

多个项目不约而同地涌现以下关键需求，已从“个别呼声”上升为“行业共识”：

### 4.1 安全护栏与隐私保护
- **涉事项目**：OpenClaw、Hermes Agent、PicoClaw、IronClaw、Moltis、CoPaw、ZeroClaw
- **具体诉求**：
  - 跨用户数据隔离/语义记忆泄露修复（OpenClaw #85240，PicoClaw #2759，IronClaw #4017）
  - API 密钥/环境变量屏蔽与凭据剥离（OpenClaw #10659，Moltis #1054，Hermes Agent #31959）
  - 工具调用审批门的强制定向（OpenClaw #78303 MCP 审批门，CoPaw #4667 QQ 审批卡片，ZeroClaw #6852 飞书审批）
  - 文件路径白名单与沙箱（CoPaw #4267，PicoClaw #1042 guardCommand 误报）

### 4.2 Agent 自主行为控制与循环检测
- **涉事项目**：NanoBot、OpenClaw、ZeroClaw、CoPaw
- **具体诉求**：
  - 通用工具循环检测与硬阻断（NanoBot #3986 / PR #3985）
  - 可配置流看门狗超时阈值，适配长思考模型（OpenClaw #68596）
  - Shell 执行资源控制/超时（Moltis #1066 runtime 限制，ZeroClaw #6910 挂起）

### 4.3 多渠道纵深与平台成熟度
- **涉事项目**：OpenClaw（iMessage、Slack Block Kit）、Hermes Agent（飞书 CardKit、WhatsApp）、PicoClaw（微信多账号）、IronClaw（企业微信 WeCom）、ZeroClaw（飞书 Cron+审批）、CoPaw（钉钉、QQ）
- **共同趋势**：从基础的消息收发向“互动卡片、审批闭环、会话管理”升级，企业级渠道（飞书、企微）投入明显增加。

### 4.4 桌面客户端与终端体验
- **涉事项目**：OpenClaw #75（Linux/Windows 桌面，106 条评论）、CoPaw #3813（Tauri 2.x 桌面）、ZeroClaw #6848（TUI 终端）
- **共同痛点**：Web 后台无法满足重度用户，原生桌面/TUI 需求强烈，是下一阶段用户增长核心驱动力。

### 4.5 记忆系统演进
- **涉事项目**：NanoBot（Dream 两阶段合并）、Hermes Agent（多 Bank 路由 #31776）、CoPaw（记忆增强 #4652）、OpenClaw（语义记忆隔离）
- **趋势**：从简单的历史存储转向分层、实时、可路由的智能记忆系统，是提升 Agent 个性化和持续学习能力的关键。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|---------|----------|-----------------|
| **OpenClaw** | 全栈个人 AI 助手，安全审批、多渠道、调度 | 开发者、重度个人用户 | Node.js/TypeScript，运行时自研，插件市场庞大 |
| **Hermes Agent** | 轻量 TUI + 插件生态，快速入门 | 个人开发者、Linux 重度用户 | Go + TUI，插件标准化（Kanban 等），配置即代码 |
| **NanoBot** | 高可控 Agent 行为，记忆与进化 | 研究者、高级用户 | Python + LLM 行为护栏（循环检测），Dream 记忆系统 |
| **PicoClaw** | 边缘/嵌入式设备（Sipeed），轻量部署 | 硬件玩家、边缘计算 | C/C++，极低资源消耗，LM Studio 等本地模型对接 |
| **NanoClaw** | 简洁 CLI，per-agent 模型配置 | CLI 爱好者、权限管理员 | TypeScript，强调最小配置级联与权限继承 |
| **NullClaw** | 自动化依赖维护，极少人工干预 | （维护者自身） | 实际处于休眠，仅 Dependabot 运行 |
| **IronClaw** | 企业级重构（Reborn），Rust 全栈 | 企业 DevOps、安全团队 | Rust 实现，WASM 渠道，OAuth 认证栈，子智能体生成 |
| **LobsterAI** | 与 OpenClaw 生态互通，网易有道背景 | 已有 OpenClaw 用户，中文用户 | 直接对接 OpenClaw 插件目录，注重 Mac/Windows 体验 |
| **TinyClaw** | （未知，当日无活动） | - | - |
| **Moltis** | 多用户多 Agent（儿童/家长），零积压 | 家庭、教育场景 | Agent 作为能力边界独立配置，Plawright 回归测试 |
| **CoPaw/QwenPaw** | 编码模式 + 数据分析，大厂生态 | 开发者、数据分析师 | 集成编码 IDE（Coding Mode）、DataPaw 插件、主题系统 |
| **ZeptoClaw** | （未知，当日无活动） | - | - |
| **ZeroClaw** | MCP 深度集成 + 飞书渠道 | MCP 生态用户、国内企业 | Rust + MCP 作为一等公民，飞书/Telegram/Slack 三端完整闭环 |

---

## 6. 社区热度与成熟度分层

### 🔥 第一梯队：极端活跃，快速迭代期
- **OpenClaw**：单日 500 条量级，但仍然保持快速响应安全事件，合并率 37%（185/500），属于高吞吐项目。处于功能扩展与架构重构并行阶段。
- **ZeroClaw**：50 条量级，合并率 16%（8/50），MCP 与飞书是核心引擎。处于功能高速推进但稳定性爬坡阶段。
- **CoPaw**：27 Issue / 37 PR，合并率 65%（24/37），Bug 修复密集，测试补全。进入质量巩固早期。

### 🔥 第二梯队：高活跃，合并瓶颈明显
- **NanoBot**：PR 量达 114，合并率仅 7%，积压最严重。处于“社区贡献爆炸 vs 维护资源不足”阶段。
- **Hermes Agent**：50 PR，合并率 10%。Bug 数量多但修复快，同样面临审核瓶颈。
- **IronClaw**：50 PR，合并率 16%。Reborn 架构推进快，但版本发布阻塞和严重 Bug 降低了交付节奏。

### ⚡ 第三梯队：中度活跃，稳定推进
- **PicoClaw**：9 PR，合并率 22%（但 2 个合并），架构 PR 审查中，健康度良好。
- **NanoClaw**：10 PR，合并率 40%，核心 per-agent 落地。
- **LobsterAI**：22 PR，合并率 64%，但 8 个 PR 积压 > 45 天，且为 bug fix，需尽快处理。
- **Moltis**：10 PR 全部合并，0 积压。成熟度最佳，已进入良性维护期。

### 🥀 第四梯队：低活跃/休眠
- **NullClaw、TinyClaw、ZeptoClaw**：当日无有意义人工贡献，项目处于停滞或静默维护。

---

## 7. 值得关注的趋势信号

### 🔍 信号一：隐私与安全从“可选项”变为“强制项”
多个项目在同一天爆发严重安全问题（OpenClaw P0 泄露、Moltis MCP 环境变量泄露、IronClaw 审计绕过、ZeroClaw WebSocket 认证绕过）。社区反馈不再容忍“先上线后补安全”，Masked Secrets、审批门、白名单成为标配需求。**给开发者的启示**：安全机制（凭据隔离、审计追踪、默认拒绝）应在架构设计阶段嵌入，而非事后补救。

### 🔍 信号二：Agent 运行时正在从“黑盒”走向“可观测、可控制”
社区对 Agent 内部行为（循环调用、超时、看门狗误报、工具调用透明度）的关注度已超过对功能花样的追求。NanoBot 的循环检测、OpenClaw 的可配置看门狗、ZeroClaw 的 Shell 执行控制共同指向一个趋势：**开发者需要深度掌控 Agent 的资源消耗与决策循环**，未来 Agent 框架将提供更细粒度的“策略即代码”能力。

### 🔍 信号三：MCP 协议成为 Rust 系项目的核心战场
ZeroClaw 与 IronClaw 均以 Rust 实现并将 MCP（Model Context Protocol）作为第一优先级，但 ZeroClaw 的进程泄漏与过滤失效表明 MCP 集成的系统工程难度远超预期。同时 OpenClaw 也在推进 MCP 审批门。**信号**：MCP 正在从“可选插件”升级为“核心基础设施”，但稳定性、进程管理和安全隔离仍是亟待突破的工程难点。

### 🔍 信号四：国产/企业渠道投入加速
飞书（ZeroClaw、LobsterAI）、企业微信（IronClaw）、钉钉（CoPaw）、QQ（NanoClaw、CoPaw）等渠道在本日均有实质性进展。**背景**：AI 助手在国内企业办公场景落地的需求正在倒逼开源项目优先适配本土平台，未来 3-6 个月飞书与企微的成熟度可能反超 Telegram/Slack。

### 🔍 信号五：桌面客户端是“兵家必争之地”
OpenClaw #75 以 106 条评论登顶社区热点，CoPaw 推进 Tauri 2.x 桌面，ZeroClaw 开发 TUI 终端。Web 端已无法满足高频交互与低延迟需求。**趋势判断**：**能率先提供稳定、功能完备的桌面客户端的项目，将在下一阶段用户增长中占据明显优势。**

### 🔍 信号六：记忆系统进入“分层+实时”架构探索期
NanoBot 的 Dream 单阶段合入、Hermes 的多 Bank 路由提议、CoPaw 的总结-关联-提醒机制，均表明记忆从简单的对话历史存储向“情境感知、长期演化、用户自定义”方向演进。这是个人 AI 助手走向“个性化”的关键技术栈。

---

*本报告基于 2026-05-25 公开 GitHub 数据自动生成，分析仅代表当日快照，不构成投资或选择建议。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的NanoBot (HKUDS/nanobot) GitHub数据生成的2026年5月25日项目动态日报。

---

### **NanoBot 项目动态日报 | 2026-05-25**

#### **1. 今日速览**

今日NanoBot项目社区活跃度极高，呈现显著的高并发提交与合并瓶颈并存的态势。过去24小时内，Pull Requests (PR) 数量激增至114条，但其中106条仍处于待合并状态，合并率不足10%，显示出维护团队面临较大的审核压力。Issues方面保持平稳，6条更新中3条已关闭，表明问题处理效率尚可。项目核心趋势聚焦于 **Agent循环行为检测与限制** 以及 **系统记忆与自我进化（Dream）机制的优化**，反映出社区对Agent稳定性和智能化水平的更高要求。

#### **2. 版本发布**

无

#### **3. 项目进展**

尽管PR合并率较低，但仍有数项关键工作取得了进展或被合并，推动了项目在稳定性和功能性的提升：

- **Agent循环检测机制 (已关闭):** **[PR #3985]** 实现了“循环检测与速率限制硬阻断”。该PR是 **Issue #3986** 的实现，通过两道护栏（通用循环检测和速率限制）来防止LLM陷入无意义的工具重试循环，如反复调用 `grep` 或 `read_file`。此项合并将显著提升Agent执行任务时的鲁棒性和资源利用率。
- **子Agent并发配置修复 (已关闭):** **[PR #3978]** 修复了一个关键配置BUG，确保 `maxConcurrentSubagents` 配置项能被正确地从配置文件传递到 `SubagentManager`，解决了用户自定义并发控制失效的问题。这是对核心多Agent编排能力的一次必要修正。
- **新功能与基础优化 (待合并):** 虽然尚未合并，但以下高质量PR的出现标志着项目正稳步向前：
    - **能力商店 (Store):** **[PR #3991]** 提议在WebUI中新增“Store”入口，整合CLI Apps和MCP能力目录，以改善用户体验。
    - **Step Plan 提供商**: **[PR #3988]** 新增对 `StepFun` 平台 `Step Plan` 订阅服务的支持，拓宽了底层模型的选择范围。
    - **Token预估优化**: **[PR #3997]** 通过预热共享tokenizer和增加性能日志，优化Agent启动和消息处理的性能。

#### **4. 社区热点**

今日社区讨论的核心议题是 **“Agent自主行为的可靠性与可控性”** ，围绕此议题形成了多个热点讨论：

- **工具循环与资源滥用:** **Issue #3986** (请求通用循环检测) 和 **PR #3985** (实现方案) 成为了今日的绝对焦点。社区用户 `codeLong1024` 系统地描述了LLM在日常使用中陷入“死循环”的多种场景（**重复参数调用**、**短时间疯狂调用**、**反复读取失败**），并提供了详实的解决方案。开发者的快速响应和实现，体现了社区对Agent稳定性的强烈诉求。
- **Dream系统的自我改进机制:** **Issue #3973** (Dream系统的饥饿问题与缺乏实时学习) 引发了关于Agent自我进化路径的深度讨论。用户指出当前系统仅依赖 `history.jsonl` 作为单一数据源是严重的瓶颈。同时，**PR #3990** 提出的“将Dream两阶段内存合并为单阶段”的架构调整，表明项目正在积极探索更高效的Agent记忆与学习方案。链接：[Issue #3973](HKUDS/nanobot Issue #3973), [PR #3990](HKUDS/nanobot PR #3990)

#### **5. Bug 与稳定性**

今日报告了2个Bug，均已关闭，未出现严重级别的系统崩溃或回归问题。

- **严重: PowerShell 终端刷屏 (已修复):** **Issue #3995** 报告了在PowerShell环境下，Agent思考流式输出由于渲染异常，每次收到新数据块都会强制换行，导致终端严重刷屏。这是一个影响PowerShell平台上用户体验的Bug，已被关闭，可推测有相应的修复合并。
- **中: 对话追踪ID不一致 (已关闭):** **Issue #3980** 报告了在通过 `antchat` 代理非OpenAI原生接口时，`conversation trace` 中的 `tool_call_id` 与 `tool_result` 不匹配。该问题已在今日关闭，表明已被解决。

#### **6. 功能请求与路线图信号**

用户提出的新功能需求主要指向两个方面，结合现有PR可预判项目未来方向：

1.  **Agent行为硬约束**
    - **需求:** **Issue #3986** 已经通过 **PR #3985** 得到解决。此外，同为循环检测主题的 **[PR #2271]** 也在积压队列中，说明这是长期且核心的路线图。未来Agent将具备更强、更通用的“自保”能力，防止算力浪费。

2.  **记忆机制与自我进化**
    - **需求:** **Issue #3973** 呼吁Dream系统解决“饥饿”问题和获取实时学习能力。同时，**PR #3990** 正在重构Dream架构。
    - **信号:** 此外，长期开放的语义记忆索引 **[PR #2618]** 旨在构建可搜索的混合向量记忆。可以预见，**构建一个分层、实时、高效的记忆系统**是NanoBot下一阶段的核心方向。

#### **7. 用户反馈摘要**

从今日的Issues和PR评论中可以得出以下关键反馈：

- **对Agent“弱智”循环行为的不满:** 用户 `codeLong1024` 在 **Issue #3986** 中详细列举了多种循环调用场景，这些反馈代表了高频用户对LLM Agent“不够聪明”的普遍打磨点。用户期待Agent能具备常识判断和错误止损能力。
- **对特定环境适配性的关注:** 用户 `Shiftqueue` 报告 **Issue #3995** 的PowerShell刷屏问题，表明用户运行环境多样，对平台兼容性有较高要求。
- **对架构复杂性的担忧:** 从多Agent系统 **[PR #2466]**、Dream合并 **[PR #3990]** 等讨论中可以看出，社区在推动功能创新的同时，也对代码复杂度和架构清晰性保持着高度关注。

#### **8. 待处理积压**

今日待合并PR数量高达106条，项目维护者面临巨大的审核压力。以下挑选几项长期未响应或重要的积压项，提请维护者关注：

- **核心功能长期搁置:**
    - **[PR #1443] (feat: decouple heartbeat reasoning from notification)** - 提出心跳Agent静默推理，减少用户通知干扰。该PR已被忽略近3个月，若无技术冲突，建议尽快决策，以优化后台Agent的用户体验。
    - **[PR #2466] (feat: multi-subagent orchestration)** - 一个较为成熟的多Agent协作框架，已停滞2个月。此功能对未来复杂任务编排至关重要，应评估其与现有架构的整合方式。
- **功能重复与概念冲突:**
    - 用户 `codeLong1024` 今日提交并关闭了功能请求 **Issue #3986** 和实现 **PR #3985**。但其提案与积压已久的 **[PR #2271] (feat(agent): add tool call cycle detection)** 在核心思路上高度重合。建议维护者评估两个方案的优劣，整合出一套统一的、更优雅的循环检测机制，避免未来社区在重复概念上投入精力。

**总结:** NanoBot正处于高速发展期，社区贡献热情高涨，但主项目维护者的人力瓶颈已开始显现，导致合并延迟。当前的项目健康度良好，核心Bug得到了及时修复，但需要加快对高质量和高优先级PR的审核合并，以保持社区贡献者的积极性并推动项目持续演进。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 - 2026-05-25

## 1. 今日速览

过去 24 小时内，项目社区活跃度达到顶峰，共产生 50 条 Issue 更新（其中 40 条为新开/活跃）与 50 条 PR 更新（其中 45 条处于待合并状态）。然而，合并率极低（约 10%，仅 5 个 PR 被合并/关闭），表明在极大贡献流量的冲击下，维护者审核带宽出现明显瓶颈。从 Bug 分布来看，**Docker 部署权限、OpenAI Codex / xAI 新后端稳定性，以及多平台网关适配器（Telegram / QQBot）的可靠性问题，构成了今日社区三大焦点**。尽管 Bug 数量庞大，但多个 P1 级别严重问题在本日被修复关闭，项目的整体健壮性正在修复与风险并存的阶段快速迭代。

**活跃度评估：🔴 极高**

## 2. 版本发布

无。

## 3. 项目进展

今日合并/关闭的 5 个 PR 虽数量不多，但含金量较高，主要集中在社区痛点的快速响应与基础设施的完善：

- **TUI 体验紧急修复**：PR [#31985](https://github.com/NousResearch/hermes-agent/pull/31985) 火速修复了 `/q` 别名冲突（`/quit` 与 `/queue` 的冲突，对应 Issue #31983）。从 Bug 报告到修复关闭仅数小时，展现了高效的社区协作氛围。
- **插件生态标准化**：PR [#26606](https://github.com/NousResearch/hermes-agent/pull/26606) 为 Kanban 插件合并了标准的包元数据，这是插件系统走向规范注册与发现机制的重要一步。
- **协作文档完善**：PR [#31990](https://github.com/NousResearch/hermes-agent/pull/31990) 补充了自定义分支策略指南，直接降低外部贡献者的参与门槛。

另有多项高风险 Issue 在本日被关闭（详见第 5 节），项目维护团队正在集中清理之前积压的严重 Bug。

## 4. 社区热点

- **最热 Issue（关联反应最多）**：[#21444](https://github.com/NousResearch/hermes-agent/issues/21444) —— `openai-codex` / `gpt-5.5` 后端的静默挂起问题。该 Bug 获得 **9 条评论、4 个 👍**。它是直接影响核心对话流程的严重超时故障，用户对新推出的 Codex Responses 传输协议的稳定性表示高度担忧。虽已关闭，但对应的 TTFB 看门狗修复 PR [#31984](https://github.com/NousResearch/hermes-agent/pull/31984) 仍在审核中，社区持续保持关注。

- **最受欢迎功能（呼声最高）**：[#18918](https://github.com/NousResearch/hermes-agent/issues/18918) —— 要求在 Slack 端支持 GFM 管道表格渲染。虽然评论数不高，但获得了 **6 个 👍**，是当日 👍 数最高的 Issue。这表明企业用户对于跨平台格式化输出（尤其是结构化数据）有刚性需求。

- **最具颠覆性提议**：[#31928](https://github.com/NousResearch/hermes-agent/issues/31928) —— 将 GitHub Issues 作为 Agent 的任务队列。该提议与 Hermes 的“Agent 化”理念高度契合，如果实现，将使项目自家的开发流程成为一次绝佳的 Agent 实践样板，吸引了大量对 Agentic Workflow 感兴趣的开发者参与讨论。

- **架构焦灼讨论**：RFC [#23717](https://github.com/NousResearch/hermes-agent/issues/23717) —— 关于引入 PostgreSQL / MySQL 替代 SQLite 作为 Session Database 的讨论持续发酵。社区用户正认真地将 Hermes 推向生产环境部署，数据库单点问题已成为架构演进的核心矛盾。

## 5. Bug 与稳定性

当日报告的 Bug 主要集中在**静默失败**与**适配器崩溃**两类，严重度分布如下：

**P1（严重）**

- **Telegram 指令后静默丢消息**（[#31884](https://github.com/NousResearch/hermes-agent/issues/31884)）：`/stop` 后用户消息被确认发送但实际被丢弃，后端继续占用资源，且最终回复无法送达。对用户感知破坏极强。**暂无修复 PR。**
- **v0.9.0 三重核心 Bug 悬而未决**（[#11096](https://github.com/NousResearch/hermes-agent/issues/11096)）：涉及 `context_length` 覆盖、`thinking-block` 会话分裂、配置文件优先级混乱。自 4 月 16 日以来已开放超 40 天，是当前积压影响面最大的已知问题。

**P2（重要）**

- **MCP HTTP 传输重连风暴**（[#31987](https://github.com/NousResearch/hermes-agent/issues/31987)）：`anyio` 锁竞争导致上下文管理器清理失败，消耗全部重试机会并不断尝试重连。
- **第三方 Web 搜索插件静默禁用**（[#31873](https://github.com/NousResearch/hermes-agent/issues/31873)）：硬编码的后端白名单检查绕过了插件注册机制，用户安装的 Web 搜索插件不会被使用且无提示。
- **QQBot WebSocket 掉线后 CPU 100%**（[#31771](https://github.com/NousResearch/hermes-agent/issues/31771)）：断线重连失败未正确处理繁忙状态，持续耗尽 CPU。
- **Gateway /model 命令配置不持久**（[#30781](https://github.com/NousResearch/hermes-agent/issues/30781)）：远程用户切换模型后，重启网关即丢失配置。
- **Docker 环境权限 Bug 复现**（[#27221](https://github.com/NousResearch/hermes-agent/issues/27221)、[#23402](https://github.com/NousResearch/hermes-agent/issues/23402)）：`HERMES_UID` 重映射时未对 `ui-tui/` 和 `gateway/` 目录执行 chown，导致 Unraid/Synology 用户容器启动后无法正常交互。
- **macOS 下 xAI OAuth 回调超时**（[#27385](https://github.com/NousResearch/hermes-agent/issues/27385)）：浏览器授权成功但 Hermes CLI 收不到解译后的 callback，导致认证彻底卡死。
- **Windows 原生 Dashboard 空白页**（[#28987](https://github.com/NousResearch/hermes-agent/issues/28987)）：JS Bundle 被服务器以错误的 MIME 类型（`text/plain`）下发。
- **macOS 网关锁互相阻塞**（[#31890](https://github.com/NousResearch/hermes-agent/issues/31890)）：PID 复用导致 scoped 锁残留，适配器永久阻塞无法初始化。
- **Wayland 下 TUI 输入重复**（[#31962](https://github.com/NousResearch/hermes-agent/issues/31962)）：窗口失焦事件处理不当导致输入累积。

**已有对应修复 PR 的 Bug**

- **Codex TTFB 看门狗**（PR [#31984](https://github.com/NousResearch/hermes-agent/pull/31984)）：直接针对 Codex 挂起问题的前置检测。
- **子进程凭据安全剥离**（PR [#31959](https://github.com/NousResearch/hermes-agent/pull/31959)）：统一入口防止 CI 凭据泄露到子进程。
- **MCP Shell 包装器进程追踪**（PR [#27516](https://github.com/NousResearch/hermes-agent/pull/27516)）：反向修复子进程管理不全导致的僵尸/无法清理问题。
- **自定义 Provider Context Length 传播**（PR [#13540](https://github.com/NousResearch/hermes-agent/pull/13540)）：修复跨模型压缩判断错误。
- **Docker 环境变量转发**（PR [#12825](https://github.com/NousResearch/hermes-agent/pull/12825)）：保障沙箱容器继承配置变量。
- **Telegram 用户名 Chat ID 兼容**（PR [#13535](https://github.com/NousResearch/hermes-agent/pull/13535)）：支持 `@username` 格式配置。

## 6. 功能请求与路线图信号

当日提交的功能请求普遍反映了从“可用”到“好用”、“生产化”的诉求：

- **Agent 原生任务队列**（[#31928](https://github.com/NousResearch/hermes-agent/issues/31928)）：将 GitHub Issues 作为 Agent 的协作循环。项目团队如采纳，将极大提升自身的 Dogfooding 自动化水平。
- **跨平台独立模型配置**（[#14327](https://github.com/NousResearch/hermes-agent/issues/14327)）：允许不同网关（飞书、Telegram）绑定不同模型，减少手动 `/model` 切换。这是多平台重度用户的刚需。
- **会话历史导入/导出**（[#31911](https://github.com/NousResearch/hermes-agent/issues/31911)）：支持导入 OpenAI Codex CLI 的对话历史。直接瞄准竞品迁移场景。
- **TUI 稳定元数据暴露**（[#31945](https://github.com/NousResearch/hermes-agent/issues/31945)）：让 `session.history` 不依赖显示层格式，利于二次开发。
- **记忆系统多 Bank 路由**（[#31776](https://github.com/NousResearch/hermes-agent/issues/31776)）：允许根据用户/平台/会话元数据动态切换记忆库，是 Hindsight 记忆系统的重大扩展。

**从已有 PR 看路线图信号：**

- **飞书 CardKit 流式卡片**（PR [#31989](https://github.com/NousResearch/hermes-agent/pull/31989)）：大幅增强飞书网关的交互表现力。
- **WhatsApp 原生引用/状态回复**（PR [#21977](https://github.com/NousResearch/hermes-agent/pull/21977)）：提升 Baileys 适配器的消息质感。
- **Dashboard 主题打磨**（PR [#31944](https://github.com/NousResearch/hermes-agent/pull/31944)）：朝着更精致的 Feishu 风格视觉系统演进。

## 7. 用户反馈摘要

**社区核心痛点：**

“**静默失败**” 是当日评论区中最高频的负面体验标签。无论是 OpenAI Codex 的 300 秒挂起（[#21444](https://github.com/NousResearch/hermes-agent/issues/21444)）、Telegram 的吞消息（[#31884](https://github.com/NousResearch/hermes-agent/issues/31884)），还是插件不工作（[#31873](https://github.com/NousResearch/hermes-agent/issues/31873)）、配置不持久（[#30781](https://github.com/NousResearch/hermes-agent/issues/30781)），都会让用户无法判断系统状态，严重损害使用信心。

“**Docker 部署太难了**” —— 以 Unraid / Synology 为代表的 NAS 用户反复提及权限挂载问题（[#27221](https://github.com/NousResearch/hermes-agent/issues/27221)、[#23402](https://github.com/NousResearch/hermes-agent/issues/23402)），门槛远高于标准 Linux 部署。

“**新东西好吃，但不够熟**” —— 用户对新接入的 xAI 认证和 OpenAI Codex 后端表示了极高的开箱即用兴趣，但频繁遭遇超时和鉴权断裂（[#27385](https://github.com/NousResearch/hermes-agent/issues/27385)）。

**积极信号：**

尽管 Bug 众多，但极高的 Issue/PR 提交数量以及快速关闭关键 Bug（如 #21444、#29335）表明社区对项目有着极大的热忱和耐心。用户愿意花费数小时撰写详尽的 Bug 报告和日志，这是一种强烈的高忠诚度信号。

## 8. 待处理积压

以下 Issue 和 PR 长时间处于无人响应或待合并状态，是项目健康的潜在风险点，建议维护者重点关注：

- **[P1 严重 Bug] [#11096](https://github.com/NousResearch/hermes-agent/issues/11096)**：v0.9.0 的三个核心 Bug 已开放 **40 天**（自 2026-04-16），是当前积压中最严重、影响面最广的稳定性债务。尽管社区提供了本地 Workaround，但 Root Cause 仍在 Upstream。

- **[Bug Fix PR] [#13540](https://github.com/NousResearch/hermes-agent/pull/13540)**：修复自定义 Provider 的 `context_length` 未正确传播到压缩可行性检查的问题。已开放 **超过一个月**（2026-04-21），对多模型异构部署用户的上下文管理有直接影响。

- **[功能 PR] [#12743](https://github.com/NousResearch/hermes-agent/pull/12743)**：Honcho 记忆自动迁移。已经积累了一个月，长时间搁置可能导致功能分支与主干产生较大冲突。

- **[Bug Fix PR] [#12825](https://github.com/NousResearch/hermes-agent/pull/12825)**：Docker 环境变量转发到沙箱容器。阻碍了需要通过环境变量配置沙箱工具的复杂 Docker 使用场景落地。

- **[Bug Fix PR] [#13535](https://github.com/NousResearch/hermes-agent/pull/13535)**：Telegram 用户名 ChatID 支持。开放超过一个月，是提升 Telegram 网关易用性的基础性补丁。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据 PicoClaw 2026-05-25 的 GitHub 数据生成的每日项目动态分析。

---

# PicoClaw 项目日报 — 2026-05-25

**分析师**: AI Agent 开源项目分析师
**数据来源**: github.com/sipeed/picoclaw

---

### 1. 今日速览

PicoClaw 今日活跃度处于**高位**，24 小时内处理了 8 个 Issue 和 9 个 PR，并发布了夜间构建版本。社区对 `claude-opus-4-7` 模型的兼容性危机响应极其迅速（Issue #2939 提交后立即被 PR #2940 跟进修复）。架构级特性“Agent 协作总线”（PR #2937）正式进入审查，标志着项目在多智能体方向迈出关键一步。整体来看，项目在 Bug 修复与大型特性开发上并行推进，健康状况良好，但部分高优先级 Bug 修复 PR（如 #2813）仍处于待审查积压状态。

---

### 2. 版本发布

- **发布版本**: `v0.2.9-nightly.20260525.ab6d3946`
- **类型**: 自动夜间构建 (Nightly)
- **稳定性提示**: 自动构建版本，包含最新代码但可能不稳定，供尝鲜测试用。
- **变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

### 3. 项目进展

今日有 **2 个 PR** 被合并，解决了重要的回归和安全隐患；同时数个重大特性 PR 已进入最终审查阶段。

**已合入修复：**
- **[修复] Cron 任务静默失败（#2938）**: 修复了 `CronTool` 调用 `ExecTool` 时缺少 `"action": "run"` 参数，导致所有定时命令任务静默失败的回归问题。该问题由重构提交 `3f1ac2` 引入。
- **[修复] 会话检索安全性（#2759）**: 将 `short_grep` 和 `short_expand` 检索工具的作用域默认限定在当前活跃会话，防止通过消息 ID 猜测访问其他会话的数据。

**审查中的重大进展：**
- **[架构] Agent 协作总线（#2937）**: 引入了一等公民的智能体间通信机制（邮箱、线程、结构化消息），这是实现复杂多智能体编排的基础设施。
- **[稳定性] 总线背压与健康检查（#2906）**: 优化了消息队列饱和时的处理逻辑（Bounded Waiting），并增加了流级别丢弃统计和健康信号，提升系统在高负载下的鲁棒性。
- **[稳定性] 智能体重载和 Panic 修复（#2904）**: 修复了 `ReloadProviderAndConfig` 的协程泄漏和对 `panic` 的清理逻辑。
- **[特性] 微信多账号（#2883）**: 支持动态识别 `weixin_*` 配置键，允许用户配置和管理多个微信账号，显著增强了渠道层的灵活性。

---

### 4. 社区热点

- **🥇 高讨论度：本地模型连接诉求（Issue #28）**
  - **链接**: [Issue #28](https://github.com/sipeed/picoclaw/issues/28)
  - **分析**: 尽管是二月的 Issue，但其 **20 条评论** 和持续的关注度表明，降低与 LM Studio 等第三方本地推理引擎的连接门槛是社区最强烈的“痛点”之一。用户吐槽“just outside my reach”，暗示现有的配置方式对非技术用户不友好。

- **🥇 高互动性 Bug：exec 工具安全守卫误报（Issue #1042）**
  - **链接**: [Issue #1042](https://github.com/sipeed/picoclaw/issues/1042)
  - **分析**: 拥有 **13 条评论** 和 2 个 👍。`restrict_to_workspace` 的 `guardCommand` 方法被普遍认为过于简单粗暴，将 `curl wttr.in/Beijing?T` 等正常命令误判为路径穿越。这直接触发了核心工具的可用性危机，社区对此表示沮丧。

- **⚡ 快速响应范例：claude-opus-4-7 兼容问题（Issue #2939 / PR #2940）**
  - **链接**: [Issue #2939](https://github.com/sipeed/picoclaw/issues/2939) / [PR #2940](https://github.com/sipeed/picoclaw/pull/2940)
  - **分析**: 用户 @LegendAlessandro-Liguori 在提交 Issue 报告 `claude-opus-4-7` 因 `temperature` 弃用导致 HTTP 400 错误后，**随即提交了修复 PR**。这种“自提自修”的模式展现了社区中高级用户的高度参与和项目组对主流模型兼容性的重视。

---

### 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| **严重/崩溃** | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | 单例 PID 检查误杀：旧 PID 被系统进程（如 `systemd-resolved`）占用，导致网关启动时崩溃循环。 | **已有修复 PR (#2813)** 已打开 18 天，待审查合并 |
| **严重/模型失灵** | [#2939](https://github.com/sipeed/picoclaw/issues/2939) | `claude-opus-4-7` 完全无法使用。Anthropic API 弃用 `temperature` 参数导致所有请求返回 400 错误。 | **已有修复 PR (#2940)** 今日提交 |
| **中等/功能异常** | [#2796](https://github.com/sipeed/picoclaw/issues/2796) | 历史记录缺陷：多轮对话在历史记录中只显示最后一条用户消息，之前的全部丢失。 | **暂无修复 PR** |
| **中等/工具可用性** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` 工具安全守卫误报：`guardCommand` 正则逻辑缺陷，阻止了诸多合法命令。 | **暂无修复 PR** |
| **低/已解决** | [#2839](https://github.com/sipeed/picoclaw/issues/2839) | Steering Chain 最终回复错误地编辑了 `Working...` 占位符。 | 已关闭 |

---

### 6. 功能请求与路线图信号

- **🚀 下一个大版本的核心特性（v0.3.x 候选）**:
  - **Agent 协作总线 (#2937)**: 这可能是近期最重量级的 PR，将 PicoClaw 从单一的“任务执行器”升级为“多智能体操作系统”的核心通信层。
  - **微信多账号 (#2883)**: 渠道层的大幅增强，表明项目在服务特定区域市场（如中国）的重度用户。
  - **AGENT.md 工具策略 (#2837, 已关闭)**: 虽已关闭，但为智能体提供了基于文件的权限配置（`allow/deny/glob`），是多智能体治理的基础，预示该功能可能已合入或规划在即。

- **💰 性能优化方向**:
  - **减少技能目录 Token 消耗 (#2781)**: 该 PR 通过避免在工具调用循环和后续轮次中重复注入技能列表来节省 Token。对于依赖非缓存提供商、对 API 成本敏感的用户，这是极具价值的优化。该 PR 虽被标记为 **stale**，但作者仍在更新。

- **📋 用户长期诉求**:
  - **LM Studio 简易连接 (#28)**: 虽无关联 PR，但 20 条评论的高热度明确指向简化第三方后端配置的需求。

---

### 7. 用户反馈摘要

- **“命令被粗暴拦截”的挫败感**：用户在 `#1042` 中直言 `guardCommand` 的逻辑**“简单粗暴”**（simple and crude），执行一个简单的 `curl` 查天气命令却因为路径被误判为 `../../../../Beijing?T` 导致失败。这严重影响了用户对工具链安全功能的信任。
- **“历史消息去哪了”的困惑**：用户 @EverestSnow 在 `#2796` 中发现了对话记录显示不完整的 Bug，并明确表达了期望：**“消息压缩应该是针对大模型的，对用户显示的历史消息应该完整”**。这强调了前端展示数据完整性的重要性，任何后端压缩逻辑都不应影响用户感知到的对话上下文。
- **“安装门槛高”的求助**：用户 @Franzferdinan51 在 `#28` 中坦言“just outside my reach”，希望有技术大牛帮忙制作简易连接 LM Studio 的方案。这真实反映了 PicoClaw 在降低非技术用户使用门槛上还有巨大的提升空间。

---

### 8. 待处理积压（需维护者关注）

| 类型 | 编号 | 标题 | 关注原因与建议 |
|---|---|---|---|
| **Issue** | [#28](https://github.com/sipeed/picoclaw/issues/28) | Feat Request: LM Studio Easy Connect | **高人气、高评论（20条）**，但无所有权无进展。建议标记为 `help-wanted` 或明确是否在路线图中。 |
| **Issue** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | [BUG] exec工具guardCommand方法问题 | **直接影响核心工具体验**。讨论热烈但无修复 PR。建议评估是否重写或配置化 `guardCommand` 逻辑。 |
| **PR** | [#2813](https://github.com/sipeed/picoclaw/pull/2813) | fix(pid): verify gateway identity before blocking startup on stale PID | **对应高优 Bug #2720，已打开 18 天**。合并此 PR 可以消除一个导致网关启动崩溃的常见问题，对提升新用户和开发者体验至关重要。 |
| **PR** | [#2781](https://github.com/sipeed/picoclaw/pull/2781) | perf: reduce skill catalog token usage on tool iterations | **重要性能优化，已标记 stale**。虽然长时间未合并，但今日仍有更新。如果可以提供 Code Review，这将是一个极具性价比的优化。 |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-05-25

## 1. 今日速览

今日项目活跃度极高，24 小时内共有 **10 个 PR** 和 **2 个 Issue** 产生更新。项目健康度良好，社区贡献持续旺盛。高优先级的 CLI 分组删除 Bug 已在今晨修复并合并（#2526），体现了问题闭环的高效。社区贡献者 `IamAdamJowett` 主导的 **“端到端按智能体配置供应商和模型”** 核心功能也于今日正式合并落库（#1968），成为本次迭代中最关键的交付物。不过，新报告的 `engage_mode='always'` 静默丢弃全部消息的 Bug（#2606）严重影响了消息路由的可靠性，需维护者高度重视。

- **Issues**: 2 条（新开/活跃 1 条，已关闭 1 条）
- **Pull Requests**: 10 条（待合并 6 条，已合并/关闭 4 条）
- **版本发布**: 0 个

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

### 🎉 今日合并/关闭的关键 PR

#### 核心功能
- **[#1968] End-to-end per-agent provider and model configuration** ⭐（已合并）
  - 该 PR 历经一个月打磨，正式合入 `main` 分支。它使每个智能体可以独立配置大模型供应商与推理参数，彻底终结了全局模型的限制。这是项目迈向企业级灵活性的一块重要基石，已在聊天界面内可完整驱动。
- **[#2604] web: add GET /admin/agent-activity batch endpoint**（已合并）
  - 为管理系统仪表板新增批量查询“最后活跃时间”端点，减少了多行数据查表时的轮询开销，是社区驱动的后台优化。

#### 稳定性与 Bug 修复
- **[#2526] fix(cli): cascade dependent rows on groups delete**（已合并，Fixes #2525）
  - 修复了 `ncl groups delete` 在删除非空组时因外键约束失败导致无法操作的阻塞性问题。现在删除命令会级联清理依赖的子表数据行。
- **[#2344] fix(tests): satisfy tightened RoutableAgentMessage and Session types**（已合并）
  - 解决了因类型定义变动导致的 `pnpm run build` 阻塞问题，恢复了 `main` 分支的可构建状态。

### ⏳ 待合并的重点 PR

以下 PR 今日均有更新且处于开放状态，值得关注：
- **[#2609]** `fix(apple-container)` — 容器文件挂载与 `host.docker.internal` 修复，Mac 用户友好度提升
- **[#2345]** `feat(claude-md-compose)` — 自动按组导入 `CLAUDE.role.md`，多 agent 文档管理利器
- **[#2346]** `fix(formatter)` — 未知斜杠命令不再被静默丢弃，改善交互反馈
- **[#2607]** `Use platform IDs for inbound message actions` — 提升平台 API 兼容性
- **[#2605]** `feat: inherit parent agent permissions via OneCLI` — 权限继承精细化
- **[#2608]** `ci: bump Node 20 actions to v5` — 提前应对 Node 20 弃用倒计时，基础设施现代化

---

## 4. 社区热点

| 编号 | 标题 | 热度信号 | 核心诉求 |
|------|------|----------|----------|
| [#2606](nanocoai/nanoclaw Issue #2606) | `engage_mode='always'` silently drops all messages | ⭐ 新开即热点，静默丢消息，潜在影响力极大 | 核心路由函数 `evaluateEngage()` 缺少对该模式的逻辑分支，社区高度关注数据安全问题 |
| [#2609](nanocoai/nanoclaw PR #2609) | fix(apple-container): file mounts, host.docker.internal, user mapping | ⭐ 高价值社区贡献 | Mac 用户容器体验的重大改善，`CashQ` 发起的修复涉及配置文件挂载、网络和用户权限映射 |
| [#2605](nanocoai/nanoclaw PR #2605) | feat: inherit parent agent permissions via OneCLI | ⭐ 精细化权限管理需求 | 用户 `guyb1` 贡献的权限继承功能，体现社区对企业级用户管理（RBAC扩展）的强烈期待 |
| [#2525](nanocoai/nanoclaw Issue #2525) | `ncl groups delete` fails with `FOREIGN KEY constraint failed` | ✅ 已关闭修复 | 用户 `glifocat` 完美复现的 High 级 Bug，社区协作快速闭环的典型案例 |

## 5. Bug 与稳定性

### 🔴 严重
- **[#2606] `engage_mode='always'` 静默丢弃全部消息**（新开，未修复）
  - **现象**：用户将配置写入 `engage_mode: 'always'` 后，该配置可正常存储，但运行时在 `evaluateEngage()` 中无对应处理分支，所有消息均以 `no_agent_engaged` 理由静默丢弃，且用户无任何显式错误反馈。
  - **影响范围**：所有使用 `always` 模式的 Wiring 配置，可能导致生产环境下消息完全不可用。
  - **是否已有 Fix PR**：尚未分配，风险等级最高，建议优先响应。

### 🟡 中/低风险 & 已修复
- **[#2525] CLI 分组删除阻塞**（已修复，#2526 已合并）
  - 已圆满解决，无需进一步操作。
- **[#2346] 未知斜杠命令被错误传递**（待合并）
  - 未被识别的 `/` 命令被归类为 `passthrough`，SDK 将其当作内置命令处理，输出不含标准 `<message>` 块，导致响应被丢弃。长期可用性隐患。
- **[#2608] Node 20 运行时弃用预警**（待合并）
  - 严格来说不是 Bug，但 2026 年 6 月 GitHub Actions 将弃用 Node 20，当前 CI 依赖的三个 Action 均需升级到 Node 24。
- **[#2607] Inbound message actions 使用错误消息 ID**（待合并）
  - 内部复合 ID 被发送到平台 API，导致消息操作（如添加 Reaction）失败。

## 6. 功能请求与路线图信号

综合分析近期 Issue/PR 高频词汇，以下功能极可能被纳入 **v1.6 / 下一个小版本**：

| 期望功能 | 推进证据 | 优先级预测 |
|----------|----------|------------|
| **Per-agent Provider** 独立配置 | ✅ [#1968] 已合并，基础能力已具备，后续需要文档和 UI 跟进 | 🔥 最高优先级 |
| **CLAUDE.role.md 自动导入** | ⏳ [#2345] 开放近三周，今日有更新，等待评审 | 高 |
| **平台原生 ID 支持 Inbound 操作** | ⏳ [#2607] 对接外部平台（如 Slack、Discord）的刚性需求 | 高 |
| **权限继承** | ⏳ [#2605] 权限模型细化：OneCLI 继承父级权限 | 中/高 |
| **容器 Mac 体验优化** | ⏳ [#2609] Apple Silicon + Docker 深度修复 | 中 |
| **Admin Dashboard Agent Activity** | ✅ [#2604] 已合并，后台管理用户体验提升 | 中 |

## 7. 用户反馈摘要

### ✅ 满意点
- **CLI 删除修复闭环高效**：用户 `glifocat` 提交的 High 级 Bug 从复现到修复仅经过一次 PR 迭代便完成合入，对项目响应速度表示认可（未直接评论，但从 Issue/PR 的链式跟踪可以看出流畅的协作）。
- **Per-agent provider 落地**：社区核心贡献者 `IamAdamJowett` 持续投入，该功能从系列提交到最终合入，标志着项目在“灵活编排”方向上获得了里程碑式的支撑。

### ⚠️ 不满意 / 痛点
- **`engage_mode='always'` 静默失败**：用户 `nikki-assistant` 报告的这个问题非常值得警惕。Bug 表现为“静默丢弃”，这意味着在生产环境中用户可能数天甚至数周察觉不到消息丢失，直到用户开始投诉“智能体不回复”。**这种 Zero-feedback 的故障模式是 API 工具的大忌**。
- **删除操作的阻塞性外键约束**：简单直接的 `DELETE` 语句在关联表面前完全无能为力。这暴露了 CLI crud 模块在处理复杂级联删除时的设计空缺，虽然已经修复，但在未发布新版本前用户仍需手动规避。
- **斜杠命令模糊行为**：#2346 的描述表明，不支持的 `/` 命令不是“报错”，而是“产生空响应”。这种默认降级处理容易让用户陷入“智能体答非所问”的困惑中。

## 8. 待处理积压

以下为需维护者重点关注的长期开放 / 高危未响应项：

| 编号 | 类型 | 标题 | 创建时间 | 积压风险 |
|------|------|------|----------|----------|
| [#2606](nanocoai/nanoclaw Issue #2606) | Bug | `engage_mode='always'` drops all messages silently | 2026-05-24 | **高** — 高危数据丢失 Bug，截止本日报发布仍无 PR 关联，建议 24h 内分配 |
| [#2346](nanocoai/nanoclaw PR #2346) | Fix | 未知斜杠命令视为正常对话 | 2026-05-08 | **中** — 已开放超 17 天，虽有更新但无实质合并进展，影响命令行交互体验 |
| [#2345](nanocoai/nanoclaw PR #2345) | Feature | CLAUDE.role.md 自动导入 | 2026-05-08 | **中** — 开放超 17 天，文档自动化功能长期未合入，等待维护组意见闭环 |

---

*注：本日报基于 2026-05-25 当日 GitHub 公开数据生成，仅反映仓库活动快照，不构成投资或使用建议。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是根据您提供的 NullClaw GitHub 项目数据生成的 2026-05-25 项目动态日报。

---

### NullClaw 项目动态日报 | 2026-05-25
**数据时间范围**: 2026-05-24 ~ 2026-05-25
**分析师**: AI Agent / 开源项目健康度分析

---

#### 1. 今日速览

NullClaw 项目今日处于极低活跃度状态。过去 24 小时内，项目未产生任何新 Issue，唯一的 PR 活动来自 Dependabot 的自动化依赖版本更新（[#931](https://github.com/nullclaw/nullclaw/pull/931)），且无新版本发布。从社区互动指标来看，项目进入了 **“静默维护期”**：无人工提交、无用户反馈、无代码合并。唯一的正向信号是自动化 CI 与依赖管理流程仍在按部就班地运行，保障了基础设施的基本安全线。项目活跃度健康度评分较低，但稳定性未见负面警报。

#### 2. 版本发布
（今日无新版本发布，此部分省略）

#### 3. 项目进展
**合并/关闭**: 0。项目主线代码在此周期内无任何变更被合入。
**待推进**:
- **[#931](https://github.com/nullclaw/nullclaw/pull/931) [dependencies, docker] ci(deps): bump busybox from 1.37 to 1.38 in the docker-images group**
  - **状态**: OPEN
  - **概述**: 由 Dependabot 发起，旨在将 Docker 构建环境中的 `busybox` 基础镜像从 1.37 升级至 1.38。属于被动依赖维护，不涉及核心业务逻辑变更。合入后将有助于解决旧版本的基础镜像 CVE 风险。

#### 4. 社区热点
**热度稀疏，自动化唱独角戏**：
- 今日仅有一条活动记录，即 **[#931](https://github.com/nullclaw/nullclaw/pull/931)**。该 PR 由机器人创建，至今无人评论、无人点赞。
- **诉求分析**: 零互动的 PR 通常意味着：项目缺乏积极响应变更的维护者，或社区成员缺乏参与代码审查的动力。Dependabot 试图传达的“保持依赖更新”的诉求被暂时搁置。若此 PR 长期无人处理，可能会造成版本滞后甚至 CI 失败，这是当前项目健康度的最大风险点。

#### 5. Bug 与稳定性
- **新报告 Bug**: 0。无任何崩溃、回归或安全性问题被提交。
- **评估**: 项目代码库表面稳定，但由于缺乏用户反馈与使用场景佐证，这种“稳定”是建立在低曝光度基础上的“假设性稳定”。

#### 6. 功能请求与路线图信号
- **新功能请求**: 0。
- **路线图信号**: 无。今日数据面完全无法支撑对未来路线图的判断。项目当前处于纯粹的维护模式，无功能开发迹象。

#### 7. 用户反馈摘要
- **摘要**: 无用户通过公开渠道（Issue/PR评论）留下反馈。项目在用户侧当前处于“黑盒”状态，真实痛点和使用场景无法提炼。

#### 8. 待处理积压
- **长期积压**: 无。
- **短期待办提醒**: 虽然 **[#931](https://github.com/nullclaw/nullclaw/pull/931)** 为今日创建，尚未构成系统意义上的“积压”，但其零互动状态已构成潜在风险。**建议维护者尽快审核此 PR，** 避免因自动化 PR 堆积而导致 CI 流水线维护成本上升，同时也能通过合并让项目依赖保持最新状态。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw GitHub 数据生成的 2026-05-25 项目动态日报。

---

# IronClaw 项目日报 | 2026-05-25

## 1. 今日速览

过去 24 小时，IronClaw 项目维持极高的开发活跃度：共产生 **27 条 Issue 更新**（20 条活跃 / 7 条关闭）和 **50 个 PR 操作**（42 个待处理 / 8 个已合并或关闭）。核心主线依然是庞大的 **“Reborn” 架构重构**，覆盖渠道迁移、认证体系、子智能体生成等模块。安全方面，核心贡献者 [`zmanian`](https://github.com/zmanian) 指出了工具执行路径的安全审计绕过问题（[#4017](#4017)），并推动系统性加固方案（[#4019](#4019)）。

**关键里程碑**：Reborn 原生认证栈的三步走策略（契约定义、服务拼接、OAuth 回调）全部关闭（[#3810](#3810)、[#3811](#3811)、[#3812](#3812)），标志新认证层基础设施落地。

**风险警示**：**crates.io 发布严重滞后**（被 wasmtime CVE 审查阻塞），下游用户被锁定在旧版本（[#3259](#3259)）；**Discord 渠道出现完全瘫痪**（CPU 100% 打满）（[#4030](#4030)）；**Nightly E2E 持续失败**（[#3447](#3447)）。

---

## 2. 版本发布

**今日无新版本发布。**

- 最新发布 PR [`#3708`](https://github.com/nearai/ironclaw/pull/3708) (chore: release) 仍在开放中（拟将 `ironclaw` 从 0.24.0 发布至 0.28.2，包含 breaking changes）。
- 当前社区最大痛点集中在 **[Issue #3259](#3259)**：GitHub Tags 已存在 `ironclaw-v0.27.0`，但 crates.io 因 wasmtime 28.x 系列 CVE 审查而卡在 0.24.0。发布 PR [#3708](#3708) 已积压 9 天，等待阻塞问题解决。

---

## 3. 项目进展：重要合并/关闭及推进

过去 24 小时 **8 个 PR 被合并或关闭**，在 Reborn 认证、渠道迁移、开发体验方面有显著推进：

**认证与授权层基础落地**
- **[#3810](https://github.com/nearai/ironclaw/issues/3810) & [#3811](https://github.com/nearai/ironclaw/issues/3811) & [#3812](https://github.com/nearai/ironclaw/issues/3812) (CLOSED)**：Reborn 原生认证 Step 1-3 全部关闭。完成了产品级认证契约定义、原生密钥组合、OAuth 回调和设置延续。
- **[#4031](https://github.com/nearai/ironclaw/pull/4031) (新 PR)**：挂载了产品 OAuth 路由（开始/回调），通过 WebUI v2 组合生效。
- **[#4029](https://github.com/nearai/ironclaw/pull/4029) (新 PR)**：新增审批交互服务，用于审批流程列表和同意/拒绝决策。

**渠道迁移**
- **[#2394](https://github.com/nearai/ironclaw/pull/2394) (CLOSED)**：**WeCom (企业微信) WASM 渠道**正式合并。由持续贡献者 `hanakannzashi` 主导，包括 WebSocket 入站、被动回复、安全验证、媒体附件等。
- **[#3579](https://github.com/nearai/ironclaw/issues/3579) & [#3580](https://github.com/nearai/ironclaw/issues/3580) (CLOSED)**：Slack 和 WebUI/Web Gateway 的 Reborn 渠道迁移规划追踪全部关闭。

**开发体验与底层改进**
- **[#4018](https://github.com/nearai/ironclaw/pull/4018) (CLOSED)**：Reborn 本地开发环境接入 HTTP 能力。
- **[#2941](https://github.com/nearai/ironclaw/pull/2941) (CLOSED)**：合并了 Slack 回调 HMAC 诊断日志改进，有助于排查 401 验证失败问题。
- **[#4020](https://github.com/nearai/ironclaw/pull/4020) (CLOSED)**：合并工具失败分类审核反馈，改进了错误映射（`ResponseError` -> `OperationFailed` 等）。

---

## 4. 社区热点

### 🔥 #3259：下游发布阻断（9 条评论）
- **链接**: [Issue #3259](https://github.com/nearai/ironclaw/issues/3259)
- **诉求**: `ironclaw-v0.27.0` 已在 GitHub Tags，但 crates.io 最高只到 0.24.0。用户 `dacoldest` 发起讨论，揭露 wasmtime 28.x CVE 导致发布流水线卡死。这是社区当前**最大共识性痛点**，直接影响所有外部消费者的安全更新和功能获取。
- **状态**: 无修复 PR，发布 PR [#3708](https://github.com/nearai/ironclaw/pull/3708) 等待合并。

### 💬 #4017 / #4019：安全执行护城河（3-1 条评论，技术深度高）
- **链接**: [Issue #4017](https://github.com/nearai/ironclaw/issues/4017) / [Issue #4019](https://github.com/nearai/ironclaw/issues/4019)
- **诉求**: 核心贡献者 `zmanian` 发现**交互式聊天不经过 `ToolDispatcher::dispatch`**，绕过了 `ActionRecord` 审计和渠道工具过滤。该洞见引发了围绕“如何系统化固化安全约定”的热烈讨论，并生成了加固提案（#4019：审计单漏斗 + 默认拒绝 + CI 边界测试）。

### ⚙️ #3702：二进制 E2E 测试框架规划（4 条评论）
- **链接**: [Issue #3702](https://github.com/nearai/ironclaw/issues/3702)
- **诉求**: 为整个 Reborn 复生计划设计独立的二进制端到端测试框架。属于 **Reborn 质量门禁** 的核心话题。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | 编号 | 标题 | 状态 | 链接 |
|---|---|---|---|---|
| **严重** | #3259 | crates.io 版本滞后，下游 pinned 在 0.24.0 | 待修复。wasmtime CVE 阻塞 | [Issue #3259](https://github.com/nearai/ironclaw/issues/3259) |
| **严重** | #4017 | 交互式聊天绕过 ToolDispatcher 审计 | 待修复。已有跟进方案 (#4019) | [Issue #4017](https://github.com/nearai/ironclaw/issues/4017) |
| **严重** | #4030 | Discord 渠道完全停止响应，Tokio 100% CPU | 待修复。QA 用户 `sanghyunna` 报告 | [Issue #4030](https://github.com/nearai/ironclaw/issues/4030) |
| **高** | #3447 | Nightly E2E 测试持续失败 (Commit: `030cfeb0`) | 待修复。自 5 月 10 日起触发 | [Issue #3447](https://github.com/nearai/ironclaw/issues/3447) |
| **中** | #4027 | macOS/Linux `cargo test` 弹出钥匙串弹窗 | **已有修复 PR** | [PR #4027](https://github.com/nearai/ironclaw/pull/4027) |
| **中** | #3917 | `PathPlaceholder` 凭据注入风险（URL 路径泄露） | 待决策（移除或加固） | [Issue #3917](https://github.com/nearai/ironclaw/issues/3917) |

---

## 6. 功能请求与路线图信号

### 用户请求
- **[#4034](https://github.com/nearai/ironclaw/issues/4034) 自定义 Telegram API Host**：用户 `senseab` 请求支持自定义 Telegram Bot API 服务器地址。对于私有化部署和企业内网环境有明确需求，预计可纳入 WASM 渠道配置层。

### 路线图信号（模块化进展）
- **子智能体生成 (Subagent Spawn)**：设计稿 [#3798](https://github.com/nearai/ironclaw/issues/3798) 已定型，三个 Draft PR（[#3869](https://github.com/nearai/ironclaw/pull/3869) Phase 2、[#3870](https://github.com/nearai/ironclaw/pull/3870) Phase 3、[#3872](https://github.com/nearai/ironclaw/pull/3872) Phase 4）正在并行推进。这是未来 **Reborn 复杂 Agent 编排** 的核心能力。
- **工具执行固化 (Tool Hardening)**：[#4019](https://github.com/nearai/ironclaw/issues/4019) 提出将安全约定从代码约束升级为系统级强制机制（审计单漏斗 + 默认拒绝 + CI 边界测试）。这是 **Reborn 安全模型升级**的关键信号。
- **代码结构优化**：[#3988](https://github.com/nearai/ironclaw/issues/3988) 要求对超 3000 行的 `capability_port.rs` 文件进行拆分，表明项目开始关注**长期可维护性**。

---

## 7. 用户反馈摘要

基于 Issue/PR 评论提炼的真实用户痛点：

| 类型 | 来源用户 | 核心反馈 | 原文摘要 |
|---|---|---|---|
| **最失望** | `dacoldest` (#3259) | 上游 TAG 已到 0.27，但 crates.io 卡死在 0.24 | "Downstream consumers pulling from crates.io are pinned to 0.24.0" |
| **最担忧** | `zmanian` (#4017) | 交互式聊天绕过了所有审计和安全过滤 | "skips the audit trail (`ActionRecord`) and the channel tool-permit filtering" |
| **最受阻** | `zmanian` (#4027) | macOS 下 `cargo test` 会被系统钥匙串弹窗阻塞 | "`cargo test` on macOS pops a Keychain authorization dialog (and blocks on a locked Secret Service on Linux)" |
| **最致命崩溃** | `sanghyunna` (#4030) | Discord 渠道 Bot 完全静默，CPU 占满 100% | "Discord channel stops replying while ironclaw stays active with tokio workers pinned at 100% CPU" |

---

## 8. 待处理积压

以下 Issue 或 PR 长期未得到响应或合并，建议维护者关注：

### 🔴 高优先级
- **[Issue #3259](https://github.com/nearai/ironclaw/issues/3259) 发布阻断**：**严重度最高**。下游生态系统被 wasmtime CVE 完全阻塞。关联发布 PR [#3708](https://github.com/nearai/ironclaw/pull/3708) 已积压 9 天。
- **[Issue #3447](https://github.com/nearai/ironclaw/issues/3447) Nightly E2E 持续失败**：自动化质量红线第 **15 天**，Commit `030cfeb0` 疑似引起回归。
- **[Issue #3807](https://github.com/nearai/ironclaw/issues/3807) Reborn WebUI Beta 路径完成**：开放 6 天，**0 条评论**，缺乏推动。
- **[Issue #3613](https://github.com/nearai/ironclaw/issues/3613) Beta 端到端验收测试**：开放 11 天，**0 条评论**，缺乏推动。

### 🟡 中等优先级
- **[Issue #3279](https://github.com/nearai/ironclaw/issues/3279) TurnCoordinator 验收测试**：开放 19 天，标记 P1，**0 条评论**。
- **[Issue #3286](https://github.com/nearai/ironclaw/issues/3286) Agent 命令行为保持**：开放 19 天，标记 P1，**0 条评论**。
- **[Issue #3889](https://github.com/nearai/ironclaw/issues/3889) 审批交互服务**：开放 3 天，需推动 Code Review 或分配合并。

### 🟠 待进入合并流程
- 三个子智能体生成 Draft PR（[#3869](https://github.com/nearai/ironclaw/pull/3869) Phase 2、[#3870](https://github.com/nearai/ironclaw/pull/3870) Phase 3、[#3872](https://github.com/nearai/ironclaw/pull/3872) Phase 4）长期处于 Draft 状态，需尽快推进 Review 以避免功能分支发散。

---
**总结：项目处于高强度的架构重构期（Reborn），活跃度极佳。但版本发布流水线的阻塞（wasmtime CVE）、关键渠道的崩溃（Discord）和质量门禁的失效（Nightly E2E）构成了当前三大主要风险。**

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-05-25

## 今日速览

过去 24 小时内，LobsterAI 共产生 22 条 Pull Request 更新（14 条已合并/关闭，8 条仍开放待审）；无新 Issue，无新版本 Release。主要进展集中在 **插件自动同步（OpenClaw）**、**子代理会话详情与渲染复用**、**模型自定义参数透传及 Thinking 块显示**，以及多项稳定性修复（跨 DPI 窗口尺寸、Dreaming 配置非法属性、GitHub Copilot Token 刷新导致网关重启）。主分支合并密度较高，预示一个小版本迭代正在酝酿中。

## 项目进展

以下为今日合并/关闭的核心 Pull Request，它们直接推进了项目功能与稳定性的向前演进：

- **[#2042](https://github.com/netease-youdao/LobsterAI/pull/2042) — feat(plugins): 支持从 OpenClaw 扩展目录同步插件**  
  实现插件自动发现与同步，让通过 OpenClaw 界面安装的插件自动纳入 LobsterAI 管理，打通插件生态。

- **[#2043](https://github.com/netease-youdao/LobsterAI/pull/2043) — fix: fixed gateway restart caused by github copilot token refresh**  
  修复 GitHub Copilot 令牌刷新导致网关意外重启的问题，保障持续运行。

- **[#2011](https://github.com/netease-youdao/LobsterAI/pull/2011) — feat: subagent session sidebar display and detail view**  
  在侧边栏展示子代理会话树，并新增独立详情页，大幅提升子代理的可视化能力。

- **[#2019](https://github.com/netease-youdao/LobsterAI/pull/2019) — feat: model custom params + thinking block display**  
  新增 per‑model 自定义参数 JSON 输入（支持 `extra_body` 透传），并实现流式 Thinking 块显示，改善推理模型的使用体验。

- **[#2020](https://github.com/netease-youdao/LobsterAI/pull/2020) — fix: prevent small window on Windows with cross-DPI multi-monitor**  
  修复 Windows 跨 DPI 多显示器下窗口异常缩小的问题。

- **[#2021](https://github.com/netease-youdao/LobsterAI/pull/2021) — feat: support contextWindow for package models**  
  支持套餐模型透传 `contextWindow` 字段，使引擎可根据后端推荐值控制上下文截断长度。

- **[#2026](https://github.com/netease-youdao/LobsterAI/pull/2026) — fix: remove unsupported dreaming config properties causing gateway crash**  
  移除 dreaming 配置中 `model` / `timezone` 等不被 OpenClaw 模式支持的属性，阻止 gateway 启动崩溃。

- **[#2027](https://github.com/netease-youdao/LobsterAI/pull/2027) / [#2029](https://github.com/netease-youdao/LobsterAI/pull/2029) / [#2030](https://github.com/netease-youdao/LobsterAI/pull/2030) — subagent 界面修复与渲染重构**  
  侧栏切换、拖拽标题栏、Mac 适配；修复子代理记录因 agentId 冲突导致的覆盖缺失；将子代理历史转换为标准 CoworkMessage 格式，复用主对话渲染组件，代码架构大幅收敛。

- **[#2013](https://github.com/netease-youdao/LobsterAI/pull/2013) — fix: context window slider snap-to-preset and K/M text input**  
  滑块支持吸附到 32K/64K/200K/1M/2M 预设点，文本输入支持 `1m`、`200k` 简写，提升交互效率。

- **[#1584](https://github.com/netease-youdao/LobsterAI/pull/1584) — fix(agent): 使用短 UUID 替代名称生成 Agent ID**  
  避免删除 Agent 后因文件残留导致重建同名 Agent 时旧数据意外复活。

以上合并进一步强化了插件互通性、子代理完整性、模型灵活性与跨平台稳定性。

## 社区热点

今日虽无新 Issue 提交，但 8 个较早打开的 PR 被标记为 stale，表明这些贡献长期未获审查。以下三个与用户日常操作紧密相关，值得特别关注：

- **[#1510](https://github.com/netease-youdao/LobsterAI/pull/1510) — 定时任务 IM 通知静默失败**  
  表单缺少会话必填校验，导致运行时通知不可达，影响自动化可靠性。

- **[#1514](https://github.com/netease-youdao/LobsterAI/pull/1514) — QQ Bot 群组白名单无法添加群组 ID**  
  因 UI 缺失输入框，白名单功能形同虚设。

- **[#1517](https://github.com/netease-youdao/LobsterAI/pull/1517) — 关闭 Settings 面板导致 Copilot OAuth 令牌丢失**  
  轮询未取消，用户必须重新认证，体验割裂。

上述问题已在 PR 中给出修复代码但未合并，希望维护团队尽快推进。

## Bug 与稳定性

| 严重程度 | 问题描述 | 状态 |
|---|---|---|
| **严重** | Dreaming 配置含不支持的属性导致 gateway 无法启动 | ✅ [#2026](https://github.com/netease-youdao/LobsterAI/pull/2026) 已修复 |
| **严重** | GitHub Copilot Token 刷新触发 gateway 重启 | ✅ [#2043](https://github.com/netease-youdao/LobsterAI/pull/2043) 已修复 |
| **中** | Windows 跨 DPI 多屏窗口缩小至 400×300 | ✅ [#2020](https://github.com/netease-youdao/LobsterAI/pull/2020) 已修复 |
| **中** | 定时任务 IM 通知因 `to` 为空而静默失败 | ⏳ [#1510](https://github.com/netease-youdao/LobsterAI/pull/1510) 待合并 |
| **中** | QQ Bot 白名单无法添加群组 ID | ⏳ [#1514](https://github.com/netease-youdao/LobsterAI/pull/1514) 待合并 |
| **中** | 日志导出超时（`Log export timed out`） | ⏳ [#1515](https://github.com/netease-youdao/LobsterAI/pull/1515) 待合并 |
| **中** | Settings 关闭时 Copilot OAuth 轮询未取消，Token 丢失 | ⏳ [#1517](https://github.com/netease-youdao/LobsterAI/pull/1517) 待合并 |
| **低** | `skills-changed` 信号引发不必要的 gateway 重启 | ⏳ [#1521](https://github.com/netease-youdao/LobsterAI/pull/1521) 待合并 |

另有 [#2029](https://github.com/netease-youdao/LobsterAI/pull/2029) 修复了子代理记录因主键冲突导致的覆盖与缺失问题。

## 功能请求与路线图信号

**今日合并的新功能**暗示了项目下一步的发力方向：

- **插件生态互通**（[#2042](https://github.com/netease-youdao/LobsterAI/pull/2042)）：对接 OpenClaw 扩展目录，未来可能支持更多第三方插件源。
- **自定义模型参数**（[#2019](https://github.com/netease-youdao/LobsterAI/pull/2019)）：允许用户透传任意 `extra_body`，配合 Thinking 块显示，为推理模型或厂商特有参数提供弹性通道。
- **套餐模型上下文窗口**（[#2021](https://github.com/netease-youdao/LobsterAI/pull/2021)）：使引擎能精准截断上下文，提升长对话体验。
- **子代理全面可视化**（[#2011](https://github.com/netease-youdao/LobsterAI/pull/2011)、[#2027](https://github.com/netease-youdao/LobsterAI/pull/2027)~[#2030](https://github.com/netease-youdao/LobsterAI/pull/2030)）：基本补齐子代理的侧栏、详情页与渲染管线。

**仍处于开放状态的 PR** 也反映了用户诉求：

- **[#1522](https://github.com/netease-youdao/LobsterAI/pull/1522) — 动态模型列表获取**：从 provider API 拉取最新模型，减少手动维护。
- **[#1524](https://github.com/netease-youdao/LobsterAI/pull/1524) — 测试连接详细错误信息**：提升配置排错效率。
- **[#1526](https://github.com/netease-youdao/LobsterAI/pull/1526) — 会话颜色标注**：支持 7 种颜色标签，便于多会话管理。

若这些功能被纳入下一个版本，将进一步提高灵活性与用户体验。

## 用户反馈摘要

从相关 PR 描述中提取的真实用户痛点：

- **定时任务通知不可靠**（[#1510](https://github.com/netease-youdao/LobsterAI/pull/1510)）：用户配置 IM 通知后任务触发却静默失败，自动化工作流受阻。
- **QQ Bot 白名单配置阻塞**（[#1514](https://github.com/netease-youdao/LobsterAI/pull/1514)）：因 UI 缺少添加按钮，用户无法使用群组白名单，被迫退回到宽松模式。
- **认证流程脆弱**（[#1517](https://github.com/netease-youdao/LobsterAI/pull/1517)）：关闭设置面板导致 Copilot OAuth 令牌丢失，需要重复认证。
- **日志导出超时**（[#1515](https://github.com/netease-youdao/LobsterAI/pull/1515)）：用户无法导出日志用于调试或反馈，低配机器上尤为明显。
- **模型列表更新滞后**（[#1522](https://github.com/netease-youdao/LobsterAI/pull/1522)）：新模型发布后无法自动发现，需手动添加，不够及时。
- **会话管理缺少视觉区分**（[#1526](https://github.com/netease-youdao/LobsterAI/pull/1526)）：多个会话难以快速分辨，期望颜色标签功能。

这些反馈表明，虽然在功能迭代上快速前进，但稳定性与基础配置细节仍是用户关注的痛点。

## 待处理积压

以下 PR 自 4 月 7 日起开放，今日被标记为 stale，请维护者关注 review 与合并：

| PR | 类型 | 说明 |
|---|---|---|
| [#1510](https://github.com/netease-youdao/LobsterAI/pull/1510) | bug | 定时任务 IM 通知静默失败 |
| [#1514](https://github.com/netease-youdao/LobsterAI/pull/1514) | bug | QQ Bot 白名单 UI 缺失 |
| [#1515](https://github.com/netease-youdao/LobsterAI/pull/1515) | bug | 日志导出超时 |
| [#1517](https://github.com/netease-youdao/LobsterAI/pull/1517) | bug | Copilot OAuth 轮询未取消 |
| [#1521](https://github.com/netease-youdao/LobsterAI/pull/1521) | bug | skills-changed 误重启 gateway |
| [#1522](https://github.com/netease-youdao/LobsterAI/pull/1522) | enhancement | 动态模型列表获取 |
| [#1524](https://github.com/netease-youdao/LobsterAI/pull/1524) | enhancement | 测试连接详细错误信息 |
| [#1526](https://github.com/netease-youdao/LobsterAI/pull/1526) | enhancement | 会话颜色标注 |

这些 PR 均已有完整的修复方案或实现代码，且涉及用户直接感受的稳定性与易用性，建议尽早安排审阅并合入主分支。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据 2026-05-25 提供的 Moltis 项目数据生成的当日项目动态日报。

---

## Moltis 项目日报 | 2026-05-25

### 1. 今日速览
过去 24 小时，Moltis 项目展现出极高的维护冲刺态势。社区提交的 **8 个 Issue** 与 **10 个 Pull Request** 全部被关闭或合并，实现了“零新增积压”。核心架构迎来关键突破（Agent 作为能力边界），同时大量涉及安全与用户体验的 Bug 被闪电修复。项目健康度极佳，维护者的响应速度堪称典范。

---

### 2. 版本发布
今日无新版本发布。

---

### 3. 项目进展
项目在架构演进与社区反馈闭环上实现了双重飞跃，累计合并/关闭了 10 个 PR。

- **核心架构革新：** PR [#1049](https://github.com/moltis-org/moltis/pull/1049) 完成了重大重构，正式将 **Agent 作为能力边界**。每个 Agent 预设现在可以独立控制其模型、MCP 服务器、沙箱策略和技能，极大地提升了系统的模块化程度，为后续支持“儿童 vs 家长”等多用户/多渠道场景奠定了坚实基础。
- **功能增强落地：** PR [#1066](https://github.com/moltis-org/moltis/pull/1066) 积极响应社区需求，为 Agent 增加了运行时限制支持（`timeout_secs` 和 `max_iterations`），实现了对细粒度资源控制的承诺。
- **全面扫清积压：** 维护者（penso）对近期暴露的 8 个 Bug 和 1 个功能请求进行了集中攻坚，所有对应修复 PR 均在一天内被合并，项目正快速向稳定版本迈进。

---

### 4. 社区热点
今日社区讨论热度较低（评论数普遍为 0-1），但这并非因为缺乏关注，而是因为维护者的高效“秒修”策略直接化解了潜在讨论。

- **快速闭环引人注目：** Issue [#553](https://github.com/moltis-org/moltis/issues/553)（Agent 超时设置）和 Issue [#1054](https://github.com/moltis-org/moltis/issues/1054)（MCP 环境变量泄露）涉及核心功能与安全，本可能引发激烈讨论，但均在提出当日即被实现/修复并关闭。这种“即报即修”的模式本身就是社区最强烈的正面反馈。
- **贡献者高度活跃：** 贡献者 `IlyaBizyaev` 一次性提交了 3 个 Bug（#1052, #1053, #1054），均被完整修复，展现了高效的协作生态。

---

### 5. Bug 与稳定性
今日是项目的“Bug 清除日”，修复覆盖安全、功能和 UI 层面，按严重程度排列如下：

- **[严重] MCP 环境变量泄露：** Issue [#1054](https://github.com/moltis-org/moltis/issues/1054) 报告了一个严重安全漏洞，`mcp_list` API 会将标准 I/O MCP 服务器配置中的明文环境变量暴露给 LLM。该问题已由 PR [#1063](https://github.com/moltis-org/moltis/pull/1063) 通过 `Secret<String>` 类型严格隔离修复。
- **[中] OpenAI 兼容端点未校验：** Issue [#1051](https://github.com/moltis-org/moltis/issues/1051) 指出 `baseUrl` 缺少校验，且失败日志未包含完整构造 URL。PR [#1061](https://github.com/moltis-org/moltis/pull/1061) 已完善校验与日志逻辑。
- **[低-中] UI 与功能稳定性修复：**
  - 模型选择器不显示完整版本号（[#1052](https://github.com/moltis-org/moltis/issues/1052) -> PR [#1060](https://github.com/moltis-org/moltis/pull/1060)）
  - 会话标题自动生成功能失效（[#1053](https://github.com/moltis-org/moltis/issues/1053) -> PR [#1064](https://github.com/moltis-org/moltis/pull/1064)）
  - 聊天界面因工具栏出现横向滚动（[#1055](https://github.com/moltis-org/moltis/issues/1055) -> PR [#1062](https://github.com/moltis-org/moltis/pull/1062)）
  - 沙箱镜像预构建日志刷屏（[#1056](https://github.com/moltis-org/moltis/issues/1056) -> PR [#1065](https://github.com/moltis-org/moltis/pull/1065)）
  - 禁用外部 Agent 后 UI 仍有残留（[#1057](https://github.com/moltis-org/moltis/issues/1057) -> PR [#1059](https://github.com/moltis-org/moltis/pull/1059)）

---

### 6. 功能请求与路线图信号
社区的诉求在今日得到了高效的转化，凸显了路线的演进方向。

- **Agent 精细化配置：** Issue [#553](https://github.com/moltis-org/moltis/issues/553) 提出的“每个 Agent 的回环和超时设置”已由 PR [#1066](https://github.com/moltis-org/moltis/pull/1066) 实现。这表明项目组正在积极将 Agent 从单一配置实体转变为可独立调优的执行单元，是 PR [#1049](https://github.com/moltis-org/moltis/pull/1049) 架构变更的自然延伸。
- **进入“Agent 中心化”时代：** PR [#1049](https://github.com/moltis-org/moltis/pull/1049) 标志着 Moltis 正式将 Agent 作为系统的一级公民。未来版本的能力竞争点将围绕“如何定义、组合和管理这些 Agent”展开。

---

### 7. 用户反馈摘要
从今日处理的 Issue 中，可以提炼出以下核心用户痛点和满意点：

- **安全焦虑被及时回应：** 贡献者 `IlyaBizyaev` 和 `sayotte` 对 MCP 配置泄露和 URL 未校验的担忧得到了最高优先级响应。维护者通过代码层面的封装（`Secret<String>`）给予了最直接的安全感。
- **开发体验优化呼声高：** 用户对 “Docker 构建日志刷屏”（[#1056](https://github.com/moltis-org/moltis/issues/1056)）和“模型名显示不全”（[#1052](https://github.com/moltis-org/moltis/issues/1052)）等体验细节非常敏感，这些反馈的快速解决显著提升了开发者日常使用的流畅度。
- **UI 回归问题受关注：** `vvuk` 反馈的横向滚动问题（[#1055](https://github.com/moltis-org/moltis/issues/1055)）是“第二次”出现，说明 UI 布局维护仍是需要警惕的环节，PR [#1062](https://github.com/moltis-org/moltis/pull/1062) 加入的 Playwright 回归测试机制有望从根本上遏制此类问题。

---

### 8. 待处理积压
**当前状态：零积压。**

根据提供的数据，截至 2026年5月25日，Moltis 项目在过去 24 小时的活跃 Issue 和 PR 队列已完全清空。所有 Bug 均得到修复，所有功能请求均被合并，项目处于极度健康的状态。

**待观察：** 这种爆发式的合并后（特别是 PR [#1049](https://github.com/moltis-org/moltis/pull/1049) 的大规模架构变动），通常需要密切关注用户端是否会有新的回归问题出现。建议社区在未来 48 小时内重点测试 Agent 配置的兼容性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据您提供的 GitHub 数据（仓库来源：`agentscope-ai/QwenPaw`）生成的 **CoPaw (QwenPaw) 项目动态日报**。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-05-25

## 1. 今日速览
- **活跃度评估：极高** 🚀
- 过去 24 小时，项目经历了爆发式的社区互动与工程推进：共产生 **27 条 Issue**（关闭 13 条）和 **37 个 PR**（合并/关闭 24 个）。
- 尽管没有新版本发布，但项目健康度非常优秀：
  - **Bug 修复密集**：历史记录丢失、Markdown 表格渲染、推理模型 `<think>` 标签解析等核心 Bug 被集中攻克。
  - **测试套件大幅补全**：贡献者 `aqilaziz` 一次性合并了超过 10 个测试相关的 PR，系统加固了持久化、遥测、多渠道兼容等模块。
  - **大型功能蓄力待发**：“编码模式（Coding Mode）”、“DataPaw 数据分析插件”等重量级 PR 正在等待合并。

## 2. 版本发布
无

## 3. 项目进展
**亮点：系列 Bug 修复与测试基建的大规模推进**
- **社区信任修复**：
  - `fix: render table line breaks` ([PR #4379](agentscope-ai/QwenPaw/pull/4379))：解决了长期存在的 Markdown 表格内 `<br>` 换行符不渲染的问题。
  - `fix(providers): parse raw think tags` ([PR #4364](agentscope-ai/QwenPaw/pull/4364))：修复了 OpenAI 兼容接口返回的原始 `<think>` 标签无法被前端折叠为“思维链”的问题，显著提升推理模型体验。
- **新渠道与安全增强**：
  - `feat(QQ): add tool_guard interactive approval card` ([PR #4667](agentscope-ai/QwenPaw/pull/4667))：为 QQ 渠道增加了交互式工具授权卡片，提升了多端安全性。
  - `fix(DingTalk): use sender_id prefix` ([PR #4665](agentscope-ai/QwenPaw/pull/4665))：修复了钉钉会话 ID 后缀冲突导致的 Webhook 覆盖问题。
- **工程基建**：
  - **测试覆盖**：贡献者 `aqilaziz` 合并了覆盖环境变量、配置工具、时区检测、钉钉消息解析等核心模块的测试 PR，为后续快速迭代提供了安全网。
  - `fix(console): add dark mode support` ([PR #4599](agentscope-ai/QwenPaw/pull/4599))：修复了暗色模式下的 UI 可见性问题。

## 4. 社区热点
- **#4620 [已关闭]：聊天记录消失** (12 条评论)
  - **背景**：用户反复反馈切换 Session 后历史记录完全丢失，被认为是一个长期存在的致命 Bug。
  - **分析**：该 Issue 昨日已关闭，表明问题已得到紧急修复。这类数据安全问题能迅速解决，对维护社区信任至关重要。
- **#4644 [开放]：工具调用不实时显示** (9 条评论)
  - **背景**：Web 控制台中多数工具调用（除 `read_file` 外）需要手动刷新页面才能显示，且没有任何日志错误。
  - **分析**：这是当前影响日常调试和体验最直接的痛点，开发者社区呼吁极高。
- **#4653 [开放]：定时任务与用户消息共享 Session 导致中断** (4 条评论)
  - **背景**：Cron 任务在执行时，用户发消息会导致任务中断。
  - **分析**：暴露了 Session 管理机制在多任务场景下的设计缺陷，直接影响功能的可靠性。

## 5. Bug 与稳定性

| 严重程度 | 编号 | 描述 | 状态 | 链接 |
|---|---|---|---|---|
| 致命 | #4666 | 新建会话后 Models 配置页面完全丢失并报错 | **开放** | [Issue #4666](agentscope-ai/QwenPaw/issues/4666) |
| 高 | #4644 | 控制台工具调用需刷新页面才能显示 | **开放** | [Issue #4644](agentscope-ai/QwenPaw/issues/4644) |
| 高 | #4649 | 更新 `jobs.json` 后残留“孤儿”定时任务无限执行 | **开放** | [Issue #4649](agentscope-ai/QwenPaw/issues/4649) |
| 高 | #4653 | 定时任务被用户消息抢占中断 | **开放** | [Issue #4653](agentscope-ai/QwenPaw/issues/4653) |
| 中 | #4650 | GLM-5.1 思维链在控制台不显示 | **开放** | [Issue #4650](agentscope-ai/QwenPaw/issues/4650) |
| 中 | #4661 | 上下文压缩配置在 v1.1.8.post1 中未生效 | **已关闭** | [Issue #4661](agentscope-ai/QwenPaw/issues/4661) |
| 低 | #4663 | Telegram/Discord 中 `/models` 命令失效 | **已关闭** | [Issue #4663](agentscope-ai/QwenPaw/issues/4663) |

## 6. 功能请求与路线图信号
- **高概率纳入下版本**：
  - **Token 用量与速度显示** ([Issue #4647](agentscope-ai/QwenPaw/issues/4647), [对应 PR #4433](agentscope-ai/QwenPaw/pull/4433))：实现 PR 已在合并进程中，即将为用户提供可量化的监控数据。
  - **OpenCode 端点模型过滤** ([Issue #4656](agentscope-ai/QwenPaw/issues/4656), [PR #4660](agentscope-ai/QwenPaw/pull/4660))：防止用户选错模型导致 API 报错。
- **大型功能/路线图信号**：
  - **Coding Mode 编码模式** ([PR #4578](agentscope-ai/QwenPaw/pull/4578))：这是当前最瞩目的重大特性，在聊天面板旁嵌入浏览器 IDE，实现真正的编码 Agent。
  - **记忆系统增强** ([Issue #4652](agentscope-ai/QwenPaw/issues/4652))：用户提出了“总结-关联-提醒”机制，标志社区对 Agent 的要求已从“能记录”发展到“能学习”。
  - **DataPaw 数据分析插件** ([PR #4622](agentscope-ai/QwenPaw/pull/4622))：展示插件生态正在向专业领域纵深发展。
  - **Pet 远程连接守护进程** ([Issue #4645](agentscope-ai/QwenPaw/issues/4645))：试图实现“远程运行 Agent，本地 Puppet 显示”的分离式架构。

## 7. 用户反馈摘要
- **数据安全感亟需加固**：
  - 聊天记录丢失 (#4620)、Session 隔离失效导致中断 (#4653)、新建会话即丢失配置 (#4666) 等问题冲击了用户信任。
- **操作透明度是核心诉求**：
  - 大量反馈集中在“看不见”的体验上：工具调用看不见（#4644）、Token 用量看不见（#4647）、消息时间戳看不见（#4662）、启动进度看不见（#4664）。
- **UI 一致性有待统一**：
  - 用户反馈控制台页面风格不统一（环境变量动画 vs 其他页面），颜色样式不统一（模型/文档下拉箭头），细节决定品质。
- **本地化/配置兼容性**：
  - 升级版本后上下文压缩参数未继承生效（#4661），语音转录忽略配置的 Whisper 接口（#4556），这些配置失效问题令用户困惑。

## 8. 待处理积压（需维护者重点关注）
以下为长期未响应或可能陷入僵局的重要 Issue/PR，可能影响开发者社区的贡献积极性。

1.  **[大型桌面端重构] PR #3813: 添加 Tauri 2.x 桌面应用支持**
    - 作者：`youngchan1988` | 创建：2026-04-24 | **时长：31 天**
    - 关键性：对包体积、性能和安全性有质的提升。Review 周期过长，建议维护者给予明确推进时间表。
    - [PR #3813](agentscope-ai/QwenPaw/pull/3813)

2.  **[核心安全特性] PR #4267: Mac OS 文件路径白名单**
    - 作者：`gnipping` | 创建：2026-05-13 | **时长：12 天**
    - 关键性：引入文件白名单和沙箱机制，是 Agent 安全防护的关键一环。目前停留在等待 Review。
    - [PR #4267](agentscope-ai/QwenPaw/pull/4267)

3.  **[体验积压] Issue #4644: 工具调用不实时显示**
    - 报告：2026-05-23 | **时长：2 天 (但热度极高)**
    - 关键性：作为当前 Console 端的最大 UX 痛点，9 条评论代表了广泛社区呼声，建议优先解决。
    - [Issue #4644](agentscope-ai/QwenPaw/issues/4644)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 2026-05-25

---

## 1. 今日速览

过去24小时（截至 2026-05-25），ZeroClaw 项目整体维持高强度活跃，Issue 与 PR 更新数均达到 **50 条**。**8 个 PR 成功合并/关闭**，标志着飞书（Lark）渠道集成全面完工，DeepSeek 提供商关键 Bug 得到修正。但与此同时，**MCP 协议集成层面的可靠性问题集中爆发**（工具过滤失效、进程泄漏、延迟加载死锁），成为社区当前最焦虑的稳定性核心议题。此外，社区治理 RFC 引发了热烈讨论，表明项目正从“野蛮生长”向“规范化协作”过渡。

| 指标 | 数量 | 趋势 |
|---|---|---|
| Issue 更新总数 | 50（新开/活跃 46，关闭 4） | 🔴 高活跃 |
| PR 更新总数 | 50（待合并 42，合并/关闭 8） | 🔴 高活跃 |
| 新版本发布 | 0 | ⚫ 无 |

---

## 2. 版本发布

（无，今日无新版本发布。）

---

## 3. 项目进展

今日有多项关键功能完成合入，推进了项目正式功能集与基础设施成熟度：

### ✅ **飞书（Lark）渠道集成全面完工**
- **`[feat]` 支持 Lark 作为 Cron 定时任务目标渠道**（PR #6851）  
  🔗 [PR #6851](https://github.com/zeroclaw-labs/zeroclaw/pull/6851)
- **`[feat]` 实现 Lark 渠道的 `request_approval()` 审批弹窗**（PR #6852）  
  🔗 [PR #6852](https://github.com/zeroclaw-labs/zeroclaw/pull/6852)  
  → 至此 Lark 已成为继 Telegram、Slack 之后第三个具备“消息接收 → 工具调用 → 用户审批 → 结果推送”完整闭环的一线渠道，对国内企业用户意义重大。

### ✅ **DeepSeek 提供商基础 URL 修复**
- **`[fix]` 修正 DeepSeek 提供商硬编码基址**（PR #6753）  
  🔗 [PR #6753](https://github.com/zeroclaw-labs/zeroclaw/pull/6753)  
  → 用户现在可以配置自建 DeepSeek 网关或非官方代理，解决了企业级部署场景下的灵活性瓶颈。

### ✅ **渠道可选编译机制落地**
- **`[feat]` 引入 `default-channels` 特性捆绑包**（PR #6866）  
  🔗 [PR #6866](https://github.com/zeroclaw-labs/zeroclaw/pull/6866)  
  → 支持 `--no-default-features --features agent-runtime,channel-slack` 等组合，可显著缩小二进制体积与编译时间。

### ✅ **Email 渠道多项体验修复**
- **`[fix]` 修复 HTML 渲染、主题线程、附件路径解析**（PR #6512）  
  🔗 [PR #6512](https://github.com/zeroclaw-labs/zeroclaw/pull/6512)

### 🚧 **正在积极 Review 的大型功能 PR**
| 功能 | PR | 目标 |
|---|---|---|
| `channel_send` 工具 | [#6665](https://github.com/zeroclaw-labs/zeroclaw/pull/6665) | 解决 Cron 结果被动推送缺失 |
| `file_upload` 工具 | [#6773](https://github.com/zeroclaw-labs/zeroclaw/pull/6773) | HTTP 原生上传能力 |
| 多数据库会话后端 | [#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893) | Postgres/Oracle/MySQL/Db2 |
| TUI 终端界面 | [#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848) | 替代部分 Web / CLI 交互 |

---

## 4. 社区热点

### 🔥 治理架构 RFC：工作泳道与看板自动化
**Issue #6808** | 评论: 6 | 标签: `type:rfc`, `priority:p2`  
🔗 [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

**内容**：Contributor @Audacity88 提出了一份重量级的治理 RFC，旨在引入“轻型 PR 泳道”（Lightweight Lanes）以按风险等级分流 PR，同时实现工单看板自动化与标签命名规范整理。

**分析**：这是近期社区最值得关注的元-工程讨论。相比于具体功能的 Bug/Feature，这份 RFC 直接回应了 Issue/PR 数量激增带来的规模化管理挑战。如果落地，将显著降低维护者的认知负担，并让外部贡献者拥有更清晰的“下一步该做什么”指引。**路标信号：强，很可能被纳入 v0.80+ 路线图的治理部分。**

---

### 🔥 MCP 集成可靠性的大规模集中质疑

**Issue #6699**（`tool_filter_groups` 空操作，6 条评论）  
🔗 [Issue #6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)  
**Issue #6721**（`tool_search` 延迟加载 + Webhook 模式死锁，2 条评论）  
🔗 [Issue #6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721)  
**Issue #5903**（MCP 子进程每心跳泄漏一个，1 条评论）  
🔗 [Issue #5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)

- **用户画像**：这些问题的提出者（@nick-pape, @rordd）都附带了极高质量的根本原因分析与代码行定位，属于“黄金 Bug 报告”。
- **核心诉求**：MCP 是 ZeroClaw 区别于竞品的核心能力，但当前状态是**“文档承诺的功能在运行时不生效”（#6699）、依赖此功能的高级模式会导致死锁（#6721）、且在默认配置下会缓慢耗尽服务器进程资源（#5903）**。这些问题构成了一个系统性的“MCP 可靠性危机”，是当前整个社区最迫切希望看到解决的目标。

---

## 5. Bug 与稳定性

### 🚨 高危 / 工作流阻塞（S1 / P1 级别）

| # | 描述 | 组件 | 状态 | Fix PR |
|---|---|---|---|---|
| **#6647** | Cron 结果仅显示在 Web 面板，不推送到 Telegram 等渠道 | runtime/daemon | 讨论中 | 无 |
| **#6699** | `tool_filter_groups` 对真实 MCP 工具完全无效（前缀不匹配） | agent/runtime | accepted | 无 |
| **#6302** | Gemini 400 错误：Assistant tool_call 出现在首个 User 轮次之前 | provider/gemini | in-progress | 无 |
| **#6844** | Slack `bot_token` 不支持环境变量读取（违反 12-Factor） | channel/slack | accepted | 无 |
| **#6841** | `vision_provider` 配置被静默忽略，图片路由到 Fallback | provider/vision | accepted | 无 |
| **#6472** | Gateway 连接 Postgres 时报“Cannot start a runtime” Panic | gateway/memory | accepted | 无 |
| **#5962** | Ollama 提供商在工具调用场景下会话完全卡死 | provider/ollama | in-progress | 无 |
| **#5903** | MCP stdio 子进程在每次心跳（默认 30min）泄漏一个 | runtime/mcp | accepted | 无 |

### ⚠️ 中等风险（S2 / P2-P1 级别）

| # | 描述 | 严重性 | Fix PR |
|---|---|---|---|
| **#6254** | WASM 插件安装路径与扫描路径分歧，导致插件不可见 | S2 | 无 |
| **#6856** | Schema v3 中 `show_tool_calls` 丢失 | S2 | 无 |
| **#6723** | OpenAI 原生提供商硬编码 120s 超时，忽略 `timeout_secs` | S2 | 无 |
| **#6884** | `web_fetch` 设置 `max_response_size=0` 时仅读取 1 字节 | S2 | **[已在 #6884 审核中](https://github.com/zeroclaw-labs/zeroclaw/pull/6884)** |
| **#6885** | Gateway WebSocket 节点在 `nodes.enabled=false` 时仍可访问且可选认证 | **安全风险** | **[已在 #6885 审核中](https://github.com/zeroclaw-labs/zeroclaw/pull/6885)** |
| **#6910** | Shell 执行时孙子进程继承管道句柄导致挂起 | S2 | **[已在 #6910 审核中](https://github.com/zeroclaw-labs/zeroclaw/pull/6910)** |
| **#6911** | Agent 初始化时忽略 `runtime_profile`，始终使用默认预算 | S2 | **[已在 #6911 审核中](https://github.com/zeroclaw-labs/zeroclaw/pull/6911)** |

---

## 6. 功能请求与路线图信号

### 📌 强路线图信号（推测纳入 v0.80 beta）

| 功能 | 链接 | 判断依据 |
|---|---|---|
| **Cron 主动推送**（`channel_send` 工具） | [PR #6665](https://github.com/zeroclaw-labs/zeroclaw/pull/6665) | 直接匹配高优 Bug #6647 需求，且代码质量成熟 |
| **TTUI 终端界面** | [PR #6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848) | XL 级重构，标记为 `risk:high`，可能是长期主干分支 |
| **多数据库会话** | [PR #6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893) | 为多 Agent 集群铺路，基础设施信号 |
| **Memory Strategy 特质** | [PR #6907](https://github.com/zeroclaw-labs/zeroclaw/pull/6907) | 解耦内存生命周期策略，架构优化信号 |
| **治理 RFC #6808** | [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | 社区一致看好，标签清理和泳道分流降低成本 |

### 📌 社区呼吁的新 Providers / Channels

| 功能 | 链接 | 当前状态 |
|---|---|---|
| Arcee AI 提供商 | [Issue #6456](https://github.com/zeroclaw-labs/zeroclaw/issues/6456) | in-progress |
| Mastodon 渠道 | [Issue #6423](https://github.com/zeroclaw-labs/zeroclaw/issues/6423) | in-progress |
| Twilio SMS 渠道 | [Issue #6427](https://github.com/zeroclaw-labs/zeroclaw/issues/6427) | in-progress |
| Rocket.Chat 渠道 | [Issue #6435](https://github.com/zeroclaw-labs/zeroclaw/issues/6435) | in-progress |
| Zulip 渠道 | [Issue #6437](https://github.com/zeroclaw-labs/zeroclaw/issues/6437) | in-progress |

---

## 7. 用户反馈摘要

### 👍 正向反馈
- **飞书渠道的完善**获得了企业用户的明确肯定，特别是 Cron 投递和审批弹窗的补全被认为“具备了与 Slack 同等的生产级可用性”（源自 PR #6851 / #6852 讨论串）。

### 👎 痛点与批评

1. **“配置承诺不兑现”是最普遍的负反馈**：
   - `tool_filter_groups` 不生效（#6699）→ 用户称这是“配置语法看起来有效但实际零输出的典型诱饵问题”。
   - `vision_provider` 不生效（#6841）→ “我花了两个小时检查模型名大小写，但原因是代码根本没读这个段”。
   - `show_tool_calls` V3 回归（#6856）→ “这是一次不可接受的降级，升级后功能反而减少了”。

2. **“Cron 只能看不推送”阻碍自动化场景**：
   - **用户原话**（#6647）：“定时任务的结果只出现在 Web 面板的角落，而不是我配置的 Telegram/Slack 群里。Cron 功能因此失去了最关键的价值——被动通知。”

3. **MCP 高期望 vs 低可用性**：
   - 核心 MCP 用户群体的批评集中在：“MCP 的概念很好，但目前运行时中的进程泄漏、路径分歧和过滤失效让我不得不关掉它”。

---

## 8. 待处理积压

以下 Issue / PR 距今已超过合理处理窗口，建议维护者团队优先给予关注或官方回复：

| # | 类型 | 描述 | 存活时长 | 建议行动 |
|---|---|---|---|---|
| **#5903** | Bug | MCP stdio 子进程每心跳泄漏一个（P1） | **37 天** | 紧急分配 P0 级修复，这是生产部署死线问题 |
| **#5122** | Bug | `allowed_private_hosts` 域名解析到内网 IP 时防御绕过 | **57 天** | 安全性 Bug，需确认 Next Action |
| **#6074** | Meta | 153 次提交被回滚后的审计与恢复计划 | **31 天** | 这是代码库的一次信任事件。建议指定维护者发布审计方案 |
| **PR #5838** | Enhancement | Webhook 渠道指数退避重试 | **38 天** | 代码完整，等待 Review |
| **PR #5450** | Enhancement | 工具层 IPv6 支持 | **48 天** | 等待作者回应（`needs-author-action`），建议维护者介入判定 |

---

*本报告基于 ZeroClaw 公开 GitHub 仓库 2026-05-24 ~ 2026-05-25 数据生成，由 AI 助理自动整理。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*