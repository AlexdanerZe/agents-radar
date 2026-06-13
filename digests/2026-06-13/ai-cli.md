# AI CLI 工具社区动态日报 2026-06-13

> 生成时间: 2026-06-13 03:25 UTC | 覆盖工具: 9 个

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

# 2026-06-13 AI CLI 工具横向对比分析报告

---

## 1. 生态全景

当前 AI CLI 工具正从“单模型对话终端”快速进化为“多 Agent 协作操作系统”。社区对 **Agent 安全性、成本可观测性、跨平台兼容性** 的关注达到新高峰；各工具普遍陷入“功能快速迭代 vs 稳定性失控”的矛盾期——Fable 5 大面积不可用、Copilot CLI 连续两版致命回归、Codex Windows 沙箱反复失败等事件表明，用户对服务可用性和版本质量的容忍度正在下降。与此同时，多提供商解绑（Claude、Gemini、Qwen 均在支持外部模型）、持久化工作流（Cron、Session 压缩）、Agent 架构分层（大脑+工人、舰队调度）成为共同演进方向。

---

## 2. 各工具活跃度对比

| 工具 | 今日精选 Issues | 重要 PR 进展 | 版本发布 | 社区情绪 |
|------|---------------|-------------|---------|---------|
| Claude Code | 10 | 1 | 3 (v2.1.175–177) | 焦虑（宕机+成本失控） |
| OpenAI Codex | 10 | 10 | 4 (rust alpha .14–.17) | 密集但稳定（Windows 痛点） |
| Gemini CLI | 10 | 10 | 1 (nightly) | 中性（Agent 可靠性待提升） |
| GitHub Copilot CLI | 10 | 1 | 1 (v1.0.62-1) | 信任危机（连续 Bug） |
| Kimi Code CLI | 3 | 1 | 0 | 付费用户不满（计费争议） |
| OpenCode | 10 | 10 | 0 | 讨论活跃（数据层+权限） |
| Pi (pi-mono) | 10 | 10 | 1 (v0.79.2) | 积极（多 Provider 扩展） |
| Qwen Code | 10 | 10 | 1 (v0.18.0) | 谨慎（OAuth 调整引争论） |
| DeepSeek TUI (CodeWhale) | 10 | 10 | 1 (v0.8.59) | 高迭代（舰队调度+解耦） |

> *Issues/PR 数据取自各日报“社区热点 / 重要 PR”精选列表，不代表当日全量；版本发布为日报明确提及的最近发布。*

---

## 3. 共同关注的功能方向

### ① Agent 安全与成本失控
- **Claude Code** – 子 Agent 递归无限制导致指数级 Token 消耗（#68110）
- **Gemini CLI** – 子代理达到 MAX_TURNS 仍误报成功（#22323），通用代理挂起（#21409）
- **Qwen Code** – 取消后工具继续执行（#5016）、重复工具调用被错误执行（#5015）
- **GitHub Copilot CLI** – MCP 无退避无限重连（#3782）
- **社区诉求**：递归深度上限、预算控制、取消语义保证、失败透明

### ② 成本/Token 消耗透明度
- **Claude Code** – 用户要求可知模型降级原因、自动重试（Fable 5 事件）
- **Kimi Code CLI** – 计费标准不透明，2 小时额度仅能执行 2 次（#1994）
- **GitHub Copilot CLI** – 系统提示词固定消耗 3 万 tokens，用户称“空气税”（#2627）
- **Pi** – `maxTokens` 对推理模型不生效（#5595），成本显示浮点尾数清理（PR #5634）
- **社区诉求**：Token 预估、按任务动态计费、可配置上下文上限

### ③ 跨平台兼容性（尤其是 Windows）
- **Claude Code** – Windows 安装残骸导致重复失败（#49917）、Ctrl+V 粘贴失效（#68136）
- **OpenAI Codex** – Windows 沙箱 `spawn setup refresh` 失败（#24098）、插件不可用（#25220）、WSL 集成缺口（#25216）
- **Gemini CLI** – Wayland 下浏览器代理不可用（#21983）
- **GitHub Copilot CLI** – 非美式键盘 `@` 无法输入（#1999）、WSL 粘贴乱码
- **OpenCode** – inotify 实例耗尽导致启动挂死（#16610）
- **社区诉求**：环境检测健壮、安装/更新流程无残留、输入法兼容

### ④ 持久化与状态一致性
- **Claude Code** – Cron 任务 `durable:true` 不持久，CLI 退出即丢失（#50911）
- **OpenAI Codex** – CLI 远程压缩失败导致 resumed 线程失去上下文（#22335）
- **OpenCode** – JSON→SQLite 迁移在非 `latest` 渠道每次运行（#16885）
- **Gemini CLI** – Shell 历史记录反斜杠命令合并错误（#27555，已修）
- **社区诉求**：状态可靠持久化、跨会话连续性、可预测的 CLI 行为

### ⑤ Agent 架构分层
- **Claude Code** – Opus 大脑 + Sonnet 工人 + 持久状态（#56913）
- **Pi** – AiGameAgent 领域特定 Agent 整合（PR #5681）
- **DeepSeek TUI (CodeWhale)** – 舰队调度器：租约、心跳、背压（#3159）
- **Gemini CLI** – 组件级评估体系（#24353）、AST 感知文件读取（#22745）
- **社区诉求**：多层 Agent 编排、子 Agent 深度推理、角色自定义

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线 | 差异化优势 |
|------|---------|---------|---------|-----------|
| **Claude Code** | Anthropic 模型专属深度 Agent | 重度开发者、AI 前沿探索者 | TypeScript，Monorepo，深度集成 Claude Fable/Opus | Agent 能力最强，但成本和服务稳定性依赖 Anthropic API |
| **OpenAI Codex** | OpenAI 全栈开发助手 + GPT 生态 | 全栈开发者、企业 | Rust 底层重构，Electron 客户端，MCP 插件，Guardian 安全 | 跨平台执行统一（PathUri），沙箱安全体系完善，但 Windows 体验割裂 |
| **Gemini CLI** | Google Cloud 原生 AI 工具 | GCP 用户、Android 开发者 | Node.js，A2A 协议，Vertex AI 集成，Nightly 迭代 | 与 Google 云服务深度绑定，组件级评估体系；Agent 主动使用率待提升 |
| **GitHub Copilot CLI** | GitHub 工作流嵌入式 AI 助手 | GitHub 重度用户、企业 | VS Code 扩展架构，MCP, YOLO 模式 | IDE 联动最强，Issue/PR 全局搜索；但非英语支持差，版本信任危机 |
| **Kimi Code CLI** | 极简轻量 Kimi 模型终端 | 个人开发者、Kimi 用户 | Node.js，单一模型绑定（K2.6） | 入门简单；但计费不透明，功能迭代慢，社区规模最小 |
| **OpenCode** | 开源通用 Agent 工作台 | 开源社区、自部署团队 | TypeScript，SQLite + permissions 系统，MCP | 权限规则灵活、DB 修复工具；但响应慢（GLM-5 十多分钟），性能待优化 |
| **Pi (pi-mono)** | 多 Provider 通用智能体 CLI | 多模型用户、游戏/安全领域 | TypeScript，插件化 Provider，`AiGameAgent` | 提供商适配最广（Vertex, Bedrock, vLLM），领域 Agent 拓展快；但依赖分裂问题突出 |
| **Qwen Code** | 阿里 Qwen 模型生态 CLI | 阿里云用户、Qwen 开发者 | TypeScript，Daemon 模式，Agent 定义 Frontmatter | 服务端部署（`qwen serve`），多 Provider 配置热重载；但工具调用副作用控制仍需加强 |
| **DeepSeek TUI (CodeWhale)** | 从 DeepSeek 转型通用多 Agent 平台 | Agent 编排用户、CI 集成者 | TypeScript，Fleet 调度，Hooks 系统 | 舰队架构最先进、多 Provider 解绑彻底、TUI 交互深度优化；更名初期认知度重建中 |

---

## 5. 社区热度与成熟度

- **最成熟（用户量大、生态丰富）**：**Claude Code** 与 **OpenAI Codex**。Claude Code 的 Issue 评论动辄上百，但 PR 产出低（今日仅 1 个），显现出核心团队与社区活跃度倒挂。OpenAI Codex 版本迭代密集（每日 4 个 alpha），社区讨论围绕 Windows 和沙箱，成熟度较高但跨平台仍不均衡。
- **高速迭代（版本频繁、PR 活跃）**：**Gemini CLI**、**Pi**、**Qwen Code**、**CodeWhale**。这四款工具每日 PR 数量多（各 10 个），版本发布快（1 个/日），且都在进行架构级重构（多 Provider 支持、Agent 调度）。
- **争议与信任危机**：**GitHub Copilot CLI**。Issue #53 连续 9 个月占据热度榜首，MCP 无限重连、Linux ARM 崩溃等严重回归让社区质疑版本质量。非英语用户问题长期未解决，社区自发维护 Fork。
- **早期阶段（规模小、功能单一）**：**Kimi Code CLI**。仅 3 个活跃 Issue，版本发布停滞，社区讨论集中在计费争议，总体量级远低于其他工具。
- **特色社区（自部署、数据安全敏感）**：**OpenCode**。社区讨论技术深度高（DB 迁移、权限通配符、安全审计），但用户群偏技术向，对响应速度和 IDE 集成诉求强烈。

---

## 6. 值得关注的趋势信号

### 🔴 1. 单点模型依赖风险暴露
Claude Code 的 Fable 5 宕机事件（全平台、无优雅降级）和 Kimi Code 的计费争议表明：**绑定单一模型 / 单一 API 的 CLI 正在遭遇用户信任危机**。行业正快速向“多 Provider 原生支持”演进——Pi、CodeWhale、Qwen Code 均已或正在移除硬编码，支持 Anthropic Vertex、Bedrock Mantle、vLLM DeepSeek 等异构后端。**开发者选型时应关注工具的模型供应商多样性，避免锁死。**

### 🟡 2. “无上限”模式走向终结
Agent 递归失控（Claude Code #68110）、MCP 无限重连（Copilot CLI #3782）、`maxTokens` 不生效（Pi #5595）等事件揭示：**当前 CLI 在成本和资源保护上几乎裸奔**。社区强烈要求递归深度上限、预算阈值、取消语义保证。未来几个季度，**速率限制、预算控制、强制中止**将成为各工具标配，也是企业采购的前提条件。

### 🟢 3. 从 CLI 到“Agent 操作系统”
Claude Code 用户提出“Opus 大脑 + Sonnet 工人 + 持久状态”（#56913），CodeWhale 推出舰队调度器（租约、心跳、背压、收据），Pi 整合领域特定 Agent（AiGameAgent）。AI CLI 不再仅是“对话式编程助手”，而是**长期运行、可编排、具有状态和生命周期的 Agent 操作系统**。这意味着：持久化存储、跨会话记忆、角色系统、权限审计将从“锦上添花”变为“刚需”。

### 🟠 4. 成本可观测性成为基础能力
从 KIMI 的“2 小时用 2 次”到 Copilot 的“3 万 token 空气费”，社区对 Token 消耗的敏感度显著提高。多款工具已开始增加成本指标（Copilot CLI 请求 OTel 输出 #3778、Pi 规范化成本数据 PR #5634）。**未来，按任务/Agent 粒度的成本分解、实时 token 计数器、预算告警将决定生产力工具能否进入企业预算体系。**

### 🔵 5. 开源治理模式分化
OpenCode、Pi、CodeWhale 等较新项目采用“社区 PR 驱动 + 快速合并”模式（今日 PR 10 个），迭代活力强；而 Claude Code、Copilot CLI 等背靠商业公司的工具 PR 数量少（1 个），版本回退成本高。**决策者可依据自身对迭代速度 vs 商业支持的权重进行选型：前者适合前沿探索团队，后者适合需要稳定支撑的企业。**

---

*报告基于 2026-06-13 各工具 GitHub 社区动态生成，数据来源见对应日报。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

### Claude Code Skills 社区热点报告
**数据截止 2026-06-13**

---

### 一、 热门 Skills 排行

以下按社区关注度与讨论活跃度排序，聚焦 8 个最受瞩目的 PR：

