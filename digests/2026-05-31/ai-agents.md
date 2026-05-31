# OpenClaw 生态日报 2026-05-31

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-31 03:31 UTC

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

**OpenClaw 项目动态日报 — 2026‑05‑31**

---

## 今日速览

过去 24 小时项目活跃度处于极高水位：共处理 500 条 Issue 更新（新开/活跃 427，关闭 73）和 500 条 PR 更新（待合并 317，已合并/关闭 183）。两个新版本（v2026.5.30‑beta.1、v2026.5.28）集中修复了 Agent 运行时恢复、飞书消息投递和 Codex OAuth 压缩等关键稳定性问题，但仍有多个 P1 级漏洞（如 Matrix 线程回复、Codex 超时）待解决。社区关注焦点集中在升级后通道功能失效和 Codex 集成可靠性上。

---

## 版本发布

### v2026.5.30‑beta.1  
- **核心修复**：Agent 与 CLI 运行时的工具中断、过期的会话绑定、压缩交接以及媒体投递重试场景下的恢复能力增强（相关 PR: #88129, #88136, #88141, #88162, #88182）。  
- **通道稳定**：Telegram、WhatsApp、iMessage、Slack 等通道的投递可靠性和移动端表现更平滑。  
- **破坏性变更**：无明确报告，但飞书和 Codex OAuth 配置在升级后需按文档重新检查。

### v2026.5.28  
- Agent/Codex 运行时：子代理保持 cwd/workspace 隔离、hook 上下文保持 prompt 本地化、会话锁超时释放、Codex app‑server/helper 失败时避免陈旧重启延续。  
- **迁移注意**：建议用户升级后运行 `openclaw doctor --fix` 以修复可能遗留的路由状态。

---

## 项目进展

今日共合并/关闭 183 个 PR，以下为已合并的高亮条目（来自 Top 30 展示列表）：

- **#79116** (CLOSED) — `feat(plugins): enrich before_dispatch hook with message and media metadata`  
  在 `before_dispatch` 钩子事件中增加消息和媒体元数据，使路由插件能更高效地处理文件附件。

- 其余重要 PR（仍为 OPEN 状态，但今日有显著活动或已进入最终审核）：
  - **#87072** — Telegram 可选交错进度通道 (interleaved progress lane)，将推理过程和运行时事件投影到一条持久消息中。
  - **#88238** — `perf(memory): batch memory embeddings across files`，批量索引内存嵌入以降低小文件开销。
  - **#88374** — `fix(gateway): honor signed node ids`，修复节点 ID 在配对、注册等环节中的签名验证问题。
  - **#88485** — `fix(agents): guard vanished workspaces`，防止工作区目录消失后静默重建导致状态丢失。

项目整体在 **Agent 稳定性、Telegram 交互体验和内存性能** 上迈出了明显步伐，大量 PR 正处于“等待维护者审查”状态，合并节奏保持快速。

---

## 社区热点

以下 Issue 在今日讨论最活跃、关注度最高：

1. **#87646** (12 评论, 👍 1) — 【飞书】升级 v2026.5.27 后消息投递失败：`TypeError: Cannot read properties of undefined (reading 'run')`  
   **状态**: CLOSED（已修复）。用户报告升级后机器人无法投递私信，社区反馈集中，最终通过新版本修复。

2. **#86820** (12 评论, 👍 6) — 【Codex】OAuth 压缩回退到直接 OpenAI API 且缺少 API Key 时失败  
   **状态**: CLOSED。关注热度最高，表明 Codex OAuth 工作流是多数用户的核心路径。

3. **#73424** (9 评论, 👍 1) — 【图像工具】JPEG 分析时 “Failed to optimize image”  
   **状态**: OPEN。持续一个月的旧问题，虽然有模型直连正常，但内置 tool 仍然失败，用户期待修复。

4. **#87307** (8 评论, 👍 1) — 【Matrix】2026.5.22 回归：线程回复变成普通回复，`/status` 和 `/model` 静默  
   **状态**: OPEN。Matrix 用户的日常体验受明显影响，急需 P1 级跟进。

5. **#88234** (5 评论, 创建于 2026‑05‑30) — 【飞书】新报告：`TypeError: Cannot read properties of undefined (reading 'run')`  
   **状态**: OPEN。与 #87646 症状相同，但用户反馈在最新版本仍出现，提示修复可能不完整或存在变种。

**社区诉求核心**：升级后的通道兼容性（飞书、Matrix、Codex）是最为集中的痛点，用户期望项目在版本发布前覆盖更全面的回归测试。

---

## Bug 与稳定性

按严重程度（P1 > P2 > stale）排列，标注是否已有修复 PR（Fix PR）。

| 等级 | Issue | 描述 | 状态 | Fix PR |
|------|-------|------|------|--------|
| P1 | #88020 | REPLAY_INVALID_RE 缺少 Anthropic thinking 签名错误，导致硬失败而非恢复重试 | **OPEN** | 未关联 |
| P1 | #87744 | Codex Telegram 超时：turn 永远不变成 completed，会话失败 | **OPEN** | 未关联 |
| P1 | #88234 | 飞书 dispatch `read property 'run'` TypeError（新出现） | **OPEN** | 未关联 |
| P1 | #87646 | 飞书 dispatch 错误（已关闭，但用户疑似仍遇到） | **CLOSED** | 已包含在 v2026.5.30‑beta.1 |
| P1 | #86820 | Codex OAuth 压缩降级失败 | **CLOSED** | 已修复 |
| P1 | #87307 | Matrix 线程回复回归 | **OPEN** | 未关联 |
| P1 | #86996 | Active Memory + Codex 导致长延迟、hook 超时、事件循环阻塞 | **OPEN** | 未关联 |
| P2 | #88352 | Codex 瞬态/新鲜 no‑context‑engine 启动丢失先前会话上下文 | **OPEN** | PR #88262 已合并但有新问题 |
| P2 | #87801 | `supportsAdaptiveThinking()` 遗漏 opus‑4‑8 → reasoning 开启导致 400 | **OPEN** | 未关联 |
| P2 | #87436 | Codex harness 在 `doctor --fix` 后重建旧的路由状态 | **CLOSED** | 已修复 |
| P2 | #65156 | Memory 向量搜索 sqlite‑vec ABI 不匹配 | **OPEN** | 未关联 |
| P2 | #73814 | 安装脚本 `curl | bash` 因 stdin 消费而挂起 | **OPEN** | 未关联 |
| stale | #73424 | 图像工具 “Failed to optimize image” | **OPEN** | 未关联 |
| stale | #76315 | Linux 下子 Agent 负载导致网关不稳定、WhatsApp 408 | **OPEN** | 未关联 |
| stale | #74907 | 多工具回合重放产生孤立 tool_use 块 | **OPEN** | 未关联 |

今日新增了 **#88234、#88352、#88327** 等 Bug，多数回归与 Codex 和飞书相关。

---

## 功能请求与路线图信号

### 用户高频新需求（来自 Issue）
- **#86169** — 添加 Xiaomi MiMo Token Plan 原生支持（👍 1，8 评论）  
- **#73699** — Discord 语音通道桥接到文本会话（voice‑as‑IO）  
- **#75074** — `/v1/responses` 输出中暴露内建工具调用（便于 eval）  
- **#76952** — 完善 Realtime Talk 文档与手机/电话桥接选项（用户表示功能“低延迟且实用”）  
- **#72950** — 插件配置支持环境变量或可写覆盖路径（在 Landlock 策略锁定场景中有刚需）

### 很可能进入下一版本的功能（对应早期或活跃 PR）
- **#81851** — `claude-cli-interactive` 后端，通过本地 TLS 代理流式输出推理（P1，已经过展示证明）  
- **#87072** — Telegram 交错进度通道（已进入等待维护者审查）  
- **#88212** — `localModelLean: "auto"` 自动裁剪小模型工具，避免爆上下文  
- **#88504** — 多槽记忆角色架构（`memory.recall`, `memory.compaction` 等），支持记忆插件组合  
- **#88477** — 控制 UI Projects 面板 + SNES 工作室界面（重量级 Dashboard 改善）  
- **#88507** — 插件槽位支持带所有者记录的对象形式（从单一 ID 升级为 `{owner, config}`）

路线图信号：项目正从“单一记忆插件”转向**多槽组合架构**，Telegram 和 Web UI 的交互层在快速完善，并开始支持更多国产平台（小米、飞书等）。

---

## 用户反馈摘要

从 Issue 评论中提炼的真实用户声音：

- **飞书用户（#87646, #88234）**：  
  “升级后机器人连接正常也能收消息，但 dispatch 立即崩溃——**TypeError: read property 'run' of undefined**。尝试重启、回退均无效，生产环境完全不可用。希望修复尽快合入稳定版。”

- **Codex 用户（#86820, #87744）**：  
  “使用 `openai/gpt-5.5` + Codex OAuth 时 compaction 直接报 Missing API key，只能换回旧配置。而 Telegram 上 Codex 持续 ‘**timeout waiting for turn/completed**’，重试 5 次都失败，用户消息被吞。”

- **Matrix 用户（#87307）**：  
  “2026.5.22 升级后 Thread 回复全部变成普通回复，而且 bot 不再响应 `/status` 和 `/model`。**这让我们团队无法正常使用 Matrix 频道**。”

- **Realtime Talk 用户（#76952）**：  
  “低延迟、真正实用。但文档缺乏 voice‑agent role 和 mobile 桥接的说明，希望能尽快补上。”

- **Windows 用户（#76884, #79099）**：  
  “每个新版本在 Windows 上**越来越慢**，`gateway probe` 一直报告 unreachable 但 health 正常，排查困难。”

- **性能关注者（#86996）**：  
  “同时启用 Active Memory + Codex + lossless‑claw， Telegram 消息延迟从 2 秒飙升到 40+ 秒，甚至导致 gateway 重启。”

整体情绪：项目功能强大（特别是 Real-time Talk 和 Codex），但**升级后稳定性退化**是用户最大的不满来源；文档和 Windows 体验存在明显短板。

---

## 待处理积压 ⏳

以下长期未响应的 Issue 涉及核心稳定性或用户高频场景，建议维护者优先分配资源：

| Issue | 创建时间 | 最后更新 | 详情 | 优先级建议 |
|-------|----------|----------|------|------------|
| #73424 | 2026‑04‑28 | 2026‑05‑30 | 图像优化失败（JPEG），9 条评论 | **高**（常见媒体操作阻塞） |
| #76315 | 2026‑05‑02 | 2026‑05‑30 | Linux 下子 Agent 负载导致网关不稳定、WhatsApp 408 | **高**（直接影响多用户部署） |
| #75739 | 2026‑05‑01 | 2026‑05‑30 | Codex harness 路由迁移两个相关 Bug | **中高**（阻碍 Codex 标准化配置） |
| #74907 | 2026‑04‑30 | 2026‑05‑30 | 多工具回合重放产生孤立 tool_use 块，7 条评论 | **中高**（长期会话必现） |
| #73814 | 2026‑04‑28 | 2026‑05‑30 | `curl | bash` 安装挂起，新用户首次体验受影响 | **中**（影响新用户转化） |
| #72950 | 2026‑04‑27 | 2026‑05‑30 | 插件配置无环境变量/覆盖路径（Landlock 只读环境） | **中**（企业部署需求） |
| #65156 | 2026‑04‑12 | 2026‑05‑30 | Memory 向量搜索 sqlite‑vec ABI 不匹配 | **中**（记忆功能折损） |

这些 Issue 的评论数和赞数都维持高水平，却长时间无标签推进或指派。建议在 2026 年 6 月第一周进行集中 triage。

---

## 横向生态对比

好的，作为一名专注 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是我基于您提供的 2026-05-31 各项目动态，生成的横向对比分析报告。

---

# 个人 AI 助手开源生态横向对比分析报告（2026-05-31）

---

## 1. 生态全景

2026年5月31日的数据表明，个人AI助手与自主智能体开源生态正处于 **高度活跃但分化加速** 的阶段。以 OpenClaw、Hermes Agent、IronClaw 为代表的核心项目每日处理数百项 Issue 与 PR，快速迭代新功能，生态“头部效应”显著。社区关注焦点已从基础对话能力全面转向 **生产级可靠性**（通道稳定、升级兼容）、**安全与权限精细化管理**（工具白名单、MCP沙箱），以及 **多模态与自主交互**（桌面控制、语音双工）。然而，版本回退、平台兼容性（尤其是 Windows 与 macOS）以及长期积压的待修复 Bug 仍是各项目面临的共性挑战，用户对“可用的稳定版”诉求强烈。

---

