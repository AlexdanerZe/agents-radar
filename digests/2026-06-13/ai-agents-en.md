# OpenClaw Ecosystem Digest 2026-06-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-13 03:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

## OpenClaw Project Digest — 2026-06-13

### 1. Today's Overview

Project activity is extremely high, with **500 issues** and **500 pull requests** updated in the last 24 hours, alongside two new releases. The dominant theme is a major security hardening sweep, with v2026.6.6 tightening boundaries across transcripts, sandboxes, MCP, and the execution pipeline. This momentum, however, is sharply tempered by the surfacing of **two P0 critical bugs** — a severe gateway memory leak and a broken memory search index — that demand immediate maintainer intervention. 144 PRs were merged or closed over the cycle, indicating a highly responsive development process operating under significant stability pressure.

---

### 2. Releases

Two new versions were published today: **v2026.6.6** and **v2026.6.6-beta.2**.

- **Highlights (identical for both):** Security boundaries are substantially tighter across transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, elevated sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group actions; exec
- **Analysis:** This is a broad, systemic security release. The prominent mention of `exec` suggests significant hardening of the command approval and execution pipeline. **Users upgrading should review their `exec` approval policies, sandbox configurations, and environment variable inheritance rules**, as these changes may enforce stricter default security postures that break existing workflows.

---

### 3. Project Progress

144 PRs were merged or closed in the last 24 hours, reflecting strong development throughput.

