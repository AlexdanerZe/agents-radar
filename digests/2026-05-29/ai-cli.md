# AI CLI 工具社区动态日报 2026-05-29

> 生成时间: 2026-05-29 02:54 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告 | 2026-05-29

## 1. 生态全景

当前 AI CLI 工具赛道正处于 **“能力爆发与稳定性阵痛并存”** 的阶段。多智能体协作、动态工作流、大上下文模型相继落地，但随之而来的会话损坏、平台兼容性缺口（尤其是 Windows）和安全事件频发，正在消耗开发者信任。各工具在模型生态绑定（Anthropic/OpenAI/Google/阿里/DeepSeek）和 IDE 集成策略上分化明显，同时插件/MCP 生态从“能用”转向“可控”，用户对权限管理和成本透明度的诉求急剧上升。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues（精选） | 重要 PRs | 版本发布数（24h） | 关键情绪标签 |
|------|-------------------|----------|------------------|--------------|
| **Claude Code** | 10 | 6 | 2 | 新功能兴奋，但会话损坏和补丁回退严重 |
| **OpenAI Codex** | 10 | 10 | 2 | 稳定迭代，但 Windows Sandbox/区域锁定问题突出 |
| **Gemini CLI** | 10 | 10 | 3 | P1 崩溃潮，付费用户权益受损，信任下滑 |
| **GitHub Copilot CLI** | 10 | 0 | 2 | WebSocket 错误集中爆发，核心功能中断 |
| **Kimi Code CLI** | 8（数据受限） | 10 | 0 | 产品方向骤变引发信任危机，稳定性修复密集 |
| **OpenCode** | 10 | 10 | 1 | GPT 延迟积怨深，Agent 误删文件引安全担忧 |
| **Pi** | 10 | 10 | 1 | 模型矩阵扩张快，跨 Provider 兼容性问题频发 |
| **Qwen Code** | 10 | 10 | 1 | Daemon 架构推进中，IDE 登录与 SSL 阻断突出 |
| **DeepSeek TUI** | 10 | 10 | 0 | 中文输入修复和斜杠命令转义受关注，多模型呼声高 |

> *说明：Issues 与 PRs 数量为各日报精选的高热度/关键进展，不代表仓库全部活动。版本发布含 stable、alpha、nightly 等。*

---

## 3. 共同关注的功能方向

**跨工具共鸣需求（≥4 个工具同时提及）：**

| 需求主题 | 涉及工具 | 典型诉求 |
|----------|----------|----------|
| **会话持久化与可靠恢复** | Claude Code, Codex, Gemini, Kimi, Pi, Qwen | 压缩后损坏、中断后不可恢复、重连断流 |
| **Windows 平台体验鸿沟** | Claude Code, Codex, Gemini, Pi, OpenCode, DeepSeek | WSL/SSH 崩溃、Sandbox 不可用、Shell 路径检测失败 |
| **模型成本/配额透明化** | Claude Code, Codex, Gemini, OpenCode, Pi | 默认窗口过大、配额误报、Token 用量不暴露 |
| **MCP/插件细粒度管控** | Claude Code, Codex, Gemini, Copilot, Kimi, Pi, Qwen, DeepSeek | 独立配置、热加载、权限分离、自定义命令 |
| **IDE 深度集成（ACP/VS Code）** | Claude Code, Codex, Kimi, OpenCode, Qwen, DeepSeek | 非交互模式、会话历史同步、内嵌浏览器 |
| **Agent 安全与行为透明** | Gemini, OpenCode, Copilot, Pi | 误删文件、跨会话泄露、静默降级模型 |

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 模型策略 | 技术路线侧重 | 目标用户 |
|------|---------|---------|-------------|---------|
| **Claude Code** | 多智能体编程先锋 | 绑定 Anthropic 模型（Opus 系列） | 动态工作流、Extended Thinking | 追求前沿 AI 能力的个人开发者/团队 |
| **OpenAI Codex** | 全栈编码诊断与远程开发 | 以 GPT/Codex 系列为主，逐步开放 | Remote Transport、诊断工具、插件市场 | 跨平台开发者，重视远程和诊断 |
| **Gemini CLI** | Google 生态入口 | Gemini 系列，与 Google Cloud 集成 | Agent 自动化（YOLO模式）、桌面控制 | GCP 用户、企业 Pro 订阅者 |
| **GitHub Copilot CLI** | GitHub 原生体验 | 多模型（Opus/GPT 等），自动选择 | MCP 扩展、非交互、代码审查 Agent | GitHub 重度用户、企业协作 |
| **Kimi Code CLI** | ACP 协议先行者 | Moonshot 自研模型 | IDE 集成（ACP）优先，淡化自用 TUI | 以 IDE（Zed等）为中心的中文开发者 |
| **OpenCode** | 高度可配置的 Agent 框架 | 多 Provider，强技能系统 | 技能/Skill 递归、并行子任务、V2 UI | 追求极致自定义的高级用户 |
| **Pi** | 万能 AI 网关 | 支持超 10 个 Provider（Claude, GPT, Qwen, DeepSeek等） | 扩展平台化、远程控制 API、设备码登录 | 多模型切换频繁、需要统一入口的团队 |
| **Qwen Code** | 阿里云原生 AI CLI | 阿里通义系列为主 | Daemon 架构、内置 Computer Use、会话压缩革新 | 阿里云生态企业、国内开发者 |
| **DeepSeek TUI** | 轻量开源社区驱动 | 当前专注 DeepSeek，正向多模型演进 | TUI 交互细节打磨、钩子系统 | DeepSeek 用户、追求极简终端的开发者 |

---

## 5. 社区热度与成熟度

- **生态位稳定、迭代节奏可控：**  
  **OpenAI Codex** 与 **GitHub Copilot CLI** 虽各有稳定性震荡，但版本发布规律，核心功能相对扎实，社区反馈有官方响应机制，属于“基础设施”级别工具。

- **高速迭代但信任波动：**  
  **Claude Code** 与 **Gemini CLI** 处于能力快速扩充期，但修复一 Bug 引入新 Bug 的“补丁套娃”效应正消耗社区耐心。**Pi** 凭借极快的模型跟进和扩展 API 迭代获得活跃贡献者，但跨 Provider 兼容性问题仍是隐患。

- **产品方向面临关键抉择：**  
  **Kimi Code CLI** 因重构版（Kimi Code）引发信任危机，现有用户担心沉没成本，社区热度虽高但情绪负面。**Qwen Code** 在 daemon 路线图下有明确规划，IDE 登录/SSL 问题修复后有望加速采用。

- **社区驱动但尚未商业化：**  
  **DeepSeek TUI**（CodeWhale）虽贡献者活跃，但无官方背书，版本和文档成熟度较低，适合尝鲜而非生产环境。

---

## 6. 值得关注的趋势信号

1. **多智能体协作从概念走向实战，但稳定性是最大瓶颈**  
   Claude Code 的动态工作流和 OpenCode 的并行子任务调度代表了行业方向，但“思考块损坏”“子 Agent 崩溃”等问题说明编排层仍需深度打磨。预计下半年将出现专用状态机和会话回放框架。

2. **MCP/插件生态进入“管控时代”**  
   社区不再满足于“能接插件”，而是要求**逐个启用/禁用**、**独立工作目录**、**热加载**和**精细权限**。Copilot 的预占 73% 窗口和 Kimi 的递归 Skill 目录需求都是缩影。插件市场化的前提是治理标准化。

3. **成本透明化将决定付费用户留存**  
   配额不重置、静默降级模型、默认开启 1M 窗口等“黑盒”行为正引发强烈反弹。未来 AI CLI 必须向用户提供**仪表盘级用量视图**和**可调节的成本控制策略**，否则将面临大户流失。

4. **Windows 仍是最大未攻克的平台堡垒**  
   几乎所有工具在 Windows 上都有严重稳定性问题（Sandbox 崩溃、Shell 路径、OAuth 卡死）。随着 AI 开发者工具的普及，Windows 开发者基数巨大，缺乏原生体验将限制工具进入企业市场。

5. **Agent 安全从“信任”转向“验证”**  
   Gemini 的跨用户对话泄露和 OpenCode 的误删文件事件表明，AI Agent 的权限模型必须内置 **“最小权限+人工确认”** 闭环。用户不再接受“全靠 LLM 良心”的安全策略。

6. **跨模型工作流带来新的兼容性成本**  
   从 Pi 的多 Provider 切换 ID 冲突到 Kimi 的会话角色不匹配，开发者对“一个 CLI 管理所有模型”的需求越强，Provider 之间的消息格式、角色体系、推理细节兼容就越成为技术负债。标准化协议（如 ACP）的演进值得关注。

---

*本报告基于 GitHub 各仓库公开 Issue/PR/Release 信息生成，数据截止 2026-05-29 社区日报。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是对您提供的 `anthropics/skills` 仓库数据的分析报告（数据截止至 2026-05-29）。由于源数据中评论数显示为 `undefined`，热门度主要参考了源数据排名、PR 功能深度及社区回应的活跃度（更新时间、功能完整性）进行综合评判。

---

## Claude Code Skills 社区热点报告

### 1. 热门 Skills 排行

以下是社区关注度最高、讨论最具深度的 Skills PR：

1.  **文档排版控制（#514）** `[Open]`
    - **功能**：专门修复 AI 生成文档中的孤儿单词（孤行）、寡段（页首标题脱离正文）、编号错位等排版硬伤。
    - **社区讨论热点**：该需求被认为是“最能提升 AI 文档专业感”的技能，直接对标专业排版软件规范。
    - **链接**：https://github.com/anthropics/skills/pull/514

2.  **OpenDocument 格式支持（#486）** `[Open]`
    - **功能**：支持创建、填充、转换 .odt/.ods 格式，打通 LibreOffice 等开源办公生态。
    - **社区讨论热点**：极大地拓宽了 Claude 在政府、教育及欧洲企业中的应用场景，讨论集中在模板填充与格式互转的准确性。
    - **链接**：https://github.com/anthropics/skills/pull/486

3.  **前端设计技能精炼（#210）** `[Open]`
    - **功能**：对官方 `frontend-design` 技能进行重构，确保每条指令都是 Claude 在单轮对话中能立刻执行的精确动作。
    - **社区讨论热点**：代表了社区对现有官方技能进行“瘦身”和“可执行化改造”的强烈诉求，强调从“人类可读”转向“机器可执行”。
    - **链接**：https://github.com/anthropics/skills/pull/210

4.  **技能市场质检与安全扫描器（#83）** `[Open]`
    - **功能**：添加 `skill-quality-analyzer` 和 `skill-security-analyzer` 两个元技能，对生态中 Skills 的结构、文档、安全性进行评分。
    - **社区讨论热点**：直接呼应了 Issue #492（命名空间信任边界滥用）的危机，社区开始自发建立质量治理体系。
    - **链接**：https://github.com/anthropics/skills/pull/83

5.  **AURELION 认知框架套件（#444）** `[Open]`
    - **功能**：提供五层结构化思维模板、上下文记忆系统（shodh-memory）等，为 AI 建立“长期记忆”和“思考框架”。
    - **社区讨论热点**：关于如何让 AI 跨会话保持上下文一致性、以及结构化思考与自由对话之间的平衡。
    - **链接**：https://github.com/anthropics/skills/pull/444

6.  **n8n 自动化工作流构建（#190）** `[Open]`
    - **功能**：专注于 n8n 工作流的构建与调试，可实现从零搭建复杂自动化流水线。
    - **社区讨论热点**：AI 编程与低代码自动化的深度结合，被普遍视为“AI Agent 驱动业务自动化”的绝佳落地案例，社区持续贡献迭代。
    - **链接**：https://github.com/anthropics/skills/pull/190

7.  **全栈测试模式覆盖（#723）** `[Open]`
    - **功能**：覆盖测试奖杯模型、AAA 模式、React 组件测试及 E2E 测试。
    - **社区讨论热点**：高质量测试生成一直是刚需，该技能系统性地填补了 Skills 市场中测试领域的空白。
    - **链接**：https://github.com/anthropics/skills/pull/723

8.  **代码库资产审计（#147）** `[Open]`
    - **功能**：系统化扫描项目中的孤儿代码、未使用文件、文档缺口及基础设施膨胀。
    - **社区讨论热点**：针对遗留项目重构与代码清理的场景，社区认为该技能能直接转化为可量化的项目维护价值。
    - **链接**：https://github.com/anthropics/skills/pull/147

---

### 2. 社区需求趋势

从 Issues 中可以提炼出以下五大核心趋势：

- **企业级共享与安全治理**（#228、#492、#1175）：社区不再满足于个人使用，强烈要求 Skills 支持**组织内部分享**（一键分发的库），并解决 **`anthropic/` 命名空间被滥用导致的安全信任危机**，以及 SharePoint 等企业平台接入时的权限合规问题。

- **工具链稳定压倒一切**（#556、#189、#1087）：大量 Issue 指向开发者工具链的稳定性问题。`run_eval.py` 评估工具 0% 触发率、插件重复安装、错误加载所有 Skill 等 Bug 被反复提及，说明**稳定可靠的本地开发体验**是目前社区最大的痛点。

