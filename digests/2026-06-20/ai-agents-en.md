# OpenClaw Ecosystem Digest 2026-06-20

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-20 03:23 UTC

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

Here is the OpenClaw project digest for 2026-06-20, based on the provided GitHub data.

---

## OpenClaw Project Digest — 2026-06-20

### 1. Today’s Overview
OpenClaw remains in a period of extremely high development velocity, with **500 issues and 500 pull requests** updated in the last 24 hours. A new **v2026.6.9-beta.1** release shipped today that significantly overhauls Telegram message delivery. Despite this feature progress, project health is under immediate strain from two **P0 blockers**: a severe Gateway memory leak causing production OOM crashes ([#91588](openclaw/openclaw Issue #91588)) and a silent data-loss bug in the memory-core dreaming pipeline ([#84882](openclaw/openclaw Issue #84882)). The sheer volume of open work (453 open issues, 453 open PRs) continues to suggest a meaningful bottleneck in maintainer review and product decision capacity.

### 2. Releases
- **v2026.6.9-beta.1**
  - The primary focus is a major enrichment of the Telegram delivery path.
  - **Rich content**: Telegram now sends rich HTML, preserves rich markdown and sticker paths, and renders progress drafts and command output more faithfully.
  - **Routing fixes**: Mentions and spooled handlers are now kept on the correct delivery path. (Refs: [#93286](openclaw/openclaw Issue #93286), [#93164](openclaw/openclaw Issue #93164), [#93124](openclaw/openclaw Issue #93124), [#93364](openclaw/openclaw Issue #93364)
  - *No breaking changes or migration notes were specified.*

### 3. Project Progress
A total of **47 PRs were merged or closed** today. Key thematic advances visible in the open/updated PR pipeline include:
- **Claude/Anthropic Compatibility**: PRs [#95187](openclaw/openclaw PR #95187) and [#95172](openclaw/openclaw PR #95172) resolve hardcoded version strings and deprecated permission schemas that broke interactions with the latest Claude Code CLI.
- **Provider fixes**: OpenRouter short aliases for DeepSeek V4 models are being normalized to prevent `400 model_not_found` errors ([#95202](openclaw/openclaw PR #95202), [#95208](openclaw/openclaw PR #95208)). Subagent model override persistence has also been corrected ([#95210](openclaw/openclaw PR #95210)).
- **macOS Tahoe Support**: Three PRs ([#95170](openclaw/openclaw PR #95170), [#95194](openclaw/openclaw PR #95194), [#95195](openclaw/openclaw PR #95195)) were opened to fix OS version detection on macOS 26, ensuring diagnostics and runtime prompts report the correct product version.
- **Security Hardening**: PR [#84738](openclaw/openclaw PR #84738) (stopping plaintext API keys in `models.json`) and PRs [#84326](openclaw/openclaw PR #84326) / [#84450](openclaw/openclaw PR #84450) (config audit and sandbox registry findings) continue to advance the project’s security posture.

### 4. Community Hot Topics

| Topic | Issue / PR | Comments | 👍 | Analysis |
|---|---|---|---|---|
| **Session State Migration** | [#88838](openclaw/openclaw Issue #88838) | 31 | 1 | Deep community engagement with the SQLite migration abstraction. Users are heavily invested in the architecture that prevents future data loss. |
| **Gateway Memory Leak (P0)** | [#91588](openclaw/openclaw Issue #91588) | 13 | 1 | Highest stress point for production users. Memory grows from 350MB to 15.5GB. No fix PR is linked yet. |
| **Doctor Performance Regression** | [#85333](openclaw/openclaw Issue #85333) | 13 | 1 | A pervasive pain point—`doctor --fix` is 4-5x slower. Tagged as `stale`, which is concerning for a P1 impact issue. |
| **Model Fallback Reliability** | [#85103](openclaw/openclaw Issue #85103) | 10 | 1 | Users are experiencing hard failures when providers hit quota limits, as the fallback chain is not triggered. |
| **Per-Agent Memory Vaults** | [#63829](openclaw/openclaw Issue #63829) | 10 | 9 | The highest-community-demand feature. Users are blocked on multi-agent deployments without isolated memory wikis. |
| **Session Isolation Failure** | [#84903](openclaw/openclaw Issue #84903) | 8 | 2 | "One agent's stalled session blocks the entire Gateway event loop" — a fundamental reliability concern for multi-tenant setups. |

### 5. Bugs & Stability

**P0 — Critical Risk**
- **Gateway Memory Leak** ([#91588](openclaw/openclaw Issue #91588)): RSS grows to 15.5GB causing OOM kills. No fix PR currently in the pipeline.
- **Silent Daily Memory File Deletion** ([#84882](openclaw/openclaw Issue #84882)): The `memory-core` dreaming pipeline is deleting `memory/YYYY-MM-DD.md` files. This is a **data loss** incident.

**P1 — High Impact / Regression**
- **Event Loop Saturation** ([#84771](openclaw/openclaw Issue #84771)): Startup blocks the event loop for 28–64 seconds.
- **Matrix Channel Broken** ([#90325](openclaw/openclaw Issue #90325)): Regression in v2026.6.1 — `TypeError` on every inbound message.
- **Subagent Output Leak** ([#90840](openclaw/openclaw Issue #90840)): Raw subagent output delivered to the user instead of the parent agent's summary.
- **Active Memory Circuit Breaker** ([#90082](openclaw/openclaw Issue #90082)): Too aggressive — injects error prompts into the main session context.
- **Delivery Recovery Silent Failure** ([#91212](openclaw/openclaw Issue #91212)): After restart, recovery attempts start before WebSocket transports are ready, causing "0 recovered, N failed."

**P1 — Fix PRs in Flight**
- **Telegram Web Support Broken** ([#93794](openclaw/openclaw Issue #93794)): *Closed* — the team responded quickly to this regression.
- **Telegram `/usage` Broken** ([#93905](openclaw/openclaw Issue #93905)): Regression in v2026.6.8. Fix being tracked.
- **Auto-Reply Fence Interleaving** ([#93858](openclaw/openclaw Issue #93858)): Fix PR linked.

### 6. Feature Requests & Roadmap Signals

- **Architectural (Next Major)**: The **SQLite migration for session/transcript** ([#88838](openclaw/openclaw Issue #88838)) and **bounded memory append semantics** ([#90354](openclaw/openclaw Issue #90354)) signal a strong program to harden state management. Likely landing in the next stable release.
- **Mid-Term / High Demand**: **Per-agent memory wiki vaults** ([#63829](openclaw/openclaw Issue #63829)) and **Topic-session families** ([#90916](openclaw/openclaw Issue #90916)) are highly requested for multi-agent orchestration. **Per-channel model overrides** ([#53638](openclaw/openclaw Issue #53638)) address a core deployment flexibility gap.
- **Channel Parity**: The **Webchat inline button support** ([#46656](openclaw/openclaw Issue #46656)) is a long-standing feature needed to bring Telegram's `buttons` parameter to the Control UI.
- **Enterprise Readiness**: The **Kubernetes documentation update** ([#91455](openclaw/openclaw Issue #91455)) and **slim Docker image** ([#85332](openclaw/openclaw Issue #85332)) requests indicate growing demand for easier cloud and containerized deployment.

### 7. User Feedback Summary

- **Satisfaction**: Users respond positively to rapid triage of channel-breaking regressions (e.g., Telegram Web in [#93794](openclaw/openclaw Issue #93794)). The active engagement in architectural discussions (e.g., the SQLite migration) shows a technically sophisticated user base that feels invested in the project's direction.
- **Dissatisfaction / Pain Points**:
  - **Production Stability**: The strongest theme. Users are getting killed by the OOM leak ([#91588](openclaw/openclaw Issue #91588)) and the event loop blocking ([#84903](openclaw/openclaw Issue #84903)). One user explicitly noted, "One agent's stalled session blocks the entire Gateway event loop."
  - **Data Integrity Breach**: The silent deletion of daily memory files ([#84882](openclaw/openclaw Issue #84882)) is the most severe trust-damaging bug in this snapshot.
  - **Upgrade Friction**: A user reported needing a "Time Machine restore of `~/.openclaw`" to recover from an upgrade ([#85027](openclaw/openclaw Issue #85027)).
  - **Configuration Diagnostics**: The `doctor --fix` performance regression ([#85333](openclaw/openclaw Issue #85333)) and false-positive warnings ([#95067](openclaw/openclaw PR #95067)) remain a source of user frustration.

### 8. Backlog Watch

Items requiring maintainer attention that are showing stagnation or high risk:

| Issue / PR | Age | Status | Risk |
|---|---|---|---|
| **#85333** — `doctor --fix` 4-5x slower | May 22 (29 days) | P1, `stale` | A major performance regression affecting all users is being ignored. |
| **#63829** — Per-agent memory vaults | Apr 9 (72 days) | P1, `needs-product-decision` | The community’s most wanted feature is blocked on internal triage. |
| **#49063** — Telegram native channel commands | Mar 17 (95 days) | P2, `needs-proof` | A requested channel feature has sat untouched for 3 months. |
| **#84645** — Inline interpreter eval materialization | May 20 (31 days) | P2, `ready for maintainer look` | A security boundary improvement with high merge risk that appears ready for review. |
| **#84738** — Stop plaintext keys in models.json | May 21 (30 days) | P1, `waiting on author` | A critical security improvement awaiting final sign-off. |

**Assessment of the `clawsweeper` triage system**: While the labeling infrastructure is producing thorough metadata, the volume of items sitting behind `needs-maintainer-review` and `needs-product-decision` gates is a specific project health risk. The team’s ability to sustain its high development velocity depends on resolving this review bottleneck, particularly for P0 and P1 items.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** June 20, 2026  
**Scope:** Personal AI Agent / Open-Source Assistant Ecosystem  
**Audience:** Technical Decision-Makers & Developers

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing an aggressive transition from experimental chat wrappers to production-grade multi-agent platforms, with six projects showing very high development velocity. A clear bifurcation is emerging: comprehensive, horizontally-scaled platforms (OpenClaw, Hermes, IronClaw) versus specialized, vertically-integrated forks targeting specific deployment topologies (NullClaw for mobile, CoPaw for the Chinese ecosystem). Despite the rapid feature output across all active projects, **provider compatibility, memory integrity, and security hardening** remain the universal pain points, with every major project reporting regressions against non-OpenAI providers or data-loss incidents in the last 24 hours. The landscape is healthy but strained—platforms with the highest community engagement (OpenClaw) are simultaneously the ones showing the clearest signs of maintainer bottleneck and production stability risk.

---

## 2. Activity Comparison

| Project | Issues (Updated/24h) | PRs (Updated/24h) | PRs (Merged/24h) | Release Status | Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 47 | v2026.6.9-beta.1 | ⚠️ **Strained** – P0 blockers active, review bottleneck |
| **Hermes Agent** | 50 | 50 | 7 | v0.17.0 (massive) | ✅ **Excellent** – Rapid post-launch stabilization |
| **NanoBot** | 11 | 34 | 19 | v0.2.1 | ✅ **Excellent** – Exceptional responsiveness |
| **IronClaw** | — | 30 | 12 | None (Reborn phase) | ✅ **Good** – Strong team-driven velocity |
| **ZeroClaw** | 28 | 50 | 3 | v0.8.x | ✅ **Good** – Hardening for v0.9.0 |
| **CoPaw (QwenPaw)** | 11 | 17 | 6 | v1.1.12.post2 | ✅ **Excellent** – High velocity + immediate community fixes |
| **PicoClaw** | 4 | 7 | 1 | v0.3.0-nightly | ⚠️ **Moderate** – Critical memory loss bug unpatched |
| **NanoClaw** | 0 | 5 | 0 | None | ✅ **Stable** – Quiet feature iteration |
| **NullClaw** | 2 | 1 | 0 | None | ✅ **Stable** – Platform-focused patching |
| **LobsterAI** | 1 (closed) | 0 | 0 | None | ❌ **Low** – No development activity |
| **TinyClaw / Moltis / ZeptoClaw** | 0 | 0 | 0 | None | ✝️ **Inactive** |

**Key Insight:** The top 6 active projects (OpenClaw, Hermes, NanoBot, IronClaw, ZeroClaw, CoPaw) represent the core of the ecosystem's innovation. OpenClaw dominates raw volume but shows signs of triage fatigue. NanoBot and CoPaw demonstrate the healthiest signal-to-noise ratio in community responsiveness.

---

## 3. OpenClaw's Position

**Role in the Ecosystem:**  
OpenClaw functions as the **de facto reference architecture** and broadest-scope implementation. It is the project against which others are benchmarked, both in feature breadth and community size.

**Advantages vs. Peers:**
- **Community scale:** Largest volume of issues and PRs by an order of magnitude (500/500 in 24h vs. 50/50 for the next highest).
- **Architectural rigor:** Active work on SQLite session migration ([#88838](#)), bounded memory semantics ([#90354](#)), and security hardening (API key encryption [#84738](#)).
- **Platform reach:** Most diverse channel list (Telegram, Matrix, Webchat, CLI) with active development across all.

**Technical Approach Differences:**
- Where Hermes focuses on Desktop UX (Electron, `/goal` commands) and NanoBot focuses on developer workflow (MCP, cron, subagent pipelines), OpenClaw distributes its effort across the entire stack—memory, gateway, providers, channels, and tool execution.
- This breadth is a double-edged sword. OpenClaw has P0 data loss ([#84882](#)) and an OOM leak ([#91588](#)) simultaneously, while more focused projects (NanoBot) address their critical issues within hours.

**Community Size Comparison:**
- OpenClaw's 500+ daily interactions dwarf other projects. The 453 open issues and 453 open PRs signal a community that is highly engaged but running into a **maintainer review bottleneck** (noted specifically in the digest's "clawsweeper" assessment).
- Hermes (v0.17.0, 245 contributors) shows stronger contributor diversity per release.
- NanoBot's community is smaller but exceptionally efficient—PRs opened within hours of bug reports (#4420→#4421).

**Risk:** OpenClaw's review bottleneck risks community fatigue. Items like `doctor --fix` performance regression ([#85333](#)) sitting stale for 29 days suggests that raw issue volume is outpacing maintenance capacity.

---

## 4. Shared Technical Focus Areas

These requirements are emerging simultaneously across **2+ projects** in the ecosystem:

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **Multi-Agent Orchestration & HITL** | NanoBot (#4411 SuspendTurn), Hermes (#49363 Delegate Task), OpenClaw (#63829 Per-Agent Vaults), IronClaw (#5061 Skill Evolution), ZeroClaw (#7759 Background Turns) | Human-in-the-loop pause/resume, subagent result aggregation, per-agent memory isolation |
| **Provider Compatibility & Resilience** | OpenClaw (#85103 Fallback Reliability, #95202 DeepSeek aliases), Hermes (#49297 Gemma 4/Ollama, #47868 Strict-mode metadata leaks), NanoBot (#4287 Empty response fallback), CoPaw (#5328 DeepSeek freeze, #5330 Zhipu connection) | Non-OpenAI strict-mode compliance, graceful handling of provider outages, model hot-swapping |
| **Memory & State Integrity** | OpenClaw (#84882 data loss, #91588 OOM), Hermes (#49307 Context compression corruption), CoPaw (#4795 ChromaDB 37GB leak), NanoBot (#4246 Session cleanup), ZeroClaw (#7907 State persistence ordering) | Bounded memory growth, crash-safe persistence, transactional state changes |
| **Security & Auth** | OpenClaw (#84738 API key encryption), Hermes (#4656 Credential Proxy), ZeroClaw (#7432 OIDC for v0.9.0), PicoClaw (#3143 SSRF), IronClaw (#5091 Feature Flags) | Credential management, SSRF prevention, role-based access, tenant isolation |
| **Channel Parity & Expansion** | All projects improving Discord/Telegram/Signal. Specific: NanoClaw (#2812 Discord chunking), ZeroClaw (#7965 Discord buttons), OpenClaw (#46656 Webchat buttons), NullClaw (#484 Feishu), CoPaw (#5329 Sidebar agent switcher) | Rich message support across all channels, interactive UI components |

**Conclusion on Shared Focus:** The ecosystem is converging on a **"Multi-Agent Operating System"** architecture: isolated memory spaces, structured approval workflows, resilient provider chaining, and cross-platform identity management. Projects that lag on any of these are likely to be overtaken.

---

## 5. Differentiation Analysis

| Project | Core Thesis | Target User | Unique Technical Bet |
|---|---|---|---|
| **OpenClaw** | **"Infrastructure-First Reference Platform"** | Developers building custom deployments | SQLite-based state management, `clawsweeper` triage, broadest provider/channel matrix |
| **Hermes Agent** | **"Consumer Desktop Agent Leader"** | Power users, desktop-first workflows | Electron desktop, rich Electron UX (Dashboard, `.venv` detection), Signal/BlueBubbles integration |
| **NanoBot** | **"Developer-First Workflow Engine"** | Devs automating complex pipelines | `SuspendTurn` async HITL, subagent aggregation, cron model presets, MCP timeout management |
| **IronClaw** | **"Multi-Tenant Enterprise Backend"** | Organizations with custom toolchains | OpenAI-compatible external tool endpoings, per-tool permission overrides, Reborn architecture |
| **ZeroClaw** | **"Enterprise Security & Channel Parity"** | Teams requiring compliance | OIDC auth (v0.9.0), Discord interaction components, strict agent lifecycle state control |
| **CoPaw (QwenPaw)** | **"China Ecosystem Powerhouse"** | Chinese-market developers | Deep integration with Zhipu, DeepSeek, LongCat-2.0; Tauri desktop; highly responsive UI iteration |
| **NullClaw** | **"Mobile / Minimalist Agent"** | Tinkerers on non-standard platforms (Android/Termux, local Ollama) | Zig build system, mobile-first focus, privacy-preserving local LLM path |
| **NanoClaw** | **"Apple Ecosystem & Compliance"** | macOS-focused teams | Apple Container runtime, parent-agent permission inheritance, approval audit trails |

**Strategic Observations:**
- **No project** has solved memory/data integrity perfectly. The entire ecosystem is vulnerable here.
- **NanoBot and CoPaw** demonstrate the strongest community feedback loops (< hours for fix PRs).
- **Hermes's giant v0.17.0** release (1,475 commits) is both a strength (rapid expansion) and a risk (integration surface for regressions).
- **LobsterAI, TinyClaw, Moltis, ZeptoClaw** are effectively dormant. The ecosystem is consolidating around the active players.

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity / Market Expansion
| Project | Signal | Velocity Grade |
|---|---|---|
| **Hermes Agent** | Just shipped v0.17.0 (235k lines changed), 245 contributors, active bug fix PRs | 🚀 **Hyper-expansion** |
| **CoPaw** | 6 PRs merged in 24h, multiple features opened and addressed same day (sidebar switch, model ordering) | 🚀 **Rapid iteration** |
| **NanoBot** | 19 PRs merged in 24h, user-reported token estimation bug fixed in hours | 🚀 **Developer-velocity leader** |
| **ZeroClaw** | 50 PRs updated, Discord interaction components merged, v0.9.0 OIDC auth planned | 🚀 **Approaching major security release** |

### Tier 2: Steady / Core Development
| Project | Signal | Velocity Grade |
|---|---|---|
| **OpenClaw** | High raw output, but bottlenecked. P0s coexisting with feature work | 🐢 **Volume leader, velocity bottleneck** |
| **IronClaw** | 12 PRs merged, strong internal team, Reborn architecture maturing | ✅ **Steady rebuild** |
| **PicoClaw** | Small team, niche features, critical bug unpatched (memory loss) | ⚠️ **At risk of stagnation** |
| **NullClaw / NanoClaw** | Quiet but targeted progress | ✅ **Maintenance mode** |

### Tier 3: Dormant / At Risk
| Project | Signal |
|---|---|
| **LobsterAI** | Zero PRs, only stale bug closures. AI Collaborator vision document with no maintainer response. |
| **TinyClaw, Moltis, ZeptoClaw** | No activity in 24h. Likely stalled. |

**Assessment:** The ecosystem is healthy in its core but ruthlessly pruning inactive projects. Maintainers should watch OpenClaw's bottleneck—if the community loses patience, Hermes or NanoBot could absorb significant mindshare.

---

## 7. Trend Signals

### 1. Memory as the Critical Infrastructure Layer
- **Signal:** Every major platform has a memory bug (deletion, leak, corruption, fallback failure).
- **Value for Developers:** Memory stability is the single highest-ROI contribution opportunity. A shared "Dream" / memory compaction library that works across providers would be ecosystem-defining.
- **Projects to watch:** OpenClaw's SQLite session migration; CoPaw's ChromaDB compact fix.

### 2. The "Non-OpenAI Provider Tax"
- **Signal:** DeepSeek, Gemma, Zhipu, and local models are causing disproportionate friction (400 errors, reasoning block mismatches, freezes, metadata leaks).
- **Value for Developers:** Provider abstraction layers and "strict-mode" compliance parsing are critical gaps. Tools that normalize API schemas between OpenAI, Anthropic, DeepSeek, and local endpoints will see high adoption.
- **Projects to watch:** NanoBot's fallback logic (#4287); Hermes's strict-mode debugging (#47868).

### 3. Human-in-the-Loop Becomes Table Stakes
- **Signal:** SuspendTurn (NanoBot), Approval modals (IronClaw, ZeroClaw), buttoned Discord approvals (ZeroClaw), async continuation.
- **Value for Developers:** The "chat as single turn" paradigm is dying. Building agents that can pause, gather input, and resume is now baseline.
- **Projects to watch:** NanoBot's SuspendTurn PR (#4411) is the most innovative approach.

### 4. Security & Auth Moving Out of "Nice-to-Have"
- **Signal:** OIDC (ZeroClaw), credential proxy (Hermes), API key encryption (OpenClaw), SSRF patching (PicoClaw).
- **Value for Developers:** Enterprise deployment requirements are trickling down to the open-source community. Removing `env::var` gating in favor of dynamic feature flags (IronClaw #5091) is the next step.
- **Projects to watch:** ZeroClaw's v0.9.0 umbrella (#7432).

### 5. Platform Gatekeeping is Failing
- **Signal:** Users are refusing to be locked into a single provider. CoPaw users run Zhipu + DeepSeek + LongCat. Hermes users run Ollama + OpenAI + Fireworks.
- **Value for Developers:** Modular provider adapters (like NanoBot's `tools.file.enable` toggle) are more important than deep integration with any single API.
- **Projects to watch:** OpenClaw's provider fixes; NanoBot's graceful degradation.

### 6. Channel UX Parity is the Last Mile
- **Signal:** Webchat buttons, Discord component parity, Telegram rich messages, Feishu card rendering. Users expect full interactive UI regardless of platform.
- **Value for Developers:** Don't launch a channel if you can't do buttons, rich cards, and streaming.
- **Projects to watch:** ZeroClaw's Discord interaction components (#7965); NanoClaw's Discord chunking (#2812).

---

## Final Recommendation for Ecosystem Observers

**Invest tracking effort in Hermes, NanoBot, and CoPaw** for the best signal-to-noise ratio in feature velocity and community satisfaction. **Watch OpenClaw closely** for its bottleneck resolution—if the maintainer team scales review capacity, it remains the dominant reference; if not, community fragmentation may accelerate. **Avoid building on stalled projects** (LobsterAI, TinyClaw, Moltis, ZeptoClaw) unless there is a clear maintainer succession plan. **Contribute to memory and provider compatibility tooling**—these are the highest-impact, least-solved problems across the entire landscape.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-06-20**, generated from the provided GitHub activity data.

---

## NanoBot Project Digest – 2026-06-20

### 1. Today’s Overview
NanoBot is in a high-velocity development sprint. Over the last 24 hours, **34 pull requests** were updated, with **19 merged or closed**, alongside 11 updated issues. The project is clearly in a stabilization and integration phase, with the maintainers showing exceptional responsiveness to community feedback—most notably resolving a reported token-estimation performance bottleneck within hours. Community focus is shifting from basic chatbot functionality toward advanced orchestration features, including human-in-the-loop pauses, multi-agent result aggregation, and per-run model overrides. No new releases were cut today, but the volume of merged code strongly suggests that a patch release is imminent.

### 2. Releases
**No new releases.** The latest stable version remains **v0.2.1**. Given the volume of merged PRs addressing regressions (stream stalls, cron spam) and new features (subagent aggregation, cron model presets), a v0.2.2 or v0.3.0 release tag is expected soon.

### 3. Project Progress
Key merged/closed pull requests from the last 24 hours:

- **File Tool Toggle** ([PR #4138](https://github.com/HKUDS/nanobot/pull/4138)): Added `tools.file.enable` flag, allowing operators to disable built-in filesystem tools in favor of external MCP servers, bringing parity with `exec` and `web` tool groups.
- **MCP Timeout Stability** ([PR #4230](https://github.com/HKUDS/nanobot/pull/4230)): Fixed an indefinite hang in the `streamableHttp` MCP transport by replacing the `timeout=None` client default with a strict timeout.
- **Session Cleanup Hygiene** ([PR #4246](https://github.com/HKUDS/nanobot/pull/4246)): Fixed a critical persistence bug where `delete_session` failed to remove legacy history files in the global `~/.nanobot/sessions/` directory, preventing deleted session history from "reviving."
- **Feishu Channel Parsing** ([PR #4342](https://github.com/HKUDS/nanobot/pull/4342)): Fixed three structural mismatches in Feishu card rendering for messages arriving via WebSocket.
- **OpenAI Image API Compliance** ([PR #4394](https://github.com/HKUDS/nanobot/pull/4394)): Correctly routes GPT image edit requests to `/images/edits` with multipart uploads, while keeping generation calls on `/images/generations`.

### 4. Community Hot Topics

- **Stream Stall Regression** ([Issue #4013](https://github.com/HKUDS/nanobot/issues/4013)) – *5 comments*  
  The most discussed issue. A user reports that the hardcoded 90-second timeout introduced in v0.2.0 makes long-thinking workflows unusable, requiring constant manual prompting. This reflects deep concern about rigid timeouts in the LLM call loop.

- **Workspace R/W Asymmetry** ([Issue #4374](https://github.com/HKUDS/nanobot/issues/4374)) – *3 comments*  
  A critical design bug for multi-project setups: `SOUL.md` and `USER.md` are read from the project workspace per-turn, but written back to the default workspace, leading to data divergence.

- **Human-in-the-Loop Pattern** ([PR #4411](https://github.com/HKUDS/nanobot/pull/4411)) – *High activity*  
  A highly innovative proposal for a `SuspendTurn` sentinel. This would allow tools to pause a turn cleanly for async continuation, signaling a strong community desire for advanced workflow orchestration beyond simple REACT loops.

- **Performance Immediate Response** ([Issue #4420](https://github.com/HKUDS/nanobot/issues/4420) / [PR #4421](https://github.com/HKUDS/nanobot/pull/4421))  
  A user flagged redundant `tiktoken` encoding of tool definitions on every call. A maintainer immediately opened a fix PR within hours, highlighting the project’s rapid feedback loop.

### 5. Bugs & Stability

| Severity | Issue | Summary | Status |
|---|---|---|---|
| **High** | [#4410](https://github.com/HKUDS/nanobot/issues/4410) | Regression: Heartbeat cron jobs deliver routine messages to the user even when explicitly instructed to stay silent. | **Open;** Fix PR [#4412](https://github.com/HKUDS/nanobot/pull/4412) in progress. |
| **High** | [#4013](https://github.com/HKUDS/nanobot/issues/4013) | Hardcoded 90-second LLM stream timeout renders the v0.2.x line unreliable for complex reasoning. | **Resolved** (closed as question/bug). |
| **Medium** | [#4287](https://github.com/HKUDS/nanobot/issues/4287) | Empty model responses (e.g., DeepSeek during peak hours) were not triggering fallback models. | **Resolved.** |
| **Medium** | [#4345](https://github.com/HKUDS/nanobot/issues/4345) | Image-stripping fallback leaked local file paths into the text prompt and made the model hallucinate "seeing" images. | **Resolved.** |
| **Low** | [#4052](https://github.com/HKUDS/nanobot/issues/4052) | MCP `notifications/progress` messages caused Pydantic validation errors. | **Resolved.** |

### 6. Feature Requests & Roadmap Signals

- **Per-Run Model Configuration:** Issues [#4389](https://github.com/HKUDS/nanobot/issues/4389) (per-model context windows) and [#4419](https://github.com/HKUDS/nanobot/issues/4419) (automatic reasoning effort escalation) are being actively implemented in PRs [#4416](https://github.com/HKUDS/nanobot/pull/4416) (cron job model presets) and [#4415](https://github.com/HKUDS/nanobot/pull/4415) (subagent model override). This signals a roadmap shift toward fine-grained, per-invocation provider configuration.

- **Subagent Orchestration:** PR [#4414](https://github.com/HKUDS/nanobot/pull/4414) proposes an "aggregated" result mode for subagents, buffering results and publishing them as a single combined message. This is a major signal for enterprise-grade task decomposition.

- **Async Human-in-the-Loop:** PR [#4411](https://github.com/HKUDS/nanobot/pull/4411) (`SuspendTurn`) is likely to be a flagship feature for the next release, enabling tool-execution pauses without terminating a conversation.

- **Channel Expansion:** The long-running XMPP PR ([#1945](https://github.com/HKUDS/nanobot/pull/1945)) remains active, while a new request for Telegram Bot API 10.1 rich messages ([#4413](https://github.com/HKUDS/nanobot/issues/4413)) indicates strong demand for native channel formatting.

### 7. User Feedback Summary

**Satisfaction:** Users continue to praise the WebUI and core agent logic ("it's been very good, way to say ty"). The project maintains a highly technical and constructive community that actively profiles and diagnoses problems (providing exact code lines and stack traces).

**Pain Points:**
- **Upgrade Regression Sensitivity:** The transition from v0.1.5 to v0.2.x has been rough for some users, specifically regarding stream timeouts ([#4013](https://github.com/HKUDS/nanobot/issues/4013)) and unwanted cron messages ([#4410](https://github.com/HKUDS/nanobot/issues/4410)).
- **Workspace Model Mismatch:** The asymmetry in how `SOUL.md` is read vs. written ([#4374](https://github.com/HKUDS/nanobot/issues/4374)) breaks the mental model for users managing multiple projects.
- **Cost Control:** Users are actively seeking ways to manage costs via better fallback logic ([#4389](https://github.com/HKUDS/nanobot/issues/4389)) and dynamic effort levels ([#4419](https://github.com/HKUDS/nanobot/issues/4419)).

### 8. Backlog Watch

- **[PR #1945 – XMPP Channel](https://github.com/HKUDS/nanobot/pull/1945) (~100 days)**  
  Opened March 12, 2026. This is the oldest significant feature branch, introducing the XMPP protocol. It requires a formal maintainer review and merge decision or a clear path forward.

- **[PR #3591 – Dream Update Scope](https://github.com/HKUDS/nanobot/pull/3591) & [PR #3590 – Manual Heartbeat Trigger](https://github.com/HKUDS/nanobot/pull/3590) (~49 days)**  
  Opened May 2, 2026. These provide essential user controls over the Dream memory consolidation system and cron scheduling. Their prolonged wait time suggests they may need conflict resolution or a final reviewer pass.

- **[PR #3662 – Token Estimation Caching](https://github.com/HKUDS/nanobot/pull/3662) (~45 days)**  
  Opened May 6, 2026. This PR attempts to avoid network loads and repeated file reads during token estimation. Given the spike in performance-related activity today directly targeting the `estimate_prompt_tokens` path ([#4420](https://github.com/HKUDS/nanobot/issues/4420)/[#4421](https://github.com/HKUDS/nanobot/pull/4421)), this branch has dramatically increased in relevance and should be re-evaluated for merge priority.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 20, 2026

## 1. Today's Overview
The day following the massive **v0.17.0 ("The Reach Release")** launch finds the project in an intense cycle of real-world stabilization and rapid patching. **50 issues and 50 pull requests** have been updated in the last 24 hours, with **7 PRs merged/closed** and **10 issues resolved** yesterday and today. While the release dramatically expands platform reach and desktop capability, the community has quickly surfaced critical regressions in session management, provider metadata compatibility, and local model support (notably Gemma 4 on Ollama). The development team and community contributors are actively responding with targeted fixes, many already open in the PR queue. Project velocity and community health are excellent, with deep technical debugging evident across all categories.

## 2. Releases
**Hermes Agent v0.17.0 (v2026.6.19) — "The Reach Release"**
- **Release Date:** June 19, 2026
- **Scale:** ~1,475 commits, ~800 merged PRs, 1,693 files changed (235,390 insertions, 50,730 deletions), 300+ issues closed, 245 community contributors.
- **Context:** This release builds directly on v0.16.0 and focuses on extending the agent's reach across more platforms, providers, and interaction modes.
- **Potential Breaking Changes / Migration Notes:**
  - The volume of changes (1,693 files) implies provider configuration changes. Ongoing user reports of metadata leaks (`[#47868](https://github.com/NousResearch/hermes-agent/issues/47868)`, `[#48523](https://github.com/NousResearch/hermes-agent/issues/48523)`) suggest that provider schema adherence may have been relaxed in this release, affecting users of strict-compliant non-OpenAI endpoints.
  - Users on Gemma 4 + Ollama should test carefully; issue `[#49297](https://github.com/NousResearch/hermes-agent/issues/49297)` reports that the bug persists despite the closure of its parent issue (`#39281`).

## 3. Project Progress
Seven pull requests were merged or closed in the last 24 hours. While the top 20 open PRs dominate the data, resolved issues provide strong signals of what shipped:

- **Platform Reliability Stabilization:**
  - Signal cron silent delivery failure (`[#49260](https://github.com/NousResearch/hermes-agent/issues/49260)`) — resolved.
  - WhatsApp bridge Docker dependency reinstall loop (`[#36641](https://github.com/NousResearch/hermes-agent/issues/36641)`) — resolved.
- **Desktop / CLI UX Fixes:**
  - `/goal` command swallowing in Desktop (`[#43476](https://github.com/NousResearch/hermes-agent/issues/43476)`) — resolved.
  - Dashboard `.venv` conflict detection (`[#21788](https://github.com/NousResearch/hermes-agent/issues/21788)`) — resolved.
- **Key Open PRs Imminent:**
  - Xiaomi MiMo vision analysis fix (`[#49389](https://github.com/NousResearch/hermes-agent/pull/49389)`) — directly addresses image degradation bug `[#49388](https://github.com/NousResearch/hermes-agent/issues/49388)`.
  - SQLite WAL state handling repair (`[#49354](https://github.com/NousResearch/hermes-agent/pull/49354)`) — strengthens database reliability.
  - Russian locale inclusion (`[#49387](https://github.com/NousResearch/hermes-agent/pull/49387)`) and Linux desktop launcher registration (`[#49384](https://github.com/NousResearch/hermes-agent/pull/49384)`).

## 4. Community Hot Topics
- **Security Architecture:**
  - `[#4656](https://github.com/NousResearch/hermes-agent/issues/4656)`: **Credential Proxy Daemon** (11 comments). Long-running, high-engagement discussion on zero-knowledge HTTP/HTTPS broker for agent credentials. Signals deep community interest in production-grade secrets management.
- **Local Model Compatibility:**
  - `[#45924](https://github.com/NousResearch/hermes-agent/issues/45924)` / `[#49297](https://github.com/NousResearch/hermes-agent/issues/49297)`: **Gemma 4 + Ollama failures** (5 + 3 comments, respectively). The most prominent user pain point. A user deliberately re-created the issue (`#49297`) because they felt the original (`#39281`) was closed without a fix. This is a significant community trust signal.
- **Ecosystem Strict Mode Enforcement:**
  - `[#47868](https://github.com/NousResearch/hermes-agent/issues/47868)` / `[#48523](https://github.com/NousResearch/hermes-agent/issues/48523)`: **Metadata leaks causing 400 errors** (3 + 2 comments). Users are actively debugging Hermes' protocol compliance against Fireworks-backed and strict OpenAI-compatible providers.
- **Desktop Feature Parity:**
  - `[#49363](https://github.com/NousResearch/hermes-agent/issues/49363)`: **Desktop dashboard plugin loading** (2 comments). A strong signal that users expect the Electron desktop to match the web dashboard's extensibility.

## 5. Bugs & Stability
**P1 (Critical)**
- `[#49361](https://github.com/NousResearch/hermes-agent/issues/49361)`: **Session Index Blindness** — The session index only tracks WhatsApp. All CLI/TUI sessions are invisible to `/session list` and auto-resume. Breaks core session management.
- `[#49307](https://github.com/NousResearch/hermes-agent/issues/49307)`: **Context Compression Corruption** — Causes answer repetition and loss of new instructions. Rated critical by the reporter.

**P2 (High)**
- `[#49297](https://github.com/NousResearch/hermes-agent/issues/49297)`: **Gemma 4 / Ollama broken in v0.17.0** — Persists despite the original issue being closed.
- `[#47868](https://github.com/NousResearch/hermes-agent/issues/47868)` / `[#48523](https://github.com/NousResearch/hermes-agent/issues/48523)`: **Strict Provider Metadata Leaks** — `timestamp`/`message_id` fields cause 400 errors.
- `[#49388](https://github.com/NousResearch/hermes-agent/issues/49388)`: **Xiaomi MiMo Vision Degradation** — Images silently degraded to text summaries. **Fix PR exists** (`[#49389](https://github.com/NousResearch/hermes-agent/pull/49389)`).
- `[#49386](https://github.com/NousResearch/hermes-agent/issues/49386)`: **Tool Policy Security Bypass** — `disabled_toolsets=["memory"]` is bypassed for external memory providers.
- `[#49345](https://github.com/NousResearch/hermes-agent/issues/49345)`: **Desktop GUI 'Start Gateway' Button Non-Functional** — Gateway cannot be started from the monitoring dashboard.
- `[#49332](https://github.com/NousResearch/hermes-agent/issues/49332)`: **Delegate Task Model Override Ignored** — `model` parameter has no effect; subagents always use the session default.
- `[#48991](https://github.com/NousResearch/hermes-agent/issues/48991)`: **Vision Provider Auto Broken** — Fails to inherit `base_url`/`api_key` for custom providers.

**P3 (Moderate)**
- `[#49326](https://github.com/NousResearch/hermes-agent/issues/49326)`: **Chinese IME Conflict** — Inputting commas/periods triggers settings panel.
- `[#49242](https://github.com/NousResearch/hermes-agent/issues/49242)`: **Windows Node PATH Priority** — WhatsApp gateway prefers system Node over Hermes-managed Node.
- `[#49293](https://github.com/NousResearch/hermes-agent/issues/49293)`: **Profile Switch Race Condition** — File browser doesn't update on profile switch.
- `[#23802](https://github.com/NousResearch/hermes-agent/issues/23802)`: **Plugin CLI Filters Bug** — Entry-point-discovered plugins filtered out by CLI `list`/`enable`.

## 6. Feature Requests & Roadmap Signals
Features rising in this snapshot suggest a clear direction for v0.18:

- **Project & Workspace Overhaul:**
  - `[PR #49037](https://github.com/NousResearch/hermes-agent/pull/49037)`: **First-class "Projects" with a backend-authoritative session tree.** A massive UX overhaul replacing git-branch inference with human-named project entities. The strongest roadmap signal in the data.
- **Desktop Maturation:**
  - `[#49363](https://github.com/NousResearch/hermes-agent/issues/49363)`: Plugin system parity for the Electron desktop app.
  - `[#49384](https://github.com/NousResearch/hermes-agent/pull/49384)`: Linux desktop launcher registration.
- **Platform Expansion:**
  - Zulip adapter (noted as superseding issue `[#49229](https://github.com/NousResearch/hermes-agent/issues/49229)` via PR #3335).
  - GLM-5.x reasoning support for the OpenCode Go profile (`[#49279](https://github.com/NousResearch/hermes-agent/issues/49279)`).
- **Cost & Performance Optimization:**
  - `[PR #49252](https://github.com/NousResearch/hermes-agent/pull/49252)`: Background self-improvement review routing to cheaper auxiliary models to cut token costs.
  - `[PR #46428](https://github.com/NousResearch/hermes-agent/pull/46428)`: Recursive large-context substrate tool for externalizing large files.

## 7. User Feedback Summary
- **Satisfaction:**
  - The community is deeply engaged and technically sophisticated. Many bug reports include complete root-cause analysis (e.g., `[#47868](https://github.com/NousResearch/hermes-agent/issues/47868)`, `[#49386](https://github.com/NousResearch/hermes-agent/issues/49386)`, `[#49388](https://github.com/NousResearch/hermes-agent/issues/49388)`).
  - v0.17.0 is being rapidly adopted and stress-tested against a very diverse provider and platform landscape (Ollama, OpenCode Go, Signal, BlueBubbles, Xiaomi MiMo).
  - Voluntary i18n contributions (Russian locale, `[PR #49387](https://github.com/NousResearch/hermes-agent/pull/49387)`) signal strong global community investment.
- **Dissatisfaction / Pain Points:**
  - **Gemma 4 user frustration** is the single loudest sentiment. The closing of `#39281` without a working fix, requiring users to re-open the issue (`#49297`), is likely to erode trust if not addressed promptly.
  - **Desktop rough edges** (Gateway button, profile switching, IME conflicts, `/goal` swallowing) suggest the Electron desktop rollout in v0.16/v0.17 still needs significant polish.
  - **Windows PATH management** for WhatsApp Node.js remains an unresolved friction point (`[#49242](https://github.com/NousResearch/hermes-agent/issues/49242)`).
  - **Provider strict-mode compatibility** breaks user workflows on non-OpenAI APIs, a growing concern as the model ecosystem diversifies.

## 8. Backlog Watch
Several important, older issues lack sufficient maintainer attention or linked fix PRs:

- `[#4656](https://github.com/NousResearch/hermes-agent/issues/4656)` — **Credential Proxy Daemon** (Created Apr 2, 11 comments). The most commented open feature request. A popular security infrastructure ask with no visible maintainer assignment or RFC. Risk of community fatigue if left unaddressed in the roadmap.
- `[#23802](https://github.com/NousResearch/hermes-agent/issues/23802)` — **Plugin CLI Filters Bug** (Created May 11, 3 comments). Entry-point-discovered plugins are invisible to the CLI. This breaks third-party plugin management entirely. A P3 bug that blocks fundamental plugin ecosystem growth.
- `[#25106](https://github.com/NousResearch/hermes-agent/issues/25106)` — **CLI Model Switch Persistence** (Created May 13). The `--global` model switch saves only partial state (missing `base_url`, `api_mode`). P2 but important for users who switch between local and remote providers frequently.
- `[#33327](https://github.com/NousResearch/hermes-agent/issues/33327)` — **BlueBubbles Webhook Conflicts** (Created May 27, 2 comments). A local fix branch exists but hasn't been merged. Delays could erode contributor morale.
- `[PR #34109](https://github.com/NousResearch/hermes-agent/pull/34109)` — **Holographic Memory Numpy Fallback** (Created May 28). Open for nearly a month. Adds warnings when numpy is missing so users aren't surprised by silent degradation. Simple UX fix languishing in review.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw Project Digest -- 2026-06-20**

---

### 1. Today's Overview
PicoClaw development proceeds at a moderate pace with 4 issues and 7 pull requests updated over the past 24 hours. A new automated nightly build (`v0.3.0-nightly.20260620`) was published, reflecting ongoing integration from the `main` branch. One fix has been merged, and several critical security and stability patches are in active review. Community engagement remains high, with users reporting a blocking memory-loss defect and pushing for long-standing platform compatibility fixes.

---

### 2. Releases
**New Release:** `v0.3.0-nightly.20260620.287853ab`
- This is an **automated nightly build** and may be unstable.
- Full changelog: [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)
- **Assessment:** No explicit breaking changes or migration notes are available for this snapshot. Users requiring stability should remain on the `v0.3.0` stable tag until a release candidate is cut.

---

### 3. Project Progress
- **Merged/Closed:**
  - [#2956](https://github.com/sipeed/picoclaw/pull/2956) (Closed) -- **fix: preserve channel enabled state when merging security.yml.** Resolves a bug where channels explicitly `enabled: true` in `config.json` were disabled after applying `.security.yml`.
- **Under Active Review:**
  - [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Open) -- **Feat/agent collaboration.** This large feature branch adds a durable inter-agent communication bus with per-agent mailboxes, collaboration threads, and structured message envelopes.
  - [#3143](https://github.com/sipeed/picoclaw/pull/3143) (Open) -- **fix(web): block private IPv4 embeds in ISATAP literals.** Addresses the SSRF bypass vulnerability reported in [#3074](https://github.com/sipeed/picoclaw/issues/3074).
  - [#3091](https://github.com/sipeed/picoclaw/pull/3091) / [#3053](https://github.com/sipeed/picoclaw/pull/3053) (Open) -- Unchecked type-assertion fixes for the OpenAI compat provider and Evolution store, preventing potential runtime panics.

---

### 4. Community Hot Topics
- **"Memory Loss" Bug ([#3150](https://github.com/sipeed/picoclaw/issues/3150))** -- A critical report claiming the AI assistant forgets its own context. This is the most urgent topic today, directly impacting core agent behavior. No linked fix PR yet.
- **Windows `list_dir` Failure ([#2472](https://github.com/sipeed/picoclaw/issues/2472))** -- The most commented issue (6 comments, 1 👍). Users are struggling with platform-specific path separator mismatches between Go's `os.DirFS` and the `list_dir` tool.
- **Telegram Channel Permission Control ([#3114](https://github.com/sipeed/picoclaw/issues/3114))** -- A well-received request (1 👍) to apply different capability sets based on chat type (private/group/channel) in Telegram. Reflects a growing demand for safe multi-user deployments.
- **Attachment Support ([#348](https://github.com/sipeed/picoclaw/issues/348))** -- This high-priority roadmap feature continues to draw discussion as users want to feed documents, code, and media across Telegram, Discord, and other channels.

---

### 5. Bugs & Stability
| Severity | Issue / PR | Summary |
|---|---|---|
| **Critical** | [#3150](https://github.com/sipeed/picoclaw/issues/3150) | AI agent memory module failure ("它给自己整失忆了"). No fix open. |
| **High (Security)** | PR [#3143](https://github.com/sipeed/picoclaw/pull/3143) | SSRF bypass via ISATAP IPv6 literals in `web_fetch`. Fix under review. |
| **High** | [#2472](https://github.com/sipeed/picoclaw/issues/2472) | Windows `list_dir` returning "invalid argument" due to `os.DirFS` path separator constraints. Open since April. |
| **Medium** | PR [#3045](https://github.com/sipeed/picoclaw/pull/3045) | Matrix `allow_from` parsing fails for standard IDs containing colons (e.g., `@alice:example.com`). |
| **Medium** | [#3091](https://github.com/sipeed/picoclaw/pull/3091) / [#3053](https://github.com/sipeed/picoclaw/pull/3053) | Unchecked type assertions in OpenAI compat and Evolution store causing potential panics. |
| **Resolved** | [#2956](https://github.com/sipeed/picoclaw/pull/2956) | Channel `enabled` state incorrectly overwritten by `.security.yml` merge. Merged. |

---

### 6. Feature Requests & Roadmap Signals
- **High Priority / Roadmap:** **General Attachment Support** ([#348](https://github.com/sipeed/picoclaw/issues/348)) -- This is the strongest near-term signal. Processing files, documents, and media across IM channels remains the top-requested functional gap.
- **Next Major Feature:** **Agent Collaboration Bus** ([PR #2937](https://github.com/sipeed/picoclaw/pull/2937)) -- A first-class internal messaging system with mailboxes and permission-aware agents. If merged, this could define the v0.4 roadmap.
- **Emerging Safety Requirement:** **Telegram Permission Control** ([#3114](https://github.com/sipeed/picoclaw/issues/3114)) -- As agent capabilities grow (exec, file access), the community is increasingly demanding granular "security boundaries" for groups and channels.

---

### 7. User Feedback Summary
- **Pain Points:**
  - **Windows Support:** The `list_dir` bug ([#2472](https://github.com/sipeed/picoclaw/issues/2472)) has been open for over two months, creating a significant barrier for Windows users.
  - **AI Instability:** The memory loss report ([#3150](https://github.com/sipeed/picoclaw/issues/3150)) represents a severe regression trust for current deployers.
  - **Deployment Safety:** Users are hesitant to deploy capable agents in shared spaces (Telegram groups) without proper permission scoping.
- **Use Cases:** The community is actively using PicoClaw as a cross-platform assistant, a file server, and an MCP host. The push for attachment and collaboration features suggests expansion into team or organizational workflows.
- **Satisfaction/Dissatisfaction:** The developer response is perceived as active, but user frustration is accumulating around the Windows bug and the memory regression.

---

### 8. Backlog Watch
- **Issue [#2472](https://github.com/sipeed/picoclaw/issues/2472) (Windows `list_dir`)** -- Stale since April. The longest-standing functional blocker. Requires abstraction-layer changes to support `os.DirFS` on Windows.
- **Issue [#3114](https://github.com/sipeed/picoclaw/issues/3114) (Telegram Permissions)** -- No maintainer triage or milestone assignment. Risks falling through the cracks despite clear community demand.
- **PR [#3048](https://github.com/sipeed/picoclaw/pull/3048) (MCP Flag Parsing)** -- Open since June 7 with no core review. A targeted fix for the `mcp add` subcommand.
- **PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Agent Collaboration)** -- Open since May 24. A very large branch that is at high risk of bit-rot without sustained review bandwidth from maintainers.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest based on the provided data.

---

## NanoClaw Project Digest – 2026-06-20

### 1. Today’s Overview
NanoClaw experienced a quiet day on the issue tracker with zero new reports or releases, yet development focus remains strong with five open pull requests active. Activity is concentrated around fixing data integrity issues in the approval system and expanding platform reach with an Apple Container runtime and remote gateway. The absence of merged PRs today suggests the team is consolidating these changes for a likely upcoming patch or minor release. Overall, the project is in a stable maintenance phase with steady feature iteration.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
No pull requests were merged or closed today. Several key open PRs advanced or remain under active review:

- **[#2820 – fix(approvals): persist delivery target on pending_approvals rows](https://github.com/nanocoai/nanoclaw/pull/2820)** (caburi00) — Fixes a critical data correctness bug where approval delivery targets are not recorded.
- **[#2812 – fix(discord): chunk replies over 2000 chars instead of truncating](https://github.com/nanocoai/nanoclaw/pull/2812)** (axnjxn415) — Wires the Chat SDK chunker into the Discord adapter to prevent silent truncation of long messages.
- **[#2809 – feat(apple-container): Apple Container runtime + remote OneCLI gateway](https://github.com/nanocoai/nanoclaw/pull/2809)** (hidenwalker) — Adds an env-gated `CONTAINER_RUNTIME` option to support macOS targets and remote gateway connections.
- **[#2605 – feat: inherit parent agent permissions via OneCLI](https://github.com/nanocoai/nanoclaw/pull/2605)** (guyb1) — A long-running feature PR adding hierarchical permission inheritance for multi-agent setups.
- **[#2819 – Add MseeP.ai badge](https://github.com/nanocoai/nanoclaw/pull/2819)** (mseep-ai) — Community contribution integrating a third-party security monitoring badge into the README.

### 4. Community Hot Topics
- **[#2605 – Inherit parent agent permissions](https://github.com/nanocoai/nanoclaw/pull/2605)** (guyb1) is the most notable item based on its longevity (open since May 24). It implies either a complex feature undergoing heavy review or a stalled approval workflow, making it the highest-traffic discussion item.
- **[#2812 – Discord message chunking](https://github.com/nanocoai/nanoclaw/pull/2812)** (axnjxn415) addresses a direct user experience pain point where long AI responses on Discord were silently cut off at 2,000 characters. This PR has likely generated positive attention from community members using the Discord channel.
- **[#2820 – Approval persistence gap](https://github.com/nanocoai/nanoclaw/pull/2820)** (caburi00) is a compliance-sensitive fix surfaced either by an enterprise user or an internal audit.

### 5. Bugs & Stability
No new bugs were filed in the issue tracker today. However, two significant fixes are currently under review via PRs:

- **High Severity**: `pending_approvals` rows are created with `NULL` values for `channel_type`, `platform_id`, and `platform_message_id` because delivery targets are never persisted after an approver is selected. This breaks the approval list view and audit trail. Fix open in [#2820](https://github.com/nanocoai/nanoclaw/pull/2820).
- **Medium Severity**: The Discord adapter does not pass `maxTextLength` to the Chat SDK Bridge, so the built-in `splitForLimit` chunker is never triggered on the platform. Any reply over 2,000 characters is silently truncated. Fix open in [#2812](https://github.com/nanocoai/nanoclaw/pull/2812).

### 6. Feature Requests & Roadmap Signals
No user feature requests were submitted as issues today, but the open PRs strongly signal the project’s roadmap direction:

- **Apple Container runtime & remote gateway** ([#2809](https://github.com/nanocoai/nanoclaw/pull/2809)) points to expanding beyond standard Docker into macOS-native execution and allowing agents to be accessed through remote OneCLI gateways. This is a strong candidate for inclusion in the next minor release.
- **Parent agent permission inheritance** ([#2605](https://github.com/nanocoai/nanoclaw/pull/2605)) addresses a clear organizational need for hierarchical permission management, suggesting demand from multi-tenant or team-based deployments.

### 7. User Feedback Summary
Direct user feedback in the issue tracker was absent today, but the active PRs reveal underlying pain points:

- **Dissatisfaction**: Users relying on the Discord adapter are experiencing truncated replies, a degraded experience addressed by [#2812](https://github.com/nanocoai/nanoclaw/pull/2812).
- **Compliance Needs**: Incomplete audit trails on approval workflows (PR [#2820](https://github.com/nanocoai/nanoclaw/pull/2820)) imply a need for robust record-keeping from enterprise/regulated users.
- **Platform Demand**: Interest in macOS deployment and remote gateways ([#2809](https://github.com/nanocoai/nanoclaw/pull/2809)) suggests a growing user base outside strict Linux/Docker environments.
- **Access Control**: The permissions feature ([#2605](https://github.com/nanocoai/nanoclaw/pull/2605)) indicates users are scaling up their agents and need better role management.

### 8. Backlog Watch
- **[#2605 – Inherit parent agent permissions](https://github.com/nanocoai/nanoclaw/pull/2605)** (guyb1, opened May 24) is the top item needing maintainer resolution. With no merge or closure for over three weeks, it may be blocked by design debates or scope concerns.
- **[#2819 – MseeP.ai badge](https://github.com/nanocoai/nanoclaw/pull/2819)** (mseep-ai) is a low-complexity, low-risk community integration. Merging this promptly could encourage further third-party security and monitoring contributions.
- No stale issues exist in the main tracker today, keeping the project’s open bug count healthy.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the project digest for NullClaw based on the provided GitHub data for 2026-06-20.

---

### 1. Today's Overview
On June 20, 2026, the NullClaw project saw moderate but focused activity centered on platform compatibility and local model stability. No new releases were published, but a significant bug affecting local Ollama users was resolved, and a targeted fix was opened for Android/Termux build failures. The project is currently in a stable phase where maintainers and contributors are actively patching platform-specific issues rather than introducing new features.

### 2. Releases
No new releases were published today.

### 3. Project Progress
Progress today was concentrated on resolving specific blocking issues across different platforms:
- **Resolved:** Issue **[#952](https://github.com/nullclaw/nullclaw/issues/952)** (Local model using Ollama returns incomplete answers) was closed. This directly addressed a core functionality regression for users running local LLMs.
- **In Progress:** Pull Request **[#966](https://github.com/nullclaw/nullclaw/pull/966)** was submitted to fix HTTP routing on `aarch64-linux-android` (Termux). This targets a fundamental connectivity issue blocking the build process on Android (linked to Issue #868).

### 4. Community Hot Topics
The community’s focus remains on cross-platform reliability and integration robustness:
- **[#952](https://github.com/nullclaw/nullclaw/issues/952): *Local model using ollama returns incomplete answers.** * (3 Comments) — This thread was highly active prior to its closure today. The underlying need is for reliable local inference without API dependencies.
- **[#484](https://github.com/nullclaw/nullclaw/issues/484): *飞书无法联网查询 (Feishu cannot connect to the internet).** * (3 Comments) — A persistent thread from the Chinese user base. The core demand is stable integration with popular regional enterprise tools (Lark/Feishu).
- **[#868](https://github.com/nullclaw/nullclaw/issues/868): *Zig build fails on Android/Termux.** * (2 Comments) — This is a critical blocker for mobile developers. The creation of PR #966 shows the community is trying to solve it, but the issue itself remains open pending maintainer review.

### 5. Bugs & Stability
- **High Severity – Blocked:**
    - **[#868](https://github.com/nullclaw/nullclaw/issues/868):** Build failure on Android/Termux (aarch64). The root cause is a missing `/etc/resolv.conf` in Termux, causing DNS failures. PR [#966](https://github.com/nullclaw/nullclaw/pull/966) proposes routing stdlib HTTP through cURL as a fix. This is the most critical stability issue currently open.
- **Medium Severity – Stale:**
    - **[#484](https://github.com/nullclaw/nullclaw/issues/484):** Feishu / Lark network query failure. Open for over 3 months. While not blocking the build, it represents a degraded experience for a specific integration.
- **Resolved:**
    - **[#952](https://github.com/nullclaw/nullclaw/issues/952):** The Ollama incomplete answer bug (high severity when active) has been closed.

### 6. Feature Requests & Roadmap Signals
User activity suggests the following roadmap priorities:
- **Enhanced Local LLM Support:** The swift closure of Issue #952 and the existing reliance on Ollama indicate that local inference is a core non-negotiable feature. Future releases will likely include better default prompts or timeout handling for local models.
- **Android / Termux as a First-Class Platform:** The effort behind PR #966 signals strong community demand for running NullClaw on mobile. We can expect the next version to include explicit support and documentation for Android deployment.
- **Enterprise Integration (Lark/Feishu):** Issue #484 is a low-noise but persistent signal that the Chinese enterprise market is an active user base. A fix or investigation into proxy handling for integrations is likely on the roadmap.

### 7. User Feedback Summary
- **Pain Points:** Users are experiencing friction when deploying NullClaw in non-standard environments. The top complaints are (1) instability of local Ollama models, (2) inability to compile on Android via Termux, and (3) broken connectivity for Lark/Feishu integrations.
- **Use Cases:** The data confirms three primary user personas: privacy-focused individuals running local models, tinkerers deploying agents on mobile hardware, and enterprise users in Asia integrating with internal chat platforms.
- **Satisfaction:** Sentiment appears mixed. The quick fix for #952 demonstrates strong responsiveness to clear-cut bugs. However, the longevity of Issue #484 suggests that regional or platform-specific issues may lack maintainer bandwidth or reproduction environment.

### 8. Backlog Watch
The following items require immediate maintainer attention:
- **PR [#966](https://github.com/nullclaw/nullclaw/pull/966):** *Route stdlib HTTP through curl on aarch64-linux-android*. This is the highest priority item on the board. It directly unblocks the Android build (Issue #868) and has been waiting for review since it was opened on 2026-06-19.
- **Issue [#484](https://github.com/nullclaw/nullclaw/issues/484):** *飞书无法联网查询*. Open since March 13, 2026. This issue is turning into a silent user churn risk for the Chinese community. It needs a maintainer to triage whether this is a config issue, a network proxy problem, or a core integration bug.
- **Issue [#868](https://github.com/nullclaw/nullclaw/issues/868):** *Zig build fails on Android/Termux*. While a PR exists to fix it, the issue itself should be kept under watch to ensure the proposed fix covers all failure modes (e.g., offline environments without curl).

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw Project Digest — 2026-06-20**

### 1. Today’s Overview
Development velocity on the IronClaw Reborn product suite was extremely high over the last 24 hours, with **30 pull requests** actively updated and **12 merged or closed**. The core team led by ilblackdragon, henrypark133, and serrrfirat pushed major phases of OpenAI-compatible external-tool support (#5099, #5094) and completed the long-running “Projects” frontend stack (#5019). Infrastructure and CI hardening continued aggressively, with serrrfirat shipping a wave of QA‑recorded fixtures (#5095, #5096) and build‑time experiments (#5092, #5090). New contributors made two high‑impact proposals—Telegram ingress (#5100) and skill self‑evolution (#5061)—signaling healthy community engagement. The project is clearly in a rapid‑iteration phase on the Reborn architecture with a strong investment in test and release infrastructure.

### 2. Releases
**No new releases** were published today. The project’s focus remains on completing the Reborn feature surface rather than cutting new distribution artifacts.

### 3. Project Progress
The day saw **12 PRs merged or closed**. Key items landed in the top‑20 list include:

- **Reborn Projects Launch** – [#5019 (5/5 Web UI)](https://github.com/nearai/ironclaw/pull/5019) closed, completing the frontend wiring for the Reborn Projects feature (CRUD + membership via `/api/webchat/v2/projects`). Post‑merge review fixes followed in [#5064](https://github.com/nearai/ironclaw/pull/5064).
- **QA & Test Infrastructure** – Three PRs from serrrfirat expanded the Reborn QA harness: [#5095](https://github.com/nearai/ironclaw/pull/5095) added committed LLM‑trace fixtures, [#5096](https://github.com/nearai/ironclaw/pull/5096) ported seven project‑setup benchmarks to record/replay, and [#5097](https://github.com/nearai/ironclaw/pull/5097) codified cross‑layer testing rules in AGENTS.md.
- **CI Performance** – [#5092](https://github.com/nearai/ironclaw/pull/5092) ran an A/B comparison of `sccache` vs. `Swatinem/rust-cache`, [#5090](https://github.com/nearai/ironclaw/pull/5090) extended the mold linker recipe to e2e/replay Rust jobs, and [#5098](https://github.com/nearai/ironclaw/pull/5098) wired the Reborn dependency closure into `nightly-deep-ci`.

### 4. Community Hot Topics
**Most Discussed Issues**
- [#5078 (CLOSED) – Approval modal diffficult for large commands](https://github.com/nearai/ironclaw/issues/5078) — *sunglow666*. Closed today, indicating a fix was accepted.
- [#5091 – Unified feature‑flag system for Reborn](https://github.com/nearai/ironclaw/issues/5091) — *ilblackdragon*. A strategic enhancement proposing per‑tenant targeting, dynamic switching, and graduated rollouts, reflecting internal needs for production deployment.
- [#5088 – “reads” shown as a shell command in approval prompts](https://github.com/nearai/ironclaw/issues/5088) — *think‑in‑universe*. A misleading UX sub‑issue of #4879; users are asking for clearer semantic tool naming in the approval UI.

**Most Active Pull Requests**
- [#5099 – External‑tool Responses round‑trip (Phase 4b‑4f)](https://github.com/nearai/ironclaw/pull/5099) — *ilblackdragon*. Completes the OpenAI‑compatible external‑tool flow; heavily awaited by developers integrating custom toolchains.
- [#5061 – Skill extraction & self‑evolution](https://github.com/nearai/ironclaw/pull/5061) — *krishna‑505* (new contributor). Brings Hermes‑style learning to Reborn; strong community interest in agent self‑improvement.
- [#5100 – Telegram ingress from extension state](https://github.com/nearai/ironclaw/pull/5100) — *abbyshekit* (new contributor). Immediate growth of Reborn’s platform reach.

**Underlying Needs**
Users need mature approval UX (large commands, clear tool names) and are demanding both agent extensibility (Telegram, Slack, external tools) and agent autonomy (skill evolution). The feature‑flag issue confirms that the team is already planning for multi‑tenant gate deployment.

### 5. Bugs & Stability
| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **High** | [#4108 – Nightly E2E failure](https://github.com/nearai/ironclaw/issues/4108) | Open since May 27 | No recurrence notes, but the volume of CI work suggests active diagnosis. |
| **Medium** | [#5088 – “reads” command in approval prompt](https://github.com/nearai/ironclaw/issues/5088) | Open | Misleading user‑facing text; lowers trust in permission visibility. |
| **Resolved** | [#5078 – Large‑command approval modal](https://github.com/nearai/ironclaw/issues/5078) | Closed | Fix merged, addressing a clear usability blocker. |

No critical crashes were reported. The team continues heavy investment in CI reliability (#5095, #5096, #5098), and the extended nightly‑deep‑CI infrastructure should catch regressions more comprehensively going forward.

### 6. Feature Requests & Roadmap Signals
**Explicit User/Core Requests**
- **Unified Feature Flags** ([#5091](https://github.com/nearai/ironclaw/issues/5091)) — The strongest roadmap signal today. This would unify ad‑hoc `env::var` gating into a dynamic, targeted system, a prerequisite for production multi‑tenant Reborn.
- **Per‑Tool Permission Overrides** ([#5062](https://github.com/nearai/ironclaw/pull/5062)) — Already in open PR; adds `always_allow`/`ask_each_time`/`disabled` states per tool capability.

**Likely Next‑Version Items**
- Completion of **OpenAI‑compatible endpoints** (`/v1/models`, external‑tool `function_call` projection in #5094, #5099).
- **Slack & Telegram bridges** (#5093, #5100) projected from extension state.
- **Concurrent turn execution** ([#5085](https://github.com/nearai/ironclaw/pull/5085)) paired with per‑user caps.
- **One‑shot scheduled triggers** ([#5065](https://github.com/nearai/ironclaw/pull/5065)).
- **Hosted Postgres profile** ([#5081](https://github.com/nearai/ironclaw/pull/5081)) for durable control‑plane state.

### 7. User Feedback Summary
**Pain Points**
- *Approval modal for large commands* (#5078): Users found the modal “difficult to review” when commands were long. Closed positively.
- *Misleading “reads” prompt* (#5088): Described as confusing and not reflecting actual user‑invoked commands or model capabilities.
- *Nightly E2E failures* (#4108): Undermining confidence in CI signal for almost a month.

**Use Cases Emerging**
- Platform integration (Slack, Telegram) via the new ingestion system.
- Agent self‑improvement through skill extraction (#5061).
- External tool orchestration through the OpenAI‑compatible Responses surface (#5099).

**Satisfaction Indicators**
New contributors are submitting large, well‑scoped feature PRs (skill evolution, Telegram ingress). The core team’s consistent tagging of `risk: low` on major feature PRs suggests experimental changes are being handled with care.

### 8. Backlog Watch
| Item | Age | Issue |
|------|-----|-------|
| [#4108 – Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108) | Since May 27 | Open, no explicit root‑cause update in the data window. Current CI work (#5098, #5095) should improve coverage but the immediate failure is unaddressed. |
| [#4002 – CI dependency updates](https://github.com/nearai/ironclaw/pull/4002) | Since May 24 | Dependabot PR with 16 action bumps; high merge‑conflict risk as it ages. |
| [#4829 – Retire reborn‑integration workflow](https://github.com/nearai/ironclaw/pull/4829) | Since June 12 | Housekeeping PR that has been open for over a week, risking conflicts with the parallel CI additions. **Maintainer attention needed** to merge or close. |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest | 2026-06-20

## 1. Today's Overview
The LobsterAI project exhibited a low-activity maintenance cadence on June 20. No code changes were submitted or merged via pull requests, and no releases were published. Project management efforts centered on back-office housekeeping, with three stale bug reports from April (Issues #1471, #1472, #1487) being closed. A single new item entered the tracker: a substantial feature vision document (Issue #2180) proposing a deep architectural evolution of the platform. Overall project velocity appears idle on the development front, though the tracker shows a technically engaged community actively submitting detailed UX bug reports and high-level roadmap ideas.

## 2. Releases
No new versions of LobsterAI (OpenClaw) were released in the last 24 hours.

## 3. Project Progress
Zero pull requests were opened, merged, or updated in this period. No features advanced or bugs were explicitly fixed via code integration. The closure of three stale issues represents the extent of observable progress, which is entirely a management signal rather than a development output.

## 4. Community Hot Topics
- **Python Skill Execution Disparity ([#1487](https://github.com/netease-youdao/LobsterAI/issues/1487)):** The most commented issue (3 comments) details a functional gap where Python scripts called within a LobsterAI session fail with a local 30B model, despite working correctly in Claude Code CLI and elsewhere. The underlying community need is for consistent tool-calling behavior across all backends, especially for users who rely on local models for cost or privacy reasons. This issue has been closed as stale.
- **Input State Management Bugs ([#1471](https://github.com/netease-youdao/LobsterAI/issues/1471), [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472)):** Both authored by *MaoQianTu*, these reports attracted moderate discussion (2 comments each) and represent significant UX friction. The core demand from the community is for a lossless, resilient text input system where navigating between views or editing history does not silently destroy user work. These were also closed as stale today.
- **No other issues or PRs generated significant reactions or comments in this window.**

## 5. Bugs & Stability
All three bugs active today were closed as stale. No associated fix PRs were identified, meaning the root causes may still exist in the codebase.

**Moderate–High Severity (UI Data Integrity):**
- **Input Draft Loss on View Switch ([#1471](https://github.com/netease-youdao/LobsterAI/issues/1471)):** The 300ms debounce mechanism for saving drafts fails to flush on component unmount, causing content loss when users navigate between sessions or views. This directly undermines user trust in the Cowork interface.
- **Unsent Input Overwrite ([#1472](https://github.com/netease-youdao/LobsterAI/issues/1472)):** Clicking "re-edit" on a historical message silently replaces the current unsent draft without a confirmation dialog. Users may lose carefully composed prompts without any recourse.

**Low Severity (Functional Parity):**
- **Python Script Execution Bugs ([#1487](https://github.com/netease-youdao/LobsterAI/issues/1487)):** Environment-specific issues with local models failing to call Python skills. Less severe given the specific hardware/software constraints.

## 6. Feature Requests & Roadmap Signals
- **"AI Collaborator" Proposal ([#2180](https://github.com/netease-youdao/LobsterAI/issues/2180)):** A single, very high-ambition feature request was opened by user *woxinsj*. The proposal includes a full design document advocating for a shift from low-level tooling to an "AI Collaborator" platform targeting non-elite programmers. Features proposed include a natural language command bar, a task dispatch console, cross-model orchestration, and project-level memory.
    - **Roadmap Prediction:** This is too expansive for a minor or patch release. It is more likely a community vision document. The maintainers may extract specific concepts (e.g., enhanced task dispatch or session memory) for future incremental work, or use it as a discussion catalyst for a major version roadmap. Currently has 0 maintainer responses.
- **No other new feature requests were observed, suggesting the feature backlog is either quiet or funneled elsewhere.**

## 7. User Feedback Summary
- **Pain Points:**
    - **Data Integrity Crisis:** The loudest signal from the community centers on losing work in the editor. The debounce and overwrite bugs (#1471, #1472) create an environment where users are wary of navigating the UI while composing input.
    - **Backend Tooling Parity:** Users running local models feel a functional gap in Python skill execution compared to cloud agents like Claude Code CLI (#1487), which imposes a ceiling on the usefulness of local deployments.
- **Satisfaction:**
    - No positive user sentiment or "thank you" type comments were captured in this 24-hour data window. The community's engagement is primarily through high-fidelity bug reports, suggesting a technically sophisticated user base that sets a high bar for software polish.

## 8. Backlog Watch
- **Stale Bug Closure (##1471, 1472, 1487):** All three were closed as stale today without a visible fix audit. If these bugs remain reproducible, the community may re-file them, generating double work and frustration. A maintainer note explaining the rationale (e.g., "fixed in vX.X", "cannot reproduce", "deprioritized for v2") would significantly reduce uncertainty.
- **Unanswered Vision Proposal (#2180):** The "AI Collaborator" proposal has zero comments. While it was posted only yesterday (June 19), a timely initial response from maintainers acknowledging the effort and outlining constraints would encourage continued community contribution at a strategic level.
- **Zero Open PRs:** Having no open pull requests in the tracker may indicate a high barrier to external contributions or a quiet development cycle. Maintainers may wish to review whether any in-flight features are being developed outside of the GitHub flow.

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

### CoPaw (QwenPaw) Project Digest – 2026-06-20

**Source Repository:** [agentscope-ai/QwenPaw](https://github.com/agentscope-ai/QwenPaw)

---

#### 1. Today's Overview

QwenPaw development and community engagement remained at a very high tempo today, with **11 issues** and **17 pull requests** receiving updates. Maintainers demonstrated strong responsiveness, opening companion PRs for the day’s most requested features (sidebar agent switching, custom model ordering) within hours of community submission. The project's balance of effort tilted heavily towards stabilization this sprint, with critical fixes merged for ChromaDB memory expansion, cron reliability, and context compaction timeouts. The pending volume of open PRs (11) suggests an imminent organizational push toward a new patch release.

---

#### 2. Releases

*No new releases were published today.* The latest version remains v1.1.12.post2 as referenced by recent bug reports. Given the high volume of merged fixes and open feature PRs, an early v1.1.13 release is likely being prepared.

---

#### 3. Project Progress — Merged/Closed PRs

Today's **6 closed/merged PRs** signal a strong focus on hardening the core:

- **Memory Stability** — [PR #5332](https://github.com/agentscope-ai/QwenPaw/pull/5332) (Merged) tackles the critical ChromaDB unbounded index growth bug from [Issue #4795](https://github.com/agentscope-ai/QwenPaw/issues/4795). Adds `compact_index()`, `purge_index()`, and auto-compact strategy with configurable thresholds.
- **Reliability** — [PR #5242](https://github.com/agentscope-ai/QwenPaw/pull/5242) (Merged) prevents context compaction from hard-freezing the agent by adding a timeout to `agent.reply()`. [PR #5241](https://github.com/agentscope-ai/QwenPaw/pull/5241) (Merged) resolves silent job failures by expanding the APScheduler misfire grace window from 60s to 3600s.
- **Skills & Collaboration** — [PR #5179](https://github.com/agentscope-ai/QwenPaw/pull/5179) (Merged) enhances `multi_agent_collaboration` trigger detection using expanded Chinese keyword matching.
- **Provider Compatibility** — Two iterative Zhipu model connection fix attempts ([PR #5337](https://github.com/agentscope-ai/QwenPaw/pull/5337), [PR #5338](https://github.com/agentscope-ai/QwenPaw/pull/5338)) were closed in review queue in favor of the ongoing refined approach in [PR #5339](https://github.com/agentscope-ai/QwenPaw/pull/5339).

---

#### 4. Community Hot Topics

The most active discussions today highlight Deepseek integration friction and strong demand for UI customization:

- **[Deepseek Agent Freeze](https://github.com/agentscope-ai/QwenPaw/issues/5328)** — This is the conversations cluster with the highest heat. Users consistently report agent stalling during the "thinking" phase, requiring manual stop/re-start. A correlated UX glitch [Issue #5333](https://github.com/agentscope-ai/QwenPaw/issues/5333) (UI fails to show stop button when agent is stuck) amplifies the frustration.
- **[UI Customization Demand](https://github.com/agentscope-ai/QwenPaw/issues/5329)** — The request for an agent switch button in collapsed sidebar mode immediately resonated with mobile users and was picked up by a maintainer within the same hour ([PR #5334](https://github.com/agentscope-ai/QwenPaw/pull/5334)).
- **[Model List Sorting](https://github.com/agentscope-ai/QwenPaw/issues/5267)** — Power users discussed the need to drag/reorder models within provider lists. Maintainer response was equally rapid ([PR #5336](https://github.com/agentscope-ai/QwenPaw/pull/5336)).
- **[Reasoning Block Format](https://github.com/agentscope-ai/QwenPaw/issues/5208)** — The 6-comment thread continues to explore how to handle the `type: "reasoning"` variant vs expected `thinking` blocks from OpenAI-compatible endpoints like LongCat-2.0-Preview.

---

#### 5. Bugs & Stability

The bug queue shows a project maturing rapidly with edge-case stability concerns.

| Severity | Issue | Summary | Fix Status |
|----------|-------|---------|------------|
| **Critical** | [#5328 / #5333](https://github.com/agentscope-ai/QwenPaw/issues/5328) | Agent stalls on Deepseek; UI stays in submit mode | Fix in [PR #5335](hhttps://github.com/agentscope-ai/QwenPaw/pull/5335) (Open) |
| **High** | [#5330](https://github.com/agentscope-ai/QwenPaw/issues/5330) | Zhipu models fail connection despite supplier-level test pass | Fix in [PR #5339](https://github.com/agentscope-ai/QwenPaw/pull/5339) (Open) |
| **High** | [#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) | Image preview broken in v1.1.12 (regression from FileResponse refactor) | Fix in [PR #5324](https://github.com/agentscope-ai/QwenPaw/pull/5324) (Open) |
| **High** | [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | ChromaDB 37GB unbounded index expansion | **Resolved** — [PR #5332](https://github.com/agentscope-ai/QwenPaw/pull/5332) merged |
| **Medium** | [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317) | Tauri/Windows fails to detect Python for skill execution | Awaiting triage |
| **Medium** | [#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208) | Assistant message count mismatch from reasoning block parsing | Ongoing discussion, no fix PR yet |
| **Resolved** | [#5319](https://github.com/agentscope-ai/QwenPaw/issues/5319) | Console "Answers have stopped" false positive | User-resolved by reinstall |

---

#### 6. Feature Requests & Roadmap Signals

User requests today were heavily oriented toward **workflow customization and management sophistication**, pointing to a user base that has moved past basic chat into complex orchestration.

**Highly Likely for Next Release (v1.1.13):**
- **Collapsed sidebar agent switcher** ([#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329) / [PR #5334](https://github.com/agentscope-ai/QwenPaw/pull/5334))
- **Custom model ordering within providers** ([#5267](https://github.com/agentscope-ai/QwenPaw/issues/5267) / [PR #5336](https://github.com/agentscope-ai/QwenPaw/pull/5336))
- **Inline file preview fix** ([#5320](https://github.com/agentscope-ai/QwenPaw/issues/5320) / [PR #5324](https://github.com/agentscope-ai/QwenPaw/pull/5324))

**Strong Roadmap Signals (next 1-2 releases):**
- **Context Management Redesign** — The new "Scroll" strategy ([PR #5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)) proposes replacing native compression with retrieval-driven durable history, a foundational architecture change.
- **Dashboard & Orchestration** — Simultaneous feature submissions for Agent Office chat-to-agent ([#5327](https://github.com/agentscope-ai/QwenPaw/issues/5327)), TodoWrite progress panels ([PR #5323](https://github.com/agentscope-ai/QwenPaw/pull/5323)), SSE push notifications ([PR #5331](https://github.com/agentscope-ai/QwenPaw/pull/5331)), and system tray minimization ([PR #5326](https://github.com/agentscope-ai/QwenPaw/pull/5326)) suggest a push to evolve QwenPaw into a full agentic operations center.

---

#### 7. User Feedback Summary

**Satisfaction Drivers:**
- Exceptional PR turnaround time on user-requested UI quality-of-life features (hours, not days).
- Clear documentation of regression root causes by maintainers (e.g., debugging Zhipu array-vs-string content format, FileResponse attachment disposition).

**Pain Points:**
- **Deepseek integration fragility** is the singular biggest user-reported workflow blocker. Users are having to constantly manually intervene ("stop and send continue").
- **v1.1.12 upgrade regressions** (image sending, memory indexing) eroded trust in the upgrade path, though rapid fix availability and manual workarounds (deleting `file_store/`) mitigated abandonment.
- **Windows/Tauri isolation** for Python skills remains a blocker for desktop Windows users wanting to execute custom code.

**Use Case Profile:**
The user base is clearly poly-provider, actively using non-OpenAI endpoints (Deepseek, Zhipu, LongCat-2.0). Users are pushing the tool beyond single-turn chat into persistent, multi-agent, skill-augmented task execution—and hitting the inevitable growth pains of that complexity.

---

#### 8. Backlog Watch

| Priority | Item | Issue | Status Signal |
|----------|------|-------|---------------|
| **High** | Tauri Python environment isolation (Windows) | [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317) | Only 1 maintainer comment; blocks core Skill execution for desktop users |
| **Medium** | Reasoning block type mismatch | [#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208) | Open since June 15; 6 comments but no fix PR linked. Root cause analysis is mature—needs code action |
| **Low** | Embedded ChromaDB link_list cleanup docs | Derived from [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | Fix is merged, but the root cause (`_next_link_list_id` overflow) should be documented to prevent recurrence in forks or upgrades |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

**ZeroClaw Project Digest — June 20, 2026**

**1. Today's Overview**
ZeroClaw development remains highly active as the team stabilizes the v0.8.x series while preparing the security overhaul planned for v0.9.0. Over the past 24 hours, 28 issues and 50 pull requests received updates, with 7 issues closed and 3 PRs merged. The project is currently addressing a cluster of critical regressions (S0/S1) involving agent lifecycle state persistence and channel lifecycle controls. No new releases were cut today, but the community is eagerly watching the response to the v0.8.0 Slack/Discord packaging regression.

**2. Releases**
No new releases were published on this date. The current stable track is v0.8.x.

**3. Project Progress**
- **Discord Interaction Surface Delivered:** A major feature milestone was reached with the merge of [#7965 — *feat(channels/discord): interaction components — buttons, selects, modals, buttoned approval, autocomplete*](https://github.com/zeroclaw-labs/zeroclaw/pull/7965). This completes Epic B of the Discord parity tracker [#7831](https://github.com/zeroclaw-labs/zeroclaw/issues/7831).
- **Ongoing Features in Flight:** The conversational onboarding assistant ([#8034](https://github.com/zeroclaw-labs/zeroclaw/issues/8034), PR [#8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033)) and the context window bar UI ([#7946](https://github.com/zeroclaw-labs/zeroclaw/pull/7946)) are progressing toward inclusion in the next minor release.
- **Test Coverage Expansion:** PRs [#8040](https://github.com/zeroclaw-labs/zeroclaw/pull/8040) and [#8037](https://github.com/zeroclaw-labs/zeroclaw/pull/8037) are actively narrowing test gaps in runtime tool execution ordering and OpenAI responses-wire option propagation.

**4. Community Hot Topics**
- **🔐 High Engagement on OIDC Auth:** Issue [#7141 — *OIDC Authentication Provider support*](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) continues to draw sustained interest as the community's most requested security feature, confirmed as the P1 target for v0.9.0.
- **📦 Slack/Discord Binary Regression:** Issue [#7787 — *Prebuilt v0.8.0 binaries ship without Slack/Discord channel features*](https://github.com/zeroclaw-labs/zeroclaw/issues/7787) has forced users to downgrade to v0.7.5, generating multiple comments and 👍 reactions. This is driving the request for "full-channel" prebuilt bundles ([#7952](https://github.com/zeroclaw-labs/zeroclaw/issues/7952)).
- **📱 Android Platform Demand:** The Android Termux setup issue ([#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911)) is a strong signal from power users seeking broader deployment coverage for headless Linux environments.

**5. Bugs & Stability**
- **S0 — Data Loss / Security Risk:**
  [#8013 — *Disabling an agent does not stop its bound Discord channel*](https://github.com/zeroclaw-labs/zeroclaw/issues/8013) — Accepted. A critical failure of the agent disable control, leaving channels active. No fix PR yet.
- **S1 — Workflow Blocked (State Corruption):**
  [#7907 — *Agent rename moves owned state before config persistence*](https://github.com/zeroclaw-labs/zeroclaw/issues/7907) — Open, P1.
  [#7941 — *Agent delete purges owned state before config persistence (mirror of #7907)*](https://github.com/zeroclaw-labs/zeroclaw/issues/7941) — Open, P1.
  These two bugs represent an ordering defect in the gateway API that can result in data loss during rename/delete operations.
- **S2 — Degraded Behavior:**
  [#8039 — *fill-translations leak-repair leaves orphaned continuation lines*](https://github.com/zeroclaw-labs/zeroclaw/issues/8039) — Now fixed on master via [#7869](https://github.com/zeroclaw-labs/zeroclaw/pull/7869).
  [#7964 — *Context compression summary model is provider-sepecific on a shared runtime profile*](https://github.com/zeroclaw-labs/zeroclaw/issues/7964) — Accepted, P2. Fix PR [#7973](https://github.com/zeroclaw-labs/zeroclaw/pull/7973) is open but stalled.

**6. Feature Requests & Roadmap Signals**
- **v0.9.0 Security Architecture:** The umbrella tracker [#7432 — *v0.9.0 auth, security, gateway, and breaking-change queue*](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) is active, packing OIDC auth ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) and legacy cursor deprecation ([#8012](https://github.com/zeroclaw-labs/zeroclaw/issues/8012)).
- **v0.8.3 Web Dashboard:** Tracker [#7320 — *MCP dashboard and web/plugin-management surfaces*](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) is the near-term focus for the web experience.
- **Background Turn Execution:** Issue [#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759) proposes decoupling WebSocket lifetime from agent turn lifecycle — a roadmap signal for major web UX improvements (queue P1).
- **Slash Command Unification:** The RFC [#7929](https://github.com/zeroclaw-labs/zeroclaw/issues/7929) to unify the three separate slash-command registries suggests an architecture push toward consistency across the web dashboard, TUI, and channels.

**7. User Feedback Summary**
- **Pain Points:**
  - v0.8.0 forcing downgrades to regain Slack/Discord support ([#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787)).
  - Android Termux binary completely failing to install ([#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911)).
  - Agents unable to answer questions about themselves due to lack of docs in Docker images ([#7950](https://github.com/zeroclaw-labs/zeroclaw/issues/7950)).
- **Satisfaction Signals:**
  - The community is responding well to the rapid closure of the Matrix channel memory leak ([#6651](https://github.com/zeroclaw-labs/zeroclaw/issues/6651)).
  - Completion of Discord interaction components ([#7965](https://github.com/zeroclaw-labs/zeroclaw/pull/7965)) positions ZeroClaw as a premier Discord agent platform.

**8. Backlog Watch**
- **Stalled PRs Needing Author Action:**
  [#6693 — *feat(memory): add dream mode for periodic memory consolidation*](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) (35 days stalled).
  [#7922 — *feat(channels/discord): slash command localizations + guild scope*](https://github.com/zeroclaw-labs/zeroclaw/pull/7922) (2 days stalled, needs-author-action).
  [#7973 — *fix(agent): self-contained context-compression summary provider*](https://github.com/zeroclaw-labs/zeroclaw/pull/7973) (1 day stalled, needs-author-action).
- **Awaiting Maintainer Review:**
  [#7952 — *Feature: publish full-channel prebuilt assets*](https://github.com/zeroclaw-labs/zeroclaw/issues/7952) (needs-maintainer-review).
  [#7929 — *Feature: Unify slash-command registries (RFC)*](https://github.com/zeroclaw-labs/zeroclaw/issues/7929) (needs-maintainer-review).
- **Deprecation Risk:** The legacy log cursor removal ([#8012](https://github.com/zeroclaw-labs/zeroclaw/issues/8012)) may affect downstream tooling if overlooked during the v0.9.0 migration.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*