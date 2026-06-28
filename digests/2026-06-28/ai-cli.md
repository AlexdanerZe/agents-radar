# AI CLI 工具社区动态日报 2026-06-28

> 生成时间: 2026-06-28 03:30 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-06-28）

**生成时间：** 2026-06-28 · **数据来源：** GitHub Issues/PR 公开动态

---

## 1. 生态全景

当前 AI CLI 工具生态正从实验探索走向生产化基建，社区关注重心已从“能否生成代码”全面转向可靠性、成本可观测性、多平台兼容与安全护栏。一方面，模型升级引起的回归问题（如 Opus 4.7 Thinking 失效、额度暴涨等）让用户安全意识觉醒，对稳定性和透明度的诉求显著上升；另一方面，MCP 协议成为事实上的扩展标准，各工具在 OAuth、流式传输、容错等领域密集迭代。同时，跨设备协作、后台任务编排、编辑器深度融合等需求快速升温，竞争焦点正从模型智力比拼转向工程体验的全方位较量。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues（精选） | 重要 PR（24h） | 版本发布 | 最高赞/热议题 | 社区活跃标志 |
|------|------------------|--------------|--------|-------------|-------------|
| **Claude Code** | 10 | 2 | 0 | #49268: 👍75, 💬46 | Thinking 回归引爆讨论 |
| **OpenAI Codex** | 10 | 10 | 3 alpha | #28879: 👍334, 💬186 | 额度问题关注度极高 |
| **Gemini CLI** | 10 | 10 | 1 nightly | #21409: 👍8, 💬7 | 安全补丁密集合入 |
| **Copilot CLI** | 10 | 3 | 0 | #2165: 👍20 | Windows Bug 集中爆发 |
| **Kimi Code CLI** | – | – | – | – | 过去 24h 无活动 |
| **OpenCode** | 10 | 10 | 0 | #8816: 👍34, 💬15 | 技能/WSL 生态讨论活跃 |
| **Pi** | 10 | 8 | 0 | #5825: 💬34 | TUI 交互投诉集中 |
| **Qwen Code** | 10 | 10 | 1 nightly | #4175: 💬43 | 模型费用与持久化诉求强烈 |
| **DeepSeek TUI (CodeWhale)** | 10 | 10 | 0（release ledger） | #1177: 💬24 | 缓存优化与插件基础建设 |

注：Issues/PR 仅统计报告期内涉及的热点/重要条目，非仓库总量。

**综合判断：** OpenAI Codex 和 Claude Code 拥有最大社区影响力和讨论深度；Gemini CLI 和 Qwen Code 发布频率领先（nightly）；Copilot CLI 迭代节奏偏慢；Pi 和 OpenCode 在 TUI 与扩展性上社区反馈积极，CodeWhale 则以高频合入展现出强劲增长势头。

---

## 3. 共同关注的功能方向

多个工具社区不约而同聚焦以下六大方向：

| 方向 | 涉及工具 | 代表诉求 |
|------|---------|---------|
| **成本透明与消耗控制** | OpenAI Codex, Qwen Code, Claude Code, Gemini CLI | 额度暴涨、自动升档、Token 死循环、无限重试 — 均指向实时计量与熔断机制的缺失 |
| **跨平台与 ARM 兼容** | Claude Code, OpenAI Codex, Copilot CLI, OpenCode, Qwen Code | Windows ARM 引导失败、Linux 桌面原生应用呼声高、WSL 路径错误、高 CPU 占用 |
| **MCP 协议成熟度** | Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI | 指令截断、管道泄漏、MIME 类型探测错误、OAuth 刷新失败 — 从“能连”走向“稳连” |
| **Agent 行为可观测性** | Claude Code, Gemini CLI, OpenCode, Qwen Code, CodeWhale | 子代理误报成功、技能随机丢失、后台任务不可见、模式感知混乱 |
| **通知与异步化工作流** | Claude Code, Copilot CLI, Qwen Code | VS Code 通知、移动端推送、即时提问、Chrome 扩展 — 终端不应该是唯一界面 |
| **安全与隐私内建** | Gemini CLI, OpenAI Codex, Copilot CLI | DNS 重绑定防御、路径遍历修复、`.codexignore`、配置隔离 — 安全从附加走向标配 |

---

## 4. 差异化定位分析

- **Claude Code** — 聚焦最强推理可视化（Thinking），以 Opus 模型深度对话为卖点。Cowork 协作模式是独特优势，但对上游 API 变更敏感，模型回归问题频现。用户偏重度开发者，社区审美细腻。

- **OpenAI Codex** — 用户基数最大的官方 CLI，快速 alpha 迭代（日发 3 版本）。社区规模一骑绝尘，额度管理与平台扩展（Linux 桌面禁用了 4 年）是核心矛盾。PR 活跃，工程响应快，但积压需求也多。

- **Gemini CLI** — Google 血统，强调安全优先（当日 4 条安全 PR 合入）。子代理（Multi-Agent）架构是最大特色，但挂起/误报等问题凸显成熟度不足。夜版发布频繁，工程投入持续。

- **GitHub Copilot CLI** — 承载 GitHub Copilot 品牌，但社区规模偏小。功能趋于保守（alt‑screen 默认引发不满），PR 活跃度低，Windows 兼容问题集中爆发。需加速迭代以避免边缘化。

- **OpenCode** — 社区主导的开放工具，强调多模型兼容（GLM、NVIDIA NIM 等），但适配断层频现。WSL/Windows 是明显短板，技能系统有亮点但稳定性不足，社区讨论质量较高。

- **Pi** — 专注 TUI 交互质量与扩展 API。国际化支持缺失暴露盲区，但扩展接口设计（reportUsage、externalEditor）颇具前瞻性。社区偏向插件开发者和细粒度体验控。

- **Qwen Code** — 阿里系，面向生产场景：任务持久化、待办同步、多频道驻留 Agent（qwen tag）。是少数关注团队协作与跨设备工作流的工具，模型费用管理与后台任务控制是当前焦点。

- **DeepSeek TUI (CodeWhale)** — 从 TUI 出发，实质是编辑器（Zed/Cursor）的后端引擎（ACP 协议）。输入缓存命中率是最大痛点，插件系统与提示词可替换预示其向通用 AI 平台演进。

---

## 5. 社区热度与成熟度

**第一梯队（影响力+迭代双领先）：**  
- **OpenAI Codex**：最高赞 Issue 达 334👍，186 条讨论，社群规模最大。0.143.x-alpha 说明仍处快速迭代，但产品力逐步成型。
- **Claude Code**：#49268 引发超百条评论，社区深度高。虽无公开版本号，但模型回归类 issue 高发，表明用户基数大且对体验敏感。
- **Gemini CLI**：日发 nightly + 多条安全 PR，社区热情正在积累，但头部议题热度还不高（最高 8👍），处于用户群扩张期。

**第二梯队（特定方向快速追赶）：**  
- **OpenCode**：#8816（llms.txt）34👍，社区共识高。多模型兼容在吸纳多样用户群，但稳定性 issue 不少。
- **Qwen Code**：43 条评论的路线讨论➕频繁 nightly，团队协作特性差异化明显。
- **Pi**：#5825 TUI scroll bug 34 条讨论，扩展 API 兴趣持续增长，但国际化缺陷制约上限。

**第三梯队（亟需加速）：**  
- **Copilot CLI**：头部 issue 20👍，PR 仅 3 个且含实验性质，创新节奏放缓。若无法解决 Windows 生态短板，将逐渐边缘化。

**高速增长期：**  
- **CodeWhale**：v0.8.x，24h 合入 10 个重要 PR 含插件基础及 ACP 流式支持，社区贡献活跃，处于功能快速膨胀期。

---

## 6. 值得关注的趋势信号

1. **模型升级导致“预期退化”风险常态化**  
   Claude Code Opus 4.7 Thinking 失效、OpenAI Codex Responses-Lite 报错、Qwen Code 自动升档，均证明最强版本≠最佳体验。**开发者应建立模型评估矩阵与降级预案，工具厂商需完善升级兼容性测试。**

2. **Token 成本透明度从可选变为刚需**  
   额度暴涨、Auto Memory 无限重试、后台无声消耗 token 等事件表明，“成本无底洞”正在侵蚀用户信任。**实时计量、阈值告警、历史明细将成为 AI CLI 的基础功能。**

3. **安全左移 — Agent 安全性成为生产级准入门槛**  
   Gemini CLI 单日合入 4 条安全补丁（DNS 重绑定、路径穿越、环境变量泄露、Shell 参数扩展），标志 AI CLI 开始被按生产系统对待。**路径黑名单、命令确认、沙箱隔离等安全机制将成为差异化关键。**

4. **从“一人终端”到“团队工作流”演进**  
   Qwen Code 的多频道驻留 Agent、Claude Code 的 Cowork 权限面板、CodeWhale 的 ACP IDE 集成，说明**多用户协作、跨设备同步、工具链集成**正成为下一个竞争主战场。

5. **“CLI”不再是“终端”的同义词**  
   Claude Code 的 VS Code 扩展、OpenAI Codex 的桌面应用、Qwen Code 的 WebUI 和 Chrome 扩展、CodeWhale 作为编辑器后端 — **AI CLI 正在蜕变为智能代理引擎，前端可以是编辑器、浏览器、IM、移动设备。** 工具的品牌边界正在模糊，能力下沉成为趋势。

---

*本报告基于公开的 GitHub 动态生成，数据截至 2026-06-28 23:59 UTC，仅供决策参考。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是基于你提供的数据生成的 **Claude Code Skills 社区热点报告**。

---

# 📈 Claude Code Skills 社区热点报告（截至 2026-06-28）

## 1. 热门 Skills 排行

> 所有列出的 PR 当前均处于 **Open** 状态，显示出社区贡献非常踊跃，但审核合并流程可能存在瓶颈（也与下文提及的评估工具链崩溃有关）。

