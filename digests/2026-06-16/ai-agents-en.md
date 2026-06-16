# OpenClaw Ecosystem Digest 2026-06-16

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-16 03:44 UTC

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

# OpenClaw Project Digest — 2026-06-16

## 1. Today’s Overview

OpenClaw is experiencing exceptional activity, with **500 issues and 500 pull requests updated** in the last 24 hours. The community merged or closed **87 PRs** today, reflecting a sustained high-velocity development cycle. The release of **v2026.6.8-beta.2** underscores a concentrated effort to harden channel delivery, specifically Telegram and WhatsApp. Security and message integrity continue to dominate the conversation, while the overwhelming demand for native Linux and Windows clients signals a project outgrowing its macOS/iOS origins. The project remains in a highly responsive but heavily burdened state, with critical regressions competing against an ambitious feature roadmap for maintainer attention.

---

## 2. Releases

**v2026.6.8-beta.2** — *Released 2026-06-16*

**Summary:** A focused beta release making Telegram and WhatsApp delivery richer and less brittle.

**Key Changes:**
- **Telegram:** Structured rich text now supports tables, lists, and expandable blockquotes. Intentional line breaks are preserved.
- **CLI Backend:** Prompt-preserving delivery logic improved.
- **Safer Rich Media:** Retired native draft migration logic reduced fragmentation in outbound media handling.
- **Broken/Partial Jobs:** No breaking changes or migration steps documented, though users with heavily customized Telegram or WhatsApp draft pipelines should validate behaviors against this beta.

**Links:**
- [v2026.6.8-beta.2 Release](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.2)

---

## 3. Project Progress

With **87 PRs merged or closed** today, the project is moving fast. Key highlights:

