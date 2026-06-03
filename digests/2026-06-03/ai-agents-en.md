# OpenClaw Ecosystem Digest 2026-06-03

> Issues: 425 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-03 03:46 UTC

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

# OpenClaw Project Digest — 2026-06-03

## 1. Today's Overview
The OpenClaw project is experiencing a surge in activity, with **425 issues updated** (272 active, 153 closed) and **500 pull requests** (391 open, 109 merged/closed) in the last 24 hours. This high throughput underscores a deeply engaged community, but the volume of open items—coupled with recurring P1 regressions in core session, channel, and Codex runtime logic—indicates the project is in a critical stabilization phase. No new releases were published today, but the rate of PR merging signals rapid iteration on `main`. Project health is mixed: contributions are robust, but regression fatigue is the dominant user sentiment.

## 2. Releases
**No new releases** were published as of 2026-06-03.

## 3. Project Progress
Several impactful fixes landed today, reflecting focused effort on session resilience, channel reliability, and agent infrastructure.

### Session & Data Integrity
- **[PR #89065](openclaw/openclaw PR #89065)** (fix(sessions): prevent silent data loss when resuming corrupted header) — A P0 fix merged, closing Issue #89037. This addresses a severe bug where a single corrupted transcript line could silently wipe the entire session history.
- **[PR #84009](openclaw/openclaw PR #84009)** (fix(gateway): run daily session resets on schedule) — Advanced through review, moving session reset maintenance to a scheduled gateway task.

### Channel Reliability
- **[PR #87626](openclaw/openclaw PR #87626)** (fix(telegram): skip chat_window context for persistent DMs) — Merged, eliminating duplicated conversation context blocks on every inbound Telegram DM turn.
- **[PR #79176](openclaw/openclaw PR #79176)** (fix(github-copilot): drop encrypted reasoning on replay) — Merged, fixing a cross-turn crash where encrypted reasoning content from a prior turn was replayed upstream and rejected.
- Multiple Feishu fixes were opened and progressed: **PR #89659** (rate-limit retry logic), **PR #89680** (audited content redaction), and **PR #89687** (topic-scoped queues).

### Agent & Infrastructure
- **[PR #86883](openclaw/openclaw PR #86883)** (fix(subagents): expose announce retry config) — Merged, giving operators control over sub-agent announcement retries on flaky channels.
- **[PR #67202](openclaw/openclaw PR #67202)** (fix: add post-write verification) — Merged to prevent false "Successfully wrote X bytes" reports when the file was never actually created on disk.

## 4. Community Hot Topics
The community is most vocal around core architecture evolution and high-priority production blockers.

### Most Active Discussions
- **[Issue #52875](openclaw/openclaw Issue #52875)** (*Session_send gives no session found*, 21 comments): A long-running thread from March detailing failures in multi-agent coordination. Users report agents cannot reliably discover or contact one another after upgrades. The underlying need is for robust cross-agent session discovery and basic interoperability guarantees.
- **[Issue #88838](openclaw/openclaw Issue #88838)** (*SQLite session/transcript migration tracking*, 17 comments): High engagement on the architectural plan to migrate core session state to SQLite. The community is deeply reviewing the "branch-by-abstraction" strategy, signaling buy-in for this major infrastructure overhaul.
- **[Issue #63918](openclaw/openclaw Issue #63918)** (*Cron agentTurn sends thinking=none*, 17 comments): A persistent configuration gap where cron jobs send an unsupported `thinking` value to OpenAI models, causing hard failures.

### Highest Community Demand (👍)
- **[Issue #39604](openclaw/openclaw Issue #39604)** (*Feature: private network access for web_fetch*, 9 👍): Overwhelming user request for a simple config toggle (`tools.web.fetch.allowPrivateNetwork`) to reach internal network addresses. Blocked on security review and product decision.
- **[Issue #80715](openclaw/openclaw Issue #80715)** (*Slack replies silently dropped*, 8 👍): Users report significant frustration over replies composed in the transcript that never post via the Slack API, with no error surfaced to the user.
- **[Issue #67035](openclaw/openclaw Issue #67035)** (*Windows chat UI regression*, 14 comments, 0 👍): A highly active thread on the 2026.4.14 Windows UI regression where typed input is swallowed and streamed replies are invisible until refresh.

### Recurring Regressions
- **[Issue #88312](openclaw/openclaw Issue #88312)** (*Codex turn-completion stall returned*, 10 comments, 2 👍): Users have bisected this down to a regression of Issue #84076 (fixed by PR #85107) that re-emerged in 2026.5.27. This demonstrates a sophisticated user base actively tracking commit-level side effects.

## 5. Bugs & Stability
Stability remains the dominant theme, with a cluster of high-severity regressions impacting core workflows.

### Critical / Priority 1 Regressions
- **Codex Runtime:** The "turn-completion stall" has returned (**Issue #88312**). Plugin approval stalls in Codex are causing tool-execution timeouts in Nextcloud Talk sessions (**Issue #86047**).
- **Session & Message Loss:** `sessions.json` unbounded growth causes gateway OOM (**Issue #55334**). ACP parent sessions remain stuck until manual UI refresh (**Issue #52249**). Slack replies silently dropped (**Issue #80715**).
- **Channel Duplication:** Telegram agents sending 2–10x duplicate replies per user message persists (**Issue #86519**), with a previous update only reducing severity.
- **Provider & Auth:** Bedrock `image` tool fails for IAM roles (**Issue #72031**). MiniMax Portal OAuth cannot auto-refresh (**Issue #77467**). Agents completely ignore workspace profiles after reinstall on Ollama (**Issue #85773**).

### Newly Reported (06-02 / 06-03)
- **sessions_spawn auth failure:** Child runs fail with `HTTP 401 Missing scopes: api.responses.write` (**Issue #89549**).
- **Telegram /compact broken:** Manual compaction slash command broken post-upgrade (**Issue #89525**, regression).
- **Timeout compaction failures:** Compaction reports success but leaves Codex sessions unrecoverable (**Issue #89374**).
- **Corrupted header wipe:** Fixed by PR #89065, but users reported silent data loss before patch.

### Fix PRs in Progress
- **Issue #86036** (CJK IME composition fix in WebUI) has a ready PR.
- **Issue #88052** (debug proxy crash on upstream disconnect) has a ready PR.
- **Issue #89678** (macOS LaunchAgent restart failure) has a PR awaiting author.

## 6. Feature Requests & Roadmap Signals
The project trajectory is clearly toward deeper platform integration, better developer ergonomics, and improved channel parity.

### Likely Upcoming Releases
- **SQLite Session Migration** (**Issue #88838**): The formal tracking issue for this major architectural overhaul has high engagement, suggesting it is a top priority for the next minor release.
- **Private Network Access** (**Issue #39604**): With 9 👍 and a clear design spec, this is a high-probability addition once the security and product reviews clear.
- **Followup Queue Persistence** (**PR #82572**): A critical reliability feature preventing message loss across gateway restarts, actively being PR'd.
- **Model Failover Hooks** (**PR #70990**): Adding plugin observability hooks for model failover decisions, signaling a push toward enterprise-grade fault tolerance.

### Quality of Life & User Requests
- **UI/UX:** Collapsible recent sessions menu (**Issue #84216**); preserve visible chat stream text on stale history / terminal errors (**PR #89530**).
- **Extensibility:** Pre-routing inbound message hook for channel bridging / proxying (**Issue #81061**); `acceptSilentStop` flag for cron jobs (**Issue #76159**).
- **Provider Expansion:** First-class Xiaomi MiMo Token Plan support (**Issue #86169**, closed); Batch memory embedding over files (**PR #89138**).

### Community Plugin Innovation
- **[PR #89677](openclaw/openclaw PR #89677)** proposes an "ApexSpiral ΔG Self-Evolution Framework" plugin, showcasing the platform's extensibility for experimental self-reflective agent architectures.

## 7. User Feedback Summary
The OpenClaw user base is technically sophisticated, deeply reliant on the platform for production agent orchestration, and active in upstream debugging.

### Pain Points: Regression Fatigue
- *"After upgrading to 2026-3-22 my main agent is not able to contact other agents."* (**Issue #52875**)
- *"After updating from v2026.5.26 to v2026.5.27, the feishu channel fails to dispatch."* (**Issue #87646**, closed)
- *"Agents completely ignore workspace files content and skills"* after reinstall (**Issue #85773**)
- The consistent pattern of core feature regressions across release updates is the single largest source of user dissatisfaction. Users frequently report that sessions simply "stop working" without clear error messages.

### Pain Points: Silent Failures & Data Loss
- *"Slack replies are composed in transcript but never posted to Slack"* (**Issue #80715**)
- *"Phantom run returns status: ran in 78ms but no model turn executed"* (**Issue #86090**)
- *"sessions.json unbounded growth causes OOM"* (**Issue #55334**)
- Users express frustration with "false success" states that erode trust in the system.

### Positive Engagement Signals
- **Sophisticated Debugging:** Users are actively bisecting regressions and identifying root causes: *"This is a regression of #84076 (fixed by #85107)"* (**Issue #88312**).
- **Strong Contribution Pipeline:** Many fixes are submitted by the community (PR #89681 for UI, PR #89659 for Feishu), indicating a healthy and committed contributor base despite stability struggles.

## 8. Backlog Watch
A significant number of high-impact issues are aging on the backlog, awaiting maintainer review or product decisions.

### Critical, Unresolved (Open 2+ Months)
| Issue | Date | Severity | Status |
|-------|------|----------|--------|
| **#55334** Gateway OOM from `sessions.json` growth | 2026-03-26 | P1 | `needs-maintainer-review`, `needs-product-decision` |
| **#52249** ACP parent session stuck until refresh | 2026-03-22 | P1 | `needs-maintainer-review`, `needs-product-decision` |
| **#41199** Agent-to-Agent tool parameter conflicts | 2026-03-09 | P1 | Blocked: core feature broken for 3 months |
| **#67035** Windows WebChat UI regression | 2026-04-15 | P1 | `needs-maintainer-review` |
| **#72031** Bedrock image tool auth fail (IAM roles) | 2026-04-26 | P1 | `linked-pr-open` |
| **#77467** MiniMax OAuth auto-refresh not implemented | 2026-05-04 | P1 | `needs-maintainer-review` |
| **#86519** Telegram duplicate replies | 2026-05-25 | P1 | `needs-maintainer-review`, `needs-info` |

### Blocked on Process
- **[Issue #39604](openclaw/openclaw Issue #39604)** (2026-03-08, 9 👍): Private network fetch. Blocked by `needs-product-decision` and `needs-security-review`.
- **[Issue #45269](openclaw/openclaw Issue #45269)** (2026-03-13): `apply_patch` tool stripped from agent policy pipeline. Blocked on `needs-product-decision` and `needs-security-review`.
- **[Issue #60841](openclaw/openclaw Issue #60841)** (2026-04-04): `toolsAllow` cannot re-expose core tools in embedded cron runs. Blocked on `needs-product-decision` and `needs-security-review`.

The accumulation of unresolved P1 issues on the backlog—many running for 2–3 months—represents a growing risk to long-term project health, particularly for users relying on multi-agent collaboration, specific cloud provider auth flows, and non-English UI input methods.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the June 3, 2026 community digests.

---

## Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-03
**Scope:** AI Agent / Personal AI Assistant Open-Source Projects

---

### 1. Ecosystem Overview

The open-source AI agent ecosystem is experiencing a bifurcation between scale-driven maturity and architecture-driven innovation. Mature reference platforms like **OpenClaw** and **IronClaw** are grappling with significant regression fatigue and technical debt, while next-generation forks and new entrants (**ZeroClaw**, **NanoBot**, **CoPaw**) are capitalizing on leaner architectures and tighter feedback loops. The Model Context Protocol (MCP) has emerged as the universal transport layer, but its reliability and provider-compatibility friction remain the single largest pain point across all projects. A strong trend towards **security hardening** and **cost-aware architecture** suggests the ecosystem is shifting from rapid prototyping towards production-grade deployment, making stability the primary competitive differentiator.

---

### 2. Activity Comparison (24h Ending 2026-06-03)

| Project | Issues Updated (Open/Active) | PRs Updated | PRs Merged/Closed | Release Status | Ecosystem Role | Health Score |
|---|---|---|---|---|---|---|
| **OpenClaw** | 425 (272 active, 153 closed) | 500 (391 open, 109 merged) | 109 | None | Reference / Generalist OS | **6/10** |
| **IronClaw** | 30 | 50 | 31 | None (latest v0.28.2) | Advanced Automation (Reborn) | **6/10** |
| **Hermes Agent** | 50 (41 open) | 50 | 7 | None (latest v0.15.1) | Enterprise Multi-Platform | **7/10** |
| **CoPaw** | 36 (16 open, 20 closed) | 31 (21 open, 10 merged) | 10 | Beta v1.1.11b1 prepared | Multi-Agent / Security | **8/10** |
| **ZeroClaw** | 33 (All closed) | 47 (All merged) | 47 | **New** v0.8.0-beta-2 | Terminal-First / Secure (Rust) | **9/10** |
| **NanoBot** | 9 | 25 | 17 | None | Lightweight / WebUI-First | **8/10** |
| **PicoClaw** | N/A | 14 | 6 | Nightly v0.2.9 | Go-based Lightweight | **7/10** |
| **LobsterAI** | 0 | 9 | 6 | None | Rich Output (Artifacts) | **8/10** |
| **NanoClaw** | 1 | 6 | 4 | None | Plugin / Container Runner | **8/10** |
| **NullClaw** | 1 | 1 | 0 | None | Security Utility | **8/10** |
| **Moltis** | 1 | 1 | 0 | None | Session Robustness | **7/10** |
| **TinyClaw** | 0 | 0 | 0 | N/A | Dormant | **5/10** |
| **ZeptoClaw** | 0 | 0 | 0 | N/A | Dormant | **5/10** |

*Health Score is a composite assessment including velocity, response time to critical bugs, regression prevalence, and backlog discipline.*

---

### 3. OpenClaw’s Position

OpenClaw remains the **hegemonic reference platform** by pure volume—its 24-hour activity (500 PRs, 425 issues) dwarfs every other project combined. However, this scale is a liability as much as an asset.

**Advantages vs. Peers:**
- **Unmatched Breadth:** The deepest integration surface for channels (Telegram, Slack, Feishu), agent infrastructure, and community plugins (e.g., self-evolution frameworks).
- **Network Effects:** The largest contributor base, ensuring long-term survival even with high churn.

**Technical Approach Differences:**
- OpenClaw follows a **monolithic Python core** with deep channel abstraction. It is highly coupled, making surgical patches risky. Major architectural shifts (e.g., SQLite migration via "branch-by-abstraction") are slow.
- In contrast, **ZeroClaw** (Rust, TUI-first, Bubblewrap sandbox) and **IronClaw** (Reborn event-driven architecture) are built with stricter modularity and security boundaries from the ground up.

**Community Size Comparison:**
- **OpenClaw** possesses an order of magnitude more active participants. The gap between it and the next tier (IronClaw, Hermes) is widening, but the **quality of engagement is degrading**. Regression fatigue ("*sessions just stop working*", "*this is a regression of #84076*") is the dominant user sentiment. The project is the "safe choice" for deployment scale but is increasingly viewed as the highest-maintenance option for stability.

---

### 4. Shared Technical Focus Areas

Multiple projects are independently converging on the same pain points, indicating high-priority requirements for the entire ecosystem:

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **MCP Reliability** | IronClaw, NanoBot, NanoClaw, LobsterAI | Session termination recovery, proxy compatibility, launch latency reduction, silent execution failures. |
| **Provider Parameter Friction** | IronClaw, Hermes, PicoClaw, CoPaw, ZeroClaw | Robust parameter filtering (e.g., Claude Opus `temperature`), graceful degradation for API changes, custom provider support. |
| **Session & Context Integrity** | OpenClaw, PicoClaw, Moltis | Corruption recovery, size capping for tool results, prevention of cross-contamination on restore. |
| **Security Hardening** | ZeroClaw, CoPaw, NullClaw, NanoClaw | Default sandboxing, vulnerability disclosure pipelines, PII redaction accuracy, injection validation. |
| **Channel Fragility** | OpenClaw, CoPaw, ZeroClaw | Upstream protocol bumps (WhatsApp, WeChat), silent message drops, duplicate delivery regression. |
| **Onboarding & Config UX** | ZeroClaw, OpenClaw, Hermes, NanoBot | "Default model" edge cases, first-run wizard confusion, Windows-specific regressions, `uv tool` packaging. |

**Key Insight:** MCP and Provider parameter handling are the two highest-impact areas for platform developers. Fixing these generically would benefit nearly every project in the space.

---

### 5. Differentiation Analysis

While the ecosystem shares core infrastructure challenges, projects are diverging sharply in feature focus and target users.

| Project | Target User | Primary Feature Focus | Technical Architecture | Key Differentiator |
|---|---|---|---|---|
| **OpenClaw** | Generalist / Ops | Breadth of integrations | Monolithic Python | The "Standard Library" of agents |
| **ZeroClaw** | Developer / Security-Conscious | Terminal UI, sandboxing | Rust, Ratatui, Bubblewrap | Security-by-default + TUI power |
| **IronClaw** | Advanced Automation | Reborn (scheduled/event-driven) | Event-driven, OAuth-centric | Trigger-based multi-agent orchestration |
| **Hermes Agent** | Enterprise | Desktop app, i18n, secret mgmt | Python, Electron, Codex WS | Corporate compliance & multi-OS (Intel Mac gap) |
| **NanoBot** | Lightweight / Web | WebUI polish, channel expansion | Python, uv packaging | "Just works" low-friction experience |
| **CoPaw** | Asian Market / Educators | Multi-model subagents, WeChat | AgentScope framework | Education sector signal + multi-model orchestration |
| **LobsterAI** | Creative / Richer UX | Artifacts, Cowork subagents | Electron, internal polish | Client-rendered rich outputs |
| **PicoClaw** | Performance / Microservices | Stability, streaming control | Go | Low footprint, high throughput |
| **NullClaw** | Privacy | PII redaction, safety | Focused utility | Zero false-positive rate redaction |

---

### 6. Community Momentum & Maturity

The ecosystem can be divided into four distinct phases:

**1. High-Growth / Stabilizing Sprint:**
- **ZeroClaw** (Health: 9) is the standout. v0.8.0-beta-2 launched with relentless bug squashing. 47 PRs merged, 33 issues closed. The tight Rust codebase and strict security posture give it the strongest velocity-to-quality ratio.
- **CoPaw** (Health: 8) is building strong trust through rapid security triage (7 disclosure issues resolved in 24h) and a clear beta release path.
- **NanoBot** (Health: 8) is aggressively expanding its channel footprint while polishing UX. High contributor responsiveness.

**2. High Churn / Debt Management:**
- **OpenClaw** (Health: 6) and **IronClaw** (Health: 6) are iterating at massive velocity but suffering the cost of architectural complexity. OpenClaw’s 500 PRs mask a deep backlog of unresolved P1s. IronClaw’s 31 merges are counterbalanced by a failing CI pipeline and a critical Claude Opus lockout. The user base is sophisticated but visibly frustrated.

**3. Steady State / Polish:**
- **LobsterAI** (Health: 8), **Hermes Agent** (Health: 7), **PicoClaw** (Health: 7), and **NanoClaw** (Health: 8) are in controlled feature integration phases. They are less volatile but risk being overtaken by faster-moving peers if they do not accelerate.

**4. Dormant:**
- **TinyClaw** and **ZeptoClaw** showed zero activity. Moltis is in a deliberate low-activity refinement phase.

**Bottom Line:** ZeroClaw is the most momentum-driven project in the report. OpenClaw is too big to fail but is currently failing its users on stability.

---

### 7. Trend Signals

For technical decision-makers and AI agent developers, the data reveals the following high-value signals:

- **The "MCP Reliability Tax":** Every major project is fighting MCP transport fragility. Investing in a robust, retry-capable, and proxy-aware MCP stack is the highest ROI architectural investment right now.
- **Channel Fragmentation is Unsustainable:** Hardcoded integrations against upstream APIs (Telegram, WhatsApp, WeChat) create constant regression risk. An abstracted channel protocol or a proxy daemon is a missing market opportunity.
- **"Security as a Feature" is Now Table Stakes:** The rapid response to the CoPaw disclosure wave and the ZeroClaw sandbox enforcement signals that security is no longer an afterthought. Expect SBOM support and approval manager audits to become standard requirements for enterprise adoption.
- **Cost-Awareness Driving Model Routing:** Explicit discussions about token cache optimization (NanoBot) and model failover hooks (OpenClaw) suggest the era of "use the best model for everything" is ending. Agents must expose cost analytics and routing.
- **The TUI vs. WebUI Tension:** The strong reception of ZeroClaw’s Ratatui TUI indicates a significant segment of power users prefers the terminal over increasingly complex web UI stacks. Agent frameworks should consider native terminal output formats.
- **Regression Fatigue is the #1 Retention Risk:** The most repeated pain point is "after upgrading, X stopped working." Prioritizing a stable LTS track or a strict semantic versioning commitment—rather than nightly/rolling releases—could be the best competitive advantage for projects like OpenClaw and IronClaw.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest | 2026-06-03

## 1. Today’s Overview
NanoBot experienced an exceptionally high-velocity development cycle on June 2–3, with **25 pull requests updated** and **9 issues touched** in the last 24 hours. The project maintainers successfully merged **17 PRs**—a massive single-day throughput—while 8 new feature and bugfix PRs remain open for review. Focus this cycle was concentrated on **WebUI reliability**, **channel expansion** (Napcat/QQ and email attachments), and **core architecture improvements** (Dream refactor, lightweight RAG). Community contributors were notably active around packaging fixes for the `uv tool` ecosystem and OpenAI API compatibility gaps. No formal release was cut today, but the volume and quality of merged code strongly suggest a significant release is crystallizing.

## 2. Releases
*No new releases were published in the last 24 hours.*

## 3. Project Progress
**Merged/closed PRs today: 17 items.**

- **Memory & Retrieval**
    - A major feature landed: **lightweight RAG for memory retrieval** using local embeddings ([#4109](https://github.com/HKUDS/nanobot/pull/4109)).
- **Dream Architecture**
    - The two-phase `Dream` class was replaced with a simpler **cron + process_direct** flow, removing technical debt from the background agent scheduler ([#3990](https://github.com/HKUDS/nanobot/pull/3990)).
- **Channels**
    - **Napcat (QQ) channel** backported and merged, adding OneBot v11 protocol support for private/group chats ([#4146](https://github.com/HKUDS/nanobot/pull/4146)).
    - The **email channel now supports file attachments** via two converging PRs ([#4162](https://github.com/HKUDS/nanobot/pull/4162), [#4160](https://github.com/HKUDS/nanobot/pull/4160)).
- **WebUI Stability (4 fixes merged)**
    - Startup fetches now have bounded timeouts to prevent infinite loading ([#4157](https://github.com/HKUDS/nanobot/pull/4157)).
    - Hash-routing persists WebUI location; refresh correctly restores active chat ([#4150](https://github.com/HKUDS/nanobot/pull/4150)).
    - "Chats" sidebar group now correctly sorted by recency ([#4151](https://github.com/HKUDS/nanobot/pull/4151)).
    - Fallback `document.execCommand("copy")` added when Clipboard API is unavailable ([#4149](https://github.com/HKUDS/nanobot/pull/4149)).
- **Core Fixes**
    - Runner fixed to prevent **infinite offload loop** when `read_file` recovers persisted tool results ([#4155](https://github.com/HKUDS/nanobot/pull/4155)).
    - WebUI gateway dependencies successfully **decoupled from WebSocket channel** ([#4115](https://github.com/HKUDS/nanobot/pull/4115)).
    - Auto-fix applied for `uv tool` pip installation issue ([#4159](https://github.com/HKUDS/nanobot/pull/4159)).

## 4. Community Hot Topics
| Issue / PR | Comments | Core Discussion |
|---|---|---|
| [#4167](https://github.com/HKUDS/nanobot/issues/4167) *Image generation fails* | 2 | Hard crash when OpenAI-compatible APIs (e.g., Agnes AI) don't support `response_format`. High urgency for third-party provider users. |
| [#4158](https://github.com/HKUDS/nanobot/issues/4158) *WebUI CLI pip under uv tool* | 1 | Fundamental UX failure: CLI app installation is broken when NanoBot is launched via `uv tool`. Spawned multiple competing fix PRs ([#4159](https://github.com/HKUDS/nanobot/pull/4159), [#4164](https://github.com/HKUDS/nanobot/pull/4164)). |
| [#4142](https://github.com/HKUDS/nanobot/issues/4142) *Cache miss cost optimization* | 1 | Power-user discussion on optimizing API tokens for cache misses, specifically targeting DeepSeek v4 flash/pro models. Closed but signals cost-conscious community. |
| [#4166](https://github.com/HKUDS/nanobot/issues/4166) *Subagent MCP access* | 0 | Users need spawned subagents to access MCP-created tools—a blocker for complex multi-step workflows. |
| [#4163](https://github.com/HKUDS/nanobot/pull/4163) *Fork-from-here WebUI* | 0 | New UX feature allowing users to fork conversation history from any user message. Strong quality-of-life signal. |

## 5. Bugs & Stability
**Critical**
- **MCP Session Termination** ([#4168](https://github.com/HKUDS/nanobot/issues/4168)): MCP servers become unreachable after random time (`McpError: Session terminated`). Only full NanoBot restart resolves. **No fix PR yet.**

**High**
- **Image Generation Hard Crash** ([#4167](https://github.com/HKUDS/nanobot/issues/4167)): `generate_image` breaks on any provider that rejects `response_format`. Potential fix via custom provider support ([#4132](https://github.com/HKUDS/nanobot/issues/4132)).
- **Session History Corruption** ([#4169](https://github.com/HKUDS/nanobot/pull/4169)): Corrupt `last_consolidated` offset can hide all history behind a valid session. Fix exists in open PR (reset out-of-range offset to 0).

**Medium / Resolved**
- **MemoryStore Duplicate Cursors** ([#4081](https://github.com/HKUDS/nanobot/issues/4081)): Concurrent writes under async produced duplicate history cursors. **Fixed**.
- **Empty Emails After Tool Calls** ([#4165](https://github.com/HKUDS/nanobot/pull/4165)): Progress messages sent as regular outbound emails. **Fixed**.
- **`read_file` Offload Loop** ([#4155](https://github.com/HKUDS/nanobot/pull/4155)): Recovery path for large tool results caused infinite loop. **Fixed**.

## 6. Feature Requests & Roadmap Signals
- **Virtually certain for next release:**
    - **Custom Image Generation Providers** ([#4132](https://github.com/HKUDS/nanobot/issues/4132)). Directly addresses the critical bug in [#4167](https://github.com/HKUDS/nanobot/issues/4167) and is explicitly labeled "good first issue".
    - **Subagent MCP Access** ([#4166](https://github.com/HKUDS/nanobot/issues/4166)). High community demand; subagents are currently crippled without MCP tools.
- **Strong candidates for next minor release:**
    - **Cloud Deployment Layer** ([#4139](https://github.com/HKUDS/nanobot/pull/4139)): +851 lines adding zero-dependency HF Spaces & ModelScope Studio support.
    - **"Fork-from-Here" WebUI** ([#4163](https://github.com/HKUDS/nanobot/pull/4163)): Already submitted by community with maintainer interest.
    - **MCP URL SSRF Guard** ([#4123](https://github.com/HKUDS/nanobot/pull/4123)): Security hardening for MCP SSE and streamable HTTP connections.

## 7. User Feedback Summary
The community is actively **stress-testing NanoBot in production-like environments**, revealing clear friction points:
1. **MCP reliability** is the top stability concern; users need persistent sessions without random termination.
2. **Provider API strictness** creates integration friction; the `response_format` issue blocks alternative image generation providers entirely.
3. **Modern Python packaging** under `uv tool` is a significant UX barrier that drew immediate community fix attempts.
4. **Subagent capabilities** are limiting autonomous workflows; users need spawn() agents to inherit MCP tools.

Positive signals: the rapid merge cadence (especially WebUI polish and channel expansion) demonstrates high project velocity. The detailed **cache-miss cost optimization discussion** ([#4142](https://github.com/HKUDS/nanobot/issues/4142)) confirms a technically sophisticated, cost-conscious user base actively shaping the roadmap.

## 8. Backlog Watch
| Item | Age | Status |
|---|---|---|
| [#1168](https://github.com/HKUDS/nanobot/issues/1168) *Notion MCP Connection Failure* | Since Feb 2026 (3+ months) | **Stale.** Major integration gap for a core platform. Updated but unresolved. |
| [#3983](https://github.com/HKUDS/nanobot/pull/3983) *Test coverage for blocked finish reasons* | Since May 24 (9 days) | **Pending review.** Foundation for runner reliability but unmerged. |
| [#4123](https://github.com/HKUDS/nanobot/pull/4123) *MCP URL SSRF validation* | Since May 31 (3 days) | **Pending review.** Mature defensive PR with test coverage. |
| [#4134](https://github.com/HKUDS/nanobot/pull/4134) *WebSocket error event handling* | Since June 1 (2 days) | **Pending review.** Adds proper error events for permission denials. |
| [#4168](https://github.com/HKUDS/nanobot/issues/4168) *MCP session termination* | Since June 2 (1 day) | **Critical bug, no fix PR.** Needs maintainer escalation. |

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-06-03  
**Repo:** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. Today's Overview

The Hermes Agent project sustained an exceptionally high tempo on June 3, with **50 Issues** and **50 Pull Requests** updated in the last 24 hours. 9 issues were closed and 7 PRs were merged or closed, reflecting strong community engagement and a responsive core engineering team. Mainline development is heavy on multi-platform polish (Feishu, Desktop, TUI) and laying groundwork for enterprise features (i18n, advanced secret management, Codex WebSocket transport). However, a cluster of **three P1 infrastructure bugs**—the broken Matrix Docker image, the Discord gateway turn termination, and the provider inline API key resolution failure—remain open with no fix PRs, posing a growing risk to release channel trust and user satisfaction.

**Key Metrics:**
- Open Issues: 41 | Closed in last 24h: 9
- Open PRs: 43 | Merged/Closed in last 24h: 7
- New Releases: 0

---

## 2. Releases

*No new releases were published in the last 24 hours.* The most recent known stable is `v0.15.1` (2026-05-29), referenced in the bug report environment for issue [#37812](https://github.com/NousResearch/hermes-agent/issues/37812).

---

## 3. Project Progress (Merged/Closed PRs & Closed Issues)

The following represent noteworthy closures and merges from the period:

**Merged/Closed PRs:**
- [#34559](https://github.com/NousResearch/hermes-agent/pull/34559) – *fix(switcher): respect discover_models:false in custom_providers section*. Resolves a configuration override bug affecting model selection in the `/model` picker.
- [#35145](https://github.com/NousResearch/hermes-agent/pull/35145) – *fix(model_switch): merge live API models with user-configured models*. Fixes a critical regression where provider discovery could overwrite user-configured model entries.
- [#37786](https://github.com/NousResearch/hermes-agent/pull/37786) – *fix(tui): clear selection on right-click copy + clearer block boundaries*. Polish for the terminal UI text interaction.
- [#37855](https://github.com/NousResearch/hermes-agent/pull/37855) – *chore: remove committed RELEASE_v*.md changelogs from repo root*. Standardizes repository hygiene.

**Closed High-Impact Issues:**
- [#37399](https://github.com/NousResearch/hermes-agent/issues/37399) – **Desktop remote mode WebSocket origin rejection** (P2, bug). Root cause: Electron WebSocket origins rejected on non-loopback dashboard binds. Resolved.
- [#37813](https://github.com/NousResearch/hermes-agent/issues/37813) – **ACP mode ignores platform_toolsets** (P3, bug). Memory provider tools (e.g. `hindsight_retain`) gated out in ACP sessions. Resolved.
- Multiple **autonomous triage E2E test validation issues** (e.g. [#37806](https://github.com/NousResearch/hermes-agent/issues/37806), [#37801](https://github.com/NousResearch/hermes-agent/issues/37801)) were closed by the test author, indicating active internal CI/automation pipeline development.

---

## 4. Community Hot Topics

The community is deeply engaged in both debugging regressions and shaping the future architecture of the agent.

### Most Active Issues
- **[#25495](https://github.com/NousResearch/hermes-agent/issues/25495) – Matrix / synapse broken in official Docker image** (P1, 10 comments)  
  *Underlying need:* The official Docker distribution channel has a critical boot regression. Users report the image "stays at fixing ownership: 1000" and never completes. A working SHA was identified, but the root cause (likely a git/dependency issue in the entrypoint) remains unaddressed. This is the single highest-pain issue on the board.

- **[#31392](https://github.com/NousResearch/hermes-agent/issues/31392) – RFC: Agent-native task relay with auto-forking subagents** (8 comments)  
  *Underlying need:* A strong desire for complex, multi-step query orchestration without losing context or requiring manual segmentation. Users want the agent to autonomously fork sub-agents for parallel workstreams and manage human approval gates asynchronously.

- **[#27221](https://github.com/NousResearch/hermes-agent/issues/27221) – entrypoint.sh misses chown for ui-tui/ and gateway/** (P2, 6 comments, 2 👍)  
  *Underlying need:* Docker host UID remapping is critical for NAS users (Unraid/Synology). The entrypoint's incomplete `chown` breaks TUI and gateway directories when `HERMES_UID` is remapped.

- **[#37447](https://github.com/NousResearch/hermes-agent/issues/37447) – DIKW Memory System: 4-layer self-healing loop** (2 comments, 2 👍)  
  *Underlying need:* A sophisticated community "Show & Tell" submission. Users are building advanced context/memory management on top of the Holographic memory plugin, signaling a demand for a more capable built-in memory pipeline.

- **[#37812](https://github.com/NousResearch/hermes-agent/issues/37812) – Desktop approval prompts do not render** (P2, 2 comments, 1 👍)  
  Immediate report of a functional regression in the Desktop GUI—a direct hit to user trust in the approved binary.

---

## 5. Bugs & Stability

### Critical (P1) – No Fix PRs
| Issue | Summary | Impact |
|-------|---------|--------|
| [#25495](https://github.com/NousResearch/hermes-agent/issues/25495) | Matrix/Synapse Docker boot hang | Blocks all users relying on official Docker image |
| [#14065](https://github.com/NousResearch/hermes-agent/issues/14065) | Custom providers drop inline `api_key` at runtime | Core configuration system regression; provider auth fails silently |
| [#27881](https://github.com/NousResearch/hermes-agent/issues/27881) | Discord Gateway premature turn termination | Primary gateway UX degraded; agent cuts off mid-response |

### High (P2) – Mix of Open & Fixes Inbound
- [#27221](https://github.com/NousResearch/hermes-agent/issues/27221) – Docker UID remap incomplete *No fix PR*
- [#24012](https://github.com/NousResearch/hermes-agent/issues/24012) – Agent spews token-wasting unverified alternatives on tool failure *No fix PR*
- [#37827](https://github.com/NousResearch/hermes-agent/issues/37827) – Windows setup error (git checkout failure) *No fix PR, needs reproduction*
- [#37812](https://github.com/NousResearch/hermes-agent/issues/37812) – Desktop approval prompts not rendering **→ Fix PR [#37856](https://github.com/NousResearch/hermes-agent/pull/37856) open**
- [#37847](https://github.com/NousResearch/hermes-agent/issues/37847) – Feishu approval resolver authorization bug **→ Fix PR [#37847](https://github.com/NousResearch/hermes-agent/pull/37847) open**
- [#37849](https://github.com/NousResearch/hermes-agent/issues/37849) – Feishu historical user ID authorization regression **→ Fix PR [#37849](https://github.com/NousResearch/hermes-agent/pull/37849) open**
- [#37854](https://github.com/NousResearch/hermes-agent/issues/37854) – Dangerous command detection false positives (e.g. `echo rm -rf /`) **→ Fix PR [#37854](https://github.com/NousResearch/hermes-agent/pull/37854) open**
- [#37853](https://github.com/NousResearch/hermes-agent/issues/37853) – Profile name normalization failure **→ Fix PR [#37853](https://github.com/NousResearch/hermes-agent/pull/37853) open**

### Moderate (P3) – Desktop & Platform
- [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) – Desktop DMG is arm64-only, fails on Intel Macs *No fix PR*
- [#37527](https://github.com/NousResearch/hermes-agent/issues/37527) – Desktop chat scroll snaps back on upward wheel scroll **→ Fix PR [#37831](https://github.com/NousResearch/hermes-agent/pull/37831) open**
- [#37851](https://github.com/NousResearch/hermes-agent/issues/37851) – MiniMax `new_sensitive` content policy not caught by blocked-pattern list **→ Fix PR [#37851](https://github.com/NousResearch/hermes-agent/pull/37851) open**

**Summary:** The team is rapidly deploying targeted fixes for P2/P3 surface-level bugs (TUI, Desktop binding, Feishu auth, MiniMax, profile norms). However, the three P1 infrastructure bugs remain open without any obvious recovery path visible in this window, which is a growing project health risk.

---

## 6. Feature Requests & Roadmap Signals

### Strong Upstream Indicators (Open Feature PRs)
- [#36896](https://github.com/NousResearch/hermes-agent/pull/36896) – **1Password (`op://`) secret source** for provider credentials. Enterprise security chain.
- [#35127](https://github.com/NousResearch/hermes-agent/pull/35127) – **Enterprise-grade i18n framework** for CLI and Gateway. A massive PR signaling serious internationalization investment.
- [#35911](https://github.com/NousResearch/hermes-agent/pull/35911) – **Multiple Feishu/Lark app support** via `FEISHU_MULTI_APP` env var. High priority on Chinese enterprise market.
- [#37392](https://github.com/NousResearch/hermes-agent/pull/37392) – **Codex Responses WebSocket transport** (provider-gated). New low-latency provider transport layer.
- [#37846](https://github.com/NousResearch/hermes-agent/pull/37846) – **Dashboard Telegram QR onboarding**. UX improvement for gateway onboarding.

### Community Features with High Inclusion Probability
- [#27742](https://github.com/NousResearch/hermes-agent/issues/27742) – Agent internal clock. Considered fundamental for autonomous deadline/commitment management.
- [#12213](https://github.com/NousResearch/hermes-agent/issues/12213) – Expose `compress_context` as a native Tool. Low complexity, high value for long-running sessions.
- [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) – Expose `model_switch` as agent-callable tool. Enables autonomous cost/speed/quality routing.
- [#31392](https://github.com/NousResearch/hermes-agent/issues/31392) – Agent-native task relay with sub-agent forking. The "killer app" for complex orchestration.

### Strategic Product Signals
- [#37835](https://github.com/NousResearch/hermes-agent/issues/37835) – **PRD: Mobile-first Mac chat hub (v1)**. A formal product requirement document published directly to the issue tracker, signaling official product planning beyond open-source iteration.
- [#32507](https://github.com/NousResearch/hermes-agent/issues/32507) & [#35709](https://github.com/NousResearch/hermes-agent/issues/35709) – Audit decision trails and OpenCode governance. Community is actively designing the accountability and security layers for autonomous coding.
- [#37491](https://github.com/NousResearch/hermes-agent/issues/37491) – One-click installer for Windows users in China. Specific regional access barrier raised.

---

## 7. User Feedback Summary

**Pain Points & Dissatisfaction Signals:**
- **Docker Channel Fragility:** The Matrix image breakage ([#25495](https://github.com/NousResearch/hermes-agent/issues/25495)) and UID remap bug ([#27221](https://github.com/NousResearch/hermes-agent/issues/27221)) point to an unreliable official container distribution channel, the primary deployment method for self-hosters.
- **Desktop GUI Regressions:** Multiple immediate reports of functional regressions (approval prompts [#37812](https://github.com/NousResearch/hermes-agent/issues/37812), scroll snapping [#37527](https://github.com/NousResearch/hermes-agent/issues/37527), Intel Mac compatibility [#37505](https://github.com/NousResearch/hermes-agent/issues/37505)) suggest a rapidly growing installed base of non-CLI users who are highly sensitive to release quality.
- **Config System Gaps:** Reports of providers dropping API keys ([#14065](https://github.com/NousResearch/hermes-agent/issues/14065)) and ACP mode ignoring platform toolsets ([#37813](https://github.com/NousResearch/hermes-agent/issues/37813)) reveal brittleness in the v12+ configuration resolution layer.
- **Missing Autonomous Intelligence:** Users report the agent cannot track time ([#27742](https://github.com/NousResearch/hermes-agent/issues/27742)), wastes tokens guessing alternatives after failures ([#24012](https://github.com/NousResearch/hermes-agent/issues/24012)), and lacks a unified tool for context compression ([#12213](https://github.com/NousResearch/hermes-agent/issues/12213)).

**Satisfaction Signals:**
- **High-Quality Community RFCs:** Proposals like task relay ([#31392](https://github.com/NousResearch/hermes-agent/issues/31392)), shared memory store ([#31388](https://github.com/NousResearch/hermes-agent/issues/31388)), and the DIKW memory system ([#37447](https://github.com/NousResearch/hermes-agent/issues/37447)) demonstrate a technically sophisticated user base deeply invested in the project's trajectory.
- **Active Third-Party Bug Fixing:** The Feishu authorization fixes ([#37847](https://github.com/NousResearch/hermes-agent/pull/37847), [#37849](https://github.com/NousResearch/hermes-agent/pull/37849)) and MiniMax pattern fix ([#37851](https://github.com/NousResearch/hermes-agent/pull/37851)) were authored by external contributors, demonstrating a healthy and capable open-source ecosystem.
- **Diverse Deployment Scenarios:** Users mention Unraid, Synology, Tailscale, Intel Macs, Discord, Telegram, Matrix, and Feishu—indicating the agent is meeting real-world deployment diversity needs.

---

## 8. Backlog Watch

The following high-merit items have gone without meaningful maintainer engagement or movement for an extended period:

### Unresolved P1 Bugs (Urgent)
- **[#25495](https://github.com/NousResearch/hermes-agent/issues/25495) – Matrix Docker broken (10 comments, no fix PR).** Current top community pain point. Needs a dedicated fix or a revert strategy.
- **[#14065](https://github.com/NousResearch/hermes-agent/issues/14065) – Provider API key runtime drop (4 comments, no fix PR).** Core v12+ config infrastructure bug with ripple effects.
- **[#27881](https://github.com/NousResearch/hermes-agent/issues/27881) – Discord gateway turn termination (4 comments, no fix PR).** Primary gateway UX bug on a major platform.

### Long-Standing High-Impact Features
- **[#5114](https://github.com/NousResearch/hermes-agent/issues/5114) – Autoresearch skill** (Created 2026-04-04). Ambitious proposal for autonomous git-based experiment loops. Stalled without maintainer signal.
- **[#17272](https://github.com/NousResearch/hermes-agent/issues/17272) – Google Workspace service-account auth** (Created 2026-04-29). Critical blocker for enterprise/robotic deployments using Google tools.
- **[#16525](https://github.com/NousResearch/hermes-agent/issues/16525) – model_switch agent tool** (Created 2026-04-27). High demand, moderate complexity. No recent PR or assignment.

### PRs Requiring Maintainer Review
- **[#35127](https://github.com/NousResearch/hermes-agent/pull/35127) – i18n framework.** Massive codebase change. Requires careful architectural review from core team.
- **[#36896](https://github.com/NousResearch/hermes-agent/pull/36896) – 1Password secret source.** Security-sensitive new feature. Needs security review.
- **[#37392](https://github.com/NousResearch/hermes-agent/pull/37392) – Codex Responses WebSocket transport.** Significant new transport protocol. Needs protocol review.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**Project Digest: PicoClaw (sipeed/picoclaw)**
**Date:** 2026-06-03

---

### 1. Today's Overview
PicoClaw is currently in a heavy stabilization and regression-fix phase following its v0.2.9 nightly cycle. Development velocity remains exceptionally high, with **14 pull requests updated** and **6 merged/closed** in the last 24 hours. The core team, alongside active community contributors, is aggressively patching a wave of regressions, particularly around session history management, context compression configuration, and provider-specific API changes. A new nightly build (`v0.2.9-nightly.20260603`) was released, continuously integrating these rapid fixes. While the torrent of patches indicates some instability from recent builds, the project’s responsiveness to issues is excellent, and project health remains strong.

### 2. Releases
- **Nightly Build: [v0.2.9-nightly.20260603.a502aa7f](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)**
  Automated build tracking the `main` branch. As a nightly, it is considered unstable and intended for testing. It includes all fixes and features merged as of the snapshot date.
  **Full Changelog**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

### 3. Project Progress
The focus of merged work this period is entirely on back-end resilience, tool safety, and provider error handling:
- **Agent Stability**: [PR #2991](https://github.com/sipeed/picoclaw/pull/2991) overhauls LLM retry logic by introducing a universal provider error classifier. Agent turns can now retry transient HTTP 500 errors (e.g., from OpenRouter) instead of failing immediately.
- **Memory Safety**: [PR #2986](https://github.com/sipeed/picoclaw/pull/2986) patches a goroutine leak in the `SessionManager` by introducing a proper `Stop()` mechanism, preventing resource exhaustion in tests and long-running instances.
- **Provider Compatibility**: [PR #2989](https://github.com/sipeed/picoclaw/pull/2989) adds Zhipu API error code 1210 to the error classifier, fixing a bug where image requests from the WeChat channel to GLM-5-Turbo would fail with an unhandled parameter error.
- **Documentation**: [PR #2994](https://github.com/sipeed/picoclaw/pull/2994) / [PR #2993](https://github.com/sipeed/picoclaw/pull/2993) introduce a self-describing `picoclaw-agent` skill guide into the workspace to improve onboarding.
- **Infrastructure**: [PR #2239](https://github.com/sipeed/picoclaw/pull/2239) updates Docker Compose templates to support privileged mode (merged after significant backlog time).

### 4. Community Hot Topics
- **Streaming Configuration Demand**: [Issue #2404](https://github.com/sipeed/picoclaw/issues/2404) remains the highest-traffic open discussion (10 comments). The request for a simple `"streaming": true` config toggle continues to garner strong support from users seeking predictable client behavior independent of provider defaults.
- **WebSocket Protocol Maturation**: [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984) is a new, high-signal feature request from an external tool developer asking for an explicit WebSocket "turn complete" event. This signals growing adoption of PicoClaw as a backend by third-party clients requiring deterministic lifecycle hooks.
- **The "Fix Blitz"**: The coordinated effort by developers `yuxuan-7814` and `chengzhichao-xydt` to submit multiple high-quality fix PRs constitutes the hottest topic of the day. The community is closely watching the resolution of the session cross-contamination bug and the `tool_calls` dropping bug.

### 5. Bugs & Stability
Several regressions and compatibility issues are currently in the pipeline with open fix PRs. The volume of patches is high, but the response time is fast.
- **[CRITICAL] Session History Cross-Contamination**: [PR #2992](https://github.com/sipeed/picoclaw/pull/2992) (Fixes #2972). A severe regression where upgrading to v0.2.9 causes old session aliases to leak into new Web UI sessions. **Status: Open, awaiting merge.**
- **[HIGH] Tool Calls Dropped During Streaming**: [PR #2987](https://github.com/sipeed/picoclaw/pull/2987) (Fixes #2958). The `preSend()` filter in the channel manager incorrectly drops `tool_calls` auxiliary messages during active streams. **Status: Open, awaiting merge.**
- **[HIGH] Context Compression Config Ignored**: [PR #2988](https://github.com/sipeed/picoclaw/pull/2988) (Fixes #2968). The `summarize_token_percent` config setting is effectively ignored by the compression logic. **Status: Open, awaiting merge.**
- **[MEDIUM] Web UI History Truncated**: [PR #2990](https://github.com/sipeed/picoclaw/pull/2990) (Fixes #2796). Web UI only shows the last user message in multi-message conversations. **Status: Open, awaiting merge.**
- **[MEDIUM] Claude Opus 4/7 Deprecation**: [PR #2948](https://github.com/sipeed/picoclaw/pull/2948). Fixes HTTP 400 errors by skipping the deprecated `temperature` parameter. **Status: Stale, awaiting review.**
- **[LOW] Web Search API Compatibility**: [PR #2951](https://github.com/sipeed/picoclaw/pull/2951). Fixes HTTP 400 errors on OpenAI endpoints that don't support `web_search_preview`. **Status: Stale, awaiting review.**

### 6. Feature Requests & Roadmap Signals
- **Near-Term Candidates (v0.2.10 / v0.3.0)**:
  - [#2404](https://github.com/sipeed/picoclaw/issues/2404) **Configurable Streaming**: Unblocks users who need strict control over LLM backend streaming behavior. High demand.
  - [#2984](https://github.com/sipeed/picoclaw/issues/2984) **WebSocket Turn Completion Signal**: Adds a deterministic protocol event, paving the way for robust external client integrations.
- **Long-Term Signal**:
  - [PR #2945](https://github.com/sipeed/picoclaw/pull/2945) **Debug Trace Viewer (`picoclaw-tracer`)**: A major community contribution offering a standalone Web UI for real-time visualization of LLM internals (system prompt, tool calls, messages). If merged, this signals a strong strategic push toward developer experience and debuggability.

### 7. User Feedback Summary
- **Pain Points**: The primary user frustration centers on regressions introduced by the rapid nightly cycle. The session history corruption bug and the broken context compression configuration directly impacted daily workflows, shaking immediate confidence in the v0.2.9 stream. Provider friction (Anthropic deprecations, Zhipu error codes, OpenAI web search types) remains a constant nuisance requiring frequent patching.
- **Satisfaction**: The project team's response time is highly commendable. Multiple critical PRs were submitted within hours of bug reports. This fast turnaround time builds strong trust, even when bugs arise. The community is highly engaged, contributing both large features (the tracer) and detailed, actionable bug reports.

### 8. Backlog Watch
Several valuable contributions risk becoming stale and require maintainer triage:
- **[#2404](https://github.com/sipeed/picoclaw/issues/2404) - Streaming Config Enhancement**: Marked `stale` despite being the highest-demand feature request. Needs prioritization or an explicit decision.
- **[PR #2951](https://github.com/sipeed/picoclaw/pull/2951) - Web Search API Compatibility Fix**: A clean, low-risk fix for endpoint compatibility. Unmerged for over a week.
- **[PR #2948](https://github.com/sipeed/picoclaw/pull/2948) - Claude Opus 4/7 Temperature Fix**: A significant blocker for users of the latest Anthropic models. Left stale.
- **[PR #2945](https://github.com/sipeed/picoclaw/pull/2945) - Debug Trace Viewer**: A substantial feature addition (a new binary + UI). Without maintainer engagement, this complex contribution risks diverging and becoming unmergeable.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest – 2026-06-03**

---

### 1. Today's Overview
NanoClaw is demonstrating strong development velocity. Over the last 24 hours, 4 out of 6 updated pull requests were merged, reflecting an efficient review cycle. The project merged a critical security patch for the container runner, completed a foundational plugin hook system, and shipped a new webchat integration. Development energy is concentrated on standardizing the Codex runtime and resolving MCP transport issues for enterprise proxy environments. No new releases were cut, but the accumulation of features and fixes points toward a significant versioned release on the horizon.

---

### 2. Releases
No new releases were published today.

---

### 3. Project Progress (Merged/Closed PRs)
Four pull requests were closed or merged, advancing both the platform’s feature set and security posture:

- **Plugin Hook System** – PR [#1193](https://github.com/nanocoai/nanoclaw/pull/1193) (`cyber-rye`) merges a host-side hook system that loads `plugins/*/index.js` ES modules exporting `onStartup(ctx)` and `onShutdown()` lifecycle callbacks. This runs after channels connect, enabling plugins to bootstrap long-running services.
- **Security Hardening** – PR [#2538](https://github.com/nanocoai/nanoclaw/pull/2538) (`sebastiondev`) fixes a critical OS command injection vulnerability (CWE-78) by validating package names before Dockerfile interpolation in `buildAgentGroupImage()`.
- **New Skill / Channel** – PR [#2069](https://github.com/nanocoai/nanoclaw/pull/2069) (`javexed`) merges the `webchat v1` skill, adding webchat channel support.
- **Runtime Standardization** – PR [#2674](https://github.com/nanocoai/nanoclaw/pull/2674) (`pinetreelic`) standardizes long-running runtime status messages in the Codex provider, adds metadata, and introduces internal-channel guards to prevent self-loops.

---

### 4. Community Hot Topics
- **Education Automation Signal (Issue #2673)** – The only issue filed in the last 24 hours ([#2673](https://github.com/nanocoai/nanoclaw/issues/2673) by `smartgain2026`) proposes an *Automated Student Grading System*. The description is an AI video/prompt detail, but the underlying need is clear: users want private, on-device AI agents for spreadsheet processing and educational grading.
- **MCP & Proxy Compatibility (PR #2672)** – This open PR ([#2672](https://github.com/nanocoai/nanoclaw/pull/2672) by `apparentsoft`) addresses a regression on the `providers` branch where `McpServerConfig` evolved into a `stdio | http | sse` union. The HTTP-only transport fix is critical for users deploying behind corporate proxies.
- **Aging CLI Fix (PR #2187)** – Open since May 2, PR [#2187](https://github.com/nanocoai/nanoclaw/pull/2187) (`alex-shepel`) resolves a platform identity bug where CLI bare platform IDs are incorrectly namespaced. It received a recent update, indicating continued interest and maintainer awareness.

---

### 5. Bugs & Stability
| Severity | ID / Description | Status |
| --- | --- | --- |
| **Critical** | OS Command Injection via crafted package names in `container-runner.ts`. ([PR #2538](https://github.com/nanocoai/nanoclaw/pull/2538)) | **Fixed (Merged)** |
| **High** | Codex provider broken by MCP config union type change; HTTP transport blocked behind proxies. ([PR #2672](https://github.com/nanocoai/nanoclaw/pull/2672)) | Fix Proposed (Open) |
| **Medium** | CLI platform IDs incorrectly namespaced, causing potential message routing errors. ([PR #2187](https://github.com/nanocoai/nanoclaw/pull/2187)) | Fix Proposed (Open) |

The project shows strong security hygiene—the critical injection vulnerability was patched promptly. The primary stability risk lies in the Codex provider regression, which is actively under review.

---

### 6. Feature Requests & Roadmap Signals
- **Plugin Ecosystem Maturation** – The merge of PR [#1193](https://github.com/nanocoai/nanoclaw/pull/1193) is a clear roadmap milestone. Expect a community plugin push in the coming sprints.
- **Multi-Channel Strategy** – The Webchat v1 skill (PR [#2069](https://github.com/nanocoai/nanoclaw/pull/2069)) confirms the ongoing investment in a multi-channel agent platform.
- **Education Sector Entry** – Issue [#2673](https://github.com/nanocoai/nanoclaw/issues/2673) hints at a vertical opportunity for local, private AI processing in schools.
- **Enterprise-Grade Runtime** – Active work on MCP union types and proxy support (PR [#2672](https://github.com/nanocoai/nanoclaw/pull/2672), PR [#2674](https://github.com/nanocoai/nanoclaw/pull/2674)) indicates the Codex provider is being hardened for production and enterprise deployments.

---

### 7. User Feedback Summary
- **Pain Points:** Breaking changes on the `providers` branch and proxy configuration friction are the primary reported issues. The CLI identity bug (PR #2187) remains a persistent annoyance for power users.
- **Preferred Use Cases:** Document/sheet processing (education), live webchat agents, and secure sandboxing (container runner) dominate recent community signals.
- **Satisfaction:** The core team demonstrates strong responsiveness. The security fix (PR #2538) was handled decisively, and major feature branches (plugins, webchat) are landing consistently, which points to high contributor and user satisfaction.

---

### 8. Backlog Watch
- **PR #2187: fix(platform-id): don't namespace CLI bare platform ids**
  - **Author:** `alex-shepel`
  - **Age:** Open since 2026-05-02 (32 days)
  - **Status:** Updated 2026-06-02, awaiting final maintainer review/merge.
  - **Why it Matters:** This is the longest-standing open PR with a completed fix. It addresses a concrete identity routing bug affecting CLI users and follows the contributing guidelines.
  - **Link:** [https://github.com/nanocoai/nanoclaw/pull/2187](https://github.com/nanocoai/nanoclaw/pull/2187)

---

*Data sourced from the nanocoai/nanoclaw repository activity for the 24-hour period ending 2026-06-02.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 3, 2026, based on the latest GitHub activity.

---

## NullClaw Project Digest – 2026-06-03

### 1. Today's Overview

Project activity in the last 24 hours was highly targeted, focusing entirely on a single regressive bug and its immediate proposed fix. The maintainer and community have zeroed in on a critical false-positive in the default PII redactor, which corrupts basic system command output. No new releases, unrelated pull requests, or feature requests were introduced, indicating a tight feedback loop between the bug report (Issue #944) and the submitted patch (PR #945). Overall project health appears solid, with the community providing high-quality, actionable contributions that keep the PII feature maturing.

### 2. Releases

**No new releases were published in the last 24 hours.**

### 3. Project Progress

**No pull requests were merged or closed today.** One open pull request addresses the day's primary bug report.

- **#945 (Open):** *fix(redaction): reject ISO date/time patterns as false-positive phone matches*
  - Author(s): vernonstinebaker
  - Status: Awaiting review and merge.
  - Details: Introduces an `isDateLike()` guard to the phone number matching logic to prevent the redactor from masking timestamps.

### 4. Community Hot Topics

Activity was entirely concentrated on a single, well-defined issue.

- **Issue #944 | PR #945 – PII Redaction False Positives**
  - **Topic:** The default PII redactor aggressively masks date command output (e.g., `2026-06-02 20:17`) as phone numbers, replacing them with `[PHONE_X]` placeholders.
  - **Analysis:** The core user need here is **reliable system interoperability**. A PII redaction feature must not break the output of standard Unix utilities like `date`. The underlying assumption that digit-dash patterns are exclusively phone numbers fails against ISO timestamps. The community is signaling a strong desire for context-aware redaction logic.
  - **Links:**
    - Issue: nullclaw/nullclaw Issue #944
    - PR: nullclaw/nullclaw PR #945

### 5. Bugs & Stability

| Severity | Bug | Status | Impact | Fix Available |
|---|---|---|---|---|
| **High** | **#944:** PII redactor falsely matches date/time output as phone numbers | Open | **Functional Regression:** When `enable_pii_redaction` is `true` (default since commit `41cdb493`), an agent running `date` loses temporal context in its output. This breaks logging, timestamp formatting, and any downstream agent logic relying on standard timestamps. | **Yes (PR #945)** – Adds an ISO date/time format guard to the phone matching regex. |

- **Regression Window:** Introduced in May 2026 (commit `41cdb493`) when the feature was set to default-on.

### 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. However, the rapid creation of PR #945 signals that the project's immediate roadmap priority is **hardening the PII redaction engine.**

- **Near-term Prediction:** The next release will almost certainly include the `isDateLike()` guard from PR #945.
- **Long-term Signal:** The false-positive issue highlights a gap in the current naīve regex-based approach. Future versions (0.x or 1.x) may need to implement a **pattern exclusion whitelist** or an **LLM-evaluated redaction pass** to handle dynamic system outputs without breaking core agent functionality.

### 7. User Feedback Summary

The predominant user voice this window is **vernonstinebaker**, whose actions define the session.

- **Pain Point:** The default PII redaction is too aggressive and breaks standard tooling. Users expect opt-in functionality to be safe by default.
- **Satisfaction Indicator:** The user was able to identify the source of the regression (commit `41cdb493`), file a clear bug report, *and* immediately write a corresponding fix. This suggests a power user who holds the project in high enough regard to invest in a direct fix rather than simply switching the feature off and walking away.
- **Use Case:** The user's environment is likely an agent-heavy setup where `date` output is dynamically fed back into the context window. The breaking of this prompt logic (`appendDateTimeSection`) represents a serious workflow disruption.

### 8. Backlog Watch

The provided data snapshot covers only the last 24 hours. No long-unanswered issues or stale pull requests were visible within this window. The project maintains a healthy incident response cadence, with a critical bug report and a corresponding code fix submitted within the same day. No maintainer bottlenecks are currently observable in this timeframe.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for June 3, 2026, based strictly on the provided GitHub data.

---

## IronClaw Project Digest — 2026-06-03

### 1. Today's Overview
The IronClaw project is undergoing an extremely high-velocity development phase, dominated by the maturation of the **Reborn** architecture. With **50 updated Pull Requests** and **30 updated Issues** recorded in the last 24 hours, the core team is intensely focused on hardening the Reborn loop (safety, budgets, cancellations), landing platform integrations (Slack, MCP, OAuth), and addressing a broad QA bug bash. The project merged or closed **31 PRs** today, signaling strong feature completion velocity. On the health side, a critical user-facing blocker was reported for **Claude Opus 4.7/4.8**, and the **nightly E2E test suite** continues to fail. No new public releases were cut.

### 2. Releases
**None.** The latest public release remains **v0.28.2**.

### 3. Project Progress
The project landed **31 merged/closed PRs** today. Key advances include:
- **Reborn Safety & Subagents:** A major fix for subagent capability gating and safety context wiring landed ([#4373]), closing out audit finding C4 ([#4351]).
- **Platform Integrations:** Significant OAuth and integration work was completed, including Gmail scopes ([#4347], [#4346]), Notion DCR ([#4345]), and the Slack Reborn final-reply delivery ([#4321]).
- **Reborn Features:** The trigger system moved forward with the closure of PR17 (first-party capabilities, [#4318]). The GitHub WASM capability path for Reborn ([#3806]) was finally closed out as completed.
- **Tooling & DX:** The `builtin.memory_search` tool was hardened to accept common query aliases ([#4374]), and the local development Reborn memory mount was fixed ([#4357]).
- **Engine & History:** The engine v2 newtype client IDs feature ([#4355]) was finalized, closing a follow-up from the larger correlation PR.

### 4. Community Hot Topics
- **Claude Opus 4.7/4.8 Blockade ([#4334]):** The most impactful single issue for users of premium models. IronClaw unconditionally sends the `temperature` parameter, which these models reject with a `400` error. The issue has no fix PR attached yet, representing a critical gap for Anthropic users.
- **QA Bug Bash (P2 Cluster, [#4338-#4344]):** A coordinated testing wave by `joe-rlo` against **Qwen3.6-35B** and **MiniMax-M2.7** generated a cluster of high-visibility P2 bugs. The exposure of the internal **chain-of-thought** to the user ([#4341]) has significant privacy implications. The **message mirroring** issue ([#4344]) where the UI echoes user text as an agent response is a critical UX failure.
- **Engine v2 Correlation API ([#3669]):** This long-running XL-sized PR to expose channel-supplied thread/response IDs remains open and closely watched by developers building downstream tooling.

### 5. Bugs & Stability
*Ranked by estimated severity:*

- **Critical (User-Facing):**
  - **Claude Opus 4.7/4.8 Unusable ([#4334]):** A 400 error blocks all requests. No fix PR detected.
  - **Broken Model Switching ([#4377]):** The `/model` command returns unparseable display names (e.g., "GPT OSS 120B") for the NEAR AI provider, making it impossible to switch models.
  - **Persistent CI Failure ([#4108]):** The nightly E2E test pipeline has been failing since May 27 and was updated again today without resolution.

- **High (QA Bash P2):**
  - **Thinking State Exposure ([#4341]):** The agent's internal reasoning is leaked to the user.
  - **Message Mirroring ([#4344]):** The chat UI displays the user's message as the agent's own response.
  - **Auth Modal Persistence ([#4342]):** The authentication modal blocks chat even after a hard page refresh.
  - **MCP Driver Failure ([#4343]):** Extension integrations acknowledge capability but fail silently to execute.

- **Structural (Reborn Architecture):**
  - A deep audit of the Reborn system was filed by `henrypark133`, detailing systemic holes in capability validation (`$ref` bypass, [#4360]), prompt safety wiring ([#4359]), budget accuracy (wall-clock not enforced, [#4364]), and subagent durability ([#4348]). Fix PRs such as [#4373] (for safety gating) are already in review.

### 6. Feature Requests & Roadmap Signals
The data strongly indicates the roadmap is fully saturated with the **Reborn architecture rollout** and **first-class tool integrations**.

- **Scheduled/Event-Driven Agents (Triggers):** The merging of PR17 ([#4318]) and the immediate wiring of the trigger poller lifecycle in PR18 ([#4375]) signals that scheduled agent execution is a top priority for the next milestone.
- **Platform as a Hub:** The aggressive push for hosted MCP negotiation and OAuth credential reuse ([#4354]) across Notion, GSuite, and GitHub suggests a strategic move to make IronClaw an interoperability hub for external tool ecosystems.
- **Required Fix (Prediction):** The Claude Opus 4.7/4.8 failure ([#4334]) will likely force a higher priority on flexible provider parameter handling in the LLM gateway, specifically the ability to omit default parameters when models deprecate them.
- **Enterprise Governance:** The long-standing `DISABLE_TOOLS_LIST` flag ([#3548]), while stuck in review, remains a strong roadmap signal for administrative tool control.

### 7. User Feedback Summary
- **Satisfaction Signals:**
  - The high volume of merges (31 PRs) implies a responsive development cycle.
  - Users of Slack, Gmail, and Notion integrations should see immediate quality-of-life improvements from the OAuth and delivery fixes landed today.

- **Pain Points & Dissatisfaction:**
  - **Model Lockout:** Users of Claude 4.7/4.8 are effectively locked out, representing a high churn risk for that demographic.
  - **Configuration Friction:** The `/model` display name bug [#4377] directly prevents users from switching models, a core workflow.
  - **UI Brittleness:** The QA bash results describe a chat UI that breaks under non-standard model output, exposing users to raw thinking tokens or mirrored messages.

### 8. Backlog Watch
- **Persistent CI Failure ([#4108]):** Updated today after failing since May 27. This is a significant red flag for release readiness and requires immediate maintainer attention.
- **Security/Compliance Feature ([#3548]):** The `DISABLE_TOOLS_LIST` PR (opened May 12) remains unmerged. It is an XL-sized change that is critical for enterprise/strict administrators.
- **Engine v2 Correlation ([#3669]):** Despite the closure of its follow-up issue ([#4355]), this core PR remains open after three weeks. Its lengthy gestation suggests a high-risk merge requiring careful sequencing.
- **Model Parameter Fixes ([#4334]):** With no fix PR attached yet, this critical bug is a fast-track candidate for the backlog. Its current orphan status directly impacts user retention.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured **LobsterAI Project Digest** for **2026-06-03**, based strictly on the provided GitHub activity data.

---

### 1. Today’s Overview

In the 24-hour period leading up to June 3rd, the LobsterAI project demonstrated a strong focus on stabilization and feature integration, with **6 out of 9 updated PRs being merged or closed** and zero new issues opened. The absence of new user-submitted issues and releases suggests the team is in a rigorous internal polish phase following the integration of a major artifacts feature. Activity was concentrated across four key areas: **Artifacts**, **MCP tooling**, **Cowork subagent management**, and **MiniMax model support**. Project health appears stable, with the core developer team driving a high velocity of critical fixes and performance improvements.

---

### 2. Releases
**None.** No new releases were created in this period.

---

### 3. Project Progress
**6 PRs merged/closed today**, spanning new features and targeted bug fixes:

- **Feat: Artifacts System** (PR [#2092](netease-youdao/LobsterAI PR #2092)): The headline `2026.5.28 artifacts` feature was fully merged, marking the largest functional addition to the codebase in this cycle.
- **Feat: MCP Launch Optimization** (PR [#2091](netease-youdao/LobsterAI PR #2091)): Added resolution caching for npx-based MCP servers, converting slow `npx -y` paths into direct `node` executions, plus new timing diagnostics.
- **Fix: MiniMax-M3 Image Support** (PR [#2093](netease-youdao/LobsterAI PR #2093)): Hardcoded image support was corrected for the M3 model, enabling the previously broken image upload feature for this provider.
- **Fix: Cowork Subagent Management** (PR [#2095](netease-youdao/LobsterAI PR #2095)): Batch selection and deletion were added to the sidebar for subagent sessions, alongside async cleanup improvements for the gateway transcript.
- **Fix: Plugin Management Cleanup** (PR [#2096](netease-youdao/LobsterAI PR #2096)): Internal OpenClaw runtime plugins are now filtered from the plugin management UI.
- **Fix: Share Popup UX Polish** (PR [#2094](netease-youdao/LobsterAI PR #2094)): Visual hierarchy and redundancy in the share success popup were optimized.

---

### 4. Community Hot Topics

While the dataset records **zero direct comments or reactions** on the updated items, the development activity itself signals the hottest areas of the project:

1.  **Artifacts Feature** (PR [#2092](netease-youdao/LobsterAI PR #2092)): The merge of this feature is the single strongest signal of the current roadmap direction. It introduces a persistent, rendered output format similar to Claude Artifacts.
2.  **MCP Toolchain Reliability** (PR [#2091](netease-youdao/LobsterAI PR #2091)): The intense focus on reducing launch latency for MCP servers indicates that developer experience and tool integrations are currently a top priority.
3.  **Model Compatibility** (PR [#2093](netease-youdao/LobsterAI PR #2093)): The rapid patch for MiniMax-M3 image support reflects a deep need to keep pace with rapidly evolving upstream model capabilities.

*Analysis: The community is likely heavily focused on using Lobster as an agentic platform (MCP + Subagents) and consuming multimodal models, rather than debating specific issues.*

---

### 5. Bugs & Stability

No new crashes or regressions were filed as issues. However, **4 bugs were fixed via direct PRs**, ranked by severity:

| Severity | Bug Description | Fix PR |
|---|---|---|
| **High** | **MiniMax-M3 image input hardcoded to false** (carried over from M2.5/M2.7 which do not support images). This completely blocked a key modal feature for users on the new model. | [#2093](netease-youdao/LobsterAI PR #2093) |
| **Medium** | **Slow MCP startup** – every session launch using `npx -y` packages was forced to resolve and download from scratch, causing significant latency. | [#2091](netease-youdao/LobsterAI PR #2091) |
| **Medium** | **Missing Subagent batch operations** – users could not select and delete multiple subagent sessions from the sidebar. | [#2095](netease-youdao/LobsterAI PR #2095) |
| **Low** | **Internal plugins exposed in UI** – OpenClaw runtime plugins were visible to users in the plugin management screen. | [#2096](netease-youdao/LobsterAI PR #2096) |

**Verdict:** The project handled stability well by proactively patching these issues before they accumulated into formal bug reports.

---

### 6. Feature Requests & Roadmap Signals

*Strong Signals (Merged):*
- **Artifacts (PR #2092):** This is the definitive roadmap item. It heavily implies the next version will focus on rich, persistent, client-rendered UI elements (charts, documents, code).
- **Cowork System Maturation (PR #2095):** Batch subagent management suggests the "multi-agent cowork" feature is moving from basic functionality to power-user scale.

*Pending Signals (Open PRs):*
- **MiniMax Model Upgrade (PR #388):** While image support was fixed, the actual *default* model still needs to be swapped to M3. This is a necessary companion PR to #2093.
- **IM Instance Duplicate Validation (PR #1464):** This has been pending since early April. It indicates users managing multiple IM bots (Feishu, DingTalk, QQ) are hitting data integrity issues.

*Prediction for Next Release (v2026.6.x):*
The next minor version will almost certainly feature **Artifacts** as the headline, combined with a **performance pass on MCP tools** (enabled by #2091) and full **MiniMax M3 default status**.

---

### 7. User Feedback Summary

**Data Limitation:** The dataset shows **zero user-authored issues** and **zero reactions/comments** on the updated items for this period, making explicit sentiment analysis impossible.

**Implicit Pain Points (Inferred from Fixes):**
- **Frustration:** Users likely experienced friction when trying to use images with the newly integrated MiniMax M3 model, only to find the feature silently disabled.
- **Friction:** Power users relying on custom MCP tools likely experienced significant wait times on every session start.
- **Satisfaction:** The rapid turnaround on merging these fixes (all within 24 hours) suggests highly responsive engineering, which generally correlates with positive developer sentiment despite the quiet community engagement.

---

### 8. Backlog Watch

Three open PRs require maintainer attention, all of which have been updated recently but remain unmerged:

- **PR [#388](netease-youdao/LobsterAI PR #388)**: **[Upgrade MiniMax default model to M3]** – *Stale (Opened March 12)*. This PR explicitly aims to make MiniMax-M3 the default. After the fix in #2093, the scope of this PR is narrowed to just the priority/ordering logic. It needs a decision: merge or close as partially superseded.
- **PR [#1277](netease-youdao/LobsterAI PR #1277)**: **[chore(deps): Bump electron group]** – *Dependabot PR (Opened April 2)*. This upgrades Electron from **40.2.1 to 42.3.1**. This is a significant major version jump containing critical security patches and performance improvements. It should be prioritized to avoid accumulating tech debt.
- **PR [#1464](netease-youdao/LobsterAI PR #1464)**: **[fix(im): Add duplicate validation for instance name/credential]** – *Stale (Opened April 4)*. A crucial UX fix for the multi-instance IM feature. It prevents data corruption scenarios (duplicate names, duplicate bots). This has been waiting for review for over two months.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest — June 3, 2026**

**1. Today's Overview**
Moltis experienced a quiet but focused day on June 3, with no new releases and no PRs merged. Activity was limited to one new feature request and one ongoing pull request update, both authored by `s-salamatov`. The project appears to be in a deliberate refinement phase, prioritizing memory management stability and presentation layer customization. Overall project health remains stable, with development concentrated on foundational robustness rather than expanding the feature surface.

**2. Releases**
No new versions of Moltis were published today. The current feature set remains unchanged, and the next release is likely to bundle the ongoing session history improvements (PR #1089) with the UX configuration being requested by the community (Issue #1092).

**3. Project Progress**
*No PRs were merged or closed today.*

- **Active Work:** **PR #1089 (Cap persisted tool results before rehydration)** — `s-salamatov` continues to drive this critical backend improvement. The PR applies a size cap on `tool` and `tool_result` content when session history is rehydrated into provider-bound `ChatMessage`s. It integrates across all chat modes: normal, streaming, retry-after-compaction, prompt inspection, silent memory turns, and LLM-backed compaction prompts. The database records are left intact, ensuring only the prompt context is slimmed down. *[GitHub: moltis-org/moltis PR #1089]*

**4. Community Hot Topics**
- **Issue #1092 ([OPEN] Add config option to disable Activity log tool-status messages)** — The most notable community signal today. Users are requesting control over the "Activity log" block that appears after tool usage, particularly in Telegram where it either creates a collapsible HTML block inside the main message or a distracting separate follow-up message. The underlying need is **presentation sovereignty**: users want the reliability of tool-driven agents without exposing technical execution traces in public-facing channels. *[GitHub: moltis-org/moltis Issue #1092]*

- **PR #1089 (Cap persisted tool results)** — While technical, this PR receives implicit community interest because it underpins the stability of tool-heavy workflows and sets the stage for future UI / UX changes.

**5. Bugs & Stability**
No new bugs, crashes, or regressions were reported in the last 24 hours.

- **Proactive Stability Work:** The only stability signal comes from **PR #1089**, which proactively caps tool result data during rehydration. This prevents unbounded memory growth in provider context windows, eliminating a class of silent failures and hard-to-debug context overflow errors that can corrupt long-running sessions or compaction cycles.

**6. Feature Requests & Roadmap Signals**
- **UX Customization (Issue #1092):** The request to disable the tool-status Activity log is the clearest roadmap signal. It indicates a move toward "quiet mode" tool use, where the agent's reasoning is hidden from the end user by default. A future minor release (e.g., v0.5.x) could introduce a `show_tool_activity` config flag as a companion to the memory-capping infrastructure in PR #1089.
- **Session Robustness (PR #1089):** The rigorous capping logic applied across all chat modes signals a commitment to production-grade session management, which is a prerequisite for enterprises deploying long-running agents.

**7. User Feedback Summary**
- **Pain Point:** The compulsory display of tool-status blocks breaks conversational flow in channel environments.
- **Use Case:** Telegram deployment is a major driver; users want the precision of edit-in-place streaming without a follow-up Activity block.
- **Satisfaction Level:** The community is engaged enough to submit specific configuration requests rather than filing defect reports. This suggests high baseline satisfaction with the core agent intelligence, with frustration concentrated on the presentation layer.

**8. Backlog Watch**
No long-dormant issues were flagged in today's data. The primary item requiring continued attention is **PR #1089 (`moltis-org/moltis PR #1089`)** . It represents a high-impact refactor touching nearly every code path in the chat pipeline. While actively maintained by `s-salamatov`, its merge schedule warrants monitoring, as it will unblock further UX work (including the config toggle requested in Issue #1092).

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-03

## 1. Today's Overview

Today marks a significant day of security hardening and critical bug fixing for CoPaw. Activity was very high, with **36 issues** updated (16 open/active, 20 closed) and **31 PRs** updated (21 open, 10 merged/closed). The most notable event was a coordinated wave of 7 security disclosures from researcher @YLChen-007 (issues #4908–#4914), all of which were rapidly triaged and closed, demonstrating the project's strong security response posture. Concurrently, the community flagged major concerns in channel integrations (WeChat, Yuanbao) and Windows stability. The merging of the `v1.1.11b1` version bump PR (#4907) signals a new beta is imminent. First-time contributor activity remains strong, with several PRs in the pipeline.

## 2. Releases

**No new stable releases were published today.** The `chore(release): bump version to v1.1.11b1` PR (#4907) was merged, indicating a new beta release is currently being prepared or rolled out. Users on the stable channel remain on **v1.1.10**.

## 3. Project Progress

Today's merged/closed work focused on stabilizing core integrations and improving the Windows experience:

- **Channel Fixes:**
  - WeChat cron message delivery fixed (#4878 / #4883)
  - WeCom session isolation vulnerability patched (#4845 / #4850)
- **Windows Improvements:**
  - Multi-drive browsing support in coding mode (#4906)
  - Major Windows startup performance optimization: lazy loading, caching, progressive initialization (#4772)
- **Provider Compatibility:**
  - Non-standard `generate_kwargs` (e.g., DashScope's `enable_search`) now properly routed to `extra_body` instead of being silently dropped (#4689)
- **Security Hardening:**
  - All 7 vulnerabilities from the YLChen-007 report were closed with accompanying fixes (see Bugs section)
- **Infrastructure:**
  - Cloudflared download now shows real-time progress notifications in the console (#1317)

**Key Open PRs Under Review:**
- Agentscope 1.x → 2.0 migration (#4846) — major breaking change
- Plugin-based custom channels replacing legacy directory system (#4693)
- Prompt Section Registry for plugin system (#4804)
- Self-evolving skill creation flow (#4857)
- Xiaomi MiMo Token Plan built-in provider (#4722)

## 4. Community Hot Topics

The most active discussions and issues reflect three clear themes:

**1. Security Audit & Disclosure (@YLChen-007)**
A single researcher filed a comprehensive sweep of vulnerabilities in a single day. All 7 issues (#4908–#4914) were closed promptly, which is a strong positive signal for the project's security maturity. Issues covered:
- Unauthenticated settings modification
- ToolGuard bypass
- Session ID tampering
- Path traversal / local file exfiltration
- Workspace secret leakage in exports
- MCP configuration error handling
- Cron timezone validation

**2. Windows User Activism (@rescodexx)**
A power Windows user submitted three targeted feature requests and a major bug today:
- File upload limits should not apply on Windows (#4893)
- Drag-and-drop multi-file support needed (#4894)
- Subagent tasks not viewable during execution (#4923)
Keyboard arrow key behavior fix also merged (#4920)

**3. Channel Fragmentation Headaches**
Three separate issues report _different_ channel integrations breaking simultaneously:
- WeChat cron delivery silent failure (#4878)
- Yuanbao missing proto files (#4890, #4898)
While #4878 and #4898 were closed, the pattern of channel fragility worries users.

## 5. Bugs & Stability

*Issues separate from the security vulnerabilities which were already closed.*

**🔴 Critical (No Fix Yet)**
- **Agent Perma-Crash (#4922):** A single `PermissionError` accessing a local file path causes the agent to enter a permanent failure state—*every* subsequent query fails. This is a major resilience gap with no fix PR yet.
- **Context Compression Failure (#4924):** Automatic compaction is throwing `'str' object has no attribute 'get'`, leaving long conversations unmanaged and at risk of overflowing context limits.
- **System Fallback Regression (#4837):** v1.1.9 introduced a bug where normal agent replies are silently cancelled and replaced with a generic "unable to process" fallback. Frequency is elevated.

**🟡 High Severity**
- **browser_use Broken on Windows (#4919):** Managed CDP start fails completely on Windows 10 with Chrome/Edge.
- **MCP Dot Name Blocked (#4918):** Tools like `pat.batch_plan` fail with gpt-5.5 because `.` is not in the allowed validator regex. Framework raw-passes names without sanitization.

**🔵 Medium/Low Severity**
- Custom channel settings save kills listener without restarting (#4877)
- Chat switching UI shows spurious loading states (#4903)
- Large history causes multi-second UI lag on Windows (#4917)
- Images loaded as raw Base64 into context, wasting tokens (#4921)
- DeepSeek `reasoning_content` multi-turn crash — root caused and closed (#3985)

## 6. Feature Requests & Roadmap Signals

Several trends point to where the project is heading:

| Signal | Relevance | Likely Target |
|---|---|---|
| **On-demand tool loading** (#4836) cuts initial context by 55–65%. Highly requested. | High impact, moderate complexity | Next stable release |
| **Multi-model subagents** (#4901) let simple tasks use cheap models. Modern orchestration pattern. | Power-user feature | v1.2+ |
| **DAG-based lossless compression** (#4551) | Fundamental architecture change | Long-term roadmap |
| **Plugin system expansion** (Prompt Registry #4804, Custom Channels #4693, Uninstall hooks #4794) | Ecosystem enabler | Current beta |
| **Agentscope 2.0 migration** (#4846) | Breaking change, major refactor | Beta |

## 7. User Feedback Summary

**Satisfaction Drivers:**
- Rapid security response (all 7 vulns closed same-day)
- Welcoming community for first-time contributors (5+ first-time PRs active)
- Cross-platform ambition (Windows, Web, Desktop Tauri)

**Dissatisfaction / Pain Points:**
1. **Channel reliability is the #1 trust eroder.** WeChat, WeCom, and Yuanbao all broke in different ways this week. Automation users on these platforms are frustrated.
2. **Agent resilience is too low.** One bad file path (#4922) or one compaction failure (#4924) kills the entire session — there is no graceful degradation.
3. **Windows is treated as a secondary citizen.** Multiple bugs unique to Windows: browser automation broken, file upload restrictions, UI lag, drive navigation issues.
4. **UI complexity overshadows daily use.** Users report the sidebar and menu system is "too complicated" and that frequent actions require too many clicks (#4904).

## 8. Backlog Watch

Several items require maintainer attention:

**Stale First-Contributor PRs (No Review Activity):**
- [#760](agentscope-ai/QwenPaw PR #760) — Context length detection with auto-/compact suggestion (Opened Mar 5)
- [#1086](agentscope-ai/QwenPaw PR #1086) — Handle missing media files during memory compaction (Opened Mar 9)
- [#2275](agentscope-ai/QwenPaw PR #2275) — E2B/AgentScope sandbox backend integration (Opened Mar 25)

**Unresolved High-Impact Bugs Awaiting Fix:**
- v1.1.9 System Fallback regression (#4837) — actively degrading user experience
- Agent Perma-Crash on file error (#4922) — critical reliability issue with no assignee
- Context Compression TypeError (#4924) — core feature broken for some users

**Roadmap Decisions Overdue:**
- DAG-based compression (#4551) needs a maintainer comment on feasibility and timeline
- On-demand tool loading (#4836) has high community alignment but no roadmap commitment

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for 2026-06-03 based on the provided GitHub activity data.

---

## 1. Today's Overview

ZeroClaw is in a full stabilization sprint following the landmark **v0.8.0-beta-2** release, which introduced the new `zerocode` terminal UI and the multi-agent runtime. Activity is at a peak: the team closed 33 issues and merged 47 pull requests in the last 24 hours alone. While the community is actively testing the new features, the past day has been dominated by fixing high-severity regressions in provider integrations, hardening security boundaries, and resolving skill ecosystem friction. The project is demonstrating extremely rapid triage, with most critical (P1/S1) bugs being resolved within the same cycle they are reported.

## 2. Releases

- **v0.8.0-beta-2** (New)
  - **Headline**: **zerocode** — a full-featured Ratatui-based terminal UI for operating agents without leaving the terminal.
  - **Included**: Multi-agent runtime.

- **Breaking Changes & Migration Notes:**
  - **Stricter Skill Manifest Parsing**: `SkillMeta` now uses `#[serde(deny_unknown_fields)]` ([#6128](https://github.com/zeroclaw-labs/zeroclaw/issues/6128)). Typos in the `[skill]` block of `SKILL.toml` will now produce hard parse errors instead of dropping silently.
  - **Skill Audit Scope Change**: The audit now restricts itself to structural and filesystem checks. Command-content safety enforcement has been moved *exclusively* to runtime shell policy (`is_command_allowed` in `zeroclaw-config/src/policy.rs`) ([#5956](https://github.com/zeroclaw-labs/zeroclaw/issues/5956)).
  - **Config Aliases**: `allowed_path` and `allowed_paths` are now valid serde aliases for `allowed_roots` in `AutonomyConfig` ([PR #6086](https://github.com/zeroclaw-labs/zeroclaw/pull/6086)).
  - **Crate Reorganization**: The TUI crate moved from `crates/zeroclaw-tui` to `apps/zerocode` to match project conventions ([#6821](https://github.com/zeroclaw-labs/zeroclaw/issues/6821)).
  - **Versioned Docs**: Documentation deployment now supports version-specific pages with a shared global chrome ([PR #7023](https://github.com/zeroclaw-labs/zeroclaw/pull/7023), with a follow-up fix in [#7124](https://github.com/zeroclaw-labs/zeroclaw/pull/7124)).

## 3. Project Progress

The last 24 hours show the team heavily refining the v0.8.0-beta-2 release surface.

- **Core Runtime & Context Management:** The context compressor was fixed to prevent dropping `reasoning_content` from DeepSeek messages ([#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)). Cron agent runs were hardened to handle raw tool-only outputs and now properly report degraded delivery failures ([PR #6026]).
- **Skills Ecosystem:** The `ReadSkillTool` fix merged, ensuring skills blocked by `allow_scripts = true` actually run ([PR #5981], closing [#5697]). Timeout values from `SKILL.toml` are now correctly deserialized and enforced ([PR #6054]). The SkillForge auto-integrator was cleaned up to stop emitting non-schema fields ([#6210]).
- **Providers & Channels:** The WhatsApp Web channel was restored after an upstream April 2026 protocol bump ([#6246]). Llama.cpp tool schema sanitization for Gemma 4 landed ([PR #5254]). On the observability side, OTel tool spans were enriched with semantic convention attributes ([PR #6009]).
- **Security & Access:** A critical patch closed the web dashboard WebSocket path that was bypassing the `ApprovalManager` for supervised tools ([#6207]). Bubblewrap sandbox was fixed for Fedora 43 to include required `/lib64` bindings ([#6878]).
- **Configuration & Documentation:** Versioned documentation deployment landed ([#7023]). A sandbox and Python skills quickstart guide was added to help users configure safe skill execution ([PR #6057]).

## 4. Community Hot Topics

The most active discussions reveal where the release is putting the most stress on the user experience:

1.  **[#6123 (18 comments, Closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)** – **Fresh Install `default_model` Bug**: This was the top engagement item. Users on fresh installs (LXC, remote Ollama) hit a workflow-blocking config error. The issue was closed quickly, demonstrating the team's responsiveness to onboarding friction.
2.  **[#5962 (6 comments, Open)](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)** – **Ollama Provider Fails with Tools**: This remains the largest open pain point for the self-hosted community. Users relying on local Ollama instances find the agent completely blocked when tools are invoked. The issue has persisted for over six weeks.
3.  **[#6246 (6 comments, Closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)** – **WhatsApp Web Protocol Bump**: A server-side change by WhatsApp Web silently broke the channel. The community engaged heavily here, showing high dependency on this channel and frustration with the silent failure mode.
4.  **[#5722 (6 comments, Closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/5722)** – **Sandbox Blocks Python Skills**: Jason Perlow (InvestorClaw) documented how the default `alpine:latest` sandbox blocks all realistic Python/Julia/R patterns. The community resolution (documentation of config overrides) satisfied the immediate need but highlighted a persistent "security vs. usability" tension.
5.  **[#6127 (4 comments, Open)](https://github.com/zeroclaw-labs/zeroclaw/issues/6127)** – **Gateway Silent-Fallback Hardening**: This security-sensitive P1 has the community's attention as the gateway counterpart to a runtime credential fix, with users pushing for complete elimination of silent failure modes in authentication.

## 5. Bugs & Stability

The project focused intensely on stability today, closing the vast majority of critical bugs.

- **Critical (S1 – Workflow Blocked):**
  - *Closed:* Fresh install `default_model` ([#6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)), WhatsApp Web broken ([#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)), Web Dashboard bypassing ApprovalManager ([#6207](https://github.com/zeroclaw-labs/zeroclaw/issues/6207)), ACP `cwd` lockout ([#6516](https://github.com/zeroclaw-labs/zeroclaw/issues/6516)), and skills install panic ([#6681](https://github.com/zeroclaw-labs/zeroclaw/issues/6681)).
  - *Open:* **Ollama provider tool call failure ([#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962))** – This is the most critical remaining open S1 for local-LLM users.
- **High (P1 – Degraded Experience):**
  - *Closed:* Bubblewrap on Fedora 43 ([#6878](https://github.com/zeroclaw-labs/zeroclaw/issues/6878)), DeepSeek reasoning content loss ([#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)), skills blocked by `allow_scripts` ([#5697](https://github.com/zeroclaw-labs/zeroclaw/issues/5697)), and Z.AI provider 1214 errors ([#5636](https://github.com/zeroclaw-labs/zeroclaw/issues/5636)).
  - *Open:* **Delegate agents ignore injection mode ([#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155))** – A long-running P1 with no merged fix yet, undermining the whole skills privacy model.

## 6. Feature Requests & Roadmap Signals

- **`.well-known` URI for Skills ([#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853))**: This feature is waiting on the external Agentskills group standardization. Given production usage by Cloudflare and Vercel, adoption by ZeroClaw is a likely **v0.9.0** milestone.
- **ACP Protocol Extensions ([#6820](https://github.com/zeroclaw-labs/zeroclaw/issues/6820))**: Diff display and file-proposal types are being built to fully support the `zerocode` TUI chat experience. This is already partially shipped and will complete in the coming patch releases.
- **Observability Investment**: The merging of OTel tool span enrichment ([PR #6009](https://github.com/zeroclaw-labs/zeroclaw/pull/6009)) and streaming payload tracing tests ([#6742](https://github.com/zeroclaw-labs/zeroclaw/issues/6742)) signals a roadmap commitment to production-grade monitoring.
- **Prediction for v0.8.0 Stable**: The team is methodically closing P1 bugs. The likely final blockers for a stable v0.8.0 release are the gateway silent-fallback hardening ([#6127](https://github.com/zeroclaw-labs/zeroclaw/issues/6127)) and the Ollama provider tool regression ([#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)).

## 7. User Feedback Summary

- **Satisfaction**: Users are highly engaged with the rapid release cadence and quick turnaround on P1 bugs (e.g., WhatsApp channel restored within the same day). The `zerocode` TUI is generating positive sentiment as a practical replacement for the web dashboard in headless environments.
- **Pain Points**:
  - **Provider Configuration Friction**: Setting up local providers (Ollama, Z.AI) is a recurring source of workflow-blocking bugs. Users desire more robust integration testing against the long tail of local LLM backends.
  - **Security vs. Usability**: The default sandbox is too restrictive for data science/scripting workflows. While documentation alleviates this, users are calling for smarter defaults that auto-detect skill language requirements.
  - **Onboarding Flow**: The recent influx of P1 onboarding bugs ([#6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123), [#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120)) suggests the new first-run experience is not yet robust across all environments (LXC, remote providers).
  - **Channel Stability**: The WhatsApp Web silent failure highlights a need for upstream protocol version monitoring or pinning.

## 8. Backlog Watch

Several high-priority items remain open for extended periods and require maintainer attention:

1.  **[#5155 (Delegate agents ignore prompt_injection_mode)](https://github.com/zeroclaw-labs/zeroclaw/issues/5155)** –  **Opened: 2026-03-29 | P1 | Accepted / In Progress**
    A critical privacy bug that has been open for over two months. The delegate agent path hardcodes `SkillsPromptInjectionMode::Full`, completely bypassing the user's `[skills]` config. This is the single oldest unresolved P1 issue.
2.  **[#6127 (Gateway silent-fallback hardening)](https://github.com/zeroclaw-labs/zeroclaw/issues/6127)** – **Opened: 2026-04-26 | P1 | Accepted**
    A security-sensitive follow-up to the runtime credential fix. The gateway side still has silent failure paths for credential resolution. Marked as a merge condition, this looks like a definitive blocker for the v0.8.0 stable release.
3.  **[#4853 (.well-known URI for skills)](https://github.com/zeroclaw-labs/zeroclaw/issues/4853)** – **Opened: 2026-03-27 | P2 | Accepted**
    Blocked on an external standard, but has been idle for over two months. A maintainer status update or interim RFC would help reassure the community that this highly requested feature is still on the roadmap.
4.  **[#6120 (Onboarding: Codex prompts for API key)](https://github.com/zeroclaw-labs/zeroclaw/issues/6120)** – **Opened: 2026-04-26 | P1 | Accepted**
    A UX bug misdirecting new users during the very first interaction with the product. Despite being P1, it remains unassigned and unresolved, which is a blocker for a polished v0.8.0 stable experience.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*