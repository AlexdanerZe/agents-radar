# AI Open Source Trends 2026-06-10

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-10 03:26 UTC

---

# AI Open Source Trends Report
**Date: 2026-06-10 | Analysis of GitHub Trending & AI Topic Data**

---

## 1. Today's Highlights

The AI open-source ecosystem is undergoing a major structural shift from monolithic chatbots toward **skill-driven autonomous agents**. The explosion of `mvanhorn/last30days-skill` (+3,191 stars) and `addyosmani/agent-skills` (+443) signals the emergence of "agent app stores"—reusable, domain-specific competencies rather than single-purpose bots. Meanwhile, hardware-aware tools like `whichllm` (+633) and the Rust-based vector index `turbovec` (+1,801) reveal a community laser-focused on **local performance optimization**. The most emblematic project is `santifer/career-ops` (+1,110), a complex job-search application built entirely by Claude Code—proving that "agent-coded applications" are now a legitimate, trending category of their own.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **mvanhorn/last30days-skill** ([link](https://github.com/mvanhorn/last30days-skill)) ⭐ +3,191 today — An AI agent skill that researches topics across Reddit, X, YouTube, HN, Polymarket, and the web into grounded summaries; the day's absolute breakout star.
- **RyanCodrai/turbovec** ([link](https://github.com/RyanCodrai/turbovec)) ⭐ +1,801 today — A high-performance vector index written in Rust with Python bindings (TurboQuant-based), pushing local vector search performance to new limits.
- **Andyyyy64/whichllm** ([link](https://github.com/Andyyyy64/whichllm)) ⭐ +633 today — A CLI tool that ranks local LLMs by real, recency-aware benchmarks on your specific hardware—essential for navigating the fragmented local model landscape.
- **roboflow/supervision** ([link](https://github.com/roboflow/supervision)) ⭐ +733 today — The reusable computer vision tool library of choice for production CV agent pipelines.
- **vllm-project/vllm** ([link](https://github.com/vllm-project/vllm)) ⭐ 82,366 total — The definitive high-throughput LLM inference engine powering large-scale model deployments.

### 🤖 AI Agents / Workflows
- **aaif-goose/goose** ([link](https://github.com/aaif-goose/goose)) ⭐ +489 today — A Rust-based extensible AI agent that installs, executes, and tests code beyond generation—positioning itself as a universal development agent.
- **addyosmani/agent-skills** ([link](https://github.com/addyosmani/agent-skills)) ⭐ +443 today — A curated collection of production-grade engineering skills for coding agents, addressing the critical "agent skill gap" in real-world workflows.
- **phuryn/pm-skills** ([link](https://github.com/phuryn/pm-skills)) ⭐ +806 today — A marketplace of 100+ agentic product management skills, demonstrating the verticalization of agent capabilities into specific disciplines.
- **shareAI-lab/learn-claude-code** ([link](https://github.com/shareAI-lab/learn-claude-code)) ⭐ 65,724 total — A nano agent harness built from scratch, showing massive interest in hackable, minimalistic agent architectures.
- **CopilotKit/CopilotKit** ([link](https://github.com/CopilotKit/CopilotKit)) ⭐ 34,473 total — The frontend stack for generative UI and agents (AG-UI Protocol), defining how users interact with agents across React, Angular, and mobile.

### 📦 AI Applications
- **santifer/career-ops** ([link](https://github.com/santifer/career-ops)) ⭐ +1,110 today — An AI-powered job search system built on Claude Code with 14 skill modes and a Go dashboard; the flagship example of an agent-coded application.
- **yikart/AiToEarn** ([link](https://github.com/yikart/AiToEarn)) ⭐ +402 today — A TypeScript app leveraging AI for income generation, tapping into the practical "AI for side-hustle" movement.
- **maziyarpanahi/openmed** ([link](https://github.com/maziyarpanahi/openmed)) ⭐ +191 today — An open-source healthcare AI platform targeting high-impact, privacy-sensitive medical applications.
- **francescopace/espectre** ([link](https://github.com/francescopace/espectre)) ⭐ +134 today — An edge AI application using Wi-Fi CSI analysis for Home Assistant motion detection.
- **browser-use/browser-use** ([link](https://github.com/browser-use/browser-use)) ⭐ 98,009 total — Making the web programmatically accessible for AI agents; essential infrastructure for automated web tasks.

### 🧠 LLMs / Training
- **ollama/ollama** ([link](https://github.com/ollama/ollama)) ⭐ 173,723 total — The dominant local model runner, now supporting Kimi-K2.6, GLM-5.1, DeepSeek, Qwen, and Gemma.
- **hiyouga/LlamaFactory** ([link](https://github.com/hiyouga/LlamaFactory)) ⭐ 72,036 total — The unified efficient fine-tuning framework for 100+ LLMs and VLMs (ACL 2024), essential for model customization.
- **x1xhlol/system-prompts-and-models-of-ai-tools** ([link](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)) ⭐ +79 today — A comprehensive collection of system prompts from Cursor, Claude Code, Devin, and others—codifying "prompt-as-infrastructure."
- **skyzh/tiny-llm** ([link](https://github.com/skyzh/tiny-llm)) ⭐ 4,264 total — An educational course on building LLM inference serving on Apple Silicon, meeting surging demand for systems-level AI knowledge.

### 🔍 RAG / Knowledge
- **infiniflow/ragflow** ([link](https://github.com/infiniflow/ragflow)) ⭐ 82,337 total — A leading RAG engine fusing retrieval-augmented generation with agent capabilities for a superior LLM context layer.
- **mem0ai/mem0** ([link](https://github.com/mem0ai/mem0)) ⭐ 58,214 total — The universal memory layer for AI agents, solving persistent context across sessions.
- **thedotmack/claude-mem** ([link](https://github.com/thedotmack/claude-mem)) ⭐ 81,502 total — Captures, compresses, and injects relevant agent session context—a critical enabler for long-running agent tasks.
- **safishamsi/graphify** ([link](https://github.com/safishamsi/graphify)) ⭐ 64,323 total — An AI skill that transforms any codebase or document set into a queryable knowledge graph.
- **Mintplex-Labs/anything-llm** ([link](https://github.com/Mintplex-Labs/anything-llm)) ⭐ 61,333 total — The "own your intelligence" platform for building powerful local-first agent experiences with integrated RAG.

---

## 3. Trend Signal Analysis

**The Agent Skill Economy is the dominant narrative.** The simultaneous rise of `mvanhorn/last30days-skill` (+3,191), `addyosmani/agent-skills` (+443), and `phuryn/pm-skills` (+806) strongly indicates the community is pivoting from building general-purpose agents toward creating, packaging, and distributing specialized agent competencies. This mirrors the mobile industry's shift from operating systems to app stores. The value capture is no longer in the agent "shell" but in the skills that define what an agent can actually *do*.

**Local-first, hardware-aware optimization is peaking.** `whichllm` (+633) perfectly addresses the fragmentation of the local model landscape by providing recency-aware, hardware-specific benchmarks. `turbovec` (+1,801), a Rust-native vector index, signals that performance on consumer hardware (Apple Silicon, RTX) is now a primary engineering constraint and differentiator. The ecosystem is maturing from "will it run?" to "what runs best on *my* machine?"

**Agent-written applications are a new software category.** `santifer/career-ops` is not just a tool—it is an entire job-search platform (Go dashboard, PDF generation, batch processing, 14 skill modes) built entirely by Claude Code. Its trending success validates that the prompt engineer / agent supervisor is now a primary application architect. This radically lowers the barrier to complex software creation and signals a shift toward "vibe coding" producing production-grade results.

**Memory is the deepest unsolved problem.** The consistent high ranking of memory projects (`mem0` at 58k, `claude-mem` at 81k, `graphify` at 64k, `cognee` at 17k) across topic searches reveals that persistent, structured memory remains the critical bottleneck for coherent, long-running agents. Innovation in context compression, knowledge graph construction, and hybrid recall is the highest-impact engineering frontier.

**Rust is emerging as the agent infrastructure language.** Both `goose` (agent runtime) and `turbovec` (vector index) are built in Rust, suggesting a shift toward systems-level performance for agent infrastructure, where Python bindings provide accessibility. This mirrors the "Rust rewrites" wave in databases but now applied to agent tooling.

---

## 4. Community Hot Spots

- **Agent Skill Marketplaces:** The cluster of `addyosmani/agent-skills`, `phuryn/pm-skills`, and `last30days-skill` points to a gold rush in creating packaged, domain-specific agent skills. Developers should focus on building for engineering, product, legal, and healthcare verticals—this is the "app store" moment for AI agents.

- **Hardware-Aware LLM Optimization:** `whichllm` addresses a genuine pain point in a saturated market. Tools that provide intelligent model selection based on user hardware profiles (VRAM, latency, context window) will see strong adoption as local models continue to proliferate.

- **Agent Memory & Context Systems:** Projects like `mem0`, `claude-mem`, and `graphify` occupy the most technically challenging space in the ecosystem. Any advancement in context compression, persistent knowledge graphs, or multi-session memory coherence will have outsized impact on agent reliability and utility.

- **Agent-Coded Application Blueprints:** `santifer/career-ops` is a reference architecture. Expect a wave of "agent-native" applications (e.g., CRM, project management, analytics dashboards) built entirely within agentic coding sessions. This is a paradigm shift in software production.

- **Prompt Engineering Infrastructure:** The systematic collection and analysis of AI tool prompts (`x1xhlol/system-prompts-and-models`) is becoming a recognized knowledge domain. Treating prompts as data to be curated, versioned, and reverse-engineered is a fast-emerging practice with lasting value.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*