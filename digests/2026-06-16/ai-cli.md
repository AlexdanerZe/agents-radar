# AI CLI 工具社区动态日报 2026-06-16

> 生成时间: 2026-06-16 03:44 UTC | 覆盖工具: 9 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告（2026-06-16）

---

## 1. 生态全景

当前 AI CLI 工具整体处于“从对话助手向自主 Agent 快速演进”的阶段，各项目在 **Agent 能力、MCP 生态、跨平台兼容性** 上密集发力。但伴随能力膨胀，**稳定性回退、资源泄漏、安全误报** 成为社区普遍焦虑点——用户对可靠性的诉求已超过对功能的追求。同时，**多 Provider 支持、会话持久化、精细权限控制** 正成为各工具竞争的基础配置。社区活跃度呈“头部集中、长尾跟进”格局：OpenAI Codex 与 Claude Code 以庞大用户基数维持高热讨论，而开源新秀如 OpenCode、Qwen Code、Pi 则在特定领域快速追赶。

---

## 2. 各工具活跃度对比

| 工具 | 当日版本发布 | 热点 Issues¹ | 热点 PRs¹ | 当天 Issue 更新量 | 当天 PR 更新量 | 社区最高赞² |
|---|---|---|---|---|---|---|
| **Claude Code** | v2.1.178 | 10 | 10 | — | — | 163👍 |
| **OpenAI Codex** | v0.140.0 / Alpha | 10 | 10 | — | — | 583👍 |
| **Gemini CLI** | 无 | 10 | 10 | — | — | 8👍³ |
| **GitHub Copilot CLI** | v1.0.63 / v1.0.63-0 | 10 (精选) | 1 | 44 | 1 | 8👍 |
| **Kimi Code CLI** | 无 | 4 | 2 | 4 | 2 | 0👍 |
| **OpenCode** | 无 | 10 | 10 | — | — | 84👍 |
| **Pi** | v0.79.4 | 10 | 10 | — | — | 30👍 |
| **Qwen Code** | v0.18.1 / desktop-v0.0.4 | 10 | 10 | — | — | —⁴ |
| **DeepSeek TUI** | 无（v0.8.59 里程碑） | 10 | 10 | — | — | —⁵ |

> ¹ 各日报精选的代表性 Issues/PRs，非当日全量。² 各仓库当前 Issues 最高 👍 数（反映社区规模）。³ Gemini CLI 因早期阶段或社区语言原因，👍 数整体偏低。⁴ Qwen Code 日报未标注 👍 数，但评论活跃（如 #5055 评论5， #5180 评论2）。⁵ DeepSeek TUI 热点 Issue 多靠评论数体现（#2487 13 评论）。

**解读：**
- **OpenAI Codex / Claude Code** 仍为社区体量第一梯队，单 Issue 点赞可超 500。
- **Copilot CLI** 当日 Issue 更新 44 条，社区参与度高，但 PR 活跃度极低（仅 1 条垃圾 PR），说明核心团队发布节奏与社区期待可能脱节。
- **Kimi Code CLI** 活跃度最低，处于早期用户积累阶段。
- **OpenCode / Qwen Code / Pi / DeepSeek TUI** 均有 10 个以上 PR 进入日报精选，开发迭代活跃。

---

## 3. 共同关注的功能方向

### ① 会话持久化与记忆生命周期管理
- **涉及工具**：Claude Code、Codex、Gemini CLI、Copilot CLI、OpenCode、Qwen Code、Pi
- **具体诉求**：用户不满足于简单的对话续接，要求**持久会话目标（/goal）、多层记忆（外部知识库）、归档/清空/删除的标准化 API**，并希望记忆系统能自动过滤低价值信息（Gemini CLI #26522）。这是所有工具迈向“生产力工具”的共同基础能力。

### ② MCP 协议标准化与扩展治理
- **涉及工具**：Claude Code、Copilot CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI
- **具体诉求**：MCP 服务器无界扇出导致资源耗尽（Claude Code #64366）、Schema 兼容性问题（Pi #3214）、企业策略屏蔽第三方服务器（Copilot CLI #3756）、落后于 MCP 最新标准（OpenCode #28567）。社区强烈要求官方提供 **工具注册、权限隔离、SSRF 防护、配置优先级合并** 等治理能力。

### ③ 跨平台体验一致性
- **涉及工具**：全部 9 个工具
- **具体诉求**：Windows TUI 滚轮（Claude Code #12953）、WSL 路径重写（Codex #28094）、macOS 资源泄漏（Codex #25719）、Linux 桌面端缺失（Codex #11023）、乱码/编码问题（Copilot CLI #3776）、Wayland 兼容（Gemini CLI #21983）、Git Bash 识别失败（Pi #5103）、安全软件误报（Qwen Code #5055）。用户期望“一次学习，处处可用”，各平台稳定性成为口碑分水岭。

### ④ 安全与权限精细控制
- **涉及工具**：Claude Code、Gemini CLI、Copilot CLI、OpenCode、DeepSeek TUI
- **具体诉求**：细粒度权限规则（Claude Code `Tool(param:value)` 语法）、持久化允许/拒绝规则（DeepSeek TUI #1186）、最小权限原则（Copilot CLI #953）、沙箱限制 Agent 只操作当前目录（OpenCode #2242）、SSRF 防护与 DNS 解析拦截（Gemini CLI #27744）。Agent 越强，安全边界越重要。

### ⑤ 性能与资源效率透明化
- **涉及工具**：Claude Code、Codex、Copilot CLI、OpenCode、Qwen Code、DeepSeek TUI
- **具体诉求**：请求失败仍计费（Copilot CLI #3814）、大工具结果反复塞入导致上下文爆炸（Qwen Code #5101）、Token 速率显示（OpenCode #5374）、Memory 低价值会话无限重试（Gemini CLI #26522）、OOM 崩溃（Qwen Code #5147）。用户要求 **可观测的用量和可预期的资源消耗**。

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 功能侧重 | 目标用户 | 技术路线特征 |
|---|---|---|---|---|
| **Claude Code** | Agentic 开发协作者 | 高级权限控制、技能目录、子代理调度 | 追求深度 Agent 自动化与安全治理的团队 | 基于 Anthropic 模型，强调规则引擎与 Hookify 插件体系 |
| **OpenAI Codex** | 全栈智能 IDE 扩展 | 性能、多 Agent 模式、Guardian 安全审查 | 大规模团队、企业级用户 | Rust 核心，重度集成 VS Code，强调多模型与多模态 |
| **Gemini CLI** | 安全优先的 Agent 工具 | SSRF 深度防御、Auto-memory、AST 感知代码 | 对安全合规有高要求的开发者 | 深度绑定 Google 生态，强调 DNS 级 SSRF 防护与配置合并 |
| **GitHub Copilot CLI** | 企业级 GitHub 生态 CLI | BYOK 模型、会话管理、MCP 扩展 | GitHub Enterprise 用户 | 与 GitHub 深度集成，近期重心在插桩稳定性与插件 Hook |
| **Kimi Code CLI** | 轻量对话式代码助手 | 会话续接、Hook 系统 | 个人开发者 | 最小化功能集，起步阶段，依赖 Moonshot 模型 |
| **OpenCode** | 开源全能型 Agent 平台 | MCP 标准化、会话生命周期、内存管理 | 开源社区与自建用户 | 社区驱动，强 MCP 兼容性，注重 OSS 生态和 TUI 体验 |
| **Pi** | Provider 多元化的 TUI 终端 | 多云服务接入（Bedrock、ZAI、OpenAI）、Vim 模式 | 多模型使用者、Vim 用户 | 插件系统开放，强调 Provider 即插即用与扩展架构解耦 |
| **Qwen Code** | 循环自动化与工作流 | /loop 原语、工作流阶段树、safe-mode | 需要长时间后台任务的用户 | Qwen 模型围绕，强调 /loop 生态、多 Provider 消歧义和交互式扩展管理器 |
| **DeepSeek TUI** | 架构驱动的 Agent 运行时 | Provider 注册表、子代理无头化、持久权限、i18n | 开源贡献者与架构探索者 | 坚持底层重构（registry、worker runtime），国际化（i18n）同步推进 |

**核心分化主线：**
- **生态绑定 vs 开放中立**：Codex（OpenAI）、Gemini CLI（Google）、Claude Code（Anthropic）深度绑定自家模型；Copilot CLI 绑定 GitHub 生态；OpenCode、Pi、DeepSeek TUI 更强调 Provider 中立。
- **Agent 自主度**：Claude Code 在权限控制上最激进（`Tool(param:value)` 语法），Qwen Code 在循环自动化上最专注，Gemini CLI 则在安全隔离上走在前列。
- **成熟度 vs 创新速度**：Codex 与 Claude Code 社区庞大但性能和安全问题多；Qwen Code、OpenCode、DeepSeek TUI 迭代迅猛，但功能稳定性和文档仍需追赶。

---

## 5. 社区热度与成熟度

| 梯队 | 工具 | 社区热度特征 | 发展阶段 |
|---|---|---|---|
| **头部成熟** | OpenAI Codex、Claude Code | 高赞 Issue 数百、讨论密集、回归问题引发信任度波动 | 快速迭代但稳定性承压；版本号高（v2+/v0.140+） |
| **快速成长** | OpenCode、Qwen Code、Pi | 日均 PR 10+，功能提案活跃，社区贡献者积极 | 从早期走向主流：OpenCode 记忆管理与 MCP 标准化、Qwen Code 工作流、Pi 多 Provider 扩展 |
| **企业级演进** | GitHub Copilot CLI | 更新量大（44 Issues），但核心开发活跃度偏低（PR 仅1），用户期待深度治理 | 依托 GitHub 生态，在安全/多模型/会话管理上需求强劲，需加快响应 |
| **特化跟随** | Gemini CLI、DeepSeek TUI | 社区规模较小，但技术深度强（SSRF、架构重构），吸引特定用户 | 早期快速发展期：Gemini CLI 是安全标杆，DeepSeek TUI 在重构上投入大 |
| **初期探索** | Kimi Code CLI | 每日 4-6 更新，点赞少，社区尚未形成规模 | 功能基础补全与平台适配阶段 |

**补充观察：**
- **Copilot CLI** 虽然社区活跃（44 条更新），但只有 1 个 PR，存在“用户反馈越多，官方交付越慢”的风险，可能影响生态信心。
- **OpenCode** 最高赞 Issue 84👍，且内存排查帖获得 97 条评论，说明其用户群体不仅关注功能，也愿参与诊断，社区共建氛围好。
- **Pi** 虽然版本号低（v0.79.4），但已支持丰富 Provider 和 Vim 插件，社区反馈积极，属于隐藏黑马。

---

## 6. 值得关注的趋势信号

### ① 安全正从“功能选项”变为“准入条件”
Gemini CLI 连发 3 个 SSRF 修复 PR，Claude Code 新增 `Tool(param:value)` 精确拦截，Copilot CLI 社区反复要求最小权限——当 Agent 能写文件、改代码、发请求时，**安全防护不再是加分项，而是用户愿不愿意使用的先决条件**。开发者选型时需将该工具的权限模型纳入第一优先级评估。

### ② “失败不计费”成为信任锚点
Copilot CLI #3814（失败仍计 AIC）、Codex 社区对性能的抱怨，显示用户对资源消耗的敏感性已从 Token 数量上升到**成本与成功率的挂钩**。未来 CLI 工具需提供“请求不成功不计费”或“失败重试不重复计费”的机制，否则将面临用户流失。

### ③ MCP 急需治理框架
几乎所有工具的 MCP 模块都出现“无界扇出”“Schema 不兼容”“配置绕过”等问题。MCP 虽已成为事实上的扩展标准，但缺乏**资源限制、权限分域、服务器生命周期管理**能力。能够率先提供成熟 MCP 治理方案的工具，将在生态位竞争中占据高地。

### ④ 会话生命周期管理已成为“刚需基础设施”
从 `/goal`（OpenCode）、`--continue`（Kimi）、会话归档（OpenCode #32499）到记忆低价值过滤（Gemini CLI），用户不再把对话看成一次性交互，而是**可持久化、可检索、可回溯的知识资产**。工具需要提供显式 API 来管理会话状态，而非让用户依赖文件系统 hack。

### ⑤ 跨平台兼容决定长尾用户留存
Windows、macOS、Linux 三端的表现差距正在消耗用户的耐心。特别是 **Windows WSL 路径重写**（Codex #28094）和 **macOS 资源泄漏**（Codex #25719）等问题是高频复现的“劝退 Bug”。对于追求开发者全平台覆盖的团队，建议关注工具的跨平台测试密度和 issue 响应速度。

### ⑥ 社区渴望“可预测的稳定性”胜过“新奇功能”
多份日报提及回归问题（Copilot CLI v1.0.60 Hook 断裂、Claude Code Opus 思维块丢失、Qwen Code 子代理崩溃）。用户对“前一个版本能用，升级后坏了”的容忍度急剧降低。建议工具维护者在发布前引入**更严格的自动化回归测试与兼容性检查**，尤其是针对插件接口、MCP 协议和安全策略。

