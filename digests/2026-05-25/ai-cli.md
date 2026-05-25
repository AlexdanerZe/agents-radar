# AI CLI 工具社区动态日报 2026-05-25

> 生成时间: 2026-05-25 09:58 UTC | 覆盖工具: 9 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，以下是我基于今日（2026-05-25）各主流 AI CLI 工具社区动态生成的横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-05-25)

**核心判断：** 当前 AI CLI 工具赛道正处于从“尝鲜期”向“生产依赖期”剧烈转变的阵痛阶段。**稳定性与 Agent 行为可预测性**成为社区最核心的诉求，功能数量的增长已不再是主要矛盾。工具间的竞争焦点正从“模型智能”转向“工程可靠性”与“生态互操作性”。**平台方对基础体验的投入深度，将决定谁能赢得开发者的长期信任。**

#### 1. 生态全景

全行业正经历一场 **“信任筑底”** 的艰难过程。所有主流工具的社区动态都显示出相似的矛盾：一方面，多模型路由、Agent 间协议（ACP、MCP）和插件深化等“未来能力”的探索令人兴奋；另一方面，Windows 平台兼容性崩溃、模型响应性能退化、核心配置失效、以及 Agent“失控”执行破坏性操作等基础问题，正在严重消耗用户信任。这标志着市场已进入 **“剩者为王”** 的阶段——谁能率先解决这些基础体验问题，谁就能在下一阶段的竞争中占据显著优势。

#### 2. 各工具活跃度对比

