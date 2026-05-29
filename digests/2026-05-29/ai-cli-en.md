# AI CLI Tools Community Digest 2026-05-29

> Generated: 2026-05-29 02:54 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-05-29

---

## 1. Ecosystem Overview

The AI CLI tools market is caught between aggressive feature expansion and foundational reliability crises. Claude Code’s bleeding-edge Dynamic Workflows and Opus 4.8 support triggered a severe session-serialization meltdown, while Gemini CLI is fundamentally compromised by `node-pty` terminal crashes. A common thread is the struggle for Windows parity—almost every tool reports critical platform-specific bugs—and the industry is converging on MCP/ACP protocols as the standard for composability, yet implementation maturity varies dramatically. Session state management has emerged as the single most catastrophic failure vector this week, underscoring that the industry is still learning how to safely serialize the reasoning traces of autonomous agents.

---

## 2. Activity Comparison

| Tool | Top Issue Theme | Issue Volume | PR Count (24h) | Release Status |
|---|---|---|---|---|
| **Claude Code** | Session bricking (thinking block serialization), hotfix regression | 10 hot, 200+ comments | 7 | v2.1.156 hotfix / v2.1.154 feature |
| **OpenAI Codex** | Windows sandbox `spawn setup refresh` failure | 10 hot | 10 | rust-v0.135.0 stable + alpha |
| **Gemini CLI** | `ioctl(2) EBADF` crashes, cross-user data leak | 10 hot (multi-P1) | 10 | v0.44.1 stable + v0.45 preview |
| **Copilot CLI** | CAPI 400 “Duplicate item found” errors | 10 noteworthy | 0 (3 rapid patches) | v1.0.56-1 / v1.0.56-0 / v1.0.55 |
| **Kimi Code CLI** | Export crash, strategic project-split anxiety | 8 hot | 10 / 14 total | Staging v1.46.0 |
| **OpenCode** | GPT model latency variance, VS Code extension request | 10 hot | 10 | v1.15.12 |
| **Pi** | OpenAI Codex provider hang, provider API inconsistency | 10 hot | 10 | v0.77.0 |
| **Qwen Code** | SSL certificate crisis, Mode B daemon roadmap | 10 hot | 10 | Nightly |
| **CodeWhale** | Chinese IME compatibility, GLIBC version wall | 10 hot | 10 | No tag (active dev) |

---

## 3. Shared Feature Directions

**A. Extensible Agent Architectures (MCP / Hooks / Plugins)**
- **MCP lifecycle management** — Qwen Code (runtime add/remove), Kimi Code (load `mcp.json` in ACP sessions)
- **Hooks reliability** — Copilot CLI (hooks fail in subagents, double-confirmation bugs), Claude Code (Hookify semantics fixed)
- **Plugin discoverability** — OpenAI Codex (marketplace allowlist), CodeWhale (tool search result caps burying MCP tools)

**B. Context Window & Session Sovereignty**
- **Configurable context tiers** — Copilot CLI (tier setting silently ignored), Claude Code (forced 1M context for Pro hurts)
- **Transparent compaction** — Qwen Code (refactoring to summary + restoration model), OpenAI Codex (stream disconnect on compact), Kimi Code (export crash on compact), Claude Code (compaction corrupts thinking blocks)
- **Token attribution** — Kimi Code (ACP per-turn usage), OpenAI Codex (`/usage` PR stack), Pi (context window metadata misconfigured)

**C. Background / Daemon Architecture (ACP & Headless)**
- **Qwen Code:** Mode B (`qwen serve`) production-readiness drive — state caching, telemetry, workspace isolation
- **Pi:** Remote-control extension APIs (`executeInputLine`, `writeToEditor`)
- **OpenAI Codex:** Durable session interface for code mode
- **Kimi Code:** Wire-history replay on ACP session load

**D. Cross-Platform Reliability (Windows Focus)**
- **Terminal layers:** Gemini CLI (WSL `node-pty` crash), Pi (hardcoded Git Bash path), OpenCode (`node-pty` Windows crash)
- **Security software:** Claude Code (TLS-intercepting AV breaks Remote Control), Gemini CLI (AV conflicts on WSL)
- **Sandboxing:** OpenAI Codex (Windows sandbox spawn failure)

**E. Computer Use & Multi-Surface Agents**
- **Qwen Code:** Merged zero-config Computer Use (click, scroll, drag)
- **OpenAI Codex:** Chrome plugin (regionally gated)
- **Pi:** Headless / remote client APIs
- **Claude Code:** Dynamic Workflows orchestrating background agents

---

## 4. Differentiation Analysis

| Tool | Strategic Focus | Strengths | Critical Weaknesses |
|---|---|---|---|
| **Claude Code** | **Deep Agentic Orchestrator** | Pioneering multi-agent workflows, Opus reasoning | Cutting-edge tax: session serialization crisis, regression velocity |
| **OpenAI Codex** | **Infrastructure Builders** | Robust diagnostics (`doctor`), exec server security, ACP investment | Windows sandbox broken, Chrome plugin region-gated |
| **Gemini CLI** | **Recovery Candidate** | Feature velocity, `/chat` optimization | `node-pty` instability making tool unusable on WSL/Linux, OAuth fragmentation, session leaks |
| **Copilot CLI** | **Ecosystem Enforcer** | Deep GitHub integration, enterprise governance | CAPI backend fragility, context tier ignored, token waste from bloated prompts |
| **Kimi Code CLI** | **Perfect External Agent** | Fastest bug-to-patch cycle, focuses on ACP correctness for editors | Project-split confusion undermining community trust, stablizing ACP path |
| **OpenCode** | **Desktop Native** | Dedicated app experience, responsive to pricing/community | GPT latency variance, V2 UI regression, VS Code adjacency gap |
| **Pi** | **Universal Connector** | Broadest provider support, provider-agnostic, active extension API | Highest integration tax (provider-specific bugs), fragile composition APIs |
| **Qwen Code** | **Daemon & Computer Use Pioneer** | Mode B ambition, zero-config Computer Use, fast feature shipping | SSL infrastructure hurdle, IDE integration gaps |
| **CodeWhale** | **Localization Specialist** | Best Chinese IME support, playful UX pivoting | Smallest community, GLIBC wall blocking Linux LTS users |

---

## 5. Community Momentum & Maturity

**Established Leaders (High Maturity, High Burden)**
- **Claude Code** and **Copilot CLI** have the largest user bases but are weathering severe reliability crises this week. Their bugs are sophisticated (state serialization, CAPI conflicts), indicating deep platform complexity but eroding enterprise trust.
- **OpenAI Codex** has the most mature diagnostic and infrastructure foundation, though Windows sandbox and Chrome plugin issues remain glaring gaps.

**Fast Followers (Highest Momentum)**
- **Qwen Code**, **Kimi Code**, **Pi**, and **OpenCode** are closing feature gaps rapidly. Qwen is shipping major architectural shifts (compaction overhaul, Computer Use). Kimi demonstrates the tightest engineering discipline in bug-to-patch turnaround. Pi continues expanding its provider network despite the integration tax.

**Struggling Incumbent (Negative Momentum)**
- **Gemini CLI** is currently the most fragile major tool. Fundamental terminal crashes and a session leak incident make it a risky daily driver for developers across multiple platforms.

**Niche but Growing**
- **CodeWhale** serves a small, engaged community with localization-first priorities. Its project governance (brand migration, unofficial extensions) is a key maturity challenge.

---

## 6. Trend Signals

**1. Context Window is the New Memory Management**
The 1M-token model is here, but tools haven’t caught up. Copilot CLI's report of “146k tokens of system prompt before the first user message” and Claude Code's compaction crisis highlight deep system-design debt. Smarter context budgeting is a major market opportunity.

**2. Agent State Serialization is Dangerously Immature**
Claude Code’s “thinking block hell” is a harbinger for the ecosystem. As reasoning models proliferate, serializing extended thought traces, tool call graphs, and session history is proving profoundly difficult. Expect more `400` errors and “session unrecoverable” bugs across the board.

**3. Protocol Convergence is Happening—First Mover Advantage**
MCP and ACP are becoming the lingua franca of AI tooling. Kimi, Qwen, and OpenCode are investing heavily in protocol maturity. The vendor that standardizes lifecycle management and debugging for these protocols will own the middleware layer.

**4. Windows is the Underserved Greenfield**
Every tool has a Windows issue—sandboxing, terminal emulation, AV conflicts, or file system quirks. The tool that delivers a polished Windows experience first (stable sandbox, functional OAuth, reliable terminal) will capture a massive underserved developer segment.

**5. Token Transparency is the New Pricing Lever**
Users are demanding token-level attribution, configurable context windows, and pricing that reflects provider cost changes (see OpenCode’s DeepSeek pass-through demand). Tools that obfuscate quota and usage are losing power users.

**6. Security is a Core UX Feature, Not Backend Compliance**
Gemini’s cross-user conversation leak (`#22525`), Copilot’s enterprise permission gaps, and sandbox bypasses across tools demonstrate that security must be deeply wired into the agent loop, not treated as an API-level check. This will define the next wave of “production-grade” tools.

**7. The “Garbage Context” Problem**
System prompts and tool definitions silently consume 70%+ of context windows. Token efficiency in prompt design (e.g., Copilot omitting `gh`-redundant tools) is becoming a new optimization category, critical for maintaining session quality across long conversations.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Claude Code Skills Community Highlights Report** (Data as of May 29, 2026)

---

### 1. Top Skills Ranking

*Based on highest community commentary/discussion across all open PRs.*

