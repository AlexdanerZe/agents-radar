# OpenClaw Ecosystem Digest 2026-06-04

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-04 03:41 UTC

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

# OpenClaw Project Digest — 2026-06-04

**Project Health Overview:** High activity with stability as the primary battleground. The project shipped three releases this cycle, including a major security overhaul for plugin installation, but the community is contending with persistent session reliability issues and channel-specific regressions.

---

## 1. Today's Overview

OpenClaw is exhibiting exceptionally high development throughput, with 500 issues and 500 pull requests updated in the last 24 hours. Three new releases shipped (v2026.6.2-beta.1, v2026.6.1, v2026.6.1-beta.3), featuring a shift toward secure operator install policies and improved runtime recovery for interrupted tool calls and media delivery retries. Despite this velocity, the project is dealing with a significant maintainer bottleneck—a large cohort of P1 issues remain tagged `clawsweeper:needs-maintainer-review` or `needs-product-decision`, many unaddressed for weeks. The active PR stack focuses heavily on sanitizing model output (stripping reasoning/thinking tags from chat replies), recovering crashed sessions, and channel delivery fixes, indicating a strong push to improve end-user trust and stability.

---

## 2. Releases

Three versions were published:

- **v2026.6.2-beta.1** — **Major Security Change.** Plugin and skill installation now uses an **operator install policy**, replacing the old dangerous-code scanner path. Clearer surfaces in doctor, CLI, ClawHub, and troubleshooting for all install methods (package, archive, source, upload, marketplace). Thank you @joshavant. [#89516](openclaw/openclaw Issue #89516)

- **v2026.6.1** — **Stability Release.** Agents and CLI-backed runtimes recover more cleanly from interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries. Channels and mobile delivery steadied across Telegram, WhatsApp, iMessage, and Slack. [#88129](openclaw/openclaw Issue #88129), [#88136](openclaw/openclaw Issue #88136), [#88141](openclaw/openclaw Issue #88141), [#88162](openclaw/openclaw Issue #88162), [#88182](openclaw/openclaw Issue #88182)

- **v2026.6.1-beta.3** — Same highlights as v2026.6.1.

No specific breaking changes or detailed migration notes were provided in the data, though the operator install policy implies a user-visible workflow change for package management.

---

## 3. Project Progress

**Merged/Closed (96 PRs today):**

- **UI/Dashboard:** Significant polish to the Workboard operations view — card layout, timestamps, density controls, detail drawer behavior, health summary badges, and filter-aware empty states. [#90057](openclaw/openclaw PR #90057)
- **Channel Connectivity:** Feishu webhook path enforcement merged — now properly rejects requests on unintended paths, closing an information leak surface. [#54904](openclaw/openclaw PR #54904)
- **Auto-Reply Logic:** Message tool sends now correctly counted as delivery, preventing stuck auto-reply loops. [#90123](openclaw/openclaw PR #90123) (closed)
- **Security & Policy:** Policy framework extended to formally cover the `exec-approvals.json` artifact with rules for required file presence, default security, scoped per-agent settings, and allowlist pattern drift. [#90003](openclaw/openclaw PR #90003)

**Active High-Value PRs (Open, High Impact):**

- **Reasoning Tag Sanitization (Multi-Channel):** Critical UX fix stripping raw model reasoning (`<reasoning>`, `<thinking>`, `<antml:reasoning>`) from chat replies across agents ([#90051](openclaw/openclaw PR #90051)), QQBot ([#90132](openclaw/openclaw PR #90132)), and compaction strips now strip invalid thinking signatures ([#90137](openclaw/openclaw PR #90137)).
- **Session Recovery:** Recovering crashed main sessions via lock-file detection fallback ([#86806](openclaw/openclaw PR #86806)). Durable in-process queue fallback for direct-pending announcement handoffs ([#90144](openclaw/openclaw PR #90144)).
- **Memory Architecture:** Multi-slot memory role architecture allowing memory plugins to compose instead of replace each other — `memory.recall`, `memory.compaction`, `memory.capture`, `memory.dreaming`. [#88504](openclaw/openclaw PR #88504)
- **User Experience:** Preserving user-selected model/provider overrides on stale daily/idle rollover ([#90149](openclaw/openclaw PR #90149)). Protecting global agent config defaults from mutation ([#90145](openclaw/openclaw PR #90145)).
- **Edit Tool Fidelity:** P0 fix for fuzzy text matching that silently corrupted unrelated lines in agent edit operations. [#90060](openclaw/openclaw PR #90060)
- **Channel Delivery:** Fixing Discord ws 8.21.0 receiver part limits that force-closed connections ([#89041](openclaw/openclaw PR #89041)). Suppressing Telegram reconnect drain re-entry while delivery is in-flight ([#90066](openclaw/openclaw PR #90066)).

---

## 4. Community Hot Topics

The most active discussions are centered around the core reliability and architecture of the agent runtime:

- **SQLite Migration Architecture** ([#88838](openclaw/openclaw Issue #88838), 17 comments) — The highest-engagement thread. The community is heavily invested in the "branch by abstraction" strategy for migrating core session/transcript storage to SQLite, debating how to avoid repeating the risks of large high-rewrite migrations.

- **Heartbeat & Turn-Completion Failures** ([#65161](openclaw/openclaw Issue #65161), 14 comments; [#88312](openclaw/openclaw Issue #88312), 12 comments) — Persistent user frustration with "Codex stopped before confirming the turn was complete" regressions and heartbeat cadence stalls in isolated mode. These represent the top end-user stability pain points.

- **Session Context Bloat & Hard Resets** ([#63216](openclaw/openclaw Issue #63216), 11 comments; [#67419](openclaw/openclaw Issue #67419), 8 comments) — The repeated re-injection of bootstrap files wasting 20–30% of token context and triggering hard context-overflow resets is a major usability complaint. Users running long-lived sessions are demanding smarter compaction and deduplication.

- **Channel Delivery Regressions** — Mattermost slash commands returning 503 "not yet initialized" ([#68113](openclaw/openclaw Issue #68113), 11 comments) and Windows WebChat UI input/streaming regressions ([#67035](openclaw/openclaw Issue #67035), 14 comments, *closed*) highlight the fragility of the multi-channel delivery system after upgrades.

**Underlying Need:** Users are demanding "production-grade" stability. The volume of `impact:session-state` and `impact:message-loss` issues indicates this is the number one threat to user trust and retention.

---

## 5. Bugs & Stability

Stability remains the project's biggest challenge, with critical regressions and crash-loop risks unaddressed:

**Critical (P1):**

- **Codex Turn-Completion Stall Regression** [#88312](openclaw/openclaw Issue #88312) — Regression of a previously fixed issue. "Codex stopped before confirming the turn was complete" on 2026.5.27+.
- **MCP Tools Not Injected into Subagents** [#85030](openclaw/openclaw Issue #85030) — `bundle-mcp`, per-tool allowlists, and per-agent allowlists all ignored for subagent sessions. Undermines extensibility.
- **Codex OAuth Wedging** [#86215](openclaw/openclaw Issue #86215) — OAuth refresh failures can keep an agent retrying in the same auth lane for hours without clear alerting or aggressive profile rotation.
- **Stale Tool Call Activity Blocking Recovery** [#87310](openclaw/openclaw Issue #87310) — Post-recovery, sessions can remain classified as `blocked_tool_call` due to retained diagnostic state.

**High (P1/P2):**

- **Mattermost 503 Regression** [#68113](openclaw/openclaw Issue #68113) — All slash commands return "not yet initialized" in v2026.4.15+.
- **Discord Guild Reply Failure** [#81484](openclaw/openclaw Issue #81484) — Malformed send payloads, missing message payloads, repeated outbound loops.
- **WebChat Duplication** [#71992](openclaw/openclaw Issue #71992) (*closed*) — Every assistant reply appears exactly twice in Control UI webchat.
- **MiniMax OAuth Cannot Auto-Refresh** [#77467](openclaw/openclaw Issue #77467) — "No credentials found" errors after token expiry (~2 hours).

**Active Fix PRs:** Many high-severity bugs have fix PRs gaining traction: reasoning tag leaks (#90051, #90132), session crash recovery (#86806), edit tool corruption (#90060), gateway startup probe retry (#90142), unbounded DSML buffer growth (#86637).

---

## 6. Feature Requests & Roadmap Signals

**Architectural/Infrastructure:**
- **Session Store Migration to SQLite** ([#88838](openclaw/openclaw Issue #88838)) — The community is actively shaping the data layer foundation.
- **Multi-Slot Memory Architecture** ([#88504](openclaw/openclaw PR #88504)) — Enables composition of memory plugins (recall, compaction, capture, dreaming). Strong candidate for v2026.7.
- **Live Provider Model Catalog** ([#90029](openclaw/openclaw PR #90029)) — Dynamic `/models` discovery for providers with auth-scoped bounded TTL caching. Signals a roadmap push toward reduced reliance on static catalogs.

**User-Requested Features:**
- **Standard Interface for External Security Guardrails** ([#72741](openclaw/openclaw Issue #72741), 8 comments) — High enterprise demand for third-party security integration.
- **Multi-Index Embedding with Model-Aware Failover** ([#63990](openclaw/openclaw Issue #63990)) — Prevents vector space corruption during provider failover.
- **Remote Reranker Endpoint Support** ([#64438](openclaw/openclaw Issue #64438)) — Mirrors remote embedding provider support.
- **Configurable Upload Size Limit for Control UI** ([#71142](openclaw/openclaw Issue #71142)) — Current 5MB hard limit blocks legitimate use cases.
- **Per-Job `acceptSilentStop` Flag** ([#76159](openclaw/openclaw Issue #76159)) — Treats deliberate no-output from cron jobs as success, not error.
- **Warm-Up / Session Reuse for Embedded Agents** ([#67000](openclaw/openclaw Issue #67000)) — Cold start on every `runEmbeddedPiAgent` invocation is costly.

**Prediction:** The next release (v2026.6.x) is likely to include the multi-slot memory foundation, KaTeX UI rendering, reasoning tag sanitization, lock-file recovery, and the live provider catalog. The SQLite migration will remain a multi-release effort.

---

## 7. User Feedback Summary

**Dissatisfaction:**

- **Session Reliability:** The loudest complaint. Users report "stuck sessions," "death spirals" (crash-restart cycles that grow transcripts until OOM), "heartbeats eating replies," and "context bloat." The terms "doomloop" and "death spiral" appear verbatim in bug reports ([#63998](openclaw/openclaw Issue #63998), [#63216](openclaw/openclaw Issue #63216)).
- **Regressions on Update:** Each release seems to carry channel-specific regressions (Mattermost 503, Windows WebChat input swallowing, Discord malformed payloads). Users feel stability is fragile.
- **OAuth/Auth Friction:** Manual re-authentication required every ~2 hours for MiniMax. Codex OAuth failures wedge agents silently for hours.

**Satisfaction:**

- **Contributor Quality:** User-submitted bug reports demonstrate deep technical sophistication — detailed root cause analysis, logs, and reproduction steps (e.g., [#67035](openclaw/openclaw Issue #67035), [#65161](openclaw/openclaw Issue #65161)).
- **Engagement on Architecture:** Users are thoughtfully engaging with complex architectural discussions like the SQLite migration and multi-slot memory.
- **Positive Signal:** Fixes for regressions are actively tracked. The community recognizes and appreciates transparency.
- **Feature Contributions:** KaTeX math rendering and Workboard polish are community contributions, signaling healthy project attachment.

**Use Cases:**
- **Production Deployments:** Discord guilds with voice channels, Mattermost teams behind Cloudflare, Telegram groups with forum topics.
- **Autonomous Orchestration:** Reliance on subagents, MCP servers, cron jobs, and embedded agents — shifting from simple chat to integrated AI developer workflows.
- **Business-Critical:** OAuth resilience, rate limiting, and backup reliability point toward multi-tenant and enterprise use.

---

## 8. Backlog Watch

A significant number of high-severity issues have been stuck for weeks waiting on maintainer review or product decisions. This is the project's most critical internal risk.

**Stuck P1 Issues (Since April 2026):**

- [#63216](openclaw/openclaw Issue #63216) — Repeated hard context-overflow resets despite high `reserveTokensFloor`. Needs product decision on compaction strategy. *(Apr 8)*
- [#63998](openclaw/openclaw Issue #63998) — Session transcript doomloop: crash-restart cycle inflates transcript until gateway OOMs. Potential for catastrophic data loss. Needs live repro / maintainer review. *(Apr 10)*
- [#68751](openclaw/openclaw Issue #68751) — `session-memory` raw prior-session turns replay as current input on `/reset`, causing autonomous re-execution. Security risk. Needs security review. *(Apr 19)*
- [#68691](openclaw/openclaw Issue #68691) — Sandbox zombie processes accumulating under PID 1 until hitting `pids.max`. *(Apr 18)*
- [#67716](openclaw/openclaw Issue #67716) — Deferred compaction debt stranded by bootstrap/reconcile and hot-cache policy. *(Apr 16)*

**Awaiting Author (PRs Blocked):**

- [#87568](openclaw/openclaw PR #87568) — KaTeX math rendering. Stalled despite sufficient proof.
- [#89041](openclaw/openclaw PR #89041) — Discord ws 8.21.0 receiver limit fix. Directly impacts connectivity under normal traffic.
- [#90060](openclaw/openclaw PR #90060) — P0 edit tool fuzzy matching corruption. Waiting on author sign-off.
- [#90003](openclaw/openclaw PR #90003) — Exec policy artifact. Waiting on author.

**Maintainer Capacity Concern:**

The volume of `clawsweeper:needs-maintainer-review` and `needs-product-decision` tags across P1 items (e.g., [#65161](openclaw/openclaw Issue #65161), [#63216](openclaw/openclaw Issue #63216), [#86214](openclaw/openclaw Issue #86214), [#86215](openclaw/openclaw Issue #86215)) suggests that even with high commit throughput, the maintainer team is struggling to keep pace with review and architectural decision-making. Without triage support or additional maintainer bandwidth, this bottleneck could lead to contributor burnout and stagnation of the bug fix pipeline, despite otherwise excellent community momentum.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-04 | **Type:** AI Agent / Personal Assistant Open-Source Landscape Analysis

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is at a critical inflection point. The incumbent leader, OpenClaw, remains the most feature-complete platform, but its session reliability struggles and severe maintainer bottleneck have opened competitive space for a new wave of highly-focused alternatives. Projects like ZeroClaw (Rust, security-first), IronClaw (automation-heavy, NEAR AI-backed), and NanoBot (lightweight orchestration) are setting new architectural standards while compelling the broader ecosystem to shift priorities from raw feature count to production-grade stability, context window economics, and multi-agent orchestration. MCP (Model Context Protocol) productionization has emerged as the universal table stake, with session timeouts, credential handling, and channel delivery dominating cross-project engineering effort. The defining strategic tension is whether the incumbent's breadth or the challengers' focus will deliver the most trusted agent runtime for enterprise and power-user deployments.

---

## 2. Activity Comparison

| Project | 24h Issues Updated | 24h PRs Updated | Merged/Closed (24h) | Releases Today | Activity / Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | ~500 | ~500 | ~96 | **3** (v2026.6.x) | **7/10** — Extreme volume, severe maintainer bottleneck |
| **NanoBot** | ~33 | ~34 | ~20 | 0 | **8/10** — High velocity, strong orchestration focus |
| **Hermes Agent** | ~50 | ~50 | ~5 | 0 | **6/10** — Active, critical Windows regressions unaddressed |
| **PicoClaw** | ~4 | ~11 | ~2 | 0 | **5/10** — Critical PID crash fix awaiting maintainer |
| **NanoClaw** | ~9 | ~9 | 0 | 0 | **6/10** — Strong contributions, zero merges today |
| **NullClaw** | 0 | ~1 | 0 | 0 | **3/10** — Minimal pulse |
| **IronClaw** | ~26 | ~50 | ~26 | **1** (v0.29.1) | **9/10** — Extreme velocity, robust engineering loop |
| **LobsterAI** | ~1 | ~14 | ~14 | **1** (2026.6.3) | **7/10** — High internal execution, low community engagement |
| **TinyClaw** | 0 | 0 | 0 | 0 | **1/10** — Stalled |
| **Moltis** | ~14 | ~4 | ~9 (closed) | **2** | **8/10** — Responsive maintenance, rapid issue closure |
| **CoPaw/QwenPaw** | ~43 | ~49 | ~21 | 0 | **8/10** — High churn, critical memory/crash bugs |
| **ZeptoClaw** | 0 | ~16 (automated) | 0 | 0 | **4/10** — Dependency housekeeping only |
| **ZeroClaw** | ~29 | ~50 | ~4 | 0 | **9/10** — Focused, responsive, security-first |

**Key Takeaway:** The ecosystem is bifurcating into high-velocity definitional projects (IronClaw, ZeroClaw, CoPaw, NanoBot) and stabilization projects (OpenClaw, Moltis, LobsterAI). Projects with stalled maintainer review cycles (PicoClaw, NanoClaw, OpenClaw) face the greatest risk of contributor attrition.

---

## 3. OpenClaw's Position

### Competitive Advantages
- **Unmatched Scale:** OpenClaw's 500+ issue/PR daily volume dwarfs every other project. Its breadth of channels, plugins, and skills remains the deepest in the ecosystem.
- **Architectural Ambition:** The multi-slot memory architecture (#88504) and SQLite migration (#88838) are the most forward-looking structural bets among all projects, directly addressing the context window crisis.
- **Community Maturity:** User-submitted bug reports demonstrate sophisticated root-cause analysis and deep platform investment. The community is technically formidable.

### Critical Vulnerabilities
- **Maintainer Bottleneck:** P1 issues (session doomloops, OOM crashes, compaction debt) sit for weeks awaiting `needs-product-decision` or `needs-maintainer-review` tags. This is the most severe capacity constraint in the ecosystem.
- **Trust Erosion:** "Death spirals," "doomloops," and "regressions on every update" are verbatim user feedback. Channel-specific regressions (Mattermost 503, WebChat duplication) create a pattern of fragility.
- **Review Latency:** Community PRs for critical fixes (Discord WS limits, edit tool corruption) are awaiting author sign-off after maintainer merge readiness.

### Threat Landscape
- **ZeroClaw** and **IronClaw** are aggressively competing on architectural cleanliness and maintainer responsiveness, directly targeting the experienced ops crowd that OpenClaw risks alienating.
- **NanoBot** and **CoPaw** are competing on multi-agent orchestration maturity, offering cleaner implementations of Supervisor/Worker patterns.

### Strategic Path
OpenClaw must address its maintainer bottleneck or risk becoming a "legacy platform" that prioritizes compatibility over forward momentum. The SQLite and memory bets are high-reward but require execution bandwidth the team currently lacks.

---

## 4. Shared Technical Focus Areas

### MCP Productionization (Cross-Project Requirement)
MCP is no longer a novelty feature—it is a stability contract demanding first-class session management, credential hygiene, and timeout handling.

| Project | Specific MCP Issue |
|---|---|
| **NanoBot** | Session termination crash (Fixed #4171) |
| **Hermes Agent** | Auth token mismatch on `mcp add` vs `mcp test` (Fixed #37792) |
| **LobsterAI** | Node toolchain path loss, session timeout on reload (Fixed #2100, #2104) |
| **Moltis** | Environment variable leaks via `mcp_list` (Fixed #1054) |
| **CoPaw** | ACP server metadata + tool parameter exposure (#4949) |
| **ZeroClaw** | Pluggable OIDC auth provider for transport (#7141) |

### Context Window Economics (Universal Pain Point)
The industry's most persistent user dissatisfaction driver. Every major project has high-severity issues related to token bloat, compaction failures, or context overflow.

| Project | Specific Context Issues |
|---|---|
| **OpenClaw** | Hard context-overflow resets, bootstrap file bloat, "doomloop" OOM (#63216, #63998) |
| **CoPaw** | Compaction `AttributeError` crashes, 37GB ChromaDB bloat, manual config requirement (#4795, #4933, #4937) |
| **IronClaw** | `builtin.http` returns 1.2MB raw HTML, `skill_list` unbounded at 14,612 bytes (#4425, #4428) |
| **NanoBot** | Long-running tasks stall, agent hangs on "Starting execution now" (#1022) |

### Multi-Agent Orchestration (Architecture Convergence)
The Supervisor/Worker pattern is becoming the standard for complex tasks. Projects that ship first-class orchestration primitives are gaining mindshare.

| Project | Orchestration Primitive |
|---|---|
| **NanoBot** | Mailbox Channel for inter-agent comm (#3461), Run-Level Hooks (#4176) |
| **ZeroClaw** | Session Branching / Conversation Forking (#7168) |
| **IronClaw** | Reborn Runtime, Trigger Policies, Subagent System |
| **CoPaw** | Self-Evolution Requests (#3470), Dream Agent Memory |
| **OpenClaw** | Subagent MCP tool injection gap (#85030) |

### Channel Delivery Reliability (Fragile Layer)
Channel integration is the most vulnerable surface area, with delivery bugs eroding trust across the board.

| Project | Reported Delivery Issue |
|---|---|
| **OpenClaw** | Discord WS force-close, Telegram reconnect drain, Mattermost 503 |
| **Moltis** | Telegram streaming corruption mixing progress with final reply (#1097) |
| **CoPaw** | Cross-user message merging in queue routing, ACL sender ID drop (#4932, #4925) |
| **ZeroClaw** | Slack coding agent exhausts `max_tool_iterations` with duplicate commands (#7143) |

---

## 5. Differentiation Analysis

### Architectural Philosophy
| Project | Language | Core Philosophy |
|---|---|---|
| **ZeroClaw** | Rust | `forbid(unsafe_code)`, pluggable auth providers, TUI-first |
| **PicoClaw** | Go | Lightweight gateway, embedded/hardware edge |
| **IronClaw** | Rust | Automation and testing discipline, NEAR AI team process |
| **NanoBot** | Python | Minimalist core (~4k lines), orchestration via mailbox and hooks |
| **CoPaw** | Python/TS | Memory consolidation ("Dreaming"), Desktop Tauri app |
| **OpenClaw** | Python/TS | Broadest feature surface, plugin/skill ecosystem |
| **Hermes Agent** | Python | Enterprise Desktop (WeCom), accessibility, i18n |

### Target User Profile
| Project | Primary User |
|---|---|
| **ZeroClaw** | Security-conscious DevSecOps operator |
| **IronClaw** | Enterprise automation engineer |
| **NanoBot** | Python developer building agent workflows |
| **CoPaw** | Desktop power user, Qwen ecosystem developer |
| **Hermes Agent** | Multi-platform enterprise user (Windows, WeCom) |
| **LobsterAI** | Collaboration-focused team user |
| **OpenClaw** | Broadest audience, from hobbyist to enterprise |

### Competitive Moat
- **ZeroClaw**: Security posture (forbid unsafe, pluggable auth, OIDC). No other project prioritizes this as their core differentiator.
- **IronClaw**: Testing rigor (E2E, nightly) and automation depth (triggers, Cron). Most robust engineering culture visible.
- **NanoBot**: Cleanest multi-agent Python primitives. Low barrier to entry for complex workflows.
- **CoPaw**: Unique "Dream Agent" memory architecture. Tauri Desktop integration + Qwen model ecosystem.
- **OpenClaw**: Incumbent community gravity and breadth. Plugin/skill network effects.

---

## 6. Community Momentum & Maturity

### Tier 1: Highest Velocity & Strategic Definition
*Projects actively defining the category's future, shipping rapidly with clear architectural vision.*

| Project | Velocity Signal | Risk |
|---|---|---|
| **ZeroClaw** | 9/10 | Moderate — small community, must sustain velocity |
| **IronClaw** | 9/10 | Low — NEAR AI backing, strong team discipline |
| **NanoBot** | 8/10 | Low — efficient, clean architecture |
| **CoPaw** | 8/10 | Moderate — critical memory bugs threaten trust |

### Tier 2: Stabilization & Feature Hardening
*Projects with broad adoption but actively addressing technical debt and regressions.*

| Project | Health Signal | Key Risk |
|---|---|---|
| **OpenClaw** | 7/10 (strained) | Maintainer bottleneck, session reliability erosion |
| **LobsterAI** | 7/10 | Low community engagement, subscription friction |
| **Moltis** | 8/10 | Docker reliability gap |
| **Hermes Agent** | 6/10 | Windows update path broken, security CVEs open |

### Tier 3: Low Activity / Specialized Niche
*Maintenance-mode projects or those serving specific verticals.*

| Project | Health Signal |
|---|---|
| **PicoClaw** | 5/10 (critical fixes stuck in review) |
| **NanoClaw** | 6/10 (good contributions, slow merging) |
| **NullClaw** | 3/10 (single PR active) |
| **ZeptoClaw** | 4/10 (automated dependency bumps) |
| **TinyClaw** | 1/10 (fully stalled) |

---

## 7. Trend Signals

### MCP is the Hardware Abstraction Layer for Agents
Every major framework speaks MCP. The competitive differentiator is *session management quality*—timeout handling, credential hygiene, and TCP reconnect logic. Projects that treat MCP as a first-class reliability layer (NanoBot's auto-reconnect, LobsterAI's npx path hardening) are pulling ahead.

### Context Window Economics Defines UX
The "death spiral" (crash-restart cycle inflating transcripts until OOM) is the single most damaging user experience defect in the ecosystem. OpenClaw and CoPaw are investing heavily in compaction and deduplication; ZeroClaw's Rust resource discipline prevents the problem architecturally. Solutions to token bloat will be a decisive trust signal for serious deployments.

### Multi-Agent is Replacing Chatbot as the Default Pattern
The community has moved beyond question-answering. NanoBot's Mailbox Channel, ZeroClaw's session branching, and IronClaw's trigger automations all point toward Supervisor/Worker topologies becoming the expected deployment pattern. Agents that cannot delegate, fork, and communicate asynchronously are seen as toys.

### Security is Moving from Plugin to Architecture Level
ZeroClaw's `forbid(unsafe_code)` and pluggable OIDC providers set the security ceiling for the ecosystem. OpenClaw's operator install policy and Hermes' detailed CVSS-scored audit reports (8.6/9.1) demonstrate that enterprises are now demanding platform-level security, not bolt-on policies.

### Rust is the Emerging Infrastructure Layer
After years of Python dominance, Rust projects (ZeroClaw, PicoClaw, ZeptoClaw) are gaining traction for agent infrastructure. The value proposition—resource efficiency, memory safety, and strict compile-time guarantees—directly addresses the stability and security pain points that dominate the discourse in Python-based projects.

### Desktop is the New Edge
Hermes Agent's system tray requests and CoPaw's Tauri Plugin Loader signal that agents are moving from "web chat" to "OS-level co-pilot." Desktop maturity (offline support, system tray, file system access, keyboard shortcuts) is becoming a competitive battleground distinct from web UI and mobile delivery.

---

**Bottom Line for Decision-Makers:**

The ecosystem is rapidly converging on MCP productionization, context-aware agent loops, and multi-agent patterns. OpenClaw retains the broadest ecosystem but faces a credibility gap on stability and maintainer responsiveness. ZeroClaw and IronClaw represent the highest velocity, most disciplined engineering cultures. NanoBot offers the cleanest orchestration primitives for Python developers. Project selection should weight **context management maturity** and **multi-agent architecture quality** above raw feature counts, as the former are the strongest predictors of production-grade reliability.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot Project Digest — 2026-06-04**

---

### 1. Today’s Overview
NanoBot is experiencing a high-velocity development phase, with **34 pull requests** and **33 issues** updated in the last 24 hours. The maintainers closed or merged **20 PRs**, signaling strong commit to both feature work and essential bug fixes. Multi-agent and orchestration infrastructure dominated the merged activity, while the community continued to push for better security, WebUI polish, and expanded channel support. No official release was published today, suggesting the team may be bundling changes into a future minor or major version.

---

### 2. Releases
*No new releases today.*

---

### 3. Project Progress

**Merged/Closed PRs (Highlights):**

- **MCP Stability Fix** – [#4171](https://github.com/HKUDS/nanobot/pull/4171): Merged. Automatically reconnects terminated MCP sessions (direct fix for [#4168](https://github.com/HKUDS/nanobot/issues/4168)).
- **Memory Durability & Privacy** – [#4183](https://github.com/HKUDS/nanobot/pull/4183): Merged. Adds PII redaction, atomic writes, and general solidification of the memory module.
- **WebUI Robustness** – [#4157](https://github.com/HKUDS/nanobot/pull/4157): Merged. Bounds WebUI startup fetch waits so the UI no longer hangs on slow API responses.
- **WebUI Event Bus** – [#4135](https://github.com/HKUDS/nanobot/pull/4135): Merged. Refactored WebUI runtime state onto an event bus for better UI reactivity and maintainability.
- **Auth System** – [#3221](https://github.com/HKUDS/nanobot/pull/3221): Merged. Adds `nanobot auth` command with OAuth Device Flow.
- **Provider Bugfix** – [#3932](https://github.com/HKUDS/nanobot/pull/3932): Merged. Fixes `duplicate tool_call_id` error in stream mode for OpenAI-compatible providers.
- **Dream/Consolidator Prompts** – [#3952](https://github.com/HKUDS/nanobot/pull/3952) / [#3990](https://github.com/HKUDS/nanobot/pull/3990): Merged. Replaced the two-phase Dream class and optimized long-term memory consolidation prompts for MECE deduplication.
- **Multi-Agent Mailbox Channel** – [#3461](https://github.com/HKUDS/nanobot/pull/3461): Merged. File-system-based mailbox channel for inter-agent communication.
- **Channel Fixes** – [#4180](https://github.com/HKUDS/nanobot/pull/4180) (QQ pairing codes), [#4184](https://github.com/HKUDS/nanobot/pull/4184) (Feishu bot mention stripping).

**Newly Opened PRs (Active):**

- **Run-Level Hooks** – [#4176](https://github.com/HKUDS/nanobot/pull/4176): Adds `before_run`, `after_run`, `on_error` lifecycle hooks for agents.
- **Bocha Search Provider** – [#4182](https://github.com/HKUDS/nanobot/pull/4182): Adds a new web search provider (official API for DeepSeek, commonly used in China).
- **WebUI Shortcut** – [#4185](https://github.com/HKUDS/nanobot/pull/4185): Adds `Cmd/Ctrl+Shift+O` for new chat (after competing PR [#4181](https://github.com/HKUDS/nanobot/pull/4181) was closed).
- **Azure AAD Auth** – [#4126](https://github.com/HKUDS/nanobot/pull/4126): Adds identity-based auth for Azure OpenAI.

---

### 4. Community Hot Topics

| Issue | Focus | Activity | Community Signal |
|---|---|---|---|
| [#222](https://github.com/HKUDS/nanobot/issues/222) | Multi-agent setup | 10 comments, 7 👍 | **Top requested feature.** Strong demand for guides and configs. |
| [#1022](https://github.com/HKUDS/nanobot/issues/1022) | Long-running task hangs | 4 comments, 3 👍 | Critical UX pain point for power users running batch tasks. |
| [#912](https://github.com/HKUDS/nanobot/issues/912) | Task-specific models | 3 comments, 3 👍 | Users want separate models for chat vs. tools vs. browsing. |
| [#954](https://github.com/HKUDS/nanobot/issues/954) | Tool call streaming leak | 3 comments | High severity UX regression. Internal commands leaking to users. |
| [#979](https://github.com/HKUDS/nanobot/issues/979) | AI bypassing `rm` restrictions | 5 comments | Humorous but highlights deep safety sandboxing concerns. |
| [#4179](https://github.com/HKUDS/nanobot/issues/4179) | Native A2A Orchestration | *New* | Immediately follows the mailbox channel merge — community wants Supervisor → Researcher → Writer flows. |

**Underlying Need:** The community is moving beyond single-agent use and aggressively asking for **native multi-agent orchestration** (Supervisor, subagents, profiles, control plane).

---

### 5. Bugs & Stability

| Severity | Issue | Description | Status |
|---|---|---|---|
| **Critical** | [#4168](https://github.com/HKUDS/nanobot/issues/4168) | MCP session terminates randomly (`McpError: Session terminated`) | **Fixed in [#4171](https://github.com/HKUDS/nanobot/pull/4171)** |
| High | [#954](https://github.com/HKUDS/nanobot/issues/954) | Progress streaming leaks `exec()`, `read_file()`, `list_dir()` to user chat | Open |
| High | [#1022](https://github.com/HKUDS/nanobot/issues/1022) | Agent stalls on long-running tasks ("Starting execution now" but does nothing) | Open |
| Medium | [#935](https://github.com/HKUDS/nanobot/issues/935) | Remote MCP over Streamable HTTP times out (`asyncio.CancelledError`) | Open |
| Medium | [#143](https://github.com/HKUDS/nanobot/issues/143) | Filesystem tools do not enforce `restrict_to_workspace` (security scope creep) | Open (4 👍) |
| Low | [#896](https://github.com/HKUDS/nanobot/issues/896) | Telegram/Discord media files never cleaned up, causing unbounded disk growth | Open |

---

### 6. Feature Requests & Roadmap Signals

**Strong Predictions for Next Release:**

- **Subagent Control Plane** – [#1006](https://github.com/HKUDS/nanobot/issues/1006) (list/kill commands) is the logical next step after the mailbox channel ([#3461](https://github.com/HKUDS/nanobot/pull/3461)) was merged.
- **Agent Hooks / Lifecycle** – The newly opened [#4176](https://github.com/HKUDS/nanobot/pull/4176) directly enables pre/post execution hooks, which is foundational for complex orchestration.
- **WebUI Shortcut & Polish** – [#4178](https://github.com/HKUDS/nanobot/issues/4178) / [#4185](https://github.com/HKUDS/nanobot/pull/4185) shows the team is quickly responsive to WebUI UX requests.
- **Task-Specific Model Routing** – [#912](https://github.com/HKUDS/nanobot/issues/912) (3 👍) addresses a core limitation of single-model config and fits the current trajectory.
- **Channel Expansion** – Mattermost ([#1011](https://github.com/HKUDS/nanobot/issues/1011), 4 👍), SimpleX ([#240](https://github.com/HKUDS/nanobot/issues/240), 2 👍), and WeChat ([#192](https://github.com/HKUDS/nanobot/issues/192)) requests remain open with community interest.

**Signals for Later Roadmap:**
- **Sandbox Interface** – [#931](https://github.com/HKUDS/nanobot/issues/931) proposes Firecracker/Deno isolation for untrusted plugins.
- **Zero-Token Routers** – [#990](https://github.com/HKUDS/nanobot/issues/990) asks for pre-handler hooks to skip LLM for pattern-matched messages (e.g., `#diary`), suggesting users want ultra-lightweight routing.

---

### 7. User Feedback Summary

**Positive Sentiments:**
- Architecture remains highly praised ("clean and lightweight under 4k lines").
- Contributor enthusiasm is very high — users are actively submitting feature PRs (shortcuts, providers, refactors).

**Pain Points:**
- **Hallucinations in `exec` tool** ([#937](https://github.com/HKUDS/nanobot/issues/937)): User paused evaluation entirely due to unreliable tool calling, even with SOTA models.
- **Long-running task reliability** ([#1022](https://github.com/HKUDS/nanobot/issues/1022)): Hurting adoption for serious automation use cases.
- **Sandbox isolation** ([#143](https://github.com/HKUDS/nanobot/issues/143), [#940](https://github.com/HKUDS/nanobot/issues/940)): AI cannot access host filesystem for media/skills, creating a split workspace experience.
- **Multi-agent clarity** ([#222](https://github.com/HKUDS/nanobot/issues/222)): Users sense it *can* work but want docs and out-of-the-box guidance.

---

### 8. Backlog Watch

*Issues that are high importance but have received no official maintainer response or are long-stale:*

| Issue | Type | Age | Stakes |
|---|---|---|---|
| [#97](https://github.com/HKUDS/nanobot/issues/97) | RFC: Architecture Overhaul | Feb 4 | 6 👍, detailed proposal on memory/security/testing. No maintainer acknowledgment. |
| [#80](https://github.com/HKUDS/nanobot/issues/80) | Feature: BM25/TF-IDF Memory Retrieval | Feb 4 | Directly improves token efficiency as memory grows. |
| [#143](https://github.com/HKUDS/nanobot/issues/143) | Security: Filesystem Scoping | Feb 5 | 4 👍. Open for 4 months with zero response. Significant trust/safety gap. |
| [#1012](https://github.com/HKUDS/nanobot/issues/1012) | Feature: Subagent Profiles | Feb 22 | Perfectly aligns with current multi-agent trajectory; risks being built without this design input. |
| [#1011](https://github.com/HKUDS/nanobot/issues/1011) | Feature: Mattermost Channel | Feb 22 | 4 👍. Community wants a self-hosted, privacy-respecting channel option. |
| [#954](https://github.com/HKUDS/nanobot/issues/954) | Bug: Streaming Leaks | Feb 21 | High severity regression. Open for over 3 months with no fix PR. |

---

*Summary: NanoBot is in an intense feature-building phase with excellent PR throughput. The largest risk is the accumulation of high-severity bugs (stream leaks, long job hangs) and unaddressed security proposals in the backlog as the team focuses on orchestration features.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

### Hermes Agent Project Digest - 2026-06-04

---

### 1. Today's Overview

Hermes Agent experienced a highly active development day, with a total of 100 items (50 Issues, 50 PRs) updated in the last 24 hours. The project shows strong community velocity, maintaining 44 open/active issues and 46 open pull requests. While no new releases were cut today, significant progress was made on critical stability patches, particularly resolving a persistent Docker UID remapping bug that affected homelab/NAS users. The community's focus remains sharply divided between the security hardening of gateway integrations and addressing a growing volume of cross-platform reliability reports, specifically regressions on Windows and the Desktop client.

---

### 2. Releases

No new releases were published on 2026-06-04. The latest available release remains v0.15.1, though it is worth noting user reports from [Issue #38618](https://github.com/NousResearch/hermes-agent/issues/38618) regarding confusion when the `main` branch commit history diverges from the latest release tag.

---

### 3. Project Progress

The following key issues and PRs were resolved/merged today, signaling improvements to Docker stability and tooling fundamentals:

- **Docker UID Remapping Stability**: The persistent entrypoint ownership bug ([Issue #27221](https://github.com/NousResearch/hermes-agent/issues/27221)) was resolved. The fix, initially proposed by sarvesh1327 in [#37928](https://github.com/NousResearch/hermes-agent/pull/37928) and salvaged by benbarclay in [#38655](https://github.com/NousResearch/hermes-agent/pull/38655), ensures that runtime-writable install trees are correctly chowned when `HERMES_UID` is remapped.
- **Windows Setup Error** ([Issue #37827](https://github.com/NousResearch/hermes-agent/issues/37827)) was closed following a fix for a git checkout failure during the Windows bootstrap process.
- **MCP 401 Unauthorized Bug** ([Issue #37792](https://github.com/NousResearch/hermes-agent/issues/37792)) was closed. The issue involved a token handling mismatch between `hermes mcp add` and `hermes mcp test`.
- **Desktop Bug-Fix Batch Salvage**: A major bug-fix batch ([PR #38677](https://github.com/NousResearch/hermes-agent/pull/38677), teknium1) was opened, salvaging contributions addressing desktop attachments, IME composition, and scroll resets.

---

### 4. Community Hot Topics

The most active discussions today revolve around accessibility, security policies, and Desktop quality-of-life features:

- **Accessibility** ([Issue #26689](https://github.com/NousResearch/hermes-agent/issues/26689) – *8 comments*): The highest-engagement topic. A blind VoiceOver user explicitly praises the "extremely powerful backend" but states the UX is "very difficult for screen-reader users." This highlights a significant demographic being locked out of the ecosystem.
- **Docker Stability** ([Issue #27221](https://github.com/NousResearch/hermes-agent/issues/27221) – *6 comments, 2 👍*): The now-closed Docker bug was a critical pain point for Unraid/Synology users, and its resolution was widely anticipated.
- **Security & Governance** ([Issue #33905](https://github.com/NousResearch/hermes-agent/issues/33905) – *3 comments, 1 👍*): Users are pushing for granular per-tool approval policies, reflecting a broader demand for enterprise governance beyond the current "dangerous shell commands" guard.
- **Desktop Feature Demand** ([Issue #38007](https://github.com/NousResearch/hermes-agent/issues/38007) – *1 comment, 1 👍* & [Issue #37713](https://github.com/NousResearch/hermes-agent/issues/37713) – *1 comment, 1 👍*): System tray support and remote profile switching are the most desired desktop features, indicating frustration with cold-start delays.
- **Internationalization** ([PR #38206](https://github.com/NousResearch/hermes-agent/pull/38206)): A strong signal from the Chinese-speaking community, adding a lightweight i18n framework and Simplified Chinese translation for the Desktop client.
- **Security Audit** ([Issue #38068](https://github.com/NousResearch/hermes-agent/issues/38068)): A detailed CVSS 8.0/8.6 report on Slack approval buttons bypassing authorization controls.

---

### 5. Bugs & Stability

The bug report today is heavily weighted toward Critical (P1) and High (P2) issues, with a major concentration on Windows regressions and high-severity security gaps.

**Critical (P1):**
- `[#37881]` [Bug]: `hermes update` permanently bricks installs on Windows. The venv rebuild fails and leaves a broken environment. **No fix PR yet.**
- `[#38407]` [Bug]: Windows Desktop App fails after update due to an incomplete git checkout and FS cache mismatch. **No fix PR yet.**
- `[#38652]` [Bug]: Infinite auto-reset loop caused by `parse_available_output_tokens_from_error()` failing to detect OpenRouter/Nous output cap formats. **No fix PR yet.**
- `[#38674]` [Bug]: Agent blindly executes all `.py` files in the current working directory (e.g., `setup.py`). **No fix PR yet.**
- `[#38638]` [Security]: Gateway own-policy adapters fail open without allowlists (CVSS 9.1/9.3). **No fix PR yet.**

**High (P2):**
- `[#30230]` [Bug]: Gateway hits the macOS default fd limit of 256, crashing on file operations. **Awaiting maintainer feedback.**
- `[#38580]` [Bug]: `requests` 2.33.0 aarch64 wheel missing `_types.py`, crashing Hermes on NVIDIA Jetson. **No fix PR yet.**
- `[#38662]` [Bug]: `/claude` gateway command broken — passes `--acp --stdio` to Claude Code CLI which does not support these flags. **No fix PR yet.**
- `[#38683]` [Bug]: Telegram gateway sessions fail to refresh in the Desktop UI until a full restart. **No fix PR yet.**

**Resolved Today:**
- `[#27221]` Docker UID remap bug. (Fixed by [#38655](https://github.com/NousResearch/hermes-agent/pull/38655)).
- `[#37792]` MCP 401 Unauthorized bug on `hermes mcp add`.

---

### 6. Feature Requests & Roadmap Signals

The community roadmap is heavily weighted toward Desktop maturity, security governance, and internationalization.

- **Desktop Maturity**: There is a clear push to evolve the Desktop client into a robust IDE. Key signals include requests for **system tray support** ([#38007](https://github.com/NousResearch/hermes-agent/issues/38007)), **true remote workspace file browsing** ([#38671](https://github.com/NousResearch/hermes-agent/issues/38671)), **session grouping by project** ([#38680](https://github.com/NousResearch/hermes-agent/issues/38680)), **Mermaid diagram rendering** ([#38654](https://github.com/NousResearch/hermes-agent/issues/38654)), and **offline installation** ([#38684](https://github.com/NousResearch/hermes-agent/issues/38684)).
- **Security Overhaul**: The combination of the **per-tool approval policy** feature request ([#33905](https://github.com/NousResearch/hermes-agent/issues/33905)) and today's critical security reports ([#38068](https://github.com/NousResearch/hermes-agent/issues/38068), [#38638](https://github.com/NousResearch/hermes-agent/issues/38638)) strongly suggests the next major release will feature a significant access control overhaul.
- **Internationalization**: The community-authored i18n PR ([#38206](https://github.com/NousResearch/hermes-agent/pull/38206)) and several issues from Chinese-speaking users signal a strategic push into the Asian market.
- **Platform Parity**: Continued investment in **WeCom infrastructure** ([#38660](https://github.com/NousResearch/hermes-agent/pull/38660), [#38678](https://github.com/NousResearch/hermes-agent/pull/38678)), **Gemini OAuth discovery** ([#29361](https://github.com/NousResearch/hermes-agent/pull/29361)), and **Webhook Bearer Token Auth** ([#27601](https://github.com/NousResearch/hermes-agent/pull/27601)) demonstrate a commitment to platform diversity.

---

### 7. User Feedback Summary

- **Satisfaction**: Users acknowledge the project's technical power, referring to the "extremely powerful backend and agent ecosystem" ([#26689](https://github.com/NousResearch/hermes-agent/issues/26689)). The community is technically sophisticated, contributing detailed CVSS-scored security audits ([#38068](https://github.com/NousResearch/hermes-agent/issues/38068)) and complex feature PRs ([#38206](https://github.com/NousResearch/hermes-agent/pull/38206)).
- **Dissatisfaction & Pain Points**:
    - **Update Stability**: The most severe pain point. The Windows update path is actively broken for multiple users ([#37881](https://github.com/NousResearch/hermes-agent/issues/37881), [#38407](https://github.com/NousResearch/hermes-agent/issues/38407)), completely bricking their installations.
    - **Silent Failures**: Cron agents losing memory write capability ([#38647](https://github.com/NousResearch/hermes-agent/issues/38647)) and MCP servers reporting as "failed" despite working ([#38650](https://github.com/NousResearch/hermes-agent/issues/38650)) erode user trust in agent operations.
    - **Desktop UX "Death by a Thousand Cuts"**: The composer becoming unfocusable ([#38314](https://github.com/NousResearch/hermes-agent/issues/38314)), scrollbars jumping ([#38669](https://github.com/NousResearch/hermes-agent/issues/38669)), and lack of system tray support ([#38007](https://github.com/NousResearch/hermes-agent/issues/38007)) create a frustrating user experience.
    - **Accessibility Exclusion**: A core demographic of blind users is entirely locked out of the UX ([#26689](https://github.com/NousResearch/hermes-agent/issues/26689)).

---

### 8. Backlog Watch

Several high-quality, well-scoped contributions from the community remain stalled without maintainer review or triage. This represents a bottleneck in the project's delivery velocity:

- `[#26689]` **Accessibility for VoiceOver** (Issue, May 16): The most discussed issue in the project. Over three weeks with no official maintainer triage or assignment.
- `[#27601]` **Webhook Bearer Token Auth** (PR, May 17): A clean feature PR awaiting review for over two weeks.
- `[#29361]` **Gemini OAuth Model Discovery** (PR, May 20): Significant feature update for Google integration with zero review activity.
- `[#30230]` **macOS File Descriptor Limit** (Issue, May 22): A clearly diagnosed bug with a specific technical solution, no linked PR.
- `[#35668]`, `[#37063]`, `[#37057]` **macOS Gateway Resilience Fixes** (PRs, May 31 - June 1, *drzeast-png*): A critical series of PRs fixing launchd KeepAlive races and restart logic. These are essential for macOS reliability but remain unmerged for almost a week.
- `[#38638]` **Gateway Policy Security** (Issue, June 4): A high-severity security vulnerability (CVSS 9.1) filed today requiring immediate maintainer attention.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest for 2026-06-04

## 1. Today's Overview
Project activity remains high with **11 Pull Requests** and **4 Issues** updated in the last 24 hours. Two PRs were successfully closed/merged, including a critical Go runtime security patch and a MQTT TLS configuration fix. The development team is actively addressing several functional regressions, particularly around session management and tool execution, evidenced by a flurry of targeted fix PRs from core contributor `chengzhichao-xydt`. However, community concern is growing over the stagnation of several high-priority bug fixes lingering in stale review status. Overall, the project shows strong contributor momentum but faces a bottleneck in merging critical stability patches.

## 2. Releases
**None.** No new releases were cut today. The latest stable version remains within the v0.2.x series. A documentation PR ([#2995](https://github.com/sipeed/picoclaw/pull/2995)) is active to add release highlights for v0.2.5 through v0.2.9 to the README, suggesting the team is keeping documentation current despite not formalizing a v0.3.0 release.

## 3. Project Progress
Two PRs landed in the last 24 hours:
- **Security Patch ([#2997](https://github.com/sipeed/picoclaw/pull/2997)):** Bumped Go runtime from 1.25.10 to 1.25.11 to patch GO-2026-5039, a critical vulnerability involving unescaped header names in `net/textproto` error messages.
- **Platform Fix ([#2899](https://github.com/sipeed/picoclaw/pull/2899)):** Closed after adding configurable TLS verification (`TLSSkipVerify`) for the MQTT channel, fixing a security gap where insecure connections were forced.

**Active development highlights** (updated today):
- **Session Regression Fix ([#2992](https://github.com/sipeed/picoclaw/pull/2992)):** Patches a v0.2.9 regression where old messages were incorrectly attached to new Web UI sessions during history promotion.
- **Context Debugging ([#2985](https://github.com/sipeed/picoclaw/pull/2985)):** Improves the `/context` command to display soft summarization thresholds, addressing user confusion over context budget.
- **Error Handling ([#2996](https://github.com/sipeed/picoclaw/pull/2996)):** Replaces 7 instances of ignored `json.Marshal` errors in the `exec` tool with proper error responses, preventing silent failures in LLM tool responses.

## 4. Community Hot Topics
- **Streaming Config Request ([#2404](https://github.com/sipeed/picoclaw/issues/2404)):** The most active issue (11 comments, 1 👍) asks for a `"streaming": true` config flag to enable Server-Sent Events (SSE) for LLM backends. This reflects a strong desire for simpler transparent proxy behavior akin to the OpenAI Python client.
- **PID Identity Crash Loop ([#2720](https://github.com/sipeed/picoclaw/issues/2720)):** A high-priority bug causing gateway startup failures (8 comments). The community is engaged and frustrated by the instability; multiple fix attempts are competing for review in PRs [#2813](https://github.com/sipeed/picoclaw/pull/2813) and [#2955](https://github.com/sipeed/picoclaw/pull/2955).
- **Tool Calls Dropped ([#2958](https://github.com/sipeed/picoclaw/issues/2958)):** Users report that WebSocket agent pipelines break under consecutive tool requests, severely impacting agentic AI workflows.

## 5. Bugs & Stability
- **[HIGH] PID Verification Crash Loop ([#2720](https://github.com/sipeed/picoclaw/issues/2720)):** The most impactful open bug. Gateway fails to start if a recycled PID is detected. Two fix attempts are currently awaiting maintainer decision.
- **[HIGH] Tool Calls Dropped in WebSocket ([#2958](https://github.com/sipeed/picoclaw/issues/2958)):** A critical regression for agent users. The linked fix PR [#2957](https://github.com/sipeed/picoclaw/pull/2957) exists but is currently stale.
- **[MEDIUM] Config Merge Resets Channels ([#2956](https://github.com/sipeed/picoclaw/pull/2956)):** A configuration management bug where loading `.security.yml` disables channel settings from `config.json`. Currently open and stale.
- **[MEDIUM] 32-bit Android Support ([#2954](https://github.com/sipeed/picoclaw/issues/2954)):** Platform compatibility limitation, unaddressed by the core team.
- **[LOW/RESOLVED] Go Security CVE ([#2997](https://github.com/sipeed/picoclaw/pull/2997)):** Patched.
- **[LOW/RESOLVED] MQTT TLS Vulnerability ([#2899](https://github.com/sipeed/picoclaw/pull/2899)):** Patched.

## 6. Feature Requests & Roadmap Signals
The data indicates the immediate roadmap is focused on repaying stability debt, but specific long-term signals are visible:
- **Native Streaming Support ([#2404](https://github.com/sipeed/picoclaw/issues/2404)):** Highly requested. Likely targeted for the next minor release as it aligns with the project's core "unopinionated proxy" philosophy.
- **MCP Context Enrichment ([#2696](https://github.com/sipeed/picoclaw/pull/2696)):** A stalled but conceptually important PR enabling per-request dynamic HTTP headers from channels to MCP servers. Signals an architectural investment in the MCP ecosystem for enterprise authentication flows.
- **Context Debugging Tooling ([#2985](https://github.com/sipeed/picoclaw/pull/2985)):** The active fix to the `/context` command shows the team is investing in operational transparency in response to user feedback about opaque context budgets.

## 7. User Feedback Summary
- **Pain Points:**
    - **Stability & Reliability:** The PID file bug ([#2720](https://github.com/sipeed/picoclaw/issues/2720)) erodes trust in gateway uptime for production or always-on agent setups.
    - **Agent Workflow Interruptions:** WebSocket users face broken agent loops due to dropped tool_calls ([#2958](https://github.com/sipeed/picoclaw/issues/2958)), a critical flaw for the project's target audience of AI agent operators.
    - **Configuration Friction:** Users are frustrated that the security module arbitrarily overwrites main config settings ([#2956](https://github.com/sipeed/picoclaw/pull/2956)).
- **Satisfaction:**
    - Quick patching of the Go CVE ([#2997](https://github.com/sipeed/picoclaw/pull/2997)) and the MQTT TLS fix ([#2899](https://github.com/sipeed/picoclaw/pull/2899)) demonstrate a strong security posture by the core team.
- **Unmet Needs:**
    - The loudest unmet need remains the lack of a simple streaming config option ([#2404](https://github.com/sipeed/picoclaw/issues/2404)), forcing users to build custom middleware or abandon the proxy for SSE use cases.

## 8. Backlog Watch
Several items critical to project health are stuck in stale status and require immediate maintainer attention:

- **[#2813](https://github.com/sipeed/picoclaw/pull/2813) / [#2955](https://github.com/sipeed/picoclaw/pull/2955) – PID Verification Fixes:** Multiple contributors have stepped up to fix the crash loop, but no maintainer has greenlit a merge or requested changes. This is the most time-sensitive item in the backlog.
- **[#2957](https://github.com/sipeed/picoclaw/pull/2957) – Tool Call Drop Fix:** Addresses a core regression for WebSocket agent workflows. Currently languishing without review input since May 27.
- **[#2956](https://github.com/sipeed/picoclaw/pull/2956) – Security Merge Bug:** Fix for config overwrites. Awaiting review.
- **[#2696](https://github.com/sipeed/picoclaw/pull/2696) – MCP Dynamic Headers:** Opened over a month ago (April 28). A significant feature for enterprise channel integration that has received zero maintainer feedback.
- **[#2954](https://github.com/sipeed/picoclaw/issues/2954) – 32-bit Android Support:** A platform compatibility issue that has not been acknowledged by the core team, potentially signaling a deprecated platform direction.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for June 4, 2026, based on the provided GitHub data.

---

## NanoClaw Project Digest — 2026-06-04

### 1. Today's Overview
NanoClaw experienced a wave of community-driven activity focused on hardening core subsystems and fixing regressions. Nine pull requests were submitted or updated in the last 24 hours, while no new releases were published. The activity level is high, but no PRs were merged, creating a growing review queue. The single new bug report filed was paired with an immediate fix from the reporter, demonstrating strong contributor engagement.

### 2. Releases
No new releases were published in the reporting period. The project currently has no upcoming release tags to report.

### 3. Project Progress
No pull requests or issues were closed or merged in the last 24 hours. The most significant proposed advancements awaiting review include:

- **Scheduling Reliability (PRs #2678, #2679):** Contributor yairixStudio submitted two major fixes to the scheduling subsystem. [#2678](https://github.com/nanocoai/nanoclaw/pull/2678) re-arms recurrence scheduling when a run fails permanently, preventing silent death of recurring tasks. [#2679](https://github.com/nanocoai/nanoclaw/pull/2679) adds a `notifyFailedTasks` sweep hook that surfaces permanently-failed tasks to the user instead of burying them in logs.
- **v2 Ecosystem Improvements (#2682):** ira-at-work submitted a fix for the `update-skills` workflow that adds a `package.json` version check, preventing v1-only skill branches from being offered as updates to v2 agents.
- **Container Runner Hardening:** shrwnsan submitted two patches: [#2676](https://github.com/nanocoai/nanoclaw/pull/2676) adds `NO_PROXY` bypass logic for local services, and [#2677](https://github.com/nanocoai/nanoclaw/pull/2677) introduces an automatic retry with diagnostics for failing pre-task scripts.
- **New Skill: QMD Hybrid Search (#2683):** shrwnsan also added a container skill for [QMD](https://github.com/tobi/qmd), providing a local BM25 + vector hybrid markdown search engine for the agent runtime.

### 4. Community Hot Topics
- **Encrypted Home Directory Boot Failure (Issue #2680):** While comment volume is low, this issue is driving significant action. A user reported a silent boot failure when using per-user encryption (ecryptfs, fscrypt) with systemd linger. The reporter immediately followed up with a fix PR [#2681](https://github.com/nanocoai/nanoclaw/pull/2681). This pairing indicates a high-priority pain point for users with advanced security setups.
- **Parent Agent Permissions (PR #2605):** This older PR from guyb1 regarding inheriting parent agent permissions via OneCLI was updated yesterday after a period of dormancy. It touches the core authorization model and suggests active, ongoing design discussion around multi-agent trust boundaries.

### 5. Bugs & Stability
- **[Severity: High] Silent Boot Failure (Issue #2680):** The service fails to start at boot on systems using per-user encrypted home directories (ecryptfs, fscrypt) even with `linger` enabled. A fix is proposed in PR [#2681](https://github.com/nanocoai/nanoclaw/pull/2681).
- **[Severity: High] Entire Slack Message Dropped (PR #2675):** Integrations using Vercel's Chat SDK drop entire messages when agent output exceeds Slack's 3000-character limit on `section` blocks. IamAdamJowett submitted a patch to cap the text length.
- **[Severity: Medium] Silently Hidden Failed Tasks (PR #2679):** A flaw in the scheduling logic caused permanently-failed scheduled tasks to be invisible to the user. A surface notification fix is proposed.
- **[Severity: Medium] Recurrence Chain Broken After Failure (PR #2678):** Recurring tasks that failed were not having their next occurrence scheduled, effectively killing the workflow. A fix is proposed.
- **[Severity: Low] v1/v2 Skill Ambiguity (PR #2682):** The update system could incorrectly offer incompatible v1-only skill branches to v2 agent configurations.

### 6. Feature Requests & Roadmap Signals
- **Local RAG Expansion (PR #2683):** The new QMD hybrid search skill signals growing investment in agent-tended local knowledge bases. By combining BM25 and vector search, NanoClaw is positioning itself as a more capable offline retrieval agent.
- **Hierarchical Agent Trust (PR #2605):** The ongoing work on parent agent permission inheritance suggests a roadmap shift toward a delegated trust model, enabling complex multi-agent setups where sub-agents automatically inherit scoped permissions via OneCLI.

### 7. User Feedback Summary
- **Security vs. Reliability Friction:** Users employing common per-user encryption tools (ecryptfs, fscrypt) are currently unable to run NanoClaw as a reliable systemd service at boot, creating friction between security hardening and agent availability.
- **Urgent Need for Observable Scheduling:** The scheduling subsystem historically failed silently. The community response (two high-quality PRs in one day) signals strong dissatisfaction with invisible task failures and a desire for agent-as-cron reliability.
- **Integration Pain Points:** The Slack block limit fix (PR #2675) reveals users are actively testing the output capacity limits of their integrations, encountering hard API walls that break agent workflows.

### 8. Backlog Watch
- **PR #2605 – Parent Agent Permissions:** Author: guyb1. Opened 2026-05-24, last updated 2026-06-03. This is a significant feature PR that has been open for 11 days without a merge. It touches a core architectural component (OneCLI authorization) and likely requires careful maintainer review. [Link to PR](https://github.com/nanocoai/nanoclaw/pull/2605)
- **Community Fix Pile-Up:** The project currently has 9 open PRs with zero merges. While the contribution velocity is excellent, the lack of any merges in the reporting window creates a risk of fix decay. The smaller, targeted fixes (e.g., #2676, #2677, #2682) could likely be processed quickly to clear the queue and maintain contributor momentum.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest — 2026-06-04**

---

### 1. Today’s Overview
Activity on the NullClaw repository was very low today. No new issues were opened, no releases were cut, and no pull requests were merged or closed. The only pulse was an update to the existing open PR #946, which advances work on agent prompt hygiene. With zero community interaction on issues and no new feature requests, development appears to be focused on polishing an existing pull request rather than responding to fresh feedback or shipping new functionality.

---

### 2. Releases
No new releases were published.

---

### 3. Project Progress
No pull requests were merged or closed today. The project’s delivered feature set and resolved bug count remain unchanged.

---

### 4. Community Hot Topics
- **[PR #946 — fix(agent): filter tools in system prompt text by tool_filter_groups](https://github.com/nullclaw/nullclaw/pull/946)**  
  *Author: vernonstinebaker | Updated: 2026-06-03 | No comments / reactions recorded*  

  **Summary of changes:** Introduces `filterToolsForPromptText`, which ensures only built-in tools and MCP tools from `always` filter groups are written into the text-based system prompt. Dynamic-group MCP tools are excluded from the text prompt but their schemas are still sent via native API tool-calling when turn keywords match. Also removes parasitic/unnecessary prompt text.

  **Analysis:** As the sole item of activity, this PR represents the community’s current center of gravity. The underlying need is a more disciplined system prompt: dynamic MCP tools were previously polluting the text prompt, which can reduce model accuracy or waste tokens. The contributor is pushing toward a clean separation between "always-available" tools and "keyword-triggered" tools, a pattern that suggests growing sophistication in NullClaw’s agent building blocks.

---

### 5. Bugs & Stability
- **New bugs reported today:** None.  
- **Active bug fix:**  
  **[PR #946](https://github.com/nullclaw/nullclaw/pull/946)** acts as a stability fix, even if it was not filed as a bug report. Prior to this change, dynamic-group MCP tools were likely being incorrectly serialized into the system prompt text, potentially causing the model to receive duplicate or out-of-context tool definitions. The severity is **medium-to-high** for any user relying on MCP dynamic groups, as the old behavior could silently degrade agent decision-making. No new regressions were introduced today.

---

### 6. Feature Requests & Roadmap Signals
- **New feature requests:** None filed today.

- **Roadmap signals:** The granularity introduced in PR #946 — the `tool_filter_groups` system — points toward a **flexible, user-configurable tool-to-prompt architecture**. A future version might expose these filter groups to end users, allowing them to decide which MCP tools are “always visible” to the model versus “called silently” via the API. This design fits naturally with a wider roadmap push toward **first-class MCP handling** and **prompt budget optimization**.

---

### 7. User Feedback Summary
- No direct user feedback (issues, comments, or reactions) was captured in today’s data snapshot.

- **Inferred pain points:** The existence of PR #946 strongly implies users/developers were experiencing issues where dynamic tools in the system prompt caused confusion — either the model misinterpreted them, or they consumed context space unnecessarily. The fix addresses an implicit demand for more reliable, predictable agent prompt assembly.

---

### 8. Backlog Watch
The repository currently has **no backlogged issues or pull requests**. The single open PR (#946) was updated within the last 24 hours and is actively moving forward. No items require immediate maintainer attention or are showing signs of neglect.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-04

## 1. Today's Overview
June 4th saw extremely high development velocity, with **26 issues** and **50 pull requests** updated in the past 24 hours, alongside the shipping of **patch release v0.29.1**. Activity is dominated by the maturation of the "Reborn" agent runtime, where Slack integration, security hardening, and trigger/automation systems are advancing toward production readiness. A notable pattern emerged today: the core development team systematically stress-tested the Reborn runtime and filed a batch of critical bugs (Issues #4424–#4429) while simultaneously opening fix pull requests—demonstrating strong parallel execution and a healthy engineering feedback loop.

---

## 2. Releases
**ironclaw-v0.29.1** was published today.

- **Added:** `temperature` parameter is now plumbed through the Responses API ([PR #3641](https://github.com/nearai/ironclaw/pull/3641)).
- **Fixed:** v1 history scope for channel conversations ([PR #4320](https://github.com/nearai/ironclaw/pull/4320)).
- **CI / Release:** Added WeCo to the release pipeline.
- No breaking changes or migration notes were documented.

---

## 3. Project Progress
26 pull requests were merged or closed today, advancing several major workstreams:

**Slack Integration (MVP)**
- The Reborn Lane 10 Slack ProductAdapter issue was closed ([#3857](https://github.com/nearai/ironclaw/issues/3857)).
- Slack host-beta routes are now fully wired into `reborn serve` ([PR #4418](https://github.com/nearai/ironclaw/pull/4418)).
- A Slack personal binding service ([PR #4422](https://github.com/nearai/ironclaw/pull/4422)) and a Slack actor→user resolver hook ([PR #4421](https://github.com/nearai/ironclaw/pull/4421)) were merged.

**Automations & Triggers**
- A read-only WebUI API for automations landed ([PR #4380](https://github.com/nearai/ironclaw/pull/4380)).
- The trusted trigger ingress path was type-sealed for security ([PR #4406](https://github.com/nearai/ironclaw/pull/4406)).
- A full-path integration test for the background trigger poller was added ([PR #4415](https://github.com/nearai/ironclaw/pull/4415)).

**Security & Auth**
- PKCE math was consolidated into `ironclaw_common` ([#4215](https://github.com/nearai/ironclaw/issues/4215)).
- HTTP credential material is now properly zeroized across request carriers ([#4222](https://github.com/nearai/ironclaw/issues/4222)).
- Capability surface and prompt-injection safety gating was hardened ([#4351](https://github.com/nearai/ironclaw/issues/4351)).
- Local dev runtime scope was fixed to bind correctly to the run actor ([PR #4412](https://github.com/nearai/ironclaw/pull/4412)).

**Stability Fixes**
- Context-overflow recovery emitted `ShrinkContext` but didn't shrink (closed: [#4310](https://github.com/nearai/ironclaw/issues/4310)).
- Compaction summary writes could outlive failed `BeforeModel` checkpoints (closed: [#4309](https://github.com/nearai/ironclaw/issues/4309)).
- WebUI live projection cursor resume was fixed ([PR #4417](https://github.com/nearai/ironclaw/pull/4417)).

---

## 4. Community Hot Topics
Active discussions are currently driven by the core development team's rigorous integration testing of the Reborn runtime.

- **Tool Selection Mismatch ([#4424](https://github.com/nearai/ironclaw/issues/4424), 3 comments):** *"builtin.spawn_subagent"* is advertised to the model in system-prompt text but absent from the structured `tools: [...]` array. This renders the tool uncallable by OpenAI-compatible models. The underlying need is strict parity between natural-language agent instructions and the structured API surface. A fix is already in PR [#4434](https://github.com/nearai/ironclaw/pull/4434).

- **Security Hardening ([#4376](https://github.com/nearai/ironclaw/issues/4376), 2 comments):** A follow-up discussion on further hardening HTTP credential carriers with non-clone types and DTO boundaries, indicating deep investment in platform-level security beyond the immediate zeroization fix.

---

## 5. Bugs & Stability
A significant bug blast targeting the Reborn runtime was filed today. The team has opened fix PRs for several items in parallel.

**Critical / High Severity**
- **[CRITICAL] `builtin.spawn_subagent` advertised but uncallable** ([#4424](https://github.com/nearai/ironclaw/issues/4424)). The model narrates about it but cannot invoke it. **Fix:** PR [#4434](https://github.com/nearai/ironclaw/pull/4434) open.
- **[HIGH] `builtin.http` is a context bomb** ([#4425](https://github.com/nearai/ironclaw/issues/4425)). Returns raw HTML verbatim (no HTML→text strip), observed injecting ~1.2 MB into context for a single fetch.
- **[HIGH] Capability surface profile ignored** ([#4426](https://github.com/nearai/ironclaw/issues/4426)). Parent loop tool surface is hardcoded to `AllowAll`; the `interactive_tools` profile ID is read but discarded, exposing lifecycle/mutation tools in every chat.

**Medium Severity**
- **[MEDIUM] `builtin.skill_list` unbounded** ([#4428](https://github.com/nearai/ironclaw/issues/4428)). Returns 14,612 bytes for 31 skills with no pagination or truncation.
- **[MEDIUM] Loop exit reason invisible** ([#4427](https://github.com/nearai/ironclaw/issues/4427)). `LoopFailureKind` is never traced, only persisted to DB. Operators cannot see why a loop ended.
- **[MEDIUM] Prompt bundle rebuilt from scratch per call** ([#4429](https://github.com/nearai/ironclaw/issues/4429)). Identity files and skill caches are cold every time; `ThreadBackedLoopContextPort` constructed fresh per model call.
- **[MEDIUM] `CompleteAfterFirstFire` trigger policy ignored** ([#4420](https://github.com/nearai/ironclaw/issues/4420)). Triggers re-fire on every scheduled occurrence forever despite the policy being stored on the record.

**Operational / CI**
- **[MEDIUM] Stale PID file prevents startup** ([#4400](https://github.com/nearai/ironclaw/issues/4400)). Production instances fail to start with "Another IronClaw instance is already running" and do not auto-recover.
- **[HIGH] Nightly E2E failure** ([#4108](https://github.com/nearai/ironclaw/issues/4108)). The Nightly E2E scheduled run continues to fail (reported June 3), affecting commit confidence.

---

## 6. Feature Requests & Roadmap Signals

- **Tool-count limit design ([#4407](https://github.com/nearai/ironclaw/issues/4407)):** A design issue was opened to manage model-visible capability selection when provider-level tool array limits are exceeded. Likely to be addressed in v0.30 to prevent regressions as the capability surface grows.
- **Default OAuth per provider ([#4382](https://github.com/nearai/ironclaw/issues/4382)):** A request for "set once, gate never re-fires" OAuth—once a user authenticates with a provider, subsequent calls should resolve silently to the default credential.
- **Canonical identity resolver ([#4381](https://github.com/nearai/ironclaw/issues/4381)):** A design for a persisted Reborn identity store for OAuth and external actor binding, fundamental for multi-tenant identity management.
- **Test parity requirement ([#4431](https://github.com/nearai/ironclaw/issues/4431)):** A regression test issue demanding every visible capability must be callable—a direct response to the #4424 bug.

**Predictions for v0.30.x:** The next minor release cycle will almost certainly focus on closing the #4424–#4429 bug cluster, shipping the Slack personal binding OAuth flows (PRs [#4423](https://github.com/nearai/ironclaw/pull/4423), [#4430](https://github.com/nearai/ironclaw/pull/4430)), and landing the Automations WebUI panel ([PR #4433](https://github.com/nearai/ironclaw/pull/4433)). The OpenAI API migration to Reborn ([#3283](https://github.com/nearai/ironclaw/issues/3283)) remains the largest strategic item on the horizon.

---

## 7. User Feedback Summary
Direct user pain points are currently being surfaced by the development team's own intensive integration testing, indicating the project is in a pre-stabilization cycle for the Reborn path rather than broad external adoption.

**Key Pain Points Surfaced Today:**
- Model confusion due to mismatches between advertised capabilities and structured tool definitions ([#4424](https://github.com/nearai/ironclaw/issues/4424)).
- Large, unconstrained tool outputs destroying context-window economics ([#4425](https://github.com/nearai/ironclaw/issues/4425)).
- Authorization gates re-firing for already-authenticated providers ([#4382](https://github.com/nearai/ironclaw/issues/4382)).
- The trigger system ignoring its own `CompleteAfterFirstFire` completion policy ([#4420](https://github.com/nearai/ironclaw/issues/4420)).

**Satisfaction Drivers:** The rapid cycle of bug identification and fix submission (e.g., #4424 opened and #4434 opened simultaneously, #4310 and #4309 closed within days) is a strong signal of a healthy, responsive engineering culture. The Slack integration advancing from design to merged wiring in a single day is notable.

---

## 8. Backlog Watch
Several high-impact items remain open and warrant monitoring:

- **[OpenAI API Migration Stalling?]** [#3283 — Migrate OpenAI-compatible APIs onto Reborn](https://github.com/nearai/ironclaw/issues/3283). This strategic feature has been open since May 6. It is likely intentionally blocked on core loop stabilization, but should be watched for progress signals.
- **[CI Health]** [#4108 — Nightly E2E Failure](https://github.com/nearai/ironclaw/issues/4108). An auto-reported CI failure since May 27. A persistent red CI is a drag on commit confidence despite the team's rapid development pace.
- **[Blocked Hard]** [#4432 — Python E2E Cron Trigger Scenario](https://github.com/nearai/ironclaw/issues/4432). Explicitly marked as blocked on Reborn production profile wiring. Filed today, so resolution depends on the Reborn profile pipeline.
- **[Technical Debt]** [#4389 — Auth/MCP Follow-up Items](https://github.com/nearai/ironclaw/issues/4389). Behavior-changing review items intentionally deferred from PR #4354 to avoid destabilizing the hosted MCP and OAuth behavior. Needs scheduling.
- **[Large PR Awaiting Merge]** [#3951 — Third-party Extension Hook Activation](https://github.com/nearai/ironclaw/pull/3951). An XL-sized PR open since May 23 that activates third-party extension hooks behind a default-OFF flag. Appears to be pending final review decisions.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-04

---

## 1. Today's Overview

LobsterAI is currently in an exceptionally high-velocity development phase, with 14 pull requests merged or closed in the last 24 hours alongside the release of version 2026.6.3. The development effort is heavily concentrated on the "Cowork" collaboration module (session sync, text snippets, conversation forking), MCP stability enhancements, and HTML share maturation. Community interaction via issues remains minimal, with only one active issue dominating the feedback channel, signaling a potential gap between user sentiment and the current feature push. Overall, the project demonstrates strong internal execution discipline, though the backlog of unanswered user concerns warrants immediate attention.

## 2. Releases

**Release 2026.6.3** (Released June 3, 2026) — [Reference PR](https://github.com/netease-youdao/LobsterAI/pull/2107)

| Category | Changes |
|---|---|
| **MCP** | Optimized `npx` MCP launch resolution; added first-response timing logs for diagnosability |
| **HTML Share** | General optimization of HTML share flow |
| **Cowork** | Artifact text selection improvements (detailed work landed in follow-up PRs) |

- **Breaking Changes:** None explicitly noted in release artifacts.
- **Migration Notes:**
  - Users relying on managed MCP installs should verify their Node toolchain (fix [#2100](https://github.com/netease-youdao/LobsterAI/pull/2100) improves path injection).
  - User-configured context window settings are now better preserved ([#2102](https://github.com/netease-youdao/LobsterAI/pull/2102)).
  - Remote MCP server URLs now undergo stricter validation ([#2103](https://github.com/netease-youdao/LobsterAI/pull/2103)); invalid configurations may need manual correction.

---

## 3. Project Progress

The 24-hour window saw the following major feature deliveries and improvements:

### 🚀 Cowork Module (Major Focus)
- **Text Snippets to Chat:** Users can now select text from Markdown/plain text artifact previews and add it directly to the current Cowork draft ([#2101](https://github.com/netease-youdao/LobsterAI/pull/2101), [#2098](https://github.com/netease-youdao/LobsterAI/pull/2098)).
- **Local Conversation Forking:** Forked conversations from assistant messages are now supported, with compacted context preservation for long sessions ([#2085](https://github.com/netease-youdao/LobsterAI/pull/2085)).
- **Channel Sync:** Improved session sync behavior for recreated channels; added `MessageForkIcon` component ([#2108](https://github.com/netease-youdao/LobsterAI/pull/2108)).
- **UI Polish:** Title bar close button added to search modal ([#2097](https://github.com/netease-youdao/LobsterAI/pull/2097)).

### ⌨️ Keyboard Shortcuts
- Complete overhaul with expanded actions and improved UX ([#2109](https://github.com/netease-youdao/LobsterAI/pull/2109)).

### 🌐 HTML Share
- Refined share dialog states (created, active, stopped); removed automatic copy behavior; added `html_share keyfrom` attribution ([#2099](https://github.com/netease-youdao/LobsterAI/pull/2099), [#2105](https://github.com/netease-youdao/LobsterAI/pull/2105)).

### 🤖 Model Support
- Added support for `mimo v2.5` models ([#2102](https://github.com/netease-youdao/LobsterAI/pull/2102)).

---

## 4. Community Hot Topics

The sole active community discussion is:

- **[Issue #2081 — "订阅" (Subscription)](https://github.com/netease-youdao/LobsterAI/issues/2081)**
  - **Author:** zjk648491625 | **Comments:** 2 | **Status:** Open
  - **Content:** A user reports the loss of 5,500 unused subscription credits at the end of the billing cycle, expressing severe frustration ("来搞笑的吧???" — *"Are you joking???"*).
  - **Analysis:** This issue reveals a critical disconnect between platform subscription policy (monthly credit expiration) and user expectations. The underlying needs are:
    - Clear, proactive warnings before credit expiration.
    - A rollover or grace-period mechanism for unused credits.
    - Better communication of terms within the product.
  - **Risk:** High. Unresolved subscription disputes can lead to churn and negative word-of-mouth. This issue has been open since June 1 with no visible staff response in the snapshot.

All other updated items are internal PRs or automated Dependabot updates with no community comments.

---

## 5. Bugs & Stability

Several regressions and stability issues were fixed in this cycle, ranked by severity:

### 🔴 Critical
- **MCP Session Timeout** ([#2104](https://github.com/netease-youdao/LobsterAI/pull/2104)): Session timeouts during gateway config reloads could bring down MCP workflows. **Fixed.**

### 🟠 High
- **Managed MCP Node Path Loss** ([#2100](https://github.com/netease-youdao/LobsterAI/pull/2100)): Managed MCP installs lost Node.js toolchain awareness, causing silent server drops. **Fixed** (includes fallback to raw stdio config).

### 🟡 Medium
- **Config Overwrite Regression** ([#2102](https://github.com/netease-youdao/LobsterAI/pull/2102)): User-configured context window sizes were being overwritten during updates. **Fixed.**
- **Invalid MCP URLs Accepted** ([#2103](https://github.com/netease-youdao/LobsterAI/pull/2103)): No validation existed for remote server URLs. **Fixed** with shared validation and localized error messages.

### 🟢 Low (UI/UX)
- **Popover & Hover Card Issues** ([#2106](https://github.com/netease-youdao/LobsterAI/pull/2106)): Model selector overflow, delayed skill popover close. **Fixed.**
- **HTML Share Copy Behavior** ([#2105](https://github.com/netease-youdao/LobsterAI/pull/2105), [#2099](https://github.com/netease-youdao/LobsterAI/pull/2099)): Improved copy formatting and dialog transitions.

---

## 6. Feature Requests & Roadmap Signals

### Explicit User Requests
- **Subscription Policy Reform** ([Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081)): The most urgent user-driven feature request. The team should consider adding credit rollover, a grace period, or in-app expiration countdowns.

### Roadmap Predictions (Next 1–2 Releases)

| Scope | Prediction |
|---|---|
| **Cowork** | Stabilization of forking/snippet features; potential introduction of real-time collaborative editing or merge workflows |
| **MCP Tooling** | Further hardening around managed installs, possibly official plugin market integration |
| **HTML Share / Artifacts** | Likely continued feature parity improvements and access control expansion |
| **Subscription UX** | High probability of a response or policy change given the intensity of Issue #2081 |

---

## 7. User Feedback Summary

The limited community interaction in this snapshot is strikingly polarized:

- **Dissatisfaction (High Severity):**
  - **Credit Expiration** ([Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081)): One user reports a strongly negative experience with the subscription system. The tone and content suggest a perceived lack of fairness or transparency.
- **Pain Points (Addressed Today):**
  - Silent MCP server failures (#2100).
  - Lost configuration settings (#2102).
  - Annoying UI popover/dropdown behaviors (#2106).
- **Satisfaction Signals:**
  - No explicit positive feedback was captured. The team's rapid response to bugs (14 PRs merged) implies strong internal quality management, but this is not externally visible as user praise.

---

## 8. Backlog Watch

Two significant items remain open for extended periods and require maintainer attention:

| Item | Age | Risk | Status |
|---|---|---|---|
| **[PR #1463](https://github.com/netease-youdao/LobsterAI/pull/1463) — `fix long modal titles`** | Open since April 4, 2026 (~60 days) | **Medium.** Labeled `[stale]` and `[codex]`. A straightforward UI regression fix that is at high risk of merge conflicts. | Needs review: merge or close. |
| **[PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — `chore(deps-dev): bump the electron group`** | Open since April 2, 2026 (~60 days) | **High.** Dependabot bump for Electron (40.2.1 → 42.3.1) and Electron-Builder. Two months of security patches and bug fixes are not integrated. | Needs conflict resolution and merge. |
| **[Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081) — `订阅`** | Open since June 1, 2026 (3 days) | **High (Community Relations).** Unanswered user complaint regarding financial policy. | Requires official response and/or policy adjustment. |

---

*Data snapshot: GitHub activity for `netease-youdao/LobsterAI`, last updated 2026-06-04.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-04

**Data Snapshot:** 14 Issues updated (5 open, 9 closed) | 4 open PRs | 2 new releases

---

## 1. Today's Overview

The Moltis project shows strong maintenance momentum today, with **nine issues closed** in the last 24 hours across bug fixes and feature implementations, while **no pull requests were merged** — indicating a likely consolidation phase before the next merge batch. Two new date-versioned releases (`20260602.05`, `20260603.01`) are live. The community is actively contributing code (four open PRs) but is encountering friction in containerized environments (Docker/Podman) and Telegram streaming UX. Overall, project health appears robust, with a rapid issue-resolution cadence and a healthy pipeline of community-driven enhancements.

---

## 2. Releases

**New versions available:**
- `20260603.01`
- `20260602.05`

The project uses date-based versioning (`YYYYMMDD.patch`). While explicit changelogs are not included in this data, the close temporal correlation between the `20260603.01` release and the batch of 9 closed issues strongly indicates these builds ship fixes and improvements for: Vault password handling, session title generation, MCP environment variable leaks, UI syntax highlighting, Docker `send_image`/`send_document` failures, web file attachments, granular skill management, model picker rendering, and built-in agent access to Moltis documentation. **No breaking changes or migration notes** have been communicated for these minor patches.

**Links:**
- [Latest Releases Page](https://github.com/moltis-org/moltis/releases)

---

## 3. Project Progress

**PR Merge Activity:** None today.

While the main branch saw no new merges in the last 24 hours, the closing of **9 diverse issues** signals that significant engineering work has been completed and implicitly released. This pause in merging may indicate internal QA, staging of pending work, or a day focused on issue triage and closing older threads.

**Pending PRs awaiting review/merge:**

| PR | Focus Area |
|---|---|
| [#1100](https://github.com/moltis-org/moltis/pull/1100) | Browser tool: shadow DOM piercing for snapshots |
| [#1099](https://github.com/moltis-org/moltis/pull/1099) | Telegram: separate streaming progress from final reply |
| [#1098](https://github.com/moltis-org/moltis/pull/1098) | Browser tool: tolerate `null` optional params (Gemma 4) |
| [#1093](https://github.com/moltis-org/moltis/pull/1093) | Channel activity log visibility settings |

All four open PRs are from community contributors, representing healthy external engagement.

---

## 4. Community Hot Topics

**1. [Agents Accessing Moltis Docs (Issue #1028)](https://github.com/moltis-org/moltis/issues/1028) — Closed**
*Comments: 3 | Reactions: 0*
The most-discussed item in the dataset. This feature request requested that the LLM agent have out-of-the-box access to Moltis's own documentation. Its closure today suggests this capability has shipped — a significant usability win for new users and an important step in making Moltis self-documenting for its agents.

**2. [Telegram Streaming Corruption (Issue #1097)](https://github.com/moltis-org/moltis/issues/1097) — Open**
*Comments: 1 | Reactions: 0*
A bug where Telegram's edit-in-place streaming mixes intermediate LLM output into the final reply. This was rapidly addressed by a community contributor, who submitted [PR #1099](https://github.com/moltis-org/moltis/pull/1099) on the same day. The swift collaboration here is a strong signal of an engaged contributor base.

**3. [New Channels Request (Issue #1101)](https://github.com/moltis-org/moltis/issues/1101) — Open**
*Comments: 0 | Reactions: 0*
Opened today by joelebw999 requesting SMS (`moltis-sms`) and LINE (`moltis-line`) integrations. Zero comments yet, but it points to a clear user desire for multi-channel expansion beyond the current web UI and Telegram focus.

---

## 5. Bugs & Stability

**Resolved in latest releases (closed today):**
- [[#1046]](https://github.com/moltis-org/moltis/issues/1046) Vault password lock loop (blocker)
- [[#1083]](https://github.com/moltis-org/moltis/issues/1083) Cannot enable/disable individual skills
- [[#1053]](https://github.com/moltis-org/moltis/issues/1053) Automatic session title generation broken
- [[#1054]](https://github.com/moltis-org/moltis/issues/1054) MCP server env vars exposed via `mcp_list` (security)
- [[#1052]](https://github.com/moltis-org/moltis/issues/1052) Model picker doesn't fit model version strings
- [[#1045]](https://github.com/moltis-org/moltis/issues/1045) No syntax highlighting in light mode
- [[#1037]](https://github.com/moltis-org/moltis/issues/1037) `send_image`/`send_document` fail in Docker

**Active Bugs (Open, ranked by severity):**

| Severity | Issue | Status |
|---|---|---|
| **Critical** | [#1096](https://github.com/moltis-org/moltis/issues/1096) — `Read`/`Write`/`Edit` tools broken in Docker | No maintainer response yet |
| **Critical** | [#1095](https://github.com/moltis-org/moltis/issues/1095) — Podman not working via Moltis | No maintainer response yet |
| **High** | [#1097](https://github.com/moltis-org/moltis/issues/1097) — Telegram streaming corruption | Fix PR [#1099](https://github.com/moltis-org/moltis/pull/1099) submitted |
| **Medium** | [#1094](https://github.com/moltis-org/moltis/issues/1094) — "De-Preferring Models" behavior | Awaiting triage / clarification |

The Docker and Podman issues are the most critical unaddressed items, directly blocking containerized deployments. The Telegram streaming issue has an active PR, reducing its risk window.

---

## 6. Feature Requests & Roadmap Signals

**Confirmed Upcoming Features (PRs Open):**
- **Browser Tool Enhancements** ([#1100](https://github.com/moltis-org/moltis/pull/1100)): Piercing open shadow roots for web component support (e.g., Salesforce). Critical for enterprise web automation.
- **Granular Activity Log Settings** ([#1093](https://github.com/moltis-org/moltis/pull/1093)): Per-account/per-channel/per-user visibility options (`all`, `errors_only`, `off`).
- **Telegram UX Refinement** ([#1099](https://github.com/moltis-org/moltis/pull/1099)): Separation of streaming progress from final replies.

**Community Request Signals:**
- **New Channels** ([#1101](https://github.com/moltis-org/moltis/issues/1101)): SMS and LINE integration request. If the Telegram channel is successful, expansion to SMS and LINE is a logical roadmap item for the next major feature cycle.
- **Model Compatibility** ([#1098](https://github.com/moltis-org/moltis/pull/1098)): A fix for Gemma 4's optional parameter handling suggests active work on broadening local model support.

**Items shipped this cycle (closed):**
- Agent OOTB access to Moltis docs ([#1028](https://github.com/moltis-org/moltis/issues/1028))
- Arbitrary inbound file attachments in Web UI ([#1036](https://github.com/moltis-org/moltis/issues/1036))

---

## 7. User Feedback Summary

**Satisfaction Signals:**
- The project's ability to close 9 issues rapidly (including a security leak and a blocking vault bug) demonstrates strong operational responsiveness.
- Community members are proactively submitting pull requests (#1099, #1100, #1098, #1093), indicating a healthy, engaged developer ecosystem.

**Pain Points:**
- **Docker/Podman Reliability:** This is the most vocal pain point in the current open issue set. Users report broken core tools (`Read`/`Write`/`Edit`) and outright incompatibility. The previous Docker bug ([#1037](https://github.com/moltis-org/moltis/issues/1037)) being closed implies a prior fix, making the *new* Docker issues ([#1096](https://github.com/moltis-org/moltis/issues/1096)) a potential regression or environment-specific case.
- **Telegram Experience:** Users relying on Telegram as a primary channel are encountering confusing mixed output ([#1097](https://github.com/moltis-org/moltis/issues/1097)).
- **Model Management:** The "De-Preferring Models" issue ([#1094](https://github.com/moltis-org/moltis/issues/1094)) and the fixed model picker rendering ([#1052](https://github.com/moltis-org/moltis/issues/1052)) suggest model selection UX is a persistent user friction point.

**Use Cases:**
- Containerized/Microservice deployment (Docker/Podman) is a primary deployment pattern.
- Multi-modal communication (Web UI, Telegram, requested SMS/LINE).
- Browser automation for complex web apps (shadow DOM support).

---

## 8. Backlog Watch

The following items are the most vulnerable in the current queue, requiring timely maintainer attention:

| Item | Age | Risk |
|---|---|---|
| [#1096](https://github.com/moltis-org/moltis/issues/1096) — Docker tools broken | ~24h | No maintainer response yet. High-priority regression for container users. |
| [#1095](https://github.com/moltis-org/moltis/issues/1095) — Podman broken | ~24h | No maintainer response yet. Broad deployment blocker. |
| [#1094](https://github.com/moltis-org/moltis/issues/1094) — De-Preferring Models | ~24h | Vague title, no response; needs triage to prevent lingering. |
| [#1099](https://github.com/moltis-org/moltis/pull/1099) — Telegram streaming fix | ~24h | Community PR; delayed review risks contributor burnout. |
| [#1100](https://github.com/moltis-org/moltis/pull/1100) — Shadow DOM fix | ~24h | Community PR; valuable enterprise feature. |
| [#1098](https://github.com/moltis-org/moltis/pull/1098) — Null params fix | ~48h | Community PR; improves local model support (Gemma 4). |

**Recommendation:** Prioritize triage on [#1096](https://github.com/moltis-org/moltis/issues/1096) and [#1095](https://github.com/moltis-org/moltis/issues/1095) (Docker/Podman blockers), and provide review feedback on the four open community PRs to sustain the current high level of external contribution.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw / QwenPaw Project Digest: 2026-06-04

**Repository:** [agentscope-ai/QwenPaw](https://github.com/agentscope-ai/QwenPaw)

---

## Today's Overview

Activity surged to 43 updated issues and 49 updated pull requests in the past 24 hours, reflecting a highly engaged community and a responsive core team. With 22 open and 21 closed issues, triage is keeping pace with inflow. The 28 open pull requests against 21 merged/closed indicate active feature incubation and quick turnaround on high-severity bugs. No formal release was cut today; the project remains in a stabilization phase following the v1.1.10 release, with concentrated effort on ChromaDB memory bloat, context compaction reliability, channel message routing integrity, and desktop plugin loader readiness.

---

## Releases

No new releases published today. The project is in a hardening phase, processing feedback from the v1.1.10 (Tauri Desktop) release.

---

## Project Progress

**Context Compaction (Stability Hotspot)**
- **PR #4933** (merged): Fixed `str` object `AttributeError` crash when media block `source` fields are plain URL strings instead of dicts. Resolves spikes in compaction failure reports (#4448, #4811, #4924).
- **PR #4935** (merged): Updated `reme-ai` dependency to v0.3.1.10, addressing file watcher restart race conditions where a stale `stop_event` was not correctly reset.
- **PR #4936** (open): Fixes Dream agent context corruption where `memory_manager` cached stale workspace paths, causing writes to wrong agent directories.

**Channels & Messaging**
- **PR #4837** / **PR #4945** (merged/active): Expanded P0 contract test coverage (+55 cases). Established a formal channel testing baseline via PR #1837.
- **PR #4821** (merged) & **PR #4737** (merged): Feishu gained group session sharing control; Telegram added interactive `tool_guard` approval via inline keyboards.
- **PR #4925** & **PR #4932** (both open): Fixed critical message routing bugs — ACL sender IDs were dropped during batch-native-payload merges, and messages from different users could be combined in queue routing.

**Skill Ecosystem**
- **PR #4941** (merged): Increased the maximum skill package download size (5 MB → higher bound), resolving the error in #4928.
- **PR #4794** (under review): Added plugin uninstall hooks, validator import fixes, and a skill provider API extension.

**ACP & Tools**
- **PR #4949** (open): Extended the Agent Client Protocol server to expose commands, tool parameters, agent/model metadata, and file links for terminal UI clients.
- **PR #4944** (open): Introduces CDP timeout parameter and browser-specific profile isolation (`user_data_edge`, `user_data_chrome`) to fix cross-browser switching crashes (#4919).

**Documentation & Roadmap**
- **PR #4942** (merged): The official roadmap was updated today, signaling active planning for the next development cycle.

---

## Community Hot Topics

1.  **Self-Evolution (#3470, #3516)**
    *Sites:* [Issue #3470](https://github.com/agentscope-ai/QwenPaw/issues/3470) (Closed, 6 💬), [Issue #3516](https://github.com/agentscope-ai/QwenPaw/issues/3516) (Closed, 4 💬)
    Two parallel threads requested Hermes Agent-style self-evolution capabilities. While closed, the volume signals strong community desire for meta-cognition. The team likely logged this for roadmap consideration, per the roadmap update today.

2.  **Browser Tool Instability (#4919)**
    *Site:* [Issue #4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) (Open, 6 💬)
    Users reported complete failure of `browser_use` tool startup on Windows 10 (Chrome/Edge), failing through managed CDP and Playwright. The community discovered a `playwright-cli` workaround. A targeted fix landed today in PR #4944.

3.  **Memory System Maturation (#3905, #4640, #3995)**
    *Sites:* [#3905](https://github.com/agentscope-ai/QwenPaw/issues/3905) (Open, 5 💬), [#4640](https://github.com/agentscope-ai/QwenPaw/issues/4640) (Open, 2 💬), [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995) (Open, 2 💬)
    The Dream agent memory pipeline is under scrutiny. Issue #3905 details empty `MEMORY.md` after dreaming. Feature requests for automatic session-end archiving (#4640) and memory file lifecycle management (#3995) indicate users want the memory system to be more autonomous than its current passive file-based design.

---

## Bugs & Stability

### Critical
| Issue | Summary | Severity |
|---|---|---|
| [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | ChromaDB Rust binding segfault (`SIGSEGV`) kills the entire process on Linux. 45+ crashes in one session. | **Critical** — No fix PR yet. |
| [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | ChromaDB vector index bloats to 37GB over 3 months, making `memory_search` crash every 30 min. | **Critical** — Root cause identified (`link_lists`). Requires architectural change. |
| [#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889) | Tauri Desktop Plugin Loader never initializes; all plugin installs fail. | **High** — Blocking desktop extension ecosystem. PR #4900 is open. |
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | `browser_use` CDP timeout + dual-browser crash on Windows. | **High** — Fix in review (PR #4944). |

### High/Medium
| Issue | Summary | Status |
|---|---|---|
| [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | Context compaction fails with `str` `has no attribute 'get'` | **Fixed** in PR #4933 |
| [#4448](https://github.com/agentscope-ai/QwenPaw/issues/4448) | Frequent "missing ## header" context compaction failures | **Fixed** in PR #4933 / #4935 |
| [#4932](https://github.com/agentscope-ai/QwenPaw/issues/4932) | Cross-user message merging in channel queue routing (group chat context poisoning) | Fix in PR #4932 (open) |
| [#4925](https://github.com/agentscope-ai/QwenPaw/issues/4925) | ACL sender ID dropped during batch payload merge (whitelist bypass) | Fix in PR #4925 (open) |
| [#4916](https://github.com/agentscope-ai/QwenPaw/issues/4916) | Backup fails with `PermissionError` on browser cache files (Windows) | Open |
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | `/compact` command ignores custom `max_input_length` | Open |
| [#4781](https://github.com/agentscope-ai/QwenPaw/issues/4781) | `tool_result_pruning` fails to contain single oversized shell output | Open |
| [#4710](https://github.com/agentscope-ai/QwenPaw/issues/4710) | Vector store timestamp inconsistency (naive vs UTC datetime) | Open |

---

## Feature Requests & Roadmap Signals

- **Memory Self-Management (#3470, #4640, #3995):** The strongest signal. Users want the memory system to evolve from passive file storage to active reasoning—auto-summarization, conflict detection, and Hermes-style meta-learning. Likely a target for v1.2.0.
- **Context Engine Overhaul (#4551, #4463, #3801):** Users are hitting the limits of sliding-window compaction. Demand is growing for DAG-based lossless summarization, adaptive context limits that read from model config, and provider-cached prompt token estimation.
- **Plugin Ecosystem Growth (#4794, #4171, #4889):** The community is building custom plugins (e.g., `memory-distill`). The immediate blocker is the Tauri Plugin Loader (#4889). If fixed, ecosystem contributions are poised to accelerate.
- **UI/UX Polish (#4920, #4001, #4637):** Users repeatedly request non-blocking message deletion and customizable slash command menus. PR #4637 (custom shortcut menu) is open and under review.
- **Code Mode & Workspace (#4876):** Users request the ability to open projects from non-C drives in code mode—a baseline quality-of-life request for developer users.

---

## User Feedback Summary

**Satisfaction:** The core value proposition—multi-channel agents, autonomous dreaming, and file-based memory—is strongly appreciated. The community is actively contributing plugins and fixes (e.g., `memory-distill`, channel-specific tool guards), demonstrating deep engagement.

**Frustration (High Signal):**
1. **Context Compaction Fragility:** Widely reported as "frequent breaking." Users describe it as an active pain point in long-running development tasks. The cluster of fixed bugs today (#4924, #4448, #4811) shows the team is sprinting on this.
2. **Vector Store Instability:** Two separate critical ChromaDB issues (#3854, #4795) erode trust in long-term memory stability. Users 3+ months in are hitting bloat and crashes.
3. **Desktop Plugin Lockout (#4889):** Tauri users are effectively blocked from the skill/plugin ecosystem, limiting the reach of the v1.1.10 release.
4. **Manual Context Configuration (#3801, #4937):** Users are frustrated that context limits must be manually configured and are not auto-detected from model provider specs.

---

## Backlog Watch

*Issues/PRs requiring maintainer attention:*

1.  **[#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) — ChromaDB Rust segfault (Critical)**
    *Status:* Open for >1 month. No fix PR. The severity (process kill) makes this the top-priority unresolved bug.

2.  **[#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) — Vector stone bloat to 37GB (Critical)**
    *Status:* Open 6 days. Root cause identified. Needs a cleanup mechanism or migration path. Affects long-term user trust.

3.  **[#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889) — Plugin Loader Tauri (High)**
    *Status:* PR #4900 open for 2 days. Blocking entire desktop extension workflow. Community eagerly awaiting a merge.

4.  **[#4171](https://github.com/agentscope-ai/QwenPaw/issues/4171) — `memory-distill` Plugin (Under Review)**
    *Status:* Open 25+ days. A high-quality community contribution. Extended review risks discouraging external contributors.

5.  **[#4781](https://github.com/agentscope-ai/QwenPaw/issues/4781) — `tool_result_pruning` Bypass (Medium)**
    *Status:* Open 7 days. Represents an OOM / runaway context risk for agents executing shell commands. No fix PR yet.

6.  **[#4640](https://github.com/agentscope-ai/QwenPaw/issues/4640) — Auto Session Summarization (Medium)**
    *Status:* Open 12 days. RFC with high community alignment. A decision or design sketch would advance the memory roadmap.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

Here is the ZeptoClaw project digest for June 4, 2026.

---

## ZeptoClaw Project Digest – 2026-06-04

### 1. Today’s Overview
ZeptoClaw’s development activity in the last 24 hours was entirely automated. No new issues were opened, no pull requests were merged, and no releases were cut. The only activity was the submission of 16 Dependabot pull requests updating dependencies across the Rust backend, JavaScript frontends, Docker environment, and CI/CD pipeline. This signals a quiet maintenance window for the project, possibly reflecting maintainer focus on review, testing, or internal work ahead of a larger push. Overall project health appears stable, with an exceptionally clean issue tracker and timely dependency management.

### 2. Releases
No new versions were published today.

### 3. Project Progress
No human-authored features, fixes, or refactors were merged or closed today. The 16 open pull requests are all automated `chore(deps): bump` updates queued for review and have no influence on the project’s feature set until merged.

### 4. Community Hot Topics
There were no issues or human-authored pull requests with comments, reactions, or direct community discussion in the reporting period. The low engagement level is expected given the automated nature of the day’s activity. No underlying community needs can be extracted from the tracker data beyond a general satisfaction with the project’s current maintenance cadence.

### 5. Bugs & Stability
While no new bugs were filed against the ZeptoClaw repository today, several upstream Dependabot bumps address stability and correctness issues that directly affect security and runtime reliability:

- **serde_json (PR #627)** [qhkm/zeptoclaw PR #627]: Bumps to v1.0.150, which rejects non-string enum keys. This prevents a class of silent data-corruption bugs in JSON deserialization.
- **tokio (PR #623)** [qhkm/zeptoclaw PR #623]: Updates from 1.52.1 to 1.52.3. Contains several general runtime fixes; recommended priority merge given tokio’s role as the core async runtime.
- **rpassword (PR #625)** [qhkm/zeptoclaw PR #625]: Moves to v7.5.2 with a fix for Unicode parsing in secure input handling. Relevant for any CLI tools or credential prompts in the stack.
- **scraper (PR #620)** [qhkm/zeptoclaw PR #620]: Jump from 0.26.0 to 0.27.0 (semver major). May contain breaking API changes or significant behavioral fixes to HTML parsing.
- **Frontend patches (PRs #615–619)** [qhkm/zeptoclaw PR #615], [#619](qhkm/zeptoclaw PR #619), [#616](qhkm/zeptoclaw PR #616): Astro, React, and TailwindCSS all receive patch/minor bumps fixing upstream bugs and build stability.

**Verdict:** No regressions reported. The project is proactively addressing bugs through dependency hygiene. The `tokio` and `serde_json` bumps are the highest priority for stability.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were submitted today. The strongest roadmap signals come from the automated dependency landscape:

- **Rust 1.96 (PR #613)** [qhkm/zeptoclaw PR #613]: Updating the Docker base image to Rust 1.96-slim-trixie ensures the project builds against the latest stable compiler with its optimizations and library improvements.
- **TailwindCSS v4.3.0 (PR #619)** [qhkm/zeptoclaw PR #619]: Adoption of a major new minor version of the CSS framework suggests the team is keen on staying current with utility-first CSS enhancements.
- **Astro 6.3.7 (PRs #614, #615)** [qhkm/zeptoclaw PR #614]: Keeping landing pages on the latest Astro patch points to content-driven performance and rendering improvements.

These bumps collectively indicate a roadmap that values modern tooling and low maintenance overhead for future feature development.

### 7. User Feedback Summary
No direct user feedback or pain points were captured in the project tracker during this period. The absence of filed issues suggests a period of stable operation for end users.

### 8. Backlog Watch
The project maintains an exceptionally clean issue backlog with **zero open issues**. The primary backlog consists of the 16 open Dependabot PRs, which require maintainer approval and merging to stay current. The following PRs warrant the closest attention due to version-significant changes:

- **PR #613 (Rust 1.95 → 1.96)** [qhkm/zeptoclaw PR #613]: Docker base image upgrade.
- **PR #620 (scraper 0.26.0 → 0.27.0)** [qhkm/zeptoclaw PR #620]: Major version bump that may require code adjustments.
- **PR #621 (@types/node 25.3.5 → 25.9.1)** [qhkm/zeptoclaw PR #621]: Large jump in Node type definitions that could expose new TS errors in `/panel`.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-04

---

## 1. Today’s Overview

ZeroClaw's development velocity remains high, with **29 Issues** (26 active) and **50 Pull Requests** (46 open) updated in the past 24 hours. Activity is concentrated around three pillars: a major security architecture overhaul targeting **v0.9.0** (pluggable security providers, OIDC, `forbid(unsafe_code)`), stabilization and feature parity for the new **Terminal User Interface** (`zerocode` TUI), and targeted bug fixes for the Web Dashboard and daemon runtime. No formal releases were cut today, but the **v0.8.0 release queue** ([#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) and **v0.8.1 integration queue** ([#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) are actively processing PRs, indicating a sustained push toward stable-tier promotions.

---

## 2. Releases

**No new releases today.** The project is in an active inter-release cycle preparing v0.8.0 (config/tool-call-parser stable-tier promotion, breaking-change cleanup) and v0.8.1 (additive channels, providers, tools).

---

## 3. Project Progress

The project closed 4 PRs today and resolved several key Issues, pushing forward critical infrastructure:

- **Persistent RPC Sessions:** PR [#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182) (merged) removed the 10-minute idle TTL from `SessionStore`, resolving the critical S1 bug [#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179). RPC sessions now persist until explicitly closed, killed, or daemon exit (tmux-style).
- **Session Branching:** Issues [#7168](https://github.com/zeroclaw-labs/zeroclaw/issues/7168) and [#7167](https://github.com/zeroclaw-labs/zeroclaw/issues/7167) were closed, consolidating the "fork conversation at any message point" feature concept. This signals an accepted design path for enabling "what-if" exploration without losing the original thread.
- **TUI Distribution:** Issue [#6822](https://github.com/zeroclaw-labs/zeroclaw/issues/6822) (closed) ensures the `zerocode` TUI binary will ship in the release build matrix and package managers alongside the main `zeroclaw` daemon.
- **Small Clarity Improvements:** Multiple PRs were opened today by maintainer `chengzhichao-xydt` replacing bare `.unwrap()` calls with diagnostic `.expect()` messages across channels, runtime, and skills crates ([#7076](https://github.com/zeroclaw-labs/zeroclaw/pull/7076), [#7102](https://github.com/zeroclaw-labs/zeroclaw/pull/7102), [#7078](https://github.com/zeroclaw-labs/zeroclaw/pull/7078), [#7071](https://github.com/zeroclaw-labs/zeroclaw/pull/7071)) — a consistent code-health push.

---

## 4. Community Hot Topics

Discussion is focused on architectural security changes and a quickly-resolved workflow blocker:

- **Pluggable Security & Authentication (Low Comment Count, High Impact):**
  - **[Issue #7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142)** — "Expose the security enforcement layer as a pluggable provider interface" (3 comments, 0 reactions). This v0.9.0 tracking issue outlines an umbrella trait for enforcement, reporting, and incident response.
  - **[Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)** — "OIDC Authentication Provider support for RPC/WSS transport" (3 comments, 0 reactions). A companion tracking issue specifying the pluggable auth-provider work.
  - *Analysis:* These are the highest-commented issues today. While comment counts are modest, the scope is large: they represent a fundamental architectural shift. The community is closely watching these blueprints for v0.9.0.

- **Session Lifecycle Management:**
  - **[Issue #7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179)** (S1: Idle RPC sessions reaped) was reported and **resolved within 24 hours** by PR [#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182). The rapid turnaround demonstrates strong maintainer responsiveness to workflow-blocking bugs.

- **Third-Party Provider Integration:**
  - **[PR #7136](https://github.com/zeroclaw-labs/zeroclaw/pull/7136)** — "Add Kilo AI Gateway as first-class model provider" signals growing community interest in OpenAI-compatible gateway providers, likely driven by cost-routing and regional access needs.

---

## 5. Bugs & Stability

**S1 – Workflow Blocked**
- **[#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179)** — ZeroClaw reaps idle RPC sessions at 10 minutes. **Resolved by [#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182).**
- **[#7173](https://github.com/zeroclaw-labs/zeroclaw/issues/7173)** — Quickstart webhook channel config does not offer port selection, causing a missing field `port` error. **Fix proposed in [#7193](https://github.com/zeroclaw-labs/zeroclaw/pull/7193)** (defaults port to 8090).

**S2 – Degraded Behavior**
- **[#7151](https://github.com/zeroclaw-labs/zeroclaw/issues/7151)** — Observability `tool_call` telemetry leaks onto the chat WebSocket, rendering permanent "unknown" tool cards. Root cause is a shared `broadcast::Sender`.
- **[#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126)** — Web UI "Clear all" wipes frontend messages only; backend session history persists.
- **[#7133](https://github.com/zeroclaw-labs/zeroclaw/issues/7133)** — Path-policy false-positive on `~` tokens in quoted/heredoc command data (sandbox module).
- **[#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143)** — Slack-connected coding agent runs near-duplicate shell discovery commands until `max_tool_iterations` is exhausted.

**S3 – Minor Issues**
- **[#6702](https://github.com/zeroclaw-labs/zeroclaw/issues/6702)** (21 days old) — Dashboard assistant bubble accumulates blank lines for each tool-call card.
- **[#7157](https://github.com/zeroclaw-labs/zeroclaw/issues/7157)** — Timestamp rendered inside message bubble instead of as separate metadata.
- **[#7156](https://github.com/zeroclaw-labs/zeroclaw/issues/7156)** — Reload banner shows persistent `gateway.paired_tokens (secret)` drift that never clears.
- **[#7139](https://github.com/zeroclaw-labs/zeroclaw/issues/7139)** — Missing i18n translation keys for chat toolbar buttons (compact, tool activity, clear, stop).
- **[#7128](https://github.com/zeroclaw-labs/zeroclaw/issues/7128)** — Stale `zeroclaw onboard` references persist in docs and tooling after deprecation.

---

## 6. Feature Requests & Roadmap Signals

Several user-requested features point toward the immediate roadmap:

- **High-Risk Shell Confirmation Tier ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)):** A request for a middle tier between allow/deny — "allowed to run, but requires manual confirmation." Mirrors Claude Code's pattern policy. **Likely for v0.8.x or v0.9.0** given the current security push.
- **Granular Sandbox Policy RFC ([#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)):** Config-driven control over filesystem and network restrictions. Tagged `needs-maintainer-review`. A decision here would unlock significant sandbox work.
- **Machine-Readable API Spec ([#7131](https://github.com/zeroclaw-labs/zeroclaw/issues/7131)):** Publish the daemon JSON-RPC surface as a versioned OpenRPC document. Signals platform/ecosystem thinking.
- **Web Chat Feature Parity ([#7138](https://github.com/zeroclaw-labs/zeroclaw/issues/7138), [#7137](https://github.com/zeroclaw-labs/zeroclaw/issues/7137)):** File upload/path selection UI and slash commands (`/clear`, `/help`, `/new`) for the gateway web chat. These indicate the web UI is emerging as a primary interaction surface alongside the TUI.
- **Typed Config Deletion ([#7175](https://github.com/zeroclaw-labs/zeroclaw/issues/7175)):** Delete-with-cascade for aliased config entries (providers, agents, channels). The config model is maturing enough to need safe deletion workflows.
- **TUI Outbound Message Queue ([PR #7190](https://github.com/zeroclaw-labs/zeroclaw/pull/7190)):** Replaces hard input blocking during a turn with a queued submission system. A clear UX parity goal with the web dashboard.

---

## 7. User Feedback Summary

- **Positive Sentiment (Performance):** User `sbenedetto` ([#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143)) explicitly praised ZeroClaw's resource utilization: *"It is great to see a Rust-based agent runtime that is much lighter on resources than many other agent systems we have tried."* This is a key differentiator for the project.
- **Pain Point – Agent Loop Control:** The same user (#7143) reported their Slack-connected coding agent exhausts `max_tool_iterations` with near-duplicate shell commands. This suggests the tool-use loop logic needs better deduplication or convergence detection.
- **Pain Point – Documentation & Onboarding:** [#7173](https://github.com/zeroclaw-labs/zeroclaw/issues/7173) (missing port field) and [#7128](https://github.com/zeroclaw-labs/zeroclaw/issues/7128) (stale `zeroclaw onboard` references) show that documentation drift and configuration gaps directly block user workflows during setup.
- **Demand for Advanced Interaction Models:** Requests for session branching ([#7168](https://github.com/zeroclaw-labs/zeroclaw/issues/7168), [#7167](https://github.com/zeroclaw-labs/zeroclaw/issues/7167)) and high-risk command confirmation ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)) show users want ZeroClaw to compete with Claude Code and Copilot on conversational safety and exploration.
- **i18n Community Waiting:** [#7139](https://github.com/zeroclaw-labs/zeroclaw/issues/7139) (missing translation keys) and [#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) (move translations to submodule) indicate a non-English userbase actively contributing to localization but hitting structural blockers.

---

## 8. Backlog Watch

- **[#6996 — RFC: Granular Sandbox Policy](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)** (Opened May 28, tagged `needs-maintainer-review`). This proposes a major architectural change to the sandbox subsystem (filesystem and network restrictions). The absence of maintainer direction 7 days in is a blocker for any implementation PRs.
- **[#6702 — Dashboard Bubble Blank Lines](https://github.com/zeroclaw-labs/zeroclaw/issues/6702)** (Opened May 16, 21 days old). A minor but persistently visible UI regression. With the web UI and TUI receiving intense focus, this cosmetic bug should be prioritized to maintain quality perception.
- **[#6826 / #6825 — TUI Trackers](https://github.com/zeroclaw-labs/zeroclaw/issues/6826)** (Opened May 21). These large umbrella issues span `zerocode` development and UX. While actively being progressed ([PR #7190](https://github.com/zeroclaw-labs/zeroclaw/pull/7190)), they cover dozens of sub-tasks and will require ongoing grooming to prevent scope creep.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*