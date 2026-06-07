# AI 开源趋势日报 2026-06-07

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-07 03:35 UTC

---

# AI 开源趋势日报 | 2026-06-07

## 1. 今日速览

- **Agent 技能化浪潮集中爆发**：CopilotKit（+631）、Agent-Reach（+683）、Superpowers（+700）等 Agent 基础设施项目今日获大量新增，社区正从通用 Agent 转向“技能 + 工具 + 方法论”的专业分工。
- **记忆系统与知识管理升温**：开源 NotebookLM 替代品 **open-notebook**（+794）摘得今日新增冠军，AI 记忆系统 **MemPalace**（+446）同步登榜；同时 **mem0**、**claude-mem** 等 RAG 记忆项目持续走红，Agent 长期上下文问题成为关注焦点。
- **语音 AI 双雄竞逐**：微软开源 **VibeVoice**（+216）与 OpenAI **Whisper**（+150）同时出现在热榜，语音模态正在快速成为 Agent 标配。
- **OpenAI 重启插件生态**：**openai/plugins** 仓库今日更新（+213），第三方能力扩展标准化或迎来新阶段。
- **传统 RAG 与新生融合**：Dify、Open WebUI 等稳居百万量级，但 Agent-Reach、MemPalace 等以“零 API 费多源检索”和“记忆优先”切入，揭示 RAG 正向动态、记忆增强的 Agent 系统演进。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐138,681  
  LLM 应用编排框架，集 Agent、RAG、工具于一体，生态最广的 LLM 中间件。

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,363  
  模型定义与训练标准库，支持几乎所有 SOTA 模型，新模型发布首选。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,088  
  高吞吐、低延迟 LLM 推理引擎，生产部署的事实标准。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐57,906  
  通用 AI 记忆层，为 Agent 提供跨会话的长期上下文保持。

- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐129,574  
  大规模 Web 抓取 API，让 LLM 和 Agent 轻松获取实时网络数据。

- **[openai/plugins](https://github.com/openai/plugins)** ⭐0（今日+213）  
  OpenAI 插件开放仓库，第三方扩展生态核心，今日更新获关注。

---

### 🤖 AI 智能体 / 工作流

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,801  
  自主 AI Agent 先驱，长期引领 Agent 开源社区方向。

- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐76,045  
  AI 驱动软件开发，自动完成代码编写、调试等任务，Agent 落地的典型范例。

- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐33,271（今日+631）  
  前端 Agent 与生成式 UI 框架，提出 AG-UI 协议，覆盖 React、Angular 等，今日热度极高。

- **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)** ⭐53,385  
  可视化构建 AI Agent，低门槛拖拉拽即可搭建复杂工作流。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐97,508  
  让 AI 自主操控浏览器，网页自动化与 Agent 感知的关键工具。

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐新项目（今日+439）  
  Agent 技能，跨 Reddit、X、YouTube 等多平台聚合信息并生成总结，技能化代表。

- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** ⭐新项目（今日+683）  
  让 Agent 读取 Twitter、B 站、小红书等全网内容，零 API 费，今日爆炸式增长。

