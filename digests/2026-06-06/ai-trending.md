# AI 开源趋势日报 2026-06-06

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-06 02:50 UTC

---

#  AI 开源趋势日报 | 2026-06-06

## 🔍 今日速览
- **压缩与记忆成今日主旋律**：token 压缩工具 **headroom** 单日暴涨 2,473⭐，开源 NotebookLM **open-notebook** 收获 1,152⭐，Agent 记忆层 **MemPalace** 首次登榜并获 227⭐。
- **Agent 生态持续井喷**：Agent harness 类项目 **hermes‑agent**（+1,845⭐）、**ECC**（+1,361⭐）与 **last30days‑skill**（+731⭐）引领风潮；微软 Copilot SDK 及 OpenAI Plugins 同日更新。
- **物理 AI 开源里程碑**：NVIDIA **Cosmos** 世界模型平台开源（+479⭐），为机器人、自动驾驶等 physical AI 场景提供开箱即用的基础模型与工具。
- **文档 / 图像 → LLM 管道加速**：PaddleOCR（+747⭐）强调“将 PDF/图像结构化后喂给 LLM”，进一步推动多模态 RAG 落地。
- **向量数据库与 RAG 框架稳固增长**：Dify、Open WebUI、RagFlow 等成熟项目继续保持高关注，低存储成本方案 **LEANN** 也在细分赛道引起讨论。

---

## 📦 各维度热门项目

