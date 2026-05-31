# AI 开源趋势日报 2026-05-31

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-05-31 03:31 UTC

---

# 🔥 AI 开源趋势日报｜2026-05-31

---

## 一、今日速览

1. **视频 + 语音生成全面井喷**：`MoneyPrinterTurbo` 以单日 +2,768 stars 领跑 Trending，VoxCPM（+779）与 MOSS-TTS（+62）同期发力，多模态内容创作成为社区最热赛道。
2. **Agent 生态系统从「单体」走向「工程化」**：ECC（+908）、Claude Code（+592）、Anthropic Skills（+454）及各类插件（compound‑engineering +349）同时上榜，开发者正聚焦 Agent 的性能、技能标准化与工具链整合。
3. **文档解析层迎来新突破**：LlamaIndex 团队的 `liteparse` 首日即获 +925 stars，高速、开源的文档解析能力让 RAG 与 Agent 数据管线更健壮。
4. **前沿研究方向进入开源视野**：`stable‑worldmodel`（世界模型平台）与 `RuView`（WiFi 信号空间智能）首次登榜，预示 AI 正从纯语言迈向物理感知与基础模型评估。
5. **训练与微调工具持续受关注**：`train‑llm‑from‑scratch`（+327）提供低门槛全流程教程，结合老牌微调框架 `LlamaFactory`（71k stars），LLM 定制化需求依然旺盛。

---

## 二、各维度热门项目

