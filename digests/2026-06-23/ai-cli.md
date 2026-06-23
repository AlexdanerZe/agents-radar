# AI CLI 工具社区动态日报 2026-06-23

> 生成时间: 2026-06-23 02:54 UTC | 覆盖工具: 9 个

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

# AI CLI 工具生态横向对比分析报告（2026-06-23）

---

## 1. 生态全景

当前 AI CLI 工具整体处于 **快速迭代与信任重塑并行** 的阶段。一方面，各工具几乎周更甚至日更版本，MCP 生态、Agent 工作流、多 Provider 路由等新功能快速落地；另一方面，数据持久化缺陷、计费不透明、Windows 平台体验劣化、Agent 行为不可控等“信任赤字”问题正在集中爆发。从社区反馈看，用户已不满足于“能回答问题”，而是要求工具具备 **生产级的可靠性、可观测性与协作可控性**。值得注意的是，多工具不约而同地在同一周内处理“死循环检测”“Token 计费回归”“子 Agent 状态透明”等同类课题，说明行业正在从功能竞赛转向 **工程成熟度竞赛**。

---

## 2. 各工具活跃度对比

| 工具 | 今日热点 Issues | PR 数 | 版本发布 |
|------|----------------|-------|----------|
| **Claude Code** | 10（最高评论 45） | 4 | v2.1.186 |
| **OpenAI Codex** | 10（最高评论 121） | 10 | rust‑v0.142.0 + 多个 alpha |
| **Gemini CLI** | 10（最高评论 8） | 10 | 无正式发布 |
| **GitHub Copilot CLI** | 10（最高评论 20） | 0 | v1.0.64‑2 / v1.0.64‑3 |
| **Kimi Code CLI** | 4（活跃） | 3 | v1.48.0 |
| **OpenCode** | 10（精选） | 10 | 无正式发布 |
| **Pi** | 10（最高评论 64） | 10 | v0.79.10 |
| **Qwen Code** | 10（最高评论 5） | 10 | 无正式发布 |
| **DeepSeek TUI (CodeWhale)** | 10（精选） | 10 | v0.8.64（更名版） |

*注：Issues/PR 数量均来自各工具日报的“精选 Top”统计，实际社区仓库总活动量可能更大；版本发布以日报提及为准。*

---

## 3. 共同关注的功能方向

### 3.1 MCP / 插件生态的深度运营
几乎所有工具都在围绕 MCP 做增强：
- **Claude Code** 新增 MCP CLI 认证命令，支持 SSH 免浏览器；
- **OpenAI Codex** 修复 Desktop 端 MCP schema 兼容性，新增 `/plugins` 三分类视图；
- **Copilot CLI** 社区反馈集中在 MCP 初始化指令被忽略、变量插值缺陷；
- **Kimi Code** 出现 MCP 配置残留自动恢复、工作区路径隔离 Bug；
- **OpenCode** MCP 图像附件返回回归、要求完整 MCP 客户端能力；
- **Qwen Code** 实现 MCP 热重载（#5561）和名字补全增强；
- **DeepSeek TUI** 重构路由时也为 MCP Provider 准备了路由 Fixture。

**共同诉求**：MCP 配置需像 IDE 扩展一样稳定可靠，支持热加载、路径隔离、多版本兼容。

### 3.2 计费透明化与配额信任
| 工具 | 具体表现 |
|------|----------|
| OpenAI Codex | #28879 预算消耗突增10–20倍，121条评论，社区危机 |
| Claude Code | #69592 质疑5小时配额计算不透明 |
| Copilot CLI | #3886 重启/恢复会话固定消耗174 Credits |
| Qwen Code | #5683 子Agent Token计数异常偏高 |
| Gemini CLI | 未直接涉及，但企业版 OAuth 故障也影响使用 |

**共同诉求**：提供 token 级别细粒度计费日志，公开配额消耗计算模型，修复计费回归。

### 3.3 Agent 行为的可观测性与可控性
多工具用户明确要求从“交付型 Agent”转向“协作型 Agent”：
- **Claude Code** #60226 模型明知分析无依据仍执行；希望 `$EDITOR` 干预写入、不确定时主动停止；
- **Gemini CLI** #22323 SubAgent 虚假报告成功；#22672 要求 Agent 主动劝阻破坏性命令；
- **Kimi Code** 在 v1.48.0 中移植了重复工具调用检测与强制停止；
- **OpenCode** #32301 支持5层嵌套子Agent，同时需配套状态显示；
- **Pi** #5778 Agent 主循环在流断开时会卡死，缺乏超时；
- **Qwen Code** #5734 fork 子Agent 权限请求被静默拒绝；
- **DeepSeek TUI** #3289 Fleet Worker 导致 TUI 冻结。

**共同诉求**：Agent 执行轨迹实时可见、不确定时回退而非死磕、子Agent 状态透传、可强制中断。

### 3.4 Windows 平台“二等公民”问题
| 工具 | 关键问题 |
|------|----------|
| Claude Code | 白屏、进程泄漏、用户名含空格报错 |
| OpenAI Codex | 沙箱安装失败、闲置高 GPU 占用、Crashpad 膨胀 |
| Copilot CLI | 鼠标滚轮捕获回归、WSL 令牌存储不安全 |
| Kimi Code | 无明显大问题 |
| OpenCode | 桌面版高负载冻结 |
| Qwen Code | 特定终端兼容性（Alacritty） |
| DeepSeek TUI | Windows DSML 流式回归 |

**共同诉求**：Windows 用户数量可观，但稳定性明显劣于 macOS，亟需专项投入。

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 典型差异点 |
|------|----------|------------|
| **Claude Code** | 全功能 AI 编程 IDE 替代 | 团队协作工具（TeamCreate/Delete）、/workflows 工作流、复杂配置（JSONC呼声高） |
| **OpenAI Codex** | OpenAI 原生 CLI，重度模型绑定 | 与 gpt-5.5 计费深度耦合、子代理与父子等待、订阅等级识别 Bug 影响核心权益 |
| **Gemini CLI** | 企业级 GCP 集成 | Auto Memory 记忆系统、AST 感知探索、GCP 项目 ID 校验；企业 OAuth 故障影响大 |
| **GitHub Copilot CLI** | GitHub 生态入口 | Skills 子文件夹、MCP 初始化指令传递、国际化和授权管理；更新频次高但 PR 活跃度低 |
| **Kimi Code CLI** | Moonshot 模型深度优化 | Kosong 推理内容修复、“死循环” 检测与强制停止领先；开源兼容性（OpenAI Legacy）逐步完善 |
| **OpenCode** | 可扩展的 TUI 插件平台 | Effect 生态（HttpApi codegen）、内建 Websearch、工作流引擎拆分；嵌套子 Agent 深度5层 |
| **Pi** | 模型中立、扩展驱动的 Agent 平台 | Provider 数量极多（Merge Gateway、DeepSeek 自动路由等）、扩展 API 完善；关注连接健壮性与包管理 |
| **Qwen Code** | 通义系模型 + 国产化场景 | MCP 热重载率先实现、视觉桥接（纯文本模型也可看图）；输入校验 Bug 批量修复、文档更新力度大 |
| **DeepSeek TUI (CodeWhale)** | 从单一模型向多 Provider 路由转型 | v0.8.64 更名 + v0.8.65 路由重构、Fleet 子Agent 执行基座、国产模型（千帆、百炼）支持快速响应 |

---

## 5. 社区热度与成熟度

### 高度活跃 / 危机感唤醒
- **OpenAI Codex**：#28879 单日 121 评论，社区情绪激烈，用户流失风险高；版本迭代密集（多个 alpha），但计费问题未彻底解决。
- **Pi**：#4945 64 条评论，连接挂起问题牵动大量用户；扩展 PR 丰富，社区贡献活跃。
- **Claude Code**：45 条评论的 #60226 引发 Agent 哲学讨论，同时 Windows 数据丢失（#53717、#12908）持续发酵，社区信任受考验。

### 稳健迭代 / 中度活跃
- **Gemini CLI**：企业用户基数稳定，今日无大版本发布，但 PR 数量多（10 个）且偏安全修复（SSRF、信任对话框）。
- **Copilot CLI**：版本发布频繁（一天内两个补丁），但社区 PR 数为 0，官方主导痕迹明显；Issues 集中在认证和 MCP 配置。
- **OpenCode**：工作流引擎拆分合入（4 个 PR），背后是大功能落地的信号；Bug 集中在稳定性（Worker 终止、内存膨胀），说明社区已开始“压力测试”。
- **Qwen Code**：Bug 批量修复（类型安全）与功能 PR（MCP 热重载、视觉桥接）并行，文档同步更新，处于快速上升期。

### 早期高增长 / 架构转型
- **Kimi Code CLI**：社区规模较小但反馈集中，v1.48.0 重点解决 Agent 死循环，Monitor 流式输出 PR 显示用户对可观测性的迫切需求。
- **DeepSeek TUI (CodeWhale)**：更名 + 大重构，多 Provider 路由和 Fleet 是下阶段焦点；维护者响应极快（#3357 千帆支持当日提交 PR），社区贡献者涌入。

---

## 6. 值得关注的趋势信号

1. **“模型内省可靠性”成为 Agent 瓶颈**  
   Claude Code #60226 揭示的“明知分析无依据仍执行”并非个案，背后是 LLM 缺乏自我行为门控的架构局限。这一现象在 Kimi Code（死循环）、Qwen Code（重复提交）、Pi（流断开卡死）中均有变体。**短期解决方向**是构建工具调用频率限制和超时兜底；**长期**需要模型级别的“stop & reflect”原生能力。

2. **计费透明化决定付费用户去留**  
   OpenAI Codex 的预算突增事件已敲响警钟。当用户发现“没怎么用但额度没了”时，信任崩塌的速度比功能缺失更快。Copilot CLI 和 Claude Code 的类似投诉佐证了这一点。**建议**所有 CLI 工具尽早公开 token 级计费日志，并提供实时配额看板。

3. **Windows 体验正在拖累整体采用率**  
   从白屏、进程泄漏到沙箱安装失败，Windows 问题是跨工具的系统性短板。考虑到 .NET / C++ / 游戏等开发者仍大量使用 Windows，忽视该平台意味着放弃关键市场。**可借鉴** Copilot CLI 的一日两 patch 响应节奏，或 Gemini CLI 添加 CI 覆盖 Windows 回归测试。

4. **MCP 从“能连上”转向“全生命周期管理”**  
   数个工具社区不再满足于基本连接，而是要求热重载（Qwen Code）、路径隔离（Kimi Code）、彻底删除（Kimi Code #2457）、schema 一致性（OpenAI Codex #28978）。MCP 的易用度正成为插件生态竞争的核心分水岭。

5. **Agent 从“助手”向“同事”进化：需要上下文和工作流引擎**  
   嵌套子 Agent（OpenCode 5层）、Fleet 持久化执行（DeepSeek TUI）、父子等待（OpenAI Codex #16900）都指向同一方向：AI 工具不仅要单轮对话，还要能编排长期运行的多 Agent 任务。**工作流引擎 + 状态持久化**将成为下一阶段 CLI 的标配。

6. **开源兼容性与国产化并进**  
   Kimi Code 修复 `reasoning_effort: null` 以对齐 OpenAI 标准，Qwen Code 提供视觉桥接以扩源非视觉模型，DeepSeek TUI 一天内新增千帆/百炼路由。**全球化和本地化并不矛盾**——灵活的 Provider 路由架构是同时覆盖两者的最佳工程实践。

---

*本报告基于 2026‑06‑23 各工具 GitHub 社区公开数据生成，仅供参考。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是基于你提供的 GitHub 数据生成的 **Claude Code Skills 社区热点报告**。

---

## Claude Code Skills 社区热点报告（截至 2026-06-23）

### 1. 热门 Skills 排行（按关注度/评论量 Top 8）

**① #1298: fix(skill-creator): run_eval.py reports 0% recall**
- **功能**：修复 `run_eval.py` 及 `run_loop.py` 中召回率始终报 0% 的严重错误。该 Bug 导致所有技能描述的优化循环基于“噪声”信号运行，评估完全失能。
- **社区热点**：当前社区头号痛点。关联 Issue #556（12 条评论）、#1169，大量用户在 Windows/Linux 下复现。评估机制失能使得技能迭代陷入“开环”状态。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/1298

**② #514: Add document-typography skill**
- **功能**：增加文档排版质检技能，解决 AI 生成文档中的孤儿词、寡妇段落、编号对齐等常见排版问题。
- **社区热点**：需求非常明确且实用。用户无需手动纠正细微排版，直接提升生成文档的“交付质感”。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/514

**③ #83: Add skill-quality-analyzer / skill-security-analyzer (元技能)**
- **功能**：引入两个元技能，从 5 个维度（结构、文档、安全等）审计社区技能的质量与安全性。
- **社区热点**：生态治理标志性 PR。社区开始从“生产”转向“审计”，对技能商店的信任与标准化提出了框架方案。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/83

**④ #210: Improve frontend-design skill clarity and actionability**
- **功能**：重写前端设计技能，确保每条指令清晰、可执行，避免 Claude 行为偏离。
- **社区热点**：对官方技能质量的普遍反思。社区要求 SKILL.md 必须像“代码”一样精确，而不是“文档”一样模糊。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/210

