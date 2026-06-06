# AI CLI Tools Community Digest 2026-06-06

> Generated: 2026-06-06 02:50 UTC | Tools covered: 9

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
**Date:** 2026-06-06 | **Audience:** Technical Decision-Makers & Developers

## 1. Ecosystem Overview

The AI CLI tool landscape is nearing a stability inflection point. After a year of breakneck feature expansion, the dominant pattern emerging across all major tools is an industry-wide struggle to translate autonomous agent promises into production-grade reliability. Common fracture points—session state corruption, silent cost leaks from "doom loops," OAuth credential fragility, and severe platform-specific regressions on Windows/WSL2—create a significant gap between the ceiling of what these tools can demo and the floor of daily developer trust. Concurrently, the community is voting heavily on enterprise readiness: multi-user authentication, declarative permission systems, and audit-friendly session transparency are the loudest cross-cutting demands. The ecosystem is clearly moving from an era of capability demonstration to one of reliability engineering and operational maturity.

## 2. Activity Comparison (24-Hour Window)

| Tool | Repository | Hot Issues (Notable) | Key PRs (Substantive) | Releases (24h) |
|---|---|---|---|---|
| **Claude Code** | anthropics/claude-code | 10 (Parser failures, credential corruption) | 2 (Plugin metadata, dev container fix) | 3 (v2.1.165–167) |
| **OpenAI Codex** | openai/codex | 10 (WSL perf collapse, MCP pooling, remote dev) | 10 (MCP lifecycle, subagent cancel, plugin sharing) | 1 (v0.138.0-alpha.5) |
| **Gemini CLI** | google-gemini/gemini-cli | 10 (Pro auth issues, subagent opacity) | 10 (3.5 Flash support, PTY crash, Gateway auth fix) | 3 (nightly, preview, stable) |
| **GitHub Copilot CLI** | copilot-cli | 10 (WSL CPU spin, ARM64 abort, MCP leaks) | 0 | 1 (v1.0.60) |
| **Kimi CLI** | MoonshotAI/kimi-cli | 2 (WS daemon brick, session logout) | 6 (RalphFlow, MCP cleanup, migration UX) | 1 (v1.47.0 rebrand) |
| **OpenCode** | anomalyco/opencode | 10 (Plan mode, auto-scroll bug, multi-user auth) | 10 (Service API refactor, skill toggle, inline skills) | 1 (v1.16.2) |
| **Pi** | earendil-works/pi | 10 (Working hang, compaction crash) | 10 (Multi-agent workflow, Vertex provider, self-evolver) | 0 |
| **Qwen Code** | QwenLM/qwen-code | 10 (OOM on resume, daemon gaps, web search) | 10 (Daemon mode merge, HTTP parity, memory commands) | 1 (v0.17.1-nightly) |
| **DeepSeek TUI / CodeWhale** | Hmbown/CodeWhale | 10 (UI refactor, IDE plugin demand) | 10 (WhaleFlow engine, VS Code scaffold, HarmonyOS port) | 0 |

**Key Observations:**
- **Bug Fix Mode:** Claude Code and Copilot CLI show high release cadence but low/no substantive PRs, indicating reactive stabilization cycles.
- **Feature Velocity:** Qwen Code, OpenCode, and Pi exhibit the highest substantive PR output, actively expanding architecture.
- **Stealth Building:** DeepSeek TUI (CodeWhale) has deep PR investment without a public release, suggesting a major v0.9.0 "big bang" is brewing.

## 3. Shared Feature Directions

The following requirements recurred across multiple tool communities with high signal:

| Requirement | Tools Affected | Community Pain Point |
|---|---|---|
| **Multi-Agent Orchestration & Visibility** | Claude Code, Codex, Pi, OpenCode, Gemini CLI | Non-blocking sub-agents, real-time status dashboards, inter-session communication |
| **MCP Server Lifecycle Maturity** | Codex, Copilot CLI, Kimi CLI, Qwen Code, Pi, DeepSeek TUI | Persistent process pools (not per-session spawning), clean shutdown, OAuth recovery, deduplication |
| **Platform Parity (WSL2, ARM64, Alpine)** | Codex, Copilot CLI, OpenCode, Qwen Code | Windows/WSL2 performance collapse is the single largest cross-tool regression cluster. macOS is universally first-class; everything else is second-class. |
| **Cost Governance & Loop Detection** | OpenCode, Pi, Kimi CLI, Claude Code | "Doom loops" burning API credits, silent cost leakage, need for budget caps and cost-per-agent tracking |
| **Config Portability & Declarative Setups** | Claude Code, Copilot CLI, Qwen Code, Gemini CLI | Account-level settings sync, case-insensitive session names, shared base URLs, CLI-selectable profiles |
| **Auth Infrastructure Hardening** | Claude Code, Gemini CLI, Pi, DeepSeek TUI | OAuth refresh corruption, stale token recovery, provider-scoped credentials, enterprise SSO |
| **Session State Integrity** | Claude Code, Gemini CLI, Copilot CLI, Pi, Qwen Code | Crashes on `--resume`, corrupted transcripts/JSONL, hanging `/rewind`, silent compaction failures |

## 4. Differentiation Analysis

| Tool | Feature Focus | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Deep agentic depth, Plugin ecosystem, Anthropic model exclusivity | AI-native engineers, power users | Node.js, rich TUI, closed-source core |
| **OpenAI Codex** | MCP infrastructure, Computer Use skill, Remote workspaces, Model leadership | Early adopters, API-first teams | Rust + TypeScript hybrid, heavy MCP investment |
| **Gemini CLI** | Multi-model portfolio (3.5 Flash), Vertex AI/GCP integration, Enterprise Gateway auth | Enterprise teams already on GCP | TypeScript, cloud-integrated auth path |
| **GitHub Copilot CLI** | IDE synergy (VS Code), Terminal multiplexer behavior, GitHub ecosystem | GitHub-centric developers, CI/CD users | Rust-based, strong GitHub platform tie-in |
| **Kimi CLI** | Agent loop safety (RalphFlow), Smooth migration to successor Go binary | Moonshot AI ecosystem users | Python (maintenance mode) → Go (successor) |
| **OpenCode** | Extensibility (Skills, MCP), Multi-provider agnosticism, Rapid community iteration | Open-source community, platform-agnostic teams | TypeScript, modular plugin architecture |
| **Pi** | Research-grade agent orchestration, Self-evolving architectures, Deep extension APIs | Agent researchers, advanced power users | TypeScript, experimental high-concept features |
| **Qwen Code** | HTTP-first "Daemon Mode", REST API parity with CLI, Server-centric deployment | Programmatic orchestration, CI/CD pipelines, web-shell users | TypeScript (Ink/React), strong API-first design |
| **DeepSeek TUI (CodeWhale)** | Native Rust performance, VS Code IDE integration, Typed workflow engine (WhaleFlow) | Performance-sensitive developers, IDE-native users | Rust, typed domain logic, formal workflow engine |

## 5. Community Momentum & Maturity

- **Highest Volume / Signal-to-Noise Ratio:** **Claude Code** and **OpenAI Codex** command the largest user bases and most issue engagement. Feature requests from these communities (e.g., multi-agent orchestration, remote workspaces) effectively set the roadmap for the broader ecosystem. However, the high volume includes a substantial tail of critical reliability complaints.

- **Highest Code Velocity (Substantive Changes):** **Qwen Code**, **OpenCode**, and **Pi** show the strongest evidence of rapid, concurrent feature development across PR pipelines. Qwen Code's Daemon Mode merge (386 files, +115k LOC) is the single largest architectural change in this window. OpenCode is building a mature skill ecosystem. Pi continues pushing advanced agent research concepts into production paths.

- **Enterprise-Stabilization Mode:** **Gemini CLI** and **OpenCode** are clearly investing in enterprise-hardening features: multi-user auth, Vertex AI integration, workspace approval flows, and session snapshotting.

- **Crisis Mode / Stabilization:** **GitHub Copilot CLI** is facing a severe regression cluster (WSL CPU spin, ARM64 aborts, Alpine packaging). The zero-PR count in 24 hours suggests the team is fully occupied with high-severity triage and testing.

- **Transitioning Project:** **Kimi CLI** is proactively warning users of its deprecation toward a new Go successor. Community momentum is split between migration and maintenance.

- **Pre-Release Building:** **DeepSeek TUI (CodeWhale)** is investing heavily in foundational re-architecture (WhaleFlow, VS Code scaffold, HarmonyOS port) without a corresponding release, signaling a major v0.9.0 milestone in the near term.

## 6. Trend Signals (Actionable Insights for Developers & Decision-Makers)

1. **The "Agent Runtime" Is the New Battleground.** Tools are no longer LLM wrappers—they are becoming full-fledged agent runtimes (RalphFlow in Kimi, WhaleFlow in CodeWhale, Daemon Mode in Qwen Code). The winner will be the platform with the most robust state management, sub-agent lifecycle handling, and error recovery across interruptions.

2. **MCP Is Ubiquitous but Immature.** Every tool with MCP support is struggling with process leaks, deadlocks on startup/shutdown, credential state management, and tool name parsing edge cases. Investment in MCP lifecycle tooling (pooling, credential rotation, network resilience) is a high-ROI differentiator.

3. **Platform Parity Is Table Stakes, Not a Feature.** macOS enjoys first-class support everywhere. Windows/WSL2 (Codex, Copilot, OpenCode) and Linux musl/ARM targets (Copilot, Pi, CodeWhale) are routinely broken. Rust-native tools (CodeWhale, Copilot CLI) have an inherent advantage in predictable cross-platform behavior, but must avoid testing gaps.

4. **Cost Governance Is the Unlocking Feature for Enterprise.** "Doom loops" (OpenCode, Pi), silent cost leakage (Claude Code image processing), and quota drain from orphaned sub-agents (Codex) are the loudest enterprise blockers. Features like `--ephemeral` mode, real-time cost-per-agent dashboards, and automatic runaway detection are becoming non-negotiable for adoption by cost-conscious teams.

5. **Observability Is the Top Unresolved Pain Point.** Across the board, users express a deep need to see *what the agent is doing* (subagent status, file changes, thinking trace), *what it costs* (usage summary), and *why it failed* (auth vs. API vs. tool parsing). Tools providing excellent audit trails, session replay, and failure diagnostics will win developer trust.

6. **IDE Integration Is the Endgame for Mass Adoption.** Multiple communities (DeepSeek TUI, Claude Code) explicitly demand VS Code parity. Pure terminal experience is valued by power users, but the IDE canvas is where most professional developers live. Copilot CLI's IDE synergy is a strength. CodeWhale's VS Code scaffold is a strategic bet.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on repository activity as of June 6, 2026.

---

### 1. Top Skills Ranking
*The following represent the most-discussed and highest-activity skill submissions currently under review.*

