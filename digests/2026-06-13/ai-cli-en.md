# AI CLI Tools Community Digest 2026-06-13

> Generated: 2026-06-13 03:25 UTC | Tools covered: 9

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

**Ecosystem Comparison Report: AI CLI Tools (2026-06-13)**

---

### 1. Ecosystem Overview

The AI CLI tools landscape is accelerating through a fundamental architectural transition from chat-based code assistants to full-fledged agentic runtimes. Trust and reliability remain the paramount friction points: platform-specific failures (particularly Windows), runaway agent costs from unbounded recursion, and opaque billing models are generating the strongest community backlash across virtually every tool. A robust divide is emerging between incumbent platforms managing enterprise-scale governance regressions (Claude Code, Copilot) and high-velocity challengers aggressively stripping away vendor lock-in to build universal agent hosts (CodeWhale, Pi, Qwen Code). The most significant strategic signal across the board is the community demand for declarative agent definitions, persistent session state, and programmatic cost observability — indicators of a user base rapidly maturing from conversational tinkerers to production workflow builders.

---

### 2. Activity Comparison

| Tool | Releases (24h) | Hot Issues (High Signal) | Significant PRs (24h) | Community Pulse |
|---|---|---|---|---|
| **Claude Code** | 3 (v2.1.175–177) | Fable-5 Outage, Unbounded Sub-Agents, CLI Freeze | 1 (Triaging bot fix) | Disruption crisis; enterprise governance vs. user autonomy |
| **OpenAI Codex** | 4 (Rust alphas .14–.17) | Win Sandbox Fail, Update Crashes, Context Full | 10 (PathUri, NativePathString, Wine Test) | High infra velocity; Windows is systemic blocker |
| **Gemini CLI** | 1 (v0.48.0 nightly) | Agent Hangs, False Success, Dashboard Quota | 10 (MCP fixes, tmux, AST foundation) | Quality-focused; agent reliability ceiling |
| **GitHub Copilot CLI** | 1 (v1.0.62-1) | Streaming Corruption, ARM64 Panic, MCP Loop | 0 (No core PRs merged) | High regressions; rendering crisis, ecosystem identity problems |
| **Kimi Code CLI** | 0 | Billing Opacity, File Read Loop, Web WS Error | 1 (Python 3.13 compat) | Lowest momentum; acute trust erosion |
| **OpenCode** | 0 | SQLite Crashes, Permission Bugs, Stuck Sessions | 10 (DB Doctor, OAuth Refresh, Security Audit) | Active but state complexity debt |
| **Pi** | 1 (v0.79.2) | Codex Freeze, Env Config Bugs, Duplicate Installs | 16 (AiGameAgent, Anthropic Vertex) | Extreme velocity; expanding far beyond coding |
| **Qwen Code** | 1 (v0.18.0) | Free Tier Policy Cut, Tool Call Loops, AV False Pos | 10 (DaemonTransport, OTel, Backpressure) | Strong architecture; controversial business risk |
| **CodeWhale (DeepSeek TUI)** | 1 (Rebrand v0.8.59) | TUI Freeze, Provider Lock-In, Fleet Scheduler | 10 (Anthropic Adapter, CI Flags, Hook Contract) | Explosive pace; full architectural identity shift |

---

### 3. Shared Feature Directions

**1. Declarative Agent Definitions (Claude Code, Qwen Code, Copilot CLI, CodeWhale)**
The community is converging on file-based agent configuration (`.claude/agents`, `.github/prompts`, YAML frontmatter). Users demand the ability to define agents, skills, and permissions as version-controlled config files rather than code.

**2. Unbounded Recursion & Cost Controls (Claude Code, Gemini CLI, OpenCode)**
Missing safety constraints for autonomous sub-agent spawning are causing exponential cost blowups. All major agentic tools require built-in recursion depth limits, spend caps, and termination signals to be production-viable.

**3. Intelligent Context Window Management (Codex, Copilot CLI, Claude Code, Qwen Code, Pi)**
Long sessions degrade into stalls, repetitive tool loops, or crashes. Smart compaction, token budgets, and graceful degradation are recognized as essential infrastructure across the board.

**4. Cross-Platform UX (Windows Gap) (Codex, Claude Code, Copilot CLI, Kimi Code, Qwen Code)**
Windows consistently suffers from sandbox failures, keyboard layout blockers (`@` key), AV false positives, and WebSocket initialization bugs. This is the single largest platform-specific pain point.

**5. Multi-Provider Abstraction / Model Hub (CodeWhale, Pi, Qwen Code, OpenCode)**
Users explicitly want tools that can route to any LLM backend. CodeWhale and Pi are aggressively removing hardcoded provider assumptions; Qwen Code added model identity disambiguation.

**6. MCP Infrastructure Maturation (Claude Code, Copilot CLI, OpenCode)**
The MCP ecosystem shows severe growing pains: infinite respawn loops, installation hangs on Windows, and OAuth token expiration are common failure modes.

**7. Observability & Billing Transparency (Kimi Code, Codex, Copilot CLI, OpenCode)**
Itemized token consumption, per-model cost breakdowns, and quota management are becoming table stakes. Kimi Code’s billing opacity incident is a warning to the entire ecosystem.

**8. Persistent Memory & Session State (Copilot CLI, OpenCode, Claude Code, Qwen Code)**
Cross-session goals, durable cron tasks, and reliable session migration are frequently requested, indicating production dependence on CLI continuity.

---

### 4. Differentiation Analysis

| Tool | Core Strategic Focus | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Agent orchestration reference; enterprise governance | Professional developers in large orgs | Proprietary models, managed settings, community-driven agent patterns |
| **OpenAI Codex** | Cross-platform execution infrastructure | Power users needing reliability across OSes | Rust rewrite, `PathUri` abstraction, sandbox isolation |
| **Gemini CLI** | Evaluation-driven quality & code intelligence | Developers who trust systematic testing | Heavy eval suites, AST-aware tooling, deterministic coverage |
| **GitHub Copilot CLI** | GitHub ecosystem bridge | Enterprise users tied to GitHub workflows | Tight coupling to GitHub API, IDE parity, server-side search |
| **Kimi Code CLI** | Niche generalist (low velocity) | Users of MoonshotAI models | Minimal engineering capacity; trust deficit |
| **OpenCode** | Permission & state management pioneer | Security-conscious developers | SQLite state engine, detailed permission rules, open-core licensing |
| **Pi** | Universal agentic runtime | Developers building custom workflows | Fastest provider expansion, game-dev niche, mesop architecture |
| **Qwen Code** | Daemon-first platform | Infrastructure engineers running remote agents | `qwen serve` as first-class server, OTel, backpressure, transport pluggability |
| **CodeWhale** | Hyper-velocity multi-provider disruptor | Developers seeking cutting-edge agent infrastructure | Constraints-driven feature flags, fleet scheduling, aggressive de-hardcoding |

- **Platform strategy gap:** Claude Code and Copilot CLI are tied to specific ecosystems (Anthropic, GitHub). CodeWhale, Pi, and Qwen Code are explicitly investing in provider fungibility.
- **The "agent runtime" vs. "code assistant" split:** CodeWhale, Pi, and Claude Code are evolving into durable agent hosts (fleet scheduling, server daemons, background tasks). Copilot CLI and Kimi CLI remain more narrowly focused on interactive code generation.
- **Permission architecture divergence:** OpenCode has the most rigorous permission system but suffers from logic errors. CodeWhale is moving to structured JSON hook contracts. Copilot introduced a "YOLO mode" indicator, embracing the opposite extreme.

---

### 5. Community Momentum & Maturity

**Explosive Velocity & Architectural Disruption**
- **CodeWhale:** Highest iteration cadence. The rebrand from DeepSeek TUI to a multi-provider agent platform signals a strategic ambition to be the universal agent host. Its fleet scheduling, hook contracts, and Web UI plans represent the most aggressive roadmap in the ecosystem.
- **Pi:** 16 PRs in 24 hours. Expanding from a coding CLI into game development tools and an open provider hub. High-risk, high-reward platform expansion.
- **OpenAI Codex:** Sustained alpha release cadence (4 releases/day). The Rust rewrite and `PathUri` infrastructure represent the most significant core re-architecture in the ecosystem, albeit with front-end regressions.

