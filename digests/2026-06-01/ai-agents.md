# OpenClaw 生态日报 2026-06-01

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-01 03:42 UTC

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

# OpenClaw 项目动态日报 — 2026-06-01

---

## 今日速览

过去 24 小时，OpenClaw 项目持续高速迭代：

- **Issues**：500 条更新（新开/活跃 276，已关闭 224）
- **Pull Requests**：500 条更新（待合并 217，已合并/关闭 283）
- **新版本**：连续发布 4 个 beta 版本（`v2026.5.31-beta.1` → `beta.4`），重点修复 Agent/CLI 运行时中断恢复、会话绑定及多渠道交付稳定性。
- **活跃度评估**：极高。社区讨论集中在会话上下文混淆、Matrix 线程回归、MCP 工具审批等关键问题。关闭速度与新增速度基本持平，项目健康度良好。

---

## 版本发布

昨天（2026-05-31）共发布 4 个 beta 修订，官方 notes 一致，推测为逐次热修复。

| 版本 | 亮点 |
|------|------|
| `v2026.5.31-beta.1` | Agent 与 CLI 运行时从工具调用中断、过期会话绑定、compaction 传递、媒体重试中更干净地恢复 |
| `v2026.5.31-beta.2` | 同上 |
| `v2026.5.31-beta.3` | 同上 |
| `v2026.5.31-beta.4` | 同上 + 渠道传递在 Telegram、WhatsApp、iMessage、Slack 上更稳定 |

**迁移注意事项**：官方未列出破坏性变更，建议生产环境直接升级至 `beta.4`。若使用 Telegram/Matrix 等渠道，请核实线程与流式行为是否恢复正常。

---

## 项目进展

24 小时内 283 个 PR 被合并/关闭，交付节奏密集。以下为代表性的重要合并：

