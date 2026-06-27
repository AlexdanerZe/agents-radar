# AI CLI 工具社区动态日报 2026-06-27

> 生成时间: 2026-06-27 02:49 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-06-27）

## 1. 生态全景

当前 AI CLI 工具已全面走出“能否生成代码”的初期验证阶段，进入 **稳定性、安全性与企业级可控制性** 的深水区。社区反馈高度一致地集中在 **上下文管理、Agent 行为可预测性、跨平台一致性、计费透明性** 等工程化指标上，而非单纯的功能数量扩充。另一方面，**插件/MCP 生态** 与 **远程/分布式执行** 正在成为各工具的架构标配，差异体现在集成深度与默认策略上。同时，多个工具在“核心功能退化（回归 Bug）”和“配置被静默变更”上的用户信任损耗，已成为当前最紧迫的治理挑战。

## 2. 各工具活跃度对比

| 工具 | 今日热点议题数¹ | 重点 PR 数² | 版本发布 | 社区情绪焦点 |
|------|----------------|-------------|----------|-------------|
| **Claude Code** | 10（精选）+ 多起并发 | 2 | v2.1.195 | 1M 上下文丢失、付费信任崩塌 |
| **OpenAI Codex** | 10（精选） | 10 | rust-v0.142.3 / alpha | 计费暴涨 10–20 倍、Windows 兼容 |
| **Gemini CLI** | 10（精选） | 10 | 无 | Agent 误报成功、Shell 假死 |
| **GitHub Copilot CLI** | 10（精选） | 1（陈旧） | v1.0.66-1 | 剪贴板跨平台崩溃、Memory 泄露 |
| **Kimi Code CLI** | 3 | 2 | 无 | 状态机死锁、Linux 输入 Bug |
| **OpenCode** | 10（精选） | 10 | 无 | 降价传导、工具调用死循环 |
| **Pi** | 10（精选） | 10 | 无 | TUI 强制滚动、回滚缓冲清除 |
| **Qwen Code** | 10（精选） | 10 | nightly v0.19.2 / cua v0.6.8 | Windows OOM 崩溃、安全加固 |
| **DeepSeek TUI** | 10（精选） | 10 | v0.8.59 追踪关闭 | 推理坍缩修复、编辑器冻屏 |

¹ “精选”指各日报从仓库当天活动中筛选出的最具代表性议题数量，非当日全部 Issue。  
² “重点 PR”同样为日报筛选数；Copilot CLI 当日仅 1 条自动 PR 更新，反映团队处于发版后稳定期。

**解读**：OpenAI Codex、Gemini CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI 的 PR 活跃度最高，表明社区贡献和团队迭代并进；Claude Code 和 GitHub Copilot CLI 当日 PR 活动少，但 Issue 热度极高，处于修复/信任修复期；Kimi Code CLI 数据量明显偏低，社区规模或当日活跃度较小。

## 3. 共同关注的功能方向

社区跨工具诉求高度重合，以下为 **至少 3 个工具同时强调** 的五大方向：

### 3.1 上下文隔离与数据安全
- **涉及工具**：Claude Code（#3945 Memory泄露）、Gemini CLI（#27966 大小写绕过敏感路径）、Copilot CLI（#3945/#3946 仓库间 Memory 泄露）、Qwen Code（#5829 路径穿越修复）
- **核心诉求**：AI 必须严格区分不同项目/全局/局部上下文，避免代码建议污染和敏感信息泄露；同时对文件访问做强制白名单与路径校验。

### 3.2 Agent 行为确定性与可审计性
- **涉及工具**：Claude Code（Skill优先级覆盖 #71734）、Gemini CLI（Subagent误报成功 #22323、通用Agent挂起 #21409）、OpenCode（工具调用截断死循环 #18108）、Copilot CLI（子代理日志内联 #3944）
- **核心诉求**：用户不希望 Agent 是“黑盒”，需要精确的状态反馈、可配置的并发/深度上限、以及可审查的工具调用日志。

### 3.3 跨平台与终端一致性
- **涉及工具**：Claude Code（Windows ARM #39636）、Codex（Intel macOS崩溃 #29000、Windows消息发送失败 #29632）、Copilot CLI（Linux剪贴板 #2082、Windows复制失效 #3949）、Kimi Code（Linux双回车 #2477）、Pi（tmux视口跳跃 #6073）、Qwen Code（Windows OOM #5873）
- **核心诉求**：各平台基础交互（剪贴板、输入法、文件拖拽）无差别；Windows 和 Linux 体验应追平 macOS，终端渲染兼容 tmux/回滚。

### 3.4 计费透明与配额治理
- **涉及工具**：Claude Code（Max 计划风控 #5088）、Codex（token 消耗暴涨 10–20x #28879）、OpenCode（DeepSeek降价后调整用量 #28846）、Gemini CLI（递归推理无限消耗 #27738）
- **核心诉求**：需要实时 token 级仪表盘、模型选择确认机制、防止静默切换高价模型或无限递归导致额度迅速耗尽。

### 3.5 长上下文/超长输出的可靠性
- **涉及工具**：Claude Code（1M token 消失 #36351）、Codex（diff 优化）间接相关、Qwen Code（8K 硬上限截断 #5756）、Pi（智能上下文管理）未直接反映但基础 TUI 可见性问题相关
- **核心诉求**：长上下文必须稳定存在且不被更新意外移除；超长输出不应无声截断导致 Agent 反复重试。

## 4. 差异化定位分析

| 工具 | 核心能力侧重 | 目标用户画像 | 技术路线特征 |
|------|-------------|-------------|-------------|
| **Claude Code** | 超长上下文 + 深度 Agent 工作流 | Max 付费开发者、企业团队 | 闭源核心，100K–1M Token 长窗口；Hook/Skill 可扩展；强依赖 Anthropic API |
| **OpenAI Codex** | 远程/分布式执行 + 插件市场 | 追求云原生与生态扩展的开发者 | remote plugin 默认开启；exec-server 事件驱动；强调 Marketplace 治理 |
| **Gemini CLI** | Skills / Sub-agent 灵活编排 | 需要高度自定义 Agent 行为的开发者 | AST 感知文件读取、细粒度组件评估；Caretaker 自动化运维框架 |
| **GitHub Copilot CLI** | GitHub 生态深度绑定 + 子代理管理 | GitHub 重度用户、CI/CD 工程师 | 与 GitHub Models 和 Codespace 集成；`/chronicle` 技能草案审查；强调桌面通知与权限控制 |
| **Kimi Code CLI** | 计划/执行模式二分（Plan & Build） | 早期采用者，偏向结构化对话 | 状态机驱动的交互模式；OpenAI API 兼容；社区规模尚小 |
| **OpenCode** | 多模型/多提供商 + 订阅管理与终端 UI | 自部署与多模型切换的开发者 | 支持 OpenAI/Bedrock/DeepSeek 等；TUI 与桌面版并行；强调费用优化 |
| **Pi** | 高度模块化扩展 + TUI 渲染体验 | 追求极客式终端体验的开发者 | @earendil-works 包体系；Pi Orchestrator 守护进程；嵌入式 SDK 化趋势 |
| **Qwen Code** | 服务端生产就绪（Serve/ACP）+ 安全纵深 | 企业部署与渠道 Agent 开发者 | ACP 可恢复流；多平台二进制 (CUA Driver)；`/loop` 任务持久化 |
| **DeepSeek TUI** | 推理模型兼容 + 消息平台桥接 | DeepSeek 用户及跨 IM 自动化开发者 | 侧重推理内容流式处理；WeCom/Telegram 桥接；持久化权限规则 |

## 5. 社区热度与成熟度

### 高热/成熟阶段
- **Claude Code / OpenAI Codex / GitHub Copilot CLI**：Issue 评论量常超百条（#5088 达 177，#28879 达 175），用户基数大，付费比例高，但回归 Bug 频发已开始反噬信任。
- **Gemini CLI / OpenCode / Qwen Code**：社区贡献活跃，PR 数量多（日更 10+），组件化评估与安全体系已成型，处于快速迭代但尚未完全稳定阶段。
- **Pi / DeepSeek TUI**：社区虽规模略小，但技术讨论深度高，扩展 Or 桥接生态活跃，正从“个人工具”向“平台级运行时”演进。

### 早期/成长阶段
- **Kimi Code CLI**：当日仅 3 个 Issue 和 2 个 PR，社区规模最小，尚处于核心逻辑完善期（状态机 Bug、输入兼容性）。

## 6. 值得关注的趋势信号

1. **模型降价正在重塑订阅逻辑**：DeepSeek V4 Pro 降价 75% 直接引发 OpenCode 用户要求调整用量限制（#28846），未来更多模型 API 价格战将倒逼 CLI 工具做更灵活的费用传导和套餐设计。

2. **Agent 基础可靠性 > 新功能**：Claude Code 1M token 丢失、Codex 计费异常、Gemini Subagent 误报等均是“曾经稳定”功能退化；社区用脚投票，稳定性已成为第一用户留存要素，而非模型能力。

3. **安全从“外围”走向“核心”**：Qwen Code 两天内 4 个安全 PR（#5829 + #5914/#5913/#5911）、Copilot CLI 用户申请 CVE（#3906）、DeepSeek TUI 持久化权限规则 —— 安全不再仅是边界拦截，而是深入 Agent 执行引擎和存储层。

4. **TUI 渲染瓶颈爆发**：Pi 的 #5825（强制滚动）、#6050（回滚清除），Qwen Code 的 #5800（最后一行覆盖）等密集出现，表明终端 UI 已成为用户感知质量的关键战场，增量渲染、平滑滚动、tmux 兼容成为必备能力。

5. **Windows on ARM / Linux Wayland 等小众平台加速觉醒**：Snapdragon X 设备普及叠加 WSL 与 Wayland 场景，社区对原生 ARM64 支持、Wayland 兼容性的呼声从“有更好”变为“必须”。未提前适配的工具将在 12–18 个月内面临显著的生态流失。

6. **计费透明政策将成竞争壁垒**：当前仅有少数工具提供 token 级账单或实时告警。随着 Codex 和 Claude Code 的计费信任危机发酵，率先推出清晰消耗仪表盘、预算警戒线、模型切换授权确认的工具将获得差异化竞争优势。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是根据截至 2026-06-27 的仓库数据生成的 **Claude Code Skills 社区热点分析报告**。

---

### 1. 热门 Skills 排行

基于社区讨论深度、功能切面及技术挑战，以下是最受关注的 8 个 PR：

