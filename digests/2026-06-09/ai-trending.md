# AI 开源趋势日报 2026-06-09

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-09 02:49 UTC

---

## 🤖 AI 开源趋势日报 | 2026-06-09

### 1. 今日速览
- **Agent “技能”范式爆发**：今日最热门的 `last30days-skill` (+3558)、`google/skills` (+461) 等项目，标志着 AI 智能体从单一工具进化为可组合的“技能市场”。
- **Rust 加速重构 AI 基础设施**：`turbovec`（向量索引，+1729）、`goose`（Agent 引擎，+699）等 Rust 项目霸榜，内存安全与极致性能成为新一代 AI 基础软件的标配追求。
- **开源 Agent 工厂崛起**：`aaif-goose/goose`、`Personal_AI_Infrastructure` 等项目推动开发者构建完全自主、私有的 AI 环境，挑战依赖专有云的模式。
- **高价值垂直场景 Agent 化**：`santifer/career-ops`（求职，总 ⭐50k+）证明了在高度复杂、个性化的个人工作流中，Agent 具备极大的商业与社会潜力。
- **多模态与本地化齐驱**：`roboflow/supervision`（CV，+1288）热度不减，`whichllm`（+143）则直击本地模型选型的痛点。

---

### 2. 各维度热门项目

#### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

- **[RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec)** ⭐0 (+1729 today)  
  基于 TurboQuant 的高性能向量索引，Rust 内核 + Python 绑定。在 FAISS 和 pgvector 之外给出了一个更现代、更快的选择，是 AI 搜索与 RAG 管道的核心组件。

