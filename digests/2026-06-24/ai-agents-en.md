# OpenClaw Ecosystem Digest 2026-06-24

> Issues: 190 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-24 02:54 UTC

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

# OpenClaw Project Digest | 2026-06-24

## Today's Overview

The OpenClaw project is in a period of intense stabilization and regression hunting following the recent `2026.6.x` release train. A remarkable **190 issues** and **500 pull requests** were updated in the last 24 hours, with **140 issues** and **460 PRs** remaining actively open. No new release was cut today, indicating that maintainer focus is squarely on processing the high-volume bug reports and advancing the deep backlog of open patches. The core themes of the day are state management correctness (compaction, locks, session migration), provider-specific integration fixes (Anthropic, DeepSeek, Ollama, Matrix, Telegram), and the early scaffolding for a hosted plugin marketplace.

---

## Releases

**No new releases were published today.** The current landscape spans versions `2026.5.x` -> `2026.6.1` -> `2026.6.9`, with `2026.6.10-alpha.2` also referenced in bug reports, confirming the team is actively iterating on a stabilization release.

---

## Project Progress

**40 PRs were closed or merged today**, representing significant forward momentum across the codebase. Key completed work includes:

**State & Migration**
- [`#95631`](https://github.com/openclaw/openclaw/pull/95631) (P1): Memory store relocation fix — addresses a silent breaking migration in `2026.6.9` that forced full re-embedding of memory indexes.
- [`#95885`](https://github.com/openclaw/openclaw/pull/95885) (P2): Prevents repeated byte-triggered compactions by recording retry state on `SessionEntry`.
- [`#95305`](https://github.com/openclaw/openclaw/pull/95305) (P2): Stabilizes prompt cache prefix stability by fixing historical tool-result re-truncation.

**Platform & Provider Stability**
- [`#96261`](https://github.com/openclaw/openclaw/pull/96261) (XS): Bounds OpenAI-compatible image API response reads to prevent unbounded buffering.
- [`#96210`](https://github.com/openclaw/openclaw/pull/96210) (P1): Fixes Matrix SAS verification stalling when Element sends an `m.key.verification.accept` missing the `method` field.
- [`#96260`](https://github.com/openclaw/openclaw/pull/96260): Ensures embedded agent runs properly fall back on upstream provider errors.
- [`#94949`](https://github.com/openclaw/openclaw/pull/94949) (P2): Routes `isPortBusy` through the multi-endpoint `checkPortInUse` probe to catch IPv4-only port occupants.

**Tooling, CLI & Security**
- [`#96252`](https://github.com/openclaw/openclaw/pull/96252): Fixes TUI to properly handle live session message updates (closes [#38829](https://github.com/openclaw/openclaw/issues/38829)).
- [`#96216`](https://github.com/openclaw/openclaw/pull/96216): Hardens strict inline-eval approval detection to block interpreter bypasses.
- [`#96247`](https://github.com/openclaw/openclaw/pull/96247): Prevents outbound queue entry replay loops on Telegram reconnect by properly advancing state on mid-batch failure.
- [`#94562`](https://github.com/openclaw/openclaw/pull/94562) (P2): Hides archived Workboard cards by default in CLI output.

**Resolved Community Bug Reports**
- [`#90991`](https://github.com/openclaw/openclaw/pull/90991) (P1): Cron scheduled trigger global runtime state contamination — **CLOSED**.
- [`#90404`](https://github.com/openclaw/openclaw/pull/90404) (P1): acpx `TypeError: Cannot use in operator to search for "method" in 1` — **CLOSED**.
- [`#93465`](https://github.com/openclaw/openclaw/pull/93465) (P1): Windows embedded ACPX runtime spawn EINVAL — **CLOSED**.
- [`#76729`](https://github.com/openclaw/openclaw/pull/76729) (P1): Feishu replies disappearing after compaction — **CLOSED**.
- [`#92273`](https://github.com/openclaw/openclaw/pull/92273) (P1): Tool Search mode breaking pre-compaction memory flush — **CLOSED**.
- [`#96118`](https://github.com/openclaw/openclaw/pull/96118) (P2): [6.9 Regression] Dreaming runs but memory never promotes — **CLOSED**.

---

## Community Hot Topics

### Most Active Issues

- **[#88838](https://github.com/openclaw/openclaw/issues/88838) (35 comments, Diamond Lobster):** Core session/transcript SQLite migration via accessor seam. Represents the deepest architectural thread currently active, reflecting the community's intense focus on the state migration path.
- **[#96148](https://github.com/openclaw/openclaw/issues/96148) (17 comments, Platinum Hermit):** iMessage source-reply latency instrumentation. Significant operator interest in proactive channel performance observability.
- **[#92201](https://github.com/openclaw/openclaw/issues/92201) (14 comments, Diamond Lobster):** Anthropic thinking signatures intermittently invalid on replay. A critical provider-side regression with no fix PR yet, drawing sustained attention.
- **[#90991](https://github.com/openclaw/openclaw/issues/90991) (14 comments, CLOSED):** Cron scheduled trigger contaminating global runtime state — generated high discussion before being resolved.
- **[#42840](https://github.com/openclaw/openclaw/issues/42840) (8 comments, +7 👍):** Long-standing feature request for MathJax/LaTeX rendering in Control UI. Highest raw reaction count in the issue tracker.

### Most Active Pull Requests
- **[#96211](https://github.com/openclaw/openclaw/pull/96211) (XL, Ready for Maintainer Look):** Exposing requester origin to tool policy hooks. Broader enterprise policy implications driving engagement.
- **[#88968](https://github.com/openclaw/openclaw/pull/88968) (P1, Platinum Hermit):** Preventing memory flush failure from aborting user reply. An older critical patch gaining renewed urgency.
- **[#95631](https://github.com/openclaw/openclaw/pull/95631) (P1, Platinum Hermit, XL):** The memory store relocation fix is the most scrutinized patch of the day due to its high merge risk and direct user impact.
- **Marketplace Feed Stack (PRs #96158, #96155, #95981, #95969, #96194):** A coordinated series of pull requests by `giodl73-repo` signaling a major upcoming feature. The hosted marketplace feed is the most significant roadmap signal visible in the PR queue.

---

## Bugs & Stability

The bug landscape today is dominated by **regressions introduced in the `2026.6.x` train** and **provider-specific contract breakages**.

### Critical (P1 / Diamond Lobster)

| Issue | Summary | Status |
|---|---|---|
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic thinking signatures invalid on replay; recovery wrapper never fires | **No fix PR exists** |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | Native Anthropic path: replaying `thinking` blocks bricks long tool-use threads (400 error) | **No fix PR exists** |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s compaction timeout is single wall clock with no progress reuse | **PR #95885 in flight** |
| [#95833](https://github.com/openclaw/openclaw/issues/95833) | Subagent abort-settle fails to release `.jsonl.lock`, permanently breaking session | **No fix PR exists** |
| [#92057](https://github.com/openclaw/openclaw/issues/92057) | Gateway becomes slow/times out under multi-session / multi-agent load | **No fix PR exists** |
| [#94939](https://github.com/openclaw/openclaw/issues/94939) | 6.x state migration leaves channel conversation-store SQLite empty (0 bytes) — MS Teams | **No fix PR exists** |

### High / Regressions (Platinum Hermit / P1-P2)

| Issue | Summary | Status |
|---|---|---|
| [#96118](https://github.com/openclaw/openclaw/issues/96118) | [6.9 Regression] Dreaming runs but memory never promotes | **CLOSED** |
| [#95554](https://github.com/openclaw/openclaw/issues/95554) | [6.9 Regression] Telegram richMessages breaks paragraph breaks and table rendering | **No fix PR exists** |
| [#95538](https://github.com/openclaw/openclaw/issues/95538) | [6.9 Regression] Telegram `/status` card collapses into one run-on line | **No fix PR exists** |
| [#94251](https://github.com/openclaw/openclaw/issues/94251) | Ollama remote provider streaming not consumed — model_call never progresses | **No fix PR exists** |
| [#94518](https://github.com/openclaw/openclaw/issues/94518) | DeepSeek cache hit rate <10% after 6.x upgrade | **Linked PR open** |
| [#95136](https://github.com/openclaw/openclaw/issues/95136) | No migration path/warning when model provider `openai-codex` is removed | **Linked PR open** |

### Data Loss / Session Integrity
- `#94939`: Migration orphans references, breaks proactive sends in MS Teams.
- `#88657`: DeepSeek V4 Flash produces incomplete turns (`payloads=0, tools=2`).
- `#88870`: Stuck-session recovery aborts legitimately long, actively working agent runs with misleading "aborted by user" errors.

---

## Feature Requests & Roadmap Signals

### Highly Voted User Requests
- **[#42840](https://github.com/openclaw/openclaw/issues/42840) (+7 👍):** MathJax/LaTeX rendering support for Control UI. Unaddressed since March, remains the highest-voted feature request.
- **[#93422](https://github.com/openclaw/openclaw/issues/93422) (+2 👍):** `/label` slash command and session naming for WebChat/Control UI sessions.
- **[#92314](https://github.com/openclaw/openclaw/issues/92314) (+2 👍):** Workboard card delete/remove API.

### Architecture & Roadmap Signals
- **[#96156](https://github.com/openclaw/openclaw/issues/96156):** Allow compaction providers to be MCP servers — a forward-looking abstraction that would dramatically expand the compaction engine ecosystem.
- **[Marketplace Feed Stack](https://github.com/openclaw/openclaw/pulls?q=is%3Apr+author%3Agiodl73-repo+hosted-feed):** Eight PRs from maintainer `giodl73-repo` layering hosted catalog config, validation, feeds, commands, telemetry, and plugin registry findings into `openclaw doctor`. This is the single strongest roadmap signal in the current data — a **built-in plugin marketplace** is actively being built.
- **[#91945](https://github.com/openclaw/openclaw/issues/91945):** Upgrade Cloudflare AI Gateway provider to use the new REST API.
- **[#90916](https://github.com/openclaw/openclaw/issues/90916):** Topic-session families for one assistant across multiple context lanes.
- **[#71712](https://github.com/openclaw/openclaw/issues/71712):** Agent-facing scheduling API with non-forgeable provenance.

### Likely for Next Patch Release
- Memory store migration hotfix (#95631)
- Compaction loop prevention (#95885)
- Provider fallback fix (#96260)
- Matrix SAS verification fix (#96210)
- The marketplace feed stack (if it clears review)

---

## User Feedback Summary

### Pain Points
1. **Upgrade Fragility:** Users report that the 6.x upgrade path silently corrupts or empties state stores (conversation DBs, memory indexes) with no migration warning ([#94939](https://github.com/openclaw/openclaw/issues/94939), [#95495](https://github.com/openclaw/openclaw/issues/95495)).
2. **Provider Breakage:** DeepSeek cache hit rates collapse, Anthropic thinking blocks brick sessions, and Ollama remote provider streaming silently fails — all without clear error messaging ([#88657](https://github.com/openclaw/openclaw/issues/88657), [#94228](https://github.com/openclaw/openclaw/issues/94228), [#94251](https://github.com/openclaw/openclaw/issues/94251)).
3. **Aggressive Defaults:** The 180s compaction timeout and 90s stuck-session abort threshold are too aggressive for workflows with long history or slow providers, causing false crash loops ([#92043](https://github.com/openclaw/openclaw/issues/92043), [#88870](https://github.com/openclaw/openclaw/issues/88870)).
4. **Lock Contention:** Subagent lock files (`jsonl.lock`) are not released on abort failure, permanently breaking sessions until manual intervention ([#95833](https://github.com/openclaw/openclaw/issues/95833)).

### Satisfaction Signals
- The "clawsweeper" triage label system is well-received and provides transparency into maintainer prioritization.
- The community is highly engaged in providing structured reproduction steps and even submitting PRs for the bugs they find — a strong sign of ecosystem health.
- Advanced users appreciate the depth of feature requests being drafted (topic-session families, agent scheduling, MCP compaction providers).

### Channel-Specific Feedback
- **Telegram:** Users report high satisfaction with TTS features but frustration with rich message regressions in 6.9.
- **Windows:** ACPX runtime has been largely unusable, creating a significant platform gap that the closure of [#93465](https://github.com/openclaw/openclaw/issues/93465) should help remedy.
- **Feishu / Discord:** Compaction and mention alias bugs have been resolved, restoring trust in these channels.

---

## Backlog Watch

### Old Feature Requests Awaiting Maintainer Attention

| Issue | Created | Summary | Impact |
|---|---|---|---|
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | 2026-03-11 | MathJax/LaTeX in Control UI | User Experience, +7 votes |
| [#46548](https://github.com/openclaw/openclaw/issues/46548) | 2026-03-14 | Tool error messages should include failure reason | Debugging, P2 |
| [#49931](https://github.com/openclaw/openclaw/issues/49931) | 2026-03-18 | Configurable shell override for exec tool | Platform Parity, Security |
| [#38520](https://github.com/openclaw/openclaw/issues/38520) | 2026-03-07 | Pre-compaction agent notification & handoff window | Stateful Workflows |
| [#71712](https://github.com/openclaw/openclaw/issues/71712) | 2026-04-25 | Agent-facing scheduling API | Automation |
| [#79047](https://github.com/openclaw/openclaw/issues/79047) | 2026-05-07 | Preserve context across cross-backend model switches | Architecture |
| [#72021](https://github.com/openclaw/openclaw/issues/72021) | 2026-04-26 | Short-term promotion signalCount bug | Memory Accuracy |

### Critical Fix PRs in Maintainer Review Queue
- **[#88968](https://github.com/openclaw/openclaw/pull/88968) (P1):** Preventing memory flush failure from aborting user reply. Filed June 1, still awaiting final merge despite being marked "ready for maintainer look."
- **[#95631](https://github.com/openclaw/openclaw/pull/95631) (P1):** Memory store relocation fix. The highest-risk patch in the queue with multiple merge flags (compatibility, session-state).

### Overall Backlog Health
The project maintains a highly organized triage pipeline with explicit labels for maintainer review status, but the sheer volume of incoming issues (190/day) is creating latency for older, valuable feature requests that lack dedicated PRs. The "hosted marketplace" initiative, if merged, would be the largest feature addition since the plugin system launch.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date:** 2026-06-24

---

## 1. Ecosystem Overview

The open-source personal AI agent landscape is undergoing a rapid maturation phase characterized by intense competition, architectural consolidation, and growing pains around security and state reliability. Projects are universally moving beyond simple conversational interfaces toward autonomous, scheduled, and multi-agent workflows, with plugin ecosystems and mobile/desktop parity emerging as baseline expectations. The community is highly engaged but burdened by regressions introduced during rapid feature iteration, particularly around state migration paths and provider contract changes. Vendor lock-in is being aggressively broken down as teams build abstraction layers to support diverse LLM backends, though standardizing model behavior across providers remains the ecosystem's most persistent technical debt.

---

## 2. Activity Comparison

| Project | Issues Updated (Open) | PRs Updated (Open) | Release Today | Health Assessment |
|---|---|---|---|---|
| **OpenClaw** | 190 (140) | 500 (460) | No | ★★★☆☆ – Highest volume; signal vs. noise concerns; regression-heavy |
| **NanoBot** | 14 (6) | 40 (25) | No | ★★★★☆ – Fast triage; security disclosures add maturity pressure |
| **Hermes Agent** | 50 | 50 | No | ★★★★☆ – Deep architectural engagement; token cost friction dominates |
| **PicoClaw** | 2 | 15 (10) | No | ★★★☆☆ – Healthy contributor base; Android stability gap |
| **NanoClaw** | 1 | 12 (4) | No | ★★★★★ – High velocity, excellent maintainer responsiveness |
| **NullClaw** | 1 | 1 (1) | No | ★★☆☆☆ – Low activity; major feature branch in progress |
| **IronClaw** | 22 | 40 | No | ★★★☆☆ – Heavy feature churn; CI deadlock blocking merges |
| **LobsterAI** | 1 (critical) | 11 (6) | No | ★★☆☆☆ – Internal velocity decent; community trust at risk |
| **Moltis** | 0 | 1 (0) | No | ★☆☆☆☆ – Dormant |
| **CoPaw/QwenPaw** | 36 | 50 (24 merged) | **Yes** (v1.1.12.p2) | ★★★★★ – Explosive velocity; mobile sprints dominating |
| **ZeroClaw** | 44 | 50 | No (v0.9.0 prep) | ★★★★☆ – Security-first posture; blocked S1 items persist |
| **TinyClaw** | 0 | 0 | No | ★☆☆☆☆ – Dormant |
| **ZeptoClaw** | 0 | 0 | No | ★☆☆☆☆ – Dormant |

---

## 3. OpenClaw's Position

**Advantages:** OpenClaw serves as the ecosystem's de facto reference architecture, driving the deepest technical debates around state management correctness, compaction mechanics, and session lifecycle. The hosted plugin marketplace initiative (8 coordinated PRs) is the most advanced ecosystem play visible across any project, signaling a clear roadmap toward extensibility that competitors are still drafting. The Diamond Lobster / Platinum Hermit severity taxonomy is a unique organizational advantage that provides the highest transparency into regression prioritization.

**Technical Approach:** OpenClaw emphasizes deep provider-specific integration (Anthropic thinking blocks, DeepSeek caching contracts) rather than broad abstraction layers. This yields higher fidelity with each provider's capabilities but creates a larger regression surface when contracts change upstream—an increasingly frequent event given the rapid pace of LLM provider API evolution.

**Relative Weaknesses:** The regression burden is the highest in the ecosystem. Six P1 "Diamond Lobster" issues remained open or unresolved at the time of digest, including Anthropic thinking signature invalidation and subagent lock file leaks. While the volume of contributions suggests the largest community, it also implies a stabilization gap that more conservative projects (NanoClaw, CoPaw) have managed to avoid.

**Community Scale:** Issue/PR volume (190/500) is an order of magnitude higher than most peers, but this correlates with churn, not necessarily happiness. The community provides detailed reproduction steps and contributes patches actively, signaling a high-skill user base that is simultaneously the project's greatest asset and most demanding stakeholder.

---

## 4. Shared Technical Focus Areas

**Token & Cost Optimization (All Tier 1–2 Projects)**
- Hermes Agent: Lazy tool schema loading (73% fixed overhead identified)
- OpenClaw: Anthropic thinking block efficiency, prompt cache stabilization
- IronClaw: Progressive tool disclosure (91 schemas → relevant subsets)
- NanoBot: Dream cursor bloat prevention
- CoPaw: Context window management in mobile adaptation

*Implication: The market no longer tolerates "inject all context" architectures. Lazy loading, context pruning, and provider caching are now table stakes.*

**Security & Execution Hardening (7+ Projects Active)**
- NanoBot: MCP enabledTools bypass disclosures (unfixed, highest-severity open issue)
- ZeroClaw: WASM host function allowlists, supply chain SLSA attestation
- PicoClaw: CSRF launcher rejection, exec deny-pattern enforcement
- NanoClaw: Slack Socket Mode (eliminates exposed ports)
- Hermes: Inline-eval hardening, credential pool integrity
- OpenClaw: Plugin signature enforcement preview

*Implication: The ecosystem is shifting from "trusted plugins" to capability-gated, sandboxed models as a direct response to the security implications of agentic file/network access.*

**State Management Reliability (Universal Pain Point)**
- Session corruption: OpenClaw (compaction locks), NanoBot (duplicate tool_use IDs)
- Credential integrity: Hermes (credential pool drops), LobsterAI (upgrade crash)
- Memory optimization: OpenClaw (memory promotion regression), NanoBot (Dream lifecycle)
- Cron/scheduled task reliability: CoPaw (fixed), ZeroClaw (in-flight)

*Implication: Persistent state remains the single most fragile layer. Silent corruption (empty SQLite files, missing credentials) is the most dangerous failure mode across the board.*

**Provider Abstraction & Model Agnosticism (6+ Projects Active)**
- NanoBot: Kimi Coding, OpenCode integration
- CoPaw: Custom provider function calling
- LobsterAI: LiteLLM gateway
- PicoClaw: AWS Bedrock prompt caching
- NanoClaw: Manifest model router
- ZeroClaw: OpenRouter fallback models

*Implication: Standard OpenAI-compatible abstraction is insufficient. Projects are building sophisticated multi-LLM routing and caching layers as core infrastructure, not add-ons.*

**Mobile, Desktop & CLI Parity (4+ Projects Significant)**
- CoPaw: Massive mobile adaptation sprint (8+ PRs)
- NanoBot: PWA mobile support with gestures and service-worker caching
- Hermes: Desktop offline mode, CLI parity fixes
- PicoClaw: Android/Termux stability

*Implication: Platform convergence is an explicit requirement. Users demand continuity across mobile, desktop, terminal, and messaging channels.*

---

## 5. Differentiation Analysis

| Project | Primary Target | Architecture Philosophy | Winning Differentiator | Critical Risk |
|---|---|---|---|---|
| **OpenClaw** | Power users, self-hosters | Deep provider integration, extensible core | Plugin marketplace, state management depth | Regression pace |
| **NanoBot** | End-users, mobile consumers | Lightweight, rapid feature delivery, PWA-first | Speed of iteration, provider diversity | Security audit gaps |
| **Hermes Agent** | Enterprise ops, production AI | Performance-first, token-optimized orchestration | Lazy schema loading, ACP orchestration | State/config fragility |
| **CoPaw/QwenPaw** | Qwen ecosystem, mobile users | Full-stack MVC, mobile-first Console UI | Mobile adaptation velocity, Qwen integration | RAM overhead, vendor affinity |
| **ZeroClaw** | Security teams, self-hosted | Secure-by-default, WASM isolation | Supply chain security, plugin sandboxing | Blocked architectural S1 items |
| **IronClaw** | Enterprise productivity | Integrated SaaS skills, Google/Microsoft focus | Native Workspace integration, Reborn arch | CI debt, scheduler deadlock |
| **LobsterAI** | Team collaboration | Cowork plan-centric workflows | LiteLLM gateway, persistent plan mode | Unresolved upgrade regression |
| **PicoClaw** | Edge/embedded, East Asia | Lightweight agent SDK, Chinese platforms | Remote agent mode, Bedrock caching | Android stability |
| **NanoClaw** | Developer tooling | Extension-point seams, plugin framework | Runtime extensibility, Hook Surface Guard | Newer project, smaller base |
| **NullClaw** | Decentralized / Nostr ecosystem | Minimal core, cron/automation | Cron subagent hierarchy | Very low iteration speed |
| **Moltis** | Channel tooling | Simple skill tool additions | `send_image` tool | Dormant |

---

## 6. Community Momentum & Maturity

**Tier 1 – Explosive Growth / Highest Iteration**
- **CoPaw/QwenPaw:** 24 PRs merged in 24 hours, patch release shipped. Mobile adaptation sprint is the single most focused initiative in the ecosystem this period.
- **OpenClaw:** Raw volume (500 PRs, 190 issues) indicates the largest engaged user base despite regression frustrations.
- **ZeroClaw:** Sprinting toward v0.9.0 with coordinated security hardening, unified command registries, and streaming improvements.
- **NanoClaw:** 8 PRs merged in 24 hours with nearly perfect maintainer responsiveness — the most efficient ratio of merges to activity.

**Tier 2 – High Velocity, Maturing**
- **Hermes Agent:** 6 PRs merged, deep architectural discussions (lazy loading, orchestration) driven by a sophisticated power-user base.
- **NanoBot:** 15 PRs merged, security disclosures adding maturity pressure. Fast triage is generating strong community trust despite open vulnerabilities.
- **IronClaw:** 19 PRs merged, heavy Reborn architecture investment, but stability debt (CI deadlock, scheduler) is accumulating.

**Tier 3 – Niche Development**
- **PicoClaw:** Healthy contributor culture, quality security patches, but smaller issue volume. Android crash is a platform blocker.
- **LobsterAI:** Internal development is moving (5 PRs merged), but the community view is dominated by a single unresolved critical regression and stalled community contributions.

**Tier 4 – Consolidation / Stasis**
- **NullClaw:** Quiet period resolved a critical crash bug. Long-running cron feature branch is the primary signal.
- **Moltis, TinyClaw, ZeptoClaw:** Near-dormant activity levels. No meaningful feature or stability signals.

---

## 7. Trend Signals

**1. The Shift from Chat to Autonomous Workflow**
The clear trajectory across all active projects is toward *persistent, scheduled, and multi-step* execution—not reactive chat. LobsterAI's persistent plan mode, NullClaw's cron subagent hierarchy, OpenClaw's scheduling API drafts, and IronClaw's automation CRUD all converge on a vision of the agent as an autonomous worker rather than a conversation partner. The "post-chat" agent is the end state.

**2. Security as the Critical Path to Production**
NanoBot's MCP bypass disclosures, ZeroClaw's comprehensive WASM/SLSA hardening, and the widespread credential/state integrity bugs across Hermes and OpenClaw signal a market-wide reckoning. Plugin ecosystems cannot scale without granular, auditable security models. The community is learning this lesson in real time through exploitation risk rather than foresight. Projects that ship robust security defaults (ZeroClaw, NanoClaw's socket mode) will have a competitive advantage.

**3. Token Efficiency is a Platform Feature, Not an Optimization**
Lazy loading, context pruning, progressive tool disclosure, and provider caching are moving from nice-to-have to mandatory architecture decisions. The cost of "brute force" context injection is no longer acceptable at scale. This is driving deep architectural changes (Hermes two-pass schema loading, IronClaw tool subsets, OpenClaw prompt cache stabilization) that define the next generation of agent runtimes.

**4. Ubiquitous Multi-Surface Interfaces**
The dissolution of boundaries between mobile, desktop, web, and CLI is a first-order requirement. Users expect continuity without platform sacrifice. CoPaw's mobile sprint, NanoBot's PWA, Hermes' desktop offline mode, and ZeroClaw's unified command registry all respond to the same demand: the agent must be everywhere.

**5. Provider Abstraction Remains Unsolved**
The proliferation of dedicated provider PRs (Kimi, OpenCode, LiteLLM, OpenRouter), alongside persistent failures in custom provider tool calling (CoPaw, OpenClaw), reveals a painful truth: standardizing LLM behavior across non-OpenAI providers is the ecosystem's most volatile technical debt. Every major project is building bespoke routing and caching layers, indicating that the market has not yet converged on a stable abstraction protocol for multi-LLM orchestration.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-24

**Data Snapshot:**
- Issues Updated: 14 (6 Open, 8 Closed)
- PRs Updated: 40 (25 Open, 15 Merged/Closed)
- New Releases: 0

---

## 1. Today's Overview

Today was a high-velocity development day for NanoBot, marked by critical security disclosures, rapid bug fixes, and strategic provider expansion. The community submitted and merged fixes for severe session-poisoning bugs (duplicate `tool_use` IDs) and platform-specific regressions (Telegram line-breaks, iOS Safari zoom). Concurrently, two high-severity security vulnerabilities concerning the MCP `enabledTools` policy were disclosed and remain open for resolution. The addition of formal providers for Kimi Coding and OpenCode underscores a clear push toward diversifying and optimizing backend model support. With 40 active PRs, the project demonstrates a highly responsive and engaged maintenance cycle, though the open security issues temper overall project confidence.

## 2. Releases

No new releases were published today.

---

## 3. Project Progress (Merged/Closed PRs)

### Provider Ecosystem Expansion
- **Kimi Coding Plan:** PR [#4464](https://github.com/HKUDS/nanobot/pull/4464) (closed) introduced the `kimi_coding` provider, giving subscription users access to Kimi's Anthropic-compatible Messages API endpoint.
- **OpenCode Integration:** PR [#4476](https://github.com/HKUDS/nanobot/pull/4476) (closed) added support for OpenCode Zen (curated coding models) and OpenCode Go (low-cost models), significantly broadening the available model ecosystem.

### Stability & Core Fixes
- **Session Poisoning Resolved:** A critical bug where streaming providers produced duplicate `tool_use` IDs (permanently bricking sessions with HTTP 400 errors) was fixed by PR [#4444](https://github.com/HKUDS/nanobot/pull/4444) and PR [#4443](https://github.com/HKUDS/nanobot/pull/4443) (both closed).
- **Gateway Lifecycle:** PR [#4447](https://github.com/HKUDS/nanobot/pull/4447) (closed) fixed multiple edge cases in the gateway lifecycle, including proper launchd enable/start semantics and timeout state handling.

### UI & Platform Fixes
- **Telegram Streaming:** PR [#4472](https://github.com/HKUDS/nanobot/pull/4472) (closed) resolved two major regressions: line breaks being ignored and message flickering caused by `sendRichMessage` integration.
- **iOS Safari Zoom:** PR [#4471](https://github.com/HKUDS/nanobot/pull/4471) (closed) fixed the persistent auto-zoom bug on the WebUI composer input.
- **Pairing Store:** PR [#4433](https://github.com/HKUDS/nanobot/pull/4433) (closed) fixed a type-coercion inconsistency that could silently deny pairing operations.

### Infrastructure & Documentation
- **Node Upgrade:** PR [#4460](https://github.com/HKUDS/nanobot/pull/4460) (closed) bumped the project to Node 24.
- **Environment Variables:** PR [#4462](https://github.com/HKUDS/nanobot/pull/4462) (closed) formally documented all public and internal runtime environment variables.

---

## 4. Community Hot Topics

- **Critical Security Audit — MCP `enabledTools` Bypass:** Issues [#4434](https://github.com/HKUDS/nanobot/issues/4434) and [#4435](https://github.com/HKUDS/nanobot/issues/4435) by YLChen-007 detail a fundamental architectural flaw where the documented per-server allowlist (`enabledTools: []`) fails to restrict resource and prompt capabilities. This is the highest-priority conversation on the tracker and represents a significant trust and governance risk for users relying on MCP security boundaries. The underlying community need is clear: robust, auditable access controls for multi-server MCP setups.

- **Endless Tool Calling Loops:** Issue [#2298](https://github.com/HKUDS/nanobot/issues/2298) (created March 2026, 5 comments) continues to draw attention. Users running smaller or local models report the agent enters infinite loops repeating the same tool calls. The underlying need is a built-in circuit breaker or heuristic detection for non-progressing tool sequences, which remains an unaddressed gap in the agent runtime.

- **Raw Thinking Tags in WebUI:** Issue [#4465](https://github.com/HKUDS/nanobot/issues/4465) and associated PR [#4466](https://github.com/HKUDS/nanobot/pull/4466) sparked significant discussion. The WebUI renders `<thinking/>` tags as visible text rather than parsing them into a dedicated reasoning block, leaking model control tokens to the user. The community expects proper normalization alongside existing `<think>/<thought>` handling.

---

## 5. Bugs & Stability

### Critical
- **MCP Security Bypass ([#4434](https://github.com/HKUDS/nanobot/issues/4434), [#4435](https://github.com/HKUDS/nanobot/issues/4435)):** [OPEN] No fix committed. Architectural vulnerability allowing unintended model access to MCP resources and prompts.
- **Session Bricking — Duplicate tool_use IDs ([#4442](https://github.com/HKUDS/nanobot/issues/4442)):** [FIXED] Permanently corrupted sessions via HTTP 400 errors. Resolved by PR [#4444](https://github.com/HKUDS/nanobot/pull/4444) and PR [#4443](https://github.com/HKUDS/nanobot/pull/4443).

### High
- **Endless Tool Loops ([#2298](https://github.com/HKUDS/nanobot/issues/2298)):** [OPEN] No mitigation strategy implemented. Core reliability issue for local model users.
- **MCP Reconnect Crash ([#4441](https://github.com/HKUDS/nanobot/pull/4441)):** [OPEN PR] `RuntimeError: Attempted to exit cancel scope in a different task` when `streamable_http` generators fail to reconnect.
- **Dream Cursor Bloat ([#4481](https://github.com/HKUDS/nanobot/pull/4481)):** [OPEN PR] Disabling Dream prevents cursor advancement, causing unbounded prompt growth over time.

### Medium
- **Telegram Regressions ([#4470](https://github.com/HKUDS/nanobot/issues/4470)):** [FIXED] Newline stripping and visual flickering in streaming responses. Resolved by PR [#4472](https://github.com/HKUDS/nanobot/pull/4472).
- **iOS Safari Zoom ([#4388](https://github.com/HKUDS/nanobot/issues/4388)):** [FIXED] Form control auto-zoom. Resolved by PR [#4471](https://github.com/HKUDS/nanobot/pull/4471).
- **Subagent fail_on_tool_error ([#4485](https://github.com/HKUDS/nanobot/pull/4485)):** [OPEN PR] Hardcoded to `True`, causing premature subagent failures on minor tool errors.

### Low
- **Local Provider Hijacking ([#3732](https://github.com/HKUDS/nanobot/pull/3732)):** [OPEN] Keyword matching favors local providers without requiring an `api_base` check.
- **DuckDuckGo Proxy Support ([#4484](https://github.com/HKUDS/nanobot/pull/4484)):** [OPEN] DDGS client ignores configured proxy settings, blocking users in restricted networks.

---

## 6. Feature Requests & Roadmap Signals

### Strong Signals & Likely Next Features
- **Provider Diversification:** Merged PRs for Kimi Coding and OpenCode confirm the roadmap prioritizes giving users choice in specialized, optimized backend endpoints. Expect continued provider registration patterns.
- **Mobile Experience (PWA):** Issue [#4457](https://github.com/HKUDS/nanobot/issues/4457) was closed outlining the implementation, and PR [#4480](https://github.com/HKUDS/nanobot/pull/4480) adds swipe gestures and full service-worker caching. Mobile parity is clearly a near-term goal for the next release.
- **Advanced Memory/Dream System:** PR [#4477](https://github.com/HKUDS/nanobot/pull/4477) introduces a lifecycle-aware wiki memory writer. Issue [#4467](https://github.com/HKUDS/nanobot/issues/4467) requests incremental skill updates instead of duplication. The "Dream" feature is evolving from a simple cron task into a structured long-term memory layer.
- **Agent Behavior Configuration:** PR [#4485](https://github.com/HKUDS/nanobot/pull/4485) (subagent error handling) and PR [#4482](https://github.com/HKUDS/nanobot/pull/4482) (custom provider thinking style) suggest a push toward making agent internals deeply configurable per-user.

**Prediction:** The next version will likely ship PWA mobile support, a security patch for MCP tool/resource filtering, the Dream lifecycle wiki memory writer, and configurable subagent error handling.

---

## 7. User Feedback Summary

### Pain Points
- **Security Anxiety:** The MCP bypass disclosures ([#4434](https://github.com/HKUDS/nanobot/issues/4434), [#4435](https://github.com/HKUDS/nanobot/issues/4435)) raise significant governance concerns, especially for users who rely on `enabledTools` for multi-tenant or production MCP deployments.
- **Reliability Frustrations:** Users on local/budget models continue to experience broken sessions from infinite tool loops ([#2298](https://github.com/HKUDS/nanobot/issues/2298)). The "session bricking" bug ([#4442](https://github.com/HKUDS/nanobot/issues/4442)) was a major trust disruption, though the 24-hour patch cycle was appreciated.
- **Visual Polish:** Raw thinking tags ([#4465](https://github.com/HKUDS/nanobot/issues/4465)) and iOS zoom ([#4388](https://github.com/HKUDS/nanobot/issues/4388)) indicate that frontend UX—especially on mobile—is a distinct community priority.

### Satisfaction & Use Cases
- **Rapid Bug Triage:** The quick turnaround on Telegram and iOS regression fixes (often within hours of reporting) is generating strong community approval and signals high maintainer responsiveness.
- **Dream Feature Engagement:** Despite edge cases, the user base is deeply invested in the Dream system, requesting sophisticated features like incremental skill updates ([#4467](https://github.com/HKUDS/nanobot/issues/4467)) and lifecycle memory ([#4477](https://github.com/HKUDS/nanobot/pull/4477)).
- **Strong Contributor Culture:** A large portion of today's progress came from community-authored PRs (zpljd258 on Kimi/OpenCode/PWA, chengyongru on Telegram/lifecycle/docs, axelray-dev on subagent/dream fixes), indicating a healthy, motivated contributor ecosystem.

---

## 8. Backlog Watch

The following items require maintainer attention to prevent stagnation:

- **[STALE — 3 Months] Breaking Endless Tool Loops ([#2298](https://github.com/HKUDS/nanobot/issues/2298)):** Created 2026-03-20. No maintainer assignment, no roadmap label. This is the single most impactful reliability gap for local model users. Needs a strategy proposal (e.g., max consecutive identical calls, similarity threshold).
- **[STALE — 6 Weeks] Local Provider Matching Bug ([#3732](https://github.com/HKUDS/nanobot/pull/3732)):** Opened 2026-05-11. This subtle provider resolution bug can silently hijack cloud endpoints. No recent maintainer activity or review.
- **[ACTIVE — Today] DuckDuckGo Proxy Support ([#4484](https://github.com/HKUDS/nanobot/pull/4484)):** Critical for users behind firewalls. Should be triaged and merged promptly.
- **[ACTIVE — 3 Days] MCP Reconnect Crash ([#4441](https://github.com/HKUDS/nanobot/pull/4441)):** High-severity stability issue for persistent MCP connections. Needs review and testing.
- **[ACTIVE — Today] Config Preservation Bug ([#4478](https://github.com/HKUDS/nanobot/pull/4478)):** Dream cron excluded from `save_config()`, silently losing user-provided overrides on unrelated config saves.

---

*Generated for 2026-06-24*  
*Project: [NanoBot (HKUDS/nanobot)](https://github.com/HKUDS/nanobot)*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-24

## 1. Today's Overview
Activity levels are very high, with **50 issues and 50 pull requests** updated in the last 24 hours, though **no official releases** were cut today. The community closed **7 issues** and merged/closed **6 pull requests**, signaling a productive cycle of bug fixing and cleanup. Core themes dominating the conversation include **token overhead optimization**, **credential and session-state integrity**, **multi-agent orchestration (ACP)**, and **desktop/CLI parity fixes**. The project appears to be in a stabilization and polish phase ahead of a likely feature-focused minor release.

## 2. Releases
**None.** No new versions or release artifacts were published today.

## 3. Project Progress
Six pull requests were merged or closed today, advancing several areas:

- **WhatsApp Routing (Merged):** [PR #51635](https://github.com/NousResearch/hermes-agent/pull/51635) adds chat/group-to-profile routing for the WhatsApp gateway, with dashboard API support. A significant gateway feature.
- **WSL-to-Windows Skill (Merged):** [PR #17209](https://github.com/NousResearch/hermes-agent/pull/17209) introduces a reusable skill for printer invocation from WSL, filling a cross-platform automation gap.
- **MCP Stability (Closed):** [Issue #51587](https://github.com/NousResearch/hermes-agent/issues/51587) (tools not surfacing after connecting) was resolved, fixing a high-impact integration blocker.
- **Security (Merged):** [PR #51305](https://github.com/NousResearch/hermes-agent/pull/51305) bumps dependencies for critical CVEs (starlette, cryptography, tornado).
- **Environment Compatibility (Closed):** [Issue #39118](https://github.com/NousResearch/hermes-agent/issues/39118) (`_ensure_uv_for_termux` Rust compile) and [Issue #51575](https://github.com/NousResearch/hermes-agent/issues/51575) (desktop stop-button popup /interrupt ghost command) were resolved.

**Open PRs closing in:** Long-running features like **Zulip integration** ([PR #3335](https://github.com/NousResearch/hermes-agent/pull/3335), open since March 27) and **Vertex AI provider** ([PR #8427](https://github.com/NousResearch/hermes-agent/pull/8427), open since April 12) continue to receive updates, nearing review readiness.

---

## 4. Community Hot Topics

### Highest Engagement — Issues

| Issue | Comments | Reactions | Topic |
|-------|----------|-----------|-------|
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | 26 | 14 👍 | Lazy Tool Schema Loading |
| [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) | 15 | 0 | 73% fixed token overhead |
| [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) | 11 | 16 👍 | Generalized ACP client |
| [#38387](https://github.com/NousResearch/hermes-agent/issues/38387) | 8 | 1 👍 | Windows blank console gateway |
| [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) | 8 | 1 👍 | OpenAI-Codex credential pool drop |

**Underlying Needs Analysis:**
- **Token Economics Dominates:** The top two threads ([#6839](https://github.com/NousResearch/hermes-agent/issues/6839) and [#4379](https://github.com/NousResearch/hermes-agent/issues/4379)) reflect a community intensely focused on cost efficiency. Users have built their own monitoring dashboards and are demanding a shift from "inject all schemas" to a demand-driven, two-pass schema loading model. This is the most urgent architectural pain point for power users.
- **Agent Orchestration Demand:** The high reaction count on [Issue #5257](https://github.com/NousResearch/hermes-agent/issues/5257) (Generalized ACP Client) signals a clear strategic desire: users want Hermes to act as a **conductor for multi-agent workflows** (orchestrating Claude Code, Cline, etc.), not just a standalone agent.
- **Reliability Confidence Errosion:** [Issue #19566](https://github.com/NousResearch/hermes-agent/issues/19566) (credentials disappearing during rotation) and [Issue #43083](https://github.com/NousResearch/hermes-agent/issues/43083) (password masking breaking tool calls) are eroding trust in state management, especially for production or "always-on" setups.

---

## 5. Bugs & Stability

### Critical Severity (P1) — Active or Updated Today
- **Credential Integrity:**
  - [Issue #19566](https://github.com/NousResearch/hermes-agent/issues/19566) — OpenAI-Codex credential pool drops newly added credentials during auth.json rewrite. Risk: security, session state. No linked fix PR.
  - [Issue #43083](https://github.com/NousResearch/hermes-agent/issues/43083) — Password masking (`***`) causes the model to fail on second tool call when reading its own history. Risk: security boundary, session failure. No fix PR observed.
- **Gateway Regressions:**
  - [Issue #51579](https://github.com/NousResearch/hermes-agent/issues/51579) — Docker `gateway run` strips `$HERMES_HOME/.env` on every container start. Risk: compatibility, data loss. Regression of #26804.
  - [Issue #48648](https://github.com/NousResearch/hermes-agent/issues/48648) — Telegram infinite message duplication loop on 4096-char overflow. Risk: message delivery.

### Medium Severity (P2) — Reported or Updated Today
- **Desktop / TUI Gaps:**
  - [Issue #50005](https://github.com/NousResearch/hermes-agent/issues/50005) — Desktop app freezes on WebSocket disconnect (no offline mode).
  - [Issue #47368](https://github.com/NousResearch/hermes-agent/issues/47368) — "Delete profile" in Desktop silently fails; profile keeps reappearing.
  - [Issue #51636](https://github.com/NousResearch/hermes-agent/issues/51636) — `terminal.working_dir` config ignored on new session start.
- **Config & Provider:**
  - [Issue #51607](https://github.com/NousResearch/hermes-agent/issues/51607) — Session billing fields don't track mid-session model switches.
  - [Issue #27538](https://github.com/NousResearch/hermes-agent/issues/27538) — `auxiliary.compression.provider` ignored after `/model` switch.
  - [Issue #51578](https://github.com/NousResearch/hermes-agent/issues/51578) — `computer_use` cannot find Qt6 apps (FreeCAD) even though `cua-driver` sees them.
  - [Issue #38146](https://github.com/NousResearch/hermes-agent/issues/38146) — Desktop build on `main` fails with 389 TypeScript errors.

### Fix PRs Moving Today
- [PR #51638](https://github.com/NousResearch/hermes-agent/pull/51638): Fixes `/learn` command routing in desktop/TUI.
- [PR #50876](https://github.com/NousResearch/hermes-agent/pull/50876): Bounds provider-facing terminal output to prevent large inline dumps.
- [PR #47604](https://github.com/NousResearch/hermes-agent/pull/47604): Clears stale `base_url` on provider switch (fixes Desktop model picker).
- [PR #47668](https://github.com/NousResearch/hermes-agent/pull/47668): Detects modern `services.ai.azure.com` URLs.

---

## 6. Feature Requests & Roadmap Signals

**Likely Candidates for Next Release (v0.18.0+):**
- **Lazy Tool Schema Loading** ([Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839)). Given the overwhelming data-backed demand and deep community analysis, this is the strongest candidate for a headline feature in the next major version.
- **Generalized ACP Client** ([Issue #5257](https://github.com/NousResearch/hermes-agent/issues/5257)). High community reaction count and industry alignment (MCP/ACP) make this a strong roadmap differentiator.
- **Gateway & Platform Expansions:**
  - **Zulip** ([PR #3335](https://github.com/NousResearch/hermes-agent/pull/3335)) and **Vertex AI** ([PR #8427](https://github.com/NousResearch/hermes-agent/pull/8427)) are approaching maturity.
  - **WhatsApp routing** ([PR #51635](https://github.com/NousResearch/hermes-agent/pull/51635)) just landed, confirming a focus on enterprise messaging.
- **Gamification / Delight:**
  - **Pet Generation** ([PR #47959](https://github.com/NousResearch/hermes-agent/pull/47959)) introduces a full Pokédex-style overlay (hatching, adopting). Signals a desire to differentiate the Desktop UX.

**Predictions:**
- A **v0.17.1 patch** is likely imminent to address the critical Docker `.env` regression ([#51579](https://github.com/NousResearch/hermes-agent/issues/51579)) and Telegram loop ([#48648](https://github.com/NousResearch/hermes-agent/issues/48648)).
- The next minor release (v0.18) will likely be branded around **"Token Efficiency & Orchestration"** if the maintainers adopt the lazy loading and ACP proposals.

---

## 7. User Feedback Summary

**Primary Pain Points:**
- **Token Waste is the #1 Frustration:** The community is vocal and data-backed about 73% fixed overhead. Users feel they are paying for unused capabilities on every API call.
- **State & Config Fragility:** Credentials dropping out ([#19566](https://github.com/NousResearch/hermes-agent/issues/19566)), auxiliary providers breaking after model switches ([#27538](https://github.com/NousResearch/hermes-agent/issues/27538)), and Docker configs being reset ([#51579](https://github.com/NousResearch/hermes-agent/issues/51579)) create a sense of unreliability in persistent setups.
- **Desktop-Offline Parity Gap:** Users want the Desktop app to survive network blips ([#50005](https://github.com/NousResearch/hermes-agent/issues/50005)) and have feature parity with the CLI/TUI ([#51575](https://github.com/NousResearch/hermes-agent/issues/51575)).
- **Windows Deployment Friction:** Windows users face a disproportionate share of platform-specific bugs (Tirith installation, blank console windows, build failures).

**Strengths & Satisfaction:**
- **High Power-User Investment:** Users are building monitoring dashboards, writing detailed performance analyses, and proposing architectural changes. This signals a deeply engaged technical user base.
- **Extensibility is Working:** The gateway architecture (WhatsApp, Feishu, Telegram) and plugin system are enabling real-world enterprise integrations, which users appreciate.
- **Personality/UX Wins:** The pet generation feature receives positive buzz, indicating appetite for agent personality and gamification in the official client.

**Sentiment Rating:** The community seems **cautiously optimistic** — excited about the platform's potential but strained by token costs and state-management stability.

---

## 8. Backlog Watch

Items requiring maintainer triage or resolution:

### Stalled Critical Bugs (P1)
- [**Issue #19566**](https://github.com/NousResearch/hermes-agent/issues/19566) (May 4, 2026): OpenAI-Codex credential pool drops. **No fix PR attached.** Two months open for a security-domain bug.
- [**Issue #43083**](https://github.com/NousResearch/hermes-agent/issues/43083) (June 9, 2026): Password masking breaks tool calls. **No fix PR attached.** High risk for session-state integrity.

### Long-Lived Feature Branches Needing Decision
- [**PR #3335**](https://github.com/NousResearch/hermes-agent/pull/3335) (Open since **March 27, 2026**): Zulip integration. In review for 3 months.
- [**PR #8427**](https://github.com/NousResearch/hermes-agent/pull/8427) (Open since **April 12, 2026**): Vertex AI provider. 2.5 months without merge.
- [**Issue #5257**](https://github.com/NousResearch/hermes-agent/issues/5257) (Open since **April 5, 2026**): Generalized ACP Client. 16 👍 and no formal maintainer decision/roadmap acknowledgment.

### Blocked Platform Parity
- [**Issue #26044**](https://github.com/NousResearch/hermes-agent/issues/26044) (May 15, 2026): Tirith security scanner fails on Windows. Security feature blocked for a major platform.
- [**Issue #38146**](https://github.com/NousResearch/hermes-agent/issues/38146) (June 3, 2026): Desktop build fails on `main` (389 TS errors). Severely impacts new contributors trying to run the Desktop app from source.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw Project Digest — 2026-06-24**

---

### 1. Today’s Overview
PicoClaw saw exceptionally high development velocity over the last 24 hours, with **15 pull requests updated** alongside modest issue activity (2 updated). Of those PRs, 10 remain open and actively developed while 5 were merged or closed. The maintainers also performed a noticeable backlog sweep, closing several stale items and shifting focus toward security hardening and enterprise feature work. Although no new release was cut, the project is in a healthy, community-driven state with strong contributor momentum.

---

### 2. Releases
None.

---

### 3. Project Progress
Five PRs were closed or merged, spanning bug fixes, code quality, and critical LLM compatibility:

- **Critical LLM Fix — Doubao Seed Tool Calls ([#3154](sipeed/picoclaw PR #3154)):** Resolved a parsing defect where the Volcengine Doubao Seed model leaked tool calls as raw XML inside `message.content` instead of using the standard `tool_calls` field. This fix closes [#3153](sipeed/picoclaw Issue #3153) and restores reliable agentic workflows.
- **Session History Repair ([#3047](sipeed/picoclaw PR #3047)):** Restored full JSONL history visibility in the session detail view without degrading list pagination performance.
- **LINE Channel Hardening ([#3054](sipeed/picoclaw PR #3054)):** Added missing `ok` checks for `sync.Map` type assertions in `LINEChannel.Send` to prevent potential panics.
- **Resource Cleanup ([#3059](sipeed/picoclaw PR #3059)):** Explicitly acknowledged ignored `Close()` return values in error paths and retry loops, silencing linter warnings.
- **Old Image Fix ([#2888](sipeed/picoclaw PR #2888)):** Closed a stale PR from May that corrected tool config image loading.

---

### 4. Community Hot Topics
- **Windows QQ Channel Troubles:** The now-closed **[#3015](sipeed/picoclaw Issue #3015)** attracted the highest comment count (4) for a discussion around token retrieval timeouts in the official Windows release build. The issue was closed as stale, but the engagement signals strong user interest in robust multi-platform adapter support.
- **Security Hardening Sweep:** PRs **[#3160](sipeed/picoclaw PR #3160)** and **[#3161](sipeed/picoclaw PR #3161)** by contributor *danmobot* are drawing attention for addressing cross-site launcher setup requests and maintaining deny-pattern enforcement for custom allow rules. This reflects a proactive community aligning around execution and auth security.
- **Mobile Breakage:** The newly filed **[#3164](sipeed/picoclaw Issue #3164)** (Android/Termux crash) is the top open issue by recency and is likely to attract rapid community discussion given the popularity of mobile deployment.

---

### 5. Bugs & Stability
- **Critical:** **[#3164](sipeed/picoclaw Issue #3164)** – Process hooks (JSON-RPC over stdio) crash the gateway within 2 seconds on Android/Termux under v0.2.9. No fix PR exists yet. This severely impacts mobile deployment viability.
- **High:** **[#3115](sipeed/picoclaw PR #3115)** – (Open) Session-history corruption bug where `data:image/…` strings inside generic tool output (e.g., `exec`, `read_file`) are incorrectly treated as real media attachments. A fix PR is open and awaiting review.
- **Medium:** **[#3054](sipeed/picoclaw PR #3054)** – (Closed) Unchecked type assertions in the LINE adapter posed a panic risk.
- **Fixed:** **[#3154](sipeed/picoclaw PR #3154)** – Doubao Seed tool call leak. **[#3047](sipeed/picoclaw PR #3047)** – JSONL history truncation.
- **Security Fixes In Progress:** Launcher CSRF rejection ([#3160](sipeed/picoclaw PR #3160)) and exec deny-pattern bypass ([#3161](sipeed/picoclaw PR #3161)) are both open and represent the most impactful stability/security improvements likely to land in the next release.

---

### 6. Feature Requests & Roadmap Signals
- **Enterprise/Cloud Performance:** **[#3163](sipeed/picoclaw PR #3163)** by *loafoe* introduces explicit cache points for AWS Bedrock’s Converse API prompt caching. This is a strong candidate for the next minor release, reducing input token costs for long-context conversations.
- **Agent Connectivity:** **[#3118](sipeed/picoclaw PR #3118)** adds a `--remote` WebSocket mode to the `picoclaw agent` command, enabling distributed, multi-machine agent setups without changing local behavior.
- **Platform UX – Telegram:** **[#2975](sipeed/picoclaw PR #2975)** (open since May 30) would allow Telegram group chats to treat replies to the bot as equivalent to `@mentions`. It remains the longest-pending feature contribution without maintainer feedback.

---

### 7. User Feedback Summary
User pain points continue to center on **cross-platform stability**. The Android/Termux crash ([#3164](sipeed/picoclaw Issue #3164)) directly impacts mobile and headless-server users, while the Windows QQ token issue ([#3015](sipeed/picoclaw Issue #3015)) highlights friction for users on Asian messaging platforms. On the positive side, the rapid submission of high-quality security PRs (danmobot) and enterprise feature work (loafoe’s Bedrock caching, jp39’s remote agent mode) suggests a healthy, skilled contributor base actively shaping the roadmap. The community is clearly moving PicoClaw beyond simple chat into production-grade agent infrastructure.

---

### 8. Backlog Watch
- **Most At-Risk Contribution:** **[#2975](sipeed/picoclaw PR #2975)** (Telegram reply-as-mention) has been open for 25 days with zero maintainer interaction. If this languishes further, contributor attrition risk increases.
- **Stale Sweep:** Today saw the closure of **[#2888](sipeed/picoclaw PR #2888)**, **[#3047](sipeed/picoclaw PR #3047)**, **[#3054](sipeed/picoclaw PR #3054)**, and **[#3059](sipeed/picoclaw PR #3059)**. This aggressive grooming is healthy and suggests the project is compressing its backlog to focus on current active work. However, the Telegram PR (#2975) and the remote agent PR (#3118) should be explicitly triaged (accepted, rejected, or assigned a milestone) to prevent them from entering the same stale path.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-06-24

## 1. Today's Overview
Project activity was exceptionally high today, with **12 pull requests (PRs)** updated and **1 new issue** filed. The core team focused heavily on infrastructure, completing a comprehensive Chat SDK dependency bump to version **4.29.0** across all major development branches. A total of **8 PRs were merged or closed**, signaling strong release velocity and active roadmap execution. The community remains highly engaged, contributing both critical bug reports and substantial architectural enhancements to the runtime. Overall project health is excellent, with a clear balance of maintenance, new features, and forward-looking design work.

## 2. Releases
No new releases today.

## 3. Project Progress
The project saw significant movement in dependency management, integration features, and backend architecture.

- **Bulk Dependency Upgrade:** The entire Chat SDK surface was migrated to **4.29.0**. Key PRs include the core upgrade on `main` ([#2834](https://github.com/nanocoai/nanoclaw/pull/2834)), the `channels` branch ([#2835](https://github.com/nanocoai/nanoclaw/pull/2835)), and the `providers` branch ([#2836](https://github.com/nanocoai/nanoclaw/pull/2836)).
- **Slack Socket Mode:** A major feature was merged allowing Slack connections via an **outbound WebSocket** ([#2837](https://github.com/nanocoai/nanoclaw/pull/2837)), removing the need for a public HTTPS webhook. This was successfully backported to the `channels` branch ([#2839](https://github.com/nanocoai/nanoclaw/pull/2839)).
- **Skill Update Reliability:** A fix merged by Koshkoshinsk prevents users from accidentally skipping critical upstream fixes to channel and provider skills during `/update-nanoclaw`, and ensures containers are rebuilt when skills change ([#2826](https://github.com/nanocoai/nanoclaw/pull/2826)).
- **Development Guidelines Enforcement:** javexed merged a new "Hook Surface Guard" ([#2833](https://github.com/nanocoai/nanoclaw/pull/2833)) to automate compliance with contribution guidelines and ensure stability in the hook/extension system.

## 4. Community Hot Topics

- **Runtime Extensibility Framework (PR [#2842](https://github.com/nanocoai/nanoclaw/pull/2842) | OPEN):** Authored by foxsky, this PR introduces generic `registerX` / `applyX` extension-point seams across the host and container runtime. This architecture is critical for developers who need to deeply customize the core agent loop without direct upstream merges. A prior iteration ([#2841](https://github.com/nanocoai/nanoclaw/pull/2841)) was closed in its favor. *Underlying need: Customization without fork maintenance burden.*

- **Richer Human-in-the-Loop (PR [#2832](https://github.com/nanocoai/nanoclaw/pull/2832) | OPEN):** moshe-nanoco's PR adds a "Reject with reason…" button to module approval cards, letting human operators send specific feedback back to the requesting agent. *Underlying need: Better agent adaptation loops and alignment workflows.*

- **Multi-Provider Model Routing (PR [#2838](https://github.com/nanocoai/nanoclaw/pull/2838) | OPEN):** SebConejo's proposal for a "Manifest model router provider" would allow the system to route requests to different LLM providers based on model capabilities. *Underlying need: Sophisticated multi-LLM strategy management.*

- **Slack Security Contradiction (Issue [#2840](https://github.com/nanocoai/nanoclaw/issues/2840) | OPEN):** User sirpy reports that the default Slack integration binds port **3000 to the external IP** (`0.0.0.0`), which completely negates the security benefit of the recommended tunnel setup. *Underlying need: Secure-by-default local configurations.*

## 5. Bugs & Stability

- **[HIGH SEVERITY] Slack Port Security Flaw (Issue [#2840](https://github.com/nanocoai/nanoclaw/issues/2840)):** The default v2 Slack integration binds to the host's external IP address on port 3000, making the service directly accessible on the local network. This invalidates the documented tunnel-based security model. **Mitigation:** The strategic fix is the newly merged **Slack Socket Mode** ([#2837](https://github.com/nanocoai/nanoclaw/pull/2837)), which bypasses the need for exposed ports and tunnels entirely by using an outbound WebSocket. The documentation for the standard integration should be updated to address this binding behavior.

- **[MEDIUM SEVERITY] Silent Skill Update Gaps (Fixed in [#2826](https://github.com/nanocoai/nanoclaw/pull/2826)):** Users could previously complete the `/update-nanoclaw` process while silently missing critical bug fixes for installed channel or provider skills. The fix now actively nudges users toward performing the update and enforces container rebuilds on re-application.

- **[LOW SEVERITY] Agent Browser Container Stability (PR [#2771](https://github.com/nanocoai/nanoclaw/pull/2771) | OPEN):** A pending PR from ankushchadha addresses crashes in `agent-browser` (headless Chromium) inside Docker containers. The fix proposes adding `--shm-size=1g` (increasing shared memory from default 64MB) and `--init` (ensuring proper signal handling) to Docker run arguments.

## 6. Feature Requests & Roadmap Signals
The data strongly suggests the next minor release will focus on making NanoClaw a more **secure, extensible, and transparent** platform.

- **Locked for Upcoming Release:**
    - **Chat SDK 4.29.0 Bump** (Merged across all branches).
    - **Slack Socket Mode** (Merged, eliminates the port exposure issue).

- **High Probability for Next Release:**
    - **Extension-Point Seams ([#2842](https://github.com/nanocoai/nanoclaw/pull/2842))** – This is a major architectural commitment. If merged, it will be a headline feature unlocking deep customization for enterprise and power users.
    - **Reject with Reason ([#2832](https://github.com/nanocoai/nanoclaw/pull/2832))** – Small code footprint, high UX impact for human-agent interaction loops.

- **Emerging Themes:**
    - **Multi-Provider Orchestration ([#2838](https://github.com/nanocoai/nanoclaw/pull/2838))** – Community demand for routing to different models/providers based on task requirements.
    - **Security-First Configurations** – The tension between [#2840](https://github.com/nanocoai/nanoclaw/issues/2840) (port binding) and [#2837](https://github.com/nanocoai/nanoclaw/pull/2837) (Socket Mode) signals a strong push towards secure-by-default setups.

## 7. User Feedback Summary

- **Pain Points:**
    - **Security Contradiction ([#2840](https://github.com/nanocoai/nanoclaw/issues/2840)):** The clearest user-reported pain point today. User sirpy explicitly flags that the standard Slack setup documentation calls for a secure tunnel, but the application binds to the external IP, rendering the "secure tunnel" recommendation contradictory.
    - **Stability in Containers:** The pending container performance fix ([#2771](https://github.com/nanocoai/nanoclaw/pull/2771)) implies that agent browser crashes are a recurring stability issue for Docker users.
    - **Update Blind Spots:** Users were missing critical skill updates, addressed by the fix in [#2826](https://github.com/nanocoai/nanoclaw/pull/2826).

- **Satisfaction Indicators:**
    - **High Velocity:** 8 merged PRs in 24 hours signals a low-friction, responsive maintainer team.
    - **Good Contributor Hygiene:** PRs [#2833](https://github.com/nanocoai/nanoclaw/pull/2833) and [#2838](https://github.com/nanocoai/nanoclaw/pull/2838) both successfully pass the automated `follows-guidelines` check, showing clear documentation and community alignment.
    - **Responsive Feature Delivery:** The Slack Socket Mode was clearly developed in response to the exact class of security/deployment issues represented by [#2840](https://github.com/nanocoai/nanoclaw/issues/2840), even before the bug was formally reported.

## 8. Backlog Watch

- **Stalled Container Stability Fix (PR [#2771](https://github.com/nanocoai/nanoclaw/pull/2771)):** Open since June 15 (9 days) by ankushchadha. This PR adds `--shm-size=1g` and `--init` to the Docker run arguments. Despite being a straightforward "quick win" for user stability (fixing Chromium crashes), it remains unmerged. It was updated yesterday, suggesting the author is actively looking for a review. High priority for maintainer attention to clear the backlog.

- **Architecture Transparency Needed (PRs [#2841](https://github.com/nanocoai/nanoclaw/pull/2841) / [#2842](https://github.com/nanocoai/nanoclaw/pull/2842)):** The rapid closing of [#2841](https://github.com/nanocoai/nanoclaw/pull/2841) and opening of [#2842](https://github.com/nanocoai/nanoclaw/pull/2842) (both by foxsky, both addressing extension-point seams) raises questions. Was it a rebase? A retargeting to a different branch? A fresh approach? A brief comment from the author or a maintainer on the rationale would clarify the iteration strategy for the community watching this critical architectural feature.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 24, 2026, based on the provided GitHub snapshot.

---

## 1. Today's Overview

Today's activity on NullClaw is characterized by low volume but focused resolution. One critical bug issue was closed, and a major feature Pull Request received an update, while no new releases were cut. This quiet period suggests the project is in a consolidation phase, prioritizing stability fixes and the gradual integration of a large automation subsystem. The timely closure of a high-frequency crash bug is a net positive for user stability, while the continued work on the cron subagent hierarchy signals a commitment to platform maturity.

## 2. Releases

No new versions of NullClaw were published in the last 24 hours. The project remains on the `v2026.5.29` release. Users experiencing the `NoResponseContent` bug (see section 5) or awaiting new features will need to wait for the next tagged artifact.

## 3. Project Progress

No Pull Requests were formally merged or closed during this period. However, significant progress is visible on a long-running feature branch:

- **PR #783 (Open): feat(cron): cron subagent, run history, JSON output, security hardening**
  - *Author:* yanggf8
  - *Link:* [PR #783](https://github.com/nullclaw/nullclaw/pull/783)
  - This substantial PR introduces a DB-backed cron scheduler, agent/skill/shell job types, structured JSON output, and operator alerting. Updated on June 23rd, it remains in active development and review.

## 4. Community Hot Topics

Community discussion this cycle is minimal, centering entirely on a single critical bug:

- **Issue #967 (CLOSED): [bug] error: NoResponseContent**
  - *Author:* svier0
  - *Comments:* 2
  - *Link:* [Issue #967](https://github.com/nullclaw/nullclaw/issues/967)
  - This is the most active discussion thread. The user reported a systematic crash rendering the agent nonfunctional on Windows. The closure of this issue implies maintainers acknowledged the severity and addressed it rapidly.
- **PR #783 (Open): feat(cron)**
  - While low on direct comments, the scope of this PR makes it a hot topic for developers and advanced users interested in automation and operational features.

## 5. Bugs & Stability

- **Severity: Critical (Resolved)**
  - **Issue:** `error: NoResponseContent`
  - **Link:** [Issue #967](https://github.com/nullclaw/nullclaw/issues/967)
  - **Affected Config:** Windows 11, `v2026.5.29`, `Agnes-2.0-Flash` model.
  - **Impact:** The agent failed entirely in >50% of attempts (12 failures out of 21 test dialogues), rendering the application effectively unusable with this specific model.
  - **Status:** **CLOSED**. The ticket was created on June 20th and closed by June 23rd. This resolution is a strong positive indicator of maintainer responsiveness to severe regressions, preventing further downstream user impact.

## 6. Feature Requests & Roadmap Signals

No new feature requests were filed in the tracking period. The primary roadmap signal remains the maturation of the **cron subagent engine** in PR #783. The feature set bundled there points to a roadmap increasingly prioritizing:
- **Automation & Trust:** Scheduled agent tasks, run history, and operator alerts.
- **Integration:** Structured JSON output for scripting and external consumption.
- **Security:** Hardening the subagent execution environment.

## 7. User Feedback Summary

The main voice of the user base in this window is a report of significant dissatisfaction, though it was promptly addressed:

- **Pain Point:** User `svier0` encountered a severe reliability issue on Windows 11 with the `v2026.5.29` release. The `Agnes-2.0-Flash` model proved highly unstable (>50% failure rate) with the native build.
- **Satisfaction:** Initially low for affected users, but the closure of the ticket is a strong signal that the feedback loop is working. Users on other platforms or models appear to have a stable experience based on the lack of additional crash reports in this snapshot.

## 8. Backlog Watch

- **PR #783 – The Long-Running Feature Branch**
  - *Link:* [PR #783](https://github.com/nullclaw/nullclaw/pull/783)
  - *Status:* Open since **2026-04-07** (~78 days).
  - *Risk:* **High.** This PR has been open for over two months without merge. It encompasses numerous subsystems (DB migrations, queuing engine, CLI output, security hardening). The risk of bit rot and merge conflicts increases significantly the longer it lingers. Maintainer attention is required to either accelerate this review/merge process or split it into smaller, more manageable atomic PRs to keep development velocity high.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-24

## 1. Today's Overview
Activity on the IronClaw project remained very intense on June 23–24, 2026, with 40 Pull Requests updated and 22 Issues active across the repository. The development focus is heavily concentrated on the "Reborn" architecture, with several major feature branches—userland memory, skill-learning governance, and context window optimization—in active review. No new releases were published, suggesting the team is consolidating sprint work before a shipment. While feature velocity is high, the project is carrying significant stability debt, including a critical scheduler deadlock, persistent CI flakiness blocking the merge queue, and a month-old Nightly E2E failure that remains unresolved.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Nineteen Pull Requests were merged or closed today, advancing several key areas:

- **Slack Integration Overhaul:** A series of PRs by `serrrfirat` moved Slack setup entirely into the WebUI ([#5152](nearai/ironclaw PR #5152)), restored Slack routine outbound targets ([#5164](nearai/ironclaw PR #5164)), and wired dynamic Slack delivery for triggered runs ([#5166](nearai/ironclaw PR #5166)). This represents a major migration from legacy TOML configuration to a dynamic, user-facing setup flow.
- **Google Workspace Auth Stability:** The structured `auth_required` fix for Google API 401 responses in WASM tools was merged ([#4969](nearai/ironclaw PR #4969)), directly improving error recovery for expired/invalid Drive, Docs, Sheets, and Slides tokens.
- **Automation Management:** WebUI-based deletion of Reborn automations was shipped ([#5133](nearai/ironclaw PR #5133)), filling out the CRUD surface for the native trigger system.
- **API Correctness:** Initial corrections to Reborn GitHub API request shapes were merged ([#5168](nearai/ironclaw PR #5168)), laying groundwork for the broader GitHub PAT auth bug fix.
- **Testing Infrastructure:** A new full-path Reborn/Emulate E2E harness for Google Calendar was added ([#5155](nearai/ironclaw PR #5155)), building out the quality assurance toolkit for first-party extensions.

## 4. Community Hot Topics

- **Performance & Architecture Overhaul:** PR [#5149](nearai/ironclaw PR #5149) (Progressive tool disclosure to slash token overhead from ~91 schemas to relevant subsets) and PR [#5145](nearai/ironclaw PR #5145) (Capability activity lifecycle cleanup) are the most actively reviewed core infrastructure items. They directly target the root causes of production latency and WebUI rendering issues (stuck tool lists).
- **Skill-Learning Safety Gate:** PR [#5156](nearai/ironclaw PR #5156) introduces an approval gate and pending-review state for learned skills. This was specifically flagged as a deferred risk in a prior sprint, and its implementation is a critical trust mechanism for the autonomous learning workflow.
- **Memory Restructuring:** The stacked PRs by `BenKurrek` ([#5163](nearai/ironclaw PR #5163), [#5165](nearai/ironclaw PR #5165)), which lift memory out of the kernel into a provider-neutral contract, are the largest architectural changes in the pipeline. They promise significant modularity benefits but require careful cross-team review.
- **Dogfooding Feedback Loop:** Core contributor `think-in-universe` filed several high-signal UX findings from internal testing, most notably that the "Always approve" feature is broken for specific capability gates ([#5129](nearai/ironclaw Issue #5129)), and that the Inference section is missing from Settings on Railway hosting ([#5157](nearai/ironclaw Issue #5157)).

## 5. Bugs & Stability

- **[Critical] Turn Scheduler Self-Deadlock ([#5148](nearai/ironclaw Issue #5148)):** A concurrency bug where a scheduler heartbeat fires while a running turn holds an async store lock, causing a permanent hang. No fix PR is linked yet.
- **[Critical] Prompt Safety False Positive ([#5169](nearai/ironclaw Issue #5169)):** Bundled skill instructions containing vocabulary like "Bearer" and "access token" trigger the vocabulary denylist, causing completely benign requests to fail with a misleading "temporary system issue" error. This is a full dead-end for users on a clean setup.
- **[Critical] Subagent Spawn Failure ([#5170](nearai/ironclaw PR #5170)):** Model handoffs and subagent spawns are failing under specific conditions. A fix PR is open and under review.
- **[Critical] Claude Automation Failure ([#5151](nearai/ironclaw Issue #5151)):** Reborn fails to correctly handle `anthropic/claude-sonnet-4.5`'s tool selection for creating automations, causing the model to default to irrelevant tools.
- **[Medium] Persistent CI Failure:** The Nightly E2E pipeline ([#4108](nearai/ironclaw Issue #4108)) remains broken since May 27. A flaky test (`trigger_poller_does_not_submit_turn_for_unpaired_actor`, [#5147](nearai/ironclaw Issue #5147)) is actively blocking the merge queue, kicking PRs out of the queue.
- **[Medium] Google Calendar Data Integrity ([#4640](nearai/ironclaw Issue #4640)):** The flagship `list_events` tool returns events in the wrong order (oldest first, missing `orderBy`/`timeMin` defaults), rendering the "upcoming meetings" use case non-functional.
- **[Low] Gmail Auth UI Inconsistencies ([#3732](nearai/ironclaw Issue #3732), [#3733](nearai/ironclaw Issue #3733)):** Inconsistent auth gates and false "success" toasts for invalid tokens remain unresolved for over a month.

## 6. Features & Roadmap Signals

- **Pluggable Memory (Imminent):** PR [#5163](nearai/ironclaw PR #5163) is poised to finalize the extraction of memory into a provider-neutral contract, a major step toward modular extensibility.
- **Approval and Permissions Rebuild (Imminent):** The convergence of PR [#5068](nearai/ironclaw PR #5068) (Global tool permissions), PR [#5156](nearai/ironclaw PR #5156) (Skill learning gates), and the dogfooding bug [#5129](nearai/ironclaw Issue #5129) (Always approve fix) strongly signals a complete overhaul of the authorization UX is on the immediate horizon.
- **Context Window Optimization (Imminent):** PR [#5149](nearai/ironclaw PR #5149) is a direct response to NEAR AI's API timeouts (re-sending ~91 tool schemas per call). It is likely a high-priority merge to improve model response reliability.
- **Build Pipeline Hygiene (Signaled):** Issue [#5167](nearai/ironclaw Issue #5167) ("Stop tracking `dist` in git") indicates a push towards modern CI/CD practices with build artifacts generated at release time rather than committed.
- **Enterprise Integration (Continuing Priority):** The intense activity on Slack and Google Workspace confirms that first-party productivity integrations remain a core strategic investment for the Reborn platform.

## 7. User Feedback Summary

- **Safety Overreach Erodes Trust:** The most damaging user-facing issue is the prompt-safety false positive ([#5169](nearai/ironclaw Issue #5169)), where the system rejects benign requests and blames "temporary system issues". This directly sabotages first-time user experience on a clean setup.
- **Model Compatibility Gap:** Users of Claude are experiencing broken workflow creation ([#5151](nearai/ironclaw Issue #5151)), while the overall benchmark suite reveals high failure rates on DeepSeek models ([#5173](nearai/ironclaw Issue #5173)). This indicates a remaining model-agnostic orchestration gap in Reborn.
- **Core Integration Weakness:** The broken Calendar ordering ([#4640](nearai/ironclaw Issue #4640)) and confusing Gmail auth process ([#3733](nearai/ironclaw Issue #3733)) undermine confidence in the flagship Google Workspace integration, a key value proposition for productivity users.
- **Power User Needs:** The intense activity around "Always approve" and tool permissions ([#5129](nearai/ironclaw Issue #5129), [#5068](nearai/ironclaw PR #5068)) signals that advanced users find the current per-action approval model friction-heavy and need more efficient workflow controls.

## 8. Backlog Watch

- **[Month-old] Gmail Auth UI Bugs ([#3732](nearai/ironclaw Issue #3732), [#3733](nearai/ironclaw Issue #3733)):** Open since May 17, 2026. These significant UX regressions for Gmail authentication have no linked fix PRs. They represent a critical path liability for the reliability of the Gmail integration.
- **[Month-old] Nightly E2E Failure ([#4108](nearai/ironclaw Issue #4108)):** Open since May 27, 2026. A nightly CI failure persisting for nearly a month without a fix is a significant project health risk, signaling deep integration or configuration issues.
- **[Two-week-old] Google Calendar Ordering ([#4640](nearai/ironclaw Issue #4640)):** Open since June 9, 2026. This functional bug makes a flagship feature ("what are my upcoming meetings?") harmful rather than useful. No linked PR has been opened.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-24

## 1. Today's Overview
The project is experiencing a surge in development activity, with **11 Pull Requests updated in the last 24 hours**, 5 of which were merged or closed. The focus of internal development is heavily concentrated on stabilizing the **OpenClaw gateway** and enhancing the **Cowork collaborative agent** features. While this internal velocity is robust, a **critical, unaddressed community regression bug** (Issue #1400) continues to pose a significant risk to user trust. No new releases accompanied today's activity, suggesting the team is consolidating fixes for an upcoming patch.

---

## 2. Releases
None.

---

## 3. Project Progress
The team merged several significant PRs today, advancing stability and core UX:

- **Persistent Cowork Plan Mode** ([PR #2192 – Merged](https://github.com/netease-youdao/LobsterAI/pull/2192)): Adds a persistent plan confirmation flow. Plan Mode remains active per draft/session until the user explicitly confirms or adjusts execution. A major UX enhancement for multi-step agent workflows.
- **OpenClaw Stabilization (3 PRs by btc69m979y-dotcom):**
  - [PR #2189](https://github.com/netease-youdao/LobsterAI/pull/2189): Migrates legacy cron storage automatically on startup.
  - [PR #2190](https://github.com/netease-youdao/LobsterAI/pull/2190): Fixes run-scoped cron session key management for the OpenClaw gateway.
  - [PR #2191](https://github.com/netease-youdao/LobsterAI/pull/2191): Distinguishes startup, loading, ready, and error states in scheduled tasks, refreshing data immediately after gateway handshake.
- **Internal Infrastructure** ([PR #2188 – Merged](https://github.com/netease-youdao/LobsterAI/pull/2188)): Closed by liuzhq1986, likely supporting the new Cowork logging and runtime record infrastructure.

---

## 4. Community Hot Topics

- **Most Active Issue – Critical Regression** ([Issue #1400](https://github.com/netease-youdao/LobsterAI/issues/1400)):
  6 comments, 0 reactions. User reports an **infinite restart loop** after upgrading from v3.30 to v4.1, rendering the application completely unusable. A secondary bug prohibits custom Qwen 3.5 endpoints due to a rigid `web-extractor`/`web-search` dependency chain. The user provided personal contact (email/WeChat), indicating high frustration and urgency.

- **Aging Community Contributions (Stale):**
  A backlog of high-quality community PRs is waiting for maintainer review:
  - [PR #1404](https://github.com/netease-youdao/LobsterAI/pull/1404): Detailed UI mockups for replacing native HTML time/select elements in the scheduled task creator.
  - [PR #1401](https://github.com/netease-youdao/LobsterAI/pull/1401): Security fix for predictable SSE request IDs via `crypto.randomUUID()`.
  - [PR #1402](https://github.com/netease-youdao/LobsterAI/pull/1402): Fix for multi-select file attachment only retaining the last file.
  - [PR #1403](https://github.com/netease-youdao/LobsterAI/pull/1403): i18n fix for a missing `delete` translation key.

---

## 5. Bugs & Stability

| Severity | Item | Status | Details |
|---|---|---|---|
| **CRITICAL** | Issue #1400 – 4.1 upgrade crash | **Unresolved** | Gateway infinite restart loop. Custom LLM config blocked by rigid dependency chain. No maintainer response yet. |
| **MEDIUM** | OpenClaw legacy migration | **Fixed** ([#2189](https://github.com/netease-youdao/LobsterAI/pull/2189)) | Automatic migration of legacy cron storage prevents data loss. |
| **MEDIUM** | OpenClaw cron session handling | **Fixed** ([#2190](https://github.com/netease-youdao/LobsterAI/pull/2190)) | Normalizes run-scoped session keys for stable cowork sessions. |
| **MEDIUM** | Scheduled task state clarity | **Fixed** ([#2191](https://github.com/netease-youdao/LobsterAI/pull/2191)) | Distinguishes loading/ready/error states in task and history tabs. |
| **LOW** | Stale Community PRs (#1401, #1402, #1403, #1406) | **Awaiting Review** | Security, data loss, i18n, and dropdown bugs have fix PRs stalled since April. |

---

## 6. Feature Requests & Roadmap Signals

- **LiteLLM Gateway Provider** ([PR #2193 – Open](https://github.com/netease-youdao/LobsterAI/pull/2193)): Strong roadmap signal. Allows users to route through a LiteLLM proxy for 100+ LLM providers via an OpenAI-compatible endpoint. No new dependencies required. High impact feature if merged.
- **Cowork Interaction Flow** ([PR #2192 – Merged](https://github.com/netease-youdao/LobsterAI/pull/2192)): The roadmap for Cowork clearly points toward complex, multi-step plan/confirm/execute interaction loops, moving beyond simple chat.
- **Scheduled Task UI Polish** ([PR #1404 – Open/Stale](https://github.com/netease-youdao/LobsterAI/pull/1404)): Community-driven demand for a native Electron UI overhaul of the cron scheduler, moving away from OS-rendered `<select>` and `<input type="time">` elements.

**Prediction for next release:** LiteLLM integration, Cowork persistent plan flows, and the OpenClaw cron stabilization fixes.

---

## 7. User Feedback Summary

- **High Dissatisfaction – Upgrade Stability:** The dominant user feedback is the severe, application-breaking regression introduced in v4.1 (Issue #1400). This is a critical trust deficit for the project's release pipeline.
- **Frustration with Dependency Rigidity:** The hard coupling between custom LLM configuration and internal modules (`web-extractor` requiring `web-search`) limits advanced user flexibility and is a recurring pain point.
- **Positive Community Investment:** Despite critical bugs, the project retains a dedicated community. The detailed mockups in PR #1404 and the security-conscious contribution in PR #1401 demonstrate a high level of technical investment from external contributors.

---

## 8. Backlog Watch

Items requiring immediate maintainer attention, ranked by impact:

1. **[Issue #1400 – Dormant Critical Bug](https://github.com/netease-youdao/LobsterAI/issues/1400):** Opened April 3rd. No official triage or workaround. **This is the single biggest risk to project reputation and user retention.**
2. **[PR #1401 – Security Patch](https://github.com/netease-youdao/LobsterAI/pull/1401):** A cryptography fix using `crypto.randomUUID()` over `Math.random()`. Stalled for 2.5 months. Should be reviewed promptly as a security best practice.
3. **[PR #1402 – Data Loss Bug Fix](https://github.com/netease-youdao/LobsterAI/pull/1402):** Fix for multi-file attachment only keeping the last selected file. Stalled for 2.5 months. Directly impacts daily user workflows in Cowork.
4. **[PR #1406 – UI Regression Fix](https://github.com/netease-youdao/LobsterAI/pull/1406):** Fix for empty notification channel dropdown when IM settings exist. Stalled since April.

**Recommendation:** A dedicated "community contribution sprint" is strongly advised to clear these high-quality, time-sensitive PRs before they diverge significantly from the codebase.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-24

## Today’s Overview
The Moltis project experienced a quiet development day, with no new issues or releases reported. One pull request (#215) was closed after merging a feature that adds a `send_image` tool for delivering local images to channel targets, reflecting continued incremental enhancement of the skill tool ecosystem. No bug reports or community discussions were recorded, indicating a period of low overall activity on the repository.

## Releases
*None*

## Project Progress
One pull request was merged (or closed) in the last 24 hours:

- **[#215 – feat(tools): add send_image tool for channel image delivery](https://github.com/moltis-org/moltis/pull/215)** — Authored by `maximilize`. This PR introduces a `send_image` tool that allows skills to send local image files (PNG, JPEG, GIF, WebP) to supported channel targets, such as Telegram. It reuses the existing screenshot pipeline and supports an optional `caption` parameter. The change advances the project’s capacity for media‑rich interactions within skill workflows.

## Community Hot Topics
No issues or pull requests generated meaningful discussion during this period. The only active item (#215) was closed without comments or reactions, suggesting limited community engagement in the current window.

## Bugs & Stability
No bug reports or stability issues were filed or addressed today.

## Feature Requests & Roadmap Signals
No user‑generated feature requests were recorded today. The introduction of the `send_image` tool may reflect an underlying demand for broader channel image support and could signal future work on additional media‑handling capabilities in skill tools.

## User Feedback Summary
No explicit user feedback (comments, reactions, or use‑case descriptions) was present in the project’s GitHub activity for this date.

## Backlog Watch
The project currently has no open issues or pull requests requiring maintainer attention. The backlog remains clear, with no long‑unanswered items outstanding.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

### CoPaw Project Digest: 2026-06-24
**Project:** QwenPaw (CoPaw Repository)

---

### 1. Today's Overview

QwenPaw saw exceptionally high development velocity on 2026-06-24, with **36 issues** updated and **50 pull requests** active (24 merged/closed). A new patch release (`v1.1.12.post2`) shipped mid-day with minor frontend and session fixes. A massive wave of mobile adaptation PRs for the Console UI dominated contributions, signaling a clear roadmap priority. Meanwhile, a cluster of high-priority Cron scheduling bugs appears to have been fully resolved, restoring trust in autonomous task execution. Overall project health is strong, reflected in rapid issue triage and aggressive feature development, though user feedback highlights persistent friction around configuration persistence and model provider flexibility.

---

### 2. Releases

**`v1.1.12.post2`**
- **Changes:**
  - `fix: navigate to new chat after deleting the current session` (PR [#5376](https://github.com/agentscope-ai/QwenPaw/pull/5376))
  - `feat(console, chat): enhance file preview to support relative path` (PR [#5377](https://github.com/agentscope-ai/QwenPaw/pull/5377))
  - Additional unnamed `fix(q...)` patch
- **Migration Notes:** None. Standard patch release recommended for users experiencing session navigation issues.

---

### 3. Project Progress

**Merged/Closed PRs (24 total):**

- **Core / Memory Refactor:** PR [#5450](https://github.com/agentscope-ai/QwenPaw/pull/5450) (`+702/-602`) restructured auto-memory lifecycle and hardened the `/compact` command — a significant internal improvement.
- **Mobile Adaptation Sprint:** Multiple PRs by @yaozy2020 were merged, adapting Console UI for narrow viewports:
  - **Voice Transcription:** PR [#5470](https://github.com/agentscope-ai/QwenPaw/pull/5470)
  - **Agent Stats:** PR [#5465](https://github.com/agentscope-ai/QwenPaw/pull/5465)
  - (More open PRs in this sprint await review: Skills, Skill Market, Security, etc.)
- **Testing Infrastructure:** PRs [#5437](https://github.com/agentscope-ai/QwenPaw/pull/5437) (`+171` tests) and [#5433](https://github.com/agentscope-ai/QwenPaw/pull/5433) (`+135` tests) added zero-code-change unit tests for Inbox, Settings, and Agent hooks.
- **Bug Fixes:**
  - **MacOS Sandbox:** PR [#5454](https://github.com/agentscope-ai/QwenPaw/pull/5454) fixed a missing closing bracket.
  - **File Upload:** PR [#5467](https://github.com/agentscope-ai/QwenPaw/pull/5467) refactored upload validation.
  - **Cron/Task Reliability:** Multiple high-activity scheduling bugs were closed (Issues [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398), [#5235](https://github.com/agentscope-ai/QwenPaw/issues/5235), [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064), [#5402](https://github.com/agentscope-ai/QwenPaw/issues/5402)), indicating the core scheduling subsystem has been patched this week.

---

### 4. Community Hot Topics

*(Items ranked by comment count / reaction)*

- **Skill Persistence on Upgrade (Issue [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262))** — 12 comments, **open**
  - *Underlying need:* Configuration stability across version upgrades. Users want a "lock/persist" flag for built-in skills. This is a re-open of a previously reported bug (#4807), highlighting a recurring trust issue with the update process.
- **Cron Task Failures (Issues [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064), [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398), [#5235](https://github.com/agentscope-ai/QwenPaw/issues/5235))** — 12 comments, **closed**
  - *Underlying need:* Core promise of an AI assistant is reliable autonomous execution. The failures broke user trust in automation. All resolved in today's sprint, which is a strong positive signal.
- **Custom Provider Function Calling (Issue [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345))** — 6 comments, **open**
  - *Underlying need:* Vendor/model independence. Users adopting non-OpenAI providers (e.g., OMLX) hit a hard wall where agents cannot use tools, severely limiting agentic capability.
- **Thinking Output Not Displayed (Issue [#5416](https://github.com/agentscope-ai/QwenPaw/issues/5416))** — 4 comments, **open**
  - *Underlying need:* Transparency and usability with reasoning models (DeepSeek, Stepfun). Content placed in `thinking`/`reasoning_content` fields results in blank replies.

---

### 5. Bugs & Stability

**High Severity:**
- **(Resolved) Cron Scheduler Halting** — Issue [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398). Job dispatching stopped for active agents. Closed today with fix patches.
- **(Active) Shell Command Parsing** — Issue [#5373](https://github.com/agentscope-ai/QwenPaw/issues/5373). `execute_shell_command` fails on pipes, redirects, and standard shell syntax. Blocks developer use cases.
- **(Active) Console Frontend Crash** — Issue [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401). Sessions with heavy tool-use history white-screen the UI due to unhandled `type: "data"` content blocks.
- **(Active) Agent Identity Mismatch** — Issue [#5456](https://github.com/agentscope-ai/QwenPaw/issues/5456) (2.0 beta). Multi-agent context can incorrectly use agent ID `default` due to a missing field in `AgentRequest`.

**Medium Severity:**
- **(Active) Thinking Content Lost** — Issue [#5416](https://github.com/agentscope-ai/QwenPaw/issues/5416). Reasoning model output invisible to users.
- **(Active) Internal Server Error on Install** — Issue [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379). Startup crash on Windows (`get_remote_addr`).
- **(Active) Python Not Found in Tauri** — Issue [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317). Blocks custom Python skills on Windows Tauri client.
- **(Active) Agent Thinking Freeze (DeepSeek)** — Issue [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328). Agent hangs during thinking requiring manual restart.

**Low Severity / Annoyances:**
- **Memory Usage** — Issue [#5441](https://github.com/agentscope-ai/QwenPaw/issues/5441). 1.4GB RAM on fresh start.
- **Python 3.13 / imghdr** — Issue [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166). Plugin installation fails.
- **Browser Autofill Hijack** — Issue [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403). Search input treated as password field.

---

### 6. Feature Requests & Roadmap Signals

- **Primary Signal: Mobile Console is the Focus.** The sheer volume of open/merged mobile adaptation PRs this week (#5451, #5452, #5458, #5459, #5462, #5463, #5464, #5470) strongly indicates that a responsive WebUI is the top roadmap priority. Issue [#4635](https://github.com/agentscope-ai/QwenPaw/issues/4635) (Mobile QwenPaw client) was closed as a corollary.
- **Drag-and-Drop File Upload (Landed):** Requested in Issue [#5420](https://github.com/agentscope-ai/QwenPaw/issues/5420) and immediately implemented in PR [#5436](https://github.com/agentscope-ai/QwenPaw/pull/5436) — a fast turnaround.
- **Plugin Middleware Architecture (In Review):** PR [#5221](https://github.com/agentscope-ai/QwenPaw/pull/5221) adds formal plugin-based middleware registration, enabling plugins to inject custom logic into the agent reasoning loop. This could be a major architectural shift for `v1.2.0`.
- **Memory Search Ranking:** Issue [#5316](https://github.com/agentscope-ai/QwenPaw/issues/5316) requests recency-aware ranking. Given the parallel memory refactor, this is likely on the shortlist.
- **Broader Model Support:** Requests for Kimi Coding Plan (Issue [#5427](https://github.com/agentscope-ai/QwenPaw/issues/5427)) and KaTeX rendering (Issue [#5453](https://github.com/agentscope-ai/QwenPaw/issues/5453)) signal a desire for deeper mathematical/scientific and model ecosystem compatibility.

---

### 7. User Feedback Summary

**Satisfaction Drivers:**
- Rapid iteration and fix velocity. Users reporting cron/scheduling failures saw issues closed within the same week.
- Responsive feature implementation (e.g., drag-and-drop file upload).

**Key Pain Points:**
- **Configuration Persistence:** The skill re-enabling bug on upgrade (#5262) creates recurring friction and erodes trust in updates.
- **Scheduling Trust:** The cron reliability issues, while fixed, highlighted a core feature fragility that impacted power users relying on autonomous agents.
- **Model Flexibility Limits:** Users of non-OpenAI providers (OMLX, Kimi) feel locked out of core agentic features like tool calling. The missing thinking field rendering (#5416) also impacts users of popular reasoning models.
- **Performance:** High baseline RAM usage (1.4GB idle) was explicitly called out by users as a problem for a locally-running assistant.

---

### 8. Backlog Watch

*High-community-interest items needing maintainer attention.*

- [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262): **Skill Persistence Bug** — Open for 7 days. Recurring issue, 12 comments. Needs robust config save/restore logic.
- [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345): **Custom Provider Function Calling** — Open for 4 days. Blocks a growing user segment.
- [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166): **Python 3.13 / imghdr** — Open since June 12. Blocks plugin installation on newest Python.
- [#5111](https://github.com/agentscope-ai/QwenPaw/pull/5111): **DingTalk Custom Endpoint PR** — Open for 14 days. Enterprise users needing private deployment await merge.
- [#5059](https://github.com/agentscope-ai/QwenPaw/pull/5059): **Matrix Encrypted Media PR** — Open for 15 days. Long-standing bug fix pending review.
- [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995): **Enhanced Memory Management** — Open since May 1. A detailed feature request with no maintainer engagement for over 3 weeks.
- [#5221](https://github.com/agentscope-ai/QwenPaw/pull/5221): **Plugin Middleware PR** — Complex architectural change awaiting review.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the structured project digest for ZeroClaw based on the activity data from June 23–24, 2026.

---

## ZeroClaw Project Digest — 2026-06-24

### 1. Today's Overview

ZeroClaw saw exceptionally high activity today with **44 issues** and **50 pull requests** updated, indicating a highly engaged maintainer team and community pushing hard toward the **v0.9.0 milestone**. **18 issues were closed** and **2 critical PRs were merged**, including the long-awaited fix for the Windows self-update pipeline and a resolution to the repeated shell approval loop bug. The overall project health is strong, though two S1 workflow-blocking bugs remain blocked pending architectural decisions. The development narrative today is dominated by **security hardening** (WASM plugin isolation, supply chain SLSA, dependency policy) and **maturation of user-facing surfaces** (unified command registries, streaming, upgrade flows).

### 2. Releases

No new releases were published in the last 24 hours.

### 3. Project Progress

**Merged/Closed PRs:**
- **`[PR #7853]`** (Closed): Fixes the Windows self-update pipeline. Previously, `swap_binary` used remove-then-copy, which failed silently on locked Windows process images. The PR hardens the entire update pipeline for that platform.
- **`[PR #7901]`** (Closed): Adds a turn-local guard to bound repeated identical shell tool-call requests, preventing the runtime from flooding the operator with approval prompts for commands like `pwd`.

**Key Closed Issues (Features & Fixes):**
- **`[Issue #8193]`** (S1): MCP tools discovered by the gateway are now correctly passed to Zerocode TUI sessions — resolved a workflow-blocking gap.
- **`[Issue #5919]`** / **`[Issue #5918]`**: Closed the critical security triad for WASM host functions (`zc_env_read` allowlist and `zc_http_request` SSRF protection). Plugins can no longer read arbitrary environment variables or reach internal network addresses with the `env_read` / `http_client` permissions.
- **`[Issue #8125]`**: Quickstart now auto-applies the `yolo` risk preset so new users don’t unintentionally restrict themselves.
- **`[Issue #7531]`**: Streaming card message support added for QQ, DingTalk, WeChat, and Feishu channels to reduce perceived latency.
- **`[Issue #8075]`**: Resolved macOS keybinding conflict (`ctrl+up`) and improved ZeroCode default keybindings.

### 4. Community Hot Topics

- **`[RFC #8177]` — Supply Chain Signing and SLSA Provenance** (4 comments): A comprehensive proposal for hardware-backed PGP keys, hermetic builds, and container image signing. This is part of the broader CI hardening push seen across `[#8058]` and `[#8059]`, signaling the community’s strong interest in production-grade operational security.
- **`[RFC #8170]` / `[PR #8173]` — In-App Upgrade from Web Dashboard** (3 comments): Users want to move beyond the static version tag in the sidebar to a full supervised upgrade flow (detect → release notes → apply → restart). The companion PR is already open, suggesting fast movement on this feature.
- **`[RFC #6943]` / `[RFC #8043]` / `[RFC #8187]` — Plugin Architecture Overhaul** (3 comments each): A cluster of RFCs discussing the shift from Extism to native `wasmtime`, crate retirement, and capability-gated hardware host functions. This represents a major architectural discussion currently underway in the community.
- **`[RFC #7929]` — Unified Slash-Command Registries** (2 comments): A recurring pain point where the TUI, Web UI, and channel runtime each have independent hardcoded slash-command maps. The RFC proposes a single gateway-served catalogue.

### 5. Bugs & Stability

**Resolved:**
- **`[Issue #8193]`** (S1 - Workflow Blocked): MCP tools missing in TUI sessions — **Closed**.
- **`[Issue #7820]`** (S2 - Degraded Behavior): Repeated identical shell approval loops — **Fixed by `PR #7901`**.
- **`[Issue #2091]`** (S3 - Minor): Telegram bot API token leaked in poll error logs — **Closed**.
- **`[Issue #7814]`** (S2 - Degraded Behavior): ZeroCode config fields appearing editable before Enter was pressed — **Closed**.

**Open / Active High-Severity Bugs:**
- **`[Issue #8054]`** (S1 - Workflow Blocked / Blocked): System prompt advertises tools that don’t match per-turn effective tools across channels, WebSocket, and `/think` endpoints. The fix for the direct runtime path is complete (`PR #8053`), but the broader alignment across all entry points remains blocked.
- **`[Issue #8151]`** (S1 - Workflow Blocked / Blocked): When a user sends an image in Matrix and the bot delegates it, the image reference is lost in cached history, causing the bot to deny seeing it on a later turn.
- **`[Issue #7800]`** (S2 - Degraded Behavior): ZeroCode help and keybindings remain misleading or unreachable on macOS in certain states.

### 6. Feature Requests & Roadmap Signals

The v0.9.0 tracker **`[Issue #7432]`** remains the central coordination point. Based on active RFCs and open PRs, the following features are likely candidates for the next release:

- **OAuth Login Expansion**: **`[PR #7945]`** adds first-class xAI/Grok OAuth support so users can authenticate without manually copying API keys.
- **Model Context Window UI**: **`[PR #7946]`** introduces a ctx usage bar across the TUI, Gateway agent chat, and CLI interactive mode.
- **Plugin Signature Enforcement**: **`[PR #8172]`** replaces the hardcoded `SignatureMode::Disabled` with configurable trusted-signer policy.
- **Enhanced Provider Support**: **`[PR #8100]`** enables vision for NVIDIA NIM; **`[PR #8207]`** adds OpenRouter `fallback_models` for automatic failover.
- **Autonomous Skill Reflection**: **`[PR #8261]`** adds an opt-in path for the agent to synthesize `SKILL.md` from execution logs.
- **Dedicated Approver Channel**: **`[PR #8231]`** allows tool-approval requests to be routed to a different channel than the one that triggered the run.
- **Telegram Webhook Mode**: **`[Issue #8046]`** proposes an optional webhook ingress as an alternative to long polling.
- **DingTalk Streaming**: **`[Issue #8228]`** requests streaming message support to reduce wait times for long-running completions.

### 7. User Feedback Summary

Real user sentiment driving the current development wave:

- **Security Anxiety** is the top theme. Users with access to plugin environments are deeply concerned about env-var leaks and SSRF. The `env_read` allowlist (`#5919`) and deduplication requests are direct responses to user feedback.
- **Cross-Platform Reliability**: The Windows self-update fix (`#7853`) addresses a major adoption blocker. On the flip side, the request for self-signed SSL support (`#551`) was marked `wontfix`, which may frustrate enterprise/local-deployment users.
- **Latency & Waiting**: Users consistently report dissatisfaction with the “silence” between sending a message and seeing a response. This is driving streaming improvements across Card messages (`#7531`), DingTalk (`#8228`), and general initial response time optimization (`#8142`).
- **Team/Enterprise Needs**: Requests for `session_ttl_hours` to auto-truncate stale history (`#8134`), dedicated approver channels (`#8231`), and per-agent environment variable isolation (`#8226`) indicate growing multi-user and organizational adoption.
- **UI Confusion**: The ZeroCode config editor was directly cited as confusing because fields looked editable before Enter was pressed (`#7814`). The fix was quickly delivered.

### 8. Backlog Watch

Several important items are stalled or awaiting maintainer action:

- **Lost Commit Audit** **`[Issue #6074]`** (p2, In Progress): Tracking 153 commits lost in a single bulk revert from March 2026. This is a significant operational debt item that requires a recovery strategy.
- **Plugin Architecture RFC Triad**: **`[Issue #6943]`** (accepted), **`[Issue #8043]`** (needs-maintainer-review), and **`[Issue #8187]`** (needs-maintainer-review) collectively define the move to native wasmtime, crate retirement, and hardware plugin access. They have been open for several weeks to over a month.
- **Agent Skills Logo Integration** **`[Issue #5262]`** (p2, no-stale): A low-effort marketing task to get ZeroClaw listed on the `agentskills.io` clients page, open since April.
- **Blocked S1 Bugs** **`[Issue #8054]`** and **`[Issue #8151]`** (S1, Blocked): Both are workflow-blocking issues for channels and tool availability that lack a clear path forward without broader architectural changes.
- **Per-Agent Environment Variables** **`[Issue #8226]`** (needs-author-action): This requested feature has stalled pending clarification or revision from the author.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*