| 工具名称 | 今日热点 Issues 数 | 重要 PR 数 | 版本发布 | 社区活跃焦点 | 总体评价 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 4 | 无 | Windows 网络故障、Agent 误判、插件规则绑定 | 稳定性危机，社区对核心功能回归与数据安全极度敏感。 |
| **OpenAI Codex** | 10 | 10 | 无 | GPT-5.5 性能退化、新功能 `/Goal` 翻车、恶意软件误报 | 功能发布质量严重滑坡，模型信任度降至冰点，急需危机公关与修复。 |
| **Gemini CLI** | 10 | 10 | 无 | Agent 无限挂起、子代理误报成功、配置 “enableInteractiveShell” 失效 | 基础 Agent 稳定性捉襟见肘，社区贡献的修复补丁集中涌现，项目组响应需提速。 |
| **GitHub Copilot CLI** | 10 | 0 | 3 个（Patch） | 终端渲染兼容性（IME/滚动条/粘贴）、插件钩子(Bug | 终端兼容性成为主要摩擦点，社区对多模型支持的呼声强烈。修复节奏频繁但效果待检验。 |
| **Kimi Code CLI** | 3 | 7 | 无 | Agent 协议（ACP）集成、WebSocket 挂起、嵌套 Skill 加载 | **功能演进激进**，社区力量主推 ACP 协议兼容，展现出极强的生态开放性。 |
| **OpenCode** | 10 | 10 | 无 | 模型响应卡顿、Agent 沙箱、内存溢出、支付安全欺诈 | **自由与混乱并存**，创新功能（AI 精神病检测）与严重 Bug（流式中断）齐飞，安全事件引发信任危机。 |
| **Pi** | 10 | 10 | 无 | Codex 模型卡死、XDG 规范支持、阿里云 DashScope 供应商 | **稳扎稳打**，坚固工程基础（RPC 稳定性、XDG 迁移），同时拥抱中文模型生态。 |
| **Qwen Code** | 10 | 10 | 1 个（Nightly） | IDE（VSCode/Rider）兼容性、OOM 崩溃、服务端（Mode B）增强 | 处于 **快速迭代追赶期**，服务端能力显著增强，但 IDE 客户端体验是明显短板。 |
| **CodeWhale** | 10 | 10 | 2 个 | 项目更名阵痛、Docker 崩溃、Agent 控制平面（可中断/恢复） | **品牌重塑关键期**，更名引发分发故障，但 v0.8.45 规划的 Agent 控制平面是行业级亮点。 |

#### 3. 共同关注的功能方向

以下需求在多个工具的社区中高频出现，反映了行业的普遍诉求：

- **Agent 行为边界与安全（跨工具普遍）**：
    - **核心诉求**：阻止 Agent 执行破坏性命令（`git reset --force`），要求对危险操作进行二次确认或沙箱隔离。
    - **涉及工具**：Claude Code (#62168)、Gemini CLI (#22672)、OpenCode (#2242)。
    - **解读**：开发者对 AI “失控”的恐惧是共通的，“人在回路中”不是选项，而是底线。

- **配置与规则的可观察性与可靠性（跨工具普遍）**：
    - **核心诉求**：配置（如超时、删除策略、模型参数）必须严格执行，不应被静默忽略或覆盖。
    - **涉及工具**：Claude Code (#41458)、Gemini CLI (#27418)、OpenCode (#22020)、CodeWhale (#2114)。
    - **解读**：“说了不算”比“功能缺失”更令人沮丧，配置系统的健壮性是专业工具的基本功。

- **跨 IDE/TUI 体验一致性（Claude Code, OpenAI Codex, Copilot CLI）**：
    - **核心诉求**：VSCode 扩展或桌面应用与 TUI 终端的功能不应有差异，如 `/btw` 命令、`/Goal` 功能。
    - **涉及工具**：Claude Code (#37323)、OpenAI Codex (#24269, #20598)。
    - **解读**：用户在不同工作模式下（IDE vs 纯终端）都期望获得同等的 Agent 能力。

- **深度插件/Agent 生态与治理（Claude Code, Copilot CLI, OpenCode, Kimi）**：
    - **核心诉求**：插件应支持规则绑定、按项目启用、来源管理（Git 仓库），并具备更稳定的 SDK。
    - **涉及工具**：Claude Code (#14200)、GitHub Copilot CLI (#3507, #3508)、OpenCode。
    - **解读**：生态已不仅是“安装工具”，而是进入“治理与编排”的深水区。

- **成本透明与 Token 控制（Qwen Code, OpenCode, CodeWhale）**：
    - **核心诉求**：提供详细的 Token 消耗统计、计费审计和实时余额查询功能。
    - **涉及工具**：Qwen Code (#4479)、CodeWhale (#2019)。
    - **解读**：当深度使用时，成本成为核心关切，缺乏透明度将阻碍企业级采纳。

#### 4. 差异化定位分析

- **Claude Code：生态领航者，但正在为“大而全”付出稳定性代价。** 其插件系统和规则治理思路最前沿，但 Windows 支持、数据流失和 Agent 误判等基础问题使其“光环”受损。
- **OpenAI Codex：品牌信任危机中的巨人。** 依赖 GPT 生态，但模型性能和核心功能的退化正在动摇根基。其问题最具代表性，反映了从“实验室预览”到“生产工具”转型的艰难。
- **Gemini CLI：潜力巨大，但基础不稳。** 拥有优秀的模型能力，但 CLI 端的 Agent 稳定性（挂起、误报）严重限制了其价值。当前必须优先修补基础体验。
- **GitHub Copilot CLI：平台优势者，但终端体验是阿喀琉斯之踵。** 背靠 GitHub 生态，功能齐全，但终端渲染兼容性的持续“爆雷”严重影响了其在重度用户中的口碑。
- **Kimi Code CLI：开放的“连接者”。** 将重心置于 ACP、MCP 等开放协议，致力于成为 Agent 生态的枢纽节点。这是一种极具前瞻性的差异化策略，能吸引平台型开发者。
- **OpenCode：社区驱动的“激进创新派”。** 缺乏大厂资源，但社区活跃、创意十足（如 AI 精神病检测）。然而，稳定性问题和安全事件也是其“野性生长”的代价。
- **Pi 与 Qwen Code：“工程师的瑞士军刀”。** Pi 更强调工程健壮性与 Linux 原生体验；Qwen Code 则背靠阿里云，主打中文模型与云服务集成。两者都在解决特定场景下的“好用”问题。
- **CodeWhale：重生的“TUI 先驱”。** 完成更名，聚焦“TUI 中的 Agent 控制平面”这一细分方向，其 v0.8.45 规划是技术亮点，但更名和 Docker 稳定性是短期不确定性。

#### 5. 社区热度与成熟度

- **社区热度最高（讨论量大，情绪高涨）：OpenAI Codex** (电话验证、Mac 误报)、**Claude Code** (Windows 问题、数据丢失)、**Qwen Code** (Docker 乱码) 和 **OpenCode** (模型慢、支付欺诈)。**但热度往往与负面情绪和严重Bug正相关**，并非健康信号。
- **迭代最激进的产品：Kimi Code** (ACP 协议栈快速推进) 和 **CodeWhale** (v0.8.45 多项特性同期推进)，它们正处于功能快速丰富的阶段。
- **成熟度感知最高的产品**：**GitHub Copilot CLI** 发布频繁（Patch），社区对终端兼容性的抱怨虽多，但表明其在大量生产环境中被使用。**Pi** 的议题则更多集中在工程细节打磨，而非根本性的“能不能用”。
- **社区贡献生态最活跃**：**Gemini CLI** 和 **Kimi Code CLI** 的 PR 提交密集，且多为高价值的外部贡献（如修复崩溃、实现新协议），说明其开发者社区的“自愈”能力正在形成。

#### 6. 值得关注的趋势信号

1.  **“稳定性”取代“功能”成为最高优先级**：所有工具的社区都在呐喊“不要搞砸我的代码”和“不要卡死”。这是一个明确的信号，**AI CLI 工具已从“能不能做”迈入“做不做得住”的阶段**。决策者在选型时，应优先考察工具的工程稳健性（如 Windows 支持、错误处理、配置不可变），而非模型数量。

2.  **Agent 行为边界是“一票否决”项**：Agent 自动执行破坏性命令（Claude Code #62168, Gemini CLI #22672）或核心工具死锁（OpenAI Codex #24407），这些不再是普通的 Bug，而是 **“信任核弹”** 。任何一次此类事件都可能导致开发者永久放弃该工具。**自动审批流和沙箱能力将成为产品标配。**

3.  **多模型路由从“加分项”变为“必选项”**：社区不再满足于绑定单一模型体系（Copilot CLI #2854, OpenCode #28846）。用户希望根据任务复杂性、成本和延迟动态选择最合适的模型。**支持自定义模型供应商和路由策略的能力，将成为中大型团队选型的关键考量。**

4.  **“配置即代码”成为产品分水岭**：开发者期望所有行为（Claude Code #14200, Gemini CLI #27406, Copilot CLI #3507）都能通过代码/配置文件声明式地管理，并期望配置被严格尊重。**那些配置系统混乱、优先级不可预测的工具将首先被企业团队淘汰。**

5.  **TUI 与 GUI 的界限模糊化**：TUI 工具不再满足于纯文本交互，正在进化出独立滚动区（CodeWhale）、悬停Tooltip（CodeWhale）、搜索结果高亮（Codex）等“GUI式”交互。这暗示了 **“纯终端”到“混合交互”** 的演进方向，这将是未来 TUI 工具的核心体验竞争力。

**对技术决策者和开发者的建议：**
- **短期（1个月内）**：密切监控您所使用的工具的 **End of Support 公告**（如 CodeWhale 弃用 deepseek 命令）和 **严重稳定性补丁**（如 Codex 的 GPT-5.5 修复、Claude Code 的 Windows 修复）。优先选择发布补丁节奏稳定、对社区反馈响应积极的工具。
- **中期（1-3个月）**：开始评估工具的 **Agent 安全沙箱** 和 **权限审批流程**。将“能否有效阻止 Agent 误操作”作为内部选型的关键评分项。同时，关注 Google Gemini CLI 和 Kimi CLI 在 Agent 稳定性与协议互操作性上的进展。
- **长期（3-6个月）**：考虑构建 **多工具组合或统一网关**，以整合不同工具的优势（如 Pi 的 Linux 体验 + Kimi 的 ACP 生态）。密切关注 **MCP/ACP 协议标准化**的进展，这将是未来 AI 工具协同工作的基石。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为 Claude Code 生态技术分析师，基于您提供的仓库数据，我为您生成了这份社区热点报告。

---

# Claude Code Skills 社区热点报告
（数据截止：2026-05-25 · 来源：github.com/anthropics/skills）

## 1. 热门 Skills 排行 (Top 5-8 PRs)

以下按社区关注度（评论及热度排序）精选了最具代表性的 Skills PRs：

### 🥇 document-typography（PR #514）
- **功能**：对 AI 生成文档进行排版质量控制，自动修复孤行、寡段和编号错位等视觉病句。
- **讨论焦点**：这是首个专门聚焦“排版美学”的 Check 型 Skill。用户公认 AI 输出内容虽好但格式混乱，该 PR 直击 AI 写作体验的最后 10% 质量差距。
- **状态**：**Open**，规则阈值如何界定是社区讨论的重点。
- **链接**：https://github.com/anthropics/skills/pull/514

### 🥇 n8n-builder & n8n-debugger（PR #190）
- **功能**：分别实现基于自然语言快速搭建 n8n 工作流并辅助调试，将 AI 对话转化为自动化流水线。
- **讨论焦点**：工作流自动化是 AI Agent 落地的直接体现，社区反复强调“生成代码不如生成工作流”。该 Skill 是社区公认的“生产力杀手锏”。
- **状态**：**Open**，持续活跃更新至 2026-05-18，作者使用了生产环境验证过的逻辑，合并前景非常好。
- **链接**：https://github.com/anthropics/skills/pull/190

### 🥇 testing-patterns（PR #723）
- **功能**：覆盖全栈测试（单元、React 组件、E2E），引入 Testing Trophy 模型并明确“什么该测、什么不该测”。
- **讨论焦点**：社区对“生成的代码谁来测试”的呼声终于有了回应。大家讨论的是该 Skill 如何与现有代码生成能力无缝编排，而非是否应该接受。
- **状态**：**Open**，内容全面且结构清晰，已被多次引用为“标准测试 Skill 的模板”。
- **链接**：https://github.com/anthropics/skills/pull/723

### 🥇 AURELION 认知框架套件（PR #444）
- **功能**：包含 Kernel、Advisor、Agent、Memory 四个 Skill，构建完整的结构化思维与持久记忆系统。
- **讨论焦点**：突破了“单 Skill”的局限，展示了如何通过多个 Skill 组合打造专业的认知架构。这是社区中“最复杂的代理设计”之一。
- **状态**：**Open**，持续更新至 2026-05-06，讨论集中于命名空间隔离与框架通用性。
- **链接**：https://github.com/anthropics/skills/pull/444

### 🥇 skill-quality & security analyzer（PR #83）
- **功能**：Meta-Skill，用于评估其他技能的结构质量、文档完整度和潜在安全风险。
- **讨论焦点**：随着仓库 Skills 数量爆炸，社区觉醒了对“生态治理”的需求。该 PR 代表社区自下而上推动质量标准化的努力。
- **状态**：**Open**，长期活跃，是“Skill 治理 Skill”范式的代表作。
- **链接**：https://github.com/anthropics/skills/pull/83

### 🥇 ServiceNow 平台技能（PR #568）
- **功能**：全方位覆盖 ServiceNow 平台的 ITSM、ITOM、SecOps、HR 等核心模块。
- **讨论焦点**：企业级 IT 平台的需求极其明显，讨论焦点集中在如何绕过严格的平台权限体系并安全地执行自动化操作。
- **状态**：**Open**（最后更新 2026-04-23），体量巨大但填补了商业生态空白。
- **链接**：https://github.com/anthropics/skills/pull/568

### 🥇 SAP 预测模型技能（PR #181）
- **功能**：驱动 SAP 开源的表格基础模型进行企业数据预测分析。
- **讨论焦点**：标志着 Skills 从纯文本/NLP 正式迈入“数据科学”领域，探讨 Claude 如何作为企业数据工作台。
- **状态**：**Open**，社区对推理成本和 SaaS 集成模式有深度讨论。
- **链接**：https://github.com/anthropics/skills/pull/181

### 🥇 ODT 文档技能（PR #486）
- **功能**：全面支持 ISO 标准的 OpenDocument 格式（.odt, .ods）创建、填充与转换。
- **讨论焦点**：欧洲政府、教育及公共机构对 ODF 标准的强制要求，该 Skill 是 Claude 进入这些合规市场的关键桥梁。
- **状态**：**Open**，讨论侧重于格式互操作性的边界问题（如宏保留）。
- **链接**：https://github.com/anthropics/skills/pull/486

---

## 2. 社区需求趋势（Issues 提炼）

综合 Issues 讨论，当前社区最期待的能力方向为：

- **组织级共享与协作（#228，13评论/7赞）**：当前“下载→传Slack→手动上传”的原始分享流程是企业采用的最大阻塞项。原生 Org 内 Skill 分享库是最高呼声。
- **安全与信任治理（#492，6评论）**：用户已意识到非官方 Skill 可能冒充 Anthropic 官方资源，要求引入签名验证或分级市场策略。
- **生态稳定性与去重（#189, #1087，8赞）**：插件安装机制导致 Skill 重复加载，用户强烈要求更可靠的依赖管理和精确的 Plugin 声明。
- **评估/调试工具链（#556, #202，8评论/6赞）**：`run_eval.py` 触发率 0% 的致命 Bug 导致社区对如何正确创建 Skill 缺乏信心，稳定工具链需求压倒性。
- **跨平台兼容（#29, #1099）**：AWS Bedrock 集成与 Windows 原生 CLI 兼容性是目前 Skill 跨入实际生产环境的主要物理障碍。
- **代理治理与安全规范（#412）**：社区提出了系统性的 Agent 安全范式（策略执行、信任评分、审计追踪），标志着 Skill 从单点任务走向系统级控制的意识觉醒。

---

## 3. 高潜力待合并 Skills

基于评论活跃度、更新频率和实现成熟度，以下 PR 预计近期会落地：

| PR | Skill 名称 | 高概率合并理由 |
|---|---|---|
| **#514** | document-typography | 刚需极强，无争议，随时可能被仓主直接 Merge。 |
| **#190** | n8n-builder / n8n-debugger | 持续活跃更新，生产环境验证，符合 Agent 自动化趋势。 |
| **#723** | testing-patterns | 内容质量极高，社区引用度高，填补开发基础设施空白。 |
| **#538/539/541** | PDF/DOCX 及 Creator 修复集 | 纯 Bug Fix，解决文件损坏与解析崩溃，价值最高，合并优先级最高。 |
| **#1099/1050** | Windows 兼容性修复 | 解决 Windows 用户无法使用 Eval 工具和调用 CLI 的致命问题。 |
| **#444** | AURELION 认知框架 | 虽复杂，但代表了 Skill 设计的前沿范式，有较大参考价值被收录。 |

---

## 4. 生态洞察

**一句话总结：**
当前 Claude Code Skills 社区正从 **“创意爆发期”向“工程成熟期”** 转折，最强烈的诉求已不是“创造更多 Skill”，而是 **“让已有 Skill 更可靠、可共享、可治理”**——具体表现为必须优先解决**生态质量（安全/去重/评估）、组织协作（共享/权限）与跨平台基建（Windows/Bedrock/兼容性）三大核心痛点**。

---

好的，这是为你准备的 2026-05-25 Claude Code 社区动态日报。

---

# Claude Code 社区日报 | 2026-05-25

## 今日速览
今日暂无新版本发布。社区关注点集中在 **Windows 平台突发的网络与 API 错误集群**（#62146, #62181），以及 **Opus 4.7 思考摘要缺失** 这一高赞回归 Bug。功能需求方面，围绕 **插件治理**（规则绑定、按项目启用）和 **IDE 功能一致性** 的呼声依旧强劲。

## 社区热点 Issues

1. **[BUG] Opus 4.7 思考摘要缺失 (#49268)**
   - **热度:** 34条评论 / 57个赞
   - **概述:** 切换至 Opus 4.7 模型后，思考摘要不再显示。经排查是请求中未设置 `display: "summarized"` 参数。
   - **重要性:** ★★★★★。高赞回归性 Bug，严重影响依赖扩展思维功能的用户开发体验。
   - **链接:** [Issue #49268](https://github.com/anthropics/claude-code/issues/49268)

2. **[FEATURE] 插件支持绑定自定义规则 (#14200)**
   - **热度:** 24条评论 / 76个赞
   - **概述:** 请求支持在插件中内嵌或关联 `.claude/rules`，使插件具备上下文感知能力。
   - **重要性:** ★★★★★。社区长期以来的呼声，代表了插件生态从“工具加载”向“智能模块”演进的迫切需求。
   - **链接:** [Issue #14200](https://github.com/anthropics/claude-code/issues/14200)

3. **[BUG] Slack 插件认证失败 (#18009)**
   - **热度:** 18条评论 / 48个赞
   - **概述:** Slack 插件无法完成 OAuth 认证，报错 "*does not support dynamic client registration*"。
   - **重要性:** ★★★★☆。团队协作核心痛点，高赞说明大量团队受阻，对插件可用性造成信任危机。
   - **链接:** [Issue #18009](https://github.com/anthropics/claude-code/issues/18009)

4. **[FEATURE] VS Code 扩展支持 `/btw` 命令 (#37323)**
   - **热度:** 16条评论 / 62个赞
   - **概述:** `/btw` 命令在终端 CLI 可用，但 VS Code 扩展中缺失，请求保持功能一致性。
   - **重要性:** ★★★★☆。62个赞，反映出用户在 IDE 中对其轻量级交互模式的高度依赖。
   - **链接:** [Issue #37323](https://github.com/anthropics/claude-code/issues/37323)

5. **[BUG] `cleanupPeriodDays` 设置项被忽略，490个会话丢失 (#41458)**
   - **热度:** 12条评论 / 数据丢失严重
   - **概述:** 用户明确设定 `cleanupPeriodDays: 99999`，但系统依然按默认策略清理了历史会话。
   - **重要性:** ★★★★★。**数据流失** 问题，直接导致用户对存储机制的信任崩塌。
   - **链接:** [Issue #41458](https://github.com/anthropics/claude-code/issues/41458)

6. **[FEATURE] 支持 Git 仓库作为组织技能源 (#28729)**
   - **热度:** 14条评论 / 30个赞
   - **概述:** 目前技能只能通过 GUI 管理，请求支持将 GitHub/GitLab 仓库直接链接为组织技能的来源。
   - **重要性:** ★★★★☆。企业级治理的关键需求，标志着社区正推动 Claude Code 走向大规模团队协作。
   - **链接:** [Issue #28729](https://github.com/anthropics/claude-code/issues/28729)

7. **[BUG] Windows Node SDK 反复 Socket 断连 (#62146)**
   - **热度:** 今日新增 / 2条评论
   - **概述:** 用户报告在 Windows 平台出现大量 `fetch()` socket 断开连接，引发 Claude Code 和 Claude Desktop 同时报错，并与状态页错误峰值相关联。
   - **重要性:** ★★★★★。**今日最严重的稳定性 Bug**，直接影响 Windows 用户核心工作流。
   - **链接:** [Issue #62146](https://github.com/anthropics/claude-code/issues/62146)

8. **[BUG] Windows 端 API 高错误率 (#62181)**
   - **热度:** 今日新增 / 1条评论
   - **概述:** 用户报错 `ECONNREFUSED`，指数级上升的 API 调用失败，疑似与 socket 断连问题同源。
   - **重要性:** ★★★★☆。与 #62146 联动，可能是客户端与服务端的并发问题。
   - **链接:** [Issue #62181](https://github.com/anthropics/claude-code/issues/62181)

9. **[BUG] Agent 提问后未经确认即执行多步修改 (#62168)**
   - **热度:** 今日新增 / 3条评论
   - **概述:** Agent 在向用户提问后，将用户随附的上下文误判为“批准执行”，直接开始大规模代码修改。
   - **重要性:** ★★★★☆。严重的 **AI 对齐** 问题，用户失去了对 Agent 的控制权。
   - **链接:** [Issue #62168](https://github.com/anthropics/claude-code/issues/62168)

10. **[Enhancement] SSH 远程开发环境下的图片粘贴支持 (#5277)**
    - **热度:** 16条评论 / 30个赞
    - **概述:** 在通过 SSH 连接远程服务器开发时，无法粘贴图片给 Claude Code CLI 理解上下文。
    - **重要性:** ★★★★☆。此需求已存在近一年，是远程开发者的核心工作流短板。
    - **链接:** [Issue #5277](https://github.com/anthropics/claude-code/issues/5277)

## 重要 PR 进展

1. **[Feature] 新增凭证守卫插件 (credential-guard) (#62099)**
   - **状态:** OPEN
   - **概述:** 社区贡献的插件，在 `PreToolUse` 钩子中扫描 20+ 种硬编码凭证模式，阻止密钥被写入文件。
   - **评价:** 极高的社区贡献价值，响应了 #62095 需求，精准切中软件开发安全痛点。
   - **链接:** [PR #62099](https://github.com/anthropics/claude-code/pull/62099)

2. **[Fix] 修复 CI 工作流 `@claude` 触发器误匹配 (#62023)**
   - **状态:** CLOSED (Merged)
   - **概述:** 修复了 `.github/workflows/claude.yml` 中 `@claude` 字符串匹配会误触 `@claude-*` 第三方插件名的问题，改用正则边界匹配。
   - **评价:** 润物细无声的修复，避免了自动化流程的无意义触发。
   - **链接:** [PR #62023](https://github.com/anthropics/claude-code/pull/62023)

3. **[Proposal] CLI 与桌面端会话同步 (#61969)**
   - **状态:** OPEN (Proposal)
   - **概述:** 提案建议将 CLI 端的本地会话历史同步至 Claude 桌面应用，实现双端浏览和复盘。
   - **评价:** 一旦落地将极大提升工作连续性，目前是收集反馈的阶段。
   - **链接:** [PR #61969](https://github.com/anthropics/claude-code/pull/61969)

4. **[Docs] AskUserQuestion 回滚检查点缺失的排查文档 (#61968)**
   - **状态:** OPEN
   - **概述:** 补充了 `AskUserQuestion` 类工具返回后无法创建回滚断点的原因分析（工具结果位于 Assistant 消息内）及回显规避方案。
   - **评价:** 极高的文档价值，解决了用户误以为是 Bug 的逻辑困惑。
   - **链接:** [PR #61968](https://github.com/anthropics/claude-code/pull/61968)

## 功能需求趋势

- **插件深度治理：** 社区不再满足于简单的“安装/卸载”，而是要求插件具备规则绑定（#14200）、按项目精细化开关（#62174）以及组织级来源管理（#28729）。
- **跨端体验一致性：** VS Code 扩展与终端 CLI 的功能差分（如 `/btw` 命令 #37323）成为主要矛盾点，用户希望在 IDE 内获得和终端无差别的 TUI 能力。
- **模型配置扩展：** Opus 4.7 的回归 Bug 和对 Sonnet 4.6 百万级上下文预设的诉求（#53987），表明社区在追求更强模型能力的同时，对配置透明度和可控性要求更高。
- **安全左移：** 从插件层面阻止密钥泄露（#62099）到沙箱写操作逃逸（#52325），社区安全意识正在从被动防御转向主动拦截。

## 开发者关注点

- **稳定性压倒一切：**  今天集中爆发的 Windows 网络断连（#62146）和 API 高错误率（#62181），以及 Opus 4.7 的回归性 Bug，证明频繁的功能迭代必须建立在坚实的基础设施稳定性之上。用户宁可慢，也不要“失控”。
- **Windows 平台体验亟待加固：**  从登录（#44585）、权限（#47821）、网络（#62146）到桌面应用误报（#61673），Windows 用户几乎覆盖了所有平台层面的 Bug。这显然是当前支持力度最薄弱的环节。
- **Agent 行为边界是核心信任点：**  Agent 未经批准擅自执行代码（#62168）是 AI Agent 最致命的信任破坏行为。社区对“人在回路中”的需求极其强烈，期望用户审批流程被严格遵循。
- **配置失效极大消耗信任：**  `cleanupPeriodDays` 被忽略导致数据丢失（#41458）、MCP 超时设置不生效（#16837），这些配置黑盒问题让资深开发者感到强烈的挫败感，反馈“说了不算”。

---

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，以下是基于今日 GitHub 数据生成的 **OpenAI Codex 社区动态日报**。

---

# OpenAI Codex 社区动态日报 | 2026-05-25

## 今日速览

1. **模型性能引发信任危机：** 社区集中反馈 GPT-5.5 系列模型出现严重性能退化，不仅响应速度显著变慢，甚至在修复代码时出现破坏已有功能的严重问题，这是今日最重大的负面动态。
2. **新功能上线即翻车：** 备受瞩目的 `/Goal` 功能在桌面端和 TUI 终端均被报告完全无法使用，反映出该功能发布前的测试存在严重不足。
3. **基础稳定性问题持续发酵：** macOS 恶意软件误报、桌面端对话历史丢失、上下文压缩卡死等长期问题依旧活跃，开发者对 Codex 作为生产工具的可靠性担忧加剧。

---

## 版本发布
今日无新版本发布。

---

## 社区热点 Issues
*以下为本日最值得关注的 10 个 Issue，排序综合考虑了评论数、用户反响及影响范围。*

### 1. 电话验证错误阻止账号登录 (#20161)
- **重要性：** 🔴 极高。评论数高达 **161** 条，点赞 **102**。该问题涉及 SSO 登录后强制要求电话验证且无法绕过，导致用户无法跨设备使用，严重阻碍了用户访问。
- **链接：** [Issues #20161](openai/codex Issue #20161)

### 2. macOS 恶意软件误报 (#23195)
- **重要性：** 🔴 极高。用户在使用 Codex Desktop 过程中突然被 macOS 系统拦截并警告为恶意软件，导致应用无法打开且会话中断，引发了社区广泛恐慌。
- **链接：** [Issues #23195](openai/codex Issue #23195)

### 3. GPT-5.5 Fast 模式严重变慢 (#24422)
- **重要性：** 🔴 极高。核心模型性能严重退化，用户反馈 Fast 模式速度已降至与 Standard 无异，简单任务需等待 10-20 分钟才能完成，极大影响了编码效率。
- **链接：** [Issues #24422](openai/codex Issue #24422)

### 4. GPT-5.5 可靠性显著下降，会破坏已有代码 (#24431)
- **重要性：** 🔴 极高。今日新增反馈，用户抱怨模型不仅无法修复 Bug，甚至在多轮对话后破坏了之前正常的功能。这动摇了用户对模型智能程度和输出质量的信任基础。
- **链接：** [Issues #24431](openai/codex Issue #24431)

### 5. 桌面端对话历史显示错误 (#21076)
- **重要性：** 🟠 高。用户反馈桌面 App 显示的是一份“过时/错误”的对话列表，尽管本地数据库中存在正确的线程。这表明 UI 层与数据层之间存在严重的同步 BUG。
- **链接：** [Issues #21076](openai/codex Issue #21076)

### 6. `/Goal` 指令执行失败 (#24269)
- **重要性：** 🟠 高。作为新推出的核心交互模式，`/Goal` 指令在桌面端始终执行出错，直接导致该功能“不可用”。
- **链接：** [Issues #24269](openai/codex Issue #24269)

### 7. TUI 终端 `/Goal` 功能同样失效 (#20598)
- **重要性：** 🟠 高。与 #24269 相关联，表明该问题不仅限于桌面 App，在 TUI 终端环境中同样存在，指向了后端的统一故障。
- **链接：** [Issues #20598](openai/codex Issue #20598)

### 8. MCP OAuth 缺少资源指示器 (#13891)
- **重要性：** 🟠 高。这是一个影响生态集成的关键 BUG。MCP 登录流程在生成 OAuth 授权 URL 时遗漏了资源指示器，导致生成的 Token 受众错误，影响第三方 MCP 服务器的正确集成。
- **链接：** [Issues #13891](openai/codex Issue #13891)

### 9. 上下文压缩卡住 (<16%) (#14425)
- **重要性：** 🟡 中。这是一个长期存在的性能问题，影响长对话的连续性。当上下文需要压缩时常卡在 16%，导致会话卡死或后退，是重度用户的持续痛点。
- **链接：** [Issues #14425](openai/codex Issue #14425)

### 10. `apply_patch` 文件变更工具死锁 (#24407)
- **重要性：** 🟡 中。核心执行工具存在非确定性死锁（添加文件接近 100%，更新文件约 50% 的概率），导致任务永远无法完成，必须重启。对于依赖 CLI 自动化的用户而言非常致命。
- **链接：** [Issues #24407](openai/codex Issue #24407)

---

## 重要 PR 进展
*以下为 10 个值得关注的重要 PR，内容涉及核心稳定性修复、功能优化及新能力探索。*

### 1. 防止自动压缩陷入死循环 (#23585)
- **内容：** 当自动压缩成功执行后，若上下文仍处于触发阈值，系统会陷入“执行-压缩”的死循环。此 PR 新增了防护逻辑，可有效退出该状态。
- **链接：** [PR #23585](openai/codex PR #23585)

### 2. 拒绝空 Base64 图片输入，防止线程中毒 (#24376)
- **内容：** 拦截并清理空 Base64 图片。这些图片会污染对话历史，在恢复会话时导致 API 调用失败。此 PR 从源头切断了这一常见的线程中毒路径。
- **链接：** [PR #24376](openai/codex PR #24376)

### 3. 修复 TUI 对 Tmux 扩展键模式兼容性问题 (#24371)
- **内容：** 修复了 Codex 0.131 版本启用 Tmux `modifyOtherKeys` 模式后，导致 iTerm2 控制模式失效的问题。现在会正确识别兼容的终端格式。
- **链接：** [PR #24371](openai/codex PR #24371)

### 4. 新增 Doctor 线程清单审计命令 (#24305)
- **内容：** 新增诊断功能，用于对比本地 SQLite 状态数据库与磁盘上持久化的 JSONL 文件，帮助用户和官方排查“会话丢失”问题。
- **链接：** [PR #24305](openai/codex PR #24305)

### 5. 在请求头中标记压缩元数据 (#24368)
- **内容：** 在 API 请求中显式标记压缩类型，并附带压缩调度元数据以提升对上下文管理行为的可观察性。
- **链接：** [PR #24368](openai/codex PR #24368)

### 6. 引导用户接受自动压缩机制 (#24356)
- **内容：** 针对喜欢手动压缩的用户，当他们手动执行压缩时，系统会提供温和的提示，引导用户信任自动压缩功能，以减少不必要的干预。
- **链接：** [PR #24356](openai/codex PR #24356)

### 7. TUI 增强 Vim 文本对象操作 (#24382)
- **内容：** 在 TUI 编辑器中完善了 Vim 模式，新增了 `ciw`、`da(`、`di”` 等常用文本对象组合的操作，提升了代码编辑流畅度。
- **链接：** [PR #24382](openai/codex PR #24382)

### 8. 在 `/status` 中显示远程连接详情 (#24420)
- **内容：** 允许用户通过 `/status` 命令查看当前 TUI 是否通过远程传输连接，并显示远程服务器版本。这对于调试 SSH 连接问题非常有帮助。
- **链接：** [PR #24420](openai/codex PR #24420)

### 9. TUI 增加对话记录搜索功能 (#23539)
- **内容：** 为 TUI 的对话记录覆盖层增加了任意文本搜索能力。在拥有大量 prompt 的长会话中，用户可以快速定位到特定内容，大幅提升了导航效率。
- **链接：** [PR #23539](openai/codex PR #23539)

### 10. 新增 “Review Story” 交互式代码审查功能 (系列 PRs)
- **内容：** #24358 / #24350 / #24353 系列 PR 引入了全新的“Review Story”。功能将代码 diff 转换为有序的模型生成叙事，并支持在 TUI 中进行交互式阅读，且支持渐进式生成体验。
- **链接：** [PR #24358](openai/codex PR #24358)

---

## 功能需求趋势
*根据近期 Issues 与 PR 走向，社区最关注的功能方向如下：*

1. **模型行为透明度与性能稳定性：** 社区强烈要求 GPT-5.5 模型提供更稳定的性能指标，并优化“黑盒”现象。用户需要明确的信号来知道模型是处于“正常思考”还是“缓慢/错误状态”。
2. **上下文管理的可视化回归：** 多个 Issue 表明用户非常依赖上下文进度条。在最近的更新中，桌面端和插件端的指示器被移除引发了大量不满，社区呼吁恢复并优化该组件。
3. **跨平台体验统一：** macOS 的安全警告、Windows 的窗口冻结、以及移动端 Remote Control 功能的连接不稳定，暴露出严重的平台兼容性差距。用户希望核心功能在所有平台上体验一致。
4. **MCP 与 IDE 深度集成：** 用户期望在 Codex VSCode 扩展中获得与 GitHub Copilot 平级的 MCP 管理能力（#2901），支持 `mcp.json` 配置，实现企业级的协议管理。

---

## 开发者关注点
*针对开发者反馈，当前的高频痛点和需求总结如下：*

1. **模型质量是生命线：** 当前最紧急的诉求是修复 GPT-5.5 的性能和代码生成质量。开发者普遍表示近期的模型退化已经严重影响日常开发，甚至造成了项目回退，信任度降至冰点。
2. **核心功能 Bug 不可接受：** 无论是 `/Goal` 的完全无法使用，还是 `apply_patch` 的死锁，亦或是上下文压缩卡死，这些核心功能的崩溃对于将 AI 作为生产力工具的开发者而言是致命的。社区呼吁严格把控发布质量。
3. **需要更强的用户可见性：** 当后台执行远程任务、模型变慢、或连接切换时，用户界面缺乏清晰的标识。开发者不想依赖猜测或第三方诊断工具来感知应用状态。
4. **移动端体验严重制约自由：** 尽管 Remote Control 功能概念上很有吸引力，但实际使用中 Android 端无法加载线程、iOS 端 SSH 连接不可靠等问题，使得该功能在现有状态下几乎无法用于严肃工作。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 (2026-05-25)

## 今日速览
过去24小时无新版本发布，但社区活跃度较高。**多个关键修复PR集中提交**：`--resume` 时 PTY 句柄陈旧导致的崩溃、非交互式 Shell 忽略 `enableInteractiveShell: false` 的问题以及工具调用超时配置等均被社区开发者重点攻克。与此同时，**Agent 稳定性的老问题仍在发酵**，通用代理无限挂起（#21409）和子代理超时误报成功（#22323）引发持续讨论。

---

## 版本发布
无

---

## 社区热点 Issues

### 1. Generalist agent 无限挂起 [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **优先级**: P1 | **👍 8** | **评论 7**
- **摘要**: 委托给通用 agent 后 CLI 无限挂起，简单的文件夹创建也无法完成。用户发现通过提示词禁止使用子代理可临时规避。
- **社区关注**: 该问题严重影响日常使用，属于最严重影响之一，已被标记 `need-retesting`，但尚未修复。

### 2. 子代理 MAX_TURNS 后错误报告成功 [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **优先级**: P1 | **👍 2** | **评论 6**
- **摘要**: `codebase_investigator` 子代理已达最大轮数但返回 `success`/`GOAL`，实际并未完成分析，导致用户误信结果。
- **社区关注**: 直接破坏了对子代理执行结果的信任，开发者已标记 `need-retesting`。

### 3. Shell 命令执行后卡死 [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **优先级**: P1 | **👍 3** | **评论 4**
- **摘要**: 极简单的 shell 命令（如 `ls`）执行完毕后 CLI 仍显示“等待输入”，进程始终活跃。
- **社区关注**: 频繁出现，严重破坏交互流，影响范围广。

### 4. 浏览器子代理在 Wayland 下崩溃 [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
- **优先级**: P1 | **👍 1** | **评论 4**
- **摘要**: 在 Wayland 上运行浏览器子代理会导致终端全屏显示混乱并失败。
- **社区关注**: Linux 用户受影响明显，急需兼容性修复。

### 5. 自动内存缺少确定性编辑 & 过度日志 [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
- **优先级**: P2 | **评论 3**
- **摘要**: Auto Memory 在读取本地转录后才会指示模型编辑，内容已进入模型上下文；同时服务日志可能记录敏感信息。
- **社区关注**: 隐私安全侧漏洞，社区建议在发送前强制编辑。

### 6. 自动内存无效补丁被静默跳过 [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)
- **优先级**: P2 | **评论 3**
- **摘要**: 收件箱静默跳过畸形补丁，但聚合删除只移除有效补丁，导致背景提取器无限重读 `.patch` 文件。
- **社区关注**: 自动化功能出现循环浪费，影响使用体验。

### 7. 自动内存无限重试低信号会话 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **优先级**: P2 | **评论 3**
- **摘要**: 若提取代理认为某会话为低信号而不读取，该会话不会被标记已处理，下次仍会重复出现并重试，消耗配额。
- **社区关注**: 资源浪费问题，社区期望对已跳过的会话做持久化标记。

### 8. 超过 128 个工具时返回 400 错误 [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)
- **优先级**: P2 | **评论 3**
- **摘要**: 当可用工具超过 128 个时直接拒绝请求（400 error），期望 Agent 能动态限制当前关心的工具范围。
- **社区关注**: 工具生态扩展后，容量瓶颈突出。

### 9. Gemini 不主动使用技能/子代理 [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **优先级**: P2 | **评论 6**
- **摘要**: 用户配置了 Gradle、Git 等技能，但模型几乎从不主动调用，除非明确指示。
- **社区关注**: 技能系统价值未充分发挥，社区希望模型能根据上下文主动决策。

### 10. Agent 应阻止破坏性行为 [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)
- **优先级**: P2 | **👍 1** | **评论 2**
- **摘要**: 复杂 Git 操作、数据库修改等场景下，模型会使用 `git reset --force` 等危险命令，而安全替代方案可用。
- **社区关注**: 社区希望默认行为更保守，或加入主动确认/回溯机制。

---

## 重要 PR 进展

### 1. 可配置数值路由规则（修复 #21805） [#27406](https://github.com/google-gemini/gemini-cli/pull/27406)
- **作者**: ujjwalv01 | **状态**: OPEN | **标签**: `area/agent help wanted`
- **要点**: 允许用户在 `settings.json` 中定义复杂度得分到模型的映射，替代硬编码二分阈值。
- **意义**: 这是社区期待的功能需求，精细路由可优化成本与质量。

### 2. 处理 resizePty 的 EBADF 错误 [#27429](https://github.com/google-gemini/gemini-cli/pull/27429)
- **作者**: LifeJiggy | **状态**: OPEN | **标签**: `priority/p1 area/core`
- **要点**: `--resume` 时 PTY fd 已失效，`ioctl` 返回 EBADF 导致崩溃；此 PR 将 EBADF 视同 ESRCH 静默忽略。
- **意义**: 直接修复 session resume 高频崩溃，社区贡献。

### 3. 修复 Docker sandbox 镜像检查 [#27428](https://github.com/google-gemini/gemini-cli/pull/27428)
- **作者**: LifeJiggy | **状态**: OPEN | **标签**: `priority/p1 area/core area/platform`
- **要点**: 改用 `docker inspect` 返回值替代解析 `docker images -q` 输出，解决 DOCKER_BUILDKIT 下假阴性。
- **意义**: 提升沙箱功能可靠性。

### 4. 非交互式 Shell 尊重 `enableInteractiveShell: false` [#27418](https://github.com/google-gemini/gemini-cli/pull/27418)
- **作者**: stevescherer-sherpa | **状态**: OPEN | **标签**: `priority/p1 area/non-interactive`
- **要点**: `shellExecutionService` 忽略设置，导致非交互模式仍启动交互 Shell；此 PR 强制遵守配置并增强桥接稳定性（处理非 UTF-8 字节/堆限制）。
- **意义**: 修复企业级场景的核心配置生效问题。

### 5. 可配置单工具调用超时 [#27423](https://github.com/google-gemini/gemini-cli/pull/27423)
- **作者**: officialasishkumar | **状态**: OPEN | **标签**: `priority/p3 area/agent help wanted`
- **要点**: 新增 `tools.callTimeout` 设置，限制任何单一工具调用的最大耗时，解决 shell 命令无限运行问题。
- **意义**: 社区长期呼吁的功能（#3375），提升可控性。

### 6. 从自定义路径读取 Bootstrap 设置 [#27425](https://github.com/google-gemini/gemini-cli/pull/27425)
- **作者**: officialasishkumar | **状态**: OPEN | **标签**: `priority/p2 area/core`
- **要点**: 当设置 `GEMINI_CLI_HOME` 时，bootstrap 阶段也从该路径而非默认路径读取配置。
- **意义**: 修补多环境配置一致性问题。

### 7. 停止扩展更新失败后遗留无效状态 [#26930](https://github.com/google-gemini/gemini-cli/pull/26930)
- **作者**: Eswar809 | **状态**: CLOSED | **标签**: `priority/p1 area/extensions`
- **要点**: 若扩展更新中失败（复制、完整性检查等），恢复原有版本，而非留空。
- **意义**: 扩展生态的兜底机制，避免用户完全失去功能。

### 8. 修复 A2A Server 设置深浅合并 [#26931](https://github.com/google-gemini/gemini-cli/pull/26931)
- **作者**: Eswar809 | **状态**: CLOSED | **标签**: `priority/p2 area/core`
- **要点**: 工作区设置只指定部分嵌套 key 时，会丢弃用户设置的其他嵌套 key；改为深度合并。
- **意义**: 配置系统行为符合预期。

### 9. 非交互路径下处理 refreshAuth 拒绝 [#26932](https://github.com/google-gemini/gemini-cli/pull/26932)
- **作者**: Eswar809 | **状态**: CLOSED | **标签**: `priority/p1 area/core`
- **要点**: 非交互流程中 OAuth 刷新未捕获错误导致未处理 Promise 拒绝而崩溃。
- **意义**: 提升非交互/CI 场景稳定性。

### 10. 默认回退链加入 flash-lite 模型 [#26914](https://github.com/google-gemini/gemini-cli/pull/26914)
- **作者**: Eswar809 | **状态**: CLOSED | **标签**: `priority/p1 area/core area/agent area/security area/platform`
- **要点**: 当 Pro 和 Flash 配额耗尽时自动降级到 `gemini-2.5-flash-lite`（免费层 1000 RPD），无需手动指定模型。
- **意义**: 免费用户友好性大幅提升，降低使用门槛。

---

## 功能需求趋势

1. **动态模型路由与超时配置** – 社区不满足于固定阈值，希望按任务复杂度/成本动态选择模型（#27406），并给工具调用设置独立超时（#27423）。反映 fine-grained control 的强烈需求。
2. **内存系统完善** – Auto Memory 的隐私编辑（#26525）、无效补丁处理（#26523）、低信号会话跳过（#26522）等要求表明，用户对自动化记忆功能有更高期望，不愿承担配额浪费或安全风险。
3. **AST 感知工具探索** – #22745 系列 Epic 关注利用 AST 实现更精确的代码读取、搜索和代码库映射，期待减少 token 消耗和错误读取。
4. **服务器驱动模型管理** – #20878 提出通过 `LoadCodeAssist` 端点远程获取模型列表，减轻客户端维护负担，与云服务趋势一致。
5. **远程代理与后台操作** – 社区希望子代理可后台化（#22741），并对远程代理提供高级认证和异步操作（#20303），进一步扩展 CLI 的自动化边界。

---

## 开发者关注点

- **Agent 稳定性仍是头号痛点** – 通用 agent 挂起（#21409）、子代理误报（#22323）、shell 卡死（#25166）不断出现，严重影响可信度。**建议项目组优先修复这些“基础体验”问题**。
- **配置生效不可靠** – 浏览器 agent 忽略 `settings.json`（#22267）、子代理无视禁用设置（#22093）、非交互模式忽略 `enableInteractiveShell: false`（#27418），开发者期望 **“一次配置，处处生效”**。
- **破坏性行为缺乏防护** – 模型使用 `git reset --force` 等危险命令（#22672），用户需要安全护栏（如自动备份、undo stack 或前置确认）。
- **扩展兼容性与恢复** – 扩展更新失败可能遗留空状态，社区贡献的恢复旧版本功能（#26930）说明用户将自己动手解决此类问题。**官方需提供更健壮的扩展生命周期管理**。
- **终端兼容性持续摩擦** – Wayland 下浏览器 agent 失败（#21983）、终端 resize 性能问题（#21924）、外部编辑器退出后界面混乱（#24935），尤其是 Linux 用户受影响较深。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我为您整理了 2026-05-25 日的 GitHub Copilot CLI 社区动态日报。

---

# GitHub Copilot CLI 社区动态日报
**日期：2026-05-25 | 分析师：AI 开发工具技术分析师**

## 1. 今日速览

今日发布了 `v1.0.55-0` 补丁，修复了单文件打包（SEA）场景下扩展加载失效的问题。终端渲染兼容性成为本周最大的雷区，macOS 中文输入法错乱（👍 29）、Windows 滚动条错位以及输出内容无故裁剪等问题集中爆发。同时，社区对原生支持 **Google Gemini 模型** 的呼声（👍 15）达到了新高，标志着社区对多模型路由的渴望愈发强烈。

## 2. 版本发布

今天共收录了 3 个版本的更新，主要集中在 Bug 修复与功能完善：

- **v1.0.55-0** (2026-05-25):
  - **修复**: 解决了 CLI 在打包为单文件可执行文件（SEA）时，扩展启动失败的问题。
- **v1.0.54** (2026-05-24):
  - **变更**: 常规修复与性能改进。
- **v1.0.53** (2026-05-24):
  - **修复**: 多行提示现在可以完整显示，不会有内容被截断或选择偏移。
  - **修复**: `/skills` 选择器现在正确地遵循 `--config-dir` 参数来保存用户偏好。
  - **修复**: 当环境中设置了 `PS0` 或 `PROMPT_COMMAND` 环境变量时，Bash 会话不再挂起。

## 3. 社区热点 Issues

挑选过去 24 小时内最受关注的 10 个 Issue：

1. **[#3502] macOS 内置输入法预编辑文本渲染异常** (👍 29)
   - **简介**: 在 macOS 下使用中文注音输入法时，拼音（预编辑文本）会堆积在终端右下角，而非显示在光标位置。
   - **重要性**: 高达 29 个赞，是目前社区情绪最强烈的 UI Bug，严重影响非英文用户的核心交互体验。
   - [链接](https://github.com/github/copilot-cli/issues/3502)

2. **[#2854] 请求支持 Google Gemini 模型** (👍 15)
   - **简介**: 用户明确要求 Copilot CLI 接入 Google Gemini 模型，目前仅支持 OpenAI 系模型。
   - **重要性**: 15 个赞位居 Feature Request 榜首，反映了社区对选择权和模型多样性的强烈诉求。
   - [链接](https://github.com/github/copilot-cli/issues/2854)

3. **[#2317] 执行命令后 ~/.bash_history 被截断** (👍 8)
   - **简介**: Copilot 执行 Bash 命令时会错误截断用户的 `~/.bash_history`，无视 `HISTFILESIZE` 等配置。
   - **重要性**: 这是一个严重的数据安全 Bug，触动了用户对 CLI 工具的信任底线。虽已修复但评论认为仍有残留问题。
   - [链接](https://github.com/github/copilot-cli/issues/2317)

4. **[#3497] 终端输出在 Resize/重排后被裁剪且不可达** (👍 8)
   - **简介**: 在调整终端窗口大小后，长输出的部分内容不可见，且无法通过滚动条访问。
   - **重要性**: 核心体验回归，严重影响长代码块或日志的输出浏览。
   - [链接](https://github.com/github/copilot-cli/issues/3497)

5. **[#3501] Windows 下滚动条导致文本错位** (👍 7)
   - **简介**: 引入垂直滚动条后，Windows Terminal 和 Console Host 下的文本渲染无法对齐。
   - **重要性**: Windows 平台下的高频 UI 问题，影响用户阅读舒适度。
   - [链接](https://github.com/github/copilot-cli/issues/3501)

6. **[#3333] v1.0.48+ 破坏了 Android/Termux 支持** (glibc 依赖)
   - **简介**: `runtime.node` 原生模块编译时链接到了 glibc，导致在运行 Bionic libc 的 Termux 上无法运行。
   - **重要性**: 虽然只有 1 个赞，但这意味着一个特定用户群体（Android 开发者）的完全被排除。
   - [链接](https://github.com/github/copilot-cli/issues/3333)

7. **[#3414] GNOME Wayland 下粘贴功能回归**
   - **简介**: 在 Ubuntu GNOME Wayland 环境下，升级到 v1.0.49 后文本粘贴异常。
   - **重要性**: 针对 Linux 主流桌面环境的关键输入功能失效。
   - [链接](https://github.com/github/copilot-cli/issues/3414)

8. **[#3514] `list_agents` 返回空列表但后台 Agent 仍运行**
   - **简介**: 调用 `list_agents` 工具返回 `<no background agents>`，但 UI 上能看到 7 个活跃的 Agent 在运行。
   - **重要性**: 暴露了 Agent 系统内部的严重状态管理 Bug，导致 AI 无法正确感知上下文环境。
   - [链接](https://github.com/github/copilot-cli/issues/3514)

9. **[#3508] 扩展生命周期钩子获取的 `workingDirectory` 为空**
   - **简介**: 自 CLI 1.0.51 起，`onSessionStart`、`onPreToolUse` 等钩子接收到的 `workingDirectory` 为空字符串。
   - **重要性**: 严重破坏了依赖工作目录的第三方插件功能。
   - [链接](https://github.com/github/copilot-cli/issues/3508)

10. **[#3507] `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` 环境变量支持不完整**
    - **简介**: 该环境变量对 `AGENTS.md` 和 `.github/instructions/**` 有效，但对 `CLAUDE.md`、`GEMINI.md` 等常用项目级指令文件无效。
    - **重要性**: 配置行为一致性存在缺陷，导致用户迁移或 CI/CD 集成困难。
    - [链接](https://github.com/github/copilot-cli/issues/3507)

## 4. 重要 PR 进展

**无更新。** 过去 24 小时内没有 Pull Request 提交或更新。这表明团队可能正处于一个密集的稳定期或忙于内部审查，集中精力修复上述爆发的终端兼容性问题。

## 5. 功能需求趋势

从最近的 Issues 中可以提炼出以下几个关键的功能演进方向：

- **多模型路由**: 以 **Google Gemini**（#2854）为代表的第二大模型接入请求，社区不再满足于单一的 OpenAI 体系。
- **Agent 生态深化**:
  - **多源目录支持**: 用户期望像 Skills 一样支持从多个路径加载 Agent（#3505）。
  - **子 Agent 工具链继承**: 父 Agent 调用子 Agent 时，工具集应继承而非丢弃（#3506）。
  - **MCP 交互体验优化**: MCP 服务器工具列表的滚动和查看体验亟待改进（#3486）。
- **IDE 功能下移**: 用户期望 CLI 拥有 VS Code 中那样便捷的**可视化创建工作流**（如内置 `/create-skill`、`/create-agent` 等指令）（#3503）。
- **移动端协同**: 随着 GitHub Mobile App 远程会话的普及，**UI 渲染**（#3498）、**通知机制**（远程 Agent 阻塞时手机通知）（#3512）和**计费配额逻辑**（#2979）成为新的关注点。

## 6. 开发者关注点

汇总社区开发者的核心痛点与高频需求：

- **🔥 终端渲染兼容性是主要矛盾**: 不同平台（macOS IME、Windows 滚动条、Linux Wayland 粘贴、Resize 闪烁）逐一响起警报。这说明 CLI 的终端渲染层（TUI）存在深层架构问题，亟需重构或加固。
- **🛠️ Plugin/SDK 成熟度不足**:
  - **调试困难**: 生命周期钩子的输入数据（如 `workingDirectory`）都不可靠（#3508）。
  - **静默失败**: Skill 描述超过 1024 字符直接丢弃无任何反馈（#3494）。
  - **状态不一致**: `list_agents` 无法反映真实运行状态（#3514）。
  - 新插件系统的可靠性严重影响了第三方开发者的信心。
- **⚙️ 配置灵活性有待提升**:
  - 环境变量 `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` 支持不完整（#3507）。
  - `/skills` 界面不遵守 `--config-dir`（虽已修复，但也反映了过去几个月配置管理的混乱）。
- **🔒 数据安全与行为一致性**:
  - `Bash_history` 截断问题（#2317）提醒了开发者，对终端核心文件的操作必须慎之又慎。任何意外篡改都会导致用户强流失。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，收到您的指令。请查收基于提供数据生成的 **Kimi Code CLI 社区动态日报**。

---

# Kimi Code CLI 社区动态日报 — 2026-05-25

**数据来源:** github.com/MoonshotAI/kimi-cli

---

## 1. 今日速览

昨日项目活跃度较高，共 3 个活跃 Issue 和 7 个 PR 获得更新。**ACP（Agent Communication Protocol）协议支持**是当前最大的功能演进热点，外部贡献者连续提交 3 个栈式 PR（#2359, #2363, #2364），系统性地提升 Kimi 在 Agent 互联层面的能力。与此同时，**稳定性与兼容性**仍是社区关注的核心：WebSocket API 触发 Worker 挂起（#2365）属于高优先级 Bug，而嵌套 Skill 目录（#1894）则反映了与 Codex 生态对齐的持续诉求。

---

## 2. 版本发布

过去 24 小时内无新版本发布。

---

## 3. 社区热点 Issues

*共 3 条活跃 Issue，以下逐一分析：*

1. **[#1894 Enhancement] 嵌套 Skill 目录加载兼容性**
   - **重要性**: 用户明确指出了 Kimi CLI 与 Codex 在功能粒度上的关键差异。若缺失递归加载能力，依赖复杂 `.agents/skills/{name}/skills/` 结构的项目将无法在 Kimi 中运行，这是从 Codex 生态迁移的核心障碍之一。
   - **社区反应**: Issue 创建于 4 月 15 日，昨日有更新，共 4 条评论。社区讨论了该功能实现的复杂度，但目前尚未被官方标记或排期，用户期待度较高。
   - **链接**: [Issue #1894](https://github.com/MoonshotAI/kimi-cli/issues/1894)

2. **[#2232 Enhancement] 后台任务超时时间可调**
   - **重要性**: 直击 Agent 自动化任务的痛点。Kimi 的“一刀切”静默超时策略缺乏灵活性，导致长时间运行的任务中途被强制终止，开发者希望获得动态调整超时或预设策略的能力。这是提升生产可靠性的关键诉求。
   - **社区反应**: 2 条评论，用户建议能否在任务启动后实时调整 timeout 参数，而不是终止重来。
   - **链接**: [Issue #2232](https://github.com/MoonshotAI/kimi-cli/issues/2232)

3. **[#2365 Bug] kimi-code-worker 通过 WebSocket API 调用 Shell 工具挂死**
   - **重要性**: 昨日刚提交的新 Bug，涉及 WebSocket 接口的严重稳定性问题。Work Flow 中调用 Shell 工具会导致 Worker 进程无响应，严重阻碍 IDE 插件或自动化平台的远程集成。
   - **社区反应**: 暂无评论，但提交者提供了完整的复现环境（版本 1.44.0，Linux + Python 3.12/3.13），信息完备，应优先排查。
   - **链接**: [Issue #2365](https://github.com/MoonshotAI/kimi-cli/issues/2365)

---

## 4. 重要 PR 进展

*共 7 个 PR 获得更新，覆盖重构、ACP 协议、跨平台兼容和文档建设：*

1. **[#1707 提议] 全量重构：Python 迁移至 Bun + TypeScript**
   - **内容**: 社区成员 `Yuandiaodiaodiao` 提交了极具野心的重构 PR（166 个 TS 文件，约 3.2 万行代码），完全放弃 Python 栈，转向 Bun + TypeScript + React Ink。
   - **观察**: 尽管合并可能性暂不明朗，但该 PR 侧面反映出社区中对当前 Python 版本（依赖重、启动慢）存在改进呼声。
   - **链接**: [PR #1707](https://github.com/MoonshotAI/kimi-cli/pull/1707)

2. **[ACP 协议栈 PR #2359] fix(acp): 为流式内容分配消息 ID**
   - **内容**: 升级至 ACP SDK 0.10.0，修复流式传输时缺少 `messageId` 的缺陷，这是实现可靠 Session 追踪的基础。
   - **链接**: [PR #2359](https://github.com/MoonshotAI/kimi-cli/pull/2359)

3. **[ACP 协议栈 PR #2363] fix(acp): 重放加载的 Session 历史**
   - **内容**: 基于 #2359，确保 `session/load` 端点能正确重放历史消息上下文，防止恢复对话后丢失信息。
   - **链接**: [PR #2363](https://github.com/MoonshotAI/kimi-cli/pull/2363)

4. **[ACP 协议栈 PR #2364] feat(acp): 支持权限模式切换**
   - **内容**: 实现协议级别的权限模式（Permission Mode）切换，关联 Issue #1414。这使得外部应用能通过 ACP 协议控制 Kimi 的审批流程。
   - **观察**: #2359 → #2363 → #2364 构成完整的 ACP 增强链条。贡献者 `huntharo` 正在为 **PwrAgent** 平台集成 Kimi，这表明第三方 Agent 平台正在积极对接 Kimi 生态。
   - **链接**: [PR #2364](https://github.com/MoonshotAI/kimi-cli/pull/2364)

5. **[#2362 修复] 保留原始文件换行风格 & 修复跨平台 CRLF/LF 问题**
   - **内容**: 修复 `StrReplaceFile` 和 `WriteFile` 工具在编辑文件时，默认将 `\r\n`（Windows）转换为 `\n`（Linux）的问题，由 `readtext()` 的 universal newlines 模式引起。
   - **观察**: 修复了 #1952 和 #2191，这是一个非常实用的跨平台协作 Bug 修复。
   - **链接**: [PR #2362](https://github.com/MoonshotAI/kimi-cli/pull/2362)

6. **[#2361 & #2335 文档修复] 澄清/修正 Notification Hook 示例**
   - **内容**: 两位贡献者 `Randy-sin` 和 `he-yufeng` 均指出 Hooks 文档中 `Notification` 的 Matcher 示例不可用（误用了 `permission_prompt`），并修正为实际的后台任务通知类型。
   - **观察**: 多个 PR 修改同一处文档错误，说明该文档确实造成了混淆，阻碍了用户自定义 Hooks 系统的积极性。
   - **链接**: [PR #2361](https://github.com/MoonshotAI/kimi-cli/pull/2361), [PR #2335](https://github.com/MoonshotAI/kimi-cli/pull/2335)

---

## 5. 功能需求趋势

- **协议互操作性（ACP 优先）**: 社区力量正在强势推动 Kimi 在 ACP 协议侧的成熟度。从流式消息 ID 到权限切换，目标是让 Kimi 无缝接入更大的 Agent 互联生态。
- **Codex 兼容性**: 嵌套 Skill 目录（#1894）等需求说明，开发者对“好用”的定义基准是与 Codex 持平。Kimi 需要在功能完备性上与 Codex 对齐，降低开发者的迁移摩擦。
- **任务自治与容错**: 用户不满足于“黑盒”运行，期望对后台任务有超时控制（#2232）、进度查询和失败恢复能力。
- **跨平台健壮性**: 换行符问题（#2362）的出现表明，Windows 平台的用户体验仍需打磨，跨平台测试矩阵需要加强。

---

## 6. 开发者关注点

- **“Codex 能做”是高优先级的标杆**：开发者对比竞品的习惯非常普遍，任何功能缺失（如递归加载 Skill）都会直接影响用户心智和产品选择。
- **稳定压倒一切**：WebSocket Worker 挂死（#2365）这类阻塞型 Bug 一旦被大面积复现，将严重打击开发者对产品工程可靠性的信任。
- **文档是社区的接口**：Hooks 示例文档的错误被多人修复，说明模糊的文档会大量消耗社区的贡献热情。清晰、可运行的文档能有效转化为高质量的社区产出。
- **主动贡献生态**：看到开发者提前为自家平台集成 Kimi（如 PwrAgent + ACP），这是一种非常健康的生态信号。项目方应维护好此类第三方集成者的开发体验，并加速合并相关 PR。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 OpenCode 社区动态日报。

---

# OpenCode 社区动态日报 | 2026-05-25

## 1. 今日速览

今日社区焦点事件频发：DeepSeek V4 Pro 官方宣布永久降价 75% 后，大量用户呼吁 OpenCode Go 订阅计划同步提升配额；GPT 系列模型的**响应速度慢**、**流式传输中断**等稳定性问题成为社区最大痛点（#29079， #29187）；此外，**支付安全**问题引发关注（#29195），一名用户举报了虚假的 “OpenCode ZEN” 订阅欺诈。代理沙箱（Sandbox）功能以 46 个 👍 继续稳居最高票需求。

## 2. 版本发布

过去 24 小时内无新版本发布。

## 3. 社区热点 Issues （10 条）


1.  ##### **[#29079] GPT Models takes too long to respond**
    ##### 🔥 讨论热度最高：40 条评论
    **摘要**：用户反映 GPT-5.4 等模型响应极不稳定，即使是简单的 “更新 graphify” 指令，有时几秒内响应，有时却需要几分钟。这指向了 OpenAI 流式传输的严重延迟抖动问题，社区共鸣强烈。
    **链接**：https://github.com/anomalyco/opencode/issues/29079

2.  ##### **[#2242] Is there a way to sandbox the agent？**
    ##### 👍 呼声最高：46 个赞
    **摘要**：开发者强烈要求为 Agent 的终端命令增加沙箱限制（类似 Gemini Codex 的 Seatbelt），禁止 Agent 访问当前工作目录以外的文件系统。这是目前社区最主流的**安全与权限控制**诉求。
    **链接**：https://github.com/anomalyco/opencode/issues/2242

3.  ##### **[#15585] When use a free model “free usage exceed” appeared**
    ##### 🔥 争议问题：38 条评论
    **摘要**：用户反映免费模型（如 Big Pickle）在长时间会话后出现“free usage exceed”错误。社区质疑免费模型是否存在未声明的隐藏限制，该议题已持续数月，成为老生常谈但未解决的问题。
    **链接**：https://github.com/anomalyco/opencode/issues/15585

4.  ##### **[#29195] Zen Payment SCAM**
    ##### ⚠️ 安全事件：6 条评论
    **摘要**：一名用户发帖警告社区，小心虚假的 “OpenCode ZEN” 支付重定向欺诈。该用户建议受骗者立即联系银行发起申诉，并保留截图作为证据。此事件暴露出支付流程中可能存在的安全盲区，社区信任度受挫。
    **链接**：https://github.com/anomalyco/opencode/issues/29195

5.  ##### **[#28846] Adjust Go usage limits after DeepSeek V4 Pro 75% price reduction**
    ##### 💰 经济驱动：10 条评论
    **摘要**：DeepSeek V4 Pro 在官方层面永久降价 75% 后，用户迅速跟进，要求 OpenCode 同步提升 Go 订阅计划的使用配额。这表明社区对 API 价格变动高度敏感，并期望平台能实时传递成本红利。
    **链接**：https://github.com/anomalyco/opencode/issues/28846

6.  ##### **[#29129] OpenAI stream intermittently freezes with high CPU**
    ##### 🐛 性能 Bug：8 条评论
    **摘要**：OpenAI 流式响应间歇性卡死，UI 显示状态为 “工作中”，但模型无实际输出，同时 CPU 占用飙升，只能通过手动重启才能恢复。该 Bug 严重影响日常编码体验。
    **链接**：https://github.com/anomalyco/opencode/issues/29129

7.  ##### **[#7827] [Windows] opencode.exe memory consumption too high**
    ##### 🐛 性能 Bug：14 条评论
    **摘要**：Windows 用户反馈 opencode.exe 内存占用异常，动辄飙升至 6GB。这是长期存在的**跨平台性能**问题，严重影响 Windows 用户的开发体验。
    **链接**：https://github.com/anomalyco/opencode/issues/7827

8.  ##### **[#22020] Global AGENTS.md silently ignored when project AGENTS.md exists**
    ##### 🐛 配置 Bug：9 条评论
    **摘要**：当全局 AGENTS.md 与项目级 AGENTS.md 同时存在时，全局规则被静默忽略。该行为违反了官方文档声明，导致开发者无法实现规则的统一管理与叠加。
    **链接**：https://github.com/anomalyco/opencode/issues/22020

9.  ##### **[#13388] ACP over WebSocket for remote/network access**
    ##### 🌐 远程开发愿景：8 条评论
    **摘要**：社区希望将 **Agent Client Protocol （ACP）** 通过 WebSocket 暴露出来，从而允许开发者在其他主机或编辑器上远程控制 OpenCode 实例。这是构建**远程开发工作流**的关键一步。
    **链接**：https://github.com/anomalyco/opencode/issues/13388

10. ##### **[#29190] MCP remote connections silently die after idle periods**
    ##### 🐛 连接可靠性：2 条评论
    **摘要**：远程 HTTP/SSE MCP 连接在空闲一段时间后静默断开，且 UI 状态仍显示 “connected”。缺乏心跳包、重连机制和错误处理，导致长时间运行的 Agent 任务在执行 MCP tool call 时突然失败。
    **链接**：https://github.com/anomalyco/opencode/issues/29190

## 4. 重要 PR 进展 （10 条）


1.  ##### **[#29193] feat（skill）： add `hidden` frontmatter field to skills**
    **摘要**：为 Skill 的 YAML 前置元数据增加 `hidden` 布尔字段，允许用户隐藏不想在 UI 列表中看到的 Skill。这对于拥有大量自定义 Skill 的管理者非常实用。
    **链接**：https://github.com/anomalyco/opencode/pull/29193

2.  ##### **[#29197] docs： add local-code-opencode-plugin to ecosystem**
    **摘要**：将基于 Git 上下文句柄注入的新插件 `local-code-opencode-plugin` 收录进官方生态文档，进一步丰富了社区插件库。
    **链接**：https://github.com/anomalyco/opencode/pull/29197

3.  ##### **[#20491] feat（opencode）： add Kiro provider**
    **摘要**：添加 Amazon Web Services （AWS） 旗下的 Kiro.dev 作为新的模型服务商 Provider，增加了用户在云 API 供应商上的选择权。
    **链接**：https://github.com/anomalyco/opencode/pull/20491

4.  ##### **[#26580] fix： normalize Windows desktop session paths**
    **摘要**：修复 Windows 桌面版会话文件路径问题。此前用户关闭并重启客户端后，所有历史会话会消失（仍存在于磁盘但无法加载），当前 PR 已合并，解决了一个关键的跨平台修复。
    **链接**：https://github.com/anomalyco/opencode/pull/26580

5.  ##### **[#26861] fix（tui）： Old messages disappearing during long sessions**
    **摘要**：修复了 TUI 在长对话中**历史消息丢失**的问题。引入了向上滚动懒加载机制，当用户滚动到顶部附近时，自动加载更早的 50 条消息。
    **链接**：https://github.com/anomalyco/opencode/pull/26861

6.  ##### **[#27785] fix（mcp）： handle oauth flows that connect without tokens**
    **摘要**：修复了 MCP OAuth 流程中，远程服务器可能在未安全持久化令牌的情况下完成传输建立的 Bug。合并后将显著提升 MCP 远程连接的安全性和稳定性。
    **链接**：https://github.com/anomalyco/opencode/pull/27785

7.  ##### **[#29183] feat（opencode）： add AI psychosis detector with heartbeat-based instance tracking**
    **摘要**：新增一个名为“AI 精神病探测器”的可选功能。通过心跳机制检测用户是否同时开启了过多 OpenCode 实例，属于社区趣味性与实用性兼具的创意功能。
    **链接**：https://github.com/anomalyco/opencode/pull/29183

8.  ##### **[#22666] feat（opencode）： Add inline $skill invocations**
    **摘要**：在提示词输入中支持 `$skill` 自动补全。用户现在可以直接输入 `$` 来搜索和调用 Skill，将 Skill 直接注入到当前对话上下文中，提升技能调用的便捷性。
    **链接**：https://github.com/anomalyco/opencode/pull/22666

9.  ##### **[#29176] fix（task）： surface non-text subagent results**
    **摘要**：修复了 `task` 工具（子代理）在完成工作且没有最终 `text` 组件时，返回空 `<task_result>` 的错误。现在非文本的结构化结果也能正确传递给父代理。
    **链接**：https://github.com/anomalyco/opencode/pull/29176

10. ##### **[#29174] fix（tui）： show direct child sessions as subagents**
    **摘要**：修复了通过 API 直接创建的子会话（`session.create（parentID）`）在父代理 UI 中不可见的问题。该 PR 确保无论子会话如何创建，都能在 UI 中正确展示层级关系。
    **链接**：https://github.com/anomalyco/opencode/pull/29174

## 5. 功能需求趋势

综合所有 Issues，当前社区关注的功能方向呈现出以下三大趋势：

1.  **经济学驱动的配额调整**：API 供应商降价（如 DeepSeek V4 Pro 降价 75%）立即传导至社区，用户期望 OpenCode 订阅计划能实时反映成本下降（#28846， #29151）。社区对模型使用成本高度敏感。
2.  **远程开发与网络架构升级**：从 “ACP over WebSocket”（#13388）、SSH 远程编辑（#29152）到 “MCP 连接可靠性”（#29190），社区不再满足于本地工具，正在强烈要求构建远程 Agent 开发的基础设施。
3.  **安全与权限治理**：Agent 沙箱（#2242）以 46 个 👍 高居榜首，对文件系统访问限制的需求日益迫切。而 “Zen Payment SCAM” 事件（#29195）更是将支付安全与平台信任推到了台前。

## 6. 开发者关注点

1.  **稳定性压倒一切**：大量 Bug 集中在**模型响应卡顿**（#29079）、**流式传输中断**（#29187）、**内存溢出**（#7827）和**连接超时**（#26602）上。开发者当前最核心的诉求是“能用且好用”，而非新增功能。版本 1.15.10 的卡死问题（#29134）尤为突出。
2.  **跨平台体验不均**：Windows 平台的内存与路径问题（#26580， #7827）与 macOS 下的证书/终端挂起问题（#21206， #29134）显示出严重的平台兼容性短板。
3.  **配置管理亟待优化**：无论是全局配置被静默覆盖（#22020），还是修改配置必须重启应用（#10899），都严重破坏了开发者的工作流连续性。
4.  **信任危机初现**：“Zen Payment SCAM” 事件（#29195）与免费模型配额不透明（#15585）正在侵蚀社区信任。代理沙箱（#2242）的强烈需求也反映出开发者对 AI 自主行为的隐忧。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，作为一名专注于 AI 开发工具的技术分析师，根据提供的 GitHub 数据，我为你生成一份结构清晰的 Pi 社区动态日报。

---

# Pi 社区动态日报 | 2026-05-25

**数据来源:** github.com/badlogic/pi-mono

---

## 1. 今日速览

尽管过去24小时无新版本发布，但Pi社区的技术动态依然密集。`openai-codex` 在特定情况下导致 TUI 永久挂起的高频 Bug (#4945) 成为今日讨论焦点；与此同时，社区呼吁已久的 **XDG Base Directory** 规范支持 (#2870) 与对应的 PR (#256) 取得了重大实质进展，Linux 用户喜大普奔。此外，官方级 **阿里云 DashScope 提供商** 支持上线，带来了 Qwen 3.7 Max 等 22 个模型 (#4964)，显著增强了 Pi 在中文生态的覆盖能力。

---

## 2. 版本发布

（过去24小时内没有新的版本发布。）

---

## 3. 社区热点 Issues

**1. #4945 `openai-codex` TUI 交互式挂起问题**
- **重要性：** 高。用户报告 `openai-codex` / `gpt-5.5` 在交互式 TUI 中随机卡死，画面停留在 “Working...” 无任何回流文字或错误信息，唯一恢复手段是强制按 Escape。这是当前最影响日常工作流的稳定性 Bug。
- **社区反应：** 13 条评论，5 个 👍，用户反馈频繁复现。
- **链接：** https://github.com/earendil-works/pi/issues/4945

**2. #4916 新增文件读取折叠设置**
- **重要性：** 中。Agent 每次读取文件都会打出约 12 行内容，社区希望增加类似“隐藏思考”的开关，将其折叠为 `read ~/path/to/file` 单行，大幅减少信息噪音。
- **社区反应：** 19 条评论（评论数最高），快速被关闭并标记为 `inprogress`，表明开发组认可该方向。
- **链接：** https://github.com/earendil-works/pi/issues/4916

**3. #2870 遵循 XDG Base Directory 规范**
- **重要性：** 极高（26 👍）。Linux 用户长期呼吁的点，要求 Pi 不再把 `.pi` 配置目录直接放在 `$HOME` 下，而是遵循行业标准使用 `$XDG_CONFIG_HOME`。
- **社区反应：** 14 条评论，于昨日关闭。配合 PR #256 的提交，标志着这一长期需求即将落地。
- **链接：** https://github.com/earendil-works/pi/issues/2870

**4. #4897 RPC 模式下高吞吐 stdout 导致 ENOBUFS 崩溃**
- **重要性：** 高。当父进程通过 JSONL 协议读取 Pi 的输出时，在高吞吐场景下 Pi 进程因 Node.js 写缓冲区爆满而崩溃退出，严重影响 RPC 集成的稳定性。
- **社区反应：** 13 条评论，已关闭修复。
- **链接：** https://github.com/earendil-works/pi/issues/4897

**5. #4046 Compaction 机制清空所有数据**
- **重要性：** 警示级。虽然标题戏谑了 “because-weekend”，但问题本身非常严肃：用户数据压缩（Compaction）流程可能会因某些未知状况直接删除所有会话记录。
- **社区反应：** 8 条评论，已关闭。这个问题促使社区对数据生命周期管理产生了更深的关注。
- **链接：** https://github.com/earendil-works/pi/issues/4046

**6. #4877 Session 文件夹哈希碰撞**
- **重要性：** 中。因为 Session 文件夹的命名规则，不同路径（如 `/a/b/c/d` 和 `/a-b/c-d`）可能会映射到同一个哈希上，导致会话错乱。
- **社区反应：** 7 条评论，仍处于 Open 状态，架构层面潜在的隐患。
- **链接：** https://github.com/earendil-works/pi/issues/4877

**7. #4801 DeepSeek v4 Pro 在 OpenRouter 上 `reasoning_effort` 参数错误**
- **重要性：** 中。用户在调用 DeepSeek v4 Pro (xhigh) 时，即使传入了正确的 `xhigh` 参数，后端依然报 400 参数错误。体现了前沿模型与 API 提供商之间的频繁兼容性问题。
- **社区反应：** 5 条评论，仍为 Open 状态，用户只能暂时降级为 `high`。
- **链接：** https://github.com/earendil-works/pi/issues/4801

**8. #4687 无障碍 / 屏幕阅读器支持**
- **重要性：** 低频率但高价值。TUI 使用了大量边框字符，导致屏幕阅读器（Screen Reader）反复朗读 “box drawing light horizontal”，无法正常使用。
- **社区反应：** 5 条评论，已关闭。体现了社区对全功能残障人士使用体验的包容性考量。
- **链接：** https://github.com/earendil-works/pi/issues/4687

**9. #4879 在 ToolInfo 中暴露 `promptGuidelines`**
- **重要性：** 中。插件开发者向核心 API 提的 Feature Request，允许扩展在运行时读取某个工具的 Prompt 指南，提升扩展的透明度与操纵能力。
- **社区反应：** 6 条评论，仍为 Open 状态，核心 API 打磨进行中。
- **链接：** https://github.com/earendil-works/pi/issues/4879

**10. #4707 429 限流错误导致 Agent 永久挂起**
- **重要性：** 高。当 API 返回 429 限流，底层 fetch 库未正确捕获异常，导致 Agent 在 “Working” 状态无限循环。
- **社区反应：** 4 条评论，3 👍。该问题已有相关 PR (#4759) 进行修复，通过配置 HTTP 空闲超时来解决。
- **链接：** https://github.com/earendil-works/pi/issues/4707

---

## 4. 重要 PR 进展

**1. #4974 大版本功能合集：回滚修复、审查重构、Hooks 兼容**
- **内容：** 积累了多日的大规模合并，包含文件回滚 Diff 修复、变更审查 UI 翻新、Hooks 兼容性改进以及自动记忆功能的 RPC 支持。
- **链接：** https://github.com/earendil-works/pi/pull/4974

**2. #4971 为 Anthropic 兼容提供商添加 `allowEmptySignature`**
- **内容：** 解决部分第三方 AI 服务商返回的 Thinking 块签名为空时，导致 Replay 失败或 Prompt Caching 失效的问题。通过新增选项允许空签名。
- **链接：** https://github.com/earendil-works/pi/pull/4971

**3. #256 实现 XDG Base Directory 规范并支持自动迁移**
- **内容：** 配合 Issue #2870 的重大基础设施改进。实现了从 `~/.pi/` 到 `$XDG_CONFIG_HOME/pi` 的自动化迁移，极大提升 Linux 用户的环境整洁度。
- **链接：** https://github.com/earendil-works/pi/pull/256

**4. #4964 新增阿里云 DashScope 提供商，支持 22 个 Qwen 模型**
- **内容：** 官方级 DashScope Provider 实现，支持 Qwen 3.7 Max 在内的 22 个模型，集成深度思考（`enable_thinking`）等功能，大大降低了国内用户的接入门槛。
- **链接：** https://github.com/earendil-works/pi/pull/4964

**5. #4965 禁用 Kitty 协议 Flag 2，修复 VS Code 终端焦点回归**
- **内容：** 解决用户在使用 VS Code 内建终端时，切换窗口后再回来，视图会自动滚动到最底部的恼人问题。
- **链接：** https://github.com/earendil-works/pi/pull/4965

**6. #4958 修复 Compaction 中止控制器竞态条件**
- **内容：** 修复自动/手动 Compaction 在异步执行后读取已失效的 `.signal` 状态，导致进程崩溃的竞态问题，提升数据压缩的健壮性。
- **链接：** https://github.com/earendil-works/pi/pull/4958

**7. #4911 为 Codex 添加设备码登录方式**
- **内容：** 新增 OAuth 设备码流，为无法打开浏览器回调的场景（如纯 SSH 环境）提供替代登录方案，完善认证流程闭环。
- **链接：** https://github.com/earendil-works/pi/pull/4911

**8. #4954 在命令上下文中暴露 `getToolDefinition` 方法**
- **内容：** 允许 `/tool` 等扩展命令获取工具的完整输入 Schema，用于手动调用 Agent 工具，极大拓展了插件能力。
- **链接：** https://github.com/earendil-works/pi/pull/4954

**9. #4873 清理跨平台路径处理逻辑**
- **内容：** 全面审查代码库中的路径拼接方式，修复 Windows 与 Unix 系之间的跨设备路径问题，减少潜在 Bug 并统一代码风格。
- **链接：** https://github.com/earendil-works/pi/pull/4873

**10. #4759 配置 HTTP 空闲超时时间**
- **内容：** 配合 #4707 修复，将 HTTP 空闲超时改为可配置属性，并设置默认的 5 分钟安全值，防止 Agent 因底层连接泄漏而无限挂起。
- **链接：** https://github.com/earendil-works/pi/pull/4759

---

## 5. 功能需求趋势

- **模型支持的多元化与本地化**：社区积极拥抱新模型（DashScope/Qwen、DeepSeek v4），对 Provider 的兼容性提出了更高要求。阿里云 DashScope 的快速支持，也体现了 Pi 向国内开发者生态靠拢的趋势。
- **Linux 原生体验**：以 XDG Base Directory 规范为代表，Linux 用户对软件行为“原生性”的要求极高。配置文件整洁度、Terminal 控件兼容性（Kitty 协议）是关键指标。
- **终端 UI 沉浸式体验**：从文件折叠、Markdown 渲染优化到 URL 智能换行，用户希望 CLI 工具的输出像原生 IDE 一样干净、有序，减少视觉噪音。
- **工程化可靠性**：用户不再满足于“能用”。Compaction 的安全边界、RPC 的稳定性、HTTP 异常恢复（超时控制、429 重试）是当前工程化的主旋律。
- **插件系统的成熟化**：核心 API 正在逐步暴露（ToolInfo、Editor Cursor、Command Context），开发者不满足于简单的脚本注入，渴望拥有标准化的工具链开发能力。

---

## 6. 开发者关注点

- **“假死”与“卡住”的零容忍**：**#4945**（Codex 卡死）和 **#4707**（429 卡死）反映出 TUI 在复杂异步状态下的健壮性是当前最大的体验痛点。一旦失去响应，开发流被迫中断，用户容忍度极低。
- **模型适配的高维护成本**：从 DeepSeek 的参数冲突到 Anthropic 的签名问题，再到 Bedrock 的空文本块，每一次模型更新都可能产生兼容性断裂。用户在无形中承担了“兼容性测试”的工作。
- **数据管理的信任危机**：**#4046**（Compaction 删库）和 **#4877**（Session 碰撞）触及了开发者最敏感的神经——数据安全。这要求开发者在数据架构上必须拿出极其扎实的证明修复方案。
- **基础交互的“未完成感”**：Shift+Enter 发送（#4918）、新行插入（#4406）、屏幕阅读支持（#4687）等长期存在的交互问题反复出现，暗示 TUI 组件在焦点管理、Keybinding 路由上的处理仍不够稳定。
- **插件生态的脆弱性**：**#4976**（`pi.addCommand is not a function`）这类错误表明，部分新版 API 可能在构建发布时被遗漏或未正确导出，插件开发者容易被不稳定的 API 消磨热情。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，没问题。作为一名专注于 AI 开发工具的技术分析师，这是为您生成的 Qwen Code 社区动态日报。

---

# Qwen Code 社区动态日报 | 2026-05-25

## 📰 今日速览

今日社区动态主要围绕 **Qwen Code 服务端能力（Mode B）的持续增强**，重点引入了会话回顾 API、实时同步修复以及运行保护机制。用户体验方面，**关于 VSCode 插件兼容性、Token 消耗统计和输出语言配置的反馈较为集中**，社区对稳定性和可观测性的诉求日益增强。

---

## 🚀 版本发布

- **[v0.16.1-nightly.20260525.84f408017]**
    - **更新内容**：修复了构建流程中 `tsc --build` 可能在源文件未更改时错误报错 `TS5055` 的问题，清理了过时的构建输出。同时，开启了 v0.16.1 正式版的发布准备工作。
    - **链接**: [Release v0.16.1-nightly.20260525.84f408017](https://github.com/QwenLM/qwen-code/releases/tag/v0.16.1-nightly.20260525.84f408017)

---

## 🔥 社区热点 Issues

1.  **[#4175] proposal(serve): Mode B feature-priority roadmap toward v0.16 production-ready**
    - **为什么重要**: 这是 Qwen Code 服务端模式（Mode B）迈向生产就绪的路线图，社区讨论最为热烈（38条评论）。它定义了 `qwen serve` 的未来功能优先级，是所有服务器端用户的关注焦点。
    - **社区反应**: 贡献者 `doudouOUC` 发布了详细的路线图，社区正围绕 Stage 1 后的功能优先级进行讨论。
    - **链接**: [Issue #4175](https://github.com/QwenLM/qwen-code/issues/4175)

2.  **[#4488] qwen code插件(v0.16.0)在vscode左侧栏不显示**
    - **为什么重要**: 直接影响用户体验的严重 Bug。新版 VSCode（1.120.0）无法正常显示 Qwen Code 插件，会导致新用户无法安装和使用，影响范围大。
    - **社区反应**: 作者描述详细，该问题已触发编辑，并由 `status/need-information` 标签跟进。
    - **链接**: [Issue #4488](https://github.com/QwenLM/qwen-code/issues/4488)

3.  **[#4276] oom-crash**
    - **为什么重要**: 内存溢出（OOM）是任何应用中最严重的问题之一，直接影响开发工作流。该问题在 18 号提出至今仍在活跃讨论，说明复现和修复有一定难度。
    - **社区反应**: 作者提供了详细的错误日志，社区正在排查根因。
    - **链接**: [Issue #4276](https://github.com/QwenLM/qwen-code/issues/4276)

4.  **[#4479] 需要一个功能统计Qwen Code每日消耗的Token数量**
    - **为什么重要**: 这是高频用户的核心诉求。一次使用 3 千万 Token 的消耗让用户对成本感到不安，缺乏透明度会阻碍重度用户的采纳。
    - **社区反应**: 请求获得社区共鸣，被标记为 `welcome-pr`，暗示项目方愿意接受社区贡献来实现此功能。
    - **链接**: [Issue #4479](https://github.com/QwenLM/qwen-code/issues/4479)

5.  **[#4493] rider无法登录qwen code**
    - **为什么重要**: 继 VSCode 问题后，IDE 集成的另一个痛点。JetBrains Rider 用户无法登录，说明 IDE 插件的兼容性和登录流程是当前的主要弱项。
    - **社区反应**: 问题尚待分类，但截图清晰显示了无限重定向的问题。
    - **链接**: [Issue #4493](https://github.com/QwenLM/qwen-code/issues/4493)

6.  **[#4421] feat(diagnostics): 本地问题诊断框架 — ring buffer + diagnostic ID + /bug collect bundle**
    - **为什么重要**: 针对“无法复现”和“用户不知如何提供信息”这类排查难题，提出了一个设计优雅的本地优先诊断方案（环形缓冲区 + 诊断 ID）。对提升问题处理效率和用户体验有重大意义。
    - **社区反应**: 社区反馈积极，认为此方案能极大改善非标准场景下的 BUG 报告质量。
    - **链接**: [Issue #4421](https://github.com/QwenLM/qwen-code/issues/4421)

7.  **[#4501] bug(provider/dashscope): side-query thinking disable doesn't reach qwen3 series**
    - **为什么重要**: 这是一个隐蔽但关键的功能 Bug。用户试图关闭 Qwen3 模型的思考过程（`thinking`），但由于代码逻辑错误导致此设置无效，会误导用户以为功能有问题。
    - **社区反应**: 提交者 `doudouOUC` 提供了精准的代码定位和根因分析，修复方向明确。
    - **链接**: [Issue #4501](https://github.com/QwenLM/qwen-code/issues/4501)

8.  **[#4444] Token Plan未启用缓存 session cache**
    - **为什么重要**: 直接关系到 Token 消耗和 API 调用成本。Token Plan 用户无法使用缓存，导致成本上升，影响该付费模式的性价比。
    - **社区反应**: 用户 `goal` 指出了 `/stats model` 统计信息中缺失缓存数据。
    - **链接**: [Issue #4444](https://github.com/QwenLM/qwen-code/issues/4444)

9.  **[#4494] Side queries ignore the user's configured output language**
    - **为什么重要**: 语言偏好设置是基本的可用性要求。当用户设置了中文输出，但 Recap、Title 等边缘查询仍返回英文，会带来割裂感，影响国际化体验。
    - **社区反应**: 问题描述清晰，精确指出了受影响的功能范围。
    - **链接**: [Issue #4494](https://github.com/QwenLM/qwen-code/issues/4494)

10. **[#4486] bug(telemetry): qwen-code.interaction span has wrong trace id**
    - **为什么重要**: 对开发者而言，OpenTelemetry 追踪数据不完整（交互 Span 与 Session 根 Context 分离）会使性能监控和问题排查变得混乱，数据不可信。
    - **社区反应**: 提交者已定位到是缺失了父 Context，修复方案明确。
    - **链接**: [Issue #4486](https://github.com/QwenLM/qwen-code/issues/4486)

---

## 💻 重要 PR 进展

1.  **[#4504] feat(serve): add POST /session/:id/recap**
    - **功能/修复**: 为服务端（daemon）增加 API，允许外部 SDK、Web UI 等客户端通过 `POST /session/:id/recap` 获取会话摘要，不用驱动 Agent 运行即可知道进度。
    - **链接**: [PR #4504](https://github.com/QwenLM/qwen-code/pull/4504)

2.  **[#4502] feat(cli): headless / non-interactive runaway-protection guardrails**
    - **功能/修复**: 为非交互模式添加“防失控”护栏，新增 `--max-wall-time` 和 `--max-tool-calls` 参数，防止任务无限执行下去（解决 Issue #4103）。
    - **链接**: [PR #4502](https://github.com/QwenLM/qwen-code/pull/4502)

3.  **[#4359] feat(ci): preflight-triage AI review + PR compliance gates**
    - **功能/修复**: 一个重要的 CI/CD 增强。引入 AI 驱动的 PR 审查和合规门禁，确保模板完整性和代码可审查性，提升协作效率。虽然还在 Open 状态，但显示了项目质量自动化的方向。
    - **链接**: [PR #4359](https://github.com/QwenLM/qwen-code/pull/4359)

4.  **[#4495] Enable Token Plan cache control**
    - **功能/修复**: 修复 Token Plan 用户无法使用缓存的问题。通过让 Token Plan 端点遵循 DashScope 路径来利用现有的缓存控制元数据，直接解决 Issue #4444。
    - **链接**: [PR #4495](https://github.com/QwenLM/qwen-code/pull/4495)

5.  **[#4499] fix(telemetry): attach interaction span to session root context**
    - **功能/修复**: 精确修复 Issue #4486，为 `startInteractionSpan` 添加上下文，确保追踪链路的完整性。
    - **链接**: [PR #4499](https://github.com/QwenLM/qwen-code/pull/4499)

6.  **[#4491] fix(sdk): honor canUseTool timeout in CLI control requests**
    - **功能/修复**: 修复了 SDK 超时配置未正确传递给 CLI 的问题，确保用户在 CLI 中响应工具权限请求时有合理的时间（而非较短的控制超时）。
    - **链接**: [PR #4491](https://github.com/QwenLM/qwen-code/pull/4491)

7.  **[#4489] fix(core): prevent auto-skill creation from overwriting existing skills**
    - **功能/修复**: 修复了一个严重的数据覆盖问题。自动技能创建功能会错误地覆盖非 `auto-skill` 来源的同名技能文件。
    - **链接**: [PR #4489](https://github.com/QwenLM/qwen-code/pull/4489)

8.  **[#4476] [type/feature-request] Add AUTO mode denial observability and caps**
    - **功能/修复**: 增强了 AUTO 模式的安全性，增加了结构化的拒绝原因类型、拒绝事件的 Hook，以及累计拒绝次数限制，提升可观测性。
    - **链接**: [PR #4476](https://github.com/QwenLM/qwen-code/pull/4476)

9.  **[#4410] feat(telemetry): Phase 3 — qwen-code.subagent span with concurrent isolation**
    - **功能/修复**: 高级 Telemetry 功能。为子 Agent 调用创建独立 Span，并解决并发隔离问题，使 Tracing 数据更清晰准确。
    - **链接**: [PR #4410](https://github.com/QwenLM/qwen-code/pull/4410)

10. **[#4482] fix(telemetry): improve LogToSpan bridge error info and TUI handling**
    - **功能/修复**: 改进了日志转 Span 桥接（LogToSpan）的错误提示，并增强了 TUI 对错误信息的处理能力。
    - **链接**: [PR #4482](https://github.com/QwenLM/qwen-code/pull/4482)

---

## 📈 功能需求趋势

从今日的 Issues 中可以提炼出社区最关注的几个功能方向：

1.  **更强的可观测性与透明度**：社区强烈希望增加 Token 消耗统计（#4479）、本地问题诊断能力（#4421）、以及更完善的 Telemetry（#4486）。用户和开发者都希望能精确掌控工具的运行状态和成本。
2.  **IDE 集成稳定性与兼容性**：VSCode 插件不显示（#4488）和 Rider 登录失败（#4493）的问题表明，IDE 集成的稳定性和对新版本 IDE 的兼容性是当前最突出的用户体验瓶颈。
3.  **服务端模式（Mode B）的完善**：`/recap` API（#4504）和“运行保护”护栏（#4502）的 PR 表明，社区正向构建一个稳定、可控、功能全面的服务端应用迈进。
4.  **核心功能配置的精确性**：输出语言配置被忽略（#4494）、Token Plan 缓存失效（#4444）、模型 Thinking 参数失效（#4501）等问题的提出，说明社区对产品功能的正确性和可靠性有很高的要求。

---

## 🧑‍💻 开发者关注点

1.  **VSCode 插件兼容性（高频痛点）**：`#4488` 问题热度极高，大量用户遭遇新版 VSCode 无法使用插件，这是当前最影响用户留存的首要问题。
2.  **OOM 崩溃（稳定性焦虑）**：`#4276` 的内存溢出问题持续发酵，部分用户的开发流程被意外中断，这是对产品稳定性的严重挑战。
3.  **UI 冻结与卡顿（体验瓶颈）**：`#4442` 和 `#4471` 提及的批量编辑时 UI 冻结、长对话卡顿问题，说明在处理复杂任务时，前端性能需要优化。
4.  **Side Queries 忽视语言配置（国际化问题）**：`#4494` 表明在非核心流程上忽略了用户的核心语言偏好，这种细节体验会造成“功能没问题，但不好用”的观感。
5.  **Token 消费不透明（成本焦虑）**：`#4479` 中用户的诉求“一次使用 3 千万 Token”凸显了用户面对高昂 Token 成本的困惑和不安，缺乏详细的消耗报告将阻碍用户大规模使用。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# 2026-05-25 CodeWhale（原 DeepSeek TUI）社区动态日报

> **数据来源**: `github.com/Hmbown/CodeWhale` | **分析时间**: 2026-05-25 | **发布频率**: 每日


## 今日速览 🔥

1. **项目正式更名为 CodeWhale**：v0.8.44 落地，遗留的 `deepseek` / `deepseek-tui` 二进制转为过渡 shim，v0.9.0 将彻底移除。更名直接导致了 Homebrew 分发故障（#2104），社区反应强烈。
2. **v0.8.45 发布周开启**：主创 `Hmbown` 密集合并了多项准备 PR（#2118），45 版本的核心主题是 **Agent 控制平面**——让 Agent 工作成为可中断、可恢复的可靠流程。
3. **Docker 稳定性成舆论焦点**：#1615 以 **188 条评论**成为社区最大噪音源，用户反馈严格按文档操作仍必现乱码崩溃，情绪激烈。


## 版本发布 🚀

### v0.8.44 / v0.8.43（2026-05-25 发布）
- **正式更名为 `CodeWhale`**。遗留的 `deepseek` 和 `deepseek-tui` 二进制作为弃用 shim 保留一个发布周期，调用时会打印一行弃用警告并自动转发至 `codewhale` / `codewhale-tui`。
- **下个版本预告**：v0.9.0 将彻底移除上述 shim，建议用户尽早迁移。
- 详见 [`docs/REBRAND.md`](https://github.com/Hmbown/CodeWhale)

> **影响面分析**：本次更新对 CI/CD 流水线和包管理器用户冲击较大，建议立即检查脚本中是否硬编码了 `deepseek` 命令。

`[查看发布页](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.44)`


## 社区热点 Issues（Top 10）

### 🐞 严重 Bug 类

1. **[[#1615] Docker 拉取直接乱码](https://github.com/Hmbown/CodeWhale/issues/1615)** [CLOSED]
   - **重要性**：⭐⭐⭐⭐⭐ | **评论 188 条**
   - **摘要**：用户完全按照文档操作，仅替换 API Key，Docker 运行后直接乱码，只能强制重启 Linux 服务器。社区情绪激烈（原文："什么垃圾玩意"），暴露出 Docker 化后的终端兼容性或环境预设有严重缺失。
   - **社区反应**：评论区大量"我也一样"的复现确认，但目前 Issue 已关闭，用户期待官方给出根本性的 root cause 分析。

2. **[[#2104] Homebrew 安装后 `codewhale` 找不到](https://github.com/Hmbown/CodeWhale/issues/2104)** [OPEN]
   - **重要性**：⭐⭐⭐⭐⭐ | **评论 2 条**
   - **摘要**：`brew upgrade` 后，`deepseek` shim 输出弃用警告并尝试调用 `codewhale`，但 Homebrew 公式未安装 `codewhale` 二进制，导致启动失败。这是项目更名的直接副作用。
   - **社区反应**：紧急程度高。对应修复 PR #2105 已提交，用户需等待新版本被 Homebrew 接纳。

3. **[[#2114] `/profile` 切换 Provider 被环境变量覆盖](https://github.com/Hmbown/CodeWhale/issues/2114)** [OPEN]
   - **重要性**：⭐⭐⭐⭐ | **评论 0 条**
   - **摘要**：使用 `/profile` 命令切换配置时，即使 profile 中正确配置了 `provider = "openrouter"`，切换后仍然显示 `deepseek`。环境变量优先级高于 profile 配置，导致多 Provider 用户无法顺利切换。
   - **社区反应**：刚发布就获得确认，属于配置架构层面的优先级 bug，影响所有多 Provider 用户。

4. **[[#2109] 模型名 `DeepSeek-V4-Flash` 被自动小写](https://github.com/Hmbown/CodeWhale/issues/2109)** [OPEN]
   - **重要性**：⭐⭐⭐⭐ | **评论 0 条**
   - **摘要**：用户输入大写模型名时，系统静默转成小写，导致 `DeepSeek-V4-Flash` 无法使用。暴露出底层字符串处理逻辑未尊重大小写敏感模型。
   - **社区反应**：虽然暂时无声量，但模型名大小写问题是 OpenAI 兼容性老生常谈的陷阱，必须根治。

### 🧑‍💻 功能/规划类

5. **[[#1879] v0.8.45 Tracker：控制平面与恢复](https://github.com/Hmbown/CodeWhale/issues/1879)** [CLOSED]
   - **重要性**：⭐⭐⭐⭐⭐ | **评论 4 条**
   - **摘要**：主创规划的本版本总纲领。目标是让 Agent 终端工作变得 **可中断、可恢复**，用户可以在飞行中重定向任务而不破坏状态或丢失进度。这是 v0.8.45 所有特性的最高指引。
   - **社区反应**：期待值拉满。这是 TUI Agent 走向生产级的关键一步。

6. **[[#2039] Shell 执行时无进度，UI 看起来像"死机"](https://github.com/Hmbown/CodeWhale/issues/2039)** [CLOSED]
   - **重要性**：⭐⭐⭐⭐ | **评论 1 条**
   - **摘要**：长命令（构建、测试、部署）执行时，UI 没有任何 Spinner、进度条或心跳信号，用户焦虑并误按键。v0.8.45 已要求在 shell 执行期间保持可见的 active 指示。
   - **社区反应**：极度共鸣。这是 TUI 交互的生死线——没有反馈就没有信任。

7. **[[#2018] 低信息行应可悬停/点击查看详情](https://github.com/Hmbown/CodeWhale/issues/2018)** [OPEN]
   - **重要性**：⭐⭐⭐⭐ | **评论 2 条**
   - **摘要**：Work / Tasks / Agents 面板中信息被截断，用户期望悬停显示完整内容，或通过点击展开。配合 PR #2110 的 Tooltip 方案，将显著提升信息密度与可用性。
   - **社区反应**：开发者对 TUI 的交互精致度要求越来越高，期待"终端交互也能像 Web 一样丰富"。

8. **[[#2019] 审计计费机制与 `/balance` 命令](https://github.com/Hmbown/CodeWhale/issues/2019)** [CLOSED]
   - **重要性**：⭐⭐⭐⭐ | **评论 2 条**
   - **摘要**：Sub-agent 和长时间工作越来越可靠，CodeWhale 需要审计其成本计算的正确性，并为用户提供查询活跃 Provider 真实余额的简单途径。
   - **社区反应**：企业级用户的心声。成本透明化是工具从个人走向团队/企业的必备条件。

9. **[[#2117] 多 Skills 分组打包与批量加载](https://github.com/Hmbown/CodeWhale/issues/2117)** [OPEN]
   - **重要性**：⭐⭐⭐ | **评论 0 条**
   - **摘要**：用户提出将多个 Skills 组合成 Group，新建项目时可一键加载预设技能集合。类似于 "TUI 工作流模板"。
   - **社区反应**：代表了社区对工作流复用和标准化配置的强烈渴望。

10. **[[#2092] 重命名 `/goal` → `/hunt` 并引入 Quarry/Verdict 裁决词汇](https://github.com/Hmbown/CodeWhale/issues/2092)** [OPEN]
    - **重要性**：⭐⭐⭐ | **评论 0 条**
    - **摘要**：赋予 Agent 会话"捕猎"语义：`quarry`（猎物目标）、`verdict`（裁决路径：hunting/hunted/wounded/escaped）。配合 v0.8.45 的状态恢复主题，将 Agent 交互变得更加沉浸和直观。
    - **社区反应**：目前尚处规划阶段，但体现了项目独树一帜的品牌风格和文化建设思路。


## 重要 PR 进展（Top 10）

### 🛠 核心修复类

1. **[[#2105] fix(homebrew): 安装 codewhale 二进制和遗留 shim](https://github.com/Hmbown/CodeWhale/pull/2105)** [OPEN]
   - **直接修复**：#2104。Homebrew 公式此前仅下载 `deepseek-*` 制品，本次更新确保 `codewhale` 主程序被正确安装，同时保留过渡 shim。等待合并至主分支。

2. **[[#1856] fix(tools): 用 Semaphore 替代 RwLock 防止死锁](https://github.com/Hmbown/CodeWhale/pull/1856)** [OPEN]
   - **深度修复**：高并发工具调用场景下，`Arc<RwLock<()>>` 可能被工具重入导致死锁。改用 `Semaphore`，串行工具持有许可，并行工具不受阻塞。**架构级优化**。

3. **[[#2103] fix(tui): 修复 Windows 鼠标捕获与方向键历史记录冲突](https://github.com/Hmbown/CodeWhale/pull/2103)** [OPEN]
   - **直接修复**：#1720 (长久遗留问题)。移除了 Windows 空编辑器方向键的 blanket 覆盖，启用鼠标捕获时自动关闭方向键浏览历史，保留回退逻辑。

### 🚀 功能增强类

4. **[[#2118] chore(release): 准备 v0.8.45 发布](https://github.com/Hmbown/CodeWhale/pull/2118)** [OPEN]
   - **要点**：RLM 会话对象、可取消的目录/搜索工具、确定性鲸鱼命名 Agent、`/balance` 框架、贡献者信用更新、多项配置/运行时加固、调色盘审计清理、同步元数据。45 版本的主要特性基本敲定。

5. **[[#2111] feat: 在快照标签中嵌入用户 Prompt 摘要](https://github.com/Hmbown/CodeWhale/pull/2111)** [OPEN]
   - **体验提升**：`/restore` 列表将从 `pre-turn: 1` 变为 `pre-turn: 1 - "重构数据库迁移脚本..."`，大幅提升快照恢复的可读性。

6. **[[#2113] feat(tui): 对话区与工具输出区独立滚动](https://github.com/Hmbown/CodeWhale/pull/2113)** [OPEN]
   - **交互革新**：将聊天区域分为上下两个独立滚动区域，各自拥有独立的滚动状态和缓存。鼠标事件可分别处理，极大提升多工具协作场景下的查看体验。

7. **[[#2102] feat: 默认延迟加载低价值原生工具](https://github.com/Hmbown/CodeWhale/pull/2102)** [OPEN]
   - **性能优化**：核心目录外的原生工具默认延迟加载，`ToolSearch` 按需物化低频率工具。同时支持 `[tools] always_load` 配置手动回切。大幅优化启动速度和内存占用。

8. **[[#2098] feat: 使用 DEC 2026 同步输出包装 TUI 帧](https://github.com/Hmbown/CodeWhale/pull/2098)** [OPEN]
   - **渲染优化**：在 ratatui 的 draw/flush 输出周围包裹同步输出序列（`\x1b[?2026h / \x1b[?2026l`），消除 iTerm2 和 Ghostty 上的渲染撕裂。同时新增 `CODEWHALE_TUI_DEBUG=1` 环境变量，输出每帧渲染 diff 日志。

### 🧪 测试/基础设施类

9. **[[#2107] feat(test): 引入 `FauxStep::Factory` 用于实时请求断言](https://github.com/Hmbown/CodeWhale/pull/2107)** [OPEN]
   - **测试能力飞跃**：允许 `FauxStep` 在被出队时，针对真实外发的 `MessageRequest` 运行闭包断言。这在模拟环境下极大增强了 Agent 行为测试的覆盖度和可靠性。

10. **[[#2099] feat(config): 允许 OpenAI 兼容端点自定义路径后缀](https://github.com/Hmbown/CodeWhale/pull/2099)** [OPEN]
    - **兼容性利器**：增加 `path_suffix: Option<String>` 到 `ProviderConfigToml`，解决部分第三方服务（如本地模型部署服务）不接受 `/v1/chat/completions` 路径的问题。


## 功能需求趋势 📈

### 1. Agent 可恢复与控制平面
这是 v0.8.45 的绝对核心主题。社区高度关注 Agent **中断后可恢复**、**状态不丢失**、以及**飞行中重定向**能力。`/hunt` 和 `verdict` 词汇的引入代表了更结构化的 Agent 生命周期管理。

### 2. 多 Provider 统一网关化
大量 PR/Issue 集中于 Provider 生态扩展（Groq/Cerebras/Together/Deeplnfra，#2087）、模型目录聚合（#2088）、API 路径自定义（#2089）。CodeWhale 正从单一模型 TUI 进化为**多后端统一管理桌面终端**。

### 3. 成本与资源透明化
`/balance` 命令、累计会话计费、缓存命中可视化（#2038）。开发者对每一次对话的成本越来越敏感，TUI 必须提供实时的财务反馈。

### 4. 终端交互精致化（TUI Native UX）
独立滚动区域（#2113）、信息悬停 Tooltip（#2018）、同步输出防撕裂（#2098）、Shell 进度反馈（#2039）。社区正在推动 TUI 交互从"能用"走向"好用"。

### 5. 配置即代码与个性化
多 Skills 分组（#2117）、持久化权限规则（#1186）、Profile 优先级规范（#2114）。开发者期望用声明式的配置来替代 UI 手动操作，实现自动化工作流。


## 开发者关注点 ⚠️

| 痛点 | 关联链接 | 严重程度 |
|---|---|---|
| **更名阵痛**：Homebrew 无法找到二进制、CI 脚本需同步更新 | [#2104](https://github.com/Hmbown/CodeWhale/issues/2104) | 🔴 高 |
| **Docker 环境稳定性**：严格按文档操作仍必现乱码崩溃 | [#1615](https://github.com/Hmbown/CodeWhale/issues/1615) | 🔴 高 |
| **配置优先级混乱**：环境变量 > Profile > Config 逻辑不透明 | [#2114](https://github.com/Hmbown/CodeWhale/issues/2114) | 🟠 中高 |
| **长命令"假死"**：Shell 执行时无 Spinner/进度条，用户焦虑 | [#2039](https://github.com/Hmbown/CodeWhale/issues/2039) | 🟠 中高 |
| **模型名大小写魔法**：大写输入被静默小写，模型不工作 | [#2109](https://github.com/Hmbown/CodeWhale/issues/2109) | 🟡 中 |

### 来自社区的原生声音 📣

> *"什么垃圾玩意啊，多会都跑不了，一跑就这样。全是按照它那个说明文档里面操作的，就换了一个 API，就把自己 API 填进去了。"* —— [#1615](https://github.com/Hmbown/CodeWhale/issues/1615) 用户
> *"Cost and timing display resets too aggressively — users can't track cumulative cost across turns"* —— [#2038](https://github.com/Hmbown/CodeWhale/issues/2038)
> *"Power is not just automation. Power is being able to stop"* —— [#1879](https://github.com/Hmbown/CodeWhale/issues/1879)（主创观点）

---

**一句话总结**：今天项目正式更名为 CodeWhale，v0.8.45 的规划版图基本清晰（可中断 Agent / 成本透明 / UI 精细化），但 Docker 稳定性和 Homebrew 分发问题是当前最紧急的两大信任危机。社区对 Agent 控制力的期待正在超过对基础聊天的需求。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*