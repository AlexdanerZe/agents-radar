# OpenClaw Ecosystem Digest 2026-05-27

> Issues: 379 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-27 03:30 UTC

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

Here is the structured project digest for OpenClaw based on the provided GitHub activity for 2026-05-27.

---

## OpenClaw Project Digest — 2026-05-27

### 1. Today's Overview
OpenClaw saw an extremely high volume of activity in the last 24 hours, with **379 issues and 500 PRs** updated. The project remains in an intense beta cycle, shipping two patches (`v2026.5.25-beta.1` and `v2026.5.26-beta.1`) focused on startup performance and iMessage reliability. However, the high velocity of architectural changes is generating significant community friction, with multiple **P1 regression reports** across core systems, particularly around the Windows daemon, Codex OAuth integration, and subagent orchestration stability. While the maintainers are actively merging fixes for session-state and memory leaks, the rapid cadence of `.x` releases is forcing some users to pin specific "known good" versions.

### 2. Releases
Two new beta releases were published.

- **v2026.5.26-beta.1:** Targets performance optimization. Delivery logic is now decoupled, meaning user-facing replies are sent immediately while slower follow-up work runs in the background. Hot paths for command/model/plugin metadata are cached to reduce redundant lookups, and Gateway startup no longer repeatedly scans plugins, channels, sessions, and filesystems.
- **v2026.5.25-beta.1:** A targeted bugfix release for the iMessage channel. Inbound attachments saved under `~/Library/Messages/Attachments` (including wildcard roots) are now staged through the proper inbound path policy instead of being rejected.
- **Migration/Compatibility Watch:** The massive open refactors—**#81402** (Move runtime state to SQLite) and **#85341** (Internalize agent runtime)—represent significant architectural shifts. Operators should monitor these closely before upgrading from the current `.x` series to a future stable release.

### 3. Project Progress
Multiple high-priority fixes were merged or advanced today, addressing deep-seated stability and feature parity gaps:

- **Subagents & Runtime:** `openclaw/openclaw PR #87138` (closed) strips invalid empty thinking signatures from Anthropic sessions. `openclaw/openclaw PR #85811` (closed) ensures Codex native subagents follow the same workspace bootstrap boundary as Pi subagents.
- **Approvals & Security:** `openclaw/openclaw PR #86771` / `openclaw/openclaw PR #87131` (closed) repair local approval resolution to prevent operator authorization scope creep. `openclaw/openclaw PR #87124` enforces the hook agent allowlist when `agentId` is omitted.
- **Infrastructure:** `openclaw/openclaw PR #86345` (closed) bounds the `INDEX_CACHE` lifetime in memory-core to prevent file descriptor accumulation in long-running daemons. `openclaw/openclaw PR #87134` fixes the Windows Gateway daemon crash when switching from AC to battery power.
- **UI/UX:** `openclaw/openclaw PR #86939` (closed) fixes the webchat run-status label being permanently stuck on "In progress". `openclaw/openclaw PR #86270` hardens the Control UI against stale approval prompts.

### 4. Community Hot Topics
The data reveals a highly engaged but stressed user base testing complex workflows with frontier models.

- **Top Feature Demand — Native Desktop Apps:** `openclaw/openclaw Issue #75` remains the single most requested feature with **109 comments and 77 👍**, showing a strong community desire for Linux and Windows apps matching the existing macOS feature set.
- **Alpha/Beta Reliability Pain:** `openclaw/openclaw Issue #44925` (Subagent results silently lost, 18 comments) and `openclaw/openclaw Issue #86827` (Group chat stuck in "failed" state) highlight core orchestration reliability issues. Users are heavily testing asynchronous and multi-agent workflows.
- **Model Compatibility:** `openclaw/openclaw Issue #68596` (14 comments, 8 👍) requesting a configurable streaming watchdog timeout reflects the friction users face when deploying extended-reasoning models like DeepSeek R1 and Kimi K2.5.
- **Platform Volatility:** Windows users are particularly vocal, with `openclaw/openclaw Issue #86599` confirmed as a beta blocker due to event loop blocking on local model calls.

### 5. Bugs & Stability
Stability is the dominant theme today, with several P1 regressions reported alongside active fixes.

**Beta Blockers / Critical (P1 — High Impact):**
- **Windows Gateway Blocking:** `openclaw/openclaw Issue #86599` — Local model provider calls block the gateway event loop on Windows beta, taking ~4 minutes for trivial inference.
- **Codex Turn Drops:** `openclaw/openclaw Issue #86948` — The Codex app-server silently drops turns after 1-4 successful interactions due to event loop saturation.
- **File Descriptor Leak:** `openclaw/openclaw Issue #86613` — Every `memory_search` call leaks one FD per `.md` file in the workspace, threatening long-running gateways with exhaustion. *Fix PR #86345 is closed.*
- **Event Loop Starvation Regression:** `openclaw/openclaw Issue #86509` — Regressed in v2026.5.22, users forced to roll back to 5.20.

**High Severity (P1 — Functional Blockers):**
- `openclaw/openclaw Issue #86820` — Codex OAuth compaction falls back to direct API and fails without an explicit key.
- `openclaw/openclaw Issue #85030` — MCP tools are not injected into subagent (`sessions_spawn`) sessions despite proper configuration.
- `openclaw/openclaw Issue #85953` — `sessions_yield` leaves the parent session transcript lock held, causing subagent timeout.
- `openclaw/openclaw Issue #86758` — Hardcoded 30s RPC timeout breaks `session_status` and enumeration-heavy MCP tools.
- `openclaw/openclaw Issue #84880` — `v2026.5.19` still rejects non-off `thinking` for subagent spawns on Codex models.

**Resolved/Mitigated:**
- `openclaw/openclaw Issue #84604` (4.x → 5.x Claude harness migration) — Closed.
- `openclaw/openclaw Issue #86746` (Default `toolResultMaxChars` too small for frontier models) — Closed.
- `openclaw/openclaw Issue #84607` (No auto-retry on overloaded model) — Closed.

### 6. Feature Requests & Roadmap Signals
The roadmap is signaling a pivot towards consolidation and a standard execution layer.

- **Near-Term (Active PRs):** The **Channel Broker Phase 3** (`openclaw/openclaw PR #86164`) aims to consolidate recurring maintenance churn across Telegram, Discord, Slack, and WhatsApp into a single contract. The **Exec Auto Mode** (`openclaw/openclaw PR #70543`) unifies the approval surface between native OpenClaw exec and Codex.
- **Strategic (Mega Refactors):** The **Internalize Runtime** (`openclaw/openclaw PR #85341` by steipete) and **Move Runtime State to SQLite** (`openclaw/openclaw PR #81402`) are massive efforts aimed at killing off the long-standing session-state and race-condition bugs by abandoning JSON/file-based state.
- **User Requests:** Beyond the perennial desktop app demand (`#75`), users are requesting practical quality-of-life improvements: `openclaw/openclaw Issue #50093` (WhatsApp message backfill), `openclaw/openclaw Issue #38626` (Subagent lifecycle observability), and `openclaw/openclaw Issue #86237` (Renaming the `cron` subsystem to avoid system cron conflicts).

### 7. User Feedback Summary
The community is deeply engaged in testing but showing signs of upgrade fatigue.

- **Dissatisfaction Drivers:** The primary complaints revolve around **silent failures** (subagents, session drops) and **performance regressions** between rapid releases. Users are actively maintaining "known good" version pinning and local `BLOCKED_VERSIONS` lists to avoid specific builds (e.g., `#80695`, `#86509`). Windows remains a clear pain point.
- **Use Case Maturity:** Users are demanding professional-grade features. Requests for configurable timeouts, message backfill after reconnection, OLTP-style observability for subagents, and reliable wall-clock time for cron jobs indicate the tooling is being used for serious production purposes, not just casual chat.
- **Positive Engagement:** Despite the churn, the volume of detailed bug reports and high-quality feature requests (e.g., iOS app direction `openclaw/openclaw Issue #85731`) demonstrates a highly vested and technically sophisticated user base actively contributing to the project's trajectory.

### 8. Backlog Watch
These important issues and PRs require specific maintainer attention or direction.

- **The Desktop App Gap (`openclaw/openclaw Issue #75`):** The #1 community request for over 5 months remains open without a visible development PR. While iOS and Android apps exist, the lack of Windows/Linux parity is a growing blind spot.
- **Core Reliability Debt:**
    - `openclaw/openclaw Issue #45952` (Webchat messages lost on reconnect) — Open since March, a very basic ACK protocol deficiency.
    - `openclaw/openclaw Issue #50093` (WhatsApp backfill) — Open since March, key for business use cases.
    - `openclaw/openclaw Issue #76104` (Feishu `sessions_send` routing) — A specific channel bug that affects a growing user segment.
- **Strategic Direction:** `openclaw/openclaw PR #81402` (SQLite) and `openclaw/openclaw PR #85341` (Internalize Runtime) are high-risk, high-reward. The community needs a clear signal on whether this is the definitive architectural path forward to avoid confusion over the influx of session-state bugfix PRs that may be obsoleted.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: Personal AI Agent Landscape
**Generated:** 2026-05-27

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape on May 27, 2026, is in a high-velocity build-out phase, transitioning from chat wrapper architectures toward complex, autonomous agentic platforms. The sheer volume of activity—dominated by OpenClaw's unprecedented 379 issues and 500 PRs updated in a single day—signals a field under immense competitive pressure, where shipping speed often outstrips stability. Across all active projects, a clear consensus is emerging on the core challenges: deterministic subagent orchestration, provider-agnostic resilience, MCP protocol maturity, and ironclad tool execution security. While community engagement is at an all-time high, user frustration with beta churn, platform regressions, and silent failures is generating distinct "version pinning" behaviors, particularly in the OpenClaw and CoPaw ecosystems. The ecosystem is clearly dividing into general-purpose orchestration platforms (OpenClaw, IronClaw, ZeroClaw) and specialized, opinionated agents (CoPaw, Hermes, Moltis).

---

## 2. Activity Comparison Table

| Project | Issues Updated | PRs Updated | Latest Release | Ecosystem Role | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 379 | 500 | v2026.5.26-beta.1 | Core Reference Monolith | **Stressed High Velocity** — P1 regressions, version pinning fatigue, massive refactors |
| **IronClaw** | 16 | 50 | v0.29.0 | Security/Enterprise Platform | **High Velocity, Production Strain** — crates.io block, background agent failures, Reborn migration |
| **CoPaw (QwenPaw)** | 33 (11 closed) | 29 (8 merged) | v1.1.9-beta.1 | Developer/IDE Focus | **Feature-Rich, Beta Fatigue** — macOS crash, ToolGuard bypass, but strong coding mode |
| **ZeroClaw** | 6 | 34 (5 merged) | None | Autonomy/Skills Platform | **High Cadence, Blockers Persist** — DeepSeek-V4 broken (33d), major TUI/Beta-2 branch in flight |
| **Hermes Agent** | 50 (20 duplicates) | 50 (15 merged) | None (patch imminent) | CLI/TUI Specialist | **Crisis Averted, Debt Lingers** — Codex crash fixed fast, MCP bypass & vision tool unresolved |
| **PicoClaw** | Few | 13 merged | v0.2.9-nightly | Embedded/Lightweight | **Healthy, Contributor-Driven** — Rapid merges, agent overhaul, API fragmentation fighting |
| **NanoBot** | 4 (1 critical) | 19 (6 merged) | v0.2.0 | Research Sandbox | **Innovative, Critical Regression** — Stream timeout blocks v0.2.0 users; great vision pipeline |
| **LobsterAI** | 0 new | 12 (9 merged) | None | OpenClaw Integrator | **Stable, Healthy** — Zero new bugs, deep OpenClaw skill sync |
| **Moltis** | 2 | 2 (1 merged) | None | Security/Privacy Focus | **Emerging, Low Volume** — Architectural changes merged, partnership inquiry received |
| **NanoClaw** | 0 | 4 (1 merged) | None | Maintenance | **Very Healthy** — Zero backlog, fast fix turnaround, healthy CI |
| **NullClaw** | 0 | 2 (1 merged) | None | Rust Maintenance | **Quiet, Stable** — One infrastructure fix merged, Nix build pending |
| **ZeptoClaw** | 0 | 16 (all Dependabot) | None | Niche | **Dormant** — 0 human activity, only automated dependency bumps |
| **TinyClaw** | 0 | 0 | None | Dormant | **Inactive** — No activity in reporting window |

---

## 3. OpenClaw's Position