## 2. 各项目活跃度对比（2026-05-31）

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|------|--------------|-----------|----------|------------|
| **OpenClaw** | 500 | 500 | 2 (v2026.5.30-beta.1 / v2026.5.28) | 🔴 极高 |
| **Hermes Agent** | ~50 (合计100) | ~50 (合计100) | 无 | 🔴 极高 |
| **IronClaw** | 4 | 18 | 无 | 🔴 极高 |
| **PicoClaw** | ≥4 (关闭4) | ≥3 (合并3) | 1 (nightly) | 🔴 极高 |
| **ZeroClaw** | 50 | 50 | 无 | 🟡 高 |
| **NanoClaw** | 3 | 16 | 无 | 🟡 高 |
| **NanoBot** | 6 | 15 | 无 | 🟡 高 |
| **CoPaw** | 9 | 1 | 无 | 🟢 中等 |
| **Moltis** | 0 | 1 | 无 | 🟢 中等 |
| **LobsterAI** | 0 | 2 (仅更新) | 无 | 🔵 低 |
| **NullClaw** | 0 | 0 | 无 | ⚪ 停滞 |
| **TinyClaw** | 0 | 0 | 无 | ⚪ 停滞 |
| **ZeptoClaw** | 0 | 0 | 无 | ⚪ 停滞 |

*注：Hermes Agent 合计100项为 Issue+PR 总更新数；PicoClaw 数字仅含关闭/合并项，实际新开可能更多。*

---

## 3. OpenClaw 在生态中的定位

- **优势**：OpenClaw 拥有生态内最大的社区规模（日处理 500+ 条更新），版本迭代最密集，渠道覆盖最广（Telegram、WhatsApp、iMessage、飞书、Matrix 等）。其插件体系与 hook 机制成熟，是多数新项目功能设计的参照基准。
- **技术路线差异**：相比 IronClaw（Rust， Reborn 架构重写）追求极致性能与类型安全，OpenClaw 采用 Python/Node 混合，强调快速功能落地与社区贡献者友好。与 ZeroClaw 侧重桌面原生控制不同，OpenClaw 更侧重通道抽象与 Agent 运行时恢复。
- **社区规模对比**：从 Issue/PR 绝对数量看，OpenClaw 是 IronClaw 的 25 倍以上、Hermes 的 5 倍左右，处于生态绝对核心位置。但高活跃也带来维护压力，其 P1 级漏洞与回归 Bug 数量同样高企（7 个 P1 仍 OPEN），反映其快速迭代与稳定性间的张力。

---

## 4. 共同关注的技术方向

| 技术方向 | 具体诉求 | 涉及项目 |
|----------|----------|----------|
| **通道兼容性与稳定性** | 飞书/Matrix 升级后投递失败、线程回复回归、WhatsApp 超时、Webhook Retry-After 解析 | OpenClaw, NanoBot, Hermes, ZeroClaw, CoPaw, PicoClaw |
| **工具权限与安全** | 精细化 RBAC、MCP 工具首次调用审核、`allowed_tools` 未强制执行、子任务默认拒绝策略、提示注入检测 | Hermes, ZeroClaw, IronClaw, NanoClaw, PicoClaw |
| **记忆系统进化** | 从单一自动记忆转向手动模式 + RAG 检索、多槽组合架构、本地知识图谱作为真实来源 | NanoBot, OpenClaw, Hermes, IronClaw |
| **桌面控制与多模态** | computer-use（截图+键鼠），图片拖拽/粘贴上传，语音双工（VAD+STT），macOS 权限流 | ZeroClaw, OpenClaw, Hermes, CoPaw, PicoClaw |
| **MCP 生态安全与可靠性** | 服务器自动安装导致供应链风险（密码勒索），断连后无法自动重连，凭据管理统一 | NanoClaw, Hermes, IronClaw, LobsterAI |
| **发布与 CI 可靠性** | crates.io 发布缺失阻塞安全更新，Nightly E2E 持续失败，Docker 无限重启，升级后功能退化 | IronClaw, Hermes, PicoClaw, OpenClaw |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键特征 |
|------|----------|----------|------------------|
| **OpenClaw** | 全功能平台：多通道、插件、Agent 编排 | 个人开发者、社区用户、多场景部署 | Python/Node 混合，插件 Hook 系统，记忆槽组合 |
| **Hermes Agent** | 企业级安全：精细化 RBAC、Tirith 策略、多 Provider | 安全敏感的企业/团队 | Python，TUI+Desktop，自带安全扫描，强权限模型 |
| **IronClaw** | 高性能底层引擎：触发引擎、产品级认证、Rust 类型安全 | 高级用户、核心贡献者、自建基础设施 | Rust，Reborn 架构重写，crates.io 组件化 |
| **ZeroClaw** | 桌面原生控制 + 语音双工：macOS 权限、computer-use | 追求桌面自主化的个人用户 | Python，TUI+WebUI+VAD 管线，强桌面集成 |
| **NanoBot** | 简洁可靠：Matrix E2EE、Heartbeat 管理、轻量记忆 | 重视稳定与低噪音的个人/团队 | Python，Dream 记忆系统，社区响应快速 |
| **NanoClaw** | 多实例高性能：单机多用户隔离、IPC 事件驱动 | 家庭/小团队多用户共享 Mac | Python，多实例配置，`fs.watch` 事件驱动 |
| **PicoClaw** | 边缘轻量 + 国际化：Azure Identity、孟加拉语、QQ | 中文与新兴市场用户、边缘设备 | 轻量级，快速支撑新渠道与语言 |
| **CoPaw** | Windows 场景 + 中文生态 | 中文 Windows 用户、量化交易 | 强调 ACP 协议兼容，隐藏工作目录提议 |
| **Moltis** | Provider 兼容层细化 | 使用非标准 API 的开发者 | 专注 Codex 流式参数修复 |
| **LobsterAI** | 开发者工具（MCP 配置快捷键） | 使用 IDE/MCP 的开发者 | Electron 桌面端，macOS 原生适配 |

---

## 6. 社区热度与成熟度分层

- **快速迭代阶段（极高活跃）**：OpenClaw、Hermes Agent、IronClaw、PicoClaw、ZeroClaw  
  这些项目每日合并大量 PR，新功能密集落地（如 IronClaw 的 Reborn 架构、ZeroClaw 的语音双工），同时 Bug 修复速度较快，但 P1/P0 级问题仍时有暴露，用户面临升级风险。

- **质量巩固阶段（高活跃）**：NanoBot、NanoClaw、CoPaw、Moltis  
  项目更侧重修复既有问题（NanoBot 的并发锁、Matrix 验证），社区反馈响应积极，但新功能推进相对克制，整体成熟度稳步提升。

- **停滞/风险阶段（低活跃或无活动）**：LobsterAI、NullClaw、TinyClaw、ZeptoClaw  
  LobsterAI 已有修复 PR 积压 57 天未合入，社区贡献者耐心面临考验；其余项目近 24 小时完全无活动，维护状态不明，或已不再活跃开发。

---

## 7. 值得关注的趋势信号

1. **“安全即功能”成为企业采纳的前提**  
   Hermes 的 RBAC 诉求、ZeroClaw 的 `allowed_tools` 执行失效、IronClaw 的子任务默认拒绝、NanoClaw 的 MCP 供应链争议，共同指向 **没有精细权限控制的生产级框架将失去企业用户**。开发者应将安全架构（沙箱、审批流、策略引擎）纳入核心设计。

2. **记忆系统从“黑盒自动”走向“用户可控+RAG”**  
   NanoBot 的手动模式 + 轻量 RAG、OpenClaw 的多槽组合、Hermes 的“大脑即真实来源”均表明，社区不再满足于单一自动记忆，期待 **语义检索、结构化融合与用户显式控制**。这是代理长期记忆落地的关键演变。

3. **多通道稳定性是信任基石，回归测试不可缺失**  
   OpenClaw 的飞书/Matrix 回归、ZeroClaw 的 WhatsApp 修复、CoPaw 的 ACP 协议失败反复出现，且用户情绪强烈。项目应建立 **核心通道的自动化回归测试套件**，避免“升级即破坏”的恶性循环。

4. **桌面控制与语音双工是下一代人机界面**  
   ZeroClaw 的 computer-use 与双工语音、OpenClaw 的 Realtime Talk、NanoBot 的 STT 可配置化，显示 Agent 正从“文本对话”转向 **多模态自主交互**。建议开发者关注 WASM 插件、VAD 管线与操作系统权限 API 提前布局。

5. **发布工程与 CI 健康度影响社区信心**  
   IronClaw 的 crates.io 缺失（0.24→0.27 跳跃）导致下游用户受 CVE 影响，Nightly E2E 持续失败；PicoClaw 的 v0.2.9 回归 Bug 未在发布前拦截——这些事件提醒我们，**自动化发布管道与持续回归测试** 是大型项目维持用户信任的必备基础设施，值得优先投资。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是基于 NanoBot 项目 2026-05-31 日 GitHub 数据生成的动态日报。

---

# NanoBot 项目动态日报 | 2026-05-31

---

## 1. 今日速览
今日项目活跃度维持高位，共处理 6 条 Issues（关闭 4 条）和 15 个 Pull Requests（合并/关闭 6 个）。项目在**稳定性修复**和**功能扩展**上双线推进：社区痛点的 Matrix E2EE 兼容性问题、Agent 并发锁缺陷均得到修复，多任务并发的修复 PR 也已提出。同时，内存系统的手动模式与 RAG 检索、新语音转录提供商等前瞻性功能正在积极开发中，项目整体健康度良好，社区响应迅速。

---

## 2. 版本发布
**无。** 今日无新版本发布。

---

## 3. 项目进展
今日多个重要 PR 被合并，项目的稳定性和可用性显著提升：

- **核心并发稳定性加固**：`#4104` 被合并，修复了 `process_direct()` API 绕过会话级分发锁的严重缺陷。此前直接调用（API/WebUI/SDK）可能与消息总线并发处理同一会话，导致历史混乱。此修改为所有外部入口增加了统一的锁机制。
- **Matrix 通道兼容性修复**：`#4110` 被合并，解决了 Element X 客户端 E2EE “未验证设备” 警告问题。现在通过配置可开启 SAS 设备验证握手。
- **安全修复**：`#4086` (SSRF IPv6 映射地址检查) 与 `#4106` (Matrix 媒体下载上限) 被合并，进一步降低了攻击面。
- **WebUI 体验升级**：`#4108` 被合并，重新设计了 Agent 输出时间线渲染，优化了文件编辑行、媒体预览和代码渲染，并添加了提示词队列编辑与持久化功能。
- **核心配置优化**：`#4054` 被合并，为 Dream 系统作业添加了 `enabled` 开关（默认 true），解决了用户无法禁用后台记忆整理作业的痛点；同时修复了 Anthropic 内容块缺少 `type` 字段的兼容性问题。

---

## 4. 社区热点

