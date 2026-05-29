# OpenClaw Ecosystem Digest 2026-05-29

> Issues: 373 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-29 02:54 UTC

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

Here is the structured project digest for OpenClaw based on the provided 2026-05-29 data snapshot.

---

## OpenClaw Project Digest — 2026-05-29

### 1. Today's Overview

OpenClaw experienced a surge of activity over the past 24 hours, with **373 issues** and **500 pull requests** updated alongside the release of two new versions (`v2026.5.27` and `v2026.5.27-beta.1`). This high velocity reflects a focused effort to stabilize the platform following the problematic `v2026.5.26` release, which introduced several regressions specifically in the native hook relay and codex harness subsystems. The `v2026.5.27` patch heavily prioritizes security hardening and content boundary enforcement, but the sheer volume of regression reports indicates significant systemic strain on the core agent infrastructure. While the team is demonstrating excellent turnaround time on hotfixes, the churn suggests a need for deeper root cause analysis and hardened test coverage across the channel and agent runtime stacks.

### 2. Releases

Two releases were shipped in the last 24 hours:

- **`v2026.5.27` (Stable)**
- **`v2026.5.27-beta.1`**

Both share identical changelog highlights, indicating a rapid beta-to-stable promotion. The primary focus is **tightening security and content boundaries**:
- **Group prompt isolation:** Group-level prompt text is kept out of the system prompt.
- **Hostname normalization:** Repeated-dot hostnames are normalized to mitigate spoofing.
- **Runtime hardening:** Side-effecting command wrappers and unsafe Node.js runtime environment overrides are blocked.
- **Network exposure prevention:** No-auth Tailscale exposure is explicitly rejected.
- **Access control:** Tightened node/device-role approval flows.

**Migration Notes:**
Operators should review their configurations against the blocked side-effecting command wrappers and safe runtime overrides, as custom setups relying on these mechanisms may now fail validation. The new Tailscale exposure rejection will immediately prevent accidental public exposure on start-up, which is a welcome safety net but could break ad-hoc debugging setups.

### 3. Project Progress

Out of the **500 PRs updated**, **163 were merged or closed**. Significant developments include:

**Major Fixes & Closures (Regressions Squashed):**
- **Native Hook Relay Fixes:** Multiple high-severity issues from the `v2026.5.26` regression were closed, including #87331 and #87395 (Native hook relay unavailable).
- **Gateway & Loop Blocking:** The gateway pre-warm event loop block (#85999) and the preflight compaction deadlock (#87016) were resolved.
- **Channel-Specific Fixes:**
  - The `v2026.5.27` Feishu dispatch crash (TypeError on `run` of undefined) was rapidly addressed via PR [#87849](https://github.com/openclaw/openclaw/pull/87664).
  - Telegram partial draft preview spam (#84885) was fixed.

**New Features & Advanced Work (Open PRs):**
- **Supervisor Plugin:** PR [#87849](https://github.com/openclaw/openclaw/pull/87849) adds a bundled `codex-supervisor` plugin for direct Codex app-server session probes, session listing, and transcript reads.
- **Core Session Goals:** PR [#87469](https://github.com/openclaw/openclaw/pull/87469) replaces a plugin-based approach with core-owned session goals, including resumable blocked/budget-limited goals.
- **Memory Architecture:** PR [#86210](https://github.com/openclaw/openclaw/pull/86210) introduces a multi-slot memory role architecture, allowing memory plugins (recall, compaction, capture, pattern) to compose instead of competing.

### 4. Community Hot Topics

The community is overwhelmingly focused on stability and regressions:

1.  **[#86599](https://github.com/openclaw/openclaw/issues/86599) – Local Model blocks event loop on Windows Beta (13 comments, P1, Beta Blocker)**
    *   **Underlying Need:** The Windows beta is effectively broken for local model usage due to event-loop starvation. Users need a functional Windows developer experience, especially given the cross-platform nature of the ecosystem.

2.  **[#87536](https://github.com/openclaw/openclaw/issues/87536) – Native hook relay bridge never spawns on v5.26 (6 comments, 2👍)**
    *   **Underlying Need:** Despite the closure of other native hook relay issues, this user reports the bridge completely fails to initialize. This suggests the diagnostic or recovery path for the native hook relay is still insufficient for some edge cases.

3.  **[#73148](https://github.com/openclaw/openclaw/issues/73148) – Image tool fails with "Failed to optimize image" without sharp (11 comments, 3👍)**
    *   **Underlying Need:** A strong desire for a graceful fallback or a clear installation-time dependency check. Users expect vision pipelines to either install dependencies automatically or provide actionable error messages rather than opaque failures.

4.  **[#84583](https://github.com/openclaw/openclaw/issues/84583) – Cron announce delivery triggers session takeover error (7 comments, 3👍)**
    *   **Underlying Need:** Users relying on automated workflows (cron) are experiencing session lock conflicts with interactive use, pointing to a fundamental flaw in how isolated cron tasks acquire and release session locks on active chat sessions.

### 5. Bugs & Stability

**Critical Regressions (P1 – Active / Recent):**
- **[#87646](https://github.com/openclaw/openclaw/issues/87646)**: Feishu channel completely fails to dispatch messages after `v2026.5.27` upgrade (`TypeError: Cannot read properties of undefined (reading 'run')`). **Fix:** Merged in [#87664](https://github.com/openclaw/openclaw/pull/87664).
- **[#87609](https://github.com/openclaw/openclaw/issues/87609)**: WhatsApp group @mentions silently drop for all but the first mention (Regression in `v2026.5.26`).
- **[#86519](https://github.com/openclaw/openclaw/issues/86519)**: Agent repeats identical replies 2-10x on Telegram (Regression in `v2026.5.20`, partially mitigated in `v2026.5.22`).
- **[#66599](https://github.com/openclaw/openclaw/issues/86599)**: Local model providers block the Gateway event loop on Windows beta. Still pending maintainer review / info.
- **[#86047](https://github.com/openclaw/openclaw/issues/86047)**: Codex app-server approval stalls cause interrupted turns and tool-execution timeouts (Regression in `v2026.5.22`).
- **[#87536](https://github.com/openclaw/openclaw/issues/87536)**: Native hook relay bridge never spawns on `v2026.5.26`.

**High-Severity Issues (P1/P2 – Open):**
- **[#87436](https://github.com/openclaw/openclaw/issues/87436)**: Codex harness recreates legacy `openai-codex` session route state after `doctor --fix`. Open fix in [#87851](https://github.com/openclaw/openclaw/pull/87851).
- **[#85888](https://github.com/openclaw/openclaw/issues/85888)**: Cron jobs consistently fail with MiniMax 503 during early morning CST, manual triggers succeed. Suggests a batch scheduling load issue.
- **[#87322](https://github.com/openclaw/openclaw/issues/87322)**: Mattermost block streaming edits a single post in place instead of sending separate messages, breaking the expected streaming user experience.
- **[#87307](https://github.com/openclaw/openclaw/issues/87307)**: Matrix thread replies are sent as normal replies on `v2026.5.22`.
- **[#85192](https://github.com/openclaw/openclaw/issues/85192)**: DeepSeek V4 reasoning-only retry logic is broken, resulting in timeouts instead of a clean continuation prompt.

### 6. Feature Requests & Roadmap Signals

The feature landscape is evolving rapidly, with several larger architectural changes in the pipeline:

**Likely Candidates for `v2026.6.x`:**
- **Session Goals (PR [#87469](https://github.com/openclaw/openclaw/pull/87469)):** This is a major shift from a plugin lease surface to a core-owned, resumable goal system. It strongly suggests the team is doubling down on autonomous agent behaviors.
- **Multi-Slot Memory (PR [#86210](https://github.com/openclaw/openclaw/pull/86210)):** The move away from a single memory plugin slot towards composable role slots (recall, compaction, capture) points to a very significant architecture upgrade designed to solve the plugin compatibility problems flagged in #82977.
- **Voice Model Cataloging (PR [#87794](https://github.com/openclaw/openclaw/pull/87794)):** A refactor to unify voice models (TTS, realtime transcription) under a single provider model entry, cleaning up current fragmentation.
- **Copilot Agent Runtime (PR [#86155](https://github.com/openclaw/openclaw/pull/86155)):** An opt-in runtime backed by the GitHub Copilot CLI and SDK suggests an ambition to bridge OpenClaw's multi-channel interface with the Copilot development ecosystem.

**Signals from Bug Reports:**
- **Better Dependency Management:** The continued struggle with `sharp`, `node-llama-cpp`, and other native dependencies points towards a bundling or runtime dependency resolution overhaul.
- **Scheduler Overhaul:** Issues like #85888 and #84583 suggest the cron/scheduler engine needs smarter batching, conflict resolution, and manual override handling.

### 7. User Feedback Summary

**Dissatisfaction & Pain Points:**
- **Regression Fatigue:** The dominant feedback theme is frustration with the quality of recent stable releases. The `v5.26` "native hook relay" failure blocked a large number of advanced users, while `v5.22` introduced the Codex approval stalls (#86047) and Telegram duplicate replies (#86519). While users appreciate the speed of hotfixes, the feeling of being a beta tester for the stable channel is strong.
- **Channel Parity Fragility:** Every update seems to cause a different channel to break. Telegram, Matrix, WhatsApp, Feishu, and Discord have all had specific regressions in the last two weeks. The user experience is that channel support is volatile.
- **Windows Beta Blocked:** The Windows beta is effectively unusable for local models due to the event-loop issue (#86599). This is a significant blocker for a major platform.

**Satisfaction & Bright Spots:**
- **Responsive Team:** The community consistently praises the triage speed. The `v5.27` hotfix was released very quickly after the `v5.26` regressions were reported.
- **Security Focus:** The clear improvements in content boundaries hostname normalization and side-effect blocking are seen as responsible engineering.
- **Deep Features:** Advanced users are excited by the Supervisor plugin and Session Goals, seeing them as signs of a maturing platform that can handle complex, autonomous workflows.

### 8. Backlog Watch

Several critical and high-severity issues have remained open for extended periods, requiring maintainer action:

1.  **[#54155](https://github.com/openclaw/openclaw/issues/54155) – Gateway Memory Leak (389MB → 14.7GB)**
    - **Status:** Open since March 25, 2026. Labeled `needs-maintainer-review`.
    - **Impact:** A critical stability risk for any long-running deployment. This has been open for over 2 months and should be the top priority for the infrastructure team.

2.  **[#48003](https://github.com/openclaw/openclaw/issues/48003) – Steer Mode does not inject messages mid-turn**
    - **Status:** Open since March 16, 2026.
    - **Impact:** A core feature (`messages.queue.mode: "steer"`) has been broken for over two months. This undermines a key differentiator of the platform.

3.  **[#69208](https://github.com/openclaw/openclaw/issues/69208) – Umbrella: Duplicate Transcript & Replay Bugs**
    - **Status:** Open since April 20, 2026.
    - **Impact:** While sub-issues are being fixed, the umbrella remains open, suggesting the architectural fix is still on the product roadmap.

4.  **[#70903](https://github.com/openclaw/openclaw/issues/70903) – Persistent File-Based Provider Cooldown Blocks Users for Hours After Billing Recovery**
    - **Status:** Open since April 24, 2026. P2.
    - **Impact:** Extremely poor user experience for paying users. If a user tops up their balance immediately after a 402 error, they are still blocked by a cached `disabledUntil` timestamp.

5.  **[#51593](https://github.com/openclaw/openclaw/issues/51593) – Duplicated Tool Call IDs with Kimi in WhatsApp**
    - **Status:** Open since March 21, 2026. P1 labeled with `queueable-fix`.
    - **Impact:** Blocks a popular model/channel combination. The root cause seems understood but continues to languish.

6.  **[#60612](https://github.com/openclaw/openclaw/issues/60612) – Doctor Loops NVM Warning Without Fix**
    - **Status:** Open since April 4, 2026.
    - **Impact:** A constant source of false-positive warnings for NVM users that cannot be resolved without manual intervention, leading to alarm fatigue.

---

## Cross-Ecosystem Comparison

# AI Agent Open-Source Ecosystem Cross-Project Comparison Report
**Date:** 2026-05-29

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape remains intensely dynamic, characterized by a core reference implementation (OpenClaw) in a high-churn stabilization cycle, while a growing cohort of specialized forks and adjacent frameworks aggressively capture distinct market niches. A decisive architectural shift is underway from conversational interfaces toward full-fledged agent operating systems, evidenced by the concurrent focus across projects on credential management, sandboxed execution, multi-agent orchestration, and asynchronous scheduling. Regression fatigue is the dominant user sentiment across the largest projects, creating a bifurcated market where users either tolerate churn for the latest features or gravitate toward more stable, specialized alternatives. The ecosystem is maturing rapidly, with interoperability protocols (MCP, GitAgent, OpenAI-compatible APIs) emerging as the primary battleground for long-term strategic positioning.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Activity Profile |
|---|---|---|---|---|
| **OpenClaw** | 373 | 500 | v2026.5.27 (Stable & Beta) | High-Churn / Regression-Prone |
| **Hermes Agent** | 50 | 50 | v0.15.1 (Hotfix) | Post-Major Release Stabilization |
| **CoPaw** | 40 | 38 | v1.1.9 (Stable) | Feature Polish & Core Bug Fixes |
| **IronClaw** | 33 | 50 | Staging (v0.29.0) | Architectural Refactoring |
| **ZeroClaw** | 20 | 34 | Beta (v0.8.0-b1) | High Tempo / User Friction |
| **PicoClaw** | 6 | 32 | Nightly (v0.2.9) | Moderate Velocity / Stale PRs |
| **NanoBot** | 10 | 20 | None | Healthy / Responsive |
| **NullClaw** | 2 (closed) | 10 (7 merged) | None | Focused Stabilization |
| **NanoClaw** | 5 (active) | ~8 (items) | None | Robust / High Trust |
| **LobsterAI** | 1 (new) | 7 (merged) | None | Feature Dev / Quiet Community |
| **Moltis** | 1 (open) | 4 (merged) | None | Focused Bug Sprint |
| **TinyClaw/ZeptoClaw** | 0 | 0 | N/A | Inactive |

---

## 3. OpenClaw's Position

**Advantages:**
- **Volume & Centrality:** OpenClaw commands an order of magnitude more activity than any peer, serving as the ecosystem's primary proving ground for new architectural concepts (supervisor plugins, multi-slot memory, copilot runtime).
- **Community Trust as Moat:** Despite significant regression churn, the team's rapid hotfix turnaround (v5.27 within 24 hours of v5.26) retains user loyalty and differentiates it from projects with stalled review pipelines.
- **Integration Breadth:** No other project matches OpenClaw's channel coverage or plugin surface area, making it the default choice for users needing maximum reach.

**Technical Vulnerabilities:**
- **High Regression Surface:** The plugin-centric architecture creates systemic fragility. The native hook relay and gateway subsystems have been recurring failure points, eroding confidence in the stable channel.
- **Structural Strain:** The sheer volume of concurrent issues (373) and pull requests (500) suggests the core infrastructure is operating at its capacity limits, with regression density directly correlated to release velocity.
- **Platform Gaps:** Windows beta remains effectively broken for local models (event-loop starvation #86599), creating an opening for competitors targeting specific OS-level improvements.

**Strategic Direction:**
OpenClaw is aggressively pushing the agent capability frontier—session goals, multi-slot memory, remote copilot integration—rather than solely polishing existing channels. This trajectory cements its role as the upstream innovation engine but leaves significant market segments vulnerable to specialized challengers offering higher reliability in narrower domains.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple projects, indicating ecosystem-wide pain points rather than single-vendor concerns.

| Focus Area | Affected Projects | Key Symptoms |
|---|---|---|
| **Provider Resilience & Fallback** | OpenClaw, ZeroClaw, Moltis, CoPaw, NullClaw, LobsterAI | DeepSeek V4 incompatibility (ZeroClaw, OpenClaw), MiniMax tool-loop crashes (Moltis, OpenClaw, NullClaw), demand for automatic model failover (CoPaw, LobsterAI) |
| **Memory & Context Architecture** | OpenClaw, NanoBot, CoPaw, ZeroClaw | Short-term memory loss (NanoBot, CoPaw), context window blowup from shell output (CoPaw), multi-slot composition vs. information accumulation models (OpenClaw, CoPaw) |
| **Security & Access Control** | IronClaw, ZeroClaw, NullClaw, NanoClaw, OpenClaw | Credential injection architecture (IronClaw), sandbox policy enforcement (ZeroClaw), config parsing auditability (NullClaw), symlink confinement for attachments (NanoClaw) |
| **Channel Reliability & Parity** | OpenClaw, NanoClaw, NullClaw, Moltis, Hermes | Telegram reply loops & draft spam (OpenClaw, NullClaw), WhatsApp session persistence (NanoClaw), Matrix E2EE verification (NanoBot), Discord voice drops (Moltis) |
| **Async & Agent Autonomy** | NullClaw, ZeroClaw, LobsterAI, OpenClaw, Moltis | Cron engine re-architecture (all major projects), agent self-modification (NanoClaw), email triggers (LobsterAI), terminal/PTY control (Moltis, ZeroClaw) |

---

## 5. Differentiation Analysis

| Differentiation Axis | Lead Project(s) | Key Distinctions |
|---|---|---|
| **Core Upstream Architecture** | OpenClaw | Broadest integration; sets the ecosystem agenda; highest churn tolerance expected of users |
| **Multi-Agent Orchestration** | Hermes Agent, NanoBot | Swarm/Kanban (Hermes), Agent Collaboration Bus (NanoBot); targeting enterprise workflows |
| **Developer Terminal Workflows** | ZeroClaw, Moltis, NanoClaw | TUI/RPC (ZeroClaw), PTY control (Moltis), self-modifying agent bridge (NanoClaw) |
| **Decentralized / Verifiable Compute** | IronClaw | NEAR ecosystem, TEE integration, credential broker architecture |
| **Chinese Consumer Ecosystem** | CoPaw, LobsterAI | Qwen integration, Kit/Expert Store, WeChat/Feishu native; distinct user culture |
| **Embedded / Edge Deployment** | PicoClaw | RISC-V support, minimal footprint; first-mover advantage in edge hardware |
| **Channel Reliability Platforms** | NullClaw, Moltis | Lowest regression rates; best for bot operators prioritizing uptime over feature breadth |

---

## 6. Community Momentum & Maturity

**Tier 1: High-Velocity Hubs (Critical Mass, Structural Churn)**
OpenClaw, Hermes Agent, IronClaw, ZeroClaw. These projects attract the majority of developer mindshare and define the ecosystem's technical agenda. They operate under constant "release early, hotfix now" pressure. Users are effectively beta testers, and community engagement correlates directly with maintainer responsiveness to regressions. These projects are best suited for early adopters and developers building on the leading edge.

**Tier 2: Specialty Contenders (High Signal, Lower Noise)**
NanoBot, CoPaw, NullClaw, Moltis. These projects demonstrate strong execution within well-defined scopes. They exhibit lower regression rates and higher community trust per unit of activity. Their user bases are more forgiving and more deeply invested in the specific value proposition. Ideal for production users who can sacrifice breadth for reliability.

**Tier 3: Niche Scoping (Positive but Paced)**
PicoClaw, LobsterAI, NanoClaw. Focused on specific hardware, platforms, or architectural features. These projects benefit from dedicated community niches but face review bottlenecks that slow feature absorption. Their trajectory depends on maintainer bandwidth allocation and the ability to clear stale PR backlogs.

**Tier 4: Inactive / Stalled**
TinyClaw, ZeptoClaw. No observable development momentum. These projects risk losing relevance unless they attract renewed maintainer attention or community-driven forks.

---

## 7. Trend Signals

**1. The "Regime of High-Velocity Churn" is Normalized**
The ecosystem has structurally adapted to a release cadence that prioritizes speed over stability, with hotfixes becoming the primary delivery mechanism for quality. Projects that fail to match this pace (accumulating stale PRs, delayed releases) lose developer mindshare rapidly. This creates a natural segmentation: innovators accept churn for features; pragmatists gravitate to stabilized forks or specialized projects.

**2. Standardization of Agent Interfaces is Accelerating**
Interoperability protocols (MCP, OpenAI-compatible APIs, GitAgent Protocol, Codex harness) are emerging as the strategic differentiator. Projects that act as bridges between standards (PicoClaw's OpenAI API channel, OpenClaw's Codex integration, NanoBot's GitAgent compliance) gain outsized strategic value. The ecosystem is rejecting fully proprietary integration models.

**3. Infrastructure is the New Battleground**
LLM integration is commoditizing. Differentiation has shifted to the operating environment: permission models (ZeroClaw's `DenyWithEdit`), credential hygiene (IronClaw's credential broker), state management (OpenClaw's multi-slot memory), and scheduling (LobsterAI's email triggers, NullClaw's cron subagent). The winners will be those who make agents safe and reliable to operate at scale, not just smarter in conversation.

**4. The "Non-Chat" Agent Interface is Ascending**
Users increasingly demand agents that operate as daemons, cron jobs, terminal utilities, or API endpoints. The chatbot is becoming one delivery channel among many. Projects with robust backend architectures (ZeroClaw's TUI/RPC, Moltis's PTY support, LobsterAI's Gmail trigger) are better positioned than those focused solely on UI polish.

**5. Credential & Secrets Management is the Unresolved UX Bottleneck**
The consistent emergence of credential injection, lifecycle management, and proxying as a top-tier pain point across IronClaw (PathPlaceholder security review), ZeroClaw (token invalidation), and NanoClaw (OneCLI credential injection) signals a critical architectural gap. Solving secrets management reliably is likely the single highest-leverage investment for enabling production enterprise deployment across the ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the structured NanoBot project digest for the activity window ending May 29, 2026.

---

## NanoBot Project Digest — 2026-05-29

### 1. Today's Overview
NanoBot saw very high development throughput over the past 24 hours, with 20 updated pull requests and 10 updated issues. Activity was heavily focused on correcting a cluster of concurrency and context-budget bugs, while continuing to push ambitious architectural features. The rapid identification and patching of the hamb1y bug cluster signal a healthy, responsive maintenance cycle. Alongside stability work, the project advanced its ecosystem play with WebUI workspaces, GitAgent Protocol compliance, and an extension registry, suggesting the project is maturing from a single-bot framework into a platform for multi-agent orchestration.

### 2. Releases
No new formal releases were published in this window.

### 3. Project Progress
Eight pull requests were merged or closed today:

- **Concurrency Bugfix Bundle ([#4041](https://github.com/HKUDS/nanobot/pull/4041))**: A comprehensive fix resolving five open issues (#4036–#4040) covering session queue overwrites, shared mutable request context in goals, streaming delta duplication during retries, context sniffing token budgets, and `/stop` failures under unified sessions.
- **WebUI Workspaces & Access Control ([#4007](https://github.com/HKUDS/nanobot/pull/4007))**: Introduced Codex-style project workspaces that bind chat scopes to project folders, plus composer access controls anchored to the active project.
- **Agent Self-Correction Loop ([#4015](https://github.com/HKUDS/nanobot/pull/4015))**: Added an observation-reflection prompt cycle that allows the agent to "think, verify, update user, act" after tool executions.
- **AUTHORITY.md Bootstrap ([#4032](https://github.com/HKUDS/nanobot/pull/4032))**: Added an optional high-priority moral/behavioral authority file injected at the very top of the system prompt.
- **Execute Confirmation ([#3937](https://github.com/HKUDS/nanobot/pull/3937))**: Merged a user confirmation gate for dangerous shell commands.
- **Discord `/model` Command ([#4031](https://github.com/HKUDS/nanobot/pull/4031))**: Native slash command for switching runtime model presets.
- **Heartbeat Refactor ([#4023](https://github.com/HKUDS/nanobot/pull/4023))**: Migrated the standalone heartbeat service into an auto-registered cron job.
- **GitAgent Protocol - Merged ([#4034](https://github.com/HKUDS/nanobot/pull/4034) / [#4030](https://github.com/HKUDS/nanobot/pull/4030))**: Support for the portable GitAgent standard (`agent.yaml` + `SOUL.md`).

### 4. Community Hot Topics
- **`nanobot-webui` Ecosystem Tool ([#1922](https://github.com/HKUDS/nanobot/issues/1922))**: This community-built self-hosted management panel generated the most engagement (12 comments, 10 👍). The strong reaction indicates high demand for visual administration, provider configuration, and multi-user support.
- **Short-Term Memory Loss ([#4044](https://github.com/HKUDS/nanobot/issues/4044))**: This open bug report garnered 3 comments with deep debate on root causes—likely context window pressure or system prompt injection conflicts. It reflects a critical UX pain point for users expecting coherent long-form conversations.
- **WebUI Workspaces ([#4007](https://github.com/HKUDS/nanobot/pull/4007))**: The merge of project workspaces was a highly anticipated feature, drawing attention from users needing persistent chat-to-codebase binding.

### 5. Bugs & Stability
- **Critical**: **Short-term memory loss** ([#4044](https://github.com/HKUDS/nanobot/issues/4044)) remains open with no assigned resolver. The conversation "snaps" between turns. Root cause is actively debated.
- **Critical**: **MCP Reconnection Dead Session** ([#4027](https://github.com/HKUDS/nanobot/pull/4027)): An open PR fixes a bug where `_mcp_connected` is never reset, permanently blocking reconnection. This is a blocking bug for users relying on MCP tools.
- **High**: **Matrix E2EE Verification Block** ([#4042](https://github.com/HKUDS/nanobot/issues/4042)): The bot cannot clear the "unverified device" warning on Element X, making E2EE rooms non-functional for Rust-based clients.
- **High (Security)**: **MS Teams Service URL Spoofing** ([#4047](https://github.com/HKUDS/nanobot/pull/4047)): Open PR to stop trusting arbitrary `serviceUrl` values in Bot Framework replies.
- **Resolved**: The **Hamb1y Concurrency Cluster** (#4036–#4040) was fully fixed in Pull Request [#4041](https://github.com/HKUDS/nanobot/pull/4041), resolving critical race conditions in streaming, session locking, and context budgeting.

### 6. Feature Requests & Roadmap Signals
The roadmap is clearly pivoting toward a **multi-agent, extensible platform**:

- **Agent Collaboration Bus ([#3992](https://github.com/HKUDS/nanobot/pull/3992))**: This open PR allows multiple running agent instances to communicate via a shared message bus. If merged, it is the anchor feature for the next major version.
- **Extension Registry ([#4046](https://github.com/HKUDS/nanobot/pull/4046))**: An open PR adding an external registry for apps/skills, foreshadowing a community plugin marketplace.
- **GitAgent Protocol ([#4034](https://github.com/HKUDS/nanobot/pull/4034))**: Already merged, aligning NanoBot with the open standard for portable agents.
- **User-Requested Config**: Users are demanding fine-grained control over behavior. The most requested features today are **configurable document extraction** ([#4043](https://github.com/HKUDS/nanobot/issues/4043)) and **improved memory control** ([#4044](https://github.com/HKUDS/nanobot/issues/4044)).
- **Provider Compatibility**: The open PR for parsing text-format `tool_calls` ([#4017](https://github.com/HKUDS/nanobot/pull/4017)) signals ongoing work to support non-standard OpenAI-compatible providers (specifically Xiaomi MiMo).

### 7. User Feedback Summary
Satisfaction remains high regarding **development velocity** and **bugfix turnaround**, evidenced by the immediate merging of the #4041 fix bundle. The ecosystem is thriving, with a user building a dedicated management UI ([#1922](https://github.com/HKUDS/nanobot/issues/1922)) before the official one was fully mature.

Primary pain points today center on **reliability and transparency**:
- **Memory snap** is the single most frustrating user experience reported.
- **MCP session drops** force users to restart the agent.
- **Provider arrearage errors** were previously opaque; an open PR ([#4048](https://github.com/HKUDS/nanobot/pull/4048)) finally surfaces these clearly to users.
- **WeChat message limits** ([#2772](https://github.com/HKUDS/nanobot/issues/2772)) remain a constraint for users on that channel.

### 8. Backlog Watch
Several high-impact items need maintainer attention:

- **Agent Collaboration PR ([#3992](https://github.com/HKUDS/nanobot/pull/3992))**: Open since May 24. This is a massive architectural feature that requires substantial review bandwidth. It is the most significant open pull request.
- **MCP Reconnection Fix ([#4027](https://github.com/HKUDS/nanobot/pull/4027))**: A high-priority bugfix for an ongoing reliability issue. Awaiting merge.
- **Memory Loss Issue ([#4044](https://github.com/HKUDS/nanobot/issues/4044))**: Has active discussion but lacks a definitive root cause statement or assignee. Needs triage.
- **Good First Issue: Document Extraction Config ([#4043](https://github.com/HKUDS/nanobot/issues/4043))**: This is a low-complexity, high-value UX improvement that is ready for a new contributor. Maintainers could accelerate adoption by linking this to new developers.
- **Matrix E2EE Fix ([#4042](https://github.com/HKUDS/nanobot/issues/4042))**: Tagged as `good first issue`, but the technical depth (Matrix crypto SDK) may require a senior contributor to design the initial approach.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent Project Digest
**Date:** 2026-05-29

---

### 1. Today’s Overview

May 29, 2026, was a high-stakes stabilization day following the landmark **v0.15.0 “Velocity Release”** on May 28. A critical dashboard regression—an infinite reload loop in loopback mode—triggered an immediate same-day hotfix (**v0.15.1**), showcasing strong operational responsiveness. Community activity remained intense, with **50 issues** and **50 PRs** updated, the vast majority driven by bug reports, regressions, and targeted patches from the post-release wave. The project is firmly in patch-and-polish mode, balancing high user engagement with the operational costs of a massive feature drop.

---

### 2. Releases

**v2026.5.29 (v0.15.1) — The Patch Release**
*(Hotfix, same day as v0.15.0)*
- **28 commits**, **21 merged PRs**, **9 contributors**
- **Headline fix:** Resolved a critical SPA infinite reload loop (`GET /api/auth/me` returning 401 in loopback/insecure mode) that rendered the dashboard completely unusable for non-OAuth users. This was the single most impactful issue of the day, with multiple duplicate reports (#34206, #34202, #34289).
- **Significance:** The rapid turnaround (v0.15.0 → v0.15.1 in <24h) signals a mature incident response protocol. Users should upgrade immediately if they run dashboard in `--insecure` mode.
- **Links:** [Release v2026.5.29](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.5.29)

**v2026.5.28 (v0.15.0) — The Velocity Release**
*(Released yesterday, context for today’s events)*
- **1,302 commits**, **747 merged PRs**, **321 community contributors**
- Closed **560+ issues** (15 P0, 65 P1, 19 security-tagged).
- Introduced the Kanban rewrite, new gateway infrastructure, and TUX enhancements—along with the auth regression fixed today.
- **Link:** [Release v2026.5.28](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.5.28)

---

### 3. Project Progress

Today’s **11 merged/closed PRs** were overwhelmingly corrective and infrastructural:

| Merged PR | Scope |
|---|---|
| [#34288](https://github.com/NousResearch/hermes-agent/pull/34288) | *feat(dobby): package productization slice* — Internal platform packaging for the “Dobby” runtime module. |
| [#33724](https://github.com/NousResearch/hermes-agent/pull/33724) | *fix(gateway)* — Telegram gateway now correctly sets `final_content_delivered=True` on all exit paths, preventing duplicate fallback messages. |
| [#33730](https://github.com/NousResearch/hermes-agent/pull/33730) | *fix(cli)* — Resolved truncation of the Identifier column in `hermes skills search`, a critical fix for skill installation. Added `--json` flag. |
| [#27115](https://github.com/NousResearch/hermes-agent/pull/27115) | *fix(docker)* — Baked `messaging` extras (Telegram, Discord, Slack deps) into the Docker image, fixing a regression where containers lacked runtime dependencies. |

**Notable Open PR Activity:**
A massive batch of **9 interlocking PRs** from contributor `Kyzcreig` entered the open queue today, targeting the auxiliary client, model resolver, and provider validation layer ([#34291](https://github.com/NousResearch/hermes-agent/pull/34291) to [#34299](https://github.com/NousResearch/hermes-agent/pull/34299)). These address deeply rooted issues around provider profile shadowing, schema validation, context-compressor refusal handling, and inline model switching. This batch suggests a planned major hardening of the configuration pipeline in the coming days.

---

### 4. Community Hot Topics

| Issue | Title | Engagement | Analysis |
|---|---|---|---|
| [#18080](https://github.com/NousResearch/hermes-agent/issues/18080) | [Feature]: Improved Themes for Dashboard | **31 👍 / 20 💬** | Persistent demand for richer UI customization; current themes criticized for low contrast and non-standard fonts. |
| [#34206](https://github.com/NousResearch/hermes-agent/issues/34206) | Dashboard infinite reload loop (Auth) | Multiple duplicates, immediate hotfix | The dominant topic of the day. Engendered an immediate community-maintainer feedback loop that resulted in the v0.15.1 hotfix. |
| [#32729](https://github.com/NousResearch/hermes-agent/issues/32729) | Auxiliary title generation timeout ignores config | **5 💬** | Configuration trust issue: users set `auxiliary.title_generation.timeout` but observe no effect. Undermines config reliability perception. |
| [#24329](https://github.com/NousResearch/hermes-agent/issues/24329) | Kanban: surface non-runnable ready tasks | **4 💬** | Power users hitting Kanban visibility limits; requests for stronger runnable-state validation. |
| [#28505](https://github.com/NousResearch/hermes-agent/issues/28505) | Bundle llms-full.txt as a built-in self-doc skill | **P3, strong concept** | Community recognizes the agent needs to understand its own tools better to reduce hallucination. Low-cost, high-value request. |

---

### 5. Bugs & Stability

A large volume of high-quality bug reports came in today, typical for a major release week. The hotfix resolved the most critical item; remaining issues span a wide range of subsystems.

**Critical (Patched in v0.15.1)**
- **Dashboard Auth Loop:** Multiple reports ([#34206](https://github.com/NousResearch/hermes-agent/issues/34206), [#34202](https://github.com/NousResearch/hermes-agent/issues/34202), [#34289](https://github.com/NousResearch/hermes-agent/issues/34289)) — SPA frontend enters ~500ms reload loop due to unhandled 401 on `/api/auth/me` in loopback mode. Fully resolved in v0.15.1.

**High (P1–P2)**
- **Docker TUI Broken** ([#34091](https://github.com/NousResearch/hermes-agent/issues/34091), P1): Dashboard v0.15.0 in Docker shows “events feed disconnected” error. No PR linked yet.
- **Cross-Filesystem Symlink EXDEV** ([#34252](https://github.com/NousResearch/hermes-agent/issues/34252), P2): `atomic_replace()` crashes when `HERMES_HOME` is a symlink across mount points. Impairs users with networked homes.
- **CLI NameError on MCP commands** ([#34220](https://github.com/NousResearch/hermes-agent/issues/34220), P2): `hermes mcp add` crashes with `NameError` if the `mcp` Python package is absent. Dependency error handling gap.
- **Feishu Session Blocker** ([#34253](https://github.com/NousResearch/hermes-agent/issues/34253), P2): Cancelling a Feishu DM session orphans the session guard, permanently blocking subsequent messages.
- **Cost Overestimate 1,000,000x** ([#34256](https://github.com/NousResearch/hermes-agent/issues/34256), P2): Pricing-unit mismatch on Crof custom endpoints records impossible costs ($555 for 13k tokens). Financial tracking UX broken.
- **WebSocket Rejection** ([#33265](https://github.com/NousResearch/hermes-agent/issues/33265), P2): TUI silently drops non-localhost WebSocket connections even with `--host 0.0.0.0`. Blocks LAN/Accessible setups.

**Moderate (P3)**
- **Codex OAuth TypeError** ([#34124](https://github.com/NousResearch/hermes-agent/issues/34124)): `‘NoneType’ object is not iterable` on every turn through `openai-codex`. Non-retryable fallback failure.
- **Honcho Memory Hang** ([#34070](https://github.com/NousResearch/hermes-agent/issues/34070)): Fresh CLI subprocesses hang in cold-start memory prefetch. Breaks cron/Paperclip dispatchers using Honcho.
- **SearXNG Env Ignored** ([#34290](https://github.com/NousResearch/hermes-agent/issues/34290)): Provider reads `SEARXNG_URL` from raw process env instead of Hermes’ config-aware env lookup.
- **Slack/Cron Codex Failure** ([#33976](https://github.com/NousResearch/hermes-agent/issues/33976)): Codex backend returning `response.output=None` with HTTP 200 causes non-recoverable Slack gateway failures.

---

### 6. Feature Requests & Roadmap Signals

**Strong Short-Term Candidates:**
- **Swarm Customization** ([#34273](https://github.com/NousResearch/hermes-agent/issues/34273)): Request to expose `verifier` and `synthesizer` task bodies and skills in `hermes kanban swarm`. Indicates advanced users need to customize the multi-agent loop. Likely to be fast-tracked given the momentum of the Kyzcreig PR batch on the agent core.
- **Self-Documenting Agent** ([#28505](https://github.com/NousResearch/hermes-agent/issues/28505)): Bundling `llms-full.txt` as a built-in skill would directly reduce hallucination of Hermes commands—a common failure mode. Low implementation risk, high user trust ROI.

**Growing Ecosystem Demand:**
- **Third-Party Provider Recognition** ([#34271](https://github.com/NousResearch/hermes-agent/issues/34271)): Request to promote Mnemosyne to official memory provider docs. Signals a maturing plugin ecosystem seeking formal marketplace/marketing support.
- **Granular Kanban Controls** ([#24329](https://github.com/NousResearch/hermes-agent/issues/24329), [#21582](https://github.com/NousResearch/hermes-agent/issues/21582)): Users want per-profile concurrency limits and visibility into non-runnable tasks. Enterprise use-case signals.

**UI/UX:**
- The **Themes request** ([#18080](https://github.com/NousResearch/hermes-agent/issues/18080), 31 👍) continues to accumulate support but lacks a maintainer commitment. It may move up the backlog if the dashboard stabilization allows UI development bandwidth.

---

### 7. User Feedback Summary

**Satisfaction Drivers:**
- **Responsiveness:** The same-day hotfix for the auth loop was widely noted. Users feel heard when critical regressions are addressed within hours.
- **Ambition:** The scale of v0.15.0 is appreciated. Users recognize the project is pushing hard on multi-agent systems, gateways, and platform extensibility.

**Pain Points (Implicit & Explicit):**
- **“We are beta testers” sentiment:** The density of P2 regressions (Docker, auth, WebSocket, Feishu, pricing) post-v0.15.0 suggests the Velocity Release model imposes a QA tax on the user base. Several reports express frustration at broken workflows that worked in v0.14.0.
- **Config trust eroding:** Issues like [#32729](https://github.com/NousResearch/hermes-agent/issues/32729) (timeouts ignored), [#34290](https://github.com/NousResearch/hermes-agent/issues/34290) (env vars ignored), and [#34252](https://github.com/NousResearch/hermes-agent/issues/34252) (symlinks ignored) chip away at confidence that configuration is consistently respected.
- **Provider lock-in friction:** Users switching between providers (Codex, xAI, OpenAI) consistently hit integration-level issues ([#34205](https://github.com/NousResearch/hermes-agent/issues/34205), [#34124](https://github.com/NousResearch/hermes-agent/issues/34124), [#33976](https://github.com/NousResearch/hermes-agent/issues/33976)). The gap between Hermes’ provider-agnostic ideal and actual backend behavior is a recurring source of friction.

**Notable Voice:**
> *“After updating to v0.15.0, I cannot use my TUI in the dashboard. In v0.14.0, access was still normal.”* — [#34091](https://github.com/NousResearch/hermes-agent/issues/34091)
> *“The dashboard frontend calls getAuthMe() → GET /api/auth/me. It gets back 401 Unauthorized every single time. The error-handling code treats this as a ‘stale token / auth failure’ and immediately retries (or triggers a full page reload).”* — [#34206](https://github.com/NousResearch/hermes-agent/issues/34206)

---

### 8. Backlog Watch

The following issues and PRs represent the oldest active items requiring maintainer decision or closure:

**Oldest Open Bug/Support:**
- **[#13849](https://github.com/NousResearch/hermes-agent/issues/13849)** (Apr 22, 2026): User unable to use models from the 9router provider. Config wizard and manual YAML editing both fail. No actionable maintainer response in >5 weeks. Highlights the custom provider onboarding friction point.

**Stalled High-Impact PR:**
- **[#14470](https://github.com/NousResearch/hermes-agent/pull/14470)** (Apr 23, 2026): Adds `per-provider model_validate` option to skip model name validation for custom endpoints. Directly addresses the class of problem in #13849. Awaiting review/merge for >5 weeks.

**Lingering Feature/Large PR:**
- **[#25345](https://github.com/NousResearch/hermes-agent/pull/25345)** (May 14, 2026): Fixes Android local HTML browser handoff. A significant UX gap for mobile users that remains unintegrated.
- **[#21797](https://github.com/NousResearch/hermes-agent/pull/21797)** (May 8, 2026): Prevents gateway from sending bogus `MEDIA:` placeholder paths as real attachments. Small security/safety fix that has been open for 3 weeks.

**Trend:** The backlog is relatively short, indicating a team with high merge throughput. However, the >5 week wait on the provider validation fix (#14470) is a notable gap given how many daily bug reports trace back to custom provider issues (#13849, #34256, #34205).

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for May 29, 2026, based on the latest GitHub activity.

---

## PicoClaw Project Digest – 2026-05-29

### 1. Today’s Overview

PicoClaw saw a surge of activity today, clocking 32 updated Pull Requests, 6 updated Issues, and a new nightly release. A significant portion of PR traffic comes from automated dependency updates, but the project also advanced several substantive features, including an image compression pipeline for vision models and a new NEAR AI Cloud provider. Importantly, the long-standing **OpenAI API Channel feature request (#1738)** was finally closed, marking a major integration milestone. However, a critical platform bug on RISC-V (#2887) remains the most discussed open topic, and a pile-up of `stale`-labeled PRs from recent weeks signals a need for maintainer triage.

### 2. Releases

- **Nightly Build: `v0.2.9-nightly.20260529.85751492`**
  This is an automated build tracking the `main` branch. It includes all changes merged since the last stable `v0.2.9` release but is flagged as potentially unstable. No breaking changes or formal migration notes were published.
  **Full Changelog:** [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

### 3. Project Progress

Nine PRs were closed or merged today. The headline achievement is the closure of **[Feature]  Add OpenAI API channel support (#1738)** (sipeed/picoclaw Issue #1738), a highly requested integration feature opened back in March that allows external systems to call Picoclaw via a standard OpenAI-compatible API. The maintainers also closed several issues, including the **[Extend message tool](#2855)** feature request and the **FUNDING.yml suggestion (#2912)**.

On the feature frontier, several promising PRs are pending:
- **Inbound Image Compression (#2964):** Submitted by `afjcjsbx`, this adds a configurable multi-level compression policy for images before building the model payload, reducing token costs for vision pipelines.
- **NEAR AI Cloud Provider (#2917):** Authored by `PierreLeGuen`, this introduces first-class support for NEAR AI Cloud.
- **MiMo CommonModels (#2915):** `SiYue-ZO` added default model recommendations (`mimo-v2.5`) to improve WebUI model selection UX.

A set of important code quality fixes for the JSONL memory store by `SiYue-ZO` (#2907, #2913) remain open but are actively updated, indicating ongoing work on memory persistence and crash recovery.

### 4. Community Hot Topics

- **[BUG] .deb version on RISC-V is not functional with OpenAI model (#2887)** (sipeed/picoclaw Issue #2887)
  The most active discussion of the week, with 7 comments. A user reports that the pre-packaged `.deb` for RISC-V architecture cannot connect to OpenAI models (specifically `gpt-5.4-2026-03-05`), rendering the platform unusable on that hardware.

- **[Feature] Add OpenAI API channel support (#1738)** (sipeed/picoclaw Issue #1738)
  While now closed, this issue generated 3 comments and a 👍. The community clearly needed this for embedding Picoclaw into existing toolchains, and its closure removes a major integration barrier.

- **CPU, Memory and IO optimizations (#2916)** (sipeed/picoclaw Issue #2916)
  This open request for deep performance optimization has attracted 3 comments. The author has done substantial codebase analysis, signaling a latent demand for lower resource usage in production deployments.

### 5. Bugs & Stability

- **Critical — [BUG] RISC-V .deb incompatible with OpenAI (#2887)**
  No fix PR has been linked to this issue yet. This is a platform-level blocking bug for the RISC-V community.

- **High — `exec` tool workspace guard breaks scheme-less URLs (PR #2965)** (sipeed/picoclaw PR #2965)
  Submitted by `maxmilian`, this fix addresses a flaw where the `exec` tool’s `restrict_to_workspace` guard misreads URLs like `curl -s "wttr.in/Beijing"` as absolute paths, blocking legitimate commands. A fix is available for review.

- **Medium — JSONL memory store crash consistency gaps (PR #2907, #2913)**
  Two PRs from `SiYue-ZO` address race conditions and metadata drift in `pkg/memory`. If the process crashes between appending to the JSONL file and writing the metadata index, data loss can occur. These remain open but tagged as `stale`.

- **Fixed — Termux X509 certificate error (#2944)**
  Correctly resolved by explicitly setting the `SSL_CERT_FILE` environment variable, closing the loop for mobile/terminal users.

### 6. Feature Requests & Roadmap Signals

The closure of the **OpenAI API Channel (#1738)** strongly suggests it will be part of the next stable release, fulfilling a core integration workflow. The pipeline for version `0.3.0` (or the next stable cut) appears to be shaping up around multimodal efficiency and provider breadth:

- **Image Input Compression (#2964):** This is a strong candidate for merging soon, as it directly enables richer agent capabilities (vision) without driving up API costs.
- **NEAR AI Cloud (#2917) & MiMo Models (#2915):** These reflect a roadmap priority on expanding the model ecosystem beyond the usual big providers, particularly into TEE-capable and decentralized AI compute.
- The quick closure of the **FUNDING.yml request (#2912)** shows maintainers are responsive to community health suggestions, which is a positive signal for project sustainability.

### 7. User Feedback Summary

User sentiment is mixed, revealing a project growing rapidly but bumping against platform edges.

- **Pain Points:**
    - **RISC-V users** are effectively blocked from using OpenAI models (#2887).
    - **Termux users** hit SSL configuration issues (#2944), which have since been resolved.
    - **Power users** deploying `restrict_to_workspace` security policies found it broke valid `curl` commands (#2965).
- **Satisfaction Signals:**
    - The **OpenAI API channel closure** satisfies a large cohort of users wanting to embed Picoclaw.
    - The immediate adoption of the **FUNDING.yml suggestion** demonstrates a welcoming maintainer attitude toward low-friction community asks.

### 8. Backlog Watch

A cluster of high-quality manual PRs from the last ten days has accumulated under the `stale` label and requires maintainer attention to avoid drift:

- **Fixes:**
    - `fix(web): restore provider logo fallbacks (#2908)` (sipeed/picoclaw PR #2908)
    - `Fix JSONL store metadata drift after crash (#2907)` (sipeed/picoclaw PR #2907)
    - `Fix JSONL session index hot-path cloning (#2913)` (sipeed/picoclaw PR #2913)
- **Features:**
    - `feat(provider): add NEAR AI Cloud provider (#2917)` (sipeed/picoclaw PR #2917)
    - `feat(providers): add CommonModels for MiMo provider (#2915)` (sipeed/picoclaw PR #2915)

If left unchecked, these PRs will require significant rebasing. A dedicated triage session by the core maintainers to push these over the finish line would significantly improve project velocity and contributor morale. Similarly, a large stack of **Dependabot dependency bumps** (#2918, #2919, #2920, #2922, #2924, #2925, #2926, #2927) are also sitting stale, which could eventually lead to security gaps if neglected.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-29

## 1. Today's Overview
The project experienced a surge in activity with 12 items updated in the last 24 hours, comprising 4 merged/closed pull requests and 1 closed issue from 5 active issues. Development centered on internal SDK upgrades, extending autonomous agent capabilities, and addressing structural reliability bugs across WhatsApp, iOS, and database delivery channels. The long-awaited closure of Issue #80 (cross-provider support) signals a potential strategic shift away from full Anthropic dependency, while several fresh bug reports indicate the project is being tested at scale by its community. Overall project health remains robust, driven by a highly technical contributor base submitting sophisticated features and sharp bug reports.

## 2. Releases
*No new releases were published today.* The current stable version remains unchanged. Infrastructure bumps to `claude-code` 2.1.154 and `claude-agent-sdk` 0.3.154 were merged via PR #2637 and are expected to be included in the next release cycle.

## 3. Project Progress — Merged/Closed PRs Today
Four pull requests advanced to completion:

- **[PR #2639](https://github.com/nanocoai/nanoclaw/pull/2639) — iOS reliability**  
  General UI and infrastructure fixes for iOS deployments. Merged.

- **[PR #2637](https://github.com/nanocoai/nanoclaw/pull/2637) — SDK bump (claude-code 2.1.154, claude-agent-sdk 0.3.154)**  
  Major internal dependency update. The 0.3 major SDK shift moved `@anthropic-ai/sdk` and `@modelcontextprotocol/sdk` to peer dependencies, requiring explicit declaration of `@anthropic-ai/sdk ^0.100.0` and upgrade of `@modelcontextprotocol/sdk` to `^1.29.0`.

- **[PR #2635](https://github.com/nanocoai/nanoclaw/pull/2635) — feat(self-mod): patch_bridge**  
  Extends the self-mod approval framework with a third action (`patch_bridge`) allowing agents (currently Pero) to propose and apply patches to the host-side `taskosaur-mcp` bridge without manual operator intervention. A significant autonomy milestone for the agent runtime.

- **[PR #102](https://github.com/nanocoai/nanoclaw/pull/102) — Notion integration skill**  
  Merged after a ~4-month lifecycle. Adds an official skill for Notion API integration via MCP server, enabling agents to read, create, and update Notion pages and databases.

## 4. Community Hot Topics

- **[Issue #80](https://github.com/nanocoai/nanoclaw/issues/80) — Support runtimes other than Claude/Anthropic**  
  *Status: CLOSED* | 34 Comments | 60 👍  
  The most resonant community item. The author explicitly cited Anthropic shutting down subscriptions for OpenClaw usage. The closure of this issue (without a clear published commitment) suggests internal deliberation or a shift to a private roadmap, but the underlying demand for OpenCode, Gemini, and Codex support remains the highest-signal feature request in the project's history.

- **[Issue #2632](https://github.com/nanocoai/nanoclaw/issues/2632) — Clarify status of Telegram agent-swarm / multi-bot identity in v2**  
  *Status: OPEN* | 0 Comments (no maintainer response)  
  A user attempting v1-to-v2 migration reports the Telegram swarm feature's status is ambiguous. The repo has implementation artifacts but no clear guidance. This is a blocking issue for Telegram-centric installations.

- **[Issue #2638](https://github.com/nanocoai/nanoclaw/issues/2638) — engage_mode=mention engages on every WhatsApp 1-on-1 message**  
  *Status: OPEN* | Filed yesterday  
  Community members identified that `mention` mode misclassifies 1-on-1 chats between two humans (with the bot as a third party) as DMs, causing unwanted engagement. Points to a structural gap in WhatsApp channel routing logic.

## 5. Bugs & Stability

| Bug | Severity | Status | Description |
|---|---|---|---|
| **[Issue #2640](https://github.com/nanocoai/nanoclaw/issues/2640)** | High | Open, no fix PR | Race condition in `src/delivery.ts`: readonly polls every 1000ms on `outbound.db` clash with `journal_mode=DELETE` transactions (1–5ms), emitting `SQLITE_READONLY_ROLLBACK` errors under load. |
| **[Issue #2638](https://github.com/nanocoai/nanoclaw/issues/2638)** | Medium | Open, no fix PR | WhatsApp `engage_mode=mention` fires on all 1-on-1 human chats, not just bot DMs. Incorrect routing for group/direct message classification. |
| **[PR #2633](https://github.com/nanocoai/nanoclaw/pull/2633)** | Critical (WhatsApp) | Open, fix proposed | Two structural bugs in `src/channels/whatsapp.ts` on Baileys 7.x: the adapter self-destructs its own OAuth session and wipes auth on shutdown. A targeted fix is under review. |
| **[PR #2630](https://github.com/nanocoai/nanoclaw/pull/2630)** | High (Security) | Open, fix proposed | Session manager hardening to prevent writing through symlinked `inbox` roots. Extends previous path-unsafe hardening to channel-inbound attachment extraction and agent-to-agent file forwarding. |

## 6. Feature Requests & Roadmap Signals

- **Cross-Provider Runtime Support** (Issue #80, closed): The project's most visible feature gap. Expect this to become a foundational capability in a future major version as dependency on a single provider is increasingly seen as a risk by the community.

- **OneCLI Credential Injection into MCP Servers** ([Issue #2636](https://github.com/nanocoai/nanoclaw/issues/2636)): Requests that `"env": {"SOME_API_KEY": "onecli-managed"}` in `McpServerConfig` be resolved at runtime rather than passed literally to external APIs. Signals growing enterprise usage needing credential proxying.

- **AWS Credential Proxy Integration** ([PR #2634](https://github.com/nanocoai/nanoclaw/pull/2634)): Adds an operator skill for paws4claws, an AWS credential proxy daemon. Supports mounting via the "mount-from-outside" pattern. Indicates community demand for secure cloud infrastructure access from within agent runtimes.

- **Self-Modifying Agent Infrastructure** (PR #2635, merged): The `patch_bridge` capability is a clear roadmap signal that the project is investing heavily in agent autonomy—enabling agents to fix bugs and add tools to the host bridge without human intervention.

- **Telegram Swarm Migration Path** (Issue #2632): A v2 roadmap decision that needs explicit communication from maintainers, as it risks alienating a segment of the user base.

## 7. User Feedback Summary

**Pain Points:**
- **Provider Risk:** Users express anxiety about Anthropic policy changes, with one user reporting subscription termination for OpenClaw usage (Issue #80). The community is actively seeking escape hatches from full Anthropic dependency.
- **Migration Friction:** Migration from v1 to v2 is unclear for advanced features like Telegram swarms (Issue #2632), causing user frustration and migration planning paralysis.
- **Channel Reliability:** WhatsApp integration is the most commonly cited stability pain point, with bugs spanning session persistence (PR #2633) and engagement routing (Issue #2638).
- **Runtime Noise:** At scale, users are seeing persistent error logs from database race conditions (Issue #2640).

**Satisfaction Signals:**
- High-trust contributor base: 7 PRs in 24 hours, including complex security audits (PR #2630) and infrastructure features (PR #2634).
- Community tolerates long merge cycles for high-quality contributions (PR #102 merged after ~4 months).
- The self-modification framework (PR #2635) is likely to be well-received by power users pushing agent autonomy to its limits.

## 8. Backlog Watch

- **[Issue #2632](https://github.com/nanocoai/nanoclaw/issues/2632) — Telegram agent-swarm status in v2**  
  *Priority: High* | No maintainer response | Users committed to Telegram need a clear deprecation statement or migration path to plan their v2 adoption.

- **[Issue #2640](https://github.com/nanocoai/nanoclaw/issues/2640) — Delivery hot-journal race**  
  *Priority: High* | No maintainer response | A runtime error pattern that will compound with scale. Early triage and reproduction guidance from maintainers would prevent escalation.

- **[PR #2630](https://github.com/nanocoai/nanoclaw/pull/2630) — Security: symlink confinement for inbox roots**  
  *Priority: High* | Needs maintainer review decision | Security hardening PRs that go un-reviewed risk accumulating context debt. This fix addresses a genuine attack vector in the attachment handling pipeline.

- **[Issue #2636](https://github.com/nanocoai/nanoclaw/issues/2636) — OneCLI credential injection**  
  *Priority: Medium* | Needs prioritization | A concrete, bounded feature request that fits the project's credential management trajectory and has a clear implementation scope.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest: 2026-05-29

### 1. Today's Overview
Today marks a concentrated stabilization sprint for NullClaw, primarily driven by core contributors. While no new releases were cut, the repository saw high PR throughput with 10 pull requests updated, of which 7 were merged or closed. Activity was heavily skewed toward defect resolution—specifically around Telegram channel reliability, platform compatibility, and test hygiene—rather than new user-facing features. The two closed issues both involved long-standing Telegram configuration frustrations that were finally addressed. Overall project health is good, with maintainers aggressively closing feedback loops on reported regressions from the previous month.

### 2. Releases
**No new releases today.** The current stable train remains the v2026.4.17 releases cited in the now-resolved Telegram bugs (#901). Users tracking the `main` branch can expect the fixes highlighted below in the next tag.

---

### 3. Project Progress (Merged/Closed PRs)
Seven PRs were merged or closed today, representing significant improvements across configuration, security, and provider expansion:

- **Config & Channel Reliability** – [PR #924](https://github.com/nullclaw/nullclaw/pull/924) (raskevichai): Fixed silent rejection of numeric `allow_from` user IDs in Telegram channel configs. Merged, directly closing issues [#869](https://github.com/nullclaw/nullclaw/issues/869) and [#901](https://github.com/nullclaw/nullclaw/issues/901).
- **Platform Compatibility** – [PR #925](https://github.com/nullclaw/nullclaw/pull/925) (vernonstinebaker): Allowed macOS workspaces under `/private/var/folders` without triggering the broader system path blocklist. [PR #878](https://github.com/nullclaw/nullclaw/pull/878) (vernonstinebaker): Replaced cooperative yields with real POSIX `nanosleep` for reliable thread suspension on Linux/macOS.
- **Testing Infrastructure** – [PR #926](https://github.com/nullclaw/nullclaw/pull/926) and [PR #927](https://github.com/nullclaw/nullclaw/pull/927) (vernonstinebaker): Made `web_search` tests hermetic against host environment variables and suppressed noisy API error logs during `zig test`, improving CI determinism.
- **Provider Ecosystem** – [PR #922](https://github.com/nullclaw/nullclaw/pull/922) (PierreLeGuen): Added NEAR AI Cloud and Atlas Cloud as OpenAI-compatible providers, expanding the deployment options for agent backends.
- **Security Hardening** – [PR #907](https://github.com/nullclaw/nullclaw/pull/907) (racribeiro): Removed credential-bearing subprocess calls from HTTP paths, enforced explicit inbound trust for channel webhooks, and hardened shell job handling in the cron pipeline.

---

### 4. Community Hot Topics
The dominant theme in today’s digest is **Telegram channel reliability**. The two closed issues ([#869](https://github.com/nullclaw/nullclaw/issues/869), [#901](https://github.com/nullclaw/nullclaw/issues/901)), both filed by the same user over a month-long span, capture a deeply frustrating experience: the config file was correct and validated by `nullclaw config show`, yet the channel runtime silently refused to load users specified as numeric IDs. The underlying need is for **type-coercion transparency** in the config parser—users naturally write Telegram user IDs as raw integers. This fix (PR #924) directly addresses that gap.

On the open PR side, [PR #928](https://github.com/nullclaw/nullclaw/pull/928) (fixing [#918](https://github.com/nullclaw/nullclaw/issues/918)) addresses the silent loss of `spawn`-tool results in Telegram polling mode. Multiple reporters hitting this in production underscores a demand for reliable subagent result delivery in conversational interfaces.

---

### 5. Bugs & Stability
| Severity | Bug | Status |
|---|---|---|
| **High** | Telegram channel always shows “not configured” for numeric `allow_from` IDs (#869, #901) | **Fixed** in merged PR #924 |
| **High** | Spawn tool results silent disappear in Telegram polling mode (#918) | **Open** fix under review in PR #928 |
| **Medium** | Global memory entries invisible via `memory_list` (#917) | **Open** fix under review in PR #929 |
| **Low** | Expected provider errors causing stderr noise during `zig test` | **Fixed** in PR #927 |
| **Low** | macOS workspaces under `/private/var/folders` incorrectly blocked | **Fixed** in PR #925 |

The Telegram configuration bug was the highest-impact issue from a user perspective—it effectively blocked all Telegram channel usage for affected users despite valid config. The fix is clean and should be cherry-picked to a patch release.

---

### 6. Feature Requests & Roadmap Signals
Two strong directional signals emerge from today’s data:

1. **Provider Expansion (PR #922)** – The addition of NEAR AI Cloud and Atlas Cloud signals an active strategy to capture the decentralized / high-performance compute segment. This aligns with the broader agent ecosystem trend toward multi-provider fallback chains.

2. **Cron Subagent Engine (PR #783)** – Still open after 52 days, this massive feature by yanggf8 brings a full DB-backed scheduler with job types (skill/agent/shell), timezone support, delivery routing, and operator alerts. This is a clear roadmap bet on NullClaw evolving from a chat assistant into a fully autonomous agent orchestration platform. The lack of movement today is notable, but the feature breadth suggests it needs dedicated maintainer bandwidth to land.

---

### 7. User Feedback Summary
Direct user feedback in the issue tracker communicates clear pain points:

- **Pain (High):** Telemetry / channel configuration should be *auditable*. Users find it confusing when `config show` validates a config but `channel list` silently rejects it. The month-long gap between the first report (April 23) and fix (May 28) indicates a validation gap in the testing harness for edge-case config types.
- **Pain (High):** Subagent results disappearing (Issue #918) is a confidence-eroding bug for anyone running NullClaw as a production bot. Users expect end-to-end delivery guarantees.
- **Satisfaction Signal:** The breadth of provider integrations (NEAR, Atlas) and the proactive security hardening (PR #907) suggest a responsive maintainer team that values both flexibility and safety. Users investing in deployment-specific setups will benefit directly.

---

### 8. Backlog Watch
Three items require maintainer attention:

- **[PR #783](https://github.com/nullclaw/nullclaw/pull/783) – Cron Subagent** (yanggf8): Last updated 2026-05-28. This is now a **52-day-old open PR** with massive surface area (DB schema, CLI JSON output, shell job execution, multi-TZ support). Without dedicated review cycles, it risks significant bit-rot or merge conflict hell. This feature is too strategically important to let drift.
- **[PR #929](https://github.com/nullclaw/nullclaw/pull/929) – Memory List Fix** (raskevichai): Freshly opened fix for global memory discoverability (Issue #917). Core memory functionality is a fundamental building block for long-term agent context. Should be prioritized for merge.
- **[PR #928](https://github.com/nullclaw/nullclaw/pull/928) – Telegram Subagent Delivery** (raskevichai): Addresses production-grade reliability for Telegram users. Multiple reporters amplify the urgency; this fix directly impacts the trust production users place in the framework.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-29

## 1. Today's Overview
Project activity is at a sustained high tempo, with **50 PRs** and **33 Issues** updated in the last 24 hours. **33 PRs were merged or closed**, demonstrating strong execution on the "Reborn" refactoring track, particularly around auth infrastructure, CI pipeline hardening, and core egress decomposition. Community testers delivered a thorough validation pass on the v0.29.0 staging release, exposing critical flaws in the new WeCom channel and OpenAI provider configuration that now require prioritised patching. Overall project health is productive but strained, with a critical security review around a credential injection primitive ([#3917](https://github.com/nearai/ironclaw/issues/3917)) still unresolved and potentially gating the Reborn integration.

---

## 2. Releases
**No new releases today.** The v0.29.0 release candidate remains in staging, tracked by open PR [#3708](https://github.com/nearai/ironclaw/pull/3708), which lists API-breaking changes for `ironclaw_common` (0.4.2 → 0.5.0). Based on the volume of staging validation findings, a hotfix cycle is likely required before the release ships.

---

## 3. Project Progress
**Merged/Closed PRs (33 total in 24h) — key advances:**

- **Reborn Egress Decomposition**: [#4213](https://github.com/nearai/ironclaw/pull/4213) splits the 1828-line `lib.rs` facade into a structured pipeline under `crates/ironclaw_host_runtime/src/egress/`, separating policy lookup, validation, credential injection, transport dispatch, and response sanitisation.
- **CI Pipeline Stability**: Three benchmarking CI fixes landed: `id-token: write` scoping fixes ([#4221](https://github.com/nearai/ironclaw/pull/4221), [#4220](https://github.com/nearai/ironclaw/pull/4220)) and tracking `@main` instead of pinned SHAs ([#4217](https://github.com/nearai/ironclaw/pull/4217)).
- **Credential Boundary Gaps Closed**: [#3903](https://github.com/nearai/ironclaw/pull/3903) (merged to `reborn-integration`) wires durable `FilesystemCredentialBroker` into production composition and routes MCP `tools/call` credential plans through production egress.
- **WebUI v2 Features**: Skill activation projections are now live ([#4212](https://github.com/nearai/ironclaw/pull/4212)). Extension search now gracefully handles omitted queries as a "list-all" mode ([#4218](https://github.com/nearai/ironclaw/pull/4218)).
- **Core Engine Fixes**: Glob scan budget truncation now returns results gracefully instead of failing ([#4211](https://github.com/nearai/ironclaw/pull/4211)). Work summary projections added to the Reborn driver ([#4196](https://github.com/nearai/ironclaw/pull/4196)).

---

## 4. Community Hot Topics
- **Security Review of PathPlaceholder ([#3917](https://github.com/nearai/ironclaw/issues/3917))**: The most technically active thread. The author argues that `RuntimeCredentialTarget::PathPlaceholder` is a "strictly worse channel" than Header or Query injection for credential leakage and whether it should be removed before shipping. Tagged `security-review-required` and `reborn` — a decision is imminent.
- **Comprehensive WeCom Validation ([#4191](https://github.com/nearai/ironclaw/issues/4191))**: A deep QA pass on the new WeCom channel generated **6 sub-issues** covering image instability, conversation merging, vision analysis correctness, and missing setup UX. The tester found core text messaging stable but almost every peripheral feature broken or confusing.
- **Auth Architecture Synchronisation**: A cluster of high-context issues ([#4175](https://github.com/nearai/ironclaw/issues/4175), [#4176](https://github.com/nearai/ironclaw/issues/4176), [#4201](https://github.com/nearai/ironclaw/issues/4201), [#4204](https://github.com/nearai/ironclaw/issues/4204)) coordinates the Reborn production auth push, covering durable OAuth ports, first-party/MCP credential consumer wiring, and manual token HTTP surfaces. Multiple authors (henrypark133, italic-jinxin, serrrfirat) are collaborating on tightly scoped follow-ups.

---

## 5. Bugs & Stability

### High Severity
- **WeCom Vision Uses Wrong Images ([#4197](https://github.com/nearai/ironclaw/issues/4197))**: The vision analysis pipeline resolves stale or unrelated screenshots instead of the currently uploaded attachment, leading to completely incorrect AI responses.
- **WeCom Image Attachments Unstable ([#4195](https://github.com/nearai/ironclaw/issues/4195))**: HEIF images, large PNGs, and JPGs all exhibit inconsistent upload, rendering, or reply behavior. Some images never appear in the Web UI.
- **WeCom DM/Group Chat Merged ([#4194](https://github.com/nearai/ironclaw/issues/4194))**: Private messages and group chat messages are irreversibly merged into a single conversation in the Web UI.
- **OpenAI Provider Returns 400 on Test ([#4188](https://github.com/nearai/ironclaw/issues/4188))**: Configuring the OpenAI provider and clicking "Test" returns a `400 Bad Request`. Blocks custom model setup entirely for v0.29.0 staging users.
- **Nightly E2E Failure ([#4108](https://github.com/nearai/ironclaw/issues/4108))**: The scheduled nightly CI workflow failed on commit `9df5e8d`. No fix PR is yet linked.

### Medium Severity
- **Credential Zeroization Gap ([#4222](https://github.com/nearai/ironclaw/issues/4222))**: While `SecretMaterial` is properly handled, plaintext credentials are still copied into standard `String` fields during injection into headers, URLs, and `NetworkRequest` carriers.
- **WeCom Setup UX Missing Instructions ([#4193](https://github.com/nearai/ironclaw/issues/4193))**: Users are presented with empty Bot ID / Bot Secret fields with no links to the WeCom Open Platform admin console, no prerequisite guidance, and no indication that an enterprise/admin WeCom account is required.
- **Skill-Context Test Failures ([#4171](https://github.com/nearai/ironclaw/issues/4171))**: Existing tests assert trusted prompt text in `safe_summary` after the [#4140](https://github.com/nearai/ironclaw/issues/4140) contract split. Tests need updating to the new field model.

---

## 6. Feature Requests & Roadmap Signals
- **Reborn Auth Consolidation (Multi-Track)**: Documents and issues indicate a structured multi-track plan ([#4215](https://github.com/nearai/ironclaw/issues/4215), PR [#4216](https://github.com/nearai/ironclaw/pull/4216)). Track A (PKCE math consolidation) is underway, with `ironclaw_common::pkce` replacing three duplicate implementations.
- **SSO for WebUI v2**: Clear roadmap commitment to carry v1 SSO forward. Split into Google ([#4179](https://github.com/nearai/ironclaw/issues/4179)), GitHub ([#4180](https://github.com/nearai/ironclaw/issues/4180)), and NEAR ([#4181](https://github.com/nearai/ironclaw/issues/4181)) tracks. Google SSO PR [#4182](https://github.com/nearai/ironclaw/issues/4182) has already landed session machinery and PKCE/CSRF support.
- **IronHub Marketplace Feature ([PR #3737](https://github.com/nearai/ironclaw/pull/3737))**: A massive PR adding CLI and agent-callable tool/skill installation from IronHub, plus gateway HTTP endpoints with HMAC-verified delivery. Still open, suggesting a careful review cycle.
- **Web Access Extension ([PR #4219](https://github.com/nearai/ironclaw/pull/4219))**: First-party bundled "web-access" extension with Exa MCP search and zero-config activation.
- **Manual Token Auth Gate ([PR #4224](https://github.com/nearai/ironclaw/pull/4224))**: Descriptor-driven routes for collecting GitHub PATs and resolving auth gates via credential references.

---

## 7. User Feedback Summary
- **What Works**: The WeCom channel's core text messaging flow is validated as "mostly stable." E2E testing infrastructure is now producing structured validation reports, indicating maturing QA processes.
- **Key Pain Points**:
    - **WeCom Setup Friction**: The current UX provides zero onboarding help. Users must navigate the WeCom Open Platform without guidance.
    - **Vision / Image Unreliability**: The WeCom vision pipeline is functionally broken for common use cases — wrong images analyzed, HEIF unsupported, large uploads failing silently.
    - **OpenAI Blocked**: The provider test failure blocks any user trying to connect a custom or self-hosted OpenAI-compatible endpoint on v0.29.0.
- **Satisfaction Indicators**: No explicit positive user testimonials in today's data, but the detailed WeCom validation report reflects invested testing effort.

---

## 8. Backlog Watch
- **[Issue #3917](https://github.com/nearai/ironclaw/issues/3917) — PathPlaceholder Security Decision**: Open since May 23. Tagged `security-review-required` and `module:M4-host-kernel`. Requires a maintainer decision (remove or harden) before the Reborn integration ships.
- **[PR #3737](https://github.com/nearai/ironclaw/pull/3737) — IronHub Tools/Skills Installation**: Open since May 17. XL scope with database migration. Needs review bandwidth to avoid stalling the marketplace feature.
- **[PR #3708](https://github.com/nearai/ironclaw/pull/3708) — Release v0.29.0**: Open since May 16. Blocked by the volume of staging validation findings. The OpenAI and WeCom blocking bugs likely need fixes to land before release.
- **[Issue #4108](https://github.com/nearai/ironclaw/issues/4108) — Nightly E2E CI Failure**: No fix PR linked. An unaddressed CI red flag that could hide regressions if not investigated promptly.
- **[PR #3834](https://github.com/nearai/ironclaw/pull/3834) — Benchmark Canary**: Open since May 21. A test PR waiting for the CI fixes in [#4220](https://github.com/nearai/ironclaw/issues/4220)/[#4221](https://github.com/nearai/ironclaw/issues/4221) to fully land before closing.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-29

## 1. Today's Overview
LobsterAI saw elevated development activity in the last 24 hours, with **7 Pull Requests merged/closed** and only **1 new Issue opened**. The primary development focus centered on shipping the new **Kit (Expert Suite)** ecosystem and reinforcing plugin/MCP infrastructure. The absence of user comments or reactions on Issues suggests quiet community engagement externally, though internal development velocity remains high. The backlog of 9 open Pull Requests saw fresh updates, indicating the maintainers are cycling through previously stalled work. No new releases were published.

**Activity Assessment:** Development-heavy, maintenance-moderate, community-quiet.

---

## 2. Releases
No new releases were published in the last 24 hours.

---

## 3. Project Progress — Merged/Closed PRs Today
7 Pull Requests were merged or closed:

**Kit (Expert Suite) Ecosystem**
- **[#2060]** **feat: Kit（专家套件）商店与对话集成** — *Merged.* Landed the flagship Kit Store feature, enabling users to browse, install, and use curated Skill bundles directly in conversation. Includes spec documentation.
- **[#2067]** **fix: Kit try-asking 跳转后未转换为 skills** — *Merged.* Fixed a critical state sync bug where Kits installed from the store did not expand into skills when entering a chat session via "Try Asking."

**Plugin & Configuration Management**
- **[#2069]** **feat: plugin update check for npm/clawhub sources** — *Merged.* Adds a "Check Updates" button for plugins sourced from npm and ClawHub, resolving a long-standing user need for version visibility.
- **[#2068]** **fix: defer plugin settings save — batch write + dirty guard** — *Merged.* Eliminates excessive gateway restarts by batching plugin configuration writes. A significant stability improvement for users with many plugins.

**MCP & Renderer Stability**
- **[#2066]** **fix(mcp): kill stdio process trees and share runtime across sessions** — *Merged.* Fixes orphaned "grandchild" processes on Windows by replacing SDK transport with `OpenClawStdioClientTransport` using `taskkill /T`.
- **[#2070]** **fix: scope tool_result artifact detection to image gen tools only** — *Merged.* Prevents command output (e.g., `find . -name "*.png"`) from being incorrectly detected as artifacts.
- **[#2061]** **feat(cowork): support click-to-preview for image attachments in input** — *Merged.* Reuses the `ImagePreviewModal` for attachment thumbnails, improving the image workflow.

---

## 4. Community Hot Topics

With zero comments or reactions logged on the surfaced items, activity signals derive primarily from development focus rather than community discussion.

- **[#2071]** **创建定时任务错误 (Scheduled Task Creation Error)** — The sole new Issue. Reported against version `2026.5.27`. The user shared a screenshot of an error when creating scheduled tasks. This is a critical signal given the pending scheduled task UI overhaul.
- **[#1488]** **定时任务模块 UI 全面升级 (Scheduled Task UI Overhaul)** — This open PR saw an update yesterday. It proposes converting the task list to a card grid, adding search, and improving the history view. The proximity to the bug report (#2071) strongly implies this overhaul is being prepared to address existing defects.
- **[#1484]** **feat(automation): add Gmail email trigger** — Continues to receive updates. Represents the strongest automation roadmap signal, aiming to bring Gmail-triggered agent sessions without external infrastructure.

**Underlying Needs:** Users need stability in the scheduling module, are actively consuming the new Kit ecosystem (indicated by the flurry of Kit-related fixes), and are pushing for deeper agentic automation triggers.

---

## 5. Bugs & Stability

| Severity | Issue/PR | Status | Details |
|----------|----------|--------|---------|
| **High** | [#2071] Scheduled Task Error | **Open, needs triage** | User cannot create scheduled tasks (v2026.5.27). No fix PR yet. May be a regression. |
| **Resolved** | [#2066] MCP Zombie Processes | **Merged** | Windows orphaned child processes were a significant stability and resource leak. Fixed. |
| **Resolved** | [#2068] Plugin Config Race | **Merged** | Repeated gateway restarts on plugin toggle caused instability. Fixed via batch save. |
| **Resolved** | [#2067] Kit State Sync | **Merged** | Installed Kits not showing in chat provided a broken UX for the new flagship feature. |
| **Medium** | [#1478] CopyButton Memory Leak | *Stale PR* | Unmounted component timer leak. PR exists but has been open since April 4. |
| **Medium** | [#1482] Task Edit Clears Description | *Stale PR* | Editing a scheduled task resets `description` to empty and forces `enabled: true`. |

**Summary:** The pattern of stale bug-fix PRs from April (issues #1478–#1482) remains concerning. These are not new today, but their continued open status keeps risk latent in the scheduling and cowork modules.

---

## 6. Feature Requests & Roadmap Signals

**Landing Today:**
- **Kit Store & Dialog Integration** (#2060): Full lifecycle for Expert Suites.
- **Plugin Update Mechanism** (#2069): Version checking without external manual steps.
- **Image Attachment Preview** (#2061): UX polish for cowork mode.

**Strong Roadmap Predictions (likely for next release):**

1. **Scheduled Task Module Revamp (#1488):** Card grid UI, search, date-filtered history. Given the bug report (#2071), this is likely to be fast-tracked to merge soon.
2. **Per-Session Skill State (#1494):** Moves active skill IDs from global state to per-conversation state. This is a natural UX upgrade to match user expectation.
3. **Automatic Model Failover (#1483):** Retry with a fallback model on transient errors. High-value for production/automation users.
4. **Gmail Agent Trigger (#1484):** Polling-based email trigger. Signals an expansion of the automation platform beyond purely internal triggers.

---

## 7. User Feedback Summary

**Pain Points:**
- The single user issue (#2071) explicitly identifies an **error creating scheduled tasks**, indicating either a regression or insufficient UX guardrails in the current table-based UI.
- The stale PRs cover persistent pain points: **skills can be installed twice** (#1479), **editing a task discards metadata** (#1482), and **skill selection is global rather than per-session** (#1494). These are recurring themes mentioned in the backlog.

**Use Cases:**
- **Kit/Skill Curation:** The Kit feature launch demonstrates user desire for role-based bundles (e.g., "writer kit," "coder kit") over individual skill management.
- **Reliability:** The merged MCP and plugin fixes respond to silent failures (orphaned processes, config resets). Users dependent on headless/runtime agent use will benefit significantly.
- **Automation Depth:** The Gmail trigger (#1484) and Model Failover (#1483) signals point to users wanting LobsterAI to act as a reliable, long-running automation agent rather than a simple chat UI.

**Satisfaction:** Feature velocity is high (Kit store, image preview, update checks). However, the accumulation of stale bug-fix PRs and the new scheduling error create a risk that users perceive the product as prioritizing new features over core stability.

---

## 8. Backlog Watch

**High-Impact Stalled Items (Updated 2026-05-28):**

| Item | Author | Created | Notes |
|------|--------|---------|-------|
| [#1488] Scheduled Task UI Revamp | gongzhi-netease | Apr 5 | Major UX overhaul; readies fix for #2071. Needs expedited review. |
| [#1494] Per-Session Skill Selection | gongzhi-netease | Apr 6 | Separates skill state by conversation. Major UX regression fix. |
| [#1483] Model Failover | linlihua | Apr 5 | High-demand reliability feature. Large diff, complex merge. |
| [#1484] Gmail Trigger | linlihua | Apr 5 | Key automation feature. |

**Stale PRs Needing Maintainer Decision (Labeled `[stale]`):**

- [#1478], [#1479], [#1480], [#1481], [#1482] — All dated April 4–5 from `linlihua` and `kayo5994`. These cover memory leaks, duplicate skill detection, task metadata loss, and scroll behavior.
- **Risk:** These contributors have not been engaged on their PRs for nearly two months. Without closure (merge or clear rejection), this risks contributor churn and signals a bottleneck in the review pipeline.

**Watch Item:** The correlation between [#1488] (Scheduled UI Overhaul) and [#2071] (Scheduled Task Error) strongly suggests the team should prioritize reviewing and merging [#1488] to pre-empt further user-impacting bug reports.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest — 2026-05-29**

---

### 1. Today's Overview

Moltis activity on May 29th was highly productive, characterized by a focused bug-fix sprint that resolved seven issues and merged four pull requests. Maintainers demonstrated rapid turnaround, often addressing user reports within 12-48 hours of their filing. While no new release was cut, the codebase saw substantive stability improvements across Discord integration, provider compatibility, core UI workflows, and the cron scheduler. The lone open issue and a single new feature PR signal that the team is now shifting attention from reactive bug fixing toward more complex architectural features involving terminal-based agent control. Overall project velocity is strong, though the lack of a formal release tempers the immediate impact of these fixes for end users.

---

### 2. Releases

**None.**
No releases were published on May 28–29, 2026. Given the volume of merged fixes, a patch release is expected imminently.

---

### 3. Project Progress

Four pull requests were merged, all authored by *penso*, directly resolving verified user bugs:

- **PR #1081 – `fix(discord): log silent voice message drops`**  
  Adds diagnostic logging for Discord voice messages and introduces regression tests for attachment-only and voice-attachment-only payloads. Resolves Issue #817.

- **PR #1078 – `fix(providers): strip MiniMax user names`**  
  Disables OpenAI-compatible user `name` fields for MiniMax providers to avoid API error 2013 in group-chat histories. Moves provider quirks into catalog metadata for cleaner maintainability. Resolves Issue #1077.

- **PR #1080 – `fix(web): include clicked response in message forks`**  
  Corrects the session fork boundary so that forks start from the selected assistant response rather than the preceding user prompt. Includes Playwright regression coverage. Resolves Issue #1075.

- **PR #1079 – `fix(cron): preserve host execution target`**  
  Prevents agent preset resolution from overriding explicit cron "Execution Target: Host" configurations, which were defaulting to sandbox execution. Resolves Issue #1072.

---

### 4. Community Hot Topics

The most significant community discussion centers around **Issue #235** (6 comments, 1 👍), the lone open issue in today's batch. It proposes PTY-based interactive control for spawning Claude Code as a subprocess. The core technical blocker is that `exec`/`spawn` with `stdio: pipe` causes `isatty()` to return `false`, forcing CLI tools into non-interactive mode. This is a foundational feature request for users building complex multi-agent loops that require terminal interaction (e.g., `git rebase`, debuggers, interactive prompts). The issue has been open since February 2026, indicating both its high value and significant architectural complexity.

The newly opened **PR #1082** (`feat(channels): add gated tmux control command`) is likely the next hot topic. While distinct from autonomous agent PTY control, it provides an opt-in `/tmux` command for allowlisted users to inspect and interact with the host terminal directly. This represents an immediate—if gated—step toward terminal integration within the Moltis channel framework.

---

### 5. Bugs & Stability

Four bugs were actively filed and fixed within the reporting window. Ranked by severity:

- **[Critical] Provider Crash (Issue #1077)** – `Error: invalid params, user name must be consistent (2013)`  
  Multi-user group-chat sessions with the MiniMax provider would crash entirely. This was a hard blocker for anyone using that provider in group settings. **Fix merged in PR #1078.**

- **[High] Broken Fork UX (Issue #1075)** – `"fork" forks at prompt, not response`  
  The session fork mechanism, essential for exploring alternative conversation paths, was misaligned—branching from the user prompt instead of the intended assistant response. This broke a core interaction model. **Fix merged in PR #1080.**

- **[High] Cron Sandbox Override (Issue #1072)** – `cron jobs marked "Execution Target: Host" run in a sandbox by default`  
  Cron jobs explicitly configured for host execution were silently forced into sandboxed environments, breaking automated workflows that depend on full host access. **Fix merged in PR #1079.**

- **[Medium] Silent Data Loss (Issue #817)** – `Discord voice messages silently dropped`  
  Voice messages were dropped entirely without diagnostic logging, making the behavior invisible to users and operators. **Fix merged in PR #1081** (adds logging and regression tests).

---

### 6. Feature Requests & Roadmap Signals

The roadmap is clearly prioritizing **terminal-native agent interactions**.

- **Near-term signal — PR #1082:** The new `/tmux` channel command for allowlisted users is a concrete, immediately deliverable feature. It provides human-in-the-loop terminal inspection and input, which can serve as a foundation for broader terminal integration.
- **North-star feature — Issue #235:** Full PTY support for autonomous sub-agents remains the most ambitious outstanding feature request. It requires re-engineering the subprocess spawning layer to present a real TTY to spawned tools like Claude Code. This is a major architectural initiative.
- **Deprioritized — Issue #906 (WebUI Sub-agents):** This feature request was closed without a linked PR, suggesting it is either on hold or being redesigned for a more fundamental integration scheduled for a later milestone.

---

### 7. User Feedback Summary

User sentiment reflects a mix of frustration with configuration fragility and satisfaction with the speed of resolution.

- **Pain Points:**
  - **Cron reliability** remains the most recurring pain point (Issues #333, #1072). Users relying on automated agent execution are hitting subtle configuration overrides that cause unexpected behavior.
  - **Provider compatibility** continues to cause friction, with the MiniMax crash (Issue #1077) and Discord drops (Issue #817) highlighting gaps in non-core provider and channel robustness.
  - **UX regression** on the fork mechanic (Issue #1075) disrupted power users who rely on branching conversations to iterate on agent interactions.

- **Satisfaction Indicators:**
  The rapid turnaround time is a strong positive signal. All four bugs filed between May 25 and May 27 were addressed in PRs merged by May 28. This demonstrates active triage and a maintenance team that directly engages with user reports.

---

### 8. Backlog Watch

- **Issue #235 (PTY Control)** — Opened 2026-02-25, this is the single most significant open feature request. Now over 3 months old, it has robust community engagement but no linked implementation PR. The technical difficulty of grafting PTY support onto the existing subprocess execution model makes it a heavy lift. The community should watch for a design document or proof-of-concept branch in the coming weeks, especially given the adjacent `/tmux` work in PR #1082.

- **PR #1082 (Tmux Control)** — While just opened, this feature carries security implications (allowing channel commands to interact with the host tmux server). It has not yet received maintainer feedback or community comments. This is a high-priority item for code review due to the architectural surface area it introduces.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for CoPaw (QwenPaw) based on the provided GitHub data.

---

## CoPaw/QwenPaw Project Digest — 2026-05-29

### 1. Today's Overview
The project saw a significant spike in community activity, with 40 issues and 38 pull requests updated in the last 24 hours. While no new release was published, the development team maintained strong velocity, merging 20 PRs and closing 10 issues. The data reveals a highly engaged user base—predominantly from the Chinese-speaking community—that is both deeply technical and vocal about specific UI/UX pain points, particularly regarding the v1.1.9 Windows desktop build. The balance of incoming bug reports versus feature requests suggests the project is transitioning from core stability fixes toward heavy polish and power-user functionality.

### 2. Releases
**No new releases were cut today.** The current stable version remains v1.1.9.

### 3. Project Progress
The team closed 10 issues and merged 20 pull requests today, showing strong responsiveness to reported defects.

**Notable Merged/Closed Work:**
- **Chat Input Fix**: Resolved the issue where navigating away from the chat and returning refilled the textarea with previous content (#4774). Fixed by PR #4755.
- **Cron Job Management**: Addressed the inability to delete or edit manually created cron jobs in the UI (#4775).
- **Quality of Life**: Closed requests for `/skills` tab autocomplete support (#4785), quick-access buttons for generated Word/PPT files (#4786), and conversation sorting by latest message time (#4746, #4732).
- **Channels Enhancement**: Added support for keyboard/markdown messages in `channels send` (#4730).
- **UI Refactoring**: Merged style improvements for the Environments and Security tabs (#4657). Added loading states to the workspace download button (#4725).
- **Infra/Deps**: Updated the `@agentscope-ai/chat` library to version `1.1.64-beta` (#4771). Added a workflow to automatically update the contributors list on merges (#4692).
- **Security Closure**: Officially closed the investigation into Windows Defender false positives on v1.1.3 (#3718), documenting the root cause and confirming the fix.

### 4. Community Hot Topics
The most active discussions reveal a community focused on deployment, core loop stability, and advanced agent features.

- **Packaging & Distribution** ([#4754](https://github.com/agentscope-ai/QwenPaw/issues/4754), 7 comments): A user asked about the difference between the standard Windows client and the Tauri client, indicating a strong desire among developers to create custom standalone `.exe` builds. This is a recurring concern for the community.
- **Critical Core Loop Bug** ([#4739](https://github.com/agentscope-ai/QwenPaw/issues/4739), 6 comments): The highest-signal bug report. Users report the agent silently transitions to a "waiting for user input" state after a tool call completes (or errors). This represents a fundamental breakdown in the agent loop and has drawn significant community attention.
- **Memory System Overhaul** ([#4652](https://github.com/agentscope-ai/QwenPaw/issues/4652), 4 comments): A very detailed proposal from a power user critiquing the current memory system as "information accumulation" rather than "knowledge building." The user provides a thorough breakdown of gaps in summarization, state management, and associative indexing.
- **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727), 2 👍): This Breaking Change proposal received the highest reaction count today, signaling strong community support for modernizing the project’s backend architecture.

### 5. Bugs & Stability
Several critical and high-severity issues were reported today, though some have immediate fix PRs in the pipeline.

**Critical (Core Loop / Data Loss)**
- **Tool Call Hang** ([#4739](https://github.com/agentscope-ai/QwenPaw/issues/4739)): Agent goes silent after any tool call. **No fix PR linked yet.**
- **Message Loss on Restart** ([#4791](https://github.com/agentscope-ai/QwenPaw/issues/4791)): `shutdown_handler` is empty, causing the loss of the last few messages in a session when the service receives SIGTERM. Detailed root cause provided. **No fix PR linked yet.**
- **Context Window Blowup** ([#4781](https://github.com/agentscope-ai/QwenPaw/issues/4781)): Oversized shell command output bypasses pruning limits, ballooning the context window. **Fix PR #4787 is open and awaiting review.**

**High Severity**
- **Channel Reliability** ([#4788](https://github.com/agentscope-ai/QwenPaw/issues/4788)): OneBot channel disconnects randomly and stops listening. Requires manual intervention to restore connectivity.
- **Desktop Pet Loop** ([#4783](https://github.com/agentscope-ai/QwenPaw/issues/4783)): v1.1.9 Windows Desktop—starting the pet creates a terminal loop but the pet itself never opens.
- **CMD Window Popping** ([#4777](https://github.com/agentscope-ai/QwenPaw/issues/4777)): Shell commands during agent execution pop visible cmd windows, which users find disruptive.

**Medium/Low Severity**
- **Webpage Navigation Trap** ([#4764](https://github.com/agentscope-ai/QwenPaw/issues/4764)): Opening a link in the desktop app results in an inability to navigate back.
- **LaTeX Rendering** ([#4756](https://github.com/agentscope-ai/QwenPaw/issues/4756)): Poor rendering of math formulas in the web UI compared to standard Markdown editors.
- **SVG Rendering Error** ([#4768](https://github.com/agentscope-ai/QwenPaw/issues/4768)): Error `<svg> attribute width/height: Expected length, "small".` on the "AllowNoAuthHosts" tab. **Fix PR #4790 is open.**

### 6. Feature Requests & Roadmap Signals
Today’s data suggests the roadmap is heavily influenced by power users pushing QwenPaw toward being a full **code agent** rather than a pure chatbot.

- **Likely for Next Version (v1.2.0 Signals):**
    - **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)): The biggest looming architecture change.
    - **High-Fidelity Conversation Management** ([#4789](https://github.com/agentscope-ai/QwenPaw/issues/4789)): Explicitly asks for "Trae-like" behavior: reverting conversations, tracking file changes, and managing project directories directly rather than using a sandbox.
    - **Provider Failover** ([#4757](https://github.com/agentscope-ai/QwenPaw/issues/4757)): Automatic fallback to a backup LLM provider when hitting token/rate limits.
- **Polishing Candidates (Next Patch):**
    - **Session List UX** ([#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770), [#4780](https://github.com/agentscope-ai/QwenPaw/issues/4780), [#4782](https://github.com/agentscope-ai/QwenPaw/issues/4782)): Requests for column order adjustment, direct click navigation, and context window size display are all low-effort, high-impact wins.
    - **Cron Job UI** ([#4776](https://github.com/agentscope-ai/QwenPaw/issues/4776), [#4778](https://github.com/agentscope-ai/QwenPaw/issues/4778)): Users are heavily criticizing the cron popup design and session binding UX, requesting a more silent/smart interface.

### 7. User Feedback Summary
The predominant voice in today’s data is the Chinese power-user community. The sentiment is best described as **demanding but loyal**.

- **Pain Points:**
    - "Why does QwenPaw have to be so different?" (#4746) regarding session sorting.
    - "This design is terrible, it feels like a virus" (#4776) regarding cron task popups.
    - "Every time I switch back, I have to manually delete the content" (#4774) regarding the input box.
    - Strong frustration with Windows-specific clutter: popping CMD windows (#4777) and the desktop pet loop (#4783).
- **Satisfaction Signals:**
    - Users are investing time in deep architectural proposals (e.g., #4652 memory system, #4758 config versioning). This indicates a high level of trust that the team will listen.
    - The quick fix of the chat input bug (#4774 → #4755) shows the community that their bug reports translate into rapid action.

### 8. Backlog Watch
Several critical and highly visible items remain open without a clear signal from maintainers or an assigned fix.

- **Top Priority Watch:**
    - **Agent Loop Hang** ([#4739](https://github.com/agentscope-ai/QwenPaw/issues/4739)): With 6 comments and no linked fix PR, this is the most urgent unaddressed defect regarding the core agent loop.
    - **Message Loss on Restart** ([#4791](https://github.com/agentscope-ai/QwenPaw/issues/4791)): Filed today with an excellent root cause analysis. Needs immediate assignment to prevent data loss.
    - **Context Blowup Fix** ([#4781](https://github.com/agentscope-ai/QwenPaw/issues/4781) -> [#4787](https://github.com/agentscope-ai/QwenPaw/pull/4787)): A fix PR is pending review. High priority for memory stability.
- **Strategic Watch:**
    - **Memory System Enhancement** ([#4652](https://github.com/agentscope-ai/QwenPaw/issues/4652)): A highly engaged user provided a lengthy analysis on memory limitations. Strategic alignment and a maintainer response are needed.
    - **AgentScope 2.0 Migration** ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)): The community is eager for a timeline. This is currently the highest-stake roadmap item.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — May 29, 2026

**Project:** [zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
**Analysis Window:** 24 hours ending 2026-05-29


## 1. Today's Overview

The project is in a phase of intense development, registering activity on 34 Pull Requests and 20 Issues in the last day. The primary engine of this activity is the massive `integration/zeroclaw-tui` branch ([#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)), which packages the new `zerocode` TUI, RPC socket transport, and a `DenyWithEdit` approval model ahead of a v0.8.0-beta-2 tag. While architectural velocity is high, so is the user friction: five new bugs landed today, including S1 workflow blockers for Slack Socket Mode ([#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992)) and the onboarding wizard ([#6975](https://github.com/zeroclaw-labs/zeroclaw/issues/6975)). Community health remains robust—contributors are filing forward-looking RFCs ([#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)) and granular i18n patches ([#6990](https://github.com/zeroclaw-labs/zeroclaw/issues/6990))—but the maintainer team faces a growing tension between shipping the next beta and stabilising the current one.

## 2. Releases

No new releases in the last 24 hours.


## 3. Project Progress — Merged / Closed

Three PRs cleared in the reporting period:

- **Anthropic Native Extended Thinking ([#5650](https://github.com/zeroclaw-labs/zeroclaw/pull/5650))** — *Merged.* Adds dedicated reasoning-chain support via `budget_tokens` for high/max thinking levels. A major competitive feature for users running Claude on the native Anthropic provider.
- **OpenAI Codex Subscription Auth ([#6908](https://github.com/zeroclaw-labs/zeroclaw/pull/6908))** — *Merged.* Fixes a long-standing onboarding gap. ChatGPT Plus/Pro (Codex) users can now configure ZeroClaw without an API key, routing through OAuth instead.
- **Slack Strict Mention Default ([#6994](https://github.com/zeroclaw-labs/zeroclaw/pull/6994))** — *Merged.* Small, high-impact behavioural fix: `strict_mention_in_thread` now defaults to `true`, enforcing uniform @-mention rules across top-level and thread messages.

**What else is imminent:**
- The `integration/zeroclaw-tui` branch ([#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)) remains open for first-round feedback. When landed, it will form the basis of v0.8.0-beta-2.
- [`feat(tools): add file_download tool` (#6957)](https://github.com/zeroclaw-labs/zeroclaw/pull/6957) extends the agent workspace with remote-fetch capability.
- [`fix(gateway): invalidate bearer token on device rotate/delete` (#6988)](https://github.com/zeroclaw-labs/zeroclaw/pull/6988) addresses a security gap in token lifecycle management.


## 4. Community Hot Topics

| Issue / PR | Engagement | Summary | Community Need |
|---|---|---|---|
| **DeepSeek-V4 API Block [#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)** | 14 comments, 4 👍 | DeepSeek-V4-Pro and V4-Flash error out on thinking-mode responses. | **Stability.** Early adopters of V4 are completely blocked. Top priority for the provider team. |
| **Reply Intent in 1:1 Chats [#5674](https://github.com/zeroclaw-labs/zeroclaw/issues/5674)** | 4 comments, 3 👍 | `classify_channel_reply_intent` makes the agent ignore users in private chat. | **Correctness.** A per-user/per-agent configurable classifier provider (see [PR #6945](https://github.com/zeroclaw-labs/zeroclaw/pull/6945)) is the expected fix. |
| **Slack Socket Mode Auth [#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992)** | 0 comments (fresh) | All Slack messages rejected as "unauthorized user" via Socket Mode. | **Critical UX.** No workaround evident. Expect rapid escalation. |
| **RFC: Granular Sandbox Policy [#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)** | 0 comments (fresh) | Config-driven filesystem/network restrictions for Landlock, Bubblewrap, Seatbelt. | **Roadmap signal.** A highly architecture-aware request from the community for production-grade sandboxing. |
| **Multiple Safety Issues [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470)** | 4 comments | Duplicate memories, cron delivery gaps, token wastage with `gpt-5.4` high reasoning. | **Trust.** The `r:needs-repro` label has stalled this for 7 weeks. Users want the safety/consistency path validated. |

**Analysis:** The community is deeply invested in provider resilience (DeepSeek, Slack, MiniMax) and behavioural determinism (reply intent, safety loops). The engagement on #6059 and #5674 reflects growing adoption of paid-tier models paired with expectations of reliability.


## 5. Bugs & Stability

**S1 — Workflow Blocked**

| ID | Component | Impact | Fix Status |
|---|---|---|---|
| [#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992) | `channel: slack` | Slack Socket Mode rejects ALL incoming messages. Channel is dark. | No fix PR yet. |
| [#6975](https://github.com/zeroclaw-labs/zeroclaw/issues/6975) | `config, onboard` | `zeroclaw onboard` marks sections complete but writes **zero config**. Onboarding is a no-op. | No fix PR yet. |
| [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | `provider` | `context_compression` drops `tool_calls` and `tool` result messages for OpenAI-compatible providers (MiniMax). Causes tool-calling loops. | Likely addressed in [#6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848) rewrite. |

**S2 — Degraded Behaviour**

| ID | Component | Impact | Fix Status |
|---|---|---|---|
| [#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) | `provider:deepseek` | DeepSeek V4 API incompatible. High-risk, 4 👍. | In-progress. |
| [#6976](https://github.com/zeroclaw-labs/zeroclaw/issues/6976) | `web, gateway:ws` | Web UI WebSocket immediately drops (code 1006). Missing `?agent=` query param. | No fix PR yet. |
| [#6991](https://github.com/zeroclaw-labs/zeroclaw/issues/6991) | `runtime, tool` | Tool serialisation bypasses Risk Profile and Tool Filter restrictions in v0.8.0-beta-1. | No fix PR yet. |
| [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) | `onboard, cli` | Backspace in `zeroclaw agent` CLI deletes byte-by-byte. CJK characters require 3 backspaces. | No fix PR yet. |

**S3 — Minor**

| ID | Component | Impact |
|---|---|---|
| [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) | `channel` | Command replies hardcode English strings, bypassing Fluent locale configuration. |
| [#6990](https://github.com/zeroclaw-labs/zeroclaw/issues/6990) | `tool, i18n` | New `file_download` tool strings need Fluent licensing. |


## 6. Feature Requests & Roadmap Signals

**Most Likely for v0.8.0-beta-2:**
- **Per-Agent `classifier_provider` ([PR #6945](https://github.com/zeroclaw-labs/zeroclaw/pull/6945)):** Directly addresses the `classify_channel_reply_intent` pain point (#5674). Allows routing intent classification to a cheaper model.
- **`file_download` Tool ([PR #6957](https://github.com/zeroclaw-labs/zeroclaw/pull/6957)):** Adds workspace-based remote file fetching.
- **`zerocode` TUI + RPC Transport ([PR #6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)):** The patch is a heavy lift (XL, high risk) but is flagged as the basis for the next pre-release.
- **`--ephemeral` Daemon Mode ([#6818](https://github.com/zeroclaw-labs/zeroclaw/issues/6818)):** Daemon self-terminates when the last RPC client disconnects.

**Strong Backlog Candidates:**
- **Granular Sandbox Policy ([#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996)):** Though filed today, the architectural depth suggests it will influence the security roadmap.
- **Faster SQLite ANN ([#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570)):** A six-week-old enhancement request to move from O(n) vector scan to an in-process ANN index.
- **Cron Announce Final Message Only ([#6510](https://github.com/zeroclaw-labs/zeroclaw/issues/6510)):** A quality-of-life request to strip intermediate reasoning narration from cron deliveries.
- **Session-Scoped Runtime Overrides ([#6817](https://github.com/zeroclaw-labs/zeroclaw/issues/6817)):** Per-session model/temperature overrides without daemon restart.


## 7. User Feedback Summary

**Pain Points**

- **Provider Instability:** High friction on DeepSeek V4 (thinking mode) and MiniMax (tool loops). Users want API format hardening.
- **Onboarding is Broken:** `zeroclaw onboard` (#6975) writes no config, which is a critical discoverability barrier for new evaluators.
- **Slack Socket Mode Failure (#6992):** A major channel for many users is completely dark. Expect urgency.
- **UTF-8 Input Corruption (#6995):** CJK/IME users are significantly impacted. The terminal CLI is practically unusable for multi-byte scripts.
- **1:1 Ignorance (#5674):** Persistent frustration that the assistant ignores private chat messages. The community is vocal.

**Satisfaction Signals**

- **Anthropic Extended Thinking (#5650)** was merged successfully, a heavily requested feature for deep reasoning workflows.
- **Codex Auth (#6908)** lowers the barrier for a large cohort of OpenAI subscribers.
- **High-Quality Contributions:** Community members are authoring RFCs (#6996) and detail-oriented patches (#6990, #6989), indicating a mature, investment-positive relationship with the project.

**Overall Sentiment**
*Cautiously optimistic, moderately strained.* The beta-1 user base is pushing hard on real-world use cases and exposing deep integration bugs. The maintainers’ rapid pace signals strong intent, but the number of simultaneous S1 bugs undermines confidence for production-evaluation users.


## 8. Backlog Watch — Items Needing Maintainer Attention

**Stalled Pull Requests (needs-author-action)**

| PR | Date | Value | Status |
|---|---|---|---|
| `feat(ci): add arm64 docker target` [#5187](https://github.com/zeroclaw-labs/zeroclaw/pull/5187) | Apr 2 | Cross-platform deployment | Held on author feedback |
| `fix(tools): add ipv6 support` [#5450](https://github.com/zeroclaw-labs/zeroclaw/pull/5450) | Apr 7 | IPv6 readiness | Held on author feedback |
| `feat(channels/slack): backfill thread context` [#6428](https://github.com/zeroclaw-labs/zeroclaw/pull/6428) | May 6 | Slack thread awareness | Held on author feedback |
| `feat(channels): per-recipient reply pacing` [#6389](https://github.com/zeroclaw-labs/zeroclaw/pull/6389) | May 5 | Rate-limit compliance | Held on author feedback |

**Stale / Blocked Issues**

| Issue | Date | Risk | Blockage |
|---|---|---|---|
| [#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570) ANN SQLite Memory | Apr 9 | Medium (scale bottleneck) | Tagged `stale` / `blocked` |
| [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) Multiple Safety Issues | Apr 7 | High (memory dedup, cron bugs) | Tagged `r:needs-repro, stale, blocked` |

**Call to Action:** Four valuable community PRs are languishing under `needs-author-action`. A triage pass by maintainers to close, adopt, or request specific changes would recover significant community goodwill and feature velocity. The DeepSeek-V4 issue [#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) (April 24) deserves an active status update given its community weight.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*