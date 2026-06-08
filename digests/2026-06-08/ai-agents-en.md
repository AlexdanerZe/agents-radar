# OpenClaw Ecosystem Digest 2026-06-08

> Issues: 294 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-08 03:40 UTC

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

# 📊 OpenClaw Project Digest – June 8, 2026

**Data Snapshot:** 294 Issues updated (180 open) · 500 PRs updated (333 open, 167 merged/closed) · 0 New Releases · Generated from `openclaw/openclaw`


## 1. Today's Overview

The project is experiencing **extremely high activity** with nearly 800 total updated items in the last 24 hours, indicative of a major post-release stabilization and advancement cycle following the 2026.5 and 2026.6 trains. While the community is shipping substantial new features (voice providers, runtime self-context, subagent tool forwarding), the open issue queue reveals significant strain: multiple **P1 regressions** around session state, message delivery reliability, and security boundaries are active. The maintainer team is highly responsive, utilizing the `clawsweeper` triage bot extensively to route and prioritize work. A major architectural thread—the **SQLite session/transcript migration** (tracked in #88838)—is advancing via branch-by-abstraction, signaling a shift toward massive internal refactoring over the coming weeks.

## 2. Releases

**No new releases today.** The last known train (2026.6.x) is still being shaken out for regressions before the next cut.

## 3. Project Progress

**167 PRs merged or closed** in the last 24 hours. Notable resolved items:

- **Mattermost Stability:** Slash command 503 regression (#68113) and streaming config regressions (#70253) both fixed.
- **Discord Channel:** Exec approval card/button regression (#73802) resolved; guild ID resolution for search actions advanced (#88796).
- **Feishu Ecosystem:** Dispatch `TypeError` (#88234) and VC meeting invite handling (#89751) both addressed; retry logic for rate-limit errors (codes 230020/230006) is in review (#89659).
- **Core Agent Fixes:** Inbound media read refs resolved (#87219); stale session routes for removed providers are being guarded (#90500, active); heartbeat time-stamp refresh fix (#75025) progresses after long stall.
- **WebUI:** Recent sessions dropdown merged (#84216); Control UI bootstrap path fix submitted (#91305).
- **Security & Operations:** `npm-shrinkwrap` updated to fix moderate Hono CVEs (#91303); supervisor git handoff path implemented (#91296).

**Advances still in motion** (high-value open PRs with maintainer activity):
- 🚀 **Runtime Self Context Config & Tool** (#90101) – a showcase feature for cost/placement awareness.
- 🚀 **xAI Realtime Voice Provider** (#91308) – adds a major new provider to the Talk platform.
- 🧠 **Subagent toolsAllow Forwarding** (#78441) – extends ACP policy control.
- 🔧 **Session Cleanup & Archive Aggregation** (#89288, #89289) – improving storage accounting.

## 4. Community Hot Topics

The most active discussions reflect deep user investment in security, architecture, and stability:

- **🔥 [#25592 – Text Between Tool Calls Leaks to Channels](https://github.com/openclaw/openclaw/issues/25592)** (27 comments)
  *The #1 UX/security grievance.* Users demand strict separation of internal agent reasoning from user-facing output. Currently in `needs-product-decision` and `needs-security-review`. A diamond-lobster-rated issue with security and message-loss impacts.

- **🔬 [#88838 – Track Core SQLite Migration via Accessor Seam](https://github.com/openclaw/openclaw/issues/88838)** (18 comments)
  Heavy community engagement on the branch-by-abstraction strategy. Represents the future of session/transcript storage.

- **🐛 [#88312 – Codex App-Server Turn-Completion Stall Regression](https://github.com/openclaw/openclaw/issues/88312)** (14 comments, 👍3)
  Popular ChatGPT Plus/Codex provider completely broken for multi-tool turns since 2026.5.27. A platinum hermit regression requiring immediate live repro.

- **💥 [#90991 – Cron Scheduled Trigger Contaminates Global Runtime State](https://github.com/openclaw/openclaw/issues/90991)** (13 comments)
  Systemic reliability issue causing cascading overload failures. Platinum hermit rating, `needs-live-repro`.

- **🧩 [#22358 – Post-Subagent Completion Extension Hook](https://github.com/openclaw/openclaw/issues/22358)** (12 comments)
  Strong developer demand for generating structured trajectory files. Stale since Feb but still highly discussed.

- **🔑 [#31583 – Exec Tool Does Not Inherit `skills.entries.*.env`](https://github.com/openclaw/openclaw/issues/31583)** (12 comments, 👍2)
  Security regression blocking secret injection for subprocesses. Diamond lobster rated, linked PR open.

## 5. Bugs & Stability

The stability landscape is dominated by **session state corruption, message delivery failures, and security boundary regressions:**

### 🔴 Critical / P1 Regressions Active Today

| Issue | Impact | Fix PR in Flight? |
|-------|--------|-------------------|
| [#91283 – `minSecurity` Rank Order Inverted](https://github.com/openclaw/openclaw/issues/91283) | Security bypass – "full" treated as most restrictive instead of least, clamping override incorrectly | 🔴 No fix PR yet – filed today |
| [#90991 – Cron Global Runtime State Contamination](https://github.com/openclaw/openclaw/issues/90991) | System-wide overload, transient failures | 🔴 No fix PR yet |
| [#91212 – Delivery Recovery Starts Before Channel Transport Ready](https://github.com/openclaw/openclaw/issues/91212) | Silent message loss on gateway restart | 🔴 No fix PR yet |
| [#88312 – Codex Turn-Completion Stall](https://github.com/openclaw/openclaw/issues/88312) | Provider-specific total failure for multi-tool turns | 🔴 Needs live repro |
| [#90639 – Compaction Safeguard Mode Wedges Sessions](https://github.com/openclaw/openclaw/issues/90639) | "Something went wrong" on Slack with no recovery; high token cost | 🟡 #90641 (preserve boundary replies) |
| [#90428 – Exec Tool Triggers SIGTERM on WSL2/Node 24](https://github.com/openclaw/openclaw/issues/90428) | Crashes on Windows Linux Subsystem | 🔴 No fix PR yet |

### 🟠 High-Severity (P2 with heavy user impact)

- [#40001 – Write Tool Lacks Append Mode](https://github.com/openclaw/openclaw/issues/40001) – Silent data loss from cron overwrites
- [#29387 – Bootstrap Files Silently Ignored](https://github.com/openclaw/openclaw/issues/29387) – Per-agent configuration broken
- [#29736 – Exec Approvals Path Ignores State Root](https://github.com/openclaw/openclaw/issues/29736) – Config persisted to wrong location
- [#87326 – Telegram Streaming Text Blocks Lost](https://github.com/openclaw/openclaw/issues/87326) – Intermediate content overwritten
- [#64664 – Approvals Lost on Gateway Restart](https://github.com/openclaw/openclaw/issues/64664) – Stale callbacks show confusing errors
- [#38622 – Workspace File Injector Ignores Symlinks](https://github.com/openclaw/openclaw/issues/38622) – Shared configs silently missing

### 🩹 Notable Fixes Landed or Close

- Mattermost 503 (#68113) — **Closed**
- Discord approval cards (#73802) — **Closed**
- Feishu dispatch crash (#88234) — **Closed**
- Sub-agent Google model 404 (#71932) — **Closed**
- Hono security CVE fix (#91303) — **PR open**
- Feishu rate-limit retry (#89659) — **PR open**
- Feishu typing indicator API fix (#69572) — **Awaiting maintainer**

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release (v2026.7 / imminent)

- **Runtime Self Context Config + Tool** (#90101) – First slice of a larger runtime offloading and cost-awareness initiative. A showcase feature with significant maintainer investment.
- **xAI Realtime Voice Provider** (#91308) – New provider integration expands the Talk platform. Rapidly moving.
- **Subagent `toolsAllow` Forwarding** (#78441) – ACP policy refinement eagerly awaited by multi-agent users.
- **Topic-Session Families** (#90916) – Isolated context lanes for chat-native assistants. Newly filed, may enter early design.

### Longer-Term Roadmap Signals

- **SQLite Session/Transcript Migration** (#88838) – The largest pending architecture change. The branch-by-abstraction strategy is publicly debated and proceeding.
- **Gateway-Lite Mode** (#86881) – Deterministic deployment without AI harness, for pure automation users.
- **Bounded Append Semantics for Memory Flush** (#90354) – Hard guardrails for pre-compaction writes.
- **Relative Token Thresholds for Compaction** (#87136) – To support models with wildly different context windows (e.g., DeepSeek 1M vs GLM 200K).
- **Configurable Session Startup Message** (#45501) – Small UX change, high demand.
- **Lightweight Slug Generator** (#33962) – Avoid using the primary model just to name memory files.

## 7. User Feedback Summary

### 💢 Pain Points (Vocal Dissatisfaction)

1. **Data Integrity Fears Dominate**
   *"My cron jobs are silently destroying my memory files"* – Write tool append mode (#40001).
   *"Delivery recovery says 0 recovered, N failed, messages gone"* – Gateway restart message loss (#91212).
   *"I flush my context and it takes down my whole Slack session"* – Compaction safeguard wedging (#90639).

2. **Security Trust Deficit**
   The inverted `minSecurity` (#91283) combined with the ongoing "tool call text leak" (#25592) and "env vars ignored" (#31583) creates a perception that security boundaries are not yet rigorous enough for production/enterprise use.

3. **Configuration Confusion**
   The "bootstrap files silently ignored" bug (#29387) makes it hard to set up per-agent personalities. The Onboard UI failing to overwrite provider configurations (#38657) creates a frustrating "UI says saved, nothing changed" loop.

4. **Integration Frustration**
   Feishu users are the most vocal reporters (rate limits, wiki pagination, typing indicator). Mattermost and Discord regressions are causing trust issues with community-driven enterprise adoptions.

### 😊 Satisfaction Signals

- **High engagement on architecture.** The SQLite migration thread (#88838) shows users are deeply technical and invested in the project's future.
- **Quality over quantity.** Despite the bug count, the community-submitted PRs are substantive (xAI voice, Runtime Self Context, Feishu VC integration).
- **Triage is working.** The `clawsweeper` labels (needs-maintainer-review, queueable-fix, fix-shape-clear) show systematic handling of the load.

## 8. Backlog Watch

### 🐌 Stale Giants (Open > 2 Months, P1/P2, Awaiting Decision or Review)

| Issue | Filed | Danger |
|-------|-------|--------|
| [#25592 – Text leaks to channels](https://github.com/openclaw/openclaw/issues/25592) | Feb 26 | Needs product decision, security review |
| [#29387 – Bootstrap files ignored](https://github.com/openclaw/openclaw/issues/29387) | Feb 28 | Needs product decision |
| [#29736 – Exec approvals path](https://github.com/openclaw/openclaw/issues/29736) | Feb 28 | Core config rooted incorrectly |
| [#31583 – Exec tool env vars](https://github.com/openclaw/openclaw/issues/31583) | Mar 2 | Security regression, linked PR open |
| [#40001 – Write tool append mode](https://github.com/openclaw/openclaw/issues/40001) | Mar 8 | Data loss, linked PR open |
| [#38622 – Symlinks in workspace](https://github.com/openclaw/openclaw/issues/38622) | Mar 7 | Security review needed |
| [#38657 – Onboard UI fails](https://github.com/openclaw/openclaw/issues/38657) | Mar 7 | Product decision needed |

### ⏳ High-Value PRs Waiting on Maintainer or Author

- [#46303 – Drain inbound debounce buffer before reload](https://github.com/openclaw/openclaw/pull/46303) (Mar 14 – **P1, X-Large**)
  *A massive data-loss fix for SIGUSR1 reloads. One of the oldest P1 PRs open. Needs prioritization.*
- [#75025 – Refresh stale heartbeat timestamp](https://github.com/openclaw/openclaw/pull/75025) (Apr 30 – P2)
  *Stale since April. Simple fix with outsize impact on cron/heartbeat reliability.*
- [#87380 – Persist configured extra CA certs](https://github.com/openclaw/openclaw/pull/87380) (May 27 – P1)
  *Waiting on author, critical for enterprise/managed gateway installs.*
- [#90500 – Fix stale session routes for removed providers](https://github.com/openclaw/openclaw/pull/90500) (Jun 5 – P1)
  *Waiting on author. Session corruption fix.*
- [#91305 – Control UI bootstrap config endpoint](https://github.com/openclaw/openclaw/pull/91305) (Jun 8 – P1)
  *Waiting on author. Freshly filed but blocks web UI access on default routes.*

### Summary Assessment
**Project Health:** ⚕️ Fair / Elevated Temperature
The project is moving at an incredible pace but is sustaining a number of dangerous open wounds (security inversions, silent data loss, session wedge states) that need to be closed before the next release. The community engagement is excellent, and the architectural direction (SQLite, Self Context, Topic Families) is ambitious. The immediate priority should be resolving the **critical security and data-loss P1s** (#91212, #91283, #90991, #90639) and pushing through the stalled P1 PRs (#46303, #90500). The maintainer team's triage infrastructure (`clawsweeper`) is a clear strength, but product decisions and security reviews remain a bottleneck on several blockbuster issues.

---

## Cross-Ecosystem Comparison

## Cross-Project Ecosystem Comparison Report: Personal AI Agent Open-Source Landscape
**Date:** 2026-06-08 | **Analyst:** Ecosystem Intelligence

---

### 1. Ecosystem Overview

The open-source Personal AI Agent ecosystem on June 8, 2026, is characterized by extreme activity bifurcating into two tracks: the consolidation of full-stack "operating systems" (OpenClaw, IronClaw) and the sharpening of specialized "tools" (Hermes for orchestration, NanoBot for memory, PicoClaw for trading). A universal "Context/Memory Crunch" dominates technical discussions as users demand sessions that are both infinite and performant. Simultaneously, the rapid implementation of A2A (Agent-to-Agent) protocols across major players signals a decisive shift from monolithic agents to interoperable agent meshes. The ecosystem is maturing from experimental curiosity into production engineering, but carries significant friction from rapid past growth in the form of security regressions and data integrity bugs that projects are now urgently closing ranks to address.

---

### 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Releases (24h) | Health / Phase |
|---|---|---|---|---|
| **OpenClaw** | 294 | 500 | None | Fair / High-Velocity Stabilization |
| **Hermes Agent** | 50 | 50 | None | Robust / Feature-Driven Iteration |
| **IronClaw** | 50 | 38 | None (Blocked) | Build Phase / "Reborn" Rewrite |
| **ZeroClaw** | 50 | 50 | Pending (v0.8.0) | Intense Pre-Release |
| **CoPaw** | 22 | 10 | None | Strained / Regression Management |
| **PicoClaw** | 21 | 20 | Nightly (v0.2.9) | Strong / Active Feature Development |
| **LobsterAI** | 15 | 2 | None | Strained / Backlog Aging |
| **NanoBot** | 8 | 22 | None | Maturing / Core Infrastructure Investment |
| **NanoClaw** | 2 | 9 | None | Healthy / Stability Patches |
| **Moltis** | 1 | 0 | None | Low Activity |
| **NullClaw / TinyClaw / ZeptoClaw** | 0 | 0 | N/A | Dormant |

---

### 3. OpenClaw's Position

OpenClaw remains the community **center of gravity** and de facto reference implementation, leading in raw activity volume by a wide margin (294 Issues, 500 PRs). Its core advantage is **breadth and depth of enterprise-ready infrastructure**: formal security policy enforcement (`minSecurity`), strategic architecture shifts via branch-by-abstraction (SQLite migration #88838), and comprehensive channel coverage (Discord, Feishu, Telegram, Mattermost). The maintainer-team's triage infrastructure (`clawsweeper`) demonstrates systematic operational maturity absent in younger projects.

**Compared to peers:**

- **vs. Hermes Agent:** Hermes ships top community requests with significantly higher velocity (A2A protocol PR #41711 landed same day). OpenClaw deliberates features longer (Subagent `toolsAllow` #78441) and carries more organizational debt from its larger community surface.

- **vs. ZeroClaw:** ZeroClaw innovates aggressively on Developer Experience (async message queue #7190, live model switching #7209). OpenClaw's larger architectural surface makes it slower to adopt UX breakthroughs; its WebUI is functional but its core logic bears more abstraction weight.

- **vs. NanoBot:** NanoBot operates as a specialized laboratory for context optimization (Dynamic Pressure #4238, prompt bloat fixes). OpenClaw's context management is broader but currently struggling with specific regressions (compaction wedging #90639) that NanoBot is proactively avoiding through tighter scope.

- **Key Weakness:** Feature velocity relative to community expectations. Several top-voted issues languish in `needs-product-decision` while smaller projects ship quickly. The project delivers stability at the cost of perceived responsiveness.

---

### 4. Shared Technical Focus Areas

The community's technical priorities converge across four core systems:

| Focus Area | Active Projects | Specific Manifestations |
|---|---|---|
| **Memory & Context Governance** | OpenClaw, NanoBot, Hermes, ZeroClaw | SQLite migration (#88838), Dynamic Context Pressure (#4238), Durable Archive (#35186), Bounded Memory Strategies (#7234) |
| **Agent-to-Agent Protocols** | Hermes, ZeroClaw, OpenClaw | A2A protocol (#41711, #3566), Subagent toolsAllow forwarding (#78441) |
| **Security Hardening** | OpenClaw, NanoBot, NanoClaw, ZeroClaw, PicoClaw | `minSecurity` inversion (#91283), Bubblewrap sandbox (#4236), MCP auth bypass (#2711), file_write trust (#4627), token revocation (#7243) |
| **Multi-Provider Integration** | OpenClaw, ZeroClaw, CoPaw, PicoClaw | xAI Voice (#91308), Schema v3 provider expansion (#7260), local model regression (#4989), Kagi Search (#3037) |

The **Memory & Context Management** cluster is the defining technical battle of the ecosystem. Every major project is investing heavily in solving the "infinite context" problem without losing performance or data integrity.

---

### 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | NanoBot | IronClaw |
|---|---|---|---|---|---|
| **Target User** | Enterprise / Platform Builder | Multi-Agent Power User | Hacker / Developer | Memory & Context Engineer | Large-Scale Deployer |
| **Core Strength** | Security & Architecture | Orchestration (A2A) | Developer Experience (UX) | Context Optimization | "Reborn" Architecture |
| **Primary Surface** | Web + Chat Channels | Desktop + CLI + A2A | TUI / CLI | API / WebUI | API / WebChat v2 |
| **Architecture** | Heavy abstraction (branch-by-abstraction) | Plugin-based, modular | Schema v3, micro-services | Tightly scoped, Python | Rust-based, WASM, multi-service |
| **Release Cadence** | Stable trains (2026.6.x) | Continuous pre-release | v0.8.0 imminent | No cadence established | Blocked (v0.24 -> v0.29) |
| **Community Dynamic** | Large, formal triage | Responsive maintainers | Prolific contributors | Deep technical debates | Internal team-driven |
| **Weakness** | Slower feature velocity | Platform parity (Win/Mac gaps) | S0 bug risk (file_write) | Narrower feature surface | Release bottleneck |

**CoPaw** occupies a distinct niche as the **Chinese enterprise ecosystem leader**, with deep integration into WeCom, DingTalk, and Yuanbao channels—a domain where Western-centric projects (OpenClaw, Hermes) have limited presence. Its struggles with Windows MAX_PATH (#4988) and local model regressions (#4989) reflect different platform priorities.

**PicoClaw** is executing the clearest **vertical specialization pivot** with its ClawTrade engine (#3024–#3032), AI-powered trading. This represents a departure from general-purpose agenting into a high-value, capital-markets use case.

**LobsterAI** and **Moltis** occupy the "utility agent" space with smaller scopes (mobile UI, skills management) but lack the development velocity to compete with the top tier.

---

### 6. Community Momentum & Maturity

**Tier 1 — High-Frequency Iteration:**
- **ZeroClaw**: Most aggressive feature velocity. Closing S1 issues and landing major UX breakthroughs daily. Pre-release energy is palpable.
- **Hermes Agent**: Best "feature request to shipment" pipeline. A2A protocol turnaround (<24 hours) sets the gold standard for community responsiveness.
- **OpenClaw**: Highest raw throughput, but volume is a mix of innovation and heavy regression triage. The project is operating at maximum capacity.

**Tier 2 — Transition & Deep Investment:**
- **IronClaw**: Entirely consumed by its "Reborn" rewrite. No releases, but massive internal investment. High risk / high reward.
- **CoPaw**: Managing the hangover of a rapid release (v1.1.10 regressions) while migrating to AgentScope 2.0. Spinning multiple plates.
- **NanoBot**: Deepening core context management infrastructure. Low PR count but high intellectual weight in each submission.

**Tier 3 — Stabilization & Niche Execution:**
- **PicoClaw**: Clean execution with nightly builds and a clear vertical pivot. Strong engagement from a focused contributor base.
- **NanoClaw**: Lean operations, merging stability patches for deployment reliability.

**Tier 4 — Strained / Dormant:**
- **LobsterAI**: Critical bugs aging (April 7 issues stale) with low PR throughput. Maintainer bandwidth is the primary risk.
- **Moltis, NullClaw, TinyClaw, ZeptoClaw**: Effectively dormant. Illustrates the high metabolic cost of staying relevant.

---

### 7. Trend Signals

**1. The Session Integrity Imperative**
Silent data loss is the ecosystem's unforgivable sin. Projects with broken delivery recovery (OpenClaw #91212), silent history truncation (NanoBot #4203), config corruption crashes (CoPaw #4970), or invisible file writes (ZeroClaw #4627) face the sharpest user backlash. The universal demand is: *"Never lose my work."*

**2. Agent-to-Agent (A2A) is the New API Gateway**
Hermes shipping A2A (#41711) and ZeroClaw prioritizing it (#3566) confirms the industry shift. The monolithic single-agent paradigm is actively retrenching in favor of interoperable agent meshes. Platforms that lock agents into closed communication channels face a structural disadvantage.

**3. The Post-LLM Optimization Era**
Features like Skill Compilation (ZeroClaw #5146), Bounded Append Semantics (OpenClaw #90354), and Dynamic Context Pressure (NanoBot #4238) treat the LLM as a constrained resource to be engineered around—not just a black box API. The era of naive "stuff everything into the prompt" is ending, replaced by structured memory lifecycles and token budgets.

**4. Security Boundaries are Mainstream, Not Enterprise**
The severity of issues like `minSecurity` inversion (OpenClaw #91283), MCP auth bypass (NanoClaw #2711), and sandbox escapes on modern Linux kernels (NanoBot #4236) demonstrates that self-hosted users demand enterprise-grade security boundaries. Open-source projects can no longer rely on "trusted network" models.

**5. Developer Experience (DX) Divides Winners from Survivors**
Projects with aggressive UX investment (ZeroClaw's TUI innovations, Hermes' Desktop parity push) attract disproportionately high community contribution volume. Projects with configuration friction (LobsterAI's OAuth workflows, CoPaw's release regressions) see their community energy diverted into complaint reports.

**6. Cost Optimization is a Feature, Not a Concern**
Token waste complaints (#2121 in LobsterAI, #5146 in ZeroClaw) represent direct economic feedback. Agents that are indifferent to their operational cost (e.g., unconditionally injecting full skill lists into every prompt) are losing users to more frugal architectures. The next competitive differentiator will be *agent cost-per-task* benchmarks.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 8, 2026.

---

## 1. Today’s Overview
NanoBot is in an intense period of stabilization and feature hardening, with 22 Pull Requests and 8 Issues actively updated in the last 24 hours. The community’s focus has sharply narrowed to critical infrastructure: session history management, sandbox security on modern Linux, and MCP transport robustness. While no new releases were cut, the sheer volume of sophisticated patches being submitted—and the speed at which maintainers are merging critical fixes—signals a project rapidly maturing for production workloads. The dominant theme is **context management**, with competing PRs and deep technical debates around prompt bloat and memory lifecycles.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Five pull requests were merged or closed today, indicating significant cleanup and feature integration:

- **Session & Prompt Management:** [#4244](https://github.com/HKUDS/nanobot/pull/4244) (merged) fixes a critical regression where disabling the Dream feature still injected all chat history into the system prompt.
- **WebUI Enhancement:** [#4240](https://github.com/HKUDS/nanobot/pull/4240) (merged) brings ANSI output rendering to code blocks, dramatically improving the terminal feedback loop for browser-based users.
- **Model Compatibility:** [#4227](https://github.com/HKUDS/nanobot/pull/4227) (merged) resolves a bug where custom providers (DeepSeek, Kimi) had their empty-string `reasoning_content` fields dropped, breaking tool calls.
- **Channel Integrations:** [#2885](https://github.com/HKUDS/nanobot/pull/2885) (Feishu mention resolution) and [#2663](https://github.com/HKUDS/nanobot/pull/2663) (WhatsApp LID group mentions) both closed, stabilizing two major community channels.

## 4. Community Hot Topics
The most active discussions revolve around the core agent loop and state management:

- **Session History Truncation ([#4203](https://github.com/HKUDS/nanobot/issues/4203)):** A detailed bug report from *huji820* reveals a logic flaw in `find_legal_message_start` that silently drops the entire conversation history when an orphaned tool result trails a user message. This has spawned a fix PR ([#4219](https://github.com/HKUDS/nanobot/pull/4219)) and represents the highest-stakes stability concern today.
- **Context Bloat ([#4242](https://github.com/HKUDS/nanobot/issues/4242)):** The revelation that disabling Dream still injects all history prompted an unusually competitive response, with two independent fix PRs ([#4243](https://github.com/HKUDS/nanobot/pull/4243) and [#4244](https://github.com/HKUDS/nanobot/pull/4244)) submitted within hours. The underlying need is clear: users demand predictable, configurable memory management.
- **Subagent Orchestration ([#4231](https://github.com/HKUDS/nanobot/issues/4231)):** A request for a `model` parameter on the `spawn` tool received zero comments but represents a high-demand use case for users building complex multi-agent workflows with specialized models.

## 5. Bugs & Stability
**Critical:**
- **Bubblewrap Sandbox Failures:** Two related reports from *primit1v0* indicate the sandbox is currently broken on modern distributions. [#4236](https://github.com/HKUDS/nanobot/issues/4236) notes total failure on Ubuntu 24.04 due to restricted user namespaces. [#4237](https://github.com/HKUDS/nanobot/issues/4237) identifies that `$HOME` is not overridden, breaking any tool that tries to write to the home directory. A fix PR for the latter exists ([#4239](https://github.com/HKUDS/nanobot/pull/4239)).
- **API Duplication ([#4234](https://github.com/HKUDS/nanobot/pull/4234)):** The OpenAI-compatible API handler retries empty responses, causing user turns to be silently duplicated in session history. A fix PR is open by *michaelxer*.

**High:**
- **Session Data Loss:** [#4203](https://github.com/HKUDS/nanobot/issues/4203) remains a high-severity risk for any user with complex tool-use patterns.

**Medium:**
- **MCP Transport Timeout ([#4230](https://github.com/HKUDS/nanobot/pull/4230)):** The `streamableHttp` MCP client creates a connection with `timeout=None`, risking indefinite hangs. Fix PR open.
- **Workspace Escape ([#4119](https://github.com/HKUDS/nanobot/pull/4119)):** A security fix blocking relative symlink escapes in the exec sandbox remains open.

## 6. Feature Requests & Roadmap Signals
The development trajectory points toward a more robust, self-aware agent platform:

- **Predictive (Likely Next Release):**
    - *Dynamic Context Pressure:* PR [#4238](https://github.com/HKUDS/nanobot/pull/4238) moves compaction logic from a fixed tool-result count to actual turn-internal context pressure. This is a sophisticated architectural leap for memory management.
    - *Version Awareness:* PR [#4235](https://github.com/HKUDS/nanobot/pull/4235) adds version display and upgrade checks to the WebUI Settings panel.
    - *Shared Transcription:* PR [#4232](https://github.com/HKUDS/nanobot/pull/4232) centralizes voice input as a core capability rather than a channel-specific feature.
- **Long-term Signals:**
    - *Advanced Orchestration:* [#4231](https://github.com/HKUDS/nanobot/issues/4231) (Subagent model override) and [#4238](https://github.com/HKUDS/nanobot/pull/4238) (Context governance) suggest the project is moving towards structured, multi-model agent workflows.
    - *Strict Tool Validation:* PR [#4190](https://github.com/HKUDS/nanobot/pull/4190) indicates a push to harden the tool-use pipeline, rejecting invalid arguments rather than silently repairing them.

## 7. User Feedback Summary
- **Pain Points:** The dominant theme is **context window unpredictability**. Users report opaque history truncation ([#4203](https://github.com/HKUDS/nanobot/issues/4203)), silent prompt bloat ([#4242](https://github.com/HKUDS/nanobot/issues/4242)), and sandboxing friction on modern Linux distributions ([#4236](https://github.com/HKUDS/nanobot/issues/4236)). API users are frustrated by duplicate turns on error ([#4234](https://github.com/HKUDS/nanobot/pull/4234)).
- **Use Cases:** Requests for version awareness ([#4233](https://github.com/HKUDS/nanobot/issues/4233)) and subagent model overrides ([#4231](https://github.com/HKUDS/nanobot/issues/4231)) reveal a user base graduating from hobbyist chat to production deployments requiring observability and orchestration.
- **Satisfaction:** The project enjoys highly sophisticated community contributions. Multiple users (*yu-xin-c, michaelxer, chengyongru, primit1v0*) are submitting well-scoped, architecturally sound fix PRs. The maintainer team is responsive, merging urgent fixes like [#4227](https://github.com/HKUDS/nanobot/pull/4227) and [#4244](https://github.com/HKUDS/nanobot/pull/4244) rapidly.

## 8. Backlog Watch
While the project demonstrates excellent throughput, several substantial Open PRs require continued reviewer bandwidth to prevent staleness:

- **Test Infrastructure:** [#3982](https://github.com/HKUDS/nanobot/pull/3982) (scripted agent runner harness) and [#4193](https://github.com/HKUDS/nanobot/pull/4193) (memory lifecycle harness) from contributor *yu-xin-c* are foundational for QA but large in scope.
- **MCP Security:** [#4123](https://github.com/HKUDS/nanobot/pull/4123) (reject unsafe HTTP URLs before probe) has been open since May 31. Given the centrality of MCP to the plugin ecosystem, this security hardening deserves high priority for merging.
- **Tool-Call Contracts:** [#4190](https://github.com/HKUDS/nanobot/pull/4190) (Improve tool call validation strictness) has been open since June 4. It changes the error-handling contract for tools, which has broad downstream implications for agent reliability.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Project Digest for Hermes Agent — 2026-06-08

## 1. Today's Overview
Today saw exceptionally high development velocity with **50 issues and 50 PRs updated**, making it one of the most active days in the project's recent history. The standout event was the submission of a consolidated pull request for Google's A2A (Agent-to-Agent) protocol support by project lead teknium1, directly addressing the community's most upvoted feature request. The team simultaneously closed several critical P1/P2 bugs, including a conversation compression desync causing silent message loss and a broken delegation configuration from v0.14.0. Platform stability remains a key focus, with specific watchdog and crash recovery improvements landing for Windows and macOS. Overall project health is very robust, characterized by rapid feature iteration and strong maintainer responsiveness to community pain points.

## 2. Releases
No new releases were published today. The project is in an active pre-release cycle with substantial infrastructure changes in progress.

## 3. Project Progress
The project advanced significantly on several fronts, with 4 PRs merged/closed. Key developments include:

- **Agent-to-Agent Protocol (A2A):** PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) delivers a plugin-based implementation of the A2A protocol, enabling remote agent discovery and standardized inter-agent communication without any core code edits. This closes the top community feature request.

- **Desktop Application:** Major UX improvements landed. PR [#39474](https://github.com/NousResearch/hermes-agent/pull/39474) adds a "send to all" concurrent broadcast across profiles. PR [#41670](https://github.com/NousResearch/hermes-agent/pull/41670) introduces hover-reveal collapsed sidebars. PR [#41762](https://github.com/NousResearch/hermes-agent/pull/41762) routes assistant preview links through a dedicated file-tab system.

- **Infrastructure & Configuration:** PR [#41741](https://github.com/NousResearch/hermes-agent/pull/41741) allows profiles to inherit config from the default profile via `inherit: true`, reducing configuration overhead. PR [#41765](https://github.com/NousResearch/hermes-agent/pull/41765) implements periodic checkpointing of streaming content to preserve partial responses during gateway crashes.

- **Platform Support:** PR [#41761](https://github.com/NousResearch/hermes-agent/pull/41761) establishes a Windows Scheduled Task watchdog for the gateway cron scheduler. PR [#36286](https://github.com/NousResearch/hermes-agent/pull/36286) adds a `minimax-cn-oauth` provider for China-region OAuth endpoints.

- **Automation & Extensibility:** PR [#41309](https://github.com/NousResearch/hermes-agent/pull/41309) introduces "Cron Recipes"—parameterized automation templates that work across CLI, Desktop, TUI, and messengers. PR [#41767](https://github.com/NousResearch/hermes-agent/pull/41767) adds an `agenticboxes-email` skill. PR [#41752](https://github.com/NousResearch/hermes-agent/pull/41752) adds an `on_session_title` plugin hook.

## 4. Community Hot Topics

- **[A2A Protocol Support (#514)](https://github.com/NousResearch/hermes-agent/issues/514):** The most active topic by a wide margin with 20 comments and 18 👍 reactions. Users are heavily invested in agent interoperability, citing use cases like multi-agent creative production teams. The consolidated implementation PR was opened the same day, showcasing exceptional maintainer responsiveness.

- **[OpenAI Codex Reauthentication Loop (#6653)](https://github.com/NousResearch/hermes-agent/issues/6653):** A persistent frustration where switching between local and cloud models across profiles triggers needless re-authentication. This issue has been open since April 9 and remains a top pain point for multi-profile power users.

- **[Kanban Board Desktop Integration (#41222)](https://github.com/NousResearch/hermes-agent/issues/41222):** Filed yesterday but quickly gained traction. Users seek to unify the Kanban multi-agent workflow tool directly into the Desktop app, eliminating friction of separate CLI terminals.

- **[Memory Management Pain Points (#32064, #35186)](https://github.com/NousResearch/hermes-agent/issues/32064):** Two related issues highlighted significant dissatisfaction with the bounded memory system, which forces manual deletion of entries without an archive or offload path, leading to permanent loss of operator corrections.

## 5. Bugs & Stability

The team swept several critical bugs from the tracker today while new platform-specific issues emerged.

**Resolved (High/Critical):**
- **[#34089](https://github.com/NousResearch/hermes-agent/issues/34089) - P1:** Conversation compression desynchronizing session ID, causing silent message loss. **Closed.**
- **[#32671](https://github.com/NousResearch/hermes-agent/issues/32671) - P2:** All `delegation.*` settings silently ignored in v0.14.0, breaking subagent routing. **Closed.**
- **[#27918](https://github.com/NousResearch/hermes-agent/issues/27918) - P2:** GPT-5.5 context window truncated to 272K instead of 1M. **Closed.**
- **[#13631](https://github.com/NousResearch/hermes-agent/issues/13631) - P2:** Honcho system prompt rebuilds invalidating KV cache. **Closed.**
- **[#15275](https://github.com/NousResearch/hermes-agent/issues/15275) - P2:** Duplicate `hermes mcp serve` subprocesses spawned by TUI. **Closed.**

**New Bugs Reported Today (Ranked by Severity):**
- **[#41662](https://github.com/NousResearch/hermes-agent/issues/41662) - P2 (Windows):** Gateway cron scheduler stops entirely if the gateway crashes; `os.kill(pid,0)` broken on Windows. **Fix PR [#41761](https://github.com/NousResearch/hermes-agent/pull/41761) already exists.**
- **[#41676](https://github.com/NousResearch/hermes-agent/issues/41676) - P2 (macOS):** Launchctl fallback gateway fails health checks after upgrade, triggering infinite `--replace` restart loop for Telegram.
- **[#41660](https://github.com/NousResearch/hermes-agent/issues/41660) - P2 (WhatsApp):** Sending messages with bare phone numbers fails with a 500 error due to missing `@s.whatsapp.net` JID suffix.
- **[#41737](https://github.com/NousResearch/hermes-agent/issues/41737) - P3 (Linux):** Desktop update reaches 100% and freezes indefinitely; Electron process never exits.
- **[#41669](https://github.com/NousResearch/hermes-agent/issues/41669) - P3 (Desktop/Gateway):** File attachments return "file not found" errors in Gateway mode.
- **[#41686](https://github.com/NousResearch/hermes-agent/issues/41686) - P3 (Terminal Tool):** `_get_env_config()` crashes with `FileNotFoundError` when worker CWD is deleted.
- **[#39685](https://github.com/NousResearch/hermes-agent/issues/39685) - P3 (Xiaomi Vision):** Native fast path sends multimodal results Xiaomi API rejects with 400, poisoning the session.

## 6. Feature Requests & Roadmap Signals

Today's activity strongly indicates the direction of the next release cycle.

- **Imminent (In Review):**
    - **A2A Protocol:** PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) is the flagship feature and likely to merge imminently.
    - **Desktop Feature Completion:** Multiple PRs ([#41670](https://github.com/NousResearch/hermes-agent/pull/41670), [#41762](https://github.com/NousResearch/hermes-agent/pull/41762), [#41747](https://github.com/NousResearch/hermes-agent/pull/41747)) signal a push to bring the Desktop app to full parity with other surfaces.

- **High Community Interest:**
    - **Cron Recipes ([#41309](https://github.com/NousResearch/hermes-agent/pull/41309)):** This parameterized automation model could significantly democratize scheduled task creation for non-technical users.
    - **Durable Memory Archive ([#35186](https://github.com/NousResearch/hermes-agent/issues/35186), [#32064](https://github.com/NousResearch/hermes-agent/issues/32064)):** The lack of an offload path for bounded memory remains an infuriation point for power users.

- **Prediction:** The next release will be heavily branded around **Agent Interoperability (A2A)** and **Platform Maturity** (Windows gateway stability, Desktop UX enhancements, Cron automation). Expect a version bump following the A2A and desktop batch.

## 7. User Feedback Summary

- **Satisfaction:** Enthusiasm is high for the A2A protocol integration. Users are actively envisioning complex multi-agent ecosystems (AI anime production studios, professional writing clusters). The maintainers' practice of shipping fixes on the same day as bug reports is clearly appreciated.

- **Dissatisfaction / Pain Points:**
    - **Reliability Gaps:** The silent message loss bug ([#34089](https://github.com/NousResearch/hermes-agent/issues/34089)) eroded trust, though now fixed. The delegation configuration failure in v0.14.0 ([#32671](https://github.com/NousResearch/hermes-agent/issues/32671)) caused significant workflow disruption.
    - **Auth Friction:** The OpenAI Codex re-auth loop ([#6653](https://github.com/NousResearch/hermes-agent/issues/6653)) is a top pain point for users managing multiple profiles.
    - **Platform Parity:** Windows users gap in cron watchdog reliability, Linux users report a broken desktop updater ([#41737](https://github.com/NousResearch/hermes-agent/issues/41737)).
    - **Feature Gaps:** Users want seamless Kanban board integration in the Desktop app, better webhook setup flows ([#24911](https://github.com/NousResearch/hermes-agent/issues/24911)), and a non-destructive memory management system.

## 8. Backlog Watch

- **[#6653](https://github.com/NousResearch/hermes-agent/issues/6653) (OpenAI Codex Reauth Loop):** This is the most significant issue currently open without an attached fix PR. Created April 9, active for 60 days, affecting a core workflow for multi-profile power users. Urgently needs maintainer triage for a fix.

- **[#24911](https://github.com/NousResearch/hermes-agent/issues/24911) (Webhooks Missing in Setup Wizard):** A relatively simple configuration/UI bug open since May 13, 2026. No maintainer response recorded in the top comments. Users following documentation expect a menu option that does not appear.

- **[#514](https://github.com/NousResearch/hermes-agent/issues/514) (A2A Protocol Support):** While functionally resolved by the open PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711), the issue itself remains open. Should be closed once the PR merges to clean up the tracker.

- **[#41222](https://github.com/NousResearch/hermes-agent/issues/41222) (Kanban in Desktop):** Filed only yesterday, but represents a major integration request that will likely become a highly watched and demanded feature.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw Project Digest — 2026-06-08**

### 1. Today's Overview
PicoClaw experienced exceptionally high development velocity over the last 24 hours, with **21 Issues** and **20 Pull Requests** updated—marking one of the most active days in recent history. The project is laying the architectural groundwork for a major new expansion: the **ClawTrade** AI-powered trading engine (Issues [#3024](#) – [#3032](#)), signaling a strategic pivot toward automated exchange connectivity and risk management. Simultaneously, contributor **chengzhichao-xydt** drove a sweeping code-hardening effort, patching dozens of unchecked errors, type assertions, and ignored `Close()` calls across the codebase. A new nightly build `v0.2.9-nightly.20260608` was published, responding to the community’s repeated calls for a faster release cadence. Overall, project health is **strong**, with rapid triage of critical bugs and ambitious feature development proceeding in parallel.

---

### 2. Releases
A **nightly build** was published today:

- **v0.2.9-nightly.20260608.875cf4a2**
    - *Type:* Automated nightly build.
    - *Stability warning:* May be unstable; intended for early testing.
    - *Changelog:* [Compare v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
    - *Notes:* This build incorporates the new ClawTrade structural foundations and the recent wave of error-handling stability fixes. No breaking changes or migration notes were provided for this specific nightly.

---

### 3. Project Progress
**11 Pull Requests** were merged or closed in the last 24 hours, spanning new features, documentation, and a major reliability push.

- **🚀 New Features & Architecture**
    - **ClawTrade Engine**: A complete batch of foundational code was merged by **jcafeitosa**, establishing the new trading subsystem:
        - `Exchange` interface and Go types ([#3024])
        - Binance WebSocket and REST connectors ([#3025], [#3026])
        - Lock-free order book ring buffer ([#3027])
        - Latency benchmarks ([#3028])
        - `RiskManager` interface ([#3029])
        - `ClawHub` message core ([#3030])
        - CI/CD pipeline ([#3031])
        - `clawtrade` CLI structure ([#3032])
    - **Kagi Search Provider**: Native integration of Kagi Search into the web search provider system ([PR #3037]).
    - **Skills Path Filtering**: Skills requiring missing binaries are now automatically skipped from the system prompt ([PR #2936], fixes [#2351]).

- **📚 Documentation**
    - **Android Termux Guide**: Dedicated guide for running PicoClaw on ARM64 Android via Termux ([PR #2902], closes [#286]).

- **🛠️ Code Hardening & Bugs**
    - Added proper `ok` checks for unchecked type assertions in agent startup, model probes, and the LINE channel ([PR #3046], [PR #3040], [PR #3018]).
    - Fixed silent `Close()` error swallowing on writable files and downloads ([PR #3034], [PR #3035], [PR #3033]).
    - Corrected `fmt.Errorf` wrapping to use `%w` instead of `%v` ([PR #3051]).
    - Fixed Anthropic default model ID (dots → hyphens) ([PR #3036], closes [#2941]).
    - Improved message bus backpressure handling and health visibility ([PR #2906]).

---

### 4. Community Hot Topics
- **Release Velocity & Feature Waiting**: Issue [#2952] reflected strong community frustration over the interval between stable releases, specifically calling out bugs in `exec` commands and QQ channels that required a new version. The project responded with accelerated nightly builds.
- **Provider Setup Friction**: Issue [#2674] (Codex OAuth empty streaming responses) and [#2941] (Anthropic model ID parsing failure) drew significant attention. The Anthropic bug was fixed same-day in [PR #3036], demonstrating responsive maintainership.
- **`mcp add` Flag Parsing Bug**: Contributor **carlosprados** filed a highly detailed bug report ([#3041]) showing that global flags break the `mcp add` command. A fix ([PR #3048]) was opened within hours, showcasing an engaged and technically sophisticated community.
- **Telegram Quality-of-Life**: [PR #2975] (treating reply-to-bot as @mention in groups) remains a popular open item for Telegram users but has been labeled stale.

---

### 5. Bugs & Stability
- **🔴 High Severity (Open)**
    - **Matrix `allow_from` Access Control Broken ([#3044])**: Standard Matrix user IDs containing colons (`@user:domain`) are silently rejected, breaking access control for non-trivial Matrix deployments. A fix is in review ([PR #3045]).
    - **`mcp add` Flag Parsing Broken ([#3041])**: Root-level flags like `--no-color` are mis-parsed as positional arguments, breaking HTTP/SSE server additions. A fix is proposed in [PR #3048].

- **🟡 Medium Severity (Open)**
    - **Telegram Location Messages Ignored ([#3049])**: Sending a location pin yields no reaction or log output.

- **✅ Addressed / Closed**
    - **Anthropic Model ID** ([#2941]): Fixed by [PR #3036].
    - **Codex OAuth Empty Responses** ([#2674]): Resolved.
    - **Systemic Defensive Coding**: A large batch of patches merged today addresses a class of "silent failure" bugs—unchecked `Close()` errors, discarded `Getwd()` errors, and missing type assertion checks—significantly reducing risk of data corruption or runtime panics.

---

### 6. Feature Requests & Roadmap Signals
- **🔮 Strategic Roadmap Signal – `ClawTrade`**: The structural foundations merged today ([#3024]–[#3032]) represent a clear and ambitious strategic expansion into AI-driven trading agents. Expect an `Exchange` framework, `RiskManager` interface, and multi-exchange connectivity to feature heavily in the next minor or major release.
- **Open Feature Requests Likely for Next Release:**
    - **OmniRoute Provider** ([#2978]): Low-effort community request to add OmniRoute as a supported provider.
    - **Telegram Reply-to-Mention** ([PR #2975]): A polished QoL feature awaiting final maintainer review.
- **Kagi Search**: Already merged ([PR #3037]), this was a high-demand feature.

---

### 7. User Feedback Summary
- **Pain Points**
    - *Release Pace*: Users explicitly asked for more frequent stable releases ([#2952]), citing specific bugs they hoped a new version would fix. The nightly builds are a direct response.
    - *Provider Configuration*: Multi-step or fragile setup flows (Codex OAuth, custom model IDs) remain a recurring friction point ([#2674], [#2941], [#2978]).
    - *Platform-Specific Regressions*: Raspberry Pi (Telegram), ARM (Termux), and Matrix deployments each encountered unique blocking bugs, highlighting the cost of maintaining a multi-platform agent.

- **Satisfactions**
    - *Responsiveness*: Critical bugs are frequently met with a fix PR within hours ([#2941], [#3041]).
    - *Feature Delivery*: Highly requested items like the Android Termux guide and Kagi search are actively being shipped.

---

### 8. Backlog Watch
- **[PR #2904]** — *Fix agent loop reload and panic cleanup stability*. Open since May 20, labeled stale. Addresses core agent runtime reliability; needs prompt maintainer review.
- **[PR #2975]** — *Telegram reply-to-bot as mention*. Open since May 30, labeled stale. Community-contributed feature with no recent activity from maintainers.
- **[#2978]** — *Add OmniRoute as provider*. Open since May 31, no maintainer acknowledgment. Feature requests left without response risk contributor churn.
- **Release Management Risk**: While [#2952] is closed, the underlying user sentiment about release cadence remains. Establishing a regular stable release cadence (e.g., monthly patches) would reduce pressure and improve project predictability.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest — 2026-06-08**

---

### 1. Today's Overview

NanoClaw saw **high development activity** on June 8, 2026, with **9 Pull Requests** updated and **2 Issues** receiving attention in the last 24 hours. Three PRs were merged, focusing on deployment safety, account reliability, and documentation improvements. While no new official release was published, the `main` branch absorbed several stability-critical patches. The project continues to see a healthy flow of well-structured community contributions, particularly around security boundaries, configuration architecture, and multi-agent trust models.

---

### 2. Releases

**No new releases.**  
The latest tagged version remains unchanged. Notable feature work and fixes merged to `main` today may form the basis for the next release candidate.

---

### 3. Project Progress

Three PRs were merged/closed today:

- **[PR #2707](https://github.com/nanocoai/nanoclaw/pull/2707) – Startup Tripwire & Upgrade Marker**  
  Enforces sanctioned upgrade paths (`/setup`, `/update-nanoclaw`). A raw `git pull` that skips migrations now fails loudly with a self-healing message instead of silently breaking the install.

- **[PR #2706](https://github.com/nanocoai/nanoclaw/pull/2706) – Account Rotation Fix**  
  Fixes cross-provider rotation errors (Codex/Gemini no longer pollute Anthropic rotation cycles), calibrates database cursor drift before switching, and adds SIGTERM → SIGKILL fallback for reliable agent cleanup.

- **[PR #2710](https://github.com/nanocoai/nanoclaw/pull/2710) – Ollama Prompt Caching Docs**  
  Documentation explaining how to bypass the cache-busting hash for faster local inference with the Claude-Code-CLI → Ollama path, a common performance pain point.

---

### 4. Community Hot Topics

- **[Issue #2312](https://github.com/nanocoai/nanoclaw/issues/2312) – CLAUDE.md Unconditional Deletion (2 comments)**  
  The most engaged item today. Users are frustrated that `migrateGroupsToClaudeLocal()` deletes a committed file on every startup, creating a permanently dirty working tree. The underlying tension is between Git-controlled repository structure and runtime lifecycle management.

- **[Issue #2711](https://github.com/nanocoai/nanoclaw/issues/2711) – Ungated Admin MCP Tool**  
  A newly filed security issue identifying that the `create_agent` tool, despite being documented as "admin-only," has no actual authorization guard. This is likely to generate significant discussion as it touches core trust assumptions in multi-container deployments.

- **[PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626) – Telegram Topic Isolation**  
  Open since early April and updated today. This large feature skill for multi-tenant Telegram auto-registration continues to draw attention from the self-hosted community seeking isolation between chat groups.

---

### 5. Bugs & Stability

**Ranked by severity:**

- **[HIGH] MCP Authorization Bypass ([#2711](https://github.com/nanocoai/nanoclaw/issues/2711))**  
  Any container can call `create_agent` despite documentation claiming admin-only. This is a critical trust-boundary flaw for deployments with untrusted agent containers. **No fix PR exists yet.**

- **[HIGH] Dirty Git Tree / File Deletion ([#2312](https://github.com/nanocoai/nanoclaw/issues/2312))**  
  Permanent working tree pollution on every restart. Breaks CI/CD pipelines and developer workflows. Unresolved for one month; an active community grievance.

- **[MEDIUM] OneCLI Gateway Bypass Broken ([PR #2705](https://github.com/nanocoai/nanoclaw/pull/2705))**  
  The `use-native-credential-proxy` skill silently fell back to the gateway rather than bypassing it. An open PR rewrites the credential detection logic to actually respect the configuration.

- **[MEDIUM] Orphaned Agent Containers ([PR #2708](https://github.com/nanocoai/nanoclaw/pull/2708))**  
  Agent containers left alive after service stop. Open PR adds proper reaping during shutdown.

- **[LOW] Duplicate Text in Poll Loop ([PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531))**  
  Mid-turn `send_message` can duplicate output. Fix open since May 18 awaiting final review.

---

### 6. Feature Requests & Roadmap Signals

- **DB-backed ContainerConfig ([PR #2709](https://github.com/nanocoai/nanoclaw/pull/2709))**  
  Implements database JSON columns for `env` and `blocked_hosts`. This modernizes configuration persistence and is a strong candidate for the next minor release, enabling dynamic container configuration without filesystem changes.

- **Telegram Topic Isolation ([PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626))**  
  Continues to be the longest-standing feature request for multi-tenant Telegram integration. Auto-registration and topic isolation address a core community use case.

- **Testing Infrastructure ([PR #2704](https://github.com/nanocoai/nanoclaw/pull/2704))**  
  Unit tests for `cli-agent parseArgs` signal a growing community investment in test coverage. This improves the codebase's ability to accept rapid contributions safely.

---

### 7. User Feedback Summary

**Pain Points:**

- **Trust & Security Boundaries:** Issue [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) reveals a gap between documented permissions and actual enforcement, a critical concern for operators running multi-agent systems.
- **Developer Experience:** Issue [#2312](https://github.com/nanocoai/nanoclaw/issues/2312) highlights friction between development workflow expectations (clean git tree) and framework runtime behavior.
- **Configuration Reliability:** PR [#2705](https://github.com/nanocoai/nanoclaw/pull/2705) reflects user frustration with proxy bypass configuration not working on real systemd/launchd installs.

**Positive Signals:**

- High contribution quality: 9 well-structured PRs in 24 hours indicates strong community satisfaction with the contribution process.
- The Ollama caching docs (PR [#2710](https://github.com/nanocoai/nanoclaw/pull/2710)) directly address a vocal user base running local inference.

---

### 8. Backlog Watch

Items that have lingered without maintainer resolution:

- **[Issue #2312](https://github.com/nanocoai/nanoclaw/issues/2312) – CLAUDE.md deletion**  
  Created May 6, updated June 7. Needs a maintainer decision: should the file be `.gitignore`d, moved, or should the migration function be refactored? Persistent community frustration.

- **[PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626) – Telegram Topic Isolation**  
  Open since April 4. A substantial feature skill that has been waiting over two months for a maintainer roadmap alignment decision.

- **[PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531) – Poll-loop Duplicate Text**  
  Open since May 18. A small, targeted bug fix that needs a final review to close out. Maintaining momentum on these "last mile" fixes prevents contributor churn.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-08

## 1. Today's Overview
IronClaw is in the midst of a massive, team-wide architectural transformation ("Reborn") focused on modularizing the host kernel, product workflow, and channel surfaces. Activity is at a fever pitch, with **50 issues and 38 pull requests updated in the last 24 hours**, reflecting a large, well-resourced team executing on multiple parallel workstreams. The overwhelming majority of motion is centered on landing product workflow facade components, stabilizing the WebChat v2 beta, and hardening security-sensitive extension and sandbox subsystems. No new releases were cut today; a critical release PR remains stranded in the backlog. The project is deep in a build-up phase, with intense forward motion on core architecture and relatively little community churn from external users.

## 2. Releases
**No new releases were published in the last 24 hours.** A significant release PR ([nearai/ironclaw#3708](https://github.com/nearai/ironclaw/pull/3708) — "chore: release") has been open since May 16, staging breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), with a version jump for the main binary from 0.24.0 to 0.29.1. Its staleness suggests the team is deferring distribution until the Reborn integration reaches a more stable head.

## 3. Project Progress
**16 pull requests were merged or closed in the past 24 hours.** Key advances include:

- **Product Workflow Refinement:** The critical `ProductWorkflow` facade was refactored into explicit `submit_inbound`, read, and subscribe doors ([#4488](https://github.com/nearai/ironclaw/issues/4488)). Structured model-visible tool observations landed to replace loose summaries ([#4530](https://github.com/nearai/ironclaw/pull/4530)). Outbound delivery preference facade contracts were merged ([#4511](https://github.com/nearai/ironclaw/pull/4511)).
- **WebChat v2 & Channel Parity:** Thread deletion was added to the WebChat v2 API ([#4516](https://github.com/nearai/ironclaw/pull/4516)). The Slack Reborn "host-beta" backend received durable conversation and outbound stores and an admin-allowed channel picker ([#4463](https://github.com/nearai/ironclaw/pull/4463), [#4532](https://github.com/nearai/ironclaw/pull/4532)). V1 Google/GitHub/NEAR SSO behavior was carried over to the new WebUI surface ([#4116](https://github.com/nearai/ironclaw/issues/4116)).
- **Developer Experience & Infrastructure:** A hermetic local development gate for fmt, clippy, and test standards was merged ([#3298](https://github.com/nearai/ironclaw/pull/3298)). The nightly E2E test timeout was extended to 90 minutes ([#3565](https://github.com/nearai/ironclaw/pull/3565)).
- **Bug Fixes:** A medium-risk fix landed for configured extension credential staging, ensuring local-dev credentials are available on the first capability call ([#4492](https://github.com/nearai/ironclaw/pull/4492)). A canonical E2E acceptance test for the WebUI beta was added ([#4529](https://github.com/nearai/ironclaw/pull/4529)).

## 4. Community Hot Topics
All of the most active discussions are driven by core team coordination around the Reborn rewrite.

- **#3280: ProductWorkflow & InboundTurnService facade** (7 comments) — [nearai/ironclaw#3280](https://github.com/nearai/ironclaw/issues/3280). This is the central coordination issue for the new product-facing workflow, linking 11+ dependencies. It reflects the sheer complexity of committing a new service boundary.
- **#3036: Configuration-as-Code Epic** (5 comments, 1 👍) — [nearai/ironclaw#3036](https://github.com/nearai/ironclaw/issues/3036). Operators explicitly demanding declarative tenant blueprints and harnesses to replace hand-edited `.env` and JSON config files. This is the highest-signal "user pain point" in the tracker.
- **#3044: Local Developer Runtime Profiles** (3 comments) — [nearai/ironclaw#3044](https://github.com/nearai/ironclaw/issues/3044). Engineers calling for a simple `ironclaw dev` command that avoids manual wiring of grants, mounts, and network policy.
- **#3333: Production Wiring & Missing Crates** (3 comments) — [nearai/ironclaw#3333](https://github.com/nearai/ironclaw/issues/3333). An audit finding that several Reborn seams remain fake/in-memory/no-op, tracking real implementation work.

## 5. Bugs & Stability
Security hardening remains the dominant stability theme in this Reborn cutover phase.

- **Critical / High Risk (Resolved):**
  - **Extension credential staging failure** fixed ([#4492](https://github.com/nearai/ironclaw/pull/4492)) — local setup credentials were not propagated to the `SecretStore` before the first capability call.
  - **SSO parity gap** closed ([#4116](https://github.com/nearai/ironclaw/issues/4116)) — v1 browser sign-in behavior was missing from WebChat v2.

- **Critical Open Trackers:**
  - **NoExposure safeguards** ([#3032](https://github.com/nearai/ironclaw/issues/3032)) — production-readiness safety layer preventing raw sensitive data from crossing model-visible boundaries. P0, open 41 days.
  - **Tenant sandbox process capabilities** ([#4042](https://github.com/nearai/ironclaw/issues/4042)) — Docker sandbox still limited to simple scoped commands, insufficient for workspace orchestration. Risk: high.
  - **Approval lease re-attenuation** ([#3609](https://github.com/nearai/ironclaw/issues/3609)) — UI-supplied attenuation values could potentially widen approved leases. P0 WebUI beta blocker.
  - **SecurityAuditSink adoption at remaining boundary call sites** ([#3959](https://github.com/nearai/ironclaw/issues/3959)) — ensuring blocked decisions are retained rather than lost to tracing.

- **Deferred Hardening (Moderate Risk):**
  - Filesystem mount containment (`RESOLVE_NO_XDEV`, [#3956](https://github.com/nearai/ironclaw/issues/3956))
  - Third-party hook activation security & quarantine surfacing ([#3957](https://github.com/nearai/ironclaw/issues/3957))

## 6. Feature Requests & Roadmap Signals
The entire roadmap is converging on completing the Reborn substrate.

- **Strongest signals for the next major release:**
  - **ProductWorkflow facade** ([#3280](https://github.com/nearai/ironclaw/issues/3280)) — the product-facing boundary between adapters and host services.
  - **OpenAI-compatible API migration** ([#3283](https://github.com/nearai/ironclaw/issues/3283)) — moving `/v1/chat` and `/v1/responses` onto the new Reborn projection model.
  - **Configuration-as-Code** ([#3036](https://github.com/nearai/ironclaw/issues/3036)) — tenant blueprints and use-case harnesses.

- **Downstream / Post-Beta Capabilities:**
  - **WASM ProductAdapters** ([#3572](https://github.com/nearai/ironclaw/issues/3572)) — structuring channel adapters (e.g., Telegram v2) as WASM components in a separate runtime to enforce safety boundaries.
  - **Native Google Calendar & Gmail extension-v2** ([#3829](https://github.com/nearai/ironclaw/issues/3829)) — "Lane 9" of the Reborn extension rollout.
  - **Durable approval-policy port** ([#3891](https://github.com/nearai/ironclaw/issues/3891)) — moving beyond hardcoded `AlwaysAllow` to persistent, auditable approval ports.
  - **CLI provider parity** ([#4118](https://github.com/nearai/ironclaw/issues/4118)) — restoring `provider add/login` to the Reborn CLI.

## 7. User Feedback Summary
The current issue stream is almost entirely authored by the core development team, reflecting internal dogfooding and architecture coordination. Nevertheless, the team's expressed priorities convey specific user-facing pain points:

- **Pain Points:** Operators explicitly want to stop hand-editing `.env` files, settings JSONs, and runtime flags ([#3036](https://github.com/nearai/ironclaw/issues/3036)). Engineers need a simple local coding agent runtime without manual wiring of grants, mounts, and process backends ([#3044](https://github.com/nearai/ironclaw/issues/3044)). Feature parity with the v1 API surface (SSO, CLI auth, OpenAI-compatible endpoints) is a blocking requirement for users migrating to the Reborn stack.
- **Satisfaction Indicators:** The rapid closure of user-facing gaps (SSO carryover, credential staging fix, thread deletion) suggests a highly responsive team that closes reported regressions within hours or days.
- **Use Cases Emerging:** Admin-managed Slack channel permissions, user-scoped skill settings, configurable outbound delivery targets, and structured model-visible error recovery contexts.

## 8. Backlog Watch
Several high-priority, long-dormant items demand attention:

- **🚩 #3708: Release PR (Open 23 days)**
  [nearai/ironclaw#3708](https://github.com/nearai/ironclaw/pull/3708) — This chore PR bumps the project from v0.24.0 to v0.29.1 with breaking changes already staged and reviewed. Its continued staleness blocks distribution and may compound merge conflicts. Significant attention risk.

- **🔴 P0 Reborn Cutover Blockers (Open 41 days)**
  Three foundational items from the original #2987 epic remain unstarted:
  - Config-driven production composition root ([#3026](https://github.com/nearai/ironclaw/issues/3026))
  - Migration and compatibility bridges ([#3029](https://github.com/nearai/ironclaw/issues/3029))
  - No-exposure safeguards ([#3032](https://github.com/nearai/ironclaw/issues/3032))

- **🔴 P0 WebUI Beta Blockers (Open 25 days)**
  - Seal dispatch authority with `AuthorizedDispatchRequest` ([#3608](https://github.com/nearai/ironclaw/issues/3608))
  - Re-attenuate approval leases against reviewed descriptors ([#3609](https://github.com/nearai/ironclaw/issues/3609))

- **Architecture Deepening (Open 36–39 days)**
  - Process-owned runtime handoff IDs for concurrent fan-out ([#3169](https://github.com/nearai/ironclaw/issues/3169))
  - Post-substrate architecture deepening follow-ups ([#3231](https://github.com/nearai/ironclaw/issues/3231))

- **Dependency PRs (Open 2-14 days)**
  Several large dependabot PRs, including a 38-update bulk bump across the Rust workspace ([#4503](https://github.com/nearai/ironclaw/pull/4503)) and Github Actions updates ([#4002](https://github.com/nearai/ironclaw/pull/4002)), are accumulating without merge, increasing integration risk.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is a structured digest for the LobsterAI project based on the provided GitHub activities.

---

# LobsterAI Project Digest - 2026-06-08

## 1. Today's Overview
The project shows high community engagement this period with **15 issues updated**, though all are in the backlog or newly reported, and **2 pull requests merged**. No new releases were cut. The issue tracker reveals a significant tension: the community is actively requesting advanced data management features while simultaneously reporting critical stability flaws (OAuth token loss, disabled skills persisting). The two PRs merged today address robustness in configuration migration and gateway payload handling, signaling a focus on backend stability. However, the lack of activity on several high-severity stale bugs is a growing health risk for the project.

## 2. Releases
*No new releases were published in this period.*

## 3. Project Progress (Merged PRs)
Two pull requests were merged/closed today targeting reliability improvements:

- **[PR #2110 - fix(cowork): guard oversized OpenClaw image payloads](https://github.com/netease-youdao/LobsterAI/pull/2110)**
  - **Summary:** Implements a guard to detect oversized image payloads in the cowork chat module before they hit the gateway. It reclassifies `1009` gateway errors as message-size errors and clarifies single-image vs. whole-message size limits.
  - **Impact:** Prevents silent failures in the cowork pipeline when large images are sent.

- **[PR #2117 - fix(config): preserve deleted provider models after migration](https://github.com/netease-youdao/LobsterAI/pull/2117)**
  - **Summary:** Fixes a configuration migration bug by tracking migration versions. Previously, default models were re-injected on every app restart, overriding user deletions.
  - **Impact:** Ensures users maintain control over their model provider lists across updates.

## 4. Community Hot Topics
- **Skills System UX Crisis (Issue #1509):** The most commented issue of the period. A user details a severe workflow blocker where the skill generation feature blocks without any progress indication. The user notes the same prompt works correctly in other clients, pointing to a frontend/backend isolation problem in LobsterAI. ([Issue #1509](https://github.com/netease-youdao/LobsterAI/issues/1509))
- **Token Waste Concern (Issue #2121):** A newly opened issue questions whether the AI model is unnecessarily repeating output text, consuming tokens without benefit. This is a high-priority concern for users sensitive to API costs. ([Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121))
- **Feature Request Cluster from MaoQianTu:** A single user submitted five distinct, well-researched feature requests (Issues #1525, #1528, #1532, #1537, #1541) focused entirely on data management. This cluster suggests a power user actively hitting the limitations of the current chat interface.

## 5. Bugs & Stability
The 24-hour activity update touched on several bugs, though no fix PRs exist for them yet.

**High Severity:**
- **Disabled Skills Persist (Issue #1500):** Toggling a skill off in the manager does not clear it from the active session state, causing it to be injected into future prompts. Root cause identified in `skillSlice.ts`. ([Issue #1500](https://github.com/netease-youdao/LobsterAI/issues/1500))
- **Copilot OAuth Token Lost on Panel Close (Issue #1516):** Closing the settings panel during OAuth polling cancels the UI but leaves the background process running. If the user authorizes the browser window, the token is fetched but silently dropped because the UI state is gone. ([Issue #1516](https://github.com/netease-youdao/LobsterAI/issues/1516))
- **Token Wastage (Issue #2121):** New report of AI repetition, likely causing inflated usage costs. No diagnosis yet. ([Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121))

**Medium Severity:**
- **State Sync Issues (Issue #1502):** Active skill list does not sync immediately after saving Agent settings.
- **Missing Validation (Issues #1504, #1506, #1512):** Multiple forms (IM keys, task notifications, QQ Bot whitelists) lack required field validation, leading to silent runtime failures.

## 6. Feature Requests & Roadmap Signals
User **MaoQianTu** has submitted a cohesive suite of feature requests that strongly signal a need for a "Session Diary / Productivity 2.0" upgrade:
- Session Color Labels (#1525)
- Batch Export (#1528)
- Local Usage Statistics (#1532)
- Message Bookmarks (#1537)
- Tag Filters (#1541)

**Prediction:** These features are likely to be bundled into an upcoming minor release (v0.x). They address the core shift from a simple chat interface to a personal knowledge management tool. If the maintainers engage positively with this batch, it would validate a strong roadmap for power users.

## 7. User Feedback Summary
- **Dissatisfaction (Reliability & Transparency):** The most intense feedback revolves around the Skills system. Users feel they are operating in the dark when tasks block (Issue #1509). The OAuth token loss (Issue #1516) erodes trust in the authentication flow.
- **Dissatisfaction (Wasted Resources):** The token waste complaint (Issue #2121) is the most urgent economic feedback—users are directly asking why they are paying for tokens that produce no new value.
- **Satisfaction / Demand (Advanced Features):** The high quality of the feature requests (Issues #1525–1541) shows a dedicated user base that wants to rely on LobsterAI for long-term work. They are not just testing the tool; they are seeking to make it their primary workspace.
- **Use Cases:** The feedback reveals users are employing LobsterAI for long-running agentic tasks (Skills), multi-session project management, and team integration (IM bots).

## 8. Backlog Watch
A significant number of critical issues are languishing in the backlog.
- **Stale Critical Issues:** Issues #1500 (Disabled Skills), #1502 (State Sync), #1509 (Skills Blocking), and #1516 (OAuth Loss) were all created on **April 7, 2026**, and marked as stale on June 7 without any linked fix PRs or maintainer responses. These are severe UX and reliability blockers.
- **New Urgent Item:** Issue #2121 (Token Waste) was created on June 7 and requires immediate investigation to determine if it is a client rendering bug or a model issue.
- **Maintainer Attention Gap:** The cluster of feature requests from April 7 is also stale with zero maintainer replies. The silence on both critical bugs and high-value feature requests is the primary risk indicator for project health today.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest**
Date: 2026-06-08
Data Source: GitHub (moltis-org/moltis)

---

### 1. Today's Overview
Moltis tracked a quiet day on June 8, 2026, with no new releases or pull request activity. The only movement was an update to a single open feature request, and no bug reports or regressions were filed. While the lack of PRs suggests development velocity is currently subdued, the stable issue count and absence of defects indicate a low-risk period for the project. Overall project health remains stable, with community attention narrowly focused on mobile UI parity.

### 2. Releases
No new releases were published today. The project remains on its last stable version. No migration notes or breaking changes are applicable.

### 3. Project Progress
No pull requests were opened, merged, or updated in the last 24 hours. There are no feature branches or fixes currently advancing through the review pipeline on this surface.

### 4. Community Hot Topics
- **[#1107 [OPEN] [Enhancement] Multiline text input in the mobile web UI](https://github.com/moltis-org/moltis/issues/1107)** (Author: IlyaBizyaev) — This is the only issue active today. It requests that the mobile web frontend support multiline text input rather than a single-line field. Mobile usability continues to be a key surface where the community is requesting investment. The underlying need is clear: power users composing complex prompts on mobile devices find the current UI friction point restrictive.

### 5. Bugs & Stability
No new bugs, crashes, or regressions were reported today. The platform appears stable with no active defect fixes in the pipeline. Based on the data provided, no stability alerts are warranted.

### 6. Feature Requests & Roadmap Signals
The sole feature request active is **[#1107](https://github.com/moltis-org/moltis/issues/1107)** (Multiline mobile text input). This is a relatively small-scope UX improvement that primarily affects the web frontend component. Given its recent filing (June 5), it is unlikely to appear in an immediate patch, but it signals a strong demand for improving the mobile agent interaction experience. This is a strong candidate for a future minor release focused on UI polish.

### 7. User Feedback Summary
User feedback today is entirely concentrated in Issue #1107. The expressed pain point is a limitation in composing longer prompts or chat messages on mobile browsers. This suggests that while users are satisfied with the core AI agent functionality, they find the mobile web interface lacking in feature parity with the desktop experience. The community is asking for a more flexible and natural text entry method.

### 8. Backlog Watch
The backlog is minimal. Issue [#1107](https://github.com/moltis-org/moltis/issues/1107) is the only open item updated today. Although it is not a long-neglected issue (open since June 5), it represents the single most prominent open conversation requiring maintainer input. No deeply stalled or neglected items were observed. Maintainers should provide initial UX feedback on #1107 to keep community engagement healthy.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

## CoPaw Project Digest — 2026-06-08

### 1. Today's Overview
The QwenPaw project (CoPaw ecosystem by AgentScope AI) saw high activity on June 8, with **22 issues** and **10 pull requests** updated. The project is navigating a critical tension: rapid feature development (AgentScope 2.0 migration, plugin infrastructure) is proceeding in parallel with a wave of regressions introduced in v1.1.10 that are frustrating the user base. Enterprise channel support (Yuanbao/WeCom) received rapid fixes, while core user workflows—local model deployment, Coding Mode, and Windows compatibility—are showing instability. First-time contributors are stepping up with major test coverage additions, signaling a healthy contributor pipeline despite the stability headwinds. Overall project health is **engaged but strained**, with maintainers actively triaging a heavy bug load.

### 2. Releases
**No new releases were published today.** The community continues to evaluate v1.1.10, which exhibits regressions in several areas (see Bugs & Stability). Users on earlier versions (e.g., v1.1.5.post2) are reporting more reliable local model experiences, suggesting the latest release may benefit from a patched point release soon.

---

### 3. Project Progress

**Merged / Closed PRs Today:**

- **[PR #4983](agentscope-ai/QwenPaw PR #4983) — fix(channels): store connectId from AuthBindRsp for connection tracking** (Closed, Under Review)
  Resolved a protobuf-encoding bug (#4978) that prevented the Yuanbao channel from tracking server connections.

- **[PR #4982](agentscope-ai/QwenPaw PR #4982) — fix(channels): fix Yuanbao streaming replies silently dropped** (Closed, Under Review)
  Fixed silent message failures when `streaming_enabled=True` in the Yuanbao channel (#4979).

- **[PR #4996](agentscope-ai/QwenPaw PR #4996) — WIP: Plugin extension infrastructure** (Closed)
  Closed in favor of higher-quality follow-up PRs #4997 and #4998 targeting separate branches.

**New Open PRs of Note:**

- **[PR #5000](agentscope-ai/QwenPaw PR #5000) — fix(mission): prevent agent crash on corrupted loop_config.json/prd.json** (@rayrayraykk)
  Directly addresses the critical crash bug #4970 with hardened JSON parsing.

- **[PR #5002](agentscope-ai/QwenPaw PR #5002) — feat(mcp): add per-server tool whitelisting with frontend toggle UI** (@qbc2016)
  Adds user-facing controls to selectively enable/disable MCP tools, persisted in config and hot-patched at runtime.

- **[PR #4973](agentscope-ai/QwenPaw PR #4973) — test(phase5): add unit tests** (first-time contributor @EaveLuo)
  129 new test cases across 1,374 lines covering `local_models/`, `providers/`, `tunnel/`, and `utils/` modules.

- **[PR #4995](agentscope-ai/QwenPaw PR #4995) — fix(channels): preserve renderer tool output** (first-time contributor @AbbyJL)
  Prevents tool output from being reduced to placeholder text when `show_tool_details` is disabled.

---

### 4. Community Hot Topics

- **[Issue #4727 — Breaking Change: Migrate backend to AgentScope 2.0](agentscope-ai/QwenPaw Issue #4727)** (Open, 6 comments, 2👍)
  The most consequential architectural discussion on the project. Users are closely watching for migration guidance and timeline commitments.

- **[Issue #4585 — WeCom channel plugin auto-discovery failure](agentscope-ai/QwenPaw Issue #4585)** (Open, 5 comments)
  A persistent enterprise blocker: self-developed plugins work in the desktop UI but are invisible in WeCom channel conversations.

- **[Issue #4587 — Shutdown leaves orphaned backend processes](agentscope-ai/QwenPaw Issue #4587)** (Closed, 5 comments)
  Recently resolved macOS process management issue that generated substantial community discussion.

**Underlying Needs:** The community is heavily invested in making QwenPaw enterprise-ready (WeCom reliability, process cleanliness) while pushing for multi-model flexibility (visual model fallback in #4992). The high interaction on the AgentScope 2.0 migration issue signals a user base that is technically sophisticated and cares about architectural direction.

---

### 5. Bugs & Stability

**Critical**

- **[Issue #4988](agentscope-ai/QwenPaw Issue #4988) — Duplicated session ID in filename causes Windows MAX_PATH overflow**
  Session JSON files are written with the session ID duplicated in the filename, making full Windows path strings exceed the 260-character limit. This breaks session persistence entirely on Windows.

- **[Issue #4970](agentscope-ai/QwenPaw Issue #4970) — Corrupted `loop_config.json` / `prd.json` crashes agent session completely**
  Any JSON corruption in mission configuration files leaves the agent unresponsive across all channels (Telegram, Console, etc.). **Fix PR #5000 is open.**

**High**

- **[Issue #4989](agentscope-ai/QwenPaw Issue #4989) — Local Qwen 3.6-27B model unresponsive in v1.1.9/v1.1.10**
  Regression from v1.1.5.post2. vLLM-deployed models using standard OpenAI protocol fail to respond despite passing connectivity tests. Blocks entirely local deployment scenarios.

- **[Issue #4987](agentscope-ai/QwenPaw Issue #4987) — Session switching fails in Coding Mode**
  Another v1.1.10 regression. Normal Chat Mode works, but Coding Mode is completely broken for session switching.

- **[Issue #5003](agentscope-ai/QwenPaw Issue #5003) — Ali Coding Plan qwen3.7-plus gets stuck**
  The agent hangs indefinitely when using this specific model/provider combination.

**Medium / Low**

- **[Issue #4993](agentscope-ai/QwenPaw Issue #4993) — Image preview jitter on zoom/drag** (macOS, V1.1.10)
- **[Issue #4990](agentscope-ai/QwenPaw Issue #4990) — WeCom unfriendly error message on tool use**: Returns "抱歉，我无法回答你的问题，请稍后再试" instead of useful diagnostics.
- **[Issue #5001](agentscope-ai/QwenPaw Issue #5001) — 9router model connectivity issue**: Models cannot connect when routing through specific infrastructure.

**Resolved Yesterday** — Five Yuanbao channel bugs (#4976, #4977, #4978, #4979, #4980) all closed with merged fixes.

---

### 6. Feature Requests & Roadmap Signals

**Already in Development / Strong Signals:**

- **AgentScope 2.0 Migration** (Issue #4727) — The defining infrastructure initiative. Work-in-progress branch `dev/agentscope2.0` has been established and is receiving plugin infrastructure code.
- **Plugin Extension Infrastructure** (PRs #4997, #4998) — A comprehensive frontend/backend plugin registry system enabling menu registration, chat extensions, and UI slot fills. This is the project's largest feature investment currently active.
- **MCP Tool Whitelisting** (PR #5002) — Already coded and up for review; highly likely to ship in next release.

**High Community Demand (Likely to ship in v1.2.x or sooner):**

- **[Issue #4992](agentscope-ai/QwenPaw Issue #4992) — Independent Visual Model configuration**: Decouple vision processing from the primary text model using a fallback chain. Relatively contained implementation scope.
- **[Issue #4986](agentscope-ai/QwenPaw Issue #4986) — Shell real-time interaction feedback**: Users want streaming command output visibility (inspired by Cursor/WorkBuddy UX).
- **[Issue #4999](agentscope-ai/QwenPaw Issue #4999) — Session filtering by title**: A practical UX need for managing many conversations.

**Longer-Range Signals:**

- **[Issue #4994](agentscope-ai/QwenPaw Issue #4994) — Self-evolving memory system**: The community is asking for layered, hierarchical memory architectures commonly seen in advanced agent frameworks.

---

### 7. User Feedback Summary

- **Dissatisfaction / Pain Points:**
  Users are frustrated by v1.1.10 regressions. Common sentiment patterns include: "version X worked, version Y does not" (#4989, #4987). Windows users face a complete platform blocker (#4988). Enterprise users hit a wall with WeCom plugin detection (#4585). The "agent crash on config corruption" bug (#4970) is especially jarring because it bricks the entire session without a recovery path.

- **Satisfaction Drivers:**
  Maintainer responsiveness is a bright spot: multiple Yuanbao channel bugs were filed and fixed within 24 hours (Issues #4976–#4980 → PRs #4982, #4983). New contributors are shipping real, non-trivial improvements (EaveLuo's 129 tests, AbbyJL's renderer tool preservation). The plugin infrastructure work signals that the project is maturing beyond a single-purpose agent.

- **Unspoken Needs:**
  The community would benefit from a "known regressions" page or pinned issue for each release. Users are doing that detective work themselves by filing separate bugs. Better integration test coverage before minor version bumps would prevent the current trust erosion from v1.1.10.

---

### 8. Backlog Watch

- **[Issue #4727 — AgentScope 2.0 Migration](agentscope-ai/QwenPaw Issue #4727)**
  Open since May 27, updated today. This is the project's highest-impact open item with no published migration guide, compatibility matrix, or timeline. Plugin developers (watching PRs #4997/#4998) are operating in uncertainty. **Needs: A roadmap communication from maintainers.**

- **[Issue #4585 — WeCom Plugin Auto-Discovery](agentscope-ai/QwenPaw Issue #4585)**
  Open since May 21. No fix PR exists. Blocks a core enterprise workflow (DingTalk/Feishu/QQ users may be affected similarly). Priority should be elevated given the rapid closure of other WeCom bugs yesterday.

- **[PR #4949 — ACP Server Enhancements](agentscope-ai/QwenPaw PR #4949)**
  Under review since June 3. This PR serves the terminal TUI client (`paw`) and provides critical metadata (commands, tool params, file links) for a first-class terminal experience. Has not been merged despite being in review for five days.

- **[Issue #4989 — Local Model Unresponsive](agentscope-ai/QwenPaw Issue #4989)**
  A v1.1.10 regression affecting self-hosted users. This user demographic (self-hosting via Docker, local vLLM) is typically a power-user and community builder. A fast fix here would go a long way toward restoring confidence in the release.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-06-08

**Data Snapshot:** 50 Issues updated (32 open, 18 closed) · 50 PRs updated (38 open, 12 merged/closed) · 0 new releases

---

## 1. Today's Overview

ZeroClaw is in a period of intense pre-release development, with 50 Issues and 50 Pull Requests updated in the last 24 hours. The team closed 18 issues and finalized 12 PRs, including several long-standing S1 blockers. While no new version was published today, the release machinery for **v0.8.0** is clearly spinning up (PR #7364). Activity is balanced across three fronts: major TUI/UX overhauls for `zerocode`, urgent provider stability fixes, and the ongoing Schema v3 provider migration. The community remains highly engaged, particularly around multi-agent routing, token cost optimization, and lowering the onboarding barrier for Docker users.

---

## 2. Releases

No new releases today.

---

## 3. Project Progress

**Merged/Closed PR Highlights (12 total today):**

- **zerocode TUI Revolution:**
  - **Outbound Message Queue** (PR [#7190](zeroclaw-labs/zeroclaw/pull/7190)) — Users can now compose and submit messages *while* a turn is responding, replacing the previous hard input block.
  - **In-Session Model/Provider Picker** (PR [#7209](zeroclaw-labs/zeroclaw/pull/7209)) — Live `/model` and `/model-provider` switching without exiting to reconfiguration.
  - **Theme System Overhaul** (PR [#7249](zeroclaw-labs/zeroclaw/pull/7249)) — Color-depth fallback, registry-generated presets, per-agent overrides, and palette swatches.
  - **Quickstart Modal Fix** (PR [#7360](zeroclaw-labs/zeroclaw/pull/7360)) — Modal sizing now correctly accounts for wrapped text.

- **Provider & Reliability:**
  - **Per-Alias Model Fallback** (PR [#7178](zeroclaw-labs/zeroclaw/pull/7178)) — Operators can now declare per-alias fallback-on-failure chains, restoring a critical resilience feature removed in a previous schema refactor.

- **Critical Bug Fixes (Closed):**
  - **Web Dashboard Unavailable** (Issue [#4866](zeroclaw-labs/zeroclaw/issues/4866), S1) — *Closed*. The top-voted community pain point.
  - **Fallback Provider Chain Ignores Config** (Issue [#5803](zeroclaw-labs/zeroclaw/issues/5803), S1) — Credentials and `base_url` now properly resolve from `[providers.X]` config.
  - **Delegate Agents Ignore Prompt Injection Mode** (Issue [#5155](zeroclaw-labs/zeroclaw/issues/5155), S1) — Delegates now respect `compact` mode instead of always injecting full skills.
  - **`web_fetch` Private IP Blocklist Ineffective** (Issue [#5122](zeroclaw-labs/zeroclaw/issues/5122)) — DNS resolution logic fixed for `allowed_private_hosts`.
  - **Context Compression Not Triggered in Daemon Mode** (Issue [#4880](zeroclaw-labs/zeroclaw/issues/4880))
  - **MCP Detection Broken** (Issue [#4848](zeroclaw-labs/zeroclaw/issues/4848))

---

## 4. Community Hot Topics

| Issue | Comments | 👍 | Core Theme |
|---|---|---|---|
| [#4710 Better LOGO](zeroclaw-labs/zeroclaw/issues/4710) | 11 | 2 | Branding & Community Identity |
| [#5146 Token consumption via skill compilation](zeroclaw-labs/zeroclaw/issues/5146) | 9 | 1 | **Cost & Performance Optimization** |
| [#3642 Full Docker image](zeroclaw-labs/zeroclaw/issues/3642) | 9 | 3 | Onboarding & Accessibility |
| [#2503 Napcat/OneBot channel](zeroclaw-labs/zeroclaw/issues/2503) | 9 | 0 | Channel Ecosystem Expansion |
| [#3566 A2A Protocol Support](zeroclaw-labs/zeroclaw/issues/3566) | 6 | **7** | **Interoperability** |
| [#2767 Multi-Agent Routing](zeroclaw-labs/zeroclaw/issues/2767) | 6 | **9** | **Architecture & Scaling** |
| [#4627 file_write silently fails](zeroclaw-labs/zeroclaw/issues/4627) | 3 | 1 | **S0 Bug (Trust/Security)** |

**Analysis:** The community's strongest demands cluster around **scaling and cost** (Multi-Agent Routing, A2A, skill compilation) and **barrier to entry** (Docker, channel support, branding). The S0 `file_write` bug (#4627) continues to generate quiet but serious concern.

---

## 5. Bugs & Stability

**Critical (S0 — Data Loss / Security):**
- [#4627](zeroclaw-labs/zeroclaw/issues/4627) **file_write tool silently fails** — Files report success but are invisible on the host filesystem. *Open since March 25. No fix PR merged.*

**Severe (S1 — Workflow Blocked):**
- [#4879](zeroclaw-labs/zeroclaw/issues/4879) **Gemini CLI OAuth not working** — Rates-limited errors immediately after successful auth. *Open since March 28. Needs a fix.*
- [#7243](zeroclaw-labs/zeroclaw/pull/7243) **Token revocation on rotation** (PR) — High-risk security fix partially addressing vulnerability [#6984](zeroclaw-labs/zeroclaw/issues/6984). Under active development.

**Degraded Experience (S2):**
- [#4721](zeroclaw-labs/zeroclaw/issues/4721) — Logs stream to stdout instead of stderr, breaking CLI piping.
- [#4873](zeroclaw-labs/zeroclaw/issues/4873) — Feishu/Lark integration routes to raw LLM instead of the Agent.

**Security Fixes in Progress:**
- PR [#7243](zeroclaw-labs/zeroclaw/pull/7243) — Token revocation on rotation.
- PR [#7234](zeroclaw-labs/zeroclaw/pull/7234) — Memory strategy migration (reducing attack surface via bounded consolidation).
- PR [#7367](zeroclaw-labs/zeroclaw/pull/7367) — Per-alias webhook routing (fixes security boundary by correctly routing multi-instance channels).

**Assessment:** S1 hygiene has improved dramatically today with several high-profile closures. The S0 `file_write` bug (#4627) remains the project's most urgent unresolved stability risk.

---

## 6. Feature Requests & Roadmap Signals

**Imminent (v0.8.0 Release):**
- **Release Prep** (PR [#7364](zeroclaw-labs/zeroclaw/pull/7364)) — v0.8.0 branch created.
- **Schema v3 Provider Expansion** (PR [#7260](zeroclaw-labs/zeroclaw/pull/7260)) — 7 new OpenAI-compatible providers (morph, github_models, upstage, featherless, arcee, lambda_ai, inception).
- **MemoryStrategy Migration** (PR [#7234](zeroclaw-labs/zeroclaw/pull/7234)) — Final slice wiring gateway WebSocket and channel consolidation to the new bounded memory strategy.
- **Web Dashboard Management Tabs** (PR [#7229](zeroclaw-labs/zeroclaw/pull/7229)) — MCP, Skills, Plugins, and Providers tabs.
- **Per-Alias Webhook Routing** (PR [#7367](zeroclaw-labs/zeroclaw/pull/7367)) — Solves Issue [#6312](zeroclaw-labs/zeroclaw/issues/6312) for multi-instance channels.

**Accepted / In-Progress (Likely v0.9+):**
- **Skill Compilation** (Issue [#5146](zeroclaw-labs/zeroclaw/issues/5146)) — Minimizing token consumption by compiling skills. High community desirability.
- **Multi-Agent Routing** (Issue [#2767](zeroclaw-labs/zeroclaw/issues/2767)) — Isolated workspaces + bindable channels. 9 👍.
- **A2A Protocol Support** (Issue [#3566](zeroclaw-labs/zeroclaw/issues/3566)) — Google/Linux Foundation Agent2Agent interop. 7 👍.
- **Air-Gapped Execution Mode** (Issue [#6293](zeroclaw-labs/zeroclaw/issues/6293)) — Enclave/split-process architecture for offline-first security. *RFC, needs maintainer review.*
- **Configurable Bubblewrap Sandbox** (Issue [#5127](zeroclaw-labs/zeroclaw/issues/5127)) — Writable paths and network access for sandboxed commands.

---

## 7. User Feedback Summary

**Pain Points:**
- **Cost Anxiety:** Token consumption during skill injection is a top concern (#5146). Users want "compiled" workflows to cut LLM bills.
- **Onboarding Friction:** Docker complexity (#3642), MCP configuration confusion (#4848, now fixed), and missing Chinese ecosystem channels (NapCat/OneBot #2503, Feishu agent bypass #4873) create significant entry barriers.
- **Tooling Trust:** The S0 `file_write` bug (#4627) and ineffective private IP blocking (#5122, now fixed) erode confidence in core agent capabilities.
- **Logging Hygiene:** Logging to stdout (#4721) breaks standard Unix scripting for `zeroclaw config schema`.

**Desired Capabilities:**
- Multi-instance, isolated agent workspaces (#2767).
- Direct per-user channel messaging from within agents (#5145).
- Custom webhook transforms for arbitrary payloads (#2467).
- Better Gemini support (#4879) and Qwen OAuth refresh tokens (#4703, now closed).

**Positive Signals:**
- The community deeply appreciates the rapid development cadence and the prolific contributions from members like `singlerider` and `theonlyhennygod`.
- The closure of the web dashboard bug (#4866) and fallback config bug (#5803) addressed two of the most visible user frustrations.

---

## 8. Backlog Watch

**Long-Blocked Items Needing Maintainer Resolution:**

| Issue | Blocked Since | Risk | Summary |
|---|---|---|---|
| [#3642 Full Docker image](zeroclaw-labs/zeroclaw/issues/3642) | 2026-03-15 | Medium | Barrier to entry for non-technical users. Needs priority decision. |
| [#2467 Webhook transforms](zeroclaw-labs/zeroclaw/issues/2467) | 2026-03-02 | Medium | Core gateway extensibility blocked. |
| [#4627 file_write silently fails](zeroclaw-labs/zeroclaw/issues/4627) | 2026-03-25 | **S0** | Data loss / security. Most critical open bug. |
| [#4879 Gemini CLI OAuth broken](zeroclaw-labs/zeroclaw/issues/4879) | 2026-03-28 | **S1** | No fix linked. Grows stale. |

**Awaiting Review / Author Action:**
- [#6293 Air-gapped mode RFC](zeroclaw-labs/zeroclaw/issues/6293) — Pending maintainer review since May 3.
- [#6490 Integration labels fix (PR)](zeroclaw-labs/zeroclaw/pull/6490) — Needs author action since May 6.
- [#7184 Move translations to git submodule (RFC)](zeroclaw-labs/zeroclaw/issues/7184) — Architectural debate open since June 4.

**Recommendation:** The S0 `file_write` bug (#4627) and the Gemini OAuth S1 bug (#4879) should be the project's top maintenance priorities ahead of the v0.8.0 release to avoid shipping with known critical regressions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*