- **Security Fixes (Merged/Closed):**
    - **Bootstrap token rate-limiting** ([PR #76322]) — Closed. Added rate limiting and failure recording to the bootstrap token WebSocket path, closing a mutex-stall DoS vector.

- **Platform & Integration Fixes (Merged/Closed):**
    - **Kimi K2.6 regression** ([#71491]) — Closed. Resolved `reasoning_content` 400 errors in long conversations after LCM context compaction.
    - **Gateway event loop saturation** ([#75378]) — Closed. Fixed a 1012 service restart when spawning 3 subagents simultaneously with heavy models.
    - **OpenAI Codex SSE abort** ([#66561]) — Closed. Fixed local abort of SSE responses being surfaced as generic timeouts.
    - **ClawHub CI** ([PR #92311]) — Closed. Split plugin publishing into normal OIDC and protected token bootstrap paths.
    - **Codex chat plan controls** ([PR #88446]) — Closed. Added native plan-mode controls and `think` defaults for bound Codex conversations.

- **Fixes In Flight (Open PRs):**
    - **Control UI token leak** ([PR #92584]) — Aims to stop the gateway from accepting the shared secret via the `?token=` query string.
    - **Cron delivery channel resolution** ([PR #92580]) — Persists resolved delivery targets into isolated cron session contexts.
    - **Model registry resilience** ([PR #92585]) — Fixes invalid plugin catalog shards from aborting the entire model loading process.
    - **Slack final reply mirroring** ([PR #92498]) — Mirrors same-channel final replies into the owning session transcript.
    - **Session identity in runtime prompt** ([PR #92468]) — Carries `sessionKey`/`sessionId` into the runtime prompt for session-aware agent behaviors.

- **Control UI Overhaul (Open Community PRs):**
    - A significant series from contributor **BunsDev** is open and awaiting review, targeting UX, accessibility, mobile responsiveness, and visual polish for the admin dashboard. These represent a major community investment in the project's frontend.

---

### 4. Community Hot Topics

The most active discussions reveal strong user demand for workflow reliability and explicit security controls.

- **[#18160] Direct Exec Mode for Cron Jobs** (13 comments, 11 👍) — The community is loudly requesting a non-LLM path for cron jobs to eliminate timeouts and API costs. This is a top candidate for the next roadmap sprint.
- **[#25592] Text Leaks Between Tool Calls** (32 comments, P1, Security) — A high-severity UX and data-loss issue where internal agent narration is sent to public channels. A fix PR is open but awaiting product and security reviews.
- **[#9443] Prebuilt Android APK** (25 comments, P2) — A long-standing request for compiled APK downloads. Demand remains high, with no product decision yet.
- **[#27445] Sub-Agent Announce Target** (10 comments, 5 👍) — Users want to route sub-agent completion messages back to the parent session for orchestration, rather than directly to the channel.
- **[#6615] Exec-Approvals Denylist** (7 comments, 7 👍) — Strong demand for "allow everything except X" policies to complement the current allowlist.
- **[#20786] Telegram Business Bot Support** (8 comments, 6 👍) — Extending the integration for Business-connected personal chats.

---

### 5. Bugs & Stability

Stability is a significant concern today, with several P0 and P1 regressions actively impacting users.

- **P0 — Critical:**
    - **Memory Leak** ([#91588]) — Gateway RSS grows from 350 MB to 15.5 GB over days, causing repeated OOM and `launchd-handoff` cycles on normal use. **No fix PR is linked.**
    - **Memory Search Broken** ([#91778]) — `memory_search` index metadata is missing since v2026.6.1, rendering memory search non-functional. Report is in French, severity rated P0. Needs live reproduction.

- **P1 — High Severity:**
    - **Text Leaks Between Tool Calls** ([#25592]) — Internal text routed to channels. Fix PR exists but is blocked by product/security review.
    - **Session Context Confusion** ([#32296]) — Agent replies to the previous message instead of the current one. Needs maintainer review.
    - **Bootstrap Files Ignored** ([#29387]) — Per-agent `agentDir` configs silently failing. Fix PR is open.
    - **Signal Daemon Race Condition** ([#22676]) — SIGUSR1 restarts cause orphaned processes and port contention. No maintainer review since Feb.
    - **Sandbox Workspace Read-Only** ([#37634]) — Tools requiring filesystem writes fail inside isolated sandboxes.
    - **Duplicate Messages** ([#88951]) — Messages duplicated 2–4 times after upgrading to v2026.5.27+.
    - **WhatsApp Session Stalls** ([#84569]) — Long model calls cause incomplete turns and message loss.
    - **Deferred Turn Livelocks** ([#77340]) — Lane collisions cause monotonic trailing assistant accumulation.
    - **Gateway Memory Leak** ([#91588]) — P0, described above.
    - **Heartbeat Delivery Bug** ([#83184]) — `pendingFinalDelivery` is never cleared, blocking subsequent heartbeat cycles.
    - **Write-Lock Timeouts** ([#86538]) — Session JSONL locks block subagent delivery lanes.
    - **Compaction Timeout** ([#92043]) — The new 180 s compaction timeout turns slow-but-recoverable compactions into permanent failures (fix PR is open).
    - **Exec Env Inheritance** ([#31583]) — Skills env vars not passed to `exec` subprocesses (regression).
    - **Google Vertex Regression** ([#38327]) — `"Cannot convert undefined or null to object"` on v2026.3.2 with `gemini-3.1-pro-preview`.
    - **Gateway Pairing Deadlock** ([#74484]) — CLI cannot approve/reject over-scoped repair requests due to scope mismatch.
    - **Subagent Session Persistence** ([#47975]) — Main session becomes unresponsive after subagent completion.

- **P2 — Regressions:**
    - **Control UI HTTPS Requirement** ([#32473]) — Blocks users on plain HTTP VPS setups. Needs product decision.
    - **Webchat Avatar 404** ([#38439]) — Avatar endpoint returns 404. Needs live reproduction.
    - **LiteLLM Cache Ignored** ([#37966]) — `cacheRetention` silently ignored for LiteLLM-proxied Anthropic models.

---

### 6. Feature Requests & Roadmap Signals

The project's roadmap is clearly steering toward better security and user control over agent execution.

- **High Probability for Next Release:**
    - **Tiered Bootstrap Loading** ([#22438]) — Progressive context control is highly requested for token management.
    - **Direct Cron Exec** ([#18160]) — The strongest community signal (11 👍) indicates this is a critical workflow gap.
    - **Exec-Approvals Denylist** ([#6615]) — Directly aligns with the current "security boundary tightening" theme.
    - **Sub-agent Routing** ([#27445]) — Essential for complex multi-agent automation.

- **Longer Term / Under Discussion:**
    - **Slack Block Kit** ([#12602]) — Richer message formatting.
    - **Dynamic Model Discovery** ([#10687]) — Automatic updates for provider model lists (e.g., OpenRouter).
    - **Multi-Agent Collaboration RFC** ([#35203]) — Formal proposal for capability profiling, shared blackboards, and token cost governance.
    - **Backup & Restore Utility** ([#13616]) — Standardized disaster recovery and environment migration.
    - **Native Secrets Management** ([#13610]) — Vault / AWS Secrets Manager integration.
    - **Tool Schema Optimization** ([#14785]) — Reducing the ~3,500 token tax of full tool schemas per session.
    - **Pre-Response Enforcement Hooks** ([#13583]) — Hard gates for mandatory tool-call policies in high-stakes workflows.

---

### 7. User Feedback Summary

- **Significant Pain Points:**
    - **Stability Regressions:** Users are expressing frustration with recent versions breaking core features like memory search ([#91778]) and causing message duplication ([#88951]).
    - **Sandbox Usability:** The read-only workspace mount in sandboxes ([#37634]) is a major blocker for users trying to leverage the sandbox for development.
    - **Configuration & Onboarding Gaps:** The lack of native secrets management and backup utilities suggests a high operational burden. The gap in memory setup during onboarding ([#16670]) is a noted deficiency.
    - **Cron Reliability:** The forced reliance on `agentTurn` for cron jobs is a significant source of timeouts and unnecessary API costs ([#18160]).

- **Satisfaction & Engagement:**
    - The sheer volume of activity (500+ PRs/Issues) and 144 merged PRs demonstrates a deeply engaged and invested community.
    - The comprehensive Control UI overhaul PRs from **BunsDev** represent high-quality community investment in the project's future.
    - High 👍 counts on feature requests (Cron exec, Telegram Business, exec denylist) show an active user base strategically shaping the product.

---

### 8. Backlog Watch

Several high-impact issues are languishing without maintainer input or a clear path forward.

- **[#25592] Text Leaks Between Tool Calls (P1, Security)** — Open since Feb 24. A diamond-lobster-rated security issue with a fix PR waiting for product/security review. Needs urgent unblocking.
- **[#9443] Prebuilt Android APK (P2, Enhancement)** — Open since Feb 5. A significant barrier for mobile users. Requires a product decision.
- **[#22676] Signal Daemon Race Condition (P1, Crash-Loop)** — Open since Feb 21. A clear reproduction exists, but the issue lacks a maintainer review.
- **[#10687] Dynamic Model Discovery (P2, Enhancement)** — Open since Feb 6. Has a linked PR but needs a product decision. Critical for users of APIs with fast-moving model catalogs.
- **[#14785] Tool Schema Token Overhead (P2, Enhancement)** — Open since Feb 12. A hard "diamond lobster" rated issue aiming to fix a ~3,500 token tax on every session. Needs a product decision.
- **[#13610] Native Secrets Management (P3, Security)** — Open since Feb 10. No maintainer review despite being a high-impact security best-practice request.
- **[#47975] Subagent Session Persistence (P1, Session State)** — Open since Mar 16. Needs live reproduction but is a confirmed blocker for complex multi-agent workflows.
- **[#38439] Webchat Avatar 404 (P2, Regression)** — Open since Mar 7. A noticeable UX regression needing live reproduction.

---
*This digest reflects a project scaling rapidly, shipping aggressive security features while grappling with the regressions that high-speed development can introduce. The community is robust and vocal, providing clear signals on where the project should focus its stabilization and feature efforts next.*

---

## Cross-Ecosystem Comparison

**Cross-Project Ecosystem Comparison Report: AI Agent Open-Source Landscape**
**Date:** 2026-06-13
**Scope:** 12 active projects in the personal AI assistant / agent open-source ecosystem

---

### 1. Ecosystem Overview

The open-source agent ecosystem is in a hyper-competitive phase of fragmentation and convergence. The "Claw" architecture family—characterized by a modular gateway, sandboxed execution, MCP integration, and multi-channel delivery—has become the dominant design pattern, with OpenClaw serving as the reference implementation and multiple forks (NanoClaw, PicoClaw, ZeroClaw, IronClaw) diverging across specific strategic axes. Development velocity is extreme across the board, with the top five projects collectively processing over 1,300 issues and PRs in a single 24-hour cycle. However, this pace is producing significant stability pressure: critical memory bugs, context management failures, and onboarding friction are emerging as universal growing pains as the ecosystem transitions from experimental prototypes toward production infrastructure.

---

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | PRs Merged/Closed | Releases (24h) | Est. Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 144 | 2 (v2026.6.6) | 8/10 – Highest volume; P0 regressions erode stability confidence |
| **IronClaw** | 50 | 50 | Several UX/Infra | 0 | 8/10 – Blistering feature pace; CI failure blocks merge queue |
| **Hermes Agent** | 50 | 50 | 3 | 0 | 8/10 – High engagement, responsive fix cycles, desktop narrative growing |
| **ZeroClaw** | 12 | 36 | 4 | 0 | 7/10 – Major RFCs in flight; S1 onboarding bugs threaten growth |
| **NanoBot** | 6 | 29 | 9 | 0 | 7/10 – High feature velocity; critical memory bug (#4044) unresolved |
| **CoPaw (QwenPaw)** | 21 | 23 | 10 | 0 | 8/10 – Excellent responsiveness; patch regression risk |
| **NanoClaw** | 0 | 18 | 10 | 0 | 9/10 – Best merge-to-open ratio; fixing core crash loops rapidly |
| **PicoClaw** | 6 | 14 | 3 | 1 (nightly) | 8/10 – Lean execution; strong architectural focus on protocols |
| **LobsterAI** | 1 | 17 | 11 | 0 | 8/10 – Clear pre-release sprint; Computer Use MVP is a major differentiator |
| **Moltis** | 3 | 0 | 0 | 0 | 4/10 – Triage/discussion; no code production |
| **NullClaw** | 1 | 3 | 0 | 0 | 5/10 – Stable but low throughput; stagnation risk if unreviewed |
| **TinyClaw** | 0 | 0 | 0 | 0 | 2/10 – Dormant |

---

### 3. OpenClaw's Position

**Advantages:**
- **Undisputed market share and mindshare:** Community volume is 5–10x larger than the nearest peer. 144 PRs merged in 24 hours demonstrates unmatched contributor depth and maintainer capacity.
- **Architecture reference standard:** Sets the security baseline (v2026.6.6 systemic hardening), MCP integration patterns, and sandbox execution model that the rest of the ecosystem follows.
- **Mature gateway and pipeline:** Most comprehensive implementation of the agent turn loop, exec approvals, and multi-channel delivery.

**Key Weaknesses vs. Peers:**
- **Complexity-induced fragility:** P0 bugs (memory leak #91588, search index #91778) directly break core value propositions. The scale of codebase churn increases regression surface.
- **UX iteration gap:** Lacks the polished desktop/WebUI investments seen in IronClaw (WebUI v2) and Hermes (Desktop Kanban, unified history). Strictly backend/protocol focused.
- **Configuration overhead:** The "Big Tent" security and configuration surface creates onboarding friction compared to leaner forks like NullClaw or PicoClaw.

**Technical Approach Differences:**
| Dimension | OpenClaw | Peers (Example) |
|---|---|---|
| **Language** | Rust (heavy, integrated) | Zig (Null – minimal), Python (NanoBot, CoPaw – research speed) |
| **Runtime Model** | Gateway + Agent Core | IronClaw: Reborn runtime. ZeroClaw: Unified turn engine RFC |
| **UI Philosophy** | Minimal (Admin dashboard, config) | Hermes: Desktop first. IronClaw: WebUI v2. LobsterAI: Computer Use |
| **Extensibility** | Plugin ecosystem | ZeroClaw pushing WASM (wasmtime PR #7429) |

---

### 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple projects, indicating convergent evolution:

| Area | Projects Affected | Specific Signals |
|---|---|---|
| **Context Window & Memory Governance** | OpenClaw, NanoBot, Hermes, IronClaw, CoPaw, NanoClaw | P0 broken search (OpenClaw #91778), short-term memory loss (NanoBot #4044), compression integration (Hermes #39691), context slice (IronClaw #4828), long context hang (CoPaw #5161) |
| **Security Boundaries & Approval Systems** | OpenClaw, NanoClaw, PicoClaw, IronClaw | v2026.6.6 hardening, exec denylist (OpenClaw #6615), container cap-drop (NanoClaw #2748), group permissions (PicoClaw #3109/3114), persistent approvals (IronClaw #4825) |
| **Multi-Agent / Sub-Agent Orchestration** | OpenClaw, CoPaw, NanoBot, IronClaw | Sub-agent routing (OpenClaw #27445), swarm/collaboration (CoPaw #5139), cron subagent lifecycle (NanoBot #4304), DeferredBusy thread blocking (IronClaw) |
| **MCP Infrastructure Hardening** | ZeroClaw, NanoClaw, Moltis, OpenClaw | Auto-reconnect (ZeroClaw #7351), tool injection (ZeroClaw #7547), per-tool timeouts (NanoClaw #2668), Fastmail auth failure (Moltis #1115) |
| **Desktop / Web UI Maturation** | Hermes, IronClaw, LobsterAI, CoPaw, NanoBot | Kanban integration (Hermes #41222), WebUI v2 QA (IronClaw), Computer Use (LobsterAI), WebUI config parity (NanoBot #4313), Coding Mode UI (CoPaw #5147) |
| **Channel Platform Expansion** | NanoClaw (Signal), PicoClaw (DeltaChat), ZeroClaw/CoPaw (Feishu/DingTalk), OpenClaw (Telegram Business), IronClaw (Slack re-arch) | The agent is racing to become the universal integration bus across all major messaging ecosystems |

---

### 5. Differentiation Analysis

| Strategic Axis | Project Cluster | Characteristics |
|---|---|---|
| **Language & Runtime** | **Rust cluster** (OpenClaw, IronClaw, ZeroClaw, NanoClaw, PicoClaw) vs. **Python cluster** (NanoBot, CoPaw, LobsterAI) vs. **Zig outlier** (NullClaw) | Rust projects prioritize performance, static compilation, and low latency. Python projects prioritize research velocity, ML integration, and flexible prompt orchestration. Zig offers minimal binary size and direct OS integration. |
| **Target User** | **Platform Devs / Integrators:** OpenClaw, ZeroClaw, NullClaw<br>**Power Users / Prosumers:** Hermes, NanoBot, PicoClaw, CoPaw<br>**Enterprise POC:** IronClaw, LobsterAI | Decision point: Deep control and API surface vs. polished UX and onboarding velocity. IronClaw's Reborn WebUI v2 explicitly targets the enterprise UX gap. |
| **Architecture Philosophy** | **Batteries-included / Integrated stack:** OpenClaw, IronClaw<br>**Lean / Minimal fork:** NullClaw, PicoClaw<br>**Research / Experimental:** NanoBot (Dreams, SOUL.md), CoPaw (Runtime 2.0, AgentOS driver) | Integrated stacks offer coherence but increased complexity. Lean forks offer speed and low cognitive overhead. Experimental projects test new paradigms (self-modifying prompts, composable executors). |
| **Community Governance** | **Single-org core + ecosystem PRs:** OpenClaw, IronClaw, Hermes<br>**Foundation/Vendor-backed:** NanoBot (HKU), CoPaw (AgentScope), LobsterAI (NetEase) | Vendor-backed projects show stronger sprint cadence and release discipline. Community-driven projects show more diverse contributor input and feature exploration. |

---

### 6. Community Momentum & Maturity

**Tier 1 – Core Powerhouses (Extreme Volume, Agenda Setting)**
- **OpenClaw** and **IronClaw** dominate raw activity (500+ items each). Both are pushing security and UI boundaries respectively. Stability risk is highest here due to sheer surface area.

**Tier 2 – High-Growth Specialists (Strong Velocity, Clear Niche)**
- **NanoBot:** Solving memory governance (#4044) is the single highest-impact open engineering problem in the ecosystem. If resolved, this project leapfrogs.
- **Hermes Agent:** Best Desktop + Multi-platform story among the group. Strong provider integration focus.
- **NanoClaw:** Highest operational maturity (9/10 health). Rapidly closes critical bugs. Production-ready Signal channel is a competitive differentiator.
- **CoPaw (QwenPaw):** Most responsive to regressions. Significant Chinese-language community signal. Runtime 2.0 refactor indicates architectural confidence.
- **ZeroClaw:** High execution risk (major RFCs in flight). WASM plugin system and unified turn engine are ambitious architectural bets.
- **LobsterAI:** Most differentiated feature (Computer Use MVP). Scheduled task and voice features target workflow automation use case directly.

**Tier 3 – Lean / Niche (Lower Volume, Targeted Impact)**
- **PicoClaw:** Strong architectural vision (WebSocket lifecycle, DeltaChat). Permission scoping is a pressing community demand.
- **NullClaw:** Smallest viable contributor base. Risk of stalling if PRs #949/#951/#953 drift without maintainer review.

**Tier 4 – Pre-Production / Dormant**
- **Moltis** is in a feature planning/triage cycle. **TinyClaw** and **ZeptoClaw** are inactive. These projects lack the daily development signal to be considered competitive.

---

### 7. Trend Signals

**1. Security has moved from "nice-to-have" to "non-negotiable."**
The v2026.6.6 systemic hardening release from OpenClaw, combined with dedicated container isolation and npm supply-chain hardening PRs across NanoClaw (#2748, #2749) and PicoClaw (permission scoping #3109), confirms that production deployments require zero-trust architecture as a baseline. Projects without a clear security narrative will not gain enterprise traction.

**2. Context window management is the universal scaling bottleneck.**
Memory search broken (OpenClaw P0), short-term memory loss (NanoBot P0), context hang (CoPaw), and token overhead (Hermes) all point to the same underlying challenge: current agent architectures cannot reliably maintain state over long interactions. The project that delivers production-grade context governance (intelligent compression, cursor management, semantic decay) will have a decisive competitive advantage.

**3. The "Claw" stack is converging toward a standardized modular architecture.**
The emergence of a shared reference model—gateway → runtime → sandbox → MCP client → channel adapters—across 10+ independent projects mirrors the early OSI model standardization. This convergence lowers switching costs for developers and invites third-party plugin ecosystems. ZeroClaw's WASM plugin PR (#7429) and CoPaw's Agent OS Driver (#5067) are early signals of a formalized plugin economy.

**4. Desktop and rich Web UIs are ending the CLI era for agent tools.**
IronClaw's WebUI v2, Hermes's Desktop app (Kanban, unified history), LobsterAI's Computer Use, and CoPaw's Coding Mode represent a structural shift. The market is demanding persistent state machine interfaces (conversations, workspaces, background processes) rather than stateless chat windows. Projects without a UI investment (NullClaw, PicoClaw) will be increasingly relegated to headless/embedded infrastructure roles.

**5. Multi-channel ubiquity is the table stakes, not the differentiator.**
Signal (NanoClaw), Telegram Business (OpenClaw), Discord fixes (Hermes, NullClaw, NanoClaw), Feishu (CoPaw, ZeroClaw), DeltaChat (PicoClaw), Slack (IronClaw re-arch) — every project is racing to connect agents to every communication platform. The agent inbox is becoming the universal cloud-native integration point. Differentiation now lies not in *which* platforms are supported, but in how reliably and securely they handle multi-session, multi-tenant delivery at scale.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 13, 2026.

---

### 1. Today's Overview
NanoBot is exhibiting extremely high development velocity, with **29 pull requests** active and **6 issues** updated in the last 24 hours. The project is in a dual-phase sprint of **heavy feature delivery** (new TTS, Audit, and SDK systems) alongside **deep stability and security hardening**. While the core team is churning out new capabilities, the most significant community frustration—acute **short-term memory loss** in the agent loop—remains unresolved, though several related bug fix PRs are now in the pipeline. Overall project health is strong, but the backlog of critical security and testing PRs suggests a widening bottleneck in maintainer review capacity.

### 2. Releases
**None.** No new versions or release candidates were published today.

### 3. Project Progress
**9 PRs were merged or closed** in the last 24 hours, driving several key feature completions and bug fixes across the stack:

- **Audit Module (Merged):** `#4319` / `#4318` — The new `tools.audit` system was successfully merged. It provides configurable agent action observability with Loguru, HTTP webhook, JSONL, and programmatic callback transports.
- **Cron Subagent Lifecycle (Merged):** `#4304` — Fixes a critical bug where cron jobs spawning subagents were marked complete before the subagent task finished.
- **Tool Result Fixes (Closed):** `#4203` & `#4006` — Two major bugs in conversation history processing (`find_legal_message_start` discarding all messages and orphaned tool results) were resolved and closed.
- **Open PRs Progressing:**
    - **Refactoring:** `#4314` — Breaking the config schema’s dependency on tool runtime modules to improve modularity.
    - **Testing:** `#4193`, `#3982`, `#3983` — Large testing harnesses for memory lifecycle and agent runners are under review.
    - **Security:** `#4119` (symlink escapes) & `#4053` (read-only roots) remain open but are advancing.

### 4. Community Hot Topics
The community is currently most focused on the stability of the core agent loop and the expansion of configuration surfaces.

- **Short-Term Memory Loss (`#4044`):** The most active and upvoted discussion. User *bjoshuanoah* provides a deep root cause analysis, pointing to context window pressure and system prompt bloat (SOUL.md, USER.md, MEMORY.md) as the primary suspects. The thread has 5 comments and reflects the highest user pain point in the project right now. **[#4044](https://github.com/HKUDS/nanobot/issues/4044)**
- **WebUI / Config Parity (`#4313`):** This large PR from *La-Volpe* closes the gap between the WebUI and `config.json`, adding write endpoints for temperature, tool limits, dream, channels, and memory fields. This is a response to widespread user friction around configuration complexity. **[#4313](https://github.com/HKUDS/nanobot/pull/4313)**
- **Python SDK Expansion (`#4296`):** The PR from *Re-bin* upgrading the Python SDK from a basic `bot.run()` facade to a full developer API with `RunResult` metadata and runtime controls signals a strong user demand for programmatic control and better CI/CD integration. **[#4296](https://github.com/HKUDS/nanobot/pull/4296)**

### 5. Bugs & Stability
Bug reports today are concentrated on the agent session layer, ranked by severity:

- **Critical – Short-Term Memory Loss (`#4044`):** The agent is losing conversational context between turns, making multi-message interactions largely broken for many users. This remains the highest-priority stability issue in the project. No dedicated fix PR exists yet, though related context cursor fixes are in review.
- **Critical – Post-Turn Consolidation Wipes Messages (`#4307`):** When `context_window_tokens` is set modestly, consolidation fires after a long turn and archives the assistant’s own delivery message, causing user follow-up references to be lost entirely. A highly disruptive behavior reported by *MARJORIESHA-pBAD*.
- **High – Zero Usage Tokens in API (`#4309`):** The `/v1/chat/completions` endpoint always returns hardcoded `0` for `prompt_tokens`, `completion_tokens`, and `total_tokens`. This breaks billing, token counters, and any downstream tooling relying on OpenAI-compatible usage stats.
- **High – MCP Server Crash on Reconnect (`#4303`):** A `RuntimeError` related to cancel scopes occurs when an MCP server session terminates and reconnects. A fix PR is active.
- **Medium – Dream Cursor Bloat (`#4321`):** With Dream disabled, the cursor never advances, causing unbounded prompt bloat over time. A fix PR is active.
- **Medium – Memory Cursor Non-Monotonic (`#4256`):** History cursors can go stale or negative, leading to incorrect reads. A fix PR is active.

### 6. Feature Requests & Roadmap Signals
The merge queue and active PRs provide a strong signal of where the project is heading in the next release:

- **Multi-Provider TTS (High Likelihood):** `#4316` adds a full TTS config system supporting OpenAI, Groq (Orpheus), and ElevenLabs. This is a major leap for voice-based interactions and is actively being integrated with the WebUI settings API.
- **Agent Action Audit (High Likelihood):** The `tools.audit` feature has already been merged. Expect it in the next release, providing the foundation for enterprise monitoring and compliance.
- **Configuration Parity (High Likelihood):** The WebUI parity PR (`#4313`) is large and detailed, indicating a strong push to eliminate the current config.json vs. WebUI gap before the next stable release.
- **Multiple Custom Providers (Uncertain):** `#4305` requested a template parameter for custom providers. It was closed quickly without a merged solution, suggesting the feature may be landing in a different architectural form or is currently deprioritized.

### 7. User Feedback Summary
- **Dissatisfaction:** Agent memory is the dominant pain point. Users are reporting that conversational threads “snap” between turns, making sustained reasoning across a dialogue unreliable. The loss of the agent’s own delivery message during consolidation (`#4307`) is driving acute frustration for users with constrained context windows.
- **Desire for Observability:** There is clear demand from power users and deployers for better monitoring. The community response to the Audit module and the detailed nature of the SDK expansion PR suggest a growing enterprise/ops user base that needs production telemetry and scripting.
- **Complexity Barrier:** The heavy investment in WebUI parity implies significant user feedback about the difficulty of navigating the raw `config.json` settings.

### 8. Backlog Watch
Several high-value items are languishing without maintainer action or merge, creating risk:

- **`#4044` – Short-Term Memory Loss (Open 16 Days):** This is the single most impactful bug in the project. The lack of a confirmed fix or detailed maintainer response is the biggest risk to user retention.
- **`#4119` – Symlink Workspace Escape (Open 13 Days):** A security vulnerability fix from *yu-xin-c* that blocks relative symlink escapes. It has no recent activity from maintainers, despite being critical for sandbox security.
- **`#4053` – Read-Only Root Write Protection (Open 15 Days):** Another security hardening PR from *yu-xin-c* waiting for review. It prevents write tools from inheriting read-only media directory paths.
- **`#3982` & `#4193` – Testing Harnesses (Open 20+ Days):** These extensive test framework PRs (scripted agent runner harness and memory lifecycle harness) are foundational for preventing regressions. Their long stall time suggests a serious capacity constraint in the maintainer review cycle for complex infrastructure code.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

**Hermes Agent Project Digest — 2026-06-13**

---

### 1. Today’s Overview
Hermes Agent saw a surge in activity on June 13, with 50 issues and 50 PRs updated, signaling a highly productive phase focused on debugging and enhancing provider and gateway integrations. While 2 issues were closed and 3 PRs were merged, the vast majority of activity remains open (48 issues, 47 PRs), indicating an intense development cycle with rapid iteration. The community is heavily engaged in reporting specific regressions around Desktop UI, gateway chat flooding, and provider authentication flows. No new releases were published today, but the concentrated fix efforts point towards a significant upcoming build.

---

### 2. Releases
No new releases were published today.

---

### 3. Project Progress
The project saw 3 PRs merged today, but the overall health and velocity are best observed in the 47 open PRs actively resolving high-priority bugs. The most coordinated development effort is around the `notify_on_complete` feature, with multiple contributors providing overlapping fixes to restrict background process notifications to successful exits only:
- **Process Notifications**: PRs [#45357](https://github.com/NousResearch/hermes-agent/pull/45357), [#45359](https://github.com/NousResearch/hermes-agent/pull/45359), and [#45366](https://github.com/NousResearch/hermes-agent/pull/45366) all target the same root cause.
- **Provider Compatibility**: [#45364](https://github.com/NousResearch/hermes-agent/pull/45364) strips unsupported `reasoning_content` fields to fix API crashes; [#45370](https://github.com/NousResearch/hermes-agent/pull/45370) defaults macOS installer to native TLS.
- **CLI/Cron & Dashboard**: [#45350](https://github.com/NousResearch/hermes-agent/pull/45350) adds the `--profile` flag to all cron subcommands; [#45349](https://github.com/NousResearch/hermes-agent/pull/45349) restores the last chat on bare `/chat` startup.
- **Desktop & Web**: [#45355](https://github.com/NousResearch/hermes-agent/pull/45355) adds a show/hide toggle for gitignored files; [#45348](https://github.com/NousResearch/hermes-agent/pull/45348) ships a full French (fr) locale; [#45373](https://github.com/NousResearch/hermes-agent/pull/45373) requires explicit backend selection for web tools.

---

### 4. Community Hot Topics
The highest engagement was driven by a mix of critical bugs and UX feature requests:
- **[#39691](https://github.com/NousResearch/hermes-agent/issues/39691) — feat(compression): integrate headroom-ai** (6 👍): The most popular feature request signals strong demand for moving beyond simple conversation summarization to granular, tool-output-level compression for smarter token management.
- **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237) — [Bug]: Response truncated due to output length limit** (41 comments, now closed): The most discussed issue reveals a critical barrier for long-form content generation across gateways. The extended conversation around this fix underscores its importance to the user base.
- **[#41222](https://github.com/NousResearch/hermes-agent/issues/41222) — Integrate Kanban Board into Desktop App**: Users want to reduce context switching between the CLI Kanban tool and the desktop interface.
- **[#44140](https://github.com/NousResearch/hermes-agent/issues/44140) — Desktop GUI: auto-scroll, sidebar overlap fix**: Core UX polish remains a hot topic, with demands for basic streaming and layout improvements.
- **[#45275](https://github.com/NousResearch/hermes-agent/issues/45275) — Unified session history across Desktop and Telegram**: Reflects a strong desire for Hermes to function as a true cross-platform, unified personal AI.

---

### 5. Bugs & Stability
A wave of P2 (High) severity bugs was reported today, with several seeing immediate fix PRs:
- **P2 — Gateway/Provider**: [#45323](https://github.com/NousResearch/hermes-agent/issues/45323) (Telegram rich tables rewritten into bullets); [#45250](https://github.com/NousResearch/hermes-agent/issues/45250) (Anthropic OAuth login broken, blocking Claude Pro subscribers).
- **P2 — Chat Flooding / Agent**: [#45352](https://github.com/NousResearch/hermes-agent/issues/45352) (notify_on_complete pushes ALL process exits to conversation, including failed/killed). **Fix PRs in review**: [#45357](https://github.com/NousResearch/hermes-agent/pull/45357), [#45359](https://github.com/NousResearch/hermes-agent/pull/45359), [#45366](https://github.com/NousResearch/hermes-agent/pull/45366).
- **P2 — CLI/Cron & Configuration**: [#45335](https://github.com/NousResearch/hermes-agent/issues/45335) (`--profile` flag ignored by cron edit). **Fix PR**: [#45350](https://github.com/NousResearch/hermes-agent/pull/45350). [#45129](https://github.com/NousResearch/hermes-agent/issues/45129) (`docker_extra_args` silently ignored by gateway).
- **P2 — Core Tools**: [#44763](https://github.com/NousResearch/hermes-agent/issues/44763) (macOS `computer_use` element bounds always zero, breaking spatial grounding).
- **P3 — Desktop/Install**: [#45264](https://github.com/NousResearch/hermes-agent/issues/45264) (macOS fullscreen sidebar displacement); [#45279](https://github.com/NousResearch/hermes-agent/issues/45279) (node shims shadowing Homebrew); [#45226](https://github.com/NousResearch/hermes-agent/issues/45226) (Windows GPU crash on Desktop launch).

---

### 6. Feature Requests & Roadmap Signals
- **Intelligent Memory Management**: The strong reaction to [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) shows users are hitting context limits and want compression that operates at the tool level, not just the conversation level.
- **Desktop Maturation**: Requests for Kanban integration ([#41222](https://github.com/NousResearch/hermes-agent/issues/41222)), unified session history ([#45275](https://github.com/NousResearch/hermes-agent/issues/45275)), and i18n (PR [#45348](https://github.com/NousResearch/hermes-agent/pull/45348)) strongly indicate the Desktop app is being targeted as the primary user interface.
- **Multi-Profile Synergy**: The push for `--profile` flags on cron commands ([#45350](https://github.com/NousResearch/hermes-agent/issues/45350)) and the YAML+Git `plur` memory provider ([#45331](https://github.com/NousResearch/hermes-agent/issues/45331)) suggest a growing demand for managing multiple profiles and devices simultaneously.
- **Prediction for Next Version**: The upcoming release will likely bundle the `notify_on_complete` fix, the Desktop UI polish patches (auto-scroll, sidebar), the new French locale, official `--profile` support for cron, and potentially the initial framework for headroom-ai integration.

---

### 7. User Feedback Summary
- **Pain Points**: Silent configuration failures (Docker args ignored, endpoint overrides broken) and provider authentication friction (Anthropic OAuth 404) are the dominant sources of user dissatisfaction. Token limit truncation during long outputs remains a critical barrier for power users.
- **Use Cases**: Users are heavily leveraging the agent for multi-platform communication (WhatsApp, Telegram, WeChat/WeCom) and complex agentic workflows involving MCP tools and background processes. The proposal for a YAML+Git memory provider ([#45331](https://github.com/NousResearch/hermes-agent/issues/45331)) specifically targets developers running Hermes as a core daily driver across multiple devices.
- **Satisfaction Indicators**: The rapid creation of overlapping fix PRs for the same bugs (e.g., three PRs for `notify_on_complete`) demonstrates a highly responsive development cycle and a committed maintainer team that fosters strong contributor investment. The highly technical and detailed nature of bug reports reflects a dedicated power-user base.

---

### 8. Backlog Watch
Several critical issues remain open without resolution and require maintainer attention:
- **[#18646](https://github.com/NousResearch/hermes-agent/issues/18646) (P2, May 2)**: WhatsApp `send_message` ignores group targets. A fundamental functional bug for the WhatsApp gateway that has been open for over six weeks.
- **[#17199](https://github.com/NousResearch/hermes-agent/issues/17199) (P2, April 29)**: DeepSeek provider’s aggressive model name normalization breaks compatibility with custom OpenAI-compatible endpoints (e.g., Volcengine ARK). Open for 45 days.
- **[#26264](https://github.com/NousResearch/hermes-agent/issues/26264) (P2, May 15)**: Dashboard “Resume in Chat” fails when served on a non-loopback host. This specific LAN/VPN edge case breaks a core navigation workflow for self-hosted users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for 2026-06-13.

---

## **PicoClaw Project Digest – 2026-06-13**

### **1. Today’s Overview**
The PicoClaw project is in a period of very high velocity, with **6 issues** and **14 pull requests** updated in the last 24 hours, plus an automated nightly release. Development activity is split between significant feature expansion (remote WebSocket mode, DeltaChat gateway, WebSocket lifecycle signals) and a strong push to harden existing code against silent errors in serialization and type assertions. While the Gemini 3.5 Flash incompatibility represents a notable regression, the project is proactively addressing core stability. Community discussion is heavily weighted toward safety and determinism, specifically permission scoping for group channels and explicit agent lifecycle signaling.

### **2. Releases**
- **Nightly Build (v0.2.9-nightly.20260613.c362114c)**: The only release published today is an automated nightly build from `main`. This build aggregates all recent fixes and features but is explicitly marked as potentially unstable. No formal stable release or release candidate was cut.
- **Full Changelog**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **Download**: [Nightly Release](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260613.c362114c)

### **3. Project Progress**
Three pull requests were merged or closed today, primarily focused on reliability and architecture:
- **Architecture Refactoring**: **[PR #2551 (closed)](https://github.com/sipeed/picoclaw/pull/2551)** — "refactor: standardize channel identification and decouple name from provider type". This foundational change allows multiple instances of the same provider, unlocking multi-channel flexibility.
- **Error Handling (Data Loss Prevention)**:
    - **[PR #3112 (merged)](https://github.com/sipeed/picoclaw/pull/3112)** — "fix(tools): handle json.Marshal error in toolloop tool call arguments". Prevents tool call arguments from silently becoming empty strings on marshal failure.
    - **[PR #3113 (merged)](https://github.com/sipeed/picoclaw/pull/3113)** — "fix(channels): check json marshal/unmarshal errors in toChannelHashes". Prevents silent channel identification failures.

### **4. Community Hot Topics**
- **Explicit Turn Completion Signal**: **[Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)** (2 reactions, 2 comments) remains the highest-signal protocol request. External WebSocket clients require a deterministic `turn.done` lifecycle event. This is now directly addressed by **[PR #3116](https://github.com/sipeed/picoclaw/pull/3116)** ("fix(pico): complete `turn.done` lifecycle signaling"), signaling strong maintainer alignment with community needs.
- **Channel-Level Permission Scoping**: **[Issue #3109](https://github.com/sipeed/picoclaw/issues/3109) (EN)** and **[Issue #3114](https://github.com/sipeed/picoclaw/issues/3114) (CN)** represent converging community demand for distinguishing between private chats, groups, and channels for permission control. This reflects a core user anxiety about safely deploying PicoClaw in uncontrolled group environments.

### **5. Bugs & Stability**
- **Critical – Gemini 3.5 Flash Incompatibility**: **[Issue #3111](https://github.com/sipeed/picoclaw/issues/3111)** reports a `400 Bad Request` when executing tools against the new `gemini-3.5-flash` model due to a missing `thought_signature` in the response schema. This blocks a major new provider model. **No fix PR is currently open.**
- **High – Token Consumption Loop**: **[Issue #3012 (stale)](https://github.com/sipeed/picoclaw/issues/3012)** describes continuous token consumption every minute when Evolution is enabled with MiniMax on FreeBSD. This represents a serious potential cost/memory overflow. **No fix PR is open.**
- **Medium – Telegram Forum Topics**: **[Issue #3110](https://github.com/sipeed/picoclaw/issues/3110)** reports that replies in Telegram Supergroup Forum topics incorrectly default to the `#General` thread, breaking a key organizational feature. **No fix PR is open.**
- **Proactive Hardening**: A strong theme today is the merging of error-handling fixes. In addition to the merged PRs above, several open PRs address unchecked type assertions and fallthroughs: **[PR #3053](https://github.com/sipeed/picoclaw/pull/3053)**, **[PR #3045](https://github.com/sipeed/picoclaw/pull/3045)**, and **[PR #3091](https://github.com/sipeed/picoclaw/pull/3091)**.

### **6. Feature Requests & Roadmap Signals**
- **Protocol & Lifecycle**:
    - **Remote Agent Mode**: **[PR #3118](https://github.com/sipeed/picoclaw/pull/3118)** adds a `--remote ws://...` flag to `picoclaw agent`, enabling headless/remote agent operation. This is a strong signal for a decoupled agent architecture.
    - **Turn.done Signal**: **[PR #3116](https://github.com/sipeed/picoclaw/pull/3116)** is a strong candidate for the next stable release, fulfilling the community's top protocol request.
- **Safety & Security**:
    - **Permission Scoping**: The momentum behind **[Issues #3109/#3114](https://github.com/sipeed/picoclaw/issues/3109)** makes this the most likely headline feature for the next minor version (v0.3.0). The bilingual demand suggests it is a critical blocker for broader Telegram/group adoption.
- **Channel Expansion**:
    - **DeltaChat**: **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063)** (feat: add deltachat gateway) is open, adding federated communication protocol support.
- **UX**:
    - **[PR #3097](https://github.com/sipeed/picoclaw/pull/3097)** adds a persistent Shift+Enter hint below the Web chat composer, a small but highly visible UX refinement.

### **7. User Feedback Summary**
- **Pain Points**:
    - **Safety Concerns**: Users are explicitly worried about deploying PicoClaw in Telegram groups and channels, fearing abuse of `exec`/`write_file` by non-admin members. The lack of context-specific permissions is a significant barrier to adoption in team/community settings.
    - **Fragility with New Models**: The Gemini 3.5 Flash regression highlights a lack of backward compatibility with new model requirements, eroding trust in model-switching stability.
    - **Platform Friction**: The Telegram Forum topic bug creates a specific, frustrating failure for power users organizing conversations.
- **Satisfaction**:
    - The community is technically sophisticated and highly engaged, providing detailed root cause analysis and bug reports.
    - Users are actively contributing features (DeltaChat, shift-enter hint), indicating strong buy-in to the platform's direction.

### **8. Backlog Watch**
The following items require maintainer attention due to their age, impact, or stalled state:
- **[Issue #3012](https://github.com/sipeed/picoclaw/issues/3012) [BUG] Continuous token consumption with Evolution** (Created: 2026-06-05, Stale). High potential cost impact. Needs triage or prioritization of a fix.
- **[PR #2964](https://github.com/sipeed/picoclaw/pull/2964) [Feature] Image input compression** (Open: 2026-05-28, Stale). A significant performance and cost optimization stalled without review/rebase.
- **[PR #2917](https://github.com/sipeed/picoclaw/pull/2917) [Feature] NEAR AI Cloud provider** (Open: 2026-05-21, Stale). Adding a major new provider (TEE-capable) is stuck in review limbo.
- **[PR #3045](https://github.com/sipeed/picoclaw/pull/3045) [Bug] Matrix user ID parsing failure** (Open: 2026-06-07). Fixes a critical identity parsing bug for Matrix users (`@user:domain.com`). Should be prioritized for the Matrix adapter to function correctly.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-06-13

## 1. Today's Overview

Development velocity is high. **18 pull requests** were updated in the last 24 hours, with **10 reaching a merged or closed state** and **8 active PRs** advancing. No release was tagged today, but the volume of merged work—spanning critical crash-loop fixes, Signal channel feature-completeness, backup infrastructure, and API resilience—strongly suggests an imminent point release. The community is actively contributing security hardening patches and complex database recovery fixes, signaling a healthy, technically engaged base. Overall, project health is robust, transitioning from core feature delivery into a phase of hardening, reliability engineering, and platform abstraction.

## 2. Releases

No new releases in the reporting period.

## 3. Project Progress (Merged/Closed PRs Today)

**10 PRs were merged, marking significant milestones for stability and channel parity:**

- **Signal Channel Maturation:** Four PRs—[#2040](https://github.com/nanocoai/nanoclaw/pull/2040), [#2070](https://github.com/nanocoai/nanoclaw/pull/2070), [#2071](https://github.com/nanocoai/nanoclaw/pull/2071), and [#2203](https://github.com/nanocoai/nanoclaw/pull/2203)—deliver outbound attachments, host-path inbox routing, and full bidirectional reaction support. Signal is now a first-class channel alongside Telegram and Discord.

- **Ollama Multimodal:** [#2072](https://github.com/nanocoai/nanoclaw/pull/2072) adds an `images` field to `ollama_generate` enabling vision capability via workspace-relative file paths.

- **Backup & Disaster Recovery:** [#2084](https://github.com/nanocoai/nanoclaw/pull/2084) introduces a daily snapshot system with local and optional S3 backends plus a CLI for full or per-agent restore, filling a critical production-readiness gap.

- **Session Crash-Loop Self-Healing:** [#2670](https://github.com/nanocoai/nanoclaw/pull/2670) (fixes [#2669](https://github.com/nanocoai/nanoclaw/issues/2669)) resolves a catastrophic infinite-loop where corrupt `thinking`/`redacted_thinking` blocks in resumed transcripts blocked session recovery. The system now self-heals instead of crashing.

- **Routing & Session Fixes:**
  - [#2267](https://github.com/nanocoai/nanoclaw/pull/2267) fixes agent-to-agent reply routing to the originating session, preventing split-brain conversations.
  - [#2277](https://github.com/nanocoai/nanoclaw/pull/2277) prevents frozen routing context on follow-up messages that caused null-routed cron tasks to misdirect real user messages.
  - [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) retries transient 5xx API errors (e.g., 529 Overloaded) and notifies users on exhaustion instead of silently dropping the turn.

## 4. Community Hot Topics

**Most Active Issues (by engagement and severity):**
- **[#2506](https://github.com/nanocoai/nanoclaw/issues/2506)** — `send_message` dedup silently drops responses when turns complete within 60 seconds. *3 comments. Underlying need:* Reliable concurrent message handling with no silent data loss.
- **[#2632](https://github.com/nanocoai/nanoclaw/issues/2632)** — User asking for clarity on Telegram swarm migration from v1 to v2. *Underlying need:* Clear, supported migration documentation between major versions.
- **[#2711](https://github.com/nanocoai/nanoclaw/issues/2711)** — `create_agent` MCP tool documented as admin-only but exposed to all containers. *Underlying need:* Trustworthy security boundaries and proper role-based access controls.
- **[#2668](https://github.com/nanocoai/nanoclaw/issues/2668)** — A single hung MCP tool blocks the session for up to 30 minutes with no per-tool timeout. *Underlying need:* Predictable, bounded tool execution and session availability.

**Notable Community PR Contributions:**
- **Security hardening:** [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) (cap-drop, no-new-privileges, pids-limit) and [#2749](https://github.com/nanocoai/nanoclaw/pull/2749) (npm package age gating) by `boazdori`.
- **Database recovery:** [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) by `sturdy4days` targets stale `outbound.db` journals, addressing two long-standing community-reproduced bugs ([#2516](https://github.com/nanocoai/nanoclaw/issues/2516), [#2640](https://github.com/nanocoai/nanoclaw/issues/2640)).
- **Discord attachments:** [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) by `jsigwart` fixes inbound Discord attachments (pasted text, images) never reaching the agent.

## 5. Bugs & Stability

**Active Bugs Ranked by Severity:**

| Severity | Issue | Synopsis | Fix Status |
|---|---|---|---|
| **Critical** | [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) | Silent response dropping under concurrent turn completion within 60s; no user feedback | Open, no fix PR |
| **High** | [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) | No per-MCP-tool timeout; a hung tool blocks session up to 30 min | Open, no fix PR |
| **High** | [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) | `create_agent` MCP tool is ungated despite "admin-only" documentation | Open, no fix PR |
| **Medium** | [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) | Budget-exhausted LLM turns silently dropped; user gets no reply | **Closed** today |

**Bugs Fixed Today:**
- [#2670](https://github.com/nanocoai/nanoclaw/pull/2670) — Poisoned-resume crash loop (infinite restart) **merged**.
- [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) — Transient 5xx API errors treated as terminal **merged**.

**Bugs with Open Fix PRs:**
- [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) — Stale `outbound.db` journals after container SIGKILL.
- [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord attachments not reaching the agent.

## 6. Feature Requests & Roadmap Signals

**Near-Term (open PRs likely to merge quickly):**
- **Platform Security Hardening:** Container isolation defaults (`--cap-drop=ALL`, `no-new-privileges`, pids-limit) via [#2748](https://github.com/nanocoai/nanoclaw/pull/2748), and npm package release-age gating via [#2749](https://github.com/nanocoai/nanoclaw/pull/2749). These represent a strong shift toward production security posture.
- **Data Integrity:** The `outbound.db` journal recovery fix ([#2750](https://github.com/nanocoai/nanoclaw/pull/2750)) addresses a core stability concern.
- **Channel Parity:** Discord attachment fix ([#2752](https://github.com/nanocoai/nanoclaw/pull/2752)).

**Medium-Term Roadmap Signals:**
- **Provider Abstraction Layer:** PR [#2746](https://github.com/nanocoai/nanoclaw/pull/2746) ("agent-surfaces capability seam") introduces a formalized host-side registry where providers declare capabilities. This suggests a decoupling from specific backends toward a plugin architecture.
- **Persistent Memory Scaffold:** PR [#2745](https://github.com/nanocoai/nanoclaw/pull/2745) adds an opt-in memory scaffold as a provider capability, pointing toward stateful, context-retaining agents.
- **OneCLI Enterprise Integration:** PR [#2747](https://github.com/nanocoai/nanoclaw/pull/2747) (SDK 2.2.1 bump, credential-stub mounts, machine-checkable pins) signals deeper cloud platform integration for enterprise secrets management.

**Prediction:** The next minor release will likely combine today's merged fixes with the open hardening PRs. The provider capability seam and memory scaffold are likely to land in a v2.1 or v3.0 cycle.

## 7. User Feedback Summary

**Common Pain Points:**
- **Silent Failures:** Repeated user frustration with responses being silently dropped—whether by dedup logic ([#2506](https://github.com/nanocoai/nanoclaw/issues/2506)), budget limits ([#2751](https://github.com/nanocoai/nanoclaw/issues/2751)), or API error exhaustion. The fix to [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) (retry + notify) directly addresses this pattern.
- **Migration Clarity:** Users running custom forks on v1 are uncertain about the v2 migration path, specifically around Telegram swarm features ([#2632](https://github.com/nanocoai/nanoclaw/issues/2632)).
- **Security Confidence:** The unauthenticated `create_agent` finding ([#2711](https://github.com/nanocoai/nanoclaw/issues/2711)) and general container security concerns are prompting community contributions for hardening.
- **Integration Reliability:** MCP tool timeouts ([#2668](https://github.com/nanocoai/nanoclaw/issues/2668)) and channel-specific attachment bugs (Discord [#2752](https://github.com/nanocoai/nanoclaw/pull/2752)) show the cost of supporting multiple provider backends.

**Satisfaction Signals:**
- The high quality of community-submitted bug reports and PRs indicates a technically sophisticated, invested user base.
- Users are not just reporting issues but actively submitting patches (database recovery, security hardening, Discord fixes).
- The maintainers demonstrated responsiveness today by closing and merging 10 PRs in a single batch.

## 8. Backlog Watch

The following issues are open, important, and have not received a maintainer response or fix PR:

| Issue | Created | Days Open | Priority | Status |
|---|---|---|---|---|
| [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) | 2026-05-16 | 28 days | Critical (silent data loss) | **No response or fix PR** |
| [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) | 2026-06-01 | 12 days | High (30-min session block) | **No response or fix PR** |
| [#2632](https://github.com/nanocoai/nanoclaw/issues/2632) | 2026-05-28 | 16 days | Medium (user blocked on migration) | **No response or fix PR** |
| [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) | 2026-06-07 | 6 days | High (security/authorization gap) | **Reported, no fix PR** |

Also watch: PR [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) (fixing [#2516](https://github.com/nanocoai/nanoclaw/issues/2516) and [#2640](https://github.com/nanocoai/nanoclaw/issues/2640)) has been open for 1 day and addresses two unreported or long-standing database races—maintainer review is warranted given the severity of the underlying issues.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-13

## 1. Today's Overview
Activity on the NullClaw project is moderate and concentrated on maintenance and stabilization. Three open pull requests, all by contributor `vernonstinebaker`, are advancing configuration flexibility, error handling, and Discord platform reliability. A new high-severity bug was reported concerning incomplete responses from locally hosted Ollama models. No new releases or merges occurred in the last 24 hours, suggesting the project is currently in a review cycle for these pending changes.

## 2. Releases
No new releases were published today. The project has no recent releases listed in the provided data.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The current development frontier is represented entirely by open PRs:
- **PR #949** (queue_mode configuration)
- **PR #951** (agent runner stderr suppression)
- **PR #953** (Discord gateway recovery)

All items remain open pending review or further testing.

## 4. Community Hot Topics
The project's immediate activity is concentrated on three infrastructure-focused PRs and one user-raised bug report:
- **[PR #949](https://github.com/nullclaw/nullclaw/pull/949)** — Exposes `agent.default_queue_mode` in `config.json`, moving the `QueueMode` enum to a centralized `config_types.zig`. This addresses a clear need for persistent configuration control.
- **[PR #953](https://github.com/nullclaw/nullclaw/pull/953)** — Fixes a critical stability issue where the Discord gateway socket could stall or fail to reconnect, adding regression coverage for pre-HELLO stalls.
- **[PR #951](https://github.com/nullclaw/nullclaw/pull/951)** — Suppresses noisy initialization error logs from appearing in user-facing channels when an agent child process fails.
- **[Issue #952](https://github.com/nullclaw/nullclaw/issues/952)** — A user report of incomplete answers from local Ollama models is the only open bug and represents the most direct community interaction outside of the developer PRs.

## 5. Bugs & Stability
- **Severity: High — [Issue #952](https://github.com/nullclaw/nullclaw/issues/952)**: A user reports truncated responses when using local models (Gemma via Ollama). The description and attached screenshot suggest a potential flaw in the agent's response streaming or parsing logic for local providers. No fix PR currently exists for this issue.
- **Stability Fixes (Open PRs)**: **[PR #953](https://github.com/nullclaw/nullclaw/pull/953)** directly resolves a crash/deadlock scenario in the Discord gateway by ensuring proper socket cleanup and heartbeat thread joining during reconnection. **[PR #951](https://github.com/nullclaw/nullclaw/pull/951)** improves user-facing stability by suppressing irrelevant initialization logs on agent failure.

## 6. Feature Requests & Roadmap Signals
The clearest roadmap signal comes from **[PR #949](https://github.com/nullclaw/nullclaw/pull/949)**, which makes `queue_mode` configurable from `config.json`. This indicates an architectural emphasis on:
- **Persistent configuration**: Moving beyond ephemeral per-session settings toward a file-based, user-controlled setup.
- **Modularization**: The refactoring of the `QueueMode` enum into `config_types.zig` suggests ongoing work to separate and clean up configuration types, a prerequisite for more complex user-facing settings.

If this pattern continues, the next minor release is likely to include deeper `config.json` integration for agent behaviors.

## 7. User Feedback Summary
The project benefits from a small but engaged contributor base.
- **Pain Points**: The most significant user pain point is the local model bug in **[Issue #952](https://github.com/nullclaw/nullclaw/issues/952)**. Running private/local models is a core value proposition for an open-source agent, and the completeness bug creates a functional barrier. The user provided detailed reproduction steps and a screenshot.
- **Contributor Sentiment**: The three PRs by `vernonstinebaker` reflect a developer-user actively fixing friction points around platform stability (Discord), error verbosity, and configuration.
- **Overall Sentiment**: The project feels actively maintained and responsive, though the high-severity local model bug risks eroding confidence in local inference use cases if not addressed quickly.

## 8. Backlog Watch
The provided data covers only items updated in the last 24 hours, limiting visibility into a broader backlog.
- **Items Awaiting Review**: PRs [#949](https://github.com/nullclaw/nullclaw/pull/949) and [#951](https://github.com/nullclaw/nullclaw/pull/951) have been open since June 10th (3 days), while [#953](https://github.com/nullclaw/nullclaw/pull/953) is fresh from June 12th. Timely review from maintainers is needed to sustain contributor momentum.
- **Neglected Bug**: **[Issue #952](https://github.com/nullclaw/nullclaw/issues/952)** (high severity) currently has no comments, labels, or assignees. It requires immediate triage to prevent user churn in the local model community.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-06-13.

---

## IronClaw Project Digest — 2026-06-13

### 1. Today's Overview
The project is in an extremely high-activity cycle, with 50 Issues and 50 PRs updated in the last 24 hours. Effort is overwhelmingly concentrated on the **"Reborn" agent runtime** and its corresponding WebUI v2. The team closed a major block of UX bugs while simultaneously iterating on core architectural decisions regarding thread blocking and approval persistence. A CI-wide failure caused by `cargo-deny` is currently blocking merges on `main` and every open PR. Overall, the project is moving rapidly but faces infrastructure pressure as features mature.

### 2. Releases
*No new versions were released today.*

### 3. Project Progress
The following features and fixes advanced to merged or closed status today:

- **Thread Blocking UX (DeferredBusy):** The automated drain mechanic (PR #4812) landed previously, and its follow-ups for batching, indexing, and routing (#4831, #4832, #4833) were closed out. However, engineering review concluded that a silent automated drain was the wrong UX, leading to the immediate opening of a replacement contract (PR #4838).
- **Reborn WebUI V2 QA:** A massive bug-fix push closed over a dozen issues filed by tester `sunglow666`, including fixes for the model picker saving display names (#4703), broken SSO flows (#4705), link navigation hijacking (#4733), missing user/assistant identity (#4722), improper sidebar pinning (#4721), conversation flickering (#4719), composer interactivity during "Working" state (#4725), persistent attachment warnings (#4720), lost unsent drafts (#4724), unrecoverable sign-in defeats (#4706), and unreachable provider configuration (#4673).
- **Approvals:** Issue #4825 was raised to fix "Always Allow" approvals not surviving thread boundaries. A fix PR (#4835) was opened on the same day.
- **Security & Hooks:** Core infrastructure PRs were merged to record security audit events for auth-continuation failures (#4562) and to enforce caps on capability dispatch fan-out (#4568) and tenant predicate keys (#4569).
- **Observability & Testing:** PR #4773 introduced a record/replay mechanism to pin agent behavior for QA phrases in CI.

### 4. Community Hot Topics
- **Persistent "Always Allow" Approvals (#4825 | PR #4835):** The issue of durable approvals generated significant discussion. Users expect a single “always allow” decision to apply across all threads for the same agent. The solution—dropping `thread_id` from the persistent approval scope—is already in PR and signals a strong commitment to user trust.
- **DeferredBusy Drain vs. Explicit Feedback (#4817, #4812, #4838):** This architectural arc drew the highest conceptual engagement. The team swiftly pivoted from an automated background drain (which silently processes parked messages) to a hard rejection with explicit feedback (PR #4838). The underlying need is **user agency**: the team concluded that silently retrying is less desirable than telling the user "the thread is busy, try again later."
- **Attachment Track (#4644):** The massive multi-PR effort to bring file uploads to Reborn remains the largest ongoing feature set. PRs #4654, #4655, #4668, #4670, and #4738 (Web UX) all remain active. This is the clearest signal of the next major capability landing in the Reborn interface.

### 5. Bugs & Stability
- **[CRITICAL] CI Blocked on `main` (#4824):** The `cargo-deny` job is failing repo-wide due to newly published RUSTSEC advisories against postgres crates (unbounded CPU-exhaustion, panic on malformed data). This is blocking the merge queue for all open PRs and requires immediate maintainer attention.
- **[HIGH] Conversation State Inconsistency (#4762):** A failed tool workflow causes follow-up messages and activity ordering to become inconsistent. The conversation model breaks after an error.
- **[MEDIUM] UI/UX Regressions:** Several open visual and functional bugs from the Reborn QA pass remain unaddressed:
    - Duplicated workspace paths when using relative paths (#4759).
    - No UI feedback when deleting a conversation in the "Running" state (#4823).
    - LLM lacks inherent awareness of current date/time (#4796).
    - Test connection returns false positive for unavailable Ollama instances (#4696).
    - Inconsistent active provider state display (#4697).
    - Hover state and light theme readability issues (#4723, #4819).

### 6. Feature Requests & Roadmap Signals
- **Imminent (In PR):**
    - Full attachment support for Reborn WebChat v2 (PRs #4654, #4655, #4668, #4670, #4738).
    - Explicit gate-open rejection replacing automated thread drain (PR #4838).
    - Slack re-architected as a product adapter extension (PR #4778).
- **Near-term Candidates:**
    - **LLM Context Slice (#4828 / PR #4836):** A new runtime-context block telling the model which channels are connected and where delivery points—addressing a major failure mode for Slack users.
    - **Admin Usage Tracking (#4822):** Engine V2 LLM usage is not yet visible in the admin API, blocking production billing rolls.
    - **CI Performance (#4813):** Splitting slow test jobs into smaller shards.
    - **Code Architecture (#4818):** Decomposing the ~4k line `slack_delivery.rs` file.

### 7. User Feedback Summary
- **Pain Points:**
    - **Reconnect & State Loops:** Slack users consistently hit a reconnect loop where the UI treats Slack as disconnected even after a successful delivery setup (PR #4777). This is the primary driver behind the Slack extension re-architecture (#4778).
    - **Inconsistent Model Behavior:** The LLM’s lack of time awareness (#4796) directly breaks calendar and scheduling workflows. Users also report frustration when tool failures cascade into broken conversation ordering (#4762).
    - **Wasted Efforts:** Losing unsent drafts (#4724) and finding that "Always Allow" approvals do not persist across threads (#4825) erodes trust in the system's reliability.
- **Satisfaction:**
    - The team is scoring highly on **responsiveness**. The majority of UI bugs reported by testers were closed within 24 hours. The rapid reversal from silent drain (#4812) to explicit feedback (#4838) demonstrates a development culture that prioritizes user agency over engineering convenience.

### 8. Backlog Watch
- **PR #3708 (Release chore):** **Open since May 16.** The automated release process is defined but has not been triggered. The accumulation of closed bugs and new features (Slack, Attachments, Hooks) strongly suggests a major version bump is imminent but is likely being blocked by the ongoing feature tracks and the current CI failure.
- **PR #4561 (MCP Security Audit):** **Open since June 8.** This security-critical PR from `zmanian` provides audit trails for MCP direct-lease denials. It has been waiting for review and merge for several days despite a relatively small footprint.
- **Issue #4824 (CI Failure):** While not a "backlog" item in the traditional sense, this active blocker on `main` is the single highest-priority item requiring immediate maintainer intervention, as it halts all other work.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**LobsterAI Project Digest – 2026-06-13**

---

### 1. Today's Overview
LobsterAI is in an intense pre-release sprint, with 17 Pull Requests updated and 11 merged/closed in the last 24 hours. The core event is the merging of the `release/2026.6.11` branch into `main`, bundling major features such as the **Computer Use MVP**, **realtime ASR for cowork inputs**, and expanded **artifact sharing** (HTML public mode, image & SVG support). A significant stack of UX safety fixes from the April backlog (unsaved-change confirmations across Agent and MCP dialogs) was finally cleared, showing strong maintainer focus on data integrity ahead of the next stable tag. Community issue activity was low, with only one historical issue updated.

### 2. Releases
**No new releases were published today.** The merge of the release candidate into `main` ([PR #2158](https://github.com/netease-youdao/LobsterAI/pull/2158)) strongly indicates that an official **2026.6.12** release is being finalized.

### 3. Project Progress
- **Major Feature Bundle:** [PR #2158](https://github.com/netease-youdao/LobsterAI/pull/2158) merges `release/2026.6.11` into `main`, deploying the Computer Use MVP, realtime ASR voice input for cowork prompts, HTML public sharing, and image/SVG artifact sharing.
- **Computer Use Runtime:** [PR #2156](https://github.com/netease-youdao/LobsterAI/pull/2156) bumps the managed runtime to v1.0.7, adding UIA breadcrumbs for diagnosing unexpected helper exits.
- **Media Handling:** [PR #2157](https://github.com/netease-youdao/LobsterAI/pull/2157) fixes a data-integrity bug where AI-generated images were saved with mismatched file extensions (e.g., saving PNG bytes as `.jpg`).
- **Cowork & Model Stability:**
    - [PR #2153](https://github.com/netease-youdao/LobsterAI/pull/2153) resolves model-selection conflicts between same-name package and custom models.
    - [PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154) preserves model metadata for manually stopped streaming replies.
    - [PR #2155](https://github.com/netease-youdao/LobsterAI/pull/2155) prevents duplicate realtime ASR start requests in the voice input flow.
- **UX Safety Sweep (Stale Cleanup):** A batch of five PRs by `MaoQianTu` ( [#1473](https://github.com/netease-youdao/LobsterAI/pull/1473)–[#1477](https://github.com/netease-youdao/LobsterAI/pull/1477) ) were finally merged, adding unsaved-change confirmation dialogs to Agent creation, Agent settings, MCP server config, input draft persistence, and message re-editing.

### 4. Community Hot Topics
- **API Configuration Errors:** Issue [#1](https://github.com/netease-youdao/LobsterAI/issues/1) by `simson2010` (7 comments, closed) remains the most discussed community issue. The user hit a `400 API Error` when using the "OpenAI API" type with a MiniMaxi key. The recent update (2026-06-12) aligns with the model-normalization work in [PR #2153](https://github.com/netease-youdao/LobsterAI/pull/2153), which may have resolved the root cause. This underscores strong user demand for flexible multi-provider support.
- **Stale PR Activity Surge:** The six open PRs from April 3rd (gateway loop, skill injection, i18n, task form, shortcuts) were all batch-updated on June 12th. While they lack public comment threads in this snapshot, the coordinated update signals maintainer triage ahead of the upcoming release.

### 5. Bugs & Stability
- **[High] Fixed – Image Extension Corruption:** [PR #2157](https://github.com/netease-youdao/LobsterAI/pull/2157) fixes a severe bug where generated files (e.g., PNG) were saved with wrong file extensions (`.jpg`, `.jpeg`, `.webp`), causing unopenable or corrupt assets.
- **[Medium] Fixed – Cowork Data Integrity:**
    - **Stream Metadata Loss ([PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154)):** Manually stopping a partial reply previously stripped model metadata.
    - **Duplicated ASR Starts ([PR #2155](https://github.com/netease-youdao/LobsterAI/pull/2155)):** Voice input race condition fixed.
- **[Medium] Fixed – Silent Data Loss (Multiple):** [PRs #1473–1477](https://github.com/netease-youdao/LobsterAI/pulls?q=is%3Apr+author%3AMaoQianTu+is%3Aclosed) close a critical gap where agent configs, MCP settings, and chat drafts were silently discarded when closing dialogs or switching views.
- **[Open – High] Gateway Restart Loop:** [PR #1446](https://github.com/netease-youdao/LobsterAI/pull/1446) addresses the OpenClaw gateway's infinite restart cycle.
- **[Open – High] Disabled Skill Injection:** [PR #1453](https://github.com/netease-youdao/LobsterAI/pull/1453) fixes disabled skills still being injected into conversation prompts.
- **[Open – Medium] Task Form Unresponsive:** [PR #1454](https://github.com/netease-youdao/LobsterAI/pull/1454) resolves the "No Repeat" scheduled task form freezing the "Create Task" button.
- **[Open – Low] Shortcut Conflicts:** [PR #1456](https://github.com/netease-youdao/LobsterAI/pull/1456) adds missing duplicate detection for keyboard shortcuts.

### 6. Feature Requests & Roadmap Signals
- **Computer Use MVP:** Launching Computer Use as a built-in kit signals deep investment in desktop automation and positions LobsterAI ahead of the AI agent "computer use" trend.
- **Voice-First Interaction:** Realtime ASR integration for cowork prompts indicates a roadmap shift toward hands-free, power-user workflows.
- **Content Publishing:** Expanding artifact sharing (HTML, Image, SVG) suggests a goal of making AI outputs directly publishable and shareable.
- **Scheduled Task UX ([PR #1449](https://github.com/netease-youdao/LobsterAI/pull/1449)):** A strong user-facing request to group repeated scheduled-task sessions in the sidebar is pending merge, directly addressing a common complaint about session list clutter.

### 7. User Feedback Summary
- **Data Safety is a Core Pain Point:** The large batch of "unsaved changes" fixes (PRs #1473–1477) strongly implies users were frequently losing unsaved configuration and input content, eroding trust in the UX. The merges today directly address this.
- **Provider Flexibility Demand:** Issue #1 reflects ongoing user desire for looser coupling between the UI and specific API provider types, especially for OpenAI-compatible endpoints.
- **Task Management Friction:** Users are heavily dependent on scheduled tasks, but the form freeze bug (#1454) and verbose session history (#1449) create friction in daily workflows.
- **Silent Failures Erode Trust:** The image format corruption bug (#2157) represents a dangerous silent failure that undermines confidence in file generation outputs.
- **Overall Sentiment:** The development velocity and sweeping cleanup of old PRs indicate a responsive maintainer team and a healthy project trajectory.

### 8. Backlog Watch
The following stale PRs (created April 3rd, updated June 12th) require maintainer attention and appear queued for the next release cycle:

| PR | Area | Severity | Issue |
|---|---|---|---|
| [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) | OpenClaw | **High** | Gateway infinite restart loop |
| [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) | Skills | **High** | Disabled skills still injected into prompts |
| [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448) | i18n | Medium | Agent settings/skill selector showing untranslated English |
| [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) | Tasks | Medium | "Create Task" button unresponsive in non-repeat mode |
| [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) | Cowork | Medium | Requested UX: group scheduled task execution records |
| [#1456](https://github.com/netease-youdao/LobsterAI/pull/1456) | Shortcuts | Low | Missing duplicate keybinding detection |

**Backlog Health:** Positive. The batch-update on June 12th strongly suggests the maintainers have rebased and are actively testing these PRs for inclusion in the upcoming `2026.6.12` stable release.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for 2026-06-13, based on the provided GitHub activity snapshot.

---

## Moltis Project Digest | 2026-06-13

### 1. Today's Overview
Moltis is currently in a quiet phase concerning direct code contribution, with zero pull requests merged or new releases generated in the last 24 hours. Project activity is concentrated entirely in the issue tracker, where three open issues received updates, focusing on feature planning and a specific integration bug. The project maintainers appear to be in a triage and discussion mode, collecting detailed user feedback on proposed major features like Kubernetes sandboxing and new STT backends. Overall project velocity is low on the commit side, but the community signal for future direction remains strong.

### 2. Releases
**None.** No new releases were published in the 24-hour window of this digest. The project remains on its latest stable version from a prior cycle.

### 3. Project Progress
**None.** No pull requests were opened, merged, or closed in the last 24 hours. This indicates a pause in development throughput on the main branch. The lack of recently merged PRs should be monitored in the coming days to confirm whether this is a lull or a slowdown.

### 4. Community Hot Topics
Discussion is split between a specific blocker bug and two high-value feature requests:

*   **[Issue #1115: Fastmail MCP Authorisation Bug](https://github.com/moltis-org/moltis/issues/1115)** — **Most Active (2 Comments)**
    This is the most immediate community friction point. The reporter has identified a specific authorization failure when integrating with Fastmail via MCP. The underlying need here is **reliable external tool connectivity**; users depend on seamless email integration for agent workflows.
*   **[Issue #1118: Kubernetes-native sandbox backend](https://github.com/moltis-org/moltis/issues/1118)** — **Strong Roadmap Signal**
    This request for `runtimeClassName` (Kata Containers/gVisor) indicates a user demand for **enterprise-grade security isolation**. The community is looking to run untrusted LLM-generated code in production environments with strong VM-level guarantees.
*   **[Issue #1102: FunASR/SenseVoice local STT engine](https://github.com/moltis-org/moltis/issues/1102)** — **Long-standing Request**
    A detailed proposal to add a faster, native streaming STT backend. The underlying driver is a desire for **low-latency and privacy-preserving voice interfaces**, bypassing cloud dependencies.

### 5. Bugs & Stability
*   **Severity: High (Integration Blocker)**
    *   **[Issue #1115: Fastmail MCP Authorisation](https://github.com/moltis-org/moltis/issues/1115)** — Reported by kmath313. This bug blocks the Fastmail integration path entirely. The authorization flow appears to have a regression or misconfiguration specific to Fastmail. No fix pull request has been linked to this issue yet. Users relying on the Fastmail MCP server should monitor this issue for workarounds.

### 6. Feature Requests & Roadmap Signals
The issue tracker reveals a clear divergence in complexity for upcoming features:

*   **High Probability (Near-term):** **Local STT Engine ([Issue #1102](https://github.com/moltis-org/moltis/issues/1102)).** Adding FunASR/SenseVoice is a backend integration task that does not require changes to the core agent architecture. It directly improves the voice assistant experience and is the most likely candidate for a minor release (e.g., v0.1.x).
*   **Low Probability / Major Release (Long-term):** **Kubernetes Sandbox ([Issue #1118](https://github.com/moltis-org/moltis/issues/1118)).** This is a significant architectural undertaking requiring a new execution backend, lifecycle management, and OCI runtime configuration. This is likely destined for a v0.2.0 milestone or later.

### 7. User Feedback Summary
*   **Pain Points:** **Integration friction is the primary pain point.** The Fastmail bug ([Issue #1115](https://github.com/moltis-org/moltis/issues/1115)) represents a concrete barrier to daily workflows.
*   **Use Cases:** Users are clearly leveraging Moltis for **voice interaction** (STT request) and **safe code execution** (Kubernetes request). The requests are not trivial; they indicate users are moving beyond simple demos into production or heavy personal use.
*   **Satisfaction:** The community is proactive and technically literate, offering well-specified feature proposals. However, the lack of a closed feedback loop on the Fastmail bug and the older STT request ([Issue #1102](https://github.com/moltis-org/moltis/issues/1102)) may create mild dissatisfaction until maintainers provide resolution timelines or workarounds.

### 8. Backlog Watch
*   **[Issue #1102: FunASR/SenseVoice STT Engine](https://github.com/moltis-org/moltis/issues/1102)** — **Needs Maintainer Attention.**
    Opened over a week ago (June 4) with a clear technical explanation and specific user need. While it received an update on June 12 (likely a user comment), there is no evidence of a maintainer response or roadmap assignment. This is the highest priority item for the maintainers to address to confirm the viability of the request or explain why it conflicts with the current architecture. A simple "we are looking into it" would satisfy the backlog.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# QwenPaw (CoPaw) Project Digest | June 13, 2026

## 1. Today's Overview
The project saw exceptionally high activity with **21 issues** and **23 pull requests** updated in the past 24 hours. The development team closed **10 PRs** and resolved **7 issues**, demonstrating strong responsiveness. Activity is split between stabilizing the `v1.1.11` series—where several regressions were filed and promptly patched—and making progress on major architectural upgrades, including a modular **Runtime 2.0** execution engine and the planned migration to **AgentScope 2.0**. The community remains technically engaged, actively bisecting regressions and submitting detailed feature proposals.

## 2. Releases
**No new releases were published today.** However, two version-bump PRs were closed, indicating an imminent **v1.1.12 beta** release:
- [#5157](https://github.com/agentscope-ai/QwenPaw/pull/5157): Bump to `1.1.12.beta1`
- [#5159](https://github.com/agentscope-ai/QwenPaw/pull/5159): Reformat version to `1.1.12b1`

## 3. Project Progress
Key pull requests merged or closed today:

**Architecture & Infrastructure**
- [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) — **Runtime 2.0**: A major refactor replacing the monolithic `Runner` with composable, testable units and introducing a `ToolCoordinator` layer for granular tool-call lifecycle control.
- [#5121](https://github.com/agentscope-ai/QwenPaw/pull/5121) — **Release Verification Gate**: Automated installation, boot, and health-check validation before publishing to PyPI/DockerHub.
- [#5022](https://github.com/agentscope-ai/QwenPaw/pull/5022) — **Workspace Security**: Shared validation preventing agent workspaces from being placed inside QwenPaw-managed directories.

**Console / UI Fixes**
- [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) — Fixed long-standing memory configuration loss by forcing render of Collapse panels.
- [#5147](https://github.com/agentscope-ai/QwenPaw/pull/5147) — Fixed session loss when refreshing the Coding Mode page.
- [#5154](https://github.com/agentscope-ai/QwenPaw/pull/5154) — Refactored memory search tool result rendering to display correctly.
- [#4144](https://github.com/agentscope-ai/QwenPaw/pull/4144) — Fixed desktop readiness check when bound to wildcard address `0.0.0.0`.

## 4. Community Hot Topics
The following issues and PRs generated the most discussion and reactions:

- [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) (11 comments) — **Bug**: Agent-generated scheduled tasks fail to trigger. This is a core functionality issue blocking autonomous agent workflows.
- [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) (10 comments, 2 upvotes) — **Breaking Change**: Migration of backend from AgentScope 1.x to AgentScope 2.0. Users are actively asking for timelines and details.
- [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) (6 comments) — **Bug**: Non-plain-text file downloads (docx/pdf) return 404 error in `v1.1.11.post2`.
- [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) (3 comments) — **Feature Request**: Whitelist `kimi-for-coding` in the UV allowlist to allow Kimi subscribers to use their API.
- [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) (3 comments) — **Feature Request**: Native multi-agent team/swarm collaboration capability.

## 5. Bugs & Stability
The `v1.1.11` series encountered several regressions, though most are being addressed promptly.

**Critical / High Severity (Open)**
- [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) — **Gemini Regression**: Tool calling confirmed broken in `v1.1.11.post2` but working in `v1.1.10`.
- [#5155](https://github.com/agentscope-ai/QwenPaw/issues/5155) — **Docker Stability**: The `v1.1.11` Docker image experiences spontaneous crashes and restarts.
- [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) — **Long Context Hang**: QwenPaw stops responding as conversation history grows.
- [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) — **Infinite Loop**: The dialogue thinking logic enters a non-terminating loop.
- [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) — **Scheduled Tasks**: Agent-generated timed tasks never execute on schedule.

**Moderate Severity (Open)**
- [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) — Python 3.13 compatibility (`imghdr` module removed from stdlib).
- [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165) — PyInstaller packaging script broken, leading to white screen on launch.
- [#5145](https://github.com/agentscope-ai/QwenPaw/issues/5145) — Execution details always expanded, distracting from real outputs.

**Resolved Today**
- [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) — Attachment download 404
- [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) — Memory search / vector config loss
- [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) — Memory search tool results UI broken
- [#5142](https://github.com/agentscope-ai/QwenPaw/issues/5142) — Coding Mode session loss on refresh
- [#5143](https://github.com/agentscope-ai/QwenPaw/issues/5143) / [#5148](https://github.com/agentscope-ai/QwenPaw/issues/5148) — Math formula square-root rendering

## 6. Feature Requests & Roadmap Signals

**Confirmed Near-Term**
- **v1.1.12 Beta**: Version bump PRs merged; patch release is imminent.
- **Runtime 2.0** ([#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078)): Modular execution engine with `ToolCoordinator`.
- **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)): Planning phase underway.
- **Agent OS Driver** ([#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067)): Unified abstraction for MCP, A2A, ACP protocols.

**High Community Demand (Open/Under Discussion)**
- **Slack Channel Support** ([#5152](https://github.com/agentscope-ai/QwenPaw/issues/5152))
- **Agent Team / Swarm Collaboration** ([#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139))
- **Kimi for Coding Integration** ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156))
- **Desktop System Tray & Background Service** ([#5164](https://github.com/agentscope-ai/QwenPaw/issues/5164))
- **Feishu CardKit Streaming Performance** ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167))

**In-Review Enhancements**
- Visual model fallback for text-only models ([#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069))
- Per-turn token usage popover ([#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130))
- User input queue for console chat ([#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158))
- DataPaw analytics plugin with 12 BI skills ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622))

## 7. User Feedback Summary
The user community is technically sophisticated, actively deploying the project in Docker and desktop environments and filing high-quality bug reports with version bisections. There is clear satisfaction with the pace of development and the team's responsiveness—many bugs filed one day are fixed the next. However, the frequency of regressions in patch releases (especially `.post` bumps) is a source of frustration. Users are pushing for enterprise-grade features (multi-agent teams, LM provider flexibility, desktop lifecycle management) indicating QwenPaw is increasingly seen as a viable replacement for commercial AI assistant platforms.

## 8. Backlog Watch
Items requiring maintainer attention due to community interest, age, or severity:

- [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) — **Scheduled Task Bug** (11 comments, 6 days open): Core agent autonomy feature is broken; high priority.
- [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) — **AgentScope 2.0 Migration** (10 comments, 17 days open): The most anticipated roadmap item; needs a clear timeline and communication plan to manage community expectations.
- [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) — **DataPaw Plugin** (22 days open): Large first-time contributor PR waiting for review.
- [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) — **Plugin Decoupling** (11 days open): Critical fix for PyInstaller/Tauri desktop environments; plugin system fails to initialize.
- [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) — **Gemini Regression** (1 day, 0 responses): A confirmed downgrade in support for a major model provider requiring immediate triage.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 13, 2026, based on the provided repository data.

---

## ZeroClaw Project Digest — 2026-06-13

### 1. Today’s Overview
ZeroClaw is in a **high-velocity stabilization and integration phase**, with **36 PRs** and **12 issues** updated in the last 24 hours. Activity is heavily weighted toward bug fixes and infrastructure alignment rather than new feature work, suggesting the team is consolidating toward the **v0.8.1** milestone tracked in [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970). Five **S1 (workflow-blocked) bugs** were filed today, covering macOS, Windows, Docker, and the web dashboard, indicating that while the codebase is advancing rapidly, the user onboarding experience is currently fragile. On the positive side, major RFC-driven changes (unified agent turn engines) and deep plugin-system refactors are actively landing.

### 2. Releases
**No new releases** were published today. The current release remains at **v0.8.0**. The community tracker [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) suggests a **v0.8.1** is next, focused on the additive PR queue across channels, providers, and tools.

### 3. Project Progress — Merged/Closed PRs
Four PRs were merged or closed in the last 24 hours. The two explicitly detailed are:

- **[#7447 (closed)](https://github.com/zeroclaw-labs/zeroclaw/pull/7447):** The native OpenAI provider (`OpenAiModelProvider`) now correctly wires the `timeout_secs` config field instead of using a hardcoded 120-second timeout. This is a targeted fix for users running slow local models (llama.cpp, vLLM) that previously saw silent request failures.
- **[#7548 (closed)](https://github.com/zeroclaw-labs/zeroclaw/pull/7548):** A massive **cross-cutting dependency and Cargo.toml cleanup** (labeled affecting core, providers, channels, tools, and CI). This type of maintenance reduces audit noise and stabilizes the build matrix across a very wide surface area.

### 4. Community Hot Topics
The most active technical discussions and contributor magnets this cycle are:

- **RFC: Unify Agent Turn Engines** ([#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)) — The top-commented issue. This RFC proposes merging `run_tool_call_loop`, `turn_streamed`, and `Agent::turn` into a single engine. The author reports it is **being executed as a single consolidation PR** (#7540), making this a top-risk architectural change currently in flight.
- **MCP Tooling Surge** — Two high-interest PRs dominate the MCP track: **auto-reconnect on stale sessions** ([#7351](https://github.com/zeroclaw-labs/zeroclaw/pull/7351)) and **auto-injecting discovered MCP tools into agent risk profiles** ([#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547)). The latter is a direct consequence of flipping `mcp.enabled` to `true` by default in a recent commit, exposing a gap where tools were discovered but never attached to agents.
- **Plugin Path Alignment** ([#7549](https://github.com/zeroclaw-labs/zeroclaw/pull/7549)) — A fix for a silent mismatch where `zeroclaw plugin install` wrote to `data_dir/plugins` while the runtime scanned `config.plugins.plugins_dir`. This is a critical developer-experience fix for the nascent WASM plugin ecosystem.
- **East-Asian IM Channels** ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)) — A feature request for streaming card messages on QQ, DingTalk, WeChat, and Feishu. The request draws 0 comments but signals a **strong and growing Chinese-language user base** demanding rich, low-latency messaging.

### 5. Bugs & Stability
Five **S1 (workflow-blocked)** bugs were reported today, making stability the dominant narrative.

| Severity | Issue | Component | Status / Fix |
|---|---|---|---|
| **S1** | [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | quickstart (Windows 10) | New user blocked by TOML parsing error. **No fix PR yet.** |
| **S1** | [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | runtime/daemon (macOS 15) | Blank screen, permission detection, window disappearing. **No fix PR yet.** |
| **S1** | [#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) | Docker build | Fails due to missing C++ compiler (cc-rs). **Fixed by [#7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534).** |
| **S1** | [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | Web Dashboard | `cargo web build` not available; misleading startup message. **Fixed by [#7529](https://github.com/zeroclaw-labs/zeroclaw/pull/7529) / [#7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534).** |
| **S1** | [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | Gateway API / `ask_user` | Fails instantly in WS sessions. **Fixed by [#7551](https://github.com/zeroclaw-labs/zeroclaw/pull/7551).** |
| **S2** | [#7541](https://github.com/zeroclaw-labs/zeroclaw/issues/7541) | Gateway / Paths | V3 schema rename leftover: `data_dir` used instead of `workspace_dir`. **No fix PR yet.** |

**Analysis:** The rapid fix of [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) and [#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) **within the same 24-hour window** shows a responsive maintainer team. However, the Windows and macOS S1 blockers ([#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537), [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)) remain unassigned, which is a risk for the v0.8.1 release's accessibility goals.

### 6. Feature Requests & Roadmap Signals
Several submitted features point to where the roadmap is heading next:

- **Multi-Session Web Chat** ([#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543)) — A clean request for session management (new/switch/rename/delete) in the gateway UI. Likely a strong candidate for a fast-follow patch given the UX gap.
- **llama.cpp Model Router** ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)) — Users want the ability to hot-switch local models without restarting the provider. Combined with the timeout fixes in [#7447](https://github.com/zeroclaw-labs/zeroclaw/pull/7447) and [#7504](https://github.com/zeroclaw-labs/zeroclaw/pull/7504), **local/self-hosted model ergonomics** are clearly a top user desire for the next cycle.
- **Streaming Card Messages** ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)) — Reducing latency for rich interactions on Asian IM platforms. High-value for the international community.
- **WASM Plugin Backend (wasmtime)** ([#7429](https://github.com/zeroclaw-labs/zeroclaw/pull/7429)) — This is a high-risk, large PR adding a wasmtime dependency as an alternative to Extism. It is a **strong roadmap signal** for a maturing plugin architecture, even if it remains in review for a while.
- **Unified Turn Engine** ([#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)) — The execution PR (#7540) implies this will land in the very near future, fundamentally changing how agents process streaming vs. blocking turns.

### 7. User Feedback Summary
Real user signals extracted from today's issue/PR data:

- **Accessibility Pain:** New users on macOS ([#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527): “app can't detect granted permissions … empty page”) and Windows ([#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537): “cannot create the agent via zeroclaw quickstart”) are hitting hard walls. This is the most acute dissatisfaction signal today.
- **Developer Experience:** The Docker build ([#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533)) and dashboard build ([#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)) friction frustrates contributors who want to run locally. The fast fixes on these suggest the team prioritizes contributor velocity.
- **MCP Confusion:** The flurry of fixes around MCP tools not appearing in agent tool-lists ([#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547)) indicates that users enabling MCP are finding it doesn't "just work" yet.
- **Satisfaction Signals:** The sheer volume of feature requests (Twitch, llama.cpp, multi-session, streaming cards, MCP auto-reconnect) indicates a **highly engaged user base** that sees ZeroClaw as a platform worth extending and advocating for.

### 8. Backlog Watch
Issues and PRs that require maintainer action or are at risk of stalling:

- **Needs Author Action — [#7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245):** `fix(read_skill)` for plugin-bundled skills. Open since June 5, this PR is blocked because the author has not responded to requests for changes. If it stalls, plugin adoption suffers.
- **Needs Author Action — [#7351](https://github.com/zeroclaw-labs/zeroclaw/pull/7351):** MCP auto-reconnect. Open since June 7. This is a critical quality-of-life fix for MCP reliability, awaiting author revisions.
- **Unassigned S1 Bug — [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527):** The macOS app crash/permissions bug. With no fix PR yet, this is a dangerous blind spot for the v0.8.1 release on a primary consumer platform.
- **Unassigned S1 Bug — [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537):** The Windows quickstart TOML parsing error. Similar to macOS, this blocks a major platform.
- **High Risk — [#7429](https://github.com/zeroclaw-labs/zeroclaw/pull/7429):** The wasmtime PR is a large surface area change. With `risk: high` and `size: L`, it requires careful maintainer bandwidth to review, but the payoff for the plugin system is substantial.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*