**Merged/Closed This Window:**
- **[PR #68936]** — *Autofix PR review pipeline + Windows daemon (Closed).* A major infrastructure addition: the Claude Agent SDK–powered autofix pipeline and Windows background daemon are now merged, bringing Windows server capability much closer to parity.
- **[Issue #43015]** — *message.send schema overexposes poll/components/modal (Closed).* The fix prevents GPT-family models from auto-populating optional Discord fields, reducing schema-triggered delivery failures.

**Features & Fixes Nearing Landing:**
- **[PR #93265]** — *Streamlined setup with agent-assisted onboarding.* Ready for maintainer look. This radically simplifies the `openclaw onboard` experience and addresses a top community pain point.
- **[PR #92477]** — *Migrate watch app to single-target app.* Proof supplied via screenshot, waiting on author. Brings watchOS support current with Xcode 26.
- **[PR #93480]** — *Restore suppressed answer when before_agent_finalize revision is silent.* Fixes a data-loss bug in the core response loop.
- **[PR #85254]** — *Thread prepared manifestPlugins through runtime model-id normalize chain.* Performance optimization ready for maintainer look.
- **[PR #92086]** — *Security Matrix runtime-fact audit model.* A large security engineering effort adding deterministic, auditable runtime policy evaluation.

**Links:**
- [PR #68936](https://github.com/openclaw/openclaw/pull/68936)
- [Issue #43015](https://github.com/openclaw/openclaw/issues/43015)
- [PR #93265](https://github.com/openclaw/openclaw/pull/93265)
- [PR #92477](https://github.com/openclaw/openclaw/pull/92477)
- [PR #93480](https://github.com/openclaw/openclaw/pull/93480)
- [PR #85254](https://github.com/openclaw/openclaw/pull/85254)
- [PR #92086](https://github.com/openclaw/openclaw/pull/92086)

---

## 4. Community Hot Topics

The community is deeply engaged, with highly specific and sophisticated feedback.

- **[Issue #75] Linux/Windows Clawdbot Apps** — *109 comments, 79 👍*
  - **Link:** [Issue #75](https://github.com/openclaw/openclaw/issues/75)
  - **Analysis:** This is the single most requested feature in the project’s history. Nearly three months with no maintainer action. Users need full desktop parity with macOS, and the frustration is becoming the dominant signal about OpenClaw’s accessibility.

- **[Issue #25592] Text between tool calls leaks to messaging channels** — *32 comments, P1*
  - **Link:** [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
  - **Analysis:** A critical UX and security flaw. Internal processing output, error handling, and narration are broadcast to Slack, iMessage, and other channels. The community is demanding a “quiet execution” mode. No dedicated fix PR exists yet.

- **[Issue #9443] Prebuilt Android APK releases** — *25 comments, 2 👍*
  - **Link:** [Issue #9443](https://github.com/openclaw/openclaw/issues/9443)
  - **Analysis:** Related to #75’s platform expansion theme. Users want ready-to-install Android companion apps, not just source code.

- **[Issue #39604] Allow private network access in `web_fetch`** — *13 comments, 9 👍*
  - **Link:** [Issue #39604](https://github.com/openclaw/openclaw/issues/39604)
  - **Analysis:** A highly supported, focused config request. Enterprise and homelab users need an opt-in flag to reach internal services without breaking security defaults.

- **[Issue #10659] Masked Secrets — Prevent Agent from Accessing Raw API Keys** — *13 comments, 4 👍, P1*
  - **Link:** [Issue #10659](https://github.com/openclaw/openclaw/issues/10659)
  - **Analysis:** Prompt injection defense is top of mind. Users want the agent to *use* secrets without being able to *read* them.

- **[Issue #12602] Slack Block Kit support** — *13 comments*
  - **Link:** [Issue #12602](https://github.com/openclaw/openclaw/issues/12602)
  - **Analysis:** Users are building production workflows and need rich, interactive Slack messages (summaries, tables, action buttons).

---

## 5. Bugs & Stability

OpenClaw is currently dealing with an unusually high concentration of P1 regressions, particularly in session management and message integrity.

**Critical (P1 | Security / Data Loss / Message Loss / Crash Loop):**

| Issue | Summary | Severity | Status |
|-------|---------|----------|--------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to channels | P1, Security, Message Loss | No fix PR |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal daemon SIGUSR1 race condition (orphaned processes) | P1, Crash Loop, Message Loss | No fix PR |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent replies to previous message (context confusion) | P1, Session State, Message Loss | No fix PR |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` tool ignores `skills.entries.*.env` (regression) | P1, Regression, Security | Linked PR open |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | Write tool lacks append mode, cron jobs destroy shared files | P1, Data Loss | No fix PR |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" on Google Vertex | P1, Regression, Crash Loop | Needs live repro |
| [#40611](https://github.com/openclaw/openclaw/issues/40611) | Heartbeat drift fix causes aggressive retry, blocks Telegram | P1, Message Loss | No fix PR |
| [#41165](https://github.com/openclaw/openclaw/issues/41165) | Telegram DMs pollute `agent:main:main` session | P1, Session State, Message Loss | Needs live repro |

**High Severity (P1/P2 | Regression | Security Boundary):**
- [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI requires HTTPS/localhost (regression, P1)
- [#29387](https://github.com/openclaw/openclaw/issues/29387) – Bootstrap files in `agentDir` silently ignored (P1, Session State)
- [#31331](https://github.com/openclaw/openclaw/issues/31331) – Docker + Sandbox workspace can’t bind mount (P1)
- [#37634](https://github.com/openclaw/openclaw/issues/37634) – Sandbox `workspaceAccess: "none"` mounts workspace read-only (P1)
- [#41201](https://github.com/openclaw/openclaw/issues/41201) – Control UI Avatar broken image (regression, P2)
- [#40540](https://github.com/openclaw/openclaw/issues/40540) – `openclaw update` fails with EBUSY on Windows (P1)

**Active Fix PRs:**
- [#93480](https://github.com/openclaw/openclaw/pull/93480) – Fix core loop data loss on `before_agent_finalize` revision
- [#93276](https://github.com/openclaw/openclaw/pull/93276) – Stop plugin discovery loads from clearing active providers
- [#85403](https://github.com/openclaw/openclaw/pull/85403) – Suppress Telegram message-tool reply previews
- [#44098](https://github.com/openclaw/openclaw/pull/44098) – Add default `pidsLimit` for sandbox containers (security)

**Analysis:** The concentration of regressions in session routing (#32296, #41165, #40611) and credential propagation (#31583) suggests the recent refactors in the session isolation and environment injection layers introduced significant churn. These need urgent maintainer triage as they erode user trust in deterministic behavior.

---

## 6. Feature Requests & Roadmap Signals

**Landing Likely in the Next Release:**
- **[PR #93265] Agent-Assisted Onboarding** — RTM-ready. Solves the #1 UX complaint (confusing setup).
- **[PR #92086] Security Matrix Audit Model** — Large, well-received, advanced architectural step.
- **Platform Parity Acceleration** — With the Windows daemon PR (#68936) merged, expect movement on [#75](https://github.com/openclaw/openclaw/issues/75) and [#9443](https://github.com/openclaw/openclaw/issues/9443).

**Strong Roadmap Signals:**
- **Security & Governance:** Masked Secrets (#10659), Memory Trust Tagging (#7707), Denylist for exec approvals (#6615), Pre-response Hard Gates (#13583). The community is treating prompt injection and memory poisoning as existential threats to agent reliability.
- **Multi-Agent Coordination:** [#35203](https://github.com/openclaw/openclaw/issues/35203) (Multi-Agent Collaboration RFC) and [#43656](https://github.com/openclaw/openclaw/pull/43656) (Cross-Gateway sessions) point toward a radically more connected agent ecosystem.
- **Enterprise Readiness:** Slack Block Kit (#12602), Telegram Business (#20786), Encrypted Backup (#44111), Backup Exclusion Patterns (#40786), Feishu Card Actions (#43953).
- **UX & Efficiency:** Tiered Bootstrap Loading (#22438), Reduce Tool Schema Token Overhead (#14785), Reasoning Stream (#42276).

**Prediction:** v2026.7 will likely focus on **Onboarding + Security + Message Integrity**, as the beta workflow and P1 bugs demand stabilization before major multi-agent architecture lands.

---

## 7. User Feedback Summary

**Core Pain Points:**
- *Session/Message Integrity:* “My agent replies to the wrong message” (#32296, #25592). “Messages arrive out of order on Telegram” (#44143, #40611). These are the community’s loudest operational complaints.
- *Platform Fragmentation:* “I can’t run OpenClaw on my Windows/Linux machine or get an APK” (#75, #9443). This is the dominant barrier to adoption.
- *Setup Complexity:* “Onboarding doesn’t set up memory storage, making the bot forget everything” (#16670). “Backups are huge, fragile, and have no exclude patterns” (#40786, #13616).
- *Security Anxiety:* “My agent can read my API keys” (#10659). “The agent can’t write to its own sandbox workspace” (#37634). “Web fetch can reach my internal network without opting in” (#39604).

**Positive Signals:**
- **Deep Integration:** Users are building multi-agent A2A pipelines, complex cron jobs, cross-gateway sessions, and custom hooks in production.
- **High Sophistication:** Issues like the Security Matrix (#92086), Memory Trust Tagging (#7707), and Tiered Bootstrap Loading (#22438) demonstrate a user base operating at an advanced infrastructure level.
- **Active Contribution:** 87 PRs merged in one period shows a vibrant, capable contributor community.

---

## 8. Backlog Watch

Several high-impact items are languishing without maintainer action, creating growing community frustration.

| Issue / PR | Summary | Opened | Score | Blocking Status |
|------------|---------|--------|-------|-----------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | Jan 1 | 109 comments, 79 👍 | Needs product decision, needs security review |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) | Backup/Restore Utility | Feb 10 | 8 comments | Fix PRs exist (#44288, #44111) but stalled in “waiting on author” |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (Prevent Agent from Reading API Keys) | Feb 6 | 13 comments, 4 👍, P1 | Needs product decision, security review |
| [#16670](https://github.com/openclaw/openclaw/issues/16670) | Onboarding Wizard should include Memory/Embedding setup | Feb 15 | 8 comments | P2, largely addressed by incoming PR #93265 |
| [#20786](https://github.com/openclaw/openclaw/issues/20786) | Telegram Business Bot support | Feb 19 | 8 comments, 6 👍 | Needs security review, product decision |
| [#13469](https://github.com/openclaw/openclaw/pull/43656) | Cross-Gateway sessions_send / sessions_spawn | Mar 12 | Stale, P1 | Merging this would unlock multi-machine agent swarms |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | Feb 3 | 12 comments, P2 | Needs architectural decision; high impact for anti-poisoning |
| [#6731](https://github.com/openclaw/openclaw/issues/6731) | Safe/Unsafe “Rust rewrite” proposal | Feb 2 | 12 comments | Vocal but niche; needs product conversation |

**Watch Item:** The **Signal daemon race condition** (#22676) and **Text leaks** (#25592) are critical backlog items. Both are P1, both lack dedicated fix PRs, and both directly impact user trust in the platform’s core value proposition: reliable, private agent communication.

---

*Digest generated 2026-06-16 from public OpenClaw GitHub data. All links point to openclaw/openclaw.*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: The State of Open-Source AI Assistants
**Date:** 2026-06-16  
**Analyst:** Senior Analyst, AI Agent & Personal Assistant OSS Ecosystem

---

## 1. Ecosystem Overview

The open-source personal AI agent ecosystem has entered a phase of intense competitive differentiation, splitting cleanly into platform-scale agent servers, developer-focused agent IDEs, lightweight channel bot frameworks, and specialized collaboration tools. Unifying these diverging tracks is a shared operational crisis: every active project is struggling to balance ambitious feature velocity against fundamental stability demands in session integrity, tool execution reliability (MCP), and credential security. The ecosystem is no longer proving it can build agents—it is competing on resilience, governance, and platform-specific UX maturity. A clear four-tier hierarchy has emerged by community scale and development velocity, with OpenClaw standing alone at the top, a strong contender tier challenging its dominance, and a long tail of niche or stalled projects.

---

## 2. Activity Comparison (24h Snapshot)

| Project | Issues Updated | PRs Updated | Merged/Closed | Release Published | Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | ~500 | ~500 | 87 | v2026.6.8-beta.2 | 8/10 |
| **Hermes Agent** | ~50 | ~50 | Multiple (implied) | None (v0.16.0 since Jun 5) | 7/10 |
| **IronClaw** | ~46 | ~50 | Multiple closed | None | 8/10 |
| **ZeroClaw** | ~50 | ~50 | 1 PR + 4 Issues | None | 8/10 |
| **CoPaw (QwenPaw)** | ~50 | ~50 | 32 | None (v1.1.11.post2) | 7/10 |
| **NanoBot** | ~5 | ~26 | 5 | None | 8/10 |
| **PicoClaw** | ~3 | ~13 | 3 | v0.2.9-nightly | 7/10 |
| **NanoClaw** | ~0 | ~12 | 3 | None | 7/10 |
| **LobsterAI** | ~0 | ~11 | 5 | None | 7/10 |
| **NullClaw** | ~2 | ~1 | 0 | None | 3/10 |
| **Moltis** | ~0 | ~2 | 0 | None | 4/10 |
| **TinyClaw** | ~0 | ~0 | 0 | None | 1/10 |
| **ZeptoClaw** | ~0 | ~0 | 0 | None | 1/10 |

*Health Score: Blended assessment of development velocity, merge ratio, bug severity, and community engagement. Tier 1-2 projects cluster at 7-8, reflecting high activity balanced against regression loads. Lower scores indicate stalled development.*

---

## 3. OpenClaw's Position

**Unmatched Scope, Accumulating Platform Debt**

OpenClaw operates at a community scale without peer—its daily update volume (~500 issues and PRs) is roughly ten times that of the next tier of active projects. Its primary architectural differentiator is a structural commitment to **agent security and governance** (Masked Secrets, Security Matrix runtime audits, Trust Tagging against prompt poisoning). This makes it the default reference implementation for enterprise and compliance-heavy deployments.

**However, three vulnerabilities are emerging:**

1. **Platform Parity Gap:** The demand for Linux/Windows desktop clients (#75 — 109 comments, 79 👍) is the single highest-reacted request across the entire analyzed ecosystem. OpenClaw remains macOS/iOS-centric in a market that is rapidly demanding Desktop-first experiences.

2. **Regression Accumulation:** The project shows an unusually high concentration of P1 session-routing bugs (context confusion, Telegram DM pollution, heartbeat drift). These directly erode trust in the core value proposition of reliable agent communication.

3. **Maintainer Throughput Strain:** Despite massive contributor velocity, critical community asks (Linux desktop, masked secrets, backup utilities) languish without maintainer action for months, creating a backlog of frustration that competitors are actively capitalizing on.

OpenClaw's competitive moat increasingly depends on its **security architecture** rather than its raw feature set—a sustainable advantage if the project can stabilize its core session layer and expand platform support.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging simultaneously across multiple independent projects, indicating strong ecosystem-wide signals:

### Session Integrity & Context Fidelity
The single most painful operational issue across the landscape. Projects are independently converging on fixes for the same class of bug.
- **OpenClaw:** Context confusion, Telegram session pollution (#32296, #41165)
- **Hermes Agent:** Concurrent session cross-contamination (#46303)
- **NanoBot:** Sustained goal context loss requiring lazy continuation (#4359)
- **CoPaw:** Context compression totally destroying agent state (#5171)
- **ZeroClaw:** Ordering race conditions in session-store mutation (#7753)

### MCP Reliability & Scaling
The protocol is winning, but the ecosystem is straining against its basic stdio implementation.
- **NanoClaw:** Adds remote HTTP/SSE MCP server support (#2776)
- **ZeroClaw:** Finds `mcp_bundles` scoping is silently non-functional (#7733)
- **Hermes Agent:** MCP misconfiguration is invisible to users (#31246)
- **PicoClaw:** Systematic error-handling cleanup for MCP tool execution

### Credential Architecture Reform
Every major project is concluding that agents must not be able to read their own secrets.
- **OpenClaw:** Masked Secrets — prevent agent reading raw API keys (#10659)
- **IronClaw:** Owner-scoped credentials replacing thread-scoped approvals (#4939)
- **ZeroClaw:** OAuth credential delegation for sub-agents (#7640)

### Cross-Platform Desktop Parity
Windows and Linux support is shifting from "nice to have" to "urgently demanded."
- **OpenClaw:** #75 (109 comments) — the community's top frustration
- **Hermes Agent:** SQLite WAL corruption fix for Windows (#47007)
- **PicoClaw:** QQ channel broken on Windows (#3015)
- **CoPaw:** macOS ARM64 crash loop, Windows process leak fixes

### Cost-Aware Architecture
Context compression, token accounting, and light-model pre-checks are becoming core features.
- **CoPaw:** Compression stats discrepancy and headroom integration (#5122, #5063)
- **ZeroClaw:** `CompressionDecorator` RFC and light model pre-check requests (#7673, #6067)
- **OpenClaw:** Tool schema token overhead reduction (#14785)

---

## 5. Differentiation Analysis

| Project Category | Represented By | Core Value Proposition | Target User |
|---|---|---|---|
| **Agent Server OS** | OpenClaw, ZeroClaw | Security-first multi-agent platform with strict governance boundaries | Enterprise / Self-Hosting |
| **Agent Dev Workbench** | Hermes, IronClaw | Desktop IDE with visual workflow orchestration (Kanban, DAG) and model composition (MoA) | AI Software Engineers |
| **Channel Bot Framework** | NanoBot, CoPaw, NanoClaw | Pragmatic always-on assistant for Telegram, WeChat, WhatsApp. Rich cron/automation support | Power Users / Operators |
| **Edge/Lightweight Client** | PicoClaw | Low-resource, Go-based, broad hardware support (RISC-V) | Embedded / Performance-Critical |
| **Collaboration Platform** | LobsterAI | Realtime async interaction, voice-first, document artifact sharing | Team Collaboration |
| **Niche / Inactive** | NullClaw, Moltis, TinyClaw, ZeptoClaw | Small or stalled projects with increasingly commoditized feature sets | Niche / At-Risk |

**Key Architectural Differences:**
- **Security Model:** Only OpenClaw and ZeroClaw treat *the agent reading its own configuration* as a threat requiring cryptographic separation. Others rely on sandboxing.
- **Concurrency Model:** Hermes (DAG-based parallel wave execution) and OpenClaw (cross-gateway sessions) provide the most sophisticated multi-agent primitives.
- **Local Model Support:** NullClaw differentiates on Ollama streaming, while others focus primarily on cloud API providers.
- **Ecosystem Lock-In:** CoPaw is deeply tied to the Chinese LLM ecosystem (Qwen, XiaoYi, WeChat Work), providing channels and model support not prioritized elsewhere.

---

## 6. Community Momentum & Maturity

### Tier 1: The Reference Implementation
**OpenClaw.** Unrivaled in scale but burdened by platform debt and regression load. Its moat is security architecture; its risk is being outflanked on UX and platform support by Tier 2.

### Tier 2: The High-Velocity Challengers
**Hermes, IronClaw, ZeroClaw, CoPaw.** 50+/50+ daily issue/PR velocity with multiple merges. They are actively capturing the market segments OpenClaw cannot serve efficiently.
- **Hermes** is the strongest competitor in the Developer Workbench space. A v0.16.1 hotfix is imminent to address post-release regressions.
- **ZeroClaw** has the most ambitious long-term roadmap (v0.9.0 security/multi-tenancy, Wasm-first build, A2A discovery).
- **CoPaw** dominates the Chinese market channel integrations but suffers from regression fatigue after v1.1.11.post2.

### Tier 3: The Specialist Workhorses
**NanoBot, PicoClaw, NanoClaw, LobsterAI.** Lower volume but high merge ratios and cleaner stability profiles. They serve specific, defensible niches with strong contributor communities.
- **NanoBot** stands out for its incredibly efficient contributor-driven development (high merge-to-issue ratio).
- **PicoClaw** and **NanoClaw** are clearing quality backlog effectively.

### Tier 4: Inactive / At-Risk
**NullClaw, Moltis, TinyClaw, ZeptoClaw.** Minimal engagement, no maintainer response to bugs. Their feature sets are increasingly subsumed by Tier 1-3 projects. Unlikely to remain viable as independent projects without intervention.

---

## 7. Trend Signals

### MCP is Winning, But the Cargo Cult is Over
Implementing MCP is no longer a differentiator—it is table stakes. The competitive differentiator is now **MCP reliability**: remote server support, error propagation to the user, and runtime enforcement of tool scoping. Projects that treat MCP as a simple checkbox (ZeroClaw's `mcp_bundles` silent no-op is a cautionary tale) will lose developer trust.

### Trust Architecture is the New Moat
The ecosystem-wide convergence on Masked Secrets, audit trails, sandboxing, and prompt-injection detection signals a fundamental shift. Users are demanding agents that are *provably* safe, not just functionally capable. OpenClaw's Security Matrix (#92086) and ZeroClaw's per-agent prompt injection override (#7749) represent the leading edge of this trend.

### The Desktop Client is the New CLI
Terminal-based UIs are becoming insufficient for professional users. The surge in desktop-related issues (Hermes Desktop run history, OpenClaw Windows daemon, CoPaw macOS crash loop, IronClaw WebChat v2) proves that packaging as a native application is critical for mainstream adoption and enterprise credibility.

### The Cost of Reasoning is Reshaping Architecture
As agentic workloads increase, token budgets are hitting hard limits. Features like context compression algorithms, lightweight pre-check models, and token usage transparency are shifting from "optimizations" to **core UX requirements**. The projects that manage cost best will win price-sensitive deployment scenarios.

### Windows is the New macOS
For two years, macOS dominated agent development. The data today shows an ecosystem scrambling to fix Windows-specific bugs (SQLite corruption, process leaks, daemon support). The enterprise runs on Windows, and the agent platforms that deliver a first-class Windows experience will capture a massive underserved market that OpenClaw's macOS bias leaves exposed.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot Project Digest – 2026-06-16**

---

### 1. Today's Overview
Activity remains exceptionally high, with **26 Pull Requests** and **5 Issues** updated in the last 24 hours. The development focus is split between enriching the WebUI as a complete management interface (automations, configuration parity) and hardening provider reliability (empty response handling, audio transcription, token counting). No releases were cut today, indicating the project is consolidating a large wave of bug fixes and community contributions into a prepared milestone. The project health is strong, evidenced by the rapid pace of contributor-driven fixes addressing regression bugs filed earlier this week.

---

### 2. Releases
No new releases were published today. The project is currently in a high-velocity feature and bug-fixing cycle.

---

### 3. Project Progress
Five PRs were merged or closed in the last 24 hours, primarily addressing critical session and agent stability regressions:
- **Session Context Fix ([PR #4359](https://github.com/HKUDS/nanobot/pull/4359)):** Resolved the widely reported "sustained goal" context loss (Issue #4286) by implementing lazy goal continuation evaluation, preventing agents from forgetting long-running task context.
- **History Trimming Fix ([PR #4348](https://github.com/HKUDS/nanobot/pull/4348)):** Corrected the idle auto-compaction logic that was incorrectly stripping user turns from the conversation history.
- **API Endpoint Correctness ([Issue #4309](https://github.com/HKUDS/nanobot/issues/4309)):** The bug where `/v1/chat/completions` returned hardcoded zero token usage was closed, improving OpenAI-compatible API parity.

---

### 4. Community Hot Topics
- **Installer Blocking New Users ([Issue #4360](https://github.com/HKUDS/nanobot/issues/4360)):** A fresh Debian Docker container fails installation with a shell syntax error (`end of file unexpected`). This is a high-priority blocker for new evaluations and currently lacks a fix PR.
- **Empty Response Fallback Reliability ([Issue #4287](https://github.com/HKUDS/nanobot/issues/4287)):** Users report that when DeepSeek returns empty responses, NanoBot fails to trigger fallback models. The proposed fix ([PR #4358](https://github.com/HKUDS/nanobot/pull/4358)) ensures retries don't log duplicate user turns.
- **WebUI Maturation ([PR #4330](https://github.com/HKUDS/nanobot/pull/4330) & [PR #4313](https://github.com/HKUDS/nanobot/pull/4313)):** The community is actively pushing the WebUI toward feature parity with the JSON configuration. PR #4330 adds a full automation management view (listing, running, pausing automations), while PR #4313 adds write endpoints for settings like temperature, memory, and tool limits. These represent the strongest signals for the project's immediate roadmap.

---

### 5. Bugs & Stability

**Critical / Blocker:**
- **Docker Installer Crash ([Issue #4360](https://github.com/HKUDS/nanobot/issues/4360)):** The installer aborts with a shell syntax error. No fix PR exists yet. High impact on onboarding.
- **Image Path Leak ([PR #4346](https://github.com/HKUDS/nanobot/pull/4346)):** The provider-agnostic image stripping fallback previously leaked local file paths to users in error messages. Fix submitted.

**High Priority:**
- **Empty Response Handling ([PR #4358](https://github.com/HKUDS/nanobot/pull/4358)):** Models returning empty completions silently bypass the fallback mechanism. Fix submitted.
- **MCP Server Crash on Reconnect ([PR #4303](https://github.com/HKUDS/nanobot/pull/4303)):** Asynchronous task lifecycle mismanagement causes a hard crash when `streamableHttp` MCP servers reconnect. Fix submitted (needs review).

**Medium Priority:**
- **Audio Transcription Failure ([PR #4353](https://github.com/HKUDS/nanobot/pull/4353)):** Raw `.ogg`/`.opus` voice notes from WhatsApp fail on some STT providers. Fix submitted by converting to WAV 16k mono.
- **Context Digest Over-Truncation ([PR #4352](https://github.com/HKUDS/nanobot/pull/4352)):** History digest capped by character count (~32k chars) instead of tokens, causing issues with CJK text. Fix submitted.
- **Anthropic Tool ID Rejection ([PR #4356](https://github.com/HKUDS/nanobot/pull/4356)):** Tool IDs with special characters (pipes, dots) were rejected by the Anthropic API. Fix submitted.
- **Session Key NameError ([Issue #4322](https://github.com/HKUDS/nanobot/issues/4322)):** `NameError: name 'session_key' is not defined` crash after a merge. Marked stale, awaiting triage.

---

### 6. Feature Requests & Roadmap Signals
Several major features in the pipeline strongly indicate the direction of the next release:
- **WebUI as Primary Interface:** The push toward full WebUI/config parity ([PR #4313](https://github.com/HKUDS/nanobot/pull/4313)) and a dedicated Automation management view ([PR #4330](https://github.com/HKUDS/nanobot/pull/4330)) signals a shift toward GUI-first configuration.
- **Provider and Search Expansion:**
    - Full Mistral adapter support with proper parameter validation ([PR #4351](https://github.com/HKUDS/nanobot/pull/4351)).
    - Kimi K2.7 thinking model support ([PR #4361](https://github.com/HKUDS/nanobot/pull/4361)).
    - Keenable as a new integrated web search provider ([PR #4350](https://github.com/HKUDS/nanobot/pull/4350)).
- **Granular Agent Control:** "Silent" cron jobs ([PR #4357](https://github.com/HKUDS/nanobot/pull/4357)) allow scheduled tasks to act only when reporting results. Tool-specific model preset switching ([PR #4347](https://github.com/HKUDS/nanobot/pull/4347)) provides power-user flexibility.
- **Observability:** A new `tools.audit` config module ([PR #4320](https://github.com/HKUDS/nanobot/pull/4320)) for logging agent actions, flagging a move toward enterprise-grade auditing.

---

### 7. User Feedback Summary
- **Satisfaction:** The community is highly technical and deeply engaged. Users frequently convert their own bug reports into code contributions (chengyongru, franciscomaestre, La-Volpe, Re-bin, BearMett), signaling strong project stickiness.
- **Dissatisfaction:** User friction concentrates at system boundaries: **initial setup** (Docker installer broken), **LLM API edge cases** (DeepSeek empty responses, Anthropic tool ID patterns), and **session fidelity** (context loss, replay window truncation).
- **Use Cases:** Deployments are production-oriented: autonomous Telegram bot assistants, long-form article generation, scheduled monitoring, and multi-modal messaging (WhatsApp/Feishu). Users strongly depend on reliable long-term context and background execution.

---

### 8. Backlog Watch
The following items require prompt maintainer review:
- **[Issue #4322](https://github.com/HKUDS/nanobot/issues/4322) – Session Key Regression:** Marked stale. A user reports an unresolvable `NameError` after merging latest `main`. Likely a subtle merge-resolution bug needing a quick diagnosis.
- **[PR #4303](https://github.com/HKUDS/nanobot/pull/4303) – MCP Server Crash Fix:** Unreviewed for 5 days. A critical stability fix preventing hard crashes on server reconnection for `streamableHttp` MCP setups.
- **[Issue #4360](https://github.com/HKUDS/nanobot/issues/4360) – Docker Installer Failure:** Fresh issue, high severity. Blocks all new user evaluation paths and warrants immediate triage.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is a structured project digest for Hermes Agent based on the provided GitHub data.

---

## Hermes Agent Project Digest — 2026-06-16

### 1. Today’s Overview
Hermes Agent exhibits extremely high development velocity, with activity recorded on 50 Issues and 50 Pull Requests in the last 24 hours, though no new release was cut today. The project is clearly in a heavy stabilization phase following the v0.16.0 launch, with several critical regressions (SQLite initialization, Desktop Run History, session isolation) reported and actively debated. Concurrently, major infrastructure work continues, particularly around a new DAG-based multi-agent orchestration engine and refinements to the Kanban workflow error handling. Overall project health is strong, characterized by rapid iteration and deep community engagement, though the high volume of immediate post-release bugs signals an urgent need for a targeted hotfix patch.

### 2. Releases
**None.** No new releases were published today (current version remains v0.16.0 from 2026-06-05). Given the volume of regressions identified—including database crashes and missing UI features—a v0.16.1 hotfix release seems imminent.

### 3. Project Progress
**Merged/Closed PRs:**
- **[[CLOSED] #46958](https://github.com/NousResearch/hermes-agent/pull/46958) — Hide hosted dashboard update controls**: Improves containerized deployment UX by hiding update buttons and guarding backend update endpoints when running inside a detected container environment.

**Key Features and Fixes Advanced via New PRs:**
- **Multi-Agent Orchestration**: [[PR #47016]](https://github.com/NousResearch/hermes-agent/pull/47016) introduces a full DAG TaskGraph with DFS cycle detection and parallel wave execution, building heavily on the architectural groundwork laid in [[PR #12436]](https://github.com/NousResearch/hermes-agent/pull/12436).
- **Kanban Error Handling Overhaul**: [[PR #46985]](https://github.com/NousResearch/hermes-agent/pull/46985) and [[PR #47005]](https://github.com/NousResearch/hermes-agent/pull/47005) directly target the widely-criticized "protocol violation" error by surfacing the actual worker failure reason and properly aging out stale diagnostics.
- **Windows Stability**: [[PR #47007]](https://github.com/NousResearch/hermes-agent/pull/47007) forces SQLite into `DELETE` journal mode to prevent WAL corruption during abnormal shutdowns—a major pain point for Desktop users.
- **MCP Server UX**: [[PR #47013]](https://github.com/NousResearch/hermes-agent/pull/47013) fixes the long-standing issue of spawning visible, never-closing console windows on Windows when launching MCP servers via `npx` or `.cmd`.
- **Desktop UI Polish**: [[PR #46959]](https://github.com/NousResearch/hermes-agent/pull/46959) introduces a composer-level model selector (anchored to the mic button), per-model presets, and fixes silent provider disconnect failures.

### 4. Community Hot Topics
The following discussions reflect the most significant community activity and underlying user needs:

- **[[#7237]](https://github.com/NousResearch/hermes-agent/issues/7237) — Response truncated due to output length limit** (50 Comments, 6 👍)
  *Status:* CLOSED. This was the dominant discussion. The community heavily criticized the hard output ceiling in CLI and chat interfaces that breaks long-form responses mid-stream. The volume of comments suggests significant user frustration with losing work; its closure today indicates a mitigation has been deployed.
- **[[#22620]](https://github.com/NousResearch/hermes-agent/issues/22620) — Skill list bloat causes massive context window inflation** (5 Comments)
  Users with large skill libraries are facing severe context overhead. The demand for "vector-based skill routing or lazy loading" highlights a sophisticated user base requiring scalable, intelligent knowledge retrieval rather than brute-force insertion.
- **[[#18715]](https://github.com/NousResearch/hermes-agent/issues/18715) — Support remote Hermes agent with local tool execution** (4 Comments, 15 👍)
  The highest-voted open feature request. The community strongly desires a split architecture (LLM on GPU server, tools on local machine). This is the clearest gap in the current deployment model.
- **[[#27178]](https://github.com/NousResearch/hermes-agent/issues/27178) / [[#46593]](https://github.com/NousResearch/hermes-agent/issues/46593) — Kanban “protocol_violation” errors** (6 Combined Comments)
  Multiple users independently reported the same opaque failure mode where Kanban workers exit silently. The unified feedback is that "protocol violation" is useless for debugging. The project responded today with direct fix PRs (#46985, #47005).

### 5. Bugs & Stability
Several critical regressions and high-impact bugs were reported or updated today. Fix PRs are noted where applicable.

**Critical (P1):**
- **[[#47002]](https://github.com/NousResearch/hermes-agent/issues/47002) — `SessionDB.__init__` crashes on SQLite without trigram tokenizer** (v0.16.0 Regression): A blocker for users with specific SQLite builds. No explicit fix PR linked yet.
- **[[#40691]](https://github.com/NousResearch/hermes-agent/issues/40691) — Telegram Gateway freezes after polling conflict recovery** (Open since June 6): The gateway becomes a silent zombie. Remains without a known fix PR.
- **[[#46675]](https://github.com/NousResearch/hermes-agent/issues/46675) — Max OAuth requests rejected as third-party (HTTP 400 "extra usage")**: Blocks all Anthropic Max users from using tools due to the `mcp_` tool-name prefix. A critical provider integration issue.

**High (P2):**
- **[[#46303]](https://github.com/NousResearch/hermes-agent/issues/46303) — Concurrent sessions cross-contaminate**: No memory or git worktree isolation between concurrent sessions. High severity for power users.
- **[[#46979]](https://github.com/NousResearch/hermes-agent/issues/46979) — Desktop Run History empty for agent cron jobs** (v0.16.0 Regression): A core UI feature is broken despite the backend API returning correct data.
- **[[#46934]](https://github.com/NousResearch/hermes-agent/issues/46934) — Stale `resume_pending` sessions bypass idle reset**: Creates "zombie sessions" that replicate context bleed after gateway restarts.
- **[[#31246]](https://github.com/NousResearch/hermes-agent/issues/31246) — MCP server misconfiguration is invisible** (Open since May 24): Silent failures when MCP setup is wrong; errors are logged only at DEBUG level and never reach the user.

**Fix PRs Available:** [#47007](https://github.com/NousResearch/hermes-agent/pull/47007) (Windows WAL corruption), [#47013](https://github.com/NousResearch/hermes-agent/pull/47013) (MCP console windows), [#47010](https://github.com/NousResearch/hermes-agent/pull/47010) (custom endpoint models), [#47008](https://github.com/NousResearch/hermes-agent/pull/47008) (Discord URL safety).

### 6. Feature Requests & Roadmap Signals
Today’s submissions and engagements provide strong signals for the project's direction:

- **Multi-Agent Orchestration as the Flagship Build**: The submissions of [[PR #47016]](https://github.com/NousResearch/hermes-agent/pull/47016) alongside [[PR #12436]](https://github.com/NousResearch/hermes-agent/pull/12436) signal a major strategic investment in structured, parallel agent workflows. This is almost certainly the centerpiece of the next major release (v0.17+).
- **Model Composition as a Service**: [[PR #46081]](https://github.com/NousResearch/hermes-agent/pull/46081) and [[PR #46094]](https://github.com/NousResearch/hermes-agent/pull/46094) elevate MoA and Fusion presets to first-class virtual providers, positioning Hermes as a meta-orchestrator over a swarm of models.
- **Desktop as a Professional Client**: Features like per-model presets ([#46959](https://github.com/NousResearch/hermes-agent/pull/46959)), font size settings ([[#46097]](https://github.com/NousResearch/hermes-agent/issues/46097)), and per-call delegation overrides ([[#47014]](https://github.com/NousResearch/hermes-agent/issues/47014)) signal a push toward a high-quality, power-user desktop experience.
- **Community Needs**: Requests for better proxy support for Chinese users ([[#46839]](https://github.com/NousResearch/hermes-agent/issues/46839)), custom models during onboarding ([[#47006]](https://github.com/NousResearch/hermes-agent/issues/47006)), and a remote agent architecture ([[#18715]](https://github.com/NousResearch/hermes-agent/issues/18715)) highlight the need to support diverse, non-standard deployments.

### 7. User Feedback Summary
- **Dissatisfaction & Pain Points:**
  - **v0.16.0 Regressions:** Users immediately reported broken Desktop features and database initialization errors. Trust in the latest stable release is currently strained.
  - **Workflow Opacity:** The Kanban system’s "protocol violation" error is a consistent source of frustration. Users want actionable debugging information rather than generic failure codes.
  - **Deployment Rigidity:** The lack of a remote agent/local tools architecture and poor proxy handling are actively blocking advanced enterprise and international users.
- **Satisfaction & Use Cases:**
  - The community remains deeply technical and engaged, filing detailed reports on complex topics like DAG orchestration, MCP configuration, and session isolation.
  - There is strong trust in the project's rapid iteration cycle, evidenced by the high volume of constructive feature requests despite the current bug surge.
  - The "Beings" mechanic ([[#46917]](https://github.com/NousResearch/hermes-agent/issues/46917)) and Kanban workflows show deep, sophisticated usage of the agent's customization capabilities.

### 8. Backlog Watch
Several critical or highly-demanded items remain open without a clear maintainer resolution:

- **[[PR #10707]](https://github.com/NousResearch/hermes-agent/pull/10707) (April 16, P2): `fix(cli): honor config base_url for openrouter`** — A simple but vital fix for users behind OpenRouter proxies. Needs review.
- **[[#18715]](https://github.com/NousResearch/hermes-agent/issues/18715) (May 2, 15 👍): `Support remote agent with local tools`** — The highest-reacted feature request. Needs an official roadmap response or assignment.
- **[[#22620]](https://github.com/NousResearch/hermes-agent/issues/22620) (May 9): `Skill list bloat context inflation`** — A fundamental architectural scalability question that affects all power users.
- **[[#31246]](https://github.com/NousResearch/hermes-agent/issues/31246) (May 24, P2): `MCP misconfiguration invisible`** — A high-impact UX gap for the server plugin system.
- **[[PR #32663]](https://github.com/NousResearch/hermes-agent/pull/32663) (May 26): `fix(openviking): sanitize skill memory input`** — Awaiting maintainer review.
- **[[#40691]](https://github.com/NousResearch/hermes-agent/issues/40691) (June 6, P1): `Telegram Gateway freezes`** — A critical P1 issue with no fix PR in sight. The longest-running critical bug currently active.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-16

## 1. Today’s Overview

PicoClaw is firmly in a **code quality and security hardening sprint**. The repository logged 13 PRs and 3 issues updated in the past 24 hours, culminating in a new nightly build (`v0.2.9-nightly`). Activity is heavily weighted toward the open PR queue (10 open), where a wave of low-level Go hygiene fixes—explicit error handling for `Close()`, `Marshal`, type assertions, and goroutine panic recovery—dominates the board. A critical security advisory concerning the launcher's `allowed_cidrs` bypass was resolved and followed up with diagnostic improvements. Community feature contributions continue to accumulate in the backlog awaiting maintainer review, suggesting a healthy but slightly strained review pipeline.

## 2. Releases

A single release was published:

- **Nightly Build `v0.2.9-nightly.20260616.c1ff5aa6`**  
  [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  Automated build tagging the current state of `main`. No breaking changes or migration notes are documented; the standard nightly caveat ("may be unstable") applies. The delta against the last stable tag (`v0.2.9`) is actively expanding as the code-cleanup wave lands.

## 3. Project Progress

Three pull requests were merged or closed in the reporting window:

- **PR #3126 [CLOSED]** — `fix(web): improve launcher allowlist bypass diagnostics`  
  Directly addresses lessons from the security advisory (#3069), adding startup logging for `allow_localhost_bypass` state.  
- **PR #3096 [CLOSED]** — `docs: add PicoPaw banners to READMEs`  
  A branding/docs update.  
- **PR #3097 [CLOSED]** — `feat: add shift-enter hint below chat composer`  
  A small but user-facing Web UI improvement adding a visible newline shortcut hint.

The broader **open PR landscape** reveals the true current focus: a systematic cleanup of error handling and crash safety. Multiple PRs authored by `chengzhichao-xydt` explicitly acknowledge previously ignored errors across:
- TTS I/O (`#3129`)
- Directory file descriptors (`#3127`)
- HTTP response bodies in search providers (`#3128`)
- Seahorse grep/expand marshal errors (`#3130`)

A complementary batch adds `ok` checks to unsafe type assertions in the LINE channel (`#3054`) and the tools registry (`#3131`). Finally, **PR #3132** adds `defer-recover` protection to critical-path goroutines, preventing a single panic from crashing the entire process—a significant stability improvement.

## 4. Community Hot Topics

- **[Security Advisory #3069 [CLOSED]](https://github.com/sipeed/picoclaw/issues/3069)** — `allowed_cidrs` bypass via same-host reverse proxy  
  The highest-impact discussion of the week. The issue was reported by `YLChen-007` and triggered immediate action. While the root cause fix itself is not explicitly visible in today's merge list, the diagnostic improvements landed today.  
- **[Issue #3015 [OPEN]](https://github.com/sipeed/picoclaw/issues/3015)** — QQ Channel connection failure on Windows  
  3 comments, authored by `cuandada`. The token retrieval timeout bug persists with no fix PR attached. A clear pain point for the Windows-based Chinese user segment.  
- **Issue #2887 [CLOSED - Stale]** — `.deb` version on RISC-V not functional with OpenAI  
  10 comments over a month. Closed due to inactivity from the reporter, but the underlying desire for RISC-V support is real and lingered in discussion.

## 5. Bugs & Stability

| Severity | Issue | Status | Fix |
|---|---|---|---|
| **Critical** | Security: `allowed_cidrs` bypassable (#3069) | **Closed** | Diagnostics improved (#3126) |
| **High** | Crash risk: unprotected goroutines | **Open, fix ready** | PR #3132 (panic recovery) |
| **High** | Platform: QQ channel broken on Windows (#3015) | **Open, stale** | No fix PR |
| **Medium** | Data safety: ignored `Close()` errors could mask I/O failures | **Open, fix ready** | PRs #3127, #3128, #3129, #3059 |
| **Medium** | Data integrity: silent `json.Marshal` failures in Seahorse tools | **Open, fix ready** | PR #3130 |
| **Medium** | Panic risk: unsafe type assertions in LINE channel & registry | **Open, fix ready** | PRs #3054, #3131 |
| **Low** | Platform: RISC-V .deb not functional (#2887) | **Closed - Stale** | — |

The stability story for the day is overwhelmingly positive: **a raft of ready-to-merge fixes exists for nearly every open stability concern**. The only unattended high-severity item is the QQ Channel connectivity issue.

## 6. Feature Requests & Roadmap Signals

- **Telegram: Reply-to-bot as mention** ([PR #2975](https://github.com/sipeed/picoclaw/pull/2975), authored by `Jlan45`)  
  Currently pending review. Treats replying to a bot message in group chats as equivalent to a mention (`@bot`). This is a mature, user-contributed feature that directly addresses a popular request for group chat UX.  
- **Web UI: Shift+Enter hint** ([PR #3097](https://github.com/sipeed/picoclaw/pull/3097), **merged**)  
   Already landed—a small but thoughtful UX polish for the chat composer.  
- **Session history improvements** ([PR #3047](https://github.com/sipeed/picoclaw/pull/3047), open)  
  A detail-only JSONL reader that surfaces archived messages in session detail views, while keeping the list endpoint light. This unblocks users who rely on session history review.

Given the heavy weight of stability PRs, the **Telegram feature (#2975)** is the strongest candidate for the next minor release, assuming the team clears the review backlog.

## 7. User Feedback Summary

- **Satisfaction drivers:** The transparent and rapid handling of the security advisory (#3069) is a strong trust signal. The UX improvement in the Web chat composer was immediately delivered.  
- **Pain points (unresolved):**  
  - QQ Channel users on Windows are blocked by a persistent token timeout ([#3015](https://github.com/sipeed/picoclaw/issues/3015)).  
  - RISC-V users faced a broken `.deb` and the issue was closed as stale ([#2887](https://github.com/sipeed/picoclaw/issues/2887)). The underlying gap for this platform remains.  
- **General sentiment:** The project maintains an active core developer presence handling bugs, but community feature contributions face mounting review latency.

## 8. Backlog Watch

Several items risk losing momentum due to lack of maintainer interaction:

1. **PR #2975 — Telegram `mention` via reply**  
   *17 days open, 0 maintainer comments in data.* A polished feature from an external contributor at risk of going stale.

2. **PR #3047 — Full JSONL history for session detail**  
   *9 days open.* Adds meaningful history browsing capability; no visible review feedback yet.

3. **PR #3059 — Explicitly ignore Close() errors in error paths / retry loops**  
   *8 days open.* Part of the broader code hygiene push—should be relatively low-risk to merge.

4. **Issue #3015 — QQ Channel connection failure on Windows**  
   *10 days open.* The only open bug without an associated fix PR. If the team lacks a Windows maintainer, a repro request or community contribution callout would prevent this from becoming a stale frustration point.

The **stale bot** appears to be correctly tagging long-dormant items (e.g., #2887), but active engagement from the core team on the open PR queue will be critical to sustaining community contributor momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the structured NanoClaw project digest for 2026-06-16.

---

## NanoClaw Project Digest — 2026-06-16

### 1. Today’s Overview
NanoClaw saw moderate but focused activity over the past 24 hours, with **12 pull requests updated** and **3 merged/closed**. No new issues were filed, and no new releases were published. The project’s health is stable, with maintainers actively reviewing long-standing fix PRs and merging important reliability improvements. Activity was concentrated on fixes for silent errors (budget exhaustion, media routing, channel setup) and foundational infrastructure for remote MCP server support, indicating the project is maturing toward broader third-party tool integration.

---

### 2. Releases
**None.** No new versions were tagged today.

---

### 3. Project Progress
Three pull requests were closed/merged today, all by **Koshkoshinsk**:

*   **Automatic OneCLI Gateway Upgrades ([PR #2774](nanocoai/nanoclaw PR #2774)) – *merged***: The `update-nanoclaw` process now checks version pins in `versions.json` and automatically upgrades the `onecli-gateway` and `onecli-cli` when they shift. This closes a gap where new code could silently fail against a stale gateway.

*   **Per-Thread Codex Conversation Archive ([PR #2772](nanocoai/nanoclaw PR #2772)) – *merged*** (CDX-004): Fixes fragmented conversation history in Codex. Instead of writing one file per exchange (scattering context across hundreds of files), archives are now keyed on thread/continuation IDs, appending each exchange into a single coherent transcript.

*   **Docs cleanup for add-codex ([PR #2773](nanocoai/nanoclaw PR #2773)) – *merged***: Removed a redundant non-interactive TTY warning from the authentication note in the `add-codex` skill documentation.

---

### 4. Community Hot Topics
No individual issues or PRs generated high comment counts, but the following PRs represent the most active community-driven work:

*   **Remote MCP and Strava Skill (clementdecoligny):** Two linked PRs—[#2776](nanocoai/nanoclaw PR #2776) (HTTP/SSE MCP server support) and [#2777](nanocoai/nanoclaw PR #2777) (Strava MCP skill)—show strong demand for consuming external, hosted MCP servers. The Strava skill serves as both a practical integration and a reference implementation for remote MCP.

*   **Long-Brewing Fixes Unstuck (eldar702):** Three issues from late May—[#2626](nanocoai/nanoclaw PR #2626) (Signal restart), [#2627](nanocoai/nanoclaw PR #2627) (Reaction emoji handling), and [#2628](nanocoai/nanoclaw PR #2628) (CLI `--id` flag)—all received maintainer updates today after weeks of inactivity. This signals a maintainer push to clear the quality backlog.

*   **Budget Error Handling ([PR #2759](nanocoai/nanoclaw PR #2759)):** This open fix by **assapin** (updated today) addresses a high-impact silent failure where agent-runner drops billing/token-exhausted turns instead of delivering them to the user. It has drawn attention from users relying on budget-managed agents.

---

### 5. Bugs & Stability
No new issues were filed today, but several open PRs target critical stability bugs:

*   **Critical — WhatsApp Media Routing ([#2778](nanocoai/nanoclaw PR #2778)):** Inbound media (images, video, audio, documents) never reaches the agent. `downloadInboundMedia` writes files to the host’s `data/attachments/` directory, but agent containers only mount the per-session directory. Fix PR is open by **IamAdamJowett**.

*   **High — Silent Budget/Termination Errors ([#2759](nanocoai/nanoclaw PR #2759)):** The agent-runner drops LLM error turns (e.g., Anthropic token exhaustion or budget caps) instead of surfacing them to the user. This causes users to think agents are frozen when they are only out of budget. Fix PR is open.

*   **High — Signal Channel Setup Failure ([#2626](nanocoai/nanoclaw PR #2626)):** `restartService()` silently no-ops if a prior `launchctl unload` was run, breaking the Signal channel setup wizard. Fix PR is open.

*   **Medium — Cross-Platform Reaction Emoji ([#2627](nanocoai/nanoclaw PR #2627)):** The MCP `add_reaction` tool sends shortcodes verbatim, but only Slack expects them—WhatsApp, Discord, Telegram, and GChat require unicode. Reactions fail silently on most channels. Fix PR is open.

*   **Low/Usability — CLI `--id` Ignored ([#2628](nanocoai/nanoclaw PR #2628)):** The `ncl groups create` flag `--id` is documented but silently replaced by a random UUID, causing significant user confusion.

---

### 6. Feature Requests & Roadmap Signals
The following signals point to near-term architectural shifts:

*   **🔮 Near-term / Likely Next Release:**
    *   **Remote HTTP/SSE MCP Servers ([#2776](nanocoai/nanoclaw PR #2776)):** Extending `McpServerConfig` to a union type supporting remote (HTTP/SSE) servers alongside existing stdio. This unblocks cloud-hosted MCP tools and is the largest infrastructure lift in the current queue.
    *   **Strava MCP Integration ([#2777](nanocoai/nanoclaw PR #2777)):** A new `/add-strava` skill with OAuth flow, token management, and auto-refresh. Likely a marquee feature for the next minor release.
    *   **Container Performance Tuning ([#2771](nanocoai/nanoclaw PR #2771)):** Adding `--shm-size=1g` and `--init` to agent container run args to fix Chromium crashes in `agent-browser`. This addresses concrete user pain around browser stability.

*   **🔭 Long-term Signals:**
    *   **Multi-modal Media Architecture**: The WhatsApp media fix (#2778) exposes a deeper architectural issue about how the host and agent containers share file access. A general solution may be needed going forward.
    *   **OneCLI as a Formal Dependency**: The merged gateway upgrade feature (#2774) suggests the OneCLI integration is becoming deeply embedded, possibly warranting its own lifecycle management.

---

### 7. User Feedback Summary
Derived from the nature of PRs submitted and updated today:

*   **Pain Points:** Silent errors are the dominant source of frustration. Users report agents “going quiet” when budgets are exhausted (#2759), media disappearing into unmapped directories (#2778), and channel setup failing with zero feedback (#2626). Configuration mistrust persists due to the `--id` flag silently being ignored (#2628).
*   **Use Cases:** The community relies on NanoClaw for multi-channel messaging agents (WhatsApp, Slack, Signal), fitness/health tooling (Strava), and automated web browsing (Chromium). The push for HTTP/SSE MCP support indicates demand for integrating external SaaS tools beyond the local stdio scope.
*   **Satisfaction / Engagement:** The project benefits from a technically sophisticated contributor base. The fact that users like **eldar702** and **clementdecoligny** submit complete, production-ready fix PRs rather than simple bug reports underlines strong developer buy-in. Maintainer responsiveness to these contributions appears to be improving, as evidenced by today’s review activity on previously stalled PRs.

---

### 8. Backlog Watch
The following long-unanswered or high-severity PRs require attention:

*   **🚨 #2628 — CLI `--id` flag ignored** (eldar702, opened May 27)
    *   *Status:* Updated by maintainer today, suggests imminent review.
    *   *Impact:* Core CLI usability bug affecting every `ncl groups create` command.

*   **🚨 #2627 — MCP Reaction emoji transcoding** (eldar702, opened May 27)
    *   *Status:* Updated today by maintainer.
    *   *Impact:* Cross-channel feature parity for reactions.

*   **🚨 #2626 — Signal `restartService` silent failure** (eldar702, opened May 27)
    *   *Status:* Updated today by maintainer.
    *   *Impact:* Blocks reliable Signal channel installation.

*   **⚠️ #2759 — Budget error turns dropped** (assapin, opened June 14)
    *   *Status:* Updated yesterday.
    *   *Impact:* High severity for production deployments relying on budget enforcement. Needs prioritization for merge alongside the maintainer’s backlog clear.

*   **⚠️ #2778 — WhatsApp media routing** (IamAdamJowett, opened today)
    *   *Status:* Brand new, high visibility.
    *   *Impact:* Blocks all multimodal agent interactions over WhatsApp. Immediate triage needed.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest | 2026-06-16**

### 1. Today's Overview
NullClaw experienced a quiet day on June 16, 2026, with no new releases or merged code. Community activity was limited to two open issues and one automated dependency pull request. While the issues highlight friction in two core use cases—local model support and agent runtime configuration—no direct maintainer engagement was observed on the public threads. The lack of merged fixes or feature commits suggests the project may be in an internal development or stabilization phase, though the absence of maintainer response to active bugs is a concern for project health.

### 2. Releases
No new versions were published today. The project’s Latest Releases section is empty.

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours.
- **PR #956** [OPEN]: `[dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24` (Author: Dependabot). This is a routine automated infrastructure update maintaining Docker image security. It indicates active CI/dependency monitoring but no manual feature or bugfix integration occurred today.

### 4. Community Hot Topics
The two open issues represent the entirety of public user engagement:
- **Issue #957** – **Rate limit issue** (Author: `jacktang`): The user is running NullClaw as a stateless agent runtime with JSON output and hitting “The config reader hit a rate limit” error. This points to a documentation gap or non-intuitive default behavior for the config reader’s rate limiter. Underlying need: clear documentation on threshold values or a user-configurable parameter exposed in the runtime mode. → [View Issue](https://github.com/nullclaw/nullclaw/issues/957)
- **Issue #952** – **Local model using ollama returns incomplete answers** (Author: `bloodgroup-cplusplus`): A critical functional bug where NullClaw provides truncated responses when using Gemma via the Ollama backend. With a screenshot showing incomplete sentences, this is a top concern for users relying on local model inference. → [View Issue](https://github.com/nullclaw/nullclaw/issues/952)

### 5. Bugs & Stability
Two bugs were discussed today, ranked by severity:
1.  **Critical** – **Issue #952 (Local model truncation)**: The agent fails to deliver complete output when paired with a local Ollama model. This is a fundamental functional regression for the local model workflow. No fix PR currently attached.
2.  **Medium** – **Issue #957 (Config Reader Rate Limit)**: A specific blocker preventing JSON output in agent runtime mode. Unclear if this is a misconfiguration or a bug in how the rate-limit interacts with the memoryless runtime flag.

No new crashes, regressions, or security issues were reported in the last 24 hours.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today.
- **Roadmap Signal**: The prevalence of Issue #952 strongly signals that local model compatibility (specifically streaming/cutoff handling for Ollama models) is the community’s highest priority.
- **Configuration UX**: Issue #957 signals a need for better defaults or transparent documentation for internal rate limiters when running in specialized modes.
- **Prediction**: Given the severity of Issue #952, a hotfix or patch release addressing local model streaming truncation is likely in the near future.

### 7. User Feedback Summary
- **Pain Points**: Two distinct user pain points emerged:
    1. Reliability of local model inference (truncated output).
    2. Opaque rate-limiting behavior in the config reader under the “agent runtime without memory” mode.
- **Use Cases**: Users are actively testing NullClaw in production-adjacent scenarios: fully local privacy-oriented agents (Ollama) and lightweight stateless runtimes (JSON output).
- **Satisfaction**: Feedback is entirely problem-focused today. Users are hitting hard blockers, and the lack of public maintainer comments on either issue may lead to growing dissatisfaction if unaddressed.

### 8. Backlog Watch
- **Issue #952** (Created 2026-06-11): This bug report is now five days old without a public maintainer triage or status update. As local model support is a key differentiator for AI agent tools, this issue has high risk of becoming a community trust problem.
- **Issue #957** (Created 2026-06-15): Freshly filed, but requires prompt maintainer triage to clarify whether this is a documentation issue or a config software bug.

*Maintainer action recommended*: Acknowledging these two issues with a “looking into it” or “needs more info” label would significantly improve perceived project responsiveness.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest
**Date:** 2026-06-16
**Source Data:** GitHub activity for `github.com/nearai/ironclaw` (Issues updated: 46, PRs updated: 50, Releases: 0)

---

## 1. Today's Overview

Project activity is extremely high, with **46 issues** and **50 pull requests** updated in the last 24 hours, signaling a concentrated "stabilization sprint" on the **Reborn** architecture. Development is overwhelmingly focused on fixing authentication and OAuth flows for third-party extensions (Google, GitHub, Notion, Slack), improving the extension lifecycle UX, and closing out critical bugs in tool execution and the automations module. A high-severity Rust security advisory (`RUSTSEC-2026-0182`) prompted two urgent Wasmtime patch PRs. No new releases were cut today, but the volume of merged fixes and fresh feature work suggests a release may be imminent.

---

## 2. Releases

**No new releases were published today.** The latest release data shows no tagged versions. Given the number of closed bugs and merged feature PRs, a patch or minor release bundling these fixes is likely in the coming days.

---

## 3. Project Progress (Merged/Closed PRs & Resolved Issues)

Several high-priority features and fixes advanced today, primarily around the Reborn stack:

**Features Merged:**
- **Image Attachment Support for Vision Models** (`nearai/ironclaw PR #4871`) — Merged. Images attached by users are now sent as real multimodal content to vision-capable models, closing a major gap in the #4644 attachments epic.
- **Routine Delivery via Outbound Targets** (`nearai/ironclaw PR #4780`) — Merged. Adds model-visible guidance for choosing delivery targets before creating routines/triggers.
- **Trace Commons Merge Conflicts Resolved** (`nearai/ironclaw PR #4929`) — Merged. Makes the agent-invoked Trace Commons onboarding work mergeable again.

**Key Bug Fixes & Resolutions (Closed Issues):**
- **Automations Now Functional** (`nearai/ironclaw Issue #4917`) — Closed. Scheduled automations were completely non-functional ("stays at SCHEDULED forever"). Fix deployed.
- **Notion OAuth Redirect Fix** (`nearai/ironclaw Issue #4928`) — Closed. Production deployment (Railway) was using localhost callback URLs.
- **Persistent "Always Allow" Approvals** (`nearai/ironclaw Issue #4825`) — Closed. Users no longer re-prompted for approved capabilities across threads (`thread_id` removed from scope).
- **Excessive GitHub Approval Prompts** (`nearai/ironclaw Issue #4854`) — Closed. Simple read-only requests no longer trigger redundant approval gates.
- **Workspace Path Duplication** (`nearai/ironclaw Issue #4759`) — Closed. `workspace/demo/` paths no longer incorrectly duplicating the root.
- **Extension Setup Flow Guidance** (`nearai/ironclaw Issue #4890`, `#4886`) — Closed. Post-install steps are now clearer, reducing UX fragmentation.

---

## 4. Community Hot Topics

The most active discussions reflect deep engagement with the Reborn authentication and UX model:

| Issue/PR | Comments | Theme |
|---|---|---|
| `nearai/ironclaw Issue #4825` *Reborn: persist "always allow" approvals...* | 3 | **Approval UX Core Design:** Should durable approvals be tied to a thread or an agent/user? Transient vs. persistent scope. |
| `nearai/ironclaw Issue #4908` *Google Calendar shows "Activate" when active* | 3 | **Extension Lifecycle UX:** UI state inconsistency where a configured extension still prompts activation. |
| `nearai/ironclaw Issue #4764` / `nearai/ironclaw PR #4944` *Denying shell approval leaves tool pending* | 2 / - | **Critical UX Loop:** Denying a gate silently breaks the run. The fix (`PR #4944`) is a hot topic as it addresses an immediate user blocker. |
| `nearai/ironclaw Issue #4880` *Automate Code Review...* | 2 | **Development Workflow:** Community discussion on dogfooding IronClaw for AI-driven code review and PR resolution. |
| `nearai/ironclaw Issue #4907` *Run fails after successful Google OAuth* | 2 | **OAuth Reliability:** Successful authorization fails to resume the original run—a critical usability gap. |

**Underlying Need:** The community is demanding a **seamless, persistent, and stateful** authentication model. The biggest friction points are:
1. Auth gates leaving the agent in a broken/looping state.
2. OAuth flows succeeding technically but failing to deliver the promised result.
3. UI not reflecting the true state of integrations (Active vs. Needs Setup).

---

## 5. Bugs & Stability

Stability issues dominated the project today, ranked by severity:

### Critical / Immediate Attention
| Bug | Severity | Status |
|---|---|---|
| **Wasmtime RUSTSEC-2026-0182** (*fd_renumber leak*) | **Security / Repo-wide CI Block** | Fixes in `nearai/ironclaw PR #4949` & `#4950` |
| **Auth Denial Infinite Loop** (`nearai/ironclaw Issue #4764`, `#4800`) | **Run-Borking** | Fix in `nearai/ironclaw PR #4944` |
| **Agent Tool Failure Recovery** (`nearai/ironclaw Issue #4761`) | **Resilience** | No fix PR yet; agent stops dead after repeated tool failures |

### Major
| Bug | Severity | Status |
|---|---|---|
| **OAuth Flows Not Resuming Execution** (`nearai/ironclaw Issue #4907`, `#4887`, `#4921`) | **Functional Breakage** | Multiple reports for Google/Gmail/MCP. Open. |
| **Ollama "Test Connection" False Positive** (`nearai/ironclaw Issue #4696`) | **Misleading UI** | Closed (Fix deployed). |
| **Provider Status Inconsistency** (`nearai/ironclaw Issue #4857`, `#4697`) | **User Trust** | Open. NEAR AI provider shown as Active when not configured. |
| **Calendar Auth Not Reused Across Conversations** (`nearai/ironclaw Issues #4841` `#4913`) | **UX Regression** | Open. Users must re-approve every conversation. |

### Minor / Polish
- Tool call failures require manual re-fetch to appear (`nearai/ironclaw Issue #4942`).
- Google Calendar prompts for access token instead of guiding OAuth flow (`nearai/ironclaw Issue #4884`).
- NEAR AI MCP shows "SETUP NEEDED" when fully ready (`nearai/ironclaw Issue #4925`).

---

## 6. Feature Requests & Roadmap Signals

### Likely in Next Release
- **Vision & Attachments**: Image support for vision models (`PR #4871`) is merged. Universal attachment pipeline (#4644) is progressing with the OpenAI-compat `/v1/chat/completions` inline images step (`PR #4902`).
- **Downloadable Project Files**: `PR #4933` lets agents produce downloadable files (CSV, exports) in WebChat v2.
- **Slack Personal Token Tool**: `PR #4941` proposes a `slack_user_tool` (user-token) for capabilities bot tokens cannot provide (e.g., `search_messages` across all channels).
- **Operator Diagnostics**: `PR #4801` wires a diagnostics endpoint for checking operator readiness.

### Strategic Signals
- **Coding Agent Dogfooding**: Issues `#4880` and `#4882` outline plans for an automated AI code review and cloud coding agent workflow. IronClaw appears to be advancing towards running its own development lifecycle.
- **Credentials Scoping Reform**: `nearai/ironclaw PR #4939` (owner-scoped, not thread-scoped) represents a fundamental architectural correction to the credential model. This will unblock many OAuth persistence issues.
- **Trace Commons / Telemetry**: `nearai/ironclaw Issue #4940` calls for test coverage of agent-invoked host-egress path for telemetry (Trace Commons), indicating growing investment in observability.

---

## 7. User Feedback Summary

### Expressed Pain Points
1.  **"Setup feels fragmented"** (Issues #4890, #4886, #4908): Users struggle to navigate the Registry -> Install -> Configure -> Authorize pipeline. The UI inconsistently shows "ACTIVE" but still presents an "Activate" button.
2.  **"OAuth doesn't work reliably"** (Issues #4907, #4921, #4928, #4887): Multiple users report that going through the full OAuth flow leaves them empty-handed—authorization succeeds, but the run fails, the tool doesn't fire, or the authorization is lost in the next conversation.
3.  **"The app lies to me"** (Issues #4696, #4857, #4697): The UI reports "Connection OK" when Ollama is down, shows providers as "ACTIVE" when unconfigured, and suggests setup is needed when it isn't. Core trust issue with the platform.
4.  **"Automations were totally broken"** (Issue #4917): A fundamental feature of the platform shipped with no apparent functionality. Closed, but represents a significant quality gap.

### Expressed Satisfaction
- **High Release Cadence**: Users are filing issues and seeing them closed within hours or days (e.g., #4917, #4825). This validates the project's responsiveness.
- **Active Community Contribution**: Regular and new contributors (thisisjoshford, serrrfirat, sergeiest) are submitting real features and fixes, signaling a healthy OSS community outside the core team.

---

## 8. Backlog Watch

Several important items risk falling through the cracks amidst the high daily churn:

| Item | Age | Risk / Note |
|---|---|---|
| `nearai/ironclaw PR #3705` *bump rand in WeChat channel* | **1 Month** (since May 16) | Oldest open dependabot PR. Neglect of the WeChat channel may indicate deprecation or low priority. Needs maintainer decision. |
| `nearai/ironclaw Issue #4761` *Agent stops after repeated tool failures* | **5 Days** (since Jun 11) | Core resilience bug. Agent has no recovery mechanism from tool failures. No active fix PR. |
| `nearai/ironclaw PR #4876` *Massive 43-package dep bump* | **2 Days** (since Jun 14) | High risk of regressions. Requires careful human review. Stalls updates for the entire dependency group. |
| `nearai/ironclaw Issue #4644` *Universal Attachments* | **7 Days** (since Jun 9) | Large multi-step epic. While vision is done (`#4871`), the core pipeline for all channels (Reborn, v1, Web) is still unresolved. |
| `nearai/ironclaw Issue #4882` *Build Coding Agent Cloud Workflow* | **1 Day** | Ambitious scope (issue assignment -> complete PR). Requires significant architectural investment. Needs maintainer roadmap sign-off. |

**Maintainer Attention Needed:** The `#4761` resilience bug and the `#4644` attachments core pipeline are the most impactful items needing prioritization to prevent user frustration from compounding.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**Project Digest: LobsterAI (github.com/netease-youdao/LobsterAI)**
**Date:** 2026-06-16

---

### 1. Today’s Overview
The LobsterAI project demonstrated strong development velocity over the past 24 hours, driven by a focused sprint toward the v2026.6.11 release branch. Activity was high, with 11 pull requests updated and 5 merges completed, primarily targeting voice input simplification, artifacts feature finalization, and CI dependency hygiene. No new releases were cut, and no new issues were filed, suggesting the team is in a stabilization and integration phase. Overall project health is robust, with core features maturing alongside a growing dependency maintenance burden.

---

### 2. Releases
No new versions were published in the last 24 hours.

---

### 3. Project Progress
Five pull requests were merged today, all of which feed directly into the upcoming release branch:

- **Voice Input Architecture Refactor:**
  - **[#2160](https://github.com/netease-youdao/LobsterAI/pull/2160)**: Removed the legacy short ASR upload flow and the associated `asr:recognize` IPC surface. Cowork voice input now always uses realtime ASR, stripping the Settings mode switch and the `voiceInput.recognitionMode` config.
  - **[#2162](https://github.com/netease-youdao/LobsterAI/pull/2162)**: Resolved merge conflicts to preserve realtime-only ASR while retaining draft ownership, stale callback guards, session-switch cancellation logic, and diagnostic logging.
  - **[#2163](https://github.com/netease-youdao/LobsterAI/pull/2163)**: Added an in-memory ASR quota slice and shared constants, coupled with UI refinements for the dictation recording experience.

- **Artifacts Document Sharing (Major Feature):**
  - **[#2159](https://github.com/netease-youdao/LobsterAI/pull/2159)**: Introduced comprehensive document artifact sharing. Includes support for DOCX, PPTX, XLSX, PDF, CSV, and TSV files with type validation, size limits, pagination (DOCX), native PDF fallback, and automatic table column width rendering. Also updated CSP policies and included pdfjs font/cMap static assets.

- **Chores & Polish:**
  - **[#2161](https://github.com/netease-youdao/LobsterAI/pull/2161)**: Updated the application “About” page.

---

### 4. Community Hot Topics
The most active backend discussions remain concentrated on issues related to the local skill upload workflow:

- **[#1426](https://github.com/netease-youdao/LobsterAI/issues/1426)**: Users report no success prompt after uploading a skill locally, and the skill list fails to refresh.
- **[#1427](https://github.com/netease-youdao/LobsterAI/issues/1427)**: Users can repeatedly upload the same skill, resulting in multiple duplicate entries with identical names.

**Analysis:** Both issues, filed by the same user and flagged as stale, point to a gap in user experience feedback loops and data integrity constraints in the plugin management system. The community is actively trying to extend the platform via local skills but is encountering friction due to missing UI confirmations and deduplication logic. The lack of comments on other PRs/Issues suggests that the user base is either primarily interacting with the product via direct usage rather than GitHub discourse, or that developer attention is heavily concentrated on the current sprint’s scope.

---

### 5. Bugs & Stability
No new bugs were filed today. The two existing bugs under the **Backlog Watch** section remain the most pressing stability issues reported by the community.

**Severity Ranking (Open Bugs):**
1. **High – [#1427](https://github.com/netease-youdao/LobsterAI/issues/1427)**: Duplicate skill uploads allowed. This affects data integrity and user sanity by polluting the skill list.
2. **Medium – [#1426](https://github.com/netease-youdao/LobsterAI/issues/1426)**: Missing success feedback and list refresh after upload. Frustrating UX but does not corrupt data.

**Note:** None of the five PRs merged today addressed these bugs. The team’s focus remains on voice and artifacts, leaving these skill management issues untriaged in the current delivery cycle.

---

### 6. Feature Requests & Roadmap Signals
- **Document Artifact Sharing ([#2159](https://github.com/netease-youdao/LobsterAI/pull/2159))**: **Merged**. This is a major milestone, lowering the barrier for sharing structured outputs (Office docs, PDFs) directly within the cowork interface. Very strong signal that collaborative document workflows are a high priority.
- **Realtime-Only Voice Input ([#2160](https://github.com/netease-youdao/LobsterAI/pull/2160))**: **Merged**. The architectural simplification to remove short ASR suggests the team has committed to a streaming-first dictation model, prioritizing low latency over alternative recording modes.
- **Background System Notifications for Cowork Sessions ([#1428](https://github.com/netease-youdao/LobsterAI/pull/1428))**: **Open/Stale**. This feature requests Electron `Notification` API integration to alert users when a session completes or errors while the window is unfocused.

**Prediction:** The next release will heavily emphasize *Artifacts as a sharing medium* and a *robust, realtime-only voice dictator*. The open system notification PR (#1428) is the most likely candidate for the next sprint given its direct relation to the “cowork” user experience and parity with tools like Claude Code.

---

### 7. User Feedback Summary
- **Pain Points:**
  - The skill management system lacks basic UX feedback (no upload confirmation, no duplicate prevention). Users feel they are operating blindly when extending the platform.
  - Users working with background sessions (e.g., long-running LLM tasks) find the lack of system-level notifications disruptive.
- **Use Cases & Satisfaction:**
  - High engagement with the **cowork** and **voice input** features is implied by the volume of voice-related PRs and the community request for background notifications.
  - The completion of document artifact sharing signals that users are using LobsterAI for complex, document-centric tasks and want seamless export/share capabilities.

---

### 8. Backlog Watch
The following items are flagged as stale or long-unanswered and require maintainer triage:

- **Issues:**
  - **[#1426](https://github.com/netease-youdao/LobsterAI/issues/1426)**: Skill upload feedback (Opened 2026-04-03, Updated 2026-06-15).
  - **[#1427](https://github.com/netease-youdao/LobsterAI/issues/1427)**: Duplicate skill uploads (Opened 2026-04-03, Updated 2026-06-15).

- **Pull Requests:**
  - **[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277)**: Dependency bump for the Electron group (Electron 40.2.1 → 42.4.0). Open since 2026-04-02.
  - **[#1428](https://github.com/netease-youdao/LobsterAI/pull/1428)**: Feature request for system notifications during cowork sessions. Open since 2026-04-03.

**Assessment:** These items represent the oldest actionable community input in the repository. Addressing them in a dedicated maintenance sprint would significantly improve user trust and clear technical debt that has accumulated over the past 2.5 months.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for June 16, 2026, based on the provided GitHub data.

---

## Moltis Project Digest — 2026-06-16

### 1. Today’s Overview
Moltis experienced a quiet day on June 16, with no new issues filed and no releases published. Development focus remained entirely centered on two feature pull requests opened the previous day by author `gptme-thomas`. These PRs—addressing external agent model configuration and automated context injection—represent the totality of the project’s forward momentum. Neither PR has received comments or reactions yet, and no code was merged to the main branch. Overall, project health appears stable, with activity currently concentrated in a narrow feature-development phase.

### 2. Releases
No new releases were published in the last 24 hours. This section is omitted.

### 3. Project Progress
No pull requests were merged or closed today. The two open PRs from June 15 remain in an unmerged state:
- **None merged/closed today.** Development is currently stalled at the review stage, or work is ongoing on these branches without having been submitted for integration yet. The project's main branch saw no new commits from merged PRs over the period.

### 4. Community Hot Topics
The only active items are the two open PRs, which are nascent with **zero comments and zero reactions** so far. While not yet "hot" in terms of engagement, they constitute the entire current conversation in the repository.

- **[PR #1125: Support model and effort selection for external agents](moltis-org/moltis PR #1125)**
- **[PR #1124: Add context command support for chat turns](moltis-org/moltis PR #1124)**

**Underlying Needs:** These PRs signal a push toward deeper configuration flexibility and operational maturity.
- **#1125** addresses the need to granularly control which models and reasoning efforts are used by third-party external-agent providers, moving beyond simple API passthrough.
- **#1124** addresses production deployment requirements by allowing automated injection of runtime context (e.g., system stats, timestamps) into every chat turn without manual input.

The absence of community feedback suggests these are maintainer-led features currently being developed or tested internally.

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The issues tracker recorded zero new items (open, active, or closed). This absence of stability tickets indicates a period of high surface stability or that the project is currently operating in a feature-development cycle without addressing open bug reports.

### 6. Feature Requests & Roadmap Signals
Although no explicit feature requests were filed as issues today, the open PRs serve as the strongest signals for the immediate roadmap:

- **Automated Context Injection (`chat.context_command`, PR #1124):** This strongly suggests Moltis is preparing for broader or more automated deployment use. Users deploying Moltis as a service need dynamic context injected natively without manual editing of session prompts.
- **Model & Effort Metadata for External Agents (PR #1125):** This indicates the `/model` command is being evolved into a rich abstraction layer for provider management. This is a strategic move to position Moltis as a flexible agent gateway rather than a single-model tool.

**Prediction:** These two features are highly likely to be bundled into the next minor release. They address core config (models/efforts) and deployment ergonomics (context commands), which are logical blockers for a stable release candidate.

### 7. User Feedback Summary
No direct user feedback in the form of bug reports or feature requests was recorded today. However, the PRs authored by `gptme-thomas` implicitly reflect developer pain points with the current tooling:

- **Pain Point:** Inability to customize model selection and effort levels for non-native external agents (addressed by #1125).
- **Pain Point:** Lack of native support for automatically injecting run-specific environment context into repetitive chat interactions (addressed by #1124).
- **Satisfaction Signal:** The absence of new issues or regressions suggests that existing users are either satisfied with the current stable behavior or are themselves the engineers contributing code to close their own feature gaps.

### 8. Backlog Watch
No existing issues or PRs were updated in the last 24 hours. The active view of the issue tracker shows zero items, indicating either a completely clean backlog or that no long-standing threads received maintainer attention today.

**Item to Watch:** While not old, the two open PRs (**#1124** and **#1125**) are the most critical items requiring attention or review. If these remain unmerged and uncommented upon for an extended period, they could become the next backlog candidates.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest (2026-06-16)

*Generated using GitHub data for the QwenPaw project (the continuation of CoPaw).*

---

## 1. Today’s Overview
Today marks an exceptionally high-velocity development day. **50 issues** and **50 pull requests** were updated, with **32 PRs merged or closed** — a strong signal that the team is pressing hard on stability and UX. No new releases were cut, meaning the high closure rate is likely consolidating improvements for a future version. Community engagement is intense: channel integration friction (Huawei XiaoYi), regression churn around the `post2` patch, and fresh feature demands (queuing, compression) dominate the discussion.

---

## 2. Releases
**No new releases** today. The latest tagged version remains **v1.1.11.post2**, against which most fresh bug reports are filed. A significant volume of regressions and crash reports suggests a hotfix (or v1.2.0) is being actively assembled by the team.

---

## 3. Project Progress
The following high-impact PRs were merged or closed today:

- **Agent OS Driver** ([#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067)) — Merged. A unified abstraction layer for external capabilities (MCP, A2A, ACP), standardizing how agents interact with tools and remote agents.
- **Skill Market & UI** ([#5123](https://github.com/agentscope-ai/QwenPaw/pull/5123), [#5146](https://github.com/agentscope-ai/QwenPaw/pull/5146)) — Merged. Added the official QwenPaw skill market with categories/previews. Also fixed the `/skill` injection issue where raw SKILL.md was displayed instead of a clean execution block.
- **Context & Token Usage UI** ([#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310), [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130)) — Merged. Chat header now shows a context usage indicator, and response cards include a per-turn token usage popover. Directly fulfills four long-standing feature requests.
- **Enhanced Resilience** ([#5040](https://github.com/agentscope-ai/QwenPaw/pull/5040), [#5041](https://github.com/agentscope-ai/QwenPaw/pull/5041)) — Merged. Cron jobs now tolerate individual malformed entries; backups skip unreadable files instead of failing entirely.
- **Windows Client Memory Fix** ([#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138)) — Closed. The memory leak that caused process count and RAM to balloon to 90% has been resolved.
- **Plugin Rename Migration** ([#5104](https://github.com/agentscope-ai/QwenPaw/issues/5104)) — Closed. Critical support for the `copaw` → `qwenpaw` path migration landed, fixing plugin install failures and directory confusion.
- **Enterprise WeChat Approval** ([#5190](https://github.com/agentscope-ai/QwenPaw/issues/5190)) — Closed. The approval interface for private chat access control is now visible.
- **Input Queue Feature** ([#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158)) — Active. Implements the requested conversational queue, allowing users to type their next input while the agent is still processing.
- **Models Page Overhaul** ([#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203)) — Active. Major redesign with provider aggregation and updated card UI.
- **Desktop Startup Optimization** ([#5153](https://github.com/agentscope-ai/QwenPaw/pull/5153)) — Active. Ports the Tauri instant-window trick to the pywebview client.

---

## 4. Community Hot Topics

| Issue / PR | Comments | Context |
|---|---|---|
| [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) — XiaoYi Channel | **22** | Heaviest engagement overall. Users can register the channel successfully, but Huawei XiaoYi mobile returns "network congestion" errors and chat logs never sync to CoPaw. |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) — Attachment Download 404 | **6** | High frustration. v1.1.11.post2 fixed plain text downloads, but `.docx` / `.pdf` downloads still fail with 404 errors. |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) — MiniMax XML Incompatibility | **5** | MiniMax-M2.5 returns `thinking` in XML, breaking agent tool execution and skill flows. Community tagging this as a severe model parsing gap. |
| [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) — Plugin CMD Popups | **5** | `pip install` errors for plugin dependencies cause visible CMD windows to flash repeatedly, a significant Windows UX degradation. |
| [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) — Context Compression Data Loss | **4** | When an agent's persona file (AGENTS.md, SOUL.md) is too large, compression drops *all* context, completely terminating the session. |
| [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) — Long Conversation Timeout | **4** | Agents stall and stop responding entirely after many turns, suggesting a context management or token limit bug beyond normal compression. |

---

## 5. Bugs & Stability

### 🔴 Critical
- **macOS Tauri Crash Loop** ([#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209)) — `qwenpaw-backend` crashes every ~60 seconds (SIGSEGV, EXC_BAD_ACCESS) on Apple Silicon, making the desktop client unusable. **No fix PR open yet.**
- **Context Compression Total Data Loss** ([#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)) — Agent tasks are completely destroyed when persona files exceed token thresholds during compression. High impact for long-running agents.

### 🟠 High
- **File Attachment Download 404** ([#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140), [#5199](https://github.com/agentscope-ai/QwenPaw/issues/5199)) — Binary files fail to download across multiple patch versions; regression not fully resolved.
- **Long Conversation Stall** ([#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161)) — Agent stops responding entirely after extended context, mirroring user anxiety around cost and session viability.

### 🟡 Medium
- **MiniMax XML Breakage** ([#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)) — XML reasoning output from MiniMax blocks agent execution flow. Reopened.
- **Plugin Install CMD Popups** ([#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)) — pip retries cause desktop clutter on Windows with poor PyPI access.
- **Local Provider Display Bug** ([#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184)) — Locally created model providers vanish from the UI after upgrading to `post2`.
- **Wayland Desktop Pet Incompatibility** ([#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183)) — Pet widget fails on Niri and other non-X11 compositors.
- **Submit-to-Agent Path Bug** ([#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025)) — Inter-agent task submission fails due to incorrect session file path generation.
- **Context Compression Stats Discrepancy** ([#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122)) — Reported 0.9% compression, but actual API input is dozens of KB. MCP/Skill metadata inflation suspected.

### ✅ Fixed Today
- **Windows Client Process Leak** ([#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138)) — Patched.
- **Skill Display Bug** ([#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) → [#5146](https://github.com/agentscope-ai/QwenPaw/pull/5146)) — Patched.
- **Renamed Plugin Path Chaos** ([#5104](https://github.com/agentscope-ai/QwenPaw/issues/5104)) — Patched.

---

## 6. Feature Requests & Roadmap Signals

| Request | Signal Strength | Notes |
|---|---|---|
| **User Input Queue** ([#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103)) | Very High | Directly inspired by OpenClaw. **Active PR exists** ([#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158)), strong candidate for next minor release. |
| **Context Compression Optimization** ([#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063), [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122)) | High | Headroom integration requested to reduce token usage 60–95%. Backed by evidence of compression stat inaccuracy. |
| **Desktop UI Overhaul** ([#5211](https://github.com/agentscope-ai/QwenPaw/issues/5211)) | Medium | User detailed excessive top-nav height and low space utilization. New PR for **Wide Mode toggle** ([#5212](https://github.com/agentscope-ai/QwenPaw/pull/5212)) already landed. |
| **Models Page Redesign** ([#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203)) | Active PR | Provider aggregation, unified cards, Aliyun Token Plan support. Likely to ship in next UI update. |
| **Agent Self-Evolution** ([#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)) | Emerging | Novel request: agents automatically update behavior rules from runtime mistakes. |
| **Feishu Streaming Card Optimization** ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)) | Medium | Long replies in Feishu CardKit are noticeably slow; user requests chunking or byte-level streaming. |
| **Cron Update CLI** ([#4939](https://github.com/agentscope-ai/QwenPaw/issues/4939) → [#5210](https://github.com/agentscope-ai/QwenPaw/pull/5210)) | Active PR | Adds `qwenpaw cron update` to replace delete-and-recreate workflow. |

---

## 7. User Feedback Summary

**Satisfaction Drivers:**
- The merge of Context & Token Usage UI ([#4310](https://github.com/agentscope-ai/QwenPaw/pull/4310), [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130)) was extremely well-received, satisfying a top community pain point.
- Users praise the rapid pace of feature delivery (Skill Market, Agent OS Driver).

**Dissatisfaction Drivers:**
- **Regression fatigue:** v1.1.11.post2 is perceived as unstable. The macOS crash loop ([#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209)) and persistent download bugs ([#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140)) are causing users to avoid upgrading or roll back.
- **Plugin ecosystem friction:** The rename from `copaw` → `qwenpaw` broke paths ([#5104](https://github.com/agentscope-ai/QwenPaw/issues/5104)), and pip dependency installs are intrusive ([#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)). Users want a polished plugin experience.
- **Channel reliability:** XiaoYi and Enterprise WeChat channels show functional gaps (network errors, missing approval UI). Channel developers are hitting hard early-adopter walls.

---

## 8. Backlog Watch
Items requiring maintainer attention due to age, severity, or lack of progress:

- **[#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) — XiaoYi Channel Stability** | Open since **March 2026** | 22 comments, no assigned PR. The most commented issue in the dataset remains unresolved.
- **[#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) — MiniMax XML Model Bug** | Open since May 22 | Reopened after being briefly closed. Affects a growing subset of users trying non-OpenAI providers.
- **[#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025) — Submit-to-Agent Path Bug** | Root cause clearly identified but still open. A systematic blocker for multi-agent workflows.
- **[#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) — Plugin Loader Decoupling** | Critical for PyInstaller/Tauri desktop builds. Plugin system silently fails to initialize in frozen environments. Needs review and merge.
- **[#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) — DataPaw Plugin** | First-time contributor PR from May 22. A significant community plugin (12 BI skills) tagged "Under Review" but still pending final approval.
- **[#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) — Governance & Sandbox Interface** | Open since June 10 with no clear merge signal. Given the security implications of MCP/A2A, this deserves prioritization.
- **[#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) — Context Compression Stats Discrepancy** | Multiple users confirming that compression UI does not match API payload. Undermines trust in the new context display feature.
- **[#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209) — macOS Crash Loop** | Brand new but critical. No fix PR open yet; this will block all macOS ARM64 users from the latest builds.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the structured ZeroClaw project digest for 2026-06-16.

---

## 1. Today's Overview

The ZeroClaw project remains in a high-velocity development cycle, with **50 issues and 50 pull requests updated in the last 24 hours**. Activity spans security hardening, multi-agent architecture, channel integrations, and significant bug triage. Community engagement is exceptionally strong, evidenced by a surge in detailed RFCs from contributors. While no formal release was published today, the project appears to be consolidating work toward the **v0.8.1 integration milestone** (`zeroclaw-labs/zeroclaw#6970`) and the more ambitious **v0.9.0 security and multi-tenancy release** (`zeroclaw-labs/zeroclaw#7432`).

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

One PR was merged and **four issues were closed** over the past day, signaling forward momentum on key pain points:

- **Feature Completion – Local CA Certificates (`zeroclaw-labs/zeroclaw #1458`):** A long-standing enterprise blocker was resolved. Users can now specify a trusted root CA for custom inference endpoints, enabling connectivity with private PKI. This closes a gap that was previously tracked alongside a related request for self-signed certs (`zeroclaw-labs/zeroclaw #551`).
- **API Fix – `ask_user` Tool & Gateway Web Dashboard (`zeroclaw-labs/zeroclaw #7542`):** A critical bug where the `ask_user` tool failed instantly with "Channel closed before receiving a response" in WebSocket sessions was resolved. This unblocks a core human-in-the-loop workflow.
- **Rate Limit Enforcement – Skill Patching (`zeroclaw-labs/zeroclaw #6683`):** The `SkillImprover::should_improve_skill` predicate was functionally dead code; `skill_manage action=patch` now correctly enforces disk cooldowns, preventing unbounded patch operations.
- **Localization Polish – Quickstart Strings (`zeroclaw-labs/zeroclaw #7005`):** Remaining bare user-facing strings in the onboarding flow were cleaned up.

## 4. Community Hot Topics

The majority of high-engagement discussions center on scaling ZeroClaw from a single-agent tool to a secure, multi-agent platform.

- **Multi-Agent Routing (`zeroclaw-labs/zeroclaw #2767`):** The top-voted open feature request (9 👍, 6 comments). Users want isolated agent workspaces, multiple channel accounts, and binding-based inbound routing in a single gateway instance. This is the core tentpole feature for the v0.9.0 milestone.
- **Performance Optimization (Light Models for Pre-check):** `zeroclaw-labs/zeroclaw #6067` (5 comments) requests a configurable reply-intent precheck that uses a smaller/faster model with a hard timeout. This reflects a strong user demand for reducing latency and cost in non-critical path classifications.
- **RFC Discussions:**
    - **Context Compression (`zeroclaw-labs/zeroclaw #7673`):** A proposal for a `CompressionDecorator` to compress `ChatRequest` payloads before forwarding to the provider. Addresses the cost of long-context LLM requests.
    - **A2A Agent Discovery (`zeroclaw-labs/zeroclaw #7218`):** Defines `/.well-known/agent-card.json` for multi-agent installs, laying groundwork for external interoperability.
    - **Hardened CI (`zeroclaw-labs/zeroclaw #7675`):** Proposes supply-chain scanning, provenance, and SBOM generation.
    - **WebAssembly-First Build (`zeroclaw-labs/zeroclaw #7674`):** A proposal to eliminate Node.js from ZeroClaw's build and runtime entirely.

## 5. Bugs & Stability

Stability remains an active concern. While critical bugs were closed, several high-impact issues surfaced today.

| Severity | Issue | Component | Summary |
|---|---|---|---|
| **S1 – Blocked** | `zeroclaw-labs/zeroclaw #7756` | Tools/Runtime | Native MCP tools are **not sent to the model** on `wire_api=responses` and for Anthropic models. The model receives an empty tool list. |
| **S2 – Degraded** | `zeroclaw-labs/zeroclaw #7753` | Channels | Pre-existing per-session ordering race: concurrent processing of messages for the same sender causes session-store mutation ordering issues. |
| **S2 – Security** | `zeroclaw-labs/zeroclaw #7733` | Config/Security | `mcp_bundles` is parsed and displayed in the config but **never enforced at runtime**. Per-agent MCP scoping is a silent no-op. |
| **S2 – Degraded** | `zeroclaw-labs/zeroclaw #7741` | Runtime/Multimodal | Response cache does not skip cache operations when messages contain `[IMAGE:...]` markers, causing degraded behavior. |
| **S2 – Degraded** | `zeroclaw-labs/zeroclaw #7739` | Channel (Email) | Email OAuth refresh path lacks retry/backoff wrappers for transient failures, unlike OpenAI/Gemini providers. |
| **S2 – Degraded** | `zeroclaw-labs/zeroclaw #7757` | Gateway (API) | Gateway web dashboard Skills page only reflects `skill_bundles`, missing workspace/open-skills/plugin skills. |
| **S2 – Blocked** | `zeroclaw-labs/zeroclaw #7038` | Gateway/Auth | `zeroclaw check` fails 11/11 with 401 despite valid auth configuration. Status: blocked, needs reproduction. |

**Incoming Fixes:** PRs are actively addressing related stability issues, including WebSocket authentication in self-test (`zeroclaw-labs/zeroclaw #7732`), poisoned lock recovery in tool-spec assembly (`zeroclaw-labs/zeroclaw #7755`), and OAuth credential delegation for sub-agents (`zeroclaw-labs/zeroclaw #7640`).

## 6. Feature Requests & Roadmap Signals

The roadmap bifurcates clearly into two tracks:

- **v0.8.1 (Integration Track – `zeroclaw-labs/zeroclaw #6970`):**
    - **Slack:** Hydrate thread context from `conversations.replies` on first mention (`zeroclaw-labs/zeroclaw #6055`).
    - **Mattermost:** Optional WebSocket listener mode for real-time events (`zeroclaw-labs/zeroclaw #7098`).
    - **WhatsApp:** `add_reaction` / `remove_reaction` parity (`zeroclaw-labs/zeroclaw #7535`).
    - **TUI:** Ability to rename aliases (`zeroclaw-labs/zeroclaw #7468`) and more flexible string editing (`zeroclaw-labs/zeroclaw #7467`).

- **v0.9.0 (Security & Multi-Tenancy – `zeroclaw-labs/zeroclaw #7432`):**
    - **Core Feature:** Multi-Agent Routing (`zeroclaw-labs/zeroclaw #2767`).
    - **RFCs:** Native context compression (`zeroclaw-labs/zeroclaw #7673`), A2A discovery (`zeroclaw-labs/zeroclaw #7218`), WebAssembly-first build (`zeroclaw-labs/zeroclaw #7674`), and Hardened CI pipeline (`zeroclaw-labs/zeroclaw #7675`).
    - **Security:** Per-agent `prompt_injection_mode` override (`zeroclaw-labs/zeroclaw #7749`), explicit target-profile authority for delegate handoffs (`zeroclaw-labs/zeroclaw #7743`).

## 7. User Feedback Summary

- **Pain Points:**
    - **Configuration Friction:** Users report frustration with config validation. The discovery that `mcp_bundles` scoping is silently ignored (`zeroclaw-labs/zeroclaw #7733`) and that auth checks fail against seemingly valid configs (`zeroclaw-labs/zeroclaw #7038`) undermines developer trust in the dashboard.
    - **Tooling Reliability:** The report that registered MCP tools are silently dropped from requests (`zeroclaw-labs/zeroclaw #7756`) and the uncanny behavior of the skills dashboard (`zeroclaw-labs/zeroclaw #7757`) heightens concern about core reliability.
    - **Windows Support:** Ongoing encoding issues (`zeroclaw-labs/zeroclaw #7670`) and `.zip` release asset handling (`zeroclaw-labs/zeroclaw #7530`) highlight Windows as a secondary but actively maturing platform.

- **Satisfaction & Engagement:**
    - The closure of **#1458** (Local CA Certs) addresses a vocal demand from the self-hosted enterprise segment.
    - The community is demonstrating a high degree of technical investment. The RFCs on context compression, Wasm-first architecture, and CI hardening are sophisticated contributions from users who are deeply invested in ZeroClaw's long-term future.

## 8. Backlog Watch

Several items risk stalling and require maintainer prioritization attention:

- **Lost Commit Audit (`zeroclaw-labs/zeroclaw #6074`):** An open audit tracking the recovery of **153 commits** lost in a bulk revert. This has been open since April and no restoration PR is linked, creating a significant gap between master and previously merged features.
- **Self-Signed Certs Stalemate (`zeroclaw-labs/zeroclaw #551`):** The request to allow insecure HTTPS to OpenAI-compatible endpoints remains **blocked since February**. While #1458 addressed local CAs, users with self-signed certs are still unsupported.
- **PRs Near Stale:**
    - **Mattermost WebSocket Mode (`zeroclaw-labs/zeroclaw #7098`):** A highly requested enhancement tagged `needs-author-action` and `stale-candidate`.
    - **CLI Model Persistence (`zeroclaw-labs/zeroclaw #7094`):** Fixes a documented command that routes to a read-only diagnostic instead of persisting config. Also tagged `stale-candidate`.
    - **Domain Validation Refactor (`zeroclaw-labs/zeroclaw #7340`):** Extracts duplicate URL/domain validation but is awaiting author updates.
- **Internationalization Debt:** The gap between English source strings and Fluent locale files (`zeroclaw-labs/zeroclaw #6698`) is a growing technical debt item that quietly limits the project's global accessibility.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*