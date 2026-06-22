# AI CLI 工具社区动态日报 2026-06-22

> 生成时间: 2026-06-22 03:54 UTC | 覆盖工具: 9 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我已根据您提供的 2026-06-22 工具社区动态，为您生成以下横向对比分析报告。

---

## AI CLI 工具生态横向对比分析报告（2026-06-22）

### 1. 生态全景

当前 AI CLI 工具生态呈现 **“平台巨头维稳求生”与“开源新贵激进创新”** 的分化局面。成本失控（Token 消耗不透明）、Agent 行为不可靠（挂起、循环、过度干预）和平台兼容性回归（Android、Windows）成为全行业必须紧急解决的“信任赤字”问题。与此同时，以 Qwen Code、CodeWhale 为代表的开源/准开源项目正通过极快的迭代速度（语音交互、MCP 热重载、Artifact）抢夺用户体验高地，而生态标准 MCP/ACP 的建设已从“能否连接”进入到“能否安全可控”的深水区。

### 2. 各工具活跃度对比

过去 24 小时内各工具的社区活跃度分化显著：

| 工具 | 热点 Issues 规模 | 重要 PR 数量 | 版本发布 | 社区生态活力评级 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAI Codex** | 极高（费率危机 #28879） | 极高（10+ 架构重构） | **2 个 Alpha** | 动荡高能（🔥🔥🔥🔥🔥） |
| **Qwen Code** | 高（语音、Agent 循环） | 极高（10+ 功能合并） | **v0.18.5 Stable** | 快速创新（🔥🔥🔥🔥🔥） |
| **CodeWhale** | 高（UI 冻结、安全门） | 极高（10+ 安全/修复） | **v0.8.63 品牌重塑** | 品牌跃升（🔥🔥🔥🔥🔥） |
| **Claude Code** | 极高（回归、成本恐慌） | 低（2 个） | 无 | 高活跃高抱怨（🔥🔥🔥🔥） |
| **Gemini CLI** | 高（Agent 挂起、安全审计） | 极高（10+ 信任修复） | 无 | 深度工程（🔥🔥🔥🔥） |
| **OpenCode** | 高（OAuth、用量 API） | 高（10 个） | 无 | 稳健演进（🔥🔥🔥🔥） |
| **Pi** | 中（本地模型、扩展 API） | 高（7 个合并） | 无 | 开发者导向（🔥🔥🔥） |
| **GitHub Copilot CLI** | 低（7 个） | 无关（1 个被污染） | 无 | 稳定沉寂（🔥） |
| **Kimi Code** | 极低（2 个） | 无 | 无 | 休眠（💀） |

### 3. 共同关注的功能方向

多个工具社区在同一周内不约而同地指向了三大核心诉求：

- **成本透明化与“成本锁”机制**
  - **关联工具：Claude Code、OpenAI Codex、Gemini CLI、Copilot CLI、OpenCode、Pi**
  - **具体诉求**：社区不再满足于事后查看 `/cost`。用户要求**执行前估算开销**（Claude #68703）、**执行中 OTel 暴露配额指标**（Copilot #3778）、**对子代理设置独立预算限额**，以及**配额耗尽时的优雅降级**而非粗暴断开。成本已从指标演变为**运行时门控（Gate）**。

- **Agent 行为可靠性与防失控护栏**
  - **关联工具：Claude Code、Gemini CLI、Qwen Code、CodeWhale**
  - **具体诉求**：工具重复调用导致死循环（Qwen #5019）、Agent 过度干预偏离用户指令（CodeWhale #3275）、子代理误报成功（Gemini #22323）以及信任模型/权限保活失效。用户需要**可中断、可观察、可追踪**的执行流程，以及“读前编辑”（Read-before-edit）等中等粒度审查。

- **MCP/ACP 生态深水区（安全与可管理性）**
  - **关联工具：Claude Code、OpenAI Codex、OpenCode、Qwen Code、Kimi Code**
  - **具体诉求**：MCP 协议标准化后，社区焦点转向**认证授权**（OpenCode #988 OAuth）、**内联 UI 渲染**（Codex #21019）、**成本归属与沙箱嵌套**（Codex #29358）和**配置热更新**（Qwen #5561）。谁能解决 MCP 的可信分发与运行治理，谁就能定义下一阶段生态标准。

### 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线特征 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **Agent 编排器** | 追求极致 Agent 工作流的高端开发者 | 深度绑定 Claude 模型体系，MCP 生态最广，但供应链风险（可用性/成本）也最大 |
| **OpenAI Codex** | **平台旗舰** | OpenAI/ChatGPT 深度用户、企业 | 模型层（GPT-5.5）与架构层（Code-Mode、Thread Store）同时高强度重构，以平台化解决规模化问题 |
| **Gemini CLI** | **安全研究先锋** | 对数据安全与合规性极为敏感的企业开发者 | 极致的信任透明度（反向钩子修复）、AST感知分析、学术级行为评估，在安全口碑上独树一帜 |
| **Qwen Code** | **速度型全能选手** | 追求新特性、高性价比的开发者 | 迭代极快，率先落地语音输入、Artifact、MCP热更新等差异化功能，直接对标 Claude Code 填补空白 |
| **CodeWhale** | **去中心化代理平台** | 拒绝模型锁定的开源/技术极客 | 后 DeepSeek 品牌，强调多模型供应商兼容性、自定义 Agent 定义和 CI/CD 安全管线加固 |
| **OpenCode** | **全栈开源工作站** | 需要桌面端与 CLI 均衡体验的中型团队 | 高完整度（TUI/Electron/Web），侧重会话管理、大文件渲染稳定性与支付/认证流程 |
| **Pi** | **扩展开发平台** | 工具链贡献者、插件开发者 | 以扩展 API 完备性（Compaction事件、navigateTree）为核心卖点，强调本地模型支持 |
| **Copilot CLI** | **生态守门员** | GitHub/Azure 生态的忠实用户 | 依托企业级体系（配额、Sandbox、Hooks），但 CLI 独立创新力较弱，问题修复滞后 |
| **Kimi Code** | **缺席** | N/A | 无实质社区活动，战略地位存疑 |

### 5. 社区热度与成熟度

- **最高强度（行业风向标）**：**OpenAI Codex** 与 **Claude Code** 拥有最大的用户基数和最深的生态捆绑，其每一次回归（Codex 费率、Claude Android）都会引发行业级震动。它们是市场情绪的晴雨表。
- **最高增速（潜力股）**：**Qwen Code** 与 **CodeWhale** 社区正处于**创新爆发期**。Qwen 凭借高性价比和快速跟进能力在吸引“逃离 Claude 高价”的用户；CodeWhale 通过品牌重塑和安全特色，正在构建高粘性的技术硬核社区。
- **最成熟稳健（工程技术驱动）**：**Gemini CLI** 与 **Pi** 的讨论质量最高。Issues 往往指向架构级或安全协议级细节（信任对话框钩子方向错误、Compaction 原因字段缺失），说明用户群体多为资深开发者或贡献者。
- **最低活跃（边缘化）**：**Kimi Code** 和 **GitHub Copilot CLI**（相对其母公司体量）几乎处于冻结状态，急需战略调整或资源注入。

### 6. 值得关注的趋势信号

对技术决策者与开发者的参考价值如下：

1.  **“成本哨兵”将取代“模型能力”成为第一购买决策因素。**
    - 用户正在用脚投票：对隐性成本零容忍。不具备执行前成本估算（Pre-run Estimate）、子代理预算配额（Sub-agent Budget）、API 配额自动告警的 CLI 工具，将在企业采购中直接出局。

2.  **Agent 自主性的“卢比孔河”已经跨过，现在是修补护栏的时候。**
    - “Agent 太笨”的时代过去了，现在的问题是“Agent 太勤快且不可控”。工具调用死循环和过度推理消耗正成为模型幻觉之后最严重的生产力杀手。**“可靠胜于智能”** 是 2026 年下半年的产品设计哲学。

3.  **跨平台兼容性不再是加分项，而是及格线。**
    - Windows ARM64 崩溃、Linux 沙箱回归、中文路径乱码（Codex #13123）……大量低级环境问题侵蚀着工具的严肃性。如果一款 CLI 工具只能在 macOS 上稳定运行，它正在丧失进入企业市场的资格。

4.  **MCP/ACP 协议进入“治理”阶段，安全管理能力决定生态上限。**
    - 协议连接已普及，但 MCP 服务的**OAuth 分发**（OpenCode #988）、**沙箱嵌套**（Codex #29358）、**权限失效**（Claude #61097）和**成本归属**正在成为新瓶颈。具备强大 MCP 治理能力的工具将主导下一代生态话语权。

5.  **语音交互（Voice）正在成为 CLI 的“杀手级辅助”。**
    - Qwen Code 的 #5502 并非孤例。语音输入能极大幅度提升复杂 Prompt 的输入效率。当终端 TUI 遇上语音识别，AI CLI 正在从一个“编程工具”进化为“开发伙伴”，这是一个极具想象力的交互范式迁移。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截至 2026-06-22）

**分析师摘要：** 基于 anthropics/skills 官方仓库的 PR 与 Issue 数据，当前社区正从“技能数量的野蛮扩张”进入“生态质量的精细化建设”阶段。核心矛盾集中于工具链稳定性、企业级治理与安全分发机制的缺失。


## 1. 热门 Skills 排行

> 注：下方 Top PR 列表的评论数在提供数据中未明确展示，以下排行综合评估了 Skill 的前沿性、与社区高频 Issue 的关联度以及技术复杂度。

**① shodh-memory (PR #154) — 跨会话持久记忆系统**
- **功能：** 为 AI Agent 提供跨对话的持久化上下文，包含主动记忆召回与结构化存储机制。
- **社区热点：** 讨论集中在触发时机与 Token 开销的平衡，代表了社区对“强 Agent 连续性”的追求。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/154)

**② AURELION skill suite (PR #444) — 结构化认知框架（四件套）**
- **功能：** 五层认知思维模板（Kernel）+ 顾问 + Agent + 记忆，试图将 Agent 推理过程高度结构化。
- **社区热点：** 是社区探索“超越 Prompt 工程”的标志性实践，复杂度与实用性存在激烈辩论。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/444)

**③ ServiceNow platform skill (PR #568) — 企业级全平台覆盖**
- **功能：** 覆盖 ITSM、ITOM、ITAM、SecOps、HRSD、CSDM 等几乎所有 ServiceNow 模块。
- **社区热点：** 代表大型企业对“All-in-One 统一底座”的强硬需求，讨论围绕模块深度与指令精度的取舍。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/568)

**④ testing-patterns (PR #723) — 全栈测试套路**
- **功能：** 完整测试哲学（Trophy 模型）、Unit/React/E2E 测试模式、命名约定与边界用例。
- **社区热点：** 反映了社区对“AI 负责任地生产可靠代码”的强诉求，哲学层面的讨论尤其积极。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/723)

**⑤ Masonry Image & Video (PR #335) — 多模态内容生成**
- **功能：** 封装 Masonry CLI，支持 Imagen 3.0 文生图和 Veo 3.1 文生视频。
- **社区热点：** 创意与营销领域最直接的生产力诉求，讨论围绕作业管理（状态/历史/下载）展开。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/335)

