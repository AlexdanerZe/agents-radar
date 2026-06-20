# AI 开源趋势日报 2026-06-20

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-20 03:23 UTC

---

# AI 开源趋势日报 | 2026-06-20

---

## 今日速览

Google 时间序列基础模型 **TimesFM** 与智谱新模型 **GLM-5** 同日登榜，表明基础模型仍在快速迭代，且开始向垂直时序场景延伸。Token 压缩工具 **headroom** 以单日 4,000+ stars 成为今日最大黑马，反映社区对降低 LLM 调用成本有极高刚需。Agent 领域继续分化：既有 **flue**、**superpowers** 等新框架出现，也有 **agent-native** 从框架层推动“Agent 原生应用”概念，Agent 技能化、工具化趋势明显。多模态视频生成再添新军，**LTX-2** 与 **OpenMontage** 分别从模型权重与 Agent 工作流两个方向攻占视频创作赛道。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars / 今日新增 | 一句话说明 |
|------|-----------------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐ 174,566 | 最流行的本地 LLM 运行工具，已支持 Kimi-2.6、GLM-5.1 等最新模型 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐ 83,370 | 高吞吐、内存高效的 LLM 推理与服务引擎，生产部署标配 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐ 139,726 | Agent 工程平台，提供链、工具、RAG 等全栈抽象 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐ 99,623 | 让 AI Agent 能像人一样操作网页，自动化任务利器 |
| [chopratejas/headroom](https://github.com/chopratejas/headroom) | ⭐ 0 (+4,005 today) | 为 LLM 输入做 token 压缩（工具输出、日志、RAG 块），降低 60‑95% 开销，输出不变 |
| [DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) | ⭐ 0 (+1,058 today) | 高性能代码智能 MCP 服务器：将代码库索引为知识图谱，毫秒级查询，158 语言 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐ 135,386 | 为 LLM 和 Agent 提供搜索、抓取、网页交互的 API，规模级数据管道 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars / 今日新增 | 一句话说明 |
|------|-----------------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐ 185,041 | 让 Agent 自主完成复杂任务的标志性项目，持续演化 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐ 197,699 | 与用户一同成长的 Agent，强调自我进化和持续学习 |
| [withastro/flue](https://github.com/withastro/flue) | ⭐ 0 (+309 today) | 沙盒 Agent 框架，为安全执行 Agent 代码提供隔离环境 |
| [obra/superpowers](https://github.com/obra/superpowers) | ⭐ 0 (+1,110 today) | Agent 技能框架 + 开发方法论，将技能抽象为可组合单元 |
| [BuilderIO/agent-native](https://github.com/BuilderIO/agent-native) | ⭐ 0 (+147 today) | “Agent 原生应用”框架，让应用从头为 Agent 设计 |
| [Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents) | ⭐ 5,995 | 原子化 Agent 构建库，小粒度组合，灵活度高 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐ 87,480 | 多 Agent 金融交易框架，LLM 驱动的量化 Trade |

### 📦 AI 应用（具体产品、垂直场景）

| 项目 | Stars / 今日新增 | 一句话说明 |
|------|-----------------|------------|
| [palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro) | ⭐ 0 (+756 today) | macOS 原生 AI 视频编辑器，专为 AI 创作流程打造 |
| [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) | ⭐ 0 (+156 today) | 首个开源 Agent 视频制作系统：52 工具、500+ Agent 技能，将代码助手转为视频工作室 |
| [Lightricks/LTX-2](https://github.com/Lightricks/LTX-2) | ⭐ 0 (+196 today) | 官方开源音频‑视频生成模型 LTX-2 的推理与 LoRA 微调包 |
| [koala73/worldmonitor](https://github.com/koala73/worldmonitor) | ⭐ 0 (+156 today) | AI 驱动的全球态势感知仪表盘，聚合新闻与地缘信息 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐ 47,559 | AI 生产力工作室：智能对话、自主 Agent、300+ 助手，统一入口 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐ 29,402 | AI 根据文档自动生成可编辑 PPT，含动画、讲稿音频 |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | ⭐ 44,464 | 轻量开源 AI 助手，适合工具集成与日常自动化 |

### 🧠 大模型 / 训练（模型权重、训练框架、微调、评测）

| 项目 | Stars / 今日新增 | 一句话说明 |
|------|-----------------|------------|
| [zai-org/GLM-5](https://github.com/zai-org/GLM-5) | ⭐ 0 (+480 today) | GLM-5 发布，口号从“Vibe Coding”转向“Agentic Engineering”，预示模型能力重心偏移 |
| [google-research/timesfm](https://github.com/google-research/timesfm) | ⭐ 0 (+1,510 today) | Google 的时间序列基础模型，预训练后可做通用时序预测 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐ 161,732 | 模型定义框架，支持文本/视觉/语音/多模态，训练与推理 |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐ 72,304 | 统一高效微调 100+ LLM & VLM，ACL 2024 论文级工具 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐ 7,107 | 大模型评测平台，覆盖 100+ 数据集、主流模型 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐ 265 | 预训练基础模型/世界模型的可靠、可扩展库，适合自研训练 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars / 今日新增 | 一句话说明 |
|------|-----------------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐ 83,202 | 领先的开源 RAG 引擎，融合 Agent 能力，构建 LLM 上下文层 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐ 61,825 | 本地优先的 Agent + RAG 平台，一站式私有部署 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐ 58,942 | AI Agent 通用记忆层，跨会话持久化 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐ 44,849 | 高性能云原生向量数据库，支撑大规模 ANN 检索 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | ⭐ 33,222 | 无需向量嵌入的“推理式 RAG”，文档索引新范式 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | ⭐ 17,913 | 自托管知识图谱引擎，给 AI 长期记忆 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐ 12,436 | MLsys 2026：在个人设备上实现 97% 存储节约的高效 RAG |

---

## 趋势信号分析

**1. Token 经济学成为社区最强烈的痛点**  
headroom 以单日 4,005 stars 断层领先，其“在数据到达 LLM 前压缩 60-95% 令牌”的承诺，直击开发者对 API 成本与上下文窗口的焦虑。同类项目如 codebase-memory-mcp（知识图谱索引减少重复 token）也引广泛关注，表明优化 LLM 输入效率正从“锦上添花”变成“刚需标配”。

**2. Agent 框架进入“技能化”与“原生化”阶段**  
superpowers（+1,110）提出 agentic skills 方法论；flue 专注沙盒安全；agent-native 从架构层面定义“为 Agent 而生”的应用。Agent 不再只是链式编排，而是开始拥有独立技能标准、安全运行环境和原生设计范式——这或许是下一代 Agent OS 的雏形。

**3. 视频生成成为多模态新战场**  
LTX-2 提供官方推理/微调包，OpenMontage 则将 Agent 与视频管线结合，palmier-pro 专注于桌面端剪辑体验。AI 视频创作正从“模型演示”走向“可用的产品”，且三种路线（模型、Agent 工作流、原生应用）同时登榜，说明生态正快速成熟。

**4. 时序基础模型首次进入热榜**  
TimesFM 代表 Google 将 Foundation Model 范式扩展到时间序列领域。这一信号预示着“通用时序预训练”可能变成继 LLM、ViT 之后的下一个基础模型风口，与产业 IoT、金融预测高度相关。

**5. 国产模型持续开源：GLM-5 跻身今日明星**  
GLM-5 发布的主题从“Vibe Coding”转向“Agentic Engineering”，暗示智谱正将模型定位从编码辅助转向 Agent 基础能力，也与当天多个 Agent 框架热潮形成呼应。

---

## 社区关注热点

- **headroom** —— 单日 4k+ stars，如果你的 Agent/RAG 应用被长上下文成本困扰，这个工具能直接节省 60% 以上 token 费用，值得立刻试用。
- **GLM-5** —— 智谱最新模型，标志着大模型从“聊天/编码”向“Agent 基础模型”演化，开发者应关注其 Tool-Use、规划等 Agent 原生能力。
- **superpowers** —— Agent 技能框架+方法论，如果你正在设计多 Agent 系统，该项目的“技能定义”范式能极大提高可复用性。
- **codebase-memory-mcp** —— MCP 生态再添重磅工具，用知识图谱加速代码理解，对使用 Claude/Copilot 的工程师有直接提效作用。
- **OpenMontage** —— 首个 Agent 视频生产系统，适合想用自然语言驱动视频制作的团队，其 52 工具 + 500 技能的架构设计也值得 Agent 开发者参考。

---

*数据来源：GitHub Trending (2026-06-20) 与 AI 主题搜索（tag: rag, llm, vector-db, ml, llm-model, ai-agent），已做 AI 相关性筛选与去重。 stars 量基于搜索数据，今日新增基于 Trending 榜单。*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*