# OpenClaw Ecosystem Digest 2026-06-23

> Issues: 259 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-23 02:54 UTC

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

Here is the structured project digest for OpenClaw based on the data provided.

---

## OpenClaw Project Digest – 2026-06-23

### 1. Today's Overview
The OpenClaw project saw extremely high activity in the reporting period, with **259 issues** and **500 pull requests** updated in the last 24 hours. **60 PRs were merged or closed**, demonstrating strong forward momentum despite significant stability headwinds. The project remains in a sprint cadence with the release of `v2026.6.10-beta.2`, which introduces automatic fast mode for conversational turns and more reliable model routing. However, community engagement is heavily dominated by a **Critical (P0) gateway memory leak** and a series of **P1 regressions** from the recent 2026.5.x and 2026.6.x release cycles, indicating a period of intense stabilization.

### 2. Releases
A new beta version was shipped: **`v2026.6.10-beta.2`**. While the full changelog is not exhaustive in the data, the headline features include:
- **Automatic Fast Mode for Talks ([#85104](https://github.com/openclaw/openclaw/issues/85104))**: Short conversational turns can now automatically engage fast mode, returning to normal behavior for longer runs. This is a direct responsiveness improvement for chat interfaces.
- **More Reliable Model Routing**: Backend improvements to Zai (and presumably other providers) to better handle fallback distribution.

*No explicit breaking changes or migration notes were included in the provided summary, though users should expect the usual beta caveats.*

### 3. Project Progress
Major features and fixes that were closed or merged in the last 24 hours:

- **New Autofix Pipeline & Windows Daemon ([PR #68936](https://github.com/openclaw/openclaw/pull/68936))**: Merged. A size XL PR adding a PR review autofix pipeline using the Claude Agent SDK, plus a Windows background daemon for gateway supervision.
- **Per-Channel Model Override ([Issue #53638](https://github.com/openclaw/openclaw/issues/53638))**: Closed (likely merged). Allows users to define specific models for channels, groups, or DMs, bypassing the global default.
- **Telegram Crash Loop Fix ([Issue #93375](https://github.com/openclaw/openclaw/issues/93375))**: Closed. Resolves the silent crash loop where health monitors could not recover polling workers after a transient network timeout.
- **E2EE State Destruction Fix ([Issue #78396](https://github.com/openclaw/openclaw/issues/78396))**: Closed. Fixes a critical Matrix crypto bug where `--force-reset-cross-signing` destroyed encryption state.
- **WebChat Node Exec ([Issue #92141](https://github.com/openclaw/openclaw/issues/92141))**: Closed. WebChat now correctly exposes `host=node exec` for Windows nodes connected via Codex.
- **QMD Windows Path Fix ([Issue #92302](https://github.com/openclaw/openclaw/issues/92302))**: Closed. Fixes the QMD memory backend on Windows systems.
- **Codex UI Regression ([Issue #93041](https://github.com/openclaw/openclaw/issues/93041))**: Closed. The Codex usage/limit interface was restored to the Control UI.
- **Onboarding Loop Fix ([Issue #95765](https://github.com/openclaw/openclaw/issues/95765))**: Closed. External provider plugin installation no longer skips the OAuth/auth flow.

### 4. Community Hot Topics
The most engagement centers on critical architecture and operational stability:

- **Core SQLite Migration ([#88838](https://github.com/openclaw/openclaw/issues/88838) – 34 comments):** This remains the top long-running thread. It tracks the massive effort to move from JSONL to SQLite via an accessor seam (Path 3). The community is heavily invested in the outcome as it promises to solve session-state and message-loss issues.
- **Codex Turn-Completion Regression ([#88312](https://github.com/openclaw/openclaw/issues/88312) – 17 comments, 4👍):** A high-severity regression in 2026.5.27 where the Codex app server stalls mid-turn. Users report downgrading to 2026.5.26 as the only current workaround.
- **Gateway Memory Leak ([#91588](https://github.com/openclaw/openclaw/issues/91588) – 13 comments, P0):** The most critical open issue. RSS growth from 350MB to 15.5GB leading to OOM kills. This is the top infrastructure concern for self-hosters.
- **PostgreSQL Support ([#90370](https://github.com/openclaw/openclaw/issues/90370) – 11 comments, 2👍):** A persistent community demand for replacing SQLite with PostgreSQL for enterprise deployment (resource usage, data isolation, pgvector).
- **Antigravity CLI Backend ([#84527](https://github.com/openclaw/openclaw/issues/84527) – 3 comments, 9👍):** High user demand for migrating from the deprecated Gemini CLI to the new `agy` Antigravity CLI, driven by the Google I/O deprecation deadline.

### 5. Bugs & Stability
The project is currently managing a heavy bug load, with multiple P0 and P1 regressions active:

- **Critical (P0):**
    - **Gateway Memory Leak ([#91588](https://github.com/openclaw/openclaw/issues/91588)):** RSS grows uncontrollably over 2-3 days. Repeated OOM kills. No fix PR yet attached.

- **High Severity (P1 - Active):**
    - **Codex Turn Stall ([#88312](https://github.com/openclaw/openclaw/issues/88312)):** Regression of a previously fixed bug. No fix PR confirmed.
    - **Session Write-Lock Timeouts ([#86538](https://github.com/openclaw/openclaw/issues/86538)):** Blocks subagent delivery lanes. Fix PR linked as open.
    - **Memory Store Relocation ([#95495](https://github.com/openclaw/openclaw/issues/95495)):** 2026.6.9 silently moved the vector store, forcing a full re-embed of 1499 files with zero warning. **Data-loss risk.**
    - **Anthropic Thinking Signature Replay ([#92201](https://github.com/openclaw/openclaw/issues/92201)):** Intermittent signature invalidation when replaying streams.
    - **Isolated Cron Failures ([#91363](https://github.com/openclaw/openclaw/issues/91363), [#92460](https://github.com/openclaw/openclaw/issues/92460)):** High-profile bugs where cron jobs fail at "model-call-started" phase or drop explicit `delivery.channel` config.
    - **Non-Anthropic Tool Call Regression ([#90288](https://github.com/openclaw/openclaw/issues/90288)):** Models outputting `[tool: exec]` as plain text instead of structured blocks.
    - **OAuth & Auth Failures ([#94432](https://github.com/openclaw/openclaw/issues/94432), [#95612](https://github.com/openclaw/openclaw/issues/95612)):** Cloudflare 403 blocking OpenAI/Codex backend, and `cli-backend` returning 401 despite working shell auth.
    - **Subagent Lock Hangs ([#95833](https://github.com/openclaw/openclaw/issues/95833)):** Abort-settle mechanism fails to release `.jsonl.lock`, permanently breaking sessions.
    - **Ollama Streaming Blocked ([#94251](https://github.com/openclaw/openclaw/issues/94251)):** Remote Ollama provider sessions get stuck at `model_call:started`.

- **Medium Severity (P2/P3 - Active):**
    - `web_fetch` ignoring `NO_PROXY` ([#93807](https://github.com/openclaw/openclaw/issues/93807)).
    - exec failing on private-LAN hosts ([#94032](https://github.com/openclaw/openclaw/issues/94032)).
    - macOS app spamming TCC permissions ([#94147](https://github.com/openclaw/openclaw/issues/94147)).

### 6. Feature Requests & Roadmap Signals
- **PostgreSQL as Internal Store ([#90370](https://github.com/openclaw/openclaw/issues/90370)):** Unlikely to land in a point release soon, but the high number of comments signals it is a major pain point for professional users.
- **Antigravity CLI (agy) Integration ([#84527](https://github.com/openclaw/openclaw/issues/84527)):** **Urgent.** Google Gemini CLI is being deprecated. This must land before the June 18, 2026 cutoff mentioned in the community thread. Expect a fast-track PR.
- **ACP Everywhere RFC ([PR #69824](https://github.com/openclaw/openclaw/pull/69824)):** A major architecture proposal to consolidate all LLM launches behind a single ACP runtime seam. Still in RFC review.
- **MCP Apps Support ([PR #69039](https://github.com/openclaw/openclaw/pull/69039)):** A large PR adding MCP UI resource/metadata support. Stalled on "waiting on author".
- **Per-Source Memory Indexing ([#95724](https://github.com/openclaw/openclaw/issues/95724)):** A newly opened feature request to eliminate duplicate vector stores for same-workspace agents. Very likely to get traction given its direct impact on storage efficiency.

### 7. User Feedback Summary
- **Satisfaction:** The new **fast mode for talks** and **model routing** improvements are positive signals. Community praise for contributors like `@alexph-dev` and `@vincentkoc` suggests a healthy contributor ecosystem.
- **Dissatisfaction & Pain Points:**
    - **Regression Fatigue:** Multiple users report downgrading (e.g., 2026.5.26 over 2026.5.27, 2026.6.8 over 2026.6.9) to maintain stability. The silent memory store relocation ([#95495](https://github.com/openclaw/openclaw/issues/95495)) has eroded trust in upgrade safety.
    - **Opaque Failures:** Generic error messages ("Something went wrong", "LLM request failed") without actionable diagnostics frustrate users trying to debug session-state issues.
    - **Self-Hosted Complexity:** Plugin unbundling created a trust gap for self-hosted deployments ([#92516](https://github.com/openclaw/openclaw/issues/92516)). Users struggle with configuration nuances (e.g., channel IDs vs plugin IDs).
    - **Missing Enterprise Features:** The demand for PostgreSQL is rooted in real operational overhead (running dual databases) and feature requirements (vector search).

### 8. Backlog Watch
Several high-value issues and PRs are languishing without maintainer decision or review:

- **Issues Needing Maintainer Product Decision:**
    - [#8299](https://github.com/openclaw/openclaw/issues/8299) (Feb 3) – Config option to suppress sub-agent announce.
    - [#54794](https://github.com/openclaw/openclaw/issues/54794) (Mar 26) – Telegram Inline Query support.
    - [#43564](https://github.com/openclaw/openclaw/issues/43564) (Mar 12) – ACP Session Skill Context Injection.
    - [#78431](https://github.com/openclaw/openclaw/issues/78431) (May 6) – Discord lifecycle status reactions.

- **PRs Stalled in Review/Author Responsiveness:**
    - **#69039 MCP Apps Support** (Apr 19) – Large PR, waiting on author.
    - **#68986 Assistant Output Normalization** (Apr 19) – Large PR, waiting on author.
    - **#60212 Cron Empty Sanitized Replies** (Apr 3) – Large PR, waiting on author.
    - **#69824 ACP Everywhere RFC** (Apr 21) – Requires architectural alignment before merging.
    - **#60048 Memory System Deep Dive Docs** (Apr 3) – Waiting on author, but requested by the community.

*Project Health Verdict:* The project is sprinting hard but is in a **"stabilization crunch"** phase. The number of P1 regressions combined with a P0 memory leak is concerning for production users. The community is resilient and highly active, but maintainer bandwidth for reviewing large, stalled PRs appears to be a bottleneck.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: AI Agent / Personal Assistant

**Date:** 2026-06-23 | **Scope:** Active open-source ecosystem

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is undergoing a critical transition from rapid prototyping to production-grade stabilization. Community data from June 23rd reveals an ecosystem bifurcating between generalist reference platforms and vertically specialized agents, with reliability concerns dominating user sentiment across the board. "Regression fatigue" has emerged as the most significant cross-cutting theme, with multiple projects reporting user downgrades to maintain stability. The Model Context Protocol (MCP) has solidified as the de facto standard for tool interoperability, but scaling issues around stream assembly, duplicate tool IDs, and security bypasses have become universal blockers. Platform expansion—particularly Windows parity and mobile support—remains the second-highest infrastructure demand, while security hardening is rapidly transitioning from nice-to-have to core architectural requirement.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Signal | Maturity Tier |
|---|---|---|---|---|---|
| **OpenClaw** | 259 | 500 | v2026.6.10-beta.2 | Stabilization crunch / P0 leak | Core Reference |
| **Hermes Agent** | 50 | 50 | None | Scaling pains / platform gaps | Rapid Scaling |
| **CoPaw** | 23 | 50 | None | Community hardening / mobile push | High Velocity |
| **ZeroClaw** | 50 | 50 | None | Architecture refinement / bottlenecked | Architectural Pivot |
| **IronClaw** | 16 | 23 | None | Feature churn / critical regression | Aggressive Expansion |
| **NanoBot** | 6 | 30 | v0.2.2 Durability | Focused iteration / strong cadence | Iterative Maturity |
| **PicoClaw** | 3 | 19 | None | Security focus / embedded niche | Niche Velocity |
| **LobsterAI** | 5 | 8 | None | Core momentum / community stagnation | Risk Zone |
| **NanoClaw** | 0 | 6 | None | Community-driven / steady | Moderate |
| **NullClaw** | 0 | 2 | None | Low-intensity / Matrix focus | Maintenance |

*Inactive: TinyClaw, Moltis, ZeptoClaw (no 24h activity)*

---

## 3. OpenClaw's Position

**Advantages:** OpenClaw remains the undisputed reference implementation with a community footprint an order of magnitude larger than peers (259 issues, 500 PRs). Its feature breadth—E2EE Matrix state fix (#78396), per-channel model overrides (#53638), autofix pipelines (#68936), Telegram crash loop resolution (#93375)—sets the baseline for what a full-featured agent should do. The new fast mode for talks (#85104) and improved model routing are direct competitive differentiators for chat UX.

**Technical Approach:** Monolithic gateway architecture with the broadest provider/model support. OpenClaw's design decisions (JSONL-to-SQLite migration #88838, PostgreSQL demand #90370) heavily influence the entire ecosystem's storage architecture debates.

**Community Size Comparison:** OpenClaw attracts the most diverse contributor base and the highest raw volume. However, this brings compounded maintenance costs—P0 memory leak (#91588), P1 regressions across three release cycles (2026.5.x and 2026.6.x), and users explicitly downgrading versions. NanoBot's v0.2.2 "Durability" release contrasts sharply with OpenClaw's regression-heavy cadence, highlighting the core tradeoff between breadth and stability.

**Peer Comparison:**
- *vs NanoBot*: NanoBot is smaller but has cleaner MCP lifecycle management and fewer regressions. OpenClaw serves more use cases but requires more operational discipline.
- *vs Hermes Agent*: Hermes leads in provider autonomy (Vertex AI demand) and memory tiering but lags in channel diversity. OpenClaw has better E2EE and Telegram stability.
- *vs ZeroClaw*: ZeroClaw's Wasm-first approach offers stronger sandboxing; OpenClaw offers faster feature time-to-market.

---

## 4. Shared Technical Focus Areas

### A. Model Context Protocol (MCP) Scaling & Stabilization
- **Projects:** Hermes Agent, NanoBot, ZeroClaw, PicoClaw, OpenClaw
- **Specific Needs:** Duplicate `tool_use` IDs bricking sessions (NanoBot #4443), stream assembly crashes on reconnect (NanoBot #4441), `enabledTools` allowlist bypasses for resources/prompts (NanoBot #4436/#4452), tools unavailable on non-Anthropic/OpenAI paths (ZeroClaw #7756, Hermes #90288). MCP lifecycle management is the single largest reliability gap.

### B. Multi-Platform Parity (Windows / macOS / Linux)
- **Projects:** Hermes Agent, IronClaw, OpenClaw, PicoClaw, CoPaw
- **Specific Needs:** Windows ACP hang (Hermes #50765, IronClaw #5139 regression), macOS file descriptor limits (Hermes #30230), Intel Mac arm64-only DMG (Hermes #37505), Windows QMD path fix (OpenClaw #92302). Cross-platform CI blind spots create recurring regressions.

### C. Durable Session State & Memory Management
- **Projects:** OpenClaw, ZeroClaw, Hermes Agent, CoPaw, IronClaw
- **Specific Needs:** SQLite migration for session state (OpenClaw #88838), context budget overflow on first turn (ZeroClaw #5808), memory tiering to reduce token costs (Hermes #51152), context compaction freezes (CoPaw #5218), session write-lock timeouts (OpenClaw #86538). State loss is the universal pain point.

### D. Security & Auth Hardening
- **Projects:** ZeroClaw, PicoClaw, Hermes Agent, OpenClaw
- **Specific Needs:** CSRF via API auth setup (PicoClaw #3160), exec allowlist bypass (PicoClaw #3161), OAuth/OIDC enterprise auth (Hermes #42448), Discord stale session key leak (Hermes #24100), Cloudflare 403 blocking backends (OpenClaw #94432). The autonomy-to-trust continuum is forcing security to the roadmap top.

### E. Channel Expansion (Telegram, WhatsApp, Mattermost, Slack)
- **Projects:** NanoBot, IronClaw, CoPaw, PicoClaw, OpenClaw, NanoClaw
- **Specific Needs:** Telegram rich messages v10.1 (NanoBot #4413), WhatsApp stability (PicoClaw #3162), Mattermost WebSocket/REST (NanoBot #4459), Slack Socket Mode (CoPaw #5193). Users demand agent access across their existing communication tools.

---

## 5. Differentiation Analysis

| Dimension | Generalist (OpenClaw, CoPaw) | Reliability Specialist (NanoBot) | Innovation R&D (Hermes Agent) | Enterprise/Governance (IronClaw, ZeroClaw) | Embedded/Niche (PicoClaw, NullClaw) |
|---|---|---|---|---|---|
| **Architecture** | Monolithic gateway, broadest providers | Focused MCP core, lightweight | Modular, provider-agnostic | Concurrent engine (IronClaw), Wasm-first (ZeroClaw) | Claw-focused, single-adapter |
| **Target User** | Power users, self-hosters | Bot developers, integrators | Heavy LLM users, researchers | Multi-agent deployments, security teams | Ethical hackers, privacy advocates |
| **Key Weakness** | Regression fatigue, P0 leak | Scaling MCP complexity, limited scope | Platform parity, scaling tech debt | Feature churn breaks stability | Narrow user base, low community |
| **Key Strength** | Breadth of features, community depth | Durability as a feature, fast turnaround | Provider autonomy, experimental velocity | Performance (IronClaw), Sandboxing (ZeroClaw) | Deep domain fit, security hardening |
| **Cadence** | Continuous canary (beta) | Batch milestones ('Durability') | Feature accumulation | Architecture refactors + feature | Batch + niche features |

**Architecture Spectrum:**
- **Monolithic Heavyweight:** OpenClaw, CoPaw
- **Modular / Lightweight:** NanoBot, Hermes Agent
- **Future-Native (Wasm/ Rust):** ZeroClaw
- **Embedded / Specialized:** PicoClaw, NullClaw

---

## 6. Community Momentum & Maturity Tiers

### Tier 1: High-Velocity / Scaling Pains
**OpenClaw, Hermes Agent, CoPaw, ZeroClaw** (50-500 daily PRs/Issues)

These projects attract the most contributors and user bugs. OpenClaw and Hermes are experiencing the classic "success crisis"—high feature velocity undermining stability. ZeroClaw is bottlenecked on review but has closed foundational RFCs indicating maturity. CoPaw is aggressively hardening with a massive test infrastructure buildout (~170 unit tests added in one day).

### Tier 2: Iterative Maturity / Focused Velocity
**NanoBot, IronClaw, PicoClaw** (19-30 daily PRs)

NanoBot's v0.2.2 "Durability" release exemplifies the market's current demand: stability over novelty. IronClaw is the most aggressive in architecture modernization (god-crate decomposition, performance week) but bears the highest churn risk from its concurrent engine merge. PicoClaw punches above its weight on security contributions.

### Tier 3: Risk Zone
**LobsterAI** (8 PRs, 5 issues)

LobsterAI exhibits the most concerning signal in the ecosystem: high internal development velocity (Plan Mode, OpenClaw plugin fixes) paired with zero community maintenance. Five issues and seven PRs have been stale for 80 days. This divergence between core development and community health signals a project at risk of losing external contributors.

### Tier 4: Low Activity / Niche Maintenance
**NanoClaw, NullClaw** (0-6 items)

NullClaw is functionally a single-adapter Matrix bridge with low churn. NanoClaw shows consistent but low community contribution. TinyClaw, Moltis, ZeptoClaw are dormant.

---

## 7. Trend Signals (For AI Agent Developers)

1. **"Boring Is the New Feature":** The ecosystem-wide regression fatigue and explicit user downgrading validate that session durability, memory permanence, and crash recovery are the top competitive differentiators. NanoBot's entire v0.2.2 branding around "Durability" captures this sentiment. Prioritize stable state persistence over new channel integrations.

2. **MCP Hygiene Is the New Integration Tax:** Duplicate tool IDs, stream crashes, and access control bypasses are emerging as universal costs. Invest in MCP lifecycle management (reconnection, deduplication, permission scoping) as a foundational infrastructure layer rather than an afterthought.

3. **Provider Diversification Is Accelerating:** The intense demand for non-OpenAI providers (Google Vertex for Hermes #12639, Kimi for IronClaw #8154, Zhipu for CoPaw #5330, OMLX function calling for CoPaw #5345) signals that LLM lock-in is breaking. Agent frameworks must abstract model differences aggressively.

4. **Desktop Remains Primary, Mobile Is Catching Up:** Despite the mobile push across projects (CoPaw mobile responsiveness, IronClaw WebUI v2), desktop infrastructure issues (DMGs for Intel Macs, Electron updates, Tauri auto-updaters, daemon modes) represent most UI/UX complaints. Desktop is still the battleground; mobile is a trailing indicator.

5. **Security Is Unlocking Autonomy:** The preponderance of fixes for exec allowlist bypasses, CSRF in setup flows, and supply chain signing (ZeroClaw #8177) shows that the bottleneck for autonomous agents is trust. Developers building on these frameworks must embed permission models and sandboxing from the start, not as bolt-on features.

6. **Architecture Simplification Is the Next Wave:** ZeroClaw's Wasm-first pivot, IronClaw's god-crate decomposition, and OpenClaw's SQLite migration all point toward a recognition that current architectures are too complex to maintain. The next 12 months will likely see a push toward smaller, more auditable codebases.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot Project Digest – 2026-06-23**

---

### 1. Today’s Overview
NanoBot is in a period of exceptionally high maintainer velocity. In the past 24 hours, **30 pull requests** and **6 issues** were updated, culminating in the release of **v0.2.2**. This release marks a critical "durability" milestone, heavily reinforcing WebUI transcript handling, forked conversation fidelity, and gateway shutdown semantics. The high ratio of merged/closed PRs (14) to open PRs (16) signals a deliberate push toward a stable baseline for end users. Community health is strong, with **21 new contributors** represented in the current release cycle.

---

### 2. Releases
- **v0.2.2** — *"Durability Release"*
  - **Changes:** Aggregates **140+ merged PRs** focusing on real-world survival.
    - **WebUI:** Transcripts are now segmented per session instead of one fragile file; forked chat replies survive history refreshes; post-send scrolling layout is stabilized ([#4451](https://github.com/HKUDS/nanobot/PR/4451), [#4453](https://github.com/HKUDS/nanobot/PR/4453), [#4455](https://github.com/HKUDS/nanobot/PR/4455)).
    - **Gateway:** `nanobot gateway` now traps `SIGINT`/`SIGTERM` at the boundary layer instead of relying on `asyncio.run()` teardown ([#4454](https://github.com/HKUDS/nanobot/PR/4454)). Cancelled channel tasks no longer cause crash traces ([#4456](https://github.com/HKUDS/nanobot/PR/4456)).
    - **Agent:** Routine cron jobs returning "nothing to report" are correctly suppressed, fixing a regression ([#4412](https://github.com/HKUDS/nanobot/PR/4412)).
  - **Breaking Changes:** None documented. Standard upgrade path.
  - **Migration Notes:** Users experiencing prior cron-notification noise should update to v0.2.2 for the fix.

---

### 3. Project Progress
**Merged/Closed Pull Requests (Today’s Window):**
| Area | Key PRs |
|------|---------|
| **WebUI Stability** | [#4451](https://github.com/HKUDS/nanobot/PR/4451), [#4453](https://github.com/HKUDS/nanobot/PR/4453), [#4454](https://github.com/HKUDS/nanobot/PR/4454), [#4455](https://github.com/HKUDS/nanobot/PR/4455) – layout, forks, scrolling anchored. |
| **Gateway Lifecycle** | [#4454](https://github.com/HKUDS/nanobot/PR/4454), [#4456](https://github.com/HKUDS/nanobot/PR/4456) – shutdown and task cancellation hardening. |
| **Agent Behavior** | [#4412](https://github.com/HKUDS/nanobot/PR/4412) – cron notification suppression. |
| **Documentation** | [#4461](https://github.com/HKUDS/nanobot/PR/4461) – v0.2.2 news entry; [#4462](https://github.com/HKUDS/nanobot/PR/4462) – runtime environment variable reference. |
| **Infrastructure** | [#4460](https://github.com/HKUDS/nanobot/PR/4460) – Node version bumped to 24. |
| **Release Chores** | [#4445](https://github.com/HKUDS/nanobot/PR/4445) – version bump and packaging cleanup. |

**Open / In-Review (Feature Development):**
- **Mattermost channel** ([#4459](https://github.com/HKUDS/nanobot/PR/4459))
- **`search_history` tool** for agent memory recall ([#4439](https://github.com/HKUDS/nanobot/PR/4439))
- **Gateway lifecycle edge-cases** — separate `--enable` / `--start` semantics for `launchd` ([#4447](https://github.com/HKUDS/nanobot/PR/4447))

---

### 4. Community Hot Topics
- **MCP Ecosystem Stability (Highest Signal):** The most active development area revolves around Model Context Protocol robustness. Multiple interlocking PRs are targeting different failure modes:
  - [PR #4441](https://github.com/HKUDS/nanobot/PR/4441): Streamable HTTP generator crashes on reconnect → `RuntimeError`.
  - [PR #4443](https://github.com/HKUDS/nanobot/PR/4443): Duplicate `tool_use` IDs permanently brick sessions.
  - [PR #4436](https://github.com/HKUDS/nanobot/PR/4436) / [#4452](https://github.com/HKUDS/nanobot/PR/4452): `enabledTools` allowlist bypass for resources/prompts.
  - *Analysis:* These are the top remaining stability blockers; their resolution will be the largest single improvement in user confidence.

- **Platform Expansion:**
  - **Mattermost** ([#4459](https://github.com/HKUDS/nanobot/PR/4459)) – a full WebSocket + REST channel. Strong community interest in expanding beyond Telegram/Discord.
  - **PWA Support** ([#4457](https://github.com/HKUDS/nanobot/Issue/4457)) – requested for mobile. The implementing PR ([#4458](https://github.com/HKUDS/nanobot/PR/4458)) carries the `[invalid]` label, suggesting a design dispute or technical veto.
  - **Telegram 10.1 Rich Messages** ([#4413](https://github.com/HKUDS/nanobot/Issue/4413)) – user demand for native Telegram formatting.

- **Mid-Turn User Interruption** ([#4397](https://github.com/HKUDS/nanobot/PR/4397)) – A proposed fix injecting a "hint" message is labeled `[invalid]`, indicating maintainers likely prefer a different architectural approach for tool-chain interruption.

---

### 5. Bugs & Stability
| Severity | Issue / PR | Problem | Status |
|----------|------------|---------|--------|
| **High** | [PR #4443](https://github.com/HKUDS/nanobot/PR/4443) | Duplicate `tool_use` IDs persist into history → permanent HTTP 400 on every turn. Session is bricked. | **Open / Fix proposed** |
| **High** | [PR #4441](https://github.com/HKUDS/nanobot/PR/4441) | MCP `streamable_http` reconnect failure crashes the gateway with a `RuntimeError` cancel-scope mismatch. | **Open / Fix proposed** |
| **High** | [Issue #4410](https://github.com/HKUDS/nanobot/Issue/4410) / [PR #4412](https://github.com/HKUDS/nanobot/PR/4412) | Cron jobs always delivered response despite "don't send" instruction (regression). | **RESOLVED (v0.2.2)** |
| **Medium** | [PR #4436](https://github.com/HKUDS/nanobot/PR/4436) / [#4452](https://github.com/HKUDS/nanobot/PR/4452) | MCP `enabledTools` allowlist not enforced for resources/prompts. | **Open / Fix proposed** |
| **Medium** | [PR #4433](https://github.com/HKUDS/nanobot/PR/4433) | Pairing store type-coercion inconsistency (non-string IDs silently denied). | **Open / Fix proposed** |
| **Low** | [PR #4451](https://github.com/HKUDS/nanobot/PR/4451) | WebUI layout flex-align and scroll anchor jank on fresh turns. | **RESOLVED (v0.2.2)** |
| **Low** | [PR #4455](https://github.com/HKUDS/nanobot/PR/4455) | Fork replies disappearing on history refresh. | **RESOLVED (v0.2.2)** |

---

### 6. Feature Requests & Roadmap Signals
- **Under Development (Likely v0.3.x):**
  - **Mattermost Channel** ([#4459](https://github.com/HKUDS/nanobot/PR/4459)) – WebSocket + REST, real-time messaging, streaming responses.
  - **`search_history` Tool** ([#4439](https://github.com/HKUDS/nanobot/PR/4439)) – read-only memory recall.
  - **Gateway Lifecycle Refinement** ([#4447](https://github.com/HKUDS/nanobot/PR/4447), [#1461](https://github.com/HKUDS/nanobot/Issue/1461)) – evolving toward a unified daemon semantic.
  - **Kimi Coding Plan Support** ([#4463](https://github.com/HKUDS/nanobot/Issue/4463)) – extending platform partnership into paid plans.
- **User-Requested:**
  - **Telegram 10.1 Rich Messages** ([#4413](https://github.com/HKUDS/nanobot/Issue/4413)) – regular expression of desire for platform-native features.
  - **PWA for WebUI** ([#4457](https://github.com/HKUDS/nanobot/Issue/4457)) – mobile home-screen installation, though the implementation approach remains contested.
- **Prediction:** The next minor release will likely feature the Mattermost channel, the `search_history` tool, and the currently open set of MCP stability fixes. The Telegram rich-message and PWA requests may slip if no consensus is reached.

---

### 7. User Feedback Summary
- **Pain Points:**
  - **MCP brittleness:** Users experience "bricked sessions" due to stream assembly errors ([#4443](https://github.com/HKUDS/nanobot/Issue/4443)) and gateway crashes on reconnection ([#4441](https://github.com/HKUDS/nanobot/Issue/4441)).
  - **Regression sensitivity:** The cron notification regression ([#4410](https://github.com/HKUDS/nanobot/Issue/4410)) shows that even well-intended refactors can disrupt core agent behavior, causing noise or unwanted messages.
  - **Onboarding complexity:** Issue [#4376](https://github.com/HKUDS/nanobot/Issue/4376) (closed) confirms the `--wizard` mode remains too technical for non-expert users.
- **Satisfaction Signals:**
  - Users are actively investing in integrations (Mattermost, Kimi), indicating a strong platform mindset.
  - The rapid v0.2.2 release cycle with **140 merged PRs** and quick turnaround on reported regressions demonstrates high maintainer responsiveness.

---

### 8. Backlog Watch
- **Unmerged Blockers (MCP):** Three critical MCP fixes remain unmerged for 2+ days despite being the highest-traffic topic:
  - [PR #4441](https://github.com/HKUDS/nanobot/PR/4441) (reconnect crash)
  - [PR #4443](https://github.com/HKUDS/nanobot/PR/4443) (session bricking)
  - [PR #4436](https://github.com/HKUDS/nanobot/PR/4436) (access control bypass)
  - *These likely missed the v0.2.2 merge window. Their continued openness is the largest risk to user confidence.*

- **Design Conflicts (Lack of Clear Alternatives):**
  - [PR #4397](https://github.com/HKUDS/nanobot/PR/4397) (mid-turn hint) and [PR #4458](https://github.com/HKUDS/nanobot/PR/4458) (PWA) both carry `[invalid]` labels. While maintainers are setting boundaries, no accepted alternative design proposal has been published.

- **Daemon Gateway Architecture (Historical):** Issue [#1461](https://github.com/HKUDS/nanobot/Issue/1461) (unified semantic layer for background daemon) was recently closed. Its long-term goals appear to be decomposed into smaller lifecycle PRs ([#4447](https://github.com/HKUDS/nanobot/PR/4447), [#4456](https://github.com/HKUDS/nanobot/PR/4456)). The community should watch for a concrete tracking issue or RFC covering the remaining scope.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for **June 23, 2026**, based on the latest 24-hour GitHub activity data.

---

## 1. Today’s Overview

Hermes Agent is in a period of intense development velocity and community growth, with 50 issues and 50 pull requests updated over the last day. Maintainers are keeping pace, merging 6 PRs while actively reviewing 44 open contributions. The project is clearly experiencing scaling pains, with the majority of activity concentrated on platform compatibility (macOS, Windows, Linux), integration reliability (Telegram, Discord), and essential infrastructure stability (session management, file descriptors). The high volume of open bugs (46) relative to closed items suggests that while the community is submitting an impressive volume of high-quality fixes, core system robustness remains the central challenge.

## 2. Releases

**None**

No new releases were cut today. The project appears to be in a heavy feature-and-fix accumulation phase on `main`, likely preparing for a v0.18 release given the volume of stability patches currently under review.

## 3. Project Progress

Although the 6 merged PRs are not detailed in the provided data, the issue tracker shows strong project momentum across several key areas:

- **Feature Implementation:** **[Feature] Telegram passive history mode** (#27912) is now **closed** and marked `sweeper:implemented-on-main`, allowing Hermes to read group messages without responding unless a wake word is used.
- **Bug Fixes Advanced:**
    - **Telegram Rich Tables** (#45323) are no longer incorrectly flattened into bullet points by the shared formatter.
    - **`computer_use` Windows support** (#41044) has been closed, expanding the agent’s desktop automation capabilities.
    - **Linux Window Listing** (#51033) was fixed; `list_windows` now returns correct results under X11/AT-SPI.
- **Major Stability Contributions:** Today saw a concentrated wave of new PRs targeting code quality and system resilience:
    - `fix(gateway): add explicit encoding` (#51151) – Prevents `UnicodeDecodeError` on Windows gateways.
    - `fix(agent): use time.monotonic()` (#51144) – Removes NTP-reliant timing in `tool_executor.py`.
    - `fix(agent,gateway): use is_truthy_value` (#51147) – Fixes YAML boolean coercion for quoted config values.
    - `feat(memory): core/extended tiering` (#51152) – Reduces system prompt token costs with `[core]` prefixing.
    - `feat: load project mcp json servers` (#51135) – Opt-in support for industry-standard `.mcp.json` configs.

## 4. Community Hot Topics

The community’s most vocal demand continues to be a **Native Google / Vertex AI Provider**. **Issue #12639** has the highest engagement of any active issue (11 comments, 10 👍), with users extensively detailing workarounds for OpenRouter 402 errors and rate limits. This suggests a significant cohort of heavy users migrating from OpenAI to Gemini.

Other active community discussions:

- **Intel Mac Users Blocked**: **Issue #37505** (7 comments) documents a major platform gap where the Hermes Desktop DMG ships as arm64-only, producing `Bad CPU type in executable` errors on Intel Macs.
- **Telegram Stream Duplication**: **Issue #48648** (4 comments) has users debugging a severe infinite nested reply loop caused by the 4096-char message limit, which exhibits high anxiety for production deployments.
- **ACP Windows Regression**: **Issue #50765** (3 comments) signals user frustration with a `0.16.0 -> 0.17.0` regression where `session/prompt` hangs entirely on Windows.
- **Desktop Customization**: **Issue #37566** (3 comments, 4 👍) shows a segment of users eager for advanced UI customization, specifically a font selector.

## 5. Bugs & Stability

The backlog reveals a tiered stability crisis, with the most severe issues concentrated in the Discord and Telegram gateway layers as well as macOS infrastructure.

**Critical (P1)**
- **Discord Double Dispatch (#51057)**: A single message triggering two agent runs and two responses. **Fix PR #51153 is open** to prevent duplicate processing.
- **state.db Corruption (#30636)**: Persistent SQLite corruption under high load during SIGTERM shutdown. Users report data loss every 48 hours.
- **Discord Command Blocking (#41289)**: The `/model` command blocks the Discord event loop for 120–150 seconds.
- **Discord Command Routing (#24100)**: Approval prompts are routed to the wrong thread due to a stale `os.environ` session key leak.

**High (P2)**
- **macOS FD Limit (#30230)**: Default OS limit of 256 easily exceeded by gateway profiles, causing `OSError: Too many open files`.
- **ACP Windows Hang (#50765)**: `session/prompt` never progresses past the conversation turn log.
- **Session Resume State (#51089)**: In-progress tool loops are lost on restart. **Fix PR #51088 is open**.
- **`write_file` Secret Mangling (#51141)**: The redaction system aggressively corrupts valid Python code containing `os.getenv("SECRET")`.
- **Docker Lazy Dependencies (#51136)**: Lazy-installed packages cannot be installed in the official Docker image.

**Medium (P3)**
- **macOS arm64 DMG (#37505)**: No x86_64 support shipped.
- **Telegram HTTPx Leak (#31599)**: Accumulated half-closed sockets hit the macOS fd limit after ~2 days behind an HTTP proxy.
- **Personality Persistence (#51155)**: Personality cannot be changed mid-session; the setting is stuck in `config.yaml`.
- **Desktop Session Sleep/Reap (#44183)**: WS orphan reap grace (20s) is too short, causing stale sessions after wake.

## 6. Feature Requests & Roadmap Signals

The roadmap is heavily influenced by a push toward **provider autonomy** and **better session/memory hygiene**.

- **Top Priority Signal**: **Native Google/Vertex AI Provider** (#12639) remains the single most requested feature. With OpenRouter stability issues driving this demand, it is the strongest candidate for the next release.
- **Memory/RAG**: **Memory Tiering** (PR #51152) and **Session Persistence** (PR #51088) signal a clear focus on reducing token costs and improving long-running agent reliability.
- **MCP Ecosystem**: **Project `.mcp.json` loading** (Issue #51069, PR #51135) indicates a push for Hermes to fit into standard developer tooling workflows.
- **Desktop & Enterprise Auth**: **OIDC/WebAuthn** (Issue #42448) and **Session-Scoped Reasoning Overrides** (PR #51158) point toward professional/corporate use cases.
- **i18n**: **Telegram Command i18n** (Issue #51046) is requested by a non-English user base, signaling global adoption pressure.

## 7. User Feedback Summary

**Satisfaction Drivers:**
- The community trust in contributors is high; extensive refactoring PRs (e.g., removing bare `assert` statements in PR #51154, swapping `time.time()` for `monotonic()`) are being submitted en masse.
- Responsive patches for recent regressions (#51033 Linux, #45323 Telegram tables) are keeping contributor morale healthy.

**Dissatisfaction / Pain Points:**
- **Reliability Anxiety:** The parallel severity of Telegram duplication loops (#48648) and Discord double-dispatch (#51057) undermines user trust in production-grade message delivery.
- **Platform Parity Frustration:** Intel Mac users (#37505) and Windows users (#50765) are experiencing outright failure-to-launch or hang scenarios, indicating insufficient CI coverage for non-arm64/non-macOS platforms.
- **API Middleman Fatigue:** The passionate engagement on the Vertex AI request (#12639) suggests heavy users are experiencing significant financial and reliability costs from the required OpenRouter routing.

## 8. Backlog Watch

Several high-severity items are languishing without clear maintainer response or assignment, which may impact contributor trust:

- **Issue #12639** (Google/Vertex AI Provider): The #1 community feature request has been open for over 60 days with no official roadmap guidance.
- **Issue #24100** (Discord Thread Route Leak, P1): Open since May 12. A critical security/identity bug in concurrent sessions with no assigned fixer.
- **Issue #30230** / **#30636** / **#31599** (macOS Infrastructure, P1/P2): These three macOS-specific bugs (fd limits, DB corruption, leaked sockets) represent systematic technical debt in the gateway layer and have been open for over a month.
- **Issue #41289** (Discord /model Blocks Loop, P1): An execution-blocking bug in a core platform interface, open since June 7.
- **Issue #50765** (ACP Windows Hang, P2): A clean `0.17.0` regression with no workaround documented, only 1 day old but rapidly accumulating comments.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-23

## 1. Today's Overview
The PicoClaw project is in a high-velocity development cycle, with **19 pull requests** and **3 issues** updated in the last 24 hours. Activity is sharply focused on **security hardening**, **channel stability**, and **experimental platform expansion**. Despite the large volume of merged PRs (7), no formal release was cut today, suggesting the maintainers are accumulating fixes and features for a larger upcoming version. The overall project health is strong, characterized by active external contributions and rapid turn-around on reported bugs.

## 2. Releases
No new releases were published today. The latest available release remains unchanged.

## 3. Project Progress
Seven pull requests were merged or closed in the last 24 hours. Key advancements include:

- **WhatsApp Channel Stability (#3162)** — *Merged.* Adds async message processing, pong keepalives, read deadlines, and exponential backoff reconnection to fix automatic WebSocket disconnections.
- **Spawn Tool Duplicate Fix (#3155)** — *Merged.* Solves Issue #3094 by introducing a `direct_reply` parameter with `SkipInboundTurn` support, preventing duplicate assistant messages when spawn callbacks fire.
- **Skill Search UX (#3152)** — *Merged.* Enhances the `picoclaw skills search` output to display explicit installation instructions for each discovered skill.
- **Defensive Type Assertions (#3053, #3091)** — *Merged.* Added safe `ok` checks in the Evolution API `lockStoreFile` and OpenAI compatibility `native_search` layers to prevent potential nil panics.
- **Dependency Maintenance (#3101, #3105)** — *Merged.* Routine bumps for `vite` (8.0.13 → 8.0.16) and `eslint` (10.2.1 → 10.4.1).

## 4. Community Hot Topics
- **Privacy Protocol Demand (Issue #3093)** — The most active issue, with 3 comments and the only 👍 reaction in the dataset. The user explicitly requests gateways for **SimpleX, Wire, or Tox**. This reflects a growing community desire to move beyond mainstream centralized channels toward fully decentralized, encrypted messaging backends.
- **Agent Automation Pipeline (PR #3118)** — The "Remote Pico WebSocket mode" PR proposes an `--remote ws://...` flag for `picoclaw agent`, enabling programmatic control over WebSocket. This is widely anticipated by developers seeking headless, scriptable agent integration.
- **Mobile Device Control (PR #3157)** — An experimental ADB-backed remote operations tool. The community is rallying around the use case of AI-driven Android device automation (screenshots, taps, UI hierarchy).
- **Token Usage Tracking (PR #3156)** — This PR emitting per-turn LLM token usage on the Pico channel addresses a common pain point for users managing API costs and monitoring consumption.

## 5. Bugs & Stability

### High Severity
- **Task Repetition / Context Loss (Issue #3159)** — *Newly opened.* A core AI loop bug where asking for "French news" after "US news" causes the agent to re-execute the US news task. This indicates a significant state management failure in the conversational context. **No fix PR yet.**
- **Exec Deny Pattern Bypass (PR #3161)** — *Fix open.* A security flaw where a custom allow rule (e.g., `^jq\b`) bypasses all deny patterns entirely, allowing dangerous commands. **Fix PR:** #3161 (open).
- **Auth Setup CSRF Vulnerability (PR #3160)** — *Fix open.* Cross-site requests could mutate the first-run dashboard password store via `POST /api/auth/setup`. **Fix PR:** #3160 (open).

### Medium Severity
- **Volcengine Doubao Tool Call Leak (Issue #3153)** — *Fix open.* The `doubao-seed-2.0-pro` model occasionally returns raw `<seed:tool_call>` XML in `message.content` instead of executing the tool. **Fix PR:** #3154 (open).

### Low Severity / Testing
- **WhatsApp Connection Drops (PR #3162)** — *Merged.* Stale connections caused by missing pong handling / read deadlines are now fixed with exponential backoff reconnection.
- **Windows Sandbox Path Handling (PR #3158)** — *Test PR open.* Adds regression coverage to ensure `sandboxFs.ReadDir` and `sandboxFs.Open` correctly handle OS-specific relative paths from `filepath.Join`.

## 6. Feature Requests & Roadmap Signals
- **Decentralized Communication Backends (Issue #3093)** — The most active feature request. Predict next version will include a formal maintainer response or call for contributors to implement a gateway architecture for SimpleX/Tox/Wire.
- **Android Device Automation (PR #3157)** — Strong candidate for inclusion. The experimental ADB tool provides fixed primitives (screenshots, taps, swipe, text input). Likely to be stable by the next minor release.
- **Remote Agent Mode (PR #3118)** — High-impact architectural change. The `--remote` flag extends the agent surface beyond local TUI/Web. Signals a roadmap shift towards headless/server-mode operation.
- **LLM Cost Observability (PR #3156)** — A clear roadmap signal. Emitting per-turn input/output token counts is a high-value feature for enterprise and power users.
- **Spawn Tool Refinement (PR #3155)** — Just merged. The `SkipInboundTurn` pattern is likely to be applied to other tool callback flows.

## 7. User Feedback Summary
- **Pain Points:**
  - **Context Management Failures:** The task repetition bug (#3159) represents the highest severity user-facing flaw, undermining trust in multi-step workflows.
  - **Model-Specific Fragility:** The Doubao tool call leak (#3153) highlights reliability gaps with non-OpenAI providers.
  - **Channel Reliability:** Prior WhatsApp disconnections (now fixed) and desire for privacy-focused backends (#3093) show infrastructure expectations.
  - **Security Concerns:** Users are actively testing and reporting allow/deny list bypasses and CSRF vulnerabilities.
- **Use Cases:** The ADB PR (#3157) reveals a strong experimentation bent—users are pushing PicoClaw into mobile testing and automation. The Remote WS mode (#3118) targets DevOps pipeline integration.
- **Satisfaction Indicators:** The volume of high-quality external PRs (danmobot, jp39, loafoe) and rapid maintainer merges (7 closed PRs today) signal a healthy, responsive collaborative ecosystem.

## 8. Backlog Watch
- **Issue #3093 (SimpleX/Wire/Tox)** — Open for **13 days**, 3 comments, 1 upvote. No maintainer response. Needs a roadmap decision or a request for community contribution to break the stalemate.
- **PR #3118 (Remote Pico WebSocket Mode)** — Substantial feature branch open since June 12. Updated recently but lacks visible maintainer review comments. At risk of stalling without explicit maintainer guidance.
- **PR #3128, #3131 (Defensive Coding Fixes)** — Both open for over a week. Well-written, low-risk type assertion and body-close fixes. Merging these would reduce friction in the open PR queue.
- **PR #3100, #3103, #3104 (Stale Dependabot PRs)** — Routine frontend dependency bumps (`shadcn`, `typescript-eslint`, `vite-react`) open since June 11. If CI passes, they are safe to batch-merge to stay current.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest | 2026-06-23

*Repository: [github.com/nanocoai/nanoclaw](https://github.com/nanocoai/nanoclaw)*

---

## 1. Today's Overview

NanoClaw shows moderate development activity today, driven entirely by community pull requests updated in the past 24 hours. While no new releases or fresh issues were recorded, the project saw significant movement on 6 PRs, with one major feature (Telegram integration via [PR #2831](https://github.com/nanocoai/nanoclaw/pull/2831)) successfully merged. The development focus remains strongly on expanding agent communication capabilities, with an extensive IMAP/SMTP email integration and an approvals refinement both actively under review. Overall, the project is in a healthy state of iterative feature development and targeted bug fixing, with strong contributions from the community.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest stable release remains v2.1.1, against which the newly merged Telegram integration was explicitly verified.

---

## 3. Project Progress

**One pull request was merged today:**

- **[PR #2831](https://github.com/nanocoai/nanoclaw/pull/2831) (Closed/Merged): feat: add Telegram integration**  
  Authored by @aarchh, this adds Telegram as a full communication channel for the agent. The submitter explicitly confirmed it works on the current stable release (v2.1.1), ensuring a smooth adoption path for existing users. This is a significant milestone for mobile accessibility.

**Active features advancing toward completion (all updated in the last 24h):**

- **[PR #1235](https://github.com/nanocoai/nanoclaw/pull/1235): IMAP/SMTP Email Integration** — The largest open feature. Adds email as both a channel (inbox polling) and a toolset (reading, composing, managing email) with 6 MCP tools exposed. Updated yesterday after a sustained development period.
- **[PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832): Reject with Reason for Approvals** — Enhances the module approval workflow by allowing human approvers to attach a one-line explanation when declining an agent's request, which is then relayed back to the agent.
- **[PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795): CLI-Derived Dashboard Skill** — Adds a read-only skill providing system observability directly through the CLI, targeting power users who want insight without external dashboards.

---

## 4. Community Hot Topics

No new Issues were created in the last 24 hours, and direct comment counts were not available in this data window. However, the PR activity clearly reveals the community's leading interests:

- **[PR #1235 — IMAP/SMTP Email Integration](https://github.com/nanocoai/nanoclaw/pull/1235)**  
  *Opened March 18 · Updated June 22*  
  This remains the defining community feature request. It represents the deepest integration of the current slate, merging channel & toolset paradigms. The fact it was updated as recently as yesterday signals the author is pushing hard toward completion. This is likely the most-anticipated feature by the broader user base.

- **[PR #2831 — Telegram Integration](https://github.com/nanocoai/nanoclaw/pull/2831)**  
  *Created and Merged June 22*  
  The rapid lifecycle of this PR—authored, reviewed, and merged within a single 24-hour window—suggests strong demand for mobile-accessible, real-time messaging backends. The Telegram channel will likely see heavy adoption.

- **[PR #2832 — Reject with Reason](https://github.com/nanocoai/nanoclaw/pull/2832)**  
  *Created June 22*  
  This UX-focused feature addresses a subtle but important gap: the inability for an approver to give an agent context on *why* a request was declined. The underlying need is richer, more transparent human-agent collaboration loops.

---

## 5. Bugs & Stability

Two bug fixes are currently under active review:

- **High Severity: [PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830) — Reap dead peer service registrations**  
  Authored by @amit-shafnir. Addresses a systemic resource leak where deleting a NanoClaw installation without first running its uninstaller leaves orphaned `launchd` plists (macOS) or `systemd` units (Linux). These accumulate over time, causing the OS to continuously attempt launching a non-existent binary. One test system had 6 such orphaned registrations. The fix adds logic to detect and clean up these dead entries automatically. This is a significant reliability improvement for long-running or heavily-tested environments.

- **Medium Severity: [PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531) — Suppress duplicate text in poll loop**  
  Authored by @cfis. Fixes a bug where a `send_message` event firing during an agent's turn causes text duplication in polling-based channels. This impacts conversational flow and user experience. The fix targets the polling loop logic to deduplicate output.

No critical crashes or regressions were reported in this window.

---

## 6. Feature Requests & Roadmap Signals

The current PR slate strongly signals the roadmap direction:

- **Near-term flagship feature:** The IMAP/SMTP email integration ([PR #1235](https://github.com/nanocoai/nanoclaw/pull/1235)) will anchor the next major release. Its combination of channel and toolset modes represents a significant expansion of the agent's operating domain.

- **Immediate UX polish:** The "Reject with Reason" feature ([PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832)) is scoped and focused. It addresses a clear gap in the current approvals workflow and is a strong candidate for a minor patch release following the email merge.

- **Platform expansion:** The merged Telegram integration ([PR #2831](https://github.com/nanocoai/nanoclaw/pull/2831)) and in-progress email integration signal a clear strategy to support all major communication backends.

- **Observability / Power-user tooling:** The CLI-derived dashboard skill ([PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795)) suggests user demand for built-in, terminal-accessible monitoring without needing external dashboards.

---

## 7. User Feedback Summary

Direct user-reported issues were absent in this 24-hour window, but the pull requests submitted by the community provide strong indirect feedback:

- **Pain point: Orphaned services** — [PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830) directly addresses a frustration for users who switch between NanoClaw builds or checkouts. The accumulation of dead `launchd`/`systemd` units is a real friction point for power users.

- **Pain point: Garbled conversation output** — [PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531) targets a bug in the polling loop that degrades the chat experience. Users are clearly running persistent polling channels and encountering this behavior regularly.

- **Feature demand: Email & Messaging** — The sustained effort on email integration (3 months in development) and the quick merge of Telegram show that the community is pushing hard for external connectivity. Users want to interact with their agent through their existing daily tools.

- **Feature demand: Smarter approvals** — [PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832) reflects a user base that wants more than binary approve/decline decisions, demanding an audit trail and contextual feedback loops in human-agent interactions.

---

## 8. Backlog Watch

Two PRs in today's update window require particular maintainer attention due to their age and impact:

- **[PR #1235 — IMAP/SMTP Email Integration](https://github.com/nanocoai/nanoclaw/pull/1235)**  
  *Opened March 18, 2026 | Updated yesterday*  
  This is the single most important open item in the project. While actively updated, its three-month development cycle puts it at risk of accruing merge conflicts with other subsystems. Maintainers should prioritize review bandwidth to move this across the finish line, as it represents the most heavily requested community feature.

- **[PR #2531 — Poll Loop Duplicate Text Fix](https://github.com/nanocoai/nanoclaw/pull/2531)**  
  *Opened May 18, 2026 | Updated yesterday*  
  This fix addresses a visible, ongoing user experience bug. Its one-month open status suggests it may be blocked by design decisions or testing requirements. Given that it directly impacts conversational quality, maintainers should ensure it receives clear guidance to reach resolution.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest — 2026-06-23**

---

### 1. Today's Overview
NullClaw experienced a quiet day on 2026-06-23, with no new issues opened or releases published over the previous 24 hours. Activity was limited to two open pull requests that received updates within the refresh window, reflecting a steady but low-intensity maintenance phase. The project’s focus appears tuned toward fixing adapter-level reliability and refreshing container infrastructure rather than shipping new features.

### 2. Releases
*No new releases were published in the last 24 hours.*

### 3. Project Progress
No pull requests were merged or closed today. Two open PRs remained active:

- **PR #968** (matrix fix): Work on persisting the sync cursor across restarts is underway.
- **PR #956** (dependencies): The Alpine base image bump to 3.24 is pending maintainer review.

No code was landed into the main branch in this window.

### 4. Community Hot Topics

Most active items (by technical substance rather than comment volume, given the quiet period):

- **PR #968 — `fix(matrix): persist next_batch across restart + test env isolation`**
  Author: `addadi` | Created: 2026-06-22 | Updated: 2026-06-22
  [View PR #968](https://github.com/nullclaw/nullclaw/pull/968)

  This is the most significant piece of work in the queue. The PR fixes a critical behavioral gap in NullClaw’s Matrix bridge: the `/sync` cursor was stored only in RAM, causing an expensive initial sync on every server restart. The proposed fix moves the token to persistent storage and adds test environment isolation. The underlying need is **operational reliability**—Matrix users require an agent that survives restarts gracefully without message loss or duplicate processing.

- **PR #956 — `ci(deps): bump alpine from 3.23 to 3.24`**
  Author: `dependabot[bot]` | Updated: 2026-06-22
  [View PR #956](https://github.com/nullclaw/nullclaw/pull/956)

  A routine automated dependency bump, but worth noting as it signals the project is actively maintaining its Docker build chain. Delays in merging this kind of PR can eventually block security patches or cause CI friction.

### 5. Bugs & Stability

**Critical – Matrix Sync State Loss**
  The bug underlying PR #968 is the highest-severity issue currently pending. On every NullClaw restart, the in-memory `next_batch` cursor is zeroed, forcing the client to request a full initial sync from the Matrix homeserver. This behavior can:
  - Overwhelm the agent with historical message replay.
  - Duplicate outbound deliveries.
  - Waste bandwidth and memory during recovery.
  A fix is already drafted in PR #968.

No new bugs, crashes, or regressions were reported in the last 24 hours. The issues list remains entirely empty (0 open items), suggesting either a very small user base or that bugs are being caught and fixed promptly outside the public tracker.

### 6. Feature Requests & Roadmap Signals

No explicit feature requests were opened today. The dominant signal from the current PR queue points toward an **upcoming incremental release** focused on:

- **State persistence** (Matrix bridge reliability)
- **Infrastructure modernization** (Alpine 3.24 base image)

No major roadmap shifts, new protocol support, or breaking changes are foreshadowed in today’s data.

### 7. User Feedback Summary

Direct user feedback is absent from today’s data, as no issues were filed and no PRs have comment threads. The existence of PR #968 strongly implies that a contributor or user encountered a concrete pain point with the Matrix adapter’s connection behavior during operation. The fact that this was addressed with a targeted fix rather than a workaround or feature request suggests a pragmatic, stability-oriented contributor community. The zero-issue backlog implies users are either highly satisfied with current stability or are not actively reporting friction through GitHub issues.

### 8. Backlog Watch

- **PR #956 — Alpine 3.23 → 3.24 bump**  
  Opened: 2026-06-15 | Updated: 2026-06-22  
  [View PR #956](https://github.com/nullclaw/nullclaw/pull/956)  
  This automated PR has been open for over a week. While low-risk, leaving dependency bumps unmerged can eventually create merge conflicts or delay critical security updates. A maintainer review and merge would improve project hygiene.

- **Issues backlog**: Empty. No long-unanswered issues require attention. This is generally healthy but warrants monitoring to confirm that users have a path to report bugs outside the GitHub issue tracker (e.g., Discord/Matrix room) should the zero count indicate an off-platform reporting habit.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for June 23, 2026, based on the last 24 hours of GitHub activity.

---

## IronClaw Project Digest — 2026-06-23

### 1. Today’s Overview
IronClaw experienced a very high-velocity 24 hours, with **23 pull requests** and **16 issues** updated. Activity is laser-focused on the **Reborn engine**, which saw major feature merges (concurrent execution, auto-approval tooling) alongside a **critical regression** that wedges web/research tasks at initialization. The project is in an aggressive phase of architectural decomposition (breaking up god-crates) and feature expansion (Automation lifecycle, Telegram support), though this rapid churn has introduced significant short-term stability flux. New contributors are actively closing WebUI v2 bugs, while core teams are split between shipping new capabilities and stabilizing the runtime.

### 2. Releases
**No new releases** were published in this window.

### 3. Project Progress (Merged/Closed PRs)
**8 pull requests** were merged or closed in the last 24 hours, representing substantial progress in performance, governance, and architecture:

- **Concurrency (PR [#5085](nearai/ironclaw PR #5085))**: Merged. The `TurnRunScheduler` breaks the strict serial execution of turns, enabling parallel, gated run processing. A major performance multiplier for the Reborn engine.
- **Permissions & Approvals (PR [#5062](nearai/ironclaw PR #5062) & [#5063](nearai/ironclaw PR #5063))**: Merged. Introduced a DB-backed per-tool permission override model (`always_allow`/`ask_each_time`/`disabled`) and live, restart-free global auto-approve toggles.
- **Error Handling (PR [#5140](nearai/ironclaw PR #5140))**: Merged. Trigger creation failures will now surface structured, actionable repair details instead of opaque generic errors.
- **Architecture (PR [#5135](nearai/ironclaw PR #5135))**: Merged. Begins the decomposition of the massive `ironclaw_reborn_composition` god-crate (~132k lines) into isolated focused crates for faster development velocity.
- **Infrastructure (PR [#5081](nearai/ironclaw PR #5081))**: Merged. A new `hosted-single-tenant` Postgres profile is ready, enabling durable state for preview hosting environments.
- **Telemetry (PR [#4985](nearai/ironclaw PR #4985))**: Closed. Engine V2 now persists LLM usage data, fixing empty `/api/admin/usage` endpoints.
- **Dependencies (PR [#5116](nearai/ironclaw PR #5116))**: Merged. 44 dependency bumps across the Rust toolchain, including `agent-client-protocol` and `rustls`.

### 4. Community Hot Topics
The most active discussions highlight a balance between eager exploration and blocking regressions:

- **Critical Regression ([#5139](nearai/ironclaw Issue #5139))**: The most alarming issue. Web/research tasks hang at initialization making *zero* LLM calls, failing 21 out of 147 daily PinchBench tasks. The author explicitly bisected the regression to a 10-commit range on `main`.
- **Approval System Flaw ([#5129](nearai/ironclaw Issue #5129))**: "Always approve" is not functioning for the `outbound_delivery_target_set` capability. This is a direct blocker for the promised frictionless Reborn experience.
- **Skill Extraction PR ([#5061](nearai/ironclaw PR #5061))**: A large open PR from a newer contributor adding Hermes-style skill extraction and self-evolution. It generates significant interest for its "AI self-improvement" angle but has no maintainer merge comments yet.
- **Dogfooding Report ([#4879](nearai/ironclaw Issue #4879))**: A persistent weekly tracker detailing local usability friction points, acting as the "voice of the user" for Reborn.

### 5. Bugs & Stability
Stability is the primary concern entering today, with a clear hierarchy of issues:

- **Critical — Task Wedge ([#5139](nearai/ironclaw Issue #5139))**: `reborn run` fails with `turn timed out` after zero LLM calls. Affects ~14% of the benchmark suite. No fix PR is yet linked, implying an active investigation.
- **High — Auto-Approves Broken ([#5129](nearai/ironclaw Issue #5129))**: `outbound_delivery_target_set` ignores the global auto-approve setting. This breaks the core workflow UX for approved tools.
- **Medium — Nightly E2E Failure ([#4108](nearai/ironclaw Issue #4108))**: The nightly scheduled E2E run continues to fail, specifically the `v2-engine` job. Although it’s a stale bot issue, it suggests test infrastructure fragility.
- **Low — WebUI Regressions**: New contributors have submitted low-risk fixes for UI regressions, including fixing sidebar thread highlighting on non-chat pages (PR [#5130](nearai/ironclaw PR #5130)) and redirecting invalid chat thread routes (PR [#5132](nearai/ironclaw PR #5132)).

### 6. Feature Requests & Roadmap Signals
The immediate roadmap is crowded with high-impact features approaching completion:

- **Automation Lifecycle (Pause/Resume/Delete)**: Issues [#5121](nearai/ironclaw Issue #5121) and [#5122](nearai/ironclaw Issue #5122) request native pause/resume and delete support for Reborn automations. Corresponding implementation PRs ([#5131](nearai/ironclaw PR #5131), [#5133](nearai/ironclaw PR #5133)) are open and awaiting merge.
- **New Channels**: **Telegram** (Issue [#5124](nearai/ironclaw Issue #5124)) is explicitly requested for Reborn. **GitHub** workflow support (PR [#5134](nearai/ironclaw PR #5134)) has detailed design docs submitted. Slack setup is actively being moved out of TOML files into the WebUI (PR [#4712](nearai/ironclaw PR #4712)).
- **Performance Week (Meta-Issue [#5125](nearai/ironclaw Issue #5125))**: A dedicated week of work has been declared to investigate inference latency (#5127), unnecessary agent steps (#5128), and turn timing attribution (#5126). This directly addresses widespread user complaints about local slowness.
- **Self-Evolution ([#5061](nearai/ironclaw PR #5061))**: Although risky, the skill extraction mechanism is a strong signal that the project is aiming for autonomous agent improvement features.

### 7. User Feedback Summary
User sentiment is a mix of enthusiasm for the new engine and frustration with its immaturity:

- **Pain Point: Slowness**: Users find local Reborn "feel slow" during dogfooding. The response is the newly established Performance Week (#5125).
- **Pain Point: Approval Friction**: The "Always approve" feature not working (#5129) and the lack of live policy changes (#4959, now fixed) were major friction points.
- **Pain Point: Configuration Hell**: First-run setup and provider configuration remain difficult, tracked rigorously in the Dogfooding Findings ([#4879](nearai/ironclaw Issue #4879)).
- **Satisfaction Indicator**: The Barcelona Hackathon branch (PR [#4787](nearai/ironclaw PR #4787)) shows external developers are using IronClaw for real-world events, indicating strong community confidence despite the bugs.

### 8. Backlog Watch
Several important items are lingering in the backlog and require maintainer attention:

- **Nightly E2E Stability ([#4108](nearai/ironclaw Issue #4108))**: Open since May 27, this recurring failure erodes confidence in CI. It was updated yesterday but remains unresolved.
- **Stale WASM Bump ([#4032](nearai/ironclaw PR #4032))**: A dependency bump for the WASM group has been open since May 25. While low risk, its staleness suggests potential merge conflicts.
- **Google WASM Auth Fix ([#4969](nearai/ironclaw PR #4969))**: Open since June 16, this PR fixes structured `auth_required` errors for Google tools. In a week of heavy tool/model changes, this fix is important but remains unmerged.
- **Architecture God-Crate Successor ([#5137](nearai/ironclaw PR #5137))**: A second round of decomposition for the `ironclaw_reborn_composition` crate has been opened as a draft. Given the volume of other features landing, this refactoring risks conflicting with active feature branches on `main`.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-23

---

## 1. Today's Overview

LobsterAI shows a stark contrast today between strong internal development velocity and severely lagging community maintenance. Six pull requests were merged, led by a major **Cowork Plan Mode** feature and a series of OpenClaw plugin infrastructure fixes. However, the 5 Issues and 8 Pull Requests updated in the last 24 hours are all `[stale]` items from early April with zero community engagement and no maintainer activity. No new releases were published, despite the substantial merged feature work.

---

## 2. Releases

**None.**

No new releases were published in the last 24 hours. Significant merged features (Plan Mode, OpenClaw plugin enhancements) suggest a release may be forthcoming once the current development cycle closes.

---

## 3. Project Progress

**Merged/Closed PRs Today (6 items)**

The team focused heavily on maturing the Cowork agent workflow and stabilizing the OpenClaw plugin runtime.

- **Cowork Plan Mode (Major Feature)**
  - **[PR #2183](https://github.com/netease-youdao/LobsterAI/pull/2183):** Merged the new **Plan Mode** workflow into the composer. This introduces structured planning blocks, copy/download/expand actions, prevention of mutating tool calls during planning, and a clean approval flow to standard execution.

- **OpenClaw Plugin & Core Infrastructure**
  - **[PR #2182](https://github.com/netease-youdao/LobsterAI/pull/2182):** Fixed upgraded IM plugin installations (DingTalk, Lark/Feishu, WeCom, POPO) to support OpenClaw 2026.6.1 layouts.
  - **[PR #2185](https://github.com/netease-youdao/LobsterAI/pull/2185):** Fixed a bug where the `GetReplyOptions.cwd` field was missing from the OpenClaw run-cwd patch.
  - **[PR #2186](https://github.com/netease-youdao/LobsterAI/pull/2186):** Fixed NIM channel plugin compilation, extracting shared TypeScript preparation into `scripts/openclaw-plugin-preparers`.
  - **[PR #2187](https://github.com/netease-youdao/LobsterAI/pull/2187):** Aligned renderer and main test metadata expectations for reasoning-capable models.

- **Documentation**
  - **[PR #2184](https://github.com/netease-youdao/LobsterAI/pull/2184):** Refreshed `AGENTS.md` to document the current Cowork/OpenClaw architecture, Codex scope, quality gates, and common patterns.

---

## 4. Community Hot Topics

**No active community discussions emerged today.** The 5 recently updated Issues received zero reactions and only 1 comment each, all from stale-bot automation or single reporters.

| Issue | Topic | Engagement |
|---|---|---|
| [#1409](https://github.com/netease-youdao/LobsterAI/issues/1409) | Scheduled task triggered, no history generated | 0 👍, 1 comment |
| [#1411](https://github.com/netease-youdao/LobsterAI/issues/1411) | Overview time filter unresponsive | 0 👍, 1 comment |
| [#1413](https://github.com/netease-youdao/LobsterAI/issues/1413) | Skills UI overflow / display broken | 0 👍, 1 comment |
| [#1414](https://github.com/netease-youdao/LobsterAI/issues/1414) | Total session count stuck at 0 | 0 👍, 1 comment |
| [#1416](https://github.com/netease-youdao/LobsterAI/issues/1416) | English UI layout broken (text overlap) | 0 👍, 1 comment |

**Underlying Need:** Users are encountering significant friction on the core Profile/Overview page, preventing them from accurately tracking usage, filtering data, or using the app in English. The complete lack of maintainer follow-up suggests these users may be waiting for a patch or official response.

---

## 5. Bugs & Stability

All five bugs reported below are **stale** (filed April 3rd, updated June 22nd by bot). **No fix PRs have been linked** to any of these issues.

**High Severity**

| ID | Description | Impact |
|---|---|---|
| [#1414](https://github.com/netease-youdao/LobsterAI/issues/1414) | "Total Sessions" always shows 0, despite 432 API calls and 444.39 credits used | Core analytics data integrity failure; breaks user trust in reporting |
| [#1409](https://github.com/netease-youdao/LobsterAI/issues/1409) | Scheduled tasks trigger but produce no history | Automated workflows silently broken; potential data loss |
| [#1411](https://github.com/netease-youdao/LobsterAI/issues/1411) | Overview time filter ("Past 30 Days") completely unresponsive | Blocks user from viewing historical usage data |

**Medium Severity**

| ID | Description | Impact |
|---|---|---|
| [#1416](https://github.com/netease-youdao/LobsterAI/issues/1416) | Switching to English causes text/number overlapping on "Current Plan" card | Localization broken; poor UX for international users |
| [#1413](https://github.com/netease-youdao/LobsterAI/issues/1413) | Adding many skills to the input box causes severe UI distortion | Feature scaling issue; degrades prompt composition UX |

---

## 6. Feature Requests & Roadmap Signals

The most significant roadmap signal is the **Cowork Plan Mode** merged today in [PR #2183](https://github.com/netease-youdao/LobsterAI/pull/2183). This represents a major architectural shift from simple chat completion toward structured, multi-step agentic planning workflows. Combined with the OpenClaw plugin system enhancements (DingTalk, Lark, WeCom, POPO), the team is clearly prioritizing:

- **Agentic Task Decomposition & Planning**
- **Enterprise IM Integration & Plugin Extensibility**
- **Runtime Performance & Plugin Sandboxing**

No new feature requests were filed by users today.

**Prediction for Next Release:** The next LobsterAI version will likely center on **Cowork Plan Mode** as the flagship feature, paired with **OpenClaw 2026.6.1** plugin compatibility and a broader slate of enterprise messaging integrations.

---

## 7. User Feedback Summary

**Pain Points:**
- **Dashboard Reliability:** Users who actively use the platform (432 API calls documented) cannot trust the overview analytics. Session counts are frozen at zero ([#1414](https://github.com/netease-youdao/LobsterAI/issues/1414)), filters don't work ([#1411](https://github.com/netease-youdao/LobsterAI/issues/1411)), and language switching breaks the UI ([#1416](https://github.com/netease-youdao/LobsterAI/issues/1416)).
- **Automation Failures:** Scheduled tasks executing without recording history ([#1409](https://github.com/netease-youdao/LobsterAI/issues/1409)) represents a silent failure mode that undermines trust in background agent processes.
- **Lack of Maintainer Response:** All five bugs are 80 days old with zero maintainer replies, signaling to the community that these critical UX areas may not be prioritized.

**Dissatisfaction Indicator:** Despite users providing detailed bug reports with screenshots and reproduction steps, the lack of any response or resolution after nearly 3 months is the strongest negative signal in today's data.

---

## 8. Backlog Watch

The most significant project health concern is the **accumulated triage backlog**. A complete block of community-submitted work remains untouched since April 2026.

**Stale Issues (Filed April 3rd, 80 days stale):**
- [#1409](https://github.com/netease-youdao/LobsterAI/issues/1409) — Scheduled history generation broken
- [#1411](https://github.com/netease-youdao/LobsterAI/issues/1411) — Overview time filter dead
- [#1413](https://github.com/netease-youdao/LobsterAI/issues/1413) — Skills UI overflow
- [#1414](https://github.com/netease-youdao/LobsterAI/issues/1414) — Session count stuck at zero
- [#1416](https://github.com/netease-youdao/LobsterAI/issues/1416) — English UI layout broken

**Stale PRs (Filed April 2–3rd, awaiting review):**
- [#1407](https://github.com/netease-youdao/LobsterAI/pull/1407) — Proxy body size limit (potential OOM fix)
- [#1408](https://github.com/netease-youdao/LobsterAI/pull/1408) — MCP Bridge unhandled Promise fix
- [#1410](https://github.com/netease-youdao/LobsterAI/pull/1410) — Sqlite synchronous write performance fix (debounce)
- [#1415](https://github.com/netease-youdao/LobsterAI/pull/1415) — Migration completion flag logic fix (data loss risk)
- [#1419](https://github.com/netease-youdao/LobsterAI/pull/1419) — NIM group type enum mapping fix
- [#1420](https://github.com/netease-youdao/LobsterAI/pull/1420) — Cron concurrency & phantom event fix
- [#1421](https://github.com/netease-youdao/LobsterAI/pull/1421) — User memory query caching performance fix
- [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Electron & Electron Builder version bump

**Assessment:** The project is actively investing in new architecture (Plan Mode, OpenClaw plugins) while maintaining a significant quality-of-life and community-contribution debt. Addressing this backlog—especially the stability PRs from `liulingfeng`, `wowiscrazy`, and `choyuenga`—would substantially improve project health and contributor morale.

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

Here is the QwenPaw project digest for June 23, 2026, based on the CoPaw ecosystem’s GitHub data.

---

## 1. Today’s Overview
QwenPaw is in a phase of intense stabilization and community-driven hardening. In the last 24 hours, **50 Pull Requests** and **23 Issues** were updated, representing one of the highest daily activity levels in recent months. While no new official release was published, the project’s focus is squarely on crushing critical defects (process freezes, cron failures, frontend crashes), expanding platform compatibility (mobile responsiveness, custom LLM providers, Slack integration), and building out a rigorous unit-test foundation for both frontend and backend modules. The high volume of first-time contributions indicates healthy community momentum, though the bug backlog remains substantial and threatening to overall stability.

## 2. Releases
**No new versions were released in the last 24 hours.** The latest stable version remains **v1.1.12.post1**. Given the breadth of open bug reports and pending feature PRs (particularly Slack channel support and the mobile adaptation series), the next release is likely to be a significant bump rather than a hotfix patch.

## 3. Project Progress
Despite no release, substantial code was authored and reviewed. The following reflects features advanced and bugs closed:

- **Bugs Closed:**  
  - [#5370](https://github.com/agentscope-ai/QwenPaw/issues/5370) `send_file_to_user` HTTP 404 (fix PR [#5407](https://github.com/agentscope-ai/QwenPaw/pull/5407))  
  - [#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354) Message queue session-switching confusion  
- **Testing & Quality Infrastructure:**  
  - [#5405](https://github.com/agentscope-ai/QwenPaw/pull/5405) / [#5409](https://github.com/agentscope-ai/QwenPaw/pull/5409) Added ~170 unit tests for the backend `crons` module and frontend stores/hooks (closing [#5404](https://github.com/agentscope-ai/QwenPaw/issues/5404) / [#5406](https://github.com/agentscope-ai/QwenPaw/issues/5406))  
- **Active Feature Development (Open PRs, not yet merged):**  
  - Massive mobile responsiveness overhaul by contributor `yaozy2020` covering **six** control pages: Workspace, Channels, MCP, ACP, Inbox, and Environments ([#5384](https://github.com/agentscope-ai/QwenPaw/pull/5384), [#5369](https://github.com/agentscope-ai/QwenPaw/pull/5369), [#5381](https://github.com/agentscope-ai/QwenPaw/pull/5381), [#5382](https://github.com/agentscope-ai/QwenPaw/pull/5382), [#5383](https://github.com/agentscope-ai/QwenPaw/pull/5383), [#5385](https://github.com/agentscope-ai/QwenPaw/pull/5385))  
  - Full Slack channel support via Socket Mode (~3,500 lines, [#5193](https://github.com/agentscope-ai/QwenPaw/pull/5193))  
  - Langfuse tracing Docker deployment documentation ([#5380](https://github.com/agentscope-ai/QwenPaw/pull/5380))  
  - Tauri auto-updater flow ([#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)) and pywebview instant-window startup ([#5153](https://github.com/agentscope-ai/QwenPaw/pull/5153))

## 4. Community Hot Topics
The highest-engagement items reveal deep concerns around reliability and configuration persistence:

- **[#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) (17 comments): Sub-agent context compaction freeze** – The single most active issue. Users report the entire QwenPaw process hanging when a sub-agent triggers context compaction, requiring a manual restart. This is a top-tier reliability blocker.
- **[#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) (9 comments): Built-in skills re-enable on update** – A persistent regression first reported in May (#4807) that remains unfixed, causing frustration with every version bump. Users want a “sticky” disabled state.
- **[#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) (5 comments): Custom OpenAI providers lack function calling** – Users integrating third-party providers like OMLX expect full API compatibility. Ollama works, but custom endpoints fail to invoke tools.
- **[#2969](https://github.com/agentscope-ai/QwenPaw/issues/2969) (5 comments, 2 👍): Personal Knowledge Base** – A long-running feature request that consistently attracts community support.
- **[#5370](https://github.com/agentscope-ai/QwenPaw/issues/5370) (5 comments): `send_file_to_user` 404** – A critical workflow blocker that was quickly scoped and closed, with a fix PR submitted within 24 hours.

**Underlying needs:** Users are demanding production-grade reliability (process hangs, cron jobs), frictionless provider configuration, persistent user settings across upgrades, and mobile access for daily use.

## 5. Bugs & Stability
No regressions were introduced by a new release, but several high-severity defects remain active.

**Critical (Core breakdown / crash / hang):**
- **Sub-agent freeze** – [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) Process hang on context compaction. No fix PR yet.  
- **Console frontend crash** – [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401) White screen on large tool-use histories.  
- **Cron scheduler stall** – [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398) Jobs stop dispatching while app remains alive.  
- **Dream task failure** – [#5402](https://github.com/agentscope-ai/QwenPaw/issues/5402) All three agents in the nightly consolidation task failed.  
- **Fresh install error** – [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) Internal Server Error blocks new users entirely.

**High (Feature degradation / blocking):**
- [#5345](https://github.com/agentscope-ai/QwenPaw/issues/5345) Custom providers (OMLX) lack function calling.  
- [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) Skills re-enable on every upgrade.  
- [#5373](https://github.com/agentscope-ai/QwenPaw/issues/5373) Shell command tool fails on pipes/redirects.  
- [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) Zhipu provider model connection fails despite API key passing the provider test.  
- [#5333](https://github.com/agentscope-ai/QwenPaw/issues/5333) Agent stalling on submit (potentially DeepSeek-specific).

**Medium (UI/UX issues):**
- [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403) Browser autofill hijacks Model Config search.  
- [#5374](https://github.com/agentscope-ai/QwenPaw/issues/5374) Drag-and-drop upload broken on Mac Chrome.  
- [#5378](https://github.com/agentscope-ai/QwenPaw/issues/5378) Custom model endpoint URL stuck in search box.

**Note:** Fix PRs exist for #5370 ([#5407](https://github.com/agentscope-ai/QwenPaw/pull/5407)), session lock ([#5357](https://github.com/agentscope-ai/QwenPaw/pull/5357)), and prompt file loading ([#5396](https://github.com/agentscope-ai/QwenPaw/pull/5396)).

## 6. Feature Requests & Roadmap Signals
- **High likelihood for next version:**  
  - **Slack channel** ([#5193](https://github.com/agentscope-ai/QwenPaw/pull/5193)) – A massive 3.5k-line PR, clearly a priority feature.  
  - **Mobile responsiveness** (PR series by `yaozy2020`) – Six control pages adapted; strongly signals the team is prioritizing cross-device UX.  
  - **Tauri auto-updater** ([#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)) – Desktop user experience improvement.  
- **Moderate likelihood (gathering steam):**  
  - **Knowledge base support** ([#2969](https://github.com/agentscope-ai/QwenPaw/issues/2969)) – Highly requested, often mentioned in related discussions.  
  - **Agent/Workspace decoupling** ([#5392](https://github.com/agentscope-ai/QwenPaw/issues/5392)) – A strong architectural signal from the community for reusability.  
  - **OpenClaw/Hermes import path** ([#5254](https://github.com/agentscope-ai/QwenPaw/issues/5254)) – User onboarding friction that may warrant a migration tool.  
- **Experimental / Niche:**  
  - Recall-aware dream consolidation ([#5387](https://github.com/agentscope-ai/QwenPaw/issues/5387))  
  - ToolGuard → Policy engine refactor ([#5301](https://github.com/agentscope-ai/QwenPaw/pull/5301))

## 7. User Feedback Summary
**Satisfaction Drivers:**
- Users are actively building complex workflows (dream tasks, cron jobs, multi-agent orchestrations), indicating deep trust in the platform’s potential.  
- The adoption of the message queue (#5354) was broadly praised even as its UX kinks were discovered.  
- High community participation in mobile development suggests strong latent demand for daily mobile use.

**Dissatisfaction / Pain Points:**
1. **Reliability Gap:** The most vocal feedback revolves around process freezes (#5218) and silent failures (#5398, #5402). Users feel the core runtime is fragile under real-world loads.  
2. **Provider Fragmentation:** Users struggle with DeepSeek, Zhipu, and OMLX—providers outside the “blessed” OpenAI/Ollama nests are effectively second-class citizens.  
3. **Upgrade Fatigue:** The skill re-enable bug (#5262) erodes confidence in the upgrade process itself.  
4. **Mobile/UI Regressions:** The Console remains a pain point on mobile, with users expressing that the desktop UI is “great” but the phone experience lags behind.

## 8. Backlog Watch
The following items are of high community interest or user impact but lack a maintainer response or visible fix:

- **[#2969](https://github.com/agentscope-ai/QwenPaw/issues/2969) – Personal Knowledge Base.** Opened **April 5**. 2 👍. Zero maintainer input. One of the longest-standing feature requests.
- **[#5254](https://github.com/agentscope-ai/QwenPaw/issues/5254) – OpenClaw/Hermes Migration Path.** Opened **June 17**. Unanswered. Critical for capturing users migrating from adjacent projects.
- **[#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317) – Tauri Python path.** Opened **June 18**. User is completely blocked on Windows.
- **[#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) – Internal Server Error on fresh install.** Opened **June 22**. No maintainer response yet for a blocker that prevents new users from accessing the app.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

**ZeroClaw Project Digest — 2026-06-23**

---

## 1. Today's Overview

ZeroClaw is in a high-intensity stabilization and architectural refinement cycle, with **50 Issues** and **50 Pull Requests** updated in the last 24 hours. The close rate is modest (9 issues, 3 merged PRs), indicating a review bottleneck as a massive wave of runtime bug fixes and security hardening PRs queues for landing. The formal closure of the "WebAssembly-first, eliminate Node.js" ([#7674](zeroclaw-labs/zeroclaw Issue #7674)) and "Native Dynamic-Library Plugin System" ([#7420](zeroclaw-labs/zeroclaw Issue #7420)) RFCs signals that foundational architectural debates have concluded, clearing the way for implementation work in v0.9.0. Despite this progress, several critical S1 workflow-blocking bugs remain open, particularly around context budgeting and tool availability.

---

## 2. Releases

*None.* No releases were cut in the last 24 hours. The project is actively building toward the **v0.8.3 runtime stability milestone** (tracked by [#8071](zeroclaw-labs/zeroclaw Issue #8071)) and the larger **v0.9.0 auth/security release** (tracked by [#7432](zeroclaw-labs/zeroclaw Issue #7432)).

---

## 3. Project Progress

**Closed Issues (Resolved/Implemented):**
*   **Critical Bugfixes:** [#8193] (MCP tools missing from TUI — *workflow blocked*), [#8013] (disabled agents still answering on Discord — *security risk*), [#6037] (cron jobs launched repeatedly).
*   **RFCs Concluded:** [#7420] (Native Dynamic-Library Plugin System) and [#7674] (WebAssembly-first) were closed. [#7674] has been split into actionable child issues for the Web UI ([#8132]) and Wasm plugin runtime ([#8135]).
*   **Features:** [#6371] (WhatsApp `allowed_groups` permit list), [#7688] (runtime hook panic recovery & cancellation tests).

**Open Merge Queue (Key PRs Ready for Review):**
*   **Runtime & Agent:** [#8180] (Fix vision capability errors), [#8003] (Wire `session_end` hook lifecycle), [#7959] (Allow auto-approved tools at non-Full autonomy), [#7960] (Gate `execute_pipeline` with per-agent `ToolAccessPolicy`).
*   **Channels:** [#8145] (Standardize ack reactions/typing stubs across 23 channels), [#8153] (Preserve re-loadable media refs in cached history), [#8098] (Reject reserved agent names in config).
*   **Logging:** [#7921] (Fix same-timestamp pagination race in log reader).
*   **Web Dashboard:** [#8082] (Write-guard + skipped audit for skills), [#8086] (Themed config pickers), [#8087] (Doctor "fix in place" modal on dashboard).

---

## 4. Community Hot Topics

The most active discussions reveal a community deeply invested in architecture, security hardening, and core reliability:

*   **Architecture Pivot:** The closure of the WebAssembly-first RFC ([#7674](zeroclaw-labs/zeroclaw Issue #7674)) has generated intense follow-on activity on child RFCs [#8135](zeroclaw-labs/zeroclaw Issue #8135) (Wasm-first plugin runtime) and [#8132](zeroclaw-labs/zeroclaw Issue #8132) (Replace React/Vite with a Rust→Wasm framework). This aligns with the supply-chain signing RFC ([#8177](zeroclaw-labs/zeroclaw Issue #8177)) to form a unified push toward a fully sandboxed, auditable, Rust-native stack.
*   **MCP & Provider Tool Reliability:** Issue [#7756](zeroclaw-labs/zeroclaw Issue #7756) (tools unavailable on OpenAI/Anthropic turns) and the just-resolved [#8193](zeroclaw-labs/zeroclaw Issue #8193) (TUI ignores MCP tools) are the highest-traffic pain points, reflecting broad user frustration with multi-model tool orchestration.
*   **Config UX Friction:** The long-running context budget issue ([#5808](zeroclaw-labs/zeroclaw Issue #5808), since April) and the feature request for auto-YOLO risk profiles in quickstart ([#8125](zeroclaw-labs/zeroclaw Issue #8125)) highlight that default configurations are a major source of negative first-run experiences.

---

## 5. Bugs & Stability

**S1 — Workflow Blocked:**
*   [#5808] *(OPEN, P1)*: Default 32k context budget is exceeded 3.3x on the first turn, causing perpetual preemptive trim. Open since April 23 — **the single highest-impact open issue.**
*   [#7756] *(OPEN, P1)*: MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turn paths.
*   [#8154] *(OPEN, P1)*: Kimi Code provider endpoint is dead (404). Newly reported with no fix PR yet.
*   [#7462] *(OPEN, P1)*: 74 test failures on Windows 11. Test job only runs on Linux, creating a blind spot for cross-platform regressions.

**S0 — Security / Data Loss:**
*   [#8013] *(CLOSED)*: Disabled agent stays active on Discord. **Fix has been applied.**

**Active Fixes in Flight:**
A large batch of bug-fix PRs (see Section 3) from multiple contributors (mazhuima, Nillth, singlerider, wangmiao0668000666) targets this exact class of issue, suggesting an organized crunch toward the v0.8.3 release.

---

## 6. Feature Requests & Roadmap Signals

**Confirmed Roadmap (v0.9.0 / #7432 track):**
*   **Auth & Security:** Local password/IdP-less login ([#8076]), in-app upgrade with supervised restart ([#8170]), supply chain signing with SLSA ([#8177]).
*   **Wasm-First:** Wasm default plugin runtime ([#8135]), Rust→Wasm web UI framework ([#8132]).
*   **Web UI Overhaul:** Skills management dashboard ([#8082]), config editor UI ([#8086]), dashboard doctor linkage ([#8087]).

**Likely v0.8.x / Near-Term:**
*   **Session Management:** Automatic stale-session truncation via `session_ttl_hours` ([#8134]).
*   **Provider Enhancements:** OpenRouter model fallback arrays ([#8138]), optional Telegram webhook mode ([#8046]).
*   **Onboarding UX:** Auto-YOLO risk profile for quickstart ([#8125]).

---

## 7. User Feedback Summary

**Pain Points:**
*   **"Out-of-the-box is broken":** Users repeatedly report that the default configuration (context budget, risk profile) immediately blocks or degrades the initial experience ([#5808](zeroclaw-labs/zeroclaw Issue #5808), [#8125](zeroclaw-labs/zeroclaw Issue #8125)).
*   **Tool inconsistency erodes trust:** The unreliability of MCP and provider-native tool surfaces ([#7756](zeroclaw-labs/zeroclaw Issue #7756), [#8193](zeroclaw-labs/zeroclaw Issue #8193]) is the dominant daily frustration.
*   **Cross-platform neglect:** The 74 Windows test failures ([#7462](zeroclaw-labs/zeroclaw Issue #7462)) and CLI keybinding conflicts on macOS ([#8075](zeroclaw-labs/zeroclaw Issue #8075)) show real friction outside Linux.

**Satisfaction Signals:**
*   The community is deeply engaged in architectural RFCs and CI/security hardening (#8056, #8057, #8177), indicating strong commitment to production maturity.
*   Bug reports are highly detailed (specific logs, reproduction steps), reflecting a sophisticated and invested user base.

---

## 8. Backlog Watch

The following items are high-priority or maintenance-blocking and have been awaiting maintainer action or a clear path forward:

| Issue | Priority | Created | Status | Why It's Stalled |
|-------|----------|---------|--------|-------------------|
| [#5808](zeroclaw-labs/zeroclaw Issue #5808) - Context budget overflow | P1 | 2026-04-23 | `in-progress` | **Urgent.** Massive user impact; no visible fix PR despite being open 2 months. |
| [#7462](zeroclaw-labs/zeroclaw Issue #7462) - 74 Windows test failures | P1 | 2026-06-10 | `accepted` | CI does not run on Windows; blocking non-Linux adoption. |
| [#7756](zeroclaw-labs/zeroclaw Issue #7756) - MCP/Provider tool gaps | P1 | 2026-06-16 | `accepted` | Highly requested fix still in discussion; no active PR. |
| [#6943](zeroclaw-labs/zeroclaw Issue #6943) - Plugin system RFC deconflict | P2 | 2026-05-26 | `accepted` | RFC accepted but stalled for a month on implementation assignment. |
| [#8177](zeroclaw-labs/zeroclaw Issue #8177) - Supply chain signing RFC | P2 | 2026-06-22 | `needs-maintainer-review` | Key security RFC pending triage. |
| [#8132](zeroclaw-labs/zeroclaw Issue #8132) - Rust→Wasm web framework RFC | P3 | 2026-06-22 | `needs-maintainer-review` | Child of the closed #7674; awaiting nod from maintainers. |
| [#8043](zeroclaw-labs/zeroclaw Issue #8043) - Retire aardvark-sys crate | P2 | 2026-06-20 | `needs-maintainer-review` | Cleanup RFC awaiting maintainer ratification. |

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*