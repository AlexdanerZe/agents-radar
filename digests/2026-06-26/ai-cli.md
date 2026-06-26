# AI CLI 工具社区动态日报 2026-06-26

> 生成时间: 2026-06-26 03:23 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-06-26）

## 1. 生态全景

当前 AI CLI 工具生态处于 **功能深化与信任重建并行** 的阶段。一方面，MCP 协议成为事实标准，几乎所有主流工具都在强化工具注册、权限管控和运行时生命周期；另一方面，**Agent 可靠性、计费透明度与跨平台一致性** 成为用户强烈关注的核心痛点。社区活跃度高位运行，头部工具（OpenAI Codex、Claude Code、Gemini CLI）每日产生近百条高质量讨论，而新锐工具（DeepSeek TUI/CodeWhale、OpenCode）通过开放设计和技术差异化加速追赶。整体生态正从“能用”向“可靠、可控、可审计”的方向快速演进。

## 2. 各工具活跃度对比

| 工具 | 热点 Issue 数 | 重要 PR 数 | 版本发布 |
|------|:------------:|:----------:|---------|
| Claude Code | 10 | 1 | v2.1.193 |
| OpenAI Codex | 10 | 10 | v0.142.2 / 多个 alpha / codex-zsh-v0.1.0 |
| Gemini CLI | 10 | 10 | v0.51.0-nightly / v0.50.0-preview.1 / v0.49.0 |
| GitHub Copilot CLI | 10 | 1 | v1.0.66-0 |
| Kimi Code CLI | 2 | 0 | 无 |
| OpenCode | 10 | 10 | v1.17.11 |
| Pi (pi-mono) | 10 | 10 | 无 |
| Qwen Code | 10 | 10 | 无 |
| DeepSeek TUI (CodeWhale) | 10 | 10 | v0.8.65 (品牌重塑) |

> **趋势解读**：头部工具 PR 与 Issue 数量普遍处于高位，反映出社区参与度和项目迭代速度较快。Kimi Code CLI 尚处于早期阶段，活跃度最低。

## 3. 共同关注的功能方向

### 3.1 MCP 工具协议深化与扩展
- **涉及工具**：所有 9 个工具均有涉及
- **具体诉求**：工具注册扫描（Claude Code `classifyAllShell`、Kimi Code #2475）、MCP OAuth 自动刷新（OpenAI Codex #17265）、MCP 图片 MIME 嗅探（Gemini CLI #27850）、MCP 服务启停管理（Copilot CLI v1.0.66-0）、MCP 服务骨架搭建（OpenCode #33988）、MCP RPC 超时可配置（Pi #6087）、MCP 运行时复用（OpenAI Codex #30148）、MCP 工具与审批预览（DeepSeek TUI #3619）

### 3.2 计费透明化与配额管理
- **涉及工具**：Claude Code、OpenAI Codex、Copilot CLI、Gemini CLI
- **具体诉求**：默认模型静默升级导致高额账单（Claude Code #71481）、GPT-5.5 配额消耗异常（OpenAI Codex #28879/#30002）、响应预算控制（Copilot CLI v1.0.66-0 实验特性）、上下文预算低于声称值（Gemini CLI 类似痛点，由错误提示间接反映）

### 3.3 会话可靠性与历史恢复
- **涉及工具**：Claude Code、Copilot CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI
- **具体诉求**：VSCode 扩展历史丢失（Claude Code #29017）、Session 恢复后模型列表不认证（Copilot CLI #3596/#3680）、自动压缩导致上下文丢失（OpenAI Codex #5957）、会话快照回退（OpenCode v1.17.11）、会话结算后 Agent 恢复缺陷（Pi #5886）、长期 Session 状态同步（DeepSeek TUI #3620）

### 3.4 Windows / ARM 跨平台兼容性
- **涉及工具**：Claude Code、OpenAI Codex、Copilot CLI、OpenCode、Qwen Code、DeepSeek TUI
- **具体诉求**：Windows 权限绕过不可用（Claude Code #61415）、sandbox 弹窗（OpenAI Codex #29200）、WSL2 ARM64 剪贴板失败（Copilot CLI #3534）、Bun segfault 崩溃（OpenCode #33742）、PowerShell 内存泄漏（Qwen Code #5873）、Windows SSE 超时 UI 错乱（DeepSeek TUI #1679）

### 3.5 Agent 自主性 vs 用户控制力
- **涉及工具**：Claude Code、Gemini CLI、Copilot CLI、DeepSeek TUI
- **具体诉求**：子代理误报成功（Gemini CLI #22323）、Plan 模式仍执行 Agent 行为（DeepSeek TUI #3568）、preToolUse 静默重写仍弹窗（Copilot CLI #2643）、用户中断钩子（Claude Code #9516）、子代理状态同步（DeepSeek TUI #3620）

## 4. 差异化定位分析

| 工具 | 核心定位 | 功能侧重 | 目标用户 | 技术路线 |
|------|---------|---------|---------|---------|
| **Claude Code** | 通用 AI 编程助手 | 权限管控、自动模式分类、1M 上下文 | 全栈开发者，企业团队 | 模型能力驱动，强安全体系 |
| **OpenAI Codex** | ChatGPT 集成编码工具 | 插件生态、MCP 认证、费率管理 | ChatGPT Plus/Pro 用户 | 依托 OpenAI 模型，云服务与本地结合 |
| **Gemini CLI** | 多 Agent 协作平台 | 子代理编排、Tool Registry DI、沙箱 | 复杂工程团队 | 模型级原生 Bash 亲和，强 Agent 抽象 |
| **GitHub Copilot CLI** | GitHub 生态编码助手 | MCP 图形管理、企业策略、Voice 模式 | GitHub 企业用户 | 深度绑定 GitHub 身份，渐进式 Agent |
| **Kimi Code CLI** | 轻量极简 CLI | 模型兼容、MCP 工具支持 | 个人开发者，新手 | 快速迭代，社区驱动（当前规模较小） |
| **OpenCode** | 可编程 Agent 框架 | SDK 暴露、会话快照、v2 布局、MCP 服务层 | 框架使用者，二次开发者 | Effect-TS 响应式架构，强调嵌入式能力 |
| **Pi** | 终端优先的扩展平台 | 扩展生态、RPC 接口、TUI 定制、i18n | 重度终端用户，扩展开发者 | 插件化架构，Node 运行时 |
| **Qwen Code** | 多 IDE 全平台支持 | IDE 深度集成（VS Code/JetBrains）、CI 安全 | 前端/全栈，AI 集成商 | 自家 Qwen 模型，注重 CI 与扩展创建 |
| **DeepSeek TUI** | 多模型舰队管理 | Fleet 负载选择、审批规则持久化、Rust 原生 | 成本敏感型团队，多模型用户 | Rust 原生性能，品牌重塑为 CodeWhale |

## 5. 社区热度与成熟度

- **超高活跃度（社区大、反馈快）**：**OpenAI Codex** 与 **Claude Code** 评论区动辄 50–150 条讨论，单 Issue 点赞上百，反映出最大规模的用户基础。两者在计费透明度和模型退化方面的讨论尤为激烈。

- **高速迭代（日 PR 量 ≥10）**：**OpenAI Codex**、**Gemini CLI**、**OpenCode**、**Pi**、**Qwen Code**、**DeepSeek TUI** 每天均有 10 个左右重要 PR 在推进，表明项目处于快速功能释放期。**DeepSeek TUI** 虽然社区规模较小，但日更新 41 Issues / 50 PRs，速度惊人。

- **成熟度分化**：
  - **Claude Code** 和 **OpenAI Codex** 已进入稳定期，但频繁出现计费 / 性能回归，显示其复杂系统难以全面测试。
  - **Gemini CLI** v0.50–v0.51 仍处于 preview/nightly，Agent 可靠性问题频发，属快速迭代早期。
  - **Copilot CLI** v1.0.66 已相对稳定，但会话管理和跨平台细节仍不够成熟。
  - **Kimi Code CLI** 仅有 2 个 Issue，社区尚在培育中。
  - **Pi** 和 **OpenCode** 均在积极构建扩展 / SDK 生态，逐步从工具向平台转型。

- **潜在信任危机**：Claude Code 和 OpenAI Codex 的计费混乱、模型静默升级、以及会话数据丢失问题正在消耗用户信任，修复优先级需提升。

## 6. 值得关注的趋势信号

### 6.1 MCP 从辅助组件走向核心基础设施
几乎所有工具都在围绕 MCP 进行架构重构：从工具注册、认证刷新、资源更新通知到运行时复用。**MCP 正在成为 AI CLI 的“标准总线”**，未来跨工具互操作将成为可能。开发者应优先掌握 MCP 协议，并能通过自定义 MCP Server 扩展工作流。

### 6.2 费用透明化从“要求”变为“刚需”
多个头部社区（Claude Code、OpenAI Codex）集中暴露出**模型选择不透明、配额计算偏差和静默升级导致的高额账单**问题。这表明用户已从“尝鲜”进入“精打细算”阶段，工具必须提供：
- 模型调用的实时费用预估
- 预算上限与预警
- 默认模型的显式确认机制  
不解决这一问题的工具将流失大量付费用户。

### 6.3 跨平台体验差距成为用户流失隐患
从 Windows 崩溃（OpenCode）、PowerShell 内存泄漏（Qwen Code）、WSL2 剪贴板失败（Copilot CLI）到 SSE 超时 UI 错乱（DeepSeek TUI），**非 macOS 用户普遍感到“二等公民”待遇**。随着 ARM 架构和 Linux 桌面份额增长，工具团队需投入更多跨平台适配资源。

### 6.4 多模型舰队管理（Fleet）成为新范式
DeepSeek TUI 的 Fleet 负载选择、OpenAI Codex 的作用域感知默认模型、以及 Gemini CLI 的模型命令，共同指向**用户不再满足于固定模型，而是希望工具能根据成本/任务自动选择最优模型**。这一趋势将推动工具在路由策略、上下文预算分配和成本优化上的深度创新。

### 6.5 Agent 可靠性仍是最大“信任杀手”
子代理误报成功（Gemini CLI）、Plan 模式下仍执行 Agent 行为（DeepSeek TUI）、永久挂起（Gemini CLI）等 Bug 反复出现。**用户宁可收到明确失败，也无法接受虚假成功或无限等待**。Agent 的观测性（轨迹分享、Token 消耗分解、子状态同步）将成为下一阶段的竞争焦点。

### 6.6 安全规则走向细粒度和持久化
从 Claude Code 的自动模式分类器、Copilot CLI 的 preToolUse 拦截，到 DeepSeek TUI 的持久化审批规则（allow/deny/ask），社区普遍要求**摆脱每次弹窗的骚扰，让安全决策能够记住并按路径/工具名/命令前缀留存**。这与企业级合规需求一致，也是 CLI 工具从个人工具转向团队协作的关键能力。

---

**总结**：2026 年中的 AI CLI 生态正经历“能力膨胀后的痛苦收敛”。MCP 协议统一了扩展方式，但 Agent 可靠性、成本透明化和跨平台体验仍是决定工具能否留在开发者工作流中的关键变量。对于技术决策者，选择工具时应优先考察其**会话稳定性**、**计费可预测性**和**多平台真实表现**，而非仅关注模型能力本身。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是基于 `anthropics/skills` 仓库数据的 Claude Code Skills 社区热点报告（数据截至 2026-06-26）。

---

## Claude Code Skills 社区热点报告

### 1. 热门 Skills 排行

按社区讨论热度与影响力排序（当前全部为 `Open` 状态）：

