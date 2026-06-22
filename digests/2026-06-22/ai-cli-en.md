# AI CLI Tools Community Digest 2026-06-22

> Generated: 2026-06-22 03:54 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-06-22
**Scope:** 9 Major AI CLI Tools

---

## 1. Ecosystem Overview

The AI CLI development tools ecosystem is undergoing a critical transition from novelty to production-grade reliability. On June 22, 2026, the dominant themes across all major tools are **cost transparency**, **session persistence**, and **security integrity**, with backend reliability and billing accuracy testing user trust across several key players. While tools like Qwen Code, OpenCode, and Pi demonstrate high-velocity feature iteration, established incumbents like GitHub Copilot CLI and Gemini CLI face growing friction over platform-specific regressions and agent reliability. The cross-cutting demand for observable, controllable, and cost-aware agentic workflows signals that the market is maturing far beyond simple "code generation" toward comprehensive development automation infrastructure.

---

## 2. Activity Comparison

| Tool | Hot Issues (Today) | Key PRs (Today) | Release Status | Velocity Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 2 | None | 🟡 Consolidating |
| **OpenAI Codex** | 10 | 10 | 2x Alpha | 🟢 Heavy Infra |
| **Gemini CLI** | 10 | 10 | None (Blocked) | 🟡 Stalled |
| **GitHub Copilot CLI** | 7 | 1 | None | 🔴 Troubled |
| **Kimi Code CLI** | 2 | 0 | None | 🟡 Quiet |
| **OpenCode** | 10 | 10 | None | 🟢 Rapid |
| **Pi** | 10 | 7 (All Merged) | None | 🟢 Rapid |
| **Qwen Code** | 10 | 10 | **v0.18.5 Stable** | 🟢 Rapid |
| **CodeWhale (DeepSeek)** | 10 | 10 | v0.8.63 | 🟢 Rapid |

**Key Insight:** The ecosystem splits into three velocity tiers—agile contenders (OpenCode, Qwen Code, Pi, CodeWhale), infrastructure-heavy incumbents (OpenAI Codex, Claude Code), and tools facing execution crises (GitHub Copilot CLI, Gemini CLI).

---

## 3. Shared Feature Directions

Multiple tool communities are converging on the same requirements independently, indicating industry-wide shifts:

### Cost Observability & Guardrails (Dominant Theme)
| Requirement | Tools | Specific Evidence |
|---|---|---|
| Pre-flight cost warnings | **Claude Code** | #68703 (expensive skills) |
| Metering/Quota audits | **OpenAI Codex**, **GitHub Copilot CLI** | #28879 (10-20x cost spike), #3881 (5% vs 2% billing) |
| Programmatic cost APIs | **Claude Code**, **OpenCode** | #50926, #16017 |
| Real-time cost from provider | **Pi** | #5950 (OpenRouter actual cost) |
| Silent premium model invocation | **OpenCode** | #30320 |

### Session Persistence & Memory
| Requirement | Tools | Specific Evidence |
|---|---|---|
| Inter-session communication | **Claude Code** | #24798 |
| Persistent memory system | **Kimi Code CLI** | #1283 (top feature request) |
| Session file recovery | **Gemini CLI** | #27904, #27905, #27912 (corruption fixes) |
| Revivable sub-agents | **Qwen Code** | #5540/#5556 (background agent resumption) |
| Auto-compaction safety | **Pi**, **CodeWhale** | #5937 (opt-in, between-turn checkpoint) |

### MCP / Plugin Ecosystem Hardening
| Requirement | Tools | Specific Evidence |
|---|---|---|
| OAuth for MCP setup | **OpenCode** | #988 (95 👍, most-wanted feature) |
| Live MCP hot-reload | **Qwen Code** | #5561 |
| ACP mode MCP loading | **Kimi Code CLI** | #2464 (critical regression) |
| Broken permission models | **Claude Code**, **GitHub Copilot CLI** | #61097, #69960, #3874 (inert hooks) |
| Tool count limits | **Gemini CLI** | #24246 (400 error >128 tools) |

### Cross-Platform Parity
| Requirement | Tools | Specific Evidence |
|---|---|---|
| Windows installer | **OpenAI Codex** | #13993 (153 👍, longest requested) |
| Android support | **Claude Code** | #50270 (broken since v2.1.113) |
| Windows ARM64 crash | **GitHub Copilot CLI** | #3687 (BEX64 under load) |
| Wayland support | **Gemini CLI** | #21983 (browser agent broken) |
| Native build gaps | **Qwen Code** | #5580 (win32-arm64, musl missing) |

### Agent Loop Reliability & Safety
| Requirement | Tools | Specific Evidence |
|---|---|---|
| Turn-stall recovery | **CodeWhale** | #2487 (no recovery path) |
| Hangs/false success | **Gemini CLI** | #21409, #22323, #25166 |
| Connection/timeout hardening | **Pi** | #4945, #5778 (unresponsive streams) |
| Scope creep prevention | **CodeWhale**, **Gemini CLI** | #3275, #22672 (destructive behavior) |

---

## 4. Differentiation Analysis

| Tool | Strategic Focus | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Agent orchestration depth & cost transparency | Senior developers on complex projects | Skills/subagent economy, rich session model |
| **OpenAI Codex** | Platform scaling & architectural maturity | Enterprise teams, VS Code ecosystem | Rust backend, SQLite thread store, code-mode runtime |
| **Gemini CLI** | Institutional security & data integrity | Google Cloud ecosystem, security-conscious | Folder-trust, deterministic redaction, JSONL recovery |
| **GitHub Copilot CLI** | GitHub ecosystem integration | GitHub enterprise users, Windows | Minimal velocity, platform-dependent (Windows/Mac issues) |
| **Kimi Code CLI** | Baseline catch-up | MoonshotAI ecosystem, Chinese market | Quiet iteration on core features |
| **OpenCode** | Open-standard multi-agent orchestration | Power users, ops-friendly teams | Aggressive ACP/OAuth adoption, Postgres state, APIs |
| **Pi** | Extension platform & local flexibility | Tinkerers, self-hosters, local LLM users | Rich extension API, OpenRouter cost, agent loop hardening |
| **Qwen Code** | Feature velocity & voice innovation | Alibaba ecosystem, multimodal developers | Voice dictation, CI testing, MCP hot-reload |
| **CodeWhale** | Security guardrails & brand rebuild | DeepSeek users, security-first agents | Right guardrails, sandbox trust, auto-review policies |

**Key Differentiators:**
- **OpenCode** is pulling ahead as the standard-bearer for open protocols (OAuth, ACP, programmable APIs).
- **Qwen Code** uniquely differentiates with voice dictation and the highest feature delivery velocity.
- **Pi** stands out for operational discipline (7/7 PRs merged) and deep provider flexibility.
- **GitHub Copilot CLI** is dangerously undifferentiated, lagging in every category.

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid Feature Iteration)
- **Qwen Code**: Highest velocity combined with a stable release. Voice dictation landing and integration test infrastructure (fake OpenAI server) show strong engineering hygiene.
- **OpenCode**: Extremely active PR pipeline. Moving aggressively toward enterprise-grade multi-agent orchestration (ACP subagent routing, lazy MCP loading, OAuth).
- **Pi**: Excellent release discipline (all PRs merged). Strong focus on agent loop hardening, extension API, and local providers.
- **CodeWhale**: Aggressively rebranding and refactoring large codebase (config monolith refactor) while maintaining high PR output.

### Infrastructure Deep-Dive (Architectural Investment)
- **OpenAI Codex**: Most mature architectural debates despite cost crisis. Rust backend, SQLite thread store overhaul, code-mode runtime decoupling indicate long-term platform thinking.
- **Claude Code**: Community engagement is deepest on architectural topics (inter-session comms, skill economics) despite low PR velocity.

### Stagnation / Execution Risk
- **GitHub Copilot CLI**: Lowest trust and velocity. Broken security, billing, and platform features with negligible PR activity. Highest risk of user attrition.
- **Gemini CLI**: Technically active but stalled on nightly release. Core loop reliability issues (hangs, false success) undermine autonomous mode value proposition.
- **Kimi Code CLI**: Quietest day by far. Awaiting fundamental infrastructure (memory system) that competitors already have.

---

## 6. Trend Signals (Actionable Industry Insights)

