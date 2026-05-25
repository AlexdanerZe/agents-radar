# OpenClaw Ecosystem Digest 2026-05-25

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-25 09:58 UTC

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

# OpenClaw Project Digest — 2026-05-25

## 1. Today's Overview

OpenClaw is operating at an exceptionally high velocity, with **500 Issues and 500 Pull Requests updated** in the last 24 hours and **two new beta releases** pushed. The project is simultaneously executing a major internal architectural refactor (decoupling from the legacy "Pi" runtime) while actively patching critical stability, security, and concurrency bugs. Community engagement remains intense, with high-profile feature requests for cross-platform clients and enterprise integrations continuing to dominate discussion. Overall project health is strong in iteration speed and community investment, but reliability in core message delivery and session management remains a pressing concern requiring stabilization.

---

## 2. Releases

Two new beta versions were published on May 24, 2026. No breaking changes or migration steps were reported in either release.

### v2026.5.24-beta.2
- **iMessage Approval Reactions:** Added native support for `👍` (Like tapback) to resolve an approval as `allow-once` and `👎` (Dislike tapback) as `deny`. The explicit-approver allowlist is read from `channels.imessage.allowFrom`. Persistent `allow-always` remains a manual `/approve <id> allow-always` text command fallback.
- **Impact:** Novel UX for approval flows, reducing friction for mobile/iMessage users.

### v2026.5.24-beta.1
- **Gateway/Performance:** Reuses process-stable channel catalog reads, avoids repeated bundled-channel boundary checks, and rotates gateway watch CPU profiles so benchmark runs do not accumulate unbounded artifacts.
- **Impact:** Reduces startup and runtime overhead for gateway operations, improves long-running benchmark hygiene.

---

## 3. Project Progress

In the last 24 hours, **185 PRs were merged/closed** and **203 Issues were resolved**, reflecting sustained output.

