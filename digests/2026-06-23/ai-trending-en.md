# AI Open Source Trends 2026-06-23

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-23 02:54 UTC

---

# AI Open Source Trends Report | June 23, 2026

**Step 1 (Filter):** Non-AI projects were excluded from the analysis. Projects like **Stirling-PDF**, **penpot**, **tursodatabase/turso**, **JuliaLang/julia**, and **Developer-Y/cs-video-courses** were identified as general-purpose tools or non-AI resources and omitted from trend assessment. The remaining 80+ highly AI-relevant repos were categorized and analyzed.

**Step 2 (Categorize):** Projects were grouped into 1 of 5 primary categories: Infrastructure & Agent Tooling, Agents/Workflows, RAG/Knowledge, LLMs/Training, or Applications.

**Step 3 (Output Report):**

---

## 1. Today's Highlights

The open-source AI ecosystem has decisively pivoted from monolithic models to production-grade agent infrastructure. The standout project is **OpenMontage** (+2,938 stars), the first open-source agentic video production system, proving agents can now manage complex multi-modal creative pipelines end-to-end. Simultaneously, the viral success of **mattpocock/skills** (+2,051 stars) and **garrytan/gstack** (+573 stars) marks the mainstream adoption of "agent configurations" as shared open-source artifacts—equivalent to the early Dockerfile movement. Underpinning this shift, infrastructure for persistent agent memory (**DeusData/codebase-memory-mcp**, +1,185 stars) and extreme inference efficiency (**airllm**) is maturing rapidly to support long-running, cost-sensitive agent workloads.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure & Agent Tooling