- **[obra/superpowers](https://github.com/obra/superpowers)** ⭐新项目（今日+700）  
  Agent 技能框架与软件开发方法论，重新定义人与 Agent 的协作方式。

---

### 📦 AI 应用

- **[lfnovo/open-notebook](https://github.com/lfnovo/open-notebook)** ⭐新项目（今日+794）  
  开源 NotebookLM 实现，更灵活的功能和定制性，今日新增量最高。

- **[microsoft/VibeVoice](https://github.com/microsoft/VibeVoice)** ⭐新项目（今日+216）  
  微软开源的语音 AI，前沿语音交互，与 Whisper 正面竞争。

- **[openai/whisper](https://github.com/openai/whisper)** ⭐0（今日+150）  
  鲁棒语音识别模型，作为 LLM 语音输入的前置工具长期活跃。

- **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐81,009（今日+433）  
  将 PDF、图片转为 LLM 可用结构化数据的 OCR 工具，连接物理与数字。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐83,616  
  多智能体金融交易框架，将 LLM 代理用于量化决策。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐46,987  
  AI 生产力工作室，聚合 300+ 助手与多模型，统一管理 Agent 任务。

- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐49,437（今日+193）  
  AI 驱动的求职系统，14 种技能模式，集成了 Claude Code 自动化。

---

### 🧠 大模型 / 训练

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐96,778  
  从零实现 ChatGPT 的完整教程，PyTorch 逐行构建，学习 LLM 必备。

- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐51,247  
  2 小时从零训练 64M 参数小 LLM，极致轻量的入门实践。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,062  
  面向 LLM 的全面评估平台，支持 100+ 数据集和多模型。

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,252  
  学习 LLM 推理服务的系统实现课程，从零搭建 tiny vLLM + Qwen。

---

### 🔍 RAG / 知识库

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐144,189  
  生产级 RAG + Agentic Workflow 开发平台，企业级首选。

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐140,392  
  用户友好的 AI 界面，深度集成 Ollama，社区使用最广的 RAG 前端。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,052  
  领先的开源 RAG 引擎，融合 Agent 能力，构建 LLM 上下文层。

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐61,163  
  本地优先、隐私保护的 Agent 体验，一切 LLM 所需集成一体。

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐80,997  
  跨会话上下文记忆，被 Claude Code、OpenClaw 等多 Agent 使用。

- **[MemPalace/mempalace](https://github.com/MemPalace/mempalace)** ⭐新项目（今日+446）  
  基准测试最佳的免费 AI 记忆系统，专为 Agent 持久记忆设计。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,662  
  高性能云原生向量数据库，RAG 检索层核心基础设施。

---

## 3. 趋势信号分析

今日数据清晰反映开源社区正从“对话式 AI”向 **“Agent 全栈能力”** 跃迁。**技能化**是最强信号：`last30days-skill`（垂直调研）、`Agent-Reach`（多源感知）、`Superpowers`（开发方法论）等非通用 Agent 项目集中爆发，表明社区不再满足于单一聊天机器人，而是构建能调用工具、搜索网络、记忆上下文的专业 Agent 组件。**记忆层**成为新基建，`MemPalace` 与 `mem0` 同时在热榜与主题搜索中高位出现，长期上下文是 Agent 从 Demo 走向实用必须跨越的瓶颈。微软 `VibeVoice` 与 OpenAI `Whisper` 同台竞逐，预示**语音交互**即将成为 Agent 标配模块，多模态 Agent 雏形初现。**RAG 与 Agent 融合**明显：`Agent-Reach` 实现零费用检索多个平台，突破传统 RAG 成本限制；`Dify`、`RAGFlow` 等老牌项目也纷纷加入 Agent 工作流能力。整体上，Agent 正沿着“感知层（搜索/浏览器）→ 记忆层 → 技能层 → 编排层”全栈演进，今日榜单是一份完整的 Agent 基础设施投资地图。

---

## 4. 社区关注热点

- **[open-notebook（lfnovo/open-notebook）](https://github.com/lfnovo/open-notebook)**  
  NotebookLM 最强开源替代，支持自定义模型与插件，适合搭建个人知识助理。

- **[Agent-Reach（Panniantong/Agent-Reach）](https://github.com/Panniantong/Agent-Reach)**  
  零 API 费用、多平台（Twitter、B站、小红书等）数据获取，大幅降低 Agent 信息获取成本，值得建立数据密集型 Agent 的团队关注。

- **[Superpowers（obra/superpowers）](https://github.com/obra/superpowers)**  
  结合软件开发方法论的 Agent 技能框架，今日暴涨 700 星，可能影响 AI 辅助编程与协作的范式。

- **[CopilotKit（CopilotKit/CopilotKit）](https://github.com/CopilotKit/CopilotKit)**  
  AG-UI 协议的首个实现，试图标准化 Agent 交互界面，前端开发者应深入研究。

- **[Mem0（mem0ai/mem0）](https://github.com/mem0ai/mem0)**  
  六行代码即可为 Agent 嵌入长期记忆，与 MemPalace 共同推动记忆赛道，适合需要个性化服务的 Agent 开发者。

---
*本日报由 [agents-radar](https://github.com/AlexdanerZe/agents-radar) 自动生成。*