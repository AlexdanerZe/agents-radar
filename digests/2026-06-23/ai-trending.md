# AI 开源趋势日报 2026-06-23

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-23 02:54 UTC

---

# AI 开源趋势日报 · 2026-06-23

---

## 1. 今日速览

今日 GitHub 热门 AI 项目中，**AI 视频生产**方向异军突起：世界首个开源智能体视频系统 OpenMontage 斩获 2,938 stars，HeyGen 推出的 hyperframes 和 Palmier Pro 分别主打 Agent 驱动的视频渲染与编辑。**AI Agent 技能生态**同步爆发：mattpocock/skills、gstack 等 Claude Code 技能仓库一日涌入上千 stars，结构化技能包成为新风口。**MCP 协议周边**持续升温，codebase-memory-mcp 实现毫秒级代码图谱检索，大幅提升 Agent 编码效率。此外，低资源大模型推理方案 AirLLM（单卡 4GB 运行 70B 模型）再受关注，LLM 金融分析应用 daily_stock_analysis 也获得 1,557 stars。整体上，社区正从“使用 AI”向“为 AI 构建专业工具链”快速演进。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[firecrawl](https://github.com/firecrawl/firecrawl)** ⭐137,421（今日 +615）  
  大规模网页搜索、抓取与交互 API，成为 LLM 与 Agent 获取实时数据的核心管道，今日人气不减。

- **[langchain](https://github.com/langchain-ai/langchain)** ⭐139,915  
  Agent 工程平台，提供统一的 LLM 调用、链、工具与智能体编排能力，是当前 AI 应用开发的基石框架。

- **[open-webui](https://github.com/open-webui/open-webui)** ⭐142,649  
  用户友好的 AI 界面，兼容 Ollama 与 OpenAI API，支持开箱即用的本地智能体交互。

- **[anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐61,947  
  本地优先的全功能 Agent 桌面应用，内置 RAG 与多模型切换，强调用户数据主权。

- **[codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** ⭐1,185（今日 +1,185）  
  高性能代码智能 MCP 服务器，将仓库索引为持久化知识图谱，158 种语言毫秒级查询，大幅减少 Agent 理解代码的 token 开销。

- **[CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐35,409  
  面向 Agent 与生成式 UI 的前端栈，支持 React、Angular、移动端，加速 AI 功能集成。

- **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐83,345  
  轻量级 OCR 工具包，支持 100+ 语言，可将图片/PDF 转化为结构化数据供给 LLM，是 RAG 管线的关键组件。

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体、技能）

- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐73,342（今日 +738）  
  字节开源的长时域 SuperAgent 框架，集成沙箱、记忆、工具与子智能体，可处理分钟级到小时级复杂任务。

- **[AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,091  
  最知名的自主 Agent 项目，持续迭代，致力于让每个人都能使用和构建 AI。

- **[OpenHands](https://github.com/OpenHands/OpenHands)** ⭐78,041  
  AI 驱动的软件开发助手，能理解代码库并自主编写和调试代码。

- **[browser-use](https://github.com/browser-use/browser-use)** ⭐100,151  
  让 AI Agent 自动化操作网页的利器，几行代码即可完成复杂在线任务。

- **[mattpocock/skills](https://github.com/mattpocock/skills)** ⭐2,051（今日 +2,051）  
  资深工程师的 Claude Code 实战技能包，直接可用的 `.claude` 配置，今日新增 stars 极高。

- **[garrytan/gstack](https://github.com/garrytan/gstack)** ⭐573（今日 +573）  
  复制 Garry Tan 的 Claude Code 精确设置，23 个专业工具角色，覆盖 CEO、设计师、工程经理等。

- **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** ⭐956（今日 +956）  
  817 个结构化网络安全 Agent 技能，映射 MITRE ATT&CK 等 6 大框架，兼容 20+ LLM 平台。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐200,036  
  随用户共同成长的 Agent 框架，强调个性化记忆与持续学习，社区活跃度极高。

### 📦 AI 应用（垂直场景解决方案、具体产品）

- **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)** ⭐2,938（今日 +2,938）  
  全球首个开源智能体视频生产系统，12 条管线、52 个工具、500+ 技能，将 AI 编码助手变为完整视频工作室。

- **[palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro)** ⭐2,463（今日 +2,463）  
  专为 AI 构建的 macOS 视频编辑器，深度集成 AI 辅助剪辑能力。

- **[jamiepine/voicebox](https://github.com/jamiepine/voicebox)** ⭐529（今日 +529）  
  开源 AI 语音工作室，支持声音克隆、听写与语音合成创作。

- **[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)** ⭐395（今日 +395）  
  编写 HTML 即可渲染视频，专为 AI Agent 设计，打通前端与视频生成之间的壁垒。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐45,967（今日 +1,557）  
  LLM 驱动的多市场股票分析系统，整合多源行情、实时新闻与决策看板，支持零成本定时运行。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐88,024  
  多智能体 LLM 金融交易框架，通过多个 Agent 协同制定策略，量化交易开源化代表。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐30,408  
  从任意文档生成真正可编辑的 PowerPoint（原生形状、动画、音频旁白），支持自定义模板。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,674  
  AI 生产力工作室，支持智能聊天、自主 Agent 与 300+ 预设助手，统一管理主流 LLM。

### 🧠 大模型/训练（推理引擎、训练框架、微调、评估）

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐174,755  
  本地运行大模型的最简单方式，已支持 Kimi、DeepSeek、Qwen 等主流模型，更新活跃。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐83,590  
  高吞吐、低延迟的 LLM 推理引擎，PagedAttention 优化显存，是生产部署的首选方案。

- **[lyogavin/airllm](https://github.com/lyogavin/airllm)** ⭐193（今日 +193）  
  仅需 4GB 显存即可运行 70B 模型，通过分层推理突破显存限制，资源有限者参与大模型探索的利器。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,112  
  全面 LLM 评测平台，支持 100+ 数据集与多模型，为模型选型与对比提供客观依据。

- **[zjunlp/LightThinker](https://github.com/zjunlp/LightThinker)** ⭐164  
  【EMNLP 2025】逐步压缩思考步骤，减少推理过程中的 token 消耗，启发轻量化推理新方向。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐266  
  可靠、最小、可扩展的基座模型预训练库，降低从头训练 LLM 的工程门槛。

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐83,381  
  领先开源 RAG 引擎，融合 Agent 能力为 LLM 构建高质量上下文层，适合企业级知识库。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,899  
  高性能云原生向量数据库，专为大规模向量相似搜索设计，RAG 系统的核心基础设施。

- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐32,567  
  Rust 编写的高性能向量数据库，可靠性强，广泛用于生产级 AI 检索。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐59,155  
  AI Agent 通用记忆层，持久化存储跨会话信息，使 Agent 拥有长期记忆能力。

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐83,778  
  自动捕获 Agent 会话并压缩为记忆，注入后续对话，兼容 Claude Code、Copilot 等主流平台。

- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** ⭐33,298  
  免向量推理型文档索引，为 RAG 提供轻量级替代方案，无需单独部署向量数据库。

- **[siyuan-note/siyuan](https://github.com/siyuan-note/siyuan)** ⭐44,565  
  隐私优先的开源知识管理软件，支持本地部署与 AI 整合，今日作为 Agent 记忆生态一环受关注。

---

## 3. 趋势信号分析

今日 AI 开源社区呈现三个显著趋势：

- **Agent 技能生态大爆发**：`mattpocock/skills`、`garrytan/gstack`、`mukul975/Anthropic-Cybersecurity-Skills` 等仓库单日涌入数千 stars，社区不再满足于通用 Agent 框架，开始输出高度结构化、领域专用的“技能包”。这些配置直接供给 Claude Code、Copilot 等使用，正在形成“技能市场”雏形。结合 `codebase-memory-mcp` 等 MCP 服务器，Agent 的能力边界快速扩展。

- **AI 视频生成“Agent 化”**：OpenMontage、palmier-pro、hyperframes 同日登榜，说明视频制作正被重新定义为“AI Agent 工作流”。OpenMontage 将 52 个工具编排为管线，让 Agent 自动完成从剧本到渲染的全流程；hyperframes 则直接面向 Agent 输出 HTML 视频。这一方向与近期 AI 视频模型的成熟相呼应，但更强调工程化与 Agent 自主性，是视频制作领域的新范式。

- **低资源推理与长时任务突破**：AirLLM 以 4GB 显存运行 70B 模型，延续了小显存跑大模型的刚需；deer-flow 通过子智能体 + 记忆系统处理小时级任务，弥补了当前 Agent 在长时间尺度上的短板。两者分别从硬件效率和任务时长两个维度突破现有瓶颈。此外，金融领域的 LLM 应用持续升温（`daily_stock_analysis`、`TradingAgents`），与近期市场量化开源趋势吻合。

---

## 4. 社区关注热点

- **📦 Claude Code 技能包（Skills）**：`mattpocock/skills`、`gstack` 爆发说明开发者急需“即插即用”的 Agent 技能。建议关注 `.claude` 目录生态，探索复用或贡献此类技能库，降低 Agent 配置成本。

- **🧠 代码上下文 MCP 服务器**：`codebase-memory-mcp` 做到毫秒级代码图谱检索，极大减少 Agent 理解项目的 token 开销。对于构建高效 Coding Agent 至关重要，值得深入研究 MCP 协议生态。

- **🎬 开源 Agent 视频管线**：`OpenMontage` 重新定义视频制作流程，展现 Agent 编排复杂多媒体任务的潜力。适合探索创意内容自动化生成方向，尤其是与现有视频模型的集成。

- **📊 LLM + 金融**：`daily_stock_analysis` 提供开箱即用的 LLM 驱动看板，`TradingAgents` 等多 Agent 框架进一步降低量化交易门槛。个人投资者可借此快速搭建 AI 辅助分析系统。

- **🏠 本地 Agent 记忆方案**：`mem0` 与 `claude-mem` 分别从通用记忆层和会话记忆两个角度解决 Agent 长程遗忘问题，是构建家庭级或企业级持久化 Agent 的关键基础设施，值得跟进这两类方案的演进。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*