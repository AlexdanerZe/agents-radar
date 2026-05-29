# OpenClaw 生态日报 2026-05-29

> Issues: 373 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-29 02:54 UTC

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

# OpenClaw 项目动态日报 — 2026-05-29

## 1. 今日速览

过去 24 小时，OpenClaw 项目保持高强度迭代：共处理 **373 条 Issue 更新**（新开/活跃 176，关闭 197）和 **500 条 PR 更新**（待合并 337，合并/关闭 163），净关闭量显著，维护管线运转高效。连续发布 **v2026.5.27**（稳定版）与 **v2026.5.27-beta.1**，主要强化安全边界与内容隔离。然而社区焦点高度集中在 **native hook relay 在 5.26 版本后频繁不可用** 的严重回归，多起 Issue 获大量关注，修复状态尚不完全一致。项目整体健康度良好，版本节奏快，但稳定性类 Issue 占比上升，需持续跟踪关键回归。

## 2. 版本发布

### v2026.5.27 & v2026.5.27-beta.1（双版本同步发布）

- 发布链接：[v2026.5.27](https://github.com/openclaw/openclaw/releases/tag/v2026.5.27) ｜ [v2026.5.27-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.5.27-beta.1)
- **主要更新（Highlights）**：
  - **安全与内容边界强化**：将 group prompt 文本从系统提示中剥离，防止信息外溢；
  - **主机名规范化**：对含重复点号（`.`）的 hostname 进行标准化处理；
  - **命令包装阻断**：拦截具有副作用命令包装器以及对不安全的 Node 运行环境变量覆写；
  - **认证强制**：拒绝未经身份验证的 Tailscale 暴露；
  - **角色授权改进**：节点与设备角色的审批逻辑增强。
- **破坏性变更/迁移注意**：本次发布未明确标注破坏性变更，但 group prompt 行为变化可能影响依赖系统提示上下文的插件或自定义配置。建议用户升级后全面测试 agent 响应，并确认 Tailscale 暴露配置已含认证。

## 3. 项目进展

今日合并/关闭的重要 PR 及所推动的功能修复：

| PR | 关键内容 | 状态 |
|----|---------|------|
| [#79028](https://github.com/openclaw/openclaw/pull/79028) | fix(auto-reply): 保留嵌入式直接运行中插件的 tools.allow | ✅ 已合并 |
| [#87664](https://github.com/openclaw/openclaw/pull/87664) | fix(feishu): 为渠道运行时未初始化增加防御性检查，修复飞书静默丢消息 | ✅ 已关闭 |
| [#87849](https://github.com/openclaw/openclaw/pull/87849) | feat: 新增 `codex-supervisor` 插件，提供 endpoint 探测、session 列表/转录/中断控制 | ✅ 已关闭 |
| [#87810](https://github.com/openclaw/openclaw/pull/87810) | fix(gateway): 清除已完成会话的活动运行记录，由 ClawSweeper 自动合并 | 🚀 待自动合并 |

同时，多个关键 Issue 成功关闭，如 **native hook relay 回归**（[#87331](https://github.com/openclaw/openclaw/issues/87331)、[#87395](https://github.com/openclaw/openclaw/issues/87395)）以及 **预压紧死锁**（[#87736](https://github.com/openclaw/openclaw/issues/87736)），验证了部分紧急修复已落地。项目在 **Chat UI、Telegram 渠道、飞书渠道、DeepSeek 兼容、语音模型编排** 等方向均有 PR 推进，代码库在功能广度和稳健性上持续提升。

## 4. 社区热点

今日讨论最活跃、关注度最高的 Issues（按评论数排序）：

| Issue | 标题 | 评论数 | 👍 数 | 链接 |
|-------|------|--------|-------|------|
| **#87331** | [CLOSED] 5.26 regression: "Native hook relay unavailable" after relay re-register due to generation UUID staleness | **17** | **10** | [查看](https://github.com/openclaw/openclaw/issues/87331) |
| **#87395** | [CLOSED] Native hook relay intermittently becomes unavailable on 2026.5.26, blocking memory/filesystem tools | **14** | **8** | [查看](https://github.com/openclaw/openclaw/issues/87395) |
| **#86599** | [OPEN] Local model provider calls thread block gateway event loop on Windows beta; trivial infer takes ~4 min | **13** | 1 | [查看](https://github.com/openclaw/openclaw/issues/86599) |
| **#69208** | [OPEN] Umbrella: duplicate transcript, replay, and context assembly across channels | **12** | 0 | [查看](https://github.com/openclaw/openclaw/issues/69208) |
| **#73148** | [OPEN] Image tool: opaque "Failed to optimize image" when sharp is not installed | **11** | 3 | [查看](https://github.com/openclaw/openclaw/issues/73148) |

**分析**：社区首要关注点是 **2026.5.26 引入的 native hook relay 可靠性问题**，#87331 与 #87395 共收到 18 个 👍，反映大量用户遭遇工具调用阻断。该问题虽已在今日关闭（可能通过私有修复），但新的同类报告 [#87536](https://github.com/openclaw/openclaw/issues/87536)（评论 6，👍2）仍在出现，提示修复可能未完全覆盖所有场景。此外 Windows 本地模型阻塞 (#86599) 虽关注人多但赞数低，表明该问题影响面较特定。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug（含回归、崩溃、稳定性问题），并标注相应 fix PR 情况：

### 🔴 严重（核心功能阻断）

- **Native hook relay 持续不可用**（[#87536](https://github.com/openclaw/openclaw/issues/87536) – OPEN）：5.26 上 relay bridge 从不启动，所有原生工具全部失败。尚无直接关联 fix PR。
- **Codex 预压紧后仍出现 Missing Codex thread 失败**（[#87736](https://github.com/openclaw/openclaw/issues/87736) – CLOSED）：5.27 上复现 #86211 修复后的残留问题，已关闭（可能刚合并额外修复）。
- **飞书渠道升级后无法派发消息**（[#87646](https://github.com/openclaw/openclaw/issues/87646) – OPEN）：5.27 版本出现 `TypeError: Cannot read properties of undefined (reading 'run')`。已有 Fix PR [#87664](https://github.com/openclaw/openclaw/pull/87664)（已关闭）。
- **WhatsApp 群组后续 @提及被静默忽略**（[#87609](https://github.com/openclaw/openclaw/issues/87609) – OPEN）：5.26 回归，仅首个提及可触发回复。暂无 fix PR 标注。

### 🟡 中等（功能降级）

- **Agent 在 Telegram 上重复回复 2–10 次**（[#86519](https://github.com/openclaw/openclaw/issues/86519) – OPEN）：5.20 更新后出现，5.22 缓解但仍未根治。暂无 fix PR。
- **Cron 任务在 MiniMax 503 时失败，但手动触发成功**（[#85888](https://github.com/openclaw/openclaw/issues/85888) – OPEN）：推测是 OpenClaw 调度而非 API 问题。已有 queueable-fix 标签，但无专属 PR。
- **Control UI 会话选择器按钮因 blur/click 竞态失效**（[#87554](https://github.com/openclaw/openclaw/issues/87554) – CLOSED）：已通过修复关闭。

### 🟢 低影响/边缘

- **Mattermost block streaming 编辑单条帖子而非分多条发送**（[#87322](https://github.com/openclaw/openclaw/issues/87322) – OPEN）
- **Matrix 线程回复退化为普通回复**（[#87307](https://github.com/openclaw/openclaw/issues/87307) – OPEN）
- **Doctor 显示 Gateway auth SecretRef 不可用但实际可解析**（[#77687](https://github.com/openclaw/openclaw/issues/77687) – OPEN）

## 6. 功能请求与路线图信号

### 有望进入下一版本的新功能（已有实装 PR）

| PR | 功能 | 状态 | 路线图信号 |
|----|------|------|-----------|
| [#87845](https://github.com/openclaw/openclaw/pull/87845) | 添加 Fal Krea 图像模型 schema（native aspect_ratio 等） | OPEN | 扩大生图模型生态覆盖 |
| [#87469](https://github.com/openclaw/openclaw/pull/87469) | 核心会话目标（session goals）—— 持久化、可挂起、预算限制 | OPEN | 引入目标驱动型会话管理 |
| [#87849](https://github.com/openclaw/openclaw/pull/87849) | Codex Supervisor 插件 —— 工具化 Codex App-server 管控 | CLOSED | 强化 Codex 可观测性与运维能力 |
| [#86210](https://github.com/openclaw/openclaw/pull/86210) | 多槽位记忆角色架构（memory.recall / compaction / capture 等） | OPEN | 记忆系统模块解耦，允许多记忆插件并存 |
| [#87794](https://github.com/openclaw/openclaw/pull/87794) | 通过 providers 实现语音模型目录（TTS/实时转写/语音） | OPEN | 标准化语音能力接入 |
| [#86155](https://github.com/openclaw/openclaw/pull/86155) | GitHub Copilot agent runtime 插件 | OPEN | 拓展 Agent 后端选择 |

### 用户需求信号（来自 Issues）

- **性能监控请求**：[#86231](https://github.com/openclaw/openclaw/issues/86231) 建议跟踪 Codex harness 的延迟开销，提示社区对 wrapper 路径效率的关注。
- **Doctor 关于 Node 路径误报**：[#60612](https://github.com/openclaw/openclaw/issues/60612) 要求 Doctor 不将 NVM node 标记为问题，持续有用户提出。
- **安全审计误报**：[#84376](https://github.com/openclaw/openclaw/issues/84376) 指出 `secrets audit` 将 Codex sentinel key 误报为明文，影响自动化部署信任。

综上，项目路线图正在向 **模块化记忆架构、Codex 深层集成、语音标准化、Agent 后端多样化** 方向演进，同时社区对运维体验和性能透明度的需求开始增多。

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中提炼的真实用户反馈：

> *“After upgrading to 2026.5.26, codex tool calls intermittently fail with `Native hook relay unavailable`. Gateway restart fixes briefly, error returns.”* —— [#87331](https://github.com/openclaw/openclaw/issues/87331)
> *“Even a trivial fresh prompt like 'hi, how are you' takes ~4 minutes on Windows beta.”* —— [#86599](https://github.com/openclaw/openclaw/issues/86599)
> *“After updating from 2026.5.12 to 2026.5.20, the agent sends duplicate identical replies on Telegram (2-10x per user message). Upgrading to 2026.5.22 reduced severity but did not fully fix.”* —— [#86519](https://github.com/openclaw/openclaw/issues/86519)
> *“Running `openclaw doctor` restored the session. After that: `openclaw provider test openai-codex OK` – so the key was always present.”* —— [#83935](https://github.com/openclaw/openclaw/issues/83935)
> *“When a cron job finishes and its announce delivery sends to the same Telegram user, it triggers `EmbeddedAttemptSessionTakeoverError`.”* —— [#84583](https://github.com/openclaw/openclaw/issues/84583)

**满意度**：用户对安全更新接受度高，但连续版本（5.20→5.26）的稳定回归削弱了升级信任。Telegram 重复回复、Native relay 不可用等问题导致用户需手动回滚或重启。积极的方面是社区协作调查深入（如 [#87536](https://github.com/openclaw/openclaw/issues/87536) 报告者使用 AI 辅助分析），表明用户承诺度高。

## 8. 待处理积压

以下为长期未关闭、且仍然重要的 Issue / PR，提醒维护者重点关注：

### 积压 Issue（创建超过 30 天仍 OPEN，P1/P2）

| Issue | 标题 | 创建时间 | 影响 | 链接 |
|-------|------|---------|------|------|
| **#48003** | Steer mode does not inject messages mid-turn for main sessions | 2026-03-16 | session-state, message-loss | [查看](https://github.com/openclaw/openclaw/issues/48003) |
| **#54155** | Gateway memory leak 389MB → 14.7GB over 4 days | 2026-03-25 | crash-loop | [查看](https://github.com/openclaw/openclaw/issues/54155) |
| **#51593** | HTTP 400: "tool call id duplicated" with kimi-k2.5 in WhatsApp groups | 2026-03-21 | message-loss | [查看](https://github.com/openclaw/openclaw/issues/51593) |
| **#46252** | Cost dashboard omits .jsonl.reset archives, undercounting daily spend | 2026-03-14 | 费用错误 | [查看](https://github.com/openclaw/openclaw/issues/46252) |
| **#71491** | Kimi K2.6 reasoning_content 400 regression after long compaction | 2026-04-25 | session-state, auth-provider | [查看](https://github.com/openclaw/openclaw/issues/71491) |
| **#72015** | Active-memory blocks replies / QMD boot overloads multi-agent gateways | 2026-04-26 | crash-loop | [查看](https://github.com/openclaw/openclaw/issues/72015) |

### 积压 PR（创建超过 20 天、待审核或未合并）

| PR | 标题 | 创建时间 | 阻塞点 | 链接 |
|----|------|---------|-------|------|
| **#75336** | feat(compaction): add identifier survival validation after summarization | 2026-05-01 | 等待 proof / review | [查看](https://github.com/openclaw/openclaw/pull/75336) |
| **#78936** | fix #78919: ACP sessions_spawn doesn't route images to Codex native vision | 2026-05-07 | 等待 proof / review | [查看](https://github.com/openclaw/openclaw/pull/78936) |
| **#82887** | fix(cron): preflight model fallbacks before skip | 2026-05-17 | ready for maintainer look | [查看](https://github.com/openclaw/openclaw/pull/82887) |
| **#85572** | Policy: add sandbox posture conformance checks | 2026-05-23 | ready for maintainer look | [查看](https://github.com/openclaw/openclaw/pull/85572) |

这些积压项长期影响会话状态、内存稳定性和费用准确性，建议在下一版本周期优先处理。

---
*数据来源：OpenClaw GitHub Repository (github.com/openclaw/openclaw)，采集时间 2026-05-29。*

---

## 横向生态对比

这是一份基于您提供的 2026-05-29 社区动态数据，为您生成的横向对比分析报告。

---

## 个人 AI 智能体开源生态横向对比分析报告（2026-05-29）

---

### 1. 生态全景

当前生态正经历“功能广度”与“可靠性深度”的剧烈碰撞。通用型平台（OpenClaw、Hermes Agent）在功能合并上狂飙突进，但伴随严重的回归问题，社区对“升级稳定性”的耐心正在耗尽。与此同时，以 Moltis、NanoBot 为代表的中型项目通过极高的 Bug 响应质量建立了差异化的信任壁垒。整个行业正在从“你能做什么？”向“你能稳定可靠地做好什么？”切换。此外，记忆管理、MCP 连接可靠性以及多供应商兼容性已成为所有项目的“标配焦虑点”，而非差异化优势。

---

### 2. 各项目活跃度对比

| 项目 | Issues 动态 | PR 动态 | 版本发布 | 活跃度/健康度 |
|---|---|---|---|---|
| **OpenClaw** | 176 新/活跃, 197 关闭 | 337 待合, 163 合并/关闭 | v2026.5.27 & beta.1 | **高吞吐，回归风险大** |
| **NanoBot** | 3 新, 7 关闭 | 8 合并, 12 待合 | 无 | **闪电战修复，健康** |
| **Hermes Agent** | 50 条更新 | 50 条更新 | v0.15.0 + v0.15.1 热修复 | **P0 日级恢复，极激进** |
| **IronClaw** | 33 条更新 | 50 条更新 (66% 合并) | 无 | **内部迭代极快，发布受阻** |
| **CoPaw (QwenPaw)** | 40 条更新 | 38 条更新 (20 合并) | 无 | **桌面端阵痛，核心 Agent 阻塞** |
| **LobsterAI** | 1 新 | 7 合并 | 无 | **功能密集交付，健康** |
| **ZeroClaw** | 20 条更新 (19 开放) | 34 条更新 (3 合并) | 无 | **合并率极低，3 个 S1 阻塞** |
| **Moltis** | 0 新 | 4 合并 | 无 | **Bug 歼灭战效率最高** |
| **NullClaw** | 0 新 | 7 合并 | 无 | **稳健推进** |
| **NanoClaw** | 5 更新 | 7 更新 | 无 | **路线图关键决策落地** |
| **PicoClaw** | 6 更新 | 9 有效, 23 待合 | Nightly | **审阅瓶颈严重** |
| **TinyClaw / ZeptoClaw** | 无活动 | 无活动 | 无 | **停滞** |

---

### 3. OpenClaw 在生态中的定位

**基准地位不变，但领导力面临挑战。** OpenClaw 仍然是生态中规模最大、覆盖面最广的“重型基础设施”。其安全更新（Group Prompt 隔离、Auth 强制）和渠道广度保持领先。

- **vs. Hermes Agent：** OpenClaw 是面向终端的自我托管服务器；Hermes 是面向工作流编排的平台。Hermes 通过 v0.15.1 的“当日热修复”证明了其敏捷性，而 OpenClaw 的 Native Hook 回归（#87331）暴露了其大型代码库的耦合困境。
- **vs. NanoBot：** OpenClaw 是“全栈操作系统”，NanoBot 是“轻量级内核”。OpenClaw 的优势在于即开即用，劣势在于升级风险高。NanoBot 通过稳定修复闪电战赢得了追求低运维成本的开发者。
- **核心风险：** 社区焦点集中于 5.26 版本的 Native Hook Relay 回归，尽管该问题已被标记关闭，但同类报告仍在涌现。如果不能根治这类高频回归，用户可能流向稳定性更好的二线项目。

---

### 4. 共同关注的技术方向

1.  **上下文与记忆管理（普遍性最高）：**
    - **涉及项目：** OpenClaw (#86599)、NanoBot (#4044/#4039)、Hermes (#34291)、ZeroClaw (#6361)、CoPaw (#4652)。
    - **诉求：** 用户不满足于简单的历史记录，而是要求“目标驱动型会话”（OpenClaw #87469）、“记忆提炼与回顾”（CoPaw #4652）和“永不遗忘的上下文裁剪”（NanoBot #4039）。Agent 失忆已成为所有项目的通用痛点。

2.  **渠道接入的可靠性：**
    - **涉及项目：** OpenClaw (飞书/WhatsApp)、CoPaw (OneBot)、ZeroClaw (Slack)、Moltis (Discord)、NanoClaw/NanoBot (WhatsApp/Telegram/MS Teams)。
    - **诉求：** 静默丢消息、重复回复、认证失效是普遍问题。用户要求“开箱即用”的渠道稳定性，而非仅仅追求渠道数量。

3.  **MCP/插件生态的连接健康：**
    - **涉及项目：** OpenClaw (Native Hook)、NanoBot (MCP 重连 #4027)、CoPaw (MCP 进程清理 #2066)、NanoClaw (MCP 凭据注入 #2636)。
    - **诉求：** 连接中断后无法自动恢复是最大槽点，其次是安全性（凭据暴露、PATH 穿越）。

4.  **去供应商锁定与模型编排：**
    - **涉及项目：** NanoClaw (#80 正式关闭)、IronClaw (Reborn Auth)、ZeroClaw (per-agent classifier #6945)、NullClaw (新增 NEAR AI)。
    - **诉求：** 用户要求“按任务分配模型”（廉价分类 + 强大推理），并且不因单一 API 的封禁或故障而全面停摆。

---

### 5. 差异化定位分析

| 项目 | 核心功能侧重 | 目标用户画像 | 架构哲学 |
|---|---|---|---|
| **OpenClaw** | 全功能 Agent 服务器，安全与渠道广度 | 重度用户、自托管运维者 | 单体式，高集成度 |
| **Hermes Agent** | 工作流编排与多 Agent 协作 | 平台开发者，需看板管理 | 服务化，看板/工作流优先 |
| **NanoBot** | 轻量级 Agent 核心，MCP 生态 | 个人开发者，嵌入式场景 | 模块化，极简主义 |
| **IronClaw** | 下一代身份认证与安全凭证 | Web3/企业级用户 | 身份驱动，零信任架构 |
| **CoPaw (QwenPaw)** | 桌面端 Agent 原生体验 | 桌面端用户，Qwen 生态开发者 | Tauri 外壳 + AgentScope 后端 |
| **ZeroClaw** | 可编程沙箱与高级安全策略 | 开发者，实验室用户 | 高度可配置，策略驱动 |
| **Moltis** | 自动化（Cron）、深度进程控制 | 高级 Devops，自动化运维 | 进程级控制（PTY/tmux） |
| **NanoClaw** | Claude Code/Anthropic 专属伴侣 | Anthropic 深度用户 | 补丁桥接 + 原生闭环 |
| **NullClaw** | 多提供商轻量中继 | 普通用户/多账户管理 | 简单、稳健、低耦合 |

---

### 6. 社区热度与成熟度分层

**Tier 1：高速迭代 / 功能扩张（高活跃，高波动）**
- **项目：** OpenClaw、Hermes Agent、IronClaw、CoPaw、LobsterAI
- **特征：** 日 PR 超 30 个，版本落地快，但回归风险高。依赖社区“自愈”和快速补丁文化。

**Tier 2：质量巩固 / 稳健演进（中活跃，高可靠）**
- **项目：** NanoBot、NullClaw、Moltis、NanoClaw
- **特征：** 合并质量高，Bug 响应时间短。拥有极强的核心贡献者（如 NanoBot 的 @hamb1y），社区满意度高。

**Tier 3：发展瓶颈 / 审阅积压（中低活跃，高阻塞）**
- **项目：** PicoClaw、ZeroClaw
- **特征：** 社区提交踊跃，但维护者审阅带宽不足。23+ 个有效 PR 长期待合（PicoClaw），严重 Bug 无官方回应（ZeroClaw S1），存在贡献者流失风险。

**Tier 4：低活跃 / 停滞**
- **项目：** TinyClaw、ZeptoClaw
- **特征：** 24 小时窗口内无任何活动。项目可持续性存疑。

---

### 7. 值得关注的趋势信号

1.  **“可靠性”已成为第一优先级：** Hermes 的“日级 P0 热修复”与 NanoBot 的“一次性关闭 5 个 Bug”证明，社区对频繁升级带来的断裂感极度不满。**开发者建议：** 在评估项目时，Bug Turn Around Time（Bug 响应时间）应比功能列表更重要。

2.  **记忆即护城河：** “会话目标”（OpenClaw）、“记忆提炼”（CoPaw）的提案已进入 PR 阶段。未来的 Agent 能力上限不再取决于模型参数，而取决于**信息持久化与关联检索的能力**。能够解决“会话失忆”的项目将获得用户粘性的代际优势。

3.  **成本可视化需求爆发：** 用户不再满足于黑盒推理。API 调用成本仪表盘（OpenClaw #46252）、Token 预算可视化（CoPaw #4782）的呼声高涨。这标志着社区正在从“技术尝鲜”转向“生产级经济核算”。

4.  **去中心化身份与 Agent 的结合（Web3 影响）：** IronClaw 的 Reborn SSO（支持 NEAR 钱包）揭示了将私钥管理直接集成到 Agent 生命周期中的可能性。这是一个新兴趋势：**让 Agent 拥有独立的身份和加密钱包**，以实现真正的自主交易和授权。

5.  **桌面端与边缘计算回潮：** CoPaw 在 Windows 端的阵痛（启动速度、PATH 问题）与 PicoClaw 在 RISC-V 架构的深耕表明，随着 API 成本波动和隐私意识增强，**本地推理与离线 Agent 能力**正在从备选变为必需。

**总结对开发者的建议：**
- 如果你追求**开箱即用的稳定性**，建议优先关注 **Tier 2**（如 NanoBot、Moltis）。
- 如果你需要**最全的功能和渠道**，选择 **OpenClaw**，但务必建立“保守升级策略”（跳过中间回归版本）。
- 如果你在构建**商业化产品/工作流**，请密切跟进“记忆”与“成本管理”方向的 PR 落地。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot (HKUDS/nanobot) 数据生成的 2026-05-29 项目动态日报。

---

# NanoBot 项目动态日报 | 2026-05-29

## 1. 今日速览

过去 24 小时，NanoBot 项目处于**极高强度开发与密集修复期**，共计 20 条 PR 与 10 条 Issue 更新，显示了极佳的项目活跃度与社区参与度。核心贡献者 **@hamb1y** 主导了一场“稳定性闪电战”，一次性完成并合并了 5 个高难度 Bug 的修复（并发调度、上下文预算、流重试等）。与此同时，WebUI、扩展生态、Agent 协议标准（GitAgent）等重量级特性仍在稳步推进（共 12 个 PR 待合并）。虽然没有正式版本发布，但代码库的“内功”在今日获得了显著提升。

- **数据亮点：**
  - 24h PR 更新：20 条（合并/关闭 8 条，待合并 12 条）
  - 24h Issues 更新：10 条（新开/活跃 3 条，关闭 7 条）
  - 版本发布：0 个


## 2. 版本发布

无


## 3. 项目进展

今日项目的关键进展集中于**稳定性修复、架构精简与核心功能增强**。

- **🔥 重大稳定性修复（里程碑式）：**
  - **PR #4041** **[已合并]**：一次性关闭了 5 个严重 Bug（#4036, #4037, #4038, #4039, #4040），覆盖了 **任务队列覆盖、共享可变上下文、流式重试导致输出重复、上下文裁剪预算算错、`/stop` 命令失效**等最棘手的并发与资源管理问题。这代表了项目内部质量的一次重大飞跃。
  - **PR #4027** **[待合并]**：修复了 MCP 连接中断后无法重连的致命缺陷（`_mcp_connected` 状态未重置）。
  - **PR #4017** **[待合并]**：修复了部分兼容 OpenAI 接口的 Provider（如小米 MiMo）返回纯文本 `tool_calls` 时解析失败的问题。

- **架构演进与重构：**
  - **PR #4023** **[已合并]**：将独立的 `HeartbeatService` 后台循环迁移为基于 Cron 的自动注册服务，精简了基础设施代码。
  - **PR #4015** **[已合并]**：实现了 Agent Loop 的观察-反思机制（Observation-Reflection Prompt），让 Agent 能在执行工具后以最小代价实现“思考-验证-通知用户”的自循环。
  - **PR #3990** **[待合并]**：对 `Dream` 模块进行大规模重构，用轻量级 Cron 替代原有的两阶段繁重类（~315行）。

- **WebUI 与体验增强：**
  - **PR #4007** **[已合并]**：为 WebUI 增加了类似 Codex 风格的项目工作区（Project Workspaces）与访问控制，使项目管理更贴近文件系统。
  - **PR #3937** **[已合并]**：新增危险命令执行前的“用户确认”机制，提升了 `exec` 技能的安全性。
  - **PR #4031** **[已合并]**：为 Discord 通道添加了原生 `/model` 命令，方便用户在聊天中直接切换模型预设。

- **开放标准与生态：**
  - **PR #4034** **[待合并]**：作为 PR #4030 的改进版本重新提交，推动 **GitAgent 协议**（GAP）的集成。


## 4. 社区热点

1. **🧠 短期记忆丢失 (Issue #4044)**
   - [链接](https://github.com/HKUDS/nanobot/issues/4044)
   - **热度：** 创建不到 24 小时即获 3 条评论，直击 Agent Loop 核心痛点。
   - **诉求：** 用户描述了系统提示词（SOUL.md, MEMORY.md）挤压窗口、上下文管理不当导致 Agent 一问就忘的“失忆症”。这是当前最突出的可用性 Bug，社区正在等待根治方案。

2. **📊 社区自建 Web 面板 (Issue #1922)**
   - [链接](https://github.com/HKUDS/nanobot/issues/1922)
   - **热度：** 获 10 个 👍 和 12 条评论，Issue 虽关闭，但讨论热度不减。
   - **诉求：** 用户 **@Good0007** 展示了自建的全功能自托管面板，涵盖了 Dashboard、聊天、MCP 配置、Cron 等。这反映了社区对“好用的可视化配置界面”的强烈渴望，以及对项目未来生态化的期待。

3. **🔌 MCP 连接可靠性 (PR #4027)**
   - [链接](https://github.com/HKUDS/nanobot/pull/4027)
   - **热度：** 核心基础设施 PR，关注度持续高涨。
   - **诉求：** 所有使用 MCP 扩展用户对连接稳定性的迫切需求。断线后无法恢复是影响日常使用体验的硬伤。

4. **🧩 上下文预算与灵活性 (Issues #4039, #4043, #2772)**
   - **诉求：** 用户在讨论中普遍反映出对**上下文窗口更精细控制**的需求。无论是微信的 10 条消息限制，还是文档强制注入对工作流的干扰，亦或是工具 Token 预留的逻辑 Bug，都指向了资源调度的灵活性问题。


## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 状态 | 描述 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **🔥 致命** | #4044 | 开放 | **短期记忆丢失**：上下文管理失效，Agent 无法执行连贯对话。 | 当前最严重可用性问题，急需排查。 |
| **高** | #4040 | 已修复 | `/stop` 无法终止 `unified_session` 中的任务。 | 被 PR #4041 修复 |
| **高** | #4036 | 已修复 | 任务队列覆盖导致活跃轮次消息丢失。 | 被 PR #4041 修复 |
| **高** | #4038 | 已修复 | 流式输出失败的请求重试后，用户端收到重复输出。 | 被 PR #4041 修复 |
| **高** | #4039 | 已修复 | 上下文裁剪时未保留工具 Schema 的 Token 空间。 | 被 PR #4041 修复 |
| **高** | #4037 | 已修复 | 长任务与 Goal 工具因共享可变上下文导致并发错乱。 | 被 PR #4041 修复 |
| **中** | #4042 | 开放 | Matrix 通道 E2EE 设备验证问题，导致 Element X 客户端持续报“未验证设备”。 | 影响特定用户群 |
| **中** | PR #4047 | 开放 | MS Teams 通道未验证 `activity.serviceUrl`，存在安全风险。 | 安全修复 PR 待合 |
| **低** | #4043 | 开放 | 无法禁用文档自动提取，与既有工作流冲突。 | 提有增强提案 |


## 6. 功能请求与路线图信号

- **极有可能纳入下版本：**
  - **WebUI 上下文窗口配置 (PR #4045)**: 允许用户在 UI 上直接选择 64K 或 256K 上下文窗口，直接回应用户对灵活性的需求。
  - **扩展插件注册表 (PR #4046)**: 引入外部扩展源，标志着 NanoBot 开始构建插件生态。
  - **DingTalk 群聊用户隔离 (PR #4016)**: 针对中国用户普遍需求的精确响应。
  - **禁用文档提取 (Issue #4043 / PR 方向)**: 被标记为 `good first issue`，任务清晰，方便新贡献者接入。

- **远期路线图信号：**
  - **跨 Agent 协作 (PR #3992)**: 实现了多 Agent 实例间的消息总线，是迈向“Agent 集群”的关键架构。
  - **GitAgent 协议 (PR #4034)**: 拥抱开放标准，让 NanoBot 的 Agent 配置文件（SOUL.md, agent.yaml）具备可移植性。
  - **注册表驱动配置 (PR #3994)**: 让 Provider 的配置字段能通过后端注册自动渲染到前端 UI，极大提升扩展 Provider 的体验。


## 7. 用户反馈摘要

- **正面/积极：**
  - **强有力的社区贡献者：** 以 **@hamb1y** 和 **@Re-bin** 为代表的用户深度阅读源码，批量修复并发 Bug 并贡献 WebUI 重磅特性，显示了项目拥有极高技术素养的核心贡献者群体，项目生态健康。
  - **创作热情高涨：** 用户 **@Good0007** 为项目开发了独立的 Web 面板，社区共建意愿极强。

- **负面/痛点：**
  - **“一问就忘” 是最大痛点 (Issue #4044):** 用户报告 Agent 在单轮对话中逐步丧失上下文记忆，严重阻碍了实际使用。
  - **强制行为缺乏灵活性 (Issue #4043):** 文档自动提取功能与用户自定义的 OCR 工作流冲突，用户直言“不需要这个注入 (this injection is unnecessary)”。
  - **特定渠道体验受限 (Issue #2772, #4042):** 微信消息条数限制和 Matrix E2EE 兼容性问题，阻碍了部分重度用户将该平台作为主力通信渠道。


## 8. 待处理积压

总体来看，NanoBot 维护者响应速度极快，无严重积压现象。以下为需要核心维护者关注、评估或加速 Review 的重点工作项：

1. **PR #4027 - MCP 重连修复**：目前最影响基础设施稳定性的未合 Patch。
   - [链接](https://github.com/HKUDS/nanobot/pull/4027)
2. **PR #3992 - Agent 协作**：重量级特性，Review 周期较长，等待决策，决定了下半年路线图方向。
   - [链接](https://github.com/HKUDS/nanobot/pull/3992)
3. **Issue #4044 - 短期记忆丢失**：当前最严重的用户体验 Bug，建议优先分配资源跟进。
   - [链接](https://github.com/HKUDS/nanobot/issues/4044)
4. **PR #4047 - MS Teams 安全修复**：安全漏洞修复，建议提升合并优先级。
   - [链接](https://github.com/HKUDS/nanobot/pull/4047)
5. **PR #3994 - 注册表驱动配置**：架构性重构，涉及面广，但长期收益巨大，需尽快决策。
   - [链接](https://github.com/HKUDS/nanobot/pull/3994)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

### Hermes Agent 项目动态日报 — 2026年5月29日

---

#### 1. 今日速览

Hermes Agent 今日发布了 `v0.15.1` 紧急热修复版本，迅速解决了上一版本（v0.15.0）中 Dashboard 无限重载的 P0 级问题，体现了极高的响应速度。项目整体活跃度达到峰值：过去24小时内共有 **50 条 Issue 更新** 与 **50 条 PR 更新**。社区贡献者极为活跃，尤其是核心贡献者 `Kyzcreig` 提交了8+个深层修复 PR，覆盖网关、代理和压缩器等多个核心模块。尽管大版本发布后出现了明显的稳定性波动，但强大的社区修复力说明项目处于非常健康的“高速迭代-快速反馈”循环中。

#### 2. 版本发布

- **v2026.5.29 — Hermes Agent v0.15.1 (The Patch Release)**
  - **核心内容**：针对 v0.15.0 引入的 Dashboard 无限重载循环（`#34206`, `#34202`, `#34289`）的同日热修复。
  - **破坏性变更**：无。纯修复版本。
  - **迁移注意事项**：**强烈建议所有已升级至 v0.15.0 的用户立即升级至该版本**，否则在 `--insecure` / 环回模式下 Web UI 完全无法使用。
  - **链接**: [NousResearch/hermes-agent Release v0.15.1](https://github.com/NousResearch/hermes-agent)

- **v2026.5.28 — Hermes Agent v0.15.0 (The Velocity Release)**
  - **概述**：该版本包含 **1,302 次提交**，**747 个合并的 PR**，关闭了 560+ 个 Issues（含 15 个 P0，65 个 P1），来自 **321 位社区贡献者**。这是项目历史上规模最大的一次迭代发布。
  - **链接**: [NousResearch/hermes-agent Release v0.15.0](https://github.com/NousResearch/hermes-agent)

#### 3. 项目进展

今日合并/关闭了 **11 个 PR 和 Issue**，项目在功能完善与代码健壮性方面均有显著推进：

- **Kanban 看板全面调优**：
  - `#24329` [CLOSED] 看板现在能明确展示“不可运行”的任务和“未知指派人”。  
  - `#27145` [CLOSED] 调度器支持自动指派未分配的“就绪”任务，避免任务积压。  
  - `#21582` [CLOSED] 实现了每 Profile 的并发任务数限制（`limit tasks per profile`），解决了资源争抢问题。  
  - **分析**：Kanban 模块在用户高呼声下迅速成熟，已成为项目工作流的核心卖点。

- **网关与会话管理**：
  - `#33724` [CLOSED] 修复 Telegram 网关在特定退出路径下未设置标记导致**重复发送保底消息**的 Bug（fixes `#33708`）。

- **开发者体验**：
  - `#34288` [CLOSED] Dobby 功能的产品化封装 PR 已合并，推进了 Dobby 的独立部署能力。
  - `#33730` [CLOSED] 修复 `hermes skills search` 中 Identifier 列被截断导致无法安装技能的问题。

- **模型与代理核心**：
  - `#34294` [OPEN] 修复任务委托（`delegation`）中 `code_execution` 与用户显式声明的工具集被静默清除的问题（含测试覆盖）。
  - `#34293` [OPEN] 支持内联 `provider/model` 语法切换模型，一行命令即可切换提供商与模型。
  - `#34291` [OPEN] 上下文压缩器现可拒绝将 Provider 返回的错误/拒绝文案作为压缩摘要，防止历史污染。

#### 4. 社区热点

- **最热议题：Dashboard 主题改进（`#18080`）**
  - **数据**：20 条评论，**31 个 👍**。
  - **链接**：[NousResearch/hermes-agent Issue #18080](https://github.com/NousResearch/hermes-agent/issue/18080)
  - **诉求分析**：用户 `ogermer` 直言当前 5 套主题（Midnight, Ember 等）虽然在轮换颜色，但存在**严重的可读性问题**：默认使用了对比度极低的浅色衬线字体，导致 Dashboard 难以阅读。这不仅仅是审美需求，更是日常监控 Agent 工作流时的效率瓶颈。虽标为 P3，但社区共鸣极强，表明 UI/UX 是下一阶段重点改善方向。

- **贡献者高光：Kyzcreig 的 Bug 歼灭战**
  - 今日个人提交了 8 个高价值修复 PR（`#34291` 至 `#34299`），涵盖 **Auxiliary Client**（模型规范化、缓存路径）、**Compressor**（假摘要识别）、**Gateway**（清除陈旧打字态）和 **Delegation** 模块。这种密集的修复节奏侧面印证了 v0.15.0 虽功能强大但重构范围大，遗留了不少边缘 Case。

#### 5. Bug 与稳定性

| 严重程度 | Bug 描述 | 关联 Issue/PR | 状态 |
|---|---|---|---|
| **致命** | Dashboard 在 `--insecure` 下无限 401 重载（0.5s/次），Web UI 完全不可用 | `#34206`, `#34202`, `#34289` | **已修复 (v0.15.1)** |
| **高** | v0.15.0 Docker 镜像中 TUI 无法工作，报“events feed disconnected” | `#34091` (P1) | 待修复 |
| **高** | `hermes mcp add` 等命令在 MCP 包未安装时直接报 `NameError`，缺乏优雅降级 | `#34220` (P2) | 待修复 |
| **中** | `atomic_replace()` 在 `HERMES_HOME` 为跨文件系统符号链接时失败 (EXDEV) | `#34252` (P2) | 待修复 |
| **中** | 提供商中途切换（如 OpenAI Codex 切 xAI）残留加密上下文，导致所有请求 400 | `#34205` (P3) | 待修复 |
| **中** | Honcho 记忆插件在冷启动 cron 进程时无限制挂起（v0.15.0 回归） | `#34070` (P3) | 待修复 |
| **低** | `auxiliary.title_generation.timeout` 配置被硬编码为 30s，无视用户设定的 1800s | `#32729` (P3) | 待修复 |

#### 6. 功能请求与路线图信号

- **Swarm 自定义编排能力（`#34273`）**：用户请求 `hermes kanban swarm` 支持用户自定义验证器（Verifier）与合成器（Synthesizer）的任务体与技能。若被采纳，将标志着 Hermes **正式开放多智能体工作流的高级可编程性**。
- **内置自文档技能（`#28505`）**：建议将 `llms-full.txt` 包装为内建技能注入 Agent，使其在无网络沙盒环境中也能精准调用 Hermes 命令。这是一个**投入小、收益高**且能显著减少用户受挫感的优化。
- **Mnemosyne 记忆系统标准化（`#34271`）**：社区呼吁将 Mnemosyne 加入官方对比文档。鉴于 Honcho 插件存在回归 Bug，社区正在寻找更稳健的替代记忆方案，Mnemosyne 呼声极高。

#### 7. 用户反馈摘要

- **满意点**：
  - 高度认可项目对 Dashboard 崩溃的 **“当日 Hotfix”** 响应速度。
  - Kanban 功能（自动分配看板任务 `#27145`、Profile 限流 `#21582`）的迅速落地，让用户感到决策被倾听。

- **核心痛点**：
  - **信任冲击**：v0.15.0 直接打烂 Web UI 的 P0 回归严重打击了部分用户的升级信心。
  - **Docker 用户被困**：容器内 TUI 完全失效（`#34091`），迫使部分容器化部署用户回滚至 v0.14.0。
  - **配置系统的“假响应”**：用户反复修改`auxiliary.title_generation.timeout` 却发现底层是硬编码（`#32729`），排查过程如同“追鬼”，暴露出配置系统与实际逻辑层的脱节。
  - **多 Provider 切换的混乱状态**：切换模型暴露了网关会话状态管理的不健壮（加密残留 `#34205`），让多模型高级用户体验破碎。

#### 8. 待处理积压

- **配置兼容性老大难（`#13849`）**：
  - **链接**：[NousResearch/hermes-agent Issue #13849](https://github.com/NousResearch/hermes-agent/issue/13849)
  - **状态**：创建于 2026-04-22，存活超 1 个月。用户试图通过 9router 调用模型，但 `wizard` 和手动配置 `config.yaml` 均无效。底层配置系统的扩展性可能存在结构性缺陷，急需维护者确认。

- **被 PR 洪流淹没的核心功能 PR（`#14470`）**：
  - **链接**：[NousResearch/hermes-agent PR #14470](https://github.com/NousResearch/hermes-agent/pull/14470)
  - **背景**：该 PR 旨在为自定义 Provider 添加 `model_validate` 选项，以绕过无法通过 `/v1/models` 验证的模型（如某些供应商或老版本 API）。
  - **风险**：今日 50+ 条新 PR 涌入，该 PR 作为沉淀近 1 个月的老 PR，很可能被淹没。但它实际上是解锁**自定义私有模型接入**的关键阻塞点，建议维护者优先审阅。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据你提供的 GitHub 数据生成的项目动态日报。

---

## PicoClaw 项目动态日报 (2026-05-29)

### 1. 今日速览

今日项目数据活跃，共发生 **6 条** Issue 更新及 **32 条** PR 更新，并发布了一个 Nightly 构建版本。虽依赖管理自动化程度极高（Dependabot 驱动），但核心社区贡献的 PR 存在明显的审阅积压现象（共 23 条待合入），项目健康度受限于维护者审阅带宽。RISC-V 平台的兼容性 Bug 成为社区讨论焦点，而历史久悬的 “OpenAI API Channel 支持” 功能（#1738）正式关闭，是今日最重要的里程碑节点。

### 2. 版本发布

- **Nightly 构建**: `v0.2.9-nightly.20260529.85751492`
    - **说明**: 基于主分支 `main` 的自动化构建，可能包含未经完整测试的新变更。
    - **定位**: 提供给开发者及早期体验用户，生产环境建议谨慎使用。
    - **变更范围**: 对比上一版本 `v0.2.9`，涵盖主分支所有新提交。 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

### 3. 项目进展

今日项目向前迈出了扎实的一步，主要体现在以下关键工作项的合并/关闭：

- **核心功能里程碑**: **Issue #1738**（`[Feature] 添加OpenAI API 格式的channel支持`）被正式关闭。该功能自今年 3 月提出，历经社区讨论和开发，现已落地。这意味着用户可以将 PicoClaw 作为兼容 OpenAI API 的 Backend，直接嵌入已有工程系统，极大提升了项目的集成互操作性。
- **环境兼容性修复**: **Issue #2944**（`Termux / termux-chroot: X509 certificate error`）已关闭。修复了在 Termux 移动端环境下因证书路径导致的 HTTPS 连接失败问题，提升了项目在移动/边缘计算场景的可用性。
- **技术栈维护**: 合并了依赖升级 PR **#2918**（larksuite SDK）及 **#2920**（Anthropic SDK），确保了与相关 API 的持续兼容性。
- **项目可持续性**: **Issue #2912** 已合并，项目仓库现已添加 `.github/FUNDING.yml` 文件，社区可通过 GitHub Sponsors 为项目提供财务支持。

### 4. 社区热点

- **话题焦点**: **[BUG] RISC-V 架构兼容性问题 (#2887)**
    - **链接**: `sipeed/picoclaw Issue #2887`
    - **详情**: 该 Issue 是今日讨论最热烈的议题（共 7 条评论）。用户 `s0me0ne-unkn0wn` 指出，官方提供的 `.deb` 包在 RISC-V 架构的 Debian 系统上完全无法调用 OpenAI 模型（`gpt-5.4-2026-03-05`）。
    - **分析**: 该问题自 5 月 17 日报道，已持续近两周。目前 Issue 处于活跃开放状态，但暂无官方或社区的修复 PR。这表明 RISC-V 用户群体的需求真实且迫切，若不能尽快解决，将损害 PicoClaw 在信创及边缘计算领域的渗透率。

### 5. Bug 与稳定性

- **高优未修复 Bug**:
    - **#2887**: **RISC-V 平台无法调用 OpenAI 模型**（严重性: 阻塞）。影响核心 Agent 功能。目前无对应修复 PR，且缺乏官方回复，建议维护者尽快排查 Go 编译与 RISC-V 环境的兼容性问题。
- **修复 PR 待合并**:
    - **会话存储健壮性修复（贡献者: SiYue-ZO）**:
        - **#2913**: 修复 JSONL 会话索引热路径克隆问题，直接影响会话恢复性能与 TTL 刷新逻辑。
        - **#2907**: 修复 JSONL 存储崩溃后的元数据漂移问题，提升了数据一致性。
        - **优先级**: 这两条 PR 直接关乎 `pkg/memory` 模块的核心稳定性，建议立即 Review 并合入。
    - **误报修复**:
        - **#2965**（贡献者: `maxmilian`）: 修复了 `exec` 工具中 `restrict_to_workspace` 功能对无 scheme URL（如 `wttr.in/Beijing`）的路径误识别问题。该 PR 为今日新提，修复逻辑清晰。
    - **Web UI 修复**:
        - **#2908**（贡献者: `SiYue-ZO`）: 修复后端元数据重构后，前端模型配置页上提供商 Logo 不显示的问题。

### 6. 功能请求与路线图信号

- **下一版本潜在功能（待合并 PR）**:
    - **AI 提供商扩展**:
        - **#2917**: 新增 NEAR AI Cloud 作为 OpenAI 兼容的一流 LLM 提供商，并支持模型列表获取。
        - **#2915**: 为 MiMo 提供商添加了 `mimo-v2.5` 系列模型的推荐，支持多模态。
    - **图像处理管线升级**:
        - **#2964**: 为视觉管线新增了可配置的入站图像压缩策略，优化模型负载构建。
- **性能优化信号**:
    - **#2916**: 用户 `corporatepiyush` 提交了关于 CPU、内存和 IO 的系统性优化方案。虽然该 Issue 已标记为 stale，但其内容详实，涉及代码库多个层面。若项目进入性能调优周期，该 Issue 将极具参考价值。

### 7. 用户反馈摘要

- **特定平台痛点**: **#2944** 中，Termux 用户 `ClockW-TheROOT` 主动抓取并修复了 HTTPS 证书问题，项目积极响应，展现了活跃的社区协作生态。而 **#2887** 中 RISC-V 用户的反馈则凸显了项目在非 x86/ARM64 主流平台上的测试盲区。
- **嵌入式集成需求达成**: 用户 `j4ckzh0u` 在 **#1738** 中提出的 “将 PicoClaw 嵌入既有系统” 的需求历经两个多月终于被满足，这标志着项目从独立 Agent 向平台能力组件的转型迈出重要一步。
- **可持续性关注**: 用户 `nikolasdehor` 主动建议添加 `FUNDING.yml`（**#2912**），表明核心贡献者群体开始关注项目的长期发展，希望为项目提供资金支持而非仅仅是代码贡献。

### 8. 待处理积压

目前项目面临的最显著瓶颈是 **审阅带宽不足**。

- **PR 审阅积压**: 当前有 **23 个** PR 待合并，其中 **9 个** 已被标记为 `[stale]`（长时间无活动）。以下 5 条 PR 问题重大且质量较高，强烈建议维护者在下一轮合并窗口前优先处理：
    - `feat(provider): add NEAR AI Cloud provider` (#2917, `PierreLeGuen`)
    - `feat(providers): add CommonModels for MiMo provider` (#2915, `SiYue-ZO`)
    - `Fix JSONL session index hot-path cloning` (#2913, `SiYue-ZO`)
    - `Fix JSONL store metadata drift after crash` (#2907, `SiYue-ZO`)
    - `fix(web): restore provider logo fallbacks` (#2908, `SiYue-ZO`)
- **严重 Bug 待响应**: **#2887**（RISC-V 兼容性问题）作为阻塞性 Bug 已开放多日且无官方维护者回应。长期悬而未决将对贡献者信心及项目在多样化硬件生态中的声誉造成负面影响。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 NanoClaw 开源项目的分析师，以下是根据 2026-05-29 数据生成的每日项目动态报告。

---

# 🐚 NanoClaw 项目日报 | 2026-05-29

## 1. 今日速览

在今日的数据窗口内，NanoClaw 项目保持 **高度活跃**。共处理 **5 个 Issues** 及 **7 个 Pull Requests**。社区最受关注的多供应商支持诉求（#80）在长期讨论后正式关闭，标志着项目架构或路线图可能迎来重大转向。与此同时，维护者在核心稳定性（WhatsApp 会话销毁、交付管道竞态）与安全增强（Symlink 防护、MCP 凭据注入）上投入了大量精力，体现了项目在功能拓展与基础加固并行下的健康态势。

## 2. 版本发布

本周期内无新版本发布。

## 3. 🚀 项目进展

本周共有 **4 个 PR** 被合并/关闭，**1 个 Issue** 结案，项目在自主性、依赖管理和平台可靠性上取得了扎实进展。

- **基础架构升级** ([#2637](nanocoai/nanoclaw PR #2637))：合并了 Claude Code CLI 及 Agent SDK 的重要版本升级（至 `2.1.154` 与 `0.3.154`）。注意此次 SDK 升级涉及破坏性变更（部分依赖转为 peer dep），需要依赖此 SDK 的外部项目同步更新声明。
- **智能体自主性进化** ([#2635](nanocoai/nanoclaw PR #2635))：合并了 `patch_bridge` 特性。现在智能体（如 Pero）可以通过批准机制直接向宿主侧 bridge 提交源码补丁，这是迈向更高级自主修复与扩展能力的重要一步。
- **平台稳定性** ([#2639](nanocoai/nanoclaw PR #2639))：合并了针对 iOS 平台的可靠性修复。
- **历史积案清理** ([#102](nanocoai/nanoclaw PR #102))：关闭了长期未决的 Notion 集成技能 PR，清理了历史遗留项。
- **社区共识达成** ([#80](nanocoai/nanoclaw Issue #80))：关闭了关于支持多供应商运行时（如 OpenCode、Gemini）的 Enhancement Issue，该项目曾引发社区强烈共鸣（34 评论、60 👍）。

## 4. 🔥 社区热点

**🔥 最热讨论：[#80] 支持除 Claude/Anthropic 以外的运行环境**
- **链接**：[nanocoai/nanoclaw Issue #80](nanocoai/nanoclaw Issue #80)
- **状态**：今日已关闭
- **诉求分析**：该 Issue 以 **60 个 👍** 和 **34 条评论** 成为绝对焦点。社区核心担忧在于对 Anthropic 的过度依赖可能导致账户被封禁，进而强烈呼吁支持开源的 `opencode`、`codex` 或 `gemini` 等替代方案。该 Issue 的 **正式关闭** 可能是项目方已给出明确实现路径或路线图承诺的信号，这是今日最值得关注的社区动向。

## 5. 🐞 Bug 与稳定性

本周报告了多项 Bug，涉及 WhatsApp 可靠性、核心交付管道及安全性，其中部分已有修复 PR 在等待合并。

**严重级别：高**
- **[BUG] 交付管道竞态** ([#2640](nanocoai/nanoclaw Issue #2640))：今日新开。`outbound.db` 在轮询时因只读模式与写入事务产生竞态，抛出 `SQLITE_READONLY_ROLLBACK` 错误。**直接影响消息出站交付稳定性，暂无修复 PR。**
- **[BUG] WhatsApp 会话自毁** ([#2633](nanocoai/nanoclaw PR #2633))：报告称 Baileys 7.x 下的两个结构性 Bug 导致已配对的 WhatsApp 会话被意外销毁。**已有修复 PR 正等待合并。**

**严重级别：中**
- **[BUG] WhatsApp 提及模式误触** ([#2638](nanocoai/nanoclaw Issue #2638))：`engage_mode=mention` 将双人私聊误判为 Bot 的 DM，导致每一条消息都被截获。影响了 WhatsApp 用户的使用预期。暂无修复 PR。
- **[Security] Symlink 路径穿越** ([#2630](nanocoai/nanoclaw PR #2630))：强化了入站附件收件箱的安全性，拒绝写入通过符号链接指向的根目录。**已有修复 PR 在审查中。**

## 6. 💡 功能请求与路线图信号

- **告别供应商锁定** ([#80](nanocoai/nanoclaw Issue #80))：如上所述，该 Issue 的关闭暗示多供应商支持将是下一阶段的战略重点。
- **企业级安全接入**：
  - **MCP 凭据注入** ([#2636](nanocoai/nanoclaw Issue #2636))：请求让 OneCLI 凭据网关能注入到 MCP 容器的环境变量中，而非仅仅通过代理路由。
  - **AWS 代理技能** ([#2634](nanocoai/nanoclaw PR #2634))：新增 `paws4claws` 技能，用于集成 AWS 凭据代理守护进程。这两个议题共同指向了 **企业级安全部署场景**。
- **v2 功能澄清** ([#2632](nanocoai/nanoclaw Issue #2632))：用户询问旧版 Telegram 多 Bot 身份（agent-swarm）特性在 v2 中的兼容性。这表明部分高级用户正在规划迁移，但官方尚未给出明确答复。

## 7. 🎤 用户反馈摘要

- **对供应商锁定的焦虑**（[#80](nanocoai/nanoclaw Issue #80)）：“Anthropic already shutting down peoples' subs... opencode is a (open source!) competitor.” 用户不仅希望支持其他模型，更担心 **账户运营的可持续性**，这是推动去供应商锁定的核心动力。
- **迁移路径困惑**（[#2632](nanocoai/nanoclaw Issue #2632)）：“trying to plan a v1 to v2 migration... the current state is a little ambiguous.” 使用旧版 Telegram Swarm 功能的用户在迁移时感到 **文档缺失与状态不确定性**。
- **特定平台可用性痛点**（[#2638](nanocoai/nanoclaw Issue #2638)）：用户在 WhatsApp 使用中遇到了确实的可用性 Bug，直接影响了 “配对后默认行为” 的体验。

## 8. ⏳ 待处理积压

以下 Issue/PR 长期未获响应或当前处于阻塞状态，需维护者重点关注：

1. **[Critical P0] 交付管道竞态** ([#2640](nanocoai/nanoclaw Issue #2640))
   - 今日新开的核心 Bug，尚无修复 PR。建议项目维护者优先分配资源复现并修复。
2. **[High P1] WhatsApp 自毁 Bug 修复** ([#2633](nanocoai/nanoclaw PR #2633))
   - 已有明确的修复方案，请尽快 Code Review 并合并，以减少 WhatsApp 通道用户的流失风险。
3. **[High P1] 渠道功能澄清：Telegram v2 迁移** ([#2632](nanocoai/nanoclaw Issue #2632))
   - 用户等待官方回应以决定迁移方向，长期搁置将影响社区对 v2 的信心。
4. **[Medium P2] WhatsApp 提及模式误判** ([#2638](nanocoai/nanoclaw Issue #2638))
   - 需要确认设计意图并分配修复。

---
**总结**：今日 NanoClaw 项目在 **社区共识达成** 与 **底层 Bug 修复** 上交出了不错的答卷。关闭 #80 是令人振奋的信号，但 #2640 的高杀伤力竞态问题与积压的 WhatsApp 修复 PR 仍需尽快解决以保障用户体验的健康度。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 NullClaw 项目 GitHub 数据，为您生成 2026-05-29 的项目动态日报。

---

## NullClaw 项目动态日报 (2026-05-29)

### 1. 今日速览

过去24小时内，NullClaw 项目保持稳健的推进节奏。社区贡献者修复了两个长期困扰 Telegram 用户的“通道未配置”Bug，并完成了多项安全与兼容性优化，包括 macOS 工作区安全策略调整和 Web 搜索测试隔离。项目活跃度良好，3个待合并 PR 正在等待审核，显示社区贡献意愿强烈。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日共有 7 个 Pull Request (PR) 被合并或关闭，标志着项目在多个方面取得了实质性进展。

- **核心功能修复**： **PR #924** 被合并，该 PR 从根本上解决了长期困扰用户的问题——Telegram 通道配置中的数字用户 ID 导致通道显示为“未配置”。此修复同时关闭了 `#869` 和 `#901` 两个 Issues，是本次更新中最关键的稳定性提升。
- **新提供商支持**： **PR #922** 被合并，正式引入对 **NEAR AI Cloud** 和 **Atlas Cloud** 的支持。这扩展了 NullClaw 作为 AI 代理的兼容性，让用户能接入更多云端模型服务，是项目生态扩展的重要一步。
- **安全强化**： **PR #907** 被合并，这是一项重要的安全加固。它移除了 HTTP 请求中的免密凭证传递、要求对 Telegram/Discord/LINE 等通道设置明确的信任源 (`allow_from`)，显著降低了凭证泄露和未授权访问的风险。
- **跨平台兼容性与测试**：
    - **PR #925** 合并，修复了 macOS 系统在 `/private/var/folders` 目录下的工作区路径被错误拦截的问题，提升了 macOS 用户的体验。
    - **PR #926** 和 **PR #927** 合并，专注于测试环境的改进。它们分别隔离了 Web 搜索工具的 API Key 环境变量，以及抑制了模块测试中不必要的错误日志输出，从而让测试结果更清洁、更可靠。
    - **PR #878** 合并，优化了底层线程调度，通过在 POSIX 系统上使用 `nanosleep` 来更有效地挂起线程，这有助于提升在特定工作负载下的性能和准确性。

> 总结：当日更新解决了用户痛点，强化了安全性，并拓展了平台兼容性，项目在稳定性和功能丰富度上均有所提升。

### 4. 社区热点

今日最引人关注的是仍处于开放状态的 **PR #928** 和 **PR #929**，这两个 PR 均由贡献者 `raskevichai` 提交，并均获得多次更新。

- **PR #929: `memory_list` 无法显示全局记忆**：[链接](nullclaw/nullclaw PR #929)
    - **诉求**：用户在使用 Agent 循环时，`memory_list` 工具无法返回那些没有指定 `session_id` 的全局记忆条目。这导致通过 `memory_store` 存储的信息无法被检索，破坏了核心功能体验。
    - **分析**：这是一个关键的功能性 Bug，影响了用户使用记忆系统的流畅性。该 PR 是解决底层问题 #917 的修复方案，社区对此有明确需求。

- **PR #928: Telegram 轮询模式下子代理结果丢失**：[链接](nullclaw/nullclaw PR #928)
    - **诉求**：当用户通过 `nullclaw channel start telegram` 启动 Telegram 机器人后，通过 `spawn` 工具调用的子代理（Subagent）完成任务的结果会“静默”消失，用户无法收到。PR 中明确指出多个生产环境的 Telegram 机器人用户都遇到了此问题。
    - **分析**：这是一个影响生产环境的严重 Bug。`spawn` 是创建并行子任务的重要工具，其结果的丢失意味着用户可能无法获取关键的操作信息。该 PR (对应 Issue #918) 的修复呼声很高。

这两个 PR 反映了社区用户对 **核心功能可靠性** 和 **Telegram 通道可用性** 的高度关注。

### 5. Bug 与稳定性

过去24小时内，项目主要解决了两个已存在的 Bug，并有两个潜在的修复正在等待合并。

| 严重程度 | Bug 描述 | 状态 | 解决方案 | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **高** | **Telegram 通道配置中数字用户 ID 导致通道无效** | 已修复 | PR #924 已合并修复 | [Issue #869](nullclaw/nullclaw Issue #869) / [Issue #901](nullclaw/nullclaw Issue #901) |
| **高** | **Telegram 轮询模式下子代理 (`spawn`) 结果丢失** | 待合并 | PR #928 提供修复方案 | [PR #928](nullclaw/nullclaw PR #928) |
| **中** | **`memory_list` 无法检索全局记忆条目** | 待合并 | PR #929 提供修复方案 | [PR #929](nullclaw/nullclaw PR #929) |
| **低** | **Web 搜索测试因环境变量冲突而不稳定** | 已修复 | PR #926 通过隔离环境变量解决 | [PR #926](nullclaw/nullclaw PR #926) |

### 6. 功能请求与路线图信号

- **新 AI 云提供商集成**：**PR #922** 合并后，用户现在可以使用 `NEAR AI Cloud` 和 `Atlas Cloud`。这表明项目在开放接入多个 AI 提供商方面持续推进，降低对单一平台的依赖。这两个提供商完全符合 OpenAI API 标准，集成成本较低。
- **Cron 作业子代理与安全强化**：**PR #783**（长期开放）仍然在活跃更新。虽然未合并，但其庞大的功能集（基于数据库的调度器、JSON格式输出、安全强化）表明社区有强烈需求，且是项目未来实现高级自动化能力的重要铺垫。这可能是下一版本的关键功能。

### 7. 用户反馈摘要

- **用户痛点**：多项反馈表明 **Telegram 通道的可靠性** 是用户面临的主要挑战。多个 PR 和 Issue 都指向了 Telegram 通道配置不生效 (`#869`, `#901`) 及运行时结果丢失 (`#918`) 的问题。这说明虽然 Telegram 是重要渠道，但当前版本的接口或实现还需要打磨。
- **使用场景**：用户在 Issue `#917` 中反馈 `memory_list` 无法看到全局记忆，这暴露了在 Agent 循环中使用记忆系统的痛处。用户期望能够自由地存储和检索跨会话的全局信息。
- **积极的社区贡献**：从 PR 的作者来看，社区贡献者（如 `raskevichai`, `vernonstinebaker`）非常活跃，他们不仅发现问题，还主动提供了高质量的修复代码，体现了项目社区的健康生态。

### 8. 待处理积压

1. **PR #783: Cron 子代理功能集合**：[链接](nullclaw/nullclaw PR #783)
    - **状态**：开放中，创建于 2026-04-07，最近更新于 2026-05-28。
    - **内容**：这是一个宏大的功能 PR，包含 cron 调度、JSON输出和安全增强等。
    - **提醒**：此 PR 已经超过 50 天未合并，尽管开发者在持续更新。维护团队需要评估其复杂度，尽早决定是合并、要求分解还是关闭，以避免长期分歧增加后续合并成本。

2. **PR #928 和 PR #929**：[链接](nullclaw/nullclaw PR #928)，[链接](nullclaw/nullclaw PR #929)
    - **状态**：开放中，创建于 2026-05-23。
    - **内容**：修复了两个核心稳定性问题。
    - **提醒**：这两个 PR 已经存在一周，且内容都是修复社区报告的、影响用户体验的关键 Bug。建议尽快进行审查和合并，以提升项目稳定性和用户满意度。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目数据生成的 2026-05-29 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-05-29

## 1. 今日速览

IronClaw 项目今日保持高速迭代，24 小时内处理了 **33 条 Issue** 和 **50 个 PR**，合并率高达 **66%**。项目重心高度集中在 **“Reborn”架构的身份验证（Auth）与凭证安全加固**上，同时社区贡献者在 **WeCom 新频道集成**、**CI 流水线**和**文档**等领域也有积极产出。尽管无正式版本发布，活跃的代码合并表明项目内部迭代节奏极快，整体健康状况良好。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日项目推进迅速，多项核心功能完成合并，标志着“Reborn”架构在安全与用户体验上迈出关键一步：

- **凭证安全与身份验证 (Credentials & Auth):**
  - PR [#3903](https://github.com/nearai/ironclaw/pull/3903) 完成合并，关闭了 Reborn 生产环境凭证边界的关键缺口，并引入了 `PathPlaceholder` 注入机制。
  - 相关 Issue [#4113](https://github.com/nearai/ironclaw/issues/4113) 的解决方案（Google OAuth 刷新生命周期）落地，完善了 Google 认证后端。

- **WebUI 交互增强:**
  - PR [#4212](https://github.com/nearai/ironclaw/pull/4212) 合并，使 WebUI v2 能够实时接收并展示技能激活状态。
  - PR [#4196](https://github.com/nearai/ironclaw/pull/4196) 合并，新增工作摘要投影，让用户在 Agent 运行时能更清晰地感知执行进度。

- **代码重构与健壮性:**
  - PR [#4213](https://github.com/nearai/ironclaw/pull/4213) / [#4214](https://github.com/nearai/ironclaw/pull/4214) 合并，成功将 1828 行的巨型 `lib.rs` 中的 HTTP 出口管道拆分为独立模块，大幅降低了维护成本。
  - PR [#4211](https://github.com/nearai/ironclaw/pull/4211) 合并，修复了 `glob` 扫描在达到预算限制时返回错误而非截断结果的问题，提升了运行时健壮性。

- **开发者体验 (CI/CD):**
  - 针对 `/benchmark` 指令失效的问题，维护者迅速合并了多项修复（[#4217](https://github.com/nearai/ironclaw/pull/4217), [#4220](https://github.com/nearai/ironclaw/pull/4220), [#4221](https://github.com/nearai/ironclaw/pull/4221)），并解除了对 benchmark 工作流的 SHA 锁定。

## 4. 社区热点

今日讨论最活跃的议题集中在**安全权衡**与**平台扩展**上：

- **安全权衡：凭证注入原语的去留？**
  Issue [#3917](https://github.com/nearai/ironclaw/issues/3917) 获得 4 条评论，是关于一个核心安全问题的激烈辩论。PR #3903 引入的 `RuntimeCredentialTarget::PathPlaceholder`（将凭证注入 URL 路径段）被核心开发者视为一个比 Header 或 Query 注入更糟糕的通道。社区正在讨论是否应在发布前将其移除或加固。这反映了项目组对安全质量的高标准内省。

- **平台扩展：IronHub 集成与本地审批门禁**
  超大 PR [#3737](https://github.com/nearai/ironclaw/pull/3737)（feat(ironhub)）继续吸引广泛关注，该特性将允许 CLI 和 Agent 在运行时从 IronHub 安装工具和技能，对平台生态至关重要。同时，XL 尺寸的 PR [#4186](https://github.com/nearai/ironclaw/pull/4186)（本地开发审批门禁）也在稳步推进，旨在加强安全控制边界。

## 5. Bug 与稳定性

今日 Bug 报告集中在**新频道集成**与**基础设施回归**上：

- **严重 / 高影响:**
  - **Nightly E2E 测试失败** ([#4108](https://github.com/nearai/ironclaw/issues/4108))：自动化测试流水线出现故障，需要排查具体的回归源。
  - **WeCom 频道稳定性问题** ([#4191](https://github.com/nearai/ironclaw/issues/4191) 及其子议题)：测试人员在 v0.29.0 预发布环境中发现多项严重问题，包括图片附件非常不稳定 ([#4195](https://github.com/nearai/ironclaw/issues/4195))、视觉分析解析错误/过时的图片 ([#4197](https://github.com/nearai/ironclaw/issues/4197)) 以及群聊与私聊在 Web UI 中会话合并的 Bug ([#4194](https://github.com/nearai/ironclaw/issues/4194))。

- **安全缺陷:**
  - **凭证内存泄露风险** ([#4222](https://github.com/nearai/ironclaw/issues/4222))：报告指出，运行时 HTTP 出口在注入凭证时，明文凭证会被复制到普通的 `String` 字段中，存在生命周期结束后未及时清零（Zeroize）的安全风险。目前尚无关联修复 PR。

- **配置问题:**
  - **OpenAI 提供商配置失败** ([#4188](https://github.com/nearai/ironclaw/issues/4188))：在 v0.29.0 预发布环境中，配置 OpenAI 提供商并测试时返回 400 错误，可能与模型名称或适配器类型有关。

## 6. 功能请求与路线图信号

从今日议题中可以清晰看到项目未来的几个核心方向：

- **“Reborn” SSO 统一：** 这是当前最明确的路线图信号。系列议题（[#4116](https://github.com/nearai/ironclaw/issues/4116), [#4179](https://github.com/nearai/ironclaw/issues/4179), [#4180](https://github.com/nearai/ironclaw/issues/4180), [#4181](https://github.com/nearai/ironclaw/issues/4181)）表明，项目正致力于将 v1 的 Google、GitHub 和 NEAR 钱包登录全面迁移至全新的 WebChat v2 界面。PR [#4224](https://github.com/nearai/ironclaw/pull/4224) 已开始着手实现手动令牌提交门禁。

- **平台扩展与 MCP 生态：** 除了 IronHub 集成，今日还出现了大量构建 MCP 生态系统的信号，包括将 NEAR AI 打包为 Reborn 扩展（[#4223](https://github.com/nearai/ironclaw/pull/4223)）以及新增 Web Access 扩展（[#4219](https://github.com/nearai/ironclaw/pull/4219)）。

- **技术债务清理：** 开发者提出了将运行时 HTTP 出口管道改为全异步的请求（[#4206](https://github.com/nearai/ironclaw/issues/4206)），以及将重复的 PKCE 算法整合到公共模块的提案（[#4215](https://github.com/nearai/ironclaw/issues/4215)）。这表明项目在快速交付功能的同时，也在进行务实的重构。

## 7. 用户反馈摘要

从今日的 Issue 和评论中，可以提炼出以下真实用户/贡献者痛点：

- **WeCom 频道体验反馈（来自测试者 `sunglow666`）：** 详细报告了 WeCom 频道的多项可用性问题（[#4191](https://github.com/nearai/ironclaw/issues/4191) 至 [#4198](https://github.com/nearai/ironclaw/issues/4198)）。用户对图片解析不稳定、群聊与私聊会话混淆以及缺乏配置引导感到困扰。这些反馈对于正式发布前的质量打磨至关重要。

- **安全顾虑（来自核心开发者 `zmanian`）：** 在 [#3917](https://github.com/nearai/ironclaw/issues/3917) 中，开发者强烈质疑 `PathPlaceholder` 的设计，认为该特性在发布前必须重新评估，这体现了项目内部对引入安全风险的零容忍态度。

- **开发者工具稳定性（来自 CI 机器人及开发者 `pranavraja99`）：** 自动化流水线偶尔的失败（如 nightly E2E 和 benchmark 指令）影响了开发体验。尽管维护者迅速响应并修复了 CI 问题，但流水线的高频波动仍需引起重视。

## 8. 待处理积压

提醒维护者关注以下长期未响应的关键项：

1.  **发布阻塞 PR：** [#3708](https://github.com/nearai/ironclaw/pull/3708) **（chore: release）**。自动生成的发布 PR 自 5 月 16 日以来一直处于待合并状态。此版本涉及 `ironclaw_common` 的 API Breaking Changes，大量新功能已合并，但新版本迟迟未发布，可能阻塞下游依赖方。

2.  **安全决策待定：** [#3917](https://github.com/nearai/ironclaw/issues/3917) **（PathPlaceholder 安全评审）**。该安全评审已持续多日，且已有替代方案讨论（[#4203](https://github.com/nearai/ironclaw/issues/4203)）。维护者需要尽快决定是“加固”还是“移除”该特性，以免阻塞依赖该机制的后续 PR（如 #3903）。

3.  **超大特性跟踪：** [#3737](https://github.com/nearai/ironclaw/pull/3737) **（feat(ironhub)）**。尽管非常活跃，但该 PR 标记为 `size: XL` 且包含数据库迁移，涉及面极广。预计需要较长时间进行代码评审，建议维护者安排专项评审时间。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是基于所提供数据为您生成的项目动态日报。

---

# LobsterAI 项目动态日报 (2026-05-29)

**数据抓取时间戳:** 2026-05-29T00:00:00.000Z

---

## 1. 今日速览

项目今日活跃度极高，核心团队在持续高频率地合并 Pull Requests。过去24小时内，共有 **7 个 PR 被合并/关闭**，功能性与稳定性并重。其中，社区贡献者 `btc69m979y-dotcom` 表现尤为亮眼，独立完成了 **Kit（专家套件）商店集成**、**插件更新检查机制** 等多个重要功能的合并。尽管今日只有一个新 Issue 报告，但 PR 积压情况（9个待合并）值得关注，大多数为已存在超过一个月的“陈旧”PR，可能面临版本冲突或需维护者的最终决策。

**活跃度评估：高** (代码合并频繁，功能推进迅速)

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日项目核心进展集中在功能交付、用户体验优化和平台稳定性修复上，由社区开发者主导。

-   **重磅功能落地：Kit（专家套件）商店与对话集成 (#2060)：** 该 PR 已合并。这一新概念允许将多个 Skill 打包为一键安装的套件，并集成了商店页面和对话输入区，是一项重大的产品功能更新，显著增强了 Skill 的发现和组合使用体验。
    -   链接: [netease-youdao/LobsterAI PR #2060](github.com/netease-youdao/LobsterAI/pull/2060)

-   **核心体验优化：输入框图片附件预览 (#2061)：** 用户现在可以点击输入框中的图片缩略图进行全尺寸预览，提升了多模态交互的易用性。
    -   链接: [netease-youdao/LobsterAI PR #2061](github.com/netease-youdao/LobsterAI/pull/2061)

-   **稳定性和性能提升：**
    -   **插件管理架构优化 (#2068)：** 解决了插件配置修改导致网关频繁重启的问题，引入批量保存和“脏数据”守卫机制，提高了插件管理的稳定性和性能。
        -   链接: [netease-youdao/LobsterAI PR #2068](github.com/netease-youdao/LobsterAI/pull/2068)
    -   **Windows MCP进程清理修复 (#2066)：** 修复了 Windows 平台上 `StdioClientTransport` 关闭时无法杀死子进程树的问题，防止了孤儿进程的产生，提升了系统资源管理能力。
        -   链接: [netease-youdao/LobsterAI PR #2066](github.com/netease-youdao/LobsterAI/pull/2066)
    -   **AI Artifact 误检测修复 (#2070)：** 修复了渲染器对非图片生成工具的 `tool_result` 内容进行误渲染的问题，避免了命令输出的文件路径被错误展示。
        -   链接: [netease-youdao/LobsterAI PR #2070](github.com/netease-youdao/LobsterAI/pull/2070)

## 4. 社区热点

今日社区讨论集中在合并的 `Kit（专家套件）` 相关功能上，虽然只有一条 Issue，但围绕此功能的 PR 在推进过程中是社区关注的焦点。

-   **热点 PR：** `feat: Kit（专家套件）商店与对话集成 (#2060)`。该 PR 横跨 `renderer`、`main`、`cowork` 等多个核心区域，设计文档和功能实现一并提交，表明这是一次经过深思熟虑的重大功能迭代。社区对其带来的新可能性（如技能组合、一键安装）抱有很高期待。
    -   链接: [netease-youdao/LobsterAI PR #2060](github.com/netease-youdao/LobsterAI/pull/2060)

-   **新 Issue 信号：** `创建定时任务错误 (#2071)`。这是当日唯一的 Issue，虽然评论数为零，但用户上传了详细的报错截图，表明在创建定时任务时遇到了功能性阻碍。这是需要立刻关注的潜在 Bug。
    -   链接: [netease-youdao/LobsterAI Issue #2071](github.com/netease-youdao/LobsterAI/issues/2071)

## 5. Bug 与稳定性

今日报告了一个新 Bug，同时也有若干历史 Bug 得到了修复。

-   **[严重] 功能阻断：创建定时任务错误 (#2071)**
    -   **描述：** 用户报告在创建定时任务时系统报错，无法完成任务创建。这是直接影响核心功能的 Bug。
    -   **状态：** 新上报，待复现和排查。尚无相关的 Fix PR。
    -   链接: [netease-youdao/LobsterAI Issue #2071](github.com/netease-youdao/LobsterAI/issues/2071)

-   **已修复的 Bug：**
    -   **Kit 跳转异常 (#2067)：** 合并的 PR 修复了用户在安装 Kit 后，通过“try-asking”跳转到会话页时，Kit 中的 Skill 不会被自动展开并注入上下文的问题。这属于重要的功能联动 Bug。
        -   链接: [netease-youdao/LobsterAI PR #2067](github.com/netease-youdao/LobsterAI/pull/2067)
    -   **插件设置频繁重启 (#2068)：** 修复了插件开关状态变更导致频繁触发网关重启的稳定性问题。
        -   链接: [netease-youdao/LobsterAI PR #2068](github.com/netease-youdao/LobsterAI/pull/2068)

## 6. 功能请求与路线图信号

结合今日合并的PR和积压的PR，可以看出几个清晰的未来方向：

-   **插件生态建设：** `插件更新检查 (#2069)` 和 `批处理保存 (#2068)` 的合并，表明项目正在完善插件生命周期管理和用户体验。
    -   链接: [netease-youdao/LobsterAI PR #2069](github.com/netease-youdao/LobsterAI/pull/2069)

-   **自动化与智能化：** 长期未合并的 `feat(models): add automatic model failover` (#1483) 和 `feat(automation): add Gmail email trigger` (#1484) 表明社区对模型自动故障切换和 Gmail 触发器等高级自动化能力有强烈需求。这些功能一旦合并，将极大提升 LobsterAI 作为自动化 Agent 平台的可用性。
    -   链接: [netease-youdao/LobsterAI PR #1483](github.com/netease-youdao/LobsterAI/pull/1483)
    -   链接: [netease-youdao/LobsterAI PR #1484](github.com/netease-youdao/LobsterAI/pull/1484)

-   **UI/UX 现代化：** 积压的 `定时任务UI全面升级 (#1488)` 和 `技能选择按会话独立管理 (#1494)` 表明，社区贡献者正在尝试对核心模块进行用户体验重构。
    -   链接: [netease-youdao/LobsterAI PR #1488](github.com/netease-youdao/LobsterAI/pull/1488)
    -   链接: [netease-youdao/LobsterAI PR #1494](github.com/netease-youdao/LobsterAI/pull/1494)

## 7. 用户反馈摘要

-   **(Issue #2071) 创建定时任务报错：** 用户截图展示了一个错误弹窗，但未提供详细的操作步骤。初步判断为功能性BUG，可能影响用户正常使用自动化任务。项目维护者应立即联系用户了解详细情况。

## 8. 待处理积压

以下 PR 在较长时间前由社区贡献者提交，最近一次更新均在1-2月前。它们代表了社区重要的贡献，但至今未能合并。建议维护者评估其当前状态，处理代码冲突或给出明确决策，以避免社区贡献者流失。

-   **高优先级（自动化 & 稳定性）：**
    -   [`feat(models): add automatic model failover` (#1483)](github.com/netease-youdao/LobsterAI/pull/1483) - 模型自动故障切换。
    -   [`feat(automation): add Gmail email trigger` (#1484)](github.com/netease-youdao/LobsterAI/pull/1484) - Gmail 邮件触发 Agent。

-   **中优先级（Bug修复）：**
    -   [`fix(cowork): CopyButton 组件卸载后定时器未清理` (#1478)](github.com/netease-youdao/LobsterAI/pull/1478) - 组件卸载后状态更新导致的内存泄漏警告。
    -   [`fix(scheduled-tasks): 编辑定时任务后描述信息被清空` (#1482)](github.com/netease-youdao/LobsterAI/pull/1482) - 编辑任务信息丢失BUG。

-   **低优先级（功能增强）：**
    -   [`feat(scheduledTask): 定时任务模块 UI 全面升级` (#1488)](github.com/netease-youdao/LobsterAI/pull/1488) - 定时任务UI重构。
    -   [`fix(cowork): 技能选择状态改为按会话独立管理` (#1494)](github.com/netease-youdao/LobsterAI/pull/1494) - 会话级技能隔离。
    -   [`fix(skills): reject duplicate skill folder on install` (#1479)](github.com/netease-youdao/LobsterAI/pull/1479) - 防止重复安装 Skill。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 Moltis 项目 2026-05-29 数据生成的日报。

---

# Moltis 项目动态日报 (2026-05-29)

## 1. 今日速览

Moltis 项目在过去 24 小时内呈现高强度修复状态，活跃度极高。核心贡献者 `penso` 主导合并了 4 个修复性 PR，并关闭了 7 个 Issue，重点解决了近期用户报告的多个关键 Bug 与技术债务。尽管未发布新版本，但项目在消息分叉逻辑、CRON 任务执行目标、MiniMax 提供商兼容性以及 Discord 日志诊断方面取得了显著进展。与此同时，一项关于“PTY 级交互式 Claude Code 控制”的深度技术讨论 (#235) 持续占据社区焦点，展示了用户对底层编排能力的强烈渴望。

## 2. 版本发布

无（过去 24 小时内未发布新版本）。

## 3. 项目进展

团队在过去 24 小时内展现了高效的 Bug 响应与修复能力，主要进展如下：

- **修复消息分叉逻辑 (Fix Fork Logice)**: 合并了 PR [#1080](https://github.com/moltis-org/moltis/pull/1080)。
  修复了 WebUI 中“分叉 (fork)”功能严重错误地在 **用户提示 (Prompt)** 处截断，而非在 **助手响应 (Response)** 处截断的历史数据完整性问题。这是影响版本管理体验的核心 Bug。
- **修复 CRON 任务执行目标 (Fix Cron Execution Target)**: 合并了 PR [#1079](https://github.com/moltis-org/moltis/pull/1079)。
  解决了 CRON 任务忽略用户显式设置“执行目标: Host”而错误默认运行于沙箱环境的问题，确保了调度系统的配置严格执行。
- **修复 MiniMax 提供商兼容性 (Fix MiniMax Provider)**: 合并了 PR [#1078](https://github.com/moltis-org/moltis/pull/1078)。
  针对 MiniMax API 在群聊场景下因 `name` 字段不合规导致 2013 错误的问题，通过标准化请求处理逻辑进行了修复。
- **增强 Discord 诊断日志 (Enhance Discord Logging)**: 合并了 PR [#1081](https://github.com/moltis-org/moltis/pull/1081)。
  为 Discord 语音消息增加了丢失诊断日志，帮助管理员区分消息是被网关丢弃还是处理器丢弃，提升了可观测性。
- **进行中的新功能**: PR [#1082](https://github.com/moltis-org/moltis/pull/1082) 提出了新增特权级 `/tmux` 频道命令，允许受信用户检查或发送输入到宿主 tmux 服务器。

## 4. 社区热点

- **Issue [#235](https://github.com/moltis-org/moltis/issues/235)**: PTY-based interactive Claude Code CLI control for autonomous multi-agent orchestration
    - **讨论热度**: 评论数 6 | 👍 1
    - **诉求分析**: 该 Issue 是目前唯一的**开放活跃议题**。用户 `CyPack` 提出了一个具有极高技术深度的挑战：当前 Agent 框架通过 `exec`/`spawn` 调用 Claude Code 时，因 `isatty() == false` 导致 Claude Code 退出交互模式，丧失了对超时、内联编辑、反馈收集等关键能力的控制。社区讨论的焦点在于如何通过 **PTY (伪终端)** 来“欺骗” Claude Code 进入交互模式，从而实现真正的多智能体自主编排。这反映了高级用户对 Moltis 作为底层框架进行更深层次进程控制的需求。

## 5. Bug 与稳定性

今日进入活跃队列的 4 个 Bug 已全部被修复，项目稳定性显著提升。

| Bug 描述 | 严重程度 | 状态 | 修复 PR |
|---|---|---|---|
| **分叉 (Fork) 从提示处截断，而非响应处** [#1075](https://github.com/moltis-org/moltis/issues/1075) | 🔴 严重 (数据损坏/UX) | **已修复** | [#1080](https://github.com/moltis-org/moltis/pull/1080) |
| **CRON 任务忽略 "Execution Target: Host" 设置** [#1072](https://github.com/moltis-org/moltis/issues/1072) | 🟠 高 (功能偏离) | **已修复** | [#1079](https://github.com/moltis-org/moltis/pull/1079) |
| **MiniMax 提供商群聊报错 (2013)** [#1077](https://github.com/moltis-org/moltis/issues/1077) | 🟡 中 (兼容性) | **已修复** | [#1078](https://github.com/moltis-org/moltis/pull/1078) |
| **Discord 语音消息被静默丢弃** [#817](https://github.com/moltis-org/moltis/issues/817) | 🟢 低 (可观测性) | **已修复** | [#1081](https://github.com/moltis-org/moltis/pull/1081) |

目前无遗留的活跃 Bug。

## 6. 功能请求与路线图信号

- **接近完成的功能**: 由团队成员 `penso` 提交的 PR [#1082](https://github.com/moltis-org/moltis/pull/1082) (待合并) 提出了一个 `/tmux` 通道命令。这表明项目正在推进 **高级用户/运维人员** 的操作能力路线图，允许在聊天频道中直接控制宿主主机终端。
- **潜在需求信号**: Issue [#906](https://github.com/moltis-org/moltis/issues/906) 请求在 WebUI 中配置子智能体 (Sub-agents)。虽然已被关闭，但结合 #235 中社区对“多智能体编排”的强烈兴趣，为下层编排提供 UI 配置入口很可能是未来的一个重点方向。
- **未决的战略性任务**: [#235](https://github.com/moltis-org/moltis/issues/235) 提出了项目架构层面的挑战。虽然短期内难以通过简单 Hotfix 解决，但该讨论获得的高度关注度，使其必须被纳入线路图规划。社区希望在 2026 年第二、三季度看到架构级别的改进方案。

## 7. 用户反馈摘要

- **分叉功能的严重报错**: 用户 `vvuk` 今日精准地指出 `#1075` 中 fork 的逻辑缺陷，并提供了明确的复现预期（“fork 后的上下文应包含被点击的响应”），该反馈直接高效，帮助开发者当天完成了问题定位和修复。
- **CRON 配置的信任危机**: 用户 `thedanhoffman` 在 `#1072` 中反馈执行目标被静默覆盖，暴露了配置系统中 Agent Preset 优先级高于用户显式指令的问题。用户对“配置即代码”的信任度非常高，该修复有效地挽回了用户信心。
- **对透明度的强烈需求**: 用户 `dmitriikeler` 在 `#817` 中多次强调“静默失败”带来的运维困难，要求增加日志诊断。这反映了专业用户不仅关注功能正确性，更看重系统的**可观测性**。
- **深度技术共建**: Issue [#235](https://github.com/moltis-org/moltis/issues/235) 的参与者展示了极高的技术素养，他们正在与开发者一起探讨如何突破 `stdio: pipe` 的限制，这是项目从“好用”走向“强大”的关键节点。

## 8. 待处理积压

- **Issue [#235](https://github.com/moltis-org/moltis/issues/235)**: PTY-based interactive Claude Code CLI control for autonomous multi-agent orchestration
    - **延迟时间**: 自 2026-02-25 起，已持续 93 天。
    - **风险提示**: 这是社区讨论最活跃、技术挑战最大的议题。虽然目前无关联 PR，但其长期积压可能导致高级重度用户流失。建议项目维护者明确回复其技术可行性评估，或划定一个决策时间窗口。
- **Issue [#906](https://github.com/moltis-org/moltis/issues/906)**: Make sub-agents configurable in WebUI
    - **延迟时间**: 自 2026-04-28 起，已持续 31 天。虽已关闭，但无官方回复解释原因。如果该功能已确定不在近期路线图内，建议给出简短反馈以避免用户困惑。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据 CoPaw（产品名 QwenPaw）2026-05-28 至 2026-05-29 的 GitHub 数据生成的项目动态日报。

---

# CoPaw 项目每日动态 | 2026-05-29

## 1. 今日速览
今日项目活跃度极高，24 小时内共产生 **78 次更新**（40 个 Issue 与 38 个 PR）。社区反馈非常踊跃，核心团队响应迅速，共合并/关闭了 **20 个 PR**。当前开发焦点集中在 **桌面端（Windows）的稳定性与用户体验打磨**、**CLI/打包工具完善** 以及 **Agent 核心机制（记忆/上下文/工具调用）的深度改进**。无新版本发布，但大量修复与关键功能已进入合并管道，预示下一版本将是一次综合性的大更新。

---

## 2. 版本发布
无

---

## 3. 项目进展
今日项目在多个维度取得了实质性的代码推进：

**Console 前端持续打磨**
- **API 适配与 Bug 修复：** 适配 Ant Design 5.29 弃用 API，并修复了安全页面图标渲染报错（[PR #4790](https://github.com/agentscope-ai/QwenPaw/pull/4790)）。
- **输入框与时间戳修复：** 修复了切换页面后输入框残留内容的顽固 Bug（[PR #4755](https://github.com/agentscope-ai/QwenPaw/pull/4755)）；增强时间戳处理，支持用户时区显示（[PR #4763](https://github.com/agentscope-ai/QwenPaw/pull/4763)）。
- **UI 样式优化：** 环境与安全页面 UI 重构（[PR #4657](https://github.com/agentscope-ai/QwenPaw/pull/4657)），修复滚动条闪烁问题（[PR #4766](https://github.com/agentscope-ai/QwenPaw/pull/4766)）。

**桌面版 & 核心 CLI 完善**
- **启动性能大幅优化：** 社区贡献者通过懒加载与缓存机制，将 Windows 版响应速度提升至约 40ms（[PR #4772](https://github.com/agentscope-ai/QwenPaw/pull/4772)）。
- **CLI 打包与通路修复：** 修复桌面版外部链接跳转（[PR #4683](https://github.com/agentscope-ai/QwenPaw/pull/4683)）；合入工作区下载按钮加载态（[PR #4725](https://github.com/agentscope-ai/QwenPaw/pull/4725)）。
- **即将落地：** **Coding Mode 本地目录引用**（[PR #4762](https://github.com/agentscope-ai/QwenPaw/pull/4762)）与**桌面版 QwenPaw CLI 打包**（[PR #4779](https://github.com/agentscope-ai/QwenPaw/pull/4779)）已进入 Ready for Merge，将彻底解决定时任务等依赖环境的痛点。

**基础设施自动化**
- 新增 GitHub Actions 工作流，在 PR 合并后自动维护贡献者列表数据（[PR #4692](https://github.com/agentscope-ai/QwenPaw/pull/4692)）。

---

## 4. 社区热点

- **🔥 最热讨论：桌面版打包疑惑 (`#4754`，7条评论)**
  用户对官方提供的两种客户端（原生版 vs Tauri 版）感到困惑，并寻求自打包为 EXE 的最佳方案。这暴露了文档与交付物差异对用户的困扰，而正在推进的 CLI 打包 PR（`#4779`）正是对此诉求的直接回应。
  [https://github.com/agentscope-ai/QwenPaw/issues/4754](https://github.com/agentscope-ai/QwenPaw/issues/4754)

- **🔔 强需求：记忆系统增强 (`#4652`，4条评论)**
  一份极为详尽的需求分析，批评当前记忆系统“只记录不提炼，踩了坑还会再踩”。用户期望 Agent 具备总结、状态标记、关联索引与智能提醒四大能力。这反映了高级用户对 Agent “智商”提升的深层渴望，极可能成为下阶段核心特性。
  [https://github.com/agentscope-ai/QwenPaw/issues/4652](https://github.com/agentscope-ai/QwenPaw/issues/4652)

- **❗ 核心稳定性：工具调用后 Agent 卡死 (`#4739`，6条评论)**
  用户报告 Agent 在任意工具调用后陷入“等待用户输入”的假死状态。此 Bug 严重破坏自动化工作流，是当前极其紧迫的稳定性雷区，截至目前尚未发现与之关联的 Fix PR。
  [https://github.com/agentscope-ai/QwenPaw/issues/4739](https://github.com/agentscope-ai/QwenPaw/issues/4739)

- **⭐ 路线图基石：AgentScope 2.0 后端迁移 (`#4727`，2 👍)**
  作为社区最关注的“Breaking Change”，该议题代表了底层的架构跃迁。尽管没有代码提交，但它决定了项目未来的扩展性与生命力，是社区各方开发者密切关注的核心决策点。
  [https://github.com/agentscope-ai/QwenPaw/issues/4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)

---

## 5. Bug 与稳定性

**严重 (Critical)**
- **[待修复]** **Agent 核心停滞：** 工具调用后 Agent 无法自主生成响应（`#4739`）。严重威胁自动化场景，需开发组优先排查。
- **[Won't Fix标记]** **数据丢失风险：** 服务重启导致当前会话最后几条消息丢失，根因已定位至 `shutdown_handler` 为空（`#4791`）。此问题标记为 `wontfix`，建议团队明确回应后续方案。
- **[待修复]** **频道断连：** OneBot 频道运行后频繁掉线且无法自动重连，端口停止监听（`#4788`）。

**中高 (Medium/High)**
- **[已有 Fix PR]** **上下文爆裂：** `tool_result_pruning` 对大体积 Shell 输出裁剪失效，导致上下文超限（`#4781`，修复 PR `#4787`）。
- **[已有 Fix PR]** **桌面版 CLI/PATH 异常：** 定时任务找不到 `qwenpaw` 命令，总是重装（`#4773`，修复 PR `#4779`）。
- **[待修复]** **桌面 Pet 功能异常：** 启动桌面宠物时终端无限循环但窗口不出现（`#4783`）。

**中低 / UI 类**
- **[已修复]** 安全页面 SVG 属性报错（`#4768`，修复于 PR `#4790`）。
- **[已反馈]** LaTeX 数学公式渲染异常（`#4756`）。
- **[已关闭]** `/skills` 指令首次触发失败（`#4784`）。

---

## 6. 功能请求与路线图信号

**短期可预见功能**
- **桌面版一键分发：** 用户对 [打包成 EXE] 的强烈需求（`#4754`）与正在合入的打包 CLI 的 PR（`#4779`）形成闭环，有望在下一版本解决部署痛点。
- **Coding Mode 生产力提升：** `#4762` (本地目录引用) 几乎已准备就绪。用户 `#4789` 甚至提出了类似 Trae 的高度集成化项目管理的畅想。
- **Token/上下文可视化：** 长期搁置的 PR `#4433` 与今天新开的 Issue `#4782` 遥相呼应，用户对资源消耗透明度的需求正在加强。

**中期路线图信号**
- **记忆系统重构（`#4652`）：** 作为 Agent 区别于聊天机器人的关键。
- **配置系统重构（`#4758`）与 Provider 自动降级（`#4757`）：** 提升系统可靠性与可维护性。
- **AgentScope 2.0 迁移（`#4727`）：** 上述所有功能的基础架构。

**持续性 UI/UX 优化需求**
- **会话列表优化：** 今天有多达 3 个 Issue（`#4747`、`#4732`、`#4770`）提及会话列表排序、点击面积和信息层级问题，这是用户最高频的交互场景，亟待优化。
- **定时任务管理：** `#4776` 与 `#4778` 指出静默执行、简化配置、关联名称等需求。

---

## 7. 用户反馈摘要

- **桌面版体验是当前最大短板：** 用户集中反馈了桌面版 v1.1.9 的细节问题（输入框残留、命令弹窗、列表无法排序、功能按钮灰色等）。桌面端与 Web 端的体验一致性亟待加强。
- **“可控性”与“智能性”是高级用户的永恒追求：** 专业用户对当前的“黑盒”行为感到不满，要求更透明的资源消耗（Token 用量）、更稳定的自动化流程（不掉线、不卡死）以及更聪明的记忆机制（不反复踩坑）。
- **社区新血活跃：** 今天出现了多位首次贡献者（`first-time-contributor`），如 `SnowTQ` 提交了 UI 闪烁与 SVG 修复，`wangfei010313` 提交了性能优化 PR。说明项目对新贡献者友好，且社区“自愈”能力较强。

---

## 8. 待处理积压

- **急待响应的核心 Bug：**
  - `#4739` (Agent 工具调用后卡死) 与 `#4788` (OneBot 断连) 是两块影响核心可信度的硬骨头，截至目前无关联的 Fix PR，建议维护团队尽快分配资源或给出临时解决办法。
  - `#4791` (重启丢失消息) 虽提供了详尽根因，但被团队标记为 `wontfix`。这对于生产环境用户是严重的体验降级，建议公开说明理由（如：受限于当前架构，计划随 2.0 重构解决）。

- **长期缺乏关注的 Feature PR：**
  - **`#4433` (Token 用量信息，5 月 15 日开启，Under Review)：** 已搁置两周，建议合并或给出具体修改意见。
  - **`#4655` (Chat V2 会话面板增强，5 月 25 日开启)：** 同样待审。
  
  Feature PR 的长时间积压容易冷却贡献者热情，建议定期安排 Code Review Time。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-05-29

## 1. 今日速览
过去 24 小时项目保持高速迭代：共处理 **20 条 Issue 更新**（19 条活跃、1 条关闭），**34 条 PR 更新**（3 条合并/关闭、31 条待合并）。无新版本发布。社区贡献踊跃，但 PR 合并率仅约 8.8%，存在一定审查积压；**S1 级别阻塞性 Bug 报告 3 个**，涉及 Slack 接入、配置写入与 OpenAI 兼容工具循环，需优先响应。整体健康度良好，`integration/zeroclaw-tui` 大合入 PR（#6848）正在收集反馈，预示 v0.8.0-beta-2 即将成形。

## 2. 版本发布
无。

---

## 3. 项目进展
今日有 3 项 PR 完成合并/关闭，推进了配置修复与模型支持：

| PR  | 说明 | 合并后影响 |
|-----|------|-----------|
| [#6908](https://github.com/zeroclaw-labs/zeroclaw/pull/6908) | `fix(onboard): add Codex subscription auth for OpenAI provider` | 使 ChatGPT Pro/Plus 用户可通过 OAuth 完成配置，无需手动输入 API Key |
| [#6994](https://github.com/zeroclaw-labs/zeroclaw/pull/6994) | `fix(slack): default strict_mention_in_thread to true` | 统一 @提及规则，避免线程内遗漏消息；已通过 serde-default 同步变更 |
| [#5650](https://github.com/zeroclaw-labs/zeroclaw/pull/5650) | `feat(provider): add native extended thinking for Anthropic provider` | 为 Anthropic 模型添加原生推理链支持（`budget_tokens` 配置），完善顶级模型兼容性 |

此外，核心开发者 **singlerider** 提交的 **[#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)（feat(integration): introduce zerocode TUI, RPC socket transport, DenyWithEdit approval）** 仍在开放讨论，该 PR 涵盖约 20 个组件改动，是 v0.8.0-beta-2 的基础，标志着项目向终端用户界面和安全审批能力迈出关键一步。

---

## 4. 社区热点

### 最受关注 Issue
- **[#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)（DeepSeek-V4 API 格式不兼容）**  
  共 **14 条评论**、4 个 👍。用户报告使用 DeepSeek-V4-Pro/Flash 时因 thinking mode 触发错误，S2 降级。讨论集中在 provider 适配层对新型推理参数的兼容性，反映社区对国产模型支持的迫切需求。

### 高讨论度 PR
- **[#6945](https://github.com/zeroclaw-labs/zeroclaw/pull/6945)（per-agent classifier_provider）** 允许为回复意图预检查指定廉价模型，降低运营成本，契合大型部署场景，引发配置灵活性讨论。
- **[#6985](https://github.com/zeroclaw-labs/zeroclaw/pull/6985)（report honest channel readiness）** 改造频道健康状态 API，提高可观测性，关注度较高。

### 诉求分析
社区主要诉求集中在 **配置精细化**（按 agent 指定分类模型、会话级覆盖）、**模型兼容性**（DeepSeek-V4、Anthropic opus-4-7）和 **开箱可用性**（WebSocket 启动失败、Slack 认证阻塞）。新增的 `file_download` 工具（#6957）亦反映出用户对 Agent 主动拉取外部资源的能力需求。

---

## 5. Bug 与稳定性

| 严重程度 | Issue/链接 | 描述 | 关联修复 PR |
|----------|-----------|------|-------------|
| **S1 - 工作流阻塞** | [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | `context_compression` 丢弃 tool_calls/tool 消息，导致 MiniMax 等 OpenAI 兼容 provider 陷入工具调用循环 | 状态 `in-progress`，暂无直接 PR |
| **S1 - 工作流阻塞** | [#6975](https://github.com/zeroclaw-labs/zeroclaw/issues/6975) | `zeroclaw onboard` 标记 sections 完成但未写入 `[agents.*]` 等配置段，初始引导失效 | 无 |
| **S1 - 工作流阻塞** | [#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992) | Slack Socket Mode 拒绝所有入站消息，报 "unauthorized user" | 无 |
| **S2 - 行为降级** | [#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) | DeepSeek-V4 因 thinking 参数不兼容出错 | 无 |
| **S2 - 行为降级** | [#6976](https://github.com/zeroclaw-labs/zeroclaw/issues/6976) | Web UI WebSocket 连接缺少 `?agent=` 参数，断开码 1006 | 无 |
| **S2 - 行为降级** | [#6991](https://github.com/zeroclaw-labs/zeroclaw/issues/6991) | v0.8.0-beta-1 工具序列化忽略 Risk Profile / Tool Filter 限制 | 无 |
| **S2 - 行为降级** | [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) | CLI 回退按字节删除，CJK 字符需三次 Backspace | 无 |
| **S2 - 行为降级** | [#6147](https://github.com/zeroclaw-labs/zeroclaw/issues/6147) | 确认 Anthropic opus-4-7 原生 API 是否会因 temperature 形状拒绝请求（保守 S2） | 无 |

**小结**：S1 级别三个 Bug 均缺少直接修复 PR，尤其 Slack 与 onboard 配置两项直接影响首次使用体验，建议维护者优先分配。S2 中 WebSocket 参数缺失已明确根因而易修复。

---

## 6. 功能请求与路线图信号

### 新提出的功能需求（今日 4 个）
| Issue/链接 | 摘要 | 可能纳入版本 |
|-----------|------|-------------|
| [#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) | 沙箱精细策略：文件系统与网络限制（RFC） | v0.9+（需 RFC 阶段） |
| [#6989](https://github.com/zeroclaw-labs/zeroclaw/issues/6989) | `#[secret]` 支持 `HashMap<String, String>`，统一 Bearer Token 脱敏 | v0.8.0-beta-2（PR #6988 涉及邻近模块） |
| [#6990](https://github.com/zeroclaw-labs/zeroclaw/issues/6990) | `file_download` 工具字符串需纳入 Fluent i18n | 紧耦合 PR #6957 |
| [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) | CLI 回退按 Unicode 簇删除 | 可 quick-fix |

### 已有 PR 配合的路线图信号
- **会话级覆盖**：`#6817 Session-scoped runtime overrides` 加上 `#6945 per-agent classifier_provider`，表明 v0.8.0 将引入粒度更细的运行时参数继承系统。
- **TUI 与用户体验**：`#6821 Move crates/zeroclaw-tui to apps/zerocode` ＋ `#6825 TUI UX tracker` ＋ `#6858 first-run empty states`，预期 beta-2 大幅改善终端交互。
- **工具扩展**：`#6957 file_download` 与 `#6985 channel readiness` 正在拓宽 Agent 的对外通道能力，强化可编程性。
- **异步沙箱策略**：#6996 RFC 虽然早期，但结合已有 Landlock/Bubblewrap 后端，反映出社区对安全隔离的持续关注。

---

## 7. 用户反馈摘要

| 用户/场景 | 反馈要点 | Issue 链接 |
|-----------|---------|-----------|
| **Telegram 用户**（#5470） | 使用 GPT-5.4 高推理模式时消息被重复存储到记忆，且存在自动更新问题 | [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) |
| **Web UI 用户**（#6976） | WebSocket 连接因缺少 `agent` 参数立即 1006，需要手动配置或自动补全 | [#6976](https://github.com/zeroclaw-labs/zeroclaw/issues/6976) |
| **首次使用用户**（#6975） | `zeroclaw onboard` 完成引导但无配置写入，导致启动失效，非常困惑 | [#6975](https://github.com/zeroclaw-labs/zeroclaw/issues/6975) |
| **CJK 用户**（#6995） | CLI 模式下 CJK 字符按字节删除，严重影响中文输入体验 | [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) |
| **Slack 管理员**（#6992） | Socket Mode 全部消息被拒绝，频道无法使用 | [#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992) |
| **审计/安全用户**（#6991） | 工具序列化绕过风险配置，导致风险管控失效 | [#6991](https://github.com/zeroclaw-labs/zeroclaw/issues/6991) |
| **i18n 社区**（#6548, #6990） | 硬编码英文字符串残留，新工具也未遵循 Fluent 本地化约定 | [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) [#6990](https://github.com/zeroclaw-labs/zeroclaw/issues/6990) |
| **Secrets 配置用户**（#6989） | `HashMap` 类型无法使用 `#[secret]` 脱敏，Bearer Token 暴露 | [#6989](https://github.com/zeroclaw-labs/zeroclaw/issues/6989) |

**共性痛点**：配置引导与生效一致性不足、非英语用户本地化缺失、高级特性（风险配置、多字节字符）边缘情况处理欠考虑。

---

## 8. 待处理积压

以下 Issue/PR 长期未得到响应或作者未回复，可能阻塞后续开发：

| 类型 | 编号/链接 | 描述 | 标记状态 | 搁置时长 |
|------|-----------|------|---------|----------|
| Issue | [#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570) | SQLite 向量搜索加速（ANN） | `status:stale` + `needs-author-action` | 50 天 |
| Issue | [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) | 安全运行时多个 Bug，需维护者复现 | `r:needs-repro` + `status:stale` | 52 天 |
| PR | [#5450](https://github.com/zeroclaw-labs/zeroclaw/pull/5450) | 工具 IPv6 支持与 url 规范化 | `needs-author-action` | 52 天 |
| PR | [#6428](https://github.com/zeroclaw-labs/zeroclaw/pull/6428) | Slack 线程上下文回填 | `needs-author-action` | 23 天 |
| PR | [#5187](https://github.com/zeroclaw-labs/zeroclaw/pull/5187) | CI 加入 arm64 Docker 目标 | `needs-author-action` | 58 天 |
| PR | [#6389](https://github.com/zeroclaw-labs/zeroclaw/pull/6389) | 九通道按接收方限速 | `needs-author-action` | 24 天 |

> **建议**：上述积压项涵盖了 **性能优化、CI 基础设施、核心通道功能**，建议维护者每周批量处理 `needs-author-action` 标签项，主动联系作者或接手完成。

---

*数据采集区间：2026-05-28 00:00 UTC – 2026-05-29 00:00 UTC；部分 Issue/PR 更新日期为 2026-05-28，已纳入统计。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*