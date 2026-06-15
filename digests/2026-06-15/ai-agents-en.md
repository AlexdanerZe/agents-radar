# OpenClaw Ecosystem Digest 2026-06-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-15 03:56 UTC

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

# OpenClaw Project Digest — 2026-06-15

---

## 1. Today's Overview

OpenClaw continues to show exceptionally high community and development velocity, with **500 issues and 500 pull requests updated in the past 24 hours**, alongside a new beta release (`v2026.6.8-beta.1`). However, this pace has introduced significant stability headwinds: the majority of top-commented and most-reacted issues are regressions tied to the rapid `v2026.5.20` → `v2026.5.22` → `v2026.6.1` update cycle. The **Codex app-server harness** remains the single largest source of user friction, producing session wedging, silent truncation, and OAuth timeline failures. Message duplication on Telegram and `EmbeddedAttemptSessionTakeoverError` failures on Discord dominate the community discussion, indicating that delivery reliability has become the project's most pressing concern. At the same time, community architectural proposals (context-aware continuation, gateway-lite mode, Tree-sitter command authorization) show a deeply engaged power-user base investing in the platform's long-term direction.

---

## 2. Releases

**New: `v2026.6.8-beta.1`** — [Release Notes](openclaw/openclaw Releases v2026.6.8-beta.1)

This release is a **targeted channel-delivery stabilization patch**:

- **Telegram:** Structured rich-text sending (tables, lists, expandable blockquotes), prompt-preserving CLI backend delivery, retired native draft migration, and safer rich-media boundary handling.
- **WhatsApp:** Described as "richer and less brittle" channel delivery.
- **No breaking changes or migration notes** are reported in the highlights, though users should be aware this beta sits atop the `2026.6.x` branch where the DeepSeek Prompt Cache regression (`#91016`) was introduced.

---

## 3. Project Progress

Of the ~84 merged/closed PRs today, key closures include:

### Merged/Closed Fixes
- **Telegram delivery ledger fix** — `#93148`: `fix(telegram): record every sent message in the SQLite db` (by Andrew882024). Successful sends were not being persisted to the sent-message ledger.
- **Telegram spooled update resilience** — `#93014`: `fix(telegram): dead-letter ERR_MODULE_NOT_FOUND spooled updates` (by Coder-Wangyankun). Prevents infinite retry loops on unresolvable module errors.
- **iMessage reply actions** — `#93137`: `fix(imessage): honor disabled reply actions` (by omarshahine, closes `#92142`).
- **Closed issues**: `#86184` (Telegram fallback after successful tool turn), `#84137` (Codex post-tool semantics), `#83425` (xAI OAuth redirect_uri), `#86231` (Codex latency tracking), `#86090` (heartbeat phantom runs), `#85692` (Feishu silent replies), `#85192` (DeepSeek V4 thinking-block detection), `#83419` (group chat consecutive user roles).

### Active PRs Nearing Completion
- `#85651`: Context-pressure-aware continuation (`continue_work`/`continue_delegate`/`request_compaction`) — **status: ready for maintainer look**.
- `#92340`: Feishu VC meeting invite handler — **status: ready for maintainer look**.
- `#93117`: Anthropic thinking-block recovery after control-plane start event — **new, seeking proof**.
- `#83933`: `fix(cron)`: preserve counters for manual runs of `deleteAfterRun` jobs.
- `#83612`: Codex workspace prompt routing made user-selectable.
- `#93114`: Migration of five RFC #10 scripts into QA-lab e2e tests.

---

## 4. Community Hot Topics

The following issues dominated community engagement today, revealing deep concern with session reliability and Codex integration stability:

