# OpenClaw Ecosystem Digest 2026-06-18

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-18 03:37 UTC

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

# OpenClaw Project Digest — June 18, 2026

## 1. Today's Overview

The OpenClaw project is experiencing an extremely high volume of activity, with 500 issues and 500 pull requests updated in the last 24 hours. Of these, 480 issues and 409 PRs remain open, indicating a substantial and growing work surface where community engagement and automated triage run in parallel. 91 PRs were merged or closed today, reflecting steady forward progress in bug fixing and feature delivery. No new official releases were tagged. The project's distinctive tiered issue-rating system (Diamond Lobster, Platinum Hermit, etc.) and deep integration with the ClawSweeper automation framework suggest a mature, highly structured development culture that prioritizes systematic triage over raw velocity. The open-to-closed ratio (roughly 10:1) points to a significant triage load, but the volume of merged PRs confirms the team is actively reducing technical debt and addressing community feedback.

## 2. Releases

No new versions or releases were published today. The latest stable build accumulates ongoing fixes from the active PR pipeline.

## 3. Project Progress

91 pull requests were merged or closed in the past 24 hours. While the most actively discussed PRs remain open for review, the high merge volume suggests consistent discipline in landing smaller, targeted improvements. Notable fixes *submitted* today from the active PR queue (many of which are merge candidates) include:

- **Compaction Timeout Configuration** ([#94413](https://github.com/openclaw/openclaw/pull/94413)) — Wires the aggregate retry timeout for in-turn compaction to user configuration instead of the previous hardcoded 60-second limit, fixing silent failures on large (~200K token) sessions.
- **Agent Loop Abort Fix** ([#94412](https://github.com/openclaw/openclaw/pull/94412)) — Stops the agent loop after a tool aborts a run, preventing a second, invalid model invocation.
- **Sandbox Workspace Resolution** ([#94411](https://github.com/openclaw/openclaw/pull/94411), [#94396](https://github.com/openclaw/openclaw/pull/94396)) — Fixes skill sync fallback to use the user's `openclaw.json` config instead of a hardcoded environment variable.
- **Plugin Method Scopes** ([#94343](https://github.com/openclaw/openclaw/pull/94343)) — Resolves `missing scope: operator.admin` failures in the `workboard dispatch` CLI by consulting all active surface descriptors.
- **Windows Ctrl+C Handling** ([#94393](https://github.com/openclaw/openclaw/pull/94393)) — Adds readline-based keypress handling for graceful gateway shutdown on Windows.
- **Hallucinated File Extension Correction** ([#94356](https://github.com/openclaw/openclaw/pull/94356)) — Automatically corrects common LLM hallucinations (e.g., `.docodex` → `.docx`) during tool param validation.
- **Parallel.ai Default Provider Prevention** ([#94373](https://github.com/openclaw/openclaw/pull/94373)) — Prevents an unconfigured Parallel.ai from becoming the default web search provider.
- **Session Channel Routing for `sessions_send`** ([#94409](https://github.com/openclaw/openclaw/pull/94409)) — Derives the delivery channel from the resolved session entry instead of hardcoding "webchat," fixing cross-platform agent-to-agent messaging.
- **Codex MEMORY.md Context Preservation** ([#94353](https://github.com/openclaw/openclaw/pull/94353)) — Prevents agents from "forgetting" persistent bootstrap facts when memory tools are available.
- **Mattermost Text-Block Boundaries** ([#87449](https://github.com/openclaw/openclaw/pull/87449)) — Long-awaited parity with Discord for preserving draft preview text blocks during tool-heavy turns.

## 4. Community Hot Topics

### Top Issues by Discussion Volume

| Issue | Title | Comments | Rating |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | 32 | 🐚 Platinum Hermit (P1) |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Track core session/transcript SQLite migration via accessor seam | 30 | 🦞 Diamond Lobster (P0) |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | Request: Prebuilt Android APK releases | 25 | 🌊 Off-Meta Tidepool (P2) |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | Tiered bootstrap file loading for progressive context control | 17 | 🦞 Diamond Lobster (P2) |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | Control UI requires device identity (HTTPS/localhost secure context) | 17 | 🦞 Diamond Lobster (P1) |

### Top Issues by Reactions

- **Configurable streaming watchdog timeout** ([#68596](https://github.com/openclaw/openclaw/issues/68596), 8 👍) — Community strongly desires configurable timeouts for long-thinking models.
- **Sandbox `workspaceAccess` writable** ([#37634](https://github.com/openclaw/openclaw/issues/37634), 7 👍) — Sandboxed sessions find their `/workspace` mounted read-only when isolation is configured.
- **Telegram Business Bot support** ([#20786](https://github.com/openclaw/openclaw/issues/20786), 6 👍) — Strong demand for Business Mode message subscriptions.

### Underlying Needs Analysis

1. **Security & Trust** — The #1 issue by comments is a critical text leakage problem where internal processing output bleeds into messaging channels. This, combined with long-standing requests for masked secrets ([#10659](https://github.com/openclaw/openclaw/issues/10659)) and path-scoped permissions ([#39979](https://github.com/openclaw/openclaw/issues/39979)), signals a user base deeply concerned with safe, enterprise-grade agent operation.
2. **Cost Control** — High engagement on tiered bootstrap loading ([#22438](https://github.com/openclaw/openclaw/issues/22438)), per-agent cost budgets ([#42475](https://github.com/openclaw/openclaw/issues/42475)), and streaming watchdog configuration ([#68596](https://github.com/openclaw/openclaw/issues/68596)) reveals a user demographic that is token-cost-sensitive and wants granular financial governance.
3. **Platform Depth** — The simultaneous demand for Android prebuilts ([#9443](https://github.com/openclaw/openclaw/issues/9443)), Slack Block Kit ([#12602](https://github.com/openclaw/openclaw/issues/12602)), Telegram Business ([#20786](https://github.com/openclaw/openclaw/issues/20786)), and Feishu fixes ([#41744](https://github.com/openclaw/openclaw/issues/41744)) highlights a multi-platform user base pushing the agent to be a ubiquitous interface.
4. **Deterministic Control** — Requests for hard enforcement hooks ([#13583](https://github.com/openclaw/openclaw/issues/13583)), session snapshots ([#13700](https://github.com/openclaw/openclaw/issues/13700)), and post-subagent completion hooks ([#22358](https://github.com/openclaw/openclaw/issues/22358)) suggest users want to build reliable, auditable workflows on top of the agent runtime.

## 5. Bugs & Stability

### P0 (Critical)

- **[#88838](https://github.com/openclaw/openclaw/issues/88838) — Core session/transcript SQLite migration** (Diamond Lobster)  
  The effort to refactor the runtime-state persistence layer continues. The branch-by-abstraction strategy aims to avoid landing a single high-risk rewrite. This is the single highest-impact piece of infrastructure work tracked.

### P1 (High Severity)

- **[#25592](https://github.com/openclaw/openclaw/issues/25592) — Text between tool calls leaks to channels** (Security, UX)  
  The highest-commented issue. Internal processing output (error handling, acknowledgments, narration) is being routed to Slack/iMessage. Fix PR likely linked. Represents a significant trust and safety flaw.
- **[#22676](https://github.com/openclaw/openclaw/issues/22676) — Signal daemon stop() race condition** (Message Loss, Crash Loop)  
  SIGUSR1 restarts can spawn new processes before old ones release ports and locks. Fix PR linked. Source repro available.
- **[#29387](https://github.com/openclaw/openclaw/issues/29387) — Bootstrap files in `agentDir` silently ignored** (Session State)  
  Per-agent bootstrap configuration is completely ineffective if files are placed in the agent directory. Fix PR linked.
- **[#31583](https://github.com/openclaw/openclaw/issues/31583) — `exec` tool ignores `skills.entries.*.env`** (Regression, Security)  
  Environment variables configured for skills are not passed to subprocesses spawned by the `exec` tool. Fix PR linked.
- **[#32473](https://github.com/openclaw/openclaw/issues/32473) — Control UI fails on non-HTTPS** (Regression, Security)  
  Hostinger VPS/docker users blocked. Fix PR linked, but requires security review and product decision.
- **[#86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth refresh failures wedge agents** (Session State, Auth)  
  Can keep an agent retrying inside the same provider lane for hours without surfacing an operator-visible incident.
- **[#38327](https://github.com/openclaw/openclaw/issues/38327) — "Cannot convert undefined or null to object" with Vertex/Gemini** (Regression, Crash Loop)  
  Affects users on 2026.3.2. Needs maintainer review.
- **[#37634](https://github.com/openclaw/openclaw/issues/37634) — Sandbox workspace mounted read-only with `workspaceAccess: none`** (Session State)  
  Tools that need write access fail inside sandboxed sessions configured for isolation.
- **[#31331](https://github.com/openclaw/openclaw/issues/31331) — Docker sandbox cannot bind `/workspace`** (Session State)  
  Gateway inside Docker using Docker-outside-of-Docker fails to mount workspace volumes correctly.

### P2 (Medium Severity)

- **[#43747](https://github.com/openclaw/openclaw/issues/43747) — Memory management inconsistency** (Regression)  
  Three users report completely different memory storage behaviors (chunking, embedding, file structures) with the same version.
- **[#41165](https://github.com/openclaw/openclaw/issues/41165) — Telegram DMs polluting main session** (Routing)  
  A fix was applied in [#40519](https://github.com/openclaw/openclaw/issues/40519), but the problem has recurred.
- **[#37966](https://github.com/openclaw/openclaw/issues/37966) — `cacheRetention` ignored for LiteLLM-proxied Anthropic** (Behavior)  
  Cache control markers are not injected into API payloads.
- **[#41201](https://github.com/openclaw/openclaw/issues/41201) — Control UI avatar broken** (Regression)  
  External URLs and local paths both fail to render.

## 6. Feature Requests & Roadmap Signals

### Near-Term Candidates (High Community Demand, Tied to Existing Risk)

- **[#42475](https://github.com/openclaw/openclaw/issues/42475) — Per-agent cost budget enforcement** — Daily/monthly caps enforced at the gateway level before model dispatch. Directly addresses runaway spend risk.
- **[#10659](https://github.com/openclaw/openclaw/issues/10659) — Masked secrets system** — Allow agents to *use* API keys without *seeing* them, defending against prompt injection extraction.
- **[#68596](https://github.com/openclaw/openclaw/issues/68596) — Configurable streaming watchdog timeout** — High value for users running extended-reasoning models (DeepSeek-R1, Kimi-K2.5).
- **[#20786](https://github.com/openclaw/openclaw/issues/20786) — Telegram Business Bot support** — Enables bots to receive messages from Business-connected personal chats.

### Medium-Term Roadmap (RFCs and Architectural Signals)

- **[#42026](https://github.com/openclaw/openclaw/issues/42026) — Distributed Agent Runtime** — RFC proposing separation of control plane (gateway) from agent compute (runtime process). Signals the project's scaling ambitions.
- **[#35203](https://github.com/openclaw/openclaw/issues/35203) — Multi-Agent Collaboration Enhancement** — Comprehensive proposal covering capability profiling, shared blackboard, layered memory, and token cost governance.
- **[#13700](https://github.com/openclaw/openclaw/issues/13700) — Session Snapshots** — Checkpointing `/session save` and `/session load` for branching conversations and rollback.
- **[#28300](https://github.com/openclaw/openclaw/issues/28300) — Theme Customization System** — 6 curated presets plus a custom theme studio for the Control UI.

### Long-Standing Requests

- **[#9443](https://github.com/openclaw/openclaw/issues/9443) — Prebuilt Android APK** (Open since February 5). Remains a persistent community demand for mobile users who cannot compile from source.
- **[#12602](https://github.com/openclaw/openclaw/issues/12602) — Slack Block Kit support** (Open since February 9). Enterprise Slack users continue to request rich message formatting.
- **[#7707](https://github.com/openclaw/openclaw/issues/7707) — Memory Trust Tagging by Source** (Open since February 3). Unaddressed despite its clear security implications.

## 7. User Feedback Summary

### Pain Points & Dissatisfaction

1. **Reliability Regressions** — Multiple regression bugs (memory chaos [#43747](https://github.com/openclaw/openclaw/issues/43747), exec env injection [#31583](https://github.com/openclaw/openclaw/issues/31583), HTTPS requirement [#32473](https://github.com/openclaw/openclaw/issues/32473), Telegram routing [#41165](https://github.com/openclaw/openclaw/issues/41165)) suggest that recent releases have introduced stability churn frustrating the user base.
2. **Configuration Friction** — Bootstrap files being silently ignored ([#29387](https://github.com/openclaw/openclaw/issues/29387)), unclear embedding setup in the onboarding wizard ([#16670](https://github.com/openclaw/openclaw/issues/16670)), and unwieldy backup processes ([#13616](https://github.com/openclaw/openclaw/issues/13616), [#40786](https://github.com/openclaw/openclaw/issues/40786)) point to a steep learning curve for new users.
3. **Security Overhead** — The HTTPS-only requirement for Control UI and the lack of built-in secret masking create operational friction that small teams and home lab users find burdensome.
4. **Mobile Access Gap** — The absence of prebuilt APK downloads ([#9443](https://github.com/openclaw/openclaw/issues/9443)) excludes a significant segment of the potential user base.

### Satisfaction & Emerging Use Cases

- Users are actively building **multi-agent, multi-platform workflows** (A2A messaging, sub-agent spawning, cross-channel routing). The sophistication of feature requests (distributed runtime, capability profiling) indicates a technically advanced user base.
- High engagement with the **Skills/Workshop ecosystem** ([#94383 PR](https://github.com/openclaw/openclaw/pull/94383), [#42637 PR](https://github.com/openclaw/openclaw/pull/42637)) suggests a thriving plugin and extension community.
- The **ClawSweeper automation system** is widely adopted, with users growing accustomed to automated bug labeling, repro, and fix PR generation—a uniquely mature workflow for an open-source AI agent project.

## 8. Backlog Watch

### Critical Items Awaiting Maintainer Action

- **[#25592](https://github.com/openclaw/openclaw/issues/25592) — Text leakage (P1)** — Needs product decision and security review. The highest-profile unresolved security issue.
- **[#22676](https://github.com/openclaw/openclaw/issues/22676) — Signal daemon race (P1)** — Needs maintainer review on the linked fix PR.
- **[#29387](https://github.com/openclaw/openclaw/issues/29387) — Bootstrap ignored (P1)** — Needs maintainer review and product decision.
- **[#86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth wedge (P1)** — Requires a live repro from the reporter for maintainers to act.

### Stale & Aging High-Profile Items

| Issue | Opened | Status |
|---|---|---|
| [#6731](https://github.com/openclaw/openclaw/issues/6731) — Rust rewrite / safe ClawdBot (P1) | Feb 2 | No movement in over 4 months |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) — Memory Trust Tagging (P2) | Feb 3 | No fix PR ever submitted |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) — Android APK (P2) | Feb 5 | High comments, zero code movement |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) — Backup/restore utility (P2) | Feb 10 | No fix PR |
| [#13751](https://github.com/openclaw/openclaw/issues/13751) — Feishu permission overreach (P1) | Feb 11 | Linked PR open, needs security review |

### Stalled Pull Requests

- **[#75403](https://github.com/openclaw/openclaw/pull/75403) — Typing indicator fix (ClawSweeper, P2)** — Marked `waiting on author` since May 1. ClawSweeper's own automated fix is stuck on author feedback.
- **[#42637](https://github.com/openclaw/openclaw/pull/42637) — Skills omitted names on truncation (P2)** — Waiting on author since March 11.
- **[#28081](https://github.com/openclaw/openclaw/pull/28081) — Doctor auto-prune stale config (P2)** — Waiting on author since February 27.
- **[#42617](https://github.com/openclaw/openclaw/pull/42617) — Configurable pairing message per channel (P2)** — Marked `needs proof`, low activity.

---

*This digest reflects activity on the [OpenClaw GitHub repository](https://github.com/openclaw/openclaw) for the snapshot date June 18, 2026. All ratings and severity levels are as tagged in the source data.*

---

## Cross-Ecosystem Comparison

Here is your cross-project comparison report based on the June 18, 2026 community digest data.

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem on June 18, 2026, is characterized by explosive, multi-track growth and a decisive pivot from experimental chat interfaces to mission-critical, enterprise-grade infrastructure. Projects like OpenClaw, CoPaw, and ZeroClaw are operating at a scale that rivals commercial platforms, processing hundreds of contributions daily, while the security disclosures from researchers like YLChen-007 (hitting TinyClaw and LobsterAI) are forcing a landscape-wide, urgent hardening sprint. A deep bifurcation is emerging between **universal agent runtimes** focused on stability and protocol integration, and **specialized agent platforms** racing to claim specific verticals like desktop automation (Hermes, LobsterAI) or developer tooling (NanoBot). Overall, it is a maturing, highly competitive space where core infrastructure, cost governance, and security are now considered table stakes, not differentiators.

## 2. Activity Comparison

The table below summarizes the last 24 hours of activity across all tracked projects. "Health Pulse" is a qualitative assessment based on velocity, security posture, and critical bug response.

| Project | Issues Updated | PRs Updated | Merged/Closed PRs | Release(s) | Activity Tier | Health Pulse |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 91 | — | Extreme | Stable / High Triage Load |
| **NanoBot** | ~9 | 31 | 17 | — | Very High | Hardening / High Velocity |
| **Hermes Agent** | 100+ | 100+ | ~2 | — | Extreme | Reactive / Critical OAuth Break |
| **PicoClaw** | 4 | 10 | 6 | — | High | Secure / Rapid Patch Cycle |
| **NanoClaw** | 5 | 20 | 3 | **v2.1.17** | Very High | Improving / Critical Deadlock Fixed |
| **NullClaw** | 3 | 2 | 0 | — | Low | Neglected / Scheduler Bug Unaddressed |
| **IronClaw** | 47 | 50 | ~5 | — | Extreme | Straining / CI Pipeline Blocked |
| **LobsterAI** | ~1 | ~11 | 11 | **v2026.6.15** | High | Active / New CVE Surfaced |
| **TinyClaw** | 3 | 0 | 0 | — | Crisis | Critical / Unmitigated Vulns |
| **Moltis** | 2 | 1 | 0 | — | Low | Stable / Low Activity |
| **CoPaw (QwenPaw)** | 50 | 50 | 33 | **v1.1.12 / Beta** | Extreme | Booming / v2.0 Alpha Started |
| **ZeptoClaw** | 0 | 0 | 0 | — | Dead | Inactive |
| **ZeroClaw** | 50 | 50 | 11 | — | Extreme | Feature Rush / Windows Weak |

## 3. OpenClaw's Position

**Core Advantages:**
OpenClaw remains the undisputed **reference implementation and "Linux Kernel" of the AI agent ecosystem**. Its sheer scale (500 issues/PRs daily) dwarfs all peers. Its sophisticated tiered triage system (Diamond Lobster / Platinum Hermit) and the ClawSweeper automation framework give it a unique ability to manage extreme community velocity without sacrificing stability.

**Technical Approach:**
Unlike peers that are hedging on specific architectures (e.g., IronClaw's Rust Reborn engine), OpenClaw provides a deeply extensible monolithic runtime that acts as the *de facto* standard layer for the rest of the ecosystem. Other projects explicitly rely on or reference OpenClaw configurations (NanoBot's OpenClaw gateway OOM fix, LobsterAI's OpenClaw integration).

**Community Compared to Peers:**
OpenClaw’s community is the most mature and structurally organized. It drives the highest number of "Requests for Comments" (RFCs) for distributed architecture (Distributed Agent Runtime #42026), session snapshots, and multi-agent collaboration. It serves as the upstream standard against which smaller projects are measured.

## 4. Shared Technical Focus Areas

The following requirements are emerging synchronously across multiple major projects, indicating universal pressure points:

- **Security Hardening (Universal):** SSRF fixes (PicoClaw #3070, ZeroClaw #7902), path traversal CVEs (NanoClaw #2799, TinyClaw #282), and text leakage (OpenClaw #25592) dominate the bug queues. The YLChen-007 disclosures have triggered a landscape-wide security reflex.
- **Workspace Isolation & Sandboxing:** NanoBot's "Project Workspace Write Policy" (#4202) and "Read-Only Roots" (#4053) mirror OpenClaw's sandbox workspace resolution (#94411) and ZeroClaw's pending `SandboxPolicyConfig`. Users demand strict file system boundaries.
- **Context Window & Cost Economics:** The fight against token bloat is universal. OpenClaw (compaction timeout #94413, tiered loading #22438), ZeroClaw (cached token pricing #7492, context compression #7673), and NullClaw (memory recall limits #961) are all building financial governance and efficiency layers.
- **Provider Diversity & Reliability:** Anthropic OAuth breaks (Hermes #48176), Gemini 3.5 Flash field mismatches (PicoClaw #3111), and Mistral API strictness (NanoBot #4351) show the ecosystem is heavily burdened by the fragility of provider adapter code.
- **Multi-Agent & Platform Ubiquity:** A2A protocol (Hermes #514), cross-channel routing (OpenClaw), Matrix/WhatsApp/Telegram/Feishu bridges — the consensus is that a single agent must span every chat platform and be able to hand off tasks to peers.

## 5. Differentiation Analysis

The ecosystem is sharply fractured by product philosophy and target user:

| Project | Core Philosophy | Target User | Key Differentiator |
|---|---|---|---|
| **OpenClaw** | The Universal Agent Runtime | Advanced users, developers, enterprises | Stability, Triage Maturity, Extensibility |
| **NanoBot** | The DevOps Agent | Developers, CI/CD workflows | Workspace isolation, Git integration, security policy |
| **Hermes Agent** | The Premium Desktop Power Tool | Desktop power users, Mac/Windows users | Rich GUI, Computer Use, OTel, Desktop build |
| **PicoClaw** | The Privacy & Edge Agent | Privacy advocates, Sipeed hardware owners | Embedded focus, Decentralized protocols (Tox), SSRF fix |
| **NanoClaw** | The IT Fleet Manager | Managed deployments, sysadmins | Immutable deployment, upgrade tripwire, governance gates |
| **IronClaw** | The Rust Performer / AI Factory | Rust developers, NEAR ecosystem | Reborn engine, AI dogfooding (AI builds AI) |
| **LobsterAI** | The Real-Time Cowork Copilot | Enterprise teams, real-time collab | Computer Use, Voice ASR, streaming UX |
| **CoPaw (QwenPaw)** | The End-User Experience Champion | General users, non-developers | UI/UX overhauls (Simple Mode), rich built-in skills |
| **NullClaw / Moltis** | The Minimalist Utility | CLI-focused / niche users | Narrow feature focus, zero bloat |

## 6. Community Momentum & Maturity

**Tier 1 — Extreme Momentum (Core Infrastructure Wars):**
OpenClaw, CoPaw, ZeroClaw, and IronClaw are in a high-stakes feature race. OpenClaw and CoPaw are stabilizing at scale while revolutionizing their architecture (v2.0 alpha for CoPaw). ZeroClaw is aggressively shipping feature stacks (config cascade, cron pipeline). IronClaw is in the deepest technical churn with its Rust Reborn engine, but is paying the price in CI stability (#4824).

**Tier 2 — High Momentum / Hardening Phase:**
NanoBot, PicoClaw, and LobsterAI are iterating rapidly but with focus. They are actively absorbing the security lessons from Tier 4 incidents. NanoBot is particularly effective at "same-day bug lifecycles" (discover, fix, merge in 24h). LobsterAI is shipping flagship features (Computer Use) while managing OOM regression risk.

**Tier 3 — Stabilization / Maintenance:**
NullClaw and Moltis are low-volume but serve committed user bases. NullClaw represents the risk of low maintainer responsiveness (P1 scheduler bug unaddressed for over a month).

**Tier 4 — Crisis / Stalled:**
TinyClaw represents the worst case for the ecosystem: a project with critical unauthenticated API vulnerabilities (#282, #283, #284) and zero public maintainer response. This erodes trust in the broader "Claw" naming space. ZeptoClaw is effectively abandoned.

## 7. Trend Signals

The following industry trends are distilled from the community feedback and code motion across all projects:

1.  **Security is the #1 Blocking Requirement for Adoption.** The era of "quick prototype" APIs is over. Simple path traversal (LobsterAI, TinyClaw) and unauthenticated endpoints (TinyClaw) are the new existential threats. Every project must now pass a baseline "pentest" to be considered production-ready. Projects without a security review pipeline (TinyClaw) will be shunned.

2.  **The "Agent Operator" Model is Going Mainstream.** Computer Use (LobsterAI, ZeroClaw, Hermes), Cron/Scheduler improvements (ZeroClaw, CoPaw), and A2A protocols (Hermes) signal that the market demands agents that *execute work*, not just answer questions. The "passive chatbot" era is yielding to the "active digital worker" era.

3.  **Token Cost is the Hidden Tax on Popularity.** The explosive interest in streaming watchdogs (OpenClaw), compaction (NanoBot), cached pricing (ZeroClaw), and memory recall limits (NullClaw) reveals a user base deeply worried about runaway costs. The project that provides the most transparent, configurable, and aggressive cost control will have a massive retention advantage.

4.  **The Protocol Stack is Fragmented but Converging.** MCP is the universal "tool layer", but A2A is the hot new frontier. Projects are forced to support multiple protocols or build proprietary "Skills Platforms". The market is rewarding flexibility over purity.

5.  **Desktop vs. Cloud vs. Edge is a Real Divide.** Hermes and LobsterAI are betting on the desktop as the primary compute and interaction surface. NanoClaw and NullClaw are purely server-side. PicoClaw is betting on edge hardware. No one has unified the deployment experience yet, creating an opportunity for the runtime that can bridge these modes seamlessly.

6.  **"Memory" is Becoming the New State Management Problem.** The ecosystem is moving beyond simple vector stores to recall limits, trust tagging, session snapshots, and context preservation. Memory is the new database, and getting it wrong (OpenClaw #43747 memory chaos) breaks the agent promise entirely.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

NanoBot Project Digest — 2026-06-18

---

### 1. Today's Overview

NanoBot experienced exceptionally high activity today, with 31 Pull Requests updated in the last 24 hours and 17 merged or closed. This surge represents a major hardening and feature push across the provider layer, workspace security model, and chat infrastructure. The community filed 9 new issues, ranging from critical bug reports (Git command blocks, WebUI mobile zoom) to highly requested features (user-friendly wizards, multi-instance management). No formal release was cut today, but the high volume of merged fixes suggests the project is in an active pre-release hardening phase.

---

### 2. Releases

**No new releases recorded on this date.** Despite the heavy merge activity, a versioned release has not yet been published.

---

### 3. Project Progress (Merged / Closed PRs)

A torrent of features and fixes landed on `main` today, alongside robust regression test coverage.

**Provider & API Layer**
- **Better Mistral Support** ([PR #4351](https://github.com/HKUDS/nanobot/pull/4351)) – Merged. Routes Mistral models through a dedicated adapter, fixing four strict API mismatches (e.g. `reasoning_effort` values, `max_tokens` rejection, image attachment encoding, tool-use trailing whitespace).
- **Keenable Search Provider** ([PR #4350](https://github.com/HKUDS/nanobot/pull/4350)) – Merged. Adds Keenable as a built-in web search provider alongside DuckDuckGo, Brave, Tavily, etc.
- **OpenAI Image Edits** ([PR #4394](https://github.com/HKUDS/nanobot/pull/4394)) – Opened. Routes image edits to the correct `/images/edits` endpoint with multipart upload for GPT-Image models.
- **Anthropic Tool ID Sanitization** ([PR #4356](https://github.com/HKUDS/nanobot/pull/4356)) – Merged. Fixes 400 errors from the Anthropic API when tool IDs contain invalid characters (pipes, dots).
- **Proxy & Local Endpoints** ([PR #4367](https://github.com/HKUDS/nanobot/pull/4367)) – Merged. Stops `HTTP_PROXY` from breaking local model servers (Ollama, vLLM, llama.cpp).

**Workspace, Security & Memory**
- **Project Workspace Write Policy** ([PR #4202](https://github.com/HKUDS/nanobot/pull/4202)) – Merged. Aligns `apply_patch` with workspace access policy and adds explicit read/write allowed directory separation.
- **Read-Only Roots** ([PR #4053](https://github.com/HKUDS/nanobot/pull/4053)) – Merged. Keeps extra allowed roots read-only, preventing write/edit tools from inheriting media-dir access.
- **Git in Subdirectories** ([PR #4380](https://github.com/HKUDS/nanobot/pull/4380) & [PR #4393](https://github.com/HKUDS/nanobot/pull/4393)) – Merged. Critical fix—allows `git add/commit/push` in workspace subdirectories by correcting the path guard logic. Includes regression tests.
- **Tool Microcompaction Config** ([PR #4392](https://github.com/HKUDS/nanobot/pull/4392)) – Opened. Adds `microcompactToolResults` setting to disable dynamic compaction for cache-sensitive deployments.
- **Session Replay & Memory** ([PR #4349](https://github.com/HKUDS/nanobot/pull/4349), [PR #4373](https://github.com/HKUDS/nanobot/pull/4373)) – Merged. Preserves delivery context during consolidation and fixes replay-window trimming so LLM replay does not start in the middle of a user turn.

**Bridges & User Interface**
- **WhatsApp Blue Ticks** ([PR #4354](https://github.com/HKUDS/nanobot/pull/4354)) – Merged. Marks incoming messages as read via `readMessages()` immediately after the startup filter.
- **Feishu Card & Streaming Fixes** ([PR #4342](https://github.com/HKUDS/nanobot/pull/4342), [PR #4381](https://github.com/HKUDS/nanobot/pull/4381), [PR #4391](https://github.com/HKUDS/nanobot/pull/4391)) – Two fixes merged for WebSocket card structure and streaming update recovery; one PR opened for QR scan-to-create Feishu login flow.
- **WebUI Activity Display** ([PR #4283](https://github.com/HKUDS/nanobot/pull/4283)) – Merged. Corrects turn duration labels and distinguishes "work" from "thought" activity blocks.
- **MyTool Model Preset** ([PR #4347](https://github.com/HKUDS/nanobot/pull/4347)) – Merged. Explicitly handles `model_preset` in MyTool with clearer success/error output.

---

### 4. Community Hot Topics

The most active issues reveal a strong focus on configuration UX and workspace reliability:

- **[#4374 – Workspace Read/Write Asymmetry](https://github.com/HKUDS/nanobot/issues/4374)** (maximilize)
  > SOUL.md / USER.md bootstrap files are read from the per-turn project workspace but written to the default workspace. This creates a confusing split-brain scenario for full project isolation. The 1 comment signals immediate community awareness of this design flaw introduced in #4007.

- **[#4376 – User-Friendly Wizard](https://github.com/HKUDS/nanobot/issues/4376)** (chengyongru, 1 👍)
  > Explicit call to action from a regular contributor: the current `nanobot onboard --wizard` assumes deep technical knowledge. The author proposes a step-by-step guided UX for new and non-technical users. This is the highest-voted open issue for the day.

- **[#4390 – Multi-Instances for Normies](https://github.com/HKUDS/nanobot/issues/4390)** (bukit-kronik)
  > Freshly filed. The user finds the folder-based multi-instance approach (docs) too technical and requests a UI-driven option to hide complex settings. This closely aligns with the "wizard" request in #4376.

- **[#936 – Multi-Tenant Gateway](https://github.com/HKUDS/nanobot/issues/936)** (weibo021)
  > A long-standing request (Feb 21) for a single gateway managing multiple agents. Recently bumped with a comment on June 17, indicating the community is still eager for this scale-oriented infrastructure feature.

**Underlying Need Analysis:** Today's hot topics clearly signal a shift in the user base. Beyond raw functionality, users are now demanding **operational simplicity** (wizards, multi-instance UIs) and **robust isolation mechanics** (workspace read/write symmetry, multi-tenant gateways).

---

### 5. Bugs & Stability

Severity ranked by user impact:

| Severity | Issue | Description | Status |
|---|---|---|---|
| **High** | [#4375](https://github.com/HKUDS/nanobot/issues/4375) | Git commands (add, commit, push) blocked by workspace guard when `cwd` is a subdirectory. | **Fixed** via [PR #4380](https://github.com/HKUDS/nanobot/pull/4380) |
| **High** | [#4322](https://github.com/HKUDS/nanobot/issues/4322) | `NameError: 'session_key' is not defined` crashes agent at startup after merge. | **Closed** |
| **Medium** | [#4388](https://github.com/HKUDS/nanobot/issues/4388) | **WebUI iOS Safari** — Clicking the input box triggers automatic page zoom and UI deformation on iPhone Air (iOS 26.5). | Open |
| **Medium** | [#4389](https://github.com/HKUDS/nanobot/issues/4389) | **Per-model context window** — `contextWindowTokens` is global. Fallback models with smaller windows are not trimmed, risking silent truncation failures. | Open (Feature Request/Bug) |
| **Medium** | [#4374](https://github.com/HKUDS/nanobot/issues/4374) | **Workspace Read/Write Asymmetry** — Bootstrap files read from project workspace but written to default workspace. | Open |
| **Low** | [#4366/4367](https://github.com/HKUDS/nanobot/pull/4367) | Proxy environment variables silently breaking local model servers. | **Fixed** via [PR #4367](https://github.com/HKUDS/nanobot/pull/4367) |
| **Low** | [#4355/4356](https://github.com/HKUDS/nanobot/pull/4356) | Anthropic API 400 errors on invalid tool IDs from multi-turn sessions. | **Fixed** via [PR #4356](https://github.com/HKUDS/nanobot/pull/4356) |
| **Low** | [#4341/4342](https://github.com/HKUDS/nanobot/pull/4342) | Feishu card content displayed as blank placeholder when arriving via WebSocket. | **Fixed** via [PR #4342](https://github.com/HKUDS/nanobot/pull/4342) |

**Stability Pulse:** Very strong. The highest severity bugs (Git blocking, NameError crash, proxy blocking) were discovered and merged with fixes within the same 24-hour window. The open issues are primarily feature-level regressions or UX problems rather than core runtime crashes.

---

### 6. Feature Requests & Roadmap Signals

**Likely candidates for the next version:**
- **User-Friendly Onboarding** ([#4376](https://github.com/HKUDS/nanobot/issues/4376), [#4390](https://github.com/HKUDS/nanobot/issues/4390)) – The combined pressure for a "wizard" and "multi-instance for normies" is a major roadmap signal. Expect design work or experimental flags for guided configuration in the near term.
- **Per-model Context Window Fallback** ([#4389](https://github.com/HKUDS/nanobot/issues/4389)) – A critical reliability gap that could cause silent cost spikes or failures during model failover. Likely to be fast-tracked after the batch of provider fixes merged today.
- **Multi-Tenant Gateway** ([#936](https://github.com/HKUDS/nanobot/issues/936)) – Recently bumped. This is a heavier infrastructure lift, likely targeted for the 0.3 or 0.4 cycle rather than the immediate next patch.

**Merged features included in the next release:**
- Keenable Search Agent
- Mistral provider support with dedicated API handling
- WhatsApp read receipts (blue ticks)
- Feishu QR code-based bot creation
- Configurable tool microcompaction

---

### 7. User Feedback Summary

**Satisfaction Indicators:**
- High sprint velocity: 17 PRs merged in a single day, with critical bugs resolved within hours.
- Active community contributions from regular contributors (yu-xin-c, chengyongru, franciscomaestre, michaelxer) across workspaces, bridges, and providers.
- The recent Project Workspaces feature ([#4007](https://github.com/HKUDS/nanobot/issues/4007)) is clearly being adopted, evidenced by detailed bug reports on its edge cases ([#4374](https://github.com/HKUDS/nanobot/issues/4374)).

**Dissatisfaction / Pain Points:**
- **Onboarding Complexity** – Multiple issues directly cite the steep learning curve for configuration and multi-instance setup.
- **Workspace Edge Cases** – The security guard correctly prevents out-of-bounds operations but has overly scoped restrictions for legitimate Git workflows within subdirectories.
- **Provider Friction** – Users often hit protocol-level mismatches (proxy semantics, tool ID constraints, Mistral/Anthropic specification strictness). The flurry of provider fixes suggests this is a recurring source of frustration.
- **Mobile WebUI** – The iOS Safari zoom regression on the latest mobile UI indicates a QA gap for mobile rendering.

---

### 8. Backlog Watch

| Issue | Age | Reasoning |
|---|---|---|
| **[#936 – Multi-Tenant Gateway](https://github.com/HKUDS/nanobot/issues/936)** | ~4 months (Feb 21 → Jun 17) | Recently bumped by a comment. This is the oldest active high-impact feature request. Needs a maintainer decision on scope and target version. |
| **[#3437 – Heartbeat Trigger](https://github.com/HKUDS/nanobot/issues/3437)** | ~2 months (Apr 25) | Request for an on-demand heartbeat for debugging `HEARTBEAT.md` configurations. Still unassigned. Could be valuable for the upcoming release debugging cycle. |
| **[#4303 – MCP GC Crash Fix](https://github.com/HKUDS/nanobot/pull/4303)** | ~7 days (Jun 11) | Open PR fixing a `RuntimeError` during `streamableHttp` MCP server session termination. Not yet merged. Moderate risk for users relying on MCP tools. |

Overall, the project is in a strongly healthy state with high merge velocity and responsive maintainers. The primary risk is UX complexity for new users, which the community is loudly signaling needs to be addressed.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for Thursday, June 18, 2026.

---

## 1. Today's Overview

Hermes Agent is experiencing a surge of extremely high activity, with over 100 issues and pull requests updated in the last 24 hours. The project is in a rapid iteration phase, heavily focused on crisis-mode stability fixes and major infrastructure expansion. A critical Anthropic OAuth billing rejection ([#48176](https://github.com/NousResearch/hermes-agent/issues/48176)) has triggered an exceptionally fast maintenance response with companion fix PRs already submitted. While the community is pushing the system hard with sophisticated integrations (OpenTelemetry, LUMEN binary protocol, Linux Computer Use), desktop application stability remains the primary friction point for users, with multiple build and installer regressions reported. Overall, the project is incredibly active but is currently juggling a high volume of P1/P2 bugs alongside bold new feature work.

## 2. Releases

No new releases were cut today. The mainline is in a heavy-patching state.

## 3. Project Progress

**Merged / Closed PRs:**
- **#43051** ([fix(approval): honor glob command allowlist entries](https://github.com/NousResearch/hermes-agent/pull/43051)): A security-focused fix that properly interprets user-defined command allowlist patterns, improving the terminal safety subsystem.
- **#47477** ([WhatsApp Group Sending Guide](https://github.com/NousResearch/hermes-agent/issues/47477)): Community documentation was closed as completed.

**Advanced to Active Review / High-Value Open Work:**
- **Anthropic Provider (Urgent):** PRs [#48177](https://github.com/NousResearch/hermes-agent/pull/48177) and [#48192](https://github.com/NousResearch/hermes-agent/pull/48192) introduce the billing-attribution system block and normalize tool_choice names for OAuth compatibility, attempting to patch the HTTP 400 billing block.
- **Desktop Fixes:** PR [#48188](https://github.com/NousResearch/hermes-agent/pull/48188) scopes the install-method stamp to fix "Desktop app cannot update" errors. PR [#48186](https://github.com/NousResearch/hermes-agent/pull/48186) addresses the WSL clipboard paste issue.
- **Infrastructure:** PR [#48184](https://github.com/NousResearch/hermes-agent/pull/48184) adds a first-class bundled OpenTelemetry (OTLP) observability plugin. PR [#47740](https://github.com/NousResearch/hermes-agent/pull/47740) introduces the LUMEN binary protocol transport for MCP.
- **Platform Parity:** PR [#48180](https://github.com/NousResearch/hermes-agent/pull/48180) adds a native Linux backend for the Computer Use tool.

## 4. Community Hot Topics

The following discussions drew the most engagement today, revealing deep community priorities:

- **[#514 – A2A Protocol Support](https://github.com/NousResearch/hermes-agent/issues/514)** (22 comments, 18 👍)
  The most active thread by a wide margin. The community is heavily advocating for interoperability. Consensus is building that while MCP answers "what tools do you have?", A2A answers "who can help me?". This is the strongest roadmap signal from the user base.
- **[#38602 – Desktop Client-Only Installation](https://github.com/NousResearch/hermes-agent/issues/38602)** (18 👍, 6 comments)
  A recurring high-demand theme. Users want the Hermes Desktop app to serve strictly as a remote client connecting to a headless server, rather than bootstrapping a local runtime. The 18 upvotes suggest this is a major pain point for infrastructure-focused teams.
- **[#47917 – Desktop Build Fails on Update](https://github.com/NousResearch/hermes-agent/issues/47917)** (8 comments)
  A hot regression. The Electron binary cache continues to invalidate during updates, causing total build failures. Users are frustrated by this being the second time this specific pattern has broken (related to #47266).
- **[#27555 – Vision Fallback Chain Broken](https://github.com/NousResearch/hermes-agent/issues/27555)** (7 comments)
  A silent data-loss bug. The community has fully diagnosed the root cause (wrong kwargs in `_resolve_single_provider`) but a fix has not yet merged. The underlying need is for robust, predictable fallback logic in the agent stack.

## 5. Bugs & Stability

**P1 / Critical:**
- **[#48176 – OAuth Billing Rejection](https://github.com/NousResearch/hermes-agent/issues/48176)**: Claude Pro/Max/Team users are completely blocked by HTTP 400 billing errors. Emergency fix PRs [#48177](https://github.com/NousResearch/hermes-agent/pull/48177) and [#48192](https://github.com/NousResearch/hermes-agent/pull/48192) are under review.
- **[#27555 – Vision Fallback Broken](https://github.com/NousResearch/hermes-agent/issues/27555)**: Active since May 17. The `_resolve_single_provider()` function passes `base_url` instead of `explicit_base_url`, causing the entire fallback chain to silently return `None`. This represents a major trust-eroding bug.

**P2 / High:**
- **[#48181 – Memory Tool Security Bypass](https://github.com/NousResearch/hermes-agent/issues/48181)**: Disabled memory toolsets can be re-injected by the provider after the tool-policy filter, creating a security gap.
- **[#47917 / #48084 – Desktop Build & Update Failures](https://github.com/NousResearch/hermes-agent/issues/47917)**: The packaging pipeline remains fragile. Fix PR [#48188](https://github.com/NousResearch/hermes-agent/pull/48188) scopes the issue specifically.
- **[#48150 – Gateway Markdown Strip Corruption](https://github.com/NousResearch/hermes-agent/issues/48150)**: The `strip_markdown` helper in the SMS/iMessage adapters is stripping literal asterisks, breaking bullet lists in plain text gateways.
- **[#32497 – Agent Self-Modification](https://github.com/NousResearch/hermes-agent/issues/32497)**: The agent is rewriting its own skill definitions during unrelated tasks, indicating a critical prompt/guardrail break.

**P3 / Medium:**
- **[#47006 – Custom Endpoint Onboarding Fails](https://github.com/NousResearch/hermes-agent/issues/47006)**: Hard fails on Cohere and other non-standard OpenAI API shapes.
- **[#48161 – Chinese IME Input Broken on Windows](https://github.com/NousResearch/hermes-agent/issues/48161)**: `patch_stdout` in the TUI is interfering with IME composition, causing a poor experience for international users.
- **[#40692 – macOS Composer Lag](https://github.com/NousResearch/hermes-agent/issues/40692)**: Typing becomes progressively laggy with long conversation histories, making extended sessions difficult.

## 6. Feature Requests & Roadmap Signals

**High Likelihood for Next Release (Based on activity and PR maturity):**

- **Anthropic OAuth Overhaul**: The P1 nature of the billing fix means PRs [#48177](https://github.com/NousResearch/hermes-agent/pull/48177) and [#48192](https://github.com/NousResearch/hermes-agent/pull/48192) are likely to be fast-tracked into a hotfix release.
- **OpenTelemetry Observability**: PR [#48184](https://github.com/NousResearch/hermes-agent/pull/48184) is a major infrastructure upgrade that signals enterprise readiness. Likely a headline feature for the next minor release.
- **Linux Computer Use**: PR [#48180](https://github.com/NousResearch/hermes-agent/pull/48180) addresses a core platform gap.
- **Desktop UX Polish**: System Tray support ([#48163](https://github.com/NousResearch/hermes-agent/pull/48163)) and Kanban view ([#48159](https://github.com/NousResearch/hermes-agent/issues/48159)) suggest the team is prioritizing GUI maturity.

**Longer-Term Signals:**
- **A2A Protocol ([#514](https://github.com/NousResearch/hermes-agent/issues/514))**: Community demand is overwhelming.
- **Desktop Thin Client ([#38602](https://github.com/NousResearch/hermes-agent/issues/38602))**: Containerized/remote deployments are a clear user requirement.
- **Session Context Enforcement ([#48190](https://github.com/NousResearch/hermes-agent/issues/48190), [#13072](https://github.com/NousResearch/hermes-agent/issues/13072))**: Users are pushing for workspace-aware sessions and CLI auto-queue modes for heavy automation.

## 7. User Feedback Summary

**Pain Points / Dissatisfaction:**
- **Installing and Updating is Brittle**: The Windows installer fails at the "desktop" stage ([#46260](https://github.com/NousResearch/hermes-agent/issues/46260)) and the update pipeline breaks when the Electron cache is invalidated ([#47917](https://github.com/NousResearch/hermes-agent/issues/47917)). The update/packaging pipeline is the #1 source of user friction.
- **Silent Failures**: The vision fallback bug ([#27555](https://github.com/NousResearch/hermes-agent/issues/27555)) and the Markdown stripping ([#48150](https://github.com/NousResearch/hermes-agent/issues/48150)) erode user confidence because they fail without warnings or error logs.
- **Agent Behavior**: Users are startled by the skill self-modification bug ([#32497](https://github.com/NousResearch/hermes-agent/issues/32497)), which violates the core assumption of "the agent assists, it doesn't reconfigure me."
- **Configuration Friction**: The hard fail on custom OpenAI-compatible endpoints ([#47006](https://github.com/NousResearch/hermes-agent/issues/47006)) blocks advanced users operating cloud SaaS setups.

**Satisfaction / Successes:**
- **Rapid Response to Critical Bugs**: The community noted the exceptionally fast turnaround (single day) between the Anthropic OAuth bug report ([#48176](https://github.com/NousResearch/hermes-agent/issues/48176)) and the submission of fix PRs.
- **Strong External Developer Base**: High-quality contributions (OTLP plugin [#48184](https://github.com/NousResearch/hermes-agent/pull/48184), LUMEN binary protocol [#47740](https://github.com/NousResearch/hermes-agent/pull/47740), and new skills [#47576](https://github.com/NousResearch/hermes-agent/pull/47576)) demonstrate strong ecosystem health.
- **Power-User Adoption**: The depth of requests (multi-channel personas, per-subagent model overrides) shows that sophisticated users are betting heavily on the platform.

## 8. Backlog Watch

The following items have been open for an extended time with significant community interest but lack explicit maintainer action:

- **[#514 – A2A Protocol Support](https://github.com/NousResearch/hermes-agent/issues/514)**
  Open since March 6. This is the most reacted-to and commented-on thread in the dataset. The community is likely waiting for roadmap commitment.
- **[#8359 – Docs/Specs Out of Sync](https://github.com/NousResearch/hermes-agent/issues/8359)**
  Open since April 12. An automated audit flagged discrepancies between documented behavior and implementation for ACP, pricing, and container CLI. This debt can cause widespread misconfiguration.
- **[#13072 – CLI Auto-Queue Mode](https://github.com/NousResearch/hermes-agent/issues/13072)**
  Open since April 20. Contains a detailed user spec for smart interrupt and crash recovery. Awaiting a maintainer to champion or provide feedback.
- **[#20203 – OpenAI Verbosity Config](https://github.com/NousResearch/hermes-agent/issues/20203)**
  Open since May 5. A small, non-invasive feature request (control verbosity of OpenAI Responses API) that would be a quick win for user satisfaction.
- **[#27208 – Plugin Hook for Interrupted Agent Loops](https://github.com/NousResearch/hermes-agent/pull/27208)**
  Open since May 17. This PR has a clean implementation but has been sitting idle. It would enable plugins to clean up external resources on interrupt.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**Project Digest for 2026-06-18 | PicoClaw (sipeed/picoclaw)**

**1. Today's Overview**
On June 18th, the PicoClaw project exhibited strong, balanced activity with 10 pull requests updated (4 open, 6 merged/closed) and 4 issues updated (2 open, 2 closed). The day was dominated by security hardening and model compatibility fixes, notably the prompt closure of a critical SSRF vulnerability in the OneBot channel and a blocking issue with Gemini 3.5 Flash. While no new releases were tagged, the high close rate and rapid iteration across providers, tooling, and the web UI indicate a healthy sprint cycle focused on both stability and feature expansion. Overall project velocity is moderate-to-high, driven by responsive maintainership and active community contributions.

**2. Releases**
No new releases were published today. The project currently has no tagged release in the observed window.

**3. Project Progress**
Six pull requests were merged or closed today, representing significant progress in hardening and expanding the platform:

- **Security Fix (Critical):** [PR #3140](https://github.com/sipeed/picoclaw/pull/3140) (fix/onebot) blocked private address fetches in inbound media URLs, resolving the SSRF advisory in [Issue #3070](https://github.com/sipeed/picoclaw/issues/3070).
- **Gemini 3.5 Flash Compatibility:** [PR #3136](https://github.com/sipeed/picoclaw/pull/3136) was merged, adding support for both `camelCase` and `snake_case` `thought_signature` fields to resolve the tool execution failure reported in [Issue #3111](https://github.com/sipeed/picoclaw/issues/3111).
- **Provider Expansion:** [PR #2917](https://github.com/sipeed/picoclaw/pull/2917) was merged, integrating NEAR AI Cloud as a new first-class OpenAI-compatible provider with TEE-capable model suggestions.
- **Web Tooling Fixes:** [PR #3139](https://github.com/sipeed/picoclaw/pull/3139) patched the Sogou web search parser to match recent HTML structural changes. [PR #2990](https://github.com/sipeed/picoclaw/pull/2990) fixed the Web UI to display full session history instead of only the last user message.
- **Feature Implementation:** [PR #3138](https://github.com/sipeed/picoclaw/pull/3138) was merged, implementing a new "Review" feature, likely targeting the Web UI or plugin review pipeline.

**4. Community Hot Topics**
- **Cryptography Upgrade Push:** [Issue #3088](https://github.com/sipeed/picoclaw/issues/3088) ("use vodozemac instead of libolm") remains the most active open issue, labeled `help wanted` and `priority: high` with 2 👍 reactions. The community is clearly driving an urgent migration away from the unmaintained `libolm` library.
- **Protocol Diversification Demand:** Open [PR #3063](https://github.com/sipeed/picoclaw/pull/3063) (DeltaChat gateway) and stale [Issue #3093](https://github.com/sipeed/picoclaw/issues/3093) (requesting SimpleX/Tox) reflect a strong and persistent community desire for decentralized, privacy-preserving messaging backends beyond standard bridges.
- **Sub-Agent Reliability:** Open [PR #3142](https://github.com/sipeed/picoclaw/pull/3142) and [PR #3141](https://github.com/sipeed/picoclaw/pull/3141), addressing duplicate messages in async sub-agent turns and silent Brave search failures respectively, demonstrate active community contributions targeting core agent execution robustness.

**5. Bugs & Stability**
- **Critical (Resolved):** [Issue #3070](https://github.com/sipeed/picoclaw/issues/3070) disclosed an SSRF vulnerability where an attacker-controlled media URL in the OneBot channel could force the host to fetch internal network resources. Immediately fixed by [PR #3140](https://github.com/sipeed/picoclaw/pull/3140).
- **High (Resolved):** [Issue #3111](https://github.com/sipeed/picoclaw/issues/3111) reported a `400 Bad Request` when using the Gemini 3.5 Flash model for tool execution. The root cause was a missing `thought_signature` field in the API schema. Fixed by [PR #3136](https://github.com/sipeed/picoclaw/pull/3136).
- **Medium (Open):** [PR #3142](https://github.com/sipeed/picoclaw/pull/3142) fixes a logic error in spawn sub-agent completion where identical content in the `ForUser` and `ForLLM` fields triggered duplicate message delivery. Awaiting review.
- **Low (Open):** [PR #3141](https://github.com/sipeed/picoclaw/pull/3141) adds diagnostic logging for Brave API returning HTTP 200 with zero results. [PR #3092](https://github.com/sipeed/picoclaw/pull/3092) improves type assertion safety in skills installation to prevent silent failures.

**6. Feature Requests & Roadmap Signals**
The clearest roadmap signal is the high-priority push to replace `libolm` with `vodozemac` ([Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)), a foundational security upgrade likely bound for the next minor or major release. The completed merge of NEAR AI Cloud ([PR #2917](https://github.com/sipeed/picoclaw/pull/2917)) confirms the maintainers' commitment to expanding AI provider diversity. Looking forward, the pending *DeltaChat* gateway ([PR #3063](https://github.com/sipeed/picoclaw/pull/3063)) and the sustained calls for SimpleX/Tox support ([Issue #3093](https://github.com/sipeed/picoclaw/issues/3093)) suggest that supporting alternative, decentralized chat networks is the most heavily anticipated product direction on the current roadmap.

**7. User Feedback Summary**
- **Pain Points:** Users are actively expressing friction with legacy dependency security (`libolm`), model API breakage (Gemini 3.5 Flash), and silent tool execution failures (Brave search, Sogou parsing). There is clear demand for networking diversity beyond mainstream protocols.
- **Satisfaction:** The extremely rapid closure of the SSRF advisory (advisory filed June 9, blocked June 17) and the Gemini compatibility break (filed June 12, fixed June 17) demonstrates a highly responsive maintainer team, which is a strong positive signal for user trust in the project's security posture and support velocity.

**8. Backlog Watch**
- **[PR #3063](https://github.com/sipeed/picoclaw/pull/3063) (DeltaChat Gateway):** Open for 10 days and flagged as stale. This represents a major feature addition that the community has explicitly requested. Lack of maintainer direction risks either a missed merge opportunity or a long-lived fork.
- **[Issue #3093](https://github.com/sipeed/picoclaw/issues/3093) (SimpleX/Tox Support):** Stale with no maintainer response. As interest in privacy-focused protocols grows, a formal triage label (e.g., "help wanted" or "not planned") would help manage community expectations and potential contributor allocation.
- **[PR #3092](https://github.com/sipeed/picoclaw/pull/3092) (Skills Install Type Assertions):** Stale for 8 days. A small, clean defensive coding fix that is low risk to merge. Accumulation of such easy-to-review PRs can generate unproductive backlog friction.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the structured project digest for NanoClaw on 2026-06-18.

---

# NanoClaw Project Digest — 2026-06-18

## 1. Today's Overview
NanoClaw experienced a surge of high-velocity activity on June 18, with **20 pull requests** and **5 issues** updated, alongside the tagging of **v2.1.17**. The day was dominated by the rapid patching of a critical delivery-stalling bug, several high-priority security hardening measures, and a wave of documentation cleanup driven by engaged community contributors (notably `sturdy4days` and `specterslient95-lgtm`). Release v2.1.17 rolled up a series of patches, introduced a breaking change to the OneCLI SDK dependency, and added an emergency environment-variable escape hatch for the startup upgrade tripwire that had been blocking managed fleet deployments. Overall project health is robust, with core-team responsiveness to critical regressions, though several severe unfixed bugs remain in the open PR queue.

📊 **Activity Score:** Very High (20 PRs, 5 Issues, 2 Releases).
👥 **Key Contributors:** `sturdy4days` (4 fixes), `specterslient95-lgtm` (4 docs fixes), `gabi-simons` (2 fleet patches), `arkjun` (translation), `moshe-nanoco` (feature work).

---

## 2. Releases
Two releases are detailed in the current data. Both contain breaking changes that require operator attention.

### v2.1.17 (New)
**Rollup covering v2.1.1 through v2.1.17.**

- **⚠️ [BREAKING] OneCLI SDK Update:** The `@onecli-sh/sdk` dependency jumped from `0.5.0` to `2.2.1`. This requires the OneCLI server to expose the **`/v1` API**. Older servers will return `404` errors for *every* SDK call. The sanctioned gateway and CLI versions are now explicitly pinned.
- **Feature – Managed Fleet Opt-Out:** Added the `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` environment variable (PR [#2780](https://github.com/nanocoai/nanoclaw/issues/2780)). This allows immutable/baked-image deployments to bypass the v2.1.0 upgrade marker check.
- **Fix – Delivery Stability:** Resolved a critical bug ([#2796](https://github.com/nanocoai/nanoclaw/issues/2796)) where a single unhealthy session could stall message delivery for **all** agents until daemon restart.
- **Refactor – Dead Code Removal:** `resolveGroupIpcPath` removed as IPC was fully excised in the v2 architecture.

### v2.1.0 (Prior)
**Rollup covering v2.0.65 through v2.1.0.**

- **⚠️ [BREAKING] Upgrade Marker Required:** The host process now refuses to boot unless `data/upgrade-state.json` records a valid upgrade path to the current version. This was the change that broke managed fleets (subsequently mitigated in v2.1.17).

---

## 3. Project Progress (Merged/Closed PRs)
Three pull requests were fully merged or closed today, representing a strong focus on reliability and operational flexibility:

- **🔒 [Fixed] Agent Delivery Deadlock:** PR [#2797](https://github.com/nanocoai/nanoclaw/issues/2797) (mashkovtsevlx) was merged. It addresses a catastrophic fault-isolation hole by wrapping each session iteration in an isolated `try/catch` rather than a single loop, preventing a single corrupt session from taking down the entire agent swarm.
- **🔒 [Fixed] Managed Fleet Auth Regression:** PR [#2794](https://github.com/nanocoai/nanoclaw/issues/2794) (gabi-simons) was merged. It restores `env-var` gateway authentication for managed-fleet agents (baked into immutable VM images).
- **🚀 [Shipped] Upgrade Tripwire Env Var:** PR [#2780](https://github.com/nanocoai/nanoclaw/issues/2780) (gabi-simons) was merged and is included in v2.1.17.
- **📚 [Docs] Setup Guide Expansion:** PR [#2790](https://github.com/nanocoai/nanoclaw/issues/2790) was merged, replacing a 600-byte stub with a real phase-by-phase setup guide with recovery steps.

---

## 4. Community Hot Topics
- **🌐 Internationalization:** PR [#2806](https://github.com/nanocoai/nanoclaw/issues/2806) (arkjun) adds a complete Korean README translation, following the existing Japanese/Chinese patterns. This signals strong community demand for dedicated i18n support beyond just the English core.
- **🔌 Ecosystem Expansion:** PR [#2717](https://github.com/nanocoai/nanoclaw/issues/2717) (lucaszhu-hue) has been open since June 9 but remains highly relevant as a community-driven addition of Atlas Cloud as an LLM backend option.
- **📝 Doc Quality Assurance:** Issues [#2791](https://github.com/nanocoai/nanoclaw/issues/2791), [#2789](https://github.com/nanocoai/nanoclaw/issues/2789), [#2787](https://github.com/nanocoai/nanoclaw/issues/2787), [#2785](https://github.com/nanocoai/nanoclaw/issues/2785) (all by `specterslient95-lgtm`) highlight that power users are actively debugging official skill documentation—finding missing `mkdir` commands, generic titles, and undeclared ports—and providing their own fixes. This reflects a user base that values high-quality, concrete guides over scripts.
- **🛠️ Community Utility Skills:** PR [#2795](https://github.com/nanocoai/nanoclaw/issues/2795) (leetwito) contributes a CLI-derived dashboard skill (`/add-clidash`), showing organic ecosystem growth.

---

## 5. Bugs & Stability
Bugs are ranked by severity. Fix PR status is noted.

| Severity | Issue / Bug | Status | Details |
|---|---|---|---|
| **🔴 CRITICAL** | **Agent-to-Agent Delivery Deadlock**<br>([#2796](https://github.com/nanocoai/nanoclaw/issues/2796)) | **FIXED** (PR [#2797](https://github.com/nanocoai/nanoclaw/issues/2797) merged) | A single session with a jammed `outbound.db` threw an unhandled error, aborting the delivery loop for *all* agents. Total service degradation. Resolved in v2.1.17. |
| **🔴 CRITICAL** | **CLI `ncl messaging-groups create` Broken**<br>([#2804](https://github.com/nanocoai/nanoclaw/issues/2804)) | Fix PR Open (no review) | Every invocation throws `NOT NULL constraint failed: messaging_groups.instance`. The CLI path is completely dead for this resource. |
| **🟠 HIGH** | **Security: `send_file` Path Traversal (CVE-2026-29611)**<br>([#2799](https://github.com/nanocoai/nanoclaw/issues/2799)) | Fix PR Open | `send_file` accepts absolute `path` with no canonicalization. A compromised agent can read any container file. |
| **🟠 HIGH** | **Security: CLI `group create --folder` Traversal (CWE-22)**<br>([#2800](https://github.com/nanocoai/nanoclaw/issues/2800)) | Fix PR Open | `folder` parameter bypasses the `assertValidGroupFolder` validator, allowing `../../etc` injection. |
| **🟠 HIGH** | **CLI Socket Client No Timeout / Memory Bomb**<br>([#2802](https://github.com/nanocoai/nanoclaw/issues/2802)) | Fix PR Open | `SocketTransport.sendFrame` has no request timeout and no response buffer size limit. A slow host can hold the promise forever; a streaming host can grow the buffer unbounded. |
| **🟡 MEDIUM** | **Message Parsing Failure on Primitives**<br>([#2801](https://github.com/nanocoai/nanoclaw/issues/2801)) | Fix PR Open | `safeParseContent` passes raw `JSON.parse` results to callers expecting objects. Payloads like `"5"` or `"true"` get `undefined` fields instead of raw-text fallback. |
| **🟡 MEDIUM** | **Stale `outbound.db` Journals After Container Kill**<br>([#2750](https://github.com/nanocoai/nanoclaw/issues/2750)) | Fix PR Open (since June 12) | Host's READONLY handles to `outbound.db` get stuck on stale WAL journals after a container SIGKILL. Fixes #2516 and #2640. |
| **🟢 LOW** | **Setup Token Parsing from PTY**<br>([#2805](https://github.com/nanocoai/nanoclaw/issues/2805)) | Fix PR Open | OAuth token fails to parse when captured through a PTY that wraps long lines. |

---

## 6. Feature Requests & Roadmap Signals
- **🚦 Agent Governance (Next Major Feature):** PR [#2793](https://github.com/nanocoai/nanoclaw/issues/2793) (`moshe-nanoco`) introduces an **optional, directed, per-message approval gate** for agent-to-agent connections. Given the core-team authorship and the "fully backward compatible" design, this is likely to land in the next minor release (v2.2.0). This is a significant enterprise/governance play.
- **📦 Immutable Deployment Support:** The rapid response to managed fleet breaking changes (PRs [#2780](https://github.com/nanocoai/nanoclaw/issues/2780) & [#2794](https://github.com/nanocoai/nanoclaw/issues/2794)) signals a clear roadmap priority: NanoClaw is being hardened for containerized/CI/CD workflows where filesystem upgrade markers are impractical.
- **🌍 Internationalization (i18n):** The gap between the Korean README contribution and the existing Japanese/Chinese ones suggests a growing community need for a formal i18n framework rather than duplicating README files.
- **🔌 LLM Backend Spectrum:** PR [#2717](https://github.com/nanocoai/nanoclaw/issues/2717) (Atlas Cloud) implies a continued commitment to the OpenAI-compatible API standard, likely seeking to decouple from a single provider.

---

## 7. User Feedback Summary
- **😠 Pain Point – Brittle Dependency Upgrades:** The breaking change in v2.1.17 (OneCLI SDK bump requiring the `/v1` API) creates a hard coordination burden. Users who update NanoClaw without simultaneously updating their OneCLI server will face complete SDK failure (`404`s). This is a dangerous upgrade footgun.
- **😠 Pain Point – Doc Gaps are Real:** Multiple issues from a single power user (#2791, #2789, #2787, #2785) systematically document that the "10-line skill" paradigm is insufficient. Setup, migration, and channel skills need concrete steps, not vague pointers to scripts.
- **😟 Pain Point – Reliability Fears:** Issue #2796 likely caused significant user anxiety. While the fix (PR #2797) was exceptionally fast (created and merged on the same day), the fact that a *single session* could silently block all agent communication highlights a fundamental lack of fault isolation in the core loop.
- **😊 Satisfaction – Responsive Core Team:** The same-day turn around on issue #2796 (create, fix, merge) is a strong positive signal that the core team prioritizes stability and is engaged.
- **😊 Satisfaction – Community Agency:** Users are not just filing bugs; they are writing the missing documentation (specterslient95-lgtm), adding translations (arkjun), and building utility skills (leetwito). This indicates high ownership and a healthy onboarding experience for contributors.

---

## 8. Backlog Watch
- **📌 [STALLED – Ecosystem PR] Atlas Cloud Docs:** PR [#2717](https://github.com/nanocoai/nanoclaw/issues/2717) (lucaszhu-hue) has been open since June 9 with zero maintainer interaction. As a low-risk documentation-only change, this bottleneck is concerning and may discourage future ecosystem contributions.
- **📌 [HIGH RISK – Stability] Stale `outbound.db` Journals:** PR [#2750](https://github.com/nanocoai/nanoclaw/issues/2750) has been open since June 12 (6 days) and fixes a nasty persistence failure (#2516, #2640) that plagues users relying on container orchestration. The lack of review here creates an ongoing silent reliability threat for CMS/container-based users.
- **📌 [HIGH RISK – Security] Unreviewed CVEs:** PRs [#2799](https://github.com/nanocoai/nanoclaw/issues/2799) (CVE-2026-29611) and [#2800](https://github.com/nanocoai/nanoclaw/issues/2800) (CWE-22) are explicitly tagged with security identifiers and provide concrete attack vectors, yet neither has received a single maintainer comment or review stamp. This is the most urgent open item in the backlog.
- **📌 [BROKEN CLI] `messaging-groups create`:** PR [#2804](https://github.com/nanocoai/nanoclaw/issues/2804) fixes a completely dead CLI command. The lack of review leaves users entirely unable to use the `ncl messaging-groups` workflow.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — June 18, 2026

**Data Source:** `github.com/nullclaw/nullclaw`

---

## 1. Today's Overview
Through June 18th, NullClaw shows a stable development cadence with no new release today but two meaningful pull requests advancing core functionality and usability. Community engagement remains steady, with three ongoing issues receiving updates, although none were closed. The project is clearly responding to long-standing user pain points, particularly around the terminal interface and memory configuration, signaling incremental but focused improvement.

---

## 2. Releases
**None.** No new releases were cut today.

---

## 3. Project Progress
No pull requests were merged or closed today, but two open PRs represent active development:

- **[PR #961](https://github.com/nullclaw/nullclaw/pull/961)** (feat/memory) — Submitted by **valonmulolli**. Introduces three new config keys (`auto_recall`, `recall_limit`, `max_context_bytes`) to give users control over memory enrichment behavior. This addresses a growing need for context window optimization.
- **[PR #960](https://github.com/nullclaw/nullclaw/pull/960)** (fix/cli) — Submitted by **vernonstinebaker**. Adds a POSIX raw-mode line editor to the `nullclaw agent` REPL, fixing arrow key handling, history navigation, and cursor movement.

---

## 4. Community Hot Topics

- **[Issue #915 — Scheduler Unauthorized](https://github.com/nullclaw/nullclaw/issues/915) (2 comments)**
  User *scabros* reports that the scheduler fails with an authorization error despite the LLM and general tool calling working fine on an Ubuntu setup with external Ollama (Qwen3, RTX 3090). This is the most technically impactful open issue and highlights a critical gap in the scheduler's authentication flow. No fix PR currently exists.

- **[Issue #865 — CLI Control Characters](https://github.com/nullclaw/nullclaw/issues/865) & [PR #960](https://github.com/nullclaw/nullclaw/pull/960) (2 comments)**
  User *eabase* reports that arrow keys, Home/End, and word jumps print escape sequences instead of navigating the buffer. The community responded rapidly with PR #960, which implements a proper line editor. This issue/PR pair is the clearest example of community-driven debugging in this cycle.

- **[Issue #861 — Web UI on Headless VPS](https://github.com/nullclaw/nullclaw/issues/861) (1 comment)**
  User *eabase* directly requests plain-language documentation for deploying the Web UI on a headless VPS, describing the existing README as 70% incomprehensible. This reveals a significant documentation barrier for server-side users.

- **[PR #961 — Memory Configuration](https://github.com/nullclaw/nullclaw/pull/961)**
  Although brand new with no comments yet, this PR touches on deep user demand for controlling context usage and performance tuning, making it a likely focus of upcoming discussion.

---

## 5. Bugs & Stability
No new bugs were filed in the last 24 hours, but two existing bugs remain active:

| Issue | Severity | Description | Mitigation Status |
|---|---|---|---|
| [#915](https://github.com/nullclaw/nullclaw/issues/915) | **High** | Scheduler fails with unauthorized error for external Ollama hosts. Core functionality impacted. | No fix PR yet. Needs maintainer triage. |
| [#865](https://github.com/nullclaw/nullclaw/issues/865) | **Medium** | CLI prints escape sequences instead of handling navigation keys. Severe UX degradation. | Fix PR #960 submitted and awaiting review. |

**Assessment:** The CLI bug has a community fix in progress, which is encouraging. The scheduler bug remains unaddressed and represents the highest risk to production users.

---

## 6. Feature Requests & Roadmap Signals

- **[PR #961](https://github.com/nullclaw/nullclaw/pull/961) (Memory Config)** is the strongest roadmap signal in this digest. The addition of `auto_recall`, `recall_limit`, and `max_context_bytes` suggests the project is prioritizing user-level control over context management and performance tuning. Expect this to land in the next minor release.

- **[Issue #861](https://github.com/nullclaw/nullclaw/issues/861) (Headless VPS / Web UI)** points to an unmet need for simplified headless deployment. While not a formal feature, it strongly signals that users want first-class server-mode documentation, which may precede a "headless mode" implementation or script improvements.

**Prediction for next release:** Memory configuration knobs (from #961), likely combined with a refined CLI experience (from #960).

---

## 7. User Feedback Summary

- **Pain Points:**
  - Scheduler reliability and authentication (*scabros*, Issue #915)
  - Terminal UI unusability out of the box (*eabase*, Issue #865)
  - Configuration documentation for non-expert users (*eabase*, Issue #861)

- **Use Cases Observed:**
  - Local external model hosting (Ollama on separate machine, RTX 3090)
  - Headless VPS deployment
  - Interactive CLI usage for agent sessions

- **Satisfaction / Dissatisfaction:**
  Sentiment is **mixed**. Users are sophisticated enough to diagnose issues (auth flows, terminal raw mode) but are clearly frustrated by core functionality blockers. The quick community fix for the CLI bug (#960) demonstrates collaborative resilience, but the lack of maintainer response on the scheduler (#915) and documentation request (#861) is a pent-up risk.

---

## 8. Backlog Watch

| Item | Age | Priority | Status |
|---|---|---|---|
| [#915 — Scheduler Unauthorized](https://github.com/nullclaw/nullclaw/issues/915) | ~1 month | **High** | No maintainer comment or fix PR. Critical production blocker. |
| [#861 — Web UI setup help](https://github.com/nullclaw/nullclaw/issues/861) | ~2 months | **Medium** | Documentation gap leaving users stuck. No maintainer response. |
| [#865 — CLI control characters](https://github.com/nullclaw/nullclaw/issues/865) | ~2 months | **Medium** | Mitigated by community PR #960, but issue has no official label or status update from maintainers. |

**Watchlist Summary:** Issue #915 is the most concerning backlog item due to its severity and lack of activity. Issue #861 represents an easy documentation win that would improve first-run experience substantially.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is your IronClaw project digest based on the latest GitHub activity.

---

## IronClaw Project Digest — 2026-06-18

### 1. Today's Overview

IronClaw remains in an intense development cycle, with **47 issues** and **50 pull requests** updated in the last 24 hours. The project is deeply focused on the **Reborn engine**, where rigorous internal dogfooding is driving a high volume of bugs and UX polish items. No new releases were cut today. While a massive **Projects** feature stack (`#5015–#5019`) progresses through review, the majority of activity surrounds stabilization—particularly improving the automation dashboard, tool approval flows, and agent loop reliability. The CI pipeline remains partially blocked by a `cargo-deny` advisory issue.

---

### 2. Releases

**No new releases** were published on 2026-06-18. The last release activity was associated with the closed release chore PR `#3708`.

---

### 3. Project Progress

Several key pull requests were merged today, marking forward progress on core Reborn infrastructure:

- **Slack OAuth Security Hardening** ([PR #5052](https://github.com/nearai/ironclaw/pull/5052)) — Merged. Closes `#5009`. Brings the live Slack OAuth path to structural DM parity, closing a security gap in auth flow handling.
- **No-Progress Detection (PR2 + PR3)** — Merged. `#5000` added inert `ContentDigest` plumbing for output-aware progress tracking, while `#5022` activates the detection logic, significantly improving agent loop reliability against stalled turns.
- **NEAR AI tool-message flattening removed** ([PR #4983](https://github.com/nearai/ironclaw/issues/4983)) — Closed. Eliminates a legacy compatibility path that was rewriting OpenAI multi-turn tool messages.

**Open but active:** The massive **Projects feature stack** (`#5015`–`#5019`, authored by `ilblackdragon`) remains open under review, representing a first-class Project entity for the Reborn runtime. A new contributor PR (`#5061`) proposing **skill extraction & self-evolution** is also active.

---

### 4. Community Hot Topics

- **Skill Extraction & Self-Evolution** ([PR #5061](https://github.com/nearai/ironclaw/pull/5061)) — *New contributor / size: XL.* Proposes Hermes-style background skill generation. This is the most architecturally significant new feature raised today and has drawn attention for its autonomous learning capabilities.
- **AWS Bedrock Blocked** ([#5058](https://github.com/nearai/ironclaw/issues/5058)) — High demand for cloud-agnostic model support. The `ironclaw-reborn` binary fails to expose the `bedrock` feature, and the Converse tool schema rejects top-level combinators. Fix proposed in `#5059`.
- **Improve Engineering Productivity** ([#4878](https://github.com/nearai/ironclaw/issues/4878)) — The team's meta-project to use IronClaw to build IronClaw. Shows strong dogfooding culture and signals that task/service automation is a core roadmap priority.
- **WeChat Channel Port** ([#3582](https://github.com/nearai/ironclaw/issues/3582)) — Open. Porting WeChat from v1 WASM to the Reborn ProductAdapter. Indicates continued investment in Chinese market channel parity.

---

### 5. Bugs & Stability

**Critical / Blocker:**

- **CI blocked repo-wide** ([#4824](https://github.com/nearai/ironclaw/issues/4824)) — `cargo-deny` fails on `main` and every open PR due to new RUSTSEC advisories against postgres crates (SCRAM DoS, hstore panic, DataRow panic). Blocking all CI for six days.
- **NEARAI_MODEL=auto rejected** ([#5044](https://github.com/nearai/ironclaw/issues/5044)) — Desktop sidecar sends `auto` to `cloud-api.near.ai`, which returns HTTP 400. Fix proposed in `#5045` (resolve to `z-ai/glm-5.2`).
- **GitHub analysis approval loops** ([#5060](https://github.com/nearai/ironclaw/issues/5060)) — New report. Automations requiring `builtin.http` or similar can enter repeated approval dialogs and never produce results.

**High:**

- **Agent fails to recover from repeated tool errors** ([#4761](https://github.com/nearai/ironclaw/issues/4761)) — Agent stops instead of recovering after tool failures. Open for one week with no committed fix yet.
- **AWS Bedrock entirely blocked** ([#5058](https://github.com/nearai/ironclaw/issues/5058)) — Feature flag missing in `ironclaw-reborn` binary. Fix ready in `#5059`.

**Medium / UX:**

- **`tool_install` shows phantom success** ([#3729](https://github.com/nearai/ironclaw/issues/3729)) — Denied/denied tool install calls show green checkmarks after page refresh. Open since May 17.
- **Validation errors persist on correct input** ([#5007](https://github.com/nearai/ironclaw/issues/5007)) — Skills creation UI fails to clear validation messages after required fields are filled.
- **Delete feedback missing** ([#4823](https://github.com/nearai/ironclaw/issues/4823)) — Deleting a running conversation silently fails; no UI feedback given.

---

### 6. Feature Requests & Roadmap Signals

- **Projects Feature** (`#5015`–`#5019`) — First-class collaborative workspace entity for Reborn. Under heavy review; likely the next major landing feature.
- **Skill Extraction & Self-Evolution** (`#5061`) — Autonomous background learning from successful transcripts. A strong candidate for roadmap inclusion if the review is positive.
- **Scalable Agent Task Service** (`#5036`) — Infrastructure for running automated engineering tasks (code review, CI triage, merge conflict resolution). Tracks parent meta-issue `#4878`.
- **AWS Bedrock Support** (`#5058`) — Feature request with immediate fix PR (`#5059`). Likely to ship in the next release cycle.
- **WeChat Reborn Port** (`#3582`) — Still open. Signals continued investment in multi-channel parity.

---

### 7. User Feedback Summary

User sentiment reflects a product in **rapid iteration mode** with strong internal engagement:

- **Dissatisfaction / Pain Points:**
    - Automation dashboards lack actionable information (`#5004`, `#4988`).
    - Tool approval flows are fragile—deadlocks, silent failures, and persistent denied states (`#4764`, `#4986`, `#4977`).
    - Onboarding friction: first-run attempts to access Extensions or Automations redirect to the welcome page (`#4793`).
    - Model configuration is brittle: `NEARAI_MODEL=auto` causes hard failures with no fallback (`#5044`).
- **Satisfaction / Positive Signals:**
    - **47 issues filed in 24 hours** indicates high engagement and rigorous QA dogfooding (`#4879`).
    - Rapid bug fix turnaround (e.g., Slack OAuth security fix merged same day as report).
    - The community is actively contributing advanced features (skill extraction via `#5061`).

---

### 8. Backlog Watch

These items require maintainer attention due to age, severity, or blocking nature:

- **#4824** — **CI Blocker** (Created Jun 12, 6 days old) — `cargo-deny` RUSTSEC failures blocking `main` and all PRs. No patch or mitigation committed.
- **#4761** — **Agent Recovery Regression** (Created Jun 11, 7 days old) — Reborn agent fails to recover from repeated tool call failures. Core reliability concern with no merge-ready fix.
- **#3729** — **State Phantom Bug** (Created May 17, 1 month old) — Failed `tool_install` calls shown as successful after page refresh. Long-standing trust issue in UI state management.
- **#3582** — **WeChat Channel Port** (Created May 13) — Porting guide exists, but implementation has stalled without recent PR activity.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI Project Digest — 2026-06-18

### 1. Today’s Overview
The LobsterAI project saw a substantial spike in feature polish and stability efforts, with **11 pull requests merged** and a **new feature-rich release (v2026.6.15)** in the past 24 hours. Merge activity overwhelmingly targeted the **Cowork** module, fixing streaming UI bugs, race conditions, and model selection issues. The team also addressed a critical infrastructure bottleneck by raising heap limits in the OpenClaw gateway to prevent OOM crashes. However, the project’s day is dominated by the filing of a **critical security vulnerability** ([Issue #2176](https://github.com/netease-youdao/LobsterAI/issues/2176)) detailing an arbitrary local file read through the automatic artifact loading mechanism, which now demands immediate attention.

### 2. Releases
- **Version:** [LobsterAI 2026.6.15](https://github.com/netease-youdao/LobsterAI/releases/tag/v2026.6.15) *(Released: 2026-06-15)*
- **Key Changes:**
    - **Computer Use** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)): Landmark feature enabling AI-driven desktop automation.
    - **Realtime ASR Voice Input** ([PR #2148](https://github.com/netease-youdao/LobsterAI/pull/2148)): Real-time automatic speech recognition for the Cowork environment.
    - **Post-Compaction Context Continuity** ([PR #2145](https://github.com/netease-youdao/LobsterAI/pull/2145)): Improved agent reliability when OpenClaw compresses chat history.
- **Migration Notes:** No breaking changes were reported for this release.

### 3. Project Progress
The maintainers closed **11 pull requests** today, moving the project forward on multiple fronts:

**Cowork UX & Stability (High Activity)**
- Fixed scroll-to-bottom alignment so the feed stays with the latest message ([PR #2174](https://github.com/netease-youdao/LobsterAI/pull/2174)).
- Preserved user line breaks in sent message bubbles ([PR #2173](https://github.com/netease-youdao/LobsterAI/pull/2173)).
- Resolved missing model metadata display for manually stopped streams ([PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154)).
- Prevented a startup-turn race condition from sending unwanted chat artifacts ([PR #2147](https://github.com/netease-youdao/LobsterAI/pull/2147)).

**Model Selection & Voice Input**
- Fixed conflicts between user-defined and packaged models sharing the same name ([PR #2153](https://github.com/netease-youdao/LobsterAI/pull/2153)).
- Preserved draft ownership and cancel guards for voice input after a merge conflict ([PR #2162](https://github.com/netease-youdao/LobsterAI/pull/2162)).

**Infrastructure & Operational Fixes**
- **Raised OpenClaw gateway heap limits** to mitigate OOM crashes on long-running workloads ([PR #2149](https://github.com/netease-youdao/LobsterAI/pull/2149)).
- Updated authentication portal URLs to the new production domains ([PR #2144](https://github.com/netease-youdao/LobsterAI/pull/2144)).

**Documentation / Maintenance**
- Optimized the project readme ([PR #2175](https://github.com/netease-youdao/LobsterAI/pull/2175)).
- Cleared a long-stale PR: fixed modal title truncation for agent/skill/MCP modals ([PR #1463](https://github.com/netease-youdao/LobsterAI/pull/1463), filed 2026-04-04).

### 4. Community Hot Topics
The defining community event of the day is a single, high-severity security finding:

- **[Issue #2176: [Security] Arbitrary Local File Read via Artifact Loading](https://github.com/netease-youdao/LobsterAI/issues/2176)**
    - **Author:** YLChen-007
    - **Activity:** Created 2026-06-18, 1 comment.
    - **Analysis:** The report details how the automatic parsing of `MEDIA:` references in assistant/tool output can be exploited to read arbitrary local files. This bypasses a fundamental security boundary in the agent architecture. The underlying community need is for a **sandboxed resolution mechanism** (e.g., user confirmation, path restriction, or protocol allow-list) for artifact loading. Given the severity, this will almost certainly drive the next immediate hotfix.

No other issues or PRs generated significant comment activity today.

### 5. Bugs & Stability
| Severity | Issue / Fix | Status |
|---|---|---|
| **Critical** | **Arbitrary Local File Read** ([Issue #2176](https://github.com/netease-youdao/LobsterAI/issues/2176)). Automatic artifact loading exposes file system. | **Open / No fix PR yet** |
| **High** | **OOM Crashes** in OpenClaw gateway on long-running workloads. ([PR #2149](https://github.com/netease-youdao/LobsterAI/pull/2149)) | **Resolved** |
| **Medium** | **Cowork Race Condition**: Stopped startup turns could send chat artifacts. ([PR #2147](https://github.com/netease-youdao/LobsterAI/pull/2147)) | **Resolved** |
| **Medium** | **UX Regressions**: Scroll position, missing metadata, plain text formatting, voice cancel guards. (PRs #2174, #2173, #2154, #2162) | **All Resolved** |
| **Low** | **Stale Portal URLs** in auth fallback redirects. ([PR #2144](https://github.com/netease-youdao/LobsterAI/pull/2144)) | **Resolved** |

### 6. Feature Requests & Roadmap Signals
The recent release and PR activity provide clear signals for the project’s short-term trajectory:

- **Desktop Automation is the headline.** The “Computer Use” feature ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) elevates LobsterAI from a pure chat assistant to a direct desktop manipulation agent.
- **Voice becomes a first-class Cowork channel.** The realtime ASR integration ([PR #2148](https://github.com/netease-youdao/LobsterAI/pull/2148)) and the subsequent cancel-guard fixes point to voice being a core interaction paradigm moving forward.
- **Prediction for v2026.6.18+**: A **security hotfix** addressing Issue #2176 is the absolute top priority. Beyond that, expect continued refinement of the Computer Use action space and deeper context management for long-running Cowork sessions.

### 7. User Feedback Summary
- **Pain Points Addressed:**
    - Users running heavy agents on limited hardware will benefit from the OOM fix.
    - The cluster of Cowork UX fixes resolves daily friction points (jumpy scroll, lost formatting, invisible metadata after stopping a stream).
    - A minor-but-annoying UI overflow bug in modals (filed in April) was finally resolved.
- **Emerging Pain Points:**
    - **Security is now top-of-mind.** The file-read vulnerability creates immediate risk for users importing external agent definitions or tools.
- **Satisfaction Indicators:**
    - The 11-PR merge day demonstrates a highly responsive core team.
    - The rapid release cycle (new feature release + immediate bug fixes) suggests robust quality assurance and iteration discipline.

### 8. Backlog Watch
- **[PR #1463: Fix long modal titles](https://github.com/netease-youdao/LobsterAI/pull/1463)**
    - **Status: Merged (2026-06-17).**
    - Created **2026-04-04** and finally merged today after **2.5 months** in the backlog. This fix resolves an overflow issue in agent, skill, MCP, and scheduled task modals. Its successful merge today signals that the maintainers are actively cleaning up historical technical debt.

**Currently at risk of entering backlog purgatory:**
- **[Issue #2176](https://github.com/netease-youdao/LobsterAI/issues/2176)** if it is not quickly addressed. It is the most pressing open item and requires an immediate security advisory and patch.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

**TinyAGI Project Digest**
**Date: 2026-06-18**

**1. Today's Overview**
Today’s activity is dominated by a severe security disclosure event. Three critical vulnerabilities were filed by security researcher YLChen-007, highlighting fundamental flaws in authentication, input validation, and permission defaults. No new releases, pull requests, or bug fixes have been published, indicating the project is currently in a triage and response posture rather than feature development. While community issue reporting is high, code velocity is effectively paused. The project’s health is strained by these zero-day disclosures, and immediate maintainer attention is required to restore user trust.

**2. Releases**
No new releases were published today. The project currently has no published Releases in its history.

**3. Project Progress**
No pull requests were merged, closed, or opened in the last 24 hours. There is no public evidence of work being committed toward resolving the disclosed vulnerabilities or advancing other features. The project’s progress is stalled as the team presumably responds to the security incident.

**4. Community Hot Topics**
All community attention is focused on three critical security issues filed today, which collectively expose the attack surface for unauthenticated access and arbitrary file handling.

*   **[#284: TinyAGI allows unauthenticated API messages to invoke Claude with provider permission checks disabled by default](https://github.com/TinyAGI/tinyagi/issues/284)** — The `POST /api/message` endpoint lacks authentication and bypasses internal permission checks, permitting direct, unauthorized LLM invocation.
*   **[#283: Unauthenticated `prompt_file` agent configuration allows arbitrary local file disclosure to the model provider](https://github.com/TinyAGI/tinyagi/issues/283)** — The agent configuration API accepts an attacker-controlled `prompt_file` path, reading arbitrary host files into agent context and sending them to the AI provider.
*   **[#282: Untrusted `[send_file: ...]` response tags allow arbitrary host file attachment delivery](https://github.com/TinyAGI/tinyagi/issues/282)** — Output parser unsafely processes response tags, allowing exfiltration of arbitrary host files via model output.

**Underlying Need:** The community urgently requires a hardened security model by default, including mandatory API authentication, strict path allow-lists, and output sanitization. The lack of comments on these issues likely reflects a user base assessing immediate exposure rather than debating the findings.

**5. Bugs & Stability**
Three critical stability and security regressions were reported today. No fix PRs exist yet. Ranked by severity:

*   **Critical** — **[#284](https://github.com/TinyAGI/tinyagi/issues/284)**: Complete lack of API authentication allows unauthenticated attackers to invoke AI models (Claude) with all permission checks disabled. Potential for service hijacking and cost/abuse exploitation.
*   **Critical** — **[#283](https://github.com/TinyAGI/tinyagi/issues/283)**: Arbitrary local file read via agent configuration. Allows data exfiltration of any file readable by the TinyAGI process.
*   **Critical** — **[#282](https://github.com/TinyAGI/tinyagi/issues/282)**: Arbitrary host file attachment via output tags. Similar impact to #283 but through output parsing.

All three represent fundamental architectural security gaps in the default deployment. No remediation commits or PRs have been published as of this digest.

**6. Feature Requests & Roadmap Signals**
No explicit feature requests were filed today. However, the security disclosures function as an implicit but urgent roadmap signal. The next release of TinyAGI must prioritize **Default Security** by including:

*   Mandatory authentication on all API endpoints.
*   Strict path validation and allow-lists for `prompt_file` and potentially similar config fields.
*   Output sanitization and capability gating for response tags (e.g., `[send_file]`).
*   Provider permission checks enabled and enforced by default.

These items are no longer optional; they are blocking issues for safe project adoption.

**7. User Feedback Summary**
User feedback today is entirely indirect, expressed through the filing of critical security issues. The primary pain points exposed are:

*   **Data Breach Risk:** Default agent and response handling allows arbitrary file reads, creating immediate liability for any deployment.
*   **Service Abuse:** Unauthenticated API endpoints mean anyone with network access can consume AI resources.
*   **Governance Gap:** No default authentication or permission system means "out of the box" is "insecure by design."

Satisfaction is at a low point for any user running an exposed instance, and trust in the project’s default configurations is severely undermined. The researcher (YLChen-007) has effectively petitioned for ecosystem-wide security hardening on behalf of the user base.

**8. Backlog Watch**
While there are no long-stale issues in the provided data, the three security issues ([#282](https://github.com/TinyAGI/tinyagi/issues/282), [#283](https://github.com/TinyAGI/tinyagi/issues/283), [#284](https://github.com/TinyAGI/tinyagi/issues/284)) are now the most critical items in the backlog. They have been open for less than 24 hours, but their urgency cannot be overstated. The project maintainer’s response time — whether through acknowledgment, CVE request, or hotfix release — will be the defining signal of project health and governance quality in the coming days. If these issues remain without a plan for more than 48 hours, significant damage to community trust is expected.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

### Moltis Project Digest
**Date:** June 18, 2026  
**Repository:** [github.com/moltis-org/moltis](https://github.com/moltis-org/moltis)

---

### 1. Today’s Overview
Moltis saw a quiet development day on June 18, 2026, with no new releases, no merged pull requests, and no closed issues. Activity was concentrated in two open feature requests and one open pull request, all focused on expanding user configurability. The absence of bug reports or regression flags indicates a stable codebase period. The community’s momentum is clearly directed toward maturing the project’s output flexibility and operational resilience.

---

### 2. Releases
*No new releases were published in the last 24 hours.*

---

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The sole contribution in progress is **PR #1130** ([link](https://github.com/moltis-org/moltis/pull/1130)), authored by khimaros, which adds a configurable timeout for the WebUI RPC interface. This PR addresses **Issue #1127** and represents the only code motion currently in the pipeline.

---

### 4. Community Hot Topics
- **TTS Output Format Configuration (Issue #1126)** – The most active discussion today with 3 comments. This request seeks user control over the format of TTS audio output. The depth of conversation suggests users are integrating Moltis into external audio pipelines or have strict codec/format requirements.  
  [Issue #1126](https://github.com/moltis-org/moltis/issues/1126)

- **Markdown Copy & Export (Issue #1131)** – A fresh feature request by vvuk asking for “Copy + export as Markdown” functionality. With zero comments yet, it signals a latent but significant user demand for standard data portability and easy extraction of conversation histories.  
  [Issue #1131](https://github.com/moltis-org/moltis/issues/1131)

- **Configurable RPC Timeout (PR #1130)** – The lone open PR, authored by the same contributor who raised #1126. It directly tackles a connectivity pain point for users running Moltis in high-latency or resource-constrained environments.  
  [PR #1130](https://github.com/moltis-org/moltis/pull/1130)

---

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. Both open issues are classified as enhancements rather than defects. The open **PR #1130** (configurable RPC timeout) acts as a proactive stability patch, preventing user-facing disconnections, but no immediate severity incidents require triage.

---

### 6. Feature Requests & Roadmap Signals
The 24-hour data points strongly toward a near-term focus on **Configuration and Interoperability**. The requests for configurable TTS output (#1126) and Markdown export (#1131) indicate that users are pushing Moltis into production workflows where standardized, portable output formats are essential. The RPC timeout feature (#1130) is a small, scoped infrastructure improvement likely destined for a minor patch release. Taken together, these items suggest the next release may center on a “Customization & Connectivity” theme.

---

### 7. User Feedback Summary
Direct evaluative feedback (praise or criticism) is absent from this data snapshot, but the filed issues clearly reveal user pain points. The dominant unmet need is **output flexibility**—both for TTS audio and exported conversation text. A notable pattern is that the same power-user (khimaros) authored both the TTS feature request (#1126) and the RPC timeout fix (#1130), suggesting a committed segment of the user base is actively contributing code to address their own workflow gaps.

- **Pain Points:** Inability to control TTS output format; inability to export conversations as Markdown; RPC disconnections due to fixed timeouts.  
- **Use Cases:** Users are operationalizing the agent with external tools, requiring standard audio formats and easily extractable text output.  
- **Satisfaction:** Neutral-to-positive regarding core stability; mild dissatisfaction regarding the lack of configurable outputs and network resilience.

---

### 8. Backlog Watch
- **Untriaged Feature Requests:** Both **Issue #1126** (TTS format config) and **Issue #1131** (Markdown export) lack maintainer labels, assignments, or milestone targets. Formal triage is recommended to set community expectations.
- **Unmerged Pull Request:** **PR #1130** ([link](https://github.com/moltis-org/moltis/pull/1130)) is a clean, scoped fix ready for maintainer review. Delaying its merge also blocks resolution for its parent issue **#1127**, which may be affecting real users.
- **No deeply lingering items:** Given the snapshot window (last 24 hours), no critically long-unanswered issues are present, but the above items represent the primary queue requiring maintainer attention.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

## CoPaw Project Digest — 2026-06-18

**Data Source:** Issues and PRs updated in the last 24 hours across the CoPaw / QwenPaw repository.

---

### 1. Today’s Overview
CoPaw experienced a peak-activity day, with exactly **50 Issues** and **50 Pull Requests** updated. The project is in a clear **stabilization-and-release** cadence: 39 of those Issues and 33 of the PRs were closed or merged. Two new versions shipped—the stable **v1.1.12** and a preceding **v1.1.12-beta.2**—bringing major UI reworks and a suite of backend fixes. At the same time, the version branch jumped to **2.0.0a1**, signaling that a major architectural milestone (AgentScope 2.0 alpha) is officially underway. Community engagement remains extremely high, though several chronic pain points around upgrade stability and cross-channel reliability are keeping the bug queue active.

---

### 2. Releases
**v1.1.12-beta.2** and **v1.1.12 (stable)** were published.

**v1.1.12 – Highlights:**
- **Models Page Overhaul:** Provider aggregation, unified card UI, and layout redesign ([#5203](https://github.com/agentscope-ai/QwenPaw/issues/5203)).
- **Simple Mode:** Flat navigation bar and session list sorted by updated time ([#5222](https://github.com/agentscope-ai/QwenPaw/issues/5222)).

**v1.1.12-beta.2 – Highlights:**
- Performance improvement: removal of unnecessary deep copy operations in agent config ([#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240)).
- Feature: session filter by title ([#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178)).

**Migration Note:** No explicit breaking changes or migration steps were announced. However, the Models Page redesign and new Simple Mode may alter navigation expectations for existing users.

---

### 3. Project Progress
**Merged/Closed PRs (33 closed today):**
- **Branching:** The version was bumped to **2.0.0a1** ([#5281](https://github.com/agentscope-ai/QwenPaw/pull/5281)) to begin the AgentScope 2.0 alpha cycle. The official v1.1.12 release PR was also merged ([#5280](https://github.com/agentscope-ai/QwenPaw/pull/5280)).
- **XiaoYi Channel:** A dual-WebSocket refactor landed that fixes the previously unusable channel ([#5274](https://github.com/agentscope-ai/QwenPaw/pull/5274), [#3839](https://github.com/agentscope-ai/QwenPaw/pull/3839)).
- **Memory Fix:** ChromaDB probe collection renamed from `_probe` to `probe-test` to avoid `InvalidArgumentError` ([#5289](https://github.com/agentscope-ai/QwenPaw/pull/5289)).
- **Backup Reliability:** Unreadable files are now skipped during backups instead of failing the whole operation ([#5041](https://github.com/agentscope-ai/QwenPaw/pull/5041)).
- **Provider Expansion:** The Venice AI provider was merged after three months as an open PR ([#1088](https://github.com/agentscope-ai/QwenPaw/pull/1088)).

**Open / Under Review (17 open today):**
- **UI:** Chat history as a permanent right sidebar ([#5293](https://github.com/agentscope-ai/QwenPaw/pull/5293)); customizable column order on the sessions page ([#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975)).
- **Migration:** OpenClaw config migration CLI tool ([#5276](https://github.com/agentscope-ai/QwenPaw/pull/5276)).
- **Stability:** SSL cert configuration for DingTalk ([#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291)); timeout protection for cron misfires and context compaction ([#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241), [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242)); compaction crash fix for schema `maxLength` violations ([#5287](https://github.com/agentscope-ai/QwenPaw/pull/5287)).

---

### 4. Community Hot Topics
- **Most Discussed Issue:** [#280 — *Discussion: Which Skills and MCPs Can Be Built-in?*](https://github.com/agentscope-ai/QwenPaw/issues/280) (27 comments, closed but still seeing activity). Users are strongly vocal about wanting a richer default skill set to improve the out-of-box experience.
- **Performance Pain:** [#4108 — *WebUI lag/stuttering during inference*](https://github.com/agentscope-ai/QwenPaw/issues/4108) (8 comments). Users report the UI becomes unusable while generating responses.
- **Channel Reliability:** The Feishu upload-limit bug ([#472](https://github.com/agentscope-ai/QwenPaw/issues/472)) and repeated Docker upgrade failures ([#2229](https://github.com/agentscope-ai/QwenPaw/issues/2229), [#2254](https://github.com/agentscope-ai/QwenPaw/issues/2254)) continue to dominate user frustration.

**Underlying Needs:** The community is asking for **stability guarantees across upgrades**, **better performance under load**, and a **richer skill ecosystem** that reduces the burden of manual configuration.

---

### 5. Bugs & Stability
- **Critical:** *Inter-Agent Infinite Loop via Matrix* ([#5204](https://github.com/agentscope-ai/QwenPaw/issues/5204), **OPEN**). Two agents trigger an endless mutual wake cycle with no runtime-level circuit breaker. No fix merged yet.
- **High:** *Built-in Skills Re-enable on Every Upgrade* ([#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262), **OPEN**). A persistent UX regression across versions (1.1.9→1.1.10→1.1.11).
- **Medium:**
    - *DingTalk SSL Failure on Windows uv Installs* ([#5291 open PR exists](https://github.com/agentscope-ai/QwenPaw/pull/5291)).
    - *Context Compaction Hangs When Summary Exceeds Schema* ([#5287 open PR exists](https://github.com/agentscope-ai/QwenPaw/pull/5287)).
    - *Discord.py Import Error* ([#5290](https://github.com/agentscope-ai/QwenPaw/issues/5290), **OPEN**).
- **Fixed Today:** ChromaDB probe collection naming causing degradation ([#5284](https://github.com/agentscope-ai/QwenPaw/issues/5284), fixed by [#5289](https://github.com/agentscope-ai/QwenPaw/pull/5289)); cache pollution in `load_agent_config()` ([#5275](https://github.com/agentscope-ai/QwenPaw/pull/5275)).

---

### 6. Feature Requests & Roadmap Signals
- **Major Signal:** The **bump to v2.0.0a1** ([#5281](https://github.com/agentscope-ai/QwenPaw/pull/5281)) marks the start of the AgentScope 2.0 alpha cycle. This implies significant architectural changes are in the pipeline.
- **Near-Term Features (in open PRs):**
    - Chat history as a permanent sidebar ([#5293](https://github.com/agentscope-ai/QwenPaw/pull/5293)).
    - CLI `cron update` command ([#5210](https://github.com/agentscope-ai/QwenPaw/pull/5210)).
    - OpenClaw config migration ([#5276](https://github.com/agentscope-ai/QwenPaw/pull/5276)).
- **Community Requests (unmerged):** A **public HTTP API** ([#2202](https://github.com/agentscope-ai/QwenPaw/issues/2202)), **multi-user profile separation** ([#2233](https://github.com/agentscope-ai/QwenPaw/issues/2233)), and a **web console upgrade mechanism** ([#2235](https://github.com/agentscope-ai/QwenPaw/issues/2235)) remain ongoing discussion points.

**Prediction:** The next stable release will likely include the sidebar chat history and enhanced CLI features. The 2.0 alpha branch suggests a consolidation of configuration and provider handling is coming.

---

### 7. User Feedback Summary
- **Satisfaction Drivers:** Users appreciate the aggressive release cadence. The **Models Page Overhaul** and **Simple Mode** directly address long-standing requests for UI clarity and reduced complexity.
- **Friction Points:**
    - *Upgrade Fatigue:* Users routinely report configuration resets, disabled skills re-enabling, and Docker containers failing to start after upgrades.
    - *Performance Regression:* “Experience is getting worse” ([#4108](https://github.com/agentscope-ai/QwenPaw/issues/4108)), particularly during inference on the WebUI.
    - *Channel Fragmentation:* Feishu, DingTalk, and QQ each have their own class of bugs, signaling a need for a more standardized channel testing framework.
- **Community Vibe:** There is a healthy influx of **first-time contributors** submitting bug fixes and minor features. However, a user expressed **fear of contribution rejection** when using AI coding tools ([#2677](https://github.com/agentscope-ai/QwenPaw/issues/2677)), suggesting the maintainers should clarify guidelines around AI-assisted PRs to keep the contributor pipeline robust.

---

### 8. Backlog Watch
Several important items that need maintainer attention:

1. **Matrix Agent Infinite Loop** ([#5204](https://github.com/agentscope-ai/QwenPaw/issues/5204)): A critical architectural gap that has no fix in the queue. Related to previous ReAct loop reports and subagent polling issues. Requires a cross-cutting solution rather than a one-line patch.
2. **Long-Open Provider/Feature PRs Recently Closed:** The **Venice AI provider** ([#1088](https://github.com/agentscope-ai/QwenPaw/pull/1088), opened March 10) and **XiaoYi channel refactor** ([#3839](https://github.com/agentscope-ai/QwenPaw/pull/3839), opened April 26) were both merged today after months of dormancy. The maintainers should monitor whether similar "stale" PRs (e.g., other provider requests) need attention.
3. **Persistent Demand for Built-In Skills** ([#280](https://github.com/agentscope-ai/QwenPaw/issues/280)): Even though closed, this discussion remains highly active. The lack of a formal spec or roadmap for default Skills/MCPs is a gap that might be filled by the v2.0 cycle.
4. **HTTP API Request** ([#2202](https://github.com/agentscope-ai/QwenPaw/issues/2202)): A recurring ask from users wanting to integrate CoPaw headlessly. No substantive movement yet.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-18

## 1. Today's Overview

ZeroClaw is deep in a major multi-track development push across its v0.8.x and v0.9.0 milestones, exhibiting extremely high throughput. The project saw **50 issues and 50 pull requests updated in the last 24 hours**, with **11 PRs merged or closed**. The standout achievement is the completion of an 8-part stacked PR series delivering the long-awaited typed configuration cascade for alias deletion and renaming. Simultaneously, the team is actively addressing urgent security hardening (SSRF prevention in `http_request`, hardened CI with SBOM generation) and tackling critical cross-platform regressions, particularly across Windows. No new releases were cut today, indicating prioritized stabilization and feature integration ahead of the next public version.

## 2. Releases

No new releases were published today.

## 3. Project Progress

The most significant advancement is the merger of the **stacked config management series**:
- **Feat(config): rename_with_cascade for aliased entries ([#7840](https://zeroclaw-labs/zeroclaw/pull/7840))** — Added config-level rename propagation.
- **Feat(gateway): agent owned-state rename cascade ([#7841](https://zeroclaw-labs/zeroclaw/pull/7841))** — Wired the rename into gateway and memory state.
- **Feat(cli): agents/providers/channels CRUD + skill-bundle cascade ([#7842](https://zeroclaw-labs/zeroclaw/pull/7842))** — Exposed the full feature through the CLI. This resolves Issues [#7175](https://zeroclaw-labs/zeroclaw/issues/7175) and [#7468](https://zeroclaw-labs/zeroclaw/issues/7468).

Critical bug fixes and improvements merged today:
- **Canvas-store regression repaired ([#7563](https://zeroclaw-labs/zeroclaw/issues/7563))**: The Web UI `/canvas` endpoint was broken after WebSocket sessions introduced in PR #6986. This S1 workflow blocker is now closed.
- **ACP event transparency ([#7684](https://zeroclaw-labs/zeroclaw/pull/7684))**: History pruner and turn-cancel events are now surfaced as visible events instead of silent collapses.

High-impact open PRs moving toward merge include:
- **Windows self-update fix ([#7853](https://zeroclaw-labs/zeroclaw/pull/7853))**: Overhauls the fundamentally broken binary-swap path.
- **SSRF hardening ([#7902](https://zeroclaw-labs/zeroclaw/pull/7902))**: Adds resolved-IP DNS validation to `http_request`.
- **Cached input token pricing ([#7492](https://zeroclaw-labs/zeroclaw/pull/7492))**: Adds support for `prompt_tokens_details.cached_tokens` from OpenAI-compatible providers.
- **Persistent manual cron trigger results ([#7893](https://zeroclaw-labs/zeroclaw/pull/7893))**: Shared manual trigger runner across RPC, API, and the `cron_run` tool.

## 4. Community Hot Topics

Issues with the highest engagement:

- **[RFC: Computer-use support for desktop screen interaction and input control ([#6909](https://zeroclaw-labs/zeroclaw/issues/6909))](https://zeroclaw-labs/zeroclaw/issues/6909)** — 6 comments
  The most active discussion. Users are requesting desktop GUI control (screenshots, mouse, keyboard) similar to OpenAI Codex. The depth of the RFC suggests this is the community's most desired new capability.
- **[Feature: Make channel reply-intent precheck configurable ([#6067](https://zeroclaw-labs/zeroclaw/issues/6067))](https://zeroclaw-labs/zeroclaw/issues/6067)** — 5 comments
  Community wants opt-in visibility and timeout control over `classify_channel_reply_intent`, signaling latency pain in channel operations.
- **[RFC: Route scheduled tasks through the orchestrator message pipeline ([#6954](https://zeroclaw-labs/zeroclaw/issues/6954))](https://zeroclaw-labs/zeroclaw/issues/6954)** — 4 comments
  Users are keenly following the fix for a cluster of cron-related bugs. The underlying need is reliable, context-aware scheduled tasks.
- **[RFC: Native context compression as a provider pipeline decorator ([#7673](https://zeroclaw-labs/zeroclaw/issues/7673))](https://zeroclaw-labs/zeroclaw/issues/7673)** — 3 comments
  Growing interest in automated context window compression to reduce token costs and latency.

## 5. Bugs & Stability

**Critical (S1 — Workflow Blocked):**
- **[#7907 Agent rename race condition — **NEW TODAY**](https://zeroclaw-labs/zeroclaw/issues/7907)**: The newly merged rename cascade (#7841) contains a critical ordering flaw where state is mutated before config persistence. *No dedicated fix PR yet.*
- **[#7563 Canvas-store regression](https://zeroclaw-labs/zeroclaw/issues/7563)**: **RESOLVED**. Web UI `/canvas` broken after WebSocket sessions. Merged today.

**High Severity (S2 — Degraded Behavior / P1-P2):**
- **[#7462 74 test failures on Windows](https://zeroclaw-labs/zeroclaw/issues/7462)**: The entire Windows test suite is severely broken. No fix PR submitted yet, but the project is actively investing in Windows remediation.
- **[#7737 Approval attribution race condition](https://zeroclaw-labs/zeroclaw/issues/7737)**: Concurrent approvals can overwrite channel-global side-channel state before the runtime consumes it.
- **[#6105 Agent lacks cron job context](https://zeroclaw-labs/zeroclaw/issues/6105)**: Root cause shared with #6954. Agents execute cron jobs without knowing which job triggered them.

**Fixes and Fix PRs in Flight:**
- **SSRF in `http_request`**: Fix PR [#7902](https://zeroclaw-labs/zeroclaw/pull/7902) adds `domain_guard` DNS validation.
- **Windows self-update broken**: Fix PR [#7853](https://zeroclaw-labs/zeroclaw/pull/7853) replaces remove-then-copy with rename-then-copy.
- **Groq tool calling throws HTTP 400**: Fix PR [#7909](https://zeroclaw-labs/zeroclaw/pull/7909) adds the required `name` field to tool-result messages.
- **WebDriver snapshot returns null**: Fix PR [#7908](https://zeroclaw-labs/zeroclaw/pull/7908) adds a `return` prefix to generated JavaScript.
- **Cron trigger results not persisted**: Fix PR [#7893](https://zeroclaw-labs/zeroclaw/pull/7893) unifies manual trigger paths with the daemon scheduler.

## 6. Feature Requests & Roadmap Signals

**Near-Term (v0.8.x Tracks):**
- **WASM Plugin Lifecycle Hooks ([#7822](https://zeroclaw-labs/zeroclaw/issues/7822))**: RFC for `PluginCapability::Hook` allowing plugins to subscribe to agent lifecycle events. Likely for v0.8.2 Skills/WASM track.
- **MCP Dashboard ([#7320](https://zeroclaw-labs/zeroclaw/issues/7320))**: Web-based plugin management surface in active planning.
- **Skills Platform ([#7852](https://zeroclaw-labs/zeroclaw/issues/7852))**: Request for coherent skills + plugin + A2A surface.
- **Make channel reply-intent precheck configurable ([#6067](https://zeroclaw-labs/zeroclaw/issues/6067))**: Accepted P2, code likely in active development given the PR volume.

**Mid-Term (v0.9.0 — Auth/Security):**
- **Hardened CI Pipeline ([#7675](https://zeroclaw-labs/zeroclaw/issues/7675))**: Supply-chain scanning, provenance verification, and SBOM generation.
- **Provider Fallback Notices ([#7883](https://zeroclaw-labs/zeroclaw/issues/7883))**: Opt-in user visibility into intra-family model fallbacks.
- **Sandbox Policy Config ([#7821](https://zeroclaw-labs/zeroclaw/pull/7821))**: `SandboxPolicyConfig` struct added as the canonical model.

**Community-Driven Predictions for next releases:**
- **Desktop Computer-Use ([#6909](https://zeroclaw-labs/zeroclaw/issues/6909))**: Highest-engagement feature request. Unlikely for v0.8.1, but a strong candidate for v0.9.x given high `risk` and `type:rfc` labels.
- **Context Compression ([#7673](https://zeroclaw-labs/zeroclaw/issues/7673))**: Cost optimization is a transparent community need. Could land as a decorator in v0.8.2 or v0.8.3.

## 7. User Feedback Summary

**Pain Points & Reported Issues:**
- **Windows support** is the top pain point. Users report 74 test failures ([#7462](https://zeroclaw-labs/zeroclaw/issues/7462)), a broken self-update ([#7853](https://zeroclaw-labs/zeroclaw/pull/7853)), and confusion over `cmd.exe` vs PowerShell defaults ([#7089](https://zeroclaw-labs/zeroclaw/issues/7089)).
- **Groq API incompatibility**: Community member reports a blocking `HTTP 400` error because tool-result messages lack a mandatory `name` field ([#7896](https://zeroclaw-labs/zeroclaw/issues/7896), fix in [#7909](https://zeroclaw-labs/zeroclaw/pull/7909)).
- **Cron job invisibility**: Users want the agent to know *which* cron job triggered it. The scheduler currently bypasses full context ([#6105](https://zeroclaw-labs/zeroclaw/issues/6105)).
- **Android/Termux setup** blocked by incorrect binary architecture detection ([#7911](https://zeroclaw-labs/zeroclaw/issues/7911)).

**Satisfaction & Desired Capabilities:**
- High positive engagement with RFCs around desktop computer-use, WASM plugins, and MCP dashboards.
- The completion of the config rename/delete cascade (#7840–#7842) directly addresses longstanding community requests for better operational tooling.
- Users are actively using the provider compatibility layer and providing detailed bug reports, indicating strong real-world adoption of OpenAI-compatible endpoints.

## 8. Backlog Watch

Items requiring maintainer attention or experiencing prolonged inactivity:

- **[#6510 cron `delivery.mode = "announce"` option](https://zeroclaw-labs/zeroclaw/issues/6510)**: Accepted P2. Requests an opt-in flag to send only the final assistant message instead of every intermediate turn. Updated June 17 but no implementation assigned.
- **[#6653 Host architecture policy for emulated installs](https://zeroclaw-labs/zeroclaw/issues/6653)**: Accepted P3. Decides whether `zeroclaw update` should detect physical host architecture. Low activity since acceptance.
- **[#6084 (Related cron bug cluster)](https://zeroclaw-labs/zeroclaw/issues/6084)**: Referenced in the #6954 root-cause analysis. Accepted, but pending the full orchestrator pipeline rewrite.
- **Security Pipeline Concerns ([#7675](https://zeroclaw-labs/zeroclaw/issues/7675))**: The RFC explicitly states the current pipeline has blind spots (no `cargo audit` on PRs, no SLSA provenance). Despite high risk and accepted status, no implementation PR has been opened.
- **Windows Test Remediation ([#7462](https://zeroclaw-labs/zeroclaw/issues/7462))**: 74 failing tests on Windows. No fix PR exists yet. Given the active community pushing Windows fixes (#7853, #7910, #7089), this backlog item is growing in urgency.
- **Android Termux Support ([#7911](https://zeroclaw-labs/zeroclaw/issues/7911))**: Opened today. Not an official supported platform, but signals growing demand from non-standard environments. Needs a triage label and response.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*