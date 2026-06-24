# AI 开源趋势日报 2026-06-24

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-24 02:54 UTC

---

## 今日速览

今日 AI 开源社区呈现三大爆发点：**Agent 工程化工具链井喷**，围绕 Claude Code 的官方插件目录、CEO 级工具集以及最佳实践指南密集涌现；**多模态 AI 应用加速落地**，视频制作（OpenMontage）、语音克隆（Voicebox）和视频编辑（Palmier Pro）等产品均获得数千 stars；**RAG 与 MCP 协议深度融合**，以 codebase-memory-mcp 为代表的代码知识图谱方案实现毫秒级索引，标志着“AI 上下文工程”进入新阶段。此外 hermes-agent、deer-flow 等 Agent Harness 项目持续迭代，社区正从“框架搭建”转向“生产级工程优化”。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

- **[garrytan/gstack](https://github.com/garrytan/gstack)** [TypeScript]  
  Stars: 1,011（今日新增）  
  将 Garry Tan 的 Claude Code 开发环境封装为 23 个工具，覆盖 CEO、设计师、工程经理等角色，是 Agent 工程化最佳实践的模板化产物，今日开发者大量 fork 和实验。

- **[anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official)** [Python]  
  Stars: 77（今日新增）  
  Anthropic 官方管理的 Claude Code 插件目录，标志着 Claude 生态开始建立标准化扩展商店，直接推动 Agent 工具链的标准化。

- **[shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)** [HTML]  
  Stars: 344（今日新增）  
  从“vibe coding”进化到“agentic engineering”的实战指南，包含大量 Claude Code 的使用规范与模式，是当前 Agent 开发者必读的文档型项目。

- **[ollama/ollama](https://github.com/ollama/ollama)** [Go]  
  Stars: 174,810  
  本地 LLM 运行与管理的首选工具，持续支持最新模型（Kimi、GLM、DeepSeek 等），是 AI 开发者本地实验的基石。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** [Python]  
  Stars: 83,669  
  高性能 LLM 推理与服务引擎，依然是生产环境部署大模型的标配，社区活跃度长期居高。

---

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

- **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)** [Python]  
  Stars: 3,592（今日新增）  
  世界首个开源的“智能体视频制作系统”，内置 12 条管线、52 个工具和 500+ agent 技能，将 AI 编程助手直接转化为全栈视频工作室，今日新增 stars 全场最高。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** [Python]  
  Stars: 201,055（今日 +936）  
  “与你一同成长的 agent”，强调持续学习和记忆，是当前 Agent 框架中 star 增长最快的项目之一，代表了 Agent 自我进化的方向。

- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** [Python]  
  Stars: 73,996（今日 +739）  
  字节跳动开源的长时间跨度 SuperAgent，通过沙箱、记忆、工具、子 Agent 等模块处理分钟到小时的复杂任务，是“Agent 操作系统”的重要实践。

- **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** [Python]  
  Stars: 1,041（今日新增）  
  为 AI Agent 提供 817 个结构化网络安全技能，覆盖 6 个主流框架，支持 Claude Code、Copilot、Cursor 等 20+ 平台，是 Agent 技能库标准化的先行者。

- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** [JavaScript]  
  Stars: 220,610（今日 +593）  
  Agent Harness 性能优化系统，涵盖技能、本能、记忆、安全等模块，面向 Claude Code、Codex、Cursor 等多平台，是 Agent 工程性能调优的标杆。

- **[revfactory/harness](https://github.com/revfactory/harness)** [HTML]  
  Stars: 128（今日新增）  
  一种“元技能”：能自动设计领域专属的 Agent 团队，定义专业 agent 并生成它们所需的技能，是 Agent 自组织与自动编排的新范式。

- **[JCodesMore/ai-website-cloner-template](https://github.com/JCodesMore/ai-website-cloner-template)** [TypeScript]  
  Stars: 826（今日新增）  
  通过一条命令利用 AI coding agent 克隆任意网站，展示了 Agent 在 Web 自动化与前端生成领域的实用价值。

---

### 📦 AI 应用（具体产品、垂直场景解决方案）

- **[jamiepine/voicebox](https://github.com/jamiepine/voicebox)** [TypeScript]  
  Stars: 1,045（今日新增）  
  开源 AI 语音工作室，支持语音克隆、听写与创作，将最新语音模型封装为可直接使用的桌面级产品，降低了语音 AI 的使用门槛。

- **[palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro)** [Swift]  
  Stars: 1,630（今日新增）  
  macOS 原生视频编辑器，专门为 AI 视频生成工作流设计，强调“built for AI”，是 AI 原生创作工具的重要尝试。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** [Python]  
  Stars: 47,237（今日 +1,119）  
  LLM 驱动的多市场股票分析系统，整合行情、新闻、决策看板与自动推送，支持零成本定时运行，是金融垂直领域 AI Agent 的典型落地。

- **[koala73/worldmonitor](https://github.com/koala73/worldmonitor)** [TypeScript]  
  Stars: 294（今日新增）  
  实时全球情报仪表盘，AI 驱动的新闻聚合与地缘政治监控，适合政企用户进行态势感知，展现 Agent 在信息聚合中的应用潜力。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** [Python]  
  Stars: 88,202  
  多智能体 LLM 金融交易框架，已经在量化圈形成巨大影响力，是 Agent 在金融决策中的成熟代表。

---

### 🧠 大模型 / 训练（模型权重、训练框架、微调工具）

- **[huggingface/transformers](https://github.com/huggingface/transformers)** [Python]  
  Stars: 161,848  
  全行业标准的模型定义与训练框架，支持文本、视觉、语音等多模态，是每次新模型发布时的第一站。

- **[pytorch/pytorch](https://github.com/pytorch/pytorch)** [Python]  
  Stars: 101,020  
  深度学习训练的绝对主力框架，强大的 GPU 加速能力使其持续作为 AI 研究的基础设施。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** [Python]  
  Stars: 7,116  
  大模型评测平台，支持 100+ 数据集、全面评估 Llama、Qwen、GLM 等主流模型，是模型选型的重要参考。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** [Python]  
  Stars: 266（今日新增）  
  专注于基础模型与世界模型的稳定预训练库，虽小但代表了“预训练技术民主化”的新尝试，值得关注。

---

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

- **[DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** [C]  
  Stars: 1,300（今日新增）  
  高性能代码智能 MCP 服务器，将代码仓库索引为持久化知识图谱，毫秒级查询，支持 158 种语言，将 RAG 技术带入代码级上下文管理，今日 stars 增速惊人。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** [Python]  
  Stars: 83,476  
  领先的开源 RAG 引擎，将 RAG 与 Agent 能力融合，为 LLM 构建高性能上下文层，是企业级知识库开发的标配。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** [Python]  
  Stars: 50,325  
  业界最流行的文档 agent 与 OCR 平台，支持从非结构化数据中构建 RAG 管道，是知识库搭建的首选框架。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** [Go]  
  Stars: 44,920  
  云原生高性能向量数据库，专为大规模向量 ANN 搜索设计，是所有 RAG 系统底层存储的重要选择。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** [Python]  
  Stars: 59,263  
  通用的 AI Agent 记忆层，提供跨会话的长期记忆能力，是 Agent 能否持续学习的关键组件。

- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** [Python]  
  Stars: 71,237  
  智能体技能（skill），可将任意文件夹（代码、SQL、文档、图片）转化为可查询的知识图谱，极大降低了 RAG 的初始构建成本。

---

## 趋势信号分析

今日社区爆发性增长的 AI 工具主要集中在 **Agent 工程化** 和 **MCP（Model Context Protocol）生态**。一方面，以 gstack、claude-plugins-official 为代表的项目将 Claude Code 的使用经验沉淀为可复用工具与官方插件，表明开发者不再满足于简单调用，而是追求 **可复现、可管理、可组合的开发环境**。另一方面，codebase-memory-mcp 以“毫秒级代码索引 + 知识图谱”的方式刷新了 RAG 在代码理解上的效率，单日 1,300+ stars 显示出 **MCP 与知识库融合**正成为新热点。

值得注意的是，**多模态 Agent 应用开始脱离 demo 阶段**：OpenMontage 定义了一套完整的“智能体视频生产线”，Voicebox 提供开箱即用的语音克隆，Palmier Pro 直接为 AI 视频工作流设计编辑器——这些项目获得了大量非技术用户的关注。此外，**Agent Harness 的竞争进入“微调”阶段**，ECC 和 harness 等项目不再重复造轮子，而是聚焦性能优化、技能标准化和 agent 自组织，说明 Agent 框架已经渡过了早期“能不能做”的阶段，转向“如何做得更好”。

从行业背景看，Anthropic 不断强化 Claude Code 生态，加上近期 Claude 模型更新，引导大量开发者围绕该平台构建工具链；而字节跳动开源 deer-flow、NousResearch 持续迭代 hermes-agent，表明 **大厂和研究机构仍在加速 Agent 框架的竞赛**。

---

## 社区关注热点

- **Claude Code 插件生态（官方插件目录 + 第三方最佳实践）**  
  官方目录的发布与最佳实践指南的流行，意味着 Claude Code 已具备成为 agent 开发主流平台的基础，开发者应按需关注插件机制和 templates。

- **代码级 RAG：codebase-memory-mcp 引领的 MCP + 知识图谱路线**  
  用单一二进制实现毫秒级代码索引，未来可能改变 AI 工具的上下文管理方式，对涉及代码理解的 AI 产品具有直接参考价值。

- **OpenMontage 代表的“Agent 即 Studio”模式**  
  将 agent 能力与视频生产管线深度绑定，打开了 agent 在多媒体内容生成中的想象空间，适合关注 AI 视频/多模态方向团队深入复盘。

- **从 vibe coding 到 agentic engineering（最佳实践类项目）**  
  社区正在总结和输出“如何专业地使用 AI agent 进行开发”，这类沉淀对于企业引入 Agent 开发者文化至关重要。

- **知识图谱与 RAG 的轻量化融合（graphify 等 skill 级项目）**  
  将复杂的知识库建设封装为一条命令/一个 skill，大幅降低了 RAG 的准入门槛，预示未来“知识图谱即插件”可能成为标准功能。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*