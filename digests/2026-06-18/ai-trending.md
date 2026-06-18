# AI 开源趋势日报 2026-06-18

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-18 03:37 UTC

---

# AI 开源趋势日报（2026-06-18）

**数据范围**：GitHub Trending（20 仓）+ 主题搜索（81 仓，标签含 ai-agent / llm / rag / ml / vector-db）  
**筛选结果**：Trending 中识别 AI/ML 相关仓库 9 个，主题搜索全量纳入，去重后共 **89 个** 活跃项目。以下按五大维度分类呈现。

---

## 1. 今日速览

- **Agent 技能工程化爆发**：`mattpocock/skills`（+1,523）与 `obra/superpowers`（+1,129）双双霸榜，前者沉淀实战技能库，后者定义开发方法论，社区从“造 Agent”转向“管 Agent 技能”。
- **数据获取 Agent 成为刚需**：`Agent-Reach` 今日再增 +1,161 stars，一键读取 Twitter、Reddit、视频平台等，零 API 成本，Agent “信息孤岛”瓶颈被打破。
- **MCP 协议在代码智能落地**：`codebase-memory-mcp`（+371）用毫秒级知识图谱索引整个代码库，MCP 正从概念走向 AI 开发基础设施。
- **时间序列基础模型开源**：Google 发布 `TimesFM`（+606），填补 LLM 之外的时序 Foundation Model 空白，金融、运维场景受关注。
- **多模态 Agent 栈与视频创作**：字节跳动 `UI-TARS-desktop`（+150）开源多模态 Agent 底座；`OpenMontage` 推出首个开源 Agent 视频制作系统，AI 向多模态自动化迈进。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架·推理·数据引擎·CLI）