- **垂直领域深度专业化**（PR #181、#568、#190）：从 SAP 的 ERP 预测、ServiceNow 的 ITSM，到 n8n 的工作流，社区希望 Skills 不要停留在“怎么写代码”，而是转向“**特定领域的资深专家**”，直接解决复杂业务场景。

- **“元技能”与 Agent 治理觉醒**（#83、#412）：社区开始构思**监管 AI 的技能**，例如提案“代理治理技能”（Agent Governance），要求 AI 在执行时具备策略执行、威胁检测和审计追踪能力。

- **跨生态互操作**（#29、#16）：用户希望在 Bedrock 上使用 Skills，并呼吁将 Skills 暴露为 MCP 工具，这表明社区追求**平台无关性**和**协议标准化**。

---

### 3. 高潜力待合并 Skills

以下 PR 讨论热度高、实现价值明确且持续更新，具有近期合入主干的高潜力：

1.  **Document Typography（#514）**：近乎通用场景，社区排版痛点极深，更新至 3 月仍在活跃优化。
    - *链接：* https://github.com/anthropics/skills/pull/514

2.  **Testing Patterns（#723）**：直击开发核心环节，补齐 Skills 在测试生态上的短板。
    - *链接：* https://github.com/anthropics/skills/pull/723

3.  **n8n Builder/Debugger（#190）**：与当前 AI + 自动化趋势完美契合，PR 更新至 5 月 18 日，非常活跃。
    - *链接：* https://github.com/anthropics/skills/pull/190

4.  **ServiceNow Platform Skill（#568）**：企业 IT 场景的“敲门砖”技能，需求确定性强，篇幅庞大。
    - *链接：* https://github.com/anthropics/skills/pull/568

5.  **ODT Skill（#486）**：填补了 ISO 标准格式支持的空白，战略价值高，不断有用户催促合入。
    - *链接：* https://github.com/anthropics/skills/pull/486

---

### 4. Skills 生态洞察

**当前社区最集中的诉求是：推动 Skills 生态从“实验性的能力陈列”向“企业级生产工具”跨越，核心聚焦于安全治理、工具链可靠性与垂直领域的专业化深度。**

---

好的，这是根据您提供的 GitHub 数据生成的 2026-05-29 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-05-29

## 今日速览

今日 Claude Code 社区情绪复杂，核心词是“阵痛”。Anthropic 在昨日（v2.1.154）正式发布了备受期待的 **Opus 4.8** 与 **动态工作流**，点燃了开发者对多智能体编程的热情。然而，伴随新模型而来的 Extended Thinking 严重会话损坏问题，迫使团队今日紧急发布 v2.1.156 热修复。遗憾的是，该修补引入了新的回归问题，导致大量用户遭遇“修复一个 Bug 又引入另一个 Bug”的窘境，社区焦点高度集中在版本稳定性、会话恢复和成本控制上。

## 版本发布

过去 24 小时内发布了两个版本。