**1. `#1298` / `#1323`：`skill-creator` 工具链核心修复**
- **功能**：修复 `run_eval.py` 在每次迭代中总是报告 0% 召回率的根本原因（涉及 Windows 进程流读取、触发检测逻辑、并行 Worker 并发问题）。
- **热点**：这是目前社区最大的阻塞点，直接导致 `description-optimization loop` 失效，关联 Issue `#556`（12条评论）。
- **状态**：Open
- **链接**： [#1298](https://github.com/anthropics/skills/pull/1298) / [#1323](https://github.com/anthropics/skills/pull/1323)

**2. `#83`：元技能：质量与安全分析器**
- **功能**：新增两个元技能，从结构与文档、安全性、执行变量、边缘案例等维度评估其他 Skills 的质量。
- **热点**：直接回应了社区对命名空间安全的极大担忧（Issue `#492`，21条评论），是构建生态信任的关键基础设施。
- **状态**：Open
- **链接**：[#83](https://github.com/anthropics/skills/pull/83)

**3. `#723`：`testing-patterns` 综合测试技能**
- **功能**：覆盖 Testing Trophy 模型下的全套测试模式（单元测试、React 组件测试、集成与 E2E 测试）。
- **热点**：开发者对于“标准化、高质量”的测试辅助需求强烈，该技能填补了 Skills 在通用测试领域的空白。
- **状态**：Open
- **链接**：[#723](https://github.com/anthropics/skills/pull/723)

**4. `#514`：`document-typography` 文档排版技能**
- **功能**：专门解决 AI 生成文档中的孤行、寡行和编号错位等排版问题。
- **热点**：解决了生成式文档的通用视觉痛点，属于“高感知度、低技术争议”的优质贡献。
- **状态**：Open
- **链接**：[#514](https://github.com/anthropics/skills/pull/514)

**5. `#360`：`appdeploy` 应用部署技能**
- **功能**：使 Claude 能够直接调用 API 进行全栈 Web 应用的生命周期管理（部署、发布、版本管理）。
- **热点**：代表了社区从“代码生成”向“完整工作流自动化”迈进的强烈意愿。
- **状态**：Open
- **链接**：[#360](https://github.com/anthropics/skills/pull/360)

**6. `#154`：`shodh-memory` 持久记忆技能**
- **功能**：实现跨会话的持久化上下文管理，使 Agent 能记住并调用历史记忆。
- **热点**：围绕 Agent 记忆管理的讨论持续升温（关联 Issue `#1329`），是 Agent 工程化的核心诉求。
- **状态**：Open
- **链接**：[#154](https://github.com/anthropics/skills/pull/154)

**7. `#486`：`ODT` 开放文档格式技能**
- **功能**：支持创建、填充、转换 OpenDocument (.odt, .ods) 文件。
- **热点**：满足了企业用户和开源社区对 LibreOffice / ODF 格式互操作的刚性需求。
- **状态**：Open
- **链接**：[#486](https://github.com/anthropics/skills/pull/486)

**8. `#210`：前端设计技能深度打磨**
- **功能**：优化现有 `frontend-design` 技能的可操作性与指令清晰度，确保每一条指令在单次对话中可执行。
- **热点**：体现了社区不再满足于“新增”，开始对既有 Skills 进行精细化重构以提高质量。
- **状态**：Open
- **链接**：[#210](https://github.com/anthropics/skills/pull/210)

---

### 2. 社区需求趋势

从 Issues 数据来看，社区最期待的新方向集中在以下层面：

- **安全信任与治理**（Issue `#492`，21 条评论）：社区高度警惕社区 Skill 植入恶意代码或伪装官方技能，迫切要求建立签名机制、沙箱运行、以及安全审计标准。
- **跨平台兼容性**（Issue `#556` / `#1061`，12 / 3 条评论）：“零召回率”和“Windows 兼容性崩溃”是最尖锐的受损场景。社区不仅要求新功能，更要求核心工具链在不同 OS 上正常运作。
- **企业级组织管理**（Issue `#228`，14 条评论）：企业用户希望能在组织内像分发软件包一样共享 Skill，而非通过 Slack 传输 `.skill` 文件手动导入。
- **Agent 工程生产力**（Issue `#412`，6 条评论 / Issue `#1329`，6 条评论）：社区不再满足于单个任务的自动化，开始深入探讨 **Agent 治理模式（Governance）** 和 **上下文记忆压缩（Compact Memory）**。

---

### 3. 高潜力待合并 Skills

以下 PR 评论活跃、技术方案相对成熟，极有可能在近期落地合并：

1. **`#1298` / `#1323` 系列**：修复 `run_eval.py` 的缺陷是 **当前社区共识度最高** 的工程任务。一旦测试验证通过，合并优先级最高。
2. **`#723` (`testing-patterns`)**：范围广、内容无争议，且是基于成熟最佳实践的模板型贡献，评审门槛相对较低。
3. **`#514` (`document-typography`)**：问题定义极其精确，代码改动量预期较小，价值可测量，属于“高投资回报率”合并项。
4. **`#83` (质量与安全分析器)**：正好踩中当前安全信任的风口，如果 Anthropic 官方认可该治理模型，会快速推进合并。
5. **`#1099` / `#1050` (Windows 兼容性修复)**：这些是小改动、大价值的修复，直接拉高了生态的包容度，合并可能性很高。

---

### 4. Skills 生态洞察

**一句话洞察：当前社区最集中的诉求是重塑基础开发者体验（DevX）——修复破损的跨平台工具链（`run_eval` 多平台崩溃）并建立清晰的安全信任机制，是推动 Claude Code Skills 从“少数人测试”走向“大规模社区共建”的必须跨越的两道鸿沟。**

---

好的，以下是 2026-06-27 的 Claude Code 社区动态日报。

---

# 2026-06-27 Claude Code 社区动态日报

**数据来源**: github.com/anthropics/claude-code

---

## 1. 今日速览

- Anthropic 发布 **v2.1.195** 补丁，主要修复了 Hook 匹配器子字符串匹配的潜在逻辑错误，并新增了针对全屏模式鼠标滚轮的控制变量。
- 社区最强烈的预警集中在 **1M 上下文窗口大量消失**的回归现象（#36351 / #68287 / #69109 / #69444 多起并发），直接动摇了 Max 付费用户的核心购买动机。
- **支付风控争议**（#5088）以 177 条评论成为今日量级最高的 Issue，同时 Windows on ARM 长时间缺乏原生稳定支持（#39636）持续加剧平台兼容性负面反馈。

## 2. 版本发布：v2.1.195

**更新内容：**

- **新增**：环境变量 `CLAUDE_CODE_DISABLE_MOUSE_CLICKS`。在全屏模式下禁用鼠标点击/拖拽/悬停，仅保留滚轮滚动，适合偏好纯键盘交互或担心误触的开发者。
- **修复**：Hook 标识符（如 `code-reviewer`、`mcp__brave-search`）的匹配逻辑从**子字符串匹配**修正为**精确匹配**，避免因相似命名产生意外错误。

---

## 3. 社区热点 Issues（精选 10 条）

- **#5088** — **账户/付费**：用户购买 Max 5x 计划后账户被立即禁用，涉及金钱与安全双重信任危机。177 条评论 + 58 👍 说明影响面极广。　[链接](https://github.com/anthropics/claude-code/issues/5088)
- **#39636** — **ARM64 / Cowork**：Snapdragon X Plus (ARM64) 上 Cowork 虚拟机内核完全无法启动，每次均返回连接超时。31 条评论持续追踪。　[链接](https://github.com/anthropics/claude-code/issues/39636)
- **#36351** — **长上下文退化**：Max 计划用户在 Desktop 更新后，模型选择器中 1M Context 窗口选项消失。11 👍，严重影响高级用户生产力。　[链接](https://github.com/anthropics/claude-code/issues/36351)
- **#63604** — **模型可靠性**：Opus 4.8 重复生成畸形的 `tool_use` 数据块，导致 Agent 整轮对话响应被丢弃。14 👍，触及 Agent 核心权威。　[链接](https://github.com/anthropics/claude-code/issues/63604)
- **#71729** — **数据丢失**：Windows Desktop 中 `</> Code` 标签页的历史对话在重启后无声消失，且模型本身无法察觉断点。极为严重。　[链接](https://github.com/anthropics/claude-code/issues/71729)
- **#65585** — **第三方 API 回归**：自 v2.1.161 起，使用 Bedrock 等第三方 API 时自动压缩（Auto-compact）失效，回归 Bug。　[链接](https://github.com/anthropics/claude-code/issues/65585)
- **#30407** — **社区治理**：用户质疑几乎所有 Issue 被机器人自动关闭而未经人眼复核，16 条评论反映贡献者对沟通透明度的焦虑。　[链接](https://github.com/anthropics/claude-code/issues/30407)
- **#40173** — **浏览器扩展**：Claude-in-Chrome 扩展在服务端封锁金融/券商域名，合法 RPA 及业务自动化场景受阻。　[链接](https://github.com/anthropics/claude-code/issues/40173)
- **#70684** — **沙箱/网络代理**：启用 Sandbox 后，Git 注入的 SSH 命令无法通过需认证的 SOCKS5 代理，企业 Git 操作全面瘫痪（12 👍）。　[链接](https://github.com/anthropics/claude-code/issues/70684)
- **#71734** — **自定义 Skill 冲突**：内置 `code-review` Skill 优先级意外高于仓库自定义的 Review Skill，导致用户自定义逻辑被覆盖。　[链接](https://github.com/anthropics/claude-code/issues/71734)

---

## 4. 重要 PR 进展

*（根据数据源，过去 24 小时仓库处于低活跃期，共更新了 2 个 PR，以下为详细分析）*

- **#71627 [已开启] — 文档/沙箱**：针对 `settings-bash-sandbox.json` 中的 `allowedDomains` 配置，补充了重要说明——**提示批准的域名仅在当前会话生效**，重启后消失。对需要严格网络策略的企业团队是极有价值的文档补全。　[链接](https://github.com/anthropics/claude-code/pull/71627)
- **#71530 [已关闭] — 维护/同步**：从主分支拉取常规代码合并，不涉及实质功能变更。　[链接](https://github.com/anthropics/claude-code/pull/71530)

---

## 5. 功能需求趋势

- **超长上下文的可靠性**：1M Token 是多起故障（#36351 / #68287 / #69109）的核心焦点，社区要求长上下文不仅存在而且稳定，不可在更新中悄然丢失。
- **Windows ARM 生态补齐**：#39636 / #50674 / #45889 持续表明，Snapdragon X 设备普及后，用户对官方原生 ARM64 支持和性能优化的需求极为迫切。
- **Agent 行为的确定性控制**：自定义 Skill 优先级（#71734）、子 Agent 同步/异步切换（#69691）表明用户不满足于黑盒 Agent，要求具备精确的调度控制。
- **企业网络环境适配**：SOCKS5 代理认证（#70684）、Sandbox 网络策略的持久化管理需求，指向大型企业团队正在规模化落地 Claude Code。
- **零数据丢失与状态持久化**：会话历史丢失（#71729）是不可触碰的红线，社区对状态持久性的要求极为刚性。

---

## 6. 开发者关注点

- **付费信任动摇**：#5088 的高热度和长尾效应说明，支付和风控环节的稳定性直接决定了用户对产品的商业信心。
- **回归 Bug 频发**：1M Context 消失、Auto-Compact 失效、历史记录丢失——这些曾经稳定的核心功能在新版本出现退化，测试覆盖的充分性受到质疑。
- **Agent 核心能力红灯**：Opus 4.8 的 Tool Call 格式异常（#63604）让依赖 Agent 执行复杂任务的开发者产生严重的可靠性顾虑。
- **社区反馈通道焦虑**：#30407 引发的自动关 Issue 讨论，折射出外部贡献者对透明人工交互流程的渴望，而非完全依赖自动化。
- **DevEx 长尾打磨**：VS Code 终端 503 异常（#71683）、SCIM Profile 远程接管不可用（#71731）等细节证明了开发者在实际协同场景中仍频繁遇到摩擦。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-06-27）

---

## 今日速览
- **计费异常成为社区焦点**：多个用户报告 Plus/PRO 计划的 token 消耗突然暴涨 10–20 倍，5 小时预算在 2–3 次对话内耗尽（#28879、#30212），该话题已累积 175 条评论，成为当前最热 issue。
- **远程插件默认开启**：PR #30297 将 remote plugin 特性从实验状态升级为默认开启，标志着 Codex 插件生态向分布式部署迈进。
- **跨平台稳定性修复密集**：关于 Intel macOS 崩溃、Windows sandbox 启动阻塞、WSL Chrome 控制失效等问题的 PR 与 issue 持续更新，平台兼容性仍是开发者的核心痛点。

---

## 版本发布

### rust-v0.142.3（维护性补丁）
- **内容**：纯维护发布，无面向用户变更。
- **Changelog**：https://github.com/openai/codex/compare/rust-v0.142.2...rust-v0.142.3

### rust-v0.143.0-alpha.26（预发布）
- **内容**：alpha 版本，用于测试新特性，未提供详细变更说明。

---

## 社区热点 Issues
（挑选 10 个最值得关注的 Issue，按评论热度排序）

1. **#28879** — `rate-limit cost per token jumped ~10-20x since June 16, draining 5h budget in 2-3 prompts`  
   - **重要性**：计费模型突变，大量 Plus 用户受到影响，社区反应强烈（175 评论、326 👍）。  
   - **链接**：https://github.com/openai/codex/issues/28879

2. **#30224** — `This model is not supported when using X-OpenAI-Internal-Codex-Responses-Lite`  
   - **重要性**：自定义模型用户在使用内部头时被拒绝访问，阻碍了企业/高级用户的自定义部署。  
   - **链接**：https://github.com/openai/codex/issues/30224

3. **#30212** — `5-hour allowance consumed in about 1 hour`  
   - **重要性**：与 #28879 类似，但发生在 Pro（20x）用户上，异常消耗速度惊人。  
   - **链接**：https://github.com/openai/codex/issues/30212

4. **#29000** — `Codex CLI 0.141.0 crashes with SIGTRAP ("trace trap") on Intel macOS`  
   - **重要性**：Intel Mac 用户无法正常启动 CLI，严重影响使用；虽已关闭但标记为 bug，值得关注修复方案。  
   - **链接**：https://github.com/openai/codex/issues/29000

5. **#27536** — `code_sign_clone grows unbounded (62 GB+) across Codex auto-updates`  
   - **重要性**：磁盘空间泄漏严重，长期用户无感知堆积，影响系统稳定性。  
   - **链接**：https://github.com/openai/codex/issues/27536

6. **#18357** — `Upgraded to PRO but "You’re out of Codex messages"`  
   - **重要性**：付费升级后仍被限流，订阅与配额系统的同步 bug 影响用户体验。  
   - **链接**：https://github.com/openai/codex/issues/18357

7. **#26984** — `MCP stdio servers leak pipe fds + orphan child processes → cumulative EMFILE`  
   - **重要性**：MCP 插件模型下的资源泄漏导致文件描述符耗尽，影响长期会话的稳定性。  
   - **链接**：https://github.com/openai/codex/issues/26984

8. **#19529** — `Pressing Enter occasionally sends the same message multiple times`  
   - **重要性**：输入重复问题持久存在，影响日常对话体验，社区提交了日志分析。  
   - **链接**：https://github.com/openai/codex/issues/19529

9. **#30263** — `Prompt textarea becomes disabled after several prompts on macOS`  
   - **重要性**：需要重启 App 才能恢复，属于高频交互阻断 bug。  
   - **链接**：https://github.com/openai/codex/issues/30263

10. **#29632** — `Windows: Unable to send message`  
    - **重要性**：Windows 用户连最基本的发送消息功能都失败，社区反应无法正常使用。  
    - **链接**：https://github.com/openai/codex/issues/29632

---

## 重要 PR 进展
（挑选 10 个重要 PR，覆盖功能、性能、安全与生态）

1. **#30297** — `Enable remote plugins by default`  
   - **概述**：将 remote plugin 从实验特性转为默认启用，生态扩展关键一步。  
   - **链接**：https://github.com/openai/codex/pull/30297

2. **#30327** — `core: persist unmatched call output repairs`  
   - **概述**：修复未匹配调用输出在持久化时绕过 ID 分配的问题，保证对话历史的完整性。  
   - **链接**：https://github.com/openai/codex/pull/30327

3. **#30325** — `Read faster model from safety buffering events`  
   - **概述**：支持通过 WebSocket 读取安全缓冲元数据中的 faster_model 字段，优化第三方流量处理。  
   - **链接**：https://github.com/openai/codex/pull/30325

4. **#29691** — `Enforce marketplace source policy at runtime`  
   - **概述**：在运行时强制执行插件市场来源策略，被阻止的插件自动变为非激活状态，增强安全性。  
   - **链接**：https://github.com/openai/codex/pull/29691

5. **#30315** — `Add generated token auth to app-server WebSockets`  
   - **概述**：为 app-server WebSocket 增加自动生成的 token 认证，提升连接安全性。  
   - **链接**：https://github.com/openai/codex/pull/30315

6. **#30269** — `Gate Rendezvous TCP_NODELAY by signed path`  
   - **概述**：通过签名 URL 控制 TCP_NODELAY 的启用，优化 exec-server 通信延迟。  
   - **链接**：https://github.com/openai/codex/pull/30269

7. **#30291** — `app-server: expose environment info RPC`  
   - **概述**：新增 `environment/info` RPC，允许查询远程环境的 shell 及工作目录元数据。  
   - **链接**：https://github.com/openai/codex/pull/30291

8. **#30286** — `core: overlap diff root discovery with world state`  
   - **概述**：将远程 diff 根发现与世界状态构建并行化，减少冷启动延迟。  
   - **链接**：https://github.com/openai/codex/pull/30286

9. **#30273** — `consume pushed exec-server process events`  
   - **概述**：改用事件流驱动进程状态更新，替代原有轮询模式，提高 exec-server 可靠性。  
   - **链接**：https://github.com/openai/codex/pull/30273

10. **#30281** — `core-skills: cache snapshots before root discovery`  
    - **概述**：将 skill 快照缓存提前到根发现之前，避免远程文件系统的重复元数据探测，优化性能。  
    - **链接**：https://github.com/openai/codex/pull/30281

---

## 功能需求趋势
从过去 24 小时的 Issues 和 PRs 中，社区最关注的方向包括：

- **计费透明与配额控制**：多个 rate‑limit 异常 issue 表明用户亟需清晰的消耗仪表盘和实时告警机制，而非仅靠“预算耗尽”的笼统提示。
- **远程与分布式执行**：remote plugin 默认启用、远程环境信息 RPC、Remote Control 恢复改进等，均指向 Codex 正从本地单机向云‑端混合架构演进。
- **跨平台一致性**：Intel macOS 崩溃、Windows sandbox 启动阻塞、WSL 路径翻译错误、Clipboard 失效等 bug 暴露出非 Apple Silicon / Linux 平台的体验差距。
- **插件生态治理**：市场来源策略执行（#29691）、插件更新后消失（#30270）等问题，说明社区既期待生态丰富，也要求更强的稳定性和安全控制。
- **开发者可观测性**：TRACE 日志被忽略（#30236）、请求 memory CLI 管理命令（#30299）、背景事件 monitor 工具（#29922）等，显示高级用户希望获得更多诊断与运行时控制能力。

---

## 开发者关注点
高频痛点与用户反馈总结：

- **突发性计费异常**：Plus / Pro 用户普遍反映配额消耗速度异常，部分用户“5 小时额度在 1 小时内耗尽”，且无详细 token 级账单，严重影响信任与日常使用。
- **CLI 及 Electron App 稳定性**：Intel macOS SIGTRAP 崩溃、Windows 端无法发送消息、textarea 随机不可用、消息重复发送等问题直接中断工作流。
- **无节制磁盘占用**：`code_sign_clone` 目录累计超 62 GB 而未被清理，自动更新机制存在设计缺陷，长期用户需手动干预。
- **Windows 生态集成短板**：WSL 下 Chrome 控制完全失效、sandbox elevated 模式阻止启动、Bundled 插件更新后路径错误——Windows 用户的体验远逊于 macOS。
- **MCP/插件资源泄漏**：stdio 管道文件描述符泄漏导致 `EMFILE`，长时间运行后所有文件操作失败，对依赖 MCP 的重度用户打击明显。

> 以上日报基于 `github.com/openai/codex` 公开数据生成，所有链接均为原始 GitHub 地址。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-06-27

## 今日速览
今日没有版本发布，但社区讨论与开发活动依然活跃。多个关键 Bug 修复取得进展，尤其是 **Agent 误报成功状态**、**Shell 命令卡死** 以及 **工具路径解析** 等问题得到关注。同时，项目基础架构（Caretaker 自动化服务）持续分裂式推进，安全与体验类 PR 也密集合入。

---

## 社区热点 Issues（10 个）

1. **[Bug] Subagent 达到最大轮次后误报成功**  
   `#22323` — Subagent 明明因 `MAX_TURNS` 中断，却报告 `status: "success"` 和 `Termination Reason: "GOAL"`。隐藏了真实中断原因，影响开发者调试。  
   *8 条评论 / 2 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **[Bug] Generalist Agent 永久挂起**  
   `#21409` — 任何简单操作（如创建文件夹）都会导致 Generalist Agent 挂起，用户被迫取消。社区反应强烈，收到 8 个 👍。  
   *7 条评论 / 8 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **[Bug] Shell 命令执行后卡在 “Waiting input”**  
   `#25166` — 简单 CLI 命令完成后，Agent 仍显示命令活跃并等待输入，严重影响自动化流程。  
   *4 条评论 / 3 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **[Bug] Browser Agent 在 Wayland 环境下失败**  
   `#21983` — Browser subagent 在 Wayland 上无法正常运行，影响 Linux 用户的浏览器自动化能力。  
   *4 条评论 / 1 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

5. **[Epic] AST 感知的文件读取、搜索与代码映射**  
   `#22745` — 探索通过 AST 感知工具减少 Token 消耗、提升读取精度。这是一个影响性能优化的方向，收到 7 条讨论。  
   *7 条评论 / 1 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

6. **[Epic] 组件级评估（Component Level Evaluations）**  
   `#24353` — 在行为评估基础上建立更细粒度的组件测试体系，已生成 76 个测试项。反映团队对质量保障的重视。  
   *7 条评论 / 0 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

7. **[Bug] Auto Memory 对低信号会话无限重试**  
   `#26522` — Auto Memory 只有成功读取 transcript 后才标记已处理，导致低质量会话被反复尝试。  
   *5 条评论 / 0 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

8. **[Bug] 未对 Auto Memory 日志做确定性脱敏**  
   `#26525` — 模型上下文中已包含秘密，脱敏发生在之后；同时日志也可能记录 Skill 内容。隐私风险受关注。  
   *5 条评论 / 0 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/26525)

9. **[Bug] Gemini 不会主动使用 Skills 和 Sub-agents**  
   `#21968` — 用户定义的自定义技能与子代理极少被自动调用，必须显式指示才生效。降低自动化的实用价值。  
   *6 条评论 / 0 👍*  
   [View Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

10. **[Bug] 工具数量超过 128 时返回 400 错误**  
    `#24246` — 当 Agent 拥有超过 128 个工具时调用失败。期望能自动限制范围。影响 MCP 等扩展场景。  
    *3 条评论 / 0 👍*  
    [View Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

---

## 重要 PR 进展（10 个）

1. **修复 `@` 前缀路径解析失败**  
   `#28053` — 当模型传递 `@policies/new-policies.txt` 这类路径时，文件系统工具会报告 “File not found”。该 PR 实现了完整的防御性路径解析。*Size: XL*  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28053)

2. **限制待处理工具响应的体积**  
   `#27870` — 超大工具结果会导致 pending functionResponse 堆积。该 PR 增加了上限，避免 Agent 因此卡住。*已合并*  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/27870)

3. **修复 prompt 模板中美元符号被错误替换**  
   `#28055` — Skill、Sub-agent 描述中的 `$$`、`$'` 等序列在模板替换时被破坏，导致提示词异常。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28055)

4. **限制单次请求中递归推理轮数**  
   `#28164` — 严格限制每次用户请求内递归推理最多 15 轮，防止无限循环消耗本地资源与 API 配额。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28164)

5. **阻止模型思考过程泄漏到对话历史**  
   `#27971` — `Thought Leakage` 导致模型在后续回合中混淆、模仿思维内容。PR 通过剥离 scrubbed history 中的推理文本来解决。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/27971)

6. **强制大小写不敏感的敏感路径拦截与 VS Code HITL**  
   `#27966` — 实现对 `.git`、`.env`、`node_modules` 的严格大小写不敏感阻止，并修复 VS Code 中间人遗漏。*安全加固*  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/27966)

7. **修复 MCP 工具名解析中下划线导致的路由错误**  
   `#28033` — 当 MCP 服务器名称含有下划线时，工具被错误路由。采用最长前缀匹配解决。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28033)

8. **修复 checkpoint 名称移除扩展名的错误**  
   `#28044` — `name.replace('.json', '')` 会移除第一个 `.json` 而非尾部，导致文件名损坏。已修正为只移除末尾。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28044)

9. **修复不可读 `.env` 导致扩展加载失败**  
   `#28059` — 沙箱环境下 `.env` 无权限（EACCES）会使整个扩展系统崩溃。PR 捕获该异常并降级处理。  
   [View PR](https://github.com/google-gemini/gemini-cli/pull/28059)

10. **Caretaker Agent：Egress Cloud Run 服务（自动化 GitHub 操作）**  
    `#28167` — 介绍 caretaker 体系的新组件，接收来自 Triage Worker 的已验证事件并执行自动操作。持续强化项目自运维能力。  
    [View PR](https://github.com/google-gemini/gemini-cli/pull/28167)

---

## 功能需求趋势

- **Agent 自我觉察与工具利用率提升**：社区希望 Gemini CLI 能更主动地调用 Skills、Sub‑agents，并在提示中准确反映自身能力（旗标、热键、运行方式）。代表性 Issue: #21968, #21432。
- **AST‑aware 优化**：多个 Issue 讨论通过抽象语法树实现精确的文件读取、搜索与代码映射，以减少 Token 消耗并提升分析准确度。代表性 Issue: #22745, #22746。
- **Auto Memory 智能化与安全性**：避免无限重试、做好日志脱敏、隔离无效 patch，成为记忆系统迭代重点。代表性 Issue: #26522, #26523, #26525。
- **跨平台与终端兼容性**：Wayland 下 Browser Agent 失败、WSL 下 git branch 不刷新、终端 resize 闪烁等，反映出对更广泛环境的支持需求。
- **组件级评估体系**：从 E2E 行为测试细化到组件级别的评估，有助于提高迭代质量。代表性 Issue: #24353。

---

## 开发者关注点

- **Agent 可靠性与可预测性**：Subagent 误报成功 (`#22323`)、Generalist Agent 永久挂起 (`#21409`)、Shell 假死 (`#25166`) 是最影响日常体验的痛点。
- **配置不生效或绕过**：Browser Agent 忽略 `settings.json` 重写 (`#22267`)，以及 Subagent 在未被配置启用时仍被调用 (`#22093`)，让用户感到失控。
- **扩展与工具链兼容性**：MCP 工具名解析错误 (`#27981`)、`.env` 权限问题 (`#27894`) 以及工具过多时的 400 错误 (`#24246`) 限制了中大型插件的使用。
- **安全性顾虑**：信任对话框显示与实际运行命令不符 (`#27901`)、敏感路径可通过大小写绕过 (`#27966`)、自动记忆未脱敏即进入模型上下文 (`#26525`)，均为用户明确提出的安全缺口。
- **无限循环与资源消耗**：模型思维泄漏 (`#27971`)、递归推理无限制 (`#27738`) 等导致 token 浪费与 CPU 飙升，社区呼吁加入硬性上限。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，这是为您生成的 2026-06-27 GitHub Copilot CLI 社区动态日报。

---

# GitHub Copilot CLI 社区动态日报 | 2026-06-27

## 1. 今日速览
- **新版本 v1.0.66-1 发布**，引入了子代理并发/深度控制、技能草案审核命令以及桌面通知功能，重点在于提升用户对 AI 工作流的管理能力。
- **社区反馈集中在三大痛点**：跨平台剪贴板异常（Linux #2082、Windows #3949）、上下文记忆隔离泄露（#3945、#3946），以及自定义 API 模型适配的严重 Bug（#3954）。
- **PR 活动相对平淡**，过去 24 小时仅有一条旧有自动化 PR 获得更新，团队或处于版本发布后的稳定期。

## 2. 版本发布
**v1.0.66-1**
- **Added**
  - **子代理资源控制**：用户现可在 `/settings` 中配置子代理（subagent）的并发数和深度限制，这对使用量计费用户尤为重要。
  - **技能草案审查**：新增 `/chronicle skills review` 命令，支持审查、接受、拒绝或暂缓 AI 提交的技能草案变更，增强了对自动化流程的审查能力。
  - **桌面通知**：增加了针对注意力提示和空闲会话的桌面通知功能，改善非前台操作时的消息触达。

## 3. 社区热点 Issues (Top 10)
**标准：过去 24 小时更新/创建，按热度、严重性和功能价值综合排序。**

### 🐛 严重 Bug & 回归
1. **[#2082] [Linux] ctrl+shift+c 无法粘贴至剪贴板** (22 评论, 👍 11)
   长期存在的顽固 Bug，影响 Ubuntu 24.04 等主流发行版。社区呼声极高。
   [Issue #2082](https://github.com/github/copilot-cli/issues/2082)

2. **[#3954] explore 工具硬编码 model 为 gpt-5.4-mini，忽略用户自定义配置** (新)
   严重的适配断层。配置了 DeepSeek 等第三方端点的用户使用 `explore` 工具时会直接触发 API 调用失败，完全不可用。
   [Issue #3954](https://github.com/github/copilot-cli/issues/3954)

3. **[#3949] [Windows 11] 复制功能完全失效** (新)
   与 Linux 对应的跨平台 Bug，Copilot 提示“已复制到剪贴板”，但剪贴板实际为空，且没有错误验证。
   [Issue #3949](https://github.com/github/copilot-cli/issues/3949)

4. **[#3955] [macOS] 拖拽文件到 Copilot App 失效 (回归)** (新)
   最新的回归 Bug。从 Finder 拖拽文件到 Prompt 输入框时无任何响应，打断了 macOS 用户的核心交互路径。
   [Issue #3955](https://github.com/github/copilot-cli/issues/3955)

5. **[#3948] web_fetch 工具全部失败** (新)
   所有 `web_fetch` 调用均报 `TypeError: fetch failed`。用户已排除代理和网络问题，疑为 CLI 本身网络栈或最新版本引入的缺陷。
   [Issue #3948](https://github.com/github/copilot-cli/issues/3948)

6. **[#3947] 主题系统在 v1.0.64 中产生回归** (Closed, 👍 1)
   新版本强制覆盖背景色，导致用户无法使用终端宿主本身的背景，高对比度等主题受到影响。虽已关闭，但说明近期 in-renderer 改动风险较高。
   [Issue #3947](https://github.com/github/copilot-cli/issues/3947)

### 🛡️ 上下文与安全
7. **[#3945] Memory 在不同仓库之间泄露** (新)
   在一个新仓库中请求初始化时，Copilot 错误引用了其他仓库的“存储事实”，极可能导致代码建议污染甚至敏感信息泄露。
   [Issue #3945](https://github.com/github/copilot-cli/issues/3945)

8. **[#3946] 自定义指令泄露到仓库分析中** (新)
   用户在 `~/.copilot` 的本地指令被错误地用于分析新仓库，导致生成的配置文件包含不相关的外部规则。
   [Issue #3946](https://github.com/github/copilot-cli/issues/3946)

9. **[#3906] 请求分配 CVE 编号** (新)
   用户已提交安全报告并拿到 GHSA ID，正在推进修复方案。社区关注 CLI 安全漏洞的处理透明度。
   [Issue #3906](https://github.com/github/copilot-cli/issues/3906)

### 💡 功能请求
10. **[#3944] 子代理完整日志未经摘要直接嵌入父会话导出** (新)
    架构性设计问题。当任务使用子代理时，导出日志会内联所有子代理的完整工具调用输出，导致导出文件体积过大且难以阅读。
    [Issue #3944](https://github.com/github/copilot-cli/issues/3944)

*(其他高价值议题： #3940 自定义 Agent skills 字段、#3951 PowerShell 原生支持、#1928 会话暂停功能)*

## 4. 重要 PR 进展
- 过去 24 小时内，该仓库仅更新了 **1 条 PR** ([#570](https://github.com/github/copilot-cli/pull/570))，这是一条由 Copilot Bot 自动化创建的陈旧 PR（2025-11-15），旨在更新 README 中的 macOS 安装说明，目前仍处于 WIP 状态。
- **总结**：当前社区焦点完全集中在 Issues 中的 Bug 修复和新功能讨论上，未出现值得关注的新 PR 合并或关键代码变更。团队可能正集中精力处理积累的缺陷和高优先级的社区反馈。

## 5. 功能需求趋势
- **上下文隔离与安全机制**：`#3945` / `#3946` 将“Memory”和“自定义指令”的隔离问题推至风口浪尖。社区强烈要求 Copilot 必须严格区分不同项目、全局与局部的上下文，避免“幻觉”和数据泄露。
- **模型与服务灵活适配**：`#3954` 暴露了自定义 API 的“硬编码”缺陷。开发者不满足于仅使用 GitHub Models，希望 CLI 能无缝对接 DeepSeek、Ollama 等第三方服务，且所有工具（如 `explore`）必须遵循用户配置。
- **子代理与工作流深度控制**：`v1.0.66-1` 引入的并发控制和 `#3944` / `#3940` 的反馈表明，用户正在从“会用 Agent”走向“精细控制 Agent”，包括限制上下文、控制输出颗粒度。
- **跨平台体验一致性与基础交互**：剪贴板（#2082、#3949）、文件拖拽（#3955）等基础操作在三大平台同时出问题，表明社区对“基础体验”的稳定性和一致性要求极高。

## 6. 开发者关注点
- **痛点：剪贴板基础功能在多平台崩溃**：Linux 上的老 Bug 未解，Windows 11 又出现新 Bug。这是当前用户抱怨最强烈的开发体验障碍。
- **痛点：上下文失控产生的“幽灵建议”**：记忆和指令在不同仓库间泄露，不仅降低了开发效率，更引发了对 AI 生成内容可靠性和隐私安全的信任危机。
- **痛点：新版本带来的“惊喜回归”**：拖拽失效、主题崩溃、模型配置无效——这些本应属于质量门禁回归测试范围的 Bug 频繁流入生产版本，严重消耗了用户的信任。
- **高频需求：为自动化/非交互场景提供更稳定的基础**：`#3942` ( `--acp` 与 `--agent` 冲突) 和 `#3951` (PowerShell 原生支持) 反映了 DevOps 工程师和 Windows 用户希望 Copilot CLI 成为更可靠、可编程的自动化助手，而非仅是一个交互式聊天工具。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-06-27 Kimi Code CLI 社区动态日报。

---

# Kimi Code CLI 社区动态日报 (2026-06-27)

## 1. 今日速览
过去 24 小时内，Kimi CLI 社区无新版本发布，活跃讨论集中在 3 个 Issue 和 2 个 PR。社区关注重点从之前的认证阻塞问题（#2425 已关闭）转向了两个新破的 Bug：**Plan 模式状态机逻辑不一致** 和 **Linux 平台下的终端输入与会话管理缺陷**。PR 方面，一项关键的 **API 参数兼容性修复** 和一个 **文档优化** 正在等待审核合并。

## 2. 版本发布
（本次日报时间段内无新版本发布。）

## 3. 社区热点 Issues
*（本日数据源仅覆盖 3 个更新中的 Issue，以下为逐一深度分析。）*

- **[#2425] [已关闭] 403 认证错误（Kimi For Coding 访问受限）**
    - **重要性:** ⭐⭐⭐⭐⭐
    - **分析:** 该问题自 6 月 4 日提出，历时 22 天关闭，获得 3 个 👍 和 10 条评论。用户在所有请求中均遇到 403 错误，官方回复指出“Kimi For Coding”目前仅对特定 Coding Agent 开放。此问题的关闭可能意味着认证逻辑已修复或边界条件已澄清，对所有用户理解当前工具的使用范围具有重要参考价值。
    - **链接:** MoonshotAI/kimi-cli Issue #2425

- **[#2478] [开放] Plan 模式状态不一致（系统提示与状态机脱节）**
    - **重要性:** ⭐⭐⭐⭐
    - **分析:** 这是一个核心逻辑 Bug。系统提示明确“Plan 模式已激活”，但调用 `ExitPlanMode` 却返回“未在计划模式”。这会导致 Agent 循环或用户操作陷入死锁。由用户 `proccl` 在昨日（6 月 26 日）提交，目前暂无官方回复，属于高优先级需要排查的缺陷。
    - **链接:** MoonshotAI/kimi-cli Issue #2478

- **[#2477] [开放] 双回车键 & `/sessions` 反馈丢失（Linux 平台 QoL 问题）**
    - **重要性:** ⭐⭐⭐
    - **分析:** 运行在 Ubuntu 24.04 LTS 上的 v0.20.0 版本出现按键输入被重复识别（双回车）及会话操作反馈丢失问题。这是一个典型的终端兼容性与输入缓冲缺陷。虽不如状态机崩溃致命，但对 Linux 开发者来说使用体验影响较大。
    - **链接:** MoonshotAI/kimi-cli Issue #2477

## 4. 重要 PR 进展
*（本日数据源仅覆盖 2 个更新中的 PR，以下为详细分析。）*

- **[#2476] [开放] 修复：关闭思考时省略 `reasoning_effort` 参数**
    - **功能/修复:** 当 `thinking` 功能关闭时，不再向 OpenAI 兼容 API 发送 `reasoning_effort: null`，而是完全省略该字段。
    - **技术评价:** 这是对 OpenAI API 规范的精准对齐。许多 LLM 后端在严格模式下会拒绝 `null` 值，此 PR 有效避免了潜在的 API 调用失败，属于高价值的兼容性补丁。
    - **链接:** MoonshotAI/kimi-cli PR #2476

- **[#2287] [开放] 文档：完善 README 开发环境前置条件**
    - **功能/修复:** 在 README 的 Development 章节明确列出了运行 `make prepare` 所需的依赖项。
    - **社区意义:** 解决 Issue #2274，显著降低了开源贡献者的上手成本。该 PR 自 5 月 14 日开放至今，建议项目维护者尽快合并以激励社区贡献。
    - **链接:** MoonshotAI/kimi-cli PR #2287

## 5. 功能需求趋势
基于本日报数据源，社区当前的核心诉求方向可提炼为以下几点：
1. **核心交互稳定性 >> 新功能开发：** #2478 和 #2477 的涌现表明，用户当前最迫切的需求是修复状态机逻辑与终端输入这些基础体验，而非增加新功能。
2. **严格的 API 协议兼容性：** PR #2476 的提出反映出社区开发者对工具底层对接通用 AI 协议（OpenAI API）的规范性和严谨性有极高要求。
3. **Linux 平台精细化适配：** #2477 明确指出 Linux 下的终端兼容性问题，提示开发者在 Mac 之外，需加强对 Linux 开发者群体的使用体验测试。
4. **透明的权限与使用边界说明：** #2425 的长时间讨论表明，社区对“什么功能、哪个版本、谁可以用”这类边界信息有着强烈的透明化需求。

## 6. 开发者关注点
- **高频痛点：**
    - **状态机逻辑缺陷（State Machine Mismatch）：** #2478 中系统提示与实际状态不一致的问题，在 Agent 工作流中极其致命，会导致整个会话逻辑陷入人工无法恢复的死锁状态。
    - **终端输入解析错误（Input Buffering Issues）：** #2477 中的“双回车”问题严重破坏了命令行工具最基础的交互信任感，直接降低开发效率。
- **生态反馈：**
    - **文档完备性：** 开源社区对 README 中的构建前置条件（#2287）非常敏感，清晰的文档是吸纳新贡献者的基石。
    - **API 调试透明度：** #2425 从提出到关闭耗时 22 天，提示开发者需要提供更及时、更清晰的认证失败原因和错误日志，以加速排障流程。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-06-27

## 今日速览

- DeepSeek V4 Pro 永久降价 75% 后，社区强烈要求调整 OpenCode Go 订阅用量限制，**#28846** 以 85 条评论成为昨日最热 Issue。
- 多个影响日常使用的 Bug 正在发酵：Windows 升级后无法启动、工具调用截断导致死循环、以及部分模型空响应等问题备受关注。
- 官方积极修复 UI 交互问题，PR **#34116** 一次性关闭了 6 个与“问题对话框”相关的 Issue，大幅改善桌面端体验。

## 社区热点 Issues

### 1. 调整 Go 用量限制以反映 DeepSeek V4 Pro 降价（#28846）  
[链接](https://github.com/anomalyco/opencode/issues/28846)  
**状态：已关闭**  
社区期望 OpenCode Go 订阅能够传递 DeepSeek V4 Pro 永久降价 75% 的优惠，调整用量限制。**85 条评论、82 个 👍**，说明用户对订阅性价比高度敏感。

### 2. Windows 升级后无法启动（#12598）  
[链接](https://github.com/anomalyco/opencode/issues/12598)  
**状态：已关闭**  
更新到 v1.1.53 后，Windows 10 上 OpenCode 无任何响应。共 **16 条评论**，多个用户确认问题，属于升级阻塞类严重 Bug。

### 3. 为 UI 增加 `reasoning_effort` 参数支持（#450）  
[链接](https://github.com/anomalyco/opencode/issues/450)  
**状态：已关闭**  
已存在一年多的经典需求，要求对支持该参数的模型（如 OpenAI、DeepSeek）提供 UI 调节选项。获得 **26 个 👍**，反映社区对模型深度控制的需求。

### 4. TUI `/model` 选择器不显示所有自定义模型（#6169）  
[链接](https://github.com/anomalyco/opencode/issues/6169)  
**状态：已关闭**  
自定义提供商的模型虽已正确加载，但大量模型未出现在 TUI 列表。**12 条评论**，影响自定义模型用户的工作流。

### 5. 添加加密货币支付选项（#23153）  
[链接](https://github.com/anomalyco/opencode/issues/23153)  
**状态：开放**  
用户请求支持加密资产（如 Monero、ETH）支付 OpenCode Go 订阅。**12 条评论、23 个 👍**，说明社区对支付方式多样化的呼声很高。

### 6. 工具调用被截断后进入不可恢复死循环（#18108）  
[链接](https://github.com/anomalyco/opencode/issues/18108)  
**状态：开放**  
当 LLM 生成的工具调用 JSON 超过 `maxOutputTokens` 时，输出被截断，OpenCode 将其误判为“无效工具调用”且不给模型任何信号，导致会话循环或静默退出。**7 条评论**，属于核心推理逻辑 Bug。

### 7. 插件异步提示与 Web 提示重叠导致会话异常（#28202）  
[链接](https://github.com/anomalyco/opencode/issues/28202)  
**状态：已关闭**  
`opencode web` 中真实提示与异步插件流量重叠，产生重复的 assistant 消息。**7 条评论**，影响 Web UI 的数据持久化正确性。

### 8. OpenCode 处理请求中途停止无返回（#32149）  
[链接](https://github.com/anomalyco/opencode/issues/32149)  
**状态：开放**  
提交新提示后开始“思考”但最终无任何回复。已在多个模型下复现。**6 条评论**，直接影响日常使用。

### 9. Bedrock Mantle 代理返回空成功响应导致任务中断（#31430）  
[链接](https://github.com/anomalyco/opencode/issues/31430)  
**状态：已关闭**  
使用 `openai.gpt-5.5` via Bedrock Mantle 时，代理可能返回空的成功响应，让 OpenCode 在无错误提示下停止。**5 条评论**，涉及云部署稳定性。

### 10. 问题提示框覆盖回复内容且无法关闭/最小化（#28956）  
[链接](https://github.com/anomalyco/opencode/issues/28956)  
**状态：开放**  
AI 使用 `question` 工具时，弹出的对话框覆盖终端 UI，用户无法滚动查看之前回复。**5 条评论**，同类问题还有 #14924、#15353、#32791 等，是桌面端高频 UX 痛点。

## 重要 PR 进展

### 1. 重构核心：分离 Location Node 功能并集成 v2（#34119）  
[链接](https://github.com/anomalyco/opencode/pull/34119)  
**状态：已合并**  
将 LayerNode 图构建移入核心层，并用其建模全局及每个 location 的服务生命周期。为 v2 服务器做准备，属于架构改善。

### 2. TUI：添加子 Agent 选择器（#34135）  
[链接](https://github.com/anomalyco/opencode/pull/34135)  
**状态：开放**  
用子 Agent 选择器替换父级 composer：以扁平列表展示直接子会话，运行中会话优先、最新创建排前，并保持导航可见性。提升 TUI 多会话管理体验。

### 3. TUI：开放 Provider 授权 URL 快捷操作（#34138）  
[链接](https://github.com/anomalyco/opencode/pull/34138)  
**状态：已合并**  
在 V2 授权对话框增加 `o` 快捷键，一键在默认浏览器中打开授权 URL（此前仅有 `c` 复制），简化登录流程。

### 4. 升级 `minimatch` 依赖（#34140）  
[链接](https://github.com/anomalyco/opencode/pull/34140)  
**状态：开放**  
将 `packages/opencode` 中的 `minimatch` 从 `10.0.3` 升级，由本地安全扫描触发，属于依赖维护。

### 5. 桌面版：处理项目路径移动或删除（#34137）  
[链接](https://github.com/anomalyco/opencode/pull/34137)  
**状态：开放**  
当持久化的项目主路径不存在时，不再将新路径重定向至缺失项目；若同一项目 ID 从新路径打开，自动迁移根目录和会话目录并重置上下文 epoch。对多工作区用户至关重要。

### 6. App：暂时隐藏首页会话归档按钮（#34136）  
[链接](https://github.com/anomalyco/opencode/pull/34136)  
**状态：已合并**  
临时隐藏首页会话行的归档操作按钮，保留实现以备后续启用。属于界面微调。

### 7. App：问题对话框 UI 修复与 UX 改进（#34116）  
[链接](https://github.com/anomalyco/opencode/pull/34116)  
**状态：开放**  
**一次关闭 6 个 Issue**：#14924、#32791、#15896、#15353、#19400、#28956。主要改进包括：支持对话框折叠/展开、选项描述文字不截断、可滚动查看对话历史。是昨日最大的 UX 修复 PR。

### 8. App：首页会话列表与滚动条间距调整（#34132）  
[链接](https://github.com/anomalyco/opencode/pull/34132)  
**状态：开放**  
在首页会话列表右侧预留空间，将自定义滚动条置于外槽，避免会话悬浮状态与滚动条重叠。纯 UI 优化。

### 9. Go：筛选模型列表仅显示 OA-Compatible 支持的模型（#33547）  
[链接](https://github.com/anomalyco/opencode/pull/33547)  
**状态：开放**  
`/zen/go/v1/models` 端点之前返回所有 `lite` 目录模型，未检查 Go 端点是否实际支持。现在过滤只返回兼容模型，关闭 #33244 和 #29688。

### 10. 修复 Gemini Schema：无类型 Schema 移除 `required` 字段（#34129）  
[链接](https://github.com/anomalyco/opencode/pull/34129)  
**状态：开放**  
Google 函数调用 API 要求 `required` 只能出现在 `type: object` 的 Schema 中。当 Effect Schema 生成可空联合时，处理代码展开成 anyOf 并删除 type，但残留了 required。此 PR 后处理清除非 object 的 required，避免模型调用失败。

## 功能需求趋势

- **费用与支付灵活化**：DeepSeek V4 Pro 降价引发的用量调整诉求，以及加密货币支付（Monero、ETH 等）的多次请求，显示用户对订阅模式和支付选项多样性的关注持续上升。
- **模型兼容与可控性**：社区希望 OpenCode 更广泛地支持各类新模型（Qwen 3.7、GLM-5.2、GPT-5.5 等），并能在 UI 中控制 `reasoning_effort` 等高级参数。
- **UI/UX 可操作性**：多个 Issue 指向问题对话框遮挡内容、选项描述截断、无法最小化等交互缺陷。用户期望非模态、可折叠的界面组件，以便在执行 Agent 任务时查阅上下文。
- **稳定性与错误恢复**：工具调用截断后的死循环、空响应导致静默中断、自动压缩忽略配置等问题，暴露出核心执行链路在异常处理上的薄弱环节。
- **终端与桌面行为一致**：粘贴本地文件路径、模型选择持久化、会话标题生成逻辑等问题，反映了跨平台交互体验的统一需求。

## 开发者关注点

- **升级破坏性**：部分版本更新导致应用在 Windows 上完全无法启动（#12598），或 Desktop 版本无响应（#34087），严重影响开发者信任。
- **工具调用与 Agent 故障**：截断误分类（#18108）、空回复中止（#32149）、Qwen 3.7 工具调用失败（#33618）等问题暴露出 Agent 执行过程中缺乏有效的反馈与重试机制。
- **配置被忽略**：“自动压缩”功能无法通过配置或环境变量关闭（#32385）；`plan` 模式与 `build` 模式间模型携带错误（#29457），导致用户期望的配置行为与实际不符。
- **UI 信息可读性**：问题对话框截断长描述（#14924、#15353），以及“已修改文件”面板突然不显示（#34131），降低了终端用户对 AI 操作的可视化理解。
- **依赖与兼容性**：Gemini Schema 处理不当（#34129）、OmniRoute 解析 `< /think>` 标签异常（#34126）等问题表明，新模型与 OpenCode 之间的适配还需持续打磨。

---

*日报数据来源：[GitHub - anomalyco/opencode](https://github.com/anomalyco/opencode)*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，这是为您生成的 2026-06-27 Pi 社区动态日报。

# Pi 社区动态日报 | 2026-06-27
**数据来源:** github.com/earendil-works/pi

---

## 1. 今日速览

- **TUI 稳定性攻坚**：持续多日的流式输出滚动跳跃问题 (#5825) 迎来关键修复 PR #6026，同时 Viewport 在 tmux 中的异常跳跃也受到广泛关注。
- **架构向“平台化”演进**：实验性的 `pi-orchestrator` 包被提出，旨在通过守护进程管理多实例生命周期，引发社区对 IDE 集成和复杂工作流支持的想象。
- **扩展生态修复与 Provider 扩展并行**：扩展重载引发的副作用问题 (#6108) 和 RPC 硬编码超时 (#6088) 迅速得到修复；同时 Friendli 和 Bedrock Mantle 等新 Provider 的支持正在积极推进中。

---

## 2. 版本发布

过去 24 小时内没有新版本发布。

---

## 3. 社区热点 Issues

**#1 #5825 [Bug] 流式 Markdown 输出强制滚动到底部**
- **热度**: 33 条评论 | 0 👍
- **概述**: 用户阅读 Agent 输出时，由于 `clear on shrink` 设置，TUI 强制将视口拉回底部，打断阅读流程。这是目前社区反馈最激烈的 UX 问题。
- **链接**: [earendil-works/pi Issue #5825](https://github.com/earendil-works/pi/...)

**#2 #4877 [Bug] 会话文件夹路径冲突**
- **热度**: 19 条评论 | 2 👍
- **概述**: 因会话存储路径的哈希方式存在缺陷，不同路径（如 `/a/b/c/d` 与 `/a-b/c-d`）可能指向同一个文件夹，存在潜在的会话数据混淆风险。
- **链接**: [earendil-works/pi Issue #4877](https://github.com/earendil-works/pi/...)

**#3 #5363 [Feature] 新增 Amazon Bedrock Mantle 提供商支持**
- **热度**: 15 条评论 | 4 👍
- **概述**: 现有 `amazon-bedrock` 提供者仅支持 Converse API，无法兼容 Bedrock Mantle 系列模型（使用 OpenAI 兼容 API）。社区对该企业级特性需求迫切。
- **链接**: [earendil-works/pi Issue #5363](https://github.com/earendil-works/pi/...)

**#4 #6050 [Bug] TUI 全量重绘清除终端回滚缓冲**
- **热度**: 11 条评论 | 0 👍
- **概述**: 交互模式下，状态栏或工作指示器频繁重绘时，会触发核心 TUI 渲染器的破坏性全量重绘，导致终端回滚缓冲被清空，用户丢失聊天历史上下文。
- **链接**: [earendil-works/pi Issue #6050](https://github.com/earendil-works/pi/...)

**#5 #5871 [Bug] Anthropic OAuth Token 检测逻辑硬编码**
- **热度**: 6 条评论 | 0 👍
- **概述**: 代码硬编码了 `sk-ant-oat` 前缀来识别 OAuth Token，导致使用 Claude Code Scope Keys（标准 `sk-ant-api03-` 开头）的企业用户认证失败，缺乏配置化支持。
- **链接**: [earendil-works/pi Issue #5871](https://github.com/earendil-works/pi/...)

**#6 #6108 [Bug] 编译后二进制的扩展重载触发依赖副作用**
- **热度**: 1 条评论 | 0 👍
- **概述**: 在已编译的 Release 二进制文件中，执行 `/reload` 会重新处理扩展的依赖图，导致 `@pierre/diffs` 等模块的副作用（如注册主题）反复执行，可能引发内部崩溃。已被 PR #6109 紧急修复。
- **链接**: [earendil-works/pi Issue #6108](https://github.com/earendil-works/pi/...)

**#7 #6101 [Bug] 嵌入式库模式下的共享扩展运行时污染**
- **热度**: 1 条评论 | 0 👍
- **概述**: 将 `@earendil-works/pi-coding-agent` 作为库嵌入宿主进程时，连续创建多个 `AgentSession` 会导致 `stale ctx` 错误。这对于将 Pi 作为 SDK 使用的场景是致命打击。
- **链接**: [earendil-works/pi Issue #6101](https://github.com/earendil-works/pi/...)

**#8 #6073 [Bug] 在 tmux 中切换工具输出展开时视口跳跃**
- **热度**: 4 条评论 | 0 👍
- **概述**: 特定于 tmux 环境的 Bug。展开/收起工具输出时（Ctrl+O），TUI 主渲染器回退到破坏性全量重绘，导致可见视口跳跃。揭示了核心渲染器在回退机制上的脆弱性。
- **链接**: [earendil-works/pi Issue #6073](https://github.com/earendil-works/pi/...)

**#9 #1391 [Feature] 每 Provider 支持多账户 OAuth 登录**
- **热度**: 2 条评论（长时间未关闭，近期更新）| 0 👍
- **概述**: 延续数月的老 Feature Request。允许 `/login` 为同一个 Provider 存储多个 OAuth 凭据（如区分“工作”和“个人”账号），并支持标签化管理。
- **链接**: [earendil-works/pi Issue #1391](https://github.com/earendil-works/pi/...)

**#10 #6103 [Bug] OpenAI Responses API 将空工具结果错标为图片附件**
- **热度**: 1 条评论 | 0 👍
- **概述**: 当扩展（如 `pi-hashline-edit-pro`）返回空的工具结果时，Pi 错误地将它格式化为 `(see attached image)` 传给模型，导致模型产生困惑。
- **链接**: [earendil-works/pi Issue #6103](https://github.com/earendil-works/pi/...)

---

## 4. 重要 PR 进展

**#1 PR #6109: fix(coding-agent): 扩展重载时保留依赖缓存**
- **作者**: `dmasiero`
- **概要**: 针对 #6108 的紧急修复。确保编译版二进制在 `/reload` 时不会重新评估扩展依赖模块的副作用，保障了扩展生态的稳定性。
- **状态**: 已合并
- **链接**: [earendil-works/pi PR #6109](https://github.com/earendil-works/pi/pull/6109)

**#2 PR #6064: feat(experimental): Pi 编排器 (Pi Orchestrator)**
- **作者**: `cristinaponcela`
- **概要**: 提出实验性 `@earendil-works/pi-orchestrator` 包。通过本地 Unix Socket 实现 IPC 守护进程，提供对多 Pi 实例的声明式生命周期管理。这是 Pi 迈向 IDE 深度集成的重要一步。
- **状态**: 已关闭（仍具高度参考价值）
- **链接**: [earendil-works/pi PR #6064](https://github.com/earendil-works/pi/pull/6064)

**#3 PR #6026: fix(tui): 稳定工作状态行**
- **作者**: `xl0`
- **概要**: 直接关联最热的 Issue #5825。通过稳定工作指示器区域的渲染，减少 TUI 强制滚动的频率。社区正在密切关注此修复的效果。
- **状态**: 开放中
- **链接**: [earendil-works/pi PR #6026](https://github.com/earendil-works/pi/pull/6026)

**#4 PR #6090: feat(ai): 新增 Friendli 提供商**
- **作者**: `Lee-Si-Yoon`
- **概要**: 社区贡献的又一个 OpenAI 兼容 Provider。端点指向 `https://api.friendli.ai/serverless/v1`，默认模型为 `zai-org/GLM-5.2`，极大扩展了 Pi 的模型选择面。
- **状态**: 已合并
- **链接**: [earendil-works/pi PR #6090](https://github.com/earendil-works/pi/pull/6090)

**#5 PR #6087: fix(coding-agent): 移除 RPC 硬编码等待超时**
- **作者**: `mizuikki`
- **概要**: 修复 #6088。将 `RpcClient` 中硬编码的 60s 超时改为可配置选项 `waitTimeout`，解决了与 MCP 扩展配合时长时间运行工具任务失败的问题。
- **状态**: 已合并
- **链接**: [earendil-works/pi PR #6087](https://github.com/earendil-works/pi/pull/6087)

**#6 PR #6092: draft: 托管网络搜索**
- **作者**: `ahxxm`
- **概要**: 一个草稿 PR，尝试在 Agent 循环层面始终开启托管搜索工具，避免模型在需要搜索时因工具缺失而“困惑”。关联长期 Feature #1589。
- **状态**: 已关闭（草稿）
- **链接**: [earendil-works/pi PR #6092](https://github.com/earendil-works/pi/pull/6092)

**#7 PR #6099: fix(ai): 修正 GPT-5.2 模型 Key 命名**
- **作者**: `vamshi9666`
- **概要**: 修复了内置模型定义中的命名错误，将 `gpt-5.2-chat-latest` 更正为 `gpt-5.2-chat`，因为 OpenAI 并未提供 `-latest` 后缀的模型。
- **状态**: 已合并
- **链接**: [earendil-works/pi PR #6099](https://github.com/earendil-works/pi/pull/6099)

---

## 5. 功能需求趋势

- **AI 提供商「泛化」与「精细化」**：不再是单纯的新增 Provider（如 Friendli），社区开始追求对同一 Provider 的精细化兼容（如 Bedrock 的 Mantle 系列、Anthropic 的 Scope Keys 认证）。用户希望 Pi 能像 Kubernetes 一样屏蔽底层 API 差异。
- **TUI 渲染引擎急需重构**：从 #5825、#6050、#6073 等高频 Issue 可以看出，当前依赖全量重绘的 TUI 架构已经达到瓶颈。用户对增量渲染、平滑滚动和 tmux 兼容性提出了硬性要求。
- **Embedded SDK 化是第二增长曲线**：多个关于 `@earendil-works/pi-coding-agent` 库模式的 Bug 被提出。这暗示除了作为独立工具，Pi 正在被严肃地视为一个可嵌入的 Agent 运行时。
- **企业级身份与管理**：多账号 OAuth (#1391)、Scoped API Keys (#6093)、Session 隔离性 (#4877) 等需求频繁出现，说明付费/企业级用户在 GitHub 社区中的活跃度显著提升。
- **工具调用约束放宽**：社区希望 Pi 在 Plan Mode 中能更智能地处理工具缺失情况（#6095），以及在 `turn_end` 回调中允许其他操作（如 Compact），而不是粗暴中断循环（#6096）。

---

## 6. 开发者关注点

- **痛点聚焦：阅读体验被破坏**：首当其冲的是 TUI 强制滚动（#5825）和回滚缓冲清除（#6050）。开发者无法容忍在 Agent 长时间思考/输出时无法向上滚动阅读。这是当前最大的社区情绪爆发点。
- **扩展开发者的“外挂”感**：扩展开发者普遍反映生命周期钩子太脆弱（`turn_end` 调用 Compact 会中断 Tool Loop）、全局状态污染严重（`theme` 未初始化）、以及重载机制不够健壮（副作用重复执行）。
- **Agent Loop 的不可预测性**：`tool execution hangs`、`post-completion non-exit` 等问题频发，即使增加了 `toolTimeoutMs` 配置，仍然无法覆盖所有死锁场景（#5944），开发者对 Agent 循环的鲁棒性缺乏信心。
- **调试困难**：出现通用性错误（如 `value.startsWith is not a function` #5992）时，错误栈信息不够具体，开发者难以定位是哪个第三方扩展或核心组件出现了问题。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-06-27）

**数据来源**：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 1. 今日速览

- **双版本发布**：nightly v0.19.2 新增 `web_fetch` JSON 回退能力；cua-driver-rs v0.6.8 发布预构建全平台二进制，原生支持相对坐标。
- **安全加固持续推进**：阻止路径穿越的 #5829 已合并，同日多枚新 PR（#5914、#5913、#5911）继续覆盖 credential cache 等剩余风险点。
- **社区反馈激烈**：Windows 下工具调用每次新建 PowerShell 直至 OOM 的严重 bug（#5873）已关闭，TUI 卡死僵尸进程（#5083）正在诊断中。

---

## 2. 版本发布

### v0.19.2-nightly.20260627.d93bec905
- **主要变更**：`fix(core): allow web_fetch JSON fallback`（@tt-a1i），允许 `web_fetch` 在目标返回非 JSON 时自动降级处理。
- 其他为版本号及 CI 标准化改动。

### cua-driver-rs v0.6.8
- **macOS**：codesigned + notarized 通用二进制，附 `QwenCuaDriver.app`。
- **Linux / Windows**：提供 x86_64 + arm64 预构建（Linux 最低 glibc 2.31，Windows 未签名）。
- **重点**：启用相对坐标支持，提升 CUA（计算机使用代理）控制精度。

---

## 3. 社区热点 Issues

精选 10 个近期讨论最热烈或影响面最广的问题：

### ① #4175 — Mode B（`qwen serve`）生产就绪路线图
- **链接**：[#4175](https://github.com/QwenLM/qwen-code/issues/4175)
- **重要性**：42 条评论，社区持续追踪近两个月，定义从 Stage 1 到 v0.16 的所有堵点（ACP 命令补全、权限 API、热重载等）。
- **反应**：开放中，长期跟踪 issue，社区贡献者和核心开发者均积极参与。

### ② #5055 — VSIX 被误报为 Trojan:JS/ShaiWorm.DBA!MTB
- **链接**：[#5055](https://github.com/QwenLM/qwen-code/issues/5055)
- **重要性**：安全误报直接影响用户安装决策，7 条评论讨论检测机制与信任链。
- **反应**：已关闭，团队确认误报并推动白名单，但社区仍关注签名与扫描流程。

### ③ #5083 — TUI 卡死，僵尸子进程未被回收
- **链接**：[#5083](https://github.com/QwenLM/qwen-code/issues/5083)
- **重要性**：Linux 用户 TUI 完全冻结，诊断发现 `bash` 子进程长时间处于 `Z`（僵尸）状态，主进程未调用 `waitpid`。
- **反应**：开放中，6 条评论，开发者已定位到子进程回收缺失，需修复进程生命周期管理。

### ④ #4218 — MCP Server "filesystem" 显示已连接但工具不可用
- **链接**：[#4218](https://github.com/QwenLM/qwen-code/issues/4218)
- **重要性**：Windows 下 MCP 标准配置集成失败，模型无法接收 tool definitions，6 条评论反映多云环境复现。
- **反应**：开放中，社区提交了默认配置与自定义服务器的对比信息，等待根因分析。

### ⑤ #5873 — Windows 工具调用每调用一次开一个 PowerShell 直至 OOM
- **链接**：[#5873](https://github.com/QwenLM/qwen-code/issues/5873)
- **重要性**：每次工具调用创建一个新的 `powershell.exe` 且不关闭，直到内存耗尽。社区反馈极其激烈（“逆天BUG”）。
- **反应**：已关闭（5 条评论），问题已复现并修复或纳入紧急处理，体现团队对稳定性崩溃的快速响应。

### ⑥ #5819 — 升级后自动修改 `setting.json` 选用更贵模型
- **链接**：[#5819](https://github.com/QwenLM/qwen-code/issues/5819)
- **重要性**：从 0.18.3 升级到 0.19 后，模型被静默切换为 DeepSeek-4 Pro，导致预存话费用完才被短信预警触发。
- **反应**：开放中，4 条评论，用户质疑配置透明度和升级默认策略，需要更明确的模型选择确认机制。

### ⑦ #5875 — Skill 命令自动补全应支持子串匹配
- **链接**：[#5875](https://github.com/QwenLM/qwen-code/issues/5875)
- **重要性**：当前 `/skill` 补全仅前缀精确匹配，社区提议包含任意子串（如输入 `/store` 匹配 `front-end-store-rules`）。
- **反应**：开放中，4 条评论，属于低门槛 UX 改进，社区活跃度高，期待简单 PR。

### ⑧ #5800 — 回复高于终端时最后一行被覆盖（Static 模式）
- **链接**：[#5800](https://github.com/QwenLM/qwen-code/issues/5800)
- **重要性**：默认 TUI 模式下，回复超过终端高度时最后一行在完成后隐藏，与用户预期相悖。
- **反应**：开放中，4 条评论，已定位为上游 Ink 组件 #973 问题，社区提供 workaround 讨论。

### ⑨ #5897 — 启动时 `unknown format "uint64" ignored in schema` 警告刷屏
- **链接**：[#5897](https://github.com/QwenLM/qwen-code/issues/5897)
- **重要性**：每次启动打印数十行 `unknown format "uint64"` 警告，干扰正常日志阅读，影响专业使用体验。
- **反应**：开放仅 1 天已有 3 条评论，同日 PR #5915 提交修复，社区对快速修复表示期待。

### ⑩ #5909 — 加固剩余 slug-to-path 调用点与无效 slug 诊断
- **链接**：[#5909](https://github.com/QwenLM/qwen-code/issues/5909)
- **重要性**：继 #5829 修复核心路径穿越后，识别出 `getCredentialCachePath` 等更多未加固路径，提出防御纵深需求。
- **反应**：开放中，3 条评论，属于安全持续改进，配套 PR #5914 / #5911 已发出，社区安全研究员参与讨论。

---

## 4. 重要 PR 进展

精选 10 个涵盖新功能、核心修复与安全加固的 PR：

### ① #5852 — feat(daemon,sdk): 可恢复 ACP 会话流 + 可选 SDK 传输导出
- **链接**：[#5852](https://github.com/QwenLM/qwen-code/pull/5852)
- **内容**：为 `/acp` Streamable-HTTP 流添加 SSE `id:` 字段，支持 `Last-Event-ID` 重连，配合新的事件回放引擎实现断线续传；SDK 同时导出多种传输协议。显著提升 ACP 可靠性。

### ② #5869 — feat(web-shell): 流式代码块语法高亮 + fence 语言别名修复
- **链接**：[#5869](https://github.com/QwenLM/qwen-code/pull/5869)
- **内容**：消除流式渲染时代码块闪烁，改为增量重新高亮；同时修复了语言别名（如 `js` → `javascript` 映射）的支持。

### ③ #5890 — feat(loop): 注入 `.qwen/loop.md` 持久化任务文件
- **链接**：[#5890](https://github.com/QwenLM/qwen-code/pull/5890)
- **内容**：`/loop` 可在触发时重新读取 `.qwen/loop.md` 作为任务指令，用户可编辑此文件而不需重启循环。引入 sentinel 声明模式以兼容老配置文件。

### ④ #5915 — fix(core): 压制未知 schema 格式警告
- **链接**：[#5915](https://github.com/QwenLM/qwen-code/pull/5915)
- **内容**：在工具 schema 宽松校验器中过滤 Ajv 的 `unknown format "..." ignored` 警告，保留标准格式（如 `date`）验证。直接解决 #5897。

### ⑤ #5821 — fix(cli): 对本地 OpenAI 后端默认关闭跟进建议
- **链接**：[#5821](https://github.com/QwenLM/qwen-code/pull/5821)
- **内容**：当后端 API 为 `localhost` / `127.0.0.1` 等回环地址时，`ui.enableFollowupSuggestions` 默认为 `false`；用户显式开启仍可覆盖。避免本地部署场景产生额外 token 消耗。

### ⑥ #5778 — feat(cli): `/model --vision` 支持备用视觉模型
- **链接**：[#5778](https://github.com/QwenLM/qwen-code/pull/5778)
- **内容**：新增 `/model --vision <model-id>` 命令及交互选择器，配置一份视觉模型用于主模型无图像能力时切换。镜像 `/model --fast` 的 UX 与运行检查组。

### ⑦ #5847 — feat(serve): 运行时上下文注入（per-turn system-reminder）
- **链接**：[#5847](https://github.com/QwenLM/qwen-code/pull/5847)
- **内容**：提供每会话的 Key-Value RuntimeContext 存储，外部调用方（daemon API、SDK）可注入动态上下文。每轮 `UserQuery`/`Cron` 时作为 `<system-reminder>` 插入，实现静态系统消息之上的可变层。

### ⑧ #5879 — feat(web-shell): /mcp 对话框浏览 MCP 服务器资源
- **链接**：[#5879](https://github.com/QwenLM/qwen-code/pull/5879)
- **内容**：将终端 TUI 中的 MCP 资源浏览器能力移植到 Web Shell 的 `/mcp` 对话框。每台服务器显示资源/提示计数，展开可查看具体资源列表（再展开内容）。补全前后端功能一致。

### ⑨ #5829 — fix(desktop): 在删除前拒绝不安全 source slug（已合并）
- **链接**：[#5829](https://github.com/QwenLM/qwen-code/pull/5829)
- **内容**：核心安全修复 — 在桌面端源（source）删除路径中，对 `sourceSlug` 进行严格校验，阻止路径穿越尝试。已合并入主线，是今日安全系列的基础。

### ⑩ #5912 — fix(daemon): 跨连接解析 ACP 许可投票
- **链接**：[#5912](https://github.com/QwenLM/qwen-code/pull/5912)
- **内容**：修复 ACP-over-HTTP 许可投票只能由同连接流式响应的局限。通过给请求 ID 附加连接命名空间、让 dispatcher 按需查找待处理许可，实现跨连接投票正常完成。

---

## 5. 功能需求趋势

从近期 Issue 和 PR 中可提取出社区最关注的几个方向：

### 🔸 服务端生产就绪（Serve & ACP）
- #4175 定义从 “functional runnable” 到 “production-ready” 的剩余工作；ACP 协议正通过 #5852（可恢复流）、#5677（cd/权限/LSP 支持）、#5912（跨连接投票）等补全。

### 🔸 MCP 生态深度集成
- 用户频繁报告 MCP 连接成功但工具不生效（#4218）；PR 侧持续加码：资源浏览器（#5879）、filesystem 诊断、LSP 集成纳入 ACP。

### 🔸 安全防御纵深
- 路径穿越、未授权凭据访问是近期焦点：#5829 与 #5909 构成源头拦截→剩余调用点加固的完整链条；#5055 误报也推动签名流程改善。

### 🔸 CLI 交互体验精细化
- 自动补全子串匹配（#5875）、流式语法高亮（#5869）、虚拟终端历史默认开启（#5738）、长输出覆盖修复（#5800）等表明社区对终端内“手感”要求越来越高。

### 🔸 渠道 Agent 与后台自动化
- “qwen tag” 多人共享 Agent（#5887）、Telegram 命令菜单对齐（#5907）、QQ bot 流式改进（#5901）体现多端扩展需求；`/loop` 的任务文件持久化（#5890）使重复作业可维护化。

---

## 6. 开发者关注点

### ⚠️ Windows 平台稳定性仍是痛点
- **每次工具调用开新 PowerShell 直至 OOM**（#5873）反映进程池或 shell 复用机制缺失；MCP filesystem 连接后工具不可用（#4218）令 Windows 用户集成受阻。社区反馈措辞激烈，期待彻底修复。

### ⚠️ 配置变更的透明性与信任
- **升级后模型被静默切换至更高单价**（#5819）伤害用户信任；`POST /workspace/settings` 接受负值 `cleanupPeriodDays`（#5905）显示参数校验仍需加强。用户呼吁 **升级前 diff 提示、模型选择双重确认**。

### ⚠️ 默认行为与输出截断造成的隐形浪费
- **8K 输出硬上限截断大文件写入**（#5756）导致模型反复重试失败；本地后端默认开启 Follow-up Suggestions 无谓消耗 token（#5821）。默认参数需要区分云端与本地场景，并提供更好的超限提示。

### ⚠️ UI/UX 琐碎但频繁的干扰
- 僵尸进程致 TUI 冻结（#5083）、长回复被覆盖（#5800）、schema 警告刷屏（#5897）等 Bug 虽不致命，但频繁打断工作流，社区期待更稳健的渲染层与进程管理。

---

*本期日报基于 github.com/QwenLM/qwen-code 在 2026-06-27 00:00~24:00（UTC）间的公开活动生成，仅代表社区讨论，不构成官方发布计划。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报｜2026-06-27

## 今日速览

今天社区的核心主线是**模型提供商扩展**与**生态基础设施完善**。OpenModel 作为一等提供商正式完成合并，同时 WeCom（企业微信）桥接的部署与安全文档趋于完整。在稳定性方面，影响广泛的「思维坍缩」（Thinking Collapse）BUG 被彻底根除，但编辑器突发冻屏的新问题引发了社区的及时警觉。此外，多个依赖项（Rusqlite、SHA2、Rustls）的持续更新也反映了项目在工程健壮性上的高频迭代。

---

## 版本发布

过去 24 小时内无正式版本发布，但 `v0.8.59` 的发布追踪（Issue `#3063`）已关闭，该版本包含了 TUI 鼠标输入泄漏修复及维护者 PR 队列清理，标志着进入稳定化收尾阶段。

---

## 社区热点 Issues（Top 10）

### 1. [#3063 v0.8.59 发布追踪](https://github.com/Hmbown/CodeWhale/issues/3063) [CLOSED]
- **重要性**：v0.8.58 后的首个稳定化版本，重点修复 macOS 上 TUI 鼠标事件泄漏。
- **社区反应**：11 条评论，涵盖与 v0.8.58 的时间戳交叉验证。

### 2. [#861 思维坍缩（Thinking Collapse）](https://github.com/Hmbown/CodeWhale/issues/861) [CLOSED]
- **重要性**：DeepSeek 推理模型用户的首位社区 BUG。推理块出现假死、静默截断或完全丢失 `reasoning_content`。
- **社区反应**：8条评论，该问题的关闭对全系列推理模型的稳定性是里程碑式的提升。

### 3. [#3582 安装脚本返回 HTML 而非 Shell 脚本](https://github.com/Hmbown/CodeWhale/issues/3582) [CLOSED]
- **重要性**：`curl -fsSL https://codewhale.net/install.sh | sh` 直接崩溃，阻塞所有新用户的上手路径。
- **社区反应**：4条评论，修复后部署流程恢复正常。

### 4. [#3657 编辑器冻结并导致 CodeWhale 崩溃](https://github.com/Hmbown/CodeWhale/issues/3657) [OPEN]
- **重要性**：键入 `d` 进入草稿模式后按 `Ctrl-O` 打开编辑器，程序完全锁死，必须强制杀死进程。
- **社区反应**：3条评论，紧急 BUG，开发者表示对手头工作影响极大。

### 5. [#1186 类型化持久权限规则](https://github.com/Hmbown/CodeWhale/issues/1186) [OPEN]
- **重要性**：v0.9.0 规划中的执行策略层增强，支持按工具名、命令前缀、路径模式配置 `allow` / `deny` / `ask`。
- **社区反应**：10条评论，社区对精细化安全策略的需求非常高。

### 6. [#2870 命令边界重构（EPIC）](https://github.com/Hmbown/CodeWhale/issues/2870) [OPEN]
- **重要性**：跟踪大型架构重构 `#2791`，分阶段落地以减少合并风险，涉及 TUI 核心解析逻辑。
- **社区反应**：7条评论，开发者关注拆分策略以避免回归。

### 7. [#3490 v0.8.71 遗留代码清点](https://github.com/Hmbown/CodeWhale/issues/3490) [OPEN]
- **重要性**：在 v0.9.0 全面展开前，系统清理 `allow(dead_code)` 和过期的 TODO 注释。
- **社区反应**：4条评论，维护者强调这直接关系到未来工作流的代码健壮性。

### 8. [#3537 替换硬编码的本地化文件](https://github.com/Hmbown/CodeWhale/issues/3537) [CLOSED]
- **重要性**：`localization.rs` 已超 5000 行，严重拖慢编译与翻译链路，社区推动引入专业 i18n 库。
- **社区反应**：3条评论，国际化贡献者普遍支持该重构。

### 9. [#2612 输入法合成阶段占位符显示 BUG](https://github.com/Hmbown/CodeWhale/issues/2612) [CLOSED]
- **重要性**：拼音/假名/谚文输入时 Committed 为空，Placeholder 遮挡预编辑界面，CJK 用户不可用。
- **社区反应**：该修复标志着项目对全球输入法兼容性的重视。

### 10. [#2953 精简默认 Prompt 以对齐 Codex 输入 Token](https://github.com/Hmbown/CodeWhale/issues/2953) [OPEN]
- **重要性**：CodeWhale 基础指令体积远大于 Codex，直接影响 API 成本与上下文效率。
- **社区反应**：3条评论，长期优化项，v0.8.66 追踪中。

---

## 重要 PR 进展（Top 10）

### 1. [#3677 feat(provider): 添加 OpenModel 支持](https://github.com/Hmbown/CodeWhale/pull/3677) [CLOSED]
- 核心合并：将 OpenModel 作为一等 Anthropic Messages 提供商加入 Provider 注册表、TUI 配置及 CLI 选择器。
- 默认路由 `deepseek-v4-flash`，完全保留社区贡献者 `@noaft` 的作者信息。

### 2. [#3585 OpenModel 提供商支持（原始 PR）](https://github.com/Hmbown/CodeWhale/pull/3585) [OPEN]
- 社区贡献端：`@noaft` 提交的初始实现，包含 Provider 注册表、CLI 镜像列表、TUI 配置与选择器。
- 后续被 `#3677` 收割采纳。

### 3. [#3678 新增 WeCom 桥接部署指南](https://github.com/Hmbown/CodeWhale/pull/3678) [CLOSED]
- 从 `#3640` 中提取了可用的 Deploy/Security 文档，并修复了文档准确性阻塞项。
- 覆盖 `codewhale serve --http`、`npm run start/check/test` 等内容。

### 4. [#3640 WeCom 桥接部署指南与安全章节](https://github.com/Hmbown/CodeWhale/pull/3640) [CLOSED]
- 提供完整的部署文档（DEPLOYMENT.md）与安全边界说明（SECURITY.md）。
- 关联 `#2967`（Telegram/WeCom 桥接韧性强化）。

### 5. [#3575 feat(memory): 通过 MCP 接入 Moraine 记忆系统](https://github.com/Hmbown/CodeWhale/pull/3575) [OPEN]
- 将 `moraine-mcp` 作为默认 MCP 模板，Agent 借此获得 `search_sessions`、`file_attention` 等长期记忆检索工具。
- 同时新增 `[memory] moraine_fallback` 配置门控，淘汰旧的 Push/Inject 机制。

### 6. [#3679 CI: 重试 OHOS 依赖探测](https://github.com/Hmbown/CodeWhale/pull/3679) [CLOSED]
- 在版本漂移检查中对 `cargo tree` 加入重试逻辑，避免网络抖动导致误报故障。
- 保留最终非零退出码以捕捉真实依赖问题。

### 7. [#3676 fix(provider-links): 更新降级时的文档 URL](https://github.com/Hmbown/CodeWhale/pull/3676) [CLOSED]
- 将 `The provider docs aren't loaded` 页面的通用降级 URL 从过期页面指向最新 CodeWhale 文档。
- 新增千帆（Qianfan）专有文档链接与回归测试。

### 8. [#3674 refactor(runtime-api): 抽离 Auth 助手函数](https://github.com/Hmbown/CodeWhale/pull/3674) [CLOSED]
- 将 Bearer Token、Runtime Token Header、移动端 Cookie 流等认证逻辑移入独立的 `runtime_api/auth.rs` 模块。
- 纯净重构，不改变行为。

### 9. [#3675 build(deps): 升级 rusqlite 至 0.39.0](https://github.com/Hmbown/CodeWhale/pull/3675) [CLOSED]
- 跳过了 Dependabot 提交的 0.40.1 版本（因 `libsqlite3-sys 0.38.1` 在本地 Stable 下存在 `cfg_select!` 宏不稳定问题）。
- 手动验证了本地构建兼容性后合并。

### 10. [#3673 fix(hash): 支持 SHA2 0.11 Digest Hex 格式化](https://github.com/Hmbown/CodeWhale/pull/3673) [CLOSED]
- 承载 Dependabot 的 `sha2` 0.11 升级，替换直接的 `LowerHex` 格式化为显式 Byte-to-Hex 工具函数。
- 确保 CLI、TUI、Fleet、RLM、WhaleFlow 等各模块的哈希输出字符串保持稳定。

---

## 功能需求趋势

从过去 24 小时的 Issue 与 PR 中可以提炼出以下五大趋势：

1. **模型提供商走向多极化**：OpenModel 的加入标志着社区不再满足于单一 API，追求路由、价格与模型多样性的精细控制。

2. **Agent 记忆由「无状态」迈向「持久化」**：Moraine-MCP 的集成表明长期记忆、跨会话搜索正成为 Agent 能力的核心诉求，不再是可选的锦上添花。

3. **安全策略精细化**：持久化权限规则（`#1186`）与主 Prompt 暴露（`#3638`）表明用户正在将 TUI 投入更多生产级和自定义场景，需要更细粒度的安全执行边界。

4. **生态连接器持续爆发**：WeCom 桥接文档的完善、Telegram 桥接韧性强化（`#2967`）表明团队将消息平台集成视为用户留存的关键基础设施。

5. **Token 经济性的极致追求**：持续对标 Codex CLI 的输入/输出 Token 优化（`#2953`, `#2956`, `#2957`）说明社区对 API 成本极其敏感，Prompt 精简与结果压缩是长期主旋律。

---

## 开发者关注点

- **稳定性为最优先痛点**：编辑器冻屏（`#3657`）和思维坍缩（`#861`）占据了最多的情绪带宽，核心推理流程的稳定性是开发工具的生命线。
- **文档与上手引导至关重要**：安装脚本返回 HTML（`#3582`）和文档链接失效（`#3680`, `#3621`）直接导致新用户转化失败，亦是社区贡献者最踊跃活跃的领域。
- **代码架构健康度受瞩目**：API 认证重构（`#3674`）、命令边界重构（`#2870`）、Dead Code 清点（`#3490`）反映了项目在高速迭代中持续控制技术债务的决心。
- **依赖管理永远不简单**：Dependabot 批量发起更新，但维护者必须在升级便利性与本地 Stable 构建兼容性之间谨慎取舍（如 `#3675` 降级 rusqlite 版本）。
- **国际化进入深水区**：从 IME 输入法兼容（`#2612`）到 i18n 库重构（`#3537`），项目正从一个中文开发者工具转变为面向全球全语言用户群体的平台级应用。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*