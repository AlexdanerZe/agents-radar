# AI CLI Tools Community Digest 2026-06-09

> Generated: 2026-06-09 02:49 UTC | Tools covered: 9

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

**Cross-Tool Ecosystem Analysis Report (AI CLI Developer Tools)**
**Date:** 2026-06-09
**Author:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

### 1. Ecosystem Overview

The AI CLI tool landscape is experiencing a dual tension: rapid feature parity chasing alongside a deepening trust crisis triggered by agentic failures. Gemini CLI’s catastrophic data loss incident (#27397) and Claude Code’s fabricated tool call reports (#66408) are driving a universal community demand for safety guardrails, reliable session state, and honest failure reporting. Platform incumbents (Claude, Codex, Gemini) are managing integration complexity at scale, while a highly active open-source tier (Pi, Qwen Code, OpenCode, CodeWhale) sets the pace on architectural innovation. A critical market void persists in polished Windows/WSL support, representing a high-moat opportunity for the tool that solves it. Overall, the market is shifting from "can the agent do this" to "can the agent do this safely and consistently."

---

### 2. Activity Comparison

| Tool | Status / Release | Key Issues (Community Signal) | Key PRs (Dev Velocity) | Primary Community Friction |
|---|---|---|---|---|
| **Claude Code** | Shipped **v2.1.169** (`--safe-mode`, `/cd`) | 10 Hot. Billing block #63060 (79💬) | 5 PRs | Trust crisis: fabricated tools, context loss, billing hard stops |
| **OpenAI Codex** | Shipped **rust-v0.138.0** (`/app`, image gen) | 10 Hot. Model 404 #26892 (76💬) | 10 PRs | Windows/WSL fragility, model availability mismatches |
| **Gemini CLI** | Nightly **v0.47.0** (UI polish) | 10 Hot. Data Loss incident #27397 | 10 PRs | Safety crisis: agent hangs, false GOAL success, destructive defaults |
| **Copilot CLI** | **No release** | 33 updated. Vi mode #13 (63👍) | 1 PR | UX stagnation: 8-month Vi mode gap, sub-agent hangs |
| **Kimi Code CLI** | **No release** | 4 updated. API Key removal #2442 | **0 PRs** | Migration breakdown: silent regressions in v0.11 rewrite |
| **OpenCode** | **No release** (v1.16.x series) | 10 Hot. SQLite crash #31413 | 10 PRs | DB migration instability, provider regressions |
| **Pi** | Shipped **v0.79.0** (Project Trust) | 10 Hot. Trust backlash #5514 | 10 PRs | Feature friction vs. local model performance |
| **Qwen Code** | **No release** (v0.17.1 latest) | 10 Hot. OOM on resume #4815 (P1) | 10 PRs | Parity chase vs. critical stability regressions |
| **CodeWhale** | Shipped **v0.8.54**, Dev **v0.8.55** | 10 Hot. Rebrand migration #2924 | 10 PRs | Rebrand friction, DSML rendering bugs, massive scope expansion |

**Summary:** OpenCode, Pi, Qwen Code, and CodeWhale lead raw PR velocity (10 each). Claude and Codex lead community engagement volume. Copilot and Kimi show dangerous stagnation/regression trends. Gemini is in active crisis triage.

---

### 3. Shared Feature Directions

**Agentic Safety & Trust Guardrails**
- **Drivers:** Gemini data loss (#27397), Claude fabricated calls (#66408), Pi `alwaysTrust` backlash (#5514).
- **Demands:** Default read-only modes, explicit destructive action gates, honest failure reporting (vs. false "GOAL success" in Gemini #22323), and robust undo/rewind (Pi #5521, OpenCode #5474). The community is universally demanding the agent prove caution before capability.

**Session Lifecycle & Context Integrity**
- **Drivers:** OpenCode compaction stripping AGENTS.md (#16960), Qwen OOM from unbounded tool-result growth (#4838), Claude branching/multi-window requests (#30154, #32631).
- **Demands:** Persistent session goals (OpenCode `/goal` #27167), fork/merge/tree navigation, intent-preserving compaction, mid-turn context guards, and system state rollback. The linear chat model is breaking.

**Extensibility Maturation (Hooks, MCP, Skills)**
- **Drivers:** Copilot hooks failing (#2540), Pi landing `beforeModel` hook (#5537), OpenCode paginating MCP (#31442), Claude agent skill discovery (#66352).
- **Demands:** Synchronous and async hook contracts (OpenAI #27039), declarative agent definitions (Qwen #4821), SSRF-secure MCP connections (Gemini #27744), and cross-project skill libraries.

**Multi-Agent Orchestration**
- **Drivers:** Qwen Agent Teams (#4844), CodeWhale Whaleflow, Claude multi-window (#30154), Pi session branches.
- **Demands:** Parallel sub-agent coordination, background agent sessions, cross-tab/window handoffs, and structured agent lifecycle management (daemons, reapers).

---

### 4. Differentiation Analysis

The ecosystem breaks into three competitive tiers:

- **Platform Incumbents (Claude Code, OpenAI Codex, Gemini CLI):** These tools compete on *platform integration depth* and *enterprise readiness*. Claude has the richest plugin/hook/MCP ecosystem but is showing scaling friction (billing, context size). Codex differentiates on cloud-client continuity (`/app` handoff) and structured automation APIs (Goal SDK). Gemini is currently defensive, pivoting its differentiation to *safety-first hardening* as a direct response to the data loss crisis.

- **Ecosystem Embedded (GitHub Copilot CLI):** Copilot competes purely on *GitHub affinity*. Its PR velocity (1 PR today, Vi mode unmet for 8 months) demonstrates a critical innovation deficit. It is relying on ecosystem lock-in rather than technical merit—a significant vulnerability as alternatives mature.

- **Open Source Challengers (OpenCode, Pi, Qwen Code, CodeWhale):**
    - **Qwen Code** is the explicit "Claude Code competitor," chasing feature parity while pioneering parallel Agent Teams (#4844) and dynamic workflows (#4732).
    - **Pi** differentiates on *architectural quality*: deep hook systems (`beforeModel`), reactive compaction, local model support, and rapid community response (e.g., `alwaysTrust` hotfix within hours).
    - **OpenCode** targets the *provider-agnostic power user and CI/CD pipeline*, prioritizing NDJSON output, error retry, MCP pagination, and broad provider support (Bedrock, Mantle, Copilot).
    - **CodeWhale** (formerly DeepSeek TUI) is executing an aggressive *platform expansion*, onboarding an increasingly diverse provider catalog (Together, Codex, Volcengine) while overhauling its TUI architecture (multi-tab, l10n).

---

### 5. Community Momentum & Maturity

- **Highest Feature Velocity (Open Source Tier):** Pi, Qwen Code, OpenCode, and CodeWhale ship 10 PRs each per digest. This tier is acting as the ecosystem's R&D lab, landing experimental features (parallel agents, `beforeModel` hooks, multi-tab UIs) that incumbents will likely adopt or clone.
- **Largest Engaged User Base:** Claude Code and OpenAI Codex generate the highest community comment volume (79 and 76 comments on single issues), signaling large user bases experiencing deep integration friction.
- **Maturity Leaders:** Claude Code and OpenAI Codex demonstrate process maturity (versioned releases, structured rollouts, SDKs). Gemini CLI is regressing technically but may emerge with improved release discipline.
- **Stagnation Signals:** GitHub Copilot CLI (1 PR today) and Kimi Code CLI (0 PRs, critical regressions) show clear signals of under-investment or organizational disruption. Kimi's silent API key removal and broken `@filename` represent a fundamental breach of user trust.
- **Community Responsiveness:** Pi stands out for rapid hotfix turnaround (`alwaysTrust` within 1 day). OpenCode and CodeWhale show strong community PR integration. Copilot and Kimi show minimal community feedback loop velocity.

---

### 6. Trend Signals & Developer Reference

**1. Execute with Safety Hardening First**
The Gemini data loss (#27397) is a universal industry alarm. For any tool:
- Default to non-destructive modes for exploration.
- Gate project-level configuration loading behind trust prompts.
- Audit and log all tool call output for hallucinated execution.
- Expect and implement undo/rewind file state operations.

**2. Bet on Session State Machines over Linear Chats**
Cross-tool evidence points decisively towards persistent goals, branching, fork/merge, and parallel agents. Evaluate tool support for:
- **Persistent intent:** Native `/goal` or equivalent.
- **Session trees:** The ability to rewind, fork, and merge.
- **Compaction resilience:** Does the tool strip AGENTS.md or behavioral instructions during context window management?

**3. MCP is Table Stakes; Focus on Security and Scale**
Every tool supports MCP. Differentiation now requires:
- **SSRF protections** for MCP discovery and OAuth flows.
- **Pagination** for large MCP registries.
- **Resource reading** (as opposed to just tool calling).
- **Idempotent approval flows** for headless automation.

**4. Windows/WSL Support is a High-Moat Gap**
Claude Code (#27897 MSIX), OpenAI Codex (#25203, #25715 WSL), Copilot (#3652, #3662), and Pi (#5529 Windows popup) all demonstrate platform neglect. A tool delivering polished WSL path mapping, startup latency fixes, and first-class Windows uninstallation will have a strong competitive advantage.

**5. Watch the Open Source Tier for Leading Indicators**
Qwen’s parallel agent teams (PR #4844), Pi’s `beforeModel` hooks, CodeWhale’s multi-tab agent UIs, and OpenCode’s session goals represent features that will likely become standard across the industry in Q3-Q4 2026. Evaluate long-term lock-in risk against these open-source innovations.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Claude Code Skills Community Highlights Report**
*Data Snapshot: 2026-06-09 | Source: anthropics/skills*

---

### 1. Top Skills Ranking

**#514: Document Typography**
*Author: PGTBoos.* Detects and prevents typographic defects (orphaned words, widow paragraphs) in generated documents. The discussion indicates this is seen as a basic quality-of-life requirement for production AI output.
*Status:* Open | [PR #514](https://github.com/anthropics/skills/pull/514)

**#486: ODT (OpenDocument) Skill**
*Author: GitHubNewbie0.* Enables creation, template filling, and parsing of .odt/.ods files. High engagement reflects strong demand for LibreOffice and open-format compatibility.
*Status:* Open | [PR #486](https://github.com/anthropics/skills/pull/486)

**#83: Skill Quality & Security Analyzers**
*Author: eovidiu.* Meta-skills that evaluate community skills across five dimensions including structure and security. Signals the community's move toward ecosystem self-governance and trust scoring.
*Status:* Open | [PR #83](https://github.com/anthropics/skills/pull/83)

**#181: SAP Predictive Analytics (SAP-RPT-1-OSS)**
*Author: amitlals.* Integrates SAP's open-source tabular foundation model for business data prediction. Represents the strongest enterprise ERP integration attempt in the pipeline.
*Status:* Open | [PR #181](https://github.com/anthropics/skills/pull/181)

**#1140: Agent Creator Meta-Skill**
*Author: SyedaQurratAI.* Dynamically assembles task-specific agent sets. Includes fixes for multi-tool evaluation and Windows support. Pushes the frontier of meta-orchestration.
*Status:* Open | [PR #1140](https://github.com/anthropics/skills/pull/1140)

**#568: ServiceNow Platform Suite**
*Author: Vanka07.* Broad assistant covering ITSM, ITOM, SecOps, ITAM, and IntegrationHub. Massive enterprise platform integration drawing sustained community attention.
*Status:* Open | [PR #568](https://github.com/anthropics/skills/pull/568)

**#723: Testing Patterns**
*Author: 4444J99.* Comprehensive coverage of the testing trophy model, unit tests, and React Testing Library. Addresses demand for closing the feedback loop on AI-generated code.
*Status:* Open | [PR #723](https://github.com/anthropics/skills/pull/723)

**#190: n8n Builder & Debugger Suite**
*Author: Wolfe-Jam.* Skills for building and debugging n8n workflows from scratch. Practical, production-tested tooling for the automation community.
*Status:* Open | [PR #190](https://github.com/anthropics/skills/pull/190)

---

### 2. Community Demand Trends (From Issues)

- **Enterprise Distribution & Trust (Issues #228, #492):** The most-voted issue requests org-wide skill sharing libraries. Simultaneously, security concerns around the "anthropic/" namespace (#492) highlight anxiety about trust boundaries. The community wants enterprise-grade distribution with verification.

- **Developer Toolchain Stability (Issues #556, #1169, #202):** A major friction point—`run_eval.py` is widely reported as producing 0% trigger rates across all queries (#556), and the `skill-creator` skill itself is criticized for poor token efficiency and operational design. The community is demanding reliable build tools.

- **Security as a Core Feature (Issues #492, #412, #1175):** Users are proactively proposing dedicated **agent governance** skills and raising architecture concerns about embedding permissions logic inside SKILL.md. Security is transitioning from an afterthought to a required product capability.

- **Platform Portability (Issues #29, #16):** Persistent requests to run skills via AWS Bedrock and to expose them as MCP servers. The vision extends beyond Claude Code to a universal orchestration protocol.

---

### 3. High-Potential Pending Skills

- **Windows Compatibility Fixes (PRs #1099, #1050):** The `skill-creator` pipeline is functionally broken on Windows. PR #1099 fixes subprocess pipe crashes; PR #1050 resolves Windows command resolution. High-impact, likely to land soon.
  [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050)

- **Contributing.md (PR #509):** Not a skill, but a structural PR to fix the repository's community health score (currently 25%). Directly addresses contributor friction and is heavily linked to community sentiment.
  [PR #509](https://github.com/anthropics/skills/pull/509)

- **Feature-Dev Workflow Fix (PR #363):** Targeted fix for the `TodoWrite` overwrite bug that truncates structured coding workflows. High impact for users employing phased development.
  [PR #363](https://github.com/anthropics/skills/pull/363)

- **AURELION Cognitive Framework (PR #444):** Ambitious structured thinking and memory skill suite. Represents the frontier of cognitive architecture as a skill, still gathering interest.
  [PR #444](https://github.com/anthropics/skills/pull/444)

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand is shifting from the *application layer* (what skills do) to the *infrastructure layer* (how skills are built, shared, and trusted)—specifically requiring stable developer tooling, enterprise-grade distribution models, and embedded security verification before the ecosystem can scale to its full potential.

---

Here is the Claude Code Community Digest for 2026-06-09.

---

## Claude Code Community Digest — 2026-06-09

### 1. Today’s Highlights
Version 2.1.169 shipped with `--safe-mode` (disabling all customizations for troubleshooting) and the `/cd` command (hot-swapping working directories without prompt cache loss). The community is actively rallying around a critical billing block on 1M context windows (Issue #63060, 79 comments), while the “Multi-window Desktop” request (Issue #30154) holds the top feature vote tally. Growing reports of fabricated tool calls (Issue #66408) and silent OTLP telemetry drops (Issue #66401) signal emerging trust and observability concerns among developers.

### 2. Releases
**v2.1.169**
- **`--safe-mode` / `CLAUDE_CODE_SAFE_MODE`**: Starts Claude Code with all customizations (CLAUDE.md, plugins, skills, hooks, MCP servers) disabled, providing a clean troubleshooting path for boot failures or conflicting extensions.
- **`/cd` command**: Allows moving a session to a new working directory mid-conversation without breaking the prompt cache, solving a longstanding UX gap for multi-repo workflows.

### 3. Hot Issues
*Top 10 issues by community engagement in the last 24h:*

1. **[#63060] API Error: Usage credits required for 1M context** — 79 comments, 30 👍. The top bug by far. Max-tier users are hard-blocked by billing checks on 1M-context requests, pointing to a fragile integration between the new context tier and the credit system.  
   [Link](https://github.com/anthropics/claude-code/issues/63060)

2. **[#30154] Feature: Multi-window support in Desktop** — 55 comments, 165 👍. The highest-voted feature request. Users want to tear sessions out of the sidebar into independent OS windows for complex concurrent workflows.  
   [Link](https://github.com/anthropics/claude-code/issues/30154)

3. **[#5674] Persistent ECONNRESET Errors on macOS** — 41 comments, 36 👍. A chronic network failure confirmed macOS-exclusive. Strong signal of a platform-level TLS/socket issue degrading reliability for Mac users.  
   [Link](https://github.com/anthropics/claude-code/issues/5674)

4. **[#27897] Desktop app broken on Windows 11 Insider (MSIX)** — 35 comments, 14 👍. An unresolved EXDEV rename bug renders the desktop app unusable on Windows Insider builds, blocking an entire OS segment.  
   [Link](https://github.com/anthropics/claude-code/issues/27897)

5. **[#33045] Agent tool isolation ignored** — 19 comments, 9 👍. The `worktree` flag has no effect for team agents, meaning agent sandboxing is broken. A core trust-boundary failure for multi-tenant agent deployments.  
   [Link](https://github.com/anthropics/claude-code/issues/33045)

6. **[#29573] File limit filesystem bug on long sessions** — 16 comments, 22 👍. Power users with extended sessions or many concurrent sessions hit filesystem descriptor limits, causing hard failures.  
   [Link](https://github.com/anthropics/claude-code/issues/29573)

7. **[#43255] Claude in Chrome MCP navigation blocked** — 13 comments, 7 👍. A regression in the Chrome MCP connector blocks all navigation (“Navigation to this domain is not allowed”), breaking a primary browser-automation use case.  
   [Link](https://github.com/anthropics/claude-code/issues/43255)

8. **[#32631] Feature: Conversation Branching** — 9 comments, 30 👍. A consolidated spec for `/fork`/`/merge`/tree navigation. The community is pushing for proper branch management over the flat session model.  
   [Link](https://github.com/anthropics/claude-code/issues/32631)

9. **[#61044] MCP tool calls in Routines fail with "requires approval"** — 6 comments, 3 👍. Headless CCR Routines cannot grant UI-based approvals for MCP tools, creating an invisible automation dead end.  
   [Link](https://github.com/anthropics/claude-code/issues/61044)

10. **[#66352] User-level .agents/skills/ discovery** — 4 comments. Asks for cross-project discovery of skills defined at the user home level, reducing duplication for platform engineers.  
    [Link](https://github.com/anthropics/claude-code/issues/66352)

### 4. Key PR Progress
*5 pull requests were updated in the last 24h:*

1. **[#65286] fix(plugins): Add missing plugin.json manifest for plugin-dev** — Ensures the official plugin-dev template is correctly discoverable and installable. Unblocks developers trying to bootstrap new plugins.  
   [Link](https://github.com/anthropics/claude-code/pull/65286)

2. **[#65619 [CLOSED]] fix(plugins): Align frontend-design author with marketplace entry** — Fixes malformed author metadata (two emails in a single field) in the frontend-design plugin manifest, correcting marketplace display.  
   [Link](https://github.com/anthropics/claude-code/pull/65619)

3. **[#66372] fix(devcontainer): Detect Docker daemon failures via $LASTEXITCODE** — Fixes a PowerShell bug where `docker info` failures were silently swallowed, causing the devcontainer script to falsely report Docker Desktop as running.  
   [Link](https://github.com/anthropics/claude-code/pull/66372)

4. **[#26914 [CLOSED]] docs: Add rules frontmatter syntax examples and validation hook** — Addresses silent failures of `paths:` frontmatter in custom rules by providing documentation and a PostToolUse validator hook.  
   [Link](https://github.com/anthropics/claude-code/pull/26914)

5. **[#66171] fix: Symlink vulnerability in extensibility.py** — Prevents project-controlled symlinks from being followed in the extensibility module, closing a security boundary bypass vector.  
   [Link](https://github.com/anthropics/claude-code/pull/66171)

### 5. Feature Request Trends
- **Session Tree Management**: #32631 (Branching) and #30154 (Multi-window) signal that developers have outgrown the linear session model. They want fork/merge/tree navigation and concurrent visual access to sessions.
- **Cloud-Client Continuity**: #66373 (local-to-cloud handoff as the inverse of `--teleport`) shows demand for seamless migration between local CLI and web environments.
- **Agent Configuration Granularity**: Issues #66402 and #33045 reveal that the fleet/agent model requires per-instance model and effort settings, which the current global `settings.json` cannot support.
- **Cross-Project Skills**: #66352 and the plugin improvements point to a need for user-wide single-source-of-truth for skills and plugins, rather than per-project duplication.
- **Extensible Keybindings**: #66399 requests custom file-opening actions in keybindings, pushing beyond the predefined action set.

### 6. Developer Pain Points
- **Context Integrity**: Multiple fresh reports (##66406, 66409, 66400) detail total context loss during upgrades or tool call cycles. This is a critical reliability failure for long-running sessions.
- **Model Reliability vs. Reporting**: #66410 (CLI says 1M, Desktop says non-1M), #66408 (fabricated tool outputs), #66404 (model acknowledges error then repeats it). Trust in model self-reporting is fracturing.
- **Billing Hard Stops**: #63060 is the most-commented issue by far. The integration between the 1M context tier and the billing/auth system is brittle, hard-blocking users without clear resolution.
- **Windows Fragility**: A growing pile of platform-specific regressions: #66396 (UTF-8/Japanese text corruption), #66407 (silent Cowork model swaps), #27897 (MSIX broken). Testing gaps are mounting.
- **Permissions Friction**: Permissions set on the web UI (#64521) are not honored by the CLI, and headless Routines (#61044) cannot grant UI-based approvals. The permission model is fragmented across client surfaces.
- **Telemetry Opaqueness**: #66401 reports that OTLP metrics and logs are silently dropped from interactive macOS TUI sessions, making telemetry-driven debugging unreliable for desktop users.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-09

## 1. Today's Highlights
OpenAI shipped **rust-v0.138.0**, enabling the `/app` command for seamless CLI-to-Desktop handoff and native local image generation. Community attention is focused on a critical model availability bug where `gpt-5.5` is listed locally but returns a 404 on actual requests (Issue #26892). On the development side, the team is heavily focused on landing a structured **Python SDK Goal API** and expanding internal observability with fine-grained tracing spans across tool loading and turn orchestration.

## 2. Releases
- **[rust-v0.138.0](openai/codex)** (Stable): The `/app` command can now hand off CLI threads into Codex Desktop on macOS and native Windows. Windows workspace launches can open directly into Desktop. Includes support for local image attachments and standalone image generation.
- **Pre-releases**: `0.139.0-alpha.1`, `0.138.0-alpha.8`, `0.138.0-alpha.7` were also cut without detailed change logs in this interval.

## 3. Hot Issues
1. **[Issue #26892](openai/codex Issue #26892) (OPEN, 76 comments, 28 👍)** — `gpt-5.5` is listed as available locally but real requests fail with 404 "Model not found" in both Desktop and CLI. This is the most active current issue, blocking access to the latest model.
2. **[Issue #25144](openai/codex Issue #25144) (OPEN, 52 comments, 65 👍)** — Request to add an option disabling automatic conversion of long pasted prompts into `.txt` attachments. Highly upvoted UX papercut.
3. **[Issue #25203](openai/codex Issue #25203) (OPEN, 37 comments, 21 👍)** — GitHub OAuth callback fails on Windows with "Unable to find Electron app", completely blocking authentication.
4. **[Issue #25715](openai/codex Issue #25715) (OPEN, 36 comments, 36 👍)** — Codex App is unusably slow when using WSL as the agent environment. Routine turns take excessive time. High-impact performance regression for Windows developers.
5. **[Issue #12029](openai/codex Issue #12029) (OPEN, 9 comments, 43 👍)** — Request for using more than one account (personal + corporate) on a single machine. Long-standing, high-demand feature.
6. **[Issue #25719](openai/codex Issue #25719) (OPEN, 20 comments, 20 👍)** — Codex Desktop on macOS repeatedly triggers `syspolicyd` / `trustd` CPU and memory runaway, indicating a system-level resource leak.
7. **[Issue #26149](openai/codex Issue #26149) (OPEN, 10 comments, 16 👍)** — Desktop on Windows + WSL repeatedly scans `.codex/.tmp/plugins` over `/mnt/c`, causing severe per-command latency.
8. **[Issue #24675](openai/codex Issue #24675) (OPEN, 21 comments, 16 👍)** — Desktop keeps a stale app connector link after a 401 reauth-required, requiring manual cache clearing to fix.
9. **[Issue #21753](openai/codex Issue #21753) (OPEN, 11 comments, 15 👍)** — Umbrella request for full Claude Code Hook Parity (29+ hooks). Shows strong community push for scriptable automation surfaces.
10. **[Issue #21671](openai/codex Issue #21671) (CLOSED, 25 comments)** — `/compact` failed with a `service_tier` error post-0.129.0 upgrade. Closed, but a notable regression illustrating API integration fragility in core CLI flows.

## 4. Key PR Progress
1. **[PR #27112](openai/codex PR #27112) — Dedicated Python Goal API**: Exposes `run_goal(objective)` and `start_goal(objective)` to represent server continuations as a single logical operation for Python callers.
2. **[PR #27094](openai/codex PR #27094) — Tool Router Spans**: Adds tracing to `build_tool_router` to track a known ~113ms hot spot in `append_tool_search_executor`, enabling targeted optimization.
3. **[PR #27101](openai/codex PR #27101) — User Instructions Provider**: Decouples `codex-core` from `$CODEX_HOME` by injecting user-level instructions via a provider, improving embeddability.
4. **[PR #27107](openai/codex PR #27107) — Run Turn Spans**: Breaks down `run_turn` latency into setup, input-handling, prompt-prep, and tool-loading phases for better app-server observability.
5. **[PR #26880](openai/codex PR #26880) — fsmonitor Fix**: Stops Codex from forcing `core.fsmonitor=false` on internal Git commands, restoring fast worktree reads in large repositories.
6. **[PR #25704](openai/codex PR #25704) — Responses Strict Mode Images**: Feature-flagged normalization of local/data URL images for strict-mode compatibility with the Responses API.
7. **[PR #27062](openai/codex PR #27062) — Guardian Retry**: Adds retry handling for transient failures in the automated permission review session (Guardian), improving reliability of Auto Review.
8. **[PR #27039](openai/codex PR #27039) — Async Command Hooks**: Introduces a deliberately narrow contract for non-blocking `async: true` hooks that run outside the blocking hook lane.
9. **[PR #27105](openai/codex PR #27105) — Plan Refresh from Usage**: Makes the `/usage` endpoint the authoritative source for account plan data, fixing staleness issues from auth-token claims.
10. **[PR #27103](openai/codex PR #27103) — Compaction Cached Tokens**: Adds `cached_input_tokens` to compaction analytics for v2, providing visibility into prompt-cache hit rates.

## 5. Feature Request Trends
- **Multi-Account & Identity**: The sustained demand for separate personal/corporate accounts (Issue #12029, 43 👍) signals a critical pain point for organizational adoption.
- **Advanced Automation & Hooks**: Requests for Claude Code hook parity (Issue #21753) and the landing of async hooks (PR #27039) show the community pushing Codex towards a first-class orchestrator for CI/CD and complex multi-agent workflows.
- **Native Asset Generation**: The high popularity of the closed image generation request (Issue #8758, 55 👍) confirms that developers want AI agents to handle visual assets, not just code.
- **Agent Lifecycle Management**: Calls for TUI Agent Views (Issue #22321) and explicit task-clearing primitives (Issue #23218) indicate users need better tooling to manage multiple concurrent agent sessions.
- **Environment & Git Integration**: Issues around worktrees (Issue #12863) and MCP tool approval flows (Issue #24135) demonstrate that deep compatibility with existing developer tooling is a growing priority.

## 6. Developer Pain Points
- **Windows + WSL Fragility**: This remains the top area of friction. Authentication failures (Issue #25203), severe WSL performance regressions (Issues #25715, #26149), path mismatches (Issue #22185), and project data loss (Issue #19615) make the Windows experience fragile.
- **macOS System Resource Bugs**: The app triggers system process runaways (`syspolicyd`/`trustd`, Issue #25719), generates excessive Crashpad dump files (Issue #25921), and experiences Computer Use hangs (Issue #26415), raising stability concerns.
- **Model Availability Mismatches**: The disconnect between locally listed models and their actual API availability (Issue #26892, Issue #26860) erodes trust in the model selection UI and blocks access to new capabilities.
- **Configuration Staleness**: Stale OAuth connectors (Issue #24675), plan information mismatches (PR #27105), and cache invalidation issues require frequent manual intervention.
- **Performance Regressions**: Recurring regressions in core commands like `/compact` (Issue #21671) and idle I/O activity (Issue #20563) highlight the need for more robust integration testing around critical paths.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — 2026-06-09**

---

### Today's Highlights

The community is grappling with the aftermath of the catastrophic data loss incident (Issue #27397), which has become the rallying point for a broader push on agentic safety and defensive programming. While the nightly release (v0.47.0) focuses on UI polish, the most active development energy is going into security hardening—SSRF protections for MCP tool discovery and zero-quota fail-fast logic. The overriding concern remains sub-agent reliability: the system still hangs, reports false success, and ignores user configurations.

---

### Releases

**v0.47.0-nightly.20260609.g0567b25a2** — Nightly build shipping two small improvements: the Antigravity transition banner is now rate-limited to reduce UI noise, and the "experimental" label has been officially dropped from the Browser Agent documentation, signaling growing confidence in the feature.

---

### Hot Issues

1. **[#27397 — CLOSED] Catastrophic Data Loss (1.2TB)**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/27397)  
   The highest-severity incident in recent memory. The agent executed a generated script that permanently destroyed massive curated media due to missing defensive file I/O. Although closed, this issue is the primary catalyst for the current safety-focused community dialogue.

2. **[#21409 — OPEN] Generalist agent hangs indefinitely**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21409) (👍8)  
   The most upvoted active bug. The CLI hangs on simple tasks like folder creation. The only workaround is to disable sub-agent delegation, defeating the core value of the tool.

3. **[#25166 — OPEN] Shell command stuck "Waiting input" after completion**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/25166) (👍3)  
   A persistent frustration where the CLI hangs post-command execution, breaking automation and scripting use cases.

4. **[#22323 — OPEN] Subagent MAX_TURNS reported as GOAL success**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/22323)  
   A breach of trust: the `codebase_investigator` reports "success" and "GOAL" even when it hits the turn limit having done zero work. Misleading feedback at scale.

5. **[#21968 — OPEN] Agent does not use custom skills autonomously**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21968)  
   Users create skills and sub-agents, but the model rarely invokes them without explicit instruction. The extensibility system is effectively opt-in only.

6. **[#26525 — OPEN] Auto Memory sends unredacted secrets to model context**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/26525)  
   A serious security gap: redaction is requested *after* secrets are already in the model context. Enterprise users are calling for deterministic front-end filtering.

7. **[#22672 — OPEN] Agent should discourage destructive behavior**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/22672) (👍1)  
   The model defaults to `git --force` and destructive resource commands when safer alternatives exist. Directly tied to the root cause of #27397.

8. **[#22267 — OPEN] Browser Agent ignores settings.json overrides**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/22267)  
   Configuration like `maxTurns` is read during initialization but never applied at runtime, making the Browser Agent behave inconsistently across environments.

9. **[#27444 — CLOSED] Unhandled Promise Rejection crash**  
   [Issue Link](https://github.com/google-gemini/gemini-cli/issues/27444)  
   Raw Node.js stack trace flooding the terminal. While closed, it highlights a recurring pattern of fragile error handling that hurts professional adoption.

10. **[#23571 — OPEN] Model creates tmp scripts in random directories**  
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/23571)  
    Users want workspace-constrained temp directories. The current behavior creates cleanup overhead and risks accidental commit of agent artifacts.

---

### Key PR Progress

1. **[#27744 — OPEN] DNS resolution before SSRF guard**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27744)  
   Critical security fix. Prevents SSRF bypass via wildcard DNS services (e.g., `nip.io`) targeting internal metadata IPs.

2. **[#27626 — OPEN] Block private OAuth metadata URLs**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27626)  
   Adds SSRF protection to the MCP OAuth metadata fetch path, guarding against internal network probing from malicious MCP servers.

3. **[#27698 — OPEN] Zero-quota fail fast to prevent retry loop hang**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27698)  
   Fixes a bug where hitting a hard quota of 0 burned through all 10 retries with no progress. Now provides immediate failure feedback.

4. **[#27429 — CLOSED] Handle EBADF in resizePty on resume**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27429)  
   Resolves a crash on `--resume` where a stale PTY fd caused an `ioctl` crash. Improves session restoration reliability.

5. **[#27438 — CLOSED] Configurable tool call timeout (`tools.callTimeout`)**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27438)  
   A heavy community ask: a centralized timeout for tool execution, preventing a single hung tool from blocking the entire session.

6. **[#27619 — OPEN] Atomic MCP tool discovery update**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27619)  
   Prevents the tool registry from being wiped clean during transient network blips, ensuring the agent retains its last known good tool set.

7. **[#27603 — OPEN] Platform-aware shell guidance**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27603)  
   Injects Windows-specific command examples into the model prompt, reducing cross-platform execution errors for Win32 users.

8. **[#27605 — OPEN] Consolidated MCP server lists for policy engine**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27605)  
   Closes a policy bypass vector by correctly unioning MCP allow/block lists across all settings scopes (user, system, workspace).

9. **[#27428 — CLOSED] Fix sandbox imageExists via Docker inspect exit code**  
   [PR Link](https://github.com/google-gemini/gemini-cli/pull/27428)  
   Replaces brittle `stdout` parsing with exit code checks, fixing false negatives caused by Docker BuildKit's stderr output.

10. **[#27440 — CLOSED] `[Skill]` tag in slash command autocomplete**  
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27440)  
    UX improvement: skills now get a `[Skill]` badge in the `/` menu, matching `[MCP]` and `[Agent]` for instant recognition.

---

### Feature Request Trends

Requests are converging on three pillars:

- **Hardened Agentic Safety.** Post-#27397, the community demands explicit guardrails: confirm-before-write, safe file I/O modes, and undo workflows. Users want the agent to default to safe behavior and escalate before breaking things.
- **Reliable Multi-Agent Orchestration.** The "set and forget" promise is failing. Users want the agent to autonomously delegate to sub-agents and skills without hanging or lying about success. Better failure reporting and automatic retry with escalation are top asks.
- **Context-Aware Intelligence.** There is strong interest in AST-aware file reading to reduce token waste and incorrect context (#22745). Users also want the Memory system to be smarter about when to extract signals and when to discard noise (#26522).

---

### Developer Pain Points

- **Agent Unreliability (#1 Concern).** The agent hangs indefinitely (#21409), reports fake GOAL success (#22323), and ignores configured skills (#21968). This fundamentally erodes trust in the tool as an autonomous programming partner.
- **Configuration Fragility.** Settings are frequently loaded from the wrong path (#27421) or completely ignored at runtime (#22267). Sub-agents run despite being explicitly disabled (#22093). The environment feels non-deterministic.
- **Lack of Default Safety.** The default behavior is too aggressive. Random scripts pollute workspaces (#23571), dangerous git commands are issued without caution (#22672), and the data loss incident has made everyone wary of letting the agent run unchecked.
- **Terminal & UI Flickering.** The interface has persistent quality issues: corruption after external editor exits (#24935), flicker on resize (#21924), and character rendering bugs with international text (#27505). These chip away at the professional development experience.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — June 9, 2026

## Today's Highlights
No new releases landed today, but the repository saw heavy community activity with **33 issues updated** in the last 24 hours. A critical regression in JSON schema validation broke function calling in v1.0.60, while a long-standing sub-agent hang bug and persistent demand for Vi input mode dominated discussions. On the platform side, significant WSL performance issues and a Windows uninstall bug continue to generate friction.

---

## Releases
No new versions of `github.com/github/copilot-cli` were published in the past 24 hours.

---

## Hot Issues

1. **[#3716 [Regression] Function call fails](https://github.com/github/copilot-cli/issues/3716)** — A `moonshot flavored json schema` validation error breaks tool calling, introduced in v1.0.60. Zero comments but filed as a regression, which typically warrants immediate triage.

2. **[#3547 Background sub-agent silently hangs at total_turns=0](https://github.com/github/copilot-cli/issues/3547)** — Sub-agents dispatched with `model="gpt-5.5"` report success but never progress past zero turns. 6 comments, active discussion on agentic workflow reliability.

3. **[#13 CLI input should have a vi/vim input mode](https://github.com/github/copilot-cli/issues/13)** — The single most-requested feature in the repo, still collecting votes (63 👍, 7 comments). A major usability blocker for modal-editor users that remains unresolved after eight months.

4. **[#3436 MCP search constructs wrong URL for custom MCP registries](https://github.com/github/copilot-cli/issues/3436)** — The `/mcp search` command omits the `/v0.1/` path segment, causing 404s against any self-hosted MCP registry. 5 comments; a blocking issue for enterprise adopters using custom registries.

5. **[#2867 Claude Opus 4.6 "model not supported" after quota reset](https://github.com/github/copilot-cli/issues/2867)** — Users who wait for their quota reset are rewarded with a permanent `model not supported` error. 5 comments; highlights poor error-state recovery in the model routing layer.

6. **[#2540 Plugin-defined preToolUse hooks do not fire](https://github.com/github/copilot-cli/issues/2540)** — Hooks defined in a plugin's `hooks.json` are entirely ignored by the agent runtime, both in the main session and in sub-agents. 4 comments, 3 👍 — a major gap in the extensibility system.

7. **[#3652 WSL Chat experiences 40–80 second startup delays](https://github.com/github/copilot-cli/issues/3652)** — `CopilotCLIChatSessionContentProvider.listSessions` creates a massive bottleneck in WSL. 3 comments; directly impacts daily workflow velocity for Linux-on-Windows developers.

8. **[#3709 Allow /model to switch between multiple models including BYOK](https://github.com/github/copilot-cli/issues/3709)** — BYOK mode is pinned to a single model; the `/model` picker only shows GitHub-hosted options. 1 comment, actively collecting 👍. Users want the freedom to switch between local and hosted models mid-session.

9. **[#3717 BYOK: Add an option to disable streaming](https://github.com/github/copilot-cli/issues/3717)** — Already closed (likely accepted internally). A straightforward but important feature for compatibility with non-streaming providers and users who prefer deterministic response boundaries.

10. **[#3662 Can't uninstall Copilot CLI on Windows 11](https://github.com/github/copilot-cli/issues/3662)** — The Control Panel applet silently fails; no CLI uninstall command is documented. 1 comment; a basic platform hygiene issue that erodes trust in the installation lifecycle.

---

## Key PR Progress

Only one pull request was updated in the past 24 hours:

- **[#1960 install: use GITHUB_TOKEN for authenticated GitHub requests](https://github.com/github/copilot-cli/pull/1960)** — *Author: devm33, Closed.* The install script now passes `GITHUB_TOKEN` as an `Authorization` header for `curl`/`wget` downloads and embeds it in Git remote URLs for `ls-remote`. This directly addresses rate-limit failures and private-repo installation support in CI environments. Small change, high impact for automated setups.

---

## Feature Request Trends

- **Vi/Vim Input Mode (#13)** — 63 upvotes, by far the dominant UX request. The absence of modal editing in the interactive CLI continues to be a source of friction for a vocal and large segment of power users.
- **Session & Prompt Management (#1928, #2966, #3720, #3713)** — Users are asking for the ability to pause sessions, stash typed prompts with `ESC ESC`, manage concurrent sessions across repos, and modify prompts via plugin hooks. The agentic workflow is creating a demand for richer session lifecycle controls.
- **Model Flexibility (#3709, #3717, #3707, #3705)** — A strong trend around unlocking model choice: switching models mid-session, disabling streaming, supporting lower-cost/open-weight models, and expanding free-tier access beyond Haiku.
- **Plugin System Maturation (#2540, #2201, #3713)** — The hooks system is under active scrutiny. Requests center on making hooks reliable (they currently fail silently), and expanding hook capabilities to allow prompt mutation, not just observation.
- **Background & Scheduled Execution (#3714)** — A newer aspirational request: using Copilot CLI as a cron-like scheduled task runner. Early stage but signals where power users want to take the tool next.

---

## Developer Pain Points

- **Windows & WSL Friction** — A recurring cluster of issues. WSL startup delays of 40–80 seconds (#3652), a broken Windows uninstaller (#3662), clipboard interception conflicts (#3724), and ReFS sandbox incompatibility (#3712) suggest the platform port is not receiving adequate QA attention.
- **Agent Reliability** — Sub-agents hanging indefinitely (#3547) and a fresh function-calling regression (#3716) undermine the reliability of multi-step, multi-agent workflows.
- **Plugin & Hook Fragility** — PreToolUse hooks (#2540) and sessionStart hooks (#2201) failing to fire makes the plugin platform unreliable for any serious customization work. Developers cannot trust the contract.
- **Model Routing Quirks** — Erroneous `model not supported` errors after respecting quota back-offs (#2867) and the inability to switch models in BYOK mode (#3709) create a frustrating, unpredictable model selection experience.
- **Input UX Degradations** — Multi-line input invisibility in `ask_user` (#3722), inconsistent picker navigation (#3715), and the missing Vi mode (#13) collectively degrade the core interactive experience that defines the CLI.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**
*Date: 2026-06-09*

---

### 1. Today’s Highlights

The Kimi Code CLI ecosystem is in a tense migration period following the v0.11.0 TypeScript rewrite. User reports over the last 24 hours surface two major regressions: the silent removal of API key authentication and a broken `@filename` context-injection command, both of which severely impact automation and core workflows. A long-standing documentation issue to explicitly deprecate the Python version was finally closed, but no hotfix releases arrived to stabilize the new client.

---

### 2. Releases

No new versions of `kimi-cli` (Python, v1.47.0) or `kimi-code` (TypeScript, v0.11.0) were published in the last 24 hours.

---

### 3. Hot Issues
*Only four issues were updated in the reporting window, but they represent high-severity signals about the stability of the new codebase.*

**#2436 – Installation & Dual-Client Confusion**
[🔗 GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2436)
*Why it matters:* User reports installation failures on the legacy `kimi-cli` while simultaneously having `kimi-code` installed. The issue title (“Kimi can’t seem to make up her mind”) captures the community frustration with the project’s current dual-version fragmentation.
*Reaction:* 0 comments, 0 👍. Suggests an edge-case conflict, but highlights that the login/auth flow is not properly isolated between the Python and TypeScript clients.

**#2442 – Silent API Key Removal Breaks Workflows**
[🔗 GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2442)
*Why it matters:* **Highest severity item today.** API key authentication was silently removed from the v0.11.0 TypeScript rewrite on macOS. This is a regression that breaks all headless, scripted, and CI/CD use cases.
*Reaction:* 0 comments, 0 👍. Still fresh, but the impact on automation-oriented users is immediate. If you rely on the CLI in pipelines, upgrading to v0.11.0 is currently unsafe.

**#2376 – Deprecation Banner for Docs (CLOSED)**
[🔗 GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2376)
*Why it matters:* The project formally acknowledged the Python → TypeScript split by adding a deprecation banner to the GitHub Pages documentation.
*Reaction:* Merged without comment. While good for clarity, it highlights that no migration script or compatibility layer was provided alongside this formal deprecation.

**#2441 – `@filename` Command Completely Broken**
[🔗 GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2441)
*Why it matters:* The `@filename` directive—the primary mechanism for injecting file context into a conversation—no longer works in v0.11.0. This severely degrades the core user loop of “refer to file X, analyze file Y.”
*Reaction:* Reported bilingually (English/Chinese), indicating global impact. This is a fundamental regression that forces users to fall back to manual copy-paste.

---

### 4. Key PR Progress

No pull requests were updated, merged, or opened in the last 24 hours. The team appears to be in a triage-and-bug-fix cycle following the v0.11.0 release rather than shipping new features.

---

### 5. Feature Request Trends

The community’s strongest signal is **not** a demand for new capabilities, but a call for **stability and feature parity** in the TypeScript rewrite:

- **Stabilize Authentication:** API key support was considered a baseline feature; its silent removal in v0.11.0 is a hard blocker for professional use.
- **Restore Core Context Commands:** `@filename` is critical for the AI coding assistant loop. The community expects this to work from day one of a new release.
- **Simplified Version Management:** Users need a single, unambiguous path forward. The coexistence of `kimi-cli` and `kimi-code` without a clear migration script is causing trust erosion.

---

### 6. Developer Pain Points

- **Automation Unreliability:** The silent removal of API key auth (#2442) makes the CLI untrustworthy for CI/CD. Developers currently cannot safely upgrade without breaking their pipelines.
- **Contextual Workflow Blocked:** The `@filename` regression (#2441) forces manual context injection, negating the primary efficiency gain of an agentic CLI tool.
- **Upgrade Path Anxiety:** With no hotfix in sight, developers are stuck choosing between a stable but deprecated Python client and a new TypeScript client whose core features are broken. Installation confusion (#2436) compounds this uncertainty.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-09

---

## Today's Highlights

No new official release landed today, but the community is actively shipping fixes for a wave of regressions. The **Bedrock/Mantle** integration is seeing multiple fresh bug reports (empty responses, auth signature mismatches), while a critical **SQLite `NOT NULL` constraint** crash (#31413, #31204) is blocking headless runs and agent switching for users on the latest builds. On a positive note, PRs for better **MCP pagination** (#31442) and **session idle draining for JSON output** (#31434) are moving forward, improving stability for CI users and large-server setups.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#27167 – Native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)**  
   *Author: jorgitin02 | 👍 65 | 💬 37*  
   The most-liked open feature request. Proposes a `/goal` command to set a persistent session lifecycle goal. The heavy upvote count signals strong demand for structured intent management beyond slash commands.

2. **[#5474 – `/undo` does not roll back file changes](https://github.com/anomalyco/opencode/issues/5474)**  
   *Author: sdivens | 👍 12 | 💬 28*  
   A long-standing UX friction point. The chat message is undone, but file edits survive, forcing manual workspace restoration. This mismatch erodes trust in the command.

3. **[#29548 – OpenAI provider header timeout regression](https://github.com/anomalyco/opencode/issues/29548)**  
   *Author: rayborg | 👍 0 | 💬 11*  
   Upgrading to 1.15.11 caused `Provider response headers timed out after 10000ms`. The community has confirmed raising `headerTimeout` works, but it’s a clear regression.

4. **[#30948 / #31349 – Bedrock/Mantle regressions](https://github.com/anomalyco/opencode/issues/30948)**  
   *Authors: FelipeNystrom, nisanthchunduru | 👍 4 | 💬 8+5*  
   OpenCode 1.16.0 fails against Bedrock-compatible gateways with empty outputs, and Bedrock Mantle's new GPT-5.x models trigger SigV4 signature mismatches. Two distinct issues suggesting a brittle provider path.

5. **[#31247 – Opus 4.8 via Copilot leaks tool-call text](https://github.com/anomalyco/opencode/issues/31247)**  
   *Author: doomsday616 | 👍 0 | 💬 6*  
   In long sessions, the assistant emits raw `call read`, `call write`, and `<invoke>` markup into conversation text. Highly disruptive to agentic workflows.

6. **[#15535 – Support MCP Resources](https://github.com/anomalyco/opencode/issues/15535)**  
   *Author: feiwhang | 👍 16 | 💬 6*  
   The desire for `resources/read` support in addition to tools continues to gain traction. MCP servers often expose configs, docs, and schemas as resources, and missing this feature limits agent context.

7. **[#16960 – Compaction loses AGENTS.md/CLAUDE.md context](https://github.com/anomalyco/opencode/issues/16960)**  
   *Author: jblenman | 👍 2 | 💬 5*  
   Session compaction calls the LLM with an empty system prompt, stripping behavioral instructions from AGENTS.md. Post-compaction, the agent is effectively lobotomized—a severe governance hole.

8. **[#31413 / #31204 – `NOT NULL constraint failed: session_message.seq`](https://github.com/anomalyco/opencode/issues/31413)**  
   *Authors: High-cla, coygeek | 👍 2 | 💬 4+2*  
   A critical migration bug in recent builds (1.15.13+). Every code path creating a session message (agent switch, `opencode run`, HTTP API) crashes with a SQLite constraint violation. Highest urgency bug reported today.

9. **[#13430 – Clickable file:line references in Web UI](https://github.com/anomalyco/opencode/issues/13430)**  
   *Author: InCerryGit | 👍 0 | 💬 5*  
   Basic developer quality-of-life: assistant messages containing `src/foo.ts:123` should link to the built-in editor. Currently plain text only.

10. **[#23153 – Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)**  
    *Author: suse-coder | 👍 15 | 💬 7*  
    Niche but significant demand for crypto payment support. 15 👍 indicates a real segment of the community wants consumption-based billing outside traditional cards.

---

## Key PR Progress

1. **[#31343 – Draft tab support for tabs store](https://github.com/anomalyco/opencode/pull/31343)**  
   *Author: Brendonovich*  
   Foundations for a larger UI upgrade (decomposed from #31034). Adds draft tab state management—a building block for session preview and multi-tab workflows.

2. **[#31297 – Force UTF-8 encoding for PowerShell output](https://github.com/anomalyco/opencode/pull/31297)**  
   *Author: duofuwang*  
   Direct fix for non-ASCII garbled output on Windows. Sets `$OutputEncoding` and `[Console]::OutputEncoding`. Closes three related issues (#23636, #31187, #30205).

3. **[#31434 / #31446 – Drain pending events before idle in JSON format](https://github.com/anomalyco/opencode/pull/31434)**  
   *Authors: jangel97*  
   Fixes `opencode run --format json` terminating prematurely before text and reasoning events are emitted. Essential for CI/headless environments piping the NDJSON output.

4. **[#31447 – Ensure config directory exists before writing `.gitignore`](https://github.com/anomalyco/opencode/pull/31447)**  
   *Author: deepshekhardas*  
   Prevents startup crash `ENOENT: no such file` when `OPENCODE_CONFIG_DIR` points to a wiped directory (common after auto-updates). Improves boot resilience.

5. **[#31448 / #31438 – v2 layout corner radius fixes](https://github.com/anomalyco/opencode/pull/31448)**  
   *Authors: deepshekhardas, gcavanunez*  
   Polish for the new v2 UI: adds `overflow-hidden` and `rounded-b-[10px]` so the chat panel and composer dock render consistently rounded bottoms.

6. **[#31329 – Graceful PDF/image read failure handling](https://github.com/anomalyco/opencode/pull/31329)**  
   *Author: zhiyiwang-byte*  
   Prevents session crashes when ingesting corrupted or permission-restricted PDFs/images. Catches the error in `prompt.ts` instead of letting it propagate.

7. **[#31444 – Skip spinner animation in non-TTY environments](https://github.com/anomalyco/opencode/pull/31444)**  
   *Author: deepshekhardas*  
   Stops `@clack/prompts` from emitting raw ANSI Braille characters in CI/piped stdout. Important automation hygiene.

8. **[#31442 – Paginate MCP catalogs](https://github.com/anomalyco/opencode/pull/31442)**  
   *Author: rekram1-node*  
   Enables cursor-based pagination for MCP tools, prompts, and resources. Caps traversal at 1,000 pages. Critical for users with large MCP servers.

9. **[#30332 – OpenRouter reasoning variants for all models](https://github.com/anomalyco/opencode/pull/30332)**  
   *Author: AnthonyMLau*  
   Fixes `variants()` returning empty for non-GPT models on OpenRouter. Unlocks reasoning models for a wider variety of OpenRouter providers.

10. **[#31440 – Retry transient network errors](https://github.com/anomalyco/opencode/pull/31440)**  
    *Author: Sylchi*  
    Adds retry logic for `ECONNRESET`, `ECONNREFUSED`, and fetch failures instead of surfacing raw error content as terminal. Closes four related issues (#31133, #20822, #15350, #21893).

---

## Feature Request Trends

- **Session Lifecycle & Context Persistence**  
  The strongest signal this week. `#27167` (native `/goal` lifecycle) and `#16960` (compaction retaining AGENTS.md) both target a common gap: instructions and goals do not survive session management operations. Users want a concept of *persistent intent*.

- **Enhanced MCP Integration**  
  `#15535` (MCP Resources) keeps gaining traction. The community is outgrowing "tools-only" MCP and wants full resource reading capabilities for documentation, schemas, and config files.

- **Provider Coverage & Reliability**  
  The Bedrock/Mantle cluster (`#30948`, `#31349`, `#31430`), OpenAI header timeout (`#29548`), and Copilot Opus leakage (`#31247`) all point to a consistent theme: new model/provider integrations are landing faster than their error handling matures. Upgrading between minor versions carries real risk of provider-specific breakage.

- **Web UI Maturation**  
  Requests for clickable file lines (`#13430`), built-in file opening (`#31406`), and restored navigation buttons (`#31441`) indicate the v2 web interface is seeing real use but still needs basic developer UX love.

- **Payment Flexibility**  
  `#23153` (crypto payments) reflects a small but vocal cohort wanting alternative billing. Worth watching if OpenCode expands its consumption-based monetization.

---

## Developer Pain Points

1. **Database Migration Instability**  
   The `session_message.seq` constraint violations (`#31413`, `#31204`) are the single largest operational blocker right now. They break agent switching, headless CLI runs, and HTTP API usage—impacting almost every workflow.

2. **Provider Fragility on Upgrade**  
   Developers upgrading between recent versions (1.14.x → 1.15.x → 1.16.x) frequently encounter provider-specific regressions (timeouts, empty responses, tool call leakage). The lack of a regression test suite for each provider channel erodes upgrade confidence.

3. **Contextual Amnesia**  
   `/undo` not reverting files (`#5474`) and compaction stripping AGENTS.md (`#16960`) represent a broader systemic issue: OpenCode fails to maintain a coherent causal link between conversation history, system instructions, and file system state.

4. **Headless / CI/CD Friction**  
   The `--format json` output bug (`#31404`, `#31434`) and raw ANSI output in non-TTY environments (`#31444`) show that scripting and automation use cases still feel like second-class citizens.

5. **Plugin Cache Staleness**  
   `#25293` – `@latest` plugin tags remaining pinned to old npm versions even after new publishes. A sharp edge for plugin ecosystem governance.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

**Pi Community Digest – 2026-06-09**

---

### 1. Today's Highlights
The immediate backlash against the just-landed **Project Trust** feature (v0.79.0) dominates today's discussion, prompting a rapid hotfix PR for an `alwaysTrust` setting. On the performance front, the team merged critical fixes for quadratic TUI rendering on large sessions and mid-turn context compaction failures that have been plaguing power users and local model backends.

---

### 2. Releases
- **v0.79.0** – The headline feature is **Project Trust**, an interactive gating mechanism for loading project-local settings, resources, and packages. It allows users to save trust decisions per project and introduces `--approve` / `--no-approve` flags for non-interactive use. The release notes also contain broken links which have already been filed as a bug.

---

### 3. Hot Issues
1. **#5514 – Project Trust Feature Feedback**  
   `markg85` immediately calls the new gating "annoying," arguing power users do not want to repeatedly approve directory access. 14 comments and 5 reactions show the community is sharply split between security and friction.  
   [Issue #5514](https://github.com/earendil-works/pi/issues/5514)

2. **#5492 – High CPU in TUI on Large Sessions**  
   `somjik-api` traces ~100% CPU idle usage to a quadratic branch traversal (62k session size). The root cause is `getContextUsage → sessionManager.getBranch`. This has severely impacted long-running sessions.  
   [Issue #5492](https://github.com/earendil-works/pi/issues/5492)

3. **#5478 – CWD Bridge Captures but Never Propagates**  
   A significant state-hygiene bug: the `cwd` bridge correctly captures directory changes after every `bash` tool execution but *never reads the captured value back*. The tool loop and footer silently drift from the actual shell working directory.  
   [Issue #5478](https://github.com/earendil-works/pi/issues/5478)

4. **#5464 – Local Model "Working" Latency**  
   Users running local models (e.g., Minstral 3B via Ollama) report a 3–5 minute delay on the "Working" status for every message, making local-only sessions nearly unusable for iterative tasks.  
   [Issue #5464](https://github.com/earendil-works/pi/issues/5464)

5. **#5427 – OpenAI Codex Transport Issues**  
   Reliable SSE response timeouts (10,000 ms) after a few messages in a session. This is a hard block for any developer relying on Codex models through a ChatGPT subscription.  
   [Issue #5427](https://github.com/earendil-works/pi/issues/5427)

6. **#5536 – Split-Turn Compaction 429 on Local Backends**  
   Auto-compaction launches two summarization requests in parallel, which single-slot local backends (like `llama.cpp`) reject with `429 Too Many Requests`. Compaction then fails silently.  
   [Issue #5536](https://github.com/earendil-works/pi/issues/5536)

7. **#5512 – Auto-Compaction Lacks Mid-Turn Context Guard**  
   Long tool loops can grow past the configured `contextWindow` before compaction is checked, because large tool results are appended immediately before the next LLM call.  
   [Issue #5512](https://github.com/earendil-works/pi/issues/5512)

8. **#5529 – Windows Terminal Popup Regression**  
   The fix for `windowsHide:true` (previously addressed in #5113, #4699) has regressed from the central spawn wrapper. Users see terminal windows flash/pop on every child process spawn.  
   [Issue #5529](https://github.com/earendil-works/pi/issues/5529)

9. **#5538 – Anthropic Session Stuck After Aborting Tool Call**  
   Aborting a stream mid-`toolCall` (Esc key) leaves a malformed assistant message (`arguments: {}`, no `tool_result`). Every subsequent prompt in that session then fails with a hard error.  
   [Issue #5538](https://github.com/earendil-works/pi/issues/5538)

10. **#5363 – Amazon Bedrock Mantle Provider Request**  
    Strong demand (6 comments, 3👍) for a new AI provider supporting Bedrock Mantle’s OpenAI-compatible API, which is incompatible with the existing Converse API provider.  
    [Issue #5363](https://github.com/earendil-works/pi/issues/5363)

---

### 4. Key PR Progress
1. **#5537 – `beforeModel` Hook & Reactive Compaction**  
   Merged. Adds two powerful callbacks to `AgentLoopConfig`: `beforeModel` (pre-LLM context manipulation) and reactive compaction hooks. This is a major architectural step for provider-specific logic and mid-turn backpressure.  
   [PR #5537](https://github.com/earendil-works/pi/pull/5537)

2. **#5524 – Fix Azure OpenAI `store: false`**  
   Merged. A critical three-line fix adding `store: false` to Azure OpenAI Responses requests, preventing stateful API bugs that Azure users were hitting disproportionately.  
   [PR #5524](https://github.com/earendil-works/pi/pull/5524)

3. **#5521 – Restore Files on Rewind (Checkpoints)**  
   Merged. Extends the existing rewind feature to optionally roll back file edits on disk alongside the conversation history. This closes a long-standing gap in the agent’s undo model.  
   [PR #5521](https://github.com/earendil-works/pi/pull/5521)

4. **#5515 – `alwaysTrust` Setting**  
   Merged. Direct community response to the Project Trust backlash (#5514). Adds a flag to completely disable project trust gating, restoring the frictionless experience for power users.  
   [PR #5515](https://github.com/earendil-works/pi/pull/5515)

5. **#5513 – Mid-Turn Context Window Guard**  
   Merged. Exposes `shouldStopAfterTurn` to stop a tool loop when it crosses the compaction threshold, compact, and resume. Directly addresses the fragility described in #5512.  
   [PR #5513](https://github.com/earendil-works/pi/pull/5513)

6. **#5493 – Fix Quadratic Session Branch Traversal**  
   Merged. Performance patch for the high CPU issue (#5492) by caching or avoiding the O(n²) lookup in `sessionManager.getBranch` inside the TUI footer render loop.  
   [PR #5493](https://github.com/earendil-works/pi/pull/5493)

7. **#5533 – Fix Binary Assets for `--export`**  
   Merged. Patches the binary build script to copy missing `template.{css,js}` files, fixing the export feature when Pi is launched from the dist folder (#5534, #5240).  
   [PR #5533](https://github.com/earendil-works/pi/pull/5533)

8. **#5527 – Fix Bedrock Region Extraction from ARN**  
   Open. Corrects the Bedrock provider to extract the region from inference profile ARNs instead of silently falling back to the `AWS_REGION` environment variable, which could point to a completely different region.  
   [PR #5527](https://github.com/earendil-works/pi/pull/5527)

9. **#5503 – MiniMax M3 Adaptive Thinking**  
   Merged. Flags the MiniMax-M3 model for the adaptive thinking request format, matching the support already present for Claude Opus, enabling `thinking: { type: "adaptive" }` + effort control.  
   [PR #5503](https://github.com/earendil-works/pi/pull/5503)

10. **#5509 – Amazon Bedrock Mantle Provider**  
    Open. A new provider for Amazon’s Bedrock Mantle OpenAI-compatible API, supporting GPT 5.5 and 5.4. Modelled after the Azure OpenAI Responses provider. Strong community interest.  
    [PR #5509](https://github.com/earendil-works/pi/pull/5509)

---

### 5. Feature Request Trends
- **Provider Expansion:** There is persistent demand for new backends. Today’s top requests are **Amazon Bedrock Mantle** (OpenAI-compatible API), **Azure Cognitive Services**, and expanded model lists for Together.ai / MiniMax.
- **Trust & Security Re-balancing:** The Project Trust feature landed to significant friction. The community is now requesting **exposed trust APIs for extensions** and **user-level opt-out flags** to skip gating entirely on trusted machines.
- **Context & Session State Management:** Users want the agent to handle context windows more intelligently: **mid-turn compaction guards**, **restoring file state on rewinds**, and preventing **state drift** between the shell and the internal CWD bridge.
- **Configurability & UX:** Consistent push to make more internals configurable: **clipboard image storage paths**, **autocomplete cursor behavior**, **theme auto-detection**, and **rewind granularity**.

---

### 6. Developer Pain Points
- **State Hygiene:** The CWD bridge writing captured data that is never read (#5478) and malformed session state on stream abortion (#5538) reveal a recurring struggle with keeping the agent loop, shell state, and session history perfectly synchronized.
- **Compaction Fragility:** Compaction is the single biggest source of mid-session failures. It fails under local backends (429 from parallel requests #5536), lacks a mid-turn safety guard (#5512), and can lock sessions with unexpected "context shift disabled" errors (#5511).
- **Performance Degradation Over Time:** The quadratic rendering issue (#5492) and extreme latency with local models (#5464) erode confidence in Pi’s ability to handle sustained, multi-hour coding sessions without a heavy server-side backend.
- **Build & Deployment Friction:** The recurring missing `template.{css,js}` files in binary builds (#5534, #5240) introduces a basic functional failure in the distribution pipeline, forcing users to debug export functionality immediately after installation.
- **Cross-Provider Inconsistency:** Each provider backend introduces unique one-off bugs — Azure stateful mode, Together.ai serverless restrictions, Gemini parallel tool call errors, and Kimi thinking mode toggles — making provider switching a gamble for users.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for the simulated GitHub activity on **2026-06-09**, structured for a technical developer audience.

---

### Qwen Code Community Digest — 2026-06-09

### 1. Today's Highlights
This week’s activity revolves heavily around two poles: **Claude Code feature parity** and **core session stability**. Several high-impact PRs implementing declarative agent frontmatter (PR #4842), parallel Agent Teams (PR #4844), and a dedicated `enter_plan_mode` tool (PR #4853) are pushing the agent orchestration surface forward. However, this is balanced by a serious P1 OOM regression when using `qwen --resume` (Issue #4815) and a deep-dive into microcompaction gaps in long-running `/goal` loops (Issue #4838), which has drawn immediate fix PRs. On the operational side, the community is demanding stricter CI enforcement to prevent broken main branches (Issue #4864).

### 2. Releases
**No new releases** were published in the last 24 hours. The latest available stable version remains **v0.17.1**.

### 3. Hot Issues
*Pick of the 10 most impactful Issues based on urgency, community reaction, and strategic importance.*

1.  **[#4815] Severe OOM with `qwen --resume` and Escape key broken (P1/Bug)**
    - *Why it matters:* A critical stability block. Session restore (`--resume`) leads to an unrecoverable OOM crash within ~10 minutes, rendering long-running agent workflows impossible. High community confirmation.
    - *Reaction:* Escalated to P1. The Dev team is actively investigating relation to hook continuations (see #4838).
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4815)

2.  **[#4838] Hook continuations skip tool-result microcompaction in `/goal` loops (P1/Bug)**
    - *Why it matters:* Root cause analysis of #4815. Long `/goal` loops recursively call `sendMessageStream()` without compacting stale tool results, leading to unbounded context growth and eventual OOM.
    - *Reaction:* High urgency. Two targeted fix PRs (#4823, #4840) have been submitted in parallel.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4838)

3.  **[#4821] Support declarative agent definitions via frontmatter files (Feature)**
    - *Why it matters:* The most requested parity feature this period. Users want to define agents via Markdown/YAML (`.qwen/agents/*.md`) instead of TypeScript, enabling sharing and version control of agent personalities.
    - *Reaction:* Very positive. Community sees this as essential for building an agent marketplace/ecosystem.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4821)

4.  **[#4877] OpenWork cannot distinguish same model from different providers (P2/Bug)**
    - *Why it matters:* A real-world usability bottleneck. When configuring multiple OpenAI-compatible providers (e.g., local GLM-5 vs Qwen-provided models), the UI conflates them by ID, making provider selection impossible.
    - *Reaction:* Frustrated. Highlights the growing complexity of multi-provider config management.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4877)

5.  **[#4845] `feat: add /import-config for Claude user config migration (Feature)**
    - *Why it matters:* Directly addresses switching friction. Users migrating from Claude Code want a one-click import for MCP servers, instructions, permissions, and custom commands.
    - *Reaction:* High interest from the developer adoption crowd.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4845)

6.  **[#4782] ACP Streamable HTTP transport implementation & upgrade plan (Feature)**
    - *Why it matters:* Foundation for IDE integration. Qwen Code Daemon now supports ACP natively, enabling zero-adapter connections to editors like Zed and JetBrains. This issue tracks API alignment and future upgrade paths.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4782)

7.  **[#4801] Add a dedicated `web_search` tool (Feature)**
    - *Why it matters:* Qwen Code is the only major Code Agent CLI lacking a native search tool. The model currently has to guess URLs via `web_fetch`, which is inefficient.
    - *Reaction:* Strong support. Users note that DashScope (the backend) already has this capability (Issue #3841).
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4801)

8.  **[#4675] Vim INSERT mode Esc key leak & mode indicator lag (Bug)**
    - *Why it matters:* Affects the entire terminal-based power-user workflow. The Esc key action bleeds into the app-level handler, and the NORMAL/INSERT mode indicator lags significantly.
    - *Reaction:* High frequency of upvotes and "me too" comments from Vim users.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4675)

9.  **[#4864] CI: Enable required status checks on main branch (Enhancement)**
    - *Why it matters:* A PR with failing CI was merged (PR #4798), breaking `tsc --build` on main. This incident has galvanized the community to demand branch protection rules.
    - *Reaction:* Strong consensus on engineering hygiene. Represents a maturation point for the project.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4864)

10. **[#4876] Subagent reading image file returns unexpected content (Bug)**
    - *Why it matters:* Multimodal subagent orchestration is broken. The parent agent reads images correctly, but spawned subagents return hallucinated descriptions, undermining a key use case.
    - [GitHub](https://github.com/QwenLM/qwen-code/issues/4876)

### 4. Key PR Progress
*The 10 most important Pull Requests updated in the last 24h, covering features, stability fixes, and technical debt.*

1.  **PR #4842 — `feat(core): declarative agent frontmatter v1`** (OPEN)
    - *What it does:* A vertically-sliced implementation of Issue #4821. Bridges Claude Code’s `permissionMode` enum to Qwen's `approvalMode` and wires `maxTurns` and color allowlisting.
    - *Significance:* The foundational layer for a fully declarative agent ecosystem.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4842)

2.  **PR #4844 — `feat: Agent Team: parallel sub-agent coordination`** (OPEN)
    - *What it does:* An experimental mode allowing the model to spawn named sub-agents ("teammates") that work in parallel, message each other, and consolidate results.
    - *Significance:* Bold architectural move; represents the next generation of swarm/team execution in the roadmap.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4844)

3.  **PR #4823 — `fix(core): microcompact resumed goal continuations`** (CLOSED)
    - *What it does:* Makes long-running `/goal` loops eligible for the same stale tool-result cleanup as regular user turns.
    - *Why it matters:* Directly addresses the OOM issues in #4815 and #4838.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4823)

4.  **PR #4840 — `fix(core): microcompact hook continuations`** (OPEN)
    - *What it does:* Twin fix to #4823. Specifically targets Hook continuations (the Stop hook in `/goal` loops) to compact old tool results.
    - *Why it matters:* Ensures the fix covers all code paths in autonomous loops.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4840)

5.  **PR #4732 — `feat(core): Workflow tool P1 — node:vm sandbox + agent()` (OPEN)**
    - *What it does:* Ports "Dynamic Workflows" (Ultracode) from Claude Code. Implements a `Workflow` tool running JS in a `node:vm` sandbox with a sequential `agent()` global.
    - *Significance:* Major third tier of multi-agent execution alongside `/swarm`.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4732)

6.  **PR #4853 — `feat(core): enter_plan_mode tool and Plan Approval Gate`** (OPEN)
    - *What it does:* Allows the model to proactively self-lower into plan mode for complex tasks. Adds an approval gate when exiting plan mode in AUTO/YOLO modes.
    - *Significance:* Improves agent autonomy safety without hard-coding plan-only modes.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4853)

7.  **PR #4764 — `feat(memory): user-level auto-memory`** (CLOSED)
    - *What it does:* Adds a cross-project memory directory (`~/.qwen/memories/`), mirroring Claude Code's private/team scope. Closes Issue #4747.
    - *Why it matters:* Eliminates the need to re-learn user preferences in every new project.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4764)

8.  **PR #4871 — `refactor(core): remove GitService, migrate /restore to FileHistoryService`** (OPEN)
    - *What it does:* Removes the shadow-git-based `GitService` entirely, unifying file recovery under the existing `FileHistoryService`.
    - *Significance:* Major technical debt cleanup, simplifying the codebase and removing potential `git` edge cases.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4871)

9.  **PR #4833 — `feat(daemon): session idle reaper for automatic cleanup`** (OPEN)
    - *What it does:* Implements a two-layer session lifecycle cleanup (close-on-last-detach + idle timeout) for the daemon bridge.
    - *Why it matters:* Prevents session leaks in IDE-backed daemon processes, a key infrastructure upgrade.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4833)

10. **PR #4867 — `feat(web-shell): double-ESC clear, thinking block collapse, layout`** (OPEN)
    - *What it does:* Major UX polish for the web shell client: matching CLI double-ESC behavior, accurate thinking block line counting, and layout padding fixes.
    - *Why it matters:* Demonstrates ongoing investment in the Web UI as a first-class client.
    - [GitHub](https://github.com/QwenLM/qwen-code/pull/4867)

### 5. Feature Request Trends
- **Claude Code Parity (Dominant Theme):** The single strongest signal from the community is narrowing the gap with Claude Code. High-profile requests include **declarative agent YAML frontmatter** (#4821), **Dynamic Workflows / Ultracode** (#4721), **global user memory** (#4747), **dedicated `web_search` tool** (#4801), and **one-click config migration** (#4845).
- **Multi-Agent Orchestration:** Beyond parity, there is strong interest in **parallel agent execution** (PR #4844) and **background fork agents** (#4757), suggesting the community is ready to move past simple sequential swarms.
- **Daemon & Editor Integration:** Requests for **Streamable HTTP (ACP)** (#4782) and **session lifecycle management** (PR #4833) reflect a shift from CLI-first to IDE-integrated workflows.

### 6. Developer Pain Points
- **Memory Management in Long Sessions:** The most acute pain point. Severe OOM crashes on `--resume` (#4815) and unbounded context growth in `/goal` loops (#4838) are actively breaking production workflows.
- **Terminal UI / Vim Friction:** Power users are frustrated by Esc key leaks, mode indicator lag, and cursor handling bugs (#4675, #4852). These are daily impediments for Vim users.
- **Model Provider Configuration Confusion:** Managing multiple providers (OpenAI, DashScope, Ollama) is brittle. Users report that models with identical names from different providers get conflated in the UI (#4877).
- **CI & Release Process Immaturity:** The fact that a PR with failing CI can ship and break `tsc --build` (#4864) has shaken developer trust. Demand for automated CHANGELOGs (#4872) and stricter branch protection is rising.
- **Agent Reliability Regressions:** The subagent image reading bug (#4876) and the foreground sleep interception blocking legitimate API backoff (#4707) point to subtle but impactful regressions in agentic reliability.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**CodeWhale (formerly DeepSeek TUI) Community Digest — June 9, 2026**

---

### 1. Today’s Highlights
The community is navigating the final stages of the rebrand from `deepseek-tui` to `codewhale`, with a couple of migration snags still causing friction for `npm` and `cargo` users. On the development front, the project is aggressively expanding its model catalog, with Together AI and experimental OpenAI Codex support landing in the upcoming v0.8.55. A focused internationalization push from contributor Gordon Lu is also localizing deep TUI surfaces (sidebar, config, tool labels), rounding out a very productive 24 hours.

---

### 2. Releases
- **v0.8.54 [Latest]:** Shipped June 8th. Merges the stable v0.9.0 stewardship work. Delivers benchmark harvester runners (SWE-bench, Terminal-Bench, PinchBench), direct Xiaomi MiMo routing, community test harnesses, and the foundational `whaleflow` multi-agent orchestration crate.
- **v0.8.55 [Active Development]:** Maintainer Hmbown has opened PR #2916. Key targets are a dedicated Together AI provider profile and an experimental OpenAI Codex (ChatGPT OAuth) provider via the Responses API. Release-blocker issues (#2914, #2915) are being actively tracked.

---

### 3. Hot Issues

1.  **#2924 — Can’t update using npm** *(New)*
    *Synopsis*: Users stuck on the now-deprecated `deepseek-tui` npm package cannot update to `codewhale`. The migration path is not fully automated.
    *Reaction*: High immediate friction. Likely requires a documentation patch or a no-op stub package to smooth over the rename. [Link](Hmbown/CodeWhale Issue #2924)

2.  **#2917 — `codewhale` not found on PATH after Cargo update** *(New)*
    *Synopsis*: Cargo users who updated from `deepseek-tui` are hitting a `failed to spawn codewhale` error because the new binary name isn't aliased on PATH.
    *Reaction*: Classic rename pain. The community is looking for explicit upgrade guidance. [Link](Hmbown/CodeWhale Issue #2917)

3.  **#2893 — SiliconFlow provider config requires duplicate entries**
    *Synopsis*: Both `[providers.siliconflow]` and `[providers.siliconflow-CN]` must be populated identically. Defining only the region-specific variant silently fails.
    *Reaction*: A clear config UX regression (labeled "unreasonable action" by commenters). Active dev attention expected. [Link](Hmbown/CodeWhale Issue #2893)

4.  **#2641 — PDF `read_file` hangs without `pages` parameter**
    *Synopsis*: Calling `read_file` on a PDF without the `pages` argument causes the channel to hang and eventually error out. Specifying pages works normally.
    *Reaction*: High-severity default-behavior bug for document-heavy workflows. Commenters confirmed the workaround but flagged the default as broken. [Link](Hmbown/CodeWhale Issue #2641)

5.  **#2904 — Persistent agent state & compressed KV cache capsules**
    *Synopsis*: A detailed feature proposal to maintain agent state across sessions and leverage server-signed compressed KV cache capsules to cut cost/latency on long coding tasks.
    *Reaction*: Positive, technically deep discussion. Represents a long-term ambition for the agent runtime. [Link](Hmbown/CodeWhale Issue #2904)

6.  **#1327 — FreeBSD x86_64: Engine dispatch timeout**
    *Synopsis*: Persistent platform bug since May 9. Every prompt on FreeBSD 14.4 results in a "Turn dispatch timed out" error.
    *Reaction*: Low engagement but total blocker for the FreeBSD niche. Remains unresolved. [Link](Hmbown/CodeWhale Issue #1327)

7.  **#2922 — Agent excessively confirms YOLO mode**
    *Synopsis*: The agent re-asserts YOLO mode verbosely before every atomic operation (e.g., editing a CSS file).
    *Reaction*: UX annoyance. The community is questioning whether this confirmation level is intentional design or an oversight. [Link](Hmbown/CodeWhale Issue #2922)

8.  **#2900 — DSML tool calls rendered as plain text**
    *Synopsis*: The model randomly outputs DSML as text instead of executing it, wasting context and causing agent loop instability.
    *Reaction*: Critical reliability bug. Causes session corruption ("outputs for several minutes"). High priority for core stability. [Link](Hmbown/CodeWhale Issue #2900)

9.  **#2889 — Restored sidebar detail rows for Works/Tasks/Agents**
    *Synopsis*: A previously deleted community issue was resurrected to explore structured sidepanel inspection of complex agent runs.
    *Reaction*: Positive community stewardship. Signal that users want richer observability into multi-step workflows. [Link](Hmbown/CodeWhale Issue #2889)

10. **#2490 — Cannot compile Unreal Engine project**
    *Synopsis*: A game-development-specific bug where CodeWhale fails to correctly route UE build commands.
    *Reaction*: Niche but high-signal for the game dev contingent. Indicates deeper tool routing issues. [Link](Hmbown/CodeWhale Issue #2490)

---

### 4. Key PR Progress

1.  **#2916 — v0.8.55: Together AI + OpenAI Codex Provider**
    *Impact*: Major backend expansion. Together AI gets a native profile. The experimental Codex provider opens the door to ChatGPT OAuth flows. [Link](Hmbown/CodeWhale PR #2916)

2.  **#2753 — Multi-tab system with cross-tab collaboration**
    *Impact*: A massive TUI architecture change. Introduces `TabManager`, per-tab session persistence, and a `TaskDelegator` for cross-tab agent hand-offs. [Link](Hmbown/CodeWhale PR #2753)

3.  **#2920 — Migrate oversized paste files to `.codewhale/pastes/`**
    *Impact*: Final cleanup of rebranding artifacts. Prevents new sessions from writing into the legacy `.deepseek` directory. [Link](Hmbown/CodeWhale PR #2920)

4.  **#2921 / #2919 / #2918 / #2901 — i18n Localization Series (Gordon Lu)**
    *Impact*: Localizes sidebar panels, config edit modes, config sections/scopes, and tool family labels. Dramatically improves non-English UX. [Link](Hmbown/CodeWhale PR #2921) [+ others](Hmbown/CodeWhale PR #2919)

5.  **#2923 — Enable Volcengine provider in TUI dispatcher**
    *Impact*: Unlocks full TUI functionality for Volcengine Ark users instead of crashing on launch. [Link](Hmbown/CodeWhale PR #2923)

6.  **#2905 — Better `allow_shell` blocker diagnostics**
    *Impact*: UX improvement. When `allow_shell` is disabled, the error now explicitly names the confining setting instead of a generic "tool unavailable" message. [Link](Hmbown/CodeWhale PR #2905)

7.  **#2903 — Static Linux x64 builds with musl**
    *Impact*: Fully static binaries eliminate runtime glibc and libdbus dependencies, vastly improving distro portability. [Link](Hmbown/CodeWhale PR #2903)

8.  **#2902 — v0.8.54 Release (Merged)**
    *Impact*: Delivered the stable cut of Whaleflow, community test harnesses, and benchmark runners. [Link](Hmbown/CodeWhale PR #2902)

9.  **#2884 / #2881 / #2882 / #2883 — HUQIANTAO’s Bugfix Series (Merged)**
    *Impact*: Cleaned up 20+ bugs covering security (whitespace bypass), error handling (silent discards), concurrency (mutex poisoning), and HTTP client leakages. [Link](Hmbown/CodeWhale PR #2884)

10. **#2781 — Ghost-text follow-up prompt suggestions (Merged)**
    *Impact*: Mirrors Claude Code’s workflow. A lightweight model generates a dimmed follow-up question after each turn. Tab to accept or keep typing to ignore. [Link](Hmbown/CodeWhale PR #2781)

---

### 5. Feature Request Trends
- **Model/Provider Ecosystem Expansion:** A massive batch of issues today (#2906–#2915) came directly from the maintainer. The trend is clear: moving away from generic OpenAI-compatible configs toward **native provider profiles** (Together AI, OpenAI Codex, Volcengine) and **cutting-edge model support** (Qwen 3.7 Max, DeepSeek V4 Pro, Nemotron 3 Ultra, Kimi K2.6, MiniMax 2.7).
- **Internationalization (i18n):** The strongest development signal of the day. Gordon Lu has submitted a series of PRs targeting almost every TUI text surface for localization.
- **Advanced Agentic & Multi-Session Workflows:** The multi-tab system (#2753), Whaleflow orchestration (#2482), persistent state capsules (#2904), and sidebar agent inspection (#2889) point toward CodeWhale evolving from a chat TUI into a full agent IDE.

---

### 6. Developer Pain Points
- **Rebranding Migration Friction:** Two separate issues today (#2917, #2924) document compile-time and runtime failures caused by the `deepseek-tui` → `codewhale` rename. Users need clearer upgrade guides or automated path migration.
- **Provider Config Complexity:** The SiliconFlow regional config bug (#2893) and the historic model picker blindness (#2596) show that provider customization remains a consistent UX headache.
- **Agent Loop Reliability:** Core loop bugs are a top concern. The DSML-as-text rendering bug (#2900), excessive YOLO confirmations (#2922), and the PDF tool hang (#2641) erode user trust in the agent’s execution stability.
- **Platform Support Gaps:** The FreeBSD timeout (#1327) remains unresolved after a month, limiting the tool’s reach for that segment of developers.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*