- **Heartbeat 误报通知（[#4111](https://github.com/HKUDS/nanobot/issues/4111)）**
  这是今日最受关注的 Bug 报告。用户反馈 Heartbeat 定时任务在无任务时仍向飞书推送 “All clear.” 消息，造成信息噪音。该话题在一天内直接催生了两份修复 PR（[#4112](https://github.com/HKUDS/nanobot/pull/4112)、[#4114](https://github.com/HKUDS/nanobot/pull/4114)），体现了社区对消息质量和低噪音的刚性需求。
- **Dream 系统作业全局开关（[#3885](https://github.com/HKUDS/nanobot/issues/3885)）**
  尽管该 Issue 已关闭，但其获得了 4 条评论并最终被采纳。用户希望获得对 Agent 自主行为的绝对控制权，该诉求快速落地为 `enabled` 配置项。这表明项目方对用户可控性（User Agency）的重视。

---

## 5. Bug 与稳定性

| 严重程度 | 状态 | 问题 | 修复 PR |
|---|---|---|---|
| **高** | **已修复** | `process_direct` 绕过会话分发锁，引发并发数据损坏 ([#4080](https://github.com/HKUDS/nanobot/issues/4080)) | [#4104](https://github.com/HKUDS/nanobot/pull/4104) |
| **高** | **已修复** | Matrix 通道未处理 SAS 设备验证，Element X 用户无法清除未验证设备警告 ([#4042](https://github.com/HKUDS/nanobot/issues/4042)) | [#4110](https://github.com/HKUDS/nanobot/pull/4110) |
| **中** | **已有修复 PR** | Heartbeat 定时任务在无任务时错误发送 “All clear.” 通知到飞书 ([#4111](https://github.com/HKUDS/nanobot/issues/4111)) | [#4114](https://github.com/HKUDS/nanobot/pull/4114), [#4112](https://github.com/HKUDS/nanobot/pull/4112) |
| **低** | **已修复** | Anthropic 提供者要求内容块必须声明 `type`，裸字典返回导致 API 拒绝 ([#3993](https://github.com/HKUDS/nanobot/issues/3993)) | [#4054](https://github.com/HKUDS/nanobot/pull/4054) |
| **中** | **已修复** | SSRF 检查中 IPv6 映射的 IPv4 地址未能被正确识别为私有地址 ([#4086](https://github.com/HKUDS/nanobot/pull/4086)) | 已在 PR 中修复 |
| **中** | **已修复** | Matrix 通道未对入站媒体下载设置上限，存在资源耗尽风险 ([#4106](https://github.com/HKUDS/nanobot/pull/4106)) | 已在 PR 中修复 |

---

## 6. 功能请求与路线图信号

- **下一代内存系统 🌟**：
  - **手动内存模式（[#4050](https://github.com/HKUDS/nanobot/pull/4050)）**：提议推出手动内存模式，与现有的自动 Dream 作业隔离。此为对 #3885 诉求的深化方案。
  - **轻量级 RAG 检索（[#4109](https://github.com/HKUDS/nanobot/pull/4109)）**：提议基于本地 embeddings 实现内存的轻量级检索增强生成。
  **信号分析**：结合来看，项目正在从单一的自动记忆（Dream）转向更灵活、用户可控、支持语义检索的复合记忆系统，这将是未来几个版本的核心亮点。
- **STT 模型可配置化（[#4113](https://github.com/HKUDS/nanobot/pull/4113)）**：提议为语音转录添加自定义 `transcriptionModel` 设置，并新增 OpenRouter 作为提供商，减少对单一 API 的依赖。语音交互的灵活度有望大幅提升。
- **沙箱环境可配置化（[#4107](https://github.com/HKUDS/nanobot/issues/4107)）**：用户要求允许为 `bwrap` 沙箱自定义绑定挂载路径。这一需求来自高级用户，旨在解决沙箱环境与本地开发环境路径不一致的问题。
- **标准化协议支持（[#4034](https://github.com/HKUDS/nanobot/pull/4034)）**：虽标记为 `duplicate`，但添加 GitAgent 协议的支持体现了社区对 Agent 互操作性的期待。

---

## 7. 用户反馈摘要

- **满意的反馈**：
  - 用户 `codeLong1024` 提出的 Dream 作业开关需求得到快速响应，其诉求确保了用户可以完全掌控 Agent 后台行为。
  - 用户 `PaddyPatPat` 详细报告了 Matrix 验证难题，该问题在 **1-2 天**内即被修复，维护了项目对核心信道的可用性承诺。
- **痛点和不满**：
  - **消息噪音：** `CashSoldier` 报告 Heartbeat 在空载时发送 “All clear.” 造成困扰，这代表用户对 AI 助手输出的“简洁性”和“价值”有很高期待，不希望收到无意义的消息。
  - **沙箱灵活性不足：** `Kyakui` 指出 bwrap 沙箱的硬编码挂载路径限制了很多高级工具的运行，需要更细粒度的配置。
  - **兼容性问题：** `mraad` 反馈了 Anthropic API 类型校验过于严格导致错误的场景（该问题当日已修复）。

---

## 8. 待处理积压

以下 PR/Issue 已保持多日未获得核心维护者的明确反馈或合并，可能成为项目潜在的瓶颈：

- **Provider 配置重构（[#3994](https://github.com/HKUDS/nanobot/pull/3994)，6 天无更新）**：涉及 WebUI 和 Bedrock 提供商配置字段的重大重构，将大幅提升扩展性。建议维护者尽快审核，避免与后续 Provider 开发产生大量冲突。
- **Token 预热优化（[#3997](https://github.com/HKUDS/nanobot/pull/3997)，6 天无更新）**：共享 `tiktoken` 实例并预热，对于减少首次消息延迟有显著效果。长期未合并可能影响高并发场景下的用户体验。
- **GitAgent 协议支持（[#4034](https://github.com/HKUDS/nanobot/pull/4034)，3 天，标记 `duplicate`）**：该项目被标记为重复但未被关闭。如果项目有意支持标准化 Agent 协议，应给予明确指引；如果不在规划内，应给予明确回复并关闭 PR，避免贡献者等待。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 (2026-05-31)

**数据来源:** GitHub (NousResearch/hermes-agent)
**报告生成日期:** 2026-05-31

---

### 1. 今日速览

Hermes Agent 项目今日保持极高活跃度，Issues 与 PRs 合计更新 **100** 项。社区对**精细化工具权限系统**（#21849 / #33905 / #35479）的呼声达到峰值，形成了今日最强烈的功能诉求集群。稳定性和兼容性方面，v0.15 版本引入了两项令社区敏感的核心回归问题（#35595 `/model` 显示异常、#35393 Docker 循环重启），好在后者的修复已关闭。核心维护者正集中精力处理 **Anthropic 历史记录损坏**（P1, PR #35586），该 PR 质量较高，预计近期合入。今日无版本发布，但项目在**桌面端**、**TUI 稳定性**及**模型列表更新**方面均有实质性 PR 推进，整体迭代强度可观。

---

### 2. 版本发布

无新版本发布。

---

### 3. 项目进展 (今日合并/关闭的重要 PR 与 Issue)

今日共合并/关闭 **10 个 PRs** 和 **9 个 Issues**，主要集中在稳定性修复和桌面端体验基建上：

**桌面端与 TUI 体验**
- **[PR #35607] [CLOSED]**: macOS 桌面端安装与自更新链路闭环，统一了 Tauri 安装器与 Python 运行时路径，解决了生产环境安装失败的问题。([链接](https://github.com/NousResearch/hermes-agent/pull/35607))
- **[PR #35512] [CLOSED]**: 修复 TUI 在工具调用期间被终端鼠标噪音序列锁死的问题，大幅提升 Windows Terminal 等高噪音场景下的体验。([链接](https://github.com/NousResearch/hermes-agent/pull/35512))
- **[PR #35501] [CLOSED]**: 新增皮肤驱动的启动横幅模式（支持 Claude 风格），提升了 CLI 启动的美观度与个性化能力。([链接](https://github.com/NousResearch/hermes-agent/pull/35501))

**核心 Agent 稳定性**
- **[Issue #35543] [CLOSED]**: 紧急修复跨提供商切换（如 DeepSeek → Cerebras）时，因历史记录残留 `reasoning_content` 导致 HTTP 400 的问题。([链接](https://github.com/NousResearch/hermes-agent/issues/35543))
- **[Issue #33580] [CLOSED]**: 修复 `kanban_db` 连接泄漏导致 macOS 上文件描述符耗尽（`Too many open files`）的稳定性 Bug。([链接](https://github.com/NousResearch/hermes-agent/issues/33580))
- **[Issue #34202] [CLOSED]**: 修复 Dashboard 在 loopback 模式下的无限页面重载循环。([链接](https://github.com/NousResearch/hermes-agent/issues/34202))
- **[Issue #35393] [CLOSED]**: 解决了 v0.15 在 Docker (s6-overlay) 环境下因信号异常导致无限重启的问题。([链接](https://github.com/NousResearch/hermes-agent/issues/35393))

**Kanban 与工作流**
- **[PR #35662] [OPEN]**: 修复归档父任务时未能清理 `task_links` 记录，子工作线指向已删除 `workspace_path` 的问题。([链接](https://github.com/NousResearch/hermes-agent/pull/35662))

---

### 4. 社区热点 (高互动 Issues/PRs 与背后诉求)

**1. 跨平台会话延续 — Issue #8366**
- 状态: 💬4, 👍6 (过去24小时评论次数最多)
- **诉求分析**: 用户期望在 CLI（桌面）、Telegram（路途）、iMessage 之间无缝切换任务。当前各平台会话孤立，导致工作流断裂，是高频用户的刚需体验优化。
- **链接**: `https://github.com/NousResearch/hermes-agent/issues/8366`

**2. 工具权限系统 — Issue #21849 / #33905 / #35479**
- 状态: 社区呼声最集中的功能簇（共 3 条相关 Issues）
- **诉求分析**: 当前权限仅对“危险 shell 命令”生效。用户希望按单个工具/工具集/数据源设置审批策略，特别是“对同事开放文档 QA 但阻止终端操作”的协作场景。“全有或全无”是企业用户拒绝采用的核心理由。
- **链接**: `https://github.com/NousResearch/hermes-agent/issues/21849`

**3. MCP 安全与可靠性 — Issue #16462 / PR #35661**
- **诉求分析**: MCP 服务器工具缺乏首次调用审核节点，LLM 可直接调用；同时 MCP 服务器断连后无法自动重连（PR #35661 已提出修复，防止永久断连）。生态成熟度的关键瓶颈。
- **链接**: `https://github.com/NousResearch/hermes-agent/issues/16462` / `https://github.com/NousResearch/hermes-agent/pull/35661`

**4. 大脑即真实来源 — Issue #27657**
- 状态: 💬3, 讨论密集
- **诉求分析**: 用户希望将本地已有知识库（`/home/shlee/Brain`）作为 Agent 长期记忆的“真实来源”，而仅在需要时归档进 Hermes。体现社区对记忆架构的第二阶段需求——从序列记忆转向结构化知识融合。
- **链接**: `https://github.com/NousResearch/hermes-agent/issues/27657`

---

### 5. Bug 与稳定性 (按严重程度排列)

**P0 — 严重安全风险**
- **[#35584]** Gateway 在文件守卫拒绝写入后，通过 `extract_local_files` 将 `config.yaml` 路径暴露给 Agent，存在凭据泄漏风险。 **（需紧急处理）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35584))

**P1 — 核心功能崩溃/回归**
- **[#17861]** 多轮会话中 Anthropic `thinking/redacted_thinking` 块未被保留，恢复后引发 API 400 错误。 **→ PR #35586 已提交修复** ([链接](https://github.com/NousResearch/hermes-agent/issues/17861) / [PR #35586](https://github.com/NousResearch/hermes-agent/pull/35586))
- **[#35595]** v0.15 回归：`/model` 命令返回结构化字段名而非人类可读信息，破坏了基本模型切换交互。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35595))
- **[#35543]** 历史记录跨提供商污染。 **（已关闭，修复已应用）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35543))
- **[#35393]** Docker 容器在 s6-overlay 下无限重启。 **（已关闭）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35393))

**P2 — 功能阻塞 / 体验严重受损**
- **[#33961]** CLI `/new`/`/clear`/`/reset` 导致终端完全挂起，Ctrl+C 无法中断。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/33961))
- **[#35576]** Gateway 重启恢复会话时，飞书旧 `thread_id`（消息已撤回）导致消息发送失败，无优雅降级。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35576))
- **[#35654]** Windows 下 `browser_tool` 的 URL 中含 `&` `|` 等 shell 元字符时，策略评估失败/截断。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35654))
- **[#28291]** `moonshot_schema._fill_missing_type` 对 JSON Schema 联合类型 `type: ["number", "string"]` 崩溃（`unhashable type: 'list'`）。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/28291))
- **[#32737]** Tirith 安全扫描器对 `本地脚本 | python3` 模式误报 HIGH 风险，影响正常开发工作流。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/32737))
- **[#5129]** 后台记忆审查创建完整 AIAgent 克隆，导致内存/数据库提供者重复初始化，影响长期运行稳定性。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/5129))
- **[#35652]** TUI 多会话环境下，后台进程通知可能投递至错误窗口。 **（待修复）** ([链接](https://github.com/NousResearch/hermes-agent/issues/35652))
- **[#35661]** MCP 服务器重连逻辑缺陷：重连次数达到上限后永久断连。 **→ PR #35661 已提交修复** ([链接](https://github.com/NousResearch/hermes-agent/pull/35661))

---

### 6. 功能请求与路线图信号

结合今日提交的 Issues 与活跃 PRs，以下功能请求具备高路线图优先级：

**🔴 最高优先级信号：精细化权限系统 (RBAC)**
- #21849, #33905, #35479
- **路线图判断**: 社区诉求已形成集群效应，且是阻碍企业部署的核心瓶颈。预计 v0.16 必须引入某种形态的 `per-tool` / `per-user` 审批策略。PR 暂无，但代码库工具定义层已有铺垫。

**🟡 高优先级：国际化与多身份认证**
- **PR #35127 [OPEN]**: 完整的 YAML 语言包 + 区域化配置系统。i18n 分支改动量较大但机制优雅，适合大版本发布。([链接](https://github.com/NousResearch/hermes-agent/pull/35127))
- **PR #27601 [OPEN]**: Webhook 新增 `Bearer Token` 认证。已有 HMAC/GitLab Token，补全标准认证方式提升可集成性。([链接](https://github.com/NousResearch/hermes-agent/pull/27601))

**🔵 高价值特性：上下文与记忆进化**
- **#20717**: “动态上下文裁剪”——让 Agent 主动管理历史窗口，而非被动的截断式压缩。
- **#27657**: “大脑即真实来源”——将本地知识图谱与 Hermes 记忆深度整合。体现了社区对 Agent 长期架构的第二阶段期望。

**🟢 持续打磨：模型生态**
- **PR #35659 [OPEN]**: 新增 `deepseek-v4-flash`、按厂商分组列表、清理冗余。维护者高频跟进模型更新，用户体验直接受益。([链接](https://github.com/NousResearch/hermes-agent/pull/35659))
- **#35587**: 官方 Claude 技能导入路径。社区有 1000+ 个 Claude 技能，打通迁移通道可大幅丰富 Hermes 的 skill 生态。

---

### 7. 用户反馈摘要

| 痛点场景 | 原始用户声音提炼 | 关联 Issue |
|---|---|---|
| **版本升级信任危机** | "v0.14 本可用，v0.15 的 `/model` 直接没法用了，这种核心交互不能回归测试吗？" | [#35595](https://github.com/NousResearch/hermes-agent/issues/35595) |
| **Windows 二等公民感** | "每次用浏览器工具带个 `&` 参数就爆炸，Windows 用户就这么不受待见吗？" | [#35654](https://github.com/NousResearch/hermes-agent/issues/35654) |
| **企业协作的“全有或全无”困境** | "我只想给飞书群里的同事开文档 QA 权限，但系统说要么是 Owner 要么啥也没有——这让我没法部署。" | [#35479](https://github.com/NousResearch/hermes-agent/issues/35479) |
| **MCP 又爱又怕** | "MCP 很酷，但工具注册完不用问就能让 LLM 调，加上一旦断线就永久失联——用起来提心吊胆。" | [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) / [#35661](https://github.com/NousResearch/hermes-agent/pull/35661) |
| **文档/代码不一致** | "官方 SKILL.md 让我跑 `--services` 参数，但 `setup.py` 根本没有这个 flag，按文档做就是做不通。" | [#35560](https://github.com/NousResearch/hermes-agent/issues/35560) |
| **飞书用户特定痛点** | "Gateway 重启后旧会话 thread_id 失效，消息发不出去，恢复能力太脆弱了。" | [#35576](https://github.com/NousResearch/hermes-agent/issues/35576) |

---

### 8. 待处理积压 (提醒维护者关注)

以下为长时间未响应或关键路径上阻塞、但当前讨论热度不足的重要 Issue/PR：

**Issues**

| ID | 标题 | 创建日期 | 重要性评估 | 推荐操作 | 链接 |
|---|---|---|---|---|---|
| #5129 | 背景记忆审查重复创建 Provider 实例 | 2026-04-04 | **P2** — 影响长期运行的内存与数据库连接稳定性 | 评估是否对生产环境构成风险，分配维护者 | [链接](https://github.com/NousResearch/hermes-agent/issues/5129) |
| #6345 | Slack Gateway 应暴露 `conversations.history` 工具 | 2026-04-09 | **P3** — 对 Slack 用户是“有/无”的质变体验 | 标记 `help wanted`，已有明确的 PR 设计思路 | [链接](https://github.com/NousResearch/hermes-agent/issues/6345) |
| #28291 | Moonshot Schema 联合类型崩溃 | 2026-05-19 | **P2** — 接入非标准 API 时的硬障碍 | 已有根因分析，仅需添加 `isinstance` 检查，易修复 | [链接](https://github.com/NousResearch/hermes-agent/issues/28291) |

**PRs**

| ID | 标题 | 创建日期 | 重要性评估 | 推荐操作 | 链接 |
|---|---|---|---|---|---|
| #23100 | 修复记忆文件写入覆盖原有权限 (0660→0600) | 2026-05-10 | **P2** — NixOS / 共享部署阻塞 | 代码影响面极小，建议快速审查合入 | [链接](https://github.com/NousResearch/hermes-agent/pull/23100) |
| #17480 | 修复 Codex 用量查询从 Credential Pool 读取凭据 | 2026-04-29 | **P2** — 阻塞 OAuth 用户的 `/usage` 命令 | 检查合并冲突，推动进入下个发布窗口 | [链接](https://github.com/NousResearch/hermes-agent/pull/17480) |
| #21774 | Google Workspace OAuth 命令标志修复 + 格式化输出 | 2026-05-08 | **P3** — 解决文档与实际代码不一致 | 关联 #35560，审查 scope 元数据持久化逻辑 | [链接](https://github.com/NousResearch/hermes-agent/pull/21774) |

---

**报告总结:** Hermes Agent 正处于从“个人 AI 工具”向“安全的生产级 Agent 框架”转型的关键期。权限系统的精细化、版本质量的门控和 MCP 生态的健壮性是社区关注的三大主航道。今日 P1 回归 Bug 的快速识别与修复体现了维护者的响应意愿，但 P0 安全风险 (#35584) 的暴露和多个 P2 长期积压仍需投入更系统的管理。桌面端与 i18n PR 的活跃标志着下一个大版本已在路上，项目整体健康度良好，处于高速迭代的活跃区间。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据你提供的 GitHub 数据生成的 PicoClaw 项目动态日报。

**日期：** 2026-05-31

---

# PicoClaw 项目动态日报

## 1. 今日速览

过去24小时内，PicoClaw 项目保持了极高的活跃度。发布了最新的 `nightly` 版本，同时合并了3个Pull Request（PR），并关闭了4个Issue。社区贡献主要集中在功能增强（如图片上传、国际化）和基础设施支持（如 Azure 身份验证）上。值得关注的是，`v0.2.9` 版本出现了一个影响Web UI的回归性Bug，需要维护团队优先处理。整体来看，项目正处于快速迭代期，社区活跃，但稳定性测试需同步加强。

## 2. 版本发布

- **`nightly` 构建版本 (v0.2.9-nightly.20260531.1ce353ba)**
  - **更新内容**：此版本为自动化构建的 `nightly` 版本，包含了截至最新的代码变更。
  - **破坏性变更**：无明确说明，但作为 `nightly` 构建，稳定性无法保证。
  - **迁移注意事项**：
    - **稳定性警告**：此版本可能不稳定，不建议在生产环境使用。
    - 升级前请务必做好数据备份，并建议在测试环境中先行验证。
    - 请特别关注来自 `v0.2.9` 正式版的已知问题（如 Issue #2972 和 #2968），确认 `nightly` 是否已包含修复。
    - **完整变更日志**：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展

今日合并/关闭了多项重要成果，标志着项目在多方面取得进展：

- **功能完善**：
  - **Web UI 增强**: PR [#2969](https://github.com/sipeed/picoclaw/pull/2969) 已合并，为聊天界面增加了图片粘贴和拖拽上传功能，显著提升了Web端用户体验。
  - **国际化 (i18n)**: 为支持孟加拉语 (Bangla)，相关功能请求 Issue [#2973](https://github.com/sipeed/picoclaw/issues/2973) 和 PR [#2974](https://github.com/sipeed/picoclaw/pull/2974) 均已关闭/合并，扩展了项目的多语言覆盖范围。
- **基础设施支持**：
  - **云服务对接**: PR [#2971](https://github.com/sipeed/picoclaw/pull/2971) 合并，为 Azure OpenAI 服务商增加了可选的 Azure Identity 认证支持，满足企业级安全策略需求。对应的 Feature Request Issue [#2970](https://github.com/sipeed/picoclaw/issues/2970) 也已关闭。

这些进展表明，项目团队正同时在用户体验、国际化和企业级集成能力上稳步推进。

## 4. 社区热点

今日社区讨论热烈，主要有以下几个焦点：

- **功能讨论与Bug反馈(中文)**: Issue [#2952](https://github.com/sipeed/picoclaw/issues/2952) 是目前评论数最多的活跃Issue（3条评论），由中文用户提出。核心诉求包括：
    - `exec`命令中的`actions:run`存在问题，多数AI模型首次调用时会遗漏该参数，导致报错并执行多余命令。
    - QQ 渠道在重启后存在Bug，发送信息会再次触发重启，只有清除历史上下文才能解决。
    - UI/UX改进建议：模型界面应默认显示已保存的key对应的提供商，并希望实现提供商下拉选择、key复用及一键测试获取模型列表等功能。
    - **分析**：此Issue突显了在非英文渠道（QQ）的稳定性问题，以及AI Agent与工具交互过程中的可靠性挑战。同时，用户对配置界面的智能化（如自动填充、一键添加）有较高期待。
- **PR 的设计讨论**: PR [#2977](https://github.com/sipeed/picoclaw/pull/2977)（为cron工具添加`get`和`update`操作）虽然评论数未明确，但其设计目标是让Agent能更精细地管理定时任务，避免因“删除-重建”流程导致的调度中断，这是一个非常实用的功能改进，引发了社区对Agent能力边界的积极讨论。

## 5. Bug 与稳定性

今日报告了几个值得关注的Bug，按严重程度排列如下：

- **严重（回归Bug）**:
    - **Issue [#2972](https://github.com/sipeed/picoclaw/issues/2972): [BUG] 升级到 v0.2.9 后，Web UI 消息错乱**。
        - **描述**：每次新会话都会自动附带旧的对话历史。这属于严重影响用户体验的回归问题。
        - **状态**：OPEN，未有修复PR关联。
- **中等**:
    - **Issue [#2968](https://github.com/sipeed/picoclaw/issues/2968): [BUG] `/context`命令始终显示“Compress at: 76800 tokens”**。
        - **描述**：上下文压缩显示固定值，无法反映真实状态，影响用户对Token消耗的判断。
        - **状态**：OPEN，获得1个👍，表明有用户遇到相同问题。
- **待验证（已关闭）**:
    - **Issue [#2742](https://github.com/sipeed/picoclaw/issues/2742): [Bug] v0.2.8 中Gateway启动没有频道**。该Bug已被标记为stale并关闭，但修复的有效性需在后续版本中验证。

## 6. 功能请求与路线图信号

- **很可能纳入下个版本**:
    - **Agent工具增强**：PR [#2977](https://github.com/sipeed/picoclaw/pull/2977) 对cron工具的增强设计精良，解决了Agent流程的痛点，预计会被合入。
    - **UI/UX改进**：Issue [#2952](https://github.com/sipeed/picoclaw/issues/2952) 中提到的UI改进建议，如“提供商下拉选择和Key复用”，与项目提升易用性的方向一致，很有可能在未来版本中实现。
    - **Azure Identity 支持**: 已合并的PR [#2971](https://github.com/sipeed/picoclaw/pull/2971) 将为使用Azure的企业用户提供关键支持。
    - **孟加拉语支持**: 国际化的 PR [#2974](https://github.com/sipeed/picoclaw/pull/2974) 已合并，将随下一个正式版本发布。
- **长期潜力**:
    - **富媒体消息**: PR [#2856](https://github.com/sipeed/picoclaw/pull/2856) (已stale) 提出的为消息工具支持媒体附件功能，若被合并将极大提升Agent的表达和交付能力，是Agent能力演进的重要一步。
    - **工具策略控制**: PR [#2838](https://github.com/sipeed/picoclaw/pull/2838) (已stale) 提出的`agent.md`前端工具策略过滤器，为Agent的安全和权限控制提供了更细粒度的方案，是走向企业级应用的重要基础设施。

## 7. 用户反馈摘要

从今日的Issue和PR中，可以提炼出以下真实用户反馈：

- **痛点**:
    - **稳定性与可靠性**: 用户 `xpader` 在升级后遭遇Web UI混乱（#2972），用户体验急降。用户 `xhynice` 对QQ渠道的稳定性表示不满，重启后存在循环重启Bug（#2952）。
    - **工具执行力**: `exec` 命令在与AI模型交互时存在参数遗漏问题（#2952），导致Agent行为不符合预期，影响自动化任务的可靠性。
    - **信息透明度**: 用户 `xpader` 指出 `/context` 命令显示的Token压缩信息不准（#2968），对开发者和高级用户是个困扰。
- **使用场景与满意/不满意**:
    - **满意**: 开发者和贡献者乐于见到项目功能的增强，如图片上传（#2969）、更灵活的cron工具（#2977）以及企业级认证支持（#2970）。
    - **不满意/建议**: 用户 `xhynice` 提出了非常具体的UI/UX改进建议，反映了用户对界面智能化和配置简化的迫切需求。中文用户群体希望项目能更好地支持其生态（如QQ）。

## 8. 待处理积压

以下为一些持续时间较长但尚未解决或未获得足够关注的重要Issue/PR，提醒维护者关注：

- **关键的待合并PR**:
    - **[stale] PR [#2856](https://github.com/sipeed/picoclaw/pull/2856): `feat(message): support media attachments...`** (自2026-05-11起无实质更新)。这是一个功能增强PR，若合并将显著提升 `message` 工具的能力。建议维护者评估其当前状态，决定是继续推进、关闭还是合并。
    - **[stale] PR [#2838](https://github.com/sipeed/picoclaw/pull/2838): `feat(agent): support frontmatter tool policy filters`** (自2026-05-09起无实质更新)。此PR能带来强大的安全控制能力，对项目成熟度至关重要，同样需要维护者跟进。
- **重要的开放Bug**:
    - **[OPEN] Issue [#2972](https://github.com/sipeed/picoclaw/issues/2972): Web UI消息错乱**。这是一个影响范围广的回归Bug，应作为最高优先级处理。
    - **[OPEN] Issue [#2952](https://github.com/sipeed/picoclaw/issues/2952): 多个功能与Bug反馈（中文用户）**。虽然内容混合，但其中QQ渠道的问题和exec工具的问题是亟待处理的稳定性Bug。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报（2026-05-31）

## 1. 今日速览

截至 2026-05-31，NanoClaw 项目保持 **高活跃度**。24 小时内共有 **16 个 PR** 和 **3 个 Issue** 更新，社区贡献者持续输出高质量代码。今日暂无新版本发布，但有 **4 个 PR 被合入**，涵盖多实例部署支持、群聊上下文窗口和核心性能优化等关键领域。安全与稳定性方面的讨论热度依旧居高不下——供应链安全风险的 Issue（#2641）和 Apple Container 兼容性修复（#2649/#2650）成为今日最受关注的议题。项目总体上正在 v2 阶段快速推进基础设施成熟度，同时社区对 **多用户/多实例家庭场景** 的需求信号不断增强。

**活跃度评估：🟢 高度活跃**

---

## 2. 版本发布

（本日无新版本发布）

---

## 3. 项目进展（已合入/已关闭 PR）

### 今日合入的 4 个 PR

- **多实例网关代理修复** [#2652](nanocoai/nanoclaw/pull/2652)  
  作者 `matty271828` 修复了 OneCLI `/api/container-config` 中 `HTTPS_PROXY`/`HTTP_PROXY` 硬编码 `host.docker.internal:10255` 的问题，使其兼容 `instances.conf` 定义的自定义端口偏移。**意义**：为多实例生产部署扫清了关键网络障碍。

- **群聊上下文窗口** [#2645](nanocoai/nanoclaw/pull/2645)  
  作者 `yairixStudio` 新增了可选的 per-agent-group 上下文消息窗口。当 Agent 在群聊中被 `@mention` 触发时，现在可以接收最后 N 条未读消息作为 `[Context — last N messages]` 前缀。**意义**：极大提升了多 Agent 群聊场景的对话连续性与感知能力。

- **消息可观测性增强** [#2521](nanocoai/nanoclaw/pull/2521)  
  作者 `crookies` 在 XML 消息属性中增加了 `from-channel` 和 `from-type` 字段（已在 `findByRouting()` 中解析但未对外暴露）。**意义**：支持外部监控仪表盘解析多通道转录文件，增强了生态可扩展性。

- **核心性能优化** [#6](nanocoai/nanoclaw/pull/6)  
  作者 `gavrielc` 将 IPC 层的忙循环轮询（`setTimeout`）替换为异步 `fs.watch` 事件驱动模式，并用 `fs.promises` 替代同步文件操作。**意义**：减少 CPU 空转与事件循环阻塞，对小内存/低功耗部署场景（如 Mac Mini、树莓派）尤其友好。

### 项目整体进展判断

以上合入内容标志着 NanoClaw 在 **v2 多实例部署、群聊体验、运维可观测性、性能优化** 上均取得了实质性推进。结合社区贡献的活跃度，项目正处于 v2 功能的密集落地期。

---

## 4. 社区热点

### 🔥 供应链安全争议 #2641
[Issue #2641](nanocoai/nanoclaw/issues/2641)  
用户 `NoamGit` 引用外部分析文章，严厉批评 `@gongrzhe/server-gmail-autoauth-mcp` 的自动安装行为——“AI 未经明确授权就在机器上安装陌生人代码并索要 Gmail 密码”。该 Issue 提出了一个 **深刻的架构层面追问**：MCP 生态是否需要更严谨的沙箱机制和权限提示？社区评论区有望进一步发酵。

### 💬 Discord v2 URL 回归问题 #2044
[Issue #2044](nanocoai/nanoclaw/issues/2044)（👍 2）  
用户 `pwinnski` 指出 v2 中对 `<URL>` 的处理破坏了 Discord 的原生 URL 预览抑制功能，请求配置化回退。**背后诉求**：用户害怕“升级带来的不可控特性改动”，希望核心通道适配器的行为保持稳定可预测。

### 🏠 多用户/家庭共享场景需求 #2653
[Issue #2653](nanocoai/nanoclaw/issues/2653)  
用户 `elancode` 精准描述了家庭共享 Mac 上运行多个 Telegram Bot 的用例，指出数据模型虽支持多角色，但 `src` 目录的配置冲突是实际障碍。**社区信号**：NanoClaw 正被小团队和家庭用户用于个人 AI 助理部署，该需求说明项目的易用性天花板正在被触碰。

### 🛡️ 跨频道问答安全加固 #2651
[PR #2651](nanocoai/nanoclaw/pull/2651)  
`Hinotoi-agent` 提交了安全检查修复——确保 `ask_user_question` 的待处理提问只能被原始频道/线程回答。这是安全边界上的必要加固。

---

## 5. Bug 与稳定性

| 严重程度 | 标题 | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 **严重** | 供应链安全风险 #2641 | MCP Server 自动安装机制可导致未授权密码索取，属安全范式问题 | 仅 Issue 讨论，无修复 PR |
| 🔴 **严重** | Apple Container MCP 静默失效 #2649 | 嵌套文件挂载在 Apple Container 下产生幻影 inode，`stat()` 返回 0644 但 `read()` 失败，所有 MCP 服务器静默禁用 | 修复 PR [#2649](nanocoai/nanoclaw/pull/2649) & [#2650](nanocoai/nanoclaw/pull/2650) 已提交待审 |
| 🟡 **高** | Discord URL 抑制回归 #2044 | v2 修改了 `<URL>` 处理方式，导致用户无法像 v1 一样抑制 Discord 预览 | 长期开放，无对应修复 PR |
| 🟡 **中** | 跨频道问答安全漏洞 #2651 | 存在潜在缺陷允许不同渠道回复本频道待处理问题 | 修复 PR [#2651](nanocoai/nanoclaw/pull/2651) 待合并 |
| 🟢 **低** | OneCLI 代理端口硬编码 #2652 | 已在今日合入修复 | ✅ 已关闭 |

### 重点关注

**Apple Container 兼容性** 是今日最值得关注的技术债。`jurre-mbt-it` 贡献的 #2649 和 #2650 发现问题根因在于嵌套文件挂载的 overlay 竞态条件（Apple Silicon 下 virtio-fs 特有），这意味着目前所有在 Mac 上通过容器运行用户流程的 NanoClaw 用户都可能遇到 MCP 全部失效的问题，建议项目维护者优先审查这两条 PR。

---

## 6. 功能请求与路线图信号

### 潜在纳入 v2 下一阶段的功能

| 功能 | 来源 | 状态 | 路线图判断 |
|---|---|---|---|
| **多用户/单实例隔离** [#2653](nanocoai/nanoclaw/issues/2653) | 社区需求 | 刚提交 | 🟢 高优先级，数据模型已支持，仅配置冲突 |
| **WebUI 控制面板** [#212](nanocoai/nanoclaw/pull/212) | 历史 PR | 阻塞/待关闭 | 🟡 虽标签差，但 11 个标签页的完整 UI 工程价值极大 |
| **本地语音转录** [#2317](nanocoai/nanoclaw/pull/2317) | `ira-at-work` | 开放中 | 🟢 符合 AI 助手多模态方向 |
| **GitHub 轮询模式** [#2301](nanocoai/nanoclaw/pull/2301) | `ira-at-work` | 开放中 | 🟢 解决 NAT/防火墙用户痛点 |
| **每日备份与恢复** [#2084](nanocoai/nanoclaw/pull/2084) | `ddaniels` | 开放中 | 🟢 生产环境刚需，可提升稳定性信心 |
| **Hugging Face 追踪上传** [#2648](nanocoai/nanoclaw/pull/2648) | `gavrielc` | 开放中 | 🟢 符合实验可复现性趋势 |
| **AWS 凭证代理** [#2634](nanocoai/nanoclaw/pull/2634) | `ira-at-work` | 开放中 | 🟡 特定用户群高价值 |

### 路线图分析

**多用户隔离** 和 **语音交互** 是两个明显的关键信号。社区正在将 NanoClaw 从“开发者玩具”推向“家庭/轻量级生产应用”。如果项目团队能在下一个 minor 版本中解决 multi-instance 的配置冲突（#2653），并合入 Whisper 转录技能（#2317），将极大拓宽受众面。

---

## 7. 用户反馈摘要

> **用户 `pwinnski`**（#2044）  
> *“V2 现在将 `<URL>` 转换为 `[URL](URL)`，这与任何可能的预期效果正好相反。”*  
> **分析**：反映了用户对核心通道行为稳定性的高要求。升级带来的破坏性改动需要清晰的配置出口。

> **用户 `NoamGit`**（#2641）  
> *“我建议阅读这篇文章……我的 AI 在我的机器上安装了陌生人的代码，并索要了我的 Gmail 密码。”*  
> **分析**：用户对 MCP 市场的信任度正在被质疑。社区期待明确的沙箱策略或“确认即安装”流程。

> **用户 `elancode`**（#2653）  
> *“数据模型已经支持了用户/角色/agent_group。阻塞点在 `src` 目录。”*  
> **分析**：用户已经深入代码进行了可行性分析，说明需求非常迫切，且项目代码结构清晰度得到了认可（易于自审）。

> **用户 `crookies`**（#2521，已合入）  
> *“我运行着 Telegram + Discord 的多通道设置，为了在面板上显示通道图标，这些数据在内部已经解析了，但没有对外暴露。”*  
> **分析**：展示了社区自我赋能的模式——只要内部数据结构完整，社区能快速补齐外部生态工具。

---

## 8. 待处理积压

### 🔴 需项目维护者重点关注

- **PR #212** —— WebUI 控制面板（`harperaa`）  
  自 2026-02-13 起敞开至今，已超 3 个月。尽管被标记为 `Blocked` / `Pending Closure`，但该 PR 提供了完整的 11 标签页前端工程。项目组应明确传达该方向的最终决策（重启还是废弃），避免社区贡献者观望。

- **PR #2084** —— 每日备份与恢复（`ddaniels`）  
  33 天未合入。灾难恢复属于生产级基础设施，延迟合入可能影响中重度用户的稳定性判断。建议本轮优先处理。

### 🟡 审查瓶颈提示

- **`ira-at-work` 系列 PR**（#2301 GitHub 轮询 / #2317 语音转录 / #2634 AWS 凭证代理）  
  贡献者近期极活跃（均在 5/30-31 有更新），且属于 moat 级特性（防火墙穿透、多模态、云原生）。目前 25-24 天等待审查，如能分批合入，对社区士气将有明显提振。

- **PR #2649 / #2650** —— Apple Container 修复  
  问题影响面广（所有 Mac 容器用户都可能遇到 MCP 失效），且贡献者已提供了详尽分析和修复方案。建议优先合并以消除这一严重的功能盲区。

### 🟢 长期开放 Issue

- **Issue #2044** —— Discord URL 回归  
  已存在 34 天。虽未阻塞核心功能，但作为高可见性通道（Discord）的基础行为退步，建议在下一个补丁中给出合入或配置化方案，避免用户流失。

---

*本报告基于 github.com/nanocoai/nanoclaw 的 2026-05-31 公开时间序列数据生成。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026‑05‑31

## 1. 今日速览

IronClaw 在 24 小时内保持极高开发强度：处理 **4 个 Issue**（新开/活跃 3，关闭 1）和 **18 个 Pull Request**（7 个待合并，11 个已合并/关闭）。核心团队围绕 Reborn 架构的触发、出站交付和产品认证交付了大量代码，同时新贡献者 neoguyverx 合入了 4 个代理改进补丁。版本发布继续保持静默，但 crate.io 发布滞后问题（#3259）及 Nightly E2E 失败（#4108）仍是需关注的风险点。总体项目活跃度极高，社区贡献活跃，发布流程和 CI 稳定性有待改善。

---

## 2. 版本发布

（无新版本发布，本节略）

---

## 3. 项目进展

今日共有 **11 个 PR 合并/关闭**，覆盖 Reborn 架构核心组件、关键 Bug 修复、代理行为增强以及安全防护。

### Reborn 架构持续推进
- **#4254 – 可信入站门面**  
  为触发器入口添加了密封请求形状、重放优先幂等性、可信绑定解析与接收/提交流程，是触发器循环的关键基础设施。  
  [PR #4254](https://github.com/nearai/ironclaw/pull/4254)
- **#4255 – 出站交付解析域类型**  
  在 `ironclaw_outbound` 中定义了 `CommunicationDeliveryResolutionRequest`、`CommunicationDeliveryIntent` 等合约，为触发器的出站分发提供类型基础。  
  [PR #4255](https://github.com/nearai/ironclaw/pull/4255)
- **#4245 – 产品级认证 HTTP 表面**  
  挂载了手动令牌、账户恢复、刷新、清理等剩余认证路由，完成 WebUI/CLI/API 的完整认证生命周期。关闭 #4201。  
  [PR #4245](https://github.com/nearai/ironclaw/pull/4245)
- **#4246 – NEAR AI MCP 凭据迁移至产品认证**  
  将 `nearai-mcp` 内置清单从静态 `SecretHandle` 切换为运行时 `ProductAuthAccount` 凭据源，统一凭证管理。  
  [PR #4246](https://github.com/nearai/ironclaw/pull/4246)

### 运行时与代理 Bug 修复
- **#4259 – 修复 synthetic capability 自省**  
  曾导致模型在调用 `capability_info { name: "capability_info" }` 时触发 `InvalidInvocation` 并异常终止运行。合入此修复后，模型可以正确内省合成工具。**含数据库迁移。**  
  [PR #4259](https://github.com/nearai/ironclaw/pull/4259)
- **#4258 – 路由 dispatch 失败处理与 oneOf/anyOf 容器规整**  
  修复两处 Bug：dispatch 失败未走正确的 disposition 路径（#4236 的方案），以及 LLM 传入字符串化 JSON 数组导致 `builtin.http` 解析崩溃。  
  [PR #4258](https://github.com/nearai/ironclaw/pull/4258)
- **#4206 – HTTP 出口全异步化（Issue 关闭）**  
  “Make runtime HTTP egress async end to end” 标记关闭，说明该改进已在近期 PR 中落地。  
  [Issue #4206](https://github.com/nearai/ironclaw/issues/4206)

### 代理行为改进（社区贡献者 neoguyverx）
- **#4250 – 可中断在途 LLM 调用**  
  用户发送 `/interrupt` 后可立即断开 `reqwest` HTTP 流，无需等待当前请求自然结束。  
  [PR #4250](https://github.com/nearai/ironclaw/pull/4250)
- **#4251 – 结构化压缩摘要 + 关键上下文内存刷出**  
  压缩摘要改用 7 节模板（目标/约束/进度/决策/文件/下一步/关键上下文），并主动将关键上下文写入内存，防止上下文窗口压缩时丢失重要信息。  
  [PR #4251](https://github.com/nearai/ironclaw/pull/4251)
- **#4252 – 空闲迭代后记忆写入行为提示**  
  连续 N 轮未调用 `memory_write` 时注入系统提示，引导代理主动保存上下文。  
  [PR #4252](https://github.com/nearai/ironclaw/pull/4252)
- **#4253 – 身份文件读取时注入检测**  
  对 `AGENTS.md`、`SOUL.md` 等文件进行读取时扫描，识别已知的提示注入模式，提升安全性。  
  [PR #4253](https://github.com/nearai/ironclaw/pull/4253)

### 设计文档
- **#4247 – WebUI v2 认证 E2E 设计**  
  为 #4112（GSuite/Notion/GitHub 认证 E2E）提供架构设计文档，代码尚未实现。  
  [PR #4247](https://github.com/nearai/ironclaw/pull/4247)

---

## 4. 社区热点

- **#3259 – 请求发布 0.25.0~0.27.0 到 crates.io**  
  12 条评论，持续近一个月。用户指出 GitHub 已打标签至 0.27.0，但 crates.io 仅发布到 0.24.0，导致下游固定于旧版并受 wasmtime 28.x CVE 影响。社区对发布延迟关注度高，希望项目团队尽快发布包含安全修复的新版本。  
  [Issue #3259](https://github.com/nearai/ironclaw/issues/3259)
- **#228 – 子任务创建默认拒绝策略**  
  虽然只有 1 条评论，但 Issue 在 2026‑05‑31 获得更新，表明该长期（二月提出）的安全增强提案重新被激活。作为潜在的安全基线功能，社区讨论值得关注。  
  [Issue #228](https://github.com/nearai/ironclaw/issues/228)
- **#4035 – Slack Reborn 适配器（持续开放）**  
  该大型 PR 经过一周开发，仍处于审查阶段，作为第三方平台集成的首块拼图，期待更多社区贡献者参与讨论。  
  [PR #4035](https://github.com/nearai/ironclaw/pull/4035)

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 说明 |
|----------|----------|------|
| **高** | **#4108 – Nightly E2E 持续失败** | 自动化报告 v2‑engine 测试失败，最新更新于 2026‑05‑30，尚未有关联修复 PR。需优先定位是否为主干回归。 [Issue #4108](https://github.com/nearai/ironclaw/issues/4108) |
| **中** | **#3259 – 发布缺失** | 虽非代码 Bug，但下游因无法获取 0.25+ 而受 wasmtime CVE 影响，属于交付流程的稳定性风险。 |
| **中** | **#228 – 子任务创建无限制** | 当前 `CreateJobTool` 缺少默认拒绝策略，LLM 幻觉或注入可滥用生成并行任务，存在安全风险。 |
| **已修复** | #4259、#4258 | 今日合并的修复解决了 capability_info 自省崩溃和 dispatch 失败路径问题。 |
| **已关闭** | #4206 | HTTP 出口改为全异步，改善运行时稳定性。 |

---

## 6. 功能请求与路线图信号

从今日活跃的 Issue / PR 可清晰看到项目的近期发力方向：

- **触发（Trigger）引擎**：`ironclaw_triggers` crate 骨架 [#4261](https://github.com/nearai/ironclaw/pull/4261)、出站通信偏好存储 [#4260](https://github.com/nearai/ironclaw/pull/4260) – 预计下一版本将引入完整的触发器域模型与调度。
- **产品级认证**：多 PR 并行推进（#4245、#4246、#4257、#4229、#4256），覆盖 OAuth、GitHub SSO、手动令牌，认证体系日趋完整。
- **第三方集成**：Slack 适配器 [#4035](https://github.com/nearai/ironclaw/pull/4035) 仍在开发，有望随 Reborn 发布一同推出。
- **代理能力增强**：推理摘要保留 [#4230](https://github.com/nearai/ironclaw/pull/4230)（Codex reasoning）、可中断调用、记忆提示等已合入或待合并。
- **安全基线**：#228 的默认拒绝策略、#4253 的提示注入检测，表明团队正在系统性地加强代理安全。

这些功能的组合指向 **IronClaw 0.28+** 将是一次包含触发引擎、产品认证、第三方集成和安全强化的重大更新。

---

## 7. 用户反馈摘要

- **#3259 – 发布期待与安全焦虑**  
  用户 @dacoldest 明确指出“crates.io 只到 0.24.0”，而 GitHub 已有 0.27.0 tag，下游因依赖锁定被迫停留在旧版，且受到 `wasmtime 28.x` 安全漏洞影响。12 条评论表明社区对延迟发布的不满和对安全修复的急切需求。  
  [Issue #3259](https://github.com/nearai/ironclaw/issues/3259)
- **#228 – 安全策略需求**  
  虽然评论数不多，但 Issue 提出若 LLM 被注入或幻觉，可调用 `CreateJobTool` 无限制创建子任务。创建者希望引入“默认拒绝”策略，这反映出用户对代理在生产环境中安全性越加重视。  
  [Issue #228](https://github.com/nearai/ironclaw/issues/228)

---

## 8. 待处理积压

| 项目 | 创建/更新 | 状态 | 提醒 |
|------|-----------|------|------|
| **#228：子任务创建默认拒绝策略** | 2026-02-19 / 2026-05-31 更新 | 长期增强，1 评论 | 虽近期更新，仍缺乏明确决策或指派，需维护者给出路线图安排。 [Issue #228](https://github.com/nearai/ironclaw/issues/228) |
| **#3259：crates.io 发布阻塞** | 2026-05-05 / 持续活跃 | 12 评论，未关闭 | 社区高度关注，严重影响下游用户安全与体验，应尽快推动发布或发布回应。 [Issue #3259](https://github.com/nearai/ironclaw/issues/3259) |
| **#4108：Nightly E2E 失败** | 2026-05-27 / 2026-05-30 更新 | 未关联修复 PR | 持续失败可能导致问题堆积，建议定位关联 commit 并回滚或快速修复。 [Issue #4108](https://github.com/nearai/ironclaw/issues/4108) |
| **#4035：Slack Reborn 适配器** | 2026-05-25 / 2026-05-30 更新 | 大型 PR，待审查 | 已开放近一周，涉及架构边界，需 reviewer 持续跟进避免阻塞。 [PR #4035](https://github.com/nearai/ironclaw/pull/4035) |
| **#4229、#4230、#4257** | 2026-05-29~30 | 较新但等待合并 | 多为核心贡献者 PR，应在下次合并窗口优先处理，避免积压。 |

---

*本期日报基于 2026-05-31 项目数据生成，旨在客观反映项目健康状况，为维护者和社区提供参考。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 | 2026-05-31

---

## 1. 今日速览

- 过去24小时项目**整体活跃度较低**，无新 Issue 提出、无版本发布、无 Pull Request 被合并或关闭。
- 两个此前提交的修复型 PR（#1466、#1467）在今日得到了更新，目前仍处于**待合并**状态，标志着社区贡献的推进，但官方入库环节尚未完成。
- 项目目前处于**存量修复沉淀期**，代码仓库无实质性增量；但已积压近两个月的修复方案如持续得不到处理，将面临社区贡献积极性下降的风险。维护者对停滞 PR 的响应是当前项目健康度的主要观测指标。

---

## 2. 版本发布

**无**

*过去 24 小时无新版本发布。*

---

## 3. 项目进展

**合入 / 关闭：** 无  
**代码变更：** 主分支无新增合并

### 关键待合入 PR 分析

尽管今日无实际入库，以下两个 PR 在昨日（2026-05-30）均被贡献者 `linlihua` 更新，代表项目在可用性与平台适配层面有明确推进，仅待维护者完成 Code Review 与合入：

| PR | 标题 | 影响模块 | 推进价值 |
|---|---|---|---|
| #1466 | fix(mcp): modal close button unreachable when content grows tall | MCP Server 配置弹窗 | 修复表单复杂时底部按钮不可点击的交互阻塞 Bug，提升 MCP Agent 配置的生产力 |
| #1467 | fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS | 设置 > 快捷键面板 | 修复 macOS 硬编码 'Ctrl' 的平台适配缺陷，提升跨平台使用体验 |

→ **[PR #1466](netease-youdao/LobsterAI PR #1466) | [PR #1467](netease-youdao/LobsterAI PR #1467)**

---

## 4. 社区热点

**今日无新评论、新议题产生，社区讨论热度偏低。**

但值得关注的是，贡献者 `linlihua` 长期跟进的两个 PR 在昨日同一时间（2026-05-30）均被做了推送更新（可能为同步基线或修复冲突），这种持续性维护行为表明：

- **MCP 配置体验优化**是当前社区关心的重点功能入口，用户在使用中真实遇到了模态框交互卡点；
- **macOS 原生体验**是进阶用户的高频痛点，快捷键显示错误属于显性“减分项”，社区开发者愿意为此投入修复精力；
- 两位 PR 创建于 **2026-04-04**，至今已开放 **57 天**，贡献者仍在积极更新，反映出对 LobsterAI 项目的高度责任感与耐心。

**背后诉求核心**：社区希望维护方加快对长期停滞 PR 的响应速度，保障贡献闭环，避免贡献价值在积压中流失。

---

## 5. Bug 与稳定性

**今日新增 Bug：** **无**

### 待解决 Bug（已有 Fix PR，待合并）

| 严重程度 | 描述 | 对应修复 PR |
|---|---|---|
| **P2（功能性阻塞）** | MCP Server 表单（环境变量、Header 等）内容过多时，Modal 整体滚动导致底部的 Cancel 等操作按钮超出视口，无法点击 | #1466 |
| **P3（体验缺陷 / 视觉误导）** | macOS 系统下“设置 > 快捷键”面板仍显示 `Ctrl` 而非 `⌘`，硬编码导致与系统常规规范冲突 | #1467 |

目前项目稳定性方面未出现崩溃类（P0/P1）安全事件，但上述两个 Bug 的修复方案均已就绪，技术债务的存在周期是当前稳定性的主要关注点。

---

## 6. 功能请求与路线图信号

**今日无新 Feature Request 提出。**

从现有 PR 内容可提取以下路线图信号：

- **MCP Agent 深度配置化**：PR #1466 修复的表单支持 `env vars` 和 `headers` 的多项配置，暗示 LobsterAI 在 MCP 协议集成侧正走向更高定制性，未来可能开放更多 Agent 行为配置能力。
- **跨桌面端体验统一**：PR #1467 反映项目正在优化 macOS 基础交互元素，表明跨平台一致性是当前用户体验打磨的一个子方向。
- **整体判断**：项目当前处于**功能沉淀与体验修复**的阶段，无大规模新功能上线的迹象，以修补存量问题、巩固基础可用性为主。

---

## 7. 用户反馈摘要

**今日未产生新的 Issue 评论或用户反馈。**

可作为参考的“隐性”用户痛点来自待合并 PR 的摘要描述：

> “When form content grew tall (e.g. adding multiple env vars or headers), the Cancel button scrolled below the fold and the modal close button was unreachable.”
> —— 反映了用户在复杂配置场景下操作流程中断的真实烦恼。

> “displayed Ctrl+N / Ctrl+F / Ctrl+, — following Windows/Linux conventions instead of macOS.”
> —— 反映了 macOS 用户在初次接触快捷面板时的认知冲突与困惑。

**结论**：社区用户的注意力目前集中在 **MCP 配置实操便利性** 与 **macOS 平台原生体验**两个关键痛点上。

---

## 8. 待处理积压

以下两个 PR 均已开放超过 **57 天**，并被 GitHub 机器人打上 `[stale]` 标签，属于项目当前最值得维护者立即关注的积压项：

| 编号 | 标题 | 创建日期 | 最后更新 | 过期时长 | 影响用户面 | 建议操作 |
|---|---|---|---|---|---|---|
| #1466 | fix(mcp): modal close button unreachable when content grows tall | 2026-04-04 | 2026-05-30 | 57 天 | 所有 MCP Server 配置用户 | ✅ Code Review + Merge |
| #1467 | fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS | 2026-04-04 | 2026-05-30 | 57 天 | 所有 macOS 平台用户 | ✅ Code Review + Merge |

### ⚠️ 风险提示

- 贡献者 `linlihua` 在近两个月的开放期内持续维护这两个分支，若长期得不到合并，极易浇灭外部贡献者的热度。
- 两个 PR 分别涉及 MCP Agent 生产力入口的可用性修复与 macOS 平台的关键体验修复，是现有用户直接受益的补丁。
- **强烈建议项目维护者本周优先完成对 #1466 和 #1467 的 Review 与合入**，释放阻塞，维护社区活力。

---

*数据来源：netease-youdao/LobsterAI GitHub 仓库 | 报告生成时间：2026-05-31*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-05-31

---

## 1. 今日速览

- 过去 24 小时内无新 Issue 或版本发布，项目整体进入平稳迭代期。
- 一条新的 Pull Request #1088 已提交，专注修复 OpenAI Codex provider 在最终工具调用参数上的处理逻辑，目前处于待合并状态。
- 该 PR 虽未合并，但其涉及的核心功能改进（缺失参数增量时的 fallback 机制）对 AI provider 兼容性有实质提升。
- 社区互动较少（0 评论、0 反应），但贡献者仍保持活跃，项目维护节奏稳定，评价为 **中等偏静但有关键进展**。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

### ⏳ 待合并 PR

#### [#1088 – Handle OpenAI Codex final tool-call arguments](https://github.com/moltis-org/moltis/pull/1088)
- **作者**: s-salamatov  
- **创建/更新**: 2026-05-31  
- **状态**: OPEN  
- **摘要**:
  - 在 OpenAI Codex provider 中记录 `response.function_call_arguments.done` 负载。
  - 当没有参数增量（argument deltas）被发出时，从最终参数中合成一个流式参数增量。
  - 保持空的累积参数字符串通过解码诊断流动，以避免缺失参数时的错误报告空白。

**分析**  
该 PR 填补了 Codex provider 在流式场景下的一个关键缺失：当模型只输出一次完整参数（而非增量）时，原有逻辑无法正确处理，可能导致下游诊断丢失或参数错误。本次改进增强了 provider 的鲁棒性，对使用 Codex 模型的用户影响较大。**虽未合并，但代码质量成熟，预计短期内会进入主分支。**

---

## 4. 社区热点

今日唯一活跃条目为 [#1088](https://github.com/moltis-org/moltis/pull/1088)，但尚无评论或表情反应。由于缺乏 Issue 讨论和新问题，项目讨论热度较低。  
**潜在关注点**：PR 涉及 OpenAI Codex 底层参数处理，后续可能需要用户反馈来验证修复效果。

---

## 5. Bug 与稳定性

- **今日新报告 Bug**：0 条  
- **已存在但未修复的 Bug**：无新增记录  
- **稳定性评估**：项目当前未见明显回归或崩溃报告，状态稳定。

---

## 6. 功能请求与路线图信号

[#1088](https://github.com/moltis-org/moltis/pull/1088) 本质上是一项 **功能增强**，它解决的是流式场景下参数增量的缺失问题，而非全新功能。  
**路线图信号**：  
- 团队正在持续打磨 AI provider 的兼容层，尤其是对 OpenAI Codex 的流式输出处理。  
- 可推测下一版本将包含更完善的 provider 参数传输机制，可能涉及更多 provider 的类似适配。

---

## 7. 用户反馈摘要

今日无新 Issue 或 PR 评论，未能收集到用户直接反馈。  
项目暂时缺乏用户声音，可能需要通过发布新版本或引导社区测试来提高互动。

---

## 8. 待处理积压

| 条目 | 类型 | 创建时间 | 说明 |
|------|------|----------|------|
| [#1088](https://github.com/moltis-org/moltis/pull/1088) | PR (待合并) | 2026-05-31 | 核心参数处理改进，无 Comments，建议尽快安排 Review 并合并。 |

其余历史 Issue 与 PR 未见长期未响应情况，积压压力极小。

---

**报告结束** — 下次更新时间：2026-06-01  
*分析依据：Moltis GitHub 公共仓库 24 小时活动数据*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报（2026‑05‑31）

> **数据来源**：GitHub `agentscope-ai/QwenPaw`（项目原名 CoPaw）  
> **统计时段**：2026‑05‑30 ~ 2026‑05‑31（24 小时内）

---

## 1. 今日速览

- 过去 24 小时共有 9 条 Issue 更新（8 条开放、1 条关闭），1 条 PR 仍在开放等待合并，无新版本发布。
- 社区反馈活跃，Windows 下 `execute_shell_command` 触发 cmd 窗口闪烁的问题被多个用户重复报告（#4123、#4828、#4829），其中 #4828 已关闭，但 #4829 为新开类似问题，表明该 Bug 仍未彻底解决。
- `/mission` 命令导致控制台完全卡死（#4454）是一个严重功能不可用问题，影响使用体验。
- 功能请求集中在桌面端路径可点击、对话消息处理模式、Docker 镜像预置依赖包等方向，用户对体验和稳定性的诉求明显。
- 整体项目维护活跃度中等，Bug 修复响应较快，但高优先级问题（如 cmd 窗口闪烁、Mission 卡死）尚未有明确修复 PR 合并。

---

## 2. 版本发布

当日无新版本发布。

---

## 3. 项目进展

#### 3.1 已合并 / 关闭的 PR  
当日无 PR 被合并。

#### 3.2 重要进展中的 PR  
- **[#4689] feat(providers): route non-standard generate_kwargs into extra_body**  
  状态：**OPEN**（待合并）  
  此 PR 解决 OpenAI Python SDK 静默拒绝非标准参数（如 DashScope 的 `enable_search`）的问题，通过 `__init__` 注入 `extra_body`。若合入，将提升对各类推理平台的非标参数兼容性。  
  [→ PR #4689](https://github.com/agentscope-ai/QwenPaw/pull/4689)

#### 3.3 问题关闭情况  
- **#4828**（Bug：Windows 下 cmd 窗口闪烁）已由作者关闭，但相同问题 #4829 随后被新开，说明根本原因未被解决。  
  [→ Issue #4828](https://github.com/agentscope-ai/QwenPaw/issues/4828)

> **小结**：当日项目未完成实质性合并/关闭的重要 PR，核心 Bug 仍处于讨论阶段，进展偏慢。

---

## 4. 社区热点

以下 Issue 在当日评论最活跃，反映出用户关注的重点：

| Issue | 标题 | 评论数 | 核心诉求 |
|-------|------|--------|----------|
| [#4123](https://github.com/agentscope-ai/QwenPaw/issues/4123) | [Bug] Windows: execute_shell_command flashes a console window | 8 | 后台执行命令不应弹出 cmd 窗口，严重影响连续操作的体验 |
| [#4408](https://github.com/agentscope-ai/QwenPaw/issues/4408) | [Feature]: 建议工作目录默认文件统一放到一个文件夹 | 7 | 借鉴 OpenCode，使用 `.qwenpaw` 隐藏文件夹保持工作区整洁 |
| [#4454](https://github.com/agentscope-ai/QwenPaw/issues/4454) | [Bug]: /mission command causes Console to freeze completely | 4 | 执行 `/mission` 后界面完全卡死，清空目录无法恢复 |
| [#4826](https://github.com/agentscope-ai/QwenPaw/issues/4826) | [Feature]: 三种新消息处理方式 + 路径点击 | 2 | 类似 Hermes Agent 的打断/等待/插入模式，提升交互灵活性 |
| [#4824](https://github.com/agentscope-ai/QwenPaw/issues/4824) | [Bug]: ACP连接Claude Code协议对不上 | 2 | 协议版本号格式不匹配导致 `delegate_external_agent` 失败 |

**分析**：  
- **Windows 平台用户体验**是当前社区最大痛点，cmd 窗口闪烁和 Mission 卡死均直接影响日常使用。  
- **工作区整洁**与 **ACP 协议兼容性** 反映用户对集成外部工具（Claude Code）有较强需求，且对项目文件管理提出了更高标准。

---

## 5. Bug 与稳定性

按严重程度排列，标注是否已有修复 PR 关联。

| 严重级别 | Issue | 描述 | 状态 | 是否有 Fix PR |
|----------|-------|------|------|----------------|
| **严重** | [#4454](https://github.com/agentscope-ai/QwenPaw/issues/4454) | `/mission` 命令导致 Console 完全卡死，无法响应 | 开放 14 天 | 无 |
| **高** | [#4123](https://github.com/agentscope-ai/QwenPaw/issues/4123) | 每次 `execute_shell_command` 弹出 cmd 窗口闪烁 | 开放 23 天 | 无 |
| **高** | [#4829](https://github.com/agentscope-ai/QwenPaw/issues/4829) | 与 #4123 基本重复，Windows Tauri 版也有相同问题 | 新开 1 天 | 无 |
| **中** | [#4824](https://github.com/agentscope-ai/QwenPaw/issues/4824) | ACP 协议版本号格式错误，无法连接 Claude Code | 新开 1 天 | 无 |
| **低** | [#4831](https://github.com/agentscope-ai/QwenPaw/issues/4831) | Docker 镜像缺少 `psycopg2-binary`、`pytz`、`mootdx`，重建后 Agent 功能异常 | 新开 1 天 | 无（功能需求） |

> **注意**：已关闭的 #4828 与 #4123/#4829 内容相同，可能是作者误操作，建议维护者统一追踪窗口闪烁问题。

---

## 6. 功能请求与路线图信号

当日出现多项新功能请求，部分与已有 PR 方向吻合。

| Issue | 功能描述 | 重要性信号 |
|-------|----------|------------|
| [#4408](https://github.com/agentscope-ai/QwenPaw/issues/4408) | 工作目录默认文件统一放入 `.qwenpaw` 隐藏文件夹 | 评论 7 条，社区共鸣强 |
| [#4826](https://github.com/agentscope-ai/QwenPaw/issues/4826) | 支持三种新消息处理模式（打断、等待、插入） | 类似 Hermes Agent 机制 |
| [#4830](https://github.com/agentscope-ai/QwenPaw/issues/4830) | Desktop 输出本地路径自动生成可点击链接 | 与 #4826 需求 1 完全重复，需求集中 |
| [#4831](https://github.com/agentscope-ai/QwenPaw/issues/4831) | 预置 `psycopg2-binary`、`pytz`、`mootdx` 到 Docker 镜像 | 来自量化交易场景，有明确使用场景 |

**路线图信号**：  
- **多模式消息打断机制** 和 **隐藏工作目录** 属于可预期的用户界面改进，与已有 PR #4689（provider 层兼容性）共同指向 QwenPaw 走向更成熟的桌面 Agent 平台。  
- 本地路径可点击功能在两天内被重复提出（#4826 和 #4830），说明该功能对桌面端用户是刚需，预计短期内会进入开发队列。

---

## 7. 用户反馈摘要

从 Issue 评论与描述中提炼：

- **好消息**：用户认同 Docker 镜像预装 `requests` 等包的做法，并希望继续扩展（#4831）。  
- **痛点**：  
  - Windows cmd 窗口闪烁：“连续执行多个命令时疯狂闪烁，根本无法专注”（来自 #4123 评论）  
  - `/mission` 卡死：“重置 session 也无效，只能 kill 进程”（#4454）  
  - ACP 协议报错：“版本号格式问题，导致 Internal error，完全无法使用 Claude Code 扩展”（#4824）  
- **期望**：  
  - “希望能像 Hermes 那样配置消息处理策略，现在打断机制太粗暴”（#4826）  
  - “工作目录太乱，所有配置文件散落在根目录，建议学习 OpenCode”（#4408）  
  - “桌面端输出路径如果能点击打开，就太方便了”（#4830）

> 整体而言，用户对项目功能方向认可，但稳定性细节（尤其是 Windows 和 Docker 持久化）亟需加强。

---

## 8. 待处理积压

以下 Issue / PR 长时间未得到充分响应或进展，建议维护者重点关注：

| 项目 | 创建/更新 | 天数 | 重要性 | 备注 |
|------|-----------|------|--------|------|
| [#4123](https://github.com/agentscope-ai/QwenPaw/issues/4123) | 2026‑05‑08 | 23 天 | ★★★★ | 窗口闪烁，重复举报 2 次，无 fix PR |
| [#4408](https://github.com/agentscope-ai/QwenPaw/issues/4408) | 2026‑05‑15 | 16 天 | ★★★ | 工作目录整洁，评论多，无跟进 |
| [#4454](https://github.com/agentscope-ai/QwenPaw/issues/4454) | 2026‑05‑17 | 14 天 | ★★★★★ | Mission 命令卡死，严重功能缺失 |
| [#4689](https://github.com/agentscope-ai/QwenPaw/pull/4689) | 2026‑05‑26 | 5 天 | ★★★ | 重要 provider 兼容性改进，仍待 review |

> 建议：下周应优先解决 **Mission 卡死** 和 **Windows 窗口闪烁** 两个核心 Bug，同时推进 #4689 合并以兼容更多推理服务。

---

**报告生成时间**：2026‑05‑31 23:59 UTC  
**分析师角色**：AI Agent 与个人 AI 助手领域开源项目分析师

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-05-31

**数据来源**：GitHub（github.com/zeroclaw-labs/zeroclaw）  
**统计时段**：2026-05-30 至 2026-05-31（过去24小时）  
**总览**  
- Issues 更新：50条（新开/活跃14条，已关闭36条）  
- PR 更新：50条（待合并22条，已合并/关闭28条）  
- 新版本发布：0个  

---

## 1. 今日速览

过去24小时项目保持高活跃度。新开14个 Issue 和 22 个待合并 PR 表明社区讨论和贡献仍在持续涌入。**桌面端功能完善**（macOS 权限流、菜单栏聊天面板）与 **语音双工通信**（VAD、STT 管线）的多项 PR 已合并落地，标志着 v0.8.0-beta-2 的功能集趋于完整。同时，关于 **computer-use 桌面控制**（#6909）和 **统一输出路由模型**（#6969）的 RFC 引发了热烈讨论，可能成为下一阶段核心方向。Bug 修复集中在渠道兼容性（WhatsApp、Webhook）和运行时稳定性，整体项目健康度良好。

---

## 2. 版本发布（无）

当前最新标签仍为 v0.8.0-beta-1，过去24小时内无新版本发布。大体积 PR #6848（“beta-2 integration”）仍处于 open 状态，等待首轮反馈，预计将构成下一预发布版本的基础。

---

## 3. 项目进展

**今日合并/关闭的重要 PR（选取对整体架构或关键功能有显著影响的条目）**

| PR | 标题 | 说明 |
|---|---|---|
| #6761 | feat(desktop): capability handlers for macOS UI control | 新增点击、按键、通知、AX读取等桌面控制能力，配合权限流实现 agent 对 macOS 的原生操作。 |
| #6762–#6767 | 系列 PR：macOS 权限流（辅助功能、屏幕录制、麦克风、输入监控、全盘访问、本地网络） | 统一引入 resume 权限重检、撤销检测及 WebView 事件通知，为桌面 agent 的敏感性操作提供基础安全设施。 |
| #5974, #5976, #5978 | 语音双工：WebSocket 二进制音频帧 + EnergyVAD + 语音捕获缓冲区 | 完成全双工语音通话的核心管线，支持 barge-in 打断，推动 #5896 语音功能从 RFC 走向可用原型。 |
| #6858 | fix(tui): clarify first-run empty states | 为 TUI 桌面版添加首次引导提示，提升新用户体验。 |
| #6952 | fix(tui): add Tab/Shift+Tab mode cycling for compact keyboards | 解决了紧凑键盘（无 F 键）无法切换 TUI 模式的问题，降低使用门槛。 |
| #6905 | fix(channels): keep runtime reload defaults context-scoped | 修复渠道运行时重载时默认值跨代理泄漏的问题，增强隔离性。 |
| #7027 | fix(channels): honor webhook Retry-After dates | 补齐 Webhook 重试对 HTTP-date 格式 `Retry-After` 的解析，避免重试逻辑失效。 |
| #7008 | fix(channels): deliver WhatsApp replies for LID JIDs | 修复 WhatsApp LID JID 到 phone JID 的解析，使 DM 自聊和回复可送达。 |

**总体判断**：项目在 **桌面原生控制**、**语音通话**、**TUI 体验** 三个方向同时取得实质性进展，累计合并约 15 个 PR，代码健康度和功能覆盖进一步提升。

---

## 4. 社区热点

以下 Issue / PR 在24小时内获得了最密集的讨论（按评论数排序，均 ≥3 条）：

- **#6909** [[Feature]: computer-use support](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)  
  讨论焦点：ZeroClaw 是否应引入类似 OpenAI Codex/Peekaboo 的桌面 GUI 控制（截图+鼠标键盘事件）。作者 `NiuBlibing` 提出了完整的需求场景。社区对 risk:high 和 p2 优先级有不同看法，但普遍认为这是 agent 能力的重要补充。

- **#6883** [RFC: Shared reply-message constructor on SendMessage](https://github.com/zeroclaw-labs/zeroclaw/issues/6883)  
  讨论焦点：如何标准化从 `ChannelMessage` 构建 `SendMessage` 的三个重复步骤。作者 `mov-xound-glitch` 提供了实现草案，社区讨论了是否应与现有 builder 模式兼容。

- **#6954** [RFC: Route scheduled tasks through the orchestrator message pipeline](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)  
  讨论焦点：将 cron 任务也纳入 orchestrator 消息管线，解决一系列由绕过管线导致的 bug（#6037 等）。社区一致认同方向，但关注风险（high）和迁移成本。

- **#6969** [RFC: unified output routing model](https://github.com/zeroclaw-labs/zeroclaw/issues/6969)  
  讨论焦点：允许用户/agent 通过持久偏好或指令控制回复的发送方式和位置（如特定渠道、格式）。作者从 Letta 迁移而来，列举了多个缺失场景。社区反应积极，认为是提升自主性的关键设计。

**诉求分析**：上述热点揭示了社区对 **agent 环境交互能力**（computer-use）、**编排透明性**（scheduled tasks）、**输出个性化**（routing）的强烈需求，用户希望 ZeroClaw 不仅是一个聊天框架，更是一个能够自主操控桌面和灵活响应的智能体平台。

---

## 5. Bug 与稳定性

**今日更新的 Bug 报告，按严重程度排列（p1 最严重）：**

| Issue | 标题 | 严重程度 | 状态 | 修复 PR |
|---|---|---|---|---|
| #7022 | [kimi-k2.6 fails with 400 invalid temperature](https://github.com/zeroclaw-labs/zeroclaw/issues/7022) | p1 (workflow blocked) | OPEN | 暂无 |
| #6876 | [allowed_tools does not restrict MCP tools](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) | p1 (安全/配置歧义) | OPEN | 讨论中，已在 #6914 提案执行强制 |
| #6914 | [enforce allowed_tools / denied_tools in main agent loop](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) | p1 (安全机制缺失) | OPEN (blocked) | 对应 PR 未出现，但 #7014 提及运行时 profile 可能涉及 |
| #6916 | [process-memory limits on shell/skill_tool subprocess](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) | p1 (容器 OOM 风险) | OPEN (blocked) | 暂无 |
| #6876 | 同上 | p1 | OPEN | 见上文 |
| #6917 | [honor action-scope filter in Composio tool dispatch](https://github.com/zeroclaw-labs/zeroclaw/issues/6917) | p2 | OPEN (blocked) | 暂无 |
| #6915 | [skill-scoped tool activation](https://github.com/zeroclaw-labs/zeroclaw/issues/6915) | p2 | OPEN (blocked) | 暂无 |
| #7008 | WhatsApp 回复送达问题 | p2? | 已修复 (#7008 merged) | 已合并 |
| #7027 | Webhook Retry-After 解析 | p2? | 已修复 (#7027 open, 待合并) | 待合并 |
| #6983 | 流式回退失败修复 | p2? | 已修复 (#6983 open) | 待合并 |

**稳定性小结：** 今日新增 p1 bug 1个（#7022 Kimi 兼容性），另有 4 个 p1 级 Bug 尚未修复，集中分布在工具执行强制与资源限制方面。好消息是渠道相关的 3 个 bug 已有修复 PR，接近合并。

---

## 6. 功能请求与路线图信号

**过去24小时提出的新功能 / RFC（enhancement 类型）：**

- **#6909** computer-use 支持：若被接受，将开启桌面 agent 的 GUI 操作能力，预计需要大量基础设施（截图、输入模拟、权限管理）。已有部分权限 PR 为此铺垫（#6761 等）。
- **#6969** 统一输出路由模型：允许 agent 和用户设置偏好渠道/格式，配合 #6883 的 reply 构造器可形成完整的消息定制方案。
- **#6915** skill-scoped tool activation：为技能执行期间临时提升工具权限，与 #6914 的 allowlist 强制形成互补。
- **#7024** office-document parsing WASM 插件（p3）：社区贡献者 `metalmon` 提出，准备使用 WASM 插件实现 DOCX/XLSX/PPTX 到 Markdown 的转换，属于 feeler 提案，可能成为插件生态扩展方向。

**路线图信号：**
- `v0.8.0-beta-2` 的门槛 PR #6848 仍在等待 feedback，包含 TUI、RPC、DenyWithEdit 审批等重大变动。
- desktop 权限和语音管线已就绪，**computer-use** 可能成为 v0.9.0 的 Core Feature。
- 多个 block 状态的 Issue 依赖 maintainer review（`needs-maintainer-review`），若获得及时反馈，有望在 beta-2 中部分落地。

---

## 7. 用户反馈摘要

从 Issue 评论中提取的真实用户声音：

> **#6909** “ZeroClaw currently has no ability to interact with the desktop GUI. OpenAI Codex and openclaw/hermes both support computer-use…” — 用户希望 agent 能像竞品一样操控本地桌面，完成截图、点击等操作，这是当前明显的功能缺口。

> **#6969** “I recently migrated from Letta to ZeroClaw and one behaviour I relied on heavily is gone: the ability to control *how* and *where* a reply is delivered…” — 迁移用户对输出路由的缺失感到不便，早晨简报能发到 Telegram、深夜摘要存为邮件这类场景无法实现。

> **#6876** “Setting `allowed_tools = [...]` in a risk profile does not restrict MCP tools. This is intentional by design (there is a source comment explaining it), but the documentation does not reflect this.” — 用户对 allowed_tools 不限制 MCP 工具感到困惑，认为文档与行为不一致，影响信任。

> **#5649**（已关闭）“When using the web chat UI, there's no way to paste a screenshot from clipboard (Ctrl+V) or drag-and-drop an image file… Both feel like natural gestures and currently missing.” — 用户期待更直觉的图片输入方式，该需求已在 desktop 面板中通过 #6323 解决，web 端仍需跟进。

**总体情绪：** 社区对 ZeroClaw 的定制性和扩展性有较高期待，迁移用户（来自 Letta）带来了新的使用场景压力；配置文档的一处 gap（#6876）引发了安全顾虑，需要尽快澄清。

---

## 8. 待处理积压

以下为长期未响应或可影响重要功能推进的 Issue / PR，提请维护团队关注：

| 编号 | 标题 | 静默时长（从最后更新计算） | 阻碍因素 |
|---|---|---|---|
| #6876 | allowed_tools does not restrict MCP tools — by design or documentation gap? | 8天（p1，安全相关） | 需 maintainer 明确设计决策并更新文档 |
| #6914 | enforce allowed_tools/denied_tools in main agent loop | 6天（p1，blocked） | 依赖 #6876 决策，且需要 maintainer review |
| #6915 | skill-scoped tool activation | 6天（p2，blocked） | needs-maintainer-review |
| #6916 | process-memory limits on shell subprocess | 6天（p1，blocked） | 设计讨论未启动，但生产环境已暴露风险 |
| #6917 | honor action-scope filter in Composio dispatch | 6天（p2，blocked） | 需要 Composio 集成维护者确认 |
| #6883 | RFC: Shared reply-message constructor | 8天（p3） | 虽为 p3，但影响 #6969 实现，建议加快决策 |
| #6848 | beta-2 integration（PR） | 9天（DO NOT MERGE） | 等待首轮反馈，若长期无 review 可能影响 beta-2 发布节奏 |

**建议行动：**  
- 对 #6876 尽快给出官方回复（design 或 doc gap），解除 #6914 的阻塞。  
- 对 #6916 评估现代 overcommit 环境下的实际风险，可参考 #6914 的 profile 方案。  
- 对 #6848 发起 maintainer review 轮次，避免 beta-2 无限期延迟。  

---

*日报自动生成，数据基于 ZeroClaw GitHub 仓库公开信息。如有遗漏，请以原始 Issue/PR 讨论为准。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*