- **DeusData/codebase-memory-mcp** ([link](https://github.com/DeusData/codebase-memory-mcp)) — Surged +1,185 stars today. A high-performance MCP server that indexes codebases into persistent knowledge graphs with sub-ms queries, directly attacking the agent context window bottleneck.
- **mattpocock/skills** ([link](https://github.com/mattpocock/skills)) — Surged +2,051 stars today. Production-grade Claude Code skills from a leading TypeScript educator, representing the new paradigm of sharing agent capabilities as code.
- **garrytan/gstack** ([link](https://github.com/garrytan/gstack)) — Surged +573 stars today. The exact Claude Code setup used by YC CEO Garry Tan: 23 opinionated tools acting as an entire engineering and product organization.
- **lyogavin/airllm** ([link](https://github.com/lyogavin/airllm)) — +193 stars today. Enables 70B parameter LLM inference on a single 4GB GPU, dramatically lowering the hardware barrier for local model deployment.
- **headroomlabs-ai/headroom** ([link](https://github.com/headroomlabs-ai/headroom)) — ⭐47k. Compresses tool outputs, logs, and RAG chunks by 60-95% before they reach the LLM. A critical cost-saving layer for agentic systems.
- **ollama/ollama** ([link](https://github.com/ollama/ollama)) — ⭐174k. The universal standard for running open-source LLMs locally, continuously onboarding frontier models right on developer machines.
- **mem0ai/mem0** ([link](https://github.com/mem0ai/mem0)) — ⭐59k. The universal memory layer for AI agents, providing persistent context across sessions—a foundational piece for autonomous agent operations.
- **firecrawl/firecrawl** ([link](https://github.com/firecrawl/firecrawl)) — ⭐137k (+615 today). The leading web data API built for AI agents, essential for grounding LLMs with real-time web information.

### 🤖 AI Agents / Workflows

- **bytedance/deer-flow** ([link](https://github.com/bytedance/deer-flow)) — ⭐73k (+738 today). ByteDance's open-source long-horizon SuperAgent harness that researches, codes, and creates using sub-agents, sandboxes, and persistent memory.
- **OpenHands/OpenHands** ([link](https://github.com/OpenHands/OpenHands)) — ⭐78k. The premier AI software development agent that operates directly inside the developer environment and IDE.
- **NousResearch/hermes-agent** ([link](https://github.com/NousResearch/hermes-agent)) — ⭐200k. An agent framework architecturally focused on continuous growth, learning, and state persistence across interactions.
- **langchain-ai/langchain** ([link](https://github.com/langchain-ai/langchain)) — ⭐139k. The foundational agent engineering platform, now deeply integrated with MCP tools and multi-agent orchestration patterns.
- **browser-use/browser-use** ([link](https://github.com/browser-use/browser-use)) — ⭐100k. Makes websites natively accessible for AI agents, solving the critical gap in autonomous web interaction.
- **TauricResearch/TradingAgents** ([link](https://github.com/TauricResearch/TradingAgents)) — ⭐88k. A sophisticated multi-agent LLM framework for financial trading, showcasing enterprise-grade agent coordination.
- **zhayujie/CowAgent** ([link](https://github.com/zhayujie/CowAgent)) — ⭐45k. A super AI assistant & agent harness supporting multiple models and channels, emphasizing lightweight extensibility.

### 🔍 RAG / Knowledge & Vector Databases

- **infiniflow/ragflow** ([link](https://github.com/infiniflow/ragflow)) — ⭐83k. A leading RAG engine that fuses deep document understanding with agent capabilities to create a superior context layer for LLMs.
- **safishamsi/graphify** ([link](https://github.com/safishamsi/graphify)) — ⭐70k. Transforms any folder of code, docs, or schemas into a queryable knowledge graph for AI agents.
- **milvus-io/milvus** ([link](https://github.com/milvus-io/milvus)) — ⭐44k. The cloud-native vector database standard for scalable ANN search powering production RAG systems.
- **alibaba/zvec** ([link](https://github.com/alibaba/zvec)) — ⭐12k. A lightweight, lightning-fast in-process vector database from Alibaba, pushing the limits of embedded retrieval.
- **StarTrail-org/LEANN** ([link](https://github.com/StarTrail-org/LEANN)) — ⭐12k. A 2025 [MLsys] project offering 97% storage savings while running fast, accurate, private on-device RAG.
- **PaddlePaddle/PaddleOCR** ([link](https://github.com/PaddlePaddle/PaddleOCR)) — ⭐83k. Turns PDFs and images into structured data for LLMs—a critical document pre-processing step for enterprise RAG.
- **NirDiamant/RAG_Techniques** ([link](https://github.com/NirDiamant/RAG_Techniques)) — ⭐28k. The community's primary educational resource for implementing advanced RAG techniques with detailed notebook tutorials.

### 🧠 LLMs / Training & Evaluation

- **zjunlp/LightThinker** ([link](https://github.com/zjunlp/LightThinker)) — ⭐164. An EMNLP 2025 paper implementation that compresses the "thinking step" in chain-of-thought, addressing the prohibitive token cost of reasoning models.
- **open-compass/opencompass** ([link](https://github.com/open-compass/opencompass)) — ⭐7k. A comprehensive LLM evaluation platform supporting models like Llama, Qwen, and GPT across 100+ datasets.
- **asgeirtj/system_prompts_leaks** ([link](https://github.com/asgeirtj/system_prompts_leaks)) — ⭐45k. An essential community intelligence resource documenting the evolving system prompts from Claude, GPT, and Gemini.
- **galilai-group/stable-pretraining** ([link](https://github.com/galilai-group/stable-pretraining)) — ⭐266. A reliable, minimal library standardizing the pretraining process for foundation and world models.
- **testtimescaling/testtimescaling.github.io** ([link](https://github.com/testtimescaling/testtimescaling.github.io)) — ⭐104. A comprehensive survey on test-time scaling ("o1-style reasoning"), shaping the community's understanding of inference-time compute optimization.

### 📦 AI Applications (Vertical)

- **calesthio/OpenMontage** ([link](https://github.com/calesthio/OpenMontage)) — Surged +2,938 stars today. The world's first open-source agentic video production system: 12 pipelines, 52 tools, and 500+ agent skills turning AI assistants into full video studios.
- **ZhuLinsen/daily_stock_analysis** ([link](https://github.com/ZhuLinsen/daily_stock_analysis)) — ⭐45k (+1,557 today). An LLM-powered multi-market stock analysis system demonstrating explosive demand for personal finance AI agents.
- **heygen-com/hyperframes** ([link](https://github.com/heygen-com/hyperframes)) — Surged +395 stars today. A novel approach to agent-native video generation where agents write HTML to render video.
- **jamiepine/voicebox** ([link](https://github.com/jamiepine/voicebox)) — Surged +529 stars today. The open-source AI voice studio for cloning, dictation, and audio creation.
- **mukul975/Anthropic-Cybersecurity-Skills** ([link](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)) — Surged +956 stars today. 817 structured cybersecurity skills mapped to 6 frameworks (MITRE ATT&CK, NIST CSF, D3FEND, etc.), standardizing how agents execute security operations.
- **open-webui/open-webui** ([link](https://github.com/open-webui/open-webui)) — ⭐142k. The most popular user-friendly interface for local LLMs, supporting Ollama and all major providers.
- **hugohe3/ppt-master** ([link](https://github.com/hugohe3/ppt-master)) — ⭐30k. An AI that generates real, editable PowerPoints from documents with native shapes, animations, and audio narration.

---

## 3. Trend Signal Analysis

The data overwhelmingly signals that June 2026 is the month the open-source AI ecosystem "grew up" from experimental toolkits into production-ready infrastructure.

**The most powerful trend is the commoditization and standardization of agent behavior.** Rather than building agents from scratch, the community is sharing, forking, and refining "skills" and "configurations." The viral success of **mattpocock/skills** (+2k stars) and **gstack** (+573 stars) mirrors the early days of Dockerfiles—a standard, shareable way to configure a complex platform is emerging. This is directly enabled by the **Model Context Protocol (MCP)**. Projects like **codebase-memory-mcp** strike a chord because they solve the core problem of agent "amnesia" and context window limits through a standard protocol that any agent can consume.

**A direct attack on the primary bottlenecks of agentic AI is in full force.** The ecosystem is demonstrating a clear understanding that the unit economics of software are now defined by token cost. **airllm** tackles the compute cost (70B on 4GB GPU), **headroom** tackles the token cost (60-95% compression), and **codebase-memory-mcp** tackles context limits (persistent knowledge graphs with 99% fewer tokens). Every one of these projects is addressing a fundamental friction point that prevents agents from running continuously and autonomously.

**Vertical agents are exploding in specific, high-value domains.** The intense interest in finance (**TradingAgents**, **daily_stock_analysis**, **OpenBB**) and creative media (**OpenMontage**, **hyperframes**, **voicebox**) shows that the "full-stack agent"—capable of replacing an entire suite of tools and managing a human workflow from start to finish—is the killer app. These projects are complex, multi-pipeline systems managing 50-500+ skills, not simple chatbots.

---

## 4. Community Hot Spots

- **The MCP Server & Agent Skills Gold Rush** — The massive traction of `mattpocock/skills` and `codebase-memory-mcp` confirms that building and sharing MCP servers and agent skill collections is the highest leverage activity for developers in the AI ecosystem today. This is the new "open-source library" distribution model.

- **Agentic Creative Production** — `OpenMontage` (agentic video) + `voicebox` (agentic audio) + `hyperframes` (agentic HTML→video) tap into a massive unmet need for AI systems that don't just generate content but *manage the entire production pipeline*. This space is wide open and actively being defined.

- **Persistent Agent Memory** — Memory is the key to unlocking truly autonomous agents. The variety of approaches (`mem0ai`, `cognee`, `codebase-memory-mcp`, `deer-flow`, `claude-mem`) represents the most critical architectural debate in the agent space right now, and every memory project is seeing explosive growth.

- **Local & Efficient Inference** — `airllm` hitting the trending list proves the deep hunger for running powerful models without expensive hardware. Projects focusing on quantized inference, KV cache optimization, and consumer-grade hardware compatibility will continue to see massive adoption.

- **Finance-First Autonomous Agents** — The hypergrowth of `TauricResearch/TradingAgents`, `ZhuLinsen/daily_stock_analysis`, and `OpenBB` proves that financial analysis and trading are a primary proving ground for complex multi-agent systems, driven by clear metrics and the high value of automated financial workflows.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*