---

**总结：**  
AI CLI 工具正经历从“技术演示”到“严肃生产力工具”的阵痛期。社区核心诉求从“更多功能”转向“更稳定、更安全、更一致”。对于技术决策者：**优先选用在安全治理、会话管理、跨平台兼容性上有明确路线图且社区响应迅速的工具**；对于开发者：持续关注 MCP 生态演进与 Provider 中立性，减少未来迁移成本。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，根据提供的仓库数据，我为你整理了一份关于 Claude Code Skills 生态的社区热点分析报告。

---

## Claude Code Skills 社区热点报告（数据截止 2026-06-16）

### 1. 热门 Skills 排行

根据社区评论活跃度，以下 Skills 最受关注：

- **#514 Add document-typography skill** [OPEN]
  - **功能**：针对 AI 生成文档的排版质检，修复孤词、孤行及编号错位。
  - **讨论热点**：这是 AI 文档生成的“最后一公里”痛点，用户共鸣度极高。几乎所有由 Claude 生成的报告都需要此类 Quality Control。
  - **状态**：Open，社区反响热烈，期待落地。
  - **链接**：https://github.com/anthropics/skills/pull/514

- **#154 Add shodh-memory skill** [OPEN]
  - **功能**：跨会话持久记忆系统，允许 AI Agent 维护上下文状态。
  - **讨论热点**：长周期 Agent 任务和复杂项目管理的基础设施，社区激烈讨论结构化记忆存储与检索的效率。
  - **状态**：Open，已有一段时间的迭代历史。
  - **链接**：https://github.com/anthropics/skills/pull/154

- **#444 feat: add AURELION skill suite** [OPEN]
  - **功能**：AURELION 生态的4个技能（内核、顾问、Agent、记忆），提供结构化的认知框架（5层思维模型）。
  - **讨论热点**：高阶 Agent 设计模式。社区关注如何通过 SKILL.md 文件注入复杂的认知逻辑，以提升 Agent 的推理能力。
  - **状态**：Open
  - **链接**：https://github.com/anthropics/skills/pull/444

- **#723 feat: add testing-patterns skill** [OPEN]
  - **功能**：覆盖完整测试栈，包含单元测试、React 组件测试及测试哲学。
  - **讨论热点**：开发者社区的基础诉求，讨论了“测试奖杯模型”与实际场景的结合。
  - **状态**：Open
  - **链接**：https://github.com/anthropics/skills/pull/723

- **#1140 feat: implement agent-creator skill** [OPEN]
  - **功能**：元技能（Meta-Skill），用于动态生成特定任务的 Agent 工具集。
  - **讨论热点**：解决技能组合的灵活性问题，同时修复了并行多工具调用的评估 bug。
  - **状态**：Open，关联 Issue #1120，热度很高。
  - **链接**：https://github.com/anthropics/skills/pull/1140

- **#147 Add codebase-inventory-audit skill** [OPEN]
  - **功能**：系统化代码库清理和文档审计，识别遗弃代码和监控盲区。
  - **讨论热点**：面向大型遗留代码库的维护场景，产出物 `CODEBASE-STATUS.md` 的标准化格式受到关注。
  - **状态**：Open
  - **链接**：https://github.com/anthropics/skills/pull/147

- **#210 Improve frontend-design skill** [OPEN]
  - **功能**：重写前端设计技能，使其指令更具体、可执行性强。
  - **讨论热点**：如何撰写真正能让 Claude 严格遵循的设计规范，避免 AI 生成设计的随机性。
  - **状态**：Open
  - **链接**：https://github.com/anthropics/skills/pull/210

---

### 2. 社区需求趋势

从 Issues 分析，社区最期待的新 Skill 方向集中在以下几点：

