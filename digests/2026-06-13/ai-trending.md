# AI 开源趋势日报 2026-06-13

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-13 03:25 UTC

---

# AI 开源趋势日报（2026-06-13）

## 1. 今日速览

- **AI Agent 技能体系集中爆发**：Trending 榜前 10 中 4 个项目围绕标准化 Agent Skills（agent-skills、superpowers、agency-agents、pm-skills），表明社区正从单体 Agent 转向可组合的技能生态。
- **基础设施优化持续升温**：LMCache 凭借 KV 缓存加速首次登榜，vllm、ollama 等成熟引擎地位稳固，同时 Rust 语言 AI 框架 rig 和本地学习项目 tiny-llm 崭露头角。
- **垂直领域 AI 落地加速**：医疗 AI 项目 openmed 上榜，金融分析（daily_stock_analysis）、办公（ppt-master）等应用同样吸引大量关注。
- **RAG 与向量数据库仍是基石**：Milvus、Qdrant、RAGFlow 等持续迭代，LEANN 等新项目在存储效率上做出突破。
- **Agent 评估标准浮现**：ICLR 2026 收录的 FeatureBench 为 Agent 编程能力提供基准，行业开始重视评测。

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

- [LMCache](https://github.com/LMCache/LMCache) ⭐0（+28 today）  
  为 LLM 提供最快的 KV 缓存层，降低推理延迟，今日登榜趋势信号。

- [vllm](https://github.com/vllm-project/vllm) ⭐82,725  
  高吞吐、内存高效的 LLM 推理引擎，已成为生产部署标准。

- [ollama](https://github.com/ollama/ollama) ⭐173,984  
  本地运行大模型的最简方案，持续整合 Kimi、DeepSeek 等最新模型。

- [huggingface/transformers](https://github.com/huggingface/transformers) ⭐161,548  
  支持文本、视觉、多模态的模型训练与推理框架，AI 开发的基础设施。

- [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) ⭐7,602  
  Rust 语言下的模块化 LLM 应用框架，代表 AI 开发向系统级语言迁移的趋势。

- [googleworkspace/cli](https://github.com/googleworkspace/cli) ⭐27,023  
  集成 AI Agent 技能的 Google Workspace 命令工具，终端内直接调用服务。

- [ultralytics](https://github.com/ultralytics/ultralytics) ⭐58,337  
  YOLO 模型训练与部署框架，AI 视觉应用的核心工具。

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) ⭐0（+2656 today）  
  生产级 AI 编码 Agent 技能集，今日热榜第一，社区对标准化技能组件渴求的缩影。

- [obra/superpowers](https://github.com/obra/superpowers) ⭐0（+1275 today）  
  Agent 技能框架与软件开发方法论，强调可复用的工程实践。

- [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) ⭐0（+1026 today）  
  完整 AI 代理机构，囊括前端、运营、审查等多角色专业 Agent。

- [phuryn/pm-skills](https://github.com/phuryn/pm-skills) ⭐0（+827 today）  
  面向产品经理的 Agent 技能市场，探索技能商业化路径。

- [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) ⭐184,916  
  通用自主 Agent 先驱，始终是 Agent 领域代表性项目。

- [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) ⭐192,063  
  能自我进化的 Agent 框架，强调长期生长与适应能力。

- [browser-use/browser-use](https://github.com/browser-use/browser-use) ⭐98,529  
  使 AI Agent 真实操作浏览器的工具，是 Web 自动化关键组件。

- [langchain-ai/langchain](https://github.com/langchain-ai/langchain) ⭐139,154  
  Agent 工程化平台，统一 API、工具调用与 MCP 支持。

### 📦 AI 应用（具体产品、垂直场景解决方案）

- [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) ⭐0（+515 today）  
  开源医疗 AI，满足医疗行业对智能化的迫切需求，今日亮点。

- [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) ⭐47,251  
  AI 生产力工作室，支持智能聊天、自主 Agent 与 300+ 助手。

- [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) ⭐27,024  
  从任意文档生成可编辑 PPT，保留原生形状与演讲者注释。

- [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) ⭐42,337  
  LLM 驱动的多市场股票分析系统，集成实时新闻与决策看板。

- [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) ⭐69,027  
  面向分析师和 AI Agent 的金融数据平台。

- [ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai) ⭐27,143  
  AI 驱动的 Python 爬虫，智能提取网页结构化数据。

### 🧠 大模型 / 训练（训练框架、微调、评估）

- [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) ⭐72,122  
  统一高效微调 100+ LLM/VLM 的框架（ACL 2024），训练必备工具。

- [open-compass/opencompass](https://github.com/open-compass/opencompass) ⭐7,081  
  LLM 评估平台，覆盖 100+ 评测数据集，助力模型选型。

- [LiberCoders/FeatureBench](https://github.com/LiberCoders/FeatureBench) ⭐75  
  ICLR 2026 收录的 Agent 编程基准，推动 Agent 能力评估标准化。

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

- [milvus-io/milvus](https://github.com/milvus-io/milvus) ⭐44,751  
  云原生高性能向量数据库，大规模向量 ANN 搜索标准。

- [qdrant/qdrant](https://github.com/qdrant/qdrant) ⭐32,065  
  高可扩展向量数据库，为 AI 搜索提供生产级支持。

- [infiniflow/ragflow](https://github.com/infiniflow/ragflow) ⭐82,585  
  领先的开源 RAG 引擎，融合 Agent 能力构建优质上下文层。

- [neuml/txtai](https://github.com/neuml/txtai) ⭐12,652  
  一体式 AI 语义搜索框架，整合 LLM 编排与工作流。

- [lancedb/lancedb](https://github.com/lancedb/lancedb) ⭐10,587  
  嵌入式多模态检索库，开发者友好，适合本地 AI 应用。

- [zilliztech/claude-context](https://github.com/zilliztech/claude-context) ⭐11,832  
  将整个代码库转为 Agent 上下文的 MCP 工具，提升编码 Agent 效果。

- [run-llama/llama_index](https://github.com/run-llama/llama_index) ⭐50,098  
  文档 Agent 与 OCR 平台，RAG 生态核心组件。

- [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) ⭐11,913  
  MLsys2026 成果：在个人设备上运行 RAG，节省 97% 存储。

## 3. 趋势信号分析

今日数据最强烈的信号是 **Agent 技能生态从概念走向落地**。Trending 榜 top 10 中四个项目（agent-skills、superpowers、agency-agents、pm-skills）均围绕“可复用 Agent 技能”，说明社区正从“造单个 Agent”转向“搭标准组件”。pm-skills 甚至提出“技能市场”，暗示 Agent 技能的商品化萌芽。与此同时，**基础设施层仍在加速进化**：LMCache 首次登榜，代表 KV 缓存优化成为推理降本的新焦点；Rust 框架 rig 和 tiny-llm 等学习项目表明开发者开始追求更高性能和本地化工具链。**垂直应用多点开花**——医疗（openmed）、金融（daily_stock_analysis）、办公（ppt-master）等项目集体登榜，印证开源 AI 正在快速渗透具体行业。此外，**Agent 评估基准 FeatureBench** 入选 ICLR 2026，配合 OpenCompass 等评测平台，行业对 Agent 质量的衡量正走向标准化。结合近期 K2.6、DeepSeek 等模型发布，本地推理与 Agent 工程化已成为当前开源 AI 的两大主线。

## 4. 社区关注热点

- **🔥 Agent 技能标准化与市场**：关注 addyosani/agent-skills、obra/superpowers，它们定义了可组合的技能单元，可能成为下一代 AI 开发的主流范式。
- **🔧 轻量高性能推理**：LMCache、rig、tiny-llm 等项目彰显社区对减少推理成本、实现本地化部署的强烈兴趣。
- **📈 垂直行业 AI 落地**：openmed（医疗）、OpenBB（金融）、ppt-master（办公）等开源应用崛起，证明 AI 正从通用走向专用。
- **📚 Agent 持久化记忆**：mem0、cognee、claude-context 等项目持续迭代，长期记忆与上下文管理成为 Agent 实用化的关键瓶颈。
- **📊 Agent 能力评测**：FeatureBench 与 OpenCompass 共同推动 Agent 与 LLM 的标准化评估，保证质量将愈发重要。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*