### 🔧 AI 基础工具

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama](https://github.com/ollama/ollama) | ⭐172,689 | 本地大模型运行平台，支持 Kimi、DeepSeek 等最新模型，零门槛部署。 |
| [liteparse](https://github.com/run-llama/liteparse) | ⭐今日+925 | LlamaIndex 出品的高速开源文档解析器，为 RAG/Agent 提供标准化数据输入。 |
| [vllm](https://github.com/vllm-project/vllm) | ⭐81,452 | 高吞吐、低延迟的 LLM 推理引擎，被大量生产环境采用。 |
| [firecrawl](https://github.com/firecrawl/firecrawl) | ⭐126,561 | 专为 AI Agent 设计的网页搜索与抓取 API，让模型安全地访问互联网。 |
| [cursor/plugins](https://github.com/cursor/plugins) | ⭐今日+205 | Cursor IDE 插件规范与官方插件，进一步扩展 AI 编程能力边界。 |

### 🤖 AI 智能体 / 工作流

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐199,410 (今日+908) | Agent 性能优化系统（Skills/Instincts/Memory），兼容 Claude Code、Cursor 等主流 Agent。 |
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | ⭐今日+592 | Anthropic 官方终端 Agent，理解代码库并自动执行编码、Git 等任务。 |
| [dify](https://github.com/langgenius/dify) | ⭐143,212 | 生产级 Agentic 工作流开发平台，可视化编排 LLM 应用。 |
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐184,659 | 经典自主 Agent 项目，持续引领 AI 自动化探索。 |
| [anthropics/skills](https://github.com/anthropics/skills) | ⭐今日+454 | 官方推出的 Agent Skills 仓库，为智能体能力标准化奠定基础。 |
| [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | ⭐今日+349 | 为 Claude Code、Codex、Cursor 提供复合工程能力，Agent 插件生态快速扩展。 |
| [revfactory/harness](https://github.com/revfactory/harness) | ⭐今日+55 | 元技能设计工具，可定义领域专用 Agent 团队并自动生成技能。 |

### 📦 AI 应用

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐今日+2,768 | 利用大模型一键生成高清短视频，热度断层领先。 |
| [VoxCPM](https://github.com/OpenBMB/VoxCPM) | ⭐今日+779 | Tokenizer‑free 多语言语音生成与克隆，支持创意语音设计。 |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | ⭐今日+655 | 通过 WiFi 信号实现空间感知、生命体征监测，不依赖摄像头。 |
| [project-nomad](https://github.com/Crosstalk-Solutions/project-nomad) | ⭐今日+469 | 离线智能生存套件，集成 AI 知识库、工具链，可脱离网络运行。 |
| [MOSS-TTS](https://github.com/OpenMOSS/MOSS-TTS) | ⭐今日+62 | 开源语音/音效生成模型家族，覆盖长文、对话、实时流等复杂场景。 |
| [TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐81,031 | 多智能体金融交易框架，将 LLM 用于量化决策。 |
| [anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐60,814 | 全功能 AI 生产力工具，本地优先，开箱即用。 |

### 🧠 大模型 / 训练

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) | ⭐今日+327 | 从数据下载到文本生成，一条清晰的 LLM 全流程训练教程。 |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐71,730 | 统一高效微调 100+ 大语言模型与视觉语言模型（ACL 2024）。 |
| [galilai-group/stable-worldmodel](https://github.com/galilai-group/stable-worldmodel) | ⭐今日+318 | 可复现的世界模型研究与评估平台，推动基础模型标准化测试。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,048 | 支持 100+ 数据集的大模型评测框架，覆盖主流闭源/开源模型。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐238 | 轻量、可靠的基础模型预训练库，搭配世界模型使用。 |

### 🔍 RAG / 知识库

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐81,570 | 领先开源 RAG 引擎，融合 Agent 能力构建 LLM 上下文层。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐44,550 | 高性能云原生向量数据库，支撑大规模 ANN 检索。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐57,163 | 通用 AI Agent 记忆层，6 行代码实现持久化记忆。 |
| [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) | ⭐35,985 | 简单快速的 RAG（EMNLP 2025），以图结构增强检索质量。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐79,774 | 跨会话上下文压缩与注入，为 Claude Code 等 Agent 提供「记忆」能力。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | ⭐79,091 | 支持 100+ 语言的 OCR 工具，将图像/PDF 精准转换为 LLM 可读的结构化数据。 |

---

## 三、趋势信号分析

今日 Trending 榜单清晰地反映出 AI 开源的几个结构性变化：

1. **Agent 工程化成为主旋律**——ECC、Claude Code、Skills 等项目的集中涌现表明，社区已从「跑通一个 Agent Demo」转向「让 Agent 稳定、高效、可组合」。Agent Harness、性能优化、技能标准开始成为新一代基础设施。Anthropic 官方推动的 Skills 仓库与各插件生态（compound‑engineering、Cursor plugins）正在形成事实标准。

2. **多模态生成进入「一键化」阶段**——`MoneyPrinterTurbo` (视频) 与 `VoxCPM`/`MOSS-TTS` (语音) 的同时爆发，意味着大模型驱动的创意工具已降低到普通用户可用的门槛。这背后是底层 TTS、视频合成模型的成熟与工程封装。

3. **文档解析层价值凸显**——`liteparse` 以 +925 stars 首日冲榜，反映 RAG 与 Agent 对高质量、结构化文本输入的迫切需求。文档解析正从辅助工具上升为关键中间层，与向量数据库、记忆层构成「数据三角」。

4. **新兴方向：世界模型与非视觉感知**——`stable‑worldmodel` 为世界模型提供标准化评估平台，`RuView` 利用 WiFi 信号实现空间智能。这两个项目首次进入大众视野，预示 AI 正在向物理世界理解和多模态感知延伸，可能成为下一阶段的研究热点。

5. **与近期行业事件的联动**——Claude Code 发布后，相关技能、插件、记忆项目（ECC、skills、claude‑mem）迅速跟进，体现了官方 Agent 发布对开源生态的强拉动效应。

---

## 四、社区关注热点

- **🏆 ECC（Agent 性能优化）** — 以 199k 总 stars + 今日 908 新增高居 Agent 类第一。它不只优化速度，更涵盖技能、记忆、安全等维度，是构建生产级 Agent 无法绕过的参考实现。
- **🎬 MoneyPrinterTurbo（一键视频生成）** — 单日 2768 stars 说明「LLM + 视频」的想象空间仍然巨大。值得关注其背后的模型调用链路与素材生成方案。
- **📄 liteparse（文档解析新标准）** — +925 stars 来自 LlamaIndex 团队，专为 Agent/RAG 场景设计。随着文档格式日益复杂，轻量、准确的解析器将成为 AI 数据管线的基础组件。
- **🧠 stable‑worldmodel（世界模型平台）** — +318 stars，代表开源世界从「语言模型」向「环境模型」的拓展。值得关注其评测标准对行业的影响。
- **🔌 Anthropic Skills & Plugin 生态** — 官方 Skills 仓库（+454）与 compound‑engineering 插件（+349）标志着 Agent 能力正在模块化、标准化。开发者可基于这些 skill 快速组装自有 Agent，降低重复开发成本。

---

*数据来源：GitHub Trending 2026-05-31 + GitHub Search API (topic 标签，7天活跃项目)*

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*