# OpenClaw Ecosystem Digest 2026-06-27

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-27 02:49 UTC

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

Here is the OpenClaw project digest for 2026-06-27, based on the provided GitHub activity data.

---

## OpenClaw Project Digest – 2026-06-27

### 1. Today’s Overview
OpenClaw is in an exceptionally intense development and triage cycle, with **500 Issues** and **500 Pull Requests** updated in the last 24 hours. Of these, **24 Issues were closed** and **58 PRs were merged or closed**, leaving a large active queue of 476 open issues and 442 open PRs. No official releases were published today. The community is deeply engaged—filing detailed bug reports, contributing feature PRs, and voting on priorities—but the sheer volume of open items, particularly those blocked on product decisions and security review, indicates that maintainer bandwidth is a significant bottleneck relative to the velocity of community and internal contributions.

### 2. Releases
No new versions were published today.

### 3. Project Progress (Merged/Closed PRs)
Today’s 58 closed/merged PRs addressed several core stability and security items:

- **Session Integrity & Safety (Highest Impact):** Multiple fixes for truncated assistant tool calls were merged. PRs `#97140` (steipete), `#97092` (galiniliev), and `#97159` (thescottgarcia) prevent incomplete tool calls—generated when a session hits an output or abort limit—from executing, persisting, or replaying as valid tool use. This is a critical protection against session corruption.
- **Agent Isolation & Security:** PR `#96883` (joshavant) scopes agent-originated cron tool operations to the calling agent, fixing a significant multi-tenant security vulnerability.
- **Channel & Integration Fixes:** A fix for Feishu `appSecret` resolution was merged (`#96933`), and vCard media MIME type support was added (`#97143`).
- **Infrastructure:** The Autofix PR review pipeline (`#68936`) was merged, adding an automated loop for addressing review comments and a Windows daemon.
- **Diagnostics:** Guarded fetch diagnostics for model-fetch errors were added to improve debuggability of provider failures.

### 4. Community Hot Topics
The following issues and PRs generated the strongest engagement today:

- **Linux/Windows Desktop Apps (`#75`)** — 109 comments, 81 👍.  
  This remains the single most discussed topic. The community is strongly vocal about needing full desktop platform parity with the existing macOS app.
- **Native Anthropic Thread Bricking (`#94228`)** — Platinum Hermit severity, 7 comments.  
  A critical bug where long-running tool-use sessions on the native Anthropic provider path permanently break with “Invalid signature in thinking block” 400 errors. Users are highly concerned about this being a session-killing blocker.
- **Stuck Session Recovery Failure (`#76038`)** — Platinum Hermit severity.  
  The gateway’s stuck session recovery mechanism is doubly failing (lane occupancy and session pre-processing), leading to systemd timeouts and gateway crashes. This is the top stability complaint.
- **Clean Install Regression (`#76042`)** — Platinum Hermit severity.  
  Users are reporting that clean installations of versions 2026.5.xx are effectively impossible. This is a critical blocker for new user onboarding.
- **Masked Secrets (`#10659`)** — 13 comments, 4 👍.  
  The request for a system that lets agents use API keys without seeing them continues to draw strong support as the leading security feature.
- **Slack Block Kit Support (`#12602`)** — 13 comments.  
  Users want richer, interactive Slack messages instead of plain text. This is a key UX integration pain point.
- **Session Write-Lock Timeouts (`#86538`)** — Diamond Lobster severity.  
  Timeouts are blocking subagent and cron delivery lanes, creating cascading delivery failures.

### 5. Bugs & Stability
Ranked by severity and community impact:

**Critical (Platinum Hermit / P1)**
- `#94228` **Anthropic Native Path Bricks Long Sessions:** Permanent “Invalid signature” 400 error on multi-turn tool-use threads. Needs live repro. **No fix PR identified.**
- `#76042` **Clean Install Regression:** Users on 2026.5.xx versions cannot complete onboarding. Regression.
- `#76038` **Stuck Session Recovery Double Failure:** Gateway hangs until killed by systemd. Needs product decision and live repro.
- `#94224` / `#95725` **Cron Jobs with Empty Replies:** Cron jobs intentionally producing “silent” outputs fail with `FailoverError: CLI backend returned an empty response`. Fix PR `#95725` open.

**High (Diamond Lobster / P1)**
- `#22676` **Signal Daemon Race Condition:** Orphaned processes and send failures on SIGUSR1 restarts. Linked PR open.
- `#86538` **Session Write-Lock Timeouts:** Blocking subagent delivery lanes. Linked PR open.
- `#29387` **Bootstrap Files Silently Ignored:** Per-agent `agentDir` bootstrap configs have no effect.
- `#75380` **Unbounded Log Growth:** `provider-payload.jsonl` and `cache-trace.jsonl` grow without rotation (*impact:crash-loop*).
- `#75593` **Empty Subagents List:** `/subagents list` returns empty even after a successful spawn.
- `#76171` **Stale Worker Accumulation:** Stale processes drive host load averages to 25-31.
- `#77802` **`doctor --fix` Atomic Failure:** Multiple validation errors create a broken loop where fixes cannot persist.

**Regressions**
- `#77930` Discord channel loading broken in 2026.5.4-beta.2+.
- `#75621` Duplicate stdio MCP child processes lazy-spawned by gateway. (Closed as stale, but behavior is live).
- `#76038` / `#76042` Session recovery and install regressions.

### 6. Feature Requests & Roadmap Signals
Several strong roadmap signals emerged from the community today:

- **Platform Expansion:** The unprecedented demand for Linux/Windows apps (`#75`, 81 👍) and prebuilt Android APKs (`#9443`) signals the user base is scaling beyond the core developer niche and expects OS-agnostic tooling.
- **Production Security Stack:** There is a clearly defined roadmap emerging for enterprise-grade security:
  - **Masked Secrets** (`#10659`) — hide API keys from agent context.
  - **Filesystem Sandboxing** (`#7722`) — restrict `tools.fileAccess` paths.
  - **Exec-Approvals Denylist** (`#6615`) — “allow everything except X” policies.
  - **Capability-Based Permissions** (`#12678`) — default-deny for risky skill/tool actions.
- **Integration Maturity:** Requests for Slack Block Kit (`#12602`), Telegram Business Bot support (`#20786`), and Feishu permissions reduction (`#13751`) show deep platform-specific integration is a priority.
- **Context Budget Management:** The long-running Tiered Bootstrap proposal (`#22438`) with a ready companion PR (`#22439`) addresses a universal pain point (LLM token waste).

**Likely Features for Next Release:**
- **Tiered Bootstrap Loading** (`#22438`/`#22439`): A heavily vetted feature with a waiting PR. Token economy is a universal need.
- **Filesystem Sandboxing** (`#7722`): Given the number of security-flavored issues in the top 50, this feels like a headline feature in development.
- **Masked Secrets** (`#10659`): Directly addresses the single biggest user security anxiety.

### 7. User Feedback Summary
- **High Engagement, High Technical Sophistication:** The volume of high-quality, detailed issue reports and companion PRs indicates a deeply technical, invested user base. The “clawsweeper” triage labels provide transparent feedback on why items are blocked.
- **Core Frustration: Session Stability:** The most painful feedback revolves around session integrity. Stuck sessions (`#76038`), write-lock timeouts (`#86538`), and the Anthropic bricking bug (`#94228`) are causing users to lose work and trust in the session replay mechanism.
- **Growing Security Anxiety:** A significant fraction of top issues are security-related. Users love the platform’s power but are increasingly wary of running it without sandboxing (`#7722`), secret masking (`#10659`), and strong permission models.
- **Onboarding Pain:** The clean install regression (`#76042`) combined with a lack of prebuilt binaries for non-expert platforms creates a high barrier to entry.
- **Configuration Burden:** Users are asking for tools to manage complexity: the `doctor --fix` utility is popular, but its atomic failure bug (`#77802`) is painful. Backup/restore (`#13616`) and session cleanup (`#77941`) are highly requested.

### 8. Backlog Watch
Several high-value items with clear community investment remain stalled in the triage pipeline:

**Stalled Issues (needs maintainer / product decision)**
- `#22438` **Tiered Bootstrap Loading:** Ready PR (`#22439`), P2, fantastic signal. **Stalled since February.** (needs-maintainer-review, needs-product-decision)
- `#10659` **Masked Secrets:** High interest (4 👍). **Stalled on maintainer review + product decision + security review.**
- `#7722` **Filesystem Sandboxing:** High interest (4 👍). **Stalled on the same triple block.**
- `#6615` **Exec-Approvals Denylist:** High interest (7 👍). **Stalled on review.**
- `#12602` **Slack Block Kit:** P2, clear community value. **Stalled on product decision.**
- `#20786` **Telegram Business Bot:** Clear use case, 6 👍. **Stalled on product decision.**

**Stalled PRs (waiting on author / maintainer)**
- `#18889` **Agent Lifecycle Hooks:** Significant architectural PR. **Waiting on author since February.**
- `#28081` **Doctor Auto-Prune Config:** Small, safe QoL improvement. **Waiting on author since February.**
- `#22439` **Tiered Bootstrap Implementation:** **Waiting on maintainer review.**

**Long-Open Critical Bugs**
- `#22676` **Signal Daemon Race Condition:** Open since Feb 21. Linked PR exists but hasn't landed.
- `#11665` **Webhook Session Reuse:** Documented feature that is silently non-functional. Open since Feb 8.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: Personal AI Agent Open-Source Landscape

**Date:** 2026-06-27  
**Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The open-source personal AI agent ecosystem is undergoing an explosive maturation phase, driven by a highly technical user base that is demanding production-grade reliability, enterprise security, and multi-platform deployment. On June 27, 2026, the landscape reveals a clear bifurcation: the core reference implementation (OpenClaw) serves as the architectural gravitational center, while a wave of rapidly iterating derivative projects—IronClaw, ZeroClaw, CoPaw, LobsterAI—push boundaries in specific verticals like multi-agent orchestration, enterprise governance, and channel integration. The defining tension of the ecosystem is the widening gap between community contribution velocity and maintainer review bandwidth, forcing projects to choose between architectural consensus (OpenClaw) and rapid feature delivery (ZeroClaw, IronClaw). Session stability, multi-agent coordination, and cross-platform support have emerged as the non-negotiable battlegrounds where user trust is won or lost.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed (24h) | Release Today | Activity Level | Health Signal |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 82 | None | Extreme | Bottlenecked (maintainer bandwidth constrained) |
| **IronClaw** | 30 | 50 | 20 | Imminent | Very High | Unstable (deep feature churn, UX regressions) |
| **ZeroClaw** | 50 | 50 | 17 | v0.8.2 | Very High | Healthy (strong governance, feature velocity) |
| **CoPaw** | 28 | 50 | 32 | v2.0.0-beta.1 | Very High | Stabilizing (post-migration stress testing) |
| **Hermes Agent** | 50 | 50 | 16 | None | High | Targeted stabilization (Windows crises, compaction) |
| **NanoBot** | 20 | 39 | ~2 | None | High | Contributor-driven (v0.3.0 milestone push) |
| **LobsterAI** | ~3 | ~10 | 8 | v2026.6.26 | Moderate-High | Strong (polished feature shipping) |
| **PicoClaw** | 5 | 22 | 14 | None | Moderate | Healthy (rapid security/code hardening) |
| **NanoClaw** | 3 | 11 | 2 | None | Modest | Stable (focused stability patches) |
| **NullClaw** | 1 | 0 | 0 | None | Low | Idle (single build issue outstanding) |
| **Moltis** | 0 | 1 | 0 | None | Low | Niche (browser auto-screenshot focus) |
| **TinyClaw** | 0 | 0 | 0 | None | Inactive | Dormant |
| **ZeptoClaw** | 0 | 0 | 0 | None | Inactive | Dormant |

---

## 3. OpenClaw's Position

OpenClaw remains the undisputed **reference architecture** and **community giant**, with an issue/PR volume that exceeds the next most active project by an order of magnitude. Its advantages are structural: it defines the core security model, session protocol, and tool execution semantics that downstream projects inherit. LobsterAI explicitly bundles the OpenClaw runtime, demonstrating its foundational role.

