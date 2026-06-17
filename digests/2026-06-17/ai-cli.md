# AI CLI 工具社区动态日报 2026-06-17

> 生成时间: 2026-06-17 03:46 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-06-17）

## 1. 生态全景

当前 AI CLI 工具正从原型验证加速迈入生产就绪阶段，**模型兼容性、安全管控与跨平台体验**成为社区核心诉求。各工具均在高频迭代（单日发布2个版本的工具不在少数），但频繁的回归也让用户对“修好一个，弄坏三个”产生疲劳。MCP（Model Context Protocol）已从可选功能上升为生态基础设施，围绕其安全性、配置管理与子进程资源控制的讨论显著增长。整体而言，行业正从跑马圈地转向精细化打磨，**稳定性与信任度成为用户粘性的关键分水岭**。

## 2. 各工具活跃度对比

| 工具 | 重点议题（精选） | 活跃 PR（精选） | 版本发布 | 社区规模感知 |
|------|----------------|----------------|----------|-----------|
| Claude Code | 10 | 10 | 1 (v2.1.179) | 极高（单Issue评论87） |
| OpenAI Codex | 10 | 10 | 2（alpha.3/4） | 高（账户锁死46条评论） |
| Gemini CLI | 10 | 10 | 0 | 中等 |
| GitHub Copilot CLI | 10 | 0 | 1 (v1.0.64-0) | 高（企业模型支持焦点） |
| Kimi Code CLI | 4 | 1 | 0 | 低 |
| OpenCode | 10 | 10 | 0 | 中高（/goal获88👍） |
| Pi | 10 | 9 | 2 (v0.79.5/6) | 中等 |
| Qwen Code | 10 | 10 | 0*（发布失败） | 极高（API额度调整136评论） |
| DeepSeek TUI (CodeWhale) | 10 | 9 | 1 (v0.8.61) | 中等 |

> *Qwen Code 的 release 流水线因集成测试失败中断，未实际发布正式版。GitHub Copilot CLI 的 PR 数在统计期内为 0，但其版本发布包含新功能代码（已在之前合并）。*

## 3. 共同关注的功能方向

**（1）MCP / 插件系统的安全与配置管理**
几乎所有工具都在讨论 MCP 相关问题：Claude Code 面临子进程泄漏（#68933）和符号链接逃逸（#68689）；OpenAI Codex 修复 MCP OAuth 刷新竞争（PR #28647）；Gemini CLI 关注 OAuth 令牌原子写入与跨服务器 URI 混淆（#27664, #27964）；Copilot CLI 在 v1.0.64-0 中新增 MCP 注册表安装；Kimi Code 出现已删除 MCP 仍被自动发现的 Bug（#2457）；Qwen Code 推动项目级 `.mcp.json` 批准语义（#4615）和密钥加密存储（#5221）。**社区共识是 MCP 需要企业级权限模型和生命周期管理**。

**（2）跨平台兼容性与国际化**
Windows 仍是薄弱环节：Claude Code 的桌面进程锁（#42776, 87条评论）和路径归一化（#68694）；OpenAI Codex 的非 ASCII 用户名崩溃（#27506）和 Git 进程风暴（#20567）；Copilot CLI 的 ARM64 崩溃（#3687）；OpenCode 的 PowerShell UTF-8 包装（PR #31985）；Pi 的 CP1252 编码问题（#5797）；Qwen Code 的 Trojan 误报（#5055）。多字节字符（西里尔文、中日韩）在终端下的复制乱码被多工具用户诟病，**国际化现已成为影响工具口碑的硬指标**。

**（3）Agent 行为的可预测性与稳定性**
多工具用户反映 Agent 挂起、卡死、状态误报：Claude Code 的 agent 通知路由错误（#68065）；Gemini CLI 的“无限挂起”（#21409）和子代理误报“成功”（#22323）；Copilot CLI 的子代理模型不一致（#3824）与取消操作被重新注入（#3826）；DeepSeek TUI 的 turn stall（#2487, #2739）和过度修改（#3275）；OpenCode 的随机挂起（#2940）。**用户对 Agent 自主性的耐心正在下降，强烈要求“ask before act”模式和清晰的熔断机制**。

**（4）成本与配额透明化**
Claude Code 的配额重置首请求即耗尽（#68973）、Pro 计划被阻止使用 1M 上下文（#65514）；OpenAI Codex 引入共享 Token 预算（PR #28494）；Qwen Code 的免费额度拟从 1000 降至 100 次/天（#3203, 136条评论，该工具当前最热议题）。**开发者要求 AI 工具提供细粒度的消耗分析和可配置的限流策略，而不仅是硬性中断**。

**（5）安全加固全面升级**
从 shell 注入（Claude Code PR #68786）到符号链接逃逸（#68689）、敏感路径阻断（Gemini CLI #27966）、凭证代理（OpenAI Codex PR #28034）、CRLF 清洗（Claude Code #68701）、密钥加密回退（Qwen Code #5221），**安全已成为每个版本发布的标准组成部分，而非事后补丁**。

## 4. 差异化定位分析

| 工具 | 核心绑定 | 特色定位 | 目标用户 | 技术路线 |
|------|---------|---------|---------|---------|
| **Claude Code** | Anthropic Claude 模型 | 深度插件化 + 企业级安全 | 高端开发者、团队协作 | 封闭模型 + 开放插件体系 |
| **OpenAI Codex** | OpenAI GPT/Codex | 桌面+CLI 双入口，原生 Codex 优化 | OpenAI 生态用户 | 封闭模型，桌面优先 |
| **Gemini CLI** | Google Vertex AI | GCP 集成，多模态潜力 | Google Cloud 开发者 | 封闭模型，注重安全与合规 |
| **GitHub Copilot CLI** | GitHub + OpenAI | GitHub 工作流一体化，企业管控 | GitHub 企业用户 | 封闭模型，托管开发闭环 |
| **Kimi Code CLI** | 月之暗面 Kimi | 轻量简洁，优先中文市场 | 国内个人开发者 | 封闭模型，易用性优先 |
| **OpenCode** | 模型中立（OpenAI 兼容） | 社区驱动，功能密集（Skill/插件/TUI） | 偏好开源的开发者 | 开放多模型，自托管友好 |
| **Pi** | 模型中立（多 Provider） | 高可配置性（provider 作用域环境变量） | 多后端混合使用的开发者 | 开放多模型，灵活配置架构 |
| **Qwen Code** | 阿里通义千问 | 本土生态（QQ频道，视觉桥接），MCP安全 | 中文开发者、阿里云用户 | 以 Qwen 为主，兼容多模型 |
| **DeepSeek TUI (CodeWhale)** | 原 DeepSeek，现已品牌中立 | Rust 实现 + Chat-native Workroom（持久化工作区） | 追求性能与新交互形态的用户 | 开源多模型，TUI 性能优先 |

**核心差异线**在于：官方绑定模型 vs. 模型中立。Claude Code / Gemini CLI / Qwen Code / Kimi Code 高度绑定自家模型，可深度优化但面临模型质量波动风险（如 Opus 4.8 问题直接冲击 Claude Code 口碑）。OpenCode、Pi、DeepSeek TUI 走开放路线，灵活但需为每个模型做兼容修复。Copilot CLI 绑定 OpenAI 但背靠 GitHub 生态，企业定制空间更大。

## 5. 社区热度与成熟度

- **高热社区**：Claude Code（单 Issue 87 条评论，Opus 质量引发广泛讨论）、OpenAI Codex（账户死锁 46 条、macOS 崩溃 33 条）、Qwen Code（免费额度调整 136 条回复）。这三家**用户基数大、期待高，但稳定性问题也最突出**，处于“高关注、高不满”的摩擦期。
- **中高活跃**：OpenCode（/goal 获 88 👍，多个功能 PR 同步推进）、GitHub Copilot CLI（企业自定义模型诉求 4 👍，社区期待强烈但 PR 更新少，说明开发可能以内部为主）、Pi（连续 2 个版本，9 个 PR 更新，迭代积极）。这些工具**社区反馈质量较高，官方响应速度快**。
- **中等活跃**：Gemini CLI（PR 多但 Issue 热度相对平缓）、DeepSeek TUI（品牌重塑期，Workrooms PR 引入，但稳定性 Bug 持续）。
- **低活跃**：Kimi Code CLI（仅 4 个重点 Issue、1 个 PR，社区体量较小，产品处于早期）。

**成熟度判断**：没有任何工具达到 1.0+ 的成熟水平。Copilot CLI 版本号最高（v1.0.64），但社区依然频繁遇到崩溃和配置问题；Claude Code 迭代最密集（每日发布），但也因此回归频繁；OpenCode 和 Pi 虽无正式大版本，功能完整性已不逊于官方工具。整体来看，**CLI 市场仍处于“青春期”，用户对稳定性的耐心正在消耗，率先解决基础可靠性的工具将赢得信任分水岭**。

## 6. 值得关注的趋势信号

**（1）MCP 标准化进入深水区——安全与治理成为新瓶颈**
所有工具都在抢着支持 MCP，但 token 刷新竞争条件、URI 跨服务器混淆、子进程泄漏等问题表明，**协议本身已够用，但运行时安全架构还远未成熟**。未来 6-12 个月，MCP Server 的生命周期管理、权限沙箱、审计日志可能成为差异化竞争点。

**（2）模型质量波动直接反噬工具口碑**
Claude Code 的 Opus 4.8 tool_use 畸形（#63604）、Qwen Code 的模型切换失效、OpenCode 的 MiniMax 兼容问题，说明**AI CLI 作为“模型消费者”，其用户体验高度依赖上游模型稳定性**。工具开发团队应建立模型灰度发布和快速回退机制，降低单一模型质量波动带来的冲击。

**（3）“AI 代理疲乏”显现——用户要求更可控的执行流**
从多个工具的反馈看，用户已经厌倦了 Agent 自行其是、卡住或消耗大量配额的行为。**2026 年下半年的趋势将是“可控 Agent”：明确的任务边界、可取消的中间步骤、透明的成本显示**。Copilot CLI 的 `--allow-all` 导致界面卡死（#3825）、DeepSeek TUI 的过度修改（#3275）都是反例。

**（4）跨平台不再是可选项，而是基础入场券**
Windows 用户已成为社区反馈的主力（Claude Code #42776 是最高评论 Issue），亚洲用户的多字节编码问题也频繁出现。**忽视平台差异的工具将失去大量潜在用户**，OpenCode 和 Pi 通过快速修复编码问题获得了社区点赞，值得借鉴。

**（5）开源多模型 CLI 正在形成对官方工具的替代压力**
OpenCode、Pi、DeepSeek TUI（CodeWhale）三个开源项目在功能迭代速度上不输官方工具，且在模型中立性、本地部署、自定义配置方面具备天然优势。**对于对 Vendor Lock-in 敏感的开发者，这些工具正在成为主流选择**。官方工具若不在开放性和企业可控上加大投入，可能被开源生态蚕食市场份额。

---

**对开发者的建议**：选择 AI CLI 工具时，优先考虑**社区响应速度、安全实践成熟度、以及对多种模型的容错能力**。核心工作流不应绑定单一模型的稳定性；在预算敏感场景下，选择支持清晰配额可见性（如 OpenCode 的 token 浪费追踪）和可配置限流的工具更为稳妥。同时，关注工具对于 Agent 自主度的可调节性——能够从“完全自主”到“逐步确认”之间切换的工具，将更适合多样化的开发任务。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-06-17）

---

## 一、热门 Skills 排行

社区关注度由 Pull Request 评论数衡量（数据取自官方仓库 `anthropics/skills` 按评论数排序的前 20 条 PR，以下列出其中 8 个新增 Skill 类 PR，状态均为 **Open**）。