1.  **修复 skill-creator 核心评估系统 (PR #1298)**
    - **功能：** 修复 `run_eval.py` 导致所有 Skill 召回率归零的致命缺陷，并修正 Windows 流读取、触发检测及并行工作器问题。
    - **热点：** 该 BUG 被 10+ 用户独立重现（关联 Issues #556, #1169），直接导致描述优化循环完全失效，是当前社区最急迫解决的工具链故障。
    - **状态：** Open
    - **链接：** [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **添加测试模式 Skill (PR #723)**
    - **功能：** 统一化 Web 测试体系，涵盖单元测试（AAA 模式）、React 组件测试（Testing Library）及 E2E 测试。
    - **热点：** 社区对规范化测试指导的渴求极高，该 Skill 提供了一套完整的测试 Trophy 模型和正反例，是质量保障的核心诉求体现。
    - **状态：** Open
    - **链接：** [PR #723](https://github.com/anthropics/skills/pull/723)

3.  **添加文档排版 Skill (PR #514)**
    - **功能：** 解决 AI 生成文档中的孤儿行、寡行段落及编号错位等专业排版问题。
    - **热点：** 体现社区对 AI 产出物“专业感”的极致追求，属于小而精但普适性极强的实用 Skill。
    - **状态：** Open
    - **链接：** [PR #514](https://github.com/anthropics/skills/pull/514)

4.  **添加 Skill 质量与安全分析器元技能 (PR #83)**
    - **功能：** 引入针对 Skill 本身的质量评估（结构/文档）与安全扫描工具。
    - **热点：** 直接回应了命名空间信任危机（Issue #492），社区期待以此建立社区 Skill 的自动化审核与治理标准。
    - **状态：** Open
    - **链接：** [PR #83](https://github.com/anthropics/skills/pull/83)

5.  **添加 AppDeploy 部署 Skill (PR #360)**
    - **功能：** 让 Claude 直接从对话中执行全栈 Web 应用的部署、状态管理与版本控制。
    - **热点：** 标志着社区从“生成代码”向“执行部署”的关键跃迁，是 Agent 自主能力闭环的重要补全。
    - **状态：** Open
    - **链接：** [PR #360](https://github.com/anthropics/skills/pull/360)

6.  **添加代码库库存审计 Skill (PR #147)**
    - **功能：** 提供系统化的 10 步工作流，用于清理僵尸代码、识别未使用文件及定位文档缺口。
    - **热点：** 针对大型项目维护与重构的强需求，提供了极具操作性的标准化流程。
    - **状态：** Open
    - **链接：** [PR #147](https://github.com/anthropics/skills/pull/147)

7.  **Windows 平台兼容性集中修复 (PR #1050, #1099, #538)**
    - **功能：** 修复 Windows 下子进程 PATH 解析失败、cp1252 编码崩溃、文件大小写引用错误等。
    - **热点：** 跨平台粘性是本次社区发声中反馈最密集的技术债，影响着大量 Windows 用户的基本使用。
    - **状态：** Open
    - **链接：** [PR #1050](https://github.com/anthropics/skills/pull/1050) | [PR #1099](https://github.com/anthropics/skills/pull/1099)

---

### 2. 社区需求趋势

从 Issues 中提炼的核心期望方向：

- **安全与治理框架（High Priority）：** 社区强烈要求划清“官方”与“社区” Skills 的信任边界（Issue #492），并引入统一的命名与审核机制。
- **Skill 分发与协作：** 企业级用户迫切需要组织内 Skill 的共享库与直接链接分享，以彻底告别手动传输 `.skill` 文件（Issue #228）。
- **跨平台稳定性：** Windows 环境下子进程处理和编码问题（Issue #1061）是阻碍用户基数扩大的首要技术障碍，修复呼声极高。
- **AI 原生文档处理：** 用户对生成文档的排版（PR #514）、格式兼容（ODT、修正 DOCX 冲突）有明确诉求，希望输出达到可直接交付的水准。
- **Agent 持久化与记忆：** 长会话与跨对话的上下文维持（PR #154, Issue #1329）被视为构建复杂 Agent 应用的底层基础设施。
- **标准接口与可组合性：** 社区期待 Skill 能向 MCP（Model Context Protocol）标准化演进（Issue #16），以便于更灵活的工具链集成。

---

### 3. 高潜力待合并 Skills

以下 PR 讨论热烈、价值明确，预计近期落地优先级较高：

1.  **skill-quality-analyzer & skill-security-analyzer (PR #83)**
    - **理由：** 直接填补了治理机制的空白。缺乏这套工具，社区对“三方 Skill”的信赖度就无法建立，合并紧迫性极高。
    - **链接：** [PR #83](https://github.com/anthropics/skills/pull/83)

2.  **testing-patterns (PR #723)**
    - **理由：** 包装完整、视角全面（测试奖杯模型），是开发者呼声最高的日常刚需，具备极强的用户基数。
    - **链接：** [PR #723](https://github.com/anthropics/skills/pull/723)

3.  **shodh-memory (PR #154)**
    - **理由：** 提供 `proactive_context` 和结构化记忆模式，设计成熟。一旦合并，将催生大量依赖长期上下文的 Agent 应用。
    - **链接：** [PR #154](https://github.com/anthropics/skills/pull/154)

4.  **codebase-inventory-audit (PR #147)**
    - **理由：** 针对遗留系统与现代仓库的维护痛点，提供可复用的标准化工作流，企业级用户价值明显。
    - **链接：** [PR #147](https://github.com/anthropics/skills/pull/147)

---

### 4. Skills 生态洞察

一句话总结：
**当前社区最集中的诉求是：优先修复核心工具链（skill-creator）的致命评估缺陷与跨平台兼容性瓶颈，并迅速建立 Skills 分发的安全信任与治理标准机制，为下一阶段生态的规模化扩张扫清障碍。**

---

好的，作为专注 AI 开发工具的技术分析师，我为您呈上 2026-06-26 的 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-06-26

## 今日速览

今日社区讨论热度集中在 **v2.1.193 版本发布**带来的安全与权限管控新特性，以及围绕 **1M 上下文窗口计费、Opus 模型性能退化**和**多会话数据丢失**等问题的广泛讨论。此外，关于**默认模型静默升级导致高额意外账单**的投诉引发了社区对平台透明度的严肃反思。

## 版本发布

### v2.1.193 版本更新
- **发布内容：** 主要增强了命令执行的自动模式分类器功能，并完善了权限控制的可视化。
- **更新要点：**
  - 新增 `autoMode.classifyAllShell` 设置，将所有 Bash/PowerShell 命令路由至自动模式分类器处理。
  - 在会话记录、拒绝提示框及 `/permissions` 最近拒绝列表中，增加了自动模式拒绝原因的明确说明。
  - 新增 `cla` 相关内容（因原文截断，推测为 CLA 贡献者协议相关流程或检查）。
- **GitHub:** [v2.1.193 Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.193)

## 社区热点 Issues

1.  **#36151 [功能] 移动端多账户切换功能**
    - **热度：** 110 条评论，380 👍
    - **重要性：** 社区呼声最高的功能之一，却因无法切换账户（受限于共享邮箱）导致用户体验割裂，说明用户对有清晰的个人工作/生活边界的移动端体验有强烈需求。
    - **链接:** [Issue #36151](https://github.com/anthropics/claude-code/issues/36151)

2.  **#3412 [功能] 粘贴文本块内容可预览/编辑**
    - **热度：** 76 条评论，269 👍
    - **重要性：** 针对依赖听写软件等特殊场景，精准指出了当前“黑盒式”粘贴体验的痛点。若能实现，将极大提升无障碍支持和高级用户的控制感。
    - **链接:** [Issue #3412](https://github.com/anthropics/claude-code/issues/3412)

3.  **#71481 [BUG] 默认模型静默升级导致高额意外账单**
    - **热度：** 2 条评论，但属今日新开 Issue，已引发关注。
    - **重要性：** 用户投诉 Claude Code 在无任何通知的情况下将默认模型从价格较低的 Sonnet 切换至价格高昂的 Opus，6 天内产生 506 美元额外费用。这触及了对用户知情权和费用透明度的信任危机。
    - **链接:** [Issue #71481](https://github.com/anthropics/claude-code/issues/71481)

4.  **#68780 [BUG] Claude Opus 4.8 推理能力严重下降**
    - **热度：** 12 条评论，16 👍
    - **重要性：** 核心模型的能力退化是致命问题。用户声称模型在“Max effort”模式下推理能力极差，并质疑存在误导性商业行为，情绪激烈，可能预示着模型版本迭代中的质量回退。
    - **链接:** [Issue #68780](https://github.com/anthropics/claude-code/issues/68780)

5.  **#61869 & #63896 [BUG] 1M 上下文窗口计费与“使用额度 (Usage Credits)”错误**
    - **热度：** 共 100+ 条评论
    - **重要性：** 这是一个高频 Bug 集群。用户在使用 Opus 4.x 的 1M 上下文模型时，频繁遭遇“需要打开使用额度”的 API 错误，即使是在付费状态下。这严重影响了长上下文场景下的可用性，暴露出 API 计费与模型选择之间的逻辑紊乱。
    - **链接:** [Issue #61869](https://github.com/anthropics/claude-code/issues/61869) & [Issue #63896](https://github.com/anthropics/claude-code/issues/63896)

6.  **#9516 [功能] 用户中断钩子 (User Interrupt Hook)**
    - **热度：** 23 条评论，43 👍
    - **重要性：** 用户希望能在手动中断 Claude Code 执行时，自定义触发一个钩子函数。这表明高级用户渴望更深度的自定义能力和工作流集成，以更好地控制 Agent 的行为。
    - **链接:** [Issue #9516](https://github.com/anthropics/claude-code/issues/9516)

7.  **#29017 [BUG] VSCode 扩展中对话历史丢失**
    - **热度：** 25 条评论，18 👍
    - **重要性：** 作为最重要的 IDE 集成入口，会话历史丢失是致命缺陷，会严重破坏用户的工作流和信任。此问题长期未解，说明 VSCode 扩展的数据持久化机制可能存在深层次问题。
    - **链接:** [Issue #29017](https://github.com/anthropics/claude-code/issues/29017)

8.  **#49747 [BUG] Opus 4.7 混合使用旧版 XML 和 JSON 工具调用格式**
    - **热度：** 30 条评论，32 👍
    - **重要性：** 模型在长上下文中混淆指令，会直接导致工具执行失败。这不仅是 Bug，更可能是模型内部指令冲突的表现，对整个 Agent 系统的稳定性构成威胁。
    - **链接:** [Issue #49747](https://github.com/anthropics/claude-code/issues/49747)

9.  **#61415 [BUG] macOS Desktop 绕过权限模式无法启用**
    - **热度：** 63 条评论
    - **重要性：** “绕过权限 (Bypass Permissions)”是高级用户的核心需求。此议题在 macOS 上持续异常，并影响 Desktop 应用，表明权限模型在不同平台和客户端间可能存在实现一致性缺陷。
    - **链接:** [Issue #61415](https://github.com/anthropics/claude-code/issues/61415)

10. **#71493 [BUG] 内存泄漏导致极端延迟**
    - **热度：** 1 条评论，但属严重性能问题。
    - **重要性：** 用户通过 /heapdump 发现内存以 348 MB/小时的速度增长。这种“慢性死亡”式的内存泄漏会严重影响长时间运行的会话的稳定性和响应能力，是典型的平台级稳定性隐患。
    - **链接:** [Issue #71493](https://github.com/anthropics/claude-code/issues/71493)

## 重要 PR 进展

1.  **#63686 [已关闭] 将 Stale 和 Auto-close 超时时间从 14 天延长至 90 天**
    - **分析：** 一个针对社区治理的 PR。将 issue 自动标记为“过时”并关闭的时间从 14 天大幅延长至 90 天。这表明项目维护者意识到很多问题需要更长的观察和讨论周期，短期内的沉默不代表问题已被解决，社区也普遍欢迎这种更宽松的“冷却期”。
    - **链接:** [PR #63686](https://github.com/anthropics/claude-code/pull/63686)

*注：今日数据中仅包含一条已处理的 PR，其内容聚焦于社区管理策略的调整。*

## 功能需求趋势

从今日的活跃议题中，可以提炼出社区最关注以下几个功能方向：

1.  **跨平台与 IDE 深度集成：** 用户对会话数据（如 VSCode 中的历史记录）的一致性和持久性有着核心诉求。同时，Desktop 应用在不同平台（尤其是 Windows）上的原生体验（如 SSH、快捷键、输入法支持）亟待完善。
2.  **模型选择与成本透明化：** 社区对计费模型的敏感性达到新高。不仅要支持 1M 长上下文，更要求**清晰、可控的计费规则**，对“静默升级”等高额收费行为极度反感。自定义模型选择、费用预警和用量监控是迫切需求。
3.  **安全与权限粒度：** 除了基本的权限管控（如 Bypass），开发者迫切需要更细粒度的控制，例如“用户中断钩子 (User Interrupt Hook)”、“粘贴内容预审”以及更智能的自动模式分类器（如 `classifyAllShell` 的实现）。
4.  **系统稳定性与性能：** 内存泄漏、工具调用格式混乱 (XML/JSON)、内核崩溃 (OOM) 等问题的高优先级修复是社区呼声最高的。Agent 在复杂场景下的**可靠性 (Reliability)** 是决定其能否真正投入生产的关键。
5.  **Agent 协作与云同步：** “Remote Control”、“Cowork”等协同功能备受关注，但也暴露了在跨设备（如 Mac vs Windows ARM64）和网络环境下的兼容性问题。云同步会话和配置的呼声持续高涨。

## 开发者关注点

1.  **模型能力决定论下的信任危机：** 当前最大的痛点在于模型（特别是 Opus 4.8）在推理、遵循指令和工具调用格式上的**性能退化**。开发者依赖于模型能力，任何退化都会直接摧毁对工具的信任。
2.  **“付费墙”与“1M 上下文”的混乱：** 付费用户在尝试使用核心的 1M 上下文功能时，频繁遇到“需要开通使用额度”的错误提示，无论使用 API Key 还是订阅。这暴露了后端计费逻辑的重大缺陷，直接阻碍核心功能的使用。
3.  **会话数据安全与“幽灵”体验：** 对话历史丢失（VSCode）、会话被静默关闭后残留进程、文件写入失败但无错误报告等问题，让开发者感觉数据是不可靠的，影响了将 Claude Code 用于长期、复杂项目的信心。
4.  **默认设置或升级带来的负面影响：** 无论是模型默认升级导致高额花费，还是系统配置变更导致新启动的会话挂起，开发者都**厌恶任何不被明确告知且预期外的行为变更**。“只管提交，不管后果”的体验是用户流失的关键原因。
5.  **“最佳平台”与“二等公民”的反差：** 多个 Bug（如权限绕过、IME 输入、TUI 界面）都明确标注 `platform:windows` 或 `platform:linux`。开发者，尤其是 Windows/Linux 用户，强烈感觉到自身平台的体验劣于 macOS，存在明显的“功能兑现”延迟或“bug 修复”优先级差异。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-06-26

> 数据来源：github.com/openai/codex  
> 统计时段：过去 24 小时内更新（2026-06-25 ~ 2026-06-26）

---

## 今日速览

- **费率问题持续发酵**：`gpt-5.5` 的预算消耗异常（#28879）仍是社区最关注的 Bug，152 条评论、304 个 👍，用户反馈同一工作负载每小时额度从 20+ 次对话骤降至 2-3 次。
- **SQLite 日志写入量过大部分缓解**：`rust-v0.142.0` 合并的 #29432/#29457 可减少约 85% 的日志，但仍有用户报告残留写入（#29532、#29814），官方正在持续跟进。
- **新稳定版 0.142.2 发布**：MCP 工具默认启用 tool search，macOS 客户端新增对系统代理、PAC/WPAD 的兼容支持。同时多个 0.143.0-alpha 版本释出，预告更多会话与模型管理改进。

---

## 版本发布

| 版本 | 说明 |
|------|------|
| [rust-v0.142.2](https://github.com/openai/codex/tree/rust-v0.142.2) | 稳定版更新：MCP 工具默认使用 tool search（向后兼容）；macOS 认证客户端新增 `respect_system_proxy` 选项以支持系统代理、PAC、WPAD。 |
| [rust-v0.143.0-alpha.25](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.25)<br>rust-v0.143.0-alpha.22<br>rust-v0.143.0-alpha.21<br>rust-v0.143.0-alpha.16 | 0.143.0 系列多个 alpha 迭代，未提供详细 Changelog。 |
| [codex-zsh-v0.1.0](https://github.com/openai/codex/releases/tag/codex-zsh-v0.1.0) | 首个 Zsh 插件版本，提供 shell 集成能力。 |

---

## 社区热点 Issues

挑选过去 24 小时内更新、讨论热度最高的 10 个 Issue，涵盖严重 Bug、性能退化和用户强烈需求的功能。

### 1. [#28879] GPT-5.5 费率成本突增 10-20 倍，5h 额度 2-3 次对话即耗尽
- **评论 / 👍**：152 / 304  
- **概要**：自 6 月 16 日起，ChatGPT Plus 用户的 Codex（`gpt-5.5`）预算消耗异常，同样模型/计划下从原来 20+ 次对话骤降至 2-3 次。日志显示每次 token 消耗的额度百分比增长约 10-20 倍。  
- **影响**：直接影响大量 Pro/Plus 用户的核心使用，社区反应极为强烈。  
- **链接**：[openai/codex Issue #28879](https://github.com/openai/codex/issues/28879)

### 2. [#28224] Codex SQLite 反馈日志写入量惊人：最高可达 640 TB/年
- **评论 / 👍**：86 / 385  
- **概要**：Codex 在 `～/.codex/logs_2.sqlite` 中高频写入 TRACE 日志，估算年写入量达 640 TB，严重消耗 SSD 寿命。社区贡献者发现并提交了 #29432/#29457 修复（已合并至 0.142.0），可避免约 85% 的日志量。  
- **追踪**：仍有用户报告残留写入（#29532、#29814、#30162）。  
- **链接**：[openai/codex Issue #28224](https://github.com/openai/codex/issues/28224)

### 3. [#9203] 强烈要求恢复 `/undo` 命令
- **评论 / 👍**：51 / 297  
- **概要**：用户反馈 Codex 无意中删除未跟踪文件或修改未提交内容时无法撤销，怀念之前的 `/undo` 功能。该请求已持续近半年，社区点赞数极高。  
- **链接**：[openai/codex Issue #9203](https://github.com/openai/codex/issues/9203)

### 4. [#25749] 无法验证遗留电话号码，无恢复路径导致账号锁死
- **评论 / 👍**：64 / 38  
- **概要**：用户使用 Google OAuth 可正常登录 ChatGPT，但 Codex 要求验证一个已经不可用的旧手机号，且不提供更换方式。该问题导致部分用户无法使用 Codex。  
- **链接**：[openai/codex Issue #25749](https://github.com/openai/codex/issues/25749)

### 5. [#13733] 后台进程轮询浪费大量 Token：每次查询都触发完整 API 往返
- **评论 / 👍**：30 / 23  
- **概要**：当后台任务（如 `cargo build`）运行时，Codex 进入轮询循环，每次状态检查都发送完整对话历史，导致 Token/额度快速消耗。用户期望轮询只消耗少量上下文。  
- **链接**：[openai/codex Issue #13733](https://github.com/openai/codex/issues/13733)

### 6. [#30002] 5h 配额重置后 41 分钟即再超限，服务端配额上报有 Bug
- **评论 / 👍**：25 / 4  
- **概要**：Pro 用户 5h 限额重置后，实际只使用了约 1.35M tokens（之前满窗口可用 156M tokens）就再次触发 `usage_limit_reached`，说明服务端计数器存在超报。  
- **链接**：[openai/codex Issue #30002](https://github.com/openai/codex/issues/30002)

### 7. [#30008] 所选模型已满，请更换模型
- **评论 / 👍**：22 / 1  
- **概要**：多位用户反馈 Codex App 和 CLI 频繁返回“Selected model is at capacity”，即使只做简单 Prompt 也提示容量不足，推测与近期资源调度变化有关。  
- **链接**：[openai/codex Issue #30008](https://github.com/openai/codex/issues/30008)

### 8. [#17265] 路由 MCP OAuth Token 不会自动刷新
- **评论 / 👍**：19 / 39  
- **概要**：Codex 将 MCP 服务器的 `refresh_token` 存储在 `～/.codex/.credentials.json`，但 access token 过期后不会自动刷新，导致 MCP 工具调用持续认证失败。  
- **链接**：[openai/codex Issue #17265](https://github.com/openai/codex/issues/17265)

### 9. [#29200] Windows Desktop：应用 `apply_patch` 时弹出 `codex-windows-sandbox-setup.exe` 对话框
- **评论 / 👍**：17 / 6  
- **概要**：升级至 26.616 后，每次调用 `apply_patch` 都会弹出 Windows 错误对话框，尽管 patch 结果成功。与 Windows sandbox 辅助程序有关。类似问题 #29782 已关闭。  
- **链接**：[openai/codex Issue #29200](https://github.com/openai/codex/issues/29200)

### 10. [#9203]（已选为第3条）  
**补选：** [#4867] 允许 Codex Web 创建包含二进制的 PR  
- **评论 / 👍**：27 / 46  
- **概要**：用户抱怨 Codex 成功完成任务但无法合并 PR，因为不慎生成了一个小的二进制文件。希望官方允许 PR 中包含二进制文件。  
- **链接**：[openai/codex Issue #4867](https://github.com/openai/codex/issues/4867)

---

## 重要 PR 进展

挑选过去 24 小时更新、功能影响较大的 10 个 PR。

### 1. [#30144] fix terminal rollout event durability（OPEN）
- **概要**：修复会话结束时 `TurnComplete`/`TurnAborted` 事件未刷新存储的问题，确保异步存储的线程商店也能正确持久化。  
- **链接**：[openai/codex PR #30144](https://github.com/openai/codex/pull/30144)

### 2. [#29375] Support npm marketplace plugin sources（OPEN）
- **概要**：使 Codex 插件源解析支持 `"source":"npm"`，从而让 npm 托管的插件能够正常显示在 `plugin list --available` 中并可添加。修复早期反序列化不可用的问题。  
- **链接**：[openai/codex PR #29375](https://github.com/openai/codex/pull/29375)

### 3. [#30164] Make new-thread model defaults scope-aware（OPEN）
- **概要**：允许 Codex 在同一配置包中为多个产品场景（如 Work、Coding）分别加载模型默认值，新线程启动时可按作用域选择正确的默认模型、推理力度等，无需重载配置。  
- **链接**：[openai/codex PR #30164](https://github.com/openai/codex/pull/30164)

### 4. [#30148] Reuse MCP runtimes when selected availability changes nothing（OPEN）
- **概要**：优化 MCP 运行时生命周期，当环境更新但未添加/移除 MCP 服务器时，不再重建运行时，避免不必要的资源浪费和工具注册抖动。  
- **链接**：[openai/codex PR #30148](https://github.com/openai/codex/pull/30148)

### 5. [#30087] app-server: forward MCP resource updates（CLOSED）
- **概要**：将 MCP 服务器的 `notifications/resources/updated` 回调转发至核心事件流，并暴露实验性的 `mcpServer/resource/updated` app-server 通知，使客户端能实时感知资源变更。  
- **链接**：[openai/codex PR #30087](https://github.com/openai/codex/pull/30087)

### 6. [#30156] Fall back when remote filesystem walk is unavailable（CLOSED）
- **概要**：新版本 Codex 客户端连接旧版 exec-server 时，若 `fs/walk` RPC 不存在，现会优雅降级而非直接报错，提升向后兼容性。  
- **链接**：[openai/codex PR #30156](https://github.com/openai/codex/pull/30156)

### 7. [#30000] Prototype Codex Apps as virtual HTTP MCP servers（OPEN）
- **概要**：引入 `codex-apps` crate，将 App 快照封装为独立的 Streamable HTTP MCP 端点，每个连接器对应一个认证端点，从而让 MCP 管理器统一管理 App 的工具调用，无需特殊启动分支。  
- **链接**：[openai/codex PR #30000](https://github.com/openai/codex/pull/30000)

### 8. [#29909] allow CCA image generation and web search extensions（CLOSED）
- **概要**：允许 CCA（Cross-Capability Agent）使用独立的 image_generation 和 web_search 扩展，同时保留旧模型的内置实现，并保持对非 OpenAI 提供商的排除。  
- **链接**：[openai/codex PR #29909](https://github.com/openai/codex/pull/29909)

### 9. [#29934] Expose MCP app identity in app context（CLOSED）
- **概要**：在 MCP 工具调用的 `appContext` 中新增 `appName`、`templateId`、`actionName` 可选字段，使 v2 客户端无需从工具名/URI 解析即可获取可信的应用身份。  
- **链接**：[openai/codex PR #29934](https://github.com/openai/codex/pull/29934)

### 10. [#30147] Use managed defaults for TUI threads（OPEN）
- **概要**：TUI（终端 UI）客户端现在会主动消费 `configRequirements/read` 暴露的管理默认值，使新线程使用与服务端一致的默认模型设置，对齐桌面 App 行为。  
- **链接**：[openai/codex PR #30147](https://github.com/openai/codex/pull/30147)

---

## 功能需求趋势

从过去 24 小时的 Issues 与 PR 中，可看出社区最关注的几个功能方向：

- **费率与配额透明化**：多个 Issue（#28879、#30002）反映配额消耗不透明和异常，用户期望更精细的用量报告和公平的限额机制。
- **MCP（Model Context Protocol）生态增强**：OAuth 刷新（#17265）、资源更新通知（#30087）、运行时复用（#30148）、工具发现（#30148）等 PR 持续完善 MCP 基础架构。
- **插件与扩展市场**：NPM 源支持（#29375）、插件服务预览（#28582）表明社区正推动开放插件生态，减少对单一源依赖。
- **会话 / 状态管理**：`/undo` 回归（#9203）、自动压缩丢失上下文（#5957）、后台轮询浪费（#13733）等诉求聚焦于会话的可靠性、可恢复性和资源效率。
- **模型默认值与作用域**：PR #30164、#29683、#30147 构建了按场景管理模型默认值的能力，为不同工作模式（Coding/Work）提供预设。
- **Sandbox / 本地执行**：Windows sandbox 弹窗（#29200、#29782）、sandbox ingress 暴露（#29263）提示用户对沙箱稳定性和网络互通的需求上升。
- **跨平台一致性与认证**：macOS 系统代理（已在 0.142.2 修复）及遗留号码验证（#25749）反映认证和网络配置的平台差异仍是痛点。

---

## 开发者关注点

综合 Bug 反馈与功能讨论，开发者遇到的主要痛点和高频需求包括：

1. **费率与配额异常** ★★★★★  
   GPT-5.5 成本飞升及应用内配额超报（#28879、#30002）导致正常开发中断，开发者亟需官方确认根因与补偿。

2. **本地日志写入过高** ★★★★☆  
   即使部分修复后仍有残留写入（#29532、#29814、#30162），对 SSD 寿命和多平台稳定性造成持续压力。

3. **MCP 工具调用认证不稳定** ★★★★☆  
   OAuth 不刷新（#17265）以及令牌过期后无自动续期，影响集成第三方服务的可靠性。

4. **模型容量限制频繁** ★★★★☆  
   “Selected model is at capacity” 错误频发（#30008），尤其是高峰时段，影响开发流程度。

5. **会话 / 历史丢失** ★★★☆☆  
   自动压缩（#5957）导致模型遗忘任务上下文，以及 `/undo` 缺失（#9203）让开发者无法撤销意外操作。

6. **Windows 平台稳定性** ★★★☆☆  
   sandbox 弹窗（#29200）、内存压力（#30050）、以及 app 无法启动（#29040）等问题主要影响 Windows 用户，负面反馈集中。

7. **认证与账户恢复** ★★★☆☆  
   遗留电话号码验证（#25749）无更换途径，导致部分用户账号被锁定；macOS 上还有 daemon socket 路径限制问题（#27765）。

8. **后台任务与资源浪费** ★★★☆☆  
   轮询触发完整历史（#13733）、持久化 `function_call` 超时（#29773）等暴露了资源使用不够经济。

---

*以上日报基于 GitHub 公开数据自动生成，仅供社区参考。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，作为一名专注于 AI 开发工具的技术分析师，我根据今天（2026-06-26）提供的 GitHub 数据，为您整理了 Gemini CLI 社区动态日报。

---

## Gemini CLI 社区动态日报 | 2026-06-26

### 1. 今日速览

今天社区聚焦于**Agent 可靠性与安全加固**。`v0.50.0-preview.1` 的发布引入了 Tool Registry 依赖注入，标志着架构层面的进化。安全方面，针对 **CVE-2026-48931** 的 OAuth 连接池修复（[#28103](https://github.com/google-gemini/gemini-cli/pull/28103)）进入审查阶段。社区层面，围绕 “Auto Memory” 系统的隐私与可靠性争议（[#26516](https://github.com/google-gemini/gemini-cli/issues/26516) 系列）持续发酵。**Agent 通用挂起**（[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)）和**子代理误报成功**（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)）仍是开发者最严重的阻塞性痛点。

### 2. 版本发布

过去 24 小时内有 3 个版本上线：

*   **v0.51.0-nightly.20260626**：主要修复了 `no_proxy` 环境变量的测试兼容性问题，并持续加固 NPM 发布流水线（修复 `gb14416447`）。
*   **v0.50.0-preview.1**：重要里程碑预览版。核心变化包括 **Tool Registry 依赖注入（DI）** 架构改造，以及修复了 Release 验证中工作区二进制文件相互遮蔽（Shadowing）的问题。
*   **v0.49.0**：正式版稳定更新，主要引入了 Dependabot 冷却期机制，以防止依赖更新过于频繁。

### 3. 社区热点 Issues（Top 10）

以下是根据评论活跃度、点赞数和影响面筛选出的最值得关注的 Issue：

1.  **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) [P1/bug] 子代理在达到 MAX_TURNS 后错误上报为 GOAL 成功**
    *   **为什么重要**：这是最危险的逻辑 Bug 之一。`codebase_investigator` 等子代理在超时中断后，向用户报喜不报忧，报告 `status: "success"`，导致用户误以为任务完成。
    *   **社区反应**：8 条深度评论，正在讨论如何区分“真实成功”与“中断后错误终止”。

2.  **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) [P1/bug] 通用 Agent（Generalist Agent）永久挂起**
    *   **为什么重要**：当 CLI 转交给 Generalist Agent 时，即使只是创建文件夹等简单任务，也会永久挂起（等待超 1 小时）。用户必须明确指示“不要使用子代理”才能绕过。
    *   **社区反应**：8👍，是目前点赞数最高的 Bug 之一，严重破坏了 CLI 的信任度。

3.  **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) [P1/bug] Shell 命令执行完毕后被错误阻塞 “Waiting input”**
    *   **为什么重要**：CLI 执行完简单命令（如 `ls`, `git status`）后，状态显示仍在等待用户输入，导致流程卡死。这严重影响了日常的 Shell 交互体验。
    *   **社区反应**：3👍，属于高频触发的回归性 Bug。

4.  **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) [P2/bug] Gemini 不会主动使用注册的技能和子代理**
    *   **为什么重要**：用户注册了大量 Gradle、Git 等技能，但模型除非收到明确指令，否则完全忽视这些技能。这引发了社区对“智能调度”能力的质疑。
    *   **社区反应**：6 条评论，普遍认为需要大幅改进模型对工具注册表的检索与匹配策略。

5.  **[#26516 系列](https://github.com/google-gemini/gemini-cli/issues/26516) [P2/bug] Auto Memory 系统系列问题**
    *   **为什么重要**：这是一个组合拳：`#26525` 指出数据脱敏发生在内容传输到模型之后（有泄露风险）；`#26522` 指出低价值会话会被无限重试；`#26523` 指出无效 Patch 被静默跳过。新 Memory 系统的落地过程可谓状况百出。
    *   **社区反应**：开发者对新引入的自动记忆功能安全性普遍表示担忧。

6.  **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) [P2/enhancement] 零依赖 OS 沙箱与执行后意图路由**
    *   **为什么重要**：Gemini 模型原生高度适配 Bash 操作。此 Issue 探讨如何在保障用户安全的前提下，利用模型的这种“原生亲和力”，而非限制它。
    *   **社区反应**：8 条评论，技术含量较高，触及了 AI CLI 工具安全与执行效率的核心矛盾。

7.  **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) [P2/epic] AST 感知的文件读取与搜索**
    *   **为什么重要**：试图用语法分析（AST）代替逐行读取，在单次调用中精确读取方法边界，减少 Token 消耗和因错位读取导致的幻觉。
    *   **社区反应**：7 条评论，普遍认为这是处理大型代码库的必经之路。

8.  **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) [P2/bug] 工具超过 128 个时触发 400 错误**
    *   **为什么重要**：这是扩展性问题。随着 MCP 和自定义技能的丰富，工具数量激增导致 API 拒绝服务。社区期待更智能的按需加载或范围裁剪。
    *   **社区反应**：3 条评论，提报人明确指出模型应更智能地“限制”当前可用工具范围。

9.  **[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) [P2/bug] v0.33.0 后子代理无视“禁用”权限设置**
    *   **为什么重要**：用户在配置中明确禁用了 Agent 模式，且仅期望使用 MCP 功能，但升级后子代理（如 Generalist）依然被调用。
    *   **社区反应**：尽管评论数不多，但这属于严重的安全与控制权倒退。

10. **[#22598](https://github.com/google-gemini/gemini-cli/issues/22598) [P3/feature] 子代理轨迹应支持 `/chat share` 分享**
    *   **为什么重要**：目前子代理的执行过程无法通过分享链接查看，导致开发和评测团队无法有效地复盘 Agent 工作流。
    *   **社区反应**：1👍，但代表了开发者对“Agent 可观测性”的强烈需求。

### 4. 重要 PR 进展（Top 10）

筛选了功能价值高、修复关键 Bug 或引入重要架构变化的 PR：

1.  **[#28103](https://github.com/google-gemini/gemini-cli/pull/28103) [Security] 修复 OAuth Socket 重用问题（CVE-2026-48931）**
    *   **内容**：修复了 `http.Agent` 的 keep-alive socket 在 OAuth Token 交换过程中的请求队列毒化漏洞。适配了 Node.js 24.17.0、22.23.0 等新版本的安全机制。
    *   **评价**：企业级安全性的关键补丁。

2.  **[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) [Core] 修复历史记录的“思维泄露（Thought Leakage）”**
    *   **内容**：过滤掉模型内部独白被序列化至明文对话历史的问题，防止模型在后续轮次中读取到自己的“内心戏”从而陷入无限循环。
    *   **评价**：对模型输出质量和稳定性有重大积极影响。

3.  **[#27850](https://github.com/google-gemini/gemini-cli/pull/27850) [Core] MCP 图片 MIME 类型嗅探修复**
    *   **内容**：针对 MCP 服务器上报错误的 MIME 类型（如 WebP 报为 PNG），通过二进制签名修正，确保模型正确处理图片。
    *   **评价**：修复了 MCP 生态中一个非常隐蔽的互操作 Bug。

4.  **[#27845](https://github.com/google-gemini/gemini-cli/pull/27845) [UX] 交互式文件夹信任提示**
    *   **内容**：将“信任此文件夹”的提示从初始化后移至鉴权之前，并支持信任后自动重载本地配置。
    *   **评价**：优化了安全交互流程，解决了“未经工作区确认就尝试加载配置”的问题。

5.  **[#27461](https://github.com/google-gemini/gemini-cli/pull/27461) [Core] 抑制 PTY 调整大小时的 EBADF 错误**
    *   **内容**：修复了终端 resize 时由于进程正在退出导致的崩溃问题。这是 UI 布局重构后高频触发的问题。
    *   **评价**：显著提升了颜值党用户的 UI 交互稳定性。

6.  **[#27848](https://github.com/google-gemini/gemini-cli/pull/27848) [CLI] 新增 `gemini models` 命令**
    *   **内容**：允许用户通过 CLI 列出当前支持的 Gemini 模型、上下文窗口和层级（Pro/Flash），支持 JSON 输出。
    *   **评价**：提升了 CLI 的可探索性和开发者体验，无需再查文档。

7.  **[#28013](https://github.com/google-gemini/gemini-cli/pull/28013) [Prompts] 修复 `$` 模式替换污染**
    *   **内容**：修复了 `applySubstitutions` 函数中，由于技能或子代理描述包含 `$` 字符（如 `$$`, `$&`, `$n`）导致的字符串替换异常。
    *   **评价**：修复了一个隐蔽的 Prompt Templating 引擎 Bug，避免了代码被错误解释。

8.  **[#28153](https://github.com/google-gemini/gemini-cli/pull/28153) [Core] 忽略会话重置后过时的 `update_topic` 调用**
    *   **内容**：防止模型在用户执行 `/clear` 前后发出的异步 `update_topic` 调用对新的会话状态造成污染。
    *   **评价**：修复了会话状态管理中的竞态条件。

9.  **[#28012](https://github.com/google-gemini/gemini-cli/pull/28012) [CLI] 修复 WSL 下 Footer 分支名不更新**
    *   **内容**：通过主动轮询 Git 状态，解决了 WSL 挂载 Windows 驱动区内因缺乏 `fs.watch` 事件导致 Footer 分支名称卡死的问题。
    *   **评价**：修复了 Windows 平台用户的 Git 工作流可用性问题。

10. **[#28149](https://github.com/google-gemini/gemini-cli/pull/28149) [Agent] 技能资源列表支持 .gitignore**
    *   **内容**：激活技能时，将技能文件夹结构暴露给模型前，现在会过滤掉 `.gitignore` 和 `.geminiignore` 中配置的文件。
    *   **评价**：有效减少了发送给模型的无效 Token，避免了 Side-Effect 文件混淆 Agent。

### 5. 功能需求趋势

综合今日数据，社区对未来功能的需求集中在以下方向：

*   **Agent 深度自主性**：从“能执行”转向“会思考”。社区强烈要求 AST 感知文件处理（[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)）、原生 Bash 沙箱（[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)）和阻止破坏性行为（[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)）。
*   **Agent 可观测性**：开发者需要“Agent 调试器”。Component Eval 体系（[#24353](https://github.com/google-gemini/gemini-cli/issues/24353)）和轨迹分享（[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)）是当前最迫切的调试需求。
*   **企业级安全与治理**：安全修复（CVE）、数据脱敏（`Auto Memory`）、MCP 输入封装（[#27979](https://github.com/google-gemini/gemini-cli/pull/27979)）以及共享责任模型文档（[#27224](https://github.com/google-gemini/gemini-cli/pull/27224)）表明 CLI 正经历企业级安全洗礼。
*   **平台扩展与生态**：从 `gemini models` 命令到 Vertex AI 官方端点路由（[#28145](https://github.com/google-gemini/gemini-cli/pull/28145)），用户对非谷歌云原生环境的诉求正在被认真对待。

### 6. 开发者关注点

从 Issue 和 PR 中反馈的痛点来看，开发者的体验主要被以下高频问题困扰：

*   **Agent 不可靠性**：**挂起**（[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)、[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)）和**误报状态**（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)）是最致命的“信任杀手”。开发者宁可得到明确的失败，也无法接受永久卡死或虚假成功。
*   **配置与隐私意外**：Agent **无视用户配置**（[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)、[#22267](https://github.com/google-gemini/gemini-cli/issues/22267)）和 Auto Memory 的**先上传后脱敏**设计（[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)）是当前最让用户感到“失控”的点。
*   **工具注册表拥塞**：超过 128 个工具就报错（[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)），且工具实际调用率低（[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)），表明工具匹配与裁剪算法亟待优化。
*   **跨平台兼容性**：Wayland 浏览器子代理失败（[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)）和 WSL 文件同步问题（[#28012](https://github.com/google-gemini/gemini-cli/pull/28012)）是 Linux 和 Windows 用户的持续痛点。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-06-26

---

## 1. 今日速览

- **v1.0.66-0 正式发布**，重点关注 MCP 服务器的图形化管理（新增启停开关），并引入实验性的响应预算控制与 OpenTelemetry 导出，企业级管控能力进一步增强。
- **会话连续性 Bug 仍在发酵**，“恢复 Session 后模型列表显示未认证”（#3596 / #3680）和“Session 记录丢失”（#3931）问题持续引发高热度讨论，成为今日社区最集中的痛点。
- **插件/Skills 生态迎来波折**，严格的参数格式校验（#3929）导致部分已有技能无法加载，社区对新版本的向前兼容性提出质疑。

---

## 2. 版本发布：v1.0.66-0

📦 **[Release: v1.0.66-0](github/copilot-cli Releases)**

**新增亮点：**

- **MCP 服务器管理增强**：在 `/mcp show` 列表视图中新增“启用/禁用”开关，无需记忆命令行即可控制 MCP 服务器的运行状态（回应 #2956 / #3564 社区诉求）。
- **响应预算控制（实验性）**：新增 CLI 设置选项，允许用户对 Token 消耗进行预算约束，为精细化成本管理铺垫基础设施。
- **可观测性升级**：托管设置现在可以配置 OpenTelemetry 导出，方便企业集中运维监控。
- **OAuth 远程 MCP 自动恢复**：解决了 OAuth 认证的 MCP 远程服务器在会话中期 Token 过期后无法自动重连的问题，显著提升远程 MCP 稳定性。

---

## 3. 社区热点 Issues（Top 10）

### 🔴 #700 ［功能请求］提供一个列出所有支持模型的方法
- **评论数：14 | 👍：4 | 状态：OPEN**
- **分析**：该 Issue 自 2025 年 12 月提出至今仍被反复提及，社区普遍认为 CLI 应像 IDE 插件一样提供 `copilot --list-models` 来查看可用模型及乘数，以便做模型选择决策。
- [GitHub 链接](github/copilot-cli Issue #700)

### 🔴 #2643 ［Bug］`preToolUse` 静默重写命令依然弹出确认对话框
- **评论数：12 | 👍：2 | 状态：OPEN**
- **分析**：即使插件 Hook 通过 `updatedInput` 重写命令并声明 `permissionDecision: allow`，CLI 仍然向用户弹确认框。完全自动化的工作流因此中断，是 Agent 插件生态成熟路上的关键阻塞点。
- [GitHub 链接](github/copilot-cli Issue #2643)

### 🔴 #3596 / #3680 ［Bug］恢复 Session 后 `/model` 命令报 "Not authenticated"
- **评论数：7+1 | 👍：11+0 | 状态：OPEN**
- **分析**：这是今日社区反应最集中的 Bug 之一。用户通过 `--resume` 恢复前一天的会话后，无法用 `/model` 切换模型。所有其他功能正常，唯独模型列表加载失败，严重打消持续作业的积极性。
- [GitHub 链接 #3596](github/copilot-cli Issue #3596) / [#3680](github/copilot-cli Issue #3680)

### 🔴 #3501 ［Bug］Windows 终端滚动条导致文本布局错位
- **评论数：5 | 👍：9 | 状态：OPEN**
- **分析**：滚动条引入后，Windows Terminal 和 Console Host 下的文本渲染出现偏移。视觉效果 Bug 虽然不影响功能，但极大降低了 TUI 的专业感，且 CLI 自身无法通过指令修复。
- [GitHub 链接](github/copilot-cli Issue #3501)

### 🟠 #3534 ［Bug］WSL2 (ARM64) 下 `/copy` 命令因 `cmd.exe` 引号问题失败
- **评论数：4 | 👍：4 | 状态：OPEN**
- **分析**：在 ARM64 架构的 WSL2 环境中，`clip.exe` 因为 shell 引号处理不当报 `exit code 1`。这是一个典型的跨平台兼容性漏洞，直接影响 ARM 设备的开发体验。
- [GitHub 链接](github/copilot-cli Issue #3534)

### 🟠 #3636 ［Bug］企业 VPN 下语音模式无法启用
- **评论数：3 | 👍：5 | 状态：OPEN**
- **分析**：因企业 VPN/代理导致 CLI 无法拉取语音（STT）模型目录，语音模式完全不可用。这暴露了 CLI 缺乏对企业网络隔离环境的通用适配策略，是进入大型企业的硬性门槛。
- [GitHub 链接](github/copilot-cli Issue #3636)

### 🟠 #3929 ［Bug］Skills `argument-hint` 格式校验错误
- **评论数：1 | 👍：0 | 状态：OPEN**
- **分析**：新版本对 `argument-hint` 字段进行了严格类型校验（要求字符串），导致 `[regression directory]` 这种在 VS Code 和 Claude Code 中合法使用的语法在 Copilot CLI 中报错，社区吐槽向前兼容性不足。
- [GitHub 链接](github/copilot-cli Issue #3929)

### 🟠 #3935 ［Bug］VS Code 终端下用户主题被覆盖为浅色主题
- **评论数：0 | 👍：0 | 状态：OPEN**
- **分析**：自 v1.0.64 起，VS Code 内置终端启动 Copilot CLI 后强制显示浅色主题，无视用户终端主题设置。对于黑/深色主题用户来说属于可感知的体验降级，需要紧急修复。
- [GitHub 链接](github/copilot-cli Issue #3935)

### 🟠 #3933 ［Bug］自动模式（Autopilot）每次请求后自动退出
- **评论数：0 | 👍：0 | 状态：OPEN**
- **分析**：自动模式原本可以保持连续的对话工作流，现在每次请求完成后自动退出（颜色也从绿色变为紫色）。重度用户需要反复手动进入，破坏 Agent 闭环体验。
- [GitHub 链接](github/copilot-cli Issue #3933)

### 🟠 #3931 ［Bug］Session 在哪里？会话记录丢失或不可恢复
- **评论数：0 | 👍：0 | 状态：OPEN**
- **分析**：用户反映前一天的重要 Session 无法通过 `/resume` 恢复，甚至在列表中都找不到。对于依赖 CLI 进行长期项目的开发者来说，Session 的稳定性是核心信任基石，此 Bug 情绪反应烈度较高。
- [GitHub 链接](github/copilot-cli Issue #3931)

---

## 4. 重要 PR 进展

今日 PR 数量较少，仅有 1 个处于开放状态。

### 📌 #3928 ｜ 添加 `.gitignore` 和 settings 配置
- **作者：** tpsaint
- **状态：** OPEN
- **分析：** 该 PR 旨在完善 Copilot CLI 的项目初始化流程，增加 `.gitignore` 和初始配置文件模板。属于基础设施层的小幅迭代。
- [GitHub 链接](github/copilot-cli PR #3928)

> 注：今日无新的合并且社区修复类 PR 活跃度较低，推测团队正集中精力处理 v1.0.66-0 发布后的稳定性收尾任务。

---

## 5. 功能需求趋势

### 趋势一：MCP 全生命周期管理
从简单的“添加/删除”到“启用/禁用”（#3564），再到“策略拦截提示”（#3934）、“指令遵循”（#1579），社区对 MCP 服务器的控制力要求持续提升。v1.0.66-0 的启停开关是对此的快速回应，但策略层和可观测性（OpenTelemetry）仍需完善。

### 趋势二：模型透明度与配额可感知
用户希望 CLI 提供“列出所有可用模型”（#700）和“查看月度配额使用”（#3932）两种核心能力。这与 IDE 插件的体验对齐，反映出社区越来越关注成本控制（AIC 用量）和模型选择的自主权。

### 趋势三：企业级标准适配
三项并列需求：受限制网络下的功能可用性（#3636 VPN）、中心化配置推送（#3909 Enterprise Settings）、环境变量隔离（#3925 LD_LIBRARY_PATH）。Copilot CLI 正在从“个人开发者玩具”向“企业开发标配”演进。

### 趋势四：插件/Agent 生态的体验一致性
用户期待 Copilot CLI 的插件系统能与 VS Code Agent 和 Claude Code 保持同等级别的体验——静默执行（#2643）、宽松的语法兼容（#3929）、更新后技能持久化（#3938）。这几个问题正是“看起来功能有了，用起来感觉不对”的缩影。

---

## 6. 开发者关注点（痛点与高频反馈）

### 痛点一：Session 的脆弱性
**表现**：`--resume` 后 `/model` 失效（#3596）、Session 从列表中消失（#3931）、Autopilot 自动退出（#3933）。
**影响**：重度用户的核心工作流（长时间 Agent 对话）被彻底打断，信任度下降。

### 痛点二：Windows & ARM 平台的二等公民感
**表现**：滚动条错位（#3501）、WSL2 ARM64 剪贴板失败（#3534）、VS Code 终端浅色主题强制覆盖（#3935）。
**影响**：虽然不是核心逻辑 Bug，但这些 UI/UX 瑕疵让非 macOS 用户产生“被忽略”的印象。

### 痛点三：网络层适配缺失
**表现**：企业 VPN 下语音不可用（#3636）、AppImage 的 `LD_LIBRARY_PATH` 泄漏破坏 git HTTPS 操作（#3925）。
**影响**：直接阻断产品在企业网络内的落地，属于功能可用性层面的致命伤。

### 痛点四：更新机制不稳健
**表现**：`autoUpdate: false` 配置在 v1.0.4 之后被忽略（#2615）、更新导致全球用户 Skills 丢失（#3938）。
**影响**：开发者失去对本地环境变更的控制感，面对更新产生恐惧心理。

---

*数据来源：GitHub `github/copilot-cli`，采集范围：2026-06-25 至 2026-06-26。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-06-26

## 今日速览

截至今日，Kimi Code CLI 社区没有新版本发布或 PR 合并，但新增了两个值得关注的 bug 报告：一个涉及 MCP 工具数量过多时的兼容问题，另一个是终端界面持续抖动、反复重绘的严重 UI 问题，两者都可能影响用户实际体验，官方尚未回应。

## 版本发布

（无新版本发布，该部分省略）

## 社区热点 Issues

### 1. #2475 – [bug] MCP tools
- **作者**：ptyll  
- **标签**：bug  
- **状态**：Open  
- **链接**：[MoonshotAI/kimi-cli Issue #2475](https://github.com/MoonshotAI/kimi-cli/issues/2475)  
- **摘要**：用户配置了包含 212 个工具的 MCP server，在 Kimi Code v0.19.2 上使用时出现异常。  
- **为何重要**：MCP 工具生态正快速扩展，大量工具的支持能力直接关系到 Kimi Code CLI 在复杂工作流中的实用性。该问题可能暴露了工具注册、上下文或请求处理的性能瓶颈。社区暂无讨论跟进，但若影响广泛，可能成为后续版本优化的关键参考。

### 2. #2474 – [bug] 界面抖动、莫名其妙重新从头渲染整个对话
- **作者**：yudichimiantiao  
- **标签**：bug  
- **状态**：Open  
- **链接**：[MoonshotAI/kimi-cli Issue #2474](https://github.com/MoonshotAI/kimi-cli/issues/2474)  
- **摘要**：在 Linux 系统上使用 Kimi Code CLI 时，终端界面反复抖动，并触发整个对话从头重新渲染，严重影响操作。  
- **为何重要**：终端 UI 的稳定性是核心体验之一，该问题直接导致用户无法正常使用。推测可能与终端重绘逻辑、缓冲区管理或插件兼容性有关。Linux 是开发者常用平台，该问题的修复优先级应当较高。

## 重要 PR 进展

（过去 24 小时内无新 Pull Request 更新，暂无可汇报的 PR 进展。）

## 功能需求趋势

由于今日仅有两份 bug 报告，暂未收到明确的新功能请求。但从问题内容可间接看出社区关注的方向：

- **MCP 工具的扩展性**：单个 server 提供 200+ 工具的场景已出现，用户期望 CLI 能稳定处理大规模工具集，这暗示了 **大规模工具集成** 是未来的潜在需求。
- **终端渲染稳定性**：对话重绘抖动问题表明用户对 **终端交互体验** 的依赖性很强，任何 UI 层面的回退或异常都可能导致工作流中断。
- **最新模型支持**：用户已在尝试 K2.7 等新模型，社区对 **前沿模型的兼容性** 保持敏感，后续可能持续期望对新模型的快速适配。

## 开发者关注点

综合今日反馈，开发者最关注的问题集中在：

1. **MCP 大规模工具支撑**：当工具数量突破上百时，注册、路由、上下文拼装等环节是否会出现瓶颈，是用户实际操作中遇到的第一道坎。
2. **终端 UI 重绘异常**：界面抖动与不自主的全量重绘严重打断工作流，且出现在 Linux 平台，可能是跨终端兼容性问题，需要开发团队优先排查。
3. **稳定性优先于功能** ：两个 issue 均为 bug 而非 feature request，反映出用户当前更希望版本稳定，特别是核心的交互与扩展接口不应出现失效或异常反复。

> 官方尚未对上述 issue 作出回复，社区主动发起的讨论也暂未出现。建议关注后续评论与补丁动向。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-06-26

## 今日速览
- OpenCode 发布 v1.17.11，核心新增**会话快照与回退控制**功能，允许将对话状态连同文件变更一起回滚。
- **Windows 平台崩溃问题（#33742）** 仍是社区焦点，v1.17.10 引发的 Bun segfault 已累积 45 条讨论，新版本未明确修复，但相关 Error 诊断 PR（#33996）已提交。
- 多领域 PR 活跃：MCP 服务骨架搭建、SDK 暴露活跃会话接口、v2 布局 Agent 选择器修复等重要变更正在推进。

## 版本发布
### v1.17.11
**Core 改进：**
- **会话快照与回退控制**：可将整个会话回滚到之前的某条消息，包括当时的所有文件变更，大幅提升对话管理灵活性。
- **Bug 修复**：始终打印 MCP OAuth URL，确保浏览器无法自动打开时仍可手动完成登录。

**Desktop 改进：**
- 添加 Chrome 风格的窗口控制（原文 `Add Chrome-sty...`，推测为窗口装饰或标签页相关优化）。

[查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.11)

## 社区热点 Issues
1. **#33742 – Windows 平台 v1.17.10 崩溃（Bun segfault）**  
   Windows 用户升级后频繁出现原生段错误，降至 v1.17.9 恢复正常。45 条评论、42 👍，属当前最高优先级回归 Bug。  
   [链接](https://github.com/anomalyco/opencode/issues/33742)

2. **#33815 – 更新至 v1.17.10 后出现 Internal Server Error 且响应极慢**  
   用户反馈更新后几乎无法使用，即使简单的 "Hi" 也要等待很久，可能与 `#33742` 有关。  
   [链接](https://github.com/anomalyco/opencode/issues/33815)

3. **#33903 – 相同环境反复出现 Effect.tryPromise 错误**  
   卸载重装、切换版本及网络环境均无法解决。开发者在对应 PR（#33996）中改进错误传递以便定位。  
   [链接](https://github.com/anomalyco/opencode/issues/33903)

4. **#15676 – Bun 在输入过程中突然崩溃**  
   提供截图但无法复制错误内容。Windows 上多次复现，至今未彻底解决。  
   [链接](https://github.com/anomalyco/opencode/issues/15676)

5. **#32821 – GLM-5.2 通过 OpenCode Go 调用返回 400**  
   `messages.content` 被错误序列化为数组格式，模型期望纯文本字符串，反映多模型适配仍有 gap。  
   [链接](https://github.com/anomalyco/opencode/issues/32821)

6. **#11314 – 要求可配置上下文压缩阈值**  
   目前 75% 硬编码触发压缩，社区希望支持自定义百分比。获得 32 👍、15 条讨论，是配置灵活性的代表需求。  
   [链接](https://github.com/anomalyco/opencode/issues/11314)

7. **#30360 – v2 布局中 Build/Plan Agent 选择器丢失**  
   新布局下 agent picker 被隐藏，影响多 agent 工作流。对应修复 PR #30352 已提交。  
   [链接](https://github.com/anomalyco/opencode/issues/30360)

8. **#28656 – CentOS 7 上 TUI 代码部分渲染为空白**  
   LLM 回复中的代码区域不可见，仅能复制到其他地方查看，属于终端兼容性问题。  
   [链接](https://github.com/anomalyco/opencode/issues/28656)

9. **#34003 – sdk-next 需要持久的终端运行失败事件**  
   当前 session 因非 provider 错误失败时仅简单记录日志，嵌入式消费者无法获知 final 状态，要求增加持久化事件。  
   [链接](https://github.com/anomalyco/opencode/issues/34003)

10. **#33866 – 加载 skills 配置时使用了旧版 `opencode.jsonc` 语法**  
    中文用户反映 build agent 自动生成的配置仍采用数组语法，而新版已改为对象结构，导致 skills 无法加载。  
    [链接](https://github.com/anomalyco/opencode/issues/33866)

## 重要 PR 进展
1. **#33988 – 搭建 MCP 服务基础骨架（`MCP.Service`）**  
   新增 Location 作用域下的服务层接口，包括连接/断开/超时等基础框架。  
   [链接](https://github.com/anomalyco/opencode/pull/33988)

2. **#33991 – SDK 暴露活跃会话查询 API**  
   添加 `client.sessions.active()` 方法，用于 TUI 及其他客户端获取当前前台运行中的 session。  
   [链接](https://github.com/anomalyco/opencode/pull/33991)

3. **#33880 – 使用 dnd-kit 替换自定义标签页拖拽处理**  
   重构桌面端标签拖拽状态机，改用 `@dnd-kit/solid`，减少维护成本并保留触屏与动画能力。  
   [链接](https://github.com/anomalyco/opencode/pull/33880)

4. **#33996 – 保留 TUI 渲染器初始化原始错误**  
   修复 `Effect.tryPromise` 吞掉底层错误（如原生库加载失败）的问题，直接关联 `#33903` 的排查。  
   [链接](https://github.com/anomalyco/opencode/pull/33996)

5. **#33990 – 暂停隐藏终端页面的渲染器**  
   终端面板关闭后卸载渲染器实例，防止后台资源泄漏，重新打开时自动重连。  
   [链接](https://github.com/anomalyco/opencode/pull/33990)

6. **#33994 – 桌面端按服务器粒度自动批准权限**  
   权限自动批准从会话/目录级别改为服务器级别，同一 server 的后续会话不再重复弹窗。  
   [链接](https://github.com/anomalyco/opencode/pull/33994)

7. **#30352 – 修复 v2 布局中 Build/Plan Agent 选择器隐藏问题**  
   移除了不必要的功能开关 gating，使 agent picker 在新布局下正常显示。  
   [链接](https://github.com/anomalyco/opencode/pull/30352)

8. **#33860 – 细化会话 UI 样式（V2 设计令牌）**  
   更新 markdown/时间线区域的色板、边框、排版，并改进行内代码路径检测。  
   [链接](https://github.com/anomalyco/opencode/pull/33860)

9. **#33892 – 限制会话 diff 摘要负载上限**  
   对工作区 diff 进行大小封顶，防止巨大的文件变更导致 session 摘要膨胀与性能问题。  
   [链接](https://github.com/anomalyco/opencode/pull/33892)

10. **#29281 – Windows 上防止 `process.exit()` 杀死父终端**  
    通过改进退出逻辑避免 OpenCode 关闭时连带退出 PowerShell/cmd 窗口。  
    [链接](https://github.com/anomalyco/opencode/pull/29281)

## 功能需求趋势
- **配置细粒度增强**：上下文压缩阈值（#11314）、压缩模型选择（#11930）、copy-on-select 开关（#4751）等“可调式”需求高频出现。
- **多模型与 Provider 扩展**：GLM、Vertex AI、Claude Opus 4.6 for Copilot、自定义 Anthropic 兼容 provider 等支持请求持续增长。
- **UI/UX 精细化**：v2 布局功能补齐（agent picker、session 时间戳）、TUI 鼠标行为改进、统一设计令牌。
- **SDK 与嵌入式能力**：sdk-next 系列的 session 元数据、活跃查询、配置注入、失败事件持久化是当前迭代重点。
- **稳定性与兼容性**：Windows 平台（Bun segfault）、旧终端（CentOS 7）、iTerm2 鼠标冲突等平台适配仍是重要改进方向。

## 开发者关注点
- **Windows 稳定性仍是第一痛点**：#33742 及其子问题（#33815、#33903）说明升级即崩溃的现象严重影响了 Windows 用户的信心，社区呼吁尽快修复 Bun 原生层问题。
- **升级回退成为常态**：由于 v1.17.10 引入严重回归，许多用户选择停留在 v1.17.9 或回滚，新版本 v1.17.11 未明确提及 Windows 修复，观望情绪浓。
- **v2 布局过渡期体验不完整**：agent picker 缺失等关键功能 gaps（#30360）迫使用户在旧版与新布局间反复切换。
- **自动配置与文档滞后**：skills 语法变更后自动生成仍输出旧格式（#33866），自定义 provider 缺少文档（#34004），增加了新用户上手难度。
- **会话管理复杂度上升**：多 agent 场景下 session 隔离（#11802）、时间戳显示（#16341）、失败事件通知（#34003）等需求说明用户正在构建更复杂的工作流，对会话基建提出了更高要求。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，各位开发者，早上好！

这里是 2026 年 6 月 26 日的 Pi 社区动态日报。我是你们的技术分析师，今天由我来为大家梳理 Pi 项目的最新进展。

---

## 📰 今日速览

昨日 Pi 社区热度主要在围绕 **`openai-codex` 连接可靠性**这一顽固问题进行深度讨论（#4945）。同时，**TUI 渲染体验**的优化成为多个 Issue 和 PR 的焦点，包括修复滚动跳转、自定义组件渲染顺序等问题。此外，社区对 **RPC 接口**与**扩展生态**的完善呼声较高，`pi-orchestrator` 实验性功能的出现也预示着项目在架构层面的新探索。

## 🚀 版本发布

昨日无新版本发布。

## 🔥 社区热点 Issues

1.  **#4945: `openai-codex` 连接可靠性问题 | 评论: 71 | 👍: 30**
    - **摘要**: 用户反馈使用 `openai-codex` / `gpt-5.5` 时，TUI 界面频繁卡在 `Working...` 状态，无法正常输出流文本或调用工具，只能通过强制退出恢复。该问题已持续数天，影响广泛。
    - **为什么重要**: 这是目前社区影响最大、讨论最激烈的 Bug，直接关系到核心编码助手功能的可用性。大量用户参与讨论，点赞数极高，表明这是一个普遍且严重的痛点。
    - **链接**: [#4945](https://github.com/earendil-works/pi/issues/4945)

2.  **#5825: 流式 Markdown 渲染强制滚动至底部 | 评论: 31 | 👍: 0**
    - **摘要**: 当 AI 以 Markdown 格式流式输出时，如果用户向上滚动阅读历史内容，TUI 会强制将视图滚回底部，打断阅读体验。该问题在开启 `clear on shrink` 设置时出现。
    - **为什么重要**: 这是一个严重影响用户阅读体验的交互问题，尤其对于长文本输出。虽然有临时解决方案（关闭设置），但社区期望更智能的滚动策略。
    - **链接**: [#5825](https://github.com/earendil-works/pi/issues/5825)

3.  **#5886: AgentSession 结算/续期及助手回合生命周期 Bug | 评论: 3 | 👍: 2**
    - **摘要**: 知名开发者 mitsuhiko 创建了此元问题，汇总了一类在会话结束后，后续逻辑尝试从未完成的对话记录中恢复 Agent 而导致的各种问题。
    - **为什么重要**: 虽评论不多，但由核心贡献者提出，指出了 Agent 核心生命周期管理中一个系统性缺陷，可能引发多种偶发性的会话异常。
    - **链接**: [#5886](https://github.com/earendil-works/pi/issues/5886)

4.  **#6050: TUI 完整重绘会清除终端回滚缓冲区 | 评论: 10 | 👍: 0**
    - **摘要**: 在交互模式下，Pi 的完整界面重绘会导致终端滚动条跳转到聊天开头，丢失之前的会话历史视图。
    - **为什么重要**: 与 #5825 类似，都属于 TUI 渲染的可用性问题。频繁的视图跳转会严重干扰用户查阅对话历史，尤其是在长会话中。
    - **链接**: [#6050](https://github.com/earendil-works/pi/issues/6050)

5.  **#5595: `openai-completions` 的 `maxTokens` 参数未透传 | 评论: 8 | 👍: 2**
    - **摘要**: 对于使用 `openai-completions` API 格式的提供商（如 Together.ai），配置的 `maxTokens` 参数未能传递给推理模型（如 DeepSeek v4 pro），导致输出被意外截断。
    - **为什么重要**: 该问题直接导致模型生成内容不完整，影响了与第三方 API 的兼容性。社区对此反馈积极，希望尽快修复。
    - **链接**: [#5595](https://github.com/earendil-works/pi/issues/5595)

6.  **#5989: Pi 更新破坏了 `pi-lovely-codex` 扩展 | 评论: 7 | 👍: 0**
    - **摘要**: 用户在升级 Pi 后，之前正常运行的 `@xl0/pi-lovely-codex` 扩展加载失败，提示 `Failed to load extension...`。此问题突显了扩展生态系统的稳定性挑战。
    - **为什么重要**: 这是对 Pi 扩展兼容性的一个警示。随着 Pi 核心的快速迭代，如何保证扩展的稳定性是一个关键挑战。
    - **链接**: [#5989](https://github.com/earendil-works/pi/issues/5989)

7.  **#6065: 建议发布单二进制可执行文件 | 评论: 3 | 👍: 0**
    - **摘要**: 用户建议 Pi 像 deno、esbuild 等工具一样，提供一个包含 Node.js 运行时的单文件二进制版本，以避免在不同项目中使用不同 Node.js 版本带来的依赖问题。
    - **为什么重要**: 这个需求代表了许多希望简化部署和消除环境差异的开发者心声，是提升开发者体验的重要方向。
    - **链接**: [#6065](https://github.com/earendil-works/pi/issues/6065)

8.  **#6002: `SessionManager.open()` 静默截断非会话文件 | 评论: 4 | 👍: 0**
    - **摘要**: 使用 `SessionManager.open()` 或 `--session <path>` 参数打开一个非会话文件（如 NDJSON 日志）时，会静默地将该文件内容截断并重写为空会话头，且无任何警告或备份。
    - **为什么重要**: 这是一个破坏性极强且不易察觉的 Bug。用户可能因操作失误导致重要数据文件被不可逆地损坏，安全隐患巨大。
    - **链接**: [#6002](https://github.com/earendil-works/pi/issues/6002)

9.  **#6061: MiniMax-M2.7-highspeed 上下文预算低于预期 | 评论: 4 | 👍: 0**
    - **摘要**: 使用内置 `minimax-cn` 提供商和 `MiniMax-M2.7-highspeed` 模型时，长对话会因为触发了约131k tokens 的上下文限制而失败，但这与模型声明的上下文窗口大小不符。
    - **为什么重要**: 这表明 Pi 在计算或传递上下文预算给特定模型时可能存在偏差，影响了与特定模型的兼容性和长会话的稳定性。
    - **链接**: [#6061](https://github.com/earendil-works/pi/issues/6061)

10. **#6052: 举报 `@hypabolic/pi-hypa` 包存在可疑行为 | 评论: 2 | 👍: 0**
    - **摘要**: 有用户举报，下载量达 20.3万/月的热门包 `@hypabolic/pi-hypa` 可能存在恶意或不安全行为。
    - **为什么重要**: 此举触及了包管理生态的安全信任问题。虽然评论不多，但其严重性不容忽视，需要项目维护者高度关注并进行审查。
    - **链接**: [#6052](https://github.com/earendil-works/pi/issues/6052)

## 🔧 重要 PR 进展

1.  **#6087: 移除 coding-agent 中硬编码的 RPC 超时 | 状态: 已合并**
    - **摘要**: 修复了 `RpcClient` 中 60 秒的硬编码等待上限，该问题会导致长时间运行的 MCP 工具调用失败。通过引入 `RpcClientOptions.waitTimeoutMs` 让调用方可配置。
    - **为什么重要**: 直接解决了影响 MCP 扩展和长时间执行工具的关键 Bug，提升了 Agent 的稳定性和扩展性。
    - **链接**: [#6087](https://github.com/earendil-works/pi/pull/6087)

2.  **#6078: 为 coding-agent 添加 `get_entries` 和 `get_tree` RPC 命令 | 状态: 打开**
    - **摘要**: 新增两个只读 RPC 命令，允许外部程序（如 IDE 插件、仪表盘）获取会话条目列表和会话树结构。
    - **为什么重要**: 这是构建 Pi 外部工具和 IDE 集成的基础设施，扩展了 Pi 的可编程性和集成能力。
    - **链接**: [#6078](https://github.com/earendil-works/pi/pull/6078)

3.  **#6084: 修复背景刷新时自定义组件的渲染顺序 | 状态: 已合并**
    - **摘要**: 解决了由于 JS `Map` 的 `delete` + `set` 操作导致自定义组件在后台定时刷新时渲染顺序混乱的问题，使用 `Map` 的 `set` 方法保留插入顺序。
    - **为什么重要**: 保证了扩展开发者创建的自定义 UI 组件稳定性和可预测性，修复了一个难以定位的 UI 渲染 Bug。
    - **链接**: [#6084](https://github.com/earendil-works/pi/pull/6084)

4.  **#6063: 扩展统计功能与 OSC 垃圾数据修复 | 状态: 已合并**
    - **摘要**: 作者 xl0 贡献了一个 PR，完成了扩展统计功能，并修复了退出 Pi 后在终端中输出 OSC 转义序列垃圾字符的问题。
    - **为什么重要**: 前者为管理和监控扩展提供了数据支持，后者清理了一个影响终端卫生的烦人 Bug。
    - **链接**: [#6063](https://github.com/earendil-works/pi/pull/6063)

5.  **#6081: 支持 `#RRGGBBAA` 格式的透明主题色 | 状态: 已合并**
    - **摘要**: 主题颜色现在支持 8 位十六进制格式，允许指定 Alpha 通道（透明度）。由于终端不支持真正的透明，颜色会在加载时与背景色进行混合。
    - **为什么重要**: 极大丰富了主题定制的可能性，允许用户和主题开发者创建更酷、更现代的外观。
    - **链接**: [#6081](https://github.com/earendil-works/pi/pull/6081)

6.  **#6064: 新增实验性 `pi-orchestrator` 包 | 状态: 打开**
    - **摘要**: 作者 cristinaponcela 添加了一个实验性的编排器，作为本地守护进程运行，可以通过 IPC 管理多个 Pi 实例的启动、列举等生命周期。
    - **为什么重要**: 这是一个具有前瞻性的架构变动，为实现多会话管理、后台服务和复杂工作流奠定了基础。
    - **链接**: [#6064](https://github.com/earendil-works/pi/pull/6064)

7.  **#5832: 改善提供商 HTTP 错误信息传递 | 状态: 打开**
    - **摘要**: 当 API 提供商返回非 2xx 响应时，Pi 之前会丢弃或混淆错误体中的详细信息。此 PR 旨在将底层 HTTP 错误信息透传给用户。
    - **为什么重要**: 显著提升了对 API 集成问题的诊断能力，帮助用户更快定位是配置问题、API 限流还是模型错误。
    - **链接**: [#5832](https://github.com/earendil-works/pi/pull/5832)

8.  **#5515: 添加 `alwaysTrust` 设置以跳过项目信任门控 | 状态: 已合并**
    - **摘要**: 新增一个配置项，允许用户完全禁用项目信任门控功能（默认禁用）。
    - **为什么重要**: 为高级用户或自动化场景提供了灵活性和便捷性，避免了在受信任的项目中反复进行权限确认。
    - **链接**: [#5515](https://github.com/earendil-works/pi/pull/5515)

9.  **#6074: 修复 coding-agent 中预提示压缩导致的继续问题 | 状态: 打开**
    - **摘要**: 修复了在 `continue` 模式下，由于预提示（pre-prompt）的压缩逻辑可能引发的问题。
    - **为什么重要**: 虽然描述简短，但“继续”模式是 Agent 核心工作流，任何与此相关的 Bug 修复都能直接提升会话的连续性和准确性。
    - **链接**: [#6074](https://github.com/earendil-works/pi/pull/6074)

10. **#5270: 临时会话模型和思考层级选择 | 状态: 已合并**
    - **摘要**: 将会话内切换模型和思考层级的操作默认改为仅影响当前临时会话，除非显式传递 `{ persist: true }` 参数，防止误操作覆盖全局设置。
    - **为什么重要**: 这是一种细粒度的配置控制，解决了用户不慎修改全局默认设置的痛点，设计更人性化。
    - **链接**: [#5270](https://github.com/earendil-works/pi/pull/5270)

## 📈 功能需求趋势

从最新 Issues 中，可以看出社区最关注以下几个功能方向：

1.  **IDE 和外部工具集成**: 大量需求集中在通过 **RPC 接口**暴露内部状态（如 #5810, #6078），以及提供**命令行自动补全**（#6086），旨在将 Pi 无缝嵌入更广泛的开发者工作流中。
2.  **终端体验与 TUI 稳定性**: 围绕 TUI 的 **滚动行为**（#5825, #6050）、**渲染稳定性**（#6058）和**终端适配**（#6073）的反馈和修复非常集中，是提升日常使用体验的核心。
3.  **新模型与提供商兼容性**: 持续关注对**思考模型**的深度支持（#6057, #6009），以及修复与特定第三方 API（如 Minimax、Together.ai）的兼容性问题（#5595, #6061），确保 Pi 能灵活接入最新、最多样的 AI 能力。
4.  **包管理与生态安全**: `@hypabolic/pi-hypa` 的举报（#6052）和扩展与核心兼容性问题（#5989）表明，社区对 **包安全和生态稳定性** 的担忧正在升温。
5.  **配置与可扩展性**: 对**主题深度定制**（#6081）、**会话配置持久化**（#5270）和**单二进制分发**（#6065）的需求，反映了用户希望 Pi 能更好地适应个人习惯和环境。

## 👀 开发者关注点

1.  **连接可靠性是首要之痛**: `openai-codex` 的卡死问题（#4945）是目前开发者反馈中最核心的痛点，急需修复。
2.  **UI/UX 体验细节亟待打磨**: “滚动被强制跳转”（#5825）、”视图被清空“（#6050）、”行太长导致崩溃“（#6058）这些是高频出现的负面体验反馈，严重影响了用户对 TUI 的信心和日常使用的流畅度。
3.  **扩展兼容性风险**: 核心版本的更新导致扩展“一言不合就挂掉”（#5989），开发者要求更稳定的 API 或更完善的向下兼容策略。
4.  **潜在数据安全风险**: `SessionManager.open()` 静默破坏文件（#6002）是一个极其危险的 Bug，开发者社区期望得到明确回应和紧急修复。
5.  **对“电量”和成本的精细控制**: 社区不满足于简单的模型切换，而是希望更精确地控制**思考层级**（#5270）、**上下文预算**（#6061）和**潜在的经济性模型**，这反映了从尝鲜到精打细算的成熟用户心态。

以上就是今天的 Pi 日报。总体来看，社区活跃度很高，项目正在快速迭代中，但也伴随着一些成长的阵痛。希望各位开发者能从中获益，我们明天见！

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，作为专注 AI 开发工具的技术分析师，我为您整理了 2026 年 6 月 26 日的 Qwen Code 社区动态日报。

---

# Qwen Code 社区日报 | 2026-06-26

## 今日速览

今日社区动态聚焦于 **Windows 平台的严重性能问题**（每次工具调用都会新建 PowerShell 进程导致内存泄漏）以及 **CI 安全与稳定性**（发现未隔离的运行环境导致跨 PR 污染）。同时，社区在交互改进（如 `@extension` 提及、`qwen update` 命令）和架构设计（如会话恢复、运行时上下文注入）方面有多项重要 PR 推进。

## 社区热点 Issues

1.  **[[Bug] 难绷逆天BUG：用一次工具开一个powershell 并且不再关闭 直到OOM](https://github.com/QwenLM/qwen-code/issues/5873)**
    *   **重要性：** 极高。这是一个严重影响 Windows 用户使用的性能 Bug，会导致内存耗尽。用户情绪激动，描述“百分百复现”，要求立刻修复。
    *   **社区反应：** 5 条评论，被标记为 P1 优先级。开发者已确认并分配 agent 处理。

2.  **[[Bug] Trojan:JS/ShaiWorm.DBA!MTB 病毒误报](https://github.com/QwenLM/qwen-code/issues/5055)**
    *   **重要性：** 高。安全问题是开发者的红线，VSCode 扩展的 `.vsix` 文件被 Windows Defender 误报为木马，会严重影响用户信任和下载安装。
    *   **社区反应：** 7 条评论。被标记为 P1 优先级，团队非常重视。

3.  **[[Bug] Tool calls with edits/write fail when using Qwen3 30b](https://github.com/QwenLM/qwen-code/issues/535)**
    *   **重要性：** 高。核心编辑功能在搭配特定模型（Qwen3 30b）时完全失效，错误信息为参数类型错误，直接破坏了工具的核心价值。
    *   **社区反应：** 12 条评论。是一个历史遗留的顽固 Bug，用户多次尝试均失败。

4.  **[[Bug] Streaming setup timeout after 64s](https://github.com/QwenLM/qwen-code/issues/239)**
    *   **重要性：** 中高。流式超时是普遍性痛点，影响所有用户。该 Issue 提供了详细的排除步骤，是社区解决此类问题的核心参考。
    *   **社区反应：** 16 条评论，收获了 8 个 👍，说明是高频共性问题。

5.  **[[Bug] rider无法登录qwen code](https://github.com/QwenLM/qwen-code/issues/4493)**
    *   **重要性：** 高。JetBrains Rider 用户无法通过 OAuth 登录，意味着无法使用云服务。这会阻碍部分使用特定 IDE 的用户群体。
    *   **社区反应：** 11 条评论。用户反馈登录页面会陷入无限重定向。

6.  **[[Feature] Support project-level Insight](https://github.com/QwenLM/qwen-code/issues/2040)**
    *   **重要性：** 中。用户迫切需要项目级别的分析能力，当前仅有机器级别的汇总，无法满足多项目管理需求。
    *   **社区反应：** 28 条评论，讨论热烈，说明这是企业级用户和高级用户的重要需求。

7.  **[[Bug] Useless compression and buggy contextWindowSize](https://github.com/QwenLM/qwen-code/issues/1924)**
    *   **重要性：** 中。上下文压缩功能在限制窗口大小时失效，对于一个依赖大上下文窗口的 AI 编程工具而言，这是严重的逻辑 Bug。
    *   **社区反应：** 6 条评论。用户怀疑是模型或工具本身的问题，需要进行深度排查。

8.  **[[Feature] Agent Team - Multi-Agent Collaboration](https://github.com/QwenLM/qwen-code/issues/1815)**
    *   **重要性：** 中。这是一个极具前瞻性的功能请求，希望引入多 Agent 协作模式。虽然复杂，但代表了社区对下一代 AI 编程能力（例如自动分工、协调）的渴望。
    *   **社区反应：** 3 条评论，但收获了 8 个 👍，社区呼声很高。

9.  **[[Feature] Add `qwen update` and `/update` commands with auto-update support](https://github.com/QwenLM/qwen-code/pull/5780)**
    *   **重要性：** 中。为用户提供了便捷的版本更新渠道，改善了开发者体验。虽然是个 PR，但其功能本身是社区长期以来的隐性需求。
    *   **社区反应：** 当前 PR 开放中，无评论。

10. **[[Feature] Move tool-use summaries to loading indicator](https://github.com/QwenLM/qwen-code/issues/5656)**
    *   **重要性：** 中低。专注于 UI/UX 优化，希望将工具调用的摘要信息从对话记录移动到 loading 指示器，以减少信息冗余。
    *   **社区反应：** 5 条评论，属于对体验细节的打磨。

## 重要 PR 进展

1.  **[ci(autofix): loosen issue candidate filters](https://github.com/QwenLM/qwen-code/pull/5860) (OPEN)**
    *   **内容：** 自动修复 CI 流程目前找不到任务，此 PR 放宽了 Issue 的筛选条件，让自动修复 Agent 能“找到活干”，提高 CI 的自动化修复效率。

2.  **[feat(core): add bundled extension creator skill](https://github.com/QwenLM/qwen-code/pull/5828) (OPEN)**
    *   **内容：** 内置了一个“扩展创建器”技能，可以指导 Agent 自动完成 Qwen Code 扩展的脚手架、定制和本地测试，极大降低了开发者的二次开发门槛。

3.  **[fix(daemon): resume /acp session stream via Last-Event-ID](https://github.com/QwenLM/qwen-code/pull/5852) (OPEN)**
    *   **内容：** 修复了守护进程（daemon）的 ACP 会话流中断后无法恢复的问题。通过支持 `Last-Event-ID`，实现断线重连后的无缝续传，提升了网络环境下的稳定性。

4.  **[feat(serve): add runtime context injection](https://github.com/QwenLM/qwen-code/pull/5847) (OPEN)**
    *   **内容：** 在服务端增加运行时上下文存储，允许外部调用者动态注入会话级别的系统提示，使得在对话过程中可以灵活调整上下文策略。

5.  **[feat(cli): support @extension mention in input autocomplete](https://github.com/QwenLM/qwen-code/pull/5849) (OPEN)**
    *   **内容：** 在 CLI 输入中支持 `@extension` 语法来触发已安装的扩展，使得扩展与文件、MCP 资源并列展示，交互更加统一和便捷。

6.  **[feat: add `qwen update` and `/update` commands](https://github.com/QwenLM/qwen-code/pull/5780) (OPEN)**
    *   **内容：** 新增 `qwen update` 命令行和 `/update` 斜杠命令，支持自动检查和安装更新（独立版用户），或提供手动升级指引（其他方式安装的用户）。

7.  **[fix(cli): skip default follow-up suggestions on local backends](https://github.com/QwenLM/qwen-code/pull/5821) (OPEN)**
    *   **内容：** 当用户使用本地 OpenAI 兼容后端（如 Ollama）时，默认关闭后续建议功能，避免因本地模型响应慢或格式不符导致的不良体验，体现了对不同使用场景的适配。

8.  **[fix(desktop): reject unsafe source slugs before deletion](https://github.com/QwenLM/qwen-code/pull/5829) (OPEN)**
    *   **内容：** 修复一个潜在的安全漏洞，在删除 source 时拒绝路径形式的 slug（如 `../sessions`），防止路径穿越攻击导致的文件误删。

9.  **[feat(web-shell): stream-highlight code blocks](https://github.com/QwenLM/qwen-code/pull/5869) (OPEN)**
    *   **内容：** 提升了 Web Shell 的代码块体验，实现了“流式语法高亮”，不再像以前一样随着 token 生成而频繁闪烁抖动，最终结果也更匹配正确的语言别名。

10. **[fix(cli): make alt+t expand thinking on macOS](https://github.com/QwenLM/qwen-code/pull/5872) (CLOSED)**
    *   **内容：** 修复了 macOS 系统下 `Alt+t` 快捷键在某些终端（如 iTerm2、VSCode 内置终端）下无法展开“思考”功能的问题，修复了跨平台输入体验。

## 功能需求趋势

从本期数据看，社区对 Qwen Code 的需求集中在以下几个方向：
1.  **项目级与精细化度量：** 用户不再满足于机器级别的分析，希望获得项目粒度的 Insight 洞察和多语言报告，这表明工具正从小型试用走向中大型项目实战。
2.  **IDE 深度集成与兼容性：** 大量 Issue 围绕 VSCode、JetBrains 系 IDE（特别是不受支持的 Rider 版本）展开。兼容性（尤其是 OAuth 登录、插件设置面板）是用户体验的基石。
3.  **核心稳定性和性能优化：** “流式超时”、“API 断流”、“连接错误”等是永恒的主题。新的 Bug（如 Windows 下 PowerShell 泄漏和 CI 环境隔离问题）显示了随着功能增加，并发和资源管理成为新的挑战。
4.  **自动化与 CI/CD 工作流：** 社区对自动修复 Issue、优化 CI 流水线（如测试分片、合并队列）等提升工程效率的功能表现出浓厚兴趣，说明高级开发者群体在积极参与工具共建。
5.  **扩展性与桥接能力：** 内置 “Extension Creator” 技能、支持 `@extension` 提及、以及搭建 Chrome Extension 等动向，表明 Qwen Code 正朝一个可编程的 AI 平台方向发展，而不仅仅是一个聊天工具。
6.  **终端用户体验改善：** 修复“流式高亮闪烁”、优化“Cmd+O 转录视图”、以及“计划批准门（Plan Approval Gate）”的讨论，都指向了提升交互流畅度和可控性。

## 开发者关注点

1.  **Windows 平台稳定性是重中之重：** `#5873` 中 PowerShell 进程泄漏问题引发了用户的强烈不满，这暴露了在 Windows 平台上的进程管理和资源回收机制存在严重缺陷。
2.  **安全性与可信度至关重要：** `#5055` 的安全误报案例明确传递了信号：任何可能被安全软件标记的问题都会迅速获得高优先级响应。开发者对异常打包产物充满警惕。
3.  **工具调用模式的健壮性：** `#535` 中提到的与特定模型的兼容性问题，表明在处理不同模型返回的 JSON 时，数据校验和容错机制有待加强。`old_string` 和 `content` 必须为字符串的错误过于基础，不应出现。
4.  **本地开发与云端连接体验的割裂：** 多个 Issue 反映了从本地模型切换到云端服务时遇到的问题，如 `#2724` （本地 Ollama 无法工作）、`#4493` （云登录失败）。流畅地在本地和云端之间切换，对于不同偏好和场景的用户至关重要。
5.  **核心交互逻辑的深度需求：** `/undo` 回退 (`#2342`) 和多 Agent 协作 (`#1815`) 虽然不是新概念，但社区持续高呼。这表明当前工具的“决策纠错”和“复杂任务分解”能力是短板，用户渴望更成熟的解决方案。
6.  **版本迭代与透明沟通：** 发布 (`#5831`) 和工作流 (`#5831`) 的失败被自动化 bot 报告，这种公开透明的失败跟踪机制受到欢迎。但用户也通过 `#5154` 等讨论表现出对底层性能开销的关注。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI（CodeWhale）社区动态日报 — 2026-06-26

---

## 1. 今日速览

- **品牌重塑正式落地**：v0.8.65 发布，项目规范名称变更为 **CodeWhale**，旧 npm 包 `deepseek-tui` 停止更新，用户需按迁移指南操作。
- **社区高度活跃**：过去 24 小时共更新 41 条 Issue 和 50 条 PR。审批流程改进、模式混合 Bug、多模型与 Fleet 自动负载选择是讨论最集中的主题。
- **关键修复与功能合并**：审批预览正式显示、提示词占用大幅精简、LSP 自定义服务器支持、以及子 Agent 状态同步等一系列 PR 已完成合并，产品稳定性与可扩展性显著提升。

---

## 2. 版本发布

### v0.8.65 — CodeWhale 品牌规范化
> **发布说明**：  
> 此版本是**品牌重塑**里程碑。从该版本起，正式项目名称、命令、npm 包名称统一为 `CodeWhale`。历史包 `deepseek-tui` 已废弃且不再发布。来自 v0.8.x 旧名称的用户请参考 `docs/REBRAND.md` 完成迁移。  
> 功能层面主要延续 v0.8.64 的 Fleet 模型类、负载自动选择等特性，详情见关联 Issue。

---

## 3. 社区热点 Issues（10 条）

### ① `#3568` — Plan 与 Agent 模式混合问题再次出现
- **作者**：DracheTek  
- **状态**：🟡 开放  
- **重要原因**：用户明确提供 log 证明模型在 Plan 模式下仍然执行 Agent 行为（尝试多个文件修改），说明该 Bug 尚未彻底根除，社区强烈关注（👍 1）。
- **链接**：[#3568](https://github.com/Hmbown/CodeWhale/issues/3568)

### ② `#861` — Thinking 块冻结/静默截断/丢失 reasoning_content
- **作者**：ZhouChaunge  
- **状态**：🔴 已关闭（修复已在历史版本合入）  
- **重要原因**：这是影响深度的推理显示缺陷合集，曾导致 spinner 卡死、输出截断等。虽然关闭，但作为历史高复现 Bug 仍值得回顾。
- **链接**：[#861](https://github.com/Hmbown/CodeWhale/issues/861)

### ③ `#3466` — 审批模态框取消与「审查必选」语义造成使用负担  
- **作者**：Artenx  
- **状态**：🔴 已关闭  
- **重要原因**：用户反馈升级后在 YOLO 模式下仍频繁要求确认，希望恢复「无需确认」的旧逻辑。该 Issue 推动后续审批预览及 Auto 模式的改进。
- **链接**：[#3466](https://github.com/Hmbown/CodeWhale/issues/3466)

### ④ `#3205` — v0.8.65 Fleet 模型类、Loadout 自动选择与语义路由角色
- **作者**：Hmbown  
- **状态**：🟡 开放  
- **重要原因**：定义 Fleet 自动模式的完整负载解析逻辑，是多模型并发的核心设计文档。讨论涉及 TUI/CLI/子 Agent 统一 selector。
- **链接**：[#3205](https://github.com/Hmbown/CodeWhale/issues/3205)

### ⑤ `#1186` — 添加类型化持久权限规则（execpolicy）
- **作者**：greyfreedom  
- **状态**：🟡 开放  
- **重要原因**：为执行策略层增加按工具名、命令前缀、路径模式的 allow/deny/ask 规则。安全与易用性关键增强，社区评论积极（10 条）。
- **链接**：[#1186](https://github.com/Hmbown/CodeWhale/issues/1186)

### ⑥ `#2300` — 多模型兼容文档与 Fleet 自动选择接纳标准
- **作者**：gavinwang668  
- **状态**：🟡 开放  
- **重要原因**：用户请求改善 `provider=vllm` 与 `provider=openai` 的文档差异说明，并希望增加多模型自动切换能力。直接关联 v0.8.65 交付清单。
- **链接**：[#2300](https://github.com/Hmbown/CodeWhale/issues/2300)

### ⑦ `#3541` — 功能请求：Rust 原生运行时/桌面端
- **作者**：jghwwnq  
- **状态**：🟡 开放  
- **重要原因**：社区提出 Node 运行时带来的冷启动、内存与事件循环瓶颈，希望迁移至 Rust 原生客户端以获得更低延时与更好的非编码体验。已有 3 条讨论。
- **链接**：[#3541](https://github.com/Hmbown/CodeWhale/issues/3541)

### ⑧ `#2953` — 精简默认提示词路径以接近 Codex 输入 Token 水平
- **作者**：Hmbown  
- **状态**：🟡 开放  
- **重要原因**：当前 CodeWhale 基础提示词明显大于 Codex，导致输入 Token 偏高。该 Issue 是 Token 优化系列（#2954 #2956 #2957）的纲领，对成本影响重大。
- **链接**：[#2953](https://github.com/Hmbown/CodeWhale/issues/2953)

### ⑨ `#1679` — Windows 下 SSE 多智能体并行超时（45s）且 UI 错乱
- **作者**：xaviertung  
- **状态**：🔴 已关闭  
- **重要原因**：Windows 平台特定 Bug，4 个智能体探活后正式执行失败，最终降级串行。跨平台稳定性重点 Issue。
- **链接**：[#1679](https://github.com/Hmbown/CodeWhale/issues/1679)

### ⑩ `#3369` — 恢复 Nightly 跨平台构建与自动标签幂等性
- **作者**：Hmbown  
- **状态**：🔴 已关闭  
- **重要原因**：CI/CD 关键修复。主分支构建在跨平台目标上出现失败，影响发版流水线。维护者关注点。
- **链接**：[#3369](https://github.com/Hmbown/CodeWhale/issues/3369)

---

## 4. 重要 PR 进展（10 条）

### ① `#3633` — fix(release): 在发布资产新鲜时才允许 registry 推送
- **作者**：Hmbown  
- **状态**：🟡 开放  
- **内容**：新增脚本校验本地/远程 tag SHA 与 Release workflow 是否一致，防止过期或不完整资产被发布。提升发布安全性。
- **链接**：[#3633](https://github.com/Hmbown/CodeWhale/pull/3633)

### ② `#3619` — fix(tui): 在审批卡片中显示提议的文件更改
- **作者**：Hmbown  
- **状态**：🔴 已合并  
- **内容**：闭合 #1846。在扩展审批卡内展示 `write_file`、`edit_file`、`apply_patch` 的差异预览，紧凑模式则回退显示参数摘要，解决之前无法看到变更内容的问题。
- **链接**：[#3619](https://github.com/Hmbown/CodeWhale/pull/3619)

### ③ `#3629` — perf(prompt): 精简默认静态提示词
- **作者**：Hmbown  
- **状态**：🔴 已合并  
- **内容**：压缩 `constitution.md` 中冗长的 RLM、思考预算、子Agent 等章节，保留结构锚点。新增回归测试确保静态提示词占用下降。对应 #2953 系列。
- **链接**：[#3629](https://github.com/Hmbown/CodeWhale/pull/3629)

### ④ `#3628` — feat(exec): 报告输入提示词构成分析
- **作者**：Hmbown  
- **状态**：🔴 已合并  
- **内容**：在 `codewhale exec --output-format stream-json` 元数据中添加 `input_analysis`，包含请求/消息/系统/框架 token 估算及 text、thinking、tool 占比，辅助 Token 优化。
- **链接**：[#3628](https://github.com/Hmbown/CodeWhale/pull/3628)

### ⑤ `#3627` — feat(exec): 报告可见最终答案大小
- **作者**：Hmbown  
- **状态**：🔴 已合并  
- **内容**：增加 `visible_final_answer_chars` 元数据字段，与 provider 输出 token 分离，帮助监控 Completion Token 使用情况。关联 #2957。
- **链接**：[#3627](https://github.com/Hmbown/CodeWhale/pull/3627)

### ⑥ `#3632` — feat(tui): 从验证过的触摸文件保存 apply_patch ask 规则
- **作者**：greyfreedom  
- **状态**：🔴 已合并  
- **内容**：实现持久化审批规则的保存快捷键 `S`。仅当 preflight 成功且所有触摸文件都能规范化成相对路径时启用，保存准确的一条 `apply_patch`+`path` 规则。推进 #1186。
- **链接**：[#3632](https://github.com/Hmbown/CodeWhale/pull/3632)

### ⑦ `#3620` — fix(tui): 在状态查询前同步过期子 Agent
- **作者**：Hmbown  
- **状态**：🔴 已合并  
- **内容**：在父 Agent 捕获运行状态之前清理心跳过期的子 Agent，使其显示为终态而非运行中，避免错误状态传递。
- **链接**：[#3620](https://github.com/Hmbown/CodeWhale/pull/3620)

### ⑧ `#3583` — refactor(localization): 将硬编码文本提取到 JSON 并通过 rust-i18n 加载
- **作者**：hongqitai  
- **状态**：🟡 开放  
- **内容**：将 `localization.rs` 中的文案移入 `crates/tui/locales`，引入 `rust-i18n` crate，是国际化（i18n）基础设施的关键重构。下一步替换手工字符串拼接。
- **链接**：[#3583](https://github.com/Hmbown/CodeWhale/pull/3583)

### ⑨ `#3624` — Codex/LSP: PHP 自定义服务器支持
- **作者**：yekern  
- **状态**：🟡 开放  
- **内容**：在内置 LSP 注册表中添加 PHP（intelephense），并新增 `[lsp.custom]` 配置段，允许用户按文件扩展名注册任意语言服务器（如 Ruby、C# 等），极大扩展编辑器集成能力。
- **链接**：[#3624](https://github.com/Hmbown/CodeWhale/pull/3624)

### ⑩ `#3571` — 清理 OHOS 及工具链，更新为 stable
- **作者**：shenjackyuanjie  
- **状态**：🟡 开放  
- **内容**：将 `rust-toolchain.toml` 由锁定 `1.88` 改为 `stable`，并移除多余 `.cargo/config.toml`。简化工具链维护。
- **链接**：[#3571](https://github.com/Hmbown/CodeWhale/pull/3571)

---

## 5. 功能需求趋势

从近期 Issues 与 PR 中可提炼出社区最关注的 **6 大功能方向**：

- **多模型与 Fleet 自动负载选择**  
  [#3205](https://github.com/Hmbown/CodeWhale/issues/3205)、[#2300](https://github.com/Hmbown/CodeWhale/issues/2300) 等表明，用户需要统一的模型/负载选择层，支持自动模式（Fleet loadout auto），并改善本地端点与多 provider 的文档差异。

- **执行策略与安全权限**  
  [#1186](https://github.com/Hmbown/CodeWhale/issues/1186) 提出的持久化权限规则（allow/deny/ask）获大量讨论，同时 [#3466](https://github.com/Hmbown/CodeWhale/issues/3466) 反映审批频繁问题，社区对可控、可记忆的审批逻辑需求迫切。

- **热栏（Hotbar）命令面板**  
  [#3389](https://github.com/Hmbown/CodeWhale/issues/3389) 及子 Issue 组成的 EPIC 显示，MMO 风格的 8 槽快捷动作条正在积极构建中，涵盖配置、渲染、按键分发与 MCP 工具集成。

- **输入/输出 Token 优化**  
  以 [#2953](https://github.com/Hmbown/CodeWhale/issues/2953)、[#2956](https://github.com/Hmbown/CodeWhale/issues/2956)、[#2957](https://github.com/Hmbown/CodeWhale/issues/2957) 为代表，社区强烈希望降低基础提示词体积、减少重复转录和完成 token，达到与 Codex 相近的效率。

- **终端 UI 可靠性与国际化的提升**  
  [#3487](https://github.com/Hmbown/CodeWhale/issues/3487) 要求建立终端视觉回归矩阵（对比度、边框、截断、覆盖），[#3583](https://github.com/Hmbown/CodeWhale/pull/3583) 则推动 i18n 基础设施，反映出全球用户对界面质量与本地化的更高期待。

- **扩展 LSP 与集成能力**  
  [#3624](https://github.com/Hmbown/CodeWhale/pull/3624) 的自定义 LSP 服务器功能，配合 [#3541](https://github.com/Hmbown/CodeWhale/issues/3541) 对 Rust 原生客户端的呼吁，体现了社区希望 CodeWhale 向更通用的开发工具链进化的意愿。

---

## 6. 开发者关注点

- **模式切换 Bug 顽固存在**  
  [#3568](https://github.com/Hmbown/CodeWhale/issues/3568) 代表的问题——模型在 Plan 模式下仍执行 Agent 行为——虽经多次修复仍复现，开发者对模式隔离的彻底性存疑，期望增加 turn 元数据中的模式策略提示（已在 [#3623](https://github.com/Hmbown/CodeWhale/pull/3623) 中部分解决）。

- **审批流程过于频繁**  
  升级后 YOLO 模式仍弹出审批要求（[#3466](https://github.com/Hmbown/CodeWhale/issues/3466)、[#3606](https://github.com/Hmbown/CodeWhale/issues/3606)），用户希望“Auto”模式名副其实，并能够全局或按路径记忆选择。新合并的 [#3618](https://github.com/Hmbown/CodeWhale/pull/3618) 正在改善此问题，但社区仍期待默认行为更智能。

- **终端渲染与兼容性问题**  
  多平台用户报告 UI 错乱、对比度过低、文本截断（[#3487](https://github.com/Hmbown/CodeWhale/issues/3487)）。Windows 下多智能体 SSE 超时（[#1679](https://github.com/Hmbown/CodeWhale/issues/1679)）是另一个长期痛点，虽然已关闭但根因是否彻底解决仍需观察。

- **安装体验故障**  
  [#3582](https://github.com/Hmbown/CodeWhale/issues/3582) 报告 `install.sh` 端点返回 HTML 导致脚本安装失败，直接影响新用户上手。维护者已响应并着手修复。

- **代码清理与技术债务**  
  多个 PR（[#3587](https://github.com/Hmbown/CodeWhale/pull/3587)、[#3571](https://github.com/Hmbown/CodeWhale/pull/3571)）专注于移除死代码、更新工具链到 stable，反映出维护团队正在为 v0.9.0 大版本清理债务。

- **子 Agent 状态一致性与监控**  
  [#2666](https://github.com/Hmbown/CodeWhale/issues/2666) 与 [#3620](https://github.com/Hmbown/CodeWhale/pull/3620) 表明，长时间运行任务中 Agent 对自身 Token 预算、上下文窗口、子任务状态缺乏可见性，开发者希望增加更多遥测和状态同步。

---

*本日报基于 GitHub 公共数据自动聚合，仅供参考。详细讨论请参阅对应链接。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*