- **工作流自动化与代码质量**
  - 通过 `testing-patterns` (PR #723) 等技能，社区强烈需要更可靠的代码测试生成方案，以嵌入 CI/CD 流程。
  - `document-typography` (PR #514) 的高热度反应了社区对“成品质量”的极致追求，期望 AI 输出直接达到出版级标准。

- **Agent 认知架构与持久化**
  - 社区不满足于无状态对话。`shodh-memory` (PR #154) 和 `AURELION` (PR #444) 揭示了对“记忆”和“结构化思维”的强需求。
  - Issue #412 提案的 `agent-governance` 反映了对 Agent 行为的策略强制、威胁检测和审计追溯的深层安全担忧。

- **生态与平台痛点**
  - **组织级共享**：Issue #228 获得极高的赞数，用户迫切需要通过链接或共享库分发技能，而非手动传文件上传。
  - **安全性**：Issue #492 强烈批判了第三方技能借用官方命名空间造成的信任边界问题，社区对安全审计的关注度急剧上升。
  - **工具链稳定性**：Issues #556, #1169, #1061 反复报告 `skill-creator` 脚本在不同环境下（尤其是 Windows）返回 `recall=0%` 或崩溃。这是阻碍社区贡献与效率的最大摩擦点。

---

### 3. 高潜力待合并 Skills

以下 PR 评论活跃、解决核心痛点、代码逻辑清晰，预计近期有高度落地可能：

- **skill-creator 修复全家桶 (PR #1298, #1099, #1050, #361, #362)** [ALL OPEN]
  - **说明**：围绕 `run_eval.py` 在 Windows 上的崩溃、YAML 解析失败、UTF-8 编码导致 Panic 等问题，多位贡献者提交了互补性修复。这是目前最紧急、合并价值最高的基础设施改进，直接决定了生态开发者体验。
  - **链接**：https://github.com/anthropics/skills/pull/1298

- **document-typography (PR #514)** [OPEN]
  - **说明**：覆盖极广（所有 Claude 生成的文档），逻辑清晰（孤行/孤页/编号），无复杂副作用，是提升用户体验的“守门员”型技能。
  - **链接**：https://github.com/anthropics/skills/pull/514

- **testing-patterns (PR #723)** [OPEN]
  - **说明**：不只是一个技能，而是一个完整的“测试方法论套装”。如果 Anthropic 希望 Claude Code 进入专业 DevOps 流程，这是必要的基础设施。
  - **链接**：https://github.com/anthropics/skills/pull/723

- **shodh-memory (PR #154)** [OPEN]
  - **说明**：Agent 持久化是通往自主工作流的必经之路，该技能如能合并，将大幅提升 Claude 对复杂多轮项目的理解和跟踪能力。
  - **链接**：https://github.com/anthropics/skills/pull/154

---

### 4. Skills 生态洞察

> **一句话总结：社区当前最集中的诉求是“加固基础工具链并突破 Agent 能力天花板”——一方面在疯狂修复技能开发脚本的 Windows 兼容性与评估准确性（run_eval.py），另一方面则通过记忆系统、认知架构和治理模型探索 Agent 的自主性边界。**

---

好的，各位开发者，以下是 2026 年 6 月 16 日的 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-06-16

## 1. 今日速览

今日社区围绕 **macOS 平台严重的资源泄露与磁盘误报问题** 展开了密集讨论（ENOSPC 假阳性、MCP 无界扇出），多项 Issue 持续发酵。官方方面，**v2.1.178 正式发布**，主要增强了权限控制语法并支持技能目录嵌套。与此同时，外部贡献者 **AZERDSQ131 今日集中提交了超过十项修复型 PR**，覆盖插件系统、工作流 CI 及跨平台兼容性，成为今日生态修复的主力军。

## 2. 版本发布

**v2.1.178** 更新内容如下：
- **权限规则增强**：新增 `Tool(param:value)` 语法，允许匹配工具的具体输入参数。典型场景如 `Agent(model:opus)` 可精确拦截对 Opus 子代理的调用，支持 `*` 通配符。
- **技能目录嵌套**：现在可以加载嵌套在 `.claude/skills` 目录中的技能。当出现重名冲突时，嵌套目录的技能享有更高优先级。

## 3. 社区热点 Issues (Top 10)

1. **#24726** [Feature] [VS Code] 添加禁用自动附加打开文件/选区的设置
   - 热度：163 👍 / 53 💬。社区最强烈的 IDE 集成诉求，用户反感“过度自动化”干扰正常编码流程。
   - [链接](https://github.com/anthropics/claude-code/issues/24726)

2. **#29045** [Bug] Claude Desktop 每次启动都会生成 1.8GB 的 Hyper-V 虚拟机
   - 热度：56 👍 / 27 💬。即使仅用于纯聊天也无法避免巨大资源开销，引发对沙箱架构合理性的质疑。
   - [链接](https://github.com/anthropics/claude-code/issues/29045)

3. **#47023** [Feature] 基于 Profile/会话生命周期 Hook 实现外部记忆层
   - 热度：22 💬。社区自建解决方案（三层 Markdown、知识图谱）日益成熟，但渴望官方提供标准 API 来接入持久化记忆，避免重复造轮子。
   - [链接](https://github.com/anthropics/claude-code/issues/47023)

4. **#48334** [Bug] Desktop 应用更新导致会话历史丢失
   - 热度：16 💬。涉及 sessions-index.json 及 .jsonl 文件被清空，属于严重的数据丢失事故，信任度受创。
   - [链接](https://github.com/anthropics/claude-code/issues/48334)

5. **#12953** [Bug] Windows TUI 鼠标滚轮滚动输入历史而非聊天历史
   - 热度：14 👍 / 16 💬。2025 年 12 月提起的“化石级” Bug，严重影响 Windows 平台用户的浏览体验，尚未修复。
   - [链接](https://github.com/anthropics/claude-code/issues/12953)

6. **#38536** [Feature] 团队共享记忆系统
   - 热度：13 💬。针对工程团队协作场景，要求打破个体记忆孤岛，实现上下文无缝流转。
   - [链接](https://github.com/anthropics/claude-code/issues/38536)

7. **#63909** [Bug] Bash 工具捕获子进程输出时误报 ENOSPC（空间不足）
   - 热度：19 👍 / 12 💬。高频复现，所有带输出的命令均会失败，极端影响 macOS 用户日常开发节奏。
   - [链接](https://github.com/anthropics/claude-code/issues/63909)

8. **#64366** [Bug] Cowork/Agent 模式下 MCP 服务器无界扇出，耗尽内存并导致 macOS 内核崩溃
   - 热度：12 💬。报告了 4 次内核恐慌及强制关机事件（M2 Max / 32GB），属于重大的稳定性事故。
   - [链接](https://github.com/anthropics/claude-code/issues/64366)

9. **#63358** [Bug] Opus 4.8 返回空白 Extended Thinking 块
   - 热度：10 👍 / 10 💬。与 Opus 4.7 的回归属同源问题，开启思考后 UI 没有任何渲染内容，模型核心价值缩水。
   - [链接](https://github.com/anthropics/claude-code/issues/63358)

10. **#63423** [Bug] CLI v2.1.154 因 API 返回 422 “system” role 错误而全面瘫痪
    - 热度：8 💬。典型的版本回归Bug，直接阻断用户正常使用 CLI 连接 Anthropic API。
    - [链接](https://github.com/anthropics/claude-code/issues/63423)

## 4. 重要 PR 进展 (Top 10)

1. **#68707** [新功能] 新增 `/bug` 命令以直接在终端内提交 Issue
   - 自动采集环境信息并提交 GitHub Issue，显著降低 Bug 上报门槛。
   - [链接](https://github.com/anthropics/claude-code/pull/68707)

2. **#68678** [修复] 修复 Triage 机器人误将 Desktop 问题标记为无效
   - 确保桌面端用户的 Bug 反馈能被正常接收与处理。
   - [链接](https://github.com/anthropics/claude-code/pull/68678)

3. **#68679** [修复] 修复 Ralph-Wiggum 循环停止钩子的控制字符污染
   - 核心修复。解决终端转义序列导致 `<promise>` 令牌检测失败的问题，确保 Agent 循环的正向终止。
   - [链接](https://github.com/anthropics/claude-code/pull/68679)

4. **#68672** [修复] 修复 Hookify 插件事件路由逻辑
   - 修复了当工具非 `Bash`/`Edit` 时 event 变量为 `None`，导致 Hook 无法加载的严重 Bug。
   - [链接](https://github.com/anthropics/claude-code/pull/68672)

5. **#68671** [修复] 修复 Hookify 中 PostToolUse 权限决策错误
   - 修复规则引擎在工具调用后错误返回 `deny` 的逻辑，保证权限链路准确。
   - [链接](https://github.com/anthropics/claude-code/pull/68671)

6. **#68681** [修复] 修复 CI 工作流分页逻辑 Bug
   - 修复 `length === 0` 导致的提前终止问题，确保脚本在处理大量 Issue 时能完整遍历所有页。
   - [链接](https://github.com/anthropics/claude-code/pull/68681)

7. **#68700** [修复] 修复 `learning-output-style` 插件在 Windows 上的路径兼容性
   - 解决 Windows 路径反斜杠及缺少 Bash 前缀导致 Hook 执行失败的问题。
   - [链接](https://github.com/anthropics/claude-code/pull/68700)

8. **#68702** [修复] 修复 macOS Bash 3.x 上 Ralph-Wiggum 脚本的变量扩展错误
   - macOS 用户无法直接使用 `/ralph` 命令的问题被解决，覆盖大量还未迁移新 Shell 的开发者。
   - [链接](https://github.com/anthropics/claude-code/pull/68702)

9. **#68689** [安全] 修复 `security-guidance` 插件符号链接逃逸漏洞
   - 防止恶意符号链接通过配置文件读取实现路径穿越，保障自定义安全规则库的隔离性。
   - [链接](https://github.com/anthropics/claude-code/pull/68689)

10. **#68699** [修复] 修复 Windows 上 Hookify 插件 Python 解释器检测
    - 解决 `python3` 命令在 Windows 上指向错误解释器（如 Microsoft Store 占位程序）导致插件失效的问题。
    - [链接](https://github.com/anthropics/claude-code/pull/68699)

## 5. 功能需求趋势

- **IDE 集成精细化**：社区不再满足于简单的插件嵌入，而是追求**深度可控的 IDE 交互**（如精确控制自动上下文注入、增量选择代码）。这是从“可用”迈向“好用”的必经之路。
- **持久化记忆体系亟待官方化**：围绕记忆管理的多项高赞 Issue 表明，**社区对官方记忆 API 的渴求已到临界点**。自建方案已泛滥，但缺乏安全、稳定的官方接口限制了一键式体验。
- **对话生命周期管理需求觉醒**：随着使用时长增加，用户开始要求**基础的对话管理设施**（归档、清空、删除）。这是成熟开发工具的必需品。
- **平台一致性呼声高涨**：Windows 和 macOS 上的各种怪异 Bug（TUI 滚轮、ENOSPC 假警报、路径兼容性）正在消耗用户的耐心。社区强烈要求各平台间的基础体验能够拉齐。

## 6. 开发者关注点

- **对“稳定性回归”极度敏感**：Opus 思维块丢失、CLI API 握手失败、Agent 权限回退……高频的回归 Bug 正在消耗用户对新版本的信任。开发者呼吁引入更严格的自动化回归测试套件。
- **扩展机制仍有距离**：虽然 Hookify 等插件展现了巨大潜力，但**10k 字限制**、**跨平台兼容性差**、**缺乏完善的官方文档**使得深度玩家在扩展时步履维艰，期待官方投入更多资源到扩展层的成熟度上。
- **协作模式需要更坚固的安全沙箱**：Agent/Cowork 的下放能力令人兴奋，但 **MCP 无界扇出踩穿内存**、**子 Agent 权限失效** 等问题暴露了沙箱隔离机制的不足。在推广 Agentic 能力的同时，资源审计和隔离防护必须同步跟上。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-06-16

---

## 今日速览

- **版本加速迭代**：`v0.140.0` 正式版发布，带来 `/usage` 用量视图、`/goal` 增强及永久会话删除功能；同时 `v0.141.0-alpha.1/2` 启动新一轮 alpha 测试。
- **社区焦点转移至稳定性**：Linux 桌面端请求（#11023）已收获 583 👍 仍为最强呼声；macOS 系统进程资源泄漏（#25719）和 Windows WSL 路径回归（#28094）成为平台侧最热的 bug，安全误报问题（#27817、#28015）也引发大量讨论。
- **基础设施持续加固**：PR 方面重点推进了持久化导入、推荐缓存、本地凭据代理及 Guardian 预启动，底层可靠性与响应速度有望明显提升。

---

## 版本发布

| 版本 | 类型 | 关键内容 |
|------|------|----------|
| `rust-v0.141.0-alpha.2` / `rust-v0.141.0-alpha.1` | Alpha | 下一阶段早期迭代 |
| `rust-v0.140.0` | 正式版 | 新增 `/usage`（日/周/累计 token 活动）；`/goal` 保留超大文本、粘贴块与图片附件；支持永久会话删除 |
| `rust-v0.140.0-alpha.20/21/22` | Alpha | v0.140.0 发布前内测 |

> 完整 Release Notes 可查看 GitHub Releases 页面。

---

## 社区热点 Issues（10 个）

### 1. #11023 — Linux 桌面 App 请求
- **链接**：https://github.com/openai/codex/issues/11023
- **状态**：OPEN | 评论 113 | 👍 583
- **为何重要**：长期高热度功能请求。用户因 macOS 能耗问题（#10432）急需 Linux 客户端，社区呼声极高，但至今无正式支持计划。

### 2. #12661 — Windows 上 Markdown `file://` 链接打开默认浏览器而非 VS Code
- **链接**：https://github.com/openai/codex/issues/12661
- **状态**：OPEN | 评论 47 | 👍 43
- **为何重要**：直接影响开发效率，点击本地 .md 文件链接会跳出到 Edge，而非在 VS Code 内打开。Windows 用户普遍受影响。

### 3. #3355 — MacBook 睡眠后请求断连
- **链接**：https://github.com/openai/codex/issues/3355
- **状态**：OPEN | 评论 37 | 👍 19
- **为何重要**：长时间任务合盖后重新打开无法继续，会话丢失。移动办公场景痛点，已存在近 10 个月仍未彻底修复。

### 4. #21527 — Codex 整体响应太慢
- **链接**：https://github.com/openai/codex/issues/21527
- **状态**：OPEN | 评论 32 | 👍 17
- **为何重要**：用户抱怨桌面 App 和 VS Code 插件均慢，Pro 订阅亦然。性能是普遍第一抱怨点。

### 5. #25719 — macOS `syspolicyd` / `trustd` CPU 与内存暴涨
- **链接**：https://github.com/openai/codex/issues/25719
- **状态**：OPEN | 评论 26 | 👍 33
- **为何重要**：Codex Desktop 在 macOS 上持续触发系统安全进程导致资源泄漏，只能重启恢复。严重干扰日常使用。

### 6. #27817 — 授权税务工作被误报为网络安全风险
- **链接**：https://github.com/openai/codex/issues/27817
- **状态**：OPEN | 评论 18 | 👍 0
- **为何重要**：正常个人税务对话被安全系统标记，要求加入“可信访问”计划。安全审查过于激进，影响真实业务场景。

### 7. #28015 — CLI 正常仓库维护被重复误报安全
- **链接**：https://github.com/openai/codex/issues/28015
- **状态**：OPEN | 评论 18 | 👍 0
- **为何重要**：`git add`、`git commit` 等日常操作频繁触发安全审查，中断交互式会话。与 #27817 一并反映误报问题的普遍性。

### 8. #28094 — Windows WSL 路径被重写为 `C:\home`，项目关联丢失
- **链接**：https://github.com/openai/codex/issues/28094
- **状态**：OPEN | 评论 13 | 👍 1
- **为何重要**：更新至 26.609.41114 后，WSL 下的 `/home` 路径被错误映射为 `C:\home`，导致已有项目聊天绑定全部失效。Windows + WSL 用户升级需谨慎。

### 9. #28190 — macOS 阻止 `rg`（ripgrep）运行
- **链接**：https://github.com/openai/codex/issues/28190
- **状态**：OPEN | 评论 9 | 👍 8
- **为何重要**：Codex CLI 依赖的 ripgrep 被 macOS Gatekeeper 阻断，直接影响了代码搜索功能。用户被迫寻找复杂变通方案。

### 10. #27331 — `multi_agent_v2` 启用后每轮都因 `encrypted-tools 400` 失败
- **链接**：https://github.com/openai/codex/issues/27331
- **状态**：OPEN | 评论 4 | 👍 5
- **为何重要**：仅在 `config.toml` 开启多智能体 v2 特性就导致每次对话请求都被拒绝，属于严重功能退化。阻碍用户尝试新能力。

---

## 重要 PR 进展（10 个）

### 1. #28396 — 持久化记录外部 Agent 导入结果
- **链接**：https://github.com/openai/codex/pull/28396
- **状态**：OPEN
- **摘要**：恢复导入进度通知，并将导入结果持久化至状态 DB，包括配置、AGENTS.md 和 skill 的详细成功/失败信息。

### 2. #28307 — TUI 通过 app-server 排队 follow-up 消息
- **链接**：https://github.com/openai/codex/pull/28307
- **状态**：OPEN
- **摘要**：终端 UI 可将 follow-up 消息交由 app-server 持久化并排队，解决了当前 TUI 只能本地保持消息的限制。

### 3. #28399 — 添加推荐插件端点缓存
- **链接**：https://github.com/openai/codex/pull/28399
- **状态**：OPEN
- **摘要**：对 `/ps/plugins/suggested/?scope=GLOBAL` 进行认证解析、去重、筛选及缓存，减少重复请求，加速推荐加载。

### 4. #27704 — [3/3] 激活端点插件推荐
- **链接**：https://github.com/openai/codex/pull/27704
- **状态**：OPEN
- **摘要**：每轮对话构建时等待端点推荐结果，消除首次缓存的竞争条件；按次快照推荐集，确保工具暴露与安装验证的一致性。

### 5. #28163 — 用户 Shell 命令使用本地环境
- **链接**：https://github.com/openai/codex/pull/28163
- **状态**：OPEN
- **摘要**：修复远程环境下 `shellCommand` 仍使用遗留会话 cwd 和 shell 的问题，统一为所选本地环境，提升跨环境一致性。

### 6. #28034 — 添加本地凭据代理
- **链接**：https://github.com/openai/codex/pull/28034
- **状态**：OPEN
- **摘要**：在 `network_proxy` 特性下新增 `credential_broker` 模式，虚拟化子进程凭据，仅在 MITM 请求时注入真实令牌，增强安全性。

### 7. #27982 — 在父会话启动时预创建 Guardian 子会话
- **链接**：https://github.com/openai/codex/pull/27982
- **状态**：OPEN
- **摘要**：自动审查（Guardian）子会话不再按需创建，改为随父会话一起初始化并预暖 WebSocket，减少首次审查延迟。

### 8. #28429 — 添加可中断睡眠工具
- **链接**：https://github.com/openai/codex/pull/28429
- **状态**：OPEN
- **摘要**：新增内置 `sleep` 工具（`sleep_tool` 特性门控），允许模型暂停等待外部操作，且收到新输入时可立即唤醒，避免进程阻塞。

### 9. #26334 — 重试 Guardian 临时审查失败
- **链接**：https://github.com/openai/codex/pull/26334
- **状态**：CLOSED（已合并）
- **摘要**：将临时性故障（容量、超时、传输错误）与真正的安全拒绝区分，对前者进行重试而非直接阻断，大幅减少误拒。

### 10. #27945 — 从状态 DB 预填充会话选择器
- **链接**：https://github.com/openai/codex/pull/27945
- **状态**：OPEN
- **摘要**：恢复/分叉会话列表不再完全依赖文件系统扫描，优先从状态 DB 索引首页展示，使选择器更快可用，同时保留后台扫描修正。

---

## 功能需求趋势

从本周议题标签及内容来看，社区最关注的方向依次为：

1. **跨平台支持与桌面生态**：Linux 桌面端仍是呼声最高的功能缺失；macOS 和 Windows 的稳定性问题（资源泄露、WSL 路径、提权）占 bug 报告超半数。
2. **性能与资源占用**：模型响应慢、syspolicyd/trustd 的 CPU 泄漏、Windows 下 WSL 大幅延迟被反复提及，成为影响留存率的核心因素。
3. **安全审查精确性**：正常工单被标记为网络安全风险的案例增多，社区要求更健全的误报判断和用户申诉渠道。
4. **会话与状态管理**：归档删除无效、特定类型的 `/goal` 会话不显示在恢复列表、持久化语义不一致等问题持续出现，体验细节有待打磨。
5. **Windows WSL 深度集成**：路径重写、sandbox helper 缺失、codex.exe 无法执行等问题说明 Codex 在 Windows 子系统上的适配仍不成熟。
6. **多智能体与计算机使用能力**：`multi_agent_v2` 的稳定性阻碍尝鲜；Windows 平台 Computer Use 入口缺失说明功能覆盖还不完整。

---

## 开发者关注点

汇总社区反馈中的痛点与高频需求：

- **性能首要痛点**：桌面 App 和 CLI 均被抱怨“慢”，尤其是与模型交互的首轮延迟和 WSL 下的每轮间隔。
- **安全误报引发信任危机**：允许的财务、Git 操作被阻断，用户不得不重复解释或放弃使用，严重影响工作效率。
- **macOS 特定资源问题**：`syspolicyd` 失控、睡眠后断连、rg 被拦截——macOS 用户正面临大量环境兼容性困扰。
- **Windows 平台磨损严重**：WSL 路径错误、提权模式混乱、sandbox helper 缺失、MSIX 包无法启动——多版本并存导致体验分裂。
- **会话管理不一致**：归档删除后 UI 不同步、`/goal` 建立的会话从恢复列表消失、远程会话文件查看失败等，基础功能的可靠性仍不牢固。
- **Linux 桌面呼声持续高涨**：583 👍 和 113 条评论表明这不是小众需求，而是跨平台开发者生态的重要卡点。

---

*本期日报基于 GitHub openai/codex 公开社区数据生成，数据采集时间截至 2026-06-16。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，没问题。作为专注于AI开发工具的技术分析师，我已根据您提供的GitHub数据，为您整理出2026年6月16日的Gemini CLI社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-06-16

## 今日速览

今日社区动态主要集中在**安全加固**和**Agent稳定性**两个核心方向。多个修复SSRF（服务端请求伪造）漏洞的PR进入待审或合并状态，同时关于Sub-agent挂起、日志错误报告等问题持续引发开发者讨论，反映出社区对生产环境可靠性的高度关注。此外，依赖项的批量更新也表明项目正在积极维护技术栈的健康度。

## 社区热点 Issues

1.  **Agent通用性挂起问题** (`#21409`)
    - **重要性**: 社区高度关注（👍 8），一个P1级别的严重Bug。`gemini-cli`在将任务委派给通用Agent时，会导致进程无限期挂起（最长等待1小时），严重影响任务完成。
    - **链接**: `google-gemini/gemini-cli Issue #21409`

2.  **Sub-agent达到最大轮次后误报成功** (`#22323`)
    - **重要性**: 这是一个关键的行为逻辑错误。`codebase_investigator`子代理在达到执行轮次上限（MAX_TURNS）后，本应报告失败，但却错误地报告为“成功”，从而隐藏了任务被中断的真相，给用户造成困惑。
    - **链接**: `google-gemini/gemini-cli Issue #22323`

3.  **AST感知的文件读取、搜索和映射影响评估** (`#22745`)
    - **重要性**: 这是一个EPIC（大型功能跟踪问题），旨在探索引入“AST感知”工具是否能提升代码理解和操作的精确度。这代表了Agent智能化发展的一个重要方向，即让Agent像资深开发者一样理解代码结构。
    - **链接**: `google-gemini/gemini-cli Issue #22745`

4.  **Shell命令执行后卡住** (`#25166`)
    - **重要性**: P1级别Bug，影响核心工作流。Gemini执行完简单的Shell命令后，状态仍然显示“等待输入”，导致流程无法继续。社区报告频率高，是影响用户体验的痛点。
    - **链接**: `google-gemini/gemini-cli Issue #25166`

5.  **Gemini不会主动使用技能和子代理** (`#21968`)
    - **重要性**: 虽然这是一个P2问题，但它关乎AI的可控性和深度使用。用户反馈，即使配置了高质量的自定义技能（如Gradle、Git），Gemini也不会主动调用，必须用户明确指令。这限制了Gemini CLI作为“智能助手”的潜力。
    - **链接**: `google-gemini/gemini-cli Issue #21968`

6.  **Automemory低信号会话无限重试** (`#26522`)
    - **重要性**: 这是一个资源浪费和效率问题。Auto Memory功能在遇到“低价值”会话（如简单的问候）时会不断重试，而不是跳过。这会导致无谓的API调用和Token消耗。
    - **链接**: `google-gemini/gemini-cli Issue #26522`

7.  **Browser Agent在Wayland下失败** (`#21983`)
    - **重要性**: 兼容性问题。Browser Agent在Wayland显示服务器环境下运行失败，限制了在特定Linux发行版上的可用性。对于依赖浏览器自动化的开发者来说是个明显的障碍。
    - **链接**: `google-gemini/gemini-cli Issue #21983`

8.  **Agent应阻止/劝阻破坏性行为** (`#22672`)
    - **重要性**: 这是一个关于AI安全与可控性的重要讨论。社区期望Agent在处理复杂操作（如Git强制推送到数据库修改）时，能优先选择安全路径，并在执行危险操作前对用户进行警告。
    - **链接**: `google-gemini/gemini-cli Issue #22672`

9.  **超过128个工具时的400错误** (`#24246`)
    - **重要性**: 当用户配置的工具数量超过128个时，Gemini CLI会直接返回400错误。这表明Agent管理大规模工具集的能力有限，需要更智能的工具调度和选择机制。
    - **链接**: `google-gemini/gemini-cli Issue #24246`

10. **Sub-agent配置覆盖被忽略** (`#22267`)
    - **重要性**: 配置不生效的Bug。用户通过`settings.json`为Browser Agent设置的参数（如`maxTurns`）被完全忽略，说明Agent配置的加载和优先级逻辑存在问题，破坏了用户的个性化控制能力。
    - **链接**: `google-gemini/gemini-cli Issue #22267`

## 重要 PR 进展

1.  **支持GDC Air-Gapped服务身份** (`#27956`)
    - **内容**: 新增功能。通过更新后的谷歌认证库，为GDCH（Google Distributed Cloud Hosted）离线环境下的Service Identity Token交换提供支持，拓展了在私有化部署场景的适用性。
    - **链接**: `google-gemini/gemini-cli PR #27956`

2.  **修复Tmux中的背景色误检测** (`#27572`) 【已关闭】
    - **内容**: Bug修复。解决了在Tmux（尤其是通过Mosh连接）中，Gemini CLI错误地将终端背景色检测为白色的问题，避免了因主题切换不当导致的兼容性警告。
    - **链接**: `google-gemini/gemini-cli PR #27572`

3.  **添加平台感知的Shell指导** (`#27603`) 【已关闭】
    - **内容**: Bug修复/功能增强。修正了在非Unix平台上（如Windows）仍显示Unix命令示例的问题。通过增加平台感知的逻辑，为Windows用户提供正确的Shell操作指引（如`dir`而非`ls`）。
    - **链接**: `google-gemini/gemini-cli PR #27603`

4.  **阻止私有OAuth元数据URL** (`#27626`) 【已关闭】
    - **内容**: 安全修复。在MCP OAuth发现流程中增加了SSRF（服务端请求伪造）防护，避免Gemini CLI被恶意或配置错误的MCP服务器引导去访问内部或危险的URL。
    - **链接**: `google-gemini/gemini-cli PR #27626`

5.  **合并MCP服务器列表以防绕过** (`#27605`) 【已关闭】
    - **内容**: 功能修复。修复了MCP允许/阻断列表的绕过漏洞。通过合并不同作用域（用户级、项目级）的配置，确保安全工作区的设置不会被低优先级的配置所覆盖。
    - **链接**: `google-gemini/gemini-cli PR #27605`

6.  **通过DNS解析防止SSRF绕过** (`#27744` 及 `#27739`)
    - **内容**: 安全加固。一组关键的SSRF漏洞修复。之前的`isBlockedHost`检查无法阻止诸如`127.0.0.1.nip.io`这类域名指向内网IP的绕过方式。这两个PR通过在SSRF防护前进行DNS解析，有效地阻断了对内部私有地址的访问。
    - **链接**: `google-gemini/gemini-cli PR #27744` `google-gemini/gemini-cli PR #27739`

7.  **为`@`引用文件修复路径解析** (`#27943`)
    - **内容**: Bug修复。修复了当模型尝试读写通过`@`符号引用的文件时，报错“文件未找到”的问题。这是一个关键的文件系统交互bug，直接影响Agent操作文件的准确性。
    - **链接**: `google-gemini/gemini-cli PR #27943`

8.  **修复待处理工具和信任覆盖逻辑** (`#27854`) 【已关闭】
    - **内容**: Bug修复。修复了多个稳定性问题：当等待用户批准工具调用时，Agent状态不应继续前进；文件写入操作应顺序执行以避免竞态条件；修复了一个配置Bug。
    - **链接**: `google-gemini/gemini-cli PR #27854`

9.  **将`coreTools`配置迁移至`tools.core`** (`#27947`)
    - **内容**: Code Refactoring。将废弃的`coreTools`配置属性迁移到新的`tools.core`嵌套结构中。这是一个基础性工作，确保代码库内部配置模式的统一。
    - **链接**: `google-gemini/gemini-cli PR #27947`

10. **固定依赖版本并强制执行14天更新冷却期** (`#27948`)
    - **内容**: 工程实践。一个旨在提高构建稳定性和可复现性的PR。通过移除语义化版本范围（`^`、`~`），将依赖锁定到精确版本，并设置自动化依赖更新的冷却期，减少意外变更带来的风险。
    - **链接**: `google-gemini/gemini-cli PR #27948`

## 功能需求趋势

从社区的Issue和讨论中，可以提炼出以下几个最受关注的功能方向：

1.  **Agent的智能性与自主性**：社区不满足于Agent仅仅执行简单命令。热门讨论如“AST感知的代码操作”（`#22745`）和“主动使用技能”（`#21968`），表明开发者希望Agent能像资深同事一样，**理解代码结构和上下文，并主动应用最合适的工具**。
2.  **安全加固**：安全是当前最热的主题。多项PR（`#27626`， `#27744`， `#27739`）集中修复SSRF漏洞，同时Issue讨论也在关注“防止破坏性行为”（`#22672`）和“凭证隐私”（`#26525`）。这表明随着Agent权限和能力增强，**安全防护成为社区最核心的关切**。
3.  **自动化记忆系统的可靠性**：Auto Memory功能（`#26522`， `#26523`， `#26516`）是关注的焦点，但这个模块仍不成熟。社区要求它能更智能地**过滤低价值信息、优雅地处理错误、并提高其提取内容的准确性**，以免产生噪声或误导。
4.  **工具生态的扩展与管理**：当Agent接管的工具超过一定数量后（`#24246`），其性能和管理问题凸显。社区需要一个更健壮的**工具注册、调度和冲突解决机制**，以支持复杂的、插件式的工具生态。

## 开发者关注点

从开发者的反馈和Bug报告中，可以看出几个核心痛点或高频需求：

1.  **稳定性与可预测性**：这是最普遍的痛点。无论是Agent挂起（`#21409`）、错误报告（`#22323`）还是命令卡住（`#25166`），开发者普遍**无法信赖Agent能够稳定、可预测地完成任务**，这严重影响了将其应用于实际工作流的信心。
2.  **配置生效与优先级逻辑**：多个报告（`#22267`， `#20079`， `#27943`）指出，配置被忽略、不生效或逻辑混乱。开发者期望Gemini CLI的**配置系统能清晰、严格且可预测**，特别是当存在不同作用域（用户级、项目级）配置时，其优先级逻辑应该明确。
3.  **跨平台与环境兼容性**：Wayland（`#21983`）和Tmux（`#27572`）环境下的问题，以及Windows命令的适配问题（`#27603`），反映出在**异构的开发环境下，Gemini CLI的兼容性和适应性仍有待提升**。
4.  **避免“脏活”和“副作用”**：开发者对Agent在文件系统中乱写临时脚本（`#23571`）以及执行危险命令（`#22672`）感到不满。社区渴望一个**更“干净”和“保守”的Agent**，能最小化对工作区的污染和执行不可逆的操作。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-06-16 社区动态日报。

---

# GitHub Copilot CLI 社区动态日报 | 2026-06-16

---

## 1. 今日速览

昨日，Copilot CLI 密集发布了 v1.0.63 主线版及 v1.0.63-0 实验版，修复了图像附件的易用性问题，并增强了 MCP 服务器的灵活性。然而，社区近期被 v1.0.60 以来的系列回归问题困扰，包括插件 Hook 断裂、MCP 循环崩溃及跨平台乱码。权限精细化控制和多模型支持依旧是社区呼声最高的演进方向。

---

## 2. 版本发布

### v1.0.63 (2026-06-15)
- **改进**：被屏蔽的图像附件现在会提供清晰指引——建议启用 Vision 预览功能、切换到支持 Vision 的模型，或换用其他图片，不再显示令人困惑的错误。
- **优化**：`--help` 输出中的选项已改为按字母顺序排序。
- [发布链接](github/copilot-cli/releases/tag/v1.0.63)

### v1.0.63-0 (2026-06-15)
- **新增**：在 `/diff` 模式下按 `w` 键可切换忽略空白变更。
- **新增**：MCP 服务器配置新增 `deferTools` 选项，确保即使启用了工具搜索，特定服务器的工具也始终可用。
- **改进**：显著提升了 OpenAI、Anthropic 和 Azure OpenAI 请求的稳定性。
- **实验性**：`/rewind` 命令持续迭代（具体变更因篇幅限制未完全展示）。
- [发布链接](github/copilot-cli/releases/tag/v1.0.63-0)

---

## 3. 社区热点 Issues (Top 10)

以下是从过去 24 小时更新的 44 条 Issue 中精选的 10 个最值得关注的问题：

1.  **[#953] 权限过度请求 (Over excessive permissions Request)**
    - **热度**：👍 3 | 💬 7
    - **摘要**：用户反馈当前认证过程要求对整个账户的读写权限，建议能限制 AI 只访问特定的仓库和区域。这是企业安全治理的核心需求，长期位居热门榜单。
    - [链接](github/copilot-cli/issue/953)

2.  **[#3727] [回归] v1.0.60 中 userPromptSubmitted Hook 的 additionalContext 不再注入 Plannner**
    - **热度**：💬 4
    - **摘要**：插件开发者报告严重回归。在 v1.0.59 中工作正常的 Hook 机制，在 v1.0.60 中完全失效，导致依赖上下文注入的插件全部瘫痪，影响面极广。至今仍处于开放状态。
    - [链接](github/copilot-cli/issue/3727)

3.  **[#3282] 请求为 Copilot CLI 增加多 BYOK 模型能力**
    - **热度**：👍 8 | 💬 3
    - **摘要**：社区高赞请求。当前仅支持单个 BYOK 模型且需环境变量设置，无法在 TUI 界面中切换。用户强烈希望在会话内动态切换模型，以提升灵活性和开发效率。
    - [链接](github/copilot-cli/issue/3282)

4.  **[#3781] [已关闭] 在非多模态模型中粘贴图片导致会话进入不可恢复的 400 错误**
    - **热度**：💬 3
    - **摘要**：Bug 直接，破坏性强。一旦在非 Vision 模型会话中粘贴图片，整个对话 log 就会永久损坏，唯一的修复方式是手动编辑 JSONL 文件。新版本 v1.0.63 的发布正是针对此问题的优化。
    - [链接](github/copilot-cli/issue/3781)

5.  **[#3756] [已关闭] 企业 Copilot 策略禁用第三方 MCP 服务器**
    - **热度**：💬 3
    - **摘要**：企业用户常见的拦路虎。被策略限制后完全无法使用第三方 MCP Server，且缺乏绕过方案，直接中断了企业内部的工具链整合（与 #1707 高度关联）。
    - [链接](github/copilot-cli/issue/3756)

6.  **[#2966] 请求内置管理多个并发 CLI 会话的工具**
    - **热度**：💬 3 | 👍 1
    - **摘要**：高级用户的痛点。随着 `--yolo/--autopilot` 模式普及，用户同时管理数十个跨仓库会话的能力捉襟见肘，迫切期望官方的多会话管理工具。
    - [链接](github/copilot-cli/issue/2966)

7.  **[#3776 / #3813] UTF-8 文本复制粘贴后乱码 (Mojibake)**
    - **热度**：💬 2-3
    - **摘要**：跨平台基础体验问题。从 WSL、iTerm2 或 VS Code 终端复制输出（含中文、东欧字符）粘贴到 Windows 应用变成乱码，全球化开发团队影响严重。
    - [#3776 链接](github/copilot-cli/issue/3776) | [#3813 链接](github/copilot-cli/issue/3813)

8.  **[#3784] [已关闭] Linux ARM64 平台 Tokio Reactor Panic**
    - **热度**：💬 2
    - **摘要**：致命级系统崩溃。在 ARM64 机器上发送第一条消息后进程直接退出（代码 134）。日志显示为 WebSocket 连接阶段崩溃，严重阻碍 Apple Silicon 上的 Linux 开发用户。
    - [链接](github/copilot-cli/issue/3784)

9.  **[#3769] [已关闭] Copilot CLI 终端输出线程混乱**
    - **热度**：👍 3 | 💬 2
    - **摘要**：渲染 Bug。AI 输出内容在终端中被打乱，直到响应完全结束才恢复正常，直接影响用户体验和可读性，尤其是使用 Agency 模式时。
    - [链接](github/copilot-cli/issue/3769)

10. **[#3814] 请求持续失败但 AIC 消耗持续增加**
    - **热度**：💬 0 | 👍 1 *(新发，热度正起)*
    - **摘要**：成本信任危机。用户反馈在连续遇到“服务器错误”和“重试”的情况下，AIC（AI 额度）消耗依旧不断攀升。这是用户最敏感的计费相关问题。
    - [链接](github/copilot-cli/issue/3814)

---

## 4. 重要 PR 进展

> 说明：根据数据范围，过去 24 小时内仅更新 1 条 PR，无实质性功能或修复代码入库，核心代码库提交活动相对平淡。
>
> - **#3817 [待审核] `kCreate "#"`**
>   - 摘要：标题与描述无实际意义（测试垃圾内容），未包含任何代码变更或有效讨论。建议维护者及时标记清理。
>   - [链接](github/copilot-cli/pull/3817)

---

## 5. 功能需求趋势

近期 Issue 反映出社区对以下五大功能方向的高度关注：

1.  **模型的自由化与配置下沉**：高频词汇为**多 BYOK 模型支持** (#3282) 及**自定义 HTTP 请求头** (#3399)。用户越来越不满足于绑定的模型，希望接入自有的 LLM 网关或定制化端点。
2.  **高级会话与知识管理**：用户不再满足于单一会话。**多会话原生管理** (#2966)、**会话内容深度检索** (#3807) 以及 **`/chronicle` 功能的演进** (#3816) 说明用户渴望将 AI 对话转化为可检索、可追溯的知识库。
3.  **MCP 生态的深度与治理**：除了基础的连接性，社区开始关注 **MCP 的权限治理** (#3756)、**工具继承** (#3812) 以及 **服务器的弹性** (#3782)。
4.  **精细化权限与安全**：以 #953 为代表，用户对“最小权限”原则的诉求从软件安全角度出发，要求能够细粒度控制 AI Agent 的行为边界。
5.  **跨平台体验一致性**：Unix 与 Windows 之间、不同终端模拟器之间的渲染和编码差异正在成为新的摩擦点，影响全球团队协作。

---

## 6. 开发者关注点

1.  **版本发行质量之痛**：v1.0.60 至 v1.0.62 的连续回归（Hook 断裂、MCP 循环、ARM64 Panic）动摇了开发者对“快速迭代”的信心。社区普遍期待更严格的集成测试，特别是对插件接口和 MCP 协议的回归扫描。
2.  **计费透明度与容错**：失败请求依然计费 (#3814) 被视作开发工具的“红线问题”。开发者要求“请求不成功不计费”或“失败重试不应重复计费”的明确承诺。
3.  **企业级卡点**：权限过度、模型无法自定义、第三方 MCP 策略屏蔽——这些是目前 Copilot CLI 在大型企业普及的主要阻力。开发者希望看到从“个人神器”到“企业级平台”的蜕变。
4.  **容灾与可恢复性弱**：会话因错误数据（超大附件 #3767、错误图片格式 #3781）永久性损坏，需要用户手动编辑底层 JSONL 文件，这在生产环境中是不可接受的。自动检测恢复或降级机制是刚需。
5.  **开发者体验细节**：Windows 路径转义缺失 (#3815)、字符编码不一致 (#3776)、Linux ARM64 的稳定性，这些看似“小事”的基础体验正在成为拉低 NPS 的关键因素。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报  
**日期：2026-06-16**  
**数据来源：**[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

### 1. 今日速览

过去24小时内，社区提交了2个关键Bug修复PR，分别针对`--continue`会话恢复失败和Hook接收空prompt的问题；同时新出现1个网络代理兼容性Issue，反映了用户在被墙环境下的使用障碍。整体来看，**会话管理和网络适配**是当前社区最关注的稳定性议题。

### 2. 版本发布

无新版本发布。

### 3. 社区热点 Issues

过去24小时内共有 **4 个 Issue 更新**（均为Bug），详情如下：

#### #2402 – compaction.failed 错误：请求被判定为高风险并拒绝  
- **描述：** 使用 Kimi-k2.6 模型时，操作被中断并报错 `Error: [compaction.failed] APIStatusError: 400 The request was rejected because it was considered high risk`，出现在 Windows 环境下。  
- **重要性：** 影响关键任务执行（compaction取消），可能涉及API调用频率或内容安全策略，需要官方明确风险判定机制。  
- **社区反应：** 有2条评论，暂无官方回应，点赞0。  
  [https://github.com/MoonshotAI/kimi-cli/issues/2402](https://github.com/MoonshotAI/kimi-cli/issues/2402)  

#### #2303 – UserPromptSubmit Hook 在 Shell UI 输入时收到空 prompt  
- **描述：** 当用户在交互式Shell中以纯文本输入时，`UserPromptSubmit` hook 始终接收到 `"prompt": ""`，导致基于正则的prompt hook无法匹配。影响所有使用自定义Hook的用户。  
- **重要性：** 属于Hook系统的功能性Bug，破坏扩展能力。版本 v1.44.0，macOS。  
- **社区反应：** 1条评论，已有对应PR #2454 修复。点赞0。  
  [https://github.com/MoonshotAI/kimi-cli/issues/2303](https://github.com/MoonshotAI/kimi-cli/issues/2303)  

#### #2222 – `kimi --continue` 报错 “No previous session found”  
- **描述：** 同一目录下直接运行 `kimi` 能显示历史记录，但使用 `--continue` 标志却提示无历史会话。版本 v1.41.0，Windows。  
- **重要性：** 核心工作流阻断，影响用户续接对话的效率。与会话管理逻辑直接相关。  
- **社区反应：** 1条评论，已有对应PR #2453 修复。点赞0。  
  [https://github.com/MoonshotAI/kimi-cli/issues/2222](https://github.com/MoonshotAI/kimi-cli/issues/2222)  

#### #2455 – FetchURL 未读取系统代理，被墙环境无法访问外网  
- **描述：** `FetchURL` 功能忽略系统代理设置，导致在受限网络环境中无法正常获取外部资源，而 Shell 和 curl 均正常。版本 v1.43.0，Linux WSL2。  
- **重要性：** 新提交的严重性问题，直接剥夺用户在代理/内网环境下的网络能力，影响面广。尚无评论，但预计会成为高频需求。  
- **社区反应：** 0条评论，官方尚未回应。  
  [https://github.com/MoonshotAI/kimi-cli/issues/2455](https://github.com/MoonshotAI/kimi-cli/issues/2455)  

---

### 4. 重要 PR 进展

过去24小时内共 **2 个 PR 更新**（均为修正性PR），目前均处于 Open 状态：

#### #2454 – fix(hooks): 从结构化输入中正确传递 prompt 文本到 UserPromptSubmit  
- **修复内容：** 解决了 #2303 中 Hook 收到空 prompt 的问题。在 `KimiSoul._turn` 中，从输入数据中正确提取 `text_input` 作为 hook 的 prompt，而非空字符串。  
- **影响：** 恢复所有基于 Hook 的交互增强功能（如关键字匹配、输入预处理）。  
- **作者：** logicwu0  
  [https://github.com/MoonshotAI/kimi-cli/pull/2454](https://github.com/MoonshotAI/kimi-cli/pull/2454)  

#### #2453 – fix(session): 当 last_session_id 缺失时恢复最新会话  
- **修复内容：** 针对 #2222 ，改进 `Session.continue_` 逻辑：当未找到 `last_session_id` 时，依据 `work_dir` 从数据库中检索最新会话，而非直接返回“无会话”。  
- **影响：** 修复 `--continue` 命令在历史存在时的错误提示，提升 CLI 使用流畅度。  
- **作者：** logicwu0  
  [https://github.com/MoonshotAI/kimi-cli/pull/2453](https://github.com/MoonshotAI/kimi-cli/pull/2453)  

---

### 5. 功能需求趋势

从近期 Issues 和 PR 中可提炼出以下社区关注的功能方向：

- **网络兼容性增强**：系统代理读取、被墙环境下的访问能力（#2455）是新增痛点，反映出用户对企业内网/受限网络使用的需求日益增加。
- **会话管理健壮化**： `--continue` 失败、历史记录丢失等问题的集中出现，表明用户对 CLI 的工作流连续性有较高期望。
- **Hook 系统稳定性**：空 prompt 问题暴露出 Hook 与 Shell UI 的数据流割裂，社区期待更完整的扩展支撑。
- **API 风险控制透明化**： compaction failed 等请求被拒的问题提示用户需要知晓模型安全限制的详情，可能希望增加配置或日志提示。

### 6. 开发者关注点

- **跨平台体验一致**：问题集中在 Windows 与 Linux WSL2 环境（#2402、#2222、#2455），macOS 也有涉及（#2303），表明用户期望多平台稳定工作。
- **高频痛点：会话恢复**： #2222 与 PR #2453 体现了用户对快速接入历史会话的强烈依赖，“No previous session” 这类阻断性错误会严重影响信任度。
- **网络障碍**：无法读取系统代理（#2455）是当前最热门的新反馈，猜测随后会有更多用户表达类似需求。
- **零门槛扩展**：Hook 系统是 CLI 高级功能的关键接口，其中“传入数据与 UI 行为不一致”属于影响开发效率的低级错误，修复后预计会提升生态开发者的满意度。

---

*本日报基于 MoonshotAI/kimi-cli 仓库 2026-06-16 的数据生成，仅反映当日更新动态。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-06-16

## 今日速览

社区围绕内存问题排查、MCP 标准跟进和原生会话目标（`/goal`）功能展开了热烈讨论；多项涉及 Windows 兼容性、MCP 能力增强的 PR 提交，其中 PowerShell 编码修复与自动压缩循环修复是关键进展。同时，付费订阅激活失败的问题持续引发用户不满，商业服务稳定性受到关注。

---

## 社区热点 Issues

### 1. [#20695 Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)
- **评论 97 · 👍 65**
- 内存问题的集中讨论帖，作者鼓励用户提供堆快照而非 LLM 建议（“PLEASE DO NOT RUN YOUR LLM”）。社区协作氛围浓厚，是当前最活跃的 issue 之一。

### 2. [#2242 沙箱 Agent 能力请求](https://github.com/anomalyco/opencode/issues/2242)
- **评论 69 · 👍 53**
- 用户希望限制 Agent 仅可访问当前目录，类似 Gemini CLI 的 seatbelt 功能。该需求跨越近一年，今天仍有更新，说明社区对安全隔离的刚性需求。

### 3. [#27167 原生会话目标 /goal](https://github.com/anomalyco/opencode/issues/27167)
- **评论 49 · 👍 84**
- 提议增加持久会话目标与生命周期管理，以 `/goal` 命令实现。赞数最高之一，说明开发者在复杂场景下对会话上下文控制有强烈诉求。

### 4. [#27906 v1.15.1+ 破坏 Bun 安装](https://github.com/anomalyco/opencode/issues/27906)
- **评论 18 · 👍 13**
- 新版本要求 postinstall 脚本，而 Bun 默认禁止全局包执行此类脚本，导致安装失败。社区期待修复或提供配置手段绕过。

### 5. [#5374 显示 tokens/second](https://github.com/anomalyco/opencode/issues/5374)
- **评论 17 · 👍 81**
- 请求展示当前及平均 token 生成速率，便于对比不同提供商性能。获得 81 个赞，反映用户对成本与效率可见性的重视。

### 6. [#28567 完整 MCP 客户端能力](https://github.com/anomalyco/opencode/issues/28567)
- **评论 14 · 👍 22**
- 指出 OpenCode 的 MCP 客户端功能落后于最新标准，要求补齐。今日有更新，与 MCP 生态演进密切相关。

### 7. [#28957 “Upstream idle timeout exceeded”](https://github.com/anomalyco/opencode/issues/28957)
- **评论 14 · 👍 0**
- 用户在 “writing-plans” 技能中频繁遇到上游空闲超时，模型响应中断。虽然未获得点赞，但评论数高，属于影响使用的隐蔽 Bug。

### 8. [#6930 Anthropic OAuth 违反 ToS 导致封号 (已关闭)](https://github.com/anomalyco/opencode/issues/6930)
- **评论 22 · 👍 14**
- 用户因通过 OpenCode 使用 Anthropic OAuth 被判定违规而导致账号封禁。尽管已关闭，仍引发对 OAuth 合规性和使用边界的热议。

### 9. [#32420 付费 Go 订阅未激活](https://github.com/anomalyco/opencode/issues/32420)
- **评论 3 · 👍 0**
- 用户付款后订阅未生效，客服无回复。摘要称“many identical reports”，说明此非孤例，影响商业信任度。

### 10. [#21345 从 bash 工具描述移除 git/PR 指令以节省 Token](https://github.com/anomalyco/opencode/issues/21345)
- **评论 3 · 👍 9**
- 通过性能分析发现 git/PR 说明每条请求消耗约 1.7K tokens，建议移出以降低上下文开销。该优化思路获得不少认同。

---

## 重要 PR 进展

### 1. [#31985 fix(shell): 使用 PowerShell EncodedCommand 确保 Windows UTF-8 输出](https://github.com/anomalyco/opencode/pull/31985)
- 采用 PowerShell 编码命令替代原始输出读取，解决 Windows 下乱码问题。关闭 5 个相关 issue，是跨平台兼容性的关键修复。

### 2. [#32499 fix(opencode): 允许清除会话归档时间](https://github.com/anomalyco/opencode/pull/32499)
- 为用户提供取消会话归档的能力，回应社区关于灵活管理会话生命周期的需求。

### 3. [#29150 fix(opencode): 自动压缩循环无进展时跳出](https://github.com/anomalyco/opencode/pull/29150)
- 修复当模型上下文限制小于实际值时，自动压缩陷入无限循环的问题。提升长时间会话的稳定性。

### 4. [#32494 fix(opencode): 在 GitHub 上下文中包含 PR 身份](https://github.com/anomalyco/opencode/pull/32494)
- 为 `opencode github run` 添加 PR 号和 URL，使 PR 评论运行可识别身份，利于 CI 协作和追溯。

### 5. [#31645 feat(cli): 升级命令添加进度反馈](https://github.com/anomalyco/opencode/pull/31645)
- 为 `opencode upgrade` 增加实时下载进度，解决升级过程中用户误以为卡顿的体验问题。

### 6. [#32490 feat(mcp): 将服务器指令追加到上下文](https://github.com/anomalyco/opencode/pull/32490)
- 在会话上下文中注入 MCP 服务器的 `InitializeResult.instructions`，增强 MCP 集成能力。是全面 MCP 修订的一部分。

### 7. [#31644 fix(acp): 注册 compact 和 summarize 命令到帮助列表](https://github.com/anomalyco/opencode/pull/31644)
- 修复 `/compact` 和 `/summarize` 命令未出现在自动补全和 `/help` 中的问题，提高功能可发现性。

### 8. [#32489 fix(opencode): 清理 MCP 工具 Schema 以兼容 OpenAI](https://github.com/anomalyco/opencode/pull/32489)
- 清理 MCP 服务器输出的 JSON Schema 中 OpenAI 不支持的字段，避免工具调用失败。提升 MCP 互操作性。

### 9. [#32487 feat: 可配置成本显示货币](https://github.com/anomalyco/opencode/pull/32487)
- 新增 `display.currency` 等配置项，支持按美元、人民币等不同货币显示使用成本，满足国际化需求。

### 10. [#32479 fix(tui): 支持 Windows 下通过 FileDrop 格式粘贴图片](https://github.com/anomalyco/opencode/pull/32479)
- 修复 Windows 中 Ctrl+Shift+V 无法粘贴截图的问题，解析 FileDrop 格式实现图片粘贴，提升 TUI 用户体验。

---

## 功能需求趋势

从近期的 issues 中可提炼出以下社区最关注的方向：

- **会话生命周期管理**：用户希望拥有持久的会话目标（`/goal`）、灵活的归档控制（清除归档时间）以及明确的压缩/摘要命令（`/compact`、`/summarize`）。
- **MCP 标准补全与互操作性**：要求全面实现 MCP 最新规范（#28567），包括服务器指令注入（#32490）、Schema 清理（#32489）与资源管理。
- **性能监控与资源优化**：对 token 速率显示（#5374）、内存泄漏排查（#20695）、请求超时（#28957）以及 Prompt token 节省（#21345）有迫切需求，用户希望透明化成本与效率。
- **安全与权限控制**：持续要求沙箱隔离（#2242）、文件/命令访问限制（#16914），以及 OAuth 使用的合规指引（#6930）。
- **跨平台兼容与本地模型支持**：Windows 字符编码、CJK 输出、图片粘贴、WSL 工作区选择，以及 Ollama、Moonshot 等本地/新模型提供商集成持续受到关注。

---

## 开发者关注点

综合反馈中的痛点与高频需求：

- **内存泄漏/高占用**：多个用户报告内存问题，官方开辟集中排查贴，但尚无最终解决方案。
- **付费订阅激活失败**：付款后显示未订阅，客服无响应，多个用户反映同一问题（#32420、#32466、#32482），影响商业信誉。
- **MCP 功能不完整**：落后于 MCP 标准，导致 IDEA 等第三方工具无法正常使用（#32491）。
- **Agent 构建质量差异**：部分用户认为 “build agent” 效果远不如 “subagents”（#32484）。
- **上游超时中断**：模型服务端空闲超时导致任务中断，缺乏重试或超时配置（#28957、#31456）。
- **破坏性更新**：v1.15.1 强制 postinstall 导致 Bun 用户无法安装（#27906）。
- **反病毒误报**：Windows 版本被 Kaspersky 报毒，影响 CLI 使用信任（#32350）。
- **命令阻塞与进程残留**：Playwright 命令在 OpenCode 中无法退出（#22767），Gradle 构建后终端不回收（#22154）。
- **桌面端渲染卡死**：Markdown 解析同步阻塞 UI 线程，启动后约 60 秒无响应（#32452）。

以上需求与痛点反映了社区对 **稳定性、安全性、标准兼容性以及商业服务可靠性** 的强烈期待。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报（2026-06-16）

---

## 今日速览

pi 发布 v0.79.4，新增首次自动主题选择（暗/亮），以及独立二进制安全改进背景下的 SHA256SUMS 倡议。社区最热话题仍是 **openai-codex/gpt-5.5 连接可靠性问题**（Issue #4945，57 条评论），严重影响日常 TUI 使用。同时，关于 Amazon Bedrock Mantle 和新版 ZAI China 提供商的 PR 与 Issue 持续推进，显示出社区对更多云服务商接入的迫切需求。

---

## 版本发布

### v0.79.4
- **自动主题选择**：pi 在首次运行时会检测终端背景色，默认使用 `dark` 或 `light` 主题。
- **Standalone 构建**（描述截断，推测为独立二进制的安全加固相关，配合 Issue #5739 的 SHA256SUMS 添加说明）。
> 链接：v0.79.4 Release

---

## 社区热点 Issues

### 1. [#4945 – openai-codex Connection Reliability Issues](https://github.com/earendil-works/pi/issues/4945)  
**状态**：OPEN | 评论 57 | 👍 30  
**摘要**：使用 `openai-codex`/`gpt-5.5` 时，交互式 TUI 随机卡在“Working…”状态，无流输出、无工具调用、无错误提示，只能按 Escape 中断。近几日反复出现，严重影响开发工作流。  
**重要性**：最热门 Bug，直接影响核心使用体验，社区寻求根因。

### 2. [#5103 – Windows git-bash 检测失败](https://github.com/earendil-works/pi/issues/5103)  
**状态**：OPEN | 评论 21  
**摘要**：从 GitHub Release 下载的 `pi-windows-x64.zip` 无法正确识别 PATH 中的 Git Bash，导致内置 bash 工具报告找不到 shell。  
**重要性**：Windows 用户首要堡垒，阻止在 Windows 上正常使用 bash 工具。

### 3. [#4877 – Session 文件夹碰撞](https://github.com/earendil-works/pi/issues/4877)  
**状态**：OPEN | 评论 15 | 👍 2  
**摘要**：会话存储路径采用路径字符串拼接，不同路径可能映射到同一文件夹（例如 `/a/b/c/d` 与 `/a-b/c-d`），导致会话混淆。  
**重要性**：设计缺陷，长期可能引发数据覆盖或恢复错误。

### 4. [#5363 – 添加 Amazon Bedrock Mantle 提供商](https://github.com/earendil-works/pi/issues/5363)  
**状态**：OPEN | 评论 13 | 👍 3  
**摘要**：请求新增 `amazon-bedrock-mantle` 提供商，其使用 OpenAI 兼容 API，与现有 Bedrock Converse API 不兼容。  
**重要性**：云厂商新服务支持，已有关联 PR #5509（Open），社区关注度高。

### 5. [#5653 – Shrinkwrap 包重复问题](https://github.com/earendil-works/pi/issues/5653)  
**状态**：OPEN | 评论 10  
**摘要**：同时安装 `pi-ai` 和 `pi-coding-agent` 时，因模块级 `Map` 对象导致两份相同代码存在磁盘上，API 注册中心相互隔离。  
**重要性**：直接影响包管理和扩展系统的稳定性，涉及代码重复和功能异常。

### 6. [#3214 – 工具参数 $schema 导致 400 错误](https://github.com/earendil-works/pi/issues/3214)  
**状态**：CLOSED | 评论 10  
**摘要**：使用 antigravity/google cloud code assist 提供商时，部分 MCP 工具包含 `$schema` 字段，导致 API 拒绝请求抛 400。  
**重要性**：已闭环但极具参考价值，揭示 MCP 工具与严格 API 的兼容性陷阱，影响后续提供商适配。

### 7. [#5702 – prompt_cache_retention 被不支持提供商拒绝](https://github.com/earendil-works/pi/issues/5702)  
**状态**：CLOSED | 评论 8  
**摘要**：`prompt_cache_retention` 参数被发给不支持的提供商（opencode/zen），同时指出模型注册构建系统的可维护性问题。  
**重要性**：小型 Bug 引出发维护性讨论，涉及模型构建配置与提供商策略分离。

### 8. [#5696 – TUI 右下角模型名称不刷新](https://github.com/earendil-works/pi/issues/5696)  
**状态**：CLOSED | 评论 8  
**摘要**：`CTRL+P` 切换模型时，状态栏模型名常不更新；按一次无反应，按两次才跳到+2 位置。  
**重要性**：UI 反馈错误，影响用户切换模型时的认知，社区已确认并修复。

### 9. [#5687 – pi list/update 因 MCP 服务器挂起](https://github.com/earendil-works/pi/issues/5687)  
**状态**：CLOSED | 评论 7  
**摘要**：当扩展运行长寿命 MCP 服务器时，`pi list`、`pi update` 等命令完成任务后不退出，直到 Ctrl-C。  
**重要性**：暴露扩展生命周期管理缺陷，影响包管理命令的可用性。

### 10. [#5728 – 支持 provider-specific 配置 in auth.json](https://github.com/earendil-works/pi/issues/5728)  
**状态**：OPEN | 评论 6  
**摘要**：部分提供商（如 cloudflare-ai-gateway）需要 `accountId` 等额外参数，目前只能通过环境变量传递。希望 `auth.json` 支持承载此类配置。  
**重要性**：解决多提供商配置分散问题，提升用户体验和可移植性。

---

## 重要 PR 进展

### 1. [#5789 – fix(tui): restore cursorUp line-start jump before history browsing](https://github.com/earendil-works/pi/pull/5789)  
**状态**：OPEN  
**摘要**：修复之前优化导致光标上移时总是进入历史浏览的问题，恢复在第一行按↑跳转到行首的行为。  
**价值**：修正编辑体验回归，保持操作一致性。

### 2. [#5675 – fix: stabilize compaction after reload](https://github.com/earendil-works/pi/pull/5675)  
**状态**：CLOSED  
**摘要**：修复重载后或压缩后消息队列投递失败的问题，保留之前的压缩边界，确保压缩流程稳定。  
**价值**：核心稳定性修复，避免对话压缩导致的数据丢失或异常。

### 3. [#5784 – fix(coding-agent): sort threaded sessions by latest activity in the subtree](https://github.com/earendil-works/pi/pull/5784)  
**状态**：OPEN  
**摘要**：线程模式下，按会话子树内最新活动排序，而非按根会话修改时间。  
**价值**：改进线程模式可用性，方便用户快速定位活跃分支。

### 4. [#5779 – feat(coding-agent): XML-structure /review prompt responses](https://github.com/earendil-works/pi/pull/5779)  
**状态**：CLOSED  
**摘要**：将 `/review` 命令改为 XML 结构化指令，支持覆盖率感知工作流，同时兼容传统 JSON 格式。  
**价值**：提升代码审查功能的可扩展性和模型理解度。

### 5. [#5758 – fix: diagnose when a child holds stdio open past exit](https://github.com/earendil-works/pi/pull/5758)  
**状态**：CLOSED  
**摘要**：检测子进程退出后仍保持标准输出的情况，避免管道阻塞导致无限等待。  
**价值**：解决 #5303 等长时间等待问题，提高 bash 工具执行可靠性。

### 6. [#5587 – feat(coding-agent): add experimental first-time setup flow](https://github.com/earendil-works/pi/pull/5587)  
**状态**：CLOSED  
**摘要**：在 `PI_EXPERIMENTAL=1` 下，交互式启动时显示首次设置对话框（主题选择、分析共享），集成自动主题检测和预览。  
**价值**：降低新手使用门槛，配合 v0.79.4 的新主题功能。

### 7. [#2331 – feat(extensions): add vim-like modal editor extension](https://github.com/earendil-works/pi/pull/2331)  
**状态**：CLOSED  
**摘要**：为 pi 添加类似 Vim 的模态编辑器扩展（Normal/Insert/Visual/Command-line 模式），支持基本动作、操作符和 Ex 命令。  
**价值**：满足 Vim 用户偏好，扩展生态系统多元化（最近更新，仍被关注）。

### 8. [#5509 – feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/5509)  
**状态**：OPEN  
**摘要**：增加 Amazon Bedrock Mantle 的 OpenAI Responses API 提供商，支持 GPT 5.5/5.4 模型。  
**价值**：快速跟进 AWS 新服务，使 pi 用户可在 Bedrock 上使用最新模型。

### 9. [#5765 – feat(d-pi): split createDPiExtension into remote-executor-extension and multi-agent-extension](https://github.com/earendil-works/pi/pull/5765)  
**状态**：CLOSED  
**摘要**：将原本单体 `createDPiExtension` 拆分为远程执行器和多代理两个独立扩展，提升可组合性。  
**价值**：解耦分布式执行和动态代理编排，利于维护和扩展。

### 10. [#5762 – feat: Add ZAI-CN (bigmodel.cn) provider](https://github.com/earendil-works/pi/pull/5762)  
**状态**：CLOSED  
**摘要**：新增 `zai-cn` 内置提供商，指向 `https://open.bigmodel.cn/api/paas/v4`，与已有的 ZAI 提供商并存。  
**价值**：为中国智谱用户提供直接可用的大模型接入，扩大区域覆盖。

---

## 功能需求趋势

从近期的 Issue 与 PR 可看出社区当前关注以下方向：

- **新 AI 提供商与模型支持**：Amazon Bedrock Mantle (#5363, #5509)、ZAI China (#5762)、Google Vertex Gemini 3.5 Flash (#5761)、ZhipuAI (#2345) 等提案密集出现，表明用户希望 pi 能覆盖更多云服务商与模型。
- **扩展 API 与体系化集成**：暴露 edit-diff (#5756)、增加 prompt guideline API (#5711)、拆分分布式扩展 (#5765) 等，社区正在推动扩展能力的标准化和解耦。
- **配置灵活性与安全性**：auth.json 支持提供商特定参数 (#5728)、truncate 选项环境变量化 (#5759)、SHA256SUMS 完整性校验 (#5739) 反映出对安全、可移植配置的追求。
- **TUI 交互细节打磨**：会话排序改进 (#5784)、模型名刷新 (#5696)、session 选择器自动关闭 (#5747)、Markdown 渲染 (#5766) 等，显示社区期望终端体验更人性化。
- **包管理与扩展生命周期**：Shrinkwrap 包重复 (#5653)、npmCommand 导致 CWD 污染 (#5774)、MCP 服务器导致命令挂起 (#5687) 是包管理系统当前的主要痛点，促使架构层面改进。

---

## 开发者关注点

1. **连接稳定性首位**：openai-codex 的 TUI 卡死（#4945）虽未完全定位，但社区复现率高，是当前最大痛处。
2. **扩展副作用难控制**：扩展加载 MCP 服务器导致包管理命令不退出（#5687），且 sendMessage 不返回 Promise 造成火并失火（#5751/PR #5752），异步契约需要统一。
3. **提供商兼容性参差不齐**：工具 schema、prompt_cache_retention 参数等被不同提供商拒绝（#3214、#5702），开发者需反复适配，核心需建立更健壮的参数过滤或配置校验。
4. **编译与运行环境问题**：Windows Git Bash 检测（#5103）、Bun 包管理器 CWD 污染（#5774）反映出平台兼容性和包管理细节仍需完善。
5. **安全与供应链担忧**：`pi update` 使用 `--min-release-age=0` 覆盖 npm 安全保护（#5785）引发社区警觉，安全与便利的平衡需要更多讨论。
6. **配置硬编码缺乏弹性**：truncate 限制（#5759）、默认最大行数等硬编码，用户希望环境变量或配置文件控制，减少对源码的依赖。

---

*本期日报基于 github.com/earendil-works/pi 仓库截至 2026-06-16 的公开数据整理。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-06-16）

---

## 1. 今日速览

今日发布了 **v0.18.1 正式版** 及 **Desktop v0.0.4**，修复了上下文过大警告、MCP 服务器移除持久化等问题；`v0.18.1-preview.0` 也同步推出。社区围绕 **`/loop` 循环自动化** 提交了密集的功能提案与实现（session 唤醒原语、任务文件、对齐命令等），但同时爆发了 **VSIX 文件被误报木马**、**子代理执行中途崩溃**、**`/quit` 后 OOM** 等关键 Bug，安全与稳定性成为关注焦点。

---

## 2. 版本发布

### v0.18.1（正式版）
- **新增**：daemon 直接 session shell 必须显式选择加入（`feat(daemon): gate direct session shell behind explicit opt-in`）
- **底层**：基于 v0.18.0 的版本发布。

### v0.18.1-preview.0 & nightly
- **修复**：对超大上下文指令给出运行时警告（`fix: warn on oversized context instructions`）
- **文档**：更新了过时的默认值、CLI 语法和工具命名。

### desktop-v0.0.4（桌面客户端）
- **修复**：MCP 服务器移除操作现在会真正持久化到配置
- **修复**：模型下拉列表现在会从原始模型定义刷新默认值
- 支持 Windows / macOS / Linux，可通过 `desktop-latest` 自动更新。

---

## 3. 社区热点 Issues（10 条）

1. **[#5055] Trojan:JS/ShaiWorm.DBA!MTB**（Open，评论 5）  
   VSIX 插件被 Windows Defender 标记为木马。影响所有下载安装的用户信任度，社区强烈关注。  
   https://github.com/QwenLM/qwen-code/issues/5055

2. **[#5180] 主会话派发子代理，子代理执行一半崩溃**（Open，评论 2）  
   multi-agent 场景下，subagent 在任务中途崩溃，导致 12 小时会话失败。涉及核心协调逻辑。  
   https://github.com/QwenLM/qwen-code/issues/5180

3. **[#5173] 多个 Provider 共享相同模型 ID 时选择不持久**（Open，评论 2）  
   当多个 OpenAI‑compatible provider 注册相同 `id`（如 `qwen3.7-max`）但不同 `baseUrl` 时，选择在重启后丢失。  
   https://github.com/QwenLM/qwen-code/issues/5173

4. **[#5147] `/quit` 后 OOM（managed auto‑memory 构建摘要时）**（Open，评论 2）  
   退出会话时自动内存提取触发 `buildTranscriptMessages()`，导致 V8 堆溢出，即使工具调用数为 0。  
   https://github.com/QwenLM/qwen-code/issues/5147

5. **[#5101] 重复大工具结果反复塞入 Provider 历史**（Closed，评论 2）  
   确定性 provider 反复请求同一命令，Qwen Code 将大工具结果累加至上下文爆炸。  
   https://github.com/QwenLM/qwen-code/issues/5101

6. **[#5142] CLI 虚拟历史模式下历史不可见，仅按 `/` 键才出现**（Open，评论 4）  
   输入框期望在底部、历史应始终可见，目前需按键触发，严重影响使用体验。  
   https://github.com/QwenLM/qwen-code/issues/5142

7. **[#5160] `/model` 列表显示已弃用的 OAuth 模型（即便未配置 OAuth）**（Open，评论 3）  
   干扰模型选择，用户需手动辨别已失效的选项。  
   https://github.com/QwenLM/qwen-code/issues/5160

8. **[#5159] macOS tmux 中触控板滚动触发历史导航而非视口滚动**（Open，评论 2）  
   触控板向上/下滑动误触 Prompt 历史，无法翻阅对话记录。  
   https://github.com/QwenLM/qwen-code/issues/5159

9. **[#3979] Plan 模式完成后在 Ghostty 终端不停闪屏**（Open，评论 2）  
   终端渲染问题，自 0.15.6 版本起存在，影响 Plan 模式使用。  
   https://github.com/QwenLM/qwen-code/issues/3979

10. **[#5177] `exit_plan_mode` 收到空 `plan` 参数，导致浪费重试轮次**（Open，评论 1）  
   模型在 Plan 模式下调用退出工具时传递空参数，反复失败重试，浪费 token。  
   https://github.com/QwenLM/qwen-code/issues/5177

---

## 4. 重要 PR 进展（10 条）

1. **[#5182] feat(loop): add session wakeup primitive**（Open）  
   新增 `loop_wakeup` 工具，为自定节奏 `/loop` 提供一次性会话唤醒原语，不改变当前行为。  
   https://github.com/QwenLM/qwen-code/pull/5182

2. **[#5181] fix(core): prevent OOM in auto‑memory extraction during /quit**（Open）  
   修复 #5147：在 `buildTranscriptMessages` 中分批处理，避免全量 Regex 导致堆溢出。  
   https://github.com/QwenLM/qwen-code/pull/5181

3. **[#5179] fix(model): remember selected provider when multiple share a model id**（Open）  
   修复 #5173：将选定 provider 的 `baseUrl` 持久化，重启后自动恢复。  
   https://github.com/QwenLM/qwen-code/pull/5179

4. **[#5175] feat(daemon): deliver web‑shell mid‑turn messages into the running turn**（Open）  
   允许用户在 turn 进行中输入消息，并将其注入到当前批处理之间，显著提升 daemon 交互体验。  
   https://github.com/QwenLM/qwen-code/pull/5175

5. **[#4943] feat(cli): add --safe-mode flag**（Open）  
   新增 `--safe-mode`（及环境变量 `QWEN_CODE_SAFE_MODE`），禁用所有自定义（QWEN.md、hooks、MCP 等），用于故障排查。  
   https://github.com/QwenLM/qwen-code/pull/4943

6. **[#5094] feat(core+cli): Workflow P4 — meta + /workflows + phase‑tree**（Open）  
   动态工作流大版本的最后一块：元数据提取、`/workflows` 命令、阶段树渲染，基于已合并的 P1‑P3。  
   https://github.com/QwenLM/qwen-code/pull/5094

7. **[#4850] feat(extensions): interactive multi‑tab /extensions manager**（Open）  
   将 `/extensions` 改为交互式三标签管理器：已安装、发现、源管理，支持扩展和 MCP 服务器全生命周期。  
   https://github.com/QwenLM/qwen-code/pull/4850

8. **[#4793] fix: coerce non‑string tool params to strings for self‑hosted LLMs**（Open）  
   LMStudio、vllm 等自托管模型有时返回数字/布尔参数，现自动转为字符串，避免 `SchemaValidator` 拒绝。  
   https://github.com/QwenLM/qwen-code/pull/4793

9. **[#5171] fix(core): auto‑retry transport stream errors before first chunk**（Open）  
   针对流式传输首块之前的网络抖动，增加有限重试，提升服务稳定性。  
   https://github.com/QwenLM/qwen-code/pull/5171

10. **[#4564] feat(stats): expose token usage for cost visibility**（Open）  
    持久化 token 用量，扩展 `/stats` 命令支持日/月汇总、模型分解和 CSV/JSON 导出。  
    https://github.com/QwenLM/qwen-code/pull/4564

---

## 5. 功能需求趋势

从近期 Issues & PRs 提炼出社区最关注的 **5 个功能方向**：

- **循环自动化（/loop 生态）**  
  自定节奏循环、任务文件、唤醒调度、取消与状态反馈——用户对长时间后台任务有强烈需求，相关 PR 已密集落地。

- **多 Agent 协调**  
  主会话派发 subagent、分支（fork）语义、agent 类型可配置，代理间的稳定性和结果返回是痛点。

- **模型 / Provider 管理**  
  多 Provider 消歧义、已弃用模型过滤、provider 选择持久化——随着服务商增多，配置体验亟待优化。

- **上下文与内存治理**  
  OOM 保护、超大工具结果去重、QWEN.md 长度自适应警告、结构化克隆优化——长会话稳定性是刚需。

- **扩展与生态系统**  
  交互式扩展管理器、钩子系统传递原始 `toolCallId`、MCP 参数类型兼容、Desktop 客户端功能增强（如 Git 分支显示）。

---

## 6. 开发者关注点（痛点 / 高频反馈）

- **安全疑虑**：`.vsix` 被误报木马，需官方及时回应并可能调整打包签名。
- **子代理可靠性**：subagent 执行中途崩溃（#5180）导致长时间工作丢失。
- **模型选择器混乱**：多个 provider 同名时选择不持久，且展示已停用模型（#5173, #5160）。
- **内存崩溃**：`/quit` 后 OOM（#5147）和重复大工具撑爆上下文（#5101）频繁出现。
- **CLI 基本体验**：历史模式不可见（#5142）、触控板误触历史（#5159）、计划模式闪屏（#3979）影响日常使用。
- **权限与流程**：sudo 命令无法直接允许（#5119）、`exit_plan_mode` 空参数导致浪费（#5177）暴露对话流程缺陷。
- **文档过时**：CLI 语法、默认值、工具命名存在漂移，需跟进维护。

---

*数据来源：[QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) | 生成时间 2026-06-16*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是为您生成的 2026-06-16 DeepSeek TUI 社区动态日报。

---

# DeepSeek TUI 社区动态日报 ｜ 2026-06-16

## 今日速览

项目今日核心动态集中在架构优化与新功能拓展。主要亮点包括：核心贡献者合并了 Provider 元数据注册表重构（PR #3005），为未来支持更多模型供应商铺平道路；同时，社区对 Agent 协议注册（#3192）和子代理持久化权限（#1186）的需求讨论热烈。此外，Windows 平台稳定性问题（#1812）及任务卡死（#2739）等老问题持续引发用户关注。

## 社区热点 Issues

1. **[#2487] Frequent error: Turn stalled - no completion signal received** (评论: 13)
   - **摘要**：在 `yolo` 模式下频繁出现“Turn stalled”错误，任务卡死后无法通过 `continue` 恢复。这是当前社区反馈最集中的稳定性问题，严重影响使用体验。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/2487

2. **[#3063] v0.8.59: release tracker — TUI mouse-report leak, runtime safety** (评论: 11)
   - **摘要**：作为 v0.8.59 版本的发布跟踪 Issue，主要修复了 macOS 上 TUI 鼠标报告泄露问题，并进行了多项运行时安全性改进。该 Issue 已关闭，代表一个重要的稳定性里程碑。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/3063

3. **[#1186] feat(execpolicy): add typed persistent permission rules** (评论: 9)
   - **摘要**：提议为执行策略层增加类型化持久权限规则，支持按工具名称、命令前缀、路径模式设置 `allow/deny/ask` 规则。这是一项提升安全性和用户体验的关键功能，社区讨论积极，目标版本为 v0.9.0。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/1186

4. **[#891] Support Codex /goal long-running task mode** (评论: 8)
   - **摘要**：建议移植 Codex 的长期目标模式，让 Agent 可以持续工作直至完成重构、多文件修改等复杂任务，而非单次响应后停止。该 Issue 已关闭，表明功能可能已被采纳或已有替代方案。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/891

5. **[#3096] Split sub-agents into a headless worker runtime with lightweight TUI projections** (评论: 8)
   - **摘要**：提出将子代理架构进行解耦，从“UI 密集型”转变为“无头工作运行时”。这旨在解决子代理在并发场景下资源占用过高的问题，是架构级别的重大改进。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/3096

6. **[#3192] Put it up for agentclientprotocol/registry** (评论: 6, 更新于今日)
   - **摘要**：社区成员提议将 CodeWhale 注册到 Agent Client Protocol (ACP) 注册表中，这将使 Zed 等其他工具能更容易地发现和集成 CodeWhale。反映了社区对更开放协议和生态集成的渴望。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/3192

7. **[#1812] TUI-freeze-Windows-crossterm-poll** (评论: 6)
   - **摘要**：长期存在的 Windows 平台 TUI 间歇性冻结问题。用户报告界面完全无响应但进程仍在运行。该问题至今未关闭，是 Windows 用户的核心痛点。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/1812

8. **[#2574] Feature Request: Provider fallback chain — auto-switch on API failure** (评论: 4)
   - **摘要**：建议增加 Provider 自动故障切换链功能。当当前 Provider 因配额、认证或服务端错误不可用时，能自动切换到备选 Provider，避免手动中断对话。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/2574

9. **[#2629] 无法与硅基流动(SiliconFlow)和腾讯云TokenHub配合使用，返回401认证错误** (评论: 4)
   - **摘要**：中文用户报告 CodeWhale 无法正常使用硅基流动和腾讯云 TokenHub 等国内平台。虽然配置为 OpenAI 兼容接口，但仍返回 401 认证错误，影响了国内用户的使用。
   - **链接**：https://github.com/Hmbown/CodeWhale/issues/2629

10. **[#2739] 依然会出现任务执行过程中卡死的状态** (评论: 3)
    - **摘要**：用户反馈即便在购买了 API 服务后，任务执行时仍会卡死，陷入无限等待。此问题历史较久，反复出现，严重影响用户信任度。
    - **链接**：https://github.com/Hmbown/CodeWhale/issues/2739

## 重要 PR 进展

1. **[#3005] refactor(config): extract provider metadata into data-driven registry** (状态: 已合并)
   - **摘要**：核心重构：将 Provider 的 ID、显示名、别名、默认配置等信息统一到一个静态的 `PROVIDER_REGISTRY` 中。此 PR 消除了大量重复的代码匹配分支，极大地简化了新 Provider 的添加流程。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3005

2. **[#3244] fix(update): retry release lookups and downloads** (状态: 已合并)
   - **摘要**：修复更新模块：增加了对 GitHub Release 元数据查询和资产下载失败的重试逻辑，提升了更新过程的稳健性。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3244

3. **[#3241] [codex] accept dollar skill aliases** (状态: 已合并)
   - **摘要**：功能增强：允许用户在 composer 中输入 `$skill-name` 来直接激活技能，提供了除 `/skill` 命令外的快捷方式，并支持了相关的补全和选择功能。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3241

4. **[#3235] feat: add DeepInfra provider support** (状态: 已合并)
   - **摘要**：新 Provider 支持：DeepInfra 是一个托管的 AI 推理云平台，拥有超过 100 个开源模型。此 PR 允许用户将 CodeWhale 连接到 DeepInfra 后端。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3235

5. **[#3233] feat(config): persist ask-only permission rules atomically** (状态: 已合并)
   - **摘要**：功能实现：为持久化权限规则（#1186）奠定了基础，实现了仅保留 'ask' 类型规则的原子化持久化 API，但不改变审批语义。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3233

6. **[#3257] feat(app-server): make app-server the canonical runtime API entrypoint** (状态: 已合并)
   - **摘要**：架构改进：将 `app-server` 命令标准化为运行时 API 的规范入口点，统一了 HTTP 和移动端接口的调用路径。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3257

7. **[#3242] feat: add workspace_follow_symlinks setting for symlink-aware tool operations** (状态: 开放中)
   - **摘要**：功能需求：新增 `workspace_follow_symlinks` 配置项，使文件遍历相关的工具（如文件搜索）能够跟随符号链接，满足特定开发场景需求。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3242

8. **[#3239] docs: add Atlas Cloud as OpenAI-compatible LLM backend** (状态: 开放中)
   - **摘要**：文档更新：社区贡献者提交了关于集成 Atlas Cloud（59个模型）作为 OpenAI 兼容后端的文档和 `.env.example` 配置示例。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/3239

9. **[#2986] docs(contributing): harvest-credit close template + stewardship branch explanation** (状态: 已合并)
   - **摘要**：流程改进：增加了对“Harvest-Credit”关闭模板的文档说明，旨在更好地记录和感谢社区贡献者，即使他们的 PR 代码以不同形式被合并。
   - **链接**：https://github.com/Hmbown/CodeWhale/pull/2986

10. **[#2239] feat: i18n Phase 1-4b wiring + rebase compile fixes** (状态: 开放中)
    - **摘要**：长期分支的国际化功能（Phase 1-4b）正在进行架构适配和编译错误修复。此 PR 涉及 47 个文件，是推进多语言支持的关键一步。
    - **链接**：https://github.com/Hmbown/CodeWhale/pull/2239

## 功能需求趋势

1. **Provider 模型支持**：社区对新模型 Provider 的热情持续高涨，如 DeepInfra (#3235)、Atlas Cloud (#3239) 的 PR 提交，以及 Provider 自动故障切换 (#2574) 的功能请求，表明用户希望拥有更多元、稳定且灵活的 AI 后端选择。

2. **Agent 协议与生态集成**：将项目注册到 Agent Client Protocol (#3192) 的建议，反映了社区不满足于现有 TUI，期望能与 Zed 等其他开发工具实现更深度集成的趋势。

3. **安全与权限管理**：围绕执行权限持久化 (#1186, #3233) 和 API Key 的安全管理 (#3004) 的讨论热度很高，用户对在共享环境中安全、方便地使用工具提出了更高要求。

4. **长期运行与稳定性**：对“Goal 模式” (#891)、子代理检查点 (#2029) 和解决任务卡死 (#2739, #2487) 的讨论，表明用户对项目在处理长期、复杂工作流时的稳定性和可恢复性有强烈诉求。

## 开发者关注点

1. **稳定性是首要痛点**：多个高评论的 Issue 指向了任务执行过程中的卡死和 "Turn stalled" 错误（#2487, #2739）。
2. **Windows 用户体验亟待优化**：Windows 平台的 TUI 冻结问题（#1812）是长期存在的顽固 Bug，影响了大量用户。
3. **后端兼容性挑战**：与中国本土平台（如硅基流动）的兼容性问题（#2629），以及与其他 API 的部分不兼容（#3265），是国际化与本地化面临的现实挑战。
4. **多代理并行超时**：关于 SSE 多智能体在 Windows 下 45 秒超时的问题（#1679）以及子代理 API 超时（#1806）依然存在，限制了复杂并行任务的效率。
5. **对架构改进的期待**：社区深度用户对项目的架构演进表现出浓厚兴趣，并对诸如子代理架构解耦 (#3096) 这样的重大改进表示认可和期待。

---

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*