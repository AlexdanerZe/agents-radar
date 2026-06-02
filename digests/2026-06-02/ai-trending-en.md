# AI Open Source Trends 2026-06-02

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-02 03:39 UTC

---

# AI Open Source Ecosystem Trends Report: 2026-06-02

---

## 1. Today's Highlights

Today's AI open-source landscape is defined by an aggressive community pivot toward **production-ready agent infrastructure** and **generative content pipelines**. The viral explosion of `MoneyPrinterTurbo` (+3,375 stars) signals an insatiable market demand for automated AI video generation that goes beyond text. Equally significant is the rise of "Agent Harnesses"—meta-frameworks for orchestrating specialized agent teams—and persistent memory layers, indicating the community is actively solving the hard coordination and context problems that limit current agents. This infrastructure build-out is fueled by the latest wave of powerful open-weight models (Kimi-K2.5, GLM-5, DeepSeek) tracked in `ollama`, while new frontiers in voice AI (`VoxCPM`) and accessible LLM training (`train-llm-from-scratch`) are broadening the ecosystem's scope from consumption to creation.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, Dev Tools, CLI)

- **[microsoft/markitdown](https://github.com/microsoft/markitdown)** (+3,034 stars today) — Python tool for converting files and office documents to Markdown. Its explosive growth reveals the massive, unglamorous need for reliable document preprocessing in LLM ingestion pipelines.

- **[ollama/ollama](https://github.com/ollama/ollama)** (⭐172k) — The essential local LLM runtime, updated to support the latest frontier OSS models including Kimi-K2.5, GLM-5, and DeepSeek, directly powering the entire downstream agent ecosystem.

- **[D4Vinci/Scrapling](https://github.com/D4Vinci/Scrapling)** (+1,486 stars today) — An adaptive web scraping framework optimized for AI data pipelines, responding to the critical need for scalable, generic data extraction for agents and RAG.

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** (⭐81k) — The standard high-throughput inference and serving engine for deploying demanding open-source LLMs in production.

- **[can1357/oh-my-pi](https://github.com/can1357/oh-my-pi)** (+335 stars today) — A terminal AI coding agent with hash-anchored edits and an optimized tool harness, adding novel engineering rigor to the rapidly differentiating coding agent space.

- **[dmtrKovalenko/fff](https://github.com/dmtrKovalenko/fff)** (+135 stars today) — The fastest file search toolkit, explicitly designed for AI agents, Neovim, and Rust tooling, exemplifying the optimization of low-level infrastructure for agentic workflows.

---

### 🤖 AI Agents / Workflows (Agent Frameworks, Automation, Multi-Agent Systems)

- **[langgenius/dify](https://github.com/langgenius/dify)** (⭐143k) — The leading open-source platform for agentic workflow development, bridging prototype experimentation and complex production deployment.

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** (⭐176k) — A foundational, adaptable agent framework that "grows with you," representing the community's deep commitment to building versatile, long-lived agent platforms.

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** (⭐81k, +299 today) — A multi-agent LLM framework for financial trading, demonstrating the powerful verticalization of agent systems into high-stakes domains.

- **[revfactory/harness](https://github.com/revfactory/harness)** (+524 stars today) — A meta-skill that designs domain-specific agent teams and generates their skills, pushing the frontier of agent specialization, hierarchies, and orchestration.

- **[EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)** (+417 stars today) — Official plugins for Claude Code, Cursor, and Codex, standardizing how compound AI systems integrate with major coding assistants—a clear sign of ecosystem maturation.

- **[nesquena/hermes-webui](https://github.com/nesquena/hermes-webui)** (+945 stars today) — A dedicated WebUI for Hermes Agent, fulfilling the strong demand for accessible interfaces to manage and monitor complex agent interactions.

- **[ShareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)** (⭐64k) — A nano "agent harness" built from scratch, reflecting the community's drive to deeply understand and reimplement agent frameworks from the ground up.

---

### 📦 AI Applications (Specific Apps, Vertical Solutions)

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** (+3,375 stars today, #1 trending) — Leverages AI LLMs for one-click high-definition short video generation. This is the clearest signal yet that generative video has crossed the chasm from demo to accessible tool.

- **[OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM)** (+888 stars today) — VoxCPM2 introduces tokenizer-free TTS for multilingual speech generation and true-to-life voice cloning, marking a leap forward in open-source speech AI.

- **[FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch)** (+861 stars today) — A practical, straightforward method for training an LLM from data download to text generation, fulfilling the community's deep desire for hands-on ML engineering knowledge.

- **[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB)** (⭐68k) — The open-source financial data platform for analysts, quants, and now explicitly AI agents, cementing finance as the premier vertical for applied agent systems.

- **[stefan-jansen/machine-learning-for-trading](https://github.com/stefan-jansen/machine-learning-for-trading)** (+93 stars today) — The canonical code repository for the 2nd edition of Machine Learning for Algorithmic Trading, a foundational reference for the AI-finance intersection.

- **[pbakaus/impeccable](https://github.com/pbakaus/impeccable)** (+485 stars today) — A design language specifically crafted to make AI harnesses better at UI/UX, indicating a maturing focus on the end-user experience of AI tools.

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** (⭐39k) — LLM-powered stock analysis system for A/H/US markets, showing the trend of accessible, zero-cost AI finance automation.

---

### 🧠 LLMs / Training (Model Weights, Training Frameworks, Fine-Tuning)

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** (⭐71k) — The unified standard for efficient fine-tuning of over 100 LLMs and VLMs, essential for adapting general foundation models to specific enterprise or research tasks.

- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** (⭐50k) — Demonstrated how to train a 64M-parameter LLM from scratch in just 2 hours, significantly lowering the barrier to entry for LLM pretraining research.

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** (⭐7k) — A comprehensive LLM evaluation platform supporting 100+ datasets, whose importance grows as the open-source model ecosystem becomes more crowded and fragmented.

- **[p-e-w/heretic](https://github.com/p-e-w/heretic)** (+249 stars today) — Fully automatic censorship removal for language models, reflecting ongoing community debate and engineering around model alignment and openness.

---

### 🔍 RAG / Knowledge (Vector DBs, Retrieval-Augmented Generation, Knowledge Management)

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** (⭐57k) — The universal memory layer for AI Agents, a critical component in the community drive to make agents genuinely adaptive and capable of long-term learning.

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** (⭐80k) — Captures, compresses, and reinjects agent context across sessions, directly solving the missing "persistent memory" layer for coding agents like Claude Code and Codex.

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** (⭐49k) — Evolved from a simple index into the leading document agent and OCR platform, powering complex enterprise RAG over diverse and messy document types.

- **[supermemoryai/supermemory](https://github.com/supermemoryai/supermemory)** (+647 stars today) — A new, fast, scalable "Memory API for the AI era," entering the fiercely competitive but essential agent memory infrastructure space.

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** (⭐81k) — A leading RAG engine that fuses cutting-edge retrieval augmentation with agent capabilities to create a superior context layer for LLMs.

- **[HKUDS/LightRAG](https://github.com/HKUDS/LightRAG)** (⭐36k) — An EMNLP 2025 project that became the community standard for simple, fast, and effective retrieval augmentation, benchmarking modern RAG architecture.

- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** (⭐32k) — Introduces "vectorless, reasoning-based RAG," pushing the paradigm beyond pure embedding similarity toward semantic document understanding.

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** (⭐17k) — A memory platform for AI agents that compresses complex RAG pipelines into six lines of code, reflecting the drive toward developer ergonomics.

---

## 3. Trend Signal Analysis

The dominant signal from today's data is a decisive community pivot **from model-consumption to agent-orchestration**. The hottest projects are no longer mere wrappers around APIs; they are **Agent Harnesses**—meta-frameworks for tool delegation, sub-agent spawning, and state management. `revfactory/harness`, `compound-engineering-plugin`, and `oh-my-pi` represent a Cambrian explosion of architectural patterns around how agents coordinate, resembling the early web framework wars. The community is converging on the insight that the bottleneck is coordination infrastructure, not model intelligence.

The simultaneous, intense focus on **Memory Layers** (`claude-mem`, `supermemory`, `mem0`, `cognee`) is a direct response to the fundamental limitation of stateless LLMs in agentic contexts. The open-source community is building the "hippocampus" for AI—persistent context across sessions—which is the essential prerequisite for autonomous, long-running agents. This is arguably the most critical unsolved middleware problem in production AI today.

A powerful verticalization signal is emerging in **Finance and Content Creation**. `TradingAgents` (81k stars) and `MoneyPrinterTurbo` (+3,375 today) demonstrate that structured finance and creative content are the killer verticals for the current generation of agent frameworks. The sheer velocity of video generation tools indicates text-to-video has outpaced even image generation in community adoption velocity.

This entire boom rests on the **commoditization of extremely capable models**. The explicit listing of models like Kimi-K2.5, GLM-5, and DeepSeek in `ollama`'s description draws a direct causal line: as open-weight frontier models become widely available via simple runtimes, the community naturally shifts its innovation energy up the stack to memory, tools, orchestration, and multimodal output. The rise of training resources (`train-llm-from-scratch`, `minimind`) further shows the community is simultaneously a consumer and creator of model technology—a hallmark of a maturing platform ecosystem.

---

## 4. Community Hot Spots

- **Agent Memory & Context Systems** (`thedotmack/claude-mem`, `supermemoryai/supermemory`, `mem0ai/mem0`, `topoteretes/cognee`)
  The defining unsolved problem in applied AI. Projects providing durable, cross-session memory for coding and general agents are the most actively discussed and integrated infrastructure pieces today.

- **Vertical Multi-Agent Finance** (`TauricResearch/TradingAgents`, `OpenBB-finance/OpenBB`, `stefan-jansen/machine-learning-for-trading`)
  Finance is the leading edge for multi-agent frameworks due to its quantifiable outcomes. Expect the architectural patterns established here to be ported to legal, medical, and engineering domains.

- **Generative Video Pipelines** (`harry0703/MoneyPrinterTurbo`)
  The staggering +3,375 daily stars confirm text-to-video is the breakout consumer/creator use case of the cycle. This space is moving rapidly toward production polish and API-accessible tooling.

- **Coding Assistant Extensibility** (`compound-engineering-plugin`, `oh-my-pi`, `shareAI-lab/learn-claude-code`)
  The "plugin ecosystem" moment for AI coding assistants. Developers are flocking to open-source harnesses that offer control, customization, and transparency over proprietary frontends.

- **Multimodal Document & Voice AI** (`OpenBMB/VoxCPM`, `microsoft/markitdown`, `PaddlePaddle/PaddleOCR`)
  Beyond text, the community is relentlessly attacking the "last mile" problems of real-world data: converting messy office PDFs and generating lifelike speech. These unsexy infrastructure tools consistently attract massive star counts, revealing deep enterprise demand.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*