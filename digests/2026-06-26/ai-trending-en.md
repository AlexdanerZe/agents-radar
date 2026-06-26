# AI Open Source Trends 2026-06-26

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-26 03:23 UTC

---

**AI Open Source Trends Report: June 26, 2026**

---

### 1. Today’s Highlights

The AI open-source landscape today is defined by the rapid maturation of **production-grade, specialized AI agents**. The standout signal is `calesthio/OpenMontage` (+3,434 stars), packaging an entire video production suite as agent skills and proving developers are hungry for vertical agent applications. Concurrently, the infrastructure layer is hardening: Amazon entered the MCP arena with the official `aws/agent-toolkit-for-aws`, while `mukul975/Anthropic-Cybersecurity-Skills` (+571 stars) and `google-labs-code/design.md` (+1,475 stars) formalize structured skill sets and agent-native design standards. As frontier models proliferate via platforms like `ollama` (supporting Kimi-K2.6, GLM-5.1), the community’s focus has decisively shifted up the stack—into orchestration, memory, and domain-specific execution.

---

### 2. Top Projects by Category

#### 🔧 AI Infrastructure (Frameworks, SDKs, MCP, Agent Dev Tools)

| Project | Stars / Daily Delta | Why It Matters Today |
|---------|---------------------|----------------------|
| [`aws/agent-toolkit-for-aws`](https://github.com/aws/agent-toolkit-for-aws) | +47 today | Official AWS MCP servers and plugins, validating MCP as the enterprise standard for agent-tool interaction. |
| [`mukul975/Anthropic-Cybersecurity-Skills`](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) | +571 today | 817 structured cybersecurity skills mapped to 6 frameworks; a blueprint for the coming "skill engineering" discipline. |
| [`garrytan/gstack`](https://github.com/garrytan/gstack) | +767 today | Opinionated Claude Code environment acting as CEO, Designer, and QA—curated agent workflows are the new full-stack. |
| [`google-labs-code/design.md`](https://github.com/google-labs-code/design.md) | +1,475 today | A formal specification giving agents persistent understanding of visual identity; a potential `robots.txt` for agentic UIs. |
| [`NousResearch/hermes-agent`](https://github.com/NousResearch/hermes-agent) | ⭐203,155 | The leading community agent harness, representing the broadest base LLM agent framework. |
| [`CopilotKit/CopilotKit`](https://github.com/CopilotKit/CopilotKit) | ⭐35,521 | The frontend stack for agents and generative UI, enabling agent integration into any application. |
| [`shareAI-lab/learn-claude-code`](https://github.com/shareAI-lab/learn-claude-code) | ⭐68,457 | A minimal “agent harness” built from scratch; the definitive educational resource for agent mechanics. |
| [`shanraisshan/claude-code-best-practice`](https://github.com/shanraisshan/claude-code-best-practice) | +287 today | Documenting the migration from "vibe coding" to rigorous agentic engineering. |

#### 🤖 AI Agents / Workflows

| Project | Stars / Daily Delta | Why It Matters Today |
|---------|---------------------|----------------------|
| [`calesthio/OpenMontage`](https://github.com/calesthio/OpenMontage) | +3,434 today | World’s first open-source agentic video production system (52 tools, 500+ skills). The biggest indicator of the “vertical agent” gold rush. |
| [`xbtlin/ai-berkshire`](https://github.com/xbtlin/ai-berkshire) | +309 today | Multi-agent value investing framework (Buffett, Munger, etc.) built on Claude Code. Domain-specific agent research is exploding. |
| [`alibaba/page-agent`](https://github.com/alibaba/page-agent) | +163 today | JavaScript in-page GUI agent; controlling web interfaces with natural language. The browser is the new API. |
| [`CherryHQ/cherry-studio`](https://github.com/CherryHQ/cherry-studio) | ⭐47,803 | Unified AI productivity studio with 300+ assistants and autonomous agents. The self-hosted alternative to SaaS agent platforms. |
| [`browser-use/browser-use`](https://github.com/browser-use/browser-use) | ⭐100,711 | Making entire websites accessible to AI agents without custom integrations. |
| [`Significant-Gravitas/AutoGPT`](https://github.com/Significant-Gravitas/AutoGPT) | ⭐185,159 | The foundational open-source agent project, continuing to lead the autonomous agent philosophy. |
| [`bytedance/deer-flow`](https://github.com/bytedance/deer-flow) | ⭐74,747 | Long-horizon SuperAgent harness by ByteDance, handling tasks spanning minutes to hours with sandboxed tool execution. |
| [`TauricResearch/TradingAgents`](https://github.com/TauricResearch/TradingAgents) | ⭐88,574 | Multi-agent LLM financial trading framework. |
| [`headroomlabs-ai/headroom`](https://github.com/headroomlabs-ai/headroom) | ⭐51,139 | Compresses tool outputs, logs, and RAG chunks by 60–95% before they reach the LLM. |

#### 🔍 RAG / Knowledge & Vector DB

| Project | Stars / Daily Delta | Why It Matters Today |
|---------|---------------------|----------------------|
| [`opendatalab/MinerU`](https://github.com/opendatalab/MinerU) | +644 today | Transforms PDFs and Office docs into LLM-ready Markdown/JSON. Data ingestion for agents is a critical bottleneck being solved. |
| [`infiniflow/ragflow`](https://github.com/infiniflow/ragflow) | ⭐83,643 | Leading open-source RAG engine fusing retrieval with agent capabilities. |
| [`thedotmack/claude-mem`](https://github.com/thedotmack/claude-mem) | ⭐84,314 | Captures and compresses agent session data, injecting relevant context across sessions. The “database of context”. |
| [`mem0ai/mem0`](https://github.com/mem0ai/mem0) | ⭐59,465 | Universal memory layer for AI agents; persistent long-term context outside the LLM context window. |
| [`milvus-io/milvus`](https://github.com/milvus-io/milvus) | ⭐44,961 | High-performance, cloud-native vector database for scalable ANN search. |
| [`zilliztech/claude-context`](https://github.com/zilliztech/claude-context) | ⭐11,964 | Code search MCP for Claude Code, turning an entire codebase into agent context. |
| [`PaddlePaddle/PaddleOCR`](https://github.com/PaddlePaddle/PaddleOCR) | ⭐83,844 | Bridges images/PDFs and LLMs with a powerful, lightweight OCR toolkit. |

#### 🧠 LLMs / Training & Core ML

| Project | Stars / Daily Delta | Why It Matters Today |
|---------|---------------------|----------------------|
| [`ollama/ollama`](https://github.com/ollama/ollama) | ⭐174,914 | Local inference for Kimi-K2.6, GLM-5.1, DeepSeek, and more; the backbone of the self-hosted agent stack. |
| [`vllm-project/vllm`](https://github.com/vllm-project/vllm) | ⭐84,342 | High-throughput, memory-efficient LLM inference serving. |
| [`huggingface/transformers`](https://github.com/huggingface/transformers) | ⭐161,925 | The model-definition framework for state-of-the-art ML. |
| [`zjunlp/LightThinker`](https://github.com/zjunlp/LightThinker) | +164 today | Step-by-step thinking compression for LLMs (EMNLP 2025). Reduces inference cost for chain-of-thought workflows. |
| [`open-compass/opencompass`](https://github.com/open-compass/opencompass) | ⭐7,121 | Comprehensive LLM evaluation platform supporting 100+ datasets and major models. |

#### 📦 AI Applications (Vertical Solutions)

| Project | Stars / Daily Delta | Why It Matters Today |
|---------|---------------------|----------------------|
| [`hugohe3/ppt-master`](https://github.com/hugohe3/ppt-master) | ⭐31,411 | AI generates real, editable PowerPoints from documents—a concrete productivity win for enterprise users. |
| [`santifer/career-ops`](https://github.com/santifer/career-ops) | ⭐55,764 | AI-powered job search system built on Claude Code (14 skill modes, PDF generation, batch processing). |
| [`OpenBB-finance/OpenBB`](https://github.com/OpenBB-finance/OpenBB) | ⭐69,684 | Financial data platform now targeting AI agents as first-class users. |

---

### 3. Trend Signal Analysis

The data reveals four converging macro-trends redefining the AI OSS ecosystem.

**First: The "Skill Engineering" economy is formalizing.**  
The massive response to `mukul975/Anthropic-Cybersecurity-Skills` (+571 stars), `affaan-m/ECC` (agent harness optimization, ⭐221k), and `google-labs-code/design.md` (+1,475 stars) signals that the community has recognized the primary bottleneck is no longer the base model, but the *structured capabilities and knowledge* injected into the agent. We are moving from “prompt engineering” to a discipline of **curating, formatting, and versioning agent skills**. This will likely lead to package registries specifically for agent skills.

**Second: Agent-native context management is the new database layer.**  
Projects like `claude-mem` (⭐84k), `mem0ai` (⭐59k), and `headroomlabs-ai/headroom` (⭐51k) represent a fundamental architectural shift. Long-running, autonomous agents require persistent memory that compresses and retrieves context across sessions. The ability to store and recall context with 60-95% token reduction is no longer optional—it is the core infrastructure enabling agents to operate as reliable, long-term employees rather than stateless assistants.

**Third: The browser is the universal OS for agents.**  
`alibaba/page-agent` (in-page GUI agent), `browser-use` (⭐100k), and `jackwener/OpenCLI` (making any website an agent CLI) demonstrate that the community is bypassing traditional API-first integration. By giving agents the ability to interact with software through the same graphical interface as humans, the addressable automation surface expands to every existing website and desktop application. This is the “Robotic Process Automation (RPA)” moment for the AI agent era.

**Fourth: The Claude Code platform effect is building.**  
The sheer number of high-star projects extending Claude Code—from `gstack` (curated dev setups), to `claude-mem` (memory), to `AionUi` (24/7 coworker UI), to `openclaude` (runs anywhere)—confirms that Claude Code has evolved from a coding assistant into an extensible **agent operating system**. This mirrors the early ecosystems around Linux, VS Code, or Kubernetes, where a strong central platform spawns a wave of specialized tools and services.

---

### 4. Community Hot Spots

Developers should closely monitor these areas based on today’s explosive community activity:

- **Curated Agent Environments (`garrytan/gstack`, `claude-code-best-practice`):** Pre-configured, opinionated agent setups are in high demand. Treating the AI agent’s development environment like a deployable configuration (manifesting its tools, memory, and philosophy) is the next evolution of DevOps.

- **Agent-Native Data Standards (`google-labs-code/design.md`, `MinerU`):** Standards like `DESIGN.md` and deterministic document-to-LLM pipelines represent a new class of infrastructure. The community is actively defining how agents *read* and *understand* the world. Investing in these data protocols today is investing in the communication layer of tomorrow’s AI economy.

- **Vertical Agent Applications (`OpenMontage`, `TradingAgents`, `ai-berkshire`):** The most explosive star growth is in hyper-specific agents. The “horizontal” agent is giving way to deeply skilled domain experts in video, finance, and security. This de-risks agent development by delivering clear, measurable value in a single domain.

- **Browser-Based Agent Interfaces (`page-agent`, `browser-use`):** Controlling the browser (and therefore any web app) via natural language is seeing massive reinvestment. The ability for an agent to use a SaaS product without an API key unlocks enterprise automation at an unprecedented scale.

- **Long-term Agent Memory (`claude-mem`, `mem0`, `headroomlabs-ai/headroom`):** Solving the persistence and context compression problem is universally recognized as the critical path to reliable, autonomous agents. This is the most active area of architectural experimentation in the entire dataset.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*