# AI Open Source Trends 2026-05-25

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-25 09:58 UTC

---

## Step 1 (Filter)

From the 16 trending repositories, I excluded **`codecrafters-io/build-your-own-x`** as a general programming education resource not specific to AI/ML. The remaining 15 trending projects, plus the 80 topic-search results, were confirmed as AI-relevant.

**Filter Outcome:** 95 out of 96 total entries retained for analysis. The filtering confirms a near-total AI saturation on GitHub's trending surfaces today, with coding agents dominating over classical ML tooling in immediate activity.

## Step 2 (Categorize)

The filtered projects are grouped into the following primary categories (projects can span categories; primary assignment here reflects the core value proposition):

| Category | Description | Key Projects (Trending + Topic) |
|---|---|---|
| **🔧 AI Infrastructure** (Frameworks, SDKs, Inference, Dev tools, CLI, MCP) | Core tooling enabling agent development, LLM serving, and ecosystem integration | `pi`, `cmux`, `vllm`, `firecrawl`, `browser-use`, `rig`, `CopilotKit`, `Cherry Studio`, `free-claude-code` |
| **🤖 AI Agents / Workflows** (Frameworks, Multi-agent, Skills, Orchestration) | Composable agent behaviors, swarms, skill ecosystems, and task management | `claude-plugins-official`, `codegraph`, `multica`, `MiroFish`, `ECC`, `Heres-Agent`, `ruflo`, `Activepieces`, `nanobot`, `CowAgent`, `Cybersecurity Skills`, `dotnet/skills`, `karpathy-skills` |
| **🔍 RAG / Knowledge** (Vector DBs, Knowledge Graphs, Retrieval, Memory) | Structured context layers, persistent memory, and code/index knowledge bases | `Understand-Anything`, `claude-mem`, `mem0`, `Dify`, `RAGFlow`, `Qdrant`, `Milvus`, `Weaviate`, `LEANN`, `Graphify` |
| **🧠 LLMs / Training** (Model weights, Fine-tuning, Alignment, Education) | Foundation models, training-from-scratch tools, inference optimization | `Kronos`, `LlamaFactory`, `minimind`, `OpenCompass`, `tiny-llm`, `LLMs-from-scratch` |
| **📦 AI Applications** (Vertical solutions, End-user products) | Specific domain deployments solving real user problems | `frigate`, `career-ops`, `ppt-master`, `daily_stock_analysis`, `OpenBB` |

---

## Step 3 (Output Report)

### 1. Today's Highlights

The open-source AI ecosystem has decisively entered the **"Agent Middleware Era."** Today's trending list is not dominated by new models or training frameworks, but by the metadata, memory, and context infrastructure that makes agents *useful in complex environments*. The biggest story is the meteoric rise of **graph-based context retrieval**, led by `Understand-Anything` (+3,999 stars) and `codegraph` (+3,003 stars), signaling that flat text injection for coding agents is rapidly being replaced by structured knowledge graphs. Simultaneously, Anthropic's official push for a **plugin/skill manifest standard** (`claude-plugins-official`, `knowledge-work-plugins`, and the viral `andrej-karpathy-skills` file) has created a gold rush around reusable, domain-specific agent behaviors. A third signal is the radical specialization of infrastructure: `cmux`—a terminal built exclusively for AI coding agents—suggests the operator experience is now a serious product category of its own.

### 2. Top Projects by Category

