# AI 开源趋势日报 2026-06-15

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-15 03:56 UTC

---

# AI 开源趋势日报 — 2026-06-15

## 今日速览

- NVIDIA 推出的 AI Agent 技能安全扫描器 **SkillSpector** 以单日 +964 stars 登顶 Trending，标志着 Agent 安全正成为社区刚需。
- 吴恩达发布统一多模型接口 **aisuite**（+291 stars），简化 LLM 提供商切换，推动工具链标准化。
- 金融垂直领域基础模型 **Kronos**（+244 stars）亮相，专注金融市场语言理解，显示行业大模型进入加速落地期。
- 经典教程《Introduction to Autonomous Robots》因更新登上热榜（+293 stars），AI 教育类项目依然有强劲的长尾需求。
- 智能体框架竞争持续白热化，Hermes‑Agent（193k stars）、ECC（215k stars）等头部项目保持高关注度，多智能体交易框架 TradingAgents（86k stars）异军突起。

---

## 各维度热门项目

### 🔧 AI 基础工具

- [ollama/ollama](https://github.com/ollama/ollama) ⭐174,183 — 本地 LLM 运行工具，支持最新模型（Kimi、DeepSeek 等），是个人与企业私有化部署的首选方案。
- [vllm‑project/vllm](https://github.com/vllm-project/vllm) ⭐82,866 — 高吞吐 LLM 推理引擎，通过 PagedAttention 等技术成为在线服务的事实标准。
- [langchain‑ai/langchain](https://github.com/langchain-ai/langchain) ⭐139,307 — 智能体工程平台，提供构建 LLM 应用的核心抽象，持续加强工具调用与 RAG 能力。
- [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) ⭐132,845 — 专为 AI Agent 设计的网页抓取 API，可将任意网页内容高效转换为 LLM 可用格式。
- [browser‑use/browser‑use](https://github.com/browser-use/browser-use) ⭐98,849 — 让 AI Agent 直接操控浏览器的自动化库，开辟 Web 操作新范式。
- [andrewyng/aisuite](https://github.com/andrewyng/aisuite) 今日新增 +291 — 统一多 AI 提供商接口，一行代码切换 OpenAI/Anthropic 等模型，降低集成成本。
- [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) 今日新增 +964 — 针对 AI Agent 技能的安全扫描器，可自动识别恶意代码与漏洞，Agent 安全领域新标杆。
- [open‑compass/opencompass](https://github.com/open-compass/opencompass) ⭐7,084 — 全面的大模型评估平台，支持 100+ 数据集与多模型横向比较，为模型选型提供客观依据。

### 🤖 AI 智能体/工作流

- [NousResearch/hermes‑agent](https://github.com/NousResearch/hermes-agent) ⭐193,670 — “与你共同成长的智能体”，强调持续学习与上下文演化，长期占据 Agent 框架头部。
- [affaan‑m/ECC](https://github.com/affaan-m/ECC) ⭐215,594 — Agent 性能优化系统，统合技能、记忆、安全与研究方向，专为 Claude Code 等 CLI Agent 设计。
- [Significant‑Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) ⭐184,943 — 自主 Agent 的开源里程碑，持续通过插件生态扩展自主任务能力。
- [langgenius/dify](https://github.com/langgenius/dify) ⭐145,230 — 生产级智能体工作流开发平台，提供可视化编排与 RAG 能力，企业级采纳广泛。
- [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) ⭐86,213 — 多智能体金融交易框架，利用 LLM 进行市场分析、策略生成与执行。
- [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) ⭐77,091 — AI 驱动的软件开发智能体，能自主完成代码编写、调试和部署，DevOps 自动化新范式。
- [mem0ai/mem0](https://github.com/mem0ai/mem0) ⭐58,573 — 通用 AI 记忆层，为 Agent 提供跨会话的长期上下文，解决遗忘问题。
- [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) ⭐53,581 — 低代码 AI Agent 构建平台，拖拽式工作流编排，适合快速原型与内部工具搭建。

### 📦 AI 应用

- [open‑webui/open‑webui](https://github.com/open-webui/open-webui) ⭐141,533 — 最流行的 LLM 用户界面，兼容 Ollama 与 OpenAI API，提供类 ChatGPT 体验。
- [Mintplex‑Labs/anything‑llm](https://github.com/Mintplex-Labs/anything-llm) ⭐61,595 — 全功能本地 LLM 应用，内置文档管理、Agent 执行与知识库，主打数据主权。
- [CherryHQ/cherry‑studio](https://github.com/CherryHQ/cherry-studio) ⭐47,336 — AI 生产力工作室，融合智能聊天、自主 Agent 与 300+ 助手模板，支持多模型。
- [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) ⭐82,224 — 轻量 OCR 工具，覆盖 100+ 语言，可将 PDF/图片快速转化为 LLM 可用的结构化数据。
- [OpenBB‑finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) ⭐69,151 — 金融数据平台，为分析师和 AI Agent 提供统一的数据接口与建模环境。
- [santifer/career‑ops](https://github.com/santifer/career-ops) ⭐53,755 — AI 驱动求职系统，自动化简历优化、职位搜索与投递，集成 Claude Code。
- [hugohe3/ppt‑master](https://github.com/hugohe3/ppt-master) ⭐27,586 — 从文档直接生成可编辑 PowerPoint，支持原生形状、动画与语音旁白。
- [Introduction‑to‑Autonomous‑Robots/Introduction‑to‑Autonomous‑Robots](https://github.com/Introduction-to-Autonomous-Robots/Introduction-to-Autonomous-Robots) 今日新增 +293 — 自主机器人经典教材（SLAM、运动规划等），因内容更新重回热榜。

### 🧠 大模型/训练

- [shiyu‑coder/Kronos](https://github.com/shiyu-coder/Kronos) 今日新增 +244 — 专为金融市场语言打造的基础模型，在金融 NLU 任务上表现突出，受到量化社区关注。
- [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) ⭐58,389 — YOLO 系列统一框架，支持检测、分割、分类等 CV 任务，是训练与推理的首选库。
- [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) ⭐195,659 — Google 开源的机器学习框架，工业生态庞大，持续更新 TPU 支持与 2.x 演进。
- [pytorch/pytorch](https://github.com/pytorch/pytorch) ⭐100,760 — 最主流的深度学习框架，动态图与 GPU 加速使其成为研究与生产的标配。
- [huggingface/transformers](https://github.com/huggingface/transformers) ⭐161,592 — 模型定义与微调的核心库，集成数万预训练模型，推动 LLM 民主化。

### 🔍 RAG/知识库

- [infiniflow/ragflow](https://github.com/infiniflow/ragflow) ⭐82,741 — 先进 RAG 引擎，融合 Agent 能力，为企业提供高质量的 LLM 上下文增强层。
- [run‑llama/llama_index](https://github.com/run-llama/llama_index) ⭐50,131 — 文档智能体与索引平台，简化非结构化数据连接 LLM 的流程。
- [meilisearch/meilisearch](https://github.com/meilisearch/meilisearch) ⭐58,097 — 极速搜索引擎，内置 AI 混合搜索，开箱即用的知识库底座。
- [milvus‑io/milvus](https://github.com/milvus-io/milvus) ⭐44,779 — 云原生向量数据库，高可用、高扩展，支撑大规模 RAG 与相似性搜索。
- [qdrant/qdrant](https://github.com/qdrant/qdrant) ⭐32,279 — 高性能向量搜索引擎，Rust 实现，提供丰富过滤与量化功能，生产级 AI 搜索首选。
- [weaviate/weaviate](https://github.com/weaviate/weaviate) ⭐16,323 — 云原生向量数据库，支持对象与向量混合检索，容错性强。
- [safishamsi/graphify](https://github.com/safishamsi/graphify) ⭐67,231 — 将代码、文档、数据库等转化为可查询知识图谱，为 Agent 提供结构化上下文。
- [pathwaycom/llm‑app](https://github.com/pathwaycom/llm-app) ⭐59,364 — 实时数据 RAG 模板，对接 Sharepoint、Kafka、S3 等，保证知识库持续同步。

---

## 趋势信号分析

- **AI Agent 安全迅速升温**：SkillSpector 单日新增近千 star，首次将 Agent 技能安全作为独立工具推出，暗示社区对 Autonomy 风险的焦虑正在催生新赛道。
- **统一接口层工具受追捧**：aisuite 的走红表明多模型共存成为常态，开发者亟需降低切换成本，类似的抽象层项目（如 Rig、LangChain4j）也将持续受益。
- **垂直行业 LLM 加速落地**：Kronos（金融）与 TradingAgents（量化交易）双双向社区证明了行业大模型的实用性，未来更多垂直基础模型有望出现。
- **记忆与知识图谱成为 RAG 的进阶方向**：mem0、graphify 等项目从“检索”走向“理解与联想”，Agent 的长期记忆和知识结构化正成为新的技术洼地。
- **本地化部署仍是主流叙事**：ollama、open‑webui 等持续霸榜高星区间，即使大模型 API 日益丰富，社区对数据主权和离线运行的需求依然强劲。

---

## 社区关注热点

- **Agent 安全体系构建**：SkillSpector 提醒开发者在交付 Agent 前需要进行技能安全审计；类似的安全扫描、权限隔离工具将迎来第一波市场。
- **多模型统一接入（aisuite 模式）**：开发者无需为每个模型编写单独适配代码，此类 SDK 将显著降低 LLM 应用的多供应商维护成本。
- **金融 + AI 的深层融合**：Kronos 与 TradingAgents 的上榜意味着 LLM 在量化分析、财报解读、交易策略上的应用已从理论走向可复现的开源实现。
- **知识图谱增强 Agent（graphify 等）**：将代码、文档、数据库构建为图结构，使 Agent 不仅“检索”还能“推理”，有望成为 RAG 的下一代范式。
- **低门槛 Agent 开发工具**：Flowise、dify 等可视化平台的用户量持续增长，非专业开发者也能快速搭建智能体，推动 Agent 应用的民主化。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*