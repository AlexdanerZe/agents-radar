# OpenClaw 生态日报 2026-06-18

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-18 03:37 UTC

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

# OpenClaw 项目动态日报 — 2026-06-18

---

## 1. 今日速览

OpenClaw 项目在 2026 年 6 月 18 日维持了**极高强度**的社区活跃度，24 小时内 **500 条 Issues 更新**（其中 480 条新开/活跃）、**500 条 PR 更新**（409 条待合并），呈现出社区“高产”与维护者“高压”并行的局面。今日**无新版本发布**，但多个高优先级修复 PR（如插件作用域解析、Session 压缩超时、子 Agent 消息投递）已进入待审核状态。项目在**安全边界加固、会话状态重构（SQLite 迁移）以及多 Agent 架构演进**上方向明确，但安全类（文本泄露、OAuth 卡死）和稳定性回归问题正快速累积，对项目健康度构成挑战。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

项目今日在多个关键基础设施模块上取得了实质性的修复/推进。

### 已合并/关闭的 PR
| PR | 关联问题 | 要点 |
|---|---|---|
| [#94396](https://github.com/openclaw/openclaw/pull/94396) [CLOSED] | - | **修复(sandbox):** 沙箱技能同步时 `ensureSandboxWorkspaceLayout` 回退到硬编码路径，现已改为解析用户配置。 |

### 待审核的核心修复 PR（Ready for maintainer / Proof supplied）
- **[P1, #94343](https://github.com/openclaw/openclaw/pull/94343) — 修复插件方法作用域解析:**
  `openclaw workboard dispatch` 因 `resolveScopedMethod` 只查 gateway 注册表、未查插件描述符而失败。PR 将其改为跨所有活动表面（网关、插件、通道）进行作用域解析。**安全边界修正，影响面大。**
- **[#94413 / #94407](https://github.com/openclaw/openclaw/pull/94413) — 修复合并超时硬编码:**
  大 Session（~20 万 token）压缩因外层聚合等待写死为 60 秒而静默失败。PR 将超时改为读取用户配置的 `compaction.timeoutSeconds`。
- **[#94375](https://github.com/openclaw/openclaw/pull/94375) — 子 Agent 完成通知的文本投递回退:**
  当请求方 Session 不活跃或锁定时，原有唤醒/通道投递均失败。PR 增加了纯文本回退，减少了消息静默丢失的场景。
- **[#87449](https://github.com/openclaw/openclaw/pull/87449) — Mattermost 文本块边界修复:**
  解决 Mattermost 渠道中草稿预览时文本块在多次工具调用回合中被覆盖丢失的问题，对齐 Discord 已有行为。
- **[#94383](https://github.com/openclaw/openclaw/pull/94383) — Skill Workshop 持久化“始终允许”审批:**
  为 Skill Workshop 生命周期操作添加了基于工作区目录的持久化一次性审批能力，改善市场生态用户体验。
- **[#93853](https://github.com/openclaw/openclaw/pull/93853) — 修复内存嵌入提供者路由:**
  当 `memorySearch` 提供者名为 `"openai"` 但配有自定义 `baseUrl` 时，之前直接走 OpenAI 适配器短路，现已改为通过通用提供者解析层路由。
- **[#94393](https://github.com/openclaw/openclaw/pull/94393) — Windows Ctrl+C 支持:**
  基于 `readline` 的按键事件处理，解决 Windows 下网关前台模式无法被 Ctrl+C 退出的问题。

**总评：** 项目在**插件系统架构、Session 状态持久化、渠道消息可靠性**三个方向的内部质量修复上稳步推进，但大量重要 PR 仍积压在 `needs-maintainer-review` 或 `waiting on author` 状态，审核吞吐量是当前进度的主要瓶颈。

---

## 4. 社区热点

今日讨论最活跃/反应最强烈的 Issues：

| Issue | 评论数 | 👍 | 核心诉求 |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) (**Text between tool calls leaks**) | **32** | 1 | **严重UX/安全问题：** Agent 在工具调用之间产生的内部处理文本（错误处理、确认、叙述）会直接路由到 Slack/iMessage 等消息渠道暴露给用户。用户要求将内部日志与对外输出严格分离。 |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) (**Track SQLite migration via accessor seam**) | **30** | 1 | **架构变革关注：** 社区高度关注核心 Session/Transcript 向 SQLite 的迁移。开发团队选择通过 accessor seam 分小 PR 推进，避免一次性大规模重构的高风险。 |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) (**Prebuilt Android APK releases**) | **25** | 2 | **移动端呼声高：** 持续 4 个多月，用户希望 GitHub Releases 提供预编译的 Android 伴侣 App APK，降低自行编译门槛。 |
| [#68596](https://github.com/openclaw/openclaw/issues/68596) (**Configurable streaming watchdog timeout**) | **15** | **8** | **模型兼容性痛点：** 使用 Kimi-k2.5、DeepSeek-R1 等长推理模型的用户频繁触发 30 秒流式看门狗超时，要求提供可配置的超时阈值。 |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) (**Control UI requires device identity**) | 17 | **5** | **生产环境阻塞：** Hostinger VPS / Docker 用户遭遇 Control UI 要求 HTTPS/Localhost 安全上下文，属于回归且没有提供反向代理之外的工作区。 |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) (**Dynamic model discovery for OpenRouter**) | 9 | **3** | **模型市场诉求：** 用户希望抛弃静态模型列表，具备从 OpenRouter 等动态提供商自动发现模型的能力。 |
| [#28300](https://github.com/openclaw/openclaw/issues/28300) (**Theme Customization System**) | 6 | **5** | **UI 美化期望：** 用户希望 Control UI 提供预设主题 + 自定义主题工作室功能，高赞但没有维护者分配。 |

**分析：** 社区讨论的核心矛盾逐渐从“功能有无”转向“成熟度与安全性”。文本泄露（#25592）和 OAuth 卡死（#86215）等可靠性/安全问题获得了大量关注，表明用户正在将 OpenClaw 推往更严格的生产与安全场景。

---

## 5. Bug 与稳定性

### 严重安全/数据丢失（Impact: security / message-loss / crash-loop）

| Issue | 严重程度 | 状态 | 修复 PR |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) Text 在 tool call 间泄露 | **P1, 🐚 Platinum Hermit** | 需产品决策/安全评审 | **无** |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) Codex OAuth 失效后 Agent 卡死数小时 | **P1, 🐚 Platinum Hermit** | 需要 live repro | **无** |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) Signal 重启竞态致孤儿进程 | **P1, 🦞 Diamond Lobster** | 有 linked PR | 关联 PR 待合 |
| [#39476](https://github.com/openclaw/openclaw/issues/39476) A2A 双向 sessions_send 导致重复消息 | **P1, 🐚 Platinum Hermit** | 需要 live repro | **无** |

### 严重回归/功能阻断（Impact: session-state / crash-loop / auth-provider）

| Issue | 严重程度 | 摘要 |
|---|---|---|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | **P1, Regression** | Google Vertex / Gemini 3.1 在升级到 2026.3.2 后报 `Cannot convert undefined or null to object` |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | **P2, Regression** | Control UI 在非 Localhost 下要求设备身份，VPS 用户被阻塞 |
| [#31331](https://github.com/openclaw/openclaw/issues/31331) | **P1, Behavior Bug** | Docker 内运行 Gateway + 沙箱时 `/workspace` 绑定挂载失败 |
| [#41201](https://github.com/openclaw/openclaw/issues/41201) | **P2, Regression** | Control UI 头像无法显示（外链 404 / 路径解析失败） |
| [#43747](https://github.com/openclaw/openclaw/issues/43747) | **P2, Regression** | 团队成员间 Memory 行为不一致（同一项目存储路径/分块策略各异） |
| [#41744](https://github.com/openclaw/openclaw/issues/41744) | **P1, Stale** | 飞书 `read` 图像工具结果在最终出包前丢失媒体附件 |

### 已有修复 PR 的 Bug
- **[P1, #94343](https://github.com/openclaw/openclaw/pull/94343)** → 修复插件作用域缺失问题。
- **[#94413](https://github.com/openclaw/openclaw/pull/94413)** → 修复 Session 压缩超时硬编码。
- **[#94375](https://github.com/openclaw/openclaw/pull/94375)** → 修复子 Agent 投递失败无回退。
- **[#94044](https://github.com/openclaw/openclaw/pull/94044)** → 修复 Matrix 因 MEGOLM 解密失败导致网关停机。
- **[#94393](https://github.com/openclaw/openclaw/pull/94393)** → 修复 Windows Ctrl+C 失效。

---

## 6. 功能请求与路线图信号

### 高可能纳入下版（已有清晰 PR 或极高社区共识）
- **安全/合规:**
  - `#10659` [Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) — 防止 Agent 读取原始 API Key
  - `#13583` [Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) — 函数级强制前置调用门控
  - `#7707` [Memory Trust Tagging](https://github.com/openclaw/openclaw/issues/7707) — 按来源标记记忆可信度
- **会话管理:**
  - `#22438` [Tiered bootstrap loading](https://github.com/openclaw/openclaw/issues/22438) — 分层加载引导文件以节省 token
  - `#13700` [Session Snapshots](https://github.com/openclaw/openclaw/issues/13700) — 保存/加载上下文检查点
- **渠道增强:**
  - `#20786` [Telegram Business](https://github.com/openclaw/openclaw/issues/20786) — 支持商业版 Telegram 消息
  - `#12602` [Slack Block Kit](https://github.com/openclaw/openclaw/issues/12602) — 富交互消息支持
  - `#33413` [Slack 工具级状态](https://github.com/openclaw/openclaw/issues/33413) — 实时显示当前执行的工具
- **系统/运维:**
  - `#42475` [Per-agent cost budgets](https://github.com/openclaw/openclaw/issues/42475) — 网关级花费预算阀值
  - `#68596` [Configurable streaming timeout](https://github.com/openclaw/openclaw/issues/68596) — 可配流式传输超时

### 远期架构信号
- `#35203` [Multi-Agent 协作框架](https://github.com/openclaw/openclaw/issues/35203) — 能力画像 + 共享黑板 + 分层记忆 + Token 治理
- `#42026` [分布式 Agent 运行时](https://github.com/openclaw/openclaw/issues/42026) — 控制面与计算面分离
- `#40418` [Session 记忆自动保全](https://github.com/openclaw/openclaw/issues/40418) — `/new` 时自动合成上一轮记忆
- `#10687` [动态模型发现](https://github.com/openclaw/openclaw/issues/10687) — 移出静态模型列表，动态查询 OpenRouter

---

## 7. 用户反馈摘要

| 反馈类型 | 代表 Issue | 引用 |
|---|---|---|
| **机密性与可用性的冲突** | [#25592](https://github.com/openclaw/openclaw/issues/25592) | “Internal processing output, failed exec… that text gets routed to the active messaging channel as a visible message. This is a significant UX problem.” |
| **配置行为不可预测** | [#43747](https://github.com/openclaw/openclaw/issues/43747) | “I never see any of our memory is managed in same way. Mine keeps chunking & embedding… my colleague A, her claw is storing… different location?” |
| **模型支持局限** | [#68596](https://github.com/openclaw/openclaw/issues/68596) | “When using models that perform extended reasoning… the streaming watchdog frequently triggers warnings. The backend may have dropped this run silently.” |
| **生产环境脆弱** | [#32473](https://github.com/openclaw/openclaw/issues/32473) | “I'm using a Hostinger VPS and Docker… control ui requires device identity (use HTTPS or localhost secure context). I can't find how to solve this.” |
| **更新即回归** | [#38327](https://github.com/openclaw/openclaw/issues/38327) | “After updating to 2026.3.2, any message causes embedded agent to fail with ‘Cannot convert undefined or null to object’.” |
| **开箱即用体验差** | [#9443](https://github.com/openclaw/openclaw/issues/9443) | “I would like to have prebuilt APK downloads available in GitHub releases. Currently the repository includes Android source code… but no precompiled APK.” |

---

## 8. 待处理积压

以下长期未响应的 Issue 与 PR 对项目健康度与用户信任具有显著影响，建议维护者优先关注：

### 高影响长期未决 Issue

| Issue | 创建时间 | 原因 |
|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) **文本泄露** | 2026-02-24 | 4个月无 PR，需产品与安全联合决策 |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) **Android APK** | 2026-02-05 | 4个月持续高关注，社区多次提及 |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) **Codex OAuth 卡死** | 2026-05-24 | 严重生产可靠性问题，需 aggressive profile 切换 |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) **Webhook 多轮对话失效** | 2026-02-08 | 文档声明支持但代码绕过硬编码，linked PR 存在 |
| [#41744](https://github.com/openclaw/openclaw/issues/41744) **飞书图片丢失** | 2026-03-10 | 标记 stale，有 linked PR |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) **动态模型发现** | 2026-02-06 | 用户持续+1，需产品方向性决策 |

### 等待作者回复的 PR（Status: waiting on author）

| PR | 问题 |
|---|---|
| [#75403](https://github.com/openclaw/openclaw/pull/75403) | ClawSweeper 机器人在修输入状态指示器残留回退，等待作者确认 |
| [#42637](https://github.com/openclaw/openclaw/pull/42637) | 技能列表截断时显示被省略的技能名，等待作者补充 |
| [#28081](https://github.com/openclaw/openclaw/pull/28081) | `doctor config` 自动清理废弃插件配置，等待作者更新 |

---

**总结：** OpenClaw 项目正处于**社区需求爆炸增长与内部架构质量重构并行**的关键阶段。短期的 Bug 积压和审核瓶颈是显性风险，但 SQLite 迁移、插件 SDK 重构、安全门控等方向的选择是正确的。维持当前的高强度修复节奏、加速高优 PR 审核、并对文本泄露（#25592）等长期悬而未决的核心问题作出决策，是项目健康度提升的核心关键点。

---

## 横向生态对比

# 2026-06-18 个人AI智能体开源生态横向对比分析报告

---

## 1. 生态全景

过去24小时，个人AI助手/自主智能体开源生态维持**极高活跃度**，但热潮之下分化明显。头部项目（OpenClaw、IronClaw、ZeroClaw）单日Issues+PR合计近百至千量级，社区吞吐量巨大；与此同时，安全事件集中爆发——TinyClaw、LobsterAI、OpenClaw等至少5个项目在同一天被曝出高危或严重安全漏洞，显示出在快速功能迭代中安全设计的普遍滞后。跨项目共同趋势包括：**多Agent互联与协作架构**成为下一代核心诉求，**桌面/计算机操控能力**开始从实验走向发布，**Windows兼容性、配置简化与移动端支持**则成为制约用户扩大的共性瓶颈。整体而言，生态正从“功能丰富度竞争”转向“成熟度、安全性与易用性竞争”。

---

## 2. 各项目活跃度对比

| 项目 | Issues更新数 | PR更新数 | 版本发布 | 健康度评估 | 活跃度等级 |
|------|------------|--------|---------|-----------|--------|
| **OpenClaw** | 500（480新开） | 500（409待合并） | 0 | 高产但高压，安全风险累积 | 极高 |
| **NanoBot** | 9 | 31（17合并） | 0 | 极佳，响应迅速 | 极高 |
| **Hermes Agent** | 50 | 50 | 0 | 高速迭代，P1 Bug待解 | 极高 |
| **PicoClaw** | 4（2新开） | 10（6合并） | 0 | 良好，安全快速闭环 | 高 |
| **NanoClaw** | 5 | 20（3合并） | 2（v2.1.0/v2.1.17） | 良好，安全PR待审 | 高 |
| **NullClaw** | ~5（讨论） | 2（待合并） | 0 | 一般，核心Bug积压 | 中 |
| **IronClaw** | 47（25新开） | 50（17合并） | 0 | 良好，修复效率高 | 极高 |
| **LobsterAI** | 1（安全） | 11（全合并） | 1（v2026.6.15） | 中等，严重安全未响应 | 高 |
| **TinyClaw** | 3（全安全） | 0 | 0 | 差，安全危机 | 中（安全驱动） |
| **Moltis** | 2 | 1（待合并） | 0 | 良好，稳定 | 中低 |
| **CoPaw** | 72（关闭39） | 72（关闭33） | 2（v1.1.12 / beta.2） | 良好，回归问题可关注 | 极高 |
| **ZeptoClaw** | 0 | 0 | 0 | 停滞 | 无 |
| **ZeroClaw** | 50（49新开） | 50（11合并） | 0 | 良好，Windows测试缺口 | 极高 |

*注：Issues/PR更新数指过去24小时变动总量，包含新开、活跃、关闭、合并等多种操作。活跃度为综合判断。*

---

## 3. OpenClaw在生态中的定位

OpenClaw依然是生态中**社区规模最大、协作密度最高**的参照级项目（单日500+ Issues/PR），其插件系统架构、Session压缩、子Agent消息投递等方向的技术决策直接影响大量下游项目。与同类相比：

- **优势**：生态辐射力强，PR和Issue讨论深度高，安全性（文本泄露等）和稳定性回归虽被社区诟病，但暴露后能迅速形成修复PR。SQLite迁移、插件SDK重构等架构级升级显示其对长期技术债的重视。
- **劣势**：审查吞吐量严重不足（409条待合并PR），核心P1安全Bug（文本泄露#25592）悬而未决超4个月，维护效率已被NanoBot、IronClaw等“轻量高响应”项目反超。与PicoClaw、NanoClaw等敏捷项目相比，OpenClaw的社区产出与维护投入失衡问题最突出。
- **技术路线差异**：OpenClaw走通用核心+插件集市路线，目标是成为“智能体操作系统”；而NanoBot、Hermes更侧重安全模型和通道体验，ZeroClaw更强调配置管理和工程化。OpenClaw仍是生态中覆盖面最广的平台，但若无法解决审核瓶颈，其“参照”地位可能被更敏捷的竞争者逐步侵蚀。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/事件 |
|----------|--------|--------------|
| **安全加固与漏洞修复** | OpenClaw（#25592文本泄露）、TinyClaw（#282-#284三个漏洞）、LobsterAI（#2176任意文件读取）、ZeroClaw（#7902 SSRF保护）、NanoBot（工作区权限修复）、PicoClaw（#3070 SSRF立即修复） | 默认安全、输入/输出隔离、认证绕过、文件路径校验成为集体短板，多个项目在同日出现安全事件，表明行业正处于“安全补课”期。 |
| **多Agent互联与协调** | OpenClaw（子Agent投递）、Hermes（A2A协议需求，#514）、CoPaw（Agent互聊死循环，#5204）、ZeroClaw（ACP会话历史回放）、NanoBot（多实例/多租户，#936） | 社区不满足于单Agent，期望建立“智能体联邦”，但互操作协议（A2A、ACP）和死循环检测等基础问题仍缺标准解法。 |
| **Computer Use / 桌面操控** | LobsterAI（v2026.6.15正式发布Computer Use）、Hermes（#48180 Linux Computer Use后端）、ZeroClaw（#6909 RFC桌面GUI控制） | Agent从对话扩展到直接操作屏幕/操作系统，是下一波能力竞争的制高点。LobsterAI率先发布提供了参考实现。 |
| **Windows兼容性** | OpenClaw（#94393 Windows Ctrl+C）、Hermes（#48100更新权限、#46260安装失败）、ZeroClaw（#7853自更新修复、#7462 74项测试失败）、CoPaw（无特别提及，但其他项目凸显短板） | Windows用户占比不低，但兼容性问题长期未被系统解决，近期多个项目集中攻关，反映出向“全平台覆盖”的共识。 |
| **配置简化与文档易用性** | NullClaw（#861 用户抱怨文档晦涩）、NanoBot（#4376 向导不友好）、NanoClaw（多个技能缺前置条件）、OpenClaw（#9443 APK预编译降低门槛） | 随着用户从开发者向普通爱好者扩散，“开箱即用”不再是口号而是刚需，无简化配置的项目将面临增长瓶颈。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|------|---------|---------|------------|
| **OpenClaw** | 全功能核心框架 + 插件集市 | 开发者、社区运维者 | 多表面作用域、插件SDK、SQLite重构 |
| **NanoBot** | 安全工作区 + 多Provider + 飞书通道 | 开发者、项目管理者 | 工作区安全模型、强Provider兼容、CLI+WebUI |
| **Hermes Agent** | Desktop原生体验 + A2A互操作 | 个人开发者、企业早期采用者 | Electron桌面、计算机操控、OTLP可观测 |
| **PicoClaw** | 轻量嵌入式 + 去中心化网关 | 资源受限设备、隐私优先用户 | Rust实现、OneBot/DeltaChat、低资源占用 |
| **NanoClaw** | CLI优先 + 消息组管理 + 结构化SDK | CLI偏好者、自动化运维 | OneCLI SDK、outbound.db日志、升级合规 |
| **NullClaw** | 个人轻量Agent + 记忆控制 | 个人开发者、本地模型用户 | 极简配置、JSON记忆策略、REPL交互 |
| **IronClaw** | 生产力自动化 + Reborn WebUI | 企业团队、NEAR生态用户 | Reborn v2 UI、Projects实体、AWS Bedrock |
| **LobsterAI** | 多模态 + Computer Use + 实时语音 | 网易生态用户、多模态开发者 | ASR语音输入、Computer Use、OpenClaw网关集成 |
| **TinyClaw** | 极简接口 + 最小原型 | 实验者、快速验证 | 接口极简，但安全严重缺失 |
| **Moltis** | TTS/语音输出 + 导出集成 | 语音交互场景、内容创作者 | 聚焦TTS配置、Markdown导出、WebUI RPC |
| **CoPaw** | 渠道丰富 + UI重构 + AgentScope生态 | 国内用户、多渠道集成 | 多渠道（飞书、钉钉等）、Provider聚合UI、v2路线图 |
| **ZeroClaw** | 工程化配置 + 安全 + 多里程碑规划 | 严肃开发者、企业运维 | 类型化别名、WASM插件、Windows更新修复、SSRF |

**关键差异提炼**：OpenClaw和ZeroClaw追求“大而全”的平台化；NanoBot、Hermes、IronClaw聚焦特定场景深度优化；PicoClaw走轻量专用路线；CoPaw、LobsterAI深度绑定特定云生态/区域市场；TinyClaw和Moltis为小型实验项目。功能性上，Computer Use和实时语音仅LobsterAI已发布，多Agent互联仅Hermes和ZeroClaw有明确协议投入。

---

## 6. 社区热度与成熟度

**极高活跃度（日更新50+）**：OpenClaw、IronClaw、ZeroClaw、NanoBot、Hermes、CoPaw。这些项目Issues和PR数双高，社区讨论活跃，但OpenClaw存在审核积压，反之CoPaw和NanoBot在产出与合并间更平衡。

**高活跃度（日更新10-50）**：PicoClaw、NanoClaw、LobsterAI。项目处于密集迭代周期，LobsterAI虽然合并效率高但安全漏洞未响应是隐患。

**中等活跃度（日更新1-10）**：NullClaw、TinyClaw（安全事件推高单日但整体贡献低）、Moltis。NullClaw和Moltis开发节奏平缓，TinyClaw活跃度由安全报告驱动而非正向开发。

**低/无活跃度**：ZeptoClaw。连续无活动表明项目可能停滞。

**成熟度分层**：
- **较成熟/规划清晰**：OpenClaw（架构方向明确）、ZeroClaw（版本里程碑细化至v0.8.x/v0.9.0）、CoPaw（稳定发布+UI重构）、IronClaw（Reborn走向生产）。
- **快速成长但架构仍在塑形**：NanoBot、Hermes、PicoClaw、NanoClaw。
- **早期实验或瓶颈期**：NullClaw、TinyClaw、Moltis、ZeptoClaw。

---

## 7. 值得关注的趋势信号

1. **安全事件从“偶发”变成“集体爆发”**：TinyClaw、LobsterAI、OpenClaw、PicoClaw、ZeroClaw在同日出现安全修复或报告，表明行业在功能竞赛中普遍忽略了安全设计。对于开发者而言，**“默认安全”和“输入输出审计”必须成为新建项目的基线要求**。

2. **多Agent互联从“愿望”走向“刚需”**：Hermes的A2A协议请求、CoPaw的互聊死循环、ZeroClaw的ACP支持，说明用户已不满足于单个Agent，并开始在实际部署中遇到跨Agent协调问题。这一趋势推动下一波基础设施（Agent发现、通信协议、共享记忆）的发展。

3. **Computer Use成为新能力分水岭**：LobsterAI成为首个正式发布该功能的开源项目，Hermes和ZeroClaw紧随其后。**能够安全可靠地操控桌面的Agent将开辟自动化测试、RPA、个人助理等全新场景**，也是产品差异化的核心。

4. **Windows兼容性受关注度快速上升**：多个项目同时投入修复（更新机制、Ctrl+C、权限、测试覆盖），反映出**个人用户中Windows占比远超维护者预期**。忽视Windows兼容性将显著限制用户规模。

5. **配置与文档成为增长瓶颈**：从NullClaw“70%的README看不懂”到NanoClaw技能文档缺前置条件，再到NanoBot的“向导不够友好”，说明**当核心功能趋于同质化后，用户流失原因从“功能不够”转为“上手太难”**。投资Onboarding体验的回报率将高于添加新功能。

---

*报告基于2026-06-18各开源项目公共GitHub数据生成，所有分析仅反映当日快照。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是为你生成的 NanoBot 项目动态日报。

---

# NanoBot 项目动态日报 | 2026-06-18

## 1. 今日速览
今日 NanoBot 项目处于**极高活跃度**状态。**31 项 PR** 在 24 小时内得到更新，其中 **17 项已合并/关闭**，**14 项待处理**，开发与维护节奏紧凑。社区在 Issues 中提出了 **9 个问题**，涵盖了从工作区权限阻断性 Bug 到移动端 UI 体验优化等多个维度。维护团队响应迅速，针对 Git 命令阻断、代理冲突等高频问题已实现当日快速修复并合并。项目整体健康度极佳，正处于密集的功能迭代与稳定性加固期。

## 2. 版本发布
无

## 3. 项目进展

**工作区安全模型重塑**
- 合并了 PR #4053 与 PR #4202，系统性地重构了文件系统工具（`apply_patch`、读写工具）的安全策略。明确了额外允许目录的只读属性，并分离了读写权限。这是对工作区安全模型的一次根本性加固。
- 合并了 PR #4380，直接修复了 Git 命令在 Workspace 子目录下被安全策略误杀的问题（关联 Issue #4375），保障了开发流工作者的基础 Git 操作流畅性。

**重要 Provider 扩展与兼容性修复**
- **Mistral 支持增强 (PR #4351, 已合并)**：适配了 Mistral API 对 `reasoning_effort` 参数的严格限制，并支持了`multi-text` 消息结构，大幅提升了该提供者的可用性。
- **Anthropic 兼容 (PR #4356, 已合并)**：修复了跨会话或跨 Provider 时，`tool_use` 与 `tool_result` ID 包含非法字符导致 Anthropic API 返回 400 错误的问题。
- **OpenAI 图像编辑 (PR #4394, OPEN)**：新增了对 OpenAI 参考图像编辑（`/images/edits`）端点的支持，为 GPT-Image 模型提供了清晰的调用路径。
- **代理冲突修复 (PR #4367, 已合并)**：解决了系统环境变量（`HTTP_PROXY`）误伤本地模型服务器（Ollama/vLLM）请求的问题，显著优化了混合网络环境用户的体验。

**飞书 (Feishu) 通道持续演进**
- **流式更新健壮性 (PR #4381, 已合并)**：为飞书 CardKit 流式更新增加了失败重试机制，并兜底关闭空白的流式卡片。
- **二维码注册 (PR #4391, OPEN)**：新增了通过手机飞书扫码即可自动注册 Bot 的 CLI 命令，极大简化了机器人的首次创建流程。

**对话与记忆机制微调**
- 合并了 PR #4349，修复了在重放窗口（Replay Window）中，长用户轮次（包含大量工具调用信息）可能被意外截断的问题。
- 开放了 PR #4373，持续优化记忆合并（Consolidation）过程中的频道上下文保留。

**可观测性改进**
- 合并了 PR #4385，在模型 Fallback 发生前，先将主模型的报错信息记录到日志中，便于开发者精准定位模型调用失败原因。

## 4. 社区热点

- **No.1 热度: 项目工作区读写不对称 (Issue #4374)**
  - **链接**: [HKUDS/nanobot Issue #4374](https://github.com/HKUDS/nanobot/issues/4374)
  - **分析**: 这是过去一天社区反馈中最具技术质量的问题。用户精准指出了 WebUI 项目工作区（Project Workspace）刚上线后的逻辑缺陷：Agent 在每轮交互中从正确的项目根目录读取 `SOUL.md`，但写入时却落到了默认工作区。这直接导致了单项目下 Agent 状态写入的失效。该 Bug 触及了项目工作区这一核心功能的状态一致性，是当前高级用户群体最看重的待决问题。

- **No. 2 关注: Git 安全策略误杀 (Issue #4375)**
  - **链接**: [HKUDS/nanobot Issue #4375](https://github.com/HKUDS/nanobot/issues/4375)
  - **分析**: 社区在发现 `guard_command` 的路径解析漏洞后迅速上报，并且维护团队在 **24 小时**内即完成了 PR #4380 的合并修复，形成了完美的反馈闭环。这体现了项目极高的维护效率和社区响应速度。

- **No. 3 需求: 多实例与多租户 (Issues #4390 / #936)**
  - **链接**: [HKUDS/nanobot Issue #4390](https://github.com/HKUDS/nanobot/issues/4390) / [HKUDS/nanobot Issue #936](https://github.com/HKUDS/nanobot/issues/936)
  - **分析**: 多个 Issue 围绕 “Multi-*” 展开。Issue #936 (多租户网关) 代表了企业级用户对资源池化的需求，而 Issue #4390 (为普通人设计的多实例) 则代表了个人用户对简化配置管理的期待。这表明随着用户基数的增长，项目的部署和运维友好度正成为下一波社区共识的重点。

## 5. Bug 与稳定性
| 严重程度 | Bug 描述 | Issue/PR | 状态 | 处理进度 |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | MCP `streamableHttp` 服务端重连时 asyncio 任务状态冲突导致进程崩溃 | PR #4303 | **OPEN** | 已有 Fix PR 待评审，建议优先处理 |
| **High** | Git 命令在 Workspace 子目录被安全策略禁止 | #4375 | **已修复** | 已被 PR #4380 合并修复 |
| **High** | 系统代理 (`HTTP_PROXY`) 导致本地 Ollama/LLM 服务完全不可用 | PR #4367 | **已修复** | 已被 PR #4367 合并修复 |
| **High** | 合并分支后 `session_key` 未定义导致 Agent 启动崩溃 | #4322 | **已修复** | 已确认修复并关闭 |
| **High** | Anthropic 因工具 ID 格式问题返回 400 错误 | PR #4356 | **已修复** | 已被 PR #4356 合并修复 |
| **Medium** | iOS Safari 点击 WebUI 输入框触发页面放大导致 UI 变形 | #4388 | **待解决** | 暂无 Fix PR |
| **Medium** | 飞书 WebSocket 卡片渲染结果为空 | PR #4342 | **OPEN** | 已有 Fix PR 待评审 |
| **Low** | 记忆合并时可能丢失频道消息上下文 | PR #4373 | **OPEN** | 已有 Fix PR 待评审 |

## 6. 功能请求与路线图信号

- **高概率纳入下一个版本**:
  - **可配置的工具结果微压缩 (PR #4392)**: 社区贡献者已提交完整的 PR，允许用户在配置文件中通过 `microcompactToolResults` 字段关闭或调整工具结果的压缩逻辑，尤其利于对缓存敏感的高频 Agent 部署场景。此功能已在审查中，大概率会合入。
  - **Fallback 模型上下文窗口感知 (Issue #4389)**: 用户提出了一个极具工程价值的功能：当 Fallback 模型上下文窗口小于主模型时，系统应自动截断 Prompt 以避免超出限制。这直接影响高可用 Agent 服务的故障转移成功率。

- **路线图重要信号**:
  - **多实例配置简化**: Issues #4390 和 #936 同时指向了多实例/多租户管理的痛点。该方向的呼声增多，暗示项目可能需要从 CLI 层面或 WebUI 层面提供一个更集中的管理后台。
  - **浅层交互优化**: Issue #4376（用户友好型向导）与 #4390（多实例对普通人友好）表明，社区开始从追求功能丰富转向追求易于上手。这也是项目走向大众化的重要标志。

## 7. 用户反馈摘要

- **核心矛盾：功能完整性与用户体验的平衡**：用户 `chengyongru` 指出 `nanobot onboard --wizard` 目前“假设你懂很多技术细节”，对非技术用户不友好。同时，`bukit-kronik` 在 `#4390` 中表示阅读了多实例配置文档后依然觉得复杂。这说明项目的功能参数暴露度较高，配置新用户引导（Onboarding）是提升留存率的关键。
- **深耕的期待：项目工作区功能**：用户 `maximilize` 对 #4007 合并后引入的项目工作区功能进行了深度测试，并清晰指出了读写不对称的架构 Bug。这表明高端用户社群正在积极推动项目核心功能的成熟度。
- **移动端体验的持续阵痛**：用户 `zpljd258` 报告 iOS Safari 的输入框放大问题“在最新代码已包含移动端 UI 修复的情况下”依然存在。这提示维护组，WebUI 的移动端适配可能需要更深入的工程重构，而非简单的样式调整。
- **社区热情高涨**：从 #4375 到关闭的 24 小时闭环来看，社区不仅擅长发现 Bug，维护者也展现出了极高的修复热情，整体社群生态非常健康。

## 8. 待处理积压

- **Issue #936 - 多租户网关**（自 2 月 21 日起超过 4 个月未获官方回复）
  请求增加一个支持管理多个 Agent 的网关实例以降低资源开销。虽然该功能涉及架构变动，但建议项目维护者给出明确 roadmap 信号（如 Planned / On Hold / Not Planned）以避免社区高期待落空。
  - **链接**: [HKUDS/nanobot Issue #936](https://github.com/HKUDS/nanobot/issues/936)

- **PR #4303 - MCP 重连崩溃修复**（OPEN 已 7 天，严重性 Critical）
  该 PR 解决了 MCP 服务端在 `streamableHttp` 会话终止并重连时，因异步作用域问题导致进程崩溃的问题。作为 Agent 扩展能力的关键组件，此 Bug 的阻塞性极高，强烈建议维护团队优先安排评审。
  - **链接**: [HKUDS/nanobot PR #4303](https://github.com/HKUDS/nanobot/pull/4303)

- **PR #4342 - 飞书 WebSocket 卡片渲染修复**（OPEN 已 4 天）
  飞书通道的用户目前可能因该 Bug 无法看到卡片内容。该 PR 已提供明确的修复方案，等待合并。
  - **链接**: [HKUDS/nanobot PR #4342](https://github.com/HKUDS/nanobot/pull/4342)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是根据提供的 Hermes Agent GitHub 数据生成的 2026-06-18 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-18

## 1. 今日速览
过去24小时内，Hermes Agent 斩获了极高的社区活跃度（50条Issue更新 + 50条PR提交），项目处于高速迭代与密集缺陷反馈并行的阶段。A2A 智能体互联协议与纯客户端桌面模式成为社区呼声最高的两大诉求。稳定性方面，Anthropic OAuth 认证断裂与 Vision 备用链路静默失效两大P1级Bug出现，但核心开发组响应迅速，已在当日提交了对应的高优修复PR。整体来看，项目生态扩张迅猛，但跨平台稳定性和核心安全性面临“成长的烦恼”。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
- **重要合入:**
  - **命令白名单通配符支持 (#43051)**: 合入 `fix(approval): honor glob command allowlist entries` 修复，用户现可使用 `podman *` 等 shell 风格通配符进行命令授权，提升了安全模型与用户体验的平衡。
  - **Desktop 构建路径修复 (#48084)**: 修复了 `electronDist` 路径错配导致的构建重复失败问题。
  - **gh CLI 认证修复 (#48149)**: 修复了特定 session 上下文中 GITHUB_TOKEN 传递异常导致的 401 错误。

- **关键功能/修复 PR 推进:**
  - **Anthropic OAuth 断裂修复 (#48177)**: 针对 Pro/Max/Team OAuth 请求被 HTTP 400 拒绝的问题，社区贡献者立即提交了修复 PR，添加了必要的 Claude Code 计费归属系统块。
  - **Linux Computer Use 后端 (#48180)**: 新增首个针对 Linux 平台的计算机操控工具后端，扩展了 Hermes 对非 macOS/Windows 环境的覆盖。
  - **OTLP 可观测性插件 (#48184)**: 提交 OpenTelemetry (OTLP) 导出器，标志着项目正式向企业级观测性集成迈进。
  - **macOS 浏览器工具发现 (#48185)**: 修复了浏览器可用性检测逻辑，确保能识别 `/Applications` 下的 macOS 应用包版 Chrome/Chromium。

## 4. 社区热点
- **🔥 最高关注度：A2A 智能体互联协议支持 (#514)**
  - [Issue #514](NousResearch/hermes-agent Issue #514) | 22评论 | 18👍
  - **分析**: 社区压倒性地期望 Hermes 集成 Google 的 A2A 协议，以实现跨智能体系统的发现与互操作。用户不满足于单智能体，开始强烈需求构建“智能体联邦”，这是未来生态建设的绝对核心。

- **🔥 高度共鸣：Desktop 纯客户端安装模式 (#38602)**
  - [Issue #38602](NousResearch/hermes-agent Issue #38602) | 6评论 | 18👍
  - **分析**: 大量用户希望将 Hermes Desktop 降级为“薄客户端”连接远端服务，而非在本地强制自举运行时。这是企业级管控与个人轻量化使用的共同刚需。

- **💡 新提议：Session ↔ Workspace 上下文绑定 (#48190)**
  - [Issue #48190](NousResearch/hermes-agent Issue #48190)
  - **分析**: 用户在会话管理中要求绑定工作目录和当前 Git 分支，以实现上下文恢复。这反映了开发场景下的专业需求，如果实施将大幅提升开发者体验。

## 5. Bug 与稳定性
- **🟥 P1 严重级**
  - **Anthropic Pro/Max/Team OAuth 请求被拒 (#48176)**: 第三方应用使用计划额度时返回 HTTP 400，支付链路断裂。**当日已有修复 PR (#48177)**。
  - **Vision fallback_chain 静默失效 (#27555)**: `_resolve_single_provider` 函数参数命名错误导致视觉备用链路完全不可用。由于异常被静默吞掉，极难排查。**此 Bug 已滞留超过一个月，严重影响依赖视觉能力的用户。**

- **🟧 P2 高危级**
  - **安全漏洞：禁用 Memory 工具集可被绕过 (#48181)**: 晚期 memory-provider 工具注入可绕过 `disabled` 策略过滤，这是一个严重的设计级安全缺陷。
  - **Desktop 构建反复失败 (#47917)**: 更新代码后 Electron 缓存被清除，构建再次失败，属于典型的回归问题，严重阻塞桌面端开发者。
  - **Windows 更新“访问被拒” (#48100)**: 自动更新时无法替换 `pythonw.exe`（权限/文件锁定），安装体验差。
  - **Windows 10 安装器 NPM 阶段失败 (#46260)**: install 脚本在 `desktop` 阶段因 npm install 退出码 1 而中断。
  - **网关 GUI 启动按钮失效 (#48167)**: 桌面应用和 Web UI 的 Gateway 启动按钮点击无反应，但 CLI 命令 `hermes gateway run` 工作正常。
  - **中文 IME 输入回显延迟 (#48161)**: 在 Windows 上使用中文输入法时，确认选字后必须额外按一次键才能显示。
  - **纯文本网关误吞 Markdown (#48150)**: `strip_markdown` 辅助函数在处理纯文本网关（SMS、iMessage等）时误删了星号和列表符号。

- **🟨 P3 其他**
  - **macOS Composer 长对话卡顿 (#40692)**: 超过30轮对话后输入延迟严重。
  - **自定义端点硬校验失败 (#47006)**: Onboarding 向导要求 `GET /v1/models` 返回非空响应，阻止了不暴露该接口的兼容端点的配置。

## 6. 功能请求与路线图信号
- **预计近期合入：**
  - **Linux Computer Use 后端 (#48180)**、**macOS 浏览器工具修复 (#48185)**、**系统托盘支持 (#48163)** 等均有完成度极高的对应 PR，大概率进入下个小版本。
- **路线图指向：**
  - **智能体联邦**：《A2A 协议》(#514) 的需求热度确立了“多智能体协作”作为未来生态的绝对重心。
  - **企业就绪**：**OTLP 可观测性插件 (#48184)** 和 **LUMEN 二进制 MCP 协议 (#47740)** 的提交，表明项目正致力于高负载部署和标准化监控。
  - **MCP 生态深化**：**LUMEN 协议**及**多项新 Skills (#47576)** 的 Draft PR 显示了 MCP 工具生态的持续茁壮。

## 7. 用户反馈摘要
- **痛点与挫折：**
  - **Windows 体验分化严重**：从安装器崩溃（#46260）、更新权限拒绝（#48100）、中文I/E输入问题（#48161）到路径问题，Windows 用户的使用门槛明显高于 macOS。
  - **Agent 行为不可控**：Agent 在无关任务中修改自身系统提示词（#32497），引发用户对安全边界的担忧。
  - **OAuth 高门槛**：Anthropic 用户因计费头缺失完全无法使用，障碍极大。
- **期望与诉求：**
  - **即插即用的配置**：用户希望大幅降低自定义端点和网关的配置门槛（#47006, #48175）。
  - **稳定的核心体验**：多次回归的构建 Bug（#47917）让社区对桌面端的自动化测试回归保护产生了质疑。

## 8. 待处理积压
- **👑 #514 A2A Protocol Support**（创建于3月6日，3个月未分配里程碑，大量用户期待官方设计文档）。
- **⚠️ #27555 Vision Fallback Silent Broken (P1)**（滞留超一个月，影响所有视觉任务依赖链）。**呼吁维护者重点关注。**
- **🧹 #8359 Docs out-of-sync**（自4月起的自动化报告，文档与代码多处脱节，影响新手上手）。
- **🔧 #32497 Unintentional Self-Modification (P2)**（涉及AI行为对齐的核心安全风险，复现场景清晰但久未定位）。
- **🔧 #40692 macOS Composer Lag (P3)**（重度用户日常效率杀手，改善后能显著提升Desktop端好评率）。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 (2026-06-18)

## 📊 数据概览

| 指标 | 过去24小时 |
|---|---|
| Issues 更新数 | 4（新开/活跃: 2，已关闭: 2） |
| PR 更新数 | 10（待合并: 4，已合并/关闭: 6） |
| 版本发布 | 0 |

---

## 1. 今日速览

昨日是 PicoClaw 安全性与兼容性双双显著提升的一天。**两起高危事件在一日之内闭环**：一个严重的 OneBot SSRF 安全漏洞（[#3070](https://github.com/sipeed/picoclaw/issues/3070)）从披露到修复 PR（[#3140](https://github.com/sipeed/picoclaw/pull/3140)）合并仅用数小时；Gemini 3.5 Flash 模型不兼容导致工具流全崩的 Bug（[#3111](https://github.com/sipeed/picoclaw/issues/3111)）也通过 [#3136](https://github.com/sipeed/picoclaw/pull/3136) 解决。此外，**NEAR AI Cloud 服务商支持**（[#2917](https://github.com/sipeed/picoclaw/pull/2917)）成功合入，搜狗搜索兼容性修复（[#3139](https://github.com/sipeed/picoclaw/pull/3139)）和会话历史修复（[#2990](https://github.com/sipeed/picoclaw/pull/2990)）均已完成合并。项目活跃度非常高，开发者对关键问题的响应速度值得肯定。尽管 `vodozemac` 替换等高优先级积压问题仍悬而未决，但项目整体健康度在这 24 小时内显著回升。

## 2. 版本发布

无已发布的新版本。

尽管没有正式打 Tag，但项目积累了多项重要修复及功能增量。预计待 DeltaChat 网关（[#3063](https://github.com/sipeed/picoclaw/pull/3063)）及 Spawn 消息重复修复（[#3142](https://github.com/sipeed/picoclaw/pull/3142)）等积压 PR 合并后，近期可能迎来一个 Patch 或小版本发布。

## 3. 项目进展

过去 24 小时合并/关闭了 6 个 PR，项目在安全防御、模型兼容性与用户体验上均有突破。

#### 🔒 安全与集成
- **[OneBot SSRF 漏洞修复]** ([PR #3140](https://github.com/sipeed/picoclaw/pull/3140), 已合并) — 作者 lc6464 将已有的 HTTP 地址守卫逻辑移植到 OneBot 媒体抓取链路上，彻底封堵了攻击者利用恶意 URL 让 PicoClaw 访问内网/元数据端点的隐患。修复了 Issue [#3070](https://github.com/sipeed/picoclaw/issues/3070)。
- **[搜狗搜索兼容性]** ([PR #3139](https://github.com/sipeed/picoclaw/pull/3139), 已合并) — 作者 SiYue-ZO 发现搜狗 WAP 页面改版（引号变化、class 变更）导致搜索解析失败，已及时适配新的 HTML 结构。

#### 🤖 模型与功能
- **[修复 Gemini 3.5 Flash 报错]** ([PR #3136](https://github.com/sipeed/picoclaw/pull/3136), 已合并) — 修复了当使用 `gemini-3.5-flash` 时 Google API 返回 400 的问题。根因在于新模型要求 tool call 请求体中同时包含 `thought_signature`（snake_case）字段。
- **[新增 NEAR AI Cloud 提供商]** ([PR #2917](https://github.com/sipeed/picoclaw/pull/2917), 已合并) — 正式支持 NEAR AI Cloud 作为 OpenAI 兼容服务商，内置 TEE 功能模型推荐与模型列表拉取接口。

#### 🖥️ 用户体验修复
- **[Web UI 会话历史完整展示]** ([PR #2990](https://github.com/sipeed/picoclaw/pull/2990), 已合并) — 修复了用户只能看到最后一条用户消息的严重视觉 Bug，历史会话完整读回。
- **[添加功能增强]** ([PR #3138](https://github.com/sipeed/picoclaw/pull/3138), 已合并) — 合并了一个功能特性（리뷰기능 추가）。

## 4. 社区热点

#### 🔥 [#3088: use vodozemac instead of libolm](https://github.com/sipeed/picoclaw/issues/3088)
- **Priority: high / help wanted** | 👍 2 | 评论 1
- **诉求分析**：用户 **pbsds** 以专业视角提出替换 libolm 为官方后继库 vodozemac。这不仅是单纯的功能请求，更是**安全技术债清退**诉求。libolm 已停止维护，继续使用将面临累积的 CVE 风险。该 Issue 获得社区认可，但缺少对应的实现 PR，是项目近期最受关注的发展方向。

#### 📢 [#3070: OneBot SSRF 安全漏洞报告](https://github.com/sipeed/picoclaw/issues/3070)
- **评论 1**，**状态：已闭环**
- **争议点**：该 Issue 由 **YLChen-007** 负责任披露，详细分析了攻击者如何通过 `message[].data.url` 欺骗 PicoClaw 访问 `169.254.169.254` 等元数据端点。社区对漏洞严重性的讨论迅速转化为维护者的即刻行动，是一起典型的高效安全协作案例。

#### ⚡ [#3111: Gemini 3.5 Flash 工具执行失败](https://github.com/sipeed/picoclaw/issues/3111)
- **用户 Giordano10** 报告，**状态：已关闭**
- **信号解读**：这是“前沿用户最先受伤害”的典型场景。用户反馈 `gemini-3.5-flash` 新增了 Agentic Reasoning 要求（需要 `thought_signature`），而本地却正常执行。暴露了后端 API 适配对上游改动的滞后性。好在修复 PR [#3136](https://github.com/sipeed/picoclaw/pull/3136) 在一天内合入，缓解了社区焦虑。

## 5. Bug 与稳定性

昨日 Bug 修复力度极大，**两处严重级别 Bug 全部修复闭合**，项目稳定性得到根本性加固。

| 严重程度 | 描述 | Issue / PR | 状态 |
|---|---|---|---|
| 🔴 **严重（安全）** | OneBot SSRF 漏洞，攻击者可任意强制 PicoClaw 发起内网请求 | [#3070](https://github.com/sipeed/picoclaw/issues/3070) | **已关闭**（[#3140](https://github.com/sipeed/picoclaw/pull/3140) 已合并） |
| 🔴 **严重（功能）** | Gemini 3.5 Flash 执行 Tool/Skill 抛出 `400 Bad Request` | [#3111](https://github.com/sipeed/picoclaw/issues/3111) | **已关闭**（[#3136](https://github.com/sipeed/picoclaw/pull/3136) 已合并） |
| 🟡 **中（数据）** | Spawn 子智能体完成时 `ForUser` 段未清理，产生重复消息 | [#3142](https://github.com/sipeed/picoclaw/pull/3142) | **待合并（开放中）** |
| 🟡 **中（UI）** | Web UI 无法加载完整历史会话（只显示最后一条） | parent: [#2796](https://github.com/sipeed/picoclaw/issues/2796) | **已关闭**（[#2990](https://github.com/sipeed/picoclaw/pull/2990) 已合并） |
| 🟡 **中（集成）** | 搜狗搜索结果页 HTML 结构变动导致解析完全失效 | [#3139](https://github.com/sipeed/picoclaw/pull/3139) | **已合并** |
| 🔵 **低（质量）** | Brave 搜索空结果无日志，难以诊断 | [#3141](https://github.com/sipeed/picoclaw/pull/3141) | **待合并（开放中）** |
| 🔵 **低（健壮性）** | `skills_install` 中 `version`/`force` 类型断言缺 `ok` 校验 | [#3092](https://github.com/sipeed/picoclaw/pull/3092) | **待合并（开放中）** |

## 6. 功能请求与路线图信号

#### 🎯 可能纳入下个版本
- **[vodozemac 替换 libolm]** ([#3088](https://github.com/sipeed/picoclaw/issues/3088)) — 高优先级，标记为 help wanted。目前没有对应的实现 PR，但如果维护者接受此提案，这将是一个**架构级别的安全与现代化重构**，预计拆包量较大。
- **[DeltaChat 网关实现]** ([#3063](https://github.com/sipeed/picoclaw/pull/3063)) — 作者 **trufae** 已提交完整代码，**当前最有机会合入的大功能**。若合并，意味着 PicoClaw 正式接入 DeltaChat 协议，大幅扩展消息触达范围。
- **[NEAR AI Cloud 已合并]** ([#2917](https://github.com/sipeed/picoclaw/pull/2917)) — 标志着项目对 TEE 友好型 AI 计算服务的支持拉开序幕，可作为评估后续类似提供商入库的模板。

#### 🔭 远期方向
- **去中心化网关（SimpleX / Tox）** ([#3093](https://github.com/sipeed/picoclaw/issues/3093)) — 作者 Damian-o2 的呼声。当前停留在功能请求阶段，但叠加 DeltaChat 贡献，社区对**去中心化通信协议**的渴望正在逐渐形成路线图驱动力。

## 7. 用户反馈摘要

#### 用户痛点与优秀反馈
1. **Giordano10**（Gemini 3.5 Flash 报错）：明确指出“本地脚本执行成功，但后端 schema 不兼容”。暴露了测试环境与真实 API 的差异——这是使用开源 LLM 网关项目时的典型但极具价值的 Bug 报告。
2. **YLChen-007**（SSRF 漏洞）：提交了极其详尽的安全报告，细节包含攻击向量与完整的复现方式。此类“白帽式”反馈是开源项目最宝贵的资产，直接推动了 PicoClaw OneBot 安全模型的完善。
3. **pbsds**（vodozemac 替换）：不仅提出诉求，还给出了架构建议——“make libolm optional at compile time/is a drop-in replacement”。这是**资深 Rust 社区开发者**的视角，提示项目团队需尽快在架构上解耦遗留依赖。
4. **Damian-o2**（Need SimpleX or Tox）：简短但指向明确。反映出部分用户将 PicoClaw 视为个人隐私通信中轴，对端到端加密赛道有刚性需求。

## 8. 待处理积压（维护者关注）

以下问题/PR 已在一段时间内缺乏有效推进，需维护团队关注以避免社区参与感下降：

#### 🚩 高优先级积压
- **[#3088] use vodozemac instead of libolm** — 创建于 2026-06-09，已标记为 high priority。当前无关联 PR。PicoClaw 作为 AI Agent 框架，依赖 unmaintained 的密码学库是长期隐患。建议维护者明确表态（规划版本/欢迎贡献/搁置原因），否则社区可能重复开类似的 Issue。
  [🔗 直达](https://github.com/sipeed/picoclaw/issues/3088)

#### 🚩 待审 PR 积压
- **[#3063] feat: add deltachat gateway** — 创建于 2026-06-08，已超出 10 天，一个功能较完整的网关 PR，一旦 Review 过久，与主干的 merge 冲突成本会急剧上升。若不希望合入，也应尽快关闭并给出理由。
  [🔗 直达](https://github.com/sipeed/picoclaw/pull/3063)

- **[#3092] fix(skills_install): add ok checks** — 创建于 2026-06-10，已标记为 stale。虽然改动极小，但涉及 SKill 安装这一用户高频操作的类型安全性。此类微修复长期搁置容易消磨新贡献者的积极性。
  [🔗 直达](https://github.com/sipeed/picoclaw/pull/3092)

---

*报告生成时间：2026-06-18 | 项目：sipeed/picoclaw*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 — 2026-06-18

---

## 1. 今日速览

过去 24 小时 NanoClaw 项目极为活跃：累计产生 **20 条 PR**（含 3 条已合并/关闭）和 **5 条 Issue 更新**，并发布了 **2 个包含破坏性变更的版本**（v2.1.0 / v2.1.17）。一个严重级别的消息传递停滞 bug（#2796）在当天被发现并得到修复，同时多个安全补丁与文档改进被提交。整体看，项目正处于快速迭代期，社区贡献踊跃（尤其是 `specterslient95-lgtm` 系列文档修正和 `sturdy4days` 的稳定性/安全修复），但待合并 PR 积压较多（17 条），维护者需要优先审查安全类合并请求。

---

## 2. 版本发布

### v2.1.17（Rollup 发布）
- **范围**：从 v2.1.1 至 v2.1.17 的所有 `package.json` 升级。
- **破坏性变更**：**`@onecli-sh/sdk` 从 0.5.0 升至 2.2.1**，此版本要求 OneCLI server 必须支持 `/v1` API。旧版 server 会 404 所有 SDK 调用。
- **迁移注意**：
  - 必须将 OneCLI gateway / 服务端升级至兼容 `/v1` 的版本。
  - 官方 gateway 和 CLI 版本已锁定，请参考发行注记同步升级。

### v2.1.0（Rollup 发布）
- **范围**：从 v2.0.65 至 v2.1.0 的所有 `package.json` 升级。
- **破坏性变更**：**启动时新增升级标记要求**。主机会拒绝启动，除非 `data/upgrade-state.json` 中记录本次安装已通过合规升级路径到达当前版本。
- **迁移注意**：
  - 对于通过不可变镜像部署的托管集群，新版 v2.1.17 已提供环境变量 `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` 绕过该检查（见 PR #2780），建议立即更新至 v2.1.17 并设置该变量。
  - 普通升级路径请确保 `bash nanoclaw.sh` 完整执行，该脚本会自动生成所需的升级状态文件。

---

## 3. 项目进展（已合并/关闭的重要 PR）

### Bug 修复
- **#2797 — fix(delivery): 隔离 per-session 失败，防止单一会话阻塞全局消息投递**  
  关闭对应 issue #2796。核心贡献：`pollActive`/`pollSweep` 循环从单 `try/catch` 改为每个 session 独立捕获异常，`deliverSessionMessages` 不再向外抛出错误。**从根本上消除了一个不健康 session 导致整个守护进程投递停滞的问题。**  
  GitHub: nanocoai/nanoclaw PR #2797

- **#2794 — fix(providers): 恢复托管集群的 env-var 网关认证**  
  修复 v2.1.17 导致的回归：托管 VM 映像中的 agent 无法认证 LLM（401 `No credentials config`）。还原了对环境变量 `ANTHROPIC_API_KEY` 的支持，确保不可变部署正常工作。  
  GitHub: nanocoai/nanoclaw PR #2794

### 功能 / 兼容性
- **#2780 — feat(upgrade-state): 为启动检查提供环境变量 opt-out**  
  配合 v2.1.0 破坏性变更，允许托管集群通过 `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` 跳过升级标记检查，避免无法启动。该 PR 已合入 v2.1.17。  
  GitHub: nanocoai/nanoclaw PR #2780

**小结**：今日项目在**稳定性（消息投递健壮性）**、**安全边界（后续 PR 待合）**和**托管部署兼容性**上均有明显推进。同时，三个待合并的社区 PR（#2792 #2790 #2788）直接针对用户上报的文档/体验问题，修复路径清晰。

---

## 4. 社区热点

### 最受关注的问题 / PR 组合
- **#2796 / #2797 —— 消息投递停滞**  
  用户 `mashkovtsevlx` 报告了一个极为严重的生产问题：任何 session 出站数据库短暂不可读将导致所有 agent 的消息投递在重启前完全停止。该 issue 在一天内获得修复并合并，体现了项目对核心稳定性反馈的高优先级响应。  
  GitHub: nanocoai/nanoclaw Issue #2796 | PR #2797

### 高频贡献者
- **specterslient95-lgtm**：今日提交了 **4 条 Issue**（#2791 #2789 #2787 #2785）均为文档/SKILL 描述问题，并随后提交了 **4 条修复 PR**（#2792 #2790 #2788 #2786）。反映出用户对项目文档质量和上手引导的重视，社区以“发现问题 → 贡献修复”的方式快速改善。
- **sturdy4days**：集中提交了 **5 条修复 PR**（#2804 #2803 #2802 #2801 #2800）及一条增强 #2750，覆盖 CLI 崩溃、响应超时、JSON 解析安全等，展现了较强的技术深度。

### 讨论分析
目前 Issue 评论数偏少（大多为 1 条），可能是维护者尚未大规模介入讨论，但 PR 的快速提交表明用户与贡献者之间已形成基于代码的协作模式。缺乏长线讨论说明社区更倾向于直接提 PR 而非争论，整体氛围务实。

---

## 5. Bug 与稳定性

按严重程度排序，标注修复状态。

| 严重程度 | 问题 | 影响 | 修复状态 |
|----------|------|------|----------|
| **严重** | **#2796 — 单会话异常阻塞全局投递** | 一个 `outbound.db` 读失败的 session 会导致所有 agent 消息停止投递，直至 daemon 重启。 | ✅ 已修复 & 已合并（PR #2797） |
| **严重** | **#2799 — send_file 任意文件读取（CVE-2026-29611）** | 被注入或受损 agent 可读取容器内任意文件（凭证、挂载数据等），并携带至出站消息。 | 📌 PR #2799 已提交待合并 |
| **严重** | **#2800 — `ncl groups create` 路径遍历（CWE-22）** | `--folder ../../etc` 可越界写入 `GROUPS_DIR`，绕过文件夹合法性验证。 | 📌 PR #2800 已提交待合并 |
| 中 | **#2804 — `ncl messaging-groups create` 总是抛出 NOT NULL 错误** | CLI 创建消息组功能完全不可用。 | 📌 PR #2804 已提交待合并 |
| 中 | **#2802 — `ncl socket` 无请求超时与响应大小限制** | 服务端不响应时 Promise 永远挂起；响应无边界时内存无限增长。 | 📌 PR #2802 已提交待合并 |
| 中 | **#2801 — `safeParseContent` 对非对象 JSON 返回非对象值** | 调用者期望 `.text`/`.sender` 属性，遇到原始值（如 `"5"`）返回 undefined。 | 📌 PR #2801 已提交待合并 |
| 低 | **#2791 — install-imessage 技能重定向时缺少 `mkdir`** | 新检出目录缺少 `src/channels/` 时命令失败。 | 📌 PR #2792 已提交待合并 |
| 低 | **#2789 — setup 技能仅 10 行，无具体步骤** | 用户只看到 `bash nanoclaw.sh`，缺乏故障排查指引。 | 📌 PR #2790 已提交待合并 |
| 低 | **#2787 — init-onecli 端口 10254 仅出现在故障排查末尾** | 用户在前面部分完全未获知默认端口。 | 📌 PR #2788 已提交待合并 |
| 低 | **#2785 — migrate-nanoclaw 技能 H1 标题“Context”过于泛泛** | 不符合技能本身主题，影响可发现性。 | 📌 PR #2786 已提交待合并 |

**注**：多个高严重性安全修复（#2799 #2800）已处于待合并状态，建议维护者尽快审查发布热修复版本。

---

## 6. 功能请求与路线图信号

| 功能 | 说明 | 相关 PR/Issue | 引入时间 |
|------|------|---------------|----------|
| **Agent-to-Agent 每消息审批策略** | 为现有 agent 连接增加可选的双向 `require-approval` 门控，消息被暂存并由接收方审批后释放。无策略时保持向后兼容。 | PR #2793 | 2026-06-17 |
| **只读 CLI 仪表盘技能** | 新增 `/add-clidash` 技能，允许用户通过 CLI 快速生成只读仪表盘，无需修改项目核心。 | PR #2795 | 2026-06-17 |
| **Atlas Cloud LLM 后端集成** | 将 Atlas Cloud 添加为文档化的兼容 OpenAI API 的 LLM 后端选项，附带 59 模型支持详情。 | PR #2717 | 2026-06-09 |
| **容器崩溃后 outbound.db 日志恢复** | 解决容器 SIGKILL 后 journal 文件残留、以及热轮询竞态导致的死锁问题，增强 host 只读 DB 句柄的鲁棒性。 | PR #2750 | 2026-06-12 |

**路线图判断**：agent 审批策略（#2793）是一个重要的企业级 feature，可能被纳入 v2.2 主版本。而 CLI 仪表盘和 Atlas Cloud 属社区生态增强，合并优先级可能较低。PR #2750 对生产环境的稳定性至关重要，目前处于开放且未合并状态，值得维护者优先评估。

---

## 7. 用户反馈摘要

从 Issues 及 PR 描述中提炼实际用户痛点与诉求：

1. **“一个会话的故障导致所有代理的消息传递停止，除非重启守护进程”**  
   —— Issue #2796 报告者描述了一个极为严重且隐蔽的生产故障。此问题在今天已被修复，但反映出系统在错误隔离方面存在架构缺陷，用户期望更好的容错机制。

2. **“文档技能缺失前置条件说明”**  
   多位用户（主要来自 `specterslient95-lgtm`）指出：
   - `add-imessage` 技能步骤假定 `src/channels/` 已存在，新用户执行即失败。
   - `init-onecli` 技能在正文中未声明端口 10254，仅在故障排查段意外出现，用户感到困惑。
   - `setup` 技能太短，只指向一个 shell 脚本，没有解释内部阶段和失败恢复方法。
   - `migrate-nanoclaw` 的标题不明确。

   这些反馈表明用户群体正在快速扩大，文档需要从“开发笔记”转型为“面向初学者的完整指南”。好在所有反馈均有对应的修复 PR 提交。

3. **“托管集群认证在 v2.1.17 回归”**  
   Issue 并未单独提交，但 PR #2794 的描述指出 `managed-fleet` 模式下 agent 完全无法工作（401 错误），这个问题由内部用户/团队发现并修复，体现了托管部署用户对稳定集成的依赖。

---

## 8. 待处理积压

### 关键待合并 PR（按优先级排序）
| PR 编号 | 内容 | 提交时间 | 重要性 | 备注 |
|---------|------|----------|--------|------|
| #2799 | 修复 `send_file` 任意文件读取（CVE-2026-29611） | 2026-06-17 | 🔴 安全 | 建议优先合并并发布补丁版本 |
| #2800 | 修复 `ncl groups create` 路径遍历（CWE-22） | 2026-06-17 | 🔴 安全 | 同上 |
| #2802 | 为 `ncl socket` 添加超时与缓冲区上限 | 2026-06-17 | 🟡 稳定 | 防挂起/内存泄露 |
| #2804 | 修复 `messaging-groups create` NOT NULL 崩溃 | 2026-06-17 | 🟡 功能 | CLI 关键路径阻塞 |
| #2750 | 修复容器 kill 后 outbound.db 日志恢复（#2516 #2640） | 2026-06-12 | 🟡 稳定 | 已开放 6 天，生产必要改进 |
| #2717 | 文档添加 Atlas Cloud 作为 LLM 后端 | 2026-06-09 | 🟢 生态 | 较长时间未审核 |

### 长期未合并的重要 Issue
- 暂无长期无人响应的严重 Issue。今日提交的 Issue 均在一日内获得 PR 处理，响应良好。

### 提醒
当前 **17 条 PR 处于开放待合并状态**，其中包含高优先级的稳定性和安全修复。建议维护者安排一次集中审查（patch review day），优先合入 #2799 及 #2800 以发布安全修复版本，随后跟进 #2802、#2804、#2750。

---

**数据源**：nanocoai/nanoclaw · 统计区间 2026-06-17 至 2026-06-18 · 报告生成 2026-06-18

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 NullClaw 项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-18

---

## 1. 今日速览
NullClaw 项目今日无新版本发布，但开发与社区活动保持良性健康运转。两项高质量的 Pull Request 正在等待合并，分别针对长期存在的终端字符 Bug 和核心记忆系统的功能增强，展现了社区贡献者与维护者之间积极的正反馈循环。社区讨论焦点集中在调度器认证故障与 Web UI 文档易用性上，核心 Agent 基础能力的稳定性获得了用户正面肯定。

---

## 2. 版本发布
无

---

## 3. 项目进展
今日项目进展主要体现在两项关键的待合并 Pull Request 上，从“稳定性修复”与“功能演进”两个维度推动项目前进：

- **修复：CLI 终端交互体验**（PR #960）
  社区贡献者 **vernonstinebaker** 提交了对 Issue #865 的修复方案。通过引入一个轻量的、零分配的 POSIX 原生命令行编辑器，该 PR 正确处理了交互式 Agent REPL 中的方向键、历史记录、光标移动及退格键，直接解决了终端无法使用原生键绑定的“垃圾字符”问题。这标志着项目在 CLI 用户体验上迈出了重要一步。

- **功能：记忆（Memory）系统可配置化**（PR #961）
  **valonmulolli** 贡献了一份重要的功能增强，为 `memory` 模块添加了三个 JSON 配置项：
  - `auto_recall`: 允许用户完全跳过记忆召回（FTS5/LIKE 查询）。
  - `recall_limit`: 控制每次注入上下文的记忆条目上限（默认 5）。
  - `max_context_bytes`: 限制记忆上下文所占 Token 长度。
  该 PR 使得用户在处理长上下文模型与时受限于 Context Window 的模型之间，能够更精细地控制 Agent 的记忆行为。

- **项目向前迈进的判断**：这两项 PR 若成功合并，将同时解决“交互体验差”与“记忆控制模糊”两大社区核心痛点，标志着项目正从“基础功能可用”向“细化配置与体验优化”阶段跃进。

---

## 4. 社区热点
今日社区最活跃的讨论集中在以下几个老牌 Issue 上，背后反映了用户对功能完整性与文档易用性的迫切需求：

- **热点 #1：调度器无法使用（无法授权）**（[Issue #915](https://github.com/nullclaw/nullclaw/issues/915)）
  尽管 Agent 的基本推理和工具调用正常，但调度器（Scheduler）在 Telegram 和 CLI 下完全失效，错误表现为“未经授权”。由于该功能涉及自动化任务执行，严重影响依赖定时任务的用户。**至今没有关联的修复 PR**，是当前社区最关注的阻塞性 Bug。

- **热点 #2：用户对 Web UI 配置手册的困惑**（[Issue #861](https://github.com/nullclaw/nullclaw/issues/861)）
  用户直言“无法理解 README 中 70% 的内容”，呼吁用通俗语言解释如何在 headless VPS 上启用 Web UI。这暴露了项目在面向非网络专家用户时的文档鸿沟，合理、清晰的快速上手指南是目前社区呼声最高的文档需求。

---

## 5. Bug 与稳定性
今日按严重程度排列的 Bug 及回归问题如下：

- **[严重] 调度器授权故障**（[Issue #915](https://github.com/nullclaw/nullclaw/issues/915)）
  **状态**：开放中（5月15日至今） | **修复 PR**：无
  **影响**：导致 cron 类定时任务、提醒等自动化功能完全不可用。尽管触发 LLM 请求正常，但调度器在执行时被权限系统拦截。建议维护者优先排查 `scheduler` 模块与 `auth` 模块之间的接口或 token 传递逻辑。

- **[中等] CLI 终端控制字符乱码**（[Issue #865](https://github.com/nullclaw/nullclaw/issues/865)）
  **状态**：开放中 | **修复 PR**：已有 [PR #960](https://github.com/nullclaw/nullclaw/pull/960)
  **影响**：方向键、Home/End 键无法正常工作，严重影响交互式终端的日常使用体验。得益于社区贡献，该问题已有关联修复方案，稳定性风险较低。

---

## 6. 功能请求与路线图信号
结合最新 PR 与讨论热度，以下功能极有可能被纳入下一版本或短期路线图：

- **高信号 / 高完成度（预计即将合并）**：
  - **可配置的记忆召回策略**（[PR #961](https://github.com/nullclaw/nullclaw/pull/961)）：代码实现完整，直接向配置层暴露 `auto_recall`、`recall_limit` 等开关。适合运行在严格 Token 预算（如本地小参数模型）或需要精确控制知识注入频率的用户。
  - **原生终端键绑定**（[PR #960](https://github.com/nullclaw/nullclaw/pull/960)）：修复长期弱点，是提升用户体验的必经之路。

- **需求信号 / 待代码化**：
  - **简化的 Web UI 部署流程**（[Issue #861](https://github.com/nullclaw/nullclaw/issues/861)）：虽然不是纯粹的 Feature Request，但如果项目组希望降低入门门槛，提供一个默认的 localhost 直连脚本或更清晰的隧道指南将是极大的加分项。
  - **调度器多平台兼容与权限透明**（[Issue #915](https://github.com/nullclaw/nullclaw/issues/915)）：修复该 Bug 不仅是修复稳定性，更是完善 Agent 自动化闭环的核心功能。

---

## 7. 用户反馈摘要
从今日更新的 Issues 评论中提炼的用户真实反馈：

- **满意点**：
  - **核心能力扎实**：用户在 #915 中明确指出“**LLM 工作正常，工具调用大部分也没问题**”（The LLM is working fine, and tool calling in nullclaw in general also works mostly fine）。这表明 Agent 的核心推理与函数调用链路的稳定性得到了社区认可。
- **痛点与不满**：
  - **调度器不可用是最大的单一痛点**：用户投入了硬件（RTX 3090）和软件（Ollama + Qwen3）资源，却无法使用 Agent 的定时任务功能，挫败感较强。
  - **文档与真实场景脱节**：README 中的“高级”配置对于新手过于晦涩，用户明确表达了对“非行话”（non-jargon human terms）的需求，认为当前的教程可能预设了用户拥有网络工程背景。
  - **CLI 终端体验糟糕**：连基础的 bash 行编辑功能都无法使用，损害了专业用户对项目的“工业级”印象。

---

## 8. 待处理积压
以下为长期未响应或处于停滞状态的重要事项，提醒维护者重点关注：

1. **[严重] 调度器授权 Bug**（[Issue #915](https://github.com/nullclaw/nullclaw/issues/915)）
   - **状态**：创建于 2026-05-15，已超过 1 个月无修复方案。
   - **建议**：鉴于该 Bug 直接导致核心自动化功能瘫痪，且无关联 PR，建议开发主力优先审查相关认证逻辑，必要时请求用户提供详细的 Ollama 与网络拓扑日志。

2. **[文档] Web UI 配置文档晦涩难懂**（[Issue #861](https://github.com/nullclaw/nullclaw/issues/861)）
   - **状态**：创建于 2026-04-22，缺乏通俗易懂的解答。
   - **建议**：该 Issue 本质上是文档欠缺的信号。建议在 README 中增加一个“零基础快速启用 Web UI”章节，提供针对 headless VPS 的复制粘贴式命令指南。

3. **[修复中] CLI 控制字符问题**（[Issue #865](https://github.com/nullclaw/nullclaw/issues/865)）
   - **状态**：创建于 2026-04-23，虽已有关联 PR（#960），但需要一个维护者进行合并前审查。
   - **建议**：尽快 Code Review PR #960 并合并，以清理积压。

---

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 (2026-06-18)

## 1. 今日速览

过去 24 小时内，项目共更新 **47 条 Issue**（新开/活跃 25 条，关闭 22 条）和 **50 条 Pull Request**（待合并 33 条，已合并/关闭 17 条）。无新版本发布。整体活跃度处于高位，关闭率（Issue 与 PR 合并/关闭比例均超过 45%）表明维护团队响应迅速。修复集中在 **Reborn WebUI 反馈透明度和稳定性**（工具批准流、自动化面板、数据一致性），功能开发侧则有 **Projects 实体堆栈（5 个 PR）**、**技能提取**与 **AWS Bedrock 支持** 等新能力被提出或进入合并。项目健康度良好，正处于由“核心稳定”向“下一代功能”跃迁的关键阶段。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

### 重要合并/关闭的 Pull Request

- **#5052 – fix(reborn): live Slack OAuth path structural DM-parity**  
  为实时 Slack OAuth 提供与 triggered 路径一致的 DM 防护，授权 URL 在发送时即严格检验目标是否为个人 DM，合入后有效防止授权泄漏。  
  https://github.com/nearai/ironclaw/pull/5052

- **#5022 / #5000 – output‑aware no‑progress detection (PR2/PR3)**  
  重构 Agent 循环中的“无进度检测”机制：PR2 为每次工具调用输出添加 `ContentDigest`，PR3 利用该摘要判断是否产生实质性进展，避免了长期重复执行时的无效循环。核心稳定性提升。  
  https://github.com/nearai/ironclaw/pull/5022  
  https://github.com/nearai/ironclaw/pull/5000

- **#3708 – chore: release**  
  发布 `ironclaw_common` 0.5.0、`ironclaw_skills` 0.4.0 等多个 crate，包含 API 破坏性变更，为后续开发奠定版本基础。  
  https://github.com/nearai/ironclaw/pull/3708

### 批量 Issue 关闭反映的修复进展

今日关闭的 22 条 Issue 绝大部分为 **Reborn WebUI v2 相关 Bug**，代表性修复包括：

| 问题 | 影响 | 状态 |
|------|------|------|
| #4764 拒绝 shell 后无反馈 | 用户操作无响应 | 已关闭 |
| #4986 自动化因待批准永久阻塞 | 无人值守场景瘫痪 | 已关闭 |
| #4961 “Working”指示器残留 | 误导用户 | 已关闭 |
| #4853 工具活动完成后消失 | 多租户环境认知混乱 | 已关闭 |
| #4762 失败工作流后消息顺序错乱 | 对话历史不一致 | 已关闭 |
| #4793 首次运行锁住扩展/自动化 | 新用户入门困难 | 已关闭 |
| #5004 自动化失败不可追溯 | 排查成本高 | 已关闭 |
| #4988 / #4980 自动化面板空状态 & 可视化 | 易用性不足 | 已关闭 |
| #4974 工具行重复按钮 | UI 混乱 | 已关闭 |

这些修复使 **Reborn 前端体验**和 **自动化可靠性** 大幅提升，项目在“稳定化”方向迈进了扎实一步。

### 新功能堆栈进入 Review

- **Projects 实体**：#5015–#5019（5 个递进 PR）从数据模型、port/门面、前端路由到 WebUI 全部提交，已完成方案设计并进入审查。  
  https://github.com/nearai/ironclaw/pull/5015

- **技能提取**：#5061（新 PR）引入 Hermes 风格自学习功能，可在安全扫描后自动生成并安装技能。  
  https://github.com/nearai/ironclaw/pull/5061

- **AWS Bedrock 支持**：#5059（新 PR）对应 Issue #5058，解决 feature 透传与 Converse schema 问题。  
  https://github.com/nearai/ironclaw/pull/5059

## 4. 社区热点

评论与反应最集中的 Issue：

- **#4761 – Agent stops after repeated tool failures instead of recovering**（3 评论）  
  用户提供完整复现步骤（fetch commits、保存文件），观察到 Agent 在工具连续失败后不再继续，期望内置恢复机制。讨论反映社区对 **Agent 容错能力**的高度关注。  
  https://github.com/nearai/ironclaw/issues/4761

- **#1584 – WeChat channel for IronClaw**（3 评论，+3 👍）  
  WeChat 插件 NPM 包已发布，社区期待 IronClaw 官方跟进适配，信号表明 **渠道扩展** 是用户核心诉求之一。  
  https://github.com/nearai/ironclaw/issues/1584

- **#3026 – Epic: Reborn production wiring and cutover readiness**（3 评论）  
  该生产就绪追踪 Issue 今日关闭，标志着 Reborn 已具备面向生产环境的配置、验证与流量阻断能力，是项目成熟度的重要里程碑。  
  https://github.com/nearai/ironclaw/issues/3026

此外，#5009（Slack OAuth 安全）与 #5058（Bedrock 支持）虽评论较少，但涉及安全与云基础设施，讨论深度高。

## 5. Bug 与稳定性

按严重程度排列今日活跃（OPEN）的关键 Bug，并标注是否已有修复 PR：

| 严重级别 | Issue | 描述 | 创建日 | 关联 PR | 链接 |
|----------|-------|------|--------|---------|------|
| 🔴 安全 CI 阻塞 | #4824 | `cargo-deny` 因新 RUSTSEC 公告失败，阻断所有 PR 合并 | 06-12 | 暂无 | [链接](https://github.com/nearai/ironclaw/issues/4824) |
| 🔴 核心 Agent 行为 | #4761 | 工具多次失败后 Agent 停止恢复，需手动重开对话 | 06-11 | 暂无 | [链接](https://github.com/nearai/ironclaw/issues/4761) |
| 🔴 核心基础设施 | #5058 | Bedrock 在 `ironclaw-reborn` 中不可用，编译 feature 未透传 | 06-18 | #5059 | [链接](https://github.com/nearai/ironclaw/issues/5058) |
| 🔴 核心工作流 | #5060 | GitHub 分析任务进入重复批准循环，无法输出结果 | 06-18 | 暂无 | [链接](https://github.com/nearai/ironclaw/issues/5060) |
| 🟡 功能缺陷 | #5044 | `NEARAI_MODEL=auto` 被 cloud-api 拒收（HTTP 400） | 06-17 | #5043 #5045 | [链接](https://github.com/nearai/ironclaw/issues/5044) |
| 🟡 功能缺陷 | #5007 | Skills 验证错误在填入内容后仍不消失 | 06-17 | 暂无 | [链接](https://github.com/nearai/ironclaw/issues/5007) |
| 🟡 数据一致性 | #3729 | 拒绝的 `tool_install` 刷新后显示成功（安全幻觉） | 05-17 | 暂无 | [链接](https://github.com/nearai/ironclaw/issues/3729) |

其中 #4824（安全）与 #3729（数据错误）遗留时间较长，建议优先处置。

## 6. 功能请求与路线图信号

| 功能 / 请求 | 状态 | 进入下一版本可能性 |
|------------|------|-------------------|
| **Projects 实体**（#5015-5019 栈） | 5 个 PR 全部 OPEN，密集 Review 中 | 极高，已接近完整实现 |
| **技能提取与自我进化**（#5061 PR） | 新提交，社区贡献者发起 | 高，与“Agent 自我进化”路线合拍 |
| **AWS Bedrock 支持**（#5059 PR） | OPEN，对应严重 Bug | 高，一旦修复即可合并 |
| **WeChat 渠道移植 Reborn**（#3582） | OPEN，未见对应 PR | 中低，需社区贡献推动 |
| **Scalable Agent Task Service**（#5036） | 新 Epic，作为 #4878 子任务 | 中，属于工程效率路线图 |
| **Denied activity id 显式化**（#5028） | OPEN，安全增强请求 | 中，属于 #4978 后续 |
| **新建用户引导**（#4793 已关闭） | 已修复 | — |

路线图信号清晰：**Projects 与技能提取**是下一版本的绝对主角；**云模型支持（Bedrock）** 和 **安全深化（OAuth 检查、状态一致性）** 同步推进。

## 7. 用户反馈摘要

从 Issue 描述与复现步骤中可以提炼出真实用户的典型痛点：

- **Agent 行为不可预期**：工具失败后 Agent 静默停止（#4761），拒绝批准后无任何反馈（#4764），删除对话失败且无提示（#4823）——用户希望 Agent 具备“容错 + 透明反馈”能力。
- **自动化可靠性**：周期性任务因等待工具批准而永久阻塞（#4986），失败后无法定位具体是哪个 run 出错（#5004）——用户对无人值守场景的稳定性和可观测性要求迫切。
- **UI 一致性与易用性**：工具活动凭空消失（#4853）、运行历史仅用圆点无法理解（#4988）、空状态无操作引导（#4980）、重复按钮混淆（#4974）——表明 Reborn WebUI 在状态表达和初学友好性上仍有提升空间。
- **数据可信度**：`tool_install` 被拒后刷新显示成功（#3729）引发安全担忧，用户期待状态在生命周期内严格一致。

总体而言，测试者与早期采用者对功能集认可，但强调 **反馈闭环、状态一致性和新用户引导** 需优先打磨。

## 8. 待处理积压

以下重要 Issue / PR 长期未解决或处于停滞，请维护方关注：

- **#4761 – Agent 工具失败不恢复**（06-11，6 天，无 PR）  
  https://github.com/nearai/ironclaw/issues/4761

- **#3729 – tool_install 刷新后状态错误**（05-17，超 1 个月，无 PR）  
  https://github.com/nearai/ironclaw/issues/3729

- **#4824 – cargo-deny 安全公告阻塞 CI**（06-12，影响所有 PR）  
  https://github.com/nearai/ironclaw/issues/4824

- **#3582 – 移植 WeChat 至 Reborn**（05-13，无 PR）  
  https://github.com/nearai/ironclaw/issues/3582

- **#4876 – 依赖批量更新（43 包）**（06-14，open，需安全审核）  
  https://github.com/nearai/ironclaw/pull/4876

- **#5060 – GitHub 分析重复批准循环**（06-18 新开，尚无 PR，QA 阻塞）  
  https://github.com/nearai/ironclaw/issues/5060

- **Projects 栈 PR（#5015–#5019）** 均未合并，若下一版本时间线紧张，建议加速 Review。  
  https://github.com/nearai/ironclaw/pull/5015

---

*生成时间: 2026-06-18 | 基于 GitHub 公开数据*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据 LobsterAI 昨日 GitHub 数据生成的项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-18

## 1. 今日速览

- **开发节奏极快**：昨日共有 **11 个 Pull Request** 被合并或关闭，待合并队列清零，团队交付效能极高。
- **重大版本发布**：发布 v2026.6.15，正式引入 **Computer Use** 与 **实时 ASR 语音输入**，项目向多模态自主智能体方向迈出关键一步。
- **安全警报拉响**：收到 **1 个严重安全漏洞报告**（#2176），涉及自动工件加载导致的任意本地文件读取，是当日最需关注的议题。
- **Cowork 模式成熟度提升**：本次合的大量提交（8+ 个）均围绕 Cowork 模块的稳定性、UI 交互与上下文连续性进行深挖修复。
- **整体活跃度**：极高。核心贡献者 @liuzhq1986 贡献了绝大部分 fix，测试与回归覆盖完善。

## 2. 版本发布

- **版本号**：[LobsterAI 2026.6.15](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.15)（发布于 2026-06-15）
- **核心特性**：
  - **Computer Use**：Agent 获取计算机使用能力，允许大模型通过桌面 GUI 与操作系统进行交互。
  - **实时语音输入（Realtime ASR）**：Cowork 模式新增实时语音输入功能，极大提升人机交互的流畅度。
  - **上下文压缩优化**：改善 Cowork 模式下的上下文连续性，让 Agent 在长对话或任务压缩后能更可靠地继续执行。
- **注意事项**：本次更新无显著的破坏性变更（Breaking Changes）说明，建议所有用户根据需求及时升级以获取新功能及稳定性修复。

## 3. 项目进展

昨日合并/关闭的 11 个 PR 覆盖了多个核心模块，项目在“自主 Agent 交互”与“稳定性”上推进明显。

| 方向 | 关键 PR | 描述 |
|---|---|---|
| **Cowork 交互改进** | [#2173](https://github.com/netease-youdao/LobsterAI/pull/2173) | 用户消息以纯文本渲染，正确保留换行符 |
| | [#2174](https://github.com/netease-youdao/LobsterAI/pull/2174) | 修复滚动到底部的位置计算，确保新消息对齐 |
| | [#2153](https://github.com/netease-youdao/LobsterAI/pull/2153) | 解决同名 Package 模型选择冲突，完善模型选择状态 |
| **任务可靠性** | [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154) | 修复手动停止流式输出后模型元数据丢失的问题 |
| | [#2147](https://github.com/netease-youdao/LobsterAI/pull/2147) | 修复用户快速点击停止时消息被错误发送的启动竞争条件 |
| | [#2145](https://github.com/netease-youdao/LobsterAI/pull/2145) | 新增上下文压缩后的连续性层，提升 Agent 多轮任务续接可靠性 |
| **性能与基础设施** | [#2149](https://github.com/netease-youdao/LobsterAI/pull/2149) | 为 OpenClaw 网关进程设置 V8 堆上限，大幅降低长时多通道 OOM 崩溃率 |
| | [#2144](https://github.com/netease-youdao/LobsterAI/pull/2144) | 更新 Portal 认证域名及降级链接 |
| **项目维护** | [#2175](https://github.com/netease-youdao/LobsterAI/pull/2175) | 优化项目 README 文档 |
| | [#1463](https://github.com/netease-youdao/LobsterAI/pull/1463) | 修复 Agent/Skill/MCP 弹窗中长标题溢出问题（遗留 PR 清扫） |
| | [#2162](https://github.com/netease-youdao/LobsterAI/pull/2162) | 修复合并冲突导致的语音输入取消逻辑受损 |

**项目健康度评估**：代码清理效率极高，所有 Bug 修复均有对应的回归测试覆盖，Cowork 模块的稳定性正在快速接近生产级。

## 4. 社区热点

- **[Issue #2176] 安全漏洞：任意本地文件读取**
  - **链接**：[netease-youdao/LobsterAI Issue #2176](https://github.com/netease-youdao/LobsterAI/issues/2176)
  - **热度**：新开 1 小时即获 1 条评论。虽然互动数量不高，但此为 **Severity 严重的 Security Advisory**，是当日关注度最高、影响面最大的讨论。
  - **诉求分析**：社区安全研究员（YLChen-007）发现 LobsterAI 自动解析 `MEDIA:` 文件引用时，可以直接读取用户本地任意文件。这表明 LobsterAI 的用户数据隔离机制存在薄弱环节，社区期待项目方能迅速响应、分步修复并发布安全公告。

## 5. Bug 与稳定性

按严重程度排列如下：

| 严重度 | 问题描述 | Issue/PR | 修复状态 |
|---|---|---|---|
| **Critical** | 自动工件加载导致的任意本地文件读取 | [#2176](https://github.com/netease-youdao/LobsterAI/issues/2176) | **待响应**。无 Assignee，无 Fix PR |
| **Medium** | 长期运行多通道后 OpenClaw 网关 OOM 崩溃 | [#2149](https://github.com/netease-youdao/LobsterAI/pull/2149) | **已修复**（已合并） |
| **Medium** | 流式输出停止后模型元数据不显示 | [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154) | **已修复**（已合并） |
| **Medium** | 启动阶段快速 Stop 导致消息误发 | [#2147](https://github.com/netease-youdao/LobsterAI/pull/2147) | **已修复**（已合并） |
| **Low** | 语音输入合并冲突导致取消逻辑失效 | [#2162](https://github.com/netease-youdao/LobsterAI/pull/2162) | **已修复**（已合并） |
| **Low** | 长弹窗标题溢出破坏 UI 稳定性 | [#1463](https://github.com/netease-youdao/LobsterAI/pull/1463) | **已修复**（已合并） |
| **Low** | 用户消息文字内换行符被丢弃 | [#2173](https://github.com/netease-youdao/LobsterAI/pull/2173) | **已修复**（已合并） |

## 6. 功能请求与路线图信号

- **Confirmed Roadmap Signals**:
  - **Computer Use (Agent 操控桌面)**：v2026.6.15 的发布标志着该项目正式入局电脑操控 AI Agent 赛道，可以预见未来版本将围绕 Tool Call 与 GUI 追溯做深度优化。
  - **Realtime 交互**：ASR 语音输入的落地表明项目正在从“文字对话”转向“实时多模态交互”。结合 Computer Use，构成了完整的“语音指令+视觉反馈”闭环。
  - **Conversational Continuity (会话连续性)**：[#2145](https://github.com/netease-youdao/LobsterAI/pull/2145) 的合并非常关键。它不是简单的 Bug 修复，而是为 Agent 长期自主任务设计的“上下文压缩后的高速缓存层”。这暗示项目正在认真对待 “Long-lived Agent” 场景，而不仅仅是单轮问答。

- **潜在方向**：安全漏洞 #2176 的暴露可能会迫使项目在短期内加入 **输入审计 / 文件路径沙箱** 机制，成为近期基础设施的重心。

## 7. 用户反馈摘要

从今日的 Issue 和 PR 描述中，可以提炼出以下真实用户痛点与场景：

1. **安全信任危机**：安全研究员报告零点击本地文件泄漏风险。**反馈**：LobsterAI 安全模型需要加强。
2. **中断体验不佳**：用户反映手动停止 AI 回复后，之前的回复内容/元数据丢失（`#2154`），或者在快速点击停止时，消息仍被错误发送（`#2147`）。**反馈**：操作中断的 UI 反馈和底层状态机逻辑需要更细腻地处理。
3. **Visual Polish**：用户报告输入消息换行符丢失（`#2173`）、自定义模型长名称导致界面溢出（`#1463`）。**反馈**：用户对 UI 的期望是两个“自然”的用户输入保持原样。

开发者反馈主要集中在 @liuzhq1986，他在 `#2162` 中特别说明了需要“*resolve voice input merge conflict*”，反映开发团队内部协作合并时需要更仔细的 guard 保护，以防止功能交叉处出现回退。

## 8. 待处理积压

- **紧急（Urgent）**：
  - **[Issue #2176] Security: Arbitrary local file reads**
    - **状态**：OPEN | 无 Assignee | 无社区管理员正式回复
    - **影响面**：严重安全漏洞，可能影响所有依赖自动工件加载的用户。
    - **建议**：项目核心维护者（@btc69m979y-dotcom 或网易有道团队）应尽快标记为 `security` 并分配，至少给出临时缓解措施（Mitigation）或禁用不安全的 feature flag。建议立即开 Hotfix 分支。
    - 链接：[netease-youdao/LobsterAI Issue #2176](https://github.com/netease-youdao/LobsterAI/issues/2176)

- **备注**：当前 Pull Requests 待合并积压：**0**。项目洗代码效率极高，无需警告。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的TinyAGI（TinyClaw）项目数据，为您生成一份结构清晰、客观专业的项目动态日报。

---

### **TinyAGI (TinyClaw) 项目动态日报 | 2026-06-18**

#### **1. 今日速览**

今日项目面临严峻安全挑战，社区活跃度极高但情绪负面。过去24小时内集中爆出3个高危安全漏洞（Issue #282, #283, #284），均由安全研究员报告，涉及未认证的API调用、任意文件读取及响应投毒。目前所有问题均处于待处理状态，尚无修复PR提交。项目整体活跃度因安全事件而骤升，但项目健康度面临重大威胁，维护团队需立即介入响应。

#### **2. 版本发布**

无

#### **3. 项目进展**

今日无任何Pull Requests被合并或关闭。项目核心功能开发进展停滞，安全修复成为当前唯一优先级。此次安全事件的集中曝光，使得项目从功能迭代阶段紧急切换至安全加固阶段，对后续版本路线图可能产生重大影响。

#### **4. 社区热点**

今日社区讨论几乎完全集中在三个新开的安全漏洞议题上，评论区虽冷清（0评论），但议题本身因其严重性已成为绝对焦点。

-   **核心议题**：三个安全漏洞的原始报告。
    -   [#284 [Security] TinyAGI allows unauthenticated API messages to invoke Claude with provider permission checks disabled by default](https://github.com/TinyAGI/tinyagi/issues/284)
    -   [#283 [Security] Unauthenticated `prompt_file` agent configuration allows arbitrary local file disclosure to the model provider](https://github.com/TinyAGI/tinyagi/issues/283)
    -   [#282 [Security] Untrusted `[send_file: ...]` response tags allow arbitrary host file attachment delivery in TinyAGI](https://github.com/TinyAGI/tinyagi/issues/282)

-   **诉求分析**：社区（以安全研究员为代表）的核心诉求已从功能请求转向**安全审计与漏洞修补**。议题提交者YLChen-007显然对项目进行了系统性的安全扫描，其报告内容专业，直指设计缺陷。社区的隐性诉求是希望项目方能迅速确认漏洞、修复并发布安全更新，以保障用户数据和系统安全。

#### **5. Bug 与稳定性**

今日共报告3个安全漏洞，均严重危害系统安全，需优先处理。按严重程度排列如下：

1.  **（危急）[#284] 未认证API绕过权限检查**：允许未经任何身份验证的攻击者通过`POST /api/message`端点，调用配置中的Claude等AI模型，可能导致服务被滥用和数据泄露。**无修复PR**。
2.  **（高危）[#283] 任意本地文件泄露**：允许攻击者通过构造特定的`prompt_file`参数，诱导AI模型读取服务器上的任意敏感文件并输出给攻击者。**无修复PR**。
3.  **（高危）[#282] 响应标签投毒导致任意文件分发**：攻击者可通过控制模型输出内容中的`[send_file: ...]`标签，强制AI系统将服务器上的任意文件作为附件发送给用户。**无修复PR**。

**总结**：这三个漏洞形成了完整的攻击链：从无权限调用 - > 泄露文件 - > 分发恶意文件，对项目及其部署者而言是极高优先级的安全风险。

#### **6. 功能请求与路线图信号**

今日无新的功能请求提交。然而，这三个安全漏洞本质上是对项目架构设计的强烈信号：

-   **安全设计缺失**：项目在设计API接口、权限控制、数据流处理时，缺乏“默认安全” (Secure by Default) 的考量。
-   **输入验证不足**：对用户输入（`prompt_file`, `send_file`标签）和网络请求缺乏严格的过滤、验证和授权。

**对路线图的建议**：下一版本（或紧急补丁）必须将**安全修复**作为唯一目标。建议路线图增加“安全加固”专项，包括但不限于：
-   实现API Key或OAuth2等认证机制。
-   对所有用户可控制的输入进行严格的白名单验证和上下文清理。
-   对模型输出进行后处理过滤，防止标签注入攻击。

#### **7. 用户反馈摘要**

今日无来自普通用户的Issue反馈。现有Issues完全由安全研究员YLChen-007提交，其反馈可被理解为“专业审计员”视角的痛点：

-   **核心痛点**：项目在未做任何安全配置的情况下默认暴露了大量风险接口，这对于任何生产环境部署都是不可接受的。用户将扮演的不是“受益者”，而是“潜在受害者”。
-   **使用场景**：研究员模拟了恶意攻击者利用TinyAGI作为跳板攻击下游（Claude模型）和上游（服务器文件系统）的场景，揭示了项目当前设计存在重大安全隐患。
-   **满意/不满意**：研究员对项目的安全性**明确表示不满意**，并认为此状态是**高风险**的。这也间接反映了普通用户在未知情况下的潜在不满。

#### **8. 待处理积压**

今日无长期未响应Issue。但新产生的3个高危安全Issue已构成最紧急的“待处理积压”。维护团队应立即：

1.  **确认并回复**：在24小时内确认漏洞报告，并向社区通报响应计划。
2.  **分配优先级**：将这3个Issue标记为 `bug` 且 `critical` 优先级，成立专门小组处理。
3.  **发布公告**：如无法立即修复，应发布安全公告，建议所有部署者暂停对外服务或增加外部WAF/API网关进行临时防护。

**链接**：
-   [`#284`](https://github.com/TinyAGI/tinyagi/issues/284) [`#283`](https://github.com/TinyAGI/tinyagi/issues/283) [`#282`](https://github.com/TinyAGI/tinyagi/issues/282)

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报（2026-06-18）

**数据周期**：2026-06-17 00:00 UTC – 2026-06-18 00:00 UTC  
**数据来源**：[moltis-org/moltis](https://github.com/moltis-org/moltis)

---

## 1. 今日速览

- 过去 24 小时项目保持中等活跃度：收到 **2 个新功能请求**（均为 enhancement），**1 个新 PR**（待合并），未发布新版本。
- Issues 互动集中在 TTS 输出格式的灵活配置（#1126，含 3 条讨论），Markdown 导出功能为新的用户呼声（#1131）。
- PR #1130 提出了 WebUI RPC 超时配置，直接关联已存在的问题 #1127，可能进一步提升 Web 客户端的稳定性。
- 未发现 Bug、崩溃或回归相关报告，整体项目健康度良好，社区主要围绕功能增强进行贡献。

---

## 2. 版本发布

本周期内无新版本发布。

---

## 3. 项目进展

- **无 PR 被合并或关闭**，今日并未完成功能里程碑。
- **新增 PR #1130**（`feat: make webui rpc timeout configurable`）由 khimaros 提交，尚处于开放状态。该 PR 允许用户设置 WebUI RPC 的超时时间，修复了 #1127 中可能涉及的连接或等待问题。  
  链接：[PR #1130](https://github.com/moltis-org/moltis/pull/1130)

---

## 4. 社区热点

- **🔥 Issue #1126 – [Feature]: allow to configure the format of tts output**  
  - 作者：khimaros | 评论数：3 | 👍：0  
  - 该 issue 是今日唯一产生讨论的条目。用户希望支持配置 TTS 输出的格式（如语音、语速、语调等），表明语音功能的使用场景正在多样化，社区对输出可定制性有明确需求。  
  链接：[Issue #1126](https://github.com/moltis-org/moltis/issues/1126)

- Issue #1131 虽暂无评论，但其“复制 + 导出为 Markdown”的功能点切入协作记录场景，可能成为后续讨论热点。

---

## 5. Bug 与稳定性

- **无 Bug 或回归问题** 报告。今日所有新 Issue 均为增强性需求（标签 `enhancement`），说明当前版本在用户手中运行稳定。
- 未涉及崩溃、安全漏洞或性能退化问题。

---

## 6. 功能请求与路线图信号

| 特征 | 对应条目 | 状态 | 是否可能纳入下一版本 |
|------|----------|------|----------------------|
| 允许配置 TTS 输出格式 | [#1126](https://github.com/moltis-org/moltis/issues/1126) | 已开放，有讨论 | 较高：用户活跃度高，且已有初步方案 |
| 复制并导出为 Markdown | [#1131](https://github.com/moltis-org/moltis/issues/1131) | 新开，无评论 | 中：属于常见需求，依赖路线图优先级 |
| WebUI RPC 超时可配置 | [#1130 (PR)](https://github.com/moltis-org/moltis/pull/1130) | 待合并 | 很高：直接修复已确认的 issue，预计会合入下个小版本 |

- 值得注意的是，#1130 直接绑定了 #1127，说明维护者已有明确规划。结合 #1126 与 #1131 对输出控制和导出的关注，下一版本可能方向为 **“输出与集成增强”**。

---

## 7. 用户反馈摘要

- **Issue #1126 用户（khimaros）**：在 Preflight Checklist 中强调已搜索过现有请求，属于经过调研的有理有据的需求。使用场景可能是希望 TTS 输出符合特定格式（如语音导出到不同平台），当前项目未提供配置接口，导致灵活性不足。
- **Issue #1131 用户（vvuk）**：同样遵循了检查清单，但遗漏了提供聊天会话上下文说明（未勾选相关选项）。这暗示用户可能更关注隐私保护（不想泄露敏感内容），但仍提出明确的“复制 + 导出”功能需求，方便将对话记录保存或分享。
- 两则反馈均指向 **用户对“内容控制”的期望增强**——既希望输出定制，也期望数据的便携与安全。

---

## 8. 待处理积压

- 目前无长时间未响应的 Issue 或 PR。所有条目均在 2 天内创建或更新，项目团队反馈及时。
- **建议关注**：
  - [PR #1130](https://github.com/moltis-org/moltis/pull/1130) 的 Review 进度，尽快决定是否合并，以此解决 #1127 并鼓励更多类似贡献。
  - [Issue #1126](https://github.com/moltis-org/moltis/issues/1126) 的讨论已具雏形，建议维护者给出初步方向或请求明确设计，避免讨论停滞。

---

*总结*：今日 Moltis 项目以功能建议为主，社区表达了对输出控制（TTS 格式、Markdown 导出）和 WebUI 配置灵活性的明确需求。虽无版本发布，但开发线正在推进，整体生态活跃且健康。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 CoPaw 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 GitHub 数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

### **CoPaw 项目动态日报 | 2026-06-18**

项目健康度：**高**。项目保持高度活跃，过去 24 小时内关闭了大量 Issue 和 PR，显示了高效的问题处理和代码合并节奏。两个新版本的发布（包括重要的 UI 重构和功能优化）为项目注入了新的活力。社区讨论热烈，尤其关注多 Agent 交互、性能优化和版本升级体验。尽管存在一些影响体验的 Bug，但核心功能开发与维护进展稳健。

---

### **1. 今日速览**

- **响应迅速，处理高效**：过去 24 小时内，项目团队处理了 72 个 Issue/PR（关闭 39 个 Issue 和 33 个 PR），展现了极高的响应和执行力度。
- **功能与体验双重推进**：连续发布 `v1.1.12` 和 `v1.1.12-beta.2` 版本，前者重点改写了模型提供商选择和 WebUI 简洁模式，后者则包含性能优化和会话过滤功能，朝着更好的用户装机体验迈进。
- **Bug 修复与社区反馈联动**：当天成功修复了 `ChromaDB 探针命名问题` (#5284) 和 `DingTalk 通道 SSL 问题` (#5291) 等用户报告的 Bug，并积极讨论多 Agent 互聊死循环等复杂问题。
- **路线图清晰化**：`v2.0.0a1` 版本的创建和路线图的更新，标志着项目在积极为下一代架构（agentscope 2.0）做准备。

### **2. 版本发布**

过去 24 小时内，CoPaw 发布了 **2** 个新版本。

- **`v1.1.12` (稳定版)**
  - **更新内容**: 本次版本是一次重要的功能迭代，核心在于提升用户界面和使用体验。
    - **模型页面全面改版**: 实现了提供商聚合 (`Provider Aggregation`)、统一卡片式 UI (`Unified Card UI`) 和布局重设计，预计将极大改善多模型选择时的混乱感。 ([PR #5203])
    - **简洁模式上线**: 新增简化导航栏和按更新时间排序的会话列表，为追求轻量级操作的用户提供了新的选择。 ([PR #5222])
  - **破坏性变更**: **无**。该版本主要增加新功能，不涉及底层架构的破坏性变更。
  - **迁移注意事项**: 由于 UI 有较大调整，请用户注意清理浏览器缓存，确保新 UI 正常加载。

- **`v1.1.12-beta.2` (测试版)**
  - **更新内容**: 该版本侧重于性能优化和小功能改进。
    - **性能优化**: 通过 `perf(config)` 移除了 `agent config` 中不必要的深度复制操作，可能改善配置加载性能。
    - **功能增强**: 增加了会话 (`Session`) 按标题搜索的功能 (`#4999`)，方便用户管理大量会话。
  - **破坏性变更**: **无**。
  - **迁移注意事项**: 测试版用户可直接升级，此版本为 `v1.1.12` 的补充，稳定性良好。

### **3. 项目进展**

今日项目完成了多项关键任务的合并与推进：

- **核心架构演进**:
  - **`[CLOSED] chore: release v1.1.12`**: 标志着 WebUI 重大重构的里程碑达成。
  - **`[CLOSED] bump: version to 2.0.0a1` (rayrayraykk)**: 项目正式迈入 `2.0` 时代的 Alpha 阶段，暗示着可能对 AgentScope 2.0 进行深度集成或架构革新。
  - **`[CLOSED] docs(roadmap): update roadmap` (cuiyuebing)**: 路线图更新，为社区指明了未来的发展方向。

- **Bug 修复与稳定性**:
  - **`[CLOSED] fix(memory): rename ChromaDB probe collection to 'probe-test'` (#5289)**: 修复了 ChromaDB 运行时探针因集合名不合规导致的启动警告。
  - **`[CLOSED] fix: explicitly configure SSL certificates for DingTalk channel...` (#5291)**: 修复了通过 `uv` 安装时，钉钉通道因 SSL 证书问题无法通信的 Bug。
  - **`[CLOSED] fix(proactive): prevent cache pollution of load_agent_config()` (#5275)**: 修复了主动响应模式下配置缓存可能被污染的问题。

- **功能开发**：
  - **`[OPEN] Feat/chat history right panel` (#5293)**: 一项重要的用户体验改进（将聊天历史从抽屉式改为右侧面板）已提交，正在审查中。
  - **`[CLOSED] refactor(xiaoyi): refactor connection to dual WebSocket...` (#5274)**: 重构了小艺渠道的连接架构，修复了该渠道不可用的问题。
  - **`[OPEN] feat(migrate): add OpenClaw config migration CLI tool` (#5276)**: 提供了从社区知名项目 `OpenClaw` 迁移配置的 CLI 工具，有助于吸引更多用户。

### **4. 社区热点**

- **多 Agent 互聊死循环成为焦点**：
  - **`[Bug]: 两个 QwenPaw Agent 通过 Matrix 互聊时陷入无限循环` (#5204)**: 这是目前社区讨论的核心议题之一，评论数 2 条但关注度极高。用户 `laeni` 指出了一个系统级的设计缺陷：两个通过 Matrix 通信的 Agent 之间缺乏循环反馈打断机制。这一问题比单个 Agent 的死循环影响更大，是未来实现自主多 Agent 协作必须解决的架构难题。
  - **用户诉求**: 社区希望项目不仅能提供强大的单个 Agent，更要有能力构建稳定、不失控的 Agent 网络。

- **升级后遗症引用户抱怨**：
  - **`[Bug]: 每次升级之后，被禁用的内置技能又会重新变回启用` (#5262)**: 该 Bug 在最近三个版本 (`v1.1.9` -> `v1.1.11`) 中反复出现，且是用户第二次提交。评论数 5 条，反映了用户对此类体验问题的强烈不满。
  - **用户诉求**: 期望项目的配置持久化做得更好，严格遵守“更新不改变用户既有设置”的基本原则。

### **5. Bug 与稳定性**

| 严重程度 | Issue | 描述 | 状态 & Fix PR |
| :--- | :--- | :--- | :--- |
| **高** | [#5204](https://github.com/agentscope-ai/QwenPaw/issues/5204) | 两个 Agent 通过 Matrix 互聊时陷入无限循环，缺乏环形打断机制 | OPEN，无直接 Fix PR，已获社区关注 |
| **中** | [#5284](https://github.com/agentscope-ai/QwenPaw/issues/5284) | ChromaDB 探针集合名以下划线开头，违反命名规则导致探针失败并触发降级警告 | CLOSED，已由 [#5289](https://github.com/agentscope-ai/QwenPaw/pull/5289) 修复 |
| **中** | [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | 每次升级后，已禁用的内置技能被重新启用 | OPEN，暂无 Fix PR。这是已知的用户体验回归问题 |
| **低** | [#5291](https://github.com/agentscope-ai/QwenPaw/issues/5291) (PR) | 钉钉通道在 `uv` 环境下因 SSL 配置问题而无法通信 | OPEN，已在 [#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291) 提交修复待合并 |
| **低** | [#5275](https://github.com/agentscope-ai/QwenPaw/pull/5275) (PR) | 主动响应器中 `load_agent_config()` 缓存可能被错误配置污染 | CLOSED，已修复 |

### **6. 功能请求与路线图信号**

- **UI/UX 增强是主旋律**：
  - **请求**: 社区期望能通过 Web 控制台远程升级 CoPaw ([#2235](https://github.com/agentscope-ai/QwenPaw/issues/2235))。
  - **路线图信号**: 今日合并的 `v1.1.12` 版本 UI 大改和仍在审查中的 `历史聊天面板` ([#5293](https://github.com/agentscope-ai/QwenPaw/pull/5293)) 以及 `会话页面列排序` ([#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975)) 表明，项目组将 **用户体验** 放在优先级较高的位置。

- **工具与集成扩展**：
  - **请求**: 用户希望增加后台持久化运行命令 ([#983](https://github.com/agentscope-ai/QwenPaw/issues/983))，以及优化技能使用方法 ([#2210](https://github.com/agentscope-ai/QwenPaw/issues/2210))。
  - **路线图信号**: 新建的 `OpenClaw 配置迁移工具` ([#5276](https://github.com/agentscope-ai/QwenPaw/pull/5276)) 和 `Venice AI 提供商集成` PR ([#1088](https://github.com/agentscope-ai/QwenPaw/pull/1088)) 显示项目正在积极扩大自身生态和与其他工具的互操作性。

- **Agent 能力演进**:
  - **请求**: 增加定时任务的历史执行记录 ([#1366](https://github.com/agentscope-ai/QwenPaw/issues/1366))。
  - **路线图信号**: `v2.0.0a1` 版本和 `refactor(xiaoyi)` 等多个渠道的重构工作，暗示项目正为更复杂、多 Agent、多通道的下一代架构铺路。

### **7. 用户反馈摘要**

- **痛点与不满**：
  - **升级体验差**: 用户 `daigoopautoy` 对内置技能每次升级后都被重置感到沮丧 (`#5262`)，并指出这是同一个问题第二次提交，表明该 Bug 已成顽疾。
  - **性能下降**: 用户 `pengliang159` 抱怨新版本 WebUI 在模型推理时会导致整个电脑系统卡顿 (`#4108`)，严重影响了多任务工作流。
  - **稳定性不足**: `zyc530` 反映 Agent 在思考后直接沉默 (No Response) (`#2258`)，`zyulin77-ux` 指出多 Agent 模式下模型加载经常失败 (`#2174`)，这表明核心运行时和 Agent 调度仍有待打磨。
- **使用场景与反馈**：
  - **渠道集成是核心需求**: 多个 Issue 围绕 QQ (`#2196`, `#1499`)、飞书 (`#472`) 等渠道展开，说明用户对 Agent 接入各类平台（尤其是国内平台）的需求非常高。
  - **社区包容性讨论**: 用户 `mofeiss` 在提问中吐露了因使用 AI 写代码被开源项目作者羞辱的经历 (`#2677`)，这侧面反映了 CoPaw 社区对新工具和贡献方式的开放态度（该 Issue 已关闭，但社区有友善回应）。

### **8. 待处理积压**

- **`[PR #3839] fix: XiaoYi A2A protocol implementation and tests`**: 尽管已有较新的 `#5274` 对其进行了重构并关闭，但此 PR 自 4 月底起一直处于 `Under Review` 状态。建议确认 `#5274` 是否完全覆盖了此 PR 的功能，若无，应尽快处理或明确弃用。
- **`[PR #5041] fix(backup): skip unreadable files instead of failing the whole backup`**: 此 PR 修复了一个对用户数据安全至关重要的备份问题（单个文件不可读导致整个备份失败），且已经标记为 `first-time-contributor`，自 6 月 9 日起已等待超过一周。建议维护者优先审查并合并，以鼓励社区贡献和保护用户数据。
- **`[Issue #1366] [Feature]: 增加定时任务的历史执行记录`**: 用户 `quanterRocky` 已声明本地实现了此功能并愿意贡献代码，然而该 Issue 自 3 月 12 日创建后便无后续。这是一个典型的“需求明确且有现成贡献”的场景，建议积极与用户沟通，推动此功能落地。

**结论**: CoPaw 在 2026-06-18 日表现出一个成熟且高度活跃的开源项目特质。在积极推出新功能和版本的同时，需要更加关注用户反复报告的回归 Bug（如技能重置）和严重影响体验的性能问题。同时，对积压的社区贡献（尤其是来自首次贡献者和修复关键数据的 PR）应给予更高优先级的响应，这对于维持健康的社区生态至关重要。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-06-18

---

## 1. 今日速览

过去 24 小时内，ZeroClaw 项目保持高度活跃：共处理 **50 条 Issue**（新开/活跃 49 条，关闭 1 条）以及 **50 条 PR**（待合并 39 条，已合并/关闭 11 条）。无新版本发布。  
今日亮点包括：Windows 自更新修复 ([#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853)) 进入审查；类型化别名级联删除/重命名功能堆栈完成合并 ([#7842/#7841/#7840](https://github.com/zeroclaw-labs/zeroclaw/pull/7842))；多个高影响 Bug 被修复（canvas-store 回归、ACP 事件可视化等）。社区讨论集中在桌面 GUI 控制、原生上下文压缩等高价值 RFC 上。项目整体正向 v0.8.1~v0.9.0 多个里程碑稳步推进。

---

## 2. 版本发布

**无**（过去 24 小时无新版本发布）

---

## 3. 项目进展

**今日合并/关闭的重要 PR（共 11 个）**

| PR | 说明 | 类型 |
|----|------|------|
| [#7842](https://github.com/zeroclaw-labs/zeroclaw/pull/7842) | CLI CRUD + skill-bundle cascade（8/8 堆栈尾） | enhancement |
| [#7841](https://github.com/zeroclaw-labs/zeroclaw/pull/7841) | Gateway 端 agent owned-state 重命名级联（7/8） | enhancement |
| [#7840](https://github.com/zeroclaw-labs/zeroclaw/pull/7840) | Config rename_with_cascade（6/8） | enhancement |
| [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563) | 修复 canvas-store 回归（S1） | bug fix |
| [#7684](https://github.com/zeroclaw-labs/zeroclaw/pull/7684) | ACP history-pruner / turn-cancel 现为可见事件 | bug fix |

以上配置管理堆栈的合并使 `providers/agents/channels` 的别名条目获得了完整的 **类型化级联删除与重命名** 支持，增强了配置变更的安全性。

**值得关注的活跃 PR（未合并）**

- **[Windows 自更新修复](https://github.com/zeroclaw-labs/zeroclaw/pull/7853)**（[#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853)）：将二进制交换方式从 remove-then-copy 改为 rename-then-copy，并引入 rollback/sidecar 机制，解决 Windows 上因文件锁导致的更新失败。
- **[Cron 手动触发持久化](https://github.com/zeroclaw-labs/zeroclaw/pull/7893)**（[#7893](https://github.com/zeroclaw-labs/zeroclaw/pull/7893)）：统一 RPC/API/工具三种触发路径，确保手动触发结果被持久化存储。
- **[ACP 会话历史回放](https://github.com/zeroclaw-labs/zeroclaw/pull/7903)**（[#7903](https://github.com/zeroclaw-labs/zeroclaw/pull/7903)）：修复 `session/messages` 无法读取 ACP 会话的问题。
- **[Shell 审批循环限制](https://github.com/zeroclaw-labs/zeroclaw/pull/7901)**（[#7901](https://github.com/zeroclaw-labs/zeroclaw/pull/7901)）：增加 turn-local 防护，避免重复 shell 请求反复触发审批。
- **[SSRF 保护增强](https://github.com/zeroclaw-labs/zeroclaw/pull/7902)**（[#7902](https://github.com/zeroclaw-labs/zeroclaw/pull/7902)）：为 `http_request` 工具添加 DNS 解析 IP 校验。
- **[Groq 原生工具调用修复](https://github.com/zeroclaw-labs/zeroclaw/pull/7909)**（[#7909](https://github.com/zeroclaw-labs/zeroclaw/pull/7909)）：补充 tool result 消息中的 `name` 字段，解决 HTTP 400 错误。
- **[浏览器 WebDriver 驱动修复](https://github.com/zeroclaw-labs/zeroclaw/pull/7908)**（[#7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908)）：修复截图返回 null 和 CSS 选择器转义问题。

项目整体在 **Windows 兼容性、安全性、配置管理成熟度** 方面取得了明显进步。

---

## 4. 社区热点

**最受关注的 Issues（按评论数排序）**

1. **[#6909 – RFC: Computer-use support for desktop screen interaction](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)**（6 条评论）  
   用户明确要求 ZeroClaw 具备截图和鼠标键盘控制能力，与 OpenAI Codex、Hermes 对比。目前是风险高、优先级 p2 的 RFC。若被接受将开辟全新的桌面自动化场景。

2. **[#6067 – Make channel reply-intent precheck configurable](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)**（5 条评论）  
   希望用更小/更快的模型做频道意图预检查，避免阻塞主 Agent 线程。体现了对性能透明度和可观测性的需求。

3. **[#6954 – Route scheduled tasks through orchestrator message pipeline](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)**（4 条评论）  
   旨在将 cron 调度纳入统一消息管道，解决多个上下文缺失 bug（[#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105) 等）。标志着对调度安全性和一致性的追求。

4. **[#7673 – RFC: Native context compression](https://github.com/zeroclaw-labs/zeroclaw/issues/7673)**（3 条评论）  
   提出 Provider 层的装饰器压缩方案，减少 token 消耗。商业模式价值明显，讨论热情较高。

**PR 方面**（虽无明显评论，但关注度高）  
[#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853)（Windows 更新）和 [#7492](https://github.com/zeroclaw-labs/zeroclaw/pull/7492)（缓存 token 计费）因影响面广而备受社区关注。

---

## 5. Bug 与稳定性

**严重级别划分**

| 严重度 | Issue / PR | 状态 | 说明 |
|-------|-----------|------|------|
| **S1 (工作流阻塞)** | [#7907](https://github.com/zeroclaw-labs/zeroclaw/issues/7907) | **未修复** | agent rename 在配置持久化前移动 owned state，可能导致状态不一致 |
| | ~~#7563 canvas-store regression~~ | ✅ 已关闭 | 已修复，WebSocket 后 canvas 空白 |
| **S2 (行为降级)** | [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | **未修复** | 74 个 Windows 测试失败，CI 仅覆盖 Linux |
| | [#7737](https://github.com/zeroclaw-labs/zeroclaw/issues/7737) | **讨论中** | 审批归属依赖全局侧信道，并发下可能覆盖 |
| | [#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105) | blocked | Agent 无 cron 任务上下文（待 #6954 解决） |
| **安全相关** | [#7902 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/7902) | 已提交 | http_request SSRF 漏洞修复 |
| | [#7821 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/7821) | needs-author-action | 引入沙箱策略模型，尚未对接后端 |
| **快速修复** | [#7909](https://github.com/zeroclaw-labs/zeroclaw/pull/7909) | 已提交 | Groq native tool 400 错误 |
| | [#7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908) | 已提交 | WebDriver 截图+选择器修复 |
| | [#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853) | 已提交 | Windows update 彻底失效问题 |

**重点观察**  
- [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) 已持续一周，虽然 [#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853) 改善了部分 Windows 场景，但 74 个测试失败需专项投入。  
- [#7907](https://github.com/zeroclaw-labs/zeroclaw/issues/7907) 为今日新报 S1，修复优先级极高。

---

## 6. 功能请求与路线图信号

**已接受（status:accepted）或趋势明确的功能请求**

| Issue | 方向 | 预计影响 |
|-------|------|----------|
| [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) | Computer-use 桌面控制 | 极大扩展 Agent 自动化范围 |
| [#7673](https://github.com/zeroclaw-labs/zeroclaw/issues/7673) | 原生上下文压缩 (Provider 装饰器) | 节省 API 成本，适配长上下文场景 |
| [#6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) | 调度任务接入消息管道 | 根治 cron 上下文缺失系列 bug |
| [#7675](https://github.com/zeroclaw-labs/zeroclaw/issues/7675) | 强化 CI 供应链安全 (SBOM/扫描) | 提升开源供应链安全性 |
| [#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822) | WASM 插件生命周期钩子 | 扩展插件能力，与 v0.8.2 路线图吻合 |
| [#7089](https://github.com/zeroclaw-labs/zeroclaw/issues/7089) | Windows Shell 可选 | 改善 Windows 用户体验 |
| [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) | llama.cpp 模型路由器 | 本地模型快速切换 |
| [#7887](https://github.com/zeroclaw-labs/zeroclaw/issues/7887) | Cron 日期范围条件调度 | 更灵活的定时任务配置 |
| [#7897](https://github.com/zeroclaw-labs/zeroclaw/issues/7897) | 安全策略/通道配置热加载 | 零宕机配置更新 |

**路线图信号**  
从 tracker issue 可见项目短期里程碑规划清晰：
- **v0.8.1** ([#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) – 通道/提供者/工具集成队列
- **v0.8.2** ([#7852](https://github.com/zeroclaw-labs/zeroclaw/issues/7852) 技能平台 + [#7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314) WASM 插件)  
- **v0.8.3** ([#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320)) – MCP 仪表盘与网页管理界面
- **v0.9.0** ([#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)) – 认证、安全、网关突破性变更

以上功能请求多数已被标记 accepted，预计会排入对应里程碑。

---

## 7. 用户反馈摘要

从本日 Issue 描述与讨论中提炼的用户痛点与诉求：

- **跨平台体验欠缺**：Windows 用户遇到 74 个测试失败 ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) 和自更新彻底不能用（促使 [#7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853) 修复）；Android Termux 用户安装时架构识别错误 ([#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911))。
- **上下文与记忆痛点**：Agent 执行 cron 任务后不知道已发送的消息 ([#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105))；Slack 用户必须在每次回复时再 @机器人才能让 Bot 感知线程历史 ([#6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055))。
- **可用性改进需求**：频道意图预检查希望能用轻量模型并设超时，避免阻塞 ([#6067](https://github.com/zeroclaw-labs/zeroclaw/issues/6067))；cron 广播模式希望只发送最终消息而非中间推理过程 ([#6510](https://github.com/zeroclaw-labs/zeroclaw/issues/6510))；llama.cpp 用户期望支持模型快速切换 ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539))。
- **误报与审查不满**：Skill 审核中远程 Markdown 链接的误报阻止了 `anthropics/knowledge-work-plugins` 等热门插件的安装 ([#6714](https://github.com/zeroclaw-labs/zeroclaw/issues/6714))。
- **安全性关注**：Windows 下 shell 工具限制于 cmd.exe，用户希望支持 PowerShell 并可选 ([#7089](https://github.com/zeroclaw-labs/zeroclaw/issues/7089))；并发审批归属可能被覆盖引起担忧 ([#7737](https://github.com/zeroclaw-labs/zeroclaw/issues/7737))。

总体来看，用户对 **跨平台支持、上下文管理、配置灵活性、安全性** 的诉求最为突出。项目组的快速响应（同日提交修复 PR）获得了社区的信任。

---

## 8. 待处理积压

以下 Issue/PR 长期未解决或需要维护者介入：

**严重 Bug 积压**
- [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)（6月10日） – 74 个 Windows 测试失败，无直接修复 PR，CI 也未覆盖 Windows。
- [#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105)（4月25日） – Agent 无 cron 上下文，依赖 RFC [#6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)，但 RFC 尚在讨论。

**已接受但未开始实现的 Feature**
- [#6067](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)（4月24日） – 频道 reply-intent 预检查可配置
- [#6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055)（4月24日） – Slack 线程历史回填
- [#7089](https://github.com/zeroclaw-labs/zeroclaw/issues/7089)（6月2日） – Windows Shell 可选
- [#6510](https://github.com/zeroclaw-labs/zeroclaw/issues/6510)（5月7日） – Cron announce 模式只发最终消息

**等待作者更新的 PR（needs-author-action）**
- [#7821](https://github.com/zeroclaw-labs/zeroclaw/pull/7821) – 沙箱策略配置文件
- [#7835](https://github.com/zeroclaw-labs/zeroclaw/pull/7835) – git_operations 工具恢复提示
- [#7098](https://github.com/zeroclaw-labs/zeroclaw/pull/7098) – Mattermost WebSocket 模式（已近三周）

**大型跟踪 Issue** 需维护者定期同步进展：
- [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)（v0.8.1）
- [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320)（v0.8.3）
- [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)（v0.9.0）

这些问题的推进对于维护社区信心和项目健康度至关重要。

---

*本报告基于 ZeroClaw 公开 GitHub 数据生成，所有链接可点击直达。统计区间为 2026-06-17 至 2026-06-18。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*