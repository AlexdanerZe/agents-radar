# OpenClaw Ecosystem Digest 2026-05-30

> Issues: 330 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-30 02:47 UTC

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

# OpenClaw Project Digest — 2026-05-30

## 1. Today's Overview

OpenClaw is in an intense stabilization cycle following the v2026.5.27–.28 beta rollout. **330 issues** and **500 PRs** were updated in the last 24 hours, and **4 immediate beta releases** (v2026.5.28-beta.1 through -beta.4) were cut to address emergent regressions. The dominant theme is the **Codex runtime** and **event-loop reliability**: the project is clearly firefighting a wave of session-state corruption, provider routing mismatches, and stability regressions introduced in recent days. While fix velocity is extremely high—165 PRs were merged or closed—the volume of critical "platinum hermit" and "diamond lobster" bugs indicates the platform is currently fragile for multi-agent and multi-channel production deployments.

---

## 2. Releases

**Four rapid releases today, all focused on runtime hardening:**

| Release | Summary |
|---|---|
| v2026.5.28-beta.1 | Codex/app-server runtime recovery stabilization — cwd/workspace separation, prompt-local hooks, session lock release on timeout abort, stale restart continuations avoided. |
| v2026.5.28-beta.2 | Identical highlight summary; incremental bug fixes in the same area. |
| v2026.5.28-beta.3 | Further runtime recovery hardening. |
| v2026.5.28-beta.4 | Polished version of the above. |

**Key Fixes across all four releases:**
- Subagents now reliably keep `cwd`/workspace separation.
- Hook context remains prompt-local (not leaking across turns).
- Session locks are released cleanly on timeout aborts.
- Stale restart continuations are avoided.
- Codex app-server/helper failures no longer tear down shared runtime state.

**⚠️ Migration Caution:** Given the critical `doctor --fix` regression documented in **#84038**, users should backup their `openclaw.yaml` and session state before applying these betas. These releases do not appear to contain breaking API changes, but the fix velocity means configuration internals are in flux.

---

## 3. Project Progress (Merged/Closed PRs Today: 165)

The core maintainers and community contributors are aggressively landing fixes:

**Codex Runtime Stability:**
- **#87879** (`fix(codex): recover context overflow and budget skip paths`) — Fixes two tightly related native-session recovery edges, including a terminal overflow loop and a budget skip recovery. *Ready for maintainer look.*
- **#88207** (`Fix Codex native thread overflow rotation`) — Rotates stale native Codex threads before overflow, tolerates compaction skips.
- **#88206** (`fix(codex): coalesce in-flight dynamic tool calls`) — Prevents duplicate tool calls keyed by `threadId`, `turnId`, namespace.

**Gateway & Security:**
- **#85916** (`fix(gateway): require admin scope for browser proxy invoke`) — Closes a privilege escalation path on `browser.proxy`.
- **#73163** (`fix(gateway): warn for insecure Control UI access`) — Startup warning when Control UI is exposed on non-loopback without device auth.
- **#87141** (`fix(plugin): harden schema and metadata fuzz boundaries`) — Expanded hardiness against malformed `fuzzplugin`/`mockplugin` fixtures.

**MCP & Cron Infrastructure:**
- **#87981** (`fix(cron): retire MCP runtimes on isolated cron timeout and dispose`) — Prevents MCP resource leaks during isolated cron session timeouts.
- **#88172** (`fix(mcp): kill orphaned stdio children on session teardown + auto-reconnect`) — Addresses `Not connected` errors and orphaned child processes.

**Channel & UI Fixes:**
- **#88194** (`[BUG]: Internal messages surface in Telegram chat`) — Filters out LLM-provider artefacts (`<channel|>`, `set-thought`, `───`) from streaming responses.
- **#87072** (`feat(telegram): opt-in interleaved progress lane`) — New renderer for reasoning text and runtime events on a dedicated lane.

**Architecture & Tooling:**
- **#88200** (`Refactor task state onto shared SQLite`) — Moves task/task-flow registry persistence onto the shared OpenClaw SQLite database.
- **#86627** (`Keep core doctor health in contribution order`) — Integrates structured health checks with the ordered core `doctor` checks.
- **#87796** (`feat(ci): autoscrub dependency lockfile-only PR changes`) — Reduces accidental dependency drift in PRs.

---

## 4. Community Hot Topics

The community is deeply engaged but clearly stressed by the regression velocity. The most active threads all center around **update trust** and **Codex configuration fragility**.

