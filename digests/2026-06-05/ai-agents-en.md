# OpenClaw Ecosystem Digest 2026-06-05

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-05 03:29 UTC

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

## OpenClaw Project Digest
**Date:** June 5, 2026
**Data Source:** GitHub (openclaw/openclaw)

---

### 1. Today's Overview
The OpenClaw project experienced a burst of intense activity in the 24 hours leading up to this digest, with **500 Issues and 500 Pull Requests** updated. This elevated volume is almost entirely driven by the community's response to regressions introduced in the **2026.6.1 release**, particularly surrounding the SQLite session migration and the new Codex default runtime. **No new releases were published today**, signaling a strategic pause to prioritize stabilization and bug fixing over feature velocity. The project is currently under significant operational strain, but is supported by an exceptionally engaged and technically proficient community that is actively contributing targeted fix PRs.

---

### 2. Releases
**No new releases were published today.** The latest stable version remains **OpenClaw 2026.6.1**.

---

### 3. Project Progress
**103 Pull Requests were merged or closed** in the last 24 hours. The project's progress is heavily weighted toward stabilizing the current release:

- **High-Impact Fixes in Queue:**
  - Mattermost slash command initialization ([#90389](https://github.com/openclaw/openclaw/pull/90389), for #68113)
  - OpenAI ChatGPT Responses stream content-type parsing ([#90399](https://github.com/openclaw/openclaw/pull/90399))
  - MiniMax M3 thinking wrapper exemption ([#90138](https://github.com/openclaw/openclaw/pull/90138))
  - Stale session model route clearing ([#90514](https://github.com/openclaw/openclaw/pull/90514))
  - Discord multi-account startup priority ([#89744](https://github.com/openclaw/openclaw/pull/89744))

- **Community-Featured Fixes:**
  - Edit tool fuzzy matching rewrite ([#90060](https://github.com/openclaw/openclaw/pull/90060))
  - QQBot reasoning block sanitization ([#90132](https://github.com/openclaw/openclaw/pull/90132))
  - Agent-run error persistence in chat history ([#89483](https://github.com/openclaw/openclaw/pull/89483))
  - Skill workshop proposal reconciliation ([#90421](https://github.com/openclaw/openclaw/pull/90421), [#90493](https://github.com/openclaw/openclaw/pull/90493))

- **Infrastructure & Features Merged:**
  - QMD query rerank toggle ([#90304](https://github.com/openclaw/openclaw/pull/90304))
  - Cron-driven reply payload origin tagging ([#90527](https://github.com/openclaw/openclaw/pull/90527))
  - Config editor local schema generation ([#89992](https://github.com/openclaw/openclaw/pull/89992))
  - Codex runtime snapshotting ([#90411](https://github.com/openclaw/openclaw/pull/90411))

---

### 4. Community Hot Topics
The most active discussions reveal the community's primary concerns:

- **Data Integrity Fears:** [#90072](https://github.com/openclaw/openclaw/issues/90072) – 44 of 45 cron jobs silently wiped during the SQLite migration (5 comments, 3 👍). Users are demanding safe, non-destructive upgrade paths.
- **Model API Blockers:** [#90083](https://github.com/openclaw/openclaw/issues/90083) – OpenAI ChatGPT transport fails completely for GPT-5.4/5.5 (11 comments, 3 👍). A related issue, [#90093](https://github.com/openclaw/openclaw/issues/90093) (7 comments, 2 👍), reveals encrypted reasoning breaking multi-turn conversations. Users need immediate compatibility with upstream provider API changes.
- **Core Channel Reliability:**
  - [#72808](https://github.com/openclaw/openclaw/issues/72808) – Silent Slack disconnection (20 comments, 3 👍, Diamond Lobster).
  - [#87307](https://github.com/openclaw/openclaw/issues/87307) – Matrix thread replies sent as normal messages (13 comments, P1).
  - [#68113](https://github.com/openclaw/openclaw/issues/68113) – Mattermost permanent 503 error (11 comments, 3 👍, P1, Diamond Lobster).
- **Context Management:** [#63216](https://github.com/openclaw/openclaw/issues/63216) – Repeated hard context-overflow resets (11 comments, 3 👍, Platinum Hermit) and [#90082](https://github.com/openclaw/openclaw/issues/90082) – Active-memory circuit breaker polluting session context (5 comments, 2 👍, P1).

**Underlying Needs Analysis:** The community's top priority is **stable, non-destructive upgrades** and **bullet-proof core messaging integration**. There is zero tolerance for silent data loss and a strong expectation that major platform channels (Slack, Mattermost, Matrix, Discord) are treated as critical infrastructure. Users also demand rapid adaptation to upstream AI model API changes without breaking existing sessions.

---

### 5. Bugs & Stability

**Critical (Data Loss / Complete Feature Breakage):**
- [#90072](https://github.com/openclaw/openclaw/issues/90072): Cron state wiped during SQLite migration (v2026.6.1). No fix PR in batch.
- [#90083](https://github.com/openclaw/openclaw/issues/90083): OpenAI ChatGPT transport fails with `invalid_provider_content_type`. Fix PR [#90399](https://github.com/openclaw/openclaw/pull/90399) in review.
- [#90093](https://github.com/openclaw/openclaw/issues/90093): Native replay sends encrypted reasoning, breaking next turn. No fix PR in batch.
- [#90082](https://github.com/openclaw/openclaw/issues/90082): Active-memory circuit breaker fallback pollutes main session context. No fix PR in batch.
- [#72808](https://github.com/openclaw/openclaw/issues/72808): Silent Slack connection loss. Diamond Lobster rating.

**Severe Regressions (Core Feature Breakage):**
- [#68113](https://github.com/openclaw/openclaw/issues/68113): Mattermost slash commands return permanent 503. Fix PR [#90389](https://github.com/openclaw/openclaw/pull/90389) in review.
- [#87307](https://github.com/openclaw/openclaw/issues/87307): Matrix thread replies sent as normal messages (P1).
- [#88929](https://github.com/openclaw/openclaw/issues/88929): Feishu streaming card truncated to last character (Bug).
- [#63216](https://github.com/openclaw/openclaw/issues/63216): Repeated hard context-overflow resets (P1, Platinum Hermit).
- [#65161](https://github.com/openclaw/openclaw/issues/65161): Heartbeat isolated mode stalling and mislabeling (Diamond Lobster).
- [#67777](https://github.com/openclaw/openclaw/issues/67777): Subagent completion delivery can be lost (P1, Diamond Lobster).

**Security Concerns:**
- [#65624](https://github.com/openclaw/openclaw/issues/65624): Mattermost slash commands expose reusable cleartext callback tokens (P1, High CVSS).
- [#64046](https://github.com/openclaw/openclaw/issues/64046): Sensitive data (API keys/tokens) stored and logged in plain text (P1, Diamond Lobster).

---

### 6. Feature Requests & Roadmap Signals
While the roadmap is currently reactive to stability issues, several persistent feature signals are gaining traction:

- **Data Governance ([#64046](https://github.com/openclaw/openclaw/issues/64046)):** Strong community demand for masking API keys and secrets in logs, configuration files, and the Control UI.
- **Embedding Resilience ([#63990](https://github.com/openclaw/openclaw/issues/63990)):** A request for multi-index embedding memory to allow resilient failover between provider models without corrupting vector spaces.
- **Plugin SDK Growth ([#71736](https://github.com/openclaw/openclaw/issues/71736)):** An RFC for Control UI plugin contribution slots, which would unlock significant ecosystem extensibility, remains pending a product decision.
- **Anthropic Advisor Tool ([#63930](https://github.com/openclaw/openclaw/issues/63930)):** Support for Anthropic's beta server-side advisor tool.

**Prediction for Next Version:** The immediate next release will be a **dedicated stabilization release** (likely 2026.6.2 or 2026.7.x). The focus will be on: hardening the SQLite migration path (rollbacks, state backup, idempotency), resolving the blocking channel regressions (Mattermost, Matrix, Discord), and addressing the accumulation of high-severity context management bugs. Deeper architectural features (multi-index memory, Control UI plugin slots) will likely be deferred to a Q3 feature cycle.

---

### 7. User Feedback Summary
Overall user sentiment is one of **deep engagement mixed with significant frustration**.

**Dissatisfaction Drivers:**
- **Upgrade Risk:** Silent cron data loss ([#90072](https://github.com/openclaw/openclaw/issues/90072)) and blocking transport errors ([#90083](https://github.com/openclaw/openclaw/issues/90083)) have made users cautious about upgrading immediately.
- **Stalled Regression Fixes:** The Mattermost 503 bug ([#68113](https://github.com/openclaw/openclaw/issues/68113)) has persisted as P1 since April 17, eroding trust in channel-specific SLAs.
- **Silent Failures:** Lost Slack connections ([#72808](https://github.com/openclaw/openclaw/issues/72808)) and swallowed heartbeat replies ([#64810](https://github.com/openclaw/openclaw/issues/64810)) frustrate users who rely on the bot being responsive.

**Satisfaction Drivers:**
- **Triage Maturity:** The elaborate rating system (Diamond Lobster, Platinum Hermit, etc.) demonstrates a shared, professional understanding of operational severity between maintainers and users.
- **Fix Velocity:** The community collaborates effectively with maintainers to produce rapid, targeted fix PRs ([#90389](https://github.com/openclaw/openclaw/pull/90389), [#90399](https://github.com/openclaw/openclaw/pull/90399), [#90138](https://github.com/openclaw/openclaw/pull/90138)). This "many hands" approach is highly valued.

**Common Themes:** Users overwhelmingly prefer **stability over new features**. They demand **non-destructive upgrades** and **explicit error messages** over silent failures. The project's ability to attract high-quality community debug reports and fix PRs is a significant asset.

---

### 8. Backlog Watch
Several critical, long-standing issues remain stuck in the review/decision pipeline, posing a risk of accumulating technical debt and maintainer burnout:

- [#65161](https://github.com/openclaw/openclaw/issues/65161) **Heartbeat Isolated Mode Regressions** (Opened Apr 12, Diamond Lobster): Stalled cadence and mislabeled `exec-events`. Tags: `needs-maintainer-review`, `needs-product-decision`.
- [#63216](https://github.com/openclaw/openclaw/issues/63216) **Repeated Hard Resets** (Opened Apr 8, Platinum Hermit): Critical context management bug destroying session state. Tags: `needs-maintainer-review`, `needs-product-decision`, `needs-live-repro`.
- [#64046](https://github.com/openclaw/openclaw/issues/64046) **Sensitive Data Masking** (Opened Apr 10, Diamond Lobster): Security and compliance requirement. Tags: `needs-maintainer-review`, `needs-product-decision`, `needs-security-review`.
- [#69066](https://github.com/openclaw/openclaw/issues/69066) **Service Identity RFC** (Opened Apr 19, Diamond Lobster): Foundational gateway authentication architecture. Tags: `needs-maintainer-review`, `needs-product-decision`, `needs-security-review`.
- [#67777](https://github.com/openclaw/openclaw/issues/67777) **Subagent Completion Delivery Loss** (Opened Apr 16, P1, Diamond Lobster): Core reliability issue for agent orchestration. Tags: `needs-maintainer-review`, `needs-product-decision`.
- [#71736](https://github.com/openclaw/openclaw/issues/71736) **Control UI Plugin Slots RFC** (Opened Apr 25): Blocks UI ecosystem extensibility. Tags: `needs-maintainer-review`, `needs-product-decision`.
- [#60612](https://github.com/openclaw/openclaw/issues/60612) **Doctor Warns About NVM Node Path** (Opened Apr 4, Diamond Lobster): Persistent UX friction that cannot be resolved by the user. Tags: `needs-maintainer-review`, `needs-product-decision`.

**Risk:** The accumulation of unaddressed high-severity items in the backlog—many originating from April—creates a blind spot in the project's otherwise rapid triage system and may erode community trust if not addressed with clear timelines in the upcoming stabilization cycle.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison: Personal AI Agent Open Source Landscape
**Date:** June 5, 2026  
**Analyst:** Senior Analyst, AI Agent Open-Source Ecosystem

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem is experiencing a high-stakes transition from prototype to production runtime. October's feature velocity is giving way to June's stabilization sprint, with most major projects firefighting regressions introduced by recent architectural overhauls. A clear stratification is emerging: foundational runtime projects (OpenClaw, IronClaw) are battling the scaling pains of becoming agent operating systems, while specialized projects (ZeroClaw, NanoClaw, Moltis) are carving deep niches in coding, channel resilience, and voice interaction. The overarching trend is the market demanding production-grade reliability—durable state management, enterprise identity governance, observable agent loops, and bulletproof cost controls—over raw feature expansion. The Rust-based projects (IronClaw, ZeroClaw) show the strongest engineering discipline signals, while the largest community project (OpenClaw) demonstrates the most stress under its own success.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Latest Release | Health Signal |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 2026.6.1 | High Trauma / High Community Response |
| **IronClaw** | 41 | 50 | N/A (Pre-Reborn GA) | High Discipline / High Velocity |
| **ZeroClaw** | 33 | 50 | N/A (v0.8.0 Track) | High Feature Churn / Consolidating |
| **Hermes Agent** | 50 | 50 | v0.15.1 | Critical Regressions / Reactive |
| **NanoBot** | 6 | 74 | N/A | Strong Maturation / Testing-First |
| **CoPaw** | 32 | 33 | v1.1.11-beta.1 | Rapid Iteration / Hotfix Cycle |
| **PicoClaw** | 7 | 22 | v0.2.9-nightly | Effective Targeted Hotfixing |
| **LobsterAI** | 0 | 16 | v2026.5.28 | Backlog Cleaning / Stabilizing |
| **NanoClaw** | 1 | 8 | N/A | Consolidating / Structural Fixes |
| **Moltis** | 2 | 3 | N/A | Steady Niche Growth |
| **NullClaw** | 0 | 0 | N/A | Dormant |
| **TinyClaw** | 0 | 0 | N/A | Dormant |
| **ZeptoClaw** | 0 | 0 | N/A | Dormant |

*Note: The 500/500 OpenClaw figures are anomalous and represent the largest single-day regression spike observed across any project. High issue counts generally correlate with community size but also structural instability.*

---

## 3. OpenClaw's Position

**Advantages:**
- **Unmatched Ecosystem Breadth:** OpenClaw remains the defacto reference implementation with the widest channel integration surface (Slack, Discord, Matrix, Mattermost, Feishu, QQ). No project comes close to its plugin library and community-contributed skill workshop.
- **Community Self-Healing Capacity:** The "Diamond Lobster" rating system and 500 PR/day response velocity demonstrate a uniquely self-organizing contributor base that can generate targeted fix PRs within hours of a regression report.
- **Triage Maturity:** Despite the numerical noise, the community has developed sophisticated operational severity language (Platinum Hermit, Diamond Lobster) that enables rapid prioritization.

**Disadvantages:**
- **Integration Complexity & Fragility:** The 2026.6.1 release's SQLite migration silently wiped cron state (#90072) and broke major transport integrations (#90083). This erodes the trust that its ecosystem size demands.
- **Reactive Engineering Profile:** Unlike IronClaw's proactive decomposition trackers (#4470) or ZeroClaw's structured observability RFCs (#7232), OpenClaw's engineering is largely event-driven. Technical debt is accumulating in its "Blocked" backlog (items from April still unresolved).
- **Community Size Comparison:** OpenClaw's community is an order of magnitude larger in activity than any peer, but the signal-to-noise ratio is lower. IronClaw and ZeroClaw receive higher engineering quality scores per capita.

**Technical Approach:** Plugin-centric monolith with a wide surface area. Its transition to a Codex runtime is causing friction. By contrast, IronClaw (Rust, modular crates) and ZeroClaw (Rust, coding-focused runtime) pursue stricter architectural discipline.

---

## 4. Shared Technical Focus Areas

| Technical Area | Affected Projects | Specific Needs |
|---|---|---|
| **Resilient State & Data Migration** | OpenClaw, CoPaw, NanoClaw, PicoClaw | Non-destructive SQLite/SQL migrations, state rollback paths, compaction that respects model configurations |
| **Provider API Adaptation** | OpenClaw, CoPaw, NanoBot, PicoClaw, Hermes | Rapid response to OpenAI transport changes, tool call ID normalization for non-OpenAI providers, model ID updates |
| **Multi-Agent Orchestration** | IronClaw, ZeroClaw, CoPaw, OpenClaw | Durable subagent completion delivery, A2A protocol support, agent interruption/circuit-breaking mechanisms |
| **Channel Platform Hardening** | OpenClaw, NanoClaw, Hermes, CoPaw, Moltis, LobsterAI | WhatsApp LID migration compliance, Signal first-message handling, Slack/Mattermost thread reliability, Telegram streaming UX |
| **Enterprise & Security Compliance** | IronClaw, ZeroClaw, NanoBot, OpenClaw, Hermes | Azure AAD/OAuth identity resolution, credential masking in logs, role-based gateway access, TLS CA cert support |
| **Observability & Debugging** | ZeroClaw, IronClaw, OpenClaw, CoPaw | Structured event telemetry, agent loop failure logging, token/context usage visibility, latency breakdowns |
| **MCP Infrastructure** | CoPaw, LobsterAI, NanoBot, ZeroClaw | Tool name validation (regex compatibility), SSRF prevention, startup optimization, streamable HTTP transport |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw / ZeroClaw | NanoBot / CoPaw | Moltis |
|---|---|---|---|---|
| **Target User** | General power users, bot operators | Enterprise devs, platform engineers | Full-stack web users, MCP consumers | Voice-first mobile users |
| **Technical Stack** | Community monolith (diverse) | Rust (safety, low resource) | Python (rich ecosystem, rapid dev) | Unspecified (lightweight) |
| **Feature Focus** | Ecosystem breadth, plugins | Agent runtime, durability, observability | Web UI, enterprise auth, skills | Voice, local STT, SMS/LINE |
| **Maturity Model** | Reactive, community-driven | Proactive, structured decomposition | Testing-first, hook lifecycle | Steady, niche consolidation |
| **Risk Profile** | High surface area, regression pron | High discipline, slower to new features | Good pace, secure foundations | Slow, limited community |
| **Desktop Strategy** | Heavy desktop integration | TUI + coding focus (ZeroClaw) | Desktop shell in progress (NanoBot #4195), Tauri (CoPaw) | No desktop signal |

**Key Strategic Insight:** IronClaw and ZeroClaw represent the "agent operating system" school—minimalist runtime, strong safety guarantees, structured observability. OpenClaw represents the "application platform" school—maximize integrations, let the community handle diversity. Both strategies are valid, but the platform school currently bears more operational risk.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity & Mature Engineering**
- **IronClaw, NanoBot, ZeroClaw**
- *Signals:* Proactive decomposition tracking (#4470), deterministic test harnesses (#4193), structured RFCs (#7232), clear release trackers (#7112). These projects are investing in engineering infrastructure that scales without proportional increases in burn rate.

**Tier 2: High Activity / Community-Driven**
- **OpenClaw, Hermes Agent, CoPaw**
- *Signals:* Massive contributor volume, rapid bug-to-fix cycles, but higher noise floor. These projects demonstrate the web's "many eyes" principle but suffer from periodic stability crises. OpenClaw's backlog of unresolved April issues is a warning signal.

**Tier 3: Responsive Niche / Consolidation**
- **PicoClaw, NanoClaw, LobsterAI, Moltis**
- *Signals:* Smaller teams, deep focus on specific channel or platform stability (WhatsApp LID, Telegram streaming), rapid hotfix sprints. Healthiest per-contributor impact ratios.

**Tier 4: Dormant**
- **NullClaw, TinyClaw, ZeptoClaw**
- *Status:* No code activity in 24 hours. Project retention risk for these repos.

---

## 7. Trend Signals

**1. From Chatbot to Agent Operating System**
The industry is commoditizing chat and racing to build durable multi-agent runtimes. IronClaw's subagent spawn/durability cycle, ZeroClaw's A2A protocol investment, and CoPaw's ephemeral sub-agent tool (#4806) indicate that the next competitive differentiator is not "can it chat" but "can it orchestrate reliably." Developers need to invest in state management, idempotency, and interruption logic.

**2. Production Cost Consciousness**
Token drain bugs (PicoClaw #3012), runaway agent loops (CoPaw #4967), and cache efficiency concerns (CoPaw #3891) reveal that API cost management is a first-class UX requirement, not an afterthought. Circuit breakers, budget tracking, and user-facing cost dashboards will be table stakes for production deployments in Q3.

**3. Desktop is the New Frontier—With Growing Pains**
Hermes' boot loop saga (#39505), ZeroClaw's TUI freeze (#7125), and NanoBot's desktop shell PR (#4195) confirm that every major project is investing heavily in native desktop clients. However, the volume of desktop-specific regressions (Windows shell bugs, Mac installer fails, sandbox cleanup issues) indicates this remains a high-risk engineering investment. Cross-platform CI/CD and sandboxing standards are urgently needed.

**4. The MCP Standardization Struggle**
MCP has won universal adoption, but its operational friction is the dominant integration pain point. Tool name rejection by provider APIs (CoPaw #4958), SSRF prevention (NanoBot #4123), and cold-start latency (LobsterAI #2091) dominate commit messages. The ecosystem desperately needs standardized MCP tool validation and registry hygiene before the next layer of agent-to-agent protocols can scale.

**5. Enterprise Compliance Bottleneck**
Azure AAD support (NanoBot #4126), identity resolver standardization (IronClaw #4461), RBAC for gateways (Hermes #527), credential masking (OpenClaw #64046), and TLS CA certs (ZeroClaw #5797) are explicitly blocking enterprise adoption. Projects that solve identity and security compliance in the next quarter will capture institutional deployments. The data overwhelmingly shows enterprise procurement requirements driving engineering priorities across the entire ecosystem.

**6. Observability as Architectual Requirement**
Operators—not just end users—are emerging as a key audience. ZeroClaw's structured observability RFC (#7232), IronClaw's agent loop trace logging gap (#4427), and CoPaw's context usage UI demands signal that "making it work" is no longer sufficient. The market is moving toward "making it observable and debuggable in production."

---

*Report generated from 24-hour digest data (2026-06-05). Analysis reflects cross-project synthesis for technical decision-makers evaluating the personal AI agent open-source landscape.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the structured NanoBot project digest for June 5, 2026.

---

## NanoBot Project Digest — 2026-06-05

**1. Today's Overview**
Activity surged on the pull request front, with 74 PRs updated in the last 24 hours—60 of which were either merged or closed. This indicates a heavy cycle of code hardening, test expansion, and merging of long-running feature branches. Issue traffic remained quiet at 6 total updates, most of which were closed or clarified quickly. No new releases were published today, confirming focus is on internal stability and architectural improvements rather than packaging.

**2. Releases**
No new versions were published today.

**3. Project Progress**
Of the 60 merged/closed pull requests today, several key themes emerged:
- **Lifecycle & Core Architecture:** The agent hook lifecycle was introduced ([#4176](https://github.com/HKUDS/nanobot/pull/4176)), alongside a refactor of the capture state to rely on authoritative run-level hook snapshots ([#4194](https://github.com/HKUDS/nanobot/pull/4194)).
- **User-Facing Features:** The WebUI now supports a "fork-from-here" action on historical user messages ([#4163](https://github.com/HKUDS/nanobot/pull/4163)). A large Chinese-authored PR was merged adding sensitive info desensitization, dual-phase Dream rewrites, and atomic writes ([#4186](https://github.com/HKUDS/nanobot/pull/4186)).
- **Enterprise Providers:** Azure AAD-based authentication is now fully supported ([#4126](https://github.com/HKUDS/nanobot/pull/4126)), resolving a blocking policy issue for enterprise deployments. OpenAI-compatible tool call IDs are now properly preserved for APIs like GLM-4.7 and Kimi 2.6 ([#3984](https://github.com/HKUDS/nanobot/pull/3984)).
- **CLI & Tooling:** The WebUI CLI installer was fixed to fall back to `uv pip` when `pip` is not a module ([#4164](https://github.com/HKUDS/nanobot/pull/4164)).
- **Testing & CI:** Massive deterministic test coverage landed, including memory lifecycle harnesses ([#4193](https://github.com/HKUDS/nanobot/pull/4193)), scripted agent runner harnesses ([#3982](https://github.com/HKUDS/nanobot/pull/3982)), and a sweeping improvement to remove timing-based waits from unit tests ([#4189](https://github.com/HKUDS/nanobot/pull/4189)).

**4. Community Hot Topics**
- **[#912](https://github.com/HKUDS/nanobot/issues/912) [Stale] Feat: Support Task-Specific Model Configuration** — With 3 👍 and 4 comments, this is the highest-voted open feature request. Users are seeking separate model configurations for conversational, tool-use, and browser-use tasks. While marked as stale, the recurring interest suggests it remains a critical user need.
- **[#4195](https://github.com/HKUDS/nanobot/pull/4195) feat(desktop): polish desktop shell** — An open PR signaling the project’s first native desktop surface, with high internal activity and implications for the broader WebUI shared surfaces.
- **[#11121](https://github.com/HKUDS/nanobot/issues/1121) Fallback model not triggered on LLM timeout** — An issue that was closed today. The failure of fallback models to fire on ServiceUnavailableErrors was a key stability concern, and its closure (alongside the general stability PRs) is likely relieving user trust friction.

**5. Bugs & Stability**
No critical regressions or new high-severity bugs were reported today.
- **Recently Fixed:**
  - *Azure API Key Policy Blocking Deployments* — Closed by [#4125](https://github.com/HKUDS/nanobot/issues/4125) and resolved via merged PR [#4126](https://github.com/HKUDS/nanobot/pull/4126).
  - *WebUI `uv tool` Install Crash* — Closed by [#4158](https://github.com/HKUDS/nanobot/issues/4158) and resolved via merged PR [#4164](https://github.com/HKUDS/nanobot/pull/4164).
  - *Tool Call ID Corruption for Non-OpenAI APIs* — Resolved via merged PR [#3984](https://github.com/HKUDS/nanobot/pull/3984).
- **In Progress:**
  - *Security Hardening:* PRs are open for blocking symlink workspace escapes ([#4119](https://github.com/HKUDS/nanobot/pull/4119)), rejecting unsafe MCP HTTP URLs before probing ([#4123](https://github.com/HKUDS/nanobot/pull/4123)), and isolating read-only filesystem roots from write paths ([#4053](https://github.com/HKUDS/nanobot/pull/4053)).
  - *Channel Pairing:* A fix for denied sender DM pairing in Weixin and Telegram is currently under review ([#4197](https://github.com/HKUDS/nanobot/pull/4197)).
  - *Tool Validation:* Tool call strictness is being increased to reject near-miss names and non-object arguments rather than silently executing them ([#4190](https://github.com/HKUDS/nanobot/pull/4190)).

**6. Feature Requests & Roadmap Signals**
- **Provider Expansion:**
  - A request for Volcano Engine image generation support ([#4196](https://github.com/HKUDS/nanobot/issues/4196)) was closed. Users seeking this may need to await broader MaaS support.
  - The Azure AAD PR ([#4126](https://github.com/HKUDS/nanobot/pull/4126)) is a strong signal for enterprise identity compliance.
- **Desktop Platform:** The open desktop shell PR ([#4195](https://github.com/HKUDS/nanobot/pull/4195)) is the clearest roadmap signal for a native application layer.
- **Agent Orchestration:** The merged agent hook lifecycle ([#4176](https://github.com/HKUDS/nanobot/pull/4176)) and the open PR for subagent MCP tool inheritance ([#4192](https://github.com/HKUDS/nanobot/pull/4192)) signal that multi-agent orchestration and observability are priority items for the upcoming minor version cycle.
- **WebUI UX:** A "New Chat" keyboard shortcut (`Cmd/Ctrl+Shift+O`) was introduced today ([#4178](https://github.com/HKUDS/nanobot/issues/4178)). The new "fork-from-here" feature was also merged.

**7. User Feedback Summary**
- **Satisfaction Indicators:**
  - High maintainer responsiveness: The Azure AAD block and the `uv tool` CLI crash were identified, resolved, and merged within a short window.
  - The steady stream of test harnesses and lifecycle hooks suggests heavy investment in reliability that directly serves users running production agents.
- **Pain Points:**
  - *Provider Lock-In:* Users relying on strict Azure policies had no path forward without AAD support (now resolved).
  - *Model Flexibility:* The persistent demand for task-specific model configuration ([#912](https://github.com/HKUDS/nanobot/issues/912)) remains the most vocal unmet need in the backlog.
  - *Tool Compatibility:* Non-OpenAI API users were experiencing silent tool-call failures due to ID mismatches (now resolved).
- **Use Cases:** The pattern of pull requests indicates a user base moving past simple chat into complex tool-augmented workflows, MCP server ecosystems, and platform-level security requirements.

**8. Backlog Watch**
- **[#912](https://github.com/HKUDS/nanobot/issues/912) Support Task-Specific Model Configuration** — Created February 20, marked stale, but remains the backlog item with the highest user demand (3 👍). Maintainers should re-evaluate or communicate a roadmap status for this feature.
- **[#3968](https://github.com/HKUDS/nanobot/pull/3968) Add a `/skill` slash command** — An open pull request awaiting maintainer review. It directly fills a user-reported discovery gap and is relatively low risk to merge.
- **[#4053](https://github.com/HKUDS/nanobot/pull/4053) / [#4119](https://github.com/HKUDS/nanobot/pull/4119) / [#4123](https://github.com/HKUDS/nanobot/pull/4123) Security Hardening PRs** — Multiple open PRs from the same author addressing symlink escapes, MCP SSRF, and read-only path isolation. These are critical for deployments with stringent security requirements but have been open since late May. They likely need a coordinated review and merge.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 5, 2026, based on the provided GitHub data.

---

### 1. Today's Overview
The project is experiencing a high-volatility day dominated by regressions from the recent v0.15.1 release, with 50 Issues and 50 PRs updated. The Desktop application is the primary source of friction, with multiple reports of boot loops, launch failures, and input handling bugs. Despite this, the contributor community is highly responsive, submitting fix PRs for critical bugs on the same day they are reported. Feature development is also active, with advancements in memory tool configuration, system tray integration, and platform expansions. No official releases were cut today.

### 2. Releases
No new versions were published today. The current stable version remains v0.15.1, though internal builds are beginning to reference v0.15.2 in recent issue reports (#39512).

### 3. Project Progress
Five pull requests were merged or closed today. Feature development advanced on several fronts:

- **Memory Customization:** A new PR implements a highly requested config option to disable the built-in memory tool while keeping external memory providers active (#39531), directly responding to community feedback (#39492).
- **Desktop UX:** PRs were submitted for a system tray minimize-to-tray feature for Windows and Linux (#39468) and a cron message history preview dialog (#39344).
- **Platform Integration:** A fix for Slack slash commands breaking in DM threads was submitted (#39527), and the shared OneBot client for platform expansion (QQ) was refined (#38037).
- **Security & Stability:** A critical `aiohttp` dependency was bumped to clear security advisories (#39467). A self-heal mechanism for a broken `uvicorn` install causing desktop boot loops was submitted (#39530). The installer was also patched (#39518).

### 4. Community Hot Topics
Analysis of the most active discussions reveals a community focused on customization, security, and multi-user deployments.

- **#527 – Gateway Permission Tiers (RBAC):** This remains the most commented issue (10 comments). The request for role-based access control for messenger gateways signals a strong demand for enterprise and multi-tenant deployment capabilities.
- **#39492 / #39531 – Disabling the Built-in Memory Tool:** This is the fastest lifecycle item of the day, transitioning from a feature request to a submitted PR within hours, demonstrating high community alignment with the project’s responsiveness.
- **#3969 – Docker Security Configuration:** Although now closed, this security issue garnered significant community support (4 upvotes), indicating strong user approval for the project's recent hardening efforts.
- **#39505 – Desktop Boot Loop:** A critical regression blocking new users. The community and maintainers quickly identified the root cause (`uvicorn` subpackage), resulting in a same-day fix PR (#39530).

### 5. Bugs & Stability
Stability is the dominant theme today, with several regressions reported in v0.15.1, particularly regarding the Desktop app and CLI.

**Critical / Blocking (P2):**
- **Desktop App Boot Loop:** First-launch bootstrap fails with `ImportError: No module named 'uvicorn.supervisors'` (#39505). *Fix exists: #39530.*
- **Desktop Fails to Start (Multiple Reports):** Issues include `unrecognized arguments: --tui` (#39503), blank page post-install on Mac (#39484), and missing `--no-sandbox` on Linux (#39533). Mac installer also fails (#39332, now closed).
- **CLI Freeze on `/reload-mcp`:** Terminal becomes completely unresponsive, requiring a force-close (#39418).

**Moderate Impact:**
- **Input Handling:** CJK IME input truncation on macOS (#39457) and Chinese prompt cutoff on Windows (#39534).
- **Session Management:** Resuming sessions crashes with `Rich MarkupError` (#39469). Long conversations break after session switching (#39512).
- **Misleading Errors:** Desktop reports "OpenRouter API key missing" when the actual failure is a 401 gateway auth error (#39365).
- **Resource Cleanup:** The `/stop` command fails to clean up Docker sandbox environments (#39489).
- **Platform-Specific Bugs:** Feishu MEDIA attachments in threads route to the main conversation (#39526). Gateway fails permanently after WiFi change or laptop sleep (#39525).

### 6. Feature Requests & Roadmap Signals
The data reveals strong signals for both enterprise polish and deeper infrastructure integration.

- **Multi-User & Enterprise (Gateway RBAC #527):** This is the strongest product signal for enterprise growth. Expect this to be a headline feature for a major release.
- **Memory Customization (#39492):** Already implemented in PR #39531. Likely for v0.15.2.
- **Desktop Power Features (System Tray #39468, Cron History #39344):** Users want the Desktop client to function as a persistent background service.
- **Model Flexibility (Routing Profiles #39507):** The demand for model presets suggests a desire to switch between "speed" and "quality" configurations easily.
- **Sandbox HOME Bridge (#39523):** Users request better integration of the subprocess HOME sandbox with system tools (SSH, Keychain, Python), indicating advanced DevOps use cases.
- **Network-Agnostic Installation (#39529):** The request for ZIP fallback as a first-class citizen suggests the project is expanding its global user base into restricted network environments.

### 7. User Feedback Summary
- **Dissatisfaction:** The dominant theme is frustration with the v0.15.1 Desktop release stability. Installation friction and launch failures are the primary onboarding barriers. The misleading "OpenRouter key missing" error (#39365) creates significant confusion during troubleshooting.
- **Satisfaction:** The community is highly technically capable, often submitting root cause analysis within bug reports. The rapid conversion of the memory tool feature request (#39492) into a PR (#39531) signals strong developer relations and project responsiveness.
- **Use Cases:** Signals point towards multi-platform gateway operations (Telegram, Discord, Slack, Feishu, QQ) and deep personal infrastructure integration (Keychain, SSH, Docker sandbox, local LLMs).

### 8. Backlog Watch
Several high-priority items require maintainer attention to clear the pipeline.

- **[CRITICAL ALERT] Session Management Security Fix (#9560):** A P0 vulnerability fix for `gateway/session.py` has been open since **April 14**. This unmerged security patch is the single largest risk in the backlog.
- **[Triage Needed] Gateway RBAC (#527):** This highly-requested feature has been open since **March 6**. It requires a product decision and assignment to move forward.
- **[Stalled] Ollama Cloud Provider (#22648):** Open since **May 9**, this significant community-facing integration appears blocked and needs unblocking.
- **[Stalled] MCP Registry Documentation (#31292):** Open since **May 24**. Formalizing MCP metadata is important for ecosystem growth.
- **[Ready to Merge?] Sweep Task Leak Fix (#22064):** A clean, small fix for a startup race condition waiting since **May 8**.
- **[Decision Needed] Network Install Strategy (#39529):** A well-argued case to change the installer logic to prioritize ZIP downloads over Git clones on restricted networks.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for 2026-06-05, generated from the provided GitHub data.

---

## PicoClaw Project Digest — 2026-06-05

### 1. Today's Overview

PicoClaw saw a significant spike in development activity over the past 24 hours, with **22 pull requests** and **7 issues** updated, resulting in **12 PR merges**. The project is clearly in a high-velocity hotfix sprint following the v0.2.9 stable release, with a strong focus on resolving critical regressions and hardening core infrastructure. A new nightly build (`v0.2.9-nightly.20260605`) was published, aggregating these fixes for early adopters. While a serious new bug regarding runaway token consumption in Evolution Mode was reported, the project's rapid turnaround on earlier critical issues (e.g., the singleton crash loop and Codex integration) signals a healthy and highly responsive maintenance cycle.

### 2. Releases

**New Release: `v0.2.9-nightly.20260605.5224b9a4`**
- **Changelog:** [Compare v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **Summary:** An automated nightly build containing all changes merged to the `main` branch since the v0.2.9 stable release.
- **Notable Changes Included:**
    - **Fix:** Singleton PID check now verifies process identity (prevents crash loops).
    - **Fix:** Codex OAuth tool calls are no longer dropped on empty final responses.
    - **Fix:** Makefile compatibility with Go toolchains returning version strings with embedded spaces.
- **Notes:** This build is labeled as potentially unstable. No database migrations or breaking configuration format changes are indicated, making it suitable for users who need immediate fixes but should be tested thoroughly.

### 3. Project Progress

The 12 closed/merged PRs focus heavily on **reliability, provider stability, and code hardening**.

**Stability & Build:**
- **Merged [#3000](https://github.com/sipeed/picoclaw/pull/3000):** Fix for the stale PID crash loop. The singleton check now verifies the *identity* of the process owning the PID, not just its existence.
- **Merged [#2999](https://github.com/sipeed/picoclaw/pull/2999):** Build system fix for Go toolchains returning version strings with embedded spaces (e.g., `go1.25.10 X:nodwarf5`), superseding prior attempts (#2976).
- **Merged [#2996](https://github.com/sipeed/picoclaw/pull/2996):** Added proper error handling for 7 previously ignored `json.Marshal` calls in the exec tool, preventing silent data corruption in LLM responses.

**Provider & API Fixes:**
- **Merged [#3007](https://github.com/sipeed/picoclaw/pull/3007):** Fix for Codex OAuth GPT-5.5 dropping function calls during streaming when the final response output was empty.
- **Merged [#3008](https://github.com/sipeed/picoclaw/pull/3008):** Adapted the codebase to breaking changes in `larksuite/oapi-sdk-go` v3.9.4 (renamed `ReceiveIdTypeChatId`).

**Dependency Updates:**
- Merged bumps for `larksuite/oapi-sdk-go` ([#3005](https://github.com/sipeed/picoclaw/pull/3005)), `aws-sdk-go-v2/service/bedrockruntime` ([#3004](https://github.com/sipeed/picoclaw/pull/3004)), and `modernc.org/sqlite` ([#3003](https://github.com/sipeed/picoclaw/pull/3003)).

### 4. Community Hot Topics

**1. [Issue #2720](https://github.com/sipeed/picoclaw/issues/2720) — Singleton PID Crash Loop (Closed)**
- **Activity:** 8 comments.
- **Analysis:** Previously the dominant user pain point. User `weissfl` reported a complete crash loop caused by the gateway failing to recognize a reused PID (from `systemd-resolved`). The community correctly identified the root cause, which was directly resolved by the merged fix in [#3000](https://github.com/sipeed/picoclaw/pull/3000). This highlights a strong user investment in daemon reliability.

**2. [Issue #2968](https://github.com/sipeed/picoclaw/issues/2968) — `/context` Command Transparency (Open)**
- **Activity:** 5 comments, 1 thumbs up.
- **Analysis:** User `xpader` flagged a UX/transparency gap where the `/context` command only shows the hard compression threshold ("Compress at: 76800 tokens"), omitting the soft summarization trigger. This reveals a maturing user base that wants deeper insight into context management. A targeted fix is already in review via **[PR #2985](https://github.com/sipeed/picoclaw/pull/2985)**.

### 5. Bugs & Stability

**Critical:**
- **[Issue #3012](https://github.com/sipeed/picoclaw/issues/3012) [OPEN] — Continuous Token Consumption with Evolution Enabled**
    - **Reporter:** xpader
    - **Summary:** Enabling Evolution Mode causes indefinite token consumption every minute regardless of user interaction, posing a significant financial and performance risk.
    - **Status:** Newly reported. No fix PR linked yet. Highest priority issue on the board.

**High:**
- **[Issue #3002](https://github.com/sipeed/picoclaw/issues/3002) [OPEN] — OneBot Group Chat Using Private Message API**
    - **Reporter:** Xuan-Xuann
    - **Summary:** Group chat replies in OneBot are sent via `send_private_msg` with the group ID as a user ID, breaking group functionality entirely.
    - **Status:** Fix drafted in **[PR #3009](https://github.com/sipeed/picoclaw/pull/3009)** (Open). Awaiting review and merge.

**Medium:**
- **[Issue #2968](https://github.com/sipeed/picoclaw/issues/2968) [OPEN] — `/context` Display Bug**
    - **Status:** Fix in review via **[PR #2985](https://github.com/sipeed/picoclaw/pull/2985)**.

**Low (Proactive Hardening):**
- **[PR #3011](https://github.com/sipeed/picoclaw/pull/3011) & [PR #3010](https://github.com/sipeed/picoclaw/pull/3010) [OPEN] :** Proactive discovery of unchecked type assertions in agent subscriptions and channel configuration that could cause panics.

### 6. Feature Requests & Roadmap Signals

- **Evolution Mode Hardening:** The severe token waste bug (#3012) makes stabilization of Evolution Mode the absolute top priority for an immediate hotfix.
- **WhatsApp Native Mode:** **[PR #2934](https://github.com/sipeed/picoclaw/pull/2934)** (open, stale) seeks to enable local WhatsApp integration via `whatsmeow` without a bridge. This is a strong candidate for the next minor feature release (v0.3.0).
- **Anthropic & Bedrock Support:** Active dependency bumps ([#2962](https://github.com/sipeed/picoclaw/pull/2962), [#3004](https://github.com/sipeed/picoclaw/pull/3004)) indicate continued investment in AWS and Anthropic provider parity.
- **Configuration Simplification:** The dual `config.json` / `.security.yml` merge logic is still causing friction ([#2956](https://github.com/sipeed/picoclaw/pull/2956)). Improving this workflow is a clear roadmap signal.

### 7. User Feedback Summary

- **Pain Points:**
    - **Cost Concerns:** The Evolution token drain (#3012) is the loudest signal, indicating a strong user expectation for robust safeguards against runaway API consumption.
    - **Integration Friction:** FreeBSD users face build failures (#2999), while bot operators find OneBot group messaging completely non-functional (#3002).
    - **Config Complexity:** Users are navigating the new dual-config system, leading to subtle channel disabling errors (#2956).
- **Satisfaction:**
    - User trust remains high. Contributors are filing extremely detailed, actionable reports (including provider stream logs in #3006), and the rapid closure of issues like #2720 and #3006 demonstrates a capable and responsive development team. The community is acting as an effective QA force.

### 8. Backlog Watch

Items requiring maintainer attention:

- **[PR #2813](https://github.com/sipeed/picoclaw/pull/2813) [Stale, 29 days] — Original PID Fix**
    - **Issue:** This older PR proposing a fix for the stale PID issue has been superseded by the merged [#3000](https://github.com/sipeed/picoclaw/pull/3000). It needs a formal "Closed" status by a maintainer to clean up the project board and avoid reviewer confusion.

- **[PR #2947](https://github.com/sipeed/picoclaw/pull/2947) [Stale, 10 days] — Claude Sonnet 4.6 Model ID**
    - **Issue:** A simple, well-understood fix correcting an invalid default model ID for `claude-sonnet-4-6`. This has gone unmerged for over a week and blocks a first-use failure for new Anthropic users.

- **[PR #2956](https://github.com/sipeed/picoclaw/pull/2956) [Stale, 9 days] — Security.yml Channel State**
    - **Issue:** A critical fix for the `security.yml` merge logic that prevents channels from being silently disabled. This touches core configuration behavior and requires a thorough code review to prevent regression.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-05

## 1. Today's Overview

NanoClaw shows a focused, maintenance-heavy pulse today. **8 Pull Requests** were updated in the last 24 hours, but only **1 new Issue** was opened, suggesting core contributors and community members are deep in stabilization work rather than surfacing new feature requests. The three merged/closed PRs resolved critical WhatsApp session bugs and a code quality issue, while several open PRs target Signal DM reliability and LID migration bugs in WhatsApp. No new releases were cut, indicating the project is consolidating patches before the next version. Community interaction via comments or reactions is nil across the board today, but the technical depth of the submitted fixes is high, revealing strong contributor investment in keeping the platform working against upstream library changes.

## 2. Releases

**No new releases** were created today.

---

## 3. Project Progress

Three Pull Requests were closed/merged in the last 24 hours:

- **[#2687] Trip agent skill** (dtanikella) — *Closed*. A community-contributed skill, accepted into the ecosystem. Indicates continued growth of NanoClaw's agent skill library.
- **[#2633] fix(whatsapp): two structural bugs that destroy paired sessions on Baileys 7.x** (maschenborn) — *Closed*. **Critical fix.** Resolves a self-destruct mechanism and auth wipe bug that made WhatsApp installations with `WHATSAPP_PHONE_NUMBER` set unreliable on Baileys 7.x. This directly improves production reliability for WhatsApp channel users.
- **[#104] fix: replace `as any` casts with proper BoomError type** (Alakazam03) — *Closed*. A housekeeping improvement that removes unsafe type casts in `index.ts` and `whatsapp-auth.ts`, replacing them with a strictly typed `BoomError` interface. Improves long-term code maintainability.

---

## 4. Community Hot Topics

While no Issues or PRs show comment or reaction activity today, the *nature* of the open PRs reveals the community's deepest areas of focus:

### Signal Integration Churn
- **[#2689] fix(signal): set isMention for DMs and use signal: prefix for platform IDs** (klingel) — Open. Addresses a critical onboarding bug where the router silently drops first-ever DMs on Signal because `isMention` wasn't set, preventing the group from being registered. Also fixes platform ID prefixing.
- **[#2685] docs(signal): group typing, outbound reactions, quote-reply fix** (ira-at-work) — Open. Documents rich interaction features for Signal, including group typing indicators (with 4s refresh), outbound reactions, and a quote-reply fix. This suggests Signal is rapidly catching up to feature parity with other channels.

**Analysis:** The Signal channel is undergoing a heavy stabilization push. The implicit need is clear: users deploying NanoClaw on Signal are hitting fundamental barriers (messages swallowed, missing features). The community is actively building the missing pieces.

### WhatsApp LID Migration Crisis
- **[#2688] fix(whatsapp): stop translating group participants to phone JIDs (fixes ack 421 on LID groups)** (mcaldas) — Open. WhatsApp is migrating groups to LID (LinkedID) participant addressing. NanoClaw's current code translates these LIDs to phone JIDs in `getNormalizedGroupMetadata`, causing outgoing messages to silently fail with **ack error 421**. The fix stops the translation altogether, allowing LIDs to pass through unmodified.

**Analysis:** This is arguably the most impactful community contribution today. A silent delivery failure in groups is a production emergency for any WhatsApp bot. The fix is surgical and well-scoped.

### Long-Running Feature Flag: Voice Transcription
- **[#2459] feat(skill): add /add-voice-transcription-chat-sdk** (mtichikawa) — Open (since May 13). Adds opt-in on-device voice transcription via `whisper.cpp` for Discord and all Chat SDK-bridged channels (Slack, Teams, Webex, Google Chat). Fully local, no cloud API key required.

**Analysis:** This PR has been open for over three weeks without merge feedback. It represents a highly-desired "offline-first" capability. The lack of movement is a potential source of contributor frustration.

---

## 5. Bugs & Stability

Bugs are the dominant theme today. Ranked by severity:

### [CRITICAL] WhatsApp Session Self-Destruction
- **Fix merged (#2633).** Paired WhatsApp sessions were spontaneously wiping their own auth data on Baileys 7.x. Merged today.

### [CRITICAL] WhatsApp Silent Message Failures on LID Groups
- **Fix proposed (#2688, Open).** Outbound group messages fail silently with ack error 421 due to LID migration. The proposed fix is a one-line change in `getNormalizedGroupMetadata` that stops JID translation.

### [HIGH] Signal First-Message Drop
- **Fix proposed (#2689, Open).** The router drops the very first DM sent to a NanoClaw bot on Signal because `isMention` is not flagged. This breaks new user onboarding entirely. The fix adds the missing flag and corrects platform ID formatting.

### [HIGH] Agent Core Loop Compaction Bug
- **Open since May 11 (#2405, Open).** After the poll-loop performs auto-compaction, the model frequently drops the `<message to="…">…</message>` XML wrapping discipline. This leads to malformed outputs and degraded agent behavior. **This is a fundamental reliability issue in the core agent engine that has gone unmerged for 25 days.**

### [LOW] Type Safety
- **Fix merged (#104).** Removed `as any` casts for Baileys error handling.

---

## 6. Feature Requests & Roadmap Signals

Several signals point to the direction of the next NanoClaw release:

1. **Offline-First Voice Transcription (PR #2459):** The push for local `whisper.cpp` integration across multiple channels strongly suggests that **on-device AI features** are the next major feature pillar. The community clearly values privacy and independence from cloud APIs.

2. **Rich Interactive Features for Signal (PR #2685):** The documentation of group typing indicators, outbound reactions, and quote-reply fixes indicates that Signal is being hardened into a first-class citizen with full interactive parity. Expect Signal to be highlighted in the next release notes.

3. **Travel Agent Skills (Issue #2686, PR #2687):** The co-occurrence of a "Traveling" issue and a "Trip agent" skill today hints at user demand for specialized agentic workflows (travel planning, itinerary building). This may inspire a broader "productivity skills" category.

4. **WhatsApp LID Compliance (PR #2688):** WhatsApp's forced LID migration is an external pressure. The next release must incorporate this fix to remain viable on the platform.

---

## 7. User Feedback Summary

No direct user satisfaction or dissatisfaction is expressed in today's issue comments. However, the following pain points can be inferred from the patches submitted today:

| Pain Point | Evidence | Implied Impact |
|---|---|---|
| "My WhatsApp bot auth keeps breaking on restart" | PR #2633 (closed fix) | High. Production stability at risk. |
| "My WhatsApp bot replies vanish in groups" | PR #2688 (open fix) | Critical. Silent failures erode user trust. |
| "My Signal bot ignores the first message I send" | PR #2689 (open fix) | High. Blocks new user onboarding on Signal. New users walk away. |
| "My agent produces broken output after running for a while" | PR #2405 (open, aged) | High. Long-running sessions degrade. |
| "I want voice transcription without paying OpenAI" | PR #2459 (open, aged) | Medium. Feature desire, user expectation. |

The overall sentiment appears to be a **committed but frustrated user base** that is solving its own problems through code contributions rather than waiting for maintainers. This is a double-edged sword: it shows strong community capability but risks contributor burnout if PRs go stale (see: #2405, #2459).

---

## 8. Backlog Watch

Several significant items are languishing without maintainer action:

- **[#2405] fix(poll-loop): deliver unwrapped output** — Open for **25 days**. A core agent loop regression where model output discipline breaks after compaction. This undermines the fundamental value proposition of the assistant. **Requires immediate design review or merge.**

- **[#2459] feat(skill): add /add-voice-transcription-chat-sdk** — Open for **23 days**. A large, well-structured feature adding local voice transcription across multiple channels. Silence from maintainers risks losing the contributor and delaying a key roadmap item.

- **[#2686] Issue: Traveling** — Opened 1 day ago with the single line "I want to travel to Canada." While low-effort, it signals unmet user expectations. A response directing the user to the Trip agent skill (PR #2687) or requesting clarification would improve project responsiveness health.

**Summary of Backlog Risk:**
The lack of movement on **PR #2405** is the single most concerning data point in today's digest. A core loop reliability bug sitting for nearly a month without comment suggests the maintainer team may be resource-constrained or that the fix requires a deeper architectural discussion. Either way, transparency and triage on this item would significantly improve project health perception.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**Ironclaw Project Digest — 2026-06-05**

---

### 1. Today's Overview
Ironclaw development velocity remains exceptionally high as the project pushes toward Reborn runtime production readiness. In the last 24 hours, 41 issues and 50 pull requests were updated, with 14 issues closed and 16 PRs merged. The core team is cycling rapidly between landing new integration features (Slack, WebUI v2, Feishu) and stabilizing core runtime mechanics (subagent durability, compaction, trigger lifecycle). A defining signal this cycle is the team’s explicit technical-debt intervention: tracking issues for decomposing the oversized `ironclaw_reborn_composition` crate were filed proactively (#4470, #4469, #4471), reflecting disciplined engineering practice despite high shipping pressure.

---

### 2. Releases
No releases published today.

---

### 3. Project Progress
Progress was concentrated on production hardening of the Reborn agent runtime and expanding channel integration:

- **Agent Durability:** A complete cycle of subagent correctness work landed. Issues [#4348](https://github.com/nearai/ironclaw/issues/4348), [#4349](https://github.com/nearai/ironclaw/issues/4349), [#4350](https://github.com/nearai/ironclaw/issues/4350), and [#4358](https://github.com/nearai/ironclaw/issues/4358) closed, delivering durable completion delivery, spawn compensation, and gate-replay re-validation. The result is tracked under umbrella [#4474](https://github.com/nearai/ironclaw/issues/4474).
- **Trigger Lifecycle:** The `builtin.trigger_create` tool was rebuilt to support one-time runs, proper creator pairing, and activation gating ([#4466](https://github.com/nearai/ironclaw/pull/4466), [#4473](https://github.com/nearai/ironclaw/issues/4473), [#4472](https://github.com/nearai/ironclaw/issues/4472)). Umbrella [#4475](https://github.com/nearai/ironclaw/issues/4475) now consolidates the remaining trigger-lifecycle spec.
- **Slack Integration:** Full Slack channel activation shipped ([#4476](https://github.com/nearai/ironclaw/pull/4476), [#4478](https://github.com/nearai/ironclaw/pull/4478)), supporting proper actor/subject identity separation and automated OAuth prompt delivery.
- **WebUI v2:** The LLM provider settings were redesigned for progressive disclosure ([#4477](https://github.com/nearai/ironclaw/pull/4477)), and a first-run provider onboarding flow ([#4481](https://github.com/nearai/ironclaw/pull/4481)) was opened.
- **Infrastructure:** Security advisories were patched ([#3719](https://github.com/nearai/ironclaw/pull/3719)), read-only CLI commands migrated to Reborn ([#4379](https://github.com/nearai/ironclaw/pull/4379)), and a canonical identity resolver was introduced for OAuth standardization ([#4461](https://github.com/nearai/ironclaw/pull/4461)).

---

### 4. Community Hot Topics

- **Decomposition of the Monolith ([#4470](https://github.com/nearai/ironclaw/issues/4470)):** A formal acknowledgment that `ironclaw_reborn_composition` has accumulated too many cross-cutting responsibilities. Companion tracking issues ([#4471](https://github.com/nearai/ironclaw/issues/4471), [#4469](https://github.com/nearai/ironclaw/issues/4469)) establish a dedicated decomposition workstream.
- **Canonical Identity Resolver ([#4461](https://github.com/nearai/ironclaw/pull/4461)):** A large PR from italic-jinxin establishes a single boundary for resolving external identities to `UserId`, replacing the prior WebUI-specific user store. This is a foundational architectural move that consolidates SSO, OAuth, and external actor handling.
- **OpenAI-Compatible API Contracts ([#4459](https://github.com/nearai/ironclaw/pull/4459)):** A new dedicated `ironclaw_reborn_openai_compat` crate was introduced with route descriptors for Chat Completions and Responses APIs. This slice of epic [#3283](https://github.com/nearai/ironclaw/issues/3283) provides fail-closed beta stubs until the ProductWorkflow facade lands.
- **Feishu Integration ([#4178](https://github.com/nearai/ironclaw/pull/4178)):** A large PR for Feishu/Lark websocket event intake is open with zero comments, indicating a need for broader reviewer bandwidth to advance this community-facing channel.

---

### 5. Bugs & Stability

**Critical:**
- **[#4431](https://github.com/nearai/ironclaw/issues/4431) (FIXED / Regression Test Demanded):** `builtin.spawn_subagent` was advertised in system-prompt surface text but missing from the structured `tools` array, making it wholly uncallable by OpenAI-compatible models. This is a systemic validation gap: a regression test is now required to enforce parity between advertised capabilities and the tool definitions array.
- **[#4311](https://github.com/nearai/ironclaw/issues/4311) (OPEN):** Budget governance failures (e.g., rate limits, quota exhaustion) are incorrectly mapped to `ContextOverflow`, triggering the wrong retry/recovery logic. This masking of true failure modes could lead to runaway retries or invisible budget exhaustion.

**High:**
- **[#4427](https://github.com/nearai/ironclaw/issues/4427) (OPEN):** The Reborn agent loop never emits a trace line for `LoopFailureKind` exits. Operators running with `RUST_LOG=debug` cannot see why a loop ended, directly contradicting standard debugging workflows.
- **[#4420](https://github.com/nearai/ironclaw/issues/4420) (FIXED):** Triggers created with `CompleteAfterFirstFire` policy re-fired indefinitely because the settlement path never consulted the stored policy.
- **[#4084](https://github.com/nearai/ironclaw/issues/4084) (FIXED):** Background subagents completed silently, writing results to storage but never notifying the parent agent. Resolved via the durable subagent delivery work in [#4348](https://github.com/nearai/ironclaw/issues/4348).

**Medium:**
- **[#4368](https://github.com/nearai/ironclaw/issues/4368) (OPEN):** Six required fields on `RebornLoopDriverHostFactory` are typed as `Option`, duplicated constants violate hygiene rules, and `tracing::warn!` in hot REPL paths corrupts terminal output.

---

### 6. Feature Requests & Roadmap Signals

- **API Parity for Agents ([#4468](https://github.com/nearai/ironclaw/issues/4468)):** A direct request to expose the `previous_response_id` term (`resp_...`) to tools for external-API conversation continuation, seeking parity with "engine v2" ([#3669](https://github.com/nearai/ironclaw/issues/3669)). This is a clear signal that production users need agent-level conversation routing.
- **OpenAI API Migration ([#3283](https://github.com/nearai/ironclaw/issues/3283)):** The dominant roadmap item remains the migration of `/v1/chat/completions` and Responses APIs onto the Reborn product workflow. The new contract crate ([#4459](https://github.com/nearai/ironclaw/pull/4459)) is the first formal step.
- **One-Time Triggers ([#4473](https://github.com/nearai/ironclaw/issues/4473)):** Quickly resolved. The ability for `trigger_create` to model one-shot runs rather than only cron schedules was a product request that was identified and closed within the same sprint.
- **Third-Party Extension Ecosystem (OPEN):** The hooks infrastructure series (PRs [#3936](https://github.com/nearai/ironclaw/pull/3936), [#3937](https://github.com/nearai/ironclaw/pull/3937), [#3951](https://github.com/nearai/ironclaw/pull/3951)) represents the strategic roadmap for third-party installed extensions. These PRs remain open and are a critical dependency for ecosystem growth.

---

### 7. User Feedback Summary

The data reveals a project in active stabilization, with developer pain points surfacing through the issue tracker:

- **Pain Point (Reliability):** Core async primitives suffered significant correctness gaps. Background subagents silently dropped results ([#4084](https://github.com/nearai/ironclaw/issues/4084)), one-shot triggers looped infinitely ([#4420](https://github.com/nearai/ironclaw/issues/4420)), and advertised tools were invisible to API-compatible models ([#4431](https://github.com/nearai/ironclaw/issues/4431)). The rapid turnaround on fixes (often < 48 hours) indicates strong maintainer responsiveness, but the density of bugs in new features is characteristic of the high-velocity Reborn migration.
- **Pain Point (Developer Experience / Operators):** Debugging agent loops is explicitly opaque; the failure reason is persisted to DB but never logged, directly contradicting standard operator expectations ([#4427](https://github.com/nearai/ironclaw/issues/4427)). The monolithic composition layer is explicitly called out as an impediment to development velocity ([#4470](https://github.com/nearai/ironclaw/issues/4470)).
- **Satisfaction:** The community’s disciplined approach—creating structured tracking umbrellas, filing targeted decomposition tickets, and fixing bugs immediately upon discovery—indicates a highly mature developer base aligned with the project’s long-term health.

---

### 8. Backlog Watch

The most significant risk in the backlog is the "hooks" infrastructure stack:

- **[#3951](https://github.com/nearai/ironclaw/pull/3951) (Third-party extension activation)**
- **[#3941](https://github.com/nearai/ironclaw/pull/3941) (Hooks maintainability follow-ups)**
- **[#3936](https://github.com/nearai/ironclaw/pull/3936) (LibSqlPredicateStateBackend)**
- **[#3937](https://github.com/nearai/ironclaw/pull/3937) (Cross-backend adversarial parity suite)**

Submitted by `zmanian` on **May 23**, these PRs form a chain (3/4 and 4/4 of a broader series) that unlocks the third-party extension ecosystem. They have been open for nearly two weeks without closure or substantive review activity. Their size and cross-cutting scope (dependencies, CI) likely account for the delay, but the lack of reviewer bandwidth creates a growing risk of merge conflicts and blocks a major roadmap pillar.

Additionally, issue **[#4238](https://github.com/nearai/ironclaw/issues/4238)** (Project product-auth accounts into credential store, opened May 29) is a required follow-up to already-merged auth infrastructure and remains unassigned.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-05

## 1. Today's Overview
The project experienced a major maintenance push, with **16 pull requests merged or closed** in the last 24 hours while **no new issues** were filed. A single existing issue received an update. The bulk activity came from merging the **v2026.5.28** release branch back into `main` and bulk-resolving a batch of six long-dormant ("stale") feature and bugfix PRs from April. This suggests the team is actively stabilizing the codebase after a significant feature release. No new software releases were published today, but the release pipeline was finalized.

## 2. Releases
*No new releases published in the last 24 hours.*

**Note:** The release cycle for **2026.5.28** concluded with the merge of PR [#2090](netease-youdao/LobsterAI PR #2090). This version includes the **Kit (Expert Suite) Market**, **Cowork session local forking**, **manual plugin updates**, and multiple MCP/Gateway/Artifacts stability fixes (73 commits total).

## 3. Project Progress
All 16 PR updated today were merged or closed. Activity clustered around three areas:

**Cowork Agent (Assistant)**
- **Voice input refactored** (PR [#2111](netease-youdao/LobsterAI PR #2111)): ASR IPC registration, recording, WAV encoding, and error handling split into focused modules.
- **Subagent batch deletion** (PR [#2095](netease-youdao/LobsterAI PR #2095)): Batch selection and proper cleanup paths for subagent sessions.
- **System notifications on completion/failure** (PR [#1536](netease-youdao/LobsterAI PR #1536)): Electron native OS notifications so users are alerted outside the app.
- **Message bookmarking** (PR [#1538](netease-youdao/LobsterAI PR #1538)): Database-backed bookmark system with session cascading deletes.
- **Session tag classification** (PR [#1542](netease-youdao/LobsterAI PR #1542)): Custom tags stored as JSON in SQLite, supporting creation, deletion, auto-suggest, and sidebar filtering.
- **Oversized image payload guard** (PR [#2110](netease-youdao/LobsterAI PR #2110)): Pre-send size estimation and error classification for 1009 gateway errors.

**MCP Infrastructure**
- **NPX startup optimization** (PR [#2091](netease-youdao/LobsterAI PR #2091)): Pre-resolves npm packages and converts commands to stable `node <bin>` paths, avoiding cold-start delays. Also adds timing logs.
- **Node toolchain injection** (PR [#2100](netease-youdao/LobsterAI PR #2100)): Managed MCP installs now retain the proper Node path; fallback to raw stdio is graceful.
- **Remote URL validation** (PR [#2103](netease-youdao/LobsterAI PR #2103)): Shared URL validation with localized errors for remote MCP server configs.
- **Streamable HTTP support** (PR [#367](netease-youdao/LobsterAI PR #367)): Imports and normalizes `streamable_http` configs into internal `http` transport, clarifying SSE vs Streamable HTTP in the UI.

**General Fixes**
- **MiniMax-M3 image support** (PR [#2093](netease-youdao/LobsterAI PR #2093)): Fixed a hardcoded `false` flag inherited from M2.5/M2.7 that blocked image input.
- **Internal plugin hiding** (PR [#2096](netease-youdao/LobsterAI PR #2096)): Runtime-bundled OpenClaw plugins now filtered from plugin management UI.
- **i18n corrections** (PRs [#1540](netease-youdao/LobsterAI PR #1540), [#1543](netease-youdao/LobsterAI PR #1543)): Fixed missing translations for the memory edit button and hardcoded Chinese strings in Cowork approval dialogs.
- **Copilot OAuth cleanup** (PR [#1544](netease-youdao/LobsterAI PR #1544)): AbortController properly triggered on Settings unmount to stop background polling.

## 4. Community Hot Topics
- **Issue #769: OpenClaw Gateway Startup Failure** ([netease-youdao/LobsterAI Issue #769](netease-youdao/LobsterAI Issue #769))
  *Updated 2026-06-04.* The only issue touched in the last 24 hours. User reports a timeout error ("网关未能在规定时间内启动成功"). No maintainer response or fix attached yet. The 0-reaction count suggests a narrow user impact, but the 3-month age without triage is notable.

- **Stale Feature Batch Merge**
  Six PRs from early April (#1536, #1538, #1540, #1542, #1543, #1544) were bulk-closed/merged. These represent high-community-interest additions (session tags, bookmarks, notifications) and critical i18n fixes. The simultaneous resolution signals a dedicated backlog-clearing initiative, likely boosting contributor trust and satisfaction.

## 5. Bugs & Stability
| Severity | Issue | Status |
|----------|-------|--------|
| **High** | **OpenClaw gateway timeout** (Issue #769) – User cannot start the gateway at all. No fix merged. Oversized payload crash was separately fixed (#2110) but timeout root cause is distinct. | **Unresolved** |
| **High** | **Hardcoded Chinese in approval dialogs** (PR #1543) – Cowork danger confirmations showed Chinese in English UI, blocking non-Chinese workflows. | **Fixed** |
| **Medium** | **MCP slow startup** (PR #2091) – Repeated `npx -y` resolving on every session causing latency. | **Fixed** |
| **Medium** | **MiniMax-M3 image support hardcoded off** (PR #2093) – Regression carried from older model configs. | **Fixed** |
| **Low** | **Copilot OAuth memory leak** (PR #1544) – Polling continued in background after Settings panel close. | **Fixed** |
| **Low** | **Internal plugins showing in UI** (PR #2096) – User confusion from runtime plugins in management list. | **Fixed** |

## 6. Feature Requests & Roadmap Signals
- **Kit Expert Suite Market** (seen in #2090): A full Redux-integrated marketplace UI with install/uninstall, tab browsing, and kit selection in the chat input. This is the largest new surface area in the 2026.5.28 release and points toward a pluggable capability ecosystem.
- **Streamable HTTP MCP** (#367): Moving beyond basic SSE/stdio to the newer MCP transport spec suggests a focus on low-latency, scalable tool integration for the routing layer.
- **Session Organization** (#1538, #1542): The rapid merging of bookmarks and tags signals strong demand. The roadmap likely includes export/sharing and more advanced search over these metadata fields.
- **Better Plugin/MCP Reliability** (#2091, #2100, #2103): Heavy investment in MCP launch reliability indicates the team is hardening the framework for production agent loops. Expect a formal "MCP Health Dashboard" in a future release.

## 7. User Feedback Summary
*Inferred from recently addressed pain points and features:*

- **Satisfaction Drivers:** The batch merge of user-submitted features (tags, bookmarks, notifications) directly addresses requests for better Cowork session management. Users wanting non-Chinese localization should see dramatic improvements with the i18n fixes merged today.
- **Pain Points:**
  - *Gateway reliability:* At least one user cannot start the gateway (#769). Combined with the crash-on-large-image bug (#2110 fix), gateway stability is a recurring concern.
  - *MCP cold start:* Users experiencing multi-second delays every session (addressed by #2091).
  - *Platform consistency:* "edit" / "Edit" / "编辑" string mix-ups in i18n (#1540, #1543) show UI polish gaps for multi-language users.
- **Adoption Signals:** No negative churn signals visible. The release review in #2090 shows active internal testing and the stale batch merge shows maintainers are listening to the community.

## 8. Backlog Watch
- **Issue #769: OpenClaw Gateway Startup Failure** ([netease-youdao/LobsterAI Issue #769](netease-youdao/LobsterAI Issue #769))
  *Created 2026-03-24, updated 2026-06-04, 1 comment.*
  This is the only issue without a merged fix that saw update. With the oversized-payload guard (#2110) merged, the gateway code path has been touched but this specific startup timeout remains unexplained. Needs maintainer reproduction and triage; should be higher priority given it blocks core functionality.

- **No other long-dormant PRs remain in the active window.** The 6 stale PRs that were the biggest backlog items are now resolved. Monitor for new stale submissions.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest: 2026-06-05

## 1. Today's Overview
Development velocity remains steady with 3 open pull requests updated in the last 24 hours, though no PRs were merged or closed today. The community contributed two new feature requests ([SMS/LINE channels](https://github.com/moltis-org/moltis/issues/1101) and [local STT engine support](https://github.com/moltis-org/moltis/issues/1102)), signaling expansion interest beyond the current Telegram-focused architecture. No new releases were cut. Core contributor **s-salamatov** drove all active PRs, focusing on session history robustness, browser agent reliability, and Telegram UX refinement. Overall project health appears stable, with maintainers actively addressing community pain points before committing to a new release.

## 2. Releases
No new releases were published today. The project does not have an official versioned release.

## 3. Project Progress
**No PRs were merged or closed in the last 24 hours.** Active work in progress includes:

- **[PR #1099 – Separate Telegram progress stream from final replies](https://github.com/moltis-org/moltis/pull/1099)** – Treats Telegram streaming as temporary progress updates, sends a silent progress message that is edited with throttled updates, then deletes it on stream completion to allow the normal final reply delivery. Fixes Issue #1097.
- **[PR #1103 – fix(browser): pierce shadow DOM lookups efficiently](https://github.com/moltis-org/moltis/pull/1103)** – An alternative/update path for a previously reviewed PR, keeping original behavior and adding review fixes. Improves snapshot and ref-based lookup paths to handle Shadow DOMs correctly.
- **[PR #1089 – Cap persisted tool results before rehydration](https://github.com/moltis-org/moltis/pull/1089)** – Applies size limits to persisted `tool` and `tool_result` content across all conversation flows (normal chat, streaming, retry-after-compaction, compacting, silent memory turns). Prevents context inflation during session history rehydration.

These three PRs are all authored by the same contributor and represent the majority of code movement this week.

## 4. Community Hot Topics
None of the open Issues or PRs have yet accumulated comments or reactions, suggesting either the community is young or users are waiting for maintainer feedback. However, the topics themselves reveal strong directional signals:

- **[Issue #1102: Local STT Engines (FunASR / SenseVoice)](https://github.com/moltis-org/moltis/issues/1102)** – The user specifically highlights ultra-fast local inference (SenseVoice-Small achieves ~70ms for 10s audio) and native streaming support via Paraformer-streaming. The underlying need is low-latency, fully offline voice processing—a clear gap in the current architecture.
- **[Issue #1101: SMS and LINE Channels](https://github.com/moltis-org/moltis/issues/1101)** – The user requests expanding beyond Telegram into SMS and LINE. The underlying driver is platform ubiquity: users want Moltis to act as a universal assistant that lives on their phone's native messaging stack.
- **[PR #1099: Telegram UX Fix](https://github.com/moltis-org/moltis/pull/1099)** – Closes a previously unreported (or separate) issue regarding Telegram message delivery. This is likely the most user-facing hot topic, as broken final-reply delivery directly impacts daily use.

## 5. Bugs & Stability
No new bugs were filed as Issues today. The stability work being done lies entirely within the open PRs:

| Severity | Issue / PR | Description | Fix Status |
|---|---|---|---|
| **High** | [PR #1089](https://github.com/moltis-org/moltis/pull/1089) | Unbounded `tool_result` growth during session history rehydration could lead to provider context overflows and degraded reasoning. | Fix pending merge |
| **Medium** | [PR #1099](https://github.com/moltis-org/moltis/pull/1099) | Telegram treats streaming progress as a final answer, resulting in missing/incorrect message delivery. | Fix pending merge |
| **Medium** | [PR #1103](https://github.com/moltis-org/moltis/pull/1103) | Browser snapshot lookups fail or are slow when elements reside inside Shadow DOMs. | Fix pending merge |

All three stability concerns are already under remediation by the same maintainer, which is a strong indicator of focused team attention.

## 6. Feature Requests & Roadmap Signals
Two community feature requests were opened today:

1. **[#1102 – FunASR / SenseVoice STT](https://github.com/moltis-org/moltis/issues/1102)** – This is the strongest roadmap signal. The request for a high-performance local ASR engine aligns with the broader open-source agent trend toward on-device inference. Given Moltis’s current voice focus, it is **highly likely** this feature will be marked for the next minor milestone (v0.x+1).

2. **[#1101 – SMS & LINE channels](https://github.com/moltis-org/moltis/issues/1101)** – Multi-channel support represents a major architectural expansion. Predictably this will be prioritized behind the current Telegram stability work (PR #1099). A plugin/connector framework may emerge to support this.

**Short-term prediction**: The next release (when it happens) will primarily batched the three pending PRs: tool result limits, Shadow DOM fixes, and Telegram streaming fixes. Feature requests #1101 and #1102 will likely be accepted with a planning label and targeted for the subsequent cycle.

## 7. User Feedback Summary
- **Pain Points**: Telegram message delivery (PR #1099 fix underway). Lack of low-latency local STT (Issue #1102). Inability to run the agent outside Telegram (Issue #1101).
- **Use Cases**: Users are deploying Moltis in voice-first, real-time, and multi-platform scenarios. The request for SMS/LINE implies mobile-native, notification-driven assistant usage. The STT request suggests audio-heavy workflows where cloud round-trips are unacceptable.
- **Satisfaction / Dissatisfaction**: The tone of the new issues is supportive (“Great voice assistant project!”), indicating a receptive user base that wants to grow with the project. The absence of bug reports or complaints suggests core functionality is stable for existing users, though Telegram streaming (PR #1099) was clearly a known breakage that needed a dedicated fix.

## 8. Backlog Watch
The overall backlog is lean. Key items requiring attention:

| Item | Age | Risk | Notes |
|---|---|---|---|
| **[PR #1089 – Cap persisted tool results](https://github.com/moltis-org/moltis/pull/1089)** | Open since June 1 (4 days) | **Medium** | A core stability PR from a major contributor with no review comments yet. Risk of stalling delays the robustness fixes it contains. |
| **[Issue #1102 – FunASR/SenseVoice](https://github.com/moltis-org/moltis/issues/1102)** | Opened June 4 (1 day) | Low | Needs a maintainer label and acknowledgment. No response yet. |
| **[Issue #1101 – SMS/LINE](https://github.com/moltis-org/moltis/issues/1101)** | Opened June 4 (1 day) | Low | Same as above. Pre-filled checklist suggests a power user—worth engaging quickly. |

No item in the backlog has languished beyond a week. Maintaining this low-latency response loop is healthy for community momentum.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

**CoPaw Project Digest — 2026-06-05**

### 1. Today’s Overview
The project saw high activity with 32 issues and 33 PRs updated in the last 24 hours, alongside a new patch release, **v1.1.11-beta.1**. The day’s work was dominated by stability fixes for the core backend (state storage corruption, provider startup crashes, MCP recovery) and a series of user-facing fixes for the context compaction system. The community submitted several critical bug reports around infinite loops and provider-specific rendering issues, while feature development advanced on sub-agent lifecycle management and the DataPaw analytics plugin. Contribution diversity remains healthy, with multiple first-time-author PRs landing today.

### 2. Releases
**New: v1.1.11-beta.1**
- **Fixes:** Added a fallback in `ProviderManager` for `get_model_max_input_length` to handle missing configuration edge-cases.
- **Refactor:** Disabled push notification bubbles for cron jobs of type `agent` to reduce channel noise.
- **Migration Notes:** None required.

### 3. Project Progress
A significant number of PRs were merged or updated to final state today, advancing several areas:

- **MCP & Agent Execution:**  
  - `fix(mcp): alias-rewrite tool names rejected by OpenAI-style regex` ([#4958](https://github.com/agentscope-ai/QwenPaw/pull/4958)) — fixes a blocking issue where MCP tools with dots in names (e.g., `pat.batch_plan`) were rejected by OpenAI/Anthropic API validation.  
  - `feat(agents): add spawn_subagent tool for ephemeral in-workspace sub-agent execution` ([#4806](https://github.com/agentscope-ai/QwenPaw/pull/4806)) — merged, providing three collaboration modes for sub-tasks.

- **Core Backend Hardening:**  
  Several legacy fixes were finalized:  
  - `fix(app): harden state storage against corruption` ([#1240](https://github.com/agentscope-ai/QwenPaw/pull/1240)) — replaces fragile JSON state with SQLite-backed default.  
  - `fix(providers): defer builtin provider instantiation` ([#3403](https://github.com/agentscope-ai/QwenPaw/pull/3403)) — resolves gunicorn startup crashes.  
  - `fix(mcp): recover crashed clients automatically` ([#1347](https://github.com/agentscope-ai/QwenPaw/pull/1347)) — extends MCP auto-recovery logic.

- **Channel Integrations:**  
  - `feat(feishu): support interactive card content extraction` ([#4879](https://github.com/agentscope-ai/QwenPaw/pull/4879)) — merged.  
  - `feat(channels): add QR code authorization for QQ channel` ([#4848](https://github.com/agentscope-ai/QwenPaw/pull/4848)) — merged.

- **Quality & Testing:**  
  - `test(console): complete frontend unit test milestone — constants, contexts, layouts, api-types, components` ([#4332](https://github.com/agentscope-ai/QwenPaw/pull/4332)) — merged, adding ~100 new test cases.

### 4. Community Hot Topics
The most active discussions highlight deep user engagement with the agent’s feedback loop and runtime predictability:

- **UI Tool Call Responsiveness:** [#4644](https://github.com/agentscope-ai/QwenPaw/issues/4644) (20 comments, *Closed*) — Tool calls not displaying until a refresh was the single most discussed issue, indicating high sensitivity to real-time feedback lags.
- **Agent Execution Control:** Three issues from a single user (`feng183043996`) request an **interrupt/abort mechanism** ([#4961](https://github.com/agentscope-ai/QwenPaw/issues/4961), [#4964](https://github.com/agentscope-ai/QwenPaw/issues/4964)) and **direct shell execution for cron** ([#4950](https://github.com/agentscope-ai/QwenPaw/issues/4950), [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963)). This cluster signals a power-user push toward reliable automation.
- **Context Compaction Crashes:** [#4953](https://github.com/agentscope-ai/QwenPaw/issues/4953) and [#4956](https://github.com/agentscope-ai/QwenPaw/issues/4956) (both *Closed*) detailed compaction failures with `AttributeError`, affecting a core memory workflow.
- **DeepSeek Cache Cost Concern:** [#3891](https://github.com/agentscope-ai/QwenPaw/issues/3891) (4 comments, 1 👍) remains a persistent talking point about the financial impact of low prefix-cache hit rates.

### 5. Bugs & Stability

- **Critical:**
  - **Infinite Execution Loop** ([#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967), *Open*) — Agent task cannot be exited, representing a high-severity runtime block.
  - **Context Compaction Ignores Model Config** ([#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937), *Open*) — The `/compact` command overrides user-configured `max_input_length` (e.g., MiniMax M3 512K defaulted to 128K).

- **High:**
  - **DeepSeek Reply Folding** ([#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962), *Open*) — Content always folded into the thinking block, requiring manual expansion.
  - **Compaction Crash** ([#4953](https://github.com/agentscope-ai/QwenPaw/issues/4953), [*Closed*](https://github.com/agentscope-ai/QwenPaw/issues/4956)) — `'str' object has no attribute 'get'` crashes on mixed content types. Issues closed but root cause pattern tracked.

- **Medium:**
  - **Desktop LAN Access** ([#4960](https://github.com/agentscope-ai/QwenPaw/issues/4960), *Open*) — v1.1.9 desktop app cannot be reached from mobile browsers on the same LAN.
  - **Latex Rendering** ([#4959](https://github.com/agentscope-ai/QwenPaw/issues/4959), *Open*) — Abnormal formula display in console.
  - **MCP Tool Name Validation** ([#4958](https://github.com/agentscope-ai/QwenPaw/pull/4958), *Merged*) — A fix landed today for this blocking bug.

### 6. Feature Requests & Roadmap Signals
The community is converging on a few key enhancements that are strong candidates for the next stable release:

- **Agent Interrupt/Abort ([#4961](https://github.com/agentscope-ai/QwenPaw/issues/4961), [#4964](https://github.com/agentscope-ai/QwenPaw/issues/4964)):** Multiple requests for stopping ongoing execution immediately. Very high community priority.
- **Cron Shell Execution ([#4950](https://github.com/agentscope-ai/QwenPaw/issues/4950), [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963)):** Extending cron beyond text/agent prompts to raw script execution.
- **Token/Context Usage UI ([#4767](https://github.com/agentscope-ai/QwenPaw/issues/4767), [#4782](https://github.com/agentscope-ai/QwenPaw/issues/4782), [PR #4433](https://github.com/agentscope-ai/QwenPaw/pull/4433)):** A frontend badge showing context consumption is under review and aligns with heavy community demand.
- **Provider Card Merging ([#4965](https://github.com/agentscope-ai/QwenPaw/issues/4965)):** Collapsing duplicate providers into single dropdown cards to reduce UI clutter.
- **DataPaw Plugin ([PR #4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)):** Under review, this BI plugin would be a major ecosystem addition.
- **Tauri Desktop Auto-Updater ([PR #4669](https://github.com/agentscope-ai/QwenPaw/pull/4669)):** Essential for the desktop distribution path.

### 7. User Feedback Summary
- **Satisfaction Drivers:** Users are pushing the project into complex automation workflows. The high feature velocity and open contribution culture (multiple first-time contributors) foster strong engagement. The ecosystem value of tools like `spawn_subagent` and MCP is well recognized.
- **Dissatisfaction Points:** Stability of the context management pipeline is a recurring friction point. The inability to interrupt agents leads to wasted time and cost (tokens). DeepSeek users face distinct economic (cache miss costs) and rendering (folded replies) pain. Desktop network binding issues limit mobile access for local users.

### 8. Backlog Watch
The following items require maintainer attention or strategic decisions:

- [**#3891**](https://github.com/agentscope-ai/QwenPaw/issues/3891) **DeepSeek Prefix Cache Hit Rate** (Created Apr 27) — High financial impact; no official technical response yet from the core team.
- [**#4937**](https://github.com/agentscope-ai/QwenPaw/issues/4937) **Compaction Ignores Model_max_input_length** (Created Jun 3) — Unresolved regression that contradicts user configuration.
- [**PR #4900**](https://github.com/agentscope-ai/QwenPaw/pull/4900) **Decouple Plugin Loader from Agent Startup** (Created Jun 2) — A blocker for desktop users running plugins in PyInstaller environments; pending review.
- [**PR #4622**](https://github.com/agentscope-ai/QwenPaw/pull/4622) **DataPaw Plugin** (Created May 22) — Under review for over two weeks; a high-value community contribution awaiting merge.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-05

## 1. Today's Overview
ZeroClaw is in a period of intense engineering velocity. Over the last 24 hours, 33 issues and 50 pull requests were updated, with 11 PRs merged or closed. Activity is split between targeted bug fixes (Windows shell compatibility, TUI stability, Web UI inconsistencies) and major architectural investment (a full observability overhaul, memory strategy migration, and a comprehensive web dashboard revamp). The v0.8.0 release track is being actively organized via a dedicated tracker (#7112), signaling that the project is consolidating feature work and hardening the codebase for an upcoming stable milestone. Community engagement remains high, particularly around agent-to-agent interoperability and desktop automation.

## 2. Releases
**No new releases were published** in the reporting period. The next major release is expected to be **v0.8.0**, which is being tracked explicitly via issue #7112 as a coordination hub for Stable-tier blockers and breaking-change cleanup. No v0.7.x releases were cut today either.

## 3. Project Progress
With 11 non-open PRs and several closed issues, meaningful forward motion was visible across the stack:

- **Provider Reliability**: A critical bug in the Ollama provider that blocked workflows when tools were required was closed (#5962).
- **Distribution Fixes**: The Twitter/X channel is now correctly included in pre-built binaries (#7069).
- **Runtime Stability**: The aggressive 10-minute idle session reaping behavior was fixed, preventing premature session termination (#7179).
- **Windows Parity**: The double-quote mangling bug in the Windows shell tool was resolved (#7083).
- **Platform Support Enhancement**: Claude Code execution on Windows was specifically addressed in a newly submitted PR (#7214).
- **New Feature Landings**: CI/CD improvements are underway, and the groundwork for structured observability and a memory strategy pattern is being laid across several open PRs (#7233, #7234).

## 4. Community Hot Topics
The following discussions are driving the most community energy this week:

- **Computer-Use Support (#6909)**: This is the most actively discussed feature request. The community is calling for screen capture and mouse/keyboard event capability, directly comparing ZeroClaw to OpenAI Codex and Peekaboo. It cuts across desktop, security, and tool domains and is likely to remain a top-line request for the foreseeable future.

- **A2A Protocol (#3566)**: With 7 👍, this is the most *reaction-wanted* issue. Users are eager for native Agent-to-Agent protocol support. A spin-off RFC on agent discovery via `/.well-known/agent-card.json` (#7218) was filed today, showing that the community is actively driving the design.

- **Structured Observability RFC (#7232)**: This deep technical RFC received immediate developer follow-up in the form of a matching PR (#7233). It addresses three specific gaps (sparse events, flat OTel traces, bridge design), indicating that *power users and developers* are pushing for the runtime observability needed to operate ZeroClaw in production multi-agent or complex integration setups.

## 5. Bugs & Stability
The bug landscape today shows a clear pattern: the *Web UI/Gateway* stack is where the most regressions are being surfaced, but the *Windows platform* continues to be the highest-risk operational area.

- **S1 – Workflow Blocked (Critical)**:
    - **TUI Freeze on Daemon Disconnect (#7125)**: The TUI becomes entirely unresponsive when the daemon terminates, requiring a force-quit. A fix appears to still be in development.
    - **Quickstart Alias Collision (#7227)**: The `zerocode` Quickstart hardcodes a `default` provider alias, causing an immediate, blocking collision if any provider already exists in the config. No fix PR exists yet.

- **S2 – Degraded Behavior (High)**:
    - **Skill Loading Broken (#7236, NEW)**: `load_skills_for_agent` receives an incorrect `workspace_dir` set to `config.data_dir`, making it unable to locate skills in `data/skills/`. This is a freshly reported regression and a significant blocker for agent extensibility.
    - **Web UI Clear-All Bug (#7126)**: "Clear all" only flushes the frontend React state, not the backend session. A fix PR (#7222) is already up to synchronize them.
    - **Slack Agent Shell Looping (#7143)**: An agent repeatedly spawns near-identical shell discovery commands until it exhausts `max_tool_iterations`. This degrades Slack-connected coding workflows significantly.
    - **Observability Telemetry Leak (#7151)**: Tool-call telemetry bleeds onto the chat WebSocket, causing permanent "unknown" tool cards. A targeted fix PR (#7221) is open.

- **S3 – Minor / Cosmetic**:
    - Timestamps rendered inside message bubbles (#7157).
    - i18n keys missing for chat toolbar buttons (#7139).

## 6. Feature Requests & Roadmap Signals
The project is clearly navigating toward a "v0.8.0 big bang" release, with several features appearing to be critical blockers versus "nice-to-haves".

- **Likely v0.8.0 Blockers / High Priority**:
    - **Web Dashboard Tabs (#7229)**: MCP, Skills, Plugins & Providers management UI is a major gateway feature, currently in PR.
    - **Web Slash Commands (#7223 / #7137)**: A feature PR is already open, signaling this will likely ship in the upcoming cycle.
    - **Shell Security Tiering (#7155)**: The request for a Claude Code-style allow/ask/deny policy for high-risk commands is tagged P1 and actively discussed.
    - **Per-Model Capability Config (#7100)**: Enabling users to set `vision` and `context_window` per model is flagged P1 and essential for multi-provider correctness.

- **v0.8.1 / Future Releases**:
    - **Computer-Use (#6909)**: While high profile, this is a large architectural lift (risk: high, involves desktop interaction) and is likely slotted post-v0.8.0.
    - **A2A Protocol (#3566)**: Blocked and waiting on maintainer action. The discovery RFC (#7218) may accelerate this, but it remains on the back burner.
    - **Azure `reasoning_effort` (#7228)**: A gap in the dedicated Azure provider compared to the compatible provider. Likely a smaller fix for a minor release.

## 7. User Feedback Summary
- **Pain Points (Explicit & Implicit)**:
    - **Windows Suffering**: The double-quote shell fix (#7083) and the Claude Code Windows PR (#7214) reveal a persistent theme: Windows users are experiencing a degraded tool experience compared to Linux/macOS.
    - **Session & UI Reliability**: Users are hitting real workflow disruptions (TUI freezing #7125, session reaping #7179, web chat history bugs #7126). These erode trust in long-running agent sessions.
    - **Feature Disparity with Tools Like Codex**: The computer-use request (#6909) implicitly criticizes ZeroClaw's lack of desktop automation parity with commercial alternatives and other open-source tools. The LSP request (#5907) reinforces this for coding use cases.

- **Satisfaction Signals**:
    - A user explicitly praised ZeroClaw as "much lighter on resources than many other agent systems" (#7143), validating the Rust-based runtime choice.
    - The breadth and depth of community-driven RFCs (#7232, #7218) show a user base that is deeply invested in the project's architecture, not just surface features.

## 8. Backlog Watch
Several items are at risk of stagnation due to blocking labels or lack of maintainer bandwidth:

- **LSP Support (#5907)**: Blocked for over a month. This is a major feature that directly impacts the core value proposition of zero-cost agent code generation. The community cannot move this forward without maintainer architectural decisions.
- **TLS CA Cert Support (#5797)**: This PR has been open since mid-April. Enterprise users behind corporate PKI are locked out. The lack of movement here is a blocker for organizational adoption.
- **Lost Commits Audit (#6074)**: An open audit task tracking 153 commits lost in a bulk revert. While marked `in-progress`, this has been open since late April. The longer this sits, the harder the historical recovery becomes.
- **A2A Protocol (#3566)**: Despite being the most "liked" issue with 7 👍 and a design RFC (#7218) being submitted today, the core issue has been blocked for months. This is the single highest-signal feature the community wants that is currently stalled.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*