| 项目 | Stars 数据 | 一句话说明 |
|------|------------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐174,419 | 极简本地大模型运行器，已支持 DeepSeek、Kimi、GLM 等最新模型 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐83,204 | 高吞吐 LLM 推理引擎，PagedAttention 核心驱动 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐134,208 | 为 AI Agent 提供规模化网页搜索、抓取与交互的 API 服务 |
| [bytedance/UI-TARS-desktop](https://github.com/bytedance/UI-TARS-desktop) | 今日 +150 | 字节开源多模态 Agent 栈，连接前沿模型与 Agent 基础设施 |
| [DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) | 今日 +371 | MCP 版代码智能服务器，毫秒级知识图索引，零依赖单二进制 |
| [google-research/timesfm](https://github.com/google-research/timesfm) | 今日 +606 | Google 时间序列基础模型，专为预测任务预训练 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐7,663 | Rust 生态模块化 LLM 应用框架，兼顾安全与性能 |
| [alexzhang13/rlm](https://github.com/alexzhang13/rlm) | 今日 +43 | 递归语言模型（RLM）通用推理库，即插即用支持多种沙盒 |

### 🤖 AI 智能体/工作流（Agent 框架·多智能体·自动化）

| 项目 | Stars 数据 | 一句话说明 |
|------|------------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐185,005 | 自主 Agent 先驱，持续进化的任务规划与工具执行平台 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐139,592 | Agent 工程平台，统一工具调用、记忆管理与 RAG 抽象 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐77,584 | AI 驱动软件研发 Agent，自动编写、调试及协作 |
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐145,655 | 生产级 Agentic 工作流开发平台，可视化编排 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | ⭐33,419 (+1,161 today) | 为 Agent 开启互联网之眼，支持 6+ 主流内容平台，零 API 费用 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐99,349 | 让 Agent 像人一样操作浏览器，自动化网页任务 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | ⭐35,267 | React/UI 前端的 Agent 集成栈，生成式 UI 与 AG-UI 协议 |
| [obra/superpowers](https://github.com/obra/superpowers) | 今日 +1,129 | Agent 技能框架+开发方法论，聚焦能力复用与协作 |

### 📦 AI 应用（垂直场景·产品·工具）

| 项目 | Stars 数据 | 一句话说明 |
|------|------------|------------|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐142,059 | 用户友好本地 AI 聊天界面，支持 Ollama / OpenAI |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐61,752 | 本地优先全能 Agent 体验，内置 RAG，完全私有 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐86,999 | 多智能体金融交易框架，LLM 驱动决策 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | ⭐69,353 | 金融数据平台，赋能分析师、量化与 AI Agent |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐47,483 | AI 生产力工作室：智能聊天+自治 Agent+300+ 助手 |
| [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) | 今日 +98 | 全球首个开源 Agent 视频制作系统，52 个管道、500+ 技能 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐28,888 | 从文档 AI 生成真实可编辑 PPT，含动画、语音 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | ⭐114,896 | 100+ 可运行 AI Agent 与 RAG 应用集合 |

### 🧠 大模型与训练（模型框架·训练·微调·评估）

| 项目 | Stars 数据 | 一句话说明 |
|------|------------|------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐161,683 | 模型框架事实标准，涵盖文本、视觉、多模态架构 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | ⭐100,843 | GPU 加速张量库，深度学习研究与训练首选 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | ⭐58,522 | YOLO 系列目标检测训练与推理，视觉 AI 标配 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,101 | 全模型评测平台，100+ 数据集，支持主流 LLM |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐264 | 可靠、可扩展的预训练库，用于基础模型与世界模型 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,289 | 在 Apple Silicon 上构建轻量 LLM 推理服务的课程项目 |

### 🔍 RAG/知识库（向量检索·检索增强·知识图谱）

| 项目 | Stars 数据 | 一句话说明 |
|------|------------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐83,060 | 领先开源 RAG 引擎，融合 Agent 能力，为 LLM 提供上下文层 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐83,021 | 跨 Agent 会话的持久上下文捕获、压缩与注入 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | ⭐82,857 | 将 PDF/图片转化为结构化数据，桥接 OCR 与 LLM |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,823 | 云原生向量数据库，高性能 ANN 搜索 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐58,811 | Agent 通用记忆层，跨会话知识维护 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐32,418 | 大规模向量搜索引擎，支持图式精准检索 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | ⭐17,889 | 自托管 Agent 记忆平台，基于知识图谱引擎 |
| [lancedb/lancedb](https://github.com/lancedb/lancedb) | ⭐10,637 | 开发者友好的嵌入式多模态检索库，零运维 |

---

## 3. 趋势信号分析

从今日数据可提炼三大趋势信号：

**Agent 技能工程化时代开启**  
`superpowers` 与 `skills` 的爆发式增长标志着 Agent 开发进入“能力复用”阶段。社区不再只关心如何构建单个 Agent，而是通过标准化技能包（Shell 脚本、.claude 配置目录）实现跨 Agent 共享。这和 `learn-claude-code`（67k stars）的低门槛 Agent 制造形成上下游生态。

**MCP 协议从概念走向代码智能**  
`codebase-memory-mcp` 在 Trending 上快速积累星数，意味着 Model Context Protocol 与代码库结合已获认可。它将代码索引为持久知识图，毫秒级查询、99% token 压缩，有望成为类似 LSP 的 AI 开发基础设施。

**时序与多模态基础模型补位**  
Google TimesFM 填补 LLM 之外的时序 Foundation Model 空白，今日 +606 stars 表明开发者对专用基础模型的迫切需求。同时 `UI-TARS-desktop` 与 `OpenMontage` 推动 Agent 向多模态视觉、视频创作扩展，纯文本 Agent 正朝多模态交互与生成演进。

**RAG 从“能用”转向“好用且省”**  
`RAGFlow` 持续领跑，新项目 `LEANN`（97% 存储节约）、`zvec`（进程内极简向量库）等降本方案涌现，向量数据库 `Milvus 44k`、`Qdrant 32k` 继续稳固。RAG 正朝着轻量私有化、低成本部署快速迭代。

---

## 4. 社区关注热点

- **⭐ Agent-Reach**（+1,161 stars）：零成本 CLI 一键接入主流平台，解除 Agent “信息孤岛”瓶颈，Agent 数据获取的最佳实践。
- **⭐ codebase-memory-mcp**（+371 stars）：MCP 协议在代码智能的标杆实现，一次性索引持久受益，为 AI 编程助理提供底层能力。
- **⭐ mattpocock/skills**（+1,523）& **obra/superpowers**（+1,129）：前者提供实用技能库，后者提供工程方法论，共同催生 Agent 技能生态，值得所有 Agent 开发者跟踪。
- **⭐ TimesFM**（+606 stars）：Google 开源时间序列基础模型，若生态成熟有望成为时序领域的 “Llama”，金融、气象、运维等场景想象空间大。
- **⭐ UI-TARS-desktop**（+150 stars）：字节开源多模态 Agent 底座，统一视觉理解、工具调用与交互，是构建下一代全能 Agent 的重要参考。

---

**总结**：2026-06-18 的 GitHub AI 开源热门清晰地展现了三大延伸方向——Agent 能力标准化（技能框架、MCP 协议）、数据基础设施（互联网访问、向量数据库）以及多模态/垂直场景落地（时序模型、视频制作、金融交易）。开发者可重点围绕 Agent 技能复用和 MCP 生态进行技术布局。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*