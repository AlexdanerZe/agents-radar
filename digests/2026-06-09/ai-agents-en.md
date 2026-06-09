# OpenClaw Ecosystem Digest 2026-06-09

> Issues: 500 | PRs: 473 | Projects covered: 13 | Generated: 2026-06-09 02:49 UTC

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

Here is the structured OpenClaw project digest for **2026-06-09**, based on the provided GitHub data.

---

## OpenClaw Project Digest — 2026-06-09

### 1. Today’s Overview

OpenClaw is in a period of very high activity, with **500 issues** and **473 pull requests** updated in the last 24 hours, accompanied by two new beta releases. However, the data reveals a project under significant maintenance strain: a high volume of open items (435 issues, 329 PRs) persists, and critical “stale” bugs with no fix PRs suggest a bottleneck in maintainer bandwidth or product decision-making. The most intense community focus right now is split between **urgent compatibility regressions** (GPT-5.x transport failures, Node 23 SQLite crashes) and **deep ecosystem frustration** (the ClawHub skill marketplace). While impactful bugs are being closed, the sheer volume of regressions indicates that velocity is currently outpacing stability.

### 2. Releases

**New Versions:** `v2026.6.5-beta.3` and `v2026.6.5-beta.5`

Both releases share identical highlighted changes, indicating this is a hotfix chain:
- **Security/UX Fix:** QQBot now strips raw `<thinking>` model reasoning scaffolding before native delivery. This prevents internal cognitive traces from leaking into public channel replies. (#89913, #90132) – Thanks @openperf.
- **MCP Robustness:** Tool results handling is hardened to coerce `resource_link`, `resource`, `audio`, and malformed image types, preventing delivery failures for MCP tools returning unexpected payloads.

**Recommendation:** No breaking changes or specific migration steps noted. These are safe rolling patches for users on the beta channel.

### 3. Project Progress

Several significant items moved from open to closed today:

- **Node.js Compatibility:** PR #90035 ([Link](openclaw/openclaw PR #90035)) closed. Fixes a critical crash on Node 23.0–23.10 where `StatementSync.columns()` was missing, breaking migrations and plugins.
- **Configuration Safety:** PR #91551 ([Link](openclaw/openclaw PR #91551)) closed. Introduces an explicit `replacePaths` contract for destructive `config.patch` array replacement, preventing accidental data loss during config updates.
- **Data Integrity:** PR #90856 ([Link](openclaw/openclaw PR #90856)) closed. Solves a major bug where persisted transcripts contained corrupted image payloads after redaction, causing provider 422 errors on every subsequent turn.
- **UI Polish:** PR #87474 ([Link](openclaw/openclaw PR #87474)) closed. Fixes a false "In progress" state in the Control UI webchat that left users unable to send new messages after a response completed.
- **Channels:** Bugs causing streaming text loss on Telegram (#87326), card truncation on Feishu (#88929), and SQLite vector search breaks on ARM (#65156) were all closed with fixes.

### 4. Community Hot Topics

The following issues and PRs generated the most engagement (by comments) today, revealing deep user needs:

- **#90083 — GPT-5.x Transport Failure (15 comments)**
  [Link](openclaw/openclaw Issue #90083)
  An immediate blocker for early adopters. Upgrading to `2026.6.1` with `gpt-5.4`/`gpt-5.5` models causes a `invalid_provider_content_type` error. No fix PR exists yet. **Underlying Need:** Bleeding-edge model support must be tested before release to avoid alienating power users.

- **#50090 — ClawHub Ecosystem Dissatisfaction (15 comments)**
  [Link](openclaw/openclaw Issue #50090)
  A direct call-out: “The gap between promise and practice is wide.” Users feel the skill marketplace is immature, with problems ranging from discovery to quality control. **Underlying Need:** The community desperately wants OpenClaw to fulfill its vision as a platform, not just a single-agent tool.

- **#48788 — Centralized Filename Encoding (18 comments)**
  [Link](openclaw/openclaw Issue #48788)
  A long-standing architectural request to handle multiple encodings (Shift-JIS, EUC-KR) for Content-Disposition across all channels. **Underlying Need:** Global users need the platform to handle their native languages correctly without per-channel hacks.

- **#32473 — Control UI HTTPS Requirement (17 comments, 4 👍)**
  [Link](openclaw/openclaw Issue #32473)
  Users on VPS/Docker setups without proper HTTPS are locked out of the Control UI. The tone suggests frustration that this isn’t resolved. **Underlying Need:** Simpler, managed deployment workflows that don't require deep TLS expertise.

### 5. Bugs & Stability

The stability signal is mixed. High-severity regressions are being fixed, but several P1-level bugs remain open with no forward motion.

| Severity | Issue | Summary | Status |
|---|---|---|---|
| **Critical** | #90083 | GPT-5.4/5.5 Responses transport fails (invalid_provider_content_type) | OPEN, No Fix PR |
| **Critical** | #32296 | Agent replies to previous message (session context confusion) | OPEN, Stale (P1) |
| **High (Regressed)** | #48003 | Steer mode does not inject messages mid-turn for main sessions | OPEN, Stale (P1) |
| **High (Security)** | #44905 | Discord leaks internal LLM tool-call traces (NO_REPLY, raw JSON) | OPEN, Stale (P1) |
| **High (Security)** | #45740 | `gh-issues` skill injects untrusted issue bodies into sub-agent prompts | OPEN, Stale (P2) |
| **Medium** | #88929 | Feishu streaming card truncates content to last character | **CLOSED (Fixed)** |
| **Medium** | #87326 | Telegram intermediate text blocks silently lost between tool calls | **CLOSED (Fixed)** |

**Key takeaway:** The project is effectively closing bugs found in specific channels (Telegram, Feishu) and runtime environments (Node 23), but **core session logic bugs** (#32296, #48003) and **security boundary leaks** (#44905) are lingering without fixes, presenting a serious reliability risk.

### 6. Feature Requests & Roadmap Signals

The data suggests the following features are bubbling up as high community priorities and are likely candidates for upcoming releases:

- **ClawHub & Skill Ecosystem Maturity:** Multiple issues (#50090, #43260, #45031) demand a better skill marketplace with security scanning and per-skill model routing. This is the single loudest roadmap signal.
- **Session & Observability Control:**
  - #42475: Per-agent cost budget enforcement at the gateway.
  - #45565: Route lifecycle warnings to a dedicated health channel.
  - #50291: Missing trace context (`messageId`, `runId`) in plugin hooks for distributed tracing.
- **QoL Improvements:**
  - #42840: MathJax/LaTeX rendering in Control UI (High 👍 count).
  - #45758: YAML config file support.
  - #91557 & #91543: Major iPad/iPhone control surface improvements and collapsible workspace rail (PRs in progress).
- **Prediction:** The **next minor version** will likely prioritize the ACP Hub delegated sessions architecture (PR #91093) and ClawHub improvements to solve the growing capacity and ecosystem pain points.

### 7. User Feedback Summary

**Satisfaction Drivers:**
- **Velocity:** Users appreciate the rapid release cycle and the fact that specific channel bugs (Telegram, Feishu, Discord) are being tackled aggressively.
- **Feature Innovation:** Large PRs for ACP sessions and Apple device control surfaces generate positive sentiment.

**Dissatisfaction Drivers:**
- **Regression Fatigue:** Users report that upgrades frequently break existing workflows. Common complaints on the top issues include “memory is in chaos” (#43747) and a lack of consistency across user installations.
- **Trust Concerns:** The discovery of hardcoded workspace paths (#51429: “Hardcode into the code and merged”) and the leaking of internal tool traces (#44905) have shaken user trust in code review and QA processes.
- **Ecosystem Stalling:** The sentiment around ClawHub (#50090) is notably frustrated. Users feel the "promise of a living ecosystem" is not materializing, which could cap long-term community growth.

### 8. Backlog Watch

The following high-importance items are "stale" or awaiting key maintainer decisions. Their age is a risk to project health:

- **#32473 — Control UI HTTPS Requirement (P2, Security, Stale)**
  [Link](openclaw/openclaw Issue #32473)
  Blocking non-HTTPS deployment. Impact: High. Needs a product decision on authentication fallback.

- **#32296 — Agent Replies to Previous Message (P1, Stale)**
  [Link](openclaw/openclaw Issue #32296)
  Core conversational context bug open since March. Impact: Critical for UX.

- **#43367 — Multi-agent Orchestration Instability (P1, Stale)**
  [Link](openclaw/openclaw Issue #43367)
  Concurrent agent config overwrites and session lock failures. Impact: High for power users scaling their setups.

- **#50090 — ClawHub Ecosystem (P2, Stale)**
  [Link](openclaw/openclaw Issue #50090)
  The most important community-building feature is stuck in discussion stage.

- **#45740 — Gh-issues Skill Injection (P2, Security, Stale)**
  [Link](openclaw/openclaw Issue #45740)
  Untrusted data is injected into sub-agent prompts without sanitization. Risk: High. Needs a security review verdict.

**Maintainer Attention Required:** The concentration of P1 bugs and security issues in the "stale" zone suggests the project may need to declare a **stability sprint** to clear this backlog before adding further feature surface area.

---

## Cross-Ecosystem Comparison

**Cross-Project Comparison Report: AI Agent Open-Source Ecosystem**
**Date:** 2026-06-09 | **Scope:** Personal AI Assistant / Agent Projects

---

### 1. Ecosystem Overview
The personal AI agent landscape is sharply bifurcated. Established platform projects (OpenClaw) are wrestling with scaling maintainer capacity and architectural debt, while a wave of challengers (ZeroClaw, CoPaw, IronClaw) are shipping significant architectural rewrites and platform features at high velocity. Across every active project, the conversation has shifted from raw capability to **trustworthy reliability** — security hardening (SSRF blocking, egress lockdown, context isolation) and multi-agent orchestration stability dominate the bug tracker data. This snapshot reflects an industry rapidly maturing past demos, with the tax of production deployment (channel fragility, desktop regressions, provider compatibility) consuming the majority of engineering effort.

---

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | PRs Merged/Closed | Release Status | Activity Tier | Key Signal |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 473 | Medium | Beta chain | Extreme / Strained | High volume, stale P1 bugs, ecosystem frustration |
| **CoPaw** | 38 | 41 | High (22) | None | Hyper-Growth | Plugin infra, ACP, strong China-market velocity |
| **ZeroClaw** | 50 | 50 | Low (11) | Planned (v0.9.0) | Hyper-Growth | Security RFCs, S0 OOM bug unresolved, high ambition |
| **IronClaw** | 34 | 50 | High (25) | Pending (v0.29.1) | Hyper-Growth | Reborn architecture, API parity focus |
| **NanoBot** | 0 | 36 | High (16) | None | Very High | Agent collaboration bus, transcription standardization |
| **Hermes** | 50 | 50 | Low (4) | None | Very High | Desktop regressions, context safety, cost tracking |
| **LobsterAI** | 0 | 17 | Very High (16) | None | High | Data migration, auth revamp, stale Dependabot risk |
| **PicoClaw** | 3 | 19 | High (9) | Nightly | High | Code quality overhaul, DeltaChat gateway |
| **NanoClaw** | 1 | 3 | Medium (2) | None | Moderate | Egress lockdown merged, WhatsApp media broken |
| **TinyClaw** | 0 | 1 | None | None | Low | Single install-fix PR, effectively stalled |
| **NullClaw / Moltis / ZeptoClaw** | 0 | 0 | None | None | Inactive | No development signal |

---

### 3. OpenClaw’s Position

**Advantages vs. Peers:**
- Largest absolute community surface area (500 issues, 473 PRs) and most mature release pipeline (hotfix beta chain).
- Unmatched breadth of channel and provider support (Telegram, Feishu, Discord, GPT-5.x, ACP Hub).
- Ecosystem play (ClawHub) gives it a first-mover narrative on skill marketplaces, despite execution struggles.

**Technical Approach Differences:**
- OpenClaw is a **monolithic platform** aiming to standardize everything under one roof (ACP, ClawHub, Shared Sessions). Peers like NanoBot and ZeroClaw favor **modular, composable architectures** (message buses, pluggable security backends).
- The community is experiencing **regression fatigue** — critical bugs in core session logic (#32296) and security boundary leaks (#44905) remain open for weeks, unlike the rapid hotfix cycles seen in NanoBot or IronClaw.
- Openclaw is the only project where *user trust in ecosystem quality* (#50090) is a top comment thread, indicating a maturity gap between its promises and delivery.

---

### 4. Shared Technical Focus Areas

| Focus Area | Affected Projects | Common Requirements |
|---|---|---|
| **Multi-Agent Safety** | OpenClaw, NanoBot, Hermes, ZeroClaw, CoPaw, IronClaw | Context corruption fixes (`delegate_task`, `session_id` collisions), subagent lifecycle isolation, message idempotency |
| **Provider Fragility** | OpenClaw, Hermes, ZeroClaw, IronClaw, NanoBot | GPT-5.x transport failures, Gemini history ordering, DeepSeek duplicate fields, `extra_query` for custom gateways |
| **Security Boundaries** | OpenClaw, NanoBot, ZeroClaw, NanoClaw, Hermes, IronClaw | SSRF, symlink escapes, egress lockdown, OIDC integration, shell command policy engines, credential leak prevention |
| **Channel Reliability** | OpenClaw, CoPaw, ZeroClaw, PicoClaw, NanoClaw | WeChat token expiry / duplicate replies, Matrix session isolation, Telegram message splitting, WhatsApp media ingestion |
| **Desktop UX Buildout** | OpenClaw, Hermes, CoPaw, LobsterAI | Electron auth callbacks, terminal panes, file browsers, theme flash fixes, iPad collapsible rails |

---

### 5. Differentiation Analysis

| Project | Core Identity | Target User / Use Case | Architecture |
|---|---|---|---|
| **OpenClaw** | The Platform Standard | Community power users, ecosystem builders | Monolithic, ACP Hub, ClawHub marketplace |
| **ZeroClaw** | The Security Agent | Enterprise admins, automation engineers | Pluggable backends (Security, Auth), MCP-first, OIDC |
| **CoPaw (QwenPaw)** | The China-Native Agent | Chinese-market individuals & enterprises | Deep WeChat/DingTalk integration, Plugin Market, Learning Loops |
| **IronClaw** | The Scalable Backend | API-first integrators, parallel agent ops | "Reborn" rewrite for OpenAI API parity, SSE streaming, idempotency |
| **NanoBot** | The Infrastructure Bus | Developers building agent systems | Modular bus, highest transcription velocity, Agent Collaboration infra |
| **Hermes** | The Developer IDE | Coders, desktop-heavy workflows | Desktop terminal/file browser, cost tracking, Slack/Telegram codespace |
| **LobsterAI** | The Desktop Portal | Electron desktop users, data-conscious admins | Electron auth, backup/restore, dynamic provider model fetching |
| **PicoClaw** | The Embedded Go Agent | Niche platforms (RISC-V), legacy stability | Go-based, linting/error-wrapping focus, DeltaChat gateway |

---

### 6. Community Momentum & Maturity

**Tier 1 — Hyper-Growth (High Bugs, High Architectural Ambition)**
- **ZeroClaw, CoPaw, IronClaw.** Taking the biggest swings (pluggable security, plugin markets, full architecture rewrites). Bug density is high, but contributor enthusiasm and PR velocity are unmatched. These projects are defining the next architectural tier.

**Tier 2 — Established Iteration (Large Community, Stabilizing)**
- **OpenClaw, Hermes, NanoBot.** Large, established user bases. The conversation is dominated by regression fixes, maintainer bandwidth limits, and security hardening. These are the most "production-ready" but carry the most technical debt.

**Tier 3 — Niche Hardening (Low Volume, High Code Quality)**
- **LobsterAI, PicoClaw, NanoClaw.** Smaller, focused development teams. Clean PR hygiene, targeted feature additions, and dedicated security hardening. Ideal for specific use cases (desktop portal, Go deployments, high-security needs).

**Tier 4 — Dormant**
- **TinyClaw, NullClaw, Moltis, ZeptoClaw.** No development activity. Viable codebases but no current community momentum. Risk of bit rot.

---

### 7. Trend Signals

**1. The End of Binary Safety**
Projects are actively moving away from simple `allow/deny` gates toward rich, declarative policy engines. ZeroClaw’s shell confirmation tiers, Hermes’ Declarative Skill Protection Policy, and the universal push for OIDC and SSRF hardening indicate that the next competitive moat will be **trust infrastructure**, not raw capability.

**2. Self-Hosting is the De Facto Standard**
The volume of Docker, macOS Launchd, Windows Service, and WSL2-specific patches across every major project confirms that deployment is overwhelmingly on-premise. "Agent as a Service" (OpenClaw ACP Hub, IronClaw Reborn) remains largely aspirational.

**3. Multi-Agent is Still Fragile**
Context corruption (`delegate_task` singleton bugs, `session_id` collisions, `trim_history` cascades) is the single most recurring technical failure mode across OpenClaw, NanoBot, Hermes, ZeroClaw, and CoPaw. The industry has strong opinions about orchestration but lacks reliable low-level primitives—this remains a **Trough of Disillusionment** area for developers.

**4. Multi-Modal Integration is a Universal Bottleneck**
WhatsApp media ingestion (NanoClaw), image compression loops (CoPaw), and transcript transcription overhauls (NanoBot) confirm that text-only agents are no longer sufficient, but robust multi-modal pipelines are still an expensive engineering burden for every project.

**5. The Chinese Market is Building Independently**
CoPaw’s depth of WeChat/DingTalk support, the number of China-specific channel bugs across OpenClaw and ZeroClaw, and the localized i18n PRs (Indonesian, Chinese) signal that this ecosystem is diverging from the Western LLM-centric stack. Developers targeting this market must invest in channel-first architecture.

**6. Maintainer Capacity is the Hidden Variable**
OpenClaw’s gap between community volume and structural fix velocity is a cautionary tale. Projects offering clear contribution pathways and modularity (NanoBot’s transcription bus, ZeroClaw’s pluggable providers) are seeing higher *constructive* contributor density. **The next competitive advantage will be developer experience for contributors.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-09

## 1. Today's Overview
Project NanoBot is experiencing a surge in development velocity, with 36 Pull Requests updated in the last 24 hours, of which 16 were merged or closed. Community activity is concentrated on two major initiatives: a sweeping standardization of the voice transcription subsystem (adding AssemblyAI, Xiaomi MiMo, and OpenRouter providers), and the consolidation of a foundational Agent Collaboration architecture enabling cross-instance messaging. Security and stability remain a high priority, with critical fixes addressing symlink workspace escapes and a loopback SSRF vulnerability in MCP handlers. No formal release was cut today, but the volume of merged code strongly suggests an imminent feature-rich release candidate is building.

## 2. Releases
No new releases today.

## 3. Project Progress
The project advanced significantly on infrastructure, provider support, and hardening:

- **Agent Collaboration (#3992 [CLOSED]):** A major architectural milestone. This PR enables multiple agent instances to communicate through a shared message bus, moving NanoBot beyond single-agent loops toward autonomous multi-agent workflows.
- **Transcription System Standardization:** Voice input was elevated to a top-level shared capability (#4232 [CLOSED]). New transcription providers shipped: OpenRouter (#4113 [CLOSED]), Xiaomi MiMo ASR (#4175 [CLOSED]), and AssemblyAI (#4224 [CLOSED]).
- **Provider Flexibility:** Added `extra_query` configuration for OpenAI-compatible providers (#4217 [CLOSED]), directly resolving Azure-style gateway compatibility issues where `?api-version=` params are required.
- **WebUI Polish:** Version information is now displayed in Settings > Overview (#4235 [CLOSED]), closing a long-standing UX gap.
- **Security Hardening:** A vulnerability allowing restricted exec tools to follow symlinks out of the workspace was blocked (#4221 [CLOSED]). Session history trimming was also fixed to drop orphan tool results before legal-boundary cuts (#4219 [CLOSED]).

## 4. Community Hot Topics
The contributor base is highly engaged and shipping production-quality code:

- **Agent Collaboration (#3992 [CLOSED]):** The cross-instance message bus is the most architecturally significant merged PR this period. It unlocks complex agent-to-agent workflows and has likely been the project’s most discussed internal feature.
- **Email Inbox Automation (#4170 [OPEN]):** This PR proposing configurable IMAP post-actions for agent-managed mailboxes signals a clear community appetite for turning NanoBot into a full inbox operator. It has remained under review since 2026-06-03.
- **Model Flexibility (#4253 [OPEN]):** A user request to override models per conversation — switching between fast remote OpenRouter models and private local llamacpp instances based on privacy or speed demands — reflects a growing need among power users for per-task model routing.
- **Version Badge Extension (#4255 [OPEN]):** After merging version display in Settings, a contributor has already submitted an extension adding a header badge with real-time PyPI update notifications, showing rapid iterative UX improvement.

## 5. Bugs & Stability

**High Severity (Security):**
- *MCP HTTP/SSE Loopback SSRF (#4074 [CLOSED]):* Fixed. MCP URL setup no longer attempts a loopback connection before applying SSRF rejection, aligning it with the security posture of network-facing fetch tools.
- *Symlink Workspace Escape (#4221 [CLOSED]):* Fixed. Relative symlink operands in restricted `ExecTool` commands are now resolved and blocked when they escape the working directory.

**Medium Severity:**
- *Telegram Fenced Code Block Splitting (#4250 [OPEN]):* The `split_message` utility can land on fence boundaries, causing broken HTML rendering in both chunks. A community fix PR (#4257 [OPEN]) making the splitter code-block-aware is already submitted.
- *WeChat Session Renewal Deadlock (#4223 [OPEN]):* After token expiry and a 60-minute pause, the polling loop returns without reloading `account.json`, creating a permanent silent failure. A fix is open and awaiting review.

**Low-Medium Severity:**
- *Memory Cursor Monotonicity (#4256 [OPEN]):* A regression fix to ensure cursor allocation stays stable when history is compacted or the cursor is stale.
- *Context Governor / Microcompaction Gating (#4238 [OPEN]):* An architectural refinement extracting model-message governance and gating compaction on actual context pressure rather than hard tool-result counts.

## 6. Feature Requests & Roadmap Signals

- **Per-Conversation Model Override (#4253):** The request to assign models at the conversation level is one of the strongest feature signals this period. It directly enables user workflows like "public fast model for quick questions / private local model for sensitive documents." Likely to see a PR within the next release cycle.
- **File & Image Upload in Chat Channels (#4251):** A user request to upload images or PDFs into WeChat/Telegram for summarization or vision analysis. This is a natural companion to the transcription revamp and points toward full multi-modal channel support.
- **Version Badge + Update Notifications (#4233 → #4235 → #4255):** The rapid lifecycle of this feature — from feature request to merged display to PyPI update notification PR — signals that basic UX quality-of-life improvements are a high priority for maintainers and contributors alike.
- **Context Optimization (#4238):** The move toward dynamic context pressure gating rather than fixed limits suggests the project is actively preparing for long-running, memory-intense agent sessions.

**Prediction for Next Release:** The unified transcription system, Agent Collaboration infrastructure, and the backlog of security fixes are strong candidates to ship together as a milestone release.

## 7. User Feedback Summary

- **Pain Points:**
  - *Telegram Formatting:* Fenced code blocks breaking across split messages is a concrete daily annoyance for Telegram users.
  - *WeChat Silent Failures:* The token expiry deadlock is a hard blocker for the WeChat channel, which serves a large Asian user base.
  - *Missing Versioning:* The gap that prompted #4233 has now been resolved, but it underscores that basic UI maturity was lagging.
  - *Gateway Incompatibility:* Azure and custom gateway users needed explicit `extra_query` support (#4204), which is now merged.
- **Satisfaction Signals:**
  - Rapid merging of community-provided transcription providers (AssemblyAI, Xiaomi, OpenRouter) indicates a responsive maintainer team.
  - Security reports (#4074) are being actively triaged and patched.
- **Use Cases Expressed:**
  - Alternating between privacy-sensitive local models and fast remote models per conversation.
  - Turning the email channel into a fully autonomous agent inbox.
  - Running multiple agent instances collaborating on a shared task.

## 8. Backlog Watch
Several items need maintainer attention to prevent stagnation:

- **Yu-Xin-C's Feature/Test Suite (#3982, #3983, #4053, #4119, #4193):** A cluster of test harnesses, runner coverage, and security hardening PRs have been open since late May. While some related fixes have been shipped (e.g., #4221 supersedes elements of #4119), these PRs lack explicit maintainer confirmation on whether they are superseded or still pending review.
- **Email Channel Automation (#4170):** Open since 2026-06-03 with no recent maintainer activity. Given its alignment with the Agent Collaboration direction, this would benefit from triage.
- **WeChat Session Fix (#4223):** Open since 2026-06-06. This is a critical fix for a major channel and already has a proposed implementation. Delayed review risks user attrition on the WeChat platform.
- **Split-Message Fenced Code Fix (#4257):** Submitted by the same author as the provider `extra_query` feature. It directly solves a reported bug (#4250) and is ready for review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-09

## 1. Today's Overview
The project is in a period of intense stabilization and feature integration, with a remarkably high volume of activity. **50 issues and 50 pull requests** received updates in the last 24 hours, yet no new releases were cut. The community is heavily engaged in reporting platform-specific orchestration issues (macOS Tahoe, Windows, Docker) and a growing cluster of Desktop application UI regressions. Simultaneously, core contributors submitted a strong wave of fix PRs covering cost tracking accuracy, agent context safety, web search reliability, and gateway infrastructure hardening (systemd, launchd, Windows transactional restarts). This pattern strongly suggests an upcoming maintenance or minor release focused on reliability and cross-platform robustness.

## 2. Releases
**No new releases were published today.** All development activity is concentrated on the default branch, with 46 open PRs awaiting review and merge.

---

## 3. Project Progress
*(Note: 4 PRs were closed/merged today; the below covers the most impactful open PRs driving the codebase forward.)*

### Core Agent Safety
- **Context Safety Refactor ([PR #42549](NousResearch/hermes-agent PR #42549)):** The unfinished-action guard is renamed and made mode-agnostic, unifying fallback detection across API modes (Codex and non-Codex).
- **Title Generation Timeout ([PR #42548](NousResearch/hermes-agent PR #42548)):** Passes timeout from caller and reduces `max_tokens` from 128 to 64 to prevent blocking on slow providers.
- **Billing Routing Fix ([PR #42547](NousResearch/hermes-agent PR #42547)):** Reorders ZAI endpoint probing so Coding Plan keys don't silently drain pay-as-you-go wallets.

### Gateway & Infrastructure Hardening
- **Systemd Clean Shutdowns ([PR #42555](NousResearch/hermes-agent PR #42555)):** Adds `ExecStop` helper to write planned-stop markers before `SIGTERM`.
- **Windows Transactional Restart ([PR #41148](NousResearch/hermes-agent PR #41148)):** Fail-closed coordinator for `hermes gateway restart` to prevent dual-gateway port conflicts.
- **Kanban DB Migration Protection ([PR #42553](NousResearch/hermes-agent PR #42553)):** Adds `_add_column_if_missing()` guard and conditional index creation to prevent race conditions.
- **Slack Liveness Check ([PR #42545](NousResearch/hermes-agent PR #42545)):** New `/hermes ping` command for detecting silent socket-mode disconnections.
- **Telegram UTF-16 Text Splitting ([PR #42523](NousResearch/hermes-agent PR #42523)):** Respects UTF-16 code unit budgets to prevent message truncation.
- **OpenRouter URL Fix ([PR #42558](NousResearch/hermes-agent PR #42558)):** Resolves `ERR_NAME_NOT_RESOLVED` from a malformed `https://openrouter/` URL missing the `.ai` TLD.

### Desktop & UI
- **Terminal Side Pane ([PR #42521](NousResearch/hermes-agent PR #42521)):** A resizable, themed terminal pane adjacent to the chat column.
- **Dashboard File Browser ([PR #42534](NousResearch/hermes-agent PR #42534)):** In-browser file browsing with upload, download, and drag-and-drop support.
- **Theme Flash Fix ([PR #34248](NousResearch/hermes-agent PR #34248)):** Injects active theme into served HTML to prevent default-palette flashes.
- **Loopback Dashboard Auth ([PR #42546](NousResearch/hermes-agent PR #42546)):** Allows token-mode desktop remotes to connect without a saved token via ephemeral session detection.

### Web & Search
- **Timeout Capping & Parallelization ([PR #42543](NousResearch/hermes-agent PR #42543)):** Caps search/extract timeouts and parallelizes Firecrawl scraping to prevent 14+ minute hangs (fixes #42360).
- **Cascade Backend for Web Extract ([PR #42550](NousResearch/hermes-agent PR #42550)):** Adds fallback priority chain when primary extraction service is unavailable.
- **Platform-Aware Tool Deferral ([PR #42551](NousResearch/hermes-agent PR #42551)):** Opt-in progressive disclosure for core tools via `tool_search_deferred_core` config.

### Bug Fixes
- **Cost Tracking Massive Undercount ([PR #42554](NousResearch/hermes-agent PR #42554)):** Fixes three root causes: dropped token fields for Telegram sessions, missing pricing aliases, and API call cost counting.
- **STT Command Security ([PR #40948](NousResearch/hermes-agent PR #40948)):** Quotes local command placeholders by context to prevent shell-template injection.

---

## 4. Community Hot Topics

### Most Active Discussions

- **Declarative Skill Protection Policy ([Issue #27997](NousResearch/hermes-agent Issue #27997)):** The highest-comment issue (7 comments). Users are demanding a centralized, declarative policy to address scattered skill safety enforcement. Deep architectural concern with high community alignment.

- **Dashboard Ctrl+V Paste Broken ([Issue #24860](NousResearch/hermes-agent Issue #24860)):** 6 comments, 1 reaction. A fundamental UX workflow has been broken for nearly a month. This remains a persistent source of user friction with no dedicated fix PR yet visible.

- **Docker s6-log Lock Collision ([Issue #34457](NousResearch/hermes-agent Issue #34457)):** 6 comments, 3 reactions. Highly disruptive for multi-container deployments; interest significantly outpaces the attention seen in PRs.

- **macOS Launchd Double-Spawn Death Spiral ([Issue #21549](NousResearch/hermes-agent Issue #21549)):** 4 comments. This P1 bug has been resident for over a month; it remains a critical stability blocker for the macOS segment.

- **Multi-Profile Session Visibility ([Issue #38357](NousResearch/hermes-agent Issue #38357)):** 3 comments, 1 reaction. Users orchestrating multiple agent profiles want sidebar visibility across all sessions, not just the active profile.

### Underlying Needs
The community is signaling a clear hierarchy of unmet needs:
1. **Reliability:** Silent failures (cost, memory, Slack drops) erode trust.
2. **Platform Consistency:** Mac (launchd), Windows (restarts), and Docker (s6-log) each have distinct stability gaps.
3. **Desktop UX Maturity:** The Desktop app is gaining features but regressing in basic text interaction and state persistence.
4. **Configuration Centralization:** Users want formal skill policies, default sampling params, and standardized tool safety.

---

## 5. Bugs & Stability

### P1 – Critical
| Issue | Description | Status |
|---|---|---|
| [#42449](NousResearch/hermes-agent Issue #42449) | `delegate_task` corrupts parent context via shared singleton | Open – no dedicated fix PR yet |
| [#21549](NousResearch/hermes-agent Issue #21549) | macOS `launchd` infinite restart death spiral | Open for 33 days |
| [#42524](NousResearch/hermes-agent Issue #42524) | macOS 26 Gateway: `launchctl` exit 5 → detached fallback | Open (filed today) |
| [#42021](NousResearch/hermes-agent Issue #42021) | API call failed after retries / HTTP 500 cascade | Open (new report) |

### P2 – High Impact
| Issue | Description | Status |
|---|---|---|
| [#42505](NousResearch/hermes-agent Issue #42505) | Matrix recovery key logged in plaintext by default | Open (security) |
| [#42405](NousResearch/hermes-agent Issue #42405) | Memory at capacity → `replace` zero-match retry loop → silent hang | Open |
| [#42120](NousResearch/hermes-agent Issue #42120) | Desktop: manual Stop/Cancel loses partial turn content (data loss on user action) | Open |
| [#42376](NousResearch/hermes-agent Issue #42376) | macOS 26.5.1: `hermes gateway restart` generates broken plist | Open |
| [#24860](NousResearch/hermes-agent Issue #24860) | Dashboard Chat Ctrl+V paste broken | Open (27 days) |
| [#34457](NousResearch/hermes-agent Issue #34457) | Docker multi-container s6-log lock crash loop | Open (11 days, high interest) |

### P3 – Desktop UI Regression Cluster (48h)
Multiple Desktop bugs filed in the last 48 hours suggest integration testing gaps:
- [#42401](NousResearch/hermes-agent Issue #42401): Prompts discarded when switching screens
- [#42409](NousResearch/hermes-agent Issue #42409): Artifact timestamps render as Jan 1970 (epoch seconds / millisecond confusion)
- [#42422](NousResearch/hermes-agent Issue #42422): Discord sessions resurrected after deletion
- [#42431](NousResearch/hermes-agent Issue #42431): Files panel ENOENT in remote mode
- [#42433](NousResearch/hermes-agent Issue #42433): Cron view empty for script/no_agent jobs
- [#42468](NousResearch/hermes-agent Issue #42468): "Copy ID" broken due to nested Radix menu conflict
- [#42479](NousResearch/hermes-agent Issue #42479): Running state not cleared after stop button click

### Recently Resolved
- **OpenRouter Auth Header** ([#42130](NousResearch/hermes-agent Issue #42130)): *Closed today.* Requests were sent without the `Authentication` header despite configured credentials.
- **Langfuse Telemetry** ([#42306](NousResearch/hermes-agent Issue #42306)): *Closed today.* GENERATION spans were missing token counts and costs.

---

## 6. Feature Requests & Roadmap Signals

### Strong Roadmap Signals from PRs
- **Desktop as Primary Delivery Surface:** The incoming terminal side pane ([PR #42521](NousResearch/hermes-agent PR #42521)) and in-browser file browser ([PR #42534](NousResearch/hermes-agent PR #42534)) indicate a significant Desktop UX buildout is nearing readiness.
- **Observability & Hardiness:** Cascade web extract backends ([PR #42550](NousResearch/hermes-agent PR #42550)), timeout capping ([PR #42543](NousResearch/hermes-agent PR #42543)), and Slack liveness pings ([PR #42545](NousResearch/hermes-agent PR #42545)) point to a roadmap focused on resilient, observable deployments.
- **Multi-Agent Safety:** The `context_length` corruption fix ([#42449](NousResearch/hermes-agent Issue #42449)) and mode-agnostic guard refactoring ([PR #42549](NousResearch/hermes-agent PR #42549)) suggest deeper investment in multi-agent workflow integrity.

### User-Requested Features Likely for Next Release
| Request | Why It Fits |
|---|---|
| **Declarative Skill Protection Policy** ([#27997](NousResearch/hermes-agent Issue #27997)) | Matches the reliability/configuration centralization theme |
| **Multi-Profile Session Sidebar** ([#38357](NousResearch/hermes-agent Issue #38357)) | Aligns with Desktop feature expansion |
| **Default Sampling Params** ([#41988](NousResearch/hermes-agent Issue #41988)) | Sought by local model users; low complexity, high impact |
| **Usememos Memory Provider** ([#42506](NousResearch/hermes-agent Issue #42506)) | Clear niche extension, low overhead plugin |

---

## 7. User Feedback Summary

### Satisfaction Drivers
- **Responsiveness:** The core team and community contributors frequently submit fix PRs within hours or a day of bug reports. The cost tracking fix ([PR #42554](NousResearch/hermes-agent PR #42554)) and web search timeout fix ([PR #42543](NousResearch/hermes-agent PR #42543)) exemplify this.
- **Platform Breadth:** Users are actively using Hermes across Discord, Telegram, WeCom, iMessage (Photon), Slack, and Desktop CLI/TUI, and the team is maintaining feature support across all of them.

### Dissatisfaction & Pain Points
1. **Silent Failures:** Users are distrustful of gaps in feedback – cost reports show $0.01 for 400+ messages ([#42477](NousResearch/hermes-agent Issue #42477)), memory consolidation hangs without error ([#42405](NousResearch/hermes-agent Issue #42405)), and Slack events drop without detection ([#42545](NousResearch/hermes-agent PR #42545)).
2. **Data Loss:** Disappearing prompts ([#42401](NousResearch/hermes-agent Issue #42401)) and lost partial turn content ([#42120](NousResearch/hermes-agent Issue #42120)) are unacceptable for a productivity tool.
3. **macOS Tahoe Fragility:** Two P1/P2 issues specifically for macOS 26.x suggest the Tahoe release introduced significant regressions for Hermes.
4. **Desktop UI State:** The volume of recent P3 issues around the Desktop app suggests users are adopting it heavily but hitting rough edges.

### Use Cases Seen in the Data
- Multi-agent orchestration across profiles (orchestrator + specialist).
- Telegram groups using Hermes as a decision-making partner.
- Headless Docker deployments with shared state volumes.
- China-based users pushing for WeCom streaming parity.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Concern |
|---|---|---|
| [#12020](NousResearch/hermes-agent Issue #12020) – SSE event toggle | 52 days | Low priority but no roadmap commitment. Community needs a simple config flag. |
| [#24860](NousResearch/hermes-agent Issue #24860) – Dashboard paste broken | 27 days (P2) | High-engagement UX bug with no dedicated fix PR. Odd gap given Desktop activity. |
| [#21549](NousResearch/hermes-agent Issue #21549) – macOS launchd death spiral | 33 days (P1) | Remains open with no conclusive fix. This is a critical blocker for the macOS ecosystem. |
| [#34457](NousResearch/hermes-agent Issue #34457) – Docker s6-log lock | 11 days | Highest community reaction count. No clear fix path in current PRs. |
| [#16675](NousResearch/hermes-agent Issue #16675) – WeCom optimization | 43 days | Niche platform, but the ecosystem is clearly growing. Needs a feature plan. |

### PRs in Limbo
- **[#34248](NousResearch/hermes-agent PR #34248) – Theme Flash Fix (P3):** Open since May 29. A clean UX improvement that appears merge-ready.
- **[#41148](NousResearch/hermes-agent PR #41148) – Windows Transactional Restart (P2):** A critical fix for Windows stability; open since June 7.
- **Desktop UI Bug Cluster (Issues #42401, #42409, #42468, #42479, etc.):** Filed within 48h. These may indicate a broader Desktop regression that needs a consolidated triage and response, rather than isolated fixes.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw Project Digest — 2026-06-09

### 1. Today's Overview

PicoClaw has experienced a significant surge in activity, driven largely by a systematic code quality overhaul. In the last 24 hours, **19 pull requests** were updated with **9 merged/closed**, alongside **3 issues** updated. The project cut a new **nightly build (v0.2.9-nightly)**, while the main contributor focus shifted to hardening the codebase against panics and ensuring robust error handling. This "white-glove" refactoring, combined with a new DeltaChat gateway feature and fixes for the Telegram channel, indicates a project in a healthy state of active maturation alongside ongoing feature development.

---

### 2. Releases

**Nightly Build — `v0.2.9-nightly.20260609.46b29a0a`**
- **Note:** Automated build, may be unstable per the project warning.
- **Full Changelog:** [Compare v0.2.9…main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **Migration Notes:** None provided.
- **Assessment:** Heavy code quality changes have landed over the last 24 hours. Users on the stable `v0.2.9` branch should be aware that `main` contains sweeping low-level refactoring (type assertion guards, error wrapping, structured logging). No database schema or configuration-breaking changes are evident.

---

### 3. Project Progress

**9 PRs merged/closed in the last 24 hours,** representing a major push for stability and code quality:

**Agent & Core Stability**
- **Health check fixed:** A bug causing `/health` to always return "not ready" was resolved ([PR #3062](https://github.com/sipeed/picoclaw/pull/3062) by trufae).
- **`os.Getwd` error handling:** Two PRs addressed silenty ignored `os.Getwd()` errors in `NewContextBuilder` ([#3055](https://github.com/sipeed/picoclaw/pull/3055) & [#3018](https://github.com/sipeed/picoclaw/pull/3018)).

**Channel Fixes**
- **Telegram:** Location messages (`message.location`) were completely ignored by the adapter. Now converted to text for the agent pipeline ([#3052](https://github.com/sipeed/picoclaw/pull/3052) by wzg-gie, closes Issue #3049).
- **LINE Channel:** Fixed unchecked `sync.Map` type assertions in `Send` that could cause panics ([#3018](https://github.com/sipeed/picoclaw/pull/3018)).

**Code Quality & Linting ("The Great Cleanup")**
- **Structured Logging:** Replaced raw `log.Printf`/`fmt.Printf` calls with the configured structured logger across the codebase ([#3050](https://github.com/sipeed/picoclaw/pull/3050)).
- **Error Wrapping:** Fixed many sites using `%v` instead of `%w` in `fmt.Errorf`, restoring `errors.Is`/`errors.As` chain introspection ([#3051](https://github.com/sipeed/picoclaw/pull/3051)).
- **Type Assertion Safety:** Added `ok` checks to dozens of unchecked type assertions in Tools ([#3056](https://github.com/sipeed/picoclaw/pull/3056), [#3057](https://github.com/sipeed/picoclaw/pull/3057)), Webfetch ([#3058](https://github.com/sipeed/picoclaw/pull/3058)), and Evolution ([#3018](https://github.com/sipeed/picoclaw/pull/3018)).

**Open PRs of Note**
- **Agent Loop Reload Stability:** A structural fix for goroutine leaks and panic recovery during provider/config reloads remains open ([#2904](https://github.com/sipeed/picoclaw/pull/2904)).
- **DeltaChat Gateway:** A new communication channel backend is proposed ([#3063](https://github.com/sipeed/picoclaw/pull/3063)).

---

### 4. Community Hot Topics

- **[[ISSUE #2887]](https://github.com/sipeed/picoclaw/issues/2887) RISC-V .deb not functional with OpenAI model** — *9 comments, Open (stale)*
  The most active open issue. The RISC-V packaged version is broken with OpenAI's GPT models. While marked stale, the volume of troubleshooting discussion indicates a real community blocker for users on alternative architectures.

- **[[PR #3063]](https://github.com/sipeed/picoclaw/pull/3063) DeltaChat Gateway** — *New Feature*
  A notable roadmap signal. Adding DeltaChat suggests interest in unifying communications over email/MATRIX protocols and increasing privacy/sovereignty for users.

- **[[ISSUE #3015]](https://github.com/sipeed/picoclaw/issues/3015) QQ Channel Connection Failure on Windows** — *2 comments, Open*
  Active troubleshooting for a platform-specific bug (token retrieval timeout). Affects Windows users relying on the QQ channel bridge.

---

### 5. Bugs & Stability

**High Severity (Resolved)**
- **Telegram Location Messages Ignored** (Issue #3049 → PR #3052): Entire message type silently dropped. **Fix merged immediately.**
- **Health Check Broken** (PR #3062): `/health` endpoint always returned false positive "not ready". **Fix merged.**

**Medium Severity (Open / Fixes Pending)**
- **Windows Console Flashes** ([#3061](https://github.com/sipeed/picoclaw/pull/3061)): GUI users see flickering console windows when child processes spawn. Open PR.
- **Agent Loop Panic Risk** ([#2904](https://github.com/sipeed/picoclaw/pull/2904)): Detached goroutines on reload path can cause blocked goroutines and panics. Structural fix awaiting review.
- **Type Assertion Panic Vectors** (Multiple open PRs: [#3054](https://github.com/sipeed/picoclaw/pull/3054), [#3053](https://github.com/sipeed/picoclaw/pull/3053), [#3064](https://github.com/sipeed/picoclaw/pull/3064), [#3065](https://github.com/sipeed/picoclaw/pull/3065), [#3066](https://github.com/sipeed/picoclaw/pull/3066)): Unchecked assertions on `sync.Map` values, config entries, and migration keys could cause panics on malformed data. Systematic fixes are in the pipeline.

**Stale / Triage Needed**
- **[#2887] RISC-V + OpenAI Incompatibility:** A long-standing functional regression on RISC-V hardware with no clear path to resolution from maintainers.

---

### 6. Feature Requests & Roadmap Signals

- **DeltaChat Gateway** ([PR #3063](https://github.com/sipeed/picoclaw/pull/3063)): The most prominent new feature on the horizon. Predicts a move toward added user sovereignty and an alternative to proprietary channels.
- **Platform Hardening:** The massive volume of error-wrapping and type-assertion PRs signals that the core team is prioritizing stability and defensive programming. This likely precedes a minor stable release (v0.3.0).
- **Roadmap Prediction:** Expect the next stable release to focus on:
  1. **Channel Expansion** (DeltaChat)
  2. **Reliability** (Agent loop refactor, concurrent map guards)
  3. **Platform Parity** (RISC-V, Windows launcher UX)

---

### 7. User Feedback Summary

**Pain Points**
- **Windows UX:** Console flashes degrade the user experience for GUI launcher users.
- **Platform Fragmentation:** RISC-V users are locked out of OpenAI integrations; Windows users face QQ channel connectivity failure.
- **Silent Data Loss:** Telegram location messages were dropped entirely without log output, eroding trust in channel reliability.

**Positive Signals**
- **Rapid Response Time:** The Telegram location bug was filed on 2026-06-07 and the fix was merged by 2026-06-08. This demonstrates excellent triage and velocity for reported regressions.
- **Technical Debt Prioritization:** The community sees maintainers actively investing in structural code quality (error chains, logging infrastructure, type safety). This reduces long-term friction and burnout risks for the project.

---

### 8. Backlog Watch

- **[[ISSUE #2887]](https://github.com/sipeed/picoclaw/issues/2887) RISC-V `.deb` not functional with OpenAI model** *(Created: 2026-05-17, Updated: 2026-06-08)*
  *Highest priority backlog item.* Despite 9 comments and a clear user base on RISC-V, the issue is marked "stale" with no maintainer triage. This is a growing risk for community trust in platform support. Requires reproduction or a targeted workaround.

- **[[PR #2904]](https://github.com/sipeed/picoclaw/pull/2904) Fix agent loop reload and panic cleanup stability** *(Created: 2026-05-20, Updated: 2026-06-08)*
  *Critical stability fix awaiting review.* While the team merges many smaller linting PRs, this structural fix remains open for over two weeks. It blocks a class of serious runtime bugs (goroutine leaks, panics on reload). Deferring it indicates a careful review is required, but it should be prioritized for the next release cycle.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest – 2026-06-09

### 1. Today’s Overview

On June 9th, 2026, the NanoClaw project showed moderate activity driven largely by security hardening efforts alongside a critical functional regression. One new issue and three pull requests were updated in the last 24 hours. A major opt-in egress lockdown feature was merged, marking a significant step toward enterprise-ready container security. At the same time, a newly filed issue reveals that the v2 WhatsApp channel is completely unable to process inbound media files due to a container volume mount misconfiguration. No new releases were published today.

### 2. Releases

**None.** No new releases were tagged in the last reporting period.

### 3. Project Progress

Two pull requests were closed/merged today, and one security-focused PR remains open:

- **[PR #2713 – Closed/Merged: feat(security): egress lockdown (opt-in, off by default)](https://github.com/nanocoai/nanoclaw/pull/2713)**  
  A significant contribution from omri-maya. This feature places each agent container on a Docker `--internal` network, cutting off direct internet access and forcing all egress traffic through the OneCLI gateway. This is a foundational security layer for production or multi-tenant deployments.

- **[PR #2712 – Closed/Merged: [follows-guidelines] pull request](https://github.com/nanocoai/nanoclaw/pull/2712)**  
  A structural update from juhojeon86, appearing to be a template-based or guideline-related contribution, likely standardizing how new skills or integrations are submitted.

- **[PR #2714 – Open: security: fix four auth/security issues](https://github.com/nanocoai/nanoclaw/pull/2714)**  
  Authored by JorellDacasin, this open PR proposes critical fixes including binding the webhook server to `127.0.0.1` by default and replacing `Math.random()` with `crypto.randomUUID()` for approval IDs, guarding against prediction attacks on authentication tokens.

### 4. Community Hot Topics

The most significant community topic today is the newly filed **Issue #2715**, which exposes a critical functionality gap in the v2 WhatsApp channel:

- **[Issue #2715 – Open: Inbound WhatsApp media (images/docs/audio) is unreachable by the agent](https://github.com/nanocoai/nanoclaw/issues/2715)**  
  Filed by jon-ruth, this issue identifies a complete breakdown: inbound media files are saved to a host directory (`DATA_DIR/attachments`) that is not mounted into the agent container. The agent receives a non-functional path (`/workspace/attachments/...`).  
  **Underlying Need:** The community expects seamless multi-modal input handling (images, documents, audio) from core messaging channels. This bug reveals a deeper need for a robust, channel-agnostic file ingestion and workspace mounting layer in the v2 architecture.

Additionally, the open **PR #2714** on webhook binding and token security may attract attention from contributors concerned with OWASP-style vulnerabilities in default configurations.

### 5. Bugs & Stability

One high-severity bug was reported today:

- **[Issue #2715 – High Severity: Inbound WhatsApp media unreachable](https://github.com/nanocoai/nanoclaw/issues/2715)**  
  The agent is completely unable to access or process any media files sent via WhatsApp due to a container volume mount misconfiguration. No fix pull request has been linked to this issue yet. This represents a total failure of the media ingestion pipeline for one of the platform’s most popular channels and should be treated as an urgent stability item.

### 6. Feature Requests & Roadmap Signals

Today’s activity provides clear signals for the immediate roadmap:

- **Security Hardening Focus:** The merging of the egress lockdown feature ([PR #2713](https://github.com/nanocoai/nanoclaw/pull/2713)) and the pending auth/security fixes ([PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714)) strongly suggest that production-level container security and secure defaults are top priorities. PR #2714 is a highly likely candidate for the next patch release.

- **File System Architecture Rework:** The WhatsApp media bug ([Issue #2715](https://github.com/nanocoai/nanoclaw/issues/2715)) will almost certainly force a critical review of how the v2 attachment system maps directories into the agent workspace. Expect either an immediate hotfix to mount the `attachments` directory correctly, or a broader re-architecture of the agent inbox filesystem in a coming minor release (e.g., v2.1.x).

### 7. User Feedback Summary

- **Pain Point:** The most direct user pain point is the broken WhatsApp media handling. User jon-ruth explicitly details a failed core interaction: the agent “cannot open images/documents/audio”. This undermines trust in the v2 channel reliability and signals that core integration testing may need to be expanded.

- **Satisfaction Signal:** The successful merge of the egress lockdown feature ([PR #2713](https://github.com/nanocoai/nanoclaw/pull/2713)) is a strong positive signal for the DevOps and security community, demonstrating the project’s commitment to safe, auditable, and isolated agent deployments.

- **Use Case Insights:** The nature of the security fixes (webhook host binding, secure token generation) indicates that users are actively pushing NanoClaw toward production and multi-tenant environments where standard security audits are gatekeepers. The WhatsApp bug shows heavy reliance on multi-modal chat integrations.

### 8. Backlog Watch

- **[PR #2714 – Open, 0 comments: security: fix four auth/security issues](https://github.com/nanocoai/nanoclaw/pull/2714)**  
  Authored by JorellDacasin, this PR addresses four distinct security vulnerabilities (webhook default binding, weak RNG for tokens, etc.). Despite its critical importance for deploying NanoClaw securely, it has received no comments from the maintainers. Delaying this review and merge keeps users running on insecure default configurations. **This should be prioritized for review immediately.**

- **Issue #2715** is the most severe open functional bug. A fix should be drafted and linked to it as soon as possible to prevent the accumulation of user frustration and to restore WhatsApp channel functionality for the v2 user base.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-06-09

## 1. Today's Overview
Activity on IronClaw remains at a sustained high level, with 34 issues updated (22 open, 12 closed) and 50 pull requests updated (25 open, 25 merged/closed) in the last 24 hours. The project is firmly inside a major architectural transition: the bulk of development and discussion centers on the **Reborn product migration**, including auth parity, OpenAI-compatible API surfaces, operator tooling, and production storage wiring. Bug-fix velocity is also robust, with several regressions (OAuth lockout, Telegram conversation reset) caught and closed quickly. No new releases were cut today, but a pending v0.29.1 release PR remains in review.

---

## 2. Releases
**None.** No new releases were published today.

*(Note: Release PR [#3708](https://github.com/nearai/ironclaw/pull/3708) is open, detailing a jump from v0.24.0 to v0.29.1 with breaking changes in the `ironclaw_skills` crate.)*

---

## 3. Project Progress
Key features and fixes that reached a merged/closed state today:

### Reborn Architecture & API Surface
- **OpenAI-compatible ingress contracts** landed ([#4442](https://github.com/nearai/ironclaw/issue/4442)) — foundational route types for `/v1/chat/completions` and Responses.
- **Product refs and idempotency** added ([#4443](https://github.com/nearai/ironclaw/issue/4443)) — opaque `chatcmpl-*` / `resp_*` IDs and idempotency-key support.
- **Carry v1 SSO into WebChat v2** epic completed ([#4116](https://github.com/nearai/ironclaw/issue/4116)).
- **Product-facing auth HTTP surfaces** (manual token, recovery, refresh) implemented ([#4201](https://github.com/nearai/ironclaw/issue/4201)).

### LLM & Agent Capabilities
- **`ToolCall` gains `arguments_parse_error` field** ([#4576](https://github.com/nearai/ironclaw/pull/4576)) — improves error surfacing from provider tool-call parsing.
- **Planner subagent flavor** replaces researcher ([#4572](https://github.com/nearai/ironclaw/pull/4572)) — produces structured `Goal / Plan / Risks / References` output.
- **Codex client_version auto-detection** ([#4566](https://github.com/nearai/ironclaw/pull/4566)) — unlocks newer models (gpt-5.5) for ChatGPT-subscription users.

### Integrations & Platform
- **Google Calendar `list_events` fixed** ([#4578](https://github.com/nearai/ironclaw/pull/4578)) — `timeMin` now defaults to "now", returning upcoming events instead of oldest.
- **Slack host-beta workflow state persisted** ([#4528](https://github.com/nearai/ironclaw/pull/4528)) — adds durable idempotency ledger for Slack.
- **Automation run history UI** added ([#4580](https://github.com/nearai/ironclaw/pull/4580)).
- **Scoped outbound delivery defaults** implemented ([#4581](https://github.com/nearai/ironclaw/pull/4581)).

---

## 4. Community Hot Topics
The most active discussion threads reflect the intense focus on Reborn migration and security hardening:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#3283](https://github.com/nearai/ironclaw/issue/3283) | 3 | Migrate OpenAI-compatible Chat and Responses APIs onto Reborn (parent epic) |
| [#4175](https://github.com/nearai/ironclaw/issue/4175) | 3 | Reborn ProductAuth backend parity + OAuth PKCE HA safety |
| [#3957](https://github.com/nearai/ironclaw/issue/3957) | 2 | Hooks third-party activation hardening follow-ups |
| [#3959](https://github.com/nearai/ironclaw/issue/3959) | 2 | SecurityAuditSink adoption at remaining boundary sites |
| [#3026](https://github.com/nearai/ironclaw/issue/3026) | 2 | Epic: Reborn production wiring and cutover readiness |
| [#4587](https://github.com/nearai/ironclaw/issue/4587) | 1 | Bug: Cannot configure Minimax provider (filed today) |

Underlying needs: The community (largely core contributors and active staging users) is acutely focused on the stability and feature-completeness of the Reborn stack. OpenAI-compatible API parity is the most-requested architectural goal, while security authors are pushing hard on audit-sink coverage before third-party hooks go wide.

---

## 5. Bugs & Stability

### Critical / High Severity
- **OAuth users locked out of chat** ([#4536](https://github.com/nearai/ironclaw/issue/4536)) — Google/GitHub OAuth users redirected to `/welcome` and unable to send messages. **Closed** with fix.
- **Telegram conversation regression** ([#4556](https://github.com/nearai/ironclaw/issue/4556)) — upgrading from 0.28.2 to 0.29.1 causes every message to create a new WebUI conversation instead of continuing the existing thread.
- **403 Forbidden on running hosted agents** ([#4557](https://github.com/nearai/ironclaw/issue/4557)) — staging agents return `403` even while reported as `RUNNING` in CrabShack. Recovered automatically for some cases.
- **Minimax provider configuration fails** ([#4587](https://github.com/nearai/ironclaw/issue/4587)) — secret metadata reading error blocks chat completions. **Filed today.**
- **DeepSeek duplicate `model` field (400 error)** ([#4548](https://github.com/nearai/ironclaw/issue/4548)) — JSON body contains two top-level `model` fields when tools are present.

### Medium Severity
- **Incomplete i18n / translator crashes** ([#4554](https://github.com/nearai/ironclaw/issue/4554)) — hardcoded English strings remain across several WebUI v2 components; runtime crashes in the translator.
- **Reborn streaming projection does not yet support OpenAI SSE** — multiple PRs are in flight ([#4552](https://github.com/nearai/ironclaw/pull/4552)).
- **Nightly E2E test failure** ([#4108](https://github.com/nearai/ironclaw/issue/4108)) — scheduled CI run failing.

### Fixed Today
- Google Calendar `list_events` returning oldest events ([#4577](https://github.com/nearai/ironclaw/issue/4577), fixed in [#4578](https://github.com/nearai/ironclaw/pull/4578)).
- Codex `client_version` hidden models ([#4564](https://github.com/nearai/ironclaw/issue/4564), fixed in [#4566](https://github.com/nearai/ironclaw/pull/4566)).

---

## 6. Feature Requests & Roadmap Signals
The roadmap clearly prioritizes Reborn production readiness and developer ergonomics:

### Likely for v0.30 / Near Future
- **Reborn OpenAI-compatible routing** — #4495 (Chat Completions) and #4546 (Responses) are the top open PRs, with #4552 (SSE streaming) and #4571 (security gates) also in flight. This is the flagship feature.
- **Reborn operator experience** — #4533 is a new Epic covering `ironclaw-reborn` setup, config inspection, diagnostics, and service lifecycle.
- **Self-serve secrets management** — #4545 proposes a full UX for user-generated tool secrets without exposing values to the LLM.
- **Runtime service profiles** — #4543 adds credential injection for generic HTTP and skill-declared requirements.
- **Reborn approvals parity** — #4539 targets bringing V1-level approval UX (allow once, deny, always allow) to the new stack.

### Longer-term Signals
- **Trace Commons** — agent-driven onboarding via invite link (#4559/#4560) shows investment in federated observability.
- **WeCom channel** — validation (#4191) is thorough but reveals several unresolved edge cases (image recall, mention detection, onboarding flow).
- **Subagent compaction** — durability specs are landing (#4582), laying groundwork for multi-turn subagent interactions.

---

## 7. User Feedback Summary
Real user pain points visible from today's issues:

### Pain Points
- **Upgrade anxiety:** Telegram users experienced conversation discontinuity after upgrading to 0.29.1 (#4556). OAuth users were fully locked out (#4536, quickly fixed).
- **Provider configuration fragility:** Minimax (#4587) and DeepSeek (#4548) both exhibit integration bugs that block basic chat functionality.
- **Missing parity features:** Users need approvals (#4539), i18n (#4554), and secret management (#4545) to use Reborn in production workflows.
- **Operational confidence:** The 403 erratically on RUNNING staging agents (#4557) erodes trust in deployment status.

### Satisfaction Signals
- **Responsiveness:** The OAuth login bug was identified and closed within the same 24-hour window.
- **Aligned investment:** Community sentiment appears positive toward the OpenAI-compatible API push — it directly enables existing tooling to work against IronClaw agents.
- **Structured agents:** The planner subagent flavor (#4572) replaces a generic researcher with structured output, a clear quality-of-life improvement for agent authors.

---

## 8. Backlog Watch

| Issue | Age | Status | Risk |
|-------|-----|--------|------|
| [#3288](https://github.com/nearai/ironclaw/issue/3288) — Reborn capability lifecycle admin parity | Since May 6 | Open, 2 comments | **Medium** — blocks self-serve admin UX in Reborn. Many related issues are moving, but no dedicated implementation PR has materialized. |
| [#4191](https://github.com/nearai/ironclaw/issue/4191) — WeCom channel validation findings | Since May 28 | Open, 0 comments recently | **Medium** — a thorough review lists several functional gaps (image recall, refresh login, onboarding) with no fix PRs attached yet. |
| [#3957](https://github.com/nearai/ironclaw/issue/3957) — Hooks third-party activation hardening | Since May 23 | Open, 2 comments | **High (Security)** — must be resolved before `HOOKS_THIRD_PARTY_ENABLED` can be enabled in multi-tenant production. |
| [#3959](https://github.com/nearai/ironclaw/issue/3959) — SecurityAuditSink adoption at remaining boundaries | Since May 23 | Open, 2 comments | **High (Security)** — auditing gaps at auth-continuation dispatch, approval gating, and ThreadScope resolution. |
| [#3708](https://github.com/nearai/ironclaw/pull/3708) — Release v0.29.1 | Since May 16 | Open | **Low (Blocked)** — the release PR appears to be waiting on additional features or bug fixes before merging. The gap from 0.24.0 to 0.29.1 is large. |
| [#4108](https://github.com/nearai/ironclaw/issue/4108) — Nightly E2E failure | Since May 27 | Open | **Medium** — recurring CI failure without a clear root cause, reduces confidence in automated testing. |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI Project Digest – 2026-06-09

### 1. Today's Overview
Today the LobsterAI project showed sustained high development velocity, with **17 Pull Requests updated** in the 24-hour window, 16 of which were merged or closed. The activity was dominated by a coordinated push on **data migration** (backup/restore with rollback) and **authentication UX** (local callback server, Windows focus fix). A sizeable batch of community-submitted “stale” PRs was also closed, clearing long-standing fixes for log-export timeouts, silent bot failures, and missing UI fields. **No new issues were filed** and **no releases were cut**, suggesting the team is wrapping up feature work before an upcoming stable release.

---

### 2. Releases
**None.** No new releases were published today. Given the breadth of merged feature work (data migration, auth flow, model fetching), a version bump appears imminent.

---

### 3. Project Progress

Merged/closed PRs today represent major advances in both feature work and technical debt cleanup:

- **Data Migration Service (new feature):** A full user-data backup/restore service was added via [#2125](...). Follow-up fixes [#2126](...) (preserves runtime lock files and adds a rollback protocol) and [#2128](...) (excludes the `Network` directory from backup) hardened the implementation against corruption risks.
- **Authentication Revamp:** PR [#2122](...) introduced a localhost callback login flow that bypasses the browser protocol-handler confirmation dialog. PR [#2127](...) ensures the main window is brought to focus on Windows after callback login. Diagnostics were added in [#2129](...) to log portal URL selection (overmind vs. fallback) and callback redirect mechanism.
- **OpenClaw Gateway UI:** [#2123](...) now surfaces the gateway port, HTTP URL, phase-aware status badges, and a startup progress bar inside the Settings panel.
- **Test Infrastructure:** [#2124](...) enhanced the internal test mode.
- **Community Stale PRs Cleaned Up:** Multiple community-submitted fixes were finalized, including:
    - [#1510](...) – IM notification validation fix (task form no longer submits with empty `delivery.to`).
    - [#1514](...) – QQ Bot group allowlist now has a proper input field and add button.
    - [#1515](...) – Log-export timeout resolved by lowering DEFLATE compression level.
    - [#1517](...) – GitHub Copilot OAuth polling now cancels correctly on Settings panel unmount.
    - [#1521](...) – Fixed spurious OpenClaw gateway restart on `skills-changed` events.
    - [#1522](...) – Dynamic model list fetching from provider API (no more hardcoded model lists).
    - [#1524](...) – Detailed connection error messages (network, auth, proxy, DNS).
    - [#1526](...) – Cowork session color labels (7 colors) with full IPC + SQLite support.

---

### 4. Community Hot Topics
With **zero new issues filed** today and **zero comments/reactions** recorded on the latest PRs, the community discussion was effectively quiet. Activity was focused on merges rather than debate.

The only **open PR** is [#1277](...), a dependency bump by `dependabot[bot]` that has persisted since **April 2, 2026** (over 2 months). This is the single most visible community-facing risk item in the backlog.

The closed “stale” PRs represent a historical snapshot of user pain points that were addressed, covering model discovery, bot configuration, and OAuth robustness.

---

### 5. Bugs & Stability
No new bugs were filed today, indicating the current build is relatively stable. That said, several bugs were fixed in the batch of merged PRs:

- **[High] Data Migration Could Corrupt Runtime State ([#2126](...)):** Initial restore logic renamed the entire data directory, which destroyed runtime locks (SingletonLock, Cookie, lockfile) and risked crashes. **Fixed** by restoring entries in-place with a rollback safety net.
- **[High] Log Export Timeout ([#1515](...)):** Serial DEFLATE compression of multiple large log files exceeded the 30-second timeout, especially on lower-end machines. **Fixed** by reducing compression level.
- **[Medium] GitHub Copilot Token Loss ([#1517](...)):** Closing Settings during OAuth polling left the polling active; if the token arrived, it was silently discarded because the handler was unmounted. **Fixed** via proper `useEffect` cleanup.
- **[Medium] Windows Focus After Login ([#2127](...)):** After browser-based login, the app window remained buried behind the browser. **Fixed** by toggling always-on-top and stopping taskbar flash.
- **[Low] Silent Task Failure ([#1510](...)):** Scheduled IM notifications could be created with an empty recipient list, causing silent runtime failures. **Fixed** by adding form validation.
- **[Low] QQ Bot Allowlist Broken ([#1514](...)):** The allowlist switch had no UI input, making it completely unusable. **Fixed** by adding the missing input/add-button/tag-list.
- **[Low] OpenClaw Spurious Restart ([#1521](...)):** Minor skill changes triggered an unnecessary gateway process restart. **Fixed** by filtering the `skills-changed` event.

---

### 6. Feature Requests & Roadmap Signals

Based on the PRs merged today, several strong roadmap signals emerge:

- **Data Portability & Backup:** The new backup/restore service ([#2125](...)) signals a commitment to enterprise-grade data safety. This is a strong candidate for the next major release.
- **Seamless Desktop Login:** The local callback flow ([#2122](...)) addresses a ubiquitous UX pain point across Electron apps. Expect this to be the default login path going forward.
- **Proactive Connection Debugging:** Users will no longer see a generic “Connection Failed” message ([#1524](...)). The new granular errors empower users to self-troubleshoot.
- **Dynamic Provider Support:** Fetching model lists from provider APIs ([#1522](...)) instead of hardcoding them signals a strategic shift toward a more flexible, future-proof provider integration model.
- **UI Customization:** Session color labels ([#1526](...)) hint at a broader theme of workspace customization, potentially expanding to more visual organization tools.

---

### 7. User Feedback Summary
Since no new issues were created today, feedback is implicitly captured through the PRs that were closed:

- **Pain Points Resolved:**
    - “Logs can’t be exported because it times out.” *(Frustration, solved in #1515)*
    - “I can’t use new models unless I manually edit config files.” *(Blocking workflow, solved in #1522)*
    - “QQ Bot white-list mode is completely broken – no input field.” *(Unusable feature, solved in #1514)*
    - “Connection failures give no useful information for debugging.” *(Confusion, solved in #1524)*
    - “I have many sessions and need a visual way to organize them.” *(Usability gap, solved in #1526)*
- **Sentiment:** The willingness of maintainers to fix deep edge cases (e.g., rollback archives, lock-file preservation, DEFLATE levels) suggests a high standard of engineering and strong respect for user data safety. The multi-week lag on stale PRs is a downside, but the eventual closure was positive.

---

### 8. Backlog Watch

- **[CRITICAL] PR #1277 – Electron Deps Bump (dependabot[bot]) | [Link](...):**
    - **Status:** Open since **2026-04-02** (over 2 months).
    - **Scope:** Bumps `electron` from `40.2.1` → `42.3.3` and `electron-builder`.
    - **Risk:** This is the most prominent danger signal in the current backlog. Electron 40 → 42 includes significant Chromium engine upgrades, crucial security patches, and API changes. Developing new features (e.g., `area: main`, `area: renderer`) on an outdated Electron version while this bump languishes creates **growing security and compatibility debt**. Maintainers should prioritize rebasing and merging this PR before the next release.

- **No other stale/critical items:** The zero-issue count today implies a clean issue tracker, which is a healthy sign for maintainer responsiveness, though the *closed* stale PRs suggest some community contributions sat for over two months before action.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

**TinyClaw Project Digest — 2026-06-09**

---

### 1. Today’s Overview
The TinyAGI / TinyClaw project recorded a day of minimal public activity on June 9, 2026. The issue tracker remained completely idle, with zero issues opened or closed over the previous 24 hours. No new releases were cut. The single development signal is a community-contributed pull request addressing an installation blocker. Overall, the project is in a quiet phase with very low user-reported churn, likely reflecting a stabilization period or a narrow active user base.

### 2. Releases
**N/A** — No new releases were published today. The latest release remains unchanged.

### 3. Project Progress
No pull requests were merged or closed today. A single open pull request was submitted by a community contributor:

- **PR #280 – fix(install): add postinstall script to auto-rebuild better-sqlite3**
  *Author: dsy122 | Created: 2026-06-08*
  [https://github.com/TinyAGI/tinyagi/pull/280](https://github.com/TinyAGI/tinyagi/pull/280)
  This PR introduces an automated `postinstall` hook to handle native compilation of the `better-sqlite3` C++ addon, eliminating the previously required manual `npm rebuild` step.

### 4. Community Hot Topics
Discussion volume was exceptionally low. The primary topic among the community is implicit in the single open PR:

- **PR #280** — While it currently has no formal comments or reactions, it addresses a felt pain point: installation friction caused by native module builds. The underlying demand is for a zero-friction `npm install` experience, where the project compiles its dependencies automatically. This is the only signal for community interest today.

### 5. Bugs & Stability
- **No new bugs** were formally filed in the issue tracker.
- **Stability Signal**: The submission of PR #280 reveals an existing installation regression. Users on fresh clones were encountering `ModuleNotFound` errors because `better-sqlite3` (a native C++ addon) was not being compiled for the running Node.js runtime.
  - **Severity**: High — installation-blocking for new developers.
  - **Fix PR**: Exists (#280), currently open and awaiting review/merge.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were submitted today. The sole contribution signal points toward **Developer Experience (DX)** and **build-system hardening** rather than new user-facing features. The immediate roadmap trajectory implied by this single activity is reliability and friction reduction for new contributors.

### 7. User Feedback Summary
Direct user feedback (issues, comments) was absent in the data window. The strongest feedback signal is embedded in the contributor code submission: the `better-sqlite3` manual rebuild requirement is a recognized pain point that degrades satisfaction with the setup process. The community preference expressed here is for a "just works" installation, removing the need for users to understand or manually execute native rebuild commands.

### 8. Backlog Watch
The active issue queue is completely clean. The available snapshot data shows zero open or updated issues across the 24-hour window and a total of zero recent issues in the tracker. No long-standing or unattended items require maintainer attention at this time.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-09

*Project: agentscope-ai/CoPaw (QwenPaw), Data snapshot: GitHub Issues/PRs updated in last 24h*

---

## 1. Today's Overview
CoPaw is in a phase of exceptionally high development velocity, with **38 issues and 41 pull requests updated in the last 24 hours** — a significant spike in activity. Of these, **18 issues and 22 PRs were closed or merged**, reflecting a strong push towards stabilization and feature delivery. No formal release was cut today, but the volume of merged infrastructure work (plugin framework, protocol extensions) suggests an upcoming milestone release is being prepared. Community engagement remains intense, with users both stress-testing channel integrations and actively debating the future cognitive architecture of the agent.

---

## 2. Releases
**No new releases were published today.**

---

## 3. Project Progress
Several key pull requests were merged, advancing both stability and the feature roadmap:

- **DingTalk stability fix** — [[#4932](https://github.com/agentscope-ai/QwenPaw/pull/4932)] (hongxicheng): Fixes critical cross-user message merging bug caused by `conversation_id` suffix collisions.
- **Plugin Extension Infrastructure** — [[#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997)] (sanfran1068): Lands the unified frontend extension point registration mechanism for plugins (menus, routes, slots, chat extensions).
- **ACP Protocol Metadata** — [[#4949](https://github.com/agentscope-ai/QwenPaw/pull/4949)] (ekzhu): Extends the Agent Client Protocol server with command advertising, error surfacing, tool params, and model metadata.
- **Internationalization** — [[#4286](https://github.com/agentscope-ai/QwenPaw/pull/4286)] (aqilaziz): Adds Indonesian locale support for Sessions and Cron Jobs pages.
- **Installation fix** — [[#2771](https://github.com/agentscope-ai/QwenPaw/pull/2771)] (Kai-dev7): Restricts `mlx-lm` dependency to Apple Silicon macOS.

**Active PRs under review** signal a robust pipeline: Plugin Market tab [[#5023](https://github.com/agentscope-ai/QwenPaw/pull/5023)], DataPaw data-analysis plugin [[#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)], Tauri Desktop auto-updater [[#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)], lightweight Goal Mode [[#4443](https://github.com/agentscope-ai/QwenPaw/pull/4443)], and collapsible console code blocks [[#4345](https://github.com/agentscope-ai/QwenPaw/pull/4345)].

---

## 4. Community Hot Topics
The most active discussions reveal deep community investment in CoPaw's roadmap alongside frustration with critical channel bugs:

- **[[#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017)] Hermes Agent "Learning Loop" Integration** — 7 comments, **2 👍**: User `tecgic` praises QwenPaw as "very good" and "smooth out of the box in China," but strongly urges adopting Hermes-style automatic skill creation and iteration. This is the most-reacted topic today and signals strong user demand for self-improving agents.
- **[[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)] AgentScope 2.0 Migration** — 6 comments, **2 👍**: Users are actively anticipating and discussing this major backend re-architecture. Votes on this issue make it one of the highest-signal roadmap items.
- **[[#4477](https://github.com/agentscope-ai/QwenPaw/issues/4477)] WeChat iLink Cron Push Failure** — **15 comments** (highest today): Deep debugging of `context_token` expiry causing silent failures. Users are demanding retry logic and better logging.
- **[[#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003)] Ali Coding Plan Model Hang** — 8 comments: Users experiencing complete freezes when using `qwen3.7-plus` from Alibaba's Coding Plan provider.

---

## 5. Bugs & Stability
Stability is the dominant theme in today's reports, with several high-severity issues affecting core workflows:

### Critical
- **[[#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)] MCP Server Process Accumulation** — Processes leak across restarts, causing severe slowdown. A dedicated fix PR [[#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014)] (rayrayraykk) is under review.

### High Severity
- **[[#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025)] `submit_to_agent` FileNotFoundError** — Breaks inter-agent task submission due to a duplicated `session_id` in filenames. Fix submitted in [[#5026](https://github.com/agentscope-ai/QwenPaw/pull/5026)] (jc200808).
- **[[#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015)] Desktop Frontend Performance Lag** — Users report severe CPU spikes and UI stuttering during task execution on Windows desktop.
- **[[#5016](https://github.com/agentscope-ai/QwenPaw/issues/5016)] Web Console Multi-Agent Instability** — Custom agents are not reliably registered, displayed, or selectable in console chats.
- **[[#5030](https://github.com/agentscope-ai/QwenPaw/issues/5030)] WeChat Active Mode Duplicate Replies** — A single user message generates two similar responses. Workaround is disabling active mode.

### Medium Severity
- **[[#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031)] Skill Slash Command Displays Raw Content** — Invoking skills like `/pdf` renders the raw `SKILL.md` instead of executing the skill.
- **[[#5029](https://github.com/agentscope-ai/QwenPaw/issues/5029)] Pet Feature Crashes** — Frequent flash-crashes; users request it be marked experimental.
- **[[#4926](https://github.com/agentscope-ai/QwenPaw/issues/4926)] OneBot Listener Unresolved** — Zero-downtime reload breaks OneBot entirely.
- **[[#4895](https://github.com/agentscope-ai/QwenPaw/issues/4895)] Infinite Image Compression Loop** — Images compressed repeatedly, causing hallucination cycles.

---

## 6. Feature Requests & Roadmap Signals
User feature requests are coalescing around three themes: **agent cognition**, **infrastructure upgrades**, and **ecosystem expansion**.

### Cognitive / Self-Improvement
- **[[#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017)] Learning Loop (Hermes)** — Strongest demand signal. Users want agents that automatically create/iterate skills from experience.
- **[[#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994)] Self-Evolving Memory System** — Requests for hierarchical, adaptive memory.

### Infrastructure & Roadmap
- **[[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)] AgentScope 2.0 Migration** — High impact. The merged Plugin Extension Infrastructure [[#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997)] and this issue strongly signal a major architectural jump in the next version.
- **[[#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992)] Independent Visual Model Fallback** — Pragmatic: allow vision tasks without sacrificing a text-only primary model.
- **[[#5001](https://github.com/agentscope-ai/QwenPaw/issues/5001)] 9Router Support** — Connectivity request for an alternative API provider.

### Channel / UX Features
- **[[#4838](https://github.com/agentscope-ai/QwenPaw/issues/4838)] Silent Tool Execution** — Option to suppress final text response after tool calls in interactive channels.

**Prediction:** The combination of the Plugin Market PR [#5023], the Plugin Extension Infrastructure [#4997], and the AgentScope 2.0 breaking change [#4727] strongly suggests the **v1.2 (or v2.0) release will center on a revamped backend with a fully extensible plugin ecosystem.**

---

## 7. User Feedback Summary
**Satisfaction:** Core users express strong appreciation for CoPaw's localization, feature breadth, and ease of use. The praise in [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) ("体验非常好…开箱即用") is representative of the project's strong product-market fit in its primary region.

**Dissatisfaction / Pain Points:**
1. **Channel Reliability** — WeChat (token expiry, duplicate replies) and DingTalk (message merging) are the top friction points for production users.
2. **Desktop Performance** — The Windows desktop app's CPU spikes and session switching lag are generating multiple complaints.
3. **Pet Instability** — The new Pet feature is generating negative sentiment; users feel it was shipped prematurely.
4. **MCP Ecosystem** — Tool naming limitations and process leaks in MCP are blocking enterprise / structured API users.

**Engagement Quality:** The community is technically sophisticated — users are reading code to file bugs (e.g., pinpointing exact line numbers in `as_msg_handler.py` in [#5019] and `manager.py` in [#4877]), and they are actively linking their feature requests to competitor analysis.

---

## 8. Backlog Watch
Several long-standing or high-impact items require maintainer attention to avoid community fatigue:

| Issue | Opened | Days Open | Status |
|-------|--------|-----------|--------|
| **[[#2777](https://github.com/agentscope-ai/QwenPaw/issues/2777)] GPT-5.x model failures** | Apr 1 | 69 | No linked fix; hardcoded model list persists |
| **[[#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873)] Subagent infinite polling loop** | Jun 1 | 8 | Complex concurrency bug, no fix PR yet |
| **[[#4926](https://github.com/agentscope-ai/QwenPaw/issues/4926)] OneBot listener unrepaired** | Jun 3 | 6 | Stalled; maintainer awareness requested |
| **[[#4895](https://github.com/agentscope-ai/QwenPaw/issues/4895)] Infinite image compression loop** | Jun 2 | 7 | No linked fix; hallucination risk |
| **[[#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)] MCP subprocess leak** | May 31 | 9 | Fix PR [[#5014](https://github.com/agentscope-ai/QwenPaw/pull/5014)] submitted but unmerged |

The **GPT-5.x failure** is the most critical aging issue — untouched for over two months despite being updated today, indicating it is a persistent blocker for OpenAI-powered users.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-09

---

## 1. Today's Overview

ZeroClaw is in an exceptionally high-velocity development cycle, with **50 issues** and **50 pull requests** updated in the last 24 hours. The project merged or closed **11 PRs** in this period, demonstrating strong maintainer momentum despite a large parallel queue of 48 open issues and 39 open PRs. Activity is split between critical bug fixes (Matrix session isolation, runtime history trimming, file-write guarding) and major architectural RFCs for v0.9.0 (pluggable security providers, OIDC authentication, computer-use support). The project is simultaneously stabilizing existing features and laying groundwork for a significant security architecture overhaul, with community engagement remaining intensely high.

---

## 2. Releases

**No new releases were published** in this period. The heavy RFC activity targeting v0.9.0 suggests a major release is being actively prepared.

---

## 3. Project Progress

Despite the high open-item count, **11 PRs were merged or closed**, reflecting significant advancement across multiple components:

- **Runtime Stability (Merged):** [#7403](https://github.com/zeroclaw-labs/zeroclaw/pull/7403) (`tidux`) — Fixed a severe bug where `trim_history` could orphan-cascade and empty all conversation messages. Closed the same day it was opened.
- **Matrix Channel Overhaul (Merged):** [#7388](https://github.com/zeroclaw-labs/zeroclaw/pull/7388) (`singlerider`) — **Breaking change:** Isolates Matrix session state per channel alias, fixing the critical session-clobbering bug [#6487](https://github.com/zeroclaw-labs/zeroclaw/issues/6487). Requires manual session migration.
- **Hardware Demo (Closed):** [#6148](https://github.com/zeroclaw-labs/zeroclaw/pull/6148) (`Rhoahndur`) — End-to-end ESP32 smart-room demonstrator controlled via Telegram successfully completed.
- **Inbound Webhook Routing (Open/Advancing):** [#7367](https://github.com/zeroclaw-labs/zeroclaw/pull/7367) (`IftekharUddin`) — Routes webhooks per channel alias, resolving a long-standing defect where multi-instance configs only delivered to the first instance.
- **Web Chat Slash Commands (Open/Advancing):** [#7223](https://github.com/zeroclaw-labs/zeroclaw/pull/7223) (`NiuBlibing`) — Adds client-side slash commands (`/help`, `/clear`, `/model`, `/status`) to the gateway web chat.
- **Azure OpenAI Reasoning (Open/Advancing):** [#7350](https://github.com/zeroclaw-labs/zeroclaw/pull/7350) (`chengzhichao-xydt`) — Wires `reasoning_effort` into the dedicated Azure OpenAI provider.
- **Cron Job Startup Logic (Open/Advancing):** [#7348](https://github.com/zeroclaw-labs/zeroclaw/pull/7348) (`chengzhichao-xydt`) — Fixes overdue jobs being launched immediately on startup despite `catch_up_on_startup = false`.
- **Plugin Tool Parity (Open/Advancing):** [#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337) (`theonlyhennygod`) — Namespaces plugin tools (`plugin__tool` style) and wraps them in `RateLimitedTool`, bringing them to parity with native/MCP tools.

---

## 4. Community Hot Topics

The most active discussions reveal deep engagement with ZeroClaw's configuration surfaces, security model, and integration gaps:

| Item | Type | Comments | Core Theme |
|------|------|----------|------------|
| [#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) `tool_filter_groups` is a no-op for real MCP tools | Bug | 7 | Configuration disconnect — documented features don't affect runtime |
| [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) RFC: Computer-use for desktop interaction | Enhancement | 6 | Strong market demand for GUI automation (matching OpenAI Codex / Claude) |
| [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) Too much emphasis on memory | Bug | 5 | User pain with cron jobs over-prioritizing stored memories over prompts |
| [#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) Move translated i18n files to git submodule | RFC | 5 | Community interest in cleaner repo management for localization |
| [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) OIDC Authentication Provider | RFC | 4 | Enterprise auth demand, tracked for v0.9.0 |
| [#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) Pluggable security provider interface | RFC | 4 | Core architectural RFC for security extensibility |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) Per-execution shell confirmation tier | RFC | 4 | Community rejection of binary allow/ask/deny; wants Claude Code-style policy |

**Underlying needs:** Users are hitting real integration walls (MCP is non-functional, memories are too aggressive, Matrix is unreliable) while simultaneously pushing for ambitious new capabilities (computer-use, enterprise auth, granular shell security). The community is technical, demanding, and deeply invested in the project's architecture.

---

## 5. Bugs & Stability

The bug tracker shows a high density of severity S0 (data loss/security risk) and S1 (workflow blocked) issues, but the PR velocity suggests the team is actively firefighting.

### Critical (S0 — Data Loss / Security Risk)

- **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) Consecutive OOM in WSL2** — Open since April 9. `anon-rss: 8.4GB` before OOM kill. Status `in-progress` with `r:needs-repro`. Unresolved for two months. **Highest priority item needing maintainer investigation.**
- **[#4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627) `file_write` silently fails** — Files invisible on host filesystem. **Fix PR [#7129](https://github.com/zeroclaw-labs/zeroclaw/pull/7129)** (`IftekharUddin`) is open and actively reviewed, guarding all workspace surfaces against ephemeral targets.

### High Severity (S1 — Workflow Blocked)

- **[#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) Gemini 400 error** — History serializer places `assistant` tool_calls before first `user` turn, violating Gemini's strict ordering. Status `in-progress`.
- **[#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) Context compression drops `assistant(tool_calls)`** — Breaks multi-turn tool conversations with MiniMax and other OpenAI-compatible providers. Status `in-progress`.
- **[#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) Shell tool refused at `autonomy level = "full"`** — A confusing contradiction where permissive settings still block shell execution. Status `in-progress`.
- **[#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) Gemini CLI OAuth broken** — Authentication succeeds but requests immediately hit `rate_limited` errors. Open since late March.
- **[#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) Cron jobs launched repeatedly** — Jobs run 20+ times in bursts when they exceed the poll interval. Status `in-progress`.

### Fixes Actively Circulating

- **[#7404](https://github.com/zeroclaw-labs/zeroclaw/pull/7404) Matrix 30-second busy-poll** — `matrix-sdk` default timeout causes wasteful spinning. Fix proposed.
- **[#7402](https://github.com/zeroclaw-labs/zeroclaw/pull/7402) Gateway crash on transient `accept()` errors** — `EMFILE` conditions crash the gateway. Fix proposed.
- **[#7348](https://github.com/zeroclaw-labs/zeroclaw/pull/7348) Cron overdue job startup logic** — Fixes the `catch_up_on_startup` bypass bug. In review.

---

## 6. Feature Requests & Roadmap Signals

The v0.9.0 roadmap is clearly telegraphed through tracking issues, while community-requested features point to future priorities.

### Explicitly Tracked for v0.9.0

- **[#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) Pluggable Security Provider Interface** — Umbrella tracking issue. Exposes enforcement, reporting, and incident response behind a single trait.
- **[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) OIDC Authentication Provider** — Enterprise-grade authentication extensibility.

### High-Velocity Features Likely for v0.9.0

- **[#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) Per-execution shell confirmation tier** — Claude Code-style allow/ask/deny policy for shell commands. High community consensus, multiple PRs touching security infrastructure.
- **[#7267](https://github.com/zeroclaw-labs/zeroclaw/pull/7267) Per-field MCP server config editing** — Reduces reliance on raw `config.toml` editing, improving UX for the web dashboard.
- **[#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337) Plugin tool namespacing** — Closes the last parity gap between plugin tools and native tools.

### Market-Pressure Features (Probable Next Major Cycle)

- **[#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) Computer-Use (Desktop Screen/Mouse/Keyboard)** — Matches OpenAI Codex and Claude computer-use capabilities. High 👍 and active RFC discussion.
- **[#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) MCP Resource and Prompt Support** — Extending ZeroClaw from a pure MCP tool client to a full resource consumer. Open since March 24, status `accepted`/`in-progress`.
- **[#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287) Local-First Mode** — Compact prompts, strict parsers, no prompt-leakage for small models (Ollama). Vocal user base, growing demand.

---

## 7. User Feedback Summary

**Pain Points:**
- **Configuration Friction:** Users consistently report that documented features (`tool_filter_groups`, plugin paths, LeakDetector options) don't work as expected or require deep source-level debugging. The MCP filter no-op ([#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)) is a prime example of the trust gap this creates.
- **Model Support Gaps:** Provider-specific invariants are blocking workflows — Gemini history ordering ([#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)), MiniMax context compression ([#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361)), and Gemini OAuth ([#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)).
- **Memory System Over-prioritization:** Users running cron jobs report the system over-weights stored memories vs. the immediate prompt ([#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844)), leading to garbled outputs.
- **Security Model Binary:** The shell tool's allow/deny/auto-approve is too rigid; users want a middle tier requiring confirmation for high-risk commands ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)).

**Use Cases:**
- **Automation:** Cron jobs are a primary workload, but reliability is suffering (burst launches [#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037), memory over-emphasis [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844)).
- **Communication Channels:** Matrix is a deeply used channel (session isolation fix, 30s timeout fix, localization bypass) but has been unstable. Telegram users want smart message truncation ([#6225](https://github.com/zeroclaw-labs/zeroclaw/issues/6225)).
- **Local / Offline Agents:** A vocal subset runs Ollama and small models, seeking compact prompts and strict parsing to avoid prompt leakage and bloat ([#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)).

**Satisfaction / Dissatisfaction:**
- The community is highly technical and deeply engaged, but the density of S0/S1 bugs is eroding trust in production readiness.
- The transparent handling of the breaking Matrix change ([#7388](https://github.com/zeroclaw-labs/zeroclaw/pull/7388)) with clear migration documentation is a positive signal.
- The gap between "documented features" and "working features" remains a recurring source of user frustration.

---

## 8. Backlog Watch

Several critical and long-standing issues remain without clear resolution or maintainer action.

| Issue | Opened | Severity | Status | Concern |
|-------|--------|----------|--------|---------|
| **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)** Consecutive OOM in WSL2 | Apr 9 | **S0** | `in-progress`, `r:needs-repro` | **Most critical unresolved bug.** 2+ months without conclusive reproduction. Blocks all WSL2 users. |
| **[#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)** 153 commits lost in bulk revert | Apr 24 | **High** | `in-progress`, `help wanted` | Codebase integrity issue. Loss of reviewed/merged features. Needs forensic git recovery. |
| **[#4832](https://github.com/zeroclaw-labs/zeroclaw/issues/4832)** Config option to disable LeakDetector high-entropy redaction | Mar 27 | **P2** | `accepted` | Simple config addition. Unaddressed for 2+ months. Causes false positives on MD5 hashes, random filenames. |
| **[#3767](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)** Cross-channel TOTP gate for critical tools | Mar 17 | **P1** | `in-progress`, `accepted` | Ambitious security feature. No recent PR activity. Risks falling to v0.9.x. |
| **[#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467)** MCP Resource and Prompt support | Mar 24 | **P2** | `accepted`, `in-progress` | Foundational MCP enhancement. 4 👍 votes, no implementor assigned. |
| **[#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)** Local-First Mode for small models | Apr 4 | **P2** | `accepted`, `in-progress` | Growing demand. No dedicated PRs. Community is waiting. |

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*