1.  **Document Typography Skill** ([PR #514](https://github.com/anthropics/skills/pull/514))
    - **Functionality:** Prevents orphan word wraps, widow paragraphs, and numbering misalignment in AI-generated documents.
    - **Discussion Highlights:** Raised a universal pain point overlooked in generative text output. Significant engagement over standardizing typographic quality in Claude’s default document pipeline.
    - **Status:** Open

2.  **ODT Skill** ([PR #486](https://github.com/anthropics/skills/pull/486))
    - **Functionality:** Enables creation, filling, reading, and conversion of ISO-standard OpenDocument Format files (.odt, .ods), including ODT-to-HTML parsing.
    - **Discussion Highlights:** Addresses a major gap for open-source (LibreOffice/OpenOffice) users. Debate centers on ODF compliance versus proprietary format support in the skills ecosystem.
    - **Status:** Open

3.  **Skill Quality & Security Analyzer** ([PR #83](https://github.com/anthropics/skills/pull/83))
    - **Functionality:** Meta-skills that evaluate community skills across five dimensions: structure, documentation, examples, security, and resource efficiency.
    - **Discussion Highlights:** Represents a community push toward self-governance and quality gates for the marketplace. Viewed as a foundational trust and validation tool for skill submissions.
    - **Status:** Open

4.  **SAP-RPT-1-OSS Predictor** ([PR #181](https://github.com/anthropics/skills/pull/181))
    - **Functionality:** Integrates SAP’s open-source tabular foundation model (Apache 2.0) for predictive analytics directly through Claude’s conversational interface.
    - **Discussion Highlights:** Signals demand for domain-specific, on-premise-capable ML models as skill triggers. Discussion focuses on connector patterns for specialized enterprise runtimes.
    - **Status:** Open

5.  **Testing Patterns Skill** ([PR #723](https://github.com/anthropics/skills/pull/723))
    - **Functionality:** Covers a full testing stack: philosophy (Testing Trophy model), unit test design (AAA), React Testing Library patterns, E2E strategy, and a comprehensive checklist.
    - **Discussion Highlights:** The most broadly applicable developer skill in the top set. Key discussion thread around pyramid vs. trophy testing philosophy for AI-augmented workflows.
    - **Status:** Open

6.  **AURELION Skill Suite** ([PR #444](https://github.com/anthropics/skills/pull/444))
    - **Functionality:** Four-skill cognitive framework (Kernel, Advisor, Agent, Memory) providing a structured 5-floor architecture for professional knowledge management and AI reasoning.
    - **Discussion Highlights:** Represents the most ambitious “cognitive scaffolding” skill. Community commenting focuses on composability and whether an agent should own such a complex internal framework.
    - **Status:** Open

7.  **ServiceNow Platform Skill** ([PR #568](https://github.com/anthropics/skills/pull/568))
    - **Functionality:** Broad platform assistant covering ITSM, ITOM, ITAM, SecOps, HRSD, CSDM, and IntegrationHub scripting.
    - **Discussion Highlights:** Directly addresses enterprise ITSM demand. Discussion centers on balancing skill breadth (10+ modules) against prompt efficiency and precise trigger scoping.
    - **Status:** Open

8.  **Codebase Inventory Audit Skill** ([PR #147](https://github.com/anthropics/skills/pull/147))
    - **Functionality:** Systematic 10-step workflow for identifying orphaned code, unused dependencies, documentation gaps, and infrastructure bloat.
    - **Discussion Highlights:** Pairs with testing and refactoring skills to form a “developer hygiene” trilogy. Community interest centers on maintaining clarity in large, long-running projects.
    - **Status:** Open

---

### 2. Community Demand Trends

*Distilled from the most-commented issues in the repository.*

- **Enterprise Governance & Sharing (7 of top 15 issues):** The strongest consistent signal is the need for organizational controls—org-wide skill sharing ([#228](https://github.com/anthropics/skills/issues/228)), namespace trust boundaries vs. community authorship ([#492](https://github.com/anthropics/skills/issues/492)), and formal agent governance patterns ([#412](https://github.com/anthropics/skills/issues/412)). The ecosystem is being asked to support enterprise security constraints.
- **Developer Workflow Stability (5 issues):** A significant friction cluster around reliability: skills disappearing silently ([#62](https://github.com/anthropics/skills/issues/62)), evaluation tooling failing to trigger skills at all ([#556](https://github.com/anthropics/skills/issues/556)), and plugin systems installing duplicate or oversized content ([#189](https://github.com/anthropics/skills/issues/189), [#1087](https://github.com/anthropics/skills/issues/1087)). Tooling maturity is the primary blocker for power users.
- **Platform Interoperability (2 issues):** Users explicitly demand skills consumable outside the CLI—via MCP protocol ([#16](https://github.com/anthropics/skills/issues/16)) and AWS Bedrock ([#29](https://github.com/anthropics/skills/issues/29)). The implication is that skills must be designed protocol-agnostic.
- **Context & Security Boundaries (2 issues):** Emerging concern about context window pressure when MCPs return massive data ([#1102](https://github.com/anthropics/skills/issues/1102)) and appropriate permission handling for external data sources like SharePoint ([#1175](https://github.com/anthropics/skills/issues/1175)).

---

### 3. High-Potential Pending Skills

*Active, open PRs that are well-positioned to merge given community demand and discussion velocity.*

- **Document Typography Skill** ([PR #514](https://github.com/anthropics/skills/pull/514)) — Universal formatting QoL; top of the comment list.
- **Testing Patterns Skill** ([PR #723](https://github.com/anthropics/skills/pull/723)) — Broadest developer workflow appeal; high synergy with Claude Code’s agentic coding features.
- **n8n Builder & Debugger** ([PR #190](https://github.com/anthropics/skills/pull/190)) — Taps directly into the workflow automation trend; two complementary skills in one submission.
- **Shodh-Memory Skill** ([PR #154](https://github.com/anthropics/skills/pull/154)) — Addresses the persistent context gap for long-running agent tasks.
- **AURELION Skill Suite** ([PR #444](https://github.com/anthropics/skills/pull/444)) — Ambitious cognitive architecture; strong early engagement indicates a dedicated user segment.
- **ServiceNow Platform Skill** ([PR #568](https://github.com/anthropics/skills/pull/568)) — Matches the strong enterprise demand signal from issues; large potential user base.
- **Skill Quality & Security Analyzer** ([PR #83](https://github.com/anthropics/skills/pull/83)) — Foundational marketplace infrastructure; may become a prerequisite for future submissions.

---

### 4. Skills Ecosystem Insight

The Claude Code skills community is converging on a **professionalization mandate**: the most concentrated demand is for enterprise-grade governance (org sharing, trust boundaries, ServiceNow/SAP integration), robust and reliable developer tooling, and structured cognitive frameworks (memory, reasoning architectures) that transition Claude from an experimental coding assistant into a trusted, auditable, autonomous platform agent.

---

# Claude Code Community Digest — 2026-05-29

## 1. Today's Highlights
This week's major `v2.1.154` release—featuring Opus 4.8 and the new Dynamic Workflows engine—has triggered a severe stability crisis. A wave of session-bricking `400` errors related to thinking block serialization dominates the tracker, and the emergency `v2.1.156` hotfix has introduced a secondary `Invalid message role "system"` regression. Community investigators have isolated the root cause to how transcripts serialize extended thinking content, while the engineering team races to stabilize core session reliability.

## 2. Releases
- **v2.1.156 (emergency hotfix):** Patches an issue where thinking blocks were incorrectly modified on Opus 4.8, leading to `400` API errors.
- **v2.1.154 (major feature release):** Introduces **Opus 4.8** (defaults to high effort, supports `/effort xhigh`) and **Dynamic Workflows**—orchestrating work across tens to hundreds of background agents for complex multi-step tasks.

## 3. Hot Issues
The last 24 hours are dominated by a single crisis. Here are the 10 most significant discussions:

1. **#10199 – API Error 400 – Thinking Block Modification Error** (92 comments, 55 👍)
   The original dormant bug that has become ground zero. Every new thinking block issue traces back to this core serialization problem with extended thinking content blocks.
   [Link](https://github.com/anthropics/claude-code/issues/10199)

2. **#63147 – Resuming extended-thinking session fails permanently** (26 comments, 32 👍)
   A definitive root cause deep-dive. Traces the `400` error to how the transcript stores thinking blocks (empty text + preserved signature), making session resumption unrecoverable.
   [Link](https://github.com/anthropics/claude-code/issues/63147)

3. **#63469 & #63423 – API Error 400: Invalid message role "system"** (8+ comments)
   **Hotfix regression.** The v2.1.156 patch incorrectly injects a `system` role message into the conversation history, breaking both the CLI and VS Code extension immediately.
   [Link](https://github.com/anthropics/claude-code/issues/63469)

4. **#63448 – Context compaction breaks thinking blocks permanently** (3 comments)
   A specific trigger: the conversation compactor corrupts extended thinking content on Opus 4.8, making every turn fail with `400` after the first compaction event.
   [Link](https://github.com/anthropics/claude-code/issues/63448)

5. **#63464 – Context exceeds 100% without triggering autocompaction** (2 comments)
   Context usage hit `136%` and the compactor failed to fire, causing an unrecoverable crash. Exposes a critical reliability gap in context window management.
   [Link](https://github.com/anthropics/claude-code/issues/63464)

6. **#63447 – Opus 4.8 context window size misreported as 200K** (2 comments)
   The statusline reports `context_window_size: 200000` for Opus 4.8 (1M context), causing premature `100% context used` warnings and aggressive compaction.
   [Link](https://github.com/anthropics/claude-code/issues/63447)

7. **#63258 – Backgrounded subagents crash with `400 thinking blocks`** (2 comments, 5 👍)
   The flagship Dynamic Workflows feature is severely impacted—background agents immediately crash on their first turn with the same serialization error.
   [Link](https://github.com/anthropics/claude-code/issues/63258)

8. **#63470 – Remote Control silently fails with TLS-intercepting AV on Windows** (2 comments)
   HTTPS-scanning antivirus (Norton 360, Bitdefender) causes silent failures in Remote Control on Windows because Node rejects MITM certificates.
   [Link](https://github.com/anthropics/claude-code/issues/63470)

9. **#62123 – Model's tool call could not be parsed (retry also failed)** (15 comments, 28 👍)
   A widely-felt reliability issue where the model generates structurally invalid tool calls that can't be recovered, halting autonomous execution.
   [Link](https://github.com/anthropics/claude-code/issues/62123)

10. **#62063 – Pro plan users defaulted to 1M context with no workaround** (10 comments, 6 👍)
    Fresh sessions default to 1M context, hitting Pro users with `Usage credits required` errors. No toggle exists to cap context to their plan limit.
    [Link](https://github.com/anthropics/claude-code/issues/62063)

## 4. Key PR Progress (7 PRs updated in the last 24h)

1. **#63262 / #63252 – feat: add side-threads plugin** (`/thread` and `/back`)
   A creative community plugin introducing Slack-style side-threads to run tangent explorations without polluting the main conversation context.
   [Link](https://github.com/anthropics/claude-code/pull/63262)

2. **#63189 – Use PR template in `/commit-push-pr`**
   Reads `.github/PULL_REQUEST_TEMPLATE.md` to guide PR generation, ensuring output follows repository conventions rather than a freeform description.
   [Link](https://github.com/anthropics/claude-code/pull/63189)

3. **#63467 – docs: add Windows gh CLI install instruction**
   Closes a documentation gap by adding `winget install --id GitHub.cli` instructions for Windows users in the commit-commands README.
   [Link](https://github.com/anthropics/claude-code/pull/63467)

4. **#63460 – docs: update deprecated npm install instructions**
   Aligns plugin installation docs with the main README, deprecating `npm install -g` in favor of `curl`/`irm` one-liners.
   [Link](https://github.com/anthropics/claude-code/pull/63460)

5. **#63382 – Fix Hookify tests example semantics**
   Corrects documentation for the test-before-stop hook, replacing a misleading regex-like pattern with explicit `not_contains` checks matching engine behavior.
   [Link](https://github.com/anthropics/claude-code/pull/63382)

6. **#62941 – fix(ralph-wiggum): correctly read last assistant text**
   Fixes a parsing bug in the Ralph Wiggum stop hook that only read the last line of the JSON transcript, potentially missing earlier assistant messages.
   [Link](https://github.com/anthropics/claude-code/pull/62941)

7. **(Awaiting fix) TUI arrow key regression #63191** – A confirmed regression (v2.1.149+) broke Up/Down arrow navigation in multiline input, forcing users to cycle history instead of moving between lines. No fix PR has landed yet.

## 5. Feature Request Trends
- **Dynamic Workflows Maturation:** The top enhancement demand is per-agent configuration—distinct working directories, MCP server profiles, and `CLAUDE.md` rules for each teammate in a workflow (#23669, 26 👍). Users also want push notifications for permission approval during Remote Control sessions (#29438, 54 👍).
- **TUI/Input Quality of Life:** Users are seeking parity with competitive tools (e.g., Codex CLI) for multiline input handling, specifically arrow key navigation within the input buffer rather than cycling history (#62922, #63191).
- **Platform Parity:** Requests for FreeBSD native binaries (#61313) and fixes to Windows installer DACL permissions blocking upgrades (#57035) highlight ongoing demand for consistent cross-platform support.

## 6. Developer Pain Points
- **Session Stability Crisis (Thinking Block Fallout):** The dominant theme. Opus 4.8 exposed a latent, severe bug in extended thinking serialization. Sessions are permanently bricked, background agents crash, and the hotfix introduces new errors. Trust in session reliability is significantly shaken.
- **Regression Velocity:** Users are frustrated that stable features (thinking summaries on Opus 4.7, TUI multiline input, Hookify transcript parsing) break between minor patches without warning, eroding confidence in the release process.
- **Cost/Context Ambiguity:** The hard default to 1M context for Pro users, combined with the misreported context window size for Opus 4.8, creates a confusing experience where users hit undisclosed usage limits or experience prematurely aggressive context compaction.
- **Windows Ecosystem Fragility:** Windows continues to be a second-class citizen. TLS-intercepting AV breaks Remote Control, installer permission DACLs block upgrades, and specific builds crash with segmentation faults.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest — 2026-05-29**

---

### 1. Today’s Highlights
The ecosystem sees the stable release of `rust-v0.135.0` with a heavily revamped `codex doctor` for deep diagnostics and a new `/status` TUI command. Meanwhile, the Windows sandbox `spawn setup refresh` regression continues to dominate community frustration, and the `/usage` reporting stack makes its way through the PR pipeline, promising much-needed token observability for developers.

---

### 2. Releases
- **rust-v0.135.0**  
  Now on the stable channel. Highlights include an overhauled `codex doctor` command that surfaces richer environment, Git, terminal, app-server, and thread inventory diagnostics for support cases. The TUI now supports `/status` to display remote connection details and server version.
- **rust-v0.136.0-alpha.1**  
  An early alpha for the next minor release is available for testing.

---

### 3. Hot Issues (Top 10)
1. **#21598 – Windows Chrome Plugin Unavailable in Norway/EU** *(25 Comments | 11 👍)*  
   The `@Chrome` route is blocked by a regional gate despite the extension reporting “Connected.” A confusing UI/runtime mismatch that frustrates users with a perfectly healthy local setup.  
   *(openai/codex Issue #21598)*

2. **#22107 – Context Compaction Fails with “Stream Disconnected”** *(13 Comments | 9 👍)*  
   A critical stability defect: the remote compact task hits a stream disconnection error, breaking session context management and leaving users with corrupted thread state.  
   *(openai/codex Issue #22107)*

3. **#19909 – Feature Request: Configurable Chats Directory** *(12 Comments | 16 👍)*  
   The highest-voted feature request in this window. Developers need to move the `~/Documents/Codex` chat storage to avoid iCloud Drive sync conflicts and improve project isolation.  
   *(openai/codex Issue #19909)*

4. **#24391 – Windows Sandbox `spawn setup refresh` Fails on CLI 0.133.0** *(7 Comments | 15 👍)*  
   A widespread regression on Windows. Shell commands and `node_repl` execution are killed immediately by a sandbox provisioning failure, effectively blocking all CLI workflows.  
   *(openai/codex Issue #24391)*

5. **#20538 – Desktop Preferences “Unable to Save” / Config Version Conflict** *(7 Comments | 17 👍)*  
   A sticky UX bug where `configVersionConflict` errors put the preferences panel into a persistent fail state that survives restarts. High community signal (17 upvotes).  
   *(openai/codex Issue #20538)*

6. **#24006 – macOS: Database Access Failure After Update** *(7 Comments | 6 👍)*  
   A launch-killer for macOS users. The app cannot access its local database after a Codex update, completely preventing startup on Apple Silicon machines.  
   *(openai/codex Issue #24006)*

7. **#24969 – Windows Store Browser Use Blocked by Enterprise Policy** *(7 Comments)*  
   The Windows Store variant uses the in-app browser (IAB) instead of the Chrome extension, exposing users to enterprise network policies that block all URL navigation.  
   *(openai/codex Issue #24969)*

8. **#24933 – Seccomp `sendto` Deny Breaks Python `asyncio`** *(2 Comments)*  
   A deep sandbox bug: the Linux seccomp profile’s strict rules silently break core Python `asyncio` cross-thread primitives, impacting data science and async workflows.  
   *(openai/codex Issue #24933)*

9. **#23953 – Remote Quota Exceeded Error vs. Direct CLI Success** *(3 Comments | 9 👍)*  
   Confusing behavior where Remote and mobile sessions report quota limits even though the CLI works directly on the same host. Suggests a per-session billing state bug.  
   *(openai/codex Issue #23953)*

10. **#24780 – iOS Remote Tasks Disappear After Refresh** *(3 Comments)*  
    Remote-controlled threads using custom providers vanish from the thread list after a refresh, breaking workflow continuity for mobile remote users.  
    *(openai/codex Issue #24780)*

---

### 4. Key PR Progress (Top 10)
1. **#24992 – Move Skills Path Refs into Exec Server**  
   Refactors environment path primitives into the exec server as `EnvironmentPathRef`, enabling more robust multi-environment skill loading and plugin reads.  
   *(openai/codex PR #24992)*

2. **#25000 – CI: Test Windows Cross Build**  
   Introduces code-mode tests for cross-compiled V8 on Windows to prevent platform-specific sandbox regressions from reaching users.  
   *(openai/codex PR #25000)*

3. **#24999 – Add Per-Session Realtime Model/Version Overrides**  
   Adds optional `model` and `version` fields to `thread/realtime/start`, giving clients per-session configuration without mutating persistent server state.  
   *(openai/codex PR #24999)*

4. **#24996 – Use Marketplace Allowlist for Plugin Install Suggestions**  
   Replaces a hardcoded tool-suggest allowlist with a dynamic marketplace allowlist for better, context-aware plugin discovery.  
   *(openai/codex PR #24996)*

5. **#24958 – Add Exec Server Direct Websocket Connection Token**  
   Adds a `--connection-token TOKEN` flag and enforces a `?token=` parameter on direct websocket upgrades, improving security for remote exec-server sessions.  
   *(openai/codex PR #24958)*

6. **#16974 – Preserve zsh PATH in Shell Snapshots**  
   Fixes a long-standing macOS issue where zsh’s unique `export -T PATH path` syntax caused `PATH` to be dropped from shell snapshots, breaking environment inheritance.  
   *(openai/codex PR #16974)*

7. **#24180 – Introduce Durable Session Interface for Code Mode**  
   An architectural milestone: creates a `CodeModeSession` abstraction to decouple cell execution from the in-process model, paving the way for resilient, restartable code sessions.  
   *(openai/codex PR #24180)*

8. **#22668 – Wire Managed MITM CA Trust into Child Env**  
   Core proxy infrastructure: automatically trusts Codex’s managed MITM CA in spawned child processes, preventing TLS errors in intercepted environments.  
   *(openai/codex PR #22668)*

9. **#24972 – Route Extension Image Generation Through Native Pipeline**  
   Aligns extension-based image generation with the native artifact pipeline, replacing developer-message workarounds with proper tool-result integration.  
   *(openai/codex PR #24972)*

10. **#24124/#24122/#24123 – Usage Report Feature Stack**  
    The `/usage` command is materializing across three PRs: adds token attribution storage (#24122), an app-server `usage/read` endpoint (#24123), and the TUI rendering and command interface (#24124).  
    *(openai/codex PR #24124)*

---

### 5. Feature Request Trends
- **Environment Configuration** – Strong demand for configurable storage paths (#19909) and user-chosen shells on Windows (#13165), indicating developers want Codex to adapt to their local OS habits rather than enforce defaults.
- **Hooks Extensibility** – Requests like the `PostToolUseFailure` hook (#24907) show that power users need failure-branch logic to match the existing success-path hooks, pointing to a maturing automation story.
- **Remote Workflow Parity** – Issues around heartbeat automations (#24640) and thread persistence (#24780) confirm that Remote is now a primary workflow, and gaps in feature parity are becoming critical adoption blockers.

---

### 6. Developer Pain Points
- **Windows Sandbox Reliability Crisis** – The `spawn setup refresh` failure (#24259, #24391) is the single highest-impact issue on the platform, blocking basic shell execution for a large segment of Windows users.
- **Chrome Plugin Regional Gating Confusion** – Multiple high-traffic issues (#21598, #21741) show a broken UX where the extension is locally healthy but backend region checks silently disable the feature, leaving users with a “Connected but can’t use it” state.
- **Desktop App State Corruption** – Config version conflicts (#20538) and database launch failures (#24006) point to an app that struggles with stateful migrations and safe config writes, causing persistent errors on both Windows and macOS.
- **Sandbox vs. Standard Libraries** – The Linux sandbox seccomp profile is too aggressive, breaking core Python `asyncio` primitives (#24933) and multiprocessing (#24943), forcing developers to disable the sandbox or adopt fragile workarounds.
- **Plugin/Connector Scope Fragility** – Google Drive integrations (#24373, #24233) consistently pass read checks but fail on write due to incomplete OAuth scope negotiation, creating a confusing “half-working” integration state.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-29

## Today’s Highlights
The `ioctl(2) EBADF` crash cluster in `node-pty` continues to dominate, with multiple open P1 issues (#27533, #27544, #27538) and targeted PRs (#27354, #27329) aiming to stabilize the terminal layer. Security concerns are acute: a now-closed cross-user conversation leak (#22525) underscores systemic isolation risks, while an SSRF fix in the `web-fetch` tool (#27335) blocks open-redirect exploitation of internal metadata endpoints. On a positive note, the `/chat` command now loads large histories in under a second (#27028), Windows image pasting lands (#27054), and the stable channel received an important patch in `v0.44.1`.

## Releases
- **v0.45.0-preview.1**: Cherry-pick fix into the preview branch (PR #27535).
- **v0.44.1**: Stability cherry-pick backported to the stable release track.
- **v0.45.0-nightly.20260528.g5cac7c10f**: Fix for ignoring unmapped Vim normal keys (first contribution from @MukundaKatta, PR #27102).

## Hot Issues (10 Topics)
**1. Terminal Crash Cluster: `ioctl(2) failed, EBADF`**  
[#27544](https://github.com/google-gemini/gemini-cli/issues/27544) [OPEN / p1], [#27533](https://github.com/google-gemini/gemini-cli/issues/27533) [OPEN / p1], [#27538](https://github.com/google-gemini/gemini-cli/issues/27538), [#27541](https://github.com/google-gemini/gemini-cli/issues/27541)  
The highest-signal issue group this week. Multiple users report hard crashes originating from `@lydell/node-pty` during terminal resize operations on WSL, SSH, and Linux hosts. The CLI aborts entirely, blocking all usage.

**2. Cross-User Conversation Data Leak**  
[#22525](https://github.com/google-gemini/gemini-cli/issues/22525) [CLOSED / p1]  
A deeply concerning incident: the CLI began streaming an unrelated user’s chat history in Polish/Dutch into another user’s session. This has significant security implications for session isolation.

**3. WSL2 OAuth Broken + Anti-virus Conflicts**  
[#23865](https://github.com/google-gemini/gemini-cli/issues/23865) [CLOSED / p1]  
Paid Pro users on WSL2 cannot complete OAuth login. The issue also highlights conflicts with security software that intercept the login flow. High urgency for the WSL developer audience.

**4. MCP Server OAuth Origin Mismatch**  
[#20017](https://github.com/google-gemini/gemini-cli/issues/20017) [CLOSED / p2]  
A friction point in the MCP ecosystem: the CLI rejects OAuth flows when the protected resource origin doesn't exactly match the SSE connection URL, blocking custom MCP server auth.

**5. Gemini 3.1 Pro Preview Denied on Paid Plan**  
[#24222](https://github.com/google-gemini/gemini-cli/issues/24222) [CLOSED / p1] (7 👍)  
Users with active premium subscriptions seeing “You don’t have access to gemini-3.1-pro-preview.” Signals a broken entitlement gate between subscription tiers and model preview access.

**6. Quota Consumed "Super Fast" Per Request**  
[#22634](https://github.com/google-gemini/gemini-cli/issues/22634) [CLOSED / p2] (4 👍)  
A single coding task burns through hundreds of requests, exhausting daily limits in minutes. Suggests a regression in how internal tool calls or context windows are counted against user quota.

**7. Infinite Rate-Limit Loop + Fatal Crash**  
[#23738](https://github.com/google-gemini/gemini-cli/issues/23738) [CLOSED / p1]  
The CLI ignores the server’s `Retry-After` instruction, enters an infinite retry loop that exhausts quota, and then fatally crashes with a `node-pty` allocation failure. A compounded stability and UX failure.

**8. Agent “Thinks” for 30+ Minutes, No Progress**  
[#23627](https://github.com/google-gemini/gemini-cli/issues/23627) [CLOSED / p1]  
The agent read a `README.md` file for half an hour without providing any output or making progress on the assigned task. Undermines trust in agent-based workflows.

**9. Missing Formal Validation for Build/Lint Configs**  
[#16114](https://github.com/google-gemini/gemini-cli/issues/16114) [CLOSED / p2]  
(14 comments) A maintenance debt issue identifying no tests for native module exclusion, WASM resolution, or security linting. This has directly influenced PRs #27257 and #27068.

**10. CLI Starts But Never Responds**  
[#27520](https://github.com/google-gemini/gemini-cli/issues/27520) [CLOSED / p2]  
Users report the CLI launches but hangs completely with no response for 6+ minutes, suggesting a terminal initialization or network connectivity deadlock.

## Key PR Progress (10 Topics)

**1. Prevent SSRF via Open Redirect in `web-fetch`**  
[#27335](https://github.com/google-gemini/gemini-cli/pull/27335) [OPEN]  
`fetchWithTimeout` follows HTTP redirects by default, but the `isBlockedHost` check only applies to the initial URL. An attacker can redirect the tool to `http://169.254.169.254/`. Critical security hardening.

**2. Bypass `node-pty` on WSL for Windows Executables**  
[#27354](https://github.com/google-gemini/gemini-cli/pull/27354) [OPEN / p2]  
Directly addresses the top crash theme. Falls back to standard Node `child_process` when `.exe` files are run inside WSL, avoiding known PTY interop failures.

**3. Strip `functionCall.id` / `functionResponse.id` from API Payload**  
[#27341](https://github.com/google-gemini/gemini-cli/pull/27341) [OPEN / p2]  
Fixes 400 "Unknown name 'id'" errors that break every turn after a tool call. Internal ACP IDE IDs were leaking into the Gemini API request payload.

**4. Gracefully Skip Missing `includeDirectories` on Startup**  
[#27329](https://github.com/google-gemini/gemini-cli/pull/27329) [OPEN / p1]  
Prevents a hard crash on startup when a directory referenced in `settings.json` no longer exists. Now skips the missing path instead of aborting.

**5. Sub-Second `/chat` Loading for Large Histories**  
[#27028](https://github.com/google-gemini/gemini-cli/pull/27028) [OPEN / p2]  
Load time benchmarked from 25+ seconds down to 634ms on a 59-session, 2.3 GB dataset. Eliminates three compounding bottlenecks in `chatRecordingService.ts`.

**6. Windows Image Pasting and Clipboard Styling**  
[#27054](https://github.com/google-gemini/gemini-cli/pull/27054) [OPEN / p2]  
Closes feature parity gap for Windows Terminal users. Handles empty bracketed paste sequences and adds clean UI rendering for pasted clipboard images.

**7. Wrap Ajv `validate()` in try/catch to Prevent Schema Crash**  
[#27348](https://github.com/google-gemini/gemini-cli/pull/27348) [OPEN / p1]  
Prevents a `Cannot read properties of undefined` crash in `write_file`/`replace` tools when the LLM sends unexpected parameter shapes.

**8. F10 Fallback for Approval Mode Cycling**  
[#26088](https://github.com/google-gemini/gemini-cli/pull/26088) [OPEN / p3]  
`Shift+Tab` sequences are misparsed by Windows/WezTerm. Adds F10 as a reliable fallback for cycling the approval mode, improving terminal compatibility.

**9. Prevent Natural Language Being Saved as Shell Commands**  
[#27347](https://github.com/google-gemini/gemini-cli/pull/27347) [OPEN / p2]  
Fixes data corruption when `/statusline` or MCP tools receive natural language input (e.g., “mostrar diretório”). Raw text no longer gets written into the command history as an executable command.

**10. Fix `AfterAgent` Hook `prompt_response`**  
[#27047](https://github.com/google-gemini/gemini-cli/pull/27047) [OPEN / p2]  
Ensures the hook payload mirrors the exact text streamed to the user, instead of rebuilding it from the turn debug buffer which could contain corrupted or duplicated content.

## Feature Request Trends
- **Explicit Model Pinning**: Users are demanding the ability to lock a specific model version (e.g., Gemini 2.5 Pro) without being silently upgraded to preview channels or blocked from new GA models. (#23721, #24222)
- **CI-Level Configuration Validation**: Issue #16114 has sparked PRs (#27068, #27257) that the community clearly wants as standard practice: automated tests for bundling rules, security linting, and native-module externalization.
- **First-Class OAuth for MCP Servers**: The strict origin matching in the CLI OAuth flow is a recurring friction point for developers building custom MCP backends. (#20017)
- **Session Resilience & Persistence**: A2A task workspace archives (#27343) and server-side trust derivation (#27337) signal a push toward more reliable, cross-session context management.
- **Terminal Survival Mechanics**: Users want the agent to survive SIGHUP, SSH disconnects, and terminal resize events without crashing (#27533, #27544).

## Developer Pain Points
1. **`node-pty` Instability**  
   The defining pain point of the week. The CLI is unusable on WSL and many Linux/SSH setups due to fatal `ioctl(2)` errors on resize. Developers feel blocked from daily use.

2. **Quota / Rate-Limit Opaqueness**  
   Users on paid plans cannot predict when they will be throttled. Requests are consumed “super fast,” `Retry-After` headers are ignored, and daily limits don’t reset properly (#22634, #23738, #22643).

3. **Authentication Fragmentation**  
   Overlapping subscription types (Google One AI Pro vs. Gemini Code Assist Enterprise) cause entitlement stripping and “shadow ban” errors. WSL users face a completely broken OAuth flow (#19970, #23865).

4. **Unpredictable Agent Behavior**  
   From stalling for 30 minutes on a README (#23627) to deleting project contents in YOLO mode (#23837), the agent’s task loop remains a source of deep uncertainty for users trusting it with real work. The communication leak (#22525) is the most extreme example of this unpredictability.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for 2026-05-29.

---

## GitHub Copilot CLI Community Digest — 2026-05-29

### 1. Today’s Highlights
The team shipped two rapid patches (v1.0.56-0 and v1.0.56-1) to fix session persistence and context tier bugs, signaling an aggressive push on reliability. However, a flood of “Duplicate item found” CAPI 400 errors is breaking agentic workflows across the community, making session stability the top pain point of the week. Meanwhile, the debate over context window bloat from MCP tools is driving demand for better context tier management and model-native limits.

### 2. Releases
Three versions were cut in the last 24 hours:

- **v1.0.56-1**: The code review agent now uses the user’s current session model instead of a fixed default. The GitHub MCP server omits redundant `gh`-replaceable tools by default to reduce token usage. *Fixed*: Cursor position after pasting.
- **v1.0.56-0**: *Fixed*: Context window tier selection now persists durably in session events and survives SDK-only resume paths, preventing unexpected compaction on session restoration.
- **v1.0.55**: Free and Student plan users are now restricted to Auto model selection with an explanatory tooltip. Added official support for Claude Opus 4.8 and reporting of Claude thinking/reasoning tokens. *Fixed*: Loading spinner no longer hangs indefinitely.

### 3. Hot Issues (10 Noteworthy)

1. **[#223: “Copilot Requests” Permission Visibility](https://github.com/github/copilot-cli/issues/223)** (👍73, 27 comments)
   Enterprise orgs cannot see the “Copilot Requests” permission when creating organization-owned fine-grained tokens. This blocks corporate governance policies that prohibit individual PATs for automations. High community demand.

2. **[#3539: Context Window Bloat](https://github.com/github/copilot-cli/issues/3539)** (3 comments)
   System and tool definitions consume 146k tokens out of the 200k window before the user sends a single message. This triggers immediate auto-compaction in fresh sessions, degrading response quality from the first turn.

3. **[#3560 / #3558 / #3559: Duplicate Item CAPI Errors](https://github.com/github/copilot-cli/issues/3560)** (7 comments combined)
   A cluster of reports about `Execution failed: CAPIError: 400` with “Duplicate item found” for `fc_call_*` IDs. The bug appears related to session-state replay on resume or tool call history deduplication. This is the most active disruption this week.

4. **[#1274: CLI 400 Errors](https://github.com/github/copilot-cli/issues/1274)** (24 comments)
   A long-running issue resurfaced where 95% of code review prompts on diffs result in 400 errors. Users suspect both server-side validation and client-side malformation. Debug logs included.

5. **[#3042: Double Confirmation for Plugin Hooks](https://github.com/github/copilot-cli/issues/3042)** (3 comments)
   When a `PreToolUse` hook returns `permissionDecision: "ask"`, the plugin dialog fires, followed immediately by the native trust prompt. Users must approve twice, breaking the desired seamless UX.

6. **[#3355: Claude Opus 4.6 Context Cap](https://github.com/github/copilot-cli/issues/3355)** (2 comments, 👍2)
   The CLI caps Claude Opus 4.6 at 200k tokens despite the model natively supporting 1M. Frequent compaction in deep sessions frustrates power users who want to opt-in to the full window.

7. **[#3527: contextTier Setting Ignored](https://github.com/github/copilot-cli/issues/3527)** (2 comments)
   The `contextTier` setting is persisted to `settings.json` but not read at session start. Fresh sessions always default to 200k, ignoring the user’s explicit opt-in via `/model`.

8. **[#2540: Plugin preToolUse Hooks Not Firing in Subagents](https://github.com/github/copilot-cli/issues/2540)** (3 comments)
   Hooks defined in a plugin’s `hooks.json` fail entirely in the main session and in subagents spawned via the `task` tool. This undermines safety checks for autonomous workflows.

9. **[#3543: Startup Freeze](https://github.com/github/copilot-cli/issues/3543)** (1 comment)
   A 15–30 second freeze on launch traced to an unbounded recursive glob over `COPILOT_CUSTOM_INSTRUCTIONS_DIRS`. Users with large home or monorepo directories experience full TUI unresponsiveness.

10. **[#3520: Session Event Schema Broken](https://github.com/github/copilot-cli/issues/3520)** (1 comment)
    CLI 1.0.54 writes session events without the required `ephemeral` field, violating its own bundled JSON schema. This breaks VS Code session resume and downstream tooling.

### 4. Key PR Progress
**No pull requests were updated in the last 24 hours.** The rapid cadence of v1.0.56-x patch releases suggests the team is currently in a stabilization and hotfix cycle focused on session state integrity, context tier persistence, and the “Duplicate item” regression.

### 5. Feature Request Trends

- **Context Window Sovereignty**: Developers increasingly want configurable context tiers, the ability to use models at their native cap (e.g., 1M for Opus), and visibility into session identifiers to manage parallel sessions.
- **MCP Lifecycle Management**: Users are asking for toggle-based enable/disable of MCP servers without full deletion, config-file auto-enablement, and stricter enterprise governance over which servers can be installed.
- **New Slash Commands**: Continued interest in `/security-review` for pre-commit vulnerability scanning and better slash-command support in non-interactive (ACP) modes.
- **Plugin Hooks Reliability**: The failure of hooks in subagents and double-confirmation bugs are driving calls for a full audit of the plugin execution pipeline.

### 6. Developer Pain Points

- **Session Reliability Crisis**: The #1 complaint this week is the flood of “400 Duplicate item found” errors that destroy agent sessions and force full restarts. Trust in the CLI’s state management is eroding.
- **Token Waste**: Between immediate auto-compaction from bloated system prompts, models dumping code in plan mode, ignored context tier settings, and dropped MCP content types, developers feel the CLI is fighting them for useful context.
- **Configuration Drift**: Persisted settings like `contextTier` and subagent model overrides are silently ignored or reset, creating an unpredictable experience where advanced configuration feels useless.
- **Plugin Fragility**: Core plugin features (permission hooks, subagent propagation) are broken or produce double prompts, making them unreliable for production agentic workflows.
- **Startup Performance Regression**: The 15–30 second freeze from directory globbing is a significant UX regression for power users with complex setups.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-05-29**

---

### 1. Today’s Highlights
Today’s digest is dominated by critical bug fixes for data persistence and IDE integration. A fresh crash in `kimi export` during context compaction was reported and patched within hours ([#2396](#), [#2395](#)). The community continues to push hard on ACP completeness, with meaningful progress on session replay ([#2132](#)) and custom MCP tool loading ([#2047](#)). At the same time, the growing frustration over the strategic split between **kimi-cli** and **kimi-code** boiled over into a pointed issue ([#2381](#)), signaling trust concerns among power users that the maintainers will need to address.

---

### 2. Releases
No new stable release was published today. The release pipeline is active: **v1.46.0** is being staged via [#2391](#), which will gather the accumulated bug fixes and polish from the past several days.

---

### 3. Hot Issues
*Picked 8 (all issues updated in the last 24h)*

1. **[#2396] kimi export crashes during context compaction — API 400 text content is empty** (NEW)  
   **Why it matters:** A hard crash on session export. The compaction code fails to filter empty `TextPart`s, causing an unrecoverable API 400. Immediate community attention.
   **Mood:** Urgent, quickly actionable.

2. **[#2381] Why abandon kimi-cli and redo kimi code?** (NEW, HIGH TRAFFIC)  
   **Why it matters:** The most visible community sentiment signal this month. A user openly questions the split between the two projects, calling it a “community divide” and threatening to cancel subscriptions.
   **Mood:** Angry, distrustful.

3. **[#1894] Kimi CLI cannot recursively load nested skill directories** (LONGRUNNING)  
   **Why it matters:** A feature parity gap with Anthropic’s Codex. Users migrating configurations lose structured `.agents/skills/{name}/skills/` hierarchies.
   **Mood:** Persistent, waiting for product leadership.

4. **[#2394] ACP server does not expose per-turn token usage** (FEATURE)  
   **Why it matters:** Essential for host apps (Zed, etc.) to display real-time cost and context consumption. Kimi calculates the data internally but drops it on the wire.
   **Mood:** Feature gap, low noise.

5. **[#2385] Infinite loop while searching for files in Zed** (BUG)  
   **Why it matters:** A complete UX blocker for the Zed workflow. File search is a fundamental action.
   **Mood:** Frustrated, waiting for a fix.

6. **[#2384] Large context requests cause ConnectTimeout — httpx connect_timeout is not configurable** (BLOCKER)  
   **Why it matters:** Hard-coded client timeout hits users running contexts over ~120k tokens. No workaround without source modification.
   **Mood:** Critical for heavy users.

7. **[#1984] Terminal hang on exit and MCP connection leak** (CLOSED)  
   **Why it matters:** A long-standing stability issue. Fix merged via [#1985](#) — non-blocking `os.read` and proper MCP shutdown. Positive closure for the community.

8. **[#2127] ACP `session/list`, `session/get` not implemented** (CLOSED)  
   **Why it matters:** Previously blocked historical session loading in Zed. Resolved by [#2132](#), which replays wire history on load. A key integration win.

---

### 4. Key PR Progress
*Picked 10 of 14 PRs updated in the last 24h*

1. **[#2395] fix(compaction): filter empty text parts to avoid API 400**  
   **What it does:** Hotfix for [#2396](#). Extends the empty-text guard that was applied to tool messages in [#1663](#) to the compaction code path. Prevent data loss on export.

2. **[#2391] chore(release): bump kimi-cli to 1.46.0**  
   **What it does:** Prepares the next version tag. Locks release notes and syncs the `kimi-code` wrapper dependency.

3. **[#2047] fix(acp): load ~/.kimi/mcp.json in ACP server sessions**  
   **What it does:** High-impact fix. Currently `kimi acp` ignores user-defined MCP configs. This PR loads local tools so Zed users can use custom MCP servers.

4. **[#2132 (CLOSED)] fix(acp): replay session history on load**  
   **What it does:** Implements persistent wire history and replays it during `session/load`. Previously ACP sessions were empty on reconnect.

5. **[#2389] fix(tools): include trailing output in error briefs and render brief as plain text**  
   **What it does:** UX improvement. Failed shell commands now show the full tail of their output in the error summary, making debug much easier.

6. **[#2388] fix(shell): persist pasted text placeholders**  
   **What it does:** Fixes a data-loss edge case where `[Pasted text #1]` placeholders were forgotten after session history recall.

7. **[#2386] fix(session): map undo wire turns to context turns**  
   **What it does:** Corrects the `/undo` index mapping. Previously, local slash-commands inside a turn could break undo and fork operations.

8. **[#2383] fix(soul): repair orphan tool_calls when replaying history**  
   **What it does:** Edge-case resilience. If `context.jsonl` contains a partial `assistant` message from a killed session, the replay no longer blocks.

9. **[#2382] fix(file): convert unsupported image formats to PNG in ReadMediaFile**  
   **What it does:** Transparently converts `.ico`, `.bmp`, etc. to `.png` before sending to the model. Closes a long standing feature gap in image support.

10. **[#2369] feat(subagent): add API key pool for parallel subagent execution**  
    **What it does:** Introduces a round-robin `APIKeyPool`. Enables parallel subagent workflows without hitting per-key rate limits.

---

### 5. Feature Request Trends

- **ACP Protocol Maturity**  
  The loudest signal is demand for complete ACP support. Users expect session history persistence, token usage reporting, and local MCP tool loading to work out of the box in editor integrations. Every gap here (e.g., [#2394](#), [#2127](#)) impacts trust in the “Kimi as an external agent” workflow.

- **Codex Feature Parity**  
  Nested skill directories ([#1894](#)) and broader image support ([#2382](#)) are the clearest examples. The community sees Codex as the competitive benchmark and expects Kimi to match its configuration flexibility.

- **Scalability Infrastructure**  
  Configurable timeouts ([#2384](#)), API key pools ([#2369](#)), and token usage transparency ([#2394](#)) all point to a growing power-user segment using Kimi for long-running, multi-agent sessions. This group is pushing the tool beyond simple chat.

---

### 6. Developer Pain Points

- **Strategic Fragmentation Anxiety**  
  Issue [#2381](#) is more than noise — it reflects a real trust deficit. Users invested time in `kimi-cli` and feel blindsided by the `kimi-code` split. Without clear leadership messaging, the community is questioning the longevity of both projects.

- **Stability Around IDE Integration**  
  Despite progress, the ACP path remains fragile. Infinite loops in file search ([#2385](#)), missing session history, and MCP loading failures ([#2047](#)) make the “Kimi inside Zed” experience feel like early beta, not production-ready.

- **Hard-Coded Bottlenecks**  
  The HTTP client timeout ([#2384](#)) is emblematic of a broader frustration: users are hitting hard-coded limits that prevent Kimi from working in exactly the scenarios it was designed for (large-context, long-running sessions).

- **Data Integrity Edge Cases**  
  The compaction export crash ([#2396](#)) and orphaned `tool_calls` ([#2383](#)) reveal that the session persistence layer, while clever, still has rough edges that can lose work if the process is killed or runs a long session.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

**OpenCode Community Digest — 2026-05-29**

---

### 1. Today's Highlights
OpenCode **v1.15.12** shipped today, adding experimental WebSocket transport for OpenAI models and deeper ACP integration via `acp-next`. Community attention is heavily focused on **GPT model latency variance** (#29079, 104 comments), while the PR queue saw critical fixes for **MCP auth file corruption** (#29820) and **parallel sub-agent dispatch** (#29819). The long-running demand for an official **VS Code extension** (#11176) remains the most-upvoted feature request by a wide margin.

---

### 2. Releases
**v1.15.12** — [Release Notes](https://github.com/anomalyco/opencode/releases/tag/v1.15.12)
- **ACP Integrations**: Can now send prompts, slash commands, and usage updates through `acp-next`.
- **WebSocket Transport**: Added for OpenAI responses on supported channels. Enable with `OPENCODE_EXPERIMENTAL_WEBSOCKETS=true`.
- **Adaptive Reasoning**: Enabled adaptive reasoning controls for Anthropic models.

---

### 3. Hot Issues (Top 10 Noteworthy)

| Issue | Title / Relevance | Community Signal |
|---|---|---|
| [#29079](https://github.com/anomalyco/opencode/issues/29079) | **GPT Models take too long to respond** — Wildly variable latency (seconds vs. minutes) for simple prompts. Top engagement driver today. | 104 comments, 48 👍 |
| [#28846](https://github.com/anomalyco/opencode/issues/28846) | **Adjust Go usage limits after DeepSeek V4 Pro 75% price cut** — Community expects subscription savings to be passed through. | 28 comments, 46 👍 |
| [#11176](https://github.com/anomalyco/opencode/issues/11176) | **Official VS Code extension** — Longest-running, highest-voted request. Desktop-only is a dealbreaker for many core devs. | 18 comments, 91 👍 |
| [#27530](https://github.com/anomalyco/opencode/issues/27530) | **"4 of 5 requests failed" on startup** — Server error blocks new users immediately. Major onboarding friction. | 19 comments, 10 👍 |
| [#28686](https://github.com/anomalyco/opencode/issues/28686) | **V2 UI hides prompt controls and status popover** — Regression in Desktop beta; agent/model/thinking selectors vanish. | 2 comments, 4 👍 |
| [#29779](https://github.com/anomalyco/opencode/issues/29779) | **write/edit tools silently abort for files >~6KB** — No fallback or error message, just `Tool execution aborted`. High frustration. | 2 comments |
| [#29571](https://github.com/anomalyco/opencode/issues/29571) | **Conversation permanently stuck after "vision is not enabled" error** — No recoverability from Copilot provider policy blocks. | 5 comments, 1 👍 |
| [#29727](https://github.com/anomalyco/opencode/issues/29727) | **Skill permissions not enforced** — `opencode.json` allow/deny rules are ignored; all skills visible regardless. | 3 comments |
| [#29764](https://github.com/anomalyco/opencode/issues/29764) | **LLM-ordered file deletion** — Users report agents nuking files with no undo or recovery mechanism. | 3 comments |
| [#29808](https://github.com/anomalyco/opencode/issues/29808) | **Desktop UI toggle buttons disappear** — New layout flags cause permanent disappearance of file tree and review toggles. | 2 comments |

---

### 4. Key PR Progress (Top 10)

| PR | Summary | Impact |
|---|---|---|
| [#29819](https://github.com/anomalyco/opencode/pull/29819) | **Parallel sub-agent dispatch** — `runLoop` now spawns subtasks concurrently instead of one-at-a-time. | Drastically reduces latency for complex multi-step tasks. |
| [#29820](https://github.com/anomalyco/opencode/pull/29820) | **Serialize mcp-auth.json writes** — Fixes concurrent corruption of token storage. | Critical stability fix for MCP token refresh races. |
| [#29815](https://github.com/anomalyco/opencode/pull/29815) / [#29818](https://github.com/anomalyco/opencode/pull/29818) | **Skip persisting empty text parts** — Models jumping straight from `text-start` to tool call no longer create blank message bubbles. | Cleaner UI when using planning agents with Sonnet. |
| [#29217](https://github.com/anomalyco/opencode/pull/29217) | **Inline `$skill` invocations in TUI** — Autocomplete + execution from the prompt composer. | Major power-user UX improvement for skill workflows. |
| [#29755](https://github.com/anomalyco/opencode/pull/29755) | **Enforce read deny rules in glob/grep** — Fixes bugs where `**/.env*` deny patterns were silently ignored. | Critical secret-leak prevention fix. |
| [#29812](https://github.com/anomalyco/opencode/pull/29812) | **Desktop menu: Open Config File** — Adds menu item and command palette action. | Quality of life for frequent config tweakers. |
| [#29710](https://github.com/anomalyco/opencode/pull/29710) | **Fix prompt corruption with wide characters** — Pasting near Unicode chars no longer breaks the prompt. | Important international/Unicode UX fix. |
| [#27654](https://github.com/anomalyco/opencode/pull/27654) | **Subagent permission override fix** — Explicit `edit:allow` in subagents now correctly beats inherited parent `edit:deny`. | Fixes broken permission model inheritance. |
| [#29805](https://github.com/anomalyco/opencode/pull/29805) | **Animate pending inline tools** — Adds spinner while tools load, removes static "Delegating..." status. | UI polish for inline tool workflows. |
| [#29803](https://github.com/anomalyco/opencode/pull/29803) | **Bump node-pty to fix Windows crash** — Stops repeated sidecar crash/stderr flood on Windows Desktop. | Resolves a persistent Windows platform bug. |

---

### 5. Feature Request Trends
- **IDE Adjacency** (#11176, #29763): The overwhelming call remains for **native editor integration** (VS Code) and even **Android support**. The desktop-first model is seen as limiting.
- **Native Scheduling** (#11232): Users want cron-style recurring tasks built in, not platform crontab hacks.
- **Integrated Browser Workspace** (#26772): A first-class browser panel inside the Desktop app for live web inspection, indicating demand for a combined dev environment.
- **Dynamic Pricing & Quotas** (#28846, #29642): A vocal segment of users expects usage limits and Go subscription prices to automatically reflect provider API cost changes (DeepSeek cuts, Mimo increases).
- **Skill System Expansion**: Multiple issues target better skill configuration—permissions (#29727), serialization formats (#24852), and inline invocation (#29217).

---

### 6. Developer Pain Points
- **Performance Unpredictability**: The #1 active frustration. GPT models exhibit *seconds-to-minutes* variance on trivial tasks (#29079). This erodes trust in model responsiveness.
- **UI Regression Churn**: The Desktop V2 rollout is causing significant **loss of controls** — model selectors, reasoning toggles, and file tree buttons are disappearing under feature flags (#28686, #29051, #29808).
- **Silent Failures & Data Loss**: Write/edits aborting without feedback (#29779), LLMs deleting user files (#29764), and conversations getting permanently stuck (#29571) are the highest-severity reliability issues.
- **Onboarding Friction**: The "Unexpected server error" on first boot (#27530) combined with tricky OAuth setups (#29787, #15109) creates a high barrier to entry for new users.
- **Permission Complexity**: The deny/allow permission model is hard to get right, leading to either overly permissive agents or broken configs (#29727, #27654).
- **Platform Parity**: The nightly Windows Desktop crash (#29803) and Copilot-specific errors (#29571) highlight gaps in cross-platform provider support.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

**Pi Community Digest – 2026-05-29**  
*Based on data from `github.com/badlogic/pi-mono` (Issues/PRs tracked at `earendil-works/pi`)*

---

### 1. Today's Highlights
Pi v0.77.0 shipped with Claude Opus 4.8 support and the highly-requested `--exclude-tools` flag for selective tool disablement. A critical hotfix series resolved the "file review diff empty" root cause, where subagent Git garbage collection was deleting blobs needed by the main session. Meanwhile, the community rallied around a major provider expansion (Ant-ling Ling/Ring 2.6 model series) and the first RFC for remote-control extension APIs, signalling a push to evolve Pi beyond a pure TUI tool.

---

### 2. Releases
**v0.77.0**  
- **Claude Opus 4.8 support** – Adds full metadata and adaptive-thinking coverage for Anthropic's latest model.  
- **`--exclude-tools` / `-xt` flag** – Users can now selectively disable specific built-in, extension, or custom tools at startup without removing the rest.

---

### 3. Hot Issues (Top 10)

1. **#4945 – [OPEN] openai-codex can hang on `Working...` with zero-usage aborted turns**  
   *45 comments, 22 👍*  
   The most-discussed bug in the tracker. The OpenAI Codex / gpt-5.5 provider intermittently leaves the TUI stuck on "Working..." with no streaming output, tool calls, or errors. Recovery requires pressing Escape, which logs an aborted turn. The volume of community engagement points to a systemic reliability problem in the Codex integration.  
   `earendil-works/pi Issue #4945`

2. **#5148 – [CLOSED] Resuming ChatGPT 5.5 after Claude Opus 4.7 extended thinking returns 400**  
   *4 comments, 6 👍*  
   Switching from a Claude session (with extended-thinking turns) to OpenAI's gpt-5.5 corrupts the session state with a duplicate message ID (`msg_17`), triggering a 400 on resume. A clear cross-provider state serialization failure that undermines multi-model workflows.  
   `earendil-works/pi Issue #5148`

3. **#5087 – [CLOSED] GPT-5.5 context window is capped at 272K**  
   *4 comments*  
   Pi reports a 272K context window for gpt-5.5, but OpenAI docs and Shopify AI Proxy metadata both show 1,050,000 tokens. Users relying on long-context tasks are silently truncated—a straightforward metadata misconfiguration with significant downstream impact.  
   `earendil-works/pi Issue #5087`

4. **#5129 – [OPEN] `ctx.ui.custom(factory)` without `overlay:true` bricks any open sibling overlay**  
   *3 comments*  
   A subtle extension API state bug. Calling `ctx.ui.custom()` without the `overlay: true` option while another overlay is active makes the original overlay permanently unresolvable. Extension developers should consider this a critical UX blocker when composing custom UIs.  
   `earendil-works/pi Issue #5129`

5. **#5117 – [OPEN] Qwen 3.7 Max on OpenRouter is broken**  
   *3 comments*  
   Users hitting a 400 error due to an invalid `developer` message role in Qwen 3.7 Max requests. A provider-specific mapping failure that completely blocks the model.  
   `earendil-works/pi Issue #5117`

6. **#5103 – [OPEN] Windows bash detector fails when Git Bash is on PATH but not under `C:\Program Files`**  
   *3 comments*  
   Pi's built-in bash tool prefers a hardcoded `C:\Program Files` path over standard PATH resolution. Any Windows user with Git Bash on a non-default drive (e.g., `D:\Program Files`) will see "no bash shell found".  
   `earendil-works/pi Issue #5103`

7. **#5145 – [CLOSED] Skills with a `.gitignore` file in their directory are not discovered by Pi**  
   *4 comments*  
   Adding a `.gitignore` containing `*` to a skill directory causes Pi’s skill loader to completely skip the directory—even when `SKILL.md` itself is not git-ignored. A surprising anti-pattern that breaks version-controlled skill distribution.  
   `earendil-works/pi Issue #5145`

8. **#5102 – [OPEN] IME candidate window misplaced when slash-command autocomplete is active**  
   *2 comments*  
   CJK input method users report their IME candidate window is repositioned (often far below the cursor) when the `/` slash-command autocomplete menu appears. A critical quality-of-life issue for the international user base.  
   `earendil-works/pi Issue #5102`

9. **#5098 – [OPEN] Inline images and arrow keys broken inside tmux**  
   *2 comments*  
   `detectCapabilities()` unconditionally returns `images: null` when `$TMUX` is set, even when the parent terminal supports image protocols. Combined with broken arrow keys, it makes Pi nearly unusable inside tmux for power users.  
   `earendil-works/pi Issue #5098`

10. **#4801 – [CLOSED] Error: 400 `reasoning_effort` for DeepSeek v4 pro `xhigh` on OpenRouter**  
    *7 comments*  
    Passing `reasoning_effort: "xhigh"` for DeepSeek models on OpenRouter returns a 400 despite "xhigh" being a valid enum value. Highlights the ongoing challenge of correctly mapping Pi's standardized options across diverse provider APIs.  
    `earendil-works/pi Issue #4801`

---

### 4. Key PR Progress (Top 10)

1. **#5139 – fix(coding-agent): file review diff empty root cause fix + v0.74.56 release**  
   `InternalGit.gc()` was rewritten to auto-protect tree objects and referenced blobs. This is the long-awaited fix for the "file review returns null" bug caused by subagent GC deleting blobs needed by the main session.  
   `earendil-works/pi PR #5139`

2. **#5091 – fix(tui): harden keyboard protocol negotiation**  
   Maintainer `mitsuhiko` takes another pass at fixing #3259, improving how Pi negotiates keyboard protocols with the terminal for more reliable arrow key and special key handling.  
   `earendil-works/pi PR #5091`

3. **#5118 – fix(ai): buffer `reasoning_details` that arrive before `tool_calls`**  
   Providers like OpenRouter stream encrypted thought signatures (`reasoning_details`) before the `tool_calls` chunk. The pre-existing matching logic looked for tool call IDs that didn't exist yet, silently dropping signatures. This PR buffers them properly.  
   `earendil-works/pi PR #5118`

4. **#4971 – fix: add `allowEmptySignature` compat option for Anthropic-compatible providers**  
   Some Anthropic-compatible providers return thinking blocks with empty `thinkingSignature`. Previously these were rewritten as plain text, breaking prompt caching and causing 400 errors.  
   `earendil-works/pi PR #4971`

5. **#5155 – fix(tui): account tabs as 3 columns in overlay compositing**  
   Tab characters in overlay content (e.g., tab-indented source code popups) caused the TUI width guard to miscalculate, leading to fragmented lines and a smeared footer/status bar.  
   `earendil-works/pi PR #5155`

6. **#5029 – fix(coding-agent): abort in-flight LLM call on `AgentSession.dispose()`**  
   When a session is switched or disposed mid-stream (`switchSession`, `fork`, `clone`), the previous LLM HTTP request was left running. This change properly aborts it, preventing wasted API calls and potential race conditions.  
   `earendil-works/pi PR #5029`

7. **#4911 – feat(ai): add Codex device code login**  
   Implements a full device code flow for Codex authentication (closes #3424). Users now get a second authentication screen that works in headless or restricted environments where browser OAuth is impractical.  
   `earendil-works/pi PR #4911`

8. **#5107 / #4978 – feat(coding-agent): expose `streamingBehavior` on `InputEvent`**  
   Extends the extension API so input handlers can distinguish between initial prompts, mid-stream steers, and queued follow-ups. Enables more context-aware extensions that respond differently based on interaction type.  
   `earendil-works/pi PR #5107`

9. **#5110 – [OPEN] Add Ant-ling Provider with the Ling 2.6 / Ring 2.6 series**  
   A major new provider contribution supporting models up to 1T parameters via an OpenAI Completions compatibility layer. The community is watching this closely for what it signals about Pi's provider extensibility.  
   `earendil-works/pi PR #5110`

10. **#5140 – feat(extensions,tui): APIs for remote-control extensions (RFC)**  
    Introduces `ctx.executeInputLine(text)` and `pi.writeToEditor(text)` to the extension API surface. The explicit goal is enabling non-TUI remote clients—phone apps, web bridges, IDE plugins—to drive the Pi engine.  
    `earendil-works/pi PR #5140`

---

### 5. Feature Request Trends

- **Provider Ecosystem Expansion** – The community consistently pushes for first-class support for more backends. Recent requests target NVIDIA NIM, Anthropic Vertex AI, and Ant-Ling. Users want Pi to be a universal gateway without relying on third-party extensions for core connectivity.
- **Headless / Remote Platform** – A strong signal towards decoupling the Pi engine from the TUI frontend. Requests for `executeInputLine`, `writeToEditor`, and explicit remote-control APIs suggest developers are building custom interfaces (mobile, web, IDE) on top of Pi's agent infrastructure.
- **Tooling Introspection & Control** – Beyond the new `--exclude-tools` flag, users want provider-hosted tool support and richer discovery APIs (`getToolDefinition`). Extension authors are asking for the ability to inspect, call, and debug tools at a lower level.
- **Scriptability & CI Integration** – CLI flags for session naming (`--name`), file-based prompt loading (`@path` paths in `--system-prompt`), and better session filtering are recurring requests. Integration into automated scripting pipelines is clearly a priority use case.

---

### 6. Developer Pain Points

- **Provider API Inconsistency** – The sheer variety of LLM backends remains the #1 source of defects. Issues with tool call ordering (`reasoning_details` before `tool_calls`), non-standard message roles (`developer` vs `system`), shape conversion (`tool_choice`), and enum validation (`reasoning_effort`) dominate the tracker. Each new provider integration increases the maintenance surface.
- **Terminal Environment Fragility** – The TUI struggles with real-world terminal diversity. Specific pain points include tmux (broken images/keys), Windows Terminal (IME positioning, ANSI colors, Git Bash detection), and keyboard protocol negotiation. These regressions heavily impact power users from non-macOS environments.
- **Session State Management** – Users hit confusing state bugs: corrupt sessions when switching providers, compaction ignoring `transport` config, `readPipedStdin` timing leaking across async boundaries, and flat session storage when using `PI_CODING_AGENT_SESSION_DIR`. Debugging these is an overhead for both users and the core team.
- **Extension/Tool System Edge Cases** – The tool system has surprising failure modes: `.gitignore` in skill directories silently hides the skill, undefined `result.content` crashes the TUI, and system prompts list tools that don't exist. These bugs erode trust in the extension ecosystem's stability.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for May 29, 2026, based on the latest GitHub activity.

---

## Qwen Code Community Digest — 2026-05-29

### 1. Today's Highlights
Today’s activity was dominated by two major agentic strides: the merging of a **zero-config Computer Use** integration ([PR #4590](https://github.com/QwenLM/qwen-code/pull/4590)) and a deep refactor of the **session compaction model** ([PR #4599](https://github.com/QwenLM/qwen-code/pull/4599)). An urgent **SSL certificate error** on `coder.qwen.ai` ([#4612](https://github.com/QwenLM/qwen-code/issues/4612)) was raised and resolved quickly, while the community remains deeply engaged in shaping the **production roadmap for Mode B (serve daemon)** ([#4175](https://github.com/QwenLM/qwen-code/issues/4175)).

### 2. Releases
- **v0.16.1-nightly.20260529.7bed56b9b**: A new nightly build is out that fixes the CLI to surface startup warnings on stderr before the TUI renders ([#4448](https://github.com/QwenLM/qwen-code/pull/4461)). This improves debugging for headless/CI workflows.
- **TUI spacing density evidence**: A tag was cut with VHS/tmux captures comparing the current spacing in origin/main against the upcoming PR1 changes.

### 3. Hot Issues (Top 10)

1.  **[#4612](https://github.com/QwenLM/qwen-code/issues/4612) / [#4611](https://github.com/QwenLM/qwen-code/issues/4611) — SSL Certificate Invalid on coder.qwen.ai [URGENT]**
    A critical blocker raised by multiple users across networks and devices. The `ERR_CERT_AUTHORITY_INVALID` error blocked active development. Quickly resolved and closed by the team.

2.  **[#4175](https://github.com/QwenLM/qwen-code/issues/4175) — Mode B (`qwen serve`) Production Roadmap**
    The most active discussion (41 comments). Lays out the final work items (state caching, ACP alignment, telemetry) needed to graduate the daemon from functionally runnable to production-ready.

3.  **[#4493](https://github.com/QwenLM/qwen-code/issues/4493) — Rider IDE Login Failure (OAuth / Token Plan)**
    Users on JetBrains Rider cannot complete OAuth login; the redirect loop prevents applying Alibaba Cloud token plans. High frustration in the comments due to a broken IDE onboarding path.

4.  **[#3696](https://github.com/QwenLM/qwen-code/issues/3696) — [P1] Comprehensive Hot-Reload System**
    A long-running P1 request to enable runtime reloading of skills, extensions, MCP servers, and config files without restarting sessions. The tracking issue lists sub-tasks by dependency order.

5.  **[#2128](https://github.com/QwenLM/qwen-code/issues/2128) — [P1] Unbounded Memory Growth in UI History**
    Root-caused to a perpetually growing `useHistoryManager.history` array. Long-running sessions (dozens of hours) see unbounded RAM consumption, forcing periodic restarts.

6.  **[#4592](https://github.com/QwenLM/qwen-code/issues/4592) — Refactor Compaction to Summary + Restoration Model**
    Proposes replacing the current "summarize front 70%, preserve tail 30%" strategy with a Claude-Code-style full-history summary + restoration attachments. Gaining traction as a better long-context strategy.

7.  **[#4591](https://github.com/QwenLM/qwen-code/issues/4591) — Zero-Config Built-in Computer Use**
    A feature request to make desktop automation (click, scroll, type, drag) a first-class built-in skill on macOS, Windows, and Linux. Closely tied to the merged PR #4590.

8.  **[#4597](https://github.com/QwenLM/qwen-code/issues/4597) — Enhanced `/stats` with Cross-Session Persistence**
    Community asks for persistent usage analytics (token, tools, duration) written to `~/.qwen/usage-history.json`, with an interactive dashboard akin to Claude Code.

9.  **[#4593](https://github.com/QwenLM/qwen-code/issues/4593) — `/clear` Creates a New Session ID**
    A subtle but impactful bug: running `/clear` generates a fresh session ID instead of clearing the current session context. This breaks log correlation and session-based debugging workflows.

10. **[#4588](https://github.com/QwenLM/qwen-code/issues/4588) — TUI Display Optimization Epic**
    A tracking issue for making the CLI "quieter, denser, and more scannable." Targets spacing, tool output formatting, and Qwen-branded UI polish.

### 4. Key PR Progress (Top 10)

1.  **[#4599](https://github.com/QwenLM/qwen-code/pull/4599) — Refactor Core Compaction Model**
    Replaces the tail-preservation auto-compaction with a full-history summary + restoration-attachments model. A deep architectural change aimed at better long-session context retention. **Open.**

2.  **[#4590](https://github.com/QwenLM/qwen-code/pull/4590) — Zero-Config Built-in Computer Use**
    Delivers on the major request in [#4591]. Integrates an `open-computer-use` MCP server with nine native tools (`click`, `scroll`, `drag`, `type_text`, etc.). **Closed (Merged).**

3.  **[#4563](https://github.com/QwenLM/qwen-code/pull/4563) — Extract DaemonWorkspaceService from AcpSessionBridge**
    Decomposes the bloated `HttpAcpBridge` into a clean `DaemonWorkspaceService` facade with four internal sub-services (File, Auth, Agents, Memory). Critical architecture cleanup for Mode B. **Open.**

4.  **[#4608](https://github.com/QwenLM/qwen-code/pull/4608) — Add Telemetry Tool Spans to Daemon/ACP Path**
    Wraps `Session.ts` tool execution with `startToolSpan`/`endToolSpan` and adds `session.id` attributes, making daemon spans queryable in ARMS. **Open.**

5.  **[#4613](https://github.com/QwenLM/qwen-code/pull/4613) — Daemon Side-Channel State Layer (A1/A2/A5)**
    Introduces atomic state caching (`currentModelId`, `currentApprovalMode`) and post-roundtrip reconciliation to the daemon, reducing race conditions in concurrent sessions. **Open.**

6.  **[#4332](https://github.com/QwenLM/qwen-code/pull/4332) — Keep `/model` Switches Session-Scoped**
    Fixes a major UX pain point where `/model` changed persisted global settings instead of applying only to the current session. Adds `--default` flag for explicit persistence. **Closed (Merged).**

7.  **[#4603](https://github.com/QwenLM/qwen-code/pull/4603) — Web-Shell `/delete` Command with Batch Support**
    Adds a `POST /sessions/delete` daemon endpoint and corresponding CLI `/delete` command for cleaning up session data files. **Open.**

8.  **[#4552](https://github.com/QwenLM/qwen-code/pull/4552) — Runtime MCP Server Add/Remove**
    Implements mutate-gated HTTP routes (`POST /workspace/mcp/servers`) to add or replace MCP servers at runtime without restarting the daemon. **Open.**

9.  **[#4520](https://github.com/QwenLM/qwen-code/pull/4520) — Truncate Model-Facing Tool Output**
    Prevents oversized tool results from overflowing the context window. Truncated output is saved to temp files to avoid double-truncation. **Open.**

10. **[#4485](https://github.com/QwenLM/qwen-code/pull/4485) — Update `@google/genai` from v1 to v2**
    Major dependency bump (`1.30.0` -> `2.6.0`) to align with upstream SDK changes. **Open.**

### 5. Feature Request Trends

- **Daemon / Mode B Production Readiness:** The strongest signal is the push to make `qwen serve` robust. Nearly 20% of recent issues focus on state caching, telemetry alignment, workspace isolation, and runtime configuration for the serve daemon.
- **Session & Memory Architecture:** Developers are heavily invested in how Qwen Code manages context. The compaction overhaul ([#4592](https://github.com/QwenLM/qwen-code/issues/4592)), hot-reload ([#3696](https://github.com/QwenLM/qwen-code/issues/3696)), and persistent `/stats` ([#4597](https://github.com/QwenLM/qwen-code/issues/4597)) represent a collective push for smarter, more persistent session handling.
- **Agent Expansion:** The Computer Use capability ([#4591](https://github.com/QwenLM/qwen-code/issues/4591)) indicates the community is eager for Qwen Code to act beyond the IDE—on the entire desktop OS.
- **IDE Ecosystem Parity:** Users are actively requesting consistent behavior across VSCode, JetBrains (Rider, PyCharm), and terminal shells. Authentication, keybindings, and terminal signals are recurring friction points.
- **TUI Polish:** The terminal UI is maturing from "functional" to "pleasant." Requests for denser layouts, improved auto-mode indicators, and better tool output formatting are on the rise.

### 6. Developer Pain Points

- **Authentication & Infrastructure Hurdles:** The SSL issue on `coder.qwen.ai` ([#4612](https://github.com/QwenLM/qwen-code/issues/4612)) and the broken Rider OAuth flow ([#4493](https://github.com/QwenLM/qwen-code/issues/4493)) created hard blocks for developers trying to start sessions.
- **API Error Handling Fragility:** Users frequently hit cryptic errors like "Body Timeout" ([#4604](https://github.com/QwenLM/qwen-code/issues/4604)), "DOMException" with local models ([#4609](https://github.com/QwenLM/qwen-code/issues/4609)), and reasoning content errors. The lack of built-in exponential backoff ([#3004](https://github.com/QwenLM/qwen-code/issues/3004)) exacerbates API instability.
- **Session Lifecycle Rigidity:** The inability to hot-reload configs, the creation of new session IDs on `/clear` ([#4593](https://github.com/QwenLM/qwen-code/issues/4593)), and unbounded memory growth ([#2128](https://github.com/QwenLM/qwen-code/issues/2128)) force developers into frequent context-loss resets.
- **IDE/Terminal Integration Bugs:** PyCharm users report unintended agent exits from Ctrl+C ([#4586](https://github.com/QwenLM/qwen-code/issues/4586)), and VSCode users hit a `fetchFn` import compatibility issue ([#4589](https://github.com/QwenLM/qwen-code/issues/4589)), indicating platform-specific QA gaps.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-05-29

> **Note on naming:** The project has fully migrated from the codename "DeepSeek TUI" to **CodeWhale** (binary `codewhale`, config path `~/.codewhale/`). This digest reflects that shift while honoring the original DeepSeek TUI community.

---

## 1. Today's Highlights

The CodeWhale community saw intense churn around two critical areas: **Chinese input method (IME) compatibility** and **shell-tool security model consistency**. PR #2330 landed to fix IME-committed characters being swallowed in terminals without bracketed paste, directly addressing a top pain point for Chinese-speaking users. Concurrently, a cluster of issues and PRs (#2328, #2303, #2331) surfaced a confusing inconsistency where `exec_shell` works in YOLO mode but blocks in Agent mode, exposing holes in the security gate. On the feature front, the multi-provider push remains the strongest signal of the week, with the SiliconFlow PR (#1868) moving forward and custom API provider support (#2247) gathering the most community engagement.

---

## 2. Releases

No new GitHub releases were tagged in the last 24 hours.

---

## 3. Hot Issues (10)

**#2247 – Custom DeepSeek-Compatible API Providers / 支持自定义 DeepSeek 兼容 API 提供商**
*Author: hatakes | Comments: 4 | 👍: 0*
The most strategically requested feature this sprint. Users want to route CodeWhale through local deployments (vLLM, Ollama) or third-party services that speak the DeepSeek protocol. Directly blocks enterprise adoption where official DeepSeek API isn't viable.
[Link](Hmbown/CodeWhale Issue #2247)

**#2328 – `exec_shell` Mode Availability Inconsistency**
*Author: octasin | Comments: 1 | 👍: 0*
A documented tool that breaks completely in Agent mode while working fine in YOLO mode. This kind of silent regression erodes trust in the tool catalog and forces users to constantly test mode compatibility.
[Link](Hmbown/CodeWhale Issue #2328)

**#2323 – TUI Not Adapted for Chinese Input Method (IME)**
*Author: cmdcorp6534 | Comments: 1 | 👍: 0*
Detailed bug report showing pinyin composing leaks into the command area behind modal dialogs, and input in confirm/config screens appears in the model prompt instead of the text field. Blocks basic Chinese text composition.
[Link](Hmbown/CodeWhale Issue #2323)

**#2310 – Cannot Start Message with `/` (No Escape)**
*Author: zhyuzhyu | Comments: 1 | 👍: 0*
Any leading slash is unconditionally consumed by the slash-command parser. Users who want to send paths (`/home/user`), inline code, or Markdown naturally hit a hard wall in the composer.
[Link](Hmbown/CodeWhale Issue #2310)

**#2309 – `/statusline` Picker Only Shows Config-Listed Items**
*Author: zhyuzhyu | Comments: 2 | 👍: 0*
The statusline picker is effectively blind—it only surfaces items already present in `~/.codewhale/config.toml`. Users cannot discover the full palette of status chips through the UI at all.
[Link](Hmbown/CodeWhale Issue #2309)

**#2339 – `tool_search` Default Max_Results=5 Burys MCP Tools**
*Author: T-Phuong-Nguyen | Comments: 0 | 👍: 0*
When multiple MCP servers register tools with overlapping keywords, the 5-result cap hides relevant tools from other servers. Users request a sensible default of at least 20 results for real-world discovery.
[Link](Hmbown/CodeWhale Issue #2339)

**#2299 – GLIBC_2.39 Requirement Blocks Debian 12 / Deepin**
*Author: Jengro777 | Comments: 1 | 👍: 0*
The prebuilt binary requires `GLIBC_2.39`, blocking users on LTS distributions with `GLIBC_2.38`. A hard wall for anyone on stable Linux channels.
[Link](Hmbown/CodeWhale Issue #2299)

**#2327 – Copyright Concerns Over Unofficial VSCode Extensions**
*Author: VerrPower | Comments: 0 | 👍: 0*
Community governance issue: unofficial CodeWhale-branded extensions have appeared on the VS Code Marketplace. Users are confused about security and authenticity, requesting guidance from maintainers.
[Link](Hmbown/CodeWhale Issue #2327)

**#2300 – Feature Request: Multi-Model Support with Routing**
*Author: gavinwang668 | Comments: 0 | 👍: 0*
Asks for simultaneous configuration of multiple models (GLM, Qwen, GPT, vision models, OCR, embeddings) with automatic task routing. Touches documentation clarity on provider types (`vllm` vs `openai`) and the gap between OpenAI chat API and responses API.
[Link](Hmbown/CodeWhale Issue #2300)

**#1675 – Chinese Garbled Characters in Agent Real-Time Output**
*Author: AiurArtanis | Comments: 2 | 👍: 0*
Persistent encoding issue when generating content (Obsidian/Word docs) from Agent mode. Characters render as garbled text, making agent-driven document generation unreliable for Chinese-language output.
[Link](Hmbown/CodeWhale Issue #1675)

---

## 4. Key PR Progress (10)

**#2330 – fix(tui): Route IME-Committed Chinese Characters Directly to Composer**
*Author: donglovejava*
The exact fix for #2323. Prevents IME input from being intercepted by the paste-burst heuristic in terminals without bracketed paste (Windows Terminal first session, SSH, tmux). Users on affected platforms will finally see their typed Chinese appear in the composer.
[Link](Hmbown/CodeWhale PR #2330)

**#2338 – feat: Whale-Size Route Taxonomy for Model + Thinking-Effort Picker**
*Author: encyc*
Closes #2026. Introduces a central whale-species label mapping `(model, reasoning_effort)` pairs sorted from largest/deepest to smallest/fastest. The `/model` picker now presents a single-column, physically intuitive selection hierarchy.
[Link](Hmbown/CodeWhale PR #2338)

**#2336 – feat: Add `/cache stats` — Prefix Hash/Drift Exposure and Cache-Hit Summary**
*Author: encyc*
New diagnostic command exposing prefix stability (percentage, check/change counts, drift warnings), SHA-256 combined hash, and cache-hit summaries. Essential for debugging prompt caching behavior in long sessions.
[Link](Hmbown/CodeWhale PR #2336)

**#2340 – fix(tui): Treat Slash-Space Input as Message Text**
*Author: nightt5879*
Solves #2310. Allows `/ ` to pass through as normal text instead of a command dispatch. Keeps bare `/` and known commands (`/help`, `/model`) on the existing command path. Includes regression coverage for edge cases.
[Link](Hmbown/CodeWhale PR #2340)

**#2331 – fix(tools): Eagerly Load All `exec_shell` Companion Tools**
*Author: donglovejava*
Adds `exec_interact`, `exec_shell_interact`, `exec_shell_wait`, `exec_wait`, `task_shell_start`, `task_shell_wait` to `DEFAULT_ACTIVE_NATIVE_TOOLS`. Directly addresses the mode inconsistency from #2328 by ensuring all shell companion tools are loaded in Agent mode.
[Link](Hmbown/CodeWhale PR #2331)

**#2329 – fix(tui): Skip Hidden Worktrees in Workspace Discovery**
*Author: donglovejava*
Prevents TUI saturation when sub-agents fan out during release work. Hidden git worktrees (`.claude/worktrees/`, `.worktrees/`) are now skipped, drastically reducing disk I/O and load times in large repositories.
[Link](Hmbown/CodeWhale PR #2329)

**#2326 – feat: Enforce Allowed Tools for Custom Slash Commands**
*Author: aboimpinto*
Phase 1 of the custom slash command lifecycle / hooks architecture. Parses frontmatter for `description`, `argument-hint`, and `allowed-tools`. Surfaces custom command descriptions in slash autocomplete, paving the way for strict tool permission boundaries.
[Link](Hmbown/CodeWhale PR #2326)

**#2325 – fix: Approval Dialog Shows Empty Params Instead of Actual Tool Arguments**
*Author: zlh124*
Fixes a dangerous UX bug where the tool-approval dialog rendered `{}` instead of actual arguments. Root cause: `pending_tool_uses` was drained by `MessageComplete` before `ApprovalRequired` arrived. Users were potentially approving blind operations.
[Link](Hmbown/CodeWhale PR #2325)

**#2324 – fix(statusline): Keep Picker Selection Visible**
*Author: reidliu41*
Addresses #2309. Ensures the statusline picker correctly scrolls the selection cursor so it doesn't disappear when navigating below the visible modal area.
[Link](Hmbown/CodeWhale PR #2324)

**#1868 – [codex] Add SiliconFlow Provider Support**
*Author: Lee-take*
A concrete demonstrator of the multi-provider architecture. Wires SiliconFlow as a first-class provider across CLI, config, secrets, TUI selection, docs, and examples. Treats SiliconFlow streamed reasoning content like other providers.
[Link](Hmbown/CodeWhale PR #1868)

---

## 5. Feature Request Trends

- **Multi-Provider & Model Flexibility (Dominant):** The community is actively pushing CodeWhale from a DeepSeek-specific client to a universal coding agent frontend. Requests span custom API providers (#2247), multi-model configuration with auto-routing (#2300, #2337), and concrete third-party integrations like SiliconFlow (#1868).
- **Customization & Discoverability:** Users want total visibility into their environment. The `/statusline` picker should show all options (#2309), custom slash commands should have permission models (#2326), and model selection should be intuitive (#2338).
- **Performance & Caching Diagnostics:** Long session users are demanding cache transparency. The arrival of `/cache stats` (#2336) and concerns about tool search results buried in multi-MCP setups (#2339) show a maturing user base focused on production reliability.

---

## 6. Developer Pain Points

- **Chinese Locale & IME Deficiencies:** The single biggest friction point for a large segment of the user base. IME input leaks into command areas (#2323); agent output garbles Chinese characters (#1675); right-click menus ignore locale settings (#2307). CodeWhale's terminal agnosticism is struggling with non-Latin workflows.
- **Shell Security Model Inconsistency:** The `allow_shell` / `exec_shell` / `task_shell_start` interplay is confusing and broken. Tools that work in YOLO mode fail silently in Agent mode (#2328). Security gates are inconsistent: `allow_shell` blocks `exec_shell` but not `task_shell_start` (#2303). Users cannot reliably predict tool behavior across modes.
- **Platform Compatibility Walls:** The hard `GLIBC_2.39` requirement (#2299) and persistent Docker garbled output issues (#1615) create painful onboarding for Linux users on LTS distributions and containerized environments.
- **Documentation Drift:** The migration from `~/.deepseek/` to `~/.codewhale/` has left official docs referencing legacy paths (#2322/2321). New users following the "official" docs land in wrong config directories, causing confusion and misconfiguration.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*