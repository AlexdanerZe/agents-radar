# OpenClaw Ecosystem Digest 2026-06-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-14 03:41 UTC

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

# OpenClaw Project Digest — 2026-06-14

## 1. Today’s Overview
OpenClaw exhibited exceptionally high activity on June 14, 2026, with exactly 500 Issues and 500 Pull Requests updated in the preceding 24 hours. The project maintained strong throughput, closing 99 issues and merging or closing 211 PRs. Two new beta releases (v2026.6.7 and v2026.6.8) were published, continuing the project’s aggressive release cadence. However, the volume of activity masks significant stability challenges: several P0 and P1 bugs around memory leaks, session state corruption, and security boundaries dominate the tracker, signaling that rapid development is outpacing hardening in some core subsystems.

## 2. Releases
Two new releases were published today:
- **v2026.6.7-beta.1**: Tightens channel delivery across Slack and Telegram, introduces same-channel finals persistence in transcripts, a top-level `image` message-tool, and expandable Telegram blockquotes. Includes improvements to progress drafts and paged action results.
- **v2026.6.8-beta.1**: Focuses on Telegram and WhatsApp robustness. Telegram gains structured rich text (tables, lists, expandable blockquotes) while WhatsApp gets safer rich-media boundaries. Includes retired native draft migration and prompt-preserving CLI backend delivery.

No explicit breaking changes or migration notes were highlighted in the release summaries, but operators of customized channel integrations should verify delivery behavior against the new media-boundary logic.

