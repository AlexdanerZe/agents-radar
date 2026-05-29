# AI Open Source Trends 2026-05-29

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-29 02:54 UTC

---

# AI Open Source Trends Report: 2026-05-29

---

## 1. Today's Highlights

**The "Agent Skills" Standard is Solidifying at an Industry Level.** Anthropic's official `skills` repository has triggered a cascading wave of innovation in the meta-tooling layer (Superpowers, Harness, ECC), establishing "skill engineering" as the successor to prompt engineering. Concurrently, **persistent memory layers are becoming the new architectural star**, with `claude-mem`, `mem0`, and `memvid` accumulating massive stars by solving the stateless-agent amnesia problem. Notably, **Chinese open-source projects dominate the application layer**, with practical vertical tools like `MoneyPrinterTurbo` (video generation) and `Understand-Anything` (code knowledge graphs) taking the top trending spots. Finally, the emergence of `Leann` (97% storage savings for on-device RAG) and `MOSS-TTS` (high-fidelity open-source speech) signals a push toward **privacy-first, on-device, and multimodal AI infrastructure**.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure / Frameworks & Skills

- **[anthropics/skills](https://github.com/anthropics/skills)** — ⭐?? (+718 today)  
  Anthropic's official public repository defining the Agent Skills format; the industry reference standard for composable agent capabilities.

- **[obra/superpowers](https://github.com/obra/superpowers)** — ⭐0 (+1,730 today)  
  An opinionated agentic skills framework and software development methodology that is rapidly being adopted as an alternative to raw prompt engineering.

- **[microsoft/markitdown](https://github.com/microsoft/markitdown)** — ⭐0 (+1,410 today)  
  Python tool for converting files/Office documents to Markdown; solves the critical raw-data normalization pipeline for LLM ingestion.

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** — ⭐81,307  
  The industry-standard high-throughput, memory-efficient inference engine; unchanged, but remains the backbone of self-hosted LLM serving.

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** — ⭐96,082  
  Makes websites accessible as tool-calling environments for AI agents; has become essential browser automation middleware.

- **[activepieces/activepieces](https://github.com/activepieces/activepieces)** — ⭐22,459  
  An open-source AI agent and MCP workflow automation platform (~400 MCP servers), acting as a consolidation layer for agent tooling.

- **[jackwener/OpenCLI](https://github.com/jackwener/OpenCLI)** — ⭐22,955  
  Transforms any website into a CLI consumable by AI agents; a clever infra hack for agentic browsing without headless browsers.

- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** — ⭐0 (+1,385 today)  
  Agent harness performance optimization system with instincts, memory, and security support for Claude Code, Codex, and Cursor.

---

### 🤖 AI Agents / Workflows

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐171,716  
  The leading fully open-source generalist agent framework; the "agent that grows with you" has cemented its place as the PyTorch of agents.

- **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)** — ⭐44,936  
  Super-agent harness (formerly chatgpt-on-wechat) that plans tasks, runs tools/skills, and manages autonomous memory; epitomizes the all-in-one agent runtime.

- **[shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)** — ⭐63,341  
  A nano agent harness built from scratch for educational purposes, demystifying how Claude Code and similar systems work internally.

- **[langgenius/dify](https://github.com/langgenius/dify)** — ⭐143,018  
  The dominant open-source platform for production agentic workflow development; widely deployed in enterprise AI stacks.

- **[ruvnet/ruflo](https://github.com/ruvnet/ruflo)** — ⭐56,163  
  Leading agent orchestration platform with self-learning swarm intelligence; pushing boundaries in multi-agent coordination.

- **[santifer/career-ops](https://github.com/santifer/career-ops)** — ⭐47,695  
  A standout vertical agentic application — 14 skill modes for fully automated AI-powered job search, including PDF generation and batch processing.

- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** — ⭐31,830  
  The frontend stack for agents and Generative UI (React/Angular), including the AG-UI Protocol; bridges agent backends to user-facing interfaces.

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** — ⭐46,508  
  An AI productivity studio with 300+ assistants and autonomous agents, representing the "super-app" consolidation trend in desktop AI clients.

---

### 📦 AI Applications (Specific Vertical Solutions)

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** — ⭐0 (+4,698 today)  
  **Today's #1 trending repo.** One-click AI-powered high-definition short video generation using LLM models. Huge virality in content creation communities.

- **[Lum1104/Understand-Anything](https://github.com/Lum1104/Understand-Anything)** — ⭐0 (+3,776 today)  
  **Today's #2 trending repo.** Converts any codebase into an interactive, searchable knowledge graph with LLM-powered Q&A. "Graphs that teach" is resonating strongly.

- **[Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill)** — ⭐0 (+2,234 today)  
  A one-shot skill file that gives AI "good taste" by constraining outputs to non-boring, non-generic prose. Directly addresses the "slop crisis" in AI content.

- **[hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop)** — ⭐0 (+761 today)  
  Complementary to taste-skill; explicitly removes stereotypical "AI tells" (hallmark phrases, overly formal tone) from generated prose.

- **[twentyhq/twenty](https://github.com/twentyhq/twenty)** — ⭐0 (+493 today)  
  Open-source Salesforce alternative, purpose-built for AI. Natively designed for AI data ingestion and agentic CRM workflows.

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — ⭐22,155  
  Converts any document into fully editable PowerPoint (.pptx) with native shapes and animations — not just images pasted into slides.

- **[OpenMOSS/MOSS-TTS](https://github.com/OpenMOSS/MOSS-TTS)** — ⭐0 (+71 today)  
  High-fidelity open-source speech, sound generation, and real-time streaming TTS model family from MOSI.AI and the OpenMOSS team.

---

### 🧠 LLMs / Training & Fine-Tuning

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** — ⭐71,684  
  The unified standard for efficient fine-tuning of 100+ LLMs/VLMs. Remains unchallenged as the go-to tool for model customization.

- **[OpenMOSS/MOSS-TTS](https://github.com/OpenMOSS/MOSS-TTS)** — ⭐0 (+71 today)  
  New open-source speech/sound generation family covering long-form TTS, multi-speaker dialogue, voice design, and environmental sound effects.

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — ⭐7,044  
  Comprehensive LLM evaluation platform spanning 100+ datasets. Becoming increasingly critical as the model landscape diversifies.

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** — ⭐4,215  
  A course teaching LLM inference serving on Apple Silicon (build a tiny vLLM + Qwen); bridges the gap between systems engineering and ML.

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** — ⭐236  
  A new minimal library for reliable, scalable pretraining of foundation world models — filling an important infrastructure gap for research teams.

- **[thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL)** — ⭐1,454  
  Awesome list for Agentic RL; tracks the convergence of reinforcement learning and agent architectures, a critical research frontier.

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** — ⭐96,200  
  The definitive educational resource for building a ChatGPT-like LLM step-by-step in PyTorch.

---

### 🔍 RAG / Knowledge & Vector Databases

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** — ⭐79,432  
  **The most-starred project in this category.** Compresses all agent session activity and injects relevant context into future sessions. Redefines RAG as persistent memory.

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — ⭐57,008  
  Universal memory layer for AI agents. Establishes "memory" as a distinct architectural stack separate from traditional vector search.

- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** — ⭐55,686  
  Turns any folder of code, docs, images, or videos into a queryable knowledge graph; blends RAG with graph-based reasoning for agent skills.

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** — ⭐60,749  
  The all-in-one AI productivity accelerator; on-device, privacy-first RAG and document interaction.

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** — ⭐17,574  
  Memory control plane for AI agents in 6 lines of code. Pushing ergonomics for developer adoption of agent memory layers.

- **[yichuan-w/LEANN](https://github.com/yichuan-w/LEANN)** — ⭐11,806  
  "RAG on Everything with LEANN" — 97% storage savings while running 100% private RAG on personal devices. A breakthrough in efficient on-device retrieval.

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — ⭐44,516  
  The high-performance cloud-native vector database remains the backbone of production RAG architectures.

- **[NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)** — ⭐27,613  
  Comprehensive tutorial notebooks covering advanced RAG techniques; the community textbook for modern retrieval-augmented generation.

---

## 3. Trend Signal Analysis

**The Skill-Engineering Paradigm Has Arrived.** The explosive convergence of Anthropic's official `skills` repo, `superpowers`, `ECC`, `harness`, and content-quality skills (`taste-skill`, `stop-slop`) represents a fundamental shift: the community is no longer experimenting with prompt templates but building a full software engineering discipline around agent behavior specification. This is the most important signal in today's data — the agent ecosystem is maturing from hackable scripts to modular, composable, production-grade architectures.

**"Memory" vs. "Retrieval" — An Architectural Divergence.** Projects categorized under RAG are increasingly rebranding themselves as "memory layers." The massive stars on `claude-mem`, `mem0ai`, `memvid`, and `cognee` indicate that the community has concluded that "retrieving chunks" is insufficient for production agents. The new requirement is a cognitive memory system that compresses, preferences, prioritizes, and injects context across sessions. This is a genuine architectural evolution away from raw vector search toward structured, long-term state management for agents.

**On-Device, Private, and Efficient is the Unserved Frontier.** The presence of projects like `LEANN` (97% storage savings for private RAG), `picollm` (on-device X-bit quantization inference), and `MOSS-TTS` (open-source speech models) highlights a hunger for tools that break dependence on cloud APIs. As enterprises and privacy-conscious users balk at sending data to third-party LLM providers, the open-source ecosystem is rapidly building the stack for fully local, affordable, and capable AI — representing a substantial investment opportunity for infrastructure in this direction.

**China's AI Application Engine is Accelerating.** Chinese open-source projects were historically strong in model releases and foundational frameworks. Today's trending data shows a decisive shift: Chinese developers are now leading in the *application layer*, where English-first user experiences (`MoneyPrinterTurbo`, `Understand-Anything`, `PPT-Master`) are achieving global mass adoption. This suggests that the center of gravity for open-source AI *productization* is moving east.

**The "Harness" War is On.** Multiple competing "agent harness" systems (ECC, CowAgent, Superpowers, OpenClaude, learn-claude-code) are vying to be the default runtime for agentic coding. This is the new "operating system" battle of the AI era. The model provider that can define and standardize this harness layer (Claude Code's skill format being the current frontrunner) will wield immense influence over the entire ecosystem.

---

## 4. Community Hot Spots

- 🏆 **[Agent Skills Standardization](https://github.com/anthropics/skills)** — The highest-leverage activity for an AI developer today. Learning to build composable, shareable skills (as opposed to one-shot prompts) is the new core competence. The ecosystem around `superpowers` and `taste-skill` shows early entrants are building defensible expertise here.

- 🧠 **[Persistent Agent Memory Layers](https://github.com/mem0ai/mem0)** — This is the most significant architectural shift since vector databases. Production agents cannot succeed without long-term memory. Tools like `mem0ai` and `claude-mem` are rapidly becoming as critical as the LLM itself for any agentic application.

- 🖥️ **[Coding Agent Harnesses](https://github.com/zhayujie/CowAgent)** — The competition between CowAgent, ECC, and OpenClaude defines how AI will interact with software engineering. This is the new IDE/kernel war. Developers should understand the architecture of at least one harness deeply to shape how coding agents work.

- 🎙️ **[Open-Source Multimodal Generation](https://github.com/OpenMOSS/MOSS-TTS)** — High-quality open-source TTS and sound generation remains underserved. MOSS-TTS fills a critical gap for game dev, accessibility, and content creation workflows that cannot rely on proprietary APIs like OpenAI TTS.

- 🔍 **[Reasoning Graph RAG](https://github.com/Lum1104/Understand-Anything)** — The community sentiment "graphs that teach > graphs that impress" signals a strong desire for interactive, structuring knowledge representation over flat retrieval. Watch this direction as it merges code understanding, document analysis, and agent memory into a single paradigm.

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*