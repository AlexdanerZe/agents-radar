# OpenClaw Ecosystem Digest 2026-06-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-11 03:38 UTC

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

# OpenClaw Project Digest — 2026-06-11

## 1. Today's Overview

OpenClaw is experiencing extraordinary velocity, with **500 Issues** and **500 Pull Requests** updated in the last 24 hours. Of those PRs, **104 were merged or closed**, indicating a highly active development cycle. The project shipped **v2026.6.6-beta.1**, a sweeping security-boundary release hardening transcripts, sandboxing, MCP, platform integrations, and authentication flows. Despite this rapid iteration, a significant stability deficit persists: multiple P0/P1 "Diamond Lobster" issues continue to dominate discussion around core session management, message routing, and subagent orchestration, suggesting reliability struggles that are outpacing the community's capacity to resolve.

---

## 2. Releases

### OpenClaw v2026.6.6-beta.1 (2026.6.6)

**Focus:** Security boundaries are substantially tighter across the entire stack.

**Key Areas Hardened:**
- Transcripts and sandbox binding
- Host environment inheritance
- MCP stdio boundary enforcement
- Codex HTTP access restrictions
- Native search policy reinforcement
- Elevated sender checks for authentication
- Deleted-agent ACP bypass closure
- Loopback tool restrictions
- Discord moderation and Teams group account controls

**Migration Note:** Operators with custom sandbox, MCP, or environment-sharing configurations should audit their setups, as the new defaults may revoke previously permissive behaviors.

---

## 3. Project Progress

**104 pull requests were merged or closed in the last 24 hours.** Notable advances include:

### Merged/Closed Highlights
- **[#90128](openclaw/openclaw PR #90128):** Critical fix preserving user-initiated `/model` overrides across daily and idle session rollover boundaries (fixes #90119).
- **[#84938](openclaw/openclaw PR #84938):** Forward `reasoning_content` from OpenAI-compatible providers (e.g., MiMo), resolving 400 errors and restoring thinking/chain-of-thought visibility.

### Active High-Impact PRs
- **[#92073](openclaw/openclaw PR #92073):** Handles explicit `NO_REPLY` silent assistant replies, directly addressing the "leaky agent" pattern.
- **[#92021](openclaw/openclaw PR #92021):** Fixes an SSRF/credential-exfiltration vector in cross-origin MCP HTTP redirects.
- **[#90167](openclaw/openclaw PR #90167):** Resolves `${ENV_VAR}` plugin config placeholders for runtime loads.
- **[#91921](openclaw/openclaw PR #91921):** Delivers background exec completion events as `[OpenClaw exec completion]` instead of misclassifying them as heartbeat polls.
- **[#92005](openclaw/openclaw PR #92005):** Adds `force` parameter to browser `click` action to bypass strict Playwright actionability checks on React/Vue/Svelte overlays.
- **[#90110](openclaw/openclaw PR #90110):** Adds native catalog entries for Claude Haiku 4.5.

---

## 4. Community Hot Topics

The community is intensely focused on a cluster of reliability and UX issues. The top three reaction magnets and most-discussed items reveal core tension between advanced features and fundamental robustness.

### Most Discussed Issues (by Comment Count)

| Issue | Title | Comments | Severity |
|-------|-------|----------|----------|
| [#25592](openclaw/openclaw Issue #25592) | Text between tool calls leaks to messaging channels | 31 | 🦞 P1 |
| [#44925](openclaw/openclaw Issue #44925) | Subagent completion silently lost — no retry, no notification | 19 | 🦞 P1 |
| [#88838](openclaw/openclaw Issue #88838) | Core session/transcript SQLite migration via accessor seam | 19 | 🦞 P0 |
| [#32473](openclaw/openclaw Issue #32473) | Control UI requires device identity (HTTPS/localhost) | 17 | 🦞 P2 |
| [#22438](openclaw/openclaw Issue #22438) | Tiered bootstrap file loading for progressive context control (Feature) | 17 | 🦞 P2 |
| [#32296](openclaw/openclaw Issue #32296) | Agent replies to previous message instead of current (context confusion) | 15 | 🐚 P1 |
| [#58450](openclaw/openclaw Issue #58450) | Agent promises follow-up without starting any background action | 15 | 🐚 P2 |

### Top Community Reactions (👍)

| Issue | Feature/Request | 👍 |
|-------|-----------------|----|
| [#18160](openclaw/openclaw Issue #18160) | Direct Exec Mode for Cron Jobs (avoid LLM for predictable script runs) | 10 |
| [#39604](openclaw/openclaw Issue #39604) | Opt-in `tools.web.fetch.allowPrivateNetwork` for private network access | 9 |
| [#79077](openclaw/openclaw Issue #79077) | Telegram bot-to-bot and guest-bot modes (May 2026 platform release) | 7 |
| [#37634](openclaw/openclaw Issue #37634) | Keep `workspaceAccess: none` sandbox workspaces writable rather than read-only | 6 |
| [#29387](openclaw/openclaw Issue #29387) | Bootstrap files in `agentDir` silently ignored; only workspace loads | 5 |

### Signal Analysis
The "leaky agent" pattern (#25592, #44905, #32296) dominates community frustration. Users find internal processing output, tool-call JSON, and `NO_REPLY` tokens appearing in user-facing channels (Slack, Discord, iMessage) to be the platform's most damaging UX flaw. The sheer volume of discussion and the number of linked, open fix PRs suggest this is the single highest-stakes issue family currently open.

---

## 5. Bugs & Stability

### P0 Critical — Core Platform Risk
- **[#88838](openclaw/openclaw Issue #88838) — SQLite Migration (P0):** The core session/transcript runtime-state migration is being tracked via branch-by-abstraction to avoid a high-risk monolithic rewrite. A maintainer-led effort.

### P1 Diamond Lobster — Reliability / Data Loss
- **[#25592](openclaw/openclaw Issue #25592) — Text leaks between tool calls:** Top UX bug. Loosely coupled to [#92073](openclaw/openclaw PR #92073) (silent reply handling).
- **[#44925](openclaw/openclaw Issue #44925) — Subagent results silently lost:** Multiple failure modes (completion announce, timeout). **No fix PR yet** despite high severity.
- **[#40001](openclaw/openclaw Issue #40001) — Write tool lacks append mode:** Data loss in shared/cron workspaces. **Stale, needs review.**
- **[#43661](openclaw/openclaw Issue #43661) — Session hangs on compaction timeout:** Triggers duplicate message resends in a silent failure loop.
- **[#31583](openclaw/openclaw Issue #31583) — `exec` tool ignores `skills.entries.*.env`:** Regression breaking secret injection for subprocesses.
- **[#32296](openclaw/openclaw Issue #32296) — Session context confusion:** Agent responds to previous message instead of current.

### P1 Diamond Lobster — Security
- **[#45740](openclaw/openclaw Issue #45740) — gh-issues skill prompt injection:** Untrusted issue/review bodies injected directly into sub-agent prompts. Needs security review.
- **[#29387](openclaw/openclaw Issue #29387) — AgentDir bootstrap silently ignored:** Fix shape clear; awaiting product and security sign-off.
- **[#31331](openclaw/openclaw Issue #31331) — Docker Sandbox workspace binding fails:** Internal vs. host path mismatch.

### P2 Widespread Platform Issues
- **Control UI Collapse:** Multiple users report avatar/image loading failures ([#38439](openclaw/openclaw Issue #38439), [#41201](openclaw/openclaw Issue #41201)) and HTTPS/localhost lockout on VPS ([#32473](openclaw/openclaw Issue #32473)).
- **Platform Integration Regressions:**
    - [#41744](openclaw/openclaw Issue #41744): Feishu image tool loses media before final delivery.
    - [#44905](openclaw/openclaw Issue #44905): Discord leaks internal JSON/NO_REPLY artifacts.
    - [#41165](openclaw/openclaw Issue #41165): Telegram DMs still pollute `agent:main:main` session despite prior fix.
- **Provider-Specific Behavior:**
    - [#44845](openclaw/openclaw Issue #44845): Volcengine token usage shows 0/200k.
    - [#38327](openclaw/openclaw Issue #38327): Google Vertex/Gemini `null/undefined` crash.
    - [#85888](openclaw/openclaw Issue #85888): MiniMax 503 overloads during specific cron windows.

---

## 6. Feature Requests & Roadmap Signals

### Strongest Community Demand
1. **Direct Exec Mode for Cron** ([#18160](openclaw/openclaw Issue #18160), 👍10) — Move away from LLM-mediated cron to direct script execution for reliability.
2. **Private Network Access for Fetch** ([#39604](openclaw/openclaw Issue #39604), 👍9) — Enterprise/developer opt-in for internal/localhost HTTP resources.
3. **Telegram Guest-Bot / Bot-to-Bot** ([#79077](openclaw/openclaw Issue #79077), 👍7) — New Telegram platform feature integration.

### Architecture & Governance Signals
- **Tiered Bootstrap Loading** ([#22438](openclaw/openclaw Issue #22438)): Smart context window management for large workspaces. A well-scoped community design.
- **Per-Skill Model Routing** ([#43260](openclaw/openclaw Issue #43260)): Fine-grained model selection at the skill level.
- **Per-Agent Cost Budgets** ([#42475](openclaw/openclaw Issue #42475)): Gateway-level daily/monthly caps for operators.
- **Multi-Agent Blackboard & Capability Profiling** ([#35203](openclaw/openclaw Issue #35203)): Shared context and token cost governance for multi-agent orchestration.

### Prediction for Next Release Cycle
The **leaky agent problem** (#25592, #44905) is the single most impactful UX issue and will almost certainly see direct remediation in the next release, especially given active fix PRs already in flight. The **Direct Exec Mode for Cron** (#18160) has strong community demand and a clear implementation path, making it a strong candidate for `v2026.6.13`. Security-hardening follow-ups from today's release will continue.

---

## 7. User Feedback Summary

### High Satisfaction Drivers
- **Breadth of Integrations:** Users are actively deploying OpenClaw across Discord, Telegram, Feishu, Slack, Teams, and custom HTTP surfaces.
- **Agentic Power:** The community is pushing the platform into production-grade multi-agent orchestration, embedded cron workflows, and sandboxed coding.
- **Velocity:** Users appreciate rapid iteration and high issue/PR throughput.

### Major Pain Points
1. **The Leaky Agent:** The #1 community grievance. Internal LLM output, tool-call JSON, and `NO_REPLY` tokens appearing in public/messaging channels is viewed as a fundamental UX failure that undermines professional deployment.
2. **Silent Failures:** Subagents, cron jobs, and session timers failing without error notifications creates a trust deficit for automated background work.
3. **Configuration Fragility:** Several well-documented features silently do not work for subsets of users (agentDir bootstrap, skill env variable inheritance, avatar loading, WebSocket URL editing clearing tokens).
4. **UI Regression Strain:** The Control UI is described as broken by multiple users (missing avatars, HTTPS lockout, missing images)—reducing confidence in the platform's frontend.

### Operator Voice
Power users and administrators are requesting better observability (dedicated health channels, cost dashboards, token usage transparency) and governance (cost budgets, RWX permission schemes, backup exclusions). This signals growing enterprise production usage.

---

## 8. Backlog Watch

A significant number of high-severity, well-scoped issues are blocked by maintainer or product decision bandwidth, representing the project's single greatest scaling risk.

| Issue | Title | Status | Wait Duration |
|-------|-------|--------|---------------|
| [#29387](openclaw/openclaw Issue #29387) | AgentDir bootstrap silently ignored (P1, Security) | `needs-maintainer-review`, `needs-product-decision`, `fix-shape-clear` | Since Feb 28 |
| [#31583](openclaw/openclaw Issue #31583) | Exec tool ignores skill env vars (P1, Regression) | `needs-maintainer-review`, `fix-shape-clear` | Since Mar 2 |
| [#32473](openclaw/openclaw Issue #32473) | Control UI HTTPS lockout on VPS (P2, High 👍) | `needs-maintainer-review`, `needs-product-decision` | Since Mar 3 |
| [#45740](openclaw/openclaw Issue #45740) | gh-issues untrusted body injection (P2, Security) | `needs-security-review`, `source-repro` | Since Mar 14 |
| [#22438](openclaw/openclaw Issue #22438) | Tiered bootstrap loading (P2, Feature) | `needs-product-decision` | Since Feb 21 |
| [#18160](openclaw/openclaw Issue #18160) | Direct Exec Mode for Cron (P2, 👍10) | `needs-maintainer-review`, `needs-product-decision` | Since Feb 16 |
| [#40001](openclaw/openclaw Issue #40001) | Write tool lacks append mode (P1, Data Loss) | `needs-product-decision`, **stale** | Since Mar 8 |
| [#16670](openclaw/openclaw Issue #16670) | Onboarding should include Memory/Embedding setup (P2) | `needs-maintainer-review`, `needs-product-decision` | Since Feb 15 |

### Systemic Observation
The heavy `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` tag coverage across the top active issues indicates that **maintainer bandwidth is the primary throttling bottleneck** for the project. The community is producing well-formed, `fix-shape-clear` bugs and well-scoped feature requests faster than the core team can effectively triage. This is a critical health indicator as the project scales. If this triage debt is not addressed, it risks contributor disillusionment and stagnation of high-value fixes.

---

## Cross-Ecosystem Comparison

## Cross-Project Ecosystem Comparison Report — 2026-06-11

### 1. Ecosystem Overview

The open-source personal AI assistant landscape is undergoing explosive growth, but mounting strain around core reliability threatens to outpace the benefits of feature velocity. While a dozen-plus projects iterate rapidly, they converge on a set of unresolved architectural challenges: session integrity, sub-agent orchestration, context pollution, and security boundary enforcement. The community voice is shifting decisively from “can it do this?” to “will it do this reliably, every time, without leaking internal state?”. Developers who invest in reliability infrastructure, observability, and hardened security defaults will differentiate most effectively as the market matures toward production deployment.

---

### 2. Activity Comparison (24h)

| Project | Issues Updated | PRs Updated | Merged/Closed PRs | Release Status | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 104 | v2026.6.6-beta.1 | Frenetic / Maintainer strain |
| **CoPaw** | 33 | 49 | 30 | v1.1.11.post1 (hotfix) | High velocity / Strained release trust |
| **ZeroClaw** | 43 | 50 | 10 | None | High velocity / Stability push |
| **Hermes** | 50 | 50 | 11 | None | Stabilization-heavy |
| **IronClaw** | 50 | 50 | 22 | Blocked (crates.io gap) | High velocity / Release friction |
| **NanoBot** | 11 | 33 | 19 | None | Healthy / Robust contributor trust |
| **LobsterAI** | 0 | 25 | 24 | v2026.6.10 | Excellent / Clean backlog |
| **PicoClaw** | 5 | 15 | 6 | v0.2.9-nightly | Healthy / Rapid security response |
| **NanoClaw** | 2 | 12 | 4 | None | Robust / Ecosystem building |
| **NullClaw** | 0 | 4 | 0 | None | Steady / Quality focused |
| *TinyClaw* | 0 | 0 | 0 | None | Dormant |
| *Moltis* | 0 | 0 | 0 | None | Dormant |
| *ZeptoClaw* | 0 | 0 | 0 | None | Dormant |

---

### 3. OpenClaw’s Position

OpenClaw remains the ecosystem’s cornerstone reference platform, absorbing the highest integration complexity and security research burden. Its massive community (500+ issues/PRs daily) drives the deepest provider/integration matrix, making it the primary testbed for fundamental AI agent problems.

**Advantages vs. peers:**
- Broadest integration library and community contribution base.
- Strongest default security posture (sandbox binding, MCP enforcement, environment hardening).
- Acts as the innovation core; most protocol experimentation (MCP, A2A) originates here.

**Technical approach differences:**
- Security-first design from inception, where peers often retroactively patch.
- Maximum configurability (often at the cost of UX simplicity).
- Heavy emphasis on multi-agent and single-tenant infrastructure over lightweight desktops.

**Community size comparison:**
- OpenClaw’s 24h activity (500/500) dwarfs the next tier (~50/50). However, this scale is a double-edged sword. The P0/P1 “Diamond Lobster” backlog is growing, and the universally cited **leaky agent problem** (e.g., #25592, #44925) remains an open wound affecting all downstream projects.
- **Relation to peers:** NanoClaw, PicoClaw, and ZeroClaw operate as specialized derivatives, inheriting OpenClaw’s core architectural challenges while trying to insulate themselves from its instability by narrowing scope.

---

### 4. Shared Technical Focus Areas

Analysis of cross-project bug reports reveals universal pressure points:

| Focus Area | Affected Projects | Specific Example Issues |
|---|---|---|
| **Session/Context Integrity** | OpenClaw, NanoBot, Hermes, ZeroClaw | Context pollution (#4259 NanoBot), session compaction (#88838 OpenClaw), message loss (#6034 ZeroClaw), skipped turns (#24187 Hermes) |
| **Background Automation Reliability** | OpenClaw, NanoBot, CoPaw, ZeroClaw | Cron/agent-created tasks failing silently (#4290 NanoBot, #5064 CoPaw), subagent completion lost (#44925 OpenClaw) |
| **Security Boundary Enforcement** | OpenClaw, PicoClaw, NanoClaw, Hermes | SSRF bypasses (#3077 PicoClaw, #92021 OpenClaw), egress lockdown regressions (#2731 NanoClaw), redaction corrupting output (#33801 Hermes) |
| **Provider/API Resilience** | OpenClaw, NanoBot, Hermes, CoPaw | Empty API choices not triggering fallback (#4287 NanoBot), argument corruption (#5052 CoPaw), model param missing (#43899 Hermes) |
| **Cross-Platform Fragility** | Hermes, PicoClaw, CoPaw, LobsterAI, ZeroClaw | Mac launchd crashes (#43475 Hermes), Windows NSIS corruption (#2142 LobsterAI), 74 test failures on Windows (#7462 ZeroClaw), OpenSSL Windows regression (#5086 CoPaw) |

---

### 5. Differentiation Analysis

| Project | Strategic Focus | Target User | Architecture Bett |
|---|---|---|---|
| **OpenClaw** | Full-stack security reference | Devs/ops embracing complexity for max flexibility | Protocol-first (MCP/A2A), strict isolation |
| **LobsterAI / CoPaw** | Product-centric desktop automation | End-users on desktop (Win/Mac) | Desktop native (Computer Use, scheduler), corporate backing |
| **Hermes / NanoBot** | Reliability & UX polish | Power users wanting stable workflows | Rapid triage cycles, strong contributor trust |
| **IronClaw** | Performance correctness | Rust/WASM enterprise segment | “Reborn” architecture, formal trace commons |
| **PicoClaw / NanoClaw / ZeroClaw** | Niche platform optimization | Embedded, container, i18n communities | Fork-and-simplify of OpenClaw core |
| **NullClaw** | Focused minimalism | Stable API / infra operators | Extremely low churn, deliberate scope |

---

### 6. Community Momentum & Maturity

**Tier 1 — Frenetic / Operational Strain**
- **OpenClaw**, **ZeroClaw**: Highest absolute activity, but scalability bottlenecks in maintainer bandwidth and increasing quality debt. Community outpacing capacity.

**Tier 2 — High Velocity / Architecture Transition**
- **CoPaw**, **IronClaw**: Deep engineering investment in major rewrites (Runtime 2.0, Reborn). Short-term stability pain for long-term architectural bets.

**Tier 3 — Stabilizing / Production Maturation**
- **NanoBot**, **Hermes Agent**, **LobsterAI**: Healthiest merge cadence. Strong contributor trust, robust triage, low recidivism on fixed bugs. Safest bets for deployment today.

**Tier 4 — Steady / Focused**
- **PicoClaw**, **NanoClaw**, **NullClaw**: Low noise, high quality. Efficiently serving niche user bases without systemic friction.

**Tier 5 — Dormant**
- **TinyClaw**, **Moltis**, **ZeptoClaw**: Zero activity. No current competitive signal.

---

### 7. Trend Signals (Value for AI Agent Developers)

**1. The “Leaky Agent” is the #1 UX Anti-Pattern**
Internal tool call JSON, `NO_REPLY` tokens, and agent planning text escaping to user channels is uniformly reported as the most damaging bug across OpenClaw, Hermes, and NanoClaw. **Action:** Invest in strict output filtering, response templating, and explicit response attribution. Clean agents command a premium.

**2. Multi-Agent is the New Multi-Threading**
Sub-agent context pollution, silent completion loss, and failure to cascade are the hardest unsolved problems. Every major project hitting this wall confirms it is not a feature gap but a fundamental architectural challenge. **Action:** Standardized inter-agent protocols (MCP, A2A) are prerequisites for enterprise trust. Invest in the orchestration layer’s observability and fault isolation.

**3. Desktop Parity is a Hard Requirement**
Fragile desktop experiences (Windows NSIS, macOS launchd, OpenSSL regressions) consume a disproportionate share of engineering cycles. **Action:** Desktop parity testing must be a core CI gate, not an afterthought. If full parity is impossible, optimize for one platform or go web-first.

**4. Security Must Be Structural, Not Band-Aided**
SSRF, redaction, and egress bypasses recur across projects. **Action:** Design sandbox, network, and file system boundaries into the core architecture from day one. The audit-driven hardening cycle is a cost multiplier.

**5. Direct Execution Kills Prompting Overhead**
Strong demand for “Direct Exec Cron Mode” (#18160 OpenClaw) signals a market for **predictable automation** that does not rely on LLM mediation for every background task. **Action:** Hybrid architectures—LLM for planning, deterministic code for execution, cron for scheduling—represent the highest ROI pattern.

**6. Globalization is an Unlocked Need**
ZeroClaw’s massive i18n push exposes a large underserved market. **Action:** Localizing UI *and* interaction channels (Telegram, Feishu, WeChat) is a documented growth vector for global adoption.

**7. Reliability Beats Raw Features**
Users voting with bug reports and reactions consistently prioritize “works every time” over “supports the latest model”. **Action:** Allocate engineering budget to observability, health checks, and deterministic core behaviors before chasing downstream provider cutting-edge capabilities.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 11, 2026, based on the provided GitHub activity data.

---

## NanoBot Project Digest — 2026-06-11

### 1. Today's Overview
The NanoBot project exhibited a remarkably high level of activity on June 10–11, 2026, with **33 pull requests** and **11 issues** updated in the last 24 hours. The core team and community contributors merged 19 PRs and closed 7 issues, demonstrating a strong push toward stability and feature maturity. Activity was concentrated on fixing subagent workflow failures, resolving context memory pollution, improving provider resilience, and expanding the WebUI feature set. No new official releases were published, but the heavy volume of high-quality merging strongly signals an imminent significant point release.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
The project advanced across multiple critical subsystems today:

- **Memory & Context Integrity:** A major fix was merged to scope `# Recent History` prompt injection by session (HKUDS/nanobot#4274), directly closing a critical context pollution bug (HKUDS/nanobot#4259). The idle session compact logic was hardened to prevent information loss (HKUDS/nanobot#4270). The WebUI transcript system was overhauled with segmented storage (HKUDS/nanobot#4278) and auto-compaction on file size limits (HKUDS/nanobot#4247), solving the issue of disappearing chat history.
- **Provider & Fallback Logic:** Stream stalls are now properly retried and trigger fallback models (HKUDS/nanobot#4272), and the handling of empty API choices was fixed to trigger fallbacks (HKUDS/nanobot#4288).
- **Tool Execution:** The `exec` tool gained a `pathPrepend` configuration (HKUDS/nanobot#4273), finally resolving the long-standing community issue of `pip install` failing within scripts (HKUDS/nanobot#3934).
- **Configuration & Channels:** The agent now fails fast with helpful errors on invalid config files (HKUDS/nanobot#4275). The Feishu (Lark) channel SDK is now lazily loaded to prevent startup crashes (HKUDS/nanobot#4277).
- **Transcription:** Two new ASR providers were added: SiliconFlow (HKUDS/nanobot#4281) and StepFun (HKUDS/nanobot#4000).

### 4. Community Hot Topics
Discussion this week centered on reliability in complex workflows and context fidelity.

- **Context Pollution & Memory Fidelity (HKUDS/nanobot#4259, ·HKUDS/nanobot#4280):** The discovery that `history.jsonl` was cross-polluting context between sessions generated the most technically deep discussion. The user provided a detailed data-flow analysis, which the maintainers swiftly resolved via session-scoping in HKUDS/nanobot#4274.
- **Cron + Subagent Breakage (HKUDS/nanobot#4290):** A clear bug report highlighted that cron jobs silently abort when subagents are spawned. The reporter also submitted a fix PR (HKUDS/nanobot#4293), demonstrating a skilled and engaged user base.
- **Empty Response Non-Fallback (HKUDS/nanobot#4287):** A user identified that DeepSeek returning empty `choices` at peak hours was silently breaking their workflow. A fix PR (HKUDS/nanobot#4288) was opened simultaneously.
- **Reliability of Long-Term Goals (HKUDS/nanobot#4286):** A user reported the agent repeatedly failing to recall its assigned "sustained goal." This underscores the community's growing reliance on NanoBot for complex, multi-step autonomous tasks.

### 5. Bugs & Stability
Bugs reported today ranged from critical workflow breakers to minor parameter issues. Severity is assessed by user impact.

- **Critical: Cron Workflow Termination (HKUDS/nanobot#4290):** Spawning a subagent in a cron job terminates the main agent immediately upon subagent completion, failing the workflow. *Fix exists in HKUDS/nanobot#4293.*
- **Critical: Fallback Logic Gap (HKUDS/nanobot#4287):** The system fails to fall back to alternative models when the primary API returns a success status but empty `choices`. *Fix exists in HKUDS/nanobot#4288.*
- **High: Context Loss (HKUDS/nanobot#4286):** User reports the agent losing track of its primary sustained goal mid-task.
- **High: Context Pollution (HKUDS/nanobot#4259):** History entries leaking across sessions. *Resolved by HKUDS/nanobot#4274.*
- **Medium: Sandbox HOME Variable (HKUDS/nanobot#4237):** `bwrap` sandbox does not reset `$HOME`, causing tool writes to fail. *Resolved.*
- **Medium: WebUI Transcript Loss (HKUDS/nanobot#4247):** Chat history disappearing when transcript JSONL hits the size limit. *Resolved by segmented storage (HKUDS/nanobot#4278).*
- **Low: API Parameter Mismatch (HKUDS/nanobot#4261):** GPT-5.x expecting `max_completion_tokens` over `max_tokens` in custom providers. *Resolved.*

### 6. Feature Requests & Roadmap Signals
Several user-driven feature requests moved from proposal to implementation today, signaling the project's roadmap direction:

- **Subagent Model Presets (HKUDS/nanobot#4291):** A new PR allows subagents to run with different model configurations specified by the LLM, enabling powerful delegation hierarchies. This is a major step toward distributed agentic workflows.
- **Slack Granular Scoping (HKUDS/nanobot#4289):** Request for a `groupRequireMention` mode to complement existing allowlists.
- **WebUI Feature Parity (HKUDS/nanobot#4282, ·HKUDS/nanobot#4284):** Users are actively driving the WebUI beyond a simple chat interface, implementing in-browser file managers and slash-palette skill activation. This points to a "Web-first" future trajectory.
- **Aggregated Subagent Notifications (HKUDS/nanobot#4279):** A sophisticated proposal to batch subagent results to reduce LLM hallucination due to interleaved streaming.

**Prediction:** The next version will likely focus heavily on **Subagent flexibility and stability** (HKUDS/nanobot#4291, HKUDS/nanobot#4293, HKUDS/nanobot#4279), **Provider resilience** (HKUDS/nanobot#4288), and **WebUI maturation** (HKUDS/nanobot#4282).

### 7. User Feedback Summary
- **Pain Points:** The dominant sentiment revolves around **agentic reliability at scale**. Users are frustrated when agents lose track of long-term goals (HKUDS/nanobot#4286), fail to gracefully recover from transient API errors (HKUDS/nanobot#4287), or abort scheduled workflows without warning (HKUDS/nanobot#4290). A secondary theme was configuration friction, notably the missing version display (HKUDS/nanobot#4233) and silent config failures.
- **Satisfaction:** The community is highly engaged and technically proficient. Users are not just filing bug reports—they are contributing deep code-level analysis (HKUDS/nanobot#4259) and opening fix PRs alongside their bug reports (HKUDS/nanobot#4290, HKUDS/nanobot#4288). The maintainers' rapid triage (closing issues like the `pip install` blocker HKUDS/nanobot#3934 in under three weeks) is fostering strong contributor trust.

### 8. Backlog Watch
Given the project’s exceptionally high activity level, there are no truly "cold" or neglected issues. However, the following recently opened items would benefit from maintainer triage or review:

- **HKUDS/nanobot#4286 – Sustained Goal Context Loss:** Currently without a maintainer comment. This is a high-severity UX issue that requires reproduction steps or a suggested workaround.
- **HKUDS/nanobot#4257 – Fenced Code Block Splitting:** This PR has been open for several days. It fixes a visual bug where long messages break code fences. A review or merge would close a known UI rendering rough edge.
- **HKUDS/nanobot#4279 – Aggregated Subagent Notifications:** This feature request proposes a significant architectural change to the `SubagentManager`. An initial response from the maintainers acknowledging the design trade-offs could guide future community contributions.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-11

## 1. Today's Overview

Hermes Agent is experiencing an exceptionally high-activity cycle, with **100 combined issue and PR updates** logged in the last 24 hours (50 issues, 50 PRs). The open/active bug count sits at 42, and 39 PRs remain open—indicating a healthy but strained development pipeline racing to keep pace with community discoveries. Activity is concentrated around **P1 configuration and lifecycle bugs** (cron model handling, macOS launchd stability, session persistence) alongside a wave of **provider-specific rough edges** (Ollama, Bedrock, Gemma 4). The maintainer response is urgent: several critical bugs received fix PRs within hours of reporting. The project is clearly iterating fast, expanding platform support, but is currently in a **stabilization-heavy phase** as users push deployments into production-like environments (Docker, macOS services, multi-profile setups).

## 2. Releases

*No new releases were published in the last 24 hours.*

---

## 3. Project Progress

**11 PRs were merged/closed**, advancing several subsystems:

- **Session & Startup Reliability:**
  - **PR #18922** (NeloReis) — Fixed a **P1** issue where dirty gateway shutdowns (crash, drain timeout) would hard-suspend sessions instead of resuming them, preventing history loss on Telegram/messaging platforms.
  
- **Skills System:**
  - **PR #18897** (SimbaKingjoe) — `_find_skill` now excludes `.archive`, `.git`, `.github`, `.hub` directories, matching the filtering in `iter_skill_index_files`.
  - **PR #18901** (shellybotmoyer) — `skill_view` now falls back to frontmatter `name` lookup, resolving the agent tool-calling loop where discovered skills were unreachable.
  - **PR #43808** (teknium1) — Dashboard can now manage skills and toolsets for *any* profile, not just the active one.

- **Model & Provider Config:**
  - **PR #18889** (liuhao1024) — Fixed modality detection on Xiaomi models where `attachment: true` conflicted with `modalities.input`.
  - **PR #18877** (rkt2spc) — Custom provider `context_length` overrides are now passed through auxiliary compression and fallback paths.

- **UI/UX:**
  - **PR #18903** (rahulraikwar00) — Added a copy button with visual feedback to skill install commands in the website UI.
  - **PR #43582** (xxxigm) — New `display.terminal_code_blocks` toggle for compact terminal previews on markdown-capable platforms.
  - **PR #43602** (donovan-yohan) — Clarified Baoyu image generation documentation.

---

## 4. Community Hot Topics

The most active discussions reveal deep user investment in specific deployment configurations and accessibility:

- **[Issue #23402] Docker permissions with Dashboard chat** (15 comments, 3 👍)
  *Author: mmartial* — A detailed integration thread about Unraid Docker templates where UID/GID handling (`HERMES_UID`) breaks the dashboard chat. The discussion reflects a strong user base deploying Hermes in homelab/production Docker environments and finding permission boundary bugs.

- **[Issue #26689] VoiceOver accessibility improvements** (9 comments)
  *Author: xiaopinpin-music* — A comprehensive, well-researched accessibility audit from a blind macOS user. Covers specific screen reader barriers (unlabeled UI elements, dynamic content noise, modal traps). Signals an underserved but passionate user segment that could differentiate Hermes in the AI agent space.

- **[Issue #33801] Secret redaction corrupts syntax** (5 comments)
  *Author: koishi70* — Alarming report where the `security.redact_secrets` system corrupts Python/Shell tool output *before* execution. High community concern as it directly breaks code generation and terminal workflows.

- **[Issue #40239] Portuguese (pt-BR) localization** (4 comments, 2 👍)
  *Author: alexander-stack1* — Points out that the backend ships extensive pt-BR translations (`locales/pt.yaml`) but the desktop app lacks the UI selector to enable them. Clear demand for completing the localization pipeline.

---

## 5. Bugs & Stability

**P1 (Critical):**
- **[Issue #43899] Cron jobs fail with 'Model parameter is required'** — Jobs without an explicit `model` field fail silently even when `config.yaml` has a valid default. **Fix PR #43952 and revert PR #43956 opened same day.**
- **[Issue #24187] SessionDB silently skips current turn** — `_repair_message_sequence` shortens the message list, but `_flush_messages_to_session_db` uses the stale conversation length as an offset, losing the current turn entirely.
- **[Issue #43842] macOS self-update kills the CLI** — `launchctl bootout` triggered from within the gateway (via `terminal` tool) unloads the service before the CLI can complete; `KeepAlive` treats clean exit as success and never revives the service.

**P2 (High Impact):**
- **[Issue #43915] Bedrock streaming faults abort turns** — AWS `internalServerException` is not retried mid-turn, aborting long-running subagent tasks on transient failures.
- **[Issue #43666] Redaction gaps at persistence boundary** — Security audit follow-up (#43083) finds 23 plaintext password hits in `state.db` after a single session. Tool file dumps, compaction blocks, and DB URIs are unredacted.
- **[Issue #43835] Telegram double messages** — Tool output code blocks and response body are sent as separate messages, appearing as duplicates to users.
- **[Issue #43475] launchd-managed gateway bricks on macOS** — `/restart` exits 0, but `KeepAlive.SuccessfulExit=false` interprets clean exit as failure to revive. Service requires manual intervention.

**P3 (Notable):**
- **[Issue #43900] Ollama context cap** — Local models silently run at Ollama's default 4096-token context; `num_ctx` from GGUF metadata is read but never applied to the API call.
- **[Issue #43944] TTS cuts off content** — Speech buffer resets mid-message, losing content after code blocks in Desktop voice mode.
- **[Issue #43558] MemoryProvider return value discarded** — `on_pre_compress()` is implemented as a statement instead of an assignment, nullifying the return.

---

## 6. Feature Requests & Roadmap Signals

Several features in-flight or requested point to the next version's priorities:

- **Follow-up Question Suggestions (PR #43507, liuhao1024)** — Active PR adding a configurable `display.followup_suggestions` feature that appends 2–5 contextual queries to assistant responses (Claude.ai-style). Strong candidate for the next release.
- **Audio Transcription API (PR #43411, zhang-perry)** — Adds `POST /api/audio/transcribe` to the gateway API server, expanding OpenAI API parity. Signals roadmap intent to be a standalone API platform.
- **Desktop Polish Sprint:** Multiple PRs this cycle target Desktop stability — composer drafts per session (PR #43939), auto-scroll fixes (Issue #43865), `/goal` feedback (Issue #43476). A desktop-focused patch release is imminent.
- **Accessibility Overhaul (Issue #26689)** — Though no maintainer has picked it up yet, the detailed audit provides a ready-made implementation roadmap. Likely a candidate for a community contribution or a dedicated sprint.
- **i18n Completion (Issue #40239)** — Community is noticing the backend/frontend localization gap. Completing the UI language selector is a low-effort, high-impact win.

---

## 7. User Feedback Summary

**Common Pain Points:**

- **Configuration Fragmentation:** Users deploying multi-profile setups (Issue #25290) or Docker (Issue #23402) repeatedly hit permission boundaries and missed config inheritance. The cron profile fragmentation fix and revert PR (#43956) indicate maintainers recognize this architectural debt.
- **Provider Rough Edges:** Every major provider integration (Ollama #43900, Bedrock #43915, Gemma 4 #6626, Xiaomi #18889) has presented unique silent failure modes. Users perceive Hermes as "almost working" with their preferred model.
- **Security vs. Functionality Conflict:** The secret redaction system is actively breaking code execution workflows (#33801) while simultaneously leaking secrets in other paths (#43666). This is eroding trust in a core safety feature.
- **macOS Service Instability:** Two P1 bugs (#43475, #43842) within 24 hours around launchd lifecycle management. Mac users are a vocal segment, and service reliability is their primary gating factor for production use.

**Expressed User Needs:**

- Reliable Docker/Unraid deployment for home lab setups.
- Full accessibility compliance for screen reader users.
- Stable, predictable cron job execution.
- Consistent multi-platform bot behavior (Telegram/WeChat/Discord).

---

## 8. Backlog Watch

The following high-value issues and requests remain unresolved and lack visible maintainer traction:

- **[Issue #6626] Gemma 4 tool calling support** — Created April 9, 2026 (63 days open). 3 👍, 5 comments. A configuration-level blocker for users running `google/gemma-4-E4B-it` via vLLM. Despite being a flagship model, no fix PR has materialized.
- **[Issue #17198] Weixin token conflict on gateway restart** — Created April 29, 2026 (43 days open). A race condition where old and new gateway processes fight over the WeChat bot token, hard-blocking restart for WeCom users.
- **[Issue #26689] Accessibility for VoiceOver users** — The most detailed feature request in the tracker (9 comments, extremely high quality). No assignee, no milestone. Risk of losing a dedicated accessibility advocate if left unattended.
- **[Issue #40239] Portuguese (pt-BR) desktop support** — Clear, implementable request backed by existing translation files. No maintainer response yet. Low-hanging fruit that signals community responsiveness.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-11

## 1. Today's Overview

The PicoClaw project is maintaining a high development velocity, with 5 issues and 15 pull requests updated in the last 24 hours. The project is in a healthy state, merging 6 PRs while keeping 9 open for active review. The nightly release cadence remains consistent, and the development focus is clearly split between urgent bug fixing (Windows compatibility, SSRF security) and proactive codebase hardening (unchecked type assertions across multiple modules). The rapid turnaround on a reported SSRF bypass vulnerability demonstrates a mature security response pipeline.

## 2. Releases

**One new build was published today:**

- **Nightly Build `v0.2.9-nightly.20260611.d955d5bb`**
  An automated nightly build tracking the `main` branch. This build is labeled as potentially unstable and is intended for early testing. The full diff against the last stable tag (`v0.2.9`) is available in the [changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main).

*No stable release with migration notes or breaking changes was issued today.*

## 3. Project Progress

**Six pull requests were merged or closed in the last 24 hours, representing significant strides in security, compatibility, and tooling:**

- **Security Hardening:** [#3085](https://github.com/sipeed/picoclaw/pull/3085) patches a critical SSRF bypass in the `web_fetch` tool by blocking the `198.18.0.0/15` benchmark address range (RFC 2544), closing issue [#3077](https://github.com/sipeed/picoclaw/issues/3077).
- **Windows Compatibility:** [#3089](https://github.com/sipeed/picoclaw/pull/3089) resolves a long-standing bug ([#2472](https://github.com/sipeed/picoclaw/issues/2472)) where filesystem tools returned "invalid argument" on Windows due to path separator mismatches with `os.Root`.
- **Error Handling:** [#3043](https://github.com/sipeed/picoclaw/pull/3043) adds proper error checking for `strconv.Atoi` and `json.Unmarshal` calls that were silently discarding failures.
- **API Compatibility:** [#2951](https://github.com/sipeed/picoclaw/pull/2951) fixes HTTP 400 errors with OpenAI-compatible endpoints by switching `web_search` from `web_search_preview` to the standard `function` type. [#2948](https://github.com/sipeed/picoclaw/pull/2948) fixes HTTP 400 errors with `claude-opus-4-7` models by skipping the deprecated `temperature` parameter.
- **Developer Tooling:** [#2945](https://github.com/sipeed/picoclaw/pull/2945) introduces `picoclaw-tracer`, a standalone web UI for real-time inspection of LLM traces.

## 4. Community Hot Topics

- **Most Discussed Issue:** [#2472 "list_dir returns invalid argument on Windows"](https://github.com/sipeed/picoclaw/issues/2472) — 5 comments, 1 reaction. This veteran thread (open since April) represents a sustained frustration point for the Windows user base. The resolution via [#3089](https://github.com/sipeed/picoclaw/pull/3089) today should be a welcome relief.
- **Critical Bug (New):** [#3094 "异步子代理完成任务时ForUser字段导致重复消息"](https://github.com/sipeed/picoclaw/issues/3094) — Opened yesterday, this issue has zero comments but signals an immediate UX regression for users relying on async `spawn` sub-agents, who receive duplicate messages on pushed channels.
- **Security Disclosure:** [#3077 "SSRF Restriction Bypass"](https://github.com/sipeed/picoclaw/issues/3077) — While closed, this is the highest-signal interaction of the period. Researcher *YLChen-007* responsibly disclosed a verified bypass, and the project patched it within 24 hours.

## 5. Bugs & Stability

**Critical (Resolved):**
- **SSRF Restriction Bypass** ([#3077](https://github.com/sipeed/picoclaw/issues/3077)) — Patched by [#3085](https://github.com/sipeed/picoclaw/pull/3085). The `198.18.0.0/15` range is now properly blocked.
- **Windows Filesystem Tools** ([#2472](https://github.com/sipeed/picoclaw/issues/2472)) — Patched by [#3089](https://github.com/sipeed/picoclaw/pull/3089). Path separator normalization for Windows.

**High (Open):**
- **Duplicate Async Sub-agent Messages** ([#3094](https://github.com/sipeed/picoclaw/issues/3094)) — Newly reported. No fix PR. High-impact UX bug for multi-agent workflows.
- **Panel Broken on iOS < 16.4** ([#3090](https://github.com/sipeed/picoclaw/issues/3090)) — Web panel fails on older iOS Safari. Affects mobile access.

**Medium (Fix PRs Active):**
- **Unchecked Type Assertions (Sweep):** Contributor *chengzhichao-xydt* is systematically fixing unrecoverable panics across the codebase: `CreateHTTPClient` ([#3095](https://github.com/sipeed/picoclaw/pull/3095)), `native_search` ([#3091](https://github.com/sipeed/picoclaw/pull/3091)), `skills_install` ([#3092](https://github.com/sipeed/picoclaw/pull/3092)), and `evolution/store` ([#3053](https://github.com/sipeed/picoclaw/pull/3053)).
- **DM Scope Config Not Persisting** ([#3067](https://github.com/sipeed/picoclaw/pull/3067)) — Fix ready for review.
- **Exec Safety False Positive** ([#3087](https://github.com/sipeed/picoclaw/pull/3087)) — Fix ready for review.

## 6. Feature Requests & Roadmap Signals

- **New Messaging Gateways:** Issue [#3093](https://github.com/sipeed/picoclaw/issues/3093) explicitly requests **SimpleX** and **Tox** backends. This signals growing user interest in privacy-preserving, P2P communication protocols as native gateways.
- **Agent Collaboration (Stale):** PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) introduces a first-class Agent Collaboration Bus with per-agent mailboxes and structured envelopes. Open since May 24 with no recent activity, this is a large feature at risk of drifting out of sync with `main`.
- **Deployment Hardening:** PR [#3083](https://github.com/sipeed/picoclaw/pull/3083) adds configurable localhost bypass logic and trusted proxy CIDRs for the launcher. Points to roadmap focus on enterprise/production deployment scenarios.
- **Matrix Identity Parsing:** PR [#3045](https://github.com/sipeed/picoclaw/pull/3045) fixes `allow_from` filtering for standard Matrix user IDs (`@user:domain.com`).

## 7. User Feedback Summary

**Satisfaction Drivers:**
- **Rapid Patching:** The 24-hour turnaround on the SSRF bypass ([#3077](https://github.com/sipeed/picoclaw/issues/3077) → [#3085](https://github.com/sipeed/picoclaw/pull/3085)) is a strong trust signal.
- **Proactive Stability:** The systematic type assertion fixes from community contributors show that code quality is valued by the developer base.

**Pain Points:**
- **Windows Ecosystem:** The two-month lifespan of [#2472](https://github.com/sipeed/picoclaw/issues/2472) suggests Windows is under-tested in the CI pipeline.
- **User Experience Friction:** Duplicate messages from async agents ([#3094](https://github.com/sipeed/picoclaw/issues/3094)) and a broken mobile panel ([#3090](https://github.com/sipeed/picoclaw/issues/3090)) are creating immediate friction for end users.
- **Feature Gaps:** Users are pushing for more diverse communication backends (SimpleX, Tox).

## 8. Backlog Watch

- **⚠️ [PR #2937 Agent Collaboration Bus](https://github.com/sipeed/picoclaw/pull/2937)** — Stale since 2026-05-24. A massive architectural change with no recent maintainer activity. High risk of merge conflicts if it falls much further behind `main`.
- **⚠️ [PR #3045 Matrix ID Parsing](https://github.com/sipeed/picoclaw/pull/3045)** — Open since 2026-06-07. This breaks `allow_from` filters for the Matrix gateway, a core integration. A seemingly straightforward fix waiting for review.
- **⚠️ [PR #3067 DM Scope Persistence](https://github.com/sipeed/picoclaw/pull/3067)** — Open since 2026-06-09. The frontend sends the setting, but the backend silently drops it, meaning users cannot save a critical session configuration option.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-06-11

### 1. Today's Overview
Activity was robust, driven by critical bug fixes and the expansion of the skill ecosystem. The project saw **12 Pull Requests** and **2 Issues** updated in the last 24 hours, with no new formal releases tagged. Work was concentrated on container networking (egress lockdown hardening), production deployment configuration, and documenting the community skills model. The health of the contributor base is strong, with users consistently pairing bug reports with corresponding fix PRs and introducing polished new feature skills.

### 2. Releases
No new releases were published on this date. The project remains in active development toward an unspecified next patch.

### 3. Project Progress
Four PRs were merged or closed today:

- **[#2719 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2719):** Introduces an official `uninstall.sh` script with confirmation, dry-run, and OneCLI agent cleanup — a direct improvement to the developer on-boarding/off-boarding experience.
- **[#2721 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2721):** Finalizes three public documentation pieces (`customizing.md`, the skills model, and skill guidelines), formalizing the contractual basis for community contributions.
- **[#3 (Closed)](https://github.com/nanocoai/nanoclaw/pull/3):** A long-running security infrastructure PR since February has been concluded. It enforces **per-group IPC namespaces**, validating identity via directory ownership rather than self-reported data to prevent privilege escalation between agent groups.
- **[#2724 (Closed)](https://github.com/nanocoai/nanoclaw/pull/2724):** Opened against the wrong base repository and immediately closed.

### 4. Community Hot Topics
The most active discussion continues around the **Multi-Runtime Agent SDK Abstraction**:

- **[Issue #1690](https://github.com/nanocoai/nanoclaw/issues/1690)** (6 comments, 3 reactions): Author `chiptoe-svg` proposes a pattern allowing Claude, Codex, and local models to operate as modular skills. The sustained engagement reflects strong latent demand for model-agnostic runtimes and vendor flexibility.

**Ecosystem momentum:** A wave of skill submissions (Guardrails [#2726](https://github.com/nanocoai/nanoclaw/pull/2726), Web Search [#2725](https://github.com/nanocoai/nanoclaw/pull/2725), Tool Visibility [#2211](https://github.com/nanocoai/nanoclaw/pull/2211)) validates that the community is actively building on the published skills model.

### 5. Bugs & Stability
Two high-severity infrastructure bugs were reported today, alongside integration failures:

- **[Critical] Egress Lockdown Regression ([#2731](https://github.com/nanocoai/nanoclaw/issues/2731)):** Setting `NANOCLAW_EGRESS_LOCKDOWN=true` breaks access to `host.docker.internal`, blocking agents from reaching host-local services (e.g., Ollama, proxy bridges, local databases). *No fix PR exists yet; this is a major regression for local-model and hybrid deployments.*
- **[Critical] Configuration Loading Failure ([#2730](https://github.com/nanocoai/nanoclaw/pull/2730)):** `NANOCLAW_*` variables in `.env` do not reach `process.env` under `launchd/systemd`. The egress module and other runtime controllers fail silently in production environments. *Fix PR submitted by the reporter.*
- **[High] Telegram `wire-to` Intent Broken ([#2728](https://github.com/nanocoai/nanoclaw/pull/2728)):** Pairing reports success but never creates the `messaging_group_agents` database row, leaving the pairing invisible to the interceptor. *Fix PR submitted.*
- **[Medium] Telegram Documentation Discrepancy ([#2729](https://github.com/nanocoai/nanoclaw/pull/2729)):** Setup documentation references status block names that the code never emits, confusing new users. *Fix PR submitted.*

### 6. Feature Requests & Roadmap Signals
Several major signals indicate the direction of upcoming releases:

- **Multi-Runtime Support ([#1690](https://github.com/nanocoai/nanoclaw/issues/1690)):** The highest-engagement feature proposal. Likely to influence architecture planning for a v2.x milestone, though its scope makes an immediate landing unlikely.
- **New Skills Ecosystem:** The `/add-guardrails` ([#2726](https://github.com/nanocoai/nanoclaw/pull/2726)) skill for input/output filtering and `/add-web-search-plus` ([#2725](https://github.com/nanocoai/nanoclaw/pull/2725)) are polished and structurally consistent with the project guidelines — both are strong candidates for the next release cycle.
- **Operational Observability ([#2727](https://github.com/nanocoai/nanoclaw/pull/2727)):** Agent container stdout/stderr persistence to disk. This sibling PR to a Microsoft fork directly addresses a common debugging pain point and is highly likely to land in the next patch.
- **Standardization:** With the skills documentation contract finalized ([#2721](https://github.com/nanocoai/nanoclaw/pull/2721)), the next minor release is expected to focus on formalizing and documenting the contributed skill layer.

### 7. User Feedback Summary
Sentiment is characterized by high technical engagement paired with specific operational friction:

- **Pain Points:**
    - **Local networking blocked:** Users running hybrid setups (host LLMs, bridge proxies) are directly impacted by the egress lockdown regression ([#2731](https://github.com/nanocoai/nanoclaw/issues/2731)).
    - **Production config silent failure:** Security variables set in `.env` are unreliable in managed environments ([#2730](https://github.com/nanocoai/nanoclaw/pull/2730)).
    - **Integration trust eroding:** The Telegram `wire-to` bug ([#2728](https://github.com/nanocoai/nanoclaw/pull/2728)) silently breaks pairing, undermining confidence in the setup wizard.
    - **Debugging opacity:** The lack of persistent container logs ([#2727](https://github.com/nanocoai/nanoclaw/pull/2727)) remains a recurring operational gap for power users.
- **Satisfaction / Health:**
    - **High agency contributions:** Users consistently submit fix PRs alongside bug reports, indicating a healthy, invested developer base.
    - **Skills model traction:** The volume of upstreamed skills validates the project's extensibility strategy as a genuine community asset.

### 8. Backlog Watch
Three items require maintainer attention to prevent contributor stagnation:

- **[Issue #1690](https://github.com/nanocoai/nanoclaw/issues/1690) (Multi-Runtime SDK):** Open since April 7 — over two months without a formal roadmap response despite being the highest-engagement issue. Acknowledgment from maintainers would prevent community uncertainty.
- **[PR #2211](https://github.com/nanocoai/nanoclaw/pull/2211) (Tool Visibility Skill):** Open since May 3. This is a polished skill providing live tool-call previews that has been reworked to conform to the skills model. Five weeks without review risks contributor burnout.
- **[PR #2611](https://github.com/nanocoai/nanoclaw/pull/2611) (Preserve Caller Context):** Open since May 25. A security fix for the approval-gating system that preserves original caller context when replaying commands. The prolonged open state represents a potential security context escalation risk.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the project digest generated from the provided GitHub data snapshot.

---

### NullClaw Project Digest — 2026-06-11

#### 1. Today’s Overview
Based strictly on the provided 24-hour window, the NullClaw project exhibits a quiet issue tracker paired with deliberate, community-driven pull request activity. No new releases were published, and the issue queue is entirely empty (zero open or updated issues). Four pull requests were actively cycled by three different contributors, all opened and updated on June 10th. While no code was merged, the activity focuses squarely on hardening infrastructure, fixing subtle runtime bugs, and improving user configuration—indicating a stable project pulse focused on quality over raw feature velocity.

#### 2. Releases
None. No releases were published in this window, and no new versions are available for upgrade.

#### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The following open PRs represent the full breadth of active work:

- **Agent Runner Error Handling** ([PR #951](nullclaw/nullclaw PR #951)): Prevents agent initialization noise from leaking into user-facing channels on failure.
- **Configurable Queue Mode** ([PR #949](nullclaw/nullclaw PR #949)): Introduces a `default_queue_mode` field to `config.json` and moves the `QueueMode` enum to the canonical `config_types.zig`.
- **Cron Delivery Attribution** ([PR #948](nullclaw/nullclaw PR #948)): Fixes origin metadata propagation so `agent_start` is correctly attributed to the delivery channel/account in cron workflows.
- **Gateway Resource Cleanup** ([PR #950](nullclaw/nullclaw PR #950)): Moves port probing earlier in gateway startup to prevent resource leaks in test environments when the port is in use.

#### 4. Community Hot Topics
No comments or reactions were recorded on any issue or pull request in the data. Despite this, the four open PRs form the core of current community contribution. The underlying needs revealed by these PRs are:

- **Reliability at Scale**: Two of the four PRs (#951 and #950) deal directly with failures—leaking internal state on child process crashes and failing cleanly on port conflicts. This signals that real-world deployment stress is surfacing edge cases.
- **Configuration & DevOps Ease** ([PR #949](nullclaw/nullclaw PR #949)): The move to make `queue_mode` configurable from `config.json` without editing Zig source code is a strong signal that operators want to manage this setting declaratively.
- **Job Scheduling Fidelity** ([PR #948](nullclaw/nullclaw PR #948)): Fixing cron attribution shows that the scheduling feature is seeing active use, and proper channel/account wiring is a high priority for users.

#### 5. Bugs & Stability
No bugs were filed as Issues today. Inline bug fixes delivered via PRs cover the following, ranked by severity:

- **Medium — Fake Agent Responses on Crash** ([PR #951](nullclaw/nullclaw PR #951)): When an agent child process exits non-zero, `buildAgentOutput` fallback posts initialization logs (memory plans, MCP registration) to channels as if they were agent answers. Fix PR exists, unmerged.
- **Low — Test Infrastructure Resource Leak** ([PR #950](nullclaw/nullclaw PR #950)): Gateway tests fail to clean up allocated resources (`Config`, `SessionManager`, tools) when a port conflict is detected. Fix PR exists, unmerged.
- **Low — Missing Cron Origin Metadata** ([PR #948](nullclaw/nullclaw PR #948)): Spawned `nullclaw agent` subprocesses from cron lose delivery channel/account attribution, breaking downstream routing. Fix PR exists, unmerged.

All three fix PRs are authored and open but require review and merge.

#### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed as Issues. The PRs, however, signal several roadmap directions:

- **Declarative Agent Configuration** ([PR #949](nullclaw/nullclaw PR #949)): Standardizing the `queue_mode` option in `config.json` suggests the team is moving toward richer, user-facing configuration without requiring source code changes. This could extend to other agent tuning knobs in the next release.
- **Improved Cron & Channel Attribution** ([PR #948](nullclaw/nullclaw PR #948)): The involvement of local storage and gateway `/cron/add` payloads in the fix hints at a maturing cron subsystem built for multi-account, routable delivery.
- **Test Durability** ([PR #950](nullclaw/nullclaw PR #950)): The effort to clean up the gateway test suite seems preparatory for future gateway features, ensuring the test harness is resilient before adding new networking or allocation logic.

#### 7. User Feedback Summary
No direct user issues were filed. Indirect feedback inferred from the submitted PRs includes:

- **Pain Point — Channel Spam on Error**: Users experience noisy, confusing messages from failed agents ([PR #951](nullclaw/nullclaw PR #951)).
- **Pain Point — Configuration Rigidity**: Users or operators had to modify Zig code to change queuing behavior, a significant barrier ([PR #949](nullclaw/nullclaw PR #949)).
- **Pain Point — Broken Cron Routing**: Scheduled agent runs arrive in the wrong channel or without proper account attribution, breaking automation workflows ([PR #948](nullclaw/nullclaw PR #948)).
- **Satisfaction Signal**: The fact that community members (vernonstinebaker, DonPrus, addadi) are diagnosing and writing the fixes themselves indicates a healthy, engaged contributor base.

#### 8. Backlog Watch
The NullClaw issue tracker is currently empty. There are zero long-unanswered Issues or unattended PRs in this data window. The four open PRs are all recent (updated June 10th) and show no signs of stalling. If there are design discussions or roadblocks, they are happening outside of the Issues/PRs comment threads in this snapshot.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for June 11, 2026.

---

### Project Digest: IronClaw (nearai/ironclaw)
**Date:** 2026-06-11

### 1. Today's Overview
The IronClaw project is in a period of high-velocity stabilization for its "Reborn" architecture. In the past 24 hours, **50 issues** and **50 PRs** were updated, with **22 PRs merged or closed**, demonstrating intense focus on squashing regressions, fixing authentication flows, and polishing the WebUI v2 experience. Activity is overwhelmingly centered on improving the first-run user experience and extending the platform's tool and automation delivery capabilities. Despite the heavy development churn, no new releases were published to crates.io, leaving downstream consumers blocked on critical dependency updates.

### 2. Releases
**No new versions were published today.**
A release PR ([#3708](https://github.com/nearai/ironclaw/pull/3708)) proposing `ironclaw-v0.29.1` along with breaking changes to `ironclaw_common` and `ironclaw_skills` remains open. The unresolved crates.io publishing gap ([#3259](https://github.com/nearai/ironclaw/issues/3259)) continues to prevent the community from accessing versions `0.25.0` through `0.27.0`, an issue made more urgent by the security context of `wasmtime` CVEs driving the need for newer versions.

### 3. Project Progress
The project merged 22 pull requests today, advancing multiple critical workstreams:
- **Reborn Auth & Identity**: Merged [#4746](https://github.com/nearai/ironclaw/pull/4746) (Auth-gate resume re-dispatches original capability calls after OAuth completion). Merged [#4742](https://github.com/nearai/ironclaw/pull/4742) (Manual token credential selection now flows through the entire runtime). Merged [#4585](https://github.com/nearai/ironclaw/pull/4585) and [#4603](https://github.com/nearai/ironclaw/pull/4603) (Tenant identity bound to auth evidence).
- **UX & UI**: Merged [#4717](https://github.com/nearai/ironclaw/pull/4717) (Restored the "Always Allow" affordance in WebUI v2 gate prompts). Merged [#4734](https://github.com/nearai/ironclaw/pull/4734) (Agent avatar now shows the correct icon instead of "IC" initials).
- **Integrations & Fixes**: Merged [#4642](https://github.com/nearai/ironclaw/pull/4642) (Strict-mode provider tool call rejection fixed). Merged [#4743](https://github.com/nearai/ironclaw/pull/4743) (NEAR/Anthropic context length overflow correctly classified). Merged [#4730](https://github.com/nearai/ironclaw/pull/4730) (End-to-end personal Slack DM delivery for triggered events). Merged [#4739](https://github.com/nearai/ironclaw/pull/4739) (Slack enabled for QA Railway).
- **Docs & DevEx**: Merged [#4652](https://github.com/nearai/ironclaw/pull/4652) (Comprehensive Reborn testing walkthrough and launcher script).

### 4. Community Hot Topics
- **crates.io Publishing Bottleneck ([#3259](https://github.com/nearai/ironclaw/issues/3259))**: With 14 comments, this remains the highest-signal community issue. The need is clear: downstream packagers cannot upgrade due to a gap in the publishing pipeline. The underlying need is **reliable software supply chain access**, exacerbated by security pressure.
- **Reborn First-Run Friction**: A cluster of issues filed by *sunglow666* and *think-in-universe* highlights extreme friction in the initial setup, specifically around NEAR AI provider configuration ([#4703](https://github.com/nearai/ironclaw/issues/4703)) and SSO login for local builds ([#4729](https://github.com/nearai/ironclaw/issues/4729)). The community is actively trying to test the Reborn stack but hitting fundamental onboarding walls.
- **Configuration-as-Code Vision ([#3036](https://github.com/nearai/ironclaw/issues/3036))**: This epic continues to receive engagement (6 comments). The appeal for declarative, auditable tenant blueprints signals strong demand from the enterprise/operations segment, though it remains in the concept stage.

### 5. Bugs & Stability
Bug reports are elevated as the Reborn stack undergoes community beta testing.

- **Critical (Core Setup & Auth Broken)**:
    - **#4703**: [NEAR AI provider passes connection test but fails to be used in conversations.](https://github.com/nearai/ironclaw/issues/4703)
    - **#4729**: [NEAR AI SSO login rejects local frontend_callback origins, blocking local dev.](https://github.com/nearai/ironclaw/issues/4729)
    - **#4741**: [Corrupt secret key file crashes server with an opaque "Invalid master key" error.](https://github.com/nearai/ironclaw/issues/4741)
    - *Note*: A large fix PR ([#4731](https://github.com/nearai/ironclaw/pull/4731)) is actively open to address #4703 and related issues.

- **High (Functional Regressions)**:
    - **#4704**: [`builtin.http` approval loop enters an infinite failure cycle without actionable error details.](https://github.com/nearai/ironclaw/issues/4704)
    - **#4740**: [Slack tool's parameter schema is mostly untyped, causing model failures.](https://github.com/nearai/ironclaw/issues/4740)
    - **#4706**: [All authorization flows fail to recover after cancellation or failure.](https://github.com/nearai/ironclaw/issues/4706)
    - **#4683**: [Invalid model configuration yields a misleading "driver unavailable" error.](https://github.com/nearai/ironclaw/issues/4683)

- **Medium (UI Polish)**:
    - Issues such as drafts being lost ([#4724](https://github.com/nearai/ironclaw/issues/4724)), composer interactivity during generation ([#4725](https://github.com/nearai/ironclaw/issues/4725)), missing syntax highlighting ([#4708](https://github.com/nearai/ironclaw/issues/4708)), small fonts ([#4707](https://github.com/nearai/ironclaw/issues/4707)), and broken link navigation ([#4733](https://github.com/nearai/ironclaw/issues/4733)) indicate the WebUI needs significant QA passes alongside the feature work.

### 6. Feature Requests & Roadmap Signals
- **Trace Commons Onboarding ([PR #4559](https://github.com/nearai/ironclaw/pull/4559))**: An innovative agent-driven invite link flow for Trace Commons onboarding is under development, moving beyond CLI-based setup.
- **Programmatic MCP Management ([PR #4735](https://github.com/nearai/ironclaw/pull/4735))**: Support for `PATCH` updates on MCP server configurations points to a more flexible, API-driven extension ecosystem.
- **Cron Timezone Awareness ([PR #4749](https://github.com/nearai/ironclaw/pull/4749))**: Mandating IANA timezones for cron triggers addresses a core user complaint about automation predictability across time zones.
- **Attachment Web UX ([PR #4738](https://github.com/nearai/ironclaw/pull/4738))**: Wiring the front-end attachment upload flow is the final piece of the rich content puzzle.
- **Prediction**: The next release (likely v0.29+ once the crates.io issue is resolved) will prioritize the **Reborn WebUI v2 stabilization** and the **Tool/Extension API maturity**.

### 7. User Feedback Summary
The dominant user sentiment is a mix of **eagerness to adopt the Reborn stack and frustration with its fragile setup process**.
- **Pain Points**: Configuration persistence, authentication round-trips, and opaque error handling are the top blockers. Users like *think-in-universe* are filing detailed "Local Testing Findings" ([#4692](https://github.com/nearai/ironclaw/issues/4692)) that systematically document these barriers.
- **Use Cases**: Local development and testing is the primary driver of current feedback, alongside evaluation of the Reborn WebUI for personal assistant use cases.
- **Satisfaction Signals**: The extremely high quality and volume of bug reports (authored by community members with reproduction steps, screenshots, and expected behavior) indicates a deeply engaged and technically proficient community that is invested in the product's success. The responsiveness of the core team (merging 22 PRs today) suggests the feedback loop is tight.

### 8. Backlog Watch
- **[Issue #3259](https://github.com/nearai/ironclaw/issues/3259) (Publishing Gap)**: **Highest Priority.** Opened 2026-05-05. This issue has the most comments and a clear security driver. It acts as a blocker for the entire Rust downstream ecosystem. Urgent maintainer action is required.
- **[PR #3708](https://github.com/nearai/ironclaw/pull/3708) (Release PR)**: Open since 2026-05-16. Stale PRs requiring release coordination are a classic sign of release pipeline friction.
- **[Issue #3036](https://github.com/nearai/ironclaw/issues/3036) (Config-as-Code Epic)**: Opened 2026-04-28. This large epic has not seen direct child issues or PRs recently. Without active breakdown into tasks, it risks losing momentum despite initial enthusiasm.
- **[PR #4499](https://github.com/nearai/ironclaw/pull/4499) (Dependabot Tokio bump)**: Routine dependency bump that has been open since June 5. Prolonged open Dependabot PRs can lead to maintaining outdated transitive dependencies.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for June 11, 2026, generated from the provided GitHub activity data.

---

## LobsterAI Project Digest — 2026-06-11

### 1. Today’s Overview
LobsterAI saw intense activity on June 11, with **25 pull requests updated** in the last 24 hours (24 merged/closed, 1 open) and zero new issues filed, signaling excellent maintainer throughput and a quiet bug queue. The latest release, **2026.6.10**, went out yesterday, and a major feature—**Computer Use MVP**—was merged today alongside critical Windows installer and update fixes. The project’s focus remains on agent reliability, cross-platform polish, and sweeping the contribution backlog.

### 2. Releases
- **2026.6.10** (released June 10): Highlights include data backup and restore ([PR #2125](https://github.com/netease-youdao/LobsterAI/pull/2125)), a local callback login flow ([PR #2122](https://github.com/netease-youdao/LobsterAI/pull/2122)), and surfacing native OpenClaw compaction settings for user control. No breaking changes or special migration steps were noted.
- The batch of PRs merged today (#2141–#2145) are emergency fixes and feature additions that appear targeted at the **next patch release**, addressing a Windows NSIS regression, auth URL migration, and the new Computer Use runtime.

### 3. Project Progress (Merged/Closed PRs Today)
Several high-impact features and fixes were integrated from both new submissions and the stale-PR backlog:

- **Computer Use MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)): Windows x64 built-in Computer Use kit with an MCP server bridge, runtime installer, and lifecycle wiring for app/window management.
- **Context Continuity** ([PR #2145](https://github.com/netease-youdao/LobsterAI/pull/2145)): Improves Cowork agent reliability after OpenClaw compaction by adding diagnostics, session-scoped task state, and a lightweight workspace layer.
- **Core Fixes**:
  - NSIS destructive init fix + engine loading page redesign ([PR #2142](https://github.com/netease-youdao/LobsterAI/pull/2142))
  - Windows in-app update fix ([PR #2141](https://github.com/netease-youdao/LobsterAI/pull/2141))
  - Portal fallback URL migration ([PR #2144](https://github.com/netease-youdao/LobsterAI/pull/2144))
- **Backlog Cleanup**: A large batch of April-era PRs were finally merged, including:
  - Disabled skills enforcement ([PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501))
  - Scheduled task “Test Task” button and macOS notification channel ([PR #1486](https://github.com/netease-youdao/LobsterAI/pull/1486), [PR #1489](https://github.com/netease-youdao/LobsterAI/pull/1489))
  - Session pruning to prevent context overflows ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499))
  - Native close-button behavior on Windows ([PR #1497](https://github.com/netease-youdao/LobsterAI/pull/1497))
  - Rich-text Markdown editor for Agent guide files ([PR #1503](https://github.com/netease-youdao/LobsterAI/pull/1503))

### 4. Community Hot Topics
No new Issues were filed in the past 24 hours, indicating either a low bug volume or that prior concerns were addressed.

The most notable community-facing PR remains **the open dependency update**:
- **[#1277 — Bump Electron from 40.2.1 to 42.3.3](https://github.com/netease-youdao/LobsterAI/pull/1277)**: Open since April 2 but updated yesterday (June 10). This massive version jump suggests the team is carefully evaluating compatibility before merging; it is maintained by `dependabot` but heavily watched by the community.
- **Computer Use MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) is the day’s headline feature and aligns with strong community demand for on-device agentic control.

### 5. Bugs & Stability
*Ranked by severity:*

- **Critical (Fixed):** [PR #2142](https://github.com/netease-youdao/LobsterAI/pull/2142) — NSIS destructive initialization on Windows. This was a high-risk installer bug that could corrupt existing installations. Fixed and engine loading page redesigned.
- **High (Fixed):**
  - [PR #2141](https://github.com/netease-youdao/LobsterAI/pull/2141) — Windows in-app update broken.
  - [PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485) / [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501) — Disabled skills still remained in `activeSkillIds` and were injected into Cowork prompts.
- **Medium (Fixed):** [PR #2144](https://github.com/netease-youdao/LobsterAI/pull/2144) — Auth portal fallback URLs pointed to outdated domains.
- **Low (Fixed):** [PR #1490](https://github.com/netease-youdao/LobsterAI/pull/1490) — Scheduled task delivery channel did not update correctly after editing.

### 6. Feature Requests & Roadmap Signals
- **Computer Use is now a shipped MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)). This moves LobsterAI decisively into the agentic desktop-automation space, giving it a differentiation edge over pure chat agents.
- **Cowork session pruning** ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499)) and **post-compaction context continuity** ([PR #2145](https://github.com/netease-youdao/LobsterAI/pull/2145)) show the roadmap is prioritizing **reliable long-running agents** — a direct answer to a universal user pain point.
- **Scheduled Tasks** have been rounded out with test buttons, macOS notifications, and delivery channel fixes, suggesting this feature is approaching full maturity.
- **Windows UX parity** ([PR #1497](https://github.com/netease-youdao/LobsterAI/pull/1497)) adds configurable close-button behavior, a frequent request from Windows power users.

### 7. User Feedback Summary
Inferred from the issues and PRs addressed today, real user pain points include:

- *“My long Cowork session breaks the model due to context limits”* → Addressed by session pruning [#1499](https://github.com/netease-youdao/LobsterAI/pull/1499) and context continuity [#2145](https://github.com/netease-youdao/LobsterAI/pull/2145).
- *“I disabled a skill but the agent still uses it”* → Fixed in [#1485](https://github.com/netease-youdao/LobsterAI/pull/1485) / [#1501](https://github.com/netease-youdao/LobsterAI/pull/1501).
- *“Editing agent instructions in plain text is painful”* → Solved by the new Markdown editor [#1503](https://github.com/netease-youdao/LobsterAI/pull/1503).
- *“I can’t test a scheduled task without saving and leaving the form”* → Workflow friction resolved by the “Test Task” button [#1486](https://github.com/netease-youdao/LobsterAI/pull/1486).
- *“Windows close button behavior is confusing”* → Configurable exit/minimize logic added in [#1497](https://github.com/netease-youdao/LobsterAI/pull/1497).

Satisfaction indicators: the team is listening closely and delivering fixes at a high velocity, keeping the issue tracker near zero.

### 8. Backlog Watch
- **[#1277 — Bump Electron](https://github.com/netease-youdao/LobsterAI/pull/1277)** remains the single longest-open PR in the top 20 (since April 2). Its June 10 update suggests active review. A major version shift (40→42) carries risk of API breaks and regressions, so careful monitoring is warranted.
- **Positive trend:** The maintainers merged approximately 10 stale PRs from April 2026 today, demonstrating a strong effort to clear technical debt and respect community contributions. The backlog is now very clean.

---
*Digest generated from GitHub data provided for netease-youdao/LobsterAI.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the CoPaw (QwenPaw) project digest for June 11, 2026.

---

## CoPaw Project Digest – 2026-06-11

### 1. Today's Overview
CoPaw (QwenPaw) is in a period of extremely high velocity, driven by the **v1.1.11 release** and a surge of community contributions. The last 24 hours saw **49 PRs** and **33 Issues** updated, reflecting intense development activity. However, the release cycle was immediately disrupted by a **critical OpenSSL regression** on the Windows Desktop client, forcing an urgent hotfix (v1.1.11.post1). While major architectural initiatives like **Runtime 2.0** are moving forward, the spike in stability issues highlights friction between adding new capabilities and maintaining platform robustness. Overall, the project remains highly engaged and generative, but user trust in release stability is being tested.

### 2. Releases
- **v1.1.11** (2026-06-10): Core features include **Free Model OAuth** for zero-config provider setup and a built-in **Xiaomi MiMo Token Plan** provider.
- **v1.1.11-beta.3** (2026-06-10): Pre-release iteration focusing on self-evolving skill creation flows.
- **v1.1.11.post1** (2026-06-11): **Emergency hotfix** to resolve the OpenSSL 3.5 regression that blocked Windows Desktop startup. Windows Desktop users on v1.1.11 must update to this version.

### 3. Project Progress
The last 24 hours featured 30 merged/closed PRs. The majority of merges were emergency fixes for the Windows Desktop build pipeline, but several architectural features made significant progress in the review stage.

**Merged Fixes:**
- **Windows Build Stabilization:** A series of PRs resolved the `aiohttp` SSL context regression (#5082, #5083), the `conda-unpack` Windows path escaping (#5084), and ultimately pinned the Windows environment to `openssl=3.5.6` (#5096). A revert of an earlier fix (#5092) was required to unblock the post1 release.
- **Desktop Version Bump:** `chore: bump version to 1.1.11.post1` (#5093) – released to address launch failures.
- **Frontend UI:** Fixed scrollbar flickering on the Environment Variables page (#4766) by removing distracting hover transforms.

**Open / Under Review:**
- **Runtime 2.0** (#5078): A monumental contribution proposing a modular decomposition of the core `Runner` into testable units with a `ToolCoordinator` layer.
- **Agent OS Driver** (#5067): An abstraction layer for external protocols (MCP/A2A/ACP).
- **DataPaw Plugin** (#4622): A community plugin adding 12 BIOS-level data-analysis skills.
- **Token Usage Badge** (#4433): Per-conversation token visibility with a floating UI overlay.
- **Desktop Port Persistence** (#5051): Fix for `localStorage` resetting on restart.
- **Governance & Sandbox Interface** (#5088): Initial discussion on sandbox abstractions.
- **Built-in PRD Tool** (#4902): Frontend-rendered CRUD tool for managing Product Requirements Documents.

### 4. Community Hot Topics
- **AgentScope 2.0 Migration (Issue #4727):** The highest-reaction open discussion (+2 👍, 8 comments). The community is actively examining how this breaking change will affect plugin, channel, and skill compatibility. Interest is high.
- **Independent Visual Model Fallback (Issue #4992):** A steady +1 👍 and 4 comments, reflecting a common need to pair text-only LLMs (e.g., DeepSeek) with a separate vision model without switching providers.
- **Agent-Generated Cron Jobs (Issue #5064):** Very active (6 comments) because it is a core autonomy use case failing silently.
- **Local Model Regression (Issue #4989):** The volume of engagement here (5 comments) signals strong user dissatisfaction with the regression when updating from v1.1.5.

### 5. Bugs & Stability
- **[CRITICAL] Windows Desktop Launch Failure (Issues #5095, #5086):** Complete launch denial for Desktop v1.1.11 users due to OpenSSL 3.5.7 regression. Hotfix shipped in v1.1.11.post1.
- **[HIGH] Tool Call Argument Corruption (Issue #5052 – Open):** After ~5 successful rounds, all tools fail with `got an unexpected keyword argument`. No maintainer response yet. This is a high-risk data integrity issue.
- **[HIGH] Agent-Generated Cron Jobs Not Triggering (Issue #5064 – Open):** Agent-created tasks appear in the UI but fail to execute or be manually edited.
- **[MEDIUM] UI Freeze on Session Switching (Issue #5053 – Open):** Tauri Desktop takes >10s to render when switching between 4+ chat sessions.
- **[MEDIUM] MODEL_EXECUTION_FAILED (Issue #5065 – Open):** Generic but blocking error reported on several provider backends.
- **[MEDIUM] Smart Agent JSON Formatting Crash (Issue #5091 – Open):** Skills modifying agent JSON files cause the application to crash entirely.
- **[LOW] DingTalk Empty AI Card (Issue #5057 – Closed):** Empty agent output sends a misleading "Processing..." card.

### 6. Feature Requests & Roadmap Signals
- **Runtime 2.0 (PR #5078) + AgentScope 2.0 (Issue #4727):** The biggest architectural bet. Signals a shift from a monolithic agent runner to a composable, testable, plugin-friendly core execution engine.
- **Agent OS Driver (PR #5067):** Positions CoPaw as a universal hub connecting MCP tools, A2A agents, and ACP services. This strongly signals a move toward interoperability as a core identity.
- **Context Compression (Issue #5063):** Headroom integration could reduce token usage by 60–95%. If adopted, it would be a major UX and cost differentiator.
- **Security Sandbox / Governance (Issue #4356, PR #5088):** Users are demanding whitelist/read-only file systems and tool guard granularity, signaling production and enterprise adoption pressure.
- **Data Analysis Plugin (PR #4622):** The DataPaw plugin suggests the project is expanding its identity from "personal assistant" to "analytical agent platform."

### 7. User Feedback Summary
Users remain deeply engaged, but satisfaction is strained by the frequency of stability regressions. **Local model users** (Qwen 3.6-27B, DeepSeek) are the most sensitive group and feel the pain of upgrade-related breakage. **Windows Desktop users** are experiencing the most friction (launch crashes, CMD popups, severe UI lag). The community is technically sophisticated, contributing complex PRs (Runtime 2.0, DataPaw, Security), which signals high investment. There is strong demand for **transparency** (token usage) and **control** (file guards, sub-agent visibility). The recent release cycle has generated a productive but anxious energy—users are excited about the roadmap but wary of upgrading immediately.

### 8. Backlog Watch
- **Tool Call Argument Corruption (Issue #5052 – Open, Jun 9):** A high-severity bug with no maintainer assignment. This should be prioritized as it undermines the core tool-use reliability.
- **Agent Cron Jobs Not Triggering (Issue #5064 – Open, Jun 10):** A core feature regression with heavy user impact. Needs immediate triage.
- **File/Tool Guard Granularity (Issue #4356 – Open, May 14):** Waiting nearly a month for a design decision. The recent Governance & Sandbox PR (#5088) may feed into this.
- **Token Usage Badge (PR #4433 – Under Review, May 15):** A long-standing, highly-demanded feature that has stalled in review. Closing this would be a significant community win.
- **DataPaw Plugin (PR #4622 – Under Review, May 22):** A substantial community contribution waiting on a final maintainer sign-off. The longer it sits, the higher the chance of merge conflicts.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the structured project digest for ZeroClaw based on the data provided.

---

## ZeroClaw Project Digest: 2026-06-11

### 1. Today's Overview
ZeroClaw is experiencing a surge of cross-platform compatibility fixes and localization efforts, signaling a mature push for project-wide stability and internationalization. Activity is extremely high, with **43 issues** and **50 pull requests** updated, although **zero new releases** today indicates that engineering effort is concentrated on development and hardening ahead of the next tag. While significant progress is being made on closing long-standing bugs and documentation gaps, several critical open issues concerning data integrity (message loss) and ecosystem integration (MCP blocking) remain the focus of urgent community attention.

### 2. Releases
*No new releases were published on this date.*

### 3. Project Progress
**10 PRs were merged or closed** and **19 issues were resolved** today. Key developments include:
- **Documentation & Community Health:** A long-standing broken Discord invite link was replaced with a vanity invite ([PR #7096](https://github.com/zeroclaw-labs/zeroclaw/pull/7096)), resolving a common onboarding friction point.
- **CI Hardening:** The maintainers reverted the aggressive cross-platform Clippy lint gate in favor of a targeted, optional workflow to avoid blocking routine PRs ([PR #7458](https://github.com/zeroclaw-labs/zeroclaw/pull/7458)).
- **Security & Config Validation:** The silent failure where `security.otp.gated_actions` accepted arbitrary action names was fixed (#5810), closing a security-visibility gap.
- **Channel Stability:** The Matrix channel memory leak (where sessions were incorrectly keyed on unique event IDs, causing amnesia between messages) was resolved (#6958).
- **Skills Cycle:** The official tracker for the v0.7.6 "zeroclaw skills" UX theme was closed (#6253), indicating the feature batch for that cycle is complete.

### 4. Community Hot Topics
The most active discussions reveal deep community engagement with core architecture and onboarding friction:

- **Full Docker Image ([#3642](github.com/zeroclaw-labs/zeroclaw/issues/3642), 12 comments):** This remains the most commented issue. Users are actively requesting a "batteries-included" Docker image compiled with all feature flags (e.g., WhatsApp) to lower the barrier for non-technical users. The issue is currently blocked.
- **User Message Loss ([#6034](github.com/zeroclaw-labs/zeroclaw/issues/6034), 6 comments):** This high-risk bug (where single and multi-turn conversations drop user messages) is generating significant anxiety as it breaks core conversational functionality.
- **MCP Tool Hang ([#6721](github.com/zeroclaw-labs/zeroclaw/issues/6721), 5 comments):** A critical workflow blocker for non-interactive (webhook) users, where `tool_search` is not approved by default, causing a silent 120-second timeout. This is a top barrier for MCP adoption.
- **Architectural Direction (RFCs):** Discussions around a lighter core (#6165), a native plugin system (#7420), and unifying the agent turn engines (#7415) show the community is actively debating the long-term technical roadmap.

### 5. Bugs & Stability
Stability is the dominant theme today, with a strong focus on platform parity:
- **Critical Workflows Blocked:**
    - **Delegation Bug ([#7470](github.com/zeroclaw-labs/zeroclaw/issues/7470), S1):** Newly reported bug where agent delegation blocks stricter security profiles, breaking multi-agent reviewer setups.
    - **Windows Test Suite ([#7462](github.com/zeroclaw-labs/zeroclaw/issues/7462), S2):** A fresh report details **74 test failures** on Windows 11, highlighting significant gaps in cross-platform CI that were not previously visible.
- **Platform-Specific Fixes:** The project is actively patching OS-level quirks. Multiple PRs landed today to fix macOS keybinding conflicts where Cmd-C was incorrectly triggering the Quit chord ([#7484](https://github.com/zeroclaw-labs/zeroclaw/pull/7484), [#7477](https://github.com/zeroclaw-labs/zeroclaw/pull/7477)).
- **Container Defaults:** A usability bug was identified where the container lacks `vi`, but the TUI defaults to it ([#7469](github.com/zeroclaw-labs/zeroclaw/issues/7469)). Fix PRs are already in the queue to switch the fallback editor to `nano` ([#7483](https://github.com/zeroclaw-labs/zeroclaw/pull/7483)).
- **Vision Model Integration:** The `image_info` tool is failing to pass data to vision models unless absolute POSIX paths are used ([#7436](github.com/zeroclaw-labs/zeroclaw/issues/7436)), blocking common usage patterns.

### 6. Feature Requests & Roadmap Signals
The feature pipeline is heavily weighted toward user experience and localization:

- **Internationalization (i18n):** A massive push for localization is visible today. PRs are landing to localize the quickstart provider selector ([#7481](https://github.com/zeroclaw-labs/zeroclaw/pull/7481)), the file download tool ([#7480](https://github.com/zeroclaw-labs/zeroclaw/pull/7480)), the locale install flow ([#7478](https://github.com/zeroclaw-labs/zeroclaw/pull/7478)), and theme body text ([#7482](https://github.com/zeroclaw-labs/zeroclaw/pull/7482)). This strongly suggests i18n is a major track for the upcoming release.
- **Configuration UX:** User requests highlight friction in the configuration workflow, specifically the inability to rename aliases ([#7468](github.com/zeroclaw-labs/zeroclaw/issues/7468)) and lack of arrow key navigation in edit strings ([#7467](github.com/zeroclaw-labs/zeroclaw/issues/7467)).
- **Observability & Debugging:** A large high-risk PR ([#7385](https://github.com/zeroclaw-labs/zeroclaw/pull/7385)) adds turn metadata and OTel span correlation, indicating investment in production debugging capabilities.
- **Future Predictions:** The Pre-Turn Routing RFC ([#7431](github.com/zeroclaw-labs/zeroclaw/issues/7431)) suggests an upcoming focus on more intelligent agentic routing. Given the spike in localization PRs, the next release (likely v0.7.7 or v0.8.0) should feature significant multi-language support.

### 7. User Feedback Summary
Feedback captured in today's digest reflects a user base that is technically demanding and deeply invested in the platform's evolution:
- **Pain Points:** The highest friction areas are **data reliability** (message loss #6034), **complex configuration** (aliases, tool approval matrices), and **platform inconsistency** (Windows test failures, macOS UI conflicts). The invalid Discord invite (#7037) was a clear community health issue that has now been resolved.
- **Desires:** Users are showing a strong appetite for **modularity** (plugin system, lighter core) and **ease of deployment** (full Docker image). There is a clear demand for better tooling visibility, as seen in the engagement with the "Doctor" improvements ([#7450](https://github.com/zeroclaw-labs/zeroclaw/pull/7450)).

### 8. Backlog Watch
Several high-priority, high-risk items require immediate maintainer attention:
- **MCP Tool Hang ([#6721](github.com/zeroclaw-labs/zeroclaw/issues/6721), P1):** This issue has been open for nearly a month and blocks all non-interactive MCP workflows. It is a critical friction point for the tool ecosystem.
- **User Message Loss ([#6034](github.com/zeroclaw-labs/zeroclaw/issues/6034), P1):** An S1 severity bug affecting core conversation logic. Despite being accepted, there is no clear link to a fix PR.
- **Full Docker Image ([#3642](github.com/zeroclaw-labs/zeroclaw/issues/3642)):** The "blocked" status on this high-demand feature needs a decision or progress update to manage community expectations.
- **Unratified RFCs:** Both the "Lighter Core" RFC ([#6165](github.com/zeroclaw-labs/zeroclaw/issues/6165)) and the "Plugin System" RFC ([#7420](github.com/zeroclaw-labs/zeroclaw/issues/7420)) are tagged `needs-maintainer-review` and represent significant architectural forks that are stalling community contributions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*