**However, OpenClaw's strength is also its constraint.** A significant number of high-value, community-validated features (Tiered Bootstrap #22438, Masked Secrets #10659, Filesystem Sandboxing #7722, Slack Block Kit #12602) remain stalled on "maintainer review" or "product decision" labels for weeks or months. This creates a strategic vacuum that derivative projects exploit:
- **ZeroClaw** ships A2A discovery and config-driven runtime policy while OpenClaw debates them.
- **IronClaw** rapidly iterates on its Reborn Capability Policy engine (Epic #5261).
- **LobsterAI** ships Cowork Plan Mode multi-agent orchestration ahead of OpenClaw's sub-agent maturation.

**Community size comparison:** OpenClaw's 476 open issues and 442 open PRs represent an absolute user base that is 10-20x larger than any single peer. The "clawsweeper" triage system provides transparent but slow feedback, leading to user frustration on session-killing bugs (#94228, #76038, #76042, #86538). The core tension is clear: OpenClaw prioritizes architectural integrity; its peers prioritize delivery speed.

---

## 4. Shared Technical Focus Areas

Six requirements are emerging independently across multiple projects, representing the ecosystem's consensus priorities:

### 4.1 Session Integrity & Context Management
*Projects: OpenClaw, Hermes Agent, CoPaw, NanoClaw*
The single hardest infrastructure problem. Truncated tool calls, context compaction failures, and gradual state corruption are causing work loss and system crashes. CoPaw's Scroll Context Manager (PR #5321) and Hermes's aggressive compaction bug closures signal this is the defining engineering challenge of the ecosystem.

### 4.2 Platform Parity (Linux Desktop, Windows, Mobile)
*Projects: OpenClaw, Hermes Agent, NanoBot, LobsterAI, NullClaw*
The community is refusing macOS/server-only lock-in. The OpenClaw Linux/Windows Desktop app request (#75) accumulated 109 comments and 81 👍. Windows-specific crash loops in NanoBot (#4513), Hermes (#53342), and LobsterAI (#2214) confirm that stable Windows deployment is the ecosystem's most valuable unsolved market gap.

### 4.3 Enterprise Security & Governance
*Projects: OpenClaw, IronClaw, ZeroClaw, NanoBot, PicoClaw*
Demands have shifted from "can it run" to "can we control it safely." Capability policies (IronClaw), supply chain signing (ZeroClaw), masked secrets (OpenClaw), exec bypass protections (NanoBot), and SSRF hardening (PicoClaw) converge on a clear message: the ecosystem is preparing for organizational deployment.

### 4.4 Multi-Agent Orchestration
*Projects: OpenClaw, ZeroClaw, LobsterAI, CoPaw, NanoBot*
A2A discovery (ZeroClaw), Cowork Plan Mode (LobsterAI), agent delegation tools (NanoBot), and sub-agents (OpenClaw) confirm that single-agent architectures are considered legacy. The backlash against multi-agent noise in CoPaw (#5563) indicates that orchestration UX is still immature.

### 4.5 Channel Adapter Reliability
*Projects: NanoClaw, PicoClaw, Hermes Agent, ZeroClaw, CoPaw*
Chat platform integrations are the primary user interface. WhatsApp encryption fixes (NanoClaw #2870), WeChat onboarding parity (Hermes #50044), Telegram reply handling (ZeroClaw #5866), and WeCom file support (CoPaw #5554) show that channel reliability is treated as critical infrastructure, not a nice-to-have.

### 4.6 Cost & Model Management
*Projects: Hermes Agent, ZeroClaw, CoPaw, NanoBot*
Provider quota tracking in the status bar (Hermes #53375), offline pricing catalogs (ZeroClaw #8380), auto-fallback on quota exhaustion (CoPaw #5572), and reasoning effort escalation (NanoBot #4552) signal a maturing focus on operational cost control and model reliability.

---

## 5. Differentiation Analysis

The ecosystem is stratifying into distinct architectural philosophies and target user profiles:

| Dimension | OpenClaw | IronClaw / ZeroClaw | LobsterAI / CoPaw | NanoBot / Hermes | PicoClaw / NanoClaw |
|---|---|---|---|---|---|
| **Philosophy** | Reference architecture, consensus-driven | High-velocity feature factory, QA-heavy | Consumer/enterprise polished product | Power-user desktop productivity | Multi-channel proxy / bridge |
| **Primary Audience** | Framework adopters, infrastructure teams | Early adopters, feature hunters | End users, enterprise teams | Developer desktop users | Chat-platform-first users |
| **Security Approach** | Protocol-defined, review-blocked | Policy-driven (Capabilities, Signing) | Local-first, privacy-claimed | Shell allowlist, auth guards | Channel encryption, SSRF mitigation |
| **Multi-Agent Maturity** | Sub-agent primitives | A2A Discovery, Governance | Plan Mode, Room patterns | Agent delegation tools | Silent / not primary focus |
| **Platform Commitment** | macOS-first, parity demanded | Cross-platform pursuit | Polished Desktop (macOS/Windows) | Windows is a crisis | Server/headless oriented |
| **Innovation Velocity** | Slower (bottlenecked) | Very High | Moderate-High | Burst (contributor-driven) | Moderate (maintenance) |

**Key insight:** The market is not a zero-sum competition. OpenClaw defines the protocols that IronClaw, ZeroClaw, and LobsterAI implement more aggressively. A developer's choice depends on whether they need architectural stability (OpenClaw), rapid feature access (IronClaw/ZeroClaw), polished end-user UX (LobsterAI/CoPaw), or desktop productivity (NanoBot/Hermes).

---

## 6. Community Momentum & Maturity

### Tier 1: Extreme Velocity (High Churn, Heavy Investment)
- **OpenClaw:** Absolute scale leader. Maintainer bandwidth is the ecosystem's single biggest bottleneck.
- **ZeroClaw:** Strongest governance signal (RFCs, work lanes). Shipping A2A and supply chain signing.
- **IronClaw:** Deepest QA investment. Capability Policy engine advancing rapidly. Imminent release.
- **CoPaw:** Highest post-migration stress. Enterprise features (WeCom, DingTalk) driving intense Chinese-market adoption.

### Tier 2: High Velocity (Targeted Stabilization)
- **Hermes Agent:** Focused entirely on bug squashing and Windows stability. Context compaction wins are significant.
- **NanoBot:** Siloed burst toward v0.3.0. Plugin system, TTS, delegation are well-executed expansions.
- **LobsterAI:** Most polished release of the day (v2026.6.26). Cowork maturity is the headline.
- **PicoClaw:** Strongest security posture improvement across the board. Fastest response to critical bugs (WhatsApp timeout fixed same day).

### Tier 3: Modest / Niche
- **NanoClaw:** Quietly fixing channel reliability (WhatsApp, Discord). Migration fix unblocked old v1 users.
- **NullClaw:** Single engaged user wrestling with Android build. Maintainer attention absent.
- **Moltis:** Single PR for browser auto-screenshot. Low community engagement.

### Tier 4: Inactive
- **TinyClaw, ZeptoClaw:** Zero detectable momentum.

**Maturity verdict:** The ecosystem is transitioning from "prototype phase" to "production deployment phase." Tier 1 projects are where the architecture is being battle-tested. Tier 2 projects are where user-facing stability is winning. The gap between Tier 1 and Tier 3 indicates a consolidation wave is likely.

---

## 7. Trend Signals for AI Agent Developers

### 7.1 Session Infrastructure Is the #1 Competitive Moat
The cluster of session corruption bugs across OpenClaw (#94228, #76038), Hermes (#52261), and NanoClaw (#2865) reveals the deepest unaddressed risk in the ecosystem. Developers investing in robust, inspectable session stores (CoPaw PR #5321 is a textbook example) will capture disproportionate user trust.

### 7.2 Security Is the Adoption Gate
Users are refusing to deploy agents without sandboxed execution, secret masking, and signed releases. Projects without a clear security roadmap (like the `mcp_bundles` no-op in ZeroClaw #7733) will hit a deployment ceiling. The supply chain signing debate in ZeroClaw RFC #8177 is the canary in the coal mine for enterprise readiness.

### 7.3 Multi-Agent Is the Default Architecture
A2A discovery (ZeroClaw), Plan Mode (LobsterAI), and agent delegation (NanoBot) are not experimental; they are the expected interface. Building a single-agent tool in 2026 is like building a single-page app in 2016.

### 7.4 Channel Is the Real UI
The depth of investment in chat platform adapters (WhatsApp encryption, WeChat OAuth, WeCom files, Telegram caching) confirms that users do not primarily interact through custom web dashboards. A broken channel adapter is a broken product. The most successful projects will be invisible layers beneath the user's existing messaging habit.

### 7.5 Windows Is the Most Underserved High-Value Market
The volume and severity of Windows-specific crashes (NanoBot #4513, Hermes #53342, LobsterAI #2214) combined with the massive OpenClaw demand for Linux/Windows desktop apps (#75) indicate a pent-up user base that has been neglected by a macOS-first ecosystem. The first project to deliver a truly stable Windows experience will unlock significant user acquisition.

### 7.6 Cost Observability Is Becoming Mandatory
Provider quota bars, pricing catalogs, and auto-fallback are moving from "nice-to-have" to "deployment blocker." The ecosystem is producing sophisticated heavy users who operate on budgets and need reliability across multiple model providers. Tools for cost-aware agent routing and fallback will become a standard expectation.

### 7.7 The "Maintainer Gap" Is the Biggest Risk
OpenClaw's stalling on high-value features creates fragmentation risk. Development teams should evaluate whether they need the stability of the core reference (OpenClaw) or the velocity of a derivative (ZeroClaw, IronClaw). No single project currently offers both, making a multi-project dependency strategy the prudent architectural choice for production deployments.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — June 27, 2026

## 1. Today's Overview

NanoBot is experiencing an exceptional surge in development activity. While no formal release was published today, the project saw **39 Pull Requests and 20 Issues updated in the last 24 hours**, representing a coordinated push by the core team to clear the entire backlog. Contributor `dajiaohuang` submitted a sweeping batch of feature PRs and bug fixes, addressing nearly every critical open issue in a single concentrated effort. This behavior strongly suggests preparation for a major milestone release, likely v0.3.0. Project health indicators are highly positive, reflecting an extremely responsive and tightly aligned development cycle.

---

## 2. Releases

**No new releases published in this period.**

---

## 3. Project Progress

The bulk of today's activity came from submission of 12+ PRs by core contributor `dajiaohuang`, alongside meaningful community contributions. This represents a feature and stability leap across the entire application.

**Merged / Closed:**
- **[#4561](https://github.com/HKUDS/nanobot/pull/4561)** (Merged): Integrated **Crawl4AI** as an optional web extraction backend, addressing a long-standing request from April.
- **[#4539](https://github.com/HKUDS/nanobot/issues/4539)** (Closed): Fixed a bug where Telegram messages were not rendering on Telegram Web.

**New Feature PRs (Open):**
- **[#4558](https://github.com/HKUDS/nanobot/pull/4558)**: **Plugin System** — Adds minimal plugin architecture with `plugin.json` manifests for tools, skills, and MCP server configs.
- **[#4560](https://github.com/HKUDS/nanobot/pull/4560)**: **Text-to-Speech** — TTS tool supporting edge-tts, macOS `say`, espeak-ng, and Windows SAPI.
- **[#4559](https://github.com/HKUDS/nanobot/pull/4559)**: **Agent Delegation** — An `agent_delegate` tool for offloading tasks to Claude Code, Codex, and opencode.
- **[#4552](https://github.com/HKUDS/nanobot/pull/4552)**: **Reasoning Effort Escalation** — Allows the agent to dynamically deepen reasoning mid-turn.
- **[#4555](https://github.com/HKUDS/nanobot/pull/4555)**: **Per-Session Model Override** — Stores model preset in session metadata for per-conversation selection.
- **[#4556](https://github.com/HKUDS/nanobot/pull/4556)**: **Dream Model Override** — Applies a dedicated model for Dream memory consolidation.
- **[#4551](https://github.com/HKUDS/nanobot/pull/4551)**, **[#4553](https://github.com/HKUDS/nanobot/pull/4553)**, **[#4549](https://github.com/HKUDS/nanobot/pull/4549)**: **Heartbeat Revamp** — Adds `isolated_session`, `channel/chat_id` fixed delivery, and `model_override` configs.
- **[#4557](https://github.com/HKUDS/nanobot/pull/4557)**: **Parallel Tool Scheduling** — Trusts the LLM's parallel tool calls instead of serializing by tool class.

**Community Feature PRs:**
- **[#4357](https://github.com/HKUDS/nanobot/pull/4357)**: Adds `silent` flag for cron jobs that only report when action is needed.
- **[#4329](https://github.com/HKUDS/nanobot/pull/4329)**: Inline Terminal UI for `nanobot agent` via TUI.

---

## 4. Community Hot Topics

**Most Active Issue:**
- **[#660](https://github.com/HKUDS/nanobot/issues/660)** (12 comments, 5 👍) — *"Ultra-lightweight" branding controversy.* The community remains sharply divided on the project's claims of being lightweight versus the mandatory Node.js dependency in the Dockerfile. This old issue continues to draw engagement, reflecting a philosophical tension about project scope as features accumulate.

**Highly Engaged Feature Requests:**
- **[#2231](https://github.com/HKUDS/nanobot/issues/2231)** (4 comments) — **Plugin System** demand. Answered same week by PR #4558.
- **[#4253](https://github.com/HKUDS/nanobot/issues/4253)** (4 comments) — **Per-Conversation Model Switching**. This is a strong daily workflow need from users balancing local vs. cloud models. Addressed by PR #4555.
- **[#4419](https://github.com/HKUDS/nanobot/issues/4419)** (3 comments) — **Reasoning Effort Escalation**. User desire for automatic complexity-adaptive thinking. Addressed by PR #4552.

**Underlying Need:**
The thread across all hot topics is a community pushing NanoBot toward becoming a **fully extensible, multi-model agent orchestration platform**, beyond its original "ultra-lightweight personal AI assistant" framing.

---

## 5. Bugs & Stability

**Critical (Security):**
- **[#4562](https://github.com/HKUDS/nanobot/pull/4562)**: **`exec.allowPatterns` bypass** — The shell allowlist used `re.search()` on the raw command string, allowing chained commands like `echo ok && rm -rf /` to pass. Fix PR validates each shell segment individually. *Fix PR open.*

**High (Windows Stability):**
- **[#4511](https://github.com/HKUDS/nanobot/issues/4511)**: **Gateway state file PID mismatch** — After `/restart` on Windows, the PID in `gateway.json` is not updated, causing state tracking failures. *Fix PR #4547 open.*
- **[#4513](https://github.com/HKUDS/nanobot/issues/4513)**: **nssm service crash loop** — Using nssm to manage NanoBot as a Windows service leads to either infinite restart loops or silent process death. *Fix PR #4546 open.*
- **[#4544](https://github.com/HKUDS/nanobot/issues/4544)**: **Inconsistent shell semantics** — Single-line commands use `cmd.exe`, multi-line use PowerShell, causing cross-drive `cd` failures and literal `$VAR` interpretations. *Fix PR #4545 open.*

**Medium:**
- **[#4490](https://github.com/HKUDS/nanobot/issues/4490)**: **API server lacks auth guard** — OpenAI-compatible API can be bound to `0.0.0.0` without credentials, unlike the WS gateway which enforces auth. *Fix PR #4548 open.*
- **[#4082](https://github.com/HKUDS/nanobot/issues/4082)**: **Cron context leaking** — Repeated cron jobs share session context across runs due to a fixed `cron:{job.id}` key. *Fix PR #4550 open.*

**Low:**
- **[#4554](https://github.com/HKUDS/nanobot/pull/4554)**: Dream mode occasionally creates duplicate skill directories. *Fix PR open.*

---

## 6. Feature Requests & Roadmap Signals

**Strong Next-Release Predictions (v0.3.0):**
The coordinated submission of PRs #4550 through #4562 clearly signals an imminent **v0.3.0 "Extensibility & Stability" Release**.

- **Extensibility First:** Plugin system (#4558), Agent Delegation (#4559), Crawl4AI as alternative web backend (#4561).
- **Multimodal Expansion:** TTS (#4560) closes the voice loop — voice input existed, voice output arrives now.
- **Fine-Grained Model Control:** Per-session models (#4555), Dream overrides (#4556), Heartbeat overrides (#4549), Reasoning escalation (#4552).
- **Platform Maturity:** Windows stability fixes (#4545, #4546, #4547), API security (#4548), Parallel tool execution (#4557).

**Unaddressed Requests:**
- **[#4508](https://github.com/HKUDS/nanobot/issues/4508)**: `ask_clarification` tool for ambiguous user requests — a well-defined feature with no associated PR yet.
- **[#660](https://github.com/HKUDS/nanobot/issues/660)**: "Ultra-lightweight" claim remains unresolved.

---

## 7. User Feedback Summary

**Satisfaction:**
The core team's output is overwhelmingly positive from a community trust perspective. Users are seeing their top feature requests (Plugins, TTS, Per-Conversation Models) and most frustrating bugs (Windows crashes, Cron context leaks) turned into working fix PRs within hours or days of filing issues. This rapid responsiveness is a strong brand signal.

**Pain Points:**
1. **Windows Experience:** The cluster of Windows bugs (#4511, #4513, #4544) indicates Windows users face a consistently degraded experience compared to Unix users.
2. **Brand Confusion:** The `#660` "ultra-lightweight" debate highlights an identity crisis. Users appreciate rich features but feel the project description is misleading as complexity grows. The community would benefit from an explicit maintainer statement on project scope.
3. **Multi-Language Support:** Chinese-language issues (#1899, #4511, #4513) show a diverse non-English userbase that needs adequate documentation and support.

**Use Cases:**
Users are running NanoBot for persistent background automation (Cron, Heartbeat), integrating with Windows infrastructure (nssm), and seeking to extend it into an agent orchestration layer (Plugins, Delegation). This indicates a maturing userbase deploying NanoBot in production-like environments, not just experimental chat.

---

## 8. Backlog Watch

**Major Outstanding Issue (No Associated PR):**
- **[#660](https://github.com/HKUDS/nanobot/issues/660)** — *Created Feb 14, 2026 (133 days stale)*. This is the most visible unresolved community discussion. With 12 comments and 5 upvotes spanning four months, the maintainers have not directly addressed the "ultra-lightweight" claim. As PRs add more dependencies and features, this tension will only escalate. **Recommendation:** A maintainer response or README update clarifying the project's current design philosophy is overdue.

**Well-Defined Opportunity:**
- **[#4508](https://github.com/HKUDS/nanobot/issues/4508)** — `ask_clarification` tool. 1 comment, 1 day old. Clean scope, strong use case (reducing agent hallucination under ambiguity). Prime candidate for a future PR or good-first-issue.

**Cleared Backlog:**
Nearly every other open issue with a fix or feature request now has a corresponding open PR. The development team has effectively reset the board in a single push. The only items remaining unattended are #660 and #4508.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 27, 2026, based on the provided GitHub activity data.

---

# Hermes Agent Project Digest – 2026-06-27

## 1. Today’s Overview

Project activity remained very high today, with **50 Issues and 50 Pull Requests** updated in the last 24 hours. The community and maintainers appear to be in a heavy stabilization push: **11 Issues were closed** (including several long-standing P1 context-compaction bugs), and **5 PRs were merged or closed**. However, the open queue is heavily weighted toward bug reports, with **39 open issues** and **45 open PRs**. A notable concentration of **Windows-specific severity-1 bugs** emerged today, including reports of the client becoming completely inoperable due to console flickering. Concurrently, the closure of a series of high-priority context management bugs signals important progress in agent session stability.

## 2. Releases

**No new releases were cut today.** No release candidates, migration notes, or version bumps are recorded in the current data window.

## 3. Project Progress

Today saw the closure of several impactful bugs and the advancement of key features through the PR pipeline:

**Stability Milestones Achieved:**
- **Context Compaction & Session State (P1 fixes closed):** The project closed four high-priority issues related to context corruption:
    - **[#20250]:** VS Code ACP prompt remaining in-flight indefinitely after compression timeouts.
    - **[#29522]:** Automatic context compaction hiding/dropping just-completed assistant responses.
    - **[#28093]:** Context compaction dropping user messages that arrive during active processing.
    - **[#11585]:** Context compressor dropping messages when summarization fails.
- **Gateway & Config Resolution (P1/P2 fixes closed):**
    - **[#24100]:** Discord gateway command approval prompts routing to the wrong thread (stale session key leak).
    - **[#35927]:** Hermes TUI freezing on failed MCP OAuth.
    - **[#27715] & [#27602]:** Backward-compatible `HERMES_HOME` path resolver silently shadowing new config with empty old-format directories.

**Features & Enhancements in Review:**
- **[#53375] – Provider Quota in Status Bar:** A new PR adds dual-source provider quota and cost tracking to the CLI and TUI status bars, closing issue [#53306]. *(Open)*
- **[#50044] – WeChat QR Onboarding:** A major PR brings web-based WeChat (Weixin) setup parity with Telegram, enabling headless dashboard connection. *(Open)*
- **[#49958] & [#49902] – Desktop GUI Theming & User Settings:** PRs for a polished "cmux" theme and user-tunable text size/chat width are under review. *(Open)*
- **[#43812] – Teams Session Aliases:** API-server support for dynamic session aliases (`latest:teams`) was merged. *(Closed)*
- **[#51024] – Faster Docker Builds:** Docker builds were removed from default PR CI to accelerate the development loop. *(Closed)*

## 4. Community Hot Topics

The community is highly engaged, with deep investigations into blocking bugs and strong signal for desktop UX improvements.

- **[[#38240] – Skills Index Watchdog Degraded](NousResearch/hermes-agent Issue #38240) (18 comments)**
    A recurring automated health probe reports the skills index is stale (`degraded`). While a bot issue, the high traffic suggests investigation into the rebuild cron (`.github/workflows/skills-index.yml`) is ongoing.

- **[[#43564] – `hermes update` Prunes `agent-browser` Dependency](NousResearch/hermes-agent Issue #43564) (8 comments, 2 👍)**
    A critical usability blocker where `hermes update` reports success but leaves a missing Node/browser dependency. High engagement indicates this affects a significant number of users.

- **[[#52261] – Local LLM 400 Errors Misclassified as `context_overflow`](NousResearch/hermes-agent Issue #52261) (5 comments)**
    User `jp-cruz` provides a detailed analysis of a destructive loop affecting local inference (MLX/oMLX) users. Resource errors are incorrectly triggering context compression, leading to data loss. This is one of the most technically thorough investigations in the current window.

- **[[#44140] – Desktop GUI: Auto-scroll, Sidebar Overlap, Custom Groups](NousResearch/hermes-agent Issue #44140) (4 👍, 3 comments)**
    The highest-reacted feature request of the day, bundling three core desktop GUI polish issues. The strong reaction underscores desktop users' desire for a smoother chat interface.

- **[[#53349] – Feature Request: Per-Directory `soul.md`](NousResearch/hermes-agent Issue #53349) (2 comments)**
    A fresh, high-signal feature request asking for a `cwd-local` variant of `SOUL.md` to allow per-project agent identity, distinct from the global profile setting.

## 5. Bugs & Stability

A wave of **Windows-specific critical bugs** dominates today's stability landscape.

**Critical (Inoperable / Data Loss):**
- **[[#53342] – Windows: Persistent Black Console Flickering](NousResearch/hermes-agent Issue #53342)**
    *User quote: “making the program completely inoperable. This is a critical blocking bug!”* This is the highest-severity report of the day, filed by a user immediately after an upgrade.
- **[[#53374] – Desktop GUI Creates New Session After Windows Sleep](NousResearch/hermes-agent Issue #53374)**
    WebSocket reconnection logic fails after computer sleep, discarding the active session context and creating a new one.
- **[[#52261] – Local Inference 400s Misclassified (Destructive Compress/Reset)](NousResearch/hermes-agent Issue #52261)**
    A destructive loop hitting local-LM users (oMLX/MLX). The agent misreads provider resource limits as token overflows, aggressively compressing context and losing data.

**High (Blocking Workflows):**
- **[[#43564] – `hermes update` Prunes Dependencies](NousResearch/hermes-agent Issue #43564)**
    Blocks users from safely performing updates.
- **[[#53370] – Windows: Console Window Flash on `gh auth token`](NousResearch/hermes-agent Issue #53370)**
    Backend process spawning creates unwanted console windows. A fix is attached in **[#53371](NousResearch/hermes-agent PR #53371)** which also properly derives Python versions from `pyproject.toml`.

**Medium (Stability/Regression):**
- **[[#45520] – Dashboard WebGL Unavailable on Linux VPS](NousResearch/hermes-agent Issue #45520):** Blocks `hermes-desktop-launch.sh` on headless/software-rendered servers.
- **[[#52318] – TUI `/agents` Command Stuck on 'Running'](NousResearch/hermes-agent Issue #52318):** Subagent completion status not reflected in the TUI.
- **[[#53369] – Desktop: Duplicate Assistant Turn on Stream Variation](NousResearch/hermes-agent Issue #53369):** A fix is attached in the companion **[#53369 PR](NousResearch/hermes-agent PR #53369)** .

## 6. Feature Requests & Roadmap Signals

The community is signaling strong demand for **Desktop GUI maturity** and **per-directory configuration**.

- **Likely for Next Release:**
    - **[[#53349] – Per-directory `soul.md`](NousResearch/hermes-agent Issue #53349):** High-impact, low-complexity change. Aligns with existing `AGENTS.md` patterns.
    - **[[#53375] – Provider Quota/Cost in Status Bar](NousResearch/hermes-agent PR #53375):** PR is already submitted and merges a dual-source (Z.AI / standard) tracking system.
    - **[[#53341] – CLI `!` Prefix for Direct Shell Passthrough](NousResearch/hermes-agent Issue #53341):** An elegant solution for a common friction point (running shell commands via the agent loop).

- **On the Radar:**
    - **[[#50044] – WeChat QR Onboarding](NousResearch/hermes-agent PR #50044):** Active PR, critical for multi-platform parity.
    - **[[#39020] – Desktop: Dedicated Providers Settings Section](NousResearch/hermes-agent Issue #39020):** Addresses a major usability gap in managing API keys across providers.
    - **[[#4445] – Telegram Message Chunking During Streaming](NousResearch/hermes-agent Issue #4445):** Oldest open feature request (April 1), pending for large output formatting.
    - **[[#48985] – Safe MCP Profile Router for ChatGPT/Claude](NousResearch/hermes-agent PR #48985):** Draft PR exploring narrower, policy-driven MCP routing for third-party clients.

## 7. User Feedback Summary

- **Dissatisfaction: Windows Stability**
    - *“The Hermes desktop client on Windows keeps flickering black command prompt windows nonstop, making the program completely inoperable.”* – **#53342**
    - *“When the computer wakes up ... it creates a brand new session instead of resuming the previous one.”* – **#53374**
    - These two issues represent a crisis of confidence in the Windows Desktop client.

- **Dissatisfaction: Update & Workflow Gaps**
    - *“`hermes update` can leave the local Node/browser dependency `agent-browser` missing.”* – **#43564**
    - *“The web dashboard can show a session that belongs to a non-default profile, but opening/expanding the session fails to load its transcript.”* – **#44147**
    - *“After installing Hermes and configuring it with Anthropic as the provider... every API call fails immediately with extra usage limits.”* – **#31668**

- **Satisfaction / Value Confirmed:**
    - Local inference users are deeply engaged (e.g., **#52261**), actively debugging provider-interop issues, indicating Hermes is a valued tool in that space despite sharp edges.
    - The passionate response to the Desktop theme (reaction on **#44140**) shows heavy reliance on the GUI.

- **Use Case Signals:**
    - **Per-Project Persona:** The `cwd-local soul.md` request (**#53349**) highlights a growing need to segment agent identity by project/codebase.
    - **Multi-Platform Gateway:** Requests for WeChat parity (**#50044**) and Telegram chunking (**#4445**) show sophisticated multi-platform deployment patterns.

## 8. Backlog Watch

The following items are open, important, and may require additional maintainer attention.

- **[[#31668] – Hermes w/ Anthropic ratelimit/extra usage](NousResearch/hermes-agent Issue #31668) (P2, Open since May 24, 2026)**
    A critical provider configuration bug that blocks a major segment of users. Despite being updated today, it has been open for over a month.

- **[[#38240] – Skills Index Watchdog: Stale/Degraded](NousResearch/hermes-agent Issue #38240) (Open since Jun 3, 2026)**
    An automated system is continuously reporting a degraded state for the skills index. The volume of comments suggests the fix path is not trivial.

- **[[#7269] – WhatsApp `require_mention` / Allowed Users](NousResearch/hermes-agent Issue #7269) (P3, Open since Apr 10, 2026)**
    A long-standing design debate about group chat permissions. Users are confused about why mentioning the bot isn't sufficient to allow replies.

- **[[#17973] – TTS Splitting by Provider/Platform Limits](NousResearch/hermes-agent PR #17973) (Open since Apr 30, 2026)**
    An old PR solving a hard technical constraint (service limits on audio length). Context switching risk is high.

- **[[#13176] – Dashboard Security Hardening](NousResearch/hermes-agent PR #13176) (Open since Apr 20, 2026)**
    Important security PR aiming to reduce the blast radius of the `--insecure` flag. Would benefit from a final review and merge.

- **[[#13089] – Chinese Tokenization for Session Search](NousResearch/hermes-agent PR #13089) (Open since Apr 20, 2026)**
    Community-driven i18n improvement for FTS5 indexing. Low risk but likely requires Chinese-language expertise to review thoroughly.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the structured project digest for PicoClaw based on the activity data from June 27, 2026.

---

### PicoClaw Project Digest – 2026-06-27

**1. Today’s Overview**
PicoClaw is exhibiting a strong, healthy maintenance pulse on June 27th, with exceptionally high PR throughput. Of the 22 pull requests updated in the last 24 hours, 14 were merged or closed, signaling rapid iteration on code quality and stability. While no new version was released, the core team (particularly contributors `chengzhichao-xydt` and `Alix-007`) is systematically hardening the codebase by addressing linter warnings, improving error handling hygiene, and patching platform-specific bugs. Community engagement remains solid, with 5 active issues spanning Android crashes to WhatsApp connectivity problems.

**2. Releases**
No new releases were published in the last 24 hours. The project has no "Latest Releases" listed. Given the volume of merged bug fixes and improvements today, a patch release may be imminent.

**3. Project Progress**
The bulk of progress today centered on **code hardening and reliability**:
- **SSRF Security Fix Merged:** A significant vulnerability bypass (ISATAP IPv6 embedding) was patched in `#3143` (fix(web): block private IPv4 embeds in ISATAP literals).
- **Error Handling Hygiene:** Nine PRs by `chengzhichao-xydt` and `Alix-007` were merged to explicitly handle (and properly ignore) secondary `Body.Close()` and `json.Encode` errors across the LINE, OneBot, Pico, WhatsApp, health, updater, and membench modules.
- **Gateway Stability:** An open PR (`#3179`) directly addresses the newly reported WhatsApp timeout issue by implementing reconnection logic and async message dispatching.
- **CLI Robustness:** A fix (`#3180`) was introduced to gracefully skip tool calls with invalid JSON arguments rather than crashing the entire batch.
- **Dependency Updates:** Multiple automated dependency bumps were merged (`sqlite`, `line-bot-sdk-go`, `telego`, `systray`).

**4. Community Hot Topics**
The most active discussions and community pain points are centered around connectivity and security:

- **Security Upgrade Preference ([#3088](https://github.com/sipeed/picoclaw/issues/3088)):** This high-priority feature request to migrate from the deprecated `libolm` to `vodozemac` for Matrix encryption has strong community support (2 reactions). It is tagged as `help wanted`.
- **Sub-Agent Duplicate Messages Resolved ([#3094](https://github.com/sipeed/picoclaw/issues/3094)):** A user-reported bug regarding duplicate messages from asynchronous sub-agents was closed today, highlighting the team's ability to resolve complex workflow issues.
- **WhatsApp Connectivity Crisis ([#3178](https://github.com/sipeed/picoclaw/issues/3178) / [#3179](https://github.com/sipeed/picoclaw/pull/3179)):** A critical WebSocket timeout bug was reported and immediately addressed by a core developer (Alix-007) with a comprehensive fix PR. This rapid response demonstrates high maintainer vigilance.
- **DeltaChat Gateway ([#3063](https://github.com/sipeed/picoclaw/pull/3063)):** This long-running feature PR remains a hot topic, indicating a strong desire for expanding into decentralized chat protocols.

**5. Bugs & Stability**
Several bugs were reported or fixed today, ranked by severity:

- **Critical – Android Launch Failure ([#3182](https://github.com/sipeed/picoclaw/issues/3182)):** A new user reports being unable to launch PicoClaw as a service on Android despite full permissions. *No fix PR currently exists.*
- **Critical – WhatsApp WebSocket Timeout ([#3178](https://github.com/sipeed/picoclaw/issues/3178)):** Users faced persistent timeouts on the WhatsApp channel via Docker. *A fix PR (#3179) is already open and under review.*
- **Medium – CLI Invalid Arguments ([#3180](https://github.com/sipeed/picoclaw/pull/3180)):** Malformed tool calls could crash the CLI. *Open PR provides a fix.*
- **Medium / Stale – Agent Memory Loss ([#3150](https://github.com/sipeed/picoclaw/issues/3150)):** A Chinese-language bug report describes the agent losing its memory/context. The issue is stale and lacks a concrete reproduction, posing a risk of regressions.
- **Resolved – Duplicate Sub-Agent Messages ([#3094](https://github.com/sipeed/picoclaw/issues/3094)):** Fixed and closed today.
- **Resolved – SSRF Bypass ([#3143](https://github.com/sipeed/picoclaw/pull/3143)):** Fixed and merged today.

**6. Feature Requests & Roadmap Signals**
- **High Priority – Vodozemac Migration ([#3088](https://github.com/sipeed/picoclaw/issues/3088)):** This is the clearest roadmap signal. The team has acknowledged the security risk of `libolm` and is seeking implementation help. Likely target for the next major release.
- **In Progress – WhatsApp Auto-Reconnect ([#3179](https://github.com/sipeed/picoclaw/pull/3179)):** Given the urgency, this fix is highly likely to be included in the next immediate patch release.
- **Under Review – DeltaChat Gateway ([#3063](https://github.com/sipeed/picoclaw/pull/3063)):** A massive feature addition still awaiting merge. Its prolonged lifespan in the PR queue suggests it may be a **v0.3.0** or major release target.
- **Localization Expansion ([#3190](https://github.com/sipeed/picoclaw/pull/3190)):** A sync of missing keys for Bengali and Czech locales was opened, showing active work on internationalization.

**7. User Feedback Summary**
- **Pain Points:**
    1.  **Mobile/Platform Gaps:** The Android launch failure (#3182) is a significant user experience blocker.
    2.  **Channel Reliability:** Users are frustrated by WhatsApp WebSocket drops requiring manual reconnection (#3178).
    3.  **Contextual Consistency:** The "amnesia" bug (#3150), though not fully reproduced, suggests underlying fragility in long-context workflows or state management.
- **Use Cases:** Users are clearly leveraging PicoClaw as a multi-channel proxy (Telegram, WhatsApp, LINE) and utilizing the sub-agent spawning feature for complex async tasks.
- **Satisfaction:** Despite bugs, user trust appears high. The team's response time (fixing the WhatsApp issue on the same day it was reported) is extremely positive. Security-conscious users are actively requesting better encryption dependencies (Vodozemac).

**8. Backlog Watch**
The following items require maintainer attention or are at risk of stalling:

- **DeltaChat Gateway Integration ([#3063](https://github.com/sipeed/picoclaw/pull/3063)):** Open for 19 days. This is a substantial PR that adds significant value but needs maintainer review or requested changes. Risk of merge conflicts growing.
- **Vodozemac Migration ([#3088](https://github.com/sipeed/picoclaw/issues/3088)):** Tagged as `high priority` and `help wanted`, but has received no public maintainer assignment or roadmap commitment. If this is critical for Matrix users, it needs resource allocation.
- **Stale Memory Loss Bug ([#3150](https://github.com/sipeed/picoclaw/issues/3150)):** Unclear reproduction steps and a language barrier may be delaying a response. A maintainer should triage this to either close it or ask for a detailed `docker` reproduction.
- **Android Launch Failure ([#3182](https://github.com/sipeed/picoclaw/issues/3182)):** A critical issue with zero maintainer response yet. This should be escalated to prevent frustration from the mobile user base.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest: June 27, 2026

**Data Source:** [nanocoai/nanoclaw](https://github.com/nanocoai/nanoclaw)

---

## 1. Today’s Overview
NanoClaw experienced a high-velocity development day, with **11 pull requests** updated in the last 24 hours against only 3 issues. Activity is overwhelmingly tilted toward stability patches, with a single power user (grantland) driving a coordinated push across operational skills, MCP enhancements, and session management fixes. No new release was cut, but the pipeline is rich with critical fixes awaiting review. Project health is strong, though the widening gap between PR submission volume and maintainer bandwidth is becoming a visible constraint.

---

## 2. Releases
**None to report for June 27, 2026.** No new tags or releases were published today. The next release will likely bundle the growing backlog of stability fixes (WhatsApp delivery, Discord attachments, migration safety) alongside the new skill-based management tools.

---

## 3. Project Progress
Two pull requests reached final disposition:

- **[PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859) (Merged) — fix(migrate-v2): don't SELECT is_main from v1 registered_groups**  
  **Author:** cben0ist  
  **Impact:** Critical migration fix. The v2 database seed was querying an `is_main` column that only exists in later v1 installations. Older v1 instances (e.g., 1.1.0) crashed with `no such column: is_main`, blocking the entire v2.db creation and cascading failures into sessions and tasks. This PR resolves a significant upgrade blocker.

- **[PR #2867](https://github.com/nanocoai/nanoclaw/pull/2867) (Closed) — test. finding**  
  **Author:** Strke  
  **Note:** A test pull request, closed without merging.

**Advancing Features (Open PRs):**
- **[PR #2863](https://github.com/nanocoai/nanoclaw/pull/2863)**: Adds `/setup-system-digest` and `/system-digest` utility skills.
- **[PR #2862](https://github.com/nanocoai/nanoclaw/pull/2862)**: Adds `/manage-agents` and `/manage-schedules` as operational skills.
- **[PR #2861](https://github.com/nanocoai/nanoclaw/pull/2861)**: Enables `${VAR_NAME}` environment variable expansion in MCP server configurations at spawn time.

---

## 4. Community Hot Topics
While direct comment activity is low today, several items carry significant technical weight:

- **[Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868) — /update-skills is a silent no-op for installed channels**  
  glifocat filed a detailed bug report exposing that the skill-update pipeline skips code and depedency refresh for channels that are already installed. The underlying concern is trust in the update mechanism: users following the `[Unreleased]` CHANGELOG migration path are told to "re-run `/add-<channel>`", but `/update-skills` appears to do nothing silently. This erodes confidence in the skill lifecycle.

- **[PR #2870](https://github.com/nanocoai/nanoclaw/pull/2870) — fix(whatsapp): keep native participant addressing for group encryption**  
  elancode submitted a deep-dive fix for WhatsApp group replies that log as delivered but never appear. The root cause traces to `getNormalizedGroupMetadata()` being the sole provider for Baileys' `cachedGroupMetadata` hook. This is a strong signal that WhatsApp group channel reliability is a pain point for the user base.

- **[PR #2860](https://github.com/nanocoai/nanoclaw/pull/2860) — chore(logging): silence libsignal session debug spam**  
  caburi00 addresses leftover debug logging in the bundled libsignal dependency that fires `console.info` on every session open/close, including key material. This represents both a noise and a security concern.

---

## 5. Bugs & Stability
Ranked by severity:

**Critical**
- **[Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868) — `/update-skills` silent no-op**  
  The only open bug filed today. No fix PR exists yet. Should be prioritized as it undermines the entire skill update workflow.

**High**
- **[PR #2870](https://github.com/nanocoai/nanoclaw/pull/2870) — WhatsApp group replies silently dropped**  
  Fix proposed but unmerged. Group messaging in WhatsApp is non-functional without this.

- **[PR #2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord inbound attachments never reach the agent**  
  Open since **June 12** (two weeks). This is a fundamental channel feature regression. The PR stages attachments properly but awaits review.

- **[PR #2859](https://github.com/nanocoai/nanoclaw/pull/2859) — Migration crash for old v1 installs**  
  *Resolved today.* Older v1 users can now upgrade without crashing.

**Medium**
- **[PR #2866](https://github.com/nanocoai/nanoclaw/pull/2866) — Telegram legacy markdown sanitizer conflicts with MarkdownV2 adapter**
- **[PR #2865](https://github.com/nanocoai/nanoclaw/pull/2865) / [PR #2864](https://github.com/nanocoai/nanoclaw/pull/2864) — Stale session rotation logic needs ceiling-kill signal handling**

**Low**
- **[PR #2860](https://github.com/nanocoai/nanoclaw/pull/2860) — libsignal verbose session logging**  
  Fix proposed. Exposes sensitive session material in logs.

---

## 6. Feature Requests & Roadmap Signals
The clustering of PRs by grantland reveals a clear roadmap emphasis:

- **Skill-First Management Layer**  
  The introduction of `/manage-agents`, `/manage-schedules`, and `/setup-system-digest` (PRs #2863, #2862) signals a move toward making NanoClaw a self-supervising agent host rather than a simple chat bridge. These operational skills anticipate multi-agent deployments.

- **MCP Ecosystem Alignment**  
  PR #2861 (variable expansion in MCP server env) deepens NanoClaw's compatibility with the Model Context Protocol standard, enabling dynamic configuration.

- **Channel Reliability**  
  The three staggered fixes for WhatsApp, Discord, and Telegram indicate that channel adapter maturity is a current development focus.

- **[Issue #1275](https://github.com/nanocoai/nanoclaw/issues/1275) — Auto-registration on group add**  
  Closed today. The request (auto-detect new Telegram groups and prompt registration) was filed in March. Its closure without a merged implementation is ambiguous—it may have been declined or solved upstream. A maintainer note would clarify intent.

---

## 7. User Feedback Summary
**Pain Points (Recurring Themes):**
1. **Silent Failures**: The most consistent user experience complaint. `/update-skills` reports success but does nothing. WhatsApp group replies log as sent but never arrive. Discord file uploads are accepted but discarded.
2. **Upgrade Friction**: The v1→v2 migration path is brittle, as proven by the crash fixed today.
3. **Log Noise & Security**: Verbose libsignal logging exposes session key material.

**Satisfaction Signals:**
- The quality and depth of contributed fixes (elancode’s WhatsApp analysis, caburi00’s libsignal hygiene, cben0ist’s migration fix) suggest a healthy, capable contributor base.

---

## 8. Backlog Watch
Items requiring maintainer attention:

- **[PR #2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord attachments fix (🔴 2 weeks stale)**  
  Open since June 12 with no maintainer comments. This is a fundamental channel feature blocking Discord users. High priority for review or merge.

- **[Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868) — /update-skills silent failure**  
  Freshly filed, zero comments, no response. This bug invalidates the intended user workflow for the `[Unreleased]` migration. Needs at least a labeled acknowledgment or reproduction request.

- **[PR #2870](https://github.com/nanocoai/nanoclaw/pull/2870) — WhatsApp group encryption fix**  
  Detailed, well-documented fix with no review yet. Its complexity and impact warrant timely feedback.

- **[Issue #1275](https://github.com/nanocoai/nanoclaw/issues/1275) — Auto-registration (closed void)**  
  Closed without explanation. If declined or superseded, a follow-up comment would prevent confusion for kylenessen and future readers.

- **Grantland PR Cluster (5 open PRs)**  
  The burst of 5 PRs from a single contributor carries coordination risk. Prioritization and review bandwidth will be needed to avoid merge conflicts and ensure alignment with the release schedule.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest — 2026-06-27**

### 1. Today's Overview
The NullClaw project experienced a very quiet day on June 27, 2026, with no new releases or pull requests recorded. The sole activity update involved a long-standing open issue concerning a build failure on a mobile platform. Overall, project momentum is currently low, indicating a maintenance phase with no active feature development or community contributions landing today. While no new code merged, the existing conversation signals a lingering concern around platform portability.

### 2. Releases
No new releases were published in the last 24 hours. The most recent version referenced in the community is **v2026.4.17**, as noted in the open bug report.

### 3. Project Progress
No pull requests were merged or closed today. As a result, there are no newly landed features, performance improvements, or bug fixes to report on the main branch for this period.

### 4. Community Hot Topics
The entirety of community activity this period centers on a single build environment discussion:

- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868): Zig build fails on Android/Termux (aarch64) with AccessDenied**
  - *Author:* NOTJuangamer10 | *Comments:* 3 | *Updated:* 2026-06-26
  - **Summary:** The user is attempting to compile NullClaw using `zig build -Doptimize=ReleaseSmall` on a Xiaomi Redmi Note 9 running LineageOS via Termux. The build fails with an `AccessDenied` error during a `linkat` operation on `options.zig`.
  - **Analysis:** This discussion highlights a clear demand for running NullClaw directly on mobile hardware (Android/Linux). The underlying need is build system robustness across non-standard Linux environments. The use of `ReleaseSmall` flag suggests the user intends to deploy NullClaw as a resource-efficient background agent on the device.

### 5. Bugs & Stability
One active bug report was discussed, ranked here as **Medium Severity**:

- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868): Build failure on Termux**
  - **Impact:** Blocks source compilation on aarch64 Android environments entirely. This prevents a subset of users who rely on source builds from using the project on mobile hardware.
  - **Severity Assessment:** While the bug does not affect pre-built releases or standard desktop/server builds, it places a hard barrier on the project’s accessibility for the Android/Linux mobile community. No fix PRs or official workarounds have been linked to this issue.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the active bug report acts as an implicit roadmap signal:

- **Improved Build System Portability:** The failure mode (permissions error on `linkat`) suggests a lack of robust filesystem abstraction in the Zig build script. Addressing this would effectively deliver a “feature” of better cross-platform and containerized environment support.
- **Mobile Deployment Interest:** The intensive debugging (specific device, OS, and optimized build targets) strongly indicates a growing user interest in running NullClaw as a mobile-first AI agent, which could influence future packaging and documentation priorities.

### 7. User Feedback Summary
User sentiment today is limited but clearly articulated:

- **Pain Point:** The primary frustration is the inability to compile NullClaw on an Android device via Termux. The user provided detailed environment specs (LineageOS 22.2, Zig 0.16.0, aarch64) and explicit error output, signaling a technically proficient user blocked by an OS-level compatibility issue.
- **Satisfaction:** There is no evidence of dissatisfaction beyond the specific build failure. The lack of any maintainer response on the thread (since its creation in April) may contribute to a perception of neglect for alternative platform users.
- **Use Case:** The user is attempting a low-footprint optimized build (`ReleaseSmall`), implying a desire for an "always-on" AI agent running natively on a phone.

### 8. Backlog Watch
A single unresolved issue stands out as requiring urgent maintainer attention:

- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868): Zig build fails on Android/Termux**
  - **Age:** Open since April 23, 2026 (over 2 months).
  - **Status:** No official project response, triage label, or suggested workaround has been provided.
  - **Risk:** As the only actively discussed issue, its staleness poses a retention risk for the mobile hacking community. Even a brief acknowledgment or a request for more testing would help signal that the project is responsive to cross-platform deployment use cases.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

## IronClaw Project Digest — 2026-06-27

### 1. Today's Overview

The project saw extremely high activity in the last 24 hours, with **30 issues** and **50 pull requests** updated, signaling an acceleration toward a milestone release (a release PR [#5311](nearai/ironclaw Issue #5311) is already open). The majority of the churn focuses on the **Reborn stack**, where major architectural features—particularly the **Capability Policy system** (Epic #5261)—are advancing through a deep PR chain, while a simultaneous wave of QA-driven bug reports is revealing UX instability in tool approvals and automation creation. The team is keeping pace: **5 issues were closed** and **15 PRs were merged**, including several security-hardening items. Despite the high output, chronic CI flakiness and a growing list of critical UX bugs suggest stabilization work is far from done.

### 2. Releases

No new releases were published today. A release PR ([#5311](nearai/ironclaw Issue #5311)) is actively tracking version bumps, including API-breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0). A release cut appears imminent.

### 3. Project Progress

Several important features and structural improvements were merged or closed today:

- **Security Hardening:**
  - **[Issue #5009](nearai/ironclaw Issue #5009) (Closed):** Achieved structural DM-parity for the live Slack OAuth path, following a security reviewer recommendation.
  - **[PR #3766](nearai/ironclaw Issue #3766) (Merged):** `DispatchAuthorityProof` and `AuthorizedDispatchRequest` now seal the dispatch authority, preventing raw payload injection.
  - **[PR #3767](nearai/ironclaw Issue #3767) (Merged):** A host-level `NoExposureGuard` wrapping `LeakDetector` is now wired into HTTP egress and redaction paths.

- **Reborn Runtime & Infrastructure:**
  - **[PR #5265](nearai/ironclaw Issue #5265) (Merged):** The turn-runner concurrency is now configurable at runtime via an env var (0 = unlimited), facilitating stress-testing of the libSQL backend.
  - **[PR #3890](nearai/ironclaw Issue #3890) (Merged):** Added Reborn crate-level contract tests for multi-tenant isolation (filesystem, attachments, event cursors).
  - **[PR #5367](nearai/ironclaw Issue #5367) (Merged):** Regression coverage for LLM loop failure modes (invalid model output, explicit safe summaries).

- **Fixed User-Facing Bugs:**
  - App permissions persisting ([#5283](nearai/ironclaw Issue #5283)).
  - Disabled tools causing invocation of unrelated tools ([#5197](nearai/ironclaw Issue #5197)).
  - Run failures attaching to the wrong conversation turn ([#5227](nearai/ironclaw Issue #5227)).
  - "Logs" entry appearing inside the composer ([#5282](nearai/ironclaw Issue #5282)).

### 4. Community Hot Topics

The most active conversation clusters revolve around the **tool approval and permission system**, which is generating the most friction for users on the Reborn stack:

- **Auto-Approval Is Unreliable ([#5331](nearai/ironclaw Issue #5331)):** The "Always allow" setting may not auto-approve the second same-tool call. Currently under investigation as a suspected engine bug.
- **Deny Triggers More Approvals ([#5192](nearai/ironclaw Issue #5192)):** Denying a tool approval can cause the assistant to request approval for *unrelated* tools instead of reporting unavailability.
- **"Ask Each Time" Fails ([#5196](nearai/ironclaw Issue #5196)):** The "Ask each time" permission mode fails with an authorization error and triggers a duplicate approval flow, making it functionally broken.
- **Cross-Chat Blocking ([#5302](nearai/ironclaw Issue #5302)):** A pending approval in one conversation blocks sending messages in *all* other conversations until the user refreshes—a major workflow disruption.

These issues collectively indicate that the tool permission subsystem, while ambitious, requires a focused stabilization cycle before it can serve as the primary interaction model.

### 5. Bugs & Stability

Stability is the dominant theme of today's issue tracker. While several high-impact bugs were fixed, a significant number of new regressions were reported:

| Severity | Issue | Summary | Fix Status |
|----------|-------|---------|------------|
| **Critical** | [#5331](nearai/ironclaw Issue #5331) | `Always allow` fails on the second same-tool call (engine v2) | Investigating |
| **Critical** | [#5337](nearai/ironclaw Issue #5337) | Wasm-channel OAuth can never start first-time configuration (auth descriptor never seeded) | Open |
| **Critical** | [#5302](nearai/ironclaw Issue #5302) | Pending approval in one chat blocks all other chats until refresh | Open |
| **High** | [#5289](nearai/ironclaw Issue #5289) | Generic *"driver protocol error"* masks real `invalid_input` failures | Open |
| **High** | [#5322](nearai/ironclaw Issue #5322) | Automation creation times out before completing | Open |
| **High** | [#5323](nearai/ironclaw Issue #5323) | Runner lease expires before automation workflow completes | Open |
| **Medium** | [#5330](nearai/ironclaw Issue #5330) | E2E skills-tab tests fail because harness serves legacy gateway instead of v2 SPA | Open |
| **Medium** | [#5319](nearai/ironclaw Issue #5319) | Automation created with UTC schedule without asking user timezone | Open |
| **Infra** | [#5332](nearai/ironclaw Issue #5332) | `--all-features` coverage auto-enables forward gates, causing deferred-work tests to fail | Open |

**CI Health:** The Nightly E2E suite ([#4108](nearai/ironclaw Issue #4108)) has been failing since late May. A detailed failure taxonomy ([#5315](nearai/ironclaw Issue #5315)) and a dedicated harness backlog for DeepSeek-V4-Flash ([#5221](nearai/ironclaw Issue #5221)) suggest the test infrastructure is a known bottleneck the team is actively trying to resolve.

### 6. Feature Requests & Roadmap Signals

The project's forward-looking roadmap is clearly visible despite the stability churn:

- **Capability Policy (Epic [#5261](nearai/ironclaw Issue #5261)):** This is the dominant inbound feature. The PR chain is stacked and deep: Engine ([#5344](nearai/ironclaw Issue #5344)) → Availability dimension ([#5349](nearai/ironclaw Issue #5349)) → Control Plane / REST users ([#5355](nearai/ironclaw Issue #5355)). This moves IronClaw toward admin-managed shared tools and per-user authorization on the Reborn stack.
- **Default "Always Allow" ([#5364](nearai/ironclaw Issue #5364) → PR [#5366](nearai/ironclaw Issue #5366)):** A direct user request to flip the "Always allow eligible tools" default to ON. A fix PR is already open, making this very likely for the next release.
- **Trace Commons Integration ([#5280](nearai/ironclaw Issue #5280)):** Adds instance-wide enrollment and per-user trace inspection, pointing toward better observability for operators.
- **Channel Extensibility ([#5368](nearai/ironclaw Issue #5368), [#5362](nearai/ironclaw Issue #5362)):** The WebUI chat-connect shortcut is being removed in favor of generic channel pairing, with non-Slack channels being wired end-to-end.
- **Benchmark-Driven Fixes ([#5350](nearai/ironclaw Issue #5350), [#5221](nearai/ironclaw Issue #5221)):** Hill-climbing on PinchBench/ClawBench is directly generating harness fixes, showing a strong commitment to measurable task-completion quality.

### 7. User Feedback Summary

The most vocal feedback comes from **power user / QA (`sunglow666`)** and a **contributor advocating for defaults (`loopstring`)**:

- **Pain Points (sunglow666):**
  - **Automation Creation is Unreliable:** Multiple reports over two days describe timeouts, lease expirations, and confusing UTC-only scheduling ([#5320](nearai/ironclaw Issue #5320), [#5322](nearai/ironclaw Issue #5322), [#5323](nearai/ironclaw Issue #5323), [#5319](nearai/ironclaw Issue #5319)).
  - **Tool Permissions are Confusing:** Approve/Deny/Ask-each-time behaviors are inconsistent and produce unexpected cascading dialogs or silent failures ([#5192](nearai/ironclaw Issue #5192), [#5196](nearai/ironclaw Issue #5196), [#5331](nearai/ironclaw Issue #5331)).
  - **Poor Error Transparency:** Generic errors like "driver protocol error" hide real failures ([#5289](nearai/ironclaw Issue #5289)).
  - **Inconsistent Discovery:** Gmail extension discovery succeeds or fails non-deterministically ([#5316](nearai/ironclaw Issue #5316)).

- **User Experience Request (loopstring):**
  - The default "Always allow eligible tools" setting is OFF, meaning every new user/session faces repeated per-tool approval prompts. The explicit request to flip this to ON ([#5364](nearai/ironclaw Issue #5364), PR [#5366](nearai/ironclaw Issue #5366)) is a clear signal the out-of-box experience needs friction reduction.

### 8. Backlog Watch

Several items need maintainer attention to prevent stalling or to reduce risk:

- **[#4108](nearai/ironclaw Issue #4108): Nightly E2E Failure** (Open since May 2026). Continues to be updated with failures by `github-actions[bot]`. This chronic CI instability is a risk factor for regressions reaching users and blocks confidence in automated gating.
- **[#2355](nearai/ironclaw Issue #2355): Persistent Multi-Identity Browser Epic** (Open since April 2026). A massive feature (Chrome + CDP, encrypted sessions, built-in Rust tool). Despite its strategic importance, it only has a single comment and appears stagnant relative to its scope.
- **[#5221](nearai/ironclaw Issue #5221): DeepSeek-V4-Flash Harness Backlog** (Updated June 26). A detailed tracking issue with 9 hillclimb candidates and 8 steps spent. Clear owner (`pranavraja99`), but represents a large investment that needs ongoing resources to drive down.
- **[#5274](nearai/ironclaw Issue #5274): Runner-Lease CAS Loop Migration** (Updated June 26, Open since June 25). Requires migrating the runner-lease sidecar to the shared `cas_update` helper. Without a dedicated owner, this could drift, leading to CAS implementation inconsistency across the codebase.
- **[#5009](nearai/ironclaw Issue #5009):** Now closed, but this structural Slack OAuth parity work highlights the deep security investment underway that may have downstream impacts on other channel integrations.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured project digest for **LobsterAI** based on GitHub activity as of **2026-06-27**.

---

## 🏗️ Today's Overview

LobsterAI concluded an exceptionally productive development cycle on June 26, 2026, shipping version **`2026.6.26`** and merging 8 pull requests. The team's focus was split between maturing the **Cowork** multi-agent orchestration engine and hardening the **Artifacts** rendering pipeline. While the core features advanced significantly, a critical regression causing a hard crash during database backup on Windows 11 was reported, representing the primary stability threat for the daily build. Overall, project velocity is extremely high, indicating a push toward a significant milestone.

## 📦 Releases

**Version: [LobsterAI 2026.6.26](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.26)** (Released June 26, 2026)

The headline change is the upgrade of the OpenClaw runtime from `v2026.4.14` to `v2026.6.1` ([PR #2209](https://github.com/netease-youdao/LobsterAI/pull/2209)), which bundles multiple runtime patches, plugin upgrades, and build script updates. The most significant new feature is the introduction of a **Plan Mode Workflow** for the Cowork module ([PR #2183](https://github.com/netease-youdao/LobsterAI/pull/2183)), bringing structured multi-agent orchestration closer to production quality. No breaking changes or migration notes were provided in the release body.

## 🚀 Project Progress

Today saw **8 pull requests merged**, signaling a strong push toward feature stability and quality-of-life improvements.

- **Cowork Module Stabilization:** This was the primary area of investment.
  - **[PR #2207](https://github.com/netease-youdao/LobsterAI/pull/2207):** Fixes a critical UX bug where subagent progress was derived from fragile model-authored text instead of the local database. This prevents errors like showing `3/5` when the real state is `5/5`.
  - **[PR #2208](https://github.com/netease-youdao/LobsterAI/pull/2208):** Freezes the elapsed time counter for completed subagent runs using accurate `endedAt` timestamps, providing a reliable history view in the sidebar.

- **Artifacts & Rendering Rigor:**
  - **[PR #2210](https://github.com/netease-youdao/LobsterAI/pull/2210) & [PR #2213](https://github.com/netease-youdao/LobsterAI/pull/2213):** Prevented Mermaid syntax errors from leaking raw error SVGs into the document DOM. Implemented pre-validation using `mermaid.parse()` and proper cleanup of hidden containers.

- **Community Code Integration:**
  - **[PR #1459](https://github.com/netease-youdao/LobsterAI/pull/1459):** A community-authored feature (by `noransu`) for rich hover tooltips on skill selectors was finally merged after a two-month review. This enhances agent skill discoverability across the UI.

## 🔥 Community Hot Topics

- **Long-term Roadmap Discussion (Closed):** Issue **[#1462](https://github.com/netease-youdao/LobsterAI/issues/1462)** (3 comments) was the most active discussion. The user explicitly requested a formal multi-agent "manager/room" hierarchy and per-agent model binding, directly comparing LobsterAI favorably to Alibaba's Hiclaw on interaction quality but unfavorably on orchestration depth.
- **Critical Incident:** Issue **[#2214](https://github.com/netease-youdao/LobsterAI/issues/2214)** (0 comments) represents a high-stakes stability crisis that will likely dominate user discussions in the coming day. It is a 100% reproducible crash on Windows 11.
- No PRs or Issues attracted emoji reactions within this window.

## 🐞 Bugs & Stability

**Severity: Critical — Unresolved**
- **[Issue #2214](https://github.com/netease-youdao/LobsterAI/issues/2214):** The "Data Backup" function on the desktop client causes a complete hard freeze on Windows 11 24H2 when handling a database of reasonable size (71.6 MB, WAL mode). Users are forced to kill the process. No fix or assignment is yet visible.

**Severity: Moderate — Fixed**
- **[PR #2210](https://github.com/netease-youdao/LobsterAI/pull/2210) & [PR #2213](https://github.com/netease-youdao/LobsterAI/pull/2213):** Resolved Mermaid rendering crashes that leaked error SVGs into the document.
- **[PR #2207](https://github.com/netease-youdao/LobsterAI/pull/2207):** Fixed inaccurate subagent progress tracking in the Cowork sidebar.
- **[PR #2212](https://github.com/netease-youdao/LobsterAI/pull/2212):** Fixed the Skill Search popover closing prematurely on focus loss.

## 💡 Feature Requests & Roadmap Signals

The team's roadmap is heavily validated by today's activity. The "Plan Mode" workflow shipped in `v2026.6.26` is a direct architectural response to the community's request in Issue **[#1462](https://github.com/netease-youdao/LobsterAI/issues/1462)** for a "manager -> agent" room pattern.

Given the intense stabilization effort seen today, the next logical step is to close the remaining gap from that request: **per-agent model binding within a Cowork group**. This would allow users to route specialized tasks to specific models through their manager agent, unlocking the full potential of the multi-agent architecture.

## 🗣️ User Feedback Summary

- **Satisfaction Signals:** User `orion0608` (Issue #1462) praised LobsterAI's core interaction quality, stating it is superior to a competing commercial product (Alibaba Hiclaw). The resolution of the community PR #1459 also demonstrates responsiveness to user requests for better agent documentation.
- **Dissatisfaction / Pain Points:**
  - **Data Reliability:** User `woxinsj` (Issue #2214) is experiencing a catastrophic crash during data backup, eroding trust in application reliability for daily users, especially those with large datasets.
  - **Configuration Ceiling:** Power users feel constrained by the lack of individual model binding for agents, as expressed in #1462.
  - **UX Disparity:** There is a recurring theme of the polished core experience contrasting with rough edges in advanced features (orchestration/backup).

## ⏳ Backlog Watch

- **Resolved:**
  - **[PR #1459](https://github.com/netease-youdao/LobsterAI/pull/1459):** Merged. Clears a significant UX community contribution that had been open since April.
  - **[Issue #1462](https://github.com/netease-youdao/LobsterAI/issues/1462):** Closed. The underlying roadmap signal is now actively being worked on via the Cowork module.

- **Immediate Attention Required:**
  - **[Issue #2214](https://github.com/netease-youdao/LobsterAI/issues/2214) (Critical Bug):** This is the highest priority item for maintainers. An immediate hotfix or communication plan is required to address the backup workflow crash on Windows. This directly impacts user data security and application stability.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

```markdown
# Moltis Project Digest – 2026-06-27

## 1. Today's Overview
The Moltis project saw a very quiet day on June 27, with zero new issues and no releases cut. The only development activity was an update to a single open pull request from the previous day. Overall community engagement (issues, comments, reactions) was flat, indicating a low-activity period on the repository. Project health appears stable, though maintainers may be working on isolated branches rather than merging visibly.

## 2. Releases
No new releases were published today. The latest releases list remains empty, suggesting the project is between tagged versions or that development is being actively consolidated ahead of a future cut.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The sole active development item is **PR #1135** which remains open and was updated but not advanced to merge state.

## 4. Community Hot Topics
The only community-facing activity was **PR #1135**: *browser: optional auto-screenshot after each action* (0 comments, 0 reactions). Despite the lack of explicit discussion volume, this is clearly the focus item. The underlying need driving this PR is usability: chat client interfaces require visual feedback from browser agents to display a step-by-step timeline. Without automatic screenshots, users must manually instrument every action, which is a pain point for debugging and production visibility.
[GitHub Link: moltis-org/moltis PR #1135](https://github.com/moltis-org/moltis/pull/1135)

## 5. Bugs & Stability
No new bug reports, crashes, or regressions were filed today. The open issue tracker saw no activity, which suggests either strong stability or a temporary pause in community testing. No fix PRs are currently in flight.

## 6. Feature Requests & Roadmap Signals
**PR #1135** is the primary roadmap signal today. By introducing optional auto-screenshots at the single dispatch chokepoint (`BrowserManager::execute_action`), Moltis is prioritizing agent observability and client-side rendering of agent workflows. This feature strongly aligns with the industry-wide trend toward transparent agent reasoning loops and is a strong candidate for inclusion in the next minor release.

## 7. User Feedback Summary
No explicit user feedback (issues, comments, or reactions) was submitted today. However, the existence of PR #1135 implies an implicit user need: current browser agent tooling lacks a built-in mechanism for capturing visual state changes, forcing developers to build their own logging layers on top of the raw tool outputs.

## 8. Backlog Watch
Based on the provided 24-hour activity window, no long-unanswered issues or neglected pull requests were updated. The only open PR (#1135) was created on June 26 and saw a follow-up update today, indicating it is being actively tended by its author. No signals currently point to stale or abandoned work items.
```

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026‑06‑27

*Data snapshot: 28 issues updated (19 open, 9 closed) · 50 PRs updated (27 open, 23 merged/closed) · 1 new release*

---

## 1. Today's Overview

The project is in a period of exceptionally high velocity following the **v2.0.0-beta.1** release, which marks a deep architectural shift (the `agentscope 2.0` migration). With 50 PRs and 28 issues touched in the last 24 hours, the community is actively stress-testing the beta, filing detailed bug reports, and submitting code. Maintainers are responding rapidly to *stability* incidents—several critical blocker bugs filed yesterday already have fix PRs merged or open. At the same time, enterprise messaging (WeCom, DingTalk, Feishu, Slack) dominates community discussion, signalling where user energy is concentrated. The project is clearly in a `stabilise-the-breaking-changes` phase, but the high signal-to-noise ratio from contributors is a strong health indicator.

---

## 2. Releases

### v2.0.0-beta.1
**⚠️ Early beta — not for production use.** This is the first public build of the QwenPaw 2.0 line and comes with a clear breaking-change warning.

- **Core change:** Refactored agent layer (PR `#4846` family — migration from agentscope 1.x → 2.0).
- **Impact:** All five official plugins broke on this release (now fixed in PR `#5568`). Users coming from 1.x should expect instability.
- **Migration notes:** None published yet. The project is relying on early-adopter feedback to surface regressions.

**Recommendation:** Developers and integration testers should use this build to validate their toolchains. Production users should stay on the latest 1.1.12.post2 series until a stable 2.0.0 drops.

---

## 3. Project Progress

**23 PRs merged or closed.** Key milestones:

| Area | PR | Summary |
|---|---|---|
| **Desktop UX** | [`#5265`](https://github.com/agentscope-ai/QwenPaw/pull/5265) | Graceful shutdown endpoint + Tauri lifecycle fix |
| | [`#5153`](https://github.com/agentscope-ai/QwenPaw/pull/5153) | Replicate instant-window startup to pywebview client |
| | [`#5436`](https://github.com/agentscope-ai/QwenPaw/pull/5436) | Drag-and-drop file upload onto sender area |
| **Core / Backend** | [`#5440`](https://github.com/agentscope-ai/QwenPaw/pull/5440) | Post-merge agentscope 2.0 cleanup (−1493 lines, 3 fixes) |
| | [`#5297`](https://github.com/agentscope-ai/QwenPaw/pull/5297) | Batch test & batch delete models |
| | [`#5321`](https://github.com/agentscope-ai/QwenPaw/pull/5321) *(Under Review)* | **Scroll context manager** — durable SQLite history + recall REPL |
| **Channel** | [`#5577`](https://github.com/agentscope-ai/QwenPaw/pull/5577) *(Open)* | Opt-in reply aggregation (direct fix for `#5563`) |
| **Quality** | [`#5536`](https://github.com/agentscope-ai/QwenPaw/pull/5536) *(Open)* | Kill orphaned Chrome renderer processes on browser stop |
| | [`#5570`](https://github.com/agentscope-ai/QwenPaw/pull/5570) *(Open)* | Fix plugin dependency install storm + orphaned backends (`#5550`) |
| | [`#5549`](https://github.com/agentscope-ai/QwenPaw/pull/5549) *(Open)* | Sanitize nullable tool schemas (`#5543`) |

**Notable:** `#5321` (Scroll context manager) is a first-time contributor PR that adds a durable conversation store. If it lands, it will fundamentally change how long-running agent sessions are handled.

---

## 4. Community Hot Topics

*Based on comment volume, reactions, and emotional weight of threads.*

| Issue/PR | Type | Heat |
|---|---|---|
| [`#5563`](https://github.com/agentscope-ai/QwenPaw/issues/5563) — Aggregating multi-step agent responses | Feature | ⭐⭐⭐⭐ |
| [`#5550`](https://github.com/agentscope-ai/QwenPaw/issues/5550) — Remote SSH plugin dependency loop + orphan backends | Bug | ⭐⭐⭐⭐ |
| [`#5379`](https://github.com/agentscope-ai/QwenPaw/issues/5379) — Internal Server Error on fresh Python install | Bug (blocker) | ⭐⭐⭐ |
| [`#5564`](https://github.com/agentscope-ai/QwenPaw/issues/5564) — DingTalk @mention support in CLI/API | Feature | ⭐⭐⭐ |
| [`#5572`](https://github.com/agentscope-ai/QwenPaw/issues/5572) — Automatic model fallback on quota/failure | Feature | ⭐⭐⭐ |
| [`#5262`](https://github.com/agentscope-ai/QwenPaw/issues/5262) *(CLOSED)* — Built-in skills re-enable after each upgrade | Bug (recurring) | ⭐⭐⭐ |

**Underlying need analysis:**
1. **Multi-agent noise** (`#5563`) → Users are running real multi-step agents and hit UX wall. The fix PR `#5577` landed the same day.
2. **Desktop reliability** (`#5550`, `#5379`) → The 2.0 migration broke plugin dependency management and startup. Users on macOS desktop app are hitting fork-bomb-like resource exhaustion. The team reacted within hours with `#5570`.
3. **Enterprise integration** (`#5564`, `#5152`, `#5558`) → Explicit demand for DingTalk, WeCom, and Slack features. This is no longer a "nice-to-have" for the user base.
4. **Model reliability** (`#5572`, `#5573`, `#5328`) → DeepSeek V4 compatibility and auto-fallback are blocking production deployments.

---

## 5. Bugs & Stability

### Critical / Blocker
- **[`#5379`](https://github.com/agentscope-ai/QwenPaw/issues/5379)** — `Internal Server Error` on fresh install via pip. Users cannot reach the UI at all. **No fix PR yet.**
- **[`#5550`](https://github.com/agentscope-ai/QwenPaw/issues/5550)** — Remote SSH plugin spawns infinite `pip install` processes + leaves orphaned backends. **Fix exists** (`#5570`).
- **[`#5401`](https://github.com/agentscope-ai/QwenPaw/issues/5401)** *(CLOSED)* — Console white-screen on large tool-use sessions (`DataContent` type not handled). Fix merged.
- **[`#5573`](https://github.com/agentscope-ai/QwenPaw/issues/5573)** — DeepSeek V4 via OpenAI-compatible 3rd-party endpoints: streaming `reasoning_content` missing + nullable `type: null` in tool schemas. **Fix exists** (`#5549`).

### High
- [`#5554`](https://github.com/agentscope-ai/QwenPaw/issues/5554) — WeCom bot silently drops file messages; file saved but agent never triggered. **Fix exists** (`#5575`).
- [`#5539`](https://github.com/agentscope-ai/QwenPaw/issues/5539) — Heartbeat task has a hard-coded 120 s timeout, fails for complex workflows.
- [`#5328`](https://github.com/agentscope-ai/QwenPaw/issues/5328) — DeepSeek thinking mode agent freezes mid-think across all frontends (Web, Console, Tauri).

### Medium / UX
- [`#5480`](https://github.com/agentscope-ai/QwenPaw/issues/5480) *(CLOSED)* — Console long Markdown messages misrender until tab switch. Fix merged.
- [`#5561`](https://github.com/agentscope-ai/QwenPaw/issues/5561) — Feishu bot silently truncates messages beyond a length threshold.
- [`#5566`](https://github.com/agentscope-ai/QwenPaw/issues/5566) — Cron tasks cannot be silenced; empty agent replies still trigger DingTalk notifications.
- [`#5555`](https://github.com/agentscope-ai/QwenPaw/issues/5555) — Performance regression: "the new version is becoming very laggy."

### Low / Recurring
- [`#5262`](https://github.com/agentscope-ai/QwenPaw/issues/5262) *(CLOSED)* — Upgrade resets disabled built-in skills. Recurring bug user reported for the 3rd time.

---

## 6. Feature Requests & Roadmap Signals

| Issue | Feature | Likelihood |
|---|---|---|
| [`#5563`](https://github.com/agentscope-ai/QwenPaw/issues/5563) | Aggregate multi-step agent replies | **Very High** — PR `#5577` open |
| [`#5572`](https://github.com/agentscope-ai/QwenPaw/issues/5572) | Auto model fallback on quota/timeout | **High** — recurring pain point |
| [`#5558`](https://github.com/agentscope-ai/QwenPaw/issues/5558) | WeCom: allow sending files without text | **High** — PR `#5575` covers this |
| [`#5564`](https://github.com/agentscope-ai/QwenPaw/issues/5564) | DingTalk `@mention` in CLI/API | **Medium-High** — multi-agent workflow blocker |
| [`#5551`](https://github.com/agentscope-ai/QwenPaw/issues/5551) | Computer Use (CUA) support | **Medium** — trending topic, early signal |
| [`#4865`](https://github.com/agentscope-ai/QwenPaw/issues/4865) | Stream `write_file` content in Console UI | **Medium** — 3 reactions, pending attention |
| [`#5321`](https://github.com/agentscope-ai/QwenPaw/pull/5321) | Durable scroll context manager | **In review** — could be next release feature |

**Predictions for v2.1.0 / v2.0.0 stable:**
- Message aggregation (low risk, high impact).
- No-text debounce toggle for channels (already coded in `#5575`).
- Plugin installation lock fix (`#5570`).
- If the scroll context manager (`#5321`) passes review, it will be a differentiator for long-running agent memory.

---

## 7. User Feedback Summary

**Pain points voiced today:**
- *"Every update I have to manually disable built-in skills again. Third time reporting this."* (`#5262`)
- *"10-step agent = 10 spam messages in the chat. It's unusable."* (`#5563`)
- *"DeepSeek thinking mode just hangs and I have to manually interrupt."* (`#5328`)
- *"WeCom bot downloads my file but never says anything back."* (`#5554`)
- *"Fresh install today and all I get is Internal Server Error. No docs cover this."* (`#5379`)
- *"The new 2.0 version is getting slower and slower with use."* (`#5555`)

**Positive signals:**
- Community members are writing and sharing their own Skills (e.g. `#5567` — GitHub Issue Reporter Skill).
- A first-time contributor fixed a WeCom refresh bug (`#5574`).
- Detailed bug reports with full logs (`#5550`, `#5379`) show a technically engaged user base willing to help debug.

---

## 8. Backlog Watch

Issues or PRs that have been open for a significant time without a clear maintainer response or fix PR.

| Issue | Age | Status | Concern |
|---|---|---|---|
| [`#4865`](https://github.com/agentscope-ai/QwenPaw/issues/4865) — Stream `write_file` in Console | 26 days | Open, 3 comments, no maintainer assignment | UX regression for code-gen use cases. Has 2 👍 |
| [`#5328`](https://github.com/agentscope-ai/QwenPaw/issues/5328) — DeepSeek thinking freezes | 8 days | Open, 3 comments | Reported across all frontends. No fix PR. High severity. |
| [`#5474`](https://github.com/agentscope-ai/QwenPaw/issues/5474) *(CLOSED)* — Skill ZIP upload false success | 3 days | Closed | Fix status is unclear — user could still lose their namespace. |
| [`#5152`](https://github.com/agentscope-ai/QwenPaw/issues/5152) *(CLOSED)* — Slack channel support | 15 days | Closed without merge | Signals that Slack is not officially on the roadmap. |

**Maintainer attention needed:**
- **`#5328`** is a widespread user-facing bug (DeepSeek is a top model) and lacks a public fix path.
- **`#4865`** is a long-standing UX gap that would differentiate QwenPaw from raw OpenAI playgrounds.
- **`#5379`** is a fresh-install blocker — should be the highest priority unboxing issue.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-27

**Project Status: Highly active**

---

## 1. Today's Overview

ZeroClaw is firing on all cylinders following the **v0.8.2 release**. The community and core team updated 50 issues and 50 PRs in the last 24 hours, merging 11 PRs and closing 6 significant bugs. The project successfully shipped **A2A agent discovery** and a richer skills system, and has already pivoted heavily toward planning the **v0.8.3 milestone**. Project health looks strong—major chokepoints (Gemini OAuth, Shell tool autonomy, Telegram reply handling) were cleared, while ambitious governance and supply-chain security RFCs are gaining traction.

---

## 2. Releases

**[v0.8.2](https://github.com/zeroclaw-labs/zeroclaw/releases)** — *One new release today*

| Area | Change |
|---|---|
| **A2A Interop** | Agent-to-agent discovery and communication (opening a new front door for multi-agent fleets) |
| **Skills System** | User-configured extra registries, typed slash-command options |
| **Security Posture** | Hardening across plugins, channels, and runtime |
| **Breaking Changes** | *None explicitly specified in the provided release notes* |
| **Migration Notes** | *None specified* |

---

## 3. Project Progress

**11 PRs were merged/closed today**, alongside 6 issue closures. Key advances:

### ✅ Resolved Issues (Closed Today)
| Issue | Summary |
|---|---|
| [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) *(S1)* | **Memory emphasis bug** — system prompt overly prioritizing memories over current context; fixed for cron jobs |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) *(S1)* | **Gemini CLI OAuth** — was completely blocking authentication; resolved |
| [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) *(S1)* | **Shell tool autonomy** — calls refused at `full` autonomy; runtime dispatch fixed |
| [#8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047) *(S2)* | **ReadSkillTool path** — looked in `data_dir` instead of agent workspace |
| [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) *(S1)* | **Telegram reply handling** — bot ignored direct replies in groups with `mention_only=true` |

### 🔨 Active Feature Work (Open but Advancing)
- **MCP Security**: Regression tests for `mcp_bundles` enforcement ([#8370](https://github.com/zeroclaw-labs/zeroclaw/pull/8370))
- **Observability**: Rotating log-persistence mode ([#8307](https://github.com/zeroclaw-labs/zeroclaw/pull/8307)), herdr status integration ([#8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337))
- **ZeroCode UI**: Performance fix for long-session rendering ([#8330](https://github.com/zeroclaw-labs/zeroclaw/pull/8330)), agent rename flow ([#7954](https://github.com/zeroclaw-labs/zeroclaw/pull/7954))
- **Infrastructure**: Multi-database session backends ([#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)), offline pricing catalog ([#8380](https://github.com/zeroclaw-labs/zeroclaw/pull/8380)), Nix build repair ([#8336](https://github.com/zeroclaw-labs/zeroclaw/pull/8336))

---

## 4. Community Hot Topics

The most active discussions reflect deep engagement with the project's architectural future:

| # | Title | Comments | Detail |
|---|---|---|---|
| [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | **RFC: Work Lanes, Board Automation, Label Cleanup** | 11 | Governance RFC to reduce manual maintainer overhead; accepted and rolling out |
| [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) | **RFC: Supply Chain Signing** | 9 | High-stakes proposal: hardware PGP, SLSA provenance, hermetic builds. Currently **blocked** pending maintainer review |
| [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | **Bug: Memory Emphasis** | 7 *(Closed)* | Widely felt pain point in cron jobs; now resolved |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | **Bug: Gemini OAuth** | 4 *(2 👍)* | Workflow blocker that drew strong community concern; now fixed |
| [#8058](https://github.com/zeroclaw-labs/zeroclaw/issues/8058) | **CI: Cosign/SLSA/SBOM** | 4 | Pragmatic, release-only security hardening |

**Underlying community need:** Users are pushing hard for **enterprise-grade security** (supply chain, signing) and **better governance tooling**, signaling growing deployment maturity.

---

## 5. Bugs & Stability

### ✅ Recently Resolved (High Severity)
| Severity | Issue | Status |
|---|---|---|
| S1 – Workflow Blocked | [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) Gemini OAuth | ✅ Closed |
| S1 – Workflow Blocked | [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) Shell tool refusal | ✅ Closed |
| S1 – Workflow Blocked | [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) Telegram replies | ✅ Closed |
| S2 – Degraded | [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) Memory emphasis | ✅ Closed |
| S2 – Degraded | [#8047](https://github.com/zeroclaw-labs/zeroclaw/issues/8047) ReadSkillTool path | ✅ Closed |

### 🔴 Critical Open Bugs (Ranked by Severity)
| Severity | Issue | Impact | Fix Status |
|---|---|---|---|
| **S2** – Security No-op | [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) — `mcp_bundles` never enforced | Silent security isolation failure | Fix merged; regression test in review ([#8370](https://github.com/zeroclaw-labs/zeroclaw/pull/8370)) |
| **S2** – Data Loss | [#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) — Translations leak-repair stale entries | Narrow-trigger silent data-loss | Needs investigation |
| **S2** – Config Confusion | [#8366](https://github.com/zeroclaw-labs/zeroclaw/issues/8366) — Heartbeat reads wrong directory | Degraded cron/task behavior | New report; no fix yet |
| **S2** – Channel Parity | [#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360) — Telegram prompt caching broken | Performance regression on Telegram | Open since May 4 |
| **S2** – UX | [#7815](https://github.com/zeroclaw-labs/zeroclaw/issues/7815) — ZeroCode config source invisible | Editing confusion in TUI | Open |
| **S2** – UX | [#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) — macOS keybindings misleading | Friction for new macOS users | Open |

---

## 6. Feature Requests & Roadmap Signals

### 📍 Confirmed v0.8.3 Roadmap Items
The following dedicated trackers define the next milestone:
- [Config-driven runtime policy & routing](https://github.com/zeroclaw-labs/zeroclaw/issues/8363)
- [Channel adapter parity & interaction](https://github.com/zeroclaw-labs/zeroclaw/issues/8362)
- [Provider & native-tool message serialization](https://github.com/zeroclaw-labs/zeroclaw/issues/8360)
- [Observability, CI, Docs, Dependencies](https://github.com/zeroclaw-labs/zeroclaw/issues/8073)
- [Gateway, Web, ZeroCode, Onboarding](https://github.com/zeroclaw-labs/zeroclaw/issues/8070)

### 🔮 Likely v0.8.3 Candidates (Based on Momentum)
| Feature | Evidence |
|---|---|
| **Goal Mode** ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) | RFC for durable bounded autonomous sessions; natural fit for runtime tracker |
| **Discord Thread Mode** ([#7849](https://github.com/zeroclaw-labs/zeroclaw/issues/7849)) | Aligns directly with channel parity push |
| **WhatsApp Passive Context** ([#8379](https://github.com/zeroclaw-labs/zeroclaw/issues/8379)) | Continuation of channel UX theme |
| **Onboard Crate** ([#8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033)) | Two-path onboard tree (LLM + deterministic) nearing completion |

### 🔮 Longer-Term / Stretch
| Feature | Notes |
|---|---|
| **Supply Chain Signing** ([#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)) | Blocked; may slip to v0.9.0 |
| **SkillForge decision** ([#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309)) | Orphaned since Feb; community asking for wire-up or removal |
| **ACP Bridge Pairing** ([#6754](https://github.com/zeroclaw-labs/zeroclaw/issues/6754)) | Accepted but not yet in v0.8.3 trackers |

---

## 7. User Feedback Summary

| Theme | Verbatim Signal | Sentiment |
|---|---|---|
| **Security Sophistication** | *"mcp_bundles is parsed and shown in Config but never enforced at runtime"* (#7733) | Users are stress-testing the security model and expect strict enforcement |
| **Channel Consistency** | *"Prompt Caching does not work with telegram"* (#6360); *"in Telegram group bot ignores replies"* (#5866, *fixed*) | Feature parity between CLI & channels is the #1 UX pain point |
| **Configuration UX** | *"ZeroCode Config does not show which config source"* (#7815); *"keybindings are misleading… especially on macOS"* (#7800) | New users hit friction in ZeroCode TUI |
| **Feature Completeness** | *"SkillForge is wired to nothing… decide whether to finish wiring or remove"* (#8309) | Users notice orphaned features and demand clarity |
| **Cron/Memory Reliability** | *"gives too much value/… to the memories and more to the current prompt"* (#5844, *fixed*) | High visibility cron behavior issue, now resolved |
| **Pricing Awareness** | Two concurrent PRs for pricing catalogs ([#8233](https://github.com/zeroclaw-labs/zeroclaw/pull/8233), [#8380](https://github.com/zeroclaw-labs/zeroclaw/pull/8380)) | Strong operator demand for cost visibility and budget control |

---

## 8. Backlog Watch

Items needing maintainer attention to unblock community progress:

| Priority | Issue | Reason for Watch |
|---|---|---|
| 🔴 **High** | [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) — RFC: Supply Chain Signing | **Blocked / Needs maintainer review**. Top security queue item awaiting a go/no-go decision |
| 🔴 **High** | [#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309) — SkillForge orphanage | **Blocked / Needs maintainer review**. Community needs a clear integrate-or-deprecate decision |
| 🟡 **Medium** | [#6754](https://github.com/zeroclaw-labs/zeroclaw/issues/6754) — ACP Bridge Pairing | **Accepted, flagged `no-stale`** since May 18 but absent from v0.8.3 trackers |
| 🟡 **Medium** | [#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360) — Telegram Prompt Caching | Open since **May 4**. Not blocked, but an increasingly notable gap in channel parity |
| 🟡 **Medium** | [#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642) — GenAI span capture | Accepted follow-up awaiting upstream contribution; no action for 6+ weeks |
| 🟢 **Lower** | [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) — Telegram reply fix | ✅ **Closed** — monitored to ensure no regression |

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*