## 3. Project Progress
The project merged or closed 211 PRs today. Notable advances include:
- **Clownfish automated fixes**: Multiple high-quality bot patches advanced, repairing iOS Safari chat layout (#92855), slug generator error handling (#92854), ACP server MCP protocol version acceptance (#92853), memory-core reindex metadata serialization (#92850), and Tailscale JSON parse resilience (#92849).
- **High-priority resolutions**: Several P1/P2 bugs were closed, including the cron scheduled trigger global state contamination (#90991), embedded-run session state zombie agents (#48573), Feishu monitor memory leak (#48183), and Windows node command reporting (#84644).
- **Infrastructure hardening**: PR #90305 introduces gateway drain preservation during supervised restarts via systemd `KillMode=mixed`. PR #92852 adds inotify exhaustion fallback for config hot-reload, enabling resilience on constrained hosts.
- **Protocol compatibility**: PR #92853 (carried forward from #56176) fixes ACP server acceptance of MCP date-string protocol versions used by VS Code 1.113+ and Cursor.
- **External reranker support**: The large PR #92725 adds a new configuration path for using external rerankers with `memorySearch:query:hybrid`, decoupling from the built-in MMR-only approach.

## 4. Community Hot Topics
The most active discussions center on foundational stability, security, and workflow automation:

| Issue | Topic | Comments | Signals |
|---|---|---|---|
| #44925 [OPEN] | Subagent completion silently lost | 19 comments, 1 👍 | P1 diamond lobster — core orchestration reliability |
| #48788 [OPEN] | Centralized filename encoding utility | 18 comments | Multi-language support demand across channel adapters |
| #45740 [OPEN] | gh-issues skill prompt injection | 13 comments, 1 👍 | Security is top of mind — raw issue bodies injected into prompts |
| #48003 [OPEN] | Steer mode mid-turn injection failure | 12 comments, 2 👍 | Critical for advanced prompt orchestration workflows |
| #45608 [OPEN] | Pre-reset agentic memory flush | 10 comments, **4 👍** | Highest upvoted feature — users want memory persistence across `/new` |
| #91588 [OPEN] | Gateway memory leak (350MB→15.5GB) | 10 comments, 1 👍 | P0 — severe stability issue drawing wide attention |
| #40001 [OPEN] | Write tool lacks append mode | 11 comments, 1 👍 | Silent data loss when isolated cron sessions overwrite shared files |

The #44925 subagent loss thread exposes three distinct failure patterns (completion announce fails, turn timeout, no retry logic), making it the most technically detailed user report in the current backlog. The #45608 feature request for pre-reset memory flush reflects a strong community desire for continuous learning across sessions, a hallmark capability for production AI assistants.

## 5. Bugs & Stability
The project’s stability posture is under significant strain, reflected in multiple high-severity active bugs:

**Critical / P0:**
- **Gateway Memory Leak** (#91588): RSS grows from ~350 MB to 15.5 GB over 2–3 days, triggering OS OOM kills and repeated `launchd-handoff` restart cycles. No linked fix PR yet. This is the single most urgent infrastructure issue in the project.

**P1 Regressions & Core Stability:**
- **Subagent completion silently lost** (#44925): Three failure modes where results vanish without retry, notification, or auto-restart. `No-new-fix-pr`.
- **Multi-agent orchestration unstable** (#43367): Concurrent agents add/config overwrites, session-lock failures, detached child work. `No-new-fix-pr`.
- **Session hangs on compaction timeout** (#43661): Each timeout triggers a duplicate message send to the user with no recovery. `No-new-fix-pr`.
- **Telegram DMs pollute main session** (#41165): Routing regression persists even after previous fix attempts. `Needs-maintainer-review`.
- **Active Memory + Codex latency** (#86996): Long response latencies, hook timeouts, startup aborts, event-loop stalls. `No-new-fix-pr`.

**P1 Security & Data Integrity:**
- **Discord leaks internal tool-call traces** (#44905): Raw `NO_REPLY`, `to=functions.memory_search`, commentary, and JSON arguments surface in channels. `Needs-maintainer-review`.
- **Elevated exec routing broken** (#46786): Enabling `tools.elevated.enabled: true` routes ALL exec calls to the gateway host, bypassing sandbox entirely. `Needs-maintainer-review`.
- **gh-issues prompt injection** (#45740): Untrusted issue bodies injected directly into sub-agent prompts without sanitization. `Needs-maintainer-review`.
- **OpenAI Codex errors leak into user chat** (#44910): Raw model selection errors surface in Telegram. `Needs-live-repro`.

**P1 Platform-Specific:**
- **`openclaw update` EBUSY on Windows** (#40540): Six days since last maintainer activity. Blocks users on Windows from updating.
- **Google Vertex regression** (#38327): "Cannot convert undefined or null to object" on gemini-3.1-pro-preview after updating to 2026.3.2. Wide impact on Google Cloud users.
- **Cron jobs silently time out** (#45494): Full timeout window exhausted on sustained 500 errors instead of fast-failing.

**Recently Resolved (Today):**
- Fixed: Feishu monitor memory leak (#48183), cron state contamination (#90991), embedded-run session leaks (#48573), Windows node command reporting (#84644).

## 6. Feature Requests & Roadmap Signals
Several features in the backlog point toward the project’s maturation into an enterprise-grade platform:

| Request | Issue | Priority | Signal Strength |
|---|---|---|---|
| Pre-reset agentic memory flush | #45608 | P2 | **4 👍** — strongest user demand |
| Per-agent cost budget enforcement | #42475 | P2 | Long discussion, gateway-level enforcement requested |
| Memory Trust Tagging by Source | #7707 | P2 | Security-driven — prevent memory poisoning |
| Centralized filename encoding utility | #48788 | P2 | 18 comments — multi-language necessity |
| Multi-Session Architecture RFC | #48874 | P2 | Architectural RFC for shared LLM + isolated sessions |
| Per-skill model routing | #43260 | P2 | **CLOSED** — likely landing in next release |
| Browser tool 7 improvements | #44431 | P2 | Extensive field report from real-world automation |
| MathJax/LaTeX rendering | #42840 | P2 | 6 👍 — academic/science user base demand |
| YAML config support | #45758 | P3 | 2 👍 — infrastructure ergonomics |
| Path-scoped RWX permissions | #39979 | P2 | Unix DAC-style security model for tool access |

The closure of #43260 (SKILL.md `model` field frontmatter) is a strong signal that per-skill model routing will ship soon, enabling complex agents to route simple lookups to cheap models and complex coding to premium ones. The #44431 browser tool report (CSS selector support, drag-and-drop, CAPTCHA detection, PDF access, scroll stabilization) reads like a product spec for a major automation capability upgrade.

## 7. User Feedback Summary
User sentiment reveals a platform that is powerful and rapidly evolving but prone to silent failures and opaque internal state:

**Major Pain Points:**
- **Silent failures erode trust**: Users repeatedly report subagent completions lost without notification (#44925), write tool overwrites destroying data (#40001), and cron jobs timing out without fast failure (#45494). The phrase “silently lost” appears across multiple top-voted issues.
- **Observability is insufficient**: Memory management is described as “in chaos” (#43747) with different team members observing completely different storage behaviors. The cost dashboard undercounts daily spend by ignoring archived `.jsonl.reset` files (#46252). The TUI `--session` mode doesn’t live-stream messages (#45388).
- **Windows remains a second-class platform**: The `openclaw update` EBUSY failure (#40540) and the `OPENCLAW_HOME` nested directory bug (#45765) directly affect Windows users.
- **Multi-agent orchestration is fragile**: Users hitting “a cluster of failures” when trying parallel coding batches (#43367), with detached child work and session-lock failures.
- **Sensitive data exposure**: The Discord leak (#44905) where raw model internals surface in channels is a significant confidentiality concern for deployments in shared workspaces.

**Positive Signals:**
- Users are investing deeply in the platform, testing extreme edge cases like 9+ browser signups (#44431), showing high engagement.
- The demand for sophisticated features (cost budgets, memory trust tagging, multi-session architecture) indicates deployment in production or semi-production settings.
- The rapid release cadence (two betas today alone) suggests an actively responsive core team despite the backlog pressure.

## 8. Backlog Watch
Several high-impact issues persist without maintainer action or fix PRs, threatening community trust:

| Issue | Created | Priority | Status |
|---|---|---|---|
| Multi-agent orchestration unstable (#43367) | 2026-03-11 | P1 | `needs-maintainer-review`, `no-new-fix-pr` |
| Session hangs on compaction timeout (#43661) | 2026-03-12 | P1 | `needs-maintainer-review`, `no-new-fix-pr` |
| Discord tool-call leak (#44905) | 2026-03-13 | P1 | `needs-maintainer-review`, `no-new-fix-pr` |
| Windows update EBUSY (#40540) | 2026-03-09 | P1 | `needs-maintainer-review`, `needs-live-repro` |
| Control UI Avatar broken (#41201) | 2026-03-09 | P1 | `needs-maintainer-review`, `needs-security-review`, `no-new-fix-pr` |
| Memory Trust Tagging (#7707) | 2026-02-03 | P2 | Needs product decision — oldest feature request in top 50 |
| Per-agent cost budget (#42475) | 2026-03-10 | P2 | Needs product decision, no-new-fix-pr |
| WebSocket URL clears token (#41545) | 2026-03-09 | P2 | UX regression — editing URL removes token silently |
| Memory preservation across `/new` (#40418) | 2026-03-09 | P2 | Needs security review, overlapping with #45608 |
| Backup CLI exclude patterns (#40786) | 2026-03-09 | P2 | Needs product decision — security risk without exclusion |

The most concerning item on this list is the **P0 Gateway Memory Leak** (#91588), which has no linked fix PR and is driving OOM crashes in production deployments. The **Windows update bug** (#40540), now over three months old with no traction, risks alienating the Windows user base. The **Memory Trust Tagging** feature (#7707), open since February, remains the longest-standing top-voted feature without a maintainer decision, highlighting a gap in security-focused feature advancement despite the project’s otherwise rapid innovation pace.

---

## Cross-Ecosystem Comparison

**Cross-Project Ecosystem Comparison Report: AI Agent OSS Landscape**
**Date:** 2026-06-14
**Audience:** Technical Decision-Makers & Developers

---

### 1. Ecosystem Overview

The open-source personal AI agent landscape is bifurcating sharply between high-velocity generalist platforms scaling toward production and focused specialist projects optimizing for specific regions or workflows. Market leaders (OpenClaw, ZeroClaw, Hermes Agent) are absorbing massive community contributions but showing critical strain in stability, security, and maintainer bandwidth. A second tier (IronClaw, NanoBot, PicoClaw) demonstrates healthier cadence with stronger reliability hygiene. Memory persistence, cost governance, and long-running autonomous execution have emerged as the universal engineering challenges defining project maturity. Crucially, Windows and regional IM platform support remain persistent blind spots that constrain total addressable market.

---

### 2. Activity Comparison

| Project | Issues/PRs (24h) | Release Today | Community Health Score | Primary Risk |
|---|---|---|---|---|
| **OpenClaw** | 1,000+ | ✅ 2 Betas | 4/10 — Critical P0 memory leak, silent failures | Stability crisis drowning signal |
| **ZeroClaw** | 90+ | ❌ | 5/10 — S1 regressions in WS, Canvas, macOS | Release velocity vs. hardening gap |
| **Hermes Agent** | 100+ | ❌ | 4/10 — 96% open rate, community outpacing maintainers | Review bottleneck eroding trust |
| **IronClaw** | 24 | ❌ (blocked) | 8/10 — High internal velocity, structured epics | Low community diversity |
| **NanoBot** | 23 | ❌ | 7/10 — Fast bug turnaround, strong PR culture | Critical provider compatibility bugs |
| **CoPaw** | 16 | ❌ | 5/10 — Context data loss, first-contributor queue | Maintainer review bottleneck |
| **PicoClaw** | 7 | ✅ Nightly | 8/10 — Responsive fixes, balanced roadmap | Token drain bug (#3012) unresolved |
| **NanoClaw** | 4 (merged) | ❌ | 8/10 — Healthy architecture consolidation | Low activity volume |
| **LobsterAI** | 2 (closed) | ❌ | 3/10 — Stale PRs since April | Feature degradation risk |
| **Moltis** | 4 | ❌ | 8/10 — Focused, high-quality MCP fix | Fragile single-issue cycle |
| **NullClaw** | 2 | ❌ | 3/10 — Critical cron regression, fix available but stalled | Maintenance responsiveness |
| **TinyClaw / ZeptoClaw** | 0 | ❌ | Dormant | Project abandonment risk |

---

### 3. OpenClaw's Position

**Advantages:**
- **Ecosystem Gravity:** 500 issues + 500 PRs updated daily is unmatched. It is the de facto reference implementation and sandbox for the entire ecosystem.
- **Platform Breadth:** Slack, Telegram, Feishu, WhatsApp, Windows, CLI, TUI — no competitor covers more surface area.
- **Automated Hardening:** The "Clownfish" bot pipeline generates real fixes for core regressions, though not yet scaling to the P0 class.
- **Release Cadence:** Two beta releases in a single day demonstrate aggressive delivery infrastructure.

**Technical Approach Differences:**
- **Architecture:** Monolithic/Swiss-Army-Knife approach vs. ZeroClaw’s modular WASM/plugin strategy and IronClaw's Rust-based specialization.
- **Memory Model:** Lacks autonomous consolidation (Dream Mode), which is an emerging ecosystem requirement. Relies heavily on user-triggered operations.
- **Security Posture:** Lagging — prompt injection (#45740), tool call leaks (#44905), and elevated exec bypass (#46786) remain unpatched. This is the weakest security profile among Tier 1 projects.

**Community Size:** Largest in the ecosystem by a wide margin. However, volume is masking a stability crisis. The P0 gateway memory leak (350MB → 15.5GB) and multi-agent orchestration instability are existential risks for production deployments.

---

### 4. Shared Technical Focus Areas

| Requirement | Affected Projects | Specific Needs |
|---|---|---|
| **Long-Term Memory / Auto-Consolidation** | OpenClaw, Hermes, ZeroClaw, PicoClaw, CoPaw | Autonomous deduplication, context compression under load, pre-reset memory flush, cost-predictable token use |
| **MCP Protocol Maturity** | Moltis, OpenClaw, NanoBot, ZeroClaw | OAuth metadata compliance, version compatibility, GC safety on reconnection |
| **Windows Platform Parity** | OpenClaw, CoPaw, Hermes | Tauri startup regressions (CoPaw #5047), EBUSY updates (OpenClaw #40540), GBK locale crashes (Hermes #45931) |
| **Regional IM Integration** | ZeroClaw (WeChat/Feishu/DingTalk), CoPaw (Zalo), Hermes (WeChat) | Streaming cards, reaction acknowledgments, locale-aware text handling |
| **Channel Delivery Reliability** | IronClaw (Slack loops), OpenClaw (Telegram DMs), NullClaw (cron) | Opaque delivery failures, multi-approval gate loops, silent dispatch loss |
| **Observability & Cost Controls** | OpenClaw, ZeroClaw, Hermes, NanoBot | Accurate spend dashboards, OTel instrumentation, tool-call burst protection |
| **Configuration Safety** | NanoBot, OpenClaw, CoPaw | Env-var resolution leaks, unvalidated config writes, path escape in exec tools |

---

### 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | PicoClaw | CoPaw |
|---|---|---|---|---|---|
| **Architecture** | Monolithic | Modular (WASM/Plugins) | Rust-native crate | Agentic flow engine | Language-aware SaaS wrapper |
| **Target User** | General power user | Developer / Ops | Enterprise / Slack | Workflow builder | Vietnamese / E. Asian market |
| **Security Model** | Reactive (holes open) | S1 leak (#7563) | Structured | Basic | Basic |
| **Stability Priority** | Low (velocity > stability) | Medium | High | High | Medium |
| **Community Source** | Massive grassroots | Dev-heavy | Core team driven | Hobbyist / Sipeed | First-time contributors |

**Key Distinction:** OpenClaw and Hermes are fighting the "complexity tax" of generalist platforms. IronClaw and NanoClaw prioritize architectural integrity. PicoClaw and CoPaw optimize for specific use-cases (agentic evolution, regional localization). Moltis occupies a pure MCP-connectivity niche.

---

### 6. Community Momentum & Maturity

**Tier 1: Hypergrowth Under Fire**
- **OpenClaw:** Scale is the story, but stability is the story behind the story. Community trust is eroding on silent failures.
- **Hermes Agent:** Viral adoption colliding with maintainer throughput. 96% open rate signals a review bottleneck that will fragment the community if not addressed.
- **ZeroClaw:** Ambitious roadmap (Dream Mode, OTel, native plugins) but S1 regressions in core WebSocket/Chat layers signal a need to stabilize before the next wave.

**Tier 2: Productive Cadence**
- **IronClaw:** Highest feature velocity with lowest incident rate. Release PR (#3708) suggests a bundled stable release is imminent.
- **NanoBot:** Fast turnaround on critical bugs (Anthropic temperature fix in hours). Strong community PR culture.
- **PicoClaw:** Balanced bug-fix-to-feature ratio. Modality routing fix turned in 48 hours. Ideal small-project role model.

**Tier 3: Foundation Building**
- **NanoClaw:** Quietly paid down architectural debt with provider capability seams. Ready for a feature phase next.

**Tier 4: Fragile / Stalled**
- **LobsterAI, NullClaw:** Critical functionality regressing (disabled skills callable, cron silent failure). Risk of community exit without maintainer intervention.
- **Moltis:** Small but impactful. Single critical bug fix in flight. Needs scale to survive.

**Tier 5: Dormant**
- **TinyClaw, ZeptoClaw:** No activity. Risk of project abandonment a real concern for developers considering dependency.

---

### 7. Trend Signals

1. **Memory is the Moat.** The highest-voted features across *every* Tier 1/2 project relate to autonomous memory consolidation ("Dream Mode"). The winner of the ecosystem race will be the framework that solves cost-predictable, reliable long-term state. The current state (context wipes, token drain) is the largest barrier to production deployment.

2. **Reliability is the Product.** Silent failures (OpenClaw subagent loss, NullClaw cron, CoPaw context wipe) generate the strongest negative sentiment. "It works" is becoming a stronger differentiator than "it works everywhere".

3. **From Chat to Backend.** The proliferation of reverse proxy support, Docker hardening, hot-reload configs, and WebSocket architectures signals a market pivot from desktop toy to always-on personal infrastructure service.

4. **Cost Governance is a Hard Requirement.** Tool call bursts (#45783), continuous token drain (#3012), and inaccurate cost dashboards (#46252) are driving user anxiety. Any framework that cannot provide deterministic cost bounds will struggle with enterprise adoption.

5. **Security is a Retrofit, Not a Foundation.** Prompt injection, credential leaks, and sandbox bypasses are being addressed reactively across every project. For developers building on these frameworks, supply-chain security and sandboxed execution must be a first-class evaluation criterion.

6. **Regional IMs Drive Adoption.** CoPaw (Zalo/Vietnam), ZeroClaw (WeChat/Feishu), and LobsterAI (China) show that local IM integration is a critical growth vector. Global frameworks ignoring Asian IM platforms are leaving significant market share on the table.

7. **Windows is the Third-Class Citizen.** Every project with a Windows user base reports severe bugs (Tauri slowdowns, EBUSY, GBK crashes). For any enterprise portfolio targeting Windows desktops, this ecosystem gap represents a significant integration risk.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot Project Digest – 2026-06-14

### 1. Today's Overview
NanoBot experienced a highly active development cycle with **18 Pull Requests** and **5 Issues** updated in the past 24 hours, reflecting a project in rapid iteration. The maintainers merged **5 PRs** targeting memory system fixes, WebUI performance, and infrastructure refactoring. A cluster of related environment-variable resolution bugs surfaced following a recent config refactoring, prompting multiple sweeping fixes from the community. No formal release was tagged today, but the project is clearly preparing for a significant stability and feature baseline by consolidating several long-standing branches.

### 2. Releases
None.

### 3. Project Progress (Merged/Closed PRs)

Several critical fixes and enhancements were merged today:

- **Memory & Conversation History (PR #4326):** Merged to resolve Issue #4264. The `idleCompact` mechanism now summarizes the **full unconsolidated session tail** including recent user corrections, preventing incorrect summaries from being written to `history.jsonl`.
- **WebUI Startup & Performance (PR #4327):** Slow HTTP handlers were moved off the gateway event loop, halting the API from blocking on startup. Chat surface now fetches only locally installed CLI apps instead of the full remote catalog at launch.
- **Settings Parity (PR #4313):** Closed a major gap between the WebUI settings panels and raw `config.json` by adding write endpoints for temperature, tool limits, memory, and channels.
- **Architecture (PR #4314):** Resolved a complex import cycle in the tool config schema by introducing a shared `nanobot.config_base` module, paving the way for cleaner third-party tool authoring.
- **Execution Safety (PR #4098):** Hardened the exec tool against relative symlink workspace escapes (Issue #4072) and fixed `pathAppend` to prepend rather than append on Unix, fixing executable lookup precedence (Issue #4083).

---

### 4. Community Hot Topics

- **Anthropic `temperature` Deprecation (Issue #4333 / PR #4334):** User `Ulef1005` discovered that `claude-opus-4-8` and Fable models return 400 errors because the provider only exempted `opus-4-7` from sending the deprecated `temperature` parameter. The community responded immediately with **PR #4334** to widen the omission check. This issue has **0 comments** but a dedicated fix PR, reflecting a fast-moving bug cycle.

- **Environment Variable Regression (Issues #4322, #4323, #4324, #4325; PRs #4323, #4324, #4325):** A string of closely related bugs triggered by `load_config()` returning unresolved `${VAR}` templates. This caused `NameError` crashes on startup (**Issue #4322**), silent transcription failures (**PR #4323**), and broken settings read/write paths (**PRs #4324, #4325**). A major point of user friction being actively patched.

- **Ollama API Support (Issue #193):** This long-standing feature request remains a touchstone topic with **15 comments**, though it received no maintainer response today. The original author noted the lack of an Ollama provider compared to existing vLLM support.

- **MCP Server GC Crash (PR #4303):** A deep technical submission fixing a `RuntimeError` where `_close_server` ran in a different asyncio task during `streamableHttp` reconnection, causing process crashes.

---

### 5. Bugs & Stability

Bugs are ranked by severity. All have corresponding fix PRs actively open or merged:

| Severity | Issue / PR | Description | Status |
|---|---|---|---|
| **Critical** | Issue #4333 / PR #4334 | Anthropic `temperature` parameter blocks all requests for `opus-4-8` / Fable. | Fix open |
| **Critical** | Issue #4322 / PRs #4323-4325 | `NameError: 'session_key'` and env-var resolution failures break startup, transcription, and settings. | Fixes open |
| **High** | PR #4303 | MCP `_close_server` crashes on task exit during streamable HTTP reconnection. | Fix open |
| **High** | PR #4332 | Codex image SSE parser fails on incomplete chunked reads, raising `RemoteProtocolError`. | Fix open |
| **Medium** | Issue #4264 / PR #4326 | Idle compact excluded recent user corrections from summarization. | **Merged** |
| **Low** | Issue #4083 / PR #4098 | `pathAppend` didn't prepend for executable lookup. | **Merged** |

---

### 6. Feature Requests & Roadmap Signals

Several substantial feature submissions signal the project's near-term trajectory:

- **Nanobot TUI (PR #4329):** A massive community submission by `pancacake` introducing an inline interactive TUI for `nanobot agent`. Includes markdown rendering, slash commands, multimodal input (images via local attachments + audio transcription), and session management. A `--classic` flag preserves the old Rich-Live loop.

- **WebUI Automation Management (PR #4330):** A fully fledged automation management surface for the WebUI with list, filter, run, pause/resume, and delete capabilities, plus protected system automation handling. Likely tied to the upcoming agentic workflows feature set.

- **Subagent Model Presets (PR #4291):** Allows subagents spawned via `LLM.spawn()` to use a different model preset than the parent agent. Gated behind `agents.defaults.spawnPresets`. Signals a push toward hierarchical agent architectures.

- **Reverse Proxy / Sub-path Support (PR #4328):** Enables serving the WebUI under a path prefix (e.g., `https://host/nanobot/`). Essential for enterprise/production deployments behind reverse proxies.

- **`tools.file.enable` Flag (PR #4138):** The community is pushing for parity across tool groups—filesystem tools currently lack the `enable` toggle that `exec` and `web` groups already have, limiting secure deployment patterns.

**Prediction:** The env-var resolution fix set is likely to be cherry-picked into a hotfix release this week. The TUI and Automation views are major roadmap items that will likely anchor the next minor version.

---

### 7. User Feedback Summary

**Pain Points:**
- Significant frustration expressed over **breaks from mergers** (the `session_key` crash) and **incomplete provider exceptions** (Anthropic `temperature`). Users are pushing the project hard enough to trigger regressions under load.
- Silent failures in transcription and credential loading due to unresolved env-var templates have eroded trust in the configuration pipeline.
- Users deploying in sandboxed or remote environments are blocked by the lack of a `tools.file.enable` toggle and missing reverse-proxy compatibility.

**Satisfaction:**
- The community is exceptionally engaged, with multiple contributors submitting high-quality PRs (**hamb1y**, **tobrien**, **chengyongru**, **axelray-dev**, **La-Volpe**, **pancacake**).
- Rapid turnaround on critical bugs (Anthropic issue had a fix PR within hours of the bug report).
- Users are actively building advanced features on top of NanoBot (automation UIs, TUI clients, custom providers), indicating a healthy and invested developer ecosystem.

---

### 8. Backlog Watch

Items requiring maintainer attention or response:

- **Issue #193 (Ollama API Support):** 15 comments, created **February 2026**. No maintainer response in over 4 months. The community keeps asking about it relative to existing vLLM support. A roadmap decision is overdue.
- **PR #4138 (`tools.file.enable` toggle):** Open since **June 1, 2026**. No maintainer review or feedback despite matching an established config pattern. Likely a low-risk merge candidate.
- **PR #4291 (Subagent Model Presets):** Submitted **June 11, 2026**. No maintainer commentary yet. Represents a significant architectural feature that would benefit from early guidance.

*All links formatted as `HKUDS/nanobot Issue/PR #[number]`.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-14

---

## 1. Today's Overview

Hermes Agent is experiencing an extraordinary surge of community activity today, with exactly **100 issues and pull requests updated in the preceding 24-hour window**. Of these items, 96 remain open, reflecting a massive influx of user contributions, detailed bug reports, and feature demands. The project achieved a significant milestone by closing the long-running Web UI Gateway feature request, and a wide array of critical bug fixes for authentication, session management, and platform compatibility are actively progressing through the pipeline. The development queue remains heavily loaded with ~48 open PRs, signaling both high community engagement and mounting pressure on maintainers to process a deep backlog.

---

## 2. Releases

No new formal releases were published on this date.

---

## 3. Project Progress

**Merged/Closed Activity:** The project closed four items today:
- **[Issue #501 — Web UI Gateway](https://github.com/NousResearch/hermes-agent/issues/501) (CLOSED):** The most anticipated feature request—a local browser-based interface with streaming, artifacts, and rich rendering—has been resolved, moving Hermes toward parity with major competitors.
- **[Issue #44927 — Streaming auto-follow](https://github.com/NousResearch/hermes-agent/issues/44927) (CLOSED):** Request to restore streaming auto-follow behavior was closed as a duplicate, indicating the project is already tracking this TUI usability improvement.
- **Two Pull Requests** were merged or closed, though their titles are outside the top 20 most-commented PRs in the snapshot.

**Notable Open Changes:**
- **[PR #45925 — Mega Bundle (86 open PRs)](https://github.com/NousResearch/hermes-agent/pull/45925):** A community contributor has cherry-picked 86 open PRs onto a single branch for bulk CI testing and coordinated review, signaling a strong community desire to blast through the review backlog.
- **[PR #45681 — SSL Guard](https://github.com/NousResearch/hermes-agent/pull/45681):** Adds explicit CA bundle validation before provider calls to prevent opaque httpx `[Errno 2]` crashes.
- **[PR #42922 — Native OpenTUI](https://github.com/NousResearch/hermes-agent/pull/42922):** Proposes replacing the current Ink-based TUI with a new default built on OpenTUI/SolidJS/Effect.
- **[PR #45863 — WhatsApp Calling Sidecar](https://github.com/NousResearch/hermes-agent/pull/45863):** Adds optional WebRTC sidecar support for WhatsApp Cloud calls.
- **[PR #40739 — Linear Gateway Integration](https://github.com/NousResearch/hermes-agent/pull/40739):** Full AgentSession integration with Linear’s webhooks and GraphQL API.

---

## 4. Community Hot Topics

The following issues generated the most discussion and reactions today, revealing strong underlying user needs:

**1. Telegram Bot API 10.1 Rich Messages (🔥 Hottest Topic)**
- **[Issue #44428](https://github.com/NousResearch/hermes-agent/issues/44428)** (5 comments, 3 👍)
- **[Issue #45864](https://github.com/NousResearch/hermes-agent/issues/45864)** (Duplicate, 1 comment, 1 👍)
- **Underlying Need:** Users require native rich formatting in Telegram—tables, LaTeX math, collapsible `<details>` blocks, and structured lists—to match the capability of modern chat interfaces. The duplicate submissions and companion PRs ([#45854](https://github.com/NousResearch/hermes-agent/pull/45854), [#45933](https://github.com/NousResearch/hermes-agent/pull/45933)) show this is the community’s top platform-specific demand right now.

**2. Automatic Memory Consolidation ("Auto Dream")**
- **[Issue #10771](https://github.com/NousResearch/hermes-agent/issues/10771)** (8 comments, 5 👍)
- **Underlying Need:** Heavy users report that the agent’s memory degrades over time due to stale relative dates ("yesterday"), redundant entries, and bloat. The community wants a periodic, automated cleanup mechanism to maintain reliability without manual intervention. This is the single highest-upvoted open feature.

**3. Desktop/TUI Streaming UX**
- **[Issue #42366](https://github.com/NousResearch/hermes-agent/issues/42366)** (2 comments, 3 👍)
- **[Issue #44927](https://github.com/NousResearch/hermes-agent/issues/44927)** (2 comments, 3 👍 — CLOSED)
- **Underlying Need:** Users expect fluid, real-time interaction with the agent. The lack of auto-scrolling during streamed output and the disappearing input prompt break the conversational flow and make long outputs difficult to follow. The 6 total emoji reactions indicate this is a core polish issue that affects every desktop user.

**4. Planning Consultant Feature**
- **[Issue #19344](https://github.com/NousResearch/hermes-agent/issues/19344)** (4 comments)
- **Underlying Need:** Users running cost-effective models for daily tasks want a safety valve for complex architectural or security-sensitive decisions. A `/consult` mechanism for frontier-model oversight would allow Hermes to scale across different model tiers without compromising on quality.

**5. Context Compression Race Conditions**
- **[Issue #23975](https://github.com/NousResearch/hermes-agent/issues/23975)** (5 comments, P2)
- **Underlying Need:** The agent’s conversation scaling mechanism is fragile. Incoming gateway messages during compression can corrupt the context, producing fallback summary markers instead of accurate compressed history. Users need robust, background-able context management.

---

## 5. Bugs & Stability

A significant wave of bugs was reported or updated today, predominantly in authentication, agent orchestration, and platform support.

### 📌 P2 (High Severity / Critical)

**Provider & Auth Configuration Fragility**
- **[#44666](https://github.com/NousResearch/hermes-agent/issues/44666):** `api_key_env` alias silently ignored in custom providers → sends `no-key-required` header.
- **[#43586](https://github.com/NousResearch/hermes-agent/issues/43586):** Bare `provider: custom` + `key_env` fails to read key → HTTP 401 on every request.
- **[#45813](https://github.com/NousResearch/hermes-agent/issues/45813):** GitHub Copilot (non-ACP) provider consistently returns `HTTP 400: Bad Request`.
- **[#45674](https://github.com/NousResearch/hermes-agent/issues/45674):** `hermes mcp list` crashes with `AttributeError` when a `mcp_servers` entry is a raw string.

**Agent Core Mechanics**
- **[#31155](https://github.com/NousResearch/hermes-agent/issues/31155):** `delegation.model` override in config is entirely ignored; subagents always inherit the parent model.
- **[#42405](https://github.com/NousResearch/hermes-agent/issues/42405):** Memory capacity retry loop — `replace` fails via zero-match substring, then hangs silently with no user response.
- **[#45783](https://github.com/NousResearch/hermes-agent/issues/45783):** Session resume triggers a massive tool call burst (581+ calls in under 2 minutes), causing severe API cost spikes.

**Session & Data Integrity**
- **[#19245](https://github.com/NousResearch/hermes-agent/issues/19245):** `session_search` returns empty after a crash due to orphaned session JSON.
- **[#33907](https://github.com/NousResearch/hermes-agent/issues/33907):** Context compression creates orphan sessions missing from `state.db`.

**Platform Blockers**
- **[#40187](https://github.com/NousResearch/hermes-agent/issues/40187):** `hermes update` / `hermes desktop` fails at the Electron builder stage on macOS.
- **[#45860](https://github.com/NousResearch/hermes-agent/issues/45860):** Three distinct Windows installation bugs (missing `hermes.exe`, path corruption).
- **[#45792](https://github.com/NousResearch/hermes-agent/issues/45792):** Docker container doesn't understand its mounted config environment.
- **[#45931](https://github.com/NousResearch/hermes-agent/issues/45931):** WeChat gateway polling thread hangs silently on Chinese Windows (GBK locale).
- **[#45932](https://github.com/NousResearch/hermes-agent/issues/45932):** Gateway fails to start with `UnicodeDecodeError: 'gbk' codec` during dashboard token read.

### 📌 P3 (Moderate / Polish)
- **[#45493](https://github.com/NousResearch/hermes-agent/issues/45493):** Matrix thread-initial message lost on next turn.
- **[#45834](https://github.com/NousResearch/hermes-agent/issues/45834):** Duplicate patches in global and profile directories applied twice.
- **[#45877](https://github.com/NousResearch/hermes-agent/issues/45877):** Cron background review blocks read-only tools (`read_file`, `search_files`).
- **[#45921](https://github.com/NousResearch/hermes-agent/issues/45921):** TUI directory selection button missing when too many directories exist.
- **[#42228](https://github.com/NousResearch/hermes-agent/issues/42228):** Compressed TUI sessions lose their workspace context to "No workspace" group.

### Active Bug-Fix PRs in Queue
- [#45937](https://github.com/NousResearch/hermes-agent/pull/45937) (Dashboard UTF-8 encoding on Windows)
- [#45934](https://github.com/NousResearch/hermes-agent/pull/45934) (WeChat poll transport failure recovery)
- [#45930](https://github.com/NousResearch/hermes-agent/pull/45930) (False local Ollama length truncation)
- [#45868](https://github.com/NousResearch/hermes-agent/pull/45868) (Skills config reference vs. mutation distinction)
- [#45938](https://github.com/NousResearch/hermes-agent/pull/45938) (Overflow stream chunk editing)

---

## 6. Feature Requests & Roadmap Signals

### 🔮 Imminent (Active PRs / Explicit Opt-In Work Exists)
- **Telegram Bot API 10.1 Rich Messages:** Opt-in guardrails already built in **[PR #45933](https://github.com/NousResearch/hermes-agent/pull/45933)** .
- **WhatsApp Cloud Calling Sidecar:** PR [#45863](https://github.com/NousResearch/hermes-agent/pull/45863) adds the `/offer` client seam.
- **Overflow Stream Editing:** PR [#45938](https://github.com/NousResearch/hermes-agent/pull/45938) keeps overflowing chunks editable.
- **Desktop Completion Cues:** PR [#42480](https://github.com/NousResearch/hermes-agent/pull/42480) introduces 14 Web Audio synthesized turn-end sounds.
- **Linear Gateway Integration:** PR [#40739](https://github.com/NousResearch/hermes-agent/pull/40739) provides full issue/session webhook handling.

### 📈 High Demand (Strong Community Signal, Requires Design)
- **Automatic Memory Consolidation** ([#10771](https://github.com/NousResearch/hermes-agent/issues/10771)): The highest-upvoted open feature (5 👍). Periodic memory cleaning and deduplication.
- **Planning Consultant** ([#19344](https://github.com/NousResearch/hermes-agent/issues/19344)): A `/consult` mechanism for model-tier orchestration.
- **WhatsApp Message Templates** ([#45935](https://github.com/NousResearch/hermes-agent/issues/45935)): Business re-engagement messaging outside the 24-hour window.

### 🛤️ Roadmap Signals
- **Web UI Gateway (#501)** is now closed—a major roadmap checkbox checked, putting Hermes on par with competitors.
- **Mega Bundle PR (#45925)** suggests the community is pushing for a faster, batch-oriented review process. This may pressure maintainers toward CI-based auto-merge strategies.
- **Native OpenTUI (#42922)** represents a potential wholesale TUI replacement that would fundamentally change the desktop interaction model.

---

## 7. User Feedback Summary

**👍 Satisfaction Drivers:**
- The project’s velocity remains a strong magnet for contributors, who are submitting a torrent of well-structured PRs.
- Multi-platform support (Telegram, Discord, WhatsApp, CLI, Home Assistant, now Web UI) aligns well with power-user desires.
- The quick opt-in approach to new features (e.g., Telegram rich messages) shows sensible risk management.

**👎 Dissatisfaction & Pain Points:**
- **Configuration Complexity:** The auth/provider configuration system is the most common source of bugs. Error messages are actively misleading (e.g., silently defaulting to `"no-key-required"`). Users are demanding clearer validation, error surfacing, and documentation.
- **Memory Rot:** Without automatic consolidation, heavy users report degrading performance over days of use. This is the community’s #1 most-wanted feature.
- **Desktop UX Immaturity:** The TUI/Desktop client lacks basic fluid interaction (auto-scrolling, persistent prompts), which is a standard expectation for an agent chat interface.
- **Platform Imbalance:** Users on Matrix, WeChat, and Chinese Windows (GBK) encounter significantly more bugs and missing features, feeling like second-class citizens.
- **Cost Risk:** The tool call burst on session resume (#45783) is an acute billing vulnerability that erodes trust in unattended operation with API-based providers.

---

## 8. Backlog Watch

*The following older items represent significant bugs or features that have not yet received formal resolution or merge and require maintainer attention.*

- **[#10771 — Auto Dream Feature Request](https://github.com/NousResearch/hermes-agent/issues/10771)** *(Created: 2026-04-16)*: The community’s most upvoted open feature (5 👍, 8 comments) with no visible maintainer response or assigned milestone. Architectural decision needed.

- **[#17480 — fix(auth): Codex usage credentials](https://github.com/NousResearch/hermes-agent/pull/17480)** *(Created: 2026-04-29)*: An open fix PR for **7 weeks**. Critical for users relying on Codex provider billing. Unmerged despite no obvious blockers in the summary.

- **[#21774 — fix: Google Workspace OAuth](https://github.com/NousResearch/hermes-agent/pull/21774)** *(Created: 2026-05-08)*: Open for **5 weeks**. Completely blocks Google Workspace tool usage for all users.

- **[#22532 — feat: Telegram clarify prompts](https://github.com/NousResearch/hermes-agent/pull/22532)** *(Created: 2026-05-09)*: Open for **5 weeks**. Adds structured clarification choices to Telegram sessions.

- **[#31155 — delegation.model override ignored](https://github.com/NousResearch/hermes-agent/issues/31155)** *(Created: 2026-05-23)*: Open for **3 weeks**. A core configuration contract—the ability to run subagents on a different model—is entirely broken.

- **[#40187 — macOS Desktop compilation fails](https://github.com/NousResearch/hermes-agent/issues/40187)** *(Created: 2026-06-06)*: Completely blocks an entire platform from the desktop application for over a week.

- **[#37027 — fix(tts): Telegram voice bubble](https://github.com/NousResearch/hermes-agent/pull/37027)** *(Created: 2026-06-01)*: Voice notes are silently swallowed in follow-up tool turns. Fix has been open for two weeks.

- **[#45925 — Mega Bundle PR](https://github.com/NousResearch/hermes-agent/pull/45925)** *(Created: 2026-06-14)*: While well-intentioned, a single PR merging 86 open changes is inherently high-risk for regressions and merge conflicts. This requires careful, structured maintainer triage to unpack into manageable chunks.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-06-14**.

---

## PicoClaw Project Digest – 2026-06-14

### 1. Today's Overview
The PicoClaw project is in a highly active engineering state today, with **5 pull requests merged** and **2 issues updated** in the last 24 hours. A new nightly release (`v0.2.9-nightly.20260614.cf67dd38`) is now available, bundling the latest merges for testing. The core team has shown strong responsiveness by shipping a critical fix for a modality routing hallucination bug (#3108) within 24 hours of its report. However, a high-severity bug concerning continuous token consumption under Evolution (#3012) remains open and is the primary concern for the user community. Overall, the project shows a healthy balance of urgent bug fixes, code quality improvements, and the continued development of substantial features like image compression and remote agent modes.

### 2. Releases
A single new release was published today:
- **Nightly:** `v0.2.9-nightly.20260614.cf67dd38`
  - *Details:* This is an automated nightly build that reflects the current state of the `main` branch. It may be unstable.
  - *Changelog:* [Full Changelog: v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

*No breaking changes or specific migration notes are documented for this build.*

### 3. Project Progress
Five pull requests were merged or closed today, signaling significant forward momentum on agent reliability and codebase health:

- **Modality Routing Fix (Critical):**
  - **[PR #3117](sipeed/picoclaw PR #3117) fix(agent): route media turns to image models** – Merged. Fixes the hallucination bug (#3108) by ensuring the agent correctly routes image descriptions to vision-capable models instead of retrying on text-only models.

- **Text-to-Speech Flexibility:**
  - **[PR #3119](sipeed/picoclaw PR #3119) fix(tts): support OpenRouter voice overrides and fallback** – Merged. Introduces per-model override for `voice` and `response_format` via the `extra_body` config, along with an automatic single-retry fallback.

- **Code Quality & Linting:**
  - **[PR #3065](sipeed/picoclaw PR #3065) fix(seahorse): explicitly ignore Close() errors on PRAGMA/migration failure paths** – Merged.
  - **[PR #3066](sipeed/picoclaw PR #3066) fix: explicitly ignore Close() errors on temp file write/sync failure paths** – Merged. Both PRs improve code hygiene by silencing linter warnings on error paths in the Seahorse module and file operations.

- **Documentation Housekeeping:**
  - **[PR #2935](sipeed/picoclaw PR #2935) docs(i18n): add Traditional Chinese (zh-TW) locale and READMEs** – Closed as stale after being open since May 24.

### 4. Community Hot Topics
The most active topic in the community right now is a single ongoing bug report:

- **High Activity: [Issue #3012](sipeed/picoclaw Issue #3012) [BUG] Continuous consumption of tokens every minute when evolution is enabled**
  - *Author:* xpader | *Comments:* 3 | *Updated:* 2026-06-13
  - *Analysis:* This is the most active thread based on user engagement. The bug describes a scenario where enabling Evolution Mode (Draft type, Code Path trigger) with MiniMax causes constant token drain even without active user interaction. The underlying demand is for predictable cost control and reliable autonomous agent workflows. **No fix PR has been linked yet.**

### 5. Bugs & Stability

- **Critical / High Severity:**
  - **[Active] Issue #3012 – Continuous Token Consumption:**
    A confirmed bug where enabling Evolution Mode results in a continuous drain of tokens. This poses a direct billing/resource exhaustion risk. **No fix exists yet.** Highly prioritized by the community.
  - **[Resolved] Issue #3108 – Image Hallucination with Text Models:**
    Resolved by PR #3117. The bug caused the agent to hallucinate responses when a text-only model (e.g., `deepseek/deepseek-v4-flash`) was asked to describe an image. The fix correctly routes media to the proper image model.

- **Low / Medium Severity:**
  - **Error Handling Gaps ([PR #3065](sipeed/picoclaw PR #3065), [PR #3066](sipeed/picoclaw PR #3066)):** The project fixed instances of silently ignoring errors from `db.Close()` and `tmpFile.Close()` on failure paths. These are standard stability improvements to prevent edge-case resource leaks.
  - **TTS Stability ([PR #3119](sipeed/picoclaw PR #3119)):** The new retry fallback mechanism for TTS addresses transient provider errors, specifically around unsupported `response_format` parameters.

### 6. Feature Requests & Roadmap Signals

The following features are strong signals for the project's direction:

- **In Development / In Review:**
  - **Image Compression Pipeline ([PR #2964](sipeed/picoclaw PR #2964)):** Author afjcjsbx has a substantial PR open to add configurable multi-level image compression before building model payloads. This directly addresses overflow errors from high-resolution inputs. Likely a candidate for the next stable release.
  - **Remote WebSocket Agent Mode ([PR #3118](sipeed/picoclaw PR #3118)):** A new feature adding a `--remote ws://...` flag to the `picoclaw agent` command. This signals architectural work toward headless/distributed agent deployments.

- **Recently Shipped:**
  - **Flexible TTS Configuration (#3119):** User demand for overriding provider-specific TTS parameters (voice, format) has been satisfied via the `extra_body` field.
  - **Robust Modality Routing (#3117):** The system now has a foundation for correctly splitting media and text tasks across appropriate models, a prerequisite for reliable multimodal usage.

### 7. User Feedback Summary
- **Pain Points:**
  - **Cost Unpredictability:** The token drain bug (#3012) is the dominant user complaint. Trust in the Evolution workflow's cost model is currently low.
  - **Contextual Ignorance:** The hallucination bug (#3108) demonstrated a failure in context switching between text and vision models. Users expect the agent to seamlessly handle multimodal tasks without producing unrelated outputs.

- **Satisfaction & Signals:**
  - **High Responsiveness:** The fact that PR #3117 was authored and merged within roughly 48 hours of issue #3108 being filed signals a responsive development team, which boosts confidence.
  - **Demand for Advanced Networking:** The creation of PR #3118 implies a user desire to run PicoClaw agents as detached remote services.

### 8. Backlog Watch

- **High Priority (Requires Maintainer Action):**
  - **[Issue #3012](sipeed/picoclaw Issue #3012) – Continuous Token Consumption:** Open since June 5 without a linked fix. Given the direct billing implications, this represents the largest gap in user experience today.
  - **[PR #2964](sipeed/picoclaw PR #2964) – Feat/image input compression:** A long-running feature PR (opened May 28) that requires close review due to the breadth of the vision pipeline changes.

- **Needs Architectural Review:**
  - **[PR #3118](sipeed/picoclaw PR #3118) – Remote Pico WebSocket Mode:** Freshly submitted by a new contributor (jp39). This is a foundational architectural change that needs alignment with the project's long-term networking and security model.

- **Stale Items:**
  - **[PR #2935](sipeed/picoclaw PR #2935) – Traditional Chinese Locale:** Closed as stale. If the project intends to support i18n deeply, the closure of this PR without an alternative plan may require a statement from maintainers to manage community expectations.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the structured NanoClaw project digest for 2026-06-14.

---

**Project Digest: NanoClaw (github.com/nanocoai/nanoclaw)**

**Date:** 2026-06-14
**Trend:** Consolidation & Hardening
**Activity Level:** Moderate

---

**1. Today's Overview**
Project activity saw a significant shift from external issue influx to internal feature integration and stability work. No new releases were published. The maintainer team merged four open-sourced feature PRs authored by *omri-maya* that together define a new extensibility seam for providers (capability registration, memory scaffolding, runner hooks, and SDK bump). Meanwhile, two complex open PRs targeting hard production bugs (“stale outbound.db journals” and “multi-agent health audit findings”) received updates, signaling a strong ongoing focus on hardening the host runtime. No new bugs or feature requests were filed by the community today, suggesting a quiet period or that current open PRs cover the most pressing reported issues.

**2. Releases**
*No new releases were published today.*

**3. Project Progress**
Four pull requests were merged/closed today, all authored by *omri-maya*. These represent a coordinated push to standardize and extend the provider interface:

- **PR #2754** (feat(runner): onExchangeComplete provider hook + slash-command interruption)
  - Adds an optional hook for provider-side logic at the end of an exchange, plus infrastructure for in-flight slash-command handling.
- **PR #2747** (feat(onecli): SDK 2.2.1 — credential-stub mounts + machine-checkable pins)
  - Major bump of the `@onecli-sh/sdk` from 0.5.0 to 2.2.1, introducing credential-stub mounting and pin verification. Likely impacts how credentials are handled at the OS/filesystem level.
- **PR #2746** (feat(providers): agent-surfaces capability seam)
  - Creates a host-side registry where providers declare their capabilities, standardizing feature discovery across the agent ecosystem.
- **PR #2745** (feat(memory): opt-in persistent memory scaffold for providers)
  - Introduces a reusable scaffold (`usesMemoryScaffold`) enabling providers to maintain state persistently across sessions without managing raw storage.

**4. Community Hot Topics**
While explicit discussion metadata is sparse (comments are undefined in the data), the most focused development energy is on two critical open pull requests updated today:

- **PR #2750 [OPEN]** — [fix: recover stale outbound.db journals after container kills (Fixes #2516, #2640)](https://github.com/nanocoai/nanoclaw/pull/2750)
  - **Underlying Need:** Users hit data corruption or read-only lock states when containers are killed abruptly. The PR repairs stale journals and reclassifies poll races to prevent data loss.
- **PR #2732 [OPEN]** — [Harden host + agent-runner from health audit findings](https://github.com/nanocoai/nanoclaw/pull/2732)
  - **Underlying Need:** An adversarial health audit revealed systemic gaps—Docker Desktop `drvfs` crash-loops (exit 127), missing container crash circuit breakers, lack of `MAX_CONCURRENT_CONTAINERS` enforcement, and insufficient daemon-level failover. This is a broad reliability block.

**5. Bugs & Stability**
*No new bugs were filed today.* The stability effort is concentrated on fixing previously reported issues:

- **Critical — Database Persistence After Container Kill**
  - **Bugs:** Referenced in Issues #2516 and #2640. Stale journal files and race conditions in the `outbound.db` hot-journal poller cause agent data loss or unavailability when containers are SIGKILLed.
  - **Fix Status:** PR #2750 (open, actively updated) implements stale journal recovery and race classification.

- **High — Host & Agent-Runner Stability**
  - **Bugs:** Discovery from health audit: crash-on-spawn (exit 127), bind-mount source misconfiguration in Docker Desktop (`drvfs`), missing daemon fallbacks.
  - **Fix Status:** Comprehensive fix in PR #2732 (open, active).

**6. Feature Requests & Roadmap Signals**
The merged features today strongly signal the direction of the project:

- **Provider Extensibility:** The new *agent-surfaces capability seam* (#2746) and *persistent memory scaffold* (#2745) suggest the maintainers are formalizing a “provider SDK” vision where external integrations can confidently declare features and maintain state.
- **Operational Lifecycle:** The `onExchangeComplete` hook (#2754) indicates a roadmap focused on observability and cleanup hooks.
- **Hardening First:** The high-profile PR #2732 (health audit fixes) is a strong signal that production container compatibility (Docker Desktop, concurrency limits, circuit breakers) is the top operational priority for the next release.

**Predictions for next release:** The features in #2754, #2753 (not in this batch?), #2747, #2746, and #2745 will likely ship together as a major provider interface version. PRs #2750 and #2732 are strong candidates for the same release or a subsequent patch.

**7. User Feedback Summary**
- **Pain Points (Operational):** Users are experiencing tangible pain running the host on Docker Desktop (`drvfs` staging failures, exit 127) and are demanding better crash/post-kill database recovery. These are being directly addressed in the two large open PRs.
- **Contribution Culture:** The project credits original bug reporters (#2516, #2640) and appears to act on external security/health audits, indicating a healthy feedback loop with the community.
- **Use Cases:** The provider capability seam (#2746) and memory scaffold (#2745) suggest that the community is pushing for deeper integration, likely for custom tool builders and enterprise agent deployments.

**8. Backlog Watch**
- **PR #2732** (Harden host + agent-runner, _created_ 2026-06-11) — This is a large, multi-fix PR that has been open for 3 days. It touches core lifecycle logic (container spawning, daemon kill fallback, circuit breakers). Due to its size and criticality, it requires careful review to prevent regressions. Ensuring it doesn’t languish should be a priority.
- **PR #2750** (Database journal fix, _created_ 2026-06-12) — Received an update today. It addresses critical bugs for users running in containerized environments. High priority.
- No long-stale user issues are visible in the current data window.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — June 14, 2026

## 1. Today's Overview
The NullClaw project shows light but highly focused activity centered on a critical bug impacting scheduled agent tasks. No new releases or merges occurred in the past 24 hours, and project activity is dominated entirely by a single open Issue (#941) and its corresponding fix (#954). While overall velocity is low, the depth of technical analysis from the community signals strong engagement with the project's core scheduling engine. The project's health is stable, though the resolution of this regression will be a key indicator of maintainer responsiveness.

## 2. Releases
No new releases were published in the current reporting period.

## 3. Project Progress
No pull requests were merged or closed today. Development momentum is concentrated entirely on **PR #954** ("Fix: one-shot cron jobs silently fail to deliver messages"), which is open and awaiting review. Authored by *vernonstinebaker*, this PR directly targets the root cause of the community's primary pain point. The project has not yet integrated a fix, but a concrete, technically validated patch exists in the pipeline.

## 4. Community Hot Topics
The singular hot topic is **Issue #941** — "Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens" ([View Issue](https://github.com/nullclaw/nullclaw/issues/941)).

- **Comments:** 7 (highest activity in dataset)
- **Created:** 2026-05-31 (now 14 days open)
- **Reactions:** None currently

The community has deeply analyzed this failure mode, identifying that the job lifecycle completes successfully in the scheduler without ever calling the agent subprocess. The underlying need is deterministic reliability: users require scheduled agent tasks to execute silently and correctly without manual verification. The associated **PR #954** ([View PR](https://github.com/nullclaw/nullclaw/pull/954)) demonstrates that the community has moved from reporting to diagnosing the root cause—a use-after-free in the `OutboundMessage.channel` pointer.

## 5. Bugs & Stability
**Critical Severity**

| ID | Title | Severity | Status | Fix Available |
|---|---|---|---|---|
| [#941](https://github.com/nullclaw/nullclaw/issues/941) | Agent-type cron jobs silently fail to deliver | **Critical** | Open | Yes (PR #954) |

This bug represents a **silent functional regression**: scheduled `agent-type` jobs are marked as completed in `cron.json` without the agent subprocess ever being spawned. No message arrives on any configured delivery channel (Telegram, Mattermost, etc.). There is no error feedback to the user, creating a trust-breaking "silent failure" scenario.

**Root Cause (per PR #954):** Use-after-free on the `OutboundMessage.channel` pointer, causing the delivery engine to read freed memory and abort the dispatch path without raising exceptions visible to the user.

## 6. Feature Requests & Roadmap Signals
No new feature requests were submitted in the last 24 hours. However, the intense technical scrutiny of Issue #941 sends a roadmap signal: the memory safety and lifecycle management of `OutboundMessage` and agent subprocesses are weak points in the current architecture. Users are relying on scheduled agent dispatches as a core workflow. Future releases may need to prioritize:
- Robust subprocess lifecycle monitoring
- Non-silent error propagation from the delivery pipeline
- Integration tests for cron + agent + channel delivery paths

## 7. User Feedback Summary
**Primary Pain Point:** Silent failure of scheduled tasks. User *weissfl* (Issue #941) reports a scenario where the system reports success (job marked complete in `cron.json`) but the actual execution (agent subprocess spawn, message delivery) never occurs. This erodes trust in the scheduling subsystem.

**Use Case Impacted:** Automated daily/weekly agent dispatches to messaging channels (Telegram, Mattermost). This is likely a production workflow powering automated reporting, monitoring summaries, or personal assistant broadcasts.

**Satisfaction Level:** Indeterminate but strained. The community member invested significant effort in detailed reproduction steps and the PR author provided a precise analysis, indicating investment in the project's success. The lack of merge velocity is the primary risk to satisfaction.

## 8. Backlog Watch
**High Priority Item:**
- **Issue #941** (Created 2026-05-31, Updated 2026-06-13): Open for two weeks with a fix available in PR #954. This issue has sustained community attention and a reviewer decision is the primary bottleneck.

**No additional aging items** were identified in the provided dataset. The project maintains a tight, current backlog outside of this single critical bug. Maintainer action on PR #954 in the coming days will be the clearest signal of project health and governance velocity.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**IronClaw Project Digest – 2026-06-14**

---

### 1. Today's Overview
The project exhibited very high development velocity, with **24 PRs updated** and **7 merged/closed** in the last 24 hours. Core output was split between finalizing the **Attachment pipeline** (Epic #4644) and an aggressive **Slack + Reborn stability** push. Despite the intense code churn, no new releases were cut, and the Nightly E2E suite remains in a failing state. The activity strongly signals that the team is sprinting toward a bundled release containing major UX improvements for file handling, Slack delivery, and run error recovery.

---

### 2. Releases
**No new releases were published today.** A release PR ([#3708](nearai/ironclaw#3708)) that cuts new versions of `ironclaw_common`, `ironclaw_safety`, `ironclaw_skills`, and the main `ironclaw` crate remains open and undergoing updates, suggesting the next public release is deliberately held to bundle the large-scale features and fixes currently in flight.

---

### 3. Project Progress
The flurry of merged PRs today completes the full backend for the **Attachment** feature and includes a high-priority security fix:

**Merged/Closed:**
- **Attachment Pipeline (Epic #4644):**
  - `refactor(extractors): extract file text-extraction into ironclaw_extractors crate` ([#4675](nearai/ironclaw#4675)) – Extracts pure text-reading logic into a standalone leaf crate.
  - `feat(attachments): MountView-based attachment landing crate` ([#4668](nearai/ironclaw#4668)) – Provides byte-storage foundation for inbound files.
  - `feat(attachments): bridge inbound bytes into transcript AttachmentRefs` ([#4670](nearai/ironclaw#4670)) – Connects storage to transcript persistence.
  - `feat(threads): carry attachment refs through the Reborn transcript contract` ([#4655](nearai/ironclaw#4655)) – Adapts the formerly text-only transcript to carry `AttachmentRef`s.
  - `feat(reborn): accept inline attachment uploads on the WebChat v2 send path` ([#4672](nearai/ironclaw#4672)) – Wires the browser upload path end-to-end.
- **Security/Dependencies:**
  - `chore(deps): bump tar from 0.4.45 to 0.4.46` ([#4242](nearai/ironclaw#4242)) – Fixes a PAX header vulnerability.

**Active Progress:**
- `feat(attachments): extract document text on the inbound landing path` ([#4676](nearai/ironclaw#4676)) and `feat(threads): fold attachment text into model-visible context` ([#4677](nearai/ironclaw#4677)) are the remaining open attachment tracks, bringing extracted text into model context.

---

### 4. Community Hot Topics
While almost all activity comes from the core team, two deep workstreams dominate the conversation:

- **Slack Reliability & Auth Gate Refactoring:** PRs from **henrypark133** dominate the activity log.
  - `fix: preserve invocation identity across auth-gate re-dispatch (Slack re-approval loop)` ([#4839](nearai/ironclaw#4839))
  - `fix(slack): single-flight gate delivery per run_id` ([#4843](nearai/ironclaw#4843))
  - `fix(slack): filter delivered gate routes by raw gate string` ([#4844](nearai/ironclaw#4844))
  - **Underlying need:** Users in Slack QA are hitting multi-step approval loops and opaque message delivery failures. The stack of fixes aims to make Slack a first-class, one-time-approval channel.

- **Reborn Runtime Stability:**
  - `reborn: no run-borking failures — failure explanation + retryable failed runs` ([#4841](nearai/ironclaw#4841)) from **serrrfirat** is a major initiative to replace silent, non-recoverable crashes with understandable explanations.
  - **Underlying need:** Users need trust that a failing agent run will either recover or explain precisely *why* it failed.

- **New Contributor Feature:** `feat(gateway): add routine create endpoint` ([#4264](nearai/ironclaw#4264)) from **wcc945** adds a REST API for routine creation, receiving updates but awaiting maintainer review.

---

### 5. Bugs & Stability
Issues and fix PRs are ranked below by severity:

| Severity | Issue / PR | Description | Status |
|---|---|---|---|
| **Critical** | [#4108](nearai/ironclaw#4108) | **Nightly E2E scheduled run failed** – Persistent CI failure on `v2-engine`. | Open since May 27, updated yesterday. No linked standalone fix. |
| **High** | [#4839](nearai/ironclaw#4839) | **Slack re-approval loop** – Users forced through four approval gates for one logical call. | Fix PR #4839 open, coupled with #4843 and #4844. |
| **High** | [#4841](nearai/ironclaw#4841) | **Run-borking terminal errors** – `HostUnavailable`, model failures, protocol errors kill the run with no recovery path. | Fix PR #4841 open (making failures explainable + runs retryable). |
| **High** | [#4843](nearai/ironclaw#4843) | **Gate resolution-ack fanout bug** – Duplicate delivery of gate resolutions hangs channels. | Fix PR #4843 open. |
| **Medium** | [#4838](nearai/ironclaw#4838) | **Busy thread parking** – Messages arriving during a holding run were parked indefinitely. | Fix PR #4838 replaces parking with explicit rejection. |
| **Medium** | [#4844](nearai/ironclaw#4844) | **Gate kind filter regression** – Per-route allocation caused routing failures. | Fix PR #4844 refactors to raw string filtering. |
| **Low** | [#4846](nearai/ironclaw#4846) | **Bare workspace tool paths** – Paths nested incorrectly under `workspace/workspace/`. | Fix PR #4846 open with regression tests. |

---

### 6. Feature Requests & Roadmap Signals
Three major feature tracks are crystallizing for the upcoming release:

- **File Attachments for the Model (Epic #4644):** The base pipeline is now merged. The remaining open PRs ([#4676](nearai/ironclaw#4676), [#4677](nearai/ironclaw#4677)) will finalize text extraction and inject it into the model's context window. **Highly likely for the next release.**
- **Runtime Context Awareness ([#4836](nearai/ironclaw#4836)):** PR #4836 implements a new runtime slice telling the model which channels are connected, where outbound delivery is pointed, and how the run originated. This is a strong signal toward *Agentic Slacks/Routines* that can self-discover their environment.
- **Routine Creation UX (PR [#4264](nearai/ironclaw#4264) & PR [#4780](nearai/ironclaw#4780)):** A new REST API for routines and model-visible delivery target guidance indicate a drive to make routine management less opaque.

---

### 7. User Feedback Summary
Direct user pain points are strongly implied by the targeted bug fix cycles:

- **Slack Loops & Opaque State:** The biggest reported UX issue. Users in QA environments hit repeated OAuth approvals and had no visibility into whether Slack was "connected." Fixes in [#4777](nearai/ironclaw#4777) (persisting Slack state) and [#4839](nearai/ironclaw#4839) (fixing the re-approval loop) directly address this.
- **Silent Failure / Run-Borking:** Opaque crashes are a top pain point. PR [#4841](nearai/ironclaw#4841) explicitly targets converting "opaque code, no recovery path" into "explained to the user, retryable."
- **Attachments:** The inability of the model to see uploaded documents has been a major functional gap. The completion of the ingestion pipeline (Epic #4644) closes this heavily requested use-case.
- **Satisfaction Signals:** The rapid fix cycle (4 Slack-specific PRs today) and major architecture investment in crash recovery indicate a team that is highly responsive to early adopter feedback.

---

### 8. Backlog Watch
Items requiring maintainer attention to unblock project momentum:

- **Nightly E2E Failure ([#4108](nearai/ironclaw#4108)):** Updated yesterday. Open since May 27. This is a critical CI blocker for the `v2-engine` and should be a top priority. The heavy refactoring activity may be the root cause, but awareness is key.
- **Release PR ([#3708](nearai/ironclaw#3708)):** Open since May 16. This PR is the bottleneck for getting the Slack fixes, attachment features, and stability improvements to end users. It contains API-breaking changes in `ironclaw_common` and `ironclaw_skills` that need careful shepherding to merge.
- **New Contributor PR – Routine API ([#4264](nearai/ironclaw#4264)):** Open since May 31 from **wcc945**. This adds a missing REST endpoint and aligns well with the active work in [#4780](nearai/ironclaw#4780). Prompt review would encourage the contribution and unblock the gateway team.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured project digest for **LobsterAI** based on GitHub activity recorded on **2026-06-14**.

---

### 1. Today's Overview

LobsterAI enters a quiet but active maintenance phase on 2026-06-14. No new issues or releases were filed, but the team successfully closed two UI-focused pull requests related to the MCP modal and macOS keyboard shortcuts. However, a clear bifurcation in project health is visible: while these hotfixes made it through, the vast majority of open action items—three PRs and four bugs—remain tagged as `[stale]`, untouched since early April. The data suggests the project is carefully balancing incremental reliability fixes against a growing backlog of unresolved feature work and core logic bugs, which may be signaling a resource constraint on the maintainer side.

### 2. Releases

**None.**
No new releases were cut in the last 24 hours. The repository has not shipped a release label across the reported timeline.

### 3. Project Progress

Two pull requests were closed in the reporting period, reflecting concrete user-facing improvements:

- **PR [#1466](netease-youdao/LobsterAI/pull/1466) (Closed):** Resolved a critical UI bug where the close and cancel buttons in the MCP server configuration modal became unreachable when the form content grew tall. The fix properly isolates the scroll container from the modal panel.
- **PR [#1467](netease-youdao/LobsterAI/pull/1467) (Closed):** Addressed a cross-platform UX discrepancy where keyboard shortcuts displayed `Ctrl` on macOS instead of the standard `⌘`. The fix implements proper runtime platform detection.

Both fixes target the settings and configuration UIs, indicating a recent focused effort on hardening the platform layer.

### 4. Community Hot Topics

While the volume of discussion remains low (max 2 comments on any thread), several high-signal items define the current community focus:

- **OpenClaw Compatibility ([Issue #1443](netease-youdao/LobsterAI/issues/1443)):**
  The most commented issue (2 comments). A user reports that updating to `openclaw v2026.3.24` breaks their local stack due to upstream breaking changes. Underlying need: the community requires formal compatibility guarantees or a migration guide for major version bumps in core dependencies.

- **Disabled Skills Logic ([Issue #1439](netease-youdao/LobsterAI/issues/1439)):**
  A user reports that deactivated skills remain callable during dialogue. This touches on the core trust model of the Agent system and represents a significant behavioral bug. Despite high implied severity, the thread has no attached fix PR.

- **Agent Skills UI Confusion ([Issue #1442](netease-youdao/LobsterAI/issues/1442)):**
  The user expresses confusion over the Agent-Skill selection lifecycle: selected skills disappear from the view after a conversation turn. Underlying need: the system lacks clear user feedback on how Agent skills are scoped per session.

### 5. Bugs & Stability

| Severity | Issue | Status | Summary |
|---|---|---|---|
| **Critical** | [#1439](netease-youdao/LobsterAI/issues/1439) | Open (Stale) | Disabled skills are still injected and invoked in conversations. No attached fix. Highest reliability risk. |
| **Moderate** | [#1442](netease-youdao/LobsterAI/issues/1442) | Open (Stale) | Agent skills UI resets after a dialogue turn; user cannot tell if the feature is working correctly. |
| **Moderate** | [#1437](netease-youdao/LobsterAI/issues/1437) | Open (Stale) | Silent failure in task creation UI: "Create Task" button unresponsive with no error feedback. |
| **Resolved** | [#1466](netease-youdao/LobsterAI/pull/1466) | **Fixed** | MCP modal buttons unreachable on tall forms. |
| **Resolved** | [#1467](netease-youdao/LobsterAI/pull/1467) | **Fixed** | macOS shortcuts incorrectly displayed showing `Ctrl`. |

The unresolved #1439 bug remains the highest priority stability threat, as it affects the core behavioral guarantee of the skill management system.

### 6. Feature Requests & Roadmap Signals

The pending queue gives clear direction on where the project is heading:

- **Artifact Preview Pipeline ([PR #1441](netease-youdao/LobsterAI/pull/1441)):**
  This is the heaviest feature PR in the queue. It introduces a plugin-based pipeline to render HTML, React, and Mermaid previews inside Cowork sessions. The PR is a cleaned-up fork of an earlier submission (#1011) with conflicts resolved. Its stalled state since April suggests a pending architectural review.

- **Skill Import Quality Gates ([PR #1445](netease-youdao/LobsterAI/pull/1445)):**
  This PR adds deduplication checks and directory name parsing (from `SKILL.md` frontmatter) to prevent ghost skills from `zip`/`git` imports. This indicates an effort to enforce data integrity at the ingestion layer.

- **OpenClaw Compatibility ([#1443](netease-youdao/LobsterAI/issues/1443)):**
  A recurring compatibility request. A formal stance or migration path is likely needed for the next tagged release.

- **UI Polish ([PR #1440](netease-youdao/LobsterAI/pull/1440)):**
  Moves the active skills badge above the textarea for cleaner layout.

**Prediction:** The next development sprint will likely prioritize the Artifact Pipeline (#1441) and the Skill Import dedup (#1445), followed by a patch release addressing the disabled skills invocation bug (#1439).

### 7. User Feedback Summary

The user base is highly technical and detail-oriented, filing rich bug reports with annotated screenshots (#1437, #1439, #1442). Key takeaways:

- **Pain Points:**
  - **Broken Trust in Skill Logic:** Users expect that disabling a skill guarantees its removal from inference (#1439). This not being the case erodes trust in Agent configuration.
  - **Upgrade Anxiety:** The community is hesitant to upgrade core dependencies like OpenClaw without official compatibility testing (#1443).
  - **Silent Failures:** The lack of error messaging in the task creation flow (#1437) indicates a need for better user feedback patterns in form submissions.

- **Satisfaction:**
  - Users are actively experimenting with deep features (MCP configuration, Agent skills) and filing high-quality bugs, indicating high engagement.
  - The rapid closure of the MCP modal bug (#1466) should positively impact power users who frequently manage complex server configurations.

### 8. Backlog Watch

A significant portion of the repository’s active inventory is at risk of becoming deeply stale. All of the following items were created in early April, were batch-updated on June 13th, but remain open without clear resolution:

| Item | Age | Risk | Status |
|---|---|---|---|
| [#1443](netease-youdao/LobsterAI/issues/1443) OpenClaw Support | ~71 days | Medium | Awaiting roadmap signal |
| [#1439](netease-youdao/LobsterAI/issues/1439) Disabled Skills Callable | ~71 days | **High** | No fix PR identified |
| [#1437](netease-youdao/LobsterAI/issues/1437) Task Creation UI Bug | ~71 days | Low | Lacks maintainer response |
| [#1441](netease-youdao/LobsterAI/pull/1441) Preview Pipeline | ~71 days | High | Major feature blocked |
| [#1445](netease-youdao/LobsterAI/pull/1445) Skill Import Fix | ~71 days | Medium | Foundational quality fix |
| [#1440](netease-youdao/LobsterAI/pull/1440) UI Polish | ~71 days | Low | Low-lift merge |

**Recommendation:** The stale label on these four issues and three PRs requires active triage. A comment from the maintainers outlining the target release version or providing specific blockers for PRs #1441 and #1445 would significantly reduce community ambiguity. The `[stale]` batch update suggests a bot or manual triage pass occurred, but no binding decisions were executed.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest – June 14, 2026**

**Data Snapshot:** 1 open issue, 3 open pull requests, 0 new releases.

---

### 1. Today's Overview

Moltis is experiencing a tightly focused burst of activity today, centered on a single critical bug and supporting infrastructure improvements. The community is rallying around a high-severity OAuth integration failure affecting major MCP servers, with the bug reporter simultaneously providing a targeted fix pull request. No pull requests were merged in the last 24 hours, and no new releases were cut, keeping the current codebase in a state of active review and patching. Overall, the project shows healthy community engagement and rapid response to blocking bugs.

---

### 2. Releases

**None.** No new versions of Moltis were published on June 14, 2026. The latest available binary remains unchanged.

---

### 3. Project Progress

**Merged/Closed PRs today:** 0

Although no code was merged, substantial progress is visible in three open proposals:

- **MCP OAuth Fix (PR #1120):** Authored by **@xzavrel**, this PR directly resolves the `invalid_target` OAuth bug reported in Issue #1119. It modifies `discover_and_register()` to directly fetch the `resource_metadata` URL from the `WWW-Authenticate` header, fixing compatibility with Notion and Linear MCP servers. *Link: [PR #1120](https://github.com/moltis-org/moltis/pull/1120)*

- **Docker Infrastructure Fix (PR #1122):** Submitted by **sayotte**, this removes hardcoded `VOLUME` declarations from the Dockerfile to stop them from shadowing bind-mounted home directories—a known pathological case for container-based deployments. *Link: [PR #1122](https://github.com/moltis-org/moltis/pull/1122)*

- **Dependency Bump (PR #1121):** An automated update from `dependabot[bot]` bumping `esbuild` from v0.25.12 to v0.28.1 for the web UI crate. *Link: [PR #1121](https://github.com/moltis-org/moltis/pull/1121)*

---

### 4. Community Hot Topics

The single most active item today is **Issue #1119**, which has received immediate and decisive community attention.

- **Issue #1119 — [Bug]: MCP OAuth fails with `invalid_target` for servers using `resource_metadata`**
    - *Author:* @xzavrel
    - *Activity:* Opened on June 13 with a follow-up comment on June 14.
    - *Analysis:* This issue represents a critical blocker for daily users of popular MCP services. The underlying need is clear: users require Moltis to strictly comply with the OAuth 2.0 Authorization Server Metadata specification when connecting to well-known integrations. The fact that the reporter immediately followed up with a high-quality fix in PR #1120 suggests a technically sophisticated user base that expects and contributes to protocol-level precision.
    - *Link: [Issue #1119](https://github.com/moltis-org/moltis/issues/1119)*

---

### 5. Bugs & Stability

| Severity | Issue / PR | Description | Status |
|---|---|---|---|
| **High** | [#1119](https://github.com/moltis-org/moltis/issues/1119) | OAuth `invalid_target` failure when MCP servers include `resource_metadata` in the `WWW-Authenticate` header. **Affects:** Notion, Linear. | No user can connect to these servers. **Fix exists** in open PR #1120. |
| **Medium** | Context of [#1122](https://github.com/moltis-org/moltis/pull/1122) | Docker volume declarations shadow the `home` bind mount, causing confusing state in containerized deployments. | Affects users deploying Moltis with Docker who mount their entire home directory. Fix proposed. |

**Risk Assessment:** The OAuth bug is the highest-priority stability issue today. It completely blocks a core feature (connecting to remote MCP servers) for two of the most widely-used providers. The Docker issue is a deployment friction point rather than a runtime crash.

---

### 6. Feature Requests & Roadmap Signals

No explicit new feature requests appear in today's data, but the activity provides strong roadmap signals:

- **Protocol Compliance Push:** The focus on OAuth metadata handling (PR #1120) indicates the team is strengthening core MCP compliance rather than chasing workarounds. Future releases will likely prioritize strict adherence to evolving server specifications.
- **DevOps Maturation:** The Docker volume fix (PR #1122) signals a movement toward making Moltis more reliable in production container environments. This is often a precursor to improved Helm charts or Docker Compose templates in upcoming releases.
- **UI Toolchain Updates:** The automated dependency bump on `esbuild` (PR #1121) shows the web UI is being actively maintained, potentially laying groundwork for UI improvements in the next minor version.

---

### 7. User Feedback Summary

User feedback today is limited but exceptionally high-signal:

- **User Sentiment:** The single user interaction (Issue #1119) represents a highly engaged technical user who is frustrated by a compliance gap, confident enough to diagnose the root cause (`resource_metadata` parameter), and invested enough to write a fix. This suggests a power-user segment for whom stable, spec-compliant MCP connectivity is non-negotiable.
- **Pain Points:**
    - **Connectivity Blockers:** Users cannot connect to services (Notion, Linear) that follow standard OAuth patterns, eroding trust in the connection manager.
    - **Deployment Friction:** The Docker volume issue hints at broader friction for users running Moltis in containerized environments.
- **Satisfaction:** No explicit praise or complaints outside of the bug report.

---

### 8. Backlog Watch

No stale or long-abandoned issues or PRs surfaced in the last 24 hours. All items in today's digest are recent and active. The primary action item for maintainers is the timely review and merge of the following:

1. **PR #1120** ([Link](https://github.com/moltis-org/moltis/pull/1120)) — Holding up the fix for the highest-severity open bug.
2. **PR #1122** ([Link](https://github.com/moltis-org/moltis/pull/1122)) — Resolving a moderate-severity Docker deployment issue.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for **CoPaw (QwenPaw)** based on the provided GitHub data.

---

# CoPaw / QwenPaw Project Digest – 2026-06-14

## 1. Today’s Overview
QwenPaw maintained steady activity with 8 issues and 8 pull requests updated in the last 24 hours. Community participation is robust, particularly from first-time contributors submitting targeted bug fixes and a localization patch. One PR was merged to improve internationalization defaults during agent creation, though no new release was cut. Despite strong contributor throughput, several high-severity bugs remain open without linked fixes, and a queue of submitted patches is waiting on maintainer review, creating a slight bottleneck in the project’s overall stability cadence.

## 2. Releases
**None.** No new releases were published today.

## 3. Project Progress
Only one PR was fully resolved in the reporting window:

- **Merged — [#2498](agentscope-ai/QwenPaw PR #2498):** `fix(agents): use console language when creating agent and fallback unsupported langs` (by Alneys). Fixes a long-standing onboarding quirk where newly created agents always defaulted to English and copied Chinese persona files, ignoring the user’s selected UI language. The patch reads the language preference from localStorage and adds server-side fallback validation, improving the first-run experience for non-English users.

## 4. Community Hot Topics
The most active threads signal clear regional and platform-expansion priorities:

1. **[#5156 – Kimi for Coding Subscription Whitelist](agentscope-ai/QwenPaw Issue #5156)** (4 comments)
   *User Pain Point:* Users with active `kimi-for-coding` subscriptions cannot use their existing paid access through QwenPaw, which only supports standard API keys. The underlying desire is for a flexible “Bring Your Own Premium Token” model or an expandable provider allowlist.

2. **[#5047 – Windows Tauri Desktop Extreme Startup Delay](agentscope-ai/QwenPaw Issue #5047)** (3 comments)
   *User Pain Point:* The migration from Python packaging to Tauri caused startup time to balloon from ~1–2 minutes to over 10 minutes, with frequent “Not Responding” states. This is a *critical UX blocker* for the Windows user base with no communicated fix in progress.

3. **[#5169 / #5175 – Vietnamese Language Support](agentscope-ai/QwenPaw Issue #5169)** + **[PR #5175](agentscope-ai/QwenPaw PR #5175)** (2 comments)
   *Highlight:* A textbook example of efficient community workflow. A feature request for Vietnamese `(vi)` interface support was filed by `biencuong` and immediately implemented via a PR from `nguyenthanhthe`. This strongly signals demand from the Vietnamese market and a healthy localization pipeline.

## 5. Bugs & Stability
Several bugs reported today represent serious reliability risks for active users:

| Severity | Issue | Summary |
|----------|-------|---------|
| **HIGH** | [#5171](agentscope-ai/QwenPaw Issue #5171) | **Context compression can wipe the entire window to 0 tokens** when a persona file exceeds the retention threshold. The agent loses all memory mid-task, forcing a complete restart. No fix PR exists yet. |
| **HIGH** | [#5174](agentscope-ai/QwenPaw Issue #5174) | **Cron/heartbeat agents fail to execute heavy tasks** (`write_file`, `spawn_subagent`). Heartbeat agents do not reliably perform knowledge extraction. This undermines the core promise of autonomous scheduled agents. |
| **HIGH** | [#5047](agentscope-ai/QwenPaw Issue #5047) | **Desktop startup time regression** on Windows (discussed above). |
| **MEDIUM** | [#5172](agentscope-ai/QwenPaw Issue #5172) | **Chat becomes unresponsive after idle timeout.** User must manually stop the request before re-querying. Closed without a linked fix, but the underlying complaint is significant. |
| **LOW–MEDIUM** | [#5035, #5037, #5038, #5040, #5041](PRs) | Five edge-case fix PRs from first-time contributor `ly-wang19` (version parsing, empty jobs file, backup read errors, Linux browser detection, empty message guards) are all **stuck in review**, leaving minor but crash-causing paths unpatched. |

## 6. Feature Requests & Roadmap Signals
- **Strong Signal — Vietnamese (vi) Interface (PR #5175):** Already submitted, almost certainly landing in the next release.
- **Strong Signal — Zalo Bot Channel (Issue #5168):** Directly follows the Vietnam localization push. Likely to be evaluated for the next milestone if the Vietnamese user base continues to grow.
- **Moderate Signal — Kimi Subscription Allowlist (Issue #5156):** A more complex feature requiring changes to the provider/billing layer. May require architectural discussion before it lands.
- **Emerging Pattern:** The community is actively pushing toward **multi-region platform expansion** and **monetization model flexibility**. The i18n + platform expansion (Zalo) trajectory is the clearest roadmap signal this week.

## 7. User Feedback Summary
- **Dissatisfied:** Windows desktop performance is severely degraded post-Tauri migration. Users are struggling with 10+ minute startup times.
- **Dissatisfied:** Core reliability gaps (context wiping, cron task failures) erode trust in using QwenPaw for production or autonomous workflows.
- **Frustrated:** Some bugs (chat freeze, task cancellation) have been reported as long-standing without resolution, generating critical user sentiment.
- **Engaged:** The localization community is very responsive. Vietnamese-language users specifically demonstrated high engagement (request -> PR within ~24 hours).
- **Requested:** Users want better subscription flexibility (Kimi) and expanded platform reach (Zalo).

## 8. Backlog Watch
The following items have been open or under review for a notable period and require maintainer attention:

1. **Pending Review Queue (5 PRs by ly-wang19):** PRs [#5035](agentscope-ai/QwenPaw PR #5035), [#5037](agentscope-ai/QwenPaw PR #5037), [#5038](agentscope-ai/QwenPaw PR #5038), [#5040](agentscope-ai/QwenPaw PR #5040), and [#5041](agentscope-ai/QwenPaw PR #5041) have been submitted since June 9 and tagged “Under Review” without being merged. These are small, isolated crash fixes that would immediately improve stability across config, backup, cron, and context subsystems.

2. **Windows Desktop Performance (Issue #5047):** Open since June 9 with zero maintainer response. This is a critical onboarding blocker for a significant share of the user base.

3. **Context Compression Data Loss (Issue #5171):** Reported today with no maintainer acknowledgment. Given the total data-loss nature of the bug, this should be triaged urgently.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-14

## 1. Today's Overview

ZeroClaw logged a high-activity 24-hour window with over 90 updated issues and pull requests. No releases were cut today, but the project is clearly in a rigorous integration and stability phase, with maintainers converging on major architectural RFCs while simultaneously tackling critical (S1) regressions in the Web UI and macOS client. The volume of work—45 open PRs and 26 active issues—suggests a heavy push toward the v0.8.1 milestone, tracked by the community queue [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970). Long-running feature requests like Dream Mode and the Zerocode TUI continue to attract broad community interest.

---

## 2. Releases

*No new releases tagged today.*

---

## 3. Project Progress

### Merged / Closed PRs & Issues
- **Architecture consolidation:** RFC [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) (Unify the three agent turn engines) was formally closed after being executed via PR [#7540](https://github.com/zeroclaw-labs/zeroclaw/pull/7540), eliminating significant code duplication.
- **Bug fixes closed:**
  - [#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) — `allowed_tools` not restricting MCP tools (documentation gap resolved).
  - [#7507](https://github.com/zeroclaw-labs/zeroclaw/issues/7507) — `quickstart` infinite redraw loop on non-TTY stdin fixed.
  - [#6223](https://github.com/zeroclaw-labs/zeroclaw/issues/6223) — `web_fetch` not working in WhatsApp Web fixed.
  - [#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) / [#7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378) — TUI theme inheritance and keybinding bugs addressed.
  - [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) — Multiple runtime safety issues (closed stale).
  - [#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570) — SQLite memory vector search accelerated via ANN (closed stale).
- **Documentation:** Docker deployment docs iterated ([#6760](https://github.com/zeroclaw-labs/zeroclaw/issues/6760)).

---

## 4. Community Hot Topics

### Highest Engagement Issues
- **[Feature] Dream Mode — Memory Consolidation ([#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)) — 18 comments**
  The most active topic. Users strongly desire autonomous background memory consolidation. The implementation PR [#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) remains open and stalled, signaling a bottleneck the community is eager to see resolved.

- **[RFC] Unify Agent Turn Engines ([#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)) — 5 comments**
  Closed and executed, but the discussion highlighted deep concerns about maintainability of three parallel turn-taking paths.

- **[RFC] Native Dynamic-Library Plugin System ([#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)) — 3 comments**
  A high-risk architectural shift proposing to move beyond WASM-only plugins. The community is closely watching this direction.

### Trending PRs
- **Observability Push:** PR [#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570) (OTel GenAI spans) supersedes the conflict-stalled [#6190](https://github.com/zeroclaw-labs/zeroclaw/pull/6190), showing the team is actively resolving blockages to ship production-grade monitoring.
- **Cross-Profile Delegation ([#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590)):** A direct response to [#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514), this feature unblocks secure multi-agent architectures and is drawing strong interest.

---

## 5. Bugs & Stability

### S1 — Workflow Blocked
| Issue | Component | Status | Fix PR |
|---|---|---|---|
| [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563) — canvas-store regression breaks `/canvas` | Gateway/WS | Open | None listed |
| [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) — `ask_user` fails in WS sessions | Gateway/API | **Active fix** | [#7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588), [#7589](https://github.com/zeroclaw-labs/zeroclaw/pull/7589) |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) — macOS app not working | Tauri/Desktop | Open | None listed |
| [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) — Dashboard not available | Web | Open | — |
| [#7507](https://github.com/zeroclaw-labs/zeroclaw/issues/7507) — Quickstart infinite loop | Config/Onboarding | **Closed/Fixed** | — |

### S2 — Degraded Behavior
- [#7591](https://github.com/zeroclaw-labs/zeroclaw/issues/7591) — Quickstart silently accepts invalid agent aliases, forcing a full restart.
- [#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) — TUI dark themes with light terminal profiles produce unreadable text (**Closed**).

### Stability Patterns
The concentration of S1 bugs in the Gateway/WS layer suggests the new WebSocket chat architecture (from recent `v0.8.x` work) needs hardening. The `ask_user` tool specifically has multiple fixes queued. The macOS Tauri bundle regression is a notable gap with no fix PR yet.

---

## 6. Feature Requests & Roadmap Signals

### Likely for Next Patch / v0.8.1
- **Multi-Session Web Chat ([#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543)):** High-demand UX feature allowing concurrent agent conversations in the browser.
- **`file_read` Charset Detection ([#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521)):** Crucial for non-English users (cp1251, Shift-JIS).
- **llama.cpp Model Router ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)):** Local model switching, a direct frustration for on-premise users.
- **Per-Agent Delegate Roster ([#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514) / [#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590)):** High-value enterprise security feature.

### Medium-to-Long Term
- **Dream Mode ([#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)):** Autonomous memory consolidation is the single most-requested feature by comment volume.
- **Native Plugin System ([#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)):** A fundamental shift from WASM-only to dynamic libraries, pending maintainer review.
- **Zerocode TUI ([#6823](https://github.com/zeroclaw-labs/zeroclaw/issues/6823), [#6825](https://github.com/zeroclaw-labs/zeroclaw/issues/6825), [#6826](https://github.com/zeroclaw-labs/zeroclaw/issues/6826)):** Trackers for a full terminal interface parity with the web dashboard.
- **Streaming Card Messages for Chinese IM ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)):** A clear signal of the project's growing international adoption (QQ, DingTalk, WeChat, Feishu).

---

## 7. User Feedback Summary

### Pain Points
- **Web UI instability:** Users report the dashboard and `/canvas` are regularly broken ([#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523), [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563)).
- **Onboarding friction:** The `quickstart` command has multiple failure modes (non-TTY, invalid aliases) that destroy user configs ([#7507](https://github.com/zeroclaw-labs/zeroclaw/issues/7507), [#7591](https://github.com/zeroclaw-labs/zeroclaw/issues/7591)).
- **macOS app broken:** Users on macOS 15 report the app is completely unusable after install ([#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)).
- **MCP tool confusion:** Users are surprised when `allowed_tools` doesn't filter MCP-provided tools ([#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876)).
- **WhatsApp feature parity:** Lack of reaction acknowledgments compared to Telegram/Discord ([#7518](https://github.com/zeroclaw-labs/zeroclaw/issues/7518)).

### Use Cases & Satisfaction
- Strong demand for autonomous background processing suggests users want "fire-and-forget" agents.
- High interest in multi-agent coordination with strict security boundaries (subagent risk profiles).
- Enthusiastic reception of the Observability/OTel instrumentation push from the power-user community.

---

## 8. Backlog Watch

### Stalled Critical PRs (Needing Author Action)
| PR | Last Update | Risk | Impact |
|---|---|---|---|
| [#5779](https://github.com/zeroclaw-labs/zeroclaw/pull/5779) — TOTP gate for shell tool | Apr 15 | High | Security enhancement blocked |
| [#5892](https://github.com/zeroclaw-labs/zeroclaw/pull/5892) — Three vLLM/tool_choice blockers | Apr 19 | High | Production stability blocked |
| [#6719](https://github.com/zeroclaw-labs/zeroclaw/pull/6719) — `model_switch` persistence across turns | May 16 | High | Agent consistency bug blocked |
| [#6966](https://github.com/zeroclaw-labs/zeroclaw/pull/6966) — OTel prompt capture (superseded by [#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570)) | May 27 | High | Observability gap |

### Long-Standing Items
- **Dream Mode PR ([#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693)):** Massive scope (XL), stalled since May 16, but remains the top community demand.
- **Zerocode TUI Trackers ([#6823](https://github.com/zeroclaw-labs/zeroclaw/issues/6823), [#6825](https://github.com/zeroclaw-labs/zeroclaw/issues/6825), [#6826](https://github.com/zeroclaw-labs/zeroclaw/issues/6826)):** Active but without visible delivery PRs yet; the community is waiting for this substantial effort to land.
- **Node.js LTS stabilization ([#6211](https://github.com/zeroclaw-labs/zeroclaw/issues/6211)):** Open since Apr 29, a simple but impactful CI/infrastructure fix.

### Pending Maintainer Review
- [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) — RFC: Native Dynamic-Library Plugin System
- [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) — RFC: OCI-Compliant Container Registries for WASM Plugins  
  *(These two RFCs represent the future of ZeroClaw's extensibility architecture and are the most consequential items awaiting maintainer direction.)*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*