**1. Skill Creator 全线 Bug 修复（run_eval.py 核心问题 / Windows 兼容）**
- **PR**: [#1298](https://github.com/anthropics/skills/pull/1298)、[#1099](https://github.com/anthropics/skills/pull/1099)、[#1050](https://github.com/anthropics/skills/pull/1050) 等
- **功能**：系统性修复 `run_eval.py` 在多个环境下始终输出 `recall=0%` 的致命问题，以及 Windows 下子进程、编码、管道读取的一系列兼容性 Bug。
- **热点**：这是整个 Skill 生态的「卡脖子」问题。Issues #556、#1169 多人复现，评测循环全面失效导致开发者无法正常进行描述优化。多个 PR 相互竞争/互补，论证非常激烈。
- **状态**：Open（急需合并一个整合修复版本）

**2. Agent-Creator 元技能 + 多工具评估修复**
- **PR**: [#1140](https://github.com/anthropics/skills/pull/1140)
- **功能**：新增 Meta-Skill 实现「技能生成技能」，用于动态产出任务导向的 Agent 工具集。同时修复了 `evaluation.py` 在并行多工具调用时崩溃的问题。
- **热点**：社区对 Agent 自主构建工作流的探索，以及与 Issues #202（skill-creator 需重写为最佳实践）的联动。
- **状态**：Open

**3. 测试模式（testing-patterns）**
- **PR**: [#723](https://github.com/anthropics/skills/pull/723)
- **功能**：综合测试技能，涵盖 AAA 模式、React Testing Library 准则、不可测试代码的识别。
- **热点**：填补了官方测试领域的空白，社区讨论集中在测试边界定义和断言规范上，认为这是控制 AI 生成代码质量的关键。
- **状态**：Open

**4. 多项新技能批量提交（前端设计 / 自动化工作流等）**
- **PR**: [#1046](https://github.com/anthropics/skills/pull/1046)
- **功能**：一次性提交 `frontend-design`、`ai-experience-consultant`、`automation-workflows-builder` 三项技能。
- **热点**：代表了社区贡献的爆发式增长和创意溢出，涵盖 UX 到工程化全流程。
- **状态**：Open

**5. 文档排版质量控制（document-typography）**
- **PR**: [#514](https://github.com/anthropics/skills/pull/514)
- **功能**：自动检测 AI 生成文档中的孤词（orphan）、寡段（widow）、编号错位。
- **热点**：极其实用的排版洁癖 Skill，用户希望在所有长文档生成场景中默认启用，社区在讨论排版规则的精确度。
- **状态**：Open

**6. 元技能评价与安全分析**
- **PR**: [#83](https://github.com/anthropics/skills/pull/83)
- **功能**：`skill-quality-analyzer` 与 `skill-security-analyzer`，用于评估其他技能的结构、文档质量及安全问题。
- **热点**：社区开始自发应对「技能质量参差不齐」和「信任边界危机」（关联 Issue #492），是生态自我调节的体现。
- **状态**：Open

**7. N8n 工作流与上下文管理**
- **PR**: [#190](https://github.com/anthropics/skills/pull/190)
- **功能**：集成 n8n 工作流构建、调试，以及 FAF 持久化上下文技能。
- **热点**：社区对「AI 驱动的自动化工作流」的热切期待，直接补上了低代码集成的空缺。
- **状态**：Open

**8. SAP 预测分析与企业级 Skills**
- **PR**: [#181](https://github.com/anthropics/skills/pull/181)
- **功能**：调用 SAP 开源的 Tabular Foundation Model 进行业务数据预测分析。
- **热点**：垂直行业深度应用的代表，展示了 Skills 突破常规代码生成进入商业智能领域的潜力。
- **状态**：Open

---

### 二、 社区需求趋势

1. **工具链稳定性与跨平台支持**
   Issues #556（recall=0% 评测崩坏）、#1169（直接输 slash-command 也无 recall）、#1061（Windows 三连击）。**社区最强烈的呼声是「先让开发者工具可用」。** 当前的 `skill-creator` 流程在非 MacOS 环境下基本不可用，直接扼杀了技能优化迭代的闭环。

2. **企业级安全治理与平台诉求**
   Issue #492（社区技能命名空间信任边界漏洞）、#228（组织级共享）、#412（Agent 治理技能提案）。企业用户关心的是如何在团队内安全地分发和管控技能，以及如何防范恶意或低质量的第三方技能。

3. **生态互操作性（MCP 与平台解耦）**
   Issue #16（将 Skills 暴露为 MCP）、#29（Bedrock 兼容性）。社区不满足于 Skills 仅在 Claude Code CLI 内生效，希望将其标准化为跨平台、跨应用的 AI 工具协议。

4. **技能打包与上下文效率**
   Issue #1220（多文件预加载/内联打包）。优质技能通常需要大量参考文件，但当前只能在 `SKILL.md` 中分发的机制已接近极限，社区需要更高效的分发和注入方案。

---

### 三、 高潜力待合并 Skills

以下 PR 解决核心痛点且未被合入，预计近期落地的概率较大：

| 排名 | PR # | 技能 / 修复 | 近期合并概率 | 理由 |
|------|------|-------------|-------------|------|
| 1 | [#1298](https://github.com/anthropics/skills/pull/1298) | `run_eval.py` 修复（0% recall） | **极高** | 直接解锁生态健康循环，Anthropic 必须解决 |
| 2 | [#1140](https://github.com/anthropics/skills/pull/1140) | `agent-creator` 元技能 | **较高** | 契合 Agent 化趋势，且附带工具链修复 |
| 3 | [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` | **较高** | 功能完整，社区呼声最高的质量基石之一 |
| 4 | [#514](https://github.com/anthropics/skills/pull/514) | `document-typography` | **中等** | 小而美，单点突破价值显著 |

---

### 四、 Skills 生态洞察

**当前社区最集中的核心诉求是：在贡献者疯狂涌入构建各类场景化技能的同时，Skill 的创建、评测与分发工具链严重滞后（评测循环失效、Windows 崩溃），叠加命名空间安全与组织治理的信任赤字，正在制造生态扩张的最大瓶颈——社区不缺创意，缺一个稳定可靠且可验证的技能创作基础设施。**

---

好的，以下是根据截至 2026-06-13 的 GitHub 动态为您生成的 Claude Code 社区日报。

---

## Claude Code 社区动态日报 | 2026-06-13

**📆 今日速览**

- **Fable 5 模型突发大面积不可用**：大量用户在会话中遭遇 `claude-fable-5` 无权限错误，被强制降级至 Opus，引发社区数十条紧急 BUG 报告和强烈舆情。
- **Agent 递归失控漏洞被曝光**：通用子 Agent 可无限递归调用 `Agent` 工具，导致指数级 Token 消耗。Agent 安全性与成本控制成为焦点。
- **版本小步迭代**：发布 v2.1.177，v2.1.176 带来多语言标题支持与 Anazon Bedrock 凭据改进。

---

### 🚀 版本发布

| 版本 | 更新摘要 |
|------|---------|
| **v2.1.177** | 滚动发布（未提供详细变更说明）。 |
| **v2.1.176** | 新增 `footerLinksRegexes` 配置项以支持底部链接正则匹配；会话标题自动使用对话语言；改进 Amazon Bedrock 凭证处理流程。 |
| **v2.1.175** | 新增 `enforceAvailableModels` 受管设置，强化模型白名单约束，防止用户/项目设置绕过管理限制。 |

---

### 📌 社区热点 Issues（Top 10）

#### 1. Fable 5 模型大面积不可用与强制降级
**核心报告**：[#68129](https://github.com/anthropics/claude-code/issues/68129)、[#68131](https://github.com/anthropics/claude-code/issues/68131)、[#68128](https://github.com/anthropics/claude-code/issues/68128)、[#68126](https://github.com/anthropics/claude-code/issues/68126)、[#68137](https://github.com/anthropics/claude-code/issues/68137) 等
- **社区反应**：涌入超过 **10+** 条独立报告，覆盖 macOS / Linux / Windows 全平台，Max 付费用户同样中招。
- **影响**：会话中途模型不可用且没有优雅降级策略，用户需手动 `/model` 切换，直接打断工作流。将 Opus 作为兜底方案引发了重度用户对模型性能缩水的强烈不满。

#### 2. [Agent 递归失控] 子 Agent 无限制分裂导致成本爆炸
[#68110](https://github.com/anthropics/claude-code/issues/68110)
- **Bug**：通用子 Agent 拥有 `Agent` 工具权限，可无限递归调用孙 Agent。无深度/数量上限约束，导致 Token 消耗呈指数级增长。
- **重要性**：这是一个深层的 Agent 架构安全漏洞，影响所有使用子 Agent 进行任务分解的用户。社区担忧在没有预算控制机制的情况下，Agent 会成为不可控的成本黑洞。

#### 3. [严重] Claude Code 随机冻结 / 挂起 5-20 分钟
[#26224](https://github.com/anthropics/claude-code/issues/26224) （👍 142, 💬 116）
- **Bug**：大量 Prompt 执行时 CLI 进程完全挂起无响应，持续时间长，严重影响生产效率。
- **现状**：Open 状态，持续 4 个月，是社区呼声最高、影响最大的稳定性问题。

#### 4. 自主 Agent 架构讨论：Opus 大脑 + Sonnet 工人 + 持久状态
[#56913](https://github.com/anthropics/claude-code/issues/56913) （💬 26）
- **Feature**：提议将 Claude Code 从“结对编程助手”升级为长期运行的“大脑级”编排器。
- **讨论**：用户期望用 Opus 做决策，Sonnet 执行具体任务，并建立持久化状态。这代表了社区对下一代 Agent 操作系统的强烈向往。

#### 5. [需求爆发] Team 套餐急需比 Premium 6.25x 更高的等级
[#47509](https://github.com/anthropics/claude-code/issues/47509) （👍 37）
- **Feature**：重度用户认为 Premium 6.25x 的倍数不够，而 Max 个人版 20x 又无法在团队中共享，强烈要求推出 Team 版高阶倍数（如 12x - 15x）。

#### 6. Windows 安装包残骸导致重复安装失败
[#49917](https://github.com/anthropics/claude-code/issues/49917) （💬 26）
- **Bug**：之前“成功”安装留下的不一致状态导致后续安装失败（HRESULT 0x80073CF6）。
- **影响**：Windows 平台的持久性痛点，严重影响新用户上手和版本回退。

#### 7. Agent 利用 `SendMessage` 工具延续性被破坏
[#38183](https://github.com/anthropics/claude-code/issues/38183) （👍 21, 💬 19）
- **Bug**：由于 `resume` 参数的移除，Agent 引用的 `SendMessage` 工具在恢复会话时不可用，导致 Agent 无法跨轮次保持上下文。
- **影响**：这是一个回归性 BUG，直接破坏了 Agent 在长对话中的核心连续性功能。

#### 8. 子 Agent 无法使用扩展思考能力
[#14321](https://github.com/anthropics/claude-code/issues/14321) （👍 25）
- **Feature**：主 Agent 可以享受 Extended Thinking，但分发出去的子 Agent 无法开启，限制了深度推理在 Agent 层级体系中的发挥。

#### 9. Cron 定时任务持久化完全失效
[#50911](https://github.com/anthropics/claude-code/issues/50911)
- **Bug**：`CronCreate` 的 `durable: true` 参数形同虚设，任务仅存在于当前 Session，CLI 退出后即丢失，不写入 `.claude/scheduled_tasks.json`。

#### 10. Fable 分类器/内容策略误伤开发行为
[#67688](https://github.com/anthropics/claude-code/issues/67688)、[#68130](https://github.com/anthropics/claude-code/issues/68130)
- **Bug**：用户用 Fable 5 编写 Ansible 脚本或使用 Playwright 做本地登录测试时，被内容策略判定违规，直接降回 Opus。
- **社区反应**：用户对黑盒的风控策略表示沮丧，认为误杀率过高且缺乏有效的申诉/恢复机制。

---

### 🔧 重要 PR 进展

**本期仅有 1 条 PR 更新，但其修复至关重要：**

- **#26360** [Fix issues being auto-closed despite human activity](https://github.com/anthropics/claude-code/pull/26360)
    - **状态**：已合入（Closed）
    - **摘要**：修复了 Triage 机器人自动关闭 Issue 的机制。此前即使有人类参与讨论，若未移除 `stale`/`autoclose` 标签，仍可能被自动关闭。此 PR 从根本上优化了 Issue 治理策略。考虑到 Fable 5 宕机事件刚刚爆发，此修复对保证海量 BUG 报告的可见性尤为关键。

---

### 📈 功能需求趋势

从本周期的 Issue 中，可以提炼出社区最关注的三大方向：

1.  **Agent 从“工具”向“系统”演进**
    - 社区不满足于单轮对话 Agent。通过 **多层架构（大脑+工人）**、**持久状态**（#56913）和 **子 Agent 深度推理**（#14321）等需求，Claude Code 正被要求转型为一个可长期托管、自动运维的操作系统级 Agent。
    - **代价**：但 #68110（递归失控）和 #67587（后台静默扣费）尖锐地指出了当前架构在安全性和成本控制上的缺失，**递归深度/预算上限** 成为新的刚需。

2.  **模型服务的透明化与定价灵活化**
    - **Fable 5 事故**暴露了模型访问的黑箱问题。用户需要知道**模型为何降级**、服务端是否有过载、以及是否有**自动重试机制**。
    - **价格诉求**：#47509 表明，重度开发者群体需要介于 Team Premium（6.25x）和 Max（20x）之间的灵活等级。

3.  **工作流产品的“工程化”**
    - 开发者已开始将 Claude Code 集成进团队工作流，#50911（Cron 不持久）和 #62309（Worktree 不遵守 Git 约定）的提出，显示出对 **CLI 行为确定性** 的迫切需求。用户拒绝一个在自动化场景下行为不可预测的工具。

---

### 🔍 开发者关注点（痛点速览）

1.  **服务稳定性信任危机**：Fable 5 事件证明，模型严重依赖 Anthropic API 的可用性。全平台覆盖式的宕机让重度用户重新评估其生产环境风险。
2.  **Agent 成本恐惧症**：AI 编程成本不再是线性增长，Agent 递归（#68110）使得费用可能在短时间内快速失控。**“无上限”模式焦虑** 弥漫社区。
3.  **反直觉的 CLI 行为**：`--worktree` 自动添加前缀（#62309）和 Cron 任务静默不持久（#50911）破坏了开发者对 CLI “纯净”、“可预测”的预期。
4.  **平台修复需加速**：Windows 安装问题（#49917）持续困扰新用户；Windows TUI 下 Ctrl+V 无法粘贴（#68136）降低了日常体验。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# 2026-06-13 OpenAI Codex 社区动态日报

## 今日速览

今日 Codex 一口气发布了 4 个 Rust 组件 alpha 版本，版本号迭代至 0.140.0-alpha.17。社区讨论热度集中在 Windows 平台的 Sandbox/Node_REPL 启动失败（“spawn setup refresh”）以及误报网络安全拦截影响正常开发工作的问题。PR 方面，开发团队正全力推进跨操作系统执行路径的统一（PathUri/NativePathString）和执行环境身份保留，为异构环境下的远程执行铺平基础。

---

## 版本发布

过去 24 小时内发布了 4 个版本，均属于 Rust Codex CLI 组件的 **v0.140.0-alpha** 系列。虽然每个 Release 仅标注了版本号，但如此密集的 alpha 发布表明 Rust 底层正在快速迭代，很可能包含函数调用、沙箱或路径处理的实验性变更。建议关注 Rust 组件的用户留意后续 changelog。

- [rust-v0.140.0-alpha.17](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.17)
- [rust-v0.140.0-alpha.16](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.16)
- [rust-v0.140.0-alpha.15](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.15)
- [rust-v0.140.0-alpha.14](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.14)

---

## 社区热点 Issues

挑选了 10 个讨论最热烈或影响最大的 Issue。

### 1. #12564 允许重命名任务/线程标题（已关闭 · 79 评论 · 👍111）
社区最强烈的功能请求之一。用户希望在历史记录中修改任务/线程标题以便于导航，得到压倒性支持。该 Issue 已被关闭，说明开发团队已经采纳或正在实现。
[链接](https://github.com/openai/codex/issues/12564)

### 2. #9046 Codex 上下文窗口空间不足（开放 · 25 评论）
经典的上下文限制问题：用户刚开始对话就提示“ran out of room in context window”。对话长度管理仍是高频痛点，尤其在长会话中。
[链接](https://github.com/openai/codex/issues/9046)

### 3. #22423 无法定位 Codex CLI 二进制（开放 · 20 评论）
Windows 用户频繁遇到 `Unable to locate the Codex CLI binary`，即使设置了 `CODEX_CLI_PATH` 也不生效，导致 Electron 应用无法启动。WSL 环境下尤其突出。
[链接](https://github.com/openai/codex/issues/22423)

### 4. #25243 macOS 重启循环耗尽系统文件描述符（开放 · 20 评论 · 👍2）
Codex.app 在 macOS 上陷入 relaunch loop，导致 `syspolicyd` 文件描述符耗尽并阻塞其他应用启动。Pro 用户影响严重，被认为是 macOS 平台的严重崩溃问题。
[链接](https://github.com/openai/codex/issues/25243)

### 5. #25220 Windows 内置插件全部不可用（开放 · 16 评论 · 👍3）
Computer Use、Browser、Chrome、LaTeX 等内置插件显示为“不可用”，根因是 `copyfile` 对 EFS 加密的 WindowsApps 文件失败。中国大陆用户受影响较多，该问题与 Microsoft Store 安装有关。
[链接](https://github.com/openai/codex/issues/25220)

### 6. #24098 Windows 提权沙箱启动失败（已关闭 · 19 评论 · 👍6）
`spawn setup refresh` 问题在 Windows 上反复出现，提权沙箱失败但普通沙箱正常。社区提出多种排查路径，最终被关闭但类似问题仍在新版复现（见 #24963 等）。
[链接](https://github.com/openai/codex/issues/24098)

### 7. #27817 正常税务申报被误判为网络安全风险（开放 · 12 评论）
用户在授权的个人财务/税务对话中被标记“网络安全风险”，需要加入 Trusted Access 才能继续。社区担心安全策略过于严格，误伤正常使用。
[链接](https://github.com/openai/codex/issues/27817)

### 8. #22335 CLI 远程压缩反复失败，断开会话连续性（开放 · 6 评论 · 👍8）
尽管评论不多，但获得 8 个赞，说明很多用户遇到相同问题。CLI 在 `gpt-5.4/5.5` 上 remote compaction 失败，导致 resumed 线程失去上下文连续性。
[链接](https://github.com/openai/codex/issues/22335)

### 9. #27175 Windows Desktop 26.602.71036 更新后崩溃（开放 · 15 评论 · 👍3）
Pro 用户升级到 Jun 8 发布版后，应用在空会话下也崩溃或无法访问。系统集成问题（ASUS Zenbook 等）表明可能与硬件/驱动兼容性有关。
[链接](https://github.com/openai/codex/issues/27175)

### 10. #25216 Windows Desktop + WSL 跨系统集成缺口（开放 · 8 评论 · 👍6）
系统性 Issue 汇总了 Windows/WSL 边界上的路径、配置、插件缓存、SQLite 状态等多处假设不一致。社区呼吁添加端到端 release gate。这是 Windows 平台问题的根因分析典范。
[链接](https://github.com/openai/codex/issues/25216)

---

## 重要 PR 进展

以下 10 个 PR 反映了当前最核心的开发方向：跨平台执行架构、安全策略增强、插件系统优化。

### 1. #28018 app-server: command cwd 使用 NativePathString
将命令执行的 cwd 暴露为环境原生路径字符串，在 app-server v2 API 边界进行转换。这是跨 OS 执行路径统一的关键步骤。
[链接](https://github.com/openai/codex/pull/28018)

### 2. #27819 path-uri: 跨平台渲染原生路径
推广 `PathUri` 到更多位置，但对外部 API 仍保持“常规路径”形态。为 Windows/Linux/macOS 的无缝执行铺路。
[链接](https://github.com/openai/codex/pull/27819)

### 3. #28014 unified-exec: 无需宿主编沙启动远程命令
允许远程 unified-exec 命令绕过 app-host sandbox 构造，直接发送策略到 exec-server。大幅简化远程执行链路。
[链接](https://github.com/openai/codex/pull/28014)

### 4. #27937 添加 Hermetic Wine exec-server 测试
引入 Wine 实现跨平台 exec-server 测试，确保 Linux 上的 app-server 能控制 Windows 执行环境。可靠性的重要保障。
[链接](https://github.com/openai/codex/pull/27937)

### 5. #27971 协调云配置缓存在进程间共享
解决多个 Codex 进程同时获取云配置时的重复请求和缓存过期问题。通过进程间协调减少网络开销，提升启动性能。
[链接](https://github.com/openai/codex/pull/27971)

### 6. #28002 压缩请求中传递 turn state
确保内联压缩与采样请求使用相同的逻辑 turn 状态，压缩不再丢失会话连续性。直接回应 #22335 等社区痛点。
[链接](https://github.com/openai/codex/pull/28002)

### 7. #27459 根据认证路由门控插件 MCP 服务器
在 `PluginsManager` 层进行认证感知的 surface 投影，只暴露用户有权的 MCP 端点。这是插件安全体系的基础。
[链接](https://github.com/openai/codex/pull/27459)

### 8. #28012 添加 fail-closed 插件脚本解析器
作为 FOO-574 的前置 slice，以默认关闭的方式添加插件脚本命令解析器。强调安全（fail-closed）设计。
[链接](https://github.com/openai/codex/pull/28012)

### 9. #27886 更新 Guardian 策略措辞
细化敏感数据出口的判断规则，并保留用户对个人数据分享的显式授权。提升安全策略的精准度，减少误报。
[链接](https://github.com/openai/codex/pull/27886)

### 10. #27961 强制执行托管部署中远程控制的禁用
为托管部署提供可靠的 deny gate 阻止远程控制启动。满足企业级管理需求，移除旧的兼容性 no-op。
[链接](https://github.com/openai/codex/pull/27961)

---

## 功能需求趋势

从过去 24 小时的 Issues 中可以提炼出以下社区关注的方向：

- **线程/任务管理增强**：重命名线程标题（#12564）获得超高支持，上下文窗口管理（#9046）依旧紧迫。
- **Windows 平台稳定**：Sandbox/Node_REPL 启动失败、App 崩溃、CLI 路径发现、WSL 集成混乱占据了多数 Issue。Windows 用户是最急切需要稳定性的群体。
- **减少安全误报**：两项误报 Issue（#27817, #28015）表明安全策略需要更智能的上下文判断，避免影响合法财务、运维工作。
- **跨 OS 执行**：虽然在 Issues 中不明显，但从 PR 侧可以看出社区对跨平台无缝执行有着不可见的需求（统一路径、远程 exec）。
- **插件生态健康**：Windows 插件不可用（#25220）暴露了安装/发布机制的脆弱性，社区希望内置插件开箱即用。

---

## 开发者关注点

结合反馈内容，当前开发者遇到的主要痛点及高频诉求包括：

- **“spawn setup refresh” 恶性循环**：至少 7 个独立 Issue 指向 Windows 沙箱初始化失败，根因似与 UAC 检测、EFS 加密、缓存刷新竞争条件有关。用户被迫回退或反复重装。
- **App 更新即爆炸**：#27175、#27979 等多起报告显示最新版本（26.602/26.609）在 Windows 和 macOS 上启动即崩溃或丢失历史记录，用户升级意愿降低。
- **安全策略过度敏感**：正常 git 操作、税表填写被标记为网络安全风险，打断工作流。开发者希望引入可配置的白名单或更准确的分类器。
- **CLI 与 App 的二进制/路径耦合**：WSL 与非标准安装盘符导致 CLI 发现失败，开发者期望有一个更健壮的环境检测机制。
- **上下文长度限制仍未缓解**：即使在使用新模型时，长对话仍容易被截断且压缩失败（#22335），需要更好的压缩策略或手动上下文管理。

---

*以上日报基于 GitHub openai/codex 仓库 2026-06-13 公开数据生成，关注最新动态请直接访问仓库。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，作为专注 AI 开发工具的技术分析师，我根据您提供的 GitHub 数据，为您生成 2026 年 6 月 13 日的 Gemini CLI 社区动态日报。

---

## Gemini CLI 社区动态日报 | 2026-06-13

### 今日速览

今日社区动态围绕稳定性和体验优化展开。最新 Nightly 版本修复了 MCP 工具发现和 Vertex AI 模型映射的核心问题。社区方面，开发者对 Agent 挂起、子代理成功率虚报以及工具使用不足等问题反馈集中，相关 Issue 讨论热度高；同时，多项关键 PR 已合并，重点修复了 tmux 兼容性、Shell 历史记录损坏、SSE 事件流格式等 BUG。

### 版本发布

*   **v0.48.0-nightly.20260613**
    *   **核心修复：** 由 `@luisfelipe-alt` 修复了 MCP 工具发现中的原子更新问题。
    *   **兼容性修复：** `@DavidAPierce` 修复了 Vertex AI 模型映射问题。
    *   **文档与工具：** 新增了文档以及迁移命令。
    *   **链接:** [Release v0.48.0-nightly.20260613](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-nightly.20260613.g9e5599c32)

### 社区热点 Issues

1.  **[BUG] 通用代理挂起 (#21409)**
    *   **重要性：** 高优先级 (P1) BUG，影响核心体验。用户反馈 Gemini CLI 在将任务委派给通用代理时会无限期挂起，甚至简单的创建文件夹操作都无法完成。
    *   **社区反应：** 获得 8 个 👍，7 条评论，用户情绪受影响较大。有用户已找到临时解决方案（阻止模型使用子代理）。
    *   **链接:** [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

2.  **[BUG] 子代理在达到最大轮次后误报成功 (#22323)**
    *   **重要性：** 高优先级 (P1) BUG。子代理（如 `codebase_investigator`）在达到 `MAX_TURNS` 限制后，仍向主代理报告状态为“成功”和终止原因为“GOAL”，这隐藏了任务被中断的真实情况，导致问题排查困难。
    *   **社区反应：** 2 个 👍，6 条评论，开发者已关注到该逻辑缺陷。
    *   **链接:** [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

3.  **[Epic] 组件级评估 (#24353)**
    *   **重要性：** 高优先级 (P1) 特性。该项目旨在建立更健壮的组件级评估体系，是提升 AI Agent 质量和可信度的关键基础设施。目前已有 76 个行为评估测试在运行。
    *   **社区反应：** 7 条评论，显示出开发团队对质量保证的持续投入。
    *   **链接:** [Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

4.  **[Epic] 评估 AST 感知的文件读取与搜索影响 (#22745)**
    *   **重要性：** P2 优先级，探索性功能。旨在研究通过抽象语法树（AST）感知来优化代码读取和搜索，期望减少模型因读错文件边界而产生的多余交互，同时减少 Token 消耗和噪声。
    *   **社区反应：** 1 个 👍，7 条评论。社区对提升代码理解和操作精度的尝试表示关注。
    *   **链接:** [Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

5.  **[BUG] Gemini 不善于主动使用 Skills 和子代理 (#21968)**
    *   **重要性：** P2 优先级，直接影响效率。用户反馈 Gemini 在执行任务时，即使任务与已定义的 Skills（如 Gradle、Git 命令）高度相关，也很少主动使用，除非被明确要求。
    *   **社区反应：** 6 条评论，这是一个关于 Agent 自主决策能力和工具调用策略的重要反馈。
    *   **链接:** [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

6.  **[BUG] Shell 命令执行后在“等待输入”状态卡住 (#25166)**
    *   **重要性：** 高优先级 (P1) BUG。一个高频出现的交互障碍：Gemini 执行完一个简单的 CLI 命令后，会卡在“等待用户输入”状态，尽管命令早已执行完毕。
    *   **社区反应：** 3 个 👍，4 条评论。此问题严重影响自动化流程的连续性，开发者抱怨较多。
    *   **链接:** [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

7.  **[BUG] 浏览器代理在 Wayland 环境下失败 (#21983)**
    *   **重要性：** 高优先级 (P1) BUG。`browser_agent` 在 Wayland 显示服务器下无法正常工作，限制了 Linux 用户的使用。
    *   **社区反应：** 1 个 👍，4 条评论。这是特定环境下的关键兼容性问题。
    *   **链接:** [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

8.  **[BUG] 超过 128 个工具时出现 400 错误 (#24246)**
    *   **重要性：** P2 优先级 BUG。当启用工具数量超过 128 个（甚至更多）时，Gemini CLI 会遭遇 400 错误。用户期望 Agent 能更智能地管理可用工具的范围。
    *   **社区反应：** 3 条评论，暴露出当前工具调度机制的容量限制问题。
    *   **链接:** [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)

9.  **[BUG/安全] Auto Memory 日志及机密信息处理问题 (#26525)**
    *   **重要性：** P2 优先级，涉及安全隐私。Auto Memory 功能在日志和内容发送模型中存在潜在机密信息泄露风险。社区呼吁在提取前进行确定性编辑并减少自动内存日志记录。
    *   **社区反应：** 5 条评论，反映了用户对数据安全的日益关注。
    *   **链接:** [Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

10. **[BUG] 浏览器代理忽略 settings.json 的覆盖设置 (#22267)**
    *   **重要性：** P2 BUG。`browser_agent` 完全无视用户在 `settings.json` 中配置的覆盖选项（如 `maxTurns`），导致用户无法自定义代理行为。
    *   **社区反应：** 3 条评论，表明配置系统的统一性和优先级处理存在问题。
    *   **链接:** [Issue #22267](https://github.com/google-gemini/gemini-cli/issues/22267)

### 重要 PR 进展

1.  **[已合并] 修复：在 tmux 中错误的浅色背景检测 (#27572)**
    *   **内容：** 修复了一个回归问题，该问题导致 Gemini CLI 在 tmux 中运行时，错误地将终端背景检测为浅色（#ffffff），从而触发了不恰当的主题切换。
    *   **链接:** [PR #27572](https://github.com/google-gemini/gemini-cli/pull/27572)

2.  **[已合并] 修复：Shell 历史记录中反斜杠结尾的命令合并错误 (#27555)**
    *   **内容：** 解决了 Shell 历史功能的一个 BUG：任何以反斜杠结尾的命令（如 Windows 路径 `dir C:\`），会在下次启动时与下一行命令会被错误合并，导致记录损坏。
    *   **链接:** [PR #27555](https://github.com/google-gemini/gemini-cli/pull/27555)

3.  **[已合并] 修复：Vim `cc` 命令无法清除末行和特殊字符行 (#27554)**
    *   **内容：** 修复了编辑器模式下 Vim `cc`（修改行）命令在多行缓冲区和非 ASCII 字符行上无效的问题。
    *   **链接:** [PR #27554](https://github.com/google-gemini/gemini-cli/pull/27554)

4.  **[已合并] 修复：A2A 服务器 SSE 事件流格式错误 (#27549)**
    *   **内容：** 修复了 A2A 协议终端的 SSE 事件缺少必要的空行分隔，导致无法被标准 SSE 客户端解析的问题。
    *   **链接:** [PR #27549](https://github.com/google-gemini/gemini-cli/pull/27549)

5.  **[已合并] 修复：LLM 提示模板中 `$` 符号被错误替换 (#27552)**
    *   **内容：** 关键的修复，解决因使用 `String.prototype.replace` 而导致的代码注入类 BUG。当文件内容包含 `$` 符号时，会被 `replace` 方法的特殊模式错误解释和篡改，现在改为逐字插入内容。
    *   **链接:** [PR #27552](https://github.com/google-gemini/gemini-cli/pull/27552)

6.  **[已合并] 修复：Gateway 认证模式验证问题 (#27553 & #27558)**
    *   **内容：** 双 PR 修复一个回归问题：当配置了自定义 `GOOGLE_GEMINI_BASE_URL` 时，新的 `GATEWAY` 认证类型未被正确识别，导致“无效的认证方法”错误。
    *   **链接:** [PR #27553](https://github.com/google-gemini/gemini-cli/pull/27553) | [PR #27558](https://github.com/google-gemini/gemini-cli/pull/27558)

7.  **[已合并] 修复：在 ripgrep 执行失败时回退到传统 GrepTool (#27568)**
    *   **内容：** 增强了搜索功能的健壮性。当 ripgrep 工具因环境问题（如 `rg` 未安装）执行失败时，能优雅回退到传统的 `GrepTool`，避免服务中断。
    *   **链接:** [PR #27568](https://github.com/google-gemini/gemini-cli/pull/27568)

8.  **[进行中] 修复：限制待处理的 Tool 响应大小 (#27870)**
    *   **内容：** 修复一个高优先级 (P1) BUG。当工具返回的结果非常大时，会导致模型上下文拥塞。该 PR 通过限制待处理的 `functionResponse` 大小来提升稳定性。
    *   **链接:** [PR #27870](https://github.com/google-gemini/gemini-cli/pull/27870)

9.  **[进行中] 修复：消除 Agent 主目录重复加载问题 (#27694)**
    *   **内容：** 修复了项目级和用户级 Agent 目录在相同路径下（如 `~/.gemini/agents`）时，会重复加载的问题，同时完善了回归测试。
    *   **链接:** [PR #27694](https://github.com/google-gemini/gemini-cli/pull/27694)

10. **[已合并] 修复：增强 SKILL.md 文件解析的健壮性 (#27873)**
    *   **内容：** 增强了对 SKILL.md 文件 YAML Frontmatter 的解析能力，增加了对 UTF-8 BOM、尾部空格、非字符串值等的支持。
    *   **链接:** [PR #27873](https://github.com/google-gemini/gemini-cli/pull/27873)

### 功能需求趋势

*   **Agent 能力与可靠性：** 社区最关注的是 Agent 的自主决策能力和任务执行的稳定性。从“不主动使用 Skills”到“子代理误报成功”，再到“通用代理挂起”，都指向 Agent 决策逻辑、工具选择策略和状态管理需要根本性改进。
*   **评估与测试体系：** 对健壮的组件级评估（Component Level Evaluations）和 AST 感知工具的研究投入，表明开发团队正致力于通过更科学的方法来量化和提升 Agent 质量，这将是未来稳定性的基石。
*   **浏览器代理增强：** 浏览器代理相关的 BUG（Wayland支持、配置覆盖、自动接管与锁恢复）持续出现，说明社区对该功能使用率高，且期望其能在更多场景下稳定工作。
*   **内存与上下文管理：** 围绕 Auto Memory 的讨论（低信号会话重试、无效补丁隔离、隐私 Redaction）揭示出社区对 Agent 长期记忆能力、效率和安全性的综合考量。
*   **安全与合规性：** 开发者日益关注终端用户的敏感信息（如 API Keys）在传输和日志中是否被安全处理。确定性编辑、减少不必要的日志记录等需求凸显了安全优先的态势。

### 开发者关注点

*   **高频痛点 BUG：** “Shell 执行后卡住”、“通用代理挂起”、“编辑器（Vim cc）命令异常”和“工具超过 128 个报错”，这些是用户日常使用中最受干扰的问题，修复优先级高。
*   **用户期望无感体验：** 开发者希望 Agent 能不依赖用户的显式指令，自主根据任务上下文调用“Skills 和子代理”，暗示对 Agent 智能度的更高期待。
*   **配置与自定义的灵活性：** 浏览器代理忽略 `settings.json` 覆盖设置、子代理运行权限违背用户预设（Issue #22093），反映出用户对配置统一性和尊重用户设置的强烈需求。
*   **跨平台兼容性：** 无论是 Wayland 下的浏览器代理，还是 tmux 中的背景识别错误，都说明开发者希望获得一致、无错的跨平台体验。
*   **环境健壮性：** 对 `ripgrep` 失败回退、`termux-exec` 兼容性修复、Shell 反斜杠历史记录损坏等问题的修复，体现了用户对 CLI 工具在复杂和异构开发环境中依然能稳定工作的核心诉求。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-06-13

**分析师角色**：AI 开发工具技术分析师


## 1. 今日速览

- v1.0.62-1 正式发布，带来 YOLO 模式指示器、Issues/PRs 全局搜索等新能力，但随即爆出 Linux ARM64 平台 Tokio Reactor 崩溃（#3784）的严重回归问题。
- 终端流式渲染器成为“重灾区”，文字重复、截断、重叠等三大同类 Bug（#3749、#3755、#3780）集体爆发，严重影响日常流式推理体验。
- v1.0.61 遗留下来的 MCP 服务器无限重连循环（#3782）尚未解决，社区对近期版本质量的信任度明显下降。


## 2. 版本发布

**v1.0.62-1**（过去 24 小时内发布）

- **YOLO 模式指示器**：底部状态栏新增“允许全部”状态图标，并支持通过 `statusLine.command` 自定义全量确认行为。
- **键盘全局搜索**：在 Issues 或 Pull Requests 标签页按下 `/` 即可调用 GitHub 服务端过滤进行搜索。
- **Session 作用域增强**：新增 Session 范围的扩展（Extensions）和画布（Canvases）支持，提升多任务隔离性。
- **SDK 记忆配置**：允许 SDK 客户端显式配置 Session 记忆阈值。

> 链接：[Release v1.0.62-1](https://github.com/github/copilot-cli/releases/tag/v1.0.62-1)


## 3. 社区热点 Issues（精选 10 条）

### 1️⃣ #3784 — [严重回归] v1.0.62-1 在 Linux ARM64 上首次消息发送后 Tokio Reactor Panic（退出码 134）
- **重要性**：最新版本发布即崩溃，树莓派、AWS Graviton、Apple Silicon 虚拟机用户受直接影响。
- **社区反应**：评论刚起步，但开发者急切等待官方 Hotfix。
- **链接**：[Issue #3784](https://github.com/github/copilot-cli/issues/3784)

### 2️⃣ #3782 — [严重漏洞] MCP stdio 服务器在 v1.0.61 中无退避算法无限重连
- **重要性**：无指数退避、无最大重试上限，导致成百上千个子进程被循环创建，资源可能被耗尽。
- **社区反应**：严重度极高但暂缺讨论，属于波及 MCP 子系统根基的架构缺陷。
- **链接**：[Issue #3782](https://github.com/github/copilot-cli/issues/3782)

### 3️⃣ #3749 / #3755 / #3780 — 终端流式渲染器文字严重错乱（重复 / 重叠 / 截断）
- **重要性**：三大独立 Issue 指向同一个渲染引擎缺陷，覆盖推理思考阶段与最终输出。
- **社区反应**：用户提交了大量截图与复现步骤，该问题严重干扰 Copilot CLI 最核心的交互场景。
- **链接**：[#3749](https://github.com/github/copilot-cli/issues/3749)、[#3755](https://github.com/github/copilot-cli/issues/3755)、[#3780](https://github.com/github/copilot-cli/issues/3780)

### 4️⃣ #53 — 恢复 Copilot CLI 原有交互命令，避免破坏现有工作流
- **重要性**：75 👍、37 评论，连续 9 个月占据热度榜首。核心功能缺失已迫使社区创建 `shell-ai` 等 Fork 替代品。
- **社区反应**：用户自发维护替代方案清单，官方超半年不回应已严重透支社区信任。
- **链接**：[Issue #53](https://github.com/github/copilot-cli/issues/53)

### 5️⃣ #2627 — 请求可配置的系统提示词以压缩 Token 开销
- **重要性**：17 👍。当前系统提示词 + 工具定义固定消耗约 3 万 tokens，重度用户精准吐槽为“空气税”。
- **社区反应**：用户认为在 200K 窗口下白白浪费 15% 空间，强烈要求开放可配置机制。
- **链接**：[Issue #2627](https://github.com/github/copilot-cli/issues/2627)

### 6️⃣ #2306 — 企业/组织 Copilot 策略间歇性拒绝访问
- **重要性**：每周随机出现 2–3 次，连 `/context` 都返回空白，严重阻碍企业推广落地。
- **社区反应**：企业管理员遭遇配置困境，用户不断回滚版本也无法根治。
- **链接**：[Issue #2306](https://github.com/github/copilot-cli/issues/2306)

### 7️⃣ #618 — 从 .github/prompts 目录加载自定义斜杠命令
- **重要性**：99 👍 的超高支持票，要求对标 VS Code 和 Claude Code 的 prompt 文件支持。
- **社区反应**：用户期望统一标准，避免在不同工具间维护多套 prompt 配置。
- **链接**：[Issue #618](https://github.com/github/copilot-cli/issues/618)

### 8️⃣ #1999 / #2920 — 非美式键盘输入故障（德语 @、波兰语 AltGr）
- **重要性**：`@` 和众多地区字符完全无法输入，基础 i18n 缺陷让非英语用户寸步难行。
- **社区反应**：问题持续数月无人修复，德国/波兰社群普遍感到被忽略。
- **链接**：[#1999](https://github.com/github/copilot-cli/issues/1999)、[#2920](https://github.com/github/copilot-cli/issues/2920)

### 9️⃣ #3501 — Windows 滚动条导致文本对齐混乱
- **重要性**：8 👍。终端 UI 回归极其直观，Windows Terminal 用户阅读体验大降。
- **社区反应**：用户尝试通过配置禁用无果，呼吁默认关闭该功能。
- **链接**：[Issue #3501](https://github.com/github/copilot-cli/issues/3501)

### 🔟 #3778 — 通过 OpenTelemetry 输出成本 / 高级请求指标
- **重要性**：支持企业对 Copilot 使用成本进行精细化监控，对标 `claude_code.cost.usage`。
- **社区反应**：开源运维团队高度关注，希望纳入内部成本核算体系。
- **链接**：[Issue #3778](https://github.com/github/copilot-cli/issues/3778)


## 4. 重要 PR 进展

过去 24 小时内 Pull Request 活动极少，仅收录 1 条：

- **#3771 [OPEN] 项目初始化设置**  
  由社区用户提交，暂无实质性功能变更或修复内容，处于讨论阶段的初始化 PR。

> 链接：[PR #3771](https://github.com/github/copilot-cli/pull/3771)

**分析**：核心团队当前显然在全力修复 v1.0.61/62 系列带来的严重回归 Bug（MCP 重连、ARM64 Panic、终端渲染），近期 PR 合并窗口可能暂时收紧。


## 5. 功能需求趋势

| 趋势方向 | 代表 Issue | 社区热度 |
|---|---|---|
| **终端渲染稳定性** | #3749、#3755、#3780 | 🔥🔥🔥 近期最痛 |
| **MCP 治理与可靠性** | #3782（退避）、#3564（启停管理）、#3756（企业策略） | 🔥🔥🔥 |
| **上下文 Token 经济性** | #2627（系统提示瘦身）、#3364（长期目标持久化） | 🔥🔥 |
| **成本可观测性** | #3778（OTel 成本指标） | 🔥🔥 |
| **模型自定义与多元化** | #3048（ACP 自定义提供商）、#2661（模型支持） | 🔥🔥 |
| **国际化（i18n）** | #1999、#2920、#3776（WSL / 键盘 / 粘贴乱码） | 🔥🔥 |
| **与 VS Code / Claude Code 对齐** | #618（slash commands from .github）、#3331（插件自动更新） | 🔥 |


## 6. 开发者关注点（痛点与高频呼声）

1. **版本质量信任危机**  
   v1.0.61 → v1.0.62-1 连续两版引入致命回归（MCP 无限循环、ARM64 Panic），社区出现“追版本像在踩雷”的强烈情绪，建议企业用户在 Bug 修复前锁定旧版。

2. **非英语用户被边缘化**  
   `@` 无法输入、AltGr 组合键失效、WSL 粘贴乱码等基础 i18n 问题持续数月未修复。这不仅是 Bug，更反映出项目对全球用户基本体验的重视不足。

3. **“又要造轮子了”**  
   Issue #53 是信任危机的标志性事件：当官方对核心交互缺陷沉默 9 个月后，社区自发维护 Fork 替代方案 `shell-ai`。该模式一旦成熟，将对官方生态形成实质性分流。

4. **企业部署多重拦路**  
   授权策略间断性误判（#2306）加上组织级 MCP 误杀（#3756），让企业 IT 管理员既要应对随机故障，又缺乏细粒度配置能力，推广阻力大增。

5. **Token 焦虑蔓延**  
   每个 Session 启动即消耗 3 万 tokens 在系统提示词上，用户感到强烈“被浪费”。即使有 200K 窗口，15% 的无效开销也让长上下文任务效率大打折扣。

---

**总结**：v1.0.62-1 的新功能令人兴奋，但伴随的崩溃 Bug 和渲染缺陷严重拖累了用户体验。社区期盼团队优先稳定终端渲染与 MCP 基础架构，并尽快回应对非英语用户的核心输入需求。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 Kimi Code CLI 社区动态日报（2026-06-13）。由于今日数据样本相对集中，日报将重点分析这几条活跃 Issue 与 PR 背后的深层趋势。

---

## 今日速览

今日无新版本发布，但社区围绕 **用量计费不透明**（#1994）、**WebSocket 连接导致 Work 标签页完全不可用**（#2435）以及 **文件读取陷入死循环**（#640）三个问题展开了集中讨论。此外，社区贡献者提交了针对 Python 3.13 兼容性的修复 PR（#1597），反映出官方对基础环境的跟进仍需加强。

## 社区热点 Issues（共 3 条更新）

由于今日活跃 Issue 数量有限，以下列出全部更新条目，并逐一分析其重要性。

### ⚠️ 1. #1994：kimiCode 用量计算有问题（Token 消耗远超预期）
- **重要性：** ⭐⭐⭐⭐⭐（影响付费用户核心体验）
- **社区反应：** 7 个 👍、6 条评论，讨论激烈。
- **背景：** 用户反映仅运行 2 个任务就消耗完 2 小时额度，并指出模型（K2.6）思维链过长导致 Token 迅速耗尽。「订阅会员 2 小时只能问 2 次」与官方宣传的「300-1200 次 API 请求」严重不符，质疑计费标准究竟是 Token 还是请求次数。
- **分析：** 该 Issue 直击定价与信任危机。若计费模型确实按 Token 而非请求次数，当使用长思维链模型时，成本波动极大。社区要求官方澄清并优化 Token 统计策略，是当前最迫切的反馈。

### ⚠️ 2. #640：Kimi CLI 陷入反复读取同一文件的死循环
- **重要性：** ⭐⭐⭐⭐（影响基础编码流程）
- **社区反应：** 9 条评论（今日最多讨论）、1 个 👍。
- **背景：** 用户在 Linux 系统上使用自定义 Anthropic 端点（`mimo-v2-flash`）时，CLI 持续反复读取同一个文件，无法执行后续操作。用户已提供详细环境信息（Kimi CLI 0.76、Arch Linux）。
- **分析：** 尽管 👍 数不高，但讨论热度说明该 Bug 对特定场景（自定义端点 + 特定模型）的影响十分严重，可能涉及文件句柄管理或上下文循环检测缺陷。社区在等待开发者复现与修复。

### ⚠️ 3. #2435：[Bug] Work 标签页 WebSocket 初始化失败，无限重载
- **重要性：** ⭐⭐⭐⭐（阻塞核心 Web 工作流）
- **社区反应：** 1 条评论（初始报告）、0 个 👍，但问题描述清晰。
- **背景：** Windows 用户使用 Kimi CLI 1.41.0 时，Work 标签页出现 “Daimon control WS not ready” 错误，加载进度卡在 99% 并循环重试，导致该标签页完全无法使用。
- **分析：** 该问题直接阻断用户通过 Web 界面使用 Kimi Work 功能，属于严重可用性 Bug。目前社区响应较少，但潜在影响面大，尤其依赖 Web 端工作的团队。

## 重要 PR 进展（共 1 条更新）

### 🔧 PR #1597：修复 Python 3.13 下工具链加载失败
- **作者：** he-yufeng
- **状态：** 开放中（更新于 2026-06-12）
- **功能：** 在 Python 3.13 中，`charset-normalizer` 编译的 `.so` 二进制文件与解释器不兼容，导致 `trafilatura` 导入失败，进而造成 `FetchURL` 等工具无法使用。此 PR 为 `trafilatura` 的导入增加了防护逻辑（Guard），防止级联失败。
- **分析：** 这是今日唯一的 PR，体现了社区对最新 Python 版本兼容性的关心。虽然改动小，但对在 Python 3.13 上使用 Kimi Code CLI 的开发者至关重要，说明官方主线的环境适配仍依赖社区贡献。

## 功能需求趋势

从有限的更新数据中，可以归纳出以下三个明显的功能需求方向：

1. **用量计量透明化与可控制**
   - 社区强烈要求明确计费标准（Token vs 请求次数），并建议提供“思维链长度限制”或“Token 消耗预估”功能，以避免高消耗模型意外耗尽额度。用户期望能自定义“最大上下文 Token 数”以控制成本。

2. **可靠性与错误恢复机制**
   - 无论是文件读取死循环、WebSocket 断连还是工具导入失败，开发者都希望 CLI 具备更强的错误检测和自动恢复能力（如超时重试、死循环检测、连接状态监控）。

3. **环境兼容性与自定义端点支持**
   - 用户频繁在非标准环境（最新 Python、自定义 Anthropic 端点、不同操作系统）上遇到问题。社区期待官方提供更明确的兼容性矩阵，并降低对特定依赖版本的硬性要求。

## 开发者关注点

- **计费争议是当前最大痛点：** 用户对“2 小时只能使用 2 次”的体验非常不满，质疑 promotional material 的真实性。这不仅是 bug，更是产品定价与用户预期的严重错位，需要产品团队优先回应。
- **长思维链模型的 token 管理：** 随着模型能力提升（如 K2.6），思维链越来越长，现有 token 计算方式对短任务极不友好。开发者希望引入“按任务实际消耗动态计费”或“设置 token 上限”的选项。
- **工作流阻塞问题：** #640 和 #2435 都直接阻碍用户完成核心任务（代码编写、Web 工作台），优先级应高于一般功能优化。
- **基础运行环境稳定性不足：** 即使官方未主推 Python 3.13，社区已开始使用并遇到问题。表明开发者在积极跟进最新技术栈，对 CLI 的跨版本兼容性要求越来越高。

---
*注：今日社区动态受限于样本数量，重点围绕计费争议与严重 Bug。我们将持续跟踪这些问题的官方回复与修复进度。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-06-13

---

## 📌 今日速览

- 权限交互卡死（#27436）和响应速度过慢（#20404）成为社区讨论焦点，分别获得 16 条和 12 条评论，用户反馈强烈。
- 多个重要修复 PR 提交/合并：`db doctor` 诊断命令（#32093）、会话状态“卡忙”修复（#32128）、DB 迁移不再重复运行（#21056）等，社区对数据层稳定性持续关注。
- 一份涵盖 2561 个 TypeScript 文件的全面安全审计报告被提交（#32134），引发广泛讨论，核心逻辑评审需求提升。

---

## 🔍 社区热点 Issues（10 条）

### 1. #27436 permission required cannot select（评论 16）
**链接：** https://github.com/anomalyco/opencode/issues/27436  
**重要原因：** 用户在“Allow once/Always/Reject”选择时界面卡死，无法提交反馈内容，导致会话完全阻塞。这是基础交互的严重 Bug，影响几乎所有使用权限控制的工作流。社区投票 11 次，属于高关注度问题。

### 2. #20404 opencode go 访问响应速度过慢（评论 12）
**链接：** https://github.com/anomalyco/opencode/issues/20404  
**重要原因：** 用户反馈使用 OpenCode Go 接入 GLM-5 时，每次请求需要十多分钟才能得到响应。性能直接决定用户留存率，该问题长期未解决，社区已在催促。

### 3. #31996 Bug: Invalid JSON Schema Generated Due to Unsupported Regex Lookaround on GPT 5.5（评论 11）
**链接：** https://github.com/anomalyco/opencode/issues/31996  
**重要原因：** OpenCode 生成的 JSON Schema 包含正则 lookaround，被 OpenAI 兼容服务拒绝，导致无法使用 GPT 5.5 等新模型。社区点赞 5 次，认为这是一个兼容性回归。

### 4. #14187 [FEATURE] Add markdown preview toggle in file viewer sidebar（评论 8，👍 22）
**链接：** https://github.com/anomalyco/opencode/issues/14187  
**重要原因：** 当前在侧边栏查看 Markdown 文件只能看到原始文本，用户希望增加实时预览。共获得 22 个点赞，属功能需求中呼声最高。

### 5. #16885 JSON->SQLite one-time migration reruns on channel-specific DBs（评论 8）
**链接：** https://github.com/anomalyco/opencode/issues/16885  
**重要原因：** 非 `latest` 渠道（如本地开发版本）每次启动都会重新执行 JSON 到 SQLite 的迁移，浪费性能且可能引发数据不一致。社区关注 DB 迁移的稳定性。

### 6. #16610 Opencode hangs at startup if a .git repo is present and inotify user instances run out（评论 8）
**链接：** https://github.com/anomalyco/opencode/issues/16610  
**重要原因：** Linux 上 inotify 实例耗尽导致 OpenCode 完全无法启动。影响在资源受限环境下的开发者，社区强调这是严重的启动回归。

### 7. #24335 Permission Wildcard `*` Overwriting Lower Permissions（评论 7）
**链接：** https://github.com/anomalyco/opencode/issues/24335  
**重要原因：** 文档说明通配符匹配规则应为“最后一个匹配生效”，但实际表现为通配符覆盖后续更具体规则，导致安全配置失效。权限系统的核心逻辑 Bug。

### 8. #31204 BUG: session_message.seq NOT NULL constraint failed on agent-switched sessions（评论 6）
**链接：** https://github.com/anomalyco/opencode/issues/31204  
**重要原因：** 最新更新（6 月 3-5 日的迁移）导致切换 agent 时 SQLite `NOT NULL` 约束错误，会话崩溃。属于数据层近期引入的严重回归。

### 9. #27302 Warp mode + interactive Q&A: all input captured (mouse clicks, Enter, Ctrl+C) — user must force-close terminal（评论 3，👍 6）
**链接：** https://github.com/anomalyco/opencode/issues/27302  
**重要原因：** Warp 模式下与 Q&A 交互时，所有输入被截获，用户无法操作终端，只能强制关闭。尽管评论数少，但获得 6 个点赞，说明不少用户遇到。

### 10. #31423 [FEATURE] make window title show the currently selected session + project（评论 2）
**链接：** https://github.com/anomalyco/opencode/issues/31423  
**重要原因：** 浏览器窗口标题始终是“OpenCode”，多会话多项目时难以区分。该功能需求虽小但能显著提升日常使用体验。

---

## 🔧 重要 PR 进展（10 条）

### 1. #32139 fix(app): improve presets i18n, storage, and UI consistency
**链接：** https://github.com/anomalyco/opencode/pull/32139  
**内容：** 修复预设功能的国际化缺失（硬编码中文）、存储逻辑和UI一致性问题。为 18 种语言添加翻译，属于产品质量提升。

### 2. #32138 fix(command): sort numbered placeholder hints numerically
**链接：** https://github.com/anomalyco/opencode/pull/32138  
**内容：** 修复 `Command.hints()` 中对 `$N` 占位符的排序问题（原为字符串排序导致 `$10` 排在 `$2` 前面），改为按数字排序。提升命令提示准确性。

### 3. #32135 fix(mcp): refresh expired oauth tokens
**链接：** https://github.com/anomalyco/opencode/pull/32135  
**内容：** 修复 MCP（Model Context Protocol）中 OAuth Token 过期后不自动刷新的问题，提升持续集成场景的可靠性。

### 4. #31529 fix(plugin): prevent spinner garbage output in non-TTY environments
**链接：** https://github.com/anomalyco/opencode/pull/31529  
**内容：** 修复在非交互式终端（PowerShell、CI/CD）运行时，插件安装进度旋转器输出乱码的问题。提升 CI/CD 体验。

### 5. #32134 docs: add comprehensive security audit report (17 findings)
**链接：** https://github.com/anomalyco/opencode/pull/32134  
**内容：** 提交了一份涵盖 2561 个 TypeScript 文件的全面安全审计报告（`SECURITY_AUDIT.md`），列出 17 项发现，涉及代码安全性、权限处理、输入校验等。社区反应热烈，预计会推动后续安全改进。

### 6. #32130 feat(tui): Use opencode-specific tmp filename for 'editor_open'
**链接：** https://github.com/anomalyco/opencode/pull/32130  
**内容：** 使 `editor_open` 创建的临时文件使用 OpenCode 唯一标识名，方便用户编辑器配置针对 OpenCode 缓冲区的自定义行为（如代码片段、语法高亮）。

### 7. #18209 feat: App - Support setting base URL during build
**链接：** https://github.com/anomalyco/opencode/pull/18209  
**内容：** 支持通过构建时环境变量 `VITE_BASE_URL` 设置 OpenCode Web App 的基础 URL，方便自托管部署在子路径下。

### 8. #32128 fix(app): reconcile session_status in bootstrap so stale busy clears
**链接：** https://github.com/anomalyco/opencode/pull/32128  
**内容：** 修复会话“工作”状态卡住的问题：bootstrap 阶段通过 `reconcile` 而非裸 `setStore` 更新 `session_status`，确保状态正确同步。对应 Issue #17657 和近期 #32127。

### 9. #32093 feat(opencode): add db doctor and repair commands
**链接：** https://github.com/anomalyco/opencode/pull/32093  
**内容：** 新增 `opencode db doctor` 和 `opencode db repair` 命令，用于诊断并修复本地 SQLite 数据库的常见问题（如约束失败、部分损坏）。关联 10 个 DB 相关 Issue，社区期望值高。

### 10. #21056 fix(opencode): DB migrating on every run for non-latest channels
**链接：** https://github.com/anomalyco/opencode/pull/21056  
**内容：** 修复非 `latest` 渠道（如本地构建）每次启动都重复执行 JSON→SQLite 迁移的问题。解决 #16885，显著改善开发场景下的启动速度与稳定性。

---

## 🧠 功能需求趋势

从近 24 小时的 Issue 中，社区关注的功能方向主要集中在：

- **IDE 与编辑器集成**：官方 IntelliJ IDEA、PyCharm、VS Code 插件何时发布（#8794）仍是老用户的长期期待。
- **数据层稳健性**：多个 Issue 围绕 SQLite 迁移、约束、修复工具（#32097）、`db doctor` 需求，表明用户对数据持久化的可靠性有更高要求。
- **权限与安全**：通配符覆盖（#24335）、`edit` 权限覆盖失效（#18441）暴露权限系统的设计争议；安全审计 PR 也呼应这一趋势。
- **平台兼容性**：Windows 自动更新目录丢失（#26818）、Winget 升级支持（#30026）、Linux inotify 限制（#16610）说明多平台部署仍是痛点。
- **新模型与提供商支持**：GPT 5.5 JSON Schema 兼容（#31996）、TrustedRouter 提供商（#32115）反映社区紧跟模型生态。
- **UI/UX 细节**：Markdown 预览（#14187）、窗口标题展示会话（#31423）、定价表透明度（#32116）等小而美的改进需求持续出现。

---

## ⚠️ 开发者关注点

综合所有反馈，以下痛点和高频需求值得开发团队优先应对：

1. **权限交互卡死**（#27436）—— 用户常遭遇的选择弹窗无响应，直接影响工作流。
2. **响应缓慢**（#20404）—— 尤其是使用 OpenCode Go 或第三方模型时，10 分钟级别的等待不可接受。
3. **启动与 DB 稳定性** —— inotify 耗尽（#16610）、迁移反复执行（#16885）、`session_message.seq` 约束错误（#31204）等严重阻碍日常使用。
4. **会话状态不一致** —— 工作指示器永远不消失（#32127）、agent 切换后崩溃（#31204）让用户难以判断实际状态。
5. **权限规则体系混乱** —— 通配符覆盖（#24335）、`external_directory` 忽略 `edit` 规则（#18441）导致安全配置不可预测。
6. **更新与安装体验** —— Windows 自定义安装路径被重置（#26818）、Winget 安装无法自动升级（#30026）。
7. **定价与配额透明度** —— 订阅配额耗尽后无差分提示且自动重试浪费配额（#32120），Flash vs Pro 加价比例不直观（#32116）。

---

*数据来源：GitHub anomalyco/opencode 社区，统计截止 2026-06-13 24:00 UTC。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 (2026-06-13)

## 今日速览
Pi 项目发布 v0.79.2，主要增强 Amazon Bedrock 验证指引。社区中最热的讨论聚焦于**连接稳定性**（OpenAI Codex 频繁卡死）和**新模型提供商支持**（Anthropic Vertex、Bedrock Mantle 及 vLLM DeepSeek 思维链格式）。此外，全新 `AiGameAgent` 包的并入标志着 Pi 向特定领域开发工作流的正式拓展。

---

## 版本发布

### [v0.79.2](https://github.com/earendil-works/pi/releases/tag/v0.79.2)
- **Better Bedrock 验证指引**：Amazon Bedrock 数据保留验证错误现在会直接链接到 AWS 数据保留文档，帮助用户快速排错。
- **细微新增和调整**：附带了一些附加的更新内容。

---

## 社区热点 Issues（Top 10）

**1. [#4945 OpenAI Codex 连接可靠性问题](https://github.com/earendil-works/pi/issues/4945)**
- **热度**：评论 55 | 👍 30
- **核心反馈**：`openai-codex` / `gpt-5.5` 会使 TUI 频繁卡死在 `Working...` 状态，无输出、无报错、无工具调用，只能按 Esc 中断。过去几天内反复出现，严重扰乱核心交互流程。
- **社区反应**：这是目前评论和点赞数最高的 Issue，反映出用户对核心通道稳定性的迫切需求。

**2. [#5363 请求添加 amazon-bedrock-mantle 提供商](https://github.com/earendil-works/pi/issues/5363)**
- **核心反馈**：现有 `amazon-bedrock` 提供商仅支持 Converse API，而 Bedrock Mantle 模型采用 OpenAI 兼容 API，完全不兼容。用户希望新增独立提供商。
- **社区反应**：表明企业对 AWS 全系列模型接入 Pi 有强烈需求，目前开发组已纳入计划。

**3. [#5653 `pi-ai` 重复安装导致提供商注册表分裂](https://github.com/earendil-works/pi/issues/5653)**
- **核心反馈**：同时安装 `@earendil-works/pi-ai` 和 `@earendil-works/pi-coding-agent` 时，依赖解析会将 `pi-ai` 安装两次（hoisted + nested），**模块级 Map 变成两个独立的副本**，导致提供商注册混乱。
- **社区反应**：直击依赖管理的深层问题，`npm-shrinkwrap.json` 的无完整性引用是其根源。此 Issue 优先级陡升。

**4. [#5673 / #5672 为 vLLM 代理后的 DeepSeek 添加专用 thinkingFormat](https://github.com/earendil-works/pi/issues/5673)**
- **核心反馈**：在 vLLM 部署 DeepSeek-V3.x 模型时，开启思维链（Reasoning）需要发送 `chat_template_kwargs` 参数，但 Pi 的 `deepseek` 格式只兼容原生 API。用户希望新增 `vllm-deepseek` 格式。
- **社区反应**：**企业级本地部署需求显著上升**，Issue 创建不久即获关注，部分用户已在 PR 中给出了实现原型。

**5. [#5654 为自定义消息添加 `excludeFromContext` 选项](https://github.com/earendil-works/pi/issues/5654)**
- **核心反馈**：希望在 `sendMessage()` 中添加 `excludeFromContext: boolean`，类似 Bash 执行消息中的 `!!` 标记。这样扩展可以发送仅显示、**不消耗 Token** 的“状态”消息（如 `/status` 命令）。
- **社区反应**：获得 3 条评论并很快有了对应的 PR #5678，说明核心开发组对这一需求非常认可。

**6. [#5595 openai-completions 的 maxTokens 不生效](https://github.com/earendil-works/pi/issues/5595)**
- **核心反馈**：使用 Together.ai 等 OpenAI 兼容提供商运行推理模型（如 DeepSeek v4pro）时，`maxTokens` 参数无法传递，导致模型在输出未完成时被截断。
- **社区反应**：用户在新安装环境下反复验证，确认问题复现。属于提供商适配的阻塞级 Bug。

**7. [#5667 Bash 输出溢出导致 `TMPDIR` 不可写入而崩溃](https://github.com/earendil-works/pi/issues/5667)**
- **核心反馈**：Bash 工具输出超 50KB/2000 行时，溢出内容写入 `$TMPDIR`。若 `TMPDIR` 解析到 macOS 不可写路径，`createWriteStream` 抛出 `EACCES` 导致 Pi 直接崩溃退出，**属于特定平台的中断级稳定性问题**。
- **社区反应**：用户上报迅速，开发组很快定位到问题根因。

**8. [#5670 Tab 补全交互逻辑问题](https://github.com/earendil-works/pi/issues/5670)**
- **核心反馈**：编辑器 Tab 补全中，输入部分字符缩小匹配范围后按 Tab，**会自动选用列表第一项**，而不是保持菜单继续等待。致使只能完全输入正确路径才能使用 Tab。
- **社区反应**：虽是小细节，但直击编码效率，属于 TUI 体验打磨的高频诉求。

**9. [#5661 `models.json` 大写 Header 值被误当作环境变量](https://github.com/earendil-works/pi/issues/5661)**
- **核心反馈**：`models.json` 中全大写的 Header 值（如 `"BEARER"`、`"AUTH_TOKEN"`）被配置迁移引擎错误重写为 `"$BEARER"`，导致认证失败。
- **社区反应**：正则匹配 `/^[A-Z_][A-Z0-9_]*$/` 太宽泛，属于配置解析中的**隐蔽回归 Bug**。开发组已在 PR #5660 中火速修复。

**10. [#5577 用户角色（Persona）自定义需求](https://github.com/earendil-works/pi/issues/5577)**
- **核心反馈**：用户不再将 Pi 局限为编程助手，而是希望将其用作**安全测试、视频编辑、项目管理、研究等场景的通用智能体**，需要支持角色覆盖来定制行为。
- **社区反应**：虽然 Issue 已关闭，但社区对这一方向的诉求非常清晰，代表了 Pi 应用场景扩展的核心期望。

---

## 重要 PR 进展（Top 10）

**1. [#5681 [已合并] 整合 AiGameAgent 包](https://github.com/earendil-works/pi/pull/5681)**
- **摘要**：将 YeLuo45/AiGameAgent 整合进 Pi 主仓库。该包专注于 HTML5/微信/抖音小游戏多端工作流，支持 OpenAI 兼容 HTTP API。Snapshot 包含 263 次工作区编辑和 37 个 Agent 角色定义。
- **意义**：标志着 Pi 生态从通用编程辅助向**特定领域工作流**的正式拓展。

**2. [#5679 / #5262 [已合并/进行中] Anthropic Vertex AI 提供商](https://github.com/earendil-works/pi/pull/5679)**
- **摘要**：新增内置 `anthropic-vertex` 提供商，使 Pi 能够通过 GCP Vertex AI 使用 Claude 模型，支持 ADC / ambient Google 认证。已对接 Provider 注册、模型选择器和文档。
- **意义**：这是**企业级用户的强需求**——在符合合规要求的前提下无缝使用 Claude。PR #5679 是 #5262 的改进完整实现。

**3. [#5678 [进行中] 自定义消息 `excludeFromContext` 支持](https://github.com/earendil-works/pi/pull/5678)**
- **摘要**：响应 #5654，由核心维护者 mitsuhiko 提交。支持扩展 API 和自定义消息设置 `excludeFromContext` 标记，该消息仅显示不消耗 Token，且在 Session 持久化和压实中都能保留。
- **意义**：大幅提升扩展开发生态的能力上限。

**4. [#5587 [已合并] 首次运行设置流程](https://github.com/earendil-works/pi/pull/5587)**
- **摘要**：`PI_EXPERIMENTAL=1` 激活。首次进入交互模式且默认配置不存在时，自动弹出设置对话：检测终端主题（暗/亮 + 实时预览）、询问遥测分析。降低了新用户上手门槛。
- **意义**：改善新手引导是整个项目向成熟产品迈进的重要一步。

**5. [#5675 [已合并] 修复 Reload 后压实（Compaction）失败](https://github.com/earendil-works/pi/pull/5675)**
- **摘要**：修复长时间会话 Reload 后可执行的 Compaction 抛出 `prevCompaction is not defined` 崩溃的问题。同时修复了压实队列消息投递的边界情况。
- **意义**：**保障长时间工作会话的稳定性**，是解决内存和上下文溢出的关键基础修复。

**6. [#5666 [已合并] 保留 Anthropic 拒绝详情](https://github.com/earendil-works/pi/pull/5666)**
- **摘要**：当 Anthropic 模型的 `stop_reason` 为 `refusal` 时，现在会将后台返回的 `stop_details` 说明传递到前端的 `errorMessage`，而不是只返回干巴巴的拒绝状态。
- **意义**：让模型因内容安全策略拒绝请求时，用户能明确知道原因，大幅提升排错体验。

**7. [#5674 [已合并] 修复 `pi update` 触发“项目信任”弹窗](https://github.com/earendil-works/pi/pull/5674)**
- **摘要**：修复在用户根目录运行 `pi update` 时误触发“是否信任此文件夹”对话框的问题。本次修改避免将 `~/.pi` 误识别为 CWD 的项目目录。
- **意义**：解决了一个高频的日常操作 UI 污染，让更新体验更顺畅。

**8. [#5600 [已合并] 修复 Codex SSE 响应头超时设置](https://github.com/earendil-works/pi/pull/5600)**
- **摘要**：Codex SSE 等待响应头时硬编码超时为 10 秒，不稳定连接下极易超时（即使调用方已配置更长的 `timeoutMs`）。现在将 SSE Header 超时改为遵循用户配置。
- **意义**：直接回应 #4945 中连接稳定性问题的一部分——消除了导致断连的一个重要误报点。

**9. [#5660 [已合并] 修复大写 Header 值被误当作环境变量](https://github.com/earendil-works/pi/pull/5660)**
- **摘要**：修复配置解析引擎将 `models.json` 中全大写字符串（如 `"BEARER"`）解析为 `$BEARER` 的 Bug。正则已做精确化处理。
- **意义**：直接解决了 Issue #5661，修复了一个隐蔽的认证配置 Bug。

**10. [#5634 [已合并] 规范化模型成本数据](https://github.com/earendil-works/pi/pull/5634)**
- **摘要**：清理了 OpenRouter 和 Vercel AI Gateway 上游每 Token 价格换算成每百万 Token 成本时的浮点数伪影，重新生成 `models.generated.ts`。
- **意义**：模型成本显示不再出现奇怪的浮点尾数，提升了费用预览的准确性和可信度。

---

## 功能需求趋势

**1. 基础设施可靠性成为核心维护方向**
- 依赖分裂（#5653）、压实崩溃（#5676）、配置强正则误杀（#5661）等问题频发，社区和开发组正在针对内部复杂性进行系统性清理（Shrinkwrap、Compaction、Config Parsing）。

**2. 模型提供商生态加速扩展**
- **新提供商三巨头**：Anthropic Vertex（PR #5679）、Amazon Bedrock Mantle（#5363）、vLLM DeepSeek（#5673）。社区正在热切地将 Pi 集成到云托管和本地自建的多元环境中。

**3. 从“编程助手”到“通用智能体工作台”**
- **角色系统**（#5577）：用户希望 Pi 能胜任 Security、QA、视频编辑等非编程角色。
- **自定义消息上下文排除**（#5654 / PR #5678）：扩展开发者希望能在不浪费 Token 的情况下与用户交互。
- **原生图像生成**（#4095）：尽管封闭，但再次被提及。

**4. 开发者体验（DX）打磨**
- **首次运行流程**（#5587）、**Tab 补全逻辑**（#5670）、**主题检测**（#5385）等都是近期高频打磨的细节点，项目正在向更成熟的桌面级产品体验靠拢。

---

## 开发者关注点（痛点/高频需求）

**1. 连接稳定性是头号痛点**
- #4945（Codex 卡死在 Working...）是社区热议度最强 Issue。与之相关的 #5558（流式调用无限 Hang）、#5600（SSE 超时硬编码）讨论度同样很高。**用户最不能容忍的是不报错地卡住**。

**2. 配置陷阱较多，认知负荷偏高**
- 环境变量混淆（#5661）、模型信任弹窗误触发（#5619 / PR #5674）、TMPDIR 不可写崩溃（#5667）等问题表明，**配置系统的健壮性和跨平台兼容性仍需加强**。尤其是新用户容易在配置阶段遇挫。

**3. Token 和输出控制机制不足**
- `openai-completions` 的 `maxTokens` 不生效（#5595）、Bash 输出溢出无优雅处理（#5667）等表明，长时间任务和推理模型场景下，**用户对 Token 预算和输出边界的可预测性要求很高**，目前的机制不够完善。

**4. 平台差异问题依旧存在**
- macOS 的特定路径行为（`TMPDIR`、符号链接 `AGENTS.md` 导致 Prompt 重复 #5648）、Bun 的环境缺失（#4160）仍是边缘但棘手的不稳定来源。高频使用用户（尤其是 Mac 用户）感受明显。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-06-13）

---

## 今日速览

- **Qwen Code v0.18.0 正式发布**，主要包含 CLI 复制输出跳过思考段等修复；
- **社区关于 OAuth 免费配额调整的讨论持续发酵**（#3203，127 条评论），引发广泛关注；
- **多个关键 PR 落地**：模型身份识别模糊问题（#5039）、工具调用竞态修复（#5071）、Web Shell 多项增强（#5066）等，平台稳定性和易用性进一步提升。

---

## 版本发布

### v0.18.0

- **更新内容**：
  - `fix(cli): skip thought parts in copy output` – 复制输出时跳过模型思考段，避免无关内容混入；
  - 以及其他依赖更新和发布流程调整。
- **发布说明**：[Release v0.18.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0)

---

## 社区热点 Issues

以下 10 个 Issues 在今日动态中关注度最高，涵盖严重 Bug、关键功能请求与社区重要讨论。

### 1. #3203 – Qwen OAuth 免费配额调整  
- **评论**：127  
- **概要**：建议将免费版日请求量从 1000 次降至 100 次，并计划完全关闭免费入口。社区反响强烈，大量免费用户关注后续变更。  
- **链接**：[Issue #3203](https://github.com/QwenLM/qwen-code/issues/3203)

### 2. #4488 – VSCode 插件在左侧栏不显示  
- **评论**：7  
- **概要**：新版 VSCode（≥1.120.0）中插件图标闪现后消失，影响 IDE 集成体验。用户期望尽快修复以兼容主流编辑器版本。  
- **链接**：[Issue #4488](https://github.com/QwenLM/qwen-code/issues/4488)

### 3. #4514 – Daemon 能力差距与优先级待办（`qwen serve`）  
- **评论**：15  
- **概要**：系统追踪 HTTP/SSE 接口中缺失的守护进程特性（如非交互、ACP 桥接等），是服务端部署用户密切关注的 roadmap。  
- **链接**：[Issue #4514](https://github.com/QwenLM/qwen-code/issues/4514)

### 4. #4877 – 同一模型来自不同 Provider 无法区分  
- **评论**：4  
- **概要**：配置中两个不同提供商使用同名字段时，OpenWork 无法区分，导致模型切换失效。是模型管理中的常见痛点。  
- **链接**：[Issue #4877](https://github.com/QwenLM/qwen-code/issues/4877)

### 5. #5016 – 取消后工具仍继续执行  
- **评论**：2  
- **概要**：SIGINT 中断流式工具调用后，已发出的工具请求仍然被执行，属于正确性/安全性严重 bug。  
- **链接**：[Issue #5016](https://github.com/QwenLM/qwen-code/issues/5016)

### 6. #5015 – 重复工具调用被错误执行  
- **评论**：2  
- **概要**：当模型流输出中出现完全相同的工具多次调用时，本地会重复执行，可能导致多余副作用。  
- **链接**：[Issue #5015](https://github.com/QwenLM/qwen-code/issues/5015)

### 7. #5055 – Windows 版 VSIX 被检测为木马  
- **评论**：2  
- **概要**：用户报告 v0.18.0 的 `.vsix` 文件触发 Windows Defender 报警（Trojan:JS/ShaiWorm.DBA!MTB），引发安全信任疑虑。  
- **链接**：[Issue #5055](https://github.com/QwenLM/qwen-code/issues/5055)

### 8. #4891 – 终端 Resize 时流式内容碎片化  
- **评论**：3  
- **概要**：调整终端窗口尺寸后，滚动历史中出现宽度不一致的片段和错位边框，影响可读性。  
- **链接**：[Issue #4891](https://github.com/QwenLM/qwen-code/issues/4891)

### 9. #4825 – 请求添加 `qwen sessions list` 子命令  
- **评论**：4  
- **概要**：希望获得脚本友好的会话列表输出（支持 `--json`、`--tag`、日期过滤），提升 CLI 会话管理能力。  
- **链接**：[Issue #4825](https://github.com/QwenLM/qwen-code/issues/4825)

### 10. #4821 – 支持声明式 Agent 定义（Frontmatter）  
- **评论**：6  
- **概要**：建议仿照 Claude Code，通过 Markdown 文件 + YAML Frontmatter 定义自定义 Agent，降低自定义 Agent 的开发门槛。  
- **链接**：[Issue #4821](https://github.com/QwenLM/qwen-code/issues/4821)

---

## 重要 PR 进展

以下 10 个 PR 在本周期内取得关键进展，覆盖功能增强、缺陷修复与架构改进。

### 1. #5066 – Web Shell 多项增强  
- **内容**：为守护进程 Web Shell 增加 Token 用量跟踪、i18n 设置面板、重试/流指标、紧凑模式持久化等，大幅提升 Web 端体验。  
- **链接**：[PR #5066](https://github.com/QwenLM/qwen-code/pull/5066)

### 2. #5039 – 使用 `id+baseUrl` 精确模型身份标识  
- **内容**：修复模型选择歧义，引入 `baseUrl` 和 `provider` 字段，直接解决 #4877 问题，并增强配置清晰度。  
- **链接**：[PR #5039](https://github.com/QwenLM/qwen-code/pull/5039)

### 3. #5071 – 修复快速工具结果在流结束后丢失  
- **内容**：修正工具结果交付的竞态条件，确保快速完成的工具不会被回调更新延迟漏传。  
- **链接**：[PR #5071](https://github.com/QwenLM/qwen-code/pull/5071)

### 4. #5003 – 移除工具组边框、折叠已完成结果  
- **内容**：视觉优化，移除工具组圆角边框，紧凑模式下仅显示单行状态，减少界面杂乱。  
- **链接**：[PR #5003](https://github.com/QwenLM/qwen-code/pull/5003)

### 5. #5070 – 忽略已过期 Live Agent 的焦点导航  
- **内容**：修复 #5067，键盘焦点只考虑当前渲染的终端 Agent，避免聚焦隐藏面板导致界面状态异常。  
- **链接**：[PR #5070](https://github.com/QwenLM/qwen-code/pull/5070)

### 6. #5073 – 上下文指令过大时启动警告  
- **内容**：当 `QWEN.md` / context instruction 超过模型上下文 15% 时，在启动时给出警告，预防意外截断。  
- **链接**：[PR #5073](https://github.com/QwenLM/qwen-code/pull/5073)

### 7. #5040 – DaemonTransport 抽象层（REST/ACP WebSocket）  
- **内容**：新增传输抽象，使 DaemonClient 支持 REST+SSE、ACP HTTP+SSE 以及 ACP WebSocket，提升服务端可扩展性。  
- **链接**：[PR #5040](https://github.com/QwenLM/qwen-code/pull/5040)

### 8. #4933 – 配置文件热检测与自动重载  
- **内容**：使用 chokidar 监听 `settings.json` 变化并自动重载配置，无需重启即可生效，优化配置体验。  
- **链接**：[PR #4933](https://github.com/QwenLM/qwen-code/pull/4933)

### 9. #4894 – 修复 FIFO 启动阻塞  
- **内容**：当 `--json-file` 指向命名管道且无读取端时，改用非阻塞打开方式，防止启动挂起。  
- **链接**：[PR #4894](https://github.com/QwenLM/qwen-code/pull/4894)

### 10. #5033 – 为 `qwen serve` 添加 Prompt 队列背压  
- **内容**：实现队列背压机制，防止请求积压导致内存溢出或响应延迟，提升服务稳定性。  
- **链接**：[PR #5033](https://github.com/QwenLM/qwen-code/pull/5033)

---

## 功能需求趋势

从近 24 小时更新的 Issues 中可提炼出社区最关注的几个功能方向：

| 方向 | 典型 Issue |
|------|-----------|
| **模型与 Provider 配置优化** | 同一模型不同 provider 无法区分（#4877）、共享 `baseUrl`（#4813）、fastModel 跨认证类型（#4078） |
| **会话与历史管理增强** | 会话列表子命令（#4825）、CLI 标志保留（#4884）、Goal 迭代持久化（#4999）、文件历史快照持久化（#5057） |
| **Agent 与工具执行可靠性** | 工具重复执行（#5015/5019）、取消后仍执行（#5016）、后台子代理权限队列（#4928） |
| **UI/UX 精细化** | 终端 resize 内容碎片（#4891）、statusline 换行（#5064）、焦点导航改进（#5067）、可折叠思考块（#4598） |
| **平台兼容与安全** | Windows `printf` 兼容（#5010）、VSIX 杀软误报（#5055） |

---

## 开发者关注点

- **工具调用副作用控制**：多个 Bug 指向取消或重复调用时工具仍被执行，严重影响可预测性，开发者期待更严谨的状态机管理。
- **IDE 集成稳定性**：VSCode 插件在新版本中图标闪现消失（#4488），是阻碍新用户入门的主要障碍。
- **长程任务与上下文一致性**：长程任务注意力下降（#5018）、工具重复调用导致会话终止（#5019）、“降智”反馈（#5029），提示模型在长上下文中的稳定性和效率仍需优化。
- **配置复杂度**：模型 Provider 配置冗杂且无法区分同名模型（#4877），用户期望更简洁、唯一性的声明方式。
- **构建产物安全信任**：VSIX 被 Windows Defender 标记（#5055）即使可能误报，仍需官方及时澄清或改进构建流程以防信任损耗。

---

*数据来源：[GitHub - QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) | 生成时间：2026-06-13*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 (2026-06-13)

---

## 今日速览

项目正式更名 **CodeWhale**（v0.8.59 发布），“deepseek-tui” npm 包已弃用。社区围绕 **舰队（fleet）管理** 与 **多 Provider 解绑定** 展开密集开发：原 DeepSeek 硬编码被移除，新增 Z.ai、StepFlash、Anthropic 等原生适配器。UI 侧也收获多项改进（可点击侧边栏、快捷键优化、重绘防冻）。Bug 修复集中在图片上传、MCP 计数和状态同步上。

---

## 版本发布

**v0.8.59**  
代号 **CodeWhale**，新 npm 包名为 `codewhale`。旧版 `deepseek-tui` 不再接收更新。本次发布不含新功能，仅完成更名与迁移指引。用户需参照 `docs/REBRAND.md`。  

[Release 详情](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.59)

---

## 社区热点 Issues

### 1. [bug] 无法上传本地图片  
**#2584** — 用户使用 `/attach` 上传图片并询问多模态模型，但模型仅收到本地文件路径而非 base64 编码。社区 8 条评论，问题已确认并关闭，修复应已合并。  
[#2584](https://github.com/Hmbown/CodeWhale/issues/2584)

### 2. [enhancement] QoL: 任务栏进度、标题动画、完成音效  
**#1871** — 提议在模型处理时显示任务栏进度、窗口标题动态旋转、可配置完成提示音，方便 Alt-Tab 后获取状态反馈。被标记为 v0.8.61，已采纳。  
[#1871](https://github.com/Hmbown/CodeWhale/issues/1871)

### 3. [enhancement] 捆绑 Exa 网络搜索路由  
**#431** — 当设置 `EXA_API_KEY` 时通过 Exa MCP 搜索，否则降级 DDG/Bing。开放中，社区期待提供更多搜索源选择。  
[#431](https://github.com/Hmbown/CodeWhale/issues/431)

### 4. [enhancement] 可配置自动压缩阈值 + Ctrl+L 快捷键  
**#1722** — 上下文接近 100% 时 TUI 完全卡死，提出设置自动压缩阈值和快捷键。已实现并关闭，缓解了记忆溢出问题。  
[#1722](https://github.com/Hmbown/CodeWhale/issues/1722)

### 5. [bug] Sidebar “Work” 面板清单状态不更新  
**#2606** — 引擎完成 checklist 后主聊天正确显示进度，但侧栏“Work”面板仍卡在 “Updating…”。已关闭，修复已入库。  
[#2606](https://github.com/Hmbown/CodeWhale/issues/2606)

### 6. [bug] TUI 状态栏 MCP 计数显示错误  
**#2787** — 同时存在全局与项目级 MCP 配置时，状态栏 MCP 连接数显示异常。已关闭。  
[#2787](https://github.com/Hmbown/CodeWhale/issues/2787)

### 7. [bug/enhancement] 从自动路由和子代理模型选择中解硬编码 DeepSeek  
**#3018** — 自动路由和子代理角色模型只能使用 DeepSeek ID，其他 Provider（Moonshot/Ollama/OpenAI 等）收到 400 错误。此 issue 引发后续大批 PR 重构，已关闭。  
[#3018](https://github.com/Hmbown/CodeWhale/issues/3018)

### 8. [enhancement] EPIC: Web UI 脚手架  
**#471** — 计划使用 SolidJS/React+Vite 构建 Web 界面，通过 SSE 与本地服务器通信。长期项目，开放中。  
[#471](https://github.com/Hmbown/CodeWhale/issues/471)

### 9. [enhancement] 舰队调度器：租约、心跳、背压与失效恢复  
**#3159** — 为大规模子代理引入调度器可靠性，包括租约、心跳、背压和卡死 worker 恢复，是 v0.8.60 关键组件。已关闭。  
[#3159](https://github.com/Hmbown/CodeWhale/issues/3159)

### 10. [bug] 子代理会话名冲突难以诊断  
**#2656** — 代理在编排时因会话名冲突失败但错误信息不清晰。已改进错误提示，关闭。  
[#2656](https://github.com/Hmbown/CodeWhale/issues/2656)

---

## 重要 PR 进展

### 1. feat(config): 新增 Z.ai 和 StepFlash 原生 Provider  
**#3191** — 将智谱 GLM 系列与 StepFun 的 StepFlash 作为一等公民加入，支持对应的环境变量与模型参数。  
[#3191](https://github.com/Hmbown/CodeWhale/pull/3191)

### 2. feat(client): 原生 Anthropic Messages API 适配器  
**#3054** — 支持 cache_control、thinking 块和工具流，可通过 `ANTHROPIC_API_KEY` 直接使用 Claude 模型。  
[#3054](https://github.com/Hmbown/CodeWhale/pull/3054)

### 3. fix(subagent): 子代理模型选择解除 DeepSeek 硬编码  
**#3045** — 允许 Moonshot、Ollama、OpenAI 等使用自有模型 ID 作为子角色模型。配套 PR #3047、#3048 进一步修复能力查找和提示参数化。  
[#3045](https://github.com/Hmbown/CodeWhale/pull/3045)

### 4. feat(hooks): JSON 决策合约、Glob 匹配器、项目级 Hooks  
**#3049** — Hook `tool_call_before` 支持标准 JSON 输出决定、Glob 模式匹配，增加项目本地 hooks 配置，大幅提升自动化精度。  
[#3049](https://github.com/Hmbown/CodeWhale/pull/3049)

### 5. feat(exec): 新增 `--allowed-tools`、`--max-turns` 等 CLI 标志  
**#3042** — 面向 CI/非交互场景，可限制工具集、禁用特定工具、最大轮数、追加系统提示。  
[#3042](https://github.com/Hmbown/CodeWhale/pull/3042)

### 6. feat(tui): 侧边栏行可点击  
**#3040** — Tasks 和 Agents 面板行支持鼠标单击：单击任务详情可取消，单击代理行进入子代理视图。  
[#3040](https://github.com/Hmbown/CodeWhale/pull/3040)

### 7. fix(tui): 节流 AgentProgress 重绘，防止多子代理下 UI 卡死  
**#3035** — 4+ 子代理并发时每个进度事件触发全屏重绘导致冻结；引入节流后大幅改善。  
[#3035](https://github.com/Hmbown/CodeWhale/pull/3035)

### 8. fix(tui): 精简工具调用转录渲染  
**#3037** — 默认紧凑视图隐藏 “(no output)” 行和亚秒级耗时；保留信息同时减少视觉噪音。  
[#3037](https://github.com/Hmbown/CodeWhale/pull/3037)

### 9. fix(tui): Ctrl+B 直接后台运行前台命令  
**#3038** — 移除两层菜单，一键将当前 Shell 命令后台化，改进多任务流程。  
[#3038](https://github.com/Hmbown/CodeWhale/pull/3038)

### 10. fix: 借社区 PR 改进错误消息（工具拒绝、子代理冲突）  
**#3041** — 从社区 PR #2933 抽取三段改进，明确拒绝原因和子代理模型未找到提示，提升可诊断性。  
[#3041](https://github.com/Hmbown/CodeWhale/pull/3041)

---

## 功能需求趋势

- **多 Provider 与模型解绑定**：硬编码 DeepSeek 被彻底解除，Anthropic、Z.ai、StepFlash 等原生支持加入，社区持续要求“任意 Provider + 任意模型”的自由度。  
- **Agent 规模化与可靠性**：v0.8.60 围绕 Subagent/Fleet 引入调度器、租约、心跳、背压、Worker 适配器、可验证任务收据，明显向生产级 agent 集群发展。  
- **IDE 与 Web 界面**：长期有 Web UI 脚手架（#471）和 VS Code 扩展（#461），期望降低 TUI 上手门槛。  
- **权限与安全模型补全**：外部目录门禁、审批记忆、子代理权限自动派生、Hooks JSON 决策 — 社区希望更细粒度的安全控制。  
- **自动化/CI 集成**：`--allowed-tools`、Agent-task issue 模板、Hooks 增强、远程烟雾测试架构，支持无人值守和评测。  
- **UI 交互深度优化**：点击侧边栏、OSC8 超链接、可配置快捷键、任务栏进度 — 提升多任务和高级用户的操作效率。

---

## 开发者关注点

- **Subagent 使用痛点集中**：会话名冲突、eval 需两次调用、工具不可用原因不清等被反复提及，近期 PR 已针对性改善错误消息。  
- **图片上传失效** 影响多模态工作流，得到快速修复。  
- **MCP 配置共存时状态显示错误** 反映了多配置文件合并的测试盲区。  
- **硬编码限制** 曾使社区无法使用自家模型（如 Moonshot Kimi、Ollama），多个 issue 和 PR 合力解决。  
- **高频率需求**：实时状态反馈（任务栏、完成音效）、侧栏交互、上下文监控面板。  
- **Fleet 功能** 目前最受主力开发者期待，预计未来几天将合并更多调度器、SSH worker 与收据系统 PR。

---

> 数据来源：GitHub [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale) （原名 deepseek-tui）

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*