- **[roboflow/supervision](https://github.com/roboflow/supervision)** ⭐0 (+1288 today)  
  最流行的可复用计算机视觉工具集，集成了检测、分割、跟踪等常见 CV 能力，是构建视觉 AI 应用的瑞士军刀。

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐173,631  
  本地运行大模型的事实标准。现已支持 Kimi-K2.6、GLM-5.1、DeepSeek 等最新模型，持续降低 AI 本地部署门槛。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,262  
  高吞吐、低内存的 LLM 推理与服务引擎，生产环境中部署大模型的绝对主流选择。

- **[langchain4j/langchain4j](https://github.com/langchain4j/langchain4j)** ⭐12,250  
  Java 生态的 LLM 应用开发框架，为 Spring Boot 和 Quarkus 提供了统一的 AI 调用接口，支撑企业级 AI 工程落地。

- **[Andyyyy64/whichllm](https://github.com/Andyyyy64/whichllm)** ⭐0 (+143 today)  
  一个 CLI 工具，根据硬件跑分推荐最适合的本地模型。解决了“参数不止，哪个模型跑得最好”的社区核心痛点。

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐7,562  
  用 Rust 构建模块化 LLM 应用的框架，为性能敏感型 AI 组件提供了 LangChain 之外的全新选择。

---

#### 🤖 AI 智能体 / 工作流（Agent 框架、技能、自动化）

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (+3558 today)  
  **今日热度最高**。赋予 AI Agent 强大的“研究”技能，跨平台（Reddit、X、YouTube、HN）自动检索并综合摘要。是“技能化 Agent”的典范。

- **[google/skills](https://github.com/google/skills)** ⭐0 (+461 today)  
  Google 官方推出的 Agent Skills。巨头的入局意味着“技能”将成为未来 AI 生态的核心计量单位，并可能推动技能标准的统一。

- **[aaif-goose/goose](https://github.com/aaif-goose/goose)** ⭐0 (+699 today)  
  开源、可扩展的 AI Agent（Rust 编写），超越代码补全，支持安装、执行、编辑和测试。目标是成为开源界的 Copilot。

- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** ⭐0 (+679 today)  
  零 API 费用，让 AI Agent 获取全网信息的桥梁。打通了 Agent 与实时异构数据源（Twitter、Reddit、B站、小红书等）的交互通道。

- **[openai/plugins](https://github.com/openai/plugins)** ⭐0 (+296 today)  
  OpenAI 官方插件集合，是定义 Agent 能力边界与调用方式的关键参照基准。

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐144,457  
  生产级智能体工作流开发平台，将复杂的 AI 逻辑（RAG、工具调用、多 Agent）可视化、工程化。

- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐130,344  
  为 AI Agent 构建的大型网络数据采集 API，从搜索到抓取再到格式化输出，是 Agent 获取在线信息的基础设施。

---

#### 📦 AI 应用（具体产品、垂直场景解决方案）

- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐50,625 (+308 today)  
  基于 Claude Code 构建的 AI 求职系统，涵盖 14 种技能模式、Go 仪表盘和 PDF 生成。是 Agent 改造高价值个人工作流的商业化典范。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,083  
  集成 300+ 智能体的 AI 生产力工作室，统一接入前沿大模型，提供智能聊天与自主 Agent。

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐140,705  
  最受欢迎的本地 AI 用户界面。完美支持 Ollama 与 OpenAI API，是众多玩家进入 AI 世界的第一入口。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐41,405  
  LLM 驱动的多市场股票智能分析系统。零成本定时运行，展示了 LLM 在金融投资领域的落地范式。

- **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐81,506  
  RAG 的“最后一公里”工程。将任意 PDF 和图片转化为 LLM 能理解的结构化数据，是构建文档型 AI 应用的必经之路。

---

#### 🧠 大模型 / 训练（模型权重、微调、评测）

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐72,005  
  100+ 大模型的统一高效微调框架（ACL 2024）。无论是学术界还是工业界，微调私有模型的首选工具。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐187,549  
  “与你一同成长的 Agent”项目，代表了一种去中心化、社区驱动的 Agent 进化理念，社区影响力巨大。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,068  
  大模型评测基准平台，全面覆盖主流模型（Llama、Qwen、GPT-4、GLM 等），是衡量模型能力强弱的客观标尺。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐251  
  可靠、可扩展的基础模型预训练库，致力于让预训练过程更稳定高效，属于前沿基建。

- **[LiberCoders/FeatureBench](https://github.com/LiberCoders/FeatureBench)** ⭐75  
  [ICLR 2026] 专注于复杂功能开发的智能体编程基准测试，代表了 Agent 评估从基础任务向复杂工程项目的演进。

---

#### 🔍 RAG / 知识库（向量数据库、检索增强、记忆管理）

- **[MemPalace/mempalace](https://github.com/MemPalace/mempalace)** ⭐0 (+170 today)  
  声称“基准测试最佳”的开源 AI 记忆系统。免费，聚焦于解决智能体跨会话的长期记忆问题，是状态化 Agent 的核心依赖。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,236  
  领先的开源 RAG 引擎，将 RAG 与 Agent 能力深度融合，构建了 LLM 背后坚实的上下文层。

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐61,267  
  “停止租用你的智力”。提供本地优先的一站式 RAG / Agent 体验，全栈支持，重视数据所有权。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐50,014  
  文档 Agent 与 OCR 平台，连接私有数据与大模型的事实标准接口。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,687  
  高性能云原生向量数据库，支持规模化向量 ANN 搜索，是大型 RAG 系统的数据库基座。

- **[NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)** ⭐27,780  
  进阶 RAG 技术的百科全书，持续更新各种前沿的检索增强生成策略，是 RAG 工程师的必备参考。

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** ⭐17,732  
  面向智能体的开源 AI 记忆平台。使用自托管知识图谱引擎，为 Agent 提供持久化、结构化的长期记忆。

---

### 3. 趋势信号分析

1. **Agent Skills 生态即将展开平台战**：今日榜首 `last30days-skill` 与 Google 官方的 `google/skills` 遥相呼应，标志着 AI 能力正从“内置”走向“外挂”。类似移动端 App Store 或 ChatGPT Plugin 的逻辑正在重演，但这一次开放度更高、技术栈更底层。围绕技能的通用定义标准（如 CopilotKit 提出的 AG-UI 协议）可能成为下一个生态必争之地。

2. **Rust 正在征服 AI 基础设施的最后阵地**：`turbovec`、`goose`、`qdrant`、`rig` 等项目的连续登榜，印证了 Rust 在内存安全与极致性能上的绝对优势。当 Python 占据模型侧，Rust 正快速吃掉向量引擎、Agent 运行时、高吞吐通信层等对性能要求苛刻的组件。

3. **个人化“AI 工厂”取代单点工具**：`aaif-goose/goose` 配合 `whichllm` 和 `Personal_AI_Infrastructure`，构成了一整套“本地感知 → 模型选型 → Agent 执行”的个人 AI 流水线。这反映出社区不再满足于使用单一 AI 应用，而是希望构建一个能自由组装、完全受自己控制的生产力工厂。

4. **RAG 从“文本块搜索”走向“多模态知识代理”**：`PaddleOCR`（文档理解）、`Graphify`（代码/文档转知识图谱）、`safishamsi/graphify`（63k 星）以及 `MemPalace`（记忆层）的流行，说明 RAG 正在从简单的向量相似度搜索进化到深度的多模态解析、结构化知识构建和跨会话记忆管理。

---

### 4. 社区关注热点

- **`mvanhorn/last30days-skill`**：今日涨星冠军。它不是一个普通的 Agent，而是一个可交易的“技能包”。未来可能出现类似 npm 的 Agent 技能注册中心，该项目的 API 设计值得每一位 Agent 开发者关注。

- **`RyanCodrai/turbovec`**：在向量数据库和搜索算法趋于稳定的今天，一款纯 Rust 的高性能索引库带来的 10x 性能提升潜力，可能改变 RAG 应用的架构设计。

- **`aaif-goose/goose`**：如果你想拥有一个完全开源、不绑定任何云厂商的 Copilot/Devin，Goose 是最佳起点。它的可插拔架构和 Rust 内核是其相比同类项目的核心优势。

- **`CopilotKit/CopilotKit`**：Agent 的交互不再局限于命令行或对话框。CopilotKit 提供的 Generative UI 组件（React/Angular/Mobile）正在定义 Agent 前端交互的范式。其推出的 AG-UI 协议可能成为行业标准。

- **`PaddlePaddle/PaddleOCR`**：数据预处理是 RAG 实际投入生产时最大的工程难点。PaddleOCR 极高的 Stars 数和活跃度证明了大量 AI 应用开发者正在将海量非结构化文档（PDF/图片）作为 AI 系统的知识输入源。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*