# AI 开源趋势日报 2026-06-02

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-02 03:39 UTC

---

# AI 开源趋势日报 - 2026‑06‑02

## 1. 今日速览

- 短视频生成工具 **MoneyPrinterTurbo** 凭借单日 +3,375 Stars 登顶今日 Trending，AI 内容创作依然是社区最火爆的应用方向。
- 语音生成模型 **VoxCPM**（+888 Stars）采用 Tokenizer‑Free 架构，支持多语言语音生成、创意声音设计与声音克隆，推动 TTS 技术向前。
- 智能体（Agent）赛道持续升温：**TradingAgents** 多智能体金融交易框架（+299）、**harness** 元技能自动设计 Agent 团队（+524）、**oh‑my‑pi** 终端编码 Agent（+335）等新工具集中出现，Agent 正向垂直场景和自动化构建演进。
- 记忆与 RAG 层迎来新血液：**supermemory**（+647 Stars）致力于为 AI 提供超快速、可扩展的记忆 API，结合 **PageIndex** 等“无向量”RAG 理念，知识检索正从纯向量转向推理驱动。
- 训练入门教程 **train‑llm‑from‑scratch**（+861 Stars）及 **minimind**（50k Stars）证明，开发者对低成本自训 LLM 的需求与日俱增。

## 2. 各维度热门项目

### 🔧 AI 基础工具