| 排名 | PR | Skill 名称 | 功能摘要 | 社区讨论热点 | 状态 |
|------|----|------------|----------|--------------|------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | AI 生成文档的排版质量控制，解决孤词、孤行、编号错位等常见问题 | 排版质量对每个文档任务都有影响，开发者普遍认可其必要性；讨论集中在规则可配置性及与现有文档技能的集成方式 | Open |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT** | 创建、填充、读取、转换 OpenDocument 格式（.odt, .ods），兼容 LibreOffice 及 ISO 标准 | 社区对开源文档格式的原生支持呼声高，尤其在企业环境中 ODT 需求明显；模板填充和 HTML 互转是讨论焦点 | Open |
| 3 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1-OSS predictor** | 调用 SAP 开源表格基础模型进行企业数据分析预测 | 企业级智能场景受到关注，讨论集中在如何与既有 SAP 系统对接以及预测结果的可解释性 | Open |
| 4 | [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | 覆盖全栈测试模式：单元测试、React 组件测试、E2E、快照测试等 | 开发者将测试技能视为提升 Claude 代码质量的杀手锏，讨论涉及测试 Trophy 模型落地和确保技能足够具体而不泛泛 | Open |
| 5 | [#335](https://github.com/anthropics/skills/pull/335) | **masonry-generate-image-and-videos** | 通过 Masonry CLI 调用 Imagen、Veo 等模型生成图像和视频 | 多模态生成需求旺盛，社区关注技能对视频生成任务（Veo 3.1）的支持程度以及任务管理和历史追溯功能 | Open |
| 6 | [#154](https://github.com/anthropics/skills/pull/154) | **shodh-memory** | 为 AI Agent 提供跨会话持久化记忆，自动触发上下文关联 | 记忆技能被认为是 Agent 长期可用的关键；讨论集中在如何避免记忆膨胀、隐私边界以及 `proactive_context` 的触发准确率 | Open |
| 7 | [#568](https://github.com/anthropics/skills/pull/568) | **servicenow** | 全栈 ServiceNow 平台辅助，覆盖 ITSM、ITOM、SecOps、ITAM、FSM、SPM、CSDM、IntegrationHub 等 | 企业 ITSM 场景关注度高，社区讨论强调技能需覆盖模块广且提供足够的平台架构指导，而非仅限脚本编写 | Open |
| 8 | [#444](https://github.com/anthropics/skills/pull/444) | **AURELION skill suite**（kernel, advisor, agent, memory） | 结构化认知框架与知识管理套件，提供五层思维模板及协作模式 | 认知框架类技能持续获得关注，社区希望该套件能与其他记忆技能配合，形成可组合的“思维操作系统” | Open |

> 注：另有 #83（skill-quality-analyzer，元技能）和 #210（frontend-design 改进）也获得大量评论，因属改进/元技能而未列入上表，但同样说明社区对技能质量和前端领域的高度兴趣。

---

## 二、社区需求趋势

从仓库 Issues（按评论数排序前 15 条）提炼出社区最关注的 4 大需求方向：

### 1. 🔗 技能共享与组织协作
- **#228**（👍 7，评论 14）：用户强烈要求直接在 Claude.ai 内支持组织级技能共享，避免手动下载和导入的低效流程。
- **#189**（👍 9，评论 6）：插件安装导致技能重复，反映用户对技能分发机制的准确性期望更高。

### 2. 🛡️ 安全、信任与治理
- **#492**（评论 7）：社区技能以 `anthropic/` 命名空间分发引发信任边界担忧，要求明确官方与社区技能的区分机制。
- **#412**（评论 6）：明确提出需要 **agent-governance** 技能，用于 AI Agent 的策略执行、威胁检测与审计。这是目前缺失的重要领域。
- **#1175**（评论 4）：用户关注当处理 SharePoint Online 文档时，SKILL.md 中包含权限逻辑带来的安全与上下文窗口风险。

### 3. 🛠️ 工具链稳定性与跨平台兼容
- **#556**（👍 7，评论 12）与 **#1169**（评论 3）：`run_eval.py` 在评估时始终报 `recall=0%`，导致技能优化循环无法正常运作，严重阻碍社区贡献者迭代技能描述。
- **#1061**（评论 3）及多个 Fix PR（#538、#539、#541、#1099、#1050、#362）集中反映 **Windows 兼容性** 是工具链最大短板，包括子进程调用、编码处理、管道选择等问题。社区迫切希望 skill-creator 脚本能在 Windows 上开箱即用。

### 4. 📄 新技能方向呼声
- **#412** agent-governance（见上）
- **#16**（评论 4）：希望将 Skills 暴露为 MCP 协议，使技能可编程调用。
- **#1220**（评论 2）：多文件预加载 / 内联捆绑，解决技能拆分为多个参考文件后的交付效率问题。
- **#29**（评论 4）：需求 AWS Bedrock 集成支持。

**总结走势**：社区需求正从“创建更多技能”转向“技能生态基础设施”，包括共享分发、安全治理、工具链稳定及平台扩展。纯功能型技能提案热度有所下降，而治理、兼容性、元工具类议题持续升温。

---

## 三、高潜力待合并 Skills

以下 PR 评论活跃且为实质性新技能，社区关注度高、质量较成熟，有较大可能在近期合并：

1. **[document-typography](https://github.com/anthropics/skills/pull/514)**（#514）  
   - 解决 AI 文档生成的普遍痛点，定位清晰，与现有文档技能无冲突，合并优先级极高。

2. **[testing-patterns](https://github.com/anthropics/skills/pull/723)**（#723）  
   - 覆盖测试全栈，社区广泛认可，若与现有前端技能联动可产生更大价值。

3. **[shodh-memory](https://github.com/anthropics/skills/pull/154)**（#154）  
   - 记忆是 Agent 长期能力基石；虽有类似提案，但其实现方法（显式 `proactive_context`）讨论成熟，有望成为基础技能。

4. **[servicenow](https://github.com/anthropics/skills/pull/568)**（#568）  
   - 企业级 ITSM 需求旺盛，技能覆盖面广，但需关注与官方 ServiceNow 工具的重叠治理。

5. **[ODT](https://github.com/anthropics/skills/pull/486)**（#486）  
   - 填补 ISO 标准文档格式支持空白，与企业文档工作流强相关，且长期未合并（创建于 2026-03-01，持续更新），表明作者积极维护。

> 此外，**[SAP-RPT-1-OSS](https://github.com/anthropics/skills/pull/181)**（#181）和 **[AURELION suite](https://github.com/anthropics/skills/pull/444)**（#444）关注度高但领域较垂直，需视官方战略决定合并节奏。

---

## 四、Skills 生态洞察

**当前社区在 Skills 层面最集中的诉求是：从“技能数量扩张”转向“生态成熟度提升”——修复工具链可靠性、增强跨平台兼容、建立信任与治理机制，并在共享分发、记忆持久化和安全治理等基础能力上补齐短板。**  

尽管新增功能型技能依然活跃，但 Issue 区的高赞话题和大量 Fix PR 表明，**社区贡献者的主要瓶颈在于工具链不稳定（尤其是 Windows 兼容与评估流程失效），而企业用户的焦点则在于安全命名空间、组织级共享和治理技能等基础设施问题。** 唯有打好这些基础，Claude Code Skills 才能真正进入规模化采用阶段。

---

# Claude Code 社区动态日报 | 2026-06-17

## 今日速览
昨日发布 **v2.1.179**，修复了流式连接中断导致响应丢失与 WSL2 下的滚动回归。社区 Issue 方面，Windows 桌面应用因进程锁无法重登（#42776）依然热度最高；Opus 4.8 的 tool_use 异常与性能下降成为新焦点。PR 侧涌现了大量安全性及平台兼容性修复（shell 注入、符号链接逃逸、Windows 路径归一化等），同时 `PowerShell 工具`跨平台支持与 `/bug` 命令等实用功能也进入活跃阶段。

## 版本发布

### v2.1.179
- **修复** 流式连接中途断开：部分响应不再直接报错，spinner 也不再卡在 "running tool"
- **修复** WSL2 下 Windows Terminal 和 VS Code 中鼠标滚轮滚动异常（v2.1.172 引入的回归）
- **修复** Sandbox 中 `denyR`（待确认完整条目）相关问题

## 社区热点 Issues（10 条）

### 1. #42776 – [BUG] Windows 桌面应用因孤儿进程锁无法重启
- **评论**: 87 | **👍**: 31 | **状态**: 开放
- **概述**: Windows 上 Claude Code Desktop 进程异常退出后留下进程锁，导致后续无法重新启动。该问题已持续两个多月，社区反馈强烈，是目前评论量最高的 Issue。
- 👉 [https://github.com/anthropics/claude-code/issues/42776](https://github.com/anthropics/claude-code/issues/42776)

### 2. #63604 – [BUG] Opus 4.8 反复输出畸形的 tool_use 块，整条响应被丢弃
- **评论**: 10 | **👍**: 12 | **状态**: 开放
- **概述**: 使用 Opus 4.8 时模型频繁生成无法解析的 tool_use，触发 harness 错误 "Your tool call was malformed"，导致整个回复作废。4.7 无此问题。开发者高度关注，直接影响了日常自动编码流程。
- 👉 [https://github.com/anthropics/claude-code/issues/63604](https://github.com/anthropics/claude-code/issues/63604)

### 3. #68982 – [BUG] Cloud 会话消息被静默丢弃，UI 卡在 "running"
- **评论**: 2 | **👍**: 0 | **状态**: 开放（今天创建）
- **概述**: 在 Cloud 会话中发送消息后 UI 永远显示运行中，无 token 消耗，刷新后消息完全消失（未持久化）。若频繁发生将严重影响线上工作流。
- 👉 [https://github.com/anthropics/claude-code/issues/68982](https://github.com/anthropics/claude-code/issues/68982)

### 4. #68933 – [BUG] skill-creator 插件 MCP 子进程泄漏，耗尽内存强制重启
- **评论**: 4 | **👍**: 0 | **状态**: 开放
- **概述**: skill-creator 的 eval/optimizer 在每次测试查询时启动一个 `claude -p` 进程，若项目配置了 MCP Server，每个进程都会拉起完整 MCP 栈。大量并发导致内存耗尽，需要硬重启。对插件开发者影响极大。
- 👉 [https://github.com/anthropics/claude-code/issues/68933](https://github.com/anthropics/claude-code/issues/68933)

### 5. #65514 – [BUG] Pro 计划使用 1M 上下文时被阻止
- **评论**: 17 | **👍**: 2 | **状态**: 开放
- **概述**: 用户在 Pro 计划下使用量仅 17% 仍被要求购买额外 credits，无法调用 1M 上下文模型，引发对计费边界的质疑。
- 👉 [https://github.com/anthropics/claude-code/issues/65514](https://github.com/anthropics/claude-code/issues/65514)

### 6. #68973 – [BUG] 配额重置后首次请求即消耗 30%~40%
- **评论**: 2 | **👍**: 0 | **状态**: 开放（今天创建）
- **概述**: 触发限流并选择 "stop and wait" 后，配额重置的第一个请求因 prompt cache 过期及 compaction 死锁，瞬间消耗大量配额。对按量付费用户影响直接。
- 👉 [https://github.com/anthropics/claude-code/issues/68973](https://github.com/anthropics/claude-code/issues/68973)

### 7. #68979 – [BUG] Kitty 键盘协议在 tmux 中破坏 Ctrl-A / Ctrl-E
- **评论**: 1 | **👍**: 0 | **状态**: 开放（今天创建）
- **概述**: tmux 开启 `extended-keys on` 后，Claude Code 启用 Kitty 键盘协议但握手不完整，导致 iTerm2 中 Cmd+左/右 发出的 Ctrl-A/Ctrl-E 被作为字面字符插入输入框。影响终端重度用户。
- 👉 [https://github.com/anthropics/claude-code/issues/68979](https://github.com/anthropics/claude-code/issues/68979)

### 8. #64235 – [BUG] 间歇性 "tool call was malformed"，`stop_reason=tool_use` 但响应缺少 tool_use 块
- **评论**: 5 | **👍**: 2 | **状态**: 开放
- **概述**: 自 2026-05-29 起出现的回归：模型明明以 tool_use 结束，但实际响应中没有对应工具块，导致 harness 报错重试，用户看到的是 agent 思考后静默无反应。与 #63604 可能同源。
- 👉 [https://github.com/anthropics/claude-code/issues/64235](https://github.com/anthropics/claude-code/issues/64235)

### 9. #66098 – [BUG] TUI 中选择多字节 UTF-8 文本（如西里尔文）复制后乱码（OSC 52）
- **评论**: 2 | **👍**: 4 | **状态**: 开放
- **概述**: 在 Claude Code TUI 内选中非 ASCII 字符复制时，内容通过 OSC 52 路由，多字节字符损坏，ASCII 正常。影响非英语用户的日常使用。
- 👉 [https://github.com/anthropics/claude-code/issues/66098](https://github.com/anthropics/claude-code/issues/66098)

### 10. #68065 – [BUG] 顺序启动的后台 agent 通知路由到错误的 agent ID
- **评论**: 2 | **👍**: 2 | **状态**: 开放
- **概述**: 当两个独立后台 agent 顺序执行时，第二个 agent 的完成通知会在第一个 agent 的 task ID 上收到，且第二个 agent 从不发送自己的通知。导致执行树中 agent 丢失，对依赖 agent 编排的工作流造成混乱。
- 👉 [https://github.com/anthropics/claude-code/issues/68065](https://github.com/anthropics/claude-code/issues/68065)

## 重要 PR 进展（10 条）

### 1. #46351 – Enable PowerShell tool on macOS and Linux when pwsh is available
- **状态**: 已关闭 | **更新**: 2026-06-16
- **核心内容**: 解除 PowerShell 工具的 Windows 平台硬限制，macOS/Linux 上检测到 `pwsh` 即可启用，解决跨平台脚本编写的痛点。该 PR 关闭于 #45963，标志着对非 Windows 用户的重要增强。
- 👉 [https://github.com/anthropics/claude-code/pull/46351](https://github.com/anthropics/claude-code/pull/46351)

### 2. #68707 – feat(bug-reporter): add /bug command to file GitHub issues from the terminal
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 新增 `/bug` 指令，直接在终端内提交 GitHub Issue，简化用户反馈流程，降低报告门槛。
- 👉 [https://github.com/anthropics/claude-code/pull/68707](https://github.com/anthropics/claude-code/pull/68707)

### 3. #68786 – fix(plugin-dev): avoid shell injection in test-hook.sh via stdin redirection
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 修复 `test-hook.sh` 中将 `$TEST_INPUT` 嵌入单引号后放到 `bash -c` 字符串中可能导致的 shell 注入漏洞。安全相关。
- 👉 [https://github.com/anthropics/claude-code/pull/68786](https://github.com/anthropics/claude-code/pull/68786)

### 4. #68785 – fix(plugin-dev): hook responses to stdout, tighten su* glob, fix JSON injection in examples
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 修复三个示例 hook 脚本中的 bug：`validate-bash.sh` 将 hook 响应 JSON 写入 stderr（应写入 stdout），以及 JSON 注入等问题，使参考实现更可靠。
- 👉 [https://github.com/anthropics/claude-code/pull/68785](https://github.com/anthropics/claude-code/pull/68785)

### 5. #68689 – fix(security-guidance): block symlink escape in extensibility config reads
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 在可扩展性配置读取中阻止符号链接逃逸攻击，提升插件系统的安全性。
- 👉 [https://github.com/anthropics/claude-code/pull/68689](https://github.com/anthropics/claude-code/pull/68689)

### 6. #68694 – fix(security-guidance): normalize CLAUDE_PLUGIN_ROOT path separators on Windows
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: Windows 环境下 `CLAUDE_PLUGIN_ROOT` 路径分隔符归一化，避免因反斜杠/正斜杠混用导致的配置读取失败。
- 👉 [https://github.com/anthropics/claude-code/pull/68694](https://github.com/anthropics/claude-code/pull/68694)

### 7. #68701 – fix(security-guidance): strip CRLF from Python version probe on Windows
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 去除 Windows 上 Python 版本探测结果中的 CRLF 字符，防止字符串比较出错。
- 👉 [https://github.com/anthropics/claude-code/pull/68701](https://github.com/anthropics/claude-code/pull/68701)

### 8. #68699 – fix(hookify): add Python wrapper and normalize plugin root paths on Windows
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 为 hookify 添加 Python 包装器，并在 Windows 上归一化插件根路径，增强跨平台兼容性。
- 👉 [https://github.com/anthropics/claude-code/pull/68699](https://github.com/anthropics/claude-code/pull/68699)

### 9. #68678 – fix(triage): don't mark Claude Desktop issues as invalid
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 修复自动 triage 标签逻辑，不再将关于“Claude Desktop”的 Issue 自动标记为 "invalid"，减少误分类。
- 👉 [https://github.com/anthropics/claude-code/pull/68678](https://github.com/anthropics/claude-code/pull/68678)

### 10. #68679 – fix(ralph-wiggum): strip control characters before promise comparison
- **状态**: 开放 | **更新**: 2026-06-16
- **核心内容**: 在 promise 比较前剥离控制字符，避免因不可见字符导致判断失败，提升内部测试工具健壮性。
- 👉 [https://github.com/anthropics/claude-code/pull/68679](https://github.com/anthropics/claude-code/pull/68679)

## 功能需求趋势

### 1. MCP 生态扩展
社区持续要求增强 MCP（Model Context Protocol）能力，包括：
- **Microsoft 365 MCP 附件读取**（#30533，已关闭，👍15）
- **MCP stdio 服务文档补全**（#47635，文档缺失）
- **更清晰的 MCP 故障排查指引**

### 2. 平台支持与质量
Windows 仍然是问题集中区，但社区也关注 macOS/Linux 的完善：
- **进程锁 / 桌面应用稳定性**（#42776）
- **跨平台工具统一**（PowerShell 工具跨平台，PR #46351）
- **终端兼容性**（tmux / Kitty 键盘协议、OSC 52 编码）

### 3. 性能与成本控制
- **Opus 4.8 性能下降**（#68820、#68624）—— 用户期望模型速度回归正常
- **配额消耗过高**（#68973、#68961）—— 对代理循环次数缺乏智能限制
- **禁用流式输出的选项**（#37569，👍15）—— 减少视觉干扰

### 4. 代理（Agent）与工作流
- **背景 Agent 通知路由错误**（#68065）
- **Workflow 工具参数 JSON 双字符串化**（#68969）
- **代理循环过多消耗配额**（#68961） —— 用户期望 smarter throttling

### 5. 云（Cloud） / Web 会话
- **消息丢失**（#68982）
- **斜杠命令在外部触发远程执行时透传为提示词**（#68402，已关闭）

## 开发者关注点

### 1. Opus 4.8 质量问题突出
无论是 tool_use 解析失败（#63604、#64235）还是整体速度降低（#68820、#68624），开发者对 4.8 模型的稳定性表现出强烈不满。有用户直言“Haiku 当作 Opus 卖”。

### 2. Windows 平台体验仍为薄弱环节
- 桌面应用因进程锁无法重登（#42776，87 条评论，社区最热）
- Windows 上错误传递 macOS URI（#51701）
- TUI 中日语等多字节文本通过 OSC 52 复制乱码（#42417、#66098）
- 新渲染器下的键盘 & 滚动问题（#68979、#58579）

### 3. 配额与成本透明化
多个 Issue 指向“计费不清”：Pro 计划被阻止使用 1M 上下文（#65514）、重置后首次请求大量消耗（#68973）、代理循环浪费（#68961）。开发者期望 Anthropic 提供更细粒度的配额控制和消耗分析。

### 4. MCP 配置管理负担
- 系统提示因 MCP Server 安装膨胀到 9.3M tokens（#65429）
- skill-creator 插件的 MCP 子进程泄漏（#68933）—— 配置了 MCP 的开发者会意外遭受内存冲击。
- 需要更好的 stdio 错误诊断（#47635）

### 5. 自定义 API 与第三方模型兼容性
- Claude Code 在 `effortLevel: high` 时向自定义模型发送 `thinking: {type: adaptive}`，导致非 Anthropic 网关 400 或挂起（#68551）。这对使用 LiteLLM 等网关接入第三方模型的开发者造成阻塞。

---

*日报基于 GitHub 上 anthropics/claude-code 仓库截至 2026-06-17 的数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 **2026-06-17 OpenAI Codex 社区动态日报**。

---

# OpenAI Codex 社区动态日报 | 2026-06-17

### 📰 今日速览
社区今日焦点集中在**严重的账户恢复死锁**（#25749）以及 **macOS / Windows 双平台的稳定性灾难**上。多起涉及 `Computer Use` 插件在 Windows 上无法使用、以及因资源耗尽导致应用崩溃的 Bug 正在影响大量用户。开发团队在紧急应对问题的同时，也在推进 TUI 插件共享、身份联盟和配置治理等核心基础设施的更新。

---

### 🚀 版本发布
#### `rust-v0.141.0-alpha.3` 和 `rust-v0.141.0-alpha.4`
过去 24 小时内连续发布了两个 Rust CLI 的 Alpha 版本。由于发布说明未提供具体细节，推测为针对近期 `v0.140.0` 系列（如 `image_gen` 回归）的快速迭代修复。

---

### 🔥 社区热点 Issues (Top 10)

1.  [#25749] [BUG] **账号恢复无门：遗留手机号验证死锁**
    - **重要性：** **最高优先级**。用户使用 Google OAuth 可登录 ChatGPT，但因遗留手机号验证无法进入 Codex，且 OpenAI 未提供任何恢复路径。
    - **社区反应：** 46 条评论，30 个 💖。这是目前最严重的使用阻断问题。
    - **链接：** [Issue #25749](https://github.com/openai/codex/issues/25749)

2.  [#25243] [BUG] **macOS Codex 无限重启循环，耗尽文件描述符**
    - **重要性：** **严重系统级问题**。Codex 进程无限重启，导致 macOS 守护进程 `syspolicyd` 文件描述符耗尽，阻塞其他应用的正常启动。
    - **社区反应：** 33 条评论，用户报告整个系统变慢。
    - **链接：** [Issue #25243](https://github.com/openai/codex/issues/25243)

3.  [#27506] [BUG] **Windows 非 ASCII 路径导致启动即崩**
    - **重要性：** **影响亚洲用户**。当 Windows 用户目录（如 `C:\Users\김코덱스`）包含韩文等非 ASCII 字符时，应用更新后直接崩溃，完全无法使用。
    - **社区反应：** 9 条评论，6 个 👍。受影响的用户群体明确。
    - **链接：** [Issue #27506](https://github.com/openai/codex/issues/27506)

4.  [#21128] [BUG] **对话记录静默丢失**
    - **重要性：** **数据可靠性问题**。Codex Desktop 隐藏了“最近 50 条”之外的对话，用户认为这破坏了 Codex 作为“可靠工作记忆”的核心定位。
    - **社区反应：** 27 条评论，17 个 👍。社区对此设计理念普遍表示不满。
    - **链接：** [Issue #21128](https://github.com/openai/codex/issues/21128)

5.  [#20567] [BUG] **Windows 版本每分钟触发 1000+ Git 命令**
    - **重要性：** **极端资源浪费**。后台无节制地轮询 Git 状态，导致进程数暴增，严重影响主机性能。
    - **社区反应：** 9 条评论。用户担心 SSD 寿命和 CPU 占用。
    - **链接：** [Issue #20567](https://github.com/openai/codex/issues/20567)

6.  [#27287] [BUG] **Windows Computer Use 完全无法启动**
    - **重要性：** **核心功能阻断**。因 `@oai/sky` 包导出配置缺失，Windows 用户无法使用 `Computer Use` 和 `@computer` 功能。
    - **社区反应：** 9 条评论，9 个 👍。Windows 用户表示这是“必应的一步之遥”式的失望。
    - **链接：** [Issue #27287](https://github.com/openai/codex/issues/27287)

7.  [#27570] [BUG] **Review 功能在嵌套仓库中引发 Git 进程海啸**
    - **重要性：** **性能灾难**。`review-summary` 在检测嵌套 Git 子模块时，会无限制地派生 `git hash-object` 进程。
    - **社区反应：** 4 条评论。该 Bug 与 #25243 类似，都是资源管理失控的表现。
    - **链接：** [Issue #27570](https://github.com/openai/codex/issues/27570)

8.  [#25865] [BUG] **粘贴转义 JSON 使应用冻结**
    - **重要性：** **影响调试体验**。当开发者粘贴包含大量转义反斜杠的 JSON 堆栈时，应用立即失去响应。
    - **社区反应：** 9 条评论，7 个 👍。对 Debug 工作流影响较大。
    - **链接：** [Issue #25865](https://github.com/openai/codex/issues/25865)

9.  [#28121] [BUG] **更新后 Computer Use 再次损坏**
    - **重要性：** **回归问题**。在 #27287 修复后，新一轮更新再次破坏了 `@oai/sky` 的 Windows 子路径导出，说明缺乏有效的回归测试。
    - **社区反应：** 6 条评论。用户开始对“Computer Use 修好了吗”失去耐心。
    - **链接：** [Issue #28121](https://github.com/openai/codex/issues/28121)

10. [#28422] [BUG] **CLI v0.140.0 image_gen 图片保存回归**
    - **重要性：** **功能失效**。生成的图片在状态为 `generating` 时不会被保存到本地，导致图片直接丢失。
    - **社区反应：** 3 条评论。直接促使了 `v0.141.0-alpha` 的快速发布。
    - **链接：** [Issue #28422](https://github.com/openai/codex/issues/28422)

---

### 🛠 重要 PR 进展 (Top 10)

1.  **#27713** [原型] **CLI 身份联盟 (Workload Identity Federation)**
    - **内容：** 为 CLI 探索无密钥认证方案，旨在替代传统的静态 API Key，提升安全性。
    - **链接：** [PR #27713](https://github.com/openai/codex/pull/27713)

2.  **#26703/704/705** [系列] **TUI 插件共享功能落地**
    - **内容：** 三连 PR 实现了远程插件目录的渲染、用户测试流程覆盖和 UI 细节优化。标志着 TUI 插件生态正式进入市场准备阶段。
    - **链接：** [PR #26703](https://github.com/openai/codex/pull/26703)

3.  **#28409** [特性] **严格模式配置强制执行**
    - **内容：** 扩展 `requirements.toml`，允许管理员对 `sqlite_home`、`log_dir` 等关键配置进行精确强制，不匹配时发出启动警告。
    - **链接：** [PR #28409](https://github.com/openai/codex/pull/28409)

4.  **#27946** [重构] **工具接口适配 Responses Lite**
    - **内容：** 统一工具调用方式（使用 `additional_tools`），为后续解决 `image_gen` 等命名空间冲突（#28464）铺平道路。
    - **链接：** [PR #27946](https://github.com/openai/codex/pull/27946)

5.  **#28647** [修复] **MCP OAuth 刷新竞争条件**
    - **内容：** 解决多个客户端实例共享持久化 MCP OAuth Token 时，刷新令牌并发导致提供商标记失效的问题。
    - **链接：** [PR #28647](https://github.com/openai/codex/pull/28647)

6.  **#28494** [特性] **共享会话 Token 预算限制**
    - **内容：** 引入 Token 预算墙，根线程与所有子线程共享一个预算池。防止单次 `goal` 任务无限制消耗 Token。
    - **链接：** [PR #28494](https://github.com/openai/codex/pull/28494)

7.  **#28034** [实验] **本地凭证代理**
    - **内容：** 将系统凭证（如 API Key）从子进程环境变量中移除，转由本地代理托管，防止命令执行时被恶意窃取。
    - **链接：** [PR #28034](https://github.com/openai/codex/pull/28034)

8.  **#28638** [清理] **核心数据结构去冗余**
    - **内容：** 清理 `TurnContext` 中的死亡字段和重复投影，降低代码复杂度，消除潜在的“分裂”状态 Bug。
    - **链接：** [PR #28638](https://github.com/openai/codex/pull/28638)

9.  **#28219/#28189** [重构] **工具命名空间标准化**
    - **内容：** 对默认工具和客户端工具搜索标识进行清洗，明确所有权，彻底解决因 `image_gen` 注册冲突导致的功能异常。
    - **链接：** [PR #28219](https://github.com/openai/codex/pull/28219)

10. **#28598** [优化] **Bazel 构建超时优化**
    - **内容：** 调整 Rust 测试目标的默认大小，防止冗长的超时警告掩盖真正的测试失败，显著改善 CI 体验。
    - **链接：** [PR #28598](https://github.com/openai/codex/pull/28598)

---

### 📈 功能需求趋势

*   **会话与数据主权：** 用户强烈要求更合理的历史记录管理。不再满足于 UI 层面的隐藏（#21128），而是希望拥有对长对话的**绝对恢复能力**（#25215, #26012）和**完整的上下文控制**（#18052）。
*   **Windows 平台次等公民体验终结：** 从路径编码崩溃（#27506）到 Git 进程风暴（#20567），再到 Computer Use 反复失效（#27287, #28121），**Windows 用户正在要求与 macOS 同等质量的体验**。
*   **插件生态的稳定性压倒一切：** `Computer Use` 成为问题高发区。用户的核心诉求已从“功能有没有”转变为“**更新后还能不能正常用**”。缺乏回归测试是目前最大的信任危机。
*   **精细化工作流控制：** 用户期望更强的可配置性，例如默认项目路径（#19913）、TUI 中的动态目录切换（#12464），希望 AI 工具能更好地适配开发者既有的工作流，而非强行改变。
*   **远程开发支持：** SSH 远程工作区（#21509）的呼声虽然不高，但代表了企业级用户的刚需，Codex Desktop 与远程环境的无缝集成将是未来竞争的壁垒。

---

### 💬 开发者关注点

1.  **账户系统的“单点故障”风险：** 一旦遗留手机号回环验证无法通过，**用户即被完全锁定**，这直接扼杀了产品的可用性，是当前最核心的痛点。
2.  **“修好一个，弄坏三个”的回归焦虑：** 无论是 `Computer Use` 还是 `image_gen`，频繁的回归让开发者对更新产生了抵触心理，质疑测试流程的有效性。
3.  **资源管理失控：** macOS 的文件描述符耗尽、Windows 的 Git 进程海啸、硬盘被莫名其妙的大文件占满（曾报告 62GB 的缓存）。开发者的共识是：**AI 工具不应成为开发环境的性能杀手**。
4.  **数据不可靠的焦虑：** 长对话中命令执行详情丢失、归档后无法删除、恢复后线程异常（#26012, #28162）。开发者需要确信 Codex 不会成为“不可靠的副驾”，数据的确定性是信任的基石。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是为您生成的2026年6月17日 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 — 2026-06-17

## ☀️ 今日速览
今日仓库动态集中在**安全加固**与**稳定性修复**上。多项聚焦于防护 `workflow_run` 投毒攻击、强制路径阻断以及修复 MCP OAuth 令牌安全的 PR 正在进行或已合并。值得关注的是，`v0.48.0` 的**夜间构建流程失败**，可能影响开发分支的可用性。此外，一个修复模型**思维链泄露**到对话历史记录的 PR 获得了关注。

## 🚀 版本发布
*(今日无新版本发布)*

## 🔥 社区热点 Issues
1.  **[#21409] 通用代理（Generalist agent）挂起**
    *   **重要性**：核心功能严重缺陷，用户反馈频繁（👍 8，评论 7）。当 `gemini-cli` 调用通用代理时，进程会无限期挂起，用户等待长达一小时，严重阻塞工作流。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/21409

2.  **[#22323] 子代理在达到最大轮次后错误报告“成功”**
    *   **重要性**：系统状态报告不准确，直接误导用户。子代理因 `MAX_TURNS` 被中断，却返回 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了任务未完成的真实情况。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/22323

3.  **[#24353] 健壮的组件级评估（EPIC）**
    *   **重要性**：跟踪项目长期质量的关键工程。该EPIC旨在建立更细致的组件级评估体系，以替代或补充现有的端到端行为评估。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/24353

4.  **[#22745] 评估 AST 感知文件读取、搜索和映射的影响（EPIC）**
    *   **重要性**：探索性功能，可能大幅提升代理的代码理解精确度（如精确定位方法边界），减少不必要的Token消耗和交互轮次。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/22745

5.  **[#25166] Shell 命令执行完成后卡住，显示“等待输入”**
    *   **重要性**：日常高频使用痛点（👍 3，评论 4）。在简单的 Shell 命令执行完毕后，终端状态未正确更新，导致用户必须手动干预。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/25166

6.  **[#26525] 自动内存（Auto Memory）的日志存在安全风险**
    *   **重要性**：安全与隐私问题。自动内存功能在将日志发送给模型提取前未进行脱敏处理，可能导致密钥信息泄露。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/26525

7.  **[#26522] 自动内存（Auto Memory）对低价值会话无限重试**
    *   **重要性**：资源浪费与逻辑缺陷。当提取代理因“低信号”决定不读取某段会话时，系统会反复对其进行重试，形成无效循环。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/26522

8.  **[#22672] 代理应阻止/劝阻破坏性行为**
    *   **重要性**：用户体验与安全性。社区关注模型在 `git`、数据库操作中频繁使用 `--force` 或 `git reset` 等危险命令，期待其能主动选择更安全的替代方案。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/22672

9.  **[#21983] 浏览器代理在 Wayland 环境下失败**
    *   **重要性**：特定环境下的兼容性问题。在 Wayland 显示服务器上运行浏览器代理时功能异常，限制了部分 Linux 用户的使用。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/21983

10. **[#22186] “get-shit-done”输出钩子导致崩溃**
    *   **重要性**：功能性崩溃。一个核心功能在输出摘要时引发程序崩溃，严重影响用户对该功能的使用。
    *   **链接**: https://github.com/google-gemini/gemini-cli/issues/22186

## 📈 重要 PR 进展
1.  **[#27753] CI: 验证 `workflow_run` 来源，防止分支投毒**
    *   **状态**: 开放中 | **重要性**: 高 | 关键的安全修复，防止Fork的PR通过`workflow_run`攻击链窃取仓库机密。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27753

2.  **[#27971] 修复(core): 剥离净化历史记录中的思维链，解决思想泄露**
    *   **状态**: 开放中 | **重要性**: 高 | 修复一个有趣的Bug：模型的内部推理过程会泄漏到对话历史中，导致后续交互中的思维混乱或无限循环。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27971

3.  **[#27643] 修复(build): 解决并行工作区编译的竞争条件**
    *   **状态**: 已关闭 | **重要性**: 中 | 修复了并行构建时可能出现的“竞态条件”，通过将构建过程拆分为顺序阶段，提升构建稳定性。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27643

4.  **[#27771] 修复 MCP 标头对非 ASCII 值的编码问题**
    *   **状态**: 开放中 | **重要性**: 中 | 解决MCP HTTP传输中，配置头包含Unicode字符（如 `mąka`）时导致握手失败的问题。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27771

5.  **[#27963] 文档: 记录 `read_file` 工具的 20MB 文件大小限制**
    *   **状态**: 开放中 | **重要性**: 低 | 完善文档，避免用户遇到“文件大小超过20MB限制”错误时感到困惑。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27763

6.  **[#27966] 修复(安全): 强制大小写不敏感的敏感路径阻断列表和 VSCode HITL**
    *   **状态**: 开放中 | **重要性**: 高 | 加强安全防护，通过大小写不敏感匹配等方式，更严格地阻止对 `.git`、`.env` 等敏感路径的访问。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27966

7.  **[#27664] 修复(core): 原子性地写入 MCP OAuth 令牌**
    *   **状态**: 开放中 | **重要性**: 高 | 通过临时文件和原子重写操作来写入OAuth令牌文件，防止写入过程中出现问题导致令牌损坏。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27664

8.  **[#27889] 修复(core): 使用存储的客户端ID刷新 MCP OAuth**
    *   **状态**: 开放中 | **重要性**: 中 | 修复自动发现的MCP Server在刷新OAuth令牌时，无法使用已存储的`clientId`的问题，提升认证流程的健壮性。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27889

9.  **[#27964] 修复(mcp): 限定资源解析范围，防止跨服务器URI混淆**
    *   **状态**: 开放中 | **重要性**: 中 | 安全修复，当多个MCP服务器暴露相同的URI时，防止恶意服务器“劫持”信任服务器的资源请求。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27964

10. **[#27970] chore(deps): 将 `hono` 从 4.12.18 升级到 4.12.25**
    *   **状态**: 开放中 | **重要性**: 中 | 定期依赖更新，其中包含针对特定漏洞的安全修复。
    *   **链接**: https://github.com/google-gemini/gemini-cli/pull/27970

## 💡 功能需求趋势
从近期Issue中提炼出社区最关注的几个方向：
*   ** AST 感知工具化**: 社区强烈希望引入基于抽象语法树（AST）的工具来替代纯文本操作，以提高代码读取、搜索和映射的精度与效率（如 #22745, #22747）。
*   ** 代理行为的智能化与安全性**: 用户期望代理能更智能地选择操作（例如使用 `--soft` 而非 `--force`），并具备更强的安全意识，避免执行破坏性命令或泄露敏感信息（如 #22672, #21432）。
*   ** 内存系统的稳定性**: 随着“自动内存”功能的引入，社区对其可靠性、安全性和资源利用率提出了更高要求（如 #26522, #26525, #26516）。
*   ** 终端体验与性能**: 高阶用户关注终端重绘性能、外部编辑器集成后的界面恢复、以及命令执行状态的准确反馈（如 #21924, #24935, #25166）。
*   ** 模型与后端支持完善**: 社区关注对不同后端（如 Vertex AI、GDC）的兼容性以及模型名称解析的准确性（如 #27760, #27956）。

## 🧑‍💻 开发者关注点
*   ** 代理挂起与状态误报**: 代理在执行任务后无故挂起（#21409）或错误报告任务状态（#22323）是开发者最深恶痛绝的问题，严重动摇了用户对自动化工具的信任。
*   ** 工具使用不合理**: 模型被反馈认为在可以调用MCP工具或自定义技能时，倾向于选择自己编写脚本（#21968, #23571），这种行为增加了代码混乱和潜在的安全风险。
*   ** 破坏性行为缺乏约束**: 开发者指出模型在进行Git或数据库操作时，缺乏对潜在破坏性行为的认知，需要内置更安全的执行策略（#22672）。
*   ** 配置项被忽略**: 用户反映子代理（特别是浏览器代理）存在忽略用户配置（如 `maxTurns`）的问题，导致用户体验割裂（#22267）。
*   ** 终端兼容性**: 特定环境下的问题依然存在，如在 Wayland 下的浏览器代理失败（#21983）、或在 tmux 下的主题错误检测（#27572）。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据，生成了 2026-06-17 的 GitHub Copilot CLI 社区动态日报。

---

# GitHub Copilot CLI 社区动态日报 | 2026-06-17

> 数据来源: [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

## 1. 今日速览

今日社区动态主要由新版本 `v1.0.64-0` 的发布驱动，该版本引入了 `/diagnose` 诊断命令和 `/mcp` 注册表安装等关键新功能。在社区讨论方面，**企业级自定义模型支持**（Issue #3730）和 **子代理模型不一致** (Issue #3824) 成为最受关注的功能请求与Bug。此外，**Windows ARM64 平台下的稳定性问题**（Issue #3687）仍在讨论中，但尚未有明确的修复方案。

## 2. 版本发布

### v1.0.64-0

在过去24小时内，发布了新版本 `v1.0.64-0`。该版本主要带来了以下更新：
- **新增 `/diagnose` 命令**：用于分析和收集会话日志，便于排查复杂问题。
- **新增 `/mcp` 注册表安装**：支持从注册表中浏览和安装 MCP 服务器，简化集成流程。
- **安全审查公开**：`/security-review` 命令已对所有用户开放，无需再使用 `--experimental` 标志。
- **插件 MCP 发现**：新增自动发现由已安装插件提供的 MCP 服务器的能力。
- **MCP 工具 CSV 输出**：为 MCP 工具增加了 CSV 格式的输出支持。

## 3. 社区热点 Issues

以下为过去24小时内更新或创建的，最值得关注的10个 Issue：

1.  **#3687: [area:sessions, area:platform-windows] copilot.exe 在负载下致命崩溃 (BEX64 / 0xc0000409)**
    - **重要性**: 严重的稳定性问题，影响 Windows ARM64 用户。在高负载或内存压力下，`copilot.exe` 进程无法正常关闭，而是直接崩溃退出，严重影响用户体验。
    - **社区反应**: 该问题自 6月5日创建以来，虽只有1个赞同，但仍在活跃讨论中，表明受影响的用户对稳定性的迫切需求。
    - **链接**: [Issue #3687](https://github.com/github/copilot-cli/issues/3687)

2.  **#1168: [area:permissions] Copilot CLI 在单次请求中频繁提示授权（“授权疲劳”）**
    - **重要性**: 直接影响用户核心交互体验的“授权疲劳”问题。一个简单的请求可能导致超过一打的授权提示，极大降低了开发效率和工作流的连贯性。
    - **社区反应**: 拥有2个赞同，用户反馈积极，社区对此设计有强烈改进诉求。
    - **链接**: [Issue #1168](https://github.com/github/copilot-cli/issues/1168)

3.  **#3828: [area:non-interactive, area:tools] ContentExclusionFilter.isExcluded 崩溃**
    - **重要性**: 这是一个新发现的 Bug，直接导致 `rg`（ripgrep）工具因 `TypeError` 而崩溃。这会影响所有依赖该工具的代码搜索和上下文收集功能，是一个紧急的高影响问题。
    - **社区反应**: 刚刚创建，尚无太多讨论，但需要开发团队迅速介入。
    - **链接**: [Issue #3828](https://github.com/github/copilot-cli/issues/3828)

4.  **#3812: [area:agents, area:mcp] 子代理无法再访问 MCP 工具**
    - **重要性**: 这是一个功能回归 Bug。子代理无法使用 MCP 工具，这会严重破坏依赖子代理和 MCP 服务器进行复杂任务编排的工作流，对高级用户影响巨大。
    - **社区反应**: 用户已定位到问题可能和 MCP 工具的延迟加载有关，为开发者提供了有价值的排查线索。
    - **链接**: [Issue #3812](https://github.com/github/copilot-cli/issues/3812)

5.  **#3821: [area:sessions, area:installation] `/update` 后会话恢复冲突**
    - **重要性**: 这是一个与开发者体验相悖的 Bug。从恢复的会话中执行更新后，命令行会因新旧会话参数冲突而失败，无法继续工作，中断了用户的工作流。
    - **社区反应**: 用户提供了清晰的复现步骤，对开发者定位问题很有帮助。
    - **链接**: [Issue #3821](https://github.com/github/copilot-cli/issues/3821)

6.  **#3826: [area:input-keyboard] “Operation cancelled by user” 被重新注入为用户消息**
    - **重要性**: 这是一个比较奇怪的 Bug，影响了用户取消操作后的交互逻辑。AI 模型会将“操作已取消”这一提示误认为是新的用户指令而进行响应，可能导致意料之外的后续行为。
    - **社区反应**: 用户报告，问题明确，可能需要对事件处理逻辑进行修复。
    - **链接**: [Issue #3826](https://github.com/github/copilot-cli/issues/3826)

7.  **#3824: [area:agents, area:models] 子代理可能运行与会话配置不同的模型**
    - **重要性**: 这是一个严重的配置逻辑问题。即使用户为主会话配置了特定的模型，子代理也可能会使用不同的模型或实验性替代模型，且此行为对用户不可见。这会导致输出结果与用户预期和配置不符。
    - **社区反应**: 报告非常详细，指出了两种产生此问题的机制，受到高度关注。
    - **链接**: [Issue #3824](https://github.com/github/copilot-cli/issues/3824)

8.  **#3823: [area:models] 推理开销 “xhigh” 在不受支持的模型上被静默降级为 “medium”**
    - **重要性**: 这是一个配置层面的潜在陷阱。用户配置的 `xhigh` 推理开销级别，若当前模型不支持，会被静默降级至 `medium`，而不是可用的最高级别 `max`。用户可能并不知道实际使用的推理资源低于预期。
    - **社区反应**: 报告清晰详细，指出了静默降级导致的用户预期偏差问题。
    - **链接**: [Issue #3823](https://github.com/github/copilot-cli/issues/3823)

9.  **#3825: [area:permissions] `--allow-all` 读取权限泄露导致 TUI 无输入框**
    - **重要性**: 严重影响非交互式和恢复会话的可用性。`--allow-all` 参数下的权限处理逻辑存在缺陷，导致 TUI 界面卡死，用户无法进行任何输入，完全阻塞了操作。
    - **社区反应**: 报告清晰，是一个功能完整性方面的高影响Bug。
    - **链接**: [Issue #3825](https://github.com/github/copilot-cli/issues/3825)

10. **#3730: [area:enterprise, area:models] 支持企业管理的自定义模型**
    - **重要性**: 功能需求，代表了企业用户的重大诉求。企业希望能在 Copilot CLI 中使用由管理员在后台配置的自定义 AI 模型，与其他 Copilot 客户端保持一致。
    - **社区反应**: 拥有4个赞同，是过去24小时内赞同数最高的 Issue，充分表明了企业级用户对此功能的高度期待。
    - **链接**: [Issue #3730](https://github.com/github/copilot-cli/issues/3730)

## 4. 重要 PR 进展

过去24小时内没有合并或处于更新中的 Pull Request。这表明开发团队当前可能正专注于处理 `v1.0.64-0` 版本发布后的 Bug 修复和稳定性工作。上述 `Releases` 中的变更包含了对新功能的代码贡献。

## 5. 功能需求趋势

从近期创建和更新的 Issue 中，我们可以观察到社区对于 Copilot CLI 功能发展的几个明确需求方向：

1.  **企业级特性与灵活性**：
    -   **企业自定义模型支持 (Issue #3730)**:
        社区，特别是企业用户，强烈要求支持由管理员配置的自定义 AI 模型，这表明 Copilot CLI 正在被更广泛地引入企业开发环境。
    -   **子代理模型一致性 (Issue #3824)**: 要求子代理的行为与主代理完全一致，包括模型选择，体现了对复杂工作流结果可预测性的高要求。

2.  **MCP 生态的深度整合与精细化控制**：
    -   **MCP 注册表安装 (Release v1.0.64-0)**: 官方已开始推动 MCP 服务器的“应用商店”式安装，社区对此表示欢迎。
    -   **MCP 工具在子代理中的可用性 (Issue #3812)**: 子代理不能访问 MCP 工具被视作一个回归 Bug，说明社区已经依赖这种跨会话的工具调用能力。
    -   **改进 MCP 类型识别 (Issue #2790)**: 用户要求 CLI 能更准确地识别和连接不同类型的 MCP 服务器（如 HTTP 与 SSE）。

3.  **插件与仓储管理**：
    -   **批量更新插件 (Issue #3830)**: 当安装多个插件后，逐一更新的方式变得繁琐，用户期望一个“一键更新所有”的命令。
    -   **跨仓库插件配置 (Issue #3822)**: 对于大型单仓或多仓库项目，用户希望 `skillDirectories` 设置能作用于仓库级别，而不是全局或项目根目录。

4.  **会话与工作流管理**：
    -   **会话存档恢复 (Issue #3518)**: 用户需要一个明确的“取消归档”功能来恢复被误删的长期会话，这表明会话作为“工作区”正在被越来越深度地使用。

## 6. 开发者关注点

-   **稳定性问题**:
    -   **Windows ARM64 崩溃 (Issue #3687)** 和 **ContentExclusionFilter 崩溃 (Issue #3828)** 是当前最严重的高优先级 bug，直接影响了部分用户和核心工具链的可用性。
-   **交互体验问题**:
    -   **授权疲劳 (Issue #1168)** 和 **UI 卡死 (Issue #3825)** 是用户体验的核心痛点，严重阻碍了工作流程。**取消操作被误解 (Issue #3826)** 则暴露了复杂 AI 交互中逻辑状态管理的不足。
-   **配置与预期不符**:
    -   **子代理模型不一致 (Issue #3824)** 和 **推理开销静默降级 (Issue #3823)** 是“沉默的错误”，用户不知道系统配置并未按预期工作，这会导致对结果的误解和信任度的降低。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，身为专注于 AI 开发工具的技术分析师，我将根据您提供的 GitHub 数据，为您呈现 2026-06-17 的 Kimi Code CLI 社区动态日报。

---

## Kimi Code CLI 社区动态日报 | 2026-06-17

### 今日速览

尽管过去24小时无新版本发布，但社区对Kimi Code CLI的关注度依然很高。今日焦点集中在两个关键 bug 上：一是自动发现已删除 MCP 服务器导致持续 400 错误，二是新用户安装后缺乏登录引导导致无法使用。此外，一个关于默认最大步数设置的旧 Issue 被重新讨论，反映出用户对更长任务处理周期的需求。

### 版本发布
无

### 社区热点 Issues

1.  **[bug] Kimi Code CLI auto-discovers MCP server after user deleted it, causing unfixable 400 errors (#2457)**
    -   **重要性**: 🚨 **严重 Bug**。这是一个关于 MCP (Model Context Protocol) 服务器管理的问题。当用户删除 MCP 服务器后，CLI 仍会自动发现并尝试与之通信，导致持续出现 `400` 错误且用户无法自行修复。这触及了核心的配置管理和状态同步问题，严重影响用户体验。
    -   **社区反应**: 刚刚提交，暂无回复，但问题描述清晰，预计会很快获得开发者关注。
    -   **链接**: [Issue #2457](https://github.com/MoonshotAI/kimi-cli/issues/2457)

2.  **[bug] Fresh install reports "LLM not set" with no guidance to run login (#2456)**
    -   **重要性**: 🚨 **流程缺陷**。该问题指出了新用户首次使用时的关键痛点：通过 Homebrew 安装后，执行命令直接报错 `LLM not set`，却没有提示用户需要先执行 `kimi login` 进行认证。这增加了新用户的上手门槛和困惑感，是优化新手体验（First-Run Experience）的核心问题。
    -   **社区反应**: 刚发布，暂无评论，但问题清晰地暴露了产品引导环节的缺失。
    -   **链接**: [Issue #2456](https://github.com/MoonshotAI/kimi-cli/issues/2456)

3.  **[enhancement] More Steps per turn By Default (#1327)**
    -   **重要性**: ⭐ **功能增强热门**。用户抱怨默认的 `100` 步经常被触发，而上下文使用率仅 34.5%，导致无效中断。此需求代表了相当一部分处理复杂任务用户群体的呼声，希望提高默认步数以提升任务完成率。
    -   **社区反应**: 评论数 3，有讨论，用户倾向于通过修改配置来解决，但认为不合理的高上限应是默认值。
    -   **链接**: [Issue #1327](https://github.com/MoonshotAI/kimi-cli/issues/1327)

4.  **Feature Request: Option to hide thinking content while using thinking models (#1632)**
    -   **重要性**: ⭐ **常见需求**。该 Feature Request 希望添加一个选项来隐藏思考模型（如 kimi-k2-thinking-turbo）的实时推理过程。这在提高推理质量的同时，满足了部分用户对终端输出简洁性、减少干扰或提升隐私保护的需求。该问题已关闭，意味着功能可能已在路线图或待办中。
    -   **社区反应**: 获得 3 个 👍，表示有一定用户基础支持。
    -   **链接**: [Issue #1632](https://github.com/MoonshotAI/kimi-cli/issues/1632)

### 重要 PR 进展

1.  **fix: always stringify tool message content in Chat Completions provider (#1771)**
    -   **重要性**: 🛠️ **核心兼容性修复**。修复了与 OpenAI Chat Completions API 的兼容性问题。当 tool 调用返回多个 `ContentPart` 时，CLI 未能将 `content` 序列化为字符串，导致 API 返回 `400` 错误。此修复对于使用 Tool-Use/Function Calling 功能的用户至关重要，解决了功能执行中的一个潜在中断点。
    -   **链接**: [PR #1771](https://github.com/MoonshotAI/kimi-cli/pull/1771)

### 功能需求趋势

从当前数据看，社区最关注的功能方向包括：

1.  **配置灵活性与默认值优化**：用户不再满足于“能用”，而是希望默认配置（如最大步数）能贴合更复杂、真实的开发场景，而不是频繁触及限制导致任务中断。
2.  **用户体验与易用性**：从安装引导到功能使用（如隐藏思考过程），社区对流畅、直观的用户体验有很高要求。糟糕的首次体验和困惑的错误提示会严重打击用户信心。
3.  **集成与服务管理稳定性**：对 MCP（或类似插件/服务）的管理越来越受关注。自动发现机制应更智能，允许用户完全控制服务生命周期，以避免因残留配置导致的持久性错误。

### 开发者关注点

-   **新用户上手引导缺失**：`LLM not set` 错误提示不够友好，未提供 `kimi login` 等下一步操作指引，新手入门遭遇硬门槛。
-   **MCP 服务管理混乱**：用户无法可靠地删除或禁用自动发现的 MCP 服务器，导致服务冲突和持续报错，缺乏手动管理控制权。
-   **API 兼容性问题**：在 tool/function calling 场景下，仍有与标准 OpenAI API 不兼容的细节，表明兼容性测试和边界情况处理有待加强。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-06-17）

## 今日速览
昨日社区 Bug 报告与修复高度活跃：MiniMax M3 模型兼容性问题集中爆发（至少 3 条独立报告），但官方已迅速合入修复 PR；新发现空 Git 仓库无限循环、每日日期破坏 Prompt Cache 等 session 层面的深层 Bug 引发讨论。功能请求方面，原生会话目标 `/goal` 以 88 👍 继续领跑，性能优化和 Windows 支持仍是开发者投入重点。

## 版本发布
无新版本（过去 24 小时无 Release）。

---

## 社区热点 Issues

### 1. [FEATURE] 原生会话目标 /goal （#27167）
- **链接**：anomalco/opencode Issue #27167
- **热度**：👍 88 · 💬 50
- **摘要**：提议增加持久化的 session goal/lifecycle，将 `/goal` 作为内置 slash 命令，避免每次通过自然语言描述任务目标。社区支持度极高，被视为提升工作流效率的关键功能。

### 2. [BUG] OpenCode 接收指令后随机挂起 （#2940）
- **链接**：anomalco/opencode Issue #2940
- **热度**：👍 18 · 💬 39（更新于 2026-06-17）
- **摘要**：Laravel 项目中模型无关的随机 hang，`/compact` 不一定奏效，常需 `Ctrl+C` 退出。长期存在的稳定性痛点，至今未彻底解决。

### 3. [BUG] 复制文本功能失效 （#7048）
- **链接**：anomalco/opencode Issue #7048
- **热度**：👍 13 · 💬 23（更新于 2026-06-17）
- **摘要**：Ubuntu Desktop + GhostTTY 环境中右键复制仅显示“Copied to clipboard”却未真正写入剪贴板。影响日常操作，用户期待修复。

### 4. [BUG] OpenCode 无法读取图片 （#25832）
- **链接**：anomalco/opencode Issue #25832
- **热度**：👍 4 · 💬 13（更新于 2026-06-17）
- **摘要**：自 2026-04-29 起图像理解功能回归，读取 .png/.jpg 时返回 Bad Request。高优先级 regression，阻碍基于视觉的 HTML 修改等场景。

### 5. [BUG] OpenCode 严重 CPU 占用 （#21470）
- **链接**：anomalco/opencode Issue #21470
- **热度**：👍 10 · 💬 11（更新于 2026-06-16）
- **摘要**：用户提供具体数据：300K token 花费 $8.30，但 OpenCode 自身占用超 1.5 小时 CPU。与模型 API 等待不同，本地计算成为瓶颈。

### 6. [BUG] Skills 在 TUI 自动补全中不显示 （#22129）
- **链接**：anomalco/opencode Issue #22129
- **热度**：👍 12 · 💬 10（更新于 2026-06-17）
- **摘要**：Web 端能正常显示 Skill 徽标，TUI 的 autocomplete 却完全缺失。已定位至 `autocomplete.tsx:363`，社区关注度较高。

### 7. [FEATURE] 实现 /loop 命令 （#18001）
- **链接**：anomalco/opencode Issue #18001
- **热度**：👍 27 · 💬 9（更新于 2026-06-16）
- **摘要**：希望支持自动化迭代任务执行，避免重复用自然语言描述循环逻辑。适合定时任务和批量处理，评论区已有初步设计讨论。

### 8. [BUG] IDE Context Awareness 不生效 （#22235）
- **链接**：anomalco/opencode Issue #22235
- **热度**：👍 4 · 💬 7（更新于 2026-06-17）
- **摘要**：VSCode 中“Context Awareness”功能看似未自动附加选中内容，用户询问是否缺少前置配置。暴露了 IDE 集成文档和默认行为清晰度的不足。

### 9. [BUG] 空 Git 仓库陷入无限澄清/压缩循环 （#32615）
- **链接**：anomalco/opencode Issue #32615
- **热度**：💬 3（更新于 2026-06-16，新提交）
- **摘要**：在仅包含 `.git/` 的空目录中，OpenCode 会反复进行 clarification/compaction 循环，消耗 tokens 而无进度。既是正确性 Bug 也是成本控制 Bug，值得关注。

### 10. [BUG] MiniMax M3 拒绝携带工具历史的会话 （#32608 / #32614 / #32611）
- **链接**：anomalco/opencode Issue #32608
- **热度**：共 💬 6（多例报告，更新于 2026-06-16/17）
- **摘要**：切换已有工具调用历史的 session 到 MiniMax M3 时，返回 `400 tool call result does not follow tool call`。新 session 则正常，表明历史兼容性问题。社区当天即提交了修复 PR #32609。

---

## 重要 PR 进展

### 1. fix(shell): PowerShell UTF-8 命令包装器 （#31985）
- **链接**：anomalco/opencode PR #31985
- **状态**：Open · 更新 2026-06-17
- **要点**：在 Windows 上为 PowerShell 命令添加 UTF-8 包装，一次性关闭 5 个编码相关 issue。解决中文等非 ASCII 输出乱码的老大难问题。

### 2. fix(provider): 对孤儿 MiniMax 工具结果进行桩处理 （#32609）
- **链接**：anomalco/opencode PR #32609
- **状态**：Open · 更新 2026-06-17
- **要点**：直接修复 #32608，当 MiniMax 遇到历史中的 tool result 时以 stub 填充使其通过校验。社区响应最快的模型兼容修复。

### 3. fix(desktop): 跳过 $HOME 和根目录文件监控 （#32610）
- **链接**：anomalco/opencode PR #32610
- **状态**：Closed · 更新 2026-06-17
- **要点**：Desktop 版因监控整个 home 导致 inotify 超时和 CPU 飙升。PR 跳过宽泛根目录，清理持久化项目列表，并增加 Flatpak 排查指南。

### 4. fix(opencode): 净化 OpenAI MCP 工具 Schema （#32489）
- **链接**：anomalco/opencode PR #32489
- **状态**：Closed · 更新 2026-06-17
- **要点**：某些 MCP 服务器的 JSON Schema 中包含 OpenAI 不支持的字段（如 `$schema`），该 PR 在发送前做清理。提升 MCP 生态兼容性。

### 5. fix(session): 模型切换时保留 reasoning 部分类型 （#32604）
- **链接**：anomalco/opencode PR #32604
- **状态**：Open · 更新 2026-06-17
- **要点**：切换模型导致前缀缓存大规模失效、延长延迟。PR 保留 reasoning 部分类型，减少不必要的重新处理。

### 6. fix(codex): 从 ChatGPT 账户模型列表中排除 `-pro` 模型 （#32612）
- **链接**：anomalco/opencode PR #32612
- **状态**：Open · 更新 2026-06-16
- **要点**：ChatGPT OAuth 账户下 `gpt-5.5-pro` 虽可选中但请求必失败，PR 将其过滤掉，改善模型选择体验。

### 7. fix(opencode): OAuth 路径将系统上下文作为结构化消息发送 （#32592）
- **链接**：anomalco/opencode PR #32592
- **状态**：Closed · 更新 2026-06-16
- **要点**：修复 OAuth/Codex 请求路径与非 OAuth 路径之间系统上下文格式不一致的问题，消除重上下文场景下的潜在兼容性 Bug。

### 8. feat(opencode): 局域网 (LAN) 提供商自动发现 （#27554）
- **链接**：anomalco/opencode PR #27554
- **状态**：Open · 更新 2026-06-16
- **要点**：组合 mDNS、SSDP 等方式自动发现局域网内 OpenAI-compatible 模型服务器，并在 `/connect` 中展示。对本地/私有部署场景意义重大。

### 9. fix(desktop): 所有 HTTP 连接使用服务端文件选择器 （#31848）
- **链接**：anomalco/opencode PR #31848
- **状态**：Open · 更新 2026-06-17
- **要点**：修复远程连接时 `directoryPickerKind` 判断错误，强制使用服务端文件选择器，避免本机原生选择器在非 local 连接下出错。

### 10. fix(tui): 长会话中旧消息消失 （#26861）
- **链接**：anomalco/opencode PR #26861
- **状态**：Open · 更新 2026-06-16
- **要点**：实现懒加载滚动，当用户滚动到顶部 5px 内时加载更早的 50 条消息。解决 TUI 窗口长时间使用后历史消息不可见的问题。

---

## 功能需求趋势
从近期 Issue 与 PR 可以提炼出五大关注方向：

1. **持久化会话机制**：以 `/goal`、`/loop` 和可配置 fallback 模型链为代表，社区希望减少重复描述目标的负担，实现更自动化的任务编排。
2. **插件与 Skill 系统增强**：递归 Skill 发现、多 Skill 同时启用、中间件式的插件流水线（#5148）呼声增高，且 UI（TUI vs Web）一致性成为痛点。
3. **模型支持扩张与兼容性**：MiniMax M3、Gemini 3.5、DeepSeek 等新模型的适配（及对应的 Regex/thinking budget/工具调用兼容）是当前最密集的开发领域。
4. **性能与成本控制**：CPU 占用过高、空仓库 tokens 浪费、日期缓存失效等问题直接涉及用户开销，推动 session 层与缓存策略的优化。
5. **IDE / 桌面体验**：VSCode Context Awareness、面板布局可切换、文件选择器正确性、Windows 编码等问题体现了用户对“编辑器内体验”的精细化要求。

---

## 开发者关注点
- **可靠性与稳定性**：随机挂起（#2940）、图片读取回归（#25832）、复制失效（#7048）等高频率阻断式 Bug 仍是最直接的使用障碍。
- **新模型兼容成本**：MiniMax M3 的多例报错及紧急修复表明，社区对模型切换时的历史兼容性缺乏预期，需要更稳健的上下文转换层。
- **资源枯竭场景**：空仓库无限循环、大 session CPU 占满、watch 监控过度等问题显示，边界情况下的费用消耗保护不足。
- **平台差异**：Windows PowerShell 编码、macOS 非法指令（#8345）、Ubuntu 剪贴板等问题突出，跨平台一致性仍是持续投入点。
- **功能可见性与一致性**：Skills 在 TUI 不可用、Context Awareness 默认行为不清晰等现象反映，多入口（Desktop/TUI/Web/IDE）之间的功能一致性需加强文档与测试。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 | 2026-06-17

---

## 今日速览

Pi 发布 **v0.79.6** 修复了 HTTP dispatcher 配置覆盖及 DeepSeek V4 思考模式参数兼容性问题，同时 **v0.79.5** 引入 Provider 作用域 API 密钥环境变量覆盖机制。社区中 `openai-codex` 连接可靠性问题（#4945）持续高热（59 条评论），成为过去 24 小时最受关注的议题。PR #5807 *provider-scoped 环境变量* 已合并，进一步增强了多 provider 配置的灵活性。

---

## 版本发布

### v0.79.6
- **Fixed**：修复 HTTP dispatcher 配置未保留调用者自定义 `fetch` 的问题，不再强制安装 undici 全局 fetch。
- **Fixed**：修复在通过 OpenCode Go DeepSeek V4 发送 `thinking-off` 请求时，未正确传入 `thinking: { type: "disabled" }` 兼容参数的问题。

### v0.79.5
- **New Features**：`auth.json` 中 API Key 条目现支持 `env` 覆盖，可为特定 provider（如 Cloudflare、Azure OpenAI、Google Vertex、Amazon Bedrock）单独配置缓存保留、代理等环境变量，无需修改全局 shell 配置。详见 [Auth File](https://github.com/earendil-works/pi/tree/main/docs)。

---

## 社区热点 Issues

挑选了过去 24 小时内更新或讨论最热烈的 10 个议题：

### 1. #4945 [OPEN] openai-codex 连接可靠性问题
- **链接**：https://github.com/earendil-works/pi/issues/4945  
- **概要**：`openai-codex` / `gpt-5.5` 在交互式 TUI 中频繁卡在 “Working…” 状态，无流式输出、无工具调用、无可见错误，仅能通过 Escape 恢复。过去数天反复出现，社区用户反映强烈，评论已达 59 条，是当前最核心的稳定性 Bug。

### 2. #4877 [OPEN] 会话文件夹冲突
- **链接**：https://github.com/earendil-works/pi/issues/4877  
- **概要**：因会话命名方式缺陷，不同路径可能映射到相同会话文件夹（如 `/a/b/c/d` 与 `/a-b/c-d` 冲突）。虽然影响范围有限，但社区认为需要修复以防止未来混淆，获 19 条评论。

### 3. #5696 [CLOSED] TUI 右下角模型名称未在 CTRL+P 后刷新
- **链接**：https://github.com/earendil-works/pi/issues/5696  
- **概要**：用户发现切换模型时右下角显示滞后，按一次无反应、按两次才跳两个模型。虽已关闭，但暴露了 TUI 状态同步的细节问题，获 9 条评论，受到关注。

### 4. #5687 [CLOSED] `pi list` 和 `pi update` 因 MCP 服务器后台运行而无法退出
- **链接**：https://github.com/earendil-works/pi/issues/5687  
- **概要**：当已安装的扩展运行常驻 MCP 服务器时，包管理子命令输出完成后仍挂起，必须 Ctrl-C 退出。社区认为该行为严重影响脚本化使用，获得 8 条评论。

### 5. #5816 [CLOSED] 持续尝试使用不存在的 `search` 工具
- **链接**：https://github.com/earendil-works/pi/issues/5816  
- **概要**：在 v0.79.4 中，Pi 反复尝试调用 `search` 工具并得到 “Tool search not found” 错误，导致代码变更无法进行。该问题在 7 条评论后迅速关闭，但影响用户实际使用。

### 6. #5790 [CLOSED] 在 settings.json 中支持 httpProxy
- **链接**：https://github.com/earendil-works/pi/issues/5790  
- **概要**：用户请求允许在 `settings.json` 中设定固定 HTTP 代理，而不必依赖环境变量。该请求获得了 7 条评论并快速合并入 PR，体现了社区对网络代理配置的刚需。

### 7. #5571 [CLOSED] `pi -p` 在非 TTY 管道且 stdin 永不关闭时无限挂起
- **链接**：https://github.com/earendil-works/pi/issues/5571  
- **概要**：当 stdin 来自非 TTY 管道且未关闭时，`pi -p` 无限制等待，而非快速报错。影响 CI 集成，7 条评论后关闭并修复。

### 8. #5728 [CLOSED] 在 auth.json 中支持 Provider 特定配置
- **链接**：https://github.com/earendil-works/pi/issues/5728  
- **概要**：部分 Provider（如 `cloudflare-ai-gateway`）需要除 API Key 外的额外参数（accountId、gatewayId），用户希望能在 `auth.json` 内统一管理。7 条评论后功能已实现（对应 PR #5807）。

### 9. #5700 [OPEN] 支持多 Agent 会话及 TUI 切换
- **链接**：https://github.com/earendil-works/pi/issues/5700  
- **概要**：用户期望 Pi 能同时运行多个 Agent 会话，并在 TUI 中自由切换。目前 `switchSession` 会拆除当前会话，无法后台并发。该功能需求获得 5 条评论且标签为 OPEN，代表社区对并发工作流的渴望。

### 10. #5763 [OPEN] Provider 吞没 HTTP 错误体，导致网关/非 Schema 错误不可读
- **链接**：https://github.com/earendil-works/pi/issues/5763  
- **概要**：当网关返回非 2xx 响应且 body 无法解析为标准 schema 时，多数 Provider 直接丢弃 body，只显示 “UnknownError” 或 “403 status code”。严重影响调试，获得 4 条评论，目前仍 OPEN，已有关联 PR #5820。

---

## 重要 PR 进展

过去 24 小时内共有 9 个 PR 更新或合并，以下逐一说明：

### 1. #5812 — fix(tui): 保护 Markdown 表格内联代码中的管道符
- **链接**：https://github.com/earendil-works/pi/pull/5812  
- **状态**：CLOSED  
- **说明**：修复 Markdown 表格单元格内反引号包裹的 `|` 被误当作列分隔符导致渲染截断的问题。通过自定义 tokenizer 覆盖表格渲染。

### 2. #5820 — fix: 保留非 Schema 错误的原始 HTTP 状态和 body
- **链接**：https://github.com/earendil-works/pi/pull/5820  
- **状态**：CLOSED  
- **说明**：对应 Issue #5763。引入共享错误格式化辅助函数，提取并展示底层 HTTP 状态码和原始负载，改善网关错误透明度。

### 3. #5807 — feat: 增加 Provider 作用域环境变量覆盖
- **链接**：https://github.com/earendil-works/pi/pull/5807  
- **状态**：CLOSED  
- **说明**：允许 `auth.json` 中为 API Key 条目指定 `env` 对象，覆盖 Provider 配置所需的各类环境变量（Cloudflare URL、Headers 等），优先级高于进程环境变量。社区呼声较高的功能。

### 4. #5809 — feat(ai): 向 Usage 中加入 durationMs 和 timeToFirstTokenMs，并在 footer 显示 tokens/sec
- **链接**：https://github.com/earendil-works/pi/pull/5809  
- **状态**：CLOSED  
- **说明**：扩展 `Usage` 接口，添加耗时和首 Token 延迟字段，同时 TUI footer 扩展可以消费这些指标，输出 tokens/sec 等性能信息。

### 5. #5789 — fix(tui): 恢复光标回到行首再浏览历史的行为
- **链接**：https://github.com/earendil-works/pi/pull/5789  
- **状态**：CLOSED  
- **说明**：修复按 `Up` 键时光标行为，确保在输入非空的第一个视觉行按 `Up` 跳转到行首（而非进入历史浏览），与之前行为一致。

### 6. #5803 — fix(ai): 拒绝畸形的 OpenAI 工具调用
- **链接**：https://github.com/earendil-works/pi/pull/5803  
- **状态**：CLOSED  
- **说明**：针对流式 tool call 结束时不包含 id 或 function name 的情况进行拒绝，并移除此类畸形调用以防止进入会话历史，并补充了回归测试。

### 7. #5801 — Nixify pi（为 Pi 添加 Nix Flake 打包）
- **链接**：https://github.com/earendil-works/pi/pull/5801  
- **状态**：CLOSED  
- **说明**：增加 Nix Flake 支持，允许用户通过 `nix build`、`nix run` 或 `nix profile add` 从源码构建 Pi，满足 Nix 生态用户需求。

### 8. #5798 — feat(coding-agent): 添加 Vercel AI Gateway 归属标识
- **链接**：https://github.com/earendil-works/pi/pull/5798  
- **状态**：CLOSED  
- **说明**：在 Pi 发出的请求中加入 `http-referer` 和 `x-title` 头部，方便 Vercel AI Gateway 识别流量的应用来源，改善平台支持。

### 9. #5796 — chore: 将 TypeScript target/lib 升至 ES2024，使用 Promise.withResolvers()
- **链接**：https://github.com/earendil-works/pi/pull/5796  
- **状态**：OPEN  
- **说明**：技术债务清理，将 tsconfig 中的 target/lib 从 ES2022 升级到 ES2024，替换手写的 `Promise.withResolvers()` 实现。目前处于开放状态，等待合并。

---

## 功能需求趋势

综合过去 24 小时的 Issues 与 PR，社区关注点集中在以下方向：

- **Provider 生态扩展**：大量 Issue 围绕新增或对齐 Provider 参数（如 Moonshot/Kimi 工具 schema 兼容性、DeepSeek V4 思考模式切换、Cloudflare 额外配置），以及通过 `auth.json` 支持 Provider 作用域环境变量（#5728、PR #5807）。
- **多会话并发与管理**：用户强烈希望 Pi 能同时运行多个 Agent 会话并在 TUI 中自由切换（#5700），这表明工作流复杂度在上升。
- **可观测性**：为 Usage 添加计时字段和 tokens/sec 显示（PR #5809）、暴露 HTTP 错误体（#5763、PR #5820）均是为了提升调试与性能监测能力。
- **RPC 接口扩展**：有用户提出增加 `get_entries` / `get_tree` 只读命令（#5810），以便外部工具驱动 Pi，暗示社区开始将 Pi 视为可编程后端。
- **跨平台打包**：Nix Flake 支持（PR #5801）以及 Windows CP-1252 编码问题（#5797）说明用户群覆盖了更多 Linux 发行版和传统 Windows 开发环境。
- **TUI/CLI 体验细节**：Markdown 表格渲染（#5812）、Tab 补全交互（#5670）、流式输出滚动控制（#5825）等微改进获得多次讨论，表明核心用户对交互质量要求较高。

---

## 开发者关注点

- **连接与超时**：`openai-codex` 长时间卡在 “Working…”（#4945）是当前最严重的稳定性痛点，严重影响工作效率。
- **工具调用失败**：`search` 工具报 “not found”（#5816）以及畸形 tool call 未被拒绝（#5803）说明工具调用链的健壮性仍需加强。
- **流式输出滚动干扰**：多个用户报告 TUI 在流式输出时自动跳转到顶部或底部（#5576、#5825），打断阅读，且与 `clear on shrink` 设置相关。
- **错误信息不透明**：Provider 吞没 HTTP 错误体（#5763）让用户难以排查网关或配置问题，PR #5820 已在解决路径上。
- **会话管理缺陷**：会话文件夹冲突（#4877）和会话列表仍保留全文（#5556）影响大量会话下的性能与数据体积。
- **终端兼容性**：Kitty 下按键重复（#5407）、Warp 下长 URL 显示异常（#5783）表明仍有边缘终端需要适配。
- **编码与历史项目**：Windows CP-1252 文件编码被破坏（#5797）是旧 C++ 项目的痛点，提醒 Pi 应尊重原始编码。
- **安装与更新体验**：启动时 “Update Available” 对不可自更新的安装方式（如 Nix）仍推荐 `pi update` 造成误导（#5607）。

以上为 Pi 社区 2026-06-17 的完整动态日报，供技术开发者参考。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-06-17

---

## 今日速览

今日社区动态高频且多元。最核心的问题是 **CI 流水线缺陷与 Release 构建接连失败**（#5219 / #5222），官方发布的 v0.18.1-preview.1 因集成测试门禁缺失而无法通过，团队已紧急反思测试策略。与此同时，社区贡献活跃：**QQ 机器人 Channel 适配器**（#5201）与**视觉桥接功能**（#5126）两个大型 PR 已就绪。稳定性方面，Windows 平台的**误报 Trojan**（#5055）、**/quit 后 OOM 崩溃**（#5147）以及**终端残留在鼠标追踪模式**（#5212）等 Bug 引发广泛讨论。

---

## 版本发布

过去 24 小时内无正式版本发布。值得注意的是，v0.18.1-preview.1 的 Release 流水线（#5222 / #5215）及 Nightly 构建（#5214）均因集成测试固件未同步 `daemon_status` 字段而失败，修复 PR（#5211）已提交，建议关注流水线恢复情况。

---

## 社区热点 Issues（Top 10）

### 1. [#5219 CI 集成测试不在 PR 阶段运行，回归只能在发布时暴露](https://github.com/QwenLM/qwen-code/issues/5219)
- **重要性:** ⭐⭐⭐⭐⭐ 社区与官方公认的流程缺陷。e2e 集成测试仅由 nightly pipeline 触发，PR 即使破坏测试也无法被发现，一旦合入 main 流水线直接报红。**这是今日多起 Release 失败的根因。**

### 2. [#5222 / #5215 / #5214 Release 流水线连续失败](https://github.com/QwenLM/qwen-code/issues/5222)
- **重要性:** ⭐⭐⭐⭐⭐ GitHub Actions 自动创建的失败告警，v0.18.1-preview.1 及 Nightly 版本均因集成测试断言不一致（缺少 `daemon_status`）构建中断。官方需尽快恢复发布通道。

### 3. [#5055 VSIX 安装包被 Windows Defender 报木马 (Trojan:JS/ShaiWorm.DBA!MTB)](https://github.com/QwenLM/qwen-code/issues/5055)
- **重要性:** ⭐⭐⭐⭐⭐ 直接影响 Windows 用户信任与安装。虽大概率是 JS 打包逻辑的误报，但如果长期未解决，将阻碍整个 Windows 生态的落地。社区反应强烈。

### 4. [#5147 执行 /quit 后 V8 堆栈溢出 (OOM)](https://github.com/QwenLM/qwen-code/issues/5147)
- **重要性:** ⭐⭐⭐⭐ 正常退出会话仍可能 OOM，根本原因指向 `managed auto-memory` 在后台构建转录时出现内存泄漏。长会话用户高危。

### 5. [#5206 自动更新在旧 glibc（如 CentOS 7）环境静默失败](https://github.com/QwenLM/qwen-code/issues/5206)
- **重要性:** ⭐⭐⭐⭐ 当 npm 全局安装需 sudo 时，自动更新静默转为捆绑 Node 22 的独立安装包，但在 glibc 2.17 上无法启动。**严重破坏生产服务器部署体验。** PR #5207 已合入修复。

### 6. [#5210 ExitPlanMode 卡住 7 小时以上](https://github.com/QwenLM/qwen-code/issues/5210)
- **重要性:** ⭐⭐⭐⭐ 用户使用 `qwen3.7-max` 时长时间卡在退出计划模式。与 #5177（`exit_plan_mode` 空参数崩溃）具有关联性，表明该流程的容错逻辑需要系统加固。

### 7. [#5212 CLI 退出后终端残留 SGR 鼠标追踪模式](https://github.com/QwenLM/qwen-code/issues/5212)
- **重要性:** ⭐⭐⭐ 严重影响终端体验——退出后滚动变成转义序列。感谢社区迅速提交 PR 并已关闭，**处理速度值得点赞。**

### 8. [#3203 Qwen OAuth 免费额度拟从 1000 次/天降至 100 次/天](https://github.com/QwenLM/qwen-code/issues/3203)
- **重要性:** ⭐⭐⭐⭐⭐ 136 条评论，社区反响极大。虽然反馈集中在 API 调用层面，但作为生态入口的调整，直接关系到开发者是否愿意继续依托 Qwen Code 做开发。

### 9. [#4615 支持项目级 .mcp.json 及“待批准”语义](https://github.com/QwenLM/qwen-code/issues/4615)
- **重要性:** ⭐⭐⭐⭐⭐ MCP 安全体系的关键缺失。提议 MCP 服务器配置不应自动启动，而是进入待批准状态，类似 VSCode 对 Workspace 建议的提示模式。与 #5221 (密钥加密) 形成完整安全矩阵。

### 10. [#5160 /model 列表显示已下线的 OAuth 模型](https://github.com/QwenLM/qwen-code/issues/5160)
- **重要性:** ⭐⭐⭐ 未配置 OAuth 的用户仍能看到 `[qwen-oauth] coder-model (Discontinued)` 排在列表第一位。典型的配置管理 bug，欢迎提交 PR。

---

## 重要 PR 进展（Top 10）

### 1. [#5221 密钥存储回退到加密文件](https://github.com/QwenLM/qwen-code/pull/5221)
- 当 OS 密钥链（Keychain）不可用时，敏感扩展设置将自动回退到 **AES-256-GCM 加密文件存储**，按服务命名空间隔离。这是 MCP 安全基础设施日益完善的标志。

### 2. [#5211 修复集成测试断言，并推动 E2E 在 PR 阶段运行](https://github.com/QwenLM/qwen-code/pull/5211)
- **今日最重要的修复之一。** 同步了 `SERVE_CAPABILITY_REGISTRY` 中的 `daemon_status` 字段到测试固件，并致力于让 E2E 测试在每次 PR 提交时执行，从流程层面解决 #5219 所述的核心顽疾。

### 3. [#5126 视觉桥接：为纯文本模型转录图片](https://github.com/QwenLM/qwen-code/pull/5126)
- **里程碑功能**。允许纯文本主模型接收图片（粘贴或 @ 引用），Qwen Code 自动调用配置的多模态模型转为文字描述。默认关闭，但为仅支持文本的模型打开了巨大的能力空间。

### 4. [#5202 QQ 机器人 Channel 适配器](https://github.com/QwenLM/qwen-code/pull/5202)
- 来自社区的大贡献。新增 `@qwen-code/channel-qqbot` 包，与已有 Telegram/微信/钉钉/飞书并列。支持 WebSocket Gateway、HEARTBEAT、RECONNECT 等完整生命周期。

### 5. [#5207 修复 sudo npm install 被静默迁移为独立安装包](https://github.com/LM/qwen-code/pull/5207)
- 针对 #5206 的精准修复。当 npm 全局安装具有 root 权限时，不再强制迁移到捆绑 Node 22 的独立安装包，保留原有 npm 更新路径。**保护了 CentOS 7 等老系统的用户。**

### 6. [#5182 秒级精度的 Session 唤醒引擎（/loop 基础）](https://github.com/QwenLM/qwen-code/pull/5182)
- 实现了 `CronScheduler`——一个独立于 cron job 的非持久化秒级唤醒通道，对标 Claude Code 的 `ScheduleWakeup`。这是 **/loop 命令迈向自定步调自动化**的基础设施。

### 7. [#5197 将 prompt-only /loop 接入自定步调唤醒](https://github.com/QwenLM/qwen-code/pull/5197)
- 在 #5182 之上，`/loop <prompt>` 现在会立即执行请求，然后允许模型通过 `loop_wakeup` 自行调度一次未来续接，而非固定周期 cron 模式。

### 8. [#5179 记住多个 Provider 共享同一 Model ID 时的选择](https://github.com/QwenLM/qwen-code/pull/5179)
- 当 `modelProviders` 中多个条目共享相同模型 ID 但指向不同的 `baseUrl` 时，现在会将选中的 `baseUrl` 持久化，避免每次都需要重新选择。**显著的 UX 改进。**

### 9. [#5141 将 sed 编辑操作纳入文件历史追踪](https://github.com/QwenLM/qwen-code/pull/5141)
- 安全的 `sed -i` 子集现在被视为正常的编辑确认而非盲盒式的 Shell 执行——支持预览 Diff、追踪文件历史、通过现有文件写入工具落地。**提升工具链的安全可解释性。**

### 10. [#5145 输入框 Placeholder 显示模型回复后的下一步建议](https://github.com/QwenLM/qwen-code/pull/5145)
- 模型回复后，输入框灰字提示后续操作建议（通过 `fastModel` 生成）。用户无需查找底部 chips，明显降低交互摩擦。

---

## 功能需求趋势

### 🔄 后台自动化与动态工作流
以 `/loop` 自定步调唤醒（#5182 / #5197）和 Port 动态工作流（#4721 / #5124）为代表，社区对**长期运行 Agent、定时唤醒、多步嵌套工作流**的需求明显从“想法”走向“实现”，对标 Claude Code 2.1.160。

### 🔒 安全体系全面升级
从项目级 `.mcp.json` 批准语义（#4615）、密钥加密存储回退（#5221），到 Session 隔离标记冲突（#5208），开发者不再满足于基础可用，而是要求**企业级权限管控与安全沙箱**。

### 📱 多平台与本地化
QQ 机器人 Channel（#5201）的加入明确瞄准中国市场。同时硬编码英文 UI 本地化提案（#5186 / #5189）已形成 PR，说明社区开始注重**非英语使用者的完整体验**。

### 🎨 CLI / TUI 交互精细打磨
退出 SGR 模式残存（#5212）、输入框建议（#5145）、@路径补全交互（#4841）、工具调用 Badge 本地化（#5220）——高频交互环节正在被逐个优化，目标是 **“零摩擦”终端体验**。

---

## 开发者关注点（痛点与高频需求）

### ⚠️ 信任与兼容性双杀
- **Trojan 误报**（#5055）和 **OAuth 策略突变**（#3203）联手打击新用户体验。
- **glibc 兼容性问题**（#5206）暴露了在拥抱最新 Node 22 的同时，对 Legacy 生产环境的兼容性测试缺位。

### 🔧 贡献者体验瓶颈
- **CI 不在 PR 阶段运行**（#5219）是开源贡献者最大的拦路虎——即使提交了高质量的 QQ Bot 适配器、视觉桥接等大型 Feature，缺乏 E2E 回归门槛意味着合入风险难以被第一时间发现。
- 值得肯定的是，团队已迅速通过 #5211 开始纠正。

### 🤖 模型配置管理有待完善
- 废弃的 OAuth 模型依然挂在 `/model` 列表首位（#5160），多 Provider 共享同一 Model ID 时选择记不住（#5179 PR 前就存在），表明**模型配置的状态管理与优雅降级**仍有提升空间。

### 🐛 稳定性痛点
- `/quit` 后的 OOM 崩溃（#5147）和 `exit_plan_mode` 长时间卡死（#5210）是当前最影响**日常高频使用**的前两个 Bug，开发者普遍期待尽快修复合入。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，作为专注AI开发工具的技术分析师，以下是根据 GitHub 数据生成的 **DeepSeek TUI (CodeWhale) 社区动态日报**。

---

# DeepSeek TUI 社区动态日报 - 2026-06-17

> **注：** 项目已正式更名为 **CodeWhale**，原 `deepseek-tui` 名称已弃用。本文保留“DeepSeek TUI”作为社区习惯称呼，实际仓库和代码均以 **CodeWhale** 为准。

## 今日速览

1. **品牌重塑落地**：v0.8.61 正式以 CodeWhale 名称发布，旧 npm 包停止更新，社区正经历迁移阵痛。
2. **v0.9.0 划时代功能开工**：Workrooms（基于聊天的持久化 Agent 工作区）Phase 1 PR 于今日提交，多 Agent 协作步入新阶段。
3. **兼容性与稳定性仍是痛点**：Ubuntu 24.04 安装失败（#3268）与持续卡死问题（#2487）引发开发者广泛讨论，社区贡献者迅速提交了 musl 静态构建等修复方案。

## 版本发布

**v0.8.61 发布** — **品牌重塑 & 规范资产名称**
- **核心变更**：项目规范命名为 **CodeWhale**，CLI 命令、npm 包名、Release 产物均统一为 `codewhale`。旧 npm 包 `deepseek-tui` 进入维护状态，不再接收新版本。
- **迁移指引**：从旧版（v0.8.x 的 `deepseek` / `deepseek-tui`）迁移的用户请查阅 `docs/REBRAND.md`。
- **下版预告**：多个 Issue 已标记 v0.8.62，计划加入 **Agent 澄清提问**（#3102）及 **架构整合**（#3101）等能力。

## 社区热点 Issues
（按更新热度排列，附社区反应分析）

**1. [#2487 Turn stalled - no completion signal received](https://github.com/Hmbown/CodeWhale/issues/2487)**
- **标签**: bug, enhancement, v0.8.61
- **重要性**: **严重**。在 `yolo` 模式下操作频繁卡死、无法恢复，需强制退出。
- **社区反应**: 14 条评论，仅 1 个👍（可能是“我也遇到”）。用户多次反映“依然无法恢复”，是当前最影响日常使用的稳定性阻碍。

**2. [#2739 任务执行过程中卡死的状态](https://github.com/Hmbown/CodeWhale/issues/2739)**
- **标签**: bug, v0.8.61, v0.8.64
- **重要性**: **严重**。中文用户深度反馈，该问题从 v0.8.51 持续至今，v0.8.52 的修复（300秒超时）未完全奏效，用户表示“无法忍受”。
- **社区反应**: 4 条评论，描述了 `--continue` 后会话丢失的连带问题。

**3. [#3209 EPIC: Chat-native CodeWhale workrooms for threaded, shareable agent work](https://github.com/Hmbown/CodeWhale/issues/3209)**
- **标签**: v0.9.0 EPIC
- **重要性**: **战略性**。定义 CodeWhale 下一代交互形态：从终端/本地网页转向聊天原生工作区（线程、频道、分享、移动端）。
- **社区反应**: 2 条评论，由核心作者 Hmbown 创建，详细定义了 Phase 1~3。

**4. [#3101 v0.8.62: Finish Paulo Aboim Pinto's command, tool, compaction and TUI architecture stream](https://github.com/Hmbown/CodeWhale/issues/3101)**
- **标签**: documentation, enhancement, cleanup, v0.8.62
- **重要性**: **架构级别**。明确如何整合贡献者 Paulo 的大量高质量但分散的重构工作，避免设计意图丢失。
- **社区反应**: 4 条评论，Hmbown 主导了分步合并策略。

**5. [#3268 failed to install on a brand new ubuntu 24 lts](https://github.com/Hmbown/CodeWhale/issues/3268)**
- **标签**: bug, documentation
- **重要性**: **入门屏障**。在腾讯云 Ubuntu 24.04 通过 `cargo install` 失败，暴露了 libdbus 等构建依赖缺失。
- **社区反应**: 4 条评论，快速定位到缺少系统依赖，直接推动了文档更新（PR #3270）和静态构建方案（PR #3274）。

**6. [#3275 CodeWhale overly engaged in modifications, deviating from user intent](https://github.com/Hmbown/CodeWhale/issues/3275)**
- **标签**: bug, question
- **重要性**: **功能回归**。Agent 过度主动修改代码，自问自答，不等待确认。
- **社区反应**: 当日最新（6月17日创建），引用 #3061。代表用户对 Agent 自主度的担忧，若广泛出现会严重影响信任。

**7. [#2870 EPIC: staged command-boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)**
- **标签**: documentation, v0.9.0, cleanup, tui
- **重要性**: **架构重构**。将命令边界重构分成可合并的小 PR，是 v0.9.0 的核心基础设施工作。
- **社区反应**: 4 条评论，持续性跟进多个子任务。

**8. [#3015 Land constitution system prompt (YAML source-of-truth + renderer)](https://github.com/Hmbown/CodeWhale/issues/3015)**
- **标签**: documentation, enhancement, agent-ready, v0.8.58
- **重要性**: **提示工程演进**。用 `constitution.yaml` 作为权威提示来源，替换旧 `base.md`，是 v0.8.58 最大的架构变更。
- **社区反应**: 3 条评论，补上了提交时遗漏的追踪 Issue。

**9. [#3266 Sub-agent agent_eval with block=True causes TUI freeze/deadlock](https://github.com/Hmbown/CodeWhale/issues/3266)**
- **标签**: bug, documentation
- **重要性**: **并发缺陷**。多个子 Agent 同时 `block=True` 调用 `agent_eval` 导致界面死锁。
- **社区反应**: 2 条评论，快速提交并已被关闭（可能是紧急 patch）。暴露多 Agent 并发的稳定性风险。

**10. [#3240 Legacy deepseek configuration](https://github.com/Hmbown/CodeWhale/issues/3240)**
- **标签**: bug
- **重要性**: **迁移残留**。尽管改名为 CodeWhale，运行时仍创建旧的 `.deepseek` 目录，Windows 下 `.codewhale` 与 `.deepseek` 同时存在。
- **社区反应**: 2 条评论，表明部分配置/文件引用仍需清理，品牌切换未完全干净。

## 重要 PR 进展

（过去24小时内更新的 9 个 PR 均具有代表性，全部列出）

**1. [#3277 [OPEN] feat: implement Workrooms Phase 1 — data model, endpoints, docs, and tool](https://github.com/Hmbown/CodeWhale/pull/3277)**
- **贡献者**: idling11
- **重点**: v0.9.0 核心功能开端。包含 242 行的设计 RFC、数据模型、REST 接口及迁移工具。今日最大 PR。

**2. [#3274 [OPEN] feat(release): build static Linux x64 binaries with musl](https://github.com/Hmbown/CodeWhale/pull/3274)**
- **贡献者**: wavezhang
- **重点**: 将 Linux x64 发行版从动态 glibc 切换到静态 musl。直接解决 #3268、#3238 等 glibc 版本兼容问题。

**3. [#3270 [CLOSED] docs: add Linux build-time deps to cargo install guides](https://github.com/Hmbown/CodeWhale/pull/3270)**
- **贡献者**: zlh124
- **重点**: 在 `docs/INSTALL.md` 补充 libdbus-1-dev、pkg-config 依赖说明，降低 Ubuntu 用户编译门槛。

**4. [#3269 [CLOSED] feat(tui): expose slash commands as hotbar actions](https://github.com/Hmbown/CodeWhale/pull/3269)**
- **贡献者**: reidliu41
- **重点**: 允许将斜杠命令（`/mode`, `/task`）绑定到 TUI 底部 Hotbar，弥补键盘快捷键不足的问题。

**5. [#3271 [CLOSED] docs: add Ponytail personality to project instructions](https://github.com/Hmbown/CodeWhale/pull/3271)**
- **贡献者**: ousamabenyounes
- **重点**: 在项目说明中增加第三方 personality（Ponytail）推荐，丰富内置角色生态。

**6. [#3267 [CLOSED] feat(tui): keep oversized paste inline with truncation and auto-expand](https://github.com/Hmbown/CodeWhale/pull/3267)**
- **贡献者**: idling11
- **重点**: 修正大段粘贴时自动转为文件引用的问题，改为保留内联并可展开编辑，保留用户编辑权 (#3263)。

**7. [#3236 [CLOSED] add DeepInfra provider support](https://github.com/Hmbown/CodeWhale/pull/3236)**
- **贡献者**: nightt5879
- **重点**: 支持 DeepInfra 模型提供商，补齐了社区呼声很高的缺失 (#3231)。

**8. [#2998 [CLOSED] chore(deps-dev): bump tailwindcss from 3.4.19 to 4.3.1 in /web](https://github.com/Hmbown/CodeWhale/pull/2998)**
- **贡献者**: dependabot[bot]
- **重点**: Dependabot 发起的自动化版本升级（Tailwind v3→v4），触发了项目内主动进行手动升级的跟踪 (#3276)。

**9. [#2933 [OPEN] feat(hippocampal): v2 memory system — glossary, namespaces, rollback, auto-inject, daemon](https://github.com/Hmbown/CodeWhale/pull/2933)**
- **贡献者**: cy2311
- **重点**: 大版本记忆系统升级（Schema 迁移、命名空间、回滚、后台守护进程），尚未合并，标记 `needs-human`，是 v0.9 周期的重要候选。

## 功能需求趋势

从近期 Issues 可以明显看到社区关注的三个方向：

1. **多 Agent 与持久化工作区（v0.9.0 方向）**  
   `Workrooms` (#3209)、`Hippocampal Memory v2` (#2933) 表明社区已不满足于单次会话，需要**持久上下文、侧信道、共享工作流**。

2. **模型生态与元数据管理**  
   增加新提供商（DeepInfra #3236，Novita #3255 修复，Moonshot #3265 修复），以及对硬件编码模型列表的**元数据注册表**需求（#3071, #3072, #3073）——社区期望更透明的定价/上下文长度管理，并希望系统自动按模型能力调整行为。

3. **TUI 交互增强与稳定性**  
   - 输入层改进：热键绑定 (#3269)、粘贴行为 (#3267)、数字键冲突 (#3243)。  
   - 表述能力：Agent 向用户主动提问确认（#3102）、超链接可用性 (#3029)。  
   - 可靠性：剔除卡死（#2487, #2739）、子 Agent 死锁（#3266）依然是第一优先级。

## 开发者关注点

- **稳定性痛点**：`Turn stalled` 等卡死问题反复出现，在 v0.8.61 中仍未彻底解决，多名用户表示严重阻碍使用，希望核心团队优先修复。
- **构建/部署门槛**：Linux 用户因 glibc 版本或缺失 libdbus 无法安装，**musl 静态构建**成为呼声最高的发行方案（PR #3274 应运而生）。
- **系统人格过于强势**：Agent 不等待确认、过度修改（#3275）正在影响用户对 Agent 自主度的信任，需要更可控的 “ask before act” 模式。
- **迁移阵痛**：项目更名虽好，但遗留配置目录 (`.deepseek`)、旧文档引用仍需清理，否则造成混淆（#3240）。
- **子 Agent 生态尚不稳定**：`block=True` 死锁（#3266）、输出截断被当作完整证据（#2652）等，说明多 Agent 协调机制尚在早期阶段，需要更完善的熔断/提示机制。

---
*本日报由 AI 自动整理，仅供参考。如要查看最新动态，请直接访问 [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)。*

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*