**Scale Advantage:** OpenClaw remains the undisputed hub of the ecosystem. Its single feature request for native desktop apps (#75) has more engagement (77 👍, 109 comments) than the total daily activity of most other projects. This community gravity creates a robust plugin/channel ecosystem that no peer can match.

**Technical Approach:** OpenClaw is evolving into a vast orchestration monolith. Its massive concurrent refactors—**#81402 (Move runtime state to SQLite)** and **#85341 (Internalize agent runtime)** —are high-risk bets to kill long-standing session-state corruption bugs. This contrasts sharply with IronClaw's Rust-based security-first architecture or Moltis's minimal single-binary approach.

**Peer Advantages:**
- **vs IronClaw:** Open governance, wider channel support, larger plugin/skill ecosystem.
- **vs PicoClaw:** Reference implementation status, broader enterprise mindshare.
- **vs CoPaw/Hermes:** Significantly larger contributor base and feature surface area (iMessage, Feishu, WhatsApp).

**Critical Vulnerabilities:**
- **No Native Desktop Client (#75):** The #1 community request remains unmet for 5+ months. This is a strategic gap exploited by CoPaw (iOS/Android, Tauri desktop) and Hermes (TUI session orchestrator).
- **Release Cadence Fatigue:** Users are actively maintaining `BLOCKED_VERSIONS` lists against specific betas (5.22, 5.20). The rapid `.x` releases are eroding trust in the "latest" label.
- **Windows Gap:** The Windows Gateway daemon blocking (#86599) and event loop saturation (#86509) are making the platform effectively unreliable for a major OS segment.

---

## 4. Shared Technical Focus Areas

The following requirements emerged *simultaneously* across multiple independent projects, representing systemic ecosystem needs:

| Requirement | Projects Affected | Specific Signals |
|---|---|---|
| **Reliable Subagent Orchestration** | OpenClaw, IronClaw, NanoBot, ZeroClaw, Moltis | OpenClaw #44925 (results lost), IronClaw #4084 (never delivered), NanoBot #3992 (cross-instance bus), ZeroClaw #6688 (injection mode ignored) |
| **Provider Abstraction & Resilience** | OpenClaw, PicoClaw, ZeroClaw, CoPaw, Hermes | DeepSeek-V4 blocking ZeroClaw 33d (#6059), MiniMax XML breaking CoPaw (#4625), Anthropic deprecations breaking PicoClaw, Codex crash at Hermes (#11179) |
| **MCP Security & Tool Gates** | Hermes, CoPaw, IronClaw, OpenClaw | Hermes #32877 (MCP bypass), CoPaw #4709 (ToolGuard bypass), IronClaw #3931 (cross-tenant leakage), OpenClaw #86771 (approval scope) |
| **Session State Durability** | OpenClaw, CoPaw, IronClaw, NanoClaw | OpenClaw #45952 (messages lost on reconnect), CoPaw #4706 (JSON corruption on crash), IronClaw #3281 (EventStreamManager), NanoClaw #2622 (marketplace updates ignored) |
| **Desktop & UI Maturity** | OpenClaw, ZeroClaw, Hermes, CoPaw, PicoClaw | OpenClaw #75 (desktop apps), ZeroClaw #6848 (zeroCode TUI), Hermes #32980 (TUI orchestrator), CoPaw #4662 (timestamps, diff editor) |
| **Cross-Platform Portability** | OpenClaw, PicoClaw, CoPaw, NullClaw | OpenClaw Windows blocking, PicoClaw RISC-V/Termux, CoPaw macOS Tahoe crash, NullClaw Nix/Zig compatibility |

---

## 5. Differentiation Analysis

### Feature Focus Variance

| Project | Primary Differentiator | Secondary Focus |
|---|---|---|
| **OpenClaw** | Channel breadth + Plugin ecosystem | Subagent orchestration |
| **IronClaw** | Attested signing + Enterprise security | Hooks framework, Reborn platform |
| **CoPaw (QwenPaw)** | Coding mode (diff editor, stop signals) | Audio/image processing, Feishu |
| **ZeroClaw** | Autonomous skills (background review, cooldowns) | TUI experience, Beta-2 protocol |
| **Hermes Agent** | CLI/TUI power user experience | Provider crash recovery speed |
| **PicoClaw** | Embedded/Linux/Termux friendliness | Contributor RPM, channel features (WeChat, Telegram Business) |
| **NanoBot** | Multi-agent bus, Dream system, self-correction | Research flexibility |
| **Moltis** | Single-binary sandboxing, per-agent capabilities | Privacy, simplicity |

### Target User Base

- **General Developers / Enterprise:** OpenClaw, IronClaw
- **Terminal Power Users / Tinkerers:** Hermes Agent, ZeroClaw
- **IDE-Integrated Developers:** CoPaw (QwenPaw)
- **Edge Device / Embedded Users:** PicoClaw
- **Researchers / Advanced Architects:** NanoBot
- **Privacy Purists / Self-Hosters:** Moltis

### Architectural Contrasts

- **Gateway Pattern:** OpenClaw, ZeroClaw, PicoClaw, CoPaw all employ heavy gateway daemons for channel management. IronClaw goes further with a full Reborn platform layer.
- **Rust Safety Core:** NullClaw and IronClaw leverage Rust's safety guarantees, appealing to security-conscious users. Others predominantly use Python/TypeScript.
- **Innovation vs Stability:** NanoBot and Moltis push architectural boundaries (Dream system, multi-agent bus, agent-capability boundaries) but have smaller communities. OpenClaw, IronClaw, and CoPaw battle the stability consequences of breadth.

---

## 6. Community Momentum & Maturity Tiers

### Tier 1: Explosive Velocity, Pre-1.0 Churn
*OpenClaw, IronClaw, CoPaw, ZeroClaw*

These projects dominate the activity metrics and are actively redefining their architectural cores while shipping user-facing features. They face the highest regression risk and the most vocal user fatigue. **Characteristic:** Massive PR queues, rapid beta cycles, users pinning specific versions.

### Tier 2: Feature Expansion with Foundation
*Hermes Agent, PicoClaw, NanoBot*

Strong community contributors, clear product visions, and specific technical strengths. These projects handle incidents well (Hermes Codex fix) but have lingering structural gaps (Hermes vision tool, NanoBot regression). **Characteristic:** High-quality community engagement, fast maintainer response, active architecture debates.

### Tier 3: Consolidation & Maintenance
*LobsterAI, Moltis, NanoClaw, NullClaw*

Zero or minimal issue backlogs. Focused on specific integrations (LobsterAI ↔ OpenClaw) or infrastructure hardening (NullClaw error chains, NanoClaw CI). Lower churn but reliable. **Characteristic:** Clean backlogs, professional contributors, immediate turnaround on triaged items.

### Tier 4: Low Activity / Dormant
*ZeptoClaw, TinyClaw*

No human-authored activity. Dependabot-driven commits only (ZeptoClaw) or completely silent (TinyClaw). Risk of bitrot or team focus shifted elsewhere.

---

## 7. Trend Signals (Industry-Level Insights)

Extracted from cross-project community behavior and technical priorities:

### 1. The Subagent Reliability Gap is the New Market Moat
Silent subagent failures are the **single most common critical defect** across active projects (OpenClaw #44925, IronClaw #4084, ZeroClaw, NanoBot #3992). Projects that crack deterministic multi-agent result delivery and observability will capture the "production-grade" market segment. The A2A protocol interest (Hermes #514) and agent bus (NanoBot #3992) signal that this space is ripe for a universal standard.

### 2. Provider Fragmentation is Unsustainable at Current Velocity
All major projects are firefighting API drift (Anthropic deprecations, DeepSeek V4 format change, OpenAI search deprecation). ZeroClaw's DeepSeek issue is **33 days open**—a shocking duration for a P1 blocking a major provider. The ecosystem is crying out for a standardized LLM middleware layer that normalizes streaming, tool calling, and request schemas across providers.

### 3. MCP is the Universal Protocol, Security is the Unfinished Business
MCP injection is being adopted everywhere (Moltis #1049, OpenClaw #85030, ZeroClaw #6946), but security is lagging. MCP tool approval bypasses (Hermes #32877, CoPaw #4709) represent a systemic trust deficit. A deterministic, sandboxed MCP execution framework with forced-approval gates is the clear next infrastructure requirement.

### 4. Desktop is the Dominant UX Frontier
The #1 ecosystem feature request is native desktop apps (OpenClaw #75). TUI improvements are the second most active UX area (Hermes #32980, ZeroClaw #6848). CoPaw's coding mode and ZeroClaw's Beta-2 TUI suggest the "browser tab" interface is failing for complex agent interactions. Power users demand persistent, OS-integrated windows.

### 5. State Durability is the Architectural Battleground
The movement from JSON/file-based state to database-backed persistence (SQLite in OpenClaw #81402, atomic writes in CoPaw #4706, PG in IronClaw) is universal. Session state lost on crash or reconnect is a non-negotiable blocker. Projects that cannot offer crash-recoverable state will be discarded by production users.

### 6. Security Incidents Dictate Trust Trajectories
High-profile MCP bypasses and credential exposure (IronClaw #4082) are creating a political economy of trust. Projects that invest in transparent security models, deterministic approval flows (ZeroClaw DenyWithEdit, CoPaw Approve-All), and external audits will outperform peers on the enterprise curve. Security is no longer a "nice-to-have" — it is the foundation of autonomous agent adoption.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for 2026-05-27.

---

## NanoBot Project Digest — 2026-05-27

### 1. Today's Overview
NanoBot shows strong development velocity on 2026-05-27, with 19 pull requests updated and 4 active issues in the last 24 hours. The project’s open PR queue (13 items) significantly outpaces closed/merged PRs (6 items), indicating a heavy feature pipeline currently under review. While no new releases were cut, foundational work on sandbox security, agent collaboration, and MCP resilience appears to be nearing completion. However, a serious regression in v0.2.0 causing LLM stream timeouts (#4013) has introduced stability friction for users, highlighting the need for rapid mitigation alongside feature expansion.

### 2. Releases
**None.** No new versions were published on 2026-05-27. The latest release remains the previous version tag.

### 3. Project Progress
Six pull requests were merged or closed today, demonstrating ongoing refinement of existing systems:

- **WebUI Polish:** [#3944](https://github.com/HKUDS/nanobot/pull/3944) (boogieLing) was merged, fixing a regression that dropped the active chat session during list refreshes.
- **Provider Resilience:** [#4009](https://github.com/HKUDS/nanobot/pull/4009) (ehs208) fixed blank error handling for Codex transport failures. [#4004](https://github.com/HKUDS/nanobot/pull/4004) (agbocsardi) updated the Kagi search provider to their current v1 API shape.
- **Channel Expansion:** [#3996](https://github.com/HKUDS/nanobot/pull/3996) (outlook84) added opt-in webhook mode for the Telegram channel alongside existing long polling.
- **Docker & Skills:** [#4008](https://github.com/HKUDS/nanobot/pull/4008) (David-Zeng) introduced an `agentmail` skill via a read-only Docker mount.
- **Code Quality:** [#3981](https://github.com/HKUDS/nanobot/pull/3981) (yu-xin-c) enabling ESLint for the WebUI codebase.

### 4. Community Hot Topics
- **Stream Timeout Regression ([#4013](https://github.com/HKUDS/nanobot/issues/4013)):** The most critical community discussion today. The reporter notes that the v0.2.0 upgrade triggered a 90-second stream stall error, making "any real work useless." A strong negative signal given the praise for v0.1.5.
- **Cross-Agent Collaboration ([#3992](https://github.com/HKUDS/nanobot/pull/3992)):** Yiannis Sofologis’s PR for a cross-instance message bus for multi-agent systems is generating significant interest, signaling a strong community desire for distributed agent architectures.
- **GitAgent Protocol Interest ([#4005](https://github.com/HKUDS/nanobot/pull/4005)):** Even though this specific PR is marked `[invalid]`, the proposal to support an open standard for portable agents (agent.yaml) reveals a segment of the community pushing for agent discoverability and ecosystem portability.
- **Tool History Compliance ([#4006](https://github.com/HKUDS/nanobot/issues/4006) / [#4011](https://github.com/HKUDS/nanobot/pull/4011)):** A technically rigorous bug report from sgod39507-a11y regarding orphaned tool results violating strict API specs. The community responded quickly with a targeted fix PR by boogieLing.

### 5. Bugs & Stability
| Severity | Issue | Status & Details |
|---|---|---|
| **Critical** | [#4013](https://github.com/HKUDS/nanobot/issues/4013): LLM stream stalls >90s | **No fix PR yet.** A v0.2.0 regression affecting WebUI users. Highest priority for maintainer triage. |
| **High** | [#4006](https://github.com/HKUDS/nanobot/issues/4006): Orphaned tool results in history | **Fix in progress.** [#4011](https://github.com/HKUDS/nanobot/pull/4011) drops unmatched `role: "tool"` messages from session history and runtime checkpoints. |
| **Medium** | [#4012](https://github.com/HKUDS/nanobot/pull/4012): MCP reconnection failure | **Fix proposed.** The `_mcp_connected` flag is never reset on session drop, making dead sessions invisible to the connection manager. |
| **Resolved** | [#4009](https://github.com/HKUDS/nanobot/pull/4009): Blank Codex errors | Merged today. Structured error handling for the provider retry path. |

### 6. Feature Requests & Roadmap Signals
High-impact features in the active PR pipeline that are likely to land in the next release:

- **Security Sandboxing ([#4007](https://github.com/HKUDS/nanobot/pull/4007)):** Exposes workspace sandbox capability (`off` / `application` / `system`). A major step toward enterprise deployment and secure subagent contexts.
- **Agent Loop Self-Correction ([#4015](https://github.com/HKUDS/nanobot/pull/4015)):** Introduces an "observation-reflection" prompt (Think → Verify → Update User → Act) to make the agent loop self-correcting without manual intervention.
- **Dream System Overhaul ([#3990](https://github.com/HKUDS/nanobot/pull/3990)):** Merges the previous two-phase Dream system into a single AgentLoop-driven session with goal-state lifecycle management, directly addressing the "hunger problem" reported in [#3973](https://github.com/HKUDS/nanobot/issues/3973).
- **Multi-Agent Messaging ([#3992](https://github.com/HKUDS/nanobot/pull/3992)):** A shared message bus allowing multiple agent instances to communicate, unlocking distributed workflows and subagent orchestration.
- **User-Requested:** **[TTS/Voice Output](https://github.com/HKUDS/nanobot/issues/4010)** (olgagaga) and a **[Skill Discovery Command](https://github.com/HKUDS/nanobot/pull/3968)** (`/skill`) remain open in the queue.

### 7. User Feedback Summary
- **Regression Frustration:** A user (mxnbf) explicitly describes a broken trust scenario with the v0.2.0 upgrade: *“ive been using 0.1.5post2 … its been very good … a few days ago i updated to 0.2.0 and now i receive this error.”* The stall error is framed as blocking productivity entirely.
- **Feature Parity Expectation:** The TTS request (olgagaga) reflects a mature user base expecting full conversational duplex: *“nanobot already understands voice in. It cannot yet speak out … Adding voice output closes the conversational loop.”*
- **Advanced Developer Demand:** Users like sgod39507-a11y are running NanoBot against strict API contracts (OpenAI/Anthropic) and demanding exact spec compliance regarding tool call pairing. This signals that NanoBot is being used in integration-heavy production workflows.
- **Self-Improvement Ambition:** The Dream system feedback (chxuan) shows a power-user segment that views the current `history.jsonl` dependency as a bottleneck for true autonomous improvement.

### 8. Backlog Watch
Several high-value, long-standing items still require maintainer decisions:

- **[PR #1443](https://github.com/HKUDS/nanobot/pull/1443) (Heartbeat Reasoning):** Open since March 2. Proposes silent heartbeat agent reasoning by default. Was updated today by the author (phelps-sg) but lacks maintainer engagement.
- **[PR #2515](https://github.com/HKUDS/nanobot/pull/2515) (Integrated Memory Framework):** Open since March 26. A massive refactor supporting Mem0, Graphiti, and Memobase backends. As a foundational architectural change, its prolonged open status may be blocking downstream memory features and community contributions in this area.
- **[Issue #3973](https://github.com/HKUDS/nanobot/issues/3973) (Dream System "Hunger Problem"):** Created May 23 with no maintainer comment. While PR [#3990](https://github.com/HKUDS/nanobot/pull/3990) may resolve this, the lack of acknowledgment on the issue itself is a missed opportunity to engage a clearly advanced user.
- **[PR #3869](https://github.com/HKUDS/nanobot/pull/3869) (DeepSeek Hardening):** Open since May 16. Addresses critical null-content 400 errors and placeholder text leakage specific to DeepSeek providers. Unresolved pending review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the structured project digest for **Hermes Agent** based on the GitHub activity snapshot for **2026-05-27**.

---

# Hermes Agent Project Digest: 2026-05-27

## 1. Today's Overview

June 27 saw an exceptional spike in activity driven by a widespread, critical crash in the widely-used **`openai-codex` / ChatGPT Codex provider**. Over **20 duplicate bug reports** flooded in alongside a flurry of emergency fix pull requests, making this the dominant narrative of the day. The core team and community reacted quickly, with a mainline fix merged within hours. Beyond the Codex outage, the project tackled a **P1 security bypass** in the MCP tool wrapper and a silent failure in the cron scheduler. Overall, **50 issues** and **50 pull requests** were updated, marking one of the highest-velocity days for the project in recent memory. A patch release is highly imminent.

## 2. Releases

No new versions were published today. Based on the volume of merged fixes, a patch release (likely v0.14.1 or v0.15.0) is expected shortly to ship the critical provider recovery logic.

## 3. Project Progress

Of the 50 updated PRs, **15** were merged or closed today. The major milestones include:

- **🔴 Emergency Codex Fix Landed ([PR #32963](https://github.com/NousResearch/hermes-agent/pull/32963)):** Merged by maintainer **teknium1**. This fix recovers OpenAI SDK streams when the ChatGPT backend sends a terminal `response.completed` with a `null` output. Closes the master bug ([Issue #11179](https://github.com/NousResearch/hermes-agent/issues/11179)) and supersedes over a dozen duplicate crash reports.
- **Docker Build Hygiene ([PR #29025](https://github.com/NousResearch/hermes-agent/pull/29025)):** Merged to exclude local runtime secrets and cache from Docker build contexts and `.gitignore`.

Several other Codex-related fix PRs ([#32972](https://github.com/NousResearch/hermes-agent/pull/32972), [#32979](https://github.com/NousResearch/hermes-agent/pull/32979)) were acknowledged as duplicates and closed in favor of the main salvage.

## 4. Community Hot Topics

The community's focus is sharply split between a major outage and long-term architectural desires:

- **Codex Provider Collapse ([Issue #32892](https://github.com/NousResearch/hermes-agent/issues/32892), 38 👍 / 32 Comments):** The most active discussion today. User **stawiski** reported the `'NoneType' object is not iterable` crash against the ChatGPT backend. A heavy consensus emerged around the `null output` root cause.
- **Top Engagement Fix Proposal ([Issue #32883](https://github.com/NousResearch/hermes-agent/issues/32883), 48 👍):** Billythek’s specific fix proposal received the highest reaction count of the day, signaling strong community alignment on the required solution.
- **Agent-to-Agent Protocol ([Issue #514](https://github.com/NousResearch/hermes-agent/issues/514), 9 👍 / 16 Comments):** The A2A feature request continues to draw steady interest and speculation, indicating that multi-agent interoperability remains the top "aspirational" feature for the user base.
- **Claude CLI Compatibility ([Issue #29125](https://github.com/NousResearch/hermes-agent/issues/29125), 26 Comments):** A persistent pain point for users tying their Anthropic subscriptions to Hermes.

## 5. Bugs & Stability

Today’s reports reveal a mix of critical user-facing crashes and serious architectural weaknesses.

**Critical (P1)**
- **`openai-codex` Null Output Crash (Multiple Reports):** The highest-severity operational issue today. Users relying on `gpt-5.5` via the ChatGPT backend were completely blocked.
    - *Fix Status:* **Merged** ([PR #32963](https://github.com/NousResearch/hermes-agent/pull/32963)).
- **MCP Tool Approval Bypass ([Issue #32877](https://github.com/NousResearch/hermes-agent/issues/32877)):** The `approval.py` gate only protects the `terminal_tool`. MCP wrappers (`ssh`, `docker`) bypass it entirely, allowing dangerous commands to execute without user consent.
    - *Fix Status:* **Open / Unaddressed**.
- **Cron Ticker Silent Death ([Issue #32895](https://github.com/NousResearch/hermes-agent/issues/32895)):** The cron background thread can stop without logs, causing scheduled jobs to silently fail.
    - *Fix Status:* **Open / Unaddressed**.

**High (P2)**
- **Memory Silent Failure ([Issue #32965](https://github.com/NousResearch/hermes-agent/issues/32965)):** Raw markdown `MEMORY.md` files are silently ignored instead of parsed.
    - *Fix Status:* **Fix PR Submitted** ([PR #32978](https://github.com/NousResearch/hermes-agent/pull/32978)).
- **Systemd Restart Loops ([Issue #32951](https://github.com/NousResearch/hermes-agent/issues/32951)):** `Restart=always` causes conflicts with the `--replace` takeover flag.
    - *Fix Status:* **Fix PR Submitted** ([PR #32989](https://github.com/NousResearch/hermes-agent/pull/32989)).
- **Vision Tool Completely Inoperable ([Issue #9077](https://github.com/NousResearch/hermes-agent/issues/9077)):** Now open for over a month. The `vision_analyze` tool fails to process local files, URLs, or screenshots.
    - *Fix Status:* **Open / Unaddressed**.
- **TUI Remote Gateway Attach ([Issue #32882](https://github.com/NousResearch/hermes-agent/issues/32882)):** Fails with a 404 due to a missing WebSocket endpoint.

## 6. Feature Requests & Roadmap Signals

Several significant contributions signal the direction of the project:

- **TUI Session Orchestrator ([PR #32980](https://github.com/NousResearch/hermes-agent/pull/32980)):** Salvaged by **teknium1**, this adds a session switcher overlay to the TUI, enabling power users to manage multiple concurrent agent sessions from a single terminal interface.
- **ByteDance & Xiaomi Providers ([PR #32990](https://github.com/NousResearch/hermes-agent/pull/32990)):** A community submission adds first-class support for these regional model providers, indicating strong demand for diverse, low-cost international backends.
- **20-Language Backend (i18n) ([PR #32994](https://github.com/NousResearch/hermes-agent/pull/32994)):** A massive contribution adding locale files for Arabic, Hindi, Polish, and more. This is a strong signal for a globalized v0.15 release.
- **A2A Protocol ([Issue #514](https://github.com/NousResearch/hermes-agent/issues/514)):** Sustained community interest suggests this will be a tentpole feature for the next major version, aligning with industry trends in inter-agent communication.

## 7. User Feedback Summary

- **Primary Pain Point (Codex Crash):** Users relying on the `openai-codex` provider with `gpt-5.5` faced a complete blockage today. The frustration is evident from the volume of duplicates, but confidence is high due to the rapid maintainer intervention.
- **Architectural Distrust (MCP Gate):** The discovery that MCP tools bypass the approval system ([Issue #32877](https://github.com/NousResearch/hermes-agent/issues/32877)) is a major trust concern for users running Hermes in sensitive environments. This is likely a blocking issue for many enterprise adopters.
- **Reliability Concerns:** The silent failures in Memory and Cron shake user confidence. Users expect deterministic background behavior from an agent framework.
- **Positive Sentiment:** The community is highly engaged and collaborative. The speed of fix submissions and the quality of collaboration on the Codex root cause analysis reflects a healthy developer ecosystem.

## 8. Backlog Watch

Several long-standing items remain open and could use maintainer attention:

- **vision_analyze Broken ([Issue #9077](https://github.com/NousResearch/hermes-agent/issues/9077), P2):** Open since April 13. As a core differentiator for an AI agent, an entirely broken vision tool represents a significant gap in the product promise.
- **Skills Auto-Trigger Failure ([Issue #4589](https://github.com/NousResearch/hermes-agent/issues/4589), P3):** Open since April 2. The agent fails to automatically load relevant skills, forcing users into manual invocation. This undermines the core "autonomous agent" value proposition.
- **Codex Empty Output Origin ([Issue #5879](https://github.com/NousResearch/hermes-agent/issues/5879), P2):** Open since April 7. The root cause of today's crash event has been partially documented for weeks. A deeper refactor of the Codex stream normalization may still be warranted.
- **Stalled PR: Telegram Config ([PR #13420](https://github.com/NousResearch/hermes-agent/pull/13420)):** Submitted since April 21 with no maintainer interaction. A small but popular quality-of-life fix for Telegram reaction behavior.
- **Desktop App Session Loss ([Issue #31977](https://github.com/NousResearch/hermes-agent/issues/31977), P2):** A recent regression in the official desktop app concerning session continuation and API key persistence, unresolved since May 25.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the structured project digest for PicoClaw based on the GitHub data for **2026-05-27**.

---

## PicoClaw Project Digest: 2026-05-27

### 1. Today’s Overview

PicoClaw is in an exceptionally high-velocity development cycle, driven heavily by community contributors. A new **nightly build (v0.2.9-nightly)** was published, but the standout signal is the sheer volume of code flow: **13 pull requests were merged or closed** in the last 24 hours, focusing on stability, platform compatibility, and channel enhancements. While only a handful of new issues were opened, the existing backlog saw significant updates, indicating a project that is actively responding to user feedback rather than stagnating. Overall project health is excellent, characterized by rapid iteration on both agent internals and user-facing features.

### 2. Releases

- **Nightly Build v0.2.9-nightly.20260527.28ec5793**: An automated nightly build was published. This version is explicitly marked as potentially unstable and sums up the activity between the last stable tag (`v0.2.9`) and the current `main` branch.
    - **Changelog**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
    - **Note**: No stable release was cut, but the rapid merging of features suggests a stable release (v0.3.0 or v0.2.10) is likely imminent. Users migrating from `v0.2.9` should pay attention to the breaking `exec` tool path fixes and new configuration keys for agent spawn/steering behavior.

### 3. Project Progress (Merged/Closed PRs)

The last 24 hours saw major re-architecture and feature delivery:

- **Agent System Overhaul**: Contributor `bogdanovich` landed three critical PRs:
    - **#2830**: Introduced an explicit async delivery policy for `spawn` tool results, closing #2829. This prevents agents from hallucinating synthetic responses from subagent results.
    - **#2844**: Added an experimental `final_turn_render_mode` to handle "steering-heavy" conversations, allowing an extra LLM pass for cohesive final replies.
    - **#2840**: Fixed a major channel UX bug where steering final replies were sent as edits instead of new messages.
- **Channel Flexibility**:
    - **#2883** (merged): Added support for WeChat multi-account configuration.
    - **#2849** (merged): Added `guest_mode` support for Telegram.
    - **#2845** (merged): Added Telegram Business mode support.
- **Core Fixes**:
    - **#2826** & **#2750** (merged): Resolved critical path resolution bugs in the `exec` tool where relative paths were incorrectly treated as root-absolute.
    - **#2647** (merged): Enabled YAML configuration for the `web_search` tool and set DuckDuckGo as the default provider.
    - **#2946** (merged): Fixed timestamp persistence (`created_at`) in the SeaHorse history pipeline.
- **DevEx & Docs**:
    - **#2851** (merged): Added a community link for a Yocto/OpenEmbedded layer (`meta-picoclaw`) for embedded Linux builds.
    - **#2933** (merged): Added line numbers and a global wrap toggle to web UI code blocks.

### 4. Community Hot Topics

The most active discussions highlight a demand for advanced backend control and platform stability:

- **#2674: [BUG] Codex OAuth: empty assistant response** ([Link](https://github.com/sipeed/picoclaw/issues/2674))
    - *Context*: The highest-reacted open issue (👍: 4, Comments: 6). Users are hitting a hard wall using the ChatGPT backend via Codex OAuth. The streaming protocol seems misaligned (`response.output_item.done`).
    - *Analysis*: This remains the most significant unresolved regression for high-power users. Fixes in #2840 may tangentially help, but the core streaming mapping is still unpatched.
- **#2404: [Feature] Add streaming HTTP request config** ([Link](https://github.com/sipeed/picoclaw/issues/2404))
    - *Context*: The longest-running active discussion (Comments: 8). Users want a simple `"streaming": true` config flag to control how the backend receives responses.
    - *Analysis*: This is a highly desired UX improvement that would give users deep control over latency and output parsing.
- **#2952: [Feature] Feature request bundle** ([Link](https://github.com/sipeed/picoclaw/issues/2952))
    - *Context*: A user (xhynice) explicitly asks "好久没发新版本了" (It's been a while since a new version), and bundles three specific complaints: the `exec` tool firing without explicit actions, a QQ channel restart loop, and a request for a better model/provider dropdown UI.
    - *Analysis*: This single issue signals that the user base is ready for a formal release and is feeling the friction of edge cases in the current nightly cycle.

### 5. Bugs & Stability

The project is actively fighting API fragmentation and platform regressions. Severity rankings are based on user impact:

- **Critical (Fix PR Merged)**:
    - *Exec Tool Path Injection*: The path scanner bug (#2749) which could allow unintended file access was patched via #2826 and #2750.
- **Critical (Fix PR Open)**:
    - *Anthropic API Breaking Change*: PRs #2947 and #2948 (by yuxuan-7814) are open to fix HTTP 400/404 errors for `claude-opus-4-7` (deprecated `temperature`) and `claude-sonnet-4-6` (wrong model ID format).
    - *OpenAI Web Search Regression*: PR #2951 fixes `HTTP 400` errors for users hitting OpenAI endpoints that don't support `web_search_preview`.
    - *Termux SSL*: PR #2949 fixes a full blocker for Android/Termux users where HTTPS requests fail due to an undetected CA bundle path.
- **High (Unresolved)**:
    - **#2674**: Codex OAuth empty response.
    - **#2887**: The `.deb` package is broken on RISC-V Linux with OpenAI models.
- **Medium (Unresolved)**:
    - **#2943**: Weixin image sending triggers a `1210` parameter error on Zhipu GLM-5.
    - **#2952**: QQ channel restart loop and `exec` tool firing incorrectly on first call.

### 6. Feature Requests & Roadmap Signals

- **Likely for Next Stable Release**:
    - *Agent Routing*: The merged `spawn` delivery policy (#2830) and `final_turn_render_mode` (#2844) are complex new capabilities that will almost certainly define the next major feature update.
    - *Channel Expansion*: Telegram Guest/Business modes and WeChat multi-account support are mature features ready for a stable tag.
- **Hot on the Agenda**:
    - *Streaming Config* (#2404): The community strongly agrees on this, and it is a relatively simple config change. Expect a PR soon.
    - *Provider UI Overhaul*: #2952 explicitly asks for dropdown provider selection, key reuse, and API test connections. This is a strong roadmap signal that the configuration UI is falling behind the codebase's capability.
- **Project Sustainability**: PR #2950 (FUNDING.yml) has been opened, signaling a move towards accepting financial support via GitHub Sponsors.

### 7. User Feedback Summary

- **Satisfaction**: The community is deeply engaged. The velocity of merges from community contributors (`bogdanovich`, `yuxuan-7814`, `stolyarchuk`, `lc6464`) shows that contributors feel their code is welcome and valuable.
- **Friction Points**:
    - **API Fragmentation**: Users are suffering from the rapid pace of API changes from providers (Anthropic blocking `temperature`, OpenAI deprecating `web_search_preview`). The project is reacting quickly, but users on old nightlies are hitting errors.
    - **Platform Gaps**: RISC-V and Termux support is patchy. While documentation improves (Yocto layer), execution stumbles.
    - **Agent Complexity**: Users leveraging advanced features (spawn, steering) are hitting edge cases. The recent flurry of fixes directly addresses this, but the learning curve is steep.

### 8. Backlog Watch

These items are high-impact but have been waiting for maintainer triage or see no active PRs:

- **Issue #2674 (Codex OAuth empty response)**: [Link](https://github.com/sipeed/picoclaw/issues/2674)
    - *Status*: Open since April 26. The highest-voted bug with deep community debugging. Needs a maintainer to confirm the suspected streaming mismatch or assign it to a contributor.
- **PR #2551 (refactor: channel identification)**: [Link](https://github.com/sipeed/picoclaw/pull/2551)
    - *Status*: Open since April 16. This is a massive architectural refactor decoupling channel names from provider types. It is currently "stale" and likely needs a heavy rebase considering the WeChat multi-account (#2883) and Feishu name (#2846) PRs just merged. The risk of bitrot here is very high.
- **PR #2239 (Docker compose privileged)**: [Link](https://github.com/sipeed/picoclaw/pull/2239)
    - *Status*: Open since April 1. A small, isolated change that has received zero maintainer feedback. Quick to triage and merge or close.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the data-driven project digest for **NanoClaw** on **2026-05-27**, based strictly on the provided GitHub activity.

---

## 1. Today’s Overview
Activity on **NanoClaw** today is heavily focused on infrastructure hardening and operational stability. No new issues or releases were opened, but four pull requests were updated, with one critical fix already merged. The project’s open issue count sits at **zero**, suggesting a tightly maintained backlog. Developer attention is currently split between preventing a pending CI deprecation in June 2026 and fixing real-world container lifecycle bugs reported by users in production environments. While community comments are minimal, the quality of the contributions (self-healing logic, proactive CI bumps) signals a healthy, maintainer-responsive project.

## 2. Releases
*No new releases were published today.* The latest release remains unchanged.

## 3. Project Progress

**Merged / Closed:**
- **[PR #2622: web: restart container after marketplace skill/persona update](https://github.com/nanocoai/nanoclaw/pull/2622)** (Merged) by *sumsumai*
  - **Impact:** High. This closed a functional gap where provisioning a new template skill or persona from the marketplace updated the database but did not apply the configuration to the currently running container (`composeGroupClaudeMd` only reads at spawn time). The container will now restart or refresh immediately after a marketplace config update.

**Newly Opened / In Progress:**
- **[PR #2608: ci: bump Node 20 actions to v5 ahead of June 2026 deprecation](https://github.com/nanocoai/nanoclaw/pull/2608)** by *IamAdamJowett*
  - Bumps `actions/checkout`, `actions/setup-node`, and `pnpm/action-setup` to their `@v5` major versions.
- **[PR #2620: fix(container-runner): self-heal missing image before spawn](https://github.com/nanocoai/nanoclaw/pull/2620)** by *matmartinez*
  - Adds a `docker image inspect` check; if the image is missing, the host rebuilds it before issuing `docker run`.
- **[PR #2621: chore: add .gitattributes to enforce LF line endings for shell scripts](https://github.com/nanocoai/nanoclaw/pull/2621)** by *GarethWright*
  - Prevents shell script execution failures on Windows by standardizing `*.sh` files to LF line endings.

## 4. Community Hot Topics
While no issues or PRs have extensive comment threads, the underlying pain points driving the open PRs are clear.

- **PR #2620: Self-healing container images** — This addresses a specific operational pain for users running NanoClaw on **[Dokploy](https://dokploy.com/)**. Dokploy ships with a "Daily Cleanup" cron that frequently prunes Docker images, causing the container runner to enter a hard crash-loop. The contribution of a self-healing rebuild step indicates a vocal user segment pushing for production-grade resilience.
- **PR #2608: CI deprecation prep** — The urgency of this PR (ahead of the June 2026 deadline) reflects the community’s reliance on a green CI pipeline. The lack of comments likely means the change is straightforward and widely agreed upon.

## 5. Bugs & Stability

| Severity | Bug | Status |
|---|---|---|
| **High** (Fixed) | **Marketplace skill/persona config not applied to running containers.** The DB update was successful, but warm containers ignored the new templates until a manual restart. | **Resolved** by [PR #2622](https://github.com/nanocoai/nanoclaw/pull/2622). |
| **Medium** (Fix Open) | **Container crash-loop due to missing Docker image.** External tools (Dokploy) purge images, causing `docker run` to fail. | **Fix Proposed** in [PR #2620](https://github.com/nanocoai/nanoclaw/pull/2620). Awaiting merge. |
| **Low** (Fix Open) | **Unix shell scripts fail on Windows hosts.** CRLF line endings cause execution errors for developers contributing across platforms. | **Fix Proposed** in [PR #2621](https://github.com/nanocoai/nanoclaw/pull/2621). Awaiting merge. |

## 6. Feature Requests & Roadmap Signals
No formal feature requests were filed today. However, the current PRs signal strong direction for the upcoming minor release:

- **Operational Resilience:** The self-healing container runner ([PR #2620](https://github.com/nanocoai/nanoclaw/pull/2620)) suggests NanoClaw is pivoting toward surviving hostile cloud environments (Docker image pruning, disk pressure).
- **CI Modernization:** The bump to `@v5` Actions ([PR #2608](https://github.com/nanocoai/nanoclaw/pull/2608)) is a prerequisite for continued automated testing beyond June 2026.

**Prediction for the next minor version:**
The next release will likely bundle the CI bump ([#2608](https://github.com/nanocoai/nanoclaw/pull/2608)) and the self-healing fix ([#2620](https://github.com/nanocoai/nanoclaw/pull/2620)). The marketplace container restart fix ([#2622](https://github.com/nanocoai/nanoclaw/pull/2622)) is a strong candidate for a **patch release** (e.g., `vX.Y.1`) given its direct impact on the web UI workflow.

## 7. User Feedback Summary
- **Pain Points:**
  - Users on Dokploy experience daily service interruptions due to image pruning. The community directly submitted a fix to prevent crash-looping.
  - Users updating marketplace agents encountered a confusing lack of immediate feedback—the config was saved but not applied until a manual restart. This was resolved within 24 hours ([PR #2622](https://github.com/nanocoai/nanoclaw/pull/2622)).
- **Satisfaction:**
  - The maintainer team demonstrated fast turnaround time, merging a critical web UI fix on the same day it was authored.
  - Active community contributions ([#2620](https://github.com/nanocoai/nanoclaw/pull/2620), [#2621](https://github.com/nanocoai/nanoclaw/pull/2621)) indicate that users are invested in the project’s success and feel empowered to fix their own blockers.

## 8. Backlog Watch
- **Open Issues:** **0** — The project has an excellent track record of no unresolved user bug reports or feature requests. Backlog is effectively clear.
- **Critical Open Items:**
  - **[PR #2620](https://github.com/nanocoai/nanoclaw/pull/2620)** (Container self-heal): This blocks users running on Dokploy. It should be merged promptly to prevent further production incidents.
  - **[PR #2608](https://github.com/nanocoai/nanoclaw/pull/2608)** (CI bump): Needs review before the June 2026 Node 20 deprecation to avoid broken CI pipelines. No risk of becoming stale, but it has a hard deadline.
- **Low Risk / Ready-to-Merge:**
  - **[PR #2621](https://github.com/nanocoai/nanoclaw/pull/2621)** (`.gitattributes`): Simple DX improvement, no side effects. Ready for a maintainer approval.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for May 27, 2026, generated from the provided GitHub activity data.

---

### 1. Today’s Overview
Today was a quiet but productive maintenance day for the NullClaw project. No new issues were filed, and no releases were made, indicating a period of relative stability for end users. The core team made progress on the infrastructure front, successfully merging a key pull request focused on provider error handling. A critical fix for Nix-based builds is also under review. Overall project health appears stable, with the current sprint dedicated to hardening and platform compatibility rather than new features.

### 2. Releases
**None.** No new versions of NullClaw were published today.

---

### 3. Project Progress
One pull request was merged today, advancing the project's observability and reliability:

- **PR #891 [Closed/Merged]**: `fix(providers): preserve curl probe transport failures`
  - **Author**: vernonstinebaker
  - **Summary**: This fix improves health check diagnostics for OpenAI-compatible providers. Instead of collapsing transport errors into generic failures, specific errors (e.g., `CurlDnsError`, `CurlTimeout`, `CurlTlsError`) are now preserved and surfaced directly to users.
  - **Link**: [PR #891](https://github.com/nullclaw/nullclaw/pull/891)

- **PR #935 [Open]**: `fix(nix): updated lockfiles to work with zig 0.16.0`
  - **Author**: Codom
  - **Summary**: A submitted fix to resolve broken Nix builds caused by the flake.lock file pointing to an outdated version of `zig2nix`.
  - **Link**: [PR #935](https://github.com/nullclaw/nullclaw/pull/935)

---

### 4. Community Hot Topics
Community engagement was dormant in the last 24 hours, with zero comments or reactions registered across all issues and pull requests. The technical discussion in the project currently revolves around two specific infrastructure topics:

- **Provider Transport Errors ([PR #891](https://github.com/nullclaw/nullclaw/pull/891))**: The underlying community need was for better debugging tools when provider connections fail. The merge of this PR addresses that pain point.
- **Zig/Nix Build Compatibility ([PR #935](https://github.com/nullclaw/nullclaw/pull/935))**: This represents a blocking issue for users on the Nix platform who have updated their toolchains to Zig 0.16.0.

---

### 5. Bugs & Stability
No new bugs were filed in the last 24 hours. The project’s active stability concerns are centered on two items:

- **Medium Severity – Resolved**: Provider transport errors were previously masked behind generic failure messages, hampering debugging. This has been fixed via **PR #891** (merged).
- **High Severity – Pending Fix**: Nix builds are currently broken for users utilizing Zig 0.16.0. **PR #935** is open and awaiting review to resolve this regression.

---

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed or heavily discussed today. The activity signal is firmly pointed toward **hardening and developer experience**. By focusing on preserving transport error details (PR #891) and supporting the latest Zig compiler in the Nix ecosystem (PR #935), the project is prioritizing build reliability and runtime observability.

**Prediction**: The next release will likely be a maintenance-focused minor version bump. It will focus on ensuring compatibility with Zig 0.16.0 (via Nix) and delivering more granular error reporting for provider connections, setting a stable foundation for future feature work.

---

### 7. User Feedback Summary
While no direct user commentary was posted in the issues or PRs today, the content of the active pull requests reveals specific pain points:

- **Pain Point**: Inability to debug provider connection issues due to generic error messages (addressed by PR #891).
- **Pain Point**: Build environment failures for users relying on the Nix package manager with standard Zig toolchains (addressed by PR #935).

The lack of new bug reports suggests general satisfaction with the runtime stability of the current release.

---

### 8. Backlog Watch
There are zero open issues in the backlog. The primary item requiring maintainer attention is:

- **PR #935**: `fix(nix): updated lockfiles to work with zig 0.16.0`
  - While opened only yesterday (May 26), this is the single most pressing item for the contributor community.
  - **Impact**: High. Directly blocks all Nix-based builds for users on modern Zig toolchains.
  - **Action Required**: Maintainer review, testing, and merge.
  - **Link**: [PR #935](https://github.com/nullclaw/nullclaw/pull/935)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

## IronClaw Project Digest — 2026-05-27

### 1. Today's Overview
Project activity remains extremely high, with **50 pull requests updated** (16 merged/closed) and **16 active issues** in the last 24 hours. The project shipped **v0.29.0** yesterday, continuing its rapid release cadence. Developer focus is overwhelmingly concentrated on the **Reborn platform migration**, with major feature stacks converging around attested signing/chain signing, a new hooks framework, and Reborn extension lifecycles. Security hardening is a clear theme today, spanning credential handling, cross-tenant isolation, and background subagent result delivery. A persistent distribution blocker on crates.io remains the primary friction point for downstream adoption.

---

### 2. Releases
A single new release was logged today:

**`ironclaw-v0.29.0`** (2026-05-26)
- *Channels:* Added a **WeCom** (WeChat Work) channel integration ([#2394](https://github.com/nearai/ironclaw/pull/2394))
- *Web:* The Responses API now supports **externally-provided tools** ([#3122](https://github.com/nearai/ironclaw/pull/3122))
- *Gateway:* A **logs download button** was added to the gateway interface ([#3588](https://github.com/nearai/ironclaw/pull/3588))
No breaking changes or migration notes were listed in the release notes.

---

### 3. Project Progress (Merged/Closed)
Sixteen pull requests and two issues moved to a closed state today.

**Reborn Lifecycle & CLI Milestones**
- **Extension Lifecycle CLI** ([#4099](https://github.com/nearai/ironclaw/pull/4099)) was merged, enabling local-dev extension management for install/activate/remove workflows.
- The **Reborn CLI skills list** was wired ([#4095](https://github.com/nearai/ironclaw/pull/4095)), replacing the stubbed output with a live skill catalog.

**Integration & Product Features**
- **Static WebUI v2** was ported to the Reborn WebChat ingress ([#3886](https://github.com/nearai/ironclaw/issues/3886)).
- **Approval interaction service** and product resolution routing were closed out ([#3889](https://github.com/nearai/ironclaw/issues/3889)).
- **Builtin HTTP `save_to`** was enabled for Reborn ([#4103](https://github.com/nearai/ironclaw/pull/4103)), allowing agents to write HTTP bodies to a filesystem-backed body store.

---

### 4. Community Hot Topics
| Issue | Comments | Theme |
|-------|----------|-------|
| [#3259 – Publish 0.25.0–0.27.0 to crates.io](https://github.com/nearai/ironclaw/issues/3259) | 10 | **Distribution blocker** — downstream pinned to 0.24.0 while wasmtime CVEs go unfixed |
| [#3857 – Slack ProductAdapter MVP](https://github.com/nearai/ironclaw/issues/3857) | 4 | **Platform integration** — strong demand for enterprise messaging |
| [#3281 – EventStreamManager](https://github.com/nearai/ironclaw/issues/3281) | 2 | **Core infrastructure** — durable projection fanout for Web SSE/WebSocket |
| [#4102 – Grant expiry enforcement](https://github.com/nearai/ironclaw/issues/4102) | 1 | **Architectural debate** — trait-level contract equivalence vs durability fix |
| [#4085 – Missing TenantSandboxProcessPort](https://github.com/nearai/ironclaw/issues/4085) | 1 | **CI signal erosion** — perma-failing composition tests |

The dominant community concern remains the **crates.io publishing gap** ([#3259](https://github.com/nearai/ironclaw/issues/3259)), which blocks access to both features and security fixes. The Slack integration ([#3857](https://github.com/nearai/ironclaw/issues/3857)) continues to draw interest, indicating a clear enterprise go-to-market vector.

---

### 5. Bugs & Stability

**Critical**
- **Background subagent results never delivered** ([#4084](https://github.com/nearai/ironclaw/issues/4084)): Spawned background agents complete silently with no notification to the parent turn. A follow-up for mid-turn polling was filed ([#4092](https://github.com/nearai/ironclaw/issues/4092)). This is a core logic defect for parallel tasking.
- **Production composition builders missing TenantSandboxProcessPort** ([#4085](https://github.com/nearai/ironclaw/issues/4085)): Causes permanent failure in composition tests, masking legitimate CI regressions.
- **Cross-tenant leakage, replay, provider spoofing** ([#3931](https://github.com/nearai/ironclaw/pull/3931)): A fix PR is open for three critical security bugs in the hook framework.

**High**
- **Setup wizard env precedence** ([#4106](https://github.com/nearai/ironclaw/issues/4106)): `SANDBOX_IMAGE` environment variable is bypassed by the setup wizard, which always probes a hardcoded default.
- **Secrets exposure** ([#4082](https://github.com/nearai/ironclaw/issues/4082)): `SecretString` is unwrapped into plain `String` in the credential path, making secrets visible in memory.

**Medium**
- **Signer approval gate is Optional** ([#4081](https://github.com/nearai/ironclaw/issues/4081)): `gate_signing_if_required` short-circuits to `Ok(())` when no gate is installed, potentially creating a security gap in non-production configurations.

---

### 6. Feature Requests & Roadmap Signals
The following high-velocity feature stacks are predictive of v0.30.0+ priorities:

- **Attested Signing Substrate (10+ PRs)** – Final layers are landing, including multi-chain broadcasters (#3996), durable PG/libSQL stores (#3996), the `request_signature` tool (#4015), and the TrustEnrollment ceremony (#4055). This is the single largest feature sprint currently underway.
- **Hooks Framework Activation** – The hooks subsystem is approaching production activation behind the `HOOKS_ENABLED` flag (#3938), supported by a `PostgresPredicateStateBackend` (#3933) and an adversarial cross-backend parity suite (#3937).
- **Subagent Flavors** (#4086) – A dedicated coder/explorer/planner subagent system is being designed, suggesting a deeper platform abstraction for agent specialization.
- **Extension Ecosystem** – GSuite first-party extensions were committed (#4100), and the lifecycle CLI (#4099) points toward a full extension marketplace pattern.

---

### 7. User Feedback Summary
**Satisfaction Drivers**
- The rate of feature delivery (1 release per day on average) signals an active, well-resourced maintainer team.
- Heavy investment in testing infrastructure (#3937) and security review processes (attested signing reviews, #4060) builds trust with production users.

**Pain Points**
- **Distribution lag** remains the loudest signal (#3259). Users are locked out of multiple patch/minor releases and associated security fixes.
- **Functional regression in background agents** (#4084) degrades the experience for users running parallel subagent workflows.
- **Setup friction** (#4106) will frustrate first-time sandbox users trying to customize runtimes via environment variables.
- **Security hygiene issues** (#4082, #4081) suggest that internal audits are surfacing real gaps the core team is prioritizing.

---

### 8. Backlog Watch
These items remain open and require maintainer attention to unblock downstream consumers or key architectural paths:

| Issue | Age (Days) | Impact |
|-------|------------|--------|
| [#3259 – Publish to crates.io](https://github.com/nearai/ironclaw/issues/3259) | 22 | **All downstream Rust users** — pinned to 0.24.0 |
| [#3281 – EventStreamManager](https://github.com/nearai/ironclaw/issues/3281) | 21 | **Streaming & WebSocket support** — blocks durable projection fanout |
| [#3809 – EventStreamManager timeline/replay](https://github.com/nearai/ironclaw/issues/3809) | 8 | **WebUI progress & tool activity display** |
| [#4088 – Oversized file decomposition](https://github.com/nearai/ironclaw/issues/4088) | 1 | **Technical debt** — files flagged during review need structural cleanup to sustain contribution velocity |

The crates.io issue (#3259) is the most urgent single action item; nearly a month in the backlog with no resolution visible, it remains the clear project health headwind for the Rust community.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for 2026-05-27 based on the provided GitHub data.

---

# 🦞 LobsterAI Project Digest — 2026-05-27

## 1. Today’s Overview

The project maintained a very high level of activity, with **12 pull requests** processed and **9 merged** in the last 24 hours. Development effort was heavily concentrated on stabilizing the **OpenClaw skill synchronization system** and fixing blocking bugs in the **cowork / tool loop** engine. No new issues were filed, suggesting a low user friction burden despite the rapid merge cadence, though a lack of detailed community comment data limits the depth of sentiment analysis. Two long-open PRs remain tagged as `stale`, indicating a potential bottleneck in maintainer bandwidth.

## 2. Releases

**No new releases** were published today. The current latest release remains unchanged.

## 3. Project Progress — Merged & Closed PRs

The main branch absorbed significant improvements today across three primary areas:

**🔌 OpenClaw Ecosystem & Skill Manager**
- **[#2045](https://github.com/netease-youdao/LobsterAI/pull/2045)** *(Merged)*: Implemented skill syncing from OpenClaw on first visit to the skills tab, along with a manual "Sync from OpenClaw" entry point.
- **[#2055](https://github.com/netease-youdao/LobsterAI/pull/2055)** *(Merged)*: Disabled automatic OpenClaw skill sync behind a feature flag (default off) to prevent unintended overwrites. Also lifted the undeletable restriction for marketplace-installed skills.
- **[#2054](https://github.com/netease-youdao/LobsterAI/pull/2054)** *(Merged)*: Expanded the internal plugin exclusion list to hide all OpenClaw provider plugins and alias plugins from sync detection.

**🛠️ Cowork / Tool Execution Stability**
- **[#2051](https://github.com/netease-youdao/LobsterAI/pull/2051)** *(Merged)*: Re-fixed the tool loop breaker logic.
- **[#2058](https://github.com/netease-youdao/LobsterAI/pull/2058)** *(Merged)*: Tightened the grace period handling for short final messages in cowork, improving synchronization after large tool results.

**🖥️ UX & Infrastructure**
- **[#2059](https://github.com/netease-youdao/LobsterAI/pull/2059)** *(Merged)*: Fixed a blocking OAuth protocol handler issue on Windows in dev mode (callback URL was being treated as a file path).
- **[#2052](https://github.com/netease-youdao/LobsterAI/pull/2052)** *(Merged)*: Fixed a regression where selected active skills were cleared when the user switched models.
- **[#2053](https://github.com/netease-youdao/LobsterAI/pull/2053)** *(Merged)*: Fixed model select dropdown UI.
- **[#2056](https://github.com/netease-youdao/LobsterAI/pull/2056)** *(Merged)*: Introduced a "HTML Share" feature.

## 4. Community Hot Topics

No explicit comment counts or reactions were present in the data to perform standard "hotness" scoring. However, the following works represent the highest community-impact topics based on scope:

- **OpenClaw Integration Suite** (PRs [#2045](https://github.com/netease-youdao/LobsterAI/pull/2045), [#2054](https://github.com/netease-youdao/LobsterAI/pull/2054), [#2055](https://github.com/netease-youdao/LobsterAI/pull/2055)): A coordinated set of merges suggesting a strong product push towards a unified skill management pipeline. The underlying need is a seamless experience between OpenClaw plugins and LobsterAI’s native manager.
- **Tool Loop Stability** (PR [#2051](https://github.com/netease-youdao/LobsterAI/pull/2051)): The fact that this is a re-fix indicates users likely encountered sporadic agent hangs or runaway loops in the cowork environment.

**Active Contributors:**
- **btc69m979y-dotcom**: Drove the OpenClaw sync system and the Windows OAuth fix.
- **fisherdaddy**: Addressed the tool loop breaker, cowork timing, app update infrastructure, and model select UI.
- **liugang519**: Contributed the HTML Share feature.

## 5. Bugs & Stability

*No new issues were filed today, but several critical bugs were fixed via PRs.*

| Severity | Bug | Status / Fix |
|---|---|---|
| **High** | **Recurring Tool Loop** — Agents failing to break out of infinite tool call cycles (re-fix). | Fixed in [#2051](https://github.com/netease-youdao/LobsterAI/pull/2051). |
| **High** | **Windows OAuth Blocked** — Dev mode on Windows completely broken for OAuth callbacks. | Fixed in [#2059](https://github.com/netease-youdao/LobsterAI/pull/2059). |
| **Medium** | **Skill Sync Data Overwrite** — OpenClaw settings overwriting local skill state. | Fixed in [#2055](https://github.com/netease-youdao/LobsterAI/pull/2055) (gated behind flag). |
| **Medium** | **Active Skills Reset on Model Switch** — User-selected skills cleared when changing model. Root cause identified (`agentService.updateAgent()` unconditionally resyncs skills on any update). | Fixed in [#2052](https://github.com/netease-youdao/LobsterAI/pull/2052). |
| **Low** | **Internal Plugins Exposed to Sync** — Provider plugins (Anthropic, OpenAI, DeepSeek, etc.) falsely detected for synchronization. | Fixed in [#2054](https://github.com/netease-youdao/LobsterAI/pull/2054). |

## 6. Feature Requests & Roadmap Signals

The data points to a clear strategic shift towards **deep platform integration**.

- **OpenClaw as a Skill Backend**: The majority of code changes revolve around treating OpenClaw as a first-class skill source. Expect this to be a tentpole feature in the next minor version.
- **Agent Visual Identity**: The presence of the **Image Avatar** PR ([#1760](https://github.com/netease-youdao/LobsterAI/pull/1760)) signals intent to move beyond emoji-only avatars, enabling richer agent customization. This is likely aimed at the upcoming release.
- **Infrastructure Modernization**: The open PR [#2057](https://github.com/netease-youdao/LobsterAI/pull/2057) replaces a deprecated VBScript launcher with PowerShell for app updates, hardening the Windows update pipeline.

**Prediction for Next Version**:
- Official OpenClaw skill sync (possibly stable).
- Agent image avatar management.
- HTML content sharing support.

## 7. User Feedback Summary

Derived from the bugs fixed and features built:

- **Pain Points Addressed**:
  - Windows developers were completely blocked on OAuth flows in dev mode.
  - Users experienced frustration when their active skill selections were silently cleared upon model switching.
  - Users integrating OpenClaw faced data conflicts due to automatic, un-gated sync.
- **Satisfaction Signals**:
  - The community’s heavy focus on contributing to the skill management and cowork systems suggests high engagement with the agent-building features.
  - Zero issues filed today indicates stability for the user base on the current release channel.

## 8. Backlog Watch

Two long-standing PRs remain in an open and potentially conflicted state, raising concerns about contributor experience:

- **[#1760](https://github.com/netease-youdao/LobsterAI/pull/1760)** — **feat(agent): support image avatars alongside emoji avatars**
  - *Created:* 2026-04-20 | *Last Update:* 2026-05-26
  - *Status:* Tagged `stale`. Open for **37 days**.
  - *Risk:* A large feature (image upload, backend storage, new UI) waiting on review risks heavy merge conflicts and burnout for contributor `leedalei`.

- **[#1773](https://github.com/netease-youdao/LobsterAI/pull/1773)** — **fix(i18n): add missing 'edit' translation key for memory entry button**
  - *Created:* 2026-04-21 | *Last Update:* 2026-05-26
  - *Status:* Tagged `stale`. Open for **36 days**.
  - *Risk:* A trivially small, safe fix (adding `edit: '编辑'` / `edit: 'Edit'`) going unreviewed for over a month sends a poor signal to external contributors on localization.

**Actionable Advice:** Prioritizing the review and merge of the i18n fix (or a comment explaining the delay) and the image avatar feature (deciding scope or providing reviewer feedback) would significantly improve community health.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — 2026-05-27

**Data Snapshot:** 2 issues updated, 2 PRs updated, 0 releases published.

---

### 1. Today's Overview

Moltis exhibited moderate development activity over the past 24 hours, led by the merging of a major architectural PR (#1049) that restructures agents as the core capability boundary. This feature lays the groundwork for per-channel, multi-context agent security and control. A high-severity bug was reported in the core `fork` command (#1075), while an open PR advances embedding configuration flexibility (#1074). The project also received an external partnership inquiry from the managed-hosting provider MyClaw.ai (#1076), signaling growing commercial ecosystem interest. No new releases were cut today, though the merged PR is a strong candidate for the next version.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress

**Merged PR (Closed):**
- **[#1049 — feat: agents as capability boundaries (MCP, sandbox, skills)](https://github.com/moltis-org/moltis/pull/1049)** by penso
  - A foundational architectural change: each agent preset now controls its own model, MCP servers, sandbox policy, and skill set.
  - Agents are assignable to specific channels, enabling distinct contexts (e.g., child vs. parent, work vs. personal) to have separate secure profiles.
  - This is a significant step toward robust multi-user support and granular security boundaries within the single-binary Rust server.

---

### 4. Community Hot Topics

- **[#1076 — Partnership inquiry: MyClaw.ai × Moltis](https://github.com/moltis-org/moltis/issues/1076)**
  - Opened today by LeoYeAI (CEO of MyClaw.ai). The inquiry explores managed cloud hosting for Moltis based on the OpenClaw platform.
  - No comments yet, but the signal is notable: it indicates Moltis’s “secure, persistent personal agent server” pitch is resonating with infrastructure providers and validates the project’s production-oriented design.

- **[#1074 — (memory): Configurable embedding dimensions with safe auto-reindex](https://github.com/moltis-org/moltis/pull/1074)**
  - Open PR adding an optional `dimensions` config for OpenAI-compatible embedding providers plus automatic reindexing on dimension change.
  - No discussion yet, but this addresses a concrete user need for memory-system flexibility.

Overall comment volume remains very low across items, typical for a project focused on deep core development rather than community debate.

---

### 5. Bugs & Stability

- **Severity: High**
  - **[#1075 — [Bug]: "fork" forks at prompt, not response](https://github.com/moltis-org/moltis/issues/1075)** by vvuk
  - The `fork` command branches conversation from the user’s prompt text instead of the model’s response text, breaking the expected branching behavior.
  - This is a functional defect in a core UX feature that could cause session confusion for users.
  - **Status:** No fix PR raised yet. Requires prompt triage.

No other crashes, regressions, or stability issues were reported today.

---

### 6. Feature Requests & Roadmap Signals

- **Configurable embedding dimensions ([#1074](https://github.com/moltis-org/moltis/pull/1074)):** This open PR is the strongest feature signal today. It allows users to set `dimensions` for embedding providers and automatically reindex when dimensions change. This reflects demand for optimizing memory/RAG against different provider cost/performance tradeoffs, and is likely to land in the next minor release.

- **Agent capability boundaries ([#1049](https://github.com/moltis-org/moltis/pull/1049)):** Now merged, this lays the architecture for flexible role-based agent assignment and should enable downstream features like user-level sandboxing and channel-specific contexts.

- **Managed hosting interest ([#1076](https://github.com/moltis-org/moltis/issues/1076)):** While external, the MyClaw.ai inquiry functions as a soft roadmap signal. A managed cloud variant of Moltis is not yet on the roadmap but is clearly in demand from observers with commercial interests.

---

### 7. User Feedback Summary

Direct user feedback is sparse but actionable:

- **Pain point — Fork behavior ([#1075](https://github.com/moltis-org/moltis/issues/1075)):** A specific UX bug is broken, indicating either a regression or an oversight in the branching logic that needs immediate correction.
- **Missing flexibility — Embedding config ([#1074](https://github.com/moltis-org/moltis/pull/1074)):** A contributor is proactively solving a gap in memory-system configuration, suggesting users need provider-agnostic flexibility in embedding dimensions.
- **Market validation — Partnership inquiry ([#1076](https://github.com/moltis-org/moltis/issues/1076)):** External validation that Moltis’s architecture is seen as ready for production hosting, supporting the project’s “one binary, sandboxed” positioning.

---

### 8. Backlog Watch

*Note: The provided snapshot covers only the last 24 hours, so long-dormant items are not visible within this data.*

Items requiring maintainer attention to prevent backlog drift:

- **[#1075 — Fork bug](https://github.com/moltis-org/moltis/issues/1075) (High severity):** Needs triage, assignment, and likely a hotfix. No PR exists yet.
- **[#1074 — Embedding dimensions PR](https://github.com/moltis-org/moltis/pull/1074):** Open for ~1 day. Needs maintainer code review or feedback to move toward merge or iteration.
- **[#1076 — Partnership inquiry](https://github.com/moltis-org/moltis/issues/1076):** Requires a strategic response to explore the potential relationship with MyClaw.ai and assess shared roadmap interests.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest: QwenPaw
**Report Date: 2026-05-27**
**Source: agentscope-ai/QwenPaw**

---

## 1. Today’s Overview

QwenPaw experienced very high development activity over the past 24 hours, with 33 issues updated and 29 pull requests active. The close rate remains moderate (11 issues closed, 8 PRs merged), indicating a maintainer team that is actively processing contributions but also facing an expanding queue of community feedback and beta regressions. The project is currently between releases, with `v1.1.9-beta.1` serving as the latest iteration. Activity clusters around three themes: hardening the v1.1.x line against regressions (WebSocket reliability, session state integrity, audio processing), deepening the Coding mode experience, and broad community requests for enterprise-grade features (RBAC, workspace management, plugin channels). The sheer volume of first-time contributor PRs signals a healthy, engaged community, though the accumulation of critical bugs—particularly around macOS Tahoe compatibility and a ToolGuard security bypass—indicates the project is under strain from its own shipping velocity.

---

## 2. Releases

*No new releases today. Latest is `v1.1.9-beta.1`.*

---

## 3. Project Progress

**Merged/Closed PRs (8 total):**

- **`#4695`** (Closed): Upgraded `@agentscope-ai/chat` library to fix stop signal handling and inline tool call rendering — directly resolves the high-traffic issue `#4644` (console tool calls not displaying).
- **`#4294`** (Closed, Fixes `#3984`): Restructures context compaction logic to keep history boundaries on user messages, preventing orphaned assistant cards in the UI.
- **`#4383`** / **`#1896`** (Closed): Series of audio processing fixes that accept top-level `data` fields in audio blocks, unblocking Telegram voice message support after 2+ months of open state.
- **`#4694`** (Closed): Refactored website downloads UI with optimized display.

**Open PRs Advancing Core Features:**

- **`#4716`** (`rayrayraykk`): Introduces per-hunk Keep/Undo overlays in Coding mode diff editor + smart copy-to-chat — major UX upgrade for code review workflows.
- **`#4708`** (`szetohoyan`, *first-time contributor*): Adds Feishu topic/thread reply support, routing responses via the Feishu Reply API rather than top-level messages.
- **`#4706`** (`JasonBuildAI`): Replaces naive JSON overwrites with atomic tmp-file writes (`os.replace`) in session state saving — critical for preventing session corruption on crash.
- **`#4689`** (`leoleils`): Routes non-standard provider `generate_kwargs` (e.g., DashScope `enable_search`) into `extra_body` to prevent silent rejection by the OpenAI SDK — a clean compatibility bridge.
- **`#4701`** (`anThreeBody`): Adds an "Approve All" button to tool-guard approval cards, letting users unblock multi-step tool chains in a single click.
- **`#4693`** (`hongxicheng`): Allows plugins to register custom channels via `api.register_channel()`, with auto-generated frontend configuration forms — foundational plugin architecture shift.
- **`#4683`** (`jinglinpeng`): Fixes Tauri desktop external link and download handling by routing through runtime-aware helpers, fixing regressions in the desktop bundle.

---

## 4. Community Hot Topics

| Issue/PR | Comments | Theme | Analysis |
|----------|----------|-------|----------|
| [`#4644`](https://github.com/agentscope-ai/QwenPaw/issues/4644) **Closed** | 18 | Console tool calls invisible | Highest-traffic bug of the period, resolved by `#4695`. Community frustration centered on trust degradation ("nothing shows up until refresh"). |
| [`#1516`](https://github.com/agentscope-ai/QwenPaw/issues/1516) **Closed** | 9 | Telegram audio support | Long-dormant critical integration bug, finally closed across three merged PRs (`#1896`, `#4383`). |
| [`#4680`](https://github.com/agentscope-ai/QwenPaw/issues/4680) **Closed** | 7 | Agent disappears after skill rename | High-emotion bug ("HELP... 啊啊啊啊啊") caused by YAML/Parse errors during restart. Closed rapidly by maintainers, but highlights poor error recovery in skill management. |
| [`#4625`](https://github.com/agentscope-ai/QwenPaw/issues/4625) **Open** | 5 | MiniMax M2.5 XML breaks agent | Pervasive provider compatibility issue. MiniMax returns reasoning XML tags that QwenPaw's parser does not filter, causing full execution halts. No in-progress PR. |
| [`#4712`](https://github.com/agentscope-ai/QwenPaw/issues/4712) **Open** | 4 | v1.1.9-beta.1 CLI / WebSocket failures | Regression blocking local tool execution on Windows. Root cause identified as subprocess not sharing host WebSocket context. |
| [`#4662`](https://github.com/agentscope-ai/QwenPaw/issues/4662) **Open** | 5 | Message timestamps in chat UI | Broadly supported quality-of-life feature. PR `#4699` already submitted. |

**Underlying Needs Analysis:**
The community is signaling three clear needs simultaneously: **reliability** (UI rendering trust, data integrity, clean error recovery), **provider agnosticism** (MiniMax, DashScope, Xiaomi models should "just work"), and **professional UX** (timestamps, session history persistence, approval workflows). The discussion drift suggests users are evaluating QwenPaw for production workloads and hitting the friction points.

---

## 5. Bugs & Stability

### Critical & Security
- **`#4709`** - ToolGuard Bypass: `_headless_tool_guard` fails to prevent an agent from reading process environment variables via `execute_shell_command` in interactive sessions. **Security bypass.** Requires immediate triage.
- **`#4704`** - macOS Tahoe 26.5 Crash: Desktop app SIGSEGV in `tokio-rt-worker` on Feishu messages. Blocks all macOS desktop users on latest OS. No fix PR yet.
- **`#4712`** - Windows CLI/WebSocket Disconnect: Subprocess CLI tools (Feishu CLI, etc.) cannot connect to local system services due to WebSocket context isolation in v1.1.9-beta.1.

### High Impact
- **`#4714`** - Task Queue Blocked: New tasks cannot be queued during active inference; user must manually stop and retry. Parallel task execution regression.
- **`#4713`** - Session History Loss: Switching pages during active conversation loses session context; restart fails to restore active agent/session state.
- **`#4705`** - Mission Phase 2 Infinite Loop: Mission Mode continues outer iteration loop even after the agent explicitly requests missing user input (observed: Cloud API key request).
- **`#4697`** - WeChat Poll Thread Crash: Workspace zero-downtime reload kills the WeChat event loop with no auto-recovery.
- **`#4666`** - Models Config Load Failure: New chat session erases all model configuration; "Load failed" until restart.

### Fixed or in Review
- **`#4644`** (Console tool display bug) -> Fixed by `#4695`.
- **`#3984`** (Orphaned assistant messages in history) -> Fixed by `#4294`.
- **`#4706`** (Session JSON corruption on crash) -> Fix PR in review.

---

## 6. Feature Requests & Roadmap Signals

### Likely for Next Stable Release
| Suggestion | Issue | Supporting PR/Signal |
|------------|-------|---------------------|
| Per-message timestamps | [`#4662`](https://github.com/agentscope-ai/QwenPaw/issues/4662) | PR `#4699` ready |
| Non-standard provider params (`extra_body`) | [`#4688`](https://github.com/agentscope-ai/QwenPaw/issues/4688) | PR `#4689` in review |
| Task queue / concurrent inference | [`#4714`](https://github.com/agentscope-ai/QwenPaw/issues/4714) | Implied by regression complaint |
| Atomic session writes | (Implied) | PR `#4706` in review |
| Approve-all tool guard | [`#4701`](https://github.com/agentscope-ai/QwenPaw/pull/4701) | Open PR |

### Strategic / Longer-Term
- **Plugin Channel System** (`#4642`, `#4693`): Non-invasive hooks for Context, Memory, Skills, Channels — represents a major architectural upgrade toward a true plugin SDK.
- **Conversation Fork/Rewind/Regen** (`#4703`): Branching UI similar to Claude or ChatGPT, suggests ambition to compete on conversation UX depth.
- **Working Directory Management** (`#4408`): `.qwenpaw` config folder pattern, mirroring OpenCode, indicates priority on developer workflow alignment.
- **Enterprise RBAC** (`#4702`): Admin user management, driven by enterprise selection teams evaluating QwenPaw as organizational chat platform.
- **New Channel Integrations**: Yuanbao (`#4711`), Xiaomi MiMo provider (`#4715`) — steady expansion of the channel/provider ecosystem.

### Prediction
The upcoming v1.2.x stable is shaping up to emphasize **provider robustness** (extra_body, MiniMax compatibility), **UX polish** (timestamps, forking, file artifacts), and **session reliability** (atomic writes, task queues). Plugin architecture will likely land experimentally in a beta release behind a feature flag.

---

## 7. User Feedback Summary

**Satisfaction Drivers:**
- The Coding mode diff editor is receiving heavy usage; community members are building UX enhancements on top of it (per-hunk controls, copy-to-chat).
- The instrument-level extensibility (channel registration, provider configuration) is enabling power users to wedge QwenPaw into diverse production environments.
- Response times for bug fixes are fast: `#4644` (tool display) resolved in ~3 days, `#4680` (agent disappearance) resolved in <24 hours.

**Key Pain Points:**
- **Beta fatigue**: A single user (`rescodexa`) filed three high-impact bugs today (`#4712`, `#4713`, `#4714`) across CLI, history, and task management — all regressions in `v1.1.9-beta.1`.
- **Data integrity anxiety**: `#4680` ("My agent is gone!") and `#4706` (session corruption fix) show users trust QwenPaw with memory and agent config but are being burned by fragile I/O.
- **Provider fragmentation**: MiniMax (`#4625`) and macOS Tahoe (`#4704`) crashes show the pain of rapid platform/channel expansion without sufficient abstraction testing.
- **UX humility gaps**: Missing timestamps, orphaned assistant cards, and invisible tool calls erode user trust in what is otherwise a powerful agent framework.

**Community Health:**
Extremely strong. The count of first-time-contributor PRs (`#4717`, `#4708`, `#4615`) alongside sophisticated feature engineering (`#4693`, `#4716`, `#4701`) demonstrates a project successfully attracting a wide spectrum of contributors from casual bug-fixers to deep infrastructure hackers.

---

## 8. Backlog Watch

*Issues and PRs requiring maintainer attention or action:*

| Item | Date | Status | Risk |
|------|------|--------|------|
| [`#4709`](https://github.com/agentscope-ai/QwenPaw/issues/4709) | 2026-05-27 | Open, unassigned | 🔴 **CRITICAL**: ToolGuard security bypass. Environment variable leak risk. |
| [`#4704`](https://github.com/agentscope-ai/QwenPaw/issues/4704) | 2026-05-26 | Open, no fix | 🔴 **CRITICAL**: macOS Tahoe SIGSEGV kills desktop app. Apple ecosystem blocker. |
| [`#4666`](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 2026-05-25 | Open | 🟡 **HIGH**: Models config completely lost on new session. Data loss scenario. |
| [`#4625`](https://github.com/agentscope-ai/QwenPaw/issues/4625) | 2026-05-22 | Open, 5 comments | 🟡 **HIGH**: MiniMax provider broken for all users of that endpoint. No PR yet. |
| [`#4006`](https://github.com/agentscope-ai/QwenPaw/issues/4006) | 2026-05-02 | Open, 3 comments | 🟡 **MEDIUM**: Reasoning content unfiltered in OpenAI provider. Lingering for 25 days. |
| [`#4615`](https://github.com/agentscope-ai/QwenPaw/pull/4615) | 2026-05-22 | Open, "Under Review" | 🟡 **MEDIUM**: ACP orphan process fix. No review activity since submission. |
| [`#4464`](https://github.com/agentscope-ai/QwenPaw/pull/4464) | 2026-05-17 | Open | 🟡 **MEDIUM**: Python E2E migration PR, large surface area, awaiting maintainer review (10 days stale). |
| [`#4408`](https://github.com/agentscope-ai/QwenPaw/issues/4408) | 2026-05-15 | Open, 4 comments | 🟢 **LOW**: Workspace config folder feature request. Unresponded to. |
| [`#4642`](https://github.com/agentscope-ai/QwenPaw/issues/4642) | 2026-05-23 | Open | 🟢 **LOW**: Plugin architecture proposal. Detailed spec, needs roadmap acknowledgment. |

**Maintainer Action Items:**
1. **Triage `#4709` (Security) and `#4704` (macOS) immediately** — these are blocker-quality issues for production/daily driving scenarios.
2. **Respond to `#4666` (Models config loss)** — this smells like a critical initialisation bug and mirrors the data integrity fears in `#4680` / `#4706`.
3. **Review blocking PRs `#4615` and `#4464`** — both fix concrete regressions and have been waiting over 5 days for signal.
4. **Provide timeline/guidance on `#4625` (MiniMax)** — users are clearly evaluating provider parity as a dealbreaker.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

ZeptoClaw Project Digest – 2026-05-27

## Today’s Overview
The past 24 hours in ZeptoClaw were dominated by automated maintenance, with 16 Dependabot-driven pull requests touching the project’s Rust backend, JavaScript documentation sites, Docker base images, and CI workflows. No user-submitted issues or pull requests were created or updated, and no new releases were published. While this indicates a healthy automated pipeline keeping dependencies current, the complete absence of human-authored activity — features, bugs, or discussions — makes this a quiet period for community-facing development. Overall project health remains stable, but momentum is currently driven entirely by supply-chain hygiene rather than functional innovation.

## Releases
**None.** No new versions were cut in the last 24 hours.

## Project Progress
Two dependency pull requests were merged, representing successfully completed maintenance chores:
- **#578 (merged):** Bumped `astro` from 6.1.6 to 6.3.1 for the `/landing/zeptoclaw/docs` site ([qhkm/zeptoclaw PR #578](qhkm/zeptoclaw%20PR%20#578))
- **#572 (merged):** Bumped `@astrojs/starlight` from 0.38.3 to 0.39.2 for the `/landing/r8r/docs` site ([qhkm/zeptoclaw PR #572](qhkm/zeptoclaw%20PR%20#572))

The remaining 14 open pull requests cover a broad update sweep across the project’s technology stack:
- **Rust:** `tower-http` (0.6.8 → 0.6.10), `clap` (4.6.0 → 4.6.1), `mail-parser` (0.11.2 → 0.11.3), `uuid` (1.23.0 → 1.23.1), `bcrypt` (0.19.0 → 0.19.1)
- **JavaScript:** `eslint` (10.0.2 → 10.3.0), `astro` (for r8r/docs), `@astrojs/starlight` (for both docs sites)
- **Docker:** Rust base image (1.93 → 1.95), Debian slim digest update
- **CI/CD:** `taiki-e/install-action` (2.77.3 → 2.78.2), `EmbarkStudios/cargo-deny-action` (2.0.17 → 2.0.18)

*Notable:* An identical `astro` bump for `zeptoclaw/docs` that was previously merged (#578) was re-opened as a new pending PR (#607), suggesting either a recreated manifest trigger or an automated rebase cycle.

## Community Hot Topics
**No community discussion occurred.** Zero open or updated issues, and zero comments across all pull requests. The public discussion board is effectively silent; every item on the recent-activity list is an uncommented Dependabot chore. The community has provided no signal for pain points, praise, or desired features in this window.

## Bugs & Stability
**No bugs or regressions were reported in the last 24 hours.** The absence of bug reports could signify strong stability in the current release, but given the equally absent user engagement in other areas, it is just as likely a reflection of low active testing or usage volume this cycle. No stability-related fix PRs exist.

## Feature Requests & Roadmap Signals
**No explicit feature requests were submitted.**
However, the pattern of dependency upgrades offers indirect roadmap signals:
- The simultaneous updates to `astro`, `@astrojs/starlight`, `eslint`, and the Docker/CI base layers suggest the maintainers are preparing the environment for whatever comes next, likely aiming to ship a doc-site refresh or a release that requires Rust 1.95 and modern JS tooling.
- The update of `mail-parser` and `bcrypt` (auth) hints at ongoing work in the core backend’s data-handling and security layer.
- No major new features or protocol changes are detectible from this purely maintenance-oriented data set.

## User Feedback Summary
**No user feedback was captured today.** With zero comments and zero issues, it is impossible to derive satisfaction, dissatisfaction, or common use cases. This may indicate that the current stable state of the project meets user needs without friction, or that the primary channels for feedback lie outside this GitHub dashboard during this period.

## Backlog Watch
**No critical backlogs or neglected items are visible within this 24-hour window.** The two long-standing Dependabot PRs (#578, #572) that had been open since May 5 were eventually closed/merged, showing the maintainers are clearing the automation queue. The 14 open Dependabot PRs are routine and do not require special maintainer escalation. No human-authored issues are lingering stale. The project’s backlog currently carries no distress signals.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-05-27**.

---

## ZeroClaw Project Digest — 2026-05-27

### 1. Today’s Overview
ZeroClaw maintains a very high cadence of activity with **34 PRs updated** and **6 issues active** in the last 24 hours, though no new release was cut. The project is clearly sprinting toward a major milestone centered around the forthcoming **zeroCode TUI and Beta-2 integration** (PR #6848), while parallel efforts focus on maturing the skills subsystem and rapidly deploying hotfixes for provider and UI friction. The immediate turnaround from bug report to fix PR—visible for issues #6944, #6950, and #6953—indicates an exceptionally responsive merge/review cycle. The contributor mix remains diverse and healthy, with patches coming from both core team members and external contributors across every subsystem.

### 2. Releases
*No new releases were published in the last 24 hours.*

### 3. Project Progress (Merged & Closed PRs)
Five PRs were merged or closed. Two are explicitly visible in the dataset:

- **[[#6512]](https://github.com/zeroclaw-labs/zeroclaw/pull/6512) fix(channels/email): HTML body rendering, subject threading, attachment path resolution**  
  *Status: Merged.* This fix resolved three long-standing email channel issues (raw markdown in clients, unhelpful default subjects, and zero-byte attachment failures), touching support scaffolding across over a dozen other channel implementations.

- **[[#6901]](https://github.com/zeroclaw-labs/zeroclaw/pull/6901) fix(providers): Preserve full reqwest error chains**  
  *Status: Merged.* Provider transport failures now expose the full error chain (timeout vs. DNS vs. TLS) instead of collapsing to opaque one-line messages—a meaningful debug-ability improvement across all model providers.

**In-flight signals:**
The massive **[[#6848]](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)** (`feat: zeroCode TUI, RPC socket transport, DenyWithEdit, beta-2 integration`) saw continued updates, but remains explicitly flagged **DO NOT MERGE** with known unresolved issues around Delegates, fallback behavior, and context counters.

### 4. Community Hot Topics
- **[[#6059]](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) Bug: Incompatible with DeepSeek-V4 API format** (👍 4, 💬 13)  
  The most active issue by a wide margin. Users of both DeepSeek-V4-Pro and V4-Flash are fully blocked by an API incompatibility traced to the “thinking mode” format. Despite being open since April 24 (33 days) and labeled `priority:p1`, no fix branch has merged. This is the strongest single pain signal in the current tracker.

- **[[#6909]](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) Feature: Computer-use support (screen interaction)** (💬 3)  
  Mirroring the industry-wide push toward GUI-based agent control (Codex / Peekaboo), this request has immediate community resonance. ZeroClaw currently has no desktop interaction capability, making this a clear gap vs. competing projects.

- **[[#6954]](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) RFC: Route scheduled tasks through the orchestrator message pipeline**  
  Though light on discussion comments, this RFC is architecturally significant. The author identifies the cron scheduler’s direct-side-effect execution as the root cause of five separate bugs (#6037, #6105, #6648, #6632, #6686). The outcome of this RFC will directly shape the platform’s reliability story.

### 5. Bugs & Stability (Ranked by Severity)

**Critical (S2 – Degraded Behavior)**
- **[[#6059]](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) DeepSeek-V4 API failure** | *High risk, priority P1, status in-progress.* Blocks an entire model provider family. Ongoing for 33 days.
- **[[#6944]](https://github.com/zeroclaw-labs/zeroclaw/issues/6944) Interactive mode log interleaving** | *High risk.* System logs drown out assistant replies in TTY mode. → **Fix deployed:** PR [[#6947]](https://github.com/zeroclaw-labs/zeroclaw/pull/6947) suppresses INFO-level logs in interactive mode.

**High**
- **[[#6950]](https://github.com/zeroclaw-labs/zeroclaw/issues/6950) TUI unusable on compact keyboards** | Users without dedicated F-keys (Logitech MX Keys Mini, Keychron K-series) are locked out of mode switching. → **Fix deployed:** PR [[#6952]](https://github.com/zeroclaw-labs/zeroclaw/pull/6952) adds Tab/Shift+Tab cycling.
- **[[#6908]](https://github.com/zeroclaw-labs/zeroclaw/pull/6908) Codex subscription auth blocked** | OpenAI onboarding only offered API-key flow, excluding ChatGPT Plus/Pro OAuth users. → **Fix deployed** in the same PR.
- **[[#6953]](https://github.com/zeroclaw-labs/zeroclaw/pull/6953) SiliconFlow wrong default endpoint** | `DEFAULT_URL` pointed to `.cn` while API keys are issued for `.com`, causing a silent auth mismatch. → **Fix deployed** in the same PR.

**Medium**
- **[[#6934]](https://github.com/zeroclaw-labs/zeroclaw/pull/6934) Discord gateway 429 not retryable** | Rate-limit responses were wrapped as fatal errors, breaking channel supervisor backoff. → **Fix deployed** in the same PR.
- **[[#6688]](https://github.com/zeroclaw-labs/zeroclaw/pull/6688) Delegate agents ignore `prompt_injection_mode` config** | Smaller-context delegate models hit context limits unnecessarily.
- **[[#6719]](https://github.com/zeroclaw-labs/zeroclaw/pull/6719) `model_switch` not persisting across turns** | Runtime tool works on current turn but is lost on the next inbound message.

### 6. Feature Requests & Roadmap Signals
- **Beta-2 / zeroCode TUI ([#6848])**: The single largest in-flight integration. It defines the next user experience era of ZeroClaw (new TUI, RPC transport, DenyWithEdit approval model). Its resolution—whether split into merges or shipped monolithically—will dictate the next release timeline.
- **Skills Ecosystem Expansion**: A clear roadmap theme is transforming skills into autonomous, self-improving modules.
  - *Background review forks* [[#6667]](https://github.com/zeroclaw-labs/zeroclaw/pull/6667) and *cooldown enforcement* [[#6684]](https://github.com/zeroclaw-labs/zeroclaw/pull/6684) enable agents to self-improve without user intervention.
  - *Tool elevation* [[#6924]](https://github.com/zeroclaw-labs/zeroclaw/pull/6924) allows skills to request specific blocked tools (`builtin`, `composio`), enabling granular security elevation without blanket agent permissions.
  - *Runtime tool filtering* [[#6920]](https://github.com/zeroclaw-labs/zeroclaw/pull/6920) closes a bypass vector in MCP deferred tools.
- **MCP Bridge Tools ([#6946])**: Exposing resource and prompt bridges as synthetic tools strengthens the MCP protocol integration story.
- **Per-Agent Classifier Provider ([#6945])**: A direct response to cost optimization feedback—allowing cheap models to handle reply-intent routing on expensive agent instances.

### 7. User Feedback Summary
- **Pain Points (Urgent)**  
  The **DeepSeek-V4 breakage** (#6059) is the loudest, most universal blocker reported. The **TTY log noise** (#6944) was a clear daily-driver regression that was rapidly addressed. Users on **non-standard hardware** (compact keyboards) were explicitly excluded from the TUI, and the community responded with a targeted patch (#6952) within hours.

- **Power User Demands**  
  There is a strong, sophisticated signal for genuine **agentic autonomy**: desktop automation (#6909), self-improving skills (#6667, #6684), and robust cron task handling (#6954). The community is not treating ZeroClaw as a simple chatbot; they are building autonomous systems on top of it.

- **Satisfaction Drivers**  
  The most significant satisfaction signal is the **speed of maintainer response**. The rapid pairing of bug reports (#6950, #6944, #6934) with almost immediate fix PRs builds high trust. The contributor base is also impressive in its diversity—patches from `theonlyhennygod`, `NiuBlibing`, `Audacity88`, `Project516`, `mov-xound-glitch`, `alex-nax`, `JordanTheJet`, and `tidux` all in a single 24-hour window indicates a very healthy community.

### 8. Backlog Watch (Action Required)

| Item | Age | Status | Risk |
|---|---|---|---|
| **[[#6059]](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) DeepSeek-V4 Compatibility** | 33 days | `priority:p1`, `status:in-progress`, no fix merged | **Critical.** This is the release blocker for all DeepSeek users. Needs immediate maintainer attention or a published workaround. |
| **[[#6667]](https://github.com/zeroclaw-labs/zeroclaw/pull/6667) Skills Background Review + [[#6684]](https://github.com/zeroclaw-labs/zeroclaw/pull/6684) Cooldowns** | 12–13 days | `needs-author-action` | **High.** These set-the-foundation PRs are the gateway to the entire skills autonomy roadmap. Stalling creates a compound backlog across dependent features (#6924). |
| **[[#6719]](https://github.com/zeroclaw-labs/zeroclaw/pull/6719) Model Switch Persistence** | 11 days | Open, high risk | **High.** A core runtime reliability fix (dynamic model switching silently fails on subsequent turns). Under-review duration is becoming a concern. |
| **[[#6848]](https://github.com/zeroclaw-labs/zeroclaw/pull/6848) ZeroCode / Beta-2 Integration** | 5 days | DO NOT MERGE | **Project Bottleneck.** The most exciting feature branch is also the most risky. Maintainers should consider incremental merges or a clear branching strategy to avoid a destabilizing monolithic merge. |

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*