- **fix(mattermost): 路由附件经过上传路径**（[#88859](https://github.com/openclaw/openclaw/pull/88859)）  
  解决 Mattermost 消息中 `filePath`、`mediaUrl` 等附件被静默丢弃的问题。

- **feat(dreaming): 为 shadow trial 结果添加评分层**（[#88830](https://github.com/openclaw/openclaw/pull/88830)）  
  记忆模块新增 report‑only 评分器，仍不自动写入 `MEMORY.md`，为后续自主记忆晋升做铺垫。

- **fix(reply): 保留 `sessions_send` 的外部路由**（[#88803](https://github.com/openclaw/openclaw/pull/88803)）  
  修复通过内部 `sessions_send` 转发时丢失外部投递上下文的问题，确保线程消息正确路由。

- **fix(gateway): 本地探测认证缺失时快速失败**（[#68280](https://github.com/openclaw/openclaw/pull/68280)）  
  避免在未认证时尝试匿名 WebSocket 连接，提升本地管理安全性。

- **feat(workspace): 新增分层 bootstrap 加载**（[#22439](https://github.com/openclaw/openclaw/pull/22439)）  
  大型 PR（超过 3 个月），允许按 tier 选择性加载启动文件以节省 token，降低会话上下文开销。

此外，policy 系统（[#87074](https://github.com/openclaw/openclaw/pull/87074)）、文档（[#88875](https://github.com/openclaw/openclaw/pull/88875)、[#88886](https://github.com/openclaw/openclaw/pull/88886)）、安装脚本验证（[#82955](https://github.com/openclaw/openclaw/pull/82955)）等多项基础设施也在持续推进。

---

## 社区热点

以下 Issue 在 24 小时内获得最多评论和关注：

1. **[Agent 回复上一条消息（会话上下文混乱）**](https://github.com/openclaw/openclaw/issues/32296) — #32296，P1，13 评论  
   运行 3 个月的顽固 Bug，对话错位严重影响体验。社区强烈希望优先修复。

2. **[Matrix 线程退化为普通回复**](https://github.com/openclaw/openclaw/issues/87307) — #87307，P1，11 评论  
   2026.5.22 升级后 Matrix 线程行为倒退回普通消息，`/status`、`/model` 指令静默。渠道重度用户表达强烈不满。

3. **[预响应强制钩子（Hard Gates）**](https://github.com/openclaw/openclaw/issues/13583) — #13583，P2，11 评论  
   要求从机制上防止 Agent 绕过关键工具调用（金融/安全场景），社区普遍认为“软指令”不可靠。

4. **[MCP 工具调用的频道级审批**](https://github.com/openclaw/openclaw/issues/78308) — #78308，P2，11 评论  
   希望 MCP Server 也能复用 `/approve` 流程，已有 linked PR 在审查。

5. **[GHCR Docker 镜像配置 schema 过期**](https://github.com/openclaw/openclaw/issues/88788) — #88788，P2，9 评论  
   `2026.5.28` 镜像拒绝合法的 Discord 配置项，暴露发布验证缺口。

这些热点集中反映用户对**对话准确性、渠道稳定性和安全控制**的迫切需求。

---

## Bug 与稳定性

按严重程度排列，标注是否已有修复 PR：

| 优先级 | Issue | 摘要 | 状态 | 关联 PR |
|--------|-------|------|------|---------|
| P1 | [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent 回复错位，会话上下文混乱 | OPEN 3 个月 | 无 |
| P1 | [#87307](https://github.com/openclaw/openclaw/issues/87307) | Matrix 线程回复退化为普通回复 | OPEN | 无 |
| P1 | [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex 应用服务器启动重试耗尽，导致崩溃循环 | OPEN | 无 |
| P1 | [#86047](https://github.com/openclaw/openclaw/issues/86047) | Codex 审批停滞导致工具超时，Nextcloud Talk 会话中断 | OPEN | 无 |
| P1 | [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex 路径造成高延迟、启动中止、事件循环阻塞 | OPEN | 无 |
| P1 | [#88020](https://github.com/openclaw/openclaw/issues/88020) | Anthropic 签名失效未被识别为重试，硬失败 | **已关闭** | 具体 PR 未列 |
| P1 | [#88443](https://github.com/openclaw/openclaw/issues/88443) | `auth.cooldowns` 变更强制重启网关，丢弃运行中任务 | **已关闭** | 有修复 |
| P1 | [#81214](https://github.com/openclaw/openclaw/issues/81214) | 2026.5.7 子代理回归 | **已关闭** | 可能已合并 |
| P2 | [#88788](https://github.com/openclaw/openclaw/issues/88788) | GHCR Docker 镜像 schema 不匹配 | OPEN | 无 |
| P2 | [#85888](https://github.com/openclaw/openclaw/issues/85888) | Cron 任务在 MiniMax 503 时不重试，手动触发却成功 | OPEN | [#85888](https://github.com/openclaw/openclaw/issues/85888) 含 `linked-pr-open` |
| P2 | [#87616](https://github.com/openclaw/openclaw/issues/87616) | 本地 LM Studio 约 3 秒超时，调整参数无效 | OPEN | 无 |
| P2 | [#86342](https://github.com/openclaw/openclaw/issues/86342) | `MissingAgentHarnessError` 竞态条件（28 次/72 小时） | OPEN | 无 |
| P2 | [#87326](https://github.com/openclaw/openclaw/issues/87326) | Telegram 流式中间文本被最终块覆盖 | OPEN | 无 |
| P2 | [#87318](https://github.com/openclaw/openclaw/issues/87318) | Bedrock 推理配置 ARN 不支持，回退到 direct Anthropic | OPEN | 无 |

**观察**：大量 P1 仍未分配修复 PR，但过去 24 小时关闭了 224 个 Issue，部分问题可能已落地。团队需优先解决持续数月的 #32296。

---

## 功能请求与路线图信号

以下呼声较高的功能已有 PR 或处于活跃讨论：

1. **策略与审批机制**  
   - 预响应强制钩子（[#13583](https://github.com/openclaw/openclaw/issues/13583)）  
   - MCP 工具调用频道批准（[#78308](https://github.com/openclaw/openclaw/issues/78308)）—已有 linked PR  
   - Policy 配置覆盖率报告（[#87081](https://github.com/openclaw/openclaw/pull/87081)）—增强可视化

2. **记忆与上下文管理**  
   - Dreaming shadow trial 评分（[#88830](https://github.com/openclaw/openclaw/pull/88830)）  
   - 分层 bootstrap 加载（[#22439](https://github.com/openclaw/openclaw/pull/22439)）—等待合并

3. **模型参数扩展**  
   - 支持 `frequency_penalty` / `presence_penalty`（[#32496](https://github.com/openclaw/openclaw/issues/32496)）—多个用户支持

4. **国际化**  
   - 斜杠命令描述 i18n（[#79458](https://github.com/openclaw/openclaw/issues/79458)）—中文用户社区推动

5. **渠道深度整合**  
   - Discord 语音桥接到文本会话（[#73699](https://github.com/openclaw/openclaw/issues/73699)）  
   - Lean 模式裁剪 web 工具（[#88884](https://github.com/openclaw/openclaw/pull/88884)）—优化 OpenAI/Codex 工具集

这些信号显示项目正从 **“功能丰富”** 走向 **“安全可控、企业级就绪”**，同时兼顾用户体验精细化。

---

## 用户反馈摘要

从 Issue 描述与评论中提炼核心痛点：

- **对话错位**（#32296）  
  > “Agent 总是回答上一条消息，我的问题被忽略。” — 严重影响信任。

- **渠道回归**（#87307、#77666、#79308）  
  > “升级后 Matrix 回复变成了普通消息，线程完全乱掉。”  
  > “Feishu 群消息收得到但发不出回复。” — 升级恐惧真实存在。

- **安全担忧**（#78308、#13583）  
  > “MCP 工具直接执行，没有审批，我需要类似 shell-exec 的批准流程。” — 企业用户的刚需。

- **调试困难**（#78301、#88788）  
  > “插件加载失败没有任何错误，debug 花了几个小时。”  
  > “Docker 镜像与配置不一致，导致生产环境配置报错。” — 开发者体验有待提升。

- **区域访问**（#67670）  
  > “中国大陆通过 VPN 使用 openai-codex 被 Cloudflare 拦截，几乎不可用。” — 阻碍部分用户。

- **性能与超时**（#87616、#78435）  
  > “本地 LM Studio 3 秒就超时，所有参数调了都没用。”  
  > “Windows 下 Slack 启动阻塞事件循环 5 分钟。” — 默认配置需自适应。

整体情绪：**享受能力，但对回归和质量波动感到焦虑**。团队修复速度已获认可，但 P1 残留过长会侵蚀信任。

---

## 待处理积压

以下 Issue/PR 长期未响应或需维护者重点关注：

| 类型 | 编号 | 摘要 | 时长 | 建议 |
|------|------|------|------|------|
| Issue | [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent 会话上下文混乱（P1） | 自 2026-03-02（3 月） | 优先分配，已有详细症状说明 |
| Issue | [#13583](https://github.com/openclaw/openclaw/issues/13583) | 预响应强制钩子（P2） | 自 2026-02-10（4 月） | 需产品决策，安全场景高需求 |
| PR | [#22439](https://github.com/openclaw/openclaw/pull/22439) | 分层 bootstrap 加载 | 自 2026-02-21（3 月） | 影响广泛，需 Reviewer 推动 |
| Issue | [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex 启动重试耗尽（P1） | 自 2026-05-19（2 周） | 崩溃循环，无 fix PR |
| Issue | [#86047](https://github.com/openclaw/openclaw/issues/86047) | Codex 审批停滞导致超时（P1） | 自 2026-05-24（1 周） | 影响 Nextcloud Talk 会话 |
| Issue | [#77666](https://github.com/openclaw/openclaw/issues/77666) | Feishu 群消息无回复 | 自 2026-05-05（近 1 月，已 stale） | 影响中国用户核心场景 |
| Issue | [#78435](https://github.com/openclaw/openclaw/issues/78435) | Windows 下 Slack 启动阻塞事件循环 | 自 2026-05-06（已 stale） | Windows 性能瓶颈 |

建议维护者优先处理 **长期未动的 P1**，并与社区同步预计时间线，以维持信任。

---

*生成时间：2026-06-01 | 数据覆盖：github.com/openclaw/openclaw 过去 24 小时*

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告（2026‑06‑01）

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“功能竞赛” 向 “体验与信任攻坚” 转型的关键节点**。以 OpenClaw、ZeroClaw、Hermes Agent 为代表的一线项目每日处理数百项贡献，迭代速度前所未有；**但渠道兼容性波动、模型 API 非兼容变更、会话上下文混乱**等顽疾正在消耗用户信任，安全性与企业级就绪成为社区最强烈的共性诉求。项目间开始出现明确的分化：少数头部项目试图覆盖全功能，更多项目则聚焦于安全、区域生态或硬件延伸等差异化路径。

---

## 2. 各项目活跃度对比

| 项目 | 今日活跃 Issues | 今日活跃 PRs | 版本发布 | 健康度评估 |
|------|----------------|-------------|---------|------------|
| **OpenClaw** | 276 新开/活跃 | 217 待合并 | 4 个 beta | 极高活跃，健康良好 |
| **NanoBot** | 6 活跃 | 19 活跃（7 合并） | 无 | 响应迅速，安全加固 |
| **Hermes Agent** | 50 条更新 | 50 条更新（16 合并） | 无 | 高强度修复，追赶稳定 |
| **PicoClaw** | 3 新开 | 10 更新（7 待合） | nightly | 稳步前进 |
| **NanoClaw** | 3 新开 | 8 更新（6 待合） | 无 | 功能加速，稳定性待固 |
| **NullClaw** | 2 新开 | 0 | 无 | 排查期，平静 |
| **IronClaw** | 3 活跃 | 26 活跃 | 无 | 冲刺强劲，CI 隐忧 |
| **LobsterAI** | 1 新开 | 1 合并 | 无 | 指标低，信任风险 |
| **TinyClaw** | 0 | 0 | 无 | 无活动 |
| **Moltis** | 0 | 1（待合） | 无 | 低活跃，维护期 |
| **CoPaw** | 22 新开 | 11 活跃（1 合并） | 无 | 中高活跃，合入效率低 |
| **ZeptoClaw** | 0（1 关闭） | 0 | 无 | 极低，维护阶段 |
| **ZeroClaw** | 30 更新 | 50 更新 | 无 | 极高迭代，稳定性预警 |

> **注**：活跃数据口径因项目日报格式而异，横向对比应侧重相对量级；OpenClaw 与 ZeroClaw 的绝对活跃数遥遥领先。

---

## 3. OpenClaw 在生态中的定位

**核心参照系**：OpenClaw 是当前生态中**规模最大、渠道覆盖最全、迭代速度最快**的项目。

### 优势
- **功能广度**：支持 Telegram、WhatsApp、iMessage、Slack、Matrix、飞书、Discord 等十余个渠道，内置 Agent/CLI 运行时、MCP 工具、记忆分层（Dreaming）等模块。
- **社区规模**：每日 500+ 更新，276 个活跃 Issue，217 个待合 PR，是第二梯队项目的 5~10 倍。
- **迭代纪律**：一天内连发 4 个 beta 热修复，关闭/合并速度与新增基本持平，项目健康度良好。

### 技术路线差异
- 与 **NanoBot** 相比：OpenClaw 更追求全覆盖，而 NanoBot 偏重企业安全（AAD、SSRF 防护）与轻量交互。
- 与 **Hermes Agent** 相比：Hermes 紧贴上游模型（Codex、Opus）做专项适配，OpenClaw 则通过通用抽象层支撑更多 Provider。
- 与 **ZeroClaw** 相比：ZeroClaw 采用 Rust 实现高性能与硬件扩展（ESP32），OpenClaw 保持主流语言（Go/Python）的生态可及性。
- 与 **PicoClaw / NanoClaw** 相比：后两者定位为“轻量变体”，OpenClaw 则是“旗舰版”。

### 最大挑战
**P1 Bug 久治不愈**（如 #32296 会话上下文混乱已 3 个月）及渠道回归频发（#87307 Matrix），在用户信任上持续失分。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|--------|
| **会话上下文持久化与压缩** | OpenClaw、NanoBot、Hermes、Moltis、CoPaw | 上下文混乱（#32296）、记忆评分（#88830）、tool 结果截断（#1089）、按需加载（#4836） |
| **多渠道交付稳定性** | OpenClaw、Hermes、ZeroClaw、PicoClaw、NullClaw | Matrix 线程退化（#87307）、Telegram 流式覆盖（#87326）、WhatsApp mention_only（#7032） |
| **安全审批与强制策略** | OpenClaw、NanoBot、ZeroClaw、CoPaw | 预响应硬钩子（#13583）、MCP 频道级审批（#78308）、SSRF 防护（#4123）、RBAC（#5982） |
| **模型 API 兼容性** | Hermes、OpenClaw、PicoClaw、ZeroClaw | Opus 4.8 Schema 变更（#34554）、Codex 流式修复（#2967）、Gemini OAuth 失败（#4879） |
| **记忆与长期知识** | OpenClaw、NanoBot、Moltis | Dreaming shadow trial（#88830）、轻量 RAG（#4109）、持久化上限（#1089） |
| **硬件/多模态延伸** | ZeroClaw、NanoBot、Hermes | ESP32 智能房间（#7045）、浏览器录音（#4122）、视频分析（#36224） |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户画像 | 技术架构特色 |
|------|---------|-------------|-------------|
| **OpenClaw** | 全功能个人助手，渠道全覆盖 | 普通用户至高级玩家，追求开箱即用 | 统一网关 + MCP 工具生态 + 记忆分层 |
| **NanoBot** | 企业级安全与团队协作 | 中小企业、受合规约束的团队 | 强认证（AAD）、无通知净化、SSRF 防护 |
| **Hermes Agent** | 上游模型兼容与平台扩展 | 最新模型发烧友、多平台管理员 | SDK 层兜底，快速适配 Codex/Anthropic 变更 |
| **PicoClaw** | 轻量高频迭代 | 社区尝鲜者、快速验证场景 | nightly 驱动，简化组件 |
| **NanoClaw** | 网关基础与部署密度 | 自运维开发者 | 单线程宿主模型，OneCLI 网关 |
| **NullClaw** | 最小可行产品 | 极小团队或个人 | 功能极简，目前 Bug 修理期 |
| **IronClaw** | 架构现代化（Reborn） | 大型部署、多后端 | Triggers/Outbound 模块重构，libSQL 持久化 |
| **LobsterAI** | 商业 SaaS + 积分系统 | 付费用户（中文区） | 前端优化为主，积分逻辑争议 |
| **Moltis** | 会话历史健壮性 | 长对话重度用户 | Cap tool 结果截断，数据管道加固 |
| **CoPaw** | Qwen 生态 + IDE 集成 | 中文开发者、Code 用户 | 基于 agentscope，强调项目管理能力 |
| **ZeptoClaw** | 极小维护 | 研究观察 | 仅安全扫描，几乎无功能推进 |
| **ZeroClaw** | Rust 高性能 + 多渠道 + 硬件 | 技术极客、IoT 探索者 | Rust 全栈，TUI 客户端，ESP32 支持 |

---

## 6. 社区热度与成熟度分层

### 🔥 第一梯队：超高活跃、快速迭代
- **OpenClaw**：日活最高，流程成熟，但 P1 积压影响成熟度评分。
- **ZeroClaw**：Rust 社区驱动，S1 Bug 频现，处于“交付速度优先”阶段。
- **Hermes Agent**：为适配上游高频变更，处于持续“追赶-稳定”循环。
- **CoPaw**：新 Issue 大量涌入（22/日），但合并效率低（1/11），耦合风险累积。

### ✅ 第二梯队：稳定活跃、方向明确
- **NanoBot**：安全加固路线清晰，PR 合并率高（7/19）。
- **PicoClaw / NanoClaw**：小而美的迭代节奏，积压可控。
- **IronClaw**：架构迁移积极，但 CI 长期失败暴露质量缺口。

### ⏳ 第三梯队：维护或低活跃
- **LobsterAI**：单 Issue 引发信任危机，商业属性干扰开源节奏。
- **Moltis**：防御性开发，仅土壤加固。
- **NullClaw / ZeptoClaw**：接近休眠，依赖零星贡献。

### 💤 休眠
- **TinyClaw**：完全无活动。

---

## 7. 值得关注的趋势信号

### 7.1 上下文管理成为核心瓶颈
多个项目同时投入记忆评分、分层加载、tool 结果截断。**开发者应重视会话历史的持久化策略**，避免“只压缩不治理”。

### 7.2 安全治理从“软指令”走向“硬门槛”
审批钩子、RBAC、SSRF 防护不再只是企业专属，社区普遍意识到用户级 Agent 也需防止误操作。**内建可插拔策略层将成为新一代 Agent 框架的必要条件**。

### 7.3 模型 API 非兼容变更是最大外部风险
Hermes 连遭 Opus 4.8 与 Codex 冲击，PicoClaw 修复 OAuth 流式，ZeroClaw 苦于 Gemini OAuth 数周。**建议项目在 Provider 层引入契约测试与自动降级机制**。

### 7.4 渠道体验“木桶效应”显著
用户不会因为整体功能强而原谅单一渠道的回复错乱。Matrix 退化、WhatsApp 不响应、飞书静默等 Bug 直接触发社区情绪波动。**渠道回归测试应纳入 CI 核心门禁**。

### 7.5 硬件与多模态成为差异化新战场
ZeroClaw 的 ESP32 支持、NanoBot 的语音输入探索、Hermes 的视频分析表明，Agent 正在走出文本会话，**感知物理世界的能力将是 2026 下半年最具区隔度的竞争力**。

### 7.6 本地化与国际化的拉锯
LobsterAI 因积分清零引发中文用户不满，CoPaw 背靠 Qwen 生态，飞书集成在多项目出现。**尊重区域市场特性和合规诉求，是项目从小众走向主流的关键一步**。

---

**报告总结**：当前生态“头重脚轻”——头部项目功能丰度急速膨胀，但稳定性与安全性欠债同步累积；二线项目通过窄聚焦换取用户忠诚；沉睡项目则面临边缘化。对于开发者，选择框架时应优先考察其 **上下文治理能力、渠道回归质量、以及安全策略的可扩展性**，而非单纯的功能列表长度。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 GitHub 数据生成 NanoBot 项目动态日报。

## NanoBot 项目动态日报 | 2026-06-01

---

### 1. 今日速览

今日 NanoBot 项目活跃度较高。24 小时内共处理了 6 个 Issues 和 19 个 Pull Requests，合并/关闭了 7 个 PR，显示出较强的开发响应能力。核心议题集中在 **安全加固**（WebSocket 令牌签发、SSRF 防护）、**会话管理 Bug 修复**（消息重复归档、代码块渲染崩溃）以及 **企业级功能支持**（Azure AAD 认证）。尽管没有新版本发布，但多个关键 Bug 和安全修复已被合入主干，项目的稳定性和安全性得到显著提升。

### 2. 版本发布

**无**

今日无新版本发布。

### 3. 项目进展

今日合并/关闭了 7 个 PR，项目在 Bug 修复、安全加固和架构解耦方面取得了实质性进展。

- **【安全】WebSocket 令牌签发权限修复**: PR [#4103](https://github.com/HKUDS/nanobot/pull/4103) 已合并，关闭了安全 Issue [#4077](https://github.com/HKUDS/nanobot/issues/4077)。该修复阻止了在未配置 `tokenIssueSecret` 时，未经认证即可签发短时效令牌的漏洞，加强了 WebSocket 连接的安全性。
- **【Bug 修复】Heartbeat 无任务通知修复**: PR [#4112](https://github.com/HKUDS/nanobot/pull/4112) 和 PR [#4114](https://github.com/HKUDS/nanobot/pull/4114) 均已合并，关闭了 Issue [#4111](https://github.com/HKUDS/nanobot/issues/4111)。修复了 Heartbeat 定时任务在无任务时错误地向飞书发送 “All clear.” 通知的问题，并增加了“失败封闭”机制，确保内部检查的结果不会误发送给用户，提升了通知的可靠性。
- **【增强】目标追踪迭代预算扩展**: PR [#4127](https://github.com/HKUDS/nanobot/pull/4127) 已合并。该 PR 为 `/goal` 任务引入了内部持续目标延续路径，当达到常规的工具调用迭代预算时，可以继续执行，防止长任务被截断，增强了 Agent 的执行能力。
- **【Bug 修复】WebUI 代码块渲染崩溃修复**: PR [#4117](https://github.com/HKUDS/nanobot/pull/4117) 已合并，关闭了 Issue [#4116](https://github.com/HKUDS/nanobot/issues/4116)。修复了 WebUI 在处理没有指定语言的代码块时，因 `react-syntax-highlighter` 接收 `undefined` 而直接白屏崩溃的高严重性问题。
- **【架构】WebUI 渲染与宿主运行时优化**: PR [#4121](https://github.com/HKUDS/nanobot/pull/4121) 已合并。优化了 WebUI 的流式聊天渲染，使普通回复、推理过程和文件编辑动作的展示更加稳定和有序，并保持 WebUI 宿主边界通用性。

### 4. 社区热点

今日社区讨论焦点集中在以下几个方面：

1.  **企业级新需求**：来自新贡献者 **kunalk16** 的 Issue [#4125](https://github.com/HKUDS/nanobot/issues/4125) 和 PR [#4126](https://github.com/HKUDS/nanobot/pull/4126) 是一个强关联的“需求+实现”组合。该需求提出为 Azure OpenAI Provider 增加基于 Azure AAD 的身份认证（替代 API Key），这是一个典型的**企业级部署**痛点。
    - **分析:** 这释放了一个强烈信号：NanoBot 的用户群体正在从个人开发者扩展到受严格安全策略约束的企业团队。该功能有望在下一个版本中被快速集成。

2.  **外围工具集成探索**：Issue [#4120](https://github.com/HKUDS/nanobot/issues/4120) 虽然已关闭，但其讨论（1 条评论）探讨了将 NanoBot 与 Vest 的 MCP 集成，以实现 SaaS 工具的推荐或商业化角度。这表明社区不仅在关注框架本身，也在思考其与外部商业生态的结合。

3.  **多模态支持萌芽**：PR [#4122](https://github.com/HKUDS/nanobot/pull/4122) 为 WebUI 添加了录音和本地语音识别功能（基于 FunASR），处于开放状态。这反映了社区对**多模态交互**的期待，但该 PR 被标记为 `[enhancement, invalid]`，可能需要进一步的架构讨论或调整，值得关注其后续进展。

### 5. Bug 与稳定性

今日共报告 4 个 Bug，其中 2 个高/中危 Bug 已被修复。整体反馈显示项目质量处于快速迭代优化阶段。

- **(高) WebUI 白屏崩溃**: Issue [#4116](https://github.com/HKUDS/nanobot/issues/4116) (已关闭) → **已由 PR [#4117](https://github.com/HKUDS/nanobot/pull/4117) 修复**。问题在于无语言标识的代码块会导致页面直接崩溃，严重影响用户体验。
- **(中) 会话消息重复归档**: Issue [#4128](https://github.com/HKUDS/nanobot/issues/4128) (**新开**). Bug 报告者 `huji820` 详细描述了在 `retain_recent_legal_suffix` 方法的 else 分支下，用户消息会被同时归档到 archive 和 kept 中，可能导致 LLM 上下文不一致。**无修复 PR，是潜在风险点。**
- **(中) Heartbeat 错误通知**: Issue [#4111](https://github.com/HKUDS/nanobot/issues/4111) (已关闭) → **已由 PR [#4112](https://github.com/HKUDS/nanobot/pull/4112) 和 PR [#4114](https://github.com/HKUDS/nanobot/pull/4114) 修复**。
- **(高) WebSocket 令牌签发漏洞**: Issue [#4077](https://github.com/HKUDS/nanobot/issues/4077) (已关闭) → **已由 PR [#4103](https://github.com/HKUDS/nanobot/pull/4103) 修复**。

### 6. 功能请求与路线图信号

今日用户提出的功能需求明确指向了两大方向：

1.  **企业级认证与安全**:
    - **Azure AAD 认证**: Issue [#4125](https://github.com/HKUDS/nanobot/issues/4125) 需求明确，且 **PR [#4126](https://github.com/HKUDS/nanobot/pull/4126) 已提交**，这是最有可能被优先纳入下一版本的功能。
    - **URL 安全校验**: PR [#4123](https://github.com/HKUDS/nanobot/pull/4123) 为 MCP 链接增加了 SSRF 防护，体现了对安全性的持续投入，也是企业级特性之一。

2.  **WebUI 多模态能力**:
    - **WebUI 语音转录**: PR [#4122](https://github.com/HKUDS/nanobot/pull/4122) 提出的本地语音识别虽被标记为 `[enhancement, invalid]`，但其方向代表了社区对更丰富交互方式的渴望。这可能促使项目方在未来思考如何以更合理的架构来支持多模态输入。

3.  **记忆与上下文增强**:
    - **轻量 RAG**: 来自 `gqcao` 的 PR [#4109](https://github.com/HKUDS/nanobot/pull/4109) 提出了一个轻量级 RAG 方案用于记忆检索，目前处于开放状态。这表明项目正在探索赋予 Agent 更长效记忆的能力，这可能是未来版本的一个重要特性。

### 7. 用户反馈摘要

从今日的 Issues 和 PR 评论中，可以提炼出以下用户声音：

- **“请提供符合企业安全策略的认证方式”**。用户 `kunalk16` 在 Issue [#4125](https://github.com/HKUDS/nanobot/issues/4125) 中明确表示，其 Azure 订阅不允许使用 API Key 认证，迫切需要 AAD 认证。这是企业用户对安全合规性的硬性要求。
- **“代码块没有语言标识就会让我看白屏，很痛苦”**。Issue [#4116](https://github.com/HKUDS/nanobot/issues/4116) 的报告者直接指出了 WebUI 的严重崩溃问题，这是一个影响日常使用的痛点。
- **“Heartbeat 总是报告‘一切正常’，感觉很烦人”**。Issue [#4111](https://github.com/HKUDS/nanobot/issues/4111) 反映了用户对无效通知的厌恶。社区提出的解决方案（如静默推理、仅发送重要消息）被 PR [#1443](https://github.com/HKUDS/nanobot/pull/1443) 和 [#4112](https://github.com/HKUDS/nanobot/pull/4112) 等采纳，显示了社区对改善用户体验的快速响应。
- **“希望能在浏览器里直接录音让 Agent 处理”**。PR [#4122](https://github.com/HKUDS/nanobot/pull/4122) 的提交者正在为 WebUI 提供一种全新的交互方式，但尚未得到最终认可，有待观察。

### 8. 待处理积压

以下两项任务已开启较长时间，可能需要维护者关注：

- **PR [#1443](https://github.com/HKUDS/nanobot/pull/1443)**: (`feat: decouple heartbeat reasoning from notification`) 该 PR 由 `phelps-sg` 于 2026-03-02 开启，旨在使 Heartbeat Agent 默认静默推理。它与今日修复的 [#4111](https://github.com/HKUDS/nanobot/issues/4111) 问题直接相关，但解决方案更加彻底。此 PR 已存在 3 个月，建议评估其与近期 Heartbeat 修复（[#4112](https://github.com/HKUDS/nanobot/pull/4112)）的关联性，决定是否将其合并。
- **PR [#3990](https://github.com/HKUDS/nanobot/pull/3990)**: (`refactor(dream): replace two-phase Dream class with simple cron + process_direct`) 该 PR 于 2026-05-24 开启，提出对 Dream 功能进行重大重构。鉴于其改动较大且涉及核心功能，需要维护者重点审查，以避免潜在冲突。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent 项目数据生成的 2026 年 6 月 1 日项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-01

---

## 1. 今日速览

2026 年 6 月 1 日，Hermes Agent 项目运维极其活跃，呈现高强度的“修复与追赶”态势。过去 24 小时内，项目共处理 50 条 Issue 和 50 条 PR，关闭/合并了 16 项。开发团队当前的重点在于：1）紧急应对上游模型提供商（Anthropic Opus 4.8、OpenAI Codex）的 API 变更引起的兼容性危机；2）强化 Docker 与 Gateway 底层架构的稳定性；3）积极吸纳社区贡献以扩展社交平台功能。尽管当日无新版本 Release，但从 PR 提交数量和质量来看，下一个版本将面向 **“稳定性恢复”** 与 **“多平台体验补齐”** 迈进。

---

## 2. 版本发布

本日无新版本发布。

---

## 3. 项目进展

**优先响应上游变更，修复兼容性危机：**
- **OpenAI Codex / gpt-5.5 稳定性（#33075）**：关闭。针对 Codex CLI 可用但 Hermes 集成失败的顽疾，贡献者 (**matheuz31**) 在 **PR #36217** 中提交了跳过 OpenAI SDK 流式包装器、直接使用 `httpx` 消费 SSE 的原生修复。
- **Anthropic Opus 4.8 Thinking Schema 变更（#34554）**：关闭。快速适配了 Anthropic 的非兼容性变更，解决了 400 报错。

**Docker 与部署基础设施加固：**
- **Hostinger 迁移崩溃（#34192）**：**PR #34382** 合入，为旧版 `tini` 启动器添加了兼容垫片，解决了 s6-overlay 镜像的迁移阵痛。
- **Docker 运行时权限错误（#34107）**：**PR #34268** 合入，修复了新 Profile 子目录在非默认 UID/GID 环境下的权限问题。

**核心稳定性修复：**
- **Kanban 调度器楔死（#31158）**：关闭。修复了 SQLite WAL/SHM 缓存中毒导致的多线程并发死锁。
- **测试 CI 回归修复（#36215）**：提交，修复了 GUI 启动器测试和 Model Catalog 的回归。

---

## 4. 社区热点

- **Codex 稳定性持续发热（#33075, #13834）**
  尽管 Bug #33075 已标记关闭，但它在关闭前积累了 **14 条评论**和 **11 个 👍**。社区核心诉求非常尖锐：“**官方 Codex CLI 在相同环境下能用，为什么 Hermes 不行？**”。这反映出用户对代理层稳定性的极高要求。与此同时，同类型的老 Issue **#13834**（创建已 40 天，P2）依然处于未关闭状态，表明底层问题可能未被彻底根除。

- **Anthropic Opus 4.8 的“双重打击”（#34554, #36151）**
  刚刚修复了 Thinking Schema，Bedrock 渠道立刻爆出 `temperature` 参数被弃用的新问题 (**#36151**, P1, 当日创建)。用户对“新模型发布即不可用”的节奏感到焦虑，这对 Adapter 层的健壮性和测试覆盖提出了严峻考验。

- **架构级特性 RFC 引发深度讨论（#31392）**
  关于“代理原生任务中继与自动 Forking 子代理”的 RFC 收获了 **7 条评论**。社区高级用户正在探索 Agent 更复杂的协作模式，这预示着未来架构演进的前沿方向。

- **云同步刚需持续领跑社区心愿单（#20510）**
  “云同步”Feature Request 以 **9 个 👍** 高居榜首。虽无对应 PR，但强烈暗示了多设备用户对配置/记忆/技能同步的底层诉求。

---

## 5. Bug 与稳定性

**严重级（P1，直接阻断或造成数据/经济损失）**
- **#36151 (New Today)**: Bedrock 上 Opus 4.7/4.8 因带 `temperature` 参数被强制拒绝（400）。 **无 Fix PR 认领**。
- **#25281 (Pending)**: Dashboard “Update Hermes” 按钮一键清空所有 Cron 任务。**破坏性极强，等待认领**。
- **#11970 (Backlog, 44天)**: Bedrock Prompt Caching 因未注入 `cachePoint` 标记而**静默失效**，用户持续支付全价。P1 级别长期未解决。

**主要级（P2，主要功能受损或交互阻塞）**
- **#33961 (Pending)**: `/new`, `/clear` 斜杠命令导致终端完全冻结，无法 Ctrl+C 中断。
- **#36213 (New Today)**: Windows 平台下 `hermes gateway restart` 因未等待旧进程释放端口而导致新进程**静默启动失败**。**已有 Fix PR #36223**。
- **#36184 (New Today)**: Telegram 平台上 Agent 在后台任务取消后仍强行执行并推送结果。**逻辑缺陷**。
- **#36149 (New Today)**: Dashboard “Schedules” UI 因前端请求 `/api/cron/jobs` 与后端路由 `/api/jobs` 不匹配而**整体白屏**。
- **#36144 (New Today)**: Agent 会话将 `HOME` 环境变量指向 Profile 目录，导致工具内解析 `~` 指向错误路径（如 SSH 配置找不到）。

---

## 6. 功能请求与路线图信号

**高确定性（对应 PR 已提交，大概率进入下个版本）**
- **多模态体验对齐（#36224）**：新增 `video_analyze` 工具，修复 Discord 视频附件全链路并推广至所有平台。
- **飞书原生流式体验（#36202）**：利用飞书 CardKit 流式 API，解决限频和 UI 闪烁问题，提升中国大陆企业用户交互体验。
- **Agent 工具搜索智能提示（#36218）**：当工具搜索启用时，引导模型先搜索再断言能力缺失。
- **Hindsight Memory 防丢（#36219）**：修复会话结束未达到 `retain_every_n_turns` 时，已缓冲的轮次被静默丢弃的问题。

**中低确定性（社区意愿强，但官方无明确动作）**
- **云同步（#20510）**：呼声最高（9 👍），但无对应 Roadmap 或 PR 信号。
- **模型自动发现（#10011）**：趋势向好，**#36212** 正在为 MiniMax 等 Provider 扩充列表，但自动发现机制尚未铺设。

---

## 7. 用户反馈摘要

**核心痛点：**
1. **Codex 体验割裂（最关切）**：用户在 #33075 中明确表示“**同一台机器，官方 CLI 能跑，Hermes 不跑**”。这种对比严重的信任危机是项目当前在 API 代理层面面临的最大挑战。
2. **破坏性变更的惊吓**：用户 `fwends` 在 #25281 中表达了对“点击更新 → Cron 作业消失”这一毁灭性操作的震惊。
3. **配置与环境折磨**：Docker 迁移不适（#34192）、环境变量冲突（#31144）、路径指向错误（#36144）构成了自部署用户的连续挫败感。
4. **财务成本的焦虑**：Bedrock 用户 `aws-yz` 在 #11970 中精准地指出了核心矛盾：“**我在支付它根本没有使用到的缓存费用**”。

**肯定方向：**
- 社区贡献者生态活跃，来自不同地区的开发者正在积极补齐平台短板（Feishu CardKit, Discord Video, MiniMax 模型）。
- 维护团队对 P1/P2 级别 Bug 的响应速度较快（如 Opus 4.8 Schema 的当日关闭）。

---

## 8. 待处理积压

**⚠️ 最需维护者关注：**
- **#13834 (Codex 不稳定)**: 创建 40 天。尽管子 Bug #33075 关闭，但更老的 #13834 仍 Open，核心问题可能未被根除。
- **#11970 (Bedrock 缓存失效)**: 创建 44 天。P1，直接造成用户持续经济损失且无官方回复。
- **#17452 (自定义 Provider 模型名被截断)**: 创建 33 天。严重阻塞使用本地代理（CCS/LiteLLM）的用户。

**⏳ 待 Review 紧急合并：**
- **PR #33855 (Anthropic 15分钟挂起修复)**: 4 天待 Review。P1 级修复，影响大量 Anthropic 原生用户，应加速合并。
- **PR #31861 (Gateway 内存写入失败透明化)**: 7 天待 Review。功能完善，对调试 Agent 静默错误至关重要。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 — 2026-06-01

## 1. 今日速览

- 发布 Nightly 构建 `v0.2.9-nightly.20260601`，囊括从 `v0.2.9` 至今的所有主分支变更。
- 过去 24 小时 6 个 Issues 获更新（新开/活跃 3 个，关闭 3 个），10 个 PRs 获更新（合并/关闭 3 个，待合并 7 个）。项目整体保持活跃。
- **关键修复合并**：`#2967` 修复了 OpenAI Codex OAuth 场景下流式 delta 事件被忽略导致的空响应问题；`#2856` 合并实现 `message` 工具的媒体附件能力，关闭对应功能请求。
- 多个新功能（Cron 扩充、Telegram 回复触发、Anthropic SDK 升级、技能依赖检查）处于待合并状态，表明社区贡献热情持续。
- 一批较早的 `stale` PR（改善总线背压、agent 重载稳定性等）仍未回应，需维护者关注评审。

## 2. 版本发布

- **nightly (Nightly Build)**  
  `v0.2.9-nightly.20260601.ba806592`（自动构建，可能不稳定）  
  完整变更对比：https://github.com/sipeed/picoclaw/compare/v0.2.9...main  
  说明：每日自动从 `main` 分支构建，包含截至当日的全部合并提交。适合测试新功能与修复，生产环境建议使用正式版本。
  无显式破坏性变更列出，但因包含众多实验性改动，使用前请关注相关 PR 说明。

## 3. 项目进展

过去 24 小时合并/关闭的重要 PR：

- **`#2967` fix(codex): preserve streamed output text deltas**（已合并）  
  修复了 OpenAI Codex OAuth 使用 ChatGPT 后端时，因流式 `response.output_text.delta` 事件未被积累导致的空响应问题。关闭了 `#2953`。  
  https://github.com/sipeed/picoclaw/pull/2967

- **`#2856` feat(message): support media attachments and Telegram rich delivery**（已合并）  
  实现了 `message` 工具对媒体附件单次投递的支持，并利用 Telegram 原生的富文本能力。关闭了功能请求 `#2855`。  
  https://github.com/sipeed/picoclaw/pull/2856

- **`#2980` chore: gitignore debug output files**（已合并）  
  代码清理，忽略调试输出文件。  
  https://github.com/sipeed/picoclaw/pull/2980

以上合并提升了对 ChatGPT Codex 后端的兼容性，并赋予了 agent 更自然的多模态消息发送能力。项目正稳步朝更稳健、更丰富的功能集合迈进。

## 4. 社区热点

- **`#2674`** (Open) – Codex OAuth empty assistant response 问题持续受关注（7 评论，👍 4）。用户报告使用 Codex OAuth 连接 ChatGPT 后端时获得空响应，并指出根因在于 `response.output_item.done` 事件未被恰当处理。虽然 `#2967` 修复了 `output_text.delta` 事件，但本 issue 涉及不同代码路径，仍为开放状态。  
  https://github.com/sipeed/picoclaw/issues/2674

- **`#2968`** (Open) – `/context` 总是显示 “Compress at: 76800 tokens”（3 评论，👍 1）。用户在使用 MiniMax 模型时发现上下文压缩数值固定不变，指向 UI 反馈或数值更新 bug。  
  https://github.com/sipeed/picoclaw/issues/2968

- **`#28`** (Closed) – LM Studio 简易连接请求虽已关闭，但累积 21 条评论和 2 个 👍，反映社区对新 provider 简易集成的渴望。  
  https://github.com/sipeed/picoclaw/issues/28

- **`#2975`** **`#2977`** 为新提交的 PR，暂无评论，但 Telegram 回复触发和 Cron 管理增强潜力较大，值得后续关注。

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 状态 | 是否有 Fix PR |
|---------|------------|------|------|--------------|
| **严重** | `#2674` (Open) | Codex OAuth 使用 ChatGPT 后端返回空响应（`response.output_item.done` 未处理） | 未关闭，需进一步诊断 | `#2967` 修复了部分症状，但未完全覆盖该 issue |
| **中等** | `#2968` (Open) | `/context` 指令始终显示 76800 tokens，可能 UI 未刷新 | 未有 fix PR | / |
| **已修复** | `#2953` (Closed) | 同为空响应，问题在于 `output_text.delta` 被忽略 | 已关闭（由 `#2967` 修复） | `#2967` 已合并 |
| **稳定性** | `#2906` (stale) | 消息总线背压处理与健康可见性改进 | 开放未审 | 待合并 |
| **稳定性** | `#2904` (stale) | agent 循环重载及 panic 清理修复 | 开放未审 | 待合并 |

项目在 Codex 集成方面的 bug 有显著改善，但总线背压和 agent 重载等运行时稳定性补丁仍处于等待队列，一旦合并将进一步提升产品健壮性。

## 6. 功能请求与路线图信号

- **`#2978`** (Open) – 请求添加 **OmniRoute** 作为新 provider。用户贴出第三方路由项目链接，并询问如何配置 combo。表明社区希望丰富 provider 生态。  
  https://github.com/sipeed/picoclaw/issues/2978

- **`#28`** (Closed) – LM Studio 简易连接虽关闭，但高评论量显示类似简化集成请求有潜力；未来或可由新贡献者基于现有 provider 抽象实现。

- 待合并 PR 指向的下一阶段功能：
  - **`#2977`** (Open) – `cron` 工具新增 `get` 与 `update` 动作，允许 agent 检查并部分更新 cron 任务而不需重建，避免调度丢失。  
  - **`#2975`** (Open) – Telegram 回覆机器人消息视为 @提及，优化群聊交互体验。  
  - **`#2936`** (Open) – 技能依赖检查：自动跳过所需二进制缺失的技能，防止 LLM 被引导调用不可执行工具。  
  - **`#2902`** (Open) – Android Termux 运行指南，降低移动端部署门槛。  
  - **`#2979`** (Open) – 升级 `anthropic-sdk-go` 至 v1.46.0，保持 Anthropic provider 兼容性。

这些功能覆盖了 provider、工具链、消息交互、文档等多个维度，预计会纳入 `v0.3.0` 或后续版本。

## 7. 用户反馈摘要

- **`#2674`** 用户 `geekgonecrazy` 详细描述了空响应问题的触发模式，强调并非 OAuth 或 token 错误，而是代码对 `response.output_item.done` 流事件处理缺失，并提供了后端返回内容样例。表达了修复后仍希望得到彻底解决的期待。  
- **`#2968`** 用户 `xpader` 抱怨 `/context` 数值固定，在使用 MiniMax 最大 token 调优时无法确认实际压缩情况，影响调优体验。  
- **`#2978`** 用户 `urtaevS` 直截了当请求添加 OmniRoute，并截取配置界面，表明用户对第三方 provider 开放集成有真实需求。  
- **`#28`** 用户 `Franzferdinan51` 自谦技能不足，希望有人帮忙实现 LM Studio 简易连接，并感谢社区。反映出普通用户对”开箱即用“高级功能的依赖。  
- **`#2953`** 用户 `livinghorror` 精确指出 `output_text.delta` 事件被忽略，协助定位修复，社区协作质量高。  
- **`#2855`** 用户 `bogdanovich` 提出 message 工具应原生支持媒体附件，让 agent 一次调用即可发送图文，而不需拆分操作，这一需求已被合并实现。

整体来看，社区反馈集中于 **provider 兼容性细节** 和 **实用功能增强**，贡献者提交的 bug 报告质量较高，加速了问题修复。

## 8. 待处理积压

以下 PR/Issue 长期未有维护者响应或评审，建议尽快跟进：

| 编号 | 类型 | 创建日期 | 摘要 | 最后更新 | 建议处理 |
|------|------|---------|------|---------|---------|
| `#2906` | PR (stale) | 2026-05-20 | 修复总线背压与健康可见性 | 2026-05-31 | 代码质量较高，关系到运行期稳定性，优先评审 |
| `#2904` | PR (stale) | 2026-05-20 | Agent 重载与 panic 清理 | 2026-05-31 | 同上，建议与 #2906 一同审查 |
| `#2936` | PR (stale) | 2026-05-24 | 技能依赖跳过（关联 #2351） | 2026-05-31 | 对 tool-use 场景有帮助，需判断取舍 |
| `#2902` | PR (stale) | 2026-05-20 | Android Termux 指南文档 | 2026-05-31 | 低风险，可快速合并以提升移动端用户友好度 |
| `#2674` | Issue (Open) | 2026-04-26 | Codex OAuth 空响应（`output_item.done` 未处理） | 2026-05-31 | 虽部分修复但未关闭，需确认是否仍有问题，考虑关闭或标记已知限制 |
| `#28` | Issue (Closed) | 2026-02-11 | LM Studio 简易连接 | 2026-05-31 | 已关闭但可考虑作为 future 功能，添加标签订阅 |

积压主要集中在 **2026-05-20** 提交的一批 PR 上。若能及时评审合并，将显著提升项目的稳定性与平台覆盖度。建议维护者分配一轮集中审核。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 | 2026‑06‑01

## 1. 今日速览
- 过去 24 小时提交 **3 个 Issues** 和 **8 个 Pull Requests**（6 个待合并，2 个已合并/关闭），无新版本发布，整体活跃度较高。
- 新 Issues 集中曝光了核心运行时与网关的稳定性短板：单线程宿主可被同步操作完全冻结、OneCLI 网关进程无声凋亡后无法自愈、突发负载下文件描述符耗尽导致静默中断。这些问题直接威胁生产可用性，需优先响应。
- 社区贡献者 GiladShoham 单日提交 4 个功能性 PR（MCP 服务器传输扩展、技能斜杠命令注册、外部符号链接挂载、容器清理修复），加上浏览器 sidecar、Hugging Face 集成等 PR，功能迭代节奏明显加快。
- 项目正处于“功能快速推进、稳定性亟待加固”的关键期；合并/关闭的 2 个 PR 初步引入了会话追踪上传和部署整合，但关键 Bug 修复尚未落地。

## 2. 版本发布
无（本周期无新版本 Release）

---

## 3. 项目进展——今日合并/关闭的重要 PR
- **#2648**（已合并）`feat: add /upload-trace command to upload session trace to Hugging Face` —— [PR #2648](https://github.com/qwibitai/nanoclaw/pull/2648)  
  新增 `/upload-trace` 指令，允许用户将会话追踪数据上传至 Hugging Face，提升协作与数据复用能力。
- **#2658**（已关闭）`Actual deployment` —— [PR #2658](https://github.com/qwibitai/nanoclaw/pull/2658)  
  部署流程相关变更（细节未详述），标志着部分部署环节已整合。

其余 6 个 PR 仍处于待合并状态（详见第 6 节），总体看项目在 **技能集成** 和 **外部服务对接** 两个方向取得了明确进展。

---

## 4. 社区热点
尽管各议题评论区均为空，以下 Issues/PRs 因涉及核心架构或呈现高贡献密度值得关注：

- **#2665** 单线程宿主任意同步/无界操作导致完全冻结，健康检查失效  
  [Issue #2665](https://github.com/qwibitai/nanoclaw/issues/2665)  
  请求：引入 async 策略或看门狗机制，阻止单点阻塞拖垮全局。

- **#2657** OneCLI 网关 worker 进程死亡但容器状态未变，Docker `restart` 不生效  
  [Issue #2657](https://github.com/qwibitai/nanoclaw/issues/2657)  
  请求：增加进程监督与 fail-fast 容器退出逻辑。

- **共贡献者 GiladShoham 的 PR 集群**（#2662, #2661, #2660, #2659）  
  该贡献者同一日提交了 MCP 服务器 HTTP/SSE 支持、技能斜杠命令自动注册、外部符号链接容器挂载、容器清理修复等 4 个 PR，覆盖扩展性、易用性与稳定性，反映出社区对平台深度定制的强烈需求。

- **#2664** 浏览器抓取 sidecar 集成到 v2 容器，同时捆入了网页抓取、NotebookLM、Mer 音频等技能  
  [PR #2664](https://github.com/qwibitai/nanoclaw/pull/2664)  
  请求：拓宽自动化范围，使容器天然附带浏览器能力。

虽然评论数字为 0，但议题广度与 PR 密度表明社区参与度实际较高，讨论多集中在设计层面（通过 PR 代码和 Issue 摘要直接表达）。

---

## 5. Bug 与稳定性（按严重程度降序）

| 严重程度 | 编号 | 问题描述 | Fix PR 状态 |
|----------|------|----------|-------------|
| **P0‑Critical** | #2655 | OneCLI 网关在突发负载下因默认 1024 文件描述符软限制硬退出（`os error 24`），所有 Agent 静默断联 | 无对应 PR；需提升 ulimit / 引入连接池 |
| **P0‑Critical** | #2665 | 单 Node 事件循环被 unbound `await` 或同步调用完全冻结，`/health` 无法检测；所有定时器与通道适配器停止 | 无对应 PR；需架构层的异步化或超时看门狗 |
| **P1‑High** | #2657 | OneCLI gateway 容器进程死亡但容器 `Up`，Docker 标记 `unhealthy` 后因 `restart:` 策略不生效而无法自愈 | 无对应 PR；需进程 supervisor 或故障注入自终止 |
| **P2‑Medium** | #2659 (待合并) | 主机无法 `docker stop/kill`（如非特权 LXC）时产生孤儿容器，且 `activeContainers` 重启丢失导致泄漏 | [PR #2659](https://github.com/qwibitai/nanoclaw/pull/2659) 已提交，仍未合并 |

**备注**：@mshirel 提出的三个 P0–P1 问题尚无任何 Fix PR，需要维护者尽快规划。

---

## 6. 功能请求与路线图信号

以下待合并 PR 很可能被纳入下一版本，它们共同指向 **多协议连接、零配置技能发现、模块化资源挂载** 的路线：

- **#2662** `feat: add HTTP/SSE MCP server support`  
  [PR #2662](https://github.com/qwibitai/nanoclaw/pull/2662)  
  将 `McpServerConfig` 从仅 stdio 扩展为支持 HTTP、SSE 传输，便于接入远程/托管 MCP 服务。

- **#2661** `feat: register per-group skills as Claude Code slash commands at spawn time`  
  [PR #2661](https://github.com/qwibitai/nanoclaw/pull/2661)  
  自动将 `groups/<group>/skills/` 链接到 Claude Code 扫描路径，无需手动配置，大幅提升技能可发现性。

- **#2660** `feat: mount external symlink targets for per-group skills`  
  [PR #2660](https://github.com/qwibitai/nanoclaw/pull/2660)  
  使跨组共享技能库（符号链接指向宿主目录）在容器内正确解析，支持更大规模的技能复用。

- **#2664** `[codex] run browser scraping sidecar in v2 container`  
  [PR #2664](https://github.com/qwibitai/nanoclaw/pull/2664)  
  将浏览器 sidecar 及其附带技能（web‑fetch、NotebookLM、Mer audio、Paris rental）直接构建到 v2 容器镜像，降低部署复杂度。

- **#2648** 已合并（见第 3 节）的 Hugging Face 上传，未来可演化成更通用的 Trace 生态系统。

此外，**#2656** 修复了 mnemon 技能因入口点覆盖而失效的问题，是一个轻量级但重要的易用性修复。

---

## 7. 用户反馈摘要（来自 Issues 描述）

- **“宿主单线程被一次长时间构建或 channel deliver() 堵死后，整个服务静默挂起，连浅层健康检查都无法发现。”**  
  （#2665）→ 用户需求：非阻塞执行与异步健康探测。

- **“OneCLI gateway 的 worker 进程凭空消失了，容器却一直 Up。Docker 虽然给了 ‘unhealthy’，但没有触发重启——所有 Agent 的 HTTPS_PROXY 指向一个死掉的网关，造成全局不可用且无人知晓。”**  
  （#2657）→ 用户需求：进程级监督 + 容器状态联动重启。

- **“突发流量时网关直接 `Error: No file descriptors available (os error 24)` 挂掉，没有任何前置告警，Agent 们只能得到连接错误。”**  
  （#2655）→ 用户需求：自适应 fd 池 / 主动限流 / 运行时 ulimit 提升。

这些描述均出自部署运维场景，反映当前版本在 **生产健壮性** 上存在可观测性盲区和恢复缺陷。正面的功能反馈（如 Hugging Face 上传，#2648）表明社区对数据共享能力持欢迎态度。

---

## 8. 待处理积压

今日所有 Issue 与 PR 均创建于 2026‑05‑31，尚无响应，故不存在严格意义上的“长期未响应积压”。但以下事项需维护团队优先关注：

- **三个无 Fix PR 的 P0/P1 问题**（#2655, #2665, #2657）需尽快分配资源、开始设计或给出缓解措施。
- **待合并 PR 队列**（共 6 个）包括稳定性修复（#2659）和多个增强（#2662, #2661, #2660, #2664, #2656），强烈建议在本周内完成 Review 并合并，以避免分支分歧增大。
  - #2659: 容器孤儿泄漏修复
  - #2656: mnemon 技能入口修复（用户反馈入口点失效）
  - #2662 / #2661 / #2660 / #2664: 功能增强（见第 6 节）
- **贡献者 GiladShoham 的系列 PR** 涉及配置结构变更（#2662 修改了 `McpServerConfig`），建议核心维护者尽早给出反馈，避免后续冲突。

---

> **声明**：本日报基于 [qwibitai/nanoclaw](https://github.com/qwibitai/nanoclaw) 公开数据自动生成，旨在为项目社区与维护者提供快速状态摘要。所有链接均已内嵌到对应编号。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 NullClaw 项目 2026-06-01 动态日报。

---

## NullClaw 项目日报 | 2026-06-01

### 1. 今日速览
2026年6月1日，NullClaw 项目整体进入 Bug 排查期，代码提交侧相对平静，无新版本发布与 Pull Request 合并。社区贡献者 `weissfl` 提交了 2 条高质量的 Issue，精准指出了**核心调度功能的严重故障**与 **Telegram 渠道的交互体验缺陷**。今日的活跃度完全由 Issue 追踪驱动，项目亟需对关键 Bug 进行响应与修复以维持社区信任。

### 2. 版本发布
今日无新版本发布或预发布构建。

### 3. 项目进展
今日无 Pull Request 被提交或合并，项目主干未引入新的代码变更或功能增强。项目当前的开发重心预计将全面转向处理最新报告的 2 则 Issue。

### 4. 社区热点
今日社区讨论热度不高（两则 Issue 暂无评论和点赞），但集中度很高，全部围绕用户 `weissfl` 的报告展开。这两条 Issue 构成了社区当前最核心的期待：

*   **[#941] Agent 定时任务子进程未启动**：[查看详情](https://github.com/nullclaw/nullclaw/issues/941)
    *   直接攻击了项目“定时 Agent”功能的核心可用性，是今日社区投递的最重磅信号。
*   **[#942] Telegram 内联按钮缺少打字指示器**：[查看详情](https://github.com/nullclaw/nullclaw/issues/942)
    *   暴露了消息渠道交互底层的不一致性。

### 5. Bug 与稳定性

**严重级别：严重 (Critical)**
*   **[#941] Agent 定时任务子进程未启动**：[链接](https://github.com/nullclaw/nullclaw/issues/941)
    *   **描述**：使用 `schedule` 创建 `job_type: "agent"` 任务后，系统显示“完成”，但 Agent 子进程实际从未启动，导致 Telegram 消息无法投递。
    *   **影响范围**：核心功能瘫痪。依赖定时 Agent 的用户完全无法使用该功能，属于典型的静默失败。
    *   **状态**：待修复，无关联 PR。

**严重级别：中等 (Medium)**
*   **[#942] Telegram 内联按钮响应无打字指示器**：[链接](https://github.com/nullclaw/nullclaw/issues/942)
    *   **描述**：点击内联按钮（回调查询）时，用户看不到正在处理的“输入中…”状态，而普通文本消息则正常显示。
    *   **影响范围**：功能可用，但交互体验降级。容易让用户误以为 Bot 卡死或未收到命令。
    *   **状态**：待修复，无关联 PR。

### 6. 功能请求与路线图信号
今日未收到全新的功能请求 (Feature Request)，两条 Issue 均属于 Bug 修复范畴。
*   **路线图优先级信号**：`#941` 暴露了项目底层任务调度链路（调度->子进程->投递）出现了严重断裂。这必须被列为 **P0 级（最高优先级）** 紧急修复，否则该功能模块的信任度将完全归零。
*   **潜在的 UX 增强方向**：`#942` 暗示了未来 Telegram 渠道交互层需要统一化处理，无论消息类型是文本还是内联按钮回调，都应提供一致的反馈机制。

### 7. 用户反馈摘要
基于今日唯一提报用户 `weissfl` 的反馈：
*   **核心痛点：系统可信度受挫**。用户严格按照文档配置，系统静默失败（任务显示完成但未执行）。这种“静默吞没”比直接报错更具破坏性，严重透支用户对自动化功能的信任。
*   **体验细节诉求**：用户对交互即时反馈有较高期待。Bot 在 Telegram 上缺少“正在输入”状态，让用户感到困惑，说明在社区用户心目中，NullClaw 的 Bot 交互体验应该向成熟的即时通讯 Bot 看齐。
*   **用户画像**：`weissfl` 是典型的深度高阶用户，正在探索 Agent + Scheduling 的组合能力，并对交付渠道（Telegram）的体验细节非常敏感。

### 8. 待处理积压
今日无长期未响应的历史积压 Issue 或 PR，但新增了 2 个需要立即关注的任务：
1.  **[#941] Agent 定时任务子进程未启动**：当前项目最紧急且影响最广的 Bug，建议立即进入修复流程。
2.  **[#942] Telegram 内联按钮打字指示器缺失**：建议在 #941 修复后，作为增强补丁跟随下一个版本发布。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 (2026-06-01)

## 1. 今日速览

过去24小时内项目共产生26条PR更新和3条Issue更新，整体活跃度处于高位。核心团队在"Reborn"架构迁移上持续发力：Triggers模块迎来首个持久化后端（libSQL）、Outbound模块通信决议引擎落地、OAuth产品流程重构里程碑（#3289）顺利关闭。然而项目健康度存在隐忧：夜间E2E测试（#4108）连续多日失败且无人响应，MCP stdio传输的核心Bug（#2923）因被错误关闭而重新提起且尚无修复方案。**总体评价：开发冲刺势头强劲，但CI稳定性与核心Bug修复存在欠账，技术债务值得警惕。**

---

## 2. 版本发布

过去24小时内无新版本发布。

---

## 3. 项目进展

**Triggers 模块奠基**
- 作者 `henrypark133` 提交的 [`PR #4263`（已合并）](https://github.com/nearai/ironclaw/pull/4263) 为 Reborn Triggers 系统实现了首个持久化后端（libSQL），标志着触发器功能从设计走向可用。紧接着 [`PR #4270`（开放中）](https://github.com/nearai/ironclaw/pull/4270) 已开始推进 PostgreSQL 后端，多数据库支持路线明确。

**Outbound 通信模块起步**
- [`PR #4262`（已合并）](https://github.com/nearai/ironclaw/pull/4262) 添加了通信候选决议引擎（Candidate Selection Only），这是 Reborn Outbound 模块的核心基础，为后续的目标验证、负载渲染和实际发送铺平道路。同日 [`PR #4271`（开放中）](https://github.com/nearai/ironclaw/pull/4271) 在其基础上叠加了出站验证桥。

**产品级认证流程重组**
- [`Issue #3289`（已关闭）](https://github.com/nearai/ironclaw/issues/3289) 正式关闭，作为管控项标志着 secrets、OAuth 和 auth-setup 产品流程的重构（Reborn）工作完成。`serrrfirat` 的 [`PR #4257`（已合并）](https://github.com/nearai/ironclaw/pull/4257) 实现了 AuthPromptView challenge 增强及 WebUI v2 OAuth 卡片，完成了前端与底层认证能力的对接。

---

## 4. 社区热点

**最受关注的 Issue：#2923**
- [`Issue #2923`](https://github.com/nearai/ironclaw/issues/2923) "stdio MCP activation fails" 是对已关闭 Issue #2474 的重新提交。用户 `rajulbhatnagar` 明确指出了之前因非维护者评论被错误关闭的问题，并澄清 Bug 位于激活预检（activation pre-flight）而非传输层本身。4 条评论、1 个 👍 反映了社区对 MCP 标准传输层可靠性的高度关注，用户情绪带有明显的不满与急切。

**关注度最高的 PR 集群：多平台集成**
- Slack 集成栈（`PR #4035` + `PR #4272`）和飞书集成（[`PR #4178`](https://github.com/nearai/ironclaw/pull/4178)）是社区最关注的功能方向，分别涉及 Slack Events API 宿主入口和飞书长连接 WebSocket 事件摄入。
- **深层诉求**：社区不希望局限于单一通道，对生产级多平台接入（特别是企业协作工具）有强烈的路径依赖需求。

---

## 5. Bug 与稳定性

**严重（Critical）**

| 编号 | 问题 | 严重程度 | 状态 |
|---|---|---|---|
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E 定时执行失败 | **阻塞性** | Bot 自动报告，无维护者响应。连续失败自5/27起，严重影响合并信心。 |
| [#2923](https://github.com/nearai/ironclaw/issues/2923) | stdio MCP 激活失败（核心功能回归） | **高** | 重新提起的旧 Bug，尚无关联修复 PR。Issue 明确 v0.25.0 已端到端支持 stdio，Bug 仅限激活预检。 |

**潜在风险（Potential Risk）**

- 依赖批量更新 PR 堆叠严重。`[#4001](https://github.com/nearai/ironclaw/pull/4001)`（tokio-ecosystem 组，其中 tokio-tungstenite 0.26 → 0.28 含主版本跳跃）、`[#4268](https://github.com/nearai/ironclaw/pull/4268)`（45+ 依赖一并更新）均待合并超过一周。此类批量更新一旦合并引入回归，排查成本极高。

---

## 6. 功能请求与路线图信号

社区暂无新的功能请求提交；当前活跃的 PR 全部指向内部路线图的严格执行。

**确定的路线图信号：**

| 方向 | 关键 PR | 信号解读 |
|---|---|---|
| **多站点 SSO** | [`#4229`](https://github.com/nearai/ironclaw/pull/4229) webui-v2 原生 GitHub SSO | 在 Google OAuth (#4182) 之后补齐 GitHub SSO，WebUI v2 身份认证能力趋于完善 |
| **企业通道集成** | [`#4272`](https://github.com/nearai/ironclaw/pull/4272) Slack Events API / [`#4178`](https://github.com/nearai/ironclaw/pull/4178) 飞书 WebSocket | 第三方通道进入深度开发阶段，飞书走长连接方案，Slack 构建完整 ProductAdapter |
| **开发者体验提升** | [`#4184`](https://github.com/nearai/ironclaw/pull/4184) 统一 Diff 预览 | write_file / apply_patch 的 Diff 可视化，工具结果更友好 |
| **Product Auth 闭环** | [`#4239`](https://github.com/nearai/ironclaw/pull/4239) / [`#4269`](https://github.com/nearai/ironclaw/pull/4269) | 用户侧凭据配置 → Runtime 凭据代理的自动投影和认证需求传播，体系日趋成熟 |

---

## 7. 用户反馈摘要

由于过去24小时社区用户仅活跃于 Issue #2923，反馈集中在以下痛点：

- **用户 `rajulbhatnagar`** 在 [`#2923`](https://github.com/nearai/ironclaw/issues/2923) 中表达了强烈诉求：
  - 🚩 **痛点**：stdio MCP 作为核心传输通道，激活预检失败导致整个功能不可用。
  - 🚩 **不满**：Issue 之前因一条非维护者的错误评论（"stdio not supported"）被关闭，用户花了额外精力重新举证和提交，提出应提高社区回复和 Issue 关闭的门槛。
  - ✅ **亮点**：用户承认「v0.25.0 已端到端接线 stdio」，说明项目文档或能力宣发是到位的，问题具体锁定在激活环节的 pre-flight 校验，属于实现细节 Bug 而非架构缺失。

---

## 8. 待处理积压

以下为需要维护者重点关注的长期未决/高优先级项：

| 优先级 | 项目 | 问题 | 建议行动 |
|---|---|---|---|
| 🚨 **P0 阻塞** | [`#4108`](https://github.com/nearai/ironclaw/issues/4108) Nightly E2E 失败 | 自 5/27 起持续失败，无人工响应 | 立即排查 CI 基础设施或上游依赖变更 |
| 🚨 **P0 阻塞** | [`#2923`](https://github.com/nearai/ironclaw/issues/2923) stdio MCP Bug | 旧 Bug 重新提起，无修复 PR | 评估修复时间表，必要时创建修复分支 |
| ⏳ **P1 高风险依赖** | [`#4001`](https://github.com/nearai/ironclaw/pull/4001) tokio-ecosystem 更新 | 涉及 tokio-tungstenite 主版本跃进（0.26→0.28），已待合并 8 天 | 安排核心成员审查，优先测试 |
| ⏳ **P2 阻塞开发** | [`#4035`](https://github.com/nearai/ironclaw/pull/4035) Slack ProductAdapter core | 自 5/25 开放，作为 Slack 集成栈基座 PR，阻塞上层 #4272 | 尽快推进代码评审 |
| 📋 **P2 待处理** | [`#4271`](https://github.com/nearai/ironclaw/pull/4271) Outbound 验证桥 | 刚创建的 XL 规模 PR，涉及新模块架构 | 尽早分配 Reviewer 避免堆积 |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是基于您提供的 LobsterAI GitHub 数据生成的 2026-06-01 项目动态日报。

---

### LobsterAI 项目动态日报 | 2026-06-01

#### 1. 今日速览
今日项目整体活跃度**偏低**。社区方面，一条关于订阅积分月末清零的强烈投诉（`#2081`）成为焦点，其负面情绪已构成潜在的用户信任风险，需项目方密切关注。代码方面，一项涉及多模块的 UI 与代码规范优化 PR（`#2080`）已成功合入，体现了维护工作的持续性。但一个修复“定时任务幽灵会话”的严重 Bug PR（`#1465`）已停滞近两月未合并，对项目稳定性构成了长期积压风险。

#### 2. 版本发布
（今日无新版本发布，此部分略。）

#### 3. 项目进展
今日合并/关闭 PR 1 项：
- **#2080 [已合并/关闭]** `chore: optimize kits and upload file ui`
  - **链接：** [netease-youdao/LobsterAI PR #2080](https://github.com/netease-youdao/LobsterAI/pull/2080)
  - **简述：** 由贡献者 `fisherdaddy` 提交，覆盖了 `renderer`、`docs`、`main`、`cowork` 四大核心模块。本次合并主要推进了代码库的规范性优化以及文件上传界面的交互优化。这表明团队在大修大补的同时，仍在对日常用户体验进行精细化打磨。

#### 4. 社区热点
今日讨论热度最高的为 Issue #2081：
- **#2081 [Open]** `订阅`
  - **链接：** [netease-youdao/LobsterAI Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081)
  - **简述：** 作者 `zjk648491625` 因 5500 订阅积分在月底未使用即被清零感到极度不满（“来搞笑的吧???”），并附上了截图佐证。该 Issue 目前获得了一条评论响应。
  - **诉求分析：** 用户对“积分月结清零”的规则表现出了强烈的排斥心理，暴露出产品在订阅规则透明度、到期提醒及用户预期引导方面的严重缺失。

#### 5. Bug 与稳定性
- **严重 Bug (修复方案受阻) #1465**
  - **标题：** `fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现`
  - **链接：** [netease-youdao/LobsterAI PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)
  - **严重程度：** **中/高**。该 Bug 影响定时任务功能的正常工作，已删除的任务在重启后会以空内容的“幽灵会话”形式复活。开发者已定位到根因（删除时未清理本地 SQLite 关联记录）并提供了修复代码，但 PR 自 4 月 4 日起便处于停滞状态。此类数据残留问题严重影响功能可靠性，建议维护者尽快推动评审与合并。
- **高影响用户问题 (待定性) #2081**
  - **标题：** `订阅`
  - **链接：** [netease-youdao/LobsterAI Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081)
  - **严重程度：** **高（商业逻辑/用户信任）**。如果积分清零是系统逻辑 Bug（如误扣、特殊场景下的计数异常），则属于严重缺陷；如果这是既定的商业化产品策略，则暴露了严重的用户预期管理失败。无论哪种情况，都需要项目组迅速定性并公开回应，避免舆情发酵。

#### 6. 功能请求与路线图信号
今日未收到直接提出的功能请求。但 Issue #2081 向产品团队释放了强烈的**路线图信号**：
- **订阅系统透明化需求：** 用户显然反对“不结转到下月”的积分机制。社区可能呼吁增加**积分有效期可视化提醒、到期前多次推送通知、或提供消耗积分保留额度的选项**。
- **路线图预判：** 结合已合并的 `#2080`（优化 UI），下一版本迭代可能会侧重于前端用户体验的改进，极有可能会包含**订阅与积分面板的重新设计**以缓解此类矛盾。

#### 7. 用户反馈摘要
- **核心反馈来源：** Issue #2081 (`订阅`)
- **痛点分析：** 付费用户的核心资产（积分）在无消耗的情况下被系统强制回收。
- **用户情绪：** **极度不满与失望**。用户使用了明显的攻击性和嘲讽性语言（“来搞笑的吧”），心理模型是“我付费购买了我拥有所有权的商品/服务”，而“月度清零”机制打破了这个预期，产生了强烈的被欺骗感。
- **建议对策：** 如果是 Bug，需立刻致歉并恢复积分；如果是既定规则，社区经理需立即在 Issue 中发声解释规则，并认真评估此机制对核心用户留存率的潜在打击。

#### 8. 待处理积压
以下项长期未获得关注，提醒维护者重点关注：
- **#1465 [Open] (Stale)** `fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现`
  - **等待合并天数：** 58 天（自 2026-04-04 起）
  - **风险分析：** 有一个明确的 Issue (#1359) 关联该 Bug，且 Fix 分支已经写好。长时间不合并不仅让 Bug 持续影响用户，还容易导致修复代码与主分支脱节，增加未来的合并成本，并打击外部贡献者的积极性。
  - **链接：** [netease-youdao/LobsterAI PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-06-01

---

## 1. 今日速览

过去24小时内，Moltis 项目整体进入平静期。未产生新的 Issue 和版本发布，社区互动量极低。唯一的技术活动是开发者 `s-salamatov` 提交了 **PR #1089**，专注于对 tool 与 tool_result 的持久化内容进行容量上限控制，以增强会话历史重载（Rehydration）的稳定性。尽管无合并产出，该 PR 仍体现了项目在数据管道加固与长对话稳定性上的持续投入。整体活跃度评估：**低，偏维护期**。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 2. 版本发布

**无。** 今日无新版本发布。

---

## 3. 项目进展

今日**没有 PR 被合并或关闭**，项目无功能层面的前进。唯一值得关注的进展是新提交的 **PR #1089**（待合并状态）：

**PR #1089 | Cap persisted tool results before rehydration**
- **作者**: `s-salamatov`
- **内容**: 解决会话历史（Session History）反序列化为 Provider-bound ChatMessage 时，历史上持久化的 `tool` 和 `tool_result` 内容未被限制大小的问题。
- **覆盖范围**: 涉及普通对话、流式对话、压缩后重试、Prompt 检查、静默记忆轮次（Silent memory turns）、及 LLM 背书的压缩提示词等**几乎所有会话恢复场景**。
- **意义**: 该 PR 是对项目数据管道的一层关键防护，直接影响长上下文对话中的 Token 超限风险和 Provider API 调用稳定性。

虽然没有合入代码，但该 PR 的提出表明项目正在对核心的状态恢复机制进行**系统性稳定性加固**。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 4. 社区热点

今日社区讨论近乎为零，无评论、无点赞互动。唯一的活跃项是 **PR #1089**。

**诉求分析**: 尽管缺乏显式讨论，该 PR 所聚焦的 "Tool 结果持久化溢出风险" 是所有 AI Agent 项目在长对话场景下的**通用痛点**。未受控的 Tool 结果堆积会导致：
- 上下文窗口浪费
- Provider 侧请求失败
- 重载时状态不一致

这反映出开发团队正在主动清理此类隐患，而非等待用户大量反馈后再修复。项目倾向于**防御性开发策略**。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 5. Bug 与稳定性

今日无新 Bug Issue 被报告。

**隐式稳定性修复**：
- **PR #1089** 可以视为对一类潜在 Bug 的修复——持久化后的 `tool` 和 `tool_result` 数据在重载时缺乏上限检查。
- **严重程度评估**: **中-高**。未截断的 Tool 输出是长对话中最常见的稳定性杀手之一，容易导致"悄无声息"的请求失败或回退退化。
- **修复状态**: 已提交，待审查合并。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 6. 功能请求与路线图信号

今日无新增功能请求 Issue。

**路线图信号（基于 PR #1089 推测）**：

该 PR 的改动覆盖了 `retry-after-compaction`、`prompt inspection`、`silent memory turns`、`LLM-backed compaction prompts` 等多个高级功能模块。这表明项目组正在对整个**会话生命周期管理**（写入 → 持久化 → 重载 → 压缩）构建统一的容量边界控制策略。下一个版本极有可能包含以下方向的改进：

- 会话历史重载机制的健壮性大幅提升
- 工具调用（Tool Call）结果的资源控制更严格
- 内存轮次（Memory Turns）与压缩（Compaction）流程的数据安全性增强

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 7. 用户反馈摘要

今日无任何用户评论、Issue 反馈或点赞行为被记录。

由于无法获取直接反馈，我们可以从 **PR #1089 的开发动机**反推用户端可能的痛点：开发者在多个会话恢复路径上同步添加容量限制，暗示之前存在由于 Tool 结果过大导致的重载失败或下游 Provider 报错，这很可能来源于早期用户/测试者的真实反馈。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

## 8. 待处理积压

当前公开 Issue 及 PR 积压数极低，项目维维护状态良好。

**需维护者关注的一项**：

| 类型 | 编号 | 标题 | 状态 | 关键提醒 |
|---|---|---|---|---|
| PR | #1089 | Cap persisted tool results before rehydration | 待合并 | 影响多个核心流程（正常、流式、重试、压缩），建议尽快审查，避免与后续开发分支冲突。 |

该 PR 于今日提交，是当前唯一处于活跃状态的待处理项。

- 链接：[PR #1089](https://github.com/moltis-org/moltis/pull/1089)

---

报告总结：Moltis 项目今日呈 **低位运行但聚焦稳定** 的态势。尽管无合并和新发布，但对会话重载机制的深度加固表明项目正从“功能铺设”向“稳定性打磨”过渡，健康度良好。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，各位开发者和用户，以下是 CoPaw 项目 2026 年 6 月 1 日的项目动态日报。

---

### CoPaw 项目动态日报 | 2026-06-01

---

#### 1. 今日速览

项目今日活跃度处于中高水平，社区提交密集，但 resolution 速度有待提升。过去 24 小时内，社区提交了 22 个新 Issue，但仅关闭 5 个，Issue 积压量仍在缓慢增长。PR 流动方面，有 11 个 PR 处于活跃状态，但只有 1 个被合并，10 个仍处于待审核或 WIP 状态，合并速度偏慢。主要 Bug 集中在 MCP 进程管理、Windows 兼容性、定时任务与 Session 共享等问题上，其中大部分已有对应的修复 PR 在等待合并。新功能请求则聚焦在用户体验优化和配置灵活性上，例如对话管理、思考强度选择器等，反映了用户对产品成熟度的更高期望。

#### 2. 版本发布

**无**

---

#### 3. 项目进展

今日合并的 PR 数量较少，但社区提交的修复和功能 PR 质量较高，核心进展在于修复了一系列近期报告的 Bug。

- **已合并/关闭 (1个):**
    - **#4810 [已关闭] feat(console): improve chat slash skill suggestions** `saltapp`
        - **摘要:** 优化了聊天输入框的“/”技能建议功能，现在会显示当前 Agent 可用的技能，并将建议列表限制在 5 个，提升了交互体验。
        - **影响:** 仅影响 Web UI 前端。
        - **状态:** 已关闭，已合并。

- **关键待合并 PR (影响分析):**
    - **#4849 [OPEN] perf(mcp): add SharedMCPPool to reuse MCP servers across agents** `wangfei010313`
        - **摘要:** 为解决 **#4842** (Windows 下大量 Agent 导致 MCP 进程爆炸)，引入了共享 MCP 服务器池，允许多个 Agent 复用同一个 MCP 进程。
        - **影响:** 重大问题修复，对部署了大量 Agent 的用户至关重要。
    - **#4820 [OPEN] fix(context): normalize inline source URL strings in media blocks** `jc200808`
        - **摘要:** 修复 **#4811** (上下文压缩时因 `source` 字段格式异常导致崩溃) 的问题。
        - **影响:** 提高了系统的健壮性，防止因特定格式的 LLM 回复导致服务崩溃。
    - **#4822 [OPEN] fix(crons): fix share_session cron agent tasks producing empty traces** `jc200808`
        - **摘要:** 修复 **#4818** (Cron 任务在 `share_session=true` 时，执行轨迹为空且 Agent 未实际执行) 的问题。
        - **影响:** 关键 Bug 修复，保证了定时任务功能的可靠性。
    - **#4812 [OPEN] fix(website):header style, add auto continue video** `yuluo1007`
        - **摘要:** 修复了官网头部样式，并增加了自动播放视频的功能。
        - **影响:** 仅影响项目官网，与核心产品无关。

---

#### 4. 社区热点

今日最受关注的议题主要集中在**用户对 Agent 行为控制**和**协议兼容性**上。

1. **#4789 [CLOSED] [Feature] 希望 QwenPaw 能像 Trae 那样，可以删除和回退对话**
    - **热度:** 8条评论 | 1 👍
    - **诉求:** 用户强烈希望 QwenPaw 能参考 Trae 的工作模式，实现精细化的对话管理，包括：
        - 回退/删除单条对话。
        - 回退时自动还原文件状态并二次确认。
        - 管理每次更改而非整个沙箱。
        - 支持链接本地目录。
    - **分析:** 这反映了用户从“对话式编程”向“项目式编程”的演进需求，要求 Agent 能深入到文件级别的精细化管理。

2. **#4808 [OPEN] [Question] Agent "person_stat_skill" 不存在**
    - **热度:** 7条评论
    - **诉求:** 用户按照文档编写了自定义 `SKILL.md`，但 Agent 在匹配到该技能后，却报告 Agent 不存在。用户需要指导以解决如何正确配置和使用自定义技能。
    - **分析:** 这表明文档与实际逻辑可能存在偏差，或技能加载逻辑存在 Bug，是影响社区贡献自定义技能体验的关键节点。

3. **#4824 [OPEN] [Bug] ACP 协议连接 Claude Code 协议对不上**
    - **热度:** 3条评论
    - **诉求:** 用户尝试通过 ACP 协议连接 Claude Code，但遇到协议版本号格式不匹配 (`protocolVersion` 应为数字却是字符串) 和 `delegate_external_agent` 内部错误的问题。
    - **分析:** 这是一个重要的集成兼容性报告，表明 QwenPaw 的 ACP 协议在与第三方 Agent (Claude Code) 对接时存在实现差异，这可能阻碍其作为 Agent 中心的生态发展。

---

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在 **Windows 平台兼容性**、**资源泄漏**和**核心功能异常**上。

- **严重/高危:**
    - **#4842 [OPEN] [Bug]: Windows 上大量 Agent 导致 MCP 进程爆炸**
        - **问题:** 每个 Agent 独立创建 MCP 进程，300 个 Agent 会导致大量进程，造成资源耗尽。
        - **状态:** 已有修复 PR **#4849**。
        - **链接:** [#4842](https://github.com/agentscope-ai/CoPaw/issues/4842)
    - **#4844 [OPEN] [Bug]: Windows 上浏览器进程和临时目录锁未被清理**
        - **问题:** Agent 调用浏览器后，残留进程和目录锁阻止备份和后续操作。
        - **状态:** 暂无已知修复 PR。
        - **链接:** [#4844](https://github.com/agentscope-ai/CoPaw/issues/4844)
    - **#4837 [OPEN] [Bug]: v1.1.9 频繁出现系统级 fallback 回复**
        - **问题:** 升级后，Agent 在正常对话中频繁返回固定 fallback 消息，表明系统存在降级处理问题，可能与超时或调度器有关。
        - **状态:** 暂无已知修复 PR。
        - **链接:** [#4837](https://github.com/agentscope-ai/CoPaw/issues/4837)

- **中等/配置相关:**
    - **#4832 [OPEN] [Bug]: Shell 命令子进程缺少 CREATE_NO_WINDOW 标志导致 CMD 窗口闪烁**
        - **问题:** 在 Windows 上执行 shell 命令会弹出 cmd 窗口。
        - **状态:** 问题根源已指出，暂无修复 PR。
        - **链接:** [#4832](https://github.com/agentscope-ai/CoPaw/issues/4832)
    - **#4834 [OPEN] [Bug]: MCP 进程在重启后持续累积**
        - **问题:** 服务重启后旧 MCP 进程未被清理，导致进程堆积。
        - **状态:** 与 #4842 相关，可见 **#4849**。
        - **链接:** [#4834](https://github.com/agentscope-ai/CoPaw/issues/4834)
    - **#4818 [OPEN] [Bug]: Cron agent share_session=true 时执行轨迹为空**
        - **问题:** 定时任务在执行时 Agent 实际未运行。
        - **状态:** 已有修复 PR **#4822**。
        - **链接:** [#4818](https://github.com/agentscope-ai/CoPaw/issues/4818)
    - **#4811 [OPEN] [Bug]: 内联 source URL 导致上下文压缩失败**
        - **问题:** 特定格式的多媒体消息会导致 `AttributeError`。
        - **状态:** 已有修复 PR **#4820**。
        - **链接:** [#4811](https://github.com/agentscope-ai/CoPaw/issues/4811)

- **低严重/配置类:**
    - **#4835 [OPEN] [Bug]: jobs.json 中一个无效的 job 导致整个工作区无法启动**
        - **链接:** [#4835](https://github.com/agentscope-ai/CoPaw/issues/4835)
    - **#4839 [OPEN] [Bug]: Windows pip 升级导致残留 ghost 技能目录**
        - **链接:** [#4839](https://github.com/agentscope-ai/CoPaw/issues/4839)

---

#### 6. 功能请求与路线图信号

今日的新功能请求显示出社区对 **项目管理能力**、**交互精细度** 和 **性能优化** 的强烈渴望。

- **项目管理与对话控制:**
    - **#4789 [已关闭] 对话删除和回退:** 强烈需求，期望 Agent 能像 IDE 一样管理项目文件。
    - **#4843 [OPEN] 可配置的聊天模式 (打断/排队/插入):** 用户希望与 Agent 的交互模式更可控。
- **用户界面与体验:**
    - **#4830 [OPEN] 桌面端路径自动生成可点击链接:** 微小但影响效率的改进，可提升桌面端用户体验。
    - **#4840 [OPEN] 对话窗口思考强度选择器:** 希望能在 UI 中直接控制模型的思考深度，无需改配置文件。
- **性能与架构:**
    - **#4836 [OPEN] 工具定义按需加载以减少 Token 开销:** 用户明确指出了当前架构中工具定义占用了大量初始上下文 Token 的问题，这是一个极具价值的技术优化方向，有望显著降低成本。这是技术债务信号。
- **生态与渠道:**
    - **#4831 [OPEN] 预置常用包到 Docker 镜像:** 用户希望在官方 Docker 镜像中预装 `psycopg2`、`pytz` 等常用库，以提升开箱即用的体验。
    - **#4838 [OPEN] 抑制工具调用后的最终文本回复:** 允许“静默”执行工具，适用于只需要工具输出结果的场景。
    - **#4841 [OPEN] 新的 Skill 提案 (Before You Build Skill):** 社区贡献者提交了一个让 Agent 在编码前先做设计评审的 Skill。

---

#### 7. 用户反馈摘要

从今日的 Issue 和评论中，我们可以看到用户正处于 **从新功能的兴奋期过渡到生产环境的稳定期** 和 **对深度控制能力的需求爆发期**。

- **痛点与不满意:**
    - **稳定性问题:** `#4837` 报告的 v1.1.9 高频 `fallback` 回复是最严重的负面体验，因为它直接破坏了对话的可用性。用户反馈语气较为失望。
    - **高级配置门槛高:** 用户在配置 `reasoning_effort` (`#4814`)、自定义技能 (`#4808`) 时遇到困难，说明相关文档或 UI 设计不够直观。
    - **Windows 体验差:** `#4832` (CMD 窗口闪烁) 和 `#4829` (同样问题) 表明 Windows 平台的细节优化不够到位，对日常使用造成了直接干扰。
    - **资源管理隐忧:** `#4842` 和 `#4844` 的提出者可能是有大规模部署倾向的用户，对资源消耗和系统稳定性非常敏感。

- **满意与期待:**
    - **高度参与与贡献:** 用户不仅仅是提出问题，还积极参与讨论，并提出了具体的功能方案 (`#4841` Skill 提案) 和性能优化方向 (`#4836` 工具按需加载)，社区呈现出良好的共建生态。
    - **对核心能力的认可:** 用户希望 QwenPaw 能具备 Trae 等产品的部分能力 (`#4789`)，这表明他们认可 Agent 编程这个核心方向，并希望它变得更强大、更可控。

---

#### 8. 待处理积压

一些具有长期价值的问题或 PR 仍未得到维护者足够关注。

1. **#4433 [OPEN] [Under Review] Add token usage info output in each conversation**
    - **创建:** 2026-05-15
    - **摘要:** 一个非常有价值的 PR，为每个对话添加 Token 使用统计，这对用户控制成本至关重要。
    - **状态:** 开放超过两周，处于“正在审查”状态，但无后续评论。建议维护者尽快推进。
    - **链接:** [#4433](https://github.com/agentscope-ai/CoPaw/pull/4433)

2. **#4846 [OPEN] [WIP] refactor: migrate agentscope from version 1.x to 2.0.0**
    - **创建:** 2026-06-01
    - **摘要:** 一个重大的底层框架迁移 PR。虽然刚刚创建，但作为 WIP 需要维护者关注规划。
    - **状态:** 刚刚创建，需明确迁移计划和可能带来的 Breaking Changes。
    - **链接:** [#4846](https://github.com/agentscope-ai/CoPaw/pull/4846)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，这是为您生成的 ZeptoClaw 项目动态日报。

***

**ZeptoClaw 项目日报 | 2026年6月1日**

分析师： AI 智能体与个人 AI 助手领域开源项目分析师
数据源： GitHub (qhkm/zeptoclaw)
数据日期： 2026-05-31

---

### 1. 今日速览

过去24小时内，ZeptoClaw项目活动极少，处于极低活跃度状态。项目仅处理了一项由外部自动化流程触发的安全扫描工单（#609），该工单已被关闭，表明项目在安全合规层面进行了一次按需的、基础设施层面的审计。截至目前，项目无新版本发布、无待合并或活跃的Pull Request，也无新的功能请求或Bug报告。整体来看，项目在昨日处于“维护与观望”阶段，未见功能性推进或社区涌现活跃讨论。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

昨日项目未合并或提交新的 Pull Request。项目的主要“进展”体现在完成了一次针对代码库的安全扫描任务（Issue #609）。

- **安全与基础设施加固**： 关闭了 Issue #609，该工单旨在对当前代码库进行一次“Codex安全扫描”，重点关注“Webhook请求身份准入与路由”流程。尽管这是一次性扫描任务而非代码交付，但其完成意味着项目针对准入与路由组件的安全面进行了一次正式审查，可以被视为一项基础设施清理工作。
    - 相关 Issue： [qhkm/zeptoclaw Issue #609](https://github.com/qhkm/zeptoclaw/issues/609)

### 4. 社区热点

昨日项目中唯一活跃的讨论点是 Issue #609。尽管其性质是自动化安全扫描请求，但获得了一条评论（来自维护者），表明对扫描结果的确认或处理。该 Issue 迅速被关闭，说明这是一个目标明确、响应迅速的内部或协作检查。

- **关注点**： Webhook请求身份路由的安全风险。
- **链接**： [qhkm/zeptoclaw Issue #609](https://github.com/qhkm/zeptoclaw/issues/609)

### 5. Bug 与稳定性

昨日无新报告的 Bug、崩溃或回归问题。项目稳定性在数据层面未见负面信号。

### 6. 功能请求与路线图信号

昨日无新功能请求。项目路线图信号不明朗，当前无公开迹象表明下一版本将包含哪些具体功能。

### 7. 用户反馈摘要

昨日未从 Issue #609 的评论中提炼出典型的终端用户反馈。该 Issue 主要由维护者或自动化系统驱动，其反馈更偏向于开发运维层面的安全协作满意度。

### 8. 待处理积压

当前无长期未响应的重要 Issue 或 PR 积压。所有活跃 PR 和 Issues 均已闭环。**分析师备注**：Zero PRs 和 Zero 活跃 Issues 的状态，虽然在短期内表明项目稳定无突发故障，但长期来看，对于开源项目而言，这可能暗示社区参与度或新功能开发进入了平台期，需要关注后续的贡献者动态。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 (2026-06-01)

## 1. 今日速览
在过去 24 小时内，ZeroClaw 项目展现出极高的迭代强度，共有 **30 条 Issue** 和 **50 条 PR** 获得更新。尽管无正式版本发布，开发重心正聚焦于 v0.8.0 系列的最后冲刺，特别是 **`zerocode` 全新 TUI 客户端**的集成（#6848）以及**智能硬件（ESP32）** 的创新性探索（#7045~#7048）。社区讨论热度围绕 **Provider 架构统一**（#5937）与**多租户安全**（#5982）展开，但新报出的多个 S1 级严重 Bug（TUI 死锁、文件描述符崩溃）也为项目整体稳定性敲响了警钟。

## 2. 版本发布
无新版本发布。

## 3. 项目进展 (Merged/Closed PRs 与关键推进)

### 已合并/关闭的 PR
- **核心渠道修复：**
  - [#6999](https://github.com/zeroclaw-labs/zeroclaw/issues/6999) (Closed): 修复了 Telegram 语音转录因 `transcription_provider` 别名未正确配置而始终失败的问题。
  - [#7032](https://github.com/zeroclaw-labs/zeroclaw/issues/7032) (Closed): 修复了 WhatsApp Web 群聊中 `mention_only` 模式对 LID JID 提及不响应的问题。
  - [#7033](https://github.com/zeroclaw-labs/zeroclaw/issues/7033) (Closed): 修复了 Media Pipeline 在 Vision Provider 可用时，图片注解仅输出文本占位符而丢失内联图片数据的 Bug。
- **架构与构建体验：**
  - [#7044](https://github.com/zeroclaw-labs/zeroclaw/pull/7044) (Merged): 重构了 Cargo 特性项，提取出 `channels-all` 聚合特性，优化了编译模型和依赖管理。
- **TUI 前端体验：**
  - [#7029](https://github.com/zeroclaw-labs/zeroclaw/pull/7029) (Merged): 修复了 `zerocode` TUI 在初始化设置完成后，空白状态不自动刷新的体验问题。

### 关键开放 PR 进展
- [#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848) (Open): 核心集成 PR，引入 `zerocode` TUI、RPC Socket 传输和新的 Approval 机制。目前正在寻求首轮社区反馈，目标是作为 v0.8.0-beta-2 的基准。
- [#7045~7048](https://github.com/zeroclaw-labs/zeroclaw/pull/7045) (Hardware Series): Rhoahndur 提交了一系列智能房间（ESP32）PR，对应 Hackathon 项目，标志着项目向 IoT/硬件控制领域的正式扩张。

## 4. 社区热点

- **[#5937] Provider 统一重构 —— 架构之痛已成共识**：该 Issue 由核心贡献者发起，收获了 **9 条**评论。当前 `providers` 模块中 `reqwest` 客户端管理混乱、模型参数构造不一致的问题被深度暴露。社区普遍认为这是当前最制约插件化发展的技术债，诉求集中在消除配置碎片化。
- **[#5982] 多租户 RBAC —— 企业级安全诉求觉醒**：用户 `metalmon` 提出的“发送者 RBAC” **（8 条评论）**引发了强烈共鸣。在单一实例下隔离客户/运维/操作员权限被明确提及，这是项目从个人实验性工具迈向企业级平台的关键信号。
- **[#5847] 文档缺失的连锁反应**：关于 `gateway.web_dist_dir` 配置的文档缺失引发了 8 条讨论，迫使团队迅速修复并关闭 Issue。这反映出用户对清晰部署文档的渴求，文档是一种关键的功能属性。
- **[#7037] Discord 社区入口断裂**：最尴尬的热点——用户 `mn13` 发现 README 中的 Discord 邀请链接已失效。对于一个开源项目，社区入口的可靠性是第一道生命线，此 Issue 的严重性应被立刻拔高。

## 5. Bug 与稳定性

### S1 (严重 — 工作流阻塞)

| ID | 描述 | 状态 |
|---|---|---|
| [#7043](https://github.com/zeroclaw-labs/zeroclaw/issues/7043) | [NEW] `zerocode` TUI 在守护进程关闭/重启后永久失去响应，无法重连。 | **⚠️ 无修复 PR** |
| [#7042](https://github.com/zeroclaw-labs/zeroclaw/issues/7042) | [NEW] 守护进程 IPC 因文件描述符耗尽（EMFILE）崩溃。 | **⚠️ 无修复 PR** |
| [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038) | [NEW] `zeroclaw check` Websocket 健康检查在配置有效时仍返回 401。 | **⚠️ 无修复 PR** |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | [持续] Gemini CLI OAuth 认证完全失败（P1）。 | **ACCEPTED 但长期未修复** |
| [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | [持续] Ollama Provider 在需要调用工具时导致整个会话阻塞。 | In Progress |
| [#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155) | [持续] Delegate Agent 完全忽略全局 `[skills].prompt_injection_mode` 配置。 | In Progress |
| [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | [已修复] Cron 任务输出未被路由到配置频道。 | ✅ Closed |

### S2 (主要功能受损)

| ID | 描述 | 状态 |
|---|---|---|
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | [持续] `web_fetch` 的 SSRF 防护形同虚设 — `allowed_private_hosts` 对解析为内网 IP 的域名无效。 | **P1, In Progress** |
| [#6965](https://github.com/zeroclaw-labs/zeroclaw/issues/6965) | [已修复] Canvas 页面无法实时接收 Web UI Chat 的推流数据。 | ✅ Closed |

### S3 (轻微)

| ID | 描述 |
|---|---|
| [#7037](https://github.com/zeroclaw-labs/zeroclaw/issues/7037) | [NEW] README 中的 Discord 邀请链接失效。 |

## 6. 功能请求与路线图信号

### 短期纳入（v0.8.x 信号明确）
- **zerocode TUI 正式化**： `#6848`（集成 PR）和 `#6822`（加入构建矩阵）表明新一代终端界面将随 v0.8 正式发布。
- **智能硬件初探**： `#7045~#7048` 系列 PR 为 ESP32 提供了工具支持，这可能预示着 ZeroClaw 将进军边缘计算与物联网控制领域。
- **Email 渠道重大升级**： `#7021` 实现了 XOAUTH2 认证、Observer 模式及只读 IMAP 工具，补足了企业级邮箱集成的短板。
- **静态输出模态偏好**： `#7020` 允许在配置文件中为特定 Peer 指定始终输出 TTS 或文本，满足特定场景的硬性需求。

### 中远期路线图信号
- **[#4467] MCP 深度集成**：社区投票最高（👍 4）的 Feature Request。用户不满足于仅做 MCP 工具调用客户端，强烈要求支持 MCP **Resource** 和 **Prompt** 端点。
- **[#6720] 死代码治理**：用户发现 `context_aware_tools` 字段完全不被读取。这是一个对用户承诺的缺失，预计会在未来的 Skills 重构中被修复或剥离。
- **[#3100] Mattermost Oncall 模式**：企业协作场景的老牌诉求，长期处于 `in-progress` 但进展缓慢。

## 7. 用户反馈摘要

- **满意点**：
  - 社区高度认可项目在 **Telegram、WhatsApp 和 Media Pipeline** 方向的 Bug 修复速度（#6999, #7032, #7033）。
  - 对 **Hardware (ESP32)** 方向的新尝试表示惊喜和期待。
- **主要痛点**：
  - **稳定性信任危机**： “`zerocode` TUI 只要守护进程崩溃或重启一次就永久 ‘死’ 掉，开发调试时根本没法用。” —— singlerider (#7043)
  - **配置欺骗感**： “`context_aware_tools` 这个配置项是骗人的。我设了 true 但代码里根本没读它。要么修好，要么删掉它。” —— nick-pape (#6720)
  - **社区入口断裂**： “Discord 链接坏了，我加不了社区。” —— mn13 (#7037)
  - **Provider 割裂体验**： 不同 Provider（Ollama / Gemini / Bedrock）之间的行为差异和工作流阻断（#5962, #5289, #4879）让用户感到沮丧，统一的架构重构（#5937）呼声极高。

## 8. 待处理积压

| ID | 标题 | 优先级评估 | 备注 |
|---|---|---|---|
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | web_fetch SSRF 保护绕过 | **🔥 高（安全漏洞）** | 标记为 `in-progress` 已超过 60 天。在 SSRF 面前没有中间状态，必须加速。 |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | Gemini CLI OAuth 失败 | **🔥 高（生态依赖）** | P1 级别阻塞超过 60 天，直接影响 Google 云生态用户的留存。 |
| [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | Ollama 工具调用崩溃 | **🔥 高（本地部署核心）** | 本地模型场景的核心 Bug，建议社区明确 `in-progress` 下的具体修复排期。 |
| [#3100](https://github.com/zeroclaw-labs/zeroclaw/issues/3100) | Mattermost Oncall 模式 | **🟡 中（企业场景）** | 企业级用户刚需，长期无人认领。如果没有项目组排期，建议明确标注 `help wanted` 请求外部贡献。 |
| [#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) | MCP Resource & Prompt 支持 | **🟡 中（生态扩展）** | 社区最强呼声（👍 4），但深度绑定架构改动。若 v0.8 发布后仍无进展，建议在路线图中明确 Post-MVP 排期。 |

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*