### Security Hardening (Merged/Closed)
- **[P0 Security] Hook ingress token bypass fixed (#84338):** A critical vulnerability where a hook ingress bearer token could authenticate directly to password-mode Gateway HTTP surfaces was patched and auto-merged. Review rating: `rating: 🧂 unranked krab, status: 🚀 automerge armed`.
- **[P0 Security] Cross-user privacy leak resolved (#85240):** The `relevant-memories` recall mechanism lacked `sender_id` isolation, allowing private memories from one user to leak into another's context. This was identified as a P0 security issue and closed.

### Reliability Fixes (Merged/Closed)
- **Session lock races addressed (#86427):** A targeted fix ensures the embedded agent session write-lock is released on every exit path (timeout, tool error), resolving the `EmbeddedAttemptSessionTakeoverError` failures reported across multiple channels.
- **Telegram/Codex preflight recovery (#86216):** Stale native harness thread bindings in the Codex preflight compaction path now recover gracefully instead of aborting inbound dispatch.
- **Cron job payload preservation (#86415):** Unsupported `payload.kind` values (e.g., `command`, `agentmessage`) are now preserved on writes instead of being silently deleted.
- **Doctor tool crash fixed (#86384):** `openclaw doctor` now warns and continues when the cron job store is unreadable (e.g., `root:root 0600` in Docker contexts) instead of aborting mid-run.
- **macOS LaunchAgent durable update (#85120):** In-band `openclaw update` no longer stops the supervising gateway on macOS. Closed.

### Architecture & Developer Experience
- **Pi runtime internalization (#85341):** The massive refactoring PR (size XL, `status: 📣 needs proof`) advanced, removing Pi as an embedded dependency and moving agent execution, model provider routing, and SDK surfaces under OpenClaw ownership. This is a foundational change for the project's maintainability and flexibility.
- **Review policy clarified (#86288, #86185):** AGENTS.md was updated to treat new/ changed config surfaces as review metrics and merge-risk material, and OpenClaw-specific ClawSweeper policy was moved into the root AGENTS.md.

---

## 4. Community Hot Topics

The community's most engaged discussions reveal a clear trajectory toward broader platform support, deeper security, and more predictable automation.

### Cross-Platform Desktop Apps [`#75`](openclaw/openclaw Issue #75)
- **106 comments, 77 👍**
- **Underlying need:** Users require native Linux and Windows Clawdbot clients. The macOS, iOS, and Android apps exist but leave a major gap for the majority of desktop users. This is the single most active feature request and represents a key barrier to wider enterprise adoption.

### Configurable Streaming Watchdog [`#68596`](openclaw/openclaw Issue #68596)
- **13 comments, 8 👍**
- **Underlying need:** Users running extended-reasoning models (DeepSeek-R1, Kimi K2.5) are hit by false-positive watchdog resets after 30s of no stream updates. This reflects a growing use case for deep research/agentic tasks that require longer inference windows. The need is not just for a timeout configuration but for *trust* that long-running work will not be silently aborted.

### Direct Exec Mode for Cron Jobs [`#18160`](openclaw/openclaw Issue #18160)
- **12 comments, 9 👍**
- **Underlying need:** Power users find the `agentTurn` cron execution model unreliable and too slow for simple automation. They want a mode where cron tasks run without LLM interpretation overhead. This signals a split in the user base between those who want "smart" AI agents and those who need reliable, low-latency automation.

### Masked Secrets / Credential Protection [`#10659`](openclaw/openclaw Issue #10659)
- **13 comments, 4 👍**
- **Underlying need:** Deep anxiety about prompt injection and accidental credential leaks. Users want agents to *use* API keys without being able to *read* them. This is a foundational enterprise security requirement.

### Xiaomi MiMo Token Plan Support [`#86169`](openclaw/openclaw Issue #86169)
- **6 comments, 1 👍**
- **Underlying need:** First-class support for regional/non-standard inference providers is a clear signal of global adoption. Users want to leverage local token plans without hacky workarounds.

---

## 5. Bugs & Stability

Stability is the highest-risk area for the project right now. Several P1 and P0 bugs reported this week directly impact user trust in core features.

### P0 — Severity: Critical
- **[Cross-User Privacy Leak](openclaw/openclaw Issue #85240):** Semantic recall without `sender_id` isolation. Private memories from one user can be injected into another's context. **Status:** CLOSED. Fix confirmed.

### P1 — Severity: High
- **[Telegram Messages Silently Dropped](openclaw/openclaw Issue #80520):** Gateway processes messages but no `sendMessage` API call is logged. **Status:** OPEN. 10 comments, no fix PR identified yet.
- **[Telegram Generic Error Fallback](openclaw/openclaw Issue #86184):** Tool-heavy turns succeed internally but the user sees only "Something went wrong." **Status:** OPEN. 7 comments.
- **[EmbeddedAttemptSessionTakeoverError](openclaw/openclaw Issue #85913):** Race condition where concurrent embedded runs (heartbeat vs. channel/direct) on the same session file trigger takeover errors. **Status:** OPEN. Fix PR [`#86427`](openclaw/openclaw PR #86427) is ready for maintainer review.
- **[Subagent Completion Callback Timeout](openclaw/openclaw Issue #85953):** `sessions_yield` leaves parent session transcript lock held, blocking subagent completion. **Status:** OPEN. 6 comments.
- **[Codex App-Server Mid-Turn Closure](openclaw/openclaw Issue #86214):** Large image/tool requests cause the UI to show a stopped state due to oversized `logs_2.sqlite`. **Status:** OPEN. Fix PR [`#86233`](openclaw/openclaw PR #86233) caps the log size.
- **[Matrix Thread Session Duplication](openclaw/openclaw Issue #75670):** Lowercasing event IDs in session keys creates duplicate stuck sessions and thread delivery failures. **Status:** OPEN. 5 comments.

### P2 — Notable
- **[Native Hook Relay Stuck](openclaw/openclaw Issue #73723):** Codex-native tool execution blocks behind hook relay even when all hooks report ready. **Status:** OPEN. 7 comments.
- **[LLM Idle Timeout Silent Drop](openclaw/openclaw Issue #84945):** Timeout after tool calls is written to session log but never broadcast to the client. **Status:** CLOSED.

---

## 6. Feature Requests & Roadmap Signals

### Likely In Next Releases
- **MCP Tool Approval Gates (PR [`#78303`](openclaw/openclaw PR #78303)):** Adds a "consent envelope" for MCP tool calls (send email, create records), mirroring `exec-approvals` for shell commands. A strong architectural response to prior approval-flow bugs.
- **Ollama Reasoning Sanitizer (PR [`#86286`](openclaw/openclaw PR #86286)):** Strips leaked inline reasoning prefixes from Kimi Cloud models to prevent user-facing contamination.
- **Session Lineage & Discovery (Issues [`#79903`](openclaw/openclaw Issue #79903), [`#79904`](openclaw/openclaw Issue #79904), [`#79905`](openclaw/openclaw Issue #79905)):** A systematic push to add cursored SQLite transcript reads, durable session lineage, and typed transcript projections. This is a necessary maturity step for the new SQLite runtime.

### Strong Predictions for v2026.6.x
- **Enhanced Security Tooling:** Given the P0 memory leak and the popularity of Masked Secrets, expect commit toward filesystem sandboxing (Issue [`#7722`](openclaw/openclaw Issue #7722)) and denylist-based exec-approvals (Issue [`#6615`](openclaw/openclaw Issue #6615)).
- **Session Concurrency Hardening:** The raft of takeover and lock-release bugs (Issues [`#85913`](openclaw/openclaw Issue #85913), [`#85953`](openclaw/openclaw Issue #85953), [`#58479`](openclaw/openclaw Issue #58479)) makes session state the #1 reliability priority. Expect deeper fix sets around the session-lock controller.
- **Linux/Windows Client Movement:** While no active PR exists, the sustained pressure from Issue [`#75`](openclaw/openclaw Issue #75) (106 comments, 77 👍) makes this the most important platform expansion signal on the roadmap.

---

## 7. User Feedback Summary

### Pain Points (Dissatisfaction)
- **Message Reliability:** Users report Telegram messages "silently dropped" with no error trace. This is the most damaging class of bug for user trust. *"Happened multiple times today... no sendMessage API call is logged, and the user never receives a reply."*
- **Session Instability:** The `EmbeddedAttemptSessionTakeoverError` errors are frustrating users on single-direct turns, even with cron/heartbeat disabled. *"Every agent turn fails before producing a reply."*
- **Cron Job Complexity:** The mandatory `agentTurn` flow for cron jobs is seen as over-engineered for simple automation, adding unnecessary latency and cost. *"Forces LLM interpretation of simple commands... Adds unnecessary API calls and latency."*
- **Accessibility:** The TUI's heavy use of emojis and unicode box-drawing characters creates a "verbose, confusing output" for screen-reader users.

### Use Cases Emerging
- **Deep Research / Long-Context Workflows:** Users integrating Kimi K2.5 and DeepSeek-R1 are pushing the architecture's limits in streaming, watchdog timeouts, and context management.
- **Team/Enterprise Automation:** Requests for Slack Block Kit, AWS deployment guides, backup/restore utilities, and native secrets management all point to a growing segment of users deploying OpenClaw in production team environments.
- **Regional Provider Adoption:** Xiaomi MiMo Token Plan and other non-standard provider configurations signal global diversification of the user base.

---

## 8. Backlog Watch

Several high-impact issues remain unresolved for extended periods and require maintainer attention:

| Issue | Created | Comments / Reactions | Status | Risk |
|-------|---------|----------------------|--------|------|
| **[Linux/Windows Desktop Apps](openclaw/openclaw Issue #75)** | 2026-01-01 | 106 comments, 77 👍 | OPEN (P2) | **Strategic.** Most requested feature. Stagnation here creates an opportunity for competing projects. |
| **[Prebuilt Android APK](openclaw/openclaw Issue #9443)** | 2026-02-05 | 25 comments, 2 👍 | OPEN (P2) | **Adoption barrier.** Users cannot easily test the companion app without compiling from source. |
| **[Slack Block Kit Support](openclaw/openclaw Issue #12602)** | 2026-02-09 | 13 comments | OPEN (P2) | **Enterprise blocker.** Plain-text Slack responses limit professional use cases. |
| **[Filesystem Sandboxing Config](openclaw/openclaw Issue #7722)** | 2026-02-03 | 7 comments, 4 👍 | OPEN (P2) | **Security fundamental.** Current fileAccess config doesn't restrict as documented. |
| **[Backup/Restore Utility](openclaw/openclaw Issue #13616)** | 2026-02-10 | 8 comments | OPEN (P2) | **Operator essential.** No standardized way to migrate or recover environments. |
| **[Memory Trust Tagging](openclaw/openclaw Issue #7707)** | 2026-02-03 | 5 comments | OPEN (P2) | **Proactive security.** Particularly relevant after the recent P0 privacy leak. Prevents memory poisoning attacks. |
| **[AWS Deployment Guides](openclaw/openclaw Issue #13597)** | 2026-02-10 | 6 comments, 3 👍 | OPEN (P2) | **Compute adoption.** Lack of EC2/ECS/Lambda docs is a barrier to production cloud deployments. |

*Analysis: The backlog is dominated by three themes: **platform expansion** (#75, #9443), **enterprise/ops maturity** (#13616, #13597, #12602), and **proactive security** (#7722, #7707). Addressing even one of these in the next release cycle would significantly strengthen the project's position for production workloads.*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: AI Agent OSS Landscape
**Date:** 2026-05-25 | **Analyst:** Ecosystem Intelligence Unit

---

## 1. Ecosystem Overview

The open-source AI agent landscape is experiencing a hyper-competitive "platform war," with projects simultaneously racing to define architecture standards, security baselines, and user experience paradigms. The ecosystem is bifurcated between **foundational infrastructure** (reliable session management, memory isolation, secure tool dispatch, multi-agent orchestration) and **end-user experience** (cross-platform clients, rich UIs, enterprise IM integrations, intuitive configuration). A clear maturity gradient is emerging: projects focused on rapid feature iteration (OpenClaw, ZeroClaw, IronClaw) dominate raw activity metrics, while those prioritizing production stability (Moltis, LobsterAI) demonstrate higher merge-to-issue ratios and faster bug-to-fix cycles. The common strategic imperative across all projects is the urgent migration away from single-agent chat patterns toward **structured, secure, multi-channel agent platforms** capable of deeply reasoned, long-horizon tasks.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today? | Merged/Closed | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | ✓ (2 betas) | 185 PRs / 203 Issues | **Highest raw velocity;** major refactor masking stability risks |
| **ZeroClaw** | 50 | 50 | ✗ | 8 | **Architecture-driven;** MCP sharp edges, channel explosion |
| **IronClaw** | 27 | 50 | ✗ (blocked) | 8 | **Reborn migration in full swing;** release pipeline stalled |
| **CoPaw** | 27 | 37 | ✗ | 24 | **Testing & UX hardening;** Coding Mode imminent |
| **LobsterAI** | 0 (8 stale updated) | 22 | ✗ | 14 | **Subagent maturation;** OpenClaw integration sync |
| **Hermes Agent** | 50 | 50 | ✗ | 3 | **Stability sprint;** platform bugs, maintainer bottleneck |
| **NanoBot** | 6 | 114 | ✗ | 8 | **Deep backlog triage;** 106 open PRs critical risk |
| **PicoClaw** | 8 | 9 | ✓ (nightly) | 2 | **Rapid-response fixes;** Agent Collaboration Bus in review |
| **NanoClaw** | 2 | 10 | ✗ | 4 | **Feature delivery complete;** per-agent config landed |
| **Moltis** | 0 (8 closed) | 10 merged | ✗ | 8 / 10 | **Exceptional health;** zero open bugs, 1-day fix turnaround |
| **NullClaw** | 0 | 1 (auto) | ✗ | 0 | **Maintenance mode** |
| **TinyClaw / ZeptoClaw** | 0 | 0 | ✗ | 0 | **No activity** |

*Note: "Merged/Closed" measures output velocity. A lower ratio of merges to open PRs indicates a review bottleneck.*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Mindshare & Ecosystem Gravity:** With 500 issues/PRs updated (2.5x the next most active project), OpenClaw commands the largest community testing and feedback surface. The "core reference" designation is a self-fulfilling advantage—contributors build for OpenClaw first.
- **Release Cadence:** Two beta releases in a single day vs. zero for every other project. This signals mature CI/CD and a commitment to rapid iteration.
- **Security Governance:** The auto-merged hook ingress fix and P0 memory leak closure demonstrate best-in-class security response velocity.

**Technical Approach Differences:**
- OpenClaw is executing a **unified core refactor** (decoupling the monolithic "Pi" runtime). Contrast this with **ZeroClaw's trait-based abstractions** (MemoryStrategy) or **Moltis's agent-centric boundaries**. OpenClaw bets on a single, well-debugged engine; competitors bet on composability.
- The iMessage approval reaction UX (tapbacks) highlights OpenClaw's willingness to innovate on **native mobile interaction patterns**—a frontier most peers have not addressed.

**Community Size Comparison:**
- OpenClaw's 185 PRs merged in 24h exceeds the *total monthly merges* of most peers. Next highest: CoPaw (24), LobsterAI (14).
- However, **raw volume does not equal stability.** OpenClaw has the highest count of P0/P1 bugs (Telegram silent drops, session takeover races) among active projects. Moltis, by contrast, had zero open bugs today.

**Strategic Risk:**
- The Linux/Windows client gap (#75, 106 comments, 77 👍) is OpenClaw's most exploitable weakness. If a competitor ships a polished desktop client before OpenClaw, they can capture significant mindshare.

---

## 4. Shared Technical Focus Areas

Several requirements are emerging independently across multiple projects, indicating industry-wide consensus on what an AI agent platform must deliver:

| Focus Area | Manifesting Projects | Specific Needs (Examples) |
|---|---|---|
| **Memory & Data Isolation** | OpenClaw, ZeroClaw, CoPaw, LobsterAI | P0 privacy leak from shared context (OpenClaw); Intelligent Memory proposals (CoPaw); MemoryStrategy trait (ZeroClaw) |
| **Secret & Credential Protection** | OpenClaw, Moltis, IronClaw | MCP env var leakage (Moltis); prompt injection defense (OpenClaw #10659); URL path injection (IronClaw #3917) |
| **Session & Concurrency Resilience** | OpenClaw, Hermes Agent, PicoClaw, ZeroClaw | Lock takeover races (OpenClaw #85913); PID reuse crashes (PicoClaw #2720); silent timeout drops (all) |
| **Tool Loop Prevention & Audit** | NanoBot, OpenClaw, IronClaw, ZeroClaw | Tool cycles consuming tokens (NanoBot #3986); dispatch bypassing audit trail (IronClaw #4017); MCP filter no-op (ZeroClaw #6699) |
| **Per-Agent/Per-Workspace Configuration** | NanoClaw, Moltis, Hermes Agent | Agent-specific models/providers (NanoClaw #1968); role-based capability boundaries (Moltis #1049); per-platform model config (Hermes #14327) |
| **Streaming & Long-Context Watchdogs** | OpenClaw, Hermes Agent, CoPaw | 30s watchdog resets on reasoning models (OpenClaw #68596); silent Codex hangs (Hermes #21444) |
| **Enterprise Channel Support** | OpenClaw, Hermes Agent, ZeroClaw, IronClaw, LobsterAI | Slack Block Kit (OpenClaw #12602); Feishu (Hermes, ZeroClaw); WeCom (IronClaw); QQ Bot (LobsterAI) |

---

## 5. Differentiation Analysis

Despite convergent pressures, each project occupies a distinct strategic niche:

| Project | Core Identity | Target User | Key Differentiator |
|---|---|---|---|
| **OpenClaw** | The **System Standard** | Power users, enterprise pilots | Broadest integration surface; setting de facto patterns (ClawSweeper, MCP approval gates) |
| **ZeroClaw** | The **Architecture Laboratory** | Infrastructure engineers | Cleanest trait abstractions (MemoryStrategy); governance RFCs; multi-DB backends |
| **IronClaw** | The **Rust Foundation** | Performance/safety-critical teams | WASM channel isolation; Tokio-native async; strict security invariants |
| **LobsterAI** | The **Desktop IDE** | AI researchers, power desktop users | Best-in-class UI (reasoning blocks, context slider, subagent sidebar); tight OpenClaw integration |
| **CoPaw** | The **Platform Ecosystem** | Versatile developers | Plugin store (DataPaw); built-in Coding Mode; massive test coverage |
| **Moltis** | The **Security Guardian** | Enterprise, privacy-conscious users | Fastest bug-to-fix cycle (zero open bugs); sandbox-first; secret typing |
| **Hermes Agent** | The **ChatOps Connector** | DevOps, team communication | Deepest platform-specific UX (Slack blocks, Feishu cards, WhatsApp quotes) |
| **NanoBot** | The **Research Agent** | AI researchers, agent builders | Dream System (self-improvement); theory of mind; complex workflow orchestration |
| **PicoClaw** | The **Lightweight Pioneer** | Developers seeking minimal footprint | Rapid response (fixes in hours); Agent Collaboration Bus (emerging multi-agent pattern) |
| **NanoClaw** | The **Config-First Framework** | Developers wanting structured config | Per-agent model/provider config as first-class feature; strong CLI tooling |

---

## 6. Community Momentum & Maturity

The ecosystem can be categorized into four tiers based on the balance of iteration velocity, stability, and review capacity:

**Tier 1: Explosive Growth / High Risk-High Reward**
- *OpenClaw, ZeroClaw, IronClaw*
- Massive PR/issue volume. High feature throughput. Significant stability churn (P0 bugs, release pipeline blocks). Require sophisticated users who can tolerate volatility.
- *Signal:* High contributor influx but maintainer capacity is the existential risk.

**Tier 2: Rapid Maturation / Stabilizing**
- *Moltis, LobsterAI, CoPaw, PicoClaw*
- Lower raw issue counts but high merge velocity and rapid bug closure. Focused on hardening existing features and closing long-standing issues. Best ratio of quality to velocity.
- *Signal:* Ready for production-adjacent workloads. Moltis (zero open bugs) is the benchmark.

**Tier 3: Feature-Led Growth / Review Bottleneck**
- *NanoBot, Hermes Agent, NanoClaw*
- Rich feature backlog and community contributions, but maintainer review capacity is the primary constraint. High open-PR counts (NanoBot: 106, Hermes: 45) risk contributor burnout.
- *Signal:* Need to delegate trust or hire/recruit core reviewers to capitalize on community investment.

**Tier 4: Stable / Idle**
- *NullClaw, TinyClaw, ZeptoClaw*
- No organic development activity. NullClaw receiving only automated Dependabot updates. Unlikely to compete for users unless a major new release drops.

---

## 7. Trend Signals

Extracted from community feedback across all projects, the following trends will shape AI agent development over the next quarter:

1. **Reasoning Models Stress Infrastructure:** DeepSeek-R1, Kimi K2.5, and Claude Opus are breaking 30s streaming watchdogs, session timeouts, and context management assumptions. **Design implication:** The "chat" paradigm must evolve into a "deep research" paradigm with dynamic timeouts, token budgeting, and progress reporting.

2. **Trust is the Product-Market Fit:** The P0 memory leak (OpenClaw), MCP credential exposure (Moltis), and audit bypass (IronClaw) are not isolated incidents—they are symptoms of a market moving from "can it work?" to "can it be trusted?". **Action:** Security (memory isolation, secret masking, tool audit chains, sandboxing) is the highest-leverage investment for production adoption.

3. **Per-Agent Everything:** Monolithic agents are dead. NanoClaw's per-agent provider config, Moltis's agent capability boundaries, and Hermes's per-platform model settings all point to **multi-agent, multi-role, multi-context** as the new baseline.

4. **Channel Proliferation is Mandatory:** An agent that cannot speak on the user's platform of choice is invisible. The arms race for Slack, Discord, Telegram, Feishu, WhatsApp, WeChat, DingTalk, QQ, Lark, and Matrix support creates enormous integration surface area—and immense quality risk (100% CPU loops, silent drops).

5. **MCP Security is the Wild West:** ZeroClaw's tool_filter_groups no-op, Moltis's env var leakage, and OpenClaw's approval gates all highlight that **Model Context Protocol tooling lacks standardized security primitives.** This is the next critical industry infrastructure gap.

6. **Memory Architecture is the Unlocked Battlefield:** OpenClaw (trust tagging), ZeroClaw (MemoryStrategy trait), CoPaw (Intelligent Memory proposal), and NanoBot (Semantic Memory Index) are all racing to solve persistent, secure, and efficient agent memory. **This is likely the single highest-value differentiation for "personal AI" in the next 12 months.**

7. **Desktop/Client Experience Creates Winners:** The #1 feature request across the ecosystem is native Linux/Windows apps (OpenClaw #75) and polished UIs (LobsterAI's desktop IDE, CoPaw's Coding Mode). **The project that ships a truly great desktop client first will capture the "power user" segment.**

8. **Maintainer Health is a Market Signal:** Moltis's zero-bug state demonstrates the outcome of sustainable maintenance. NanoBot's 106 open PRs and Hermes's 45 open PRs signal risk. **The market will consolidate around projects that demonstrate they can both ship fast AND close the loop.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the structured project digest for NanoBot based on the provided GitHub data.

---

# NanoBot Project Digest – 2026-05-25

## 1. Today's Overview
NanoBot experienced an exceptionally high tide of activity today, with **114 pull requests** and **6 issues** updated within the last 24 hours. While no new releases were cut, the maintainers appear to be conducting a deep triage of a massive feature backlog, with dozens of long-standing PRs from March receiving fresh attention. Bug resolution velocity remained impressive, with several critical issues closed the same day they were filed. The combined focus remains on agent reliability (breaking tool loops), core architectural improvements (Dream System overhaul), and expanding connectivity. The primary risk to project health remains a significant review bottleneck, with **106 open PRs**, though today’s activity is a strong signal that the bottleneck is being actively addressed.

## 2. Releases
**None.** No new releases were published today.

## 3. Project Progress
Today saw **8 PRs merged or closed** alongside the resolution of several critical issues.

- **Bug Squashed:**
    - **Subagent Config Propagation (PR [#3978] – Merged):** A critical bug where the `maxConcurrentSubagents` configuration was completely ignored and always defaulted to `1` was fixed. This is a major unlock for users trying to run complex parallel agent workflows.
    - **Streaming Display Crash (Issue [#3995] – Closed):** A severe PowerShell terminal flickering issue caused by forced newlines in the agent streaming output was identified and fixed within hours.
    - **Provider Trace Mismatch (Issue [#3980] – Closed):** A bug causing `tool_call_id` mismatches when using third-party API proxies (antchat) was resolved.
- **Features Advancing:**
    - **Tool Loop Detection Ecosystem:** While PR [#3985] (Loop Guard v2.0) was closed as invalid, the underlying feature request (Issue [#3986]) for a general tool-level loop and rate-limiting guard was resolved. Attention is consolidating around the existing `CycleDetector` (PR [#2271]).
    - **Dream System Refactor (PR [#3990]):** In direct response to community feedback (Issue [#3973]), a major PR was opened to overhaul the Dream system, merging two-phase consolidation into a single phase.

## 4. Community Hot Topics
Despite low comment counts on specific issues, the underlying need is highly intense and shapes the bulk of the activity.

- **Agent Loop Prevention & Guardrails (Issues [#3986], PRs [#2271], [#3985]):** The hottest topic by far. Users are deeply frustrated by LLMs exhausting tokens on repetitive, failing tool calls (e.g., grepping the same pattern endlessly). The feature request for a "通用护栏" (general guardrail) reflects a widespread desire for robust self-preservation. The community has multiple competing implementations, signaling high demand for a unified review.
- **Dream System "Hunger Problem" (Issue [#3973] / PR [#3990]):** User `chxuan` provided a sophisticated critique of the Dream System, calling it "starved" and lacking real-time learning. The immediate architectural response with PR [#3990] shows exceptional developer-user engagement and is a critical discussion point for advanced users.
- **The Feature Backlog Wave (PRs [#2466], [#2509], [#2618], [#2374]):** A huge number of major enhancement PRs from March were updated today. These include Multi-Subagent Orchestration, a new Multi-Agent system with auto-routing, a Semantic Memory Index, and pluggable Security Middleware. This creates a sense of a massive feature release just over the horizon, but the sheer volume also raises questions about integration priority.

## 5. Bugs & Stability

- **Critical (Fixed):**
    - **[Issue [#3995]](https://github.com/HKUDS/nanobot/issues/3995):** **PowerShell Streaming Rendering Crash.** Forced newlines in streaming output made the terminal unusable. **Severity:** High (Windows Usability). **Fix:** Applied.
    - **[PR [#3978]](https://github.com/HKUDS/nanobot/pull/3978):** **Subagent Config Breakage.** The `maxConcurrentSubagents` config was silently ignored. **Severity:** Critical (Configuration Integrity). **Fix:** Merged.
- **High (Fixed):**
    - **[Issue [#3980]](https://github.com/HKUDS/nanobot/issues/3980):** **OpenAI Compatible API Trace Mismatch.** `tool_call_id` inconsistencies broke activity traces for specific proxies. **Severity:** High (Observability). **Fix:** Applied.
- **Moderate (Open):**
    - **[Issue [#3993]](https://github.com/HKUDS/nanobot/issues/3993):** **Anthropic Provider Content Block Error.** Tools returning bare dicts cause errors because the provider doesn't coerce them correctly to text blocks. A patch is proposed in the issue thread.

## 6. Feature Requests & Roadmap Signals

- **Next Major Features (Likely v0.3+):**
    - **Dream System V2 (PR [#3990]):** Moving to single-phase consolidation with SNIP/MECE principles.
    - **Capability Store (PR [#3991]):** A new "Store" UI tab suggests a move toward a plugin/app discovery marketplace.
    - **Multi-Agent Orchestration (PRs [#2466], [#2509]):** Role templates, progress tracking, and auto-routing signal a shift from single agents to complex, organized agent swarms.
    - **Production Channel Features (PR [#3996]):** Telegram Webhook support indicates maturation towards production scalability.
- **Roadmap Signals from User Feedback:**
    - The community is loudly demanding a robust, generalized **Tool Loop Detection** system. The next release will almost certainly include a prominent feature addressing this.
    - There is desire for **better error propagation** (config bugs like #3978 erode trust in complex setups).

## 7. User Feedback Summary

- **Pain Points & Dissatisfaction:**
    - **Agent "Dumb Loops":** The most vocal frustration is LLMs wasting resources on repetitive, failing tool calls. Users want the framework to enforce smart behavior.
    - **Configuration Friction:** Users configuring advanced features (like sub-agents) find that settings don’t always propagate correctly, leading to silent failures.
    - **Dream System Depth:** Power users like `chxuan` feel the highly-touted Dream System for self-improvement is currently superficial.
- **Satisfaction & Positives:**
    - **Rapid Bug Fixing:** Users experiencing the PowerShell rendering crash (#3995) or the config bug (#3978) saw fixes applied the same day, building trust in the project's responsiveness.
    - **Feature Richness:** The sheer volume of enhancements in the pipeline gives the community confidence in the future trajectory of the project.

## 8. Backlog Watch
The staggering number of open PRs **(106)** represents the single biggest operational challenge for the project. Today’s activity cycle is promising, but sustained effort is required to prevent contributor burnout.

- **Critical PRs Needing Maintainer Decision:**
    - **[PR [#2271]](https://github.com/HKUDS/nanobot/pull/2271) – Tool Cycle Detection (Open since Mar 19):** Directly addresses the #1 community pain point. Needs a final review to be harmonized with the feedback from Issue [#3986].
    - **[PR [#2374]](https://github.com/HKUDS/nanobot/pull/2374) – ToolGuard Security Middleware (Open since Mar 23):** A foundational security layer that supersedes string-matching approaches. High priority for production users.
    - **[PR [#2618]](https://github.com/HKUDS/nanobot/pull/2618) – Semantic Memory Index (Open since Mar 29):** Closes a core roadmap item (#80). Essential for persistent, scalable agent memory.
    - **[PR [#1443]](https://github.com/HKUDS/nanobot/pull/1443) – Silent Heartbeat Reasoning (Open since Mar 2):** The oldest actively discussed large PR. Requires a final call on merge or closure.
- **Risk Assessment:**
    - **High:** The backlog of 106 open PRs poses a significant risk of feature entropy and contributor discouragement. Today’s mass update is a very positive sign that maintainers are actively working through it, but turning this burst of activity into sustained merges is critical for project health.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the structured project digest for Hermes Agent based on the May 25, 2026 GitHub activity data.

---

## Hermes Agent Project Digest — 2026-05-25

### 1. Today's Overview
The Hermes Agent project experienced an exceptionally high volume of activity on May 25, with **50 issues** and **50 pull requests** updated in the last 24 hours. The project appears to be in an intensive **stability and triage sprint**: while 40 issues remain open, the community is actively stress-testing the agent across a wide range of providers (OpenAI, xAI, Anthropic) and platforms (Docker, Windows, macOS, Telegram, Feishu, QQBot). The 45 currently open pull requests suggest a significant review bottleneck, yet the rapid closure of several high-impact bugs (e.g., the `/q` TUI alias crash) indicates maintainers are prioritizing critical user-experience regressions. No new releases were cut today, but the sheer volume of merged and pending work strongly implies a substantial release (likely v0.14.x) is building.

### 2. Releases
**None.** No new releases were published on May 25, 2026.

### 3. Project Progress
Today saw the closure of three visible pull requests, advancing core stability and developer experience:

- **[PR #31985 (merged)](https://github.com/NousResearch/hermes-agent/pull/31985) — Fix TUI `/q` alias:** Resolved the dangerous alias collision where typing `/q` in the TUI triggered `/quit` instead of the intended `/queue` command. This fix directly addresses a major workflow disruption.
- **[PR #31990 (merged)](https://github.com/NousResearch/hermes-agent/pull/31990) — Custom branch strategy guide:** Added documentation to help contributors manage branching workflows, lowering the barrier for new community patches.
- **[PR #26606 (closed)](https://github.com/NousResearch/hermes-agent/pull/26606) — Kanban plugin metadata:** Formalized the packaging of the Kanban dashboard plugin, keeping the plugin ecosystem aligned with upstream testing requirements.

These changes solidify the **TUI** and **plugin system** as key areas of committed focus for the current sprint.

### 4. Community Hot Topics
The most active discussions demonstrate a strong user desire for **provider reliability** and **cross-platform UX parity**:

- **Silent OpenAI Codex Timeouts ([Issue #21444](https://github.com/NousResearch/hermes-agent/issues/21444) — 9 comments, 4 👍):** This remains the most deeply analyzed community thread. A non-engineer user provided extensive packet-level debugging of a ~300-second silent hang when using the `openai-codex` provider. The underlying need is clear: **users cannot trust the agent if primary inference pathways fail without feedback.** The community needs a robust streaming watchdog.
- **Slack Markdown Table Rendering ([Issue #18918](https://github.com/NousResearch/hermes-agent/issues/18918) — 3 comments, 6 👍):** Despite being almost a month old, this issue garnered the highest reaction count today. Users are asking for native Slack Block Kit rendering of pipe tables. The deep need is professional-grade output in enterprise collaboration tools where structured data (comparisons, metrics) is common.
- **Gateway Model Persistence ([Issue #30781](https://github.com/NousResearch/hermes-agent/issues/30781) — 3 comments):** Users are frustrated that `/model` switches do not persist in `config.yaml` across gateway restarts. This points to a broader need for **session durability** in remote/messaging workflows.

### 5. Bugs & Stability
Today’s bug intake was dominated by **P2 stability issues** across the platform matrix, although several critical P1 problems were also identified.

| Severity | Issue | Status | Fix PR | Analysis |
|---|---|---|---|---|
| **P1** | **Telegram silent drop after `/stop`** ([Issue #31884](https://github.com/NousResearch/hermes-agent/issues/31884)) | **OPEN** | None Yet | The gateway can mark a turn complete with `0 chars` while internal tool work continues, silently swallowing the final answer. This severely erodes user trust. |
| **P1** | **v0.9.0 Triple Bug (Context/Auth/Config)** ([Issue #11096](https://github.com/NousResearch/hermes-agent/issues/11096)) | **OPEN** | None Yet | A month-old report detailing context_length overrides failing, thinking-block session issues, and config precedence bugs. No fix has been merged. |
| **P2** | **OpenAI Codex Hang** ([Issue #21444](https://github.com/NousResearch/hermes-agent/issues/21444)) | **CLOSED** | **[PR #31984](https://github.com/NousResearch/hermes-agent/pull/31984)** | Although the issue is closed, the root cause is being architecturally solved by a new “time-to-first-byte” watchdog in the streaming transport layer. |
| **P2** | **Docker UID chown miss** ([Issue #27221](https://github.com/NousResearch/hermes-agent/issues/27221)) | **OPEN** | None Yet | Entrypoint fails to remap ownership of `ui-tui/` and `gateway/` dirs when `HERMES_UID` is changed. Breaking Unraid/Synology deployments. |
| **P2** | **QQBot 100% CPU Loop** ([Issue #31771](https://github.com/NousResearch/hermes-agent/issues/31771)) | **OPEN** | None Yet | WebSocket reconnect failure causes a sustained busy loop. |
| **P2** | **MCP HTTP Transport Crash** ([Issue #31987](https://github.com/NousResearch/hermes-agent/issues/31987)) | **OPEN** | None Yet | `anyio` RuntimeError during cleanup prevents MCP server reconnects. |
| **P2** | **Missing CODEOWNERS Security Finding** ([Issue #31935](https://github.com/NousResearch/hermes-agent/issues/31935)) | **OPEN** | None Yet | Persistent finding: workflow files lack mandatory review protection. |

**Summary:** Stability is currently the project’s biggest weakness. The influx of Docker/permission bugs and platform-specific adapter failures suggest rapid user growth outpacing the hardening of new features.

### 6. Feature Requests & Roadmap Signals
The roadmap shows a clear split between near-term platform polish and long-term architectural evolution:

- **Near-Ready Features (Likely for v0.14.x):**
    - **Feishu CardKit Streaming** ([PR #31989](https://github.com/NousResearch/hermes-agent/pull/31989)): Adds rich, collapsible reply cards for Feishu users.
    - **WhatsApp Native Quoting** ([PR #21977](https://github.com/NousResearch/hermes-agent/pull/21977)): Provides proper quote/reaction primitives via the Baileys bridge.
    - **Dashboard UI Polish** ([PR #31944](https://github.com/NousResearch/hermes-agent/pull/31944)): A visual refresh toward a cleaner, Feishu-inspired design language.
- **Long-Term Architecturals:**
    - **Pluggable SessionDB Provider** ([Issue #23717](https://github.com/NousResearch/hermes-agent/issues/23717)): An RFC for PostgreSQL/MySQL backends. This signals enterprise readiness but is likely weeks away from implementation.
    - **Per-Platform Model Config** ([Issue #14327](https://github.com/NousResearch/hermes-agent/issues/14327)): A popular request to allow different models for Discord vs. Slack vs. CLI.
- **Wildcards:**
    - **GitHub Issues as Agent Task Queue** ([Issue #31928](https://github.com/NousResearch/hermes-agent/issues/31928)): A meta-proposal to use the GH issue tracker as the agent’s own task routing system. This is an intriguing automation workflow that may appear as a plugin.

### 7. User Feedback Summary
User sentiment is bifurcated between **high engagement** from power users and **frustration** from self-hosters and Windows users.

- **Pain Points (Dissatisfaction):**
    - **Docker & Unraid Deployment:** Multiple users ([Issue #27221](https://github.com/NousResearch/hermes-agent/issues/27221), [Issue #23402](https://github.com/NousResearch/hermes-agent/issues/23402)) are hitting permission and `chown` issues. This is the #1 friction point for the homelab/self-hosted segment.
    - **Windows Support:** The Dashboard returning a blank page due to MIME type errors ([Issue #28987](https://github.com/NousResearch/hermes-agent/issues/28987)) and TUI crashes on cross-mount paths ([Issue #31915](https://github.com/NousResearch/hermes-agent/issues/31915), closed) paint a picture of Windows as a second-class platform.
    - **Provider Auth Flakiness:** Users are reporting confusing OAuth loops (xAI [Issue #27385](https://github.com/NousResearch/hermes-agent/issues/27385)) and silently dropped tokens (Auxiliary fallback [Issue #31978](https://github.com/NousResearch/hermes-agent/issues/31978), closed).

- **Positive Signals (Satisfaction):**
    - **Quality of Community Bug Reports:** The detailed, source-verified reports from “non-engineers” (e.g., [Issue #20590](https://github.com/NousResearch/hermes-agent/issues/20590), [Issue #21444](https://github.com/NousResearch/hermes-agent/issues/21444)) indicate that Hermes is attracting a sophisticated user base willing to invest in the project’s improvement.
    - **Feature Parity Desire:** The volume of requests for specific platform features (Slack tables, Feishu cards, WhatsApp quotes) indicates users aren't just trying Hermes—they are *depending* on it as their primary AI interface.

### 8. Backlog Watch
Several critical contributions and reports are languishing without maintainer action, raising concerns about review capacity:

- **Tranquil-Flow's PR Stalemate:** Community contributor **Tranquil-Flow** has five essential PRs open without merge, some over a month old:
    - Propagating custom provider `context_length` ([PR #13540](https://github.com/NousResearch/hermes-agent/pull/13540))
    - Docker environment variable forwarding ([PR #12825](https://github.com/NousResearch/hermes-agent/pull/12825))
    - Telegram `chat_id` normalization ([PR #13535](https://github.com/NousResearch/hermes-agent/pull/13535))
    - Honcho auto-migration plugin ([PR #12743](https://github.com/NousResearch/hermes-agent/pull/12743))
    - MCP grandchild process tracking ([PR #27516](https://github.com/NousResearch/hermes-agent/pull/27516))
- **Stale Critical Bug:** **[Issue #11096](https://github.com/NousResearch/hermes-agent/issues/11096)** (P1, Three bugs in v0.9.0) remains untouched by maintainers since mid-April despite providing full reproduction steps and local workarounds.
- **Security Gap:** The missing **CODEOWNERS** file ([Issue #31935](https://github.com/NousResearch/hermes-agent/issues/31935)) was noted as a persistent finding since May 11 but remains unaddressed.

**Health Assessment:** While the community is incredibly active and generous with their debugging, the project is showing signs of **maintainer bottleneck**. The high open-PR count and the age of Tranquil-Flow’s contributions suggest the team may need to increase review bandwidth or delegate trust to trusted community members to capitalize on this wave of contributions.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

1. **Today's Overview**
**PicoClaw** is seeing very high activity on 2026-05-25, with **8 issues** and **9 pull requests** updated in the last 24 hours. A new nightly build (`v0.2.9-nightly.20260525.ab6d3946`) was published, and two pull requests were successfully merged. The community and core team are actively addressing a critical compatibility break with Anthropic’s `claude-opus-4-7` model, while a major feature contribution for an internal Agent Collaboration Bus and several stability patches for the PID manager, message bus, and agent loop are under review. The high volume of merged fixes and new feature work signals a robust and responsive development cycle heading into the next stable release.

2. **Releases**
A new automated nightly build is available: **[v0.2.9-nightly.20260525.ab6d3946](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260525.ab6d3946)**. As a pre-release, it may contain unstable changes and is intended for testing. The full changelog diff against the latest stable tag `v0.2.9` can be reviewed [here](https://github.com/sipeed/picoclaw/compare/v0.2.9...main). No formal stable release or specific migration notes are associated with this nightly.

3. **Project Progress**
Two pull requests were merged/closed today, alongside the closure of several long-standing feature issues:
- **Merged — [#2938](https://github.com/sipeed/picoclaw/pull/2938)**: Fixes a critical regression in the Cron tool where `CronTool.ExecuteJob()` failed to pass the required `action` argument to the Exec tool, causing all cron command jobs to fail silently.
- **Merged — [#2759](https://github.com/sipeed/picoclaw/pull/2759)**: Improves the Seahorse retrieval tools by scoping `short_grep` and `short_expand` to the active session by default, enhancing security boundaries.
- **Closed — [#1950](https://github.com/sipeed/picoclaw/issues/1950)**: Streaming output for Web Chat (Nice-to-Have enhancement).
- **Closed — [#2837](https://github.com/sipeed/picoclaw/issues/2837)**: Support for allow/deny/glob tool policies in AGENT.md frontmatter.
- **Closed — [#2839](https://github.com/sipeed/picoclaw/issues/2839)**: Fix for steering-chain final replies incorrectly editing working placeholders instead of sending new messages.

4. **Community Hot Topics**
The most active discussions reflect a mix of long-standing user needs and immediate blocker resolution:
- **[#28 — LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28)** (20 comments, 2 👍): The most-commented open issue remains this feature request, highlighting a persistent demand for simplified LLM provider connectivity for non-technical users.
- **[#1042 — `exec` tool `guardCommand` bug](https://github.com/sipeed/picoclaw/issues/1042)** (13 comments, 2 👍): A long-running technical discussion about the tool’s regular expression logic blocking legitimate commands like `curl`. The underlying need is for a safer, context-aware path validation blacklist/whitelist.
- **[#2939 / #2940 — `claude-opus-4-7` Temperature Error](https://github.com/sipeed/picoclaw/issues/2939)**: A rapidly escalating topic where the bug report and a fix PR were submitted within hours of each other by the same user. This reflects a highly responsive community that moves quickly to unblock users.
- **[#2937 — Agent Collaboration Bus](https://github.com/sipeed/picoclaw/pull/2937)**: A new, large-scope feature PR introducing durable inter-agent communication with mailboxes and permission-aware channels. This signals strong community appetite for multi-agent architectural patterns.

5. **Bugs & Stability**
Bug triage reveals several high-priority stability and compatibility issues actively being addressed:
- **Critical — [#2939](https://github.com/sipeed/picoclaw/issues/2939)**: `claude-opus-4-7` calls fail with HTTP 400 because the model no longer accepts the `temperature` parameter. **Fix exists:** PR [#2940](https://github.com/sipeed/picoclaw/pull/2940) submitted by the same reporter.
- **High — [#2720](https://github.com/sipeed/picoclaw/issues/2720)**: The singleton PID check does not verify process identity. If a gateway crashes and the PID is reused (e.g., by `systemd-resolved`), the gateway enters a crash loop. **Fix exists:** PR [#2813](https://github.com/sipeed/picoclaw/pull/2813) is under review.
- **Medium — [#1042](https://github.com/sipeed/picoclaw/issues/1042)**: The `exec` tool’s `guardCommand` uses simple regex path evaluation, blocking harmless commands like `curl`.
- **Medium — [#2796](https://github.com/sipeed/picoclaw/issues/2796)**: History view truncates previous user messages, only displaying the last message sent in a turn.

6. **Feature Requests & Roadmap Signals**
The closure of **Streaming Output for Web Chat** ([#1950](https://github.com/sipeed/picoclaw/issues/1950)) and **AGENT.md tool policies** ([#2837](https://github.com/sipeed/picoclaw/issues/2837)) strongly indicates these features are landing in the next stable build, advancing both the user-facing experience and multi-agent governance. The most ambitious new proposal is the **Agent Collaboration Bus** ([#2937](https://github.com/sipeed/picoclaw/pull/2937)), which could be a tentpole feature for a `v0.3.0` release. The **WeChat multi-account configuration** PR ([#2883](https://github.com/sipeed/picoclaw/pull/2883)) is also moving forward, targeting the Chinese market. The stale **LM Studio Easy Connect** ([#28](https://github.com/sipeed/picoclaw/issues/28)) remains the top user experience gap to fill for casual users.

7. **User Feedback Summary**
Real user pain points this cycle center on **API compatibility** and **reliability**. The immediate breakage with `claude-opus-4-7` ([#2939](https://github.com/sipeed/picoclaw/issues/2939)) illustrates the difficulty of keeping pace with rapidly evolving external LLM APIs. The silent failure of cron jobs (hot-fixed in [#2938](https://github.com/sipeed/picoclaw/pull/2938)) eroded trust in automation features. Users are clearly deploying PicoClaw in demanding, multi-tenant environments, evidenced by rigorous requests for robust PID handling and bus backpressure. Positive sentiment is driven by the community’s proactive development of complex features (e.g., agent collaboration) and the maintainers’ ability to merge critical fixes within 24 hours of regression.

8. **Backlog Watch**
Several important items remain in the backlog requiring maintainer triage:
- **[#28 — LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28)** (Created 2026-02-11): The oldest open feature request with heavy community engagement but no official maintainer design response.
- **[#1042 — `exec` tool `guardCommand` regression](https://github.com/sipeed/picoclaw/issues/1042)** (Created 2026-03-04): A complex tool safety bug with an active technical discussion but no landed fix.
- **[#2781 — Reduce skill catalog token usage](https://github.com/sipeed/picoclaw/pull/2781)** (Created 2026-05-06): A significant performance improvement PR that has been open for 19 days without maintainer feedback or merge, representing a lost opportunity for immediate token optimization.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-25

**Data Source:** GitHub Issues & PRs updated in the last 24h for `nanocoai/nanoclaw`

---

## 1. Today's Overview

NanoClaw experienced **high-velocity development** on May 25, with **10 pull requests and 2 issues** updated in the past 24 hours. A major milestone was reached as PR #1968 was merged, delivering **end-to-end per-agent provider and model configuration** after a month-long development cycle. Critical stability fixes landed, including a prompt resolution of the high-priority `ncl groups delete` foreign-key constraint failure (PR #2526). Meanwhile, a new bug surfaced in message routing (`engage_mode='always'` silently dropping all messages, Issue #2606) that requires quick attention from the maintainers. Overall, the project shows **strong contributor velocity and healthy maintainer response times**, with rough edges typical of a rapidly maturing open-source AI agent framework.

---

## 2. Releases

No new releases were published today. The previous release remains the latest stable version. Given the volume of closed PRs (including the large per-agent config feature), a new release bundling these changes may be imminent.

---

## 3. Project Progress

Four pull requests were closed or merged in the last 24 hours, representing significant feature and stability advances:

**🔧 Major Feature Delivered**
- **[PR #1968 — End-to-end per-agent provider and model configuration](https://github.com/nanocoai/nanoclaw/pull/1968)** *(Author: @IamAdamJowett)*.
  A landmark feature finally closed after a month of review. Five chained commits make per-agent provider and model selection a first-class, fully chat-driveable capability. Sessions can now be routed to different models and providers on a per-agent basis.

**🐛 Critical Bug Fix**
- **[PR #2526 — fix(cli): cascade dependent rows on groups delete](https://github.com/nanocoai/nanoclaw/pull/2526)** *(Author: @glifocat)*.
  Fixes Issue #2525 (High priority). The `ncl groups delete` command and `deleteAgentGroup` function were executing a bare `DELETE FROM agent_groups WHERE id = ?` without clearing dependent rows, triggering a foreign key constraint error on any non-trivial group. A transactional cleanup was added.

**🧪 Build Stability**
- **[PR #2344 — fix(tests): satisfy tightened RoutableAgentMessage and Session types](https://github.com/nanocoai/nanoclaw/pull/2344)** *(Author: @IamAdamJowett)*.
  Resolved five TypeScript compilation errors on `main` resulting from conflicting merged changes, restoring the build.

**🌐 Admin Tooling**
- **[PR #2604 — web: add GET /admin/agent-activity batch endpoint](https://github.com/nanocoai/nanoclaw/pull/2604)** *(Author: @sumsumai)*.
  Added a batch endpoint (`?agentGroupIds=<id1>,<id2>,...`) allowing admin dashboards to fetch "last active" timestamps for multiple agents in a single round trip, supporting UI features like a "Last active" column.

---

## 4. Community Hot Topics

**1. Non-trivial Group Deletion Failure (Resolved)**
**[Issue #2525](https://github.com/nanocoai/nanoclaw/issues/2525) / [PR #2526](https://github.com/nanocoai/nanoclaw/pull/2526)**
*Author: @glifocat | Comments: 1*
High-priority CLI bug where `ncl groups delete` failed on any used group due to a missing cascade delete. Rapidly fixed and merged. Demonstrates strong maintainer responsiveness to blocking user-facing issues.

**2. Silent Message Drops on `engage_mode='always'` (Urgent)**
**[Issue #2606](https://github.com/nanocoai/nanoclaw/issues/2606)**
*Author: @nikki-assistant | Comments: 0*
An `engage_mode: 'always'` configuration stored in the database is completely ignored at runtime. The `evaluateEngage()` function in `src/router.ts` lacks a case for `'always'`, causing all messages from such wirings to be silently dropped with reason `no_agent_engaged`. No fix PR has been opened yet. This undermines a core feature and is likely to generate significant user frustration until resolved.

**3. Platform ID Standardization**
**[PR #2607 — Use platform IDs for inbound message actions](https://github.com/nanocoai/nanoclaw/pull/2607)**
*Author: @danshapiro*
Fixes an API compatibility issue where inbound message actions (e.g., reactions) were using NanoClaw internal composite message IDs instead of the platform's raw message ID, breaking platform API calls.

**4. Proactive CI Maintenance**
**[PR #2608 — ci: bump Node 20 actions to v5 ahead of June 2026 deprecation](https://github.com/nanocoai/nanoclaw/pull/2608)**
*Author: @IamAdamJowett*
Bumps `actions/checkout`, `actions/setup-node`, and `pnpm/action-setup` from Node 20 runtimes to their first Node 24 major (`@v5`) across all workflows, preempting the June 2026 Node 20 deprecation.

---

## 5. Bugs & Stability

| Severity | Status | Issue/PR | Description |
|---|---|---|---|
| **High** | **Active** | [#2606](https://github.com/nanocoai/nanoclaw/issues/2606) | `engage_mode='always'` silently drops all messages. `evaluateEngage()` switch statement has no matching case. No fix PR yet. Urgent. |
| **High** | **Fixed** | [#2525](https://github.com/nanocoai/nanoclaw/issues/2525) / [#2526](https://github.com/nanocoai/nanoclaw/pull/2526) | `ncl groups delete` fails with foreign key constraint on non-trivial groups. Resolved via transactional cascade. |
| **Medium** | **Open/Unmerged** | [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) | Unknown slash commands wrongly classified as `passthrough`, resulting in silent message drops when the Agent SDK produces output without `<message>` blocks. |
| **Medium** | **Open/Unmerged** | [#2607](https://github.com/nanocoai/nanoclaw/pull/2607) | Inbound message actions fail due to use of internal composite IDs instead of platform raw message IDs. |

---

## 6. Feature Requests & Roadmap Signals

**🔮 Features in Active Development (Open PRs)**

- **[PR #2605 — Inherit parent agent permissions via OneCLI](https://github.com/nanocoai/nanoclaw/pull/2605)** *(Author: @guyb1)*
  Proposes permission inheritance from parent agents, indicating users are deploying deeply nested, hierarchical agent structures requiring delegated permission management.

- **[PR #2345 — Auto-import per-group CLAUDE.role.md](https://github.com/nanocoai/nanoclaw/pull/2345)** *(Author: @IamAdamJowett)*
  Extends the `claude-md-compose` skill to auto-import role definitions from group folders. Reflects demand for modular, composable agent identity configurations.

- **[PR #2609 — Apple Container: file mounts, host.docker.internal, user mapping](https://github.com/nanocoai/nanoclaw/pull/2609)** *(Author: @CashQ)*
  Addresses several Docker-on-Apple-Silicon pain points. Signals strong adoption among macOS developers and a need for first-class Docker Desktop integration.

**📈 Roadmap Predictions**

The next minor release will almost certainly include:
1. **Per-agent provider/model config** (#1968) — Headline feature.
2. **Admin batch activity endpoint** (#2604) — Unlocks real-time admin UIs.
3. **CLI group delete fix** (#2526) — Critical blocker for power users.

Subsequent releases will likely prioritize:
4. **Fix for `engage_mode='always'` routing bug** (#2606) — Too fundamental to leave open.
5. **Slash command fallback** (#2346) — Resolves a class of silent failures in chat.
6. **Platform ID standardization** (#2607) — Enables reliable platform integrations.

---

## 7. User Feedback Summary

**User Pain Points (from Issues/PRs)**

- **Non-trivial group management was broken**: Users running complex agent groups (with dependencies, usage history) were completely blocked from deleting them until today's fix (#2525). This is a hard blocker for anyone managing more than a flat group structure.
- **Core routing feature is non-functional**: Setting `engage_mode: 'always'` leads to completely silent message drops (#2606). This represents a fundamental configuration mismatch between the database schema and the runtime code, eroding user trust in documented features.
- **Silent failures on unknown input**: Unknown slash commands are silently dropped instead of falling back to normal chat, leading to confusing "dead input" experiences (#2346).
- **Integration friction**: Platform integration developers cannot reliably use message actions (reactions, edits) because IDs are incompatible (#2607).

**Use Cases Emerging from Contributions**
- **Admin dashboards**: The batch activity endpoint (#2604) points directly to real-world dashboard requirements for monitoring agent fleets.
- **Hierarchical permissions**: Permission inheritance (#2605) signals deployments beyond single-agent, moving toward enterprise-style role-based access.
- **Local/Dev macOS environments**: Container fixes (#2609) confirm a significant developer community running NanoClaw locally on Apple hardware.
- **Composable agents**: Per-group CLAUDE.role.md auto-import (#2345) suggests users want to compose agent behaviors from reusable group-level configurations.

**Satisfaction Indicators**
- High contributor trust: Regular contributors (@IamAdamJowett, @glifocat, @sumsumai) repeatedly shipping code.
- Rapid fix turnaround for critical bugs (#2525 → #2526 closed same day).
- Maintainers proactively addressing infrastructure debt (#2608).

---

## 8. Backlog Watch

| Item | Author | Age | Needs |
|---|---|---|---|
| [PR #2346 — fix(formatter): treat unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/pull/2346) | @SidhayaPravda618 | 17 days (Created May 8) | **Maintainer review/merge decision.** Fixes a latent bug causing silent message drops. Reviewed by CI but no maintainer sign-off yet. |
| [PR #2345 — feat(claude-md-compose): auto-import per-group CLAUDE.role.md](https://github.com/nanocoai/nanoclaw/pull/2345) | @IamAdamJowett | 17 days (Created May 8) | **Maintainer architectural decision.** The author noted this is borderline between a pure skill and a source-code change. Requires explicit approval from maintainers on the preferred approach. |

No other items in the current dataset appear critically stale, but these two PRs represent the most significant open work awaiting action from project maintainers beyond today's high-velocity merges.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-25

## 1. Today's Overview
The NullClaw project saw minimal activity on May 25, 2026. No new issues were opened or updated, and no releases were published. The sole piece of activity was an automated Dependabot pull request to update the `busybox` Docker base image. With zero human-initiated issues or discussions, the project appears to be in a stable, low-engagement maintenance phase. Routine dependency upgrades are being handled automatically, but there is no visible community development or feature work occurring today.

## 2. Releases
No new releases were published today.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours.

## 4. Community Hot Topics
- **[dependencies, docker] ci(deps): bump busybox from 1.37 to 1.38 in the docker-images group**  
  ([nullclaw/nullclaw PR #931](https://github.com/nullclaw/nullclaw/pull/931))  
  *Author: dependabot[bot] | Status: Open*
  
  This was the only activity on the project today. It bumps the `busybox` Docker image from version 1.37 to 1.38 across the Docker configuration files. The PR received no comments or reactions, indicating the update was automatically generated and has not yet been reviewed or merged.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project has no known open stability issues from today's data.

## 6. Feature Requests & Roadmap Signals
No user-submitted feature requests or roadmapping signals were present in the data. The day's activity was purely operational and automated.

## 7. User Feedback Summary
No explicit user feedback, pain points, or satisfaction indicators were observed in the daily activity stream.

## 8. Backlog Watch
No long-standing or unanswered issues or pull requests requiring maintainer attention are present in the provided data. The project's queue appears fully clean.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-25

## 1. Today's Overview
The IronClaw project continues to demonstrate **high development velocity**, particularly around the architectural **Reborn** migration, with 27 issues and 50 pull requests updated in the last 24 hours. Although no formal release was published today, 8 pull requests were merged, advancing Reborn auth contracts, channel ports, and developer tooling. Project health is tempered by several concurrent risk signals: a critical QA finding of a Discord channel causing sustained 100% CPU load ([#4030](https://github.com/nearai/ironclaw/issues/4030)), recurring nightly E2E failures ([#3447](https://github.com/nearai/ironclaw/issues/3447)), and a blocking publishing gap where downstream consumers remain pinned to an outdated 0.24.0 crates.io release ([#3259](https://github.com/nearai/ironclaw/issues/3259)). Maintainers are balancing heavy Reborn feature delivery with a growing security hardening push, most visibly around tool dispatch audit and credential injection safety.

## 2. Releases
**No new releases today.** The latest published crates.io version remains `0.24.0` (Mar 31, 2026), despite tags up to `ironclaw-v0.27.0`. The automated release PR ([#3708](https://github.com/nearai/ironclaw/pull/3708), open since May 16) is stalled due to an API-breaking change in `ironclaw_common` (enum variant discriminant shift) that blocks version advancement. Downstream consumers awaiting security fixes (Wasmtime 28.x CVEs) remain blocked until this pipeline is resolved.

## 3. Project Progress (Merged/Closed Today)
The primary driver of activity remains the **Reborn** architecture migration. Key items closed or merged in the reporting window:

**Reborn Architecture & Auth:**
- **Auth contracts and fake-service tests** — Step 1 closed ([#3810](https://github.com/nearai/ironclaw/issues/3810)).
- **Reborn-native auth/secrets composition** — Step 2 closed ([#3811](https://github.com/nearai/ironclaw/issues/3811)).
- **OAuth callback and setup continuations** — Step 3 closed ([#3812](https://github.com/nearai/ironclaw/issues/3812)).
- **ProductAdapter replacement contract** — Completed ([#3269](https://github.com/nearai/ironclaw/issues/3269)). This unblocks the session thread and TurnCoordinator tracks.

**Channel Ports & WebUI:**
- **Port WebUI to native Reborn surface** — Closed ([#3580](https://github.com/nearai/ironclaw/issues/3580)).
- **Port Slack to Reborn ProductAdapter** — Closed ([#3579](https://github.com/nearai/ironclaw/issues/3579)).
- **WebChat v2 timeline/event schema** — Closed ([#3614](https://github.com/nearai/ironclaw/issues/3614)).

**Security & Tooling:**
- **HTTP wired into Reborn local dev** — Merged ([#4018](https://github.com/nearai/ironclaw/pull/4018)).
- **Tool failure taxonomy review** — Addressed and merged ([#4020](https://github.com/nearai/ironclaw/pull/4020)), mapping `ResponseError` to `OperationFailed` for model-visible failures.
- **WeCom channel** — Merged ([#2394](https://github.com/nearai/ironclaw/pull/2394)), adding a standalone WeCom WASM channel.

**Dependency Maintenance:**
- Major bumps processed across the tokio ecosystem ([#4001](https://github.com/nearai/ironclaw/pull/4001)), Wasm tooling ([#3247](https://github.com/nearai/ironclaw/pull/3247), [#4032](https://github.com/nearai/ironclaw/pull/4032)), and general dependencies ([#4003](https://github.com/nearai/ironclaw/pull/4003)).

**In-Flight (Open PRs):**
- Subagent spawn Phases 2–4 ([#3869](https://github.com/nearai/ironclaw/pull/3869), [#3870](https://github.com/nearai/ironclaw/pull/3870), [#3872](https://github.com/nearai/ironclaw/pull/3872))
- Reborn OAuth route mounting ([#4031](https://github.com/nearai/ironclaw/pull/4031))
- Approval interaction service ([#4029](https://github.com/nearai/ironclaw/pull/4029))
- Secrets master key resolution ([#4013](https://github.com/nearai/ironclaw/pull/4013))
- Codex local yolo host access ([#4007](https://github.com/nearai/ironclaw/pull/4007))

## 4. Community Hot Topics
The most active issues reflect deep architectural and security concerns rather than casual usage friction:

**Most Active:**
- **#3259 — Publish 0.25.0–0.27.0 to crates.io** (9 comments). This is the single highest-priority blocker for the downstream community. Consumers are pinned to 0.24.0 by Wasmtime CVEs, and the release pipeline breaking change has created a week-long stall. The community is clearly awaiting resolution to update their dependencies.
- **#4017 — Interactive chat tool calls bypass ToolDispatcher** (3 comments). The discovery that interactive chats skip the audit trail and channel tool-filters resonated immediately, spawning a systemic fix proposal in [#4019](https://github.com/nearai/ironclaw/issues/4019).
- **#3702 — Revise binary-E2E test framework plan** (4 comments). This internal audit and restructuring issue has significant multiparty engagement, reflecting team alignment on test quality before the Reborn stabilization.

**Feature Requests with User Engagement:**
- **#4034 — Custom Telegram API Host** (0 comments, but a direct user feature request). The requester explicitly cites a self-hosted Telegram Bot API use case, indicating enterprise/private deployment interest.
- **#4030 — Discord channel 100% CPU** (0 comments but filed by an identified QA user with full reproduction steps). This is directly user-impacting.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|---|---|---|---|
| **Critical** | [#4030](https://github.com/nearai/ironclaw/issues/4030) | Discord WASM channel causes sustained 100% CPU rendering the instance unresponsive | No fix PR linked |
| **High** | [#3447](https://github.com/nearai/ironclaw/issues/3447) | Nightly E2E consistently failing (v2-engine job) | Recurring; commit 030cfeb0 |
| **High** | [#4017](https://github.com/nearai/ironclaw/issues/4017) | Interactive chat bypasses `ToolDispatcher::dispatch`, no `ActionRecord` audit, no channel tool-filter | Fix drafted in [#4019](https://github.com/nearai/ironclaw/issues/4019) |
| **Medium** | [#3917](https://github.com/nearai/ironclaw/issues/3917) | `RuntimeCredentialTarget::PathPlaceholder` introduced a leak risk (URL path segment injection) | Under security review; shipping blocked pending decision |
| **Low** | [#4027](https://github.com/nearai/ironclaw/issues/4027) | `cargo test` prompts for OS keychain access on macOS | Fix PR open ([#4027](https://github.com/nearai/ironclaw/pull/4027)) |

**Observation:** The Discord 100% CPU bug ([#4030](https://github.com/nearai/ironclaw/issues/4030)) is the most severe quality regression reported today, effectively breaking a core channel for users. Combined with the nightly E2E red, confidence in current trunk stability is lowered.

## 6. Feature Requests & Roadmap Signals

- **Custom Telegram API Host** ([#4034](https://github.com/nearai/ironclaw/issues/4034)): A user directly requests support for a custom API domain in the Telegram WASM channel, citing self-hosted Telegram Bot API servers. This is a clean, scoped feature that aligns with the "configurable channel infrastructure" pattern seen in the Reborn ports. Likely a P2 candidate for next release.
- **WeCom Channel** ([#2394](https://github.com/nearai/ironclaw/pull/2394)): Merged today. This adds a standalone Enterprise WeChat channel, expanding the protocol integration portfolio.
- **Codex Integration Velocity**: Multiple PRs ([#4007](https://github.com/nearai/ironclaw/pull/4007), [#4018](https://github.com/nearai/ironclaw/pull/4018)) indicate a deliberate push to expose Reborn capabilities through the Codex developer experience layer.
- **Reborn Approval UI**: The approval interaction service ([#4029](https://github.com/nearai/ironclaw/pull/4029)) and OAuth route mounting ([#4031](https://github.com/nearai/ironclaw/pull/4031)) signal the incoming WebUI beta is nearing interactive feature parity.

**Roadmap Prediction:** The next minor release (0.28.x) will likely include Reborn WebUI beta, Slack & WebUI ProductAdapter ports, subagent spawning, and the approval interaction service. However, this is contingent on breaking the crates.io publication logjam ([#3259](https://github.com/nearai/ironclaw/issues/3259)).

## 7. User Feedback Summary

**Pain Points:**
1. **Downstream Blocking**: The crates.io publishing gap ([#3259](https://github.com/nearai/ironclaw/issues/3259)) is the loudest user feedback signal. 9 comments confirm real downstream consumers are unable to consume security fixes (Wasmtime 28.x CVEs). One maintainer noted this explicitly: "consumers pulling from crates.io are pinned to 0.24.0."
2. **Channel Reliability**: The Discord 100% CPU bug ([#4030](https://github.com/nearai/ironclaw/issues/4030)) represents a severe degradation of a primary user interface. The QA report is detailed and actionable.
3. **Security Transparency**: The discovery that interactive chats bypass audit/security layers ([#4017](https://github.com/nearai/ironclaw/issues/4017)) surfaced user trust concerns about the existing security model.

**Satisfaction Signals:**
- The steady closure of Reborn migration issues (six issues closed today) suggests the team is methodically delivering on the promised architecture overhaul, which has been a long-running community and developer talking point.
- The WeCom channel merge signals responsiveness to enterprise Chinese market needs.

## 8. Backlog Watch

| Issue / PR | Age | Priority | Reason for Watch |
|---|---|---|---|
| [#3259](https://github.com/nearai/ironclaw/issues/3259) — Publish to crates.io | 20 days | **Highest** | Directly blocks all downstream consumers from receiving critical fixes. |
| [#3447](https://github.com/nearai/ironclaw/issues/3447) — Nightly E2E failures | 15 days | **High** | Accepting recurring CI red on trunk erodes release confidence. |
| [#3708](https://github.com/nearai/ironclaw/pull/3708) — Release PR blocked | 9 days | **High** | Stuck on breaking API change in `ironclaw_common`. Requires a maintainer decision on versioning strategy. |
| [#3917](https://github.com/nearai/ironclaw/issues/3917) — PathPlaceholder hardening | 2 days | **High** | Security review in progress; delaying a decision risks shipping a known credential leak vector. |
| [#3608](https://github.com/nearai/ironclaw/issues/3608) — Seal dispatch with AuthorizedDispatchRequest | 11 days | **High** | A core security invariant for Reborn. Open with no recent movement despite the #4017 bypass discovery. |
| [#3988](https://github.com/nearai/ironclaw/issues/3988) — Decompose 3k+ line capability port adapter | 1 day | **Medium** | Technical debt that will grow as new capabilities are added to the port adapter module. |

The most critical action item for maintainers is resolving the crates.io publication blocking issue ([#3259](https://github.com/nearai/ironclaw/issues/3259)), which has cascading effects on every downstream user and project. The release process appears to lack automated remediation for breaking detection—this is a process gap that should be addressed to prevent future stalls.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-25

---

## 1. Today's Overview

LobsterAI experienced a highly productive day, with **22 pull requests updated** and **14 merged or closed**, signaling strong feature finalization velocity. The core development focus centered on maturing the **subagent system** (full refactor of rendering, sidebar, and data tracking), deepening **OpenClaw ecosystem integration** (plugin sync and config compatibility fixes), and enhancing **model configuration flexibility** (custom parameters, context window controls). No new issues were created, but 8 long-standing stale items received simultaneous updates, indicating active maintainer backlog review. No new releases were tagged, but the volume of merged code strongly suggests a version release is imminent.

---

## 2. Releases

None. The project remains on its previously cut version.

---

## 3. Project Progress

The following major features and fixes were merged/closed today:

- **OpenClaw Plugin Sync** — PR [#2042](https://github.com/netease-youdao/LobsterAI/pull/2042) implements automatic plugin discovery and synchronization from the OpenClaw extension directory, bridging the user experience between the two platforms. Config cleanup in [#2026](https://github.com/netease-youdao/LobsterAI/pull/2026) removes unsupported Dreaming properties that previously caused gateway crashes on startup.

- **Subagent Feature Suite** — The subagent system reached a high degree of maturity:
  - Dedicated sidebar with tree-structured session browsing ([#2011](https://github.com/netease-youdao/LobsterAI/pull/2011))
  - Robust deduplication and missing tool results fix ([#2029](https://github.com/netease-youdao/LobsterAI/pull/2029))
  - Major architectural refactor to reuse the main conversation rendering pipeline ([#2030](https://github.com/netease-youdao/LobsterAI/pull/2030))
  - UI polish including sidebar toggle, draggable header, and Mac padding ([#2027](https://github.com/netease-youdao/LobsterAI/pull/2027))

- **Model Configuration Overhaul** — Users now have fine-grained control:
  - New context window slider with smart snap-to-presets (32K/64K/200K/1M/2M) and K/M input support ([#2013](https://github.com/netease-youdao/LobsterAI/pull/2013))
  - Per-model custom parameters for arbitrary `extra_body` (e.g., `thinking` block) with streaming support ([#2019](https://github.com/netease-youdao/LobsterAI/pull/2019))
  - Backend `contextWindow` field support for package models ([#2021](https://github.com/netease-youdao/LobsterAI/pull/2021))

- **Stability & Platform Fixes** — A critical cross-DPI multi-monitor window sizing bug on Windows was fixed ([#2020](https://github.com/netease-youdao/LobsterAI/pull/2020)). Agent ID generation was migrated from name-based to short UUIDs to prevent data resurrection bugs ([#1584](https://github.com/netease-youdao/LobsterAI/pull/1584)).

---

## 4. Community Hot Topics

Although no new issues were raised, long-standing community pain points are now actively being resolved.

- **Underlying Need: Reliable Automation** — User `MaoQianTu` continues to drive quality improvements, reporting critical gaps in scheduled task IM notification delivery ([#1510](https://github.com/netease-youdao/LobsterAI/issues/1510)) and a missing QQ Bot group whitelist UI ([#1514](https://github.com/netease-youdao/LobsterAI/issues/1514)). These highlight the community's demand for LobsterAI to act as a fully reliable autonomous agent platform.

- **Underlying Need: Model Management Simplicity** — The dynamic model list fetching PR [#1522](https://github.com/netease-youdao/LobsterAI/pull/1522) reflects user frustration with manually tracking the rapidly evolving LLM landscape (e.g., new GLM versions). The community wants automated discovery rather than hardcoded defaults.

- **Underlying Need: Workbench Organization** — The session color labels feature ([#1526](https://github.com/netease-youdao/LobsterAI/issues/1526)) and full subagent sidebar ([#2011](https://github.com/netease-youdao/LobsterAI/pull/2011)) signal a maturing user base that needs visual structure as conversation surfaces and agent counts grow.

---

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **Critical** | OpenClaw gateway crash from unsupported Dreaming config properties | **Fixed** in [#2026](https://github.com/netease-youdao/LobsterAI/pull/2026) | Caused immediate startup failure when `model`/`timezone` were present. |
| **High** | Log export timeout (30s) on large logs due to serial DEFLATE | **Fixed** in [#1515](https://github.com/netease-youdao/LobsterAI/pull/1515) | Optimized compression to avoid exceeding the timeout limit. |
| **High** | Window renders at 25% size on secondary monitors with mixed DPI | **Fixed** in [#2020](https://github.com/netease-youdao/LobsterAI/pull/2020) | Root cause: `frame:false` dimensions divided by primary monitor scale factor. |
| **High** | Agent data resurrection on delete/recreate with same name | **Fixed** in [#1584](https://github.com/netease-youdao/LobsterAI/pull/1584) | Unused data (workspace, sessions) leaked into new agents. |
| **Medium** | Copilot OAuth token silently lost when Settings panel closed during polling | **Open** ([#1517](https://github.com/netease-youdao/LobsterAI/issues/1517)) | `cancelPolling()` never called on component unmount. Fix proposed. |
| **Medium** | Scheduled task IM notifications fire silently with empty `delivery.to` | **Open** ([#1510](https://github.com/netease-youdao/LobsterAI/issues/1510)) | Validating presence of `notifyTo` before submit is needed. Fix proposed. |
| **Low** | Spurious gateway restart on OpenClaw skills change | **Open** ([#1521](https://github.com/netease-youdao/LobsterAI/pull/1521)) | Fix proposed to debounce or filter the `skills-changed` event. |

---

## 6. Feature Requests & Roadmap Signals

The day's merged PRs provide strong signals for the project's trajectory:

- **Thinking Block Display (Reasoning Models)** — PR [#2019](https://github.com/netease-youdao/LobsterAI/pull/2019) adds first-class support for displaying model reasoning/thinking traces in a dedicated message block. **Prediction**: This will be a headline feature in the next release, positioning LobsterAI for the coming wave of reasoning-first LLMs (o3, Gemini Thinking, Claude 3.7 Sonnet).

- **Plugin Ecosystem Strategy** — The OpenClaw plugin sync ([#2042](https://github.com/netease-youdao/LobsterAI/pull/2042)) formalizes LobsterAI as a "plug-in" to the broader OpenClaw agent standard. **Prediction**: Expect tighter bidirectional sync and an OpenClaw Store integration in the subsequent release.

- **Power-User Flexibility** — Custom model params, context window controls, and dynamic model list fetching all point to supporting advanced users who run frontier models. **Prediction**: This positions LobsterAI as the go-to desktop frontend for AI researchers and power users specifically.

- **Subagent Productionization** — The full rendering pipeline refactor ([#2030](https://github.com/netease-youdao/LobsterAI/pull/2030)) signals subagents are close to leaving beta. **Prediction**: Subagent workflows (parallel routing, handoffs) will be the next major feature area.

---

## 7. User Feedback Summary

- **High Satisfaction Drivers**: The rapid merging of long-standing bugs (log export timeout, agent ID resurrection, window sizing) demonstrates strong maintainer responsiveness to community-reported pain points.

- **Key Contributor**: User `MaoQianTu` continues to be an invaluable source of high-quality bug reports (scheduled tasks, QQ bot UI, OAuth polling) that directly improve core reliability. This user's work suggests LobsterAI has a dedicated power-user community ensuring quality.

- **Persistent Dissatisfaction**: Users relying on QQ Bot group whitelisting and scheduled task IM notifications have experienced broken UI components and silent failures for over 48 days, awaiting final resolution of proposed fixes. Dynamic model list fetching was also a long-standing request (48 days open) before being addressed.

---

## 8. Backlog Watch

A simultaneous update sweep occurred today across 8 stale items (all created 2026-04-07, updated 2026-05-25). While the activity signals awareness, these items remain open and require resolution:

| Item | Type | Age | Urgency |
|------|------|-----|---------|
| [#1510](https://github.com/netease-youdao/LobsterAI/issues/1510) — Scheduled task IM silent failure | Issue | 48 days | **High** — Data loss / user frustration |
| [#1514](https://github.com/netease-youdao/LobsterAI/issues/1514) — QQ Bot whitelist UI missing | Issue | 48 days | **Medium** — Feature broken |
| [#1517](https://github.com/netease-youdao/LobsterAI/issues/1517) — Copilot OAuth token leak | Issue | 48 days | **High** — Security / reliability |
| [#1521](https://github.com/netease-youdao/LobsterAI/pull/1521) — Spurious gateway restart on skill change | PR | 48 days | **Medium** — Operational noise |
| [#1522](https://github.com/netease-youdao/LobsterAI/issues/1522) — Dynamic model list fetching | Issue | 48 days | **Medium** — Quality of life (fix merged today!) |
| [#1524](https://github.com/netease-youdao/LobsterAI/issues/1524) — Connection test error detail | Issue | 48 days | **Low** — UX improvement |
| [#1526](https://github.com/netease-youdao/LobsterAI/issues/1526) — Session color labels | Issue | 48 days | **Low** — Enhancement (fix merged today!) |
| [#1515](https://github.com/netease-youdao/LobsterAI/issues/1515) — Log export timeout | Issue | 48 days | **Medium** — Bug (fix merged today!) |

**Recommendation**: Maintainers should prioritize merging the unmerged proposed fixes, particularly the Copilot OAuth leak ([#1517](https://github.com/netease-youdao/LobsterAI/issues/1517)) and the QQ Bot UI regression ([#1514](https://github.com/netease-youdao/LobsterAI/issues/1514)), to clear the stale backlog ahead of the anticipated upcoming release.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest based on the provided GitHub activity data.

---

# Moltis Project Digest — 2026-05-25

## 1. Today’s Overview

Moltis exhibited exceptionally high maintainer velocity today, closing **8 issues** and merging **10 pull requests** within a single 24-hour window. The activity focus was sharply divided between hardening the codebase (security patches, UI bug fixes, log cleanup) and advancing the architectural strategy (agent-centric capability boundaries). While no new release was tagged, the sheer volume and depth of merged work indicates an imminent or batched release candidate is building. Maintainer `penso` drove the vast majority of changes, signaling strong and centralized project stewardship during this sprint.

## 2. Releases

**None.** No new releases were published today. Given the density of the merged work—especially the architectural refactor in PR #1049 (`moltis-org/moltis PR #1049`) and the immediate closure of multiple high-severity bugs—users should watch closely for an imminent release or pull the latest from `main` to take advantage of these improvements.

## 3. Project Progress

All ten pull requests merged today advanced the project's stability and architecture significantly:

- **Agent-Centric Architecture (PR #1049):** Merged a foundational feature that makes agents the core capability boundary. Each agent preset now controls its model, MCP servers, sandbox policy, and skills. This design enables agents to be assigned to specific channels for different user contexts.
  [moltis-org/moltis PR #1049]

- **Per-Agent Runtime Limits (PR #1066):** Resolves the long-standing feature request to allow individual configuration of `timeout_secs` and `max_iterations` per agent preset, with cascading fallbacks to tool-level configs.
  [moltis-org/moltis PR #1066]

- **Onboarding UX (PR #1058):** Improves the new-user setup flow by displaying already-configured LLM providers in the "Recommended" list rather than burying them in the collapsed "All providers" section.
  [moltis-org/moltis PR #1058]

- **External Agent Management (PR #1059):** Prevents the external agent picker drop-down from rendering disabled options when `external_agents.enabled` is explicitly set to `false`, correcting a confusing configuration inconsistency.
  [moltis-org/moltis PR #1059]

- **Stability & Quality-of-Life Fixes:** The remaining PRs (#1058–#1065) directly addressed bug reports filed within the same period, covering sandbox log verbosity, provider URL validation, secret management, model picker rendering, session title generation, and UI overflow (detailed below).

## 4. Community Hot Topics

Community discussion volume was low, but the topics were high-impact:

- **Feature Request Closure (Issue #553):** The most significant community interaction point was the closure of Issue #553 (`moltis-org/moltis Issue #553`), submitted by `bsarkisov` in early April. Although it had only one comment, its resolution via PR #1066 validates a month-old request for granular per-agent controls. This demonstrates that the maintainers are methodically working through the feature backlog.

- **Security Awareness (Issue #1054):** While it generated zero comments, the surrounding silence likely reflects the seriousness of the bug: environment variable secrets from stdio MCP server configs were being leaked to the LLM via `mcp_list`. The swift, same-day fix sent a strong signal of security responsiveness to the user base.

No other issues or PRs attracted discussion comments, suggesting the userbase is engaged primarily through bug reports rather than open debate, or that the rapid fix turnaround obviates extended conversation.

## 5. Bugs & Stability

Today represented a major stability push. **Every bug filed in the 24-hour window was closed via a fix PR on the same day.** Ranked by severity:

- **Critical (Security)**
  - **Issue #1054** — Env vars from stdio MCP server config exposed to LLM via `mcp_list`.
    *Fix:* **PR #1063** (`moltis-org/moltis PR #1063`). Values are now stored as `Secret<String>` through the entire config/registry pipeline; the status/list API returns only variable names. **Merged and closed.**

- **High (Validation / Error Handling)**
  - **Issue #1051** — OpenAI-compatible provider `baseUrl` not validated; constructed URL not logged on failure.
    *Fix:* **PR #1061** (`moltis-org/moltis PR #1061`). Rejects endpoints containing `/chat/completions` or `/responses` and surfaces the constructed URL in probe logs. **Merged and closed.**
  - **Issue #1053** — Automatic session title generation silently fails, returning `label: null` without notification.
    *Fix:* **PR #1064** (`moltis-org/moltis PR #1064`). Failures are now propagated through RPC and channel commands, and the working model ID is persisted for fallback. **Merged and closed.**

- **Medium (UI/UX)**
  - **Issue #1052** — Model picker does not accommodate long gateway model version IDs.
    *Fix:* **PR #1060** (`moltis-org/moltis PR #1060`). Picker is now responsively wider, with full-model-name tooltips on rows and the selected chip. **Merged and closed.**
  - **Issue #1055** — Horizontal scrolling in chat sessions (regression) caused by the chat toolbar.
    *Fix:* **PR #1062** (`moltis-org/moltis PR #1062`). Toolbar is constrained to prevent widening the chat pane. **Merged and closed.**
  - **Issue #1057** — External agent picker renders agents even when the feature is disabled.
    *Fix:* **PR #1059** (see Section 3). Returns empty list when disabled. **Merged and closed.**

- **Low (Developer Experience)**
  - **Issue #1056** — Sandbox image pre-build logs dump full Docker build output to console at `warn!` level.
    *Fix:* **PR #1065** (`moltis-org/moltis PR #1065`). Cache skips are logged at debug; full build output is kept at debug with concise failure summaries surfaced as warnings. **Merged and closed.**

## 6. Feature Requests & Roadmap Signals

Today’s activity provides clear roadmap signals:

- **Per-Agent Runtime Limits (Issue #553):** The closure of this request answers a specific community need for fine-grained control over agent execution. It fits neatly into the larger agent-boundary architecture.
  [moltis-org/moltis Issue #553]

- **Agents as Capability Boundaries (PR #1049):** This is the strongest strategic signal. By making agents the unit of configuration for models, MCP servers, sandboxes, and skills, Moltis is laying the groundwork for multi-user, role-based, and context-aware deployments (e.g., separate profiles for "kids" vs. "parents").
  [moltis-org/moltis PR #1049]

- **Prediction for Next Release:** Given the batch volume, the upcoming release will likely formalize the expanded `agents.presets.<id>` schema as the primary configuration paradigm, shipping alongside the security hardening and UX polish merged today. The onboarding improvements (PR #1058) suggest a continued investment in lowering the barrier to entry for new users.

## 7. User Feedback Summary

User input today came overwhelmingly in the form of precise, actionable bug reports rather than open-ended praise or feature requests. The underlying pain points and satisfaction drivers were:

- **Pain Points Resolved:**
  - *Security Anxiety:* Leaked MCP secrets (Issue #1054) and silent validation failures (Issue #1051) were top-of-mind for privacy-conscious and power users.
  - *Developer Experience Friction:* Verbose sandbox logs (Issue #1056) were interfering with console clarity during troubleshooting.
  - *UI/Usability Friction:* Model selection in overflow (Issue #1052), persistent horizontal scroll (Issue #1055), and a misleading external agent menu (Issue #1057) all degraded the daily workflow.

- **Satisfaction Indicators:**
  - The turnaround time is the strongest satisfaction signal. Every pain point filed on May 23–24 was patched by May 24. This rapid fix cadence builds high user trust.
  - The closure of Issue #553 (filed April 4, closed May 24) proves that older feature requests are not abandoned, even if they take time to rise to the top of the priority stack.

- **No direct positive feedback** (e.g., "this is great") was captured in the issue or PR comments, but the lack of follow-up or frustration on the closed items implies acceptance of the solutions.

## 8. Backlog Watch

The current snapshot shows **zero active open issues or pull requests** in the update window. While this is an unusual state for a complex project, it reflects a deliberate batch-cleanup session by the maintainers rather than an absence of work.

- **Lingering Latency Signal:** Issue #553 was open for **50 days** (April 4 to May 24) before being resolved. This serves as a data point on the project's overall queue depth. If the rate of incoming requests increases, the maintainers may need to establish a triage response SLA or formalize a release cadence to manage community expectations.
- **No blocking items or stalled community PRs** were detected in the data. The project’s maintenance health is currently very strong.
- **Watch for:** The `agents` schema stabilization from PR #1049 is likely to generate follow-up documentation issues and edge-case bug reports once a wider user base tests the new boundaries.

---

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for **2026-05-25** based on the QwenPaw project activity (agentscope-ai/CoPaw ecosystem).

---

### 1. Today's Overview
The QwenPaw project saw very high activity on 2026-05-25, with **27 Issues** and **37 Pull Requests** updated. Significant progress was made on stability and quality assurance, closing 13 issues and merging 24 PRs. A strong community contributor batch focused heavily on expanding test coverage across core modules including config, providers, and utilities. While no new releases were cut today, several major features are actively under review, including a full in-browser Coding Mode, a DataPaw analytics plugin, and Tauri 2.x desktop app support, signaling an exciting roadmap ahead. Overall project health is strong, with maintainers actively addressing regressions reported against the recent **v1.1.8.post1** release.

### 2. Releases
No new releases were published on this date. The most recent version remains **v1.1.8.post1**.

### 3. Project Progress
The project made excellent strides in hardening code quality and fixing rendering issues.

- **Robust Testing Foundation:** A significant uptick in code quality is evident thanks to the merges of extensive test coverage PRs by contributor `aqilaziz`. Specific areas now locked down with unit tests include:
    - Config utilities and timezone detection ([PR #4405](https://github.com/agentscope-ai/QwenPaw/pull/4405), [#4404](https://github.com/agentscope-ai/QwenPaw/pull/4404))
    - Environment variable persistence and encrypted storage ([PR #4393](https://github.com/agentscope-ai/QwenPaw/pull/4393), [#4374](https://github.com/agentscope-ai/QwenPaw/pull/4374))
    - Telemetry helper functions ([PR #4373](https://github.com/agentscope-ai/QwenPaw/pull/4373), [#4392](https://github.com/agentscope-ai/QwenPaw/pull/4392))
    - Provider capability baseline helper ([PR #4403](https://github.com/agentscope-ai/QwenPaw/pull/4403))
    - DingTalk channel quoted message parsing ([PR #4390](https://github.com/agentscope-ai/QwenPaw/pull/4390))

- **UI and Rendering Fixes:**
    - **Markdown Table Line Breaks:** A fix was merged ([PR #4379](https://github.com/agentscope-ai/QwenPaw/pull/4379)) addressing the long-standing community complaint ([Issue #4497](https://github.com/agentscope-ai/QwenPaw/issues/4497)) about `<br>` tags not rendering inside tables.
    - **Think Tags Parsing:** Raw `<think>` tags from providers are now properly structured into collapsible reasoning blocks ([PR #4364](https://github.com/agentscope-ai/QwenPaw/pull/4364)).
    - **Dark Mode UI:** The Pet import drop-zone styling was fixed for dark mode ([PR #4599](https://github.com/agentscope-ai/QwenPaw/pull/4599)).
- **Documentation:** Quickstart guides now include `uv tool install` as a recommended installation method ([PR #4391](https://github.com/agentscope-ai/QwenPaw/pull/4391), [Issue #827](https://github.com/agentscope-ai/QwenPaw/issues/827)).

### 4. Community Hot Topics
The most active discussions this period revolve around critical UX bugs and ecosystem expansion.

- **"Chat history disappeared" ([Issue #4620](https://github.com/agentscope-ai/QwenPaw/issues/4620))**: This critical bug saw the highest engagement with **12 comments**. Users reported losing all context when switching sessions, described as a "critical bug and existed for a long time." The issue has since been closed.
- **"Console UI: tool calls often not displayed" ([Issue #4644](https://github.com/agentscope-ai/QwenPaw/issues/4644))**: This open bug has **9 comments**. Users report that tool calls are invisible in the web console until a manual page refresh, with no errors logged. This severely impacts the "agent transparency" experience.
- **DataPax Analysis Plugin ([PR #4622](https://github.com/agentscope-ai/QwenPaw/pull/4622))**: Community contributor EliasMei submitted this plugin adding 12 BI skills. This is a strong signal for the expanding plugin ecosystem and was a "first-time-contributor" PR.
- **Cron / Session Sharing Bugs ([Issue #4649](https://github.com/agentscope-ai/QwenPaw/issues/4649), [#4653](https://github.com/agentscope-ai/QwenPaw/issues/4653))**: Several users are hitting significant reliability issues with scheduled tasks, where tasks cancel each other or orphaned processes persist.

### 5. Bugs & Stability
Stability remains a top focus today, with several regressions reported against the latest release.

- **High Severity:**
    - **Config Loss on Session Creation ([Issue #4666](https://github.com/agentscope-ai/QwenPaw/issues/4666))**: Creating a new session can cause all Model configurations to display "Load failed," requiring a full application restart. *Status:* Open.
    - **Cron Task Interruption ([Issue #4653](https://github.com/agentscope-ai/QwenPaw/issues/4653))**: Scheduled tasks share a session with user messages—if a user sends a message while a cron job runs, the job is silently aborted. *Status:* Open.
    - **Orphaned Cron Processes ([Issue #4649](https://github.com/agentscope-ai/QwenPaw/issues/4649))**: Removing entries from `jobs.json` does not clean up the APScheduler state, causing "ghost tasks" to execute indefinitely. *Status:* Open.

- **Medium Severity:**
    - **Startup Time ([Issue #4664](https://github.com/agentscope-ai/QwenPaw/issues/4664))**: v1.1.8 takes ~40 seconds to start on Windows with no splash screen, creating a poor cold-start experience.
    - **Context Window Config Regression ([Issue #4661](https://github.com/agentscope-ai/QwenPaw/issues/4661), Closed)**: Upgrading to v1.1.8.post1 reset the global context window setting.
    - **OpenCode Model Filtering ([Issue #4656](https://github.com/agentscope-ai/QwenPaw/issues/4656))**: The provider model list shows models from all endpoints (Zen/Go), leading to API errors. A fix ([PR #4660](https://github.com/agentscope-ai/QwenPaw/pull/4660)) is Under Review.

### 6. Feature Requests & Roadmap Signals
The feature landscape suggests a major release (v1.2.x) is taking shape.

- **Likely to Ship in Next Release:**
    - **Coding Mode ([PR #4578](https://github.com/agentscope-ai/QwenPaw/pull/4578))**: An in-browser VS Code-like IDE embedded in the chat panel with Git integration. This is a massive differentiator.
    - **Token Usage Display ([PR #4433](https://github.com/agentscope-ai/QwenPaw/pull/4433) / [Issue #4647](https://github.com/agentscope-ai/QwenPaw/issues/4647))**: Heavy demand for visible token speed/cost metrics per conversation. The PR is Under Review.
    - **Mac OS File Path Whitelist ([PR #4267](https://github.com/agentscope-ai/QwenPaw/pull/4267))**: A significant security enhancement using `sandbox-exec`, awaiting final review.

- **Deep Community Wish List:**
    - **Intelligent Memory System ([Issue #4652](https://github.com/agentscope-ai/QwenPaw/issues/4652))**: A detailed proposal asking for a "summarize, correlate, remind" logic to prevent the agent from repeating mistakes, with state management and cross-dimension indexing.
    - **QwenPaw Pet Remote Connection ([Issue #4645](https://github.com/agentscope-ai/QwenPaw/issues/4645))**: Users want the desktop companion app to interact with a remote daemon/server.
    - **Message Timestamps ([Issue #4662](https://github.com/agentscope-ai/QwenPaw/issues/4662))**: A request to display precise timestamps on messages in the Web Console.

### 7. User Feedback Summary
- **Top Pain Points:**
    - **Configuration Fragility:** Multiple reports highlight that upgrading or performing simple actions like creating a session breaks configurations. One user explicitly noted the "global context length" setting vanished after an upgrade ([Issue #4661](https://github.com/agentscope-ai/QwenPaw/issues/4661)).
    - **Agent Invisibility:** The console UI bug where tool calls and reasoning content (for non-standard models like GLM-5.1) do not display makes the agent seem slow or unresponsive ([Issue #4644](https://github.com/agentscope-ai/QwenPaw/issues/4644), [#4650](https://github.com/agentscope-ai/QwenPaw/issues/4650)).
    - **Integration Friction:** Issues with DingTalk webhooks, Anthropic API compatibility, and Whisper provider bypass show that integration setup can be fragile.
- **Satisfaction Signals:** The highly detailed and constructive feature requests (e.g., Memory System, Timestamps) suggest an advanced user base deeply invested in the project. The active submission of high-quality plugins and test coverage indicates a healthy and committed open-source community.

### 8. Backlog Watch
- **Tauri 2.x Desktop ([PR #3813](https://github.com/agentscope-ai/QwenPaw/pull/3813))**: Open and "Under Review" since **April 24**. This is a major architecture shift for the desktop client that requires careful maintainer bandwidth to merge.
- **Mac OS Path Whitelist ([PR #4267](https://github.com/agentscope-ai/QwenPaw/pull/4267))**: "Under Review" since **May 13**. Security-focused PRs take longer, but this is crucial for power users.
- **UI Inconsistencies ([Issue #4631](https://github.com/agentscope-ai/QwenPaw/issues/4631), [#4659](https://github.com/agentscope-ai/QwenPaw/issues/4659))**: Minor UI bugs (Python icon in title bar, empty returns) were opened recently and have only initial interactions. They risk being deprioritized without assignees.
- **QwenPaw Pet Remote Mode ([Issue #4645](https://github.com/agentscope-ai/QwenPaw/issues/4645))**: Open since **May 23** with no maintainer response yet. As a feature request with a clear use case, it is worthy of a roadmap triage label.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the daily ZeroClaw project digest for 2026-05-25.

---

## ZeroClaw Project Digest — 2026-05-25

### 1. Today's Overview
ZeroClaw is in a period of exceptionally high development velocity, with **50 Issues** and **50 Pull Requests** updated in the last 24 hours. No new release was cut today, but the project is clearly in an active build-up phase, likely targeting a subsequent `0.80-beta1` release. The community remains deeply engaged, pushing forward major channel integrations, surfacing sharp edges in MCP tooling, and demanding resolution on long-standing S1 stability bugs.

### 2. Releases
No new releases were published today.

### 3. Project Progress
Today saw **8 PRs merged or closed**, moving the project forward across several components:

- **Channel Expansion (Lark/Feishu):** `[PR #6851](zeroclaw-labs/zeroclaw PR #6851)` and `[PR #6852](zeroclaw-labs/zeroclaw PR #6852)` by kanmars landed, respectively adding cron delivery support and the `request_approval()` function for the Lark channel, bringing it to feature parity with other major backends.
- **Configuration Fixes:** `[PR #6753](zeroclaw-labs/zeroclaw PR #6753)` by arucil resolved a critical UX bug where the Deepseek provider hardcoded its API base URL, ignoring user configuration.
- **Build Infrastructure:** `[PR #6866](zeroclaw-labs/zeroclaw PR #6866)` by NiuBlibing landed a substantial build system improvement, introducing a `default-channels` feature bundle to allow selective channel compilation.
- **Bug Closure:** The Telegram image message precheck stall (`[#6912](zeroclaw-labs/zeroclaw Issue #6912)`) was resolved and closed.

### 4. Community Hot Topics
The most active tickets reveal a community pushing for governance improvements, robust extensibility, and richer interaction modes:

- **Governance RFC (#6808):** Audacity88’s RFC on *Work Lanes, Board Automation, and Label Cleanup* (6 comments) generated the most discussion. This proposal targets the project’s own process overhead, signaling a need to formalize the contribution pipeline as the community scales.
- **MCP Integration Pain (#6699):** The most active bug report details that `tool_filter_groups` is entirely a no-op for real MCP tools (6 comments). This is a critical frustration for users relying on the MCP ecosystem.
- **Large Feature Pull Requests:** Several “XL”-sized PRs are drawing intense scrutiny:
    - `[PR #6848](zeroclaw-labs/zeroclaw PR #6848)` — Integration of a full Terminal UI.
    - `[PR #6893](zeroclaw-labs/zeroclaw PR #6893)` — Multi-database session backends (Postgres, MySQL, Oracle) for enterprise fleets.
    - `[PR #6665](zeroclaw-labs/zeroclaw PR #6665)` — The new `channel_send` tool, directly addressing the long-standing request for proactive agent messaging (cron output, alerts).

### 5. Bugs & Stability
The tracker remains heavily loaded with critical issues affecting reliability:

- **Critical (S1 — Workflow Blocked):**
    - `[#6302](zeroclaw-labs/zeroclaw Issue #6302)` — Gemini 400 errors due to strict history ordering.
    - `[#6472](zeroclaw-labs/zeroclaw Issue #6472)` — Gateway panic when Postgres session backend is used.
    - `[#5903](zeroclaw-labs/zeroclaw Issue #5903)` — MCP stdio child processes leak indefinitely on daemon heartbeat ticks.
    - `[#6841](zeroclaw-labs/zeroclaw Issue #6841)` — `vision_provider` config is silently ignored, causing fallback misrouting.
- **High Impact (S2 — Degraded Behavior):**
    - `[#6856](zeroclaw-labs/zeroclaw Issue #6856)` — `show_tool_calls` configuration field is missing from the v3 channel schema.
    - `[#6722](zeroclaw-labs/zeroclaw Issue #6722)` / `[#6723](zeroclaw-labs/zeroclaw Issue #6723)` — Config fields for Memory reranking and OpenAI timeouts are parsed but ignored at runtime.
    - `[#5810](zeroclaw-labs/zeroclaw Issue #5810)` — `security.otp.gated_actions` silently accepts invalid action names, providing a false sense of security.
- **Active Fixes in Pipeline:** `[PR #6911](zeroclaw-labs/zeroclaw PR #6911)` resolves runtime profile budgets for security policies. `[PR #6910](zeroclaw-labs/zeroclaw PR #6910)` prevents shell command hangs on Windows. `[PR #6885](zeroclaw-labs/zeroclaw PR #6885)` fixes an unauthenticated WebSocket gateway access path.

### 6. Feature Requests & Roadmap Signals
The feature landscape is dominated by multi-channel expansion and core architecture hardening.

- **Universal Messaging:** A flood of channel proposals indicates the community wants ZeroClaw to function as an agentic message hub. Top requests include **Mastodon** (`[#6423](zeroclaw-labs/zeroclaw Issue #6423)`), **Twilio SMS** (`[#6427](zeroclaw-labs/zeroclaw Issue #6427)`), **Rocket.Chat** (`[#6435](zeroclaw-labs/zeroclaw Issue #6435)`), and **Zulip** (`[#6437](zeroclaw-labs/zeroclaw Issue #6437)`).
- **Provider Diversity:** `[#6456](zeroclaw-labs/zeroclaw Issue #6456)` proposes support for Arcee AI’s specialist models. `[#4647](zeroclaw-labs/zeroclaw Issue #4647)` requests provider-scoped model fallback chains to manage multi-provider resilience.
- **Memory & Runtime Refactoring:** `[PR #6907](zeroclaw-labs/zeroclaw PR #6907)` introduces a `MemoryStrategy` trait to decouple lifecycle policy from low-level CRUD. `[#4760](zeroclaw-labs/zeroclaw Issue #4760)` pushes for tool-calling structured output for memory consolidation.
- **Prediction for Next Version:** Based on PR velocity, the next stable release will likely include the **MemoryStrategy refactor**, the **`channel_send` tool**, the **multi-database session backend**, and **several new channel backends** currently in the `status:in-progress` pipeline.

### 7. User Feedback Summary
- **Pain Points:**
    - **MCP Sharp Edges:** Users are repeatedly hitting complex bugs around tool filtering, deferred loading approval, and child process leakage.
    - **Provider Configuration Drift:** Significant frustration is directed at providers (Deepseek, OpenAI, Gemini) that do not honor documented configuration fields.
    - **Cron & Notification Gaps:** The inability to route cron job results to configured channels (`[#6647](zeroclaw-labs/zeroclaw Issue #6647)`) is a consistently reported blocker for production use.
- **Satisfaction Indicators:**
    - The community is highly responsive and constructive. Contributors like `theonlyhennygod`, `mn13`, `perlowja`, and `kanmars` are repeatedly delivering significant features.
    - The RFC process (`[#6808](zeroclaw-labs/zeroclaw Issue #6808)`) shows a user base invested in the long-term governance and technical debt management of the project.

### 8. Backlog Watch
Several critical, long-standing items require immediate maintainer attention:

- **Security Blind Spots:**
    - `[#5122](zeroclaw-labs/zeroclaw Issue #5122)` (Since March 29) — The `web_fetch` `allowed_private_hosts` list is effectively bypassed for domains resolving to private IPs.
    - `[#5810](zeroclaw-labs/zeroclaw Issue #5810)` (Since April 16) — OTP gate silently fails to validate action names.
- **Code Governance:**
    - `[#6074](zeroclaw-labs/zeroclaw Issue #6074)` (Since April 24) — The audit to track and recover 153 commits lost in a single bulk revert remains unresolved. This is a critical documentation gap for code provenance.
- **Core Reliability:**
    - `[#5903](zeroclaw-labs/zeroclaw Issue #5903)` (Since April 19) — The MCP stdio child process leak is a major operational issue for daemon users.
    - `[#4721](zeroclaw-labs/zeroclaw Issue #4721)` (Since March 26) — The simple request to log to stderr rather than stdout remains unaddressed, causing consistent CLI friction.
- **Dangling Large PRs:** The TUI integration (`[#6848](zeroclaw-labs/zeroclaw PR #6848)`), multi-database backend (`[#6893](zeroclaw-labs/zeroclaw PR #6893)`), and email channel fixes (`[#6512](zeroclaw-labs/zeroclaw PR #6512)`) are consuming significant review bandwidth and risk blocking the resolution of smaller pending bugs.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*