# OpenClaw Ecosystem Digest 2026-06-10

> Issues: 442 | PRs: 482 | Projects covered: 13 | Generated: 2026-06-10 03:26 UTC

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

# OpenClaw Project Digest — 2026-06-10

## Today's Overview
The OpenClaw project is operating at extremely high velocity today, with **442 issues** and **482 PRs** updated in the last 24 hours. The team shipped **two releases** (`v2026.6.5` and `v2026.6.5-beta.6`), which directly address the highly visible QQBot `<thinking>` scaffolding leak and introduce MCP tool result coercion improvements. Despite this rapid output, the tracker is heavily weighted toward stabilization: a significant number of P1 regressions from the `2026.5.x` and `2026.6.x` releases are flooding the board, particularly around Codex session lifecycle, context compaction, and channel-specific delivery failures (Matrix, Discord, WhatsApp, Telegram). The project remains healthy and transparent, but the volume of `clawsweeper:needs-product-decision` and `clawsweeper:needs-security-review` blocks suggests a pipeline bottleneck on critical security and UX decisions.

---

## Releases
Two new releases were published:
- **v2026.6.5** (stable): openclaw 2026.6.5
- **v2026.6.5-beta.6**: openclaw 2026.6.5-beta.6

### Highlights
- **QQBot thinking/stripping:** Model reasoning/thinking scaffolding is now stripped before native delivery, preventing raw `<thinking>` content from leaking into channel replies. (#89913, #90132) — Thanks @openperf.
- **MCP tool result coercion:** `resource_link`, `resource`, `audio`, and malformed image results are now coerced correctly in MCP tool outputs.

No explicit breaking changes or migration notes are documented beyond these highlights, though the `#90083` transport fix implies backend alignment for the newer GPT-5.4/5.5 models.

---

## Project Progress
**130 PRs merged/closed** in the last 24 hours. Key advances and fixes include:

- **OpenAI transport fix:** [#90083] [CLOSED] — Resolved `invalid_provider_content_type` errors for `gpt-5.4`/`gpt-5.5` in the ChatGPT Responses transport.
- **Codex stabilization:** [#91590] [CLOSED] — Fixed context-engine compaction ownership for Codex sessions, preventing budget compaction from being preempted by native harness actions.
- **Codex memory recall:** [#91813] [OPEN] — Restores memory recall from plugin tools in Codex sessions (alternative to #91594).
- **Windows gateway fix:** [#86599] [CLOSED] — Fixed local model provider calls blocking the event loop on Windows beta.
- **iOS/iPad UI:** [#91557] [CLOSED] — Improved iPad and iPhone control surfaces with real sidebar navigation, workboard support, and responsive phone control hub behavior.
- **WhatsApp TTS audio delivery:** [#89251] [CLOSED] — Fixed TTS tool audio delivery for channel-backed runs.
- **Cron:** [#91811] [CLOSED] — Queue disabled wake fallback for one-shot cron jobs.
- **iMessage diagnostics:** [#91785] [CLOSED] — Added inbound startup diagnostics for echo/reflection dropping.
- **Session history dedup:** [#85669] [CLOSED] — Filtered `delivery-mirror` and `gateway-injected` messages from sessions_history.
- **WebUI fixes:** [#91810] [OPEN] — Reloads WebChat history for deferred thinking; [#91798] [OPEN] — Workboard grid overflow fix; [#91215] [OPEN] — Prompt progress indicator now scoped to session.

---

## Community Hot Topics
The most active discussions reflect widespread concern over session reliability and information leakage:

### 1. [#25592] Text between tool calls leaks to messaging channels
- **Open | P1 | Lobster | Security, Message Loss**
- *29 comments, 1 👍*
- Extremely high engagement. Users reporting that internal LLM processing output (error handling, acknowledgments, narration) is being routed to Slack, iMessage, and other channels as visible messages. The v2026.6.5 release partially addresses this for QQBot, but the underlying issue remains open and awaiting security review.

### 2. [#90083] OpenAI ChatGPT Responses transport fails for GPT-5.4/5.5
- **Closed | P1 | Platinum Hermit**
- *16 comments, 3 👍*
- A major regression in the `2026.6.1` release that broke inference for two of OpenAI's latest models. Closed quickly, indicating strong response velocity.

### 3. [#32296] Agent replies to previous message instead of current message
- **Open | P1 | Platinum Hermit | Session State, Message Loss**
- *15 comments, 1 👍*
- A core UX fidelity issue: the agent's context window appears to drift. Users report conversations becoming completely derailed.

### 4. [#88312] Codex turn-completion stall regression
- **Open | P1 | Platinum Hermit | Regression**
- *15 comments, 3 👍*
- Codex multi-tool agent turns fail with "Codex stopped before confirming the turn was complete" starting in `2026.5.27`. Identified as a regression of #84076.

### 5. [#87307] Matrix thread replies sent as normal replies
- **Open | P1 | Gold Shrimp | Message Loss**
- *14 comments, 1 👍*
- A regression in `2026.5.22` where Matrix thread scoping broke, `/status` and `/model` commands also went silent.

**Other notable hotspots:**
- [#54531] *Force reply to originating channel* (10 comments) — Users reporting complete response silence in Telegram/Discord/WhatsApp.
- [#44905] *Discord leaks internal tool-call traces* (10 comments) — `NO_REPLY`, `to=functions` commentary surfacing to end users.
- [#89315] *Gateway heap grows unbounded / OOM* (5 comments, 3 👍) — Silent failure on long-running Linux systemd deployments.
- [#84569] *WhatsApp session stalls on long model calls* (5 comments, 3 👍) — Incomplete turns with `payloads=0`.

---

## Bugs & Stability

### Critical (P1, Security / Message Loss / Data Loss)

| Issue | Title | Status | Impact |
|-------|-------|--------|--------|
| #25592 | Text between tool calls leaks to channels | **OPEN** | Security, Message Loss |
| #44905 | Discord leaks internal tool-call traces | **OPEN** | Security, Message Loss |
| #32296 | Agent replies to previous message (context confusion) | **OPEN** | Session State, Message Loss |
| #88312 | Codex turn-completion stall | **OPEN** | Session State, Message Loss |
| #86508 | EmbeddedAttemptSessionTakeoverError on Discord | **OPEN** | Session State |
| #89315 | Gateway heap OOM on long-running Linux | **OPEN** | Crash Loop |
| #54531 | Force reply to originating channel | **OPEN** | Message Loss |
| #86538 | Session write-lock timeouts block subagent lanes | **OPEN** | Session State |
| #84569 | WhatsApp session stalls | **OPEN** | Session State |
| #31331 | Docker + Sandbox \`workspaceAccess\` failure | **OPEN** | Security |
| #53540 | "Network connection lost" on large tool call params | **OPEN** | Session State, Message Loss |
| #54634 | Config silently dropped when HOME changes | **OPEN** | Data Loss |
| #56096 | Telegram infinite retry loop (no backoff) | **OPEN** | Crash Loop |
| #55694 | Agent tool-call infinite retry spam | **OPEN** | Message Loss |

### Notable Regressions
- **#90083** (GPT-5.4/5.5 transport) — *CLOSED*
- **#88312** (Codex stall) — *OPEN*
- **#87307** (Matrix thread replies) — *OPEN*
- **#86599** (Windows event loop) — *CLOSED*
- **#52186** (ElevenLabs TTS vs OpenAI voice) — *OPEN (P2, Stale)*

### Stability / Infrastructure
- [#53399] *Chrome MCP spawn hang* — P2, Open
- [#50442] *Backup leaves large .tmp files* — P2, Open (Data Loss)
- [#74586] *AM embedded run aborts memory_search* — Open, 9 comments
- [#76233] *exec-approval-followup races subagent disposal* — P1, Open

---

## Feature Requests & Roadmap Signals

### Highly demanded user features
- **[#90354] Bounded/validated append semantics for pre-compaction memory flush** — Provides hard guardrails for memory writes. (P2, Open)
- **[#54531] Force reply to originating channel** — Ensures Telegram/Discord/WhatsApp replies reach the user. (P1, Open, stuck in review)
- **[#53638] Per-channel/per-group/per-DM model override** — Fine-grained model routing without manual intervention. (P2, Open)
- **[#52640] Persistent task-status surface for long-running turns** — First-class Discord indicator for background agent work. (P2, Open)
- **[#42840] MathJax/LaTeX in Control UI** — High demand from STEM users (6 👍). (P2, Open)
- **[#55249] Session labels/nicknames** — Human-readable identifiers for opaque session keys. (P2, Open)
- **[#56110] STATE.md auto-loaded workspace bootstrap** — Context compaction recovery state. (P2, Open)
- **[#39406] Config option to suppress transient tool error warnings** — Reduces noise in channels. (P2, Open, Stale)

### Signals from Pull Requests
- **#91438** [OPEN] — Microsoft Teams CVI voice/video call provider (XL effort, cross-session).
- **#91807** [OPEN] — Support `--file` for `image generate` CLI (parity with `image edit`).
- **#55851** [OPEN, Stale] — Provider/model/profile/trigger context in overloaded error messages.
- **#79982** [OPEN] — Introduce `group:core` for all built-in core tools.
- **#62262** [CLOSED] — Intelligent reply quoting (`replyToMode auto`).

### Prediction for Next Release
Based on the current PR queue and bug density, the next release will likely focus on:
- **Codex session lifecycle stabilization** (#91590, #88312, #91813)
- **MCP and bundle-mCP runtime race fixes** (#76233)
- **Channel-specific delivery hardening** (WhatsApp #84569, Matrix #87307, Discord #44905)
- **Session context fidelity** (#32296, #48003)
- **Performance** (Gateway OOM #89315, Windows event loop #86599)

---

## User Feedback Summary

### Expressed Pain Points
- **"Agent responds to the wrong message"** (#32296) — Degraded conversation UX that undermines agent usefulness.
- **"Codex turn keeps stalling"** (#88312) — Makes multi-tool pipelines unreliable.
- **"My bot is completely unresponsive"** (#56096, #54531, #86599) — Message delivery silence after upgrade.
- **"Internal processing leaks to my users"** (#25592, #44905) — Trust-killing security issue.
- **"Gateway consumes all memory and gets killed"** (#89315) — Infrastructure instability for long-running deployments.
- **"My config is silently dropped on upgrade"** (#54634) — Upgrade path fragility.
- **"Live docs are ahead of the release"** (#48920) — Documentation trust gap.

### Satisfaction Indicators
- **Rapid fix turnaround** — #90083 (GPT transport) and #86599 (Windows loop) were closed briskly.
- **Transparent labeling** — `clawsweeper` bot labels (needs-info, source-repro, linked-pr-open) show explicit triage workflow.
- **Community contributor recognition** — "Thanks @openperf" in release notes builds goodwill.
- **Active beta testing** — Users consistently filing detailed regression reports with repro steps.

---

## Backlog Watch
Several high-priority items are stalled in the review pipeline, representing risk to project velocity:

### Stuck on `clawsweeper:needs-product-decision` + `clawsweeper:needs-security-review`
- **#25592** — Text leaks between tool calls (Diamond Lobster, P1). *The most commented issue.*
- **#44905** — Discord internal tool-call trace leaks (Diamond Lobster, P1).
- **#54531** — Force reply to originating channel (Diamond Lobster, P1).
- **#56263** — Configurable file permissions for multi-user (Diamond Lobster, P1).
- **#53540** — Network connection lost on large param generation (Diamond Lobster, P1).
- **#31331** — Docker Sandbox workspaceAccess blocked (Diamond Lobster, P1).
- **#54634** — Config silently dropped on upgrade (Diamond Lobster, P1).

### Stuck on `clawsweeper:needs-product-decision` (no security review)
- **#48003** — Steer mode does not inject messages mid-turn (Diamond Lobster, P1).
- **#52640** — Persistent task status for long runs (Off-Meta, P2).
- **#53628** — XDG_CONFIG_HOME not processed in skill install (Diamond Lobster).

### Stuck on `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-live-repro`
- **#88312** — Codex turn-completion stall regression (Platinum Hermit, P1).
- **#89315** — Gateway OOM (Platinum Hermit, P1).
- **#32296** — Session context confusion (Platinum Hermit, P1).
- **#87307** — Matrix thread regression (Gold Shrimp, P1).
- **#86996** — Active Memory + Codex latency/hook timeouts (Platinum Hermit, P1).

### Stale high-value items
- **#54253** — RISC-V64 support (Silver Shellfish, P2, Stale).
- **#52186** — ElevenLabs TTS regression (Platinum Hermit, P2, Stale).
- **#53486** — Feishu card JSON regression (Diamond Lobster, P2, Stale).
- **#48920** — Live docs ahead of release (Diamond Lobster, P2, Stale).

The concentration of P1/Diamond Lobster items awaiting product and security decisions is the single clearest bottleneck in the project's current flow. Addressing these blocks would likely clear the most severe community-reported barriers to adoption and trust.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** June 10, 2026

---

## 1. Ecosystem Overview

The open-source personal AI agent landscape is in a "second wave" growth phase, transitioning from proof-of-concept feature velocity to production-grade reliability. This manifests in heavy stabilization and security hardening sprints across the major projects, while newer entrants demonstrate the benefits of cleaner architectural foundations. A sharp divide exists between projects managing the fallout from aggressive feature cycles (OpenClaw, IronClaw) and those executing disciplined consolidation cycles (NanoClaw, NullClaw). An intense undercurrent of provider fragmentation, session reliability anxiety, and competitive benchmarking against rising peers dominates community discourse. The ecosystem is healthy and highly transparent, but the sheer volume of regression traffic is stretching maintainer capacity at the top end.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Latest Release | Velocity & Health Signal |
|---|---|---|---|---|
| **OpenClaw** | 442 | 482 | v2026.6.5 | Very High / Decision Bottleneck |
| **NanoBot** | 6 | 25 | None | High / Rapid Hardening |
| **Hermes Agent** | 50 | 50 | None | **Extreme Input / Merge Crisis** |
| **PicoClaw** | 11 | 16 | Nightly | High / Security Sprint |
| **NanoClaw** | 1 | 43 | None | Very High / Excellent Consolidation |
| **NullClaw** | 5 | 8 | None | Moderate / Steady |
| **IronClaw** | 45 | 50 | None | Very High / Exposing Regressions |
| **LobsterAI** | 1 | 3 | None | Moderate / Focused |
| **CoPaw** | 42 | 38 | v1.1.11-beta.2 | Very High / Mixed Sentiment |
| **Moltis** | 1 | 0 | None | Low / Quiet |
| **ZeroClaw** | 50 | 50 | None | Very High / Pre-Patch Sprint |

**Key Outlier:** Hermes Agent’s 50:1 input-to-merge ratio (50 Issues + 50 PRs updated, 1 merged, 1 closed) is a critical pipeline failure signal. Community enthusiasm is outpacing maintainer capacity.

---

## 3. OpenClaw's Position

OpenClaw remains the ecosystem's most comprehensive **core reference implementation**, unmatched in channel breadth and community scale. Its release discipline (two tagged releases in 24h directly addressing high-severity bugs like the QQBot `<thinking>` leak) demonstrates strong operational cadence. The project sets the standard for transparent triage workflow (`clawsweeper` bot labeling) and governance documentation.

**Advantages vs. Peers:**
- **Breadth:** No peer project matches its channel count (Matrix, Discord, WhatsApp, Telegram, iMessage, etc.) or provider flexibility.
- **Community Size:** Largest contributor base by volume (442 issues, 482 PRs). It is the default "go-to" for multi-platform deployments.
- **Technical Approach:** Heavy investment in session lifecycle management (Codex engine, compaction ownership) and MCP tool result coercion. Prioritizes structured data pipelines over ad-hoc prompt engineering.

**Key Vulnerabilities:**
- **Decision Pipeline Bottleneck:** The queue of `clawsweeper:needs-product-decision` and `needs-security-review` blocks (P1 items like #25592 text leaks, #44905 Discord traces, #54531 reply enforcement) is the single clearest risk to roadmap velocity and user trust.
- **Regression Density:** Highest absolute volume of P1 regressions in the ecosystem, particularly around Codex session lifecycle, context compaction, and channel delivery. The sheer size of the codebase makes stabilization harder than for leaner peers.

---

## 4. Shared Technical Focus Areas

Several critical requirements emerged simultaneously across multiple projects, indicating systemic industry challenges rather than isolated issues.

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **Provider API Fragmentation** | OpenClaw, NanoBot, NullClaw, IronClaw, PicoClaw | GPT-5.4/5.5 transport fix, o-series `max_completion_tokens`, DeepSeek duplicate fields, strict-mode null rejection, Claude Opus temperature deprecation. The "model API update shockwave" is creating simultaneous regressions. |
| **Session & Context Integrity** | OpenClaw, NanoBot, CoPaw, ZeroClaw, Hermes | Codex turn-completion stalls, cross-session history pollution (NanoBot #4259), context budget overflow (ZeroClaw #5808), `/compact` healing commands, bookend context bloat (Hermes #43175). Users demand deterministic session behavior. |
| **Channel Delivery Reliability** | OpenClaw, CoPaw, ZeroClaw, NullClaw, PicoClaw | QQBot/Matrix/Discord/WhatsApp message leaks, DingTalk empty cards, Telegram infinite retries, Matrix threading breaks, missing typing indicators. "Silent failure" is the most cited pain point. |
| **Desktop UI Maturation** | Hermes, CoPaw, NanoClaw, OpenClaw, ZeroClaw | Tauri startup regressions (CoPaw), VS Code terminal panes (Hermes), WebUI dashboards (NanoClaw), iOS/iPad responsiveness (OpenClaw), macOS OOM crash (Hermes), TUI Cmd-C/dark mode bugs (ZeroClaw). |
| **Production Security Hardening** | PicoClaw, OpenClaw, ZeroClaw, NanoBot, IronClaw | SSRF bypasses (PicoClaw 11 disclosures), symlink traversal, RBAC multi-tenancy (ZeroClaw #5982), approval gating, P1 security reviews stalled (OpenClaw), filesystem isolation (NanoBot #4053). |

---

## 5. Differentiation Analysis

**OpenClaw — The "Universal OS"**
- **Target User:** Power users needing maximum channel/provider breadth.
- **Architecture:** Heavy, modular, channel-abstracted runtime with Codex engine and MCP bundle support.
- **Risk:** Complexity is outpacing maintainer stamina. Community patience for P1 regressions is thinning.

**Hermes Agent — The "Desktop IDE Co-Pilot"**
- **Target User:** Developers wanting a rich, desktop-first interactive coding environment.
- **Architecture:** Desktop-native (V8, native notifications, terminal pane), strong brand cachet from NousResearch.
- **Risk:** Pure merge throughput failure. The community is contributing faster than maintainers can review, which will lead to contributor churn.

**ZeroClaw — The "Enterprise Protocol Engine"**
- **Target User:** Organizations needing SOP-driven automation, AMQP pipelines, and rigorous context control.
- **Architecture:** Protocol-heavy (AMQP, SOP), strong emphasis on cost accounting and process memory limits.
- **Risk:** Pre-release stabilization phase. Critical P1 bugs (tool_search hang, SopEngine duplication) lack fix PRs.

**CoPaw (QwenPaw / AgentScope) — The "Skill Ecosystem"**
- **Target User:** Local-first users in Asia-Pacific ecosystems (WeChat, DingTalk).
- **Architecture:** Skill-centric, plugin-based, heavily invested in the AgentScope 2.0 rewrite.
- **Risk:** Desktop performance regression (Tauri switch) is generating the most negative sentiment. Explicit competitive anxiety regarding Hermes' learning loops.

**NanoClaw / NullClaw — The "Lean Contenders"**
- **Target User:** Developers seeking lightweight, well-maintained, low-Docker-overhead solutions.
- **Architecture:** In-process direct runner mode, focus on configuration hygiene and tool filtering.
- **Advantage:** Best contributor health signals (high merge rates, low staleness). Less burdened by legacy code.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity / Regression Burden**
- **OpenClaw, IronClaw, ZeroClaw, CoPaw, Hermes Agent**
- These projects move fast and consume massive community input, but reliability suffers. Hermes is the most at-risk due to pipeline congestion. IronClaw and OpenClaw face the hardest production cutover challenges.

**Tier 2: High Hygiene / Healthy Iteration**
- **NanoClaw, NanoBot, NullClaw, PicoClaw**
- Lower absolute issue volume, but outstanding close rates and contributor satisfaction. NanoClaw’s single-day closure of 39 PRs from a months-long backlog is the standout governance event of the day. PicoClaw’s responsive security patching (same-day fix PRs for 11 CVEs) demonstrates strong trustworthiness.

**Tier 3: Low Activity / Niche**
- **LobsterAI, Moltis, TinyClaw, ZeptoClaw**
- LobsterAI maintains focused iteration on background task resilience and multi-model orchestration. Moltis saw only a single provider config bug filed.

---

## 7. Trend Signals

**1. The Post-GPT-5 Provider Shock is Systemic**
Every major project shipped a bug related to the latest model API changes. This is not a one-time event—it signals chronic instability in the LLM provider layer. Value for developers: **Invest in provider abstraction middlewares and graceful degradation logic.**

**2. Session Fidelity is the New UX Battleground**
Cross-project emphasis on compaction, budget limits, and context isolation proves that "infinite context" is an unsolved problem. Users are abandoning agents that hallucinate or lose conversational thread. Value for developers: **Context engineering (budgeting, dedup, isolation) is now a core competency, not a feature.**

**3. Desktop is the Differentiator**
Hermes and CoPaw are racing to build full Desktop IDEs. NanoClaw and OpenClaw are building web control planes. The terminal-only era is ending. Value for developers: **Agents that live in terminals will become secondary to agents with rich visual surfaces.**

**4. Safety is the Gate to Production**
PicoClaw’s coordinated vulnerability disclosure and OpenClaw’s stalled security reviews demonstrate that enterprise adoption is gated on rigorous sandboxing, SSRF protection, and RBAC. Value for developers: **Security reviews must be run as fast as feature sprints. Safety is a compliance requirement, not a checkbox.**

**5. The Race for Agentic Autonomy is Accelerating**
CoPaw’s community explicitly demands "learning loops" to match Hermes. Users want agents that self-correct, manage cron autonomously, and evolve their skill sets. Value for developers: **Static skill sets will lose to frameworks that enable runtime skill acquisition and memory-guided self-improvement.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the structured project digest for NanoBot (2026-06-10).

---

## NanoBot Project Digest | 2026-06-10

### 1. Today’s Overview
NanoBot is moving at a very high velocity. The last 24 hours saw **25 pull requests** updated and **6 active issues**, with the community submitting multiple, independent fixes for the same critical provider bug within hours of its report. The project is in a phase of rapid hardening: major security patches for symlink traversal and filesystem isolation are landing, a deep architectural memory bug has been surfaced, and significant WebUI features like conversation forking have been merged. While no new release was cut today, the volume of merged/closed PRs (10 total) indicates maintainers are actively integrating contributions rather than letting them stagnate.

### 2. Releases
No new releases were published on this date. The project appears to be accumulating significant changes in the main branch ahead of a future stable cut.

### 3. Project Progress
A strong set of high-impact features and infrastructure improvements were merged or closed today.

- **WebUI Conversation Forking ([#4208](https://github.com/HKUDS/nanobot/pull/4208)):** Users can now fork a new chat from any completed assistant response. The original conversation is preserved, and the new branch begins with an empty composer—a highly requested feature for iterative workflows.
- **Core User Autonomy ([#3400](https://github.com/HKUDS/nanobot/pull/3400)):** The Dream module’s ability to edit identity files (`USER.md` and `SOUL.md`) is now configurable. Users can lock these files to prevent the AI from modifying core identity prompts.
- **Documentation Revamp ([#4177](https://github.com/HKUDS/nanobot/pull/4177)):** Onboarding documentation was completely restructured to provide clear paths for beginners (no-background setup, CLI, WebUI, deployment), reducing friction for new contributors.
- **Platform Feature Parity ([#3434](https://github.com/HKUDS/nanobot/pull/3434)):** The Feishu/Lark channel now supports LaTeX rendering via CodeCogs, bridging a gap for technical users on that platform.
- **Codebase Modernization:** A minor internal workflow update ([#4265](https://github.com/HKUDS/nanobot/pull/4265)) was merged, adjusting a cron schedule for the `english-read` skill.

### 4. Community Hot Topics

- **Model Flexibility ([Issue #4253](https://github.com/HKUDS/nanobot/issues/4253) – 3 comments):** This is the community’s most discussed topic. The author describes a workflow that switches between a fast OpenRouter model and a slow private local model depending on privacy needs. The desire for **per-conversation model overrides** is a clear signal that users want session-level granularity, not just global defaults.

- **Architectural Integrity ([Issue #4259](https://github.com/HKUDS/nanobot/issues/4259) – 2 comments):** A deeply technical bug report from `chxuan` exposes that `history.jsonl` is **not session-isolated**. When the `ContextBuilder` injects “Recent History,” it merges summaries from *all* sessions, not just the current one. This is the most critical community analysis of the week, as it highlights a direct path to hallucination and data leakage between conversations.

- **Provider Ecosystem Friction ([Issue #4061](https://github.com/HKUDS/nanobot/issues/4061)):** A lingering bug where OpenAI-compatible providers that use plain-text tool call markup (instead of structured `tool_calls`) are completely ignored by the runner. This reflects a core architectural challenge of maintaining compatibility across a fragmented ecosystem of third-party backends.

### 5. Bugs & Stability

| Severity | Issue / PR | Description | Status |
|---|---|---|---|
| **Critical** | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | Cross-session context pollution via `history.jsonl` injection into system prompts. | **Open** – No fix PR yet. |
| **High** | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | `idleCompact` excludes the last 8 messages, causing it to summarize incorrect conclusions rather than user corrections. | **Open** – Core memory reliability failure. |
| **High** | [#4261](https://github.com/HKUDS/nanobot/issues/4261) | GPT-5.x and o-series models reject the `max_tokens` field; require `max_completion_tokens`. Blocks users on the latest models. | **2 Fix PRs Submitted** ([#4268](https://github.com/HKUDS/nanobot/pull/4268) & [#4263](https://github.com/HKUDS/nanobot/pull/4263)) |
| **High** | [#4267](https://github.com/HKUDS/nanobot/pull/4267) | WebUI silently drops assistant replies due to a WebSocket race condition. Data written to disk but not rendered. | **Fix PR Submitted** |
| **Medium** | [#4061](https://github.com/HKUDS/nanobot/issues/4061) | Structured tool calls not parsed when providers use text markup. Blocks agent functionality for many providers. | **Open** – No fix PR yet. |
| **Security** | [#4119](https://github.com/HKUDS/nanobot/pull/4119) | Blocks relative symlink escapes from the workspace during restricted commands. | **Fix PR Submitted** |
| **Security** | [#4053](https://github.com/HKUDS/nanobot/pull/4053) | Prevents write/edit tools from inheriting access to read-only media/extra directories. | **Fix PR Submitted** |

**Notable:** The rapid response to GPT-5.x compatibility ([#4261](https://github.com/HKUDS/nanobot/issues/4261))—with two separate authors submitting patches within hours—demonstrates a highly responsive contributor base, but the lack of a fix for the context pollution bug ([#4259](https://github.com/HKUDS/nanobot/issues/4259)) suggests a higher architectural complexity involved.

### 6. Feature Requests & Roadmap Signals

The community’s demands are painting a clear picture of the project’s immediate trajectory:

- **Dynamic Model Routing:** The top request ([#4253](https://github.com/HKUDS/nanobot/issues/4253)) is for session-level model overrides. This strongly suggests the roadmap should prioritize a **policy-based provider selector** that lets users assign models based on cost, capability, or privacy constraints.
- **Expanded Modalities:** The addition of the StepFun ASR provider ([#4260](https://github.com/HKUDS/nanobot/pull/4260)) signals that **voice transcription** is an active growth vector.
- **User Control over Autonomy:** The merge of the Dream identity file protection ([#3400](https://github.com/HKUDS/nanobot/pull/3400)) indicates a roadmap trend toward **user-configurable agent guardrails**, not just global on/off toggles.
- **UX Polish of Core Mechanics:** Smaller features like bot icon display on agent start ([#4262](https://github.com/HKUDS/nanobot/issues/4262)) and agent budget finalization messages ([#4269](https://github.com/HKUDS/nanobot/pull/4269)) show the community is shifting focus to **polish and reliability** rather than entirely new surface areas.

### 7. User Feedback Summary

The user base is heavily skewed toward **power users** who are deeply invested in the project’s stability and architecture.

- **Deep Technical Scrutiny:** Users are not filing surface-level bug reports. Issues like #4259 and #4061 contain root-cause analysis and data-flow diagrams. This indicates a high level of trust and technical sophistication, but also a low tolerance for non-deterministic behavior.
- **Workflow Reliability is Paramount:** The strongest pain points are related to **unreliable memory** (idleCompact losing corrections, context pollution) and **connection stability** (WebUI session drops). Users are relying on NanoBot for multi-step, long-running project work.
- **Positive Development Velocity:** The fact that a core incompatibility (GPT-5.x `max_tokens`, #4261) received two different fix PRs on the same day it was triaged is a strong signal of user satisfaction with the project’s responsiveness.
- **Desire for Granular Control:** Users consistently push against “one-size-fits-all” solutions, requesting per-session models, per-channel features (LaTeX), and the ability to lock identity files from the Dream module.

### 8. Backlog Watch

Several significant items are approaching the danger zone of staleness and require maintainer prioritization:

- **[Issue #4061](https://github.com/HKUDS/nanobot/issues/4061) – OpenAI Tool Call Parsing (12 days open):** This blocks agent execution for non-standard OpenAI-compatible providers. Despite a clear root cause analysis, no assignee or fix PR exists. This is the highest-risk unaddressed bug.
- **[PR #3869](https://github.com/HKUDS/nanobot/pull/3869) – DeepSeek Message Hardening (25 days open):** A large, feature-complete PR fixing `null` content errors and markdown injection for DeepSeek models. It appears to be awaiting a core maintainer review cycle, leaving a popular provider path fragile.
- **[PR #3983 / #3982 / #4193](https://github.com/HKUDS/nanobot/pull/3983) – Test Harnesses (13-17 days open):** A series of critical testing infrastructure contributions by `yu-xin-c` (scripted runner harness, memory lifecycle harness, blocked finish-reason coverage). These are crucial for preventing regressions but remain unmerged, slowing down the testing velocity of other PRs.
- **[PR #4053](https://github.com/HKUDS/nanobot/pull/4053) – Filesystem Isolation Security (12 days open):** A security hardening PR that prevents write tools from accessing read-only media directories. Security fixes benefit from fast merges to reduce exposure windows.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

**Hermes Agent Project Digest – 2026-06-10**

---

### 1. Today's Overview
The project saw an extreme surge in activity on June 10, with **50 Issues** and **50 Pull Requests** receiving updates—among the highest single-day engagement levels on record for Hermes Agent. Despite this flood of input from the community, the review and merge pipeline is critically strained: only **1 Issue was closed** and **1 PR was merged**. This highly lopsided ratio (49:1 open vs. closed/merged) suggests either a deliberate pre-release freeze or a significant maintainer bandwidth bottleneck. No new releases were published today. The content of incoming work is heavily concentrated on Windows/macOS stability fixes, Desktop UI polish, and multi-platform gateway integration.

---

### 2. Releases
**None.** No new versions were tagged today.

---

### 3. Project Progress
Merge throughput on `main` was minimal despite very high activity. Exactly **1 PR** was merged and **1 Issue** was closed. While the specific merged items fall outside the top-comment data sampled here, the broader context of the PR queue reveals significant community-driven forward motion: systematic fixes for Windows process detachment ([#43252](https://github.com/NousResearch/hermes-agent/pull/43252), [#43253](https://github.com/NousResearch/hermes-agent/pull/43253)), critical agent reliability fixes ([#43269](https://github.com/NousResearch/hermes-agent/pull/43269)), and major Desktop UI work ([#42521](https://github.com/NousResearch/hermes-agent/pull/42521)) are all queued and awaiting maintainer review.

---

### 4. Community Hot Topics
- **Agent Safety & LLM Compliance** – [#43245](https://github.com/NousResearch/hermes-agent/issues/43245) is the highest-engagement item today. Users universally report that models ignore the configured PTY terminal tool when `sudo` is required, instead attempting raw shell access. This reflects a core tension between prompt engineering and base-model behavior.
- **Platform Integration Pain** – Two duplicate bugs highlight sharp edges: [#42086](https://github.com/NousResearch/hermes-agent/issues/42086) (Gemini 2.x vision unsupported) and [#42084](https://github.com/NousResearch/hermes-agent/issues/42084) (WeChat Silk audio cannot be transcribed). Both show high community demand for broader media tooling support.
- **Desktop UX Battle** – Significant debate around the Desktop frontend. PR [#42521](https://github.com/NousResearch/hermes-agent/pull/42521) (VS Code-themed resizable terminal pane) is a major talking point, while users hit hard edges like UI overlap ([#39657](https://github.com/NousResearch/hermes-agent/issues/39657)) and message clipping ([#42992](https://github.com/NousResearch/hermes-agent/issues/42992)).
- **Provider Reliability** – [#43211](https://github.com/NousResearch/hermes-agent/issues/43211) discusses the flaw where stale stream kills silently retry the *same* provider instead of triggering runtime fallback. A dedicated fix PR ([#43269](https://github.com/NousResearch/hermes-agent/pull/43269)) is already proposed.

---

### 5. Bugs & Stability
**Critical (No immediate fix visible):**
- [#43242](https://github.com/NousResearch/hermes-agent/issues/43242): Desktop crash on macOS 26.5.1 (Fatal V8 OOM). No maintainer response yet.
- [#43196](https://github.com/NousResearch/hermes-agent/issues/43196): Dashboard wedges hard under Systemd, requiring SIGKILL.

**High Severity (P2, with Fix PRs incoming):**
- [#43211](https://github.com/NousResearch/hermes-agent/issues/43211) → [#43269](https://github.com/NousResearch/hermes-agent/pull/43269): Stale stream failover ignored.
- [#43175](https://github.com/NousResearch/hermes-agent/issues/43175) → [#43267](https://github.com/NousResearch/hermes-agent/pull/43267): Bookend context bloat in session_search.
- [#43253](https://github.com/NousResearch/hermes-agent/pull/43253) / [#43252](https://github.com/NousResearch/hermes-agent/pull/43252): Systemic `windows_detach_popen_kwargs` failures for local environments and cron.

**Regressions:**
- [#43099](https://github.com/NousResearch/hermes-agent/issues/43099): Loss of Chromium browser tool (marked `needs-repro`).
- [#43042](https://github.com/NousResearch/hermes-agent/issues/43042): Desktop sidebar file browser ENOENT after `session.info` event.

---

### 6. Feature Requests & Roadmap Signals
- **Provider Diversification** – [#29331](https://github.com/NousResearch/hermes-agent/issues/29331) (Volcengine / ByteDance) signals a strategic push into the Chinese cloud ecosystem.
- **Desktop Maturation** – [#43255](https://github.com/NousResearch/hermes-agent/pull/43255) (Native OS notifications) and [#42521](https://github.com/NousResearch/hermes-agent/pull/42521) (Terminal pane) show the Desktop is being positioned as a full IDE.
- **Architecture Evolution** – RFC [#36765](https://github.com/NousResearch/hermes-agent/issues/36765) proposes a major refactor of `ContextEngine` to split “context selection” from “compression.” This is a strong roadmap signal for the next major version.
- **Granular Configuration** – [#31375](https://github.com/NousResearch/hermes-agent/issues/31375) (Per-tool enable/disable) and [#13107](https://github.com/NousResearch/hermes-agent/issues/13107) (Description override) suggest the config system is due for a deep UX pass.
- **Plugin Ecosystem Expansion** – [#20307](https://github.com/NousResearch/hermes-agent/issues/20307) requests a `transform_api_message` hook, indicating power users need deeper API-level plugin integration.

---

### 7. User Feedback Summary
- **LLM Compliance Frustration** – The dominant pain point is models disobeying the explicit skill/tool constraints, particularly around `sudo` access ([#43245](https://github.com/NousResearch/hermes-agent/issues/43245)). Users feel the safety architecture is fighting the model’s training.
- **Configuration Drift** – Multiple reports of `config.yaml` values being silently ignored (title generation [#41744](https://github.com/NousResearch/hermes-agent/issues/41744), `public_url` [#42780](https://github.com/NousResearch/hermes-agent/issues/42780), `bedrock.profile` [#43143](https://github.com/NousResearch/hermes-agent/issues/43143)). This erodes trust in documentation.
- **Desktop Parity** – Users are actively comparing Hermes Desktop against Codex and WorkBuddy. The demand is clear: native notifications, reliable session rendering, and IDE-grade polish.
- **Windows Support** – A concentrated burst of Windows-specific PRs indicates a growing but underserved user base encountering systematic process handling failures.

---

### 8. Backlog Watch
- **Matrix Feature Request** – [#7507](https://github.com/NousResearch/hermes-agent/issues/7507) (Configurable reply quoting for Matrix, opened April 11). A minor but blocking UX issue for Matrix users with no movement in 2 months.
- **Critical Reliability PR Stalled** – [#26051](https://github.com/NousResearch/hermes-agent/pull/26051) (Preserve context on compression failures). Open since May 15, this P2 PR is a fundamental safety net for agent memory.
- **No Maintainer Response on macOS Crash** – [#43242](https://github.com/NousResearch/hermes-agent/issues/43242) (Fatal OOM on macOS 26.5.1) has received zero maintainer triage. This is a high-risk gap for the macOS user segment.
- **Issue Tracker Hygiene** – Nearly a third of the top recent bugs carry the `duplicate` tag (`#42086`, `#42084`, `#43042`, `#43243`, `#43247`, `#43261`). The tracker would benefit from a systematic grooming session to surface unresolved root causes.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-10

## 1. Today's Overview
Today's digest captures a pivotal security-hardening sprint for PicoClaw, triggered by a coordinated disclosure of 11 vulnerabilities from researcher YLChen-007. Despite this heavy triage load, the project maintained high development velocity with 16 PRs updated and a new nightly build published. The maintainers demonstrated strong responsiveness, with targeted fix PRs opened for SSRF bypasses and launcher access controls within hours of disclosure. Overall project health is robust but currently in an intense patch cycle, reflecting both rapid feature growth and the inherent security surface area of a multi-channel, tool-executing agent framework.

## 2. Releases
- **Nightly Build v0.2.9-nightly.20260610.b9a8fad6**
  - Automated build synced to `main`, incorporating the latest merged fixes for config migration type assertions, Claude Opus 4-7 temperature handling, and default model ID corrections.
  - **Stability Warning:** Explicitly marked as potentially unstable by maintainers.
  - **Full Changelog:** [https://github.com/sipeed/picoclaw/compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
  - *No breaking changes or formal migration notes accompany this nightly.*

## 3. Project Progress
- **Agent Collaboration Bus (PR #2937 — Closed):** A major architectural feature reached a closed state. It introduced per-agent mailboxes, structured collaboration threads, and permission-aware delivery. While carrying a `[stale]` label, its resolution signals significant progress toward first-class multi-agent orchestration in PicoClaw.
- **Provider Compatibility Fixes (PRs #2940, #2942 — Merged):** Two critical provider bugs were resolved. The `claude-opus-4-7` temperature deprecation error (HTTP 400) was fixed by omitting the parameter for affected models. The default `claude-sonnet` model ID was corrected from dotted to canonical hyphenated form.
- **Config Hardening (PR #3064 — Merged):** A panic in config migration caused by an unchecked type assertion on model name indexing was safely resolved.
- **Documentation (PR #3086 — Merged):** WeChat QR code documentation was refreshed.

## 4. Community Hot Topics
- **Security Audit Firestorm (Issues #3068–#3082):** The single most impactful topic is the 11-issue vulnerability disclosure. While the issues themselves have zero public comments (suggesting responsible disclosure or very recent filing), they dominate the project's immediate attention. This represents a significant trust signal: PicoClaw is being audited by serious security researchers, implying production/enterprise deployment growth.
- **Streaming Config Demand (Issue #2404):** The longest-running feature request with the highest engagement (11 comments, 4 👍). Users explicitly request `"streaming": true` config parity with the OpenAI Python client. The underlying need is clear: native support for streaming LLM responses is a blocker for many adopters.
- **Multi-Agent Interest (PR #2937):** The Agent Collaboration Bus PR, even in closed state, reflects deep community investment in managed multi-agent workflows rather than simple single-agent chat.
- **Platform Pain Points (Issues #2796, #2472):** Recently closed issues around Windows path handling and historical message display were persistent user frustrations that now have fix paths.

## 5. Bugs & Stability

**Critical**
- **`exec` Tool Sandbox Escapes (Issues #3079, #3081):** A whitelist bypass via `jq` environment disclosure and a symlink race in the approval hook `cwd` were reported. These expose the host to arbitrary execution and represent the highest risk items in the batch.

**High**
- **Multiple SSRF Guard Failures (Issues #3074, #3077, #3078):** Bypass vectors for `web_fetch` were disclosed via ISATAP IPv6 embedding, the `198.18.0.0/15` benchmark range, and environment-configured HTTP proxies. **Fix PR #3085** is already open blocking `198.18.0.0/15`.
- **Launcher Access Control Bypasses (Issues #3069, #3072, #3080):** The `allowed_cidrs` feature can be bypassed through same-host reverse proxies and loopback proxying. The first-run setup is also vulnerable to CSRF. **Hardening PR #3083** is under review.
- **Untrusted Skills Auto-Loading (Issue #3075):** Local `skills/` metadata from CWD is automatically pulled into the system prompt, a subtle but dangerous injection vector.

**Medium**
- **Channel Authorization Bypasses (Issues #3068, #3070, #3073, #3076):** Vulnerabilities in MQTT (`client_id` spoofing), OneBot (unvalidated media URL fetch), LINE (webhook replay), and WeCom (untriggered group messages) compromise channel-scope security guarantees.
- **WebSocket `/reload` Access (Issue #3071):** Authenticated WebSocket clients can trigger an unauthorized runtime configuration reload.
- **Empty LLM Response Retry (PR #2983 — Open):** A gap where empty 200 responses from OpenAI-compatible providers are not retried.

**Low / Resolved**
- `claude-opus-4-7` temperature error (Issue #2939) → **Resolved** by merged PR #2940.
- History display bug (Issue #2796) → **Fix** pending in Open PR #2990.

## 6. Feature Requests & Roadmap Signals

**Definite (Next Stable Release)**
- **Security Hardening:** The volume and severity of today's disclosures guarantee a coordinated security release (`v0.2.10` or `v0.3.0`). Fix PRs #3085 (SSRF range block) and #3083 (launcher access control) are strong indicators of what will land first.

**Probable**
- **Agent Collaboration Bus (PR #2937):** The closure of this feature PR suggests it is staging for merge, bringing durable inter-agent messaging to the next minor release.
- **Native Streaming Config (Issue #2404):** With strong community signal and relatively narrow implementation scope, this is the most likely community-requested feature to ship soon.
- **NEAR AI Cloud Provider (PR #2917):** This fully scoped first-class provider integration is awaiting review and merge.

**Possible**
- **Vodozemac Migration (Issue #3088):** Given the day's security theme, replacing the insecure `libolm` dependency aligns well with the project's hardening trajectory.
- **WebSocket Turn Completion Signal (Issue #2984):** Important for the external Pico Protocol client ecosystem but currently has low discussion volume.

## 7. User Feedback Summary
- **Pain Points:** The `claude-opus-4-7` temperature regression caused real API friction for users—direct frustration over a previously working model. Windows path handling and message history display were longstanding UX frictions only recently addressed. The security disclosures, while authored by a researcher, reflect advanced users operating PicoClaw in sensitive production environments facing real gaps in SSRF and sandbox defaults.
- **Satisfaction:** The rapid iteration on features like the Agent Bus and the immediate publishing of security fix PRs within the same 24-hour window demonstrate strong maintainer engagement. Community trust is evidenced by the willingness of external contributors to provide major features (NEAR AI, DeltaChat) and conduct deep security audits.
- **Dissatisfaction:** The persistent lack of OpenAI streaming parity (#2404) remains the single clearest gap between user expectations and platform capabilities. The "stale" bot closing complex issues/PRs without maintainer resolution creates minor friction for long-tail contributors.

## 8. Backlog Watch
- **Issue #2404 (Streaming Config):** The highest-voted feature request, dormant for 2 months with 11 comments. A maintainer update on priority or design decision is needed to close the feedback loop with an engaged community.
  [https://github.com/sipeed/picoclaw/issues/2404](https://github.com/sipeed/picoclaw/issues/2404)

- **Issue #2984 (WebSocket Turn Completion):** Critical for the DX of third-party Pico Protocol developers, but low engagement means it risks remaining unprioritized.
  [https://github.com/sipeed/picoclaw/issues/2984](https://github.com/sipeed/picoclaw/issues/2984)

- **Issue #3088 (Vodozemac):** Newly filed but directly addresses an insecure, unmaintained dependency (`libolm`). Should be kicked into active discussion to avoid becoming a stale security debt item.
  [https://github.com/sipeed/picoclaw/issues/3088](https://github.com/sipeed/picoclaw/issues/3088)

- **PR #2983 (Empty LLM Response Retry):** A 9-day-old open fix for a silent failure mode without maintainer comments. It represents a gap in the LLM loop logic that deserves formal review.
  [https://github.com/sipeed/picoclaw/pull/2983](https://github.com/sipeed/picoclaw/pull/2983)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest | 2026-06-10**

**1. Today's Overview**
NanoClaw experienced an extraordinary wave of maintenance and feature consolidation today, with 39 pull requests closed or merged—a massive cleanup of the backlog dating back to February 2026—while 4 new or revised PRs remain open. Key long-anticipated features crossed the finish line, including a built-in Web UI, a Docker-free direct runner mode, and an official Skill Marketplace. The single active issue updated in the last 24 hours revolves around a strategic multi-runtime agent abstraction, signaling the community’s strongest architectural desire. No formal release was cut, but the project has clearly assembled several critical components of its next major iteration in a single day.

**2. Releases**
No new releases were published in the last 24 hours.

**3. Project Progress**
The day’s merged PRs represent major strides across the platform, infrastructure, and community ecosystem:

- **Core Platform & Infrastructure:**
  - **WebUI Control Panel** ([PR #212](https://github.com/nanocoai/nanoclaw/pull/212)): A full web dashboard at `localhost:3100` with 11 tabs (Chat, Overview, Channels, Groups, Messages, Tasks, Sessions, Skills, Config, Logs, Debug), built on Lit + Vite + Fastify.
  - **Direct Runner Mode** ([PR #1285](https://github.com/nanocoai/nanoclaw/pull/1285)): Introduces `NANOCLAW_DIRECT_RUNNER=1` to run the agent SDK in-process, eliminating Docker overhead for development.
  - **Skill Marketplace** ([PR #1309](https://github.com/nanocoai/nanoclaw/pull/1309)): CLI commands to discover, install, and manage skills from GitHub-hosted repositories.
  - **Plugin System** ([PR #1387](https://github.com/nanocoai/nanoclaw/pull/1387)): Formalizes a plugin architecture analogous to the channel pattern.

- **Observability & Governance:**
  - **Agent Trace Observability** ([PR #1202](https://github.com/nanocoai/nanoclaw/pull/1202)) and **Prompt Trace Logging** ([PR #337](https://github.com/nanocoai/nanoclaw/pull/337)): Full agent invocation traces and configurable JSONL logging.
  - **Approval-Gated Skills** ([PR #1245](https://github.com/nanocoai/nanoclaw/pull/1245)): `/approve` and `/reject` commands for secure mutable operations.
  - **Build-Time Version Metadata** ([PR #1333](https://github.com/nanocoai/nanoclaw/pull/1333)): Git commit and timestamp now logged at startup.

- **Stability & Security:**
  - **Feishu Zombie Card Fix** ([PR #2718](https://github.com/nanocoai/nanoclaw/pull/2718)): Production bug squashed where interactive cards got stuck in “running” state after agent-runner timeouts.
  - **Telegram Security Fix** ([PR #2722](https://github.com/nanocoai/nanoclaw/pull/2722) – *open*): Switches pairing code generation from `Math.random` to `crypto.randomInt`.

- **Documentation & Skills:**
  - **Security Audit** ([PR #214](https://github.com/nanocoai/nanoclaw/pull/214)) formally accepted.
  - **Finance DD Agent** ([PR #2723](https://github.com/nanocoai/nanoclaw/pull/2723)) added fresh today.
  - **Container Sandbox Design** ([PR #1084](https://github.com/nanocoai/nanoclaw/pull/1084)) and various JSDoc improvements merged.

**4. Community Hot Topics**
- **Multi-Runtime SDK Abstraction** ([Issue #1690](https://github.com/nanocoai/nanoclaw/issues/1690)): The hottest open topic with 5 comments and 3 👍 reactions. Author `chiptoe-svg` proposes an `AgentRuntime` interface mirroring the channel pattern to swap Claude, Codex, and local model runtimes. The underlying need is clear: the community strongly desires to decouple NanoClaw from single-vendor model dependency. The issue was updated today and remains the most active strategic discussion.
- **High-Velocity Skill Contributions:** The rapid opening and merging of the Finance Due Diligence Agent ([PR #2723](https://github.com/nanocoai/nanoclaw/pull/2723)) demonstrates the success of the skills-based extensibility model. Community members are quickly building and shipping domain-specific vertical agents.

**5. Bugs & Stability**
- **Critical (Fix Merged):**
  - **Feishu Stuck Cards** ([PR #2718](https://github.com/nanocoai/nanoclaw/pull/2718)): Cards showed “running” for 50+ minutes after `agent-runner` was killed by `PROCESS_TIMEOUT`. Root cause was `deleteActiveCard(jid)` only firing inside the SDK’s `final` event handler. Fix merged today.
- **High (Fix Open – Needs Review):**
  - **Telegram Predictable Pairing Codes** ([PR #2722](https://github.com/nanocoai/nanoclaw/pull/2722)): `generateCode` used `Math.random()`, making the first pairer (who can be promoted to owner) predictable. Switched to `crypto.randomInt`. This patch should be reviewed and merged as a priority.
- **Medium (Documented):**
  - **Security Audit Documentation** ([PR #214](https://github.com/nanocoai/nanoclaw/pull/214)): Formally documents SDK credential isolation (FINDING-02) and Apple Container network egress (FINDING-03) risks.

**6. Feature Requests & Roadmap Signals**
The roadmap is strongly pulling in two directions: operational simplicity and platform extensibility.

- **Multi-Runtime Support** ([Issue #1690](https://github.com/nanocoai/nanoclaw/issues/1690)) is the dominant roadmap signal. With the PR backlog effectively cleared, this is the strongest candidate for the next formal feature cycle.
- **Direct Runner** ([PR #1285](https://github.com/nanocoai/nanoclaw/pull/1285)) addresses the top operational pain point (Docker complexity) and will likely become the default path for local development.
- **Ecosystem Launch:** The merging of the **Skill Marketplace** (#1309) and **Plugin System** (#1387) suggests a public curated registry or “app store” is the logical next step for the project.

**7. User Feedback Summary**
- **Pain Points Addressed:**
  - *Docker complexity* (the #1 cited friction) is resolved by Direct Runner mode (#1285).
  - *Vendor lock-in / lack of model choice* is actively debated in the multi-runtime proposal (#1690).
  - *Security gaps* are being closed (Telegram pairing fix in review, Feishu zombie bug squashed).
- **Satisfaction Signals:**
  - **Contributor velocity is extremely high:** 43 PRs updated in a single day, with many directly from community members building new skills. The extensibility model is thriving.
  - **Enterprise adoption signals:** Governance features like approval gating (#1245) and formal security audits (#214) show production/enterprise use-cases are shaping the roadmap.
  - **Responsive maintainership:** The aggressive cleanup of a months-long backlog of “Blocked” and “Needs Review” PRs indicates a project that actively values its contributors.

**8. Backlog Watch**
The project’s backlog was functionally reset today, with dozens of lingering PRs from February/March 2026 finally definitively closed or merged. This is a strong positive signal for project health.

- **Immediate Review Required:**
  - **[PR #2722](https://github.com/nanocoai/nanoclaw/pull/2722) (Telegram Security Fix)**: Open security patch. Should be prioritized.
  - **[PR #2721](https://github.com/nanocoai/nanoclaw/pull/2721) (Customization Docs)**: Critical onboarding documentation awaiting review.
- **Unresolved Strategic Discussion:**
  - **[Issue #1690](https://github.com/nanocoai/nanoclaw/issues/1690) (Multi-Runtime SDK Abstraction)**: Open since April 7. With the queue cleared and community interest high, this issue represents the project’s most important open design conversation and should be top of mind for maintainers.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest: 2026-06-10

## 1. Today's Overview

NullClaw experienced a concentrated burst of maintenance activity on June 9–10, 2026, with 8 pull requests and 5 issues updated within the last 24-hour window. The project is currently in a stabilization phase following recent feature releases, with no new releases cut today. Community contributors are driving a rapid bug-fix cycle, particularly around Telegram interaction UX, provider interoperability, and agent configuration efficiency. The most architecturally significant development is the conclusion of the long-running cross-memory feature branch (PR #711), while a critical open issue regarding agent-type cron job subprocess spawning (#941) remains the most prominent destabilizing factor.

---

## 2. Releases

*No new releases in the observed period.*

---

## 3. Project Progress

Seven pull requests were merged or closed in this period, reflecting strong forward momentum in both platform features and system stability:

**Major Infrastructure**
- **PR #711 – Cross-Memory Event Stream** (DonPrus, closed): Spans from March to June 2026. Adds a deterministic memory event stream enabling memory synchronization across agent instances. This is a foundational capability for multi-agent and persistent-context use cases.
- **PR #947 – Evolink Provider** (EvoLinkAI, closed): Adds first-class support for the Evolink multi-model gateway (GPT-5, Gemini, DeepSeek, etc.) as an OpenAI-compatible provider, expanding the project's provider ecosystem.

**Agent System Fixes**
- **PR #946 – Tool Filtering in System Prompts** (vernonstinebaker, closed): Filters built-in and MCP tools in text-based system prompts according to `tool_filter_groups`, preventing dynamic-group tools from leaking into prompt text.
- **PR #939 – `compact_context` Flag Fix** (raskevichai, closed): Resolves a dead flag where `AgentConfig.compact_context` was parsed but never consumed at runtime; `autoCompactHistory()` now respects the user's preference.

**Platform & Integration Fixes**
- **PR #945 – PII Redaction False Positives** (vernonstinebaker, closed): Adds `isDateLike()` guard to reject ISO date/time patterns from being incorrectly redacted as phone numbers.
- **PR #943 – Telegram Typing Indicator** (raskevichai, closed): Adds `sendChatAction("typing")` for callback query processing, resolving a UX gap where inline buttons produced no visual feedback.
- **PR #940 – Custom Provider Model Discovery** (raskevichai, closed): Ensures custom OpenAI-compatible providers are queried at their `base_url` `/v1/models` endpoint instead of falling back to hardcoded model lists.

---

## 4. Community Hot Topics

The most active discussion centers on agent scheduling reliability and provider flexibility:

**Agent Cron Reliability** (Highest Activity)
- **[Issue #941](https://github.com/nullclaw/nullclaw/issues/941)** (weissfl, open, 1 comment): Reports that Agent-type cron jobs are marked complete but spawn no subprocess, blocking Telegram delivery. This represents a critical workflow gap for users relying on scheduled agent execution.
- **[PR #948](https://github.com/nullclaw/nullclaw/pull/948)** (DonPrus, open, updated today): Attempts to fix cron agent delivery attribution, passing origin metadata into spawned subprocesses. Whether this fully resolves the underlying subprocess spawning issue in #941 is an open question.

**Provider Ecosystem & Model Discovery**
- A cluster of issues (#936) and fixes (#940, #947) indicates strong community demand for flexible, user-defined model backends. The quick turnaround (issue filed May 27, PR merged May 29) shows this is a priority workflow for users bringing custom API gateways.

**Notable Community Contributors**
- **weissfl** – Filed the most critical bug reports (#941, #936, #937, #942), serving as a primary quality assurance driver.
- **raskevichai** – Delivered three targeted fixes (#939, #940, #943), displaying rapid response to community-reported issues.
- **vernonstinebaker** – Self-filed and self-fixed (#944 → #945), demonstrating a strong contributor-loop model.

---

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|---|---|---|---|
| **Critical** | [#941](https://github.com/nullclaw/nullclaw/issues/941) – Agent cron jobs fail to spawn subprocesses | Open | Blocks all scheduled agent delivery via Telegram. Currently the highest-priority open stability concern. |
| **Medium** | [#936](https://github.com/nullclaw/nullclaw/issues/936) – Custom providers fall back to hardcoded models | Resolved (PR #940) | Provider discovery now correctly queries remote `/v1/models`. |
| **Medium** | [#944](https://github.com/nullclaw/nullclaw/issues/944) – PII redactor mangles date/time output | Resolved (PR #945) | False phone-number matches on timestamps are now guarded against. |
| **Low** | [#942](https://github.com/nullclaw/nullclaw/issues/942) – Missing typing indicator on inline buttons | Resolved (PR #943) | Now sends `sendChatAction` for callback queries. |
| **Low** | [#937](https://github.com/nullclaw/nullclaw/issues/937) – Dead `compact_context` configuration flag | Resolved (PR #939) | Flag now controls history compaction behavior. |

**Assessment:** Bug hygiene is high—four of five reported issues have matching fix PRs already merged. The lone open issue (#941) is a genuine blocker that likely requires deeper investigation into the cron process manager or subprocess lifecycle.

---

## 6. Feature Requests & Roadmap Signals

Several signals indicate the direction of the next release cycle:

**Likely Incoming (Next Release)**
- **Cross-Memory Synchronization (#711)**: The most substantial feature to land since March. Expect documentation, configuration examples, and follow-up issues as the community adopts multi-instance memory.
- **Provider Abstraction Hardening**: The Evolink addition (#947) and custom provider fixes (#940) suggest the API gateway layer will continue to expand, potentially toward dynamic provider registration.

**Strong Community Demand Observed**
- **Scheduled Agent Reliability (#941)**: The cron subprocess bug is the single loudest demand signal. A fix is almost certainly prioritized for the next patch release.
- **Deterministic Agent Configuration (#939, #946)**: Users are pushing for config flags to actually govern behavior and for prompt construction to respect tool filter scopes. Expect further config validation improvements.
- **Evolink (#947)**: A user-contributed provider integration. Indicates demand for multi-model gateways as first-class citizens, not just bare OpenAI-compatible endpoints.

**Speculative (Based on Trends)**
- Enhanced process monitoring for cron/spawned agents.
- Further MCP tool-group lifecycle refinements.
- Telegram UX may see additional polish (message formatting, error feedback).

---

## 7. User Feedback Summary

Feedback is conveyed primarily through high-quality bug reports and self-authored fixes rather than feature requests or comments, indicating a technically sophisticated user base.

**Pain Points Expressed:**
- **Automation Reliability**: The #941 cron bug represents a fundamental trust issue for scheduled workflows. Users expect scheduled tasks to execute reliably.
- **Provider Transparency**: #936 highlights frustration when the system silently falls back to hardcoded models instead of reporting an unavailable or unqueried provider.
- **Data Integrity Anxiety**: #944 (date/time redacted as phone numbers) is a sensitive class of bug—users expecting accurate timestamps in logs or agent output faced silent data corruption.
- **UX Friction**: #942 (silent button presses) degrades the interactive experience, making it hard for users to distinguish thinking from failure.

**Satisfaction Signals:**
- The rapid closure of community-filed bugs (avg. <7 days from report to fix) suggests strong maintainer engagement.
- Contributors are willing to invest significant development effort (#711 by DonPrus, #947 by EvoLinkAI), signaling a healthy open-source project ecosystem.
- Users are not merely filing issues; they are debugging and contributing patches (vernonstinebaker, raskevichai), a strong indicator of project stickiness.

---

## 8. Backlog Watch

**Critical Item: Issue #941 – Agent Cron Job Spawning**
- Filed: May 31, 2026
- Status: Open, 1 comment
- Risk: Blocks a core use case (scheduled agent execution).
- Watch factor: Related PR #948 addresses delivery attribution but may not resolve the fundamental subprocess spawning failure. This issue needs either a reproducer from the reporter or a maintainer investigation.

**High-Risk Integration: PR #711 – Cross-Memory Feature**
- Filed: March 23, 2026
- Merged/Closed: June 9, 2026
- Risk: This is a large, long-lived feature branch. While likely well-reviewed, the surface area for regressions is significant. Expect follow-up issues regarding:
  - Backward compatibility with existing memory stores.
  - Performance characteristics under concurrent agent access.
  - Edge cases in event stream determinism.

**No Issues Older Than 30 Days Appear Unaddressed in the Provided Window**
- The 5 most recently updated issues are all from late May/early June and are actively being resolved. The healthy average time-to-fix suggests maintainers are not accumulating technical debt on recent reports.
- Maintainers should watch for fresh issues stemming from the cross-memory rollout over the next 1–2 weeks.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw Project Digest — 2026-06-10**

**1. Today's Overview**
The IronClaw project is deep in its "Reborn" production cutover sprint, with exceptionally high activity across the board (45 Issues, 50 PRs updated in 24h). The team has closed several major milestones, including the OpenAI-compatible API migration, while simultaneously stacking large feature work for universal attachments, admin lifecycle management, and observability. This velocity is, however, exposing integration regressions. Three critical bugs related to provider compatibility and configuration persistence emerged today that threaten user trust in the new runtime. Overall, the project is healthy and executing aggressively, but a stabilization cycle may be imminent.

**2. Releases**
No new releases were published during this observation window.

**3. Project Progress**

**Major Milestones Closed**
- **OpenAI-compatible API Migration (#4447, #4446):** Final acceptance and SSE streaming work for the Reborn OpenAI-compatible surface is complete, closing the overarching migration epic (#3283).
- **Reborn WebUI Beta Audit (#4609):** Authentication parity across bearer/DB/OIDC/query-token paths for WebChat v2 has been audited and tested.
- **Operator Command-Plane (#4591):** The shared typed surface for setup, config, diagnostics, and lifecycle APIs has been successfully foundational.

**In-Flight Feature Work (Active PR Stacks)**
- **Universal Attachments (Epic #4644):** A coordinated six-PR stack is actively landing the full attachment pipeline—format registry (#4654), transcript refs (#4655), byte storage backend (#4668), inbound byte bridge (#4670), and WebChat v2 upload wiring (#4672). This represents a massive coordinated engineering push.
- **Admin & Safety:** Persistent approval policies with scoped allow/revoke (#4613) and scoped admin lifecycle for shared capabilities (#4544) are being wired.
- **Observability & Readiness:** Trajectory observer hooks and LLM provider injection (#4588, #4671) are being finalized alongside production readiness diagnostics (#4626, #4627).
- **Slack Enhancements:** Personal DM outbound target support (#4600) has been added to the Slack provider surface.
- **New Extension:** A "read-only NEAR mainnet" first-party extension has been contributed by a new contributor (#4661).

**Structural Improvements**
- Project-scoped automation ownership core model (#4663) and vocabulary surface (#4664) have been introduced.
- Security audit coverage for MCP lease denials (#4561) and auth continuation failures (#4562) has been expanded.

**4. Community Hot Topics**
- **Reborn Production Cutover (Issue #3026, 3 comments):** The most active discussion point. The community is tracking how the configured production graph will be built, validated, and gated. Multiple sub-issues are being filed and closed, signaling intense "go-live" preparation.
- **Provider API Regressions (Issues #4548, #4642):** Two blocking bugs are generating discussion from users of non-OpenAI APIs. DeepSeek integration is broken by a duplicate `model` field (#4548). Strict-mode providers (Anthropic, Google Vertex, etc.) are completely blocked when using first-party tools due to capability-port validation rejecting `null` optional fields (#4642).
- **Feature Demand:** High volumes of enhancement requests for multi-user support (#4628), unified search (#4647), and Slack channel-routed agents (#4625) demonstrate strong community appetite for IronClaw to scale into a team-oriented platform.

**5. Bugs & Stability** (Links to Issue Tracker)

**Critical**
- **Strict-Mode Provider Rejection (#4642):** Reborn's capability-port validation rejects valid tool calls from strict-mode LLM providers when `null` is sent for unset optionals. This blocks a significant portion of first-party tools across major providers. *(No fix PR identified in the current open stack.)*
- **DeepSeek Duplicate Model Field (#4548):** Chat completion requests with tools serialize two top-level `model` keys, causing HTTP 400 rejections from DeepSeek's API. *(Immediate regressive impact on DeepSeek users.)*
- **NEAR AI Config Persistence Failure (#4673):** "Test connection" succeeds but "Save" fails silently. New users of NEAR AI cannot complete onboarding. *(Created today, requires urgent triage.)*

**High/Medium**
- **Google Calendar Unordered Events (#4640):** `list_events` lacks a lower time bound and ordering, causing "upcoming meetings" queries to return the oldest events and recurring masters rather than upcoming instances. Significant data-quality degradation.

**6. Feature Requests & Roadmap Signals**

**Likely Next-Release Features**
- **Universal Attachments (#4644):** The investment in this 6-PR stack makes it the strongest candidate for the next major Reborn release.
- **Admin-Shared Tools & Skills (#4628):** PR #4544 directly serves this request. Multi-tenant capability provisioning is clearly a P1 priority for the core team.
- **Persistent Approval Policies (#4613):** Closely tied to safety and admin surfaces, this is reading as a release blocker for team deployments.
- **Ask-Gated REPL Approvals (#4667):** Developer platform maturity is being explicitly prioritized.

**On Deck / Scoping**
- **Unified Search (#4647):** Filed by a project lead (ilblackdragon) with a detailed gap analysis. Expected to enter sprint planning shortly after the attachment pipeline lands.
- **Internal Hosted Deployment (#4646):** Noted as "on Railway." This signals active work toward a hosted/SaaS version of IronClaw Reborn.
- **Google OAuth Unification (#4657):** Work to eliminate redundant auth gates across GSuite scopes is being tracked.

**7. User Feedback Summary**

**Satisfaction Signals**
- The rapid pace and architectural ambition of Reborn are energizing power users, who are filing detailed, high-quality enhancement requests (#4647, #4625).
- New contributors are actively adding first-party extensions (#4661), indicating a healthy developer experience for contributors.

**Pain Points**
- **"Save is broken" (#4673):** Direct loss of trust in the configuration UX for new users.
- **"My provider is blocked" (#4548, #4642):** Frustration from users testing the new runtime who encounter regressions that interrupt existing workflows.
- **"Wrong data returned" (#4640):** The calendar tool degradation signals a gap in integration acceptance testing for first-party extensions.
- **Developer Friction (#4665, #4666):** File-size cap warnings on `slack_host_*.rs` files (2,823+ lines) are directly impacting contributor PR workflows as the codebase outgrows its original structure.

**8. Backlog Watch**

- **Security Hardening Epic (Issue #88):** Created 2026-02-14 (nearly 4 months old). Covers device pairing, media URL validation, and safe binaries, but has received no dedicated sprint focus during the Reborn rewrite. As Reborn approaches production, this backlog item carries growing security risk.
- **New Contributor PR (PR #4521):** A JSON cleaner/sanitizer submitted by Dannye013 with zero maintainer comments since 2026-06-06. Early-stage external contributions need timely engagement to sustain contributor health.
- **Reborn Cutover Epic (Issue #3026):** While actively managed, the sheer number of open sub-issues and 48 open PRs creates a "long tail" risk. Scope discipline will be critical to avoid the cutover timeline slipping.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for June 10, 2026, based on the latest GitHub activity.

---

## LobsterAI Project Digest — 2026-06-10

### 1. Today's Overview
LobsterAI is maintaining a high development velocity today, with **3 pull requests merged** and **1 new issue** opened in the last 24 hours. The team is heavily focused on core robustness, shipping patches for background task notification resilience and data backup infrastructure, although the backup feature was briefly rolled back via a follow-up chore PR due to apparent stability concerns. On the community side, a single but deeply technical issue was raised concerning cross-model sub-task orchestration, pointing to a growing demand for more sophisticated multi-agent coordination. No new releases have been cut today, but the rapid merge cycle suggests a patch release may be imminent.

### 2. Releases
**None.**
No new releases have been tagged. The project appears to be in a rapid iteration phase accumulating fixes before the next stable cut.

### 3. Project Progress
Three pull requests were successfully merged in the last 24 hours, advancing both feature development and system reliability:

- **[#2136 — feature: data backup and migration](https://github.com/netease-youdao/LobsterAI/pull/2136)** (fisherdaddy)
  A significant feature entry covering the renderer, documentation, and main processes. This establishes a formal data backup and migration pipeline, a clear step towards enterprise-grade data persistence.
- **[#2135 — chore: temporary close databackup](https://github.com/netease-youdao/LobsterAI/pull/2135)** (fisherdaddy)
  Quickly merged immediately after the feature above. This suggests a blocking issue or unexpected behavior was identified in #2136, and the team acted swiftly to disable it pending a fix.
- **[#2134 — Liuzhq/task complete notice](https://github.com/netease-youdao/LobsterAI/pull/2134)** (liuzhq1986)
  A critical UX reliability patch. It ensures that LobsterAI can be properly restored from a closed/destroyed window state when a task completes, properly waits for the renderer notification handler to be ready, and retains active system notification references so that macOS Notification Center clicks remain actionable.

### 4. Community Hot Topics
The entire community discussion in the last 24 hours centers on a single, high-fidelity technical report:

- **[#2132 — 跨模型子任务调用的问题 (Cross-model sub-task invocation issue)](https://github.com/netease-youdao/LobsterAI/issues/2132)**
  *Author:* woxinsj | *Comments:* 0 | *Reactions:* 0

  Although it lacks comments or reactions yet, this issue is highly substantive. The author is attempting a sophisticated multi-agent workflow (M3 for planning and supervision, DeepSeek for execution) and discovered that gateway-level function calls are invisible to the main task (not found in `sessions_list` or `subagents`). The reporter provides a detailed root cause analysis and proposes a structured solution involving an explicit cross-model notification protocol. This signals a sophisticated user segment pushing the boundaries of the existing single-model sub-agent paradigm.

### 5. Bugs & Stability
- **High Severity — [Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132):** Cross-model sub-task tracking is broken. When a main task delegates to a different model at the gateway level, the orchestrator loses visibility of the sub-task's lifecycle. This is a deep architectural limitation affecting multi-LLM workflows. **No fix PR currently attached.**
- **Medium Severity — [PR #2133 (Open)](https://github.com/netease-youdao/LobsterAI/pull/2133):** `fix: fix export and code copy bugs` (fisherdaddy). This directly addresses user-facing functionality in the cowork and renderer areas. A fix is actively in progress.
- **Low/Chore — [PR #2135 (Merged)](https://github.com/netease-youdao/LobsterAI/pull/2135):** The `temporary close databackup` indicates a regression or unexpected failure in the newly merged backup feature (#2136). The team’s rapid rollback is a healthy sign of responsive maintenance.

### 6. Feature Requests & Roadmap Signals
- **Federated Multi-Agent Orchestration:** Issue [#2132](https://github.com/netease-youdao/LobsterAI/issues/2132) explicitly requests a formal protocol for cross-model sub-task awareness, including a "same-model vs. cross-model" distinction and an active notification bus for sub-tasks to report completion or blockages directly to the main task. This is the strongest signal for the next major feature cycle.
- **Headless & Background Operations:** The merged [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) confirms the team is investing heavily in making LobsterAI a reliable background agent, handling OS-level interruptions and renderer unavailability gracefully.
- **Data Resilience:** The data backup feature ([#2136](https://github.com/netease-youdao/LobsterAI/pull/2136)), despite its temporary rollback, proves this is an active roadmap item for upcoming releases.

### 7. User Feedback Summary
The predominant user sentiment comes from a single power user in **[Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132)**. The user exhibits high technical sophistication, having performed deep internal debugging to locate the root cause. They are clearly satisfied with the platform’s potential for multi-model work (M3 + DeepSeek) but express explicit dissatisfaction with the current lack of a deterministic inter-agent protocol. The underlying pain point is that complex, dynamic task routing across different models leads to silent failures and lost sub-tasks.

### 8. Backlog Watch
- **[Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132)** is the primary item requiring immediate maintainer attention. Despite being opened yesterday with a thorough analysis and proposed solution, it has received zero responses from the team. Given the complexity of the architectural change proposed and the potential impact on multi-agent reliability, a maintainer acknowledgement or technical direction is critical. No other older backlog items were updated in today's snapshot.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest: 2026-06-10**

---

### 1. Today's Overview
The Moltis project experienced a very low-activity day on June 10, 2026, with no new releases, no pull request activity, and only a single issue updated in the last 24 hours. This volume suggests the project is in a quiet maintenance phase or experiencing a typical low-traffic period. The only data point is a newly filed bug report regarding provider configuration, indicating that while development throughput is low, users are still actively engaging with the product. Overall project health remains stable, though prompt maintainer response to this new report will be critical to maintaining user confidence.

---

### 2. Releases
No new releases were published today. Users are currently operating on the latest previously published stable versions of Moltis.

---

### 3. Project Progress
No pull requests were merged, closed, or updated in the last 24 hours. No features, improvements, or bug fixes were integrated into the project codebase during this reporting period.

---

### 4. Community Hot Topics
Community discussion was effectively flat today. The single active issue ([Issue #1114](https://github.com/moltis-org/moltis/issues/1114)) was filed today and has yet to receive any comments or reactions. While the topic (provider configuration failure) could indicate a broader usability concern, the absence of engagement so far makes it difficult to gauge community-wide impact or sentiment from this data alone.

---

### 5. Bugs & Stability
A single bug was reported today:
- **Issue #1114 [Bug]: provider ‘coqui’ not configured (Minor)**
  - **Link:** [Issue #1114](https://github.com/moltis-org/moltis/issues/1114)
  - **Author:** vvuk
  - **Severity:** Minor (as labeled by the reporter)
  - **Analysis:** The user reports that the ‘coqui’ provider is not properly configured. They confirmed they searched existing issues and are on the latest version, suggesting a legitimate, potentially undocumented configuration gap or a recent regression. The issue template requests full session context, which has not yet been provided. No fix pull request currently exists for this issue.
  - **Recommendation:** Immediate triage is advised to determine if this is a documentation gap, a configuration parsing bug, or an environment-specific failure.

---

### 6. Feature Requests & Roadmap Signals
No new feature requests were submitted in the last 24 hours. User signals today were entirely focused on stability and configuration correctness rather than new capabilities. Future roadmap priorities remain unchanged based on this data.

---

### 7. User Feedback Summary
Direct user feedback today is limited to the report from user **vvuk** ([Issue #1114](https://github.com/moltis-org/moltis/issues/1114)). The core pain point involves difficulty configuring the ‘coqui’ TTS provider. The user exhibits a responsible reporting style (checked for duplicates, on latest version), implying they are an engaged user potentially encountering a blocker in their workflow. This highlights that multi-provider configuration reliability is a friction point in the user experience.

---

### 8. Backlog Watch
As the only active issue (Issue #1114) was opened today, it has not yet aged into a backlog concern. However, if it remains unaddressed for several days, it will become a prime candidate for watchlist escalation. No other long-standing unanswered issues or pull requests were identified in today’s snapshot, suggesting the maintainers have previously kept the backlog well-managed.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the CoPaw (QwenPaw framework) project digest for June 10, 2026, compiled from the latest GitHub activity.

---

### **1. Today's Overview**
The project is experiencing **high-velocity iteration** this week, with 42 issues and 38 PRs updated, alongside a new beta release. Community engagement is strong, with users actively comparing the project against rising competitors like Hermes Agent and demanding advanced "learning loop" features. The backend is being prepared for a major architectural shift to **AgentScope 2.0**, while a steady stream of bug-fix PRs from both core team and first-time contributors is addressing accumulated technical debt, particularly around MCP subprocess management and skill pool organization. Desktop performance remains the largest source of user friction.

---

### **2. Releases**
- **Version:** `1.1.11-beta.2`
- **Changes:**
  - `feat(browser)`: Added page coordinate click support to `browser_control` ([PR #4905](https://github.com/agentscope-ai/QwenPaw/pull/4905)).
  - `fix(browser)`: Added CDP timeout parameter and implemented browser profile isolation for cross-browser switching ([PR by x1n95c](https://github.com/agentscope-ai/QwenPaw/issues?q=is%3Apr+author%3Ax1n95c)).
- **Analysis:** This is a targeted stability release. The browser isolation fix directly addresses a reliability issue in multi-tab/hybrid RPA scenarios, while the coordinate-click support expands the automation capabilities of the browser agent.
- **No breaking changes or specific migration notes** are attached to this release.

---

### **3. Project Progress**
Maintainers merged/closed **18 PRs** in the last 24 hours. The top landed items by impact include:

- **Plugin & Agent Ecosystem Progress:**
  - [#5033](https://github.com/agentscope-ai/QwenPaw/pull/5033) (merged): Feature plugin for CloudPaw, enabling agent import from AgentHub and enhanced A2A capabilities.
- **Stability & Bug Fixes:**
  - [#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014) (merged): Fix for MCP server subprocess accumulation across Docker restarts. Addresses a high-severity issue where old MCP processes would survive restarts.
  - [#5062](https://github.com/agentscope-ai/QwenPaw/pull/5062) (merged): Fix for E2E token usage test failing in clean environments.
  - [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) (closed): Fix for PAT tool naming conflicts with DeepSeek API (Dots `.` replaced to comply with regex restrictions).
- **Skill System:**
  - [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) (merged): Added skill tag batch download, resolving a long-standing feature request for skill pool organization.
- **Security:**
  - [#4981](https://github.com/agentscope-ai/QwenPaw/pull/4981) (Under Review): File preview endpoint now restricted to `WORKING_DIR` with a sensitive-path deny list.
- **First-Time Contributors:**
  - `ly-wang19` is actively submitting several high-quality fixes for edge-case parsing errors (config, browser detection, backups), a strong indicator of community health.

---

### **4. Community Hot Topics**
The most active discussions reflect a community that is technically sophisticated and deeply concerned with the project's competitive trajectory.

- **Evangelizing "Learning Loops" ([#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017)):**
  - *Activity:* 10 comments, 3 👍.
  - *Discussion:* Users are strongly advocating for the project to adopt design patterns from **Hermes Agent** (46k+ Stars). The core demand is for autonomous skill creation and iteration. The community sees this as the critical differentiator to avoid falling behind.
- **AgentScope 2.0 Migration ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)):**
  - *Activity:* 7 comments, 2 👍.
  - *Discussion:* This open Breaking Change issue is a major roadmap signal. Users are closely monitoring the migration plan, which promises a new architecture but implies significant API disruption for plugin and channel developers.
- **Desktop Performance Crisis ([#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015), [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047), [#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917)):**
  - *Activity:* Multiple threads, high consensus.
  - *Pain Point:* The switch to Tauri has caused severe startup delays (up to 15 minutes reported) and UI jank during session switching. This is generating the most negative user sentiment in the current batch.
- **DingTalk Empty Cards ([#5057](https://github.com/agentscope-ai/QwenPaw/issues/5057)):**
  - *Activity:* 2 comments.
  - *Details:* When agents return empty strings, DingTalk receives a "Processing..." card. A fix is proposed in [#5061](https://github.com/agentscope-ai/QwenPaw/pull/5061).

---

### **5. Bugs & Stability**
Bug activity is high. Several regressions from recent releases are being actively patched.

**Critical / High Severity:**
- **[OPEN] [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989):** Qwen 3.6-27B (local vLLM deployment) is unresponsive in v1.1.9 and v1.1.10 (regression from v1.1.5). Fix is still pending.
- **[OPEN] [#5052](https://github.com/agentscope-ai/QwenPaw/issues/5052):** Tool calls fail after several rounds with `got an unexpected keyword argument 'arguments'`. This breaks complex agent chains after the first few turns.
- **[OPEN] [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064):** Agent-created cron jobs do not trigger and cannot be manually edited.
- **[OPEN] [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031):** Skill slash commands (e.g. `/pdf`) display raw `SKILL.md` markdown instead of executing the skill.

**Medium Severity:**
- **Desktop Performance:** Slow startup, high CPU, session history rendering lag ([#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015)), Tauri startup time ([#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047)), chat data rendering stalls ([#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917)).
- **[OPEN] [#5057](https://github.com/agentscope-ai/QwenPaw/issues/5057):** DingTalk AI Card sends empty "Processing..." content. Fix in [#5061](https://github.com/agentscope-ai/QwenPaw/pull/5061).

**Recently Resolved:**
- WeChat cron job push failure ([#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878) / [#5060](https://github.com/agentscope-ai/QwenPaw/issues/5060)) – **Merged**.
- MCP process accumulation across restarts ([#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)) – **Merged** via [#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014).
- `/compact` command ignoring model `max_input_length` ([#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937)) – **Merged**.

---

### **6. Feature Requests & Roadmap Signals**
Several requests indicate strong community demand for agent sophistication and architectural maturity.

- **Top Voted / Discussed Feature Requests:**
  - **Self-Evolving Memory ([#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994)):** Users want a layered, self-evolving memory system to compete with mainstream agent frameworks.
  - **Visual Model Fallback ([#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992)):** A request to configure a separate vision model to handle images when the main LLM (e.g., DeepSeek V4) is text-only. High demand for multimodal flexibility.
  - **OpenSandbox Support ([#4951](https://github.com/agentscope-ai/QwenPaw/issues/4951)):** Request for isolated runtime for untrusted code execution.

- **Predictions for Next Release (v1.2.x):**
  - **Skill & Plugin Infrastructure:** The multi-path skill pool ([PR #4891](https://github.com/agentscope-ai/QwenPaw/pull/4891)) and the frontend plugin extension ([PR #4997](https://github.com/agentscope-ai/QwenPaw/issues/4997)) are maturing rapidly and are likely candidates for the next minor release.
  - **AgentScope 2.0 ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)):** This will likely define the roadmap for the coming months, requiring significant coordination with channel and plugin owners.
  - **Desktop Experience:** The Tauri auto-updater ([PR #4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)) and System Tray feature ([#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751)) are waiting in the backlog for a quality-of-life push.

---

### **7. User Feedback Summary**
- **Satisfaction Drivers:** Users appreciate the local-first deployment, the breadth of channel integration (WeChat, DingTalk, Discord), and the flexible skill system. The move towards a plugin ecosystem is well-received.
- **Major Pain Points:**
  - **Desktop Client Performance:** The Tauri migration has caused significant regression in startup speed and general UI fluidity on Windows. This is the most vocal complaint currently.
  - **Regression Instability:** The community has low tolerance for regression bugs between minor versions, specifically citing the Qwen 3.6 model issue ([#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989)).
  - **Integration Fragility:** Cron jobs, WeChat delivery, and MCP processes are perceived as powerful when working but brittle, requiring frequent manual restarts.
- **Competitive Landscape:** Users are explicitly comparing QwenPaw to Hermes Agent and OpenClaw. The community is demanding "learning loop" features to keep the project relevant, suggesting they fear stagnation in agent self-improvement capabilities.

---

### **8. Backlog Watch**
Several important issues and PRs have been idle or awaiting maintainer action.

- **[#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) – AgentScope Tracing Init (Question):** Open since May 6th. A request for a standardized initialization hook for `agentscope.init()` (e.g., Arize Phoenix tracing). Relatively low effort but high value for observability.
- **[#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751) – Windows System Tray (Feature):** Open since April 23rd. A core UX feature for desktop parity with commercial products that has seen no recent maintainer activity.
- **[#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669) – Tauri Auto-Updater (PR):** Open since May 25th. This is a significant PR that directly addresses one of the biggest user complaints (desktop distribution). It is currently not merged and is a critical quality-of-life blocker.
- **[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) – AgentScope 2.0 Migration:** While very active, the sheer scope of this change means it requires immense maintainer bandwidth. Community silence on the technical discussion thread may indicate a bottleneck in decision-making.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw Project Digest — 2026-06-10

---

### 1. Today's Overview

ZeroClaw saw extremely high development velocity on June 10, 2026, with **50 issues** and **50 PRs** updated within the last 24 hours. The project remains in aggressive development mode, prioritizing bug fixes for core runtime stability (memory, cron, context limits, tool execution) while simultaneously landing major feature work across infrastructure and observability. No new releases were cut today, but the high volume of actionable PRs (48 open, 2 merged/closed) and issue resolution strongly signals an imminent patch or minor release cycle targeting the regressions exposed in the v0.8.0-beta-1 cycle. Community engagement is robust, with contributors actively submitting patches alongside bug reports, demonstrating a mature open-source maintainer-contributor feedback loop.

---

### 2. Releases

**No new releases today.** The last published release remains **v0.8.0-beta-1**, which is tied to several newly filed bugs (notably the web dashboard JSON parse crash [[#6862]](https://github.com/zeroclaw-labs/zeroclaw/issues/6862) and the MCP tool restriction gap [[#6876]](https://github.com/zeroclaw-labs/zeroclaw/issues/6876)). Given the volume of critical fixes now in review—context budget trims [[#7440]](https://github.com/zeroclaw-labs/zeroclaw/pull/7440), cron overrun prevention [[#7348]](https://github.com/zeroclaw-labs/zeroclaw/pull/7348), parallel sub-agent reliability [[#7442]](https://github.com/zeroclaw-labs/zeroclaw/pull/7442)—an early patch (v0.8.0-beta-2 or v0.8.0 stable) appears imminent.

---

### 3. Project Progress

Two issues were closed today, and one significant PR was merged:

- **Logo Feature** [[#4710]](https://github.com/zeroclaw-labs/zeroclaw/issues/4710) (20 comments, closed): After a lengthy community discussion, the project landed a new logo, resolving a long-standing cosmetic enhancement request.
- **Config UX Parity** [[#7117]](https://github.com/zeroclaw-labs/zeroclaw/issues/7117) (closed): This cross-surface initiative brought CLI, Quickstart, zerocode, and web configuration interfaces to a unified, reference-grade bar.
- **AMQP/SOP Channel** [[#7369]](https://github.com/zeroclaw-labs/zeroclaw/pull/7369) (size XL, closed/merged): A major infrastructure feature was landed—AMQP inbound channels with mutual TLS for deterministic SOP runs—unlocking an end-to-end enterprise automation pipeline.

Multiple PRs advanced towards closing core technical debt:
- **Provider reasoning field preservation** [[#7423]](https://github.com/zeroclaw-labs/zeroclaw/pull/7423) fixes a multi-turn replay regression for OpenRouter/vLLM compatibility.
- **Azure `reasoning_effort`** [[#7350]](https://github.com/zeroclaw-labs/zeroclaw/pull/7350) wires dedicated support for GPT-5.x/o-series models.
- **Matrix thread anchoring** [[#7349]](https://github.com/zeroclaw-labs/zeroclaw/pull/7349) fixes self-referencing interruption scopes.
- **Code-owner governance** [[#7443]](https://github.com/zeroclaw-labs/zeroclaw/pull/7443) updates CODEOWNERS to reflect current maintainer responsibilities.

---

### 4. Community Hot Topics

The community is deeply engaged in the tension between feature ambition and production stability. The most active threads reveal systemic pain points:

| Issue | Comments | Theme |
|---|---|---|
| **Better Logo** [[#4710]](https://github.com/zeroclaw-labs/zeroclaw/issues/4710) | 20 (closed) | Brand identity / community engagement |
| **Agent ignores cron tool** [[#5862]](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | 12 | Agent self-awareness / tool discovery |
| **Providers architecture refactor** [[#5937]](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | 10 | Core tech debt / maintainability |
| **Per-sender RBAC** [[#5982]](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | 9 | Enterprise multi-tenancy |
| **Discord channel restrictions** [[#6378]](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) | 7 | Channel granularity / parity |
| **Memory over-emphasis** [[#5844]](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | 6 | Agent behavior / prompt priority |
| **Webhook tool_search hang** [[#6721]](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) | 4 | Non-interactive workflow blocker |
| **Default context budget overflow** [[#5808]](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | 3 | Architectural scaling limit |

The memory system is a recurring point of dissatisfaction—users consistently report the agent over-indexes on stored memories at the expense of current instructions [[#5844]](https://github.com/zeroclaw-labs/zeroclaw/issues/5844). The lack of multitenancy guards (RBAC [[#5982]](https://github.com/zeroclaw-labs/zeroclaw/issues/5982)) and granular channel controls (Discord [[#6378]](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)) signals growing enterprise deployment pain. The most technically disruptive discussion is the context budget bug [[#5808]](https://github.com/zeroclaw-labs/zeroclaw/issues/5808), where system prompt + tool definitions exceed the default 32k budget by ~3.3x on the very first turn, effectively breaking many default configurations.

---

### 5. Bugs & Stability

Stability is today's dominant theme. **Critical (P1/S1) bugs** pepper the report, with corresponding fix PRs in active review:

| Bug | Component | Severity | Fix PR |
|---|---|---|---|
| **Context budget overflow** [[#5808]](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | Runtime | S1 - workflow blocked | [[#7440]](https://github.com/zeroclaw-labs/zeroclaw/pull/7440) (skip futile trim) |
| **User message loss (multi-turn)** [[#6034]](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | Provider/Runtime | S1 - workflow blocked | None yet |
| **Webhook tool_search hang** [[#6721]](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) | Tool/MCP | S1 - workflow blocked | None yet |
| **Telegram search tools blocked** [[#6646]](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | Channel/Telegram | S1 - workflow blocked | None yet |
| **Cron job repeated launches** [[#6037]](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) | Cron | P1 - in progress | [[#7348]](https://github.com/zeroclaw-labs/zeroclaw/pull/7348) (startup skip) |
| **Duplicate SopEngine instances** [[#6687]](https://github.com/zeroclaw-labs/zeroclaw/issues/6687) | SOP/Runtime | P1 | None yet |
| **Memory over-emphasis** [[#5844]](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | Memory | S2 - degraded behavior | None yet |

Additional TUI bugs filed today affect zerocode on macOS: **Cmd-C misidentified as quit chord** [[#7378]](https://github.com/zeroclaw-labs/zeroclaw/issues/7378), **dark theme unreadable on light terminals** [[#7377]](https://github.com/zeroclaw-labs/zeroclaw/issues/7377), and **loading/error states hidden by the dashboard** [[#7376]](https://github.com/zeroclaw-labs/zeroclaw/issues/7376) (fix in review [[#7444]](https://github.com/zeroclaw-labs/zeroclaw/pull/7444)). A **web console config loading failure** [[#7253]](https://github.com/zeroclaw-labs/zeroclaw/issues/7253) was also reported.

---

### 6. Feature Requests & Roadmap Signals

Enterprise hardening and ecosystem expansion are the clearest roadmap signals from today's data:

- **Core Refactoring:** The complete **providers/reqwest architecture unification** [[#5937]](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) is the single most impactful structural enhancement in flight, promising to consolidate fragmented model construction and client management.
- **Multi-Tenancy & Security:** **Per-sender RBAC** [[#5982]](https://github.com/zeroclaw-labs/zeroclaw/issues/5982), **per-skill security permissions** [[#5775]](https://github.com/zeroclaw-labs/zeroclaw/issues/5775), and **route-layer auth middleware** [[#6250]](https://github.com/zeroclaw-labs/zeroclaw/issues/6250) all point to a deliberate push toward production-grade deployments.
- **Tool Execution Safety:** **Process memory limits on subprocesses** [[#6916]](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) and **Composio action-scope filters** [[#6917]](https://github.com/zeroclaw-labs/zeroclaw/issues/6917) address container OOM risks and cross-tenant isolation.
- **Ecosystem Growth:** The push for **`.well-known` skill URIs** [[#4853]](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) suggests a planned skill ecosystem marketplace, aligning with Cloudflare and Vercel adoption.
- **Cost Visibility:** **Persisting cached input tokens for cost accounting** [[#7248]](https://github.com/zeroclaw-labs/zeroclaw/issues/7248) will fill a significant blind spot for users on token-based billing models.

*Likely next-release candidates:* The context budget trim fix [[#7440]](https://github.com/zeroclaw-labs/zeroclaw/pull/7440), cron startup fix [[#7348]](https://github.com/zeroclaw-labs/zeroclaw/pull/7348), sub-agent reliability [[#7442]](https://github.com/zeroclaw-labs/zeroclaw/pull/7442), and Azure reasoning effort [[#7350]](https://github.com/zeroclaw-labs/zeroclaw/pull/7350) are all polished and ready for a patch release.

---

### 7. User Feedback Summary

Frustration and investment coexist in today's user feedback. The dominant pain points fall into two categories:

**Agent Cognitive Behavior:**
- The agent **over-prioritizes stored memories** over current system instructions, especially in cron jobs [[#5844]](https://github.com/zeroclaw-labs/zeroclaw/issues/5844).
- The agent **lacks self-awareness of its own tools**, notably failing to suggest `zeroclaw cron` when asked for recurring tasks [[#5862]](https://github.com/zeroclaw-labs/zeroclaw/issues/5862).

**Frontend & TUI Usability:**
- The **zerocode TUI** on macOS has multiple platform-specific defects: Cmd-C triggers quit instead of copy [[#7378]](https://github.com/zeroclaw-labs/zeroclaw/issues/7378), dark themes are illegible on light terminal profiles [[#7377]](https://github.com/zeroclaw-labs/zeroclaw/issues/7377), and the dashboard hides useful error states [[#7376]](https://github.com/zeroclaw-labs/zeroclaw/issues/7376).
- The **web dashboard is effectively broken** for configuration management, failing with JSON parse errors [[#7253]](https://github.com/zeroclaw-labs/zeroclaw/issues/7253).
- **Locale switching appears inoperative** until immediate restart [[#7400]](https://github.com/zeroclaw-labs/zeroclaw/issues/7400).

Despite this, the community is **highly engaged in contributing fixes**, filing detailed bug reports with severity ratings, and participating actively in design discussions (e.g., RBAC, MCP authorization). This signals a strong, technically sophisticated user base that is willing to invest in the project's maturity.

---

### 8. Backlog Watch

Several critical items risk lingering in review or blocked state and require maintainer attention:

| Issue | Age | Status | Risk |
|---|---|---|---|
| **Per-sender RBAC** [[#5982]](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | Since Apr 22 | `needs-author-action, blocked` | High — blocks multi-tenant production deployments |
| **Composio action-scope filter** [[#6917]](https://github.com/zeroclaw-labs/zeroclaw/issues/6917) | Since May 25 | `needs-author-action, blocked` | High — security boundary gap |
| **Webhook tool_search hang** [[#6721]](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) | Since May 16 | P1, Accepted, no-fix-in-hand | Critical — blocks non-interactive workflows |
| **SopEngine duplication** [[#6687]](https://github.com/zeroclaw-labs/zeroclaw/issues/6687) | Since May 15 | P1, Accepted | Critical — state corruption |
| **MCP tool restriction gap** [[#6876]](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) | Since May 23 | Accepted | Medium — documentation/design decision needed |
| **Quickstart port field** [[#7215]](https://github.com/zeroclaw-labs/zeroclaw/pull/7215) | Since Jun 4 | `needs-author-action` | Low — blocks clean webhook onboarding |
| **`.well-known` skills** [[#4853]](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) | Since Mar 27 | Accepted | Medium — ecosystem competitive necessity |

The `needs-author-action` pile (RBAC, Composio, Quickstart) represents features submitted by external contributors that require maintainer review to unblock. The P1 bugs (tool_search hang, SopEngine duplication) are open with no associated fix PR and should be prioritized for assignment in the next sprint.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*