# AI CLI Tools Community Digest 2026-06-18

> Generated: 2026-06-18 03:37 UTC | Tools covered: 9

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

## AI CLI Tools Cross-Tool Comparison Report: 2026-06-18

### 1. Ecosystem Overview

The AI CLI tools ecosystem on June 18, 2026, presents a landscape of extraordinary feature velocity colliding with a mounting "reliability tax." Developers are demanding sophisticated multi-agent architectures, but tools are shipping regressions that silently break core workflows—from Claude Code's subagent misrouting to Gemini CLI's false success reports. Cost governance remains the single most explosive community issue, with Claude Code's Max plan limits generating nearly 1,500 comments, while Qwen Code faces a violent backlash over free tier policy changes. Across the board, tools are transitioning from isolated REPLs to persistent, integrated platforms, exposing deep architectural strain in authentication, state persistence, and enterprise security models. The industry has entered a phase where innovation is abundant, but trust is fragile.

### 2. Activity Comparison

| Tool | Release Status | Top Issue Volume | PR Velocity | Dominant Theme |
|---|---|---|---|---|
| **Claude Code** | v2.1.181 | Extreme (1,475C, #16157) | Moderate (7) | Cost Governance & Subagent Routing |
| **OpenAI Codex** | 3 Rust alphas | High (170C, #23794) | High (10) | Performance Rewrite & Voice |
| **Gemini CLI** | v0.47.0 / v0.48.0-preview | High (P1 severity) | High (10) | Agent Eval & Safety |
| **Copilot CLI** | None (Stabilizing) | Moderate (13👍, #3832) | None (0) | Post-Outage Recovery |
| **Kimi Code CLI** | None | Low (2 new issues) | None (0) | Enterprise Entry Friction |
| **OpenCode** | v1.17.8 | High (117C, #29079) | Very High (10+) | DB Stability & Rich TUI |
| **Pi** | None | Medium | High (10) | Builder SDK & Config |
| **Qwen Code** | v0.18.3 | High (151C, #3203) | Very High (10+) | Auth/Billing Friction |
| **DeepSeek TUI** | None | High (#3275, #3279) | Very High (10+) | Arch Migration & Mode Safety |

### 3. Shared Feature Directions

Several high-signal requirements appear consistently across tool communities, indicating industry-wide developer expectations:

- **Cost Governance & Metering**: The *#1 cross-cutting concern*. Claude Code (#16157) leads the charge on plan limits, while OpenCode (#6096 TPS display), Qwen Code (#4479 daily stats), and Copilot CLI (#3355 context cap) all reveal demand for real-time, granular cost observability. Qwen Code's workflow token budget PR (#5231) models the expected feature response.

- **Reliable Multi-Agent Delegation**: Orchestration reliability is universally strained. Claude Code (#69212/49) misroutes nested subagent results. Gemini CLI (#22323) reports false success after turn limits. Copilot CLI (#3812) drops MCP tool access in subagents. DeepSeek TUI (#3275) fights self-questioning loops. The gap between promised agent teams and actual reliability is the widest across the tracker.

- **Enterprise Security & Networking**: A hard wall to adoption. Kimi Code (#2458 SSL bypass), Copilot CLI (#3839 BYOK payloads), Gemini CLI (#27780 supply chain attacks), and Pi (#5849 Azure Foundry) all demonstrate that organizations cannot adopt these tools without sophisticated proxy, auth, and compliance support.

- **Session & State Persistence**: Database corruption erodes trust in long-running workflows. OpenCode (#31119/#31204), OpenAI Codex (#24030), and Copilot CLI (#3560) all report schema/state corruption crashes. Crash recovery features (Qwen Code #5030, DeepSeek TUI #3285) are becoming table stakes.

- **Rich Terminal UI as Primary Surface**: The TUI is no longer a fallback. TPS indicators (OpenCode #6096), customizable status lines (OpenAI Codex #17827), image support + terminal detection (Pi #5827), keyboard-first navigation (Qwen Code #2561), and ESC interrupt handling (OpenCode #32767, DeepSeek #3285) show the terminal is being polished into a first-class IDE.

### 4. Differentiation Analysis

Each tool reveals a distinct strategic posture:

- **Claude Code** is the *Platform Orchestrator*, leaning into its plugin/skill ecosystem and IDE integrations (JetBrains #69241, VS Code #25128). Its primary battlefield is enterprise cost governance, where the Max Plan value proposition is under the most intense community scrutiny.

- **OpenAI Codex** is the *Rust Innovation Engine*, pushing the performance frontier with aggressive alpha cycles focused on voice continuity and system clock time-awareness (varlatency series). It accepts high instability for a higher feature ceiling, targeting developer sophistication.

- **Gemini CLI** operates as the *Safety & Evaluation Lab*, featuring the most formalized testing framework (P1 evaluation epic #24353) and unique Auto Memory capabilities. Its agent reliability is its weakest link, directly contradicting the safety narrative.

- **GitHub Copilot CLI** is the *Enterprise Lock-in Gate*, uniquely differentiated by Fleet Mode and BYOK support. Currently in a fragile state post-June 16 outage, exposing its reliance on upstream API availability. Outage recovery and permission granularity (#1973, #2643) define its current trajectory.

- **Kimi Code CLI** is a nascent *Foothold* in the space, with bare-minimum daily activity exposing fundamental entry gaps (SSL, session flexibility) that must be solved before broader adoption.

- **OpenCode** thrives as the *Community Amplifier*, provider-agnostic and highly responsive to user demand (highest reaction counts on feature requests). Its primary weakness is database migration stability, causing hard crashes on update.

- **Pi** is the *Builder's SDK*, architecting explicitly for extensibility—RPC interfaces, concurrent sessions (#5700), and deep provider abstraction. Appeals to developers building custom AI tooling despite Node.js dependency duplication issues (#5653).

- **Qwen Code** serves as a *Global Bridge*, uniquely targeting the Chinese ecosystem (QQ Bot adapter #5202) while aggressively iterating on provider abstraction and token budgets. Auth and billing friction is the dominant community pain point.

- **DeepSeek TUI (CodeWhale)** acts as the *Architect's Testbed*, pursuing ambitious structural changes (Workrooms Phase 1, Rust core, static musl builds) and strict mode discipline against agent scope creep. Suffers from post-rename migration churn but shows the clearest architectural vision for v0.9.

### 5. Community Momentum & Maturity

- **Highest Raw Community Volume**: Claude Code (#16157, 1,475 comments) and Qwen Code (#3203, 151 comments) dominate engagement, driven overwhelmingly by pricing and policy friction rather than feature excitement. OpenAI Codex (#23794, 170 comments) leads on pure feature demand.

- **Fastest Iteration Velocity**: OpenAI Codex (three Rust alphas in 24 hours) and OpenCode (v1.17.8 launched with 10+ active PRs) demonstrate the highest build velocity. DeepSeek TUI maintains a similarly high PR volume alongside its architectural overhead.

- **Most Architecturally Ambitious**: DeepSeek TUI's Workrooms Phase 1 and OpenAI Codex's varlatency/voice features represent the most forward-looking investments in durable agent conversations and real-time awareness.

- **Under Most Duress**: GitHub Copilot CLI, recovering from a major outage with zero PR activity; DeepSeek TUI, struggling with v0.8.x regression fatigue; and Claude Code, managing the cost limit crisis with concurrent reliability bugs (CPU spin, subagent routing).

- **Most Stable Core**: Pi exhibits a steady, mature PR pipeline focused on configuration and provider compatibility rather than core rewrites or crisis management.

### 6. Trend Signals

**Cost is the Product Constraint.** The era of unlimited cheap tokens is ending. Across Claude Code, OpenCode, Qwen Code, and Copilot CLI, users demand real-time burn-down rates, per-model routing, and hard token budgets. Qwen Code's workflow token budget (#5231) and Pi's cache pricing fix (#5738) demonstrate how features must adapt to this new economic reality.

**Reliability is the New Competitive Moat.** The market is saturated with "agentic" capability claims. The next differentiator will be *dependability*—tools that do not drop connections (Claude Code #34255), corrupt state (OpenCode #31119), silently misroute outputs (Claude Code #69212), or report false success (Gemini CLI #22323). Developers will pay a premium for tools that simply work as promised.

**The Multi-Provider Hedge is Real.** Fear of API lock-in and supply risk drives demand for provider-agnostic architectures (OpenCode, Pi). Vendor-tied tools (Copilot CLI, Claude Code, Gemini CLI) must offer compelling integration value to offset this. DeepSeek TUI's #1481 (OpenCode Go/Zen cheap access) explicitly frames this as a cost-avoidance strategy.

**Terminal as a First-Class IDE is Table Stakes.** The terminal is being polished into a rich development environment. Image rendering, interactive session pickers, customizable status lines, flicker-free streaming, and keyboard-first navigation are no longer optional—they define modern UX baseline.

**Structured State Management is the Next Frontier.** The shift from stateless chat to durable, threaded projects (DeepSeek Workrooms Phase 1, Qwen Workflows) signals a move toward treating AI interactions as persistent engineering artifacts. The industry is learning that agentic workflows without structured session state are fragile and irreproducible.

**Enterprise Adoption Hits a Hard Infrastructure Wall.** Lost sessions, SSL negotiation failures, supply chain vulnerabilities, and auth state corruption are concrete blockers that prevent tools from crossing the enterprise chasm. Identity management and network proxy support are the critical unblockers separating niche tools from organizational standards.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the current activity in `github.com/anthropics/skills`.

---

## Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-18 | **Period:** H1 2026 Activity

### 1. Top Skills Ranking (Most-Discussed Submissions)

The following PRs represent the highest community attention and most substantive discussion volume in the pipeline.

- **🔹 ServiceNow Platform Skill (`#568`)**
  *Function:* Broad enterprise platform assistant covering ITSM, ITOM, SecOps, ITAM, FSM, SPM, CSDM, and IntegrationHub.
  *Status:* **Open | Author:** Vanka07
  *Highlights:* One of the most comprehensive enterprise verticals submitted. Maps a full Product Suite (SecOps, HR, CSM) into a single skill, generating strong discussion around scope management and token limits for large-platform skills.
  [GitHub Link](https://github.com/anthropics/skills/pull/568)

- **🔹 Shodh-Memory Skill (`#154`)**
  *Function:* Persistent memory system that surfaces relevant memories proactively and maintains agent context across conversations.
  *Status:* **Open | Author:** varun29ankuS
  *Highlights:* Heavily watched due to its architecture for long-term agentic memory. The community is debating the overhead of a "proactive context" call on every user message versus event-driven retrieval.
  [GitHub Link](https://github.com/anthropics/skills/pull/154)

- **🔹 Document Typography Skill (`#514`)**
  *Function:* Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.
  *Status:* **Open | Author:** PGTBoos
  *Highlights:* Described as fixing issues "every document Claude generates." High universal appeal; discussion focuses on whether typographic correction should be a core behavior rather than an optional Skill.
  [GitHub Link](https://github.com/anthropics/skills/pull/514)

- **🔹 AURELION Skill Suite (`#444`)**
  *Function:* Four skills (Kernel, Advisor, Agent, Memory) providing a structured cognitive framework and professional knowledge management.
  *Status:* **Open | Author:** Chase-Key
  *Highlights:* A bold multi-Skill submission with a 5-floor cognitive architecture. Discussion centers on whether this is a single meta-framework or should be split into independent utilities.
  [GitHub Link](https://github.com/anthropics/skills/pull/444)

- **🔹 Testing Patterns Skill (`#723`)**
  *Function:* Full-stack testing coverage unit testing (AAA pattern), React (Testing Library), and E2E philosophy.
  *Status:* **Open | Author:** 4444J99
  *Highlights:* Directly addresses the gap in developer tooling within the Skills repo. High engagement from developers wanting reliable code quality enforcement in agentic workflows.
  [GitHub Link](https://github.com/anthropics/skills/pull/723)

- **🔹 SAP-RPT-1-OSS Predictor (`#181`)**
  *Function:* Integrates SAP’s open-source tabular foundation model for predictive analytics directly into Claude Code.
  *Status:* **Open | Author:** amitlals
  *Highlights:* Strong enterprise traction. Discussion around model serving dependencies and whether the skill should bundle a local inference engine or assume an underlying SAP data pipeline.
  [GitHub Link](https://github.com/anthropics/skills/pull/181)

- **🔹 ODT / OpenDocument Skill (`#486`)**
  *Function:* Create, fill, read, and convert OpenDocument files (.odt, .ods) and parse ODT to HTML.
  *Status:* **Open | Author:** GitHubNewbie0
  *Highlights:* High demand from the European public sector and LibreOffice users. Discussion covers the complexity of OOXML-to-ODT fidelity and template variables.
  [GitHub Link](https://github.com/anthropics/skills/pull/486)

---

### 2. Community Demand Trends (From Issues)

Analysis of the top Issues reveals four clear demand vectors:

- **🛠 Skilling Infrastructure Stability (The #1 Botleneck)**
  The most volatile thread cluster revolves around `run_eval.py` reporting **0% trigger/recall rates** for every query (`#556`, `#1169`). Multiple independent reproductions confirm the core optimization loop is broken against noise. **Fix PRs are the fastest-moving items in the repository.**

- **🏢 Enterprise Governance & Security**
  - *Org-Wide Sharing (`#228`)* — Top-voted feature request. Demanding a shift from "Slack a .skill file" to a managed shared library.
  - *Namespace Trust (`#492`)* — Critical vulnerability disclosure: community skills under `anthropic/` namespace can impersonate official skills.
  - *Agent Governance (`#412`)* — Proposal for policy enforcement, trust scoring, and audit trails. Indicates maturity demands beyond basic function.

- **🪟 Cross-Platform Parity**
  Multiple issues (`#1061`, `#362`, `#1099`) document three distinct Windows failures: subprocess `PATHEXT` resolution, cp1252 encoding panics, and select-on-pipe crashes. Windows users are functionally locked out of the skill creation workflow.

- **📄 Document & Office Workflow Automation**
  Recurring demand across PRs (`#514`, `#486`, `#538`) and Issues (`#1220` Multi-file preload). Users want high-fidelity document output (typography, format conversion) with reliable reference file bundling.

---

### 3. High-Potential Pending Skills (Active, Not Yet Merged)

These PRs are currently open with significant community activity and are expected to land soon:

| PR | Skill | Why It Matters |
|---|---|---|
| **#1298** | Fix: `run_eval.py` 0% recall | Directly fixes the broken evaluation loop; unblocks the entire skill-creator pipeline |
| **#83** | Skill Quality & Security Analyzers | Meta-tools to enforce skill standards; creates a review layer for the marketplace |
| **#1050 / #1099** | Fix: Windows subprocess & encoding | Removes the OS blocker holding back a large segment of developers |
| **#361 / #539** | Fix: YAML parsing (unquoted special chars) | Prevents silent truncation of skill descriptions; critical for skill reliability |
| **#154** | Shodh-Memory | Broadest appeal for persistent agent memory outside of the AURELION ecosystem |
| **#335** | Masonry Generate (Image/Video) | Strongest generative AI skill submission; integrates Imagen/Veo directly into Claude |

---

### 4. Skills Ecosystem Insight

The community’s most concentrated demand is no longer for *which* new skill to build, but for **a reliable, secure, and OS-agnostic creation pipeline**—the evaluation engine is widely acknowledged as broken, Windows users are blocked, and organizations cannot securely share or govern the skills they already have. Until the infrastructure layer matures, the broader ecosystem will struggle to scale beyond individual experimentation.

---

# Claude Code Community Digest | 2026-06-18

---

## Today's Highlights

Anthropic shipped **v2.1.181** with a new `/config key=value` runtime syntax, enabling setting changes (e.g., `thinking=false`) directly from the prompt and across modes. The **cost governance debate (#16157)** remains the highest-engagement topic in the tracker, while fresh bugs in **nested subagent routing (#69212/49)** and a **macOS idle CPU spin (#68931)** are raising critical reliability alarms. Platform-specific regressions and the sustained "Open Source Claude Code" enthusiasm (#41447) underline the community's push for stability and transparency.

---

## Releases

**v2.1.181**

The team shipped a targeted quality-of-life release focused on runtime flexibility and macOS sandboxing:

- **`/config key=value`:** Set any setting from the prompt (e.g., `/config thinking=false`). Works in **interactive**, **`-p`**, and **Remote Control** modes — a direct response to workflow friction without requiring restarts.
- **`sandbox.allowAppleEvents`:** New opt-in setting for macOS, enabling sandboxed commands to send Apple Events (opens up AppleScript/OSA automation).
- **`CLAUDE_CLIENT_PAYLOAD` (truncated changelog):** A new environment variable for improved client identification in CI/CD and Remote Control contexts.

---

## Hot Issues

*10 noteworthy issues from the last 24 hours*

**1. [`#16157`](https://github.com/anthropics/claude-code/issues/16157) — Instantly hitting usage limits with Max subscription** *(1475 comments, 691 👍)*
The single most discussed issue in the repo. Subscribers at the highest pricing tier report the value proposition collapses under aggressive cost limits. Cost governance remains the #1 community concern.

**2. [`#34255`](https://github.com/anthropics/claude-code/issues/34255) — Remote Control: silent disconnection with no recovery** *(50 comments, 90 👍)*
Automatic reconnection fails silently. For developers relying on Remote Control for long-running tasks, this breaks core reliability guarantees.

**3. [`#50246`](https://github.com/anthropics/claude-code/issues/50246) — Feature Request: Message Queue Mode** *(32 comments, 99 👍)*
The highest-voted UX enhancement request. Users want to queue prompts without interrupting an active agent — a non-blocking interaction model absent from the current design.

**4. [`#63870`](https://github.com/anthropics/claude-code/issues/63870) — Bash tool calls emitted as raw `<invoke>` text** *(17 comments)*
A severe functional regression: the agent outputs tool invocations as plain text instead of executing them. Blocks all automation and agentic workflows.

**5. [`#69212`](https://github.com/anthropics/claude-code/issues/69212) / [`#69249`](https://github.com/anthropics/claude-code/issues/69249) — Subagent and nested subagent results route to wrong parent** *(New)*
Multi-agent orchestration breaks down in nested scenarios. Spawning subagents deliver conclusions to the root agent instead of the parent subagent. Critical for team-of-agents architectures.

**6. [`#68931`](https://github.com/anthropics/claude-code/issues/68931) — Idle session pinned at ~100% CPU (macOS ARM64)** *(3 comments, New)*
The main thread enters an event-loop busy-spin on idle. Destroying battery life and heating machines during what should be zero-cost pauses.

**7. [`#25128`](https://github.com/anthropics/claude-code/issues/25128) — VS Code extension: drag-and-drop broken in chat panel** *(20 comments, 40 👍)*
A regression unresolved since v2.1.6. Core IDE integration is compromised, forcing users to the terminal CLI for file attachment.

**8. [`#69234`](https://github.com/anthropics/claude-code/issues/69234) — Windows: Alt+V image paste fails for entire session** *(2 comments, New)*
A platform-specific session corruption bug. Once paste fails (often with naming artifacts), it permanently breaks for the session lifetime. Forces full restart.

**9. [`#69239`](https://github.com/anthropics/claude-code/issues/69239) — Claude Design links no longer resolve natively** *(3 comments, New)*
A first-party integration regression. Users depended on seamless design file reading via `claude.ai/design/p/...` links — now broken without an MCP connector.

**10. [`#69241`](https://github.com/anthropics/claude-code/issues/69241) — JetBrains Plugin: add setting to auto-accept edits** *(4 comments, New)*
High-value IDE workflow request. Moving from "suggestion diff" to seamless autonomous editing in JetBrains, mirroring demand seen in VS Code.

---

## Key PR Progress

*The official PR queue is light today (7 items), but several contributions are highly relevant to the developer experience.*

**1. [`#41447`](https://github.com/anthropics/claude-code/pull/41447) — feat: open source claude code** *(OPEN)*
A community-led PR referencing several long-standing feature requests. Serves as a barometer of the strong desire for codebase transparency and community-driven plugin validation.

**2. [`#41611`](https://github.com/anthropics/claude-code/pull/41611) — feat: add the missing source to claude code** *(OPEN)*
A companion to the open-source push, addressing gaps in current source distribution.

**3. [`#69226`](https://github.com/anthropics/claude-code/pull/69226) — Update frontend-design skill** *(MERGED)*
Official patch pushing the frontend-design plugin to v1.1.0. Active investment in the plugin/skill ecosystem.

**4. [`#19867`](https://github.com/anthropics/claude-code/pull/19867) — fix(code-review): allow re-reviews on new commits** *(OPEN)*
Fixes a logical gap in the code-review plugin. Prevents wasteful re-reviews while ensuring new commits get a fresh pass. Important for CI/CD parity.

**5. [`#33443`](https://github.com/anthropics/claude-code/pull/33443) — fix: Update Dockerfile to use native installer** *(OPEN)*
Critical for devcontainer and cloud development. Moves from the deprecated `npm install` path to the official installer, ensuring reliable setup in ephemeral environments.

**6. [`#60732`](https://github.com/anthropics/claude-code/pull/60732) — docs: polish plugins README wording** *(MERGED)*
Small UX improvement. Clearer onboarding documentation drives higher plugin adoption.

**7. [`#60427`](https://github.com/anthropics/claude-code/pull/60427) — docs: standard GitHub capitalization in README** *(MERGED)*
Attention to detail in official documentation. Low impact, but sets a professional tone.

---

## Feature Request Trends

*The most-requested feature directions distilled from recent issues:*

- **Asynchronous / Non-Blocking Interaction:** The dominant UX request. Users want to queue messages (#50246) and batch prompts (#68998) without interrupting active agents. The new `/config` syntax in v2.1.181 is a step towards runtime flexibility without task restarts.
- **Cost Transparency & Access Control:** Demands for regional pricing (#17432), real-time token burn-down rates (#69253), and clearer 1M context credit models (#69154). The community feels the pricing tier model lacks granularity and predictability.
- **Multi-Agent Delegation Reliability:** Bugs in subagent routing (#69212, #69249) directly oppose the demand for robust agent teams. Correct message-passing between parent and child agents is a prerequisite for scaling agentic workflows.
- **IDE Platform Maturity:** Claude Code is transitioning from a "CLI tool" to an "IDE platform." Requests for JetBrains auto-accept (#69241), VS Code chat drag-and-drop fixes (#25128), and Web UI copy buttons (#69254) reflect this widening surface area.

---

## Developer Pain Points

*Recurring frustrations and high-frequency problem clusters:*

- **Cost Surprises and Value Friction:** The Max Plan limit issue (#16157) is a systemic trust problem. High-paying customers hitting hard limits without granular controls is the most visible pain point in the repository.
- **Silent Agent Failures:** Features that break without clear diagnostics—Remote Control silent drops (#34255), Bash tool invocations rendered as text (#63870), and subagent misrouting (#69212)—are the most dangerous class of bugs for developer trust.
- **Session Instability and Regressions:** Long-running sessions become unpredictable. macOS CPU spin loops (#68931), Windows paste corruption (#69234), "Unhandled case" freezing (#59156), and UI pinned to the wrong worktree (#65767) erode confidence in session persistence.
- **Platform Parity Gaps:** Windows users face keybinding conflicts (#23146) and paste issues (#69234). Linux users hit MCP OAuth walls (#69205) and false permission denials (#69074). macOS users see CPU regressions (#68931) and broken automation sandboxing. The experience is uneven across operating systems.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest – 2026-06-18**  
*Generated from repository activity on `openai/codex`*

---

### 1. Today's Highlights
The development cycle has kicked into high gear with three rapid-fire Rust alpha releases (`v0.141.0-alpha.5` through `.7`). However, the bug tracker is flooding with reports of **authentication deadlocks** (legacy phone number verification locking out otherwise secure FIDO2 accounts) and **severe local storage bloat** (SQLite write amplification theoretically reaching ~640 TB/year, plus unbounded Crashpad dump accumulation). On the engineering side, significant pull requests landed for a new **"varlatency" time-awareness system** and **realtime voice continuity**, signaling the core team’s near-term focus on improving agent context and voice UX.

---

### 2. Releases
Three new alpha versions of the Codex Rust engine were published in the last 24 hours without detailed changelogs attached to the data:
- [rust-v0.141.0-alpha.7](https://github.com/openai/codex/releases)
- [rust-v0.141.0-alpha.6](https://github.com/openai/codex/releases)
- [rust-v0.141.0-alpha.5](https://github.com/openai/codex/releases)

The high cadence of releases suggests an aggressive hotfix or feature iteration cycle on the CLI core.

---

### 3. Hot Issues (10 Noteworthy Items)

1. **[#23794 – Context Window Indicator Missing](https://github.com/openai/codex/issues/23794)** (170C, 168👍)  
   The most active issue this week. Users are demanding the return of a visible token/context usage indicator in the Codex Desktop app. Highly voted.

2. **[#17827 – Customizable Status Line Request](https://github.com/openai/codex/issues/17827)** (16C, 71👍)  
   A strong push from the community to add a TUI status bar (token usage, model, git branch) similar to Claude Code. High reaction count.

3. **[#25719 – macOS `syspolicyd`/`trustd` CPU Runaway](https://github.com/openai/codex/issues/25719)** (31C, 39👍)  
   Persistent macOS performance bug causing runaway memory and CPU on both Intel and Apple Silicon.

4. **[#25749 – Legacy Phone Number Auth Lock](https://github.com/openai/codex/issues/25749)** (49C, 30👍)  
   A critical blocker for users with FIDO2/Passkeys who are forced into an unrecoverable SMS OTP flow due to a legacy number.

5. **[#28224 – SQLite Logs Writing ~640 TB/Year](https://github.com/openai/codex/issues/28224)** (6C, 1👍)  
   Extreme local write amplification from feedback logs—a potential SSD endurance killer for long-term CLI users.

6. **[#25921 – Crashpad Dumps Growing Unbounded](https://github.com/openai/codex/issues/25921)** (9C, 2👍)  
   Continuous generation of paired `.dmp` and `_sidecar.json` files consuming +5GB of disk space per day.

7. **[#25737 – CLI Forces SMS OTP over Security Keys](https://github.com/openai/codex/issues/25737)** (11C, 6👍)  
   The browser login honors Advanced Account Security, but the CLI OAuth flow forces a phone OTP step-up, breaking passkey workflows.

8. **[#24030 – macOS Database Malformed After Update](https://github.com/openai/codex/issues/24030)** (6C, 4👍)  
   Codex fails to launch entirely due to a corrupted SQLite state database (`state_5.sqlite`). Requires manual deletion to recover.

9. **[#28823 – 5-Hour Usage Meter Regression](https://github.com/openai/codex/issues/28823)** (4C, 0👍)  
   A brand-new report indicating that the 5-hour rate limit allowance is consuming much faster than historically comparable sessions. Gaining traction.

10. **[#21211 – Thread Navigation Metadata Bloat](https://github.com/openai/codex/issues/21211)** (12C, 2👍)  
    Performance degradation in thread loading and navigation due to unbounded metadata and eager hydration of full history from SQLite.

---

### 4. Key PR Progress (10 Important Opens/Merges)

1. **[#28843 – Persist fsmonitor Status Refreshes](https://github.com/openai/codex/pull/28843)** (Performance Fix)  
   Prevents background Git status from scanning the full worktree on every refresh when Git optional locks are disabled (0 → N full scans on daemon restart).

2. **[#28824 – System Clock Time Reminders](https://github.com/openai/codex/pull/28824)** (Feature / Varlatency 2/n)  
   Introduces a configurable, host-injectable current-time provider that injects UTC timestamps into history before model requests. Foundation for agent time-awareness.

3. **[#28835 – App-Server `currentTime/read`](https://github.com/openai/codex/pull/28835)** (Feature / Varlatency 3/n)  
   Standardizes the time reminder system across the server-client boundary via a simple RPC call.

4. **[#28836 – Support Assistant Realtime Append Text](https://github.com/openai/codex/pull/28836)** (Feature / Voice)  
   Enables realtime voice continuity by allowing replay of assistant text from previous sessions as actual conversation items.

5. **[#28790 – Support Plugin Manifest Path Lists](https://github.com/openai/codex/pull/28790)** (Plugin System)  
   Allows plugin manifests to declare `skills` as an array of path strings, enabling multi-directory skill packages.

6. **[#28838 – Codex Home Instructions Directory](https://github.com/openai/codex/pull/28838)** (Customization)  
   Adds `~/.codex/instructions/` as a global source for loading `*.md` instruction files in deterministic sorted order.

7. **[#28813 – Pause Active Goals Before Esc Interrupts](https://github.com/openai/codex/pull/28813)** (Bug Fix)  
   Ensures active `/goal` states are properly paused when users interrupt via Esc, not just Ctrl+C. Fixes [#28104](https://github.com/openai/codex/issues/28104).

8. **[#28814 – Assign Response Item IDs When Recording History](https://github.com/openai/codex/pull/28814)** (Persistence)  
   Fixes thread resume stability by assigning stable IDs to client-created response items at the history boundary. Critical for rollouts.

9. **[#28784 – Fix `install.sh` Checksum Parsing for mawk](https://github.com/openai/codex/pull/28784)** (Bug Fix)  
   Resolves an installer failure on Debian-based systems where older `mawk` implementations cannot parse the checksum interval expression.

10. **[#28674 – Remote Environment Connection Lifecycle](https://github.com/openai/codex/pull/28674)** (Infrastructure)  
    Improves remote development reliability by managing the lifecycle of remote exec-server connections, distinguishing initial startup from connection failures.

---

### 5. Feature Request Trends

- **Terminal UI Customization:** The most vocal demand is for a **customizable status line** in the TUI ([#17827](https://github.com/openai/codex/issues/17827)). Users want real-time visibility into token usage, model names, rate limits, and git state, mirroring Claude Code’s UX. The 71 👍 on this request reflect a broad desire for developer-oriented telemetry.

- **Context Window & Rate Limit Transparency:** There is a strong push for **visible context indicators** ([#23794](https://github.com/openai/codex/issues/23794)) and clearer rate limit mechanics ([#28823](https://github.com/openai/codex/issues/28823)). The community wants open feedback on what the model is consuming rather than opaque error walls.

- **Plugin & Configuration Extensibility:** The community desires a stable plugin platform. Multiple threads and PRs point to needing **multi-directory skills** ([#28790](https://github.com/openai/codex/pull/28790)), **immutable bundled plugin configs** ([#25758](https://github.com/openai/codex/issues/25758)), and **global instruction files** ([#28838](https://github.com/openai/codex/pull/28838)).

---

### 6. Developer Pain Points

- **Authentication Chokepoints:** The inability to use Passkeys/FIDO2 without a legacy SMS fallback ([#25737](https://github.com/openai/codex/issues/25737), [#25749](https://github.com/openai/codex/issues/25749)) is a critical blocker for teams adopting modern security standards. The divergence between web and CLI auth flows is especially frustrating.

- **Local Storage Bloat:** Between **unbound SQLite logs** ([#28224](https://github.com/openai/codex/issues/28224)) and **endless Crashpad dumps** ([#25921](https://github.com/openai/codex/issues/25921)), Codex can consume tens of gigabytes of disk daily. This is actively hostile to running long-lived agents locally.

- **State Corruption & Data Loss:** Malformed SQLite databases ([#24030](https://github.com/openai/codex/issues/24030)) and **repeated chat history loss** on Windows (multiple reports from user `Slyke` across versions) erode trust in the persistence layer.

- **Opaque Performance Regressions:** The **5-hour usage meter** consuming faster than comparable sessions ([#28823](https://github.com/openai/codex/issues/28823)) and **syspolicyd CPU spikes** on macOS ([#25719](https://github.com/openai/codex/issues/25719)) indicate latent observability gaps that waste developer time triaging.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest - 2026-06-18

## 1. Today's Highlights

The Gemini CLI team released two versions simultaneously (`v0.47.0` stable and `v0.48.0-preview.0`), indicating active parallel development streams. A critical fix is in progress for `write_file` silently corrupting Jupyter Notebook and JSON files (#28000), while maintainers are aggressively patching CI/CD supply-chain attack vectors (#27780, #27783). Community frustration remains concentrated on agent reliability, with significant engagement on the generalist agent hang (#21409) and shell command deadlocks (#25166).

## 2. Releases

- **v0.47.0** ([Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0)): Stable release. Key change includes respecting backend definitions. Auto-generated changelog.
- **v0.48.0-preview.0** ([Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-preview.0)): Preview release. Introduces a cooldown period for Dependabot npm updates to reduce dependency churn, along with general refactoring.

## 3. Hot Issues

1. **#21409 [P1] Generalist agent hangs** ([Link](https://github.com/google-gemini/gemini-cli/issues/21409)) — ⚠️ 8 reactions. The CLI hangs indefinitely when deferring to the generalist agent. Community workaround exists (blocking sub-agent use), but this is a top-tier UX blocker.
2. **#25166 [P1] Shell command stuck on "Waiting input"** ([Link](https://github.com/google-gemini/gemini-cli/issues/25166)) — Agent holds a shell session open as "Awaiting user input" even after trivial commands complete. Frequent recurrence reported.
3. **#22323 [P1] Subagent false success after MAX_TURNS** ([Link](https://github.com/google-gemini/gemini-cli/issues/22323)) — `codebase_investigator` reports `status: "success"` and `Termination Reason: "GOAL"` despite hitting turn limits with zero analysis. Highly deceptive.
4. **#24353 [P1] Robust component level evaluations** ([Link](https://github.com/google-gemini/gemini-cli/issues/24353)) — Tracks building a mature internal eval framework for agent components, expanding from 76 existing behavioral eval tests across 6 Gemini models.
5. **#21983 [P1] Browser subagent fails on Wayland** ([Link](https://github.com/google-gemini/gemini-cli/issues/21983)) — Platform-specific blocker preventing browser agent usage on Linux Wayland sessions.
6. **#26525 [P2] Add deterministic redaction to Auto Memory** ([Link](https://github.com/google-gemini/gemini-cli/issues/26525)) — Security concern: secrets are transmitted to the model before redaction occurs, and extraction prompts are the only guard.
7. **#26522 [P2] Stop Auto Memory retrying low-signal sessions** ([Link](https://github.com/google-gemini/gemini-cli/issues/26522)) — The background extraction agent endlessly re-processes uninteresting sessions because it skips them instead of marking them as processed.
8. **#22745 [P2] AST-aware file reads, search, and mapping** ([Link](https://github.com/google-gemini/gemini-cli/issues/22745)) — EPIC investigating AST-aware tooling for precise method bounds reading and reduced token noise versus plain-text approaches.
9. **#22672 [P2] Agent should discourage destructive behavior** ([Link](https://github.com/google-gemini/gemini-cli/issues/22672)) — Community requests for safer defaults on `git reset --force`, destructive fs operations, and database modifications.
10. **#21968 [P2] Gemini does not use skills and sub-agents enough** ([Link](https://github.com/google-gemini/gemini-cli/issues/21968)) — Custom skills and sub-agents are largely ignored by the core agent unless explicitly instructed, undermining the extensibility model.

## 4. Key PR Progress

1. **#28000 [OPEN] fix(core-tools): resolve Jupyter Notebook and JSON corruption** ([Link](https://github.com/google-gemini/gemini-cli/pull/28000)) — Critical fix for `write_file` silently corrupting `.ipynb` and JSON files, causing environments like Colab to revert changes to checkpoints.
2. **#27996 [OPEN] fix(core): decode response body using charset from Content-Type header** ([Link](https://github.com/google-gemini/gemini-cli/pull/27996)) — Fixes `web-fetch` garbled text on non-UTF-8 pages (GBK, ISO-8859-1), commonly encountered on Asian and legacy sites.
3. **#27994 [OPEN] fix(core): insert skill/agent content literally in system prompt substitutions** ([Link](https://github.com/google-gemini/gemini-cli/pull/27994)) — Patches `String.prototype.replace` usage that broke prompt construction when skill definitions contained special regex characters.
4. **#27854 [CLOSED] Fix/pending tools and trust overrides** ([Link](https://github.com/google-gemini/gemini-cli/pull/27854)) — Prevents premature agent state progression during tool approval waits and eliminates race conditions in sequential file writes.
5. **#27987 [OPEN] fix(cli): throw FatalConfigError instead of process.exit** ([Link](https://github.com/google-gemini/gemini-cli/pull/27987)) — Refactors argument parsing for testability, resolving Vitest hangs during `--help`/`--version` E2E tests.
6. **#27859 [OPEN] feat(cli): add native drag-and-drop and Cmd+V clipboard image pasting** ([Link](https://github.com/google-gemini/gemini-cli/pull/27859)) — Brings visual multimodal parity to the terminal, addressing a long-standing QoL gap.
7. **#27780 [OPEN] security: gate chained E2E on same-repository checkout** ([Link](https://github.com/google-gemini/gemini-cli/pull/27780)) — Fixes a critical supply-chain vulnerability where fork PRs could exfiltrate `GEMINI_API_KEY` via attacker-controlled artifact metadata.
8. **#27948 [OPEN] chore(deps): pin dependencies and enforce 14-day update cooldown** ([Link](https://github.com/google-gemini/gemini-cli/pull/27948)) — Strips all `^`/`~` ranges and enforces a cooldown for automated dependency updates to reduce regression risk.
9. **#27997 [OPEN] docs: remove references to deprecated consumer and free tiers** ([Link](https://github.com/google-gemini/gemini-cli/pull/27997)) — Cleans up docs following the shutdown of consumer/free tiers (Gemini Code Assist individuals, etc.), effective June 1st.
10. **#27788 [OPEN] test(core): add subfolder ignore test for getFolderStructure** ([Link](https://github.com/google-gemini/gemini-cli/pull/27788)) — Adds regression coverage for `.gitignore` rules applying to nested subdirectories in folder traversal.

## 5. Feature Request Trends

- **Context-Aware Intelligence:** Multiple EPICs push toward deep code structure awareness. AST-based tools for reading, searching, and mapping codebases are under active investigation, aiming for more precise edits and reduced token overhead (#22745, #22746).
- **Persistent and Secure Memory:** The "Auto Memory" feature suite is the largest single area of active iteration. Requests center on deterministic secret redaction (#26525), preventing wasted loops on low-signal sessions (#26522), and quarantining invalid inbox patches (#26523). Users expect memory to be both background-aware and secure.
- **Autonomous Delegation:** Users want the core agent to intelligently dispatch work to custom sub-agents and skills without explicit prompting. The gap between the platform's extensibility and the model's willingness to use it is a persistent theme (#21968, #21432).
- **Safety-Minded Execution:** A clear demand for the agent to inherently prefer safe flags, warn before destructive `git`/`fs`/`db` operations, and gracefully handle interactive prompts without hanging (#22672, #22465).
- **Terminal-Native Rich Interactions:** Beyond basic text, users expect drag-and-drop file input, clipboard image pasting, and flicker-free terminal resizing. The CLI is increasingly viewed as a first-class IDE surface, not just a REPL (#27859, #21924).

## 6. Developer Pain Points

- **Unreliable State Management:** This is the dominant frustration. The agent frequently hangs (#21409), falsely reports success after hitting limits (#22323), and gets permanently stuck waiting for input on completed processes (#25166). These issues directly erode trust in agentic workflows.
- **Configuration Neglect:** The agent routinely ignores user configuration. `settings.json` overrides are not honored (#22267), agent permissions are disregarded (#22093), and symlinked agent files are silently skipped (#20079). Tooling fails without feedback.
- **Silent Data Corruption:** The `write_file` tool corrupting structured file formats without error messages (#28000) and `web-fetch` returning garbled text for non-UTF-8 content (#27996) create cascading debugging overhead.
- **Scalability Ceilings:** Hitting 400 errors with >128 tools (#24246) and experiencing degraded performance with large contexts indicate the architecture needs better tool selection and context window management.
- **CI/CD Supply Chain Risks:** External fork PRs posed a credential exfiltration risk through chained workflows (#27780, #27783). The ongoing churn of dependency updates is forcing strict pinning and cooldown policies (#27948) to maintain stability.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for 2026-06-18.

---

## 1. Today's Highlights
The fallout from the June 16 Copilot outage dominates today’s tracker, with users reporting models stuck in a “Blocked/Disabled” state (#3832) and transient API error loops (#3831). Beyond the outage, the community is heavily engaged in discussions around granular permission controls for Interactive Mode (#1973) and the inability to create silent plugin hooks (#2643). Interoperability issues with custom BYOK models (#3839) and regressions in subagent MCP tool access (#3812) indicate sharp growing pains as the ecosystem moves toward complex multi-agent workflows.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Hot Issues (Top 10)

1. **[#1973 – Tool Whitelist for Interactive Mode](https://github.com/github/copilot-cli/issues/1973)** (20 👍)
   A highly-requested feature asking for a middle ground between approving every single tool call (including safe read-only operations) and `/allow-all`. Users want a configurable whitelist to reduce friction without sacrificing safety.

2. **[#3832 – All Models 'Blocked/Disabled' After June 16 Outage](https://github.com/github/copilot-cli/issues/3832)** (13 👍)
   Post-outage bug where the model selection interface rendered every model unusable. Quickly closed, but reveals fragile client state management when the upstream API recovers.

3. **[#2643 – preToolUse: Silent Command Rewrite via updatedInput](https://github.com/github/copilot-cli/issues/2643)** (10 Comments)
   Plugin hooks designed to rewrite commands silently still trigger confirmation dialogs. Makes it impossible to build transparent automated workflows, a core friction point in the plugin permissions model.

4. **[#254 – Keeps Asking to Login Again](https://github.com/github/copilot-cli/issues/254)** (9 Comments, 4 👍)
   A long-running authentication bug (dating back to Oct 2025) where the CLI forgets session tokens, particularly affecting GitHub Business accounts. Remains a recurring frustration for corporate users.

5. **[#3839 – Ollama Cloud BYOK Fails on `custom_tool_call` Payload](https://github.com/github/copilot-cli/issues/3839)** (7 👍)
   Fleet Mode with custom endpoints fails because Copilot CLI sends a proprietary payload format that OpenAI-compatible routers like Ollama reject. Blocks organizations from deploying BYOK models.

6. **[#3560 – Duplicate Tool Call ID Error](https://github.com/github/copilot-cli/issues/3560)** (5 Comments)
   A sudden WebSocket error where the API rejects duplicate `fc_call` IDs after a tool use turn. Suggests a session-state corruption bug that forces full session restarts.

7. **[#3074 – Add `/effort` Command for Reasoning Effort](https://github.com/github/copilot-cli/issues/3074)** (5 👍)
   Users want an inline slash command to quickly toggle reasoning effort (Low/Medium/High) rather than navigating the multi-step `/model` menu, reflecting a desire for faster iterative tuning.

8. **[#3355 – Configurable Context Window for Claude Opus 4.6](https://github.com/github/copilot-cli/issues/3355)** (4 👍)
   The CLI caps Claude Opus at 200K tokens despite a native 1M capacity. Users report frequent forced compaction during deep technical sessions and are asking for configurable limits.

9. **[#3730 – Support Enterprise-Managed Custom Models](https://github.com/github/copilot-cli/issues/3730)** (4 👍)
   Enterprise admins can add custom models centrally in VS Code, but they do not appear in Copilot CLI. Creates a feature gap that forces teams to choose between CLI and IDE workflows.

10. **[#3812 – Subagents Can No Longer Access MCP Tools](https://github.com/github/copilot-cli/issues/3812)**
    A regression where custom subagents lose visibility of MCP tools tied to the deferred loading system. Critical for complex agentic workflows that rely on external tool ecosystems.

## 4. Key PR Progress
No pull requests were updated or merged in the `github/copilot-cli` repository in the past 24 hours. The project appears to be in a stabilization phase following the June 16 outage, with the team batch-closing several bug reports and low-priority feature requests (see #3820, #3828, #3830).

## 5. Feature Request Trends
- **Granular Permissions & Safety Models:** The persistent high engagement on #1973 (tool whitelist) and #2643 (silent hooks) shows the community wants a multi-tiered trust system instead of the current binary “allow all or confirm every call” model.
- **Model Control & Context:** A strong push against rigid context limits (#3355) and fixed reasoning levels (#3074). Users want session-level configuration that matches the full capability of the underlying models.
- **Enterprise & BYOK Parity:** Organizations want a unified model management experience across IDE and CLI (#3730), and the ability to connect arbitrary OpenAI-compatible endpoints without payload compatibility breaks (#3839).
- **Plugin & MCP Ecosystem:** Requests for batch plugin updates (#3830), skills declaring MCP servers (#3292), and pre-loaded MCP tools (#3787) indicate the plugin system is approaching critical mass and needs better lifecycle tools.

## 6. Developer Pain Points
- **Post-Outage Recovery:** The June 16 outage exposed weak client-side handling of upstream failures, leaving users with blocked models (#3832), infinite retry loops (#3831), and poisoned sessions (#3791).
- **Authentication Instability:** Login session loss (#254) remains a lingering reliability issue, particularly impacting enterprise accounts without clear resolution.
- **Interoperability Barriers:** Proprietary WebSocket payloads blocking BYOK models (#3839) and content exclusions unexpectedly leaking into the CLI (#3841) create blockers in managed environments.
- **Agent Consistency:** Regressions in subagent behavior—losing MCP tools (#3812) and running unconfigured models (#3824)—undermine trust in the multi-agent feature set.
- **Ergonomic Friction:** Seemingly small UX issues accumulate, such as `--resume` silently failing on filenames with spaces (#3754) and the lack of a bulk plugin update command (#3830).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-18

## Today's Highlights
The Kimi CLI repository experienced a quiet day with no new releases or merged pull requests. Two new issues were filed that highlight emerging friction points for the developer community: enterprise network security restrictions blocking authentication, and a request for more dynamic runtime execution capabilities. While activity was low, both items touch on critical usability gaps for power users and enterprise adopters.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues
*Two issues were created/updated in the reporting period. Both are high-signal requests regarding core developer experience.*

1. **#2459 [Feature Request] Support switching execution mode during session running (Agent ↔ Cluster)**
   - **Author:** PresentXoX
   - **Summary:** Proposes the ability to toggle between local Agent mode and Cluster mode mid-session without terminating the current session or losing conversational context.
   - **Why it matters:** This reflects a need for dynamic workflow composition. Users working on complex multi-stage tasks must currently tear down their session to change the execution backend, which breaks flow and context retention. If adopted, this would be a significant UX improvement for hybrid workloads.
   - **Community Reaction:** Newly opened; no comments or reactions yet.
   - **Link:** [Issue #2459](https://github.com/MoonshotAI/kimi-cli/issues/2459)

2. **#2458 [Enhancement] Add option to ignore SSL certificate**
   - **Author:** dmorsin
   - **Summary:** Requests a `--insecure` flag or equivalent to bypass SSL certificate validation. The user states that organizational antivirus software performs MITM decryption, injecting a corporate certificate into the TLS handshake, which causes authentication to fail.
   - **Why it matters:** The absence of an insecure/custom-CA option is a hard blocker for corporate and regulated environments (Zscaler, Palo Alto proxies, etc.). This request signals that developers are actively trying to adopt Kimi CLI in enterprise settings but are hitting immediate authentication failures.
   - **Community Reaction:** Newly opened; no comments or reactions yet.
   - **Link:** [Issue #2458](https://github.com/MoonshotAI/kimi-cli/issues/2458)

## Key PR Progress
No pull requests were opened, merged, or updated in the last 24 hours.

## Feature Request Trends
Based on the high-signal items filed today, the following feature directions are emerging:

- **Runtime Execution Flexibility (#2459):** Users want the ability to change operational parameters (e.g., switching between local and distributed execution) without restarting a session. This points to a user base that depends on long-running, context-heavy workflows and finds static session modes limiting.
- **Enterprise Connectivity Controls (#2458):** The immediate ask is for an SSL bypass flag, but the deeper trend is a need for robust corporate proxy support (MITM inspection, custom Certificate Authorities, environment-aware `HTTP_PROXY` integration). The community expects production-grade network handling.

## Developer Pain Points

- **Enterprise Network Lockouts:** The SSL certificate issue (#2458) is a recurring pain point for productivity CLIs entering the enterprise market. Without support for custom certificates or an insecure mode, developers on managed devices are completely blocked from authenticating, representing a significant barrier to adoption in large organizations.
- **Session Rigidity:** The request for mid-session execution mode switching (#2459) suggests that the current session model is perceived as inflexible. Forcing users to exit, reconfigure, and restart a session to change backends creates unnecessary friction, particularly for users who manage mixed workloads (local testing → cluster processing).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for June 18, 2026.

---

# OpenCode Community Digest – June 18, 2026

**Digest generated from:** [GitHub: anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## 1. Today's Highlights

OpenCode **v1.17.8** ships today with welcome performance fixes for session timeline rendering and critical provider compatibility patches for MCP tool schemas and Cloudflare AI Gateway. The community is heavily engaged on a massive thread regarding **inconsistent GPT response times** (#29079), while feature requests for a **native VS Code extension** (#11176) and **automatic task-based model selection** (#8456) continue to draw strong support. On the development front, a flurry of PRs landed focusing on core edit tooling, CLI session management, and fixing plugin hook regressions.

---

## 2. Latest Release: v1.17.8

**Released June 18, 2026**

- **Core Improvements:** Session timelines now load significantly faster with reduced flicker and scroll instability.
- **Bugfixes:**
  - OpenAI-compatible providers correctly accept MCP tool schemas that were previously blocked by validation. (@jquense)
  - The Cloudflare AI Gateway integration now properly applies the configured API key. (@keefetang)

---

## 3. Hot Issues

| # | Issue | Why It Matters |
|---|-------|----------------|
| **[#29079](https://github.com/anomalyco/opencode/issues/29079)** | **GPT Models take too long to respond** (117 comments, 49 👍) | The highest-traffic issue today. Users report latency variance of seconds to minutes for simple tasks with GPT-5.4. A top-tier reliability problem for the primary model family. |
| **[#11176](https://github.com/anomalyco/opencode/issues/11176)** | **[FEATURE] Official VS Code Extension** (23 comments, 110 👍) | Tops the charts in community demand. VS Code integration is seen as the primary barrier to broader adoption among professional IDE users. |
| **[#17994](https://github.com/anomalyco/opencode/issues/17994)** | **[FEATURE] Multi-Agent Orchestration** (21 comments) | Reflects the industry shift toward parallel agent teams operating in isolated workspaces, mirroring features from Cline and other dev tools. |
| **[#6096](https://github.com/anomalyco/opencode/issues/6096)** | **[FEATURE] Tokens per Second Display** (18 comments, 55 👍) | Strong demand for performance observability. Without TPS, users rely on subjective speed judgments. |
| **[#8456](https://github.com/anomalyco/opencode/issues/8456)** | **[FEATURE] Task-Based Model Selection** (7 comments, 36 👍) | High like-to-comment ratio implies broad silent support for automatic model routing (cheap models for edits, strong models for architecture). |
| **[#31119](https://github.com/anomalyco/opencode/issues/31119)** | **[BUG] `Error: no such column: name`** (4 comments) | A critical database migration regression completely blocking users who update from older versions. |
| **[#31204](https://github.com/anomalyco/opencode/issues/31204)** | **[BUG] `session_message.seq` constraint failure** (7 comments) | Another high-severity SQLite crash triggered by agent switching after recent June 3-5 schema migrations. |
| **[#23566](https://github.com/anomalyco/opencode/issues/23566)** | **Docs suggest LSP is enabled by default** (10 comments, 20 👍) | A trust-breaking documentation gap where the default LSP behavior contradicts automated setup guides. |
| **[#24817](https://github.com/anomalyco/opencode/issues/24817)** | **Ctrl+Z closes/suspends OpenCode (Linux)** (5 comments) | A classic terminal UX trap where SIGTSTP overrides undo, making accidental session suspension easy. |
| **[#32444](https://github.com/anomalyco/opencode/issues/32444)** | **GLM-5.2 variants blocked by blanket regex** (3 comments, 8 👍) | Highlights a systematic issue where provider model variants are blocked by overly broad exclusion filters in the core transform logic. |

---

## 4. Key PR Progress

| PR | Description | Author & Impact |
|----|-------------|-----------------|
| **[#32771](https://github.com/anomalyco/opencode/pull/32771)** | `feat(tui): show assistant completion time` | @joeyparis — Appends turn completion time to run summaries for better performance visibility. |
| **[#32767](https://github.com/anomalyco/opencode/pull/32767)** | `fix(tui): restore ESC interrupt for delegated subagent sessions` | @tobwen — Fixes a critical regression where ESC to interrupt subagent sessions was broken (Closes #3699, #4073, #23534). |
| **[#32761](https://github.com/anomalyco/opencode/pull/32761)** | `feat(core): port V1 fuzzy edit matching to V2 core edit tool` | @Robin1987China — A major architectural upgrade porting 9 fuzzy replacer strategies (Levenshtein, similarity thresholds) to the V2 core. |
| **[#32752](https://github.com/anomalyco/opencode/pull/32752)** | `feat(opencode): add `session select` interactive picker` | @sigsegv0x0b — New CLI command using `@clack/prompts` autocomplete for interactive session navigation. |
| **[#32731](https://github.com/anomalyco/opencode/pull/32731)** | `feat(opencode): auto-discover models from OpenAI-compatible providers` | @sethjones — Major config simplification. OpenCode now queries `GET /models` instead of requiring manual model lists. (Also handled by #27554) |
| **[#32750](https://github.com/anomalyco/opencode/pull/32750)** | `feat: add global session list scope toggle` | @ZYC99 — Adds `Ctrl+g` keybinding to cycle between local, project, and global session scopes. |
| **[#30879](https://github.com/anomalyco/opencode/pull/30879)** | `feat(acp): improve display and replay of shell commands` | @imnotlxy — Enhances ACP mode with real-time output streaming and actual commands as tool titles. |
| **[#23688](https://github.com/anomalyco/opencode/pull/23688)** | `feat(app): add markdown preview with mermaid diagram support` | @Kiruno-lz — Adds built-in Markdown preview with full Mermaid (v11.4.1) rendering. |
| **[#32758](https://github.com/anomalyco/opencode/pull/32758)** | `fix(opencode): re-read plugin.trigger output` | @pplan1122 — Critical plugin ecosystem fix where `output.messages` array replacements were silently discarded. |
| **[#32753](https://github.com/anomalyco/opencode/pull/32753)** | `fix(web): add clipboard fallback for non-HTTPS contexts` | @GautamKumarOffical — Fixes copy-to-clipboard buttons for localhost/HTTP local development. |

---

## 5. Feature Request Trends

- **Intelligent Provider Routing:** The community is asking for the tool to *autonomously* select models. Task-based routing (#8456) and automatic model selection (#32736) are strong signals for a "set and forget" model strategy that optimizes for cost/latency against task complexity.
- **Deep IDE Integration:** The demand for a native VS Code extension (#11176) is the single strongest community signal, outpacing all other feature requests by reaction count.
- **Advanced Agent Safety & Control:** Users are maturing beyond basic code generation. Requests for multi-agent orchestration (#17994), runtime permission toggles (#7928), and isolated workspaces indicate a shift toward "managing AI teams" rather than just chatting.
- **Provider Parity:** There is growing friction when new models (e.g., GLM-5.2) are released but not immediately supported or are blocked by generic regex filters (#32444, #32620, #32172). Users expect rapid, first-class support for popular new provider offerings.

---

## 6. Developer Pain Points

- **Database Migration Regressions:** The most acute pain point this week. Issues #31204 (`session_message.seq` constraint) and #31119 (`no such column`) show that recent schema changes (June 3-5) are causing hard crashes on update. This severely erodes trust in the upgrade path.
- **Inconsistent GPT Performance:** The firestorm in #29079 (117 comments) highlights unpredictable latency that makes the primary model family feel unreliable. This is a top-tier stability and UX concern for the largest user segment.
- **Terminal Garbage / ANSI Escape Code Leakage:** A recurring nightmare for Windows and Wezterm users. Issues #21277, #16675, #32754, and #3541 describe terminals left in broken states with raw escape codes after crashes or reinstallations, creating a poor first impression for CLI-first users.
- **Plugin Ecosystem Friction:** Issue #32758 reveals a subtle but severe bug where plugin outputs are silently dropped. For developers investing in the plugin API, unreliable hook execution is a dealbreaker.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — June 18, 2026

This week’s activity reflects a project rapidly maturing beyond its core Anthropic/OpenAI workflows. The community directed strong attention toward provider flexibility (Azure Foundry, SiliconFlow, Warp terminal), debugging transparency (raw HTTP error bodies), and structural SDK issues like dependency duplication. A key cluster of fixes targeted route correctness for secondary providers, while several TUI bugs around scrolling, model selection, and markdown rendering were actively patched.

---

## 2. Releases

No new versions were published in the last 24 hours. Several fixes and features are incubating on `main` for the next release.

---

## 3. Hot Issues

**#5825 [OPEN] [bug, inprogress] Streaming markdown forces scroll to bottom**
*Posted by xl0 | 12 comments | [Link](earendil-works/pi Issue #5825)*  
A prominent UX breakage: when `clear on shrink` is enabled, every re-render jumps the viewport to the bottom, making it impossible to read earlier output while the agent streams. A targeted fix is now in flight via PR #5846.

**#5653 [OPEN] [inprogress] Move off Shrinkwrap**
*Posted by yoyofield | 11 comments | [Link](earendil-works/pi Issue #5653)*  
Installing `pi-ai` and `pi-coding-agent` together duplicates shareable modules on disk. Because the provider registry is a module-level `Map`, the two copies become separate instances—a classic Node.js resolution footgun that breaks shared state. The `inprogress` label indicates maintainers are actively restructuring.

**#3715 [CLOSED] [bug] local-llm streams terminate at 5 min from undici default bodyTimeout**
*Posted by LooSik | 11 comments | 👍 4 | [Link](earendil-works/pi Issue #3715)*  
Long running tool calls against local vLLM/Qwen3 backends die with `UND_ERR_BODY_TIMEOUT`. The user-facing `timeoutMs` config cannot override the lower-level undici default. High engagement (4 thumbs up) signals a significant underserved segment of local-LLM users.

**#5763 [OPEN] [bug, inprogress] Providers swallow HTTP error body**
*Posted by stephanmck | 5 comments | [Link](earendil-works/pi Issue #5763)*  
Behind a reverse proxy or gateway, non-2xx responses get their bodies stripped by most providers. A 403 surfaces as `UnknownError` on Bedrock or `403 status code (no body)` on OpenAI-shaped endpoints, making upstream debugging impossible. Two concurrent PRs (#5832, #5828) target this gap.

**#5700 [OPEN] Support multiple live agent sessions with TUI switching**
*Posted by shmuelamit | 5 comments | [Link](earendil-works/pi Issue #5700)*  
Currently `switchSession` tears down the running session. Users want concurrent background agents (e.g., a long-running review while chatting in another session). Complex architectural ask that would unlock power-user workflows.

**#5696 [CLOSED] [bug] Model name does not refresh in TUI bottom corner on CTRL+P**
*Posted by mxr576 | 10 comments | [Link](earendil-works/pi Issue #5696)*  
Off-by-one UX bug where the model selection appears to require two keystrokes to advance one slot. Shows structural fragility in keyboard-driven navigation state management.

**#534 [CLOSED] config folder is out of place on Linux**
*Posted by Ramblurr | 9 comments | 👍 20 | [Link](earendil-works/pi Issue #534)*  
The highest 👍 count in this dataset. Linux users demand XDG Base Directory compliance—currently Pi writes directly to `$HOME`. A signal that platform-specific polish carries outsized weight in community perception.

**#5654 [OPEN] Add `excludeFromContext` to custom messages sent via `sendMessage()`**
*Posted by zachmeador | 7 comments | 👍 1 | [Link](earendil-works/pi Issue #5654)*  
Enables richer bespoke UIs without context-window waste. Mirrors the flag already available on bash-execution messages. A small API addition with high leverage for extension authors.

**#5827 [OPEN] [bug] Warp terminal not detected for Kitty image protocol**
*Posted by dodiego | 3 comments | [Link](earendil-works/pi Issue #5827)*  
Warp is a dominant macOS terminal but falls back to text rendering for images because its `TERM_PROGRAM` is not matched. PR #5841 proposes adding detection via `WARP_SESSION_ID` and `WARP_TERMINAL_SESSION_UUID`.

**#5797 [CLOSED] [bug] File edits break encoding of CP-1252 stored files on Windows**
*Posted by hendrikp | 4 comments | [Link](earendil-works/pi Issue #5797)*  
Working with legacy C++ projects in Windows, file edits silently convert ANSI to UTF-8, breaking string literals. Exposes a gap in round-trip encoding preservation for non-UTF-8 codebases.

---

## 4. Key PR Progress

**#5846 [OPEN] fix(tui): stabilize streaming code fence rendering**
*Author: xl0 | [Link](earendil-works/pi PR #5846)*  
Closes the scroll-jump issue (#5825). Directly addresses one of the most disruptive open UX bugs when reviewing streaming agent output.

**#5859 [OPEN] fix(ai): send responses prompts as instructions**
*Author: theBucky | [Link](earendil-works/pi PR #5859)*  
Corrects system prompt routing for the OpenAI Responses API. Sending `context.systemPrompt` as replayed `input` messages was semantically incorrect; this changes it to the `instructions` top-level field. Affects OpenAI, Azure OpenAI, and Codex Responses providers.

**#5849 [CLOSED] feat(ai): add Azure AI Foundry provider for Anthropic Claude**
*Author: pvjagtap | [Link](earendil-works/pi PR #5849)*  
First-class support for Azure-hosted Anthropic Claude models with full Entra ID auth and base URL parity with the `anthropic-foundry` SDK. A significant enterprise-friendly push.

**#5832 [OPEN] fix(ai): surface provider HTTP error body instead of opaque SDK message**
*Author: stephanmck | [Link](earendil-works/pi PR #5832)*  
Fixes #5763. Routes provider catch blocks through a shared error formatter that falls back to raw response bodies. Implements for OpenAI-shaped, Google, Bedrock, Vertex, and Mistral providers.

**#5829 [CLOSED] feat: add "max" thinking level for adaptive reasoning models**
*Author: mcphailtom | [Link](earendil-works/pi PR #5829)*  
Extends `ThinkingLevel` from `xhigh` to `max` for models that advertise it (Claude Opus 4.8/4.7, Sonnet 4.6). Simple capability gap plugged with a clear API surface.

**#5738 [CLOSED] fix(ai): price anthropic 1h cache writes at 2x input**
*Author: theBucky | [Link](earendil-works/pi PR #5738)*  
Anthropic splits cache creation into 5‑minute and 1‑hour slots. Pi was incorrectly applying the 5‑minute rate for all writes, undercharging users for longer-lived cache entries. Fix reads `ephemeral_1h_input_tokens` explicitly.

**#5841 [OPEN] feat(tui): detect Warp terminal and enable Kitty image protocol**
*Author: dodiego | [Link](earendil-works/pi PR #5841)*  
Fixes #5827. Adds detection via `TERM_PROGRAM`, `WARP_SESSION_ID`, and `WARP_TERMINAL_SESSION_UUID` so inline images render without requiring manual `TERM_PROGRAM=kitty` hacks.

**#5801 [CLOSED] Nixify pi**
*Author: o1lo01ol1o | [Link](earendil-works/pi PR #5801)*  
Adds Nix flake packaging to the repository (`nix build path:$PWD#pi`). Opens the door for declarative system configuration and NixOS users.

**#5833 [CLOSED] Compaction-related fixes**
*Author: DzmitryTheStreak | [Link](earendil-works/pi PR #5833)*  
Three small but effective changes to session compaction: reordering the summary generation to preserve more useful content, and two related optimizations that reduce token waste during context windows.

**#5812 [CLOSED] fix(tui): protect pipe characters inside inline code in markdown tables**
*Author: aliou | [Link](earendil-works/pi PR #5812)*  
Classic markdown parser footgun: `|` inside backticks within table cells was interpreted as a column delimiter. Overrides the table renderer with a custom tokenizer to properly escape inline code.

---

## 5. Feature Request Trends

**Provider & Model Ecosystem Expansion**
The strongest signal this cycle is demand for broader provider support. SiliconFlow (#4742) and Azure AI Foundry (#5849) landed as formal requests or contributions. Users also want per-model configuration, particularly context window sizing (GitHub Copilot 1M, #5768) and reasoning effort levels (GLM-5.2, #5770; Claude Max thinking, #5829). The community is clearly running Pi against a wide range of backends beyond the core supported pair.

**Richer TUI & Session Control**
There is a distinct push for power-user TUI improvements: multiple concurrent agent sessions (#5700), a richer RPC interface (#5810, #5654) that exposes session trees programmatically, and multimedia prompt support for image/audio/video (#3200). These point toward Pi being used as a platform for building custom AI interfaces, not just a chatbot.

**Configuration Locality & Standards**
Requests to move `--no-skills` / `--skill` into project-level `.pi/settings.json` (#5570) and the long-running XDG config folder compliance (#534) show a desire for deterministic, shareable project configuration that follows OS conventions.

---

## 6. Developer Pain Points

**Dependency Duplication Breaking Shared State (#5653)**
The most critical structural pain. Installing both `pi-ai` and `pi-coding-agent` doubles the representation of the provider registry because Node.js treats them as separate module instances. For anyone building on the SDK, this creates hard-to-diagnose bugs where registered providers vanish.

**Opaque Error Handling from Non-Standard Setups (#5763, #3715)**
Whether it is a local proxy, a gateway (e.g., Vercel AI SDK), or an edge LLM, the provider layer currently throws away the most useful diagnostic data. The volume of concurrent fixes (#5832, #5828, #3715) confirms this is a top-priority irritant for the developer audience.

**Platform Encoding Gaps (#5797)**
Silent character encoding conversion on Windows edits breaks older codebases. While niche, it undermines confidence in the tool for users working in non-UTF-8 environments, particularly legacy C++.

**Linux Standards Compliance (#534)**
Writing config directly to `$HOME` is a recurring sore point for Linux users. The 20 👍 on this issue make it the most supported single request in the data—a strong signal that platform convention adherence matters disproportionately to that segment of the community.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-18

## 1. Today's Highlights
v0.18.3 ships as the latest stable release, refining permission cancellation flow and file history tracking. A critical fix for runaway tool-call loops (PR #5279) is under review, addressing a core stability vulnerability. Meanwhile, the community continues to press hard for token usage transparency and simpler custom provider configuration, while maintainers advance heavy architectural work on session resilience and provider abstraction.

---

## 2. Releases

**v0.18.3** – Latest stable release.
- `fix(cli)`: Stop execution after a cancelled `ask_user_question` flow.
- `fix(core)`: Track supported `sed` edits in file history for better rollback integrity.
[Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.3)

**v0.18.2** – Previous stable release.
- `fix`: Warn on oversized context instructions to prevent silent truncation.
- `docs`: Correct stale defaults, CLI syntax, and tool naming drift.
[Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.2)

**v0.18.3-nightly** – Ongoing development build with the latest commits.

---

## 3. Hot Issues

*(Selected 10 of 50 recently active issues by relevance and engagement)*

1. **[#3203](https://github.com/QwenLM/qwen-code/issues/3203) – Qwen OAuth Free Tier Policy Adjustment** (151 💬)  
   Proposes slashing the daily free limit from 1,000 to 100 requests immediately. The thread reveals significant community frustration and concern over access restrictions. Signals active monetization pressure.

2. **[#4479](https://github.com/QwenLM/qwen-code/issues/4479) – Need Daily Token Consumption Statistics** (16 💬)  
   A user reports a single session consumed 30M tokens and requests a dashboard/command for tracking daily usage. Reflects the highest-velocity feature demand across the issue tracker.

3. **[#3384](https://github.com/QwenLM/qwen-code/issues/3384) – Unable to Add OpenAI-Compatible Local LLM** (15 💬)  
   Configuration friction with local models (Qwen3.6-35B on VLLM). Despite following docs, users hit persistent setup errors. Highlights gaps in settings auto-detection.

4. **[#1855](https://github.com/QwenLM/qwen-code/issues/1855) – OAuth Session Persists After Switching to API Key** (14 💬)  
   Auth state not properly invalidated when migrating from OAuth to a paid API key, causing persistent 401 errors. A critical UX bug for paying customers.

5. **[#3335](https://github.com/QwenLM/qwen-code/issues/3335) – Internal Error: 401 Invalid Access Token** (14 💬)  
   Token expiration handling produces opaque errors. Users receive no actionable guidance on re-authentication.

6. **[#3307](https://github.com/QwenLM/qwen-code/issues/3307) – Endless "Temporarily Out of Stock" Coding Plan** (10 💬)  
   The Alibaba Cloud Coding Plan has been unavailable for over a week. Users who want to pay are blocked, creating a business continuity crisis.

7. **[#3914](https://github.com/QwenLM/qwen-code/issues/3914) – API Fetch Failed on Node.js 26** (9 💬)  
   Connection errors on Node.js 26 due to `fetch`/`dispatcher` changes. Growing platform compatibility pain as users adopt the latest runtime.

8. **[#5267](https://github.com/QwenLM/qwen-code/issues/5267) – `context.fileName` Setting Doesn't Work** (5 💬)  
   Global config to attach custom context files (e.g., `QWEN.md`) is ignored. A regression in settings handling.

9. **[#5234](https://github.com/QwenLM/qwen-code/issues/5234) – Tool Calls Stuck in Infinite Loop** (4 💬)  
   Agent enters an unbreakable tool-call loop. Directly prompted the circuit-breaker fix in PR #5279. High severity for agentic workflow reliability.

10. **[#5173](https://github.com/QwenLM/qwen-code/issues/5173) – Model Provider Disambiguation Fails with Shared IDs** (3 💬)  
    Multiple providers exposing the same model ID (e.g. `qwen3.7-max`) via different endpoints cannot be persisted across sessions. Addressed by PRs #5241 and #5179.

---

## 4. Key PR Progress

*(Selected 10 of 50 recently active PRs)*

1. **[#5279](https://github.com/QwenLM/qwen-code/pull/5279) – fix(core): Always-On Tool-Call Circuit Breaker**  
   Re-scoped from #5242. Adds detection and termination of repetitive tool-call loops. Directly resolves #5234. **Critical stability improvement.**

2. **[#5181](https://github.com/QwenLM/qwen-code/pull/5181) – fix(core): Prevent OOM in Auto-Memory on /quit**  
   Fixes a heap-limit crash during managed memory extraction by optimizing `buildTranscriptMessages()`. High-priority memory fix.

3. **[#5241](https://github.com/QwenLM/qwen-code/pull/5241) / [#5179](https://github.com/QwenLM/qwen-code/pull/5179) – fix(model): Disambiguate Providers Sharing a Model ID**  
   Persists provider selection by `baseUrl`, solving #5173. Two approaches collaborated on in parallel, demonstrating rapid iteration.

4. **[#5258](https://github.com/QwenLM/qwen-code/pull/5258) – fix(cli): Stop After Cancelled Permissions**  
   Extends the "stop on cancel" logic from `ask_user_question` to all permission types, making cancellation a clean turn termination.

5. **[#5259](https://github.com/QwenLM/qwen-code/pull/5259) – fix(cli): Support Ctrl+P/N in Completions**  
   Directly addresses #2561. Vim users can now navigate completion menus without arrow keys. A long-standing ergonomic fix.

6. **[#5030](https://github.com/QwenLM/qwen-code/pull/5030) – feat(core,cli,sdk): Resume Interrupted Turn Cleanly**  
   Eliminates the synthetic `"continue"` message when resuming a session after crash or interruption. A major UX win for long-running sessions.

7. **[#5145](https://github.com/QwenLM/qwen-code/pull/5145) – feat(cli): Show Follow-Up Suggestion in Input Placeholder**  
   Uses the fast model to generate next-prompt suggestions. Keeps users in flow without breaking focus.

8. **[#5231](https://github.com/QwenLM/qwen-code/pull/5231) – feat(core,cli): Workflow Tool Token Budget**  
   Adds per-run output-token budgets for the Workflow tool, surfacing resource consumption in the UI. Important for cost-conscious users.

9. **[#5202](https://github.com/QwenLM/qwen-code/pull/5202) – feat(channel): Add QQ Bot Channel Adapter**  
   Community-driven integration. Adds `@qwen-code/channel-qqbot`, expanding the official channel lineup. Includes full WS gateway lifecycle.

10. **[#2915](https://github.com/QwenLM/qwen-code/pull/2915) – feat(cli): Add /clear --all for Full Session Reset**  
    Adds a `--all` flag to `/clear` to wipe IDE/editor context state alongside conversation history. Interactive confirmation prevents accidents.

---

## 5. Feature Request Trends

1. **Token & Usage Transparency (Highest Demand)**  
   Issues like #4479 and #3267 demand per-session and daily token consumption dashboards. Users need visibility to manage costs and understand usage patterns.

2. **Provider Abstraction & Customization**  
   Strong demand for arbitrary provider IDs (#5090), protocol-level SDK routing (`OPENAI | GEMINI | ANTHROPIC`), and frictionless local model onboarding (#3384, #4814). The community clearly wants a BYO-model architecture.

3. **Session Resilience & State Management**  
   Users want seamless crash recovery without synthetic messages (#5030), robust sub-agent orchestration (#5180), and CLI-based session listing/filtering (#4825).

4. **Vim / Keyboard-First UX**  
   Persistent requests for vim-compatible keybindings in completion menus (#2561), tmux scroll compatibility (#5159), and mouse-free navigation. The Ctrl+P/N fix (#5259) directly responds to this.

5. **Channel & Platform Expansion**  
   Beyond the QQ Bot adapter (#5202), there is clear community interest in broadening chat-platform integration. Expect more channel adapters to follow.

---

## 6. Developer Pain Points

1. **Authentication & Billing Friction**  
   The most vocal pain cluster. OAuth sessions not clearing on plan upgrade (#1855), free tier limits hit without warning (#3281), and paid plans stuck in "Out of Stock" (#3307) erode trust in the monetization pipeline.

2. **Platform Incompatibilities**  
   Node.js 26 breaks the `fetch` layer (#3914, #4274). tmux users lose trackpad scroll (#5159). Windows users hit React rendering crashes (#5199). Each platform gap fragments the user experience.

3. **Core Tooling Reliability**  
   Infinite tool-call loops (#5234) and OOM crashes during `/quit` (#5181) undermine confidence in autonomous agent workflows. The rapid response with circuit breakers (#5279) shows maintainers are prioritizing this.

4. **Configuration Complexity & Documentation Drift**  
   Setting up local LLMs (#3384) requires arcane workarounds. Global settings like `context.fileName` fail silently (#5267). Default docs don't match current CLI syntax (#3267). Configuration remains a steep barrier to entry.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**DeepSeek TUI (CodeWhale) Community Digest — 2026-06-18**

### 1. Today's Highlights
The v0.8.61 release cycle hit a sharp bump today with the community reporting critical regressions in agent governance and configuration hygiene. The maintainer team responded rapidly, merging targeted fixes for mode-switching integrity and agent self-questioning loops (#3283, #3290). On the strategic front, the Workrooms Phase 1 PR (#3277) landed, establishing the data model for v0.9’s threaded agent conversations. Meanwhile, the lingering effects of the `deepseek-tui` → `codewhale` rename continue to surface as filesystem and PATH friction.

### 2. Releases
*No new releases published in the last 24 hours.*

### 3. Hot Issues
1. **[#2870 – EPIC: Staged command-boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)**  
   *Author: aboimpinto*  
   The tracking epic for the #2791 refactor continues as the architectural backbone of v0.9, breaking the large change into mergeable PRs. Low community noise, high structural importance.

2. **[#3275 – Self-questioning and self-answering agent loop](https://github.com/Hmbown/CodeWhale/issues/3275)**  
   *Author: yekern*  
   A regression from #3061. Users report the AI unilaterally expands scope by generating, answering, and executing its own follow-up prompts without user confirmation. Eroding trust in the tool’s agency model.

3. **[#2917 – Binary `codewhale` not found after rename](https://github.com/Hmbown/CodeWhale/issues/2917)**  
   *Author: jazzi*  
   Users who auto-updated from `deepseek-tui` are left with a broken `PATH` and the old binary name. Highlights ongoing migration pain from the rebrand.

4. **[#3279 – Plan/Agent toggle permission chaos](https://github.com/Hmbown/CodeWhale/issues/3279)**  
   *Author: yekern*  
   Switching from Plan to Agent mode fails to restore `write_file`/`exec_shell` permissions. Even after recovery, the AI auto-executes the plan. A comprehensive UX bug report with wide consensus on severity.

5. **[#1481 – OpenCode Go/Zen provider support](https://github.com/Hmbown/CodeWhale/issues/1481)**  
   *Author: seanthefuturegorilla*  
   A long-running feature request for cheap DeepSeek-V4 access through OpenCode. Updated today—reflects community push for provider independence and cost reduction.

6. **[#3289 – v0.8.61 UI freezes on auto-spawn](https://github.com/Hmbown/CodeWhale/issues/3289)**  
   *Author: bruce6135*  
   UI becomes completely unresponsive when the model auto-triggers multiple agents. A critical stability blocker for power users.

7. **[#3281 – Moonshot/Kimi schema fix incomplete](https://github.com/Hmbown/CodeWhale/issues/3281)**  
   *Author: jghwwnq*  
   The v0.8.61 hotfix for #3265 only covered narrow schema cases. Schemas using `$ref`, `anyOf`, or `oneOf` at root still reject with 400 errors. Community identified the incomplete patch.

8. **[#1530 – Non-interactive session continuity](https://github.com/Hmbown/CodeWhale/issues/1530)**  
   *Author: xulongzhe*  
   Closed feature request for `exec --resume / --session-id`. Reflects growing demand for CI/CD and batch processing orchestration with persistent context.

9. **[#3292 – Snapshots ignore `enabled=false` config](https://github.com/Hmbown/CodeWhale/issues/3292)**  
   *Author: LmeSzinc*  
   Despite setting `snapshots.enabled = false`, the tool copies entire `.git` directories to the app folder, consuming gigabytes. Root cause identified as a missing config gate in `pre_tool_snapshot`.

10. **[#3282 – Config comments erased by TUI writes](https://github.com/Hmbown/CodeWhale/issues/3282)**  
    *Author: Artenx*  
    Any write to `config.toml` via the TUI strips user annotations and commented-out keys. A high-friction UX trap for advanced users.

### 4. Key PR Progress
1. **[#3290 – `scope_discipline` rules to prevent self-questioning](https://github.com/Hmbown/CodeWhale/pull/3290)**  
   *Author: yekern*  
   Adds constitution-level prompt rules to prevent the agent from unilaterally generating and answering its own questions. Direct surgical fix for #3275.

2. **[#3277 – Workrooms Phase 1](https://github.com/Hmbown/CodeWhale/pull/3277)**  
   *Author: idling11*  
   The foundation of v0.9. Implements the data model, endpoints, and tooling for thread-based, durable, addressable agent conversations (WorkroomLink URLs, RFC docs, CLI scaffolding).

3. **[#3283 – Plan/Agent mode toggle + auto-execution guard](https://github.com/Hmbown/CodeWhale/pull/3283)**  
   *Author: idling11*  
   Fixes two root causes of #3279: `approval_mode` not being restored on mode switch, and the AI auto-executing after recovery. Critical UX restore.

4. **[#3274 – Static musl Linux x64 builds](https://github.com/Hmbown/CodeWhale/pull/3274)**  
   *Author: wavezhang*  
   Switches the GitHub Actions release workflow to `x86_64-unknown-linux-musl`. Eliminates glibc dependency hell for Linux users.

5. **[#3280 – Heuristic auto-routing fallback](https://github.com/Hmbown/CodeWhale/pull/3280)**  
   *Author: hongchen1993*  
   Prevents hard failure when the flash router is unavailable. Fallback to heuristic model selection allows `--model auto` to work without DeepSeek API keys.

6. **[#3284 – Debounce thinking-stream re-renders](https://github.com/Hmbown/CodeWhale/pull/3284)**  
   *Author: LeoLin990405*  
   Fixes painful character-by-character UI lag in reasoning blocks by debouncing `bump_active_cell_revision()`.

7. **[#3291 – Preserve comments in config files](https://github.com/Hmbown/CodeWhale/pull/3291)**  
   *Author: zlh124*  
   Uses `toml_edit` for merge-based serialization so user annotations survive all CLI and TUI config writes. Direct fix for #3282.

8. **[#3293 – Respect `snapshots.enabled` for per-tool snapshots](https://github.com/Hmbown/CodeWhale/pull/3293)**  
   *Author: wuisabel-gif*  
   Adds the missing `snapshots.enabled` guard to `pre_tool_snapshot`. Solves the #3292 disk space leak.

9. **[#3294 – Write composer history under `.codewhale`](https://github.com/Hmbown/CodeWhale/pull/3294)**  
   *Author: wuisabel-gif*  
   Stops writing `composer_history.txt` to the legacy `~/.deepseek/` directory. Complements the rename cleanup and prevents runtime directory recreation.

10. **[#3285 – Persist session on stall/cancel recovery](https://github.com/Hmbown/CodeWhale/pull/3285)**  
    *Author: LeoLin990405*  
    Ensures `--continue` recovers full context after a stall or Esc cancel. Partial fix for #2739—prevents total loss of the in-progress turn.

### 5. Feature Request Trends
- **Inexpensive / Alternative Providers:** Strong consistent demand for cheap DeepSeek-V4 access (OpenCode Go/Zen, #1481). The community wants to avoid single-provider lock-in and reduce inference costs.
- **Durable Agent Conversations:** The Workrooms RFC (#3277) signals a clear push toward persistent, addressable, threaded interactions that survive restarts and enable organized multi-turn workflows.
- **Strict Mode Enforcement:** Users explicitly request that Plan/Agent/YOLO modes enforce hard guardrails (no write, no shell) without allowing the AI to negotiate or silently expand scope.
- **Scriptability & CI Integration:** The appetite for `--resume` and `--session-id` flags (#1530) shows growing adoption in automated, non-interactive pipelines.

### 6. Developer Pain Points
- **Post-Rename Migration Churn:** The `deepseek-tui` → `codewhale` rename created filesystem confusion (`~/.deepseek/` vs `~/.codewhale/`), broken `PATH` entries, and lingering legacy write paths (partially fixed in #3294).
- **v0.8.x Regression Fatigue:** Users feel thrust into a beta-tester role. Each release ships with high-impact regressions (self-questioning loops, mode toggle failures, Moonshot schema issues, UI freezes) that immediately disrupt productive use.
- **Agent Scope Creep & Trust Erosion:** The loudest pain point this cycle. The tool acting autonomously—ignoring mode restrictions or generating its own scope—breaks the fundamental contract of an assistant, severely damaging user trust.
- **Config Overwrite Fragility:** TUI and CLI tooling erasing user annotations from `config.toml` (#3282) is a persistent friction point for power users who manage complex configurations and need stable, annotated files.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*