#### 🤖 AI Agents / Workflows
- **[codegraph](https://github.com/colbymchenry/codegraph) ⭐ +3,003 today** — A pre-indexed code knowledge graph specifically designed to reduce token consumption and tool calls for Claude Code, Codex, and Cursor. It represents the most practical optimization for expensive agent runs.
- **[multica-ai/multica](https://github.com/multica-ai/multica) ⭐ +585 today** — The "open-source managed agents platform" that transforms isolated coding agents into coordinated engineering teams with tracked progress and composable skills.
- **[Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) ⭐ +930 today** — A massive, structured skill set (754 skills) mapped to MITRE ATT&CK, NIST, and D3FEND frameworks. It demonstrates how agent skills are evolving into standardized, auditable competency maps.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) ⭐ 166,418 total** — The "agent that grows with you," representing the state-of-the-art in self-improving, persistent agent architectures.
- **[ruflo](https://github.com/ruvnet/ruflo) ⭐ 54,893 total** — The leading multi-agent swarm orchestration platform built specifically for the Claude ecosystem, now integrating Codex support.

#### 🔧 AI Infrastructure (Dev Tools & Platforms)
- **[earendil-works/pi](https://github.com/earendil-works/pi) ⭐ +456 today** — A holistic AI agent toolkit offering a unified LLM API, coding agent CLI, both TUI and Web UI, and native vLLM pod integration—a "jack of all trades" infrastructure layer.
- **[manaflow-ai/cmux](https://github.com/manaflow-ai/cmux) ⭐ +696 today** — A Ghostty-based macOS terminal purpose-built for AI coding agents, with vertical tabs and agent-specific notifications. This marks the emergence of agent-native operating environments.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm) ⭐ 80,942 total** — Remains the undisputed standard for high-throughput LLM serving; critical infrastructure for any production agent deployment.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) ⭐ 46,259 total** — An "AI productivity studio" unifying 300+ assistants with autonomous agent capabilities; the most ambitious universal frontend for agent backends.

#### 🔍 RAG / Knowledge
- **[Understand-Anything](https://github.com/Lum1104/Understand-Anything) ⭐ +3,999 today** — (Trending #1) Converts code into interactive, queryable knowledge graphs. The explosive growth confirms that structured graph-based retrieval is the next leap in agent context management.
- **[claude-mem](https://github.com/thedotmack/claude-mem) ⭐ 77,959 total** — The leading solution for persistent, cross-session agent memory. Captures and compresses agent activity into injectable context.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0) ⭐ 56,658 total** — The "universal memory layer" for agents, increasingly adopted as the standard memory backend across agent frameworks.
- **[LEANN](https://github.com/yichuan-w/LEANN) ⭐ 11,722 total** — An MLsys2026 paper implementation achieving 97% storage savings for local RAG, making private on-device retrieval massively more efficient.

#### 🧠 LLMs / Training & Fine-Tuning
- **[Kronos](https://github.com/shiyu-coder/Kronos) ⭐ +106 today** — A specialized Foundation Model for financial market language. Its presence on the trending list signals growing demand for domain-specific, agent-tuned models rather than general-purpose chat.
- **[LlamaFactory](https://github.com/hiyouga/LlamaFactory) ⭐ 71,574 total** — The unified fine-tuning framework supporting 100+ LLMs and VLMs; the go-to tool for adapting models to specific agentic tasks.
- **[minimind](https://github.com/jingyaogong/minimind) ⭐ 50,532 total** — Trains a 64M-parameter LLM from scratch in 2 hours; critical educational infrastructure for the next generation of agent developers.

#### 📦 AI Applications
- **[frigate](https://github.com/blakeblackshear/frigate) ⭐ +181 today** — The mature, real-time local object detection NVR. A stable AI application continuing to see growth as the smart home + AI convergence deepens.
- **[career-ops](https://github.com/santifer/career-ops) ⭐ 47,124 total** — An AI-powered job search system built entirely on Claude Code, demonstrating how agents can now build substantial vertical applications.
- **[ppt-master](https://github.com/hugohe3/ppt-master) ⭐ 20,826 total** — Generates native, editable PowerPoint files from any document—a practical, high-demand enterprise AI application.

### 3. Trend Signal Analysis

**The Cognitive Architecture of Agents is Shifting from Prompts to Structured Graphs and Skills.**

The data reveals a decisive pivot in how the open-source community is solving the agent reliability problem. A full third of today's top trending projects (`Understand-Anything`, `codegraph`, `claude-mem`, `karpathy-skills`, `Anthropic-Cybersecurity-Skills`) are explicitly designed to structure agent context and behavior externally rather than relying on in-prompt instructions. This represents a community-wide acknowledgment that **context window economics** is the binding constraint on agent utility.

The viral success of `andrej-karpathy-skills` (+2,551 stars) is particularly revealing. Derived from Karpathy's critiques of LLM coding pitfalls, this single CLAUDE.md file has become a template for how the community wants to specify agent behavior: deterministic, shareable, and auditable. Combined with Anthropic's official skill directory, we are witnessing the birth of **a universal agent capability standard**—a "Skills Manifest" ecosystem where agent behavior is distributed as structured files rather than vague system prompts.

A striking new direction is **agent-native operating tooling**. `cmux` (a terminal for agents) and `multica` (a platform for managing agent teams) suggest the infrastructure stack around agents is evolving beyond simple VSCode extensions into dedicated desktop environments and management planes. This mirrors the early days of cloud computing, when tools like Terraform and Docker emerged to manage the new paradigm.

Finally, the sustained high star counts for memory projects (`claude-mem` at 77k, `mem0` at 56k) against generational agent frameworks confirm: **memory and context are the new moats**, not general reasoning. The project that gives an agent fluent access to its entire history and codebase wins the developer's trust.

### 4. Community Hot Spots

- **Graph-Based Agent Context Layers:** `Understand-Anything` (+3,999 today) and `codegraph` (+3,003 today) are the highest-velocity projects right now. Any developer building tooling around coding agents should immediately investigate replacing raw text injection with pre-indexed, queryable graph structures. [Understand-Anything](https://github.com/Lum1104/Understand-Anything) | [codegraph](https://github.com/colbymchenry/codegraph)
- **The Standardized Skills Ecosystem:** The Anthropic plugin repos (`claude-plugins-official`, `knowledge-work-plugins`) and the cybersecurity skillset standard (`Anthropic-Cybersecurity-Skills`) represent a new distribution model for agent intelligence. Building skills in this format is the highest-ROI contribution an OSS developer can make right now. [Skills Directory](https://github.com/anthropics/claude-plugins-official) | [Cyber Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)
- **Agent-Native Infrastructure:** `cmux` and `multica` represent an entirely new product category. The former signals a UX revolution for agent operators; the latter validates the "agent-as-teammate" management layer. Watch these for where the platform is going. [cmux](https://github.com/manaflow-ai/cmux) | [multica](https://github.com/multica-ai/multica)
- **Persistent Memory Engines:** `claude-mem` (77k stars) and `mem0` (56k stars) are the standard bearers for the memory layer. Cross-session context injection is the de facto expectation for serious agent usage. [claude-mem](https://github.com/thedotmack/claude-mem) | [mem0](https://github.com/mem0ai/mem0)
- **Domain-Specific Foundation Models:** `Kronos` (finance LLM) entering the list signals an impending wave of ultra-specific models fine-tuned for focused agentic tool use, rather than generic chat. This is the "LLM app store" model arriving. [Kronos](https://github.com/shiyu-coder/Kronos)

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*