**⑤ #723: Add testing-patterns skill**
- **功能**：覆盖测试全栈（单元、组件、E2E），引入 Testing Trophy 模型，包含命名约定、边界处理等最佳实践。
- **社区热点**：开发者工作流的核心需求。减少 Claude 辅助编码时的重复指令，提升自动化测试生成能力。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/723

**⑥ #154: Add shodh-memory skill (持久记忆)**
- **功能**：实现 Agent 跨会话持久记忆。通过 `proactive_context` 调用和结构化存储维护长程上下文。
- **社区热点**：Agent 状态管理前沿探索。此技能直击“AI 无法记住自己做过什么”的根本痛点。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/154

**⑦ #181: Add SAP-RPT-1-OSS predictor skill**
- **功能**：集成 SAP 开源的表格基础模型，用于 SAP 业务数据的预测分析。
- **社区热点**：企业级需求典型代表。将 Skills 扩展到 SAP 生态，提升了在严肃商业场景中的应用价值。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/181

**⑧ #444: Add AURELION skill suite (认知框架套件)**
- **功能**：4 个技能的套件，包含 5 层结构化认知模板、Agent 记忆与自适应知识管理框架。
- **社区热点**：最强方法论输入。不只是一套工具，而是一套知识管理哲学，代表了社区对“深度引导”而非“工具调用”的追求。
- **状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/444

---

### 2. 社区需求趋势（从 Issues 提炼）

| 需求方向 | 典型 Issue | 核心诉求 |
|---|---|---|
| **基础工具链抢救** | #556, #1061, #189, #1169 | **稳定性压倒一切**。社区大量资源消耗在修复 `run_eval.py` 失能、Windows 子进程崩溃（PATHEXT/cp1252）、技能重复安装等基础缺陷。 |
| **安全与信任治理** | #492, #1175, #412 | 提出命名空间仿冒风险（`anthropic/` 权限边界）、SPO 文档安全担忧、Agent 行为治理。社区寻求类似“应用沙箱”的审批机制。 |
| **组织级协作** | #228, #29, #16 | 强烈要求组织内直接共享 Skill 链接，支持 Bedrock 部署，并计划通过 **MCP 协议** 标准化 Skill 的暴露方式。 |
| **Agent 长程记忆** | #1329, #154 | 如何让 Agent 跨会话记住状态，从“记笔记”到“符号化记忆”的提效方案在持续涌现。 |
| **新 Skill 类型诉求** | #412 (治理), #723 (测试), #514 (排版) | 社区不再满足于“基础代码生成”，开始需要 **企业运维、安全治理、精细化排版** 等垂直领域专精技能。 |

---

### 3. 高潜力待合并 Skills（评论活跃但尚未合并）

- **#83 (skill-quality-analyzer / security-analyzer)**：生态基础设施，合并后将作为技能商店的“质检网关”，极大提升社区技能的可发现性与可信度。
- **#723 (testing-patterns)**：开发者刚需，合并后可显著节省手动提示成本，落地确定性极高。
- **#514 (document-typography)**：痛点精准、代码量适当，属于典型的“高品质小型合并”候选。
- **#154 (shodh-memory)**：虽然框架较大，但代表了 Agent 记忆的核心方向，即使不完全合并，其思路也会深刻影响官方记忆实现。
- **#210 (frontend-design)**：若被接受，可能标志着 Anthropic 官方对 Skill 编写“清晰度与可执行性”标准的立场更新。

---

### 4. Skills 生态洞察（一句话总结）

**当前社区最集中的诉求是：修好基础工具链（recall=0% 和 Windows 兼容性问题），规范安全与治理标准，并打通组织共享与 MCP 互操作层——只有完成这些基础设施的“还债”，Skills 生态才能真正从“创意实验”进入“生产级交付”。**

---

# Claude Code 社区动态日报 | 2026-06-23

## 今日速览

v2.1.186 发布，带来 MCP CLI 认证和工作流过滤，但社区焦点仍被多个严重 Bug 占据：Windows 端数据丢失与白屏持续发酵（#53717, #51143），iOS 最新更新引发大规模闪退（#70164）。值得注意的是，一个关于模型“明知故犯”的深层 Bug（#60226）以 45 条评论量登顶今日热点，社区对 AI Agent 的内省可靠性展开了严肃讨论。

---

## 版本发布

### v2.1.186

**Changelog 要点：**

- **MCP 认证 CLI 化**：新增 `claude mcp login <name>` 和 `claude mcp logout <name>` 命令，无需打开 `/mcp` 交互菜单即可完成 MCP 服务器认证。同时新增 `--no-browser` 参数与 stdin 重定向支持，可在 **SSH 环境**下完成免浏览器认证，极大提升 DevOps 场景体验。
- **Workflows 增强**：`/workflows` 代理新增状态过滤能力（快捷键 `f`），方便开发者在大规模工作流列表中快速定位运行态/失败态任务。

---

## 社区热点 Issues

针对过去 24 小时内更新最活跃的 50 条 Issue，精选其中 10 条进行深度解读（按评论热度排序）：

