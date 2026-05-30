# AI 开源趋势日报 2026-05-30

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-05-30 02:47 UTC

---

# 《AI 开源趋势日报》2026-05-30

---

## 一、今日速览

- 今日 GitHub Trending 上，**AI 短视频生成**（MoneyPrinterTurbo，+3,567 stars）继续领跑，AIGC 视频热度不减。
- **Agent 技能优化工具**异军突起：Taste-Skill（+2,062 stars）和 Stop-Slop（+617 stars）分别从“赋予品味”和“去除套话”角度精细调控 LLM 输出质量，社区对 Agent 行为控制的需求强烈。
- **Claude Code 生态加速成型**：Compound Engineering Plugin（+353 stars）与 Cursor 插件（+134 stars）等标准化插件规范亮相，推动 AI 编程工具的互操作性。
- **文档解析新范式**：基于 Rust 的快速文档解析器 Liteparse（+701 stars）切入 RAG 管道前端，引发关注。
- **世界模型与预训练基础设施建设**：Stable-Worldmodel（+362 stars）与 Stable-Pretraining 双双上榜，可重复、标准化的基础模型研究平台成为新焦点。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架 / SDK / 推理引擎 / 开发插件）

1. [ollama/ollama](https://github.com/ollama/ollama) — ⭐172,622  
   本地大模型运行工具，支持 Kimi‑K2.5、GLM‑5、DeepSeek 等最新模型，是个人开发者实验 LLM 的首选入口。

2. [vllm-project/vllm](https://github.com/vllm-project/vllm) — ⭐81,387  
   高吞吐、内存高效的 LLM 推理与服务引擎，生产环境部署的事实标准。

3. [huggingface/transformers](https://github.com/huggingface/transformers) — ⭐161,051  
   多模态模型加载、训练与推理的统一框架，持续引领开源模型生态。

4. [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) — 今日 +353  
   为 Claude Code、Codex、Cursor 等 Agent 编码工具提供统一插件规范，推动跨平台能力复用。

5. [cursor/plugins](https://github.com/cursor/plugins) — 今日 +134  
   Cursor 编辑器官方插件系统，通过扩展点增强 AI 辅助编程体验。

6. [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) — ⭐7,460  
   Rust 生态中的 LLM 应用模块化框架，以高性能和安全性吸引系统开发者。

7. [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) — ⭐31,842  
   Agent 前端框架（React + Angular），让开发者快速在应用中嵌入 Copilot 式交互。

---

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、技能系统）

1. [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) — ⭐184,647  
   自主智能体概念的开山之作，至今仍是 Agent 框架的重要参考。

2. [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — ⭐172,914  
   强调“与你一同成长”的 Agent，注重个性化记忆与长期适配。

3. [browser-use/browser-use](https://github.com/browser-use/browser-use) — ⭐96,211  
   让 AI Agent 操作浏览器自动完成线上任务，Web 自动化方向的明星项目。

4. [anthropics/claude-code](https://github.com/anthropics/claude-code) — 今日 +395  
   Anthropic 出品的终端 Agent 编程工具，理解代码库、执行 Git 工作流，以自然语言驱动开发。

5. [bytedance/deer-flow](https://github.com/bytedance/deer-flow) — ⭐69,965  
   字节跳动开源的长时序超级 Agent，集成研究、编程、工具调用等能力，适合复杂任务。

6. [affaan-m/ECC](https://github.com/affaan-m/ECC) — ⭐198,625（今日 +1,406）  
   Agent 性能优化系统，涵盖技能、本能、记忆、安全等模块，兼容 Claude Code、Codex 等主流工具。

7. [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) — 今日 +2,062  
   通过定义 taste skill 文件让 AI 输出不再“无聊、套话”，今日第二热项目。

8. [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) — 今日 +617  
   专注于去除 AI 文本中的空洞表达，与 taste-skill 形成“破立”组合。

---

### 📦 AI 应用（具体产品 / 场景方案）

1. [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) — 今日 +3,567  
   利用大模型一键生成高清短视频，AIGC 视频赛道最热项目。

2. [twentyhq/twenty](https://github.com/twentyhq/twenty) — 今日 +578  
   开源 AI‑native CRM，旨在替代 Salesforce，面向销售流程的智能增强。

3. [open-webui/open-webui](https://github.com/open-webui/open-webui) — ⭐139,203  
   功能丰富的 LLM 前端，支持 Ollama / OpenAI 等多种后端，是个人部署 AI 聊天界面的首选。

4. [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) — ⭐46,574  
   多功能 AI 生产力工作室，集成聊天、自主 Agent、300+ 助手，一站式接入前沿模型。

5. [Crosstalk-Solutions/project-nomad](https://github.com/Crosstalk-Solutions/project-nomad) — 今日 +318  
   离线生存电脑，内置 AI 工具与知识库，主打无网络环境下的智能辅助。

6. [santifer/career-ops](https://github.com/santifer/career-ops) — ⭐47,839  
   AI 求职系统，基于 Claude Code 的 14 种技能模式，实现批量申请与 PDF 生成。

7. [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) — ⭐22,475  
   从任意文档直接生成可编辑 PowerPoint，原生形状与动效，支持自定义模板。

---

### 🧠 大模型 / 训练（权重、微调、预训练、评估）

1. [pytorch/pytorch](https://github.com/pytorch/pytorch) — ⭐100,263  
   深度学习主力框架，绝大多数学术与产业模型的训练基石。

2. [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) — ⭐71,701  
   统一高效微调 100+ 大语言模型与视觉语言模型（ACL 2024），是社区最流行的微调工具。

3. [galilai-group/stable-worldmodel](https://github.com/galilai-group/stable-worldmodel) — 今日 +362  
   可复现的世界模型研究与评估平台，旨在标准化智能体世界模型的实验流程。

4. [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) — ⭐238  
   配套的可靠、最小化、可扩展基座模型预训练库，与 worldmodel 形成完整研究工具链。

5. [open-compass/opencompass](https://github.com/open-compass/opencompass) — ⭐7,047  
   大模型全维度评测平台，支持 100+ 数据集，是衡量模型能力的权威工具。

6. [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) — ⭐4,216  
   从零实现 LLM 推理服务的教学项目，在 Apple Silicon 上打造极简 vLLM+Qwen，系统工程师必看。

7. [Biohub/esm](https://github.com/Biohub/esm) — 今日 +52  
   蛋白质语言模型（Evolutionary Scale Modeling），将 AI 应用于生物学序列理解。

---

### 🔍 RAG / 知识库（检索增强、向量数据库、记忆层）

1. [infiniflow/ragflow](https://github.com/infiniflow/ragflow) — ⭐81,530  
   领先的开源 RAG 引擎，深度融合 Agent 能力，为 LLM 提供高质量上下文层。

2. [run-llama/llama_index](https://github.com/run-llama/llama_index) — ⭐49,763  
   文档 Agent 与 OCR 平台，是构建 RAG 系统的核心框架之一。

3. [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) — ⭐78,973  
   轻量级 OCR 工具，将图像/PDF 转化为 LLM 可用的结构化数据，支持 100+ 语言。

4. [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) — ⭐35,965  
   EMNLP 2025 录用论文的官方实现，以简单、快速著称的 RAG 方案。

5. [mem0ai/mem0](https://github.com/mem0ai/mem0) — ⭐57,101  
   AI Agent 的通用记忆层，帮助 Agent 实现跨会话持久化上下文。

6. [milvus-io/milvus](https://github.com/milvus-io/milvus) — ⭐44,537  
   云原生向量数据库，支撑大规模向量 ANN 检索及 AI 应用。

7. [run-llama/liteparse](https://github.com/run-llama/liteparse) — 今日 +701  
   基于 Rust 的快速文档解析器，专注于为 Agent 和 RAG 管道提供预处理，兼具性能与易用性。

---

## 三、趋势信号分析

从今日热榜中提取出几个明确的信号：

1. **Agent 技能工程爆发**：Taste-Skill 和 Stop-Slop 分别以日增 2,062 和 617 星冲入 Trending，说明社区已不满足于“能用”，而是追求“用得好”——微调 Agent 的语言风格、去除模板化表达成为新的优化方向。这与 ECC 等“Agent 性能调优”系统形成互补，指向一个更成熟的 Agent 工程化阶段。

2. **Claude Code 生态快速成型**：Compound Engineering Plugin、Cursor/plugins 等标准化插件规范的出现，意味着 Agent 编程工具正在从单点走向互联。结合 Claude Code 自身 395 星/日的增长，Anthropic 正围绕终端编程场景构建新的工具链生态。

3. **文档解析向“轻量+高速”演进**：Liteparse 以 Rust 重写解析内核，日增 701 星；配合 PaddleOCR 的稳定地位和 LightRAG 的学术热度，RAG 前端的数据处理环节正在经历效率和用户体验的升级。

4. **世界模型与基础模型预训练基础设施化**：Stable-Worldmodel 和 Stable-Pretraining 的同时上榜，表明业界开始追求可复现、最小化、标准化的世界模型实验平台，呼应了近期对“基础模型科学”的呼吁。

5. **离线与本地优先的 AI 应用**：Project-Nomad 主打“无网生存 AI”，Ollama 持续高星，open-webui 部署广泛，反映出开发者对数据主权和离线场景的持续重视。

---

## 四、社区关注热点

- **Agent 技能文件生态（Taste-Skill / Stop-Slop）**：轻量级配置文件能够大幅改善 AI 输出质量，且可与 Claude Code、Cursor 等主流工具直接集成，建议探索如何将其纳入自己的 Agent 工作流。
- **Claude Code 与通用插件规范**：Compound Engineering Plugin 提供了一种跨 Agent 编程工具的插件编写标准，值得关注其在多工具协作中的潜在应用。
- **LlamaFactory 微调框架**：以 71k+ 星持续领跑，统一的微调接口覆盖 100+ 模型，是定制化 LLM 的首选工具。
- **Rust 在 AI 基础设施中的渗透**：Rig（LLM 框架）、Liteparse（文档解析）、Qdrant（向量数据库）等 Rust 项目频频上榜，语言的高性能和安全性正受到 AI 工程界的青睐。
- **终身记忆层（mem0 / claude-mem）**：为 Agent 添加跨会话记忆是当前 RAG 之外的重要方向，mem0 的 57k 星和 claude-mem 的 79k 星说明了社区对持久上下文的迫切需求。

---

*以上为 2026‑05‑30 的《AI 开源趋势日报》，所有选入项目均经过 AI/ML 相关性筛选，分类基于项目主要定位。*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*