**1. n8n Workflow Automation Suite** ([PR #190](https://github.com/anthropics/skills/pull/190))
- **Functionality:** A dual-skill submission (`n8n-builder`, `n8n-debugger`) that equips Claude to build workflows from natural language and diagnose pipeline failures within the n8n automation platform.
- **Discussion:** Signals a strong turn toward agent-driven low-code workflow configuration rather than pure code generation. The community is actively bridging agent reasoning with visual automation.
- **Status:** Open

**2. Enterprise Platform Assistants** ([PR #568](https://github.com/anthropics/skills/pull/568), [PR #181](https://github.com/anthropics/skills/pull/181))
- **Functionality:** ServiceNow skill covering ITSM, ITOM, SecOps, ITAM, and SPM. SAP skill wrapping the open-source RPT-1-OSS tabular foundation model for predictive business analytics.
- **Discussion:** Deep SME-level platform knowledge is a growing requirement. These are not shallow wrappers; they embed significant domain logic and model integration.
- **Status:** Open

**3. Persistent Agent Memory Infrastructure** ([PR #154](https://github.com/anthropics/skills/pull/154), [PR #444](https://github.com/anthropics/skills/pull/444))
- **Functionality:** `shodh-memory` provides structured, cross-conversation memory retrieval. The AURELION suite implements a five-floor cognitive framework for knowledge management and structured reasoning.
- **Discussion:** Overcomes the fundamental LLM statelessness issue. Two distinct architectural approaches (lightweight retrieval vs. structured framework) are being actively debated.
- **Status:** Open

**4. Developer Testing Patterns** ([PR #723](https://github.com/anthropics/skills/pull/723))
- **Functionality:** Comprehensive testing skill based on the Testing Trophy model, covering AAA-pattern unit testing, React Testing Library, and edge case handling.
- **Discussion:** Addresses a universal developer gap. The explicit focus on what *not* to test demonstrates a mature, token-efficiency-aware design philosophy.
- **Status:** Open

**5. Document Typography Quality Control** ([PR #514](https://github.com/anthropics/skills/pull/514))
- **Functionality:** Detects and prevents orphan word wrap, widow paragraph breaks, and numbering misalignment in generated documents.
- **Discussion:** Universally applicable across all document generation tasks. Low complexity, high cross-domain value, and a clear fix for a persistent LLM output quality issue.
- **Status:** Open

**6. Ecosystem Meta-Skills** ([PR #83](https://github.com/anthropics/skills/pull/83))
- **Functionality:** `skill-quality-analyzer` and `skill-security-analyzer` evaluate other skills across structure, documentation, and trust boundary dimensions.
- **Discussion:** Indicates ecosystem maturation. The community is proactively building quality assurance and security governance into the skills layer itself, directly responding to rising security concerns.
- **Status:** Open

**7. Workflow Integrity & Multi-Tool Agents** ([PR #363](https://github.com/anthropics/skills/pull/363), [PR #1140](https://github.com/anthropics/skills/pull/1140))
- **Functionality:** Fixes a critical `TodoWrite` overwrite bug that causes skipped phases in multi-step workflows. The `agent-creator` meta-skill generates task-specific agent teams.
- **Discussion:** Deep engagement with the mechanics of reliable agent orchestration. The `agent-creator` points toward automated agent assembly, a frontier capability.
- **Status:** Open

---

### 2. Community Demand Trends
*Derived from the highest-activity Issues.*

- **Enterprise Governance & Infrastructure Scaling:** The loudest demand is for organization-wide tooling. Issue [#228](https://github.com/anthropics/skills/issues/228) (Org-wide skill sharing, 13 comments, 7 👍) and Issue [#492](https://github.com/anthropics/skills/issues/492) (Trust boundary abuse under the `anthropic/` namespace) dominate. Companies are blocked on deployment without shared libraries, security zoning, and cloud platform support (Bedrock, [#29](https://github.com/anthropics/skills/issues/29)).
- **Tooling Stability & Developer Experience:** A significant volume of top issues are bugs in the `skill-creator` tooling itself. Issue [#556](https://github.com/anthropics/skills/issues/556) (*run_eval.py* zero trigger rate, 11 comments, 6 👍) is the single most disruptive bug for skill developers. Combined with disappearing skills ([#62](https://github.com/anthropics/skills/issues/62), [#61](https://github.com/anthropics/skills/issues/61)) and duplicate installations ([#189](https://github.com/anthropics/skills/issues/189)), the toolchain's fragility is a primary friction point.
- **Protocol Interoperability & Modular Engineering:** The community is pushing for composable skill architectures. Demands for MCP exposure ([#16](https://github.com/anthropics/skills/issues/16)), multi-file preloading ([#1220](https://github.com/anthropics/skills/issues/1220)), and portability labels ([#1156](https://github.com/anthropics/skills/issues/1156)) reveal a desire to standardize skill delivery and integrate with external tooling protocols.

---

### 3. High-Potential Pending Skills
*Active, non-merged PRs with strong community alignment and clear utility.*

- **ServiceNow Platform Skill** ([PR #568](https://github.com/anthropics/skills/pull/568)): Directly answers enterprise governance demands. Deep coverage of CSDM, SecOps, and IntegrationHub.
- **Testing Patterns Skill** ([PR #723](https://github.com/anthropics/skills/pull/723)): Fills a universal developer tooling gap. Highly likely to merge given strong standard developer workflow alignment.
- **Document Typography Skill** ([PR #514](https://github.com/anthropics/skills/pull/514)): Low implementation complexity with a clear, high-value quality promise.
- **Windows Compatibility Cluster** ([PR #1099](https://github.com/anthropics/skills/pull/1099), [PR #1050](https://github.com/anthropics/skills/pull/1050), [PR #541](https://github.com/anthropics/skills/pull/541), [PR #539](https://github.com/anthropics/skills/pull/539), [PR #538](https://github.com/anthropics/skills/pull/538)): A critical set of bug fixes and encoding patches addressing platform parity. Essential for expanding the contributor ecosystem beyond macOS/Linux.
- **Skill Security Analyzer** ([PR #83](https://github.com/anthropics/skills/pull/83)): Directly addresses the trust boundary crisis raised in Issue [#492](https://github.com/anthropics/skills/issues/492). High momentum as a governance tool.

---

### 4. Skills Ecosystem Insight
The community's most concentrated demand is a push from **individual experimentation toward production-grade enterprise infrastructure**, specifically requiring **org-wide governance, security namespacing, platform parity, and deeply reliable core tooling** (persistent memory, testing patterns, workflow orchestration) that can serve as a stable foundation for complex agentic systems.

---

# Claude Code Community Digest: June 06, 2026

## Today's Highlights

A quiet release cycle punctuated a week of reliability fixes (v2.1.167) following the notable v2.1.166 rollout which introduced configurable fallback models. Community sentiment remains dominated by agent reliability concerns—particularly the recurring tool-call parsing failures that persistently kill in-progress sessions—while a fresh wave of OAuth credential corruption reports signals deeper auth infrastructure fragility that is frustrating power users.

## Releases

Three versions shipped in the last 24 hours:

- **[v2.1.167](https://github.com/anthropics/claude-code/releases/tag/v2.1.167)** (latest): Bug fixes and reliability improvements.
- **[v2.1.166](https://github.com/anthropics/claude-code/releases/tag/v2.1.166)**: Introduced `fallbackModel` setting, allowing users to define up to three fallback models tried in order when the primary is overloaded. The `--fallback-model` flag now applies to interactive sessions. Glob pattern support was added to the deny rule tool-name position (`"*"` denies all tools).
- **[v2.1.165](https://github.com/anthropics/claude-code/releases/tag/v2.1.165)**: Bug fixes and reliability improvements.

The `fallbackModel` feature in v2.1.166 is a meaningful quality-of-life improvement for teams relying on consistent availability, though the full changelog appears to be partially truncated in the release notes.

## Hot Issues

*10 selected for community impact and signal value*

### 1. [#63875: Recurring "tool call could not be parsed" interruptions](https://github.com/anthropics/claude-code/issues/63875)
**42 comments · 62 👍 · Windows & general**
The single most disruptive active bug. Claude Code abruptly stops mid-task with a parsing error that doesn't self-correct, killing the in-progress action. The high upvote count and cross-platform reports signal a core reliability regression. *Risk: Severe to agentic workflows.*

### 2. [#60334: Image processing failures eating API tokens](https://github.com/anthropics/claude-code/issues/60334)
**54 comments · 14 👍 · macOS**
A persistent cost sink: image processing errors silently consume roughly 70% of session allowances without the model receiving the image data. Users are effectively burning budget on invisible failures. *Risk: Cost & trust erosion.*

### 3. [#63456: Opus 4.8 missing from CLI model picker](https://github.com/anthropics/claude-code/issues/63456)
**17 comments · 11 👍 · macOS**
Users with Opus 4.8 access via claude.ai cannot select it in the CLI `/model` picker, which only surfaces older Opus variants. Creates a frustrating platform parity gap for terminal-first developers.

### 4. [#64651: VSCode: background agent output floods foreground chat](https://github.com/anthropics/claude-code/issues/64651)
**4 comments · 1 👍 · VSCode**
When Claude spawns subagents (e.g. via `run_in_background: true`), output bleeds into the user's active conversation. This ruins UX for developers relying on concurrent agent workflows in the extension.

### 5. [#62202: Desktop/VSCode SIGTERM every 300 seconds](https://github.com/anthropics/claude-code/issues/62202)
**2 comments · 1 👍 · macOS, Desktop/VSCode**
A critical lifecycle bug: the child process in Desktop and VSCode wrappers is killed with SIGTERM at exactly 5-minute intervals. Terminal CLI is unaffected, pointing to a wrapper-specific regression. *Risk: Severe for IDE-dependent users.*

### 6. [#61912: OAuth refresh corruption → persistent 401 loop](https://github.com/anthropics/claude-code/issues/61912)
**4 comments · 0 👍 · Linux**
Transient Cloudflare 5xx responses during OAuth refresh can corrupt the credential state, producing an unrecoverable 401 loop across sessions. *Risk: Auth infrastructure fragility.*

### 7. [#65757: Image attachments not reaching the model](https://github.com/anthropics/claude-code/issues/65757)
**2 comments · 0 👍 · Web**
Screenshots and images attached in claude.ai code mode are silently stripped before reaching the model. A core multimodal feature is completely non-functional in this context.

### 8. [#65761: `/login` fails to fix stale OAuth tokens](https://github.com/anthropics/claude-code/issues/65761)
**2 comments · 0 👍 · WSL**
`/login` reports success but doesn't clear the bad token. Manual deletion of `~/.claude/.credentials.json` is the only recovery path. Another data point for credential management issues.

### 9. [#65620: Transcript regression—text blocks dropped from JSONL](https://github.com/anthropics/claude-code/issues/65620)
**2 comments · 0 👍 · macOS, regression (~2.1.159–162)**
When a turn produces interleaved thinking blocks, preceding assistant text blocks are silently omitted from session transcripts. Data integrity loss for teams relying on audit trails. *Risk: Moderate for compliance-minded users.*

### 10. [#65768: Plugin subagents can't resolve `${CLAUDE_PLUGIN_ROOT}`](https://github.com/anthropics/claude-code/issues/65768)
**2 comments · 0 👍 · Cross-platform**
Plugin developers hit a blocker: subagents receive plugin environment variables as literal strings, preventing access to plugin-bundled files. *Risk: Plugin ecosystem maturity.*

---

## Key PR Progress

*Only 4 PRs were active in the window. The two substantive items:*

### [PR #65619: fix(plugins): align frontend-design author with marketplace entry](https://github.com/anthropics/claude-code/pull/65619)
Fixes [#61785](https://github.com/anthropics/claude-code/issues/61785). A clean metadata schema fix for the `frontend-design` plugin where the `author` field was malformed (comma-separated values packed into single-name/email fields). Resolves rendering issues in plugin UIs and marketplaces without behavioral changes.

### [PR #65666: Fix dev container issues](https://github.com/anthropics/claude-code/pull/65666)
Resolves build failures from DNS-blocked domains in the official dev container and adds an environment variable passthrough mechanism for API keys. Low risk, practical improvement for community contributors.

*Note: Remaining PRs (#58673, #65723) appear to be test / placeholder submissions with no substantive code changes.*

---

## Feature Request Trends

*Distilled from 50 active issues*

### 1. Multi-Agent Orchestration & Session Federation
The strongest signal from enhancement requests. Users want Claude Code to function as an **orchestration layer** for interconnected agent sessions:
- **Agent-to-Agent protocol** across machines ([#28300](https://github.com/anthropics/claude-code/issues/28300))
- **Session Teams** enabling structured inter-session communication ([#65590](https://github.com/anthropics/claude-code/issues/65590))
- **Cross-project session handoff** that spawns autonomous sessions in different directories and reads results back ([#65456](https://github.com/anthropics/claude-code/issues/65456))

This suggests the community sees Claude Code evolving beyond single-session coding into an autonomous agent coordination platform.

### 2. Account & Configuration Portability
Sustained demand for multi-device parity:
- **Account-level settings sync** across machines ([#22648](https://github.com/anthropics/claude-code/issues/22648) with 37 👍 — explicitly noted as "requested multiple times")
- **Multiple Connector accounts** on the same connector type ([#27302](https://github.com/anthropics/claude-code/issues/27302)—195 comments, 261 👍, the most active feature thread)

### 3. Platform Parity
Requests to close gaps between CLI, web, Desktop, and IDE:
- **Model switching for Cowork tasks** within Projects ([#49649](https://github.com/anthropics/claude-code/issues/49649), 20 👍)
- **Diff viewer improvements** in Desktop (collapsible unchanged lines, [#65311](https://github.com/anthropics/claude-code/issues/65311))
- **VSCode session title** display in tab switcher ([#65776](https://github.com/anthropics/claude-code/issues/65776))

---

## Developer Pain Points

### 1. Fragile Agent Execution
The "#63875 class" of issues—tool call parsing failures that silently kill active tasks—is the community's top frustration. This isn't a cosmetic bug; it fundamentally breaks the core value proposition of a persistent coding agent. Developers are reporting "this happens repeatedly across many sessions" with no self-correction path.

### 2. Auth Infrastructure Weakness
A concentrated cluster of credential management failures:
- OAuth refresh corruption from transient upstream errors ([#61912](https://github.com/anthropics/claude-code/issues/61912))
- `/login` command that cannot recover bad tokens ([#65761](https://github.com/anthropics/claude-code/issues/65761))
- Inconsistent auth state between `claude auth status` and actual runtime ([#65725](https://github.com/anthropics/claude-code/issues/65725))

Manual credential file deletion as the only recovery path is a poor developer experience for a daily-driver tool.

### 3. Silent Failures & Cost Leakage
- **Image processing failures** burning API tokens without feedback ([#60334](https://github.com/anthropics/claude-code/issues/60334))
- **Transcript text blocks silently dropped** during interleaved thinking ([#65620](https://github.com/anthropics/claude-code/issues/65620))
- **Usage credit blockers** triggering prematurely during context compaction ([#65756](https://github.com/anthropics/claude-code/issues/65756))

These "invisible" failures erode trust in the tool's accounting and data integrity.

### 4. IDE/Desktop Lifecycle Inconsistency
The platform gap between CLI (stable) and Desktop/VSCode (5-minute SIGTERM timeouts, background chat pollution, branch picking issues) creates a fragmented experience. Developers working primarily in IDEs face a meaningfully worse reliability profile than terminal CLI users.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — June 6, 2026

Codex hits a stability inflection point this week: the community is loudly rallying around basic reliability on Windows and WSL2, while OpenAI internal teams make significant strides on MCP lifecycle, subagent cancellation, and a long-awaited plugin sharing system. A massive upvoted feature request for Remote Development closing signals a gap the community is desperate to fill.

---

## Today's Highlights

- **Windows/WSL2 performance cascade:** Multiple high-activity issues confirm that versions post 0.133.0 introduced severe sandbox spawn failures and UI freezes, making the Desktop app almost unusable for WSL2 users.
- **MCP lifecycle gets a deep clean:** PRs fixing lock contention during prewarm, OAuth credential false positives, and a multi-PR plugin sharing stack hit `main`, signaling a maturation of the MCP framework.
- **Subagent interruption finally works:** `#26717` ensures Guardian and parent turn cancellation is properly propagated, solving a long-standing source of "zombie" agent sessions burning quota.

---

## Releases

- **[Codex CLI 0.138.0-alpha.5](https://github.com/openai/codex/releases/tag/0.138.0-alpha.5):** Alpha staging release. No changelog provided in the release note, but the bump follows significant sandbox and session logic changes in the preceding days.
- **rusty-v8-v149.2.0:** Transitive dependency update for the bundled JavaScript runtime.

> *Omitted if no significant Codex-specific releases exist beyond the alpha CLI.*

---

## Hot Issues (10 Noteworthy)

1. **[#10450 — Remote Development in Codex Desktop](https://github.com/openai/codex/issues/10450)**
   *Closed, 177 comments, 674 👍*
   The most upvoted issue ever for Codex, asking for SSH/tunnel-based remote development (think VS Code Remote — Containers/SSH). The community was passionate, but the issue was recently closed, likely as "won't do" or deferred. A huge signal that the community wants Codex to detach from the local filesystem.

2. **[#18258 — Computer Use Plugin Unavailable (macOS)](https://github.com/openai/codex/issues/18258)**
   *Open, 39 comments*
   A persistent bug for the Computer Use skill on macOS. Community workaround involves `features.apps = true` in `config.toml` and manual cache path repairs. Affected users are stuck waiting for an official fix.

3. **[#25715 — Codex App Unusable Slow with WSL](https://github.com/openai/codex/issues/25715)**
   *Open, 31 comments*
   "Routine turns in WSL2 take minutes." The App is drastically slower than the CLI on the same WSL2 filesystem. Pro and Pro+ users are complaining loudly, marking this as the top Windows experience blocker.

4. **[#24391 — Windows Sandbox Spawn Setup Fails (CLI 0.133.0)](https://github.com/openai/codex/issues/24391)**
   *Open, 28 comments*
   `spawn setup` refresh fails after updating. Breaks all shell commands on Windows CLI. The community is actively debugging Node/npm version mismatches and path issues.

5. **[#20883 — MCP Process Pool (Project-Scoped)](https://github.com/openai/codex/issues/20883)**
   *Open, 10 comments*
   A strongly requested enhancement: share MCP server processes across sessions within a workspace instead of spawning new processes per chat. Directly tied to the memory exhaustion reports in `#11324`.

6. **[#16900 / #22099 — Subagent Status & Parallel Execution](https://github.com/openai/codex/issues/16900)**
   *Open, 10 comments each*
   Developers want parent-child subagent lifecycle visibility. `#22099` includes a working fork demonstrating parallel-first delegation. The core ask: make subagents non-blocking background tasks with real-time status.

7. **[#19891 — "For Coding" View Hides Details](https://github.com/openai/codex/issues/19891)**
   *Open, 7 comments, 7 👍*
   A UI regression where granular file edits and commands are buried under aggregate summaries, making it harder for developers to audit exactly what the agent did.

8. **[#4849 — Config Profiles Selectable via CLI](https://github.com/openai/codex/issues/4849)**
   *Open, 6 comments, 23 👍*
   Long-standing request for `codex --profile my-profile` to avoid globally switching configs. Momentum is building as multi-provider setups become common.

9. **[#11324 / #21984 — MCP Server Memory & Eager Start](https://github.com/openai/codex/issues/11324)**
   *Open, 9 comments / 7 comments*
   MCP servers started per-session with no cleanup. Headed browser MCP processes accumulate visibly. Users working across multiple worktrees hit OOM regularly.

10. **[#24618 — Context Compaction Hangs (504)](https://github.com/openai/codex/issues/24618)**
    *Open, 5 comments*
    The automatic compaction endpoint can hang for 30–60 minutes or return a 504 gateway error, while normal streaming continues to work. Wastes quota and blocks long-running sessions.

---

## Key PR Progress (10 Important)

1. **[#26717 — Stop Guardian Reviews When Parent Turns Are Interrupted](https://github.com/openai/codex/pull/26717)**
   Critical fix: Guardian approval sessions now properly cancel when the parent turn is aborted. Previously, the Guardian could keep running indefinitely, burning quota and blocking the UI.

2. **[#26432 — Release MCP Manager Lock Before Listing Tools](https://github.com/openai/codex/pull/26432)**
   Fixes a deadlock during startup prewarm. Tool listing held a read lock blocking session shutdown's write lock. This explains some "stuck on shutdown" reports, especially with sluggish MCP servers.

3. **[#26715 — Load direnv Environment into Shell Snapshots](https://github.com/openai/codex/pull/26715)**
   Integrates `direnv` with shell environment capture. If Codex is launched inside a `direnv`-managed directory, environment variables now propagate correctly to the agent's shell.

4. **[#26719 — Enable Standalone Web Search in Code Mode](https://github.com/openai/codex/pull/26719)**
   Unlocks standalone web search (via `/v1/alpha/search`) in Code Mode, allowing the coding agent to fetch context without going through the chat interface.

5. **[#26711 — Reduce TUI Legacy Core Dependencies](https://github.com/openai/codex/pull/26711)**
   Strips the TUI of its `legacy_core` dependency for thread name normalization and `/init` detection. Crucial for clean remote app-server session support.

6. **[#26703 / #26704 / #26701 — TUI Plugin Sharing Stack](https://github.com/openai/codex/pull/26703)**
   A three-PR feature drop adding full remote plugin catalog support to the TUI. Browsing, installation, deduplication, and share-management are now foundational. This is the groundwork for the "Codex App Store" the community has been asking for.

7. **[#26713 — Report Unusable MCP OAuth Credentials as Logged Out](https://github.com/openai/codex/pull/26713)**
   Expired tokens with no usable refresh token are now correctly reported as "logged out" instead of the misleading "OAuth" status. No more silent auth failures.

8. **[#26686 — Propagate Client UI Capabilities (MCP)](https://github.com/openai/codex/pull/26686)**
   Adds semantic UI capabilities to the MCP initialize handshake. MCP servers can now tell whether they are being used from the App or TUI and adjust behavior (e.g., showing popups vs. logging).

9. **[#26678 — Permission Profile Availability for Clients](https://github.com/openai/codex/pull/26678)**
   Prevents clients from offering permission policies that are blocked by enterprise requirements. A serious enterprise/compliance gap fix for managed environments.

10. **[#26542 — Responses Lite Transport Header](https://github.com/openai/codex/pull/26542)**
    Sends `X-OpenAI-Internal-Codex-Responses-Lite` on HTTP and WebSocket requests when model metadata enables Responses Lite. An infrastructure optimization likely improving latency and cost on supported models.

---

## Feature Request Trends

- **Remote Workspaces (#10450):** The single strongest community signal: users want Codex to natively support SSH, Dev Containers, and virtualized development environments. The closing of #10450 without an official solution leaves a vacuum the community is still vocal about.
- **MCP Process Management (#20883, #21984, #11324):** A clear demand for a project-scoped MCP server pool. Users are tired of per-session spawning and unmanaged process accumulation.
- **Subagent Parallelism (#16900 / #22099):** The linear subagent model frustrates power users. They want non-blocking background execution and real-time status dashboards for multi-agent workflows.
- **Custom Profiles & Agents (#4849, #26408):** Deep customization remains a priority. CLI-selectable profiles and the ability to reliably spawn project-scoped custom agents from `.codex/agents` are the top asks.

---

## Developer Pain Points

- **Windows + WSL2 Experience (The #1 Problem):**
  This is the hottest pain point. Issues #25715, #24391, #25799, #25362, #20967, and #23137 all report distinct but overlapping failures:
  - `spawn setup` refresh failures.
  - OS Error 740 (elevation issues).
  - Drastic slowdown vs. CLI.
  - Infinite sandbox configuration loops.
  - Micro-freezes on UI rendering.

  **Bottom line:** Running Codex on Windows targeting a WSL2 Linux environment is significantly degraded compared to macOS.

- **Session Leaks and Quota Drain:**
  Users frequently report mysterious quota consumption (#26600). Root causes appear to be hanging context compactions (#24618), orphaned subagents (#19197), and Guardian sessions not respecting parent interruption (now fixed in #26717).

- **MCP Fragility:**
  Eager process spawning, deadlocks on startup/shutdown, and confusing credential states make MCP feel fragile. While PRs this week target these issues, the damage to trust from silent OAuth failures and resource leaks is significant.

- **UI Regressions Eroding Trust:**
  The decision to aggregate file changes in the "For Coding" view (#19891) was widely panned. Combined with general freezes on Windows (#26401, #26697), the desktop app experience is losing polish parity with the web/CLI experience.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

Here is the Gemini CLI community digest for June 6, 2026.

---

## Gemini CLI Community Digest — 2026-06-06

### 1. Today's Highlights
Three patch releases landed today, with a critical fix backported cleanly across the stable and preview channels. On the main branch, a massive internal PR introduces Gemini 3.5 Flash support and promotes Gemini 3.1 Flash Lite to GA, signaling the team is already looking past the current preview cycle. The community remains vocal about agent reliability and session state bugs, while the team landed targeted fixes for PTY crashes, resume session corruption, and Gateway authentication regressions.

### 2. Releases
Three new builds were shipped in the last 24 hours:

- **[v0.47.0-nightly.20260605](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-nightly.20260605.g4196596f7):** Standard nightly build moving the main branch forward.
- **[v0.46.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.2):** Cherry-picks hotfix `f40498d` into the preview branch. Full changelog.
- **[v0.45.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.2):** Cherry-picks the same `f40498d` fix into the current stable line.

*Takeaway:* The backport of a specific commit across both preview and stable suggests a targeted, high-impact regression that required immediate coverage.

### 3. Hot Issues

1. **[#27033 – Pro Subscription not reflected in Tier](https://github.com/google-gemini/gemini-cli/issues/27033)** (7 comments)
   User reports Google AI Pro subscription not propagating to the CLI, which only shows "Google Assist." High friction for paid users.
2. **[#27326 – 403 PERMISSION_DENIED for Pro Subscribers](https://github.com/google-gemini/gemini-cli/issues/27326)** (5 comments)
   Sign-in works, but every prompt fails with a 403 on `cloudcode-pa`. Users express frustration that suggested fix PRs remain unmerged.
3. **[#22323 – Subagent GOAL success hides MAX_TURNS failure](https://github.com/google-gemini/gemini-cli/issues/22323)** (6 comments)
   A subagent reports `status: "success"` despite hitting the turn limit. Dangerous opacity that breaks trust in multi-agent workflows.
4. **[#25166 – Shell command hangs after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments)
   Gemini frequently hangs on "Awaiting user input" after a CLI command finishes. Top pain point for interactive coding sessions.
5. **[#21968 – Agent doesn’t use custom skills or sub-agents](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)
   Despite having "gradle" and "git" skills, the conductor ignores them unless explicitly instructed. Undermines the value of custom tool definitions.
6. **[#25646 – /rewind shows pre-load points after session resume](https://github.com/google-gemini/gemini-cli/issues/25646)** (4 comments)
   `/rewind` fails to load the correct state after `/chat resume`. A core workflow for recovering long sessions is broken.
7. **[#24246 – 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (3 comments)
   The agent breaks when the available tool count is too high. Community wants smarter tool scoping rather than a hard crash.
8. **[#26525 – Auto Memory sends content to model before redaction](https://github.com/google-gemini/gemini-cli/issues/26525)** (4 comments)
   Logs and model context receive raw transcript data before secrets are redacted. Active security concern under discussion.
9. **[#15404 – Antivirus false positive (PyStealer)](https://github.com/google-gemini/gemini-cli/issues/15404)** (6 comments)
   Temp files flagged as `Generic.PyStealer.AD`. Erodes user confidence and causes tooling conflicts.
10. **[#27692 – Duplicate agent warning in home directory](https://github.com/google-gemini/gemini-cli/issues/27692)** (3 comments)
    Running the CLI from the user home directory throws a false positive "Duplicate agent" warning. High frequency issue affecting a common setup.

### 4. Key PR Progress

1. **[#27705 – Promote 3.1 Flash Lite to GA & Add 3.5 Flash](https://github.com/google-gemini/gemini-cli/pull/27705)**
   A mega-PR promoting gemini-3.1-flash-lite to stable and adding support for Gemini 3.5 Flash.
2. **[#27372 – Fix PTY crash on resize after exit](https://github.com/google-gemini/gemini-cli/pull/27372)**
   Catches `EBADF` when a terminal resize fires just after a child PTY exits. Fixes a common crash in headless and background workflows.
3. **[#27375 – Fix Vertex AI model detection for Gemini 3](https://github.com/google-gemini/gemini-cli/pull/27375)**
   Vertex AI resource paths (`projects/.../models/gemini-3.1-pro-preview`) were failing the regex, blocking enterprise users from using most tools.
4. **[#27369 – Fix `--resume` deleting sessions](https://github.com/google-gemini/gemini-cli/pull/27369)**
   Passing `--resume` caused sessions to permanently disappear from the browser. High severity UI regressing.
5. **[#27365 – Add `--ephemeral` session mode](https://github.com/google-gemini/gemini-cli/pull/27365)**
   New flag for headless/automation runs that prevents flooding session history. Community written, guided by real data-labelling workflow needs.
6. **[#27568 – Fallback when ripgrep fails](https://github.com/google-gemini/gemini-cli/pull/27568)**
   Gracefully falls back to the legacy `GrepTool` if ripgrep is missing or exits abnormally. Improves resilience across environments.
7. **[#27558 / #27553 – Fix Gateway auth regression](https://github.com/google-gemini/gemini-cli/pull/27558)**
   Gateway authentication via `GOOGLE_GEMINI_BASE_URL` was broken because `validateAuthMethod()` lacked the new `GATEWAY` type. Two PRs targeting the same root cause.
8. **[#27552 – Fix `$` substitution in prompt templates](https://github.com/google-gemini/gemini-cli/pull/27552)**
   `String.prototype.replace` was silently corrupting user content containing `$` signs. Fix uses literal replacement to prevent prompt injection.
9. **[#27701 – Fix startup crash on missing include directories](https://github.com/google-gemini/gemini-cli/pull/27701)**
   Switches `WorkspaceContext` from strict `addDirectory` to lenient `addDirectories` so optional paths don't crash the CLI on launch.
10. **[#27708 – Harden CI prompt against untrusted data](https://github.com/google-gemini/gemini-cli/pull/27708)**
    Prevents unsafe workflow data from being passed directly into AI prompts. Security hardening for the CI pipeline itself.

### 5. Feature Request Trends

- **AST-aware Codebase Mapping:** Multiple issues and EPICs (e.g. [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)) request AST-aware file reads and codebase navigation to reduce token waste and improve code extraction precision.
- **Ephemeral & Headless Sessions:** The reception of `--ephemeral` and the community frustration with session state bugs strongly indicate a market need for a clean, non-interactive mode that doesn’t pollute persistent state.
- **Autonomous Tool Selection:** A recurring theme is the agent’s failure to autonomously activate relevant skills and sub-agents ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)). Users want smarter inference of *when* to use custom tools.
- **Sub-agent Configuration Overrides:** Users want granular control over sub-agent behavior (e.g. `maxTurns` for the browser agent) without modifying global registries ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).

### 6. Developer Pain Points

- **Session State Corruption:** Bugs with `/resume`, `/rewind`, and shell history merging create unreliable long-running experiences. The hanging "Waiting input" state ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) is a top workflow blocker.
- **Sub-agent Opacity / False Positives:** Agents reporting `"GOAL"` success despite hitting turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) severely undermines trust. When the model cannot be trusted to report its own failures, it hinders all autonomous use cases.
- **Paid Tier Friction:** Multiple reports of Pro subscribers hitting 403 errors and tier mismatches ([#27033](https://github.com/google-gemini/gemini-cli/issues/27033), [#27326](https://github.com/google-gemini/gemini-cli/issues/27326)) create immediate customer churn risk.
- **Platform Compatibility Fragmentation:** The CLI struggles to maintain feature parity across platforms, with specific breakages reported on Wayland (browser agent), Termux, Windows PTY, and specific GPU configurations.
- **Security Friction:** Antivirus false positives and pre-redaction data leaks in Auto Memory are eroding trust, especially among enterprise teams evaluating the tool.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — June 6, 2026

## Today's Highlights

Yesterday's **v1.0.60** release brought tab-completion improvements for path arguments, unified reasoning effort levels for Anthropic models, and a fix for terminal multiplexer sleep/wake rendering failures. However, the last 24 hours have been dominated by a surge of high-severity bug reports, including a **WSL2 CPU spin regression** freezing the TUI ([#3700](#3700)), **fatal aborts on Windows ARM64** under load ([#3687](#3687)), and **unbounded MCP server process leaks** ([#3701](#3701), [#3698](#3698)). The community is also actively pressing for better platform parity on Linux ARM64 and musl-based systems, increased configuration persistence, and resolution of long-standing terminal clipboard conflicts.

---

## Releases

**v1.0.60** (Released 2026-06-05)
- ✅ **Tab Completion:** `..` parent traversal now works correctly in slash-command path arguments, fixing a previous conflict with tab switching.
- ✅ **Reasoning Effort:** Added the maximum reasoning effort level for Anthropic models; all effort tiers (low, medium, high, max) are now available across all subscription plans.
- ✅ **Terminal Multiplexer Fix:** The screen no longer remains blank after waking from sleep inside a multiplexer session (tmux/screen).
- [View Release](https://github.com/github/copilot-cli/releases/tag/v1.0.60)

---

## Hot Issues (10 noteworthy items)

1. **[#3700](https://github.com/github/copilot-cli/issues/3700) — [High] WSL2 Regression: MainThread CPU Spin & TUI Freeze**  
   The CLI instantly enters a ~215% CPU spin state on idle WSL2 sessions, and the TUI output completely freezes until restart. Reported as a regression of #2208 with immediate reproducibility after a clean boot. *(1 👍, new)*

2. **[#3687](https://github.com/github/copilot-cli/issues/3687) — [High] Windows ARM64 Fatal Abort (BEX64 / 0xc0000409)**  
   `copilot.exe` hard-aborts instead of shutting down gracefully, reliably triggered by session restores and memory pressure. Confirmed on both v1.0.57 and v1.0.60, impacting Windows ARM64 users heavily. *(3 comments)*

3. **[#3701](https://github.com/github/copilot-cli/issues/3701) — Runaway MCP Server Spawning via IDE Lock-File Watcher**  
   When an IDE integration is active with a configured MCP server, the file watcher enters a re-init loop that spawns unbounded child processes, degrading the entire machine. *(1 comment, fresh report)*

4. **[#2334](https://github.com/github/copilot-cli/issues/2334) — [Popular] Bring Back `no-alt-screen` Mode**  
   One of the highest-voted open issues (28 👍). Users strongly prefer no-alt-screen for scrollback history, searching, and reviewing large diffs. The current alt-screen implementation is widely described as a usability regression.

5. **[#2101](https://github.com/github/copilot-cli/issues/2101) — Persistent Transient API Errors & Rate Limiting**  
   A long-running issue (27 comments, 17 👍). Users are hitting repeated `Request failed due to a transient API error` messages followed by aggressive rate limits, interrupting extended coding sessions.

6. **[#3563](https://github.com/github/copilot-cli/issues/3563) — Tool Approvals Silently Lost in Parallel Sessions**  
   Running multiple `copilot` sessions simultaneously can cause one session's "Always allow" permissions to silently overwrite another's in `~/.copilot/permissions-config.json`. A critical data-integrity bug for multi-tasking workflows.

7. **[#3547](https://github.com/github/copilot-cli/issues/3547) — Background Sub-Agent Hangs with `gpt-5.5` Model**  
   When spawning a background sub-agent with `model="gpt-5.5"`, the agent reports a successful start but hangs indefinitely at `total_turns=0`, blocking dependent workflows. *(3 comments)*

8. **[#3696](https://github.com/github/copilot-cli/issues/3696) — Alpine Linux Auto-Update Breaks Node Runtime**  
   The auto-update mechanism downloads the `linux-x64` package on musl-based systems (Alpine) instead of `linuxmusl-x64`, causing `Native addon "runtime" not found` errors on the very next invocation.

9. **[#2998](https://github.com/github/copilot-cli/issues/2998) — Copy/Paste Pushes Previous Clipboard Content**  
   A confounding UX bug: selecting and copying text inside the CLI replaces the selection with whatever was *previously* stored in the system clipboard. Related to a family of terminal input frustrations (#3693, #2344).

10. **[#3695](https://github.com/github/copilot-cli/issues/3695) — `/fork` Session Command Fails with NAPI String Error**  
   The core `/fork` workflow for branching conversations is broken on Windows, failing with a raw Rust-to-napi string conversion error. Blocks a key iteration pattern for users.

---

## Key PR Progress

No pull requests were updated in the last 24 hours. This typically indicates the team is actively triaging the significant influx of high-priority bug reports rather than landing new features.

---

## Feature Request Trends

- **Persistent Configuration & Session State**  
  Users are consistently pushing back on ephemeral wizard-based setups. Requests for a **default permissions config file** ([#2398]), **always-visible session names** ([#3415]), and **case-insensitive session resumption** ([#3694]) point to a desire for a stateful, declarative CLI that remembers context across terminals and reboots.

- **MCP & Agent Ecosystem Tooling**  
  The rapid adoption of MCP servers and agent skills is driving demand for **better lifecycle management** (no leaks on reconnect, #3698), **comprehensive documentation paths** ([#3688]), and **security controls for repository-provided hooks** ([#3697] in response to the Miasma worm campaign).

- **Platform Parity Expansion**  
  Linux ARM64 users are requesting **voice mode installation** ([#3690]). Alpine/musl users need correct **platform detection for auto-updates** ([#3696]). Windows ARM64 users require stable crash recovery ([#3687]). The community expects first-class support across all architectures and libc variants.

- **Terminal Input & Display Integration**  
  Feature requests continue to cluster around native terminal behavior: **opt-out alt-screen** ([#2334]), **sensible Escape handling** that preserves queued prompts ([#3692]), and **standard clipboard workflows** ([#3693]).

---

## Developer Pain Points

- **Multi-Platform Regression Clusters**  
  The simultaneous surfacing of severe regressions on **WSL2** (CPU spin, TUI freeze), **Windows ARM64** (fatal abort), and **Alpine Linux** (packaging breakage) suggests platform-specific testing gaps in the current release cycle. Each of these completely blocks productive use on the affected OS.

- **MCP Server Lifecycle Management**  
  Two separate reports of **unbounded process spawning** ([#3701], [#3698]) and a **permission-config corruption** in parallel sessions ([#3563]) erode confidence in the MCP and agent infrastructure.

- **Permission & Security Model Friction**  
  Beyond the silent overwrites, the community is actively concerned about **supply-chain risks from repository hooks** ([#3697]) and the inconsistent resolution of **`allowed-tools` in non-interactive mode** ([#3699]).

- **Transient Backend Errors**  
  The continued complaints around **rate limiting and transient API errors** ([#2101]) indicate that backend capacity or throttling logic remains a persistent source of friction for power users.

- **Configuration File Fragility**  
  Inconsistencies in how the CLI resolves paths for **custom agents vs. skills** (`git root` vs `cwd`, [#3688]), combined with **case-sensitive repository name checks** ([#3694]), create subtle "works on my machine" failures that are hard to diagnose.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi CLI Community Digest — 2026-06-06

**Data Source:** [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

## Today’s Highlights
The project officially rebranded to **Kimi CLI** in v1.47.0, drawing a clear line to its standalone Go-based successor. A major architectural milestone—the **RalphFlow** agent loop prevention framework—was merged (PR #1960). Meanwhile, a critical **WebSocket daemon failure** (Issue #2435) is actively blocking the `kimi web` Work tab for Windows users.

## Releases
**v1.47.0** ([PR #2433](https://github.com/MoonshotAI/kimi-cli/pull/2433))
- **Rebranding:** Project and docs now explicitly refer to the Python edition as *Kimi CLI* to resolve name collision with the successor at `MoonshotAI/kimi-code`.
- **Migration Path:** Introduced the `/upgrade` command to cleanly install the new single-binary Kimi Code, migrating configs and sessions automatically.
- **Bug Fixes:** Tool error messages are now rendered as plain text instead of raw `tools/include` output.

## Hot Issues
*(2 items updated in the last 24h found in the dataset)*

- **#2435 [OPEN] Work tab: "Daimon control WS not ready" + infinite reload loop**
  - **Why it matters:** A WebSocket initialization failure bricks the Work tab entirely on Windows 10/11. The UI enters an infinite 99% reload cycle, making the feature completely unusable without a workaround.
  - **Community reaction:** Very recent report (no comments yet); this is a blocking P0 for Windows users relying on the web interface.
  - **[Issue #2435](https://github.com/MoonshotAI/kimi-cli/issues/2435)**

- **#2430 [CLOSED] Auto logged out in the middle of a task**
  - **Why it matters:** Silent mid-task session expiration breaks trust in long-running agent workflows. The user returned to find their session dead.
  - **Community reaction:** Filed against v1.36.0; closed without extensive discussion, but session fragility is a recurring pain point.
  - **[Issue #2430](https://github.com/MoonshotAI/kimi-cli/issues/2430)**

## Key PR Progress
*(6 PRs updated in the last 24h found in the dataset)*

- **#1960 [CLOSED] RalphFlow architecture (ephemeral context + convergence detection)**
  - A significant agent framework overhaul. RalphFlow isolates each iteration in a temporary context, then detects convergence/divergence to prevent infinite loops in multi-step workflows. This addresses one of the loudest feature requests from agent-heavy users.
  - **[PR #1960](https://github.com/MoonshotAI/kimi-cli/pull/1960)**

- **#2434 [OPEN] Fix: suppress MCP connection errors and handle LLM double-serialization**
  - Fixes three issues from heavy MCP usage: noisy connection-drop logs (Notion, code-index servers), LLM tool-call double-serialization, and robust event-loop cleanup.
  - **[PR #2434](https://github.com/MoonshotAI/kimi-cli/pull/2434)**

- **#2429 [OPEN] Fix: prevent idle cursor blink from forcing scroll-to-bottom in Linux terminals**
  - Solves a persistent terminal UX bug where cursor idle events reset the viewport, making long output review impossible without external pagers.
  - **[PR #2429](https://github.com/MoonshotAI/kimi-cli/pull/2429)**

- **#2432 [CLOSED] feat(shell): guide users to upgrade to the new Kimi Code**
  - Implements a soft migration UX: a `/upgrade` command, welcome-screen nudges, and automatic config/session transfer. No forced prompts or sunset countdowns.
  - **[PR #2432](https://github.com/MoonshotAI/kimi-cli/pull/2432)**

- **#2433 [CLOSED] chore(release): bump kimi-cli to 1.47.0**
  - Official release integrating the renaming, migration guidance, and bug fixes.
  - **[PR #2433](https://github.com/MoonshotAI/kimi-cli/pull/2433)**

- **#2431 [CLOSED] docs: rename project to Kimi CLI and link to Kimi Code CLI successor**
  - README and docs overhaul to clearly distinguish the Python CLI from the next-gen tool.
  - **[PR #2431](https://github.com/MoonshotAI/kimi-cli/pull/2431)**

## Feature Request Trends
- **Agent Loop Safety:** The RalphFlow merge (PR #1960) directly answers demands for agents that self-terminate when stuck, rather than burning tokens in infinite loops.
- **Graceful Successor Migration:** The deliberate `/upgrade` command and documentation separation show that the community wants a clear, low-friction path to the new Kimi Code binary.
- **MCP Tooling Hardening:** Developers are pushing the tool hard through MCP integrations; the need for silent reconnection, proper serialization, and error suppression is the top integration-level ask.

## Developer Pain Points
- **WebSocket Reliability (`kimi web`):** The Work tab is completely broken for Windows users due to the Daimon WS daemon failure (Issue #2435). This is the most critical active issue.
- **Session Persistence:** Long-running tasks are prematurely killed by silent session timeouts (Issue #2430), which is a deal-breaker for agentic workflows.
- **MCP Connection Fragility:** Heavy MCP users frequently hit connection drops and double-serialization bugs (PR #2434), indicating the tool layer needs more defensive error handling.
- **Terminal UI Regression:** Linux scroll jumping (PR #2429) is a classic but highly aggravating UX flaw that degrades the reading experience for CLI-native users.
- **Naming Confusion:** The repository rename (PR #2431) is a direct response to community confusion between “Kimi Code CLI” (Python) and “Kimi Code” (Go successor)—the migration bridge is the mitigation strategy.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: 2026-06-06

---

## 1. Today's Highlights

The OpenCode team shipped **v1.16.2** with critical bugfixes, including a guard that prevents reasoning summaries from firing on incompatible providers and tighter edit operation matching to prevent accidental overwrites. On the community side, the **Plan Mode auto-switch** ([#7801](https://github.com/anomalyco/opencode/issues/7801)) and **multi-user web auth** ([#20067](https://github.com/anomalyco/opencode/issues/20067)) feature requests continue to dominate with high upvote counts, signaling strong demand for both workflow automation and enterprise readiness. A significant **service API refactor** ([#31049](https://github.com/anomalyco/opencode/pull/31049)) is underway to lay the groundwork for a more modular server architecture.

---

## 2. Releases

**[v1.16.2](https://github.com/anomalyco/opencode/releases/tag/v1.16.2)** — Hotfix (Last 24h)
- **Reasoning summaries** now only run on providers that support them, avoiding request failures on incompatible backends (e.g., GPT-5).
- **Edit operations** are safer, refusing loose matches that could corrupt existing code or replace files by mistake.
- Fixed **Bedrock sessions** that were hanging indefinitely.

**[v1.16.0](https://github.com/anomalyco/opencode/releases/tag/v1.16.0)**
- Added **managed workspace cloning** that preserves dirty and untracked files.
- Added **moving sessions** between workspaces and directories.
- Added proper **OpenAI model support through AWS Bedrock**.
- Introduced **skill discovery** and file-based agent loading.

---

## 3. Hot Issues

1.  **[#5359 — Unable to read images for some models](https://github.com/anomalyco/opencode/issues/5359)** (15 comments)
    A regression breaking vision capabilities on LiteLLM + Vertex AI backends. Works in v1.0.134 but broken from v1.0.137 onward. High priority for vision workflow users.

2.  **[#29992 — Auto-scroll stops working after manual scroll](https://github.com/anomalyco/opencode/issues/29992)** (👍 15)
    When users scroll up mid-stream and return to the bottom, auto-scroll permanently disables. Widely upvoted UX bug causing significant community frustration.

3.  **[#2047 — LM Studio Failure to refresh models](https://github.com/anomalyco/opencode/issues/2047)** (15 comments)
    A long-standing integration headache. Adding or removing models in LM Studio is not reflected in OpenCode even after `auth logout` / `auth login` cycles.

4.  **[#20067 — [FEATURE] Multi-user auth for opencode web](https://github.com/anomalyco/opencode/issues/20067)** (👍 12)
    Enterprise cornerstone request. Deploying OpenCode on shared servers requires per-user provider credentials and authentication isolation.

5.  **[#7801 — [FEATURE] Plan Mode auto-switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)** (👍 18)
    The most upvoted open feature request. Users want Plan Mode to automatically transition to Build Mode after the plan is approved, closing the "ask vs. do" workflow gap.

6.  **[#12716 — Doom loop not caught during reasoning](https://github.com/anomalyco/opencode/issues/12716)** (8 comments)
    Infinite loops slip undetected when they occur during the thinking/reasoning phase, wasting tokens and time.

7.  **[#20234 — WSL output formatting bug](https://github.com/anomalyco/opencode/issues/20234)** (👍 4)
    Under WSL, the TUI outputs one word per line during the thinking phase, severely degrading readability for Windows/Linux subsystem users.

8.  **[#22233 — Improve subagent runtime visibility](https://github.com/anomalyco/opencode/issues/22233)** + **[#23784 — Subagent status in TUI footer](https://github.com/anomalyco/opencode/issues/23784)**
    A cluster of requests asking for clear indication of which agents are running, what they are doing, and how long they've been executing.

9.  **[#30545 — Desktop File Tree not working](https://github.com/anomalyco/opencode/issues/30545)** (6 comments)
    A significant Desktop-mode UI regression in v1.15.13 where enabling the File Tree in Advanced settings has no effect.

10. **[#31009 — Bring back `//` for `/new`](https://github.com/anomalyco/opencode/issues/31009)** (3 comments)
    A quick UX regression in the latest versions. The `//` shortcut was remapped to `/models`, breaking a well-established muscle memory for creating new sessions.

---

## 4. Key PR Progress

1.  **[#31049 — refactor(server): canonicalize service API](https://github.com/anomalyco/opencode/pull/31049)**
    A major architecture refactor by `thdxr` that promotes the experimental server API to stable, standardizing route groups, authorization, and session-location middleware.

2.  **[#29217 — feat(tui): Add inline `$skill` invocations](https://github.com/anomalyco/opencode/pull/29217)**
    A massive TUI enhancement closing 5 issues. Brings skill autocompletion and execution directly into the prompt composer with a dedicated "SKILL" pill UI.

3.  **[#31054 — feat(opencode): support non-interactive MCP add](https://github.com/anomalyco/opencode/pull/31054)**
    Provides first-class CLI support for registering MCP servers entirely through arguments, enabling scripting and CI/CD workflows for tool configuration.

4.  **[#30970 — feat(skill): add skill enable/disable toggle](https://github.com/anomalyco/opencode/pull/30970)**
    Introduces granular control over skills via HTTP API (`POST /skill/:name/toggle`), TUI dialog, and persistent configuration to `skills.json`.

5.  **[#31052 — fix(provider): keep compacted Anthropic tool histories user-led](https://github.com/anomalyco/opencode/pull/31052)**
    Critical API compliance fix. After compaction or import, Anthropic could receive histories starting with an assistant message, which the API rejects.

6.  **[#31050 — fix(core): omit unavailable host tools](https://github.com/anomalyco/opencode/pull/31050)**
    Improves robustness by cleanly removing unavailable built-in and application tools before prompting, preventing downstream errors.

7.  **[#31043 — fix(core): settle owned process output](https://github.com/anomalyco/opencode/pull/31043)**
    Enhances child process lifecycle management, closing owned pipes and preventing orphaned "zombie" processes and lost output.

8.  **[#30977 — feat(tui): attach to configured server by default](https://github.com/anomalyco/opencode/pull/30977)**
    Simplifies the server connection workflow with a new `server.attach` config value. Closes #17322 with ~40% diff dedicated to test coverage.

9.  **[#28592 — fix(cli): handle OSC52 clipboard properly under GNU screen](https://github.com/anomalyco/opencode/pull/28592)**
    Community-contributed fix for a long-standing bug where clipboard passthrough used tmux DCS format incorrectly under GNU Screen.

10. **[#30242 — fix(desktop): allow choosing Windows install directory](https://github.com/anomalyco/opencode/pull/30242)**
    Switches the Windows NSIS installer from one-click mode to an assisted installer flow, resolving installation path constraints.

---

## 5. Feature Request Trends

- **Enterprise Readiness:** Requests for **multi-user authentication** ([#20067](https://github.com/anomalyco/opencode/issues/20067)) and **automated plan/build mode workflows** ([#7801](https://github.com/anomalyco/opencode/issues/7801)) indicate a clear shift toward team-based and CI-level usage.
- **Multi-Agent UX:** A strong desire for **subagent visibility** ([#22233](https://github.com/anomalyco/opencode/issues/22233), [#23784](https://github.com/anomalyco/opencode/issues/23784)) and better session navigation (page-based browsing [#26327](https://github.com/anomalyco/opencode/issues/26327)).
- **Skill System Expansion:** Users are eager to fully leverage the new skill framework, asking for **inline invocation** (addressed by [#29217](https://github.com/anomalyco/opencode/pull/29217)) and **granular enable/disable controls** (addressed by [#30970](https://github.com/anomalyco/opencode/pull/30970)).
- **Scriptable Configuration:** There is a clear push toward **non-interactive MCP registration** ([#29827](https://github.com/anomalyco/opencode/issues/29827), [#31054](https://github.com/anomalyco/opencode/pull/31054)), alongside calls for **custom provider vision support** ([#8875](https://github.com/anomalyco/opencode/issues/8875)).

---

## 6. Developer Pain Points

- **Vision Reliability:** Persistent issues with image reading across different models and backends ([#5359](https://github.com/anomalyco/opencode/issues/5359)) are a critical blocker for multimodal workflows.
- **Cost Control Gaps:** "Doom loops" evading detection during reasoning ([#12716](https://github.com/anomalyco/opencode/issues/12716), [#25254](https://github.com/anomalyco/opencode/issues/25254)) represent a significant drain on API credits, making better loop detection a top reliability priority.
- **Context & State Management:** Users struggle with subagent opacity, session history migration bugs between platforms ([#29799](https://github.com/anomalyco/opencode/issues/29799)), and orphan processes consuming memory ([#13001](https://github.com/anomalyco/opencode/issues/13001)).
- **Platform Parity:** WSL rendering issues ([#20234](https://github.com/anomalyco/opencode/issues/20234)), GNU Screen clipboard incompatibility ([#28590](https://github.com/anomalyco/opencode/issues/28590)), and Windows installation limitations ([#30242](https://github.com/anomalyco/opencode/pull/30242)) create friction for users outside the primary macOS target.
- **UI/UX Regressions:** Recent releases have introduced sharp regressions, most notably the auto-scroll breaking ([#29992](https://github.com/anomalyco/opencode/issues/29992)) and the `/` keybinding change ([#31009](https://github.com/anomalyco/opencode/issues/31009)), causing immediate community backlash and highlighting the need for a stronger regression test suite.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-06

## Today’s Highlights
The community saw a flurry of activity with **39 issues and 12 pull requests** updated in the last 24 hours, but **session stability remains the dominant theme**. The most urgent conversation is **#4945** (53 comments), where `openai-codex` leaves the TUI stuck on “Working…” with no recovery path short of aborting the turn. On the infrastructure front, a new **Anthropic Vertex provider** ([#5262](https://github.com/earendil-works/pi/pull/5262)) and a **multi-agent workflow extension** ([#5426](https://github.com/earendil-works/pi/pull/5426)) landed, signalling a strong push toward enterprise deployment and agent orchestration. Meanwhile, the recurring `"Cannot continue from message role: assistant"` crash (**#5420**, **#5445**) is drawing sharp attention as a stability bottleneck for long-running sessions.

## Releases
No new releases were published in the last 24 hours.

## Hot Issues
*Pick of 10 noteworthy issues, why they matter, and community reaction.*

1.  **[#4945](https://github.com/earendil-works/pi/issues/4945) ** `openai-codex` can hang on “Working…” with zero-usage aborted turns**
    *53 comments | 👍28*  
    The highest-engagement issue by a wide margin. The interactive TUI becomes completely unresponsive during a turn, forcing the user to press Escape (recording an aborted turn). Community discussion points to a race condition in the streaming/response handler. A high-severity UX regression.

2.  **[#2023](https://github.com/earendil-works/pi/issues/2023) ** Add `pi.runWhenIdle()` to schedule work after the agent has fully settled**
    *12 comments | 👍5*  
    A long-standing extension API request. Extension authors want a reliable lifecycle hook to run logic (e.g., tool queue flushing, reloading runtime) *after* the agent finishes thinking. The conversation shows frustration with the current `sendUserMessage({ deliverAs: "followUp" })` workaround.

3.  **[#3715](https://github.com/earendil-works/pi/issues/3715) ** `local-llm` streams terminate at 5 min from `undici` default `bodyTimeout`**
    *9 comments | 👍3*  
    Deeply technical but high impact for local-model users. Long `Write` tool calls to vLLM/Qwen3 die with `UND_ERR_BODY_TIMEOUT`. The `retry.provider.timeoutMs` cannot override the underlying HTTP client cap. Closed after a fix, but the conversation exposed a painful limitation for power users.

4.  **[#4180](https://github.com/earendil-works/pi/issues/4180) ** Links not clickable anymore**
    *8 comments*  
    A regression introduced during the coding-agent terminal mode refactor. Full URLs and Markdown links render as plain text, breaking one of the core interactive TUI flows. The community reaction was swift, and the issue was closed quickly, but it highlights the fragility of the terminal rendering layer.

5.  **[#3442](https://github.com/earendil-works/pi/issues/3442) ** Support WebSocket transport in `openai-responses`**
    *7 comments*  
    Demand is building for WebSocket transport on the general API endpoint. Currently only the ChatGPT subscription path has WebSocket support. This is a blocker for latency-sensitive and streaming-heavy workflows.

6.  **[#5384](https://github.com/earendil-works/pi/issues/5384) ** DeepSeek via OpenRouter still sends `role: "developer"` after #1048**
    *3 comments*  
    The fix for DeepSeek’s `developer` role rejection only matched the direct API endpoint. Users routing through OpenRouter or other OpenAI-compatible proxies hit the exact same rejection. A cautionary tale about proxy compatibility coverage.

7.  **[#5188](https://github.com/earendil-works/pi/issues/5188) ** `shift+enter` submits and does not create a new line**
    *5 comments | 👍2*  
    A configuration-parsing bug where `shift+enter` is bound to `newLine` but still triggers submission. Small in scope but repeatedly cited by users relying on custom keybindings for coding workflows.

8.  **[#5389](https://github.com/earendil-works/pi/issues/5389) ** macOS Speech-to-text breaks/freezes pi during a workload**
    *3 comments*  
    Using the macOS “STT” option while pi is “Working” freezes the TUI (though the agent continues in the background). Signals a deeper issue with how the TUI handles concurrent system input modalities.

9.  **[#5265](https://github.com/earendil-works/pi/issues/5265) ** `pi -p “query”` doesn’t exit after printing the answer**
    *2 comments*  
    A basic pipe-mode regression: `pi -p` holds the terminal instead of returning to shell prompt. Critical for scripting and CI integration. Closed but raised by multiple users.

10. **[#5420](https://github.com/earendil-works/pi/issues/5420) ** Auto-compaction crashes with `Cannot continue from message role: assistant`**
    *2 comments | 👍3*  
    A crash triggered when compaction leaves an `assistant`-role message at the end of the context. The follow-up `agent.continue()` throws fatally. High community signal (👍3) relative to comments, indicating many others hit this silently. Directly related to the retry crash in **#5445**.

## Key PR Progress
*Pick of 10 important pull requests, describing features or fixes.*

1.  **[#5442](https://github.com/earendil-works/pi/pull/5442) ** `@pi-mono/self-evolver` — 5D gene/genome equivalent**
    *Merged*  
    An experimental package positioning the existing “5D memory” system as a genome substrate for self-evolving agents. Controversial in approach (no parallel skill pool), but signals a strong research-direction bet on meta-cognitive tooling.

2.  **[#5426](https://github.com/earendil-works/pi/pull/5426) ** Workflow extension for multi-agent orchestration**
    *Merged*  
    A substantial API addition: `AgentStep` execution (single/parallel/chain), a context firewall (summaries to main LLM, full results in tool details), and subagent refactoring. This is the nearest thing to native agent delegation in the current codebase.

3.  **[#5262](https://github.com/earendil-works/pi/pull/5262) ** Add Anthropic Vertex provider**
    *Open*  
    A thin adapter wrapping the `AnthropicVertex` SDK client and reusing the existing Anthropic streaming path. Represents a concrete push into enterprise GCP deployments.

4.  **[#5437](https://github.com/earendil-works/pi/pull/5437) ** Fix `SUMMARIZATION_SYSTEM_PROMPT` for non-coding agents**
    *Merged*  
    Replaces the hardcoded “AI coding assistant” string with the neutral “AI assistant” in the summarization prompt. Catches an important bias that skewed compaction behavior for general-purpose agent use cases.

5.  **[#5435](https://github.com/earendil-works/pi/pull/5435) ** Validate LLM messages after extension transforms**
    *Merged*  
    A defensive fix: extensions modifying messages via the `context` hook can produce invalid sequences (e.g., `toolResult` without preceding `toolUse`). Now caught early instead of surfacing as opaque provider errors (e.g., MiniMax error 2013).

6.  **[#5434](https://github.com/earendil-works/pi/pull/5434) ** Fix(edit): tolerate extraneous keys in `edits[]`**
    *Merged*  
    Drops `additionalProperties: false` on the edit tool’s inner schema. Weak/messy models sometimes emit extra keys in JSON tool calls, and this change gracefully ignores them instead of rejecting the turn.

7.  **[#5429](https://github.com/earendil-works/pi/pull/5429) ** Fix models JSON migration error path**
    *Merged*  
    Catches `JSON.parse` errors during `models.json` migration and surfaces the resolved file path. Previously raw stack traces leaked to users on corrupted config files.

8.  **[#5332](https://github.com/earendil-works/pi/pull/5332) ** Approval system for workspaces**
    *Open*  
    Introduces `.pi.user` as a separate folder and requires user approval for interactive loads. An important step toward a trust/security model for workspace extensions, though still needing further iteration.

9.  **[#5385](https://github.com/earendil-works/pi/pull/5385) ** First-run terminal theme detection**
    *Open*  
    Queries the terminal with OSC escape codes to detect light/dark theme and persists the setting. A small but concrete UX polish for onboarding.

10. **[#5439](https://github.com/earendil-works/pi/pull/5439) ** Export coding-agent package path helpers**
    *Merged*  
    Exposes `getPackageDir()`, `getReadmePath()`, `getDocsPath()`, and `getExamplesPath()` from the coding-agent public API. Directly unblocks extension developers who previously had to import from internal paths.

## Feature Request Trends
*Distilled from the full set of issues updated this week.*

- **Multi-Agent & Workflow Orchestration:** Strong momentum behind native agent delegation. The workflow extension ([#5426](https://github.com/earendil-works/pi/pull/5426)), `runWhenIdle()` ([#2023](https://github.com/earendil-works/pi/issues/2023)), and the self-evolver concept ([#5442](https://github.com/earendil-works/pi/pull/5442)) all point toward a desire for structured, parallel agent composition rather than monolithic turns.

- **Provider Diversity & Protocol Modernisation:** WebSocket transport is the single most requested protocol feature ([#3442](https://github.com/earendil-works/pi/issues/3442), [#5446](https://github.com/earendil-works/pi/issues/5446)). There is also rising demand for proxy provider compatibility (OpenRouter, Fireworks aliases) and enterprise providers like Vertex.

- **Extension API Parity & Lifecycle Access:** Extension authors are pushing for full access to session management methods (`waitForIdle`, `fork`, `navigateTree`) from all context types ([#5443](https://github.com/earendil-works/pi/issues/5443), [#5448](https://github.com/earendil-works/pi/issues/5448)), not just slash command handlers. The current API surface forces awkward workarounds.

- **Image / Vision Attachment Support:** Multiple requests converge on the need to attach images (`clipboard paste`, `CLI file attachment`) to the model request, reflecting the growing adoption of multimodal vision models (Gemma4, etc.) ([#5279](https://github.com/earendil-works/pi/issues/5279), [#5438](https://github.com/earendil-works/pi/issues/5438)).

- **Security & Governance:** A new wave of requests around declarative permission systems, ability to exclude built-in tools, and workspace approval flows ([#4459](https://github.com/earendil-works/pi/issues/4459), [#5447](https://github.com/earendil-works/pi/issues/5447), [#5332](https://github.com/earendil-works/pi/pull/5332)). The ecosystem is beginning to treat the agent as a shared/non-trivial part of the development infrastructure.

- **TUI & Rendering Configuration:** Users want control over output padding, expand hints, and terminal theme matching ([#5436](https://github.com/earendil-works/pi/issues/5436), [#5385](https://github.com/earendil-works/pi/pull/5385), [#5359](https://github.com/earendil-works/pi/issues/5359)). The TUI is increasingly seen as a render surface that should respect user preferences.

## Developer Pain Points
*Recurring frustrations and high-frequency friction clusters.*

- **Session Stability Crisis:** The `"Cannot continue from message role: assistant"` crash is the #1 stability pain point. It surfaces both during `auto-compaction` ([#5420](https://github.com/earendil-works/pi/issues/5420)) and `_prepareRetry` ([#5445](https://github.com/earendil-works/pi/issues/5445)), killing long-running sessions and breaking trust in the persistence layer.

- **TUI Responsiveness & Input Handling:** The interactive terminal remains a major source of friction. The “Working…” hang with Codex ([#4945](https://github.com/earendil-works/pi/issues/4945)), freezes from macOS STT ([#5389](https://github.com/earendil-works/pi/issues/5389)), crash-on-wide-lines ([#5422](https://github.com/earendil-works/pi/issues/5422)), and keybinding failures ([#5188](https://github.com/earendil-works/pi/issues/5188)) collectively erode the “it just works” expectation for a local TUI app.

- **Model Provider Edge Cases:** Running local models (vLLM, Qwen) hits hard timeouts ([#3715](https://github.com/earendil-works/pi/issues/3715)). Using proxies like OpenRouter exposes missing `role: developer` filters ([#5384](https://github.com/earendil-works/pi/issues/5384)). Anthropic signature validation can be broken by internal string sanitization ([#5416](https://github.com/earendil-works/pi/issues/5416)). Each provider integration feels incomplete at the edges.

- **Extension Development Friction:** Async callbacks in extensions are dropped when `pi -p` exits ([#5423](https://github.com/earendil-works/pi/issues/5423)). Extension-loaded packages like `pi-fancy-loader` incorrectly flag as perpetually updatable ([#5388](https://github.com/earendil-works/pi/issues/5388)). Internal helpers that would unlock extension features remain unexported ([#5415](https://github.com/earendil-works/pi/issues/5415)). The extension developer experience still lags behind the core tool’s pace.

- **Regressions in Basic CLI UX:** Pipe mode not exiting ([#5265](https://github.com/earendil-works/pi/issues/5265)), clipboard image paste inserting only a temp file path ([#5438](https://github.com/earendil-works/pi/issues/5438)), and directory navigation resets (`cd` not persisting, [#5419](https://github.com/earendil-works/pi/issues/5419)) — each of these broke a simple expectation, indicating test coverage gaps in the rapid development cycle.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-06

## 1. Today's Highlights
The project is in the thick of its **Daemon Mode integration wave** (#4490), rapidly closing parity gaps between the CLI and the web-shell HTTP server. A **critical OOM regression** (#4815) tied specifically to `qwen --resume` has been filed as a P1, leaving the Escape key completely non-functional—urgent attention is needed for session stability. On the feature front, PRs landed to bring session forking (#4812), rewind (#4820), and full memory commands (#4819) to HTTP clients, while a strong **community push for a dedicated `web_search` tool** (#4801) signals growing agentic usage patterns.

---

## 2. Releases
- **v0.17.1-nightly.20260606.16c1d9a5a**: Nightly build scoped from the `v0.17.1` release branch. The single highlight is a **CLI fix that skips thought parts in copy output** (by `he-yufeng`), cleaning up clipboard content when copying model responses that include chain-of-thought reasoning. Standard CI automation via `qwen-code-ci-bot`.

---

## 3. Hot Issues
1. **#4815 – Severe OOM with `qwen --resume` & Escape key broken** (P1)  
   A 100% reproducible crash. Using `--resume` triggers rapid memory exhaustion, and the Escape key becomes completely non-functional until the process is killed. The top urgency item today.  
   [https://github.com/QwenLM/qwen-code/issues/4815](https://github.com/QwenLM/qwen-code/issues/4815)

2. **#4514 – Daemon capability gaps & prioritized backlog**  
   The master tracking ticket for every missing feature on the `qwen serve` HTTP/SSE surface. Covers rewind, session branching, settings management, and slash command support. Defines the v0.16-alpha roadmap.  
   [https://github.com/QwenLM/qwen-code/issues/4514](https://github.com/QwenLM/qwen-code/issues/4514)

3. **#4801 – Request: dedicated `web_search` tool**  
   Strong community sentiment for a tool that performs actual Google/Search queries rather than relying on the model to guess URLs. Current `web_fetch` is insufficient for open-ended research tasks.  
   [https://github.com/QwenLM/qwen-code/issues/4801](https://github.com/QwenLM/qwen-code/issues/4801)

4. **#4802 – `qwen3.7-plus` should support multimodal input**  
   The Plus model supports image/video input, but the `defaultModalities()` regex detection in `modalityDefaults.ts` falls through to text-only. A complementary fix PR (#4803) is already open.  
   [https://github.com/QwenLM/qwen-code/issues/4802](https://github.com/QwenLM/qwen-code/issues/4802)

5. **#4777 – Deferred MCP tools bust the prompt cache on every discovery**  
   Progressive MCP tool discovery invalidates the entire system prompt cache each time the set changes, causing significant latency overhead for MCP-heavy workflows.  
   [https://github.com/QwenLM/qwen-code/issues/4777](https://github.com/QwenLM/qwen-code/issues/4777)

6. **#4813 – Shared `baseUrl` cannot be set once for multiple models**  
   Each model in `modelProviders` must duplicate the `baseUrl` even when pointing to the same local endpoint (e.g., vLLM). DRY violation increases configuration friction.  
   [https://github.com/QwenLM/qwen-code/issues/4813](https://github.com/QwenLM/qwen-code/issues/4813)

7. **#4794 – Compact mode tool merge causes full-screen flash**  
   Ink/React full re-render when `mergeCompactToolGroups` shrinks the history array. Creates a distracting visual stutter on every tool batch.  
   [https://github.com/QwenLM/qwen-code/issues/4794](https://github.com/QwenLM/qwen-code/issues/4794)

8. **#3384 – Unable to add OpenAI-compatible local LLM**  
   Persistent documentation/config friction for users trying to connect local or third-party endpoints via `settings.json`. Multiple comments show differing failure modes.  
   [https://github.com/QwenLM/qwen-code/issues/3384](https://github.com/QwenLM/qwen-code/issues/3384)

9. **#4814 – UI should make it easier for Custom Provider users to add new models**  
   The initial setup wizard works well, but there is no post-setup UI to add/edit models. Users currently have to hand-edit JSON.  
   [https://github.com/QwenLM/qwen-code/issues/4814](https://github.com/QwenLM/qwen-code/issues/4814)

10. **#4791 – Tool validation fails when parameters contain valid JSON strings**  
    `SchemaValidator` incorrectly parses JSON string literals as nested objects. Breaks `write_file` and `edit` when generating code containing JSON structures.  
    [https://github.com/QwenLM/qwen-code/issues/4791](https://github.com/QwenLM/qwen-code/issues/4791)

---

## 4. Key PR Progress
1. **#4490 – Merge daemon-mode feature batch into main**  
   The integration merge of `daemon_mode_b_main`. 46 commits across 386 files (+115k LOC). Represents the core feature set for v0.16-alpha. Open for final review.  
   [https://github.com/QwenLM/qwen-code/pull/4490](https://github.com/QwenLM/qwen-code/pull/4490)

2. **#4820 – HTTP rewind endpoints**  
   Adds `GET /session/:id/rewind/snapshots` and `POST /session/:id/rewind` to the daemon. Allows web-shell and SDK clients to rewind conversations programmatically (#4514 T3.2).  
   [https://github.com/QwenLM/qwen-code/pull/4820](https://github.com/QwenLM/qwen-code/pull/4820)

3. **#4812 – Session forking via `POST /session/:id/branch`**  
   Remote clients can now fork a live session's JSONL transcript without history replay. Enables experiment branching in the web shell.  
   [https://github.com/QwenLM/qwen-code/pull/4812](https://github.com/QwenLM/qwen-code/pull/4812)

4. **#4816 – Full-stack `/settings` for web-shell**  
   Daemon API (`GET/POST /workspace/settings`), SDK client methods, React `useSettings` hook, and `settings_changed` event wiring. A massive UX upgrade for the web shell.  
   [https://github.com/QwenLM/qwen-code/pull/4816](https://github.com/QwenLM/qwen-code/pull/4816)

5. **#4819 – Enable `/remember`, `/forget`, `/dream` in ACP mode**  
   Adds `supportedModes: ['interactive', 'acp']` to memory slash commands, unblocking them for web-shell users. Includes error handling improvements in `/forget`.  
   [https://github.com/QwenLM/qwen-code/pull/4819](https://github.com/QwenLM/qwen-code/pull/4819)

6. **#4736 – ACP/REST parity wave 1**  
   Closes 24 `_qwen/*` HTTP extension methods, achieving near-complete REST parity for the `/acp` transport. Depends on the `DaemonWorkspaceService` refactoring (#4563).  
   [https://github.com/QwenLM/qwen-code/pull/4736](https://github.com/QwenLM/qwen-code/pull/4736)

7. **#4798 – Inject current date on every user query**  
   Prevents stale temporal context in long-running sessions by injecting the current date/time as a system reminder on *every* UserQuery turn, not just at session start.  
   [https://github.com/QwenLM/qwen-code/pull/4798](https://github.com/QwenLM/qwen-code/pull/4798)

8. **#4803 – Multimodal support for `qwen3.7-plus`**  
   Fixes the modality detection regex to recognize Plus models as multimodal, matching Model Studio naming conventions. Corresponds to Issue #4802.  
   [https://github.com/QwenLM/qwen-code/pull/4803](https://github.com/QwenLM/qwen-code/pull/4803)

9. **#4793 – Coerce non-string tool params to strings for self-hosted LLMs**  
   Self-hosted models (vLLM, LMStudio, sglang) sometimes return booleans/numbers for tool parameters. This PR adds coercion to prevent `SchemaValidator` rejection of `write_file`/`edit`.  
   [https://github.com/QwenLM/qwen-code/pull/4793](https://github.com/QwenLM/qwen-code/pull/4793)

10. **#2838 – Bun runtime support**  
    Long-running open PR adding native Bun support for faster startup (3–5x) and lower memory usage. A draft aimed at performance-sensitive deployments.  
    [https://github.com/QwenLM/qwen-code/pull/2838](https://github.com/QwenLM/qwen-code/pull/2838)

---

## 5. Feature Request Trends
- **Daemon & Web Shell Feature Parity**: The single most active area. The community wants every major CLI interactive feature (session branching, rewind, memory commands, settings) available in the HTTP API. Issues #4514, #4809, and several PRs (#4812, #4816, #4819, #4820) are converging on this goal.
- **Autonomous Web Search**: The demand for a genuine `web_search` tool (#4801) reflects a shift toward treating the tool as an agentic research assistant, not just a chat wrapper.
- **Model Configuration Usability**: Multiple threads (#3384, #4813, #4814) call for smarter, less JSON-brittle configuration—shared `baseUrl`, UI-based model management, and automatic modality detection.
- **Performance Optimization**: Requests for Bun support (#2838), daemon cold start reduction (#4748), and MPC cache fixes (#4777) show an ops/perf-conscious user base dealing with real production scaling pains.

---

## 6. Developer Pain Points
- **Session Memory Instability**: The OOM on `--resume` (#4815) is the top stability concern. Combined with prompt cache busting on MCP discovery (#4777), developers running long-lived or tool-dense sessions are hitting reliability walls.
- **Local Model Interoperability Friction**: Configuring and using self-hosted LLMs remains painful. `modelProviders` is verbose (#4813), tool validation is too strict for local models (#4791, #4793), and the absence of a post-setup UI (#4814) forces manual JSON editing.
- **TUI Responsiveness Regressions**: The compact mode flash (#4794) and complete Escape key failure (#4815) demonstrate that the Ink/React rendering layer struggles with dynamic session state, introducing UI breakage alongside feature additions.
- **Tool Parameter Strictness**: Self-hosted models that don't perfectly enforce string typing on tool parameters cause silent failures. Users are forced to debug schema validation errors rather than fixing model output issues, creating a poor developer experience for the self-hosted community.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest – 2026-06-06

**Project Link:** [https://github.com/Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)

---

## 1. Today's Highlights

This week's activity is dominated by the **v0.9.0 “stewardship” cycle**, with major foundational PRs merging for the **VS Code extension scaffold** (Agent View, local runtime) and the **WhaleFlow** runtime (typed workflow config, trace store schema migration). Community feature requests strongly coalesce around **IDE integration** and **provider fallback automation**, while critical bugs like MCP tool name parsing with underscores and CLI syntax deprecations were resolved. The HarmonyOS port also gained meaningful traction with an active contributor driving compilation fixes upstream.

---

## 2. Releases

*No new releases were published in the last 24 hours.*

---

## 3. Hot Issues

The following 10 issues represent the most impactful or active discussions in the community today:

**#2766** – [UI Refactor Needed (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2766)
*Author: mo-vic* | 8 comments
The output is hard to copy and confirmation pop-ups obscure the main interface while showing low-value information. High engagement signals broad agreement that the modal UX needs urgent attention.

**#1264** – [[enhancement] VS Code Plugin Request (OPEN)](https://github.com/Hmbown/CodeWhale/issues/1264)
*Author: mangdehuang* | 6 comments
Consistent, popular request for an OpenCode-like IDE plugin. Screenshots show a strong preference for GUI interaction over pure TUI for coding tasks.

**#2621** – [[enhancement] Xiaomi MiMo Token Plan API (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2621)
*Author: springeye* | 4 comments
The existing pay-as-you-go MiMo provider works, but Xiaomi’s new tiered subscription model (Lite/Standard/Pro/Max) is not supported. Users tracking costs closely want this endpoint support.

**#2574** – [[enhancement] Provider Fallback Chain (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2574)
*Author: hsdbeebou* | 3 comments
Proposes a `fallback_providers` `toml` configuration to auto-switch providers on 401/429/5xx errors. This is a recurring complaint about workflow interruptions.

**#2580** – [[enhancement] VS Code Agent View Adaptation (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2580)
*Author: AiurArtanis* | 3 comments
Proposes native adaptation of VS Code’s new Agent View canvas rather than forcing a terminal workflow. Closely tied to the v0.9 roadmap.

**#2791** – [[enhancement] Modular Command Dispatch (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2791)
*Author: aboimpinto* | 1 comment
A structural improvement request to replace the ~200-line monolithic `match` block in command dispatch with a strategy pattern. Reflects increasing maintenance complexity.

**#2787** – [[bug] TUI Status Bar MCP Count Error (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2787)
*Author: yekern* | 1 comment
Filed against the `v0.9.0-stewardship` branch. The status bar miscounts MCP servers when both global and project-level configs are present.

**#1584** – [[enhancement] Claude Code-level IDE Plugin (OPEN)](https://github.com/Hmbown/CodeWhale/issues/1584)
*Author: nasus9527* | 2 comments
A straightforward request for an IDE plugin matching the quality of Claude Code’s native integration. Reinforces the dominant IDE trend.

**#2709** – [[v0.9.0] Hugging Face MCP Hub Integration (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2709)
*Author: Hmbown* | 1 comment
Parent tracking ticket for making the official Hugging Face MCP server easy to discover and configure inside CodeWhale.

**#2625** – [[bug/enhancement] Port to HarmonyOS / OpenHarmony (OPEN)](https://github.com/Hmbown/CodeWhale/issues/2625)
*Author: shenjackyuanjie* | 3 comments
Active contributor debugging the `nix` -> `ioctl` dependency chain for `aarch64-linux-ohos` target. Has an active companion PR (#2634).

---

## 4. Key PR Progress

**#2816** – [WhaleFlow Trace Store Schema Migration (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2816)
*Author: Hmbown*
Adds state-store v2 migration for WhaleFlow trace tables (workflow, branch, leaf, control-node, teacher-candidate). Core persistence infrastructure for v0.9.0.

**#2814** – [VS Code Read-Only Agent View Preview (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2814)
*Author: Hmbown*
Adds an Agent View section to the VS Code extension panel, fetching runtime thread summaries from `/v1/threads/summary`. Immutable rendering, update/retry/undo controls left for later phases.

**#2811** – [VS Code Local Runtime Extension Scaffold (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2811)
*Author: Hmbown*
Phase 0 scaffold for the official extension: commands to open CodeWhale/start `codewhale serve --http`, activity view, status bar state, and VSIX packaging metadata.

**#2810** – [WhaleFlow Typed Workflow Foundation (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2810)
*Author: Hmbown*
Introduces the `codewhale-whaleflow` crate with typed `WorkflowConfig`, `Phase`, `Task`, and `FailurePolicy`. Fully behind a Rust-native IR boundary with no TUI registry wiring yet.

**#2486** – [WhaleFlow Cost Tracking (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2486)
*Author: AdityaVG13*
Adds `tokens_used` and `cost_usd` fields to `SubAgentResult`. Enables cost-per-agent display in the TUI agents pane.

**#2639** – [POST /v1/sessions API Endpoint (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2639)
*Author: gaord*
Allows saving a thread as a session for cross-workspace resumption. Critical for GUI workflows where sessions are the primary persistence mechanism.

**#2634** – [HarmonyOS / OpenHarmony Port (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2634)
*Author: shenjackyuanjie*
Uses `cfg` exclusion blocks on Linux-specific syscalls to target `aarch64-linux-ohos`. Blocked upstream on the `nix` crate’s `ioctl` mismatch.

**#2579** – [Replace Session.messages with AppendLog (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2579)
*Author: encyc*
Phase 4 of the AppendLog backing store project. Replaces `Vec<Message>` with an `AppendLog` wrapper implementing `Deref`/`DerefMut` for zero-impact integration.

**#2239** – [i18n Phase 1-4b UI Wiring (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2239)
*Author: gordonlu*
Wires `MessageId` translations into actual UI surface across 47 files (+1,059 lines). Fixes 109 compile errors after upstream rebase.

**#1893** – [Per-Provider TLS Verification Toggle (OPEN)](https://github.com/Hmbown/CodeWhale/pull/1893)
*Author: wavezhang*
Scopes `insecure_skip_tls_verify` per-provider rather than globally. Only affects the LLM API client, leaving other HTTP clients secure. High value for enterprise proxy setups.

---

## 5. Feature Request Trends

Several broad themes have emerged from the issue tracker:

- **IDE Integration (Dominant Trend):** The most requested feature direction is a native GUI or IDE extension (Issues #1264, #461, #1584, #2580). The community consistently describes the TUI as ill-suited for writing code, explicitly requesting parity with Claude Code or OpenCode.
- **Provider & API Resilience:** Multi-provider setups introduce friction. Demand is high for automatic fallback chains on error (#2574), configurable API endpoint paths (#1874), and clearer authentication failure diagnostics (#2665).
- **Cost & Usage Transparency:** Users actively track API spending. Requests for Xiaomi Token Plan support (#2621) and visible model pricing in the UI (#2731) indicate a desire to avoid bill shock.
- **Platform Expansion:** Beyond Linux/macOS, there is momentum for Windows (launcher assets, release pipeline in #2382) and HarmonyOS/OpenHarmony (#2625 / #2634).
- **Scalability & Stabilization:** Architectural improvements like modular command dispatch (#2791) and the AppendLog backing store (#2579) reflect the project maturing past its initial prototype phase.

---

## 6. Developer Pain Points

- **Manual Provider Failover:** The lack of automatic fallback chains forces users to run `/provider` commands manually when quotas expire or APIs return 429s (Issue #2574).
- **Uninformative Auth Errors:** Generic "invalid API key" messages obscure which provider endpoint or key source failed in a multi-provider config (Issue #2665).
- **TUI Friction for Coding:** Hard-to-select output text, pop-ups that obscure the interface, and the inherent limitations of a terminal UI are frequent frustrations when the primary task is writing code (Issues #2766, #1584).
- **MCP Tool Name Parsing:** Underscores in MCP server names break the internal `split_once('_')` parser, causing tool calls to route to the wrong server (Issue #2744).
- **State Locks on Provider Switch:** Switching providers (e.g., DeepSeek → Kimi → DeepSeek) can leave the agent in an unrecoverable authentication failure state requiring a full restart (Issue #2754).
- **Unconfigurable Timeouts:** Default 300-second timeouts on streaming prompts cannot be adjusted, breaking users with local or slow model providers (Issue #2365).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*