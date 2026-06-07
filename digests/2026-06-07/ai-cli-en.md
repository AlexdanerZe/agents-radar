# AI CLI Tools Community Digest 2026-06-07

> Generated: 2026-06-07 03:35 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report — June 7, 2026

## 1. Ecosystem Overview

The AI CLI tools landscape is transitioning from experimental pair-programming assistants to robust, autonomous agent platforms. A clear "reliability plateau" has been reached, with Claude Code, OpenAI Codex, and Copilot CLI all shipping regressions that erode user trust in core workflows—history management, tool call integrity, and session stability. Simultaneously, the market is bifurcating: proprietary platforms deepen vertical integration (Codex's strict mode, Claude's Opus orchestration) while open-source projects build bridges to heterogeneous environments (Qwen's daemon mode, OpenCode's server API). The MCP (Model Context Protocol) has achieved ubiquitous adoption, yet fragmentation in its implementations—namespacing, auth, session handling—represents the ecosystem's single biggest integration tax. Community demands are coalescing around robust sandboxing, observable agent behavior, deterministic session management, and reliable cross-platform support.

---

## 2. Activity Comparison

| Tool | Issues (Notable) | PRs (Active) | Last 24h Release | Community Signal |
|---|---|---|---|---|
| **Claude Code** | High (10) | High (5) | **v2.1.168** | Top issue: 201 👍 (VM Bloat) |
| **OpenAI Codex** | High (10) | High (10) | None | Top issue: 103 👍 (Thread Deletion) |
| **Gemini CLI** | Moderate (10) | High (10) | None | Top issue: 8 👍 (Agent Hangs) |
| **Copilot CLI** | Moderate (10) | **None** | None | Top issue: 27 👍 (Input Hook) |
| **Kimi Code** | **None** | Low (2) | None | Core bug fixes (MCP crash, Images) |
| **OpenCode** | High (10) | High (10) | None | Top issue: 51 👍 (Sandboxing) |
| **Pi** | Moderate (10) | High (9) | None | Top issues: Input ergonomics, Latency |
| **Qwen Code** | High (10) | High (10) | **Nightly** | P1 Critical: OOM on `--resume` |
| **DeepSeek TUI** | High (10) | High (10) | None | **v0.9.0 release prep** |

**Summary:** Claude Code, OpenAI Codex, OpenCode, Qwen Code, and DeepSeek TUI show the highest overall development velocity. Gemini CLI and Pi demonstrate strong engineering rigor with moderate volume. Copilot CLI is in a reactive stabilization phase. Kimi Code is currently the quietest.

---

## 3. Shared Feature Directions

