# AI 开源趋势日报 2026-06-04

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-04 03:41 UTC

---

# AI 开源趋势日报（2026-06-04）

> 分析范围：GitHub Trending 榜单 + AI 主题搜索（RAG / ai-agent / llm / llm-model / vector-db / ml），经 AI 相关性筛选，已剔除 Trivy、Odoo、coding-interview-university 等非 AI 项目。

---

## 1. 今日速览

今日 AI 开源社区呈现三大主线：**Agent 工程化加速**（ECC、hermes–agent 合计近 4000 stars）、**LLM 交互效率提升**（headroom 压缩工具首日 3530 stars）和**数据准备标准化**（微软 markitdown + opendataloader-pdf 合计超 2500 stars）。同时，**持久化记忆**（supermemory + claude-mem）与**垂直 Agent 应用**（交易、语音、PPT 生成）继续获得社区真金白银的投票。底层模型推理工具（airllm、vllm）维持热度，表明开发者仍在追求更低成本的模型部署。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架 / 推理 / 数据工具 / CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐173,091 | 本地运行主流 LLM 的事实标准 CLI，今日已支持 Kimi-K2.6、GLM-5.1 等新模型。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐138,450 | 最流行的 Agent 工程框架，以 LangGraph 为核心推动复杂工作流设计。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐81,884 | 高吞吐 LLM 推理引擎，生产部署首选，持续优化 PagedAttention。 |
| [chopratejas/headroom](https://github.com/chopratejas/headroom) | **今日 +3530** ⭐新项目 | 在到达 LLM 前压缩日志、RAG 块等文本，减少 60–95% token 而答案不变，直接降低 API 成本。 |
| [microsoft/markitdown](https://github.com/microsoft/markitdown) | **今日 +1984** ⭐新项目 | 微软开源的文档→Markdown 转换器，统一 PDF/Office 等格式，解决 RAG 数据预处理痛点。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐128,305 | 专为 AI Agent 设计的全网爬虫 API，支持搜索、抓取、与页面交互。 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐205,961（今日+2141） | Agent Harness 性能优化系统：技能、记忆、安全、研究优先，适配 Claude Code/Codex/Cursor 等。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐179,424（今日+1735） | “随你成长的 Agent”，主打可扩展性与自主能力，生态（WebUI、插件）同步爆发。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,738 | 经典自主 Agent 框架，持续迭代以支持更稳健的任务规划。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐82,730 | 多智能体金融交易框架，LLM 驱动决策，代表 Agent 在垂直金融领域的深度应用。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | ⭐31,935 | 前端 Agent 栈（React/Angular），提出 AG-UI 协议，降低 Agent UI 开发门槛。 |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | ⭐53,321 | 可视化构建 AI Agent 与工作流，拖拽式操作降低 Agent 开发门槛。 |

### 📦 AI 应用（具体产品、垂直场景）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐139,900 | 功能最全的 AI 聊天 UI，支持 Ollama/OpenAI 等后端，集成 RAG、工具调用。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐61,013 | 本地优先的 Agent 工作台，一切都在本地运行，强调数据主权。 |
| [Open-LLM-VTuber/Open-LLM-VTuber](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber) | **今日 +693** | 支持语音打断 & 本地 Live2D 的 LLM 语音交互应用，将虚拟角色与 AI 结合。 |
| [nesquena/hermes-webui](https://github.com/nesquena/hermes-webui) | **今日 +719** | Hermes Agent 的配套 Web 界面，支持手机/桌面端操作 Agent。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐46,832 | AI 生产力工作室，集成智能对话、自主 Agent 与 300+ 助手，统一模型访问。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐24,152 | AI 生成可编辑 PPT（原生形状、动画、语音旁白），支持自定义模板。 |

### 🧠 大模型 / 训练（模型权重、训练框架、微调评估）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | ⭐96,597 | 从零实现 ChatGPT 类 LLM 的经典教程，PyTorch 代码一步不落。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐51,093 | 2 小时从零训练 64M 参数小模型，极大降低 LLM 学习门槛。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,058 | 开源 LLM 评估平台，支持 100+ 数据集与主流模型。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐245 | 可靠、可扩展的基础模型预训练库，面向世界模型与统一模型。 |

### 🔍 RAG / 知识库（向量数据库、检索增强、记忆管理）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐143,761 | 生产级 Agentic Workflow 平台，RAG 是其核心能力之一，支持可视化编排。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐81,862 | 领先的开源 RAG 引擎，融合 DeepDoc 文档理解与 Agent 能力。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐57,631 | Agent 通用记忆层，跨会话存储用户偏好与事实，正在成为 RAG 的重要补充。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐80,504 | 自动捕获 Agent 会话内容、压缩并注入未来会话，实现“永久语境”。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,618 | 云原生向量数据库，支持万亿级向量 ANN 搜索，RAG 基础设施标配。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐31,785 | 高性能向量搜索引擎，Rust 实现，兼顾速度与可靠性。 |
| [supermemoryai/supermemory](https://github.com/supermemoryai/supermemory) | **今日 +600** | 极速记忆引擎，提供 Memory API，专为 AI Agent 设计持久化上下文。 |

---

## 3. 趋势信号分析

从今日 Trending 榜单的新增星数可以捕捉几个强烈信号：

1. **Token 压缩成为刚需**：headroom 以 3530 stars 登顶，反映社区对“减少 API 调用成本”的急迫需求。在 RAG 深度应用和长链 Agent 场景下，token 浪费已成瓶颈，压缩工具正在形成新的工具类别。
2. **Agent 基础设施走向精细化**：ECC（+2141）专注于 Agent Harness 的性能优化（技能、记忆、安全），hermes-agent（+1735）则提供完整的 Agent 基座。二者代表 Agent 从“能用”到“好用”的工程化拐点。
3. **数据预处理标准化加速**：微软推出 markitdown（+1984），opendataloader-pdf（+570）专攻 PDF 解析，说明 AI 数据管道的“清洗与转换”环节正在被独立产品化，且大厂与社区共同发力。
4. **记忆/上下文管理独立成层**：supermemory（+600）+ claude-mem（80k）和 mem0 一起，使“持久化记忆”成为 Agent 架构中的关键中间件，不再只是 RAG 的附属。
5. **轻量化推理持续吸睛**：airllm（+208）让 70B 模型在 4GB GPU 上运行，契合个人开发者和小团队的低资源部署诉求。结合 ollama 对新模型（Kimi-K2.6、GLM-5.1）的快速支持，本地推理生态正加速成熟。

---

## 4. 社区关注热点

- **headroom（token 压缩）**：新概念项目首日即登顶，值得关注其如何与现有 RAG、Agent 链路集成，以及竞品（如 LLMLingua）的反应。
- **affaan-m/ECC（Agent Harness 性能优化）**：今日新增 2141 stars，关注其“技能-本能-记忆”三层架构是否能成为 Agent 性能优化的参考范式。
- **microsoft/markitdown（文档转换）**：微软背书 + 1984 stars，可能成为 AI 数据预处理的标准库，关注其与 LangChain、LlamaIndex 等框架的集成适配。
- **claude-mem（跨会话上下文）**：80k stars 已证明 Agent 记忆层的巨大需求，关注其后续如何兼容更多模型和 Agent 框架。
- **Open-LLM-VTuber（语音交互 + 虚拟角色）**：将 LLM 与 Live2D 结合，类“AI 伴侣”方向持续升温，关注其能否带动多模态交互在消费端的普及。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*