### 🔧 AI 基础工具（框架 · 推理引擎 · SDK · CLI）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-------------|
| [chopratejas/headroom](https://github.com/chopratejas/headroom) | 0 (新项目) | +2,473 | **今日最大黑马**，在 LLM 前压缩工具输出/日志/RAG chunk，减少 60‑95% token 且答案不变；已提供 Library、Proxy、MCP Server。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,024 | – | 高吞吐、低内存的 LLM 推理引擎，成为众多生产部署的标准后端。 |
| [ollama/ollama](https://github.com/ollama/ollama) | 173,287 | – | 一行命令离线运行大模型，现已支持 Kimi K2.6、GLM‑5.1、DeepSeek 等最新模型。 |
| [github/copilot-sdk](https://github.com/github/copilot-sdk) | 0 (新项目) | +309 | 官方发布的 GitHub Copilot Agent 多平台 SDK，便于将 Copilot 能力集成到自有应用。 |
| [openai/plugins](https://github.com/openai/plugins) | 0 | +49 | OpenAI 插件系统仓库更新，保持前沿的 Plugin 生态标准。 |
| [MemPalace/mempalace](https://github.com/MemPalace/mempalace) | 0 (新项目) | +227 | 宣称“最佳开源 AI 记忆系统”，是面向 Agent 的持久记忆中间件，免费且已通过全面基准测试。 |

### 🤖 AI 智能体 / 工作流（Agent 框架 · 多智能体 · Automation）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-------------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 183,269 | +1,845 | “与你一同成长的 Agent”，基于持续学习和上下文扩展，已成为社区最热 Agent 框架之一。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 208,415 | +1,361 | Agent harness 性能优化系统，集成技能、本能、记忆、安全模块，适配 Claude Code、Cursor、OpenCode 等多种环境。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 32,736 | +366 | Agent 与 Generative UI 的前端全栈方案（React/Angular），提出 AG‑UI 协议。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 97,382 | – | 让 AI 代理像人一样操控浏览器，实现自主网页自动化。 |
| [withastro/flue](https://github.com/withastro/flue) | 0 (新项目) | +126 | 沙箱化 Agent 框架，强调安全隔离与可控执行。 |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | 0 (新项目) | +731 | Agent 技能插件：自动搜索 Reddit、X、YouTube、HN、Polymarket 等多源数据，综合生成摘要报告。 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 0 (新项目) | +148 | 零 API 费为 Agent 提供全网“眼睛”，可读取与搜索 Twitter/Reddit/YouTube/GitHub/B 站/小红书等平台。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 75,941 | – | AI 驱动的软件开发协作者，直接操作终端、编辑器与浏览器完成编码任务。 |

### 📦 AI 应用（垂直场景 · 产品化 · 面向用户）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-------------|
| [lfnovo/open-notebook](https://github.com/lfnovo/open-notebook) | 0 (新项目) | +1,152 | **开源 NotebookLM**，支持多模型、更多灵活定制，可本地部署，今日爆发性增长。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 80,576 | +747 | 超轻量 OCR 工具，将 PDF/图片转为 LLM 可理解的结构化数据，支持 100+ 语言，成为 RAG 管道中的重要组件。 |
| [NVIDIA/cosmos](https://github.com/NVIDIA/cosmos) | 0 (新项目) | +479 | NVIDIA 开源的“世界模型”平台，包含预训练模型、数据集与工具，面向机器人、自动驾驶、智慧基础设施等物理 AI。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 83,181 | – | 多智能体对冲基金框架，大模型驱动的金融交易决策系统。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 24,648 | – | 根据任意文档一键生成真实可编辑的 PowerPoint，包含图形、动画和语音旁白。 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 68,661 | – | 面向分析师与 AI Agent 的金融数据平台，集成了多源行情与解析模块。 |
| [666ghj/MiroFish](https://github.com/666ghj/MiroFish) | 0 (新项目) | +320 | 通用群体智能引擎，基于群体涌现能力实现“预测万物”，架构简洁。 |

### 🧠 大模型 / 训练（模型权重 · 训练框架 · 微调 · 评估）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-------------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 100,537 | – | 深度学习框架事实标准，几乎覆盖所有 AI 训练/推理场景。 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 96,725 | – | 从零手写类 ChatGPT 的完整教程，PyTorch 实现，广受自学者欢迎。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 51,193 | – | 仅需 2 小时从零训练 64M 参数小 LLM 的极简教学项目。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,061 | – | 大模型评测平台，支持 Llama3、Qwen、GLM、GPT‑4 等 100+ 数据集。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 249 | – | 基础模型与“世界模型”的预训练库，稳定、可扩展，与 NVIDIA Cosmos 形成互补。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 58,062 | – | YOLOv8/v9 统一框架，训练部署视觉模型的首选。 |

### 🔍 RAG / 知识库（向量数据库 · 检索增强 · 知识管理）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|-------------|
| [langgenius/dify](https://github.com/langgenius/dify) | 144,071 | – | 生产级 Agentic Workflow + RAG 平台，可视化编排 LLM 应用。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 140,219 | – | 最受欢迎的自托管 AI 界面，内置全面 RAG 功能，支持 Ollama/OpenAI 等后端。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,001 | – | 前沿 RAG 引擎，融合 Agent 能力，提供企业级上下文层。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 57,832 | – | Agent 通用的深度记忆层，实现跨会话的上下文持久与知识更新。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 11,875 | – | MLsys 2026 论文成果：在保持高精度的同时节省 97% 存储，为个人设备与边缘端 RAG 提供可能。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,648 | – | 云原生向量数据库，支持百亿级向量高效检索，是 RAG 架构的核心存储层之一。 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,278 | – | 混合搜索向量数据库，支持对象 + 向量联合检索，与 LLM 原生集成。 |

---

## 📈 趋势信号分析

1. **Token 压缩与成本控制成为社区爆发点**  
   headroom 以单日 +2,473⭐ 登顶今日增长王，反映出团队在大量使用 LLM 后对成本的极致敏感。该项目提供 Library / Proxy / MCP Server 三种接入方式，直击企业级落地中的 token 开销痛点。类似地，ECC 的“harness 性能优化”也包含 token 减负功能，压缩方向正从单一工具升级为 Agent 基础设施标配。

2. **Agent 记忆与上下文管理走向系统化**  
   以 MemPalace、mem0、claude‑mem（未在 Trending 但主题搜索 ⭐80k）为代表，Agent 记忆层正在成为独立的基础组件。今日 MemPalace 首次登上 Trending，其“最佳开源记忆系统”的口号暗示这一赛道竞争加剧。last30days‑skill 则展示了 Agent 如何自主跨平台搜集信息并形成综合记忆，体现“记忆即技能”的新思路。

3. **物理 AI 开源生态破冰**  
   NVIDIA Cosmos 进入 Trending 是今日最值得关注的长期信号。它提供的世界模型、数据集与训练工具直接面向机器人、自动驾驶等物理世界交互场景。与之配套的 stable‑pretraining 等基础工具也在同一脉络上出现。这表明开源社区正从纯文本 / 代码智能向具身智能（Embodied AI）延伸。

4. **检索增强再升级：从向量到多模态与极简部署**  
   PaddleOCR 将 OCR 定义为“LLM 的结构化数据入口”，LEANN 则用 MLsys 级创新将 RAG 存储成本降低 97%。传统向量数据库（Milvus、Weaviate、Qdrant）持续热门，同时新方法（如 LEANN 的“无向量”方案）开始挑战主流范式，RAG 正在变得更轻、更全能。

---

## ⭐ 社区关注热点

- **headroom**（token 压缩）— 今日最多 ⭐，成本敏感型团队必试；支持 MCP 协议，与现有 Agent 框架无缝集成。
- **NousResearch/hermes-agent** — 保持每日常规 ⭐ 激增，其“持续成长”设计理念正影响新一代 Agent 框架。
- **NVIDIA/cosmos** — 物理 AI 开源的首个重磅平台，适合机器人 / 自动驾驶 / 智能基础设施方向的开发者关注。
- **StarTrail-org/LEANN** — 97% 存储压缩的 RAG 方案，适用于资源受限的边缘场景，是 RAG 落地的重要突破。
- **open-notebook** — NotebookLM 的开源平替，支持自定义模型与更灵活的功能，知识工作者的高效生产力工具。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*