| Theme | Affected Tools | Specific Community Needs |
|---|---|---|
| **Agent Sandboxing & Security** | OpenCode (#2242, 51👍), Claude Code (subagent tools), Gemini (seatbelt), Pi (workspace approval), Qwen (MCP approval gating) | Restrict agent filesystem, network, and tool access; per-workspace security policies |
| **MCP Lifecycle & Interop** | **All 9 tools** | Standardized auth (OAUTH), crash resilience (Kimi, Claude, Codex), cross-provider compatibility (Codex namespacing), session persistence (Copilot) |
| **Session / History Reliability** | Codex (disappearing threads), Claude (truncated TUI), OpenCode (Infinite compaction loop), Qwen (OOM on resume), Pi (compaction error) | Predictable history rendering, stable compaction, reliable resume, no silent data loss |
| **Context Integrity** | Claude (`rg -rn` corruption), Copilot (compaction rewrites), Gemini (`$` prompt substitution) | Tool output must not be silently rewritten; user instructions must survive context window management |
| **Multi-Agent / Autonomous Workflows** | Claude (Opus→Sonnet tiered agents), OpenCode (Background task tool), DeepSeek (WhaleFlow), Gemini (Generalist subagents) | Orchestration of child agents, hierarchical planning, background task execution |
| **Local / BYOK Model Support** | Qwen (Ollama, vLLM), OpenCode (OpenAI-compat), Gemini (custom endpoints), Pi (local LLMs), Copilot (BYOK requests) | Self-hosted inference, lower-cost alternatives, heterogeneous model stacks |
| **IDE / Desktop Integration** | DeepSeek (VSCode Agent View), Claude (VSCode indicators), OpenCode (Desktop app), Codex (Desktop sidebar) | Moving beyond pure TUI; exposing agent state and session data in editor UIs |
| **Windows / WSL Robustness** | Copilot (CPU spike, startup delays), OpenCode (`/exit` kills terminal), Qwen (SMB path mangling), Claude (Windows LSP issues) | Systemic cross-platform failures; major barrier to enterprise adoption |

---

## 4. Differentiation Analysis

| Tool | Strategic Posture | Target User | Key Technical Bet |
|---|---|---|---|
| **Claude Code** | **Market pacesetter.** Ecosystem gravity well. | Professional developers, enterprises | Deep Anthropic model integration (Opus extended thinking), broadest plugin/MCP ecosystem. *Risk:* bloat and regression management. |
| **OpenAI Codex** | **Platform architect.** Betting on structural refactors. | Platform-focused teams, automation pipelines | Global Instruction lifecycle, Responses API strict mode. *Risk:* sacrificing desktop UX for platform flexibility. |
| **Gemini CLI** | **Safety & rigor champion.** Google-internal discipline. | Enterprise risk-managers, security-conscious teams | P1/P2 issue trackers, behavioral eval infrastructure, fast security patches. *Risk:* lower feature velocity vs. competitors. |
| **Copilot CLI** | **Workflow integrator.** Deepest GitHub/VS Code hooks. | Mainstream developer workflows | Seamless IDE integration. *Risk:* current defensive posture; regressions threaten "just works" value prop. |
| **Qwen Code** | **Open bridge.** Self-hosted and heterogeneous ecosystems. | Local model operators, OSS advocates | Daemon Mode B (ACP/REST parity), self-hosted LLM compatibility, rapid iteration. *Strength:* strongest BYOK story. |
| **OpenCode** | **Full-stack aspirant.** Desktop + CLI + Server API. | Open-source community, power users | Sandboxing (highest demand), V2 background agents, unified tool runtime. *Risk:* architectural churn vs. stability. |
| **DeepSeek TUI** | **UX innovator.** Pre-1.0 experimental plays. | Early adopters, feature seekers | Multi-tab sessions, ghost-text prompts, WhaleFlow workflow engine. *Risk:* low maturity, high instability potential. |
| **Pi** | **Config purist.** Terminal-first determinism. | Unix power users, config-heavy devs | XDG path layout, workspace approval system, extension API rigor. *Niche:* reproducible environments. |
| **Kimi Code** | **Quiet resolver.** Minimal public activity. | MCP / multi-modal terminal users | Focused patches on MCP crash resilience and image path handling. |

---

## 5. Community Momentum & Maturity

**High Volume / High Velocity**
- **Claude Code:** Largest voting user base (201👍 top issue). Development velocity is high, but quality control is strained—regressions ship alongside new features.
- **OpenAI Codex:** Highest platform maturity investment (10 major PRs today), but lowest desktop UX maturity (history, sidebar). Current refactoring phase is disruptive but strategic.
- **OpenCode:** Strongest open-source engagement (51👍 for sandboxing). Core runtime experiencing deep architectural overhaul—paying down technical debt.
- **Qwen Code:** Extremely high feature velocity. Daemon Mode B is converging quickly. Effectively shipping for the self-hosted market.
- **DeepSeek TUI:** Pre-1.0 "gold rush" energy. Highest novelty features, lowest stability maturity. Heavy feature delta per release cycle.

**Stabilizing / Deepening**
- **Gemini CLI:** Signals high engineering maturity (comprehensive evals, structured issue triage). Community volume is moderate but signal quality is high.
- **Copilot CLI:** High user base expectations, but current development cadence is defensive. PRs stalled, critical regressions unresolved.

**Niche / Low Volume**
- **Pi:** Smallest engaged community but highest signal-to-noise ratio for configuration and extension architecture.
- **Kimi Code:** Lowest activity of the cohort. Focused exclusively on patching critical defects. Community engagement metrics (issues, 👍) are negligible today.

---

## 6. Trend Signals

**1. The Reliability Plateau is Here**
The low-hanging fruit is gone. Tools are shipping regressions in core loops (tool calls, history, compaction) that break trust faster than new features build it. The engineering focus must shift from feature velocity to **systemic robustness**—circuit breakers for MCP failures, deterministic compaction, append-only history models. OpenCode's tool runtime hardening and Pi's eviction API are leading indicators of this necessary maturation.

**2. MCP is Ubiquitous, But Fragmented**
Every tool implements the Model Context Protocol, yet cross-tool interop is blocked by proprietary extensions (Codex namespacing), fragile auth (Claude OAuth trailing slash), and inconsistent lifecycle handling (Kimi, Copilot). Without standardization convergence, MCP risks becoming the "browser wars" of the AI agent era. Expect pressure for a formal compatibility test suite.

**3. The Daemon is the New CLI**
Qwen's Mode B and OpenCode's server API signal a fundamental shift: agents must persist, serve multiple clients, and operate asynchronously. The "always-on agent server" model is the logical successor to today's session-bound CLI. This enables richer IDE integration (DeepSeek, Claude VSCode extensions) and automates workflows beyond a single terminal.

**4. Trust in Autonomous Agents is Fragile**
False success reports (Gemini, Copilot), silent data corruption (Claude Code), and opaque error states (OpenCode) are powerful barriers to unattended agent execution. The industry needs **observability primitives**—token budgets, context pressure gauges, elapsed time, and clear audit trails—before teams will delegate critical pipelines to autonomous agents.

**5. Cross-Platform is Non-Negotiable, But Failing**
Windows/WSL bugs appear across *every* major tool: terminal crashes, CPU spikes, file path mangling, startup delays. This represents a systemic testing blind spot. For enterprise adoption, particularly in mixed-OS environments, solving Windows support is likely the highest-ROI engineering investment available.

**6. The BYOK Wave is Real**
The self-hosted and cost-sensitive developer segment is a key constituency. Qwen, OpenCode, and Gemini are actively capturing this market. The ability to run local models, swap API providers, and operate fully offline is a genuine differentiator in an ecosystem currently dominated by vendor lock-in (Claude, Codex, Copilot). Expect this demand to accelerate, forcing proprietary tools to offer competitive bring-your-own-key pricing or open-weight model access.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the current `anthropics/skills` activity.

---

## Claude Code Skills Community Highlights Report (June 2026)

### 1. Top Skills Ranking (Most-Discussed Pull Requests)

| Rank | PR | Skill Focus | Key Highlights & Discussion Themes | Status |
|---|---|---|---|---|
| 1 | [#83](https://github.com/anthropics/skills/pull/83) | **Meta-Skills: Quality & Security Analyzer** | Community self-governance at scale. Evaluates skills across structure, documentation, and security. Reflects demand for an internal quality gate as the ecosystem grows. | Open |
| 2 | [#1140](https://github.com/anthropics/skills/pull/1140) | **Agent-Creator & Multi-Tool Evaluation** | Defines a framework for creating task-specific agent sets. Highly discussed for fixing the parallel tool-use evaluation bottleneck and adding critical Windows compatibility. | Open |
| 3 | [#363](https://github.com/anthropics/skills/pull/363) | **Feature-Dev Workflow** | Repairs a critical `TodoWrite` overwrite bug that caused multi-phase workflows (e.g., design → QA) to skip phases. Directly addresses a painful DX issue for structured coding. | Open |
| 4 | [#514](https://github.com/anthropics/skills/pull/514) | **Document Typography** | A remarkably simple, high-impact fix: eliminates orphan words, widow headings, and numbering issues in generated documents. Appeals to the broadest user base. | Open |
| 5 | [#154](https://github.com/anthropics/skills/pull/154) / [#444](https://github.com/anthropics/skills/pull/444) | **Persistent Memory & Cognitive Frameworks** | Shodh-Memory provides cross-conversation state; AURELION gives a 5-floor structured reasoning architecture. Represents the frontier of stateful agentic skills. | Open |
| 6 | [#568](https://github.com/anthropics/skills/pull/568) / [#190](https://github.com/anthropics/skills/pull/190) | **Enterprise Platforms (ServiceNow, n8n, SAP)** | Deep specialization for enterprise tools. ServiceNow covers ITOM/SecOps, while n8n focuses on workflow automation. Signal strong demand for Claude as an enterprise platform expert. | Open |
| 7 | [#210](https://github.com/anthropics/skills/pull/210) | **Frontend-Design Skill Clarity** | A revision PR focused on making legacy skill instructions actionable within a single conversation context. Highlights the ongoing work to refine skill quality and actionability. | Open |

### 2. Community Demand Trends (From Issues)

Analyzing the top Issue threads reveals three clear demand vectors:

- **Tooling Reliability & Cross-Platform Parity (High Priority):** Multiple open issues (#556, #1099, #1050) report that the official evaluation harness (`run_eval.py`) fails on Windows or returns false negatives (0% trigger rate). The community is actively blocking on a stable, platform-agnostic development pipeline.
- **Enterprise Governance & Trust:** Issues (#228, #492, #1175) revolve around organizational controls. There is notable concern about trust boundary abuse (Issue #492 warns that community skills can impersonate the `anthropic/` namespace) and a strong request for org-wide skill sharing.
- **Standardization & Developer Experience:** The ecosystem is feeling growing pains. Issue #189 warns of skill duplication between plugins. Issue #202 calls for a complete overhaul of the `skill-creator` skill, which currently reads like developer documentation rather than an operational instruction set.

### 3. High-Potential Pending Skills (Active PRs Near Merge)

These actively discussed PRs represent the next wave of ecosystem maturity:

- **Windows & Filesystem Hardening (PR #538, #539, #541, #1050, #1099):** A concentrated cluster of fixes addressing case-sensitivity issues on Linux, YAML parsing failures, and subprocess handling on Windows. This is tactical work for the strategic goal of multi-OS support.
- **Testing Patterns Skill (PR #723):** Introduces a comprehensive `testing-patterns` skill covering the Testing Trophy model, unit tests, and React Testing Library. Directly addresses a core developer workflow that is currently missing from the official collection.
- **Skill-Creator Validation (PR #539):** A specific pre-parse validation fix for unquoted YAML descriptions containing colons (`:`). Small in scope, but indicative of a broader push to harden the skill creation pipeline against silent failures.

### 4. Skills Ecosystem Insight

The community’s single most concentrated demand is the **industrialization of the Skills development lifecycle**: the shift from ad-hoc script creation to a governed, secure, cross-platform, and quality-assured enterprise pipeline—driven almost entirely by the community’s own engineering contributions rather than official Anthropic tooling.

---

# Claude Code Community Digest — 2026-06-07

## 1. Today's Highlights
Today's release of **v2.1.168** delivers general reliability improvements, but community attention is focused on a wave of regression reports. A critical extended thinking display bug affecting Opus 4.7 ([#49268](https://github.com/anthropics/claude-code/issues/49268)) has now resurfaced identically on Opus 4.8 ([#63358](https://github.com/anthropics/claude-code/issues/63358)). Meanwhile, tool call parsing fragility ([#62123](https://github.com/anthropics/claude-code/issues/62123)) and a dangerous silent data corruption vector via ripgrep flag collisions ([#62016](https://github.com/anthropics/claude-code/issues/62016)) are dominating stability discussions.

## 2. Releases
- **[v2.1.168](https://github.com/anthropics/claude-code/releases/tag/v2.1.168)** — Bug fixes and reliability improvements.

## 3. Hot Issues
Top issues by community engagement and severity:

1. **[#22543 — Cowork VM Bloat](https://github.com/anthropics/claude-code/issues/22543)** *(201 👍, 75 comments)*  
   The Cowork feature generates a 10GB VM bundle on macOS, severely degrading startup time and UI responsiveness. The highest-voted open issue overall. Community is calling for lightweight alternatives or opt-in VM creation.

2. **[#62123 — Tool Call Parsing Error](https://github.com/anthropics/claude-code/issues/62123)** *(97 👍, 48 comments)*  
   Opus 4.7 users frequently hit *"The model's tool call could not be parsed (retry also failed)"*. Community analysis points to a serialization race specific to long-running sessions.

3. **[#49268 — Opus 4.7 Thinking Summaries Missing](https://github.com/anthropics/claude-code/issues/49268)** *(70 👍, 44 comments)*  
   Deep investigation traces the root cause to the harness failing to set `display: "summarized"` in the API call. A core UX regression that has persisted for weeks.

4. **[#63358 — Opus 4.8 Empty Thinking Blocks](https://github.com/anthropics/claude-code/issues/63358)** *(10 👍, 10 comments)*  
   A near-exact duplicate of #49268 now shipping with Opus 4.8. The API returns empty `thinking` fields, leaving extended thinking entirely invisible in the UI.

5. **[#28571 — Remote Control Resync Failure](https://github.com/anthropics/claude-code/issues/28571)** *(50 👍, 17 comments)*  
   Dropped connections between iOS remote control and local sessions silently swallow messages with no reconnection feedback. Critical for remote development workflows.

6. **[#23377 — GitHub Issue Prompt Too Long](https://github.com/anthropics/claude-code/issues/23377)** *(34 👍, 42 comments)*  
   A Windows-specific bug where GitHub issue prompts grow unbounded until the session stalls. Suggests a prompt accumulation defect in the issue management tool.

7. **[#29223 — Plan Upgrade Limits Not Reset](https://github.com/anthropics/claude-code/issues/29223)** *(27 👍, 20 comments)*  
   Upgrading a usage plan does not reset the current session's rate limits, forcing users to wait or restart sessions. A frustrating billing UX gap.

8. **[#52871 — MCP OAuth Trailing Slash](https://github.com/anthropics/claude-code/issues/52871)** *(14 👍, 17 comments)*  
   A trailing slash on the OAuth `resource` parameter breaks Entra ID (Azure AD) authentication entirely. A hard blocker for enterprise MCP adopters.

9. **[#62016 — `rg -rn` Silent Data Corruption](https://github.com/anthropics/claude-code/issues/62016)** *(8 👍, 2 comments)*  
   Ripgrep's `-r` flag is parsed as `--replace`, silently rewriting search output to the literal character `n`. Claude then misattributes the corrupted output. High risk for automated pipelines.

10. **[#28986 — VSCode Model & Thinking Indicators](https://github.com/anthropics/claude-code/issues/28986)** *(37 👍, 3 comments)*  
    A highly-requested QoL feature: show the active model and thinking mode state directly in the VSCode extension panel without needing to inspect configuration.

## 4. Key PR Progress
Five notable PRs were active in the last 24 hours:

1. **[#39370 — frontend-design-system Plugin](https://github.com/anthropics/claude-code/pull/39370) *(Merged)***  
   Adds a structured design workflow plugin: wireframes → OKLCH color tokens → implementation. Signals growing maturity in the plugin ecosystem for design-to-code handoff.

2. **[#65875 — Forward ANTHROPIC_BASE_URL](https://github.com/anthropics/claude-code/pull/65875) *(Open)***  
   Ensures the `agentic_review` child process inherits proxy/gateway base URLs (e.g., LiteLLM, Bifrost). Resolves silent authentication failures in enterprise routing setups.

3. **[#65919 — Document Subagent Plugin Limitations](https://github.com/anthropics/claude-code/pull/65919) *(Open)***  
   Adds essential documentation for a major footgun: subagents receive `CLAUDE_PLUGIN_ROOT` and `CLAUDE_PROJECT_DIR` as literal strings instead of resolved paths, breaking plugin-bundled file reads.

4. **[#65916 — Clarify `allowed-tools` Enforcement](https://github.com/anthropics/claude-code/pull/65916) *(Open)***  
   Critical security documentation clarifying that `allowed-tools` is an auto-approval filter, not a capability boundary. Only subagent `tools:` frontmatter provides a true hard restriction.

5. **[#65666 — Fix Dev Container Build](https://github.com/anthropics/claude-code/pull/65666) *(Merged)***  
   Repairs the project's dev container by removing domains blocked by DNS firewalls and adding a mechanism for injecting API keys via environment variables.

## 5. Feature Request Trends
- **Autonomous Agent Architecture**: Issue [#56913](https://github.com/anthropics/claude-code/issues/56913) crystallizes demand for tiered agent systems (Opus planners driving Sonnet workers) with persistent state, reflecting a shift from pair-programming to orchestration use-cases.
- **MCP Ecosystem Expansion**: Users want Gmail label management ([#36547](https://github.com/anthropics/claude-code/issues/36547)) and the ability to replace the built-in auto-memory backend with custom MCP servers ([#48465](https://github.com/anthropics/claude-code/issues/48465)).
- **IDE Transparency & Customization**: Persistent requests for real-time model/thinking indicators ([#28986](https://github.com/anthropics/claude-code/issues/28986)) and customizable chat UI theming ([#65857](https://github.com/anthropics/claude-code/issues/65857)) in the VS Code extension.
- **Globalization**: UI language localization support ([#31413](https://github.com/anthropics/claude-code/issues/31413)) continues to see community demand for broader international adoption.
- **LSP Deep Linking**: Monorepo support for `findReferences` across TypeScript project references ([#45625](https://github.com/anthropics/claude-code/issues/45625)) remains a pain point for large codebases.

## 6. Developer Pain Points
- **Tool Call Resilience**: The most consistent source of friction. Malformed or dropped tool calls ([#62123](https://github.com/anthropics/claude-code/issues/62123), [#64684](https://github.com/anthropics/claude-code/issues/64684), [#65965](https://github.com/anthropics/claude-code/issues/65965)) repeatedly break the core coding loop, particularly in long-context sessions.
- **Extended Thinking Regressions**: The same visualization bug affecting Opus 4.7 ([#49268](https://github.com/anthropics/claude-code/issues/49268)) has shipped unaddressed in Opus 4.8 ([#63358](https://github.com/anthropics/claude-code/issues/63358)), eroding trust in the model release pipeline's UX validation.
- **Silent Failures & Data Integrity**: The `rg -rn` flag collision ([#62016](https://github.com/anthropics/claude-code/issues/62016)) and remote resync failures ([#28571](https://github.com/anthropics/claude-code/issues/28571)) represent a class of bugs where errors surface as normal output or silent halts.
- **Usage Policy & Capacity Friction**: False-positive policy blocks on benign queries ([#59540](https://github.com/anthropics/claude-code/issues/59540), [#65973](https://github.com/anthropics/claude-code/issues/65973)) and unresponsive usage limit resets ([#29223](https://github.com/anthropics/claude-code/issues/29223), [#65942](https://github.com/anthropics/claude-code/issues/65942)) are creating unpredictable workflow interruptions.
- **Environment Configuration Friction**: PATH resolution issues on Windows LSP ([#59114](https://github.com/anthropics/claude-code/issues/59114)), hook state not persisting mid-session without restart ([#65953](https://github.com/anthropics/claude-code/issues/65953)), and third-party provider context detection ([#46416](https://github.com/anthropics/claude-code/issues/46416)) fragment the developer experience across platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

Here is the OpenAI Codex community digest for June 7, 2026.

---

## 1. Today’s Highlights
The Codex community is facing a significant Desktop reliability regression where project conversation histories disappear from the sidebar, prompting deep investigation and frustration across several high-comment threads. On the platform side, OpenAI engineers are actively executing a major architectural refactor of the global instruction lifecycle and MCP infrastructure, preparing the codebase for richer extension capabilities and reliable thread history management.

---

## 2. Releases
No new versions were published in the last 24 hours. The latest builds referenced across recent issue reports are Desktop 26.527–26.601 (Windows/macOS), the 0.135.0-alpha.1 tag, and CLI 0.113.0.

---

## 3. Hot Issues
Pick of the 10 most active discussions, ordered by community engagement.

- **[#20741 – Chat histories disappeared after recent update](https://github.com/openai/codex/issues/20741)** (29 comments, 14 👍)  
  Users report that all project chat histories vanished from the UI after an app update. Community responders confirm the data remains intact in `state_5.sqlite` / JSONL files. *Why it matters: erodes trust in the Desktop app as a reliable working memory.*

- **[#13018 – Allow deletion of threads instead of archiving](https://github.com/openai/codex/issues/13018)** (23 comments, 103 👍)  
  The highest-upvoted open issue. Users are frustrated that archiving does not free up sidebar clutter. The only current workaround is manual filesystem cleanup. *Why it matters: core UX workflow gap.*

- **[#21128 – Desktop silently hides sessions outside the recent-50 window](https://github.com/openai/codex/issues/21128)** (20 comments, 16 👍)  
  Provides a clear reproduction: the sidebar pagination drops older project threads without warning. *Why it matters: exposes a fundamental design flaw in the conversation indexing/pagination logic.*

- **[#23979 – History missing after update, state_5.sqlite data intact](https://github.com/openai/codex/issues/23979)** (16 comments, 4 👍)  
  Concrete technical evidence that the UI indexer fails post-upgrade even when the underlying SQLite database is healthy. *Why it matters: narrows the bug to the state migration or indexing pipeline.*

- **[#26234 – MCP namespacing blocks non-OpenAI providers](https://github.com/openai/codex/issues/26234)** (14 comments, 22 👍)  
  Local endpoints (Ollama, LM Studio, OpenRouter) cannot invoke MCP tools because Codex serializes them in a proprietary `"type": "namespace"` format that third-party models cannot parse. *Why it matters: blocks the entire local-first and custom-model community from using MCP.*

- **[#24510 – High CPU from unbounded thread metadata](https://github.com/openai/codex/issues/24510)** (13 comments)  
  The Desktop app-server sustains high CPU usage when a profile accumulates many active threads with large titles/previews. *Why it matters: performance degrades naturally with usage, penalizing power users.*

- **[#26843 – 137 GB disk writes leading to macOS hard reboot](https://github.com/openai/codex/issues/26843)** (3 comments)  
  A single long-running goal generated extreme write amplification, crashed WindowServer, and forced a power cycle. *Why it matters: indicates a severe I/O leak in the bundled runtime or session persistence.*

- **[#25744 – macOS zombie child processes](https://github.com/openai/codex/issues/25744)** (3 comments)  
  Computer Use / MCP sessions leave unreaped child processes, causing HID lag and WindowServer stalls. *Why it matters: the local subprocess lifetime model is not properly cleaned up.*

- **[#25820 – CLI login blocked by phone verification rate limit](https://github.com/openai/codex/issues/25820)** (10 comments)  
  Pro subscribers cannot authenticate the CLI due to aggressive OTP rate limiting. *Why it matters: directly blocks developer productivity and CI onboarding.*

- **[#26305 – CJK output duplicated into history](https://github.com/openai/codex/issues/26305)** (7 comments)  
  Streamed Chinese/CJK text is duplicated on each turn, causing runaway token growth and model limit errors. *Why it matters: renders the product unusable for CJK development tasks.*

---

## 4. Key PR Progress
Pick of 10 important pull requests updated in the last 24 hours.

- **[#26839 – Block project config permission overrides](https://github.com/openai/codex/pull/26839)**  
  Security fix that adds approval policy and sandbox mode validation to prevent config-based privilege escalation across all three desktop platforms.

- **[#26713 – Report unusable MCP OAuth credentials as logged out](https://github.com/openai/codex/pull/26713)**  
  Fixes a UX bug where expired tokens without a usable refresh flow were falsely reported as authenticated. Users now see a clear "login required" state.

- **[#26840 – Typed cross-platform path URIs](https://github.com/openai/codex/pull/26840)**  
  Foundational work introducing stable path identifiers that can refer to the current host or a remote environment without interpreting foreign path syntax.

- **[#26830–#26834 – Global Instruction Lifecycle Refactor (5 PRs)](https://github.com/openai/codex/pull/26830)**  
  A major architectural migration moving global instruction loading out of `Config` into a contributor-based extension system. Adds durable snapshots, explicit freshness tracking, and a `CODEX_HOME` contributor. Enables history-sharing threads and consistent subagent behavior.

- **[#26754 – Prepare side threads off the TUI event loop](https://github.com/openai/codex/pull/26754)**  
  Fixes a deadlock in `codex /side` by offloading fork operations from the main UI thread, preventing hangs when the main thread generates high event volume.

- **[#26719 – Enable standalone web search in code mode](https://github.com/openai/codex/pull/26719)**  
  Consumes plaintext search output and exposes `web.run` to nested JavaScript calls inside code mode, covering both direct and code-mode search paths with integration tests.

- **[#25704 – Normalize images for Responses strict mode](https://github.com/openai/codex/pull/25704)**  
  Feature-flagged pipeline that converts supported local/data URL images into prepared data before sending to `/responses`, unblocking strict-mode code execution.

- **[#26837 – Fetch installed plugins once](https://github.com/openai/codex/pull/26837)**  
  Performance fix in core-plugins that caches the installed plugin list, preventing repeated fetches on every hot-path query.

- **[#26818 – Accept prompts with `resume` and `fork`](https://github.com/openai/codex/pull/26818)**  
  Fixes Clap positional argument parsing so interactive `resume` and `fork` commands can accept a direct prompt string in addition to a session ID.

- **[#26686 – Propagate MCP client UI capabilities](https://github.com/openai/codex/pull/26686)**  
  Adds a semantic capabilities handshake to the MCP initialize flow, preserving absent/explicit-empty/populated UI profiles across thread start, resume, fork, and turn handling.

---

## 5. Feature Request Trends
Distilled feature signals from the wider issue set.

- **Thread Lifecycle Management**  
  The loudest demand is **native thread deletion** ([#13018](https://github.com/openai/codex/issues/13018), 103 👍) over the current archive-only model. Accompanying this is strong interest in **CLI session isolation** via `--worktree` / `--tmux` flags ([#12862](https://github.com/openai/codex/issues/12862), 71 👍) for reproducible coding sessions.

- **MCP & Local Model Parity**  
  Improving MCP tool serialization for non-OpenAI providers is the top extensibility request ([#26234](https://github.com/openai/codex/issues/26234), 22 👍). Users also want a **built-in quota-summary status line** ([#17457](https://github.com/openai/codex/issues/17457)) and timezone-aware rate limit messages ([#23019](https://github.com/openai/codex/issues/23019)).

- **Developer Productivity Tools**  
  Requests for an **in-app Prompt Snippets panel** ([#26467](https://github.com/openai/codex/issues/26467)) and **contextual selection toolbars** ([#25641](https://github.com/openai/codex/issues/25641)) signal a maturing user base optimizing daily workflows.

---

## 6. Developer Pain Points
Recurring frustrations and high-frequency friction zones.

- **History Reliability Crisis**  
  The overwhelming theme is the Desktop sidebar **hiding or losing local conversations**. Data is rarely permanently lost, but the UI consistently fails to index or display threads post-update or after accumulating many conversations. This forces manual file recovery and erodes trust in the "project" feature as a working memory store.

- **Long-Running Session Instability**  
  Power users report severe performance degradation (CPU spikes, multi-GB disk writes, zombie subprocesses) during long-running sessions, particularly on macOS ([#26843](https://github.com/openai/codex/issues/26843), [#25744](https://github.com/openai/codex/issues/25744)) and Windows ([#21232](https://github.com/openai/codex/issues/21232)).

- **Custom Model Friction**  
  Users running local or custom endpoints consistently face unique bugs absent from the standard ChatGPT path, such as CJK text duplication ([#26305](https://github.com/openai/codex/issues/26305)) and MCP namespace incompatibility ([#26234](https://github.com/openai/codex/issues/26234)).

- **Fragile Authentication Workflow**  
  The CLI login flow is sensitive to phone verification rate limits ([#25820](https://github.com/openai/codex/issues/25820)), creating an onboarding gate especially painful for Pro subscribers and automated environments.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — June 7, 2026**

---

## 1. Today's Highlights
This week’s digest finds the team prioritizing stability and security hardening alongside foundational agent improvements. Critical fixes for command injection vulnerabilities (#27575) and prompt corruption via `$` substitution (#27552) are in active review, while a new PR resolves model alias visibility for non-preview users (#27718). Community energy remains high around the persistent "Generalist Agent Hangs" (#21409) and the Auto Memory reliability family (#26516), signaling that core agent reliability and data privacy are the top user pain points.

---

## 2. Releases
No new releases were published in the last 24 hours.

---

## 3. Hot Issues
*Top 10 noteworthy issues by community activity and strategic importance.*

1. **[#21409 Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — [P1/Bug]
   The most heavily upvoted open issue (8 👍). Users report `gemini-cli` hangs indefinitely when deferring to the generalist agent for simple tasks like folder creation. A workaround exists (instructing the model not to use sub-agents), but the root cause remains unresolved. Strong community frustration.

2. **[#22323 Subagent recovery after MAX_TURNS reports GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — [P1/Bug]
   A critical trust issue: `codebase_investigator` hits its turn limit but falsely reports `status: "success"` and `Termination Reason: "GOAL"`. This misdirection erodes user confidence in agent state reporting and has drawn 2 👍 from concerned developers.

3. **[#25166 Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** — [P1/Bug | effort/medium]
   Repeated reports of the CLI hanging post-simple command execution (e.g., `ls`, `mkdir`) while displaying "Awaiting user input." A high-impact daily driver bug with 3 👍 demanding a fix in the shell execution lifecycle.

4. **[#21968 Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — [P2/Bug]
   A recurring community sentiment: custom skills and sub-agents are rarely invoked autonomously by the model, even when highly relevant. Users want deeper personalization but feel their configuration effort is being ignored by the agent’s routing logic.

5. **[#26525 / #26522 / #26516 Auto Memory bugs](https://github.com/google-gemini/gemini-cli/issues/26516)** — [P2/Bug Family]
   The Auto Memory subsystem is under a reliability crunch. Key sub-issues include: secret redaction happening *after* content is sent to the model (#26525), indefinite retrying of low-signal sessions (#26522), and silent skipping of invalid patches (#26523). This family of issues represents a significant data privacy and integrity concern.

6. **[#24353 Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** — [P1/Epic]
   A strategic P1 epic tracking the expansion of behavioral evaluation tests (76 generated so far). Indicates heavy internal investment in systematic eval quality, running across 6 supported models.

7. **[#22745 AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** — [P2/Investigation | 1 👍]
   An EPIC exploring AST awareness for precise method-bound reads and navigation. Users see this as a high-leverage way to reduce token waste and buggy file truncation. Connected to sub-issues #22746 and #22747.

8. **[#20079 Symlink not recognized as agent](https://github.com/google-gemini/gemini-cli/issues/20079)** — [P2/Bug]
   Custom agent `.md` files placed in `~/.gemini/agents/` via symlink are silently ignored. A sharp edge for developers using dotfile managers or centralized configurations.

9. **[#22267 Browser Agent ignores settings.json overrides](https://github.com/google-gemini/gemini-cli/issues/22267)** — [P2/Bug]
   The Browser Agent completely disregards configuration provided via `settings.json` (e.g., `maxTurns`). Despite the `AgentRegistry` correctly reading these values, the agent itself fails to apply them, acting as a "silent rebel."

10. **[#22672 Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** — [P2/Customer Issue | 1 👍]
    A safety-oriented request asking the agent to warn users before executing dangerous operations like `git reset --force` or risky database modifications. Underlines the community's need for guardrails in autonomous mode.

---

## 4. Key PR Progress
*10 important PRs updated or opened in the last 24 hours.*

1. **[#27718 fix(core): keep auto visible without preview access](https://github.com/google-gemini/gemini-cli/pull/27718)**
   Freshly opened by **he-yufeng**. Ensures the `auto` model alias remains visible in `/model` for users without preview access. Prevents confusion when dynamic model configuration is enabled. Includes regression coverage.

2. **[#27575 fix(security): prevent command injection in findCommand](https://github.com/google-gemini/gemini-cli/pull/27575)**
   Authored by **Ashutosh0x** (P2, size/m). Replaces vulnerable `execSync` calls with `spawnSync` in binary detection utilities, closing a shell metacharacter injection vector. A critical security hardening step.

3. **[#27591 fix(cli): fall back for oversized bug report URLs](https://github.com/google-gemini/gemini-cli/pull/27591)**
   Authored by **he-yufeng** (P2, size/m). Fixes `/bug` crashes on Android/Termux where deep-link intents exceed size limits. Falls back gracefully if the issue URL becomes too large.

4. **[#27580 fix(at-command): prevent stack overflow from regex backtracking](https://github.com/google-gemini/gemini-cli/pull/27580)**
   Authored by **Sauravdas007** (P1, size/m). Replaces the catastrophic backtracking regex-based `@` parser with an iterative scanner, preventing crashes on large pasted inputs. Fixes #27539.

5. **[#27552 fix(core): insert content literally into LLM prompts to avoid $ substitution](https://github.com/google-gemini/gemini-cli/pull/27552)**
   Authored by **Pluviobyte** (P2, size/m). Fixes a subtle corruption bug where `String.prototype.replace` interprets `$` patterns in user/content, silently mangling prompts before they reach the model.

6. **[#27555 fix(cli): stop merging shell history commands that end in a backslash](https://github.com/google-gemini/gemini-cli/pull/27555)**
   Authored by **Pluviobyte** (P2, size/m). Shell history is corrupted when a command ends in `\` (common in Windows paths like `dir C:\`). History entries are now read safely with trailing backslash handling.

7. **[#27405 fix(core): parse tools.callCommand before discovered tool execution](https://github.com/google-gemini/gemini-cli/pull/27405)**
   Authored by **fallintoplace** (P2, size/m). Fixes sandbox preparation by correctly parsing `callCommand` into program/argv before execution. Adds regression coverage for execution args.

8. **[#27398 fix(acp): accept string protocolVersion during initialize](https://github.com/google-gemini/gemini-cli/pull/27398)**
   Authored by **cyphercodes** (P2, size/m). Improves ACP interoperability by gracefully accepting string-format protocol versions before schema validation. Essential for federated agent compatibility.

9. **[#27385 Fix Node 20 Compatibility and Windows Symlink Test Failures](https://github.com/google-gemini/gemini-cli/pull/27385)**
   Authored by **kartikbhartiya**. Resolves a production `URL.parse` crash on Node 20.x and stabilizes platform-specific symlink tests on Windows. Important for runtime portability.

10. **[#27505 Prevent extra spaces on width-0 CJK continuation cells](https://github.com/google-gemini/gemini-cli/pull/27505)**
    Authored by **YowaiMo-Koustav** (P2, size/s). Fixes terminal rendering for CJK (wide) characters by preventing spurious whitespace injection that breaks copy-paste. An important globalization fix.

---

## 5. Feature Request Trends

- **AST-Aware Code Understanding (High Priority):** Multiple issues (#22745, #22746, #22747) push for Abstract Syntax Tree integration to improve codebase mapping, file reads, and search precision. This is seen as a major lever for reducing token waste and improving agent accuracy.
- **Remote & Federated Agents (Enterprise Shift):** The P1 Epic #20303 (Sprint 2) signals a clear push toward remote agent support, task-level auth, and background processing—pointing at team-scale and enterprise use cases.
- **Evaluation Infrastructure Maturation:** Epic #24353 and #23166 reflect deep investment in behavioral evals. The community and maintainers alike want reliable, non-flaky tests to track quality regressions across multiple models.
- **Agent Observability & "Self-Awareness":** #21432 captures a desire for the agent to accurately explain its own capabilities, flags, and hotkeys. Users want the agent to act as its own expert guide.
- **Memory System Transparency:** The #26516 family of bugs has evolved into a feature desire for a memory system that is deterministic, respects privacy, and transparently handles failures rather than retrying silently.

---

## 6. Developer Pain Points

- **Cascading Failures & Misleading States:** Issues like #21409 (agent hangs), #22323 (false GOAL success), and #25166 (stuck on input) create a high-friction environment where it is difficult to distinguish between a working system and a hung one.
- **Configuration & Customization Ignored:** The effort to personalize the CLI is often thwarted. Custom skills aren't invoked (#21968), settings overrides are ignored (#22267), and symlinked agents are silently skipped (#20079).
- **Prompt Integrity & Input Corruption:** Subtle bugs like `$` substitution (#27552) and regex-based stack overflows (#27580) erode trust in the quality of context being sent to the model.
- **Workspace Hygiene & Cleanup:** The agent's tendency to scatter temporary shell scripts across directories (#23571) and fragile cross-folder session resume create cleanup headaches for developers maintaining clean commits.
- **Cross-Platform & Edge Cases:** Wayland browser agent failures (#21983), Node 20.x crashes (#27385), and CJK rendering bugs (#27505) highlight the pain points of supporting diverse developer environments.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — June 7, 2026**

---

### 1. Today’s Highlights

The community is contending with several high-impact regressions in version 1.0.60, most urgently a WSL2 CPU spike that freezes the TUI ([#3700](https://github.com/github/copilot-cli/issues/3700)) and a context‑compaction bug that silently rewrites user instructions ([#3703](https://github.com/github/copilot-cli/issues/3703)). On the positive side, two critical MCP integration bugs—runaway server spawning ([#3701](https://github.com/github/copilot-cli/issues/3701)) and missing Session‑ID headers ([#3668](https://github.com/github/copilot-cli/issues/3668))—have been resolved. Feature demand remains strongest for an `awaitingUserInput` hook ([#1128](https://github.com/github/copilot-cli/issues/1128), 27 👍) and richer multimodal input support ([#1276](https://github.com/github/copilot-cli/issues/1276)).

---

### 2. Releases

No releases were published in the last 24 hours. The current stable version remains **1.0.60**. Patches for the MCP errors closed today are expected shortly.

---

### 3. Hot Issues

1. **[#3700](https://github.com/github/copilot-cli/issues/3700) — High‑Severity WSL2 CPU Regression**  
   MainThread pegs at ~215% CPU while idle on WSL2, freezing the TUI output until the CLI is restarted. A regression from the earlier #2208. (2 👍)

2. **[#3703](https://github.com/github/copilot-cli/issues/3703) — Context Compaction Corrupts User Instructions**  
   The agent rewrites user formatting rules (e.g., substituting em‑dashes when explicitly forbidden) during context compaction, causing serious output errors and eroding trust.

3. **[#3547](https://github.com/github/copilot-cli/issues/3547) — Background Agent Hangs with `gpt-5.5`**  
   Dispatched sub‑agents report `status: running` but sit at `total_turns: 0` forever when using the `gpt-5.5` model, effectively breaking background tasks for that model.

4. **[#3652](https://github.com/github/copilot-cli/issues/3652) — WSL Startup Delays of 40–80 Seconds**  
   Copilot Chat inside WSL suffers severe latency during session listing, making the remote development workflow painful for Windows users.

5. **[#3692](https://github.com/github/copilot-cli/issues/3692) — Escape Key Drops Queued Prompts**  
   Pressing Escape to stop a running task discards the user’s already‑typed next prompt instead of focusing it, causing unintentional work loss.

6. **[#3655](https://github.com/github/copilot-cli/issues/3655) — Autopilot Scope Creep**  
   The agent self‑answers clarifying questions and executes unrequested actions even after an explicit “stop,” raising serious usability and control concerns.

7. **[#3701](https://github.com/github/copilot-cli/issues/3701) — Runaway MCP Server Spawning *(CLOSED)* **  
   A loop of MCP server re‑initializations caused by an IDE lock‑file watcher on Windows was diagnosed and fixed in the latest builds.

8. **[#3668](https://github.com/github/copilot-cli/issues/3668) — MCP Session‑ID Header Not Persisted *(CLOSED)* **  
   The MCP client was dropping the `Mcp-Session-Id` header on subsequent requests, breaking remote HTTP MCP connections. Now resolved.

9. **[#1128](https://github.com/github/copilot-cli/issues/1128) — Feature Request: `awaitingUserInput` Hook**  
   The most upvoted open issue (27 👍). Developers need a hook that fires when the TUI is ready for input so they can automate or extend the interactive workflow.

10. **[#1276](https://github.com/github/copilot-cli/issues/1276) — Feature Request: Paste Images from Clipboard**  
    Users want to paste screenshots of code, UI bugs, or logs directly into prompts, closing a significant gap in multimodal support.

---

### 4. Key PR Progress

No pull requests were updated or merged in the last 24 hours. The development cadence appears focused on stabilizing the 1.0.60 release; the fixes for [#3701](https://github.com/github/copilot-cli/issues/3701) and [#3668](https://github.com/github/copilot-cli/issues/3668) are expected in an imminent patch.

---

### 5. Feature Request Trends

- **Model Diversity & Affordability**  
  Users are pushing for deeper model choice: multiple BYOK models in a single session ([#3282](https://github.com/github/copilot-cli/issues/3282)), lower‑cost / open‑weight options ([#3707](https://github.com/github/copilot-cli/issues/3707)), and broader free‑tier access beyond Claude Haiku 4.5 ([#3705](https://github.com/github/copilot-cli/issues/3705)).

- **MCP Production Readiness**  
  The community is moving beyond basic MCP support to demand granular permission scopes ([#3028](https://github.com/github/copilot-cli/issues/3028)), persistent session handling, and stable OAuth initialization ([#3706](https://github.com/github/copilot-cli/issues/3706)).

- **Richer Input / Output**  
  Image pasting ([#1276](https://github.com/github/copilot-cli/issues/1276)), proper RTL text rendering ([#3704](https://github.com/github/copilot-cli/issues/3704)), and customizable hooks for idle states ([#1128](https://github.com/github/copilot-cli/issues/1128)) are all trending upward.

- **Quality & Control**  
  Context integrity ([#3703](https://github.com/github/copilot-cli/issues/3703)) and agent scope adherence ([#3655](https://github.com/github/copilot-cli/issues/3655)) are being framed as features users are willing to advocate for aggressively.

---

### 6. Developer Pain Points

- **WSL2 Remains a Weak Link**  
  Two high‑severity WSL2 issues this week alone—startup delays and a total TUI freeze—signal that the Windows Subsystem for Linux experience is still brittle and a top source of friction.

- **Agent “Doesn’t Listen”**  
  The autopilot scope‑creep bug and the Escape‑key behavior both reinforce a perception that the agent is hard to control once started, diminishing developer trust.

- **Silent Failures Are the Most Dangerous**  
  Background agents hanging with zero turns and context compaction silently rewriting instructions are “stealth” bugs that waste developer time and undermine confidence in the tool’s reliability.

- **MCP Requires Too Much Babysitting**  
  Runaway processes, dropped sessions, and OAuth fan‑out loops show that while MCP is a powerful protocol, its current client implementation imposes significant operational overhead on everyday users.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-06-07**

---

### 1. Today’s Highlights
A quiet day for the Kimi CLI repository: no new releases, and zero issues were filed or updated. The project’s pulse comes entirely from the pull request queue, where two high-impact fixes from **he-yufeng** saw activity. PR #1769 tackles an unhandled `MCPRuntimeError` that bricks agents on connection failure, while PR #2183 resolves a race condition with image path handling in the shell (fixing issue #2182). The focus is squarely on runtime resilience and core UX reliability.

---

### 2. Releases
**None.**

---

### 3. Hot Issues
*(Total items updated in last 24h: 0)*

The issue tracker was completely dormant, but the active PRs directly target two critical open problems:

- **MCP Server Crash / UI Freeze (Driving PR #1769):**  
  When an MCP server fails to start (e.g., port conflict between TUI and Web UI sessions), `MCPRuntimeError` propagates uncaught through `_agent_loop()`, crashing the worker and leaving the user with a permanent “thinking” animation. This is a high-severity stability bug that undermines confidence in multi-session MCP workflows.  
  *Community reaction:* Minimal—the fix is being driven internally.

- **Image Drop Race Condition (Driving PR #2183, resolving #2182):**  
  Dropping an image file into the shell could fail because the temporary path expired before `ReadMediaFile` could access it. This made image-based prompting unreliable in terminal sessions.  
  *Community reaction:* The narrow scope of the fix suggests this was a pinpointed, repro-able bug affecting power users of multi-modal interactions.

---

### 4. Key PR Progress
*(Total items updated in last 24h: 2)*

- **PR #1769 – `fix: graceful degradation when MCP server fails to connect`**  
  *Author: he-yufeng | Updated: 2026-06-07 | State: OPEN*  
  [🔗 View PR](MoonshotAI/kimi-cli PR #1769)  
  **Summary:** Patches `_agent_loop()` in `kimisoul.py` to catch `MCPRuntimeError`. Instead of a hard crash that freezes the frontend, the worker degrades gracefully when an MCP server cannot start.  
  **Why it matters:** This is a critical reliability improvement for users running MCP servers alongside multiple Kimi sessions. It transforms a catastrophic failure into a recoverable error.

- **PR #2183 – `fix(shell): attach dropped image paths eagerly`**  
  *Author: he-yufeng | Updated: 2026-06-07 | State: OPEN*  
  [🔗 View PR](MoonshotAI/kimi-cli PR #2183)  
  **Summary:** Resolves issue #2182. When a model supports image input, the shell now scans the literal prompt text for local image paths, reads the image immediately, and sends it as an `ImageURLPart`. This avoids the race condition where a short-lived path expired before `ReadMediaFile` could process it.  
  **Why it matters:** Directly improves the UX of multi-modal terminal workflows. Moves from fragile deferred path resolution to eager synchronous attachment.

---

### 5. Feature Request Trends
With no new feature requests filed in the last 24 hours, the strongest signals come from the *types of bugs being fixed*:

- **Multi-Session & MCP Lifecycle Management**  
  The port conflict described in PR #1769 implies users want stable concurrent sessions (TUI + Web UI). The underlying demand is for robust connection pooling, per-session error isolation, and automatic retry or fallback behavior for MCP servers.

- **Synchronous / Immediate File Ingestion**  
  PR #2183 highlights a structural desire for the CLI to resolve external inputs (images, media) immediately at prompt time, rather than relying on async file watchers or temporary path passes. This suggests a community preference for “eager sidecar loading” over lazy resolution.

---

### 6. Developer Pain Points
- **Unhandled Exception Cascading to UI Freeze**  
  The core pain addressed today: an uncaught `MCPRuntimeError` in the agent loop takes down the entire worker process and hangs the UI. Developers expect MCP server failures to be isolated and logged, not to brick the whole tool.

- **Temp File Race Conditions in Async Pipelines**  
  The fragile interplay between file path creation and consumer timing (solved by #2183) is a recurring headache in terminal-based AI tools. The community wants predictable, immediate evaluation of provided resources over deferred asynchronous reads.

- **Silent PR Feedback Loop**  
  Both PRs show `undefined` comments and 0 👍. This silence may indicate the fixes address edge cases that aren’t yet widely encountered, or that the feedback channel from maintainers to community on these specific bugs is still one-way.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-07

## 1. Today's Highlights
The core runtime underwent a major architectural overhaul this week, with contributor `kitlangton` driving a series of refactoring PRs focusing on session coordination, provider isolation, and tool runtime hardening. Windows stability remains a critical pain point, with multiple reports of `/exit` crashing the parent terminal process—though a parallel fix for Windows search handle leaks in tests suggests active focus on this platform. Meanwhile, v1.16 continues to cause headaches for AWS Bedrock users, with regressions in SSO authentication and hanging model calls dominating provider-related discussion. Feature demand remains heavily weighted toward agent sandboxing and MCP tool management.

---

## 2. Releases
**No new releases in the last 24 hours.** The previous stable track remains v1.16.x, though the Bedrock regressions (#31147, #30858) suggest a patch release may be imminent.

---

## 3. Hot Issues

**#2242 — Is there a way to sandbox the agent?** (53 comments, 👍 51)
The most popular open feature request. Users want to restrict terminal/file access by agents, akin to macOS seatbelt used by gemini-cli and codex-cli. No equivalent exists in OpenCode yet. Strong community demand.
[🔗 Issue #2242](https://github.com/anomalyco/opencode/issues/2242)

**#4704 — `/undo` and `/timeline` undo does not revert file edits** (19 comments, 👍 16)
A critical workflow regression. Undo commands fail to revert file changes even in git-tracked projects, shattering user trust in the core editing loop. Logs and reproduction attached.
[🔗 Issue #4704](https://github.com/anomalyco/opencode/issues/4704)

**#16270 — `/sessions` TUI only shows recent sessions** (11 comments)
High-impact UX bug for power users. The session picker only shows ~5 sessions despite having hundreds in the database. Root cause identified in the TUI sync bootstrap timer (limited to 30 days).
[🔗 Issue #16270](https://github.com/anomalyco/opencode/issues/16270)

**#31147 — Regression: AWS Bedrock provider broken with SSO login in v1.16** (5 comments)
A blocker for enterprise teams. v1.16 returns a cryptic `Symbol` error when AWS credentials are fetched via SSO, preventing inference entirely. Reported alongside #30858 (Bedrock hangs). Ecosystem trust issue.
[🔗 Issue #31147](https://github.com/anomalyco/opencode/issues/31147)

**#27749 / #28673 / #30495 — `/exit` kills parent terminal on Windows** (Combined ~10 comments)
A cluster of reports confirming that `/exit` and Ctrl+C on Windows terminate the parent shell (pwsh/cmd) instead of returning to the prompt. Regression since v1.14.25. Affects basic terminal hygiene.
[🔗 Issue #27749](https://github.com/anomalyco/opencode/issues/27749)

**#26846 — Opencode segfaults in NixOS+WSL** (5 comments, 👍 8)
Niche but severe. Running opencode inside WSL with NixOS leads to immediate segfault. Affects both the unstable nixpkgs channel and direct GitHub builds.
[🔗 Issue #26846](https://github.com/anomalyco/opencode/issues/26846)

**#31152 — Infinite compaction loop on every response** (1 comment, new)
Peculiar and severe bug. Even with zero config and empty sessions, every message triggers a build/compaction loop. Low engagement so far, but high severity if reproduced widely.
[🔗 Issue #31152](https://github.com/anomalyco/opencode/issues/31152)

**#31155 — Illegal instruction crash on older CPUs (missing AVX2)** (2 comments)
Windows binary fails on CPUs lacking AVX2 support. Even the "baseline" binary appears to fail, leaving some hardware completely unsupported.
[🔗 Issue #31155](https://github.com/anomalyco/opencode/issues/31155)

**#21090 — "Model tried to call unavailable tool"** (3 comments)
A recurring source of user confusion. Models attempt to call tools that aren't available in their context, but error messaging is opaque. Points to a need for better tool registration/validation feedback.
[🔗 Issue #21090](https://github.com/anomalyco/opencode/issues/21090)

**#30545 — Desktop file tree broken** (8 comments)
Desktop v1.15.13 Advanced Settings (File tree) have no effect after enabling. Remains ineffective after restart. Affects Desktop UI navigation.
[🔗 Issue #30545](https://github.com/anomalyco/opencode/issues/30545)

---

## 4. Key PR Progress

**#31181 — refactor(core): specialize session run coordination** (kitlangton)
Replaces the oversized generic coordinator with per-session actor lanes. A deep architectural lift for concurrency and state management—laying groundwork for better multi-session resilience.
[🔗 PR #31181](https://github.com/anomalyco/opencode/pull/31181)

**#31176 — refactor(core): isolate provider turn runner** (kitlangton)
Extracts provider-turn streaming, tool settlement, and overflow retry from the session runner. Improves maintainability and reduces complexity in `llm.ts`.
[🔗 PR #31176](https://github.com/anomalyco/opencode/pull/31176)

**#31171 — fix(core): harden unified tool runtime** (kitlangton)
Makes tool calls more robust: durably fails unsettled calls, atomic registration, bounded output, and removes duplicate counting. Directly addresses reliability patterns seen in user reports.
[🔗 PR #31171](https://github.com/anomalyco/opencode/pull/31171)

**#31173 — feat(core): add V2 background task tool** (kitlangton)
Introduces a new `task` tool for spawning one-off child sessions with validated subagent config. Enables multi-agent orchestration with both foreground (blocking) and background (fire-and-forget) modes.
[🔗 PR #31173](https://github.com/anomalyco/opencode/pull/31173)

**#31132 — fix(tui): load root sessions safely in dialogs** (CasualDeveloper)
A direct fix for #16270 and #31125. Ensures session dialogs load all root sessions instead of mixing or truncating data. Supersedes four prior attempts (#23276, #24383, #26432). High impact.
[🔗 PR #31132](https://github.com/anomalyco/opencode/pull/31132)

**#31185 — fix(tui): enable client-side filtering for session search dialogs** (malventano)
Fixes the broken search filter in session dialogs where typing did not filter results. Targeted patch for TUI usability.
[🔗 PR #31185](https://github.com/anomalyco/opencode/pull/31185)

**#31049 — refactor(server): canonicalize service API** (thdxr)
Promotes the experimental server API to canonical names, organizes route groups, handlers, and middleware. Standardizes core defaults and CLI daemon startup. A large structural change.
[🔗 PR #31049](https://github.com/anomalyco/opencode/pull/31049)

**#31052 — fix(provider): keep compacted Anthropic tool histories user-led** (codeg-dev)
Normalizes Anthropic message histories in compacted sessions, fixing trailing assistant prefills and prefilled user tool results. Important for provider correctness.
[🔗 PR #31052](https://github.com/anomalyco/opencode/pull/31052)

**#5903 — feat(tui): Allow keybinding of custom slash commands** (ariane-emory)
Ties custom slash commands to user-defined keybindings. Long-running open PR addressing a high-demand productivity feature.
[🔗 PR #5903](https://github.com/anomalyco/opencode/pull/5903)

**#30091 — fix(session): settle pending tool calls on schema errors** (codeg-dev)
Resolves a class of silent failures where schema validation errors left tool calls in a pending state. Now settles them to error state properly.
[🔗 PR #30091](https://github.com/anomalyco/opencode/pull/30091)

---

## 5. Feature Request Trends

- **Security & Sandboxing (🔥 Highest Demand):**
  The overwhelming volume on #2242 (51 👍) signals that users need agent process/file sandboxing before putting OpenCode to work on sensitive projects.

- **MCP Tooling Control & Optimization:**
  Strong demand for per-agent MCP filtering (#28662) and dynamic/lazy loading of MCP schemas (#17482) to manage context bloat and tool-count model limits.

- **Extended Provider & Integration Support:**
  Requests for OpenAI-compatible endpoint support for the Go model (#30244), system prompt environment data APIs (#31158), an Antigravity CLI connector (#31066, recently merged), and better plugin documentation (#3067) reflect a maturing ecosystem.

- **Desktop/Workflow Enhancements:**
  Native commit actions in the Desktop UI (#18152) and custom slash command keybindings (#5903) are popular items aiming to reduce reliance on terminal tools.

---

## 6. Developer Pain Points

- **Windows Terminal Exit Instability:**
  A recurring frustration cluster (#27749, #28673, #30495) where `/exit` or Ctrl+C kills the parent shell or crashes `conhost.exe`. This is a fundamental UX failure for Windows users that persists across recent versions.

- **v1.16 Provider Regressions:**
  The 1.16 release introduced blocking issues for AWS Bedrock users (SSO auth broken #31147, hanging model calls #30858) and severe Desktop UI freezes on large diffs (#30906). Confidence in the release track is suffering.

- **Undo/Workflow Reliability:**
  The non-functional `/undo` (#4704) is a hard blocker for iterative development. If AI-generated edits cannot be reliably reverted, the tool becomes high-risk for daily use.

- **Session Management Friction:**
  Power users are hitting hard ceilings: the `/sessions` picker is artificially truncated (#16270), the `/project` API returns incomplete lists (#16025), and switching projects can drop sessions (#30826). The management layer needs a rethink.

- **Agent/Tool Debugging Opacity:**
  Custom subagents fail with bare `"Error"` messages (#31179), models call unavailable tools with no guidance (#21090), and schema errors leave tool calls pending (#30091). Error handling and observability are consistent pain points.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-07

**Data Source:** `github.com/earendil-works/pi`

---

## 1. Today's Highlights

A flurry of bug fixes landed today, resolving critical auto-compaction crashes (#5463), Markdown rendering in the TUI (#5462), and local model latency issues (#5464). A significant feature PR from mitsuhiko introduces an approval system for workspaces (#5332), strengthening security for team-based configurations. Meanwhile, TUI input ergonomics remain a hot topic, with a persistent `shift+enter` mapping bug (#5188) drawing community attention alongside a fix for Tab autocomplete submission (#5450).

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues (10 notable picks)

**#5188 (OPEN)** – *Shift+Enter submits instead of creating a new line*  
Despite explicit keybinding configuration (`tui.input.newLine`), `shift+enter` bypasses the mapping and triggers submit. High engagement (7 comments, 2 👍). A core UX friction point.  
🔗 [earendil-works/pi#5188](https://github.com/earendil-works/pi/issues/5188)

**#5464 (CLOSED)** – *Local models: 3-5 minute "Working" latency on basic messages*  
A critical performance blocker for Ollama users. Simple messages mid-session introduce multi-minute "Working" stalls. Fixed in today's update.  
🔗 [earendil-works/pi#5464](https://github.com/earendil-works/pi/issues/5464)

**#5418 (OPEN)** – *Invalid models.json crashes during migration without showing file path*  
Exposes a raw `JSON.parse` stack trace. Offers zero user guidance on which file is broken—a clear diagnostic failure.  
🔗 [earendil-works/pi#5418](https://github.com/earendil-works/pi/issues/5418)

**#5462 (CLOSED)** – *Markdown code blocks render literal triple-backtick fences in TUI*  
Rendered Markdown in the terminal looks identical to raw source markup, undermining the TUI's core promise.  
🔗 [earendil-works/pi#5462](https://github.com/earendil-works/pi/issues/5462)

**#5291 (CLOSED)** – *Sessions hang on "Working" when used with Anthropic subscription*  
Enterprise Anthropic users face intermittent, simultaneous session freezes. Standard interrupt/stop often fails to recover.  
🔗 [earendil-works/pi#5291](https://github.com/earendil-works/pi/issues/5291)

**#5456 (CLOSED)** – *openai-responses provider ignores `compat.supportsDeveloperRole`*  
Forces `role: "developer"` on providers that explicitly disable it (e.g., Gemini via Vertex), causing silent compatibility failures when `model.reasoning` is enabled.  
🔗 [earendil-works/pi#5456](https://github.com/earendil-works/pi/issues/5456)

**#5463 (CLOSED)** – *Auto-compaction after final turn throws unhandled error*  
Triggers `Cannot continue from message role: assistant` on valid session endings. Directly impacts session completion stability.  
🔗 [earendil-works/pi#5463](https://github.com/earendil-works/pi/issues/5463)

**#5301 (CLOSED)** – *Towards opt-in XDG path layout*  
A fresh attempt by kamalmarhubi to centralize directory resolution behind a `Paths` object, acknowledging but navigating around prior resistance (#534, #2870, #3310).  
🔗 [earendil-works/pi#5301](https://github.com/earendil-works/pi/issues/5301)

**#5461 (CLOSED)** – *Allow extensions to durably evict injected context mid-session*  
Proposes an API to exclude previously-injected context from session projections and compaction while keeping history append-only.  
🔗 [earendil-works/pi#5461](https://github.com/earendil-works/pi/issues/5461)

**#5454 (CLOSED)** – *Arrow key prompt navigation interferes with multiline editing*  
Cursor movement within the current prompt text takes precedence over cycling input history when a prompt spans multiple lines.  
🔗 [earendil-works/pi#5454](https://github.com/earendil-works/pi/issues/5454)

---

## 4. Key PR Progress

**#5332 (CLOSED)** – *feat(config): Approval system for workspaces*  
Submitted by mitsuhiko. Adds a `.pi.user` folder for user extensions and requires explicit interactive approval (or `-f` flag) for loading `.pi` and `.pi.user` directories. A substantial security improvement for shared configs.  
🔗 [earendil-works/pi#5332](https://github.com/earendil-works/pi/pull/5332)

**#5450 (CLOSED)** – *fix(tui): Make Tab submit slash commands from autocomplete like Enter*  
Fixes an inconsistency where Tab accepted the autocomplete text but left the slash command unsubmitted, creating a confusing half-state.  
🔗 [earendil-works/pi#5450](https://github.com/earendil-works/pi/pull/5450)

**#5451 (CLOSED)** – *Fix security issue in vitest*  
A security patch for the vitest test runner dependency was merged.  
🔗 [earendil-works/pi#5451](https://github.com/earendil-works/pi/pull/5451)

**#5452 (CLOSED)** – *Codex/readme install rewrite*  
Significant overhaul of installation documentation to improve clarity and reduce onboarding friction.  
🔗 [earendil-works/pi#5452](https://github.com/earendil-works/pi/pull/5452)

**#5440 / #5441 (CLOSED)** – *Codex/native subagents*  
Twin PRs by Piercekaoru exploring a native subagents feature within the Codex framework. Involve substantial refactoring of the agent architecture.  
🔗 [earendil-works/pi#5440](https://github.com/earendil-works/pi/pull/5440) | [earendil-works/pi#5441](https://github.com/earendil-works/pi/pull/5441)

---

## 5. Feature Request Trends

- **Declarative Team Workspaces & Reproducibility:** A strong push toward Nix-like determinism for agent configs. #2908 (CREAM) and #5332 (Workspace Approval) reflect growing demand for reliable, shareable team environments.
- **Extension API Maturation:** Multiple requests—#5461 (Context Eviction), #5455 (Export RPC Types), #5459 (Spirit Prompt Metadata)—indicate users are building on the extension API and need richer, self-documenting SDK primitives.
- **Configuration Control & Portability:** Users want stricter control over default persistence (#3254) and filesystem layout (#5301) to avoid side effects from ephemeral switches and support multi-machine workflows.
- **TUI Quality-of-Life Improvements:** Beyond bug fixes, features like the copy button in the control panel (#5457) signal a drive to polish the terminal experience into a proper power-user tool.

---

## 6. Developer Pain Points

- **Unreliable “Working…” Status:** The most painful recurring theme. Sessions freezing on "Working..." affected both cloud (Anthropic #5291) and local (#5464) providers, severely eroding user trust in session reliability.
- **Opaque Error Diagnostics:** Configuration errors (bad JSON #5418) and agent logic errors (#5463) dump raw stack traces without actionable context, forcing developers to reverse-engineer failures.
- **Inconsistent TUI Input Model:** The simultaneous existence of a “Tab fails to submit” fix (#5450) and an unresolved “Shift+Enter submits instead of newline” bug (#5188) signals a fragmented input event handling pipeline that needs architectural attention.
- **Provider Protocol Edge Cases:** The `openai-responses` provider ignoring `compat` flags (#5456) creates a class of hard-to-diagnose silent integration failures, particularly for non-standard or self-hosted API providers.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-07

## Today's Highlights
The `qwen serve` daemon (Mode B) development accelerates sharply: a massive ACP/REST parity PR (+935 lines, 29 methods) and a WebSocket transport PR are now in review, alongside a full-stack web-shell `/settings` command. On the stability front, a fix for the critical **OOM crash** with `--resume` (#4815) has been submitted, while the community continues to flag keybinding friction and rendering regressions in compact mode. The total open issue count remains high at 29 items, signaling strong engagement but also growing pressure on tooling reliability.

---

## Releases
**v0.17.1-nightly.20260607.cef26a86a** — A standard nightly release on the `release/v0.17.1-nightly` branch containing chore updates and CI infrastructure changes. No user-facing feature changes in this specific build.

---

## Hot Issues

**1. [#4815 [P1] Severe OOM with `qwen --resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)** — *zzhenyao*
A critical memory bug where `--resume` triggers old-space exhaustion within minutes. The Escape key also becomes completely non-functional. The community has engaged heavily (8 comments), as session resumption is a core workflow. A targeted fix is already proposed in PR #4824.

**2. [#4675 Vim INSERT mode Esc key leak and mode indicator lag](https://github.com/QwenLM/qwen-code/issues/4675)** — *zzhenyao*
Pressing Esc in Vim INSERT mode incorrectly triggers the application-level Esc handler, clearing buffers or interrupting model responses. This friction between Vim emulation and app shortcuts is a recurring complaint among terminal-purist users.

**3. [#4794 [P2] Compact mode tool merge causes full-screen flash](https://github.com/QwenLM/qwen-code/issues/4794)** — *zzhenyao*
Merging compact tool groups in Ink causes a full re-render flash. For users in compact mode, this creates a persistent visual disruption on every tool batch, degrading the long-session experience.

**4. [#4825 Feature: `qwen sessions list` with `--json`, `--tag`, and date filters](https://github.com/QwenLM/qwen-code/issues/4825)** — *fuleinist*
A strong signal of the tool's adoption in scripting and CI pipelines. Users want programmatic enumeration of stored sessions (`~/.qwen/history/`) without writing custom parsers.

**5. [#4821 Feature: Declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)** — *qqqys*
Directly inspired by Claude Code's `.claude/agent` pattern. The community is actively requesting YAML/Markdown-based agent definitions to avoid TypeScript compilation for custom workflows.

**6. [#4782 Tracking: ACP Streamable HTTP transport implementation and RFD alignment](https://github.com/QwenLM/qwen-code/issues/4782)** — *chiga0*
The strategic roadmap for ACP parity. Editors like **Zed**, **Goose**, and **JetBrains** can already connect to `qwen serve` without adapters. This issue tracks the remaining upgrade path to full standard compliance.

**7. [#4175 [42 comments] Mode B feature-priority roadmap toward v0.16 production-ready](https://github.com/QwenLM/qwen-code/issues/4175)** — *doudouOUC*
The canonical hub for daemon feature discussions. With 42 comments and high traffic, it outlines the phased rollout from "1 daemon = 1 workspace" to full session multiplexing and auth.

**8. [#4720 SMB shared folder access broken with absolute path space insertion](https://github.com/QwenLM/qwen-code/issues/4720)** — *MAYJINSOURCE-69214*
Windows users face a frustrating bug where Qwen Code cannot access mapped network drives and inserts stray spaces into absolute paths, completely blocking file operations in shared workspace environments.

**9. [#4700 Infinite loops and failure to read `@` images autonomously](https://github.com/QwenLM/qwen-code/issues/4700)** — *MAYJINSOURCE-69214*
The agent enters an infinite `readFile` loop and fails to process `@image` attachments unless explicitly instructed. This highlights gaps in tool-calling termination conditions and vision context handling in v0.17.

**10. [#4657 v0.17.0 + Ollama / Qwen-3.6: Tasks fail to complete](https://github.com/QwenLM/qwen-code/issues/4657)** — *QuantumAIStudio*
Despite earlier timeout fixes, local LLM integrations continue to underperform. Tasks that previously worked (e.g., generating an HTML ebook) now fail silently or hang, frustrating the self-hosted user segment.

---

## Key PR Progress

**1. [#4824 `fix(core): prevent OOM by compacting API history...`](https://github.com/QwenLM/qwen-code/pull/4824)** — *zzhenyao*
Three targeted fixes for the OOM in #4815: microcompaction on Hook messages, UI history hard-purge, and explicit GC triggering under memory pressure. A high-priority merge for session stability.

**2. [#4827 `feat(serve): ACP/REST parity — 29 new _qwen/* methods`](https://github.com/QwenLM/qwen-code/pull/4827)** — *chiga0*
A massive +935 line PR achieving full REST route parity through the ACP dispatch layer. Includes session extensions (recap, btw, shell detach), workspace CRUD, and file operations. Replaces earlier auto-closed wave PRs.

**3. [#4773 `feat(serve): ACP WebSocket transport (RFD Streamable HTTP phase 2)`](https://github.com/QwenLM/qwen-code/pull/4773)** — *chiga0*
Rebased on `daemon_mode_b_main`. Extracts a `TransportStream` interface and adds a `WsStream` adapter, enabling real-time bidirectional communication for ACP-native clients. Depends on #4827.

**4. [#4816 `feat(serve): add /settings slash command for web-shell`](https://github.com/QwenLM/qwen-code/pull/4816)** — *doudouOUC*
Full-stack implementation of `/settings` for the web-shell: daemon API routes (GET/POST), SDK client methods, React hooks (`useSettings`), and event wiring. A significant UX milestone for Mode B.

**5. [#4829 `fix(auth): time out Qwen OAuth refresh`](https://github.com/QwenLM/qwen-code/pull/4829)** — *he-yufeng*
Adds a 30-second timeout to OAuth refresh-token fetches. Directly resolves the CLI startup hang on offline/internal networks reported in #4550, a common pain point for enterprise users.

**6. [#4822 `feat(serve): add hooks diagnostic HTTP/ACP surface`](https://github.com/QwenLM/qwen-code/pull/4822)** — *doudouOUC*
Adds read-only endpoints (`GET /workspace/hooks`) for querying hook configuration status. Enables remote clients and web-shell to inspect workspace/session hooks without TUI dependency.

**7. [#4764 `feat(memory): add user-level auto-memory at ~/.qwen/memories/`](https://github.com/QwenLM/qwen-code/pull/4764)** — *LaZzyMan*
Mirrors Claude Code's `private`/`team` scope design by introducing a cross-project user memory directory. Reuses Qwen's existing 4-type taxonomy but persists facts about the user's global preferences and working style.

**8. [#4713 `feat(mcp): project .mcp.json + workspace approval gating`](https://github.com/QwenLM/qwen-code/pull/4713)** — *qqqys*
Adds approval gating for untrusted, checked-in MCP sources and a coherent cross-source precedence model. Aligns Qwen Code's MCP handling directly with Claude Code's `.mcp.json` security model.

**9. [#4793 `fix: coerce non-string tool params to strings for self-hosted LLMs`](https://github.com/QwenLM/qwen-code/pull/4793)** — *launchswitch*
Fixes `SchemaValidator` rejections when self-hosted models (LMStudio, vLLM, sglang) return numbers or booleans for string parameters like `old_string`. A targeted fix for the self-hosted UX.

**10. [#4665 `Add InstructionsLoaded hook for instruction file loading`](https://github.com/QwenLM/qwen-code/pull/4665)** — *qqqys*
Enhances the hook system by firing an event when instruction/context files are loaded during memory discovery or `@` imports. Provides the payload path, memory source, and trigger metadata for extension authors.

---

## Feature Request Trends

- **Daemon (Mode B) Production Readiness:** The dominant vector of feature requests. Users are pushing for full ACP standard compliance (Streamable HTTP, WebSocket), web-shell UI controls (settings, rewind, directory management), and production hardening (OpenTelemetry, auth resilience).
- **Declarative Agent Definitions:** Strong interest in Claude Code-style `.claude/agent` patterns. The community wants YAML/Markdown frontmatter files to define custom agents without TypeScript compilation.
- **Enhanced Session Management:** A clear gap exists in programmatic session control. Requests for `qwen sessions list` with JSON output, tagging, and date filtering indicate growing CI/CD and automation use cases.
- **Memory Architecture Evolution:** Beyond project-level memory, users want cross-project "user memories" (preferences, background) and guaranteed context persistence across task interruptions.
- **MCP Standardization:** Users want Qwen Code to match or exceed Claude Code's MCP handling, including `.mcp.json` security gating, declarative server configs, and approval workflows.

---

## Developer Pain Points

- **OOM and Long-Session Stability:** Memory leaks (especially with `--resume`), infinite tool loops, and UI freezes under long context windows remain the top reliability blockers. The P1 classification of #4815 reflects this urgency.
- **Vim/Keybinding Friction:** Repeated reports of Esc key leaking to application context, Ctrl+C causing unintended exits in IDEs (PyCharm), and Vim mode indicator lag. These significantly disrupt muscle-memory-dependent workflows.
- **Local/Self-Hosted Model Incompatibility:** Users of Ollama, vLLM, and LMStudio face persistent task failures, schema validation errors, and garbled output. Compatibility with non-standard API responses is a recurring complaint.
- **Windows and Network Environment Bugs:** SMB path mangling, absolute path space insertion, and CLI initialization hangs on offline networks indicate gaps in cross-platform and network-sanitized testing.
- **Context Loss After Interruption:** When a task is interrupted (timeout, manual stop, or crash), the model frequently loses awareness of prior turns. Manual re-contextualization is a major efficiency drain.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-07

---

## 1. Today's Highlights

The v0.9.0 release is in intense final polish, with the acceptance matrix (#2729) and long-lived PR harvest (#2722) actively gatekeeping against regressions. A major structural refactor of the command dispatch system (#2791) is moving forward in staged, mergeable layers, with Layer 1 (#2871) landing today. On the UX frontier, a multi-tab system core (#2864) and ghost-text prompt suggestions (#2781) have been merged, while a critical bug blocking European keyboard layouts (#2867) has been resolved.

---

## 2. Releases

No new releases in the last 24 hours. The community is actively stabilizing toward the **v0.9.0** tag.

---

## 3. Hot Issues

### #2729 – v0.9.0 Release Acceptance Matrix [15 comments]
The release blocker defining the full checklist for tagging: core build/test, provider routing, UI, Model Lab, WhaleFlow, docs, packaging, and rollback. This is the current dispatch center for release-critical work.
[Link](https://github.com/Hmbown/CodeWhale/issue/2729)

### #2791 – Refactor Command Dispatch to Strategy Pattern [6 comments]
Proposes breaking up monolithic command dispatch into focused command modules. Widely supported as a maintainability necessity as the codebase scales.
[Link](https://github.com/Hmbown/CodeWhale/issue/2791)

### #2580 – Adapt CodeWhale to VSCode Agent View [9 comments]
High demand for IDE integration, especially mimicking the new VSCode Agent View. The thread shows a clear community preference for editor-native UX over pure terminal.
[Link](https://github.com/Hmbown/CodeWhale/issue/2580)

### #2872 – CI Process Hangs at Smokes Tests [1 comment]
A blocking CI reliability issue: agent workflows stall indefinitely at the `verify` step without error output. This directly impacts contributor workflow.
[Link](https://github.com/Hmbown/CodeWhale/issue/2872)

### #2863 – French AZERTY `@` Key Conflicts with Sidebar Shortcut [1 comment, Closed]
On French AZERTY, typing `@` triggered the sidebar focus shortcut. A well-defined input handling bug affecting European users.
[Link](https://github.com/Hmbown/CodeWhale/issue/2863)

### #2847 – Abnormal Stop Working Mid-Session [2 comments]
Users report sudden termination with `Warn Stream read error: error decoding response body`. Stability critical for trust in the v0.9 release.
[Link](https://github.com/Hmbown/CodeWhale/issue/2847)

### #2787 – MCP Count Error in Status Bar [2 comments]
The TUI status bar shows an incorrect MCP tool count when both global and local config files are present. Undermines the status pane as a reliable dashboard.
[Link](https://github.com/Hmbown/CodeWhale/issue/2787)

### #2694 – Sidebar Detail Popovers for Work/Tasks/Agents [2 comments]
Current sidebar rows are so truncated they become unreadable during complex tasks. A high-priority UX issue for power users managing multi-agent sessions.
[Link](https://github.com/Hmbown/CodeWhale/issue/2694)

### #2691 – Plan Artifact Schema [1 comment]
Proposes requiring `sources`, `constraints`, `risks`, and `verification` in plan artifacts. Essential for making agent-generated plans auditable and reliable beyond simple step lists.
[Link](https://github.com/Hmbown/CodeWhale/issue/2691)

### #2666 – Telemetry: Token & Resource Visibility [2 comments]
The top internal feedback from agent harness testing. Agents lack visibility into token budget, context window pressure, elapsed time, and child-agent status during long tasks.
[Link](https://github.com/Hmbown/CodeWhale/issue/2666)

---

## 4. Key PR Progress

### #2762 – v0.9.0 Stewardship Integration [Open]
The main integration branch collecting stabilization, contributor-credit, and release-build prep work. Consolidates all v0.9.0 branches before tagging.
[Link](https://github.com/Hmbown/CodeWhale/pull/2762)

### #2871 – Layer 1: Clean Command Support Boundaries [Merged]
The first successful slice of the command-boundary refactor (#2791). Keeps the folder structure intact while removing public helper cruft. Signals the project can execute large refactors incrementally.
[Link](https://github.com/Hmbown/CodeWhale/pull/2871)

### #2869 – Fix: List Saved Models from All Providers [Open]
Fixes `/model` picker to show custom models saved under any provider config, not just the active one. Lowers friction when switching between providers like Moonshot and DeepSeek.
[Link](https://github.com/Hmbown/CodeWhale/pull/2869)

### #2867 – Fix: Prevent AltGr from Swallowing Characters [Merged]
Directly resolved the European keyboard layout issue (#2863) by properly handling `Ctrl+Alt` (crossterm's AltGr representation) in the composer. High practical impact for non-US users.
[Link](https://github.com/Hmbown/CodeWhale/pull/2867)

### #2864 – Multi-Tab System Core (Manager + Persistence) [Merged]
Introduces a `tab` module with manager and persistence, scoped narrowly for the v0.9 stewardship review. Sister PR to #2753, enabling multi-session workflows.
[Link](https://github.com/Hmbown/CodeWhale/pull/2864)

### #2868 – Feat: Show Thread Git Metadata in VSCode [Merged]
Extends the runtime thread summary with Git `head` and `dirty` fields, then exposes them in the VS Code Agent View. Bridges IDE visibility with TUI session state.
[Link](https://github.com/Hmbown/CodeWhale/pull/2868)

### #2865 – Modernize Toward Latest Claude Code [Open]
A comprehensive gap-closing PR covering prompts, hooks, skills, agents, and UI. Ambitious scope; the community is watching how this lands alongside the incremental v0.9.0 stewarding.
[Link](https://github.com/Hmbown/CodeWhale/pull/2865)

### #2753 – Multi-Tab System with Cross-Tab Collaboration [Open]
A deeper companion to #2864, adding cross-tab delegation (`TaskDelegator`) and session context sharing. Represents the long-term vision for multi-agent coordination.
[Link](https://github.com/Hmbown/CodeWhale/pull/2753)

### #2781 – Ghost-Text Follow-Up Prompt Suggestion [Open]
After each turn, a lightweight API call (v4-flash, max_tokens=64) generates a dimmed follow-up suggestion in the composer. Mirrors Claude Code's UX and shows investment in AI-native interaction patterns.
[Link](https://github.com/Hmbown/CodeWhale/pull/2781)

### #1893 – Per-Provider TLS Verification Toggle [Open]
Adds `insecure_skip_tls_verify` per-provider configuration (no global switch). Essential for users running self-hosted LLM endpoints behind internal CAs or test certificates.
[Link](https://github.com/Hmbown/CodeWhale/pull/1893)

---

## 5. Feature Request Trends

1. **IDE Integration (VSCode Agent View, GUI Layer)**
   The dominant feature vector. Issue #1584 and #2580 show sustained interest in moving beyond pure TUI into editor-native experiences. PRs #2868, #2862, and #2865 all directly address this bridge, exposing runtime metadata for IDE consumption.

2. **WhaleFlow: Autonomous Workflow Engine**
   A massive investment area. Request trends center on making agents scriptable and deterministic via a typed IR, Starlark DSL, and replay-safe execution (#2668, #2670, #2726). The community wants agentic behavior that is auditable, not opaque.

3. **Observability (Token Telemetry, Transcript UX, Plan Audits)**
   As tasks grow longer, users demand transparency. Issue #2666 (telemetry), #2691 (plan schema), and #2692 (transcript UX) all push for the tool to surface what the agent is doing, how much it costs, and how decisions were reached.

4. **UI Polish (Multi-Tab, Sidebar, Welcome Screen, Hotbar)**
   The core TUI is getting an experience upgrade. Multi-tab sessions (#2753, #2864), inspectable sidebars (#2694), an opinionated welcome screen (#2713), and a hotbar action system (#2866) indicate maturation of the application layer.

5. **Model Provider Flexibility (Hugging Face, Custom TLS)**
   Making Hugging Face a first-class citizen (#2727) and allowing per-provider TLS configuration (#1893) reflects a user base running diverse model stacks, not just major API providers.

---

## 6. Developer Pain Points

- **Non-US Keyboard Layouts:** The `AltGr` / `Alt` shortcut collision (#2863, #2867) caused real frustration for French, German, and UK users. While fixed, it highlights a persistent gap in cross-platform input testing for TUI tools.
- **Agent Black-Box Operations:** The lack of telemetry during long tasks (#2666) is the single most cited UX friction point from power users and agent harness testers. The community urgently wants token counters, progress indicators, and context pressure gauges.
- **CI Reliability:** The hang in smoke tests (#2872) directly blocks bot-driven and human contributor workflows. An unreliable CI pipeline erodes trust in automated gates, especially for a project leaning heavily on agent-assisted development.
- **Spontaneous Session Crashes:** The stream decode error (#2847) and similar unhandled failures create trust issues. The community expects robust error boundaries that preserve session state rather than abrupt termination.
- **Codebase Complexity (Command Dispatch):** The monolithic command dispatch (#2791) and tangled `commands::shared` tree make it difficult for new contributors to understand control flow. The staged refactor is well-received precisely because this pain point is widely recognized.
- **Configuration State Confusion:** The MCP count bug (#2787) reflects a broader challenge: as configuration surfaces grow (global, local, providers, tools), the UI must accurately reflect the merged runtime state to avoid user confusion.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*