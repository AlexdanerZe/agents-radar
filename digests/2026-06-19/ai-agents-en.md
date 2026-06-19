# OpenClaw Ecosystem Digest 2026-06-19

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-19 03:59 UTC

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

# OpenClaw Project Digest — 2026-06-19

## 1. Today's Overview

The OpenClaw project is exhibiting extremely high velocity as of June 19th, 2026. Maintainers and the community updated **500 issues** and **500 pull requests** in the last 24 hours, signaling intense development activity and a highly engaged user base. Of those, **40 issues were closed** and **53 PRs were merged**, while the project continues to manage a substantial backlog of **460 open issues** and **447 open PRs**. No new formal releases were published today; effort remains concentrated on stabilizing the 2026.5.x line with session state hardening, channel reliability (Telegram, Discord, Feishu), and provider fallback robustness.

---

## 2. Releases

**No new releases** were published today. The last tagged version was 2026.5.22. The community is actively testing on that build and reporting regression patterns, particularly around Telegram delivery, subagent isolation, and Codex app-server behavior.

---

## 3. Project Progress

**53 Pull Requests were merged or closed today**, alongside **40 closed issues**. Key merges include:

- **🔀 PR #87333** ([CLOSED](https://github.com/openclaw/openclaw/pull/87333)): Prevents `toolDiscovery` from overwriting the pinned channel registry when `tools.catalog` is called from the frontend — protects channel configurations from accidental reset.
- **🔀 PR #94746** ([CLOSED](https://github.com/openclaw/openclaw/pull/94746)): Fixes cosmetic regression in `openclaw doctor` where `clack` was re-breaking copy-sensitive tokens inside `note()` boxes, preserving file path integrity.
- **🔀 PR #86898** ([CLOSED](https://github.com/openclaw/openclaw/pull/86898)): Resolves a critical livelock in the context engine for Telegram DM sessions where turn-maintenance workers wait indefinitely on an inference lane.
- **🔀 PR #85546** ([CLOSED](https://github.com/openclaw/openclaw/pull/85546)): Adds `/rename` (and `/title`) slash command to Control UI for session labeling from chat input.
- **🔀 PR #87092** ([CLOSED](https://github.com/openclaw/openclaw/pull/87092)): Community contributor recognition update.

**Closed issues of note:**
- **#85888** ([CLOSED](https://github.com/openclaw/openclaw/issues/85888)): MiniMax 503 cron overload during 05:00-07:30 CST — root cause addressed.
- **#94309** ([CLOSED](https://github.com/openclaw/openclaw/issues/94309)): Telegram Desktop not offering Quote & Reply on bot messages — resolved.
- **#83964** ([CLOSED](https://github.com/openclaw/openclaw/issues/83964)): `@openclaw/codex` `ERR_MODULE_NOT_FOUND` on `2026.5.18` — fix shipped.

---

## 4. Community Hot Topics

The most active discussions reflect deep integration challenges and high expectations for reliability:

- **🔥 Session Write-Locks & Delivery Failures** ([#86538](https://github.com/openclaw/openclaw/issues/86538), 11 comments): P1. `session JSONL write-lock timeouts` cascade to block main, cron, and subagent lanes, surfacing as delivery failures without sufficient diagnostic data. Community demanding better "owner diagnostics" rather than trial-and-error debugging.

- **🔥 Telegram Reply Duplication Regression** ([#86519](https://github.com/openclaw/openclaw/issues/86519), 9 comments): P1 regression from 2026.5.20 update. Agents send 2-10x duplicate replies per Telegram message. Reduced but not eliminated in 2026.5.22. Making the bot effectively unusable in group chat scenarios.

- **🔥 Raw Mode Permanently Disabled** ([#59330](https://github.com/openclaw/openclaw/issues/59330), 14 👍): Open since April. Control UI Config editor remains stuck in Form-only mode since 2026.3.31. Power users are displeased — the detailed root cause analysis provided by the reporter points to `normalizeExecSafeBinProfilesInConfig()` injecting undefined keys that break round-trip checks.

- **🔥 MCP Tools Not Injected into Subagents** ([#85030](https://github.com/openclaw/openclaw/issues/85030), 8 comments, 3 👍): P1. MCP tool schemas registered via `mcp.servers` are completely absent from `sessions_spawn` sessions. A critical barrier for complex agentic workflows requiring tool access in subagents.

- **🔥 Model Fallback Chain Failure** ([#85103](https://github.com/openclaw/openclaw/issues/85103), 10 comments): Full provider quota exhaustion on OpenAI Codex fails to trigger any of the configured fallback models (deepseek-v4, kimi-k2.6). System simply fails instead of degrading gracefully.

---

## 5. Bugs & Stability

Stability is the dominant theme. Multiple P1 regressions and a single P0 data-loss bug are active today.

### Critical (P0)
- **🧨 Memory File Deletion** ([#84882](https://github.com/openclaw/openclaw/issues/84882)): `memory-core` Dreaming's `normalized recall artifacts` step silently deletes daily memory files (`memory/YYYY-MM-DD.md`). **Silent data loss bug** — highest severity. Needs immediate triage.

### High Severity (P1 — Open)
- **🧨 Gateway Event Loop Isolation Failure** ([#84903](https://github.com/openclaw/openclaw/issues/84903)): A single stalled agent session (e.g., model call hung on lock contention) blocks the **entire** Gateway event loop. No session isolation — a core architectural regression for multi-agent deployments.
- **🧨 Group Chat Silent Drops** ([#86827](https://github.com/openclaw/openclaw/issues/86827)): After an AI turn fails (timeout), the session enters `failed` state and silently drops all subsequent messages with no user-facing error.
- **🧨 Discord Channel Context Loss** ([#94750](https://github.com/openclaw/openclaw/issues/94750)): Created today. Discord sessions lose recent conversation context after idle/reset, breaking organic continuity — agent cannot pick up where the channel left off.
- **🧨 Codex Silent Truncation** ([#84516](https://github.com/openclaw/openclaw/issues/84516)): Headless `openclaw message` calls truncate output at ~1000 chars with `stopReason=null` and `aborted=false`. Automation workflows receive partial data without error signals.
- **🧨 Preemptive Context Overflow** ([#84536](https://github.com/openclaw/openclaw/issues/84536)): Embedded sessions killed silently when context overflows; user is never notified that the model implicitly dropped their session.
- **🧨 Codex App-Server Goes Silent Mid-Turn** ([#85251](https://github.com/openclaw/openclaw/issues/85251)): Emits `notification:turn/started` then goes completely silent for the full 360s stuck-session recovery window — no deltas, no error, no completion.
- **🧨 Subagent Process Accumulation** ([#86119](https://github.com/openclaw/openclaw/issues/86119)): Orphaned `node server.js` worker processes accumulate after subagent/cron embedded runs, degrading Docker host stability over time.

### Fixes in Progress
- PR #86900 ([link](https://github.com/openclaw/openclaw/pull/86900)): Circuit breaker for compaction to stop token burn when summarizer is unavailable.
- PR #86893 ([link](https://github.com/openclaw/openclaw/pull/86893)): Extends isolated cron cold runner setup timeout for long jobs.
- PR #86764 ([link](https://github.com/openclaw/openclaw/pull/86764)): Persists user turn to transcript before external runner failures to prevent message loss in CLI/ACP sessions.
- PR #94760 ([link](https://github.com/openclaw/openclaw/pull/94760)): Fixes Feishu p2p DM reply routing (`SUBSCRIPTION_NOT_FOUND`).
- PR #94777 ([link](https://github.com/openclaw/openclaw/pull/94777)): Normalizes HTML tables in Telegram rich messages before entity-escaping.

---

## 6. Feature Requests & Roadmap Signals

The community is pushing for platform maturity, extensibility, and security:

- **🧩 Plugin SDK Stabilization** ([#81913](https://github.com/openclaw/openclaw/issues/81913)): Clear demand for a small, intentional public SDK surface for skills introspection, metadata parsing, and path resolution without exposing internal agent APIs. Strong candidate for next minor release.
- **🔒 Filesystem Sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722), 4 👍): Users want first-class `tools.fileAccess` configuration with allow/deny path lists. Stalled on security review and product decision since February.
- **🔁 Webhook Multi-Turn** ([#11665](https://github.com/openclaw/openclaw/issues/11665)): `sessionKey` parameter on `/hooks/agent` is documented but wholly non-functional — `resolveCronSession()` always generates a new session. Core promise unmet.
- **📡 Pre-Routing Inbound Hook** ([#81061](https://github.com/openclaw/openclaw/issues/81061), 3 👍): Architectural enhancement for a `before_route_inbound_message` hook enabling channel bridging/proxying before session assignment.
- **💸 Operational Cost Visibility** (PR #94308, [open](https://github.com/openclaw/openclaw/pull/94308)): Introducing transcript-backed session cost display in `openclaw status` would provide much-needed operational transparency.
- **🏷️ Comms Cleanup** ([#86237](https://github.com/openclaw/openclaw/issues/86237)): Rename the internal "cron" subsystem to disambiguate from system cron — real collisions causing bugs for admins.
- **🤖 Extended Model Support**: Pro-plan path for GPT-5.5-pro/Spark ([#83954](https://github.com/openclaw/openclaw/issues/83954)), Perplexity `search_context_size` parameter exposure (PR #94757, [open](https://github.com/openclaw/openclaw/pull/94757)), and Feishu outbound rate limiting config (PR #94614) signal an expanding provider and channel surface.

---

## 7. User Feedback Summary

**Satisfaction Drivers:**
- Users are deeply integrating OpenClaw into complex, production-level workflows: multi-channel bots (Telegram, Discord, Feishu, WhatsApp), cron-driven memory pipelines, MCP tool orchestration, and subagent spawning.
- Bug report quality is exceptionally high. Users provide full root cause analysis, logs, and reproduction steps (e.g., `#59330`, `#86063`, `#84662`). This indicates a technically sophisticated and invested power-user base.

**Pain Points:**
1. **Channel Reliability Eroding Trust:** Telegram duplicate reply regression (`#86519`), Discord context loss (`#94750`), and WhatsApp session stalling (`#84569`) are making the bot behavior unpredictable on end-user channels. This is the #1 complaint cluster.
2. **Session State Fragility:** Stalled agents blocking the event loop (`#84903`), sessions stuck in `failed` state (`#86827`), and write-lock timeouts (`#86538`) are recurring themes. Simpler, more robust isolation and recovery are desperately needed.
3. **Provider/Observability Gap:** Fallback chains failing silently (`#85103`), Codex replies truncated without error signals (`#84516`), and missing diagnostics on session issues force opaque debugging.
4. **Subagent Toolchain Broken:** MCP tools not injected into subagent sessions (`#85030`) blocks the flagship multi-agent architecture for tool-using workflows.

---

## 8. Backlog Watch

Several important, long-standing issues remain open and require maintainer attention or product decisions:

- **🔴 #11665** ([link](https://github.com/openclaw/openclaw/issues/11665)): **Webhook multi-turn support.** Open since February 8, 2026 (**131 days**). The documented `sessionKey` parameter for `/hooks/agent` is completely non-functional. Blocked on product decision.
- **🔴 #7722** ([link](https://github.com/openclaw/openclaw/issues/7722)): **Filesystem Sandboxing Config.** Open since February 3, 2026 (**136 days**). Highly requested security feature with 4 👍. Stalled on security review and product decision.
- **🔴 #54531** ([link](https://github.com/openclaw/openclaw/issues/54531)): **Force reply to originating channel.** Open since March 25, 2026 (**86 days**). P1 bug affecting Telegram, Discord, and WhatsApp users whose responses never reach their phone. `needs-security-review` label appears to be the blocker.
- **🔴 #81061** ([link](https://github.com/openclaw/openclaw/issues/81061)): **Pre-routing inbound message hook.** Open since May 12, 2026 (**38 days**). Major architectural feature request with community traction (3 👍). Awaiting product decision.

**Observation:** The pattern is clear — architectural and security-forward features are blocking on maintainer decisions. Given the project's impressive velocity on bug squashing, clearing these product/Security Review bottlenecks would unlock significant community potential and reduce bespoke workarounds. The `clawsweeper:needs-product-decision` and `clawsweeper:needs-security-review` labels are becoming critical path blockers for the most willing contributors.

---

## Cross-Ecosystem Comparison

### Cross-Project Ecosystem Analysis: Personal AI Agent Open-Source Landscape

**Date:** June 19, 2026
**Scope:** OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw, NullClaw, IronClaw, LobsterAI, TinyClaw, Moltis, CoPaw, ZeptoClaw, ZeroClaw

---

#### 1. Ecosystem Overview

The personal AI agent open-source landscape is experiencing a period of extremely high-velocity maturation, marked by a collective pivot from experimental chat bots toward production-ready multi-agent orchestration platforms. The ecosystem is heavily fragmented, yet strongly aligned around common pain points: **session state reliability**, **multi-channel delivery guarantees**, and **Model Context Protocol (MCP) integration depth**. The defining tension is between feature velocity (adding desktop apps, computer use, complex automations) and foundational stability (eliminating silent data loss, process freezes, and provider fallback failures). The “Claw” architecture family (OpenClaw, NanoClaw, PicoClaw, ZeroClaw) dominates mindshare, but specialized forks are rapidly innovating in specific verticals like enterprise security (NanoClaw), desktop development workflows (Hermes Agent), and productivity tooling (LobsterAI). The ecosystem benefits from a highly sophisticated power-user base that is willing to contribute fix PRs, detailed root-cause analyses, and ambitious architectural RFCs—raising the stakes for maintainers to match this community rigor with governance and review capacity.

---

#### 2. Activity Comparison

| Project | Issues (24h Δ) | PRs (24h Δ) | Release Status | Health Score (1-10) | Key Observation |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated (40 closed) | 500 updated (53 merged) | None (2026.5.x line) | 6 | Highest raw volume; carries a P0 silent data loss bug despite high fix throughput |
| **NanoBot** | 3 updated | 24 updated (5 merged) | None | 8 | Excellent response time; critical `run()` state mutation bug has same-day fix PR |
| **Hermes Agent** | 50 updated | 50 updated (2 merged) | None | 6 | High engagement and sophisticated orchestration patterns, but heavy triage bottleneck and session data loss |
| **PicoClaw** | N/S | 14 updated (7 merged) | Nightly `v0.3.0-nightly` | 4 | Core UX bug (async subagent duplication) stale for 9 days; dominated by Dependabot |
| **NanoClaw** | 5 updated | 21 updated (6 merged) | None (v2.1.18 tip) | 8 | Focused security hardening sprint; high community PR rigor with regression tests |
| **NullClaw** | 4 updated | 4 opened (0 merged) | None | 7 | Small, healthy; community self-organized to document WeChat and fix streaming |
| **IronClaw** | 31 updated | 43 updated | None (v0.29.1 tip) | 8 | Imminent major feature release (Projects, Automations 2.0); OAuth token expiry is key risk |
| **LobsterAI** | N/S | 15 updated (14 merged) | **v2026.6.18** | 9 | Highest feature delivery density this cycle; shipped Computer Use MVP + artifact sharing overhaul |
| **TinyClaw** | 0 | 0 | None | 1 | Dormant |
| **Moltis** | 1 updated | 0 | None | 2 | Stalled; single open bug on session lifecycle |
| **CoPaw** | 44 updated | 28 updated | **v1.1.12.post1** | 5 | Highest innovation velocity in context management, but critical freeze/data loss bugs undercut stability |
| **ZeptoClaw** | 0 | 0 | None | 1 | Dormant |
| **ZeroClaw** | 50 updated | 50 updated | **v0.8.1** | 9 | Most effective patch cycle (45 contributors); strong governance, P1 provider bug cluster remains |

*N/S = Not strictly specified in the digest summary, though overall issue attention was noted.*

---

#### 3. OpenClaw’s Position

**Advantages vs. Peers:**
- **Scale and Retention**: OpenClaw dwarfs peers in raw engagement (500+ issues and PRs updated daily). This creates a massive community feedback loop, bug surface, and contribution pipeline.
- **Architecture Maturity**: As the canonical reference implementation, OpenClaw has the most mature multi-channel architecture (Telegram, Discord, Feishu, WhatsApp, custom gateways), the deepest MCP tooling pipeline, and the most extensive cron/subagent scheduling framework.
- **Channel Breadth**: No other project in this comparison supports the full suite of production communication backends that OpenClaw does out of the box.

**Technical Approach Differences:**
- Unlike **ZeroClaw** (Rust, high-perf monolithic gateway) or **NanoBot** (lean Node.js core with fast iteration), OpenClaw uses a TypeScript-based modular “chassis” design. This provides maximum extensibility but introduces complexity in session isolation and event loop management, evidenced by the Gateway Event Loop Isolation Failure (#84903).
- Compared to **IronClaw** (Rust/Typescript hybrid with strong SaaS/automation layer), OpenClaw is more general-purpose and community-governed, lacking IronClaw’s structured “Reborn” engine roadmap.

**Community Size Comparison:**
OpenClaw operates in the highest activity tier alongside ZeroClaw and IronClaw. However, its backlog (460 open issues, 447 open PRs) relative to peers suggests a growing **maintenance-debt-to-contributor-bandwidth gap**. Projects like NanoBot and NanoClaw exhibit higher *per-issue* responsiveness (same-day fix PRs), which builds deeper trust in their stability narrative.

---

#### 4. Shared Technical Focus Areas

Several critical pain points are emerging as ecosystem-wide requirements:

| Focus Area | Affected Projects | Community Demand |
|---|---|---|
| **Session State & Context Data Integrity** | OpenClaw (#84882, P0 deletion), NanoBot (#4307, wipe on consolidation), Hermes (#48519, data loss), CoPaw (#5171, zero context), ZeroClaw (#7847, race condition) | **Highest priority.** Users will not adopt advanced features if the context layer is untrusted. |
| **Multi-Agent/Sub-Agent Reliability** | OpenClaw (#84903, isolation), PicoClaw (#3094, duplication), NanoClaw (#2807, privilege escalation), NullClaw (#190, architecture) | Demanding clear sub-process isolation, tool injection into child agents, and output de-duplication. |
| **Channel Communication Robustness** | OpenClaw (#86519 Telegram duplication), Hermes (#37369 FD leak), CoPaw (#5264 Feishu routing), ZeroClaw (#7958 Telegram gate) | Native formatting, reply chains, and session continuity across all major platforms is table stakes. |
| **LLM Provider Middleware** | OpenClaw (#85103 fallback chains), ZeroClaw (#6302 Gemini 400), Hermes (#47868 metadata leak), IronClaw (#1520 Qwen) | A resilient provider abstraction layer with graceful fallback and cost observability is a core architectural requirement. |
| **Security Hardening** | PicoClaw (#3074 SSRF), NanoClaw (#2807/2818 workspace confine), CoPaw (#5310 Bubblewrap), OpenClaw (#7722 filesystem sandboxing) | Security is becoming a blocker for product decisions; the user base is actively preempting vulnerabilities. |

---

#### 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | IronClaw | LobsterAI | CoPaw |
|---|---|---|---|---|---|---|---|
| **Core Language** | TypeScript | TypeScript | TypeScript | Rust | Rust/TypeScript | TypeScript (Electron) | TypeScript/Python |
| **Primary User** | Bot Ops / Power User | Team / Enterprise | Desktop Developer | Enterprise / Security | DevOps / SaaS | Knowledge Worker | Power User / Plugin Dev |
| **Key Strength** | Broadcast channel + tool support | Lean core, exceptional response time | Desktop edit review, dual-role orchestration | High performance, security-first governance | Automations engine, OAuth, SaaS platform | Computer Use, Office artifacts, voice | Deep plugin ecosystem, context innovation |
| **Architecture** | Modular “Chassis” | Lightweight Core | Dual Role (Doer/Reviewer) | High-Perf Monolithic | “Reborn” Engine v2 | Desktop App (Electron) | AgentScope Protocol |
| **Community Maturity** | High volume, complex regression burden | Proactive, low noise | Sophisticated orchestration patterns | Structured, high governance | Active dogfooding, SRE-like | Visionary RFCs | High contribution, but stability debt |

**Key Takeaway:** No single project dominates all axes. **LobsterAI** and **ZeroClaw** currently demonstrate the highest combination of feature delivery + stability governance. **OpenClaw** and **CoPaw** drive the most architectural innovation but are paying down significant stability debt. **NanoBot** and **NanoClaw** are excellent case studies in tight community feedback loops.

---

#### 6. Community Momentum & Maturity

**Tier 1 – Extreme Velocity + Major Feature Delivery:**
- **ZeroClaw** – v0.8.1 patch by 45 contributors; Discord interactions epic, OIDC groundwork. Strong release discipline.
- **IronClaw** – Closing in on a major version jump (Projects, Automations 2.0, concurrent execution). Dogfooding culture ensures rapid UI fixes.
- **LobsterAI** – Shipped a major release (2026.6.18) with Computer Use MVP and artifact expansion. Dependabot risk (Electron drift) is the only dark spot.

**Tier 2 – High Iteration / Targeted Innovation:**
- **OpenClaw** – Highest absolute volume but needs to resolve its P0 data loss and backlog bottleneck to maintain contributor trust.
- **CoPaw** – Deep plugin/context innovation (Headroom, Scroll, Bubblewrap), but critical process-freeze bugs risk alienating the user base.
- **NanoBot** – Excellent bug-to-fix turnaround. Shifting from solo dev tool to team/enterprise deployment.
- **NanoClaw** – Focused security sprint; replacement PR culture shows high maturity.
- **Hermes Agent** – Desktop edit review and orchestration patterns are high-value, but session data loss and triage limits are holding back momentum.

**Tier 3 – Maintenance / Low Activity:**
- **PicoClaw** – Stalled on core UX bug; dominated by dependency updates.
- **NullClaw** – Healthy but small; community self-organizes effectively.
- **Moltis** – Effectively paused. A single session lifecycle bug defines the entire month.

**Tier 4 – Dormant:**
- **TinyClaw, ZeptoClaw** – No signals.

---

#### 7. Trend Signals

1. **Context is the Hardest Problem**: The ecosystem consensus is that session state management is the gating factor for all advanced features. Silent data loss (OpenClaw #84882, CoPaw #5171), session freeze (CoPaw #5218), and compression failures (ZeroClaw #7964) dominate the severity lists. **Decision-makers should evaluate context persistence architecture before feature depth.**

2. **Multi-Agent Orchestration is Moving to Production**: The community is actively building Doer/Reviewer patterns (Hermes), hierarchical sub-agent spawning (OpenClaw), and cross-model teams (LobsterAI #2180). This requires first-class tool injection, isolation guarantees, and output routing—gaps that currently block complex workflows.

3. **Channel UX is a Primary Differentiator**: Native buttons, modals, slash commands, and proper reply threading are no longer nice-to-haves. ZeroClaw’s Discord interactions epic and OpenClaw’s Telegram fix sprint show that users judge agent reliability by channel consistency, not just API depth.

4. **Security is Becoming a Product Decision**: Community-contributed SSRF fixes (PicoClaw), privilege escalation reports (NanoClaw), and demands for filesystem sandboxing (OpenClaw #7722) are pushing security from “nice to have” to “critical path blocker” on several roadmaps. The user base is increasingly deploying agents in network-sensitive production environments.

5. **Operational Visibility is non-negotiable**: Users demand cost tracking, context usage indicators, and structured logging. Projects like IronClaw (CostGuard), OpenClaw (#94308), and ZeroClaw (#7953) are racing to close the observability gap.

6. **Provider Fallback is a Feature, not a Config**: Simple retry logic is insufficient. The community is demanding intelligent circuit breakers (ZeroClaw #7881), weighted fallback chains (OpenClaw #85103), and per-provider error handling (Hermes #47868). This reflects a mature understanding that agent reliability cannot depend on any single LLM provider.

7. **“AI Collaborator” over “Single Bot”**: LobsterAI’s highly detailed RFC (#2180) for a natural language command bar and cross-model orchestration signals a shift. Users are outgrowing single-session assistants and demanding persistent, project-level platforms that coordinate multiple models, memory stores, and tools over long time horizons. This represents the next evolutionary step for the entire ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — June 19, 2026

## 1. Today’s Overview

NanoBot is in a phase of **intense development velocity**, with 24 pull requests and 3 issues updated in the last 24 hours. Development effort is concentrated across memory system rearchitecture, channel robustness, WebUI admin UX, and sandbox security. The maintainer team is highly responsive — two critical bugs reported today saw corresponding fix PRs opened within the same day. While no release was cut today, the breadth of feature work and targeted fixes strongly suggests a significant release is being assembled.

---

## 2. Releases

None.

---

## 3. Project Progress

Five pull requests were merged or closed today, each advancing the project:

- **[Consolidation Model for Cheaper Memory](https://github.com/HKUDS/nanobot/issues/1391)** — This long-standing PR adding `consolidation_model` to `AgentDefaults` was closed. It allows routing memory consolidation to a cheaper LLM than the main agent, critical for deployments running expensive orchestrator models like Opus. This work directly feeds the new eager consolidation architecture.
- **[Firecrawl Keyless Setup](https://github.com/HKUDS/nanobot/issues/4403)** — Switched Firecrawl from a local MCP requiring an API key to a hosted keyless Web Data integration, dramatically simplifying one-click setup.
- **[CI: Skip Docs-Only Changes](https://github.com/HKUDS/nanobot/issues/4400)** — Pipeline efficiency improvement; pushes and PRs touching only `docs/` now bypass CI entirely.
- **[Feishu QR Login Flow](https://github.com/HKUDS/nanobot/issues/4391)** — Full device-code flow (init → poll → probe) enabling Feishu/Lark bot creation by scanning a QR code from mobile, eliminating manual credential hunting.

---

## 4. Community Hot Topics

The most engaged discussions reveal deep concern about **state reliability** and **configuration consistency**:

- [**Issue #4307: Post-turn consolidation wipes delivery message**](https://github.com/HKUDS/nanobot/issues/4307) (3 comments) — The community’s top worry. With `context_window_tokens` set modestly, long turns accumulate 100k+ tokens of context. Consolidation fires after the turn completes and destructively archives the assistant's delivery before user follow-up can land. Users call this a **critical regression** in multi-turn UX.
- [**Issue #4374: SOUL.md/USER.md read/write asymmetry**](https://github.com/HKUDS/nanobot/issues/4374) (2 comments) — Bootstrap files are correctly read from the per-turn project workspace but written back to the default workspace. Users adopting the new project workspaces feature (#4007) find their custom identities silently overwritten in the wrong location.
- [**PR #4402: Opt-in Eager Consolidation**](https://github.com/HKUDS/nanobot/issues/4402) — Anticipated as the solution to #4307’s deep problem: archive completed slices into memory history *during* a long turn without trimming the live session, avoiding the destructive post-turn wipe.

---

## 5. Bugs & Stability

| Severity | Issue | Summary | Status |
|---|---|---|---|
| **Critical** | [#4408](https://github.com/HKUDS/nanobot/issues/4408) | `Nanobot.run()` mutates shared `_extra_hooks` state — concurrent calls clobber each other | **Fix PR #4409 opened** (draft) moves hooks to per-call context |
| **Critical** | [#4307](https://github.com/HKUDS/nanobot/issues/4307) | Post-turn consolidation wipes the agent's own delivery message; user follow-ups get no context | No dedicated fix PR yet; #4402 addresses the architecture |
| **High** | [#4374](https://github.com/HKUDS/nanobot/issues/4374) | SOUL.md/USER.md written to wrong workspace (default vs project-root) | **Fix PR #4387** implements fallback logic |
| **High** | [#4342](https://github.com/HKUDS/nanobot/issues/4342) | Feishu cards arriving via WebSocket have structural mismatches (nested lists, missing wrappers) | **Fix PR #4342** maps actual WebSocket format |
| **High** | [#4353](https://github.com/HKUDS/nanobot/issues/4353) | WhatsApp .ogg/.opus voice notes return empty strings from some STT providers | **Fix PR #4353** converts to WAV 16k mono via ffmpeg |
| **Medium** | [PR #4397](https://github.com/HKUDS/nanobot/issues/4397) | LLM ignores user messages injected mid-tool-execution, user gets no response | **Fix PR #4397** adds system hint forcing attention to interruptions |
| **Medium** | [PR #4398](https://github.com/HKUDS/nanobot/issues/4398) | `/api/settings` hangs because it blocks on OAuth token refresh | **Fix PR #4398** caches data and refreshes in background |

---

## 6. Feature Requests & Roadmap Signals

The PR pipeline clearly telegraphs the **next major release** priorities:

- **Memory 2.0 (top signal):** Three interlocking PRs point to a systemic overhaul: `consolidation_model` (#1391) for cost control, opt-in eager consolidation (#4402) for destructive-wipe prevention, and configurable tool microcompaction (#4392) for cache-sensitive deployments. This is the project’s highest-investment axis.
- **Admin & Onboarding UX:** Two PRs target multi-instance deployments: [#4399](https://github.com/HKUDS/nanobot/issues/4399) adds `hidden_settings_sections` for a “normie-friendly” simplified WebUI, and [#4395](https://github.com/HKUDS/nanobot/issues/4395) revamps the CLI wizard with a calmer terminal palette and draft-preserving navigation.
- **Optional Feature Enablement:** [PR #4396](https://github.com/HKUDS/nanobot/issues/4396) introduces optional capability discovery (`plugins list/enable`), moving Bedrock and other heavy integrations behind opt-in gates.
- **Channel & Integration Expansion:**
  - WhatsApp: LID→phone seeding on startup ([#4407](https://github.com/HKUDS/nanobot/issues/4407)) for reliable `allowFrom` matching.
  - Web Search: New Serper.dev provider ([#4406](https://github.com/HKUDS/nanobot/issues/4406)) and keyless Keenable tier ([#4405](https://github.com/HKUDS/nanobot/issues/4405)).
  - Sandbox: Configurable bwrap bind roots ([#4404](https://github.com/HKUDS/nanobot/issues/4404)) for exposing `~/.local/bin` or `~/.cargo/bin`.

---

## 7. User Feedback Summary

- **Strongest Pain Points:** Memory data loss during consolidation (#4307) dominates user concern. Second is the workspace configuration read/write inconsistency (#4374), which breaks multi-project workflows that rely on agent identity files.
- **Deployment Patterns:** The user base is shifting toward **team and enterprise deployments** — evidenced by requests for WebUI admin hiding, multi-instance config, sandbox bind roots, and enterprise channel support (Feishu, WhatsApp).
- **Sentiment:** The community is **technically sophisticated and proactive** — users submit draft fix PRs within hours of reporting bugs (e.g., #4408→#4409). This reflects a healthy contributor ecosystem and high maintainer trust. The volume of “enhancement” and “channel” labels suggests users are actively tailoring NanoBot to specific production workflows rather than just experimenting.

---

## 8. Backlog Watch

The project’s responsiveness is excellent — most bugs have same-day fix PRs. However, two items warrant attention:

- [**Issue #4307 — Post-turn consolidation wipes delivery message**](https://github.com/HKUDS/nanobot/issues/4307): Open since June 12, this is the **highest-severity unresolved bug** without a dedicated fix PR. While #4402 addresses the broader consolidation architecture, the immediate regression needs a targeted patch or a clear maintainer status update.
- [**Issue #4374 — Workspace read/write asymmetry**](https://github.com/HKUDS/nanobot/issues/4374): The fallback fix in #4387 is pending review. This impacts everyone using the project workspaces feature, a core UX path introduced in #4007.

**General Health:** Excellent. No abandoned PRs or stale critical bugs. The backlog is essentially the current day’s work-in-progress.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the project digest for **Hermes Agent** on **2026-06-19**, generated from the provided GitHub data.

---

## Hermes Agent Project Digest – 2026-06-19

### 1. Today's Overview
The project is experiencing a **sustained high-velocity cycle**, with 50 issues and 50 pull requests updated within the last 24 hours. This indicates a healthy, actively engaged community, but the sheer volume creates a significant triage challenge, as 45 issues remain open and 48 PRs await review or merge. Activity is split roughly evenly between **critical bug fixes** (session data loss, gateway stability) and ambitious **new feature PRs** for the Desktop app and platform gateways. Notably, no new release was tagged today, meaning the rapid bleeding-edge development pace is serving as the primary user-facing version.

### 2. Releases
**None.** There are no published releases for this date.

### 3. Project Progress
While the PR merge velocity on this specific date was low (only 2 closed/merged), significant progress was made by resolving four high-impact bugs today:

- **FD Leak in Telegram Gateway (#37369):** A critical `P1` bug where the gateway leaked SQLite connections leading to `OSError: Too many open files` after ~2 days of operation was closed.
- **SQLite Trigram Tokenizer Regression (#47002):** The `v0.16.0` regression that crashed `SessionDB` on systems lacking the trigram tokenizer has been resolved.
- **Live-Only Chat Risk (#41386):** The `P1` issue where CLI/Desktop sessions could run entirely in-memory when `state.db` was unavailable, causing total session loss on resume, was closed.
- **WhatsApp Group Support (#47477):** A `P3` feature request for a comprehensive, copy-paste-ready guide for WhatsApp messaging via Termux/Hermes Skill was merged/closed, indicating strong community creation of user-facing documentation.

### 4. Community Hot Topics

**Most Active Issues (by comment count):**

- **#34592 – Doer/Reviewer 双角色并行编排 + Hindsight 共享记忆** (5 comments)
  - *Analysis:* A sophisticated community user shared a detailed production architecture running a dual Doer/Reviewer parallel execution system with shared memory for complex tasks (literature review, code review). This highlights a growing demand for **multi-agent orchestration patterns** and shared memory primitives within the Hermes ecosystem.
- **#41625 – MCP tools not exposed to agent in TUI mode** (5 comments, 1 👍)
  - *Analysis:* Discovered MCP tools ("3 tools found") are entirely unavailable inside the primary TUI session. This is a critical UX gap for the MCP integration, causing significant friction for users adopting the TUI as their main interface.
- **#47477 – WhatsApp Group Sending Guide** (5 comments)
  - *Analysis:* A guide to sending WhatsApp messages via Termux was heavily engaged with. This signals strong user interest in **mobile-first and low-infrastructure deployments** of the Hermes agent.

**Most Active Pull Requests (all very fresh, mid-June dates):**

- **#48813 – Cursor-style Agent Edit Review (Desktop):** A massive feature PR introducing an accept/reject diff review surface for the desktop app. This directly targets the user pain point of trusting autonomous file modifications.
- **#23243 – TUI 16-language i18n Framework:** A long-standing PR (since May 10) that was updated today. It represents a major push for global accessibility beyond English speakers.
- **#48453 – Fix Gateway Self-Restart Deadlock:** A `P1` fix for a critical stability issue.
- **#48806 – Tighten Background Task Contract:** A refactor of the `delegate_task` tool to clarify `background=true` as a short async task rather than a durable job, aligning agent behavior with user expectations.

### 5. Bugs & Stability

**Critical (P1):**
- **#48519 – Sub-Profile Gateway Data Loss:** Sessions are created in `sessions.json` but `state.db` remains empty, resulting in **complete session data loss** for non-default profiles.
- **#48746 – Gateway Self-Restart Deadlock on macOS:** Gateway exits with code 75, but `launchd` treats it as a permanent failure, causing the service to hang in a zombie "running" state.
  - *Fix Status:* PR **#48453** (fix gateway self-restart deadlock) is open and directly addresses this.
- **#48721 – `hermes update` fails on macOS/Python 3.14:** The `uv` branch targets the wrong Python interpreter, hitting a PEP 668 block on Homebrew Python.

**High Impact (P2):**
- **#48083 – Web Tools Missing for Local Ollama Models:** The web toolset is not passed to the model unless explicitly named, forcing local model users into subpar fallback modes.
- **#33618 – Persistent `/goal` Lost on Context Compression:** The goal state is tied to a rotating `session_id`, breaking long-term task persistence.
- **#47868 – Strict Provider Rejection (Leaked Metadata):** Hermes leaks `timestamp` metadata into OpenAI-compatible payloads, causing rejection by strict providers like Fireworks-backed models.
- **#45245 – Cron Scheduler Misroutes Provider:** Cron jobs configured with a specific provider are being routed to the wrong API surface.

**Recent Regressions Addressed (Closed today):**
- **#47002 (SessionDB Crash):** Resolved v0.16.0 regression.
- **#37369 (FD Leak):** Resolved gateway stability issue.

### 6. Feature Requests & Roadmap Signals

**Desktop/Dashboard Expansion:**
- **#48813 – Edit Review Surface:** This feature (Cursor-style accept/reject diffs) is a strong candidate for the next minor release, acting as a safety net for autonomous agent file operations.
- **#48564 – Dashboard/TUI Reliability RFC:** An umbrella issue addressing event-loop starvation and stale workers. This suggests the team is prioritizing **production hardening** for the desktop UI.
- **#48805 – Usage Quotas Page:** Adds a dedicated analytics page for provider usage, indicating a move towards observability and cost management.

**Platform and Provider Extensibility:**
- **#48737 / #48807 – Native Table Rendering for Slack & Feishu:** Both PRs convert markdown tables to native Block Kit/CardKit blocks. This is a quality-of-life improvement for enterprise users reliant on structured data.
- **#48011 – Mission/Project Source-of-Truth Primitive:** A user-requested first-class abstraction for strategic multi-turn work, suggesting users are outgrowing the current memory/task system.

**Local & Cross-Platform Support:**
- **#48716 – Windows Native Integration Package:** A detailed request to run Hermes + WebUI without Docker or WSL2. The explicit rejection of Windows by `bootstrap.py` is a noted friction point.
- **#48797 – Piper TTS `speaker_id`:** A small but clear signal of demand for voice output and accessibility features.

### 7. User Feedback Summary

**Pain Points:**
- **Platform Portability:** Users are struggling with Homebrew Python updates (PEP 668) and explicit Windows bootstrapping blocks. The assumption of a Linux/Docker environment is causing friction for a growing macOS/Windows user base.
- **Session Reliability:** Multiple bugs today (#48519, #33618, #41386) point to a **crisis of trust in session persistence**, especially when using profiles or context compression.
- **MCP Integration Clarity:** While the MCP API works in CLI tests, **TUI users are completely blocked** from using MCP tools, which represents a significant feature regression for the default user interface.
- **Local Model Experience:** Users running local models like Ollama (Gemma 4, Llama) face inconsistent tool registration and specific error handling failures, diminishing the "local-first" value proposition.

**Use Cases & Satisfaction:**
- **Sophisticated Orchestration:** The highly detailed #34592 community post shows advanced users are successfully building complex **Doer/Reviewer multi-agent workflows** on top of Hermes, proving the flexibility of the core architecture.
- **Mobile/Convenience:** The WhatsApp guide (#47477) and Telegram gateway demand indicate a strong user segment wants to use Hermes as a personal assistant via mobile platforms.
- **Positive Reaction to Feature Velocity:** The rapid appearance of high-quality PRs (edit review, Slack tables, usage quotas) suggests a very **active and capable external contributor base** who are highly engaged with the project’s trajectory.

### 8. Backlog Watch

Several important items remain without recent maintainer action or are stalled in review:

- **#33314 – Post-Update Check Hooks (May 27):** A request for skill/profile drift detection after `hermes update`. 4 comments, no resolution. The underlying problem is valid but complex.
- **#30594 – PEP 668 + `hermes update` (Lazy Backends) (May 22):** A related bug to the newly filed #48721. This affects a different code path (`_venv_pip_install`) and remains unresolved, impacting Debian/Ubuntu users.
- **#31621 – Gemini/OpenRouter Web Tools Support (May 24):** A request to support Google Grounding and OpenRouter's Exa integration in `web_tools.py`. Stalled despite high-quality provider research in the comments.
- **#35409 – Profile/Model Override for `delegate_task` (May 30):** A user requests the ability to route sub-tasks to specific model profiles. There is a related refactor PR (#48806) tightening the task contract today, which may lay groundwork for this feature.
- **PR #23243 – TUI 16-Language i18n (May 10):** The largest feature PR on the board by scope. It has been open for over a month, likely waiting for a dedicated review of the localization infrastructure.
- **PR #35347 – Alibaba Cloud Token Plan Provider (May 30):** A well-defined provider PR that has received no recent attention despite being open for 20 days.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-19

## 1. Today's Overview
The project is currently in a high-activity maintenance cycle, driven heavily by automated dependency management. In the past 24 hours, 14 pull requests were updated, with 7 merged and 7 still open. A new nightly build (`v0.3.0-nightly.20260619`) was published. While a significant portion of activity was infrastructure-focused (Dependabot bumps across Go runtime, Azure SDK, Anthropic SDK, and ESLint/Vite frontend tooling), meaningful functional progress was made on debugging the `web_search` tool and patching an SSRF security bypass. Despite this, a critical user-facing bug regarding duplicate messages from async subagents (Issue [#3094](https://github.com/sipeed/picoclaw/issues/3094)) remains open and unresolved, representing the biggest risk to user experience this cycle.

## 2. Releases
A new **nightly** release was published:
- **Tag**: `v0.3.0-nightly.20260619.287853ab`
- **Description**: Automated nightly build from the `main` branch. Labeled as potentially unstable.
- **Changelog**: [Compare v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

No stable versioned release or breaking change migration guide was included in this build.

## 3. Project Progress
**Merged/Closed PRs (7 total):**

- **Web Search Reliability**: [#3141](https://github.com/sipeed/picoclaw/pull/3141) (merged by jincheng-xydt) – Adds diagnostic logging when the Brave Search API returns an empty response with HTTP 200. This fix directly addresses the silent failure mode reported in Issue [#3125](https://github.com/sipeed/picoclaw/issues/3125), improving debuggability when the response format shifts.
- **Copilot SDK Maturation**: [#3107](https://github.com/sipeed/picoclaw/pull/3107) (merged) – Bumped `github/copilot-sdk/go` from `v0.2.0` to `v1.0.1`. This major version step indicates GitHub Copilot Extension integration is moving toward a stable API contract.
- **Anthropic SDK Update**: [#3149](https://github.com/sipeed/picoclaw/pull/3149) (merged) – Bumped `anthropic-sdk-go` from `v1.46.0` to `v1.50.2`, pulling in the latest Claude API features and fixes.
- **Core Go & Azure Dependencies**: [#3146](https://github.com/sipeed/picoclaw/pull/3146) (`golang.org/x/term`), [#3147](https://github.com/sipeed/picoclaw/pull/3147) (`Azure/azidentity`), [#3148](https://github.com/sipeed/picoclaw/pull/3148) (`golang.org/x/sys`) – All merged.
- **CI/CD Pipeline**: [#3144](https://github.com/sipeed/picoclaw/pull/3144) (merged) – Bumped `actions/checkout` from `v6` to `v7`.

## 4. Community Hot Topics
The community’s attention this cycle is split between a persistent UX bug and an active security patch:

- **Primary Concern – Async Subagent Duplication** ([#3094](https://github.com/sipeed/picoclaw/issues/3094)):
    - User `v2up-32mb` reports that when using the `spawn` tool (asynchronous subagents), the exact same output is delivered twice to the user: once as a raw subagent dump and again as part of the master agent’s summary. This degrades the experience on chat platforms like Feishu/Lark and Telegram.
    - **Analysis**: This is the most commented/reported user-facing bug. The `stale` label suggests maintainer bandwidth is stretched, but this directly impacts core agent usability.

- **Security Hardening – SSRF Guard Bypass** ([#3143](https://github.com/sipeed/picoclaw/pull/3143)):
    - Contributor `lc6464` submitted a fix for an SSRF bypass (originating from Issue [#3074](https://github.com/sipeed/picoclaw/issues/3074)) where ISATAP IPv6 literals containing private IPv4 addresses could evade the `web_fetch` blocklist.
    - This is currently an **open** PR awaiting merge, indicating active community investment in enterprise security boundaries.

## 5. Bugs & Stability

| Severity | Item | Status | Analysis |
|---|---|---|---|
| **HIGH** | **Async Subagent Duplication** ([#3094](https://github.com/sipeed/picoclaw/issues/3094)) | Open / Stale | Core UX flaw. Every `spawn` invocation fires a duplicate message. No fix PR exists. This should be the top stable-release blocker. |
| **HIGH** | **SSRF Guard Bypass** (Issue [#3074](https://github.com/sipeed/picoclaw/issues/3074), PR [#3143](https://github.com/sipeed/picoclaw/pull/3143)) | Fix PR Open | Malicious ISATAT addresses can bypass the SSRF filter in `web_fetch`. A patch is written and awaiting review; this is a security-sensitive gap. |
| **MEDIUM** | **Brave Search Silent Failure** ([#3125](https://github.com/sipeed/picoclaw/issues/3125)) | **CLOSED** | The architectural migration to `.security.yml` broke the Brave API integration. A fix PR ([#3141](https://github.com/sipeed/picoclaw/pull/3141)) was merged to add logging, closing the loop. |
| **LOW** | **Frontend Dependency Backlog** (PRs [#3100](https://github.com/sipeed/picoclaw/pull/3100)–[#3105](https://github.com/sipeed/picoclaw/pull/3105)) | Open / Stale | 5 Dependabot PRs for Vite, ESLint, shadcn, and TypeScript-ESLint have been stale since June 11th. While low urgency, this represents accumulating technical debt. |

## 6. Feature Requests & Roadmap Signals
- **Copilot Extension as a First-Class Feature**: The major jump to `copilot-sdk-go v1.0.x` (PR [#3107](https://github.com/sipeed/picoclaw/pull/3107), merged; PR [#3145](https://github.com/sipeed/picoclaw/pull/3145) to `v1.0.2`, open) strongly signals that PicoClaw's role as a GitHub Copilot Agent extension is a formal, stabilized roadmap priority.
- **Web Tooling Reliability & Security**: The concurrent fixes for SSRF bypasses ([#3143](https://github.com/sipeed/picoclaw/pull/3143)) and silent search failures ([#3141](https://github.com/sipeed/picoclaw/pull/3141)) indicate a backend push toward secure, debuggable web fetch/search capabilities.
- **Frontend Refresh in Progress**: The accumulated Dependabot PRs in `/web/frontend` (Vite 8, shadcn 4.11, ESLint 10.4) suggest a UI update is pending. These updates are currently idle, but their content points to an upcoming frontend modernization wave.

## 7. User Feedback Summary
- **Core UX Downgrade**: The async duplication bug ([#3094](https://github.com/sipeed/picoclaw/issues/3094)) is the most prominent pain point. The agent is delivering repetitive, unformatted output, which heavily impacts trust and chat flow for subagent-based workflows.
- **Configuration Friction**: Issues like the `.security.yml` breaking Brave search ([#3125](https://github.com/sipeed/picoclaw/issues/3125)) show that tool configuration migrations introduce regressions. Users expect silent breakage to be caught earlier.
- **Security-Conscious User Base**: The submission of the SSRF patch ([#3143](https://github.com/sipeed/picoclaw/pull/3143)) by a community member demonstrates a user base actively invested in running PicoClaw in secure, network-sensitive environments.

## 8. Backlog Watch
| Item | Age | Action Required |
|---|---|---|
| **Async Subagent Duplication** ([#3094](https://github.com/sipeed/picoclaw/issues/3094)) | Opened 2026-06-10 (9 days stale) | **Critical.** Needs assignee immediately. This is the highest-impact open user bug. A fix in the master-agent output aggregation pipeline is required. |
| **SSRF Guard Bypass Fix** ([#3143](https://github.com/sipeed/picoclaw/pull/3143)) | Opened 2026-06-18 (today) | **Fast-track review.** A security patch with a clear regression test suite. Every day this sits open, the `web_fetch` tool is vulnerable to SSRF. |
| **Stale Frontend Dependencies** ([#3100](https://github.com/sipeed/picoclaw/pull/3100), [#3101](https://github.com/sipeed/picoclaw/pull/3101), [#3103](https://github.com/sipeed/picoclaw/pull/3103), [#3104](https://github.com/sipeed/picoclaw/pull/3104), [#3105](https://github.com/sipeed/picoclaw/pull/3105)) | Opened 2026-06-11 (8 days stale) | **Batch decision.** Maintainers should either merge these en masse or close them with a planned integration date. Leaving them open creates noise and delays critical frontend security patches. |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest — 2026-06-19**

---

## 1. Today's Overview
NanoClaw is in an exceptionally active development window with **21 PRs updated** and **5 issues updated** in the past 24 hours. The project is undergoing a coordinated **security hardening sprint** — a critical privilege-escalation report (#2807) and multiple workspace-confinement patches (#2818, #2817, #2814) are under active review. Community contribution quality is high, with several authors submitting replacement PRs that add regression tests based on maintainer feedback. No new release was cut, but the volume of merged fixes (6 PRs closed, including agent-to-agent approval policies and interop improvements) strongly signals a patch release is imminent.

---

## 2. Releases
No new releases were published in the last 24 hours. The current stable tip remains at the `main` branch content (v2.1.18 per PR #2808). Given the volume of merged fixes and pending security patches, a v2.1.19 or v2.2.0 release is expected within the next week.

---

## 3. Project Progress — Merged/Closed PRs
Six PRs were closed or merged today, spanning features, refactoring, and community outreach:

| PR | Type | Summary |
|---|---|---|
| [#2793](https://github.com/nanocoai/nanoclaw/pull/2793) | Feature | **Per-message approval policies** on agent-to-agent connections (a critical governance gate, fully backward-compatible). |
| [#2811](https://github.com/nanocoai/nanoclaw/pull/2811) | Fix | `fix(setup)` — allows environment-selected agent provider during setup. |
| [#2810](https://github.com/nanocoai/nanoclaw/pull/2810) | Refactor | Symlinks `.agents/skills` and `AGENTS.md` to `.claude` counterparts, enabling interop with agent-convention tooling (e.g., Codex). |
| [#2803](https://github.com/nanocoai/nanoclaw/pull/2803) | Refactor | **Removed dead code** — `resolveGroupIpcPath` had no callers after the v2 IPC rearchitecture. |
| [#2806](https://github.com/nanocoai/nanoclaw/pull/2806) | Docs | **Korean README** (`README_ko.md`) added and linked from existing localization switchers. |

---

## 4. Community Hot Topics

**Podman as a Docker Alternative**
- [Issue #957](https://github.com/nanocoai/nanoclaw/issues/957) (CLOSED, 10 comments, +7)
- The highest-reacted issue this period. The user requested documentation for Podman support. Now closed, implying maintainers have accepted the suggestion or made docs changes.

**Security Hardening Blitz**
- [Issue #2807](https://github.com/nanocoai/nanoclaw/issues/2807) (Sparked the conversation)
- [PR #2818](https://github.com/nanocoai/nanoclaw/pull/2818) / [#2817](https://github.com/nanocoai/nanoclaw/pull/2817) — Confining `send_file` reads to the agent workspace.
- [PR #2814](https://github.com/nanocoai/nanoclaw/pull/2814) — Validating group folders in the CLI `create` path.
- The volume of security-focused PRs and the effort taken to replace initial patches with better-tested versions (e.g., #2816 replacing #2812, #2815 replacing #2801) shows a community deeply invested in production readiness.

**Telegram Agent-Swarm Migration Blocking**
- [Issue #2632](https://github.com/nanocoai/nanoclaw/issues/2632) (Open, created 2026-05-28)
- A user explicitly trying to plan a v1→v2 migration is stalled by ambiguous telemetry around the old `/add-telegram-swarm` feature. This is a clear signal that a migration guide is the top documentation need.

---

## 5. Bugs & Stability (Ranked by Severity)

**CRITICAL — Privilege Escalation via Child Agents**
- [Issue #2807](https://github.com/nanocoai/nanoclaw/issues/2807)
- Non-owner members can create persistent child agents without approval in owner-initialized groups. No dedicated fix PR is linked yet, but today's workspace-confinement patches (#2814, #2818) indicate the team is already in the security hardening mindset.

**HIGH — CLI Create Commands Fully Broken**
- [PR #2804](https://github.com/nanocoai/nanoclaw/pull/2804)
- Every `ncl messaging-groups create` call throws `NOT NULL constraint failed: messaging_groups.instance`. The fix is on the table (adds missing `instance` validation).

**HIGH — Container Runner Source Staleness**
- [Issue #2784](https://github.com/nanocoai/nanoclaw/issues/2784)
- The source-copy logic only watches `index.ts`, missing changes to `ipc-mcp-stdio.ts`. This can cause silent failures for users relying on the container runner.

**MEDIUM — Database Integrity**
- [PR #2808](https://github.com/nanocoai/nanoclaw/pull/2808)
- `insertMessage` is not idempotent (bare `INSERT` instead of `INSERT OR IGNORE`), and approval rows lack `agent_group_id`. Fix PR includes regression tests.

**LOW — Discord Message Truncation**
- [PR #2812](https://github.com/nanocoai/nanoclaw/pull/2812) / [#2816](https://github.com/nanocoai/nanoclaw/pull/2816)
- The Discord adapter never sets `maxTextLength`, causing long replies to be truncated instead of chunked. Replacement PR with tests now available.

---

## 6. Feature Requests & Roadmap Signals

**High-Certainty Inclusions (Next Release)**
- **Expandable messaging channels** — The closure of the Signal request (#29) and active iMessage fix (#2792) suggest the next release will broaden supported communication backends.
- **Apple Container Runtime** — [PR #2809](https://github.com/nanocoai/nanoclaw/pull/2809) adds `CONTAINER_RUNTIME=container` and a remote OneCLI gateway. If merged, this is a major macOS ecosystem play.
- **Fine-grained agent permissions** — The merged per-message approval policies (#2793) open the door for richer governance models.

**Emerging User Needs**
- **CLI-Based Dashboarding** — [PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795) proposes a read-only CLI-derived dashboard skill.
- **Multi-Bot Identity / Swarms** — Issue #2632 highlights user demand for clear documentation and re-implementation of Telegram swarm features in v2.

---

## 7. User Feedback Summary

| Theme | Signal | Sentiment |
|---|---|---|
| **Security responsiveness** | Quick PR iteration on #2807, #2818, #2817 | Positive — community trusts the maintainers' reaction time. |
| **Migration friction** | Issue #2632 (Telegram swarm v1→v2) | **Frustrated** — user is planning a fork due to ambiguous roadmap. |
| **Cross-platform parity** | Issue #957 (Podman, +7) | Strong desire to reduce Docker lock-in. |
| **Quality of Life regressions** | PR #2804 (CLI dead), PR #2812 (Discord truncation) | Immediate friction for daily users; fast fix turnaround is redeeming. |
| **Community robustness** | Multiple "replacement PRs" adding regression tests | High contributor maturity and maintainer rigor. |

---

## 8. Backlog Watch

**Telegram Swarm Migration Guide**
- [Issue #2632](https://github.com/nanocoai/nanoclaw/issues/2632) — Author: arthurkrupa
- Created: **2026-05-28** (22 days ago)
- **Status:** Zero maintainer responses. This is the highest-priority documentation gap. The user is asking a direct question about the existence and future of the swarm feature, and silence is pushing them toward forking.

**Container Runner Caching Bug**
- [Issue #2784](https://github.com/nanocoai/nanoclaw/issues/2784) — Author: masslbp
- Created: **2026-06-16** (3 days ago)
- **Status:** 1 comment, no maintainer acknowledgment. While younger than #2632, this is a subtle bug that undermines the container runner's reliability and could cause confusion for new users.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the **NullClaw Project Digest** for **19 June 2026**, based on the provided GitHub activity.

---

### 1. Today’s Overview

NullClaw saw moderately active development and community engagement today, driven largely by external contributors. While no new releases were cut, four open pull requests signal meaningful progress on streaming functionality and documentation coverage. The four open issues reflect a diverse set of user interests—from edge hardware compatibility to enterprise WeChat integration. The simultaneous arrival of PR #963 alongside Issue #817 strongly indicates that the community is self-organizing to solve its own feature gaps. Overall, the project appears healthy and responsive, with a clear tilt toward solidifying integrations and fixing critical streaming bugs.

---

### 2. Releases

No new releases were published in the last 24 hours. The active PR queue (PRs #962, #963, #964, #965) suggests that the next release cycle may include significant improvements to the Anthropic provider, WeChat channel support, and streaming tool-call parsing.

---

### 3. Project Progress

No pull requests were merged or closed today. However, four new open PRs represent notable steps forward in the codebase:

- **Native Anthropic Provider Documentation** (PR [#962](https://github.com/nullclaw/nullclaw/pull/962)): Adds a full subsection for using the Anthropic API directly, including OAuth handling. This closes the previously requested Issue #767.
- **WeChat QR Code Login Channel Documentation** (PR [#963](https://github.com/nullclaw/nullclaw/pull/963)): Documents how to set up a personal WeChat account via QR code login, directly resolving Issue #817.
- **Native Tool Calls During Streaming** (PR [#964](https://github.com/nullclaw/nullclaw/pull/964)): Fixes a bug in `agent/root.zig` where native tools were silently disabled whenever streaming was enabled, preventing `tools[]` + `tool_choice: "auto"` from working.
- **Structured Streaming SSE Parser** (PR [#965](https://github.com/nullclaw/nullclaw/pull/965)): An accompanying enhancement to ensure the SSE parser handles model-emitted XML in `delta.content` cleanly when tools are active during streaming.

---

### 4. Community Hot Topics

- **WeChat QR Code Login (Issue [#817](https://github.com/nullclaw/nullclaw/issues/817) / PR [#963](https://github.com/nullclaw/nullclaw/pull/963))**: This is the most active topic of the day. A user explicitly requested confirmation and documentation for WeChat QR login. The community responded quickly with a full documentation PR, which should allow this issue to close shortly.
- **Streaming + Tool Calls (PRs [#964](https://github.com/nullclaw/nullclaw/pull/964) & [#965](https://github.com/nullclaw/nullclaw/pull/965))**: Contributor **mtdphn** submitted a deep two-PR stack addressing a core technical limitation. The discussion reveals an underlying developer pain point: the inability to use native tools reliably during streaming sessions.
- **ESP32 Feasibility (Issue [#50](https://github.com/nullclaw/nullclaw/issues/50))**: An old but still active thread (4 comments) exploring whether NullClaw can run on resource-constrained hardware. The long tail of engagement suggests a dedicated niche of IoT/edge developers following the project.
- **Subagent Architecture (Issue [#190](https://github.com/nullclaw/nullclaw/issues/190))**: A recurring architectural discussion about multi-agent orchestration with different providers. This taps into a sophisticated user base looking to build complex agent swarms.

---

### 5. Bugs & Stability

| Severity | Issue / PR | Description |
|---|---|---|
| **High** | PR [#964](https://github.com/nullclaw/nullclaw/pull/964) | Native API-level tools are completely disabled during streaming. This breaks core functionality for users who rely on structured tool calls with streaming responses. **Fix exists in open PR.** |
| Medium | Issue [#913](https://github.com/nullclaw/nullclaw/issues/913) | User reports that raw NullClaw messaging is faster than the A2A protocol implementation. This may indicate unnecessary overhead or a bug in the A2A handler. No fix PR yet. |
| Low | None reported | No crashes, regressions, or security vulnerabilities were logged in the last 24 hours. |

---

### 6. Feature Requests & Roadmap Signals

- **Native Anthropic Provider (PR [#962](https://github.com/nullclaw/nullclaw/pull/962))** — **High Probability for Next Release**: Documentation is already drafted and ready. This lowers the barrier for Anthropic API users and suggests strong internal or community prioritization.
- **WeChat Personal Account Channel (PR [#963](https://github.com/nullclaw/nullclaw/pull/963))** — **High Probability**: Directly requested by the community and now documented. Likely to ship in the next patch release.
- **Agent-to-Agent (A2A) Performance (Issue [#913](https://github.com/nullclaw/nullclaw/issues/913))** — **Needs Triage**: The user is actively benchmarking, but the lack of an official response or benchmark documentation leaves this feature in a credibility gap.
- **Subagent Spawning with Cross-Provider Support (Issue [#190](https://github.com/nullclaw/nullclaw/issues/190))** — **Medium Probability / Roadmap**: A complex architectural ask. If this lands, it signals a major shift toward multi-agent orchestration as a core use case.
- **Edge Deployment / ESP32 (Issue [#50](https://github.com/nullclaw/nullclaw/issues/50))** — **Low Probability / Strategic Exploration**: Hardware portability is mentioned but no maintainer has weighed in on feasibility or timeline.

---

### 7. User Feedback Summary

- **Satisfaction Drivers**: The rapid PR response to the WeChat feature request (Issue #817 → PR #963) indicates a responsive and contributor-friendly environment. The streaming tool-call fix (PR #964) addresses a specific advanced-user pain point that was likely a blocker for several developers.
- **Pain Points**:
    - *Performance Anxiety*: User **jacktang** (Issue #913) is directly comparing raw messaging vs. A2A protocol speeds, expressing clear disappointment with A2A latency.
    - *Feature Gaps*: Users are actively asking for mature integration support (WeChat, Anthropic) which implies the base platform is stable enough that users are ready to productionize it.
    - *Hardware Ambitions*: The ESP32 question (Issue #50) reflects an aspirational community segment wanting fully local, low-power AI agents, but the lack of progress suggests this remains an unsolved challenge.

---

### 8. Backlog Watch

- **Issue [#50](https://github.com/nullclaw/nullclaw/issues/50) — ESP32 Support (Since Feb 2026)**: The oldest open question in the dataset. While it has 4 comments, there is no official roadmap or rejection response. This is becoming a festering request that could benefit from a simple "investigating" or "not planned" label.
- **Issue [#190](https://github.com/nullclaw/nullclaw/issues/190) — Subagent Spawning (Since Mar 2026)**: A high-value architectural feature request sitting untouched for over three months. Triage here would help the community understand if this is a planned 0.x release or a v1.0 candidate.
- **Issue [#913](https://github.com/nullclaw/nullclaw/issues/913) — A2A Performance (Since May 2026)**: Newer, but left with zero maintainer interaction. If the A2A protocol is a core differentiating feature, ignoring a direct performance comparison is a risk to adoption.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-19

## 1. Today's Overview

The IronClaw project is operating at extremely high velocity, with **31 issues** and **43 PRs** updated in the last 24 hours. Development is heavily concentrated on the "Reborn" engine, specifically the new **Projects** organizational feature, **automations/scheduled triggers** overhaul, and **OAuth/auth gate** hardening. A significant simultaneous effort is underway to improve **LLM provider error handling**—particularly around silent retry hangs—and to polish the WebUI approval/consent flows based on active dogfooding feedback. While no formal release was cut today, the merge of foundational backend APIs (Projects endpoints, fire-once triggers) and the advancement of front-end wiring indicates a major feature release is imminent. Overall project health is strong, with high community engagement and rapid issue-to-fix turnaround times on UI feedback.

## 2. Releases

**No new releases were published today.** The last tagged release remains **IronClaw v0.29.1**. Given the volume of merged features targeting the Reborn engine and the closure of the Engine v2 default flip umbrella tracker ([#2800](nearai/ironclaw Issue #2800)), a significant version jump is likely in the coming days.

## 3. Project Progress

The following major efforts advanced today:

**Merged/Closed PRs:**
- **Scheduled Triggers:** [#5065](nearai/ironclaw PR #5065) (*feat(triggers): fire-once*) — Introduced one-shot scheduled triggers. `trigger_create` now requires an explicit `completion_policy` (`recurring` | `complete_after_first_fire`), preventing silent default recurrence.
- **Projects Backend:** [#5018](nearai/ironclaw PR #5018) (*feat(reborn): Projects — WebChat v2 endpoints 4/5*) — Merged the HTTP surface for project and membership CRUD (9 routes).
- **OAuth UX:** [#5067](nearai/ironclaw PR #5067) (*fix(reborn): keep OAuth auth gates visible*) — Fixed a regression where OAuth cards would hide when the authorization URL was temporarily unavailable.
- **UI Polish:** [#5055](nearai/ironclaw PR #5055) (*fix(webui): soften automation run errors*) — Changed automation error rendering from red terminal errors to yellow "Needs attention" badges.

**Active PRs of Interest:**
- **Projects Frontend:** [#5019](nearai/ironclaw PR #5019) (*5/5 stack*) — Wiring the full Projects page in WebChat v2.
- **Concurrent Execution:** [#5085](nearai/ironclaw PR #5085) — Proposes a `TurnRunScheduler` to replace strictly serial turn execution with per-user/per-type capped concurrency. Architecturally significant.
- **LLM Robustness:** [#5043](nearai/ironclaw PR #5043) & [#5045](nearai/ironclaw PR #5045) — Fixes for the critical `NEARAI_MODEL=auto` retry hang that caused multi-minute silent failures.
- **Engine V2 Analytics:** [#4989](nearai/ironclaw PR #4989) — Records Engine V2 LLM completions through CostGuard for admin usage aggregates.
- **Automations Redesign:** [#5084](nearai/ironclaw PR #5084) — Reworks the Automations page into denser summary cards with status indicators.
- **Approval Dials:** [#5082](nearai/ironclaw PR #5082) — Truncates long approval commands in modals (fixing [#5078](nearai/ironclaw Issue #5078)).

## 4. Community Hot Topics

- **Agent Recovery from Errors** ([#4761](nearai/ironclaw Issue #4761), 5 comments, CLOSED) — Users reported agents stopping completely after repeated tool failures instead of recovering. The 5-comment discussion reflects deep community concern about autonomous agent reliability. The issue is now closed, indicating a fix has landed.

- **LLM Provider Compatibility** ([#1520](nearai/ironclaw Issue #1520), 3 comments, OPEN — created Mar 21) — Users continue to experience failures with the Alibaba Qwen Coding Plan endpoint. This long-standing issue suggests either an upstream API incompatibility or a missing integration path that has not yet been prioritized.

- **OAuth Flow Breakage** ([#4907](nearai/ironclaw Issue #4907), 3 comments, CLOSED) — Google Calendar users reported successful OAuth flows that left the original run in a failed state instead of resuming. This represents a major UX pain point where the authentication UX and the execution pipeline are not properly linked.

- **Tool Call UI Staleness** ([#4942](nearai/ironclaw Issue #4942), 3 comments, CLOSED) — Tool call failures were invisible in the WebUI until a manual page reload. The community discussion highlighted the need for real-time SSE-based status updates.

## 5. Bugs & Stability

**Critical:**
- **OAuth Token Expiry** ([#5071](nearai/ironclaw Issue #5071), OPEN, risk: high) — Google OAuth access tokens expire after ~1 hour with no proactive refresh mechanism. This is a fundamental blocker for any long-running GSuite workflow. No fix PR is directly paired yet, though [#4943](nearai/ironclaw PR #4943) adds optional auto-wiring.
- **LLM Retry Hang** ([#5043](nearai/ironclaw PR #5043) / [#5045](nearai/ironclaw PR #5045), OPEN) — The `NEARAI_MODEL=auto` default in the desktop app can cause the agent to hang in a retry loop for several minutes. Fix PRs are actively open.

**High:**
- **Approval Loops** ([#5060](nearai/ironclaw Issue #5060), CLOSED) — GitHub analysis workflows entered repeated approval loops and never produced results. Fixed. A related pattern persists in [#4704](nearai/ironclaw Issue #4704) (builtin.http approval loop).
- **OAuth Cancel Replay** ([#5070](nearai/ironclaw Issue #5070), CLOSED) — Canceling an OAuth prompt after passing an approval gate could replay the prompt or leave the activity in a stuck "running" state.
- **SSO Context Mismatch** ([#4992](nearai/ironclaw Issue #4992), OPEN, risk: medium) — Railway-hosted instances can create automations that fail silently before thread creation due to access token mismatch.

**Medium/Low:**
- **Dogfooding Log** ([#4879](nearai/ironclaw Issue #4879), OPEN) — Active local testing findings, suggesting the team is using their own builds heavily.
- **Channel Bugs:** Multiple open WeCom issues ([#4502](nearai/ironclaw Issue #4502), [#4505](nearai/ironclaw Issue #4505), [#4612](nearai/ironclaw Issue #4612)) covering approval reply failures and missing notifications.
- **E2E Infrastructure** ([#4108](nearai/ironclaw Issue #4108), OPEN) — Nightly full E2E suite is failing, threatening regression detection on main.

## 6. Feature Requests & Roadmap Signals

**Imminent (next release prediction):**
- **Projects Feature:** The full 5-part stack (#5015–#5019) is nearly complete. The Projects organizational layer will likely be the headline feature of the next release.
- **Automations 2.0:** Fire-once triggers ([#5065](nearai/ironclaw PR #5065), merged) + production trigger poller wiring ([#5030](nearai/ironclaw PR #5030), active) + UI redesign ([#5084](nearai/ironclaw PR #5084), active) constitutes a comprehensive revamp of the scheduled task system.
- **Auto-Approve Settings:** [#5063](nearai/ironclaw PR #5063) adds a DB-backed per-user auto-approve eligibility store, reducing friction for trusted tools.

**Mid-term signals:**
- **Concurrent Turn Execution:** [#5085](nearai/ironclaw PR #5085) suggests the team is preparing for multi-agent orchestration and higher throughput workloads.
- **Channel Expansion:** Slack generic host-ingress ([#5072](nearai/ironclaw PR #5072)) alongside the WeCom/WeChat fixes indicates a push toward broad enterprise channel support.
- **Hosted Deployment Profile:** [#5081](nearai/ironclaw PR #5081) adds an explicit `hosted-single-tenant` Reborn Postgres profile, signaling a structured SaaS deployment path.

## 7. User Feedback Summary

**Satisfaction Signals:**
- **Rapid Issue Resolution:** The community is receiving immediate attention—issue [#5078](nearai/ironclaw Issue #5078) (approval modal display problems) was opened and a fix PR ([#5082](nearai/ironclaw PR #5082)) was raised the same day.
- **Active Dogfooding:** The detailed dogfooding logs ([#4879](nearai/ironclaw Issue #4879)) indicate the team has strong internal QA practices, which typically correlates with higher release quality.

**Dissatisfaction Signals:**
- **Authentication Fragility:** The dominant user pain point is OAuth unreliability—flows that fail after success ([#4907](nearai/ironclaw Issue #4907)), tokens that expire without refresh ([#5071](nearai/ironclaw Issue #5071)), and cancel loops ([#5070](nearai/ironclaw Issue #5070)).
- **Agent Autonomy is Brittle:** Users expect agents to recover from tool failures autonomously. Issues like [#4761](nearai/ironclaw Issue #4761) and [#4704](nearai/ironclaw Issue #4704) show the current recovery mechanisms are insufficient.
- **LLM Provider Configuration Confusion:** The long-standing Qwen/Alibaba issues ([#1520](nearai/ironclaw Issue #1520), [#1012](nearai/ironclaw Issue #1012)) and the `auto` model retry hang create significant onboarding friction for non-English users and desktop app users.

## 8. Backlog Watch

**Critical — Needs Maintainer Attention:**
- **[#1520](nearai/ironclaw Issue #1520)** / **[#1012](nearai/ironclaw Issue #1012)** — Qwen/Alibaba LLM issues. **Open since March 12 and March 21.** These represent a complete barrier for users in the Alibaba Cloud ecosystem. The lack of resolution after 3+ months is the most glaring gap in the backlog.

**Infrastructure Debt:**
- **[#4108](nearai/ironclaw Issue #4108)** — Nightly E2E is failing. Open since May 27. An unreliable CI pipeline threatens confidence in automated testing and increases risk of regressions landing on main.

**Channel Integration Staleness:**
- **WeCom Issues** ([#4193](nearai/ironclaw Issue #4193), [#4500](nearai/ironclaw Issue #4500), [#4502](nearai/ironclaw Issue #4502), [#4505](nearai/ironclaw Issue #4505), [#4612](nearai/ironclaw Issue #4612)) — A cluster of 5 issues from the same QA author covering setup guidance, conversation routing, approval replies, notifications, and title legibility. These have been open for 1–3 weeks without resolution, suggesting channel-specific work is deprioritized behind core Reborn engine development.

**Umbrella Tracker:**
- **[#2800](nearai/ironclaw Issue #2800)** — Engine v2 default flip. Closed as prerequisite work is complete. The community should watch for the actual flip commit, which will be a defining moment for the project's architecture.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is a structured project digest for LobsterAI based on the GitHub activity data for 2026-06-19.

---

# LobsterAI Project Digest — 2026-06-19

## 1. Today's Overview
The project experienced a major activity spike over the past 24 hours, driven almost entirely by the culmination of the `release/2026.6.11` cycle and the release of **LobsterAI 2026.6.18**. Out of **15 updated PRs**, **14 were merged or closed**, demonstrating strong feature delivery momentum. The two key themes of this push were **Artifact sharing expansion** (now supporting Office documents, PDFs, and diagrams) and a **complete overhaul of the voice input system** to be real-time only. Community attention centered on a highly detailed feature proposal calling for the evolution of the OpenClaw subsystem into an "AI Collaborator" platform.

## 2. Releases
- **Version:** `LobsterAI 2026.6.18` (Released 2026-06-18)
  - **Major Changes:**
    - **Artifacts Expansion:** Sharing capabilities were upgraded to support multiple newly supported file types, including **Word, PPT, Excel, PDF, Markdown, and Mermaid** files (PR [#2159](https://github.com/netease-youdao/LobsterAI/pull/2159)).
    - **Artifacts Deep Dive:** Extended the artifact panel with dedicated share entry points for `markdown_file` and `mermaid_file` sources (PR [#2178](https://github.com/netease-youdao/LobsterAI/pull/2178)).
    - **Voice Input Consolidation:** The legacy short upload ASR flow and `asr:recognize` IPC surface were fully removed. Voice input now exclusively uses the real-time ASR pipeline (PR [#2160](https://github.com/netease-youdao/LobsterAI/pull/2160)).
  - **Breaking Changes / Migration Notes:**
    - **Legacy API Removal:** Any fork or plugin relying on the old file-upload ASR workflow (`asr:recognize`) will need to migrate to the websocket-based `realtimeAsrClient`.
    - **Configuration Deprecation:** The `voiceInput.recognitionMode` setting has been removed. Real-time ASR is now the only available mode.
    - **User-Facing String Changes:** All Chinese UI copy referencing "听写" (dictation) has been standardized to "语音输入" (voice input), with corresponding English changes (PR [#2177](https://github.com/netease-youdao/LobsterAI/pull/2177)).

## 3. Project Progress
The bulk of the merged activity represents the shipping of the `release/2026.6.11` branch into `main` (merged via PR [#2179](https://github.com/netease-youdao/LobsterAI/pull/2179)).

**Key Feature Advancements:**
- **Computer Use MVP:** A fully managed **Computer Use kit** for Windows x64 landed, including a built-in MCP server bridge for app/window listing, launching, screenshots, and keyboard/mouse control (PR [#2143](https://github.com/netease-youdao/LobsterAI/pull/2143)). The runtime was subsequently bumped to **1.0.7** with improved diagnostic breadcrumbs (PR [#2156](https://github.com/netease-youdao/LobsterAI/pull/2156)).
- **Realtime Voice Input:** A new real-time ASR mode was fully integrated, with WebSocket streaming, PCM audio chunking, a WAV header in the first frame, and settings UI for mode selection (PR [#2148](https://github.com/netease-youdao/LobsterAI/pull/2148)).
- **Voice Input Polish:** A new in-memory ASR quota slice was added to manage daily availability, along with UI refinements for the dictation recording experience (PR [#2163](https://github.com/netease-youdao/LobsterAI/pull/2163)).

**Stability & Refactoring:**
- **Mac Microphone Permissions:** Resolved a systemic issue where the app failed to properly request macOS microphone access by adding entitlements and a trusted media permission policy (PR [#2113](https://github.com/netease-youdao/LobsterAI/pull/2113)).
- **Duplicate Session Fix:** Fixed a race condition that could cause duplicate real-time ASR start requests (PR [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155)).
- **UI Consistency:** Fixed the Expert Suite page controls to remain sticky during scrolling, matching the behavior of Skills and MCP pages (PR [#2150](https://github.com/netease-youdao/LobsterAI/pull/2150)).

## 4. Community Hot Topics
- **Highest Engagement / Visionary Proposal:**
  **[Issue #2180](https://github.com/netease-youdao/LobsterAI/issues/2180)** — *"Build 'AI Collaborator' Form: Introduce Natural Language Command Bar and Task Dispatch Console for Cross-Model Orchestration and Project-Level Memory"*
  - **Author:** woxinsj
  - **Analysis:** This is a dense, ambitious feature request paired with a design document. The author proposes upgrading the **OpenClaw** tooling into a full-fledged **AI Collaborator** platform targeting "tech-savvy non-elite programmers." The underlying ask is clear: the community sees OpenClaw's current form as too low-level and desires a natural language interface for orchestrating multiple models and agents with persistent project memory. This is a strong signal for where power users want the roadmap to go.
- **Long-standing UX Concern:**
  **[Issue #1422](https://github.com/netease-youdao/LobsterAI/issues/1422)** — *"[stale] MCP custom page: long service names display poorly in delete dialog"*
  - **Author:** xuzx-code
  - **Analysis:** A long-standing cosmetic UI/UX issue. When custom MCP services have very long names, the delete confirmation modal does not handle text overflow. This has been open since April and was marked stale, suggesting it is low priority but remains a noticeable friction point in the administrative UI.

## 5. Bugs & Stability
- **Severity: Medium (Resolved)**
  - **MacOS Voice Input Permissions:** A blocker for users on macOS where correct microphone permissions were not granted. Fixed by adding proper `audio-input` entitlements and a trusted renderer policy (PR [#2113](https://github.com/netease-youdao/LobsterAI/pull/2113)).
  - **ASR Session Duplication:** A race condition in the Cowork voice input flow could trigger multiple simultaneous ASR connections. Fixed by preventing duplicate start requests (PR [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155)).
- **Severity: Low (Open)**
  - **MCP Delete Dialog UI Bug:** Issue [#1422](https://github.com/netease-youdao/LobsterAI/issues/1422) remains open. It is a purely visual regression in the MCP management UI where text overflows the delete confirmation dialog for long service names. No fix PR is currently linked.

## 6. Feature Requests & Roadmap Signals
- **Strongest Signal — AI Collaborator / OpenClaw Evolution:**
  Issue [#2180](https://github.com/netease-youdao/LobsterAI/issues/2180) is the most significant roadmap signal this week. The proposal for a "Natural Language Command Bar" and "Task Dispatch Console" suggests the project is reaching a maturity point where users want a higher-level abstraction layer over individual MCP tools and skills. This aligns well with the recently shipped **Computer Use MVP**.
- **Confirmed Direction — Desktop Agentic Automation:**
  The landing of the Computer Use MVP (PR [#2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) signals a strong commitment to shifting from a chat assistant to a full desktop automation agent. This is a major strategic move.
- **Prediction for Next Version:**
  Expect a stabilization phase for Computer Use (potentially adding macOS support), deeper integration of document artifacts into the Cowork context, and potentially initial UI scaffolding to address the "AI Collaborator" vision from Issue #2180.

## 7. User Feedback Summary
- **Pain Points Addressed:**
  - **Voice input latency** was a primary target. The complete removal of the upload-based ASR in favor of purely real-time streaming directly addresses the need for a faster, more fluid dictation experience.
  - **Missing document support** in the Artifacts sharing panel was a significant blocker for users wanting to share work output. The expansion to Word, PPT, Excel, PDF, Markdown, and Mermaid is a direct response to this need.
- **Persistent Pain Points:**
  - **MCP administration UI** lacks polish in edge cases (long names in dialogs), which can be frustrating for users managing complex custom server deployments.
  - The **Mac microphone permission** issue (now fixed) likely caused negative first-time user experiences for macOS users.
- **Satisfaction Indicators:**
  The high level of detail in Issue [#2180](https://github.com/netease-youdao/LobsterAI/issues/2180) indicates a very technically engaged user base that is invested in the project's architecture, not just surface features. The high throughput of 14 closed PRs in a single cycle is a strong internal health indicator.

## 8. Backlog Watch
- **🚨 High Priority (Security/Maintenance):**
  **[PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** — *"chore(deps-dev): bump the electron group across 1 directory with 2 updates"*
  - **Status:** Open since **April 2, 2026**.
  - **Risk:** This Dependabot PR proposes a major version bump of Electron (from `40.2.1` to `42.4.0`) and `electron-builder`. Open for over 2.5 months, this drift in the core runtime introduces risk regarding security patches, API deprecations, and OS compatibility. This requires immediate maintainer attention to test and merge.
- **Low Priority (UX Debt):**
  **[Issue #1422](https://github.com/netease-youdao/LobsterAI/issues/1422)** — MCP delete dialog overflow.
  - **Status:** Open since **April 3, 2026**. Marked stale.
  - **Action:** A trivial CSS fix or tooltip addition could clear this out of the backlog.
- **Engagement Opportunity (Community PR):**
  **[Issue #2180](https://github.com/netease-youdao/LobsterAI/issues/2180)** — AI Collaborator Proposal.
  - **Status:** Opened today.
  - **Action:** This is a goldmine of community-led product vision. A maintainer acknowledgment or a spin-off into a GitHub Discussion/RFC would go a long way in validating the deep investment of power users in the OpenClaw ecosystem.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest – June 19, 2026**

---

### 1. Today’s Overview
Moltis registered zero new releases and zero pull request events in the last 24 hours, indicating a hiatus in visible commit integration. The sole signal of motion was a single open bug report filed on June 18 concerning core session management. While project health remains stable, the day’s metrics suggest a consolidation or planning phase, with the immediate community pulse depending entirely on how maintainers respond to this newly surfaced blocker.

---

### 2. Releases
*No new releases were recorded for this period.*

---

### 3. Project Progress
No pull requests were merged, closed, or updated today. No new features were integrated, and no bugs were remediated via code merges during this observation window. Development activity on the public main branch appears paused or confined to internal branches.

---

### 4. Community Hot Topics
Community interaction is narrow today, concentrated on a single issue:

- **[Bug] "main" session can't be deleted/archived (#1132)** – [View Issue](https://github.com/moltis-org/moltis/issues/1132)
  - Filed by *vvuk*, this item represents the entirety of today’s community signals (0 comments, 0 reactions so far). The lack of replies suggests it was very recently reported or the community is currently low-signal. Nevertheless, the underlying need is clear: users expect full lifecycle control over all sessions, including system defaults. The inability to delete/archive the primary session creates a significant UX friction point for workspace maintenance and data hygiene.

---

### 5. Bugs & Stability

- **Active Bug (Severity: Medium–High)** – [Issue #1132](https://github.com/moltis-org/moltis/issues/1132)
  - **Description:** The default “main” session cannot be deleted or archived. The reporter confirmed they are on the latest version.
  - **Impact:** This blocks users from performing basic data lifecycle tasks (cleaning up clutter, archiving old context, resetting state). For a local-first AI assistant, inability to purge a primary session can raise both usability and data privacy concerns.
  - **Fix Status:** No associated fix PR exists yet. Maintainers need to determine whether this is an intentional guard (to preserve user context) or a missing implementation for the default session.

---

### 6. Feature Requests & Roadmap Signals

- **Implicit Feature Signal – Full Session CRUD**
  The bug report acts as a strong roadmap indicator. Users increasingly expect to treat all sessions—including the “main” session—as first-class deletable/archivable entities. The next Moltis iteration will likely need to introduce:
  - An override mechanism for removing the default session.
  - A dedicated archive system to preserve history without deleting it.
  - Perhaps a redesign of the session sidebar that removes special privileges from the “main” label.

---

### 7. User Feedback Summary

- **Pain Point Highlighted:** Users feel trapped in the default session with no escape hatch to clean up or migrate data. This is a concrete friction point for daily power users.
- **Reporter Profile:** The reporter completed the full preflight checklist, indicating an experienced, conscientious user who exhausted search before filing. This suggests genuine frustration rather than a novice misunderstanding.
- **Satisfaction Level:** The report itself signals dissatisfaction with the current restriction. No positive feedback surfaced in the 24-hour window.

---

### 8. Backlog Watch
No long-abandoned issues or stale PRs were identified within the 24-hour data window. However, **Issue #1132** must be actively triaged soon to prevent it from slipping into backlog purgatory. If left unaddressed, this specific blocker could generate disproportionate negative sentiment, as the inability to control the default session is a highly visible and repeatable pain point for every user.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured **CoPaw Project Digest** for **2026-06-19**, based on the provided QwenPaw repository data.

---

## 1. Today's Overview
CoPaw (the QwenPaw repository) exhibits very high activity today with **44 issues** and **28 PRs** updated, alongside a minor patch release (**v1.1.12.post1**). The project health is mixed: while the community contribution pipeline is robust (multiple new-feature PRs from first-time contributors and a large test suite), user sentiment is weighted by **critical context management stability issues** that cause data loss and process freezes. The maintainers are actively merging fixes for Windows/network platform parity, but the core compaction engine remains the primary source of severe regressions.

## 2. Releases
A new patch release **v1.1.12.post1** was published. No breaking changes or migration steps were documented.
- **Fixes:**
  - Corrected prerelease script argument expansion ([#5288](https://github.com/agentscope-ai/QwenPaw/pull/5288)).
  - Renamed the ChromaDB probe collection to `'probe-test'` to resolve naming conflicts ([#5288](https://github.com/agentscope-ai/QwenPaw/pull/5288)).

## 3. Project Progress
Several significant features, fixes, and infrastructure improvements were merged or closed today:
- **Plugin Ecosystem:** Merged plugin uninstall hooks and skill provider API exposure ([#4794](https://github.com/agentscope-ai/QwenPaw/pull/4794), [#5008](https://github.com/agentscope-ai/QwenPaw/pull/5008)).
- **MCP Performance:** Merged `SharedMCPPool` to prevent server process explosion when scaling to hundreds of agents on Windows ([#4849](https://github.com/agentscope-ai/QwenPaw/pull/4849)).
- **Windows Stability:** Fixed SSL certificate handling for DingTalk/`uv` installs and general Windows certificate store errors ([#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291), [#5298](https://github.com/agentscope-ai/QwenPaw/issues/5298)). Also merged cleanup of stale ghost skill directories on Windows ([#4860](https://github.com/agentscope-ai/QwenPaw/pull/4860)).
- **Context Architecture:** Migrated from the custom `LightContextManager` to AgentScope 2.0's native compression protocol ([#5309](https://github.com/agentscope-ai/QwenPaw/pull/5309)).
- **UI/UX Accuracy:** Fixed the Web chat context usage indicator to correctly use the active model's `max_input_length` ([#5303](https://github.com/agentscope-ai/QwenPaw/pull/5303)).
- **Testing:** Integrated a comprehensive Sprint 3 test suite covering ACP runner, plugins, and security ([#5270](https://github.com/agentscope-ai/QwenPaw/pull/5270)).

## 4. Community Hot Topics
The most active discussions reveal a community deeply concerned with stability and eager for advanced compression alternatives:
- **Process Freeze on Compaction** ([#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218), 16 comments): Top concern. A sub-agent triggering context compaction freezes the entire QwenPaw process, requiring a manual restart.
- **Context Data Loss on Compaction** ([#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171), 8 comments): Users report the compaction algorithm wiping the entire context profile when character profiles exceed token thresholds, breaking tasks entirely.
- **Persistent Skill Reset on Upgrade** ([#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262), 7 comments): A recurrent pain point where disabling built-in skills resets to enabled after every version upgrade.
- **Headroom Compression Integration** ([#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063), 7 comments, with PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244)): High demand for an optional 60–95% token reduction layer.
- **Channel Routing Bug** ([#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264), 4 comments): A nuanced Feishu bug where group chat replies are incorrectly routed to a user's private chat if a private session exists.

## 5. Bugs & Stability
Stability is fragile, with context management issues dominating the severity rankings:

- **CRITICAL: Process Freeze (#5218)**: Compaction in sub-agents causes total unresponsiveness. No dedicated fix PR has been merged. (Risk: Data loss/corruption due to force-kill).
- **CRITICAL: Context Data Loss (#5171)**: Compaction can reduce context to zero. PR [#5287](https://github.com/agentscope-ai/QwenPaw/pull/5287) (crash fix on maxLength) addresses a symptom but not the root cause.
- **HIGH: Message Routing (#5264)**: Incorrect group vs. private routing on Feishu. Impacts enterprise channel reliability.
- **MEDIUM: Platform SSL/Config Regressions (#5237, #5317)**: `uv` installs breaking DingTalk; Tauri builds losing Python path. Addressed by today's fixes ([#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291), [#5298](https://github.com/agentscope-ai/QwenPaw/pull/5298)).
- **MEDIUM: Broken File Preview (#5140 / #5320, PR #5324)**: A regression in v1.1.12 from the FileResponse refactor. New PR [#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324) provides an inline content-disposition fix.

## 6. Feature Requests & Roadmap Signals
The roadmap is clearly pivoting toward offering **multiple context management strategies** and **operational tooling**:

- **In Development (Context Alternatives):**
  - **Headroom Integration** ([PR #5244](https://github.com/agentscope-ai/QwenPaw/pull/5244)): Reversible compression layer (60–95% savings). Voting and activity suggest this is a high-priority merge.
  - **Scroll Context Manager** ([PR #5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)): A retrieval-driven alternative to native compression, submitted as a first-time contribution.
- **In Development (Tooling & Automation):**
  - **Terminal Coding Mode** ([PR #5304](https://github.com/agentscope-ai/QwenPaw/pull/5304)): Interactive coding REPL connecting to the daemon.
  - **Native TodoWrite Panel** ([PR #5323](https://github.com/agentscope-ai/QwenPaw/pull/5323)): Real-time plan execution progress UI.
  - **Bubblewrap Sandbox** ([PR #5310](https://github.com/agentscope-ai/QwenPaw/pull/5310)): Linux kernel-level sandboxing for code execution.
- **Roadmap Predictions (Next Minor Version):** Given the volume of PRs and community pain, **v1.2.0** will likely feature a revamped context management system (migration in [#5309](https://github.com/agentscope-ai/QwenPaw/pull/5309) + optional Headroom/Scroll plugins) and the new terminal coding mode.

## 7. User Feedback Summary
- **Dissatisfaction:** Users are experiencing significant frustration with **update regressions** (disabling skills, breaking downloads) and **data integrity threats**. A lack of graceful error handling in the context engine forces users to hard-kill processes.
- **Use Cases:** Power users are operating complex multi-agent teams (triggering sub-agent bugs), relying heavily on file I/O, and demanding secure channel operations (DingTalk, Feishu).
- **Satisfaction Signals:** Despite stability issues, the community remains highly engaged. The quality of bug reports is high (complete with logs and configs), and the influx of **first-time contributor PRs** (Scroll, Headroom, Bubblewrap, DataPaw) suggests a healthy, invested developer base that believes in the project's potential.

## 8. Backlog Watch
The following items require maintainer attention to avoid blocking the community:

- **PR [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) (DataPaw Plugin)**: Awaiting review for **28 days**. A major contribution adding 12 BI skills.
- **PR [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) (Plugin Loader Decoupling)**: Open for **17 days**. Blocks all plugin functionality in PyInstaller/Tauri frozen environments (a critical bug for desktop users).
- **Issue [#3940](https://github.com/agentscope-ai/QwenPaw/issues/3940) (Vision Model Routing)**: Unanswered for **2 months**. A long-standing UX gap requiring architectural decision.
- **Issue [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) (Skill Reset on Upgrade)**: Persistent across multiple versions ([#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807)). The fix appears non-trivial and keeps users on a treadmill of re-configuration.
- **Issue [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) (Process Freeze)**: The most upvoted open bug. Needs a dedicated assignment or explicit workaround communication to reassure the community.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-06-19

## 1. Today's Overview

ZeroClaw is in an intense stabilization and rapid iteration cycle following the **v0.8.1 patch release**, with **50 Issues** and **50 PRs** updated in the last 24 hours. Activity is bifurcated: a high-volume bug-fix sprint targeting v0.8.x regressions runs in parallel with foundational architecture work for **v0.9.0** (OIDC auth, route-layer middleware, per-principal security). The maintainer team (Audacity88, Nillth, mazhuima) is processing an exceptional throughput of reviews, indicating healthy project governance. While the project is effectively addressing regressions, a cluster of **P1 provider-compatibility bugs** (Gemini, Anthropic, vision pipeline) remains the primary risk to user experience.

---

## 2. Releases

### **v0.8.1** *(First patch on v0.8.x line)*
- **Scope:** Stabilization of the multi-agent runtime, channel orchestration, and provider stack that landed in v0.8.0.
- **Scale:** 207 commits from 45 contributors — **123 bug fixes**, 46 new features.
- **Health Signal:** Rapid patch release (short gap after v0.8.0) demonstrates responsive maintainer triage and strong community contributor velocity. No breaking changes or migration steps flagged in the release body.

---

## 3. Project Progress

### Merged/Closed PRs (2026-06-19)
- **#7953** *(Cost capture)* – Model cost is now tracked for RPC/zerocode-TUI and standalone ACP turns, closing the long-standing cost-observability gap (#5221).
- **#6970** *(Tracker)* – The v0.8.1 integration/channel/provider/tool queue tracker closed, signaling that all targeted integration work for the patch is complete.

### Features and Fixes Advancing Through Pipeline
- **Discord Interaction Surfaces (Epic B, #7965):** Nillth's large PR adds buttons, selects, modals, slash autocomplete, and buttoned tool-approval — transforming Discord from a basic text channel into a full interactive surface.
- **Authentication Groundwork:** PR #7945 (legokichi) adds first-class xAI/Grok OAuth login with PKCE and device-code flow. The OIDC tracking issue #7141 continues to coordinate the v0.9.0 pluggable auth architecture.
- **Platform Expansion:** PR #7956 (Audacity88) introduces Windows-portable test fixtures, laying the groundwork for first-class Windows CI coverage.
- **Tool-Security Hardening:** PR #7960 gates `execute_pipeline` sub-tool execution behind per-agent `ToolAccessPolicy`, closing a bypass that allowed restricted agents to run arbitrary tools.

---

## 4. Community Hot Topics

### Most Active Discussions (by comment count)

- **#5844 – Memory Emphasis Overriding Prompts** *(6 comments)*
  A high-traffic P1 bug where the system prompt weighs long-term memory too heavily against the current instruction. Users report cron jobs ignoring immediate directives because history dominates context. Link: [Issue #5844](zeroclaw-labs/zeroclaw Issue #5844)

- **#7141 – OIDC Authentication Provider** *(5 comments)*
  The tracking umbrella for pluggable authentication in v0.9.0. Community interest is high; this represents a major enterprise readiness milestone. Link: [Issue #7141](zeroclaw-labs/zeroclaw Issue #7141)

- **#6067 – Channel Reply-Intent Precheck Config** *(5 comments)*
  Users want the reply-intent classifier to use a fast, configurable model with a hard timeout instead of blocking the main agent turn. Link: [Issue #6067](zeroclaw-labs/zeroclaw Issue #6067)

- **#6002 – Telegram Assistant Identification** *(5 comments)*
  Users report Telegram messages are not clearly addressed to the assistant, causing context confusion when ZeroClaw reads incoming messages alongside other bot traffic. Link: [Issue #6002](zeroclaw-labs/zeroclaw Issue #6002)

- **#6302 – Gemini 400 History Violation** *(4 comments)*
  A strict API invariant breaks ZeroClaw on Gemini: the history serializer emits an assistant `tool_call` before any user turn, triggering a hard 400 rejection. Link: [Issue #6302](zeroclaw-labs/zeroclaw Issue #6302)

### Most Reacted

- **#4467 – MCP Resource and Prompt Support** *(4 👍)*
  This long-standing enhancement request has high community visibility. Users want ZeroClaw to expose MCP resources and prompts, not just tools, to the agent. Link: [Issue #4467](zeroclaw-labs/zeroclaw Issue #4467)

---

## 5. Bugs & Stability

### New Bugs (Filed 2026-06-19)
- **#7964 (S2 – Degraded Behavior):** `context_compression.summary_model` is configured as a bare model ID without provider binding. When the summary model provider differs from the agent's primary provider, compression silently fails, causing runtime failures on reachable configs. Link: [Issue #7964](zeroclaw-labs/zeroclaw Issue #7964)

### Active P1 Bugs (Updated Today)
| Issue | Component | Severity | Status |
|-------|-----------|----------|--------|
| **#6302** – Gemini 400 history invariant | Provider | S1 (Blocked) | Accepted |
| **#5808** – Default 32k context exceeded on iteration 1 | Config/Runtime | S1 (Blocked) | Accepted |
| **#6037** – Cron jobs launched repeatedly during long runs | Cron/Runtime | S1 (Blocked) | Accepted |
| **#6434** – Shell tool refused at full autonomy | Tool/Security | S1 (Blocked) | In Progress |
| **#6350** – WhatsApp allowed-numbers bypass for LID contacts | Channel | S2 (Degraded) | In Progress |
| **#7756** – MCP tools unavailable on OpenAI Responses/Anthropic | Provider | S1 (Blocked) | Accepted |
| **#6841** – Vision provider silently ignored | Provider | S1 (Blocked) | Accepted |
| **#5869** – RUSTSEC dependency lock (rumqttc TLS) | Security/Deps | S1 (Blocked) | **Blocked** |

### Fix PRs in Active Review
- **#7961** – Anthropic tool schema cleaning (`$ref`/`$defs` in `input_schema`)
- **#7960** – Pipeline tool access policy bypass
- **#7959** – Auto-approved tools blocked at non-Full autonomy on channels
- **#7958** – Telegram `mention_only` gate failing for bot replies
- **#7909** – Groq native tool calling rejects missing `name` field
- **#7908** – WebDriver browser snapshot returns null
- **#7847** – Session persistence race condition (concurrent history writes)
- **#7940** – Agent rename persistence ordering (owned state moved before config write)
- **#7957** – Agent turn costs not persisted through daemon RPC

---

## 6. Feature Requests & Roadmap Signals

### v0.9.0 Horizon (Breaking Changes Expected)
- **#7432** – Auth, security, gateway, and breaking-change tracker
- **#7141** – OIDC authentication provider (pluggable, route-layer middleware)
- **#6250** – Extract `require_auth` from per-handler convention to `Router::route_layer`

### v0.8.x Evolution (Likely v0.8.2 / v0.8.3)
- **#4467 – MCP Resource & Prompt Support** *(Help Wanted, High Interest)*
  A critical feature gap for MCP parity. Comment volume and reactions suggest strong user demand.
- **#7320 – MCP Dashboard & Web/Plugin-Management Surfaces** *(v0.8.3 Tracker)*
  A dedicated web surface for managing MCP servers is on the immediate roadmap.
- **#7881 – Provider Fallback Circuit Breakers**
  Repeated failing providers can be temporarily skipped instead of retried.
- **#7875 – RunPod/ComfyUI Image Generation**
  Opt-in image gen provider with provider-scoped config.
- **#7891 – Signal Media Attachment Support**
- **#7886 – Telegram Per-Channel Inbound Debounce**

### Prediction
The next patch series (v0.8.2) will absorb the wave of P1 provider-compatibility fixes, ship the Discord interactions epic, and potentially land the xAI OAuth integration. v0.8.3 is already tracked for MCP dashboards. v0.9.0 is shaping up as a **security/auth breaking-release** that will restructure the gateway layer.

---

## 7. User Feedback Summary

### Pain Points (Explicitly Reported)
- **Memory Over-Prioritization (#5844):** "System prompt should give less priority to the memories and more to the current prompt." – *databillm*
- **Context Budget Misconfiguration (#5808):** "Default 32k context budget is exceeded by system prompt + tool definitions on iteration 1." – *JordanTheJet*
- **Telegram UX Friction (#5514, #6002):** Multi-image messages cause the agent to process each image as a separate request, and the assistant identity is not clearly communicated to the AI.
- **Cron Usability Gap (#6037, #7762):** Jobs fire in bursts if they run longer than the poll interval, and documentation is entirely missing. Users cannot assign a specific model to a cron task.
- **Observability Gaps (#4721, #5221):** Logging to stdout breaks CLI piping (`zeroclaw config schema` includes log noise). Cost tracking was missing for non-API pathways (now fixed in #7953).

### Signals of Satisfaction
- The v0.8.1 release contributed by **45 different developers** indicates a healthy, engaged contributor base.
- High PR throughput with maintainers handling large, complex changes (e.g., Nillth's 3+ PRs pushing major Discord and dashboard features).
- The project's rapid patch cycle shows that reported regressions are prioritized and addressed within days.

---

## 8. Backlog Watch

Items requiring maintainer attention or community coordination:

- **#4467 – MCP Resource & Prompt Support** *(Filed 2026-03-24, 4 👍, Accepted)*
  A heavily requested feature that periodically resurfaces in comments. It requires deep architectural changes to the MCP client crate. While it fell out of v0.8.x, it remains the #1 blocker for power users integrating with complex MCP servers.

- **#4721 – Log to stderr Instead of stdout** *(Filed 2026-03-26, Accepted, Needs Author Action)*
  A simple P2 CL1 hygiene issue that has been accepted for months but lacks a PR. It continues to create friction for any user scripting the ZeroClaw CLI.

- **#5869 – RUSTSEC Advisory Cluster (rumqttc TLS Stack)** *(Filed 2026-04-18, P1, Blocked)*
  This P1 security advisory is entirely blocked on an upstream `rumqttc` release pinning newer `rustls-webpki`. If the upstream crate does not release soon, ZeroClaw will need to evaluate switching MQTT clients or vendoring a patched dependency. This is a material CI/CD pipeline risk (`cargo deny`).

- **#7108 – CI Critical Path Optimization** *(Filed 2026-06-02, In Progress)*
  Identified by maintainer Audacity88 as a 15–20 minute friction point for PR CI. This directly impacts contributor velocity. The issue has an active design but no merged implementation yet.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*