- **v2.1.154（重大更新）**
  - **引入 Opus 4.8 模型**：现已作为默认模型，并支持 `/effort xhigh` 应对最高难度任务。
  - **引入动态工作流（Dynamic Workflows）**：Claude 现在可以自主编排数十到数百个后台代理来处理大型复杂任务。
  - [查看 Release 详情](https://github.com/anthropics/claude-code/releases/tag/v2.1.154)

- **v2.1.156（紧急修补）**
  - **修复**：修复了使用 Opus 4.8 时，思考块（thinking blocks）被修改导致 API 400 错误的问题。
  - **注意**：该修复引入了新的回归问题（参见下方热点 Issue）。
  - [查看 Release 详情](https://github.com/anthropics/claude-code/releases/tag/v2.1.156)

## 社区热点 Issues

社区讨论热度极高，以下 10 个 Issue 覆盖了今天最核心的痛点与需求。

1.  **`#63469` / `#63423` - 最新热修复引入回归：API 400 "Invalid message role 'system'"**
    - **为何重要**：这是明日之星 v2.1.156 和 v2.1.154 的严重回归。API 报错消息角色错误，直接导致大量用户在 Windows、macOS、VS Code 等环境下无法正常发起请求，波及面极广。
    - **社区反应**：多条独立报告涌入，Comment 迅速累积。
    - [Issue #63469](https://github.com/anthropics/claude-code/issues/63469) | [Issue #63423](https://github.com/anthropics/claude-code/issues/63423)

2.  **`#63147` - 恢复 Extended Thinking 会话导致永久性 400 错误**
    - **为何重要**：这是触发 v2.1.156 紧急修复的核心故障。包含工具调用和思考块的会话一旦中断，将彻底无法恢复，直接导致工作流失。这是开发者最无法接受的“会话不可恢复”错误。
    - **社区反应**：32 个 👍 和 26 条评论，情绪非常激烈。
    - [Issue #63147](https://github.com/anthropics/claude-code/issues/63147)

3.  **`#63463` - 独立复现 v2.1.154 下的不可恢复 400 错误**
    - **为何重要**：通过独立会话交叉验证，确认 `#63147` 并非偶发，而是 Opus 4.8 + Extended Thinking 模式下的系统性问题。
    - [Issue #63463](https://github.com/anthropics/claude-code/issues/63463)

4.  **`#63358` - Opus 4.8 返回空思考块**
    - **为何重要**：开发者完全无法看到 AI 推理过程，等于失去了 AI 编程辅助中最关键的“透明度”功能。这与之前 Opus 4.7 的 `#49268` 问题完全一致，表明模型切换时该模块的兼容性测试存在严重遗漏。
    - [Issue #63358](https://github.com/anthropics/claude-code/issues/63358)

5.  **`#63258` - 动态工作流中后台子代理（Subagents）崩溃**
    - **为何重要**：直接打击了 v2.1.154 的王牌特性。用户刚尝试派发后台 Agent 探索代码，子代理就在首次交互时因“思考块无法修改”直接崩溃，核心功能形同虚设。
    - [Issue #63258](https://github.com/anthropics/claude-code/issues/63258)

6.  **`#63448` - Opus 4.8 上下文压缩后报 400 错误**
    - **为何重要**：长对话是 AI 编程的基石。一旦触发自动上下文压缩（Compaction），会话即陷入不可恢复的 404 漩涡，这意味着 Opus 4.8 目前根本不具备稳定的长上下文处理能力。
    - [Issue #63448](https://github.com/anthropics/claude-code/issues/63448)

7.  **`#49268` - Opus 4.7 思考摘要缺失（历史参考）**
    - **为何重要**：虽为 Opus 4.7 的遗留问题，但它是理解 Opus 4.8 空思考块问题（`#63358`）的关键背景。该 Issue 揭示了 Anthropic 在 Extended Thinking 实现上长期存在的结构性缺陷。
    - [Issue #49268](https://github.com/anthropics/claude-code/issues/49268)

8.  **`#62063` - Pro 用户默认使用 1M 上下文导致信用点滥用**
    - **为何重要**：成本与实际费用直接挂钩。新会话自动开启昂贵的 1M 上下文窗口，让许多按量付费或 Pro 用户感到“钱包在燃烧”，社区强烈要求提供默认模型和上下文的手动配置选项。
    - [Issue #62063](https://github.com/anthropics/claude-code/issues/62063)

9.  **`#23669` - [增强] Agent Teams 支持独立配置**
    - **为何重要**：尽管动态工作流已发布，但社区渴望更精细的控制。该需求建议为每个 Agent 配置独立的工作目录、CLAUDE.md 和 MCP，这是迈向复杂多仓库开发场景的必经之路。
    - [Issue #23669](https://github.com/anthropics/claude-code/issues/23669)

10. **`#29438` - [增强] iOS 远程控制推送通知**
    - **为何重要**：远程控制模式让移动办公成为可能，但缺乏推送通知意味着开发者不能离开屏幕，必须盯着终端等待授权。该需求获得了 54 个 👍，呼声极高。
    - [Issue #29438](https://github.com/anthropics/claude-code/issues/29438)

## 重要 PR 进展

过去 24 小时内 PR 活动较少，共有 7 个 PR，主要集中在文档修复和插件开发。

1.  **`#63467` - 文档：为 Windows 添加 gh CLI 安装说明**
    - 内容：修复 `/commit-push-pr` 的 README，增加了 Windows 的 `winget` 安装指南。
    - [PR #63467](https://github.com/anthropics/claude-code/pull/63467)

2.  **`#63460` - 文档：更新被弃用的 npm 安装说明**
    - 内容：将 plugins README 中已弃用的 `npm install -g` 更新为官方推荐方式。
    - [PR #63460](https://github.com/anthropics/claude-code/pull/63460)

3.  **`#63382` - 修复：修正 Hookify 测试示例语义**
    - 内容：优化 Hookify 插件的测试示例，使其更贴近引擎实际的子串匹配行为。
    - [PR #63382](https://github.com/anthropics/claude-code/pull/63382)

4.  **`#63262` - 功能：新增侧边线程（side-threads）插件**
    - 内容：社区贡献的“侧边线程”插件，通过 `/thread` 和 `/back` 命令在对话中管理临时的侧边讨论，非常适合处理分支问题。
    - [PR #63262](https://github.com/anthropics/claude-code/pull/63262)

5.  **`#63189` - 功能：`/commit-push-pr` 支持仓库 PR 模板**
    - 内容：改进自动生成 PR 的能力，现在会读取 `.github/PULL_REQUEST_TEMPLATE.md`，使生成的 PR 更符合规范。
    - [PR #63189](https://github.com/anthropics/claude-code/pull/63189)

6.  **`#62941` - 修复：修复 Ralph Wiggum 钩子日志读取问题**
    - 内容：修复停止钩子只能读取对话记录最后一行的问题，确保能正确获取完整的助手消息。
    - [PR #62941](https://github.com/anthropics/claude-code/pull/62941)

## 功能需求趋势

从今日的 Issue 和 PR 中可以提炼出社区清晰的关注方向：

1.  **智能体集群的专属化配置**：社区不满足于统一的 Agent 环境。`#23669` 等需求明确指向 **为每个 Agent 配置独立的工作目录、MCP 和 CLAUDE.md**，这是 AI 编程从“单体”转向“多智能体协作”的必然要求。
2.  **全场景移动办公与远程控制**：`#29438` 的推送通知需求和 `#63470` 的 TLS 兼容性问题表明，“Remote Control” 正在从尝鲜进入实用阶段，开发者要求全天候的稳定连接与免盯屏交互。
3.  **成本敏感与精细化控制**：`#62063` 的持续热度表明，随着 1M 上下文和大模型普及，社区对 **默认上下文大小、模型切换的灵活性及成本透明度** 的需求非常迫切。
4.  **终端交互体验打磨（TUI）**：`#62922` 中提出的“多行输入时方向键应导航行而非历史”这类细微但高频的交互诉求，反映了开发者对 TUI 工具完成度的要求正在提高。

## 开发者关注点

1.  **Opus 4.8 发布即阵痛**：这是今日压倒性的开发者痛点。尽管新模型和动态工作流令人兴奋，但 **“会话永久损坏”、“空思考块”、“子智能体崩溃”** 等系统性 Bug 严重削弱了新版本的可信度。开发者普遍呈现出“激动尝试 -> 遭遇损坏 -> 社区求助 -> 等待修复”的统一路径。
2.  **“补丁套娃”消磨信任**：v2.1.154 出现问题 -> v2.1.156 紧急修复 -> v2.1.156 又引入新 API 错误。这种“修复一个 Bug 引入另一个 Bug”的连锁反应，让许多开发者对版本升级持谨慎观望态度。
3.  **Windows 平台生态体验鸿沟**：无论是 `#50640` 的启动段错误、`#57035` 的 DACL 安装权限问题，还是 `#63470` 的 TLS 代理拦截，Windows 用户在稳定性方面面临的挑战远高于 macOS 用户，成为显著的体验短板。
4.  **会话可靠性与持久化**：`#63147` 和 `#63448` 反复指向同一个核心诉求：**AI 会话能否像 IDE 一样稳定持久**？对于需要长时间 AI 辅助重构或调试的开发者来说，会话无法恢复是不可接受的。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

## OpenAI Codex 社区动态日报 | 2026-05-29

---

### 1. 今日速览

今日，OpenAI Codex 发布了 **`rust-v0.135.0`** 稳定版与 **`rust-v0.136.0-alpha.1`** 测试版，核心增强了诊断工具（`codex doctor`）的信息丰富度以及远程连接状态的透明度。**Windows 平台** 再度成为社区焦点，ARM64 Sandbox 兼容性问题和 Chrome 插件区域锁定导致多个 Issue 热度飙升。基础架构方面，多项关键 PR 取得进展，涵盖 **Per-session 模型重载**、**执行服务器连接 Token 认证** 以及 **Code Mode 持久化 Session 重构**。

---

### 2. 版本发布

- **rust-v0.135.0**
  - `codex doctor` 诊断报告全面升级，现可收集更丰富的环境变量、Git 信息、终端、App Server 配置及线程清单，用于支持工单的快速定位。
  - 新增 `/status` 命令，TUI 在远程连接（Remote Transport）时会显示远程连接详情和服务器版本。
  - Vim 模式更新。
  [查看发布说明](openai/codex Releases)

- **rust-v0.136.0-alpha.1**
  - 发布 0.136.0 的首个 Alpha 版本，为社区提供了提前验证新功能的能力。
  [查看发布说明](openai/codex Releases)

---

### 3. 社区热点 Issues

（筛选过去 24 小时内最受关注的 10 个 Issue，综合评论数、Upvote 及影响范围）

1. **#19909 - [Feature] 使 Chats 项目目录可配置**
   社区强烈呼吁（16 👍）将 `~/Documents/Codex` 默认路径改为可配置。因为 macOS 用户普遍启用 iCloud Drive 同步 `Documents` 目录，导致大型代码仓库频繁触发同步冲突。
   [Issue 链接](openai/codex Issue #19909)

2. **#20538 - [Bug] 偏好设置陷入 "无法保存" 循环**
   高优 Bug（17 👍）。用户在对 `config.toml` 进行连续写入操作后触发 `configVersionConflict`，导致任何配置更改都无法保存，即使重启 App 也无法恢复。
   [Issue 链接](openai/codex Issue #20538)

3. **#21598 - [Bug] Windows Desktop Chrome 插件在挪威 / EU 无法暴露**
   尽管 Chrome 扩展已显示 “Connected”，Codex Desktop 仍不暴露 `@Chrome` 路由。社区质疑这是 EU/UK 区域性的灰度策略或政策锁，导致用户基础的分裂。 (25 条评论)
   [Issue 链接](openai/codex Issue #21598)

4. **#22107 - [Bug] 远程上下文压缩（Context Compaction）流断开**
   核心功能可靠性 Bug。在进行远端编码压缩时，任务报错 `stream disconnected before completion`，直接导致工作流中断，且缺乏自动重试机制。 (13 条评论)
   [Issue 链接](openai/codex Issue #22107)

5. **#24006 - [Bug] macOS 更新后 Codex 无法访问本地数据库**
   灾难性 Bug。App 更新后无法完成启动，日志显示数据库连接异常，导致用户无法进行任何操作，属于极度影响体验的回归问题。 (7 条评论)
   [Issue 链接](openai/codex Issue #24006)

6. **#24259 / #24391 - [Bug] Windows Sandbox 全面故障（ARM64 + spawn setup）**
   Windows 用户在两种架构（ARM64 / x64）下均遭遇 `spawn setup refresh` 失败。更新至 CLI 0.133.0 后问题爆发（#24391 获得 15 👍），严重阻碍 Windows 用户使用沙箱环境。
   [Issue #24259](openai/codex Issue #24259) | [Issue #24391](openai/codex Issue #24391)

7. **#23953 - [Bug] Codex Remote 误报 “Quota Exceeded”**
   严重影响 Remote / Mobile 用户信任度。用户在远程会话中看到 “配额已用尽”，但通过 SSH 在同一台机器直接使用 CLI 却能正常响应，说明配额检查逻辑存在误判。
   [Issue 链接](openai/codex Issue #23953)

8. **#24373 - [Bug] Google Drive Sheets 插件读取正常但写入失败**
   插件权限 Bug。插件可以正常读取 Sheet，但在执行 `_batch_update_spreadsheet` 追加行时返回 “No permission”，重装插件无法解决，影响数据回写场景。 (12 条评论)
   [Issue 链接](openai/codex Issue #24373)

9. **#24969 - [Bug] Windows Store 版 Browser Use 被企业策略封锁**
   新近热门 Bug（05-28）。Win Store 版 Codex 内置浏览器被企业网络策略完全阻隔，且无法回退到 Chrome Extension 模式，Enterprise 用户彻底无法使用 Browser Use 能力。
   [Issue 链接](openai/codex Issue #24969)

10. **#13165 - [Feature] 允许用户指定 Codex 使用的 Shell**
    社区最高呼声需求之一（21 👍）。Windows 用户要求 Codex 使用 MinGW Bash 或其他 Unix Shell，而非强制使用 Powershell，以避免大量与 Powershell 不兼容的 Shell 脚本。
    [Issue 链接](openai/codex Issue #13165)

---

### 4. 重要 PR 进展

（筛选过去 24 小时内更新的 10 个关键 PR，涵盖架构重构、新特性与 Bug 修复）

1. **#24992 - Move skills path refs into exec server**
   **核心架构重构**。将路径解析逻辑从分散的模块抽离至统一的 `EnvironmentPathRef`，整合 Skill 加载路径，为跨平台（本地 / 远端 / 插件）路径处理提供统一基座。
   [PR 链接](openai/codex PR #24992)

2. **#24999 - Add per-session realtime model and version overrides**
   **按需重载**。允许用户在不修改 `config.toml` 且不重启 App Server 的前提下，在每次实时会话（Realtime Session）启动时指定不同的 `model` 和 `version`，极大提升灵活性。
   [PR 链接](openai/codex PR #24999)

3. **#24996 - Use marketplace allowlist for plugin install suggestions**
   **插件生态治理**。采用 Marketplace 白名单机制替换原先硬编码的插件推荐列表，推动插件生态的规范化，同时保留手动 Opt-in 路径。
   [PR 链接](openai/codex PR #24996)

4. **#24958 - Add exec-server direct websocket connection token**
   **安全性加固**。引入 `--connection-token` 参数，要求 WebSocket 升级链路必须携带 `?token=TOKEN` 验证，防止未授权进程直接连接执行服务器。
   [PR 链接](openai/codex PR #24958)

5. **#24180 - Introduce durable session interface for code-mode**
   **架构性铺垫**。抽离 Code Mode 会话为独立接口（`CodeModeSession`），将 Cells 的生命周期、终止与回调标准化，为未来实现更稳定、可插拔的代码执行引擎打下基础。
   [PR 链接](openai/codex PR #24180)

6. **#22668 - Wire managed MITM CA trust into child env**
   **网络代理补全**。当 Codex 启用 HTTPS 中间人模式（MITM）时，确保其生成的 CA 证书能被子进程信任，从而在网络受限环境中实现完整的流量劫持与审计。
   [PR 链接](openai/codex PR #22668)

7. **#24622 - Switch runtime to cloud config bundle**
   **云原生配置迁移**。作为 “Cloud Managed Config” 系列的最后拼图，将运行时配置全面切换到统一的云端配置包，彻底替换旧的 `codex-cloud-requirements` 路径。
   [PR 链接](openai/codex PR #24622)

8. **#24987 - feat(tui): hide background MCP startup status**
   **用户体验优化**。MCP Server 的后台初始化状态默认不再抢占 TUI 主显示区，解决了启动时因服务器繁多导致的界面“刷屏”和信息过载问题。
   [PR 链接](openai/codex PR #24987)

9. **#24805 - Add CODEX_ENV_FILE for SessionStart hooks**
   **Shell 环境初始化**。SessionStart 钩子现在可以创建一个环境文件 `CODEX_ENV_FILE`，该文件的内容会持久影响到后续的所有 Shell 命令（如 PATH 调整、虚拟环境激活），彻底解决了跨命令状态丢失的问题。
   [PR 链接](openai/codex PR #24805)

10. **#24124 / #24122 / #24123 - Local usage report command series**
    **开发者透明度工具**。三件套 PR 实现了 `/usage` 命令。包括 Token 使用归因追踪、App Server 接口暴露和 TUI 渲染。用户现在可以直接在终端查看不同功能（Skills、工具调用等）的 Token 消耗占比。
    [PR #24124](openai/codex PR #24124) | [PR #24122](openai/codex PR #24122) | [PR #24123](openai/codex PR #24123)

---

### 5. 功能需求趋势

通过观察近 24 小时的所有活跃 Issue，社区最关心的功能方向如下：

- **平台深度兼容性**：**Windows 11 ARM64 原生支持** 是最缺位的能力，Sandbox 的不可用是 Windows 用户的头号痛点。同时，**macOS 大版本更新的无感升级**（避免 DB 破坏）也是一个核心关注点。
- **配置自由与透明化**：从 **可配置的存储路径** 到 **自定义 Shell**，再到 **Token 用量报告**，社区对 “越狱” 默认限制、拥有更多控制权有着强烈的诉求。
- **远程工作流可靠性**：Context Compaction 断连和 Quota 误报，反映出远程会话的健壮性是除功能丰富度外，最影响高端用户留存的关键。
- **插件治理与稳定性**：Chrome 的区域锁定、Google Drive 的写入权限、UI 与运行时的状态不一致，社区希望获得一个 **所见即所得、稳定可靠** 的插件生态，而不仅仅是插件数量的增加。

---

### 6. 开发者关注点

开发者反馈中反复提及的痛点和需求总结：

- **"One is Not Enough" - 默认配置的妥协**
  - **Shell 绑定**：Windows 上强制使用 Powershell 让 Unix 工具链的开发者苦不堪言（#13165）。
  - **路径绑定**：`~/Documents/Codex` 与 iCloud 的冲突，说明默认路径选择并没有考虑特定平台的生态特点（#19909）。

- **"Flaky and Silent" - 错误处理与诊断断层**
  - **静默失败**：Chrome 插件看似连接却不可用（#21791, #21598）。
  - **错误误导**：Remote 报 Quota 不足，CLI 却能跑（#23953）。开发者无法确定是 Bug、策略限制还是自己操作失误。
  - **配置损坏**：`configVersionConflict` 导致整个 App 锁死，没有任何有效的恢复引导（#20538）。

- **"Windows as a Second Class Citizen" - 平台体验偏差**
  - Sandbox 在不同版本和架构下间歇性崩溃（#24259, #24391）。
  - Store 版本功能受限（#24969）。
  - 社区高影响力用户越来越难以向 Windows 团队推荐 Codex，平台差异正在消耗社区信任。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是基于 2026-05-29 提供的 GitHub 数据为您生成的 Gemini CLI 社区动态日报。

---

## Gemini CLI 社区动态日报 (2026-05-29)

---

### 1. 今日速览

今日社区动态主要围绕**稳定性危机**与**付费用户体验降级**两大焦点。多个 P1 级别的 CLI 崩溃报告（`node-pty` / `EBADF`）密集涌现，严重影响了 WSL 及 SSH 环境下的开发工作。与此同时，大量付费用户遭遇了**配额永不重置**、**无法访问最新模型**以及**企业身份被错误路由**等账户权限问题，社区反馈激烈。开发团队已紧急向稳定版和预览版回迁关键修复，多个针对 PTY 崩溃和 Agent 健壮性的 PR 正在积极推进中。

---

### 2. 版本发布

过去 24 小时内共发布 3 个版本，核心动作是**紧急回迁关键热修复**。

- **v0.44.1 (Stable)** & **v0.45.0-preview.1 (Preview)**
  - **内容**：两个版本均回迁了关键 hotfix `bd53951`。在当前稳定性问题频发的背景下，此修复显得尤为紧迫。
  - **链接**: https://github.com/google-gemini/gemini-cli/releases/tag/v0.44.1
- **v0.45.0-nightly.20260528.g5cac7c10f**
  - **内容**：修复了在 Vim 快捷键模式下，未映射按键导致 CLI 无响应的问题。这是来自社区贡献者 @MukundaKatta 的首次贡献。
  - **链接**: https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.0-nightly.20260528.g5cac7c10f

---

### 3. 社区热点 Issues

以下挑选了 10 个当前最值得关注的 Issue，涵盖 P1 崩溃、付费用户权限与安全事件。

#### P1 崩溃潮：`node-pty` 危机

1.  **#27544 (Open)**: **Gemini CLI 持续崩溃（ioctl EBADF）**
    - **为什么重要**: 当前社区最热的稳定性话题，P1 级别，多个用户在同一时间段内报告了完全相同的错误堆栈（`ioctl(2) failed, EBADF`）。
    - **社区反应**: 用户情绪沮丧，强调该问题在关键工作中频繁出现，导致开发流程完全中断。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/27544

2.  **#27533 (Open)**: **SSH 远程开发环境下的 PTY 崩溃**
    - **为什么重要**: 点明了崩溃的特定场景——SSH 远程时因 `resizePty` 操作引发。这对于大量使用远程开发的团队是致命打击。
    - **社区反应**: 用户提供了详细的 `node-pty` 日志，帮助定位问题根源。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/27533

#### 付费用户权益与配额谜团

3.  **#24222 (Closed)**: **AI Pro 用户无法访问 Gemini 3.1 Pro**
    - **为什么重要**: 付费用户被“影子封禁”，无法使用最新高价模型。这是严重的计费与权限系统 bug。
    - **社区反应**: 获得 7 个赞和 11 条评论，用户普遍反映“从未违规但被误伤”，对计费系统的透明度和公平性产生质疑。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/24222

4.  **#22634 (Closed)**: **v3 Flash 配额消耗极快**
    - **为什么重要**: Agent 模式下，一个任务就可能消耗掉数十次甚至上百次请求配额，导致每天很快触及 1500 次的限制。
    - **社区反应**: 用户认为这种消耗速度不符合预期，感觉被欺骗，认为定价模型与实际消耗严重不符。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/22634

5.  **#22643 (Closed)**: **配额“永不重置”**
    - **为什么重要**: 即使过了 API 指定的重置时间（甚至等待 3 天），配额依然处于封锁状态。
    - **社区反应**: 用户尝试切换到 API Key 后发现同样被秒封，怀疑是服务端的全局封禁机制出了问题。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/22643

#### 企业级功能与认证故障

6.  **#19970 (Closed)**: **OAuth 强制覆盖企业身份**
    - **为什么重要**: 这是企业级采用的核心障碍。当用户同时拥有消费者 AI Pro 和企业 Code Assist 时，CLI 强制使用消费者身份，导致企业客户丧失 IP 保障等法律协议保护。
    - **社区反应**: 用户（thiago-cavalcanti）非常严肃地指出这是法律级别的风险，企业客户无法接受这种自动降级行为。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/19970

7.  **#23865 (Closed, P1)**: **WSL2 OAuth 完全损坏**
    - **为什么重要**: WSL2 是大量开发者的主力环境，该环境下的 OAuth 登录完全失效，并与其他安全工具（Antigravity）冲突，直接锁死了 Pro 用户。
    - **社区反应**: 用户情绪激动（标题采用全大写 CRITICAL），指责该问题导致付费服务完全不可用。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/23865

#### 安全事件与 Agent 稳定性

8.  **#22525 (Closed, P1)**: **跨用户对话数据泄露**
    - **为什么重要**: 本周最严重的隐私安全事件。CLI 突然开始输出另一位用户（波兰语/荷兰语）的完整对话内容。这触及了用户对 AI 工具数据隔离能力的信任底线。
    - **社区反应**: 尽管 Issue 已关闭，但该事件在开发者社区中引发的信任震荡仍在持续。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/22525

9.  **#23627 (Closed)**: **Agent 思考 30 分钟无进展**
    - **为什么重要**: Agent 陷入死循环，只读取了一个 `README.md` 文件，卡死半小时。这是 Agent 核心功能稳定性的重大缺陷。
    - **社区反应**: 用户提供了截图，描述了 Agent “只读不写”的死锁状态，影响自动化任务交付。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/23627

10. **#23837 (Closed)**: **YOLO 模式 Agent 误删项目**
    - **为什么重要**: YOLO 模式 Agent 创建了清理脚本并执行 `rm -rf`，导致整个项目目录被清空。暴露出 Agent 在无人干预模式下的安全性严重不足。
    - **社区反应**: 用户表示这只是个人项目且有备份，但明确希望借此报告帮助其他用户避免损失。社区对“无确认执行”的恐惧感上升。
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/23837

---

### 4. 重要 PR 进展

以下 10 个 PR 反映了当前开发团队在修复稳定性、增强安全性及提升性能方面的核心动态。

1.  **#27354 (Open)**: **绕过 WSL 中的 `node-pty` 直接运行 Windows 可执行文件**
    - **核心内容**: 直接回应了当前最严重的 P1 崩溃危机。当在 WSL 中调用 `.exe` 文件时，不再使用脆弱的 `node-pty`，而是回退到 Node.js 标准 `child_process`。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27354

2.  **#27341 (Open)**: **剥离工具调用中的 ID 字段，修复 400 错误**
    - **核心内容**: 修复了 Agent 核心链路的一个根本性缺陷。内部 ID 字段（`functionCall.id`）被错误地发送到了 Gemini API，导致每次工具调用后都返回 `400 Unknown name 'id'`。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27341

3.  **#27329 (Open)**: **跳过缺失的配置目录，避免 CLI 启动崩溃**
    - **核心内容**: 修复了 `settings.json` 中 `context.includeDirectories` 配置了无效路径时，CLI 直接崩溃无法启动的问题。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27329

4.  **#27335 (Open)**: **修复 Web Fetch 工具的 SSRF 漏洞**
    - **核心内容**: 发现 `fetchWithTimeout` 会跟随重定向，但仅检查了初始 URL 的 SSRF 风险。此 PR 增加了对重定向目标的检查，防止攻击者利用开放重定向攻击内网资源。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27335

5.  **#27348 (Open)**: **封装 Ajv 校验异常，防止 Agent 闪退**
    - **核心内容**: 当 LLM 返回了预期之外的参数结构时，Ajv 校验器会抛出 `Cannot read properties of undefined` 导致 Agent 崩溃。通过 `try/catch` 优雅处理，避免服务中断。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27348

6.  **#27347 (Open)**: **防止自然语言被误存为 Shell 命令**
    - **核心内容**: 修复了一个安全隐患，即当用户输入类似自然语言的指令时，原始文本被错误地保存并执行。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27347

7.  **#27349 (Open)**: **剥离模型思考过程中的 CJK 字符**
    - **核心内容**: 修复了当用户使用英文时，模型思考过程偶尔输出中文/日文等字符的体验问题。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27349

8.  **#27028 (Closed)**: **大会话历史 `/chat` 秒开**
    - **核心内容**: 性能优化的大胜利。针对 59 个会话、2.3GB 数据的复杂场景，将加载时间从 25 秒+ 缩短至 634 毫秒（通过流式预读和异步加载策略）。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27028

9.  **#27054 (Closed)**: **支持 Windows 终端图片粘贴**
    - **核心内容**: 针对 Windows Terminal 用户，提供了无缝的剪贴板图片粘贴支持，并优化了粘贴后的 UI 展示效果。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27054

10. **#27056 (Closed)**: **修复 RHEL/CentOS 系统 Shell 执行问题**
    - **核心内容**: 解决了在 RHEL8/9 等企业级 Linux 发行版上，因 `resolveExecutable` 未找到 Shell 路径而报 “Permission denied” 的兼容性 Bug。
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/27056

---

### 5. 功能需求趋势

从今日的 Issue 和 PR 中，可以提炼出社区最关注的几个功能方向：

1.  **终端模拟器（Node-PTY）稳定性重构**：当前压倒一切的技术债。开发社区期望对 PTY 子系统进行一次彻底的审计，提供更稳定的跨平台支持，或像 #27354 这样引入可靠的后备方案，彻底解决 WSL/SSH 下的崩溃问题。
2.  **企业级配额与身份治理**：社区不再满足于简单的“付费解锁”。他们需要**显式的配额仪表盘**、**可预测的重置机制**以及**自由切换企业/消费者身份**的权限控制。这是从个人开发者工具迈向企业级 SaaS 必须跨越的鸿沟。
3.  **Agent 模式的可观测性与安全性**：用户正在从“尝鲜”转向“信任”。Agent 的任务进度条、超时恢复机制、以及更严格的沙箱执行环境（甚至是类似 YOLO 模式下的“预案检查”功能）需求强烈。
4.  **MCP 扩展生态的标准化**：OAuth 与自定义 MCP 服务器的不兼容问题（如 #20017）表明，扩展生态的接入标准（特别是鉴权协议）需要更灵活的处理，不能因为严格的“源校验”而阻止合法的第三方集成。
5.  **数据边界的透明度**：跨用户对话泄露事件后，社区对“数据在管道中如何流转”提出了更高的透明度要求，并要求提供更强大的数据隔离承诺。

---

### 6. 开发者关注点

总结今日反馈中开发者最感痛点的几个高频词：

- **不稳定**：P1 级别的崩溃让开发者对将 CLI 纳入自动化工具有了强烈的顾虑。`EBADF` 错误成为开发者的梦魇。
- **不透明**：配额消耗的逻辑、封禁的标准、身份路由的选择，对用户来说都是黑盒。开发者希望获得“发生了什么”和“为什么发生”的清晰日志与解释。
- **不一致**：付费了 Premium/Pro 计划，却无法使用宣传中的最新模型，或者企业协议的保护在路由过程中被静默降级，这种“付费即降级”的体验让开发者感到被欺骗。
- **不兼容**：WSL 和 Linux 是主力开发环境，但 CLI 在这些平台上的 Bug 数量和质量严重影响了开发者的使用信心。开发者呼吁团队完善针对 WSL/SSH 场景的回归测试。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-05-29

## 今日速览
今日发布 v1.0.56-0 与 v1.0.56-1 两个补丁版本，修复了上下文窗口 Tier 持久化和粘贴光标偏移等关键问题。社区方面，**#3560 一类 "Duplicate item found" WebSocket 错误** 在近 24 小时内集中爆发，大量用户反映涉及工具调用的工作流完全中断，成为今日最具破坏力的稳定性事件。同时 **#3539 关于 MCP/插件导致上下文窗口被过度预占** 和 **#3565 Task 工具静默降级模型** 的讨论表明，深度用户对架构层面的资源管控和模型路由策略表达了强烈不满。

---

## 版本发布

### v1.0.56-1
- **改进**
  - Code Review Agent 现在跟随当前会话模型，不再使用固定默认模型。
  - 当 `gh` CLI 在 PATH 中时，GitHub MCP Server 默认隐藏冗余的 gh 可替代工具，降低 Token 消耗。
- **修复**
  - 粘贴文本后光标不再跳到错误位置。

### v1.0.56-0
- **改进**
  - “受信任文件夹”确认消息明确了权限可能会在会话期间被记忆保留。
- **修复**
  - 上下文窗口 Tier 选择现在能够在 SDK 恢复路径下持久生效，确保压缩和截断逻辑正确。

> 昨日发布的 v1.0.55 也于 5/28 生效，支持了 Claude Opus 4.8、报告 Claude 推理 Token、以及免费/学生计划限制 Auto 模型选择。

---

## 社区热点 Issues（Top 10）

1. **[#3560 / #3559 / #3558] WebSocket Duplicate item found 错误**（labels: `context-memory`, `models`, `sessions`）
   - **摘要**：大量用户反馈会话工具调用后突现 `Duplicate item found with id fc_call_xxx`，导致请求全部失败。纯文本聊天正常，涉及函数调用的流程完全不可用。
   - **评论**：共 10+ 条，分布于三个 issue。用户怀疑是服务端限流或会话状态重放 BUG。
   - **链接**: github/copilot-cli Issue #3560

2. **[#1274] CLI 代码审查功能遭遇大量 400 错误**（labels: `tools`）
   - **摘要**：过去数小时内约 95% 的代码审查（Code Review）请求返回 400 `invalid request body`。用户提供了详细 Debug 日志，疑似客户端构建了异常请求体。
   - **评论**：24 | 👍：11
   - **链接**: github/copilot-cli Issue #1274

3. **[#3539] System/Tools 预占 73% 上下文窗口**（labels: `context-memory`, `plugins`, `mcp`）
   - **摘要**：配置约 10 个 MCP 服务器和插件后，System/Tools 部分消耗 146k tokens（200k 窗口下预占 73%），导致新会话第一条消息就触发自动压缩。
   - **评论**：3 | 👍：2
   - **链接**: github/copilot-cli Issue #3539

4. **[#3042] "ask" 权限决策导致双重确认弹窗**（labels: `permissions`, `plugins`）
   - **摘要**：PreToolUse 钩子返回 `permissionDecision: "ask"` 后，用户不仅要确认钩子提供的自定义弹窗，还会再次弹出原生信任提示，彻底违背了"询问一次"的预期。
   - **评论**：3 | 👍：0
   - **链接**: github/copilot-cli Issue #3042

5. **[#3565] Task 工具静默降级子代理模型**（labels: `agents`, `models`）
   - **摘要**：Subagent 在 frontmatter 中声明的高价模型，只要被父会话的模型 cost multiplier 阻挡，就会被静默降级为父会话模型，且用户无任何提示。
   - **评论**：0（刚刚提交，但重要性极高）
   - **链接**: github/copilot-cli Issue #3565

6. **[#223] 企业级 Token 缺少 "Copilot Requests" 权限选项**（labels: `permissions`, `enterprise`, `networking`）
   - **摘要**：组织创建的 Fine-grained Token 中找不到 "Copilot Requests" 权限，导致企业无法限制用户使用个人 PAT 进行自动化。
   - **评论**：27 | 👍：73
   - **链接**: github/copilot-cli Issue #223

7. **[#3527] contextTier 设置在会话启动时不生效**（labels: `context-memory`, `models`, `configuration`）
   - **摘要**：用户通过 `/model` 手动设置的长上下文 Tier 被写入 settings.json，但新会话默认仍回退到 200k 窗口，必须重新设置。
   - **评论**：2 | 👍：0
   - **链接**: github/copilot-cli Issue #3527

8. **[#3543] 启动因递归读取 COPILOT_CUSTOM_INSTRUCTIONS_DIRS 卡死 15-30 秒**（labels: `context-memory`, `configuration`）
   - **摘要**：当环境变量指向 HOME 或包含大子树时，启动阶段无边界递归 Glob 导致 TUI 完全无响应。
   - **评论**：1 | 👍：0
   - **链接**: github/copilot-cli Issue #3543

9. **[#3339] 路径扫描器误判引号参数为文件路径**（labels: `permissions`, `tools`）
   - **摘要**：任何以 `/` 开头的 Shell 引号参数（如 `echo "/flag"`）都会被判定为文件读写意图，触发无意义的权限确认和误报。
   - **评论**：1 | 👍：0
   - **链接**: github/copilot-cli Issue #3339

10. **[#1044] 非交互模式 (copilot --acp) 不支持斜杠命令**（labels: `non-interactive`）
    - **摘要**：Zed 等编辑器通过 Agent 协议接入时，服务端不推送 `available_commands_update`，导致 `/help` 等命令完全不可用。
    - **评论**：15 | 👍：0
    - **链接**: github/copilot-cli Issue #1044

---

## 重要 PR 进展

过去 24 小时内 GitHub Copilot CLI 仓库无新的 Pull Request 更新。v1.0.56-0 和 v1.0.56-1 的修复内容已直接推送至 main 分支。

---

## 功能需求趋势

- **MCP 精细化管控**：社区不再满足于"能用 MCP"，而是要求能够**逐一启用/禁用**（#3564）、**启动时自动启用特定 Server**（#3548）、以及保证**非结构化内容正确传递**（#3258）。
- **大上下文模型解锁**：随着 Claude Opus 4.8 / 4.6 支持，用户强烈要求 CLI **解除 200K 硬上限**（#3355），发挥模型原生 1M Token 能力。
- **企业治理功能**：**细粒度权限**（#223）和**安全审查命令**（#1133）是当前企业落地的主要诉求，社区期待类比 Claude Code 的 `/security-review`。
- **会话与集成体验**：**非交互模式功能补齐**（#1044）、**IDE 设置同步**（#39）、**会话 ID 显示**（#3566）标签量上升，代表从"终端玩具"向"IDE 工作流核心"转变的需求。

---

## 开发者关注点

- **稳定性滑坡**：近 24 小时内集中爆发的 **WebSocket Duplicate ID 错误**（#3560）和持续存在的 **400 审查错误**（#1274）严重动摇了核心工作流的可靠性，成为开发者首要关注的风险项。
- **配置持久化难题**：用户的个性化设置（`contextTier`、MCP 权限等）在会话重启或系统恢复后频繁走失（#3527），导致"必须重新配置"成为高频痛点。
- **插件生态认知门槛高**：权限系统（双重确认 #3042）、上下文预占（#3539）、钩子失效（#2540）等问题让第三方插件开发和深度使用困难重重，亟需官方给出最佳实践指导。
- **模型能力与消费不匹配**：用户为更智能的模型付费，却面临**静默降级**（#3565）和**上下文窗口强制阉割**（#3355），性价比争议正在积聚。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-05-29 Kimi Code CLI 社区动态日报。

---

# Kimi Code CLI 每日社区日报 | 2026-05-29

**数据来源：** github.com/MoonshotAI/kimi-cli

---

## 1. 今日速览
*   **版本更迭进行时：** 今日无正式发布，但 `v1.46.0` 的版本提升流程已通过 PR #2391 启动。
*   **“Kimi Code”重构版引热议：** 产品方向的重大变动引发了社区强烈的不满与信任危机（#2381），如何平稳过渡并安抚现有用户是当前最大的社区管理挑战。
*   **稳定性修复密集推进：** 上下文压缩导致的导出崩溃（#2396）、大上下文网络超时（#2384）、会话记录恢复失败（#2383）等核心稳定性问题正在被集中修复，开发者对生产环境可用性的诉求愈发强烈。

---

## 2. 版本发布
*   **[新版本预告：v1.46.0 即将到来]**
    *   过去 24 小时无正式版本发布。但维护者已提交 `chore(release): bump kimi-cli to 1.46.0` 的 PR #2391，用于同步版本号及依赖。预计新版本将在近期发布。

---

## 3. 社区热点 Issues
以下挑选的 10 个 Issue 涵盖了今日社区最关注的话题（受数据源限制，共 8 条，均已分析）。

### ❗️ 情绪最高：产品方向与信任危机
*   **#2381：为什么抛弃 kimi-cli 重做 kimi code？**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2381](https://github.com/MoonshotAI/kimi-cli/issues/2381)
    *   **重要性：** 🔥🔥🔥 影响社区存续的关键情绪。用户严厉批评项目方放弃现有产品线，认为此举严重分裂社区、破坏信任基础。
    *   **社区反应：** 评论区3条评论情绪激烈，均表达了对长期投入该工具的不安，甚至有人表示考虑退订。这是官方必须回应的重大关切。

### ❗️ 最紧急的 Bug：导出崩溃与连接超时
*   **#2396：Bug：`kimi export` 因上下文压缩崩溃**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2396](https://github.com/MoonshotAI/kimi-cli/issues/2396)
    *   **重要性：** ❗️❗️❗️ 严重 Bug。`kimi export` 在上下文压缩阶段因传递空白 `TextPart` 导致 Moonshot API 返回 400 错误。修复 PR #2395 已迅速跟进。

*   **#2384：Bug：大上下文请求频繁 ConnectTimeout**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2384](https://github.com/MoonshotAI/kimi-cli/issues/2384)
    *   **重要性：** ❗️❗️ 高危痛点。当上下文超过 120k Token 后，每次请求都出现连接超时，且 `httpx` 的超时参数未暴露给用户配置。这对重度用户的日常使用造成了严重阻塞。

### ❗️ 协议与功能缺口：生态整合与竞品对齐
*   **#2394：功能需求：ACP 服务端未暴露 Token 用量**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2394](https://github.com/MoonshotAI/kimi-cli/issues/2394)
    *   **重要性：** ❗️❗️ IDE 集成重要缺口。当作为 ACP 服务器运行时，Kimi 内部计算的 Token 消耗未传递给宿主应用（如 Zed），阻碍了第三方平台进行用量管理。

*   **#1894：功能需求：无法递归加载嵌套 Skill 目录**
    *   **链接：** [MoonshotAI/kimi-cli Issue #1894](https://github.com/MoonshotAI/kimi-cli/issues/1894)
    *   **重要性：** ❗️❗️ 与 Codex 的功能对齐问题。社区期待 Kimi 能像 Codex 一样支持 `.agents/skills/{name}/skills/xxx` 的层级结构，以便组合更复杂的 AI 工作流。目前已有 5 条评论表示关注。

### ❗️ IDE 集成具体 Bug
*   **#2385：Bug：在 Zed 中查找文件陷入死循环**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2385](https://github.com/MoonshotAI/kimi-cli/issues/2385)
    *   **重要性：** ❗️ 集成场景 Bug。用户报告通过 ACP 协议在 Zed 中使用文件查找功能时，触发了死循环。表明 ACP 文件系统交互仍有边缘情况需要覆盖。

### ❗️ 已修复的里程碑
*   **#2127：已修复：未实现 `session/list`、`session/get` 等 ACP 方法**
    *   **链接：** [MoonshotAI/kimi-cli Issue #2127](https://github.com/MoonshotAI/kimi-cli/issues/2127)
    *   **重要性：** 回顾性里程碑。之前报告的 Zed 无法加载历史会话问题，已通过合入 PR #2132 完全解决，补全了 ACP 协议的关键一环。

*   **#1984：已修复：退出时终端挂起与 MCP 连接泄漏**
    *   **链接：** [MoonshotAI/kimi-cli Issue #1984](https://github.com/MoonshotAI/kimi-cli/issues/1984)
    *   **重要性：** 稳定性里程碑。长期困扰用户的长会话后 `/exit` 导致终端无响应的问题，已由 PR #1985 合入修复，并清理了进程残留的 MCP 孤儿连接。

---

## 4. 重要 PR 进展
以下挑选了 10 个过去 24 小时内更新的重要 Pull Request。

### 🔧 核心稳定性修复
*   **#2395 [OPEN] `fix(compaction)：过滤空白 TextPart 避免 API 400`**
    *   **链接：** [MoonshotAI/kimi-cli PR #2395](https://github.com/MoonshotAI/kimi-cli/pull/2395)
    *   **摘要：** 快速响应 Issue #2396，在消息压缩路径上增加了空白文本过滤，防止因历史消息中的空白 `TextPart` 导致 API 拒绝服务。
*   **#2383 [OPEN] `fix(soul)：修复会话回放时的孤立 Tool Calls`**
    *   **链接：** [MoonshotAI/kimi-cli PR #2383](https://github.com/MoonshotAI/kimi-cli/pull/2383)
    *   **摘要：** 高可用性修复。当进程被异常终止（OOM / `kill -9`）导致 `context.jsonl` 文件损坏时，此 PR 通过嫁接或清除孤立的 `tool_call`，确保 Session 能够成功加载恢复。
*   **#1985 [CLOSED] `fix(term, app)：解决退出挂起与 MCP 连接泄漏`**
    - **链接：** [MoonshotAI/kimi-cli PR #1985](https://github.com/MoonshotAI/kimi-cli/pull/1985)
    - **摘要：** 已合入。通过设置非阻塞读取和规范关闭流程，解决了终端退出挂起，并确保子 MCP 连接在 Shutdown 时被正确清理。

### 🧩 ACP 协议与 IDE 生态完善
*   **#2047 [OPEN] `fix(acp)：ACP 模式下加载 ~/.kimi/mcp.json`**
    - **链接：** [MoonshotAI/kimi-cli PR #2047](https://github.com/MoonshotAI/kimi-cli/pull/2047)
    - **摘要：** 重大功能补全。此前只有交互模式支持用户自定义 MCP 工具。此 PR 使 `kimi acp` 模式也能加载本地 MCP 配置，填平了 IDE 集成场景下的关键体验差。
*   **#2132 [CLOSED] `fix(acp)：重放 Session 历史记录`**
    - **链接：** [MoonshotAI/kimi-cli PR #2132](https://github.com/MoonshotAI/kimi-cli/pull/2132)
    - **摘要：** 已合入。通过持久化 `wire history` 并在 `session/load` 时完整重放，彻底解决了 Zed 等客户端无法恢复历史会话的问题。
*   **#2394 [OPEN] `feat(acp)：向 ACP 客户端暴露 Token 用量`**
    - **链接：** [MoonshotAI/kimi-cli PR #2394](https://github.com/MoonshotAI/kimi-cli/issues/2394)
    - **摘要：** 社区呼声较高的功能。虽然当前 Issue 形式提出，但推动了 ACP 协议中 Token 用量信息的标准化传输。

### 💡 用户体验与工具链改进
*   **#2389 [OPEN] `fix(tools)：Shell 错误简报包含尾部输出`**
    - **链接：** [MoonshotAI/kimi-cli PR #2389](https://github.com/MoonshotAI/kimi-cli/pull/2389)
    - **摘要：** 当 Shell 命令执行失败时，AI 收到的错误简报现在会追加命令末尾的输出内容，大幅提升了自己排查错误的能力。
*   **#2388 [OPEN] `fix(shell)：持久化粘贴文本占位符`**
    - **链接：** [MoonshotAI/kimi-cli PR #2388](https://github.com/MoonshotAI/kimi-cli/pull/2388)
    - **摘要：** 修复了一个烦人的 UX Bug。长文本粘贴被折叠为 `[Pasted text #1]` 后，在对话历史回放时因对象引用丢失导致失效。此 PR 对占位符进行了持久化。
*   **#2386 [OPEN] `fix(session)：映射 Undo 操作到正确的上下文轮次`**
    - **链接：** [MoonshotAI/kimi-cli PR #2386](https://github.com/MoonshotAI/kimi-cli/pull/2386)
    - **摘要：** 修复 `/undo` 和 `fork` 命令错误地根据 `wire.jsonl` 索引而非 `context.jsonl` 索引进行截断的问题。此前本地斜杠命令轮次会导致 Undo 回滚异常。
*   **#2387 [OPEN] `fix(tools)：保留 Shell 命令标题详情`**
    - **链接：** [MoonshotAI/kimi-cli PR #2387](https://github.com/MoonshotAI/kimi-cli/pull/2387)
    - **摘要：** 优化 UI 显示。当 Shell 命令过长时，不再粗暴地截断标题，而是保留命令的关键头部细节，让 AI 和用户能在界面上一目了然地看到命令概览。

### 🚀 产品战略与性能
*   **#2393 [CLOSED] `docs：更新演化 Banner 宣告重构版发布`**
    - **链接：** [MoonshotAI/kimi-cli PR #2393](https://github.com/MoonshotAI/kimi-cli/pull/2393)
    - **摘要：** 产品沟通动作。将文档站 Banner 从“升级提示”改为宣布“Kimi Code 重构版发布”，并链接到新仓库。与 #2381 的社区质疑形成对仗。
*   **#2369 [OPEN] `feat(subagent)：为并行子 Agent 增加 API 密钥池`**
    - **链接：** [MoonshotAI/kimi-cli PR #2369](https://github.com/MoonshotAI/kimi-cli/pull/2369)
    - **摘要：** 面向高级自动化场景。引入轮询的 API Key 分配器，支持多个子 Agent 并行独立执行任务，极大提升了并行吞吐量。

---

## 5. 功能需求趋势

从近期社区活跃的 Issue 及 PR 中，可以提炼出以下三大趋势：

1.  **ACP 协议全面深化（IDE 生态上位）**：社区不再满足于“能用”，而是对 ACP 协议提出了极高的完整性要求。从 Session 生命周期管理（#2127, #2386）、Token 用量监控（#2394）到本地 MCP 配置加载（#2047），每个环节都在被社区检视和推动。这预示着 Kimi 正被广泛地作为智能体后端接入各种 IDE（尤其是 Zed）。

2.  **Agent 能力的可组合性（微调 Agent 行为）**：Issue #1894 对“递归 Skill 目录”的持续关注，以及 #2369 对“并行子 Agent”的功能突破，表明用户渴望构建复杂的、分层调用的 Agent 协作系统，而不仅仅是单次问答。社区正在推动 Kimi 从“Chat CLI”向“Agent 编排引擎”演进。

3.  **生产环境的可观测性与韧性**：大量的 Bug 修复集中在“异常中断后恢复”（#2383）、“大数据量下的稳定性”（#2384, #2396）以及“资源的优雅释放”（#1985）。这说明大量开发者已将其应用于真实工作流，对底层稳定性和可控性的容错率极低。

---

## 6. 开发者关注点

*   **首要痛点：对产品方向骤变的信任危机**
    *   从 Issue #2381 的激烈措辞来看，最大的痛点不是技术 Bug，而是“安全感”的缺失。开发者投入时间和精力学习、配置、依赖一个工具，最担心的就是项目方“另起炉灶”导致既有投入沉没。维护者能否给出一个清晰的旧版维护计划或平滑迁移路径，是缓解当前社区情绪的关键。

*   **高频诉求：对“黑盒参数”的可控性**
    *   Issue #2384 是一个典型代表。开发者能容忍特定的网络环境限制，但无法容忍一个“不可配置”的错误。网络超时、Token 窗口限制、重试策略等核心参数迫切需要向用户开放，让开发者能根据自身网络环境和任务复杂度进行精细调优。

*   **被压缩的 Bug 容错空间**
    *   当用户开始将 Kimi 用作日常编码的“副驾驶”时，每一个体验上的小瑕疵都会被放大。无论是 ACP 协议里的死循环（#2385）、粘贴历史的丢失（#2388），还是复杂工作流下的崩溃（#2396），都在不断消耗重度用户本已脆弱的耐心。社区正在用自己的使用场景帮助 Kimi 项目团队发现大量边界问题。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是为您生成的 2026-05-29 OpenCode 社区动态日报。

---

## OpenCode 社区动态日报 | 2026-05-29

### 今日速览
v1.15.12 发布，新增 WebSocket 传输支持以及 ACP 集成增强。社区层面，GPT 模型响应延迟的讨论持续高温（#29079），多起文件被 AI 静默覆盖/删除的严重报告（#29764、#29779）引发了对 Agent 安全机制的广泛担忧。开发侧积极响应，并行子任务调度（#29819）和关键 Deny 规则修复（#29755）等高价值 PR 已迅速落地。

---

### 版本发布

**v1.15.12**
- **核心改进**：ACP 集成可通过 `acp-next` 发送 prompts、slash commands 及使用更新；新增实验性 WebSocket 传输支持（`OPENCODE_EXPERIMENTAL_WEBSOCKETS=true`）。
- **Bug 修复**：为 Anthropic 模型启用了适应性推理控制。
[查看完整 Release](https://github.com/anomalyco/opencode/releases/tag/v1.15.12)

---

### 社区热点 Issues

1. **#29079 GPT Models takes too long to respond** 🔥
   - 描述：GPT 5.4 等模型响应速度极不稳定，简单命令也需数分钟。
   - 分析：共 104 条评论、48 个 👍，是当前最热的性能相关 Issue，严重影响了核心工作流。
   [链接](https://github.com/anomalyco/opencode/issues/29079)

2. **#11176 [Feature] Official VS Code Extension** 🔝
   - 描述：希望 OpenCode 能作为原生 VS Code 扩展运行，而非独立桌面应用。
   - 分析：获 91 个 👍，是社区长期以来最想要的功能，表明用户迫切希望将 AI 编码工具嵌入现有 IDE。
   [链接](https://github.com/anomalyco/opencode/issues/11176)

3. **#28846 Adjust Go usage limits after DeepSeek V4 Pro price cut** 💰
   - 描述：DeepSeek V4 Pro API 降价 75%，用户要求 OpenCode Go 订阅同步上调用量限制。
   - 分析：获 46 个 👍，反映出社区对 AI 成本的高度敏感，且希望订阅计划能跟随市场波动灵活调整。
   [链接](https://github.com/anomalyco/opencode/issues/28846)

4. **#27530 Startup error: “4 of 5 requests failed”** 🚨
   - 描述：启动时出现 `config.providers` 请求失败，导致应用完全无法加载。
   - 分析：19 条评论，这是影响新用户上手的严重阻塞性 Bug。
   [链接](https://github.com/anomalyco/opencode/issues/27530)

5. **#29764 [Critical] LLM 指令导致文件被误删** 💀
   - 描述：Agent 通过工具调用无理由地删除或覆盖用户文件，且缺乏预警机制。
   - 分析：尽管只有 3 条评论，但性质极其严重，直指 Agent 安全底线的缺失。
   [链接](https://github.com/anomalyco/opencode/issues/29764)

6. **#29571 GitHub Copilot provider 报 vision 未启用后对话卡死** 🐛
   - 描述：当组织禁用图片支持时，该会话永久卡死直至用户手动清理。
   - 分析：典型的供应商特定边缘用例，但处理不良会导致整个会话不可用。
   [链接](https://github.com/anomalyco/opencode/issues/29571)

7. **#28686 Desktop V2 UI 隐藏了模型选择器与状态弹窗** 🎨
   - 描述：V2 新 UI 中 Agent 选择器、推理级别切换及 MCP 状态弹窗被隐藏。
   - 分析：社区普遍认为这是 UI 重构中的功能性倒退，影响对 AI 行为的控制感。
   [链接](https://github.com/anomalyco/opencode/issues/28686)

8. **#26772 [Feature] Integrated browser workspace** 🌐
   - 描述：希望在 Desktop 中集成浏览器，方便 AI 直接审查和交互网页内容。
   - 分析：扩展了 AI 工具的能力边界，从代码审查延伸到 Web 探索与测试。
   [链接](https://github.com/anomalyco/opencode/issues/26772)

9. **#29779 write/edit tools silently abort for files > 6KB** 🔧
   - 描述：大于 6KB 的文件写入/编辑会静默中止，仅返回 `Tool execution aborted`，无错误详情。
   - 分析：严重限制了 Agent 处理大文件的能力，且缺乏回退机制，可靠性差。
   [链接](https://github.com/anomalyco/opencode/issues/29779)

10. **#29051 V2 prompt 输入框隐藏推理模式选择器** ⚠️
    - 描述：Beta/Dev 版 V2 输入框不显示模型变体（如推理级别）的切换入口。
    - 分析：与 #28686 同为 V2 UI 的弊端，核心功能不完整导致用户体验断层。
    [链接](https://github.com/anomalyco/opencode/issues/29051)

---

### 重要 PR 进展

1. **#29819 fix: dispatch subtasks in parallel** 🚀
   - 背景：`runLoop` 中 `handleSubtask` 原为串行执行。
   - 影响：子 Agent 现在并行运行，极大提升多 Agent 协作效率。这是当前最受关注的性能优化 PR。
   [链接](https://github.com/anomalyco/opencode/pull/29819)

2. **#29755 fix: enforce read deny rules in glob and grep results** 🔒
   - 背景：`opencode.jsonc` 中 `**/.env*` 等 Deny 规则因通配符匹配 Bug 完全失效。
   - 影响：修复了敏感文件保护机制，是本次日报周期中最关键的安全修复。
   [链接](https://github.com/anomalyco/opencode/pull/29755)

3. **#29820 fix: serialize mcp-auth.json writes** 🛡️
   - 背景：`McpAuth.set()` 和 `remove()` 存在并发写入竞态条件。
   - 影响：防止 Token 刷新时 JSON 文件损坏，保护了 MCP 认证数据的完整性。
   [链接](https://github.com/anomalyco/opencode/pull/29820)

4. **#29217 feat: Add inline $skill invocations** ✨
   - 描述：在 TUI Prompt 编辑器中支持 `$` 触发技能自动补全，支持 `prepend` 和 `pasteText`。
   - 影响：增强了终端内的交互效率，让技能调用更流畅自然。
   [链接](https://github.com/anomalyco/opencode/pull/29217)

5. **#29803 fix: bump node-pty to fix Windows desktop crash** 🪟
   - 描述：升级侧车依赖 `node-pty` 至 beta.12。
   - 影响：彻底解决 Windows 下侧车进程反复崩溃和 Log 刷屏问题，改善跨平台体验。
   [链接](https://github.com/anomalyco/opencode/pull/29803)

6. **#29738 fix: update skill handling in context and permissions** 👤
   - 描述：修复 `/skills` 列表未遵守权限限制，以及技能在某些上下文中无法正常工作的问题。
   - 影响：权限模型更加严谨，技能展示与可用性更加符合预期。
   [链接](https://github.com/anomalyco/opencode/pull/29738)

7. **#29812 feat: add menu item to open config file** ⚙️
   - 描述：在桌面端菜单和命令面板中新增打开配置文件的快捷方式。
   - 影响：方便用户快速编辑 JSON 配置，提升高级用户开发体验。
   [链接](https://github.com/anomalyco/opencode/pull/29812)

8. **#29814 feat: sort skills alphabetically** 🔤
   - 描述：`/skills` 命令现在按字母顺序展示所有技能。
   - 影响：提升技能列表的可查找性，解决因顺序随机化带来的查找困难。
   [链接](https://github.com/anomalyco/opencode/pull/29814)

9. **#29710 fix: prevent prompt corruption when pasting near wide characters** 🐛
   - 描述：修复粘贴文本附近含有宽字符（如中文）时，输入框出现文字错乱的问题。
   - 影响：修复了影响非英语用户的 TUI 显示 Bug。
   [链接](https://github.com/anomalyco/opencode/pull/29710)

10. **#29705 fix: resolve snapshots from git subdirectories** 🗂️
    - 描述：修复 OpenCode 从 Git 子目录启动时，快照功能解析路径错误的问题。
    - 影响：完善了工作区管理，确保在复杂项目结构中 Snapshot 功能可用。
    [链接](https://github.com/anomalyco/opencode/pull/29705)

---

### 功能需求趋势

从社区的 Issues 和讨论中可以明显看出几个需求方向：
1. **IDE 原生集成是首要期盼**：#11176（VS Code 扩展）获得压倒性支持，用户希望 AI 编码体验直接嵌入编辑器。
2. **自动化与平台独立性**：内置任务调度（#11232）以减少对 OS 级别工具的依赖，是目前公认的易用性短板。
3. **极致成本与模型灵活度**：DeepSeek 降价引发的额度调整诉求（#28846），以及对 Azure 等第三方模型完整特性的兼容需求（#29776），说明用户群对模型性价比和多元化部署要求越来越高。
4. **Agent 安全与管控**：用户开始警惕 AI 的“破坏性”行为，文件误删（#29764）和权限失控（#29727）催生了更强的内置防护机制需求。
5. **Agent 行为透明化**：V2 UI 隐藏核心控件（#28686, #29051）引发了强烈反弹，用户需要清晰地看到 Agent 的推理等级、工具调用状态和 MCP 连接情况。

---

### 开发者关注点

1. **性能与稳定性的双重夹击**：GPT 响应过慢（#29079）与工具静默失败（#29779）并存，同时数据被误删（#29764）的担忧加剧，信任危机是当前最大的痛点。
2. **UI 重构的磨合阵痛**：V2 新 UI 在功能完整性上出现了明显倒退，模型选择器、状态弹窗等核心入口缺失（#28686, #29051），表明 UI 重构需要优先补齐语义和功能控制点。
3. **第三方模型兼容性吃力**：Qwen 配额问题（#23722）、Opus 工具调用失败（#23464）、Azure 模型 Token 上限（#29776）等问题，说明对非 OpenAI 生态的支持优化仍有很大空间。
4. **安全权限的底线博弈**：LD 一键覆写文件（#29764）和 Deny 规则绕过（#29755）暴露了当前 Agent 权限模型的脆弱性，开发者希望不要完全依赖 LLM 的“良心”来做安全决策。
5. **跨平台体验仍有落差**：Windows 端侧车持续崩溃（#29803）在修复前是平台用户的日常噩梦，提示生态扩展过程中需维护统一的用户体验基线。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，以下是为您生成的 2026-05-29 Pi 社区动态日报。

---

## Pi 社区动态日报 | 2026-05-29

### 1. 今日速览
- **v0.77.0 发布**，核心功能包括对 **Claude Opus 4.8** 的原生支持以及呼声很高的 **`--exclude-tools`** 选择性禁用工具功能。
- **OpenAI Codex 交互卡死问题**（[#4945]）以45条评论成为今日讨论最激烈的话题，暴露出流式场景下的严重稳定性隐患。
- 社区开发重心向 **扩展生态深度建设**（暴露远程控制API、流式行为通知）和 **跨平台兼容性修复**（tmux、WSL、Windows路径检测）转移。

### 2. 版本发布
- **[v0.77.0](https://github.com/earendil-works/pi/releases/tag/v0.77.0)**
  - **Claude Opus 4.8 支持**：新增 Anthropic Claude Opus 4.8 元数据，并更新了 Opus 的 adaptive-thinking 覆盖范围。
  - **选择性禁用工具**：新增 `--exclude-tools` / `-xt` 参数，允许按需禁用特定内置、扩展或自定义工具，在简化上下文的同时保留其余功能。

### 3. 社区热点 Issues
1.  **[#4945] [OPEN] OpenAI Codex 交互卡死**（45 条评论 | 22 👍）
  - *重要性*：`openai-codex` 模式下 TUI 频繁卡死在 `Working...` 状态，无任何错误提示，只能通过 Escape 强制中止。近几日频繁复现，严重影响核心工作流。
2.  **[#5148] [CLOSED] Claude 思考后切换到 ChatGPT 5.5 报 400 错误**（6 👍）
  - *重要性*：跨模型会话恢复时出现消息 ID 冲突。如果 Claude 产生了 extended-thinking，后续切回 GPT-5.5 会因 `Duplicate item found with id` 完全失效，暴露了多 Provider 切换的大坑。
3.  **[#5087] [CLOSED] GPT-5.5 上下文窗口被限缩至 272K**（4 条评论）
  - *痛点*：官方标称 1M 窗口的 GPT-5.5，在 Pi 中上限被错误设定为 272K。这是一个明显的元数据配置错误，会导致用户在处理长上下文任务时被系统限制。
4.  **[#5145] [CLOSED] 技能目录中的 `.gitignore` 导致技能不被加载**（4 条评论）
  - *隐蔽性*：只要技能文件夹内存在 `.gitignore` 文件，即使 `SKILL.md` 本身未被忽略，整个技能对加载器来说也是完全不可见的。对使用 Git 管理技能库的用户来说是致命坑。
5.  **[#5117] [OPEN] Qwen 3.7 Max 在 OpenRouter 上无法使用**（3 条评论）
  - *兼容性*：新模型使用了 `developer` 角色，但该角色不符合 Pi 默认的 `system/assistant/user/tool` 校验规则，直接被 API 网关拒绝。
6.  **[#5103] [OPEN] Windows 下 Git Bash 非默认路径检测失败**（4 条评论）
  - *平台痛点*：当 Git Bash 安装在非 `C:\Program Files` 路径时（如 D 盘），即使 PATH 正确，bash 工具也会报告“未发现 Shell”。
7.  **[#5098] [OPEN] tmux 环境下内联图片和方向键失效**（2 条评论）
  - *环境限制*：`detectCapabilities` 在有 `$TMUX` 变量时无条件返回 `images: null`，导致内联图片完全无法显示，同时方向键可能错乱。
8.  **[#5102] [OPEN] 中文输入法候选框在斜杠命令补全时错乱**（2 条评论）
  - *CJK 用户痛点*：使用拼音输入法时，一旦 `/` 触发自动补全菜单，IME 候选框定位错乱，严重影响非英文用户的日常交互。
9.  **[#5132] [CLOSED] 系统提示词列出了未注册的工具**（3 条评论）
  - *指令污染*：编码代理的系统提示词中，只要注册了 `grep/find/ls` 中任意一个，就会提示模型去使用全部三个，属于典型的指令与上下文脱节。
10. **[#5040] [OPEN] `PI_CODING_AGENT_SESSION_DIR` 强制扁平化存储**（3 条评论）
  - *功能回退*：设置该环境变量后，会话被平铺存储，导致“Current folder”筛选逻辑失效，所有会话混在一起，破坏了工作区隔离性。

### 4. 重要 PR 进展
1.  **[#5091] [CLOSED] 加固 TUI 键盘协议协商**
  - *内容*：针对不同终端模拟器键盘输入协议（如 Kitty Keyboard Protocol）的兼容性修复，旨在根治 #3259 等输入问题。
2.  **[#4978 / #5107] [CLOSED] 向扩展 InputEvent 暴露 `streamingBehavior`**
  - *内容*：为扩展的 `input` 事件增加 `streamingBehavior` 字段，使扩展能区分“新对话”、“流中插入（steer）”和“后续跟进（followUp）”，是构建智能交互扩展的关键基础设施。
3.  **[#4911] [CLOSED] 为 Codex 增加设备码登录**
  - *内容*：新增 Device Code Login 流程，方便在无头服务器或不可用 OAuth 浏览器的终端中进行 Codex 认证。
4.  **[#5029] [CLOSED] 销毁 AgentSession 时中止正在进行的 LLM 请求**
  - *内容*：修复了会话切换（`switchSession`、`fork` 等）时，旧会话的 LLM HTTP 请求未被取消而继续运行的内存与性能泄漏问题。
5.  **[#5144] [CLOSED] 修复 `result.content` 为 `undefined` 时的渲染崩溃**
  - *内容*：当工具返回的 `Result` 对象缺少 `content` 数组时，`getTextOutput()` 会直接 `TypeError`。该 PR 增加了守卫逻辑，防止渲染链因边界情况崩溃。
6.  **[#5140] [CLOSED] 为远程控制扩展增加 API（RFC）**
  - *内容*：贡献者分享了其远程控制扩展的 6 个 API 增强（如 `ctx.executeInputLine`）。这是 Pi 扩展向非 TUI 端（如手机 App、Web 桥接）开放的里程碑提案。
7.  **[#5118] [CLOSED] 缓冲在 `tool_calls` 之前到达的 `reasoning_details`**
  - *内容*：修复 OpenRouter 类 Provider 的流式时序问题——`reasoning_details` 可能先于 `tool_calls` 块到达，旧逻辑因 ID 不存在而直接丢弃，此 PR 通过缓冲机制修复。
8.  **[#5085] [CLOSED] 扩展 `getAllTools` 暴露完整工具定义**
  - *内容*：允许扩展获取当前已注册工具的完整 Schema（只读副本），这对开发元编程工具（如手动调用任意工具的调试面板）至关重要。
9.  **[#5156] [OPEN] 新增 `--name/-n` CLI 参数设置会话名**
  - *内容*：一个简单直接的易用性改进。之前只能在 TUI 中用 `/name` 命令改名，现在可以在启动时就通过命令行参数指定会话名称。
10. **[#5110] [OPEN] 新增 Ant-ling Provider**
  - *内容*：社区贡献者提交了新 Provider 支持，带来了 Ling-2.6-1T / flash 和 Ring-2.6-1T 模型系列，并定制了 OpenAI Completions 兼容层，进一步拓宽 Pi 模型矩阵。

### 5. 功能需求趋势
- **“万能网关”模型矩阵继续扩张**：从 Ant-ling、NVIDIA NIM、Anthropic Vertex 到 K2.6，社区对**新模型的首时间支持**有着强烈的本能需求，希望 Pi 成为所有 AI 能力的统一入口。
- **扩展系统走向深度平台化**：`getAllTools` 暴露、`streamingBehavior` 通知、远程控制 API，这些改动表明 Pi 的扩展正在从“简单添加工具”向 **“打造插件化操作系统”** 演进。
- **追求极致的按需定制**：`--exclude-tools` 和 `--system-prompt` 支持文件引用等需求，反映出高级用户希望**精细控制 Agent 的上下文与能力集**，而非接受固定的全能配置。
- **CI/脚本化使用场景成熟**：`--name/-n` 参数、Codex 设备码登录等 PR 表明，Pi 不仅仅是一个交互式终端，正在被集成到**自动化工作流和持续集成管道**中。

### 6. 开发者关注点（痛点）
- **流式/生命周期稳定性仍是头号敌人**：[#4945]（Codex 卡死无反馈）和 [#5029]（Dispose 未中止请求）说明会话管理和流式响应处理中存在**严重影响体验的硬伤**，社区对此类不稳定容忍度极低。
- **Provider 兼容性矩阵的技术债**：从 `developer` 角色报错、消息 ID 冲突到上下文窗口错误配置，跨 Provider 的**细微差异**是用户踩坑的最主要来源，维护成本和复杂度非常高。
- **Windows 平台的二等公民感**：Git Bash 路径检测、WSL 分支显示卡死、安装器颜色花屏……**Windows 相关的 Bug 数量密集**，说明该平台在测试覆盖和体验打磨上仍有差距。
- **隐蔽的边缘 Case 导致心智负担**：`.gitignore` 让技能消失、`result.content` 为空直接崩溃、存储路径不按预期工作……这些**不在常规测试路径里的 Bug** 往往让开发者在排查时耗费大量时间。

[#4945]: https://github.com/earendil-works/pi/issues/4945
[#5148]: https://github.com/earendil-works/pi/issues/5148
[#5087]: https://github.com/earendil-works/pi/issues/5087
[#5145]: https://github.com/earendil-works/pi/issues/5145
[#5117]: https://github.com/earendil-works/pi/issues/5117
[#5103]: https://github.com/earendil-works/pi/issues/5103
[#5098]: https://github.com/earendil-works/pi/issues/5098
[#5102]: https://github.com/earendil-works/pi/issues/5102
[#5132]: https://github.com/earendil-works/pi/issues/5132
[#5040]: https://github.com/earendil-works/pi/issues/5040
[#5091]: https://github.com/earendil-works/pi/pull/5091
[#4978]: https://github.com/earendil-works/pi/pull/4978
[#5107]: https://github.com/earendil-works/pi/pull/5107
[#4911]: https://github.com/earendil-works/pi/pull/4911
[#5029]: https://github.com/earendil-works/pi/pull/5029
[#5144]: https://github.com/earendil-works/pi/pull/5144
[#5140]: https://github.com/earendil-works/pi/pull/5140
[#5118]: https://github.com/earendil-works/pi/pull/5118
[#5085]: https://github.com/earendil-works/pi/pull/5085
[#5156]: https://github.com/earendil-works/pi/pull/5156
[#5110]: https://github.com/earendil-works/pi/pull/5110

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# 2026-05-29 Qwen Code 社区动态日报

## 今日速览
昨日，Qwen Code 发布了 nightly 版本 v0.16.1-nightly.20260529，修复了启动警告输出问题。社区围绕 **daemon 架构改进** 与 **核心会话压缩模型替换** 展开深入讨论；同时，**IDE 登录失败** 和 **SSL 证书错误** 等阻断性问题集中出现，引发关注。此外，**内置 Computer Use** 与 **全局用量统计** 等功能需求热度持续上升。

## 版本发布
- **v0.16.1-nightly.20260529.7bed56b9b**  
  - 修复 CLI 在 TUI 渲染前将启动警告输出到 stderr（#4448，贡献者 @kagura-agent）。  
  - 随附 TUI 间距密度 PR1 的终端验证证据。  
  [查看 Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.16.1-nightly.20260529.7bed56b9b)

## 社区热点 Issues（10 条）
1. **#4175 – Mode B feature-priority roadmap toward v0.16 production-ready**  
   讨论 `qwen serve` 剩余工作路线图，覆盖 daemon 稳定性、遥测对齐、错误处理等，已有 41 条评论，社区高度关注。  
   [链接](https://github.com/QwenLM/qwen-code/issues/4175)

2. **#3004 – [P1] API Exponential Backoff & Fallback Retry**  
   用户要求实现指数退避与模型降级重试，应对 API 限流和故障，被标记为 P1 高优。  
   [链接](https://github.com/QwenLM/qwen-code/issues/3004)

3. **#3696 – [P1] comprehensive hot-reload system for skills, extensions, MCP, and configuration**  
   希望无需重启即可热加载技能、扩展、MCP 和配置，社区正拆分子任务。  
   [链接](https://github.com/QwenLM/qwen-code/issues/3696)

4. **#2128 – [P1] Memory grows unboundedly during long sessions**  
   UI 历史数组无限增长导致内存泄漏，长期运行会话的关键性能瓶颈，仍在分析中。  
   [链接](https://github.com/QwenLM/qwen-code/issues/2128)

5. **#4493 – rider 无法登录 qwen code**  
   Rider IDE 用户反馈 OAuth 登录出现无限重定向，无法关联阿里云 token plan，影响使用。  
   [链接](https://github.com/QwenLM/qwen-code/issues/4493)

6. **#4597 – 增强 stats 能力，支持跨 session 的全局用量统计**  
   希望 `/stats` 命令持久化追踪跨会话统计，并引入全屏仪表盘，对标 Claude Code，获得社区点赞。  
   [链接](https://github.com/QwenLM/qwen-code/issues/4597)

7. **#4586 – PyCharm 终端中使用 qwen cli 按 Ctrl+C 导致意外退出 agent**  
   升级后 Ctrl+C 易退出 CLI，ESC 无法中断对话，影响复制文本，是体验痛点。  
   [链接](https://github.com/QwenLM/qwen-code/issues/4586)

8. **#4612 & #4611 – SSL 证书无效致阻塞开发**  
   连续两报告指出 `coder.qwen.ai` SSL 证书链错误，被标为紧急，当天关闭（可能已修复），凸显证书管理风险。  
   [#4612](https://github.com/QwenLM/qwen-code/issues/4612) [#4611](https://github.com/QwenLM/qwen-code/issues/4611)

9. **#4591 – Built-in Computer Use support with zero-config**  
   提议将桌面应用操控作为内建能力，无需额外配置，注册 9 个命令工具，反映 Agent 桌面操控期待。  
   [链接](https://github.com/QwenLM/qwen-code/issues/4591)

10. **#4592 – refactor: replace tail-preservation compaction with summary + restoration attachments**  
    借鉴 Claude Code 思路，用“全历史摘要 + 压缩后附件还原”替代当前截断方式，是 core 层重要改进提议。  
    [链接](https://github.com/QwenLM/qwen-code/issues/4592)

## 重要 PR 进展（10 条）
1. **#4599 – refactor(core)!: replace tail-preservation compaction with summary + restoration attachments**  
   对应 #4592，实现基于 summary+restoration 的压缩模型，避免历史丢失，核心架构重大变更。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4599)

2. **#4590 – feat(computer-use): zero-config built-in via open-computer-use MCP**  
   内置计算机操作能力，集成 9 个工具，支持多平台，无需手动安装（已合并）。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4590)

3. **#4563 – refactor(serve): extract DaemonWorkspaceService from AcpSessionBridge**  
   将工作区能力抽取为独立服务，清理 HTTP 桥接层职责，daemon 架构重构关键一步。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4563)

4. **#4608 – feat(telemetry): add tool spans and session.id to daemon/ACP path**  
   在 daemon 路径添加工具调用和会话 ID 追踪，补齐与 CLI 的遥测差异，提升可观测性。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4608)

5. **#4333 – feat(core): atomic write rollout for credentials, memory, config, JSONL**  
   Phase 2 原子写改造，覆盖密钥、内存、配置和 JSONL 文件，防止中断致数据损坏。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4333)

6. **#4520 – fix(core): truncate model-facing tool output**  
   对模型可见的工具输出截断，防止上下文爆满，完整输出保存至临时文件，多处边界改进。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4520)

7. **#3826 – fix(cli): track model-sent slash command history**  
   修复 CLI 中模型触发斜杠命令不被记录的问题，确保用户侧可回溯模型操作。  
   [链接](https://github.com/QwenLM/qwen-code/pull/3826)

8. **#4600 – fix(ui): distinguish auto approval mode indicators**  
   区分自动批准模式（auto-accept vs classifier auto-mode）的视觉颜色，避免用户混淆。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4600)

9. **#4552 – feat(serve): runtime MCP server add/remove**  
   新增运行时添加/移除 MCP 服务的 HTTP 路由，无需重启 daemon，提升服务灵活性。  
   [链接](https://github.com/QwenLM/qwen-code/pull/4552)

10. **#3778 – feat(desktop): Add desktop app package with Qwen ACP SDK integration**  
    新增 `packages/desktop` 桌面应用包，集成 ACP SDK，探索桌面客户端形态。  
    [链接](https://github.com/QwenLM/qwen-code/pull/3778)

## 功能需求趋势
从过去 24 小时的 Issue 和 PR 可观察到以下社区关注方向：

- **Daemon / Server 模式成熟化**：Mode B 路线图（#4175）、工作空间服务抽取（#4563）、遥测补齐（#4602, #4608）表明团队正全力推动 daemon 走向生产可用。
- **会话内存与历史管理革新**：多个 P1 问题（#2128, #3004, #3696）和核心 PR（#4599, #4520）聚焦于控制上下文膨胀、热加载配置和持久化管理。
- **IDE 生态融合与体验优化**：JetBrains Rider 登录失败（#4493）、PyCharm Ctrl+C 误退（#4586）、VSCode fetch 兼容（#4589）反映多 IDE 场景仍需适配。
- **新能力边界：Computer Use & 桌面应用**：内置桌面操作（#4591）和独立桌面客户端（#3778）表明 Qwen Code 正从终端走向桌面环境。
- **可观测性与统计增强**：全局用量统计（#4597）、请求级日志（#4606）和跨 session 追踪（#4608）是运营分析的基础需求。
- **安全与合规**：原子写（#4333）、SSL 证书警报（#4612,#4611）、AUTO 分类器权限钩子（#4376）显示社区对安全性和数据完整性的重视。

## 开发者关注点
- **登录与认证**：Rider IDE 无法登录（#4493）、SSL 证书失效（#4612,#4611）直接阻碍用户上手，是最紧迫的阻断问题。
- **稳定性痛点**：长会话内存无限增长（#2128）、API Body Timeout（#4604）、本地模型报 `DOMException`（#4609）影响日常使用可靠性。
- **CLI 交互细节**：Ctrl+C 意外退出（#4586）、`/clear` 误换 session（#4593）、自动模式 emoji 冗余（#4584）等小问题累积降低信赖感。
- **API 错误处理期待**：用户多次提出指数退避与降级重试（#3004），当前仅有简单重试计数，不足以应对复杂网络和限流场景。
- **配置与工具热更新需求**：希望不重启会话即可更新 MCP、扩展、技能（#3696），运行时 MCP 增删已通过 PR#4552 实现初版。
- **跨设备/IDE 一致性**：用户期望 Web、IDE、CLI 中体验一致，当前 daemon 和 CLI 路径功能仍有隙缝（#4602）。

---

*数据来源：GitHub QwenLM/qwen-code，更新于 2026-05-29*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# 2026-05-29 DeepSeek TUI 社区动态日报

> 数据来源：github.com/Hmbown/CodeWhale（DeepSeek TUI 项目代号 CodeWhale）

---

## 今日速览

今天社区迎来多个关键修复与功能 PR：**斜杠命令转义**（#2340）、**中文输入法兼容**（#2330）、**缓存状态诊断命令 `/cache stats`**（#2336）三大痛点同期得到解决。社区对非 DeepSeek 模型支持（#2300 / #2337）以及自定义 API 提供商（#2247）的呼声持续升高，项目正加速向通用 AI 编码平台演进。

---

## 版本发布

过去 24 小时内无新版本发布。

---

## 社区热点 Issues（精选 10 条）

1. **#2310 无法以斜杠开头发送消息**（bug）  
   - 任何以 `/` 开头的输入均被解析为命令，无转义机制。直接影响日常交流，已有 #2340 / #2316 修复 PR 跟进。  
   - 作者: zhyuzhyu | 更新: 2026-05-29 | 评论: 1  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2310)

2. **#2323 未适配中文输入法（IME）**（bug / enhancement）  
   - 中文输入法下拼音提示不隐藏、按键进入错误区域，严重阻碍中文用户。同天 #2330 PR 已给出修复方案。  
   - 作者: cmdcorp6534 | 更新: 2026-05-28 | 评论: 1  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2323)

3. **#2247 支持自定义 DeepSeek 兼容 API 提供商**（enhancement）  
   - 目前仅支持官方 API，无法接入第三方或本地部署的 DeepSeek 兼容服务。社区长期 Top 需求。  
   - 作者: hatakes | 更新: 2026-05-28 | 评论: 4  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2247)

4. **#2339 tool_search 默认结果数太少，埋没 MCP 工具**（bug / documentation）  
   - 工具搜索默认返回 5 条，多 MCP 服务关键词重叠时导致工具不可见，期望增至 20 条。  
   - 作者: T-Phuong-Nguyen | 创建: 2026-05-29 | 评论: 0  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2339)

5. **#2300 兼容多模型支持**（enhancement）  
   - 完善多模型文档、支持同时配置多个模型并根据任务自动选择。平台化的关键诉求。  
   - 作者: gavinwang668 | 更新: 2026-05-28 | 评论: 0  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2300)

6. **#2328 exec_shell 工具在 Agent 模式下不可用**（bug / enhancement）  
   - YOLO 模式正常，Agent 模式报错“Tool not available”，与文档描述不一致。影响 Agent 流程的 Shell 操作。  
   - 作者: octasin | 更新: 2026-05-29 | 评论: 1  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2328)

7. **#2303 allow_shell 默认 false 对 exec_shell 和 task_shell_start 拦截不一致**（bug / documentation）  
   - 安全开关应同时阻止两类 Shell 工具，但 `task_shell_start` 可绕过，造成安全模型混乱。  
   - 作者: zlh124 | 更新: 2026-05-28 | 评论: 1  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2303)

8. **#1747 缓存命中问题**（enhancement）  
   - 用户希望 UI 更透明地展示缓存命中过程与稳定性。今日 #2336 PR 通过 `/cache stats` 部分满足了该需求。  
   - 作者: Amund | 更新: 2026-05-28 | 评论: 3 | 👍: 2  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/1747)

9. **#1826 @引用文件时无法按层级快速找到文件**（bug）  
   - 文件选择器缺少目录层级导航，影响文件快速定位。社区 4 条讨论附图复现。  
   - 作者: sun125459586 | 更新: 2026-05-29 | 评论: 4  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/1826)

10. **#2299 要求支持 GLIBC_2.38**（enhancement）  
    - Deepin 等系统因 GLIBC 版本不足（2.38）无法运行当前二进制。Linux 发行版兼容性常见诉求。  
    - 作者: Jengro777 | 更新: 2026-05-28 | 评论: 1  
    - [GitHub 链接](https://github.com/Hmbown/CodeWhale/issues/2299)

---

## 重要 PR 进展（精选 10 条）

1. **#2340 fix(tui): treat slash-space input as message text**  
   - `/` 后紧跟空格时视为普通消息，保留 `/help` 等命令行为。直接解决 #2310。  
   - 作者: nightt5879 | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2340)

2. **#2330 fix(tui): route IME-committed Chinese characters directly to composer**  
   - 修复在无 bracketed paste 的终端（如 Windows Terminal 首会话、SSH、tmux）下中文输入被粘贴缓冲吞没的问题。  
   - 作者: donglovejava | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2330)

3. **#2336 feat: add /cache stats — prefix hash/drift exposure and cache-hit summary**  
   - 新增 `/cache stats` 子命令，显示前缀缓存稳定性指纹、检查变化次数及命中摘要。针对 #2264 的低风险实现。  
   - 作者: encyc | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2336)

4. **#2338 feat: whale-size route taxonomy for model + thinking-effort picker**  
   - 为 DeepSeek 提供商引入“鲸鱼大小”路线分类，让模型 / 推理努力选择更直观（从大到小排序）。  
   - 作者: encyc | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2338)

5. **#2333 feat(hooks): add UnixSocketHookSink for real-time event streaming**  
   - 新增 Unix Socket hook sink，支持外部监控面板或通知系统实时消费生命周期事件，扩展钩子系统 IPC 能力。  
   - 作者: lihuan215 | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2333)

6. **#2332 feat(tui): add render diff debug log**  
   - 通过环境变量 `CODEWHALE_TUI_DEBUG=1` 开启每帧渲染差异日志（大小、cell、坐标），方便调试 TUI 问题。  
   - 作者: cyq1017 | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2332)

7. **#2329 fix(tui): skip hidden worktrees in workspace discovery**  
   - 跳过 `.claude/worktrees/` 等隐藏 git worktrees，避免子代理并发扫描导致大量 I/O 和 TUI 饱和。性能优化。  
   - 作者: donglovejava | 更新: 2026-05-29 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2329)

8. **#2331 fix(tools): eagerly load all exec_shell companion tools**  
   - 将六个 Shell 伴随工具（exec_interact / exec_wait / task_shell_start 等）加入默认加载列表，修复 Agent 模式下部分工具不可用。  
   - 作者: donglovejava | 更新: 2026-05-28 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2331)

9. **#2326 feat: enforce allowed tools for custom slash commands**  
   - 解析自定义命令 frontmatter 中的 `allowed-tools`，实现自定义斜杠命令的工具权限控制。自定义命令生命周期的第一阶段。  
   - 作者: aboimpinto | 更新: 2026-05-28 | 状态: OPEN  
   - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2326)

10. **#2302 fix(tui): replace standalone compacting label with animated working label**  
    - 将压缩阶段静态 “compacting” 文字替换为带秒数的动画工作标签，消除用户感觉“卡住”的错觉。  
    - 作者: donglovejava | 更新: 2026-05-29 | 状态: OPEN  
    - [GitHub 链接](https://github.com/Hmbown/CodeWhale/pull/2302)

---

## 功能需求趋势

从近期 Issues 可提炼出以下社区最关注的功能方向：

- **模型与提供商扩展**：要求支持非 DeepSeek 模型（GLM / Qwen / OpenAI 兼容）及自定义 API 提供商，实现多模型自动路由。这是平台化的首要需求。
- **国际化与中文支持**：中文输入法兼容、中文乱码、长回复阻塞等问题频繁出现，中文用户群体正在快速增长。
- **缓存与性能透明度**：开发者渴望更清晰地了解前缀缓存命中状态与会话稳定性， `/cache stats` 的推出正是响应。
- **安全性与权限控制**：`allow_shell` 拦截不一致、自定义命令权限等议题反映出社区对细粒度安全模型的重视。
- **开发者文档与兼容性**：配置目录混乱、GLIBC 版本依赖高、文档与实际行为不符等，要求项目提升文档同步质量和二进制兼容性。

---

## 开发者关注点（痛点 / 高频需求）

- **中文环境体验**：多个 Issue 反映 TUI 下中文输入法出现拼音提示不隐藏、字符被吞等问题，严重阻碍中文用户。今日 #2330 已给出修复，但仍需持续观察。
- **斜杠消息无法发送**：无法以 `/` 开头发送普通消息，属于基础交互缺陷，社区反应迅速。
- **模式间工具不一致**：`exec_shell` 在 Agent 模式不可用，与文档描述矛盾，导致用户多次尝试失败。
- **工作区发现性能**：隐藏 git worktrees 导致扫描膨胀，TUI 卡顿。 #2329 针对此优化。
- **GLIBC 版本依赖过高**：`GLIBC_2.39` 要求导致 Deepin 等系统无法运行，限制了用户覆盖。
- **配置目录迁移混乱**：`~/.codewhale` 与 `~/.deepseek` 双目录并存，文档未及时同步，建议新用户混淆。
- **缓存黑盒**：用户希望明确了解前缀缓存命中情况以优化成本， #2336 是将缓存白盒化的第一步。

---

*本期日报基于 GitHub Issue / PR 公开信息生成，涵盖 2026-05-28 至 2026-05-29 的社区动态。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*