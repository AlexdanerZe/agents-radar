# OpenClaw Ecosystem Digest 2026-06-02

> Issues: 459 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-02 03:39 UTC

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

Here is the project digest for OpenClaw based on the activity snapshot from 2026-06-02.

---

## OpenClaw Project Digest — 2026-06-02

### 1. Today’s Overview
Activity is very high as the project pushes toward a stable **v2026.6.1**. Across **459 updated Issues** (277 open) and **500 updated PRs** (106 merged/closed), the team released **two new betas** in a single day. The dominant theme remains the stabilization of the **Codex runtime migration**, with several high-priority regression fixes, fallback logic improvements, and channel delivery reliability patches in flight. Community engagement is strong, with users filing detailed regression reports and feature requests, though the rapid iteration around Codex is generating some friction.

### 2. Releases
Two beta versions were published today:
- **v2026.6.1-beta.2**: Improves recovery for agents and CLI-backed runtimes from interrupted tool calls, stale session bindings, and media delivery retries. Channel delivery is steadier across **Telegram, WhatsApp, and iMe**.
- **v2026.6.1-beta.1**: Shares identical highlights but lists a slightly broader set of channels, including **iMessage** and **Slack** in the stabilization list.

Both releases are strictly bug-fix and stability focused. No breaking changes or migration notes were issued.