**⑥ skill-quality & security analyzer (PR #83) — 生态元技能**
- **功能：** 从结构/文档/安全/性能等维度评估其他技能的质量并发现安全漏洞。
- **社区热点：** 直指生态安全与质量标准缺失的痛点，与 Issue #492（命名空间冒充）高度呼应。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/83)

**⑦ document-typography (PR #514) — 文档排版质量管控**
- **功能：** 解决 Orphan Word Wrap、孤行段落、编号错位等 AI 生成文档的排版顽疾。
- **社区热点：** 切入角度刁钻但痛点极其精准，被认为能显著提升 AI 文档的专业观感。
- **状态：** Open → [GitHub 链接](https://github.com/anthropics/skills/pull/514)

**⑧ SAP-RPT-1-OSS (PR #181) / ODT (PR #486) — 特定场景深度定制**
- **功能：** SAP 表格预测模型（#181）与 OpenDocument 格式处理（#486）。
- **社区热点：** 验证了“垂直领域超精专 Skill”的可行性路线，对政务、教育、SAP 生态用户直接利好。
- **状态：** Open → [GitHub 链接 #181](https://github.com/anthropics/skills/pull/181) | [GitHub 链接 #486](https://github.com/anthropics/skills/pull/486)


## 2. 社区需求趋势

### 趋势一：工具链可靠性危机（最紧迫）

- **0% 召回率 Bug 泛滥：** `run_eval.py` 被多次报告在所有查询下完全无法触发 Skill，导致优化循环失效（#556，12 条评论，7 👍；#1169）。这是当前所有技能开发者的头号阻塞点。
- **跨平台兼容性差：** Windows 平台存在子进程执行失败、UTF-8 编码崩溃等严重的可移植性问题（#1061，3 条评论；#1099；#1050），大量 Windows 用户处于“不可用”状态。
- **技能管理脆弱：** 出现 Skills 莫名消失（#62，10 条评论）、内容重复安装（#189，6 条评论）等基础管理 Bug。

### 趋势二：企业级安全与治理体系缺失

- **组织内共享机制空白：** 目前只能手动下载 `.skill` 文件通过聊天软件传输，缺乏组织级 Skill 商店或共享链接（#228，14 条评论，7 👍——社区最高赞 Issue）。
- **命名空间信任危机：** 社区技能随意使用 `anthropic/` 命名空间，极易冒充官方 Skill 诱骗用户授予敏感权限（#492，9 条评论）。
- **企业文档合规顾虑：** 在使用 Skills 处理 SharePoint 等企业级文档时，用户对权限写入 Skill.md 的安全性表示担忧（#1175，4 条评论）。

### 趋势三：协议开放与深层平台集成

- **MCP 化呼声高涨：** 社区强烈建议将 Skills 的能力通过 Model Context Protocol（MCP）暴露为标准化 API 接口，方便外部工具编排（#16，4 条评论）。
- **多云平台适配：** 要求 Skills 能在 AWS Bedrock 等非 Claude 原生环境中运行（#29，4 条评论）。

### 趋势四：Agent 能力深化

- **紧凑记忆机制：** 提议用符号化表示替代长 Agent 运行时的 Prose 记忆，以节省上下文窗口（#1329，3 条评论）。
- **Agent 治理安全模式：** 要求引入策略执行、威胁检测、信任评分与审计追踪等治理模式（#412，6 条评论）。

### 趋势五：站点与文档可靠性

- **参考站点宕机：** `agentskills.io` 出现“太多重定向”完全不可用（#184，4 条评论），社区对官方文档的维护力度提出质疑。
- **贡献机制缺失：** 仓库社区健康度仅 25%，急需 `CONTRIBUTING.md` 等标准化贡献文件（间接推动了 PR #509）。


## 3. 高潜力待合并 Skills（近期落地可能性大）

以下 PR 直接命中社区核心痛点，具有极高的合并优先级：

### 1️⃣ [#1298：修复 run_eval.py 始终报告 0% 召回率](https://github.com/anthropics/skills/pull/1298)
- **理由：** 直接在官方的 `skill-creator` 工具链核心下刀，解决 10+ 次独立复现的评估完全失效 Bug。**这是目前社区的绝对阻塞项。**
- **新增亮点：** 同时修复了 Windows 流读取、触发检测与并行工作者 Bug，一石多鸟。

### 2️⃣ [#1099 / #1050：Windows 兼容性修复组合](https://github.com/anthropics/skills/pull/1099)
- **理由：** 修复子进程 `PATHEXT` 解析、cp1252 编码、管道 select 等三大 Windows 不兼容问题。直接解禁 Windows 开发者社区。

### 3️⃣ [#509：添加 CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509)
- **理由：** 补齐社区贡献指引空白，将仓库社区健康指标从 25% 直接拉升，属于几乎零争议的基建合入。

### 4️⃣ [#541：修复 DOCX 跟踪修订 ID 冲突致文档损坏](https://github.com/anthropics/skills/pull/541)
- **理由：** 在 OOXML 中 `w:id` 是跨书签、修订、注释的共享 ID 空间。硬编码 ID 直接导致文档损坏。**Bug 够严重、修复够精准。**

### 5️⃣ [#210：重写 Frontend-design Skill 提升可执行性](https://github.com/anthropics/skills/pull/210)
- **理由：** 对现有旗舰 Skill 做全面重构，确保每条指令在单次对话中可严格遵循，影响前端开发者生态广泛。


## 4. 生态洞察（一句话总结）

**“社区当前最集中的诉求，是推动 Skills 生态从‘草莽创新’走向‘生产成熟’——既要紧急修补 `skill-creator` 工具链中导致评估全面失效的 0% 召回率 Bug，也要尽快搭建起官方背书的安全护栏（命名空间治理）与企业级共享分发通道，同时通过 MCP 协议开放生态融入更广阔的 AI 基础设施版图。”**

---

📊 **Claude Code 社区动态日报 | 2026-06-22**

---

### 📰 今日速览

1. **Android 兼容性危机持续**：Issue [#50270](https://github.com/anthropics/claude-code/issues/50270) 的回归（v2.1.113+ 起无 JS 回退路径）依然是最热议题，积累 53 条评论和 51 个赞，官方长期未响应加剧了用户不满。
2. **MCP 子代理成本失控引关注**：随着 `deep-research` 和 Gmail MCP 等技能普及，用户开始密集遭遇隐性 Token 消耗（[#69931](https://github.com/anthropics/claude-code/issues/69931), [#68703](https://github.com/anthropics/claude-code/issues/68703)），成本透明化呼声极高。
3. **API 可用性与错误恢复仍是核心痛点**：新收到的 API 宕机报告（[#69942](https://github.com/anthropics/claude-code/issues/69942)）和 400 错误杀死会话（[#47391](https://github.com/anthropics/claude-code/issues/47391)）表明，服务稳定性与容错机制急需加强。

---

### 版本发布

过去 24 小时内无新版本发布。

---

### 🐛 社区热点 Issues

挑选了过去 24 小时内更新且最值得关注的 10 条 Issue：

| # | 标题 | 热度 | 关键影响 |
|---|------|------|----------|
| **#50270** | [Termux/Android 原生二进制兼容性回归](https://github.com/anthropics/claude-code/issues/50270) | 💬 53 / 👍 51 | 版本切换到 glibc 导致 Android 完全不可用，无 JS fallback，**长期未解决** |
| **#24798** | [多会话间通信与工作流编排](https://github.com/anthropics/claude-code/issues/24798) | 💬 38 / 👍 18 | 大型项目需要跨 Claude 会话传递上下文和任务依赖，属**顶级功能呼声** |
| **#36179** | [VS Code 插件 `redacted_thinking` 错误](https://github.com/anthropics/claude-code/issues/36179) | 💬 29 / 👍 18 | 插件内频繁的“不支持内容类型”错误，严重阻碍 **IDE 集成体验** |
| **#69942** | [API Service Unavailable 宕机](https://github.com/anthropics/claude-code/issues/69942) | 💬 5 / 👍 11 | **当天新增高赞 Bug**，表明近期 API 稳定性出现波动，影响大量用户 |
| **#61097** | [Remote Routine 权限拦截失效：Always Allow 不生效](https://github.com/anthropics/claude-code/issues/61097) | 💬 12 / 👍 6 | MCP 自动化流程的核心信任机制损坏，**让 Routine 功能形同虚设** |
| **#65995** | [Claude Desktop PTY 泄漏导致系统终端崩溃](https://github.com/anthropics/claude-code/issues/65995) | 💬 4 / 👍 4 | **系统级 Bug**，泄漏 PTY fd 导致 macOS 无法创建新终端，破坏性极强 |
| **#69931** | [Claude Max 周配额被 MCP 子代理快速耗尽](https://github.com/anthropics/claude-code/issues/69931) | 💬 2 / 👍 1 | 使用 Gmail MCP 等子代理时 Token 消耗远超预期，**成本透明性缺失的典型代表** |
| **#47391** | [API 400 错误杀死会话且无法恢复](https://github.com/anthropics/claude-code/issues/47391) | 💬 9 / 👍 5 | 图片处理失败导致用户断开整个会话上下文，**数据和进度完全丢失** |
| **#69272** | [VS Code 插件支持 `/fork` 对话分支](https://github.com/anthropics/claude-code/issues/69272) | 💬 3 / 👍 1 | CLI 已支持的分支功能移植到 IDE，代表**用户对复杂实验性探索的需求** |
| **#68703** | [技能执行前应展示估算成本并请求确认](https://github.com/anthropics/claude-code/issues/68703) | 💬 2 / 👍 0 | 防止 `deep-research` 等技能无预警消耗大量配额，**“成本锁”概念雏形** |

---

### 🔄 重要 PR 进展

根据数据源，过去 24 小时内更新的 PR 共 2 个：

- **[#69916](https://github.com/anthropics/claude-code/pull/69916) fix: 修复 Issue 分类脚本静默退出**
  - 修复了 `scripts/edit-issue-labels.sh` 在缺少参数时以静默 `exit 1` 退出的问题，改为打印错误信息后再退出。改进了内部 Issue Triage 工作流的可用性。

- **[#4943](https://github.com/anthropics/claude-code/pull/4943) feat: 添加 Shell 命令补全脚本**
  - 为 bash、zsh 和 fish 提供了静态补全配置。该 PR 已有近一年历史（2025-08-01 提交），社区无新讨论，官方可能更倾向于动态生成方案（如 `claude completion <shell>`）。

*(注：当下 PR 活动较少，团队重心预计在处理上述高优 Bug 社区讨论上)*

---

### 📈 功能需求趋势

综合当日社区议题，用户关注的功能方向如下：

| 趋势方向 | 高关联 Issue | 用户核心期望 |
|----------|-------------|--------------|
| **多智能体协作** | #24798, #49039 | 多会话编排、项目级会话管理，建立复杂工作流 |
| **成本透明化** | #59709, #50926, #68703, #69931 | 程序化暴露 /cost 数据、技能执行前预审 Token、配额告警 |
| **IDE 功能深度对齐** | #69272, #69778, #36179 | 原生 UI（非终端）、对话分支、稳定的渲染兼容性 |
| **MCP 生态成熟化** | #61097, #65982, #69960 | 权限精细化、自动化审计门控、集成稳定性 |
| **平台兼容性扩展** | #50270, #59813 | Android Termux 回归、Linux RISC-V 原生支持 |

---

### 💡 开发者关注点

1. **稳定性是生命线**
   - **宕机与网络错误**（#69942）、**不可恢复会话**（#47391）和 **资源泄漏**（#65995）是开发者最深层的痛点。任何导致工作流中断或进度丢失的 Bug 都会迅速破坏信任。

2. **自动化信任度亟待修复**
   - MCP Routine 的 `Always Allow` 权限失效（#61097）、子代理 Token 盗刷（#69931），正在侵蚀用户对自动化模式的信心。用户需要更可靠的权限保活机制和运行时成本护栏。

3. **痛恨 Regression**
   - 新版破坏旧平台正常工作（#50270 Android）、造成 UI 渲染退化（#67763 缩进）极易引发社区反弹。稳定的 API 和全面的环境兼容性测试是刚需。

4. **成本不再是事后指标**
   - 用户不再满足于调用事后统计的 `/cost`，而是要求在 **执行前** 有估算（#68703）、**执行中** 有可视化的状态行（#59709）、**执行后** 能被钩子系统（Hooks）消费（#50926）。成本管控正在从查看工具演变为门控机制。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 2026-06-22 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 (2026-06-22)

**作者：** AI 开发工具技术分析师

## 1. 今日速览

- **Rate Limit 危机爆发**：社区最大的负面反馈集中在 Plus 计划下 `gpt-5.5` 模型的 Token 消耗量莫名激增 10-20 倍，导致大量用户额度耗尽，引发广泛讨论（#28879）。
- **Windows 平台稳定性堪忧**：Sandbox 回归、代理环境冲突、补丁工具链异常等多个严重 Bug 在 Windows 平台上集中涌现，成为开发者痛点的重灾区。
- **核心架构迎来大重构**：工程团队正在积极合入大量关于“Code-Mode”和“Thread Store”的重构 PR，旨在解决会话性能、状态同步等底层架构问题，为未来稳定性奠定基础。

## 2. 版本发布

在过去 24 小时内，连续发布了两个 Alpha 版本，主要针对底层 Rust 运行时的修复与优化：

- **[v0.142.0-alpha.9](https://github.com/openai/codex/releases/tag/v0.142.0-alpha.9)** 和 **[v0.142.0-alpha.10](https://github.com/openai/codex/releases/tag/v0.142.0-alpha.10)**
    - 鉴于当前存在大量 Rate Limit 计量和 Windows Sandbox 回归问题，这些迭代很可能包含了针对后端服务计费逻辑和客户端沙箱的紧急修补。

## 3. 社区热点 Issues

1.  **Rate Limit 成本飙升 10-20 倍** [#28879](https://github.com/openai/codex/issues/28879)
    - **🔥 热度最高**: 自 6 月 16 日起，用户在 Plus 计划下使用 `gpt-5.5`，原本能用 20+ 次的额度现在 2-3 次 Prompt 就耗尽。用户已附上详细的 `token_count` 日志证据，要求 OpenAI 官方给出明确解释与补偿。
2.  **要求提供 Windows 独立安装程序** [#13993](https://github.com/openai/codex/issues/13993)
    - **长期 Top 需求**: 企业用户受限于组策略和离线环境，无法使用 Microsoft Store，强烈需要传统的 `codex-setup.exe` 安装方式。
3.  **账号被遗留手机号认证锁死** [#25749](https://github.com/openai/codex/issues/25749)
    - **用户体验死穴**: 用户即使已通过 Google OAuth 登录并可使用 ChatGPT，但 Codex Desktop 强制要求验证一个已失效的旧手机号，且官方未提供任何更换号码或账户恢复的路径。
4.  **VSCode 扩展无法打开历史对话** [#18993](https://github.com/openai/codex/issues/18993)
    - **影响面广**: 自版本 1.117.0 起的回归 Bug，导致 VS Code 扩展中无法访问任何过往会话历史，严重影响开发者调试与回溯。
5.  **macOS Dock 严重崩溃 (DockTile 递归)** [#27694](https://github.com/openai/codex/issues/27694)
    - **致命 Bug**: Desktop 版本 26.609.30741 触发 `CodexDockTilePlugin` 的 `setDockTile` 递归调用，直接导致 macOS Dock 崩溃。
6.  **Windows Sandbox 回归 (CLI 0.138.0)** [#26158](https://github.com/openai/codex/issues/26158)
    - **核心功能损坏**: `CreateProcessAsUserW` 错误导致 Windows Sandbox 环境完全无法启动。用户被迫回滚至 0.132.0 版本保平安。
7.  **MCP App 内联 UI 无法渲染** [#21019](https://github.com/openai/codex/issues/21019)
    - **生态瓶颈**: MCP 工具调用成功后，返回的 `mcp_app_resource_uri` 在 Desktop 客户端中被忽略，导致无法渲染内联 UI。这使得 MCP 插件功能大打折扣。
8.  **Windows 全局代理导致 apply_patch 失败** [#29178](https://github.com/openai/codex/issues/29178)
    - **企业用户陷阱**: 当系统设置了全局 HTTP 代理后，最新的 Desktop 更新破坏了 `apply_patch` 和 `fs-helper` 工具。回滚到旧版本可临时解决。
9.  **中文文件名路径无法打开（Open in Finder）** [#13123](https://github.com/openai/codex/issues/13123)
    - **本地化问题**: Desktop 版在 macOS 上通过“Open in Finder”打开含有中文的路径时，因未正确处理 URL 编码而完全失败。
10. **Computer Use 触发系统安全进程 CPU 飙升** [#28545](https://github.com/openai/codex/issues/28545)
    - **奇怪的副作用**: macOS 用户在使用 Computer Use 功能时，触发了系统级安全进程 `syspolicyd` 和 `trustd` 的 CPU 持续高占用，导致整个系统卡顿。

## 4. 重要 PR 进展

1.  **Code-Mode: 重构 Cell 生命周期与运行时** [#29290](https://github.com/openai/codex/pull/29290) / [#29291](https://github.com/openai/codex/pull/29291) / [#29292](https://github.com/openai/codex/pull/29292)
    - **架构升级**：将 Cell 的**创建**与**观察**逻辑完全解耦，暴露出传输无关的 `SessionRuntime`。这为未来减少死锁和提升代码执行稳定性打下坚实基础。
2.  **优化 Thread 列表与恢复性能** [#29352](https://github.com/openai/codex/pull/29352) / [#29355](https://github.com/openai/codex/pull/29355) / [#29357](https://github.com/openai/codex/pull/29357)
    - **性能优化**：将 Thread 列表和恢复操作从繁重的文件扫描迁移至轻量级 SQLite 投影，并引入 Checkpoint 限制。对拥有大量会话的重度用户来说，这是显著的体验提升。
3.  **安全审查（Safety Buffering）事件透传到前端** [#29371](https://github.com/openai/codex/pull/29371)
    - **功能增强**：允许前端客户端展示“正在进行安全审查”的状态，提升 Agent 决策过程中的透明度与用户体验。
4.  **MCP Sandbox 状态注入** [#29358](https://github.com/openai/codex/pull/29358)
    - **生态升级**：允许 Codex Sandbox 直接消费 `codex/sandbox-state-meta`，意味着 MCP 服务器可以将自己的 Sandbox 状态无感传递给 Codex，实现更复杂的沙箱嵌套逻辑。
5.  **支持 npm 市场插件源** [#29375](https://github.com/openai/codex/pull/29375)
    - **生态扩展**：正式引入对 npm 包作为 MCP 插件源的支持。开发者可以直接通过包名引用插件，并支持版本锁定与私有 Registry。
6.  **Workspace Headline 终端状态栏** [#28232](https://github.com/openai/codex/pull/28232)
    - **用户体验**：在 TUI 状态栏中增加显示当前 Workspace 的标识，并定时刷新，方便用户在终端内感知当前工作域。
7.  **模型采样前刷新环境上下文** [#29073](https://github.com/openai/codex/pull/29073)
    - **Agent 稳定性**：修复了远程环境启动慢导致模型首次采样时上下文为空的问题。现在会在采样前尝试刷新环境状态，以提供更准确的信息。
8.  **新增自动压缩退出机制（调试开关）** [#28260](https://github.com/openai/codex/pull/28260)
    - **调试工具**：提供一个内部 Feature Flag，允许开发者禁用自动上下文压缩，便于在调试上下文窗口耗尽或压缩异常时定位问题。
9.  **更新 Plan Mode 提示词** [#29301](https://github.com/openai/codex/pull/29301)
    - **行为优化**：优化了 Plan Mode 的提示词，使其生成的计划能更好的展示给用户，并支持用户直接退出 Plan Mode 进入实现阶段，减少手动切换的步骤。
10. **冗余 Rollout 读取消除** [#29109](https://github.com/openai/codex/pull/29109)
    - **性能优化**：修复了 Thread 读取和恢复操作中对同一历史文件进行重复解析的问题，减少了不必要的 I/O 开销。

## 5. 功能需求趋势

- **Rate Limit 精细化管控**：社区不再满足于单纯的额度数字。开发者强烈要求 Agent 自身能感知和暴露剩余配额，并支持接近上限时自动执行“优雅停止”策略，而不是粗暴报错（#24927）。
- **MCP 生态进入“渲染”深水区**：基础调用能力已经具备，但社区反馈集中在**内联 UI 渲染**（#21019）和 **Sandbox 状态共享**上。能否解决“让插件能够像原生 App 一样交互”是 MCP 能否成功的关键。
- **Windows 环境“一等公民”化**：从独立安装程序（#13993）到 Sandbox 稳定性（#26158 等），Windows 用户的呼声极其强烈。Codex 在 Windows 上的体验直接决定了它在企业 .NET 开发生态中的渗透率。
- **零配置与开箱即用**：用户期待无感知的国际化支持（中文路径）、稳定的远程开发体验（SSH Remote 不卡死）以及可靠的历史记录功能。这些“小问题”直接决定了工具的专业度。

## 6. 开发者关注点

- **当前最大痛点：费用失控**
  - [#28879](https://github.com/openai/codex/issues/28879) 是绝对的舆论中心。用户震怒于单位时间的成本暴增 10-20 倍，这直接否定了 Codex 作为生产力工具的投资回报率。开发者正密切关注此问题的官方回复和处理进度。
- **认证与账户恢复流程断裂**
  - [#25749](https://github.com/openai/codex/issues/25749) 揭示了一种危险的状态：用户能够登录 ChatGPT 但却被 Codex Desktop 拒之门外。产品线之间的认证割裂成为影响客户续费的黑天鹅事件。
- **历史记录可靠性是底线**
  - VS Code 扩展无法打开历史对话（[#18993](https://github.com/openai/codex/issues/18993)）被开发者视为影响工作的严重问题。AI 辅助编程的连续性依赖于对话上下文的可回溯性，该功能损坏严重破坏了开发工作流。
- **建议 Windows 用户暂缓升级**
  - 鉴于 Windows Sandbox 回归（#26158）和全局代理冲突（#29178）等问题，建议生产环境下的 Windows 用户暂时锁定在已知稳定的旧版本（如 0.132.0 或 26.611.x），等待官方修复。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，以下是为您生成的 2026-06-22 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 — 2026-06-22

## 📰 今日速览
今日社区动态主要聚焦于**生产环境的稳定性和 Agent 行为的修复**。夜间构建 (`v0.49.0-nightly`) 失败，但开发团队迅速提交了多项关键修复 PR。社区热点集中在**子代理（Subagent）的回收机制缺陷**、**Shell 命令执行卡死**以及**Auto Memory 系统的安全性**优化上。多个关于**会话文件恢复**的 PR 被提出，显示开发者非常关注数据持久化和恢复的可靠性。

## 🚀 版本发布
截至数据采集时间，暂无新的正式版本发布。值得注意的是，**`v0.49.0-nightly.20260622` 的夜间构建流程在今日失败** (Issue #28087)，相关开发人员应已关注到此问题，建议下游测试者暂勿使用该夜间版本。

## 🔥 社区热点 Issues (Top 10)
挑选了 10 个值得关注的核心 Issue，涵盖了 Agent 行为、核心功能 Bug 和安全性改进。

1.  **[[Bug] 通用Agent挂起 #21409](https://github.com/google-gemini/gemini-cli/issues/21409)**
    - **重要性**: **P1 优先级，社区反响强烈 (👍 8)**。当 CLI 将任务委派给通用 Agent 时，会无限期挂起，严重影响日常使用。用户只能通过手动指示模型不要使用子 Agent 来规避。
    - **社区反应**: 多个用户确认此 Bug 存在，并提供了复现步骤。
    - **状态**: `status/need-retesting`，团队已标记需重新测试。

2.  **[[Bug] Shell命令执行完成后卡住 #25166](https://github.com/google-gemini/gemini-cli/issues/25166)**
    - **重要性**: **P1 优先级，影响核心交互流程**。即使 Shell 命令已完成，Gemini CLI 仍显示 “Awaiting user input” 并卡死，导致无法进行下一步操作。
    - **社区反应**: 用户报告此问题频繁出现，严重影响工作流。
    - **状态**: 等待处理。

3.  **[[Bug]子代理达到最大轮次后误报成功 #22323](https://github.com/google-gemini/gemini-cli/issues/22323)**
    - **重要性**: **P1 优先级，误导用户**。子代理（如 `codebase_investigator`）在达到 `MAX_TURNS` 限制后，本应失败，但却向主代理报告 “status: success”，导致主代理误以为任务已完成，隐藏了潜在的分析中断问题。
    - **状态**: `status/need-retesting`。

4.  **[[Bug] Auto Memory 日志安全性问题 #26525](https://github.com/google-gemini/gemini-cli/issues/26525)**
    - **重要性**: **P2 优先级，涉及安全合规**。Auto Memory 功能在将对话记录发送给模型进行摘要提取时，脱敏操作发生在模型接收到内容之后，存在密钥泄露风险。同时，Service 日志也可能泄露数据。
    - **社区反应**: 由社区成员 `SandyTao520` 提出，显示了社区对安全细节的关注。
    - **状态**: 待处理。

5.  **[[Bug] ACP模式下Token计数不完整 #27985](https://github.com/google-gemini/gemini-cli/issues/27985)**
    - **重要性**: **近期热点**。在作为 ACP 服务器运行时，报告的 token 用量遗漏了 `cached` 和 `thought/reasoning` 部分，导致客户端成本估算偏高。
    - **社区反应**: 用户 `VascoSch92` 在上周提出，讨论显示该问题会导致错误的成本归因。
    - **状态**: 新 Issue，待处理。

6.  **[[EPIC] 组件级评估 #24353](https://github.com/google-gemini/gemini-cli/issues/24353)**
    - **重要性**: **P1 优先级，长期基础设施**。此 Issue 是一个 EPIC，追踪强化组件级评估的工作。它是对之前 “行为评估（behavioral evals）” 的扩展，旨在构建更健壮的评测体系。
    - **社区反应**: 当前为维护者内部讨论，但体现了团队对代码质量的持续投入。
    - **状态**: 进行中。

7.  **[[EPIC] AST感知文件操作评估 #22745](https://github.com/google-gemini/gemini-cli/issues/22745)**
    - **重要性**: **前瞻性技术探索**。该 EPIC 旨在研究使用 AST（抽象语法树）感知的文件读取、搜索和代码映射是否能带来价值。这有望提高工具调用的精准度，减少 Token 浪费。
    - **社区反应**: 收到 1 个 👍，社区对此类提升模型代码理解能力的方向抱有期待。
    - **状态**: 探索中。

8.  **[[Bug] Agent应阻止破坏性行为 #22672](https://github.com/google-gemini/gemini-cli/issues/22672)**
    - **重要性**: **客户反馈问题**。Agent 在某些场景下（如 Git 操作）会使用 `--force` 或 `git reset` 等危险命令，用户希望在执行此类操作前得到更明确的警告或干预。
    - **状态**: 已分类，待处理。

9.  **[[Bug] 模型频繁在随机位置创建临时脚本 #23571](https://github.com/google-gemini/gemini-cli/issues/23571)**
    - **重要性**: **影响工作区整洁度**。当限制模型使用 Shell 时，它会转而生成多个编辑脚本，散落在项目各处，增加了代码审查和清理的负担。
    - **状态**: 已分类，待处理。

10. **[[Bug] 使用Vite创建应用时卡在交互提示符 #22465](https://github.com/google-gemini/gemini-cli/issues/22465)**
    - **重要性**: **P2 优先级，影响开发体验**。当用户指示 Agent 通过 Vite 创建新应用时，它会被交互式提示符卡住，无法自动完成。
    - **状态**: 团队已计划创建新的行为评估测试并调整 Prompt 来解决此问题。

## ✨ 重要 PR 进展 (Top 10)
这些 PR 正在解决今日社区讨论的许多核心问题，主要集中在会话恢复、安全性、Agent 超时和依赖更新。

1.  **[fix(core): 为 Web 搜索工具添加超时 #27910](https://github.com/google-gemini/gemini-cli/pull/27910)**
    - **重要性**: **P1 优先级**。解决 `google_web_search` 调用可能导致 Agent 无限等待的问题。通过设置 120 秒本地超时，Agent 可以优雅地处理搜索失败并自行恢复，而非永久挂起。

2.  **[fix(trust): 披露以规范嵌套形状声明的钩子 #27903](https://github.com/google-gemini/gemini-cli/pull/27903)**
    - **重要性**: **P1 优先级，安全修复**。修复了文件夹信任对话框的一个严重 Bug：它只显示扁平语法的 `command`，而忽略了规范嵌套形状中定义的 `SessionStart` 等钩子。这使用户可能在不知情的情况下运行了危险命令。

3.  **[fix(core): 修复信任对话框显示与实际执行钩子相反的问题 #27915](https://github.com/google-gemini/gemini-cli/pull/27915)**
    - **重要性**: **P1 优先级，安全修复**。此 PR（#27903 的补充）进一步指出，信任对话框仅显示实际运行的**反向**钩子，加剧了安全风险。该 PR 旨在彻底解决这一问题。

4.  **[fix(core): 验证 GCP 项目 ID 格式 #27916](https://github.com/google-gemini/gemini-cli/pull/27916)**
    - **重要性**: **P2 优先级，错误处理**。修复 `auto-memory` 因存储了无效的 GCP 项目显示名称而导致的 API 403 和 `CONSUMER_INVALID` 错误，提升了 GCP 集成的健壮性。

5.  **[fix(cli): 不提供恢复未保存会话的入口 #27914](https://github.com/google-gemini/gemini-cli/pull/27914)**
    - **重要性**: **修复用户端 Bug (Fixes #27277)**。当磁盘空间不足 (`ENOSPC`) 导致会话文件无法保存时，CLI 仍会提示 “To resume this session”，这具有误导性。该 PR 能在会话未保存时，自动屏蔽恢复提示。

6.  **[fix(core): 修复 `projectHash` 缺失时 JSONL 会话无法加载的问题 #27904](https://github.com/google-gemini/gemini-cli/pull/27904)**
    - **重要性**: **P2 优先级，数据修复**。解决了当会话记录中的 `projectHash` 字段缺失时，`loadConversationRecord` 会尝试使用错误的解析方式读取整个文件，导致加载失败。修复后能正确处理老版本或不完整的会话文件。

7.  **[fix(core): 恢复包含损坏或缺失元数据行的会话 #27912](https://github.com/google-gemini/gemini-cli/pull/27912)**
    - **重要性**: **P2 优先级，数据恢复**。此 PR 建立在 #27904 之上，进一步增强了对损坏 JSONL 会话文件的恢复能力，使其能跳过损坏的元数据行、恢复尽可能多的数据，是提升数据健壮性的重要一环。

8.  **[fix(cli): 修复列表会话时的启动竞态条件 #27906](https://github.com/google-gemini/gemini-cli/pull/27906)**
    - **重要性**: **P2 优先级，可靠性提升**。修复了启动时后台清理任务与 `--list-sessions` 命令之间的并发竞争，避免了因清理线程删除文件而导致列表扫描出现 `ENOENT` 错误。

9.  **[fix(cli): 使 `useLogger` 在 `/clear` 后跟踪新的会话 ID #27907](https://github.com/google-gemini/gemini-cli/pull/27907)**
    - **重要性**: **P3 优先级，内部状态管理**。修复了执行 `/clear` 命令后，日志记录器（Logger）未能更新到新会话 ID 的问题，可能导致后续日志被错误地关联到旧会话。

10. **[chore(deps): 批量依赖更新 #28086, #28085, #28084](https://github.com/google-gemini/gemini-cli/pull/28086)**
    - **重要性**: **安全与维护**。由 `dependabot` 自动发起的 PR，分别将 `undici` (HTTP库)、`glob` (文件匹配) 和 `http-proxy-agent` (代理) 等核心依赖升级到新版。这些更新通常包含关键的安全补丁和性能改进。

## 📈 功能需求趋势
从近期议题中可以看出社区对 Gemini CLI 的期待正在向**更高的自主性、安全性和可观测性**发展。

- **Agent 行为改进**: 社区强烈希望 Agent 能更智能、更安全。包括：**主动且恰当地使用子代理和技能**、**在执行有风险的操作（如 Git force push）前进行确认或劝阻**、**减少在文件系统中乱写临时文件的行为**。
- **提升性能与稳定性**: 用户对 CLI 卡死、挂起、Token 浪费等问题高度敏感。对 **Agent 超时机制**、**AST感知文件读取**以减少Token、**终端重绘性能**的优化是持续关注点。
- **安全与合规**: Auto Memory 的**日志脱敏**和**信任模型**的透明化是近期的热门方向。用户显然不希望自己的 API 密钥或敏感代码在不经意间被上传或暴露。
- **开发体验改善**: 改进 `/chat share` 以包含**子代理执行轨迹**、**更好的构建失败上报**（Subagent context）、**会话恢复**的功能是开发者反馈的高频需求。

## 📌 开发者关注点
总结当前开发者反馈中最突出的痛点：

- **Agent 挂起和不响应**: 这是当前最核心的痛点，无论是通用 Agent 还是 `browser_agent`，挂起问题严重影响了用户对 Agent 的信任和可用性。
- **会话与状态管理问题**: 用户对会话文件无法恢复、日志 ID 错乱、保存前提示恢复等多个会话相关问题提出了修复请求，这表明工具的**数据一致性和状态管理**是当前的一个薄弱环节。
- **工具使用的有限性**: 社区认为 Agent **“不用技能”**、**“不会主动调用”** 是个核心问题。如果配置了自定义工具（如 Gradle 或 Git 技能），Agent 却在相关场景下视而不见，这极大地削弱了工具扩展的价值。
- **构建与运维的稳定性**: 夜间构建的失败、依赖升级的频繁以及 `ACP` 模式下数据统计的不准确，都表明开发者对于整个 CI/CD 流程和运维指标的准确性有较高要求。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-06-22

**数据来源：** `github.com/github/copilot-cli`  
**统计时段：** 过去 24 小时内更新（2026-06-21 ~ 2026-06-22）  
**版本发布：** 无  

---

## 今日速览

今日无新版本发布，但社区提交了多个影响稳定性和可观测性的 Issue。**Windows ARM64 下 `copilot.exe` 在高负载时硬崩溃**（#3687）是目前最严重的 bug，已有 6 条评论并复现于多个版本。同时，**配额扣除计算错误**（#3881）、**缺少 hook 管理命令**（#3871）以及**沙箱文档与功能不一致**（#3861）引发了开发者集中讨论。整体来看，开发者对 CLI 的稳定性、计量透明度和插件管理能力有较高期待。

---

## 社区热点 Issues

过去 24 小时内共有 7 个有效 Issue 获得更新（另有 1 个空模板 Issue 已被关闭并忽略），覆盖稳定性、UX、计量、插件生态等多个维度。以下按关注度排序：

### 1. #3687 – Windows ARM64 下 `copilot.exe` 负载崩溃（0xc0000409）
- **作者：** JW-Sthlm（2026-06-05 创建，2026-06-21 更新）  
- **状态：** OPEN  
- **评论 / 👍：** 6 / 1  
- **摘要：** `copilot.exe` 在 Windows Terminal 多标签同时恢复或内存压力下会触发 Windows 致命退出（BEX64 / 0xc0000409），而非正常关闭。已在 1.0.57 和 1.0.60 上复现，影响 Windows ARM64 用户。社区期待尽快修复或提供 workaround。  
- **链接：** github/copilot-cli Issue #3687

### 2. #3881 – 预付费配额扣除比例错误（6x 模型按 5% 而非 2% 扣除）
- **作者：** yurivict（2026-06-22 创建，2026-06-22 更新）  
- **状态：** OPEN  
- **评论 / 👍：** 0 / 0  
- **摘要：** 用户使用 Claude Sonnet 4.5（6x）后，配额从 20% 降至 15%，扣除 5% 而非预期的 2%（1/300×6）。因立即影响付费用户利益，要求退回 3% 配额或澄清计算逻辑。  
- **链接：** github/copilot-cli Issue #3881

### 3. #3871 – 无法列出已安装的 hook（缺少类似 MCP 的 `copilot mcp list`）
- **作者：** ken-jo（2026-06-20 创建，2026-06-21 更新）  
- **状态：** CLOSED  
- **评论 / 👍：** 2 / 0  
- **摘要：** 插件文档提及 hooks，但 CLI 没有提供任何枚举或查看已安装 hook 的命令，与 MCP 的 `copilot mcp list` 形成反差。用户期望 hooks 具有同等级别的可发现性。虽已关闭，但反映了插件管理一致性的需求。  
- **链接：** github/copilot-cli Issue #3871

### 4. #3861 – 本地沙箱文档与功能实际不符（per-host 过滤等不生效）
- **作者：** torumakabe（2026-06-19 创建，2026-06-21 更新）  
- **状态：** OPEN  
- **评论 / 👍：** 1 / 0  
- **摘要：** 文档和 `/sandbox` UI 宣称支持 `allowedHosts` / `blockedHosts` 以及跨平台隔离，但实际并未生效。用户要求文档对齐实际情况，避免误导。这也暴露了沙箱功能尚未达到宣称的成熟度。  
- **链接：** github/copilot-cli Issue #3861

### 5. #3874 – VS Code 中 `preToolUse` hook 拒绝无效
- **作者：** springcomp（2026-06-20 创建，2026-06-21 更新）  
- **状态：** OPEN  
- **评论 / 👍：** 1 / 0  
- **摘要：** 在 VS Code 1.125.1 + Copilot Chat v0.53.1 下，通过 `hooks.json` 配置的 `PreToolUse` denial 完全不起作用。影响通过 Agent hook 实现安全控制的用户，需尽快修复。  
- **链接：** github/copilot-cli Issue #3874

### 6. #3867 – 聊天会话缺少上下文窗口指示器及压缩通知
- **作者：** sonydogg（2026-06-19 创建，2026-06-21 更新）  
- **状态：** CLOSED  
- **评论 / 👍：** 1 / 0  
- **摘要：** 当前 UI 没有显示当前会话的 token 用量/剩余，且上下文压缩（compaction）在后台静默进行，用户完全不知情。期望类似模型名称旁边的显示方式。虽已关闭，但仍代表一类常见 UX 需求。  
- **链接：** github/copilot-cli Issue #3867

### 7. #3778 – Feature Request：通过 OpenTelemetry 发射成本/配额指标
- **作者：** kewinremy（2026-06-12 创建，2026-06-21 更新）  
- **状态：** OPEN  
- **评论 / 👍：** 1 / 0  
- **摘要：** CLI 已支持 OTel 输出 token 用量和操作耗时，但缺少成本相关的 metric（如每次请求的消耗配额）。建议增加与 Claude Code 类似的 `copilot.cost.usage` 指标，方便企业监控。  
- **链接：** github/copilot-cli Issue #3778

---

## 重要 PR 进展

过去 24 小时内仅有 1 个 PR 获得更新：

### #3880 – [OPEN] 内容疑似测试/无关提交
- **作者：** 4tha5（2026-06-21 创建，2026-06-21 更新）  
- **评论 / 👍：** 无评论 / 0  
- **摘要：** 该 PR 的 diff 显示为一个 React 组件 `ArtistCard`，与 Copilot CLI 本身功能完全无关，可能来自错误的分支或测试。目前无评审活动，建议社区维护者关闭或清理。**对项目无实际影响。**  
- **链接：** github/copilot-cli PR #3880

> **说明：** 因数据来源中仅此一个 PR，且内容不相关，故本次日报不展开分析。

---

## 功能需求趋势

综合当前社区 Issue，最受关注的功能方向为：

1. **稳定性与平台兼容性**：Windows ARM64 下的进程崩溃是当前最紧迫的 bug，需优先修复。
2. **计量/配额透明化**：包括配额扣除的准确计算（#3881）以及通过 OpenTelemetry 输出成本指标（#3778）。用户要求清晰、可审计的消耗记录。
3. **插件生命周期管理**：hooks 目前无法枚举或查看（#3871），与 MCP 管理能力不对等。社区希望统一插件（MCP、hooks、agents）的可观察性。
4. **沙箱能力落实**：文档宣传的 per-host 过滤和跨平台隔离并未实现（#3861），社区要求功能对齐文档或修正文档。
5. **IDE 集成一致性**：VS Code 中 agent hook 的 denial 不生效（#3874），反映 CLI 及扩展对 hook 的支持在不同前端存在差异。
6. **会话 UX 改进**：上下文窗口可视化、压缩通知等（#3867）可提升用户对长会话的掌控感。

---

## 开发者关注点（痛点/高频需求）

- **Windows ARM64 崩溃**：⚠️ 硬崩溃导致数据丢失，影响日常使用，社区期待 hotfix。
- **配额计算偏差且无日志**：用户无法自行核算，只能依赖支持，降低信任。
- **hooks 管理黑盒**：安装/配置 hooks 后无法确认状态，调试困难。
- **沙箱功能“言行不一”**：用户投入精力配置无效功能，浪费排查时间。
- **VS Code 中 hook 权限无效**：安全策略无法落地，影响使用 Agent 的企业用户。
- **缺乏成本/配额监控**：企业用户无法将 CLI 用量纳入内部成本核算体系。
- **上下文窗口无反馈**：长会话中 token 超限导致内容丢失而不知，影响对话连贯性。

> ⚡ **建议维护团队优先关注 #3687（崩溃）、#3881（配额错误）和 #3874（VS Code hook 无效），这三项直接影响付费用户的正常使用与信任。**

---

*本日报基于 GitHub 公开数据自动生成，仅供参考。详细讨论请点击对应 Issue/PR 链接参与。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，作为专注于AI开发工具的技术分析师，以下是根据您提供的 GitHub 数据生成的 **Kimi Code CLI 社区动态日报（2026-06-22）**。

---

# Kimi Code CLI 社区动态日报 | 2026-06-22

## 今日速览

今日项目动态较为平静，无新版本发布和合并的 Pull Request。社区讨论主要围绕两个关键议题：一是长期存在的跨会话记忆系统需求仍待明确反馈；二是新提交的高优先级Bug显示，`kimi acp` 模式下无法加载 MCP 服务器，导致工具链断裂，这是开发者目前最迫切的痛点。

## 社区热点 Issues

今日共有2条活跃Issue，均对开发者的工作流程有重大影响。

1.  **[#2464] `kimi acp` 模式下 MCP 服务器不工作（严重Bug）**
    -   **重要性**：高。这是一个新提交的严重功能缺陷，直接影响使用 `acp` 协议的自动化工作流。该问题明确指向 `kimi acp` 模式无法加载 MCP 服务器配置，导致外部工具和上下文在ACP模式下完全失效，这与交互模式下正常工作的预期行为相悖。
    -   **社区反应**：暂无评论，但该问题直接阻断依赖ACP的自动化流程，预计将引发广泛关注。作者 `Tasktivity` 详细描述了版本、平台和模型信息，便于开发者复现。
    -   ✨ [Issue链接](https://github.com/MoonshotAI/kimi-cli/issues/2464)

2.  **[#1283] 功能请求：记忆系统 - 跨会话持久化上下文**
    -   **重要性**：中高。这是一个长期未解决的增强请求，旨在让Kimi CLI能够跨会话记住项目模式、用户偏好和上下文。虽然创建时间较早，但更新日期为今日，表明项目团队或社区仍在关注。
    -   **社区反应**：共有6条评论，但无新的点赞，说明社区对此功能虽有兴趣，但可能因长期未实现而热度有所下降。该issue是衡量Kimi CLI“智能代理”能力方向的关键指标。
    -   ✨ [Issue链接](https://github.com/MoonshotAI/kimi-cli/issues/1283)

## 功能需求趋势

根据今日活跃的Issues，社区对Kimi Code CLI的功能需求集中在以下方向：

-   **持久化上下文与记忆系统**：用户不再满足于单个会话内的上下文，希望工具能像一个真正的伙伴一样，跨项目会话记住关键信息（如项目架构、编码规范、用户偏好）。这是构建“AI原生”开发体验的核心需求。
-   **工具链与生态集成**：`#2464` 暴露了用户对 **MCP (Model Context Protocol)** 等外部工具集成的高依赖性。社区期望所有工作模式（特别是自动化/管道模式）都能与交互模式一样，无缝加载并利用MCP服务器，这是实现复杂工作流自动化的关键。

## 开发者关注点

从今日的Bug报告中，可以提炼出开发者最尖锐的痛点：

-   **模式不一致性**：核心痛点在于 `acp` 模式与 `interactive` 模式行为不一致。开发者期望CLI工具在所有模式下都表现出可预测的、统一的行为。`kimi acp` 不加载MCP配置，打破了这种预期，可能导致自动化脚本在无提示的情况下静默失败。
-   **对透明度和稳定性的需求**：尽管 `-v` 参数显示已加载配置文件，但实际功能并未生效，这表明工具在执行逻辑上存在内部缺陷，缺乏足够的日志或错误反馈机制。开发者需要更清晰的错误信息和功能逻辑，以快速定位问题所在。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-06-22

---

## 今日速览
过去 24 小时内，社区围绕 MCP 远程 OAuth 认证（已关闭但讨论热度高）、Go 计划用量 API 需求以及 Ctrl+C 退出冲突等 UX 问题展开激烈讨论；Zen 服务出现 "no provider available" 错误影响部分用户。PR 方面，核心包多项修复合入，包括 ACP 子会话路由、模糊编辑匹配移植、Web 客户端防冻结等，整体工程质量持续提升。

---

## 版本发布
暂无新版本发布（过去 24 小时无 Releases）。

---

## 社区热点 Issues
精选 10 个讨论最活跃或影响面最大的 Issue，附简析与链接。

### 1. Feature request: add MCP remote using OAuth (#988)
- **评论 39 · 👍 95 | 已关闭**
- 核心需求：通过 OAuth 2.1 简化 MCP 服务器安装，用户只需输入 URL 即可触发 OAuth 流程，无需手动搬运密钥。社区认为这将极大提升安全性与配置便捷性。
- https://github.com/anomalyco/opencode/issues/988

### 2. [FEATURE]: Add Go plan usage/balance API endpoint (#16017)
- **评论 20 · 👍 73 | 开放中**
- 希望暴露 Go 订阅计划的用量/余额 API（支持滚动、周、月窗口），类似 Dashboard 显示的数据。点赞数高，说明大量付费用户需要程序化监控额度。
- https://github.com/anomalyco/opencode/issues/16017

### 3. [UX] Ctrl+C should not exit OpenCode (#7957)
- **评论 14 · 👍 37 | 开放中**
- Ctrl+C 作为通用复制快捷键却导致 OpenCode 退出，极易误触。社区呼吁将该热键改为仅终止当前任务，而非退出整个应用。属于高频痛点。
- https://github.com/anomalyco/opencode/issues/7957

### 4. [bug] Black screen on just installed opencode (#10221)
- **评论 31 · 👍 16 | 已关闭**
- 新安装用户启动后仅见黑屏，严重影响首次体验。虽已关闭（原因可能是已定位或修复），但 31 条评论说明影响范围较大。
- https://github.com/anomalyco/opencode/issues/10221

### 5. Add support for cmd+ keybinds on macOS (#653)
- **评论 12 · 👍 42 | 已关闭**
- 仅支持 `ctrl+`、`alt+`、`shift+`，缺少 macOS 用户习惯的 `cmd+`。虽已关闭，但仍是 Mac 用户长期呼吁的基础功能。
- https://github.com/anomalyco/opencode/issues/653

### 6. feat: YOLO Mode — Auto-Approve All Permission Prompts (#11831)
- **评论 9 · 👍 30 | 已关闭**
- 提议增加「YOLO 模式」自动批准工具权限，仅受 `deny` 规则限制。满足高阶用户对高效工作流的追求，社区反响积极。
- https://github.com/anomalyco/opencode/issues/11831

### 7. [FEATURE]: Support more DBMS' for OpenCode state storage (#14212)
- **评论 9 · 👍 20 | 开放中**
- 基于 Drizzle 的会话存储已为支持 PG 等更多数据库打开大门。讨论围绕扩展后端存储选择，适合企业级部署。
- https://github.com/anomalyco/opencode/issues/14212

### 8. When using Claude model (OpenCode Zen) — "no provider available" (#30192)
- **评论 9 · 👍 3 | 开放中**
- 自 5 月 28 日起，OpenCode Zen 的 Claude Opus 4.6 模型报 "no provider available"，其他模型正常。影响面较广，用户焦急跟进。
- https://github.com/anomalyco/opencode/issues/30192

### 9. Zen API endpoints return 404 on CORS preflight (OPTIONS) (#31041)
- **评论 7 · 👍 2 | 开放中**
- 所有 Zen API 端点的 OPTIONS 请求返回 404 HTML 页，导致浏览器客户端被完全阻断。对于 Web 开发者是严重阻塞问题。
- https://github.com/anomalyco/opencode/issues/31041

### 10. Render process freezes/crashes when opening session with large diffs (#33195)
- **评论 4 · 👍 0 | 开放中**
- 桌面版 (Electron) 在打开包含巨大 diff（20KB+ 乱码补丁）的会话时，渲染进程卡死。TUI 不受影响，属于 Electron 端严重稳定性问题。
- https://github.com/anomalyco/opencode/issues/33195

---

## 重要 PR 进展
精选 10 个对功能和架构有实质性影响的 PR，涵盖特色功能、Bug 修复及基础设施改进。

### 1. feat(core): port V1 fuzzy edit matching to V2 core edit tool (#32761)
- 将 V1 的 9 种模糊替换策略移植到 V2 核心编辑工具，大幅提升编辑匹配的鲁棒性。是编辑能力演进的关键合并。
- https://github.com/anomalyco/opencode/pull/32761

### 2. fix(opencode): skip watching $HOME to avoid slow FSEvents exclusion setup (#30209)
- 修复 OpenCode 监视 `$HOME` 时导致 FSEvents 排除配置过慢的问题，显著降低文件系统监听开销。对 macOS 用户性能提升明显。
- https://github.com/anomalyco/opencode/pull/30209

### 3. fix(acp): surface subagent sessions and route child permissions (#32445 / #33293)
- ACP 协议原未跟踪 task 工具生成的子会话，导致子任务权限路由失败。该 PR 注册子会话、修复事件订阅逻辑。新开 #33293 是对相同问题的再次修复/补充。
- https://github.com/anomalyco/opencode/pull/32445
- https://github.com/anomalyco/opencode/pull/33293

### 4. fix(app): prevent web client freeze from delta event bursts and SSE reconnect loops (#33289)
- 解决 Web 客户端在加载大消息历史时因 delta 事件暴增和 SSE 重连循环造成的主线程阻塞，通过节流、取消重复监听等方式提升稳定性。
- https://github.com/anomalyco/opencode/pull/33289

### 5. chore(opencode): code cleanup, formatter consolidation, and perf improvements (#32765)
- 移除死类型、统一格式化配置、优化性能，虽无新功能但持续提升代码质量和维护效率。
- https://github.com/anomalyco/opencode/pull/32765

### 6. fix(tui): add default keybinding for skill selector (#33294)
- 为技能选择器增加默认快捷键（将 `prompt.current` 修改为与命令选择器一致的绑定），方便用户快速切换技能。
- https://github.com/anomalyco/opencode/pull/33294

### 7. fix(tui): correct duration() days/hours calculation past 24h (#33095)
- 修复 TUI 中超过 24 小时的任务持续时间显示错误（天数始终为 0、小时数不对）的问题。
- https://github.com/anomalyco/opencode/pull/33095

### 8. fix(core): ensure parent directory exists in writeIfUnchanged (#33096)
- 在 `writeIfUnchanged` 中补充父目录创建逻辑，避免因目录不存在而写入失败。之前只有 `create` 做了该处理。
- https://github.com/anomalyco/opencode/pull/33096

### 9. refactor(core): simplify integration test fixtures (#33292)
- 将核心测试改为默认使用内存数据库（通过 Bun preload），简化 fixture 并替换内部 mock，提升 CI 效率与可靠性。
- https://github.com/anomalyco/opencode/pull/33292

### 10. feat: mcp-search tool for lazy loading mcp (#12520)
- 为 MCP 提供懒加载搜索工具（基于前期 #8625），仍在更新中。意在减少启动时加载全部 MCP 的开销，提升资源利用效率。
- https://github.com/anomalyco/opencode/pull/12520

---

## 功能需求趋势
从今日全部 Issues 中提炼出社区最关注的四个功能方向：

- **认证与配置简化**：以 #988（MCP OAuth）为代表，社区希望减少手动密钥配置，通过 OAuth 等标准协议实现一键授权。
- **用量与资源监控**：如 #16017（用量 API）、#26184（Token 峰值导致配额耗尽），用户要求更透明的额度使用数据和预警能力。
- **快捷键与 UX 优化**：多处涉及快捷键冲突（#7957 Ctrl+C、#653 cmd+）以及 YOLO 模式等去干扰交互，表明社区对开发效率工具的细节打磨有较高期待。
- **数据库/存储扩展**：基于 Drizzle 的 pg 等多数据库支持 (#14212) 以及状态层灵活性提升，反映了从轻量客户端走向可部署服务端的趋势。

---

## 开发者关注点
汇总近期高反馈的痛点和诉求：

- **桌面端稳定性**：黑屏 (#10221)、大 diff 渲染进程冻结 (#33195)、Web 客户端冻结 (#33289) 等故障让部分用户无法正常使用，稳定性仍是最高优先级。
- **Zen 服务兼容性**：Claude Opus 模型不可用 (#30192)、CORS 预flight 404 (#31041)、Opus 4.7/4.8 列而不可用 (#33229) —— Zen 相关的多起问题说明服务端与新模型集成需要进一步打磨。
- **文件索引与@提及缺陷**：新文件不纳入索引 (#32747)、忽略点开头的文件/文件夹 (#32126)、.ignore 模式不被尊重 (#31801) 等问题持续困扰日常编码工作流。
- **成本控制缺失**：子代理自动调用高价模型未被披露 (#30320)、Token 消耗异常飙升 (#26184)，大型项目用户对成本感知有强烈需求。
- **支付流程阻碍**：意大利等欧洲用户信用卡被拒 (#33264)，国际支付渠道问题影响付费转化。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 #2026-06-22

数据源: `earendil-works/pi` (关联仓库 `badlogic/pi-mono`) | 日报生成时间: 2026-06-22

---

## 今日速览

- **安全加固**：PR #5955 被合并，新增 secret-disclosure scope discipline，防止批量文件操作中误将凭据文件拷贝到目标位置，同时避免模型因暴露规则而卡死。
- **vLLM 与自动压缩修复落地**：PR #5929 和 #5937 分别修复了 vLLM 上下文溢出检测缺失和自动压缩的安全触发时机，两个影响 LLM 使用体验的关键 bug 已合并。
- **社区热点持续发酵**：openai-codex 连接可靠性 (#4945，64 评论) 和本地 LLM 提供者扩展 (#3357，36 👍) 仍是讨论最集中的议题；今日 #5263 获得新更新，围绕会话内模型切换是否应默认临时生效展开讨论。

---

## 社区热点 Issues

以下按关注度选取 10 个最值得关注的 Issue，包含仍在讨论中的 open 项以及刚关闭但影响较大的 bug。

### 1. #4945 [OPEN] openai-codex 连接可靠性问题
- **链接**: [earendil-works/pi Issue #4945](https://github.com/earendil-works/pi/issues/4945)
- **为什么重要**: 用户在使用 `openai-codex` / `gpt-5.5` 时频繁遭遇 TUI 卡死在 `Working...`，只能通过 Esc 恢复。评论多达 **64 条**，👍 **30**，是目前评论数最高的 issue，严重影响日常编码流。已标记 `inprogress`，社区迫切期望根本修复。

### 2. #3357 [OPEN] 官方本地 LLM 提供者扩展
- **链接**: [earendil-works/pi Issue #3357](https://github.com/earendil-works/pi/issues/3357)
- **为什么重要**: 开发者希望 Pi 原生支持 llama.cpp / ollama / LM Studio 等本地推理引擎，通过动态获取模型列表（`{baseUrl}/models`）减少手动配置。该 issue 获得 **36 个 👍**，是所有 issue 中点赞数最高的，反映社区对离线/私有部署的强烈需求。

### 3. #5825 [OPEN] 流式 Markdown 强制滚动到底
- **链接**: [earendil-works/pi Issue #5825](https://github.com/earendil-works/pi/issues/5825)
- **为什么重要**: 当模型输出速度快于阅读速度时，用户向上滚动查看历史，但 Pi 每隔几秒就强制将滚动条拉回底部。评论 **28 条**，大量用户表示该行为破坏阅读连续性。目前已定位到 `clear on shrink` 设置触发的全量重渲染。

### 4. #5916 [OPEN] 支持提供者扩展的模型别名与搜索改进
- **链接**: [earendil-works/pi Issue #5916](https://github.com/earendil-works/pi/issues/5916)
- **为什么重要**: 用户尝试自定义 OpenRouter 模型别名时发现 UI 层面完全无法配置，只能手动编辑 `models.json`。该 issue 提出需要原生支持提供者级别的 model aliases 以及更友好的搜索/过滤界面。评论 **10 条**，讨论如何统一不同提供者的模型命名。

### 5. #5263 [OPEN] 使会话内模型与思维层更改默认临时生效
- **链接**: [earendil-works/pi Issue #5263](https://github.com/earendil-works/pi/issues/5263)
- **为什么重要**: 当前在会话中切换模型或调整 thinking level 会**永久**覆盖全局设置，导致用户意外修改默认值。提案要求默认只影响当前会话，并在 `/settings` 中提供明确的“默认模型”入口。今日有新更新 (2026-06-22)，社区讨论热度上升 (4 👍)。

### 6. #5217 [OPEN] 扩展事件 session_before_compact / session_compact 缺少压缩原因
- **链接**: [earendil-works/pi Issue #5217](https://github.com/earendil-works/pi/issues/5217)
- **为什么重要**: 自动压缩触发时，扩展无法区分是用户执行 `/compact`、context 阈值或 overflow 恢复。虽然 RPC 协议已暴露 `reason`，但公开的 Extension API 尚未同步。该 issue 直接影响了依赖压缩事件进行统计或 UI 更新的扩展开发者。

### 7. #5932 [OPEN] 向扩展上下文暴露 ctx.navigateTree()
- **链接**: [earendil-works/pi Issue #5932](https://github.com/earendil-works/pi/issues/5932)
- **为什么重要**: `navigateTree()` 仅存在于 `ExtensionCommandContext`，普通事件/工具扩展无法调用。作者正在实现自定义 `/goal` 功能，需要此 API 控制文件树导航。该 issue 反映了社区对扩展能力边界的持续拓展诉求。

### 8. #5930 [CLOSED] vLLM 上下文溢出错误未触发自动压缩
- **链接**: [earendil-works/pi Issue #5930](https://github.com/earendil-works/pi/issues/5930)
- **为什么重要**: vLLM 返回的 context length exceeded 错误格式与 `OVERFLOW_PATTERNS` 不匹配，导致自动压缩无法触发，agent 陷入 400 错误死循环。该 bug 影响大量使用 vLLM 的用户，PR #5929 已修复并合并，但仍值得关注后续验证。

### 9. #5778 [CLOSED] pi-agent-core 在流断开或工具死锁时无限挂起
- **链接**: [earendil-works/pi Issue #5778](https://github.com/earendil-works/pi/issues/5778)
- **为什么重要**: 当 LLM 流意外断开或工具 `execute()` 的 Promise 未决议时，agent 循环会永久挂起。评论 **7 条**，被标记为关键漏洞。虽然已关闭，但该问题暴露了 agent 循环缺少超时/容错机制的深层架构短板。

### 10. #5927 [CLOSED] WSL2 支持中危险的工作目录变更
- **链接**: [earendil-works/pi Issue #5927](https://github.com/earendil-works/pi/issues/5927)
- **为什么重要**: 在 WSL2 下运行 Pi，当使用 `\\wsl.localhost\D_Ubuntu\...` 路径时，工作目录被静默修改为 `C:\WINDOWS\`，可能导致文件误操作。虽然已关闭，但该 issue 提醒了跨平台路径处理的安全性，WSL 用户需注意更新。

---

## 重要 PR 进展

过去 24 小时共有 **7 个 PR** 被更新或合并，以下逐一说明。

### 1. #5955 [CLOSED] fix(coding-agent): add secret-disclosure scope discipline to the default system prompt
- **链接**: [earendil-works/pi PR #5955](https://github.com/earendil-works/pi/pull/5955)
- **摘要**: 修复当 agent 执行“复制所有文件”等宽泛任务时误将凭据文件写入目标目录的问题。同时解决仅靠“disclosure rule”带来的二次失败：模型正确识别安全子集后反而卡死。通过修改默认系统提示词，引入 scope discipline，在保留披露能力的前提下避免泄漏和冻结。
- **重要性**: 直接提升安全性，所有用户均可受益。

### 2. #5950 [CLOSED] fix: use OpenRouter's actual cost from API response in footer
- **链接**: [earendil-works/pi PR #5950](https://github.com/earendil-works/pi/pull/5950)
- **摘要**: OpenRouter 每次请求都会返回 `usage.cost` 作为真实美元扣费，但 Pi 过去仅用静态每 token 估算展示费用，导致自定义模型无法显示正确开销。该 PR 使 footer 直接读取 API 返回的实际数值。
- **重要性**: 对使用 OpenRouter 自定义模型的用户提供准确的费用反馈。

### 3. #5942 [CLOSED] fix(coding-agent): add required reason and willRetry to compaction events
- **链接**: [earendil-works/pi PR #5942](https://github.com/earendil-works/pi/pull/5942)
- **摘要**: 为公开 Extension API 的 `SessionBeforeCompactEvent` 和 `SessionCompactEvent` 添加 `reason` ("manual" | "threshold" | "overflow") 和 `willRetry` (boolean) 字段，与 RPC 协议对齐，使扩展可以精确区分压缩触发来源。

### 4. #5941 [CLOSED] fix(coding-agent): add required reason and willRetry to compaction events (same fix, separate branch)
- **链接**: [earendil-works/pi PR #5941](https://github.com/earendil-works/pi/pull/5941)
- **摘要**: 与 #5942 内容相同，来自不同分支的相同修复。两个 PR 均已合并，确保 `compaction` 事件字段一致性。
- **重要性**: 对扩展开发者而言，`reason` 和 `willRetry` 是区分自动压缩与用户手动压缩的关键信息，避免 UI 或日志记录产生误导。

### 5. #5938 [CLOSED] feat(tui): sync d-pi tui components to clients
- **链接**: [earendil-works/pi PR #5938](https://github.com/earendil-works/pi/pull/5938)
- **摘要**: 新增 `defineTuiComponent` 声明机制，允许 d-pi agent 定义自定义 TUI 组件并同步到连接客户端。内置的 `d-pi-message` 渲染器已迁移到该新架构，为多客户端场景下的 UI 一致性打下基础。
- **重要性**: 多客户端架构的关键基础设施，使第三方 agent 也能贡献 TUI 组件。

### 6. #5937 [CLOSED] Harden opt-in auto-compaction at between-turn checkpoint
- **链接**: [earendil-works/pi PR #5937](https://github.com/earendil-works/pi/pull/5937)
- **摘要**: 将自动压缩改为 opt-in（默认关闭），并在每次 assistant turn + tool results 完成后、下一个 provider 请求开始前插入压缩检查点，避免在工具执行中途触发压缩导致数据不一致。用户仍可手动执行 `/compact`。
- **重要性**: 解决了自动压缩在长工具循环中可能破坏上下文完整性的风险，使“安全压缩”成为可能。

### 7. #5929 [CLOSED] fix: add vLLM context overflow error patterns to OVERFLOW_PATTERNS
- **链接**: [earendil-works/pi PR #5929](https://github.com/earendil-works/pi/pull/5929)
- **摘要**: vLLM (v0.8+) 返回的 context length exceeded 错误格式为 `Error: 400 This model's maximum context length is 262144 tokens...`，未被现有 `OVERFLOW_PATTERNS` 匹配，导致自动压缩无法触发。该 PR 增加了对应的正则模式。
- **重要性**: 直接修复 vLLM 用户在长上下文场景下反复 400 错误的死循环。

---

## 功能需求趋势

从近 24 小时的所有 Issues 和 PR 中，可提炼出以下社区最关注的功能方向：

### 🔹 本地模型与提供者灵活性
- 核心需求: 原生支持 llama.cpp / ollama / LM Studio，并实现模型列表动态获取 (#3357)
- 延伸需求: 按提供者配置 model aliases、改进模型选择 UI (#5916)
- 关联: 工具输出截断限制可配置，以适配本地小模型的能力上限 (#5935)

### 🔹 扩展 API 与插件能力
- 常见诉求: 暴露更多 context 方法，如 `navigateTree`、`newSession` (#5932, #5952)
- 事件增强: 为压缩事件提供 `reason` 和 `willRetry`，让扩展能感知压缩触发来源 (#5217, #5942)
- 平台支持: 修复 Bun 对 CJS 包的 ESM import 支持，提升扩展的兼容性 (#5949)

### 🔹 用户体验与交互细节
- 滚动控制: 流式输出时用户手动滚动后不应被强制拉回底部 (#5825)
- 复制粘贴: 修复 TUI 中复制文本时产生多余空格/换行 (#5931)
- IME 输入: 防止后台渲染清除输入法预编辑文字 (#4888)
- 快捷键一致性: 修复双击 Esc 打开 `/tree` 失效 (#5946)

### 🔹 平台与安全性
- WSL2 路径安全: 避免路径映射导致工作目录异常变更 (#5927)
- 凭据泄漏防护: 在系统提示词中加入 secret-disclosure 纪律 (#5955)
- AGENTS.md: 支持以用户消息而非系统提示发送，降低 prompt 注入风险 (#5948)

---

## 开发者关注点

从开发者反馈和 bug 报告中，可以归纳出当前最常见的痛点与高频需求：

### 1️⃣ 连接稳定性仍是头号问题
`openai-codex` 频繁卡死在 `Working...` (#4945) 以及 agent 在流断开时无限挂起 (#5778) 是最影响日常使用的两类问题。社区期待更具韧性的 provider 连接管理与超时机制。

### 2️⃣ 自动压缩行为不够透明与安全
虽然今日 PR #5937 将自动压缩改为 opt-in 并在 check-point 触发，但仍有用户反映压缩后丢失消息、或在 vLLM 溢出场景下不触发 (#5930)。开发者希望压缩逻辑更具可预测性，并提供详细事件日志。

### 3️⃣ 工具执行结果被无警告截断
Bash 和 Read 工具在 `expanded=false` 时只显示 5-10 行，且无法通过配置调整 (#5906, #5935)。对于本地小模型来说，输出截断大幅降低了工具的有效性。社区期待全局或按工具配置截断限制。

### 4️⃣ 模型切换与默认设置易混淆
当前在会话中临时切换模型或 thinking level 会永久修改全局设置，导致用户下次打开 Pi 时行为与预期不符 (#5263)。普遍期望“会话内临时更改”成为默认行为，将“默认模型”移到独立的设置菜单中。

### 5️⃣ 扩展开发者的 API 不完备
多个扩展相关 issue 集中反映 `ExtensionContext` 缺少 `navigateTree`、`newSession` 等方法，且部分事件字段不完整 (#5217, #5932, #5952)。随着 d-pi 生态扩大，完善扩展 API 成为提升开发者体验的关键。

---

*本日报基于 github.com/badlogic/pi-mono 仓库在 2026-06-22 的公开数据自动生成，仅供技术参考。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，作为一名专注于AI开发工具的技术分析师，我已为您整理出 **2026年6月22日** 的 Qwen Code 社区动态日报。数据均基于 GitHub 仓库 `QwenLM/qwen-code` 的真实更新。

---

## 1. 今日速览

1.  **稳定版 v0.18.5 发布**：该版本主要修复了 “Plan Mode” 的 Prompt 问题，并更新了 VSCode 配套扩展的自动发布流程。
2.  **语音功能（Voice）引发社区热潮**：围绕 PR #5502 引入的语音听写功能，社区提交了近10个 Follow-up Issue，涵盖打包、遥测、平台兼容性等深层次问题，语音输入成为当前最热门的迭代方向。
3.  **Agent 稳定性与可控性提升**：针对长任务下工具重复调用的防护机制（#5573）被升级为始终开启，同时后台子代理可恢复功能（#5556）进入 PR 阶段，Agent 核心能力得到显著增强。

## 2. 版本发布

**v0.18.5 (Stable) & v0.18.5-nightly**
- **链接**: [v0.18.5 Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.5) | [v0.18.5-nightly Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.5-nightly.20260622.6bc3f853e)
- **主要内容**:
  - `v0.18.5` 稳定版中，核心修复了必须 Opt-In 才能使用 Plan Mode 的 Prompt 问题（`fix(core): require opt-in for plan mode prompt`）。
  - 在 CI 方面，当有稳定版本发布时，会自动发布 VSCode Companion 扩展。
  - 删除了一个重复的 gitdiff 测试用例。

## 3. 社区热点 Issues

以下挑选了10个在过去24小时内更新且值得关注的 Issue：

1.  **#4888 [BUG] IDEA 插件无法显示提问文本**
    - **链接**: [Issue #4888](https://github.com/QwenLM/qwen-code/issues/4888)
    - **重要性**: IDE 集成核心 Bug。用户在使用 JetBrains IDEA 插件时，Qwen 向用户提问的文本不显示，用户也无法输入答案，直接阻塞交互流程。社区讨论激烈（10条评论），高优先级。
2.  **#5019 [BUG] 长程任务下大量工具重复调用导致会话终止**
    - **链接**: [Issue #5019](https://github.com/QwenLM/qwen-code/issues/5019)
    - **重要性**: 严重稳定性问题。在长时间运行的任务中，模型会不断重复调用相同的工具（相同参数），导致 API 返回错误并终止会话。目前已有对应 PR #5573 正在修复。
3.  **#5540 [Feature] 允许恢复已完成的“后台子代理”**
    - **链接**: [Issue #5540](https://github.com/QwenLM/qwen-code/issues/5540)
    - **重要性**: Agent 工作流的重大诉求。目前的子代理在执行完毕后即为“终端”状态，无法再次发送消息唤醒。该提案允许对已完成的后台代理进行“复活”以继续执行后续指令，对应 PR #5556。
4.  **#5431 [Feature] 为交互式终端增加语音输入模式**
    - **链接**: [Issue #5431](https://github.com/QwenLM/qwen-code/issues/5431)
    - **重要性**: 高关注度功能请求。建议为 TUI 增加可选的语音输入模式，用户建议在复杂任务中通过语音提升输入效率。
5.  **#5424 [Feature] 允许外部注入内容在 TUI 中进行人工审核**
    - **链接**: [Issue #5424](https://github.com/QwenLM/qwen-code/issues/5424)
    - **重要性**: 安全与可控性。目前外部推送的通知或命令会跳过用户的审查直接执行，该提案要求在 Agent 执行前，给予用户在 TUI 中预览和批准注入内容的机会。
6.  **#5555 [BUG] `--resume` 后空格预览 Thinking Block 渲染截断**
    - **链接**: [Issue #5555](https://github.com/QwenLM/qwen-code/issues/5555)
    - **重要性**: 会话恢复体验 Bug。恢复历史会话后，按空格键展开查看模型的“思考”内容时，输出文本被截断，无法完整阅读。
7.  **#5562 [BUG] CLI 输入框换行时背景色渲染不连续**
    - **链接**: [Issue #5562](https://github.com/QwenLM/qwen-code/issues/5562)
    - **重要性**: UI 细节 Bug。在交互界面输入长文本换行时，输入框背景色断裂，影响视觉体验。
8.  **#5559 [Feature] 添加可重放的“假模型”响应用于无需 API Key 的集成测试**
    - **链接**: [Issue #5559](https://github.com/QwenLM/qwen-code/issues/5559)
    - **重要性**: 开发者体验关键改进。社区希望构建一个轻量级的 Fake OpenAI 服务器，使得 PR 在 CI 中运行时无需真实的 API Key 也能跑通端到端测试，降低贡献门槛。对应 PR #5560。
9.  **#5219 [Enhancement] CI 中集成测试仅在发布时运行，导致回归问题难以发现**
    - **链接**: [Issue #5219](https://github.com/QwenLM/qwen-code/issues/5219)
    - **重要性**: CI 流程痛点。E2E 测试仅在每天凌晨的发布流水线中运行，导致 PR 合并时无法暴露回归，直到发布前才发现问题，严重拖慢迭代节奏。
10. **#5575 [BUG] 官网拖拽上传文件会出现多余空格**
    - **链接**: [Issue #5575](https://github.com/QwenLM/qwen-code/issues/5575)
    - **重要性**: 平台交互细节。用户反馈在 `chat.qwen.ai` 官网（Windows + Chrome 环境下）拖动上传文件时，文件内容会被莫名其妙地添加空格，此问题存在大半年仍未解决。

## 4. 重要 PR 进展

以下挑选了10个过去24小时内更新且功能或修复意义重大的 PR：

1.  **#5502 [Feature] 语音听写功能（Voice Dictation）**
    - **链接**: [PR #5502](https://github.com/QwenLM/qwen-code/pull/5502)
    - **内容**: 为本轮社区最瞩目的 PR。支持 `/voice` 命令，实现按住空格键录音或点击开关麦克风，通过本地音频捕获和实时 ASR 进行语音输入。
2.  **#5556 [Feature] 可恢复的后台子代理**
    - **链接**: [PR #5556](https://github.com/QwenLM/qwen-code/pull/5556)
    - **内容**: 实现 Issue #5540 的诉求。允许向已完成的背景子代理发消息以“唤醒”它，并增加了子代理对话历史的 TTL 清理机制，极大增强了多 Agent 协作的灵活性。
3.  **#5557 [Feature] 增加 Artifact 工具发布交互式 HTML 页面**
    - **链接**: [PR #5557](https://github.com/QwenLM/qwen-code/pull/5557)
    - **内容**: 新增了一个实验性的 `artifact` 工具，允许模型将自包含的交互式 HTML 页面发布到本地，并直接通过 `file://` 协议为用户打开，丰富了模型输出的表现形式。
4.  **#5561 [Feature] MCP Server 支持配置热更新**
    - **链接**: [PR #5561](https://github.com/QwenLM/qwen-code/pull/5561)
    - **内容**: 实现 MCP Server 的运行时热重载。当用户在 `settings.json` 中修改 `mcpServers` 配置时，无需重启 Qwen Code 即可实时生效，显著提升扩展使用体验。
5.  **#5573 [Fix] 始终开启相同工具重复调用的防护**
    - **链接**: [PR #5573](https://github.com/QwenLM/qwen-code/pull/5573)
    - **内容**: 针对 Issue #5019 的根本性修复。将连续相同工具调用（同名+相同参数）的检测提升至“始终开启”层级，不再受 Opt-In 开关控制，有效防止模型“死循环”导致的会话中断。
6.  **#5560 [Test] 添加用于无 API Key 集成测试的 Fake OpenAI 服务器**
    - **链接**: [PR #5560](https://github.com/QwenLM/qwen-code/pull/5560)
    - **内容**: 回应 Issue #5559。新增一个轻量级的 Fake OpenAI Chat Completions 服务器，支持 Fixture 响应、流式及非流式、`tool_calls`等，让 PR CI 测试不依赖真实 API Key。
7.  **#5030 [Feature] 无需“继续”消息即可恢复中断的轮次**
    - **链接**: [PR #5030](https://github.com/QwenLM/qwen-code/pull/5030)
    - **内容**: 强大的会话管理改进。Resume 后如果发现上次回答被中断，可以直接从中断处继续输出，而无需像以前一样在历史中插入一个假的 “continue” 用户消息。
8.  **#5126 [Feature] 视觉桥接：为纯文本模型转述图片内容**
    - **链接**: [PR #5126](https://github.com/QwenLM/qwen-code/pull/5126)
    - **内容**: 即“以文生图”。当用户输入的模型不支持视觉时，系统自动将图片发送给一个额外的多模态模型生成文字描述，再将描述送入主模型，大幅提升了工作流的兼容性。
9.  **#5245 [Fix] 修复 Windows 路径问题**
    - **链接**: [PR #5245](https://github.com/QwenLM/qwen-code/pull/5245)
    - **内容**: 针对 Windows 平台的两个关键修复：1）修复 Windows 下波浪号路径 `~\` 未展开的问题；2）修复重连时 Desktop App 中空的原生 Session 显示问题。
10. **#5003 [Feature] TUI 移除工具组边框并折叠已完成的结果**
    - **链接**: [PR #5003](https://github.com/QwenLM/qwen-code/pull/5003)
    - **内容**: 优化终端交互界面。简化了“工具组”的显示样式，去除了圆角边框，并将已经完成的工具调用结果折叠起来，只显示状态头信息，让终端输出更清爽、易读。

## 5. 功能需求趋势

从今日的 Issues 和 PR 中，可以明显看到社区关注度集中在以下几个方向：

1.  **语音交互的全面爆发**：以 PR #5502 为中心，社区不再满足于“能用”，开始关注“好用”。大量 Follow-up Issues 揭示了深层需求：
    - **平台兼容性**：亟需补齐 Windows ARM64、Linux musl/Alpine 等平台的语音原生包（#5580）。
    - **部署与分发**：Standalone 版本需要内置语音原生包（#5582）。
    - **体验优化**：长按模式在终端按键重复延迟高的系统上不够可靠，建议完善 Tap 模式（#5588）。
    - **数据与监控**：需要增加语音功能的遥测事件（#5587）和失败时的静默降级可观测性（#5583）。

2.  **Agent 核心机制的深化**：
    - **持久化与恢复**：后台 Agent 的生命周期管理是关键需求，不仅仅停留在“运行完毕”，而是支持“唤醒”和“复用”。
    - **安全与人工介入**：Agent 的自主性提升的同时，社区对其“破坏力”保持警惕，要求在外部内容注入（如通知、命令）时必须有人工审核环节（#5424）。
    - **防抖与循环**：工具调用的防重复机制从“可选项”变为“必选项”，反映模型长程推理稳定性是生产的刚需。

3.  **集成与扩展性的细节打磨**：
    - **IDE 集成**：JetBrains 插件的基础交互问题（#4888）仍在困扰用户。
    - **MCP 扩展**：MCP Server 的热更新是一个极佳的开发者体验优化。
    - **Extension 机制**：支持从 Archive（.zip/.tar.gz）安装扩展（PR #4909）表明社区对扩展分发途径多样性的渴望。

4.  **开发者体验与 CI/CD 优化**：贡献者社区强烈希望能够在不依赖真实 API Key 和复杂环境的情况下进行测试和贡献（#5559, #5219）。

## 6. 开发者关注点

技术开发者们在高频反馈中表现出以下特点：

1.  **对核心稳定性的“零容忍”**：任何导致会话异常终止（如 #5019 的工具循环）或数据丢失（如 #5518 的 Bundle 恢复路径问题）的 Bug 都会被迅速标记为高优，开发者期望模型在长周期任务中能有可靠的护栏。
2.  **对标同类工具的 Feature Gap**：Issue #3565（请求 `/simplify` 技能）与 PR #5001（添加时间戳）等，直接引用 Claude Code 等竞品的功能，表明核心用户群体技术视野开阔，对 Qwen Code 的期望是达到或超越业界最先进水平。
3.  **跨平台体验一致性是硬门槛**：Windows 路径展开、Linux 下特定 GLIBC 版本兼容性问题、ARM64 架构的原生包缺失等，都是开发者反复提及的痛点（#5245, #5580）。
4.  **高质量的反馈与协作**：开发者提交的 Bug 通常带有详细复现步骤、甚至修复方向的建议（如 `welcome-pr` 标签所示）。社区已经形成了“提 Issue -> 聊方案 -> 提 PR -> 自动化 CI/Coverage”的健康协作闭环，技术氛围浓厚。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是根据 **CodeWhale (原 DeepSeek TUI)** 开源项目 2026-06-22 的 GitHub 动态生成的技术社区日报。

---

# CodeWhale (原 DeepSeek TUI) 社区动态日报 | 2026-06-22

## 📰 今日速览
随着 v0.8.63 版本的发布，项目正式完成品牌切换，官方名称锁定为 **CodeWhale**。与此同时，社区的大部分注意力已转向 v0.8.64 版本的路线图。今日动态核心围绕**安全审查流水线重构**、**频发的 UI 冻结与 Agent 执行可靠性问题**，以及由核心维护者主导的大规模**代码模块拆分工程**，旨在降低未来贡献者的门槛。

---

## 🚢 版本发布

### v0.8.63：CodeWhale 官方正名
- **核心变化：** 此版本为品牌重塑里程碑。项目规范名称、NPM 包、命令行工具及 Release 产物统一为 **CodeWhale**。旧版 `deepseek-tui` 包即日起停止更新并废弃。
- **迁移指南：** 用户需参考项目根目录下的 `docs/REBRAND.md` 完成迁移。
- **安装方式：** `npm install -g codewhale` （具体请参考官方 Install 文档）
- **发布链接：** [v0.8.63 Release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.63)

---

## 🔥 社区热点 Issues (Top 10)

以下是过去 24 小时内更新最活跃且最值得关注的议题：

1.  **[#3368] v0.8.64 安全强化发布跟踪**
    - **重要性：** ⭐⭐⭐⭐⭐ (27条评论)
    - **详情：** 作为 v0.8.64 的安全硬编码门禁追踪器，维护者在此集中管理 CodeQL 发现、安全报告。这是下个版本的 SOTA 安全目标宣告，社区响应热烈。
    - **链接：** [Issue #3368](https://github.com/Hmbown/CodeWhale/issues/3368)

2.  **[#2487] 严重 Bug：Turn Stalled 导致界面假死**
    - **重要性：** ⭐⭐⭐⭐⭐ (17条评论)
    - **详情：** 在 YOLO 模式下频繁出现“未收到完成信号”错误，终端完全卡死且无法通过 `continue` 恢复。这是当前**体验最差的可靠性 Bug**，大量用户提供复现日志。
    - **链接：** [Issue #2487](https://github.com/Hmbown/CodeWhale/issues/2487)

3.  **[#3144] 增加自然语言自动审查策略与推送门禁**
    - **重要性：** ⭐⭐⭐⭐ (12条评论)
    - **详情：** 受 Cursor 启发，提议在无人值守执行和手动批准之间增加中等粒度的审查门禁（Pre-push Review Gate）。反映了社区对 Agent **失控风险**的担忧。
    - **链接：** [Issue #3144](https://github.com/Hmbown/CodeWhale/issues/3144)

4.  **[#3275] Agent 过度干预，陷入自我问答循环**
    - **重要性：** ⭐⭐⭐⭐ (11条评论)
    - **详情：** 被标记为旧版的回归 Bug。Agent 在生成代码时过度膨胀需求，频繁自问自答并直接执行，完全偏离用户原始输入。这对生成式 AI 的可控性提出了挑战。
    - **链接：** [Issue #3275](https://github.com/Hmbown/CodeWhale/issues/3275)

5.  **[#1812] Windows 11 平台下 TUI 完全冻结**
    - **重要性：** ⭐⭐⭐⭐ (8条评论)
    - **详情：** 进程存活但界面定格。开发者利用 WinDbg 捕获了详细的线程状态分析，定位到 `crossterm` 轮询监听器死锁或挂起问题。
    - **链接：** [Issue #1812](https://github.com/Hmbown/CodeWhale/issues/1812)

6.  **[#3289] 自动衍生多个 Sub-Agent 后 UI 冻结**
    - **重要性：** ⭐⭐⭐ (5条评论)
    - **详情：** 在 Plan 模式下改进计划后，进入多 Agent 执行阶段界面再次冻结。与 #2487 类似，指向多线程控制流的问题。
    - **链接：** [Issue #3289](https://github.com/Hmbown/CodeWhale/issues/3289)

7.  **[#3222] 对 MiniMax、Qwen 等模型的推理样式解析异常**
    - **重要性：** ⭐⭐⭐ (6条评论)
    - **详情：** 针对非 OpenAI 标准模型（如 Minimax M3），内联思维链（Thinking Block）解析失败，导致推理内容显示混乱。
    - **链接：** [Issue #3222](https://github.com/Hmbown/CodeWhale/issues/3222)

8.  **[#3364] 增强编辑操作的读前护拦与模糊失败提示**
    - **重要性：** ⭐⭐⭐ (1条评论，最新提出)
    - **详情：** 指出模型在编辑文件时常常“不审题就动刀”，提议在做编辑前强制触发读取（Read-before-edit），并在编辑失败时给出具体行号而非模糊的“编辑失败”。
    - **链接：** [Issue #3364](https://github.com/Hmbown/CodeWhale/issues/3364)

9.  **[#3363] 实现无缝自动上下文压缩**
    - **重要性：** ⭐⭐⭐ (1条评论，最新提出)
    - **详情：** 长对话达到上下文限制后，用户体验十分脆弱。提议在自动压缩时携带前文总结，避免手动压缩带来的断档感。
    - **链接：** [Issue #3363](https://github.com/Hmbown/CodeWhale/issues/3363)

10. **[#3355] 沙箱拦截 Git Worktree 写入操作**
    - **重要性：** ⭐⭐⭐ (3条评论)
    - **详情：** macOS 沙箱限制导致 Git Worktree 工作流被阻断。用户希望在不启用信任模式（trust_mode）时也能正常使用 `git add` 等命令。
    - **链接：** [Issue #3355](https://github.com/Hmbown/CodeWhale/issues/3355)

---

## 🔧 重要 PR 进展 (Top 10)

1.  **[#3373] [Security] v0.8.64 安全强化与发布整合**
    - **详情：** 目前处于 Draft 状态的**旗舰级 PR**，旨在整合所有 v0.8.64 的安全扫描修复、自动审查、编辑护拦、CI 修复及社区贡献。
    - **链接：** [PR #3373](https://github.com/Hmbown/CodeWhale/pull/3373)

2.  **[#3376] [Feat] 添加开发服务器就绪检测工具**
    - **详情：** 社区贡献 `wait_for_dev_server` 工具，用于在 TUI 中检测本地开发服务器（TCP/HTTP）的就绪状态，增强自动化流水线的健壮性，并拒绝外部 Loopback 目标以保证安全。
    - **链接：** [PR #3376](https://github.com/Hmbown/CodeWhale/pull/3376)

3.  **[#3375] [Fix] 优化 Provider 等待时 UI 空闲超时提示**
    - **详情：** 针对 UI 隐私困扰，修复了等待模型响应时，在空闲时间较短（< 60s）时不再显示冗余的倒计。
    - **链接：** [PR #3375](https://github.com/Hmbown/CodeWhale/pull/3375)

4.  **[#3374] [Fix] 修复 CI 夜间构建自动标签问题**
    - **详情：** 解决了 v0.8.64 发布管线中的跨平台构建失败和自动打标签的幂等性缺失问题。
    - **链接：** [PR #3374](https://github.com/Hmbown/CodeWhale/pull/3374)

5.  **[#3372] [Fix] 修复 ACP 服务跨轮次对话历史丢失**
    - **详情：** 关键修复！`AcpSession` 结构体原本未保存历史消息，导致每次调用 `session/prompt` 都被视为新对话，现已完成数据持久化。
    - **链接：** [PR #3372](https://github.com/Hmbown/CodeWhale/pull/3372)

6.  **[#3371] [Fix] 降低侧边栏显示所需的最小宽度**
    - **详情：** 修复了终端在 100 列以下时侧边栏完全不显示的体验问题，降低至更常规的阈值，提升了小屏/分屏用户的体验。
    - **链接：** [PR #3371](https://github.com/Hmbown/CodeWhale/pull/3371)

7.  **[#3370] [Feat] 新增企业微信（WeCom）智能机器人桥接**
    - **详情：** 拓展集成生态，支持企业微信机器人接入，标志着 CodeWhale 开始向团队协作场景延伸。
    - **链接：** [PR #3370](https://github.com/Hmbown/CodeWhale/pull/3370)

8.  **[#3356] [Fix] 允许沙箱中写入 Git Worktree 元数据**
    - **详情：** 直接解决了热点 Issue #3355。通过在沙箱规则中检测 linked-worktree 的 .git 指针文件，放宽了写入限制。
    - **链接：** [PR #3356](https://github.com/Hmbown/CodeWhale/pull/3356)

9.  **[#3332] [Fix/Security] 非 Loopback 绑定应用服务器需强制认证**
    - **详情：** 安全合规修复。修复了在公网暴露后端服务时未强制要求 Token 认证的安全漏洞。
    - **链接：** [PR #3332](https://github.com/Hmbown/CodeWhale/pull/3332)

10. **[#3345] [Refactor] 配置模块大文件拆分**
    - **详情：** 将 4700+ 行的 `config/lib.rs` 中的内联测试模块拆分到独立测试文件中，减少生产代码文件体积，改善构建和合并体验。
    - **链接：** [PR #3345](https://github.com/Hmbown/CodeWhale/pull/3345)

---

## 💡 功能需求趋势

通过对近 24 小时 Issue 的分析，社区最关注的功能方向集中在：

- **安全护栏 (Guardrails)：** 社区不再满足于“全手动”或“全自动”，强烈希望在编辑、执行和推送前设置**中等粒度的审查和卡点**（如 #3144, #3364）。
- **上下文管理 (Context Management)：** 长会话的稳定性是第二大痛点。**自动上下文压缩 (Auto-Compaction)** 成为高频关键词，用户期望彻底告别手动整理上下文碎片。
- **模型供应商泛化 (Provider Agnosticism)：** 除了官方的 DeepSeek，社区对 MiniMax、Qwen、GLM 以及国内云厂商（如百度千帆）的集成需求旺盛，且要求底层推理解析器具备更强的相容性。
- **去中心化 Agent 定义：** 用户希望不再受限于内置角色，期待像 VSCode 插件一样，在项目本地通过 `.codewhale/agents/` 赋予 Agent 自定义身份和行为规范。

---

## 👨‍💻 开发者关注点

除了功能趋势，开发者们在反馈中暴露了以下高频痛点和诉求：

- **Agent 过度自主化：** 模型（尤其是非旗舰模型）在执行命令时**擅自扩大需求范围**，不仅浪费 Token，还往往产生非预期的副作用。这是当前 TUI 模式（如 YOLO）面临的最主要失控风险。
- **配置复杂度高：** 添加一个新模型供应商需要在代码中修改 15-30 个匹配分支。开发者强烈呼吁**重构配置注册中心**，降低二次开发门槛。 (#2608, #3311)
- **Windows 平台体验洼地：** 尽管跨端支持，但 Windows 下的 `crossterm` 轮询和 UI 冻结问题反复出现，相关反馈一直占比较高。
- **模型对工具集的认知负荷：** 非旗舰模型在面对过多的工作追踪工具（Plans, Tasks, Tools）时容易茫然。社区提议引入 **ModelProfile** 描述符，根据不同模型的能力动态裁剪工具集，实现提示词精简。 (#3365, #3366)

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*