**1. #60226 — 模型的自我认知悖论：明知分析无依据，却仍执行到底**  
[🔗 链接](anthropics/claude-code Issue #60226)  
标签：`bug, area:model, area:agent` | 评论：45 条  
在推理过程中，Claude 明确拆解了自己当前分析链的漏洞，并承认“这一分析无依据”，但最终回复仍然按照该有缺陷的分析完成输出。这触及了 Agent 行为模式的**本质缺陷**：模型的自我检查不构成输出门控。社区对此展开热烈讨论，认为这是“AI 具备了自省能力却缺乏自省意志”的典型案例。

**2. #68721 — 回归：v2.1.178 移除了 TeamCreate / TeamDelete 原生团队工具**  
[🔗 链接](anthropics/claude-code Issue #68721)  
标签：`bug, regression, platform:linux` | 评论：17 条 | 👍：5  
从 v2.1.177 到 v2.1.178 的升级导致团队协同的核心管理能力退化，开发者在 Linux 环境中无法继续使用原生团队工具。社区对**功能无预警消失**的敏感性极高，该 Issue 持续获得关注，要求建立严格的 API 不兼容回归测试。

**3. #17968 — 呼声最高：支持 JSONC 格式配置文件**  
[🔗 链接](anthropics/claude-code Issue #17968)  
标签：`enhancement` | 评论：16 条 | 👍：87  
用户在 `settings.json` 中添加注释的需求获得 87 个 👍，成为过去半年内社区呼声最高的功能请求。JSONC 作为 VS Code 等工具的标准化格式，如果能被支持，将显著缓解用户在复杂配置时的文档化负担。

**4. #51143 — Windows 桌面版持续白屏，Cowork 完全不可用**  
[🔗 链接](anthropics/claude-code Issue #51143)  
标签：`bug, platform:windows, area:desktop` | 评论：15 条 | 👍：12  
Windows 用户遭遇持续性白屏，多次重装无果，Cowork 功能完全无法使用。这是 Windows 平台最严重的**阻塞性问题**，无任何临时解决手段。

**5. #12908 — macOS 端更新后对话历史全部消失**  
[🔗 链接](anthropics/claude-code Issue #12908)  
标签：`bug, platform:macos, area:ide, memory` | 评论：14 条 | 👍：18  
更新后侧边栏会话存在但内容全部丢失，打开后为空。该 Issue 自 2025 年 12 月起已持续半年未关闭，社区的耐心正在被消耗。

**6. #53717 — Windows 自动更新导致消息内容全部丢失**  
[🔗 链接](anthropics/claude-code Issue #53717)  
标签：`bug, platform:windows, data-loss` | 评论：10 条 | 👍：4  
又一起数据丢失报告。Windows 端 Auto-Update 后，JSONL 会话文件中消息字段完全未被持久化。与 #12908 呼应，说明**跨平台数据持久化逻辑存在系统性风险**。

**7. #68394 — Windows local-agent-mode 进程树泄漏，MCP 集群堆积**  
[🔗 链接](anthropics/claude-code Issue #68394)  
标签：`bug, platform:windows, area:core, area:mcp, perf:memory` | 评论：3 条  
每启动一次 session，`claude.exe` 和其 MCP 服务器进程就累积一次，Session 结束后未被回收。这是 Windows 平台代理模式的**资源管理硬伤**。

**8. #39975 — 功能请求：`/unclear` 命令，恢复被 `/clear` 的上下文**  
[🔗 链接](anthropics/claude-code Issue #39975)  
标签：`enhancement, area:tui` | 评论：5 条 | 👍：31  
虽已关闭，但该 Issue 表明了用户对 TUI 撤销操作的高需求。对不可逆的 `/clear` 增加 `undo` 机制是提升交互信心的重要手段。

**9. #69592 — Session 5 小时限制触发，用户质疑配额计算透明度**  
[🔗 链接](anthropics/claude-code Issue #69592)  
标签：`question, area:cost` | 评论：6 条  
用户反映还没做什么“大活”就被限流了。消耗配额的计算逻辑不透明，导致用户对产品的信任度与付费意愿直接受损。

**10. #70164 — iOS 端最新更新：点击新建 Code Session 立即 Crash**  
[🔗 链接](anthropics/claude-code Issue #70164)  
标签：`bug, platform:ios, regression` | 评论：1 条 | 👍：1  
6 月 22 日更新后出现严重硬崩溃，点击"New Code Session"即闪退。再加上同日报告的 #70165（Remote Control 触发主线程 Stack Overflow）、#70182（静默崩溃），iOS 端用户体验正在遭遇滑铁卢。

---

## 重要 PR 进展

过去 24 小时内共有 **4 个 PR**，均已列出。

**1. #70173 — 修复 `/clean_gone` 无法识别已删除远程分支**  
[🔗 链接](anthropics/claude-code PR #70173)  
作者：AndrewDongminYoo  
`git branch -v | grep '[gone]'` 的过滤模式在 Git 新版本中已失效，导致 `/clean_gone` 从未成功删除过任何分支。PR 改为使用 `git branch -vv` 精确匹配上游状态，修复了仓库清理功能**实际失效长达数周**的问题。

**2. #63686 — 提议将 Issue 过期时间从 14 天延长至 90 天**  
[🔗 链接](anthropics/claude-code PR #63686)  
作者：caseyWebb  
当前 14 天的 Stale/Autoclose 周期被认为过于激进，许多重要 Issue 在未被维护者看到前就被机器人关闭。该 PR 提议调整为 90 天，以平衡社区反馈留存与仓库整洁度。

**3. #70074 — 修正插件市场已失效的名称引用**  
[🔗 链接](anthropics/claude-code PR #70074)  
作者：itxaiohanglover  
插件开发文档中将市场名误写为 `claude-code-marketplace`，已全部更正为 `claude-code-plugins`，修复了开发者因文档错误导致的安装失败。

**4. #70066 — 更新插件安装文档与命令规范**  
[🔗 链接](anthropics/claude-code PR #70066)  
作者：abhi-zit77  
将示例命令从 `cc --plugin-dir` 修正为官方推荐的 `claude --plugin-dir`，同时完善了贡献指南。两个 Docs PR 同日出现，侧面说明插件生态正处于**快速迭代阶段**，文档跟进压力大。

---

## 功能需求趋势

从今日所有 Issues 中提炼出的社区关注方向：

- **配置标准化与可管理性**：JSONC（#17968）获得 87 个 👍 是明确的信号——用户希望配置能加注释以追溯决策。此外，可调 Git 轮询间隔（#70186，最新提出）代表大型项目中用户对**资源细粒度控制**的需求。

- **AI 行为可干预**：不再满足于接受 AI 的最终输出。用户希望在文件写入前有 `$EDITOR` 干预微调（#70188），希望 Agent 在“不确定”时能主动停止而非死磕（#70198）。**从交付型 Agent 到协作型 Agent 的转型诉求非常明确。**

- **跨端协同与移动生态**：iOS 端连续出现的崩溃意味着 Claude Code 正在被大家“带着走”，远程控制（Remote Control）和工作流移动化的稳定性，决定了产品能否从桌面工具进化为全平台基础设施。

- **MCP 生态自举**：新版本对 MCP 登录/登出的 CLI 认证增强、插件文档的集中修订，标志着插件生态度过了“能用”的原始期，进入**开发者体验优化**的深水区。

---

## 开发者关注点

基于社区高频反馈与痛点分布：

**1. 信任赤字：数据安全是第一性原则**  
连续出现 Windows 和 macOS 端的会话历史消失（#12908, #53717），这对开发者是**零容忍的质量失败**。当一个工具不记得之前的对话，其作为“迭代式开发伴侣”的信任基础就会被动摇。这应当优先于任何新特性开发。

**2. Windows 平台的“二等公民”印记**  
白屏、进程泄漏、Defender 冲突、用户名含空格就报错——Windows 端问题密度显著高于 macOS。这类“细节但致命”的 Bug 正在深度影响大量 .NET/C++ 开发者的采用意愿。

**3. “新版本焦虑”全面蔓延**  
#68721 功能无预警移除、#70164 更新即崩溃、#63238 持续提醒更新但实际上已是最新版——社区呈现出**对升级的抵触心理**。用户不希望每次 `brew upgrade` 或 Windows 更新都变成一个“开盲盒”的行为。

**4. 核心 Agent 模式的“哲学困境”**  
#60226 和 #70196（Tool Call 解析失败循环重试）本质隐喻着当前 LLM Agent 的瓶颈：**模型无法彻底信任自己的推理过程**。当模型说“我不确定，但让我试试”，用户看到的不是一个谦虚的助手，而是浪费时间的试错。社区期待的是 **“不确定就告诉我，而不是做了再改”** 的行为范式。

---
*本日报由 AI 自动生成，所有数据源均来自 GitHub `anthropics/claude-code` 仓库的公开通信记录。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-06-23）

## 今日速览

① **[Rate-Limit 信任危机]** 自6月16日起，大量用户遭遇 `gpt-5.5` 调用成本暴涨 10–20 倍，#28879 单日涌入 121 条评论，社区情绪激烈，OpenAI 必须尽快确认是否为计费回归。

② **[磁盘写入危机解除]** #28224 描述的 Codex SQLite 日志年写入量高达 640TB 问题，已于昨日通过 #29432 和 #29457 两个 PR 合并修复，预计减少 85% 日志量，但 macOS 上日志问题仍有残余（#29532）。

③ **[版本推进]** `rust-v0.142.0` 正式发布，重点强化了 `/usage` 的额度赎回与重试逻辑，以及 `/plugins` 的远程插件分类视图（OpenAI 精选 / 工作区 / 与我共享）；多个 `v0.143.0-alpha` 版本同步推进。

---

## 版本发布

**rust-v0.142.0**（正式版）
- `/usage` 新增使用额度上限重置积分的展示和赎回机制，支持确认、重试和刷新可用状态。（#28154, #28793）
- `/plugins` 将远程插件重组为 **OpenAI Curated**（OpenAI 精选）、**Workspace**（工作区）和 **Shared with me**（与我共享）三大分类。

**rust-v0.143.0-alpha.1 / alpha.2 / 0.142.0-alpha.11 / 0.142.0-alpha.12**
- 密集的 Alpha 发布周期，表明团队正围绕配额与压缩预算进行快速迭代和内部测试。

---

## 社区热点 Issues（Top 10）

| # | 标题 | 热度 | 为什么值得关注 |
|---|------|------|----------------|
| **#28879** | `gpt-5.5` Plus 计划预算消耗突增 10~20 倍，5 小时额度 2-3 个 Prompt 即耗尽 | 🔥🔥🔥 121 评论 / 239 👍 | **目前最严重的社区危机**。用户反馈自 6/16 起无任何模型切换，`limit-% consumed per token` 指标暴涨。如不回滚或修复，大量 Plus 用户将无法正常使用。 |
| **#28224** | Codex SQLite 日志年写入量达 640TB，快速消耗 SSD 寿命 | ✅ **已关闭** / 265 👍 | **Yesterday's big win.** 社区高度关注的一项磁盘性能灾难。两个 PR 于 6/22 合并，可避免 85% 反馈日志。是过去一个月最成功的社区推动修复案例。 |
| **#28982 / #29418** | Windows App 沙箱安装助手报错 `The specified module could not be found` | 29 + 4 评论 | Windows 用户升级后沙箱功能完全不可用，新用户注册/隔离环境启动受阻。**官方亟待跟进。** |
| **#28978** | Desktop App 26.616 版 MCP 报错 `Invalid request: missing field "inputSchema"`，CLI 正常 | 20 评论 / 24 👍 | **MCP 兼容性崩塌**。Desktop GUI 端逻辑与 CLI 不一致，严重依赖 MCP Server 的高阶 Pro 用户新对话直接报错，无法使用。 |
| **#28886 / #28823** | 单次长任务导致 5 小时配额异常快速耗尽 / 使用量遥测与仪表盘严重偏差 | 16 + 2 评论 | **多重佐证** #28879 并非个案。多个用户独立报告消费速度与历史数据不可比，说明是系统级 charge 回归而非单一用户配置问题。 |
| **#25921** | Crashpad dumps 无限制增长，每日超 5GB | 13 评论 / 3 👍 | **桌面端隐藏硬盘杀手**。`Crashpad/pending` 目录以每天+5GB + 数万个文件的速度膨胀，对 macOS SSD 寿命构成持续威胁，至今未修复。 |
| **#29243** | Pro $100(5x) 计划在 Desktop 上被误识别为 `plus` 进行限速 | 5 评论 | **订阅权益 BUG**。最贵的 $200 Pro 用户 `plan_type=prolite`，但 API 反回 `X-Codex-Plan-Type=plus`，直接影响模型调用链和配额上限。 |
| **#29281** | Windows 11 更新后闲置状态持续高风扇/高 GPU 占用 | 3 评论 / 2 👍 | **性能退步**。升级至 26.616 后 Windows 用户即使不操作，Codex 也持续占用 CPU/GPU，引发设备发热和续航焦虑。 |
| **#16900** | 子代理状态检查与父子等待机制 | 11 评论 / 4 👍 | **开发者高频呼声**。多代理流程中子线程慢速运行但父线程过早回退导致重复劳动。这是一个长期未解决的产品缺口，缺少 Agent 全生命周期可见性。 |
| **#29533** | 登录验证码发送至旧手机号，无法接收 | 2 评论 | **账号安全漏洞**。新版 26.616 登录流程有严重缺陷：验证码默认发往旧号码且无法从 App 内修改，Pro 订阅用户直接无法登录。 |

---

## 重要 PR 进展（Top 10）

| PR # | 标题 | 状态 | 亮点 |
|------|------|------|------|
| **#29473** | 传播安全缓冲处理元数据 (`safety-buffering treatment`) | ✅ **已合并** | 核心安全能力。从 HTTP 响应头和 WebSocket 元数据中读取请求级安全缓冲策略，前端可根据 `showBufferingUi` / `fasterModel` 调整渲染。 |
| **#29514** | rollout-budget 线程跳过初始 prompt prefill 计费 | 🔄 **开放中** | **直接回应 Rate-Limit 争议**。每条新线程的第一个 prefill 不再扣费，仅在首次输出和后续 prefill 时扣费——让首次交互更划算。 |
| **#24092** | 拒绝未经降级的 PowerShell AST 区域 | 🔄 **开放中** | **Windows 安全加固**。PowerShell 安全命令分类器若未正确 `lower` AST 区域，恶意代码块可绕过白名单检查。对 Windows 企业用户至关重要。 |
| **#29526** | 在选定环境中解析 `view_image` 路径 | 🔄 **开放中** | **跨环境路径问题修复**。此前 `view_image` 以宿主机路径解析，导致 Codex 在 Docker/Target 环境无法正确读取图片文件。 |
| **#29527** | 压缩世界状态与上下文对齐 | 🔄 **开放中** | **核心上下文引擎正确性修复**。回合内压缩可能导致 `WorldState` 基线来自不同环境快照，引发引用错误。深度跟踪 #29249 的后续。 |
| **#29521** | Token-budget 压缩时重置上下文 | 🔄 **开放中** | **新策略**。启用 Token Budget 时，压缩行为不再要求后端压缩历史，而是直接刷新为全新的上下文窗口并注入标准初始内容。 |
| **#29519** | 持久化初始上下文窗口元数据 | 🔄 **开放中** | **可观测性增强**。#29494 将上下文窗口 ID 暴露给模型，但 `rollout JSONL` 消费方无法回溯窗口身份。此 PR 补全了 Telemetry 最后一环。 |
| **#28598** | Bazel 调整 Rust 测试目标尺寸 | 🔄 **开放中** | **工程基础设施**。解决 Bazel 中 Rust 测试默认继承不匹配 size 导致的超时警告淹没真正失败信息的问题。 |
| **#29493** | MCP 接受远程 stdio 的跨平台绝对 cwd | ✅ **已合并** | **Cross-Platform MCP 兼容性**。Windows `C:\Users\...` 格式路径被 POSIX 协调器拒绝，导致远程 stdio 服务器失败。此 PR 修正了路径校验逻辑。 |
| **#28271** | 为不支持 namespace 的 provider 展平 MCP 工具 | 🔄 **开放中** | **第三方兼容性**。部分 API 提供商不理解 Codex 私有 `type: "namespace"` 工具包装器，MCP 工具完全不可见。此举新增 provider 能力声明。 |

---

## 功能需求趋势（来自全部 Issues）

1. **计费公平性与透明化（压倒性优先级）**
  - #28879、#28823、#28886、#28504、#29243 构成「Rate-Limit 五连」，核心诉求：为什么 5 小时额度在相同模型下消耗速度快了 10-20 倍？社区强烈要求提供 `token_count` 级别细粒度的 charge 日志和配额计费审计 API。

2. **磁盘与日志性能的彻底治理**
  - #28224 的修复是一个里程碑，但 #25921（Crashpad dump 膨胀）、#24275 和 #29532（`logs_2.sqlite` WAL 持续写入）说明 Codex Desktop 端的 I/O 模式仍有严重缺陷。社区期待类似「静默模式」或「日志滚定阈值」。

3. **MCP / 插件生态系统的成熟化**
  - `rust-v0.142.0` 的 `/plugins` 分类是积极信号。但 #28978（Desktop App MCP schema 不一致）及 #28271（第三方 provider 兼容性）表明 MCP 在产品化过程中仍有许多边界问题。用户希望 MCP 配置像 VS Code 扩展一样可靠。

4. **Windows 平台深度优化**
  - #28982/29418（沙箱模块找不到）、#29281（闲置高负载）、#24427（多线程响应缓慢），Windows 用户的体验明显劣于 macOS 用户。社区对 Windows 原生性能测试和沙箱修复呼声很高。

5. **子代理与流程编排可见性**
  - #16900 自 4 月起持续有人反馈，说明多 agent 协作场景已进入真实应用阶段。用户希望看到子 agent 状态、执行进度、和父 agent 的超时控制。

---

## 开发者关注点（痛点与高频需求）

**1. 🔴 费用恐慌：预算消耗疑云不散**
这不是一个小 bug，而是动摇了「用户对平台计费系统的信任」。多位 Pro/Plus 用户明确表示：「如果再修复前频繁触发，将暂停订阅」。健康监测和实时 charge 反馈必须成为最高优。

**2. 🟠 Windows 桌面端沦为二等公民**
沙箱安装失败 + 闲置风扇狂转 + 多线程响应慢 + Crashpad 写入失控——Windows 生态的稳定性警报已亮起红灯。相比 macOS，Windows 用户面临更多的不确定性问题。

**3. 🟠 MCP 配置的脆弱性**
Desktop App 一个版本更新就能让现有 MCP 配置报废（inputSchema 字段缺失），且 CLI 表现正常。说明 App-Server 与 CLI 复用同一套底层库时前端存在差异化校验漏洞。

**4. 🟡 订阅等级识别错误**
Pro（$200）被识别为 Plus 进行限速极其敏感。这直接影响付费用户的核心权益（模型选择、速率上限），属于**账单层面的 P0 级缺陷**。

**5. 🟡 账号恢复无门**
#29533 揭示的新版登录流程缺陷——验证码锁死旧手机号且无 App 内修改途径——对需要重新登录的用户是不可进入的。建议增加备用邮箱验证机制。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，作为一名专注于 AI 开发工具的技术分析师，以下是根据提供的 GitHub 数据生成的 2026-06-23 日 Gemini CLI 社区动态日报。

---

# 2026-06-23 Gemini CLI 社区动态日报

## 1️⃣ 今日速览

今日社区面临一场**认证风暴**：大量企业用户反映 OAuth 账号突然失效（#28088），官方迅速响应并提交了针对 Node.js 24.17 Socket 复用回归的修复方案（#28103）。与此同时，**安全加固密集落地**，`web_fetch` 工具的 SSRF 漏洞（#27744, #27739）以及信任对话框的安全缺陷（#27915）均得到修复。此外，**底层稳定性依然是焦点**，SIGINT 取消后工具误执行（#28096）和模型“内心独白”泄露（#27971）的修复标志着项目正在打磨细节。

## 2️⃣ 版本发布

今日无正式版本发布。

## 3️⃣ 社区热点 Issues（Top 10）

**1. #28088: 企业版 OAuth 突然登出，授权账号报错“未授权”**
- **重要性：🔥 紧急 / 阻塞**
- **摘要：** 企业托管的 Google 账号（拥有 Gemini Code Assist 标准许可证）在 6 月 22 日早晨突遭登出，重新授权后 CLI 提示“未授权”。8 条评论反映了众多企业用户被阻断，社区反响强烈（👍 4）。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/28088)

**2. #28101: 无法正常登录 Gemini CLI**
- **重要性：🔥 紧急**
- **摘要：** 新提的 Issue，用户反映界面卡死或跳转异常，无法完成登录流程。可能和 #28088 的根系问题有关。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/28101)

**3. #22323: [P1] SubAgent 在达到 MAX_TURNS 后虚假报告“成功”**
- **重要性：⭐⭐⭐⭐⭐ （可靠性）**
- **摘要：** `codebase_investigator` 子代理在达到最大轮次限制无法进行分析时，向上层返回 `status: "success"`，导致任务中断被完全隐藏。社区认为这严重破坏了 Agent 行为的透明度。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

**4. #25166: [P1] Shell 命令执行完成后卡死在“等待输入”**
- **重要性：⭐⭐⭐⭐⭐ （核心体验）**
- **摘要：** 这是一个持续引发共鸣的痛点（👍 3）。执行简单的 CLI 命令后，界面仍显示“Awaiting user input”，导致终端假死，严重影响交互流畅性。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

**5. #27741: Gemini CLI 无视架构模式，静默删除正常代码**
- **重要性：⭐⭐⭐⭐ （信任危机）**
- **摘要：** 用户报告在大型代码库中，Gemini 不遵循已有架构模式创建平行结构，甚至静默删除了正在工作的代码。虽已关闭（需更多信息），但反映了开发者的深度忧虑。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/27741)

**6. #22745: [Epic] 评估 AST 感知文件读写的价值**
- **重要性：⭐⭐⭐⭐⭐ （长期方向）**
- **摘要：** 跟踪一系列调研，探索使用 AST 读取方法边界、导航代码库，以减少 Token 消耗和读取出错。这是 AI 编码工具进化的核心技术储备。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

**7. #26522 & #26525: Auto Memory 系统双提 Bug（无限重试 & 脱敏缺陷）**
- **重要性：⭐⭐⭐⭐ （记忆系统健壮性）**
- **摘要：** 社区希望修复 Auto Memory 对低信号会话的无限重试（#26522），以及修复日志记录中秘密信息仅在模型上下文中脱敏而非在日志存留时脱敏的问题（#26525）。
- **Link:** [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) | [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)

**8. #24246: 工具数量超过 128 个时触发 400 错误**
- **重要性：⭐⭐⭐⭐ （可扩展性）**
- **摘要：** 当可用工具过多时，CLI 直接遭遇 400 错误。社区期待 Agent 能更智能地基于上下文裁剪工具集，而不是直接崩溃。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

**9. #21983: [P1] Browser 子 Agent 在 Wayland 下无法工作**
- **重要性：⭐⭐⭐⭐ （Linux 兼容性）**
- **摘要：** 浏览器自动化功能在 Wayland 显示服务器上完全失效，限制了 Linux 桌面用户的使用。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

**10. #22672: Agent 应主动制止/劝阻破坏性行为**
- **重要性：⭐⭐⭐⭐ （安全规范）**
- **摘要：** 开发者要求模型在执行 `git reset --force` 或危险数据库操作时，能主动识别风险并劝阻用户，而非盲从指令。
- **Link:** [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22672)

## 4️⃣ 重要 PR 进展（Top 10）

**1. #28103: 修复 OAuth Token 交换中 Keep-Alive Socket 重用问题**
- **摘要：** 精准打击今日的 OAuth 风暴。Node.js 24.17 的 Socket 复用回归导致 `ERR_STREAM_PREMATURE_CLOSE`。该 PR 通过避免 Keep-Alive Socket 重用彻底修复该问题。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28103)

**2. #27744 & #27739: 修复 `web_fetch` 的 SSRF 防御绕过漏洞**
- **摘要：** 针对 DNS Hostname（如 `127.0.0.1.nip.io`）及重定向绕过 SSRF 监控的严重安全漏洞进行修复。均已关闭合并。
- **Link:** [#27744](https://github.com/google-gemini/gemini-cli/pull/27744) | [#27739](https://github.com/google-gemini/gemini-cli/pull/27739)

**3. #28096: 修复 SIGINT 中断后工具调用依旧执行的问题**
- **摘要：** 解决了用户按下 Ctrl+C 取消后，延迟到达的工具调用仍在本地执行并返回结果的 Bug，确保了中断的原子性。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28096)

**4. #28000: 修复 `write_file` 导致 Jupyter Notebook 和 JSON 文件损坏**
- **摘要：** 严重数据损坏 Bug 修复。`write_file` 在写入 `.ipynb` 和高度格式化 JSON 时静默破坏内容，现已修复并关闭。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28000)

**5. #27971: 剥离历史记录中的“模型思考”泄露，防止无限循环**
- **摘要：** 修复模型内部推理（Thoughts）泄露到对话历史的问题。这种泄露会导致模型在下轮对话中模拟思考过程，陷入自言自语式的无限循环。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27971)

**6. #28053: 防御性修复 `@` 引用路径解析问题**
- **摘要：** 当用户传入 `@policies/new-policies.txt` 等引用格式时，文件系统工具报“文件未找到”。该 PR 实现了全面的防御性路径解析，兼容跨平台。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28053)

**7. #27916: 校验 GCP 项目 ID 格式，防止 Memory 系统存储别名引发 403**
- **摘要：** Auto Memory 错误地将 GCP 项目显示名称作为项目 ID 存储，导致后续 API 调用返回 `403 CONSUMER_INVALID`。修复增加了严格的正则格式校验。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27916)

**8. #28094: 修复 A2A Server 用户与工作区设置的深度合并问题**
- **摘要：** `loadSettings` 之前使用浅拷贝，导致工作区配置完全覆盖用户 Nested 配置。修复为深度合并，确保工具、遥测等模块配置正确继承。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28094)

**9. #28093: 缓冲聊天压缩遥测数据，避免 SDK 未初始化时崩溃**
- **摘要：** `logChatCompression` 绕过统一遥测缓冲直接发送，在 SDK 未完全就绪时导致空指针崩溃。修复后统一走 Buffer 队列，提升了启动稳定性。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28093)

**10. #27915: 修复信任对话框反向显示 Hook 形状的安全问题**
- **摘要：** 工作区信任对话框显示的是“不会运行”的 Hook 而不是“实际运行”的 Hook，且点击信任即可执行恶意代码。修复了此严重安全缺陷。
- **Link:** [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27915)

## 5️⃣ 功能需求趋势

从今日的大量 Issue 中，可以提炼出社区最关注的三个功能方向：

- **“深度代码理解”需求井喷：** 社区对目前基于字符串匹配的“浅层”文件读取愈发不满，**AST 感知**成为高频词汇（#22745, #22746）。开发者需要 Agent 能够精确理解方法边界、自动解析类型，并据此导航代码库，而非通读整文件。
- **记忆系统的“透明化”与“控制权”：** Auto Memory 是双刃剑。社区希望停止其“野性生长”，包括：**停止无意义的无限重试**（#26522）、**提供确定性脱敏而非事后补救**（#26525）、**暴露失败 Patch 以供排查**（#26523）。用户希望掌控“AI 记住了什么”。
- **Agent 行为的“可预见性”与“安全性”：** 无论是 SubAgent 虚假报告成功（#22323），还是模型随意创建临时脚本（#23571），开发者迫切希望 Agent 的行为是**可预测**且**可控**的。要求模型具备“自知之明”（#21432）、劝阻破坏性命令（#22672）、以及遵守设定的禁用规则（#22093）的需求正在集中爆发。

## 6️⃣ 开发者关注点

- **稳定性与信任是最大的沉默成本：** 开发者不是不想要 AI 辅助，而是无法忍受“它看起来在干活，实际上在不动声色地闯祸”。**OAuth 登录炸毁**（#28088）直接摧毁了工作流入口，而 **Shell 命令卡死**（#25166）和**代码静默删除**（#27741）则在不断侵蚀开发者对 CLI 的信任。用户需要的是牢靠的“副驾驶”，不是需要时刻提防的“实习生”。
- **模型“幻觉”的代价正在从文本转向行为：** 过去 AI 的幻觉是写错了文字，现在 AI Agent 的幻觉则是**采取了错误的行动**（错误的工具调用、错误的参数、错误的 git 操作）。这种“行为幻觉”的调试成本极高，社区急需增强 SubAgent 轨迹的可见性（#22598）和 Bug Report 的上下文完整性（#21763）。
- **“配置即代码”但“配置很难懂”：** 用户对 `settings.json` 中配置不生效（#22267）、SubAgent 无法禁用（#22093）感到困惑。开发者们需要一种**更加简洁、直观且能立即生效**的配置机制，而不是需要翻阅文档才能理解的神秘 JSON 字段。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-06-23

## 📌 今日速览
今日发布 v1.0.64‑2 和 v1.0.64‑3 两个补丁，引入 HTTP 代理设置、内联图片渲染等功能，并修复了会话恢复含空格名称、远程会话中隐藏不支持的斜杠命令等问题。社区方面，Skills 子文件夹支持（#1632）和会话恢复认证错误（#3596）持续获得高赞；同时新增“AI Credits 消耗异常”（#3886）、“扩展思考独立控制”（#3888）等热门议题，MCP 配置与认证计费成为讨论焦点。

---

## 📦 版本发布
**v1.0.64‑3**  
- **Added** – 新增用户设置：HTTP(S) 代理  
- **Fixed** – 修复按名称恢复会话时名称含空格的问题；远程托管会话中不再显示不支持的斜杠命令  

**v1.0.64‑2**  
- **Added** – 新增隐藏对话滚动条开关；CLI 内联图片渲染；Skills 参数提示（argument-hint）前置元数据支持  
- **OpenTelemetry** – 压缩成功的对话 span 携带 `gen_ai.conversation.compacted=true`，并将摘要以 CompactionPart 形式发出  

🔗 [查看所有 Releases](https://github.com/github/copilot-cli/releases)

---

## 🔥 社区热点 Issues（Top 10）

1. **#1632 – Skills 子文件夹支持**  
   👍 20 · 💬 8 · **OPEN**  
   用户希望用子目录组织自定义 Skills，当前扁平机构管理困难。社区呼声极高，影响插件生态的可维护性。  
   [链接](https://github.com/github/copilot-cli/issues/1632)

2. **#3596 – 恢复会话时模型列表报“Not authenticated”**  
   👍 11 · 💬 6 · **OPEN**  
   `/resume` 后无法使用 `/model` 命令，认证状态丢失。严重阻塞日常工作流，评论中多人重现。  
   [链接](https://github.com/github/copilot-cli/issues/3596)

3. **#3886 – 重启/恢复会话消耗 AI Credits**  
   👍 0 · 💬 0 · **OPEN**  
   用户发现 `/restart` 或 `/resume` 会固定消耗约 174 Credits，与官方文档“仅活跃会话计费”的描述不符。潜在计费漏洞，需密切关注。  
   [链接](https://github.com/github/copilot-cli/issues/3886)

4. **#1944 – Windows 鼠标滚轮被输入框捕获（回归）**  
   👍 3 · 💬 10 · **CLOSED**  
   该回归导致无法滚动浏览对话历史，严重影响 Windows 用户体验。虽然已修复，但社区讨论充分，需警惕相似回归。  
   [链接](https://github.com/github/copilot-cli/issues/1944)

5. **#3162 – MCP 自定义服务器被错误标记为“策略阻止”**  
   👍 1 · 💬 7 · **CLOSED**  
   1.0.42 版本中，已在 MCP 注册表中的服务器仍被报为策略阻止，属验证假阴性。已修复，但暴露了 MCP 策略验证的匹配缺陷。  
   [链接](https://github.com/github/copilot-cli/issues/3162)

6. **#1579 – CLI 忽略 MCP 服务器返回的 “instructions”**  
   👍 3 · 💬 0 · **OPEN**  
   MCP 规范要求将初始化 instructions 传递给 LLM，CLI 直接忽略，导致工具行为不完整。长期 Open，影响 MCP 集成的正确性。  
   [链接](https://github.com/github/copilot-cli/issues/1579)

7. **#3888 – 将扩展思考暴露为独立控制（独立于 reasoning effort）**  
   👍 0 · 💬 0 · **OPEN**  
   针对 Anthropic 模型（如 Claude Opus 4.8），CLI 目前只开放 effort 参数，无法独立开关 extended thinking。高级用户追求精细化推理控制。  
   [链接](https://github.com/github/copilot-cli/issues/3888)

8. **#3278 – 显示每次生成/响应的耗时**  
   👍 1 · 💬 2 · **OPEN**  
   用户在长操作（尤其是 autopilot 模式）中缺少运行时间反馈。同类需求也见于 #3111、#3055，社区对透明度要求日益增强。  
   [链接](https://github.com/github/copilot-cli/issues/3278)

9. **#2337 – WSL 下应使用 git-credential-manager 安全存储 Token**  
   👍 2 · 💬 1 · **OPEN**  
   目前 WSL 登录认证通过不安全方式存储凭证，建议集成 GCM 以提升安全性。平台特定安全增强。  
   [链接](https://github.com/github/copilot-cli/issues/2337)

10. **#3883 – 国际化支持（Top 10 语言）**  
    👍 1 · 💬 0 · **OPEN**  
    非英语用户提出需要本地化菜单、状态信息及帮助文本，以降低使用门槛。反映全球社区对语言支持的期待。  
    [链接](https://github.com/github/copilot-cli/issues/3883)

---

## 🔄 重要 PR 进展
过去 24 小时内 **无新的 Pull Requests 被创建或合并**。开发重心主要集中于 Issues 讨论与补丁发布。

---

## 🧭 功能需求趋势
- **模型与推理控制精细化** – 要求独立控制扩展思考（#3888），以及对模型认证状态的透明管理（#3596）  
- **操作进度透明** – 多次请求增加“计时器”功能（#3278、#3111、#3055），希望在长任务中显示已用时间  
- **Skills 与插件可扩展性** – 子文件夹支持（#1632）、稀疏检出安装（#2399），用户对可维护性和安装效率提出更高要求  
- **MCP 生态完善** – 包括初始化指令传递（#1579）、注册表变量插值（#3887）、跨 IDE 共享 MCP（#3638），MCP 已成为集成外部工具的关键短板  
- **国际化与基础体验** – i18n 支持（#3883）和输入框滚动（#3885）显示用户覆盖范围扩大后对 UI 基本功用的关注  

---

## ⚠️ 开发者关注点
- **认证与计费** – 会话恢复报认证错误（#3596）以及重启消耗 Credits（#3886）直接关系可用性与成本，反馈最集中  
- **MCP 配置可靠性** – 忽略 instructions、变量不插值、策略误判等导致 MCP 集成不稳定，增加调试成本  
- **权限提示过剩** – 即使是无害命令（如 `2>/dev/null`）仍触发权限确认（#2693），WSL 令牌存储不安全（#2337），权限模型亟需优化  
- **基础输入与渲染** – 鼠标滚轮被输入框捕获（#1944）、长文本无法滚动（#3885）、`@` 文件引用失效（#3854）等 UI 问题影响日常编辑效率  

---

*本日报基于 [github.com/github/copilot-cli](https://github.com/github/copilot-cli) 公开数据生成，仅供技术社区参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是为您生成的 2026-06-23 的 Kimi Code CLI 社区动态日报。

---

## Kimi Code CLI 社区动态日报 | 2026-06-23

**数据来源:** github.com/MoonshotAI/kimi-cli（统计周期：2026-06-22 ~ 2026-06-23）

### 1. 今日速览
- Kimi CLI 发布 **v1.48.0** 版本，重点修复了 Kosong 推理内容空值处理，并引入了针对 Agent 死循环的强制停止机制。
- 社区集中反馈了 **MCP 配置管理** 中的两个关键 Bug（配置残留自动恢复、工作区路径隔离），以及对 **严格 API 模式** 的兼容性缺陷。
- 新增 `Monitor` 流式工具调用监控的 PR 获得关注，显示出开发者对 Agent 执行过程“可观测性”的强烈需求。

### 2. 版本发布
*   **发布版本**：[Kimi CLI v1.48.0 / Kosong v0.54.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.48.0)
*   **更新内容**：
    *   **核心修复（kosong）**：修复了空推理内容在过往轮次中的往返传输问题，提升了数据交换的健壮性。
    *   **灵魂模块增强（soul）**：移植了 Kimi Code 中的重复工具调用处理逻辑。当 Agent 连续重复调用同一工具 3 次后，会注入递进式提醒（r1/r2/r3）；达到死胡同阈值后，自动强制停止当前轮次，有效防止 Token 浪费和逻辑死循环。
    *   **依赖管理**：内部同步更新了 Kosong 核心库，并更新了 `kimi-code` 包装器。

### 3. 社区热点 Issues
*本期共有 4 个活跃 Issue，虽然数量不多，但均精准锚定了当前用户体验的核心痛点。*

1.  **[[Bug] MCP 服务器删除后仍被自动发现，导致 400 错误](https://github.com/MoonshotAI/kimi-cli/issues/2457)**
    *   **信号强度**：🔴🔴🔴🔴🔴 极高。
    *   **摘要**：用户删除了 MCP 服务器配置，但 CLI 仍通过自动发现机制重新加载并调用，导致持续 400 错误且无法修复。
    *   **社区反应**：此问题严重性极高，直接让 MCP 的“剔除”操作失效，影响了用户对 K2.7 模型 Agent 的信任。

2.  **[[Bug] `kimi web` 从安装目录而非工作区启动 MCP 服务器](https://github.com/MoonshotAI/kimi-cli/issues/2469)**
    *   **信号强度**：🔴🔴🔴🔴 较高。
    *   **摘要**：`kimi web` 命令错误地从 CLI 全局安装目录启动 MCP 服务器，导致依赖项目根路径的工具（如 Lint、构建命令）完全无法工作。
    *   **社区反应**：对于多项目并行开发的用户属于 Blocking 级 Bug，凸显了环境上下文隔离的紧迫性。

3.  **[[Bug] 子进程工具调用后 CLI 发生挂起](https://github.com/MoonshotAI/kimi-cli/issues/2468)**
    *   **信号强度**：🔴🔴🔴🔴 较高。
    *   **摘要**：用户在使用本地 Mock API 时，执行 detached 子进程工具后 CLI 完全无响应。
    *   **社区反应**：这是影响开发连续性的严重稳定性问题，暴露出 CLI 在底层进程管理（文件描述符、管道）上的短板。

4.  **[[Bug] OpenAILegacy 发送 `reasoning_effort: null` 违反 API 规范](https://github.com/MoonshotAI/kimi-cli/issues/2465)**
    *   **信号强度**：🔴🔴🔴🔴 较高。
    *   **摘要**：Kosong 在关闭 thinking 参数时发送了不合规的 `null` 值，导致严格遵循 OpenAI 标准的 API 报错，且无法真正禁用推理。
    *   **社区反应**：这暴露了 CLI 在接入标准/第三方 API 时的兼容性问题，是连接更广泛生态的潜在障碍。

### 4. 重要 PR 进展
*本期 3 个 PR 分别覆盖了重大功能提议、核心 Agent 行为修复与版本管理。*

1.  **[[Feature PR] feat(tools): 新增 Monitor 工具实现逐行 Stdout 流式输出](https://github.com/MoonshotAI/kimi-cli/pull/2471)**
    *   **信号强度**：🔵🔵🔵🔵🔵 极高。
    *   **重点解读**：此 PR 提议新增一个 `Monitor` 工具，作为现有后台执行工具的流式替代。让用户在 Agent 执行长耗时工具（如编译、测试）时，能实时看到逐行输出，而非等待最终结果。这直接指向了当前 Agent 智能体的“黑盒”痛点，是提升可观测性的关键一步。

2.  **[[Enhancement PR] feat(soul): 处理重复工具调用并强制停止死循环](https://github.com/MoonshotAI/kimi-cli/pull/2466) (已合并)**
    *   **信号强度**：🔵🔵🔵🔵 较高。
    *   **重点解读**：将已经过验证的“防呆”机制移植到 Kimi CLI。重要细节在于它的递进式提醒，让开发者可以观察 Agent 的行为异常，并在彻底失控前由系统自动干预。这构成了一个完整的“检测-提醒-打断”闭环。

3.  **[[Chore PR] chore(release): 版本发布同步](https://github.com/MoonshotAI/kimi-cli/pull/2467) (已合并)**
    *   **信号强度**：🔵🔵 一般。
    *   **重点解读**：内部工程流程维护。

### 5. 功能需求趋势
*   **Agent 行为“可视化与可控化”双轨并行**：PR #2471（Monitor 流式查看）与 PR #2466（强制打断死循环）共同描绘了社区的新诉求——不要将 Agent 视为不可知的“黑箱”。开发者希望在工具执行时拥有**实时的感知能力**，在出现异常时拥有**紧急制动能力**。这是 Agent 迈向生产级成熟度的标志。
*   **MCP 生态转向“深度运营”**：早期的“能连上 MCP”已不再满足需求。从 #2457（删除后仍残留）到 #2469（路径隔离失败），社区焦点已转向 MCP 服务器的**全生命周期管理**和**多租户环境隔离**。CLI 需要变得像 IDE 管理扩展一样去管理 MCP。
*   **严格协议合规成为标配**：#2465 的 `reasoning_effort: null` 问题表明，Kimi CLI 的用户群体正在从 Moonshot 专有模型向更广泛的 API 兼容生态扩散。Kosong 层输出的标准合规性，直接决定了第三方用户能否“无感”接入。

### 6. 开发者关注点
*   **MCP 配置管理是最大痛点**：无论是自动恢复被删除的配置（#2457），还是工作区路径错误（#2469），都指向 CLI 的**配置持久化与上下文解析**层存在严重缺陷。开发者需要一个可靠稳定的 MCP 配置机制，这是当前排在第一位的诉求。
*   **稳定性压倒一切**：子进程调用挂起（#2468）和 Agent 自动进入死循环（#2466 修复背景）是开发者最害怕的场景——既浪费时间又消耗 Token。AI 辅助编码工具的“可靠性”比“智能”更重要。
*   **开源兼容性与面向第三方**：用户正在将 Kimi CLI 接入本地模拟器、严格 OpenAI 模式 API。CLI 在“非主视觉”场景下的兼容性，将直接影响其在开源社区的渗透速率。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是根据截至 2026-06-23 的 GitHub 数据生成的 OpenCode 社区动态日报。

---

## OpenCode 社区动态日报 (2026-06-23)

### 1. 今日速览
昨日社区动态密集，**稳定性问题**成为最突出的关键词：Worker 进程异常终止、服务端内存膨胀至 26.8 GiB、以及随机 CPU 100% 等问题严重影响使用体验。功能层面，**工作流引擎 (Workflow Engine)** 核心代码通过 4 个 PR 完成初步拆解合并，标志着大型特性逐步落地；同时，**MCP 图像附件返回失效**（#32832）的回归引发了用户对版本质量的普遍担忧。

### 2. 版本发布
无（过去 24 小时无新版本发布）。

### 3. 社区热点 Issues（10 条）

1.  **[#32832] MCP 工具无法返回图像附件**
    - **链接**: https://github.com/anomalyco/opencode/issues/32832
    - **重要性**: 这是一个严重的回归问题。在 `v1.17.5+` 版本中，MCP 工具处理结果若包含图片，将无法被正确渲染，导致依赖图像输出的工具链完全失效。社区希望借此推动更完善的回归测试机制。

2.  **[#28567] 【功能请求】：完整 MCP 客户端能力**
    - **链接**: https://github.com/anomalyco/opencode/issues/28567
    - **重要性**: 获得 24 👍，是社区呼声最高的功能之一。用户期望 OpenCode 的 MCP 客户端功能完全对齐最新 MCP 标准，以充分利用模型上下文协议生态的潜力。

3.  **[#4489] 【功能请求】：`opencode run` 支持临时一次性会话**
    - **链接**: https://github.com/anomalyco/opencode/issues/4489
    - **重要性**: 获得 12 👍。用户希望 `opencode run` 能支持不持久化到本地存储的临时会话，这对于脚本化、CI/CD 等自动化场景至关重要，提议者已表示愿意协助实现。

4.  **[#18969] 【功能请求】：增加 TUI 底部状态栏持久化显示插件钩子**
    - **链接**: https://github.com/anomalyco/opencode/issues/18969
    - **重要性**: 当前 Token/TPS 监测等插件只能通过短暂弹窗（Toast）显示状态，在专注工作时造成干扰。该提案旨在新增一个持久性的状态栏模板系统，提升 TUI 信息传达质量。

5.  **[#30697] 移动项目文件夹后，OpenCode 仍导航至旧路径**
    - **链接**: https://github.com/anomalyco/opencode/issues/30697
    - **重要性**: 一个常见但影响较大的工作流 Bug。用户移动或删除项目后，即使重新打开新路径，OpenCode 仍可能读取已失效的旧路径，导致逻辑混乱和数据不可见。

6.  **[#33466] OpenCode 响应极其缓慢**
    - **链接**: https://github.com/anomalyco/opencode/issues/33466
    - **重要性**: 用户反馈无论切换什么模型、在什么网络环境下，OpenCode 服务端的响应都非常慢，甚至不响应。影响范围较广，急需排查是否是服务端端的通用性能瓶颈。

7.  **[#32694] Bug: Worker 进程被终止**
    - **链接**: https://github.com/anomalyco/opencode/issues/32694
    - **重要性**: TUI 模式下，用户发送一次消息并收到回复后，Worker 进程立即崩溃，导致会话不可用。经用户缩小范围排查，该问题与具体 Model 或插件无关，对核心交互体验破坏性极强。

8.  **[#31932] 【功能请求】：TUI 跨项目会话选择器**
    - **链接**: https://github.com/anomalyco/opencode/issues/31932
    - **重要性**: 现有 `/sessions` 命令只限于当前项目，对于在多仓库间切换的开发者来说，无法集中管理和查找所有会话，严重降低了工作效率。

9.  **[#32574] 工具调用的开始时间报告错误？**
    - **链接**: https://github.com/anomalyco/opencode/issues/32574
    - **重要性**: 用户观察到 Timing 块报告的 Start 和 End 时间间隔异常接近，怀疑是“开始时间”重置逻辑存在缺陷。这直接影响了用户对 Token 消耗、响应延迟等性能监控数据的信任度。

10. **[#15886] 【功能请求】：限制性 AI 审计策略**
    - **链接**: https://github.com/anomalyco/opencode/issues/15886
    - **重要性**: 用户强烈期望在 Desktop 和 TUI 中集成原生的 Git 状态面板，以替代“请 AI 显示状态”或手动终端操作，是 OpenCode 从问答工具向 IDE 进化的关键拼图。

### 4. 重要 PR 进展（10 条）

1.  **[#32390 ~ #32394] 工作流引擎拆分合入 (4个PR)**
    - **链接**: #32390
    - **内容**: 将超大工作流 PR（#29789）成功拆分为引擎核心、服务端路由、TUI 对话框、Web 应用四个独立的 PR。工作流功能是 OpenCode 近期最大规模的架构革新，该批次代码合入标志着重大进展。

2.  **[#33310] 功能: Bash 工具支持后台运行**
    - **链接**: https://github.com/anomalyco/opencode/pull/33310
    - **内容**: 新增 `run_in_background` 参数，允许模型将 Bash 命令放入后台执行。解决了长时间阻塞命令的痛点，并修复了 `maxOutput` 溢出截断的问题。

3.  **[#33448] 修复: TUI Worker 进程拒绝处理**
    - **链接**: https://github.com/anomalyco/opencode/pull/33448
    - **内容**: 补回了在日志迁移过程中被意外移除的 `unhandledRejection` 监听器，防止 Worker 内部的 Promise 拒绝直接导致整个 Worker 被 Bun 终止。

4.  **[#33281] 功能: CLI 独立 V2 会话流程**
    - **链接**: https://github.com/anomalyco/opencode/pull/33281
    - **内容**: 新增 `--standalone` 模式，通过启动私有服务器子进程来运行 TUI，并基于 V2 API 创建和管理会话，重构了 CLI 的会话生命周期。

5.  **[#30685] 修复: 导航时忽略失效的项目路径**
    - **链接**: https://github.com/anomalyco/opencode/pull/30685
    - **内容**: 修复了 #30462 中提及的项目目录迁移后路径错乱的问题。PR 通过过滤已知的失效项目根目录，确保应用能正确导航到新路径。

6.  **[#33445] 功能: SDK 新增 HttpApi 客户端代码生成器**
    - **链接**: https://github.com/anomalyco/opencode/pull/33445
    - **内容**: 新增私有 `@opencode-ai/httpapi-codegen` 工具，能直接从 Effect HttpApi 合约生成类型安全的客户端，支持 Effect 或纯 Promise/fetch 两种输出模式。

7.  **[#33462] 功能: Copilot 插件上下文选择暴露**
    - **链接**: https://github.com/anomalyco/opencode/pull/33462
    - **内容**: 当 GitHub 同时提供默认和长上下文两种 Copilot 模型时，插件现在可以暴露该选择，并基于不同的 Token 价格进行准确定价。

8.  **[#33454] Http-recorder 工具独立 Beta 发布准备**
    - **链接**: https://github.com/anomalyco/opencode/pull/33454
    - **内容**: 将 `@opencode-ai/http-recorder` 从主版本同步中解耦，赋予其独立的 `0.1.0` 版本生命周期，方便该工具独立迭代和 Beta 测试。

9.  **[#32301] 功能: 嵌套子 Agent 生成 (支持5层深度)**
    - **链接**: https://github.com/anomalyco/opencode/pull/32301
    - **内容**: 允许子 Agent 再生成自己的子 Agent，深度上限为 5 层。同时修复了当前版本中从第二层向第三层过渡失败的 Bug，进一步优化了多代理协作架构。

10. **[#33464] 修复: 使用 collectBoundedResponseBody 处理 Websearch SSE**
    - **链接**: https://github.com/anomalyco/opencode/pull/33464
    - **内容**: 修复了内建 `websearch` 工具返回 HTTP 400 错误的问题。根因在于 Websearch 的返回流是 SSE，而现有代码错误使用了 `response.text()` 导致解析失败。

### 5. 功能需求趋势

-   **集成化**：社区不再满足于单纯的 CLI 问答，强烈要求内建 Git 面板、文件差异比较器、状态栏自定义等传统 IDE 功能。
-   **工作流自动化**：工作流引擎的落地是近期最大期待点，配合后台 Bash 执行、嵌套代理等功能，OpenCode 正从“助手”转变为“自动任务执行器”。
-   **MCP 生态深化**：全面支持最新 MCP 标准成为刚需，特别是多模态内容（如图像）的传递能力，以及更强大的客户端/插件 API。
-   **模型与 Provider 精细化**：除了新增接口兼容的 Provider（Mistral, Together AI），用户开始关注更细粒度的模型管理，如上下文窗口选择、Token 精准计费、Rate Limit 中间件等。
-   **数据安全与透明度**：误删文件保护、会话数据跨版本迁移、明确的订阅与计费系统，正从“加分项”变为“基本盘”。

### 6. 开发者关注点

-   **稳定性瓶颈亟待解决**：`Worker 进程终止`、`服务端内存泄漏`、`CPU 100%` 是近期的“高频三连”，即便功能开发快速，核心体验的稳定性滑坡正在快速消耗用户信任。
-   **版本质量与回归测试**：MCP 图像附件、插件静默失效等问题的出现，表明部分核心路径缺乏有效的端到端回归测试。社区期待看到更健壮的 CI/CD 流程和 Beta 测试机制。
-   **数据与路径一致性**：项目迁移后路径失效、历史会话不可用、文件被意外删除且无法恢复，这些问题让用户对自己的数据安全感到不安。
-   **平台兼容性鸿沟**：Windows 下的高负载桌面包冻结、中文汉化不到位、Linux Server 模式下的内存膨胀等，表明跨平台（特别是非 macOS）的优化存在显著滞后。
-   **计费与订阅逻辑**：订阅续费失败导致金额被冻结、Copilot Token 计价不准确，这类经济层面的 Bug 对用户信任的打击尤为直接。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，这是为您生成的 2026-06-23 Pi 社区动态日报。

---

# 2026-06-23 Pi 社区动态日报

**数据来源:** github.com/badlogic/pi-mono

## 今日速览

- **连接可靠性成为焦点：** openai-codex 和 GPT-5.5 的“挂起”问题（#4945）持续发酵，已获 64 条评论，成为社区最关注的问题点。
- **Hook 生态迈出一大步：** `v0.79.10` 发布，为 `session_before_compact` 和 `session_compact` 事件添加了触发原因和重试信息，开发者现在可以区分手动压缩与自动压缩，相关 PR 已合并。
- **Provider 拓展持续活跃：** Merge Gateway 和 DeepSeek 自动路由扩展等新 Provider 相关 PR 被合并，显示社区对底层模型选择的灵活性与成本优化需求旺盛。

## 版本发布

- **v0.79.10**
    - **核心特性：** 扩展了 `session_before_compact` 和 `session_compact` 的事件上下文。现在事件会携带 `reason`（手动/阈值/溢出）和 `willRetry`（是否会重试）字段。这一变化让扩展能够精确判断触发压缩的原因，从而做出不同响应（例如，在溢出时清理缓存，而在手动压缩时跳过）。
    - **影响：** 解决了 #5217 中提出的痛点，完善了 Pi 上下文管理相关的扩展API。
    - **链接:** [Release v0.79.10](https://github.com/earendil-works/pi/releases/tag/v0.79.10)

## 社区热点 Issues

1.  **[#4945] (openai-codex) 连接可靠性问题**
    - **重要性：** **最高热度🔥** 高达 64 条评论，是当前社区痛点最集中的问题。用户报告与 `openai-codex` / `gpt-5.5` 的交互中，TUI 会卡在“Working...”界面，无响应无错误，只能通过 Esc 强制中断。这表明与 OpenAI 新模型的流式连接存在严重的不稳定性。
    - **社区反应：** 用户普遍在寻找变通方案，开发者也在积极跟进，标签为 `[inprogress]`。
    - **链接:** [Issue #4945](https://github.com/earendil-works/pi/issues/4945)

2.  **[#3357] 官方本地 LLM Provider 扩展**
    - **重要性：** **最受期待功能👍** 获得 36 个 👍，虽非新 Issue，但在持续更新中。核心诉求是让 Pi 能动态获取本地 LLM 服务（如 llama.cpp、Ollama、LM Studio）的模型列表，而非手动配置。这是推动 Pi 向本地优先和私有化部署发展的重要一步。
    - **社区反应：** 用户积极讨论实现方案，期望能无缝对接本地模型生态。
    - **链接:** [Issue #3357](https://github.com/earendil-works/pi/issues/3357)

3.  **[#5653] 移除 Shrinkwrap 依赖锁定**
    - **重要性：** **核心架构问题🔥** 由于 `shrinkwrap` 导致 `pi-ai` 等核心包出现重复安装，使得模块级的 `Map` 单例模式失效，影响 Provider 注册等核心功能。这个问题触及了 Pi 的包管理和模块隔离机制。
    - **社区反应：** 开发者正在讨论重构方案，标签 `[to-discuss]`，社区高度关注如何解决。
    - **链接:** [Issue #5653](https://github.com/earendil-works/pi/issues/5653)

4.  **[#5916] 支持 Provider 扩展的模型别名并改进搜索**
    - **重要性：** **用户体验痛点** 用户在 `models.json` 中配置了模型别名，但 Pi 的 UI 和搜索功能未能识别，导致配置失效。这暴露了对 OpenRouter 等代理 Provider 的模型配置和发现机制不完善。
    - **社区反应：** 用户认为当前的配置体系对 Provider 和模型的管理不够直观。
    - **链接:** [Issue #5916](https://github.com/earendil-works/pi/issues/5916)

5.  **[#5571] `pi -p` 在非 TTY 管道下无限挂起**
    - **重要性：** **严重 Bug** 当 `stdin` 是一个永不关闭的非 TTY 管道时，`pi -p` 命令会无限期挂起。这直接破坏了 CI/CD 或自动化脚本中调用 Pi 的场景。
    - **社区反应：** 用户指出该问题导致进程无法正常退出，影响自动化工作流的稳定性。
    - **链接:** [Issue #5571](https://github.com/earendil-works/pi/issues/5571)

6.  **[#5778] `pi-agent-core` 在流断开或工具执行死锁时挂起**
    - **重要性：** **核心稳定性风险🔥** 这是一个严重的代码级漏洞。当 LLM Provider 流意外断开或工具的 `execute()` 函数无法完成时，agent 主循环会“卡死”而没有任何超时或错误处理机制。
    - **社区反应：** 社区强调这是生产环境下的致命问题，需要引入超时和断线重连机制。
    - **链接:** [Issue #5778](https://github.com/earendil-works/pi/issues/5778)

7.  **[#5291] 使用 Anthropic 订阅时会话卡在 "Working..."**
    - **重要性：** **与大型Provider集成问题** 用户反馈使用 Anthropic Enterprise 订阅时，会话间歇性卡死。该问题与 #4945 类似，表明 Pi 与主流 LLM Provider 的流式交互普遍存在稳定性挑战。
    - **社区反应：** 用户尝试通过中断/恢复解决，但并非总是有效，影响使用体验。
    - **链接:** [Issue #5291](https://github.com/earendil-works/pi/issues/5291)

8.  **[#4748] `pi-tui` 的键绑定单例问题**
    - **重要性：** **扩展开发障碍** 由于 `pi-tui` 键绑定模块使用单例模式，当扩展加载时，它们解析的 `pi-tui` 实例与 Pi 核心的实例不同，导致扩展无法正确读取或修改键绑定。这是扩展机制的一个缺陷。
    - **社区反应：** 扩展开发者认为这限制了扩展对 TUI 的深度自定义能力。
    - **链接:** [Issue #4748](https://github.com/earendil-works/pi/issues/4748)

9.  **[#5871] Anthropic OAuth Token 检测硬编码**
    - **重要性：** **配置灵活性不足** Pi 目前通过硬编码的字符串 `sk-ant-oat` 来识别 Anthropic 的 OAuth Token。这不够灵活，无法支持自定义或未来可能变化的 Token 格式。社区呼吁提供显式的 `authMode` 配置选项。
    - **社区反应：** 开发者认为应当通过模型/Provider配置明确声明认证模式，而非依赖字符串检测。
    - **链接:** [Issue #5871](https://github.com/earendil-works/pi/issues/5871)

10. **[#5751] 扩展 API 中的 `sendMessage` 不返回 Promise**
    - **重要性：** **扩展API设计缺陷** `pi.sendUserMessage()` 等 API 没有正确返回 Promise，导致 `await` 无法等待操作完成，特别是在 print 模式下会变成“发射后不管”，造成消息丢失或顺序错乱。
    - **社区反应：** 基于 Pi 构建工具的开发者因此无法实现可靠的链式消息处理。
    - **链接:** [Issue #5751](https://github.com/earendil-works/pi/issues/5751)

## 重要 PR 进展

1.  **[#5987] fix(coding-agent): 通过身份守护进程按 agent 名称解析 session**
    - **重要性：** **修复 / 功能完善** 解决了 `--session` 参数无法识别 agent 名称的问题，使得可以根据语义化的 agent 名称（如 `lucid-gecko-24`）来恢复会话，而不是仅能使用文件路径。
    - **链接:** [PR #5987](https://github.com/earendil-works/pi/pull/5987)

2.  **[#5985] feat(ai): 添加 Merge Gateway Provider**
    - **重要性：** **新 Provider 支持** 正式将 Merge Gateway 作为内置的 OpenAI 兼容 Provider 加入。用户只需一个 API Key 即可访问 40+ 个模型，显著降低了使用多模型的门槛。
    - **链接:** [PR #5985](https://github.com/earendil-works/pi/pull/5985)

3.  **[#5962] feat(coding-agent): 为扩展的压缩事件添加 reason 和 willRetry**
    - **重要性：** **核心功能增强** （与 v0.79.10 发布对应）此 PR 实现并合并了为 `session_before_compact` 和 `session_compact` 事件添加 `reason` 和 `willRetry` 字段的功能。这是社区强烈要求的功能，增强了扩展对上下文管理控制的能力。
    - **链接:** [PR #5962](https://github.com/earendil-works/pi/pull/5962)

4.  **[#5977] feat(ai): 允许为 Anthropic Provider 显式设置 authMode**
    - **重要性：** **修复 / 配置增强** 作为对 #5871 的回应，此 PR 引入了 `authMode` 标志，允许用户和 Provider 定义明确指定 API Key 是普通 Key 还是 OAuth/Bearer Token，取代了之前不稳定的硬编码检测。
    - **链接:** [PR #5977](https://github.com/earendil-works/pi/pull/5977)

5.  **[#5981] Linkify plain URLs in Text output**
    - **重要性：** **TUI 体验改进** 解决了 #5978 中提出的长 URL 在 TUI 中换行后无法点击的问题。此 PR 实现 OSC 8 超链接支持，让 TUI 中的裸链接变得可点击，大幅提升了交互体验。
    - **链接:** [PR #5981](https://github.com/earendil-works/pi/pull/5981)

6.  **[#5859] fix(ai): 将 Responses 类型的 prompts 作为 instructions 发送**
    - **重要性：** **核心 Bug 修复** 修复了 OpenAI Responses API 调用时 System Prompt 的发送方式。此前将其放入 `input` 消息中，不符合 API 规范，可能导致行为异常。现在正确地将其放入顶级 `instructions` 字段。
    - **链接:** [PR #5859](https://github.com/earendil-works/pi/pull/5859)

7.  **[#5262] feat(ai): 添加 Anthropic Vertex Provider**
    - **重要性：** **新 Provider 支持** 此 PR 长期处于开放状态，旨在为 Google Cloud Vertex AI 上的 Claude 模型提供原生支持。一旦合并，将拓宽 Pi 在企业级 Google Cloud 生态中的应用。
    - **链接:** [PR #5262](https://github.com/earendil-works/pi/pull/5262)

8.  **[#5970] feat: 添加用于 DeepSeek V4 Pro/Flash 成本优化的自动路由扩展**
    - **重要性：** **创新扩展** 实现了一个智能路由扩展，可根据任务复杂度在 DeepSeek V4 Flash（简单/便宜）和 V4 Pro（复杂/昂贵）之间自动切换，旨在为用户节省 60-70% 的 API 成本。
    - **链接:** [PR #5970](https://github.com/earendil-works/pi/pull/5970)

9.  **[#5963] fix(ai): 拒绝格式错误的最终工具调用参数**
    - **重要性：** **稳定性提升** 在 AI 流处理路径中增加了对最终工具调用参数 JSON 合法性的校验。防止因模型生成错误格式的 JSON 导致的崩溃或未知错误，并将其作为明确的错误类型处理。
    - **链接:** [PR #5963](https://github.com/earendil-works/pi/pull/5963)

10. **[#5526] Require terminal events for OpenAI Responses streams**
    - **重要性：** **连接稳定性修复** 针对 #4945 中提到的流不完整问题，此 PR 强制要求 OpenAI Responses 流必须以终端响应事件结束。这是一种防御性编程，确保会话不会在非正常结束状态下卡住。
    - **链接:** [PR #5526](https://github.com/earendil-works/pi/pull/5526)

## 功能需求趋势

从过去24小时的 Issues 和 PR 来看，社区最关注的功能方向集中在以下三个方面：

1.  **扩展性与平台化：** 社区不再满足于基础功能，而是深度要求 Pi 成为一个可扩展的平台。这体现在对 `ExtensionContext`、`ExtensionCommandContext` 等 API 的持续完善（#4748, #5932, #5810, #5912, #5952），以及对包管理和模块隔离的架构改进（#5653）。
2.  **连接健壮性与错误处理：** 多数高热度 Issue 直指连接问题。社区强烈要求引入超时机制、流式连接状态监控、自动重试和优雅的错误降级策略（#4945, #5778, #5571, #5291），以确保 Pi 在与各种 LLM Provider 交互时的稳定性。
3.  **Provider 生态的丰富与配置灵活性：** 社区一方面通过 PR 和新 Issue 积极引入更多 Provider（Merge Gateway, Anthropic Vertex, Neuralwatt等），另一方面要求 Provider 配置更加灵活，例如支持模型别名、动态获取模型列表、以及更智能的认证模式检测（#3357, #5916, #5871, #5965）。成本优化也是重要考量（#5970）。

## 开发者关注点

- **API 连接稳定性是首要痛点：** `openai-codex` 和 Anthropic 的“Working...” 无响应问题是开发者最频繁遇到的障碍，严重影响了 TUI 的使用体验和自动化流程的执行。
- **扩展 API 的完善性是开发瓶颈：** 扩展开发者普遍感到 `ExtensionContext` 提供的 API 不够用，尤其在会话管理（创建、切换、导航、替换）和访问底层数据（Session Entries、Tree）方面存在制约，导致许多高级扩展功能难以实现。
- **配置和认证机制需要简化：** 硬编码的 Token 检测、复杂的 `models.json` 覆盖语法、以及对 Provider 模型发现机制的缺失，增加了使用和配置的复杂度。开发者希望 Pi 能提供更智能、更统一的配置管理方式，尤其是对 OpenRouter 这类聚合 Provider。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，以下是为您生成的 Qwen Code 社区动态日报。

---

# Qwen Code 社区动态日报 | 2026-06-23

## 今日速览
今日社区焦点集中在一系列由 `tt-a1i` 提交的**类型安全与输入验证修复**上，涉及 CLI、LSP 及核心配置，显著提升了项目健壮性。同时，`yiliang114` 提交了 CI 流水线硬性优化，目标是解决合并阻塞问题。功能方面，社区对 **MCP 动态热重载**、**工具输出统一**和**图片理解桥接**的 PR 讨论热烈。

## 社区热点 Issues (10 条)
1.  **#3877 [bug] .env 文件中的 API Key 未被正确读取** (👍1, 评论5)
    - **重要性**: 影响初始配置体验，多用户反馈 `qwen` 命令启动时未正确读取 `~/.qwen/.env` 中的 `OPENCODE_GO_API_KEY`，强制用户二次选择认证方式。
    - **链接**: [Issue #3877](https://github.com/QwenLM/qwen-code/issues/3877)

2.  **#5656 [feature] 将工具调用摘要移至 Loading 指示器** (评论5)
    - **重要性**: UI 优化提议。当前工具调用摘要（如“修复 NPE...”）会作为独立消息出现在历史记录中，用户希望将其压缩至加载动画旁，减少对对话流的干扰，反应了社区对**界面简洁性**的追求。
    - **链接**: [Issue #5656](https://github.com/QwenLM/qwen-code/issues/5656)

3.  **#4814 [feature] 为自定义提供商用户简化模型添加流程** (评论5)
    - **重要性**: 持续的用户体验优化。用户吐槽首次设置自定义 Provider 时，模型添加流程繁琐且不直观，希望 UI 能像第三方提供商一样提供更流畅的发现与添加机制。
    - **链接**: [Issue #4814](https://github.com/QwenLM/qwen-code/issues/4814)

4.  **#5641 [bug] Qwen Code 在特定 Provider 下重复提交已完成的 Shell 工具结果** (评论4)
    - **重要性**: 严重影响使用体验的 Bug。在特定与 OpenAI 兼容的 Provider 下，工具调用结果会被模型反复提交，导致对话逻辑混乱和工作流卡死。
    - **链接**: [Issue #5641](https://github.com/QwenLM/qwen-code/issues/5641)

5.  **#5713 [bug] Alacritty 终端下半透明光标** (评论4)
    - **重要性**: 特定终端兼容性 Bug。在Alacritty 下，光标渲染为半透明，影响输入定位。虽然只影响特定环境，但表明社区对**终端 UI 兼容性**要求较高。
    - **链接**: [Issue #5713](https://github.com/QwenLM/qwen-code/issues/5713)

6.  **#5690 [#5700 #5704 #5710 等] [bug] 一系列数值/整数参数校验问题**
    - **重要性**: 这是一组由 `tt-a1i` 提交的关于输入校验的 Bug，涉及 LSP 最大重启次数、分页查询参数、会话列表限制、Session 数量限制、文件偏移量等。它们共同暴露了系统在**输入健壮性**上的薄弱环节，可能导致潜在的静默错误。
    - **参考链接**: [Issue #5690](https://github.com/QwenLM/qwen-code/issues/5690)，[Issue #5700](https://github.com/QwenLM/qwen-code/issues/5700)，[Issue #5704](https://github.com/QwenLM/qwen-code/issues/5704)，[Issue #5710](https://github.com/QwenLM/qwen-code/issues/5710)

7.  **#5611 [bug] web_fetch 无法获取 JSON API (HTTP 415)** (评论3)
    - **重要性**: 工具功能缺失。`web_fetch` 工具由于仅发送 `text/*` 的 Accept 头，导致无法正确请求仅返回 JSON 的 RESTful API（如 GitHub API），严重限制了其作为通用网页抓取工具的实用性。
    - **链接**: [Issue #5611](https://github.com/QwenLM/qwen-code/issues/5611)

8.  **#5683 [bug] 子 Agent Token 计数异常偏高** (评论3)
    - **重要性**: 计费/配额核验问题。用户反馈运行本地模型时，子 Agent 的 Token 消耗显示远超允许值，可能导致用户对计费模型产生疑虑。
    - **链接**: [Issue #5683](https://github.com/QwenLM/qwen-code/issues/5683)

9.  **#5734 [bug] Fork 子 Agent 的权限控制工具调用被静默拒绝** (评论2)
    - **重要性**: 核心Agent功能缺陷。`/fork` 产生的子 Agent 在执行需要用户确认的权限操作时，请求未被正确传递到父会话 UI，而是被静默拒绝，导致任务静默失败。
    - **链接**: [Issue #5734](https://github.com/QwenLM/qwen-code/issues/5734)

10. **#5634 [bug] autofix 流程信任可被 Issue 内容影响的标签** (评论4)
    - **重要性**: **安全/流程风险**。自动化修复流水线信任了一个来自LLM的标签判断，而LLM的判断可能被恶意的 Issue 描述文本操控，存在被滥用的风险。
    - **链接**: [Issue #5634](https://github.com/QwenLM/qwen-code/issues/5634)

## 重要 PR 进展 (10 条)
1.  **#5732 [PR] CI: 硬性化 Test 检查**
    - **内容**: 通过使用 PR head 而非 merge ref 签出代码，并释放并发槽位，修复了 `Test (ubuntu-latest)` 阻塞合并的问题，是保障**开发流程顺畅**的关键基础设施优化。
    - **作者**: `yiliang114`
    - **链接**: [PR #5732](https://github.com/QwenLM/qwen-code/pull/5732)

2.  **#5589 [PR] 文档与当前 CLI 行为对齐**
    - **内容**: 全面刷新了 MCP 管理、扩展设置、主题、Sandbox 链接、SDK 权限选项等文档，以匹配最新 CLI 行为，有助于**降低新用户上手门槛**。
    - **作者**: `doudouOUC`
    - **链接**: [PR #5589](https://github.com/QwenLM/qwen-code/pull/5589)

3.  **#5126 [PR] 视觉桥接：为纯文本模型转录图片**
    - **内容**: 允许用户在提示中 `@` 引用图片，该 PR 将图片发送给同 Provider 下具备视觉能力的模型进行理解，并将结果文本传给主模型。**社区高度期待的功能**，极大地扩展了模型生态。
    - **作者**: `yiliang114`
    - **链接**: [PR #5126](https://github.com/QwenLM/qwen-code/pull/5126)

4.  **#5733 [PR] 按名称匹配 MCP 资源补全**
    - **内容**: 改进对话内 `@server:uri` 的 MCP 补全体验，支持不区分大小写的模糊搜索，并可发现提供补全数据的服务器。这是对**MCP交互体验**的重要增强。
    - **作者**: `wenshao`
    - **链接**: [PR #5733](https://github.com/QwenLM/qwen-code/pull/5733)

5.  **#5730 [PR] 桌面端：文件预览改为可调整大小的侧面板**
    - **内容**: 将桌面端全屏文件预览改为可拖拽的右侧面板，保持对话和文件树可见，**明显优化了多任务处理体验**。
    - **作者**: `DragonnZhang`
    - **链接**: [PR #5730](https://github.com/QwenLM/qwen-code/pull/5730)

6.  **#5661 [PR] TUI: 统一工具输出与语义摘要**
    - **内容**: 用统一的模式取代了紧凑/正常双模式。已完成工具总是显示语义摘要（如 “Read 3 files， edited 2 files”）而非原始结果。**大幅提升日志可读性**。
    - **作者**: `chiga0`
    - **链接**: [PR #5661](https://github.com/QwenLM/qwen-code/pull/5661)

7.  **#5561 [PR] MCP 热重载：设置变动时即时刷新**
    - **内容**: 解决了 Issue #3696 的关键子任务。编辑 `settings.json` 中的 `mcpServers` 后，不再需要重启即可生效，是**MCP管理体验的重大飞跃**。
    - **作者**: `water-in-stone`
    - **链接**: [PR #5561](https://github.com/QwenLM/qwen-code/pull/5561)

8.  **#5616 [PR] 技能确认：在持久化前确认自动生成的技能**
    - **内容**: 允许用户在自动生成的技能被加入技能库前进行审核，避免错误或无用的技能被自动保存。增强了**对Agent自主行为的可控性**。
    - **作者**: `LaZzyMan`
    - **链接**: [PR #5616](https://github.com/QwenLM/qwen-code/pull/5616)

9.  **#4242 [PR] 修复：回滚映射在压缩后的表现**
    - **内容**: 在对话压缩后，正确映射回滚目标。解决了一个因压缩导致回滚位置错乱的**核心数据一致性问题**。
    - **作者**: `Jerry2003826`
    - **链接**: [PR #4242](https://github.com/QwenLM/qwen-code/pull/4242)

10. **#5660 [PR] 修复 core: 允许 web_fetch JSON 回退**
    - **内容**: 为 web_fetch 的 Accept 头添加一个低优先级 `*/*;q=0.1` 回退，在保留现有格式偏好的同时，解决了无法获取 JSON API 的 **#5611** Bug。
    - **作者**: `tt-a1i`
    - **链接**: [PR #5660](https://github.com/QwenLM/qwen-code/pull/5660)

## 功能需求趋势
从今日议题和PR中，可以提炼出社区关注的几个核心功能方向：
- **工具集成与交互优化**: 社区对工具调用的**结果展示方式**（摘要、通知栏）和**交互流程**（自动填补、统一展示）有极高热情，代表为 #5656 和 #5661。
- **模型兼容性与扩展**: 对**非标准 Provider** 和 **纯文本模型**的支持需求旺盛。如 #4814（自定义Provider体验）和 #5126（视觉桥接）都旨在扩大模型的适用场景。
- **输入健壮性与类型安全**: 以 `tt-a1i` 提交的大量 Bug 为代表，社区对**参数校验的严格性**要求升高，希望避免因小数、负值、非法字符串等输入导致系统行为异常。
- **配置与自动化便捷性**: 如 #5561（MCP热重载）和 #5616（技能确认），表明社区希望系统在自动化（如热更新、自动生成）的同时，提供更灵活、更安全的控制选项。
- **文档与上手体验**: #5589 文档对齐和 #4814 简化配置流程的呼声，表明社区希望**降低新用户的学习曲线**。

## 开发者关注点
- **配置与环境变量**: #3877 凸显了环境变量读取的痛点，开发者希望 `.env` 文件能被可靠地识别。
- **错误反馈与静默失败**: #5734 (fork子Agent静默拒绝)、#5641 (工具结果重复提交) 以及多个参数校验Bug，共同构成了对**清晰、准确错误反馈**的强烈诉求，静默失败是开发者最不希望看到的情况。
- **CI/CD 与发布流程**: #5634 的自动化流程安全问题与 #5732 的CI优化，反映了开发者对**可靠的自动化流水线**和**安全的贡献机制**的关注。
- **UI/UX 细节**: #5713 (光标问题)、#5656 (摘要位置) 等表明，即使是微小的终端UI细节问题，也会被用户迅速捕获并提出改进建议，社区对**界面打磨**要求很高。
- **会话与模型管理**: 多个关于 `list` 命令、`maxSessions`、分页等问题的修复，显示社区对**批量管理**和**资源限制**的机制敏感度较高，希望通过命令行实现精确控制。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-06-23 版 DeepSeek TUI（CodeWhale）社区动态日报。

---

# 2026-06-23 DeepSeek TUI 社区动态日报
**（CodeWhale v0.8.64 时代开启）**

---

## 1. 今日速览

- **正式更名！** 项目 `deepseek-tui` 正式宣布更名为 **CodeWhale**，v0.8.64 已发布，旧版 npm 包停止更新，迎来全新品牌时代。
- **v0.8.65 重构密集推进：** 多 Provider 路由、Fleet 子Agent 架构、Web Search 后端重构、以及状态存储安全加固多项 PR 今日密集合并或提交，项目架构进入深度洗牌期。
- **国产模型呼声高涨：** 社区对百度千帆、阿里百炼的原生支持需求极高，维护者 `Hmbown` 已快速响应并提交了相关路由 Fixture PR。

---

## 2. 版本发布

**v0.8.64 (CodeWhale)**
- **核心变更:** 项目正式更名。自此版本起，**CodeWhale** 为官方唯一项目名称、命令、npm 包及 Release 产物。旧版 `deepseek-tui` 包已弃用，不再接收新版本。
- **迁移建议:** 请旧版用户参考 `docs/REBRAND.md` 进行相关配置名称的迁移。
- [查看 Release](https://github.com/Hmbown/CodeWhale/releases)

---

## 3. 社区热点 Issues (Top 10)

1.  **[#3405] v0.8.67 Setup 设置向导**
    - **摘要**：维护者将 Provider/Model 设置列为“最高摩擦”的首步体验。计划利用 v0.8.65 的架构改造成果，打造包含目录选择、身份验证和健康检查的完整向导流程。
    - **链接**: [Issue #3405](https://github.com/Hmbown/CodeWhale/issues/3405)

2.  **[#3383] Provider 范围的模型候选 /model**
    - **摘要**：核心 UX 改进。确保 `/model`、选单及斜杠补全默认锁定在当前 Provider 范围内，防止单纯的模型名导致 Provider 静默切换，提升多 Provider 场景的操控性。
    - **链接**: [Issue #3383](https://github.com/Hmbown/CodeWhale/issues/3383)

3.  **[#3357] 百度千帆 Provider 路由 Fixture**
    - **摘要**：社区强烈要求支持百度千帆编程模型。用户汇报通过 `--provider` 无法正确配置 URL 和 API Key，请求将其作为自定义/一等 Provider 纳入路由架构。
    - **链接**: [Issue #3357](https://github.com/Hmbown/CodeWhale/issues/3357)

4.  **[#3320] 阿里百炼 API Key 与 Provider 接入**
    - **摘要**：用户汇报阿里云百炼 API Key 集成缺失，导致无法通过百炼进行调用。请求通过 Provider 描述符和路由架构支持百炼的认证方式。
    - **链接**: [Issue #3320](https://github.com/Hmbown/CodeWhale/issues/3320)

5.  **[#3154] Fleet 执行基座**
    - **摘要**：v0.8.65 核心史诗。将 Fleet 打造成 CodeWhale Worker 的持久化执行基座，与 #3167（Fleet 配置文件）和 #3205（Fleet 模型类）共同构成多 Worker 自动化的底层基础设施。
    - **链接**: [Issue #3154](https://github.com/Hmbown/CodeWhale/issues/3154)

6.  **[#2608] 分离 Provider/Model 事实与路由**
    - **摘要**：v0.8.65 另一核心史诗。切断模型字符串与路由的唯一绑定，彻底重构 Provider 识别、Model 识别、模型报价及路由选择，是本次大重构的基石。
    - **链接**: [Issue #2608](https://github.com/Hmbown/CodeWhale/issues/2608)

7.  **[#2900] SiliconFlow DSML 流式回归**
    - **摘要**：严重 Bug。在 Windows 上通过 `siliconflow-CN` 路由 `DeepSeek-V4-Pro` 时，DSML 工具调用标记可能作为普通文本流式输出，而非正常解析为工具调用。
    - **链接**: [Issue #2900](https://github.com/Hmbown/CodeWhale/issues/2900)

8.  **[#3289] Fleet Worker 与 TUI 冻结回归**
    - **摘要**：可靠性问题。当自动生成多个 Fleet/Subagent Worker 时，TUI 输入、渲染和取消会完全冻结，严重影响多 Worker 场景下的使用体验。
    - **链接**: [Issue #3289](https://github.com/Hmbown/CodeWhale/issues/3289)

9.  **[#3079] 使 Web Search 可靠**
    - **摘要**：功能增强。尽管 Agent 宣称正在搜索网页，但结果往往“不可见或不可靠”。提议基于 SearXNG（自托管元搜索引擎）JSON 后端构建 Web Search 能力，并增加健康检查与状态展示。
    - **链接**: [Issue #3079](https://github.com/Hmbown/CodeWhale/issues/3079)

10. **[#3031] 紧凑的工具调用转录呈现**
    - **摘要**：UX 优化。默认视图仅展示工具名、状态（成功/失败）和耗时，折叠冗长的 Shell 输出与空 `output` 行，大幅提高界面信息密度。
    - **链接**: [Issue #3031](https://github.com/Hmbown/CodeWhale/issues/3031)

---

## 4. 重要 PR 进展 (Top 10)

1.  **[#3425] feat(provider): 添加千帆路由 Fixture**
    - 响应 #3357，将百度千帆作为一等 OpenAI 兼容 Provider 引入。支持 `QIANFAN_API_KEY` / `QIANFAN_BASE_URL` 等环境变量及 `baidu-qianfan` 别名。
    - [PR #3425](https://github.com/Hmbown/CodeWhale/pull/3425)

2.  **[#3426] fix(tui): 接受 Together 托管的 DeepSeek 路由**
    - 修复 Together 路由验证失败问题，现在 Together 支持提供 DeepSeek V4 Pro 和 Flash 模型，通过 Together 作用域内的模型 ID 进行路由。
    - [PR #3426](https://github.com/Hmbown/CodeWhale/pull/3426)

3.  **[#3428] fix(tui): 将模型候选范围限定在活跃 Provider**
    - 直接实现 #3383。移除了旧的跨 Provider 切换提示，确保裸模型名不能作为 Provider 切换的权限，彻底锁定路由。
    - [PR #3428](https://github.com/Hmbown/CodeWhale/pull/3428)

4.  **[#3430] 添加配置化的 SearXNG Web Search 后端**
    - 实现 #3079 的核心部分。新增 `SearchProvider::Searxng`，允许用户指向可信/自托管的 SearXNG 实例，替代仅依赖 HTML 爬取或付费 API。
    - [PR #3430](https://github.com/Hmbown/CodeWhale/pull/3430)

5.  **[#3431] 固化 SiliconFlow DSML 回归 Fixture**
    - 针对 #2900 报告，为该 Bug 路径（`siliconflow-CN` + CN 基础 URL + `DeepSeek-V4-Pro` DSML）添加了显式的配置 Fixture 和测试，防止未来回归。
    - [PR #3431](https://github.com/Hmbown/CodeWhale/pull/3431)

6.  **[#3427] 固化 SiliconFlow TokenHub 路由诊断**
    - 针对 #2629，添加了 Provider 作用域的路由/认证/Base URL 回归 Fixture，确保 `siliconflow-CN` 和 TokenHub 风格 OpenAI 兼容网关的正确运行。
    - [PR #3427](https://github.com/Hmbown/CodeWhale/pull/3427)

7.  **[#3432] 提取共享桥接核心助手**
    - 代码重构。将 Telegram、飞书、企业微信 Node 集成中的重复桥接逻辑提取为共享的 `integrations/bridge-core` 包，保留各传输协议的本地行为。
    - [PR #3432](https://github.com/Hmbown/CodeWhale/pull/3432)

8.  **[#3433] 强化本地状态存储边界**
    - 安全加固。在写入 Task 工单及自动化存储时拒绝路径型 ID（path-shaped IDs），防止路径遍历及信息泄露风险。
    - [PR #3433](https://github.com/Hmbown/CodeWhale/pull/3433)

9.  **[#3422] 覆盖 OpenAI Codex/Responses 重试边界**
    - 测试扩充。泛化了已有的 Responses 重试测试工具，新增对 503 服务器错误的重试回归证明，提升 Codex/Responses 路由可靠性。
    - [PR #3422](https://github.com/Hmbown/CodeWhale/pull/3422)

10. **[#3327] 添加一等子Agent 开关**
    - 新增 `/config subagents on|off|status` 命令及 `features.subagents` 配置项，使用户能方便地在会话中即时控制子Agent 功能的开启与关闭。
    - [PR #3327](https://github.com/Hmbown/CodeWhale/pull/3327)

---

## 5. 功能需求趋势

- **多 Provider 路由架构大重构：** 社区已不满足于仅支持 DeepSeek 官方。`v0.8.65` 的史诗级重构（Provider/Model/Route 分离、Provider 回退链）反映了向“模型无关的 AI 终端”进化的强烈需求。
- **Agent 与工作流（Fleet）系统：** 利用子 Agent 实现自动化、多 Worker 协同是下阶段核心亮点，但稳定性（TUI 冻结、状态管理）仍是需要优先解决的门槛。
- **国产化与本地化生态接入：** 百度千帆、阿里百炼、小米 MiMo、SiliconFlow、Ollama/local LLM。社区用户的部署环境极度分化，提供灵活的 Provider 自定义配置成为刚需。
- **可观测性与透明度：** 开发者希望工具像一个“白盒”。`/provider` 仪表盘、Web Search 健康检查、前置错误提示、详尽的速率限制日志，是社区对专业级 AI 开发工具的普遍期待。
- **安全与隔离：** 沙箱（Linux/Windows 进程加固）、Secret 管理（Provider 作用域的 API Key）、状态存储边界检查。随着 Agent 获得执行能力，安全水位必须同步提升。

---

## 6. 开发者关注点

- **稳定性是最核心的痛点：** “Codewhale会自问自答”、“TUI 界面冻帧”、“Tool Call 流式解析错误”。开发者对高端 Agent 功能非常感兴趣，但前提是基础交互不能频繁崩溃。
- **配置复杂度激增带来的恐惧：** 从单一 Provider 到数十个 Provider 支持，配置模型名、API Key、Base URL 的复杂度几何级增长。开发者急需一个“强大的 Setup 向导”来降低学习与迁移门槛。
- **更名与版本迭代的迁移焦虑：** 从 `deepseek-tui` 到 `CodeWhale` 的更名，以及 `v0.8.65` 剧烈的架构变化，让部分老用户担忧升级成本过高。维护者在文档（REBRAND.md、配置示例）上的积极更新起到了很大的安抚作用。
- **开源协作氛围活跃：** `Hmbown` 响应极快，几乎每条热搜 Issue/PR 都在当天有跟进。同时社区贡献者（`hongqitai` 修复 Clippy、`pkeging` 提交企业微信集成）的活跃参与，表明该项目正展现出良好的社区生命力。
- **安全信仰的建立：** 从 Linux/Windows 沙箱到今天的路径形 ID 拒止（#3433），维护者在安全细节上的持续投入，正在逐步建立起开发者对 CodeWhale 作为生产工具的信心。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*