### 3. Project Progress
Today saw **106 merged/closed PRs**, signaling an aggressive cleanup cycle. Notable advances include:
- **Doctor CLI fixes**: Two separate PRs ([#89308](https://github.com/openclaw/openclaw/pull/89308), [#89260](https://github.com/openclaw/openclaw/pull/89260)) improved platform detection to stop counting macOS-only skills as broken Windows installs.
- **Auth stability**: [#89305](https://github.com/openclaw/openclaw/pull/89305) bypasses stale provider auth cooldowns for plugin harnesses, preventing false negatives.
- **Message de-duplication**: Multiple PRs ([#89299](https://github.com/openclaw/openclaw/pull/89299), [#89109](https://github.com/openclaw/openclaw/pull/89109)) target volatile message IDs to stop spam loops and duplicate tool calls.
- **Hook system expansion**: [#89152](https://github.com/openclaw/openclaw/pull/89152) and [#89154](https://github.com/openclaw/openclaw/pull/89154) add `agent:turn:end` and `agent:turn:transcript:save` lifecycle hooks, signaling a deepening of the SDK’s event layer.
- **Runtime compatibility**: [#88906](https://github.com/openclaw/openclaw/pull/88906) allows `Codex Spark` through the Codex harness route, while [#89290](https://github.com/openclaw/openclaw/pull/89290) keeps Codex waiting during long reasoning tokens to prevent premature timeouts.

### 4. Community Hot Topics
The most active discussions revolve around the **Codex transition** and **channel-specific regressions**:
- **Codex-vs-Pi Runtime Parity** ([#80171](https://github.com/openclaw/openclaw/issues/80171), 15 comments, closed): The formal tracking issue is closed, but the pain lingers across multiple open bugs.
- **Gemini 3.1 Flash-Lite GA** ([#80380](https://github.com/openclaw/openclaw/issues/80380), 14 comments, 4 👍): The community is eager for the migration from preview to the stable Gemini model.
- **SQLite Migration Strategy** ([#88838](https://github.com/openclaw/openclaw/issues/88838), 12 comments): This maintainer-led issue uses a branch-by-abstraction method to move session state to SQLite. It is closely watched as a sign of future stability.
- **MCP Tool Consent Envelope** ([#78308](https://github.com/openclaw/openclaw/issues/78308), 11 comments, 1 👍): A long-running feature request to allow MCP tools to use the channel-mediated approval pipeline. It remains in limbo waiting for a product decision.
- **Telegram Guest & Bot-to-Bot Modes** ([#79077](https://github.com/openclaw/openclaw/issues/79077), 7 comments, 7 👍): The most liked feature request, tracking Telegram’s latest platform features. This is a clear community priority.

### 5. Bugs & Stability
Stability is the story of this digest. Severity ranked:

- **P1 Regression – Codex Turn-Completion Stall** ([#88312](https://github.com/openclaw/openclaw/issues/88312), 8 comments, 2 👍): A multi-tool agent turn reliably stalls with “Codex stopped before confirming the turn was complete”. This is a regression of a previously fixed issue (#84076 / #85107). **Fix PR:** [#89290](https://github.com/openclaw/openclaw/pull/89290) (treats raw reasoning as progress status).
- **P1 Regression – Message Duplication (Telegram/Feishu)** ([#86519](https://github.com/openclaw/openclaw/issues/86519), 9 comments): Agents repeating identical replies 2-10x after the 2026.5.20 update. **Fix PRs:** [#89299](https://github.com/openclaw/openclaw/pull/89299), [#89109](https://github.com/openclaw/openclaw/pull/89109).
- **P1 – Codex OAuth Refresh Wedging** ([#86215](https://github.com/openclaw/openclaw/issues/86215), 4 comments): Users report agents can be stuck for hours without clear alerting. No immediate fix PR linked.
- **P2 – Webchat Prompt Cache Destruction** ([#89139](https://github.com/openclaw/openclaw/issues/89139), 4 comments): Each message spawns a new agent run, dropping the cache hit rate from 93% to 29%. Highly impactful for web UI users.
- **P2 – Control UI Workboard Data Loss** ([#88592](https://github.com/openclaw/openclaw/issues/88592), 4 comments): Card settings fail to persist, and drag-and-drop to "running" is broken.

Other notable regressions include **Cron MiniMax 503 errors** ([#85888](https://github.com/openclaw/openclaw/issues/85888)) and **Feishu dispatch crashes** ([#88234](https://github.com/openclaw/openclaw/issues/88234)).

### 6. Feature Requests & Roadmap Signals
- **Local Providers as First-Class Citizens** ([#89265](https://github.com/openclaw/openclaw/issues/89265), 4 comments, 1 👍): A new request arguing that as open-weight models improve, local inference should get equal treatment. This signals a strong user push for cost control and privacy.
- **Plugin Hot-Reload** ([#14438](https://github.com/openclaw/openclaw/issues/14438), 4 comments, 4 👍): A long-standing request to avoid container restarts during plugin development. Now over 4 months old, it is a clear pain point for the developer community.
- **In-Flight Feature: Telegram Interleaved Progress Lane** ([PR #87072](https://github.com/openclaw/openclaw/pull/87072)): A large PR adding an opt-in reasoning lane to Telegram. This, combined with other Telegram fixes, suggests a Telegram experience refresh is near completion.

Given the pace of betas, v2026.6.1 stable is likely imminent, primarily focused on **Codex reliability, message deduplication, and platform-specific bug squashing**.

### 7. User Feedback Summary
**Satisfaction Drivers:**
- Users appreciate the transparent tracking of the SQLite migration (#88838) and the rapid release cycle (2 betas in 24h).
- The community is highly technical, providing excellent reproduction steps and logs for regressions.

**Primary Pain Points:**
- **Codex Migration Fatigue**: Multiple users reported identical issues ("Codex stopped before confirming turn complete") across different channels (Telegram, CLI). The regression pattern (#88312) indicates systemic fragility in the turn-watch loop.
- **Data Integrity**: Duplicate messages and lost settings in the Control UI are eroding trust, though the maintainers are actively patching the duplication issues.
- **Diagnostic Tool Reliability**: The `doctor --fix` command was reported to silently migrate configs and cause 3-4x token inflation ([#84038](https://github.com/openclaw/openclaw/issues/84038)), a significant user trust incident.

### 8. Backlog Watch
Several high-value, long-standing items remain in the queue without firm forward momentum:

- **Channel-Mediated MCP Approval** ([#78308](https://github.com/openclaw/openclaw/issues/78308)): P2, waiting on a product decision for 27 days. This is a key security feature.
- **Multi-Agent Collaboration RFC** ([#35203](https://github.com/openclaw/openclaw/issues/35203)): Open for 3 months. Requires security review and product decision. The complexity is high, but it remains the most ambitious roadmap signal.
- **Codex OAuth Refresh Wedging** ([#86215](https://github.com/openclaw/openclaw/issues/86215)): P1, needs live repro and maintainer review. Wedged agents are a critical reliability gap.
- **Cron Jobs + MiniMax 503** ([#85888](https://github.com/openclaw/openclaw/issues/85888)): P2, fix shape clear, queueable. Has a linked PR but lacks maintainer review.
- **i18n for Slash Commands** ([#79458](https://github.com/openclaw/openclaw/issues/79458)): P3, 1 👍. Chinese-speaking users have requested this for 25 days. It requires a source repro and product decision.

Overall, the project is in a **highly active stabilization sprint**. The maintainer team is responsive to regressions but is balancing a heavy workload across the Codex integration, SDK expansion, and community feature requests.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report structured as requested.

---

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date:** 2026-06-02 | **Prepared by:** Ecosystem Senior Analyst

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem is currently in a high-tension equilibrium between breakneck feature velocity and production stability. Projects are transitioning from chat-first interfaces to complex autonomous reasoning systems, confronting shared challenges in provider reliability, message deduplication, and multi-agent orchestration. The space is bifurcated between massive reference implementations (OpenClaw) driving ecosystem coordination and a second tier of highly opinionated projects carving niches in enterprise security, local-first inference, and Asian market integration. The dominant theme across all active projects is **cost optimization through prompt efficiency** and **architectural hardening against provider churn**.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed | Releases (24h) | Momentum Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 459 | 500 | 106 | 2 betas | Stabilization Sprint (Scale Leader) |
| **Hermes Agent** | 50 | 50 | 14 | None | Refactoring & Regression Defense |
| **ZeroClaw** | 36 | 37 | 13 | None | Security & Hardening Cycle |
| **NanoBot** | 29 | 33 | 17 | v0.2.1 | High-Velocity Feature Iteration |
| **LobsterAI** | 0 | 50 | 50 | v2026.6.1 | Release Day Execution |
| **CoPaw (QwenPaw)** | 50 | 37 | ~10 | 2 releases | Release & Regression Turbulence |
| **IronClaw** | ~6 | 47 | 32 | None | Reborn Integration Wave |
| **PicoClaw** | 7 | 11 | 5 | 1 nightly | Balanced Feature/Bugfix Cycle |
| **ZeptoClaw** | 2 | 18 | 17 | None | CI & Infrastructure Hardening |
| **Moltis** | 0 | 3 | 3 | None | Architecture Refinement |
| **NanoClaw** | 3 | 6 | 1 | None | Deep Stability Fixes |
| **NullClaw** | 0 | 1 | 0 | None | Stasis / Low Activity |
| **TinyClaw** | 0 | 0 | 0 | None | Inactive |

---

## 3. OpenClaw's Position

OpenClaw holds a commanding but measured lead as the ecosystem's reference implementation and community trust anchor.

**Key Advantages:**
- **Scale Leverage:** At 459 issues and 500 PRs updated daily, OpenClaw operates at a scale roughly **10x the next tier** of projects (Hermes, ZeroClaw). This provides immense testing coverage, rapid edge-case discovery, and the deepest contributor pool.
- **Conservative Maturity:** OpenClaw’s architectural approach (branch-by-abstraction for SQLite, dual beta release gates, formal hook system expansion) signals a production-first governance style. This contrasts with the more aggressive rewrite cycles seen in IronClaw (Reborn) or NanoBot (rapid v0.x churn).
- **Community Size:** The raw issue volume is the strongest proxy for market share; no other project approaches this level of community interdependence.

**Technical Approach vs. Peers:**
- While Hermes Agent optimizes for DevOps workflows (Kanban, cron, local dflash) and ZeroClaw builds a strict enterprise permission model, OpenClaw functions as the **SDK and protocol layer**. Its investment in lifecycle hooks (`agent:turn:end`, `agent:turn:transcript:save`) indicates a strategy of enabling higher-level orchestration rather than building it in-house.
- **Vulnerability:** The Codex runtime migration is causing systemic regression fatigue. Multiple P1 issues (turn-completion stalls, message duplication) are creating trust friction that faster-moving projects like NanoBot or LobsterAI can exploit by offering simpler, more reliable abstractions.

---

## 4. Shared Technical Focus Areas

Several cross-project requirements are crystallizing across the ecosystem:

1. **Provider Compatibility Stability**
   - **Projects:** OpenClaw, Hermes Agent, ZeroClaw, PicoClaw, NanoBot, Moltis
   - **Needs:** Handling OpenAI Codex, Bedrock deprecated parameters, Claude Sonnet ID formatting, Gemini history invariants, Kimi temperature bans, Mimo XML leakage.
   - **Trend:** Moving from heuristic provider detection to explicit capability policy registries (Moltis PR #1090, ZeroClaw WASI plugins).

2. **Message Delivery & Deduplication**
   - **Projects:** OpenClaw, Hermes Agent, ZeroClaw, NanoBot, NanoClaw
   - **Needs:** Eliminating duplicate agent replies (2-10x), orphaned tool results, silent drops in Discord/Telegram, 30-minute session freezes on hung MCP calls.
   - **Trend:** The community tolerance for message loss or duplication is approaching zero; reliability is now a table-stakes differentiator.

3. **Prompt Cost & Token Minimization**
   - **Projects:** Hermes Agent, ZeroClaw, PicoClaw, NanoBot, OpenClaw
   - **Needs:** Skill catalog injection reduction, heartbeat call elimination, shared tokenizer pre-warming, context compression without data loss.
   - **Trend:** Token consumption is the #1 pain point for heavy users. Projects failing to provide cost observability (Hermes community built a custom dashboard) are leaving money on the table.

4. **Platform Expansion (Asian Market)**
   - **Projects:** NanoBot, CoPaw, PicoClaw, IronClaw, LobsterAI
   - **Needs:** Feishu, DingTalk, QQ (Napcat), Server酱³ SC3Bot, Volcengine search, MiMo models, Qwen ecosystem.
   - **Trend:** Narrowing the parity gap between Western (Telegram, Discord, Slack) and Asian messaging platforms is a clear roadmap priority for roughly 40% of the active ecosystem.

5. **Security as Core Infrastructure**
   - **Projects:** ZeroClaw, OpenClaw, PicoClaw, Hermes Agent
   - **Needs:** Tool allowlist bypass patching, guardCommand overblocking, MCP consent envelopes, channel-mediated approvals.
   - **Trend:** ZeroClaw’s rapid response to a permission bypass (<24h fix) is setting a new baseline expectation for security patching cadence.

---

## 5. Differentiation Analysis

| Project | Core Identity | Target User | Architecture Signal |
|---|---|---|---|
| **OpenClaw** | Reference SDK & Protocol | Platform builders, integrators | Hook-driven, conservative migrations |
| **Hermes Agent** | DevOps Agent Workstation | Power users, developers | CLI-heavy, Kanban, local dflash, Cron |
| **ZeroClaw** | Enterprise Secure Agent | Security teams, enterprises | WASI plugins, strict RBAC, lean defaults |
| **NanoBot** | Web-First General Agent | Hobbyists, casual power users | Rich WebUI, broad channels, rapid v0.x |
| **LobsterAI** | Platform / App Store | Users wanting plugin marketplaces | Expert Kit Store, npm/clawhub, polished UX |
| **IronClaw** | Blockchain-Native Agent | Web3 developers | TEE, Agent NFTs, Reborn (stateless) |
| **PicoClaw** | Lightweight Embedded Agent | Hardware enthusiasts, self-hosters | RISC-V support, tiny footprint, multi-arch |
| **CoPaw (QwenPaw)** | Alibaba Ecosystem Agent | Asian developer market | AgentScope runtime, Qwen models, MiMo |
| **Moltis** | Provider Abstraction Engine | Developers integrating custom backends | Explicit capability policies, clean API |
| **ZeptoClaw** | Compiled / Performant Agent | Performance-sensitive constrained envs | Rust, 6.98MB binary, strict CI |
| **NanoClaw** | Recovery & Stability Specialist | Users needing session resilience | Focus on crash-loop recovery, MCP timeouts |
| **NullClaw** | Minimalist Utility | Niche Telegram users | Single maintainer, low surface area |

---

## 6. Community Momentum & Maturity

**Tier 1 – Pioneer (Extreme Scale & Influence)**
- **OpenClaw** — The undeniable center of gravity. Its release cadence and regression response set the tempo for the entire ecosystem.

**Tier 2 – Hypergrowth (High Velocity, High Engagement)**
- **Hermes Agent**, **ZeroClaw**, **NanoBot**, **LobsterAI**, **IronClaw**, **CoPaw**
- These projects represent the competitive frontier. Hermes and ZeroClaw are pulling ahead in architecture maturity (Kanban, WASI), while NanoBot and LobsterAI are winning on delivery velocity and user experience polish. IronClaw is executing a high-risk, high-reward rewrite. CoPaw is managing the growing pains of rapid adoption.

**Tier 3 – Stabilization (Moderate Velocity, Deep Hardening)**
- **PicoClaw**, **ZeptoClaw**, **Moltis**, **NanoClaw**
- These projects are trading feature surface area for deep maturity in specific domains (embedded systems, pure performance, provider abstraction, session resilience). They are well-positioned to serve specialized, high-retention niches.

**Tier 4 – Long Tail (Low Activity / Dormant)**
- **NullClaw**, **TinyClaw**
- No roadmap momentum. Risk of ecosystem irrelevance without a strategic pivot or renewed maintainer engagement.

---

## 7. Trend Signals

1. **Cost Efficiency is the New Performance Metric**
   - The community's detailed token overhead analysis (Hermes #4379) and heavy investment in skill compilation (ZeroClaw #5146) signal that **operating cost is now the primary differentiator**. Projects that minimize per-turn token burn will dominate the self-hosted segment.

2. **The Great Provider Abstraction**
   - The shift from brittle URL/heuristic detection to **explicit capability registries** (Moltis, ZeroClaw, OpenClaw hooks) is the most important architectural trend. This abstraction layer is becoming the "operating system" for AI agents, decoupling core logic from any single LLM provider.

3. **From Chat to Autonomous Workflow**
   - Features like Kanban boards (Hermes), cron `get`/`update` (PicoClaw), spawn_subagent (CoPaw), and inter-agent mailboxes (PicoClaw) signal a fundamental shift. The agent is no longer a chatbot; it is an **autonomous background worker with a structured task queue**. Developers should prioritize workflow primitives over chat polish.

4. **Security as a Competitive Moat**
   - ZeroClaw’s rapid response to tool allowlist bypasses and the sustained engagement on PicoClaw's `guardCommand` issue prove that the community will reward **ruthless permission models**. Enterprise adoption will flow to projects that bake security into the core architecture (WASI, RBAC), not bolt it on later.

5. **The Asian Market is the Growth Vector**
   - Over half of the top-tier projects are explicitly targeting Feishu, DingTalk, QQ, and Chinese cloud providers (NEAR, Volcengine, MiniMax, Qwen). **Global projects ignoring this trend are ceding a massive, fast-growing user base** to regional specialists.

6. **Rust Penetration Threatens Python Monoculture**
   - ZeptoClaw’s 6.98MB binary and Moltis’s system-level abstractions highlight growing appetite for **high-performance, low-footprint infrastructure**. Just as ClickHouse disrupted analytics, Rust-based agent frameworks could disrupt Python-heavy stacks in latency-sensitive deployment scenarios.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — June 2, 2026

**Project Health:** Extremely Active 🚀
- **Issues updated last 24h:** 29 (4 open, 25 closed)
- **PRs updated last 24h:** 33 (16 open, 17 merged/closed)
- **New Release:** v0.2.1

---

## 1. Today's Overview

NanoBot is surging with velocity following the v0.2.1 release, logging 33 active PRs and 29 issues in the last 24 hours. The community is closing long-standing issues at a high rate (25 closed) while simultaneously pushing major new features through the pipeline. Activity centers on Web UI transformation, channel expansion, and memory system evolution. The open PR count of 16 suggests the next minor release will bring substantial architectural changes, including manual memory mode, a dedicated QQ channel, and cloud deployment primitives.

---

## 2. Releases

### [v0.2.1](https://github.com/HKUDS/nanobot/releases)
*84 PRs merged | 17 new contributors*

The headline feature is the **WebUI becoming a full-featured workspace**. The chat surface is smoother, faster, and more reliable: live file edits show up as activity, tool traces render properly, and general speed/reliability are improved. Combined with the architectural cleanup leading to v0.2.1, this release represents a significant maturity milestone.

**No breaking changes or specific migration steps were noted beyond the standard upgrade path.**

---

## 3. Project Progress — Merged/Closed PRs Today

17 PRs were closed or merged in the last 24 hours. Key highlights:

### Channels & Connectivity
- **[PR #4016](https://github.com/HKUDS/nanobot/pull/4016)** — `feat(dingtalk): add group_user_isolation`. DingTalk group users now get independent session keys while the bot routes replies to the same group. Solves context contamination in shared channels.
- **[PR #3509](https://github.com/HKUDS/nanobot/pull/3509)** — `feat(channels): Add Napcat (QQ) channel`. Backported to main. Full OneBot v11 Forward WebSocket support for private and group chats with configurable reply policies.
- **[PR #3723](https://github.com/HKUDS/nanobot/pull/3723)** — `Local whisper transcription`. Integrates `faster-whisper` for on-device voice transcription—no API key or network required.

### Provider & Model Fixes
- **[PR #4124](https://github.com/HKUDS/nanobot/pull/4124)** — `fix(provider): handle XML tool call emissions from mimo/glm models`. Critical fix preventing raw XML (e.g., `<function=exec>`) from leaking into Telegram/WebSocket channels.

### Architecture & Core
- **[PR #4135](https://github.com/HKUDS/nanobot/pull/4135)** — `Refactor WebUI runtime state onto event bus`. Decouples UI from `AgentLoop` via a typed runtime event bus, paving the way for reliable external subscribers.
- **[PR #4143](https://github.com/HKUDS/nanobot/pull/4143)** — `Refactor session retention result`. Returns `RetentionResult` named tuple, resolving ambiguous archive semantics at call sites.
- **[PR #4129](https://github.com/HKUDS/nanobot/pull/4129)** — Fix for duplicate archive and message loss bugs in session retention.

### Bug Fixes
- **[Issue #4069](https://github.com/HKUDS/nanobot/issues/4069)** — Dream cron job registered without explicit enabled flag → **Closed**
- **[Issue #3633](https://github.com/HKUDS/nanobot/issues/3633)** — `Duplicate item found with id` error with GPT models → **Closed**
- **[Issue #3903](https://github.com/HKUDS/nanobot/issues/3903)** — MiniMax/AIHubMix hardcoded PNG mime type, bypassed base `_http_post()` → **Closed**

---

## 4. Community Hot Topics

The community is heavily engaged in foundational reliability and feature parity discussions:

### Most Active Issue
- **[Issue #4006](https://github.com/HKUDS/nanobot/issues/4006) — Orphaned tool results** (OPEN, 2 comments). Despite fix attempts in PR #3984, orphaned `role: "tool"` messages persist in conversation history. This violates OpenAI/Anthropic pairing specs and causes trace renderer errors and API rejections.

### High-Engagement Closed Issues
- **[Issue #2880](https://github.com/HKUDS/nanobot/issues/2880)** — "Every message returns error" (18 comments). A critical user-facing bug, now closed.
- **[Issue #1932](https://github.com/HKUDS/nanobot/issues/1932)** — "Skills don't support disable, only delete" (8 comments). Strong demand for flexible tool/skill configuration without deletion.
- **[Issue #3028](https://github.com/HKUDS/nanobot/issues/3028)** — "Heartbeat creates duplicate cron tasks" (4 comments). Reliability issue in the autonomous heartbeat system.

### Most Reacted
- **[Issue #49](https://github.com/HKUDS/nanobot/issues/49)** — Signal channel support (6 👍). Closed, but indicates enduring demand for secure messaging channels.
- **[Issue #1536](https://github.com/HKUDS/nanobot/issues/1536)** — MCP retry/reconnect logic (3 👍). Users in Kubernetes environments need robust connection recovery.
- **[Issue #1862](https://github.com/HKUDS/nanobot/issues/1862)** — Media path access with `restrictToWorkspace` (3 👍).
- **[Issue #2406](https://github.com/HKUDS/nanobot/issues/2406)** — Skip heartbeat LLM call when no active tasks (2 👍). Cost-conscious users.

### Underlying Needs
The data reveals three key community demands: **1) Reliability** — heartbeat duplication, orphaned tool calls, MCP disconnects; **2) Flexibility** — toggleable skills, configurable file tools, per-user sessions; **3) Channel Parity** — Signal, QQ, WebSocket, Discord bot-to-bot.

---

## 5. Bugs & Stability

### Critical
- **[Issue #4006](https://github.com/HKUDS/nanobot/issues/4006)** — **Orphaned tool results in conversation history.** Remnants of the `tool_call_id` fix (PR #3984). Causes strict API providers to reject requests and breaks trace rendering. No dedicated fix PR has been merged yet. **OPEN.**

### High
- **[Issue #4133](https://github.com/HKUDS/nanobot/issues/4133)** — **Agent response silently fails to deliver** after successful tool calls (Telegram). User sees tool results but never the final text turn. Persisted post-#4080. **CLOSED** — likely addressed by a hotfix or config change.

### Medium
- **[Issue #4128](https://github.com/HKUDS/nanobot/issues/4128)** — **Duplicate archive in session retention.** `retain_recent_legal_suffix` in `manager.py` causes user messages to be simultaneously archived and kept, leading to context corruption. **CLOSED** — fixed by PR #4129.
- **[Issue #3064](https://github.com/HKUDS/nanobot/issues/3064)** — **Cron tasks send intermediate thinking messages** instead of a single result. **CLOSED** (likely config fix or #3064 addressed).
- **[Issue #2601](https://github.com/HKUDS/nanobot/issues/2601)** — **Cron reminders not delivered in agent mode.** **CLOSED.**

### Low / Info
- **[Issue #4142](https://github.com/HKUDS/nanobot/issues/4142)** — **Optimization discussion for cache-miss input tokens**, especially relevant for DeepSeek V4 flash/pro. **OPEN.**
- **[Issue #1350](https://github.com/HKUDS/nanobot/issues/1350)** — `send_progress`/`send_tool_hints` config not working in gateway mode. **CLOSED.**

---

## 6. Feature Requests & Roadmap Signals

The open PR pipeline strongly suggests the composition of the next release:

### Likely Landing in v0.3.0
- **Manual Memory Mode** — [PR #4050](https://github.com/HKUDS/nanobot/pull/4050) introduces an explicit manual flow isolated from automatic memory. A major evolution of the memory subsystem.
- **Napcat (QQ) Channel** — [PR #4146](https://github.com/HKUDS/nanobot/pull/4146) brings robust QQ support to the main channel lineup.
- **Cloud Deployment Layer** — [PR #4139](https://github.com/HKUDS/nanobot/pull/4139) adds zero-dependency platform detection for HuggingFace Spaces and ModelScope Studio.
- **Azure AAD Auth** — [PR #4126](https://github.com/HKUDS/nanobot/pull/4126) adds Azure Identity-based authentication for Azure OpenAI, targeting enterprise deployments.

### WebUI Enhancement Wave
- **Inline Message Editing** — [PR #4148](https://github.com/HKUDS/nanobot/pull/4148) allows editing historical user messages in the WebUI.
- **Clipboard Fallback** — [PR #4149](https://github.com/HKUDS/nanobot/pull/4149) handles browsers where the Clipboard API is unavailable.
- **Voice Recording + Local ASR** — [PR #4122](https://github.com/HKUDS/nanobot/pull/4122) adds browser voice recording with FunASR transcription.

### Search & Tools
- **Volcengine Web Search** — [PR #4141](https://github.com/HKUDS/nanobot/pull/4141) adds a Bytedance search provider.
- **File Tools Enable Toggle** — [PR #4138](https://github.com/HKUDS/nanobot/pull/4138) brings `tools.file.enable` parity with `tools.exec.enable` and `tools.web.enable`.
- **Weather Skill** — [PR #4145](https://github.com/HKUDS/nanobot/pull/4145) adds a complete weather skill example.

### Performance & Architecture
- **Tokenizer Pre-warming** — [PR #3997](https://github.com/HKUDS/nanobot/pull/3997) reuses a shared `tiktoken` encoding and adds build-state timing logs.
- **Registry-Driven Provider Config** — [PR #3994](https://github.com/HKUDS/nanobot/pull/3994) introduces registry-driven provider config fields (Bedrock region/profile), exposing them in the WebUI.

---

## 7. User Feedback Summary

### Strengths Users Are Appreciating
- **Release Velocity:** v0.2.1 with 84 merged PRs signals strong forward momentum.
- **Community Responsiveness:** Long-standing issues (MCP reconnect, Signal channel, skills toggle) are finally being closed or addressed.
- **Privacy Features:** Local Whisper transcription ([PR #3723](https://github.com/HKUDS/nanobot/pull/3723)) removes the need for cloud speech APIs.

### Recurring Pain Points
- **Cron/Heartbeat Unreliability:** Multiple concurrent issues ([#3028](https://github.com/HKUDS/nanobot/issues/3028), [#3064](https://github.com/HKUDS/nanobot/issues/3064), [#2601](https://github.com/HKUDS/nanobot/issues/2601)) expose a weak point in the autonomous scheduling system—duplicate tasks, noisy intermediate messages, and missed deliveries.
- **Configurability Gaps:** Users consistently request the ability to toggle skills/tools without deleting them ([#1932](https://github.com/HKUDS/nanobot/issues/1932), [#4138](https://github.com/HKUDS/nanobot/pull/4138)).
- **Cost & Latency Pressure:** The combination of cache-miss cost discussions ([#4142](https://github.com/HKUDS/nanobot/issues/4142)), requests for streaming output ([#1547](https://github.com/HKUDS/nanobot/issues/1547)), and heartbeat token waste ([#2406](https://github.com/HKUDS/nanobot/issues/2406)) reveals a user base deeply sensitive to API expenditures.
- **Provider Compatibility Friction:** XML tool call leaks ([#4124](https://github.com/HKUDS/nanobot/pull/4124)) and orphaned tool results ([#4006](https://github.com/HKUDS/nanobot/issues/4006)) highlight the difficulty of maintaining broad model support.

### Language & Regional Signals
A significant portion of the community communicates in Chinese, and specific features (DingTalk isolation, Napcat/QQ channel, Volcengine search, ModelScope deployment) indicate heavy adoption across Asian markets.

---

## 8. Backlog Watch

While most items move quickly—often closing within days—several open items need maintainer attention to avoid stalling:

### PRs Awaiting Review
- **[PR #3997](https://github.com/HKUDS/nanobot/pull/3997)** & **[PR #3994](https://github.com/HKUDS/nanobot/pull/3994)** — These performance and configuration refactors (tokenizer sharing, registry-driven provider configs) have been open since May 25. They de-risk the startup path and enable provider-specific settings in the WebUI. Risk of merge conflicts increases daily.
- **[PR #4126](https://github.com/HKUDS/nanobot/pull/4126)** — Azure AAD authentication. A critical blocker for enterprise deployments. Open since May 31, no maintainer comments.
- **[PR #4122](https://github.com/HKUDS/nanobot/pull/4122)** — WebUI voice recording + FunASR. A large, complex feature that introduces new JS APIs and Python dependencies. Worth a design review soon to avoid last-minute conflicts.

### Open Discussions Needing Direction
- **[Issue #4142](https://github.com/HKUDS/nanobot/issues/4142)** — Cost optimization for cache-miss input tokens. This discussion touches caching strategy, prompt optimization, and provider behavior. Likely needs a maintainer to seed the implementation direction.
- **[Issue #4132](https://github.com/HKUDS/nanobot/issues/4132)** — Support for custom image generation providers. Open since June 1. Community contributor ([hesetiema](https://github.com/hesetiema)) wants to use Agnes AI via config. No maintainer response yet.
- **[Issue #4006](https://github.com/HKUDS/nanobot/issues/4006)** — Orphaned tool results. This is the most critical open bug. It breaks API compliance for strict providers. A targeted review of the trace/message persistence layer is needed to track down the remaining leak path.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-02

## 1. Today's Overview

Hermes Agent is in a period of exceptionally high development velocity, with 50 issues and 50 pull requests updated in the past 24 hours. While no formal release was cut today, the maintainers closed 14 PRs spanning critical bug fixes, Kanban workflow improvements, CLI stability, and skills discovery. A major coordinated effort is underway to harden the dflash/local backend subsystem, splitting a large stability PR into focused, reviewable chunks. The community remains deeply engaged, contributing sophisticated cost-analysis dashboards and detailed feature proposals. However, the volume of P1 regressions reported against the recent v0.15.1 build suggests release confidence remains a concern that the team is actively working to address.

## 2. Releases

**No new releases today.** The project appears to be accumulating changes for a future release (likely v0.16.x), with the dflash "snowball" refactor and Kanban maturation as likely headline features.

---

## 3. Project Progress

**14 PRs were merged or closed today**, advancing several key areas:

**Agent Core Stability**
- [#35642](https://github.com/NousResearch/hermes-agent/pull/35642) — **Merged:** Introduces a bounded retry counter for agent stall situations (default: 5 retries per turn via `HERMES_STALL_RETRY_MAX_PER_TURN`). Previously a one-shot guard, it now handles repeated stalls gracefully. The associated "snowball" split PRs (see Bugs & Stability) are proceeding in parallel to isolate specific improvements.

**Kanban & Multi-Agent Workflows**
- [#37174](https://github.com/NousResearch/hermes-agent/pull/37174) — Kanban notifier watcher now correctly gated on `dispatch_in_gateway`.
- [#37172](https://github.com/NousResearch/hermes-agent/pull/37172) — Decomposed child tasks inherit the worker's root project workspace instead of defaulting to a throwaway scratch directory.

**CLI / UI**
- [#37081](https://github.com/NousResearch/hermes-agent/pull/37081) / [#37173](https://github.com/NousResearch/hermes-agent/pull/37173) — Fixed `TypeError` crashes when a queued note (e.g., from `/model`) is prepended to a multimodal message containing an image.
- [#37175](https://github.com/NousResearch/hermes-agent/pull/37175) — The model picker no longer silently routes OpenAI selections through OpenRouter, fixing a 401 "Missing Authentication header" error for users without an OpenRouter key.

**Skills & Developer Experience**
- [#37143](https://github.com/NousResearch/hermes-agent/pull/37143) — `hermes skills browse` now surfaces the full catalog (~88k community skills), adds clickable source links, copy buttons, and one-click install.

**Integrations & Infrastructure**
- [#37154](https://github.com/NousResearch/hermes-agent/pull/37154) — Adds disabled-by-default `browser.agentcookie` config for Chrome profile reuse.
- [#24847](https://github.com/NousResearch/hermes-agent/pull/24847) — Honcho memory provider now **fails open** during startup, resolving a long-standing 60-second blocking issue.

---

## 4. Community Hot Topics

**Most Discussed**
- **[#4379](https://github.com/NousResearch/hermes-agent/issues/4379) — Token Overhead Analysis (9 comments):** A community member built a monitoring dashboard and discovered that **73% of every API call is fixed overhead (~13.9K tokens)** across Telegram, WhatsApp, and Cron gateways. The analysis includes concrete optimization proposals (bundling system prompts, batching memory reads, truncating cached contexts). This is an unusually deep and actionable community contribution.
- **[#5726](https://github.com/NousResearch/hermes-agent/issues/5726) — Honcho Slow Startup (8 comments, CLOSED):** Spurred the fix merged today in PR #24847. The debugging thread is an excellent example of community-maintainer collaboration on root cause analysis.

**Most Upvoted**
- **[#10149](https://github.com/NousResearch/hermes-agent/issues/10149) — "No auxiliary LLM provider configured" (16 👍):** The single most upvoted issue in the dataset reflects widespread user confusion around the auxiliary LLM configuration flow. Users with `OPENROUTER_API_KEY` set still see this warning. While the issue is technically closed, the underlying documentation gap remains a top friction point.
- **[#5143](https://github.com/NousResearch/hermes-agent/issues/5143) — Multi-Role Auto-Routing (14 👍, OPEN):** The v2 proposal aligns with the v0.14 architecture and introduces a contextual classifier with misroute recovery. This feature has strong demand signal for a multi-role/multi-agent roadmap.
- **[#12700](https://github.com/NousResearch/hermes-agent/issues/12700) — Gemini Flex Inference (6 👍, OPEN):** A cost-optimization feature request that maps perfectly onto Hermes's Cron and background subagent workloads.

---

## 5. Bugs & Stability

**Today was dominated by regression fixes and proactive stability hardening.**

### Highest Severity (P1)

| Issue | Status | Summary |
|---|---|---|
| [#36867](https://github.com/NousResearch/hermes-agent/issues/36867) | **CLOSED (Fixed)** | `load_jobs()` uncaught `AttributeError` on non-dict `jobs.json` taking down the entire cron subsystem. |
| [#36208](https://github.com/NousResearch/hermes-agent/issues/36208) | **CLOSED (Fixed)** | Official Docker container failing to start from build 2026.5.28. |
| [#29346](https://github.com/NousResearch/hermes-agent/issues/29346) | **CLOSED (Fixed)** | Discord tool-using responses silently dropped after `response ready` log. |
| [#37105](https://github.com/NousResearch/hermes-agent/pull/37105) | **CLOSED (Fixed)** | Hardcoded 200K context window for Bedrock Claude 4.x models (should be 1M). |
| **#35595** | **OPEN** | **v0.15 Regression:** `hermes /model` returns structured field names instead of human-readable text. |
| **#25935** | **OPEN** | **Discord:** Image attachments mixed with documents or non-supported formats cause fatal HTTP 400. |

### Notable Regressions & Functional Bugs (P2, Open)

- **Chrome CDP DOM Operations** ([#36211](https://github.com/NousResearch/hermes-agent/issues/36211)): Reported broken in v0.15.1, with `Identifier has already been declared` errors and unresponsive click actions.
- **Bedrock Auth Wizard Pitfall** ([#28156](https://github.com/NousResearch/hermes-agent/issues/28156)): Accepts Bearer-only setup for Claude on Bedrock, then fails at runtime requiring IAM credentials.
- **Memory Char Limit Bypass** ([#11665](https://github.com/NousResearch/hermes-agent/issues/11665)): `memory_char_limit` and `user_char_limit` fully ignored when the `memory` tool is dispatched via CLI/subagent paths.
- **Discord Mixed Attachments** ([#29711](https://github.com/NousResearch/hermes-agent/issues/29711)): Non-image documents serialized as `input_image` data URIs, causing API 400 errors.

### dflash / Local Backend Stability Push (The "Snowball" Effort)

The team is methodically splitting the large [#35642](https://github.com/NousResearch/hermes-agent/pull/35642) into isolated reviewable PRs, signaling deep investment in local model serving reliability:
- [#37160](https://github.com/NousResearch/hermes-agent/pull/37160) — Canary hardening loop
- [#37168](https://github.com/NousResearch/hermes-agent/pull/37168) — Local TTFB failover
- [#37166](https://github.com/NousResearch/hermes-agent/pull/37166) — Stall retry policy stack
- [#37176](https://github.com/NousResearch/hermes-agent/pull/37176) — Local backend recovery hooks

---

## 6. Feature Requests & Roadmap Signals

**Strong Upstream Signals**
- **Kanban Maturation:** Issues [#37109](https://github.com/NousResearch/hermes-agent/issues/37109) (Executor Board/active-worker panel) and [#37108](https://github.com/NousResearch/hermes-agent/issues/37108) (Column alignment for scheduled/review tasks) were filed today, suggesting the Kanban feature is being actively productionized.
- **Enterprise/Multi-Tenant Routing:** [#5143](https://github.com/NousResearch/hermes-agent/issues/5143) (Multi-Role Auto-Routing v2) and [#35408](https://github.com/NousResearch/hermes-agent/issues/35408) (auth identity propagation to agent sessions) point toward multi-user and enterprise deployment scenarios.
- **Cost Optimization:** The community's deep dive into token overhead ([#4379](https://github.com/NousResearch/hermes-agent/issues/4379)) and upvotes for Gemini Flex ([#12700](https://github.com/NousResearch/hermes-agent/issues/12700)) suggest cost management will remain a key design driver for the provider stack.

**Predicted for Next Release (v0.16.0)**
- Merging of the dflash "snowball" stability PRs (TTFB failover, stall retry, backend recovery).
- Completing the Kanban dashboard UI improvements (executor board, filtered columns).
- MCP endpoint validation/hardening following [#36052](https://github.com/NousResearch/hermes-agent/issues/36052).
- Resolution of the Discord drop/attachment regressions.

---

## 7. User Feedback Summary

**Pain Points**
- **Upgrade Regressions (High Intensity):** The v0.15.1 release delivered multiple P1/P2 regressions (model command structured output, Chrome CDP DOM breakage, Docker container startup failure). The community is providing excellent repro cases, but the pattern erodes trust in minor releases.
- **Discord Reliability:** The Discord adapter remains the largest source of front-line bugs: silent message drops, connection timeouts, and image handling failures dominate the complaint volume.
- **Observability Gaps:** Users lack native tooling for cost profiling (community had to build their own dashboard in [#4379](https://github.com/NousResearch/hermes-agent/issues/4379)) and often don't realize the agent has memory of cron deliveries ([#37070](https://github.com/NousResearch/hermes-agent/issues/37070)).

**Use Cases & Satisfaction**
- Deployments are sophisticated and diverse: multi-gateway (Telegram, WhatsApp, Discord, Cron), multi-provider (OpenAI, Bedrock, Gemini, MiniMax, local models), Kaban-backed task orchestration, and MCP server integrations.
- The community is unusually sophisticated, filing high-quality profiling data, v2 proposals with architecture diagrams, and precise root-cause analyses. This signals a deeply invested user base.

---

## 8. Backlog Watch

Several high-value issues require maintainer attention:

| Issue | Priority | Age | Rationale |
|---|---|---|---|
| [#11665](https://github.com/NousResearch/hermes-agent/issues/11665) — Memory char limits bypassed | P2 | Since 2026-04-17 | Core feature (memory limits) silently non-functional in dispatch paths. |
| [#5143](https://github.com/NousResearch/hermes-agent/issues/5143) — Multi-Role Auto-Routing | N/A (Feature) | Since 2026-04-04 | 14 👍, heavily revised v2 proposal, no maintainer activity in 24h. |
| [#19776](https://github.com/NousResearch/hermes-agent/issues/19776) — Discord connect timeout | P2 | Since 2026-05-04 | Simple configuration fix, but blocks gateway startup for Discord users with slow sync. |
| [#20507](https://github.com/NousResearch/hermes-agent/issues/20507) — Camoufox session close | P2 | Since 2026-05-06 | Breaks multi-turn browsing workflows; user is running in Docker headless. |
| [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) — Bedrock IAM wizard lapse | P2 | Since 2026-05-18 | Wizard UX that accepts invalid configurations causing silent runtime failures. |
| [#12700](https://github.com/NousResearch/hermes-agent/issues/12700) — Gemini Flex | N/A (Feature) | Since 2026-04-19 | High upvotes, low implementation complexity, strong cost-savings narrative. |

**All issues and PRs referenced are under [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent).**

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-02

## 1. Today's Overview

PicoClaw enters a period of very high development velocity with **11 pull requests** and **7 issues** updated in the past 24 hours, alongside a new nightly release. Activity is evenly split between stabilization work (model API regressions, infrastructure bugs) and ambitious new features (inter-agent collaboration, new providers, expanded cron tooling). The `v0.2.9-nightly.20260602.426046fc` build aggregates these changes ahead of a stable v0.2.9 release. The project maintains a healthy contributor mix: three external authors (dtapps, LegendAlessandro-Liguori, afjcjsbx) landed or proposed fixes today alongside core committers.

## 2. Releases

**Nightly Build — v0.2.9-nightly.20260602.426046fc**

A new automated nightly build has been published. It is explicitly marked as **potentially unstable** and intended for early testing. The changelog against stable `v0.2.9` can be inspected in full here:

[`compare/v0.2.9...main`](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

No migration notes have been provided, but users deploying this nightly should expect breaking changes related to the prompt skill catalog refactor (PR #2781) and the Bedrock/Anthropic temperature handling changes (PR #2982, #2940).

## 3. Project Progress

Five pull requests were merged or closed today, advancing the project in three key areas:

**Features**
- [#2977](https://github.com/sipeed/picoclaw/issues/2977) **feat(cron):** Added `get` and `update` actions to the cron tool. Agents can now inspect persisted job payloads and apply partial edits, preventing expensive "remove → add" rescheduling flows.
- [#2893](https://github.com/sipeed/picoclaw/issues/2893) **feat(channels):** Merged support for **Server酱³ Bot (SC3Bot)** , a popular notification service in China, with both polling and webhook modes.

**Performance**
- [#2781](https://github.com/sipeed/picoclaw/issues/2781) **perf(skill catalog):** Drastically reduced token consumption by no longer injecting the full skill XML listing into every LLM turn. On providers without prompt caching, this is a major latency and cost improvement for multi-turn sessions and tool-call round-trips.

**Stability & Fixes**
- [#2982](https://github.com/sipeed/picoclaw/issues/2982) **fix(bedrock):** Resolved a hard failure for Claude Opus 4.8 on AWS Bedrock where the deprecated `temperature` parameter caused all requests to return HTTP 400.
- [#2890](https://github.com/sipeed/picoclaw/issues/2890) **fix(macos):** Resolved symlink mismatches (`/var` → `/private/var`) that caused path validation failures in tests and runtime.

## 4. Community Hot Topics

| Issue / PR | Engagement | Topic |
|---|---|---|
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | **15 comments**, 2 👍 | `exec` tool `guardCommand` overblocking legitimate `curl` requests |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | **8 comments** | `.deb` package fully non-functional on RISC-V |
| [#2720](https://github.com/sipeed/picoclaw/issues/2720) | **7 comments** | Singleton PID check crash loop when OS reuses PID |
| [#2796](https://github.com/sipeed/picoclaw/issues/2796) | **5 comments** | History display shows only the last user message in multi-turn conversations |

**Analysis of Underlying Needs:**
The community is signaling a strong desire for **robust safety tooling that does not cripple functionality** (#1042), **cross-platform reliability** (#2887), and **infrastructure resilience** (#2720). The history display issue (#2796) touches core UX — users expect a complete audit trail rather than a compressed view optimized for the LLM context window. These four threads represent the highest concentration of user pain reported to the project.

## 5. Bugs & Stability

Bugs are ranked by severity and user impact:

**Critical / High Severity (Blocking or Crash Loops)**

| Issue | Description | Status / Fix |
|---|---|---|
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | `.deb` on RISC-V completely non-functional with OpenAI models | **No fix PR yet.** Platform blocking for RISC-V adopters. |
| [#2720](https://github.com/sipeed/picoclaw/issues/2720) | Gateway enters crash loop when PID file contains a reused OS PID | Fix PR [#2813](https://github.com/sipeed/picoclaw/issues/2813) is **open but stale** since May 7. |
| [#2939](https://github.com/sipeed/picoclaw/issues/2939) | `claude-opus-4-7` fails with *"temperature is deprecated"* | Fix PR [#2940](https://github.com/sipeed/picoclaw/issues/2940) is **open but stale** since May 25. |
| [#2941](https://github.com/sipeed/picoclaw/issues/2941) | Default config seeds model ID with dots (`claude-sonnet-4.6`) causing HTTP 404 | Fix PR [#2942](https://github.com/sipeed/picoclaw/issues/2942) is **open but stale** since May 25. |

**Moderate Severity (Functional Bugs)**

| Issue | Description | Status / Fix |
|---|---|---|
| [#2796](https://github.com/sipeed/picoclaw/issues/2796) | History UI collapses earlier user messages, showing only the last one | **No fix PR yet.** |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `guardCommand` regex incorrectly parses non-path arguments (e.g. `curl` URLs), blocking execution | **No fix PR yet.** |

**Note:** The Bedrock Opus 4.8 variant of the temperature bug ([#2982](https://github.com/sipeed/picoclaw/issues/2982)) was successfully fixed and merged today.

## 6. Feature Requests & Roadmap Signals

**High Probability for v0.2.9 / Upcoming Stable:**

- [#2937](https://github.com/sipeed/picoclaw/issues/2937) **Agent Collaboration Bus (Open):** This is the most significant architectural addition in the pipeline. It introduces durable inter-agent mailboxes, collaboration threads, and permission-aware message routing. This strongly signals a shift towards **first-class multi-agent systems** within PicoClaw.
- [#2917](https://github.com/sipeed/picoclaw/issues/2917) **NEAR AI Cloud Provider (Open):** A new OpenAI-compatible provider integrating NEAR AI Cloud, including TEE-capable model support. This expands the ecosystem for decentralized inference.
- [#2977](https://github.com/sipeed/picoclaw/issues/2977) **Cron `get`/`update` (Merged):** Empowers agents with finer-grained control over autonomous scheduling.

**Documentation Gap:**
- [#2981](https://github.com/sipeed/picoclaw/issues/2981) A formal request to update the user manual for v0.2.9 was opened today. This is likely a prerequisite for the stable release cut.

## 7. User Feedback Summary

**Satisfaction Drivers:**
- The community is **highly engaged and contributor-friendly**: external developers are shipping non-trivial features (SC3Bot, NEAR AI provider, symlink fixes) across the full stack.
- The performance improvement in skill catalog token usage ([#2781](https://github.com/sipeed/picoclaw/issues/2781)) addresses a longstanding complaint about prompt size growth in extended sessions.

**Pain Points (Repeated Themes):**
1. **Default configuration fragility.** Fresh installations break on first launch because default model IDs are incorrect (`claude-sonnet-4.6` instead of `claude-sonnet-4-6`) and deprecated parameters are sent to new models.
2. **Tooling safety vs. usability.** The `guardCommand` issue ([#1042](https://github.com/sipeed/picoclaw/issues/1042)) has the highest community engagement of any open item, reflecting a deep tension between security defaults and advanced agent capability.
3. **Reliability friction.** The stale PID bug ([#2720](https://github.com/sipeed/picoclaw/issues/2720)) continues to cause operational disruptions for self-hosters.
4. **Platform parity.** RISC-V users are blocked entirely with no workaround.

## 8. Backlog Watch

Several critical items are at risk of stalling and need maintainer attention:

| Item | Opened | Risk |
|---|---|---|
| [#2813](https://github.com/sipeed/picoclaw/issues/2813) **PR: PID identity verification** | **May 7** | Fixes a crash-loop bug. Has received no review action in 26 days despite repeated community comments. |
| [#2942](https://github.com/sipeed/picoclaw/issues/2942) **PR: Fix Claude Sonnet default model ID** | **May 25** | Trivial one-line fix blocking new Anthropic users. Stale for 8 days. |
| [#2940](https://github.com/sipeed/picoclaw/issues/2940) **PR: Omit temperature for Opus 4.7** | **May 25** | Companion fix to merged Bedrock PR #2982, but for the direct Anthropic provider. Stale for 8 days. |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) **Issue: `exec` guard overblocking** | **Mar 4** | Highest-commented issue in the project (15 comments). Core UX friction with no maintainer response or fix PR. |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) **Issue: RISC-V platform block** | **May 17** | High profile platform issue. No maintainer acknowledgement of root cause (dependency vs. runtime) in the thread. |

**Bottom Line:** The project has excellent feature velocity, but a backlog of critical bug fix PRs is accumulating without review. Resolving the stale PRs (#2813, #2940, #2942) would immediately close several of the most impactful user-facing bugs.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest – 2026-06-02**

---

### 1. Today's Overview
The project is in an intense stability and hardening cycle. Over the past 24 hours, **3 issues** and **6 pull requests** were updated, with zero new releases cut. The overwhelming focus is on runtime resilience: fixing crash-loops on corrupted transcripts, filling gaps in tool timeout handling, and improving the container execution environment for broader deployment profiles. The development velocity is strong, with fix PRs landing within 24 hours of critical bug reports, signaling a responsive maintainer team prioritizing reliability above feature velocity.

---

### 2. Releases
*None.*
No new releases were cut in the reporting period.

---

### 3. Project Progress
Two items were resolved/closed:

- **Issue #2331 (Closed)** – **[High] A2A session routing bug.** Fixed a critical logic error in `findSessionByAgentGroup` where A2A replies in multi-channel groups were routed to the wrong session due to a naive recency sort. This was a high-priority behavioral fix that closes a significant correctness gap for multi-tenant channel setups.
  *(URL: nanocoai/nanoclaw Issue #2331)*

- **PR #2664 (Merged/Closed)** – **Infrastructure: Browser scraping sidecar.** The PR to run the browser scraping sidecar inside a v2 container has been merged, standardizing the deployment model for web automation workloads and aligning it with the project’s broader containerization strategy.
  *(URL: nanocoai/nanoclaw PR #2664)*

---

### 4. Community Hot Topics
While comment volumes remain low (most issues are in the 0–1 comment range), a distinct cluster of activity surrounds **agent runtime reliability**, driven by two key issues:

- **Agent Crash-Loops (Issue #2669 / PR #2670)** – The most critical operational topic. Issue #2669 describes a permanent crash-loop when a resumed transcript contains corrupted `thinking` blocks, resulting in a tight 400-error loop. Contributor `ddaniels` submitted a fix PR (#2670) the same day, implementing a manual state reconstruction to bypass the SDK error. This reflects a deep community need for **self-healing runtimes** that can recover from malformed state without manual intervention.
  *(URL: nanocoai/nanoclaw Issue #2669, PR #2670)*

- **Provider Failure Recovery (PR #2666)** – The largest structural change in the queue, this PR introduces rollback, replay, in-turn acknowledgment, and friendly fallback for provider failures. It is currently blocked on PR #2667 (rootless Podman fix). This signals that the community is pushing the agent framework toward **production-grade operational maturity**, where provider outages are handled gracefully rather than causing session abortion.
  *(URL: nanocoai/nanoclaw PR #2666)*

---

### 5. Bugs & Stability
Three new bug reports landed, ranked by severity:

- **[CRITICAL] Issue #2669 – Corrupt transcript crash-loop (ddaniels).** An agent session enters an infinite 400-error loop when a `thinking` block is malformed in a resumed transcript. The session is permanently blocked with no built-in recovery. **Fix PR #2670 is open** (state truncation + replay).
  *(URL: nanocoai/nanoclaw Issue #2669, PR #2670)*

- **[HIGH] Issue #2668 – No per-tool timeout (mshirel).** A single hung MCP tool call runs synchronously inside the Claude Agent SDK turn loop, blocking the entire agent session for up to 30-minutes until a cold kill. The agent-runner only checks heartbeats between events, creating a wide window of unresponsiveness. **No fix PR exists yet.**
  *(URL: nanocoai/nanoclaw Issue #2668)*

- **[MEDIUM] Issue #2671 – Missing attachments mount (Ari-CMC).** The inbound attachments directory is not mounted into agent containers, causing channel adapter formatters to fail silently. **Fix PR #2671 is open** (adds a read-only bind mount).
  *(URL: nanocoai/nanoclaw PR #2671)*

- **[MEDIUM] Issue #2667 – Rootless Podman container user conflict (dtreskunov).** Running the agent container as root (required for bind-mount access under rootless Podman on LXC) clashes with Claude Code v2.1.128’s `--dangerously-skip-permissions` security check, blocking startup. **Fix PR #2667 is open.**
  *(URL: nanocoai/nanoclaw PR #2667)*

---

### 6. Feature Requests & Roadmap Signals
- **Provider Failure Recovery (PR #2666)** – The strongest roadmap signal this period. The introduction of automatic rollback, replay, and fallback provider selection represents a deliberate architectural push toward enterprise-grade uptime. If merged, this would be the most significant improvement to session durability in recent history.

- **Per-Tool Timeouts (Issue #2668)** – The absence of per-tool timeout handling is an increasingly clear operational gap. Given the concrete reproduction in this issue and the direct impact on session availability, a timeout framework for MCP tool calls is a high-probability candidate for the next feature release.

- **Browser Scraping Sidecar Containerization (PR #2664)** – Now merged, this unlocks headless browsing workflows as a standardized capability. Expect community extensions built on this pattern for web data extraction and visual testing.

---

### 7. User Feedback Summary
Real user pain points are concentrated in **runtime stability and operational maturity**:

- **Session resilience is the weakest link.** Two users (`ddaniels`, `mshirel`) independently reported blocking production issues in the same 24-hour window: one involving permanent crash-loops, the other involving 30-minute session freezes due to hung tools. This indicates that the core agent loop is functionally complete but fragile under real-world adversarial conditions (malformed LLM responses, slow MCP tools).

- **Configuration friction with non-standard Docker setups.** User `dtreskunov` reported incompatibility with rootless Podman, a common deployment choice for security-conscientious environments. This highlights a need for broader container runtime support.

- **Positive responsiveness.** The speed at which fix PRs appeared for issues #2669 and #2671 suggests users feel heard. However, the lack of a fix for #2668 (tool timeouts) suggests this is either a deeper architectural challenge or a lower priority.

---

### 8. Backlog Watch
- **PR #2346 – Fix: treat unknown slash commands as normal chat (SidhayaPravda618).**
  *Opened:* 2026-05-08 (~25 days without maintainer interaction).
  *Status:* Open, zero comments.
  *Risk:* This PR addresses a concrete UX regression where unknown slash commands are misrouted as `passthrough` to the Agent SDK, causing silent drops. Despite being open for nearly a month, there is no public review or closure. Given the current flurry of stability patches, this fix is at risk of being overlooked, but it represents a genuine quality-of-life improvement for interactive users.
  *(URL: nanocoai/nanoclaw PR #2346)*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**Project Digest: NullClaw — 2026-06-02**

**1. Today's Overview**
NullClaw experienced a quiet day with no new issues filed or releases cut. The only activity in the last 24 hours was an update to a single open pull request carried over from the previous day. Development focus appears tightly scoped on polish work for the Telegram integration. Overall project health remains stable, though the lack of merged pull requests and the absence of maintainer comments on the new PR suggest the integration pace has slowed slightly.

**2. Releases**
No new releases were published today. The latest stable release is unchanged.

**3. Project Progress**
- **Merged/Closed Pull Requests:** None. No code was merged or closed today.
- **Project Velocity:** The repository features 1 open pull request awaiting review.

**4. Community Hot Topics**
- **[PR #943] fix(telegram): show typing indicator during callback-query processing**
  - **Author:** raskevichai
  - **Status:** Open (Updated 2026-06-01)
  - **Link:** [GitHub Pull Request #943](https://github.com/nullclaw/nullclaw/pull/943)
  - **Analysis:** This is the sole active community item today. The PR addresses a missing UX affordance: Telegram inline buttons (e.g., `nc_choices`) trigger a `callback_query` that the agent processes silently. Unlike text messages, which show a "typing…" indicator, button presses leave the user staring at a blank screen during the 5–30 second model inference window.
  - **Underlying Need:** The community is signaling a need for interaction parity. Regardless of input method (text vs. button), users expect consistent real-time feedback. A silent interface implies a crash or hang, damaging trust in the agent’s responsiveness.

**5. Bugs & Stability**
- **Critical/High:** None reported in the last 24 hours.
- **Medium (Referenced as Issue #942):** Missing typing indicator on Telegram button presses. This bug degrades UX but does not cause crashes or data loss. A fix is already submitted in **[PR #943](https://github.com/nullclaw/nullclaw/pull/943)**.
- **Regressions:** None detected.

**6. Feature Requests & Roadmap Signals**
- **No New Feature Requests:** Zero new feature requests were filed today.
- **Roadmap Signal:** The heavy focus on fixing the Telegram callback-query UX suggests stabilizing and polishing core chat integrations is the top priority. The next minor release will likely include this behavioral fix, and future iterations may extend the typing indicator logic to other asynchronous processing paths.

**7. User Feedback Summary**
- **Pain Points:** The dominant pain point is the lack of visual feedback during interactive Telegram sessions. Users navigating multi-step `nc_choices` menus are met with an unresponsive "blank" UI state.
- **Use Cases:** Heavily impacts users who rely on inline keyboards for structured command selection and agent workflows.
- **Satisfaction / Dissatisfaction:** While the missing indicator caused dissatisfaction, the proactive submission of a fix by a community contributor (`raskevichai`) indicates a healthy contributor base. The absence of reactions or comments on the PR itself suggests the wider community has not yet evaluated it, or maintainer bandwidth is constrained.

**8. Backlog Watch**
- **[PR #943](https://github.com/nullclaw/nullclaw/pull/943)** (1 day old): This is the only item requiring maintainer attention. It has received no comments or reviews since creation. A brief acknowledgement from a project maintainer would prevent the PR from going stale and would encourage future contributions from the author and others in the community.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw Project Digest — June 2, 2026**

**1. Today's Overview**
The project experienced a surge in `reborn-integration` branch activity, with 47 pull requests updated and 32 merged or closed in the last 24 hours. Core contributor `henrypark133` filed a tightly scoped batch of issues (#4309–#4314) targeting critical gaps in Reborn compaction retries, error classification, and recovery logic. Community engagement is also strong, highlighted by a proactive code review flagging a potential scalability issue in ENGINE_V2. No new formal releases were published today, as the project remains heads-down on the Reborn architectural overhaul.

**2. Releases**
No new releases were cut today. The project remains in a heavy integration phase on the `reborn-integration` branch; the next stable release is pending the stabilization of the agent loop, event streaming, and capability porting work currently being merged.

**3. Project Progress**
Today marked major strides across the Reborn ecosystem, with 32 PRs merged or closed:
*   **Budgets & Agent Loop:** The massive PR [#3899](https://github.com/nearai/ironclaw/pull/3899) (Reborn budget follow-ups) landed, completing the cost-based budgets foundation. Skill activation context ([#4305](https://github.com/nearai/ironclaw/pull/4305)) was merged to progressively disclose context to the model, and provider capability input validation ([#4306](https://github.com/nearai/ironclaw/pull/4306)) closed a security bypass window.
*   **Core Infrastructure:** The trigger poller core ([#4301](https://github.com/nearai/ironclaw/pull/4301)) and product outbound orchestration seam ([#4277](https://github.com/nearai/ironclaw/pull/4277)) laid groundwork for scheduled tasks and webhooks. The `EventStreamManager` for durable projection fanout was closed ([#3281](https://github.com/nearai/ironclaw/issues/3281)).
*   **Integrations:** OAuth and capability surfaces for GSuite ([#4297](https://github.com/nearai/ironclaw/pull/4297), [#4293](https://github.com/nearai/ironclaw/pull/4293)) and Notion ([#4300](https://github.com/nearai/ironclaw/pull/4300)) were wired into Reborn. The full GitHub capability surface was ported ([#4280](https://github.com/nearai/ironclaw/pull/4280)).
*   **Developer Experience:** A startup crash caused by bundled extension manifest changes was fixed in [#4299](https://github.com/nearai/ironclaw/pull/4299).

**4. Community Hot Topics**
*   **Most Active Thread:** The now-closed [EventStreamManager issue](https://github.com/nearai/ironclaw/issues/3281) drew the highest engagement with 6 comments before resolution.
*   **Roadmap Discussion:** Issue [#4279](https://github.com/nearai/ironclaw/issues/4279) shows a community member engaging deeply with Reborn’s stateless agent model and "Agent NFT" tokenization mechanism. The user praised the architecture but requested clearer milestones for multi-tenant deployment.
*   **Code Review & Performance:** Issue [#4278](https://github.com/nearai/ironclaw/issues/4278) demonstrates proactive community auditing. The user identified a potential context window exhaustion vulnerability in ENGINE_V2 due to unbounded conversation history growth, signaling a need for better session lifecycle documentation.
*   **External Contributions:** New contributor `thisisjoshford` submitted a documentation reconciliation PR ([#4302](https://github.com/nearai/ironclaw/pull/4302)). Regular contributor `octo-patch` updated the MiniMax provider to M3 ([#4298](https://github.com/nearai/ironclaw/pull/4298)), and `danielwpz` is building out the Slack Events API host ingress ([#4272](https://github.com/nearai/ironclaw/pull/4272)).

**5. Bugs & Stability**
Several critical logic flaws were surfaced specifically targeting the Reborn agent loop’s reliability:
*   **Critical – Retry Integrity:** [#4309](https://github.com/nearai/ironclaw/issues/4309) describes a scenario where a successful compaction summary write outlives a failed `BeforeModel` checkpoint, potentially blocking future retries with a stale watermark. [#4310](https://github.com/nearai/ironclaw/issues/4310) reveals the executor ignores the `ShrinkContext` signal during context-overflow recovery, causing it to rebuild the same failing oversized prompt.
*   **Critical – Error Classification:** [#4311](https://github.com/nearai/ironclaw/issues/4311) identifies that distinct budget governance failures (e.g., credit exhaustion) are incorrectly collapsed into `ContextOverflow`, masking underlying billing issues and confusing users.
*   **Stability:** The nightly E2E test suite failed again on the `v2-engine` job ([#4108](https://github.com/nearai/ironclaw/issues/4108)).
*   **Fix in Progress:** A fix for vision attachment handling in ENGINE_V2 is being reviewed in PR [#4315](https://github.com/nearai/ironclaw/pull/4315).

**6. Feature Requests & Roadmap Signals**
The development trajectory is fully dictated by the Reborn rollout:
*   **User-Facing:** The community request for better visibility into agent state is being addressed by plans to surface compaction progress ([#4312](https://github.com/nearai/ironclaw/issues/4312)) and NEAR AI credit exhaustion ([#4286](https://github.com/nearai/ironclaw/pull/4286)) in the WebUI.
*   **Channel Integrations:** The pipeline for Reborn channel backends is filling up, with active development on Slack Events ([#4272](https://github.com/nearai/ironclaw/pull/4272)) and Feishu websocket intake ([#4178](https://github.com/nearai/ironclaw/pull/4178)).
*   **Capability System:** The addition of runtime context prompt stages ([#4304](https://github.com/nearai/ironclaw/pull/4304)) and a WebUI v2 extension registry ([#4307](https://github.com/nearai/ironclaw/pull/4307)) points to a more robust plugin system.
*   **Near-Term Milestones:** The trigger poller harness ([#4308](https://github.com/nearai/ironclaw/pull/4308)) and OAuth integration for WebUI ([#4287](https://github.com/nearai/ironclaw/issues/4287)) are close to completion.

**7. User Feedback Summary**
*   **Positive Reception:** A user reviewing the `reborn-integration` branch expressed being "very impressed" by the shift toward a stateless, cloud-native architecture ([#4279](https://github.com/nearai/ironclaw/issues/4279)).
*   **Pain Points:** The same user requested clearer roadmap documentation for early adopters. Another user ([#4278](https://github.com/nearai/ironclaw/issues/4278)) flagged a potential memory growth issue, suggesting that default session lifecycle management needs better documentation or automated safeguards.
*   **Satisfaction:** The volume of high-quality external contributions (Slack, Feishu, MiniMax, docs reconciliation) reflects a healthy, motivated community ecosystem.

**8. Backlog Watch**
*   **Critical Instability:** [#4108](https://github.com/nearai/ironclaw/issues/4108) (Nightly E2E failure) has been open since May 27 and was updated today with another failure report. It has received zero comments from maintainers. Given the high pace of merges, this persistent failure in the `v2-engine` test suite requires immediate triage to prevent masking future regressions.
*   All other open issues are recent (within 24 hours) and are actively being discussed or have associated fix PRs.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — June 2, 2026

**Project:** LobsterAI (netease-youdao/LobsterAI)
**Analysis Date:** 2026-06-02
**Data Source:** GitHub Activity (Last 24 hours)

---

## 1. Today's Overview

On June 2, 2026, LobsterAI demonstrated exceptional execution velocity, closing and merging **50 pull requests** in a single day while publishing a new minor version (**2026.6.1**). The project shows strong health, transitioning rapidly from feature development into a stabilization and integration phase. Notably, **zero issues** were updated in the last 24 hours, which may indicate the team successfully cleared the active bug tracking queue ahead of the release. The standout strategic signal is the introduction of the **Expert Kit Store**, setting the stage for a community-driven plugin marketplace. Overall, the project is in a highly productive state, prioritizing runtime reliability and user experience polish.

## 2. Releases

**Version 2026.6.1** was released today.

**Key Changes:**
- **Expert Kit Store & Conversation Integration** ([PR #2060](https://github.com/netease-youdao/LobsterAI/pull/2060)): A new storefront for discovering and installing Expert Kits directly from within the chat interface, enabling users to augment agent capabilities with specialized toolkits.
- **Plugin Update Checks** ([PR #2069](https://github.com/netease-youdao/LobsterAI/pull/2069)): Added update check support for `npm` and `clawhub` plugin sources, broadening the plugin ecosystem's reach.
- **MCP Fixes** (details truncated): A fix for the Model Context Protocol subsystem was included.
- **Migration Notes:** None provided. Standard dependency updates recommended for users leveraging the plugin registry.

## 3. Project Progress (Merged/Closed PRs)

The 50 merged PRs represent significant progress across the entire stack:

**Agent Intelligence:**
- **Thinking Level Control** ([PR #1985](https://github.com/netease-youdao/LobsterAI/pull/1985)): Introduced a granular per-session reasoning depth selector (Off, Minimal, Low, Medium, High, Adaptive), fully wired through DB, Redux, IPC, preload, and i18n.
- **Model Compatibility** ([PR #2000](https://github.com/netease-youdao/LobsterAI/pull/2000), [#2032](https://github.com/netease-youdao/LobsterAI/pull/2032), [#2035](https://github.com/netease-youdao/LobsterAI/pull/2035)): Fixed model switch errors with custom configurations, resolved Anthropic format compatibility for the Mimo model, and updated the Qwen coding plan for Qwen 3.6 Plus.

**Platform & Infrastructure:**
- **OpenClaw Gateway Optimization** ([PR #2018](https://github.com/netease-youdao/LobsterAI/pull/2018), [#2024](https://github.com/netease-youdao/LobsterAI/pull/2024)): Prevented unnecessary gateway restarts on token refresh and optimized restart logic.
- **Tool Stability** ([PR #2023](https://github.com/netease-youdao/LobsterAI/pull/2023), [#2015](https://github.com/netease-youdao/LobsterAI/pull/2015)): Improved the success rate of the Browser and WebFetch tools; fixed OpenClaw compaction retries and tool result gap handling.
- **macOS Voice Permissions** ([PR #1952](https://github.com/netease-youdao/LobsterAI/pull/1952)): Implemented a proper error flow when macOS accessibility permissions are denied, providing a toast that guides users to System Settings.

**UI/UX & Artifacts:**
- **Artifacts Refinement** ([PR #2022](https://github.com/netease-youdao/LobsterAI/pull/2022), [#2002](https://github.com/netease-youdao/LobsterAI/pull/2002), [#2012](https://github.com/netease-youdao/LobsterAI/pull/2012)): Introduced lazy-loading for source preview, theme-aware styling, fixed local resource path resolution for Markdown files, and added existence validation for HTML previews.
- **IM Bot Management** ([PR #2025](https://github.com/netease-youdao/LobsterAI/pull/2025), [#2037](https://github.com/netease-youdao/LobsterAI/pull/2037)): Redesigned the bot management interface and optimized copywriting.
- **Chores** ([PR #2028](https://github.com/netease-youdao/LobsterAI/pull/2028), [#2008](https://github.com/netease-youdao/LobsterAI/pull/2008), [#2009](https://github.com/netease-youdao/LobsterAI/pull/2009)): General UI updates, icon refresh, and cron UI improvements.

**Security**
- **Security Monitor Toggle** ([PR #1962](https://github.com/netease-youdao/LobsterAI/pull/1962)): Added `nsp-clawguard` as an optional plugin with a hot-toggle in Settings.

## 4. Community Hot Topics

With zero issues receiving comments and zero open PRs, community discussion in the tracked window is minimal. However, the allocation of development effort reveals the implicit "hot" areas:

1. **macOS User Experience ([PR #1952](https://github.com/netease-youdao/LobsterAI/pull/1952))**: The fix for silent voice input failure was a high-priority UX fix for a key demographic. The detailed test plan (deny → toast → authorize → works) suggests rigorous QA behind this.
2. **Security & Trust ([PR #1962](https://github.com/netease-youdao/LobsterAI/pull/1962))**: The ability to hot-toggle a security monitor plugin reflects user anxiety around agent autonomy. Expect more user-facing security controls in future releases.
3. **Browsing Reliability ([PR #2023](https://github.com/netease-youdao/LobsterAI/pull/2023))**: Repeated attention to the browser/webfetch tool is a strong proxy signal that this is the No. 1 pain point for agent users.

## 5. Bugs & Stability

The high velocity of fixes today indicates a focused stabilization sprint.

| Severity | Issue | Status | Patch |
|---|---|---|---|
| **HIGH** | Browser/Webfetch tool failure / low success rate | Closed | [PR #2023](https://github.com/netease-youdao/LobsterAI/pull/2023) |
| **HIGH** | Model switch error when custom models configured | Closed | [PR #2032](https://github.com/netease-youdao/LobsterAI/pull/2032) |
| **HIGH** | OpenClaw compaction retries and tool result gaps | Closed | [PR #2015](https://github.com/netease-youdao/LobsterAI/pull/2015) |
| **MEDIUM** | macOS voice input silent failure (permission denied) | Closed | [PR #1952](https://github.com/netease-youdao/LobsterAI/pull/1952) |
| **MEDIUM** | Markdown preview local resource path broken | Closed | [PR #2002](https://github.com/netease-youdao/LobsterAI/pull/2002) |
| **MEDIUM** | Artifact HTML preview shows "Not Found" for invalid files | Closed | [PR #2022](https://github.com/netease-youdao/LobsterAI/pull/2022) |
| **LOW** | OpenClaw gateway restarts on every token refresh | Closed | [PR #2018](https://github.com/netease-youdao/LobsterAI/pull/2018) |
| **LOW** | Qwen coding plan mismatched format for new model | Closed | [PR #2035](https://github.com/netease-youdao/LobsterAI/pull/2035) |
| **LOW** | Anthropic format incompatibility (Mimo model) | Closed | [PR #2000](https://github.com/netease-youdao/LobsterAI/pull/2000) |

All identified bugs from this period have been addressed with merged patches.

## 6. Feature Requests & Roadmap Signals

Based on what shipped today, three clear roadmap vectors emerge:

- **Platform Ecosystem (Expert Kit Store):** The release of v2026.6.1 marks a strategic pivot toward a marketplace architecture. Future releases will likely focus on storefront UI, author tooling, plugin rating systems, and usage analytics.
- **Inference Control (Thinking Level):** The Thinking Level Selector aligns with the industry trend of inference-time scaling ("test-time compute"). Expect deeper integration with session presets, cost controls, and model-specific adherence.
- **Agent Reliability (Browsing & Tools):** The sheer volume of patches to the browser/webfetch and OpenClaw subsystems suggests the team is laying groundwork for more ambitious autonomous workflows (e.g., multi-step research, form filling). The security toggle will likely be extended into a full audit/role-based access system.

## 7. User Feedback Summary

Inferred pain points and satisfaction drivers based on prioritized fixes:

- **Satisfaction Drivers:**
    - The agent is measurably more reliable (fewer browser failures, stable gateway).
    - The plugin ecosystem is now open to `npm`/`clawhub` sources, giving developers more freedom.
    - Security features are becoming visible and controllable by the user.
- **Pain Points Addressed:**
    - Mac users were experiencing silent failures with voice input.
    - Power users with custom model configurations faced blocking crashes.
    - Artifact users had broken previews and missing local images.
    - IM bot management was cumbersome and poorly labeled.

## 8. Backlog Watch

**Status: Clean slate.** The provided data shows **zero issues** updated in the last 24 hours and **zero items** in the Latest Issues list. This is an exceptionally strong signal that the development team has successfully cleared their active issue queue, likely as part of the release cycle for v2026.6.1. No long-dormant or unanswered items could be identified from this data feed.

We recommend monitoring the next snapshot to confirm whether this represents a sustained state or a temporary data artifact on release day.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — June 2, 2026

### 1. Today’s Overview

The Moltis project showed a healthy development cadence on June 1, closing three pull requests while recording zero new issues or bug reports. Activity focused squarely on core infrastructure: a significant refactor of the provider abstraction layer, final integration of a third major provider, and a targeted stability fix for OpenAI’s Codex endpoint. The absence of new issues suggests stable maintenance, though it could also reflect a lull in external community reporting. Overall, the project is making clear, deliberate progress toward a more modular, explicitly-capable provider ecosystem.

### 2. Releases

No new releases were published today. The features merged in the last 24 hours (NEAR AI Cloud provider, Codex tool-call fix, and provider capability refactor) reside on the main branch and will likely be batched into an upcoming minor release.

### 3. Project Progress

Three pull requests were merged, advancing both architecture and model coverage:

- **[PR #1090: refactor(providers): use explicit OpenAI capabilities](https://github.com/moltis-org/moltis/pull/1090)** (author: penso) — A foundational architectural improvement that replaces fragile heuristic checks (inferring capabilities from provider URLs or names) with an explicit capability policy system. Built-in providers are wired with known capabilities, while custom providers receive strict defaults. The PR also includes regression tests to prevent regressions in provider URL and model name handling.

- **[PR #1031: Add NEAR AI Cloud provider](https://github.com/moltis-org/moltis/pull/1031)** (author: PierreLeGuen) — A major ecosystem expansion integrating NEAR AI Cloud as a first-class OpenAI-compatible provider. It uses the `NEARAI_API_KEY` environment variable, auto-discovers models from the `/v1/model/list` catalog, and surfaces TEE (Trusted Execution Environment) awareness, positioning Moltis for secure, verifiable agent execution.

- **[PR #1088: [codex] Handle OpenAI Codex final tool-call arguments](https://github.com/moltis-org/moltis/pull/1088)** (author: s-salamatov) — A stability fix for the OpenAI Codex provider. It now correctly records `response.function_call_arguments.done` payloads and synthesizes a streaming argument delta when the final arguments arrive without preceding deltas, preventing missing-argument errors in coding-agent workflows.

### 4. Community Hot Topics

The digest period recorded zero comments across the three merged PRs, making it a quiet day for active discussion. The most significant underlying topic remains *provider ecosystem expansion and reliability*.

**[PR #1031 (NEAR AI Cloud)](https://github.com/moltis-org/moltis/pull/1031)** spent eleven days open, implying substantive review. Its inclusion of TEE capabilities signals growing community interest in secure, verifiable execution environments beyond standard cloud APIs.

**[PR #1090 (Explicit Capabilities)](https://github.com/moltis-org/moltis/pull/1090)** addresses a long-standing developer pain point: the brittleness of implicit provider detection. The community likely benefits significantly from a system where custom providers no longer break due to URL pattern matching or internal naming conventions.

### 5. Bugs & Stability

No new bugs were formally reported via issues today.

The primary stability improvement came from **[PR #1088](https://github.com/moltis-org/moltis/pull/1088)** , which addresses a medium-severity bug in the OpenAI Codex provider. The endpoint could fail to stream tool-call arguments correctly, leading to silent failures or malformed tool calls during autonomous coding agent loops. By synthesizing missing argument deltas and ensuring empty diagnostic strings continue flowing, this fix closes a critical edge case.

Additionally, **[PR #1090](https://github.com/moltis-org/moltis/pull/1090)** included dedicated regression tests, strengthening baseline stability against future changes to provider logic.

### 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today, but the merged PRs provide strong roadmap signals:

- **Capability-Driven Architecture:** PR #1090 signals a full shift toward an explicitly defined capability system. Future providers will likely define their capabilities (streaming, tools, vision, TEE) declaratively rather than inheriting them from heuristic API matches.

- **TEE and Secure Compute:** The NEAR AI Cloud integration (PR #1031) surfaces TEE awareness as a first-class concern. This could become a key differentiator, positioning Moltis for enterprise and decentralized workloads requiring verified execution.

- **Code Agent Robustness:** The Codex fix (PR #1088) shows the team is actively supporting autonomous coding agents, which depend on highly reliable tool-call streaming. This use case appears to be a core design driver.

### 7. User Feedback Summary

Direct user feedback is absent from this snapshot: no issues and no PR comments were recorded in the 24-hour window.

Indirect signals are positive. All three PRs were merged without objection, implying CI and peer review passed cleanly. The focused investment in the Codex provider (PR #1088) and the addition of NEAR AI Cloud (PR #1031) suggest that coding-agent workflows and secure, decentralized infrastructure are the primary use cases driving current development.

### 8. Backlog Watch

The project currently shows **zero open issues and zero open pull requests**, indicating a perfectly clean backlog. While this is unusual for a project of Moltis’s maturity, it reflects either exceptionally rapid triage by the maintainers or a natural sync point in the release cycle. No maintenance debt or stalled items are visible in this digest period.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# QwenPaw Project Digest – 2026-06-02

## 1. Today's Overview
QwenPaw saw intense community and development activity in the past 24 hours, with **50 issues** and **37 pull requests** updated. The project shipped **two new releases** (v1.1.10 and v1.1.10-beta.2) while the community actively debated the upcoming AgentScope 2.0 migration and reported several workspace-breaking regressions. Of the 50 updated issues, 32 remain open/active and 18 were closed, indicating maintainers are actively triaging. The high volume of bug reports around configuration loss, process accumulation, and cron job management suggests a slightly unstable period following the v1.1.9 to v1.1.10 ramp-up.

## 2. Releases
Two new versions were published:

- **v1.1.10** ([view release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.10)): Introduces a `spawn_subagent` tool for ephemeral in-workspace sub-agent execution (feature PR [#4806](https://github.com/agentscope-ai/QwenPaw/pull/4806)) and adds an "Open Directory" tab in Coding Mode. This significantly expands the tool ecosystem for recursive agentic patterns.

- **v1.1.10-beta.2** ([view release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.10-beta.2)): Patches the website header style and fixes the skill enable/disable toggle persistence (PR [#4812](https://github.com/agentscope-ai/QwenPaw/pull/4812)).

*No breaking changes explicitly documented in these releases.*

## 3. Project Progress
The merged and closed pull requests reflect ongoing stabilization and quality-of-life improvements:

- **Cron UX**: PR [#4803](https://github.com/agentscope-ai/QwenPaw/pull/4803) (refactored, merged) disables intrusive push notifications for agent-type cron jobs.
- **Context Window Config**: PR [#4827](https://github.com/agentscope-ai/QwenPaw/pull/4827) (fix, closed) adds a `ProviderManager` fallback to correctly read user-configured `max_input_length`, fixing a context compression threshold calculation bug.
- **Release Admin**: PR [#4867](https://github.com/agentscope-ai/QwenPaw/pull/4867) (chore, merged) bumps version and formalizes release notes.
- **Channel Fixes**: A fix for stale channel restart logic is under development in PR [#4884](https://github.com/agentscope-ai/QwenPaw/pull/4884), addressing the reported issue with custom channels stopping on save.

## 4. Community Hot Topics
- **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)): The most strategically significant discussion, with high upvote count (+2) and 5 comments. The community is formally proposing the transition and a WIP PR ([#4846](https://github.com/agentscope-ai/QwenPaw/pull/4846)) is already open. A separate closed question ([#4885](https://github.com/agentscope-ai/QwenPaw/issues/4885)) confirms broad interest in the direction.
- **Model Configuration Loss** ([#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666)): 6 comments. Users report models configuration being wiped on new session creation, forcing a full restart. High friction point for daily users.
- **Orphaned Cron Jobs** ([#4649](https://github.com/agentscope-ai/QwenPaw/issues/4649)): 6 comments, now closed. Ghost tasks were found to run indefinitely due to stale internal APScheduler state when `jobs.json` was updated.
- **Browser Launch Failure** ([#4731](https://github.com/agentscope-ai/QwenPaw/issues/4731)): 2 comments. Users on Windows 11 report Edge exits with code 21 immediately upon browser launch.

## 5. Bugs & Stability

**Critical**:
- **Single job crashing workspace** ([#4835](https://github.com/agentscope-ai/QwenPaw/issues/4835)): A single missing required field (e.g., `session_id`) in `jobs.json` prevents the entire workspace from starting. No fix PR detected yet.

**High**:
- **MCP process accumulation** ([#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)): MCP server processes survive across QwenPaw restarts, leading to process pileups and slow console loading. Community member reports 9 `firecrawl-mcp` processes after multiple restarts.
- **Browser / temp directory locks on Windows** ([#4844](https://github.com/agentscope-ai/QwenPaw/issues/4844)): Residual processes and locked directories persist after browser sessions end, blocking backups. A fix PR ([#4853](https://github.com/agentscope-ai/QwenPaw/pull/4853)) is open and in review.
- **Context Inflation** ([#4872](https://github.com/agentscope-ai/QwenPaw/issues/4872)): New sessions load raw, uncompressed history, bypassing the compression threshold and causing unbounded context growth.

**Medium**:
- **Custom channel stops listening** ([#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877)): The `replace_channel` method starts a new channel before stopping the old one, causing port binding failures and silent listener loss. Fix PR [#4884](https://github.com/agentscope-ai/QwenPaw/pull/4884) is open.
- **v1.1.9 message unresponsiveness** ([#4864](https://github.com/agentscope-ai/QwenPaw/issues/4864), closed): Users reported no response to inputs after upgrading; likely a configuration compatibility issue that has been addressed.

## 6. Feature Requests & Roadmap Signals
The project's immediate roadmap appears focused on three themes:

1. **AgentScope 2.0 Backend** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727), [#4885](https://github.com/agentscope-ai/QwenPaw/issues/4885)): The community and maintainers are aligning on a major architectural shift to AgentScope 2.0, which will bring a new runtime model and API surface.
2. **Provider Expansion**: PRs for Xiaomi MiMo Token Plan ([#4722](https://github.com/agentscope-ai/QwenPaw/pull/4722)) and MiniMax M3 models ([#4881](https://github.com/agentscope-ai/QwenPaw/pull/4881)) show a clear push to support major Chinese AI providers, alongside feature requests for better OpenAI `extra_body` injection ([#4689](https://github.com/agentscope-ai/QwenPaw/pull/4689)) and reasoning effort control ([#4814](https://github.com/agentscope-ai/QwenPaw/issues/4814)).
3. **Agent-Scoped Auth** ([#4859](https://github.com/agentscope-ai/QwenPaw/issues/4859)): A request for multi-tenant web login accounts signals enterprise deployment maturing.

*Predictions for vNext*: The next major release will almost certainly center on the AgentScope 2.0 migration. We also expect token usage visibility (PR [#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433), under review) to land soon given strong user interest.

## 7. User Feedback Summary
- **Upgrade Regressions**: Multiple users report settings lost on upgrade—skills re-enable themselves ([#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807), closed), virtual environments are reset by install scripts ([#4875](https://github.com/agentscope-ai/QwenPaw/issues/4875)), and model configs vanish ([#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666)). This indicates a need for robust migration and state-preservation logic.
- **Task Queue Frustration**: A user notes that new tasks cannot be queued while a prior inference is running—they must manually stop the current task first ([#4714](https://github.com/agentscope-ai/QwenPaw/issues/4714), closed). Coupled with cron job maintenance issues, this points to a core scheduling UX gap.
- **Desktop UX**: The WebView font is too small for extended use ([#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154)), the window does not restore the last agent/conversation on restart ([#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733)), and file downloads via Tauri are unsupported ([#4874](https://github.com/agentscope-ai/QwenPaw/issues/4874), closed).

## 8. Backlog Watch
Several important items lack sufficient maintainer traction:

- **Font Size Feature** ([#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154)): Opened May 9, this long-standing quality-of-life issue has 2 comments and no assigned milestone or fix PR. Given daily driver complaints about eye strain, this merits more attention.
- **Token Usage Display** ([#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433)): This PR has been in "Under Review" state since May 15 without merging. It provides per-turn token usage and context window stats—highly visible to end users.
- **Desktop Window State Restoration** ([#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733)): Opened May 27, reports that the Windows desktop app fails to show the previously active agent and conversation on restart. No fix PR currently linked.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

Here is the ZeptoClaw project digest for June 2, 2026.

---

### ZeptoClaw Project Digest | 2026-06-02

### 1. Today's Overview

ZeptoClaw entered a high-velocity stabilization cycle today, with **18 PRs updated** and **17 merged/closed** in the last 24 hours. The bulk of activity was driven by a comprehensive dependency sweep that unblocked CI across the repository following a critical RUSTSEC advisory outbreak. A long-awaited fix for a provider routing bug that caused a 100% error rate on certain self-hosted model endpoints was finally merged. Activity is tightly focused on hardening CI infrastructure and managing binary bloat, with the maintainer proactively auditing an ~800KB binary size drift. The project is in a clear “quality and CI gate” phase.

### 2. Releases

**No new releases** were cut in this period. The project remains on the previously established stable baseline.

### 3. Project Progress

17 pull requests were closed, signaling significant forward momentum on internal infrastructure and critical bug fixes.

- **Critical Provider Fix Landed:** The highly anticipated fix for **`fix(providers): keyword fallback must not claim unconfigured provider`** ([PR #592](https://github.com/qhkm/zeptoclaw/pull/592) / [PR #610](https://github.com/qhkm/zeptoclaw/pull/610)) was merged. This resolves a regression where model IDs (e.g., `openai/gpt-oss-120b`) would map to an unconfigured provider via keyword matching, causing total request failure.
- **CI Unblocked:** **`chore(deps): clear RUSTSEC advisories (lettre 0.11.22, diesel 2.3.8)`** ([PR #594](https://github.com/qhkm/zeptoclaw/pull/594)) patched the zero-tolerance advisory config, restoring green checks on **Security audit** and **Cargo deny** jobs.
- **Dependency Sweep (Merged):**
    - **Language Runtime:** Rust bumped from `1.93-slim-trixie` to `1.95-slim-trixie` ([PR #596](https://github.com/qhkm/zeptoclaw/pull/596)).
    - **Rust Libraries:** `mail-parser`, `uuid`, `bcrypt`, `tower-http`, `clap` all bumped.
    - **JavaScript / Docs:** `astro` and `@astrojs/starlight` updated across both `/landing/r8r/docs` and `/landing/zeptoclaw/docs`; `eslint` bumped to v10.3.0 in `/panel`.
    - **CI Actions:** `taiki-e/install-action` and `EmbarkStudios/cargo-deny-action` updated.

### 4. Community Hot Topics

The central conversation revolves around **binary size management**.

- **Issue #612** ([link](https://github.com/qhkm/zeptoclaw/issues/612)): `[chore, P2-high] chore(perf): audit ~800KB binary-size drift since 6.2MB low water mark, tighten gate to 7MB`
    - **Context:** The stripped binary on darwin-arm64 sits at **6.98MB**, leaving only 21KB of breathing room before hitting the strategic 7MB target.
    - **Need:** Deep audit to identify where the bloat entered.
- **PR #611** ([link](https://github.com/qhkm/zeptoclaw/pull/611)): `chore(ci): promote binary-size to PR gate at 7.5MB`
    - **Response:** Proposed tactical solution to immediately gate the binary at 7.5MB (to unblock development) while the audit runs.

**Analysis:** There is strong developer focus on shipping a lean binary. This is a developer-driven initiative (no user complaints visible in the data), but it signals a high standard for project quality and deployment efficiency.

### 5. Bugs & Stability

| Severity | Status | Item | Description |
|---|---|---|---|
| **Critical** | **Fixed** | Provider Keyword Fallback ([PR #592](https://github.com/qhkm/zeptoclaw/pull/592)) | `infer_provider_name_for_model` ignored `available_providers` in its final fallback, causing a 100% error rate for users running NIM-served models. |
| **High** | **Active** | Binary Size Drift ([Issue #612](https://github.com/qhkm/zeptoclaw/issues/612)) | An 800KB bloat was detected. Being investigated before the CI gate is tightened. |
| **Infrastructure** | **Fixed** | RUSTSEC CI Red Alert ([PR #594](https://github.com/qhkm/zeptoclaw/pull/594)) | New advisories blocked all PRs. Resolved by bumping `lettre` and `diesel`. |

### 6. Feature Requests & Roadmap Signals

There are no explicit user feature requests in this snapshot. However, the roadmap signals are strong:

- **Operational Excellence:** The rush to harden CI (binary size gates, advisory handling) indicates the next phase of development will prioritize contributor workflow efficiency and release reliability.
- **Provider System Stability:** The deep architectural fix to the provider router ([PR #592](https://github.com/qhkm/zeptoclaw/pull/592)) suggests the multi-provider routing layer is a critical path for future feature development. Expect more features built on top of a stable provider abstraction.

### 7. User Feedback Summary

Direct user feedback is minimal in this data window, but the fixes speak directly to a specific, painful use case:

- **Pain Point Resolved:** The provider keyword bug ([PR #592](https://github.com/qhkm/zeptoclaw/pull/592)) was originally reported by a user (Sisuthros) running a self-hosted NIM instance. The model `openai/gpt-oss-120b` was completely non-functional due to a false positive provider match. The merge of this fix directly restores functionality for users running non-standard or custom OpenAI-compatible endpoints.

### 8. Backlog Watch

The most notable item was the **Provider Bug Fix PR** ([PR #592](https://github.com/qhkm/zeptoclaw/pull/592)), which sat open for **12 days** (since May 20). The delay was not due to neglect, but technical friction: the original fork PR could not be rebased via `gh`, and CI demanded the exact dependency bumps from [#594](https://github.com/qhkm/zeptoclaw/pull/594) and [#604](https://github.com/qhkm/zeptoclaw/pull/604) to pass. This highlights a critical process risk in the backlog—fragile CI configuration can inadvertently gate critical bug fixes for weeks. No other items in the current 24-hour snapshot appear to be languishing.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is your structured digest for ZeroClaw based on the latest GitHub data.

---

## ZeroClaw Project Digest — 2026-06-02

### 1. Today’s Overview
ZeroClaw maintained exceptionally high development velocity over the last 24 hours, with **36 issues** and **37 pull requests** active. While no new release was cut, the project is firmly in a stability and hardening cycle. The significant volume of merged PRs—**13 closed/merged**—indicates a strong sprint focused on security patching (tool allowlists, web fetch DNS), provider compatibility (Kimi, stream recovery), and architectural groundwork (WASI plugin definitions, lean default channels). The surgical response to critical security bugs, particularly the channel tool allowlist bypass (Issue #7063) where a targeted fix was submitted within hours, signals excellent project health and responsive maintainership.

### 2. Releases
**None.** No new versions or tags were published today. The ongoing work suggests a `v0.8.0-beta-2` is being assembled around the massive integration PR [#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848).

### 3. Project Progress
The project closed or merged **13 PRs** in the last 24 hours, representing a strong output of bug fixes, security hardening, and feature delivery.

- **Bug Fixes & Stability (Regressions & Hardening):**
    - **Security:** Hardened the `web_fetch` tool to properly honor private DNS host allowlists ([PR #6974](https://github.com/zeroclaw-labs/zeroclaw/pull/6974)).
    - **Security:** Re-recovered the `image_info` path resolution fix bypassing the path policy gate ([PR #6972](https://github.com/zeroclaw-labs/zeroclaw/pull/6972)).
    - **Runtime:** Restored the stream-error recovery fallback path for provider failures ([PR #6983](https://github.com/zeroclaw-labs/zeroclaw/pull/6983)).
    - **Channels:** Restored date-only prompt context for channel messages to improve caching efficiency ([PR #6931](https://github.com/zeroclaw-labs/zeroclaw/pull/6931)).
    - **Channels:** Redacted Discord outbound delivery failure logs to prevent leaking raw targets ([PR #7031](https://github.com/zeroclaw-labs/zeroclaw/pull/7031)).
    - **Config:** Fixed the email channel to properly ignore blank SMTP credential overrides ([PR #6979](https://github.com/zeroclaw-labs/zeroclaw/pull/6979)).
    - **Providers:** Resolved the Kimi/K2 model "invalid temperature" 400 error by omitting the baseline temperature for fixed-temperature models ([PR #7049](https://github.com/zeroclaw-labs/zeroclaw/pull/7049)).

- **Features & Integrations:**
    - **Web Search:** Merged support for `jina.ai` as a new `web_search` provider ([PR #6833](https://github.com/zeroclaw-labs/zeroclaw/pull/6833)).
    - **Architecture:** Defined a leaner default channel bundle ([PR #6904](https://github.com/zeroclaw-labs/zeroclaw/pull/6904)).
    - **Latency:** Added an opt-out for the reply-intent classifier to save costs in single-bot DMs ([PR #5979](https://github.com/zeroclaw-labs/zeroclaw/pull/5979)).

### 4. Community Hot Topics
The community is highly engaged in shaping the architecture and fixing sharp edges.

- **Token Optimization (#5146):** The top-commented issue ([8 comments](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)) focuses on minimizing LLM cost by "compiling" skill prompts. This reflects strong user concern over the overhead of full SKILL.md injection.
- **Massive Integration Overhaul (#6848):** The largest open PR (tagged `XL`) is the basis for `v0.8.0-beta-2`. It introduces a `zerocode` TUI, RPC socket transport, and new approval flows. The community is closely watching this as the primary roadmap signal for the next major cycle.
- **Provider Friction:** Local and alternative cloud providers remain a key pain point. Ollama tool calling ([Issue #5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)) and Gemini history invariants ([Issue #6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)) continue to draw engagement from the self-hosting segment.
- **Security Bypass (#7063 / #7064):** A critical bug report regarding channel-served agents bypassing the per-agent tool allowlist was met with immediate collaboration. A fix PR was submitted concurrently, demonstrating a strong security culture.

### 5. Bugs & Stability

| Severity | Issue | Summary | Status |
|----------|-------|---------|--------|
| **Critical / P1** | [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | Gemini history serializer invariant violation (400 errors) | In Progress |
| **Critical / P1** | [#6472](https://github.com/zeroclaw-labs/zeroclaw/issues/6472) | Postgres memory backend causes runtime panic | In Progress |
| **Critical / P1** | [#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) | WhatsApp `allowed-numbers` bypassed for LID contacts | In Progress |
| **Critical / P1** | [#7063](https://github.com/zeroclaw-labs/zeroclaw/issues/7063) | Channel agents skip `SecurityPolicy.allowed_tools` filter | Fix in PR [#7064](https://github.com/zeroclaw-labs/zeroclaw/pull/7064) |
| **High / P2** | [#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068) | Telegram channel returns Codex scratchpad as final response | New |
| **High / P2** | [#6683](https://github.com/zeroclaw-labs/zeroclaw/issues/6683) | `skill_manage` patch has no cooldown enforcement | In Progress |
| **High / P2** | [#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155) | Delegate agents always inject full skills (ignore compact mode) | In Progress |
| **Medium / P2** | [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) | Channel runtime commands not localized (hardcoded English) | In Progress |

**Note:** Two critical P1 bugs were closed in this cycle: Kimi temperature rejection ([#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022)) and Email SMTP blank credentials ([#6881](https://github.com/zeroclaw-labs/zeroclaw/issues/6881)).

### 6. Feature Requests & Roadmap Signals

- **Likely for v0.8.0:**
    - **Agent Evaluation Harness (#7065 / #7067):** A Phase 0 proposal for `zeroclaw eval` with deterministic replay was submitted alongside its implementation PR. This is a strong signal that the project is prioritizing agent quality measurement.
    - **WASI Plugin Interface (#7060):** Foundational WIT files for Tool, Channel, and Memory plugins were defined, implementing the intentional architecture plan (FND-001).
    - **Jina AI Provider (#6833):** Already merged, locked for the next release.
    - **Integration Re-architecture (#6848):** The massive PR is the clear headliner for the v0.8 cycle.

- **High Demand Community Wishes:**
    - **Token Consumption (#5146):** Skill compilation remains the top-upvoted feature request by a wide margin.
    - **Discord Channel Filtering (#6378):** High demand from users running bots in large servers.
    - **Install Suggestions (#6289):** Users want proactive discovery of missing skills/plugins.

- **Infrastructure & UX:**
    - **Versioned Documentation (#7023):** A PR for versioned docs and a version selector was updated.
    - **Documentation Reskin (#7055):** A PoC for theming the docs to match the web dashboard was submitted.

### 7. User Feedback Summary

- **Security is the baseline expectation:** The rapid identification and patching of the tool allowlist bypass ([#7063](https://github.com/zeroclaw-labs/zeroclaw/issues/7063)) and web_fetch DNS hole ([#6974](https://github.com/zeroclaw-labs/zeroclaw/pull/6974)) confirms the user base has zero tolerance for permission model gaps. Users are treating ZeroClaw as a secure enterprise agent runtime.
- **Token costs are a daily pain point:** The sustained interest in [#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146) indicates that the "full skill injection" pattern is simply too expensive for heavy users. This is likely blocking broader adoption in cost-sensitive environments.
- **Provider flexibility is fragile:** Users report workflows blocked by local providers (Ollama [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)) and edge cases in "compatible" providers (Gemini [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302), Kimi [#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022)).
- **Positive velocity sentiment:** Despite the high number of bugs, the volume of PRs and rapid regression recovery suggests users see tangible day-to-day improvements.

### 8. Backlog Watch

| Type | Item | Age / Status | Note |
|------|------|--------------|------|
| **Stale PR** | [TLS CA Certs (#5797)](https://github.com/zeroclaw-labs/zeroclaw/pull/5797) | Opened April 16, 2026 | Critical for enterprise/corporate PKI deployments. Needs maintainer review to unblock self-hosted users. |
| **Help Wanted** | [`.well-known` URI Skills (#4853)](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) | Opened March 27, 2026 | Standardization is progressing externally. ZeroClaw risks ecosystem isolation without an owner for this. |
| **Stalled Feature** | [Token Minimization (#5146)](https://github.com/zeroclaw-labs/zeroclaw/issues/5146) | Opened March 29, 2026 | High community desire but complex architecture. Likely slips to v0.9 given the current v0.8 integration focus. |
| **Blocked** | [Node Heartbeat (#6391)](https://github.com/zeroclaw-labs/zeroclaw/issues/6391) | Opened May 5, 2026 | Blocked on liveness semantics. Requires a re-scoping proposal. |
| **Unanswered P1** | [Per-Channel Throttle (#6345)](https://github.com/zeroclaw-labs/zeroclaw/issues/6345) | Opened May 3, 2026 (P1, Accepted) | Critical for WhatsApp paired-identity users. No implementation PR has been linked yet. |

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*