**🔥 #84038 — `doctor --fix` silently migrates OAuth config, token inflation [CLOSED]**
- **12 comments, 3 👍**
- *Underlying Need:* Trust in the upgrade toolchain. The `doctor --fix` command renamed `openai-codex/` config sections to `openai/`, breaking PI+OAuth runtime and causing 3–4× token usage. This is a high-severity trust issue for the entire upgrade pipeline.
- [OpenClaw Issue #84038](https://github.com/openclaw/openclaw/issues/84038)

**🔥 #67035 — Windows Chat UI regression (input swallowed, invisible streams) [OPEN]**
- **13 comments**
- *Underlying Need:* Basic desktop usability. Months after the initial 2026.4.14 regression, the web dashboard on Windows remains broken. Streamed replies are invisible until refresh; typing indicator flashes and blanks.
- [OpenClaw Issue #67035](https://github.com/openclaw/openclaw/issues/67035)

**🔥 #86820 — Codex OAuth compaction fails without `OPENAI_API_KEY` [CLOSED]**
- **11 comments, 6 👍**
- *Underlying Need:* Reliable fallback logic. Codex-backed sessions with OAuth profiles fall back to direct OpenAI API during compaction and fail if the key isn't set.
- [OpenClaw Issue #86820](https://github.com/openclaw/openclaw/issues/86820)

**🔥 #88102 — Codex runtime rejects `openai/gpt-5.5` after upgrade [CLOSED]**
- **11 comments, 1 👍**
- *Underlying Need:* Upgrade reliability. Model `openai/gpt-5.5` with Codex harness broke immediately after v2026.5.27. Workaround (`codex/gpt-5.5`) drops Telegram `/status` usage.
- [OpenClaw Issue #88102](https://github.com/openclaw/openclaw/issues/88102)

**🔥 #77576 — Telegram group responses route to webchat [OPEN]**
- **7 comments, 4 👍**
- *Underlying Need:* Correct cross-channel routing. A fundamental regression for Telegram group automation.
- [OpenClaw Issue #77576](https://github.com/openclaw/openclaw/issues/77576)

**🔥 #87646 — Feishu dispatch crashes after v2026.5.27 [OPEN]**
- **7 comments, 1 👍**
- *Underlying Need:* Channel parity. Feishu integration is completely broken after upgrade (`TypeError: read property 'run' of undefined`).
- [OpenClaw Issue #87646](https://github.com/openclaw/openclaw/issues/87646)

**🔥 #88154 — [Feature]: Add Slack Modal Support [OPEN]**
- **5 comments, 1 👍**
- *Underlying Need:* Structural input collection. The community is pushing for Slack to be a first-class interactive surface.
- [OpenClaw Issue #88154](https://github.com/openclaw/openclaw/issues/88154)

---

## 5. Bugs & Stability

**Stability Verdict: Fragile / High Engagement.** The project is shipping fixes faster than bugs are being filed, but the root-cause complexity of the Codex runtime and session-lock issues means new regressions are appearing daily.

### Critical / Beta Blocker (P1)

| Issue | Symptom | Root Cause / Fix Status |
|---|---|---|
| **#88102** + **#87650** | Codex provider/runtime mismatch after upgrade | `doctor --fix` migration path is flawed. *Fix PRs #84728, #87879 in review.* |
| **#86948** | Codex app-server turns silently drop (event loop saturation) | Gateway event loop blocked by CPU-sync work. *Fix PRs #87879, #88207 open.* |
| **#75378** | 1012 restart on parallel subagent spawn | Event loop blocks for 5+ seconds. *Fix PR #87879 addressing budget skip paths.* |
| **#86509** / **#86358** | Event-loop starvation returns (87s lock phase, 17s compaction delay) | Regression in v2026.5.22. *Roll-back to v5.20 recommended by reporter.* |

### High Severity (P1/P2)

| Issue | Symptom | Notes |
|---|---|---|
| **#57019** | Session write lock race — async release deletes newly-acquired lock | In-memory `HELD_LOCKS` Map entry deleted before async `fs.rm()`. *PR #88210 protects writes.* |
| **#85953** | `sessions_yield` can leave parent session transcript lock held | Subagent completion callback timeout. |
| **#87615** / **#73723** | `Native hook relay unavailable` blocks Codex tool execution | Relay bridge sometimes never spawns; intermittent. |
| **#54155** | Gateway memory leak 389MB → 14.7GB over 4 days | Open since March. Session accumulation. *No fix merged.* |
| **#86613** | `memory_search` leaks one FD per `.md` file | Open since May 25. *Deterministic repro available, no fix.* |
| **#87177** | QQBot message duplication + heartbeat session leakage | Non-standard outputs instead of `HEARTBEAT_OK`. |
| **#87711** | Empty assistant delivery on first turn after `/new` on Telegram | Footer-only output (`"— out" usage`). |
| **#87744** | Codex-backed Telegram turns time out waiting for `turn/completed` | Post-upgrade regression. |
| **#83184** | Heartbeat-driven replies leave `pendingFinalDelivery` stuck, blocking subsequent heartbeats | Field never nulled after successful send. |
| **#87981** (PR) | MCP runtimes not retired on isolated cron timeout | *Fix PR just merged.* |

### Ongoing Recurring Issues
- **Model Fallback Logic Failures** (#48680, #79329, #87641): 403 / business rejections incorrectly marked as `candidate_succeeded`. Moonshot/Kimi duplicate tool-call IDs exposed (#51593).
- **Channel Regressions**: Feishu (#87646), Matrix (#87307), Discord (#81484), Telegram (#77576, #87711, #88194).
- **UI State Bugs**: Webchat run status stuck on "In progress" (#86939), Dashboard tokenized URL print (#81917).

---

## 6. Feature Requests & Roadmap Signals

### Features Most Likely to Ship in v2026.6.x

The current stabilization sprint will dominate the next release, but several features are mature and have maintainer review:

- **Slack Modal Support (#88154)** — High community demand for structural input collection. Slack channel integration is already mature; modals are a natural next step.
- **Exec Denylist (#82596)** — Large PR providing a middle ground between allowlist and full-exec. *Merge risk: 🚨 compatibility + security-boundary. High value for power users.*
- **Telegram Interleaved Progress Lane (#87072)** — Opt-in rendering of reasoning text into a single durable live message. *Ready for maintainer.*
- **Capability Manifest Verifier (#88189)** — Security/enterprise plugin for HS256 JWT capability manifests. Signals an enterprise or managed-service push.
- **Claude CLI Interactive Backend (#81851)** — Novel community integration using a local TLS MITM proxy to tap Anthropic API SSE events.

### Longer-Running Requests Needing Maintainer Signal

- **Per-Agent Dreaming Configuration (#67413)** (Reported Apr 15) — CRITICAL for OOM prevention on memory-heavy setups.
- **Native web_search for ZAI (GLM) and Google Gemini (#17925)** (Reported Feb 16) — High upvotes (5 👍), zero maintainer engagement.
- **TUI Shift+Enter for Multi-line Input (#10118)** (Reported Feb 6) — Long-standing QoL, ignored by maintainers.
- **Agent Wall-Clock Time Source (#82968)** (Reported May 17) — Architectural gap noted by community.
- **Browser Screenshot Vision for Text-Only Models (#84247)** — Large PR pending author.

---

## 7. User Feedback Summary

The overall sentiment is **engaged but frustrated**, primarily driven by the fragility of the upgrade path and the rate of regressions.

### Pain Points (High Volume)
- **"Upgrade broke my setup"** is the dominant narrative. Users upgrading from v2026.5.20 to v2026.5.22–.27 are hitting provider/runtime mismatches, routing failures, and event-loop hangs.
- **`doctor --fix` has lost trust.** Issue #84038 documented that the configuration migration tool silently corrupts setups. Users are now wary of running it.
- **Windows desktop experience is abandoned.** Issue #67035 (13 comments) has been open since April with no fix. The webchat UI on Windows actively degrades the experience.
- **Multi-channel workflows are unreliable.** Telegram, Feishu, Discord, and Matrix all have open delivery regressions. Users running multi-platform setups are having to pin versions or roll back.

### Satisfaction Signals
- **Responsiveness is appreciated.** The 4 betas today and 165 merged PRs show maintainers are *trying* to keep up. Users filing deep diagnostic reports (deterministic reproducers, stack traces) indicates a technically engaged power-user base.
- **Feature demand is high.** The volume of well-written feature requests (Slack modals, exec denylist, progress lanes) shows the community sees OpenClaw as their long-term platform.

### "Upgrade Momentum" Trend
There is a detectable cycle developing: new release → regressions discovered → panic firefighting → hotfixes. This is burning user goodwill. The project needs a stabilization release that specifically forbids "risky" features until the Codex runtime session management and the event-loop scheduler are fully hardened.

---

## 8. Backlog Watch

Several critical and long-standing issues have been eclipsed by the current Codex sprint:

| Issue | Reported | Severity | Status | Why It Matters |
|---|---|---|---|---|
| [#54155 — Gateway Memory Leak (389MB → 14.7GB over 4 days)](https://github.com/openclaw/openclaw/issues/54155) | Mar 25 | **P1, Diamond Lobster** | OPEN (updated May 29) | Existential threat to self-hosted instances. No fix in sight. |
| [#62328 — node:sqlite missing FTS5 module — memory keyword search broken](https://github.com/openclaw/openclaw/issues/62328) | Apr 7 | **P2, Diamond Lobster** | OPEN (updated May 29) | Breaks a core memory feature on default Node.js installs. |
| [#80607 — Non-default multi-agent uses `embedded_run`, 10–17s latency](https://github.com/openclaw/openclaw/issues/80607) | May 11 | **P2** | OPEN | Fundamental UX block for multi-agent setups. |
| [#81917 — Dashboard logs bare URL / UI hangs on Linux browser launch](https://github.com/openclaw/openclaw/issues/81917) | May 14 | **P2, Platinum Hermit** | OPEN | Security + Linux desktop UX gap. |
| [#67413 — Per-agent dreaming configuration (OOM prevention)](https://github.com/openclaw/openclaw/issues/67413) | Apr 15 | **P2, Diamond Lobster** | OPEN (updated May 29) | Multiple workspaces dreaming simultaneously causes OOM. |
| [#82968 — Agent lacks reliable wall-clock time source](https://github.com/openclaw/openclaw/issues/82968) | May 17 | **P2, Platinum Hermit** | OPEN | Architectural limitation for scheduled/sleep agent behaviors. |
| [#17925 — Native web_search passthrough for ZAI (GLM) / Google Gemini](https://github.com/openclaw/openclaw/issues/17925) | Feb 16 | **P2** | OPEN (5 👍) | High demand, zero maintainer commitment. |
| [#10118 — TUI: Support Shift+Enter for newline](https://github.com/openclaw/openclaw/issues/10118) | Feb 6 | **P3** | OPEN (5 👍) | Long-standing QoL request. |
| [#86613 — `memory_search` FD leak on macOS](https://github.com/openclaw/openclaw/issues/86613) | May 25 | **P1, Diamond Lobster** | CLOSED? (repro provided) | Critical for macOS long-running gateways. *Closing status unclear from data.* |

**Backlog Assessment:** The backlog is accumulating critical bug debt. The memory leak (#54155), FTS5 dependency (#62328), and multi-agent latency (#80607) are all blocking issues for specific workflows. Unless the next release explicitly resolves these in addition to the Codex stabilization, user churn on those vectors is likely to increase.

---

## Cross-Ecosystem Comparison

**Cross-Project Ecosystem Comparison Report**
**Date:** 2026-05-30
**Scope:** 12 actively monitored open-source personal AI agent projects

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is in a high-growth inflection point characterized by an intense velocity–stability tradeoff. Across the top 10 active projects, over 800 combined issue and PR updates were processed in a single 24-hour window, reflecting massive community investment and rapidly expanding use cases from personal productivity to enterprise orchestration. However, the aggregate data reveals a landscape still earning its production maturity: critical security bypasses (Hermes, ZeroClaw, NanoBot), pervasive context management failures (OpenClaw, CoPaw, IronClaw), and fragile multi-channel delivery (Telegram, Slack, Feishu) are consistent friction points. The dominant investment themes are MCP security hardening, the emergence of multi-agent protocols (A2A/ACP), and a push toward first-class observability, signaling a maturation from experimental “copilot” patterns toward auditable, controllable agent infrastructure.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs Updated (24h) | Merged/Closed PRs | Release Today | Stability Pulse | Strategic Focus |
|---|---|---|---|---|---|---|
| **OpenClaw** | 330 | 500 | 165 | 4x beta (v2026.5.28) | **Fragile / Firefighting** | Codex runtime, session recovery |
| **NanoBot** | 33 | 41 | High churn | None | **Hardening / Very High** | Security audit, data-integrity |
| **Hermes Agent** | 50 | 50 | 15 | v0.15.2 hotfix | **Stabilizing** | MCP approval gates, A2A interop |
| **NanoClaw** | ~2 new | 7 | 2 | None | **Healthy** | MCP governance, LangFuse obs. |
| **NullClaw** | 3 reported | 7 | 7 | v2026.5.29 | **Healthy / Exemplary** | Telegram/LINE parity, ACP |
| **IronClaw** | 18 | 47 | 23 | None (pipeline blocked) | **High Dev / Moderate Risk** | Product-auth, trigger loop |
| **LobsterAI** | 1 new | 14 | 9 | None | **Hardening / High** | Lazy rendering, subagent lifecycle |
| **CoPaw** | 45 (25 closed) | 31 | 18 | v1.1.10-beta.1 | **High Dev / Moderate Risk** | Platformization, IDE parity |
| **ZeroClaw** | 19 | 46 | 9 | None (v0.8.1 queue) | **Pre-Release / Fragile** | MCP filtering, new TUI, DenyWithEdit |
| **Moltis** | 3 | 2 | 1 | None | **Responsive / New Blockers** | Docker/Apple sandboxing |
| **TinyClaw / ZeptoClaw / PicoClaw** | 0 | 0 | 0 | None | **Inactive** | N/A |

---

## 3. OpenClaw’s Position

**Advantages:**
- **Scale & Gravity:** No project matches OpenClaw’s integration surface area or community testing base. It acts as the ecosystem’s primary feature incubator (session management, multi-channel architecture).
- **Feature Breadth:** Most out-of-the-box provider routing (Codex runtime) and channel support; its technical decisions heavily influence downstream forks and inspired architectures.

**Technical Approach vs. Peers:**
- OpenClaw takes a monolithic reference-implementation approach that absorbs maximum complexity upstream. This contrasts with IronClaw’s modular Rust-based design and NullClaw’s minimal Zig core. The cost is operational fragility: the project currently manages the highest regression rate in the ecosystem.

**Community Size & Impact:**
- OpenClaw dominates raw community noise (330 issues, 500 PRs in 24h), but this activity reflects both deep engagement and acute user pain. The `doctor --fix` trust crisis (#84038) and Windows Chat UI regression (#67035) have tangible downstream effects, as many ecosystem operators treat OpenClaw’s migration health as a proxy for industry readiness. Its current “fragile” state directly shapes confidence across the broader ecosystem.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging simultaneously across multiple projects, indicating neglected or universally hard industry problems:

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **MCP Security & Sandboxing** | Hermes, NanoBot, ZeroClaw, NanoClaw | Approval bypass fix (#32877, #6991), SSRF rejection (#4074), symlink escapes (#4072), supply chain vetting (#2641) |
| **Runtime State Integrity** | OpenClaw, NanoBot, IronClaw, CoPaw | Session lock corruption (#57019), cursor duplication (#4081), KV cache invalidation (#4241), vector DB bloat (#4795) |
| **Cross-Channel Reliability** | OpenClaw, ZeroClaw, NullClaw, Hermes | Telegram routing/voice (#77576, #6999), Slack auth (#6992), Feishu crashes (#87646), LINE token caching (#934) |
| **Provider/Model Config Resilience** | OpenClaw, Hermes, ZeroClaw | Migration tool corruption (#84038), fallback logic gaps (#32646), DeepSeek reasoning loss (#6233) |
| **Observability & Cost Telemetry** | NanoClaw, Hermes, IronClaw | LangFuse integration (#2456), lazy tool loading (#6839), binary-E2E framework (#3702) |
| **Multi-Agent Protocols** | Hermes (A2A), NullClaw (ACP) | Agent discovery, standardized inter-agent communication beyond MCP tool-calling |

---

## 5. Differentiation Analysis

| Dimension | Market Leader / Notable Project | Key Distinction |
|---|---|---|
| **Scope & Breadth** | **OpenClaw** | Broadest integration surface, heaviest operational burden, incubator for the ecosystem |
| **Security Rigor** | **Hermes Agent** | Fastest security fix turnaround; A2A strategic bet; enterprise approval flows |
| **Architectural Purity** | **IronClaw / NullClaw** | IronClaw: most rigorous Rust design docs (trigger loop, product-auth). NullClaw: tightest issue-to-fix cycle (Zig backend) |
| **Innovation vs. Stability** | **ZeroClaw** | Highest risk-reward; DenyWithEdit approval model, TUI rewrite, but highest S1 bug rate |
| **IDE / Desktop Integration** | **CoPaw** | Directly competing with Trae/Cursor; agent teams, file diffs, conversation rollback. Most aggressive on UX parity |
| **Academic / Under the Hood** | **NanoBot** | Most thorough concurrency/security audit. High-quality bug triage paired with immediate fix PRs |
| **Content & Collaboration** | **LobsterAI** | Best artifact rendering and subagent lifecycle; focus on verbose agent output handling |
| **Sandbox & Infrastructure** | **Moltis** | Focused entirely on container/Docker sandbox correctness; enterprise proxy & arm64 support gaps |

**Real-World User Profiles:**
- **OpenClaw:** Power user scaling multi-agent, multi-channel setups; accepts volatility for breadth.
- **Hermes / IronClaw:** Enterprise deployer requiring security audit trails and robust auth.
- **CoPaw:** Developer seeking IDE-grade agent interaction (diff-views, conversation branching).
- **ZeroClaw / NullClaw:** Early adopter pushing feature boundaries or deploying on constrained hardware.
- **NanoBot / NanoClaw:** Privacy/security-conscious user valuing audit transparency and local sovereignty.

---

## 6. Community Momentum & Maturity

**Tier 1: High Intensity / Scaling Pain**
- **OpenClaw, ZeroClaw, CoPaw.** These projects have the highest raw update volume and the highest regression velocity. They are the most visible and the most risky to deploy in production today. Contributor burnout risk is elevated.

**Tier 2: Architecture & Enterprise Hardening**
- **IronClaw, Hermes Agent.** Very high development velocity but focused on specific pillars. Lower volatility in end-user channels. IronClaw’s publishing pipeline drag (#3259) is a self-inflicted openness wound. Hermes leads on security responsiveness.

**Tier 3: Production Tail & Niche Optimization**
- **NanoBot, NanoClaw, NullClaw, LobsterAI, Moltis.** Tighter feedback loops, fewer regressions, higher stability. NullClaw demonstrates the most impressive issue-to-fix turnaround. NanoBot’s community audit model is best-in-class for responsible disclosure. These projects offer the most reliable deployment experience today.

**Tier 4: Inactive**
- **TinyClaw, ZeptoClaw, PicoClaw.** No activity in the 24-hour window suggests strategic abandonment or maintenance mode.

---

## 7. Trend Signals

**1. Security is the Universal Production Blocking Criteria.**
  Bypassed approval gates (Hermes #32877, ZeroClaw #6991), supply chain MCP risk (NanoClaw #2641), and unauthenticated API endpoints (NanoBot #4077) demonstrate that security is the single highest priority across every tier. Sandboxing and injection detection are table-stakes features for 2026.

**2. Multi-Agent Protocols (A2A/ACP) are Moving from Spec to Code.**
  Hermes’ A2A discussion (#514) and NullClaw’s merged ACP stdio adapter signal that the industry recognizes MCP as “tools” but requires a separate “agent-to-agent” standard for delegation and discovery. This will dominate roadmap discussions in Q3 2026.

**3. The “Upgrade Trust” Deficit.**
  OpenClaw’s `doctor --fix` corruption (#84038) and IronClaw’s 24-day publishing silence (#3259) show that neglecting the operator upgrade experience creates severe community erosion. CLI tooling reliability is becoming a core competitive differentiator.

**4. Observability is Non-Negotiable.**
  Operators are unwilling to run black-box agents. LangFuse integration (NanoClaw), lazy tool schema loading for token accounting (Hermes #6839), and binary E2E test frameworks (IronClaw #3702) indicate that production deployments require cost and latency transparency.

**5. Rust/Zig Dominate the Next-Generation Runtime Infrastructure.**
  The most forward-looking infrastructure projects—**IronClaw** (Rust), **NullClaw** (Zig), **ZeroClaw** (Rust)—are building on systems languages for safety and performance. Python/TypeScript remain dominant in the tooling and orchestration layers (Hermes, NanoBot, CoPaw), suggesting a future stack split.

**6. Context Management is the Core Unsolved UX Bottleneck.**
  Short-term memory loss (NanoBot #4044), vector index bloat (CoPaw #4795), KV cache invalidation (IronClaw #4241), and event-loop starvation (OpenClaw #75378) all point to a single root challenge: reliably managing agent state across long interactions. The project that structurally solves this will capture the “power user” segment of the market.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest | 2026-05-30

## 1. Today’s Overview
NanoBot is undergoing a dramatic surge in stabilization and security hardening, driven overwhelmingly by a comprehensive community-led audit. While no new releases were cut today, the project engine room is exceptionally hot: **41 pull requests** were updated and **33 issues** saw activity in the last 24 hours. The defining pattern of the day is contributor `hamb1y` systematically filing over a dozen detailed concurrency, data-integrity, and security bugs—and immediately submitting paired fix PRs. This signals rapid maturation toward production readiness. Despite the high open-bug count, the concurrent availability of fixes indicates a very healthy and responsive collaboration between community and maintainers.

## 2. Releases
**None published on 2026-05-30.**

## 3. Project Progress
Progress is overwhelmingly corrective, but two significant feature milestones landed:

### Merged / Closed
- **Model Presets** ([PR #3696](https://github.com/HKUDS/nanobot/pull/3696)) — *Merged.* A major quality-of-life feature allowing users to define named model presets with automatic failover and runtime model switching.
- **Windows Multi-line Exec Fix** ([PR #4051](https://github.com/HKUDS/nanobot/pull/4051)) — *Merged.* Fixes `cmd.exe` dropping multi-line Python commands; switches to PowerShell for multi-line scripts.
- **API Key Arrearage Warning** ([Issue #3006](https://github.com/HKUDS/nanobot/issues/3006)) — *Closed.* Users will now receive a warning when their API key is out of credit.
- **Configurable Document Extraction** ([Issue #4043](https://github.com/HKUDS/nanobot/issues/4043)) — *Closed.* Adds a config flag to disable automatic document parsing.

### Open (In Review)
- **Manual Memory Mode** ([PR #4050](https://github.com/HKUDS/nanobot/pull/4050)) — A major feature under review, isolating user-controlled memory consolidation from automatic background processing.
- **Security & Hardening Patch Set** (PRs [#4088–#4104](https://github.com/HKUDS/nanobot/pulls?q=is%3Apr+is%3Aopen+created%3A%3E2026-05-28)) — A cohesive series of 15+ fixes from the community audit awaiting review and landing.

## 4. Community Hot Topics
- **Short-Term Memory Loss** ([Issue #4044](https://github.com/HKUDS/nanobot/issues/4044)) — The most active discussion thread (4 comments). Users report the bot asks a question and then immediately forgets the conversational thread. This is the single loudest user pain point around conversational quality.
- **Coordinated Security Audit** — Contributor `hamb1y` filed 15+ issues and paired fix PRs covering SSRF bypass, unauthenticated API endpoints, symlink escapes, cursor corruption, and session key collisions. While individual issues have few discussion comments, the collective underlying need is unmistakable: **production-grade reliability and security for agentic operations.**
- **Matrix E2EE Verification** ([Issue #4042](https://github.com/HKUDS/nanobot/issues/4042)) — Tagged "good first issue" but actively blocking Element X users who cannot clear "unverified device" warnings.

## 5. Bugs & Stability
Ranked by severity. *(All filed by community contributor `hamb1y` unless noted. Almost all have immediate fix PRs.)*

### Critical – Security & Auth Bypass
| Issue | Description | Fix PR |
|---|---|---|
| [#4078](https://github.com/HKUDS/nanobot/issues/4078) | OpenAI-compatible API accepts unauthenticated requests | N/A |
| [#4077](https://github.com/HKUDS/nanobot/issues/4077) | WebSocket token issue route mints tokens without auth | [#4103](https://github.com/HKUDS/nanobot/pull/4103) |
| [#4074](https://github.com/HKUDS/nanobot/issues/4074) | MCP HTTP/SSE setup attempts loopback before SSRF rejection | [#4100](https://github.com/HKUDS/nanobot/pull/4100) |
| [#4076](https://github.com/HKUDS/nanobot/issues/4076) | `message` tool lacks outbound recipient auth | [#4102](https://github.com/HKUDS/nanobot/pull/4102) |
| [#4075](https://github.com/HKUDS/nanobot/issues/4075) | Dream can overwrite user-created skills without ownership | [#4101](https://github.com/HKUDS/nanobot/pull/4101) |
| [#4073](https://github.com/HKUDS/nanobot/issues/4073) | `extra_allowed_dirs` treated as fully writable roots | [#4099](https://github.com/HKUDS/nanobot/pull/4099) |
| [#4072](https://github.com/HKUDS/nanobot/issues/4072) | ExecTool workspace restiction bypassed via symlinks | [#4098](https://github.com/HKUDS/nanobot/pull/4098) |

### High – Data Loss & State Corruption
| Issue | Description | Fix PR |
|---|---|---|
| [#4044](https://github.com/HKUDS/nanobot/issues/4044) | Short-term memory / context window pressure loss (user-reported) | N/A |
| [#4080](https://github.com/HKUDS/nanobot/issues/4080) | `process_direct()` bypasses per-session dispatch locks | [#4104](https://github.com/HKUDS/nanobot/pull/4104) |
| [#4081](https://github.com/HKUDS/nanobot/issues/4081) | `MemoryStore.append_history` allocates duplicate cursors | N/A |
| [#4082](https://github.com/HKUDS/nanobot/issues/4082) | Cron jobs reuse fixed session context across runs | N/A |
| [#4079](https://github.com/HKUDS/nanobot/issues/4079) | API empty-response retry duplicates user turns | N/A |
| [#4066](https://github.com/HKUDS/nanobot/issues/4066) | Corrupt `last_consolidated` hides entire session history | [#4090](https://github.com/HKUDS/nanobot/pull/4090) |
| [#4057](https://github.com/HKUDS/nanobot/issues/4057) | Distinct session keys collide after filename sanitization | [#4090](https://github.com/HKUDS/nanobot/pull/4090) |

### Medium – Provider & Channel Glitches
| Issue | Description | Fix PR |
|---|---|---|
| [#4061](https://github.com/HKUDS/nanobot/issues/4061) | OpenAI-compat text-format tool calls not parsed structurally | [#4092](https://github.com/HKUDS/nanobot/pull/4092) |
| [#4059](https://github.com/HKUDS/nanobot/issues/4059) | Non-stream parser preserves duplicate tool call IDs | [#4092](https://github.com/HKUDS/nanobot/pull/4092) |
| [#4060](https://github.com/HKUDS/nanobot/issues/4060) | Anthropic provider emits dict blocks without required `type` | [#4093](https://github.com/HKUDS/nanobot/pull/4093) |
| [#4062](https://github.com/HKUDS/nanobot/issues/4062) | WebSocket drops proactive messages when no subscribers | [#4094](https://github.com/HKUDS/nanobot/pull/4094) |
| [#4063](https://github.com/HKUDS/nanobot/issues/4063) | Stream delta coalescing ignores `_stream_id` | [#4094](https://github.com/HKUDS/nanobot/pull/4094) |
| [#4065](https://github.com/HKUDS/nanobot/issues/4065) | Invalid `STREAM_IDLE_TIMEOUT_S` crashes streaming setup | [#4095](https://github.com/HKUDS/nanobot/pull/4095) |
| [#4067](https://github.com/HKUDS/nanobot/issues/4067) | Invalid config silently falls back to defaults | [#4095](https://github.com/HKUDS/nanobot/pull/4095) |
| [#4068](https://github.com/HKUDS/nanobot/issues/4068) | Matrix stream buffer keyed only by `chat_id`, not `stream_id` | [#4096](https://github.com/HKUDS/nanobot/pull/4096) |

## 6. Feature Requests & Roadmap Signals
- **Manual Memory Mode** ([PR #4050](https://github.com/HKUDS/nanobot/pull/4050)) — The strongest roadmap signal. Users want deterministic, user-initiated memory operations alongside automatic consolidation. Likely a flagship feature for the next minor release.
- **Model Presets** ([PR #3696](https://github.com/HKUDS/nanobot/pull/3696)) — Already merged. Signals focus on power-user configuration and agent reliability via automatic failover.
- **Configurable Document Extraction** ([Issue #4043](https://github.com/HKUDS/nanobot/issues/4043)) — Closed quickly, showing the team is receptive to modular configuration for workflow flexibility.
- **Dream Scheduling Gate** ([Issue #4069](https://github.com/HKUDS/nanobot/issues/4069)) — Request for an explicit `enabled` flag on Dream cron jobs, mirroring the heartbeat system.

## 7. User Feedback Summary
The primary sentiment is a **push for reliability and transparency**.
- **Pain Point: Memory Loss** ([#4044](https://github.com/HKUDS/nanobot/issues/4044)) — Users are testing NanoBot in sustained conversations and hitting context-window and state-management failures. This is the loudest user-facing quality issue.
- **Pain Point: Silent Failures** ([#3006](https://github.com/HKUDS/nanobot/issues/3006), [#4067](https://github.com/HKUDS/nanobot/issues/4067)) — Users express frustration when the system fails without feedback (e.g., expired API keys, invalid config).
- **Pain Point: Integration Friction** ([#4042](https://github.com/HKUDS/nanobot/issues/4042)) — The Matrix/E2EE verification issue is blocking users of modern Matrix clients like Element X.
- **Satisfaction Signal:** The rapid convergence of bug reports and paired fix PRs suggests a deeply engaged technical user base willing to contribute directly to project hardening, which is a strong indicator of community health and project stickiness.

## 8. Backlog Watch
The processing cadence today is aggressive. A 2-month-old issue ([#3006](https://github.com/HKUDS/nanobot/issues/3006)) was closed, and a major feature ([#3696](https://github.com/HKUDS/nanobot/pull/3696)) was merged.

- **Matrix E2EE Verification** ([Issue #4042](https://github.com/HKUDS/nanobot/issues/4042)) — Tagged "good first issue" but has wide channel-level impact. Deserves maintainer attention if Matrix interoperability is a stated priority.
- **Audit PR Bottleneck** — The primary risk to the backlog is the sheer volume of the `hamb1y` patch set. Reviewing and landing 15+ interdependent fixes without regressions will be the critical path for the coming week. The project would benefit from a dedicated stabilization branch or focused review cycle.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for May 30, 2026, based on the provided GitHub data.

---

# Hermes Agent Project Digest
**Date:** May 30, 2026
**Period Analyzed:** May 29, 2026 – May 30, 2026

---

## 1. Today's Overview
The Hermes Agent project is operating at high velocity, processing significant community engagement with **50 issues** and **50 pull requests** updated in the last 24 hours. The team shipped a packaging hotfix (**v0.15.2**) while simultaneously merging major security patches addressing critical approval bypasses. The project state is healthy but in a heavy stabilization cycle, with approximately **41 open issues** and **35 open PRs** indicating an active backlog. Community focus is split between demanding core performance improvements (lazy tool loading) and pushing for new inter-agent interoperability standards (A2A Protocol).

## 2. Releases
A new hotfix version was released on May 29th:
- **v0.15.2 (v2026.5.29.2)**
  - **Change:** Fixes a critical packaging bug where bundled `plugin.yaml` manifests were missing from the wheel and source distributions ([commit `827f7f07`](https://github.com/NousResearch/hermes-agent/commit/827f7f07825be57108cbea18325e8f5e9fb5d2f2)).
  - **Impact:** Low. This is a hotfix that corrects a build artifact issue. No API changes, migration steps, or breaking changes are required.

## 3. Project Progress
The team closed **15 pull requests** and **9 issues** in the last 24 hours. Key merged changes include:

- **Security Hardening (Major):**
  - **[PR #33828](https://github.com/NousResearch/hermes-agent/pull/33828)** (Merge): Routes shell-like MCP tool calls (`ssh`, `docker`, etc.) through the approval gate, closing the bypass identified in [Issue #32877](https://github.com/NousResearch/hermes-agent/issues/32877).
  - **[PR #32705](https://github.com/NousResearch/hermes-agent/pull/32705)** (Merge): Enforces approval revocation (fixing the permanent "always_approve" mechanic) and extends audit logging to MCP/plugin tools.
  - **[PR #35078](https://github.com/NousResearch/hermes-agent/pull/35078)** (Merge): Fixes support for running the gateway as root (`HERMES_UID=0`), a documented but non-functional configuration.

- **Platform & Integration Fixes:**
  - **[PR #35097](https://github.com/NousResearch/hermes-agent/pull/35097)** (Merge): Fixes failing macOS CI tests by narrowing an overly broad `/private/var/` sensitive path prefix.
  - **[PR #35088](https://github.com/NousResearch/hermes-agent/pull/35088)** (Merge): Adds an opt-in `capability-manifest-verifier` plugin for evaOS integrations.

## 4. Community Hot Topics
The most active discussions and high-reaction items reveal a community deeply invested in both performance and future standards:

- **Top Voted Feature: [Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839) — Lazy Tool Schema Loading** (13 👍, 20 comments)
  Users are strongly demanding a two-pass tool injection system to reduce the ~3,500-5,000 token overhead per API call caused by loading all tool schemas. This is the dominant performance pain point, especially for local models.

- **Top Discussion: [Issue #514](https://github.com/NousResearch/hermes-agent/issues/514) — A2A Protocol Support** (12 👍, 24 comments)
  A deep strategic discussion about implementing Google's Agent-to-Agent standard for remote agent discovery and communication. The community views this as the natural complement to MCP ("who can help me?" vs. "what tools can I use?").

- **Highest Engagement (Bug): [Issue #34071](https://github.com/NousResearch/hermes-agent/issues/34071) — v0.15.0 Docker Crash** (13 comments)
  This was the most impactful recent regression (container exits with code 127). The rapid closure of this issue demonstrated project responsiveness.

- **Community Demand: [Issue #10567](https://github.com/NousResearch/hermes-agent/issues/10567) — Dashboard CORS/Host Config** (9 👍)
  Users are actively asking for simple `--host` and CORS config flags to allow remote/Tailscale access to the web UI.

## 5. Bugs & Stability
Stability is under heavy fire following the v0.15.0 migration, with a wave of regressions specifically hitting gateway and Docker users.

- **Critical / P1:**
  - **[Issue #35075](https://github.com/NousResearch/hermes-agent/issues/35075)** (New) — **Cron Injection Scanner Gap:** The runtime tripwire uses a narrower invisible-unicode character set than the install-time scanner, allowing obfuscated directives to bypass security. **No fix PR yet.**
  - **[Issue #34966](https://github.com/NousResearch/hermes-agent/issues/34966)** (New) — **MCP Reload Process Leak:** Every gateway reload or `/reload-mcp` call spawns new processes but never kills the old ones, leading to OOM. **Fix pending.**
  - **[Issue #32646](https://github.com/NousResearch/hermes-agent/issues/32646)** (Updated) — **Fallback Provider Logic:** `fallback_providers` are not activated when an API 429 error follows a prior timeout recovery.

- **Major Regressions (P1/P2):**
  - **[Issue #35032](https://github.com/NousResearch/hermes-agent/issues/35032)** — Feishu approval buttons broken post-v0.15.0. **Fix exists** ([PR #35090](https://github.com/NousResearch/hermes-agent/pull/35090)).
  - **[Issue #35062](https://github.com/NousResearch/hermes-agent/issues/35062)** — Weixin cron push silently fails (`ret=-3`) on v0.15.
  - **[Issue #34091](https://github.com/NousResearch/hermes-agent/issues/34091)** — Docker v0.15.0: TUI disconnected from dashboard events.
  - **[Issue #35059](https://github.com/NousResearch/hermes-agent/issues/35059)** — Non-default profile gateway fails due to SSH config path resolution.
  - **[Issue #35025](https://github.com/NousResearch/hermes-agent/issues/35025)** — Docker `chown` triggers on every boot when using non-default `HERMES_UID`.

## 6. Feature Requests & Roadmap Signals
The data strongly suggests the following trajectory for upcoming releases:

- **Likely for v0.16 (Performance Sprint):**
  - **Lazy Tool Schema Loading ([#6839](https://github.com/NousResearch/hermes-agent/issues/6839)):** The #1 pain point by upvotes. A prime candidate for immediate development to drastically reduce token costs.
  - **Dashboard Remote Access ([#10567](https://github.com/NousResearch/hermes-agent/issues/10567)):** A simple, high-value configuration tweak the community expects.

- **Strategic Roadmap (Multi-Agent Interop):**
  - The combination of **A2A Protocol ([#514](https://github.com/NousResearch/hermes-agent/issues/514))** and **Native ACP Client Transport ([#35063](https://github.com/NousResearch/hermes-agent/issues/35063))** suggests a strategic pivot towards making Hermes a hub within a larger agent mesh ecosystem. The evaOS plugin ([PR #35088](https://github.com/NousResearch/hermes-agent/pull/35088)) validates this direction.

- **Quality of Life:**
  - **Paginated Memory ([#34745](https://github.com/NousResearch/hermes-agent/issues/34745)):** Moving past the 2,200-character memory limit with keyword search.
  - **Reasoning Fallback ([#34786](https://github.com/NousResearch/hermes-agent/issues/34786)):** Auto-disable thinking/reasoning parameters if the API rejects them.
  - **iTerm2 Support ([#35057](https://github.com/NousResearch/hermes-agent/issues/35057)):** Standardizing Shift+Enter for newlines in the CLI.

## 7. User Feedback Summary
User sentiment is polarized between the friction of regressions and high confidence in the project's security response.

- **Pain Points:**
  - **Token Bloat (Highest Frequency):** Users running local models are being squeezed hard by full tool schema injection, echoing loudly in [Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839).
  - **v0.15.x Upgrade Friction:** Enterprise and casual users alike are hitting regressions in gateway platforms (Feishu, Weixin) and Docker deployment. The number of "it worked in v0.14" comments is high.
  - **Security Trust:** The MCP approval bypass ([#32877](https://github.com/NousResearch/hermes-agent/issues/32877)) caused concern, but the rapid merger of [PR #33828](https://github.com/NousResearch/hermes-agent/pull/33828) effectively quelled the outcry.

- **Satisfaction:**
  - **Rapid Response:** Users appreciate the very short turnaround on the Docker crash ([#34071](https://github.com/NousResearch/hermes-agent/issues/34071)) and the immediate hotfix (v0.15.2).
  - **High-Quality Bug Reports:** The user base is technically sophisticated, filing detailed production-grade bug reports (e.g., [Issue #17861](https://github.com/NousResearch/hermes-agent/issues/17861) on Anthropic thinking blocks), showcasing deep trust in the project.

## 8. Backlog Watch
Several high-value items remain unassigned or lack recent maintainer action.

- **[Issue #514](https://github.com/NousResearch/hermes-agent/issues/514) — A2A Protocol:** Created March 6. Despite being the most discussed feature, it lacks a milestone or assignee.
- **[Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839) — Lazy Tool Loading:** Created April 9. The most upvoted feature request remains unassigned.
- **[Issue #17861](https://github.com/NousResearch/hermes-agent/issues/17861) — Anthropic Thinking Block Loss:** Created April 30. A **P1 bug** that degrades reasoning for Claude users on multi-turn conversations.
- **[Issue #13356](https://github.com/NousResearch/hermes-agent/issues/13356) — Telegram File Delivery:** Filed April 21. A **P1** platform-specific bug with no assignee.
- **[PR #24868](https://github.com/NousResearch/hermes-agent/pull/24868) — DingTalk Reconnect Loop:** Filed May 13. A P2 fix that has been awaiting maintainer review for over two weeks without activity.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-30

## 1. Today's Overview
The project is in a healthy maintenance and feature-delivery phase. Seven pull requests saw activity, with two major features reaching the merged state: the LangFuse observability integration for the Claude provider and the highly anticipated OneCLI-native Gmail MCP tool. Community contributor @yairixStudio landed a dedicated batch of three fixes targeting the Telegram and Router modules, signaling intense real-world use of those pathways. However, the strongest signal today is the filing of Issue [#2641](nanocoai/nanoclaw#2641) warning of a supply chain risk in a third-party Gmail authentication package, placing the broader security posture of MCP tool installation under the spotlight. No new releases were cut.

## 2. Releases
*None.*

## 3. Project Progress (Merged/Closed PRs)
- **[#2456](nanocoai/nanoclaw#2456) feat(langfuse) — LangFuse Observability for Claude** (Author: @dustinlucien)  
  *Merged.* Instruments `ClaudeProvider.query()` to emit traces for latency, API errors (retries + rate limits), tool call timing, and context compaction token counts. This provides the foundation for production-grade observability and debugging of agent sessions.

- **[#1961](nanocoai/nanoclaw#1961) skill(add-gmail-tool) — OneCLI-native Gmail MCP** (Author: @grtwrn)  
  *Merged.* Adds a Utility skill (`/add-gmail-tool`) that installs Gmail as an MCP tool using OneCLI for credential injection—no raw API keys or passwords are exposed. This directly aligns with v2’s security invariants and addresses the credential handling pattern criticized in recent community security discussions.

## 4. Community Hot Topics
- **[#2641](nanocoai/nanoclaw#2641) [OPEN] Supply chain risk — @gongrzhe/server-gmail-autoauth-mcp** (Author: @NoamGit)  
  The single most impactful community signal today. While it has zero comments and reactions, the topic is the highest-stakes discussion for the project: how does NanoClaw protect users from installing unverified, potentially malicious third-party MCP tools? The issue links to a Medium article detailing an AI agent that installed a stranger’s code and asked for a Gmail password. The underlying need is clear—the community demands a robust trust-and-safety mechanism or a clearly documented sandboxing model for MCP tool installation. The merge of [#1961](nanocoai/nanoclaw#1961) is a direct countermeasure, but this issue remains open and requires an explicit maintainer response.

- **The yairixStudio Batch ([#2645](nanocoai/nanoclaw#2645), [#2644](nanocoai/nanoclaw#2644), [#2643](nanocoai/nanoclaw#2643))**  
  A cluster of three open PRs from the same contributor addressing Telegram and Router UX:
  - [#2645](nanocoai/nanoclaw#2645) introduces per-agent-group *context windows* for group chats—agents will receive the last N unseen messages, enabling coherent multi-turn conversations.
  - [#2644](nanocoai/nanoclaw#2644) and [#2643](nanocoai/nanoclaw#2643) fix broken detection of reply-to-bot and direct @mention triggers.  
  *Underlying need:* Early Telegram adopters are hitting critical friction points where the bot fails to recognize direct address, making group chat interactions feel broken. This batch suggests the Telegram integration is under active real-world testing and the feedback is actionable.

## 5. Bugs & Stability

| Severity | Issue/PR | Description | Status |
|---|---|---|---|
| **Critical** | [#2641](nanocoai/nanoclaw#2641) | Systemic supply chain risk in MCP tool installation—no vetting or sandboxing of third-party Gmail auth packages. | Issue open. Mitigation landed in [#1961](nanocoai/nanoclaw#1961). |
| **Medium** | [#2644](nanocoai/nanoclaw#2644) | `extractReplyContext` discards quoted message author—reply-to-bot is indistinguishable from any other reply. | Fix PR open. |
| **Medium** | [#2643](nanocoai/nanoclaw#2643) | Pattern-mode wirings ignore @mention, DM, or reply-to-bot when the message text doesn't also contain the keyword. Bot remains silent on direct address. | Fix PR open. |
| **Low** | [#2642](nanocoai/nanoclaw#2642) | `/add-telegram` skill requests `@chat-adapter/telegram@4.27.0`, conflicting with root `chat@4.26.0` pin. Installation will fail. | Fix PR open. |

## 6. Feature Requests & Roadmap Signals
- **Group Chat Context Windows ([#2645](nanocoai/nanoclaw#2645)):** Allowing agents to receive the last N *unseen* messages as a context block. This is a high-impact UX improvement likely bound for the next minor release, turning group chats from isolated trigger-response loops into coherent conversations.
- **Geospatial Codex Expansion ([#2646](nanocoai/nanoclaw#2646)):** The "Street Wind & Shadow Map" app adds an interactive map stack (OSM, Overpass, Open-Meteo) to the `codex` ecosystem. This signals a roadmap direction toward deploying rich single-page geospatial tools within the platform.
- **OneCLI as Universal Auth Gateway ([#1961](nanocoai/nanoclaw#1961)):** With the Gmail tool merged, OneCLI is now firmly established as the sole credential path. Future tool integrations (GitHub MCP, Slack MCP, etc.) will almost certainly be required to follow this pattern, phasing out raw credential injection entirely.

## 7. User Feedback Summary
- **Security Anxiety (Issue [#2641](nanocoai/nanoclaw#2641)):** The dominant user sentiment is a growing distrust of unvetted MCP packages. Users are demanding clear documentation, a permission model, or a "verified" badge ecosystem before they will comfortably install third-party tools that touch sensitive services.
- **Telegram Integration Roughness:** The concentrated bug fixes from @yairixStudio imply Telegram group chat interactions are a front-line use case, but users are encountering broken reply detection and silent bots. This is an active pain point being rapidly addressed.
- **Observability Demand:** The merge of LangFuse ([#2456](nanocoai/nanoclaw#2456)) meets a widely expressed need for transparency into agent behavior, latency, and cost—especially relevant for users deploying agents in semi-production or complex personal workflows.

## 8. Backlog Watch
- **[#1961](nanocoai/nanoclaw#1961) — The 35-Day Merge Cycle:** This skill was opened on April 24 and finally merged on May 29. The delay should be noted. Was there a technical bottleneck in the OneCLI integration, or was it simply deprioritized? Users will now actively test the Gmail auth flow. Maintainers should monitor for an influx of setup-related issues or feedback.
- **General Queue Health:** No critical community issues appear to be languishing without a response. The maintainers are actively merging older backlog items alongside fresh fixes, which is a strong indicator of healthy project velocity.

---

*All GitHub links refer to the [nanocoai/nanoclaw](https://github.com/nanocoai/nanoclaw) repository.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for 2026-05-30, based entirely on the provided GitHub activity snapshot.

---

# NullClaw Project Digest — 2026-05-30

## 1. Today's Overview
The NullClaw project experienced an exceptionally high-velocity maintenance cycle over the last 24 hours, culminating in the release of **v2026.5.29**. Three critical bugs were reported by a single power user and resolved on the same day, demonstrating a very tight feedback loop between users and maintainers. Seven pull requests were merged, covering core agent execution, channel reliability (Telegram and LINE), and infrastructure compatibility. The project is currently highly active, with two additional open PRs immediately addressing configuration and integration gaps, signaling a strong short-term focus on stability and user-visible fixes.

## 2. Releases

**New Release: v2026.5.29**
This is a significant patch release that bundles multiple bug fixes and minor features. Users are encouraged to upgrade as it resolves several critical data-loss and visibility bugs.
*   **What's Changed:**
    *   **New Feature:** Added a native **ACP stdio adapter** for standardized multi-agent communication.
    *   **Infrastructure:** Migrated GitHub CI workflows to `nullbuilder`. Updated Nix lockfiles for compatibility with Zig `0.16.0`.
    *   **Gateway Expansion:** Added authenticated `POST /media/transcribe` endpoints, wizard JSON handling, and hashed gateway paired tokens.
*   **Bug Fixes Included:**
    *   Fixed the `spawn` tool silently losing results in Telegram polling mode.
    *   Fixed the `memory_list` tool ignoring global session entries.
    *   Fixed Telegram inbound context to parse `reply_to_message` text.
    *   Fixed LINE channel message routing and reply token caching.
*   **Migration Notes:** None documented. The Nix fix requires a `nix flake update`.
*   **Link:** [v2026.5.29 Release](https://github.com/nullclaw/nullclaw/releases/tag/v2026.5.29)

## 3. Project Progress
Seven Pull Requests were merged or closed in the reporting period, reflecting strong forward momentum:
*   **Core Agent Fixes:**
    *   [#928](https://github.com/nullclaw/nullclaw/pull/928) — Delivers subagent results to Telegram in polling mode (Closes #918).
    *   [#929](https://github.com/nullclaw/nullclaw/pull/929) — Fixes `memory_list` to show global (NULL session) entries (Closes #917).
*   **Channel Enhancements:**
    *   [#930](https://github.com/nullclaw/nullclaw/pull/930) — Improves Telegram context by including `reply_to_message` text (Closes #916).
    *   [#934](https://github.com/nullclaw/nullclaw/pull/934) — Fixes LINE channel `sendMessage` routing and implements a thread-safe reply token cache.
*   **Infrastructure & Gateway:**
    *   [#933](https://github.com/nullclaw/nullclaw/pull/933) — Adds new authenticated gateway methods and expands config parsing.
    *   [#935](https://github.com/nullclaw/nullclaw/pull/935) — Fixes Nix builds by updating lockfiles for Zig 0.16.0 support.
    *   [#938](https://github.com/nullclaw/nullclaw/pull/938) — Version bump for the v2026.5.29 release.

## 4. Community Hot Topics
*   **Power User Signal:** A single user, **weissfl**, is responsible for filing the three most impactful issues of the day (#916, #917, #918). While these issues garnered zero comments, the underlying problems (silent data loss, global memory invisibility) represent critical functionality gaps that heavily affect production use cases. The rapid closure of these items by contributor **raskevichai** demonstrates a highly responsive project culture.
*   **Open PRs:**
    *   **[#940](https://github.com/nullclaw/nullclaw/pull/940): Custom Provider Model Fix** — Currently open. Directly addresses a breaking UX issue where users with custom OpenAI-compatible providers see incorrect model lists. This is expected to be the next high-priority community topic as it affects a growing demographic of self-hosters.
    *   **[#939](https://github.com/nullclaw/nullclaw/pull/939): Compact Context Flag Fix** — Currently open. Addresses a configuration footgun where the `compact_context` flag is parsed but never honored by the runtime engine. This is likely to generate significant discussion among power users concerned about token consumption and context management.

## 5. Bugs & Stability
The reporting period saw three high-severity bugs fully resolved, and two medium-severity bugs with open fix PRs.

| Severity | Issue | Status | Impact |
|---|---|---|---|
| **Critical** | [#918](https://github.com/nullclaw/nullclaw/issues/918) — `spawn` tool results lost in Telegram polling | **Fixed** in [#928](https://github.com/nullclaw/nullclaw/pull/928) | Silent data loss for complex agent chains. Root cause identified in `channel_loop.zig:1296`. |
| **High** | [#917](https://github.com/nullclaw/nullclaw/issues/917) — `memory_list` hides global session entries | **Fixed** in [#929](https://github.com/nullclaw/nullclaw/pull/929) | Broke core memory functionality for users relying on global context. |
| **Medium** | [#937](https://github.com/nullclaw/nullclaw/pull/939) — `compact_context` flag completely ignored by runtime | **Open PR** ([#939](https://github.com/nullclaw/nullclaw/pull/939)) | Silent configuration failure. Agent always compacts context regardless of user setting. |
| **Medium** | [#936](https://github.com/nullclaw/nullclaw/pull/940) — Custom OpenAI base_url not queried for models | **Open PR** ([#940](https://github.com/nullclaw/nullclaw/pull/940)) | Custom providers show wrong models in interactive menu. |
| **Low** | Nix lockfiles broken for Zig 0.16.0 | **Fixed** in [#935](https://github.com/nullclaw/nullclaw/pull/935) | Ecosystem-specific build break. |

## 6. Feature Requests & Roadmap Signals
*   **Gateway Maturity:** The addition of authenticated transcription endpoints and config parsing in PR [#933](https://github.com/nullclaw/nullclaw/pull/933) reinforces the strategic expansion of NullClaw from a chat agent into a multi-modal AI gateway service.
*   **Standardized Interop:** The inclusion of the "native ACP stdio adapter" in the latest release signals an architectural move toward standardized multi-agent communication protocols, likely enabling more complex swarm or chained agent topologies.
*   **Prediction for v2026.5.30:** The immediate roadmap will almost certainly include the merging of PRs [#939](https://github.com/nullclaw/nullclaw/pull/939) and [#940](https://github.com/nullclaw/nullclaw/pull/940). Further config parsing stabilization for the Gateway (noted in the wizard JSON handling of #933) is a strong candidate for the next feature cycle.

## 7. User Feedback Summary
*   **High Satisfaction Indicators:** The rapid 48-hour turnaround from bug report to release fix for the top three issues is a strong indicator of project health and maintainer responsiveness. Users can expect their critical reports to be triaged and resolved efficiently.
*   **Pain Points:** The most severe pain points revolve around **silent failures**. The `spawn` tool silently losing results and the `compact_context` flag being silently ignored erode user trust in the system’s runtime behavior. Users are also demanding **channel parity**, with simultaneous fixes hitting Telegram and LINE.
*   **Use Cases:** The current wave of bugs and fixes reveals a user base running complex agentic workflows (using `spawn` for task decomposition), persistent memory architectures, and multi-channel production deployments.

## 8. Backlog Watch
*Based solely on the 24-hour data window, no long-dormant issues are visible. The immediate backlog consists entirely of items filed and addressed within the last 48 hours.*
*   **Immediate Backlog:**
    *   PR [#940](https://github.com/nullclaw/nullclaw/pull/940) and PR [#939](https://github.com/nullclaw/nullclaw/pull/939) require maintainer review and merge. These represent the most critical remaining work items.
*   **Risk Signal:** The `compact_context` flag bug ([#939](https://github.com/nullclaw/nullclaw/pull/939)) is explicitly described as a "dead flag" that exists in parsing code but has never been wired to the execution engine. This pattern suggests a potential class of similar config-to-runtime disconnect bugs. A technical audit of `config_parse.zig` against all runtime config consumers could be a valuable long-term hygiene task to prevent future stale configuration parameters.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-30

## 1. Today's Overview

IronClaw is experiencing an intense period of development velocity, with **47 pull requests updated** and **18 issues updated** in the last 24 hours. Core contributors merged or closed **23 PRs** in a single day, signaling a significant push toward production readiness for the **Reborn architecture**. The dominant themes are the **unified product-auth credential layer**, **MCP extension porting** (Notion, NEAR AI), and freezing the **trigger loop & delivery resolution** design contracts. While the development cadence is exceptionally strong, a critical community pain point persists around the **publishing pipeline** (crates.io stuck at v0.24.0), and several high-severity stability bugs were filed, particularly around credential memory safety and KV cache invalidation during long-running conversations.

---

## 2. Releases

No new releases were published today. The latest version available on crates.io remains **v0.24.0** (published Mar 31, 2026), despite Git tags reaching **v0.28.2**. This gap between shipped code and published artifacts remains the project's most significant downstream friction point (tracked in Issue #3259).

---

## 3. Project Progress — Merged PRs Today (Closed/Completed)

The following represents the most impactful architecture and feature work that landed today:

**Product Auth & Credential Management**  
- **[#4234] feat (reborn) durable product auth** (serrrfirat, merged) — The heavyweight PR of the day. Moved the production filesystem-backed product-auth adapter into `ironclaw_reborn_composition`, sealed the domain contract, and fixed replay safety for OAuth callback claiming. This unblocked a whole chain of dependent work.  
- **[#4233] Migrate GitHub WASM credentials to product auth** (serrrfirat, merged) — Switched the bundled GitHub WASM manifest from static `SecretHandle` to `ProductAuthAccount` runtime credential source, making the credential broker the single source of truth.  
- **[#4231] Wire Reborn auth consumers through staged credentials** (serrrfirat, merged) — Added GSuite credential stager and host-owned credential resolution paths for first-party HTTP egress.  
- **[#4232] Verify auth gate blocked exits** (serrrfirat, merged) — Hardened auth gate resolution with durable BeforeBlock checkpoints and fail-closed semantics.

**MCP Ecosystem Expansion**  
- **[#4228] Port Notion MCP extension to Reborn** (serrrfirat, merged) — Wired host-mediated MCP runtime into Reborn composition with full reads, writes, comments, views, and user tools.  
- **[#4223] Port NEAR AI MCP to Reborn extensions** (serrrfirat, merged) — Added `nearai.search` capability as a host-bundled managed MCP extension.

**Design Contracts Frozen**  
- **[#3874] docs: add trigger loop design spec** (henrypark133, merged) — 412-line design spec for cron-backed scheduled agent triggers.  
- **[#4249] Add trigger trusted ingress contract** (henrypark133, merged) — Tenant-scoped fire identity, replay-first submission, and sub-minute schedule rejection.  
- **[#4248] Add delivery resolution contract** (henrypark133, merged) — Owned by OutboundPolicyService; defines candidate validation and cross-linking to approvals, auth, product adapters, events, and workflows.  
- **[#4240] docs: add communication delivery resolution design** (henrypark133, merged) — Persisted per-user communication preferences and fail-closed target selection.  
- **[#4244] Refine trigger loop and delivery resolution specs** (henrypark133, merged) — Locked down ingress/execution/delivery authority separation.

**Technical Debt & Fixes**  
- **[#4209] Decompose ironclaw_host_runtime/src/lib.rs** (henrypark133, closed) — Extracted egress modules out of a 1828-line file, addressing the project's own codebase size threshold rule.  
- **[#4243] fix(product-workflow): update RecordingFlowManager** (serrrfirat, merged) — Fixed CI trait drift for the `mark_continuation_dispatched` method.  
- **[#4179] Carry v1 Google SSO into WebChat v2** (italic-jinxin, closed) — Ported Google SSO behavior to the new reborn-integration surface.

---

## 4. Community Hot Topics

- **Publishing Pipeline Block** — [#3259](https://github.com/nearai/ironclaw/issues/3259) (11 comments, created May 5). The single highest-signal community issue. Downstream consumers are pinned to v0.24.0 on crates.io due to wasmtime CVE failures in intermediate builds. The community is asking for a concrete release plan and transparent communication on blockers. No maintainer resolution has been posted in over a week.

- **RuntimeCredentialTarget::PathPlaceholder Security Debate** — [#3917](https://github.com/nearai/ironclaw/issues/3917) (5 comments). A sharp security review debate on whether to kill or harden a credential injection channel that places secrets into URL path segments — argued to be "strictly worse than Header or Query injection." Signals a community that values rigorous credential hygiene.

- **Slack ProductAdapter MVP** — [#3857](https://github.com/nearai/ironclaw/issues/3857) (5 comments). The parent issue for the Slack Reborn integration. Underlying need: real-world enterprise messaging use cases for the AI assistant. The first code slice is open in PR [#4035](https://github.com/nearai/ironclaw/pull/4035) (Open, XL, awaiting review).

- **Binary-E2E Test Framework Plan** — [#3702](https://github.com/nearai/ironclaw/issues/3702) (4 comments). The community and team are discussing how to achieve Rust integration-test parity for the Reborn agent loop. An 88-file audit has been completed; an implementation plan is still pending.

---

## 5. Bugs & Stability

*Ranked by severity:*

**Critical: Plaintext Credential Injection Surface**  
[#4222](https://github.com/nearai/ironclaw/issues/4222) — Runtime HTTP egress copies protected `SecretMaterial` into ordinary `String` fields on the request path (headers, URLs) and network request carriers. An explicit zeroization protocol is missing. **No fix PR identified yet.**

**Critical: KV Cache Invalidation Across Conversation Turns**  
[#4241](https://github.com/nearai/ironclaw/issues/4241) (filed by user Kisekis) — Live Workspace prompt inputs break provider-side KV cache reuse because they are not treated as a static prefix. The result is that the agent loses context and efficiency across conversational turns, forcing full recomputation. This is a core UX and latency regression for long-running conversations. **No fix PR identified yet.**

**High: Unbounded Process Handoff State Growth**  
[#4226](https://github.com/nearai/ironclaw/issues/4226) — `cleaned_process_handoffs` in `ProcessObligationLifecycleStore` grows without eviction. Long-lived host processes will accumulate total process churn in memory. **No fix PR identified yet.**

**Medium: Compile Failure in Product Workflow Tests**  
[#4237](https://github.com/nearai/ironclaw/issues/4237) — PR #4234 introduced trait/field additions that block compilation of `cargo test -p ironclaw_product_workflow`. A *related* trait drift fix landed in [#4243](https://github.com/nearai/ironclaw/pull/4243), but the specific broken integration tests remain unaddressed.

**Medium: Nightly E2E Pipeline Failure**  
[#4108](https://github.com/nearai/ironclaw/issues/4108) — The nightly scheduled E2E test run failed (Full E2E / Extensions suite). Commit 749f58441f. **No root cause or fix PR identified yet.**

---

## 6. Feature Requests & Roadmap Signals

**V1 Product Auth Layer** — The massive pipeline of PRs merged today (#4234, #4233, #4231, #4232) makes it clear that a durable, projection-based credential broker is the current flagship feature. Issue [#4238](https://github.com/nearai/ironclaw/issues/4238) (project product-auth accounts into the runtime broker) and open PR [#4239](https://github.com/nearai/ironclaw/pull/4239) suggest we are in the final assembly phase of this system. **Prediction:** Product-auth v1 ships in the next 1–2 minor releases.

**Scheduled Agents (Trigger Loop)** — The freezing of the trigger and delivery resolution design contracts (#3874, #4249, #4248, #4240) strongly signals that cron-backed agent scheduling is the next major architectural milestone after product-auth lands.

**Enterprise Integration — Slack & GSuite** — Open PR [#4035](https://github.com/nearai/ironclaw/pull/4035) (Slack ProductAdapter) and design PR [#4247](https://github.com/nearai/ironclaw/pull/4247) (WebUI v2 E2E auth for GSuite + Notion + GitHub PAT) indicate the team is building toward a production-grade, adaptive personal assistant that can operate across messaging and enterprise productivity surfaces.

**Robust Long-Running Conversations** — Issue [#4241](https://github.com/nearai/ironclaw/issues/4241) is a de facto feature request from user Kisekis: the agent must support turn-aware KV cache reuse for Live Workspace prompt inputs. This will likely drive an optimization sprint after the current auth work stabilizes.

---

## 7. User Feedback Summary

**Pain Points**
- **Release Availability:** The dominant user complaint. Downstream consumers on crates.io cannot upgrade beyond v0.24.0 despite rich feature development on Git. This is actively damaging the external contributor experience and blocking adoption of new features.
- **KV Cache/Conversation Continuity:** User Kisekis's detailed bug report on KV cache invalidation ([#4241](https://github.com/nearai/ironclaw/issues/4241)) articulates a core dissatisfaction: "provider-side KV cache reuse depends on the next request starting with the same prefix... In agent frameworks, this break reduces the model's ability to maintain coherent context across long interactions."
- **Build Friction:** Abby Shekit noted that the Durable Product Auth PR (#4234) shipped with compile-breaking integration tests in `ironclaw_product_workflow`, creating friction for reviewers.

**Satisfaction Signals**
- **Security Vigilance:** The respectful but rigorous challenge of the `PathPlaceholder` credential route ([#3917](https://github.com/nearai/ironclaw/issues/3917)) demonstrates strong community trust in the project's adversarial review process.
- **Refactoring Discipline:** The team's willingness to open tracking issues for codebase size violations (e.g., #4209, 1828-line file) and proactively refactor signals strong engineering health and maintainability values.
- **MCP Expansion:** The porting of Notion and NEAR AI MCP extensions to Reborn was met with positive velocity — the team is clearly shipping.

---

## 8. Backlog Watch

**Critical: Issue #3259 — Publish 0.25.0–0.27.0 to crates.io**  
[Link](https://github.com/nearai/ironclaw/issues/3259)  
Created May 5, last updated May 29. **No maintainer resolution comment has been posted.** This is the single most important backlog item for the project's external health. 24 days without a concrete update risks community erosion.

**Open Design: Issue #3281 — EventStreamManager**  
[Link](https://github.com/nearai/ironclaw/issues/3281)  
Created May 6. This issue defines durable projection fanout for Web SSE, WebSocket, and API subscribers. While related PRs and design work (e.g., delivery resolution) have progressed, the core `EventStreamManager` service has not begun implementation.

**Unmerged Implementation: Issue #3702 — Binary-E2E Test Framework**  
[Link](https://github.com/nearai/ironclaw/issues/3702)  
Created May 16. The team has completed an 88-file audit and deep classification of 29 core agent-loop tests, but an implementation PR for the binary-E2E framework has not been produced. This is a key quality gate for the Reborn architecture.

**Stalled Large PR: PR #4035 — Slack ProductAdapter Core**  
[Link](https://github.com/nearai/ironclaw/pull/4035)  
Opened May 25, labeled XL. This is the first reviewable slice of the Slack Reborn integration. It remains open without a reviewer merge or explicit blocker identified, suggesting it may be awaiting bandwidth or completing the stacked PR chain.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – May 30, 2026

## 1. Today's Overview
Today marks a significant "hardening sprint" for LobsterAI. Activity is high but highly focused, with **14 Pull Requests updated** (9 merged/closed) and **1 new issue reported**. Development efforts are overwhelmingly concentrated on resolving performance bottlenecks and stability issues within the **Cowork** and **Artifacts** subsystems, specifically around rendering extremely large execution outputs and Markdown content. A confirmed application freeze bug was reported (#2079), which the merged PRs directly target the root cause of. The project appears to be in a proactive stability cycle, rapidly addressing user pain points from complex agent interactions.

## 2. Releases
No new releases were cut today. The project remains on its current version as of this digest.

## 3. Project Progress
Nine Pull Requests were merged or closed today, focusing on three core themes:

**Rendering & Execution Stability (High Priority)**
- **PR #2077** (`btc69m979y-dotcom`): A critical fix for performance and connection stability during large `exec` outputs. Introduces **lazy rendering** for large tool results (>20KB) with a summary/expand pattern, preventing Markdown rendering from blocking the UI. Also fixes a **TickWatchDog** starvation scenario in the WebSocket gateway that could cause disconnections during high-throughput exec storms.
- **PR #2075** (`btc69m979y-dotcom`): Complements the above by avoiding full rendering of oversized Markdown messages by default, showing a lightweight head/tail preview instead.

**Cowork & Subagent Lifecycle**
- **PR #2078** (`fisherdaddy`): Improves the Cowork skill routing system by emitting metadata instead of inlining prompts, promoting cleaner architecture.
- **PR #2074** (`btc69m979y-dotcom`): Implements proper deletion of subagent sessions, including IPC cleanup, store state removal, and sidebar UI updates. Includes tracker tests for deletion and regressions.
- **PR #2063** (`fisherdaddy`): Fixes reply assembly in the IM/Cowork subsystem, scoping it to the current turn and stripping extraneous "thinking" blocks.

**UI/UX & Infrastructure**
- **PR #2076** (`liugang519`): Optimizes the Artifact file preview toolbar by consolidating actions into a "more" menu, decluttering the interface for HTML and other file previews.
- **PR #2073** (`liuzhq1986`): Improves user feedback by showing clear toast messages when local artifact files are moved, deleted, or inaccessible, replacing silent failures.
- **PR #2072** (`btc69m979y-dotcom`): Comprehensive startup optimization for the OpenClaw gateway, fixing redundant config syncs, plugin re-registrations, and dev mode path issues.
- **PR #2057** (`fisherdaddy`): Replaces a deprecated VBScript launcher with a hidden PowerShell method for the app update process.

## 4. Community Hot Topics
The dominant theme in the community today is **Execution Stability and UI Responsiveness**.

- **Issue #2079** – *"执行结果窗口滚动到顶端会假死"* (Result window freezes when scrolling to the top)
    - **Type:** Bug Report
    - **Status:** Active, 1 comment, confirmed reproducible.
    - **Context:** This is the most critical direct user feedback point today. The user reports that navigating to the top of a long execution results window causes the entire application to freeze.
    - **Link:** [Issue #2079](https://github.com/netease-youdao/LobsterAI/issues/2079)

    **Analysis:** While no dedicated PR explicitly labels this specific scroll action as its target, **PRs #2077** and **#2075** (merged today) are direct upstream fixes for the underlying cause. They prevent the UI thread from being monopolized by large Markdown rendering and huge tool outputs. This suggests the team is actively diagnosing and mitigating the class of bugs this issue falls into. The community is demonstrating a need for robust handling of high-throughput, verbose agent outputs.

## 5. Bugs & Stability
Stability is the headline for today’s digest. Issues are ranked by severity.

| Severity | Issue / Risk | Status | Description |
|----------|--------------|--------|-------------|
| **Critical** | **UI Freeze on Scroll** (#2079) | Active | User reports a hard freeze when scrolling to the top of execution results. Impacts primary workflow. Fix PRs (#2077, #2075) addressing likely root causes (large payload rendering) were merged. |
| **Critical** | **Disconnection during Exec Storms** (#2077) | **Fixed** | TickWatchDog in the gateway was starving for ticks during large exec outputs, causing false WebSocket disconnections. |
| **Major** | **Silent Artifact Failures** (#2073) | **Fixed** | Missing or deleted local files in artifacts previously failed silently. Now shows clear toast errors. |
| **Major** | **IM Reply Assembly Issues** (#2063) | **Fixed** | Reply messages were incorrectly scoped and included raw thinking blocks. |
| **Medium** | **Gateway Startup Overhead** (#2072) | **Fixed** | Multiple redundant config syncs and plugin registrations during startup caused unnecessary launch delays and restarts. |

## 6. Feature Requests & Roadmap Signals
No formal feature requests were filed today, but the merged PRs provide clear signals for the roadmap:

- **Mature Subagent Governance**: PR #2074 (deleting subagent sessions) implies the team is moving beyond basic subagent spawning into full lifecycle management. Expect granular permissions, resource cleanup, and parent/child state management in future versions.
- **Decluttered Artifact UI**: PR #2076 signals a shift toward a cleaner, more minimalistic file preview experience. Consolidation of toolbar actions suggests an impending revamp of the Artifact interactions.
- **Performance as a Feature**: The heavy investment in lazy rendering and preview patterns (#2077, #2075) indicates the team is preparing for very large agent runs. This is an implicit roadmap signal that agents will grow more complex and verbose in upcoming releases.

## 7. User Feedback Summary
- **Pain Point (High Severity):** Application freezing when interacting with long execution results (#2079). Users executing complex, verbose agents are hitting hard limits in the rendering pipeline.
- **Satisfaction Signal:** The project is highly responsive. The deployment of PRs #2077 and #2075 on the same general timeframe as the bug report (#2079) shows rapid iteration and direct addressal of user-blocking issues.
- **Use Cases Identified:** The primary user base is clearly running heavy-duty agent workflows. The "exec storm" language (PR #2077) and the need for a head/tail preview on Markdown (PR #2075) point to users running agents that generate multi-megabyte output streams.

## 8. Backlog Watch
Several high-quality UX improvement PRs remain in the backlog and are flagged as stale, requiring maintainer attention.

- **PRs #1473, #1474, #1475, #1476, #1477** – *fix: unsaved change confirmation and draft persistence*
    - **Author:** `MaoQianTu`
    - **Created:** April 4, 2026
    - **Updated:** May 29, 2026 (stale label applied)
    - **Summary:** This batch of 5 PRs addresses a major class of user frustration: **silent data loss**. They add unsaved change confirmation dialogs to the Agent Creation Modal (#1473), Agent Settings Panel (#1474), MCP Server Config (#1475), immediate draft persistence on session/navigation switch (#1476), and overwrite confirmation for re-editing historical messages (#1477).
    - **Risk:** These are not new features; they are fundamental UX protections. Their prolonged staleness (nearly two months) risks users losing valuable work. These PRs represent the single largest gap in user experience currently left unaddressed in the codebase.
    - **Link:** [PR #1473](https://github.com/netease-youdao/LobsterAI/pull/1473), [PR #1474](https://github.com/netease-youdao/LobsterAI/pull/1474), [PR #1475](https://github.com/netease-youdao/LobsterAI/pull/1475), [PR #1476](https://github.com/netease-youdao/LobsterAI/pull/1476), [PR #1477](https://github.com/netease-youdao/LobsterAI/pull/1477)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-05-30

## 1. Today's Overview
Moltis saw moderate but targeted activity today, with the core team demonstrating strong responsiveness to user-reported bugs. One issue was resolved and its fix merged within 24 hours of filing, while two significant new platform compatibility issues were opened by the community. No new releases were published today, but the dependency tree received a bump via automated maintenance. The project's health signal is positive overall, though the surfacing of two cross-platform sandboxing bugs (Apple Silicon Docker and corporate proxy networking) indicates growing pains as the user base diversifies beyond standard Linux setups.

## 2. Releases
No new versions of Moltis were published today.

## 3. Project Progress
- **PR #1084 – Merged:** `fix(skills): track bundled skill disables individually`
  ([Link](https://github.com/moltis-org/moltis/pull/1084))
  Authored by `penso`, this fix addresses Issue #1083 by storing bundled skill disable states independently from category-level disables. It propagates the same enable-state helper across the chat discovery layer, web API, and skill detail responses, adding regression coverage specifically for granular control of Apple skills. This is a clean architecture win that resolves a user-facing inconsistency.

- **PR #1087 – Open:** `chore(deps): bump tar from 0.4.45 to 0.4.46`
  ([Link](https://github.com/moltis-org/moltis/pull/1087))
  A routine Dependabot pull request updating the `tar` Rust crate in the cargo dependency group.

## 4. Community Hot Topics
While no issues today have accumulated comments or reactions yet, the two open bugs represent the most critical community signals:

- **Issue #1086 – Apple Containers backend fails behind corporate proxy**
  ([Link](https://github.com/moltis-org/moltis/issues/1086))
  Filed by `karlmdavis`. The sandbox image build fails because DNS resolution breaks inside the Apple Containers builder VM when a corporate HTTPS proxy (Zscaler) is active. This reveals an unmet need for enterprise-level networking configuration in the Apple Containers backend.

- **Issue #1085 – Docker sandbox completely fails on arm64**
  ([Link](https://github.com/moltis-org/moltis/issues/1085))
  Also filed by `karlmdavis`. The Docker sandbox hard-crashes on Apple Silicon because Moltis attempts tmpfs mounts at `/sys/class/dmi` and `/sys/devices/virtual/dmi`, which are x86-only SMBIOS interfaces not present in Docker Desktop's arm64 Linux VM. This is a hard blocker for the largest Mac user segment.

These two issues, while silent in terms of discussion, point to the most engaged user profile: developers deploying AI agents on modern Apple hardware, often within corporate environments.

## 5. Bugs & Stability
Three bugs were active in the reporting period. Ranked by severity:

1. **Critical – Issue #1085: Docker sandbox fails on arm64**
   ([Link](https://github.com/moltis-org/moltis/issues/1085))
   A hard startup crash due to nonexistent DMI sysfs paths. Affects the core Docker sandbox on all Apple Silicon Macs. **No fix PR exists yet.**

2. **High – Issue #1086: Apple Containers sandbox build fails behind corporate proxy**
   ([Link](https://github.com/moltis-org/moltis/issues/1086))
   Blocks the Apple Containers backend entirely for users behind transparent HTTPS proxies. **No fix PR exists yet.**

3. **Low (Fixed) – Issue #1083: Cannot disable individual bundled skills**
   ([Link](https://github.com/moltis-org/moltis/issues/1083))
   Resolved by PR #1084 within 24 hours. Excellent turnaround time from the maintainers.

## 6. Feature Requests & Roadmap Signals
Today's data provides clear signals about where the project needs to invest next:

- **Arm64 / Apple Silicon Support:** Issue #1085 strongly suggests the sandbox needs platform-conditional mount logic. Expect either a fix that probes for DMI availability before mounting, or a broader refactor to abstract sysfs interactions away from container mounts.

- **Enterprise / Corporate Proxy Support:** Issue #1086 indicates that the Apple Containers backend needs explicit proxy configuration or DNS passthrough to the builder VM, not just standard environment variable inheritance.

- **Granular Configuration UX:** The fix in PR #1084 suggests the team is moving toward first-class individual skill toggle storage. This could be a precursor to a more sophisticated skill configuration UI or API in the next release.

The `tar` dependency bump (PR #1087) is a minor maintenance signal but shows active base ecosystem upkeep.

## 7. User Feedback Summary
User `karlmdavis` contributed two of the three issues today, representing a sophisticated deployment profile: running Moltis on modern Apple hardware (arm64) in a managed corporate networking environment (Zscaler proxy). This suggests Moltis is attracting enterprise early adopters, but hitting predictable friction points:

- **Pain Point 1:** Docker sandbox is non-functional out of the box on the most common Mac hardware (Apple Silicon).
- **Pain Point 2:** The Apple Containers backend is blocked by standard corporate security infrastructure.
- **Satisfaction Signal:** User `bsarkisov`'s bug report (#1083) was filed and fixed within the same 24-hour window, which is a strong positive signal for project health and maintainer attentiveness.

## 8. Backlog Watch
Based strictly on the data visible in the 24-hour window, there are no long-neglected items. All open issues (#1085, #1086) are newly filed and have not yet received a maintainer response. **The primary items to watch are Issues #1085 and #1086** — both are high-impact bugs affecting large user segments and will require prompt triage to prevent user churn. No stale PRs or unanswered feature requests are present in this sample.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest | 2026-05-30

The following report analyzes the daily activity of the **CoPaw** project, based on its primary open-source repository (`agentscope-ai/QwenPaw`). All links below reference repository artifacts.

---

## 1. Today's Overview

CoPaw displayed exceptionally high development activity on 2026-05-30. The project saw **45 issues updated** (25 closed) and **31 PRs updated** (18 merged/closed), alongside publishing a new beta release (**v1.1.10-beta.1**). The community remains deeply engaged, filing detailed bug reports and competitive feature comparisons (particularly against Trae and Cursor), which drove a very active triage and merge cycle. While the team aggressively shipped fixes for desktop packaging, cron reliability, and agent reasoning, a major architectural breaking change (AgentScope 2.0 migration) has been formally proposed and is looming on the immediate roadmap.

---

## 2. Releases

**v1.1.10-beta.1** was published today.

- **Changelog highlights:** README refinements (`#4726`), dropping a redundant unit-tests workflow (`#4748`), and general chore commits.
- **Impact:** This release is purely infrastructure and pipeline maintenance — no new user-facing features, no breaking changes, and no migration notes are included.

---

## 3. Project Progress

The project merged **18 PRs today**. Key advances:

- **Feishu Channel (Major Push):** A simplified group session configuration (`#4537` – merged), thread/reply support (`#4708` – merged), and a full card system refactoring to match WeCom/QQ patterns (`#4742` – merged). Feishu is becoming a first-class channel.
- **Agent Framework:** The new built-in tool `spawn_subagent` now allows agents to delegate ephemeral in-workspace sub-tasks (`#4806` – merged). A critical fix preserves `reasoning_content` across file blocks, preventing silent message loss (`#4728` – merged).
- **Desktop & Windows Stability:** Several long-standing packaging pain points were resolved: the CLI executable is now bundled in the desktop build for cron support (`#4779` – merged), missing Pet dependencies are auto-installed (`#4801` – merged), and Git console windows are hidden in coding mode (`#4696` – merged).
- **Developer Experience:** OpenRouter attribution headers were added for leaderboard ranking (`#4809` – merged). Coding mode now properly clears editor tabs when switching projects (`#4805` – merged).
- **Plugin System Foundation:** Infrastructure for uninstall hooks, exposed skill provider APIs, and Windows test fixes were laid down (`#4794` – merged).

---

## 4. Community Hot Topics

- **`#3224` – CoPaw Agent Teams (OPEN, 6 comments):** A long-running vision document proposing natural-language-driven, self-evolving multi-agent collaboration teams. Continues to attract discussion but lacks formal roadmap acknowledgment.
- **`#4789` – Trae-like Conversation Rollback (CLOSED, 7 comments, 1 👍):** Highly requested. Users want per-conversation delete and rollback with cascading file changes, moving beyond the monolithic sandbox model. Paired with `#4825`, this signals a strong demand for agile version control inside the agent.
- **`#4796` – Slash Skill Suggestions (OPEN, 5 comments):** Users want `/skills` or `/` to trigger tab-completion of available skills. **PR `#4810`** was opened the same day, showcasing rapid developer responsiveness.
- **`#4825` – File Change Diff-View (NEW, 1 comment):** Requesters explicitly reference Trae, demanding a clear visual diff for every `writefile` action. This is a direct signal that the community expects IDE-grade code review transparency.

---

## 5. Bugs & Stability

Active and closed issues reveal several severity tiers:

- **CRITICAL — Vector Index Bloat (`#4795`, OPEN, 2 comments):** ChromaDB indices at `~/.qwenpaw/file_store/` bloated to **37GB** over three months of normal use, causing process crashes roughly every 30 minutes. Root cause identified (`link_lists` collection). **No fix PR is linked yet** — this is the most urgent open stability problem.
- **HIGH — Tool Call Hangs (`#4739`, CLOSED):** Agent silently enters a "waiting for user input" state after tool calls complete. A core interaction loop bug.
- **HIGH — Cron Session Conflicts (`#4653`, CLOSED / `#4822`, OPEN):** Scheduled tasks are interrupted by concurrent user messages in shared sessions. A fix is actively being developed in **PR `#4822`**.
- **MEDIUM — Streaming Output Lag (`#4792`, OPEN):** Long streaming responses cause severe local client freezing, pointing to a frontend rendering bottleneck.
- **MEDIUM — Disabled Skills Reset (`#4807`, OPEN):** User preferences for disabling built-in skills (`docx`, `xlsx`) are not preserved across upgrades.
- **RESOLVED:** Desktop Pet startup failure (`#4783` → fixed by `#4801`), CLI cron path issues (`#4773` → fixed by `#4779`), Windows Defender false positive (`#3718` → closed).

---

## 6. Feature Requests & Roadmap Signals

The data strongly signals a platformization and IDE-centric roadmap:

- **Architectural Shift — AgentScope 2.0 Migration (`#4727`, OPEN, Breaking Change, 2 👍):** This maintainer-driven proposal will fundamentally re-architect CoPaw’s backend. The community should prepare for significant API and configuration changes. This is the single highest-impact item on the roadmap.
- **Platformization Accelerates:** Merged PRs (`#4794`, `#4693`, `#4804` – OPEN) add uninstall hooks, custom channel registration, and prompt section APIs. A formal plugin ecosystem is taking shape.
- **IDE Feature Parity:** Feature requests now directly benchmark against **Trae / Cursor**, asking for diff-views (`#4825`), conversation branching (`#4789`), VSCode-compatible editing (`#4759`), and in-chat file references (`#4823`). These are strong candidates for prioritization in the next minor releases.
- **Skill Lifecycle Management:** The gap between `/skills` UX (`#4796`) and preference persistence (`#4807`) suggests a larger skill management framework is needed.

---

## 7. User Feedback Summary

- **Engagement & Trust:** The community is deeply invested. They provide high-quality bug reports, competitive analysis, and feature requests. The rapid issue-to-fix cycle (e.g., `#4796` → `#4810` in one day) builds strong developer-community trust.
- **Reliability Pain Points:** Users are frustrated by data persistence failures (vector DB bloat, disabled skill resetting), background task interference (cron session sharing), and core interaction bugs (tool call hangs, streaming lag). These erode confidence in production use.
- **Desire for Transparency & Control:** A strong, recurring theme is the demand to **see, verify, and revert** agent actions. The calls for diff-views, conversation rollback, and file references show users want auditability, not just automation.
- **Windows Desktop Gap:** While the core runtime is mature, specific Windows desktop issues (subprocess handling, missing dependencies, console windows) highlight an ongoing quality gap in the desktop distribution.

---

## 8. Backlog Watch

- **`#3224` – Agent Teams (Open since Apr 10):** A major community vision document needing a formal maintainer roadmap response or prioritization signal.
- **`#4727` – AgentScope 2.0 Migration (Breaking Change, Open since May 27):** Highest impact item. The community urgently needs a deprecation timeline, migration guide, and communication plan to avoid fragmentation.
- **`#2880` – 10MB File Upload Limit (Open since Apr 3):** An old, unaddressed limitation that will increasingly block adoption for practical data-heavy workflows.
- **`#4795` – Vector Index Bloat (Critical, New):** Despite today's extreme overall activity, the lack of an immediate triage response or linked fix for this existential stability bug is a notable risk gap requiring urgent maintainer attention.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-05-30

**Data Snapshot:** 19 Issues updated (17 open, 2 closed) | 46 PRs updated (37 open, 9 merged/closed) | 0 Releases

---

## 1. Today's Overview

ZeroClaw is in a high-velocity pre-release phase, processing an enormous 46 pull requests and 19 issues in a single day. The development focus is split between integrating the ambitious v0.8.0-beta-2 feature set (new TUI, RPC socket transport, DenyWithEdit approval model) and stabilizing the v0.8.1 queue for channels, providers, and tools. While 9 PRs were merged—including significant fixes for DeepSeek V4 reasoning and provider routing—the 37 remaining open PRs and 17 active issues signal a project prioritizing rapid feature iteration. This pace, however, has introduced regressions in several mature channels (Slack, Telegram, TTS), resulting in an exceptionally high number of S1 (workflow-blocked) severity reports today.

---

## 2. Releases

No new releases were tagged today. The latest official stable version is v0.7.5, while the active documentation and development track has moved to v0.8.0-beta-1, creating some user confusion (see the documentation mismatch bug in [Bug & Stability section](#5-bugs--stability)).

---

## 3. Project Progress

The 9 PRs merged/closed today include meaningful stabilization and feature work across the stack:

- **DeepSeek V4 & Provider Routing:** A critical fix for `reasoning_content` being dropped in multi-turn conversations with DeepSeek models (#6233) landed via [PR #6284](https://github.com/zeroclaw-labs/zeroclaw/pull/6284). Provider configuration was also improved with explicit `kind` routing in [PR #6607](https://github.com/zeroclaw-labs/zeroclaw/pull/6607).

- **Agent & Memory Architecture:** A highly requested per-agent `classifier_provider` was added in [PR #6945](https://github.com/zeroclaw-labs/zeroclaw/pull/6945), allowing reply-intent classification to be routed to a cheaper model. A new `MemoryStrategy` trait was introduced in [PR #6907](https://github.com/zeroclaw-labs/zeroclaw/pull/6907), decoupling lifecycle policy from storage.

- **Tools & Networking:** IPv6 support landed for networking tools (`http_request`, `web_fetch`, `browser`) in [PR #5450](https://github.com/zeroclaw-labs/zeroclaw/pull/5450). The `web_fetch` tool correctly treats `max_response_size=0` as unlimited in [PR #6884](https://github.com/zeroclaw-labs/zeroclaw/pull/6884).

- **Channel Support:** Long-standing feature request for Wecom (WeChat Work) channel support (#3090) was closed, suggesting the integration has landed.

- **Features in Progress (Open PRs):**
  - [PR #6924](https://github.com/zeroclaw-labs/zeroclaw/pull/6924): Scoped tool elevation for built-in and MCP tools (Skills).
  - [PR #6920](https://github.com/zeroclaw-labs/zeroclaw/pull/6920): Filter deferred MCP tools by access policy.
  - [PR #6957](https://github.com/zeroclaw-labs/zeroclaw/pull/6957): New `file_download` tool for fetching remote files.
  - [PR #7014](https://github.com/zeroclaw-labs/zeroclaw/pull/7014): Runtime profiles for agent loop configuration.
  - [PR #6848](https://github.com/zeroclaw-labs/zeroclaw/pull/6848): Massive beta-2 integration (TUI, RPC, DenyWithEdit).

---

## 4. Community Hot Topics

- **MCP Tool Filtering Bug (#6699):** The most discussed issue today, with 7 comments. It identifies that `tool_filter_groups` is completely ignored for real MCP tools and lacks integration with deferred loading. Fix PRs #6920 and #6924 are now open for review. This is a critical usability and security concern for the MCP ecosystem.

- **Skills UX Tracker (#6253):** This v0.7.6 tracker explicitly invites "community input" and covers CLI, sandbox, audit, and authoring paths. It signals a coordinated push to make ZeroClaw's skill system a mature, production-grade feature.

- **Local-First Mode (#5287):** With 2 thumbs-up and steady engagement since April, this feature request for compact, privacy-preserving local model operation without prompt leakage resonates deeply with the self-hosted, privacy-focused community segment.

- **Beta-2 Integration PR (#6848):** This massive PR (spanning over 70 labels) is seeking "first round feedback" and represents the future UX direction of the project—covering the new terminal UI, RPC socket transport, and a novel "DenyWithEdit" approval paradigm.

---

## 5. Bugs & Stability

Bug reporting is exceptionally high today, with multiple S1 (workflow-blocked) bugs in core stable channels:

**S1 - Workflow Blocked**

| Issue | Component | Summary |
|---|---|---|
| [#6992](https://github.com/zeroclaw-labs/zeroclaw/issues/6992) | Slack | Slack Socket Mode rejects all incoming messages as "unauthorized user" |
| [#6999](https://github.com/zeroclaw-labs/zeroclaw/issues/6999) | Telegram | Telegram voice transcription always fails (channel never wires `transcription_provider` alias) |
| [#6997](https://github.com/zeroclaw-labs/zeroclaw/issues/6997) | Docs | Documentation covers v0.8.0-beta-1 while official release is v0.7.5 |

**S2 - Degraded Behavior**

| Issue | Component | Summary |
|---|---|---|
| [#7001](https://github.com/zeroclaw-labs/zeroclaw/issues/7001) | TTS/Config | TTS voice replies resolve the wrong agent's `tts_provider` in multi-agent configs |
| [#6991](https://github.com/zeroclaw-labs/zeroclaw/issues/6991) | Runtime/Security | Native tool serialization ignores Risk Profile and Tool Filter restrictions |
| [#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) | MCP/Tools | `tool_filter_groups` is a no-op for MCP tools + deferred loading bypass (Fix PRs #6920, #6924 open) |

**S3 - Minor Issues**

| Issue | Component | Summary |
|---|---|---|
| [#7005](https://github.com/zeroclaw-labs/zeroclaw/issues/7005) | Onboarding | Onboarding wizard bypasses Fluent i18n path (Fix PR #7012 open) |
| [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) | CLI | Backspace deletes byte-by-byte for CJK characters |

**Fixes in Progress:** Bearer token rotation fix ([PR #6988](https://github.com/zeroclaw-labs/zeroclaw/pull/6988)), WhatsApp reply targeting fix ([PR #7008](https://github.com/zeroclaw-labs/zeroclaw/pull/7008)), and GLM invalid history fix ([PR #7013](https://github.com/zeroclaw-labs/zeroclaw/pull/7013)) are all open and under review.

---

## 6. Feature Requests & Roadmap Signals

- **RFCs Defining the Architecture:**
  - [Granular Sandbox Policy (#6996)](https://github.com/zeroclaw-labs/zeroclaw/issues/6996): Proposes config-driven filesystem and network restrictions via Landlock/Bubblewrap/Seatbelt. Labeled `needs-maintainer-review`.
  - [Schema-Guided Reasoning (#6998)](https://github.com/zeroclaw-labs/zeroclaw/issues/6998): Aims to generalize structured output across all providers, superseding #4760. Labeled `needs-maintainer-review`.

- **Release Trackers:**
  - [v0.8.1 Integration Queue (#6970)](https://github.com/zeroclaw-labs/zeroclaw/issues/6970): Operational tracker for additive channels, providers, tools, and runtime work.
  - [TUI UX Tracker (#6825)](https://github.com/zeroclaw-labs/zeroclaw/issues/6825): Covers theming, keybindings, and navigation polish for the new terminal interface.

- **Prediction for v0.8.1:** Based on the active PR queue, the next release will heavily feature the scoped MCP security model (scoped tool elevation, deferred filter), runtime profiles, the `file_download` tool, and extensive channel/provider fixes. The SGR and Granular Sandbox RFCs are too large for v0.8.1 and are likely targeted for v0.9.0.

---

## 7. User Feedback Summary

- **Pain Points:** The dominant signal today is that *core channels are unstable*. Multi-agent TTS is broken (#7001), Slack Socket Mode is completely non-functional (#6992), and Telegram voice is dropped (#6999). Security-conscious users are concerned that Risk Profiles and Tool Filters can be bypassed (#6991, #6699). The documentation mismatch (#6997) is actively leading users to follow beta instructions for the stable release.

- **Use Cases:** The community is building multi-agent workspaces with TTS, relying on voice transcription in messaging channels, and testing strict MCP security policies. The "Local-First Mode" request (#5287) highlights a significant push for private, small-model deployment without feature bloat.

- **Satisfaction:** Despite the regressions, user engagement is exceptional. The quality of bug reports is very high, complete with root causes and suggested fix paths. The rapid turnaround on the DeepSeek reasoning fix (#6233 closed, #6284 merged) demonstrates strong maintainer responsiveness to provider-level issues, which builds trust with the developer community.

---

## 8. Backlog Watch

Several significant items require maintainer attention or strategic decisions:

- **Audit: 153 Lost Commits (#6074):** Created April 24. Tracks commits lost in a bulk revert (`c3ff635`). Critical technical debt needing an ownership decision or recovery strategy. P2, `status:in-progress` but stalled.

- **ARM64 Docker Support (#5187):** PR opened April 2. Blocked on `needs-author-action`. Critical for native ARM deployments. Ready for a maintainer nudge or takeover.

- **RFCs Awaiting Maintainer Review:** Both the [Granular Sandbox (#6996)](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) and [Schema-Guided Reasoning (#6998)](https://github.com/zeroclaw-labs/zeroclaw/issues/6998) RFCs carry the `needs-maintainer-review` label. These are architectural decisions that will define the next 1–2 major releases and need a response to validate community direction.

- **Local-First Mode (#5287):** Open since April 4. P2 with strong user sentiment (2 👍, 3 comments). Needs a roadmap commitment or milestone assignment to signal priority.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*