1. [pytorch/pytorch](https://github.com/pytorch/pytorch) ⭐100,323  
   动态神经网络与 GPU 加速的深度学习框架，AI 研究与生产的基石。

2. [huggingface/transformers](https://github.com/huggingface/transformers) ⭐161,180  
   提供数千种预训练模型（文本、视觉、多模态）的框架，业界标准。

3. [vllm-project/vllm](https://github.com/vllm-project/vllm) ⭐81,641  
   高吞吐、内存高效的 LLM 推理引擎，被广泛用于模型部署。

4. [ollama/ollama](https://github.com/ollama/ollama) ⭐172,871  
   一键本地运行大模型（支持 Kimi、DeepSeek、Qwen 等），社区首选。

5. [dmtrKovalenko/fff](https://github.com/dmtrKovalenko/fff) ⭐0（今日 +135）  
   针对 AI Agent 优化的超快速文件搜索工具（Rust），兼顾速度与准确性。

6. [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) ⭐0（今日 +417）  
   Claude Code、Codex、Cursor 等 AI 编程工具的官方工程插件，扩展 IDE 能力。

### 🤖 AI 智能体/工作流

1. [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) ⭐184,707  
   自主 Agent 先驱，提供可扩展的通用任务自动化框架。

2. [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) ⭐176,168  
   主打“与您一同成长”的智能体，今日其 WebUI 项目（hermes‑webui）获 945 Stars。

3. [langchain-ai/langchain](https://github.com/langchain-ai/langchain) ⭐138,262  
   智能体工程平台，统一 LLM 调用、工具使用与 RAG 集成。

4. [browser-use/browser-use](https://github.com/browser-use/browser-use) ⭐96,595  
   让 AI Agent 直接操作浏览器，在线任务自动化利器。

5. [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) ⭐75,618  
   AI 驱动的软件开发 Agent，从编码到测试全流程辅助。

6. [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) ⭐81,867（今日 +299）  
   多智能体 LLM 量化交易框架，将 Agent 与金融决策结合。

7. [revfactory/harness](https://github.com/revfactory/harness) ⭐0（今日 +524）  
   “元技能”系统，能自动分析领域需求并生成专属 Agent 团队与技能。

8. [can1357/oh-my-pi](https://github.com/can1357/oh-my-pi) ⭐0（今日 +335）  
   终端 AI 编码 Agent，支持哈希锚定编辑、LSP、Python、浏览器、子代理等。

### 📦 AI 应用

1. [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) ⭐0（今日 +3,375）  
   利用 AI 大模型一键生成高清短视频，内容创作提效神器。

2. [OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM) ⭐0（今日 +888）  
   无分词器多语言 TTS 模型，支持创意声音设计与真实感语音克隆。

3. [p-e-w/heretic](https://github.com/p-e-w/heretic) ⭐0（今日 +249）  
   全自动语言模型审查内容移除工具，引发 AI 安全与言论自由讨论。

4. [pbakaus/impeccable](https://github.com/pbakaus/impeccable) ⭐0（今日 +485）  
   专为 AI Harness 优化的设计语言系统，提升 AI 界面的美学与一致性。

5. [open-webui/open-webui](https://github.com/open-webui/open-webui) ⭐139,585  
   最流行的本地 AI 聊天前端，完美对接 Ollama 及 OpenAI API。

6. [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) ⭐46,728  
   多功能 AI 生产力工具，集成智能对话、自主 Agent 与 300+ 预设助手。

7. [f/prompts.chat](https://github.com/f/prompts.chat) ⭐163,167  
   ChatGPT 提示词社区，免费开源，支持自托管与企业私有部署。

### 🧠 大模型/训练

1. [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) ⭐71,779  
   统一高效微调框架（ACL 2024），覆盖 100+ LLM 与 VLM。

2. [FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) ⭐0（今日 +861）  
   完整教程：从数据采集到模型生成，手把手训练自己的 LLM。

3. [jingyaogong/minimind](https://github.com/jingyaogong/minimind) ⭐50,973  
   2 小时从零训练 64M 参数小模型，极大降低预训练入门门槛。

4. [open-compass/opencompass](https://github.com/open-compass/opencompass) ⭐7,054  
   大模型评估平台，支持 Llama3、Qwen、GPT‑4 等 100+ 数据集评测。

### 🔍 RAG/知识库

1. [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) ⭐60,917  
   一站式 AI 生产力工具，本地优先、隐私第一，轻松搭建个人知识库。

2. [infiniflow/ragflow](https://github.com/infiniflow/ragflow) ⭐81,683  
   领先的开源 RAG 引擎，结合深度文档理解与 Agent 能力。

3. [run-llama/llama_index](https://github.com/run-llama/llama_index) ⭐49,834  
   文档 Agent 与 OCR 平台，构建高质量 RAG 管道的标准方案。

4. [milvus-io/milvus](https://github.com/milvus-io/milvus) ⭐44,582  
   高性能云原生向量数据库，支撑大规模近似最近邻搜索。

5. [mem0ai/mem0](https://github.com/mem0ai/mem0) ⭐57,344  
   AI Agent 通用记忆层，解决长期上下文保持与个性化问题。

6. [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) ⭐36,050  
   轻量高速 RAG 框架（EMNLP 2025），简化检索增强生成实现。

7. [supermemoryai/supermemory](https://github.com/supermemoryai/supermemory) ⭐0（今日 +647）  
   专为 AI 时代打造的记忆引擎，提供极速、可扩展的 Memory API。

8. [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) ⭐32,425  
   无向量、基于推理的 RAG 系统，号称节省 97% 存储且保持高准确率。

## 3. 趋势信号分析

从今日 Trending 榜单看，AI 开源社区呈现以下信号：

- **AI 应用层仍是流量吸铁石**：视频生成（MoneyPrinterTurbo +3,375）和语音合成（VoxCPM +888）这类直接面向用户的内容生成工具最容易引爆星星增长，说明开发者对“开箱即用”的 AI 产品保持极高热情。
- **智能体（Agent）向工程化与垂直化演进**：除了传统的通用框架（AutoGPT、LangChain），今天涌现出大量面向特定场景的 Agent 工具：金融交易（TradingAgents）、团队组建（harness）、终端编码（oh‑my‑pi）、工程插件（compound‑engineering‑plugin）。Agent 不再只是 demo，正在融入开发者的实际工作流。
- **“元技能”与自生成 Agent 成为新范式**：harness（+524 Stars）通过元技能自动设计 Agent 团队并生成所需技能，代表了一种 Agent 自动化的新思路，可能引领下一波 Agent 框架的变革。
- **RAG 技术栈从向量检索走向“记忆+推理”**：supermemory（+647 Stars）和 PageIndex（32k Stars）分别从可扩展记忆层和免向量推理两个方向挑战传统 RAG，反映出社区不再满足于单纯的向量数据库，更追求高效、低成本的上下文管理。
- **入门级 LLM 训练需求旺盛**：train‑llm‑from‑scratch（+861 Stars）和 minimind（51k Stars）主打“低成本、低门槛”训练，呼应了大量开发者希望掌握模型微调乃至预训练技能的长期诉求。

## 4. 社区关注热点

- **hermes‑webui**（[nesquena/hermes-webui](https://github.com/nesquena/hermes-webui)）—— 为高人气的 hermes‑agent 带来 Web 与移动端访问，上线首日即获近千 Star，值得体验。
- **revfactory/harness**（[revfactory/harness](https://github.com/revfactory/harness)）—— “元技能”概念新颖，能自动构建 Agent 团队，可能成为 Agent 开发的新范式。
- **supermemory**（[supermemoryai/supermemory](https://github.com/supermemoryai/supermemory)）—— 极速 AI 记忆引擎，旨在替代复杂 RAG 管线，关注其能否成为 Agent 长期记忆的标准方案。
- **compound‑engineering‑plugin**（[EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)）—— 体现 AI 编码助手生态向插件化发展，类似 IDE 扩展模式，有潜力提高工程效率。
- **train‑llm‑from‑scratch**（[FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch)）—— 最适合入门 LLM 训练的教程项目之一，从数据到生成全链路覆盖，所有资源开源。

---

*报告生成时间：2026‑06‑02 · 数据来源：GitHub Trending & Topic Search*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*