**Healthy Maturity & Enterprise Stability**
- **Claude Code:** Highest engagement metrics and deepest agentic workflow discussions. The Fable-5 outage and unbounded recursion issues show the growing pains of being the ecosystem leader in agent orchestration.
- **Gemini CLI:** Strongest investment in evaluative quality assurance. The agent hanging issue (#21409) is the single most impactful bug relative to its technical investment in AST/evals.

**Structural Technical Debt Carrying Community**
- **OpenCode:** Active contributions but heavily bogged down by SQLite schema fragility and permission logic errors. High interest in "DB doctor" tooling indicates accumulated state management complexity.
- **GitHub Copilot CLI:** Large installed base, but crippled by streaming output corruption (#3749, #3755) and MCP infrastructure regressions. The "identity crisis" between Copilot in IDE vs. CLI history (#53) remains unresolved.

**Concerning Signals (Stagnation / Trust Erosion)**
- **Kimi Code CLI:** Near-zero feature velocity. The billing transparency issue (#1994) represents the strongest trust erosion signal in the entire dataset. The community is actively questioning the fundamental fairness of the pricing model.

---

### 6. Trend Signals (Implications for Developers)

1. **The "Agent Runtime" Era Has Truly Arrived:** CLI tools are evolving into daemon-hosted agent operating systems. CodeWhale's Fleet, Qwen's `serve`, and Claude's delegation patterns are the leading indicators. **Takeaway:** Evaluate tools based on their durable execution, scheduling, and background processing capabilities, not just their chat UX.

2. **The Cost Transparency Reckoning:** Kimi Code's billing opacity is a warning to the entire ecosystem. As reasoning models (Kimi K2.6, DeepSeek, O-series) become popular, per-token costs of long CoT reasoning are shocking users. **Takeaway:** Demand itemized billing breakdowns and built-in spend caps before adopting a tool for agentic workflows.

3. **Declarative Agent Composition is the Productivity Gateway:** The consistent demand for file-based agent definitions (`.claude/agents`, `.github/prompts`, CodeWhale hooks) points toward a future where agent behavior is version-controlled and shareable. **Takeaway:** Tools without declarative agent configuration will struggle to scale into team/enterprise environments.

4. **The Great Safety/Stability Plateau:** OpenCode's permission dialog being broken, Claude Code's unbounded agent recursion, Qwen's tool execution after `SIGINT` — the whole feedback loop remains fragile. **Takeaway:** Do not trust autonomous agents with full filesystem or network access without rigorous guardrails. Expect this to be the hardest engineering problem for the next 12–18 months.

5. **The Universal Provider Bus Wins:** Projects actively investing in provider abstraction (CodeWhale, Pi, Qwen Code) are capturing the highest velocity and strongest community enthusiasm. **Takeaway:** Avoid tools that lock you into a single model provider. The ecosystem is moving toward fungible model routing as a core feature, not an afterthought.

6. **Windows Remains the Untapped Frontier:** The concentration of severe Windows bugs (sandbox failures, keyboard blockers, AV false positives) across Codex, Claude Code, Copilot, and Qwen Code leaves a massive market opportunity. **Takeaway:** If you primarily develop on macOS/Linux, you have a wider tool choice. If you are on Windows, rigorously test your specific environment before committing to any tool.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Period:** Up to 2026-06-13 | **Source:** [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following Pull Requests represent the most substantial new capabilities proposed by the community. All remain **Open** as of the data snapshot.

| Skill (PR) | Author | Functionality | Discussion Highlights | Status |
|---|---|---|---|---|
| **Document Typography** ([#514](https://github.com/anthropics/skills/pull/514)) | PGTBoos | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. | Recognized as solving a universal LLM formatting flaw. High relevancy for any document generation workflow. | **Open** |
| **ODT Skill** ([#486](https://github.com/anthropics/skills/pull/486)) | GitHubNewbie0 | Full lifecycle for OpenDocument Format files: creation, template filling, reading, and conversion to HTML. | Critical step toward LibreOffice and ISO-standard interoperability. | **Open** |
| **Meta Analyzers** ([#83](https://github.com/anthropics/skills/pull/83)) | eovidiu | Adds `skill-quality-analyzer` and `skill-security-analyzer` for auditing other skills across five quality dimensions. | First-wave ecosystem hygiene tools. Signals community focus on trust, standards, and self-regulation. | **Open** |
| **SAP-RPT-1-OSS Predictor** ([#181](https://github.com/anthropics/skills/pull/181)) | amitlals | Orchestrates SAP's open-source tabular foundation model for predictive analytics on business data. | Flagship enterprise skill combining open-source ML models with Claude's orchestration layer. | **Open** |
| **Testing-Patterns** ([#723](https://github.com/anthropics/skills/pull/723)) | 4444J99 | Comprehensive testing philosophy (Trophy model), unit testing, React Testing Library, and integration patterns. | Directly addresses the highest-demand developer gap in the official collection. | **Open** |
| **Agent-Creator** ([#1140](https://github.com/anthropics/skills/pull/1140)) | SyedaQurratAI | Meta-skill for constructing task-specific agent sets. Includes critical fixes for multi-tool evaluation and Windows support. | Demonstrates advanced meta-cognition patterns and agent orchestration techniques. | **Open** |
| **Color-Expert** ([#1302](https://github.com/anthropics/skills/pull/1302)) | meodai | Deep expertise in color naming systems (ISCC-NBS, Munsell, RAL), color spaces (OKLCH, CAM16), and accessibility. | Sets a benchmark for hyper-specialized, authoritative reference skills. | **Open** |
| **n8n Suite** ([#190](https://github.com/anthropics/skills/pull/190)) | Wolfe-Jam | Expert skills for building, debugging, and understanding n8n automation workflows and FAF context format. | Strong indicator of demand for low-code automation and project context management skills. | **Open** |

---

## 2. Community Demand Trends

Distilled from the most commented Issues:

- **Enterprise Distribution & Sharing** ([Issue #228](https://github.com/anthropics/skills/issues/228) — 14 comments, 7 👍): The dominant feature request is native org-wide skill sharing. The current manual download/upload workflow is the single largest barrier to enterprise adoption.

- **Skill-Creator Toolchain Reliability** ([Issue #556](https://github.com/anthropics/skills/issues/556) — 12 comments; [#1169](https://github.com/anthropics/skills/issues/1169); [#1061](https://github.com/anthropics/skills/issues/1061)): The `run_eval.py` 0% trigger rate bug is the community's primary technical blocker. Combined with Windows incompatibility, it prevents effective skill iteration and optimization.

- **Ecosystem Security & Trust** ([Issue #492](https://github.com/anthropics/skills/issues/492) — 7 comments): Community skills distributed under the `anthropic/` namespace impersonating official skills has sparked a critical conversation about trust boundaries and distribution verification.

- **Ecosystem Consistency** ([Issue #189](https://github.com/anthropics/skills/issues/189) — 6 comments; [#202](https://github.com/anthropics/skills/issues/202) — 8 comments): Duplicate skills across plugins and a `skill-creator` that reads as developer documentation rather than an executable instruction set point to quality gaps.

- **Governance & Safety** ([Issue #412](https://github.com/anthropics/skills/issues/412) — 4 comments): A formal proposal for an `agent-governance` skill covering policy enforcement, threat detection, and audit trails signals maturing interest in safe autonomous patterns.

- **Advanced Infrastructure** ([Issue #16](https://github.com/anthropics/skills/issues/16) — 4 comments; [#1220](https://github.com/anthropics/skills/issues/1220) — 2 comments): Requests to expose Skills as MCP servers and support multi-file reference bundles reflect a push toward composable, interoperable skill architecture.

---

## 3. High-Potential Pending Skills

These active, open PRs address critical ecosystem gaps or introduce high-demand functionality, making them strong candidates for imminent merging:

- **Fix run_eval.py 0% Recall Bug** ([#1298](https://github.com/anthropics/skills/pull/1298) — MartinCajiao): Directly resolves the primary infrastructure blocker preventing accurate skill evaluation. **Highest priority fix in the queue.**

- **Windows Compatibility Stack** ([#1099](https://github.com/anthropics/skills/pull/1099) — joshuawowk, [#1050](https://github.com/anthropics/skills/pull/1050) — gstreet-ops): Solves critical `PATHEXT`, encoding, and pipe-handling failures that block Windows contributors from the skill creation toolchain.

- **YAML Frontmatter Validation** ([#539](https://github.com/anthropics/skills/pull/539) — Lubrsy706, [#361](https://github.com/anthropics/skills/pull/361) — Mr-Neutr0n): Prevents silent misparsing of skill descriptions containing special YAML characters. High-impact, low-risk validation improvement.

- **DOCX Tracked Changes Fix** ([#541](https://github.com/anthropics/skills/pull/541) — Lubrsy706): Prevents document corruption from `w:id` collisions between tracked changes and existing bookmarks. Precision fix for a foundational document skill.

- **Testing-Patterns Skill** ([#723](https://github.com/anthropics/skills/pull/723) — 4444J99): High community demand, comprehensive in scope. Fills a major content gap for professional developers.

- **Document Typography Skill** ([#514](https://github.com/anthropics/skills/pull/514) — PGTBoos): Solves a universal UX issue in document generation. Broadly applicable across disciplines.

- **Agent-Creator Skill** ([#1140](https://github.com/anthropics/skills/pull/1140) — SyedaQurratAI): Combines a meta-skill with valuable cross-platform infrastructure fixes. Represents advanced ecosystem thinking.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is pivoting from **inventing novel skills** to **hardening the platform itself**—fixing the buggy `skill-creator` toolchain, enforcing trust boundaries in distribution, and unlocking enterprise sharing—as the essential foundation for scaling high-quality Skills across the ecosystem.

---

**Claude Code Community Digest — 2026-06-13**

**Today's Highlights**
A major `claude-fable-5` access disruption dominated the day, with dozens of Max plan users reporting sudden, mid-session model denials — sparking urgent bug reports and speculation about backend policy failures or resource constraints. On the development side, v2.1.175 and v2.1.176 shipped incremental improvements to managed model governance and session localization. Meanwhile, the community continued pushing hard on agent orchestration patterns, though new reports of unbounded recursive agent spawning highlight serious gaps in safety controls.

---

**Releases**

- **v2.1.177** — Latest hotfix bump (no specific changelog published).
- **v2.1.176** — Session titles are now generated in the language of your conversation (configurable via the `language` setting). New `footerLinksRegexes` setting for regex-matched link badges. Improved Bedrock credential handling.
- **v2.1.175** — Adds `enforceAvailableModels` managed setting: when enabled, the `availableModels` allowlist constrains the Default model, and user/project settings can no longer widen the managed restriction.

---

**Hot Issues**

1. **Widespread `claude-fable-5` Access Loss** (Aggregate of #68129, #68128, #68131, #68126, #68121, #68137)
   A wave of urgent reports from Max users hitting "Invalid or Inaccessible Model" errors mid-session. Community frustration is acute, with many stating the switch broke active workflows without warning. Issue #68128 accumulated 11 👍 in hours, suggesting a systemic backend or policy enforcement change affecting Fable availability.
   \[Link](https://github.com/anthropics/claude-code/issues/68128)

2. **#68110 — Unbounded Recursive Sub-Agent Token Burn**
   `general-purpose` sub-agents spawn child agents with no depth limit, creating exponential cost fan-out. Exposes a critical missing safety constraint in the Agent tool — calls for maximum recursion depth and spend caps.
   \[Link](https://github.com/anthropics/claude-code/issues/68110)

3. **#26224 — CLI Hanging/Freezing for 5–20 Minutes** (142 👍, 116 comments)
   The highest-voted open bug. A significant subset of users experience complete UI lockups during heavy prompting. Remains a top-tier stability concern.
   \[Link](https://github.com/anthropics/claude-code/issues/26224)

4. **#56913 — Autonomous Agent Viability: Tiered Opus + Sonnet Workers** (26 comments)
   A community design proposal for long-running orchestrator agents with persistent state, dedicated brain models, and cost-efficient workers. Represents a clear paradigm shift in how users want to deploy Claude Code.
   \[Link](https://github.com/anthropics/claude-code/issues/56913)

5. **#38183 — `SendMessage` Tool Missing, Agent Continuation Broken** (21 👍)
   The removal of a resume parameter broke multi-agent coordination. A clear regression that blocks complex agent workflows.
   \[Link](https://github.com/anthropics/claude-code/issues/38183)

6. **#67609 — Advisor Tool Unavailable on Fable-5 >100K Tokens**
   Server-side advisor tool returns `error_code: "unavailable"` once transcripts hit ~100K tokens. Strongly correlates with the broader Fable outage, pointing to backend scaling constraints.
   \[Link](https://github.com/anthropics/claude-code/issues/67609)

7. **#14321 — Enable Extended Thinking for Sub-Agents** (25 👍)
   Long-standing feature request for allowing deep reasoning in child agents. High community consensus on its necessity for sophisticated delegation.
   \[Link](https://github.com/anthropics/claude-code/issues/14321)

8. **#50911 — `CronCreate durable:true` Silently Dropped**
   The parameter is accepted but ignored — scheduled tasks are never persisted to `.claude/scheduled_tasks.json`. Kills automation on session end.
   \[Link](https://github.com/anthropics/claude-code/issues/50911)

9. **#47509 — Demand for Higher Consumption Tiers (>20x)** (37 👍)
   Power users on Team plans are hitting the ceiling of the Max 20x equivalent, requesting a new tier for heavy agentic usage. High upvote ratio signals strong market demand.
   \[Link](https://github.com/anthropics/claude-code/issues/47509)

10. **#67865 — MCP Installations Hang on Deflated Entries >16 KB (Windows)**
    Claude Desktop silently hangs when installing `.mcpb` bundles with larger files. Highlights ongoing cross-platform reliability gaps in the MCP ecosystem.
    \[Link](https://github.com/anthropics/claude-code/issues/67865)

---

**Key PR Progress**

Only one pull request met the activity threshold in the last 24 hours, but it addresses a significant contributor friction point:

- **PR #26360 — [claude-code-assisted] Fix issues being auto-closed despite human activity**
  Fixes #16497 by updating the triage bot to properly handle `stale`/`autoclose` labels. Previously, active human participation on stale issues wasn't recognized, causing legitimate discussions to be swept. Improves bot hygiene and reduces noise for maintainers.
  \[Link](https://github.com/anthropics/claude-code/pull/26360)

---

**Feature Request Trends**

- **Agentic Orchestration Architecture (#56913, #38183, #14321, #68110)**: The community is converging on a vision of Claude Code as a durable, self-managing orchestrator — not a pair-programming assistant. Requests include tiered model delegation, persistent agent state, extended reasoning for sub-agents, and recursion guards.
- **Enterprise Model Governance (#v2.1.175, #47509)**: Users want stricter managed model restrictions *and* higher consumption ceilings simultaneously, reflecting split demands between admin control and power-user throughput.
- **Cross-Platform UX (#68136, #68119)**: Reports of missing keyboard shortcuts (Ctrl-V on Windows) and rigid UI panes indicate growing demand for native-feeling polish outside macOS.

---

**Developer Pain Points**

- **Fable-5 Reliability Crisis**: The dominant story today. Sudden mid-session model access revocation — whether driven by rate limiting, content policy false positives, or backend configuration bugs — has severely undermined user trust in session continuity.
- **Runaway Agent Costs (#68110)**: The absence of built-in recursion limits or spend caps for the Agent tool is causing dangerous exponential token consumption. Users currently have no way to audit or constrain sub-agent fan-out.
- **Silent Feature Failures (#50911, #67609)**: Parameters accepted but silently ignored (`durable: true`) and server-side errors masked as generic "unavailable" messages erode confidence in both client and backend behavior.
- **Core Stability on Large Sessions (#26224)**: Multi-minute UI hangs remain the most-upvoted bug, frequently correlated with long transcripts or heavy MCP usage, indicating scaling issues in the TUI layer.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-13

## 1. Today's Highlights
Today's digest is dominated by a massive architectural push towards cross-platform stability, led by a concentrated stack of pull requests from `anp-oai` introducing `PathUri` and `NativePathString` to decouple app-server hosts from exec-server targets. The Rust-based Codex CLI saw four alpha releases (v0.140.0-alpha.14 through .17) in a single day, signaling intense iteration on the new runtime. Meanwhile, the community continues to report significant friction on Windows, where persistent sandbox initialization failures (`spawn setup refresh`) remain the single biggest blocker for developers using plugins and Computer Use.

---

## 2. Releases
The `rust-v0.140.0-alpha` line saw four rapid-fire releases in the past 24 hours (`.14`, `.15`, `.16`, `.17`). While no detailed changelogs accompanied these releases, their cadence indicates active stabilization and feature integration for the Rust-based Codex CLI and sandbox executor runtime.

---

## 3. Hot Issues

1. **[#12564 – Renaming task/thread titles](https://github.com/openai/codex/issues/12564)** *(CLOSED, 79 💬, 111 👍)*  
   The highest-engagement issue on the board. Users overwhelmingly support renaming threads for better history navigation. Its recent closure strongly suggests an implementation is imminent.

2. **[#9046 – Model context window full](https://github.com/openai/codex/issues/9046)** *(OPEN, 25 💬)*  
   A constant UX breaker for long sessions. The lack of smart automatic compaction forces users to start new threads constantly, disrupting workflow continuity across all models.

3. **[#24098 – Windows elevated sandbox fails (spawn setup refresh)](https://github.com/openai/codex/issues/24098)** *(CLOSED, 19 💬, 6 👍)*  
   Highlights a critical permissions split: sandbox works unelevated but fails with admin rights. Community quickly identified the workaround, but the root cause remains a systemic Windows pain point.

4. **[#25243 – macOS relaunch loop exhausts syspolicyd](https://github.com/openai/codex/issues/25243)** *(OPEN, 20 💬, 2 👍)*  
   A severe system-level instability where Codex crashes and relaunches, exhausting macOS file descriptors and blocking other application launches entirely.

5. **[#25220 – Windows bundled plugins unavailable (EFS)](https://github.com/openai/codex/issues/25220)** *(OPEN, 16 💬, 3 👍)*  
   Uncovers a deep OS-level incompatibility: Encrypting File System (EFS) on WindowsApps blocks Codex from copying plugin binaries, breaking Computer Use, Browser, and LaTeX plugins for Store-installed users.

6. **[#27175 – Windows Desktop crashes after update](https://github.com/openai/codex/issues/27175)** *(OPEN, 15 💬, 3 👍)*  
   Release `26.602.71036` introduces a severe regression where the app becomes inaccessible even on empty sessions. A high-priority stability incident for Windows Pro subscribers.

7. **[#27817 – False positive cybersecurity flag on finance work](https://github.com/openai/codex/issues/27817)** *(OPEN, 12 💬)*  
   Illustrates friction from safety guardrails interrupting a legitimate tax filing workflow. Calls for better contextual awareness in the Guardian moderation system.

8. **[#22335 – CLI remote compaction repeatedly fails](https://github.com/openai/codex/issues/22335)** *(OPEN, 6 💬, 8 👍)*  
   Premium users on GPT-5.5 with high reasoning report workflow-breaking compaction loops. The highly favorable reaction ratio suggests a widely shared but under-reported power-user frustration.

9. **[#27694 – macOS Dock tile recursion crash](https://github.com/openai/codex/issues/27694)** *(OPEN, 4 💬, 3 👍)*  
   Hard crash caused by `CodexDockTilePlugin setDockTile:` recursion. An ugly integration bug between the app and the macOS Dock process.

10. **[#27998 – Lost all chat history / Won't save settings](https://github.com/openai/codex/issues/27998)** *(OPEN, 2 💬)*  
    A critical data loss report following the `26.609.41114` update. Users retain projects but lose all thread history and settings—a major trust violation.

---

## 4. Key PR Progress

1. **[#27819 – path-uri: render native paths across platforms](https://github.com/openai/codex/pull/27819)**  
   Core infrastructure moving internal paths to `PathUri`. Enables cross-OS orchestration without exposing URI encoding to public API consumers.

2. **[#28018 – app-server: use NativePathString for command cwd](https://github.com/openai/codex/pull/28018)**  
   Converts command execution `cwd` to native path strings at the app-server boundary. Key dependency for the unified execution stack.

3. **[#28014 – unified-exec: launch remote commands without host sandbox](https://github.com/openai/codex/pull/28014)**  
   Allows launching commands directly on a remote exec-server, bypassing host sandbox construction. Unlocks true cross-platform command dispatch.

4. **[#27937 – Add hermetic Wine exec-server test](https://github.com/openai/codex/pull/27937)** *(CLOSED)*  
   Introduces a Wine-based integration test to validate cross-OS exec-server orchestration, proving the `PathUri` architecture works in CI.

5. **[#27369 – Add dormant plugin script lifecycle state](https://github.com/openai/codex/pull/27369)**  
   Prepares the plugin system for richer lifecycle management (FOO-574). Merged behind a default-off flag to safely iterate on shell/runtime event wiring.

6. **[#27886 – Update policy wording](https://github.com/openai/codex/pull/27886)**  
   Refines Guardian decision rules for sensitive-data egress and personal-data sharing. A direct response to the community's false-positive frustrations.

7. **[#27971 – Coordinate cloud config bundle caching across processes](https://github.com/openai/codex/pull/27971)**  
   Fixes redundant cloud config fetches when CLI and App Server share a `CODEX_HOME`. Reduces startup time and API load.

8. **[#28002 – Send turn state through compact requests](https://github.com/openai/codex/pull/28002)**  
   Fixes compaction continuity by passing `ModelClientSession` state through inline compact requests. Directly addresses the "context window full" issues in #9046 and #22335.

9. **[#27459 – Gate plugin MCP servers by auth route](https://github.com/openai/codex/pull/27459)** *(CLOSED)*  
   Makes `PluginsManager` auth-aware to prevent MCP server conflicts with App declarations. Hardens the plugin security model.

10. **[#28008 – Add external agent import result accounting](https://github.com/openai/codex/pull/28008)**  
    Improves the External Agent import API with `importId` and detailed result grouping, making enterprise migrations more observable and reliable.

---

## 5. Feature Request Trends

- **Cross-Platform CWD & Path Management:** Users consistently ask for seamless project context when switching between OSes or using WSL (#22672, #23189). The massive `PathUri` PR stack (see Section 4) is an explicit architectural response to this demand.
- **Better Thread Lifecycle Management:** The high engagement on #12564 (renaming threads) combined with complaints about lost history (#27998) signals strong demand for richer, persistent thread organization.
- **Intelligent Context Window Management:** The community is clamoring for automatic, seamless context pruning to replace the disruptive "start a new thread" pattern (#9046, #22335).
- **Reliable Plugin Ecosystem:** Users want bundled plugins (Browser, Computer Use, LaTeX) to "just work" across platforms without manual sandbox hacking or OS-specific configuration (#25220, #24198).

---

## 6. Developer Pain Points

- **Windows Sandbox (`spawn setup refresh`):** This single error code appears in nearly half of the top issues. It completely bricks the Node REPL, Browser plugin, Computer Use, and Chrome plugin on Windows. This is the **#1 systemic blocker** for the Windows developer community.
- **Update-Induced Instability:** Multiple recent updates have caused crashes, config resets, and data loss (#27175, #27979, #27998). This breeds anxiety around the update process and erodes user trust in release quality.
- **CLI Binary Discovery:** Users frequently struggle with `CODEX_CLI_PATH` and locating the binary, especially in complex Windows/WSL environments with non-standard drives (#22423, #16408, #22672).
- **Safety System Overreach:** False-positive cybersecurity flags interrupt normal DevOps and financial workflows (#27817, #28015), creating friction that breaks developer flow state.
- **macOS System Integration:** Hard crashes related to the Dock tile (`setDockTile:` recursion) and relaunch loops exhausting system resources (#25243, #27694) show macOS desktop integration needs significant hardening.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-13

## 1. Today's Highlights
The `v0.48.0-nightly.20260613` release lands with critical fixes to MCP tool discovery and Vertex AI model mapping. The community remains intensely focused on agent reliability—**Generalist agent hangs** (#21409) and **sub-agent false success reporting** (#22323) are the most active and highly-voted bugs. There is a strong surge in interest for **AST-aware tooling** to improve code intelligence precision and reduce token waste (#22745), while the **memory and auth subsystems** continue to generate steady security and stability patches.

## 2. Releases
**v0.48.0-nightly.20260613.g9e5599c32**
- `fix(core): implement atomic update in MCP tool discovery` ([PR #27619](https://github.com/google-gemini/gemini-cli/pull/27619))
- `fix(core): Vertex AI model mapping fix` ([PR #27749](https://github.com/google-gemini/gemini-cli/pull/27749))
- `Add documentation and migration command`

---

## 3. Hot Issues

1. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) Robust Component Level Evaluations (P1, 7 comments)** — An epic tracking the expansion of behavioral eval tests (currently 76) across 6 models. Critical for long-term agent quality assurance and regression detection.

2. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) AST-aware File Reads, Search, and Mapping (P2, 1👍, 7 comments)** — A heavily favored investigation into replacing line-based reads with AST-aware tools (AST grep, glyph) to reduce turn count and token noise during code navigation.

3. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) Generalist Agent Hangs (P1, 8👍, 7 comments)** — The highest-voted open bug. The generalist agent hangs indefinitely on simple tasks like folder creation, forcing users to disable sub-agent delegation entirely.

4. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) Subagent False Success on MAX_TURNS (P1, 2👍, 6 comments)** — A dangerous reporting bug: sub-agents hitting the turn limit erroneously report `status: "success"` + `Termination Reason: "GOAL"`, undermining trust in execution signals.

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) Agents Don't Use Skills/Sub-Agents Proactively (P2, 6 comments)** — Even with well-defined custom skills, the CLI rarely delegates autonomously, negating much of the agent extensibility value proposition.

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) Deterministic Redaction and Auto Memory Logging (P2, 5 comments)** — Security concern: Auto Memory processes transcripts containing secrets before redaction is applied, and logs sensitive skill content.

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) Stop Auto Memory Retrying Low-Signal Sessions (P2, 5 comments)** — Efficiency bug: the extraction agent ignores low-signal sessions instead of marking them processed, causing infinite re-processing loops.

8. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) Shell Command Stuck on "Waiting Input" (P1, 3👍, 4 comments)** — A common P1 blocking issue: shell commands complete but the CLI UI remains stuck in an "Awaiting user input" state.

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) Browser Subagent Fails in Wayland (P1, 1👍, 4 comments)** — Critical platform-specific bug breaking the browser subagent entirely under the Wayland display protocol.

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) Agent Should Stop/Discourage Destructive Behavior (P2, 1👍, 2 comments)** — Safety concern: the agent should autonomously prefer safer alternatives to destructive commands (`git reset`, `--force`).

---

## 4. Key PR Progress

1. **[#27572](https://github.com/google-gemini/gemini-cli/pull/27572) fix(cli): handle tmux false positive background detection** — Fixes a regression where Gemini misdetects terminal background color inside tmux over mosh, preventing unwanted theme switching.

2. **[#27552](https://github.com/google-gemini/gemini-cli/pull/27552) fix(core): insert content literally into LLM prompts to avoid $ substitution** — Eliminates silent prompt corruption where `$` characters in user content were interpreted as replacement patterns by `String.prototype.replace`.

3. **[#27568](https://github.com/google-gemini/gemini-cli/pull/27568) fix(core): fall back when ripgrep execution fails** — Adds resilience to the codebase investigator by falling back to the legacy `GrepTool` when `rg` is missing or exits unexpectedly.

4. **[#27555](https://github.com/google-gemini/gemini-cli/pull/27555) fix(cli): stop merging shell history commands that end in a backslash** — Corrects a history-corrupting bug where Windows paths or escape continuations were merged with the subsequent command entry.

5. **[#27694](https://github.com/google-gemini/gemini-cli/pull/27694) fix: dedupe home agent directories** — Prevents duplicate agent loading when `--home` resolves to the same path as `~/.gemini/agents`, fixing a long-standing agent registration issue.

6. **[#27873](https://github.com/google-gemini/gemini-cli/pull/27873) fix(core): improve SKILL.md frontmatter parsing robustness** — Hardens agent definition parsing against UTF-8 BOM, trailing whitespace, and non-string YAML values, reducing silent "invalid agent" failures.

7. **[#27872](https://github.com/google-gemini/gemini-cli/pull/27872) fix(core): strip line/range suffix from at-command paths to avoid CLI hang** — Prevents hangs by safely stripping line/range suffixes (e.g., `file.ts:12`) from at-command paths before filesystem operations.

8. **[#27870](https://github.com/google-gemini/gemini-cli/pull/27870) fix(core): cap pending tool responses** — Fixes a crash caused by excessively large tool results by capping the pending `functionResponse` payload sent to the model.

9. **[#27867](https://github.com/google-gemini/gemini-cli/pull/27867) fix(a2a-server): prevent crash when tasks metadata endpoint returns 501** — Improves A2A server stability by handling HTTP 501 responses from the tasks metadata endpoint gracefully.

10. **[#27854](https://github.com/google-gemini/gemini-cli/pull/27854) Fix/pending tools and trust overrides** — Stabilizes agent execution by preventing premature state progression during user tool approvals and eliminating race conditions in concurrent file writes.

---

## 5. Feature Request Trends

- **Next-Gen Code Intelligence:** A strong community and internal push to integrate **AST-aware tooling** (#22745, #22746, #22747). The goal is to replace basic text matching and line-based reads with syntax-aware code search, precise method extraction, and smarter codebase mapping, significantly reducing token waste and improving turn efficiency.

- **Autonomous Agent Orchestration:** Users consistently request a CLI that **self-directs to Skills and Sub-agents** without explicit instruction (#21968). The ideal workflow involves automatic delegation to a Gradle skill or the Browser Agent based on task context.

- **Intelligent Tool & Resource Management:** As the tool ecosystem grows, demand is rising for **smart tool scope limiting** (#24246) and **workspace cleanliness** (#23571). The agent should filter irrelevant tools and avoid generating messy temp scripts across the user's filesystem.

- **Background & Remote Operations:** The *Remote Agents* epic (#20303) reflects sustained demand for long-running background tasks, task-level authentication, and first-party agent support beyond purely interactive sessions.

---

## 6. Developer Pain Points

- **Chronic Agent Hangs & False Completions:** The most critical pain points are **agent hanging** (#21409, #25166) and **false success reporting** (#22323). These break the core loop and erode trust, forcing users to constantly supervise or apply awkward workarounds.

- **Configuration Inconsistency & Environment Fragility:** Settings like `maxTurns` are **silently ignored** (#22267), agent permissions are overridden on update (#22093), and **authentication flows break** with custom endpoints (#27553, #27558). Non-standard terminals (Wayland, tmux, Termux) face repeated breakage (#21983).

- **Memory System Overhead & Security Risk:** Auto Memory creates unwanted overhead by **retrying low-signal sessions** (#26522), fails to quarantine invalid patches (#26523), and potentially **exposes secrets** in logs and model contexts before redaction (#26525).

- **Fragile Shell & Prompt Integration:** The shell/prompt barrier remains a source of subtle corruption: **dollar sign corruption** (#27552), **newline escaping** (#22466), **backslash history merging** (#27555), and **vim command parsing** bugs (#27554) create hard-to-debug failures.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest | 2026-06-13

## Today's Highlights

A new release (`v1.0.62-1`) landed today featuring session-scoped extensions and a "YOLO" (allow all) mode indicator. However, the terminal rendering subsystem is under heavy fire with multiple reports of completely corrupted streaming output (#3749, #3755, #3780), making the CLI nearly unusable for affected users. A critical MCP server infinite respawn loop (#3782) and a Tokio reactor panic on Linux ARM64 (#3784) are already generating traction as hot regressions from recent updates.

## Releases

**`v1.0.62-1`** was released in the last 24 hours.

**Added:**
- **YOLO Mode Indicator:** Clear footer indicator when in "allow all" mode, with proper state exposed to `statusLine.command`.
- **Server-Side Search:** Press `/` on the Issues or Pull Requests tab to filter GitHub results server-side.
- **Session-Scoped Extensions:** Extensions and canvases can now be scoped to individual CLI sessions for better context isolation.
- **SDK Memory Configuration:** SDK clients can now configure session memory thresholds programmatically.

## Hot Issues

1.  **[#53: Bring back the GitHub Copilot in the CLI commands…](https://github.com/github/copilot-cli/issues/53)** *(OPEN, 75 👍, 37 comments)*
    The most-reacted issue remains open with no official word after six months. Community forks like `shell-ai` are gaining traction as replacements. This is the defining community-driven tension point for the project.

2.  **[#618: Custom slash commands from .github/prompts](https://github.com/github/copilot-cli/issues/618)** *(CLOSED, 99 👍)*
    The highest-voted feature request has been closed. The demand for parity with Claude Code's `.github/prompts` paradigm was overwhelming, suggesting internal work is likely underway.

3.  **[#3749: Terminal streaming renderer corrupts output](https://github.com/github/copilot-cli/issues/3749)** *(OPEN, 7 👍)*
    A severe UX bug. Characters are doubled, truncated, or repeated mid-stream during both the thinking phase and final responses. Community frustration is escalating as this is a core rendering path.

4.  **[#3755: Reasoning/thinking display garbles streamed text](https://github.com/github/copilot-cli/issues/3755)** *(OPEN)*
    Closely related to #3749, this specifically targets the live reasoning display (`showReasoning: true`), where text fragments like "from" render as "fromply from" due to overlapping chunk boundaries.

5.  **[#2627: Configurable system prompt](https://github.com/github/copilot-cli/issues/2627)** *(OPEN, 17 👍)*
    Users want to reclaim the ~20,500 tokens consumed by the default system prompt at session start. High demand for token efficiency and power-user customization to free up context window space.

6.  **[#3784: Copilot CLI v1.0.62-1 aborts on Linux ARM64](https://github.com/github/copilot-cli/issues/3784)** *(OPEN)*
    A fresh critical platform regression. The latest release immediately panics with a Tokio reactor error upon submitting the first prompt on ARM64 Linux.

7.  **[#3782: MCP stdio server unbounded tight loop](https://github.com/github/copilot-cli/issues/3782)** *(OPEN)*
    Since `1.0.61`, stdio MCP servers are spawned hundreds of times in a tight loop with no backoff or max-retry logic. Blocks all MCP-dependent workflows entirely.

8.  **[#1999: Cannot enter @ on German keyboard](https://github.com/github/copilot-cli/issues/1999)** *(OPEN)*
    A fundamental input blocker for international users. `AltGr + Q` produces no input, rendering the CLI unusable on German-layout keyboards.

9.  **[#2306: Enterprise authorization error](https://github.com/github/copilot-cli/issues/2306)** *(OPEN)*
    Intermittent "You are not authorized" errors strike enterprise users 2–3 times a week despite working setups. Suggests an opaque server-side policy caching issue.

10. **[#1614: Session hangs ~8 minutes after compaction](https://github.com/github/copilot-cli/issues/1614)** *(CLOSED)*
    A classic performance landmine: compaction replaces the conversation context causing an unresponsive "Thinking…" state for minutes. While closed, the underlying class of memory management issues persists (see #3621).

## Key PR Progress

**[#3771: Initial project setup](https://github.com/github/copilot-cli/pull/3771)** *(OPEN)*  
This is the only PR updated in the last 24 hours. It appears to be a personal fork/test branch and does not represent a core contribution. No feature or bugfix PRs were merged in this window.

## Feature Request Trends

The community is laser-focused on **customizability** and **competitive parity**:

- **Prompt Customization:** `.github/prompts` support (#618) and system prompt configurability (#2627) top the list. Users want the CLI to behave like an extensible agent, not a fixed black box.
- **Persistent Memory:** Cross-session goals via `.copilot/goals.md` (#3364) and finer control over context memory are rising themes, indicating users are treating the CLI as a long-running development partner.
- **MCP Lifecycle Management:** Requests for enable/disable toggles (#3564) and auto-updates for plugins (#3331) suggest MCP adoption is growing, but users want surgical control over what runs.
- **Observability:** A detailed request for OpenTelemetry cost/premium-request metrics (#3778) signals that teams want to track usage spend programmatically, mirroring Claude Code's cost telemetry.

## Developer Pain Points

- **Streaming Output Corruption (High Priority):** Multiple independent reports (#3749, #3755, #3769, #3780, #982) describe fundamentally broken terminal rendering. This is the single most disruptive issue cluster right now.
- **Non-English Keyboard Support:** The inability to type `@` (German #1999) or Polish characters (#2920) is a hard accessibility blocker for an entire class of international developers.
- **MCP Reliability Regressions:** The unbounded MCP server respawn loop (#3782) and Windows fetch failures (#3455) are eroding trust in the new MCP infrastructure.
- **Enterprise Policy Opaqueness:** Intermittent authorization errors (#2306) and blanket MCP server blocks (#3756) create a frustrating "works here, breaks there" experience without clear diagnostics.
- **Model Fragmentation:** Users experience model availability mismatches between VS Code and the CLI (#2661), leading to confusion about plan entitlements and supported features.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-13**

**Note from the Editor:** Activity in the last 24 hours focused on a small number of deeply discussed issues, allowing us to closely examine the most critical pain points currently facing the community.

---

### 1. Today’s Highlights
Developer attention remains heavily concentrated on reliability and billing transparency. The most community-engaged topic is a heated debate over kimiCode usage calculation (#1994), where users question whether token-based billing fairly accounts for long chain-of-thought reasoning models. A fresh critical blocker on the Kimi Web "Work" tab (#2435) is drawing concern for Windows users, while the post's only active PR focuses on preventing a Python 3.13 import cascade failure (#1597).

---

### 2. Releases
No new versions of the Kimi CLI were published in the last 24 hours.

---

### 3. Hot Issues
*(All 3 issues updated in the last 24h)*

1. **[Bug] Kimi CLI stuck in reading one file again and again and stuck in a loop (#640)**
   - **Why it matters:** A long-standing bug that resurfaced today. On custom endpoints (`mimo-v2-flash`, Anthropic protocol), the CLI enters an infinite loop repeatedly reading the same file. This completely halts any development pipeline for users running third-party models.
   - **Community reaction:** 9 comments. Low upvotes but high engagement from affected users.
   - [Link](MoonshotAI/kimi-cli Issue #640)

2. **kimiCode用量计算有问题 (Usage calculation problem) (#1994)**
   - **Why it matters:** The strongest community signal in the dataset (7 👍). A user reports burning 2 hours of quota in just 2 tasks using the K2.6 model, disputing whether billing should count tokens or API requests. The long CoT of reasoning models is cited as the core friction.
   - **Community reaction:** Heated debate. The community clearly wants stricter transparency on "per-request" vs. "per-token" consumption.
   - [Link](MoonshotAI/kimi-cli Issue #1994)

3. **[Bug] Kimi Work tab: "Daimon control WS not ready" + infinite reload at 99% (#2435)**
   - **Why it matters:** Fresh blocker report (filed June 6). On Windows 10/11, the Web-based Work tab fails to initialize due to a WebSocket daemon error, entering an infinite reload loop at 99%. The reporter states the feature is "completely unusable."
   - **Community reaction:** Low upvotes but very high severity for affected web UI users.
   - [Link](MoonshotAI/kimi-cli Issue #2435)

---

### 4. Key PR Progress
*(Single pull request updated in the last 24h)*

1. **fix: guard trafilatura import to prevent cascading tool load failure on Python 3.13 (#1597)**
   - **Author:** he-yufeng
   - **What it does:** Wraps the `trafilatura` import in a try/except block. On Python 3.13, `charset-normalizer` ships mypyc-compiled `.so` binaries that are incompatible with the interpreter, causing the entire `web.fetch` module to crash unconditionally.
   - **Why it matters:** Essential forward-compatibility patch. Without it, users upgrading to Python 3.13 lose all web-fetching tools in one cascading failure.
   - [Link](MoonshotAI/kimi-cli PR #1597)

---

### 5. Feature Request Trends
While explicit feature requests are sparse in today’s data, the nature of active bugs reveals three clear community desires:

- **Transparent Usage Metering:** Developers want itemized breakdowns of how many tokens specific models consume per task, and a clear distinction between "API call count" and "token consumption" for billing.
- **Robust Custom Endpoint Safeguards:** The infinite loop from #640 strongly implies a need for timeouts, max-token thresholds, or complexity limits when using non-standard model providers.
- **Resilient WebSocket Backend:** The WebUI Work tab failure signals a demand for a more resilient daemon connection layer that can auto-recover or provide clear diagnostic output instead of infinite reloading.

---

### 6. Developer Pain Points

- **Billing Opacity (Primary Pain Point):** Issue #1994 captures the loudest frustration in the dataset. Developers feel penalized by models with long reasoning chains (like K2.6) and are confused by how their quota translates between "tokens" and "requests." Trust in the credit system is actively eroding.
- **Unrecoverable Stalls:** Both the file-reading loop (#640) and the WebUI reload loop (#2435) represent a class of bugs that destroy developer trust—tools entering unrecoverable infinite states without meaningful error recovery or user control.
- **Ecosystem Compatibility Friction:** Even the single PR (#1597) highlights the ongoing burden on developers to patch the toolchain just to keep it running on upgraded Python runtimes (3.13). Unhandled import crashes create steep onboarding friction.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the **OpenCode Community Digest** for **2026-06-13**.

---

## Today's Highlights
The project saw no official releases, but the community is heavily invested in database reliability and core UX stability. A wave of PRs targeting SQLite health (`db doctor`) and a critical session state reconciliation bug (#32127 / #32128) promise to resolve persistent “stuck session” and startup issues. Meanwhile, the permission system continues to attract high-engagement bug reports (#27436, #24335), indicating deep confusion around rule evaluation logic.

## Releases
No new version was published in the last 24 hours.

## Hot Issues

1.  **[#31996 – Invalid JSON Schema (Regex Lookaround) Blocks All Providers](https://github.com/anomalyco/opencode/issues/31996)**
    *Why it matters:* Requests to OpenAI-compatible providers fail before reaching the model due to an unsupported regex pattern in the generated JSON schema. A critical networking blocker (👍5, 11 comments).

2.  **[#27436 – Permission Dialog Interaction Broken](https://github.com/anomalyco/opencode/issues/27436)**
    *Why it matters:* Users report being unable to click “Allow Once” or submit rejection feedback, completely stalling agentic sessions. Highly engaged thread (👍11, 16 comments).

3.  **[#31204 – `NOT NULL constraint failed` on Agent Switch](https://github.com/anomalyco/opencode/issues/31204)**
    *Why it matters:* The latest SQLite projection table migration crashes any session that triggers an agent switch, corrupting the conversation state.

4.  **[#16885 – Migration Reruns on Non-`latest` Channels](https://github.com/anomalyco/opencode/issues/16885)**
    *Why it matters:* The JSON-to-SQLite migration fires on every startup for local/dev builds, degrading performance and risking state duplication (👍8, 8 comments).

5.  **[#14187 – Add Markdown Preview Toggle in Sidebar](https://github.com/anomalyco/opencode/issues/14187)**
    *Why it matters:* The most upvoted feature request in this batch (👍22). Developers want a rendered preview for `.md`/`.mdx` files instead of raw syntax highlighting.

6.  **[#24335 – Permission Wildcard Overwriting Lower Rules](https://github.com/anomalyco/opencode/issues/24335)**
    *Why it matters:* Violates the documented “last matching rule wins” logic, making security configurations unpredictable (👍4, 7 comments).

7.  **[#27302 – Warp Mode Captures All Input in Interactive Q&A](https://github.com/anomalyco/opencode/issues/27302)**
    *Why it matters:* Using `/warp` with the Q&A tool captures mouse clicks and keyboard input, forcing users to kill the terminal (👍6).

8.  **[#16610 – OpenCode Hangs at Startup on Low inotify Limits](https://github.com/anomalyco/opencode/issues/16610)**
    *Why it matters:* A hard crash for Linux users with restricted `fs.inotify.max_user_instances` with no graceful fallback (👍7).

9.  **[#32127 – Stale “Busy” in Session Status Never Clears](https://github.com/anomalyco/opencode/issues/32127)**
    *Why it matters:* Sessions permanently show a “working” indicator. Root caused to a `setStore` vs `reconcile` bug in `bootstrap`. Fixed in #32128.

10. **[#32120 – Subscription 429s Burn User Quota on Retry](https://github.com/anomalyco/opencode/issues/32120)**
    *Why it matters:* Treating hard quota exhaustion as a retryable rate-limit actively makes the user’s financial situation worse. Bad failure mode.

## Key PR Progress

1.  **[#32128 – Fix Stale Session Status in Bootstrap](https://github.com/anomalyco/opencode/pull/32128)**
    Addresses the root cause of sessions being stuck in “working”. Changes `bootstrap` to use `reconcile` instead of bare `setStore` for `session_status`.

2.  **[#32093 – Add `db doctor` and `db repair` Commands](https://github.com/anomalyco/opencode/pull/32093)**
    A highly anticipated native CLI tooling for diagnosing and fixing common SQLite database inconsistencies (related to #31204, #29908).

3.  **[#32115 – Add TrustedRouter Provider](https://github.com/anomalyco/opencode/pull/32115)**
    Integrates the TrustedRouter API as an OpenAI-compatible provider, expanding the supported model ecosystem.

4.  **[#32135 – Refresh Expired OAuth Tokens in MCP](https://github.com/anomalyco/opencode/pull/32135)**
    A critical reliability fix for the Model Context Protocol, preventing silent disconnects during long-running sessions.

5.  **[#32134 – Security Audit Report (17 Findings)](https://github.com/anomalyco/opencode/pull/32134)**
    A comprehensive review covering the entire TypeScript codebase. Essential for enterprise adoption and hardening.

6.  **[#31993 – Restore Desktop “Open In” Menu](https://github.com/anomalyco/opencode/pull/31993)**
    Fixes a UI regression where the session header’s “Open in” control disappeared in the new desktop layout.

7.  **[#32125 – Fix Scheme-less Base URLs for `opencode attach`](https://github.com/anomalyco/opencode/pull/32125)**
    Fixes remote connections when using commands like `opencode attach localhost:4096` where query params were dropped.

8.  **[#32138 – Sort Numbered Placeholder Hints Correctly](https://github.com/anomalyco/opencode/pull/32138)**
    Fixes `Array.sort()` misordering `$10` before `$2`. A small but potent quality-of-life fix for command autocompletion.

9.  **[#31529 – Suppress Spinner Garbage in Non-TTY Environments](https://github.com/anomalyco/opencode/pull/31529)**
    Prevents character frame artifacts (◓, ◑) from polluting CI/CD and PowerShell logs.

10. **[#30837 – Optimize Snapshots with Deduplication](https://github.com/anomalyco/opencode/pull/30837)**
    Introduces `alternates` to eliminate per-blob duplication, mitigating snapshot directory bloat and improving performance.

## Feature Request Trends
- **Rich IDE-like UX:** The highest-voted requests tilt toward traditional editor features: a rendered markdown preview (#14187, 👍22), dynamic window titles showing the active session/project (#31423), and proper TUI scrollbars (#9929).
- **Data Observability:** Developers want full insight into agent costs and local state. This includes request for a pricing markup column on the Go pricing table (#32116), live token throughput (#30164), and native DB health tooling (#32097).
- **Monetization & Plugins:** The community is exploring commercial integration via an Ads/kickback platform (#32106) and community plugin discovery through “rotator” projects (#32112).

## Developer Pain Points
- **SQLite State Fragility:** The DB schema is a major churn point. Users face migration reruns on every start (#16885), `NOT NULL` crashes on agent switches (#31204), and sessions stuck in “working” (#32127).
- **Permission System Confusion:** Despite documentation, the permission system behaves unpredictably. Modal dialogs that block input (#27436), wildcards that ignore evaluation order (#24335), and interactions between `edit` and `external_directory` rules (#18441) erode developer trust in agentic file access.
- **Silent Failures:** Several bugs allow catastrophic failure without user feedback: subagent output silently truncated (#32131), `apply_patch` stalling (#32121), and quota-burning retries (#32120).
- **Windows Updates & Installation:** Auto-updates losing custom install directories (#26818) and the lack of a native Winget upgrade path (#30026) highlight platform-specific maintenance debt.
- **Performance Unpredictability:** OpenCode hangs entirely on specific setup scenarios: low Linux inotify limits (#16610), PowerShell 7.6 commands (#25938), and slow OpenCode Go proxy responses (#20404).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi community digest for 2026-06-13.

---

## Pi Community Digest – 2026-06-13

### 1. Today’s Highlights
The ecosystem moves quickly with **v0.79.2** shipping and a flurry of 16 PRs merged, spanning game-dev tooling (`AiGameAgent`) and a new **Anthropic Vertex** provider. Despite the velocity, the community’s loudest conversation remains **Issue #4945**, where `openai-codex` sessions routinely hang with no output, no errors, and no tool calls. Major fixes landed this cycle for macOS crash safety, config env-var migration bugs, and Anthropic refusal visibility.

### 2. Releases
- **v0.79.2**: Patch release primarily targeting the **Amazon Bedrock** experience. Data retention validation errors now link directly to AWS documentation for faster debugging.

### 3. Hot Issues
Covering the 10 most noteworthy topics from the 50 updated in the last 24 hours.

1.  **#4945 – Codex Connection Reliability (Open)**  
    *Comments: 55 | 👍: 30*  
    The top-voted open issue. The TUI frequently freezes on `Working...` with no streaming, tool calls, or visible errors, forcing users to press Escape to abort. Community is actively debugging SSE timeouts and network resilience.  
    [Issue #4945](https://github.com/earendil-works/pi/issues/4945)

2.  **#5667 – Bash Overflow Crashes Pi on macOS (Closed)**  
    *Comments: 6*  
    High-impact crash: when bash output exceeds ~50KB, Pi spills to `$TMPDIR`, which is often a non-writable placeholder path on macOS, causing an unhandled `EACCES` crash. Fixed quickly in this cycle.  
    [Issue #5667](https://github.com/earendil-works/pi/issues/5667)

3.  **#5653 – Duplicate Install Splits Provider Registry (Open)**  
    *Comments: 5*  
    Installing `@earendil-works/pi-ai` alongside `@earendil-works/pi-coding-agent` creates two module instances, splitting the global `Map` of API providers. Tied directly to the `npm-shrinkwrap.json` packaging decision. A core architecture bug for extension users.  
    [Issue #5653](https://github.com/earendil-works/pi/issues/5653)

4.  **#5633 – Kimi 2.6 “reasoning_content” Tool Call Error (Closed)**  
    *Comments: 6*  
    Continuing a session with Kimi 2.6 fails when thinking is enabled because Pi omits `reasoning_content` in tool call messages, which the Kimi API strictly requires. Highlights edge cases in multi-turn reasoning model support.  
    [Issue #5633](https://github.com/earendil-works/pi/issues/5633)

5.  **#5595 – maxTokens Not Passing Through (Open)**  
    *Comments: 4*  
    Using OpenAI-compatible providers (e.g., Together.ai) with reasoning models like DeepSeek V4 causes the agent to run out of output tokens before completing a turn because the `maxTokens` setting is silently ignored.  
    [Issue #5595](https://github.com/earendil-works/pi/issues/5595)

6.  **#5577 – Persona Override for System Prompt (Closed)**  
    *Comments: 4*  
    A heavily requested feature asking for the ability to define custom agent roles (security, QA, research) without losing the coding assistant base. Reflects the growing use of Pi as a general-purpose agentic harness.  
    [Issue #5577](https://github.com/earendil-works/pi/issues/5577)

7.  **#5619 – `pi update` Triggers Trust Dialog (Closed)**  
    *Comments: 5*  
    Running `pi update` from an untrusted directory like `~` causes an unwanted trust prompt. Fixed by filtering home directory `.pi` overlaps from the trust check.  
    [Issue #5619](https://github.com/earendil-works/pi/issues/5619)

8.  **#5654 – `excludeFromContext` for Custom Messages (Open)**  
    *Comments: 3*  
    Community member requests the ability to flag custom messages (e.g., status reports) to skip the LLM entirely, mirroring the existing bash execution flag. A key feature for managing context windows in long-running sessions.  
    [Issue #5654](https://github.com/earendil-works/pi/issues/5654)

9.  **#5661 – Uppercase Header Values Treated as Env Vars (Open)**  
    *Comments: 2*  
    Configuration bug: literal uppercase values in `models.json` (e.g., `"BEARER"`) are falsely rewritten to `"$BEARER"` by the migration script. A fix PR (#5660) is already merged for the next release.  
    [Issue #5661](https://github.com/earendil-works/pi/issues/5661)

10. **#5673 – vLLM DeepSeek Thinking Format (Open)**  
    *Comments: 3*  
    Enterprise users running DeepSeek behind vLLM need a new `chat_template_kwargs` format for thinking tokens. Demonstrates increasing demand for custom provider extensions and heterogenous deployment patterns.  
    [Issue #5673](https://github.com/earendil-works/pi/issues/5673)

---

### 4. Key PR Progress
10 significant pull requests from the 16 updated in the last 24 hours.

1.  **#5681 – Integrate AiGameAgent (Merged)**  
    *Brings `YeLuo45/AiGameAgent` into the monorepo as a new package supporting HTML5/WeChat/Douyin mini-game workflows via an OpenAI-compatible HTTP API.*  
    [PR #5681](https://github.com/earendil-works/pi/pull/5681)

2.  **#5679 – Add Anthropic Vertex Provider (Merged)**  
    *Fully integrated `anthropic-vertex` provider routing Claude through Google Cloud Vertex AI using ADC auth, including model registration and interactive picker support.*  
    [PR #5679](https://github.com/earendil-works/pi/pull/5679)

3.  **#5674 – Fix Trust Prompt on Update (Merged)**  
    *Directly fixes the #5619 UX bug by filtering out the home directory from trust resolution.*  
    [PR #5674](https://github.com/earendil-works/pi/pull/5674)

4.  **#5678 – `excludeFromContext` for Custom Messages (Open)**  
    *Implements the feature from #5654, preserving the skip flag through persistence and compaction.*  
    [PR #5678](https://github.com/earendil-works/pi/pull/5678)

5.  **#5675 – Stabilize Compaction After Reload (Merged)**  
    *Fixes the `prevCompaction is not defined` crash that could occur after session reload.*  
    [PR #5675](https://github.com/earendil-works/pi/pull/5675)

6.  **#5666 – Preserve Anthropic Refusal Details (Merged)**  
    *Propagates Anthropic `stop_details` to the user when a model refuses an output, improving the error feedback loop.*  
    [PR #5666](https://github.com/earendil-works/pi/pull/5666)

7.  **#5660 – Fix Uppercase Header Env Var Rewrite (Merged)**  
    *Fixes the root cause of #5661 by tightening the migration regex.*  
    [PR #5660](https://github.com/earendil-works/pi/pull/5660)

8.  **#5600 – Honor Codex SSE Header Timeout (Merged)**  
    *Replaces a hardcoded 10-second header timeout with the user-configured `timeoutMs`, addressing a major sub-issue in the Codex reliability saga (#4945).*  
    [PR #5600](https://github.com/earendil-works/pi/pull/5600)

9.  **#5587 – Experimental First-Time Setup Flow (Merged)**  
    *Behind `PI_EXPERIMENTAL=1`, introduces an onboarding dialog that detects terminal theme and asks for analytics consent.*  
    [PR #5587](https://github.com/earendil-works/pi/pull/5587)

10. **#5634 – Normalize Generated Model Costs (Merged)**  
    *Rounds per-token prices to 6 decimal places in generated models, eliminating floating-point artifacts across OpenRouter and Vercel AI Gateway costs.*  
    [PR #5634](https://github.com/earendil-works/pi/pull/5634)

---

### 5. Feature Request Trends
- **Provider Hub Expansion:** The community demands broad API compatibility. Requests for Amazon Bedrock Mantle, Anthropic Vertex, vLLM proxy modes, and deeper OpenCode/litellm support signal a desire to turn Pi into a universal model backend client.
- **Role-Driven Agentic Workflows:** Users want Pi to function as a swappable agentic harness, not just a coding assistant. The `persona override` request (#5577) and context-control proposals suggest an appetite for multi-role (security, QA, project management) personas built on the same scaffolding.
- **Context Window Economy:** As sessions grow longer, the community is proactively asking for tools to manage token budgets—specifically `excludeFromContext` flags and better compactor guarantees. This is a maturing user base dealing with real agentic workloads.
- **Gaming and Specialized Niches:** The merge of `AiGameAgent` alongside existing coding tooling indicates the monorepo is intentionally becoming an incubator for specialized agent packages.

### 6. Developer Pain Points
- **Stream Resilience is the #1 Friction:** Hanging streams with no timeout (`openai-codex`, `opencode-go`) are the most commonly reported reliability issue. Users rely on manual escape hatch (Escape key) to recover, which is a productivity killer.
- **Environment and Configuration Gotchas:** The frequency of subtle config bugs is high this cycle. Short-lived bugs like the `MACOS TMPDIR` crash, uppercase env-var migration bugs, and the shrinkwrap duplication all represent "first-run" or "first-deep-use" landmines that erode user trust.
- **Glue Code Fragility:** Issues around stale event listeners (#5573), broken compaction (#5676), and orphaned session trees (#5669) point to brittle timing assumptions in Pi's async state machine, particularly around session reload and tool execution settlement.
- **Package Management Tight Coupling:** The `bun` vs `npm` incompatibility and the shrinkwrap duplication issue highlight friction in the extension installation channel, which is critical to the platform's growth strategy.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-13

## 1. Today's Highlights
Release **v0.18.0** dropped overnight, fixing a CLI copy-output bug for thought parts, though its VSIX triggered a Windows antivirus false positive that is actively being triaged ([#5055](https://github.com/QwenLM/qwen-code/issues/5055)). The community is sharply divided over Issue [#3203](https://github.com/QwenLM/qwen-code/issues/3203), a controversial proposal to slash the OAuth free tier from 1,000 to 100 requests/day ahead of a full phase-out (127 comments and counting). Meanwhile, the `qwen serve` daemon architecture continues maturing: OpenTelemetry coverage landed on `main` ([#4554](https://github.com/QwenLM/qwen-code/issues/4554)), and a new `DaemonTransport` abstraction ([#5040](https://github.com/QwenLM/qwen-code/pull/5040)) paves the way for REST/ACP-HTTP/ACP-WS pluggability.

## 2. Releases
**v0.18.0** published. Changelog highlights:
- chore(release): v0.17.1 setup (CI/infra bump)
- fix(cli): skip thought parts in copy output ([@he-yufeng](https://github.com/he-yufeng))

Users installing the VS Code companion (`qwenlm.qwen-code-vscode-ide-companion-0.18.0-win32-x64.vsix`) should note the reported Trojan:JS/ShaiWorm.DBA!MTB false positive in [#5055](https://github.com/QwenLM/qwen-code/issues/5055) — the team is investigating.

## 3. Hot Issues (10 picks)

1. **[#3203](https://github.com/QwenLM/qwen-code/issues/3203) — Qwen OAuth Free Tier Policy Adjustment** *(127 comments)*  
   Proposes reducing the free daily quota from 1,000 to 100 requests, then closing the free entry point entirely on June 20. The most controversial item in the tracker this month; heavy community backlash asking for alternatives or grandfathering.

2. **[#4514](https://github.com/QwenLM/qwen-code/issues/4514) — Daemon capability gaps & prioritized backlog** *(15 comments)*  
   Master tracking issue for `qwen serve` HTTP/SSE surface gaps post-v0.16-alpha. De facto roadmap for daemon feature parity (slash commands, ACP bridge, MCP transport pool). Essential reading for anyone building on the daemon runtime.

3. **[#4488](https://github.com/QwenLM/qwen-code/issues/4488) — qwen-code plugin not visible in VS Code 1.120+ sidebar** *(7 comments)*  
   Plugin icon flashes and disappears on newer VS Code releases. Regressed somewhere between 1.95.3 and 1.120.0. Affects Windows/Linux users on the latest VS Code updates.

4. **[#4821](https://github.com/QwenLM/qwen-code/issues/4821) — Declarative agent definitions via frontmatter files** *(6 comments)*  
   Requests Claude Code's `.claude/agents` pattern for Qwen Code: define agents as Markdown+YAML frontmatter instead of hardcoded TypeScript. High-priority feature signal.

5. **[#3267](https://github.com/QwenLM/qwen-code/issues/3267) — Requests limits overview / daily quota confusion** *(6 comments)*  
   Users report hitting the 1,000/day cap before completing a single task, triggering support for the #3203 policy debate. Points to opaque quota tracking in the dashboard.

6. **[#4877](https://github.com/QwenLM/qwen-code/issues/4877) — Same model from different providers indistinguishable** *(4 comments)*  
   `modelProviders` config cannot differentiate `glm-5` from OpenAI vs. another endpoint. Causes unpredictable model switching. Addressed in PR [#5039](https://github.com/QwenLM/qwen-code/pull/5039) (see below).

7. **[#5016](https://github.com/QwenLM/qwen-code/issues/5016) — Tool execution after cancellation (SIGINT)** *(2 comments)*  
   Critical safety issue: interrupting a streaming tool call does not prevent tool work from executing. Deterministically reproducible with a local provider. Followed by [#5015](https://github.com/QwenLM/qwen-code/issues/5015) (repeated identical tool calls).

8. **[#5055](https://github.com/QwenLM/qwen-code/issues/5055) — Trojan:JS/ShaiWorm.DBA!MTB false positive in v0.18.0 VSIX** *(2 comments)*  
   Windows Defender flags the VSIX package as a trojan. A packaging/signing issue that blocks adoption for enterprise Windows users.

9. **[#5019](https://github.com/QwenLM/qwen-code/issues/5019) — Repetitive tool calls in long-context sessions** *(2 comments)*  
   Long-running tasks loop on identical tool calls until the API rejects the session. Related to [#5015](https://github.com/QwenLM/qwen-code/issues/5015) and the overarching attention-degrade thread [#5018](https://github.com/QwenLM/qwen-code/issues/5018).

10. **[#4891](https://github.com/QwenLM/qwen-code/issues/4891) — Terminal resize fragments streaming output** *(3 comments)*  
    Resizing the terminal during generation leaves scrollback rendered at inconsistent widths. Tool-call borders terminate at wrong columns. Common UX frustration for CLI-first users.

## 4. Key PR Progress (10 picks)

1. **[#5040](https://github.com/QwenLM/qwen-code/pull/5040) — `feat(sdk): DaemonTransport abstraction`**  
   Makes `DaemonClient` transport-agnostic. Clients can now use REST+SSE (default), ACP HTTP+SSE, or ACP WebSocket without forking infrastructure. Major architectural unlock for daemon extensibility.

2. **[#5066](https://github.com/QwenLM/qwen-code/pull/5066) — `feat(web-shell): daemon web-shell improvements`** *(merged)*  
   Ships structured token usage tracking, a full settings panel (i18n, theme, language, compact mode), and retry capability for the daemon web shell.

3. **[#5039](https://github.com/QwenLM/qwen-code/pull/5039) — `fix(cli): use id+baseUrl for precise model identity`**  
   Resolves [#4877](https://github.com/QwenLM/qwen-code/issues/4877). Stores `model.id`, `model.baseUrl`, and `model.provider` to disambiguate same-named models from different endpoints.

4. **[#5073](https://github.com/QwenLM/qwen-code/pull/5073) — `fix: warn on oversized context instructions`**  
   Startup warning when `QWEN.md` or always-loaded instructions exceed 15% of the active model’s context window. Prevents silent context blowups.

5. **[#5070](https://github.com/QwenLM/qwen-code/pull/5070) — `fix(cli): ignore expired live agents in focus navigation`**  
   Fixes [#5067](https://github.com/QwenLM/qwen-code/issues/5067). Prevents keyboard focus from targeting stale/expired terminal agents in the LiveAgentPanel.

6. **[#5057](https://github.com/QwenLM/qwen-code/pull/5057) — `fix(core): Persist file history snapshot updates`**  
   Durability fix for `/rewind`: file-history snapshots are now written immediately when edits occur, not deferred to turn boundaries. Prevents data loss on crash.

7. **[#5003](https://github.com/QwenLM/qwen-code/pull/5003) — `feat(tui): remove tool group borders and collapse completed tool results`**  
   UI cleanup: removes round borders from tool groups and collapses completed tool blocks to a single-line status header in compact mode.

8. **[#4598](https://github.com/QwenLM/qwen-code/pull/4598) — `feat(tui): collapsible thinking blocks with duration timer`**  
   Long-running PR (since May 28) nearing merge. Replaces the always-expanded thinking display with a collapsible streaming block + completion timer.

9. **[#4933](https://github.com/QwenLM/qwen-code/pull/4933) — `feat(config): add settings file change detection via chokidar watcher`**  
   Hot-reload support for `~/.qwen/settings.json`. Watches for file changes and applies them without a daemon restart.

10. **[#5033](https://github.com/QwenLM/qwen-code/pull/5033) — `fix(serve): Add prompt queue backpressure`**  
    Protects the daemon prompt queue under high load. Prevents unbounded queuing when forwarding to the LLM endpoint.

## 5. Feature Request Trends

- **Declarative agent definitions**  
  Strong demand for file-based agent definitions ([#4821](https://github.com/QwenLM/qwen-code/issues/4821)) mirroring Claude Code’s `.claude/agents` pattern, combined with better background agent lifecycle and approval-request queuing ([#4928](https://github.com/QwenLM/qwen-code/issues/4928)).

- **Configuration migration & scalability**  
  Users managing multiple providers want deduplication of shared `baseUrl` values ([#4813](https://github.com/QwenLM/qwen-code/issues/4813)), a `/import-config` command to migrate from Claude Code/Desktop ([#4845](https://github.com/QwenLM/qwen-code/issues/4845)), and hot-reload support (addressed by [#4933](https://github.com/QwenLM/qwen-code/pull/4933)).

- **Script-friendly session tooling**  
  Repeated calls for a `qwen sessions list` subcommand with `--json`, `--tag`, and date filters ([#4825](https://github.com/QwenLM/qwen-code/issues/4825)). Users want to script session management without parsing opaque history files.

- **Daemon mode as a first-class platform**  
  Feature requests consistently orbit the `qwen serve` runtime: OpenTelemetry (landed), transport pluggability ([#5040](https://github.com/QwenLM/qwen-code/pull/5040)), web-shell improvements ([#5066](https://github.com/QwenLM/qwen-code/pull/5066)), and prompt backpressure ([#5033](https://github.com/QwenLM/qwen-code/pull/5033)) all indicate daemon stability is the top infrastructure priority.

## 6. Developer Pain Points

- **Free tier uncertainty**  
  The proposed 90% quota cut and full phase-out in [#3203](https://github.com/QwenLM/qwen-code/issues/3203) (127 comments) is the loudest community signal. Developers relying on the free tier for prototyping are actively seeking alternatives or grandfathering paths.

- **Long-context reliability**  
  Multiple reports of model “degradation” over long sessions: repetitive tool calls that terminate sessions ([#5019](https://github.com/QwenLM/qwen-code/issues/5019)), tools executing after cancellation ([#5016](https://github.com/QwenLM/qwen-code/issues/5016)), and general “dumbing down” ([#5029](https://github.com/QwenLM/qwen-code/issues/5029)). This erodes trust for complex workflows.

- **Cross-platform friction**  
  Windows continues to lag: `printf` command not found at startup ([#5010](https://github.com/QwenLM/qwen-code/issues/5010)), VS Code plugin invisible on newer VS Code ([#4488](https://github.com/QwenLM/qwen-code/issues/4488)), and antivirus false positives on releases ([#5055](https://github.com/QwenLM/qwen-code/issues/5055)). These compound to make onboarding outside macOS/Linux surprisingly fragile.

- **Configuration overhead**  
  Duplicating `baseUrl` for every model under the same provider runtime ([#4813](https://github.com/QwenLM/qwen-code/issues/4813)) creates unnecessary config bloat. Combined with the inability to distinguish same-named models across providers ([#4877](https://github.com/QwenLM/qwen-code/issues/4877)), provider management remains a high-friction daily task.

- **Session observability**  
  Lack of a built-in `sessions list` command forces users to parse JSONL history files manually ([#4825](https://github.com/QwenLM/qwen-code/issues/4825)). The `/goal` counter resetting on resume ([#4999](https://github.com/QwenLM/qwen-code/issues/4999)) further complicates trust in long-running automated workflows.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

## DeepSeek TUI Community Digest — 2026‑06‑13

### 1. Today’s Highlights
The project formally rebrands from `deepseek-tui` to **CodeWhale** in v0.8.59. Development velocity remains extraordinary: the maintainer is simultaneously shipping a full “Agent Fleet” runtime (leases, heartbeats, inbox, alerting), a deep architectural refactor to remove DeepSeek‑specific hard‑coding, and new first‑party providers (Anthropic, Z.ai, StepFlash). Community feedback is heavily shaping this cycle, with targeted fixes for TUI freezing under high context load and much better error diagnostics for autonomous agents.

---

### 2. Releases

**v0.8.59 — New & Notable**
The only release in the last 24 h. It is a **full project rebrand**:
- The canonical project, command, and npm package are now `codewhale`.
- The legacy `deepseek-tui` npm package is deprecated and will receive no further releases.
- Migration instructions are in `docs/REBRAND.md`.

*Note:* The feature‑dense work landing today (Anthropic client, fleet infrastructure, provider abstraction) lives on higher version‑track branches (v0.8.58–v0.8.60). v0.8.59 cuts the naming change so the next round of releases carries the new identity.

---

### 3. Hot Issues (Top 10)

1.  **Hmbown/CodeWhale Issue #2584 — `[bug]` Cannot upload local images** *(Closed)*  
    A critical multimodal regression: `/attach` sends a file *path* instead of base64. Highlights fragility in the input pipeline during the rapid refactor cycle.

2.  **Hmbown/CodeWhale Issue #1871 — QoL: taskbar progress, animated title spinner, configurable completion sound** *(Closed)*  
    High community demand (+1). Users repeatedly ask for alt‑tab feedback—a strong signal that CodeWhale is being used as a background agent host.

3.  **Hmbown/CodeWhale Issue #1722 — TUI completely unresponsive at ~99.6% context saturation** *(Closed)*  
    **Pain point of the week.** “Memory 100%” was starving the TUI event loop. The fix adds an auto‑compact threshold + `Ctrl+L` binding.

4.  **Hmbown/CodeWhale Issue #3018 — Un‑hardcode DeepSeek from auto‑router and subagent model selection** *(Closed)*  
    The biggest architectural bottleneck. Non‑DeepSeek providers received `deepseek-v4-flash` model IDs, guaranteeing a 400 error. This fix is foundational for the multi‑provider future.

5.  **Hmbown/CodeWhale Issue #2606 — Sidebar “Work” panel checklist not updating after turn completes** *(Closed)*  
    The main chat says “100% complete”, but the sidebar shows stale state. Hurts trust in agent reporting.

6.  **Hmbown/CodeWhale Issue #431 — Bundled Exa web‑search route** *(Open)*  
    Clean `OPENCODE` methodology: gated behind `EXA_API_KEY` with a graceful fallback to free DDG/Bing. Shows the maintainer’s structured approach to feature flags.

7.  **Hmbown/CodeWhale Issue #3159 — Fleet scheduler: leases, heartbeats, backpressure, stuck‑worker recovery** *(Closed)*  
    Core reliability for the v0.8.60 Agent Fleet. Without this, large fan‑out reproduces the existing hung‑subagent failure modes at scale.

8.  **Hmbown/CodeWhale Issue #2657 — Modes: agents cannot easily tell why a tool is unavailable** *(Closed)*  
    A fundamental “Agent Experience” (AX) gap. If the AI cannot debug its own permission state, it wastes user time asking for mode switches.

9.  **Hmbown/CodeWhale Issue #471 — EPIC: Web UI scaffold (Option A)** *(Open)*  
    The strategic plan for escaping the terminal. SolidJS/React + Vite + SSE. Includes a file browser and Monaco editor pane.

10. **Hmbown/CodeWhale Issue #407 — Replace Tasks sidebar with an active Agents workbench** *(Open)*  
    A strategic UX pivot. The low‑value Tasks panel is to be replaced with a live dashboard showing every agent’s step, status, and controls.

---

### 4. Key PR Progress (Top 10)

1.  **Hmbown/CodeWhale PR #3191 — Z.ai & StepFlash provider routes**  
    Adds two major providers as first‑class citizens, matching their official API specs rather than routing through an OpenAI‑compatible slot.

2.  **Hmbown/CodeWhale PR #3054 — Native Anthropic Messages API adapter**  
    A full wire dialect for Anthropic with `thinking` blocks, tool streaming, and cache control. Dramatically broadens the user base.

3.  **Hmbown/CodeWhale PR #3045 — Un‑hardcode DeepSeek from model validation**  
    Allows Moonshot, Ollama, OpenAI etc. to use their own model IDs for sub‑agents and spawn‑time model selection.

4.  **Hmbown/CodeWhale PR #3042 — `exec` CLI flags for unattended/CI usage**  
    Adds `--allowed-tools`, `--disallowed-tools`, `--max-turns`. Transforms `codewhale exec` into a proper CI/benchmark runner.

5.  **Hmbown/CodeWhale PR #3035 — Throttle AgentProgress redraws**  
    Fixes a TUI freeze when 4+ sub‑agents run concurrently by debouncing `needs_redraw`. A targeted performance fix for the agent runtime.

6.  **Hmbown/CodeWhale PR #3049 — JSON decision contract for hooks**  
    Upgrades tool‑call hooks from arbitrary scripts to a structured JSON output (`allow` / `deny` / `ask`). Enables rich security policies.

7.  **Hmbown/CodeWhale PR #3034 — v0.8.58 branch: Constitution refactor + sidebar split**  
    A massive foundational commit: YAML‑based constitution, rebrand fixes, provider error improvement. The “operating system” layer of the agent.

8.  **Hmbown/CodeWhale PR #3041 — Harvested error‑message fixes from community PR**  
    Integrates community contributions (#2933) to vastly improve tool denial messages and subagent conflict diagnostics.

9.  **Hmbown/CodeWhale PR #3036 — Hide internal IDs from normal UI**  
    Replaces raw UUIDs in agent panels with stable labels. A major UX polish that makes the agent workbench human‑readable.

10. **Hmbown/CodeWhale PR #3037 — Compact tool‑call transcript rendering**  
    Suppresses boilerplate (“no output”, sub‑second timings). Cleans up the primary agent transcript during live monitoring.

---

### 5. Feature Request Trends

- **Multi‑Provider Abstraction is the #1 theme.** The project is aggressively removing DeepSeek‑specific assumptions from routing, model validation, pricing, and prompts. Users want to bring any LLM backend without friction (#3018, #3045, #3047, #3054).
- **Agent Fleet & Background Jobs.** The maintainer is investing heavily in scalable, resilient agent execution (durable inbox, leases, heartbeat, SSH workers, Slack/webhook alerts, task specs) (#3155–3162).
- **Asynchronous & Non‑Blocking UX.** Community demands auditory/visual cues for long‑running tasks (#1871), better context saturation handling (#1722), and reliable sidebar state (#2606).
- **Platform Expansion.** There is strong momentum toward a Web UI (#471-#474) and a VS Code extension (#461) as “escape hatches” from the TUI.
- **Structured Security Policy.** The hook system is moving toward a formal JSON contract, broader permission memory, and external directory gates (#3049, #411-#412).

---

### 6. Developer Pain Points

- **TUI Unresponsiveness Under Load.** “Memory 100%” context saturation (#1722) and subagent redraw storms (#3035) make the tool unusable in heavy sessions. This is the top UX complaint.
- **DeepSeek Lock‑In Causes Silent Failures.** Hardcoded model IDs and provider‑specific logic cause cryptic errors when using Ollama, OpenAI, or Moonshot (#3018, #3047). Requires careful migration.
- **Weak Agent Self‑Diagnosis.** The AI agent struggles to explain why tools are denied or why session names conflict, wasting turns and frustrating users (#2656, #2657).
- **Rebranding Migration Overhead.** The `deepseek-tui` to `codewhale` rename forces users to update scripts, muscle memory, and CI configurations.
- **Modal & Permission Complexity.** The strict Plan / Agent / YOLO mode system creates friction, though the maintainer is actively improving error messages and feedback paths (#3041, #1871).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*