### 1. Cost is the New Reliability
The single strongest signal across the ecosystem. Users are moving past "can it work?" to **"can I afford to run it and understand my bills?"** Tools that fail to provide real-time cost data, pre-flight estimates, or programmatic guardrails within the next quarter will face a trust deficit. The OpenAI Codex cost spike (#28879) is a canary in the coal mine—expect this to become the #1 evaluation criterion for paid tools.

### 2. Security is Validated, Not Declared
Users are actively probing safety features. GitHub Copilot's inert `preToolUse` hooks (#3874) and non-functional sandbox filters (#3861) represent a **catastrophic trust failure** for enterprise buyers. Pi's quick secret-disclosure fix (#5955) and Gemini's folder-trust fix (#27903) set the correct response pattern. Expect security claims to be independently verified by community penetration testing going forward.

### 3. Session Continuity is the New Latency
Just as low token latency defined the 2024-2025 generation, **session/memory/persistence is the new critical UX metric**. Tools relying on purely stateless interactions (Kimi Code CLI, early Gemini patterns) are being dragged toward durable, cross-session memory. Inter-session communication (#24798), revivable sub-agents (#5540), and memory systems (#1283) are the feature requests that will define the next 12 months.

### 4. Terminal is Becoming a Launchpad
The "CLI" tool is expanding its surface area dramatically: voice input (Qwen Code), custom TUI components (Pi), OAuth flows (OpenCode), inline MCP UIs (OpenAI Codex), and dedicated IDE integrations (Claude Code VS Code plugin). The line between "CLI tool" and "agent development environment" is blurring. Pure terminal-interaction models are at risk of commoditization.

### 5. Graded Autonomy is the Winning Model
The community is rejecting binary "on/off" autonomy switches. Users want a **spectrum of control**: YOLO mode, safe planner, interactive reviewer, pre-flight gates, and permissions matrices. Tools offering rigid autonomy models (CodeWhale's current struggles, GitHub's broken hooks) will be outperformed by those offering transparent, configurable, observable autonomy tracks.

### 6. Open Protocol Adoption Drives Ecosystem Loyalty
MCP is the universal integration layer, but standardization is painful. Tools investing in ACP, OAuth for MCP discovery, transparent permission delegation, and open source interoperability (OpenCode, Qwen, Pi) are building defensible moats against vendor lock-in. Closed ecosystems with opaque configurations are losing the community development race.

### 7. Platform Expansion is a Competitive Moat
Voice (Qwen Code), OAuth flows (OpenCode), custom DBMS (OpenCode), local model providers (Pi), and cross-platform parity (everyone's Achilles heel) are becoming table stakes. Tools that ignore platform gaps (Claude Code on Android, OpenAI Codex on Windows, GitHub Copilot on ARM64) are leaving money on the table and risking developer frustration.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of: 2026-06-22 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The highest-attention PRs reveal a community deeply focused on infrastructure reliability, enterprise platforms, and structured cognition.

**#1298 — Fix run_eval.py 0% Recall**
*Author: MartinCajiao | Status: Open*
- **Functionality:** Resolves a critical bug where `run_eval.py` reports `recall=0%` for every skill description, rendering the `skill-creator` optimization loop broken.
- **Discussion:** This is the ecosystem's most urgent technical fix. It is directly linked to Issue #556 (12 comments, 7 👍), the most discussed technical bug. The community is effectively blocked from iterating on skill descriptions until this lands.
- [View PR #1298](https://github.com/anthropics/skills/pull/1298)

**#83 — Skill Quality & Security Analyzer**
*Author: eovidiu | Status: Open*
- **Functionality:** Meta-skills that evaluate other Skills across five dimensions: structure, documentation, quality, performance, and security.
- **Discussion:** Foundational for marketplace trust. Directly intersects with the security concerns raised in Issue #492 about namespace trust boundaries. The community sees quality benchmarks as essential for scaling.
- [View PR #83](https://github.com/anthropics/skills/pull/83)

**#444 — AURELION Skill Suite**
*Author: Chase-Key | Status: Open*
- **Functionality:** A four-skill cognitive framework (Kernel, Advisor, Agent, Memory) for structured professional knowledge management.
- **Discussion:** The most architecturally ambitious submission. The 5-floor cognitive framework generated extensive discussion about moving Skills from task-automation to structured agent cognition.
- [View PR #444](https://github.com/anthropics/skills/pull/444)

**#514 — Document Typography**
*Author: PGTBoos | Status: Open*
- **Functionality:** Prevents orphans, widows, and numbering misalignment in AI-generated documents.
- **Discussion:** A tightly-scoped, high-impact skill solving a pervasive output quality problem. Received strong positive signal for its immediate, tangible value to any document workflow.
- [View PR #514](https://github.com/anthropics/skills/pull/514)

**#723 — Testing Patterns**
*Author: 4444J99 | Status: Open*
- **Functionality:** Comprehensive testing guidance covering Unit (AAA), React (Testing Library), and E2E, based on the Testing Trophy model.
- **Discussion:** Fills a universal developer workflow gap. The detailed methodology sparked debate on what Claude should "know" vs. what a Skill should encode.
- [View PR #723](https://github.com/anthropics/skills/pull/723)

**#568 — ServiceNow Platform**
*Author: Vanka07 | Status: Open*
- **Functionality:** Broad platform assistant covering ITSM, ITOM, SecOps, ITAM, FSM, CSDM, and IntegrationHub.
- **Discussion:** The strongest enterprise signal in the pipeline. The wide scope raised important discussions about domain coverage vs. prompt specificity in enterprise contexts.
- [View PR #568](https://github.com/anthropics/skills/pull/568)

**#154 — Shodh-Memory**
*Author: varun29ankuS | Status: Open*
- **Functionality:** Persistent memory system enabling context retention across conversations for AI agents.
- **Discussion:** Addresses the fundamental statelessness limitation. The discussion centers on memory structuring efficiency, surfacing memories proactively, and context window management.
- [View PR #154](https://github.com/anthropics/skills/pull/154)

---

## 2. Community Demand Trends

Analysis of the most active Issues reveals four concentrated demand vectors:

**Enterprise Scaling & Trust (Top Signal)**
- Issue #228 (14 comments, 7 👍): Org-wide skill sharing — users demand organizational libraries over manual `.skill` file distribution.
- Issue #492 (9 comments, 2 👍): Trust boundary abuse — community skills under `anthropic/` namespace erode security.
- Issue #1175 (4 comments): Security concerns when handling SharePoint documents via Skills.
- *Trend:* The community's primary bottleneck has shifted from creation to governance and distribution.

**Developer Infrastructure Reliability (Urgent Technical Debt)**
- Issue #556 (12 comments, 7 👍): `run_eval.py` 0% trigger rate — the single most discussed technical problem.
- Issue #1061 (3 comments): Windows compat (PATHEXT, cp1252, select on pipes).
- Issue #1169 (3 comments): Literal slash-command queries also score recall=0%.
- *Trend:* Cross-platform evaluation tooling is breaking contributor trust in the development loop.

**Agentic Memory & Safety**
- Issue #1329 (3 comments): Proposal for compact-memory using symbolic notation.
- Issue #412 (6 comments): Agent governance skill proposal (policy enforcement, audit trails).
- *Trend:* The community is preparing for autonomous, multi-turn agent operations requiring structured state and safety patterns.

**Standardization & Platform Integration**
- Issue #16 (4 comments): Exposing Skills as MCPs — a long-standing architectural request.
- Issue #189 (6 comments, 9 👍): Duplicate skills when installing both `document-skills` and `example-skills`.
- *Trend:* Demand for deduplication, pluggable standards, and MCP interoperability.

---

## 3. High-Potential Pending Skills

These active PRs are poised to land soon and significantly impact the ecosystem:

| PR | Skill | Author | Priority Level | Why It Matters |
|---|---|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | Eval Script Fix | MartinCajiao | **Critical** | Unblocks the entire skill-creator pipeline; directly resolves #556 |
| [#514](https://github.com/anthropics/skills/pull/514) | Document Typography | PGTBoos | **High** | Solves pervasive output quality issue; clean, merge-ready scope |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing Patterns | 4444J99 | **High** | Fills a universal developer workflow gap |
| [#444](https://github.com/anthropics/skills/pull/444) | AURELION Suite | Chase-Key | **Medium/High** | Major architectural contribution; moves beyond task automation |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow Platform | Vanka07 | **Medium/High** | Strongest enterprise platform signal; requires domain validation |
| [#154](https://github.com/anthropics/skills/pull/154) | Shodh-Memory | varun29ankuS | **Medium** | Key agent infrastructure; pending iteration on context efficiency |
| [#210](https://github.com/anthropics/skills/pull/210) | Frontend Design Clarity | justinwetch | **Medium** | Iterative improvement of an existing core skill; actionability focus |

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand spans two interdependent fronts: **reliable, cross-platform developer infrastructure** (fixing the evaluation pipeline, ensuring Windows compatibility) as the foundation for scaling towards **enterprise-grade platform automation and persistent agentic memory** as the defining killer use cases for the Claude Code Skills format.

---

# Claude Code Community Digest — 2026-06-22

## 1. Today's Highlights

API instability is the story of the day, with fresh reports of "Service Unavailable" errors (#69942) and Opus 502 responses (#69785) suggesting backend turbulence degrading user sessions. The prolonged Android/Termux regression (#50270) remains the most commented open issue at 53 messages, reflecting deep frustration over the unaddressed glibc binary switch. Underneath these surface-level bugs, a strong community consensus is forming around **cost transparency**, with users demanding pre-flight warnings on expensive skills (#68703) and better observability into subagent quota burn (#69931).

## 2. Releases

No new versions of Claude Code were published in the last 24 hours.

## 3. Hot Issues

- **[#50270] Android Termux — Broken Since v2.1.113** (53 💬, 51 👍)
  The switch from a JavaScript entry point to a native glibc binary has made Claude Code completely inoperable on Termux/Android, where `process.platform` reports `android`. Two months without a fix makes this an increasingly urgent platform gap for mobile and embedded developers.
  [Issue #50270](https://github.com/anthropics/claude-code/issues/50270)

- **[#24798] Inter-Session Communication** (38 💬, 18 👍)
  Developers running parallel Claude Code sessions on large projects want structured ways to share context and sequence tasks. This is one of the most active feature discussions, reflecting the limits of the single-session paradigm.
  [Issue #24798](https://github.com/anthropics/claude-code/issues/24798)

- **[#36179] VS Code Plugin: `redacted_thinking` Content Type Error** (29 💬, 18 👍)
  A persistent bug on Windows and VS Code where unsupported content responses cause the plugin to fail. High engagement suggests wide impact on IDE-based workflows.
  [Issue #36179](https://github.com/anthropics/claude-code/issues/36179)

- **[#69942] API: Service Unavailable** (5 💬, 11 👍)
  Fresh reports of Anthropic API downtime, accumulating upvotes rapidly today. Coupled with #69785 (Opus 4.8 502 errors), this is a clear signal that backend reliability is impacting user trust.
  [Issue #69942](https://github.com/anthropics/claude-code/issues/69942)

- **[#69931] Claude Max Weekly Quota Depleted Unexpectedly by Subagents** (2 💬)
  A specific report that Gmail MCP subagent workflows consumed an entire weekly quota faster than expected. This is the canary in the coal mine for the broader cost visibility trend.
  [Issue #69931](https://github.com/anthropics/claude-code/issues/69931)

- **[#65995] macOS pty File Descriptor Leak** (4 💬, 4 👍)
  A critical stability bug where Claude Desktop leaks `ptmx` FDs, eventually killing all terminal sessions on the host with `forkpty: Device not configured`. A system-level failure vector for a CLI tool.
  [Issue #65995](https://github.com/anthropics/claude-code/issues/65995)

- **[#61097] MCP Routine 'Always Allow' Ignored** (12 💬) [CLOSED]
  Team plan users found that 'Always Allow' permissions on Gmail MCP tools were bypassed in Cloud Routines. Closed, but the pattern of permission model fragility is a recurring theme.
  [Issue #61097](https://github.com/anthropics/claude-code/issues/61097)

- **[#68514] macOS Sequoia Checksum Mismatch** (11 💬)
  Installer integrity failures for `rootfs.img.zst` on macOS 15.7.7. An unwelcome onboarding friction that undermines confidence in the release pipeline.
  [Issue #68514](https://github.com/anthropics/claude-code/issues/68514)

- **[#68703] Pre-Flight Cost Confirmation for Skills** (2 💬)
  A direct proposal to address quota shock by surfacing estimated token cost before launching expensive skills like `deep-research`. This is rapidly becoming one of the highest-signal feature requests.
  [Issue #68703](https://github.com/anthropics/claude-code/issues/68703)

- **[#69807] Desktop Cowork/Code Sessions Hang on Load** (3 💬)
  A regression in Desktop 1.14271.0 causing sessions to freeze on startup post-update. Highlights ongoing instability in the desktop client rollout.
  [Issue #69807](https://github.com/anthropics/claude-code/issues/69807)

## 4. Key PR Progress

*The active PR queue is very quiet today (only 2 open items), but both carry notable signals about the project.*

- **[#4943] Shell Completions for Bash, Zsh, Fish** (Open since Aug 2025)
  *Analysis:* This PR has been open for over 10 months, waiting to merge basic tab-completions — a standard expectation for any professional CLI tool. The stagnation here is telling: it suggests the core CLI ergonomics team may be stretched thin or that such foundational DX improvements are being deprioritized relative to agentic/ML features.
  [PR #4943](https://github.com/anthropics/claude-code/pull/4943)

- **[#69916] Fix Silent Exit in Issue Triage Script**
  *Analysis:* A small fix for the project's own `edit-issue-labels.sh` script to replace a silent `exit 1` with a proper error message. Indicates ongoing internal CI/CD tooling refinement, but does not address any user-facing concerns.
  [PR #69916](https://github.com/anthropics/claude-code/pull/69916)

## 5. Feature Request Trends

The community is maturing past "does it work?" and asking **"can I control and observe it at scale?"**

- **Cost Observability & Guardrails:** This is the dominant trend. Users want quotas exposed in the statusline (#59709), programmatic cost data for hooks and plugins (#50926), and pre-flight confirmation dialogs before executing expensive skills (#68703). The "quota shock" of subagent-heavy MCP workflows (#69931) is accelerating this demand.
- **Advanced Session Orchestration:** Single-session limits are biting. The community wants conversation forking in IDEs (#69272), inter-session communication (#24798), and per-project session shortcuts in the sidebar (#49039). The developer is evolving into a "session conductor," not just a prompt sender.
- **MCP Ecosystem Stability & Usability:** Users are demanding that the MCP promise holds. Issues revolve around permission model bugs (#61097, #69960), missing built-in connector functionality (#69317, #69965), and insufficient tool previews in permission prompts (#69961).
- **Platform Expansion:** The Android exclusion (#50270) and requests for RISC-V support (#59813) and a native non-terminal JetBrains UI (#69778) show the userbase is diverse and actively working on non-standard platforms.

## 6. Developer Pain Points

- **The Android Blackout:** The glibc binary switch was a backwards-incompatible change that completely excluded an entire platform of developers with no rollback or fallback mechanism provided.
- **API Reliability & Session Brittleness:** Users face a confusing landscape of 502/503 errors, opaque session kills (e.g., image processing errors #47391), and server-side session leaks that burn quota after the user has exited (#69526).
- **macOS System Resource Abuse:** The pty FD leak (#65995) is a catastrophic bug for a CLI tool — it doesn't just break Claude, it breaks every terminal session on the machine.
- **MCP Permission Model Fatigue:** "Always Allow" settings being silently overridden (#61097) and missing content previews in "Ask before edit" prompts (#69961) erode trust in the automation and safety model.
- **Hidden Cost Spikes:** The community is experiencing sticker shock from subagent fan-out and expensive skills. Without pre-flight warnings or programmatic cost data, users feel powerless to control spending.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest – June 22, 2026**

### 1. Today's Highlights
A critical wave of rate-limit billing issues dominates community discussion today, with users reporting a 10–20× increase in cost-per-token on the `gpt-5.5` Plus plan (#28879). On the development front, the team is deeply engaged in architectural overhauls for "code-mode" runtime decoupling and a major SQLite-based thread store performance improvement. Meanwhile, Windows users continue to face significant platform-specific regressions, particularly around sandbox execution and the lack of a standalone installer.

### 2. Releases
Two new alpha versions of the Rust-based backend shipped in the last 24 hours. No detailed changelogs were published, suggesting targeted hotfixes or internal infrastructure refinements rather than visible user-facing features.

- [Release v0.142.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.9)
- [Release v0.142.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.10)

### 3. Hot Issues

1.  **#28879 – Severe Rate Limit Cost Spike**
    *Users on the Plus plan report a sudden 10–20× increase in per-token rate-limit consumption since June 16, draining a 5-hour budget in 2–3 prompts.*
    This is the highest-signal issue in the queue (101 comments, 195 👍), representing a major trust and value crisis for the paid user base.
    [Issue #28879](https://github.com/openai/codex/issues/28879)

2.  **#13993 – Windows Standalone Installer Request**
    *A long-standing demand for a traditional `codex-setup.exe` installer, as many Windows users are blocked by Microsoft Store restrictions, corporate policies, or offline environments.*
    75 comments and 153 thumbs up make this the most requested enhancement.
    [Issue #13993](https://github.com/openai/codex/issues/13993)

3.  **#25749 – Phone MFA Lockout**
    *Users authenticated via Google OAuth with valid MFA are completely locked out because Codex requires a legacy phone number with no recovery or replacement path.*
    A severe UX and support failure affecting 57 users.
    [Issue #25749](https://github.com/openai/codex/issues/25749)

4.  **#18993 – VS Code Extension History Regression**
    *A recent update to the VS Code extension (v1.117.0) breaks access to all past conversation sessions.*
    33 comments highlight a critical regression in daily IDE workflows.
    [Issue #18993](https://github.com/openai/codex/issues/18993)

5.  **#27694 – macOS Dock Crash**
    *Codex Desktop 26.609.30741 crashes the macOS Dock via `setDockTile` recursion.*
    A platform-specific crash affecting the native desktop experience on macOS.
    [Issue #27694](https://github.com/openai/codex/issues/27694)

6.  **#26600 / #28908 / #28492 – Quota Drain & Accounting Errors**
    *Multiple independent reports of quota decreasing while idle, or severely incorrect time accounting (e.g., 27 hours billed for a 15-hour task).*
    These systemic accounting bugs compound the anxiety around the cost spike in #28879.
    [Issue #26600](https://github.com/openai/codex/issues/26600) | [#28908](https://github.com/openai/codex/issues/28908) | [#28492](https://github.com/openai/codex/issues/28492)

7.  **#29205 – Sandbox State Metadata Regression**
    *Desktop in-app browser and annotation tools fail with "missing field sandboxPolicy", breaking the browser automation bridge.*
    A recently closed but high-activity bug (15 comments) affecting core desktop tooling.
    [Issue #29205](https://github.com/openai/codex/issues/29205)

8.  **#26158 – Windows Sandbox CLI Regression**
    *Codex CLI 0.138.0+ breaks sandbox execution on Windows with `CreateProcessAsUserW: 2`. Users must roll back to `0.132.0`.*
    A significant platform regression forcing manual version pinning.
    [Issue #26158](https://github.com/openai/codex/issues/26158)

9.  **#21019 – MCP Inline UI Rendering Broken**
    *Codex Desktop can invoke MCP tools but fails to call `read-mcp-resource`, preventing the rendering of inline iframe UI resources.*
    A core gap in the MCP Apps integration story (11 comments, 14 👍).
    [Issue #21019](https://github.com/openai/codex/issues/21019)

10. **#29200 – Windows Patch Dialog Bug**
    *A recent update causes a persistent `codex-windows-sandbox-setup.exe` error dialog to appear on every `apply_patch` invocation.*
    Annoying and disruptive behavior introduced in the latest Windows release.
    [Issue #29200](https://github.com/openai/codex/issues/29200)

### 4. Key PR Progress

1.  **#29375 – NPM Marketplace Plugin Sources**
    *Adds `npm` as a first-class plugin source, allowing developers to install plugins directly from npm registries with lifecycle scripts disabled.*
    A major new capability for extending Codex.
    [PR #29375](https://github.com/openai/codex/pull/29375)

2.  **#29371 – Propagate Safety Buffering Events**
    *Decodes and deduplicates `safety_buffering` metadata from the Responses API so clients can render in-progress safety review states.*
    Closes a critical transparency gap in the safety pipeline.
    [PR #29371](https://github.com/openai/codex/pull/29371)

3.  **#29073 – Refresh Environment Context Before Sampling**
    *Fixes a race condition where nonblocking environment startup leaves the model looking at stale “environment loading” snapshots.*
    A quality-of-life fix for remote and cloud execution flows.
    [PR #29073](https://github.com/openai/codex/pull/29073)

4.  **#29290 / #29291 / #29292 – Code-Mode Runtime Refactoring (cconger)**
    *Decouples cell creation from observation and exposes a transport-neutral session runtime. This is the architectural foundation for the upcoming "code-mode" feature.*
    A significant restructuring of how Codex handles long-running sessions.
    [PR #29290](https://github.com/openai/codex/pull/29290) | [#29291](https://github.com/openai/codex/pull/29291) | [#29292](https://github.com/openai/codex/pull/29292)

5.  **#29352 / #29355 / #29357 / #29367 – Thread Store Performance Overhaul (anaiskillian)**
    *Replaces heavy filesystem scans with lightweight SQLite projections for `thread/list`, `thread/resume`, and `thread/fork`.*
    A major backend optimization that will significantly reduce latency for users with large thread histories.
    [PR #29352](https://github.com/openai/codex/pull/29352) | [#29355](https://github.com/openai/codex/pull/29355) | [#29357](https://github.com/openai/codex/pull/29357) | [#29367](https://github.com/openai/codex/pull/29367)

6.  **#29358 – MCP Sandbox State Interop**
    *Enables `codex sandbox` to consume and reuse sandbox state directly from MCP servers without requiring the server to understand underlying sandbox internals.*
    Improves the integration surface between MCP servers and Codex runtimes.
    [PR #29358](https://github.com/openai/codex/pull/29358)

7.  **#28260 – Auto-Compaction Escape Hatch**
    *Adds an internal feature flag to disable automatic context window compaction, preserving conversation history from aggressive pruning.*
    A developer-focused control for debugging and long-running sessions.
    [PR #28260](https://github.com/openai/codex/pull/28260)

8.  **#28232 – Workspace Headline in TUI**
    *Adds a configurable status-line item to the terminal UI displaying the active workspace headline, synced from the backend.*
    A useful visual enhancement for the Codex CLI.
    [PR #28232](https://github.com/openai/codex/pull/28232)

9.  **#29301 – Updated Plan Mode Prompt**
    *Improves the plan mode prompt so the model renders the implementation plan to the user on relevant follow-ups, allowing easier transition into implementation.*
    A UX improvement reducing friction in the plan-to-code workflow.
    [PR #29301](https://github.com/openai/codex/pull/29301)

10. **#29109 – Eliminate Redundant Rollout Reads**
    *Optimizes `thread/read` by avoiding redundant file parsing when SQLite already holds the required rollout path and history.*
    A performance optimization contributing to the broader thread store improvements.
    [PR #29109](https://github.com/openai/codex/pull/29109)

### 5. Feature Request Trends

- **Granular Quota & Cost Controls:** The rate-limit crisis has catalyzed demand for agent-accessible quota status (#24927) and configurable model/cost controls for background processes like Chronicle memory writing (#26808). Users want visibility into exactly what consumes credits and the ability to stop it programmatically.
- **Windows Platform Parity:** The request for a standalone Windows installer (#13993) is the flagship feature request, but the steady stream of platform-specific bugs underscores a systemic desire for feature parity with macOS.
- **MCP Ecosystem Maturation:** Developers are pushing for full inline UI rendering for MCP Apps (#21019), better integration with popular tools like Canva (#29210), and faster startup when MCP servers are slow to list tools (#28640).
- **Session State Reliability:** Beyond features, users are requesting fundamental reliability in session mechanics, including proper handling of remote worktrees (#28238) and adherence to explicit user intent over silent background actions (#28750).

### 6. Developer Pain Points

- **The Cost Spike Crisis:** The single most urgent pain point is the 10–20× cost increase for `gpt-5.5` (#28879) combined with latent background quota drainage (#26600). This is creating a significant trust deficit with the paid user base, who feel their subscription value is degrading without warning or recourse.
- **Windows as a Second-Class Platform:** Windows developers are disproportionately impacted by regressions. Core sandbox functionality breaks across minor updates (#26158, #29200, #20570), and the lack of a standard installer (#13993) forces reliance on the Microsoft Store, which is unusable in many corporate environments.
- **Background Processes & Context Management:** Users are frustrated by actions occurring without explicit consent—whether it is `git add -A` flooding the object database (#28750), automatic context compaction destroying useful history (#28260), or background memory writers burning quota (#26808). The desire for an explicit "do what I say" mode is palpable.
- **Authentication & Support Dead Ends:** The inability to recover accounts when legacy MFA phone numbers are unavailable (#25749) represents a severe customer support failure that completely blocks productivity for affected developers.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

Here is the Gemini CLI community digest for **2026-06-22**.

---

## Gemini CLI Community Digest — 2026-06-22

### 1. Today's Highlights
The nightly release pipeline is currently blocked by a **release failure** for `v0.49.0-nightly.20260622` (#28087). A major push is underway to improve **session data integrity**, with a batch of critical PRs fixing JSONL file corruption, race conditions in session cleanup, and broken session recovery logic (#27904, #27905, #27912, #27906). On the security front, fixes landed to ensure the **folder-trust dialog** properly displays all hooks before granting trust (#27903).

---

### 2. Releases
None.

---

### 3. Hot Issues
1. **[#28087 — Nightly Release Failed](https://github.com/google-gemini/gemini-cli/issues/28087)**  
   P1 release-blocker. The automated nightly workflow failed today, halting pipeline progress.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   P1 bug with the highest community engagement (8 👍). The CLI hangs indefinitely when deferring to the generalist agent, requiring manual cancellation. A top reliability blocker.

3. **[#25166 — Shell command gets stuck on "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   P1 core bug. The terminal shows a shell command as active long after the command completes, breaking the fundamental CLI workflow.

4. **[#22323 — Subagent MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   P1 logic bug. The `codebase_investigator` subagent misreports hitting the turn limit as a successful goal completion, masking critical agent failures.

5. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   P2 security issue. User transcripts are sent to the extraction model *before* redaction, creating a risk of secret exposure in the memory system.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   Persistent user frustration. Custom skills and sub-agents are rarely invoked autonomously by the model, even when explicitly configured, limiting a key extensibility feature.

7. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   P2 scalability blocker. Users integrating many MCP tools hit a hard API limit, and the agent fails to intelligently scope tool selection.

8. **[#27985 — ACP cached/thought tokens omitted](https://github.com/google-gemini/gemini-cli/issues/27985)**  
   Important for the non-interactive ACP server mode. Incomplete token usage reporting leads to inflated client-side cost estimates.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
   Customer issue. The agent uses `git reset`, `--force`, and other destructive commands too readily without considering safer alternatives.

10. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
    Platform compatibility issue. The browser subagent is entirely non-functional on Linux Wayland sessions.

---

### 4. Key PR Progress
1. **[#27910 — Bound web search tool latency](https://github.com/google-gemini/gemini-cli/pull/27910)**  
   Adds a 120-second timeout to `google_web_search` calls (Fixes #27890). Prevents the agent from hanging indefinitely on slow or failing search queries.

2. **[#27903 — Disclose hooks in canonical nested shape](https://github.com/google-gemini/gemini-cli/pull/27903)**  
   Critical security fix. The folder-trust dialog now properly enumerates hooks declared in the canonical nested format, preventing hidden command execution.

3. **[#27730 — Keep array tool results out of structuredContent](https://github.com/google-gemini/gemini-cli/pull/27730)**  
   Fixes an MCP compliance bug where `McpComplianceTransport` incorrectly copied JSON arrays into `structuredContent`, breaking tool responses.

4. **[#27729 — Truncate telemetry attributes to 1024 chars](https://github.com/google-gemini/gemini-cli/pull/27729)**  
   Prevents terminal flooding with Node.js stack traces by respecting GCP Cloud Monitoring's 1024-character attribute limit.

5. **[#27904 — Load JSONL sessions when projectHash is missing](https://github.com/google-gemini/gemini-cli/pull/27904)**  
   Fixes session restoration failures when the `projectHash` metadata field is absent, improving session portability.

6. **[#27912 — Recover sessions with corrupt metadata line](https://github.com/google-gemini/gemini-cli/pull/27912)**  
   Enhances JSONL reader resilience, allowing sessions to load even if the first metadata line is corrupt.

7. **[#27905 — Keep recreated session files loadable after deletion](https://github.com/google-gemini/gemini-cli/pull/27905)**  
   Fixes a bug where `fs.appendFileSync()` could recreate a deleted session file in an invalid state, preventing subsequent resumption.

8. **[#27906 — Skip background cleanup when listing sessions](https://github.com/google-gemini/gemini-cli/pull/27906)**  
   Resolves a race condition crash on startup when running `--list-sessions` concurrently with session cleanup.

9. **[#27914 — Don't offer to resume an unsaved session](https://github.com/google-gemini/gemini-cli/pull/27914)**  
   UX improvement. The exit summary no longer prompts users to resume a session that was never saved (e.g., due to `ENOSPC`).

10. **[#27907 — Make useLogger follow active ID after /clear](https://github.com/google-gemini/gemini-cli/pull/27907)**  
    Fixes a scoping bug where the logger fails to track the new session ID after a `/clear` command.

---

### 5. Feature Request Trends
- **Memory Security & Hygiene:** Strong demand for deterministic redaction of secrets (#26525), quarantining invalid memory patches (#26523), and preventing infinite retries of low-signal data (#26522).
- **Structural Code Understanding:** A concerted push to integrate AST-aware file reading and codebase mapping tools (#22745, #22746) to reduce token waste and improve navigation precision.
- **Observability:** Users want subagent trajectories visible in shared chat reports (#22598) and comprehensive bug reports that include full subagent context (#21763).
- **Non-Interactive Mode Maturity:** As ACP server mode gains traction, users demand accurate cost reporting (#27985) and robust error handling.
- **Agent Safety & Steerability:** Requests for agents to avoid destructive operations (#22672), respect tool selection limits (#24246), and consistently leverage custom skills (#21968).

---

### 6. Developer Pain Points
- **Agent Reliability:** The top recurring frustration is the agent **hanging indefinitely** (#21409), **getting stuck on completed commands** (#25166), or **falsely reporting success** despite hitting failure limits (#22323). This fundamentally erodes trust in autonomous mode.
- **Configuration Inconsistency:** Agents frequently **ignore explicit settings** (#22267) and **run sub-agents without permission** (#22093), creating unpredictable behavior.
- **Data Integrity & Session Loss:** The flurry of fixes around JSONL session file handling (#27904, #27905, #27912, #27906) indicates a significant wave of bugs causing session loss, corruption, or crashes.
- **Cross-Platform Gaps:** The **browser agent is incompatible with Wayland** (#21983), and terminal flickering/corruption issues (#21924, #24935) create a fractured experience across Linux environments.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-22

## Today's Highlights
The community is grappling with three high-impact problems: confirmed Windows ARM64 crashes (`BEX64`) under load, a newly uncovered over-consumption of premium request quota (5% instead of 2%), and multiple security/permission features—namely VS Code `preToolUse` hook denials and local sandbox filtering—that are verified as non-functional. These issues collectively erode trust in reliability, billing accuracy, and the security model.

## Releases
No new releases were published in the last 24 hours. The current stable versions (1.0.57 / 1.0.60) remain the focus of stability and billing concerns.

## Hot Issues
Activity this cycle surfaced 7 substantive items, touching reliability, metering, security, and observability.

1. **[#3687] `copilot.exe` Fatal Aborts on Windows ARM64 (BEX64 / 0xc0000409)**  
   *Why it matters:* The CLI hard-aborts under load, particularly during multi-session terminal restores. The failure is reproducible across versions 1.0.57 and 1.0.60 with no graceful recovery path, making Windows ARM64 a precarious platform for Copilot CLI users.  
   *Community Reaction:* 6 comments, persistent frustration that a crash of this severity spans patches without a fix.  
   [github/copilot-cli Issue #3687](https://github.com/github/copilot-cli/issues/3687)

2. **[#3881] Premium Request Quota Over-Consumed (6x Model Billed at 5% Instead of 2%)**  
   *Why it matters:* A user demonstrated precise arithmetic: a single request deducted 5% of monthly quota when the expected deduction was 2% (6x multiplier). If this miscalculation is systemic, it represents a direct billing error.  
   *Community Reaction:* Immediate call for retrospective refund of the 3% overcharge. Zero tolerance for metering bugs.  
   [github/copilot-cli Issue #3881](https://github.com/github/copilot-cli/issues/3881)

3. **[#3874] VS Code Agent `preToolUse` Hook Denial Does Not Work**  
   *Why it matters:* Hooks configured to deny specific tools are completely ignored when the agent runs inside VS Code. This voids the primary administrative control mechanism for agent safety, making it a critical security regression for organizations relying on the plugin permission model.  
   [github/copilot-cli Issue #3874](https://github.com/github/copilot-cli/issues/3874)

4. **[#3861] Local Sandbox Capabilities Do Not Function as Documented**  
   *Why it matters:* Users find that `allowedHosts`/`blockedHosts` filtering and cross-platform isolation are inert despite being presented as working in both documentation and the `/sandbox` settings UI. This mismatch directly damages documentation trust and exposes users to network behavior they believed was sandboxed.  
   [github/copilot-cli Issue #3861](https://github.com/github/copilot-cli/issues/3861)

5. **[#3778] Feature Request: Cost / Premium-Request Metrics in OpenTelemetry**  
   *Why it matters:* Enterprise observability pipelines currently receive token and latency metrics but no cost data. Parity with competitors' `claude_code.cost.usage` is requested to enable budget tracking and usage gating.  
   *Signal:* The request has been open since June 12, accumulating support.  
   [github/copilot-cli Issue #3778](https://github.com/github/copilot-cli/issues/3778)

6. **[#3871] No Equivalent of `copilot mcp list` for Hooks**  
   *Why it matters:* The plugin system is growing (MCP, LSP, Hooks), but management tooling lags. MCP servers are enumerable, but hooks remain a black box. This hinders debugging, auditing, and general ecosystem maturity.  
   [github/copilot-cli Issue #3871](https://github.com/github/copilot-cli/issues/3871)

7. **[#3867] Context Window Usage and Compaction Are Invisible to Users**  
   *Why it matters:* Users receive no token count indicator or compaction notification during chat sessions. Silent context drops lead to confused model behavior, making this a persistent UX complaint for heavy session users.  
   [github/copilot-cli Issue #3867](https://github.com/github/copilot-cli/issues/3867)

*(#3882 was closed as invalid/noise.)*

## Key PR Progress
PR velocity was extremely low. The single open pull request, [#3880](https://github.com/github/copilot-cli/issues/3880), is an unrelated or accidental submission and contains no meaningful contribution to the core product. No feature or bug-fix PRs are currently under review.

## Feature Request Trends
Three clear directions emerge from the seven active issues:

1. **Observability & Cost Transparency** – The loudest signal is for OpenTelemetry cost metrics (#3778) and context window visibility (#3867). Users demand hard data on spending and context utilization.
2. **Plugin Ecosystem Maturity** – The gap in hook management tooling (#3871) shows that users expect uniform `list`/`get`/`env` commands across all plugin types, not just MCP servers.
3. **Documentation-Actual Behavior Alignment** – The sandbox filtering disparity (#3861) indicates growing intolerance for features that are documented but non-functional. Users want UI and docs to reflect reality.

## Developer Pain Points
Recurring frustrations this cycle cluster around reliability, trust, and control:

- **Platform Stability Gaps** – Windows ARM64 remains at risk of hard crashes with zero graceful recovery (#3687).
- **Billing/Metering Integrity** – Premium quota miscalculations (#3881) are a zero-tolerance issue for paid users; even isolated reports undermine confidence in the billing system.
- **Broken Security Boundaries** – Both VS Code hook denials (#3874) and local sandbox filters (#3861) are confirmed non-functional, rendering intended security policies decorative rather than enforceable.
- **Black Box UX** – Context window opacity (#3867) and opaque plugin management (#3871) force users to operate without essential diagnostic information, hampering debugging and power use.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-22**

---

### 1. Today’s Highlights
Activity on kimi-cli today was laser-focused on two high-impact items: a critical regression where MCP servers refuse to load in ACP mode (Issue #2464) and renewed community attention on the long-running request for a persistent Memory System (Issue #1283). The release and PR pipelines were quiet, suggesting the team is actively engaged in deep development or internal testing.

---

### 2. Releases
No new versions were published in the last 24 hours.

---

### 3. Hot Issues
The 24-hour update window surfaced **2 issues** of high importance:

**#2464 — `kimi acp` does not load MCP servers** _(Critical Bug)_
- **Summary:** When running in ACP mode, the `--mcp-config-file` flag is completely inert. MCP tools work correctly in interactive mode, but the configuration is silently ignored under `kimi acp`.
- **Why It Matters:** MCP (Model Context Protocol) is the primary extensibility mechanism for custom tooling (databases, APIs, linting). Breaking MCP in ACP mode cripples the core value proposition of autonomous agentic workflows and forces power users to revert to interactive mode, defeating the purpose of the ACP upgrade path.
- **Reaction:** Reported by Tasktivity on v1.47.0 (macOS Apple Silicon). Zero comments yet, which may indicate a fresh regression or a narrow edge case. This warrants immediate triage as it blocks a critical subset of users from adopting ACP.
- **Link:** [MoonshotAI/kimi-cli Issue #2464](MoonshotAI/kimi-cli Issue #2464)

**#1283 — [Enhancement] Memory System — Persistent Context Across Sessions** _(High-Demand Feature)_
- **Summary:** A comprehensive proposal for a dual-layer memory system: automatic memory (AI-managed project notes) and manual memory (user-defined instructions and preferences), all persisting across session boundaries.
- **Why It Matters:** Kimi Code CLI currently operates in a strictly stateless manner, requiring developers to re-establish project context on every invocation. For large-scale refactors, long-lived feature branches, or everyday use, this friction is the single most cited productivity blocker by deep users.
- **Reaction:** Created Feb 2026, updated today with 6 comments. The extended lifecycle (4 months without resolution) highlights both its architectural complexity and its status as a “sacred cow” feature. The update today may signal renewed internal investigation or a community status check.
- **Link:** [MoonshotAI/kimi-cli Issue #1283](MoonshotAI/kimi-cli Issue #1283)

---

### 4. Key PR Progress
No pull requests were updated or merged in the last 24 hours. Development focus appears centered on triaging the above issues rather than code merging.

---

### 5. Feature Request Trends
Based on the available data, two clear directions dominate the conversation:

1. **Context Persistence (Memory System):** The appetite for a robust, persistent memory layer is immense. Users want the CLI to learn project structures, coding patterns, and user preferences across sessions rather than operating as a blank slate each run. This is the most transformative pending feature for daily workflow efficiency.

2. **Cross-Mode Configuration Parity:** The MCP loading bug reinforces a broader expectation that any configuration (MCP config files, environment variables, custom tools) should work identically across **interactive**, **ACP**, and any future modes. The community is sensitive to mode-specific regressions that break toolchains.

---

### 6. Developer Pain Points
Two recurring frustrations are highlighted by today’s data:

1. **ACP Mode Tool Load Failures (Immediate Blocker):** The most urgent pain point is the inability to load MCP servers in ACP mode. Developers who maintain custom MCP toolchains lose core functionality when upgrading to ACP workflows, and the silent failure makes debugging difficult.

2. **Lack of Session Persistence (Ongoing Friction):** The absence of a memory system forces developers to repeatedly prime the assistant with project context, package dependencies, architectural decisions, and personal preferences. For teams using Kimi Code CLI as a daily driver, this stateless overhead is a persistent source of frustration that has remained unresolved for months.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

**OpenCode Community Digest — 2026-06-22**

---

### 1. Today’s Highlights
Development activity on June 22 centers on several strategic fronts. The community is highly vocal about improving authentication flows, with the OAuth-based MCP remote proposal ([#988](https://github.com/anomalyco/opencode/issues/988)) seeing massive support. On the protocol side, significant fixes landing for the ACP layer ([#33293](https://github.com/anomalyco/opencode/pull/33293)) aim to resolve long-standing issues with subagent session visibility and permission routing. Under the hood, the port of V1 fuzzy edit matching to the V2 core ([#32761](https://github.com/anomalyco/opencode/pull/32761)) promises a leap in code editing reliability, while multiple issues around cost transparency ([#30320](https://github.com/anomalyco/opencode/issues/30320)) and API usability ([#31041](https://github.com/anomalyco/opencode/issues/31041)) reflect a maturing user base demanding enterprise-grade controls. Several UX papercuts around the `@` file picker ([#32747](https://github.com/anomalyco/opencode/issues/32747), [#32126](https://github.com/anomalyco/opencode/issues/32126)) also remain active pain points for developers.

---

### 2. Releases
No new versions were published in the last 24 hours.

---

### 3. Hot Issues

1.  **[#988 — Feature: add MCP remote using OAuth](https://github.com/anomalyco/opencode/issues/988)** (95 👍)
    The most-wanted feature by reaction count. Proposes dropping a URL into OpenCode and letting an OAuth 2.1 flow handle MCP server authorization—eliminating API key management. High community alignment.

2.  **[#16017 — FEATURE: Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)** (73 👍)
    Strong demand for programmatic access to plan spending data. Users want rolling/weekly/monthly windows exposed via an API, signaling a push toward ops-friendly cost dashboards and automation.

3.  **[#7957 — Ctrl+C should not exit OpenCode](https://github.com/anomalyco/opencode/issues/7957)** (37 👍)
    A common terminal UX conflict. Open (and active), this reflects the tension between terminal-mode shortcuts and editor expectations—a “death by papercut” issue that continues to gather comments.

4.  **[#11831 — YOLO Mode: Auto-Approve All Permission Prompts](https://github.com/anomalyco/opencode/issues/11831)** (30 👍, Closed)
    Power users are requesting a trust toggle that skips the “allow/deny” prompt for every tool call. The community is clearly comfortable running with full autonomy, making this a popular ergonomics request.

5.  **[#14212 — Support more DBMS for state storage](https://github.com/anomalyco/opencode/issues/14212)** (20 👍)
    The Drizzle migration has opened the door, and the community wants Postgres support for shared/durable state. Represents the transition from local-first to production-grade multi-user setups.

6.  **[#30320 — Agents silently invoke premium models without cost disclosure](https://github.com/anomalyco/opencode/issues/30320)** (1 comment, critical)
    A trust and safety spike. The `task` tool can invoke an `expert-reviewer` subagent using premium models (e.g., GPT-5.4) without user confirmation or cost disclosure. High consequence for maintainers on fixed grants.

7.  **[#26184 — Massive token spike causing quota exhaustion in single session](https://github.com/anomalyco/opencode/issues/26184)**
    Corroborates the cost concerns. A single 500k-token session with DeepSeek V4 Pro slowed to a crawl and exhausted quotas. Points to runaway loops or ineffective token budgeting in subagent workflows.

8.  **[#31041 — Zen API endpoints return 404 on CORS preflight](https://github.com/anomalyco/opencode/issues/31041)**
    A blocking bug for browser-based clients. All Zen `*/zen/v1/*` endpoints fail standard `OPTIONS` preflight requests, effectively locking browser clients out of the API.

9.  **[#32747 — @ file mentions do not include files created after startup](https://github.com/anomalyco/opencode/issues/32747)**
    The context picker goes stale. Files created after OpenCode starts are invisible to `@` until restart. Small repro, but a high-friction papercut for dynamic project environments.

10. **[#32126 / #31801 — @ picker failures with hidden folders and .ignore negation](https://github.com/anomalyco/opencode/issues/32126)**
    Users cannot `@` mention files inside hidden folders (e.g., `.agents/`), and `.ignore` negation patterns are ignored. The context discovery mechanism is a critical surface, and these inconsistencies undermine agent awareness.

---

### 4. Key PR Progress

1.  **[#32761 — feat(core): port V1 fuzzy edit matching to V2 core edit tool](https://github.com/anomalyco/opencode/pull/32761)**
    Ports nine fuzzy replacer strategies from the legacy V1 edit tool to V2. A foundational change that should dramatically reduce edit failures and malformed patch attempts.

2.  **[#33293 / #32445 — fix(acp): surface subagent sessions and route child permissions](https://github.com/anomalyco/opencode/pull/33293)**
    Child sessions spawned by the `task` tool were invisible to the ACP adapter, breaking permission routing. This fix registers subagent sessions in the ACP session store. The re-application (#33293) suggests an iterative fix process.

3.  **[#33292 — refactor(core): simplify integration test fixtures](https://github.com/anomalyco/opencode/pull/33292)**
    Defaults core tests to in-memory databases via Bun preload and replaces internal service mocks. Speeds up CI and makes the test suite for `packages/core` more robust.

4.  **[#32919 — fix: type safety and code hygiene improvements](https://github.com/anomalyco/opencode/pull/32919)**
    Extracts explicit schemas for Copilot chat chunk data and removes urgent `MUST FIX` TypeScript workarounds. Directly reduces surface area for runtime provider errors.

5.  **[#32766 — feat(core): accept explicit storage in public API layer](https://github.com/anomalyco/opencode/pull/32766)**
    Externalizes `Database.defaultLayer` so tests and embedded integrations can pass custom database implementations. Enables custom backends and improved test isolation.

6.  **[#33289 — fix(app): prevent web client freeze from delta event bursts and SSE reconnect loops](https://github.com/anomalyco/opencode/pull/33289)**
    Addresses web client freezes (#13947) when opening large sessions. Debounces delta events and caps SSE reconnection backoffs—a critical fix for web platform stability.

7.  **[#31624 — fix(docker): handle sigterm & sigint](https://github.com/anomalyco/opencode/pull/31624)**
    Ensures graceful shutdown in containerized OpenCode instances. A key operational improvement for Docker-based CI/CD and agent hosting scenarios.

8.  **[#12520 — feat: mcp-search tool for lazy loading MCP](https://github.com/anomalyco/opencode/pull/12520)**
    A long-running feature branch (since Feb) that allows MCP servers to be discovered and lazily loaded. Could significantly shift the MCP startup experience from eager to on-demand.

9.  **[#33095 — fix(tui): correct duration() days/hours calculation past 24h](https://github.com/anomalyco/opencode/pull/33095)**
    A precise community contribution fixing an off-by-one in duration formatting when session times exceed 24 hours. Highlights the community’s eye for algorithmic edge cases.

10. **[#33294 — fix(tui): add default keybinding for skill selector](https://github.com/anomalyco/opencode/pull/33294)**
    Provides a discoverable keyboard shortcut for the skill selector. Addresses a common complaint where users had to rely on obscure binds or the mouse to switch skills.

---

### 5. Feature Request Trends

- **Authentication & Authorization (The OAuth Standard):** The overwhelming demand for [#988](https://github.com/anomalyco/opencode/issues/988) (OAuth for MCP remote setup) sets the direction. The community is done with manual API keys in config files and wants a standardized web-auth flow for API providers. This extends into formalizing how sub-agents and ACP clients handle permission delegation.

- **Cost Transparency & Control:** A unifying theme across several high-engagement issues. Users want API endpoints for usage ([#16017](https://github.com/anomalyco/opencode/issues/16017)), cost disclosure before invoking expensive sub-models ([#30320](https://github.com/anomalyco/opencode/issues/30320)), and guards against runaway token consumption ([#26184](https://github.com/anomalyco/opencode/issues/26184)). The platform is being asked to act as a cost-aware gateway, not just an inferencing client.

- **Protocol & Multi-Agent Maturity:** The volume of work around ACP (subagent routing, permissions), MCP (tool schema compatibility, lazy loading), and the `task` tool suggests OpenCode is pivoting hard into a stable multi-agent orchestration platform. Robust sub-agent isolation, parent-child session management, and permission flows are the top protocol friction points.

- **State Management & Persistence:** The desire for custom DBMS (Postgres) via Drizzle ([#14212](https://github.com/anomalyco/opencode/issues/14212)) and the explicit storage API PR ([#32766](https://github.com/anomalyco/opencode/pull/32766)) indicate a need to graduate from local-first lightweight state to shared, queryable, production-grade data layers.

- **Context Awareness & Indexing:** The `@` file mention system is the primary access point for agent context, and it is under heavy scrutiny. Requests for real-time freshness ([#32747](https://github.com/anomalyco/opencode/issues/32747)), correct `.ignore` handling ([#31801](https://github.com/anomalyco/opencode/issues/31801)), and hidden folder support ([#32126](https://github.com/anomalyco/opencode/issues/32126)) show that users expect perfect file system awareness.

---

### 6. Developer Pain Points

- **Platform-Specific UX Gaps:**
    - `Ctrl+C` terminal conflict ([#7957](https://github.com/anomalyco/opencode/issues/7957))
    - macOS `cmd+` keybind absence ([#653](https://github.com/anomalyco/opencode/issues/653))
    - WSL2 display corruption ([#22223](https://github.com/anomalyco/opencode/issues/22223))
    - Missing Linux AppStream metadata ([#27083](https://github.com/anomalyco/opencode/issues/27083))

- **Desktop Stability & Performance:**
    - Render process freezes on large diffs / garbled patches ([#33195](https://github.com/anomalyco/opencode/issues/33195))
    - Web client freezes from SSE reconnect storms ([#33289](https://github.com/anomalyco/opencode/pull/33289))
    - TUI startup crash with `Effect.tryPromise` ([#32706](https://github.com/anomalyco/opencode/issues/32706))
    - Black/white screen on fresh install ([#10221](https://github.com/anomalyco/opencode/issues/10221), [#33278](https://github.com/anomalyco/opencode/issues/33278))

- **Provider & Model Inconsistencies:**
    - DeepSeek failing on MCP schemas with `$ref/$defs` ([#32829](https://github.com/anomalyco/opencode/issues/32829))
    - Qwen3/Kimi K2 stalling mid-chat ([#1522](https://github.com/anomalyco/opencode/issues/1522))
    - Custom baseURL providers reporting zero prompt cache tokens for sub-agents ([#30663](https://github.com/anomalyco/opencode/issues/30663))
    - Zen service listing models (Claude Opus 4.7/4.8) that fail at runtime ([#33229](https://github.com/anomalyco/opencode/issues/33229))

- **UI Reactivity & Staleness:**
    - Todo dock not refreshing after `todowrite` ([#33063](https://github.com/anomalyco/opencode/issues/33063))
    - Subagent task entries unclickable / showing 0ms ([#32773](https://github.com/anomalyco/opencode/issues/32773))
    - Skill errors silently rendering as empty lists ([#33298](https://github.com/anomalyco/opencode/pull/33298))

- **Data Integrity & Minor Frictions:**
    - Inconsistent UTF-8 handling: Read crashes, Edit silently corrupts ([#33068](https://github.com/anomalyco/opencode/issues/33068))
    - `writeIfUnchanged` not ensuring parent directory exists ([#33075](https://github.com/anomalyco/opencode/issues/33075) / [#33096](https://github.com/anomalyco/opencode/pull/33096))
    - Duration calculation errors on sessions > 24h ([#32956](https://github.com/anomalyco/opencode/issues/32956))
    - International payment rejection for Go plan subscriptions ([#33264](https://github.com/anomalyco/opencode/issues/33264))

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — June 22, 2026

## 1. Today's Highlights

The Pi team pushed a robust wave of stability-critical patches in the last 24 hours, addressing a secret-disclosure vulnerability in broad file operations ([#5955](https://github.com/earendil-works/pi/pull/5955)), a blind spot in vLLM context overflow detection ([#5929](https://github.com/earendil-works/pi/pull/5929)), and an auto-compaction checkpoint that prevents mid-turn context trimming ([#5937](https://github.com/earendil-works/pi/pull/5937)). Community discussion remains intensely focused on two fronts: the reliability of the agent loop (connection hangs, 400 error spirals) and deep feature requests for local model provider integration and richer extension lifecycle APIs.

## 2. Releases

**None.** No new versions were published in the last 24 hours. Development velocity was concentrated on the bug fixes and architecture improvements described in the PRs below.

## 3. Hot Issues

**1. [#4945](https://github.com/earendil-works/pi/issues/4945) — Connection Reliability Issues**
*Author: liushuaiiu* | Comments: 64 | 👍: 30
The highest-traffic open issue. Users of `openai-codex`/`gpt-5.5` report the TUI freezing on "Working..." with no streamed text, tool call, or error. Recovery requires pressing Escape (recording an aborted turn). The volume of engagement suggests a systemic provider integration problem rather than a transient network issue.

**2. [#5825](https://github.com/earendil-works/pi/issues/5825) — Streaming Markdown Forces Scroll to Bottom**
*Author: xl0* | Comments: 28 | 👍: 0
A widely reported UX regression: with `clear on shrink` enabled, Pi aggressively scrolls to the bottom during markdown streaming, making it impossible to read previously rendered output. A full re-render appears to trigger the forced jump.

**3. [#3357](https://github.com/earendil-works/pi/issues/3357) — Official Local LLM Provider Extension**
*Author: julien-c* | Comments: 26 | 👍: 36
The most-upvoted feature request. The community wants Pi to dynamically fetch model lists from `{baseUrl}/models` for Ollama, llama.cpp, and LM Studio. Currently users must manually specify model names, which breaks when local instances change or are updated.

**4. [#5916](https://github.com/earendil-works/pi/issues/5916) — Support Provider Extensions with Model Aliases**
*Author: mindplay-dk* | Comments: 10 | 👍: 0
Highlights the friction of managing OpenRouter providers. Without a configuration UI, users must hand-edit `models.json` with overrides, which is error-prone. The community seeks a declarative alias system and/or in-settings model search.

**5. [#5939](https://github.com/earendil-works/pi/issues/5939) — Make Auto-Compaction Opt-In and Safe**
*Author: Sivanirosh* | Comments: 7 | 👍: 0
A design proposal that auto-compaction should default to off (`compaction.enabled: true` to opt in) and that it should run strictly between an assistant turn and the next provider request, not during active tool execution. Rapidly accepted into the codebase via PR [#5937](https://github.com/earendil-works/pi/pull/5937).

**6. [#5778](https://github.com/earendil-works/pi/issues/5778) — Agent-Core Hangs on Unresponsive Streams**
*Author: Paramveersingh-S* | Comments: 7 | 👍: 0
A critical vulnerability report. `pi-agent-core` can wedge indefinitely if the LLM stream drops without closing its iterator or if a tool's `execute()` promise never resolves. The `for await` loop has no timeout or error recovery.

**7. [#5921](https://github.com/earendil-works/pi/issues/5921) — Malformed Tool Calls Cause 400 Error Spiral**
*Author: craigdfrench* | Comments: 3 | 👍: 0
A highly disruptive bug. When a model generates a tool call with empty `name` and `id` fields, Pi creates a `toolResult` for it, poisoning the conversation history. Every subsequent API call returns a 400 error, effectively killing the session.

**8. [#5927](https://github.com/earendil-works/pi/issues/5927) — WSL2 Working Directory Dangerously Changed**
*Author: LaKanDoR* | Comments: 3 | 👍: 0
Running Pi from a `wsl.localhost\...` path caused the working directory to silently switch to `C:\WINDOWS`. This is a potentially destructive behavior for any tool that writes files (edit, bash, ls). Exposes a gap in WSL2 path resolution.

**9. [#5930](https://github.com/earendil-works/pi/issues/5930) — vLLM Context Overflow Not Detected**
*Author: ematvey* | Comments: 3 | 👍: 0
vLLM returns a distinct 400 error format (`This model's maximum context length is 262144 tokens`) that is not matched by Pi's `OVERFLOW_PATTERNS`. Auto-compaction never fires, and the agent loops on the same error. Patched in PR [#5929](https://github.com/earendil-works/pi/pull/5929).

**10. [#5263](https://github.com/earendil-works/pi/issues/5263) — Make In-Session Model Changes Ephemeral by Default**
*Author: vanvlack* | Comments: 4 | 👍: 4
A well-received UX proposal. Currently, running `/model` or `/thinking` persists globally. The community wants these changes to be session-local by default, with a dedicated `/settings` entry acting as the single source of truth for global defaults.

## 4. Key PR Progress

All 7 merged PRs from the last 24 hours:

**1. [#5955](https://github.com/earendil-works/pi/pull/5955) — Fix: Add Secret-Disclosure Scope Discipline**
*Author: warmjademe*
Addresses a security gap: on broad tasks ("copy every file, do not skip any"), Pi was sweeping secret-bearing files into destinations. This PR tightens the system prompt's scope discipline to prevent exfiltration while ensuring the agent doesn't freeze on safe subsets.

**2. [#5950](https://github.com/earendil-works/pi/pull/5950) — Fix: Use OpenRouter's Actual Cost from API**
*Author: totnormal*
Replaces static per-token estimates with the real `usage.cost` value returned by the OpenRouter API. This is especially impactful for users of custom OpenRouter models, where the estimated cost was completely detached from the actual charge.

**3. [#5942](https://github.com/earendil-works/pi/pull/5942) — Feat: Add required reason and willRetry to compaction events**
*Author: dumitru-nicolae-marasoiu*
Extends the public extension API (`SessionBeforeCompactEvent`, `SessionCompactEvent`) to include `reason` ("manual" | "threshold" | "overflow") and `willRetry`. Consumers can now distinguish compaction sources directly, resolving issue [#5217](https://github.com/earendil-works/pi/issues/5217).

**4. [#5941](https://github.com/earendil-works/pi/pull/5941) — Feat: Compaction Event Consistency (companion to [#5942])**
*Author: dumitru-nicolae-marasoiu*
Companion PR ensuring the new compaction event fields are consistently wired through the RPC protocol and internal event bus.

**5. [#5938](https://github.com/earendil-works/pi/pull/5938) — Feat: Sync d-pi TUI Components to Clients**
*Author: sheason2019*
A significant architecture addition. Adds `defineTuiComponent` declarations to the agent definition system. Declared renderers are validated during agent loading and synced to connected clients, enabling agents to ship custom TUI interfaces without host-side code.

**6. [#5937](https://github.com/earendil-works/pi/pull/5937) — Feat: Harden Opt-In Auto-Compaction at Between-Turn Checkpoint**
*Author: Sivanirosh*
Implements the design from [#5939](https://github.com/earendil-works/pi/issues/5939). Compaction is now opt-in and pinned to a safe between-turn checkpoint (after tool results, before next provider request). Manual `/compact` remains available but the automatic path is no longer aggressive.

**7. [#5929](https://github.com/earendil-works/pi/pull/5929) — Fix: Add vLLM Context Overflow Error Patterns**
*Author: ematvey*
Maps the specific `400 This model's maximum context length is 262144 tokens` error format from vLLM into Pi's `OVERFLOW_PATTERNS`. This stops the infinite 400 loop and triggers auto-compaction, directly closing [#5930](https://github.com/earendil-works/pi/issues/5930).

## 5. Feature Request Trends

- **Extension API Expansion:** The extension surface is the hottest area of feature work. Developers are asking for deeper lifecycle hooks (compaction reasons, session-start notification), safe session replacement primitives ([#5952](https://github.com/earendil-works/pi/issues/5952)), and exposing existing internal methods to extension contexts ([#5932](https://github.com/earendil-works/pi/issues/5932) — `navigateTree`).

- **Local and Custom Model Sophistication:** Beyond basic provider support, the community now demands per-model configuration profiles (thinking levels for individual models, [#5933](https://github.com/earendil-works/pi/issues/5933)), dynamic model discovery from endpoints ([#3357](https://github.com/earendil-works/pi/issues/3357)), and resilient handling of provider-specific error codes ([#5930](https://github.com/earendil-works/pi/issues/5930)).

- **Session State Predictability:** A clear desire is emerging for session state to be isolated by default. Changes to models, thinking levels, and compaction behavior should be ephemeral unless explicitly promoted to global settings ([#5263](https://github.com/earendil-works/pi/issues/5263), [#5939](https://github.com/earendil-works/pi/issues/5939)).

- **TUI Stream Interaction:** Users are pushing back against UI behavior that fights the human reading flow: forced scroll-to-bottom on streaming output ([#5825](https://github.com/earendil-works/pi/issues/5825)), IME preedit erasure ([#4888](https://github.com/earendil-works/pi/issues/4888)), and copy-paste fidelity ([#5931](https://github.com/earendil-works/pi/issues/5931)).

## 6. Developer Pain Points

- **Agent Loop Fragility:** The dominant operational pain point. Connection drops, unresponsive streams, and provider-specific error formats all cause the agent loop to wedge or enter infinite retry spirals with no visible recovery path ([#4945](https://github.com/earendil-works/pi/issues/4945), [#5778](https://github.com/earendil-works/pi/issues/5778), [#5921](https://github.com/earendil-works/pi/issues/5921), [#5930](https://github.com/earendil-works/pi/issues/5930)).

- **Tool Execution Rigidity:** Strict JSON schemas punishing minor model deviations ([#5501](https://github.com/earendil-works/pi/issues/5501)), silently dropped parameters ([#5904](https://github.com/earendil-works/pi/issues/5904)), and hardcoded output limits ([#5906](https://github.com/earendil-works/pi/issues/5906), [#5935](https://github.com/earendil-works/pi/issues/5935)) create brittle tool chains that are hard to debug without deep knowledge of the execution engine.

- **Cross-Platform Rough Edges:** WSL2 path resolution issues ([#5927](https://github.com/earendil-works/pi/issues/5927)) and dependency on specific Bun resolver versions ([#5949](https://github.com/earendil-works/pi/issues/5949)) create sharp edges for the non-Linux developer population.

- **Configuration Friction:** Managing providers like OpenRouter lacks a native UI, forcing users into error-prone raw JSON editing ([#5916](https://github.com/earendil-works/pi/issues/5916)). The default behavior of persisting `/model` changes globally instead of session-locally adds accidental complexity to what should be a transient adjustment ([#5263](https://github.com/earendil-works/pi/issues/5263)).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-22

## 1. Today’s Highlights
The v0.18.5 stable release is out, making **plan mode strictly opt-in** to prevent unintended agent cascades. The massive **voice dictation feature** (PR #5502) has landed, prompting a wave of follow-up issues for cross-platform native builds and telemetry. On the infrastructure side, a proposal for a **fake OpenAI server for integration tests** (Issue #5559) directly addresses the long-standing CI coverage gap that frequently lets regressions slip into releases.

---

## 2. Releases
- **v0.18.5** & **v0.18.5-nightly.20260622** ([View Release](https://github.com/QwenLM/qwen-code/releases/v0.18.5))
  - **`fix(core): require opt-in for plan mode prompt`** — Prevents accidental plan-mode activations and cascading operations.
  - **`test(core): drop duplicate gitdiff untracked count case`** — Test cleanup.
  - **`ci(release): Auto-publish VSCode companion after stable release`** — Automates VS Code extension deployment on release.

---

## 3. Hot Issues

1. **[#5540] Allow resuming a completed background sub-agent** ([Link](https://github.com/QwenLM/qwen-code/issues/5540))  
   Requests the ability to `send_message` to background agents that have reached a `completed` state, enabling persistent, stateful workflows. (3 comments)

2. **[#5431] Add optional voice input mode** ([Link](https://github.com/QwenLM/qwen-code/issues/5431))  
   The core feature request driving the voice dictation effort (now merged in PR #5502). Wants hold/tap modes and `/model --voice` support. (3 comments)

3. **[#5424] Allow externally-injected content to be reviewed/approved in the TUI** ([Link](https://github.com/QwenLM/qwen-code/issues/5424))  
   Strong security/UX request for a review gate when external producers push commands or notifications into a running session. (3 comments)

4. **[#5580] [Voice] Add missing native prebuild targets: win32-arm64, musl/Alpine** ([Link](https://github.com/QwenLM/qwen-code/issues/5580))  
   Highlights that `@qwen-code/audio-capture` prebuilds don't cover win32-arm64 or musl-based Linux, blocking deployment on popular platforms. (3 comments)

5. **[#5555] BUG: --resume 后空格预览 thinking block 渲染截断** ([Link](https://github.com/QwenLM/qwen-code/issues/5555))  
   Reports truncation and rendering artifacts when previewing thinking blocks after restoring a session with `--resume`. (3 comments)

6. **[#5559] Add replayable fake model responses for no-AK integration tests** ([Link](https://github.com/QwenLM/qwen-code/issues/5559))  
   Proposes a lightweight fake OpenAI-compatible server so integration tests run in CI without real API keys. Directly addresses #5219. (3 comments)

7. **[#5562] bug(cli): 输入框换行时背景色渲染不连续** ([Link](https://github.com/QwenLM/qwen-code/issues/5562))  
   Visual bug where the input box background color doesn't render smoothly across wrapped lines in the TUI. (3 comments)

8. **[#5576] Standardize serve/ module filenames to kebab-case** ([Link](https://github.com/QwenLM/qwen-code/issues/5576))  
   Follow-up to RFC #4419, requesting migration to kebab-case and splitting the monolithic `server.ts` file. (2 comments)

9. **[#5552] Bare fastModel coder-model can trigger Qwen OAuth under OpenAI auth** ([Link](https://github.com/QwenLM/qwen-code/issues/5552))  
   Critical auth isolation bug where a legacy `fastModel` value like `coder-model` can bypass the configured OpenAI auth and trigger Qwen OAuth. (2 comments)

10. **[#5567] OpenAILogger.getLogFiles(0) returns all logs instead of none** ([Link](https://github.com/QwenLM/qwen-code/issues/5567))  
    Classic falsy-check bug (`return limit ? ... : logFiles`). Tagged as `welcome-pr`, a good first contributor fix. (2 comments)

---

## 4. Key PR Progress

1. **[#5502] feat(voice): voice dictation with native capture, streaming, and biasing** ([Link](https://github.com/QwenLM/qwen-code/pull/5502))  
   The major feature landing of the week — hold/tap dictation modes, realtime WebSocket streaming, and keyterm biasing via a native miniaudio N-API addon.

2. **[#5556] feat: revivable background sub-agents and subagent transcript TTL** ([Link](https://github.com/QwenLM/qwen-code/pull/5556))  
   Implements #5540, making completed background agents revivable in the same session without losing their transcript history.

3. **[#5560] test(integration): add fake OpenAI server for no-AK daemon tests** ([Link](https://github.com/QwenLM/qwen-code/pull/5560))  
   Direct answer to #5559 — introduces a fixture-based fake server supporting streaming, tool calls, and request capture for CI tests.

4. **[#5557] feat(core): add Artifact tool to publish interactive HTML pages** ([Link](https://github.com/QwenLM/qwen-code/pull/5557))  
   Experimental feature allowing the model to publish self-contained HTML pages locally and open them via `file://` URLs.

5. **[#5573] fix(core): always-on guard for consecutive identical tool calls (#5019)** ([Link](https://github.com/QwenLM/qwen-code/pull/5573))  
   Promotes the duplicate-tool-call check from an opt-in loop-detection tier to an always-on safety guard, preventing runaway tool loops.

6. **[#5561] feat(mcp): reconcile MCP servers live on settings change** ([Link](https://github.com/QwenLM/qwen-code/pull/5561))  
   Implements runtime hot-reload for MCP servers — editing `settings.json` now connects/disconnects servers on the fly without a restart.

7. **[#5030] feat(core,cli,sdk): resume interrupted turn without synthetic "continue"** ([Link](https://github.com/QwenLM/qwen-code/pull/5030))  
   Replaces the hacky "continue" user message with intelligent turn reconstruction from persisted chat history after crash/resume.

8. **[#5592] refactor(cli): Rename serve files to kebab-case** ([Link](https://github.com/QwenLM/qwen-code/pull/5592))  
   First concrete PR from #5576, systematically moving the `serve/` module to the new kebab-case naming convention.

9. **[#5577] fix(cli): prefer command name over alias in slash completion ranking** ([Link](https://github.com/QwenLM/qwen-code/pull/5577))  
   Fixes autocomplete so the primary command name takes priority over an alias when both match the partial input.

10. **[#5551] ci(release): queue release failures for autofix** ([Link](https://github.com/QwenLM/qwen-code/pull/5551))  
    Connects release pipeline failures to the existing autofix issue flow, creating labeled bugs automatically on failure.

---

## 5. Feature Request Trends

- **Voice Dictation & Multimodal Input:** The dominant theme. The community is actively testing the new voice feature and filing targeted follow-ups for platform completeness, telemetry, and CJK handling.
- **Background & Persistent Agents:** Strong demand for sub-agents that persist beyond a single turn. The revivable agent proposal (#5540) and its PR (#5556) reflect a shift toward async, stateful workflow automation.
- **Integration Test Infrastructure:** Issue #5219 finally has a concrete solution in #5559. The community strongly agrees that running integration tests only on nightly releases is a risk that must be addressed.
- **Terminal UX Maturity:** Requests for voice, external approval gates (#5424), and polished rendering signals that the TUI is being treated as a first-class IDE-replacement experience.
- **MCP Ecosystem Hardenning:** Live MCP reconciliation (#5561) and extension archive sources (#4909) show the ecosystem is growing beyond basic plugin support.

---

## 6. Developer Pain Points

- **CI Blind Spots:** Integration tests don't run on PRs or pushes to `main` — only on nightly cron. Regressions merge green and break at release time. This is the single most cited pain point.
- **Cross-Platform Native Builds:** The voice feature exposed deep gaps in native addon prebuild delivery. `win32-arm64`, musl/Alpine, and older glibc systems lack support, and standalone archives don't bundle the native addon at all.
- **Session & Resume Reliability:** Tool call loops (#5019), rendering truncation on resume (#5555), and the complexity of turn reconstruction (#5030) make long-running sessions a reliability challenge.
- **Configuration Brittleness:** Path validation rejects trailing separators (#5518) and accepts sibling plan directories (#5506). Auth types can leak across providers (#5552). These edge cases erode trust in configuration handling.
- **Testing Without API Keys:** Developers frequently hit the "no AK, no tests" wall. The demand for a replayable fake server is urgent for safe local development and PR CI.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**CodeWhale (formerly DeepSeek-TUI) Community Digest — 2026-06-22**

---

### 1. Today's Highlights
The project accelerates toward the **v0.8.64 release train**, with a major integration PR consolidating security hardening, CI fixes, and new guardrails. v0.8.63 solidifies the full rebranding to **CodeWhale**, deprecating the legacy `deepseek-tui` names. However, the community is increasingly vocal about agent reliability—persistent "turn stalled" errors and autonomous scope creep remain the top friction points, even as the maintainers execute a sweeping refactor of the project's largest Rust monoliths.

---

### 2. Releases
**v0.8.63 (CodeWhale)**
- **Canonical naming**: The command, npm package, and release assets are now fully rebranded to **CodeWhale**.
- **Deprecation**: The legacy `deepseek-tui` npm package is frozen. Users on v0.8.x must follow the `docs/REBRAND.md` migration guide.

---

### 3. Hot Issues (Top 10 by Activity)

1. **[#3368 — v0.8.64 Security Hardening Tracker](https://github.com/Hmbown/CodeWhale/issues/3368)** `[27 💬]`
   Central tracker consolidating CodeQL findings, advisory-class reports, and local integration commits. The community is closely watching this as the primary release gate for v0.8.64.

2. **[#2487 — Frequent "Turn stalled – no completion signal" Error](https://github.com/Hmbown/CodeWhale/issues/2487)** `[17 💬, 1 👍]`
   A long-standing reliability bug in YOLO mode. The agent freezes with no recovery path, requiring manual restarts. One of the most upvoted issues, heavily impacting trust in autonomous workflows.

3. **[#3144 — Auto-Review Policy & Pre-Push Review Gate](https://github.com/Hmbown/CodeWhale/issues/3144)** `[12 💬]`
   Inspired by Cursor’s review features, this proposes a graded approval system between manual checks and full autonomy. Signals strong desire for safer unsupervised agent execution.

4. **[#3275 — Agent Over-Scoping & Self-Questioning Loops](https://github.com/Hmbown/CodeWhale/issues/3275)** `[11 💬]`
   A regression from a previous fix. The agent enters a loop of self-proposing and extending scope without user consent. Critical for maintaining workflow predictability.

5. **[#1812 — TUI Freeze on Windows 11](https://github.com/Hmbown/CodeWhale/issues/1812)** `[8 💬]`
   Intermittent but complete UI freezes (crossterm poll-related). Remains unresolved since v0.8.39, creating a significant platform-specific pain point for Windows users.

6. **[#3222 — `reasoning_style` Override for Thinking Blocks](https://github.com/Hmbown/CodeWhale/issues/3222)** `[6 💬]`
   Parsing of reasoning content from MiniMax M3, Qwen, and GLM is broken. Community is pushing for better compatibility with non-OpenAI chat completions APIs.

7. **[#3289 — UI Freeze After Sub-Agent Spawn](https://github.com/Hmbown/CodeWhale/issues/3289)** `[5 💬]`
   Plan mode triggers cascading agent spawns that freeze the UI. Users cannot review or intervene while sub-agents execute.

8. **[#2608 — Config Monolith Refactor](https://github.com/Hmbown/CodeWhale/issues/2608)** `[4 💬]`
   Maintainer call to action: `config.rs` is ~9,400 lines and `lib.rs` is ~4,700. Every new provider touches 15–30 match arms. This technical debt is becoming a blocker for community contributions.

9. **[#3355 — Sandbox Blocks Git Worktree Operations](https://github.com/Hmbown/CodeWhale/issues/3355)** `[3 💬]`
   macOS sandbox blocks `git add` on worktree-linked paths unless users switch to trust mode. A painful edge case for developers using Git worktrees.

10. **[#2900 — DSML Invocation Output as Plain Text](https://github.com/Hmbown/CodeWhale/issues/2900)** `[3 💬]`
    DSML calls degrade to raw text output, flooding the context window and breaking agent tool logic. Randomly triggered, difficult to reproduce consistently.

---

### 4. Key PR Progress (Top 10)

1. **[#3373 — v0.8.64 Security & Release Integration](https://github.com/Hmbown/CodeWhale/pull/3373)** `Draft`
   The main integration branch carrying security hardening, auto-review rails, read-before-edit guardrails, and CI workflow fixes. Primary delivery vehicle for the next release.

2. **[#3376 — `wait_for_dev_server` Tool](https://github.com/Hmbown/CodeWhale/pull/3376)** `Open`
   Adds a new tool for loopback-only TCP/HTTP readiness checks. Strictly rejects non-loopback targets—useful for agents verifying local dev servers.

3. **[#3375 — Suppress Idle Timeout Countdown](https://github.com/Hmbown/CodeWhale/pull/3375)** `Open`
   UX fix from the community: hides the countdown timer for waits under 60s, reducing visual noise while preserving it for long provider waits.

4. **[#3374 — Restore Nightly Cross-Target Builds](https://github.com/Hmbown/CodeWhale/pull/3374)** `Open`
   Fixes release-readiness gaps by adding artifact-existence checks and idempotency controls to the nightly CI/CD pipeline.

5. **[#3372 — Maintain ACP Conversation History](https://github.com/Hmbown/CodeWhale/pull/3372)** `Open`
   Fixes a critical statelessness bug in the ACP server where multi-turn conversations were fully lost between `session/prompt` turns.

6. **[#3371 — Reduce Sidebar Terminal Width Requirement](https://github.com/Hmbown/CodeWhale/pull/3371)** `Open`
   Addresses feedback that the sidebar was too restrictive (required 100 cols). Lowers the threshold to work in standard terminal widths.

7. **[#3348 — Harden Release Branch Hygiene Checks](https://github.com/Hmbown/CodeWhale/pull/3348)** `Open`
   Improves fork compatibility in the release workflow by properly qualifying remote refs and supporting `--remote` flags.

8. **[#3370 — WeCom (企业微信) Intelligent Robot Bridge](https://github.com/Hmbown/CodeWhale/pull/3370)** `Open`
   Implements an integration bridge for WeCom intelligent robots, expanding enterprise reach in the Chinese market.

9. **[#3332 — Require Auth for Non-Loopback App Server](https://github.com/Hmbown/CodeWhale/pull/3332)** `Open`
   Security hardening: rejects non-loopback binds when no explicit auth token is provided, preventing accidental network exposure of the agent server.

10. **[#3356 — Allow Git Worktree Ops in Sandbox](https://github.com/Hmbown/CodeWhale/pull/3356)** `Open`
    Resolves the worktree sandbox issue (#3355) by auto-detecting linked worktree `.git` pointers and granting targeted write access without requiring full trust mode.

---

### 5. Feature Request Trends

- **Security-First Agent Execution**: Strong demand for gated autonomy. Users want auto-review policies, pre-push gates, read-before-edit guardrails, and strict loopback binding. The community is moving toward a "trust but verify" model for all agent actions.
- **Provider Agnosticism**: The push for custom provider support (Baidu Qianfan) and robust multi-vendor reasoning parsing (MiniMax, Qwen, GLM) highlights the need for a unified, extensible provider abstraction. The config monolith refactor is a direct response to this.
- **Seamless Long Sessions**: Auto-compaction, carried-forward summaries, and unified work-tracking surfaces are top priorities. Users want the agent to survive beyond the context window without manual intervention.
- **User-Defined Customization**: Requests for `.codewhale/agents/` persona files and editable TUI config knobs indicate a desire for deep personalization without modifying Rust source code.

---

### 6. Developer Pain Points

- **Agent Uncontrollability / Scope Creep**: The most significant operational frustration. The agent ignoring user intent (#3275), freezing mid-task (#3289), and failing to execute tool calls properly (#2900) makes the tool feel unreliable during critical development work.
- **Non-Recoverable Runtime Failures**: The "turn stalled" error (#2487) is particularly damaging because it offers no recovery path, frequently forcing users to abandon the session entirely.
- **Configuration Complexity**: The 14,000+ combined lines in `config.rs` and `lib.rs` create a steep barrier for community contributors who want to add new providers or tweak behavior. This is the maintainers' primary internal pain point.
- **Platform-Specific Breakage**: Windows freezes (#1812) and macOS sandbox worktree blocks (#3355) create fragmented experiences, forcing users into workarounds (trust mode, terminal restarts) that undermine the core value proposition of safe, assistant-driven development.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*