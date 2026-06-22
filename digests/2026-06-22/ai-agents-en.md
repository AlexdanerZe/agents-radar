# OpenClaw Ecosystem Digest 2026-06-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-22 03:54 UTC

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

# OpenClaw Project Digest
**Analyst:** AI Agent & Personal AI Assistant Open-Source Projects
**Source:** [OpenClaw (github.com/openclaw/openclaw)](https://github.com/openclaw/openclaw)
**Date:** 2026-06-22

---

## 1. Today's Overview
Activity remains extremely high, with 500 issues and 500 PRs updated in the last 24 hours. Only 25 issues and 112 PRs were merged or closed, indicating a significant gap between reported problems and resolved ones. The project released **v2026.6.10-beta.1**, a targeted stabilization patch aimed squarely at the session-state corruption and message-loss regressions that have dominated recent reports. Despite this, the open issue count remains at 475, and the prevalence of **P1 Diamond Lobster**-rated regressions suggests the project is in a high-churn stabilization phase where the velocity of regressions is directly challenging maintainer capacity.

---

## 2. Releases

**Latest Release: `v2026.6.10-beta.1`**
- **Focus:** More reliable agent turns and session state.
- **Key Fixes:**
  - Pending subagent completion announcements are now preserved.
  - Chat history transcripts are kept non-empty.
  - Media index alignment is maintained.
  - Dormant follow-up drains are restarted correctly.
  - Compaction model aliases are resolved consistently.
- **Assessment:** This release directly addresses the cluster of `impact:session-state` and `impact:message-loss` bugs that have been the top complaint vector. No explicit breaking changes or migration notes were published in the data provided, but given the nature of the fixes, users on the beta track should update promptly.

---

## 3. Project Progress
Today saw 112 PRs merged or closed. Notable fixtures include:
- **[#94478](https://github.com/openclaw/openclaw/issues/94478) — `fix(doctor): repair legacy Codex route persistence`** (automerge merged).
- High-value P1 PRs moving through the pipeline:
  - **[#95536](https://github.com/openclaw/openclaw/pull/95536)** — Adds a tool-activity heartbeat to keep subagents alive during long tool calls.
  - **[#95652](https://github.com/openclaw/openclaw/pull/95652)** — Fixes agent harness plugin activation order on gateway restart.
  - **[#95628](https://github.com/openclaw/openclaw/pull/95628)** — Fixes Gemini web search freshness handling (`freshness: "day"` failures).
  - **[#78303](https://github.com/openclaw/openclaw/pull/78303)** — Adds channel-mediated approval envelopes for MCP tool calls (major security feature).
  - **[#90239](https://github.com/openclaw/openclaw/pull/90239) / [#90259](https://github.com/openclaw/openclaw/pull/90259)** — Large AI-assisted features adding session history family lookup and carryover summaries across resets.

**Blockers:** A large percentage of PRs remain in "needs proof" or "waiting on author" states, with a growing backlog in "ready for maintainer look," indicating a **maintainer bandwidth constraint** despite high contributor velocity.

---

## 4. Community Hot Topics
Conversation is driven by users hitting hard regressions on production workloads:

- **Telegram Duplication ([#86519](https://github.com/openclaw/openclaw/issues/86519), 10 comments):** Long-running thread about agent replies duplicating 2–10x on Telegram after the 5.20 update. The 5.22 update reduced severity but didn't fix it.
- **Isolated Cron Blocked ([#91363](https://github.com/openclaw/openclaw/issues/91363), 6 comments, 4 reactions):** A core power-user feature (cron isolated sessions) consistently fails with "LLM request failed." High upvote count signals this is a widespread blocker for automated agent workflows.
- **Memory Migrated Silently ([#95495](https://github.com/openclaw/openclaw/issues/95495), 7 comments):** Strong user emotion around the 2026.6.9 upgrade silently relocating the memory vector store with no migration, forcing a full 1499-file re-embed.
- **Reasoning Leakage ([#91804](https://github.com/openclaw/openclaw/issues/91804), 5 comments):** A privacy and UX regression exposing internal agent thinking directly to users. Significant trust impact.
- **Active Memory Aggression ([#90082](https://github.com/openclaw/openclaw/issues/90082), 5 comments, 2 reactions):** The circuit breaker is too aggressive, polluting main sessions with fallback text.

**Sentiment:** The community is engaged but frustrated. Users are providing detailed reproduction steps and upvoting critical issues, but the pace of P1 regressions is eroding confidence in the 6.x branch.

---

## 5. Bugs & Stability
The bug landscape is heavily concentrated on **session state corruption, message loss, and channel-specific crashes.**

**Critical (P1 — Diamond Lobster / Platinum Hermit):**

| ID | Title | Impact | Fix PR? |
|---|---|---|---|
| [#95495](https://github.com/openclaw/openclaw/issues/95495) | Silent memory store relocation (2026.6.9) | **Data Loss** — Full re-embed required | Not linked |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s compaction timeout has no partial-progress reuse | **Crash Loop** — Legitimate compactions fail identically | Not linked |
| [#92415](https://github.com/openclaw/openclaw/issues/92415) | `AgentSession.this.model` never refreshed after `/model` switch | **State Corruption** — Affects context window, reasoning, thinking | Not linked |
| [#95623](https://github.com/openclaw/openclaw/issues/95623) | `tool_use.id` sanitizer misses OpenAI composite ID on failover | **Session Bricks** — Cross-provider failover introduces fatal `|` character | Not linked |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent repeats identical replies on Telegram (2–10x) | **Message Spam / Loss** — Severe UX regression | Not linked |
| [#93375](https://github.com/openclaw/openclaw/issues/93375) | Telegram polling enters silent crash loop after timeout | **Channel Death** — Health monitor cannot recover | Not linked |
| [#90325](https://github.com/openclaw/openclaw/issues/90325) | Matrix channel dispatch: `TypeError: Cannot read properties of undefined` | **Channel Death** — Regression in v2026.6.1 | Not linked |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | Isolated cron fails: LLM request never reaches provider | **Feature Blocked** — Cron automation broken | Not linked |
| [#91804](https://github.com/openclaw/openclaw/issues/91804) | Internal reasoning leaked to users | **Security / Privacy** — Major UX regression | Not linked |
| [#90840](https://github.com/openclaw/openclaw/issues/90840) | Subagent raw output delivered to user instead of parent summary | **Message Leak** — Context/security failure | Not linked |
| [#92460](https://github.com/openclaw/openclaw/issues/92460) | Isolated cron completion announcer drops explicit delivery.channel | **Message Loss** — `Channel is required` error on deliveries | Not linked |

**Assessment:** *At least 11 distinct P1 regressions are live in the wild.* The root causes cluster around the new compaction timeout system, session model snapshots, and cross-provider failover handling. The v2026.6.10-beta.1 release directly targets this cluster, but the volume of issues suggests deeper structural fixes are required.

---

## 6. Feature Requests & Roadmap Signals
User requests are pushing toward structured multi-session, memory safety, and enterprise patterns.

**High Demand Feature Requests:**
- **[#90916](https://github.com/openclaw/openclaw/issues/90916) — Topic-Session Families (P2):** One assistant, multiple named context lanes with shared durable memory. Strong signal for advanced session management.
- **[#90354](https://github.com/openclaw/openclaw/issues/90354) — Bounded/Validated Append for Pre-Compaction Memory Flush (P2):** Hard guardrails against oversized memory appends.
- **[#43564](https://github.com/openclaw/openclaw/issues/43564) — ACP Session Skill Context Injection (P2):** Allow skills to be injected into Codex/Pi/OpenCode/Gemini spawned sessions.

**Predictions for Next Versions:**
- **Immediate (Stabilization):** Continued patching of the compaction timeout, session model snapshot, and cross-provider sanitization bugs.
- **Near Term:** The **Session History Family Lookup** ([#90239](https://github.com/openclaw/openclaw/pull/90239)) and **MCP Consent Envelope** ([#78303](https://github.com/openclaw/openclaw/pull/78303)) are large, well-reviewed features close to merge. These represent a shift toward trust-and-safety infrastructure for autonomous tool use.
- **Medium Term:** **Formal Release Policy** ([#95613](https://github.com/openclaw/openclaw/pull/95613)) was filed today. If adopted, this will introduce a stable/daily/monthly cadence, which directly addresses user complaints about the chaos of the current rapid-beta cycle.

---

## 7. User Feedback Summary

**Pain Points:**
- *"Bot sends 10 identical replies."* (#86519) — Core communication trust is broken.
- *"Memory silently vanished and re-embedded."* (#95495) — Data portability and trust in upgrades.
- *"Internal thoughts exposed publicly."* (#91804) — Privacy/security regression.
- *"Scheduled cron jobs silently fail."* (#91363, #92369) — Power users cannot rely on automation.
- *"Alert fatigue from false cron failure notifications."* (#90595) — Observability noise.
- *"Abandoning droplet — poor UX for background tasks."* (#88087) — Explicit user churn signal.

**Sentiment Assessment:**
The community is deeply technically engaged but experiencing **update fatigue**. Every minor release (5.20 → 5.22 → 6.1 → 6.6 → 6.9 → 6.10-beta) introduces new regressions. Users who rely on channels beyond Discord (Telegram, Matrix, Feishu) and automated workflows (cron, subagents) are bearing the brunt. The rapid iteration is impressive, but without a dedicated stabilization freeze, the project risks a trust spiral as users feel more like beta testers than consumers of a stable product.

---

## 8. Backlog Watch
Several high-impact items are languishing or blocked by maintainer bandwidth.

**Stale Critical Issues:**
- **[#67915](https://github.com/openclaw/openclaw/issues/67915) (April 17, P2) — Local attachments "Unavailable":** A long-standing UX bug affecting local media previews. A fix PR exists but has been stalled for weeks.
- **[#43564](https://github.com/openclaw/openclaw/issues/43564) (March 12, P2) — ACP Skill Context Injection:** A key architectural feature with no progress since March.

**Stalled High-Impact PRs:**
- **[#80726](https://github.com/openclaw/openclaw/pull/80726) (May 11) — Telegram DM topic thread resolution:** Stalled in "waiting on author." Critical for Telegram group chat users.
- **[#75727](https://github.com/openclaw/openclaw/pull/75727) (May 1) — Codex inline media rendering:** Stalled since May. Affects image/tool responses in Codex harness.
- **[#68967](https://github.com/openclaw/openclaw/pull/68967) (April 19) — Google Chat session thread binding:** Stalled. Impacts Google Chat users heavily.

**Maintainer Capacity Indicator:**
A large number of PRs sit in "ready for maintainer look" without movement (e.g., [#81857](https://github.com/openclaw/openclaw/pull/81857), [#89583](https://github.com/openclaw/openclaw/pull/89583), [#95652](https://github.com/openclaw/openclaw/pull/95652)). Despite high contributor activity, the triage-to-merge cycle shows significant strain, which is the primary constraint on resolving the massive P1 backlog.

---

**Project Health Score:** ⚠️ **Caution** (High activity, critical regression density, strained resolution pipeline)

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Personal AI Agent & Assistant Open-Source Landscape | 2026-06-22**

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem on June 22, 2026 displays a landscape of hyper-competitive iteration tempered by mounting stability and security pressures. Projects cluster into distinct tiers: platform-scaling feature factories (IronClaw, ZeroClaw), stabilization-focused integrators (NanoBot, PicoClaw), and high-churn orchestrators struggling with regression density (OpenClaw, CoPaw). A shared ecosystem identity crisis is forming around provider dependence, with the sudden Google Gemini CLI sunset causing cascading fallout across Hermes Agent and ZeroClaw. Simultaneously, security has transitioned from a feature to a gating requirement, as critical MCP and A2A vulnerabilities force immediate trust-boundary hardening across NanoBot, NanoClaw, and LobsterAI. The core tension is clear: contributor velocity is systematically outstripping core team capacity, with maintainer bandwidth emerging as the binding constraint on ecosystem-wide progress.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 updated | 500 updated | v2026.6.10-beta.1 | ⚠️ Caution — High regression density, strained triage |
| **ZeroClaw** | 50 updated | 50 updated | v0.8.2/3 in active dev | ✅ Strong — Modular architecture, clear roadmap |
| **IronClaw** | 6 active | 29 updated | None today | ✅ Strong — CI-led maturation, dogfooding culture |
| **CoPaw (QwenPaw)** | 18 active | 37 updated | v1.1.12 | ⚠️ Vibrant but buggy — Regression influx post-upgrade |
| **Hermes Agent** | 50 updated | 50 updated | v0.17.0 expected | ⚠️ High activity / review bottleneck |
| **PicoClaw** | 6 active | 32 updated (29 merged) | v0.3.0-nightly | ✅ Good — Responsive maintainers, 2 critical open bugs |
| **NanoBot** | 10 active | 39 updated | v0.2.2 in review | ✅ Good — Security incident response is rapid |
| **NanoClaw** | 2 critical | 5 updated | None | ✅ Good — Security architecture under review |
| **LobsterAI** | 1 active | 0 | None | 🔴 Stable but stalled — SSRF advisory unaddressed |
| **NullClaw** | 1 active | 0 | v2026.5.29 | 🔴 Fragile — Single blocking bug, no fix PR |
| **ZeptoClaw** | 0 | 1 closed | None | ✅ Stable — CI hardening phase |
| **TinyClaw** | 0 | 0 | — | 💤 Dormant |
| **Moltis** | 0 | 0 | — | 💤 Dormant |

*Note: Intersection of "issues/PRs updated" and "active issues" varies per project's digest methodology. Volumes represent relative order of magnitude.*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale and breadth**: The largest raw community engagement and the widest feature surface (session state, MCP, channels, compaction, cron, subagent orchestration). No single project covers more ground.
- **Reference status**: As the ecosystem's core reference implementation, OpenClaw defines the architectural canon against which others differentiate.

**Technical Approach Differences:**
- OpenClaw employs a monolithic, tightly coupled orchestration engine. In contrast, **ZeroClaw** modularizes via WASM plugins and per-agent tool scoping; **IronClaw** is rebuilding concurrently with its "Reborn" runtime; **CoPaw** emphasizes a data-analysis plugin ecosystem (`datapaw`). OpenClaw's architecture prioritizes raw capability breadth over modular isolation.

**Community Size Comparison:**
- OpenClaw has the highest absolute engagement (500 issues/500 PRs) but is experiencing clear user frustration ("update fatigue," "trust spiral"). **IronClaw** and **ZeroClaw** show higher *effective* momentum with better merge rates and clearer roadmaps. **Hermes Agent** demonstrates very high contributor loyalty (6+ patches from a single contributor today). **CoPaw** has a large, vocal user base (likely dominant in Asian mobile markets) but suffers regression density similar to OpenClaw.

**Strategic Assessment:**
OpenClaw's first-mover advantage in community size is actively threatened by its inability to contain regressions. The maintainer bandwidth constraint explicitly noted in the digest—where "PRs sit in 'ready for maintainer look' without movement"—is the defining bottleneck. The proposed formal release policy (PR #95613) is a direct acknowledgment of this existential risk.

---

## 4. Shared Technical Focus Areas

Several cross-cutting requirements are emerging across independent projects, indicating consensus on the hardest problems:

| Focus Area | Projects Involved | Specific Needs |
|---|---|---|
| **Agent & Tool Security Isolation** | NanoBot, NanoClaw, ZeroClaw, LobsterAI, OpenClaw | MCP allowlist enforcement (#4434 NanoBot), A2A sandbox escape prevention (#2828 NanoClaw), SSRF guard validation (#2181 LobsterAI, #5918 ZeroClaw), approval transparency (#2827 NanoClaw) |
| **Provider Resilience & Heterogeneity** | Hermes Agent, ZeroClaw, OpenClaw, CoPaw | Emergency migration paths from deprecated providers (Gemini CLI), cross-provider failover (tool_id sanitization #95623 OpenClaw), custom provider compatibility (OpenAI-compatible tool calling #5345 CoPaw) |
| **Memory & Context Architecture** | IronClaw, NanoBot, OpenClaw, CoPaw | Learning systems & reflection (IronClaw WS-1/3), agent-driven memory queries (search_history #4440 NanoBot), session history families (#90239 OpenClaw), context explosion protection (#5342 CoPaw) |
| **Channel Maturation** | OpenClaw, CoPaw, Hermes Agent, NanoBot, PicoClaw | Message deduplication (Telegram #86519 OpenClaw), mobile responsive UI (CoPaw CSS wave), multi-bot routing (#10452 Hermes), group allowlists (DingTalk #4206 NanoBot), Matrix ID parsing (#3044 PicoClaw) |
| **Update & Release Reliability** | OpenClaw, CoPaw, NanoClaw, NullClaw | Formal release policies (#95613 OpenClaw), upgrade path without regression (#5262 CoPaw skills re-enable), deterministic skill updates (#2826 NanoClaw), hotfix response cycles (#967 NullClaw) |

---

## 5. Differentiation Analysis

| Strategic Vector | OpenClaw | IronClaw | ZeroClaw | CoPaw | Hermes Agent | NanoBot/NanoClaw/PicoClaw |
|---|---|---|---|---|---|---|
| **Target User** | Power user / orchestrator | Enterprise / Desktop hybrid | Developer / Platform builder | Analyst / Asian mobile user | Power user / Desktop advocate | Hobbyist / Channel integrator |
| **Architecture Philosophy** | Monolithic orchestration | Reborn concurrent runtime | WASM plugin sandbox | Plugin ecosystem (datapaw) | Desktop-centric TUI/App | Lightweight focused stacks |
| **Best-in-Class Feature** | Breadth of subsystems | Learning system & CI gating | Modular isolation & OTel | Mobile responsiveness | Desktop Kanban/localization | Security response / Channel depth |
| **Primary Risk Factor** | Regression density | E2E nightly failures | WASM security gating v0.8.2 | Upgrade regression | Provider dependency crisis | Scope limitation |
| **Community Maturity Signal** | Formal release policy proposed (#95613) | Dogfooding sprints (#5119) | Project governance RFC (#6808) | Stabilization demands (#5360) | Contributor loyalty (6 patches/cycle) | Security advisory turnaround |

**Architectural Divergence:**
- **IronClaw** and **ZeroClaw** are betting on platform rewrites (Reborn, WASM) over incremental improvement, signaling a belief that current architectures cannot scale.
- **OpenClaw** and **Hermes** represent incremental improvement at scale, prioritizing feature velocity over architectural purity.
- **NanoBot**, **NanoClaw**, and **PicoClaw** operate in deliberately constrained scopes, achieving higher reliability per feature by saying "no" to more.

---

## 6. Community Momentum & Maturity

**Tier 1 — Feature Factories (High Risk / High Velocity):**
- **IronClaw, ZeroClaw, OpenClaw, CoPaw (QwenPaw)**
- These four drive the majority of ecosystem code and issue volume. IronClaw and ZeroClaw exhibit highest *process maturity* (dogfooding, merge gates, design documents). OpenClaw and CoPaw exhibit highest *community chaos* (regression density, "stabilize first" user sentiment). IronClaw and ZeroClaw are rapidly iterating *toward* stabilization; OpenClaw and CoPaw are iterating *through* regressions.

**Tier 2 — Targeted Growth / Consolidation:**
- **NanoBot, Hermes Agent, PicoClaw, NanoClaw**
- These projects manage scope deliberately. Hermes is in a painful but necessary provider migration. NanoBot is converging on v0.2.2 with a security-first posture. PicoClaw is merging heavily for a v0.3.0 stable release. NanoClaw is defining A2A security standards.

**Tier 3 — Maintenance / Latent:**
- **LobsterAI, NullClaw, ZeptoClaw**
- Low code cadence. LobsterAI has an unaddressed SSRF vulnerability. NullClaw cannot resolve its single blocking bug. ZeptoClaw is purely in CI/Ops mode.

**Dormant:**
- **TinyClaw, Moltis** — No activity in 24 hours.

---

## 7. Trend Signals

**1. Provider Agnosticism is Non-Negotiable**
The Google Gemini CLI sunset (June 18) is a watershed event. Hermes Agent (#29294, #49701) and ZeroClaw (#4879) faced immediate workflow collapse. Developers must decouple from single-provider SDKs via adapter layers. Projects investing in robust cross-provider failover (OpenClaw #95623) and transparent migration paths will capture fleeing users.

**2. Security is the Gating Feature for Autonomous Agents**
Three independent disclosures this cycle—MCP bypass (NanoBot #4434), A2A symlink escape (NanoClaw #2828), SSRF weakening (LobsterAI #2181)—mark a shift from "move fast" to "isolate everything." Approval UIs must show full runtime context (NanoClaw #2827). WASM plugin sandboxes must default-closed (ZeroClaw #5918). **The market is penalizing permissive defaults.**

**3. Memory is the New Competitive Moat**
IronClaw's Learning System (confidence-scored memory documents, post-turn reflection) represents the most ambitious play. Pair this with agent-driven memory recall (NanoBot `search_history`) and session families (OpenClaw). The standard is no longer "does it remember the conversation?" but "does it learn from its mistakes and query its own knowledge?"

**4. Desktop is a Distribution Strategy, but Platform Execution is Failing**
Hermes Desktop, IronClaw Workbench, and OpenClaw Desktop signal strong demand for native experiences. However, the ecosystem is failing at cross-platform reliability: arm64-only Mac builds (Hermes #37505), broken Windows zoom (#37917), broken Windows updates (ZeroClaw #7853). Desktop is a high-risk, high-reward channel.

**5. WASM as the Universal Plugin Runtime is Ecosystem-Scale Bet**
ZeroClaw's v0.8.2 gating on WASM plugin program and SSRF protection is the clearest signal yet that the ecosystem is ready for language-agnostic, sandboxed plugin architectures. If ZeroClaw ships safely, expect every other orchestrator (OpenClaw, Hermes, CoPaw) to follow.

**6. Community Governance is the Binding Constraint on Growth**
ZeroClaw's governance RFC (#6808), OpenClaw's release policy (#95613), and CoPaw's "stabilize first" user movement (#5360) all point to the same conclusion: **the rate-limiting factor for ecosystem progress is no longer code—it is triage process, CI engineering, and maintainer capacity.** Projects that invest in merge gates (IronClaw), clear communication, and contributor pathways will compound their community advantage; those that don't will fragment under the weight of their own pull requests.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **June 22, 2026**, based on the provided GitHub data.

---

## 1. Today’s Overview
The NanoBot project is in a high-velocity stabilization phase as it converges on the **v0.2.2** release. Activity is intense: 39 pull requests were updated in the last 24 hours (15 merged/closed, 24 actively open), alongside 10 issues. The community’s focus today is squarely on **security**—closing a critical MCP allowlist bypass discovered this weekend—and **stability**, with multiple fixes converging for the session-bricking duplicate `tool_use` bug. On the feature side, strong contributions to DingTalk, Telegram, and an agent-facing `search_history` tool signal growing maturity in both the channel abstraction and memory subsystems. No new release dropped today, but the chore PR for v0.2.2 ([#4445](https://github.com/HKUDS/nanobot/pull/4445)) is already in review.

## 2. Releases
**None.** No new releases were published today. The next expected release is **v0.2.2** ([PR #4445](https://github.com/HKUDS/nanobot/pull/4445)), which will bump the package version, update the changelog, and is flagged to include the top-priority MCP security fix and the streaming deduplication patch. No breaking changes or specific migration notes have been documented yet.

## 3. Project Progress
Several substantive features and stability patches advanced or were merged today:

- **DingTalk Channel Maturation:** PR [#4206](https://github.com/HKUDS/nanobot/pull/4206) (feat: add `group_allow_from` for group chat allowlist) was **merged**. A follow-up ([#4446](https://github.com/HKUDS/nanobot/pull/4446)) adding private chat gating and sender mentions was opened.
- **Memory & Agent Recall:** A new read-only `search_history` tool was proposed ([Issue #4440](https://github.com/HKUDS/nanobot/issues/4440), [PR #4439](https://github.com/HKUDS/nanobot/pull/4439)) and progressed. The opt-in eager memory consolidation feature ([PR #4402](https://github.com/HKUDS/nanobot/pull/4402)) also saw activity.
- **WebUI & Onboarding:** Work continued on the WebUI slash palette for skill activation ([#4284](https://github.com/HKUDS/nanobot/pull/4284)) and the new `nanobot onboard --wizard` flow ([#4395](https://github.com/HKUDS/nanobot/pull/4395)).
- **Tool Microcompaction:** PR [#4392](https://github.com/HKUDS/nanobot/pull/4392) added a config flag (`microcompactToolResults`) enabling cache-sensitive deployments to disable dynamic tool-result compression.
- **Pairing Store Fix:** A type-coercion bug in the pairing store that could silently deny cross-channel user identity resolution was patched ([#4433](https://github.com/HKUDS/nanobot/pull/4433)).

## 4. Community Hot Topics
The most active discussions and collaborative efforts this cycle are:

- **MCP Deny-All Bypass ([#4434](https://github.com/HKUDS/nanobot/issues/4434), [#4435](https://github.com/HKUDS/nanobot/issues/4435)):** This is the dominant topic today. Security researcher `YLChen-007` disclosed that the `enabledTools` allowlist was only enforced for tools, not for resources or prompts. This bypass allows an attacker’s MCP server to leak sensitive context. The community immediately produced a fix in [#4436](https://github.com/HKUDS/nanobot/pull/4436), which is under urgent review.
- **Session-Bricking Stream Bug ([#4442](https://github.com/HKUDS/nanobot/issues/4442)):** The error `"tool_use ids must be unique"` caused widespread concern. Two independent PRs ([#4443](https://github.com/HKUDS/nanobot/pull/4443), [#4444](https://github.com/HKUDS/nanobot/pull/4444)) were filed to guard against duplicate tool IDs from misassembled streams.
- **Mattermost Request ([#1011](https://github.com/HKUDS/nanobot/issues/1011)):** Remains the highest-upvoted open feature request (👍: 4). Users are requesting maintainer commentary on feasibility.
- **Telegram 10.1 Rich Messages ([#4413](https://github.com/HKUDS/nanobot/issues/4413)):** Following the closure of [#4422](https://github.com/HKUDS/nanobot/issues/4422) (which added `sendRichMessage`), warm discussion continues on how to standardize the markdown-to-telegram format conversion.

## 5. Bugs & Stability
Bugs reported or actively patched today, ranked by severity:

1.  **Critical — MCP Allowlist Bypass:** `enabledTools` does not restrict MCP Resources or Prompts.
    - **Status:** Fix under review ([PR #4436](https://github.com/HKUDS/nanobot/pull/4436)).
2.  **Critical — Duplicate Tool IDs Brick Session:** Misassembled Anthropic-family streams persist duplicate `tool_use` IDs, permanently killing the session.
    - **Status:** Two fix PRs in review ([#4443](https://github.com/HKUDS/nanobot/pull/4443), [#4444](https://github.com/HKUDS/nanobot/pull/4444)).
3.  **High — MCP Gateway Crash on Reconnect:** `RuntimeError: cancel scope in a different task` when an MCP server reconnects.
    - **Status:** Fix under review ([PR #4441](https://github.com/HKUDS/nanobot/pull/4441)).
4.  **Medium — Mid-Turn Messages Ignored:** The LLM can ignore user messages injected while it is executing tool calls.
    - **Status:** Fix proposed in [#4397](https://github.com/HKUDS/nanobot/pull/4397).
5.  **Resolved — Run Hook Concurrency (`#4408`):** The bug where `_extra_hooks` was clobbered by concurrent `Nanobot.run()` calls was confirmed and fixed. **Closed.**

## 6. Feature Requests & Roadmap Signals
Several requests point to likely roadmap priorities:

- **High Likelihood for v0.2.2+:**
    - **Heartbeat Model Override ([#4431](https://github.com/HKUDS/nanobot/issues/4431)):** Users want the Heartbeat service to use a cheaper/dedicated model. Given the community’s cost-consciousness, this has strong signal.
    - **Agent-Owned Memory Queries ([#4440](https://github.com/HKUDS/nanobot/issues/4440), [#4439](https://github.com/HKUDS/nanobot/pull/4439)):** The `search_history` tool is highly likely to land soon as it shifts memory from passive context-window management to active agent-driven recall.
    - **Cron Silent Mode ([#4225](https://github.com/HKUDS/nanobot/pull/4225)):** `silent` mode and `lock_recipient` for scheduled jobs are nearing readiness.
- **Roadmap Signals for Future Releases:**
    - **Read-Only Sessions ([#4271](https://github.com/HKUDS/nanobot/pull/4271)):** A clean solution for info-only dialogs (e.g., welcome pages) that avoids wasteful LLM calls.
    - **Unified Daemon Layer ([#1854](https://github.com/HKUDS/nanobot/pull/1854)):** A cross-platform process daemon remains a long-running, high-value enhancement.
    - **Enterprise Channels:** The combination of Mattermost support ([#1011](https://github.com/HKUDS/nanobot/issues/1011)), group allowlists, and private chat gating in DingTalk indicates a clear enterprise scaling vector.

## 7. User Feedback Summary
- **Satisfaction/Strengths:** Contributors consistently praise the quick turnaround on critical patches. The MCP and streaming dedup fixes were written almost immediately after disclosure. The community is technically competent and responsive.
- **Pain Points:**
    - **Security Configuration Gaps:** The MCP bypass has shaken trust that documented config flags are fully enforced. Users strongly desire clearer audit trails or config validation.
    - **Provider Fragility:** Issues with DeepSeek (null content, #3869) and Anthropic streaming (duplicate IDs) highlight that provider compatibility remains the top cause of silent failures and 400 errors.
    - **Onboarding Friction:** The push for a wizard mode and quick-start paths suggests the CLI-first setup is a barrier for new users.
    - **Cost Anxiety:** Requests for model overrides (e.g., #4431) reflect a user base that is deploying agents into production and needs granular cost control.

## 8. Backlog Watch
Items requiring maintainer attention due to age or support volume:

- **Mattermost Channel ([#1011](https://github.com/HKUDS/nanobot/issues/1011)):** 4 months stale, 4 upvotes. The single most requested communication channel is unanswered. A roadmap statement would be valuable.
- **Unified Daemon Layer ([#1854](https://github.com/HKUDS/nanobot/pull/1854)):** 3 months open. This PR solves a core UX disparity across platforms but has zero maintainer comments.
- **DeepSeek Message Hardening ([#3869](https://github.com/HKUDS/nanobot/pull/3869)):** 1 month stale. Despite multiple updates by the contributor, this fix for a provider that breaks on null/empty content hasn’t been merged.
- **OpenAI-Compatible Tool Parsing ([#4092](https://github.com/HKUDS/nanobot/pull/4092)):** 3 weeks open. A complex fix for tool-call parsing across non-standard OpenAI providers is still un-reviewed, blocking support for a broad category of inference endpoints.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-22

## 1. Today's Overview
2026-06-22 saw exceptionally high activity with 50 Issues and 50 Pull Requests updated. The community is actively responding to the post-June 18 Google Gemini CLI sunset, driving urgent migration work toward the AntiGravity provider. Simultaneously, a surge of Desktop feature requests (Kanban, system tray, zoom) and a major refactoring initiative to replace bare `assert` statements are underway. While PR creation is prolific (44 open), the merge rate (6 merged/closed today) highlights a growing review bottleneck as the project consolidates changes for a likely v0.17.0 release.

## 2. Releases
No new releases were published today. Despite intense bug-fixing and feature development, the project has not packaged a new version in the reported period.

## 3. Project Progress
- **Merged:** The comprehensive **Chinese (Simplified) dashboard translation** ([PR #49339](https://github.com/NousResearch/hermes-agent/pull/49339)) was merged, completing a major localization milestone with 42+ new keys and 8 newly refactored i18n components.
- **Fixes in Review Pipeline:** Targeted patches were authored for a series of high-impact bugs:
    - **FTS5 write-path corruption** in the gateway database ([Issue #50502](https://github.com/NousResearch/hermes-agent/issues/50502), [PR #50576](https://github.com/NousResearch/hermes-agent/pull/50576)).
    - **Bedrock non-Claude model routing crash** ([Issue #50292](https://github.com/NousResearch/hermes-agent/issues/50292), [PR #50578](https://github.com/NousResearch/hermes-agent/pull/50578)).
    - **`config set` silent failure** with space-separated keys ([Issue #50553](https://github.com/NousResearch/hermes-agent/issues/50553), [PR #50574](https://github.com/NousResearch/hermes-agent/pull/50574)).
    - **OpenRouter/Codex image generation HTTP 400** ([Issue #49008](https://github.com/NousResearch/hermes-agent/issues/49008), [PR #50579](https://github.com/NousResearch/hermes-agent/pull/50579)).
    - **Kanban native dialog dependency** replaced with in-app dialogs ([PR #50577](https://github.com/NousResearch/hermes-agent/pull/50577)).
    - **Cron session title generation** edge cases resolved ([PR #50575](https://github.com/NousResearch/hermes-agent/pull/50575)).
- **Refactoring:** Two PRs ([#50570](https://github.com/NousResearch/hermes-agent/pull/50570), [#50580](https://github.com/NousResearch/hermes-agent/pull/50580)) systematically replace bare `assert` statements across the gateway and agent modules to prevent silent failures under Python's `-O` optimization flag.

## 4. Community Hot Topics
The most energetic discussions center on three themes:

1.  **Google Gemini CLI Sunset Fallout:** The provider’s total failure since June 18 dominates attention. Issue [#29294](https://github.com/NousResearch/hermes-agent/issues/29294) (8 👍) flagged the transition early, while duplicates [#49701](https://github.com/NousResearch/hermes-agent/issues/49701) and [#49705](https://github.com/NousResearch/hermes-agent/issues/49705) reflect user frustration over unmerged fixes. The community urgently demands **AntiGravity CLI support** ([#44943](https://github.com/NousResearch/hermes-agent/issues/44943), 5 👍).
2.  **Desktop Kanban Integration:** Feature request [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) (6 👍) is the top-voted open feature, describing friction between the CLI board and GUI chat. A corresponding implementation PR ([#41756](https://github.com/NousResearch/hermes-agent/pull/41756)) is actively updated.
3.  **Multi-Telegram Bot Routing:** Issue [#10452](https://github.com/NousResearch/hermes-agent/issues/10452) (7 comments, 4 👍) reflects real operational demand for running primary and dev Telegram bots side-by-side.

*Underlying needs:* Stable provider continuity, unified multi-agent workflow visualization, and production-grade messaging infrastructure.

## 5. Bugs & Stability

**Critical (P1):**
- **FTS5 write-path corruption** silently drops gateway history. Detected via new DB health probe ([PR #50576](https://github.com/NousResearch/hermes-agent/pull/50576) fixing [Issue #50502](https://github.com/NousResearch/hermes-agent/issues/50502)).
- **Security: Browser orphan reaper** trusts arbitrary `/tmp` PID files ([Issue #14073](https://github.com/NousResearch/hermes-agent/issues/14073), closed).

**High (P2):**
- **Google Gemini CLI provider completely dead** for consumer tiers since June 18 sunset ([#49701](https://github.com/NousResearch/hermes-agent/issues/49701), [#49705](https://github.com/NousResearch/hermes-agent/issues/49705)).
- **AntiGravity sub-agent crashes, concurrency drops, and 400 errors** reported as a blocking P2 bug stack ([Issue #50530](https://github.com/NousResearch/hermes-agent/issues/50530)).
- **OpenRouter free tier returns HTTP 404** due to tool calling restrictions ([Issue #49983](https://github.com/NousResearch/hermes-agent/issues/49983)).
- **Bedrock non-Claude models routed through Anthropic SDK**, causing validation crashes ([Issue #50292](https://github.com/NousResearch/hermes-agent/issues/50292), fix in [#50578](https://github.com/NousResearch/hermes-agent/pull/50578)).
- **MCP OAuth flow times out at 40s** before user finishes authorization ([Issue #50485](https://github.com/NousResearch/hermes-agent/issues/50485)).
- **Langfuse quietly drops traces** despite valid configuration ([Issue #42033](https://github.com/NousResearch/hermes-agent/issues/42033)).
- **Desktop "Thinking" toggle snaps back on** after turning off ([Issue #50449](https://github.com/NousResearch/hermes-agent/issues/50449)).
- **Config switch not taking effect** ([Issue #50553](https://github.com/NousResearch/hermes-agent/issues/50553), fix in [#50574](https://github.com/NousResearch/hermes-agent/pull/50574)).

**Moderate (P3):**
- macOS DMG is **arm64-only**, fails outright on Intel Macs ([Issue #37505](https://github.com/NousResearch/hermes-agent/issues/37505)).
- Desktop **Ctrl+Zoom does nothing on Windows** ([Issue #37917](https://github.com/NousResearch/hermes-agent/issues/37917)).
- **Duplicate auto-generated session titles** silently cause `ValueError` ([Issue #50537](https://github.com/NousResearch/hermes-agent/issues/50537), fix in [#50575](https://github.com/NousResearch/hermes-agent/pull/50575)).
- **TUI sessions don't record cwd**, lumping them under the default Desktop workspace ([Issue #50438](https://github.com/NousResearch/hermes-agent/issues/50438)).
- **Web terminal input broken** for IME/direct-layout input ([Issue #50330](https://github.com/NousResearch/hermes-agent/issues/50330), fix in [#50582](https://github.com/NousResearch/hermes-agent/pull/50582)).
- **Multi-image composer layout** collates thumbnails vertically, wasting horizontal space ([Issue #50554](https://github.com/NousResearch/hermes-agent/issues/50554)).

## 6. Feature Requests & Roadmap Signals

**Strong Candidates for Next Release:**
- **AntiGravity CLI provider** — Mandatory replacement for deprecated Gemini CLI ([#44943](https://github.com/NousResearch/hermes-agent/issues/44943), [#50338](https://github.com/NousResearch/hermes-agent/issues/50338)).
- **Multi-Telegram bot routing** — Long-standing request with active implementation PRs ([#10452](https://github.com/NousResearch/hermes-agent/issues/10452) / [#10455](https://github.com/NousResearch/hermes-agent/pull/10455) / [#18652](https://github.com/NousResearch/hermes-agent/pull/18652)).
- **Desktop Kanban integration** — Most popular open feature (6 👍) with live PR ([#41222](https://github.com/NousResearch/hermes-agent/issues/41222) / [#41756](https://github.com/NousResearch/hermes-agent/pull/41756)).
- **Context length probe optimization** — Skips slow OpenRouter `/models` fetch for non-OpenRouter providers ([PR #50572](https://github.com/NousResearch/hermes-agent/pull/50572)).

**Medium-to-Long Term:**
- **Self-hosted Mem0** as a memory provider for local-only setups ([#31135](https://github.com/NousResearch/hermes-agent/issues/31135)).
- **Configurable tool whitelist** for background self-review writes ([#44672](https://github.com/NousResearch/hermes-agent/issues/44672)).
- **Dynamic thinking mode toggle** based on model self-detection ([#50293](https://github.com/NousResearch/hermes-agent/issues/50293)).
- **System tray minimize** on close for Hermes Desktop ([#50167](https://github.com/NousResearch/hermes-agent/issues/50167)).
- **Human-readable API error messages** replacing opaque HTTP codes ([#50460](https://github.com/NousResearch/hermes-agent/issues/50460)).

## 7. User Feedback Summary

**Pain Points:**
- **Provider Deprecation Crisis:** Users are frustrated that Google Gemini CLI was active for consumer tiers post-sunset without a pre-merged migration path, with complaints that "PRs unmerged for 30+ days" left users stranded ([#49701](https://github.com/NousResearch/hermes-agent/issues/49701)).
- **Desktop Immaturity:** The Desktop app is heavily used but lacks basic ergonomics (zoom, system tray, image layout, session workspace grouping). Intel Mac users are completely blocked by a missing universal binary ([#37505](https://github.com/NousResearch/hermes-agent/issues/37505)).
- **Configuration Friction:** OpenRouter free-tier 404s ([#49983](https://github.com/NousResearch/hermes-agent/issues/49983)), Langfuse silent drops ([#42033](https://github.com/NousResearch/hermes-agent/issues/42033)), and MCP OAuth timeouts ([#50485](https://github.com/NousResearch/hermes-agent/issues/50485)) create an exhausting setup experience.

**Positive Contributions:**
- Strong community investment in **localization** (Chinese PR [#49339](https://github.com/NousResearch/hermes-agent/pull/49339) merged, Thai translation [#15151](https://github.com/NousResearch/hermes-agent/issues/15151) in progress).
- Advanced users are pushing for sophisticated features like **dynamic thinking escalation** ([#50293](https://github.com/NousResearch/hermes-agent/issues/50293)) and **self-hosted memory** ([#31135](https://github.com/NousResearch/hermes-agent/issues/31135)).
- Repeated engagement from patch authors (e.g., `trevorgordon981` contributed a clean batch of 6+ fixes today) shows high developer satisfaction with the contribution process.

## 8. Backlog Watch

**Stalled PRs Needing Merge or Review:**
- **Telegram multi-bot PRs** — The implementation for the widely-demanded multi-bot routing ([#10455](https://github.com/NousResearch/hermes-agent/pull/10455)) and edge-case fixes ([#18652](https://github.com/NousResearch/hermes-agent/pull/18652)) have been open since April 15 and May 2 respectively, far exceeding normal review cycles.
- **Self-Hosted Mem0** — The proposal ([#31135](https://github.com/NousResearch/hermes-agent/issues/31135)) notes multiple stale PRs attempting this; no resolution since May 23.

**Maintainer Decisions Needed:**
- **Desktop App Strategy** — Issue [#41180](https://github.com/NousResearch/hermes-agent/issues/41180) (labeled `needs-decision`) raises a fundamental question about whether Desktop features risk watering down the power-user CLI core. Persistent debate without a concluded stance.
- **Thai Translation** — Pushed on Apr 24, [#15151](https://github.com/NousResearch/hermes-agent/issues/15151) remains unmerged despite active updates.

**Unresolved Regressions:**
- **Oneshot fail-closed** scenario ([#35980](https://github.com/NousResearch/hermes-agent/issues/35980)) was only partially fixed; the `hermes -z` command still exits without a final response for the Copilot/gpt-5.5 path where `chat -q -Q` succeeds.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-22

## 1. Today’s Overview
PicoClaw experienced an exceptionally active development day. A total of **32 pull requests** were updated, with **29 merging or closing**, while **6 issues** saw activity and a new nightly build (`v0.3.0-nightly.20260622`) was published. Development focus was split between hardening core runtime systems—message bus backpressure, JSONL memory consistency, and provider fallback semantics—and landing major feature work for the WebUI model configuration workflow. The high merge velocity and breadth of activity suggest the core team is consolidating toward a `v0.3.0` stable release. However, a critical bug report involving continuous token consumption in Evolution mode represents a significant community pain point that remains unresolved.

## 2. Releases
**Nightly Build:** `v0.3.0-nightly.20260622.287853ab`  
This automated build bundles the 29 PRs merged over the last 24 hours and is explicitly flagged as potentially unstable.

- **Changelog:** [Compare v0.3.0…main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)
- **⚠️ Cauton:** Users on stable `v0.2.9` should not upgrade to this nightly for production use. It includes significant core rewrites (memory store, message bus), new API endpoints, and updated V3 configuration schemas.

## 3. Project Progress
Today’s merge batch is dominated by stability hardening and the finalization of the Model Configuration Overhaul.

### Core Runtime Hardening
- **Message Bus Backpressure** — Bounded waiting and drop statistics prevent queue saturation crashes ([PR #2906](https://github.com/sipeed/picoclaw/pull/2906))
- **JSONL Memory Store** — Fixed crash-consistency gap in metadata writing to prevent data drift ([PR #2907](https://github.com/sipeed/picoclaw/pull/2907))
- **JSONL Session Index** — Fixed hot-path cloning and TTL refresh semantics ([PR #2913](https://github.com/sipeed/picoclaw/pull/2913))
- **Fallback Provider** — Context deadline handling now stops the fallback chain immediately on expiration ([PR #2905](https://github.com/sipeed/picoclaw/pull/2905))

### Model Configuration Overhaul (Major Feature)
A three-part series merged today builds the foundation for a completely revamped model management UX:
- **Part 1** — Provider selection UI and model form foundation ([PR #2831](https://github.com/sipeed/picoclaw/pull/2831))
- **Part 2** — Model fetching from upstream providers and saved catalog support ([PR #2832](https://github.com/sipeed/picoclaw/pull/2832))
- **Part 3** — Real connectivity verification via a test connection flow ([PR #2833](https://github.com/sipeed/picoclaw/pull/2833))
- *Base PR:* [PR #2752](https://github.com/sipeed/picoclaw/pull/2752)

### Web Chat Streaming & UX
- End-to-end streaming for the Pico web chat experience, including rebuilt scroll/render behavior ([PR #2587](https://github.com/sipeed/picoclaw/pull/2587))
- Thought visibility toggle persisted in local storage ([PR #2661](https://github.com/sipeed/picoclaw/pull/2661))
- Config save and restart feedback improvements ([PR #2663](https://github.com/sipeed/picoclaw/pull/2663))

### Platform, Tooling, & Config
- **Factory Reset** — Adds a recovery path for incompatible configs with API key preservation ([PR #2891](https://github.com/sipeed/picoclaw/pull/2891))
- **Serial Tool** — Cross-platform hardware support (Linux/macOS/Windows) wired into runtime ([PR #2673](https://github.com/sipeed/picoclaw/pull/2673))
- **Windows Build** — Fixed launcher console flashes and build flow Unix assumptions ([PR #2487](https://github.com/sipeed/picoclaw/pull/2487), [#2654](https://github.com/sipeed/picoclaw/pull/2654))
- **MiMo Provider** — Added `CommonModels` for vision-capable recommendations ([PR #2915](https://github.com/sipeed/picoclaw/pull/2915))
- **Documentation** — All docs synced to V3 config format ([PR #2766](https://github.com/sipeed/picoclaw/pull/2766))

### Channel Fixes
- **Matrix** — Fixed `allow_from` failing on user IDs with colons ([Issue #3044](https://github.com/sipeed/picoclaw/issue/3044))
- **Feishu** — Added `group_trigger.mention_only` and random emoji response config ([PR #2607](https://github.com/sipeed/picoclaw/pull/2607))

### CLI & Miscellaneous
- **MCP Add** — Fixed `DisableFlagParsing` breaking `mcp add` for HTTP/SSE servers ([Issue #3041](https://github.com/sipeed/picoclaw/issue/3041))
- **WebUI** — Restored provider logo fallbacks on the models page ([PR #2908](https://github.com/sipeed/picoclaw/pull/2908))

## 4. Community Hot Topics

**Most Active Issue:**
- **[#3012 — Continuous token consumption when evolution is enabled](https://github.com/sipeed/picoclaw/issue/3012)** (5 comments, 0 reactions)
  - User reports that the Evolution feature perpetually burns API tokens on MiniMax even without activity. This represents a high-severity cost concern and is the most widely discussed open issue.

**New Critical Discovery:**
- **[#3153 — Volcengine Doubao Seed tool calls leak as raw `<seed:tool_call>` text](https://github.com/sipeed/picoclaw/issue/3153)** (created today, 0 comments)
  - Tool calls are returned as unparsed XML text instead of executing. Breaks core agent functionality for a major provider.

**Feature Discussion:**
- **[#3093 — Request for SimpleX or Tox gateway](https://github.com/sipeed/picoclaw/issue/3093)** (1 reaction, 2 comments)
  - Signals demand for privacy-focused decentralized protocol support beyond mainstream channels.

## 5. Bugs & Stability

| Severity | Issue / PR | Status | Summary |
|---|---|---|---|
| **Critical** | [#3012](https://github.com/sipeed/picoclaw/issue/3012) | Open | Continuous token burn in Evolution mode |
| **Critical** | [#3153](https://github.com/sipeed/picoclaw/issue/3153) | Open | Volcengine tool calls returned as raw text |
| **High** | [#2906](https://github.com/sipeed/picoclaw/pull/2906) | **Merged** | Message bus backpressure protection |
| **High** | [#2907](https://github.com/sipeed/picoclaw/pull/2907) | **Merged** | JSONL metadata drift after crash |
| **Medium** | [#3041](https://github.com/sipeed/picoclaw/issue/3041) | **Merged** | MCP add flag parsing broke HTTP/SSE MCP servers |
| **Medium** | [#3044](https://github.com/sipeed/picoclaw/issue/3044) | **Merged** | Matrix `allow_from` rejected valid user IDs |
| **Low** | [#3090](https://github.com/sipeed/picoclaw/issue/3090) | Stale Open | Safari iOS < 16.4 panel incompatibility |

**Assessment:** The core team has aggressively patched the highest-risk runtime stability issues. The two critical open bugs (token burn, Volcengine tool leak) are the main threats to user trust going forward.

## 6. Feature Requests & Roadmap Signals

### Strong Incoming Signals (Based on Merged PRs)
The following features are now in `main` and highly likely for `v0.3.0`:
- **Model Configuration Overhaul** — Provider selection, model fetching, catalogs, and connectivity testing are completely rebuilt in the WebUI and API.
- **Web Chat Streaming** — Real-time streaming is now a first-class citizen of the web experience.
- **Factory Reset** — A safety net for config migration failures is now available.
- **Hardware Integration** — Cross-platform serial tool support signals growing IoT/edge aspirations.

### User-Requested Signals (Future Versions)
- **Privacy Channels** — SimpleX, Tox, and Wire gateway requests persist ([#3093](https://github.com/sipeed/picoclaw/issue/3093)). Given the multi-channel architecture, these are feasible additions.
- **Evolution Stability** — The token consumption bug implies Evolution mode needs deeper reliability work before it can be promoted out of experimental status.

## 7. User Feedback Summary

- **Satisfaction Drivers:** The rapid batch of fixes for MCP, Matrix, Windows builds, and config feedback demonstrates responsive maintainership. Users of advanced features (MCP, Evolution, multi-channel Matrix) are actively pushing the boundaries.
- **Top Pain Points:**
  1. **Cost Exposure:** The Evolution token burn bug directly impacts users' wallets and is the most urgent open issue.
  2. **Provider Fragility:** The Volcengine Doubao tool leak shows that provider-specific integration can break the universal agent promise.
  3. **Channel Gaps:** Users want privacy-first protocols (SimpleX/Tox) that aren't available in the current channel roster.

## 8. Backlog Watch

Items requiring maintainer attention or resolution:

| Item | Days Open | Status | Why It Matters |
|---|---|---|---|
| [#3012 — Continuous token consumption](https://github.com/sipeed/picoclaw/issue/3012) | 17 days | **Active, no fix PR** | Highest community engagement; user cost issue |
| [#3153 — Volcengine tool call leak](https://github.com/sipeed/picoclaw/issue/3153) | 0 days (new) | **Needs triage** | Core agent feature broken for major provider |
| [#3090 — Safari iOS < 16.4](https://github.com/sipeed/picoclaw/issue/3090) | 12 days | **Stale, open** | Blocks mobile web users on older iOS |
| [#3093 — SimpleX/Tox gateway](https://github.com/sipeed/picoclaw/issue/3093) | 12 days | **Open, no maintainer comment** | Feature request lacks roadmap signal |

---

**Project Health Summary:** PicoClaw is in a high-velocity development phase with strong community engagement and responsive maintainers. The massive merge batch today signals a push toward stability and UX maturation for `v0.3.0`. The primary risk factors are the two critical open bugs (#3012 and #3153) that strike at core user value (cost and agent reliability).

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for **2026-06-22**, based strictly on the provided GitHub activity data.

---

## NanoClaw Project Digest — 2026-06-22

### 1. Today’s Overview

The project saw moderate-to-high activity in the last 24 hours, driven primarily by two severe security disclosures and a cluster of infrastructure fixes. Two security advisories filed by YLChen-007 (#2828, #2827) expose critical trust-boundary flaws in the A2A attachment handler and the MCP approval UI. In parallel, the community merged fixes for fragile setup flows and rootless Docker networking, and opened PRs tackling service lifecycle management and skill update determinism. The balance of contributions tilts heavily toward hardening—both security and operational—rather than new features. Overall project health is strong in terms of contributor engagement, but the open security advisories represent urgent architectural risks that require immediate maintainer response.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress (Merged / Closed PRs)

Several important fixes were closed or merged today:

- **[Merged] [#2825](nanocoai/nanoclaw PR #2825)** `fix(setup): wait for the host socket before failing the first chat` — *by amit-shafnir*  
  Resolves a race condition in the setup wizard where the "first chat" health check pings the host CLI socket before the host process has actually bound it.

- **[Merged] [#2168](nanocoai/nanoclaw PR #2168)** `fix(container): pin host.docker.internal to OneCLI's bridge IP in rootless Docker` — *by kpscheffel*  
  Stabilizes container networking in rootless Docker environments by pinning to the bridge IP instead of relying on the unreliable `host-gateway` fallback.

- **[Closed] [#2829](nanocoai/nanoclaw PR #2829)** `[follows-guidelines] eee` — *by fingongr*  
  Low-value / test PR. Closed without substantive code changes.

### 4. Community Hot Topics

**Security Advisories (YLChen-007)** — These are the highest-impact discussions in the project today:

- **Issue [#2828](nanocoai/nanoclaw Issue #2828)** `[Security] NanoClaw A2A attachment forwarding follows a symlinked inbox and writes outside the target session root`  
  **Analysis:** A compromised or prompt-injected agent can replace its mounted `inbox/` directory with a symlink, allowing arbitrary file writes outside the target session root. This bypasses the core agent sandbox.

- **Issue [#2827](nanocoai/nanoclaw Issue #2827)** `[Security] add_mcp_server approval flow hides runtime args and env, enabling approval smuggling`  
  **Analysis:** The approval card for `add_mcp_server` only shows the server name, not the runtime arguments or environment variables. An agent can smuggle dangerous configurations past a human reviewer.

*Underlying need:* The community urgently needs deeper trust-boundary hardening, full-disclosure approval UIs, and safe path resolution for inter-agent file transfers.

**Active Feature / Improvement PRs:**

- **PR [#2531](nanocoai/nanoclaw PR #2531)** `fix(poll-loop): suppress duplicate text when send_message fires mid-turn` — *by cfis* (Open since May 18, updated today)  
  A long-standing conversational UX bug. The poll loop emits duplicated assistant utterances.

- **PR [#2795](nanocoai/nanoclaw PR #2795)** `feat: add /add-clidash — read-only CLI-derived dashboard skill` — *by leetwito*  
  Proposes a new utility skill for an operational dashboard, signaling strong demand for better read-only observability.

- **PR [#2826](nanocoai/nanoclaw PR #2826)** `fix(update-skills): nudge into skill updates, rebuild container on re-apply` — *by Koshkoshinsk*  
  Argues that the `/update-nanoclaw` flow makes skill updates too easy to skip, causing users to miss upstream fixes on channel/provider branches.

### 5. Bugs & Stability

| Severity | Item | Description | Status |
|---|---|---|---|
| **Critical** | [#2828](nanocoai/nanoclaw Issue #2828) | A2A symlink escape — dangerous agent breakout | Open, no fix PR |
| **Critical** | [#2827](nanocoai/nanoclaw Issue #2827) | MCP approval smuggling via hidden `args`/`env` | Open, no fix PR |
| **High** | [#2531](nanocoai/nanoclaw PR #2531) | Poll-loop emits duplicate text during mid-turn send_message | Fix PR open (since May 18) |
| **Medium** | [#2830](nanocoai/nanoclaw PR #2830) | Dead service registrations accumulate when binary is removed without uninstall | Fix PR open |
| **Medium** | [#2826](nanocoai/nanoclaw PR #2826) | Skill updates silently skippable, causing users to miss upstream fixes | Fix PR open |
| **Fixed** | [#2825](nanocoai/nanoclaw PR #2825) | Setup "first chat" race condition | Merged today |
| **Fixed** | [#2168](nanocoai/nanoclaw PR #2168) | Rootless Docker `host-gateway` unreliability | Merged today |

### 6. Feature Requests & Roadmap Signals

- **Operational Dashboarding (#2795):** The `/add-clidash` utility skill proposal strongly signals that advanced users want a read-only, CLI-derived management interface. This may influence the next release’s skill template guidance.
- **Update Determinism (#2826):** The pushback from Koshkoshinsk against the "safe to skip" skill update flow suggests a roadmap goal for /update-nanoclaw: guarantee that all installed skills are refreshed when upstream channel/provider branches change.
- **Security Architecture Review:** While not a classic feature request, the #2827 and #2828 advisories will inevitably force a design discussion on approval card transparency (showing full runtime args/env) and IO path validation (resolving symlinks before forwarding files).

### 7. User Feedback Summary

- **Pain Points:**
  - *Setup Flakiness:* Resolved today with #2825 (socket race) and #2168 (rootless Docker).
  - *Update Fragility:* Users are unhappy that skill updates are treated as optional during `/update-nanoclaw` (#2826).
  - *Conversational UX Degradation:* The poll-loop duplicate text bug (#2531) continues to degrade agent conversations.
  - *Security Concerns:* The disclosures of approval smuggling and agent sandbox escapes will likely reduce trust in running untrusted agents or third-party MCP servers without deep review.

- **Satisfaction / Engagement Signals:**
  - Repeated quality-of-life fixes from `amit-shafnir` and `kpscheffel` indicate a healthy contributor base committed to platform stability.
  - Community members are actively building and submitting utility skills (#2795), demonstrating a growing ecosystem around the skill system.

### 8. Backlog Watch

The following items require timely maintainer attention:

- **[#2531](nanocoai/nanoclaw PR #2531)** `fix(poll-loop): suppress duplicate text` — *Open since 2026-05-18*  
  The project’s longest-open meaningful fix PR. Unresolved for over a month. Core conversational UX suffers with every release cycle this sits open.

- **[#2795](nanocoai/nanoclaw PR #2795)** `feat: add /add-clidash` — *Open since 2026-06-17*  
  Needs design feedback or approval. Stalling contributor momentum here risks discouraging skill ecosystem participation.

- **[#2828](nanocoai/nanoclaw Issue #2828) / [#2827](nanocoai/nanoclaw Issue #2827)** — *Open since 2026-06-21*  
  **Highest priority.** These advisories have zero comments, no assignees, and no linked fix PRs. Silence on critical security issues is a risk to project health and user trust. Immediate triage, disclosure timeline, and mitigation strategy are needed.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest based on the available GitHub data for **2026‑06‑22**.

---

### 1. Today’s Overview
Public repository activity for NullClaw was very low over the last 24 hours, with no new releases or pull requests. The project’s pulse is dominated entirely by a single, high-severity bug report that directly impacts the core agent functionality. While project velocity appears dormant from a code commit perspective, the community interaction signals an urgent stability concern. Overall project health is stable but fragile, heavily dependent on maintainer responsiveness to this critical regression.

### 2. Releases
No new releases were published in the last 24 hours. The current stable release remains **v2026.5.29** (2026-05-29).

### 3. Project Progress
No pull requests were updated, merged, or closed today. No features or fixes were advanced through the standard PR process in this reporting window.

### 4. Community Hot Topics
The entire community discussion is concentrated on a single blocking bug.

* **[Issue #967 (Open): [bug] error: NoResponseContent](https://github.com/nullclaw/nullclaw/issues/967)**  
  *Author:* svier0  
  *Context:* Windows 11 user running v2026.5.29 with the `Agnes-2.0-Flash` model. The agent fails >50% of the time with `error: NoResponseContent`.  
  *Analysis:* The user explicitly states the same API key and model work correctly in another client (“picocla”), strongly indicating the bug lies in NullClaw’s request/response parsing or timeout handling rather than the upstream model. The underlying need is **reliable, first-try agent responses** on standard Windows setups.

### 5. Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **HIGH** | [#967](https://github.com/nullclaw/nullclaw/issues/967) | **NoResponseContent** – Agent returns empty output on >50% of requests with Agnes-2.0-Flash on Win11. Core functionality is broken for this user. | Open, 1 comment, **no fix PR** |

No other bugs, crashes, or regressions were recorded in the last 24 hours. The absence of any linked fix PR suggests the issue has not yet been diagnosed or reproduced by the maintainer.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. The clear implicit signal from the community is a demand for **stability and error-handling robustness**. Based on this data, the most likely prediction for the next release (v2026.6.x) is a **targeted hotfix** addressing the response retrieval pipeline—specifically the handling of empty or malformed API responses for Flash-tier models. New feature development is unlikely to be the immediate priority.

### 7. User Feedback Summary
The single user interaction today constitutes strong negative feedback regarding product reliability.

* **Pain Point:** Core function failure at a >50% rate renders the tool unusable for the user’s workflow.
* **Use Case:** Standard conversational AI agent interaction on Windows 11.
* **Satisfaction:** Low. The user’s explicit cross‑project comparison (“在picocla...” / *“in picocla it works”*) signals a risk of user churn and damage to NullClaw’s reputation as a functional AI agent tool.

### 8. Backlog Watch
No long‑dormant issues or stale PRs appear in the provided data feed. However, **[Issue #967](https://github.com/nullclaw/nullclaw/issues/967)** is a **critical item that demands immediate maintainer attention**. Because it was filed on June 20th and updated June 21st, it is still within the initial triage window, but the high severity and blocking nature of the bug mean any delay in response risks compounding user dissatisfaction and negative project perception.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-22
*Generated from GitHub data for nearai/ironclaw*

---

## 1. Today's Overview

IronClaw saw intense development activity, driven entirely by the ongoing **"Reborn"** platform maturation. **29 pull requests** were updated (14 merged/closed) alongside **6 issues** (2 closed, 4 active). While no new releases were published today, the project made significant strides in CI reliability—overhauling caching strategies and network retry logic—while concurrently advancing major feature blocks. The focus is split evenly between infrastructure hardening (caching, concurrency, E2E gating) and user-facing feature work (one-shot triggers, Composio connectors, and the learning system stack). Project health appears strong, with a high merge velocity and proactive dogfooding efforts to surface first-run UX issues before they impact the broader community.

**Key Metrics:**
- Issues updated: 6 (closed: 2, open/active: 4)
- PRs updated: 29 (merged/closed: 14, open: 15)
- New releases: 0

---

## 2. Releases

*None to report.* No new versions were tagged or released today. Users tracking the `main` branch have access to the latest merged features (one-shot triggers, CI improvements, MCP state fixes), but a formal release candidate has not yet been cut.

---

## 3. Project Progress — Merged & Closed PRs Today

**Features Delivered:**

- **One-Shot Scheduled Triggers** ([#5065](nearai/ironclaw PR #5065)) — Merged. Introduces `TriggerSchedule::Once { at, timezone }` as a first-class schedule variant alongside recurring `Cron`. Enables fire-once automations, which pairs with the `Completed` filter tab also shipped in this PR.

- **NEAR AI MCP Ready State Fix** ([#4990](nearai/ironclaw PR #4990)) — Merged. Resolves the confusing "SETUP NEEDED" projection for the built-in `nearai.web_search` MCP server, closing issue [#4925](nearai/ironclaw Issue #4925). Runtime credentials are no longer projected as browser-managed extension setup requirements.

**CI & Infrastructure:**

- **Unified Rust Caching** ([#5118](nearai/ironclaw PR #5118)) — Merged. Consolidates per-crate caches into a shared cache hierarchy, solving ~30 GB cache churn and LRU eviction that was causing red-herring CI failures across the 64-crate closure.

- **crates.io Network Retries** ([#5115](nearai/ironclaw PR #5115)) — Merged. Adds `CARGO_NET_RETRY` to mitigate transient SSL/HTTP2 failures that were hitting multiple parallel jobs simultaneously.

- **Platform & Compat Job Extraction** ([#5113](nearai/ironclaw PR #5113)) — Merged. Agent-authored verbatim extraction of cross-cutting CI jobs into a standalone workflow, improving CI organization.

- **Reborn E2E Merge Gate** ([#4830](nearai/ironclaw PR #4830)) — Merged. Reborn E2E tests now run in the merge queue with internal scope gating, enforcing deterministic Rust contract and gateway/WebUI v2 Playwright smoke tests before PRs land.

**Bugfixes:**

- **Google OAuth Proactive Refresh** ([#5071](nearai/ironclaw Issue #5071)) — Closed. Reborn now proactively refreshes GSuite access tokens before expiry, eliminating the need for hourly re-authentication.

- **First-Run Channel Activation** ([#2927](nearai/ironclaw PR #2927)) — Merged. Fixes a critical onboarding bug where WASM channels remained inactive on clean installs even when the setup wizard had just selected them.

**Dependencies:**
- Bumped the `everything-else` group across 43–44 updates ([#4876](nearai/ironclaw PR #4876), [#5116](nearai/ironclaw PR #5116))
- Tokio ecosystem group bumps ([#4499](nearai/ironclaw PR #4499), [#5114](nearai/ironclaw PR #5114))
- GitHub Actions group bulk update across 16 packages ([#4002](nearai/ironclaw PR #4002))

---

## 4. Community Hot Topics

**🔥 Active Discussion & High-Impact Features**

- **Learning System Stack (WS-1 [#4937](nearai/ironclaw PR #4937), WS-3 [#4975](nearai/ironclaw PR #4975))** — The most complex feature set currently in flight. WS-1 establishes memory documents with confidence scoring and an A/B gating framework. WS-3 adds a reflection fork for post-turn learning from mistakes/corrections. These represent a fundamental capability upgrade toward "never repeat the same error" agent behavior. High community interest in the design document referenced in the PR description.

- **Concurrent Turn Execution** ([#5085](nearai/ironclaw PR #5085)) — Open. Proposes a `TurnRunScheduler` with per-user/per-type caps. Currently, turn runs execute strictly serially, which is a clear performance bottleneck for power users. This PR addresses a widely felt pain point in the Reborn runtime.

- **Desktop Workbench Composio Integration** ([#5109](nearai/ironclaw PR #5109)) — Draft PR adding read-only + gated-write connector routes for the Workbench. Signals a strong push toward making the Workbench a fully featured agent hub with live connector data from thousands of services.

**💬 Semantic UX Issues**

- **Unified Gate/Auth Semantics** ([#5120](nearai/ironclaw Issue #5120)) — Filed today. Documents the current fragmentation: WebUI uses `Declined`, approval uses `Deny`/`Denied`, auth uses `Deny`/`Canceled`. Users are demanding a consistent vocabulary across the platform.

- **Automations Completed Summary Card** ([#5117](nearai/ironclaw Issue #5117)) — Enhancement request for a 6th grid cell showing server-side completed automation counts. Pairing with the recently shipped `Completed` filter tab.

- **Local Dogfooding Session** ([#5119](nearai/ironclaw Issue #5119)) — A tracking issue opened today for the week of June 22–28. The team is explicitly dogfooding local Reborn builds to catch startup configuration, model-provider setup, and first-run usability problems. Expect a wave of micro-fixes from this initiative.

---

## 5. Bugs & Stability

**🛡️ [HIGH] Resolved: Google OAuth Token Expiry** ([#5071](nearai/ironclaw Issue #5071))
- *Closed.* Google access tokens expire after ~1 hour. Reborn now proactively refreshes using the durable refresh token, preventing mid-session re-authentication for GSuite users.

**🛡️ [HIGH] Resolved: CI Cache Eviction Storms** ([#5118](nearai/ironclaw PR #5118), [#5115](nearai/ironclaw PR #5115))
- Two major CI instability sources eradicated today: 30+ GB cache churn from per-crate caching and transient crates.io HTTP2 failures. These directly improve contributor experience and merge velocity.

**🛡️ [MEDIUM] Resolved: MCP "SETUP NEEDED" False Positive** ([#4925](nearai/ironclaw Issue #4925))
- The built-in NEAR AI MCP server was consistently misprojected as needing user setup. Fixed in #4990. This was a significant onboarding friction point.

**⚠️ [OPEN] Nightly E2E Failures** ([#4108](nearai/ironclaw Issue #4108))
- *Created May 27, last updated June 21.* The nightly E2E suite continues to fail in the `extensions` scope. While the CI infrastructure improvements today (#5113, #5115, #5118, #4830) may address underlying causes, this remains a known instability that requires explicit diagnosis.

**⚠️ [OPEN] Reborn Local Dogfooding Tracker** ([#5119](nearai/ironclaw Issue #5119))
- Proactive monitoring issue. This week-long session is likely to generate bug reports around startup sequencing, model-provider configuration, and general first-run UX. No specific bugs reported yet, but this is a high-signal channel for upcoming stability patches.

---

## 6. Feature Requests & Roadmap Signals

**Confirmed Incoming (Active PRs/Issues):**

| Feature | Signals | Status |
|---|---|---|
| **Learning System** | WS-1 (#4937), WS-2 (#4938), WS-3 (#4975) stacked | Active review; WS-1 is the foundation week |
| **Concurrent Turns** | `TurnRunScheduler` with per-user caps (#5085) | Open; strong internal support |
| **Hosted Single-Tenant Postgres** | Production-ready profile with SSO/tool/approval wiring (#5081) | Open; signals hosted Preview path |
| **Workbench Connectors** | Composio read/write route (#5109) | Draft; targets July integration hooks |

**User-Requested Features Gaining Traction:**

- **Automations Completed Summary Card** ([#5117](nearai/ironclaw Issue #5117)) — Small UI enhancement for the `/v2/automations` page. The filter tab already exists (#5065); the summary card fills the currently empty 6th grid cell. Likely to ship in the next feature release.

- **Auth/Approval Semantic Unification** ([#5120](nearai/ironclaw Issue #5120)) — Filed today with zero comments but strong internal motivation. The inconsistent `Deny`/`Declined`/`Canceled` UX is actively confusing users across the WebUI, approval flows, and auth state machines. Predict this moves to a design proposal quickly.

**Predictions for Next Version:**
- The Learning System stack merges (WS-1 → WS-3).
- Concurrent turn execution ships.
- Desktop Workbench connector integration becomes usable (read-only first, gated-write second).
- The Dogfooding findings (#5119) generate a batch of 5–10 small fixes targeting first-run and startup reliability.

---

## 7. User Feedback Summary

**Pain Points Resolved Today:**
- **"SETUP NEEDED" confusion eliminated** — Users no longer see a false requirement to configure the pre-installed NEAR AI MCP server (#4925 → #4990).
- **No more hourly Google re-auth** — GSuite users retain access across long sessions without interruption (#5071).
- **Channels activate on first run** — Clean installs no longer leave WASM channels dormant (#2927).

**Pain Points Actively Being Addressed:**
- **Serial turn execution is a bottleneck** — The `TurnRunScheduler` PR (#5085) directly addresses user frustration with waiting on sequential LLM inference.
- **Inconsistent deny/decline semantics** — Users encountering auth and approval flows report confusion over terminology (#5120).
- **Automations lack completion visibility** — Users want to see count of fired one-shots without digging through logs (#5117).

**Satisfaction Signals:**
- High internal engagement with dogfooding (#5119) suggests the team is serious about quality before the next stable cut.
- Rapid turnaround time on reported issues (e.g., #4925 → fix in 7 days) reflects good maintainer responsiveness.

---

## 8. Backlog Watch

**🚨 Critical Backlog Items**

| Issue | Age | Status | Why It Matters |
|---|---|---|---|
| **Nightly E2E Failure** ([#4108](nearai/ironclaw Issue #4108)) | 26 days | Open | CI reliability hole in the `extensions` scope. Despite infrastructure improvements today, this has not been explicitly resolved. |
| **Actions Group Dependabot** ([#4002](nearai/ironclaw PR #4002)) | 29 days | Open | Bumps 16 critical CI packages (checkout, claude-code-action, etc.). Risk grows with every passing week. |
| **WASM Group Dependabot** ([#4032](nearai/ironclaw PR #4032)) | 28 days | Open | `wit-component` and `wit-parser` minor version bumps. IronClaw's WASM runtime surface makes this a compatibility risk if left open. |
| **Serialization Group Dependabot** ([#4498](nearai/ironclaw PR #4498)) | 17 days | Open | `serde_yml` bump from 0.0.12 to 0.0.13. Small but accumulated dependency lag is a supply chain hygiene concern. |

**📌 Items Recently Addressed:**
- **First-run channel activation** (#2927) — *Just merged.* This was a blocker for new user onboarding.
- **OAuth token refresh** (#5071) — *Closed.* Eliminated a major stability threat.
- **CI caching strategy** (#5118, #5115) — *Merged.* Should significantly reduce daily CI flakiness.

**🧹 Maintainer Attention Needed:**
- The `Nightly E2E` issue (#4108) remains the single biggest stability gap. The CI infra merges today (#5113, #5115, #5118, #4830) may provide the foundation to finally diagnose and close this.
- Open Dependabot PRs across the `actions`, `wasm`, and `serialization` groups are accumulating. A bulk merge pass or explicit conflict resolution cycle is overdue.

---

*This digest was generated from GitHub activity data for `nearai/ironclaw` as of 2026-06-22. All linked items reference the original issue or pull request on the repository.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is a structured project digest for LobsterAI based on the given GitHub snapshot.

---

## LobsterAI Project Digest — 2026-06-22

### 1. Today's Overview
Today marks a significant housekeeping event for LobsterAI, where an automated stale bot swept through the issue tracker, closing 14 long-dormant issues primarily from early April. While this cleanup clears the queue visually, it highlights a period of slow active development, with zero Pull Requests merged and no new releases published. Despite the low code activity, a critical security vulnerability was freshly reported, demanding immediate triage. The overall project health is stable but shows signs of a resource bottleneck, where detailed user feedback remains unaddressed.

### 2. Releases
None. No new releases were cut today.

### 3. Project Progress
- **Merged/Closed PRs:** None. No pull requests were opened, merged, or closed today.
- **CI/Housekeeping:** The stale bot automatically closed 14 issues that had been inactive since April 7, 2026. One CI-related issue ([[#1518](https://github.com/netease-youdao/LobsterAI/issues/1518)]) regarding fixing Labeler permissions was swept away without confirmation of a fix deployment. While this reduces the raw backlog count, it does not represent authored fixes or features.

### 4. Community Hot Topics
Community discussion is currently split between a new critical security report and a large pool of unresolved friction points from power users.

- **Security Concern (New):** [[#2181](https://github.com/netease-youdao/LobsterAI/issues/2181)] by YLChen-007 is the only open/active issue reported today. It details a severe regression where LobsterAI defaults to a "ProxyCompatible" mode that weakens the bundled SSRF protections, potentially exposing private-network browser access. This topic is likely to draw heavy scrutiny.
- **Core Skill System Friction:** The stale cleanup closed several detailed reports by user `MaoQianTu` regarding fundamental workflow flaws. [[#1500](https://github.com/netease-youdao/LobsterAI/issues/1500)] and [[#1502](https://github.com/netease-youdao/LobsterAI/issues/1502)] received multiple comments confirming that the skill activation system desynchronizes from the UI state, requiring workarounds to function. These are core UX failures for a tool based on agent skills.
- **Silent Configuration Failures:** Issues [[#1504](https://github.com/netease-youdao/LobsterAI/issues/1504)] and [[#1506](https://github.com/netease-youdao/LobsterAI/issues/1506)] highlight user frustration with the IM Bot setup, where missing validations allow users to save broken configurations that fail silently during runtime.

### 5. Bugs & Stability
| Severity | Issue | Summary | Status |
| :--- | :--- | :--- | :--- |
| **CRITICAL** | [[#2181](https://github.com/netease-youdao/LobsterAI/issues/2181)] | SSRF guard weakened by default config; private network access restored. | Open; **No fix PR**. Requires immediate triage. |
| **HIGH** | [[#1500](https://github.com/netease-youdao/LobsterAI/issues/1500)] | Disabled skills remain in `activeSkillIds` and are injected into prompts. | **Closed Stale**; Likely unresolved. |
| **HIGH** | [[#1502](https://github.com/netease-youdao/LobsterAI/issues/1502)] | Agent settings / skill list not syncing without manual Agent switch. | **Closed Stale**; Likely unresolved. |
| **HIGH** | [[#1516](https://github.com/netease-youdao/LobsterAI/issues/1516)] | GitHub Copilot OAuth Token silently lost if Settings panel closed during polling. | **Closed Stale**; Likely unresolved. |
| **MEDIUM** | [[#1506](https://github.com/netease-youdao/LobsterAI/issues/1506)] | IM notification channel bypasses session selection, causing silent failures. | **Closed Stale**; Likely unresolved. |
| **LOW** | [[#1513](https://github.com/netease-youdao/LobsterAI/issues/1513)] | Inconsistent formatting in Terms & Conditions page. | **Closed Stale**; Likely unresolved. |

**Key Observation:** No fix commits or PRs were tied to the closing of these high-severity bugs, strongly suggesting they remain reproducible in the current codebase.

### 6. Feature Requests & Roadmap Signals
User `MaoQianTu` contributed a structured series of feature requests that serve as a clear roadmap signal for future releases:
- **Session Organization:** Color coding ([[#1525](https://github.com/netease-youdao/LobsterAI/issues/1525)]) and custom tagging/filtering ([[#1541](https://github.com/netease-youdao/LobsterAI/issues/1541)]).
- **Data Portability:** Batch export of conversations ([[#1528](https://github.com/netease-youdao/LobsterAI/issues/1528)]) and message bookmarking ([[#1537](https://github.com/netease-youdao/LobsterAI/issues/1537)]).
- **User Analytics:** Local usage statistics panel ([[#1532](https://github.com/netease-youdao/LobsterAI/issues/1532)]).

**Prediction:** The volume and specificity of these requests (specifically tagging and export) suggest that a "Data Management v2" upgrade is the most likely candidate for the next minor release. These features represent "table stakes" for AI productivity tools.

### 7. User Feedback Summary
- **Dissatisfaction Drivers:**
    - **Workflow Unreliability:** The most vocal feedback concerns the skill system and agent configuration not respecting user toggles. Trust in the core state management is low.
    - **Silent Failure Modes:** Users consistently report scenarios (IM notifications, OAuth flows) where the UI shows success but the action fails silently, causing data loss or missed messages.
    - **Lack of Transparency:** There is a strong desire to see the AI agent's reasoning process ([[#1509](https://github.com/netease-youdao/LobsterAI/issues/1509)]). Users feel blocked when the system pauses to generate skills without showing any intermediate state.
    - **Model Quality Variance:** A user noted that the same model behaves differently in LobsterAI versus the bundled OpenClaw environment, suggesting prompt engineering or context injection issues ([[#1509](https://github.com/netease-youdao/LobsterAI/issues/1509)]).
- **Desired Use Case:** Users want LobsterAI to function as a daily productivity hub (scheduled tasks, IM bots, local data). The current lack of organizational features (tags, colors, bookmarks) prevents it from replacing dedicated tools.

### 8. Backlog Watch
- **🚨 Immediate Critical Watch:**
    - **[[#2181](https://github.com/netease-youdao/LobsterAI/issues/2181)] (Security):** This is the only active, open issue. A regression allowing private network access via a weakened SSRF guard is a serious security flaw that must be addressed before the next release.
- **🧊 Frozen Backlog (Maintainer Response Needed):**
    - The stale bot sweeping 14 detailed reports (including several HIGH severity bugs) without a "Won't Fix" or "Fixed in `dev`" comment is a negative signal for community health. Power users who spent time writing detailed bug reports (e.g., [[#1500](https://github.com/netease-youdao/LobsterAI/issues/1500)], [[#1506](https://github.com/netease-youdao/LobsterAI/issues/1506)]) deserve triage transparency.
    - **Maintainer Activity Gap:** With zero PRs and zero releases, the project appears to be in a quiet period. Community trust relies heavily on acknowledging the technical debt reported throughout April.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-22

## Today's Overview

The QwenPaw project saw high development activity in the 24-hour window, with **37 pull requests updated** (32 still open) and **18 issues touched** (14 open/active). While no new release was cut, the sheer number of PRs – including several first‑time contributions and mobile‑responsive CSS work – signals a vibrant contributor ecosystem. However, the issue tracker reveals user frustration with regressions introduced in v1.1.12: skills re‑enabling after upgrade, message‑queue cross‑delivery, and a broken file preview. The community is clearly engaged and rapidly submitting fixes, but the influx of bugs points to a need for tighter release validation.

## Releases

*No new releases were published today.*

## Project Progress

Four pull requests were merged or closed today, advancing both core fixes and testing infrastructure:

- **Plugin loader decoupling**  
  [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) – Closed: Decouples plugin loader initialisation from agent startup, fixing the “Plugin loader not ready” issue in frozen (Tauri/PyInstaller) environments. (Fixes [#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889).)

- **Integration test suite (Sprint 3.1‑3.4)**  
  [#5270](https://github.com/agentscope-ai/QwenPaw/pull/5270) – Closed: Adds 64 cases covering ACP runner, plugin system, security, and cross‑cutting flows.

- **Mobile responsive layout for Agent Config**  
  [#5365](https://github.com/agentscope-ai/QwenPaw/pull/5365) – Closed: CSS‑only adaptation for narrow screens (a duplicate of the newer [#5366](https://github.com/agentscope-ai/QwenPaw/pull/5366) which remains open).

- **Vector model connection test**  
  [#3831](https://github.com/agentscope-ai/QwenPaw/pull/3831) – Closed: Adds a test button for vector model endpoints (opened April 25, finally merged).

Additionally, **four issues were closed** today, many with fixes already in the PR pipeline: the Feishu @‑mention bug ([#5353](https://github.com/agentscope-ai/QwenPaw/issues/5353)) and the file‑display regression ([#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320), fixed by [#5324](https://github.com/agentscope-ai/QwenPaw/pull/5324)) were resolved. The feature request for real‑time UI updates ([#5322](https://github.com/agentscope-ai/QwenPaw/issues/5322)) was closed without merging – it may require design discussion before implementation.

## Community Hot Topics

The most active issues this week revolve around regressions and mobile usability:

- [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) (8 comments) – **Built‑in skills re‑enable after every upgrade**. A long‑standing pain point (previously reported as #4807) that remains unfixed. Users have to manually disable unwanted skills like `docx`/`xlsx` after each version bump.

- [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) (5 comments) – **Mobile sidebar: no way to switch agents in collapsed mode**. A power user accessing QwenPaw on a phone requests a dedicated button in the left sidebar so agent switching and chat history remain accessible on small screens.

- [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) (4 comments) – **Message queue cross‑agent delivery**. The new message queue is praised for efficiency but suffers a critical flaw: switching agents mid‑queue sends the pending message to the wrong agent, and subsequent session switching can get stuck.

## Bugs & Stability

Several regressions and new defects surfaced today, ranked by estimated user impact:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| Critical | [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) | Message queue delivers to wrong agent after switch; sessions can get stuck in grey state. | [#5371](https://github.com/agentscope-ai/QwenPaw/pull/5371) (binds agent ID at enqueue) |
| Critical | [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | Disabled built‑in skills re‑enable on every upgrade. | None (requires persistent config) |
| High | [#5373](https://github.com/agentscope-ai/QwenPaw/issues/5373) | `execute_shell_command` fails on pipes, redirection, stderr merge. | None |
| High | [#5370](https://github.com/agentscope-ai/QwenPaw/issues/5370) | `send_file_to_user` returns HTTP 404 in console frontend (path mangling). | None yet |
| Medium | [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) | Custom OpenAI‑compatible providers (e.g. OMLX) do not support function calling. | None |
| Medium | [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) | Zhipu model‑level test connection fails despite API‑key test passing. | None |
| Medium | [#5344](https://github.com/agentscope-ai/QwenPaw/issues/5344) | API (`/api/console/chat`) silently drops messages when agent is busy. | None |
| Low | [#5358](https://github.com/agentscope-ai/QwenPaw/issues/5358) | TypeError `Cannot read properties of null` in UI vendor bundle during session switch. | None |
| Low | [#5374](https://github.com/agentscope-ai/QwenPaw/issues/5374) | Drag‑and‑drop attachment upload broken on Mac Chrome. | None |

The only bug with a known fix today is the cross‑agent queue problem – [#5371](https://github.com/agentscope-ai/QwenPaw/pull/5371) proposes binding the `agentId` at enqueue time. The session‑switch lock is also addressed by [#5357](https://github.com/agentscope-ai/QwenPaw/pull/5357).

## Feature Requests & Roadmap Signals

The community is pushing **mobile responsiveness** as the top priority. A wave of first‑time contributors has submitted CSS‑only adaptations for several pages: Channels ([#5369](https://github.com/agentscope-ai/QwenPaw/pull/5369)), CronJobs ([#5362](https://github.com/agentscope-ai/QwenPaw/pull/5362)), Sessions ([#5364](https://github.com/agentscope-ai/QwenPaw/pull/5364)), Security ([#5367](https://github.com/agentscope-ai/QwenPaw/pull/5367)), Agent Config ([#5366](https://github.com/agentscope-ai/QwenPaw/pull/5366)), and SkillPool ([#5368](https://github.com/agentscope-ai/QwenPaw/pull/5368)). This aligns with [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) requesting a dedicated mobile agent‑switch button.

Other notable feature signals:

- **Model routing / failover** – [#5351](https://github.com/agentscope-ai/QwenPaw/issues/5351) asks for automatic failover using existing but unused `RoutingChatModel`.
- **Context‑explosion protection** – [#5342](https://github.com/agentscope-ai/QwenPaw/issues/5342) requests a hard cap on tool‑result size when LLM calls fail.
- **Memory ranking** – [#5316](https://github.com/agentscope-ai/QwenPaw/issues/5316) suggests recency‑aware scoring for daily‑memory search.
- **Scroll context manager** – [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321) (under review) introduces a retrieval‑driven alternative to built‑in compression.
- **Data‑analysis plugin** – [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) (under review) brings a `datapaw` bundle with 12 BI‑style skills.

A cross-cutting sentiment emerges in [#5360](https://github.com/agentscope-ai/QwenPaw/issues/5360): many users urge the team to **stabilise the core app** before adding further features, explicitly calling out mobile responsiveness, agent interaction, and workspace navigation as broken.

## User Feedback Summary

The community is heavily engaged but increasingly vocal about **release quality**. Key pain points:

- **Upgrade regressions hurt trust** – [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) and [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) (file preview broken after v1.1.12) show that users expect smooth upgrades without manual re‑configuration or broken features.
- **New features with rough edges** – The message queue is praised for performance but its cross‑agent delivery bug ( [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) ) disrupts daily workflows.
- **Mobile users feel abandoned** – Several users report accessing QwenPaw from phones; the lack of responsive UI and missing navigation elements forces them to use workarounds.
- **Desire for real‑time interaction** – [#5322](https://github.com/agentscope-ai/QwenPaw/issues/5322) (closed) and [#5344](https://github.com/agentscope-ai/QwenPaw/issues/5344) highlight the need for live API message feeds and non‑blocking chat.
- **Positive tone on direction** – Despite bugs, contributors continue to submit thoughtful features (e.g., [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622), [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)), indicating strong belief in the project’s potential.

## Backlog Watch

Several important items have been lingering for weeks or were reopened due to incomplete fixes:

- [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) – **Skills re‑enable on upgrade** (8 comments, ref #4807). Open since June 17 but first reported in a prior version. The underlying persistence issue still lacks an owner.
- [#5040](https://github.com/agentscope-ai/QwenPaw/pull/5040) (since June 9) vs. [#5347](https://github.com/agentscope-ai/QwenPaw/pull/5347) (since June 20) – Two PRs tackling the same `crons` invalid‑job problem with different strategies (tolerance vs. migration). Maintainers should decide and converge.
- [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) (since May 22) – Large data‑analysis plugin under review. Likely needs rebase and final approval.
- [#5097](https://github.com/agentscope-ai/QwenPaw/pull/5097) (since June 11) – Trivial CSS fix for a “Shield” icon alignment. Unmerged despite being labelled as ready.
- [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) (since June 20) – Custom provider function‑calling support. A gap that limits provider choice; no PR yet.
- [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) (since June 19) – Zhipu model‑test failure. A blocking issue for all Chinese Zhipu users, currently unassigned.

These items – especially the skill‑persistence regression and the cron‑fix duplication – warrant maintainer attention to prevent user frustration and contributor churn.

---

*Data retrieved from [GitHub](https://github.com/agentscope-ai/QwenPaw) for the 24‑hour window ending 2026-06-22T00:00:00Z.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

Here is the ZeptoClaw project digest for **2026-06-22**, generated from the provided GitHub activity data.

---

## ZeptoClaw Project Digest | 2026-06-22

### 1. Today's Overview
Today's activity on the ZeptoClaw repository was minimal in volume but strategically significant. The development team finalized a long-running CI pipeline improvement by closing the last open item in the "binary size budget" initiative. This reflects a strong commitment to the project's core tenet of maintaining a small agent footprint for constrained deployments (e.g., robotics). With zero new releases, bugs, or feature requests, the project appears to be in a phase of internal process hardening rather than rapid feature iteration.

### 2. Releases
**None.** No new versions were published in the last 24 hours.

### 3. Project Progress
The primary achievement was the closure of **PR #611**:
- **[PR #611](https://github.com/qhkm/zeptoclaw/pull/611) — chore(ci): promote binary-size to PR gate at 7.5MB** (Merged/Closed)
  - **What advanced:** This PR converted the existing `binary-size` job from a post-hoc check (running only on `push-to-main`) into a strict PR gate that runs on every pull request. It lowers the threshold to **7.5MB** for the stripped release binary, effectively blocking any PR that introduces bloat.
  - **Impact:** This hardens the CI pipeline against the "silent erosion" of the project's strategic moat, as outlined in the associated issue.

### 4. Community Hot Topics
The most active items were the closed **Issue #537** and **PR #611**, both authored solely by the project lead **qhkm** with no community comments or reactions recorded today.

- **[Issue #537](https://github.com/qhkm/zeptoclaw/issues/537) — chore(ci): binary size budget gate (fail PR if zeptoclaw > 7MB stripped)**
  - **Underlying need:** The motivation for this issue explicitly articulates a core community and architectural concern: keeping the binary small enough to "fit on a robot." This is a proactive measure against the natural bloat that occurs as dependencies are added over time.

While no direct community discussion occurred in this 24-hour window, the maintainers are clearly responding to an implicit user need for a highly performant, memory-efficient agent suitable for edge devices.

### 5. Bugs & Stability
**None reported.** There were no crash reports, regressions, or bug fixes in the last 24 hours.
- The single closed item (**#537** / **#611**) is a stability *enhancement*, as it introduces a CI gate that will prevent future regressions in application binary size, which directly impacts deployment stability.

### 6. Feature Requests & Roadmap Signals
No user-facing feature requests were submitted today. The roadmap signal is exclusively an **infrastructure and enforcement signal**:

- **Prediction:** The completion of the binary size gate suggests the immediate roadmap is shifting from workflow consolidation back to feature development or core optimization. The team now has a safety net in place that prevents uncontrolled size growth. The next version will likely resume feature work (agentic capabilities, tooling) with the confidence that the CI pipeline will enforce the "6MB strategic moat" target.

### 7. User Feedback Summary
No direct user feedback (comments, reactions, or pain points on active issues) was observed in the provided data.
- **Indirect signal:** The maintenance activity is highly positive for user satisfaction regarding deployment constraints. Users seeking a local, low-overhead agent will benefit from the explicit prioritization of a compact binary. The absence of complaints or feature requests suggests either a mature product state or a low volume of public testing on this specific day.

### 8. Backlog Watch
**No backlog items require immediate maintainer attention.**
- The long-standing critical issue **#537** (created 2026-04-23) regarding the CI binary size gate was fully resolved today by **PR #611** (created 2026-06-01). The pipeline is clear of stale or unaddressed critical tasks.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-22

## 1. Today's Overview

ZeroClaw shows high-velocity activity, with **50 issues** and **50 pull requests** updated in the last 24 hours. The project is firmly in a stabilization-and-planning cycle, closing out v0.8.0 and v0.8.1 release trackers while aggressively advancing v0.8.2 (WASM plugins, skills platform) and scoping v0.8.3 (gateway, web dashboard, ZeroCode). A pronounced wave of bug fix PRs from community contributors—particularly `mazhuima`—is rapidly closing gaps in MCP tool isolation, channel reliability, and platform packaging. No new releases were cut today, but the development pipeline is full.

## 2. Releases

No new versions were published today.

The project management trackers show that the **v0.8.0** release queue ([Issue #7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) and the **v0.8.1** integration and channel tracker ([Issue #6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) have both been closed. Active work is now concentrated on:
- **v0.8.2:** WASM plugin program ([Issue #7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314)) and skills platform ([Issue #7852](https://github.com/zeroclaw-labs/zeroclaw/issues/7852)).
- **v0.8.3:** New child trackers opened for channels/providers ([Issue #8072](https://github.com/zeroclaw-labs/zeroclaw/issues/8072)), runtime/agent execution ([Issue #8071](https://github.com/zeroclaw-labs/zeroclaw/issues/8071)), and gateway/web/ZeroCode surfaces ([Issue #8070](https://github.com/zeroclaw-labs/zeroclaw/issues/8070)).

## 3. Project Progress

A substantial set of fixes and features advanced through the PR pipeline today:

**Agent Security and Isolation**
- [PR #8120](https://github.com/zeroclaw-labs/zeroclaw/pull/8120): MCP tools are now scoped per-agent with a denylist, fixing a reported Discord tool-leak across co-resident agents.
- [PR #7960](https://github.com/zeroclaw-labs/zeroclaw/pull/7960): The `execute_pipeline` tool now honors per-agent `ToolAccessPolicy`, preventing agents with restricted toolsets from executing arbitrary tools.
- [PR #7747](https://github.com/zeroclaw-labs/zeroclaw/pull/7747): The runtime now wires `mcp_bundles` config into the agent loop, enforcing per-agent MCP server scoping that was previously schema-only.

**Runtime Stability**
- [PR #8122](https://github.com/zeroclaw-labs/zeroclaw/pull/8122): Daemon IPC loops now treat `ENOBUFS` as a recoverable `accept()` error instead of crashing.
- [PR #8003](https://github.com/zeroclaw-labs/zeroclaw/pull/8003): The previously dead `session_end` lifecycle hook is now wired into RPC session termination paths.
- [PR #7847](https://github.com/zeroclaw-labs/zeroclaw/pull/7847): Fixed a race condition where concurrent workers sharing a session key could corrupt turn order in JSONL persistence.

**Channel Integrations**
- [PR #7958](https://github.com/zeroclaw-labs/zeroclaw/pull/7958): Telegram `mention_only` gate now correctly bypasses the mention check for replies directed at the bot.
- [PR #7768](https://github.com/zeroclaw-labs/zeroclaw/pull/7768): Added loading indicators, icon/nickname branding, and reply feedback support for the LINE channel.
- [PR #7959](https://github.com/zeroclaw-labs/zeroclaw/pull/7959): Auto-approved tools now function correctly on channels configured with non-Full autonomy levels.

**Platform and DX**
- [PR #7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853): Complete overhaul of the Windows self-update mechanism, which was fundamentally broken (Windows locks a running process's image, preventing delete-and-copy swaps).
- [PR #7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946): Added a model context window usage bar to ZeroCode TUI, Gateway Chat, and CLI interactive mode.
- [PR #8093](https://github.com/zeroclaw-labs/zeroclaw/pull/8093): Docker CI now triggers builds from source when base `Dockerfile` / `Dockerfile.debian` changes, not just the pre-built-binary `.ci` variants.
- [PR #7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908): Fixed WebDriver transport bugs in the browser tool (JavaScript IIFE missing `return` keyword; CSS selector escaping for quotes/special characters).
- [PR #7771](https://github.com/zeroclaw-labs/zeroclaw/pull/7771): Observatory events now correctly propagate `channel`, `agent_alias`, and `turn_id` metadata fields across the agent lifecycle.

## 4. Community Hot Topics

The most-engaged conversations reveal a community that is both mature and vocal about specific gaps:

- **[Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808): RFC: Work Lanes, Board Automation, and Label Cleanup** (11 comments). The most active issue. The community is directly shaping how ZeroClaw manages its own backlog, proposing structured project management workflows. This is a strong signal of a committed user base invested in the project's long-term governance.

- **[Issue #2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503): Feature request for Napcat/OneBot channel** (9 comments). A persistent, multi-month request with clear user frustration: "want to connect onebot but cannot find option napcat." Continues to surface as a gap in the Chinese messaging bridge ecosystem.

- **[Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467): Webhook transforms** (6 comments). Users want ZeroClaw to function as a generic webhook receiver accepting arbitrary payloads, not just platform-specific ingresses. The author has a detailed real-world use case (GitHub webhooks).

- **[Issue #5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287): Local-First Mode for Small Models** (2 👍). A recurring request from the privacy-first and edge compute user segment. Users want compact prompting, strict parsing, and no prompt leakage when running with local models like Ollama.

## 5. Bugs & Stability

The bug landscape is dominated by integration and policy enforcement issues, with several critical items still unresolved.

**Active Critical/Severity-1 (S1/P1) Bugs**

| Issue | Description | Impact | Fix Status |
|---|---|---|---|
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | Gemini CLI OAuth authentication fails after success | Workflow blocked for Gemini users | No fix PR identified |
| [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | Context compression drops tool_calls for OpenAI-compatible providers | Tool loops and `invalid message role: system` errors MiniMax users | No fix PR identified |
| [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) | Native/MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turns | MCP tools registered but not received by model | Scoping PRs (#8120, #7747) in progress |
| [#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) | No SSRF protection for `zc_http_request` in WASM plugins | Plugin can reach internal networks | Gating v0.8.2 |

**Resolved or Under Active Fix**
- [#8089](https://github.com/zeroclaw-labs/zeroclaw/issues/8089) (Docker Debian build failing due to missing `aardvark-sys/build.rs`) — **Closed**.
- [#7898](https://github.com/zeroclaw-labs/zeroclaw/issues/7898) (WebDriver tool returns null) — **Fix in [PR #7908](https://github.com/zeroclaw-labs/zeroclaw/pull/7908)**.
- [#7753](https://github.com/zeroclaw-labs/zeroclaw/issues/7753) (Session persistence race corrupting turn order) — **Fix in [PR #7847](https://github.com/zeroclaw-labs/zeroclaw/pull/7847)**.
- [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) (Telegram `mention_only` blocking replies) — **Fix in [PR #7958](https://github.com/zeroclaw-labs/zeroclaw/pull/7958)**.
- [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038) (WebSocket 11/11 auth fail despite valid profile) — **Closed as `needs-repro`**.
- [#7042](https://github.com/zeroclaw-labs/zeroclaw/issues/7042) (Daemon IPC crashes on `ENOBUFS`) — **Fix in [PR #8122](https://github.com/zeroclaw-labs/zeroclaw/pull/8122)**.

**Notable Lower-Severity Reports**
- [#8094](https://github.com/zeroclaw-labs/zeroclaw/issues/8094): Anthropic provider added via Quickstart is unavailable in chat until a full reset. User severity classification is S0, though impact appears limited to UI lifecycle.
- [#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360): Prompt caching breaks on Telegram (forces full re-processing) while working on CLI.
- [#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721): Routing all log output to stdout instead of stderr, breaking `zeroclaw config schema | head` and similar piped workflows.

## 6. Feature Requests & Roadmap Signals

The v0.8.2 and v0.8.3 trackers, combined with user requests, paint a clear picture of where the project is headed:

**Strong Security Posture for v0.8.2**
- [Issue #5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) (SSRF protection) and [Issue #5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) (env var allowlist) are rated P1 and directly gate the WASM plugin program.
- [Issue #6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) (Stronger pairing codes) was accepted as P1. Expect the default 6-digit numeric code to be replaced with 32-character alphanumeric codes or similar.
- [Issue #5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) explicitly demonstrates the threat model: a plugin granted `env_read` permission for one key could read any environment variable.

**Observability Suite**
- [Issue #6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) (Turn-level OTel trace correlation) and [Issue #6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642) (Full prompt/completion capture on `llm.call` spans) are accepted P2 items with community members already scoping the implementation. These are likely candidates for v0.8.3.

**Local-First Strategy**
- [Issue #5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287) (Local-First Mode) is accepted and marked `in-progress`. This mode would strip prompt bloat, disable permissive fallback parsing, and prevent internal instructions from leaking into output—critical for Ollama and small-model users.

**Integration Expansion**
- Ongoing demand for [Napcat/OneBot](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) and [generic webhook transforms](https://github.com/zeroclaw-labs/zeroclaw/issues/2467) signal that users want ZeroClaw as a universal messaging hub, not just a single-platform tool.

## 7. User Feedback Summary

**Frustrations and Pain Points**
- **"Gemini CLI OAuth is simply not working"** — [Issue #4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879). "Right after successfully authenticated Gemini CLI" the provider fails with rate_limit errors. P1, workflow blocked.
- **"zeroclaw logs to stdout instead of stderr"** — [Issue #4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721). Interferes with shell piping and scripting.
- **"context_compression drops assistant(tool_calls) and tool(result)"** — [Issue #6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361). Makes multi-turn conversations with MiniMax and other OpenAI-compatible providers "unusable."
- **"the Webhook system is not really usable right now for generic Webhook senders"** — [Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467). Users want arbitrary payload inspection and transformation.
- **"Windows self-update was fundamentally broken"** — [PR #7853](https://github.com/zeroclaw-labs/zeroclaw/pull/7853). "every `zeroclaw update` failed at the swap phase."
- **"MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turns"** — [Issue #7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756). "Whether the model actually receives the registered tools on its turn depends on the model."

**Satisfaction and Engagement Signals**
- The RFC on project governance ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) has deep, considered participation from the community.
- Multiple contributors (`mazhuima`, `perlowja`, `MaHaoHao-ch`, `Nillth`) are actively submitting and iterating on fixes, demonstrating high engagement and satisfaction with the contribution process.
- Users are investing in observability (OTel span correlation, prompt capture), suggesting production deployments are underway.

## 8. Backlog Watch

Several high-priority items are lingering for weeks or months without visible movement:

- **[Issue #2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) — Napcat/OneBot Channel Request (Opened 2026-03-02).** 9 comments, frequent updates, no formal maintainer response or PR. A persistent gap in the Chinese messaging ecosystem.

- **[Issue #4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) — Gemini CLI OAuth Broken (Opened 2026-03-28).** P1, S1. Nearly 3 months old. No fix PR identified. A blocking issue for Gemini users.

- **[Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) — Audit of 153 Lost Commits (Opened 2026-04-24).** Internal housekeeping for the bulk revert `c3ff635`. No activity in 32 days despite the obvious importance for code history integrity.

- **[Issue #6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) — Context Compression Tool Loops (Opened 2026-05-04).** P1, actively breaking multi-turn tool conversations with non-OpenAI providers. No fix PR identified.

- **[Issue #5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) / [#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) — Plugin Security (Opened 2026-04-19).** P1 items gating the WASM plugin program. Their lack of visible progress is a risk to the v0.8.2 timeline.

- **[Issue #6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) — Stronger Pairing Codes (Opened 2026-05-13).** Accepted P1, no linked PR. A straightforward security improvement that could be a good candidate for a community contribution.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*