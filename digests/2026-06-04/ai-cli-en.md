# AI CLI Tools Community Digest 2026-06-04

> Generated: 2026-06-04 03:41 UTC | Tools covered: 9

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

## AI CLI Tool Ecosystem Cross-Comparison Report (2026-06-04)

---

### 1. Ecosystem Overview

The AI CLI development landscape is undergoing a rapid Darwinian shift from interactive chat interfaces to persistent, daemonized agent runtimes. Communities across all major tools are converging on demands for cost transparency, platform parity (especially Windows), and trustworthy MCP/plugin ecosystems, yet reliability execution varies dramatically. This cycle reveals a decisive split: mature incumbents (Claude Code, OpenAI Codex) are battling scaling trust deficits, while challengers (Qwen Code, CodeWhale) are aggressively shipping next-generation server-side architectures. The "session" model is dying; the "agent runtime" is being born.

---

### 2. Activity Comparison

| Tool | Release Today | Engagement (Top Issues) | Development Velocity (PRs) |
|---|---|---|---|
| **Claude Code** | v2.1.162 | Very High (session limit, silent deletion) | Moderate (4 PRs) |
| **OpenAI Codex** | rust-v0.137.0 | Extreme (#14593: 597 comments, token burn) | Very High (10 PRs, Hooks/MITM stack) |
| **Gemini CLI** | v0.46.0-preview.1 | High (agent deadlocks, security fixes) | Very High (10 PRs, SSRF/HITL fixes) |
| **GitHub Copilot CLI** | v1.0.59 (none) | High (context ceiling, non-English broken) | Low (1 PR) |
| **Kimi Code CLI** | None | High (performance regression crisis) | Low (1 PR) |
| **OpenCode** | v1.15.13 (none) | Very High (MCP GUI regression, duplicates) | Very High (10 PRs, V2 runtime) |
| **Pi** | None | High (image bloat, bash truncation) | Very High (10 PRs, Vertex/Bedrock) |
| **Qwen Code** | v0.17.1 | Very High (memory system, config fragility) | Very High (10 PRs, +115k LOC daemon) |
| **CodeWhale** | v0.8.53 (rebrand) | High (WhaleFlow roadmap, MiMo auth) | Very High (10 PRs, v0.9.0 prep) |

**Key Observations:**
- **Highest Velocity Tier:** Qwen Code (Daemon merge, Vim overhaul), OpenAI Codex (Agent Hooks, MITM), CodeWhale (v0.9.0 pipeline), and OpenCode (V2 runtime) are shipping the most architectural change.
- **Highest Community Friction:** OpenAI Codex (#14593 token burn) and Claude Code (session/data loss) have the most vocal and frustrated user bases.
- **Stalling Risks:** GitHub Copilot CLI (1 PR) and Kimi Code (1 PR, severe regression) show dangerously low feature throughput relative to their bug backlogs.

---

### 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating strong industry-wide demand:

| Need | Signal Strength | Tools Expressing This |
|---|---|---|
| **Cost & Metering Transparency** | ★★★★★ | Codex (#14593), Claude Code (#5088, #63060, #41617), OpenCode (#28846), Kimi Code |
| *Real-time token counters, session cost breakdowns, pass-through pricing.* |
| **Windows Platform Parity** | ★★★★★ | Claude Code (#61691), Codex (#13993), Copilot CLI (#3622, #1999, #3648), Qwen Code (#4218, #4720), Gemini CLI (#27301), OpenCode (#12595) |
| *Standalone installer, stable ARM64 sandbox, working clipboard/hooks, CJK/DE keyboard support.* |
| **MCP/Plugin Lifecycle Reliability** | ★★★★★ | OpenCode (#30265 cluster), Copilot CLI (#3539, #3542, #3659), Codex (#25758), Qwen Code (#4218), Claude Code (credential-guard PR) |
| *State surviving restarts, context window bloat from tool schemas, Windows `.ps1` hook execution.* |
| **Sandboxing & Security Guardrails** | ★★★★☆ | Copilot CLI (#892), Gemini CLI (#27472, #22672), Qwen Code (#4572 auto-modification), Pi (#5332 approval gate) |
| *Filesystem confinement, prompt injection defenses, self-modification prevention.* |
| **Agent Observability & Introspection** | ★★★★☆ | Claude Code (`waitingFor` field), Gemini CLI (#22323 false success), Copilot CLI (token breakdown demand), OpenCode (#30644 session tabs) |
| *Truthful sub-agent status, waiting state indicators, session resume by ID.* |
| **Persistent Memory / Rules System** | ★★★☆☆ | Qwen Code (#4747 global memory, #4723 Rules), Kimi Code (#2421 Project grouping), Claude Code (Rules feature exists), Copilot CLI (#2303 session UX) |
| *Cross-project preferences, user-level memory files, durable Instructions.* |

---

### 4. Differentiation Analysis

Each tool is pursuing a distinct strategic wedge in the market:

- **Claude Code** – The "Agent Standard Setter." Deepest hook/plugin API and model-fidelity ecosystem (Opus reasoning). Currently paying the tax of early adoption: session scaling limits and data integrity debt are the main trust eroders among power users.

- **OpenAI Codex** – The "Enterprise Platform." Unmatched investment in auth infrastructure (MITM CA, audit logging, cloud config bundles). The #14593 token burn scandal is an existential threat to its enterprise value proposition.

- **Gemini CLI** – The "Security-First Native." Uniquely prioritizing SSRF prevention, HITL bypass protection, and destructive-action deterrence. Differentiating through responsible autonomy and AST-native code intelligence.

- **GitHub Copilot CLI** – The "Lowest-Common-Denominator Integrator." Tightest GitHub and Copilot integration, but weakest on cross-platform UX and MCP scaling. Latest data suggests a feature velocity stall.

- **Qwen Code** – The "Infrastructure Builder." Daemon mode, ACP protocol, OTel monitoring, and standalone binary updates target CI/CD and persistent server-side agents, not just interactive coding. Highest architectural LOC throughput.

- **CodeWhale (ex-DeepSeek TUI)** – The "Workflow Visionary." Betting on an agentic graph runtime (WhaleFlow) and native Hugging Face hub integration. Most ambitious roadmap relative to community size.

- **Pi** – The "Provider Mutant." Broadest model support surface (Vertex, Bedrock, Ollama, Llama.cpp) and a deep community-driven extension system. Core reliability (Bash truncation, image bloat) is the primary bottleneck to mainstream adoption.

- **OpenCode** – The "Local-First Architect." Effect-TS V2 runtime for durable execution, strong provider cost pass-through. Brand identity confusion ("Go" vs "Zen" billing) is a current distraction from solid engineering.

- **Kimi Code** – The "Regional Contender." Strong in Asian markets with k2.5 flagship model. Recent severe performance regression undermines its reliability narrative.

---

### 5. Community Momentum & Maturity

**Maturity Leaders (Stabilization Phase):**
- **Claude Code** and **Gemini CLI** have the most battle-hardened workflows but are showing signs of technical debt. Community fatigue is visible around unresolved architectural bugs (parallel tool call cascade failures in Claude, agent deadlocks in Gemini).

**Feature Momentum Leaders (Rapid Iteration):**
- **Qwen Code**, **CodeWhale**, **OpenAI Codex**, and **OpenCode** are shipping the most transformative code this cycle. Qwen's daemon mode merge (+115k LOC) is the largest single architectural leap. CodeWhale's v0.9.0 roadmap is the most aggressive relative to project size.

**Risk Zones:**
- **Kimi Code**: The v1.46.0 performance regression could trigger user exodus without rapid stabilization.
- **GitHub Copilot CLI**: Stagnation (1 PR) combined with severe cross-platform input bugs risks becoming a secondary tool in its users' toolchains.
- **OpenAI Codex**: The #14593 resolution will define developer trust for the coming year.

**Emerging Leader:**
- **CodeWhale** shows the most architecturally engaged community relative to its scale, driven by the detailed v0.9.0 execution map and rapid rebranding.

---

### 6. Trend Signals

**1. From Session to Service**
The dominant architectural shift is decoupling the agent runtime from the UI. Daemon modes (Qwen Code, CodeWhale WhaleFlow), background terminal APIs (OpenAI Codex), and persistent runtimes (OpenCode V2) signal a decisive evolution from "interactive chat" to "persistent agent task management."

**2. The MCP Scaling Ceiling is Here**
The industry is hitting hard protocol limits. Tool list bloat is collapsing context windows at session start (Copilot CLI #3539: 146k/200k consumed), and hard caps of 128 tools cause 400 errors (Gemini CLI #24246). Dynamic tool gating, weighted selection, and protocol versioning are no longer nice-to-haves—they are essential.

**3. Token Economy Polarization**
Deep community backlash against opaque billing (Codex #14593, Claude Code #5088/#63060) exposes a market gap. Developers want programmable metering APIs, real-time counters, and dynamic pricing that tracks underlying provider cost decreases (OpenCode #28846). The "infinite subscription" fantasy is breaking under real usage, creating an opportunity for honest, tool-level cost management.

**4. Security is Now a Differentiator**
SSRF mitigation (Gemini CLI PR #27473), credential scanning pre-hooks (Claude Code PR #62099), filesystem confinement (Copilot CLI #892), and self-modification prevention (Qwen Code PR #4572) are shifting security from compliance checkbox to core buying criteria as agents gain autonomy.

**5. Trust is the Only Durable Moat**
Silent data loss is the fastest trust eroder. Transcript deletion (Claude Code #59248), config corruption (Qwen Code #4729), tool truncation (Pi #5303), and invisible conversation history (Codex #23979) are the most angering bugs across the ecosystem. The tools that solve "never lose my work or silently override my settings" will build an unassailable competitive advantage in the next market phase.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-04**

---

## 1. Top Skills Ranking (Leading PRs by Community Engagement)

The following eight pull requests represent the most actively discussed Skill submissions in the repository, spanning infrastructure tooling, enterprise platforms, and document quality.

### **PR #514 – document-typography**
**Author:** PGTBoos · [GitHub Link](https://github.com/anthropics/skills/pull/514) · **Status:** Open

**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents, solving a universal quality gap in Claude's output.

**Discussion Highlights:** Widely recognized as a foundational quality-of-life improvement. Community debate focused on defining precise, non-restrictive rulesets that reliably enforce typographic standards without over-constraining Claude's prose generation.

---

### **PR #486 – ODT Skill**
**Author:** GitHubNewbie0 · [GitHub Link](https://github.com/anthropics/skills/pull/486) · **Status:** Open

**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods), targeting the LibreOffice and open-source ecosystem.

**Discussion Highlights:** Strong demand from government, education, and European markets where ODF is a regulatory standard. Conversation centered on template fidelity preservation and handling complex table structures within the format's XML schema.

---

### **PR #83 – Skill Quality & Security Analyzers**
**Author:** eovidiu · [GitHub Link](https://github.com/anthropics/skills/pull/83) · **Status:** Open

**Functionality:** Meta-skills that evaluate other Skills across five quality dimensions (structure, documentation, security, etc.)—a community-driven framework for ecosystem self-regulation.

**Discussion Highlights:** Considered a critical infrastructure investment. The "meta-skill" pattern established here has become a reference model for how to structure evaluation tools within the Skills format, sparking broader conversations about automated quality gates.

---

### **PR #181 – SAP-RPT-1-OSS Predictor**
**Author:** amitlals · [GitHub Link](https://github.com/anthropics/skills/pull/181) · **Status:** Open

**Functionality:** Integrates SAP's open-source tabular foundation model for predictive analytics directly into Claude's workflow.

**Discussion Highlights:** A strong signal of enterprise demand for specialized local/published ML models. Key discussion points included pattern compatibility between imported model inference and Claude Code's reasoning loop.

---

### **PR #444 – AURELION Skill Suite**
**Author:** Chase-Key · [GitHub Link](https://github.com/anthropics/skills/pull/444) · **Status:** Open

**Functionality:** A four-skill suite (kernel, advisor, agent, memory) providing a structured cognitive framework for professional knowledge management and AI collaboration.

**Discussion Highlights:** Represents a significant architectural investment in structured reasoning patterns. The community scrutinized the compatibility of persistent memory systems with Claude's stateless session model, pushing for explicit lifecycle documentation.

---

### **PR #190 – n8n Builder & Debugger**
**Author:** Wolfe-Jam · [GitHub Link](https://github.com/anthropics/skills/pull/190) · **Status:** Open

**Functionality:** Expert-level guidance for building and debugging n8n workflows natively within Claude, alongside a .faf (Foundation AI-context Format) skill for standardized project context.

**Discussion Highlights:** Automation workflow generation is a top use case for Claude Code. The n8n skills earned praise for production-readiness, while the .faf skill provoked a wider ecosystem discussion on standardizing project context formats.

---

### **PR #568 – ServiceNow Platform Skill**
**Author:** Vanka07 · [GitHub Link](https://github.com/anthropics/skills/pull/568) · **Status:** Open

**Functionality:** A comprehensive ServiceNow assistant covering ITSM, ITOM, SecOps, ITAM, HRSD, SPM, and IntegrationHub.

**Discussion Highlights:** Reflects demand for replacing or augmenting traditional enterprise ITSM interfaces with agentic AI. The skill's breadth—covering the full platform rather than a narrow scripting helper—was a defining topic of review.

---

### **PR #1140 – Agent Creator Meta-Skill**
**Author:** SyedaQurratAI · [GitHub Link](https://github.com/anthropics/skills/pull/1140) · **Status:** Open

**Functionality:** A meta-skill for generating task-specific agent sets, coupled with critical stability fixes for multi-tool evaluation and Windows compatibility.

**Discussion Highlights:** The concept of a Skill that dynamically produces agent configurations signals a major evolution of the pattern. Discussion bridged advanced orchestration patterns with fundamental platform reliability (multi-tool calls, cross-platform paths).

---

## 2. Community Demand Trends (From Issues)

### Enterprise & Workflow Integration
The most-voted issue—**#228 (Org-wide skill sharing)** (13 comments, 7 👍)—explicitly demands organizational skill libraries, signaling a strong enterprise push. This is reinforced by heavy engagement on **#412 (Agent Governance safety patterns)**, which addresses the guardrail gap required for production deployment. Skills targeting SAP, ServiceNow, n8n, and SharePoint collectively represent the highest-density topic across both PRs and Issues.

### Skills Ecosystem Infrastructure & Governance
A secondary but equally intense demand cluster revolves around the health of the Skills ecosystem itself:
- **Trust & Security (#492):** The namespace trust boundary issue (community skills distributed under `anthropic/`) sparked a critical 7-comment thread on supply chain risk.
- **Standards & Portability (#1156, #202, #1220):** The community is vocal about needing formal standards for skill-creator patterns, portability labels, and multi-file bundling.
- **Duplicate Management (#189):** Plugin collisions waste context window space (6 comments, 8 👍), highlighting an urgent need for proper dependency resolution.

### Cross-Platform & Debugging Reliability
Persistent requests for **Skills as MCPs (#16)** and **Bedrock compatibility (#29)** indicate a desire for vendor-neutral agent standards. A high volume of Windows-specific fixes submitted (#1050, #1099, combined with **#556**'s 9 comments on `run_eval.py` trigger failures) reveals that cross-platform reliability remains a major barrier to contributor onboarding.

---

## 3. High-Potential Pending Skills (Open PRs Nearing Merge)

These open PRs show active refinement, recent updates, and strong potential to land in the main collection soon:

| PR | Title | Author | Status Signal |
|---|---|---|---|
| **#363** | Fix feature-dev workflow phases (TodoWrite overwrite) | Mr-Neutr0n | Updated 2026-06-03; fixes a critical bug in a widely used workflow |
| **#723** | testing-patterns skill | 4444J99 | Covers full testing stack (unit, React, E2E); high canonical potential |
| **#335** | masonry-generate-image-and-video | junaid1460 | Imagen/Veo integration; strategically aligned with multimodal demand |
| **#154** | shodh-memory skill | varun29ankuS | Persistent cross-session context; foundational for long-running agents |
| **#509** | CONTRIBUTING.md | narenkatakam | Closes #452; addresses a 25% community health score gap |
| **#1050 / #1099** | Windows subprocess/encoding fixes | gstreet-ops, joshuawowk | Unblocks a major platform for skill development and testing |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand centers on maturing the Skills ecosystem from a collection of individual recipes into a professionally governed platform—investing heavily in meta-tooling (quality analysis, security auditing, agent creation) and robust infrastructure (sharing, packaging, cross-platform execution) to safely support deep integration with complex enterprise platforms (ServiceNow, SAP, SharePoint) and universal productivity standards (ODF, typography, workflow automation).**

---

# Claude Code Community Digest — 2026-06-04

**Data source:** github.com/anthropics/claude-code

## Today's Highlights
Claude Code v2.1.162 shipped with better agent session introspection (the `waitingFor` field) and explicit Grep/Glob tool bindings for native builds. The community is closely watching the **session limit continuation** request (#13354, 116 👍) and the **remote reconnection failure** bug (#34255, 86 👍), while a critical parallel tool call reliability bug (#22264, 61 👍) and silent transcript deletion (#59248) continue to erode trust for long-running sessions.

## Releases
**v2.1.162** — `claude agents --json` now includes a `waitingFor` field that surfaces exactly what a waiting session is blocked on (e.g., a permission prompt). This is a meaningful improvement for agent observability at a glance. Additionally, explicitly listing `Grep` or `Glob` via `--tools` now correctly binds the dedicated embedded search tools on native builds, which previously silently ignored these names. [View release](https://github.com/anthropics/claude-code/releases)

## Hot Issues

1. **[#13354] Session Limit Continuation** — *(Enhancement, 56 comments, 116 👍)*  
   The top-voted request this week. Users want the agent to seamlessly continue past usage limits rather than halting mid-task. A clear signal for better cost-aware session lifecycle management.  
   [Issue #13354](https://github.com/anthropics/claude-code/issues/13354)

2. **[#16446] LaTeX Rendering in VS Code Plugin** — *(Enhancement, 33 comments, 93 👍)*  
   Strong demand for proper LaTeX rendering in the VS Code extension. Currently raw markup is displayed, which breaks workflows for scientific and technical writing.  
   [Issue #16446](https://github.com/anthropics/claude-code/issues/16446)

3. **[#34255] Remote Control Reconnection Failure** — *(Bug, 48 comments, 86 👍)*  
   Connections drop silently with no automatic recovery. A major blocker for remote pairing and multi-device workflows. Community anger is mounting around this regression.  
   [Issue #34255](https://github.com/anthropics/claude-code/issues/34255)

4. **[#22264] Parallel Tool Call Cascade Failure** — *(Bug, 33 comments, 61 👍)*  
   When Claude makes simultaneous tool calls and one fails, *all* sibling calls are cancelled with "Sibling tool call errored." This forces costly retries and reduces agentic reliability.  
   [Issue #22264](https://github.com/anthropics/claude-code/issues/22264)

5. **[#5088] Account Locked After Max Plan Payment** — *(Bug/Cost, 173 comments, 58 👍)*  
   Payment immediately triggers a full account lockout from both Claude Code and claude.ai with no recovery path. Remains the most commented issue by a wide margin.  
   [Issue #5088](https://github.com/anthropics/claude-code/issues/5088)

6. **[#63875] Tool Call Parsing Error Interrupts Sessions** — *(Bug, 29 comments, 36 👍)*  
   Recurring, non-self-correcting parser error kills in-progress actions mid-session. Significant trust concern for autonomous workflows.  
   [Issue #63875](https://github.com/anthropics/claude-code/issues/63875)

7. **[#63060] Usage Credits Required for 1M Context** — *(Bug/Cost, 36 comments)*  
   Users on Max 20x plans are blocked by prompts to enable usage credits for 1M context windows. Confusing UX layering on top of billing.  
   [Issue #63060](https://github.com/anthropics/claude-code/issues/63060)

8. **[#59248] Silent Transcript Deletion** — *(Bug/Data Loss, 12 comments)*  
   Conversation transcripts older than the current session are silently purged during cleanup with no recovery, opt-in, or warning. Data integrity concern for daily users.  
   [Issue #59248](https://github.com/anthropics/claude-code/issues/59248)

9. **[#41617] Excessive Token Consumption After Updates** — *(Bug/Cost, 18 comments)*  
   Token usage has spiked significantly after recent updates, making the tool feel less efficient per task and impacting cost management.  
   [Issue #41617](https://github.com/anthropics/claude-code/issues/41617)

10. **[#63396] CLI Builds Invalid Request After Context Ops** — *(Bug, 7 comments)*  
    On long-lived sessions, using `/clear`, `/model` switch, or compaction constructs an HTTP 400 request that permanently wedges the session. A critical "last straw" reliability bug.  
    [Issue #63396](https://github.com/anthropics/claude-code/issues/63396)

## Key PR Progress *(4 active items)*

1. **[#65223] Fix Typo in Security Guidance Plugin** — *[MERGED]*  
   A clean typo fix ("reqwest" → "request") in the bundled security guidance plugin. Small but meaningful for accuracy in security tooling.  
   [PR #65223](https://github.com/anthropics/claude-code/pull/65223)

2. **[#61691] Diagnostic Script for GitHub Connector (Windows)** — *[OPEN]*  
   A PowerShell diagnostic and repair script addressing the persistent bug where the GitHub MCP connector shows 'Connected' status but exposes zero tools (#61682). Built on analysis from three related Windows issues.  
   [PR #61691](https://github.com/anthropics/claude-code/pull/61691)

3. **[#62099] Credential-Guard Plugin for Secret Detection** — *[OPEN]*  
   Implements a `PreToolUse` hook that scans `Write`, `Edit`, `MultiEdit`, and `Bash` tool calls for 20+ credential patterns before content hits disk. Directly addresses secret leakage concerns.  
   [PR #62099](https://github.com/anthropics/claude-code/pull/62099)

4. **[#22919] Collab Plugin: Socratic Mentoring Mode** — *[MERGED]*  
   A plugin that transforms Claude into a mentor who asks guiding questions and lets the developer write the code themselves. An interesting design pattern for learning-oriented use cases.  
   [PR #22919](https://github.com/anthropics/claude-code/pull/22919)

## Feature Request Trends

- **Session Lifecycle Continuity:** The #1 trend is seamless continuation past session limits. Developers do not want hard stop-gates on long-running tasks; they want cost-aware pausing or smoothing.
- **Notification & Observability:** Requests for VS Code extension notifications (#65242), better status bar indicators (#65235), and command aliases (#65253) all point to demand for richer ambient UX.
- **Extensibility Depth:** Interest in hook coverage (e.g., `PostToolUse` for Agent tools, #65169) and new plugin archetypes (credential-guard, collab mentoring) shows the community wants deeper integration points.
- **Platform Parity:** Windows-specific issues (GitHub connector, MSIX, path casing) and cross-device reconnection (#34255) indicate users increasingly rely on Claude Code outside the traditional macOS CLI comfort zone.

## Developer Pain Points

- **Data Loss & Session Fragility:** Silent transcript deletion (#59248, #62476) combined with session-wedging bugs (#63396) is the most acute trust deficit. Developers cannot confidently run long sessions today.
- **Cost Opacity & Unexpected Spikes:** Token consumption regressions (#41617) layered on confusing billing flows (#63060, #5088) create anxiety even on top-tier plans. Hard limits feel arbitrary, and credit mechanics are poorly communicated.
- **Agent Reliability at Scale:** Parallel call cascade failures (#22264), unrecoverable parse errors (#63875), and models marking tasks done without testing (#60177) undermine trust in autonomous mode.
- **Ergonomic Friction:** Missing command aliases, poor paste handling overwriting status indicators, and lack of progressive warnings before context limits are hit (#64850) make the daily driver experience feel rough around the edges.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-04

## 1. Today’s Highlights

Developer sentiment is dominated by the explosive #14593 token burn rate issue (597 comments), the most engaged ticket in the repository, signaling urgent demand for billing transparency and metering controls. Behind the scenes, OpenAI is building significant platform extensibility with a stacked PR series for MITM CA management and a new Hook system (Agent Hooks + Prompt Hooks) that will fundamentally extend the subagent and event pipeline. The `rust-v0.137.0` release shipped today with improved TUI controls and new enterprise admin capabilities.

---

## 2. Releases

**rust-v0.137.0**
- Added TUI controls for F13-F24 keybindings, paste support in searchable menus, and a compact reasoning-only status/title item.
- Enterprise/admin flows now show monthly credit limits and support applying cloud-managed config bundles, including for EDU workspaces.

**rust-v0.137.0-alpha.5**
- Patch release in the 0.137.0 alpha track.

---

## 3. Hot Issues (10 Noteworthy)

1. **[#14593](https://github.com/openai/codex/issues/14593) – Burning tokens very fast** (597 💬 · 262 👍)
   The defining community flashpoint. Users on Business subscriptions report unexpectedly high token burn with no visible breakdown. The volume demands a response on metering and pricing transparency.

2. **[#13993](https://github.com/openai/codex/issues/13993) – Support standalone Windows installer** (61 💬 · 133 👍)
   A long-running high-demand request. Users in enterprise or air-gapped environments cannot use the Microsoft Store distribution, making a `codex-setup.exe` the highest-impact Windows improvement on the board.

3. **[#21128](https://github.com/openai/codex/issues/21128) – Desktop silently hides project conversations** (19 💬 · 16 👍)
   A core workflow reliability issue. Once conversations fall outside the “recent-50” window they become invisible in the UI, breaking the app as a persistent project workspace.

4. **[#25144](https://github.com/openai/codex/issues/25144) – Disable auto-conversion of pastes to .txt** (49 💬 · 56 👍)
   A UX regression where long structured prompts are silently converted into file attachments. High community agreement that this should be optional.

5. **[#23979](https://github.com/openai/codex/issues/23979) – Local conversation history missing after update** (15 💬)
   Data remains on disk in `state_5.sqlite` but is completely invisible in the UI post-update. A crisis of confidence in app state migration.

6. **[#24260](https://github.com/openai/codex/issues/24260) – gpt-5.5 xhigh turn stalled 30 minutes** (16 💬 · 9 👍)
   A high-severity performance issue where the `Thinking` state persists for extended periods before any output token, suggesting a silent startup or allocation stall.

7. **[#24259](https://github.com/openai/codex/issues/24259) – Windows sandbox fails on ARM64** (12 💬 · 9 👍)
   Despite passing `codex doctor`, the sandbox `spawn setup refresh` fails on Windows 11 ARM64, blocking an entire platform segment.

8. **[#25249](https://github.com/openai/codex/issues/25249) – Semi-transparent sidebar rendering bug on Windows** (12 💬)
   Maximizing the window with the semi-transparent sidebar leaves undrawn regions. Indicates a compositor/paint issue in the Windows desktop app.

9. **[#9648](https://github.com/openai/codex/issues/9648) – Multi-account ChatGPT OAuth rotation** (11 💬 · 12 👍)
   Power users are requesting automatic credential failover between ChatGPT accounts to gracefully manage rate limits without disrupting sessions.

10. **[#25758](https://github.com/openai/codex/issues/25758) – App overwrites plugin config, removes Computer Use / Browser plugins** (4 💬)
    A recurring and severe plugin lifecycle bug: the app reverts plugin state on restart, specifically targeting the most important bundled plugins.

---

## 4. Key PR Progress (10 Important)

1. **[#26302](https://github.com/openai/codex/pull/26302) – app-server: add in-memory config layer**
   Enables process-scoped config updates without `config.toml` writes or restarts. Also fixes Windows forks to reload current sandbox config instead of pinning startup values.

2. **[#26300](https://github.com/openai/codex/pull/26300) – Add agent hooks**
   A major architecture addition: isolated ephemeral subagents (50-request cap, recursion disabled) that can inspect the codebase via the existing subagent runtime.

3. **[#24634](https://github.com/openai/codex/pull/24634) – Add prompt hooks**
   Companion to agent hooks. Defines prompt-handler events where hook inference runs as a side request without replacing the main conversation’s cached continuation state.

4. **[#26041](https://github.com/openai/codex/pull/26041) – Add app-server background terminal process APIs**
   Moves background terminal management from local process-tree guessing into the app-server as the single source of truth, adding `thread/ListTerminals` and `thread/TerminateTerminal` v2 APIs.

5. **[#26009](https://github.com/openai/codex/pull/26009) – Add metadata-only thread catalog subscriptions**
   Optimizes sidebar performance by allowing clients to subscribe to thread metadata without paying for full detailed runtime subscriptions.

6. **[#26272](https://github.com/openai/codex/pull/26272) – Load plugin hooks without other plugin capabilities**
   Performance optimization shaving ~100ms off `hooks/list` latency by skipping the loading of skills, MCP config, and apps when only hook declarations are needed.

7. **[#26287](https://github.com/openai/codex/pull/26287) – Refine Guardian prompt for indirect exfiltration**
   Security hardening of the provenance boundary to prevent trusted user text from delegating a named source to authorize cross-source private-data export.

8. **[#26285](https://github.com/openai/codex/pull/26285) / [#26286](https://github.com/openai/codex/pull/26286) / [#25888](https://github.com/openai/codex/pull/25888) – MITM CA Management Stack**
   A foundational three-PR series: load platform roots, materialize per-child CA bundles, and wire them through sandbox/runtime launch paths.

9. **[#26276](https://github.com/openai/codex/pull/26276) – Propagate auth session logging ID in ChatGPT login**
   Adds `authSessionLoggingId` to login protocol params, enabling reliable joining of Codex-side failures with authapi outcomes for debugging.

10. **[#26284](https://github.com/openai/codex/pull/26284) – feat(code-mode): allow disabling session store and load**
    Gives code mode consumers full flexibility to opt out of session persistence at creation time.

---

## 5. Feature Request Trends

- **Windows Ecosystem Maturity**: Standalone installer, stable sandbox execution, and performance parity are the loudest demands from the Windows user base.
- **Plugin Lifecycle Reliability**: Users want persistent, inspectable plugin configurations that survive restarts without silently dropping Computer Use, Browser, or MCP servers.
- **CLI Feature Parity**: High demand for Computer Use, MCP server management, and TUI niceties (undo/redo, headless clipboard in `arboard`) as first-class CLI capabilities.
- **Cost & Metering Transparency**: The #14593 blow-up has elevated per-session and per-model token breakdowns to a top priority for all subscription tiers.
- **Auth & Account Flexibility**: Multi-account OAuth failover and the ability to update account credentials (e.g., phone numbers) without losing access to paid accounts.

---

## 6. Developer Pain Points

- **Opaque Token Consumption**: The #14593 firestorm reflects deep anxiety about billing; users want real-time counters and clearer pricing models.
- **Workflow Data Reliability**: Lost conversation history on update (#23979), threads silently garbage-collected from the UI (#21128), and broken resume-after-archive flows (#26159) undermine trust in the Desktop app as a workspace.
- **Windows Sandbox & Performance Fragility**: Sandbox setup failures (ARM64, user rights, os error 740) combined with general app slowness make the Windows experience feel unstable.
- **Plugin State Loss**: Computer Use and Browser plugins silently vanishing on restart without user intervention blocks reliance on extended agent capabilities.
- **Authentication Roadblocks**: Inability to update phone numbers for SMS-based login (#25837) effectively locks paying users out of their accounts.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-04

## Today's Highlights
The team released `v0.46.0-preview.1` to patch in the 3.5 Flash model transition. On the security front, three high-severity fixes landed or advanced in review, covering an SSRF hostname bypass, a HITL truncation exploit, and path traversal in skill management. Meanwhile, several P1 agent deadlock bugs remain the most active and upvoted community discussions, continuing to erode trust in fully autonomous workflows.

## Releases

**[v0.46.0-preview.1](https://github.com/google-gemini/gemini-cli/pull/27655)** — A cherry-pick release patching `v0.46.0-preview.0` (PR [#27645](https://github.com/google-gemini/gemini-cli/pull/27645)). This update enforces backend definitions for the Gemini 3.5 Flash model family, ensuring the `auto` mode alias and `flash` classifier tier correctly route to the GA model when the `useGemini3_5Flash` experiment flag is active.

## Hot Issues

1.  **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs (P1, Bug)**
    *Why it matters:* The agent becomes completely inoperable for automation, hanging for up to an hour. The only workaround is disabling sub-agents entirely. The highest community upvotes in this batch (👍8) signal a critical quality blocker.
2.  **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck on "Awaiting input" after completion (P1, Bug)**
    *Why it matters:* A core execution pipeline bug where simple CLI commands finish successfully but leave the shell UI blocking indefinitely, requiring user intervention to recover.
3.  **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent MAX_TURNS false success (P1, Bug)**
    *Why it matters:* The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the turn limit and achieved nothing. This violates the principle of trusted feedback in multi-agent loops.
4.  **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping (P2, Epic)**
    *Why it matters:* A strategic workstream to replace naive text reads with structural code understanding (via AST). The goal is fewer turns, less token noise, and better codebase mapping. Three linked sub-issues (##22746, #22747) track the specific investigations.
5.  **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini does not use custom skills and sub-agents (P2, Bug)**
    *Why it matters:* The core value proposition of extensibility is undermined. Users report that the orchestrator ignores carefully crafted Gradle, Git, or custom skills unless explicitly instructed.
6.  **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools (P2, Bug)**
    *Why it matters:* A hard scalability ceiling. Users integrating many MCP servers or tools hit API limits, highlighting the urgent need for dynamic tool gating and selection strategies.
7.  **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails in Wayland (P1, Bug)**
    *Why it matters:* A platform-specific blocker that renders the browser agent unusable on a major Linux display server, generating frustration among a significant portion of the developer audience.
8.  **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior (P2, Customer Issue)**
    *Why it matters:* Safety and production trust. Users report the model autonomously executing `git reset --force` or dangerous database commands when safer alternatives exist.
9.  **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Add deterministic redaction and reduce Auto Memory logging (P2, Security)**
    *Why it matters:* Redaction currently happens *after* content is in the model context. This request pushes deterministic redaction earlier in the pipeline, a prerequisite for enterprise/compliance approval.
10. **[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — Symlinked agent files not recognized (P2, Bug)**
    *Why it matters:* A simple, expected filesystem feature (symlinks in `~/.gemini/agents/`) is broken, blocking users from organizing or sharing custom agent definitions across projects.

## Key PR Progress

1.  **[#27502](https://github.com/google-gemini/gemini-cli/pull/27502) — Fix P1 crash on terminal resize (`ioctl EBADF`)**
    Solves a race condition where the UI layout engine tries to resize a PTY that has already been torn down, causing a hard crash.
2.  **[#27473](https://github.com/google-gemini/gemini-cli/pull/27473) — Fix SSRF via hostname resolution**
    `isBlockedHost()` only validated IP literals. Hostnames resolving to private/link-local IPs bypassed the check entirely. This PR adds DNS resolution before the private-IP check.
3.  **[#27472](https://github.com/google-gemini/gemini-cli/pull/27472) — Prevent HITL bypass via truncation lockout (IPI)**
    Introduces a "truncation lockout" so users must expand and view the full content of a command or diff before approving it, closing a significant Indirect Prompt Injection vector.
4.  **[#27659](https://github.com/google-gemini/gemini-cli/pull/27659) — Fix path traversal in skill install/link/uninstall**
    Fully mitigates three path traversal vulnerabilities in the agent skill management subsystem where malicious frontmatter could escape the allowed root directory.
5.  **[#27619](https://github.com/google-gemini/gemini-cli/pull/27619) — Atomic updates in MCP tool discovery**
    Fixes "tool not found" errors during transient network drops by ensuring the tool registry retains the last known good state instead of being wiped by a failed refresh.
6.  **[#27474](https://github.com/google-gemini/gemini-cli/pull/27474) — Fix empty parts classification in message inspectors**
    Fixes a logical bug where `Array.prototype.every([])` returns `true` (vacuous truth), causing messages with empty `parts` arrays to be falsely classified as function calls or responses.
7.  **[#27505](https://github.com/google-gemini/gemini-cli/pull/27505) — Fix CJK spacing in terminal output**
    Corrects a rendering bug where extra spaces were injected between wide characters, fixing copy-paste errors and improving the UX for East Asian language users.
8.  **[#27301](https://github.com/google-gemini/gemini-cli/pull/27301) — Avoid duplicate home workspace commands**
    Fixes Windows-specific duplicate command loading by comparing canonical `realpath` spellings instead of raw string paths, preventing shortcuts from loading workspace commands twice.
9.  **[#27645](https://github.com/google-gemini/gemini-cli/pull/27645) — Route auto mode to Gemini 3.5 Flash GA (Closed)**
    Updates model resolution logic to prioritize `gemini-3.5-flash` over `gemini-3-flash-preview` when the experiment flag is active, laying the groundwork for the GA rollout.
10. **[#23307](https://github.com/google-gemini/gemini-cli/pull/23307) — Prompt snippets refactor into layered architecture (Closed)**
    A major internal refactoring of `packages/core/src/prompts/snippets.ts` into a modular, type-safe, model-specific architecture using the `promptTemplating` DSL.

## Feature Request Trends

- **Deep Code Intelligence (AST):** The most prominent strategic push is replacing text-based file reads with AST-aware tools (issues #22745–#22747). The community and maintainers agree that tools like `ast-grep` can dramatically reduce token consumption and improve edit precision compared to naive line-level retrieval.
- **Agent Self-Awareness:** Issue #21432 asks for the agent to understand its own CLI flags, hotkeys, and configuration, enabling it to act as its own expert guide. This reflects a growing expectation that the tool should be capable of self-documentation and introspective help.
- **Remote & Background Agents:** Epic #20303 charts a roadmap for task-level auth, 1P service agent support, and background processing. The community is signaling a clear need to move beyond interactive local sessions toward persistent, server-side autonomous agents.
- **Eval Stability & Quality Gates:** Issues #24353 and #23166 point to increasing investment in component-level evaluations and benchmark reliability. The community and maintainers are feeling the pain of inconsistent regression detection as the agent's behavior grows more complex.

## Developer Pain Points

- **Agent Execution Deadlocks:** The most upvoted and frequently recurring theme is the agent getting stuck indefinitely—either the Generalist agent hanging entirely (#21409) or the shell executor awaiting phantom "input" after a command finishes (#25166). These P1 bugs break workflows and force users to constantly babysit the tool.
- **Sub-agent Opacity & False Positives:** The false GOAL success bug (#22323) highlights a deep trust issue. When sub-agents claim completion while accomplishing nothing, it makes their outputs untrustworthy and defeats the purpose of delegation.
- **Security & Safety Anxiety:** Users are acutely worried about the agent's power. Issues around destructive `git` operations (#22672), messy filesystem behavior (#23571), and data exfiltration risks (#26525, #27473) show that the community is demanding strong guardrails before the tool can be trusted with full autonomy.
- **Ignored User Configuration:** A major frustration is the agent ignoring custom skills (#21968), browser `settings.json` overrides (#22267), and symlinked agent definitions (#20079). This makes personalizing the agent feel futile and undermines the extensibility story.
- **Scaling & Ecology Limits:** The hard cap of 128 tools causing 400 errors (#24246) and MCP reliability issues (#27619) are blocking power users who heavily integrate with other services and custom toolchains.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – 2026-06-04**

---

### 1. Today's Highlights
The past 24 hours reveal escalating friction around context-window limits and terminal I/O reliability. Heavy MCP and plugin configurations are exhausting the 200k context window on the very first message, forcing aggressive compaction and degrading the core agent experience (#3539, #3542). Meanwhile, a cluster of clipboard, paste, and keyboard-input regressions is impacting non-English users and Windows developers particularly hard (#1999, #3622, #3648). The hook system is also showing fragility, with postToolUse hooks not dispatched for `web_fetch` (#3665) and path resolution silently blocking tools on Windows (#3659, #3664).

### 2. Releases
No releases were published in the last 24 hours. The latest stable version remains **v1.0.59**.

### 3. Hot Issues
*Top 10 issues by community impact, severity, or engagement.*

- **#3539 – System/Tools consume 73% of context window (146k/200k)**
  *5 comments | 2 👍*
  Multiple MCP servers and plugins exhaust the window before a single user message, triggering instant auto-compaction in every new session. A fundamental scaling blocker for power users.
  *URL: [github/copilot-cli Issue #3539](#)*

- **#3542 – Enterprise MCP allowlist exceeds token limit; infinite compaction loop**
  *1 comment | 1 👍*
  Enterprise configurations with allowlist tool schemas hit the hard ceiling and immediately trigger a persistent compaction loop, effectively breaking the session.
  *URL: [github/copilot-cli Issue #3542](#)*

- **#892 – Add sandbox mode to restrict file access to a working directory**
  *10 comments | 49 👍*
  The highest-voted open feature request. Users want strict filesystem confinement to prevent the code agent from reading/writing outside the workspace root.
  *URL: [github/copilot-cli Issue #892](#)*

- **#1481 – SHIFT+ENTER executes prompt instead of inserting line break**
  *24 comments | 14 👍*
  A long-standing UX regression. `SHIFT+ENTER` behaves counter to every major chat application, while `CTRL+ENTER` is the actual line-break shortcut. High frustration signal.
  *URL: [github/copilot-cli Issue #1481](#)*

- **#3622 – Copy to clipboard silently fails on Windows**
  *2 comments | 2 👍*
  Copying agent output appears to succeed but the clipboard is never updated. Regression from v1.0.48. A workflow-critical silent failure.
  *URL: [github/copilot-cli Issue #3622](#)*

- **#1999 – Cannot enter `@` on German keyboard (Alt-Gr + Q)**
  *8 comments | 1 👍*
  Makes the CLI unusable for German-layout users. Also reported for `#`. A core input blocker.
  *URL: [github/copilot-cli Issue #1999](#)*

- **#3619 – Bash exit-code sentinel `$?` breaks fish shell detection**
  *1 comment*
  The CLI wraps commands with a Bash-specific `$?` syntax, causing errors in fish shell. Higher-tier shell users are completely blocked.
  *URL: [github/copilot-cli Issue #3619](#)*

- **#3648 / #3654 – CJK input corruption after ASCII / Space**
  *1 comment each*
  Typing Japanese or Chinese after ASCII text or a Space leaves glyphs invisible (v1.0.55+ cell renderer). Blocks East-Asian language users.
  *URL: [github/copilot-cli Issue #3648](#) | [#3654](#)*

- **#3659 – CLI cannot execute hooks shipped with plugins on Windows**
  *2 comments*
  `preToolUse` hook exceptions are thrown because `.ps1` arguments are not recognized as executable paths. Breaks Windows plugin adoption.
  *URL: [github/copilot-cli Issue #3659](#)*

- **#3172 – "Somebody else is owning the clipboard" message breaks TUI**
  *1 comment | 5 👍*
  An unhelpful ownership message replaces the status line, disrupting the terminal layout.
  *URL: [github/copilot-cli Issue #3172](#)*

### 4. Key PR Progress
Only one PR was updated in the last 24 hours, suggesting the team is primarily focused on bug triage rather than feature integration.

- **#3651 – [OPEN] Create xcopilotcli**
  *0 comments*
  A new PR proposing an `xcopilotcli` wrapper or variant. Description is currently sparse, but it indicates ongoing exploration of CLI tooling or alternative bootstrap mechanisms.
  *URL: [github/copilot-cli PR #3651](#)*

### 5. Feature Request Trends
*Distilled from high-engagement issues and community feedback.*

- **Sandboxing & Permission Configuration (#892, #2398):** The single strongest trend. Users want strict filesystem confinement and a persistent default-permissions file to eliminate repetitive per-session approval workflows.
- **Session UX & Transparency (#2303, #3645, #3612):** Growing calls for auto-naming of terminal tabs, reliable session resumption by ID, and a token breakdown (input vs. output) to track credit consumption.
- **Cross-Platform Accessibility (#3663):** Demand for feature parity on linux-arm64, including voice dictation support.
- **Input Customization (#45, #3607):** Requests for configurable keybindings, modifier-key text editing, and a keyboard interrupt (`Esc`) to stop in-flight model responses.

### 6. Developer Pain Points
*Recurring systemic frustrations visible from the issue tracker.*

- **MCP/Plugin Context Ceiling (#3539, #3542):** Advanced users adopting multiple MCP servers immediately hit the hard token cap, preventing meaningful multi-tool sessions and forcing constant context flooding.
- **Non-English Input Broken (#1999, #3648, #3650, #3654):** German, Japanese, and Chinese keyboard handling is fundamentally broken in the current TUI, blocking a wide user base from daily use.
- **Windows Parity (#3622, #3659, #3664, #3593, #3662):** A disproportionate share of high-severity bugs targets Windows—clipboard, hooks, path expansion (`~`), uninstallation, and crash recovery.
- **Plugin/Hook System Fragility (#3665, #3659, #3664):** The "universal interception" promise of the hook system has specific gaps. Hooks are not dispatched for `web_fetch`, cannot resolve Windows paths, and fail on non-Bash shells. This erodes trust in the extensibility model.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for 2026-06-04, based strictly on the provided GitHub activity.

---

## Kimi Code CLI Community Digest — 2026-06-04

### 1. Today's Highlights
The community is sounding alarms over severe performance regressions in v1.46.0, with reports of drastic slowdowns and "engine overloaded" errors hitting the flagship k2.5 model ([#2423](#), [#2424](#)). A critical bug was also discovered where resuming a session silently overrides newly configured skills and system prompts ([#2420](#)). On a positive note, two long-requested UX enhancements—placeholder-as-block editing and immediate slash command execution—were finally shipped ([#1848](#), [#751](#)).

### 2. Releases
*No new releases in the last 24 hours.*

### 3. Hot Issues
*Exactly 10 issues were updated in the last 24h. All are covered below given their relevance.*

*   **[#2424] Engine overloaded error on k2.5 model** — A critical service-side issue causing immediate failures for users on the primary model over recent days. **Impact:** High—blocks core workflow. ([Issue](MoonshotAI/kimi-cli Issue #2424))
*   **[#2423] Latest versions are far slower** — A stark performance regression report. The user explicitly states Kimi Code used to be fast and is now noticeably degraded on v1.46.0 (Linux ARM64). **Community reaction:** Immediate concern; low tolerance for latency in a CLI tool. ([Issue](MoonshotAI/kimi-cli Issue #2423))
*   **[#2420] Session resume overrides system prompt (skills/config ignored)** — A fundamental state management bug. Resuming a session reads a stale `_system_prompt` from `context.jsonl`, completely ignoring newly added skills or configuration updates. **Community reaction:** High frustration among users relying on custom skills. ([Issue](MoonshotAI/kimi-cli Issue #2420))
*   **[#2422] Auto-scroll jumps to bottom when reviewing past output** — After a conversation completes, scrolling up to review earlier content snaps back to the latest response. **Impact:** Severe UX regression for code review. ([Issue](MoonshotAI/kimi-cli Issue #2422))
*   **[#2419] Web mode text copy broken** — Users of the `kimi web` interface cannot copy text from output boxes. **Impact:** Undermines the core value of an interactive AI tool. ([Issue](MoonshotAI/kimi-cli Issue #2419))
*   **[#751] Slash commands execute immediately on selection** — **CLOSED.** Previously required a second Enter press. Now runs instantly on selection. **Community reaction:** Quiet win—this gap had been pending since January. ([Issue](MoonshotAI/kimi-cli Issue #751))
*   **[#1847] Edit image/pasted-text placeholders as blocks** — **CLOSED.** A quality-of-life improvement where multi-modal placeholders are treated as atomic blocks (delete, select). **Community reaction:** Healthy—a contribution that directly responded to community friction. ([Issue](MoonshotAI/kimi-cli Issue #1847))
*   **[#2421] Request: Project model for session grouping** — User proposes grouping sessions into projects with shared memory and database indexing to reduce token usage. **Community reaction:** Signals demand for higher-level organizational structures. ([Issue](MoonshotAI/kimi-cli Issue #2421))
*   **[#2418] Replay mode disliked for session switching** — Users find the automatic replay of history when switching sessions intrusive and slow. **Community reaction:** Consistent feedback that replay should be opt-in. ([Issue](MoonshotAI/kimi-cli Issue #2418))
*   **[#2306] APC protocol playback empty on restart** — **CLOSED.** Zed editor integration (ACP/APC mode) was losing session history after restart. Fix now deployed. **Community reaction:** Important fix for the IDE-integration user base. ([Issue](MoonshotAI/kimi-cli Issue #2306))

### 4. Key PR Progress
*Only one PR was active in the reporting window.*

*   **[#1848] feat(prompt): edit image and pasted-text placeholders as blocks** — **CLOSED.** Implements the feature requested in [#1847](#). This was a community-driven PR merged after a two-month review cycle. It modernizes the terminal prompt editor to handle multi-modal inputs as atomic blocks, significantly reducing cursor-based editing errors. ([PR](MoonshotAI/kimi-cli PR #1848))

### 5. Feature Request Trends
*   **Contextual Organization & Memory:** Users are pushing beyond single sessions toward **project-level grouping** with shared memory and indexing ([#2421](#)). The goal is explicitly to reduce token consumption and manage long-running discussions.
*   **Terminal UX Streamlining:** A strong theme of **reducing friction** is emerging. Users want fewer keystrokes (immediate slash execution—shipped), atomic block manipulation (shipped), and opt-in replay ([#2418](#)).
*   **Web Mode Parity:** A gap is opening between the TUI and Web experience. Requests for fixing web-specific issues (copy, replay) indicate the web interface is under active use but lacking polish.

### 6. Developer Pain Points
*   **Performance Regression (Top Urgency):** The v1.46.0 release has triggered a wave of complaints about slowness ([#2423](#)) and backend engine overload ([#2424](#)). This is the dominant source of community friction today.
*   **Fragile State Management:** The discovery that session resumes unconditionally overwrite freshly generated config/system prompts ([#2420](#)) erodes trust in skill customization and makes configuration changes effectively volatile.
*   **Integration Roulette:** Bugs in ACP/APC protocol playback ([#2306](#), though fixed) and browser Web UI inconsistency ([#2419](#), [#2422](#)) show that platform-specific regressions are fracturing the user experience across different environments.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for June 4, 2026.

---

## OpenCode Community Digest — 2026-06-04

### 1. Today’s Highlights

The v1.15.13 release introduced a significant Desktop GUI-wide regression causing MCP, LSP, and plugin configurations to silently fail to render in the frontend, generating a flurry of duplicate bug reports over the past 24 hours. Simultaneously, a strong community backlash over the “Go” plan purchasing flow emerged, with users reporting brand confusion between “Go” and “Zen” billing. On the architecture front, a contributor merged a foundational “V2” session runtime draft (PR [#30632](https://github.com/anomalyco/opencode/pull/30632)), signaling continued investment in local-first consumers.

### 2. Releases

No new releases in the last 24 hours. The current stable version remains **v1.15.13**, which has been the subject of several rapid patch PRs today.

---

### 3. Hot Issues

1. **[#28846](https://github.com/anomalyco/opencode/issues/28846) — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction**  
   *57 comments · 72 👍 (Closed)*  
   The community is highly price-sensitive, demanding that OpenCode’s usage limits track provider cost decreases. The strong upvote count signals a widespread expectation of dynamic pass-through pricing.

2. **[#4695](https://github.com/anomalyco/opencode/issues/4695) — Speech-to-Text Voice Input for Lazy People**  
   *33 comments · 161 👍 (Open)*  
   The most enthusiastically received feature request in the dataset. Points to a significant unmet demand for asynchronous, low-effort interaction beyond keyboard input.

3. **[#27530](https://github.com/anomalyco/opencode/issues/27530) — Error: 4 of 5 requests failed: config.providers: Unexpected server error**  
   *24 comments · 15 👍 (Open)*  
   A critical startup blocker. The ambiguous “Unexpected server error” message makes self-diagnosis nearly impossible, stalling new users and specific server deployments.

4. **[#16017](https://github.com/anomalyco/opencode/issues/16017) — Add Go plan usage/balance API endpoint**  
   *13 comments · 40 👍 (Open)*  
   Power users want programmatic access to plan data for custom dashboards and metering, reinforcing the theme of OpenCode as an infrastructure component.

5. **[#30265](https://github.com/anomalyco/opencode/issues/30265) — MCP Broken on v1.15.13**  
   *8 comments · 4 👍 (Closed)*  
   The canonical bug in a cluster of ~9+ duplicates (including [#30600](https://github.com/anomalyco/opencode/issues/30600), [#30328](https://github.com/anomalyco/opencode/issues/30328), [#30390](https://github.com/anomalyco/opencode/issues/30390)). Configs load in the CLI but fail to surface in the Electron GUI—a serious sidecar-to-UI state sync failure.

6. **[#30664](https://github.com/anomalyco/opencode/issues/30664) — compaction.auto=false is bypassed by provider overflow auto-compaction**  
   *2 comments · 0 👍 (Open)*  
   A dangerous silent bug where an explicit user setting to prevent automatic compaction is overridden by a provider recovery path. High severity for users relying on data integrity.

7. **[#30662](https://github.com/anomalyco/opencode/issues/30662) — Auto session title generation fails for opencode provider models**  
   *2 comments · 0 👍 (Open)*  
   A specific UX regression where auto-naming fails due to a missing provider config, leaving sessions with default “New session” titles.

8. **[#30611](https://github.com/anomalyco/opencode/issues/30611) — Sessions fail on transient network errors instead of retrying**  
   *3 comments · 0 👍 (Open)*  
   Only `ECONNRESET` is treated as retryable. Intermittent network blips result in hard session failures and lost context, exposing a critical gap in error handling.

9. **[#26338](https://github.com/anomalyco/opencode/issues/26338) — Add CommandCode as a Provider**  
   *7 comments · 10 👍 (Open)*  
   Illustrates the community’s appetite for integrating with a wider variety of model providers beyond the current mainstays.

10. **[#28226](https://github.com/anomalyco/opencode/issues/28226) — SCAMMED with ZEN as GO**  
    *3 comments · 2 👍 (Closed)*  
    A high-trust issue: purchasing a “Go” subscription yields a “Zen” API key. Points to a branding/purchasing flow bug requiring immediate product and communications attention.

---

### 4. Key PR Progress

1. **[#30623](https://github.com/anomalyco/opencode/pull/30623) (Closed) — fix(openai): disable header timeout for websockets**  
   Quick patch to prevent WebSocket connections from failing due to an HTTP-oriented response-header timeout when a Codex auth loader installs a WebSocket adapter.

2. **[#30464](https://github.com/anomalyco/opencode/pull/30464) (Open) — feat: bump bedrock and add proper mantle support**  
   Significant infrastructure upgrade for AWS Bedrock, bumping `@ai-sdk/amazon-bedrock` from `4.0.107` to `4.0.112` and enabling new model access paths.

3. **[#30666](https://github.com/anomalyco/opencode/pull/30666) (Open) — fix(desktop): validate openExternal URLs by protocol**  
   Security hardening PR that adds URL scheme validation to the desktop app’s `shell.openExternal` IPC handler, closing a potential remote-code-execution vector.

4. **[#30644](https://github.com/anomalyco/opencode/pull/30644) (Open) — fix(app): improve desktop session tabs**  
   Collective UX fix addressing tab title clipping, subagent route attachment to parent tabs, and reactive metadata updates for renamed sessions.

5. **[#30632](https://github.com/anomalyco/opencode/pull/30632) (Closed) — feat(core): add embedded v2 session runtime and tool foundation**  
   Heavyweight draft PR building an Effect-TS-based “V2” session runtime, separating durable prompt admission from execution. Targeted at local-first consumers like OpenCord.

6. **[#30660](https://github.com/anomalyco/opencode/pull/30660) (Closed) — fix(app,ui): session review reactivity and VCS query cache**  
   Fixes a scroll-reset bug by keying file diffs on file names instead of unstable diff object references in the session review panel.

7. **[#28592](https://github.com/anomalyco/opencode/pull/28592) (Open) — fix(cli): handle OSC52 clipboard passthrough properly under GNU screen**  
   Corrects clipboard escape sequences for GNU screen, which previously wrongly assumed a `tmux`-only wrapping path.

8. **[#30658](https://github.com/anomalyco/opencode/pull/30658) (Open) — feat(acp): emit plan session updates from todowrite tool calls**  
   Extends the ACP protocol to ensure plan steps generated via tool calls are rendered in real-time, matching behavior of static plan imports.

9. **[#30647](https://github.com/anomalyco/opencode/pull/30647) (Open) — fix(app): make auto-accept permissions server-global**  
   Sensible workflow tightening: the auto-accept toggle now applies server-wide, with preserved overrides for narrower scopes like sessions or directories.

10. **[#30019](https://github.com/anomalyco/opencode/pull/30019) (Open) — feat(mcp): add TUI notifications for plugins**  
    Establishes a notification bridge for MCP servers to push status alerts into the TUI, significantly improving the plugin ecosystem’s feedback loop.

---

### 5. Feature Request Trends

- **Dynamic Pricing & Usage Transparency** (#28846, #16017)  
  The community views OpenCode as an infrastructure layer. There is strong demand for pricing that tracks underlying provider costs and for programmable access to usage metering.

- **Multimodal Interaction** (#4695)  
  Voice input is the dominant QoL feature request. The 161 upvotes suggest a clear desire for asynchronous, “lazy” interaction patterns.

- **Seamless Session UX** (#30662, #30644, #30669)  
  Requests cluster around smarter session lifecycle management: reliable auto-naming, persistent tabs across restarts, and stable metadata.

- **Provider Ecosystem Expansion** (#26338, #30464)  
  Users want frictionless integration with niche or regional providers, not just the top-tier API players.

- **Desktop/CLI Parity** (#30265 cluster, #30600, #30390)  
  The v1.15.13 regression has crystallized a high expectation that configs working in the CLI must work identically in the Desktop Electron app.

---

### 6. Developer Pain Points

- **v1.15.13 Desktop GUI MCP Regression**  
  The overwhelming story of the day. Configurations are parsed correctly by the sidecar but fail to render in the Electron frontend. This IPC state sync breakdown caused the highest volume of duplicate support noise.

- **Billing & Product Identity Confusion** (#28226, #30619)  
  A dangerous trust gap: users purchasing a “Go” plan receive a “Zen” API key. This creates immediate brand distrust and requires a cross-functional product/engineering fix.

- **Silent Config & Behavior Overrides** (#30664, #30662)  
  `compaction.auto=false` being bypassed and `session title generation failing without error` exemplify “hidden bugs” that erode user confidence and waste debugging time.

- **Fragile Network Error Handling** (#30611, #27530)  
  Hard failures on transient blips and ambiguous server error messages make the tool feel brittle under real-world conditions.

- **Platform-Specific Gaps** (#12595, #30650)  
  Continued friction on Windows (copy/paste, subagent workdirs) and niche terminals (GNU screen) surface an opportunity for more rigorous cross-platform testing of the CLI and Desktop clients.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — June 4, 2026

## 1. Today's Highlights
A flurry of fixes and community contributions rolled in today, with critical patches landing for image-heavy session crashes (PR #5370) and configuration hot-reload bugs (PR #5376). Feature velocity remains high, with a major push to add first-class Anthropic Vertex (PR #5262) and Amazon Bedrock Mantle (#5363) providers. A compelling proposal to cache extension loading promises up to 53x faster startup for power users with many extensions (#5380).

## 2. Releases
No releases were published in the last 24 hours.

## 3. Hot Issues

1. **[#5223: Anthropic provider modifies thinking blocks, causing 400 error with Opus 4.8](https://github.com/earendil-works/pi/issues/5223)** — 14 comments, 5 👍. The highest-engagement thread this period. Multi-turn conversations with Claude Opus 4.8 adaptive thinking break mid-session. The provider appears to corrupt `thinking` or `redacted_thinking` blocks in the assistant message payload. This is a critical blocker for users relying on deep reasoning workflows.

2. **[#5369: Tool-result images bypass resizeImage, making sessions uncompactable](https://github.com/earendil-works/pi/issues/5369)** — Tool-generated images (screenshots, etc.) accumulate at full resolution indefinitely, eventually causing HTTP 413 errors and "prompt too long" loops. The compaction budget explicitly excludes tool results, a significant scalability hole identified by the community.

3. **[#5303: Bash tool truncates command output when a child holds stdout past exit](https://github.com/earendil-works/pi/issues/5303)** — A silent data loss gremlin. Commands like `git commit` with pre-commit hooks lose the tail end of their output because the 100ms `waitForChildProcess` grace period expires. Highly disruptive for standard dev workflows.

4. **[#5380: Extension loading performance: 3x faster startup, 53x faster resume](https://github.com/earendil-works/pi/issues/5380)** — A performance proposal that caught the community's attention. Suggests caching compiled extensions to slash startup times from ~4s to <100ms for setups with 50 extensions. If implemented, this would deeply improve everyday DX for extension-heavy users.

5. **[#5271 / #5315: Community demand for MiniMax-M3 support](https://github.com/earendil-works/pi/issues/5271)** — Two duplicate requests filed within days of the model's release. The community deeply desires fast-track support for new state-of-the-art models. The speed of closure suggests a PR was merged quickly in response.

6. **[#4666: 429 Retry-After waits ignore retry.provider.maxRetryDelayMs](https://github.com/earendil-works/pi/issues/4666)** — A broken contract between the user's configured bounds and the provider's behavior. Users rely on `maxRetryDelayMs` to fail fast, but the client simply obeys the server. Hitting Escape or `/new` also fails to recover cleanly.

7. **[#5323: Improve Vertex + GCP metadata server support](https://github.com/earendil-works/pi/issues/5323)** — The authentication check for GCP is a synchronous `existsSync` call, which is too restrictive for modern GCP environments (workload identity, metadata server). An architectural gap for enterprise GCP users.

8. **[#5294: Llama.cpp backend timeout error despite infinite timeout setting](https://github.com/earendil-works/pi/issues/5294)** — A frustrating bug for local model enthusiasts. The `/settings` panel allows setting `http timeout` to false/infinite, but slow local models still hit a hidden timeout, suggesting a hardcoded limit isn't exposed to the UI.

9. **[#5340: Add /config and /exit aliases for Claude Code parity](https://github.com/earendil-works/pi/issues/5340)** — A simple quality-of-life request with strong resonance. Highlights how the tool's user base overlaps heavily with Claude Code users who bring specific muscle memory expectations.

10. **[#5373: High idle CPU and syscall rate on large sessions](https://github.com/earendil-works/pi/issues/5373)** — Users report ~24% CPU at idle on 150k+ token sessions. `strace` logs show ~45k syscalls in 66 seconds. A worrying performance regression for users managing large context windows.

## 4. Key PR Progress

1. **[#5262 [OPEN] feat(ai): add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262)** — A direct answer to high demand from GCP users. Constructs an `AnthropicVertex` SDK client and reuses the existing streaming path. If merged, this eliminates the need for custom adapter scripts for Vertex AI.

2. **[#5370 [CLOSED] fix(coding-agent): recover from request-size overflow by dropping oldest images](https://github.com/earendil-works/pi/pull/5370)** — Emergency fix for issue #5369. Implements a graduated compaction strategy that drops the oldest images during overflow recovery, preventing the catastrophic 413 loop.

3. **[#5332 [OPEN] feat(config): Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332)** — Introduces `.pi.user` and an approval gate for loading workspaces. A significant security and multi-tenancy foundation being laid by a prominent community contributor.

4. **[#5376 [CLOSED] fix(interactive): reload steeringMode and followUpMode on /reload](https://github.com/earendil-works/pi/pull/5376)** — Closes issue #5377. Fixes a subtle inconsistency where configuration changes to queue modes required a full restart. Keeps the config surface hot-reloadable.

5. **[#5178 [CLOSED] ai: add custom-header support to Bedrock provider](https://github.com/earendil-works/pi/pull/5178)** — Completes the `StreamOptions.headers` coverage across all provider routes. Unlocks corporate proxy gateways for AWS Bedrock users.

6. **[#5348 [OPEN] Add selective pi-ai base entrypoints](https://github.com/earendil-works/pi/pull/5348)** — A library-consuming developer's dream PR. Introduces side-effect-free entry points (`@earendil-works/pi-ai/base`) for optimal tree-shaking in downstream bundles.

7. **[#5360 [CLOSED] fix(coding-agent): isolate tool result status background](https://github.com/earendil-works/pi/pull/5360)** — Cleans up the TUI rendering so tool call previews and results are visually distinct, fixing a long-standing visual clutter issue in the shell UI.

8. **[#5371 [OPEN] fix(coding-agent): add a space between the skill and user messages](https://github.com/earendil-works/pi/pull/5371)** — A minor but welcome fix. Running `/skill:foo bar` previously concatenated the strings without a space. This PR resolves that typographical papercut.

9. **[#5356 [CLOSED] docs: add containerization guide and Gondolin example](https://github.com/earendil-works/pi/pull/5356)** — Documentation improvements are always in demand. Adding a containerization guide and an example for the "Gondolin" workflow helps users with deployment and reproducibility.

10. **[#5379 [OPEN] Store user scoped local package installs as absolute paths](https://github.com/earendil-works/pi/pull/5379)** — Converts relative paths to absolute paths for user-scoped local packages, preventing broken extension links after directory changes.

## 5. Feature Request Trends
The community is heavily invested in expanding Pi's reach into enterprise and diverse cloud environments. The dominant trend is **Provider Agnosticism Plus**: users don't just want more providers (Anthropic Vertex, Amazon Bedrock Mantle, MiniMax-M3), they want them deeply integrated, handling auth flows (GCP metadata, custom headers) automatically. A secondary trend is **Containerized & Remote Execution**, seen in requests like #5341 for remote containers over SSH. There is also a clear desire for **Power User CLI Ergonomics**, such as command aliases (#5340) and branch management in the session tree (#5366). Finally, **Extension System Maturation** continues to drive the roadmap, with calls for public `ctx.runCommand()` APIs (#5367) and formal customization of the session tree UI (#5362).

## 6. Developer Pain Points
The most acute pain points revolve around **unreliable core interactions**:

- **Silent Data Loss**: The Bash tool truncation on hooks (#5303) and uncompactable image bloat (#5369) represent a breach of trust in the tool's core operations.
- **Broken Semantics**: Thinking block mangling (#5223) and phantom follow-up prompts (#5368) indicate deeper issues in context/prompt assembly logic.
- **Poor Failure Modes**: 429 handling ignoring user caps (#4666) and hard crashes on tool name collisions (#5316) show that error recovery paths need significant hardening.
- **Performance Under Load**: High CPU at idle with large sessions (#5373) and slow startup with extensions (#5380) highlight scaling bottlenecks that annoy the tool's most dedicated users.
- **Configuration Friction**: Settings not applying on `/reload` (#5377), hidden timeouts (#5294), and missing CLI commands (#5340) create a sense of rough edges in the user experience.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-04

## Today's Highlights
The team shipped **v0.17.1** with a critical fix for false "compressed turn" errors during rewind operations, alongside a nightly build. Community discussion centers on two major feature ambitions: a **global user-level memory system** (#4747) mirroring Claude's user memory, and porting **Dynamic Workflows** (#4721) as the next tier of multi-agent orchestration. On the infrastructure side, the massive **daemon mode feature batch** (#4490) is merging into `main`, signaling a decisive pivot toward production-grade server-side architectures with OTel telemetry and ACP integration.

---

## Releases
Two versions landed in the last 24 hours:

- **v0.17.1** (Stable) — [Release v0.17.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1)  
  Contains `fix(rewind): false "compressed turn" error when mid-turn messages exist` by @doudouOUC. Full diff: [v0.17.0...v0.17.1](https://github.com/QwenLM/qwen-code/compare/v0.17.0...v0.17.1)

- **v0.17.1-nightly.20260604.16dd99fa3** — [Nightly Build](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260604.16dd99fa3)  
  Fresh nightly off the `release/v0.17.1-nightly` branch.

---

## Hot Issues — Top 10

**1. Global User-Level Auto-Memory** ([#4747](https://github.com/QwenLM/qwen-code/issues/4747))  
A highly-requested feature to store user preferences, style, and background at `~/.qwen/memories/` rather than per-project. Community points out the friction of re-learning context with every new project. Strong alignment with the existing request for a Rules system (#4723).

**2. Rules/Instructions Support** ([#4723](https://github.com/QwenLM/qwen-code/issues/4723))  
Users are explicitly asking for a dedicated rule system (distinct from Skills) akin to Claude Code's rules or Cursor's instructions. Skills currently fill this gap but lack cross-session persistence and global scope. This is the single most frequently echoed gap in the issue tracker.

**3. Config Corruption via Runtime Prefix** ([#4729](https://github.com/QwenLM/qwen-code/issues/4729))  
A critical bug where the runtime snapshot prefix (`$runtime|openai|`) leaks into `settings.json`'s `model.name`, stacking on every restart and eventually triggering 404 errors. A fix is already in progress via PR #4734, but the underlying fragility of model config persistence is a community concern.

**4. Shell Command Breaks Completely** ([#4743](https://github.com/QwenLM/qwen-code/issues/4743), CLOSED)  
A sudden regression where shell execution returned `signal 1`, then "Command produced no output", then hung indefinitely. The issue was triaged and closed quickly, suggesting a fix landed, but community confidence in shell tool reliability took a hit.

**5. Port Dynamic Workflows / Ultracode** ([#4721](https://github.com/QwenLM/qwen-code/issues/4721))  
Users want Qwen Code to match or exceed Claude Code's latest multi-agent capabilities, proposing this as a "third tier" beyond the existing `/swarm` command. Shows the community is watching Anthropic's velocity closely and expects similar innovation.

**6. OpenAI-Compatible Provider Setup Pain** ([#3384](https://github.com/QwenLM/qwen-code/issues/3384))  
Long-running (since April) issue with 12 comments. Users report that connecting local models via VLLM or Ollama through the OpenAI-compatible endpoint is opaque and often silently fails. Despite documentation updates, this remains a high-friction onboarding path.

**7. MCP Filesystem Tools Not Available** ([#4218](https://github.com/QwenLM/qwen-code/issues/4218))  
The MCP filesystem server connects in the UI but tool definitions never reach the model. Windows-specific paths appear unhandled. This is part of a broader pattern of MCP reliability gaps that erode trust in the tools layer.

**8. /model Should Not Persist by Default** ([#4754](https://github.com/QwenLM/qwen-code/issues/4754))  
A sharp UX insight from the community: switching models mid-session via `/model` silently overwrites `settings.json`. Users want in-session changes to be ephemeral unless explicitly saved. This would prevent accidental config drift.

**9. Auto-Created Skills Cause Regression** ([#4714](https://github.com/QwenLM/qwen-code/issues/4714))  
Several users are frustrated that Qwen Code auto-generates skills that contradict manually written ones, with no opt-out mechanism. The AI is overriding explicit user intent, which breaks the trust contract for an assistive tool.

**10. TUI Model Interruption & Memory Loss** ([#4740](https://github.com/QwenLM/qwen-code/issues/4740))  
Serious stability bug on TUI where certain models (DeepSeek, Meituan Longma) crash mid-session and lose context memory on recovery. The todo panel also desynchronizes. This is a major productivity blocker for interactive users.

---

## Key PR Progress — Top 10

**1. Daemon Mode Feature Batch Merge** ([#4490](https://github.com/QwenLM/qwen-code/pull/4490))  
Merges 46 commits (+115k/−12k LOC) from `daemon_mode_b_main` into `main`. Includes core daemon infrastructure, ACP session bridge, and workspace service extraction. This is the highest-velocity branch in the repo and the foundation for all upcoming server-side capabilities.

**2. Standalone Auto-Update Support** ([#4629](https://github.com/QwenLM/qwen-code/pull/4629))  
Adds self-update for non-npm installations. Downloads archives from OSS/GitHub, verifies SHA256, and atomically replaces the binary. Essential for enterprise deployments and CI runners where a package manager isn't available.

**3. Vim Mode Overhaul** ([#4677](https://github.com/QwenLM/qwen-code/pull/4677))  
Fixes three core Vim mode issues: Esc key leaking to app-level handlers, Enter unexpectedly submitting input, and render lag. Also implements missing NORMAL mode commands. A significant UX upgrade for terminal-native developers.

**4. ACP Child Lifecycle Optimization** ([#4751](https://github.com/QwenLM/qwen-code/pull/4751))  
Eliminates redundant grandchild process spawns, pre-heats ACP children at daemon boot, and adds idle keep-alive. Directly targets daemon cold start latency and memory overhead—a key metric tracked in #4748.

**5. Skills Picker Dialog** ([#4533](https://github.com/QwenLM/qwen-code/pull/4533))  
Replaces the purely binary `/skills` toggle with a full picker dialog supporting search, browse, and per-workspace disable lists. Addresses the growing complexity of skill management as the library expands.

**6. Model Display Name & Prefix Fix** ([#4741](https://github.com/QwenLM/qwen-code/pull/4741) & [#4734](https://github.com/QwenLM/qwen-code/pull/4734))  
Two PRs that together resolve the model name display issue (statusline showing `qwen3-coder-plus` instead of "Qwen3 Coder Plus") and the config-corrupting runtime prefix leak. High velocity on community-reported bugs.

**7. Web-Shell UI Fixes** ([#4752](https://github.com/QwenLM/qwen-code/pull/4752))  
Fixes JSON-RPC error serialization (`[object Object]`), floating panel auto-scroll interruptions, and ring-eviction reconnection logic. Critical polish for the daemon-mode web terminal UX.

**8. Computer Use YOLO Mode Fix** ([#4756](https://github.com/QwenLM/qwen-code/pull/4756))  
Fixes a logic error where the Computer Use install step was wrongly rejected under YOLO approval mode. Ensures the highest-trust mode actually works as intended for autonomous agent workflows.

**9. Git Submodule Crawling** ([#4596](https://github.com/QwenLM/qwen-code/pull/4596))  
Adds `--recurse-submodules` to `git ls-files` so that large monorepos with submodules are fully indexed. Directly addresses an oversight that has caused silent path omissions for teams using standard monorepo patterns.

**10. Auto Mode Self-Modification Hardening** ([#4572](https://github.com/QwenLM/qwen-code/pull/4572))  
Prevents the AI from silently overwriting Qwen Code's own config files, instructions, hooks, and MCP configuration through workspace edit fast-paths. Closes a critical safety gap in autonomous execution mode.

---

## Feature Request Trends

The community is converging on three major thematic gaps:

1. **Memory & Context Persistence** — Users want a unified memory layer (#4747, #4723) that spans projects and sessions, mirroring the "Rules + User Memory" pattern established by Claude Code and Cursor. The current project-scoped auto-memory is seen as insufficient for power users.

2. **Daemon Mode as First-Class Citizen** — Multiple open proposals (#4554, #4748, #3731) aim to productionize the daemon: OTel instrumentation, cold start benchmarks, and lifecycle optimization. The community is treating daemon mode as the future default and expects enterprise-grade observability.

3. **Advanced Multi-Agent Orchestration** — The request for Dynamic Workflows (#4721) signals that `/swarm` alone isn't the endgame. Users want autonomous sub-agent delegation, pipeline construction, and parallel task execution—features currently differentiating Claude Code.

---

## Developer Pain Points

- **Config Fragility Strikes Again** — The runtime prefix leak (#4729) and accidental `/model` persistence (#4754) show that the configuration system is too permissive and too opaque. Users are losing time to corrupted settings.

- **Auto-Generated Content Overrides User Intent** — The frustration with auto-created skills (#4714) and the inability to disable them highlights a core UX tension between AI autonomy and user control. Skills need an opt-in model or a strict priority scheme.

- **Tool Reliability on Windows Lags Behind** — MCP filesystem failures (#4218) and SMB share access issues (#4720) on Windows suggest the tool execution layer has platform-specific gaps that are not caught in the standard Linux/macOS development flow.

- **Shell Tool Trust Deficit** — The sudden shell command regression (#4743) and intentional-sleep backoff restrictions (#4708) indicate the sandboxing layer is still too aggressive or brittle, breaking legitimate workflows and eroding user trust in autonomous tool execution.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (now CodeWhale) Community Digest — 2026-06-04

**tl;dr:** The project formally rebrands to **CodeWhale** in v0.8.53 while maintainers drop an ambitious v0.9.0 milestone roadmap spanning agentic workflow engines, Hugging Face first-class integration, and a massive provider-auth stabilization push. Several critical UX bugs around the Xiaomi MiMo provider configuration were patched simultaneously.

---

## 1. Today's Highlights

The project officially **renames to CodeWhale** with v0.8.53, shipping legacy `deepseek` binaries as deprecation shims ahead of their v0.9.0 removal. A densely packed planning session produced a v0.9.0 roadmap centering on the **WhaleFlow** branch/leaf workflow runtime and making Hugging Face a native surface. Simultaneously, a rapid stabilization sprint closed a cluster of critical multi-provider auth/state bugs (Issues #2660–#2663) that were confusing users attempting to configure the new Xiaomi MiMo provider.

---

## 2. Releases

- **v0.8.53 / v0.8.52** — Project renamed to **CodeWhale**. The `deepseek` and `deepseek-tui` binaries are now deprecated compatibility shims that forward to `codewhale` and `codewhale-tui`. These shims will be removed entirely in v0.9.0.

---

## 3. Hot Issues (Top 10)

1. **[#2667] EPIC: v0.9.0 WhaleFlow branch/leaf workflow mode** — [Hmbown/CodeWhale Issue #2667](https://github.com/Hmbown/CodeWhale/issues/2667)
   The defining architectural goal of the next release: a typed workflow runtime with background pods, bounded leaf agents, deterministic trace replay, and a cached-main overlay for validated lessons.

2. **[[#2705] EPIC: Make Hugging Face a first-class CodeWhale surface](https://github.com/Hmbown/CodeWhale/issues/2705)**
   A strategic shift to deeply integrate with the open-weight ecosystem — model browsers, model cards, evals, and adapters — beyond treating HF as just another base URL.

3. **[[#2695] Agentic Harness Creator: evolve per-model harnesses from trace evidence](https://github.com/Hmbown/CodeWhale/issues/2695)**
   An ambitious proposal for the project to autonomously analyze a model’s behavior from traces and propose/profile custom harness adjustments automatically.

4. **[[#2735] MiMo endpoints are wrong (*mimo的端点错了*)](https://github.com/Hmbown/CodeWhale/issues/2735)**
   **Critical.** User reports that CodeWhale’s hardcoded endpoint mismatches Xiaomi’s official OpenAI/anthropic-compatible URLs, blocking MiMo model usage entirely.

5. **[[#2729] v0.9.0 Release acceptance matrix](https://github.com/Hmbown/CodeWhale/issues/2729)**
   A maturing release process: explicit gates for core stability, provider routing, UI, Model Lab, WhaleFlow, docs, and rollback before tagging.

6. **[[#2720] v0.9.0 Milestone execution map](https://github.com/Hmbown/CodeWhale/issues/2720)**
   An interesting meta-issue organizing v0.9.0 work into dependency lanes so AI agents tackling the milestone don’t jump into exciting features before prerequisites are closed.

7. **[[#2689] PlanReview: render Plan mode output as a reviewable artifact](https://github.com/Hmbown/CodeWhale/issues/2689)**
   Aims to graduate CodeWhale’s planning mode from a modal `update_plan` step list into a first-class, grounded, reviewable artifact with structure.

8. **[[#2731] Xiaomi Mimo Models should show Price](https://github.com/Hmbown/CodeWhale/issues/2731)**
   A recurring request from MiMo users for cost transparency. User notes the price was “harvested” before but didn’t make it into v0.8.52.

9. **[[#2664] TUI still surfaces legacy DeepSeek settings path](https://github.com/Hmbown/CodeWhale/issues/2664)**
   The `/config` settings view still reports reading from `~/Library/Application Support/deepseek/` instead of the new `~/.codewhale/` path.

10. **[[#2723] UI shell polish: slash picker, command palette, readable focus states](https://github.com/Hmbown/CodeWhale/issues/2723)**
    Addresses UX gaps surfaced by comparisons against Grok Build and Droid, particularly around discoverability of slash commands and unreadable focus colors.

---

## 4. Key PR Progress (Top 10)

1. **[[#2733] feat(plan): richer PlanArtifact schema for v0.9.0](https://github.com/Hmbown/CodeWhale/pull/2733)** (idling11)
   Extends `update_plan` with `title`, `objectives`, `dependencies`, and `risks` fields. Backward-compatible with legacy callers.

2. **[[#2732] Phase 3: pausable command lifecycle](https://github.com/Hmbown/CodeWhale/pull/2732)** (aboimpinto)
   Adds pause/resume/cancel support for custom slash commands. Builds on Phase 1 (frontmatter) and Phase 2 (hook gate).

3. **[[#2734] feat(sidebar): multi-line detail popover on truncated rows](https://github.com/Hmbown/CodeWhale/pull/2734)** (idling11)
   Replaces single-line hover tooltips with a bordered, auto-wrapping popover showing full truncated text in Work/Tasks/Agents rows.

4. **[[#2730] fix(settings): prefer canonical codewhale settings path](https://github.com/Hmbown/CodeWhale/pull/2730)** (xyuai)
   Fixes the rebranding gap from #2664. Reads legacy DeepSeek paths as fallback and migrates on load.

5. **[[#2718] fix(tui): persist provider switches to config](https://github.com/Hmbown/CodeWhale/pull/2718)** (xyuai)
   Critical fix for #2663 — ensures provider switches (/provider) survive restarts and adds regression tests for the Arcee-MiMo split-state path.

6. **[[#2717] fix(tui): make provider key replacement discoverable](https://github.com/Hmbown/CodeWhale/pull/2717)** (xyuai)
   Adds an inline `r` shortcut in the provider picker so users can edit API keys without leaving `/provider`.

7. **[[#2715] fix(tui): clear MiMo auth state after logout](https://github.com/Hmbown/CodeWhale/pull/2715)** (xyuai)
   Clears in-memory provider API-key slots on `/logout`, covering MiMo and newer hosted providers.

8. **[[#2687] feat(engine): mode-agnostic system prompt with append-only mode/approval messages](https://github.com/Hmbown/CodeWhale/pull/2687)** (LeoAlex0)
   A major engine refactoring that strips mode instructions, approval policies, and tool taxonomy from the base system prompt, delivering them as append-only messages for byte stability.

9. **[[#2634] feat: porting to HarmonyOS](https://github.com/Hmbown/CodeWhale/pull/2634)** (shenjackyuanjie)
   Community-driven port to `aarch64-unknown-linux-ohos`. Code is compileable, with a pending dependency upgrade for `nix`.

10. **[[#2525] feat(agent): classify model families](https://github.com/Hmbown/CodeWhale/pull/2525)** (cyq1017)
    Adds `ModelFamily` to the agent crate so TUI, desktop, and runtime surfaces can render consistent model affordances across first-party and self-hosted models.

---

## 5. Feature Request Trends

- **Agentic Workflow Runtime:** The "WhaleFlow" suite (#2667, #2683, #2689, #2726) clearly signals a goal to evolve from a chat TUI into an autonomous background agentic workflow system with replay, caching, and promotion logic.
- **Hugging Face as a Native Surface:** Multiple issues (#2705, #2707, #2727) argue for integrated model browsers, passports (metadata), and profile resolution — essentially becoming a terminal-native HF Hub client.
- **Provider Management Maturity:** Issues repeatedly ask for richer provider management: pricing transparency (#2731), correct endpoint discovery (#2735), and better credential UI (#2662).
- **File Decomposition / Developer Ergonomics:** Several issues (#2719, #2725) explicitly request breaking up files over 5,000 lines so AI agents and reviewers can edit safely — a rare but telling request from a project heavily developed by/for agents.

---

## 6. Developer Pain Points

- **Multi-Provider Auth Confusion:** The biggest pain point this week. Users consistently struggled with API key editing, logout semantics, and state persistence across provider switches. Issues #2660–#2663 all came from a single user attempting to configure MiMo. The rapid closure of these bugs (PRs #2714–#2718) shows the team is actively firefighting this.
- **Endpoint Compatibility Fragility:** Provider integrations (especially MiMo and OpenAI-compatible third parties) break on unexpected path formats. Issue #2735 (wrong endpoint syntax) and PR #2558 (adding `path_suffix` configurability) highlight an ongoing maintenance burden.
- **Rebranding Cleanup Debt:** The rename is generating churn. Hardcoded DeepSeek paths (#2664), legacy binary names, and compatibility shims create ambient confusion for users who rely on muscle memory or documentation.
- **Unreliable File Ingestion:** The `read_file` PDF tool crashing when `pages` isn’t specified (#2641) undermines user confidence in basic tooling for common file formats.
- **Tool Surface Size vs. Model Capability:** As the tool list grows, compatibility aliases (`todo_*` vs `checklist_*`, legacy subagent names) bloat the schema for weaker models, creating a tension between backward compatibility and tool selection accuracy (Issues #2681, #2682).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*