| Issue | Comments | Reacts | Theme |
|---|---|---|---|
| [#85888](openclaw/openclaw Issue #85888) — MiniMax 503 failures (05:00–07:30 CST) | 12 | 👍 1 | Cron scheduling logic suspect over API availability |
| [#84516](openclaw/openclaw Issue #84516) — Codex replies **silently truncated** at ~1000 chars | 11 | 👍 2 | High-severity silent data loss, `stopReason=null`, `aborted=false` |
| [#86519](openclaw/openclaw Issue #86519) — Duplicate Telegram replies (10x after 5.20, 2-3x after 5.22) | 9 | 👍 1 | Regression cluster from 5.20 update |
| [#86508](openclaw/openclaw Issue #86508) — `EmbeddedAttemptSessionTakeoverError` on Discord | 9 | 👍 4 | Session takeover error cluster, 4 upvotes |
| [#86996](openclaw/openclaw Issue #86996) — Active Memory + Codex path → hook timeouts & event-loop stalls | 9 | 👍 1 | Brokerage collapse under heavy memory backend |
| [#91016](openclaw/openclaw Issue #91016) — DeepSeek Prompt Cache完全失效，~$6/hr cost spike | 5 | 👍 5 | Highest reaction ratio; Chinese-community report of Prompt Cache broken post-2026.6.1 |
| [#84903](openclaw/openclaw Issue #84903) — Single stalled session blocks entire Gateway event loop | 8 | 👍 2 | Fundamental architecture isolation failure |
| [#85030](openclaw/openclaw Issue #85030) — MCP tools not injected into subagent (`sessions_spawn`) | 8 | 👍 3 | Blocks MCP-based multi-agent workflows |
| [#86047](openclaw/openclaw Issue #86047) — Codex app-server plugin approval stalls in Nextcloud Talk | 8 | 👍 3 | Codex harness regression breaking group sessions |

**Underlying need:** Users are demanding **session isolation guarantees**, **reliable delivery confirmation**, and **observable failure modes** (no more silent drops or truncations). The Codex harness, while architecturally promising, is degrading the baseline reliability that users expect from gateway channels.

---

## 5. Bugs & Stability

Stability is the dominant theme of today's digest. Regressions from the `2026.5.20` → `2026.5.22` → `2026.6.1` releases remain uncontained.

### Critical / P0–P1 Severity

| Issue | Severity | Short Description | Fix PR Exists? |
|---|---|---|---|
| [#84882](openclaw/openclaw Issue #84882) | **P0** | `memory-core` Dreaming silently deletes `memory/YYYY-MM-DD.md` files | No (`needs-maintainer-review`) |
| [#84516](openclaw/openclaw Issue #84516) | P1 | Codex silent truncation at ~1K chars | No (`needs-product-decision` + `needs-live-repro`) |
| [#86519](openclaw/openclaw Issue #86519) | P1 | Duplicate replies 2-10x on Telegram (regression) | No (partial fix in 5.22, not resolved) |
| [#86508](openclaw/openclaw Issue #86508) | P1 | `EmbeddedAttemptSessionTakeoverError` on Discord | No (`needs-live-repro`) |
| [#84903](openclaw/openclaw Issue #84903) | P1 | Single stalled session blocks entire Gateway | No |
| [#86827](openclaw/openclaw Issue #86827) | P1 | Group chat stuck in `failed` state silently drops messages | No |
| [#85030](openclaw/openclaw Issue #85030) | P1 | MCP tools not injected into subagent sessions | No |
| [#86047](openclaw/openclaw Issue #86047) | P1 | Codex plugin approval stalls → tool timeouts | No |

### Medium Severity (P2)

- [#87109](openclaw/openclaw Issue #87109): Gateway heap memory grows to 1GB+ at idle on macOS, cron jobs fail silently under pressure.
- [#86215](openclaw/openclaw Issue #86215): Codex OAuth refresh failures wedge an agent for hours without alerting.
- [#86214](openclaw/openclaw Issue #86214): Codex app-server client closes mid-turn during image/tool requests with large SQLite logs.
- [#85103](openclaw/openclaw Issue #85103): Model fallback chain not triggered on provider-wide quota exhaustion.
- [#86063](openclaw/openclaw Issue #86063): Anthropic 1h cache invalidated every turn by metadata strip + `cache_control` field movement.
- [#86845](openclaw/openclaw Issue #86845): `EmbeddedAttemptSessionTakeoverError` cluster — 13 events in 42h across 7 jobs.
- [#91016](openclaw/openclaw Issue #91016): DeepSeek V4 Flash Prompt Cache完全失效 after 2026.6.1 upgrade (~$6/hr cost impact).

### Notable Closed Stability Issues
- `#86184` (Telegram fallback after tool turn) — closed.
- `#83419` (Group chat consecutive user roles breaks Anthropic API) — closed.
- `#85192` (DeepSeek V4 thinking-block detection) — closed.

---

## 6. Feature Requests & Roadmap Signals

The community is signaling a desire for **greater deployment flexibility** and **agent autonomy**.

### High-Impact Feature Requests Today

| Issue | Title | Significance |
|---|---|---|
| [#86881](openclaw/openclaw Issue #86881) | **Gateway-lite mode without AI harness** | Community member requests a deterministic-only deployment mode (webhooks, cron, plugins) without loading an AI harness. Suggests platform/enterprise use case. |
| [#85651](openclaw/openclaw PR #85651) | Context-pressure-aware continuation | PR proposes agents self-elect to continue, delegate, or request compaction. High-architecture feature. |
| [#74077](openclaw/openclaw Issue #74077) | Slash command to set streaming mode per session | Stale P3 but consistently updated; users want per-chat streaming control without gateway restart. |
| [#85461](openclaw/openclaw Issue #85461) | Capture image-generation usage metadata | Cost tracking for image gen providers. |
| [#44395](openclaw/openclaw Issue #44395) | Heading-aware chunking + entity extraction for memory search | Memory quality improvement with semantic structure awareness. |

### Roadmap Predictions
- **Context-aware agent continuation** (`#85651`) has strong design docs and is in advanced PR stage — likely for `v2026.7.x`.
- **Gateway-lite mode** (`#86881`) could appear as a configuration flag in an upcoming stable release if maintainers prioritize deployment ergonomics.
- **Tree-sitter command authorization refactor** (`#84172`, `#84118`) is deep in development and represents a major security boundary rewrite for the exec pipeline.
- **Codex workspace prompt surface configurability** (`#83612`) is nearly merge-ready, giving users explicit control over a previously hardcoded optimization.

---

## 7. User Feedback Summary

### What Users Are Loving
- Deep willingness to engage with **complex architectural discussions** (ALS scoping, event-loop isolation, MCP injection patterns).
- High adoption of **multi-model fallback chains** and **Active Memory** — users are pushing the system to its limits.
- Strong **global community signal** — Chinese-language bug reports (CST timelines, DeepSeek cache issues) show international deployment depth.

### What Users Are Frustrated By

1. **Update regression churn.** The rapid cadence (5.12 → 5.20 → 5.22 → 5.28 → 6.1) is introducing regressions faster than they can be resolved. The DeepSeek Prompt Cache regression (`#91016`) costing ~$6/hr is a vivid example of this pain.
2. **Silent data loss.** The P0 memory deletion bug (`#84882`), the silent truncation bug (`#84516`), and the group-chat silent message drops (`#86827`) erode trust.
3. **Codex harness readiness.** Early adopters are encountering too many friction points (wedge states, OAuth failures, import errors, latency). The feature feels beta and isn't matching the gateway's historically higher baseline reliability.
4. **Diagnostic gaps.** Users consistently report bugs where "no error is logged" or "no message is surfaced to the user." Heartbeat phantom runs (`#86090`) and the `payloads=0` issue (`#84569`) are examples of opaque failure modes.

### Satisfaction Indicators
- Despite the bugs, users are filing detailed, structured reports with logs, traces, and timelines.
- 8+ comments on most top issues indicates engaged, collaborative debugging.
- The presence of a `clawsweeper` automated triage system and heavy use of structured tags (`impact:*`, `issue-rating:*`) reflects strong project governance.

---

## 8. Backlog Watch

Several critical items remain in waiting states without maintainer resolution, despite being updated today:

| Issue/PR | Age (from first appearance) | Status | Concern |
|---|---|---|---|
| [#84882](openclaw/openclaw Issue #84882) — **P0: memory-core silently deletes daily files** | 2026-05-21 (25 days) | `needs-maintainer-review` | Silent data loss. Only `clawsweeper` triage, no fix shape. |
| [#45494](openclaw/openclaw Issue #45494) — **P1: Cron jobs silently timeout instead of fast-failing** | 2026-03-13 (94 days) | `needs-maintainer-review` + `needs-product-decision` | Open for 3 months. Core cron reliability bug. |
| [#85030](openclaw/openclaw Issue #85030) — **P1: MCP tools not injected into subagent sessions** | 2026-05-21 (25 days) | `needs-maintainer-review` + `needs-security-review` | Blocking MCP ecosystem growth. |
| [#83964](openclaw/openclaw Issue #83964) — **P1: `@openclaw/codex` package resolution failure** | 2026-05-19 (27 days) | `needs-maintainer-review` + `needs-product-decision` | Basic dependency resolution bug in new Codex path. |
| [#77467](openclaw/openclaw Issue #77467) — **P1: MiniMax Portal OAuth cannot auto-refresh** | 2026-05-04 (42 days) | `needs-maintainer-review` | Token refresh not implemented — users hit "No credentials found" every 2 hours. |
| [#85192](openclaw/openclaw Issue #85192) — **DeepSeek V4 thinking-block detection mismatch** | 2026-05-22 | **Closed** | Closed stale, but `#91016` (Prompt Cache失效) suggests unresolved tension in the DeepSeek provider path. |
| [#86342](openclaw/openclaw Issue #86342) — **MissingAgentHarnessError race** | 2026-05-25 (21 days) | `needs-product-decision` + `needs-live-repro` | 28 incident windows in 72h — affects Discord lane spawning. |

**Callout:** The number of P1/P2 items stuck on `clawsweeper:needs-maintainer-review` or `needs-product-decision` suggests that despite strong automation, human maintainer attention is the primary bottleneck in resolving the current regression wave.

---

## Cross-Ecosystem Comparison

# Ecosystem Cross-Project Comparison Report
**Date:** 2026-06-15
**Scope:** Open-source Personal AI Agent / Assistant Projects

---

## 1. Ecosystem Overview

The open-source personal AI agent landscape on June 15, 2026, is defined by explosive growth tempered by a deepening reliability crisis. The largest projects—OpenClaw, IronClaw, and ZeroClaw—are operating at generational scale, processing hundreds of issues and PRs daily, but a clear trust gradient has emerged between volatile high-velocity projects and those prioritizing stabilization. Security is rapidly formalizing as a competitive differentiator, with independent audits surfacing across the ecosystem (IronClaw, NanoClaw) and raising the baseline for tool execution safety. Meanwhile, the user base is becoming more sophisticated and demanding: enterprise compliance features (NullClaw), "bring your own subscription" integrations, and mobile/edge deployment support are no longer aspirational but expected. The CLI-only era is ending; the WebUI/Desktop is the new product interface, and context management is the decisive technical battleground for long-running autonomous agents.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed (24h) | Latest Release | Ecosystem Health |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | ~84 PRs | v2026.6.8-beta.1 | **Strained** (Regression wave, maintainer bottleneck) |
| **ZeroClaw** | 42 | 50 | 28 Issues, 4 PRs | N/A | **Overdrive** (Feature velocity, scaling challenges) |
| **IronClaw** | 42 | 45 | 15 PRs, 7 Issues | Draft v0.29.1 | **Churning** (Reborn architecture migration) |
| **Hermes Agent** | 50 | 50 | 8 Issues, 7 PRs | v0.16.0 | **Strained** (Throughput gap, 50 open PRs) |
| **NanoBot** | High | 46 | 27 PRs | N/A | **Strong** (Fast bug fixes, excellent merge hygiene) |
| **CoPaw** | 24 | 16 | 5 PRs, 6 Issues | v1.1.11.post2 | **Strained** (Tauri/regression pain) |
| **NanoClaw** | 7 | 10 | 5 PRs | N/A | **Dynamic** (Architecture pivot, security audit) |
| **PicoClaw** | Low | 9 | 5 PRs | v0.2.9-nightly | **Stable** (Maintenance mode) |
| **LobsterAI** | Low | Low | 2 PRs | N/A | **Consolidating** (UX hardening) |
| **NullClaw** | 1 | 0 | 0 | N/A | **Dormant / Low** |
| **Moltis** | 1 | 0 | 0 | N/A | **Plateaued** |
| **TinyClaw** | 0 | 0 | 0 | N/A | **Inactive** |
| **ZeptoClaw** | 0 | 0 | 0 | N/A | **Inactive** |

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Undisputed Community Scale:** At 500 issues and PRs updated daily, OpenClaw commands roughly 10x the raw traffic of its nearest competitors (IronClaw, ZeroClaw). This drives unmatched ecosystem depth, RFC quality, and integration coverage.
- **Architectural Leadership:** The Codex app-server harness and Active Memory concepts are uniquely ambitious and are being directly replicated (NanoClaw's Codex v2 payload). The Tree-sitter command authorization and Gateway-lite mode proposals indicate the deepest architectural thinking in the space.
- **Global Depth:** Strongest multi-language community, with substantial Chinese-language bug reports (DeepSeek cache, MiniMax outages) demonstrating international enterprise deployment.

**Disadvantages vs Peers:**
- **Reliability Fragility:** The rapid `5.20 → 5.22 → 6.1` cycle has produced a regression wave unrivaled in the ecosystem. NanoBot fixed an Anthropic API break in hours; OpenClaw's DeepSeek cache regression (`#91016`) costs users ~$6/hr and remains unpatched.
- **Maintainer Bandwidth Gap:** Despite automated triage (`clawsweeper`), critical P0/P1 issues sit for weeks (P0 memory deletion `#84882`, 25 days stale; MCP injection `#85030`, 25 days stale). Smaller projects respond faster.
- **Complexity Tax:** The Codex harness, while powerful, generates a disproportionate share of user friction (silent truncation, OAuth failures, session wedging). Projects like NanoBot deliver a more polished out-of-box experience.
- **Session Isolation Deficit:** A single stalled session can block the entire Gateway event loop (`#84903`), a fundamental architectural weakness that IronClaw and ZeroClaw are actively addressing in their newer stacks.

**Bottom Line:** OpenClaw remains the standard against which all are measured, but its advantage in breadth is eroding as competitors close the feature gap while maintaining higher baseline stability.

---

## 4. Shared Technical Focus Areas

**1. Session & Gateway Reliability (ALL Top Projects)**
- **OpenClaw:** Session takeover errors (`#86508`), gateway event loop blocking (`#84903`).
- **Hermes:** Silent cron orphans (`#32091`), Matrix E2EE message drop (`#46310`).
- **IronClaw:** Input ref scoping failures (`#4887`), activity cancellation leaks (`#4889`).
- **CoPaw:** Infinite conversation loops (`#5162`), ghost session resurrection (`#1465`).
- **Shared Requirement:** Concurrent session isolation, observable failure modes, and guaranteed delivery confirmation.

**2. Model Provider & API Fragility (OpenClaw, NanoBot, CoPaw, ZeroClaw)**
- **OpenClaw:** DeepSeek Prompt Cache broken (`#91016`), cost spike.
- **NanoBot:** Anthropic Opus 4-8 parameter regression (`#4333`).
- **CoPaw:** Gemini tool calling completely broken (`#5163`).
- **Shared Requirement:** Provider-agnostic fallback chains, transparent token/cost tracking, and prompt cache reliability across model updates.

**3. Security Hardening (IronClaw, NanoClaw, Hermes, ZeroClaw)**
- **IronClaw:** 4 coordinated shell approval bypass vectors (wrapper, `sort`, auto-approval).
- **NanoClaw:** 3 critical disclosures (file exfiltration, webhook bypass, MCP args persistence).
- **Hermes:** Credential exfiltration via read_file (`#46411`), sibling profile contamination.
- **Shared Requirement:** Granular approval gates, sandboxed execution, and audit-logged tool operations.

**4. Desktop / WebUI Maturation (NanoBot, CoPaw, IronClaw, Hermes)**
- **NanoBot:** Mobile responsiveness overhaul, config.json parity.
- **CoPaw:** 10-minute Tauri startup times, Computer Use (UIA).
- **IronClaw:** Extension setup UX fragmentation, Slack as extension.
- **Shared Requirement:** First-class GUI with session persistence, extension management, and mobile support.

**5. Long-Context & Memory Management (OpenClaw, CoPaw, Hermes, NanoClaw)**
- **OpenClaw:** Active Memory + Codex path causes event loop stalls (`#86996`); dreaming silently deletes memory files (`#84882`).
- **CoPaw:** Context compression destroys persona/task context (`#5171`).
- **Hermes:** Request for background memory as context (`#31584`), context compression failure handler.
- **Shared Requirement:** Non-destructive, predictable context management with clear user visibility into memory state.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | NanoBot | Hermes | CoPaw |
|---|---|---|---|---|---|---|
| **Target User** | Dev building custom gateways | Power user wanting max connectivity | Enterprise / professional dev | Power user wanting polished WebUI | Researcher / hacker | Desktop productivity user |
| **Core Strength** | Ecosystem depth, RFCs, Codex | Connectivity velocity, community merge | Security, extension SDK, enterprise | Merge discipline, UX quality | Multi-model autonomy, TUI | Desktop/Computer Use, Chinese channels |
| **Primary Weakness** | Regression churn, maintainer bottleneck | Provider fragility, TOML config complexity | WebUI churn, Reborn migration bugs | Smaller ecosystem size | Trust controversies, throughput gap | Tauri performance, regression density |
| **Architecture** | Monolithic Gateway + Codex harness | Micro-config driven | Modular Reborn stack + extension system | Fast iterative refactoring | Plugin-heavy, Docker s6 | Tauri Desktop + pluggable backend |
| **Geographic Strength** | Global (strong CN community) | Global | Global | English-primary | English-primary | China-dominant (WeChat/DingTalk) |
| **Security Posture** | Reactive (vulnerabilities pending) | Scaling (risk profiles under debate) | **Proactive (formal audits)** | Responsive (fast patches) | Reactive (exposure incidents) | Reactive (plugin vulnerabilities) |

**Key Takeaway:** No single project dominates all dimensions. OpenClaw owns breadth. IronClaw owns security. ZeroClaw owns velocity. NanoBot owns UX polish. CoPaw owns the desktop. The ecosystem is effectively partitioning by architectural philosophy and primary user persona.

---

## 6. Community Momentum & Maturity

**Tier 1: Hypergrowth / High Churn (Risk Capital Investing)**
- **OpenClaw:** Massive scale, breaking as fast as it builds. The v2026.6.x series is the ecosystem's proving ground but exacts a heavy reliability tax.
- **ZeroClaw:** Explosive expansion through community contributions (28 issues closed, massive provider/channel batch). Risk of quality dilution from merge velocity.
- **IronClaw:** Active Reborn architecture transition. High feature activity but UX fragmentation from migration debt. The dogfooding initiative (`#4878`) signals strong internal confidence.

**Tier 2: Stabilization & Hardening (Reliability-Focused)**
- **NanoBot:** Best project hygiene observed. 27 PRs merged, including targeted architectural refactors. Model-level bugs fixed within hours. Setting the standard for responsive maintenance.
- **Hermes Agent:** Resolved major controversies (Parallel.ai routing, truncation bug), but 50 open PRs indicate a growing review debt. Platform support gaps (Windows Cron, SimpleX) need attention.
- **CoPaw:** Addressing v1.1.11.post2 regressions. High community engagement but the Tauri desktop migration is causing the most pain.

**Tier 3: Focused Maintenance / Niche**
- **PicoClaw:** Low volatility, targeted stability patches. The `--remote` WebSocket mode indicates a strategic focus on edge/client-server deployments.
- **LobsterAI:** Consolidating Artifacts and Cowork features. Waiting for the next coordinated release.
- **NanoClaw:** In a critical security-driven pivot. The operator-driven provider framework and Codex v2 merge are significant, but the three critical vulns demand immediate remediation.

**Tier 4: Dormant / Signaling**
- **NullClaw, Moltis, TinyClaw, ZeptoClaw:** Minimal to no development activity. NullClaw's single Azure identity request and Moltis's edge compression proposal are valid signals for their niches, but execution risk is high. These projects function more as proof-of-concepts than active platforms.

---

## 7. Trend Signals

**1. The Trust Deficit is Monetizable**
The frequency of "silent data loss" (OpenClaw P0 memory deletion, CoPaw ghost sessions, Hermes silent message drops) is the ecosystem's most urgent vulnerability. Projects that invest in **observable failure modes** (surface errors to users, log trace context) and **predictable session isolation** will capture the enterprise and professional market segments. The DeepSeek cache regression costing $6/hr is a stark example of invisible costs eroding trust.

**2. Security is the New Performance Battle**
The simultaneous, independent security disclosures targeting tool execution boundaries (IronClaw shell audit, NanoClaw MCP/webhook bypasses, Hermes credential leaks) signal that formal security research has entered the AI agent space. The winner of the next market phase will be the project that can prove **granular, auditable, per-invocation approval floors** for tool execution. IronClaw's proactive posture here is a strategic advantage.

**3. Context Management is the Core Algorithmic Moat**
The ecosystem is universally struggling with long-running agent tasks. Current memory solutions (Active Memory, Dreaming, Context Compression) are generating novel, high-severity bugs (P0 file deletions, context wipeouts). The project that delivers **non-destructive, verifiable, and user-transparent context optimization** will unlock the autonomous agent workflow segment.

**4. "BYO Subscription" is the Distribution Strategy**
The demand for direct OAuth integration with Claude, Kimi, and other endpoint providers (Hermes `#25267`, CoPaw `#5156`) reflects a user base unwilling to pay a middleman proxy markup. Projects that provide seamless, first-class support for **existing user subscriptions** to API providers will achieve faster adoption and lower user acquisition friction.

**5. Community Review is the Bottleneck**
Across OpenClaw (P1 issues stuck 25+ days), Hermes (50 open PRs), ZeroClaw (stale April PRs), the rate of community contribution exceeds the rate of maintainer review. The ecosystem is **supply-constrained on qualified human reviewers**. Automated triage is table stakes; the next frontier is automated code validation and intelligent merge assistance. Projects that solve this scale their community exponentially; those that don't face contributor demoralization.

**6. Mobile and Edge are the Latent Growth Vectors**
PicoClaw's WebSocket remote mode and Moltis's pure-Rust Turbovec proposal point toward a growing interest in deploying agents on constrained devices. As hardware improves and on-device models mature, the "agent on your phone" or "agent in your IoT device" will become a significant use case, favoring projects with small footprints and flexible client-server splits.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the structured English NanoBot project digest for **2026-06-15**.

---

## NanoBot Project Digest: 2026-06-15

### 1. Today’s Overview
Project activity is exceptionally high, with 46 pull requests updated and 27 merged/closed in the last 24 hours. The majority of this velocity is driven by core maintainer `chengyongru`, executing a sweeping campaign of architectural refactoring, stability fixes, and WebUI feature expansion. While no new release was cut, the sheer volume of merged work—ranging from breaking the tool-config import cycle to fixing Anthropic API regressions—suggests the codebase is being aggressively hardened for a future milestone. Project health appears strong, balancing the rapid delivery of new features with an equally rapid response to user-reported bugs.

### 2. Releases
**None.** No new releases were published in this period. Given the high number of merged PRs today, a significant release bundling these changes may be expected soon.

### 3. Project Progress (Merged / Closed PRs)
The project saw a massive wave of changes integrated into the `main` branch. Key advancements include:

- **Architecture & Refactoring:** The tool configuration schema was broken out to eliminate runtime import cycles ([PR #4314](https://github.com/HKUDS/nanobot/pull/4314)). The Feishu channel SDK was lazy-loaded to prevent worker thread conflicts ([PR #4277](https://github.com/HKUDS/nanobot/pull/4277)).
- **Agent Loop Reliability:** Finalization logic was added to ensure users get a clear message when `max_tool_iterations` is hit without tools ([PR #4269](https://github.com/HKUDS/nanobot/pull/4269)). Recent history is now strictly scoped by session to avoid context cross-contamination ([PR #4274](https://github.com/HKUDS/nanobot/pull/4274)). Cron jobs were bound to concrete sessions for better isolation ([PR #4299](https://github.com/HKUDS/nanobot/pull/4299)).
- **New Configuration Options:** A `tools.exec.pathPrepend` config was added for PATH lookup control ([PR #4273](https://github.com/HKUDS/nanobot/pull/4273)). A new `tools.file.enable` toggle was introduced to mirror the existing `exec`/`web` enable flags ([PR #4138](https://github.com/HKUDS/nanobot/pull/4138)).
- **WebUI & UX:** The WebUI received a major pass on mobile responsiveness, fixing layout overflows and spacing ([PR #4339](https://github.com/HKUDS/nanobot/pull/4339)). Token usage heatmap rendering was fixed to respect the configured timezone ([PR #4248](https://github.com/HKUDS/nanobot/pull/4248)). Desktop restart token and WebSocket replay gaps in the native engine were closed ([PR #4210](https://github.com/HKUDS/nanobot/pull/4210)).
- **Validation & Error Handling:** The system now fails fast on corrupt or invalid config files instead of silently misbehaving ([PR #4275](https://github.com/HKUDS/nanobot/pull/4275)).
- **Documentation:** Onboarding docs were reworked to help beginners choose the right setup path, and outdated "nightly branch" guidance was removed from both docs and CI ([PR #4177](https://github.com/HKUDS/nanobot/pull/4177), [PR #4245](https://github.com/HKUDS/nanobot/pull/4245)).

### 4. Community Hot Topics
The most active discussions and developments revolve around the WebUI transition and subtle agent loop failures:

- **WebUI as Primary Interface:** The open PR for WebUI / `config.json` parity ([PR #4313](https://github.com/HKUDS/nanobot/pull/4313) by `La-Volpe`) and the new Automation Management view ([PR #4330](https://github.com/HKUDS/nanobot/pull/4330) by `chengyongru`) represent the community’s push for a full GUI. This is the dominant theme across recent work.
- **Config & Agent Boundary Refactor ([PR #4344](https://github.com/HKUDS/nanobot/pull/4344)):** This open PR by `chengyongru` is silently one of the most critical changes, isolating tool config models from side effects. This deep architectural work signals preparation for a stabler third-party plugin ecosystem.
- **Subagent Injection Bug ([PR #4293](https://github.com/HKUDS/nanobot/pull/4293) by `yorkhellen`):** A fix for cron jobs that spawn subagents failing to inject results mid-turn. This highlights complex user workflows that rely on the agent loop scheduling.

### 5. Bugs & Stability
Three notable bugs were addressed or reported today, ranked by severity:

- **🔴 High (Fixed): Anthropic API Blocked on Opus 4-8** — The Anthropic provider was sending the deprecated `temperature` parameter to `claude-opus-4-8`, causing a `400` error on every request ([Issue #4333](https://github.com/HKUDS/nanobot/issues/4333)). Resolved.
- **🟡 Medium (Fix Pending): Image Fallback Hallucination & Path Leak** — A newly reported bug ([Issue #4345](https://github.com/HKUDS/nanobot/issues/4345) by `BearMett`) reveals that the provider-agnostic image stripping fallback inserts the raw file path into the conversation text, causing the model to hallucinate seeing the image. A fix PR is already open ([PR #4346](https://github.com/HKUDS/nanobot/pull/4346)).
- **🟢 Minor (Fixed): Telegram Fenced Code Blocks** — Long messages with code blocks were split mid-fence, corrupting the output ([Issue #4250](https://github.com/HKUDS/nanobot/issues/4250)). Resolved.
- **🟢 Minor (Fixed): Bot Icon Not Displayed on Start** — The `botIcon` was not shown upon initial entry into agent mode ([Issue #4262](https://github.com/HKUDS/nanobot/issues/4262)). Resolved.
- **🟠 Watch Item (Open): Zero Token Usage in API** — Issue [#4309](https://github.com/HKUDS/nanobot/issues/4309) regarding `/v1/chat/completions` always returning `0` for usage tokens remains open. This is a compliance and reporting issue for anyone integrating with the OpenAI-compatible server.

### 6. Feature Requests & Roadmap Signals
The project trajectory is clearly focused on **WebUI self-sufficiency** and **architectural modularity**:

- **WebUI is the New CLI:** The merging of config parity features ([PR #4313](https://github.com/HKUDS/nanobot/pull/4313)) and the addition of the Automation Management view ([PR #4330](https://github.com/HKUDS/nanobot/pull/4330)) strongly suggest the next version will heavily push the WebUI as a fully equivalent alternative to editing `config.json` by hand.
- **Strict Input Validation:** A new open PR ([PR #4343](https://github.com/HKUDS/nanobot/pull/4343)) enforces `additionalProperties: false` on built-in tool parameters. Expect the next release to be stricter about catching tool-call typos early instead of silently swallowing them.
- **Mobile Adoption:** The mobile responsiveness fixes ([PR #4339](https://github.com/HKUDS/nanobot/pull/4339)) signal a strategic priority to make the WebUI functional on phones, lowering the bar for on-the-go interaction.

### 7. User Feedback Summary
Real user pain points and use cases are driving the current development sprint:

- **Developer API Users:** The zero-usage token bug ([Issue #4309](https://github.com/HKUDS/nanobot/issues/4309) by `alx1379`) is the most significant dissatisfaction point for developers using NanoBot as a back-end service.
- **Model-Specific Breakage:** Users are hitting hard blocks with specific model versions (Anthropic Opus 4-8 in [Issue #4333](https://github.com/HKUDS/nanobot/issues/4333)).
- **Data Integrity:** The detailed bug report on image stripping causing the model to hallucinate file paths ([Issue #4345](https://github.com/HKUDS/nanobot/issues/4345) by `BearMett`) indicates a high level of user sophistication and concern about prompt injection and data leak vectors.
- **Satisfaction with Velocity:** The rapid response to the Telegram code block bug ([Issue #4250](https://github.com/HKUDS/nanobot/issues/4250)) and the `botIcon` startup issue ([Issue #4262](https://github.com/HKUDS/nanobot/issues/4262)) demonstrates a user base that is generally satisfied with the maintainers’ responsiveness.

### 8. Backlog Watch
While most items are moving quickly, a few important issues and community PRs require active attention:

- **[Open Issue #4309 — Zero Token Usage](https://github.com/HKUDS/nanobot/issues/4309):** This is the oldest open issue in the current data window (3 days old) and directly impacts API compatibility. It requires prioritization to maintain trust in the `serve` feature.
- **[Open PR #4293 — Subagent Pending Queue](https://github.com/HKUDS/nanobot/pull/4293):** Submitted by community member `yorkhellen`, this fix for cron + subagent result injection is critical for agent loop reliability but is currently pending review/merge from the core team.
- **[Open PR #4343 — Strict Tool Validation](https://github.com/HKUDS/nanobot/pull/4343):** A defensive programming improvement from `yu-xin-c` that builds strict validation for built-in tools. Needs review to see if it introduces any breaking behavior.
- **General Observation:** The project is currently very "maintainer-driven." The massive volume of PRs from `chengyongru` may create a bottleneck for review of external contributions like [#4293](https://github.com/HKUDS/nanobot/pull/4293) and [#4343](https://github.com/HKUDS/nanobot/pull/4343) if maintainer bandwidth is fully absorbed by core features.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 15, 2026.

---

## Hermes Agent Project Digest | 2026-06-15

### 1. Today’s Overview
Hermes Agent logged extremely high activity on June 15, with **50 Issues** and **50 Pull Requests** updated in the last 24 hours. Despite this volume, throughput remains strained: the project saw only **8 issues closed** and **7 PRs merged** against **42 open issues** and **43 open PRs**. No new releases were cut today. The development team appears focused on stabilizing the Docker/s6 runtime environment and closing out a cluster of high-profile community controversies, while the community continues to push hard on reliability, security auditing, and platform support.

### 2. Releases
No new versions were published on 2026-06-15. The most recent release remains v0.16.0 (2026.6.5).

### 3. Project Progress

**Merged/Closed PRs (from top 20):**
- **Docker/s6 Lifecycle** – [`#46291`](https://github.com/NousResearch/hermes-agent/pull/46291): Fixes gateway log parent ownership to prevent s6-log mkdir/lock loops for late-added profile services.
- **TUI Stability** – [`#39840`](https://github.com/NousResearch/hermes-agent/pull/39840): Fixes an embedded dashboard `/chat` crash when the gateway transport is not yet ready.
- **Terminal Backend** – [`#46399`](https://github.com/NousResearch/hermes-agent/pull/46399): Mirrors the Docker env-passthrough fallback to the local backend so variables in `~/.hermes/.env` are honored.
- **Telegram Platform** – [`#46438`](https://github.com/NousResearch/hermes-agent/pull/46438): Adds an opt-in `sendRichMessage` fast path so tables, task lists, and headings render natively via Bot API 10.1.

**Resolved Community Issues:**
- [`#7237`](https://github.com/NousResearch/hermes-agent/issues/7237) (46 comments) – The long-running **Response truncated due to output length limit** bug was closed.
- [`#45058`](https://github.com/NousResearch/hermes-agent/issues/45058) (15 👍) – The **Parallel.ai silent routing** controversy was resolved, likely introducing an opt-in flow.
- [`#45258`](https://github.com/NousResearch/hermes-agent/issues/45258) / [`#45963`](https://github.com/NousResearch/hermes-agent/issues/45963) – Gateway logging and profile-creation zombie processes on Docker were patched.
- [`#45865`](https://github.com/NousResearch/hermes-agent/issues/45865) – Users can now remove/disconnect provider accounts in the UI.
- [`#38963`](https://github.com/NousResearch/hermes-agent/issues/38963) – Windows Desktop installer “no git” error was addressed.
- [`#36515`](https://github.com/NousResearch/hermes-agent/issues/36515) – Test coverage for the Parallel web provider was raised above the 70% threshold.
- [`#46419`](https://github.com/NousResearch/hermes-agent/issues/46419) – Hardcoded English error banners in the chat WebSocket handler were wired into the i18n system.

### 4. Community Hot Topics
- **Response Truncation Resolution ([#7237](https://github.com/NousResearch/hermes-agent/issues/7237)):** The most commented issue in the repository (46 comments) centered on the `Response truncated due to output length limit` error breaking long-form generation across CLI, Telegram, Discord, and Slack. Its closure marks a major milestone, though the resolution path (fix, config change, or documentation) will be closely watched by users.
- **Parallel.ai Routing Controversy ([#45058](https://github.com/NousResearch/hermes-agent/issues/45058)):** This issue exploded with 15 👍 in just three days after a commit silently defaulted `web_search`/`web_extract` traffic to Parallel.ai without user opt-in. It exposed a significant trust deficit around default configuration changes and was resolved today.
- **Claude Subscription OAuth ([#25267](https://github.com/NousResearch/hermes-agent/issues/25267)):** The highest-reacted feature request (21 👍) remains open. The community is clearly demanding the ability to use their existing Claude subscriptions without paying separate API per-token costs.
- **New Security Reports ([#46411](https://github.com/NousResearch/hermes-agent/issues/46411), [#46413](https://github.com/NousResearch/hermes-agent/issues/46413)):** Two security issues filed today—credential exfiltration via `read_file` and Desktop file preview—signal the community is actively hardening the codebase.

### 5. Bugs & Stability

| Severity | Issue | Summary |
|----------|-------|---------|
| **P1** | [#46310](https://github.com/NousResearch/hermes-agent/issues/46310) | Matrix E2EE reconnects per message, exhausting one-time keys and silently dropping burst media sends. |
| **P1** | [#32091](https://github.com/NousResearch/hermes-agent/issues/32091) | Cron jobs created from a non-default profile are written to a `.json` file the gateway never reads—silent orphans. Open since May 25. |
| **P2** | [#46411](https://github.com/NousResearch/hermes-agent/issues/46411), [#46413](https://github.com/NousResearch/hermes-agent/issues/46413) | `read_file` and Desktop file preview don’t block credential stores from sibling profiles. |
| **P2** | [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) | Concurrent Desktop sessions share memory injection and git worktrees, causing cross-contamination. |
| **P2** | [#44560](https://github.com/NousResearch/hermes-agent/issues/44560) | `model.options` handler blocks the WebSocket event loop on slow custom provider HTTP calls. |
| **P2** | [#46090](https://github.com/NousResearch/hermes-agent/issues/46090) | Agent “extremely slow for basic tasks.” Stuck on `needs-repro`. |
| **P2** | [#46332](https://github.com/NousResearch/hermes-agent/issues/46332) | Windows Cron with `.sh` scripts fails due to WSL vs Git Bash conflict and MSYS path mangling. |
| **P2** | [#46265](https://github.com/NousResearch/hermes-agent/issues/46265) | SimpleX adapter silently drops all outbound DM replies. |
| **P3** | [#40480](https://github.com/NousResearch/hermes-agent/issues/40480) | Custom provider models configured via CLI don’t appear in the Desktop app model picker. |

**Active Fix PRs to Watch:**
- [`#26051`](https://github.com/NousResearch/hermes-agent/pull/26051): Preserves full conversation history when context compression fails (P2, waiting review since May 15).
- [`#46427`](https://github.com/NousResearch/hermes-agent/pull/46427): Prevents `GH_TOKEN` from leaking GitHub Copilot into the model picker (P2).
- [`#46289`](https://github.com/NousResearch/hermes-agent/pull/46289): Clears stale s6-log lock files before startup.

### 6. Feature Requests & Roadmap Signals
- **Canonical Provider OAuth** – [`#25267`](https://github.com/NousResearch/hermes-agent/issues/25267) (21 👍) is the clearest roadmap signal: users want to bring their own subscriptions without API proxy billing.
- **Memory Architecture Maturation** – Requests for treating memory as background context ([#31584](https://github.com/NousResearch/hermes-agent/issues/31584)) and a native GBrain plugin ([#46253](https://github.com/NousResearch/hermes-agent/issues/46253)) point to a pending rework of Hermes’ long-term memory pipeline.
- **Kanban / Orchestration** – New PRs add epoch callbacks ([#46360](https://github.com/NousResearch/hermes-agent/pull/46360)) and inherited notification subscriptions ([#46443](https://github.com/NousResearch/hermes-agent/pull/46443)), confirming a strong investment in autonomous multi-agent workflows.
- **UI/UX Polish** – A unified appearance system ([#44107](https://github.com/NousResearch/hermes-agent/pull/44107)), a configurable TUI status bar ([#13490](https://github.com/NousResearch/hermes-agent/issues/13490)), and a “Keep” option for model URLs ([#46192](https://github.com/NousResearch/hermes-agent/issues/46192)) suggest a user-experience-focused minor release is being prepared.

### 7. User Feedback Summary
- **Pain Points & Dissatisfaction:**
  - **Transparency:** The silent routing to Parallel.ai ([#45058](https://github.com/NousResearch/hermes-agent/issues/45058)) generated significant backlash, damaging trust in default configuration policies.
  - **Production Reliability:** The response truncation bug ([#7237](https://github.com/NousResearch/hermes-agent/issues/7237)) and systemic agent slowness ([#46090](https://github.com/NousResearch/hermes-agent/issues/46090)) are eroding confidence for long-running or complex tasks.
  - **Platform Fragmentation:** Windows Cron scripts ([#46332](https://github.com/NousResearch/hermes-agent/issues/46332)), missing Intel Mac builds ([#42199](https://github.com/NousResearch/hermes-agent/issues/42199)), and broken SimpleX DMs ([#46265](https://github.com/NousResearch/hermes-agent/issues/46265)) leave key demographics underserved.
- **Satisfaction & Engagement:**
  - The surge to **50 open PRs** indicates a highly motivated developer ecosystem investing deeply in the platform.
  - Feature requests are becoming sophisticated (GBrain, Kanban callbacks, TUI theming), showing deep product integration and advanced use cases.

### 8. Backlog Watch
Items that are aging or under-resourced despite their importance:

| Issue | Created | Status |
|-------|---------|--------|
| [#12020](https://github.com/NousResearch/hermes-agent/issues/12020) – Toggle for `hermes.tool.progress` events | Apr 18 | Unresolved; blocks OpenAI SDK frontend compatibility |
| [#13490](https://github.com/NousResearch/hermes-agent/issues/13490) – Configurable TUI status bar | Apr 21 | Stalled with minimal maintainer interaction |
| [#26051](https://github.com/NousResearch/hermes-agent/pull/26051) – Preserve context on compression failures | May 15 | P2 PR waiting for review for **1 month** |
| [#31584](https://github.com/NousResearch/hermes-agent/issues/31584) – Background memory context | May 24 | Stalled architectural discussion |
| [#32091](https://github.com/NousResearch/hermes-agent/issues/32091) – Silent cron orphan (**P1**) | May 25 | Critical reliability bug unresolved for 3 weeks |
| [#42199](https://github.com/NousResearch/hermes-agent/issues/42199) – Intel macOS Desktop build | Jun 8 | Growing demand; no work started yet |
| [#46090](https://github.com/NousResearch/hermes-agent/issues/46090) – Agent slowness | Jun 14 | Stuck on `needs-repro`; could escalate to P1 |

---

*Data sourced from GitHub (NousResearch/hermes-agent). Activity window: last 24 hours prior to 2026-06-15T23:59:59Z.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-06-15

## 1. Today’s Overview

PicoClaw experienced a surge in maintenance-focused activity today. Out of **9 Pull Requests** touched in the last 24 hours, **5** were merged or closed, signaling a deliberate clean-up and stability push. A new nightly build (`v0.2.9-nightly.20260615`) was released, tracking the `main` branch. While no major features were merged, a critical `agent` loop stability fix (#2904) was finally closed, and a developer-led error-handling sweep touched the TTS, filesystem, and evolution modules. The most urgent concern is a newly filed regression in the `web_search` tool (#3125) tied to the `.security.yml` migration, which is currently blocking Brave search users without a pending fix.

## 2. Releases

- **Nightly Build `v0.2.9-nightly.20260615.13a38bd1`**  
  This automated nightly build is generated from the `main` branch and is explicitly marked as potentially unstable. No migration notes are provided.  
  **Full Changelog**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. Project Progress (Merged/Closed Highlights)

The majority of today’s merges are focused on **error handling and concurrency stability**:

- **#2904** – *Fix agent loop reload and panic cleanup stability* (by @SiYue-ZO)  
  A significant PR that rewrites the `pkg/agent` reload path to use synchronous `defer/recover` instead of detached goroutines, eliminating a class of lingering goroutine and panic‑recovery bugs.  
  [sipeed/picoclaw PR #2904](https://github.com/sipeed/picoclaw/pull/2904)

- **Error handling improvements** (by @chengzhichao-xydt)  
  - **#3124** – TTS API now checks `io.ReadAll` errors on non‑200 responses.  
  - **#3123** – Filesystem `Close()` on directory FDs is explicitly captured.  
  - **#3122** – Evolution `appendJSONLRecords` now captures deferred `Close()` errors (disk full, NFS failures).  
  - **#3121** – OpenAI‑compat provider replaces the last `log.Printf` with structured logging, removing the `log` import entirely.  

## 4. Community Hot Topics

Activity is process‑oriented, but three items signal developing community interest:

- **#3118** – *Add remote Pico WebSocket mode to picoclaw agent* (by @jp39)  
  The most architecturally significant open feature PR. It introduces a `--remote ws://...` flag, letting the agent connect to a remote socket rather than running locally. This points toward the wider adoption of client/server splits for Pico agents.  
  [sipeed/picoclaw PR #3118](https://github.com/sipeed/picoclaw/pull/3118)

- **#3120** – *RegisterChannelSettings hook for out‑of‑tree channels* (by @carlosprados)  
  Addresses a bottleneck: while `RegisterFactory` is public, the config side is not. This PR would unlock community‑written channels without forking PicoClaw. Engaged with but not yet merged.  
  [sipeed/picoclaw PR #3120](https://github.com/sipeed/picoclaw/pull/3120)

- **#2978** (Closed, Stale) – *Add OmniRoute as provider*  
  The user asked for a “combo” provider or configuration guidance. Closed as stale, suggesting the maintainers either prefer the existing factory system or want the feature to be driven by a plugin path.  
  [sipeed/picoclaw Issue #2978](https://github.com/sipeed/picoclaw/issues/2978)

## 5. Bugs & Stability

**High Severity**  
- **#3125** – `web_search` tool fails silently with Brave API key under `.security.yml`.  
  The LLM correctly formats the call, but `No results` is returned immediately. This is a direct regression from the recent security‑architecture refactor. **No fix PR exists.**  
  [sipeed/picoclaw Issue #3125](https://github.com/sipeed/picoclaw/issues/3125)

**Medium Severity**  
- **#3044** – `allow_from` fails for Matrix IDs containing a colon.  
  Standard `@user:domain` syntax is silently rejected. Unaddressed since June 7.  
  [sipeed/picoclaw Issue #3044](https://github.com/sipeed/picoclaw/issues/3044)
- **#3041** – `mcp add` mis‑parses global flags (e.g. `--no-color`) into positional arguments, breaking HTTP/SSE MCP server registration. Unaddressed since June 7.  
  [sipeed/picoclaw Issue #3041](https://github.com/sipeed/picoclaw/issues/3041)

**Low Severity**  
- **#3090** – PicoClaw Panel does not render on Safari iOS < 16.4. Likely a frontend compatibility gap.  
  [sipeed/picoclaw Issue #3090](https://github.com/sipeed/picoclaw/issues/3090)

## 6. Feature Requests & Roadmap Signals

Three open PRs form a likely outline for the next minor release:

1. **Remote Agent Mode** (#3118) – Client/server architecture for the agent.  
2. **Out‑of‑tree Channels** (#3120) – Hooks for third‑party channel plugins.  
3. **Telegram Reply‑as‑Mention** (#2975) – Treating a reply to a bot message as a `@mention` in group chats.  
   [sipeed/picoclaw PR #2975](https://github.com/sipeed/picoclaw/issues/2975)

Additionally, the *OmniRoute* request (#2978) points to a latent need for **composite/multi‑provider routing** within PicoClaw, which could return as a roadmap item once the plugin interface stabilizes.

## 7. User Feedback Summary

- **Pain Points**:
  - The `.security.yml` migration broke an established workflow for Brave search users (#3125). The silent failure mode is particularly frustrating.
  - Matrix authentication (`allow_from`) is broken for the single most common user ID format (#3044).
  - CLI onboarding friction: `mcp add` flag parsing catches new users off‑guard (#3041).
- **Use Cases in Demand**:
  - Multi‑protocol chat interoperability (Matrix, Telegram).
  - MCP server integration over HTTP/SSE.
  - Combo providers to abstract multiple tool backends.
- **Satisfaction**: The wave of low‑level stability patches today shows active maintenance, but the lack of prompt triage on #3044 and #3041 may leave advanced early adopters waiting for essential fixes.

## 8. Backlog Watch

The following items have gone **7+ days** without a maintainer update and merit attention:

- **#3044** (Matrix `allow_from`, opened Jun 7) – A scoped, reproducible auth regression. If Matrix is a supported channel, this needs a decision or a patch.  
  [sipeed/picoclaw Issue #3044](https://github.com/sipeed/picoclaw/issues/3044)

- **#3041** (`mcp add` flag parsing, opened Jun 7) – A detailed bug report from a power user. Leaving this stale risks MCP setup frustration in the community.  
  [sipeed/picoclaw Issue #3041](https://github.com/sipeed/picoclaw/issues/3041)

- **#2975** (Telegram reply‑as‑mention PR, opened May 30) – A functionally complete feature PR. Without feedback or merge, the contributor may lose momentum.  
  [sipeed/picoclaw PR #2975](https://github.com/sipeed/picoclaw/pull/2975)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest — 2026-06-15**

---

### 1. Today's Overview

NanoClaw experienced a surge of activity on June 15th, with **7 Issues** and **10 Pull Requests** updated within the last 24 hours. The project is currently balancing aggressive architectural advancement with a major security review: three critical vulnerabilities were responsibly disclosed while the core operator-driven provider framework and Codex v2 integration were merged to trunk. A high-impact user experience fix addressing silently dropped LLM turns has been submitted, and the community continues to contribute standardized skill extensions. Overall project health is dynamic but faces important testing and hardening demands.

---

### 2. Releases

No new releases were published today. The project has no tagged release in the observed data window.

---

### 3. Project Progress

**Five pull requests were merged or closed today:**

- **feat(providers): operator-driven provider selection, switching, and memory migration** ([PR #2756](https://github.com/nanocoai/nanoclaw/pull/2756)) — Merged. Establishes the core framework for users to explicitly choose an agent provider, including a registry, setup picker, vault auth walkthrough, and memory-migration skill. Non-default provider payloads (starting with Codex) now install from the new seams.
- **feat(codex): Codex agent-provider payload v2** ([PR #2757](https://github.com/nanocoai/nanoclaw/pull/2757)) — Merged. Replaces the old Codex payload with a full agent provider running on host capability seams and authenticated exclusively through the OneCLI vault.
- **feat(container): data-drive global CLI installs from cli-tools.json** ([PR #2758](https://github.com/nanocoai/nanoclaw/pull/2758)) — Merged. Global Node CLIs (`claude-code`, `agent-browser`, `vercel`) are now installed from a data manifest rather than hardcoded Dockerfile blocks, simplifying tool management.
- **docs(CLAUDE.md): fix two relocated Key Files paths** ([PR #2764](https://github.com/nanocoai/nanoclaw/pull/2764)) — Closed. Fixes two source file paths in the Key Files table to point to their current location under `src/modules/`.
- **docs(add-codex): flag interactive auth step + add host-restart step** ([PR #2769](https://github.com/nanocoai/nanoclaw/pull/2769)) — Closed. Documents that `provider-auth codex` requires an interactive TTY and adds a required host-restart step for a reliable setup flow.

---

### 4. Community Hot Topics

Although comment and reaction counts are zero in the provided data, the content of several items signals significant community focus:

- **Security Research Advisory (YLChen-007):** Three linked security vulnerability reports are the most consequential community contribution today. They address:
    - Arbitrary local file exfiltration via `send_file` ([Issue #2760](https://github.com/nanocoai/nanoclaw/issues/2760))
    - Local gateway approval bypass via unauthenticated loopback webhook ([Issue #2761](https://github.com/nanocoai/nanoclaw/issues/2761))
    - Hidden `args`/`env` persistence in the `add_mcp_server` approval flow ([Issue #2762](https://github.com/nanocoai/nanoclaw/issues/2762))
- **Budget Handling Defect:** The issue reporting that budget-exhausted LLM turns are completely silenced ([Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)) has attracted attention as a significant UX and reliability gap.
- **Integration Friction:** Users are actively optimizing integrations, as shown by the prompt caching enablement request for the Claude provider ([Issue #2768](https://github.com/nanocoai/nanoclaw/issues/2768)) and the Telegram legacy Markdown workaround becoming obsolete ([Issue #2767](https://github.com/nanocoai/nanoclaw/issues/2767)).
- **Standardized Skill Contributions:** Two open PRs follow the published contributing guide precisely to add `.format-lint-off` skills ([PR #2765](https://github.com/nanocoai/nanoclaw/pull/2765), [PR #2766](https://github.com/nanocoai/nanoclaw/pull/2766)), indicating growing third-party engagement with the skill system.

---

### 5. Bugs & Stability

**High Severity**
- **Arbitrary File Exfiltration:** The `send_file` MCP tool accepts absolute paths without constraining the read target, allowing an attacker-controlled agent to leak any local file. ([Issue #2760](https://github.com/nanocoai/nanoclaw/issues/2760), *no fix PR yet*)
- **Approval Flow Bypass:** The self-modification flow for `add_mcp_server` allows `args` and `env` to be persisted without being displayed to the approver, enabling silent persistence of hostile tool configurations. ([Issue #2762](https://github.com/nanocoai/nanoclaw/issues/2762), *no fix PR yet*)
- **Unauthenticated Loopback Webhook:** The local gateway webhook trusts the sender without authentication, enabling a local attacker to forge approval events. ([Issue #2761](https://github.com/nanocoai/nanoclaw/issues/2761), *no fix PR yet*)

**Medium Severity**
- **Silent Turn Drops:** Budget/token-exhausted LLM turns produce an API error that the agent-runner discards without notifying the user. ([Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)) — **Fix submitted** in [PR #2759](https://github.com/nanocoai/nanoclaw/pull/2759).

**Low Severity**
- **Telegram Legacy Markdown:** The manual sanitizer in `src/channels/telegram-markdown-sanitize.ts` is obsoleted by an upstream adapter fix published June 2. ([Issue #2767](https://github.com/nanocoai/nanoclaw/issues/2767))
- **CLAUDE.md Broken Paths:** Two source file entries in the Key Files table pointed at nonexistent paths. (Closed via [PR #2764](https://github.com/nanocoai/nanoclaw/pull/2764))

---

### 6. Feature Requests & Roadmap Signals

The merged PRs strongly indicate the **next minor release** will focus on:

- **Multi-Provider Extensibility:** The merged operator-driven provider selection ([PR #2756](https://github.com/nanocoai/nanoclaw/pull/2756)) and Codex v2 payload ([PR #2757](https://github.com/nanocoai/nanoclaw/pull/2757)) signal that NanoClaw is transitioning to a plugin-like provider architecture with vault-based auth.
- **Container Declarative Management:** The shift to `cli-tools.json` for managing CLI dependencies ([PR #2758](https://github.com/nanocoai/nanoclaw/pull/2758)) suggests a move toward data-driven, skill-contributable container configuration.
- **Codex File Delivery:** The open fix for delivering harness file events from Codex ([PR #2770](https://github.com/nanocoai/nanoclaw/pull/2770)) and the feature channel skills suggest the Codex integration is being actively polished for release.
- **Community Skill Ecosystem:** The influx of PRs using the `contributing-guide` format ([PR #2765](https://github.com/nanocoai/nanoclaw/pull/2765), [PR #2766](https://github.com/nanocoai/nanoclaw/pull/2766)) implies a growing community contributing standardized channel and provider skills.

---

### 7. User Feedback Summary

- **Pain Points:**
    - **Silent Failures:** Users report a strong negative experience when budget limits are hit and the system provides no feedback whatsoever ([Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)).
    - **Security Anxiety:** The three reported security vulnerabilities highlight user concern (likely from power users and security researchers) about the risks of granting agents file system and MCP tool access ([Issues #2760–#2762](https://github.com/nanocoai/nanoclaw/issues/2760)).
    - **Integration Setup Complexity:** Documentation gaps around interactive auth for Codex and host restarts have caused setup failures for agents running in non-TTY environments ([PR #2769](https://github.com/nanocoai/nanoclaw/pull/2769)).
    - **Integration Drift:** The Telegram Markdown workaround being obsoleted demonstrates the challenge of maintaining adapter-level workarounds when upstream packages change ([Issue #2767](https://github.com/nanocoai/nanoclaw/issues/2767)).
- **Satisfaction Signals:**
    - Documentation is actively updated in response to community findings ([PR #2764](https://github.com/nanocoai/nanoclaw/pull/2764)).
    - The provider architecture changes signal a move toward more user agency over which AI backend powers the agent.

---

### 8. Backlog Watch

- **PR #2732: Harden host + agent-runner from health audit findings** ([PR #2732](https://github.com/nanocoai/nanoclaw/pull/2732)) — Open since June 11, this 19-file fix spans fixes from a multi-agent adversarial health audit. It has **zero comments from maintainers**. Given the three critical vulnerabilities disclosed today, this PR should be prioritized for review as it likely addresses related attack-surface hardening.
- There are currently **no stale issues** older than three days in the dataset, suggesting active triage by the maintainers.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 15, 2026, based on the provided data.

---

## NullClaw Project Digest – 2026-06-15

### 1. Today's Overview
Project activity remained minimal over the last 24 hours, with a single new feature request opened and no pull requests, merges, or releases closed. This quiet period may reflect a weekend cycle, a planning phase, or ongoing internal development efforts. The sole community interaction focused on enhancing security compliance for Azure deployments. Overall, the project appears stable but in a low-activity state, with maintainer attention unaccounted for in this window.

### 2. Releases
No new releases were published on June 15, 2026.

### 3. Project Progress
No pull requests were merged or closed within the reporting period. The main branch did not receive any new commits via PRs.

### 4. Community Hot Topics
The entire community discussion today centers on a single new enhancement request. Despite having zero comments or reactions yet, it represents the only active dialog.

- **[#955] Identity based authentication support for Azure OpenAI LLM Provider**
    - *Author:* kunalk16
    - *Link:* [nullclaw/nullclaw Issue #955](https://github.com/nullclaw/nullclaw/issues/955)
    - *Analysis:* The underlying need is direct support for Azure’s `DefaultTokenCredential` chain (Azure CLI, Managed Identity, Visual Studio). This request is driven by enterprise security policies that prohibit raw API key usage, requiring NullClaw to authenticate seamlessly within Azure RBAC and Conditional Access environments.

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The sole open issue is an enhancement request, suggesting no stability regressions surfaced in the last 24 hours.

### 6. Feature Requests & Roadmap Signals
The primary roadmap signal is the push toward first-class Azure Enterprise integration:

- **Issue #955** clearly requests the addition of Azure Identity-based authentication for the OpenAI LLM provider.
- **Prediction:** Given the strong security compliance driver and the broad applicability to any Azure-hosted deployment, this feature is a strong candidate for the next minor release of the relevant provider. Implementing `DefaultAzureCredential` would unblock NullClaw for users in locked-down Azure subscriptions without changing the API surface.

No other roadmap signals emerged from today’s data.

### 7. User Feedback Summary
User feedback today is singular but highly specific. The contributor `kunalk16` represents an enterprise user segment encountering friction with standard API key authentication in Azure. The core pain point is the inability to use NullClaw in environments where security policies mandate Managed Identities or Azure CLI tokens. This signals growing adoption of NullClaw inside regulated enterprise cloud tenants where identity-based access is non-negotiable.

### 8. Backlog Watch
No long-unanswered issues or PRs were updated in the last 24 hours. The only issue opened today is brand new. Without broader visibility into the total backlog, no unresolved items requiring maintainer attention were surfaced from this dataset.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-15

## 1. Today's Overview

IronClaw is in a period of intense, high-velocity development centered on the **Reborn** architecture (WebUI v2, new agent loop, extension system). 42 issues and 45 PRs were updated in the last 24 hours, with 7 issues closed and 15 PRs merged or closed. No new release was officially cut today—though a draft release PR ([#3708](nearai/ironclaw PR #3708)) continues to be actively updated, signaling that **v0.29.1 is imminent** and will bundle a wave of Reborn stabilizations and breaking API changes.

The project is simultaneously executing on three heavy tracks: **hardening the `shell` tool against approval bypasses** (4 coordinated security advisories filed today), **launching a formal "dogfooding" initiative** to prove IronClaw can build IronClaw ([#4878](nearai/ironclaw Issue #4878)), and **polishing the Reborn extension lifecycle** (install → configure → auth UX) following consistent user friction reports.

---

## 2. Releases

**No new releases today.**

One draft release PR ([#3708](nearai/ironclaw PR #3708)) remains open, proposing `ironclaw` v0.29.1 with breaking API changes in `ironclaw_common` and `ironclaw_skills`. It has been accumulating commits since mid-May and is actively updated, suggesting the team is waiting for the current Reborn stability and security hardening wave to clear before publishing.

---

## 3. Project Progress

The project closed 15 PRs and 7 issues today. Major milestones:

| Item | Type | Description |
|------|------|-------------|
| [#4738](nearai/ironclaw PR #4738) (Closed) | Feature | WebChat v2 attachment upload UX—closes the frontend gap in the universal attachments roadmap. |
| [#4836](nearai/ironclaw PR #4836) (Closed) | Feature | Runtime-context slice surfacing connected channels, delivery state, and run origin to the model. |
| [#4873](nearai/ironclaw PR #4873) (Closed) | Test | Re-homed the Slack approval→auth→final-reply delivery e2e test that was born-broken in an earlier change. |
| [#4851](nearai/ironclaw Issue #4851) (Closed) | Fix | Removed the trusted-trigger origin laundering through adapter strings—carries trust as a type now. |
| [#4848](nearai/ironclaw Issue #4848) (Closed) | Fix | Auth-resume now matches by per-invocation `input_ref` instead of only `capability_id`, closing a class of slot-reuse bugs. |

**Ongoing features advancing through the active PR pipeline:**

- **Image attachments for vision models** ([#4871](nearai/ironclaw PR #4871)): The LLM layer already supported image content; this wires it through the Reborn stack.
- **Safety/Orchestration fixes:** [#4889](nearai/ironclaw PR #4889) closes tool activities after cancelled runs; [#4888](nearai/ironclaw PR #4888) filters PRs out of GitHub issue queries.
- **Observability seams** ([#4588](nearai/ironclaw PR #4588)): Trajectory observer hooks for external benchmarking (nearai-bench).
- **Approval gate reordering** ([#4840](nearai/ironclaw PR #4840)): Missing-credential gates now surface *before* the profile approval gate, preventing burn approvals.
- **Slack as extension** ([#4778](nearai/ironclaw PR #4778)): Major refactor to represent Slack as a product-adapter extension rather than a hardcoded channel.

---

## 4. Community Hot Topics

### 🔥 Shell Security Advisory Cluster
**Issues:** [#4862](nearai/ironclaw Issue #4862), [#4863](nearai/ironclaw Issue #4863), [#4864](nearai/ironclaw Issue #4864), [#4865](nearai/ironclaw Issue #4865)

Submitted by `YLChen-007`, this is a coordinated deep audit of the built-in `shell` tool's approval boundaries. Findings include:

- **Transparent wrapper bypass** (`env /bin/sh -c` hides the real command from the classifier).
- **Auto-approval inheritance** from lower-risk commands to destructive payloads.
- **GNU `sort --compress-program`** used as a subprocess execution vector.
- The issues are comprehensively documented with reproduction steps, indicating a mature responsible-disclosure flow.

**Underlying need:** Enterprise-grade command execution with reliable per-invocation approval floors. The model cannot be trusted to self-classify command risk.

### 🚀 Engineering Productivity (Dogfooding)
**Issue:** [#4878](nearai/ironclaw Issue #4878) (parent), subtasks [#4883](nearai/ironclaw Issue #4883), [#4882](nearai/ironclaw Issue #4882), [#4881](nearai/ironclaw Issue #4881), [#4880](nearai/ironclaw Issue #4880)

`think-in-universe` launched an ambitious initiative to make IronClaw an "AI-native engineering team that dogfoods its own technology." Sub-issues propose:

- Cloud coding agent workflows from GitHub.
- Preview deployments for PRs.
- Automated AI code review.
- Baseline coverage metrics that cannot regress.

**Underlying need:** Prove the platform's own utility for complex software engineering tasks and accelerate the project's development velocity simultaneously.

### ⚙️ Reborn Extension UX Fragmentation
**Issues:** [#4890](nearai/ironclaw Issue #4890), [#4886](nearai/ironclaw Issue #4886), [#4884](nearai/ironclaw Issue #4884), [#4885](nearai/ironclaw Issue #4885)

`sunglow666` filed multiple UX findings around the Google Calendar and GitHub extensions. The core pain point is that the install → configure → auth → use flow has silent gaps where users cannot see what step is required next.

**Underlying need:** An app-store-quality onboarding flow for extensions, with clear state machines and contextual prompts for the next step.

---

## 5. Bugs & Stability

### Critical / Security
| Issue | Description | Fix Status |
|-------|-------------|------------|
| [#4862-4865](nearai/ironclaw Issue #4862) | Shell approval bypasses via wrappers, `sort`, and auto-approval inheritance. | Open; under active review. |
| [#4887](nearai/ironclaw Issue #4887) | MCP provider-backed capability approval fails on `input_ref` scoping. Blocks `nearai.web_search`. | Open; core-authored. |
| [#4874](nearai/ironclaw Issue #4874) | WebChat v2 "Illegal invocation" when accessed over plain HTTP from non-localhost. Breaks chat send. | Open; reported by `cuongdcdev`. |

### High
| Issue | Description | Fix Status |
|-------|-------------|------------|
| [#4870](nearai/ironclaw Issue #4870) | WebSocket helper `?token=` auth conflicts with v2 auth contract that rejects it. | Open; design tension noted. |
| [#4890](nearai/ironclaw Issue #4890) | Extension setup flow is fragmented across 4+ surface areas. | Open; directly actionable UX design work. |
| [#4867](nearai/ironclaw Issue #4867) | GitHub repository queries bypass the extension and fall back to `builtin.http`. | Open; routing logic bug. |

### Medium / Low
| Issue | Description | Fix Status |
|-------|-------------|------------|
| [#4852](nearai/ironclaw Issue #4852) | Shell command body invisible in approval dialog / activity history. User cannot see what they are approving. | Open; UX bug. |
| [#4868](nearai/ironclaw Issue #4868) | Inference provider card actions clip offscreen on mobile viewport. | Open; layout fix. |
| [#4838](nearai/ironclaw PR #4838) | Multiple runs on busy threads get parked instead of receiving explicit rejection. | Open; behavior change in review. |

**Overall Stability Assessment:** The Reborn stack is in a churn-heavy stabilization phase. Security finds are being handled transparently. UX regressions in the extension lifecycle are concentrated and understood. The team is closing approximately 1 bug per 6 new issues opened, consistent with an active "break it to fix it" development sprint.

---

## 6. Feature Requests & Roadmap Signals

### Likely for v0.29.x / Next Release

- **Universal Attachments — v1 landing.** The backend ([#4644](nearai/ironclaw Issue #4644) parent), image content support ([#4871](nearai/ironclaw PR #4871)), and WebUX ([#4738](nearai/ironclaw PR #4738)) are largely merged. Remaining scope: format registry and polished web UX subtasks.
- **Slack as Product-Adapter Extension** ([#4778](nearai/ironclaw PR #4778)). If landed, this is a major architectural signal: all channels become extensions. Expect this to be a tentpole for the upcoming release.
- **Observability for Benchmarking.** The trajectory observer and LLM injection seams ([#4588](nearai/ironclaw PR #4588)) are needed by nearai-bench. Moderate merge pressure.

### Emerging Roadmap Themes

- **"IronClaw builds IronClaw."** The dogfooding initiative ([#4878](nearai/ironclaw Issue #4878)) is likely to produce reusable CI workflows, agent coding bots, and coverage enforcement tools that will become project norms.
- **Enterprise Security Hardening.** The coordinated shell audit, trusted-trigger origin fix, and `system_sentinel` refactoring ([#4584](nearai/ironclaw PR #4584)) point toward a security-focused sub-release.
- **Channel Extensibility.** After Slack as product-adapter, expect more channels (Discord, Telegram) to migrate to the extension API.

---

## 7. User Feedback Summary

*Data drawn from the 42 issues active today.*

**Pain Points (High Frequency):**

- **"What do I do next?"** Post-install of an extension, the UI provides `AUTH NEEDED` but no guidance on clicking Configure or completing OAuth ([#4886](nearai/ironclaw Issue #4886), [#4890](nearai/ironclaw Issue #4890)).
- **"What is the agent doing?"** Approval dialogs lack command text for shell tools, activity history does not log the command ([#4852](nearai/ironclaw Issue #4852)).
- **"It works over localhost but not over the network."** WebSocket auth contract rejects `?token=` that the helper sends ([#4870](nearai/ironclaw Issue #4870)). Plain HTTP from a LAN address throws "Illegal invocation" ([#4874](nearai/ironclaw Issue #4874)).
- **"Tool A falls back to Tool B silently."** GitHub queries hitting `builtin.http` instead of the GitHub Extension ([#4867](nearai/ironclaw Issue #4867)).

**Satisfaction Signals:**

- High user **engagement with security auditing**—external researcher `YLChen-007` filed four detailed, reproducible advisories. The project's openness to receiving these signals fosters trust.
- The **dogfooding initiative** originated internally, reflecting strong confidence in IronClaw's capability to manage software engineering workflows.
- Despite the high churn, users are actively testing the Reborn stack on non-trivial integrations (Google Calendar, GitHub, shell commands, file analysis), indicating a **devoted early-adopter base**.

---

## 8. Backlog Watch

### Critical Blocker
- **Release PR v0.29.1** ([#3708](nearai/ironclaw PR #3708)) — Open since May 16. Continuously updated but not merged. Likely blocked by the security issues or the Slack-as-extension refactor. A release this large accumulating unmerged changes increases risk of dependency churn.

### Long-running Items Requiring Attention
- **Universal Attachments parent issue** ([#4644](nearai/ironclaw Issue #4644)) — Created June 9. Very high activity, but the final subtasks (format registry, extraction) lack assigned owners. Risk of losing momentum after the frontend/backend landings.
- **WeChat channel docs** ([#3515](nearai/ironclaw Issue #3515)) — Closed today! A win for backlog hygiene.
- **Barcelona Hackathon branch** ([#4787](nearai/ironclaw PR #4787)) — Explicitly a `NO MERGE` branch. Exists to provide a stable path for hackathon participants. If this branch must constantly pull upstream changes, stability is not yet sufficient for the hackathon target date.
- **Dependabot avalanche.** Three PRs in the top 20 are bulk dependency bumps ([#4876](nearai/ironclaw PR #4876), [#4002](nearai/ironclaw PR #4002), [#4499](nearai/ironclaw PR #4499)). These will need dedicated CI cycles to validate before merge.

### Silent Needs
- **Trigger origin trust model.** Issue [#4851](nearai/ironclaw Issue #4851) was closed, but the underlying pattern (string-based trust laundering) may have echoes in other parts of the pipeline. Watch for follow-ups.
- **Mobile / non-localhost usability.** Issues [#4868](nearai/ironclaw Issue #4868) (mobile clipping) and [#4874](nearai/ironclaw Issue #4874) (HTTP invocation) have low comment counts but affect a growing segment of "causal daily driver" users. If mobile adoption is a goal, these should be prioritized.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured project digest for **LobsterAI (netease-youdao/LobsterAI)** based on the data snapshot from **2026-06-15**.

---

# LobsterAI Project Digest — 2026-06-15

## 1. Today's Overview
Project activity is centered around **consolidation and UX hardening** today. While no new releases were cut, the team merged a major feature adding document Artifact support (e.g., DOCX, PDF, XLSX). Three long-standing feature PRs targeting the **Cowork session experience** were updated recently, signaling they are likely being prepared for merge in the next release cycle. Two open UI/UX issues related to **i18n consistency** and **form layout** remain in the backlog but saw no new development commits from the maintainers. Overall, the project shows healthy feature velocity, with a clear focus on making the agent session environment more reliable and feature-rich.

## 2. Releases
**No new releases were published today.** No release notes, breaking changes, or migration guides are applicable for this digest period.

## 3. Project Progress
Two PRs were closed/merged today, advancing both the feature surface and stability:

- **PR #2159 (CLOSED/MERGED)** — *feat(artifacts): 支持文档 Artifact 分享与预览优化*
  A significant expansion of the Artifacts system. This adds support for sharing and previewing common document formats (DOCX, PPTX, XLSX, PDF, CSV, TSV) directly within the agent UI. Includes file packaging, type validation, DOCX pagination, native PDF fallback, and CSP adjustments to allow blob resources. This lays the groundwork for a more collaborative document workflow inside the agent.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/2159)

- **PR #1465 (CLOSED/MERGED)** — *fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现*
  A critical data consistency fix. When a user deleted a scheduled task, only the gateway record was removed, leaving behind a local SQLite `cowork_sessions` record. Upon restart, this orphaned record reappeared as a ghost session. The fix now properly cascades the deletion to the local database.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1465)

## 4. Community Hot Topics
While no items have an overwhelming number of comments today, the most significant cluster of activity revolves around the **three long-standing Cowork feature PRs** that were recently updated:

- **PR #1429 (In-Session Search):** Implements real-time text highlighting (`mark.js`) and `Cmd/Ctrl+F` search within Cowork sessions.
- **PR #1430 (Sleep Prevention):** Integrates Electron `powerSaveBlocker` to prevent the system from sleeping during long-running agent tasks.
- **PR #1431 (Session Timer):** Adds a real-time `elapsed` timer to the `StreamingActivityBar`.

All three share an **underlying need**: users are pushing LobsterAI toward parity with professional development agent tools (e.g., Claude Code, Copilot Workspace). They need **session reliability** (no sleep interruptions), **discoverability** (search within long logs), and **transparency** (visibility into how long a session has been running).

- **Issue #1434** (Chinese UI shows English prompt) receives implicit community validation that i18n consistency matters for non-English user bases.  
  [View Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)

## 5. Bugs & Stability
- **High Severity — Fixed:** *Ghost Session Resurrection (PR #1465)*. A data integrity violation where deleted scheduled tasks would reappear after app restart. The fix addresses the root database cleanup gap. **Status: Resolved.**
- **Medium Severity — Open:** *i18n Fallback Failure (#1434)*. When the application language is set to Chinese, the Agent skill tab “no data” state renders English text and includes an English button. This degrades the UX for the primary target language. **Status: No fix PR identified.**
- **Low Severity — Open:** *Agent Creation Overflow (#1435)*. Excessively long agent names overflow the modal dialog without truncation or wrapping, causing layout breakage. **Status: No fix PR identified.**

No new regressions or crashes were introduced in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
**Likely shipping in the next version:**
- **Rich Document Artifacts** — PR #2159 is now merged and will allow users to view and share complex office documents. This moves Artifacts beyond simple code/output into a general-purpose document tool.
- **Cowork UX Suite** — PRs #1429 (Search), #1430 (Sleep Block), and #1431 (Timer) are cohesive. Their simultaneous update strongly suggests the team is gating them together for a coordinated Cowork quality-of-life release.

**Roadmap Prediction:**
LobsterAI is transitioning from a simple AI conversation tool to a **persistent, reliable workbench**. The addition of robust session controls (search, timer, anti-sleep) combined with document artifacts signals a roadmap focused on **enterprise-adjacent productivity and long-running autonomous agent support**.

## 7. User Feedback Summary
- **Pain Points (Inferred from Issues & PRs):**
  - **Session Instability (#1430):** Users running long autonomous agent loops are losing work to system sleep. This is the top reliability friction for power users.
  - **Information Retrieval (#1429):** Cowork sessions produce lengthy logs with no search capability, forcing users to manually scroll.
  - **Confusing Task Management (#1465):** The ghost session bug undermined trust in the scheduled tasks feature.
  - **Localization Gaps (#1434):** Chinese-language users are encountering untranslated UI elements, diminishing the localized experience.

- **Satisfaction Indicators:**
  - The quality and duration of community contributions (the three Cowork PRs have been in development for months by multiple authors) indicate a **healthy, engaged contributor base**.
  - The quick turnaround on the ghost session fix (#1465) shows that the core team responds promptly to data-corruption-level bugs.

## 8. Backlog Watch
The following items have remained open for over two months without significant maintainer action:

- **Issue #1434 — UI Language Inconsistency**  
  Chinese text is replaced by English in the agent skill search empty state. Low complexity, high visibility. Needs an i18n fallback fix.  
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1434)

- **Issue #1435 — Agent Name Overflow**  
  Modal dialog does not handle long input. A pure CSS/truncation fix.  
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1435)

- **PRs #1429, #1430, #1431 — Cowork Feature Suite**  
  All three are marked “stale” but were revived with recent updates. They require a final review batch from the maintainers. Leaving them in limbo risks merge conflicts and demotivates the external contributors (noransu, choyuenga) who have invested significant effort.  
  [View PR #1429](https://github.com/netease-youdao/LobsterAI/pull/1429) | [PR #1430](https://github.com/netease-youdao/LobsterAI/pull/1430) | [PR #1431](https://github.com/netease-youdao/LobsterAI/pull/1431)

**Recommendation:** The project would benefit from a maintainer triage session focused on merging the three Cowork PRs and tagging the UI issues as `good first issue` for new contributors.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

```markdown
# Moltis Project Digest – June 15, 2026

## 1. Today’s Overview
The 24-hour period ending June 15 saw minimal movement within the Moltis project. No pull requests were advanced, no releases were published, and the sole issue logged remained open. The absence of bug reports or regressions suggests a stable build state, though the stagnation in development commits indicates a potential plateau in active feature integration. The single piece of community input—a feature request—underscores an ongoing interest in optimizing the project for performance at the edge.

## 2. Releases
*No new releases were cut in the last 24 hours. Users remain on the latest stable channel without any migration or breaking changes to report.*

## 3. Project Progress
No pull requests were merged, closed, or updated in the last day. The codebase is static against the last reported update, with no new features, refactors, or bug fixes advancing through the development pipeline.

## 4. Community Hot Topics
Discussion volume on the repository was flat, with zero comments left across all issues and PRs. The only notable item is a fresh feature proposal:
- [#1123 [Feature]: Add pure-Rust turbovec as an alternative memory backend for extreme edge compression](https://github.com/moltis-org/moltis/issues/1123) — authored by `joeblew999`. It has yet to accumulate comments or reactions. The topic itself (pure-Rust, extreme edge compression) aligns with modern edge-AI and IoT performance goals.

## 5. Bugs & Stability
**Severity: None reported.** There were zero bug-related issues filed or updated. The project appears free of freshly surfaced stability concerns, crashes, or regressions.

## 6. Feature Requests & Roadmap Signals
A single feature request provides the only roadmap signal today:
- **Memory Backend Extension:** Issue [#1123](https://github.com/moltis-org/moltis/issues/1123) explicitly asks for a `pure-Rust turbovec` backend. The "extreme edge compression" wording strongly implies a target use case of very low-resource environments (microcontrollers, small form factors). If the maintainers share this vision for expanding Moltis’s deployment surface, this is a candidate for a future minor release. Currently, it lacks community upvotes or discussion, making its near-term priority unclear.

## 7. User Feedback Summary
Direct user feedback is scarce for this period. Submitter `joeblew999` demonstrated initiative by filing a detailed pre-flight checklist and structured feature proposal. Their primary stated need is enhanced memory compression for edge deployments. Without merged PRs from new contributors or resolved user complaints, broader sentiment analysis is impossible, but the technical depth of the request indicates a sophisticated user base pushing the project’s performance boundaries.

## 8. Backlog Watch
The backlog has no new entries requiring immediate maintainer attention beyond the single new issue. [#1123](https://github.com/moltis-org/moltis/issues/1123) is freshly created and should ideally receive a 'triage' label or a preliminary response from the core team to validate the idea or outline implementation constraints before it loses momentum. No older items were disturbed in this quiet period.
```

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

## CoPaw Project Digest — 2026-06-15

### 1. Today’s Overview
On June 15, 2026, the CoPaw project sustained a high level of community and development activity, with **24 issues** and **16 pull requests** updated in the previous 24 hours. The team merged or closed **5 PRs** and resolved **6 issues**, continuing a steady pace of patching regressions introduced in the v1.1.11 series. No new releases were published today, leaving the current `v1.1.11.post2` as the latest build under active scrutiny. Community reports point to significant regressions in the Gemini provider and context compression logic, alongside strong demand for desktop performance optimization and expanded model integration, indicating a period of high community engagement balanced against stability concerns.

### 2. Releases
*No new releases were published on this date. The latest available version remains `v1.1.11.post2`.*

---

### 3. Project Progress
The project advanced through several targeted fixes and infrastructure additions:

- **Desktop UX Fix ([#5051](https://github.com/agentscope-ai/QwenPaw/pull/5051)):** Merged. Persists the backend port across restarts so the Windows client remembers the last selected agent and session (Closes [#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733)).
- **LLM Backend Parsing Fix ([#5035](https://github.com/agentscope-ai/QwenPaw/pull/5035)):** Merged. Replaces a fixed-width string slice for llama.cpp version parsing, preventing parse failures as build numbers grow beyond 4 digits.
- **Context Manager Safety ([#5038](https://github.com/agentscope-ai/QwenPaw/pull/5038)):** Merged. Guards against `IndexError` in `LightContextManager.pre_reply()` when receiving an empty message list.
- **Plugin SDK Enhancement ([#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188)):** Merged. Adds a request payload transform hook to the chat registry, exposing `window.QwenPaw.chat.requestPayload.add(...)` for third-party plugins.
- **Packaging Revert ([#5092](https://github.com/agentscope-ai/QwenPaw/pull/5092)):** Merged. Reverts a previous discord compile-check fix to resolve build conflicts.

---

### 4. Community Hot Topics
The most active discussions reveal critical friction points and unmet needs:

- **Desktop Performance Regression ([#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047)) — 5 comments, Closed.** A major pain point. Users report the Tauri-based desktop client takes 10+ minutes to start (vs. 1–2 minutes for the old Python build) and frequently freezes. *Underlying need:* The desktop migration must not regress on startup time or reliability.
- **Kimi / uv Integration Gap ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)) — 5 comments, Open.** Users who have paid subscriptions to `kimi-for-coding` want to use those models directly through QwenPaw, and request `uv` be added to the tool whitelist. *Underlying need:* Users want to consolidate existing paid subscriptions rather than pay again through QwenPaw's native provider.
- **Agent Autonomy Limitations ([#5174](https://github.com/agentscope-ai/QwenPaw/issues/5174)) — 2 comments, Open.** A detailed report that cron/heartbeat agents cannot execute heavy tasks (e.g., writing files, spawning sub-agents) despite having a "should-do" prompt. *Underlying need:* The community expects robust autonomous, scheduled agent behavior, not just reactive chats.
- **Enterprise Observability Demand ([#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009)) — 3 comments, Closed.** A request for integration with Langfuse / OpenTelemetry. Although closed, it signals growing enterprise/professional adoption requiring production-grade tracing.

---

### 5. Bugs & Stability
A wave of reports on `v1.1.11.post2` highlights several critical and high-severity regressions:

**Critical**
- **Gemini Tool Calling Broken ([#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163)):** Confirmed working in `v1.1.10` but completely broken in `v1.1.11.post2`. Affects all users relying on Gemini for function-calling workflows.
- **Context Compression Destroys History ([#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)):** When a persona/system prompt exceeds the token threshold, compression reduces the context to zero, causing models to lose all identity and task context.

**High**
- **Local Model Providers Invisible ([#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184)):** UI regression. Locally created model providers do not appear in the settings panel after upgrading.
- **Long Conversation Stall ([#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161)):** QwenPaw stops responding entirely in long sessions.
- **Conversation Infinite Loop ([#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162)):** The agent’s thought loop enters a dead cycle under specific conditions.

**Medium**
- **Enterprise WeChat Approval Deadlock ([#5190](https://github.com/agentscope-ai/QwenPaw/issues/5190)):** Access control generates approvals but provides no UI to view or act on them.
- **Plugin Pip Spam ([#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)):** Unstable PyPI access causes repeated visible `cmd.exe` popups during dependency installation on Windows.
- **Wayland / Pet Feature Broken ([#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183)):** The desktop pet widget fails on Wayland compositors.
- **Python 3.13 Plugin Crash ([#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166)):** TeamChat and other plugins crash due to the deprecated `imghdr` module.
- **Packaged Build White Screen ([#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165)):** The `build_win_pyinstaller.ps1` script references nonexistent modules, producing a broken `.exe`.

---

### 6. Feature Requests & Roadmap Signals
The project’s near-term direction is illuminated by several high-value PRs and user requests:

**In Review / Development**
- **Computer Use ([#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)):** A major feature adding Windows GUI automation (UIA + Tauri Control Mode), allowing agents to drive the desktop visually.
- **Plugin Command Suggestions ([#5189](https://github.com/agentscope-ai/QwenPaw/pull/5189)):** Adds slash-command autocomplete for plugins with cross-tab language sync.
- **Vietnamese Language Support (PRs [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175), [#5186](https://github.com/agentscope-ai/QwenPaw/pull/5186)):** Two overlapping PRs adding full Vietnamese locale support.
- **Session Filtering ([#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178)):** Adds title-based filtering to the session list.
- **DataPaw Plugin ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)):** A long-open PR (3 weeks) adding 12 BI data-analysis skills.
- **PRD Management Tool ([#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902)):** Built-in CRUD for product requirements documents with a frontend renderer.

**Top Community Requests**
- Model support: Kimi-for-coding / uv whitelist ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156))
- Channel support: Official Zalo bot ([#5168](https://github.com/agentscope-ai/QwenPaw/issues/5168))
- Context enhancement: Real-time HH:MM:SS injection ([#5185](https://github.com/agentscope-ai/QwenPaw/issues/5185))
- UI enhancement: Code syntax highlighting ([#5191](https://github.com/agentscope-ai/QwenPaw/issues/5191))
- Config enhancement: Unified model type configuration ([#5182](https://github.com/agentscope-ai/QwenPaw/issues/5182))

---

### 7. User Feedback Summary
- **Pain Points:** The Tauri migration remains the single largest source of negative feedback, with startup times exceeding 10 minutes. The `v1.1.11.post2` release is widely perceived as introducing multiple regressions (Gemini, local providers, context compression). The cron/heartbeat limitation is frustrating power users who want to move beyond simple chat workflows.
- **Satisfaction:** The community is highly engaged and pushing the project forward. The rapid closure of 6 issues today shows responsiveness. The addition of new plugin SDK hooks and the computer-use feature signal a strong commitment to an agentic future. Vietnamese contributors are particularly active, indicating growing global adoption.
- **Use Cases:** Users are stretching the project into enterprise integration (WeChat, DingTalk, Feishu), scheduled automation (cron agents), data analysis, and multi-agent collaboration. Stability is the main bottleneck limiting these use cases from becoming reliable daily drivers.

---

### 8. Backlog Watch
Several items require maintainer attention to prevent stalling or user dissatisfaction:

- **[PR #4622] DataPaw Plugin:** Open since **2026-05-22**. A substantial data-analysis plugin (12 skills) with no recent review activity. Risk of significant drift.
- **[PR #4902] PRD Management Tool:** Open since **2026-06-02**. A complete built-in tool for managing product requirements, waiting for merge.
- **[Issue #5177] DingTalk Chat Registration Gap:** DingTalk channel sessions do not appear in `chats.json`, making them invisible to the Console frontend. A core integration bug.
- **[Issue #5166] Python 3.13 `imghdr` Deprecation:** Blocks all plugin installations on Python 3.13. No PR submitted yet.
- **[PR #5051] Desktop Port Persistence:** Although merged, the underlying issue (Tauri startup slowness) remains a top community complaint with no committed performance fix yet.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 15, 2026, based on the provided GitHub data.

---

### 1. Today’s Overview
ZeroClaw is experiencing an exceptionally high-velocity development cycle, with **42 issues** and **50 pull requests** updated in the last 24 hours. Maintainers demonstrated strong throughput by closing 28 issues and processing 4 pull requests. While no formal release was cut today, the volume of merged work points to a project scaling rapidly through heavy community contribution. The current sprint clearly prioritizes expanding connectivity—landing new SMS channels and LLM providers—while also addressing core architectural tension around security profiles and delegation.

### 2. Releases
No new releases were published in this reporting period.

### 3. Project Progress
Four pull requests and 28 issues were closed in the last 24 hours. Key merged PRs include:
- **PR #7664** — Fix for a critical Gateway bug where `ask_user` failed instantly with “Channel closed before receiving a response” (linked to Issue #7542).
- **PR #7384** — Adds a pause/resume toggle for scheduled cron tasks from the dashboard.
- **PR #7594** — Major internal config refactor moving to type-driven alias pickers, eliminating hardcoded path special-casing.
- **PR #7614** — Fix for musl libc detection in the `install.sh` target triple.

A substantial batch of **community-subscribed features** landed via Issue closures, most authored by `theonlyhennygod`. This includes **five new LLM providers** (Arcee AI, Inception/Mercury, Lambda AI, Featherless AI, Upstage Solar) and **several SMS channel integrations** (Telnyx, Plivo, Sinch, Vonage), alongside smart home tools for Sonos, Spotify, 8Sleep, and Philips Hue.

### 4. Community Hot Topics
- **“Full” Docker Image (`#3642`)** — The most upvoted thread (13 comments, 3 👍). The request for an image compiled with all feature flags enabled (e.g., WhatsApp) highlights that the current minimal default is a measurable barrier to entry for non-technical users.
- **Governance RFC (`#6808`)** — The proposed “Work Lanes, Board Automation, and Label Cleanup” (11 comments) reflects internal growing pains. The maintainers are seeking automation to handle the triage load generated by the project’s rapid expansion.
- **Delegate Agent Risk Profiles (`#7470`)** — A Severity S1 active thread (7 comments) unraveling a design conflict: the `risk_profile.allowed_tools` gate is currently too restrictive for practical multi-agent reviewer/research setups.
- **Air-Gapped Execution Mode (`#6293`)** — A detailed RFC for splitting the daemon into online/offline processes over a Unix socket. This indicates strong enterprise and security-conscious user demand surfacing at the architecture level.

### 5. Bugs & Stability
Several high-severity bugs are in the active resolution pipeline:
- **S0 – Data Loss / Security Risk:** Issue `#5528` (Improper email channel config logic) was closed with a fix merged today.
- **S1 – Workflow Blocked:** Issue `#7470` (Delegate agentic mode rejecting empty `allowed_tools`) remains open and is actively discussed. Documentation PR `#7592` and runtime fix PR `#7608` both touch this area.
- **S1 – Workflow Blocked:** Issue `#6847` (WhatsApp channel not showing QR code on onboarding) was closed with a fix.
- **S2 – Degraded Behavior:** Issue `#6856` (`show_tool_calls` missing from channel schema v3) is in progress.
- **Provider Regressions:** PR `#7616` fixes Groq rejecting `reasoning_content` on replay. PR `#5892` (open since April, currently stale) addresses two production blockers (`empty tool_choice` and `orphaned tool_use`) affecting OpenAI, Bedrock, OpenRouter, and others.
- **Infrastructure Bugs:** PR `#7549` fixes a critical mismatch where CLI-installed WASM plugins were invisible to the runtime due to discovery path divergence.

### 6. Feature Requests & Roadmap Signals
The next release (expected under the v0.80-beta1 milestone from RFC `#6808`) appears feature-complete regarding connectivity. The wave of merged SMS channels and provider integrations will debut as official features.

Looking further ahead, the strategic roadmap is being shaped by several high-effort RFCs and PRs:
- **Air-Gapped Execution (`#6293`)** — Likely a multi-release feature, but the RFC signals a significant investment in secure deployment topologies.
- **Dream Mode for Memory (`#6693`)** — A large PR (size XL) introducing periodic local-only memory consolidation with an opt-in LLM reflection phase. This represents a push toward on-device intelligence.
- **Full Docker Image (`#3642`)** — Given its strong community support and the recent organizational focus on lowering barriers, this is a strong candidate for the immediate next patch release.
- **ACP Bridge (`#6823`)** — The client-side TUI-to-daemon connection layer is being actively developed in the background for a richer terminal user interface.

### 7. User Feedback Summary
**Satisfaction drivers:**
- The rapid merge velocity of community submissions (particularly the massive batch from `theonlyhennygod`) demonstrates healthy trust and collaboration between core maintainers and contributors.
- The international user base feels actively included, evidenced by targeted zh-CN locale syncs (PR `#7612`) and efforts to fix the QQ channel (Issue `#5662`).

**Pain points:**
- **Configuration complexity remains the #1 friction.** Users are regularly hitting pitfalls with the TOML schema, demonstrated by Issues `#6856` (missing `show_tool_calls`), `#7617` (extra nested aliases silently dropping fields), and the quickstart alias validation fix in PR `#7609`.
- **Security vs. Usability tradeoff in delegation.** The `risk_profile.allowed_tools` gating mechanism in Issue `#7470` is widely seen as too brittle for practical multi-agent use cases.
- **Plugin ecosystem friction.** The discovery path bug (PR `#7549`) eroded trust in the WASM plugin system, making CLI-installed plugins invisible.

### 8. Backlog Watch
Several critical items require dedicated maintainer bandwidth:
- **Issue `#6074` (Lost Commits Audit)** — Open since April 24. Tracks the recovery of 153 commits lost in a bulk revert (commit `c3ff635`). This represents lost features and fixes that need strategic reconstruction.
- **Issue `#5842` (Codex CLI Security)** — Open since April 17. This track evaluates allowlisting for security-affecting `extra_args` flags. It has been in “accepted” status for two months without a surfaced implementation branch.
- **PR `#5892` (Production Blockers)** — Open since April 19. Addresses two severe bugs (`tool_choice` and `tool_use` corruption across multiple providers) but is currently flagged as a stale candidate. This directly impacts provider stability for the entire ecosystem.
- **Issue `#5662` (QQ Voice Duplication)** — Open since April 12, Priority P1. Users report 20+ duplicate database entries per voice message. Marked in-progress but no fix PR is visible among the recent top items.
- **PR `#6693` (Dream Mode)** — Open since May 16. A large, high-risk architectural memory feature waiting for a review cycle.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*