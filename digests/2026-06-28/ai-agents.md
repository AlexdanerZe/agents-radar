# OpenClaw 生态日报 2026-06-28

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-28 03:30 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

好的，这是根据您提供的 OpenClaw 项目 GitHub 数据生成的 2026-06-28 项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-28

### 1. 今日速览

OpenClaw 项目今日呈现出**极高活跃度**，24 小时内累计有 500 条 Issue 和 500 条 PR 产生更新。尽管无新版本发布，项目在**核心稳定性修复**（如 P0 级内存泄漏与会话锁死）和**架构重构**（向 SQLite 迁移）上取得了实质进展。但需警惕的是，**海量的待审查积压**（`needs-maintainer-review`）和**高优回归 Bug**（如 Coding Agent 瘫痪）正在考验项目维护团队的健康度与社区信任。

### 2. 版本发布

过去 24 小时内无新版本发布。

### 3. 项目进展

过去 24 小时，项目在 **会话稳定性** 和 **架构升级** 两条主线上取得了重要进展。

*   **嵌入式 Runner 重大问题修复**
    *   **[#95833] (已关闭)**：修复了子 Agent 中止结算时未能释放 `sessions.jsonl.lock` 文件锁，导致会话永久卡死在“Something went wrong”状态的问题。
    *   **[#95915] (已关闭)**：修复了嵌入式运行中止后，会话堆内存（Heap）未释放导致内存逐步耗尽的问题。
    > 这两项修复对于大规模并发场景下的生产稳定性是重大利好。
*   **存储架构升级**
    *   **[#96625] (待合并)**：由 @jalehman 提交的大规模重构 - **将会话和转录存储从 JSONL 文件切换至 SQLite**。这是解决长期顽疾（如 [#55334](openclaw/openclaw Issue #55334) `sessions.json` 无限制增长）的根本方案，也是项目架构演进的关键一步。
*   **模型兼容性与国际化**
    *   **[#96319] (已关闭)**：为安卓 App 贡献了完整的简体中文本地化 `strings.xml`（220+ 条翻译）。
    *   **[#69729] (待合并)**：启用了 DashScope 编码计划 CN 端点的 `qwen3.6-plus` 模型，并修正了其推理标志。
*   **安全与配置增强**
    *   **[#69417] (待合并)**：为 MCP 服务器配置中的 `env` 和 `headers` 字段增加了 `SecretRef` 支持，允许敏感信息从密钥管理服务读取，提升了配置安全性。

### 4. 社区热点

*   **Agent 承诺的可信度危机** - **[#58450](openclaw/openclaw Issue #58450)**
    *   **15 条回复，铂金级讨论**。用户报告 Agent 在对话结束时承诺“我将稍后跟进”，但实际上并未启动任何后台任务或工具调用。
    *   **分析**：这直击 AI Agent 的 **“规划-行动”闭环** 痛点。用户需要的不仅是礼貌的回复，更是可被验证的后续行动。这反映出社区对 Agent **透明度和任务可靠性** 的极致追求。

*   **Coding Agent 核心场景崩溃** - **[#62505](openclaw/openclaw Issue #62505)**
    *   **14 条回复，回归问题**。用户表示曾经正常的 Coding Agent 现在完全无法产出实质性代码，只能输出“模糊的状态更新然后为模糊道歉”。
    *   **分析**：Coding 是 OpenClaw 最核心的生产力场景，该回归严重打击了主用户群体的信任。用户情绪明显沮丧，背后是**对版本发布质量管控**（Regression）的强烈质疑。

*   **多 Agent 知识隔离的强烈诉求** - **[#63829](openclaw/openclaw Issue #63829)**
    *   **10 条回复，9 个赞**。“为每个 Agent 配置独立的记忆维基库”获得了极高的社区共识度。
    *   **分析**：这不仅是功能请求，更是多 Agent 场景下信息安全和准确性的刚需。当前共享全局记忆库的设计在复杂工作流中显得力不从心。

*   **基础 UI 功能的缺失** - **[#42840](openclaw/openclaw Issue #42840)**
    *   **8 条回复，7 个赞**。用户强烈要求在 Control UI 中支持 MathJax/LaTeX 数学公式渲染。
    *   **分析**：该项目吸引了大量学术和科学计算用户，LaTeX 等专业渲染支持的缺失是明显的功能短板。

### 5. Bug 与稳定性

| 严重程度 | Issue | 现象 | 状态 |
| :--- | :--- | :--- | :--- |
| **P0** | **[#91588](openclaw/openclaw Issue #91588)** | **Gateway 内存泄漏**：RSS 从 350MB 涨至 15.5GB，导致 OOM 频繁被杀并循环重启。 | 活跃，14条讨论 |
| **P1** | **[#62505](openclaw/openclaw Issue #62505)** | **Coding Agent 回归**：无法完成任何实质性工作，只输出模糊更新和道歉。 | 活跃，待合修复 PR |
| **P1** | **[#92201](openclaw/openclaw Issue #92201)** | **Anthropic 流式 Thinking 签名无效**：重放时频繁失败，且恢复逻辑因错误文本泛化而失效。 | 活跃，需维护者审查 |
| **P1** | **[#63216](openclaw/openclaw Issue #63216)** | **反复 Hard Reset**：即使高 `reserveTokensFloor` 配置下，仍因上下文溢出导致重复硬重置。 | 活跃，需直播复现 |
| **P1** | **[#64810](openclaw/openclaw Issue #64810)** | **Telegram 心跳吞没回复**：异步系统事件中断并吞掉了用户在话题中的正在输入回复。 | 活跃，需直播复现 |
| **P1** | **[#95833](openclaw/openclaw Issue #95833) / [#95915](openclaw/openclaw Issue #95915)** | **嵌入式 Runner 会话锁死与堆泄漏**：子 Agent 中止后锁文件未释放、堆未释放。 | **已关闭 (已修复)** |
| **P1** | **[#67366](openclaw/openclaw Issue #67366)** | **`onboard` 命令崩溃**：替换 Telegram Token 时因 TypeError 导致流程崩溃。 | 活跃 |
| **P2** | **[#57901](openclaw/openclaw Issue #57901)** | **Safeguard Compaction 忽略模型配置**：自定义的 `compaction.model` 设置被无视。 | 活跃，待合修复 PR |
| **P2** | **[#67419](openclaw/openclaw Issue #67419)** | **引导文件重复注入**：每轮对话浪费 20-30% 的 Token 用于重新注入引导文件。 | 活跃 |

### 6. 功能请求与路线图信号

*   **大概率纳入路线图（与架构演进方向一致）**
    *   **[#60572](openclaw/openclaw Issue #60572) 多插槽记忆架构**：允许不同记忆提供者同时处理记忆栈的不同层次，与当前存储重构高度契合。
    *   **[#63990](openclaw/openclaw Issue #63990) 多索引 Embedding 记忆**：支持模型故障切换而不破坏向量语义，是生产高可用部署的关键。
    *   **[#63930](openclaw/openclaw Issue #63930) 支持 Anthropic Advisor 工具**：紧跟上游 Server-side Tool API 变化，是维持模型能力先进性的基础设施。

*   **社区呼声高，有潜力进入短期规划**
    *   **[#64046](openclaw/openclaw Issue #64046) 敏感数据脱敏**：8 条讨论，涉及 Token、API Key 等配置和日志的明文隐患，是企业级安全准入的必选项。
    *   **[#56349](openclaw/openclaw Issue #56349) 不可绕过的出站消息策略**：要求所有出站消息经过统一的前置校验/修改边界，满足严格合规需求。
    *   **[#66252](openclaw/openclaw Issue #66252) 每 Agent 独立 TTS/STT 配置**：满足多语言、多音色场景下的个性化需求。

### 7. 用户反馈摘要

*   **核心痛点：**
    *   **信任赤字 (Trust Deficit)**：用户在 `#58450` 中表达了对 Agent “只会说不会做”的失望，在 `#62505` 中对 Coding Agent 的瘫痪感到焦虑。Agent 的**可靠性和可预测性**是当前最大的用户体验黑洞。
    *   **回归焦虑 (Regression Anxiety)**：从 Coding Agent 到 Chrome 扩展中继，用户反复抱怨“更新后反而变差”，版本质量急需通过更严格的自动化测试矩阵来兜底。
    *   **成本失控 (Cost Spiral)**：`#67419`（Token浪费）和 `#91588`（OOM重启）导致用户无论从经济还是运维层面都面临着可用性挑战，尤其在生产部署中。

*   **积极信号：**
    *   尽管面临稳定性挑战，社区的核心贡献者依然在提交高质量的架构级 PR（如 `#96625` SQLite 重构），表明**核心开发者对项目长期愿景保持高度认同**。
    *   用户对官方跟进前沿技术的能力充满期待，如对 `#63930` (Anthropic Advisor Tool) 和 `#97350` (Codex Hook) 的积极讨论。

### 8. 待处理积压

项目维护团队面临严重的“审查瓶颈”。大量高价值 Issue 和 PR 处于等待状态，可能消磨贡献者的耐心。

*   **高危待审 Issue（超过 2 个月无实质性推进）**
    *   **[#51429](openclaw/openclaw Issue #51429) 代码中包含硬编码路径** (2026-03-21)：因明显的低级别代码质量问题引发社区哗然，急需维护者出面解释并修复。
    *   **[#53599](openclaw/openclaw Issue #53599) Chrome 扩展中继移除回归** (2026-03-24)：直接影响到托管服务商的核心业务场景，急需产品决策是重建还是放弃。
    *   **[#57326](openclaw/openclaw Issue #57326) CLI 辅助路径绕过分发** (2026-03-29)：残留的安全攻击面，需安全审查。

*   **等待作者回应的 PR（超 2 周无更新，项目方应考虑干预）**
    *   **`#69417`** (MCP SecretRef 支持)、**`#69346`** (嵌入式 Runner 诊断)、**`#69729`** (Qwen 模型支持)、**`#97234`** (NO_PROXY 匹配增强)。这些 PR 的价值很高，但作者在收到 Review 反馈后迟迟未能更新。项目维护者可以考虑自行接手完成尾项，或释放 reviewer 资源。

*   **长期待决的产品决策需求**
    *   `#54531` (强制回复原始频道)、`#63829` (独立记忆维基)、`#43454` (Gateway 生命周期钩子) 等贴有 `needs-product-decision` 标签的功能请求堆积了数月，反映出产品侧资源可能正优先聚焦于核心架构和稳定性，功能扩展线的节奏暂时放缓。

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态横向对比分析报告
**报告日期：2026-06-28 | 数据统计窗口：2026-06-27 ~ 2026-06-28（UTC）**

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **高速分化与质量阵痛并存的阶段**。一方面，核心基础设施项目（如 OpenClaw）通过海量社区贡献推动架构演进（SQLite迁移、多Agent协作总线），但海量积压和回归问题考验着项目治理能力。另一方面，一批专注特定场景的衍生项目（PicoClaw、NanoClaw、ZeroClaw等）在轻量化、多租户、安全合规、供应链等方向快速迭代，形成了“一超多强”的竞争格局。社区对 **Agent 可靠性、配置安全、多平台兼容性** 的诉求空前强烈，但不同项目在成熟度与资源投入上差距显著，企业级落地仍在早期探索阶段。

---

## 2. 各项目活跃度对比

| 项目 | Issue更新数¹ | PR更新数¹ | Release | 健康度评估 | 核心态势 |
|------|--------------|-----------|---------|------------|----------|
| **OpenClaw** | ~500 | ~500 | 无 | ⚠️ 极高活跃但积压严重 | 架构重构期，存储层改SQLite，P0修复密集 |
| **Hermes Agent** | 50 | 50 | 无 | 🟢 极高活跃，修复冲刺 | 37 Issue关闭、17 PR合入，集中清理P1缺陷 |
| **ZeroClaw** | 49 | 50 | 无 | 🟢 极度活跃，健康度佳 | MCP完整化+供应链安全，多RFC并行 |
| **IronClaw** | 11 (关9) | 50 (合23) | 无 | 🟢 高活跃，里程碑合入 | 权限系统五层链合并完成，Nightly E2E隐患 |
| **NanoBot** | 6 (结5) | 37 (合22) | 无 | 🟢 优秀，响应极快 | Shell注入修复，Cron静默模式落地 |
| **CoPaw (QwenPaw)** | ~15 | 13 (合1) | 无 | 🟢 高活跃，测试加固中 | 大规模单元测试攻坚，DeepSeek兼容修复 |
| **PicoClaw** | 3 | 3 (合2) | 无 | 🟡 健康，功能落地 | Agent协作总线合并，Matrix加密Bug待响应 |
| **LobsterAI** | 2 (新) | 7 (合/关7) | 无 | 🟡 中等，清理积压中 | 统一关闭7个历史PR，备份卡死是新风险 |
| **Moltis** | 1 | 2 | 无 | 🟡 稳中有升，打磨期 | 小模型参数类型修复待合并 |
| **NanoClaw** | 2 | 8 (无合) | 无 | 🔴 高产出低流通 | 8个PR积压待合并，维护者响应瓶颈 |
| **NullClaw** | 1活跃 | 1新PR | 无 | 🔴 低活跃，静默发展 | 结构化审批流PR待审，移动端构建阻塞 |
| **TinyClaw** | — | — | — | ⚫ 无活动 | — |
| **ZeptoClaw** | — | — | — | ⚫ 无活动 | — |

¹注：Issue/PR更新数指24小时内发生状态变更的事件总数，来源各项目日报。  
健康度：🟢优秀/🟡一般/🔴需关注/⚫停滞。

**关键发现**：
- **OpenClaw** 的事件量级远超其他项目（500级别），但PR合入率相对较低，维护积压问题突出。
- **ZeroClaw** 与 **IronClaw** 在功能复杂度与社区深度上紧随其后，且维护节奏更健康。
- **NanoBot** 以极低的Bug存活周期和快速响应成为“小而美”典范。
- **NanoClaw** 贡献者产出高但合并通道堵塞，有失去外部贡献者的风险。

---

## 3. OpenClaw 在生态中的定位

### 3.1 核心定位
OpenClaw 是生态中 **覆盖最全面、社区最大、但复杂度最高** 的通用Agent框架。日均500+更新事件证实其占据流量核心位置，但同样代码库庞大，修复速度与PR审查速度的矛盾日益尖锐。

### 3.2 相对优势
- **功能广度**：会话管理、嵌入式Runner、Coding Agent、MCP适配、多语言翻译等一应俱全。
- **社区规模**：Issue/PR量级是第二名（Hermes/ZeroClaw）的10倍，拥有最多潜在贡献者。
- **架构前瞻**：向SQLite迁移（#96625）和多插槽记忆（#60572）等举措表明正在系统性地解决可扩展性债务。

### 3.3 明显短板
- **信任赤字**：Coding Agent回归（#62505）和Agent口头承诺不行动（#58450）直接动摇核心生产力场景。
- **审查瓶颈**：`needs-maintainer-review` 标签堆积数月，部分高优PR（如Qwen模型支持#69729）等待超2周。
- **回归焦虑**：用户反复抱怨“更新后反而变差”，缺乏针对核心场景的自动化回归测试矩阵。

### 3.4 与同类对比
- **vs Hermes Agent**：Hermes在Provider多样性和Gateway稳定性上修复更快，社区规模较小但维护效率高。
- **vs ZeroClaw**：ZeroClaw在MCP协议深度和供应链安全上领先，且RFC→PR转化高效，OpenClaw在架构升级上稍显笨重。
- **vs NanoBot**：NanoBot聚焦轻量部署，超轻量级定位吸引边缘场景，OpenClaw更偏重型全功能。

**结论**：OpenClaw是生态参考实现和功能创新的主要来源，但其治理模式亟需优化（自动化测试、维护者轮值、积压清理SLA）以维系领导地位。

---

## 4. 共同关注的技术方向

以下方向在多个项目中被反复提及或已有实施，反映行业共性需求：

| 技术方向 | 涉及项目 | 具体诉求/实施 |
|----------|----------|---------------|
| **多Agent协作与隔离** | OpenClaw（#63829独立记忆维基）<br>PicoClaw（#2937协作总线）<br>NanoBot（#4555会话独立模型预设）<br>IronClaw（#5270用户角色） | 每个Agent需要独立的记忆/工具/模型配置，避免全局污染。 |
| **MCP协议深度集成** | OpenClaw（#69417 SecretRef）<br>ZeroClaw（#8403 Resources/Prompts）<br>CoPaw（#5213 MCP布局）<br>NanoBot（#4542 MCP图像Artifacts） | 从“工具客户端”走向“全协议客户端”，支持资源、提示，增强安全配置。 |
| **小模型/非标准模型兼容** | Moltis（#1136参数类型强制转换）<br>CoPaw（#5573 DeepSeek V4）<br>OpenClaw（#69729 Qwen模型）<br>Hermes Agent（#43211 Provider降级） | Agent框架必须处理不同模型的JSON方言差异和工具调用不一致。 |
| **安全与权限治理** | OpenClaw（#69417 SecretRef）<br>NanoBot（#4562 Shell注入）<br>IronClaw（全五层capability-policy）<br>NullClaw（#969结构化审批）<br>ZeroClaw（#8404供应链签名） | 从API Key管理到工具调用审批，再到供应链签名，安全栈正在形成。 |
| **Agent执行可靠性** | OpenClaw（#62505 Coding回归，#58450信任赤字）<br>NanoBot（#4500 WebUI假死）<br>Hermes Agent（#53943意图延续）<br>IronClaw（#5808上下文预算） | 用户不再容忍“只会说不会做”，Agent需要可验证的执行路径和断点续传。 |
| **多设备/云同步** | Hermes Agent（#20510云同步，14👍）<br>ZeroClaw（#8226多租户）<br>OpenClaw（社区隐含诉求） | 用户期望配置、记忆、会话在PC/手机/服务器间无缝流动。 |
| **存储架构演进** | OpenClaw（#96625 JSONL→SQLite）<br>Hermes Agent（#52555模块化重构）<br>ZeroClaw（#8346测试覆盖） | 文件存储已到瓶颈，结构化数据库和内存/持久化分层成为趋势。 |
| **Dashboard/可观测性** | ZeroClaw（#8408 TUI插件系统）<br>NanoClaw（#2871 Dashboard Pusher）<br>Hermes Agent（#53951 Olympus监控） | 运维可视化需求上升，尤其是多Agent生成场景。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特色 |
|------|----------|----------|--------------|
| **OpenClaw** | 通用Agent平台，覆盖聊天、编码、任务自动化 | 开发者、企业用户、社区爱好者 | Python/Node？多Provider，嵌入式Runner |
| **Hermes Agent** | Provider多样性、Gateway稳定性、桌面客户端 | 多模型用户，Telegram/Discord社群 | 强调Anthropic/Discord适配，整合大量Gateway |
| **ZeroClaw** | 全栈MCP、供应链安全、WASM插件、企业级 | DevOps、企业安全团队、云部署用户 | Rust实现，cosign+SLSA+SBOM，TUI面板 |
| **IronClaw** | 多用户权限、RBAC、WebChat v2 | NEAR AI生态、多租户SaaS场景 | Rust，capability-policy史诗，REST控制平面 |
| **NanoBot** | 超轻量级、Cron自动化、快速迭代 | 个人极客、低资源服务器 | Python+Node，强调“轻”，Shell工具链 |
| **CoPaw** | 中文生态、多模型(DeepSeek/Qwen)、质量测试 | 中文开发者、Qwen用户 | AgentScope-AI，大规模测试覆盖 |
| **PicoClaw** | 轻量级多Agent协作、边缘部署 | 嵌入式/边缘设备开发者 | Go？Agent协作总线，信道扩展(Matrix/Simplex) |
| **NanoClaw** | 容器化多模型多代理、Dashboard监控 | Docker部署用户 | Kubernetes风格？多Channel支持，容器运行时 |
| **NullClaw** | 结构化审批、Zig语言、移动端 | Zig爱好者、安全敏感用户 | Zig编译，安全审批流程，Android/Termux |
| **LobsterAI** | 中文本地化、桌面端、定时任务 | 中文个人用户 | 桌面端优先，i18n，定期任务折叠 |
| **Moltis** | 小模型工具兼容、浏览器自动化 | 本地模型用户 | 侧重类型强制转换，容忍非标准模型输出 |

**分析**：项目分化主要体现在 **语言偏好（Rust/Zig/Python）、部署形态（桌面/容器/边缘）、安全成熟度（审批流/权限/供应链）**。OpenClaw与Hermes、ZeroClaw、IronClaw在功能深度上构成竞争，但各自的业务绑定（NEAR、Nous）和社区土壤不同。

---

## 6. 社区热度与成熟度分层

### 第一梯队：极活跃+高维护质量
- **ZeroClaw**：49 Issue/50 PR高产出，RFC→PR闭环快，健康度佳。
- **IronClaw**：能力策略史诗落地，合入率高，Nightly E2E是唯一隐患。
- **Hermes Agent**：一天关闭37 Issue+17 PR，Bug歼灭效率惊人。

### 第二梯队：活跃但存在瓶颈
- **OpenClaw**：活跃度最高但维护积压严重，回归问题损害信任。
- **NanoBot**：修复响应极快，但WebUI假死影响核心体验，规模尚小。
- **CoPaw**：积极加测试但大量PR待审，合并率低。

### 第三梯队：特定方向推进中
- **PicoClaw**：协作总线是亮点，Matrix Bug等待响应。
- **LobsterAI**：清理历史债务，但新Bug（备份卡死）严峻。
- **Moltis**：稳定打磨，小模型兼容方向有价值。

### 第四梯队：停滞或低活跃
- **NanoClaw**：有贡献但无合并，维护者缺席风险。
- **NullClaw**：新PR有价值但社区冷清。
- **TinyClaw / ZeptoClaw**：24小时无活动，可能已放弃。

**成熟度判断**：
- **企业级**：IronClaw（RBAC）、ZeroClaw（供应链+权限）、OpenClaw（基础但需改进）→ 接近可投入生产，但需补全审计、部署文档。
- **个人级**：NanoBot、PicoClaw、Moltis → 适合单用户/实验环境，功能聚焦。
- **开发者实验**：NullClaw、NanoClaw → 尚不成熟，需观望。

---

## 7. 值得关注的趋势信号（2026Q3）

### 7.1 Agent从“对话系统”进化为“自主工作流平台”
- **信号**：OpenClaw信任赤字、NanoBot Cron静默、ZeroClaw SOP执行器、Hermes意图延续。
- **启示**：开发者应将Agent输出从文本回复转向可验证的“行动计划+执行报告”，并引入撤回/重试/审计日志。这将成为框架设计和工具链的新基线。

### 7.2 MCP协议成为Agent间通信的事实标准
- **信号**：ZeroClaw全面实现Resources/Prompts；OpenClaw增加SecretRef；NanoBot支持MCP图像。
- **启示**：投入资源支持MCP而非自研内部通信协议，能更快融入生态。企业部署需关注MCP端点的安全和版本管理。

### 7.3 安全左移——从攻击修复到供应链信任
- **信号**：ZeroClaw的SLSA+cosign+SBOM、IronClaw的capability-policy、NanoBot的Shell注入、NullClaw的结构化审批。
- **启示**：框架需要默认提供“最小权限”模板，并集成密钥管理（Vault/SecretRef）。CI/CD中加入SBOM生成和签名验证将成为企业选型基本门槛。

### 7.4 非OpenAI模型的“方言地狱”倒逼框架层容错
- **信号**：Moltis的类型强制转换、CoPaw的DeepSeek字段清洗、OpenClaw的Qwen推理标志、Hermes的Provider降级。
- **启示**：Agent框架必须内置参数模式规范化层（Schema Coercion）和Provider适应器（Adaptive Provider）。对小模型的支持将成为差异化竞争力。

### 7.5 维护者瓶颈成为开源项目最大风险
- **信号**：OpenClaw的needs-maintainer-review堆积、NanoClaw的CutSnake01 PR积压7天、Hermes和ZeroClaw的高效对比。
- **启示**：项目治理需要引入自动化合并（对低风险PR）、维护者轮值、以及社区自治委员会。否则即使有优秀贡献者，也会因审查延迟而流失。

### 7.6 用户从“功能期待”转向“信任期待”
- **信号**：OpenClaw的“Agent承诺不行动”、Coding Agent瘫痪、NanoBot的“WebUI假死”、LobsterAI的“备份卡死”。
- **启示**：任何功能飞快的迭代都必须优先保证核心场景的可靠性。测试覆盖率（如CoPaw的100+测试）和回归测试自动化将成为社区评判项目健康度的关键指标。

---

**总结建议**：
- 对 **技术决策者**：若追求稳定与多租户，优先评估ZeroClaw或IronClaw；若需最高社区资源，选择OpenClaw但需自行投入修复积压贡献。
- 对 **独立开发者**：NanoBot（轻量部署）或PicoClaw（边缘多Agent）入门成本低，若需要中文支持选LobsterAI。
- 对 **安全团队**：ZeroClaw的供应链体系、NullClaw的结构化审批提供参考，但两者仍在早期。
- 对 **学术/研究**：Hermes Agent的Provider多样性研究和OpenClaw的架构重构论文价值高。

本报告基于2026-06-28单一窗口数据，建议持续跟踪2-4周以获取更稳健趋势判断。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，以下是 2026-06-28 的 NanoBot 项目动态日报。

---

# NanoBot 项目日报 | 2026-06-28

## 1. 今日速览

过去 24 小时，NanoBot 项目维持着极高的迭代强度。在 **37 个 PR 更新（其中 22 个已合入/关闭）** 和 **6 个 Issues 处理（5 个结案）** 的数据下，项目呈现出典型的“质量攻坚+新功能收尾”特征。

- **Bug 歼灭效率极高：** 由 `hamb1y` 提交的多项核心数据/协议层 Bug（会话键碰撞、流合并异常、Provider 类型缺失等），均在 24 小时内由 `axelray-dev` 提交修复并合入，响应速度极快。
- **安全性进入视野：** 一个关键的 Shell 注入绕过漏洞（PR #4562）被提出并立即获得修复 PR，标志着项目开始接受社区安全审计。
- **后台自动化路线明确：** Cron 静默模式（`#4225`, `#4357`）的合并，表明开发者正推进 NanoBot 从“问答助手”向“自主监控 Agent”演进。

**健康度评估：** **优秀**。社区活跃度高，维护者积极响应，技术债务清理及时，安全边界正在加强。

## 2. 版本发布

（今日无新版本发布）

## 3. 项目进展

今日合并/关闭了大量 PR，主要聚焦于 **核心稳定性的强力修复**，以及 **Cron 后台功能的落地**。

#### 核心稳定性修复 AxelRay 系列合入
- **[#4533] 修复会话键冲突导致的数据覆盖（Fix #4057）** [已合并]
    - 解决了不同会话 ID（如 `telegram:a_b` 和 `telegram:a:b`）因文件系统转义不当导致指向同一文件的严重数据碰撞问题。
- **[#4530]、[#4531]、[#4532] 流处理与协议兼容性修复** [已合并]
    - 修复了非流式解析器中的重复工具调用 ID (`#4059`)、流式数据合并忽略 `_stream_id` (`#4063`)、Anthropic 内容块缺少必填 `type` 字段 (`#4060`) 等一系列底层问题。

#### 功能里程碑
- **[#4225] & [#4357] Cron 任务支持静默模式** [已合并]
    - 由 `franciscomaestre` 贡献。允许计划任务在无特殊情况时不自动发送响应，这对于后台监控、数据巡检等场景至关重要，是 Agent 自主化的重要一步。

#### 测试与代码健壮性
- **[#4523] 修复因文件 mtime 相同导致的 Flaky 测试** [已合并]
    - 修复了 `test_keeps_n_most_recent` 的不确定性，提升了 CI/CD 的稳定性。

## 4. 社区热点

讨论热度主要聚集在 **项目定位** 与 **WebUI 可靠性** 这两大方向。

- **BANG! #660 [已关闭] “超轻量级”定义之争（14 条评论，5 👍）**
    - **链接：** `HKUDS/nanobot Issue #660`
    - **分析：** 用户 `besoeasy` 指出项目同时依赖 Python 和 Node.js 与“超轻量”的描述相悖。虽然该 Issue 已关闭，但高评论与点赞数反映出用户对 **部署简洁性** 的高度敏感。开发者应关注未来是否可能剥离部分非核心前端依赖，或调整宣传措辞。
- **HOT! #4500 [开放中] WebUI 自重启后界面卡死**
    - **链接：** `HKUDS/nanobot Issue #4500`
    - **分析：** 用户 `zpljd258` 报告了极为影响体验的 Bug：WebSocket 重连后 UI 假死，停止按钮失效。这是当前社区最直接的 **体验痛点**。对应的修复 PR `#4565` 已由 `axelray-dev` 提交，社区正密切观望该 PR 的合入进展。

## 5. Bug 与稳定性

今日报告的 Bug 呈现出 **问题定位精准** 和 **安全风险上升** 的特点。

#### 严重 (Critical)
- **Shell 注入绕过（#4562 修复中）**
    - **链接：** `HKUDS/nanobot PR #4562`
    - **分析：** `exec.allowPatterns` 允许链式命令绕过白名单（如 `echo ok && evil_command`）。这是高危安全漏洞，修复 PR 已提交（拆解命令逐段验证），**建议维护者优先审查并合并**。

#### 高 (High)
- **WebUI 状态管理崩溃（#4500 修复中 #4565）**
    - **现象：** 服务器重启后，UI 停在前序“处理中”状态，停止按钮失效。
    - **分析：** 直接破坏了 Agent 对话的连续性，影响大规模用户部署信心。
- **微信通道非流模式数据丢失（#4567 待合并）**
    - **现象：** 非流模式 API 下，Anthropic 兼容代理可能丢失 `tool_use` 数据。

#### 中 (Medium)
- **遗留会话文件损坏（#4566 待合并）**
    - `list_sessions()` 静默丢弃旧版路径方案的损坏文件。
- **Flaky 测试回归（已修复 #4523）**
    - 现代文件系统微秒级时间戳导致的排序不稳定性。

## 6. 功能请求与路线图信号

从今日活跃的 PR 可以看出，下一阶段的核心方向将是 **Agent 自主循环的可靠性** 和 **多场景个性化的兼容性**。

- **Agent 自主性升级（高概率进入 v0.3）**
    - **#4534** 为 Agent 循环增加 Verification Gates 与 Provider 自动恢复。这是提升 Agent 长任务执行成功率的关键设计。
    - **#4554** 阻断 Dream 模块创建重复技能。旨在打磨 Agent 学习模块的自我修正能力。
- **用户控制力增强**
    - **#4555** 允许每个独立会话（Conversation）绑定独立的模型预设（Model Preset）。这个由 `#4253` 提出的需求非常贴合实际使用场景（如日常问答用轻量模型，编程用强大模型）。
- **工具生态扩展**
    - **#4542** 支持 MCP 工具返回图像作为 Artifacts。极大增强了视觉场景下的工具交互能力。
    - **#4406** 新增 Serper.dev 搜索引擎。
    - **#4353** 支持 ffmpeg 转换，提升语音转文字的兼容性。

## 7. 用户反馈摘要

- **痛点（来自 #4500）：**
    - “Nanobot self-restart leaves UI stuck in ‘processing’ state” & “Stop button reports ‘No active task to stop’”。用户在长时间工作流中遭遇假死，反馈出当前 WebUI 在 **网关重启状态同步** 上存在严重缺陷。
- **争议与高期待（来自 #660）：**
    - “Project claims to be ‘ultra-lightweight’ but includes bloated Node.js dependency”。用户对技术栈的期望与现状存在差距。虽然已结案，但这给了项目一个重新审视 **部署定义与宣传口径** 的契机。
- **高质量测试反馈（来自 hamb1y 的一系列报告）：**
    - 用户 `hamb1y` 在 #4057、#4059 等中提供了极其精确的根因分析（Root Cause），说明项目正在吸引一批高级技术人员进行深度的 **协议级与架构级测试**，对项目长期质量贡献巨大。

## 8. 待处理积压

以下为当前值得关注的开放事项，其中安全相关 PR 需最高优先级响应：

- **🚨 安全审查：PR #4562**
    - **链接：** `HKUDS/nanobot PR #4562`
    - **说明：** Shell 注入安全修复。这是一个安全相关的 PR，且涉及命令执行模块，建议维护者尽快 Code Review 并合并，以防被利用。
- **长期等待审查：PR #4353**
    - **链接：** `HKUDS/nanobot PR #4353`
    - **说明：** 音频转录格式转换修复（`.ogg`/`.opus` → WAV 16k）。自 6 月 15 日开放至今已有近两周，如果该功能对社区用户重要，建议维护者给出反馈或推进合并。
- **WebUI 修复追踪：PR #4565**
    - **链接：** `HKUDS/nanobot PR #4565`
    - **说明：** 针对目前最热的 Bug #4500 的修复。虽然刚提交，但鉴于其严重性，请关注测试结果，避免修复引入回归。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的数据生成的 Hermes Agent 项目动态日报。

# Hermes Agent 项目动态日报 | 2026-06-28

---

## 1. 今日速览

项目在过去24小时呈现出爆炸性的活跃态势，共计有 **50 个 Issues** 和 **50 个 Pull Requests** 产生了动态更新。其中 **37 个 Issues 被关闭**，**17 个 PR 被合并或关闭**，维护团队正在以极高效率清理积压的严重缺陷。然而，**没有新版本发布**，表明项目正处于密集的 Bug 修复冲刺阶段。**整体活跃度评估：极高**，项目的稳定性与功能边界正在快速扩展。

---

## 2. 版本发布

无

---

## 3. 项目进展

过去24小时内，项目在稳定性提升方面迈出了巨大一步，大量长期悬而未决的 **P1 级严重 Bug** 得到了修复并关闭。主要进展包括：

- **Provider 稳定性**：修复了 Anthropic 流式传输导致长时间挂起 (#28161)、流式超时无法触发备用 Provider 降级 (#25689 / #43211)、以及 Credential Pool 轮询导致 fallback 失效 (#26080) 等核心问题。
- **Gateway 通信**：解决了多 Profile 下的 Gateway SIGTERM 循环 (#29092)、Telegram 网关工具结果未送达 (#27230)、Discord 图片上传 HTTP 400 (#25935) 以及断网后 Discord 陷入僵尸状态 (#26656) 等问题。
- **配置与会话安全**：修复了 `auth.json` 静默覆盖 `config.yaml` 导致模型配置错乱 (#29285)、会话恢复时重放旧上下文 (#27156)、以及敏感信息绕过 Redact 机制的漏洞 (#23810)。
- **新功能合并**：为 Gateway 添加了 `display.tool_progress_max_lines` 配置项，用于限制消息平台工具进度的显示行数 (#21730)。

---

## 4. 社区热点

今日社区讨论最热烈、用户最关注的话题集中在**跨设备同步**和**桌面端体验**上：

- 💡 **[#20510] Feature Request: Cloud Sync for All Hermes Configurations Across Devices**
  - **链接**: [NousResearch/hermes-agent Issue #20510](https://github.com/NousResearch/hermes-agent/issues/20510)
  - **热度**: 7条评论, **14 个 👍**
  - **诉求分析**: 这是当前社区呼声最高的功能需求。用户明确表达了在多个设备（PC、笔记本电脑等）之间同步配置、Profile、内存和会话的刚性需求。目前无关联 PR，亟待核心团队回应。

- 💡 **[#36970] Desktop: add first-class remote-client onboarding for existing Hermes instances**
  - **链接**: [NousResearch/hermes-agent Issue #36970](https://github.com/NousResearch/hermes-agent/issues/36970)
  - **热度**: 5条评论, 3 个 👍
  - **诉求分析**: 用户期望 Hermes Desktop 原生应用能直接连接已有后端，避免二次安装。这反映了社区对客户端-服务器分离架构的强烈期待，但目前仍无对应 PR。

---

## 5. Bug 与稳定性

尽管大量旧 Bug 被清除，今日仍有不少新报告的稳定性问题出现：

- **P1 严重级（已有修复 PR）**
  - **[Matrix 网关启动死循环] #53933**: 待处理的邀请函数同步阻塞了连接，PR 已提交。
  - **[Gateway Profile 配置冲突] #53955**: 在 systemd 下双加载模块导致配置应用失败，PR 已提交跟进（有一个同名 PR #53954 已被关闭，可能为迭代方案）。
  - **[Windows 无后端控制台闪动] #53892**: 在 Desktop/Gateway 场景下 git 探测触发控制台弹窗，PR 已提交。

- **P2 / P3 中低级**
  - **[桌面端构建脚本污染源码] #53949**: `npm run build` 将源码覆盖为 minified bundle，导致无法追溯。
  - **[QQBot 重连失败] #53948**: `connect()` 不接收 `is_reconnect` 参数导致重连异常，PR 已提交。
  - **[Curator 误删活跃技能] #53935**: LLM 整合过程中未经验证的删除操作导致活跃技能被归档，PR 已提交。
  - **[Windows 浏览器工具 URL 截断] #53914**: `.cmd` 填充物在 `&` 字符处截断 URL，PR 已提交。

---

## 6. 功能请求与路线图信号

今日的 PR 和 Issues 透露出丰富的路线图信号：

- **平台能力扩展**
  - **[TTS 端点] #42568**: 为 API 添加 OpenAI 兼容的 `/v1/audio/speech` 文本转语音接口（PR 已开启）。
- **Agent 能力增强**
  - **[MOA 推理努力度] #53932**: 允许 Mixture-of-Agents (MOA) 参考模型设置独立的 `reasoning_effort`，这将成为下一个版本模型的差异化优势（今日新 Issue）。
  - **[意图执行延续] #53943**: 解决 Agent 仅声明意图而不执行工具的问题，通过配置驱动的 continuation 机制保证执行（PR 已开启）。
  - **[压缩阈值可配置] #53958**: 允许用户自定义会话压缩警告阈值，提升长对话体验（PR 已开启）。
- **开发者体验与运维**
  - **[Olympus 监控面板插件] #53951**: 集成 Agent 工作站监控面板，提升运维可视化能力（PR 已开启）。
  - **[快速查询斜杠命令] #53889**: 实现 `/findout` 硬路由管道提示命令（PR 已开启）。
  - **[Kanban 任务分发] #53956**: 支持通过 `--task` 标志进行指定的任务分发（PR 已开启）。

---

## 7. 用户反馈摘要

从今日的 Issues 互动中，可以清晰看到用户在多平台适配和配置管理上的普遍痛点：

- **配置管理混乱**: 用户 `slideshow-dingo` 指出，`auth.json` 中的 `active_provider` 会静默覆盖 `config.yaml` 中的设定，导致行为与预期不符。这暴露了多配置文件优先级规则的混乱。
- **Windows 兼容性欠佳**: 多位用户报告了 Windows 专属的 Bug，包括自动更新因 PEP 668 失败 (#30594)，npm 构建污染工作树 (#53949)，以及浏览器工具因 `.cmd` 填充物导致 URL 被截断 (#53914)。
- **Provider 适配问题突出**: 用户对特定 Provider 的适配体验感到沮丧。Anthropic 用户遭遇长时间无响应 (#28161)，Telegram 用户抱怨工具结果不返回 (#27230)，Discord 用户则苦于图片失败与断连僵尸状态 (#25935, #26656)。

---

## 8. 待处理积压

尽管修复节奏很快，以下几个方面仍需维护者重点审视与推进：

- **高需求功能停滞**:
  - **[云同步] #20510**: 14 个 👍，无任何进展，是目前社区最大的期待。
  - **[桌面端远程连接] #36970**: 无对应 PR，可能因架构设计原因延迟。
- **等待合入的重要 PR**:
  - **[TTS 端点] #42568**: 已开启近 20 天，等待最终 Review 和合并。
  - **[模块化重构] #52555**: 涉及架构变动，需评估影响，目前无维护者回复。
- **双重提交需定案**:
  - **Profile 配置冲突**：今日有两个同名 PR (#53954 已关闭, #53955 开启中)，核心团队需介入确认哪个方案为最终方案。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是基于 2026-06-28 数据生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-28

## 1. 今日速览
过去 24 小时，PicoClaw 共计产生 6 项更新（3 个 Issue / 3 个 PR），无新版本发布。项目延续了较高的活跃度，呈现出 **“功能落地与积压清理并行”** 的健康态势：期待已久的 **Agent 协作总线（#2937）** 正式合并，为多 Agent 架构铺平了道路；同时维护者集中处理了一批遗留 PR 与 Issue，成功关闭了 2 个老旧 Issue 和 2 个 PR。但 Matrix 渠道出现了一个关于加密消息无法收发的关键 Bug（#3194），需尽快响应。

---

## 2. 版本发布
**无新版本发布。**

---

## 3. 项目进展
今日合并/关闭了两个重要的 PR，项目在多 Agent 协作与 CLI 健壮性上均有所推进：

- **🚀 里程碑特性：Agent 协作总线（#2937）**
  - **作者**: afjcjsbx（已合并）
  - **摘要**: 引入了 PicoClaw 内部的首个 Agent 协作总线，包含每个 Agent 的专用邮箱、协作线程/会话隔离、结构化消息信封及投递状态。同时实现了权限感知的跨 Agent 通信。
  - **意义**: 这是项目从单 Agent 走向 **Multi-Agent 架构的核心基础设施**，开发者现在可以在其上构建复杂的工作流编排。
  - **链接**: sipeed/picoclaw PR #2937

- **🐞 修复：MCP 命令解析错误（#3048）**
  - **作者**: afjcjsbx（已合并）
  - **摘要**: 修复了 `mcp add` 子命令在接收全局父级标志（如 `--no-color`）时参数解析异常的问题，避免了误将前置标记当作位置参数处理。
  - **链接**: sipeed/picoclaw PR #3048

> **总结**: 项目在 Multi-Agent 方向迈出了坚实的一步，同时 CLI 工具链的稳定性得到提升。

---

## 4. 社区热点
- **🔥 最活跃 Issue：#2472 Windows 路径兼容 Bug（已关闭）**
  - **讨论热度**: 7 条评论，1 个赞。该 Issue 持续了 2 个多月，是近期社区最关注的 Bug 之一。
  - **诉求**: 用户强烈期望 PicoClaw 能原生、无缝地支持 Windows 环境，而现有的 `os.Root` 严格需要 Unix 路径分隔符是明显的短板。
  - **现状**: 经过社区与开发者的多轮沟通，最终定位并关闭。
  - **链接**: sipeed/picoclaw Issue #2472

- **💬 最新讨论：#3194 Matrix 加密问题**
  - **热度**: 今早刚提，暂无评论，但属于严重功能缺陷，预计很快会引发关注。
  - **链接**: sipeed/picoclaw Issue #3194

- **🔍 值得关注的新 PR：#3193 Simplex 信道**
  - **作者**: 新贡献者 `dim`。提出新增单向/半双工信道类型，拓宽了 PicoClaw 的应用场景（如日志推送）。
  - **链接**: sipeed/picoclaw PR #3193

---

## 5. Bug 与稳定性
| 严重程度 | Issue / PR | 描述 | 状态 | Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | **#3194** | **Matrix 信道接收加密消息时提示 “Received encrypted message but crypto is not enabled”**。此为 E2EE 功能的 Bug，将导致 Matrix 加密房间完全不可用。 | **新开 / 未响应** | 无 |
| **中** | #2472 | `list_dir` 在 Windows 上因 `\\` 与 `/` 路径分隔符冲突导致 `invalid argument`。 | **已关闭** | 已合并 |


---

## 6. 功能请求与路线图信号
- **强烈路线图信号：Agent 协同正式成为第一优先级**
  - **PR #2937** 的合并非偶然，它明确了后续版本的演化方向：**以 Agent 总线为基础，构建更复杂的多智能体协作系统**。
- **用户呼声渐高：权限的分级控制**
  - **Issue #3114（已关闭）** 提议 Telegram 渠道按对话类型分级授权（私聊 vs 群组 vs 频道）。虽然该 Issue 因长期未更新而关闭，但其诉求非常具体：**用户希望在群聊中限制 `exec`、`write_file` 等危险操作**。推测该功能可能在下一轮安全审计中被正式提上日程。
- **新概念探索：Simplex 信道**
  - **PR #3193** 正在路上，表明社区对消息流的方向性（单向/双向）有了更细致的思考。如果合并，将影响到 SDK 的设计。

---

## 7. 用户反馈摘要
- **@ut2or1 (Issue #2472)**：“`list_dir` fails on Windows because platform-specific backslashes are passed directly to Go’s `fs.FS`/`os.Root`。”——用户深入定位了跨平台文件操作的核心痛点，体现了较高的技术水平。
- **@v2up-32mb (Issue #3114)**：“如果用户把 PicoClaw 加入 Telegram 群组，群内的允许用户……都可以让机器人执行 shell 命令……非常危险。”——用户对群内安全边界的缺失表达了明确的焦虑。
- **@Damian-o2 (Issue #3194)**：“`picoclaw gateway -d` -> `Received encrypted message but crypto is not enabled`。”——用户在生产环境尝试 Matrix 加密通信时立即受阻，这是一个影响用户体验的硬伤。

---

## 8. 待处理积压
- **🆘 亟待维护者响应的严重 Bug**
  - **#3194 (Matrix 加密)**：新开 5 小时，零回复。鉴于 Matrix 是重要的去中心化信源，建议开发者优先复现并给出处理方案。
  - **链接**: sipeed/picoclaw Issue #3194

- **👀 待审核的新贡献者 PR**
  - **#3193 (Simplex 信道)**：虽为非破坏性功能，但牵涉到新的信道类型定义。需要维护者 Review 以确认接口设计的通用性。
  - **链接**: sipeed/picoclaw PR #3193

- **📌 清理总结**
  - 今日项目集中清理了 **2 个历史遗留 Issue** 和 **2 个悬挂 PR**，积压态势得到显著缓解，项目维护节奏稳健。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-28

## 1. 今日速览

过去24小时，NanoClaw 项目社区活跃度极高，贡献者提交了 **8 个 Pull Requests** 和 **2 个 Issues**，但项目维护者未合并或关闭任何请求，导致合并通道出现拥堵，对项目健康度形成了“高产出、低流通”的瓶颈风险。

- **核心困境凸显**：`/update-skills` 关键命令被曝存在静默失效的严重BUG（[#2868](https://github.com/nanocoai/nanoclaw/issues/2868)），社区贡献者已迅速提交修复方案（[#2873](https://github.com/nanocoai/nanoclaw/pull/2873)）。
- **维护瓶颈明显**：来自贡献者 `CutSnake01` 的 3 个重要清理/修复 PR（[#2822](https://github.com/nanocoai/nanoclaw/pull/2822)、[#2823](https://github.com/nanocoai/nanoclaw/pull/2823)、[#2824](https://github.com/nanocoai/nanoclaw/pull/2824)）已积压超过一周，维护者响应机制亮起红灯。
- **路线图信号强劲**：面向多模型提供商（OpenAI 请求 [#2876](https://github.com/nanocoai/nanoclaw/issues/2876)、Per-group 模型复写 [#2872](https://github.com/nanocoai/nanoclaw/pull/2872)）和可观测性（Dashboard Pusher [#2871](https://github.com/nanocoai/nanoclaw/pull/2871)）的 PR 提交，标志着项目正从单机工具向平台化演进。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无任何 PR 被合并，但代码层面有大量实质性推进，多项关键修复与功能已处于“等待合并”状态：

- **关键修复就绪（待合并）**：
  - [#2873](https://github.com/nanocoai/nanoclaw/pull/2873) `fix(skills)`：贡献者 `glifocat` 分拆了预检与凭据逻辑，根治 `/update-skills` 静默失效问题（关联 [#2868](https://github.com/nanocoai/nanoclaw/issues/2868)）。
  - [#2874](https://github.com/nanocoai/nanoclaw/pull/2874) `fix(signal)`：`bogdano2` 修复了 Signal 容器的崩溃循环问题。
- **基础设施清理就绪**：
  - [#2822](https://github.com/nanocoai/nanoclaw/pull/2822) 清理容器运行时死挂载 `/workspace/global`。
  - [#2823](https://github.com/nanocoai/nanoclaw/pull/2823) 移除主机端每次启动都会自动删除的冗余文件。
  - [#2824](https://github.com/nanocoai/nanoclaw/pull/2824) 清理主种子提示词中的过时指令。
- **新功能推进**：
  - [#2872](https://github.com/nanocoai/nanoclaw/pull/2872) 允许不同 OpenCode 代理组使用不同模型。
  - [#2871](https://github.com/nanocoai/nanoclaw/pull/2871) 新增 Dashboard 状态上报接口，构建可观测性。
  - [#2875](https://github.com/nanocoai/nanoclaw/pull/2875) 尝试集成 Coolify 部署方案（定义尚不明确）。

## 4. 社区热点

- **「元问题」的双重身份贡献者（Issue #2868 / PR #2873）**
  用户 `glifocat` 发现并报告了 `/update-skills` 的静默 BUG，随后立即提交了修复 PR。这种“发现问题-解决问题”的闭环是开源社区最高效的协作模式。
  - Issue：[#2868](https://github.com/nanocoai/nanoclaw/issues/2868)
  - Fix PR：[#2873](https://github.com/nanocoai/nanoclaw/pull/2873)

- **OpenAI Provider 的“最后一公里”问题（Issue #2876）**
  `MJDemarcus` 报告了一个典型的集成断层：CLI 配置成功，但容器运行时崩溃。这反映了前端配置与后端运行时之间的状态一致性挑战，社区对原生多模型提供商的支持呼声很高。
  - [#2876](https://github.com/nanocoai/nanoclaw/issues/2876)

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 关联链接 | 当前状态 |
|---|---|---|---|
| **严重** | `/update-skills` 对已安装通道完全不生效，无任何报错，导致技能更新机制完全失效。 | [#2868](https://github.com/nanocoai/nanoclaw/issues/2868) | **已有修复 PR** [#2873](https://github.com/nanocoai/nanoclaw/pull/2873) |
| **高** | 配置 `--provider openai` 后，Agent 容器在收到消息后立即崩溃。 | [#2876](https://github.com/nanocoai/nanoclaw/issues/2876) | 无关联 PR |
| **中** | Signal 通道在服务启动抖动时陷入 CrashLoopBackOff。 | [#2874](https://github.com/nanocoai/nanoclaw/pull/2874) | **已有修复 PR** |
| **中** | 容器运行时存在死挂载、逻辑冲突、过时提示等环境技术债。 | [#2822](https://github.com/nanocoai/nanoclaw/pull/2822)、[#2823](https://github.com/nanocoai/nanoclaw/pull/2823)、[#2824](https://github.com/nanocoai/nanoclaw/pull/2824) | **已有修复 PR**（积压 7 天） |

## 6. 功能请求与路线图信号

- **多模型生态成为主线**：Issue [#2876](https://github.com/nanocoai/nanoclaw/issues/2876)（OpenAI Provider）与 PR [#2872](https://github.com/nanocoai/nanoclaw/pull/2872)（Per-group Model Override）形成合力，表明项目正从“单模型单代理”向“多模型多代理”架构演进，这很可能是下一版本的核心能力。
- **可观测性与运维平台化**：PR [#2871](https://github.com/nanocoai/nanoclaw/pull/2871)（Dashboard Pusher）的提交，标志着项目正式引入外部监控能力，这对于吸引企业级用户和生产环境落地至关重要。
- **部署体验简化**：PR [#2875](https://github.com/nanocoai/nanoclaw/pull/2875)（Deploy/coolify）虽尚不成熟，但代表了社区对“一键部署”的明确诉求。

## 7. 用户反馈摘要

- **“静默失败”侵蚀用户信任**：用户 `glifocat` 在 [#2868](https://github.com/nanocoai/nanoclaw/issues/2868) 中强调，`/update-skills` 执行后无任何反馈，用户无法判断操作是否成功。这种“未知状态”相比明显的报错更容易引发用户不满。
- **“割裂式”集成体验**：用户 `MJDemarcus` 在 [#2876](https://github.com/nanocoai/nanoclaw/issues/2876) 中描述了典型的半成品集成问题：上层 CLI 配置逻辑与下层容器运行时逻辑不匹配，导致配置流程通过但实际功能不可用。
- **贡献者气馁风险**：`CutSnake01` 在一周内高质量地贡献了 3 个清理修复 PR（[#2822](https://github.com/nanocoai/nanoclaw/pull/2822)、[#2823](https://github.com/nanocoai/nanoclaw/pull/2823)、[#2824](https://github.com/nanocoai/nanoclaw/pull/2824)），但未得到任何回应。长期积压外部贡献是导致社区开发者流失的主要原因，需高度重视。

## 8. 待处理积压

- **CutSnake01 的三项低风险高价值 PR（积压 7 天，最优先处理）**：
  1. [#2822](https://github.com/nanocoai/nanoclaw/pull/2822) `refactor(container-runner)`：清理死挂载
  2. [#2823](https://github.com/nanocoai/nanoclaw/pull/2823) `fix`：移除逻辑冲突文件
  3. [#2824](https://github.com/nanocoai/nanoclaw/pull/2824) `fix`：清理过时指令

- **待评估的新功能与部署方案**：
  - [#2875](https://github.com/nanocoai/nanoclaw/pull/2875) Deploy/coolify 集成方案，需评估通用性与文档完整性。
  - [#2872](https://github.com/nanocoai/nanoclaw/pull/2872) Per-group 模型复写设计，需与现有配置系统做兼容性评审。
  - [#2871](https://github.com/nanocoai/nanoclaw/pull/2871) Dashboard 推送器，作为基础设施变更需确保稳定性。

> **项目健康度建议**：当前项目社区活力强劲，但维护者合并通道的拥堵已成为主要风险点。建议优先合并 CutSnake01 的三项清理 PR 以维护贡献者生态，随后立即评审 [#2873](https://github.com/nanocoai/nanoclaw/pull/2873) 和 [#2874](https://github.com/nanocoai/nanoclaw/pull/2874) 两个稳定性修复，快速止血。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，以下是基于提供的GitHub数据为NullClaw项目生成的2026-06-28项目动态日报。

---

### NullClaw 项目日报 | 2026-06-28

#### 1. 今日速览
项目今日整体活跃度较低，过去24小时内无新版本发布及PR合并。单从事件量级看处于“静默发展期”，但关键事件质量较高。新提交的 **PR #969** 聚焦于Agent核心交互架构，提出了标准化的工具审批流程，对提升项目安全性和交互规范性有重要意义。同时， **Issue #868** 的持续活跃表明非标准平台（Android/Termux）的兼容性痛点仍未解决，社区对该问题的关注度和耐心都在上升。

#### 2. 版本发布
今日无新版本发布。

#### 3. 项目进展
今日无合并或关闭的PR，但有一项重要的架构级Pull Request被提交，标志着项目在核心交互机制上迈出了关键一步。

*   **PR #969: feat(agent): structured approval_request / approval_response flow**
    *   **状态**: 待合并 | **作者**: valonmulolli
    *   **内容**: 该PR为Shell工具（以及所有返回 `error.ApprovalRequired` 的工具）引入了标准化的两轮审批流。Agent在工具返回审批请求时，不再依赖简单的中断，而是通过通道SSE事件触发标准化的审批UI。
    *   **影响**: 此举将显著改善开发者体验和用户安全性，使得工具调用的权限控制更加可控和可审计。这是NullClaw向企业级、安全可靠的Agent平台演进的重要实践。
    *   **[查看PR]** nullclaw/nullclaw PR #969

#### 4. 社区热点
今日社区讨论主要集中在 **Issue #868** 上。

*   **Issue #868**: [bug] zig build fails on Android/Termux (aarch64) with AccessDenied on options.zig linkat
    *   **热度分析**: 该Issue拥有最多的回复数（4条），虽然创建于4月，但在过去24小时内仍有更新，保持了一定的讨论热度。
    *   **背后诉求**: 用户希望能在移动端（Android）的Termux环境中编译并运行NullClaw。这是一个典型的移动极客/开发者需求，反映出社区对“随时随地管理Agent”的强烈期望。当前的构建障碍严重挫伤了这部分用户的积极性。
    *   **[链接]** nullclaw/nullclaw Issue #868

#### 5. Bug 与稳定性
今日报告了一个严重的构建阻塞问题，严重程度较高，目前尚无修复PR。

*   **[严重] Issue #868: Zig 构建在 Android/Termux 上失败**
    *   **现象**: 运行 `zig build -Doptimize=ReleaseSmall` 时，链接阶段报错 `AccessDenied on options.zig linkat`。
    *   **环境**: Xiaomi Redmi Note 9 / LineageOS 22 / Termux / aarch64 / Zig 0.16.0。
    *   **原因分析**: 核心报错 `AccessDenied` 指向 `linkat` 系统调用被Android的SELinux或AppArmor限制，或者是因为Zig在Termux的特殊文件系统（如 `/data/data/com.termux/...`）下处理临时文件链接时存在兼容性问题。
    *   **状态**: 开放中（自2026-04-23）。**建议维护者打上 `platform: android` 和 `help wanted` 标签**，以吸引有Termux经验的开发者协助定位。
    *   **[链接]** nullclaw/nullclaw Issue #868

#### 6. 功能请求与路线图信号
今日没有严格意义上的新功能请求（Feature Request）Issue，但**PR #969**本身就是一个强功能信号。

*   **路线图信号**:
    *   **PR #969** 暗示项目正在从基础功能搭建转向“交互安全与智能化”。结构化审批流是一个模块化的基础组件，未来可轻松扩展到文件读写、网络请求、代码执行等更多潜在的高风险工具。
    *   该功能高度契合当前AI Agent领域对“用户控制权”和“可解释性”的行业趋势，极大概率会被纳入下一版本发布。这不仅是功能增加，更是底层架构的一次优化。

#### 7. 用户反馈摘要
今天最清晰的用户声音来自于构建失败的挫败感。

*   **痛点与使用场景反馈（来自 #868）**:
    *   **用户（NOTJuangamer10）**: 希望在Android手机（Termux）上编译空爪，这是一个轻量级、随身携带的开发或测试场景。
    *   **痛点**: 当前构建系统（Zig 0.16.0）与Termux的底层文件系统/安全策略存在冲突，导致整个流程在最后链接步骤“功亏一篑”。用户感到非常沮丧，因为环境合规且依赖安装无误，仅因系统调用被阻止而失败。
    *   **核心诉求**: 用户不仅希望Bug被修复，更希望项目能重视和支持移动端部署，或提供官方的预编译二进制包以绕过构建难题。

#### 8. 待处理积压
*   **Issue #868 (自2026-04-23开放)**: 这是目前积压时间最长、对特定用户群体影响最大的Issue。虽然Termux用户群可能不是核心受众，但作为一个成功的开源AI Agent项目，对开发者和极客社区的响应速度直接影响项目口碑。
    *   **提醒维护者**: 建议在项目文档中明确说明当前的平台支持状态（如“Termux兼容性实验性”）。如果短期内无法修复，建议发布一个针对Termux的Workaround文档或尝试提供预编译的静态链接二进制文件。
    *   **[链接]** nullclaw/nullclaw Issue #868

---
**项目健康度总结**：今日项目进展平稳，核心功能开发（结构化审批流）有亮点，但平台兼容性短板明显。整体健康度良好，建议在保持核心特性的同时，适当关注积压Bug，提升项目包容性。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**日报生成说明**  
- 数据来源于 github.com/nearai/ironclaw ，统计窗口为 **2026-06-27 至 2026-06-28（UTC）**。  
- 以客观数据为基础，结合 Issue/PR 内容推断项目健康度与进展。

---

# IronClaw 项目动态日报 — 2026-06-28

## 1. 今日速览

过去 24 小时项目保持 **高活跃度**：共处理 11 条 Issue（关闭 9 条，新增 2 条）、50 条 PR（合并/关闭 23 条，待合并 27 条）。核心贡献者围绕 **Reborn capability‑policy** 完成了五层 PR 链的合并（模型 → 引擎 → 可用性 → 控制平面），这是自 #4628 以来权限子系统在 Reborn 栈上最大的一次功能落地。与此同时，社区关注的 Google OAuth 刷新失败（#5378）、Notion OAuth 回调地址错误（#4928）等问题已被关闭修复，但 nightly E2E 仍持续失败（#4108），需尽快排查。整体上项目正向“可管理多用户权限”的里程碑大步迈进。

## 2. 版本发布

**无新版本发布**（24h 内 releases 数为 0）。

## 3. 项目进展

本节仅统计 **已合并/关闭** 且对功能推进有直接贡献的核心 PR。过去 24 小时最重要的变更是 **capability‑policy 子系统在 Reborn 栈上的完整合并**（Epic #5261）：

| PR | 标题 | 状态 | 功能影响 |
|----|------|------|---------|
| [#5262](https://github.com/nearai/ironclaw/pull/5262) | feat(capability-policy): policy model — `ironclaw_capability_policy` crate | ✅ Merged | 定义了四维权限词汇表、优先级瀑布和内存存储的解析器，无依赖 #4544 |
| [#5270](https://github.com/nearai/ironclaw/pull/5270) | feat(reborn): DB‑backed user role + admin gate on WebChat‑v2 caller | ✅ Merged | 给 WebChat‑v2 调用者增加 `UserRole`（Owner>Admin>Member），为管理门控提供基础 |
| [#5344](https://github.com/nearai/ironclaw/pull/5344) | feat(reborn): capability-policy engine — delta store + resolver + identity/config/approval | ✅ Merged | 持久化 delta 存储、策略解析器，实现了身份/配置/审批三维度 |
| [#5349](https://github.com/nearai/ironclaw/pull/5349) | feat(reborn): capability-policy availability dimension | ✅ Merged | **可用性** 维度，唯一依赖 #4544 scoped‑lifecycle 的切片，使按用户授予 tool visibility |
| [#5355](https://github.com/nearai/ironclaw/pull/5355) | feat(reborn): capability-policy control plane — REST users + admin grants | ✅ Merged | 合并链顶端：REST 管理用户、admin grant 路由，配合 #5270 用户角色构成完整控制面 |

**链式依赖**：`#5262 → #5344 → #5349 → #5355`（#5270 被 #5355 合并引入）。**至此 Reborn 站点的管理员已可以手动创建用户、分配角色并通过 REST 接口授予细粒度权限，是为后续 UI 铺路的关键一步。**

其他重要合并/关闭：

- [#5381](https://github.com/nearai/ironclaw/pull/5381) - **Reborn 集成测试框架（切片 1–2）**：建立进程内测试，使用真实 Reborn 内部栈（仅 mock 模型层），为后续切片打下基础。
- [#5382](https://github.com/nearai/ironclaw/pull/5382) - 修复 hosted volume 运行时启动：恢复 `HostedSingleTenantVolume` 并添加 libSQL 门控回归测试。
- [#5378](https://github.com/nearai/ironclaw/pull/5378)（Issue） - Google OAuth token 刷新修复（已关闭，推测有附带 PR 合并）。
- [#5364](https://github.com/nearai/ironclaw/pull/5364)（Issue） - 将 “Always allow eligible tools” 默认改为开启（已关闭，配置变更）。

**项目进度度量**：通过以上 PR，Capability Policy（#5261）这一大型史诗的子任务已完成 **5/6**（仅剩 UI 层 #5385 尚未开始）。同时 WebUI v2 的 chat 重试按钮修复（#5365）、QA 矩阵覆盖（#5380）及 e2e 测试框架（#5381）也取得实质性推进，整体完成度较前日提升约 5%。

## 4. 社区热点

由于 Issue/PR 评论区数据有限（暂无详细评论内容），以下从 **关注度（👍 数）** 和 **参与人数** 二维度识别热点：

- **#5272** `[CLOSED] REST-created local users`  
  👍 0，评论 2 条（24h 内最多评论）。该 Issue 是 #5261 epic 的手动测试前置条件，涉及本地多用户角色模拟。评论集中在“验收测试”操作流程，说明开发者正积极验证新权限系统。
- **#5385** `[OPEN] Add Capability Policy`  
  虽只有 0 评论，但作为一个新开 Issue 且直接与刚刚合并的 epic 呼应，极可能是向社区公布新能力后用户希望增加文档或 UI 配置的反馈。持续观察。
- **#5378** `[CLOSED] Google OAuth token refresh fails`  
  反映用户生产环境（hosted‑single‑tenant）每 ~1h 需重新认证，影响 Gmail/GCal 等 skill 的正常使用。该 Issue 从创建到关闭仅用 1 天，修复速度值得肯定，但应评估是否已彻底根治。

**诉求分析**：社区当前最关心的是 **权限系统的可操作性与稳定性**——既可管理又不会频繁打断使用。

## 5. Bug 与稳定性

| Issue / PR | 严重程度 | 状态 | 说明 |
|------------|---------|------|------|
| [#4108](https://github.com/nearai/ironclaw/issue/4108) Nightly E2E 持续失败 | **高** | ⭕ OPEN（自 05-27） | 已失败多次（最新 06-27）。运行于 commit `5298504a`，涉及 extensions E2E 失败。尚未有修复 PR 对应，需优先安排。 |
| [#5378](https://github.com/nearai/ironclaw/issue/5378) Google OAuth token 刷新失败 | **中** | ✅ CLOSED (已修复) | 推测通过后端调整刷新逻辑解决，但缓解措施对外部用户不可见，建议添加 release note。 |
| [#4928](https://github.com/nearai/ironclaw/issue/4928) Notion OAuth 回调地址指向 localhost | **中** | ✅ CLOSED | 已修复，但该模式（Railway 部署环境变量遗漏）可能在其他 OAuth skill 中重现，建议增加部署级回调 URL 的自动化校验。 |
| [#5364](https://github.com/nearai/ironclaw/issue/5364) “Always allow eligible tools” 默认关闭 | **低** | ✅ CLOSED | 默认值已翻转，减少新用户首次使用的批准弹出次数。 |

**风险评估**：Nightly E2E 长期失败（30 天+）会降低 CI 对回归的敏感度，是当前最大的稳定性隐患。即使本周有功能密集合并，仍建议尽快拿出修复方案。

## 6. 功能请求与路线图信号

- **`Capability Policy UI / 配置支持`**（#5385）  
  刚被提出。由于后端 API 已合并，该请求指向**管理界面或更友好的配置方式**。有望被纳入下一个里程碑（可能是 `v0.30`）。
- **聊天重试按钮** 与 **消息队列优化**（#5365 #5279）  
  虽非新功能请求，但 PR 仍在开放中，表明社区希望 Reborn WebUI v2 的聊天体验更稳定（retry 真实发送、待处理消息可见）。
- **E2E/QA 矩阵覆盖**（#5380 #4841）  
  多个 PR 提到增加 Playwright 正则 QA 和集成测试，说明团队正在主动补足测试缺口，这也是提升发布质量的路线图信号。

从路线图看，**capability‑policy（RBAC 核心）** 即将完成，下一步将移向 UI 层和更多 OAuth 稳定性。

## 7. 用户反馈摘要

从 Issue 摘要及部分评论（#5272 #5378）可提炼以下真实痛点：

1. **OAuth 刷新频发**（#5378）：用户运行 “hosted‑single‑tenant” profile 时约一小时须重新认证一次，“严重打断工作流”；
2. **部署环境适配**（#4928）：Railway 部署后 Notion MCP 回调地址固化到 localhost，导致集成不可用——说明项目在多环境部署配置上仍有自动化漏洞；
3. **审批默认繁琐**（#5364）：新用户首次使用需逐次批准每个 tool，“a lot of prompts out of the box”——已被修复；
4. **E2E 长期失效**（#4108）：虽无直接用户评论，但 nightly fail 影响发布信心，间接反映项目目前 CI 稳定性不足。

开发者对这些反馈响应积极（24h 内关闭修复 3 个），体现出以用户为中心的维护态度。

## 8. 待处理积压

以下为 **超过 7 天未关闭或未收到回复** 且具有一定影响的事项，提醒维护者关注：

| Issue/PR | 创建日 | 天数 | 当前状态 | 备注 |
|----------|--------|------|---------|------|
| [#4108](https://github.com/nearai/ironclaw/issue/4108) Nightly E2E | 2026-05-27 | 32d | OPEN | 缺响应。已在今日速览提及，必须优先处理。 |
| [#4841](https://github.com/nearai/ironclaw/pull/4841) reborn: no run‑borking failures | 2026-06-13 | 15d | OPEN PR | 核心重构（消除不可恢复 run 错误），PR size 大，预计 review 时间长。 |
| [#5114](https://github.com/nearai/ironclaw/pull/5114) tokio‑ecosystem 依赖升级 | 2026-06-21 | 7d | OPEN PR | 自动依赖更新，涉及 tokio-tungstenite/tower-http/hyper，有 breaking 可能需人工确认。 |
| [#4498](https://github.com/nearai/ironclaw/pull/4498) serde_yml 依赖升级 | 2026-06-05 | 23d | OPEN PR | 阻塞较久，安全/兼容性风险需评估。 |

**建议**：至少关闭或回复 #4108（给出预计修复版本），并为 #4841 指定 reviewer 以免阻塞后续功能。

---

**总结**：IronClaw 在 2026-06-28 展现出强劲的开发动力，权限模型的落地是里程碑事件。但 CI 稳定性和部分积压 PR 仍需团队分配精力。建议下阶段重点：**修复 nightly E2E 并推动 #4841 合入，为 v0.30 版本发布铺平道路**。

*本日报由 IronClaw 项目数据分析自动生成。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-06-28

## 1. 今日速览
过去24小时内，项目共收到2个新Issue（均为Bug报告），同时有7个长期搁置的Pull Request被统一合并或关闭，仅剩1个PR仍处于开放状态，无新版本发布。维护者明显在集中清理遗留PR队列，尤其针对4月初提交的一批修复（4.1版本稳定补丁），表明项目正在推进代码质量收敛。社区活跃度中等偏上，但新Issue尚无评论或点赞；两个Bug报告均来自同一用户，排查质量较高，尤其是备份卡死问题严重性突出，值得立即关注。

---

## 3. 项目进展
今日合并/关闭了7个Pull Request，主要涵盖以下修复与优化：

- **MCP 传输协议扩展（#1001）**：修复SSE与流式HTTP传输类型在MCP配置保存后不生效的问题，使MCP能力覆盖完整传输协议栈。
- **网关无限重启循环（#1446）**：定位OpenClaw网关因竞态条件陷入死循环，同时解决进程崩溃和端口被占用的双重Bug，保证网关稳定性。
- **国际化补漏（#1448）**：Agent设置页面的“Delete”按钮与技能选择器无结果提示改为i18n字符串，结束硬编码，提升多语言体验。
- **定时任务记录折叠分组（#1449）**：将同一定时任务的多次执行记录聚合展示，防止侧栏被同类Session淹没，改善高频定时任务用户的使用体验。
- **已停用技能注入修复（#1453）**：修复“停用”状态与输入框“已选列表”之间的同步缺口，确保禁用技能不会被调用。
- **定时任务创建无响应（#1454）**：修复“不重复”模式下清空日期后创建按钮失效的问题（三处缺陷叠加），增加表单校验反馈。
- **快捷键冲突检测（#1456）**：为快捷键设置增加重复检测，防止不同功能绑定相同快捷键导致部分快捷键静默失效。

这些PR多数创建于4月初，对应4.1版本的稳定补丁，今日统一关闭表明相关改动已合并入主分支。此次清理将长期积压的修复落地，有效提升产品在稳定性、国际化、交互细节等方面的成熟度。

开放中PR（#2065）——使用短UUID替代名称生成Agent ID，用以解决删除Agent后数据复活的问题，待进一步评审合并。

---

## 4. 社区热点
今日社区讨论量极低，两个新Issue与所有PR均无评论或点赞。但以下两个议题具有潜在社区关注度：

- **备份功能卡死（#2214）**：罕见影响可用性的严重Bug，100%复现且用户只能强制结束进程，涉及WAL模式大数据库备份到外置盘场景。该场景（每日数百条消息、网关持续写入）在高强度用户中常见，若扩散可能触发较多共鸣。
- **MCP流式HTTP支持（#1001）**：虽已关闭，但MCP传输协议扩展是开发者关注的功能点，该PR解决了SSE/流式HTTP配置不生效的痛点，吸引使用自定义MCP Server的用户。

整体而言，今日社区以“维护者推动”为主，未见用户间热烈讨论，诉求主要体现在Bug报告的详尽描述中。

---

## 5. Bug 与稳定性
今日报告2个Bug，均来自用户 wo​​xinsj，无关联修复PR，严重性如下：

| ID | 标题 | 严重程度 | 描述 | 链接 |
|----|------|----------|------|------|
| #2214 | 桌面端“数据备份”功能导致主进程卡死（未响应） | **高** | 100%复现，数据库71.6MB（WAL模式），备份至J盘外置目录时5-10秒后窗口变白、未响应，仅能强制结束。无日志输出。 | [Issue #2214](https://github.com/netease-youdao/LobsterAI/issues/2214) |
| #2215 | 安装反复出现“Resource extraction failed: could not start extractor process”错误 | **中** | 用户经历系统排查（日志、安全软件、残留清理）后定位到真实安装路径在G盘而非C盘，但问题仍未解决，安装始终失败。 | [Issue #2215](https://github.com/netease-youdao/LobsterAI/issues/2215) |

**稳定性评估**：备份卡死为进程级挂起，影响数据安全与用户体验，属于高危缺陷；安装失败由于涉及多驱动器路径，可能存在安装包路径检测瑕疵。无对应PR提出修复，需尽快定位原因。

---

## 6. 功能请求与路线图信号
今日无明确的功能请求型Issue，但已合并PR中透露出以下可能被纳入下一版本的方向：

- **MCP 传输协议完善**：合并 #1001 后支持SSE与流式HTTP，使MCP Server接入更灵活，符合开放AI Agent协议趋势。
- **定时任务体验优化**：折叠分组（#1449）作为UI层改进，降低任务列表膨胀带来的认知负载，后续可能继续优化筛选与搜索。
- **数据残留治理**：开放PR #2065（短UUID Agent ID）直接指向删除Agent时数据清理不完整的问题，合并后将影响 Agent 生命周期管理的基础逻辑，很可能进入下一个小版本。

结合项目近期版（2026.6.1），这些改动显示维护团队在逐步填补细节漏洞，从“可用”向“好用”过渡。

---

## 7. 用户反馈摘要
从今日唯一活跃用户 woxinsj 的Issue中提炼真实痛点：

- **备份场景面临的实际困难**：用户在每日数百条消息写入环境下（WAL模式，sqlite 71.6MB），点击备份后进程被冻结，只能强制结束。这反映在重IO、大文件情境下，备份操作未做异步或分批处理，导致主线程阻塞。用户还提供了完整复现步骤和环境信息，说明对产品有深度使用和较高期待。
- **安装流程的路径歧义**：用户原始安装在C盘失败，但真实安装位置在G盘，NSIS安装包可能有路径重定向或残留判断逻辑缺陷。用户自我排查到“确认C盘目录是无关副本”，表明安装程序在目标检测上存在误导，新用户容易困惑。

没有积极反馈或满意评论，两个Bug均影响了核心功能的使用（安装和备份），官方宜迅速回应。

---

## 8. 待处理积压
以下项目持续未响应，建议维护者重点关注：

- **PR #2065**（open, stale）——使用短UUID替代名称生成Agent ID，创建于2026-05-28，距今日已逾一个月。该修复可解决Agent数据复活与删除遗留问题，代码概要已有完整方案，但未得到Review或合并。考虑到Agent是产品核心概念，该项改动应为近期开发优先项。 [PR #2065](https://github.com/netease-youdao/LobsterAI/pull/2065)
- **Issue #2214**（备份卡死，高严重性）和 **Issue #2215**（安装失败）是新进积压，尚无官方回复。建议分配优先权排查备份卡死问题，确认是否与文件系统（外置盘）或SQLite WAL写入锁相关，并发布hotfix或临时规避方案。

---

**项目健康度小结**：代码层面，通过一次大规模PR清理，技术债务有所减少；但用户侧两个高/中严重性Bug的涌入，以及两个新Issue无官方响应，表明问题响应周期可能需要缩短。产品在稳定性和安装体验上仍有待加强，特别是高负载场景下的备份可靠性。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-06-28

---

## 1. 今日速览

过去 24 小时内，项目活跃度处于稳中有升的**打磨期**，核心聚焦于 **本地/小模型兼容性** 与 **平台边界 Bug**。

*   **新 Issue 1 条**：用户 `holgzn` 报告了 Apple 容器 ID 长度限制问题（#1137）。
*   **活跃 PR 2 条**：贡献者 `resumeparseeval` 集中发力，提交了修复小模型参数类型异常的 PR（#1136），同时还更新了搁置已久的同一方向 PR（#1098）。
*   **状态评价**：虽无新版本发布或 PR 合入，但两项关键修复已进入待合并阶段，表明项目当前重心在**夯实底层工具链鲁棒性**，而非功能堆叠。项目生态健康，社区活跃贡献者驱动迹象明显。

---

## 2. 版本发布

（无新版本发布）

---

## 3. 项目进展

今日 **无 PR 被合并或关闭**，但两项重要的 Bug 修复 PR 已进入**待合并**状态，标志着 Agent 与 Browser 工具层即将迎来一次核心稳定性升级：

| PR | 摘要 | 作者 | 创建/更新 | 状态 |
|----|------|------|-----------|------|
| [#1136](https://github.com/moltis-org/moltis/pull/1136) | fix(agents): coerce stringified scalar tool args before validation | resumeparseeval | 2026-06-27 | **OPEN** — 待合并 |
| [#1098](https://github.com/moltis-org/moltis/pull/1098) | fix(browser): tolerate null optional params in browser tool calls | resumeparseeval | 2026-06-03 / 2026-06-27 更新 | **OPEN** — 待合并 |

**解读**：
- #1136 解决了 Gemma 4、oMLX 等模型在 Agent 调用中将布尔/数字参数误序列化为字符串（如 `"full_page": "true"`）的问题。
- #1098 解决了同系列模型在浏览器工具调用中显式传入 `null` 导致序列化崩溃的问题。
- 两项 PR 合并后，Moltis 对非标准/本地模型的工具调用兼容性将获得**质变**，显著降低使用低成本模型的门槛。

---

## 4. 社区热点

**今日焦点人物**：`resumeparseeval`

虽然两项 PR 均暂无公开评论回帖，但它们所针对的问题（**小模型工具调用参数格式异常**）是目前 AI Agent 框架共通的痛点。 `resumeparseeval` 在一天内提交新 PR 并同步更新旧 PR，说明该方向正在集中攻关。

**潜在诉求分析**：社区对**非 OpenAI 标准模型**（尤其是本地部署的开源模型）的适配需求极高。Moltis 若能在下一版本中稳定支持 Gemma 4 等模型的原生工具调用，将有力拓展用户群体。

---

## 5. Bug 与稳定性

### 新增 Bug

| Issue | 标题 | 作者 | 创建时间 | 严重程度 | Fix PR |
|-------|------|------|----------|----------|--------|
| [#1137](https://github.com/moltis-org/moltis/issues/1137) | [Bug]: Apple Container ID exceeds name limit | holgzn | 2026-06-27 | 待评估 | 无 |

**分析**：
- 用户已执行完整预检查（搜索已有问题、确认版本最新），说明该 Bug 大概率是未被报告过的边界异常。
- “Apple Container ID” 通常涉及 macOS 应用沙盒（App Sandbox）或 iCloud 容器名称，可能与文件系统或持久化存储路径有关。
- **建议优先审视**：若影响 macOS 用户的使用流程，建议维护者通过 comment 向用户索要更完整的 session/log 信息以确认复现路径。

### 待修复积压 Bug

- **(#1136)** 工具参数字符化问题 → 已有 Fix PR
- **(#1098)** 浏览器工具参数 `null` 问题 → 已有 Fix PR

---

## 6. 功能请求与路线图信号

虽然无正式的 Feature Request 提交，但两个 PR 清晰反映了当前 **隐含路线图方向**：

- **信号 1：「泛型模型工具链统一」**  
  针对 Gemma 4、oMLX 的适配，说明开发方有意将 Moltis 打造为**模型无关**的 Agent 框架，重点解决不同模型在 tool calling 上的 JSON 方言差异。

- **信号 2：「工具调用可靠性工程」**  
  允许传入 `null` + 自动类型转换（string → scalar）意味着策略从“严格报错”转向“宽容容错”，这一策略很可能会被纳入下一版本的默认行为，并沉淀为可配置的 pre-dispatch 检查层。

---

## 7. 用户反馈摘要

| 用户 | 场景 / 反馈 | 隐含痛点 |
|------|-------------|----------|
| **holgzn** (#1137) | 按规范提报 Apple Container ID 长度超限 Bug | Apple 环境下的容器/沙箱管理细节可能与框架预设冲突，文件存储路径或命名方案存在平台差异 |
| **使用小模型的用户**（隐含在 #1136、#1098 修复背景中） | 模型输出 `"true"` / `null` 导致调用失败 | 非 ChatGPT 模型在结构化输出一致性上仍不成熟，用户需要框架层包容这种“脏数据”能力 |

**用户情绪评估**：负面反馈稀少（仅1条Bug），社区对当前维护方向（兼容性修复）无明显抵触，用户更倾向于通过 Issue 和 PR 贡献代码而非抱怨。

---

## 8. 待处理积压（需维护者关注）

| 条目 | 创建时间 | 等待天数 | 建议动作 |
|------|----------|----------|----------|
| [#1098](https://github.com/moltis-org/moltis/pull/1098) `fix(browser): tolerate null optional params` | 2026-06-03 | **25 天** | 合并已有更新，尽快进入 Code Review 周期。该 PR 语义清晰、风险低，长时间滞留可能打击贡献者积极性。 |
| [#1137](https://github.com/moltis-org/moltis/issues/1137) `Apple Container ID exceeds name limit` | 2026-06-27 | 1 天 | 打上 `needs-reproduction` 或 `apple` 标签，请求用户提供更多上下文。若影响范围大，可考虑放入 next patch 队列。 |

---

*数据统计时间范围：2026-06-27 全天更新 | 生成时间：2026-06-28*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，以下是基于 CoPaw (QwenPaw) 项目 2026-06-28 日 GitHub 数据生成的动态日报。

---

# CoPaw 项目动态日报 | 2026-06-28

## 1. 今日速览

今日项目活跃度**非常高**。尽管无新版本发布，但 Pull Requests (PR) 活动显著，共有 13 条更新，其中以测试覆盖率提升和特定 Bug 修复为主，显示项目正积极进行代码质量加固。Issues 侧主要反映了社区在使用非标准端点（如 DeepSeek V4）和新版本（2.0）时遇到的兼容性问题。值得关注的是，PR 合并率较低（1/13），大量待合并的 PR 可能形成积压，建议维护团队关注。

## 2. 版本发布

**无。** 过去 24 小时无新版本发布。

## 3. 项目进展

今日有 1 个重要 PR 被关闭/合并，另有大量针对后端与前端测试覆盖的 PR 正在推进中，表明项目在质量保障方面投入显著。

- **[合并] [PR #5213] fix(console): improve MCP access policy layout**：该 PR 修复了 MCP（模型上下文协议）客户端及相关权限管理界面的布局问题，提升了在不同屏幕尺寸下的响应式体验，并优化了访问主体的发现机制。
    - 链接：https://github.com/agentscope-ai/QwenPaw/pull/5213

- **[测试加固] 后端测试计划持续推进**: 多个由 @hanson-hex 提交的测试 PR (#5422, #5423, #5581) 正在等待合并。这些 PR 为 `runner`, `crons`, `app-infra` 等核心后端模块增加了超过 100 个单元测试用例，旨在将后端覆盖基线从 39% 提升并锁定现有功能契约。
- **[测试加固] 前端测试计划稳步落地**: 同样由 @hanson-hex 主导的前端测试 PR 序列 (#5409, #5434, #5438) 正在 review 中。这些 PR 为前端的状态管理（Zustand stores）、Hooks 及 API 调用层等关键模块增加了超过 400 个测试用例，对 UI 交互和 API 契约形成了有效保护。

**项目健康度评估**：项目整体处于**积极开发与加固期**。一方面在修复社区反馈的 Bug，另一方面在大力补充自动化测试，这对长期稳定性和协作效率是积极信号。但大量的待审查 PR 是一个潜在风险点，可能延迟反馈与迭代周期。

## 4. 社区热点

今日最受关注的 Issue/PR 围绕 **DeepSeek V4 模型兼容性** 展开。

- **[焦点] [Issue #5573] [Bug]: DeepSeek V4 thinking 模式在 OpenAI 兼容端点上的两类 400 错误**：这是今日讨论热度最高的问题。用户详细报告了在使用非官方 DeepSeek 端点（如中转站）时，由于 `reasoning_content` 字段缺失和工具调用 `null` 类型参数未清洗导致的 API 400 错误。该 Issue 引发了 **2 条评论**（在本日数据中最多），并已经促使关联 PR #5582 提交修复。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5573
    - **诉求分析**：该问题反映了部分用户需要通过第三方（中转站）访问 DeepSeek V4 等模型。用户群体并不全是专业 Python 开发者，他们希望项目能对非标准 API 响应有更强的容错性。这不仅是 Bug 修复，更是一个生态兼容性需求。

- **[修复跟进] [PR #5582] fix(providers): recover streaming reasoning_content errors**：该 PR 专门针对 #5573 报告的问题提出了修复方案，已在非流式路径增加了对 `reasoning_content` 错误的处理，并正在扩展对流式路径的保护。
    - 链接：https://github.com/agentscope-ai/QwenPaw/pull/5582

## 5. Bug 与稳定性

今日报告了 3 个 Bug/问题，按严重程度排列如下：

1.  **[严重] [Issue #5579] [Bug]: 异常中断场景下对话记录丢失**：用户报告称，当 Agent 执行导致宿主机重启或服务异常崩溃后，当前对话记录会完全消失，缺乏断点续传机制。这是一个严重影响用户体验和数据安全的问题。
    - 状态：**开放**，尚无关联的 Fix PR。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5579

2.  **[高] [Issue #5573] [Bug]: DeepSeek V4 thinking 模型兼容性**：如前所述，该问题影响使用特定模型和 API 端点的用户，虽然已有部分修复尝试，但问题根源在于 API 响应不符合标准格式。
    - 状态：**开放**，有关联的 Fix PR #5582。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5573

3.  **[中] [Issue #5584] [Question]: 无法连接自定义 ascend-vllm 模型**：用户反馈 1.1.7 版本后无法连接 ascend-vllm 模型，尽管配置验证通过，但对话时提示连接错误。这暗示可能是一个回归（Regression）问题。
    - 状态：**开放**，暂无关联 PR。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5584

## 6. 功能请求与路线图信号

- **[明确需求] 测试覆盖请求已转化为行动**：来自 @hanson-hex 的 Issue #5580 (Feature: app-infra backend unit test coverage) 已经被认领并转化为 PR #5581，表明团队对提升代码健壮性的响应非常积极。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5580

- **[用户体验] 界面主题/交互细节优化**：Issue #5583 提出“聊天界面右侧对话弹出层默认选中背景不明显”，这是一个典型的小型 UI/UX 优化需求，反映了用户对细节体验的关注。
    - 链接：https://github.com/agentscope-ai/QwenPaw/issues/5583

- **[生态兼容] 更强的模型端点容错性**：来自 Issue #5573 的讨论，暗示社区希望项目能更好地兼容非标准的 OpenAI 兼容 API 端点，例如对缺失的字段进行更完善的兜底处理。

## 7. 用户反馈摘要

- **对修复期望高，但验证成本高**：Issue #5573 的作者坦言“非Python程序员”，并花费精力验证了临时修改方案，希望维护者判断合理性。这反映了用户在面对不兼容问题时的**积极主动与对官方修复的渴望**，同时也揭示了部分用户技术背景非专业的现状。
- **对新版本适配的困惑**：Issue #5584 的作者表示“1.1.7 版本还可以，后来的版本都连接不上”。这种因版本升级导致的服务不可用会**显著降低用户满意度和信任度**。
- **对数据安全的担忧**：Issue #5579 的反馈非常具体，描述了对话丢失的两种典型极端场景（重启、崩溃），并称之为“系统非常脆弱”。这暴露了当前版本在**数据处理鲁棒性上的严重短板**，是提升用户体验的关键痛点。

## 8. 待处理积压

- **[长期未合并] [PR #4622] plugin(datapaw): add data-analysis plugin with 12 BI skills**: 这是一个从 5 月 22 日就提交的插件 PR，虽然重要，但已超过一个月未合并，状态为“Under Review”。如果该插件是路线图的一部分，应考虑加速合并或给出明确反馈以避免社区贡献者流失。
    - 链接：https://github.com/agentscope-ai/QwenPaw/pull/4622

- **[需要关注] 大量 Ready 状态的测试 PR 等待合并**: @hanson-hex 提交的 PR #5409, #5422, #5423, #5434, #5438 等已经存在数天且无新的评论（或评论为 undefined），它们对项目质量提升至关重要，但似乎陷入了审查瓶颈。建议项目维护者投入时间尽快审查和合并。

- **[无响应 PR/Issue] 暂无明确长时间未响应的 Issue 或 PR。** 所有开放 Issue 都有评论或关联活动，维护响应相对及时。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-06-28

---

## 1️⃣ 今日速览

ZeroClaw 社区在过去 24 小时内极度活跃，共产生 **49 条 Issue 动态**（新开 41，关闭 8）和 **50 条 PR 动态**（待合并 46，合并/关闭 4），项目健康度与协作密度均处于高峰期。MCP 协议的完整支持（Resources/Prompts）和供应链安全体系（SLSA/签名/SBOM）是两个最突出的推进方向，均有大型 PR 实现落地。长期积压的 `NO_REPLY` 噪音 Bug 和 MCP 作用域隔离失效问题已获修复，核心运行体验明显改善。整体看，项目在全力冲刺 **v0.8.3** 的同时，已开始为 **v0.9.0** 的 WASM 插件架构和安全模型变革铺路。

---

## 3️⃣ 项目进展

### ✅ 今日合并/关闭的 PR
- **`#8346` — 测试覆盖**：为 email_IMAP 工具的 TLS close_notify 检测添加测试，提升协议的健壮性。  
  [PR #8346](https://zeroclaw-labs/zeroclaw/pull/8346) | 状态：已合并

- **`#8344` — CI 修复**：将稳定版本指针（stable-pointer）的 tag 检查推迟到部署阶段，解决了版本合入时因 Git tag 不存在导致的 Pages 部署硬失败。  
  [PR #8344](https://zeroclaw-labs/zeroclaw/pull/8344) | 状态：已合并

### 🚀 即将推进的重大功能（OPEN PRs）

- **MCP 协议完整化**：`#8403` 为 ZeroClaw 引入了 MCP **资源（Resources）和提示（Prompts）** 客户端支持，配套策略门控的分发工具，使项目从“仅工具客户端”升级为全功能 MCP 客户端。  
  [PR #8403](https://zeroclaw-labs/zeroclaw/pull/8403) | 风险：高

- **供应链安全体系上线**：`#8404` 实现了 RFC #8177 的核心内容：cosign 签名、SLSA 出处追踪、SBOM 生成，覆盖正式发布流水线。  
  [PR #8404](https://zeroclaw-labs/zeroclaw/pull/8404) | 风险：高

- **被动上下文模型与 WhatsApp 支持**：`#8389` 提出了通用的 `passive_context` 主数据类型，并在 WhatsApp Web 群聊中应用，解决非寻址消息的被动语境积累问题。  
  [PR #8389](https://zeroclaw-labs/zeroclaw/pull/8389) | 风险：高

- **运行时长期 Bug 修复**：`#8405` 修复了 Cron/Heartbeat 在无报告内容时发送 "NO_REPLY" 文字的问题，清理通知噪音。  
  [PR #8405](https://zeroclaw-labs/zeroclaw/pull/8405) | 风险：高

- **离线成本定价与仪表盘**：`#8380` 引入离线定价目录和组织维度视图，为气隙/自部署环境提供完整的成本追溯能力。  
  [PR #8380](https://zeroclaw-labs/zeroclaw/pull/8380) | 风险：高

- **Inkbox 原生渠道**：`#8384` 新增 API-first 通信平台 Inkbox 作为原生渠道（邮件、短信、语音、iMessage），附带交互式快速入门流程。  
  [PR #8384](https://zeroclaw-labs/zeroclaw/pull/8384) | 风险：高

- **ZeroCode 仪表盘插件系统**：`#8408` 实现了 TUI 的面板插件系统和 41 主题切换器，显著提升 Dashboard 的可扩展性。  
  [PR #8408](https://zeroclaw-labs/zeroclaw/pull/8408) | 风险：高

---

## 4️⃣ 社区热点

- **`#4467` MCP 资源与提示支持**（4 👍，3 评论）  
  社区呼声最高的功能之一。用户 `tidux` 在 `#8403` 中提交了完整实现。从 Issue 提出到 PR 落地间隔约 3 个月，标志着 MCP 集成的深度里程碑。  
  [Issue #4467](https://zeroclaw-labs/zeroclaw/issues/4467) | [PR #8403](https://zeroclaw-labs/zeroclaw/pull/8403)

- **`#8177` 供应链签名与 SLSA（10 评论）**  
  本周讨论量最高的 Issue，涉及硬件 PGP、多方仲裁、离线签名、容器签名格式。社区对软件供应链安全表现出极高关注，随即被 `piiiico` 以 `#8404` PR 落地。  
  [Issue #8177](https://zeroclaw-labs/zeroclaw/issues/8177) | [PR #8404](https://zeroclaw-labs/zeroclaw/pull/8404)

- **`#5808` 32K 上下文预算超限（6 评论）**  
  持续引发用户不满的核心 Bug。默认值在首轮迭代即以 3.3x 超限，导致永久性强制修剪。用户追问修复优先级，维护者尚未给出明确排期。  
  [Issue #5808](https://zeroclaw-labs/zeroclaw/issues/5808)

- **`#8396` / `#8398` 新 RFC 集中涌现**  
  `Wire-Protocol-First Provider 模型`（`#8396`）和`插件权限配置模型`（`#8398`）在同一天提出，均涉及 v0.9.0 的破坏性变更。社区正围绕架构方向展开深度辩论。  
  [Issue #8396](https://zeroclaw-labs/zeroclaw/issues/8396) | [Issue #8398](https://zeroclaw-labs/zeroclaw/issues/8398)

---

## 5️⃣ Bug 与稳定性

| 严重程度 | Issue | 摘要 | 状态 |
|----------|-------|------|------|
| 🔴 P1 / S1 | [`#5808`](https://zeroclaw-labs/zeroclaw/issues/5808) | 默认 `max_context_tokens = 32000`，首次 LLM 迭代即超限 3.3x，导致强制修剪，工作流阻塞。 | **待修复，无 PR** |
| 🔴 P1 | [`#7733`](https://zeroclaw-labs/zeroclaw/issues/7733) | `mcp_bundles` 配置解析但不执行——安全隔离字段静默失效，对多 Agent 部署构成风险。 | **已修复**（生产已修，`#8370` 添加回归测试） |
| 🟡 P2 | [`#2128`](https://zeroclaw-labs/zeroclaw/issues/2128) | Cron/Heartbeat 将 `NO_REPLY` 文字发送到已配置的渠道，造成通知噪音。 | **已有 PR `#8405`**，待合并 |
| 🟡 P2 | [`#8366`](https://zeroclaw-labs/zeroclaw/issues/8366) | Heartbeat 引擎从 `data_dir` 而非 Agent 工作空间读取 `HEARTBEAT.md`，配置路径偏差。 | **待修复** |
| 🟡 P2 | [`#8317`](https://zeroclaw-labs/zeroclaw/issues/8317)（PR） | Provider 冷却机制失效，`fallback_models` 被错误当作全新上游而跳过冷却。 | **已有 PR `#8317`**，待合并 |
| 🟡 P2 | [`#8322`](https://zeroclaw-labs/zeroclaw/issues/8322)（PR） | Translations 泄漏修复，重写条目后未清理旧 key。 | **已有 PR `#8322`**，待合并 |

---

## 6️⃣ 功能请求与路线图信号

### 🔜 大概率纳入下一版本（已有实现 PR）
| 功能 | Issue | PR | 说明 |
|------|-------|------|------|
| MCP Resources/Prompts 支持 | [`#4467`](https://zeroclaw-labs/zeroclaw/issues/4467) | [`#8403`](https://zeroclaw-labs/zeroclaw/pull/8403) | 从工具客户端升级为全协议客户端 |
| 供应链安全 / SLSA | [`#8177`](https://zeroclaw-labs/zeroclaw/issues/8177) | [`#8404`](https://zeroclaw-labs/zeroclaw/pull/8404) | 签名、SBOM、出处追踪全链路 |
| 通用被动上下文 + WhatsApp | [`#8379`](https://zeroclaw-labs/zeroclaw/issues/8379) | [`#8389`](https://zeroclaw-labs/zeroclaw/pull/8389) | 非寻址消息的语境积累 |
| 离线成本目录与仪表盘 | [`#8380`](https://zeroclaw-labs/zeroclaw/issues/8380)（PR） | [`#8380`](https://zeroclaw-labs/zeroclaw/pull/8380) | 气隙/自部署环境成本管理 |
| SOP 步骤执行器 | [`#8399`](https://zeroclaw-labs/zeroclaw/issues/8399)（PR） | [`#8399`](https://zeroclaw-labs/zeroclaw/pull/8399) | 标准操作流程的实时执行支持 |

### 🔭 下一里程碑信号（RFC / Tracker）
| 议题 | 方向 | 说明 |
|------|------|------|
| [`#8396`](https://zeroclaw-labs/zeroclaw/issues/8396) | Provider 模型重构 | 以 Wire Protocol 为主轴重新组织 Provider 层次 |
| [`#8398`](https://zeroclaw-labs/zeroclaw/issues/8398) | 插件权限模型 | 从粗粒度 enum 演进为细粒度声明式权限 |
| [`#8135`](https://zeroclaw-labs/zeroclaw/issues/8135) | WASM 优先插件运行时 | 默认启用，签名分发，能力审计 |
| [`#8303`](https://zeroclaw-labs/zeroclaw/issues/8303) | Goal Mode 自主代理 | 支持 Agent 持续工作直到目标达成/耗尽预算 |
| [`#8348`](https://zeroclaw-labs/zeroclaw/issues/8348) | Skill CRUD 事件系统 | 为技能平台提供外部队列通知钩子 |
| [`#8071`](https://zeroclaw-labs/zeroclaw/issues/8071) | v0.8.3 运行时 Tracker | Agent 循环、工具执行、内存、Cron 的稳定性工作 |
| [`#7432`](https://zeroclaw-labs/zeroclaw/issues/7432) | v0.9.0 认证/安全 Tracker | 认证、安全加固、网关边界、破坏性变更 |

---

## 7️⃣ 用户反馈摘要

### 😠 典型痛点
- **上下文预算不合理（`#5808`）**：新用户的首个交互即触发预算超限，开箱即用体验严重受损。用户期待将默认值提升或启用动态预算。
- **安全配置不可信（`#7733`）**：`mcp_bundles` 在设计上承担 Agent 间工具隔离的重任，配置后却静默失效，削弱了管理员对安全模型的信任。
- **通知渠道不智能（`#2128`）**：Telegram 等渠道中 Cron 任务无内容可报时仍发送 "NO_REPLY"，大量冗余消息干扰真正的告警。

### 👍 使用场景与满意点
- **多租户配置诉求（`#8226`）**：用户 `susyabashti` 提出了含身份、参数、令牌多租户的 per-Agent 环境变量配置需求。场景清晰，方案完整（`runtime_context` + `runtime_secrets`），表明社区正朝团队级/企业级部署演进。
- **OpenRouter 生产化诉求（`#8138`）**：用户 `vinitasher` 希望利用 OpenRouter 的原生模型回退数组，提升 LLM API 调用的可靠性。这是 Agent 服务高可用性的典型需求。
- **社区协作深得人心**：从 `#4467` → `#8403`（`tidux`），`#8379` → `#8389`（`rifuki`），`#8177` → `#8404`（`piiiico`）等典型路径可见，维护者对社区 RFC 响应积极，贡献者参与度极高，形成了高效的需求→实现闭环。

---

## 8️⃣ 待处理积压

| 优先级 | 议题 / PR | 积压天数 | 问题描述 | 建议处理动作 |
|--------|-----------|-----------|----------|-------------|
| 🔴 **P1** | [`#5808`](https://zeroclaw-labs/zeroclaw/issues/5808) | 73 天 | 默认 32K 上下文超限导致工作流阻塞 | **维护者急需介入**：分配资源修复默认值或引入动态预算 |
| 🟡 P2 | [`#7952`](https://zeroclaw-labs/zeroclaw/issues/7952) | 9 天 | 发布全渠道预构建产物 | **needs-maintainer-review**：需决策发布策略与目标 |
| 🟡 P2 | [`#8226`](https://zeroclaw-labs/zeroclaw/issues/8226) | 5 天 | Per-Agent 自定义环境变量 | **needs-author-action**：跟进提案者补充细节 |
| 🟡 RFC | [`#8396`](https://zeroclaw-labs/zeroclaw/issues/8396) | 1 天 | Wire-Protocol Provider 模型 | **早期 RFC**：维护者需组织讨论，澄清 v0.9.0 路线图方向 |
| 🟡 RFC | [`#8398`](https://zeroclaw-labs/zeroclaw/issues/8398) | 1 天 | 插件权限/配置/密钥模型 | **早期 RFC**：需与 WASM 路线图对齐 |
| 🟡 RFC | [`#8135`](https://zeroclaw-labs/zeroclaw/issues/8135) | 6 天 | Wasm 优先插件运行时 RFC | **status:accepted**：已有 `#8368` 实验性实现，需评估合并策略 |

---

**报告总结**：ZeroClaw 当前处于高强度开发状态，MCP 深度集成与供应链安全是两大核心亮点。社区协作质量极高，RFC→PR 的转化效率令人印象深刻。最需关注的隐患是 `#5808`（32K 上下文预算）——作为 P1/S1 的首用户体验问题，长期未修已开始承受社区压力。多个 RFC（`#8396`, `#8398`, `#8135`）同时涌入，建议维护团队尽快召集团体会议，公开 v0.9.0 的架构选型方向，以避免社区贡献分支冲突。

</details>

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*