| 排名 | PR / Skill | 功能与社区焦点 | 状态 |
|---|---|---|---|
| 🔥 **1** | **[#1298]** **fix(skill-creator): run_eval.py** | **核心工具链修复**。`run_eval.py` 无论针对什么描述都报告 0% 召回率，导致优化循环完全对抗噪音。这是当前整个生态最严重的阻塞性 Bug。 | OPEN |
| 🔥 **2** | **[#514]** **document-typography** | **排版质量管控**。解决 AI 文档常见的孤词换行、段落孤行、编号错位等视觉硬伤。几乎没有争议的通用刚需。 | OPEN |
| 🔥 **3** | **[#486]** **OpenDocument (ODT)** | **企业开源办公**。填补了 LibreOffice/OpenOffice 原生格式支持的空白，社区对 ODF 国际标准格式的呼声很高。 | OPEN |
| 🔥 **4** | **[#83]** **skill-quality-analyzer / security-analyzer** | **元技能审查**。教 Claude 如何评估其他 Skill 的质量与安全性。代表社区对生态进行自检和治理的强烈意愿。 | OPEN |
| 🔥 **5** | **[#723]** **testing-patterns** | **全栈测试指南**。覆盖从测试哲学到 React/单元/集成测试的完整方法论，旨在规范 Claude 的输出质量。 | OPEN |
| 🔥 **6** | **[#360]** **appdeploy** | **代理式部署**。让 Claude 直接管理 Web 应用的全生命周期（部署、状态检查、回滚）。触及“从代码到上线”的 Agent 终局体验。 | OPEN |
| 🔥 **7** | **[#147]** **codebase-inventory-audit** | **代码治理**。提供系统化的 10 步工作流来识别僵尸代码、未使用文件和文档鸿沟。大型项目维护者的强力工具。 | OPEN |
| 🔥 **8** | **[#154]** **shodh-memory** | **持久记忆系统**。为长对话 Agent 提供跨会话的上下文检索能力。社区对“如何在上下文窗口外构建记忆”展开了深度讨论。 | OPEN |

## 2. 社区需求趋势

从 Issues 的高赞讨论中，可以提炼出社区最关注的五大方向：

1. **🚨 工具链生存危机** — 大量 Issue (#556, #1061, #1169) 报告 `run_eval.py/run_loop.py` 完全无法工作（0% 召回率）。**社区当前的最高优先级已经从“创造新 Skill”变成了“让创造 Skill 的工具能跑起来”。**
2. **🛡️ 安全与信任治理** — #492 发起对“社区技能混入 `anthropic/` 命名空间”的严重安全质疑（23条回复），社区开始关注伪装成官方技能的供应链攻击风险。
3. **👥 企业级协作** — #228 强烈要求实现**组织级 Skill 共享库**，取代当前手动发送文件、逐个上传的原始协作模式。
4. **🧠 高级 Agent 能力** — #412 (Agent 治理模式) 和 #1329 (符号化记忆压缩) 代表了社区对更复杂、更安全、更长程 Agent 行为的探索。
5. **🔌 平台互通** — #16 讨论 Skills 作为 MCP 公开的可能性，探索 Skill 标准化的 API 封装形式。

## 3. 高潜力待合并 Skills

这些 PR 评论活跃、技术完成度高，具有近期合并落地的高潜力：

* **[#514] document-typography** ([链接](https://github.com/anthropics/skills/pull/514)) — 低争议、高价值，解决用户日常生活中对“AI 味”排版的不满。
* **[#1298] skill-creator/run_eval 修复** ([链接](https://github.com/anthropics/skills/pull/1298)) — 若被采纳，将直接解锁整个生态的生产力，是最高优先级的技术贡献。
* **[#723] testing-patterns** ([链接](https://github.com/anthropics/skills/pull/723)) — 内容详实，覆盖了开发者最看重的代码质量护城河。
* **[#83] Skill 质量/安全分析器** ([链接](https://github.com/anthropics/skills/pull/83)) — 生态治理的核心拼图，对维护技能市场秩序至关重要。
* **[#486] ODT 技能** ([链接](https://github.com/anthropics/skills/pull/486)) — 企业办公刚需，有助于突破特定的政企用户场景。

## 4. Skills 生态洞察

> **一句话总结：当前社区的最强音并非探索新场景，而是集中力量解决基础工具链的瘫痪（`run_eval.py` 0% 召回率）和信任危机（命名空间伪装），社区正从“功能狂热”转向全面的“生态基础治理”。**

---

# Claude Code 社区动态日报 | 2026-06-28

**分析师：** AI 开发工具技术分析师


## 1. 今日速览

- **Opus 4.7 思考摘要渲染问题全面爆发**：围绕新模型在 VS Code 扩展等非交互界面中 Thinking Summaries 失效的 Bug（#49268 / #49322 / #49902 / #59844），社区已累积超百条评论和 120+ 👍，Root Cause 被成功定位为 API 请求头缺失 `display: "summarized"` 字段，是近期影响力最大的回归性 Bug。
- **Cowork 与 Windows 平台成为新焦点**：ARM64 兼容性阻塞（#39636）、终端交互设计争议（#70622）、手动上下文压缩需求（#65114）持续升温，反映出用户群体的扩大和对平台一致性的更高期待。
- **社区贡献活跃但 PR 节奏放缓**：过去 24 小时仅更新 2 个 PR，但在 Issue 层面社区展现了极高的参与度，贡献了大量高质量的技术分析和复现报告。


## 2. 版本发布

（过去 24 小时内无新版本发布）


## 3. 社区热点 Issues（10 条精选）

### 1. Opus 4.7 思考摘要渲染全面失效 🔥
- **Issues:** #49268 / #49322 / #49902 / #59844
- **为什么重要：** 这是 Opus 4.7 模型上线后影响最广的回归 Bug。新版 API 调整了 `display` 参数的默认行为，需要显式设置 `"summarized"`，但 CLI、VS Code 扩展、SDK 的非交互调用路径均未适配这一变化。用户升级最强模型后，反而丢失了最具特色的推理过程可视化功能，直接导致体验降级。
- **社区反应：** 反响极其热烈。开发者 `yusufmo1` 和 `ojura` 通过 API 抓包和源码分析，精准定位到运行时的逻辑缺失。大量用户涌入已有议题表达“我也遇到了”，且议题间相互关联形成完整的追踪线索。
- **链接：** [#49268 (评论: 46, 👍: 75)](https://github.com/anthropics/claude-code/issues/49268) / [#49322 (评论: 47, 👍: 41)](https://github.com/anthropics/claude-code/issues/49322)

### 2. Cowork VM 在 Snapdragon X Plus (ARM64) 上无法引导内核
- **Issue:** #39636
- **为什么重要：** 彻底阻碍 Windows ARM 用户使用 Cowork 模式。随着苹果 M 系列带动 ARM 生态，以及骁龙 X 系列笔记本的铺开，该问题的影响面持续扩大。
- **社区反应：** 用户不断报告“每试必 Timeout”，在缺乏临时解决方案的情况下，该帖已成为 Windows ARM 用户的信息枢纽。
- **链接：** [#39636 (评论: 32, 👍: 9)](https://github.com/anthropics/claude-code/issues/39636)

### 3. 请求添加禁用终端可点击 Yes/No 的配置开关 🔥
- **Issue:** #70622
- **为什么重要：** 新引入的可点击按钮虽然视觉上更友好，但在实际终端环境中极易被鼠标误触，导致意外取消或更严重的安全违规批准。用户强烈要求恢复纯键盘操作模式。
- **社区反应：** 获得了 24 个 👍，是近期 UX 方向最受关注的议题。用户直言“在黑色终端空白区域点击会误触”，请求加入 `settings.json` 配置项。
- **链接：** [#70622 (评论: 8, 👍: 24)](https://github.com/anthropics/claude-code/issues/70622)

### 4. Cowork 模式下缺少手动 /compact 命令
- **Issue:** #65114 / #71803
- **为什么重要：** 目前 Cowork 的上下文压缩完全自动执行，用户无法主动干预。开发者希望在关键节点手动触发压缩，控制上下文窗口的缩减节奏，避免关键信息丢失。
- **社区反应：** 用户认为这是 Cowork 从“自动化玩具”走向“专业工具”的必要能力。
- **链接：** [#65114 (评论: 5, 👍: 1)](https://github.com/anthropics/claude-code/issues/65114)

### 5. VS Code 扩展请求集成原生系统通知
- **Issue:** #57230 / #65241
- **为什么重要：** 当前仅通过编辑器标签页颜色和状态栏文本提示任务状态，开发者必须持续注视屏幕才能捕获状态变化。对于多任务并行的用户，缺乏系统级 Toast 通知严重制约了工作效率。
- **社区反应：** 获得了 14 个 👍，是 VS Code 扩展体验优化的核心呼声。
- **链接：** [#57230 (评论: 4, 👍: 14)](https://github.com/anthropics/claude-code/issues/57230)

### 6. Opus 4.8 安全分类器故障导致所有工具调用被拒
- **Issue:** #69950
- **为什么重要：** 当后端安全分类器 `claude-opus-4-8` 暂时不可用时，自动安全模式完全无法判断 Bash/MCP 调用的安全性，导致所有工具调用被拒绝。这属于 P0 级阻塞性故障，意味着用户完全无法使用自动化功能。
- **社区反应：** 用户报告该问题持续了较长时间且无有效的降级或重试策略。
- **链接：** [#69950 (评论: 2, 👍: 0)](https://github.com/anthropics/claude-code/issues/69950)

### 7. 多 MCP 服务器配置下指令被静默截断
- **Issue:** #43474
- **为什么重要：** 当配置 3 个及以上非入门级 MCP 服务器时，系统提示中的服务器指令会被静默截断（最后一条指令不完整），且没有任何警告。这直接导致 Agent 行为不符合预期，调试极其困难。
- **社区反应：** 用户提供了完整的抓包对比和复现步骤，证明是 MCP 协议实现中的基础 Bug。
- **链接：** [#43474 (评论: 3, 👍: 2)](https://github.com/anthropics/claude-code/issues/43474)

### 8. 权限审批的移动端推送支持
- **Issue:** #62458
- **为什么重要：** 当开发者离开电脑，终端会话阻塞在权限审批提示（`1. Yes / 2. No`）时，只能步行回到工位。移动端推送批准/拒绝是解锁“无人值守”开发体验的关键能力。
- **社区反应：** 被认为是提升远程开发体验的高级必备功能。
- **链接：** [#62458 (评论: 2, 👍: 1)](https://github.com/anthropics/claude-code/issues/62458)

### 9. Opus 4.7 思考阶段陷入 Token 重复死循环
- **Issue:** #71945
- **为什么重要：** 模型在推理时重复输出同一短语（如反复生成“not called”），消耗约 2,300+ Tokens 后才跳出循环。直接导致 API 成本飙升和生成延迟增加。
- **社区反应：** 今日最新提交，虽然评论尚少，但问题严重性高，值得高度关注。
- **链接：** [#71945 (评论: 1, 👍: 0)](https://github.com/anthropics/claude-code/issues/71945)

### 10. 跨 Surface 功能与反馈机制不一致
- **Issue:** #71941
- **为什么重要：** 用户深入对比了 Claude Code、Cowork、claude.ai 三个界面后指出，三者在功能集、UI 交互、反馈机制上存在大量“随意”且缺乏合理性的差异。这是产品战略层面的重要反馈。
- **社区反应：** 今天提交，可能成为推动 Anthropic 统一产品体验的关键议题。
- **链接：** [#71941 (评论: 1, 👍: 0)](https://github.com/anthropics/claude-code/issues/71941)


## 4. 重要 PR 进展

*过去 24 小时社区 PR 活跃度较低，仅更新 2 个 PR，全部盘点如下：*

### 1. PR #71798：空白标题 PR
- **状态：** 已关闭
- **内容：** 用户 `ShivaanjayNarula` 创建了一个标题为 `.` 的空白 PR 并随即关闭。无实质代码变更，推测为自动化测试或误创建。
- **链接：** [查看空白 PR](https://github.com/anthropics/claude-code/pull/71798)

### 2. PR #68787：修复 Issue 标签编辑脚本静默失败
- **状态：** 开放中
- **内容：** 修复了 `edit-issue-labels.sh` 脚本在未提供任何标签参数时，仅返回非零退出码（exit 1）但不输出任何错误信息的问题。新增了一条明确的 `stderr` 错误提示以辅助 CI/CD 排障。
- **意义：** 虽然是仓库工具链的微优化，但体现了社区对开发流程（DevEx）质量的关注，有助于复用脚本和 CI 流程的调试效率。
- **链接：** [查看脚本修复 PR](https://github.com/anthropics/claude-code/pull/68787)


## 5. 功能需求趋势

### 1. 智能通知与异步化工作流
社区不再满足于被动观察终端输出。从 #57230（VS Code Toast）、#67220（Windows 原生通知）、#65241（会话事件通知）到 #62458（移动端推送），用户期望 Claude Code 融入操作系统的通知体系，实现真正的“Fire and Forget”工作流。

### 2. Cowork / 多 Agent 的精细化管控
Cowork 正从“并行自动执行”向“可控协作”演进。集中式权限面板（#70591）、手动上下文压缩（#65114）、Agent 自触发压缩（#71803）、交互行为配置（#70622），用户希望拥有对多 Agent 行为的精确控制权。

### 3. 新模型的平滑接入与回退
Opus 4.7 的 Thinking 失效事件（#49268）深刻教育了社区和官方。社区期望新模型上线前，能够对上层 UI 渲染层、API 参数层（如 `display` 字段）、安全层（#69950）做全链路的兼容性自动化测试，并设置智能降级/回退机制。

### 4. MCP 协议可靠性新阶段
社区关注的焦点已从“MCP 能否连接”转向“连接后能否稳定工作”。子进程环境变量缺失（#71924）、指令静默截断（#43474）、握手协议细节（#23808），表明 MCP 进入了深度打磨期。

### 5. Windows 平台体验追平 Mac
ARM 架构支持（#39636）、原生通知（#67220）、环境变量传递（#71924）——每一条 Issue 都在填补 Windows 与 Mac 之间的体验差距，预计官方将持续加大 Windows 平台投入。


## 6. 开发者关注点

### 1. Opus 4.7 升级的体验倒退
开发者普遍反馈，升级最强模型不仅没有获得增强体验，反而失去了最核心的“Thinking 可视化”功能。这种“版本升级体验降级”的现象严重打击了开发者对新模型的信任和升级意愿。社区期待官方建立更完善的新模型上线评估矩阵。

### 2. 权限审批的平衡术困境
可点击按钮引入了误触风险（#70622），自动化安全分类器因后端波动导致流程完全卡死（#69950）。用户在“操作效率”和“安全保障”之间找不到理想的平衡点，这一交互设计难题亟待官方提出系统性解决方案。

### 3. Token 浪费的痛感强烈
无论是思维阶段的 Token 死循环（#71945），还是上下文压缩时机不可控导致的 Token 浪费，开发者对 API 成本的敏感度极高。任何显著的无效 Token 消耗都会迅速转化为社区中的负面声音。

### 4. 跨 Surface 体验碎片化
#71941 的提交颇具符号意义。开发者不仅在终端使用 Claude Code，还深入使用 VS Code 扩展、Cowork 桌面端和 claude.ai 网页端。功能与行为的不一致造成了显著的认知负担和配置困扰。

### 5. MCP 调试的“黑箱”困境
当 MCP 配置出现问题时（指令截断、环境变量未设置），系统往往静默吞掉错误。开发者在这种“无报错调试”环境中排查 MCP 连接器问题异常痛苦，强烈呼吁增加更明确、更早的错误反馈机制。

---

*数据来源：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-06-28

## 今日速览

- **Plus 用户额度异常消耗**（#28879）持续发酵，单次 prompt 消耗激增 10–20 倍，社区要求官方透明响应，相关讨论已在 6 月 27–28 日达到新高。
- **新出现的 "Responses-Lite" 模型兼容错误**（#30224/#30406）影响 GPT‑5.5 用户，已有多条独立报告，macOS 和 Windows 均有出现。
- **额度信息透明化迎来 PR 修复**（#30395），开始向客户端暴露重置额度过期时间，直接回应当前社区最关切的额度管理痛点。

---

## 版本发布

今日发布三个快速迭代的 alpha 版本，均为小步推进：

- **rust-v0.143.0-alpha.27** / **alpha.28** / **alpha.29**  
  连续发布 0.143.0-alpha 系列，按此前节奏推测包含 bug 修复和稳定性改进。

> 发布说明较简短，未列出具体变更；建议关注后续 release notes。

---

## 社区热点 Issues（10 条）

### 1. #28879 — [bug] Plus 额度消耗暴涨 10–20 倍
- **👍 334 · 💬 186 · 更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/issues/28879)  
**为什么重要：** 6 月 16 日起 gpt‑5.5 模型在 Plus 计划下每 token 消耗激增，原本 20+ 轮对话的预算现在 2–3 轮即耗尽。用户附带了 token_count 及 rate_limit 日志，问题指向服务器端限额计算调整。社区关注度最高，目前无官方回复，预期将影响 Plus 用户使用信心。

### 2. #11023 — [enhancement] Linux 桌面应用
- **👍 650 · 💬 130 · 更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/issues/11023)  
**为什么重要：** 收藏数最高的 feature request。因 macOS 版本存在电源/资源问题，大量开发者希望在 Linux 桌面使用原生应用。社区反应热烈，持续有新用户 +1。

### 3. #2847 — [enhancement] 排除敏感文件（.codexignore）
- **👍 414 · 💬 79 · 更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/issues/2847)  
**为什么重要：** 从去年延续至今的长期需求，希望增加 `.codexignore` / 全局忽略规则，防止 agent 读取或上传敏感文件（如密钥、`node_modules`）。6 月 27 日仍有新评论，说明社区对此功能期待仍然很高。

### 4. #28224 — [bug] SQLite 日志写入量过大（已修复关闭）
- **👍 400 · 💬 93 · 更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/issues/28224)  
**为什么重要：** 曾因年写入 ~640 TB 数据引发 SSD 寿命担忧。作者确认 3 个合并 PR 已减少 85% 日志，于 6 月 23 日关闭。社区对其快速修复表示认可。

### 5. #30224 — [bug] Responses-Lite 模型不支持错误
- **👍 18 · 💬 52 · 更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/issues/30224)  
**为什么重要：** 使用自定义模型或部分内置模型触发 `X-OpenAI-Internal-Codex-Responses-Lite` 报错，Windows 和 macOS 均有报告。可能是近期服务端变更导致的兼容问题，影响范围正在扩大。

### 6. #29955 — [bug] Pro*5 用户 100 余额瞬间消耗
- **👍 7 · 💬 29 · 更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/issues/29955)  
**为什么重要：** Pro 付费用户反馈 5h 额度在 1 条消息后归零，与 #28879 类似但更极端。多条同类报告表明 rate‑limit 问题不仅影响 Plus，高等级订阅同样存在。

### 7. #29532 — [bug] macOS SQLite TRACE 日志仍在写
- **👍 7 · 💬 22 · 更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/issues/29532)  
**为什么重要：** #28224 修复后，macOS 用户发现 `~/.codex/logs_2.sqlite` 仍有持续写入，确认是部分修复。社区提交了具体 trace 分析，工程团队需进一步定位。

### 8. #25744 — [bug] macOS 进程泄漏导致 HID 卡顿
- **👍 3 · 💬 8 · 更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/issues/25744)  
**为什么重要：** 长期运行的 Codex 会积累 Computer Use / MCP helper 进程和僵尸子进程，导致触控板/键盘延迟。影响日常开发体验，属于 macOS 平台特有的资源管理问题。

### 9. #26984 — [bug] MCP stdio 泄漏管道 fd 导致 EMFILE
- **👍 1 · 💬 7 · 更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/issues/26984)  
**为什么重要：** MCP 服务器未正确清理管道和子进程，累计 `too many open files` 错误。长时间会话中会直接中断工作，影响依赖 MCP 的用户。

### 10. #30390 — [bug] ambient_suggestions 后台消耗 7 万 tokens
- **👍 0 · 💬 3 · 更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/issues/30390)  
**为什么重要：** Windows Codex Desktop 后台功能“ambient_suggestions”单次即消耗约 70k tokens，用户事前不知情。暴露了后台耗 token 缺乏透明度的问题，属于新的投诉点。

---

## 重要 PR 进展（10 条）

### 1. #30395 — 显示额度重置过期详情（Open）
- **作者：** jayp-oai · **更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/pull/30395)  
**内容：** 在 `account/rateLimits/read` 接口中并发获取 reset‑credit 过期日期，并让客户端可以展示每个重置额度的到期时间。直接回应近期对透明度的大量诉求。

### 2. #30334 — 添加结构化工具与推理计时事件（Open）
- **作者：** bolinfest · **更新 2026‑06‑28**  
- [查看详情](https://github.com/openai/codex/pull/30334)  
**内容：** 在 JSON 日志中输出 tool latency 分段（dispatch/queue/handler），方便下游诊断工具耗时瓶颈。提升 app‑server 可观测性。

### 3. #30269 — 禁用 Rendezvous WebSocket 的 Nagle 算法（Open）
- **作者：** richardopenai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30269)  
**内容：** 对 exec‑server 的 WebSocket 连接加入 `disable_nagle=true`，预期减少交互式消息延迟。代码路径窄、风险低。

### 4. #30292 — 序列化共享 MCP OAuth 凭据存储（Open）
- **作者：** stevenlee-oai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30292)  
**内容：** MCP OAuth 体系重构的基础 PR，将在多线程/多进程环境下对 credential store 读写加锁，防止竞争。后续堆叠 PR 包括事务序列化、登录/登出串行化等（#30293‑#30296）。

### 5. #30294 — 路由 MCP OAuth 恢复通过 Codex（Open）
- **作者：** stevenlee-oai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30294)  
**内容：** 在 #30292 基础上将 OAuth recovery 流程统一纳入 Codex 管理，避免客户端直接调用私有端点。提升安全性和一致性。

### 6. #30291 — 暴露环境信息 RPC（已关闭）
- **作者：** maxj-oai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30291)  
**内容：** 新增 RPC 让客户端查询执行环境的 shell 和工作目录，便于在异构部署中选择正确环境。已在代码审查后合入。

### 7. #30327 — 稳定合成调用输出 ID（已关闭）
- **作者：** bolinfest · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30327)  
**内容：** 修复 `ContextManager::for_prompt` 中合成的 abort 输出未分配稳定 ID 的问题，避免重试导致对话身份不一致。提升会话连续性。

### 8. #30384 — 增加 currentTime/read 超时（已关闭）
- **作者：** rka-oai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30384)  
**内容：** 将 time 查询的超时从 5s 提高到 10s，减少因网络波动引起的超时失败，属于基础稳健性改进。

### 9. #29691 — 在运行时强制插件市场源策略（已关闭）
- **作者：** xl-openai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/29691)  
**内容：** 根据企业策略屏蔽违规 marketplace 插件，并过滤插件列表/发现接口。企业级安全管理功能，已在审查后合并。

### 10. #30089 — 测试 MCP OAuth 并发与恢复（Open）
- **作者：** stevenlee-oai · **更新 2026‑06‑27**  
- [查看详情](https://github.com/openai/codex/pull/30089)  
**内容：** 与 #30292 系列配合的测试增强，覆盖并发 OAuth 刷新、持久化失败恢复等场景。为 MCP OAuth 重构提供质量保障。

---

## 功能需求趋势

从近期 Issues 及评论区可以看出，社区最关注的三大方向为：

1. **额度管理与透明化**  
   - 多个 “rate‑limit” 标签 issue 表明用户急切需要了解消耗明细、重置时间以及异常消耗的熔断机制。
   - `#30395` 的快速出现即是工程团队对此趋势的回应。

2. **平台扩展与稳定性**  
   - **Linux 桌面原生应用** 收藏数 650+，是单一 feature 中呼声最高的。
   - **Windows 兼容**：多线程 git 轮询、spellcheck 无建议、sandbox 初始化失败等持续被报告。
   - **macOS 资源泄漏**：helper 进程、SQLite 残留日志，用户期望尽快彻底修复。

3. **用户控制力增强**  
   - **`.codexignore` / `config.toml` 忽略规则**（#2847、#24993）期待度高，用于防止机密文件泄漏。
   - **编辑前确认**（#24325）、后台行为透明化（#30390 的 ambient_suggestions）表明用户希望拥有更细粒度的操作审核权。

此外，MCP 生态的 OAuth 流程优化和稳定性也是近期高频主题。

---

## 开发者关注点（痛点）

- **额度异常消耗**：多个付费用户报告预算在极短时间内用完，且缺乏实时诊断工具，严重损害信任。开发者在 #28879 中提供了详细日志，呼吁官方尽快定位。
- **后台资源浪费**：`ambient_suggestions` 无故消耗 70k tokens，SQLite 日志写入量大、MCP 进程泄漏 pipe 和 orphan 进程，加之 macOS 僵尸进程积累，长期运行后性能明显下降。
- **认证与 OAuth 流程脆弱**：Business 用户遭遇 401 自动吊销（#28672），MCP 使用过期 access token 失败（#27165），token 写入损坏（#30254）等表明凭证管理需加强容错。
- **模型兼容性断裂**：出现 "Responses-Lite" 头部传导错误（#30224 / #30406），GPT‑5.5 在更新后突然不可用，影响正在进行的项目。
- **Windows/Crossover 平台体验**：VS Code 扩展中央面板白屏（#21863）、ARM64 sandbox 间歇失败（#24259）、git.exe 轮询进程残留（#29408）等问题表明 Windows 仍需大量适配投入。
- **无人值守行为令用户不安**：后台自动打开 Chrome 并显示 “自动化测试软件控制”（#30170），用户担心安全或隐私隐患。

---

*以上基于 openai/codex 公开数据整理，截至 2026‑06‑28 23:59 UTC。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-06-28

---

## 📌 今日速览

昨晚发布了 **v0.51.0-nightly** 安全修复版本，重点修复了敏感路径黑名单大小写不敏感匹配及 VSCode HITL 加固；社区密集提交多项安全增强 PR（DNS 重绑定防御、路径遍历还原、环境变量过滤等）。与此同时，通用代理挂起（#21409）和子代理最大轮数误报成功（#22323）两大 Bug 持续引发热议。

---

## 🚀 版本发布

### [v0.51.0-nightly.20260628.gae0a3aa7b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260628.gae0a3aa7b)

- **安全修复**：`fix(security): enforce case-insensitive sensitive path blocklist and vscode hitl`（[PR #27966](https://github.com/google-gemini/gemini-cli/pull/27966)）
- **完整变更日志**：[v0.51.0-nightly.20260626.gb14416447…v0.51.0-nightly.20260628.gae0a3aa7b](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260626.gb14416447...v0.51.0-nightly.20260628.gae0a3aa7b)

---

## 🔥 社区热点 Issues（10 条）

### 1. #22323 — 子代理达到最大轮数被误报为成功
- **链接**：[google-gemini/gemini-cli#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **标签**：`priority/p1` / `kind/bug` / `area/agent`
- **社区反应**：💬 8 条评论 | 👍 2
- **为什么重要**：`codebase_investigator` 子代理在超限后仍报告 `status: "success"`，`Termination Reason: "GOAL"`，掩盖了真实的中断原因，严重误导用户。该 Issue 被标记为 p1 且需要重新测试，社区呼吁紧急修复。

### 2. #21409 — 通用代理（Generalist agent）挂起
- **链接**：[google-gemini/gemini-cli#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **标签**：`priority/p1` / `kind/bug` / `area/agent`
- **社区反应**：💬 7 条评论 | 👍 8（本期最高赞）
- **为什么重要**：Gemini CLI 一旦委托通用代理便永久挂起，用户等待数小时后只能取消。临时解决方法是指定不使用子代理。该问题是影响日常使用的**首要稳定性 Bug**。

### 3. #21968 — Gemini 极少主动使用 Skills 和子代理
- **链接**：[google-gemini/gemini-cli#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **标签**：`priority/p2` / `kind/bug` / `area/agent`
- **社区反应**：💬 6 条评论
- **为什么重要**：社区普遍反映已注册的自定义技能和子代理几乎不会被模型自动调用，必须用户显式指定。这极大削弱了扩展能力，是目前**Agent 可用性的核心痛点**。

### 4. #25166 — Shell 命令执行完成后卡死（Waiting input）
- **链接**：[google-gemini/gemini-cli#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **标签**：`priority/p1` / `kind/bug` / `area/core`
- **社区反应**：💬 4 条评论 | 👍 3
- **为什么重要**：极其简单的 CLI 命令（如 `ls`）执行后终端仍显示“Awaiting user input”，导致会话无法继续。该 Bug **严重影响交互式工作流**，被标记为 p1。

### 5. #26525 — Auto Memory 需增加确定性脱敏与减少日志
- **链接**：[google-gemini/gemini-cli#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
- **标签**：`priority/p2` / `kind/bug` / `area/security`
- **社区反应**：💬 5 条评论
- **为什么重要**：Auto Memory 将本地转录发送给模型后要求模型擦除敏感信息，但内容已暴露；同时现有技能日志可能包含未脱敏数据。社区呼吁在输入模型前做确定性脱敏，提升隐私基线。

### 6. #26522 — Auto Memory 对低价值会话无限重试
- **链接**：[google-gemini/gemini-cli#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **标签**：`priority/p2` / `kind/bug` / `area/agent`
- **社区反应**：💬 5 条评论
- **为什么重要**：若提取代理判断某会话低价值而跳过，该记录未被标记为已处理，下次仍会被再次提取，形成无限循环。此问题可能导致**大量 Token 浪费及 API 费用**。

### 7. #22745 — AST 感知的文件读取、搜索与代码映射
- **链接**：[google-gemini/gemini-cli#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
- **标签**：`priority/p2` / `kind/feature` / `area/agent`
- **社区反应**：💬 7 条评论 | 👍 1
- **为什么重要**：通过 AST 工具更精确地读取方法边界、减少 token 消耗、提升搜索效率。该项目为**长期技术方向**，社区参与讨论积极，希望借此改善 Agent 的代码理解能力。

### 8. #24246 — 超过 128 个工具时报 400 错误
- **链接**：[google-gemini/gemini-cli#24246](https://github.com/google-gemini/gemini-cli/issues/24246)
- **标签**：`priority/p2` / `kind/bug` / `area/agent`
- **社区反应**：💬 3 条评论
- **为什么重要**：当启用工具数量超过 128（实际可能更多），Gemini API 返回 400。用户期望 Agent 能自动缩小可用工具范围，避免上限错误。这是**工具生态扩展的关键容量问题**。

### 9. #22672 — Agent 需阻止或劝阻破坏性行为
- **链接**：[google-gemini/gemini-cli#22672](https://github.com/google-gemini/gemini-cli/issues/22672)
- **标签**：`priority/p2` / `kind/customer-issue` / `area/agent`
- **社区反应**：💬 3 条评论 | 👍 1
- **为什么重要**：模型在复杂 Git 操作或数据库维护中频繁使用 `git reset --force` 等危险命令，缺乏安全引导。社区要求内置「安全护栏」，**从系统层面减少误操作风险**。

### 10. #20079 — `~/.gemini/agents/` 中的符号链接不被识别为 Agent
- **链接**：[google-gemini/gemini-cli#20079](https://github.com/google-gemini/gemini-cli/issues/20079)
- **标签**：`priority/p2` / `kind/bug` / `area/agent`
- **社区反应**：💬 4 条评论
- **为什么重要**：许多用户使用符号链接管理 Agent 配置，当前实现直接跳过 symlink，导致自定义 Agent 丢失。这是一个**常见的配置便利性问题**，影响面较广。

---

## 🛠 重要 PR 进展（10 条）

### 1. #28181 🔒 [开放] fix(security): 防止 DNS 重绑定绕过 SSRF 保护
- **链接**：[PR #28181](https://github.com/google-gemini/gemini-cli/pull/28181) | **作者**：XananasX7 | **标签**：`size/s`
- **内容**：`web_fetch` 工具原先仅对主机名字符串做同步检查，易受 DNS 重绑定攻击。修复后异步解析 DNS 并验证结果 IP，为 SSRF 保护增加实质性防御。

### 2. #28180 🔒 [开放] fix(security): 恢复对 `@` 引用文件的防御性路径解析
- **链接**：[PR #28180](https://github.com/google-gemini/gemini-cli/pull/28180) | **作者**：XananasX7 | **标签**：`size/l`
- **内容**：重新应用此前被回滚的路径遍历安全补丁（#27943）。为 `read_file`、`write_file`、`edit` 工具恢复 `resolveDefensiveToolPath`，防止通过符号链接进行路径绕过。

### 3. #28179 🔒 [开放] fix(security): 从 ALWAYS_ALLOWED 环境变量中移除 `ISSUE_BODY` / `ISSUE_TITLE`
- **链接**：[PR #28179](https://github.com/google-gemini/gemini-cli/pull/28179) | **作者**：XananasX7 | **标签**：`size/xs`
- **内容**：`ISSUE_BODY` 和 `ISSUE_TITLE` 过去始终被加入 Agent 提示，在 CI 环境下可能泄露敏感 Issue 内容。修复将其移出白名单，统一走编辑/审查流程。

### 4. #28178 🔒 [开放] fix(security): 要求机器人补丁需经批准
- **链接**：[PR #28178](https://github.com/google-gemini/gemini-cli/pull/28178) | **作者**：huynhtrungcsc | **标签**：`size/m`
- **内容**：Gemini CLI 自动发布流程不再信任未显式批准的 `bot-changes.patch`，拒绝运行的评审输出将在发布前移除产物，保证推理→发布的原子性。

### 5. #28175 🔒 [开放] fix(policy): Shell 参数扩展需要用户确认
- **链接**：[PR #28175](https://github.com/google-gemini/gemini-cli/pull/28175) | **作者**：huynhtrungcsc | **标签**：`size/m`
- **内容**：对白名单中出现的 shell 命令若包含参数扩展（如 `${}`），交互模式下要求确认，YOLO 模式直接拒绝。新增回归测试确保 `echo` 等安全用法不受影响。

### 6. #28172 [开放] fix(agent): 防止任务失败时静默扩大作用域
- **链接**：[PR #28172](https://github.com/google-gemini/gemini-cli/pull/28172) | **作者**：Suryap-hub | **标签**：`priority/p2` / `size/xs`
- **内容**：当 Agent 请求审查特定代码行失败后，不应未通知用户就读取整个文件或运行脚本。通过增强 `mandateConfirm` 限制策略切换时的自动扩张。

### 7. #28169 ✨ [开放] feat(evals): 新增 eval 覆盖率报告命令
- **链接**：[PR #28169](https://github.com/google-gemini/gemini-cli/pull/28169) | **作者**：ved015 | **标签**：`size/l`
- **内容**：`eval:coverage` 命令通过交叉引用 eval 清单与工具注册表，输出内置工具的自动化测试覆盖率。支持 `--root` 参数及外部工具，为质量基础设施添砖加瓦。

### 8. #28059 [开放] fix(cli): `.env` 文件不可读不再导致扩展加载失败
- **链接**：[PR #28059](https://github.com/google-gemini/gemini-cli/pull/28059) | **作者**：manumishra12 | **标签**：`priority/p2` / `size/m`
- **内容**：当工作区 `.env` 文件权限不足（如沙箱下 EACCES）时，扩展系统整体崩溃。修复仅降级该环境变量作用域而非中断加载，同时加强 Cloud Shell 路径兼容。

### 9. #27878 ✅ [已合并] fix(core): 嗅探 MCP 图像的 MIME 类型
- **链接**：[PR #27878](https://github.com/google-gemini/gemini-cli/pull/27878) | **作者**：Dasoam | **标签**：`priority/p1` / `size/l`
- **内容**：Figma MCP 返回的 WebP 图片被错误标记为 `image/png`，导致 Gemini API 400。修复通过读取 Base64 头部签名准确判断 MIME 类型，解决集成兼容问题。

### 10. #27889 ✅ [已合并] fix(core): 使用存储的 client ID 刷新 MCP OAuth
- **链接**：[PR #27889](https://github.com/google-gemini/gemini-cli/pull/27889) | **作者**：he-yufeng | **标签**：`priority/p1` / `size/m`
- **内容**：自动发现的 MCP 服务器在配置中无静态 `oauth.clientId`，但 CLI 已将其存入 Token 元数据。刷新时仍用原配置导致失败，修复后使用存储值完成刷新。

---

## 📈 功能需求趋势

综合所有 Issue 与 PR，社区当前最关注的五大方向：

1. **Agent 行为透明与可控**  
   - 子代理终止原因误报（#22323）、静默扩大作用域（#28171/28172）、不使用自定义技能（#21968）。  
   - 社区需要更清晰的归因、更强的用户确认机制和可预期的行为。

2. **安全与沙箱系统性提升**  
   - 密集出现 DNS 重绑定、路径遍历、环境变量泄露、Shell 参数扩展、敏感路径黑名单等安全补丁。  
   - 隐私方面聚焦 Auto Memory 的确定性脱敏（#26525）和对低价值会话的终止（#26522）。

3. **Auto Memory 机制成熟化**  
   - 当前提取代理的无限重试、无效 Patch 静默跳过、日志冗余等问题频发。  
   - 社区期望可观测、可中断、可隔离的 Memory 管理闭环。

4. **MCP 协议兼容与维护**  
   - 图片 MIME 嗅探（#27878）、OAuth 刷新（#27889）、Schema 校验（#27888）、以及 `.gitignore`/`.geminiignore` 忽略规则（#27886）等补丁，表明 MCP 集成已进入“精耕细作”阶段。

5. **开发者体验与工具链**  
   - AST 感知文件操作（#22745）是长期技术探索；Eval 覆盖率命令（#28169）、主题自定义修复（#27887）、终端 resize 优化（#21924）反映了社区对“打磨日常体验”的持续诉求。

---

## 💡 开发者关注点

从用户反馈和 Issue 讨论中提炼出的五大高频痛点：

| 痛点 | 代表 Issue | 影响 |
|------|------------|------|
| **Agent 挂起或无响应** | #21409、#25166、#22186 | 直接导致工作流中断，临时绕过只能禁用子代理 |
| **子代理行为不可预知** | #22323、#21968、#22267 | 误报成功、不使用已注册技能、忽略 settings.json |
| **安全/隐私顾虑** | #26525、#28179、#28180 | Auto Memory 内容先送后删、环境变量未过滤、路径绕过 |
| **配置不生效** | #27887、#22093、#20079 | 主题边框、权限禁用、symlink Agent 均常被忽略 |
| **工具生态容量瓶颈** | #24246、#27878、#27889 | 工具数超 128 报 400、MCP 图片类型错误、OAuth 刷新失败 |

建议团队优先解决 **p1 挂起/误报类 Bug** 以恢复基础信任，同时将安全补丁和 Auto Memory 重试机制纳入短期迭代重点。

---

*本日报由 AI 开发工具技术分析师自动生成，数据来源 [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区动态日报 | 2026-06-28

### 1. 今日速览
过去 24 小时无新版本发布，但社区活跃度依旧高涨。多个 Windows 平台严重 bug 集中爆发（复制失效、MCP 服务器启动回归），同时 alt‑screen 默认行为、Ubuntu 密钥环等问题持续被关注。此外，关于类似 Claude Code `/btw` 的上下文查询功能请求获得不少共鸣，反映了用户对更灵活对话模式的期待。

### 2. 版本发布
（无）

---

### 3. 社区热点 Issues（10 个）

1. **[#1799] alt‑screen 视图如何关闭**  
   - 最新 alt‑screen 改动引发多位用户不满，希望恢复原有终端模式。10 条讨论、7 👍。  
   - 链接：[#1799](https://github.com/github/copilot-cli/issues/1799)

2. **[#2165] Ubuntu 密钥环支持损坏**  
   - 文档错误且 `secret‑tool` 缺失时无法正常工作。20 👍 表明影响范围广，需要官方修复。  
   - 链接：[#2165](https://github.com/github/copilot-cli/issues/2165)

3. **[#2778] 请求 /btw 式即时提问功能**  
   - 社区希望像 Claude Code 一样随时利用上下文提问，不必担心干扰当前会话。  
   - 链接：[#2778](https://github.com/github/copilot-cli/issues/2778)

4. **[#3949] Windows 11 复制功能完全失效**  
   - 用户反馈复制后剪贴板为空，但工具仍提示“已复制”。刚报告即获 2 条评论，影响日常操作。  
   - 链接：[#3949](https://github.com/github/copilot-cli/issues/3949)

5. **[#3964] 软换行复制时空格仍丢失（修复不完整）**  
   - v1.0.65 未完全修复 `#3666` 的软换行空格粘连问题，用户再次提出。  
   - 链接：[#3964](https://github.com/github/copilot-cli/issues/3964)

6. **[#3958] Windows 下 v1.0.66 无法启动 .bat/.cmd MCP 服务（回归）**  
   - 导致依赖批处理文件的 MCP 工具链中断，开发者需紧急回退。  
   - 链接：[#3958](https://github.com/github/copilot-cli/issues/3958)

7. **[#3962] v1.0.65 启动后卡住无响应**  
   - 用户报告进入工作状态后界面冻结，无法继续操作，影响基本使用。  
   - 链接：[#3962](https://github.com/github/copilot-cli/issues/3962)

8. **[#3957] MacBook Pro 触控板无法滚动浏览历史**  
   - 滚动操作错误变成选中历史命令，缺少滚动支持。影响 Mac 用户交互体验。  
   - 链接：[#3957](https://github.com/github/copilot-cli/issues/3957)

9. **[#3959] 删除文本后终端残留“幽灵”字符**  
   - 退格时界面刷新不彻底，视觉残留字符虽已逻辑删除，但显示混乱。  
   - 链接：[#3959](https://github.com/github/copilot-cli/issues/3959)

10. **[#3960] 自定义模型仍消耗 GitHub AI 配额**  
    - 用户期望使用自有 provider 时不占用内置配额，但当前行为不符预期。  
    - 链接：[#3960](https://github.com/github/copilot-cli/issues/3960)

---

### 4. 重要 PR 进展（过去 24 小时共 3 个）

1. **[#3928] 添加 .gitignore 和设置配置**  
   - 新增项目基础配置文件，有助于隔离私密文件并统一设置。  
   - 链接：[#3928](https://github.com/github/copilot-cli/pull/3928)

2. **[#570] 为 README.md 添加 macOS 安装说明（WIP）**  
   - 此 PR 由 Copilot 自动生成，近期仍有更新，表明官方可能在完善跨平台文档。  
   - 链接：[#570](https://github.com/github/copilot-cli/pull/570)

3. **[#3737] “Jigg empire ai” 探索性 PR**  
   - 描述较为模糊，可能为实验性尝试或个人项目，社区关注度不高。  
   - 链接：[#3737](https://github.com/github/copilot-cli/pull/3737)

---

### 5. 功能需求趋势

从近期 Issues 中可以提炼出社区最关注的几个方向：

- **终端交互与 UI 自定义**：alt‑screen 开关、滚动行为、复制粘贴、幽灵字符等渲染问题成为高频诉求。  
- **跨平台兼容性与认证**：Windows 复制失效、Mac 触控板、Ubuntu 密钥环等平台特有 bug 与文档错误需要优先修复。  
- **MCP 服务与扩展能力**：MCP 服务器在 Windows 上的 .bat/.cmd 启动回归，表明 CI/CD 及工具链集成的稳定性仍是热点。  
- **会话管理与持久化**：用户希望查看会话过期时间、保留历史记录，避免无故丢失工作上下文。  
- **自定义模型与配额透明**：使用自定义 provider 时不希望消耗 GitHub AI 配额，要求更清晰的配额归属说明。  
- **代理插件（Hook）**：`preToolUse` 钩子拒绝机制失效影响高级安全场景，表明插件扩展尚不成熟。

---

### 6. 开发者关注点

- **Windows 生态问题集中**：复制功能不仅失效，而且 MCP 服务器回归、路径缺少反斜杠等细节 bug 让 Windows 用户普遍感到不稳定。  
- **UI 交互反直觉**：软换行粘连不修复、触控板滚动误选择、文本重影等“小问题”累积后严重削弱日常效率。  
- **认证与文档落差**：Ubuntu 密钥环文档错误，用户参照官方指引仍失败，信任度受损。  
- **新功能介入感强**：alt‑screen 强行启用，且无关闭选项，用户希望保持原有操作习惯。  
- **模型消费不透明**：自定义 provider 仍计入 GitHub 配额，暴露了计费落地的边界模糊，易引发意外超限。  
- **Agent 扩展稳定性**：`preToolUse` 拒绝未生效、MCP 服务器启动兼容性不足，使得希望通过钩子进行安全管控的团队难以依靠该功能。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报 — 2026-06-28

### 📌 今日速览

- **WSL 与桌面端兼容性问题集中爆发**：多个 Issue 报告桌面端向 WSL 发送错误的路径格式（UNC、C:\ 转换），导致会话列表和工具调用完全失效（#19473、#30895）。
- **大模型集成持续涌现 Bug**：GLM-5.2 不支持图片但模型仍尝试截图、NVIDIA NIM Nemotron 3 Ultra 在 Build 阶段永久挂起、Gemini 400 模式错误等，反映出多模型适配的痛点（#34113、#34026、#34130）。
- **核心稳定性修复活跃**：24h 内合并/提交了多项针对内存泄漏、事件监听器溢出、会话回滚及 V2 协议重构的 PR，社区响应迅速（#34263、#34227、#34272）。

### 📦 版本发布

**今日无新版本发布。**

---

### 🔥 社区热点 Issues（10 条精选）

| # | 标题 | 热度 | 一句话点评 |
|---|------|------|-----------|
| [8816](https://github.com/anomalyco/opencode/issues/8816) | [FEATURE] provide llms.txt and docs as markdown | 💬 15 · 👍 34 | **最热 Feature 请求**，要求项目提供标准化的 llms.txt 文档，方便 LLM 解析和下载，社区共识很高。 |
| [23153](https://github.com/anomalyco/opencode/issues/23153) | [FEATURE] PayGo with crypto | 💬 13 · 👍 24 | **呼声极高的支付方式扩展**，用户希望支持加密货币付款，可能面向国际开发者群体。 |
| [22422](https://github.com/anomalyco/opencode/issues/22422) | [bug, perf, core] Memory Leak Warning | 💬 7 · 👍 0 | **事件监听器泄漏警告**（MaxListenersExceededWarning），影响长期运行进程，社区贴出了完整堆栈。 |
| [19473](https://github.com/anomalyco/opencode/issues/19473) | Desktop App sends UNC paths to WSL-hosted server | 💬 7 · 👍 0 | **WSL 经典路径问题**：桌面端传入 UNC 路径导致所有 bash 工具调用失败，已有用户提供 Workaround。 |
| [12219](https://github.com/anomalyco/opencode/issues/12219) | This request requires more credits … can only afford 0 | 💬 7 · 👍 6 | **OpenRouter 额度校验缺失**，使用免费模型仍报错，影响新用户上手体验。 |
| [19130](https://github.com/anomalyco/opencode/issues/19130) | Windows ARM64 native: OpenTUI fails with bun:ffi | 💬 6 · 👍 5 | **ARM64 Windows 原生 TUI 崩溃**，非交互命令正常但 TUI 无法启动，ARM 用户被阻拦。 |
| [33890](https://github.com/anomalyco/opencode/issues/33890) | Bun 1.3.14 segfault (SIGILL) on Linux x86_64 | 💬 6 · 👍 5 | **Bun 运行时 SIGILL 崩溃**，发生在 AMD Zen4 (AVX-512) CPU 上，怀疑与 Bun 编译指令集有关。 |
| [34228](https://github.com/anomalyco/opencode/issues/34228) | opencode exposes an incomplete subset of project skills | 💬 5 · 👍 0 | **技能集暴露不一致**：35 个技能在不同会话中随机丢失，严重影响 Workflow 可靠性。 |
| [34236](https://github.com/anomalyco/opencode/issues/34236) | Opencode desktop uses a lot of CPU resources | 💬 3 · 👍 1 | **桌面端 CPU 高达 30~50%**，CLI 无此问题，用户抱怨影响日常开发。 |
| [28492](https://github.com/anomalyco/opencode/issues/28492) | MaxListenersExceededWarning after web interface starts | 💬 3 · 👍 0 | **另一例事件监听器泄漏**，在 Web 界面启动后触发，与 #22422 同族问题。 |

---

### 📌 重要 PR 进展（10 条精选）

| # | 标题 | 状态 | 核心内容 |
|---|------|------|----------|
| [34273](https://github.com/anomalyco/opencode/pull/34273) | feat(tools): add agent tools (git, format, diagnostics, memory/history, LSP rename) + fix TUI spinner | 🟢 Open | **大规模新工具集**，引入 Git、格式化、诊断、内存/历史 BM25 检索、LSP 重命名，并修复 TUI spinner，社区期待度高。 |
| [34263](https://github.com/anomalyco/opencode/pull/34263) | feat(tui): wire up undo/redo and revert for V2 sessions | ✅ Closed | **V2 会话的撤销/重做/回退功能上线**，补齐了 TUI 中「未实现」占位符，包含 BusyError 保护。 |
| [34272](https://github.com/anomalyco/opencode/pull/34272) | fix: add final empty-content guard in message() pipeline | 🟢 Open | **Provider 无关的空内容保护**，在消息管道末端增加空内容拦截，解决 #23260 和 #26320 两个老 Issue。 |
| [33202](https://github.com/anomalyco/opencode/pull/33202) | fix(agent): skip parseModel when model is "inherit" | 🟢 Open | **修复子 Agent 模型继承解析**，当 Frontmatter 中 model 未指定时不再错误调用 parseModel，一次性关闭 5 个关联 Issue。 |
| [34234](https://github.com/anomalyco/opencode/pull/34234) | fix: preserve attachment file paths | 🟢 Open | **附件路径保留**：粘贴/拖拽文件后，Agent 能直接访问原始路径而非仅内联数据，修复 #23801 和 #17488。 |
| [34256](https://github.com/anomalyco/opencode/pull/34256) | fix(server): reject foreign directory hints before instance lookup | 🟢 Open | **WSL/远程路径兜底**：拒绝非本地路径提示，防止类似 #30895、#19473 的路径拼接错误。 |
| [34242](https://github.com/anomalyco/opencode/pull/34242) | fix(tui): prevent piped stdin from breaking UI and keyboard input | 🟢 Open | **管道输入导致 TUI 崩溃修复**，覆盖 4 个 Issue，提升 CI/pipe 场景的健壮性。 |
| [34267](https://github.com/anomalyco/opencode/pull/34267) | fix(llm): collapse system messages when plugin appends a single entry | 🟢 Open | **系统消息折叠逻辑修复**：当插件追加后只有两条 system 消息时不进行无意义的折叠，修复 #34243。 |
| [34246](https://github.com/anomalyco/opencode/pull/34246) | feat(tui): add tool_output_expanded_default option | 🟢 Open | **新增 TUI 配置项**，允许用户默认展开工具输出面板，提升调试体验。 |
| [34261](https://github.com/anomalyco/opencode/pull/34261) | fix(core): guard non-reducing compaction | 🟢 Open | **防止压缩不进展时无限循环**，在溢出恢复时添加前置检查，修复 #27924。 |

---

### 🧭 功能需求趋势

- **LLM 友好文档**（#8816）：社区要求项目提供标准 `llms.txt` 和 Markdown 文档，以便 AI 工具直接爬取，反映 AI 开发工具自身「被 AI 使用」的需求。
- **加密支付**（#23153）：用户强烈要求支持加密货币支付，暗示国际用户对灵活付费方式的渴望。
- **企业模型集成**（#34030）：GitHub Copilot Enterprise 添加的第三方模型无法被 OpenCode 识别，企业用户希望无痛对接。
- **V2 会话增强**（#34263, #34264）：撤销/重做/重命名等会话管理功能正在快速填补，社区期待更完善的状态管理。
- **UI 自定义**（#34246）：允许默认展开工具输出、WSL UI v2（#34233）、粘性会话列表头（#34220），体现对桌面端用户体验的精细化追求。

---

### 🔧 开发者关注点（痛点 / 高频需求）

- **WSL / 跨平台路径问题**：多个 Issue 指向 Windows + WSL 组合的路径格式不兼容（UNC、C:\ 转换），已影响日常开发流程，社区正在集中修补（#19473、#30895、#34256）。
- **内存与 CPU 泄漏**：`MaxListenersExceededWarning` 反复出现（#22422、#28492），桌面端 CPU 占用异常（#34236），Server 模式内存膨胀至 26.8 GiB（#33213），性能稳定性成为头号公敌。
- **多模型兼容性**：GLM 系列图片输入误判（#34113）、NVIDIA NIM 悬停（#34026）、Gemini 400 模式错误（#34130）、Bun 1.3.14 SIGILL（#33890）—— 每个新模型接入都伴随适配断层。
- **技能系统不可靠**：35 个技能会话间随机丢失（#34228），子 Agent 模型回退时无限重试（#34043），核心编排能力仍需加固。
- **桌面端稳定性**：缺失会话导致渲染器 404 崩溃（#32473），ARM64 原生 TUI 无法启动（#19130），用户对 Desktop 版的可用性诟病较多。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 | 2026-06-28

## 今日速览
今日无版本发布。社区讨论焦点集中在 **TUI 交互缺陷**（滚动强制跳转、多工具调用闪烁）、**Provider 错误透明化**以及 **扩展 API 增强**（已合并 reportUsage 和 externalEditor 配置）。此外，模型支持更新（Together.ai 模型废弃、Azure 模型名修正）和安全报告（恶意包举报）也引发广泛关注。

---

## 社区热点 Issues
（挑选过去 24 小时更新的 10 个最值得关注议题，按关注度排序）

### 1. [#5825 Streaming markdown forces scroll to bottom – OPEN](https://github.com/earendil-works/pi/issues/5825)
**热度: 🔥 34 条评论**  
当启用 `clear on shrink` 设置时，Agent 生成 Markdown 期间若用户向上滚动阅读，Pi 会强制跳回底部。严重影响阅读连续性，是当前社区反馈最激烈的 Bug。

### 2. [#5763 Providers swallow the HTTP error body – OPEN](https://github.com/earendil-works/pi/issues/5763)
**评论 5 条，但影响面极广**  
网关返回非 2xx 时，Bedrock、OpenAI 等 Provider 均丢失响应体中的详细错误信息，统一返回“Unknown Error”。开发者无法快速定位代理配置问题，已有对应 PR (#5832) 在修复中。

### 3. [#6129 Package Report: @hypabolic/pi-hypa – CLOSED (恶意行为报告)](https://github.com/earendil-works/pi/issues/6129)
社区成员举报该包通过操纵安装量自我推广，虽未发现实际恶意代码，但破坏了扩展包生态的信任机制。引发对包审核和安装统计透明度的讨论。

### 4. [#6132 Remove Together.ai models deprecated July 10 – CLOSED](https://github.com/earendil-works/pi/issues/6132)
Together.ai 将于 7 月 10 日废弃 `zai-org/GLM-5.1` 和 `Qwen/Qwen3-235B-A22B-Instruct-2507-tput`。社区要求尽快更新内置模型列表并推荐替代模型（如 MiniMax-M3），反映用户对模型供应链维护的高度敏感。

### 5. [#6131 Full screen redraw (flicker) when multiple tool calls stream simultaneously – CLOSED](https://github.com/earendil-works/pi/issues/6131)
模型在一次返回中发起多个工具调用时，TUI 会整个清屏重绘，且随调用块增多愈发频繁。严重干扰使用，已确认为渲染调度 Bug。

### 6. [#6130 renderCall/renderResult silently ignore exceptions – CLOSED](https://github.com/earendil-works/pi/issues/6130)
自定义渲染函数中产生的异常被静默捕获并回退默认渲染，导致开发者白白浪费数小时排查导入错误。社区强烈要求不再忽略异常，至少要输出警告日志。

### 7. [#6127 --append-system-prompt can't override the default coding-agent identity – CLOSED](https://github.com/earendil-works/pi/issues/6127)
使用 `pi --mode rpc` 做自定义 Agent 后端时，通过 `--append-system-prompt` 传入的自定义身份描述无法覆盖 Pi 内置的 coding-agent 身份，限制 Agent 二次开发。

### 8. [#6128 Support diffusiongemma thinking and tool calls – CLOSED](https://github.com/earendil-works/pi/issues/6128)
DiffusionGemma 模型的思考块（thinking block）被错误渲染为普通输出，且工具调用格式不兼容。该模型在 Unsloth Studio 上已有趣味可视化，Pi 用户期待完整支持。

### 9. [#6124 Devnagri breaking the Pi harness – CLOSED](https://github.com/earendil-works/pi/issues/6124)
输入天城文字符（如 `नेटवर्क`）会导致终端 UI 断行、显示错乱。暴露对非拉丁字符集的支持盲区，影响印度语言用户。

### 10. [#6116 opencode-go streaming + tools ignores thinking: {“type”: “disabled”} for mimo models – CLOSED](https://github.com/earendil-works/pi/issues/6116)
即便设置了 thinking=off，mimo 模型在流式工具调用时仍产出推理内容。虽确认为 opencode-go 网关 Bug，但直接影响 Pi 用户对模型行为的控制期待。

---

## 重要 PR 进展
（24 小时内更新的 8 个 Pull Requests，全量收录）

### [#5735 fix(coding-agent): defer extension reload requests safely – OPEN](https://github.com/earendil-works/pi/pull/5735)
使扩展重载更安全：`ctx.reload()` 现对全部扩展上下文可用（不仅限斜杠命令），并通过延迟机制保证重载仅在安全边界执行，避免状态不一致。

### [#5678 Add excludeFromContext for custom messages – OPEN](https://github.com/earendil-works/pi/pull/5678)
允许自定义消息标记 `excludeFromContext`：消息在 UI 中正常渲染，但 `convertToLlm` 会跳过它们，不会送入模型上下文。同时支持压缩和分支总结时正确保留此类消息。

### [#6123 feat(coding-agent): add externalEditor setting for Ctrl+G – CLOSED (已合并)](https://github.com/earendil-works/pi/pull/6123)
新增 `externalEditor` 配置项，允许在 `settings.json` 中直接指定 Ctrl+G 打开的外部编辑器，解决 Windows + Git Bash 下 `$VISUAL`/`$EDITOR` 环境变量不可修改的问题。

### [#6119 feat: add reportUsage API for extensions to contribute session cost – CLOSED (已合并)](https://github.com/earendil-works/pi/pull/6119)
为扩展新增 `pi.reportUsage(input)` API，子代理扩展可将 token 与费用反哺至主会话的 Footer 和 `/session` 总计中，让成本核算更加透明。

### [#5832 fix(ai): surface provider HTTP error body instead of opaque SDK message – OPEN](https://github.com/earendil-works/pi/pull/5832)
对应 #5763。修改 Provider 层，当网关返回非 2xx 时不再丢弃响应 body，而是透出原始错误信息，让 “403”、“UnknownError” 变得可排查。

### [#6115 feat(coding-agent): add configurable chat padding – OPEN](https://github.com/earendil-works/pi/pull/6115)
针对社区长期呼声（Discord 反复提及）增加 TUI 「聊天间距」配置。PR 仍处于讨论阶段，作者表示由于 TUI 架构限制改动较大，需考虑标志系统。

### [#6099 Rename model key from ‘gpt-5.2-chat-latest’ to ‘gpt-5.2-chat’ – CLOSED (已合并)](https://github.com/earendil-works/pi/pull/6099)
修正 Azure OpenAI `5.2` 系列模型的名称映射，`gpt-5.2-chat-latest` 并非有效端点，现改为 `gpt-5.2-chat`，确保模型正常加载。

### [#6111 fix(coding-agent): report settings write failures in install/remove – CLOSED (已合并)](https://github.com/earendil-works/pi/pull/6111)
`pi install` 在遇到只读 `settings.json`（chmod 0444）时，之前只会报告“已安装”却未写入注册信息，导致扩展不可用。现在会正确报错并退出非零。

---

## 功能需求趋势
从过去 24 小时的所有议题中提炼出社区最关注的五个功能方向：

1. **扩展 API 能力增强**  
   - 允许扩展执行已注册工具（#6121）  
   - 向会话贡献子代理成本（#6120 / #6119）  
   - 自定义包管理器安装参数（#6125 / #6126）

2. **编辑器与环境配置灵活度**  
   - `externalEditor` 配置替代环境变量（#6122 / #6123）  
   - 额外 npm 参数控制（#6126）

3. **模型支持维护与兼容性**  
   - 及时更新废弃模型映射（#6132）  
   - 修正 Azure 模型名（#6099）  
   - 适配新模型如 DiffusionGemma thinking（#6128）

4. **错误透明化**  
   - Provider 错误体透出（#5763 / #5832）  
   - 渲染异常不应静默回退（#6130）

5. **TUI 体验优化**  
   - 可配置的聊天间距（#6115）  
   - 修复自动滚动打断阅读（#5825）  
   - 修复多工具调用闪烁（#6131）  
   - 非拉丁字符支持（#6124）

---

## 开发者关注点
综合用户报告与反馈，高频痛点包括：

- **调试困境**：静默错误、Provider 错误信息丢失、渲染异常无日志，导致排障困难。  
- **环境兼容性**：Windows 下编辑器变量不可改写、只读 settings.json 导致安装无声失败。  
- **扩展开发受限**：无法获取稳定的 faux provider 实例（#6117）、无权调用已注册工具、子代理成本无法纳入全局统计。  
- **国际化缺陷**：Devanagri 等 Unicode 文本直接导致 UI 断裂，国际用户受阻。  
- **默认行为不可覆盖**：系统提示、编辑器选择等缺乏配置入口。  
- **性能抖动**：多工具调用时画面闪烁、滚动被强制重置，影响对话流。  
- **成本可见性**：子代理消耗的 token/费用无法在会话总览中体现。

---

*数据来源：GitHub [earendil-works/pi](https://github.com/earendil-works/pi) · 统计时间窗口：2026-06-27 ~ 2026-06-28*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-06-28

---

## 今日速览

昨日 **v0.19.2-nightly** 发布，核心修复了 `web_fetch` 的 JSON 回退逻辑。社区围绕 **模型自动升档导致费用激增**（#5819）展开激烈讨论，同时 **`/loop` 后台任务不可见**（#5823）与 **任务清单跨设备同步**（#5836）成为呼声最高的两大功能缺口。PR 侧亮点颇多：多人协作 agent “qwen tag” 进入 Phase 0 阶段，桌面端语音听写与 MCP 资源浏览也正式落地。

---

## 版本发布

**v0.19.2-nightly.20260628.714513df2** — [Releases 页](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.2-nightly.20260628.714513df2)

- **fix(core):** 允许 `web_fetch` 在响应非 JSON 时走 fallback 解析（[#5660](https://github.com/QwenLM/qwen-code/pull/5660)）
- **chore:** 版本号推进至 v0.19.2

---

## 社区热点 Issues（10 条）

1. **[#4175] Mode B (serve) 生产就绪路线图讨论**  
   Issue 持续获得社区关注（43 条评论），梳理了 daemon 架构、权限、会话复用等剩余工作。虽已关闭，但为后续 serve 开发奠定了路线图基础。  
   [QwenLM/qwen-code Issue #4175](https://github.com/QwenLM/qwen-code/issues/4175)

2. **[#5819] 升级后默认改用更高单价模型，导致费用超支**  
   用户反馈从 v0.18.3 升级至 v0.19 时 `setting.json` 中的模型被自动更换为高价模型（DeepSeek-4 Pro），输出结果还出现简体→繁体转换，浪费大量 token。社区已作为严重 bug 跟踪。  
   [QwenLM/qwen-code Issue #5819](https://github.com/QwenLM/qwen-code/issues/5819)

3. **[#5823] `/loop` cron 任务静默执行，用户无法查看或停止**  
   自动添加的定时任务在后台无提示运行，重新打开对话后模型会自动开始工作，用户对此感到困惑。该 Issue 要求为循环任务提供可视化管理能力。  
   [QwenLM/qwen-code Issue #5823](https://github.com/QwenLM/qwen-code/issues/5823)

4. **[#5836] Todo / Memories / Plans 无法跨设备同步**  
   当前待办、记忆等数据仅保存在 `~/.qwen/` 下，不受 Git 控制，导致工作环境切换后项目状态丢失。社区希望能选择持久化到项目目录（如 `.qwen/todos`）以实现多端同步。  
   [QwenLM/qwen-code Issue #5836](https://github.com/QwenLM/qwen-code/issues/5836)

5. **[#5756] 默认输出上限 8K token 导致大文件写入反复重试**  
   `CAPPED_DEFAULT_MAX_TOKENS=8000` 截断大输出（如写 wiki 页面），模型被迫在失败循环中重试。此关闭的 Issue 揭示了 token 默认策略的合理性争议。  
   [QwenLM/qwen-code Issue #5756](https://github.com/QwenLM/qwen-code/issues/5756)

6. **[#5922] `cua-driver.exe` 在 Windows 上持续高 CPU 占用**  
   即使是 Agent 任务完成后，cua-driver 进程仍在后台占用 CPU。用户质疑其行为类似“病毒”，对 Windows 平台体验影响较大。  
   [QwenLM/qwen-code Issue #5922](https://github.com/QwenLM/qwen-code/issues/5922)

7. **[#5920] `/rewind` 后会话历史消失**  
   `parentUuid` 被存为 `null`，重新加载时仅剩最后一轮对话，之前的上下文全部丢失。这是一个影响会话恢复的关键数据损坏 bug。  
   [QwenLM/qwen-code Issue #5920](https://github.com/QwenLM/qwen-code/issues/5920)

8. **[#5942] Anthropic Provider：可避免的 prompt-cache 未命中导致成本上升**  
   侧查询使用不同的前缀、断点设置在移动的最后一条消息上，导致每条请求都无法命中缓存。这与 Claude Code 的表现形成对比，社区希望改善前缀对齐策略。  
   [QwenLM/qwen-code Issue #5942](https://github.com/QwenLM/qwen-code/issues/5942)

9. **[#5941] 模型输出时向上滚动滚轮直接跳到页面顶部**  
   UI 交互 bug：在滚动浏览生成内容时，轻微向上滚动便会跳回最顶端，影响阅读体验。Windows 用户反馈较多。  
   [QwenLM/qwen-code Issue #5941](https://github.com/QwenLM/qwen-code/issues/5941)

10. **[#5626] 使用 Daemon + WebUI 架构复活 Chrome Extension**  
    用户提议以新架构重新实现 Chrome 扩展（原有 PR #1432 近 4.5 万行），利用已成熟的 daemon 和 WebUI 组件降低维护成本，社区讨论积极。  
    [QwenLM/qwen-code Issue #5626](https://github.com/QwenLM/qwen-code/issues/5626)

---

## 重要 PR 进展（10 条）

1. **[#5835] fix(core): 重新应用 Provider 安装计划时保留当前模型**  
   解决了 #5819 的根因：重复运行 provider 设置不会再重置已选模型，防止升档或 re-auth 时意外切换到高价模型。  
   [QwenLM/qwen-code PR #5835](https://github.com/QwenLM/qwen-code/pull/5835)

2. **[#5890] feat(loop): 在 fire 时注入 `.qwen/loop.md` 任务文件**  
   为 `/loop` 提供可持久化、由用户编辑的任务清单，模型通过哨兵指令自动读取该文件，避免每个 tick 重复阐述任务。直接回应当前社区对循环任务可见性的需求。  
   [QwenLM/qwen-code PR #5890](https://github.com/QwenLM/qwen-code/pull/5890)

3. **[#5856] feat(desktop): 桌面端语音听写**  
   将 `/voice` 语音听写从 CLI 和 Web Shell 移植到桌面应用，麦克风按钮、录制工具栏、停止/发送等交互已实现，提升非键盘输入场景的可用性。  
   [QwenLM/qwen-code PR #5856](https://github.com/QwenLM/qwen-code/pull/5856)

4. **[#5888] feat(channels): qwen tag — 多频道驻留 Agent（Phase 0）**  
   基于现有 channel adapter 和 daemon 架构，引入“qwen tag”驻群助手概念，初步支持钉钉群内的多用户协作 agent。RFC 与 Phase 0 实现同行，标志着 Qwen Code 走向多人协同的重要一步。  
   [QwenLM/qwen-code PR #5888](https://github.com/QwenLM/qwen-code/pull/5888)

5. **[#5868] feat(core): 可配置自动压缩阈值与 Stop 钩子上下文**  
   赋予用户控制上下文压缩时机的 `auto-compact` 阈值，并让 Stop 钩子能访问当前 context 使用情况，方便精细调优长对话场景。  
   [QwenLM/qwen-code PR #5868](https://github.com/QwenLM/qwen-code/pull/5868)

6. **[#5946] fix(core): 隔离 Anthropic SDK 的 abort 监听泄露**  
   为每次请求创建独立的子 controller，避免 SDK 内部的 abort 监听器残留导致内存泄漏或意外取消。对长期运行的服务端影响显著。  
   [QwenLM/qwen-code PR #5946](https://github.com/QwenLM/qwen-code/pull/5946)

7. **[#5879] feat(web-shell): 在 `/mcp` 对话框中浏览 MCP 服务器资源**  
   让 Web Shell 的 MCP 管理面板达到终端 TUI 同等水平：展示资源数量、按服务器展开查看资源及 prompt 列表，降低 MCP 配置门槛。  
   [QwenLM/qwen-code PR #5879](https://github.com/QwenLM/qwen-code/pull/5879)

8. **[#5928] feat(config): 新增 `todosDirectory` 设置用于项目级待办持久化**  
   允许用户将 todo-write 工具创建的待办持久化到项目内目录（如 `.qwen/todos`），使之受 Git 版本控制，从而支持跨设备与团队同步。回应 #5836。  
   [QwenLM/qwen-code PR #5928](https://github.com/QwenLM/qwen-code/pull/5928)

9. **[#5943] feat(web-shell): 添加错误边界防止单组件崩溃致整页白屏**  
   在 Web Shell 中引入三层 ErrorBoundary：通用层、消息体层、以及代码块/渲染子树层。提升嵌入式场景下的健壮性。  
   [QwenLM/qwen-code PR #5943](https://github.com/QwenLM/qwen-code/pull/5943)

10. **[#5848] feat(ui): 添加 `ui.history.collapsePreviewCount` 设置**  
    恢复被折叠的会话时，支持保留最近 N 轮用户对话可见，避免完全折叠后无法快速定位上下文，改善长会话的恢复体验。  
    [QwenLM/qwen-code PR #5848](https://github.com/QwenLM/qwen-code/pull/5848)

---

## 功能需求趋势

从过去 24 小时的 Issues 中可以提炼出社区最关注的五个方向：

- **模型选择与费用透明**：自动升档、默认输出上限不合理、Prompt cache 未命中导致成本失控——开发者对 token 消耗和模型切换的 **可预见性** 要求显著提升。
- **持久化与跨设备协作**：待办/记忆/计划的 Git 化存储、`.qwen/loop.md` 可编辑任务文件、团队级 memory 分层——用户迫切需要 **工作状态能被版本管理并跨机器同步**。
- **后台任务可观测性**：`/loop` 的静默执行、无法列举/停止已调度的 cron——社区希望获得与前台相同的 **任务可见与控制能力**。
- **浏览器/IM 生态融合**：Chrome 扩展复活、Telegram bot 命令对齐、钉钉驻群助手（qwen tag）——**脱离终端**，在聊天和浏览器中使用 Qwen Code 成为重要演进方向。
- **UI/UX 细节打磨**：滚动跳跃、边界裁剪、消息重复附加、错误白屏——随着用户基础扩大，桌面与 Web Shell 的 **交互稳定性** 关注度上升。

---

## 开发者关注点

- **升级风险**：#5819 暴露了自动升级后模型配置被静默更改的问题，开发者期望版本升级时有 **清晰的变更日志与配置保留保证**。
- **成本失控焦虑**：默认 8K 截断导致的重试循环、Anthropic 侧 prompt-cache 浪费、Windows cua-driver 空转，都直接反映为 **API 费用或计算资源无谓消耗**，这是用户最敏感的痛点。
- **上下文恢复的可靠性**：#5920 的 `parentUuid` 为 null 导致历史丢失，使得“会话持久化”这一核心功能出现严重退化，社区对 **断点恢复的正确性测试** 期待更高。
- **跨设备工作流**：多名用户在 Issues 中反映“换了电脑就丢失项目状态”，将状态纳入 Git 控制已从“锦上添花”变为 **刚需**。
- **长期运行 Agent 的可管理性**：`/loop` 的静默自动执行表明，社区希望 Agent **“能创建也能销毁”**，并提供审计日志，否则会引发信任问题。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

## 2026-06-28 DeepSeek TUI 社区动态日报

### 今日速览

插件系统核心基础设施批量合入主分支，为 CodeWhale 提供轻量级扩展能力；ACP 协议适配器实现流式输出与取消支持，显著改善 Zed 等编辑器的集成体验；社区围绕缓存命中率和 token 消耗的讨论依然激烈，多个优化 PR 同步推进。v0.8.66 发布台账已更新，记录当前候选状态与关键记分卡。

> *注：数据来源于 [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale) 仓库，原描述中的 “DeepSeek-TUI” 可能为笔误，实际仓库名称为 CodeWhale。*

---

### 社区热点 Issues（10 条）

| # | 标题 | 热度 | 摘要 | 链接 |
|---|------|------|------|------|
| 1 | **输入缓存命中率太低了** | 💬 24 | 对比 DeepSeek-Reasonix 的 95%+ 命中率，CodeWhale 差距巨大，用户呼吁尽快改善。 | [#1177](https://github.com/Hmbown/CodeWhale/issues/1177) |
| 2 | **缓存命中方面似乎还是有些问题** | 💬 21 | 即使更新到 0.8.17 后 input_cache_miss 问题仍未解决，用户期望明确进展。 | [#1120](https://github.com/Hmbown/CodeWhale/issues/1120) |
| 3 | **token 消耗增大了很多** | 💬 13 | 半天消耗 4 亿 token，请求过于密集，要求优化对话轮次交互。 | [#743](https://github.com/Hmbown/CodeWhale/issues/743) |
| 4 | **Put it up for agentclientprotocol/registry** | 💬 12 | 请求列入 ACP 官方 Registry，方便 Zed 等编辑器直接安装使用。 | [#3192](https://github.com/Hmbown/CodeWhale/issues/3192) |
| 5 | **CodeWhale is overly involved in self-questioning and self-answering** | 💬 12 | #3061 引入的回归问题：Agent 在 plan 模式下自问自答，不等待用户确认便执行操作。 | [#3275](https://github.com/Hmbown/CodeWhale/issues/3275) |
| 6 | **Fleet model classes, loadout auto, and semantic route roles** | 💬 10 | 定义 Fleet 自动模式下的共享模型/负载选择器，涉及 TUI、CLI、exec、subagent 等多个维度。 | [#3205](https://github.com/Hmbown/CodeWhale/issues/3205) |
| 7 | **EPIC: staged command-boundary refactor** | 💬 9 | 大规模重构跟踪 EPIC，通过分层 PR 实现命令边界清晰化，影响核心指令解析架构。 | [#2870](https://github.com/Hmbown/CodeWhale/issues/2870) |
| 8 | **plan 和 agent 模式混合的问题似乎仍然存在** | 💬 6 👍1 | 用户上传对话证据，展示在 plan 模式下 agent 依然尝试修改文件，模式感知失效。 | [#3568](https://github.com/Hmbown/CodeWhale/issues/3568) |
| 9 | **Cache hit problem** | 💬 4 👍3 | 多用户提出 UI 可读性差的同时，缓存命中率低依然是核心痛点。 | [#1747](https://github.com/Hmbown/CodeWhale/issues/1747) |
| 10 | **Adopt Moraine as CodeWhale's memory backend** | 💬 4 | 引入 Moraine 作为长时记忆后端，无损持久化会话并通过 MCP 提供搜索召回能力。 | [#3495](https://github.com/Hmbown/CodeWhale/issues/3495) |

---

### 重要 PR 进展（10 条）

| # | 标题 | 类型 | 说明 | 链接 |
|---|------|------|------|------|
| 1 | **feat(plugins): add manifest parsing, discovery, and registry** | 功能 | 插件系统核心基础设施：`plugin.toml` 解析、目录发现、注册管理与启用/禁用。 | [#3708](https://github.com/Hmbown/CodeWhale/pull/3708) |
| 2 | **feat(prompts): allow overriding the base prompt from the config dir** | 功能 | 允许通过配置文件覆盖基础提示词（#3638），使用户能用于文学创作等非编程场景。 | [#3696](https://github.com/Hmbown/CodeWhale/pull/3696) |
| 3 | **feat(acp): stream session/prompt deltas as session/update chunks** | 功能 | ACP 适配器从缓冲输出改为流式输出，Zed 等编辑器可增量渲染回复（#3192）。 | [#3702](https://github.com/Hmbown/CodeWhale/pull/3702) |
| 4 | **feat(acp): cancel in-flight session/prompt on session/cancel** | 功能 | 支持在 session/prompt 进行中接收 session/cancel，避免阻塞后续请求（#3192）。 | [#3698](https://github.com/Hmbown/CodeWhale/pull/3698) |
| 5 | **feat(working-set): cache-maximal context mode — materialize active file contents** | 功能 | 实现缓存最大化模式：保持活跃文件的完整内容，减少模型重复读文件造成的工具调用（#528）。 | [#3697](https://github.com/Hmbown/CodeWhale/pull/3697) |
| 6 | **fix(engine): suggest direct URLs after repeated search errors** | 修复 | 搜索重复失败时收集已使用的域名，建议直接使用 `fetch_url` 作为回退（#1641）。 | [#3705](https://github.com/Hmbown/CodeWhale/pull/3705) |
| 7 | **fix(engine): add fallback hints for transient tool errors** | 修复 | 对网络超时、请求失败等临时错误附加模型可见的回退提示，避免重复调用（#1641）。 | [#3701](https://github.com/Hmbown/CodeWhale/pull/3701) |
| 8 | **fix(engine): nudge fallback after repeated tool errors** | 修复 | 多次工具错误后动态注入运行时提示，引导模型切换工具或缩小范围（#1641）。 | [#3703](https://github.com/Hmbown/CodeWhale/pull/3703) |
| 9 | **fix(verifier): emit hunt verdict mapping** | 修复 | 将验证器结果（pass/partial/fail）映射为 hunt 判定（hunted/wounded/escaped），完善奖杯系统（#2093）。 | [#3700](https://github.com/Hmbown/CodeWhale/pull/3700) |
| 10 | **docs: add v0.8.66 release ledger** | 文档 | 记录 v0.8.66 发布候选状态、ACP 注册提交情况、issue 分类进展及 token/cache 记分卡。 | [#3707](https://github.com/Hmbown/CodeWhale/pull/3707) |

---

### 功能需求趋势

从本周的 Issues 和 PR 中可以提炼出社区最关注的 **六大技术方向**：

1. **缓存与 Token 优化**  
   - 问题：输入缓存命中率远低于竞品（Codex CLI、DeepSeek-Reasonix），导致 token 消耗暴涨、响应缓慢。  
   - 方向：引入 cache‑maximal 上下文模式（#3697）、精简 prompt 体积、减少冗余工具输出。

2. **模型提供商与多模型支持**  
   - 需求：统一不同 provider（vLLM、OpenAI、Codex OAuth）的路由，实现 Fleet 自动负载选择。  
   - 相关 Issue：#2300、#3205、#2984。

3. **Agent 行为可预测性**  
   - 痛点：plan 模式下 agent 仍执行修改操作（#3568、#3275），自问自答偏离用户意图。  
   - 方向：模式状态严格隔离、增加显式确认机制。

4. **工具调用容错与回退**  
   - 场景：搜索、API 等外部服务失败时 agent 反复重试直至失败（#1641）。  
   - 今日已合并多个优雅降级 PR（#3701、#3703、#3705），引导模型主动切换策略。

5. **外部编辑器与 IDE 集成**  
   - 需求：通过 ACP 协议使 Zed、Cursor 等编辑器能够安装并使用 CodeWhale（#3192）。  
   - 进展：流式输出与取消支持已合入（#3702、#3698），初步可用。

6. **扩展性与个性化**  
   - 呼声：插件系统（#3699）、基础提示词可替换（#3638）、Moraine 记忆后端（#3495）、Rust 原生客户端（#3541）。  
   - 趋势：社区希望从 “专用编程工具” 扩展到 “通用 AI 代理平台”。

---

### 开发者关注点

根据近期用户的**高频反馈与痛点**，总结如下：

| 关注点 | 典型反馈 |
|--------|----------|
| **缓存命中率低** | “与 DeepSeek-Reasonix 差了十万八千里”，认为 “急需改善”（#1177、#1120、#1747）。 |
| **Token 消耗失控** | “半天 4 亿 token”、“合并报告时缓存命中巨低且巨慢”（#743、#1732、#1818）。 |
| **模式感知混乱** | “plan 模式下 agent 依然在尝试修改文件”（#3568、#3275），用户需要一次明确的切换。 |
| **工具失败无脑重试** | “搜索被反爬后一直重试直到失败”，希望有 fallback 策略（#1641）。 |
| **TUI 界面可用性** | “信息密集、低信噪比”，Hotbar、侧边栏等需要重新设计（#3480、#3389）。 |
| **集成壁垒** | “被 ACP registry 收录才能让 Zed 轻松使用”，需要官方主动推进（#3192）。 |
| **非编程场景受限** | 希望用相同工具进行写作、文档审阅，但 “工程提示词完全不适用”（#3638、#3354）。 |

从合并节奏看，核心维护者正在以 v0.8.66 为基线快速响应缓存与回退问题，同时推进插件与 ACP 集成。社区参与度较高，多个 PR 来自外部贡献者（findshan、cyq1017、pkeging 等），说明项目活跃度正逐步提升。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*