# AI Open Source Trends 2026-06-13

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-13 03:25 UTC

---

**Cutoff Date Note:** The provided data is dated **2026-06-13**, a future date. This report strictly analyzes the given dataset as if it were today's snapshot.

---

# AI Open Source Trends Report: 2026-06-13

## 1. Today’s Highlights

The dominant signal today is the **"Skills-ification" of AI agents**. The community is no longer focused solely on building better agent runtimes; the biggest blocks of new stars are flooding into curated marketplaces for agentic skills, led by `addyosmani/agent-skills` and `obra/superpowers`. This suggests the runtime layer (Claude Code, OpenHands, etc.) has become a commodity, and the competitive frontier is now breadth and rigor of composable agent capabilities. Simultaneously, **Persistent Session Memory** has eclipsed classic vector search as the hottest sub-topic in RAG, with projects like `claude-mem` and `graphify` seeing massive traffic for their work on cross-session context injection. Finally, a fresh vertical push in **Healthcare AI** (`openmed`) and a breakthrough in **Edge RAG storage efficiency** (`LEANN`) signal that the ecosystem is maturing into specific, high-value deployments.

## 2. Top Projects by Category

### 🔧 AI Infrastructure & Dev Tools
- **[ollama/ollama](https://github.com/ollama/ollama)** – 173,984 stars. The standard-bearer for local LLM execution, now onboarding models like Kimi and GLM.
- **[LMCache/LMCache](https://github.com/LMCache/LMCache)** – +28 stars today. A critical new latency layer that caches KV states between requests; essential reading for anyone optimizing LLM serving costs.
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** – 7,602 stars. The fastest-growing Rust framework for modular LLM apps, signaling a serious polyglot expansion of the Python-heavy AI stack.
- **[Picovoice/picollm](https://github.com/Picovoice/picollm)** – 312 stars. On-device inference via X-Bit quantization; representing the push toward totally private, edge-deployed LLMs.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** – 7,081 stars. The comprehensive LLM evaluation platform (100+ datasets). Proxy for the community's obsession with benchmarking.

### 🤖 AI Agents & Workflows
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** – 192,063 stars. "The agent that grows with you," pushing the paradigm of agents that evolve across sessions.
- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** – **+2,656 stars today**. The single hottest repo today. A curated library of production-grade engineering skills for AI coding agents. This is the "HuggingFace for agent skills."
- **[obra/superpowers](https://github.com/obra/superpowers)** – **+1,275 stars today**. An agentic skills framework *and* a software development methodology that declares how these skills should be composed.
- **[msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)** – **+1,026 stars today**. A complete multi-agent agency in a box (Reddit ninjas, reality checkers, etc.). Shows the maturation of agent team topologies.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** – 58,458 stars. The universal memory layer for agents; the foundational block upon which persistent skill frameworks (above) are built.
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** – 34,897 stars. The frontend stack (React/Angular) for embedding agents into enterprise UIs.

### 📦 AI Applications
- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** – 141,289 stars. The definitive user-friendly AI interface bridging Ollama and cloud APIs.
- **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)** – **+515 stars today**. A new, clean-room open-source initiative in healthcare AI. Signals strong developer hunger for trustworthy, auditable medical agent stacks.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** – 47,251 stars. AI productivity studio with 300+ skill presets; the consumerization of the skills trend.
- **[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB)** – 69,027 stars. The financial data platform re-engineered for AI agents; a case study in vertical-specific agent infrastructure.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** – 27,024 stars. Niche but hugely viral: generates editable, animated PowerPoints from documents. Proves long-tail agent automation is resonating.

### 🧠 LLMs / Training / Fine-tuning
- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** – 72,122 stars. The standard unified fine-tuning framework for 100+ LLMs/VLMs.
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** – 214,373 stars. Massive repo. An agent harness optimization system covering memory, skills, and security. Critics might call it "everything but the kitchen sink"; the stars say developers want integrated optimization.
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** – 4,272 stars. Educational "build a tiny vLLM" project. Growing as more systems engineers cross over into AI.
- **[JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)** – 71,966 stars. A creative token-efficiency hack ("talking like caveman") that cuts 65% tokens. Highlights that prompt-side cost optimization is a massive community concern.

### 🔍 RAG / Knowledge / Memory
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** – 82,018 stars. The breakout star of the RAG sub-topic. Captures agent behavior, compresses it, and injects relevant context into *future* sessions. This is the new frontier: Session-to-Session RAG.
- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** – 66,339 stars. Converts any codebase, schema, or document folder into a queryable knowledge graph for agents. A radically different approach to context retrieval.
- **[langgenius/dify](https://github.com/langgenius/dify)** – 145,005 stars. The most deployed production RAG platform; the incumbent against which all RAG tools are compared.
- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** – 11,913 stars. MLsys 2026 paper implementation. Achieves **97% storage savings** for fully private, on-device RAG. The most technically disruptive project in the infrastructure layer of retrieval today.
- **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** – 82,034 stars. The bridge between PDFs/images and LLMs. The exploding usage of OCR reflects that RAG is worthless without high-quality document ingestion.
- **[meilisearch/meilisearch](https://github.com/meilisearch/meilisearch)** – 58,073 stars. The lightning-fast search engine now deeply integrated with AI hybrid search. A "stealth" RAG success story.

## 3. Trend Signal Analysis

**The Death of the "Vanilla Agent":**
The most explosive energy today is not around a new model or a new inference engine, but around **Agent Skills** (`addyosmani/agent-skills`, `obra/superpowers`, `phuryn/pm-skills`). This signals a maturation point: the core coding agent runtimes (Claude Code, Codex, OpenHands) are now treated as stable operating systems. The value creation has moved to the "app store" layer—composable, tested skills for engineering, PM, and marketing. We are seeing the community effectively standardize on how skills are packaged and published.

**The Rise of "Session-to-Session" Context (Memory > Search):**
A new RAG layer is emerging. The top RAG projects by star velocity are not about vector databases (which are now mature commodities) but about **persistent memory and behavioral compression** (`claude-mem`, `mem0`, `graphify`). Classic RAG answers questions from a static corpus. Today's top tools compress *entire agent sessions* and inject them into future conversations. This is the architectural answer to the context window limit, and it is the focus of the most innovative OSS code in the ecosystem right now.

**Industry Convergence in Vertical Agents:**
We are seeing an accelerating pattern of "General Agent Infrastructure + Specific Data Layer = Vertical App." `openmed` (Healthcare), `OpenBB` (Finance), and `PaddleOCR` (Document-heavy verticals) all rely on the same stack of Ollama + milvus/qdrant + Dify, but they wrap it with deeply specific ontologies and regulatory knowledge. This strongly suggests that the next wave of unicorns will be built on top of horizontal OSS infrastructure and targeted at tightly regulated, data-complex verticals.

**Creative Engineering as a First-Class Signal:**
The success of `caveman` (71k stars) and `phuryn/pm-skills` (800+ stars today) proves that the community rewards *system-level creative thinking* just as much as raw performance. The "caveman" project—a prompt that aggressively compresses tokens—is fundamentally an engineering optimization, not a model training breakthrough. It reveals a massive appetite for cost-control and "jailbreaking" the efficiency of existing inference APIs through clever system design.

## 4. Community Hot Spots

- **🔥 Agent Skills Frameworks:** Immediately explore `addyosmani/agent-skills` and `obra/superpowers`. If you are building a coding agent, your differentiation will come from which skills you curate, not which LLM you call. The community is rapidly converging on skill formats; early participation in this standard is high-leverage.
- **🌐 Persistent Memory Injection:** `claude-mem` (82k stars) is the must-study architecture of the month. Its pattern of *capture, compress, inject* across sessions solves the biggest practical problem in enterprise agent deployment (agents starting from zero every time). Modeling your agent memory layer on this pattern is non-negotiable for production.
- **🚀 Edge RAG with LEANN:** `StarTrail-org/LEANN` provides a shocking 97% storage compression for on-device retrieval. For any developer targeting privacy-sensitive applications or offline-first agents, this is the single most disruptive infrastructure project in the data layer. It makes true personal knowledge bases viable on a phone.
- **📊 Vertical AI (Healthcare / Finance):** The +515 star surge for `maziyarpanahi/openmed` signals a community void. Developers are actively seeking clean-room, open-source alternatives in regulated industries. Anyone building an AI startup in Healthcare or Legal should fork this project as a starting template for compliance and domain-specific RAG.
- **💡 Token Efficiency Creativity:** The "caveman" prompt is a meme that is also a massive cost-saver. It proves that prompt engineering at the system level can rout a >60% reduction in LLM costs. This hack is a beacon for the community's focus on pragmatism and immediate ROI, and it will likely be integrated into standard agent harnesses within weeks.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*