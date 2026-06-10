# AI 开源趋势日报 2026-06-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-10 03:26 UTC

---

# AI 开源趋势日报（2026-06-10）

## 1. 今日速览

今日 GitHub 热榜清晰指向三个信号：**AI Agent 技能生态爆发**，last30days-skill（+3191）、pm-skills（+806）等技能市场类项目获得社区狂热点赞；**性能导向的基础组件**成为新宠，量化向量索引 turbovec 单日涨 1800+ Stars，本地 LLM 选型工具 whichllm 也获 600+；**垂直场景 AI 应用**持续多元化，医疗（openmed）、求职（career-ops）、金融（OpenBB）等均有代表项目上榜。OpenAI 插件生态和编码 Agent 技能类的活跃度同样不可忽视，AI 开源正从框架大战进入“技能 + 工具”的精细化阶段。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架・推理引擎・SDK・CLI）
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [whichllm](https://github.com/Andyyyy64/whichllm) | 🆕 +633 today | 在本地硬件上找到最适合的 LLM，按真实基准排名，一键运行 |
| [supervision](https://github.com/roboflow/supervision) | 🆕 +733 today | 可复用的计算机视觉工具集，降低 CV 应用开发门槛 |
| [opencv](https://github.com/opencv/opencv) | 🆕 +102 today | 经典开源计算机视觉库，AI 预处理与嵌入式视觉的支柱 |
| [vllm](https://github.com/vllm-project/vllm) | ⭐82,366 | 高吞吐、低内存的 LLM 推理与服务引擎 |
| [ollama](https://github.com/ollama/ollama) | ⭐173,723 | 本地快速运行大模型，已支持主流模型与社区新模型 |
| [transformers](https://github.com/huggingface/transformers) | ⭐161,465 | HuggingFace 官方模型框架，文本、视觉、语音全能 |
| [streamlit](https://github.com/streamlit/streamlit) | ⭐44,908 | 快速构建数据/AI 应用的前端框架，AI 原生产品首选 |
| [system-prompts-and-models](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) | 🆕 +79 today | 汇集各类 AI 工具的系统提示词与内部模型，资源宝库 |

### 🤖 AI 智能体 / 工作流（Agent 框架・自动化・多智能体）
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [last30days-skill](https://github.com/mvanhorn/last30days-skill) | 🆕 +3191 today | AI Agent 技能：一键研究 Reddit、X、YouTube、Hacker News 等并生成总结 |
| [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | 🆕 +806 today | 100+ 产品管理方向的 Agentic 技能市场，覆盖策略到增长 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 🆕 +443 today | Google 工程师出品的生产级编码 Agent 技能集合 |
| [aaif-goose/goose](https://github.com/aaif-goose/goose) | 🆕 +489 today | 开源可扩展 AI Agent，能安装、编辑、测试代码，超越对话 |
| [langchain](https://github.com/langchain-ai/langchain) | ⭐138,916 | Agent 工程平台，链式编排 LLM、工具和记忆 |
| [dify](https://github.com/langgenius/dify) | ⭐144,616 | 生产级 Agent 工作流开发平台，可视化编排 |
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,862 | 经典自主 Agent 项目，持续推动通用 AI 自动化 |
| [openai/plugins](https://github.com/openai/plugins) | 🆕 +284 today | OpenAI 插件规范，连接 AI 与第三方服务生态 |

### 📦 AI 应用（垂直场景・具体产品）
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [career-ops](https://github.com/santifer/career-ops) | ⭐51,822 (+1110 today) | 基于 Claude Code 的 AI 求职系统，14 种技能模式 + PDF 生成 |
| [openmed](https://github.com/maziyarpanahi/openmed) | 🆕 +191 today | 开源医疗 AI，面向健康领域的智能助手 |
| [tesseract-ocr](https://github.com/tesseract-ocr/tesseract) | ⭐74,586 | 开源 OCR 引擎，7 天内活跃，文档数字化主力 |
| [OpenBB](https://github.com/OpenBB-finance/OpenBB) | ⭐68,841 | 为分析师、量化交易和 AI Agent 打造的金融数据平台 |
| [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | ⭐81,665 | 从图像/PDF 提取结构化数据，支持 100+ 语言，LLM 的“眼睛” |
| [ppt-master](https://github.com/hugohe3/ppt-master) | ⭐25,657 | AI 根据文档生成原生 PPT，包含动画和语音，拒绝截图式输出 |
| [netdata](https://github.com/netdata/netdata) | ⭐79,099 | AI 增强的运维可观测性，全栈监控 + 智能告警 |

### 🧠 大模型 / 训练（微调・评估・预训练）
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐72,036 | 统一高效微调框架，支持 100+ LLM/VLM，ACL 2024 |
| [opencompass](https://github.com/open-compass/opencompass) | ⭐7,075 | 多模型、多数据集的 LLM 评估平台 |
| [tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,264 | 从零在 Apple Silicon 搭建微型 vLLM，系统工程师的学习项目 |
| [stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐251 | 可靠、最小化的预训练库，支持基础/世界模型 |
| [Awesome-Process-Reward-Models](https://github.com/RyanLiu112/Awesome-Process-Reward-Models) | ⭐165 | 过程奖励模型资源汇总，追踪 O1 等推理优化前沿 |
| [llm-jp/awesome-japanese-llm](https://github.com/llm-jp/awesome-japanese-llm) | ⭐1,409 | 日本語 LLM 综合列表，涵盖评估、数据集等，7 天内更新 |

### 🔍 RAG/知识库（向量数据库・检索增强・知识管理）
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [turbovec](https://github.com/RyanCodrai/turbovec) | 🆕 +1801 today | 基于 TurboQuant 的量化向量索引，Rust 编写，Python 绑定，追求极致速度 |
| [anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐61,333 | 本地优先的 Agent+RAG 一体工具，支持多种文档和模型 |
| [llama_index](https://github.com/run-llama/llama_index) | ⭐50,048 | 文档 Agent 与 OCR 平台，RAG 系统的核心框架 |
| [milvus](https://github.com/milvus-io/milvus) | ⭐44,707 | 云原生高性能向量数据库，大规模 AI 检索场景首选 |
| [ragflow](https://github.com/infiniflow/ragflow) | ⭐82,337 | 领先开源 RAG 引擎，融合 Agent 能力构建 LLM 上下文层 |
| [open-webui](https://github.com/open-webui/open-webui) | ⭐140,880 | 功能丰富的 AI 交互界面，支持 Ollama、OpenAI API，集成 RAG |
| [qdrant](https://github.com/qdrant/qdrant) | ⭐31,987 | Rust 实现的高性能向量数据库，专为下一代 AI 设计 |

---

## 3. 趋势信号分析

从今日热榜与七日内活跃项目可提炼出三大趋势：

- **Agent 技能市场正在形成**。last30days-skill（+3191）、pm-skills（+806）、agent-skills（+443）的集中爆发，表明社区已不满足于单一 Agent 框架，而是转向可组合、面向特定领域（研究、产品、工程）的技能插件。这暗示 Agent 生态正向 MCP 等协议驱动的“技能商店”演进，未来 Agent 能力将像 App 一样分发。
- **基础设施追求“极致性能 + 本地优先”**。turbovec（量化向量索引，+1801）和 whichllm（硬件适配评测，+633）的高速增长，显示开发者在拥抱大模型的同时，开始认真优化本地推理与检索成本。Rust 在 AI 基础设施层的渗透（turbovec、qdrant、rig）也印证了这一趋势。
- **AI 编码 Agent 生态快速膨胀**。围绕 Claude Code、Cursor、Windsurf 等工具衍生出的系统提示词仓库（system-prompts-and-models, +79）和垂直应用（career-ops，+1110）持续涌现，AI 不再只是辅助编程，而是通过 Agent Skills 直接渗透到项目管理、产品设计等非代码岗位。

---

## 4. 社区关注热点

- **last30days-skill**：今日 Stars 涨幅最高（3,191），定义 Agent 技能新范式——自主聚合多源（Reddit、X、YouTube、HN等）并输出有依据的摘要，适合情报分析类场景。
- **turbovec**：基于 TurboQuant 的量化向量索引，用 Rust 重写核心，Python 调用，单日 1.8k Stars——性能敏感型 AI 基础设施的重要尝试。
- **whichllm**：解决“哪个本地模型最适合我的硬件？”的刚需，633 Stars 说明社区正在从“跑模型”转向“跑对模型”。
- **addyosmani/agent-skills**：Google Chrome 团队出品，将工程最佳实践封装为 AI Agent 技能，代表编码 Agent 从“实验”走向“生产级”的最佳实践。
- **roboflow/supervision**：733 Stars，持续迭代的 CV 工具集，将 YOLO、SAM 等模型与调试、标注、部署无缝衔接，让计算机视觉更“工程化”。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*