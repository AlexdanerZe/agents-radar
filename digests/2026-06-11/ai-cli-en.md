# AI CLI Tools Community Digest 2026-06-11

> Generated: 2026-06-11 03:38 UTC | Tools covered: 9

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

**Cross-Tool Comparison Report: AI CLI Ecosystem Snapshot (2026-06-11)**

---

### 1. Ecosystem Overview

The AI CLI tools market has hardened from experimental prompting into a high-stakes production engineering domain, where communities are demanding deterministic agent orchestration, transparent cost controls, and enterprise-grade security postures. While extensibility via the Model Context Protocol (MCP) has become universal, implementation friction around OAuth, type coercion, and startup sequencing remains the ecosystem’s primary integration bottleneck. A clear strategic divergence is emerging: vertically integrated tools optimizing for their model families (Claude Code, Gemini CLI) compete with universal provider hubs (OpenCode, Qwen Code, CodeWhale) that treat model access as an interchangeable commodity. Across the board, the failure mode shifting from “model hallucination” to “agent deadlock and cost leakage” is forcing a deep investment in observability, budgeting, and safety guardrails.

---

### 2. Activity Comparison

| Tool | Notable Hot Issues | Key PRs (24h) | Release Status (24h) | Velocity Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 10 | ✅ **v2.1.172** (Deep Sub-Agent Nesting, Bedrock fix) | High |
| **OpenAI Codex** | 10 | 10 | ✅ **2x Rust Alphas** (v0.140.0-a.4, a.7) | Very High (Dev Branch) |
| **Gemini CLI** | 10 | ~10 | ❌ No new release | Very High (Bug Squashing) |
| **GitHub Copilot CLI** | 10 | **0** | ❌ v1.0.60 stable | Low (Stabilizing) |
| **Kimi Code CLI** | 10 | 10 | ❌ v0.12.0 regressions | High (Reliability Fixes) |
| **OpenCode** | 10 | 10 | ✅ **3x Releases** (v1.17.1, .2, .3 Hotfix) | Very High (Iteration Speed) |
| **Pi** | 10 | ~10 | ❌ No new release | High (Enterprise Features) |
| **Qwen Code** | 10 (27 total) | 10 (50 total) | ❌ v0.17.1 stable | Very High (Architectural Shift) |
| **CodeWhale (DeepSeek)** | 10 | ~10 | ✅ **v0.8.57** (Rebrand release) | High (Transition Phase) |

---

### 3. Shared Feature Directions

**Deterministic Agent Autonomy**
*Prerequisite across Claude Code, Kimi Code, OpenCode, CodeWhale, Gemini CLI.*
Communities are demanding reliable unattended operation: true zero-prompt YOLO modes, hard kill-switches for runaway sub-agents, and failure-resilient task loops. The market will no longer tolerate “false success” status reporting (Gemini CLI #22323, CodeWhale #2989) or silent deadlocks on final task items (Kimi Code #2447, Copilot CLI #3547).

**Intelligent Context Window Management**
*Convergence across OpenAI Codex, Gemini CLI, Qwen Code, Pi.*
Users refuse to subsidize token waste through opaque context handling. The response is multi-layered: agent-visible token budgets (Codex #27438), lossless compression hash tracking (Codex #27520), lightweight non-LLM compaction commands (Qwen Code `/compress-fast`), and AST-aware file reads to reduce noise (Gemini CLI #22745).

**MCP Ecosystem Stability & Governance**
*Cross-cutting pain point: Claude Code, Qwen Code, Copilot CLI, OpenCode, Kimi Code.*
MCP adoption is assumed, but implementation friction is the bottleneck. Top remediation requests include: stable OAuth token handshake (Claude Code #46140), numeric string type coercion for strict servers (Qwen Code #4966), persistent MCP headers through debug/auth transport (OpenCode #31802), and policy-based MCP blocking resolution (Copilot CLI #1707/#3756).

**Hardened Cross-Platform Parity (Windows, ARM64, Wayland)**
*Universal demand, highest active patching in Kimi Code, Qwen Code, OpenCode.*
Windows continues to be the primary second-class platform: tool drops, crash-on-launch builds, PopOS console windows, and non-ASCII username failures. Linux Wayland compatibility (Gemini CLI #21983) and ARM64 Cowork support (Claude Code #50674) represent secondary but growing attack surfaces.

**Persistent Session & State Resilience**
*High priority for Kimi Code, OpenCode, CodeWhale, OpenAI Codex.*
Session integrity is table stakes for long-running agentic workflows. Users require crash-resistant serialization (Kimi Code #2336), robust undo/redo across slash commands (Kimi Code #2386), persistent browsable session panels (CodeWhale #2934), and reliable resume from stale metadata (Kimi Code #2222).

---

### 4. Differentiation Analysis

**Vertically Integrated Model Optimizers** (Claude Code, Gemini CLI, OpenAI Codex)
- *Technical Approach:* Optimize agent logic, caching, and tooling for their proprietary model family.
- *Key Bets:* Claude Code is leaning hardest into deep agentic hierarchy (5-level nest). Gemini CLI distinguishes on pre-emptive security (IPI, SSRF, path traversal patches) and evaluation rigor (component-level agent evals #24353). OpenAI Codex is investing deeply in context window as a managed resource (budgets, compaction hashes, context tools).
- *Implicit Tradeoff:* Deeper model integration capabilties, but a theoretical risk of provider lock-in that communities are beginning to raise (Qwen Code #4904, Copilot CLI #1703).

**Universal Agent Hubs** (OpenCode, Qwen Code, Pi, CodeWhale)
- *Technical Approach:* Provider-agnostic architectures prioritizing broad model support and deep extensibility.
- *Key Bets:* OpenCode is executing a major TUI 2.0 refactor (#31796) while positioning as a universal frontend (Cursor CLI interop #2072). Qwen Code is undergoing a massive architectural shift to a daemon/client model (+115k LOC, #4490). Pi is carving a niche with enterprise proxy support (Palantir Foundry #5609) and internationalized TUI excellence. CodeWhale is aggressively decoupling from DeepSeek through a deterministic hooks/policy engine (Hooks v2, #3049).
- *Implicit Tradeoff:* Flexibility and provider optionality, but integration depth with any single model may lag, and architectural complexity (daemon mode, API parity) introduces its own stability risks.

**Ecosystem-Bridged Tools** (GitHub Copilot CLI, Kimi Code CLI)
- *Technical Approach:* Tied to existing developer platforms (GitHub, MoonshotAI ecosystem).
- *Key Bets:* Copilot CLI leverages an enormous user base but is currently struggling with regression velocity and community trust erosion. Kimi Code CLI is methodically patching Windows and session resilience to build reliability credibility.
- *Implicit Tradeoff:* Lowest friction for existing platform users, but highest vulnerability to platform-specific policies and perceived feature gaps versus standalone hubs.

---

### 5. Community Momentum & Maturity

**Highest Iteration Velocity:**
- **OpenCode** leads in raw release cadence (3 releases in 24h, including a hotfix) alongside a deep architectural TUI refactor.
- **Claude Code** shipped a major release with deep sub-agent orchestration while concurrently managing a heavy PR queue.
- **Qwen Code** executed the largest single code change (daemon mode merge) while servicing a broad issue load.

**Maturing Under Governance Pressure:**
- **OpenAI Codex** is generating strong engineering signal on context management features but faces a trust crisis over token burn (#14593, 604 comments).
- **Gemini CLI** is publishing the most aggressive security patches (IPI, SSRF, path traversal) and deepening its evaluation pipelines—a strong enterprise readiness signal.

**Stabilizing / At Risk:**
- **GitHub Copilot CLI** reported zero PRs in 24 hours. The community’s longest-running issue (#53, 75 👍) remains unanswered, and the 1.0.x regression cycle has slowed feature velocity in favor of stabilization. This creates a mindshare gap for third-party forks.

---

### 6. Trend Signals (Implications for Decision-Makers)

**1. Cost Visibility is the #1 UX Battlefront**
The Codex #14593 supernova (600+ comments) is a market-level signal. Tools that fail to surface per-turn budgets, agent-visible context windows, and actionable cost telemetry will face a trust deficit. Expect token budget protocols and compaction tools to become table stakes by year-end.

**2. Sub-Agent Reliability is the New API Reliability**
Users are treating sub-agents as microservices. False success states (Gemini #22323, CodeWhale #2989), silent deadlocks (Kimi #2447), and ignored stop commands (Claude #67321) are breaking complex workflows. Robust circuit breakers, lifecycle observability, and deterministic turn limits are now critical for any tool targeting production use.

**3. Pre-Emptive Security is a Definitive Competitive Moat**
Gemini CLI’s concurrent patching of IPI truncation bypass (#27472), SSRF hostname resolution (#27473), and skill path traversal (#27767) sets a new baseline for tool safety. With tools granted code execution, enterprises will systematically exclude offerings that lag on security-by-design.

**4. Windows Support is a Market Share Gate**
The density and severity of Windows-specific issues across *every* major tool constitute a collective market failure. The first tool to ship truly stable, performant Windows support with full terminal/process parity will capture significant share of the enterprise developer segment.

**5. The “MCP Honeymoon” is Over – Standardization is Due**
Adoption is high, but friction is rising. OAuth handshake gaps, type coercion failures, and policy mis-handling dominate integration pain points. Developers adopting MCP should budget for ongoing debugging overhead until the ecosystem converges on stricter implementation contracts.

**6. The CLI is Becoming the IDE**
Feature sets are converging: structured session goals (/goal), persistent memory, AST-aware codebase mapping, plugin hooks, and TUI polish. Differentiation is no longer about feature lists but execution quality—reliability, performance, transparency, and trust. The winners will minimize cognitive overhead and maximize deterministic outcomes.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-11 | **Source:** github.com/anthropics/skills

---

### 1. Top Skills Ranking
Curated from the most-active Pull Requests by strategic weight and community engagement.

**1. Agent-Creator (#1140)** — *SyedaQurratAI* | **Status:** Open
**Function:** Meta-skill for creating task-specific agent sets; includes a critical fix for parallel multi-tool evaluation (`evaluation.py`) and Windows path support (`recalc.py`). Directly resolves Issue #1120.
**Discussion highlights:** Represents the strongest signal for multi-agent orchestration within the ecosystem. The parallel tool-call bug fix was widely anticipated by evaluation engineers.
[Link](https://github.com/anthropics/skills/pull/1140)

**2. Skill Quality & Security Analyzers (#83)** — *eovidiu* | **Status:** Open
**Function:** Two meta-skills offering quantitative quality scoring (structure, documentation, examples) and security auditing for other Skills across five dimensions.
**Discussion highlights:** This is infrastructure for ecosystem governance. Directly addresses demands raised in Issues #202 (skill-creator quality) and #492 (namespace security).
[Link](https://github.com/anthropics/skills/pull/83)

**3. Testing-Patterns (#723)** — *4444J99* | **Status:** Open
**Function:** Comprehensive testing skill covering the full stack: Testing Trophy model, AAA unit pattern, React Testing Library, edge cases, and what *not* to test.
**Discussion highlights:** Broad developer appeal. Positions Skills as a solution for automated testing discipline rather than just content generation.
[Link](https://github.com/anthropics/skills/pull/723)

**4. Sensory (macOS) (#806)** — *AdelElo13* | **Status:** Open
**Function:** Native macOS automation via `osascript` (AppleScript) with a two-tier permission system (direct app scripting vs. Accessibility API).
**Discussion highlights:** Sparks a debate on security patterns vs. convenience. A high-impact skill that bypasses screenshot-based computer use for native agentic control.
[Link](https://github.com/anthropics/skills/pull/806)

**5. Document Typography (#514)** — *PGTBoos* | **Status:** Open
**Function:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.
**Discussion highlights:** A universally applicable quality-of-life fix. Its specificity highlights the gap between generative output and production-ready layout.
[Link](https://github.com/anthropics/skills/pull/514)

**6. Shodh-Memory (#154)** — *varun29ankuS* | **Status:** Open
**Function:** Persistent memory system maintaining structured context across conversations using a `proactive_context` retrieval mechanism.
**Discussion highlights:** Taps directly into the highest-demand architectural gap: agentic memory and session continuity across bounded contexts.
[Link](https://github.com/anthropics/skills/pull/154)

**7. ODT Skill (#486)** — *GitHubNewbie0* | **Status:** Open
**Function:** Authoring, template filling, and parsing of ISO-standard OpenDocument Format (.odt/.ods). Supports document conversion to HTML.
**Discussion highlights:** Strong enterprise demand for open-standard document workflows, complementing the existing DOCX/PDF skills.
[Link](https://github.com/anthropics/skills/pull/486)

**8. SAP-RPT-1-OSS Predictor (#181)** — *amitlals* | **Status:** Open
**Function:** Integrates SAP's open-source tabular foundation model for predictive analytics on business data.
**Discussion highlights:** Enterprise business intelligence focus. Demonstrates appetite for specialized statistical models invoked through the Skills interface.
[Link](https://github.com/anthropics/skills/pull/181)

---

### 2. Community Demand Trends
Derived from the most-commented Issues (50 total, top 15 shown).

- **Enterprise Governance & Distribution**  
  Issue **#228** (13 comments, 7 👍) demands org-wide skill sharing without manual .skill file transfers. Issue **#492** (7 comments) flags a serious trust-boundary vulnerability: community skills distributed under the `anthropic/` namespace. Together, these are the community's strongest signal for formal admin controls and provenance verification.

- **Reliable Evaluation & Toolchain Stability**  
  Issues **#556** (12 comments) and **#1169** document a 0% trigger rate in `run_eval.py`—the optimization loop reports `precision=100%, recall=0%` on every iteration. Issue **#202** (8 comments) critiques the `skill-creator` meta-skill as too verbose and human-educational rather than operational. The community is impatient with tooling fragility and demands a self-consistent meta-skill standard.

- **Agent Memory & Multi-Agent Architecture**  
  Issue **#412** (4 comments) proposes an `agent-governance` skill for safety patterns and audit trails. Issue **#1220** (2 comments) requests multi-file preloading for complex skills. The demand for *composition* (multiple files, multiple agents, persistent memory) is rising sharply.

- **Platform Portability & Standards**  
  Issues **#29** (4 comments, Bedrock support) and **#16** (4 comments, exposing Skills as MCPs) reveal a community that wants skills to be platform-agnostic protocols, not prompts locked to Claude Code's current runtime.

- **Cross-Platform Parity**  
  A dense cluster of Windows-specific bug reports (PRs #1099, #1050, #362, #361; Issues #556, #1169) shows a significant Windows user base experiencing subprocess, pipe, encoding, and command resolution failures that effectively block skill development outside macOS/Linux.

---

### 3. High-Potential Pending Skills
Active-comment PRs not yet merged; these are likely to land soon based on discussion momentum and repository value.

| PR# | Skill | Author | Status |
|-----|-------|--------|--------|
| #1140 | **agent-creator** | SyedaQurratAI | Open |
| #83 | **skill-quality-analyzer** / **skill-security-analyzer** | eovidiu | Open |
| #723 | **testing-patterns** | 4444J99 | Open |
| #806 | **sensory** (macOS automation) | AdelElo13 | Open |
| #147 | **codebase-inventory-audit** | p19dixon | Open |
| #514 | **document-typography** | PGTBoos | Open |
| #154 | **shodh-memory** | varun29ankuS | Open |
| #181 | **SAP-RPT-1-OSS predictor** | amitlals | Open |
| #486 | **ODT** | GitHubNewbie0 | Open |
| #210 | **frontend-design** (improvements) | justinwetch | Open |

---

### 4. Skills Ecosystem Insight
The community's most concentrated demand is shifting beyond isolated feature skills toward a **formalized governance and reliability layer**—encompassing meta-skills for quality/security auditing, reliable evaluation tooling, and enterprise distribution standards—as the ecosystem matures from a prompt gallery into a governed agentic engineering platform.

---

Here is the **Claude Code Community Digest** based on activity up to **2026-06-11**.

---

## Claude Code Community Digest — 2026-06-11

### 1. Today’s Highlights
The release of **v2.1.172** enables deep sub-agent nesting (up to 5 levels) and fixes AWS region resolution for Bedrock, marking a significant step toward complex hierarchical agent orchestration. On the stability front, the community is sounding the alarm on a critical memory leak (#11315), agent control regressions (sub-agents ignoring stop commands in #67321), and a broken OAuth token handshake in the MCP connector (#46140) that blocks authenticated server workflows. The plugin ecosystem also sees a wave of documentation and infrastructure PRs as developers push for production-ready extensibility.

### 2. Releases
**[v2.1.172](https://github.com/anthropics/claude-code/releases/tag/v2.1.172)**
- **Deep Sub-Agent Orchestration:** Agents can now spawn recursive sub-agents up to 5 levels deep—useful for complex task decomposition.
- **Amazon Bedrock Region Detection:** The client now correctly reads the AWS region from `~/.aws/config` when `AWS_REGION` is not set, aligning with AWS SDK precedence. The `/status` command now explicitly reports the region source.
- **Mark Browsing UX:** A new search bar is now available when browsing marks, improving navigation for session logs.

### 3. Hot Issues (10 Noteworthy)
1. **[#18435 — Multi-Account Management for Desktop](https://github.com/anthropics/claude-code/issues/18435)** (109 comments, 580 👍)  
   The most upvoted request overall. Users want easy identity switching in the Desktop app for work/personal accounts.
2. **[#11315 — Critical Memory Leak (129GB RAM)](https://github.com/anthropics/claude-code/issues/11315)** (64 comments)  
   A severe stability bug where Claude Code consumed 129GB of VM, freezing the host. Top priority for the core engine.
3. **[#46140 — MCP OAuth Token Never Sent to Server](https://github.com/anthropics/claude-code/issues/46140)** (17 comments)  
   The MCP connector completes the full OAuth 2.1 + PKCE flow but never sends the Bearer token, rendering all OAuth-secured MCP servers inoperable.
4. **[#26996 — Edit Tool Silently Converts Tabs to Spaces](https://github.com/anthropics/claude-code/issues/26996)** (15 comments, 27 👍)  
   A persistent annoyance causing match failures on tab-indented code (Go, Makefiles). Silent data corruption undermines trust in automated edits.
5. **[#46767 — Tool Results Silently Dropped on Windows](https://github.com/anthropics/claude-code/issues/46767)** (10 comments)  
   Regression in v2.1.101. All tools report "missing due to internal error," making the Windows client unreliable for complex tasks.
6. **[#64260 — Opus 4.8 Fabricated User Intent](https://github.com/anthropics/claude-code/issues/64260)** (9 comments)  
   The model invented a present-tense user request and persisted on an hallucinated task context—a concerning model-behavior anomaly.
7. **[#63909 — Bash Tool ENOSPC on Any Stdout](https://github.com/anthropics/claude-code/issues/63909)** (8 comments, 16 👍)  
   The Bash tool falsely reports "no space left on device" when capturing any subprocess output, silently losing command results.
8. **[#31373 — Shell Substitution `$(…)` Causes Permission Spam](https://github.com/anthropics/claude-code/issues/31373)** (6 comments, 31 👍)  
   The system prompt encourages shell command substitution, triggering endless approval dialogs. A major UX friction point.
9. **[#67321 — Background Subagents Ignore Stop Commands](https://github.com/anthropics/claude-code/issues/67321)** (New)  
   Subagents launched with `run_in_background: true` continue executing after the user orders a stop, consuming tokens and retriggering task notifications.
10. **[#67315 — macOS Keychain Prompts Loop Forever](https://github.com/anthropics/claude-code/issues/67315)** (New)  
    The binary reads credentials via `/usr/bin/security`, but the keychain partition list lacks `apple-tool:`, so the "Always Allow" permission never persists.

### 4. Key PR Progress (10 Important PRs)
1. **[#65875 — Forward `ANTHROPIC_BASE_URL` to Child Processes](https://github.com/anthropics/claude-code/pull/65875)**  
   Critical fix for enterprise proxy setups. The `agentic_review` feature now forwards the base URL env var to spawned child processes, preventing silent auth failures behind gateways.
2. **[#65916 — Docs: `allowed-tools` is NOT a Capability Boundary](https://github.com/anthropics/claude-code/pull/65916)**  
   Clarifies that `allowed-tools` is only an auto-approval mechanism; `tools:` in subagent frontmatter is the hard restriction. Essential for security posture.
3. **[#65919 — Docs: `CLAUDE_PLUGIN_ROOT` Limitation in Subagents](https://github.com/anthropics/claude-code/pull/65919)**  
   Documents a bug (≤ v2.1.166) where `CLAUDE_PLUGIN_ROOT` is passed as a literal string instead of a resolved path, breaking subagents that read plugin-bundled files.
4. **[#65286 — Add Missing `plugin.json` for Plugin-Dev](https://github.com/anthropics/claude-code/pull/65286)**  
   Fixes discoverability so that the `plugin-dev` plugin can be installed through standard plugin mechanisms.
5. **[#65314 — Add Light-Theme Color Detection Script](https://github.com/anthropics/claude-code/pull/65314)**  
   Proposes an automated triage helper to cluster reports of invisible text (color7/color0 collision) on light terminal themes.
6. **[#63686 — Bump Stale/Autoclose Timeouts to 90 Days](https://github.com/anthropics/claude-code/pull/63686)**  
   Community-driven process improvement to prevent complex bugs from being automatically closed too quickly.
7. **[#64607 — Fix `.mcp.json` Documentation](https://github.com/anthropics/claude-code/pull/64607)**  
   Corrects incorrect `mcpServers` wrapper in `.mcp.json` examples. The flat format was misdocumented, leading to configuration errors.
8. **[#67084 — Fix Hookify Prompt Fields](https://github.com/anthropics/claude-code/pull/67084)**  
   Maps legacy `event: prompt` rules to the current `UserPromptSubmit` payload while keeping backward compatibility.
9. **[#66372 — Fix Devcontainer Docker Daemon Detection](https://github.com/anthropics/claude-code/pull/66372)**  
   Fixes a silently failing Docker prerequisite check on Windows by properly tracking `$LASTEXITCODE`.
10. **[#66573 — Fix `ralph-wiggum` Error Handlers](https://github.com/anthropics/claude-code/pull/66573)**  
    Restores dead error handlers in a hook-breaking script where `set -euo pipefail` was causing premature exits.

### 5. Feature Request Trends
- **Multi-Account & Profile Switching**: The dominance of [#18435](https://github.com/anthropics/claude-code/issues/18435) signals a pressing need for identity segmentation across personal and enterprise accounts. “Cowork” reliability issues reinforce this demand for multi-session UX.
- **Deterministic Agent Control**: The community is demanding circuit breakers for runaway agents. [Sub-agents ignoring stop commands](#67321) and [infinite retry loops](#67311) show that users need hard killswitches and budget limits to prevent token waste.
- **Model Behavior Compliance**: A cluster of issues ([#54117](https://github.com/anthropics/claude-code/issues/54117), [#49259](https://github.com/anthropics/claude-code/issues/49259), [#64260](https://github.com/anthropics/claude-code/issues/64260)) highlights frustration with models ignoring `CLAUDE.md` workflows and safety constraints. Users want strict adherence to structured instructions.
- **Platform Parity**: Windows and ARM64 users feel underserved. Issues like [#46767](https://github.com/anthropics/claude-code/issues/46767) (tool drops), [#50674](https://github.com/anthropics/claude-code/issues/50674) (Cowork on ARM64), and [#67318](https://github.com/anthropics/claude-code/issues/67318) (SSH exits) point to a need for first-class cross-platform support.
- **Plugin Ecosystem Maturity**: The high volume of documentation PRs (manifests, rules resolution, `.mcp.json` formats) suggests the community is building but hitting friction from docs gaps and API inconsistencies.

### 6. Developer Pain Points
- **Silent Data Corruption & Loss**: Bugs like [#26996](https://github.com/anthropics/claude-code/issues/26996) (tabs-to-spaces), [#46767](https://github.com/anthropics/claude-code/issues/46767) (tool drops), and [#63909](https://github.com/anthropics/claude-code/issues/63909) (ENOSPC) erode trust. Developers are sensitive to tools that silently alter or discard their work.
- **Token Waste & Cost Anxiety**: Infinite retry loops ([#67311](https://github.com/anthropics/claude-code/issues/67311)) and a broken `/usage` command ([#49633](https://github.com/anthropics/claude-code/issues/49633)) mean developers lack visibility into consumption, leading to surprise bills and wasted session limits.
- **Authentication Workflow Friction**: The broken OAuth flow in MCP ([#46140](https://github.com/anthropics/claude-code/issues/46140)) and endless macOS keychain prompts ([#67315](https://github.com/anthropics/claude-code/issues/67315)) make authentication a daily struggle. For a paid tool, auth must be seamless.
- **Model Hallucination of Intent**: When Opus 4.8 fabricates a user request ([#64260](https://github.com/anthropics/claude-code/issues/64260)) or skips guardrails ([#46429](https://github.com/anthropics/claude-code/issues/46429)), the tool becomes actively counterproductive for sensitive or regulated work.
- **Plugin Developer Experience**: The rapid succession of docs-and-manifest PRs (#65286, #64607, #65916, #65919) reveals that the ecosystem is hindered by ambiguous documentation and subtle configuration API inconsistencies, slowing adoption for third-party developers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-11

## 1. Today’s Highlights
The community is voicing intense frustration over rapid token consumption in Issue #14593, which has ballooned to over 600 comments, while a wave of Windows crash reports—tied to the latest desktop builds—has caught the team’s attention. On the engineering side, the organization is clearly pivoting toward smarter context management: two Rust CLI alphas shipped in the last 24 hours, and a stack of PRs introducing token budgets, compaction hashes, and direct model-requested context window tools signals a deep investment in reigning in the resource costs of long-running agent sessions.

---

## 2. Releases
Two incremental Rust CLI alpha versions dropped yesterday:
- **[rust-v0.140.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.4)**
- **[rust-v0.140.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.7)**

The rapid iteration—skipping from `.4` to `.7`—implies fast-follow fixes for the CLI toolchain, likely addressing regressions found in the broader platform stability work landing this week.

---

## 3. Hot Issues

**1. [#14593] Burning tokens very fast** (604 comments, 265 👍)
The megathread of the month. Users across Business and Pro plans agree that Codex consumes paid tokens far too aggressively on iterative edits. The debate is forcing a reckoning with how context is managed in long threads.
*Link:* https://github.com/openai/codex/issues/14593

**2. [#27175] Codex Desktop Windows crashes after update to 26.602.71036** (8 comments, 3 👍)
A specific build regression causing immediate crashes or blank windows on Windows 11. Compounds prior reports about store-app instability, making this a recurring platform trust issue.
*Link:* https://github.com/openai/codex/issues/27175

**3. [#27491] Severe streaming slowdown (Fast mode stalls)** (6 comments)
Fast mode sending only a few characters per second on macOS Tahoe. This completely breaks the interactive coding loop and is the most critical UX regression reported this cycle.
*Link:* https://github.com/openai/codex/issues/27491

**4. [#23198] Codex Desktop on Windows extremely slow** (12 comments, 31 👍)
General sluggishness isolated to the app even under low host load. High upvote ratio confirms this is a pervasive Windows productivity killer.
*Link:* https://github.com/openai/codex/issues/23198

**5. [#25463] Project threads disappear from sidebar while JSONL remains** (12 comments)
A recurring data-integrity nightmare: conversations vanish from the UI but stay readable on disk. Shakes confidence in the local persistence layer.
*Link:* https://github.com/openai/codex/issues/25463

**6. [#26753] MultiAgentV2 encrypted tool schema returns 400** (9 comments, closed)
Enabling `features.multi_agent_v2` universally breaks all tool invocations due to rejected schema encryption, blocking the alpha multi-agent feature entirely.
*Link:* https://github.com/openai/codex/issues/26753

**7. [#13553] Windows Store app fails for non-ASCII usernames** (11 comments, 9 👍)
A hard crash on launch for users with international characters in their Windows account name. A specific localization/compatibility gap that has lasted months.
*Link:* https://github.com/openai/codex/issues/13553

**8. [#26869] App-server leaks child processes after crash/restart** (8 comments)
The desktop background daemon fails to clean up tool subprocesses on crash, leading to stale processes and runaway log files. Highlights weak state management in the local daemon.
*Link:* https://github.com/openai/codex/issues/26869

**9. [#17642] Spark model not supported with ChatGPT account** (12 comments)
`gpt-5.3-codex-spark` returns a 400 for Pro accounts using the CLI. Confusing model-access boundaries continue to frustrate power users.
*Link:* https://github.com/openai/codex/issues/17642

**10. [#22004] `RangeError: Invalid string length` on large session JSONL** (5 comments, 2 👍)
Windows users hit a V8 string-length ceiling when loading sessions with very long rollout files, making large projects inaccessible or causing data loss.
*Link:* https://github.com/openai/codex/issues/22004

---

## 4. Key PR Progress

**1. [#27438] Add token budget context feature** (CLOSED)
Merged infrastructure that injects context-window budget metadata into model-visible history, giving the model awareness of remaining space.
*Link:* https://github.com/openai/codex/pull/27438

**2. [#27520] Compact when comp_hash changes** (OPEN)
Snaps the model config hash into `TurnContext` and triggers smart compaction on config drift, preventing stale context from polluting new turns.
*Link:* https://github.com/openai/codex/pull/27520

**3. [#27488] Add new context window tool** (OPEN)
Grants the model a tool to explicitly request a fresh context window, bypassing the token cost of writing a compaction summary.
*Link:* https://github.com/openai/codex/pull/27488

**4. [#27518] Add context remaining tool** (OPEN)
Companion tool allowing the model to query remaining tokens on demand, complementing the passive budget injection from #27438.
*Link:* https://github.com/openai/codex/pull/27518

**5. [#27508/9/10] TUI Goal stack: long text, pasted text, and images** (OPEN)
A three-part series lifting the 4K-character goal limit, supporting pasted blobs, and enabling image attachments in TUI goals. Major polish for terminal users.
*Links:* https://github.com/openai/codex/pull/27508 | https://github.com/openai/codex/pull/27509 | https://github.com/openai/codex/pull/27510

**6. [#27246] Strip image detail from Responses Lite** (OPEN)
Optimizes network payloads by stripping image `detail` fields from the Responses Lite path while preserving byte-exact image URLs.
*Link:* https://github.com/openai/codex/pull/27246

**7. [#27266] Preserve metadata when resizing prompt images** (OPEN)
Ensures ICC profiles and EXIF orientation survive image resizing, fixing color and rotation issues in vision workflows.
*Link:* https://github.com/openai/codex/pull/27266

**8. [#27495] Pass agent path metadata to MCP tools** (OPEN)
Sends `/root` or `/root/worker` paths in MCP request metadata—critical for scoping tool behavior in multi-agent architectures.
*Link:* https://github.com/openai/codex/pull/27495

**9. [#26706] Add system proxy feature config surface** (OPEN)
Lays the foundation for first-class PAC/proxy support, addressing a major enterprise blocker currently requiring fragile workarounds.
*Link:* https://github.com/openai/codex/pull/26706

**10. [#27115] Break down between-sampling overhead** (OPEN)
Adds granular instrumentation (post-response, retry, compaction, request prep) to session timing, giving developers—and the system—visibility into what stalls a turn.
*Link:* https://github.com/openai/codex/pull/27115

---

## 5. Feature Request Trends

- **Intelligent Context Management:** The dominant theme across both Issues and PRs. Users don’t just want *more* tokens; they want the system to compact efficiently, surface budget transparently, and let the model actively manage its own window. The `comp_hash` + token budget + context-tool stack is a direct response to this.
- **Fault-Tolerant Multi-Agent Orchestration:** Repeated subagent “agent loop died” errors, combined with PR work on MCP agent path metadata and tool reliability, show a clear desire for robust multi-agent execution that doesn’t collapse on transient failures.
- **Windows Platform Parity:** The density of crash-on-launch, slowness, and rendering bugs on Windows is the single loudest platform-specific signal. The community expects desktop feature parity with macOS.
- **Enterprise Networking:** The PAC/proxy config PR (#26706) directly reflects unmet demand for Codex to operate inside corporate network boundaries without fragile hacks.
- **Stable MCP Plugin Ecosystem:** OAuth failures (#24103) and missing plugin-list visibility (#27493) indicate users are eager to adopt MCP but hitting high friction on setup and discovery.

---

## 6. Developer Pain Points

- **Cost Anxiety & Efficiency:** Issue #14593 is a sentiment supernova. Developers feel financially penalized by inefficient loop patterns and demand transparency and control over token burn rates.
- **Windows Instability:** Multiple crash-on-launch builds, invisible UI elements, and random degradation windows make the Windows client feel like a second-class platform. Trust is eroding with each bad build.
- **Loss of Work & Trust in Local State:** The recurring “chat disappeared but JSONL exists” bug (#25463, #20833, #22796) creates a nagging “did it save?” anxiety that undermines reliance on persistent history.
- **Integration Friction:** Broken OAuth flows for MCP servers, “model not configured” errors for Spark, and workspace deactivation confusion create high barriers to exploring advanced features.
- **Lack of Observability:** Users cannot easily diagnose *why* a turn is slow, why tokens are burning, or why a session crashed. The between-sampling overhead work (#27115) suggests the team is aware, but current black-box behavior frustrates power users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest | June 11, 2026

## 1. Today's Highlights

Activity centers squarely on squashing critical reliability and security bugs in the agent runtime. A P1 fix for the long-running "shell execution hang" bug ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) has been submitted, and a critical security patch hardening HITL tool confirmations against indirect prompt injection ([#27472](https://github.com/google-gemini/gemini-cli/pull/27472)) has been merged. Meanwhile, the team is actively addressing a cluster of "Auto Memory" system issues, targeting indefinite retries and log leak prevention.

---

## 2. Releases

*No new versions published in the last 24 hours.*

---

## 3. Hot Issues

1.  **[P1]** **Generalist agent hangs** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) (8 👍 , 7 comments)  
    The community's most upvoted active issue. The generalist agent hangs indefinitely on simple tasks (e.g., folder creation). Users resort to disabling sub-agents entirely, severely limiting the CLI's core value proposition.

2.  **[P1]** **Shell command execution hangs after completion** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (3 👍 , 4 comments)  
    A high-frequency bug that leaves the CLI stuck in "Waiting input" state on simple shell commands. A targeted fix landed today in [#27842](https://github.com/google-gemini/gemini-cli/pull/27842).

3.  **[P1]** **Subagent false success on MAX_TURNS** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) (2 👍 , 6 comments)  
    Sub-agents hitting the turn limit report `status: "success"` and `Termination Reason: "GOAL"`, effectively lying about their output. This creates significant debugging friction for users relying on multi-step agent chains.

4.  **[P1]** **Robust component level evaluations** — [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) (7 comments)  
    An EPIC tracking deeper, component-granular evaluation layers for agents, extending the 76 behavioral evals already in the repository. Signals a major infrastructure push for quality gates.

5.  **[P2]** **Assess AST-aware file reads, search, and mapping** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) (1 👍 , 7 comments)  
    Investigates whether replacing raw text operations with AST-aware CLIs can reduce token noise, improve precision in method-boundary reads, and reduce total conversation turns. High technical interest.

6.  **[P2]** **Gemini ignores installed skills and sub-agents** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) (6 comments)  
    A persistent user complaint: custom skills (e.g., `gradle`, `git`) are not used autonomously by the agent despite explicit descriptions, requiring constant manual prompting.

7.  **[P2]** **Add deterministic redaction and reduce Auto Memory logging** — [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) (5 comments)  
    The memory extraction agent sends transcript content to the model *before* redaction occurs, and existing skill transcripts may be logged. A proactive privacy/security audit of the Auto Memory pipeline.

8.  **[P2]** **Stop Auto Memory from retrying low-signal sessions** — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) (5 comments)  
    Sessions deemed "low-signal" by the extraction agent remain unprocessed and get surfaced repeatedly, causing indefinite retries and wasted model calls.

9.  **[P2]** **Agent should discourage destructive behavior** — [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) (1 👍 , 2 comments)  
    Users want built-in guardrails against dangerous operations like `git reset --force` or destructive database maintenance without explicit safety overrides.

10. **[P1]** **Browser subagent fails on Wayland** — [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) (1 👍 , 4 comments)  
    A platform compatibility gap blocking Linux users on Wayland from using the browser agent. Reports `Termination Reason: GOAL` despite actual failure.

---

## 4. Key PR Progress

1.  **`#27842`** **[NEW]** `fix(core): never let shell exit results hang on the output drain` — [Link](https://github.com/google-gemini/gemini-cli/pull/27842)  
    Directly addresses the root cause of [#25166](https://github.com/google-gemini/gemini-cli/issues/25166). Adds error handling and a bound to the PTY output processing gate that was blocking exit signals.

2.  **`#27472`** **[MERGED]** `fix(ui): enforce truncation lockout for tool confirmations to prevent IPI` — [Link](https://github.com/google-gemini/gemini-cli/pull/27472)  
    Critical security patch closing a Human-in-the-Loop bypass vulnerability ([#23433](https://github.com/google-gemini/gemini-cli/issues/23433)). Users must now expand truncated commands/diffs before approval, preventing Indirect Prompt Injection.

3.  **`#27502`** **[MERGED]** `fix(core): resolve P1 crash during terminal resize (ioctl EBADF)` — [Link](https://github.com/google-gemini/gemini-cli/pull/27502)  
    Fixes a race condition between PTY teardown and React's resize `useEffect`, which was causing a critical `ioctl EBADF` crash.

4.  **`#27767`** **[NEW]** `fix(cli): prevent path traversal vulnerabilities during skill install` — [Link](https://github.com/google-gemini/gemini-cli/pull/27767)  
    Hardens `installSkill`, `linkSkill`, and `uninstallSkill` against three path traversal vectors originating from frontmatter in malicious skill packages.

5.  **`#27473`** **[MERGED]** `fix(security): resolve hostnames before private-IP check in isBlockedHost` — [Link](https://github.com/google-gemini/gemini-cli/pull/27473)  
    Prevents an SSRF bypass where hostnames resolving to private or link-local IPs were allowed through the `web-fetch` pipeline, as synchronous checks only validated IP literals.

6.  **`#27698`** **[NEW]** `fix(core): Ensure zero-quota limits fail fast to prevent retry loop hang` — [Link](https://github.com/google-gemini/gemini-cli/pull/27698)  
    Fixes a critical retry loop bug where hard quota limits of 0 (unbilled free tier accounts) triggered a futile 10-attempt retry cycle instead of failing fast.

7.  **`#27474`** **[MERGED]** `fix(core): guard isFunctionCall/isFunctionResponse against empty parts` — [Link](https://github.com/google-gemini/gemini-cli/pull/27474)  
    Corrects a logic defect where `Array.prototype.every([])` returns `true` (vacuous truth), causing empty message parts to be incorrectly classified as function calls/responses.

8.  **`#27839`** **[NEW]** `fix(core): make read_background_output delay abort-aware` — [Link](https://github.com/google-gemini/gemini-cli/pull/27839)  
    Fixes an issue where pressing ESC to cancel `read_background_output` marked it canceled in the UI but the spinner kept spinning due to a `setTimeout` that ignored the abort signal.

9.  **`#27648`** **[NEW]** `feat(core): support list format in trustedFolders.json` — [Link](https://github.com/google-gemini/gemini-cli/pull/27648)  
    Developer QoL improvement adding a simple JSON array format for `trustedFolders.json`, alongside the existing object format.

10. **`#27753`** **[NEW]** `ci: validate workflow_run origin before consuming the E2E artifact` — [Link](https://github.com/google-gemini/gemini-cli/pull/27753)  
    CI security hardening preventing `workflow_run` artifact poisoning attacks where a fork PR could execute attacker-controlled code with repository secrets.

---

## 5. Feature Request Trends

**Deep Code Intelligence**
The community is strongly pushing beyond raw text operations. There is sustained interest in AST-aware CLI tools for codebase mapping ([#22746](https://github.com/google-gemini/gemini-cli/issues/22746)), search ([#22747](https://github.com/google-gemini/gemini-cli/issues/22747)), and reading ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745)) to improve precision and reduce token waste.

**Agent Self-Mastery & Intrinsic Control**
A recurring theme is that the agent should deeply understand its own ecosystem. This includes knowing its own CLI flags and hotkeys ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)), respecting configuration overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and proactively leveraging installed skills without explicit user prompting ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)).

**Robust Guardrails and Safety**
Users demand layered safety: preventing destructive operations ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)), deterministic secret redaction *before* model context injection ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and HITL protections against prompt injection ([#27472](https://github.com/google-gemini/gemini-cli/pull/27472)).

**Scalability Infrastructure**
Requests for handling large tool sets (>128 tools, [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) and robust remote agent backends with advanced auth ([#20303](https://github.com/google-gemini/gemini-cli/issues/20303)) point to growing enterprise and complex workflow adoption.

---

## 6. Developer Pain Points

**Agent Deception and Deadlock (Highest Friction)**
The single biggest trust-eroding pattern is agents getting stuck—hanging indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409), [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) or misrepresenting failure as success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). This forces users to become full-time supervisors rather than delegates.

**Security Properties Applied Reactively**
Several issues highlight security being patched *after* the fact: secrets sent to models before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), hostname SSRF checks missing before network requests ([#27473](https://github.com/google-gemini/gemini-cli/pull/27473)), and path traversal vectors in skill management ([#27767](https://github.com/google-gemini/gemini-cli/pull/27767)).

**Configuration and Versioning Whiplash**
Users report that their configurations are silently ignored—`settings.json` overrides are skipped by the browser agent ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), symlinks are rejected as agent definitions ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)), and version updates can revert or silently enable features ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093), [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)).

**Sub-Agent Opaqueness**
Sub-agents operate as black boxes with unreliable termination signals. They can create messy temporary artifacts ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), eat turns without progress ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), or ignore lifecycle configuration ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), making multi-agent workflows fragile to audit and maintain.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI Community Digest — 2026-06-11

### 1. Today's Highlights
The Copilot CLI community is navigating a wave of terminal rendering regressions following the rapid 1.0.x release cycle, with bugs related to garbled streaming output (#3749 / #3755) and clipboard failures on both Linux and Windows (#2082, #3622) dominating recent discussions. Enterprise users continue to face friction with MCP policy false positives (#1707 / #3756) and insufficient token scoping for org-managed deployments (#223). Meanwhile, the longest-standing open issue (#53) remains a potent symbol of community frustration, having spurred the development of third-party alternatives in the absence of official communication.

---

### 2. Releases
No new releases or release candidates have been published in the last 24 hours. The current stable version remains **v1.0.60**, which has been the subject of several new regression reports (#3727, #3749).

---

### 3. Hot Issues

1. **[#53] Bring back classic CLI commands** (Open · 75👍 · 34 comments)
   The most-reacted issue in the repository. The community has rallied behind third-party projects like `shell-ai` due to the perceived abandonment of the original "revolution" workflow. The lack of any GitHub response for months is a growing public-relations concern.
   [View Issue](https://github.com/github/copilot-cli/issues/53)

2. **[#223] "Copilot Requests" permission for org-owned tokens** (Open · 76👍 · 29 comments)
   An enterprise blocker. Organizations need to use fine-grained tokens for automations, but the “Copilot Requests” permission is invisible for org-owned tokens, forcing reliance on insecure personal PATs.
   [View Issue](https://github.com/github/copilot-cli/issues/223)

3. **[#1703] CLI model list smaller than VS Code (e.g., Gemini 3.1 Pro)** (Closed · 54👍 · 31 comments)
   Though closed, the underlying parity gap persists. Users consistently report missing Gemini models in the CLI that are available in VS Code, a theme echoed in newer issues like #2854 and #2577.
   [View Issue](https://github.com/github/copilot-cli/issues/1703)

4. **[#2334] Please bring back no-alt-screen** (Closed · 28👍 · 7 comments)
   Users strongly prefer staying in the terminal’s main scrollback buffer rather than the TUI alt-screen. This closed issue continues to capture community sentiment around the loss of native terminal search and scroll history.
   [View Issue](https://github.com/github/copilot-cli/issues/2334)

5. **[#2082] ctrl+shift+c no longer copies to clipboard on Linux** (Open · 8👍 · 21 comments)
   A major platform regression. The standard OS terminal shortcut is being intercepted by the TUI, breaking established muscle memory for Linux users.
   [View Issue](https://github.com/github/copilot-cli/issues/2082)

6. **[#3749 / #3755] Terminal streaming renderer/reasoning display corrupts output** (Open)
   Critical recent bugs. Streamed text shows doubled characters and overlapping fragments, especially during the LLM’s live thinking phase. This severely impacts readability and trust in output.
   [View #3749](https://github.com/github/copilot-cli/issues/3749) · [View #3755](https://github.com/github/copilot-cli/issues/3755)

7. **[#1707 / #3756] 3rd-party MCP servers falsely blocked by policy** (Closed / Closed)
   A recurring bug where organizational policy incorrectly blocks third-party MCP servers. Fixes shipped in v0.0.418 and v1.0.59 have not fully resolved the root cause.
   [View #1707](https://github.com/github/copilot-cli/issues/1707) · [View #3756](https://github.com/github/copilot-cli/issues/3756)

8. **[#3596] Error loading model list: Not authenticated** (Open · 10👍 · 5 comments)
   Session-management reliability issue. Resuming a long-running session loses the authentication state needed for the `/model` command, forcing users to start a fresh session.
   [View Issue](https://github.com/github/copilot-cli/issues/3596)

9. **[#3727] Regression in v1.0.60: Plugin hook contract broken** (Open · 3 comments)
   A hard regression for the plugin ecosystem. The `userPromptSubmitted` hook no longer injects `additionalContext` into the planner, breaking custom context injectors and tools that worked in v1.0.59.
   [View Issue](https://github.com/github/copilot-cli/issues/3727)

10. **[#3547] Background sub-agent silently hangs at total_turns=0** (Closed)
    Agent stability issue. Background agents dispatched for long-running tasks would report `status: running` but never execute a turn, breaking multi-step automation workflows.
    [View Issue](https://github.com/github/copilot-cli/issues/3547)

---

### 4. Key PR Progress
No pull requests were updated in the last 24 hours. While the PR queue is currently quiet, several critical issues were resolved in recent merges that are now live in stable releases. Fixes for model list parity (#1703), MCP policy false positives (#1707), background sub-agent hangs (#3547), and the restoration of Gemini Pro support (#2434) have all been deployed. The team appears to be in a stabilization phase following the rapid 1.0.x releases.

---

### 5. Feature Request Trends

- **Model Access & Custom Providers (ACP):** Users consistently demand CLI parity with the VS Code model catalog. A top unmet need is support for `COPILOT_PROVIDER_*` environment variables in `--acp` mode (#3048) to allow custom providers like OpenRouter or self-hosted models.
- **MCP Power-User Features:** The community is asking for deeper MCP integration, such as a direct tool-invocation syntax (`#mcp-server:tool arg1`) with tab-completion (#3752).
- **Safe Automation Defaults:** Issue #2243 captures strong sentiment that git worktree creation should be opt-in rather than automatic, following severe user experiences with ruined worktrees during CLI sessions.
- **Session Management UX:** Users want robust session-name handling (spaces in names, #3754) and persistent auth tokens across long-running sessions (#3596).

---

### 6. Developer Pain Points

- **Terminal Rendering Instability:** The combination of broken clipboard shortcuts, garbled streaming text, and the forced alt-screen UX creates a poor baseline experience for a tool whose core value proposition is the terminal.
- **Regression Velocity:** The v1.0.60 release introduced hard regressions in both UI (streaming) and API (hooks). Users are expressing concern that the pace of shipping is outpacing quality assurance.
- **VS Code Feature Gap:** Seeing Gemini 3.1 Pro available in VS Code but missing from the CLI feels like a tiered product experience, penalizing developers who prefer terminal-based workflows.
- **Enterprise Governance Friction:** The intersection of MCP policy bugs and incomplete token permission support presents a combined "enterprise penalty" where organizations get a less capable tool with more deployment blockers.
- **Community Communication:** The silence on Issue #53 is widely cited as a trust deficit. The lack of a clear roadmap or official response has pushed developers to build and adopt open-source forks like `shell-ai`, eroding the official tool's mindshare.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-11

## 1. Today's Highlights
The past 24 hours saw no new GitHub release, but a significant wave of reliability patches were finalized across the project. Core maintainer @he-yufeng merged extensive Windows compatibility fixes and MCP resilience improvements, while contributor @Pluviotybe landed three important session-history patches. Two critical regressions in the v0.12.0 YOLO/autonomous mode were identified by the community, putting workflow reliability in the immediate spotlight.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues
1. **[#2448] Yolo Mode Prompts for Approval** — A critical regression where `--yolo` mode still prompts for user consent. Severely impacts hands-off CI/CD and batch workflows. Zero community replies yet, but a high-urgency item for autonomy-focused users.  
   [Issue #2448](https://github.com/MoonshotAI/kimi-cli/issues/2448)

2. **[#2447] Final Todo Item Never Completes** — The agent's task loop deadlocks on the last item, preventing deterministic single-turn completions. A core workflow blocker for automated code generation tasks.  
   [Issue #2447](https://github.com/MoonshotAI/kimi-cli/issues/2447)

3. **[#2336] Orphan Tool Calls Kill Session Replay** — Sessions interrupted mid-turn (OOM, kill -9, terminal close) yield a permanently corrupted `context.jsonl`, requiring users to start over from scratch. Addressed by PR #2383.  
   [Issue #2336](https://github.com/MoonshotAI/kimi-cli/issues/2336)

4. **[#2312] Web UI: Archived Sessions Fail to Load** — Selecting archived sessions from the sidebar results in a blank state. Disrupts long-running session workflows in the Web interface. Fixed by PR #2333.  
   [Issue #2312](https://github.com/MoonshotAI/kimi-cli/issues/2312)

5. **[#2310] Shell Process Trees Survive Timeout** — Timed-out shell commands leave orphaned child processes running, causing resource leaks. Fixed by PR #2327.  
   [Issue #2310](https://github.com/MoonshotAI/kimi-cli/issues/2310)

6. **[#2279] Web Uploads Duplicated After Restart** — Session process restarts cause `sent` markers to be lost, re-uploading files and duplicating context. Fixed by PR #2288.  
   [Issue #2279](https://github.com/MoonshotAI/kimi-cli/issues/2279)

7. **[#2222] `--continue` Fails on Stale Sessions** — The resume flag cannot locate the latest session when metadata is outdated, breaking workflow persistence. Fixed by PR #2239.  
   [Issue #2222](https://github.com/MoonshotAI/kimi-cli/issues/2222)

8. **[#2197] Unwanted Console Windows on Windows** — Subprocesses spawn visible console windows on Windows due to a missing `CREATE_NO_WINDOW` flag. Fixed by PRs #2199 and #2289.  
   [Issue #2197](https://github.com/MoonshotAI/kimi-cli/issues/2197)

9. **[#2202] `kimi term` Fails on Windows** — The terminal backend depends on POSIX-only modules (`fcntl`), completely blocking the feature for Windows users. Fixed by PR #2210.  
   [Issue #2202](https://github.com/MoonshotAI/kimi-cli/issues/2202)

10. **[#2142] Shell Command Display Truncation** — Long shell commands are aggressively shortened to 50 characters in the CLI UI, hiding command intent and parameters. Improved by PR #2387.  
    [Issue #2142](https://github.com/MoonshotAI/kimi-cli/issues/2142)

## 4. Key PR Progress
1. **[PR #2387] fix(tools): preserve shell command headline details** (Pluviobyte) — Replaces the generic `shorten_middle` truncation with a contextual display of the command name and core arguments, vastly improving terminal readability.  
   [PR #2387](https://github.com/MoonshotAI/kimi-cli/pull/2387)

2. **[PR #2383] fix(soul): repair orphan tool_calls when replaying history** (Pluviobyte) — Handles incomplete `assistant` messages by detecting and stripping orphaned tool calls, preventing unrecoverable session corruption.  
   [PR #2383](https://github.com/MoonshotAI/kimi-cli/pull/2383)

3. **[PR #2386] fix(session): map undo wire turns to context turns** (Pluviobyte) — Fixes `/undo` and fork by correctly mapping wire indices to context turns, resolving issues with slash-command turns disrupting version history.  
   [PR #2386](https://github.com/MoonshotAI/kimi-cli/pull/2386)

4. **[PR #2355] fix: continue after deferred MCP startup failures** (he-yufeng) — Logs MCP server failures gracefully and continues the interactive turn without the unavailable server, instead of aborting the entire session.  
   [PR #2355](https://github.com/MoonshotAI/kimi-cli/pull/2355)

5. **[PR #2354] fix: avoid shared rotating logs on Windows** (he-yufeng) — Introduces per-process log files on Windows (`kimi.<pid>.log`) to prevent race conditions between concurrent CLI, web, and worker processes rotating the same file.  
   [PR #2354](https://github.com/MoonshotAI/kimi-cli/pull/2354)

6. **[PR #2334] fix(kosong): sanitize surrogates before Kimi requests** (he-yufeng) — Strips lone UTF-16 surrogate code units from system prompts, messages, and tool arguments to prevent hard rejections from the Kimi API.  
   [PR #2334](https://github.com/MoonshotAI/kimi-cli/pull/2334)

7. **[PR #2327] fix: terminate shell process trees on timeout** (he-yufeng) — Places foreground shell commands in their own process group, ensuring clean tree-wide termination on timeout or `Ctrl+C`.  
   [PR #2327](https://github.com/MoonshotAI/kimi-cli/pull/2327)

8. **[PR #2239] fix: continue latest persisted session** (he-yufeng) — Makes `--continue` resilient to stale metadata by searching for the newest non-empty session in the working directory.  
   [PR #2239](https://github.com/MoonshotAI/kimi-cli/pull/2239)

9. **[PR #2217] fix: recover background auto-trigger after cooldown** (he-yufeng) — Prevents the background agent from entering a permanent cooldown. After 10 minutes, the failure counter resets, allowing auto-triggering to resume.  
   [PR #2217](https://github.com/MoonshotAI/kimi-cli/pull/2217)

10. **[PR #2196] fix(kosong): sanitize malformed history tool calls** (he-yufeng) — Strips corrupted JSON from historical tool arguments, preventing repetitive API failures on every turn replay in a session.  
    [PR #2196](https://github.com/MoonshotAI/kimi-cli/pull/2196)

## 5. Feature Request Trends
The dominant feature direction emerging from recent activity is **true zero-interrupt autonomy**. The urgency of fixing YOLO mode and task completion loops signals a strong demand for a fully unattended coding agent suitable for CI/CD. This is complemented by a growing need for **first-class Windows support**, given the concentrated volume of platform-specific fixes currently landing. Users also increasingly expect **robust session resilience**—the ability to survive arbitrary process interruptions (OOM, kill, crash) without losing state.

## 6. Developer Pain Points
- **Windows Friction:** Console window popups, font resets, shared log file corruption, and encoding issues with non-English filenames create persistent friction for the Windows developer experience.  
- **Session Fragility:** The session file's vulnerability to mid-kill corruption repeatedly erodes trust for long running agentic tasks, especially under memory pressure.  
- **YOLO Mode Breaking Trust:** Critical features of the autonomous mode failing post-launch (prompting, task completion) makes the tool unreliable for unattended pipelines.  
- **MCP Brittleness:** Hard failures on MCP server startup blocking the entire interactive turn creates a fragile experience for users with complex toolchains.  
- **Background Agent Transparency:** The background auto-trigger entering an opaque cooldown state without clear user feedback leads to confusion about why the tool has stopped responding.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-11

---

## Today’s Highlights

The team pushed a critical desktop crash hotfix (v1.17.3) soon after yesterday’s v1.17.2 shipped config auth recovery and subagent permission fixes. On the development front, a major **TUI 2.0** refactor (#31796) landed, signaling deep investment in the terminal interface. The community remains focused on session lifecycle features, with the `/goal` command proposal (#27167) continuing to attract heavy engagement.

---

## Releases

Three updates landed in the last 24 hours:

**v1.17.3** *(Hotfix)*
- Resolved desktop crash introduced in v1.17.2.

**v1.17.2**
- **Core:** Recover from expired remote config auth by prompting re-login instead of failing to load config.
- **Core:** Subagents can once again use their own configured permissions.
- **Desktop:** Restored Linux launcher and icon identity so pinned apps keep opening correctly.

**v1.17.1**
- **Improvement:** References can include usage descriptions, show in the new docs, and be hidden from `@` autocomplete.
- **Bugfix:** Deprecated `reference` entries are still loaded under the newer `references` config key.
- **Bugfix:** MCP prompt and resource resolution fixes.

---

## Hot Issues

### 1. #2072 — Support for Cursor CLI
- **183 👍 | 71 comments**
- Community heavily requests interop with Cursor's proprietary CLI. While the API is undocumented, demand signals users want OpenCode as a universal agent hub.
- [anomalyco/opencode Issue #2072](https://github.com/anomalyco/opencode/issues/2072)

### 2. #27167 — Add Native Session Goals with `/goal`
- **69 👍 | 40 comments**
- Persistent session objectives are the most requested workflow feature. Users want built-in goal lifecycle akin to Claude Code’s `/goal`, rather than relying solely on custom slash commands.
- [anomalyco/opencode Issue #27167](https://github.com/anomalyco/opencode/issues/27167)

### 3. #30086 — High CPU Usage in Newer Versions
- **1 👍 | 10 comments**
- A severe performance regression beginning ~7 days ago. Users who previously ran 10 concurrent sessions now struggle with 3. Likely a core loop or snapshot compaction issue.
- [anomalyco/opencode Issue #30086](https://github.com/anomalyco/opencode/issues/30086)

### 4. #11831 — YOLO Mode (Auto-Approve All Permissions)
- **29 👍 | 9 comments**
- Power users request a mode that bypasses tool permission prompts while respecting explicit `deny` rules. Reflects a push toward fully unattended, autonomous agent workflows.
- [anomalyco/opencode Issue #11831](https://github.com/anomalyco/opencode/issues/11831)

### 5. #31247 — Opus 4.8 Leaks Tool-Call Text into Messages
- **0 👍 | 8 comments**
- `claude-opus-4.8` via GitHub Copilot leaks raw tool-call markup (`call read`, `<invoke>`) into assistant messages, polluting conversation history and context windows.
- [anomalyco/opencode Issue #31247](https://github.com/anomalyco/opencode/issues/31247)

### 6. #30158 — Web UI Terminal Button Disappears
- **6 👍 | 7 comments**
- Since v1.15.12, the terminal toggle button vanishes from the Web UI top bar. Severely impacts remote development workflows; downgrading restores it.
- [anomalyco/opencode Issue #30158](https://github.com/anomalyco/opencode/issues/30158)

### 7. #6490 — Web UI Cannot Browse Folders Outside User Profile (Windows)
- **12 👍 | 10 comments**
- When using `opencode web`, Windows users can only select projects from default profile folders (Desktop, Documents). No way to navigate to `D:\` drives.
- [anomalyco/opencode Issue #6490](https://github.com/anomalyco/opencode/issues/6490)

### 8. #16438 — Snapshot File Grows to 16GB / General Slowness
- **1 👍 | 6 comments**
- Chronic performance issues driven by a massive `snapshot` file. Users must manually delete it regularly. Points to potential leak or missing compaction in long sessions.
- [anomalyco/opencode Issue #16438](https://github.com/anomalyco/opencode/issues/16438)

### 9. #29422 — Stale Permission Prompts After Interrupted Approval
- **0 👍 | 5 comments**
- Web/Desktop UI retains permission dialogs for already-interrupted tool requests. Approving them yields `Permission request not found`, freezing the session.
- [anomalyco/opencode Issue #29422](https://github.com/anomalyco/opencode/issues/29422)

### 10. #31831 — Constant 185% CPU / 500MB+ RAM While Idle (macOS)
- **0 👍 | 1 comment**
- Fresh report of extreme resource consumption even without an active conversation. May relate to #30086 or a new background process issue introduced in 1.17.x.
- [anomalyco/opencode Issue #31831](https://github.com/anomalyco/opencode/issues/31831)

---

## Key PR Progress

### 1. #31796 — TUI 2.0
- **Open | Author: thdxr**
- A massive architectural refactor of the terminal UI. Aims to modernize session management, rendering, and state handling.
- [anomalyco/opencode PR #31796](https://github.com/anomalyco/opencode/pull/31796)

### 2. #31822 — Add v2 Session API Endpoints
- **Closed | Author: thdxr**
- Adds new REST endpoints for session creation, retrieval, and location resolution. Includes regenerated JS SDK and full HTTP API exerciser coverage.
- [anomalyco/opencode PR #31822](https://github.com/anomalyco/opencode/pull/31822)

### 3. #31819 — Retry on xfyun Engine Busy Response
- **Open | Author: magicxoxcco**
- Treats "engine busy" as a transient error, adding retry logic for the xfyun provider. Closes #31812.
- [anomalyco/opencode PR #31819](https://github.com/anomalyco/opencode/pull/31819)

### 4. #31826 — Refactor TUI: Replace v2 Sync with Data Context
- **Closed | Author: thdxr**
- Part of the TUI 2.0 effort. Replaces the `sync-v2` context with a domain-oriented `DataProvider` pattern for cleaner state management.
- [anomalyco/opencode PR #31826](https://github.com/anomalyco/opencode/pull/31826)

### 5. #31805 — Fix TUI Session Epilogue During Shutdown
- **Open | Author: tobwen**
- Fixes a bug where scoped cleanup cleared the session summary before it could be printed on exit. Closes #31803.
- [anomalyco/opencode PR #31805](https://github.com/anomalyco/opencode/pull/31805)

### 6. #31745 — Surface Content-Filter Finish Reason
- **Open | Author: kkdawkins**
- When a model (e.g., Anthropic) ends a turn with a refusal or content-filter, the error is now surfaced visibly rather than failing silently. Closes #31744.
- [anomalyco/opencode PR #31745](https://github.com/anomalyco/opencode/pull/31745)

### 7. #31329 — Graceful Error Handling for PDF/Image Read Failures
- **Open | Author: zhiyiwang-byte**
- Prevents session crashes when attempting to read corrupted or permission-locked PDF/image files. Closes #21390.
- [anomalyco/opencode PR #31329](https://github.com/anomalyco/opencode/pull/31329)

### 8. #29217 — Inline `$skill` Invocations in TUI Prompt Composer
- **Open | Author: jjdubski**
- Adds `$` autocomplete for skills in the prompt composer with inline execution and `pasteText` support. Closes multiple related skill-discovery issues.
- [anomalyco/opencode PR #29217](https://github.com/anomalyco/opencode/pull/29217)

### 9. #31809 — Correct Misleading Read Prerequisite in Tool Descriptions
- **Open | Author: szzhoujiarui-sketch**
- Fixes tool descriptions that falsely claimed Write/Edit would fail if Read wasn't called first. Reduces agent confusion. Closes #31768.
- [anomalyco/opencode PR #31809](https://github.com/anomalyco/opencode/pull/31809)

### 10. #31802 — Preserve MCP Headers During Auth and Debug
- **Open | Author: rekram1-node**
- Ensures user-configured headers pass through OAuth transport and `mcp debug` connection probes. Closes a gap for custom MCP servers requiring specific auth headers.
- [anomalyco/opencode PR #31802](https://github.com/anomalyco/opencode/pull/31802)

---

## Feature Request Trends

**1. Agent Autonomy and Workflow Persistence**
The `/goal` command (#27167, #31762) and YOLO Mode (#11831) dominate discussion. Users want agents that can own multi-step objectives without requiring manual approval or re-prompting at every turn.

**2. Universal Provider Compatibility**
OpenCode is increasingly seen as a universal frontend. Requests for Cursor CLI (#2072), Gab.ai (#8762), and better handling of xfyun / Cerebras specifics reflect a demand for broad, resilient provider support.

**3. TUI/Web Parity and Polish**
Missing UI elements (#30158), stagnant session search (#31182), and inability to resize the status panel (#24373) highlight frustration with inconsistent interfaces across platforms.

**4. Plugin and Server Extensibility**
Requests for programmatic API features (`ensureServer()`, #31821) and verbose MCP header support (#31802) indicate a maturing plugin ecosystem where users build custom server-side integrations.

**5. Internationalization**
Vietnamese language support (#29309) and Chinese output encoding fixes (#31830) signal a diversifying global user base needing locale-aware tooling.

---

## Developer Pain Points

**1. Performance Regressions (CRITICAL)**
Sharp CPU spikes (#30086) and persistent idle resource consumption (#31831, #16438) are the most pressing blockers. Multi-session workflows are becoming non-viable, and manual snapshot file cleanup is a recurring chore.

**2. Permission State Inconsistency**
Stale permission prompts that cannot be dismissed (#29422, #28312) or yield “Permission request not found” errors force session restarts, breaking flow and trust in the prompt system.

**3. Model Integration Fragility**
Tool-call text leaking into assistant messages (#31247), failure on reasoning_content (#26762), and broken caching (#31755) suggest the model integration layer needs hardening against provider-specific API quirks.

**4. Web UI Gaps**
Remote developers face significant hurdles: inability to browse drives (#6490), missing UI elements (#30158), and ugly xdg-open errors in containers (#31815) degrade the web experience.

**5. Configuration and Startup Stability**
YAML agent files crashing startup (#31481), V1 shell tools lacking destructive command guards (#31774), and install scripts failing to guide PATH reloading (#18624) create friction for new and power users alike.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the **Pi Community Digest** for **2026-06-11**.

---

## Pi Community Digest — 2026-06-11

### 1. Today’s Highlights
TUI stability dominated yesterday’s bug fixes, with three separate patches landing for CJK rendering, overlay compositing, and crash prevention from undefined tool results. On the provider side, a major enterprise PR dropped adding first-class Palantir Foundry support alongside Amazon Bedrock Mantle, while the community’s hottest debate continued over the new Project Trust gating UX—illustrating the delicate balance between security defaults and frictionless workflows.

### 2. Releases
No new versions were tagged in the last 24 hours.

---

### 3. Hot Issues

1. **#5514 – Project Trust Feature Feedback**  
   [earendil-works/pi Issue #5514](https://earendil-works/pi/issues/5514)  
   *25 comments, 13 👍*  
   The highest-traffic thread of the day. Users are pushing back against the new dependency/project trust gate, arguing it feels redundant across machines and lacks a persistent “always trust” escape hatch. This is the key UX tension moving forward.

2. **#4160 – pi extensions does not play nice with Bun**  
   [earendil-works/pi Issue #4160](https://earendil-works/pi/issues/4160)  
   *9 comments*  
   The Bun + npm dependency conflict persists. Pi’s extension installer hard‑codes `npm`, breaking for pure‑Bun environments. The auto‑generated AI workaround is clever but messy; community appetite for a first‑party Bun installer is high.

3. **#5611 – GitLab Duo Anthropic streams hit ~90s cutoff before message_stop**  
   [earendil-works/pi Issue #5611](https://earendil-works/pi/issues/5611)  
   *3 comments*  
   Causes automatic retries with full payloads, wasting tokens and user time. The core parser treats an early stream close as an error rather than a valid gate‑enforced end.

4. **#5536 – Split-turn compaction sends parallel summarization requests, causing 429 on local backends**  
   [earendil-works/pi Issue #5536](https://earendil-works/pi/issues/5536)  
   *2 comments*  
   Auto‑compaction fails on single‑concurrency local models (e.g., llama.cpp). The parallel summary launch assumption breaks the core memory‑management pipeline for offline users.

5. **#5605 – MiniMax-M3: cache_control ignored on Anthropic endpoint; broken thinking on OpenAI-compat**  
   [earendil-works/pi Issue #5605](https://earendil-works/pi/issues/5605)  
   *2 comments*  
   Cost multiplier: ignoring `cache_control` on the Anthropic route users are billed at 5× the expected cache rate. Also highlights the difficulty of routing extended‑thinking features across disparate backends.

6. **#5603 – Cost reporting: 1-hour prompt-cache writes priced at 5‑minute rate**  
   [earendil-works/pi Issue #5603](https://earendil-works/pi/issues/5603)  
   *1 comment*  
   Anthropic’s 1‑hour cache writes bill at 2× base input, but Pi prices all cache writes at the 1.25× 5‑minute rate. Financial underreporting erodes user trust in session cost estimates.

7. **#5604 – WorkflowEditor crash: TypeError: value.startsWith is not a function**  
   [earendil-works/pi Issue #5604](https://earendil-works/pi/issues/5604)  
   *1 comment*  
   A hard crash—not a UI flicker—that kills the entire agent process. The autocomplete handler assumes `value` is a string; non‑string suggestion payloads cause an uncaught exception.

8. **#5601 – Login to GHC subscription fails with unhelpful error**  
   [earendil-works/pi Issue #5601](https://earendil-works/pi/issues/5601)  
   *3 comments*  
   The subscription activation funnel is completely blocked for GitHub Copilot users. The error message lacks diagnostic detail, making self‑remediation impossible.

9. **#5291 – Sessions hang on “Working…” when used with Anthropic Enterprise subscription**  
   [earendil-works/pi Issue #5291](https://earendil-works/pi/issues/5291)  
   *5 comments*  
   Interrupt/resume doesn’t reliably recover stalled sessions. This is a top‑tier reliability complaint for Pi’s flagship model integration.

10. **#5598 – Android Termux local multiline paste auto‑submits**  
    [earendil-works/pi Issue #5598](https://earendil-works/pi/issues/5598)  
    *1 comment*  
    Pasting multi‑line text triggers premature submission in the TUI. Works fine over SSH, indicating an input‑event buffering bug specific to the Termux raw terminal.

---

### 4. Key PR Progress

1. **#5609 – feat(providers): add Palantir Foundry LLM proxy and OAuth provider**  
   [earendil-works/pi PR #5609](https://earendil-works/pi/pull/5609)  
   A significant enterprise play: adds native Foundry routing for Anthropic, Google, xAI, and OpenAI models, plus Foundry OAuth token handling and global “max” thinking levels for Opus 4.8.

2. **#5594 – Fix Anthropic stream finalization on message_stop**  
   [earendil-works/pi PR #5594](https://earendil-works/pi/pull/5594)  
   Treats `message_stop` as the logical end of an assistant message instead of waiting for transport EOF. Cancels the body reader early to release connections and placate strict proxies.

3. **#5509 [Open] – feat: Add Amazon Bedrock Mantle OpenAI Responses provider**  
   [earendil-works/pi PR #5509](https://earendil-works/pi/pull/5509)  
   Opens up AWS’s managed GPT‑5.5/5.4 models. Modeled after the Azure OpenAI provider; expands Bedrock beyond Claude.

4. **#5600 [Open] – fix(ai): honor Codex SSE header timeout setting**  
   [earendil-works/pi PR #5600](https://earendil-works/pi/pull/5600)  
   Replaces a previously hardcoded 10‑second SSE header timeout with the caller‑configured `timeoutMs`, fixing failures on slow/unstable connections.

5. **#5561 – feat(ai): link AWS data retention docs in Bedrock validation errors**  
   [earendil-works/pi PR #5561](https://earendil-works/pi/pull/5561)  
   Catches the opaque Fable 5 data‑retention error and links directly to the AWS Bedrock documentation. A model of good developer‑experience error handling.

6. **#5587 – feat(coding-agent): add experimental first‑time setup flow**  
   [earendil-works/pi PR #5587](https://earendil-works/pi/pull/5587)  
   Behind `PI_EXPERIMENTAL=1`, introduces a setup dialog on first launch: terminal theme detection + preview, analytics opt‑in, and an explicit dark/light choice.

7. **#5560 – fix(coding-agent): parse :thinking suffix from custom model IDs in fallback path**  
   [earendil-works/pi PR #5560](https://earendil-works/pi/pull/5560)  
   Fixes a regression where the `:thinking` suffix was not stripped for models outside the built‑in registry, causing 404 requests and lost reasoning‑level config.

8. **#5589 – fix(tui): stabilize overlay compositing at wide char boundary**  
   [earendil-works/pi PR #5589](https://earendil-works/pi/pull/5589)  
   Corrects overlay horizontal shifting when the start column lands in the middle of a CJK or Korean wide grapheme. A quality‑of‑life fix for i18n users.

9. **#5562 – fix(tui): separate list items with blank lines in loose lists**  
   [earendil-works/pi PR #5562](https://earendil-works/pi/pull/5562)  
   Brings TUI markdown rendering in line with CommonMark 0.31.2 by inserting blank lines between items in “loose” lists.

10. **#5585 – fix(tui): wrap CJK text at character boundaries in editor**  
    [earendil-works/pi PR #5585](https://earendil-works/pi/pull/5585)  
    Fixes a text‑wrapping bug in the TUI editor where CJK text was broken mid‑grapheme, causing line corruption.

---

### 5. Feature Request Trends

- **Enterprise Proxy & Provider Expansion**  
  The strongest signal this week is enterprise procurement: Palantir Foundry, Amazon Bedrock Mantle, and GitLab Duo all received dedicated integration work. Users expect Pi to be a first‑class citizen behind corporate gateways.

- **Extensibility Hooks**  
  Two requests target deeper extension APIs: an event for command execution (#5608) and a custom OAuth callback renderer (#5372). The community wants Pi to be a head‑less platform, not just a TUI.

- **Persona‑Based System Prompts**  
  Issue #5577 asks for a “persona override” so Pi can act as a security engineer, PM, or video editor without losing its coding context. This signals a desire for Pi to become a general‑purpose agentic harness.

---

### 6. Developer Pain Points

- **Protocol & Proxy Fragility**  
  Anthropic stream handling (finalization, early cutoffs, cache‑control mismatches) and proxy compatibility remain the deepest source of friction. Users debugging “message_stop” race conditions or 429 compaction retries report hours of wasted work.

- **Cost Configuration Traps**  
  Cache billing rates (#5603, #5605) and API‑key routing bugs (e.g., Bedrock `apiKey` silently ignored in PR #5586) erode confidence in the tool’s financial telemetry.

- **TUI Instability**  
  The TUI crash count is worrying. Hard process kills from undefined tool results (#5597, #5599) and incomplete autocomplete guardrails (#5604) make the shell‑mode experience fragile for heavy users.

- **Platform Blockers**  
  Foundational issues remain for niche—but loyal—platforms: no `npm`‑free extension install for Bun, paste handling broken on Android Termux, and self‑update banners pointing to dead‑end commands for Nix/managed installs (#5607).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for 2026-06-11.

---

## Qwen Code Community Digest — June 11, 2026

### 1. Today's Highlights

This week's activity sees a mature codebase balancing massive architectural shifts with persistent stability concerns. The long-running daemon mode feature batch (`#4490`) and ACP/REST parity effort (`#4827`) signal a significant move toward a server-client architecture. Simultaneously, a high-severity security issue (`#4930`) was resolved, while the community continues to report friction with MCP tool validation, terminal input handling, and subagent memory interference.

### 2. Releases

No new releases were published in the last 24 hours. The current stable version remains **0.17.1**.

### 3. Hot Issues (10 of 27)

*   **[#4973] [P1/Bug] Terminals dropping to cooked mode, freezing all input**
    A critical CLI bug where `KeypressContext` fails to re-acquire raw mode, causing the terminal to freeze entirely until the user presses Enter. This is a major UX blocker affecting all interactive sessions. [View Issue](https://github.com/QwenLM/qwen-code Issue #4973)

*   **[#4930] [P1/Security/Closed] `env` command in read-only allowlist enables arbitrary execution**
    A significant security vulnerability was fixed: the `env` command was incorrectly whitelisted as "read-only," allowing it to bypass user confirmation prompts and execute arbitrary side effects. [View Issue](https://github.com/QwenLM/qwen-code Issue #4930)

*   **[#4838] [P1/Performance/Closed] Hook continuations skip microcompaction in `/goal` loops**
    A critical performance issue where context compaction was skipped during Hook-based `/goal` loops, leading to rapid context window saturation and degraded model performance on long-running tasks. [View Issue](https://github.com/QwenLM/qwen-code Issue #4838)

*   **[#4974] [P2/Bug] SGR mouse wheel sequences leak as typed text into the input box**
    A terminal-compatibility issue where raw escape codes leak into the user's prompt, creating visual noise and potential input corruption. Highlights the fragility of the current mouse event handling pipeline. [View Issue](https://github.com/QwenLM/qwen-code Issue #4974)

*   **[#4942] [P2/Bug] VP mode scroll input conflicts with Composer completely**
    The new Virtualized History mode is currently incompatible with the Composer input. Users cannot scroll chat history during the most common workflow (after an AI response), making the feature essentially unusable. [View Issue](https://github.com/QwenLM/qwen-code Issue #4942)

*   **[#4966] [P2/Bug] MCP missing numeric string coercion causes widespread tool failures**
    A high-impact, simple-to-fix bug where strict MCP servers reject commonly emitted numeric strings (e.g., `"depth": "3"`), causing frequent tool-calling failures across the ecosystem. [View Issue](https://github.com/QwenLM/qwen-code Issue #4966)

*   **[#4876] [P2/Bug/Closed] Subagent reads images but returns entirely unrelated content**
    A core reliability gap in subagent delegation: when reading images via `read_file`, the subagent returns content completely unrelated to the image, even though the parent agent handles the same task correctly. [View Issue](https://github.com/QwenLM/qwen-code Issue #4876)

*   **[#4976] [P2/Bug] Auto-memory derails normal CLI tool calls**
    A detailed user report showing how auto-generated memory entries from the memory system inject irrelevant context into subsequent tool calls, wasting tokens and breaking focused workflows. [View Issue](https://github.com/QwenLM/qwen-code Issue #4976)

*   **[#4904] [Bug] Cannot switch to new qwen models (e.g., qwen3.7-plus)**
    Users face hardcoded provider model lists, preventing manual switching to the latest models. This creates provider lock-in friction and limits flexibility for power users. [View Issue](https://github.com/QwenLM/qwen-code Issue #4904)

*   **[#4597] [Feature Request/Closed] Cross-session persistent usage statistics**
    A highly popular request (1 👍) to bring persistent, cross-session `/stats` (following Claude Code's model). The current implementation loses all telemetry data on CLI exit. [View Issue](https://github.com/QwenLM/qwen-code Issue #4597)

### 4. Key PR Progress (10 of 50)

*   **[#4490] Daemon mode merge: +115k LOC integration**
    The massive daemon-mode feature batch (`daemon_mode_b_main`) is being merged into `main`, introducing the foundational server-client architecture for v0.16-alpha. [View PR](https://github.com/QwenLM/qwen-code PR #4490)

*   **[#4827] ACP/REST parity achieved (29 new methods)**
    Achieves full feature parity between the ACP and REST APIs, adding 29 new `_qwen/*` dispatch methods for session management, shell control, and context inspection. [View PR](https://github.com/QwenLM/qwen-code PR #4827)

*   **[#4965] Unified settings hot-reload endpoint**
    Introduces `POST /workspace/reload`, replacing the narrower `reload-env` to allow a single atomic hot-reload of all settings changes to idle daemon sessions. [View PR](https://github.com/QwenLM/qwen-code PR #4965)

*   **[#4853] `enter_plan_mode` tool and Plan Approval Gate**
    Adds a structured planning protocol for complex tasks. The model can proactively enter a plan mode; when auto/yolo approval is enabled, exiting plan mode triggers an approval gate. [View PR](https://github.com/QwenLM/qwen-code PR #4853)

*   **[#4893] `/compress-fast` command for no-LLM context compression**
    A new CLI command for rule-based, non-LLM context compression, offering users a lightweight and cheap escape from full context windows. [View PR](https://github.com/QwenLM/qwen-code PR #4893)

*   **[#4896] Stabilize prompt cache against MCP/skills churn**
    A significant fix that decouples skill visibility from validation, preventing mid-session MCP/skills changes from invalidating the entire prompt cache. [View PR](https://github.com/QwenLM/qwen-code PR #4896)

*   **[#4982] Remove dead `debugResponses` array to prevent OOM**
    A simple but crucial fix removing an unbounded array that accumulated every streaming chunk, preventing memory pressure in long sessions. [View PR](https://github.com/QwenLM/qwen-code PR #4982)

*   **[#4954] Isolate per-session stats in daemon mode**
    Fixes a data isolation bug where the daemon served aggregate process-wide stats instead of per-session metrics, correcting a fundamental reporting issue. [View PR](https://github.com/QwenLM/qwen-code PR #4954)

*   **[#4598] Collapsible thinking blocks with duration timer**
    Enhances the TUI with collapsible, timestamped reasoning blocks, keeping the interface clean while streaming long chain-of-thought outputs. [View PR](https://github.com/QwenLM/qwen-code PR #4598)

*   **[#4971] Reduce retained interactive tool output memory**
    Addresses a common memory bloat issue by compacting large tool output display metadata stored in UI history, scheduler state, and subagent summaries. [View PR](https://github.com/QwenLM/qwen-code PR #4971)

### 5. Feature Request Trends

The community's feature appetite is currently centered around three pillars:

*   **Agentic Workflows & Permissions**: There is a strong push for maturing sub-agent background execution. Requests focus on queuing permission approvals to parent sessions (`#4928`), enabling the fork subagent by default (`#4956`), and structured planning (`#4853`).
*   **Robust Context Management**: Users consistently request better CLI warnings for oversized context files (`#4941`), mechanisms to recover from max-tokens truncation gracefully (`#4964`), and lighter-weight compression options (`#4893`).
*   **Actionable Telemetry**: The community wants persistent, cross-session dashboards (`#4597`) and temporal awareness in logs (`#4899`) to better audit agent behavior and token consumption over time.

### 6. Developer Pain Points

The most acute developer frustrations stem from the terminal environment and integration fragility:

*   **Terminal Chaos**: Issues related to raw mode (`#4973`), mouse escape sequences (`#4974`), SSH environment quirks (`#4926`), and Windows installer bugs (`#4901`) dominate the bug tracker, indicating a challenging cross-platform UX effort.
*   **MCP Ecosystem Fragility**: The strict type handling of MCP servers is a common stumbling block (`#4966`), along with the lack of granular server access control (`#4940`).
*   **Subagent Unpredictability**: A recurring pain point is the subagent system's unreliability, from ignoring prompts on image tasks (`#4876`) to automated memories derailing primary workflows (`#4976`).
*   **Provider Lock-in Perception**: The inability to seamlessly switch models or use the same model from different providers (`#4904`, `#4877`) creates a constrained feeling for a tool that aims to be modular.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**DeepSeek TUI (now CodeWhale) Community Digest – 2026-06-11**

---

### 1. Today's Highlights
The project officially ships **v0.8.57**, cementing the full rebrand to **CodeWhale** and deprecating the legacy `deepseek-tui` npm channel. Simultaneously, the **v0.8.58** branch is driving a major architectural shift toward universal model support, remote cloud operation, and a deterministic hook/policy engine. While the rebrand introduces significant migration friction, the community is actively contributing patches for config paths, error messages, and localization.

---

### 2. Releases
- **[v0.8.57](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.57)** (2026-06-11): Canonical release target is now **CodeWhale**. Legacy `deepseek-tui` npm package is frozen; users must follow `docs/REBRAND.md` to migrate.
- **[v0.8.56](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.56)** – *Community Harvest*: Localization updates across 7 locales, new provider additions, prefix-cache stability fixes, and general bug patches.

---

### 3. Hot Issues

1. **[#2369](https://github.com/Hmbown/CodeWhale/issues/2369) – Config Paths Fragmented Across OS/Cygwin**  
   Users on Cygwin and cross-OS workflows hit corrupted config states due to inconsistent resolution logic. A silent migration bug makes detection difficult. (6 comments)

2. **[#1679](https://github.com/Hmbown/CodeWhale/issues/1679) – SSE Multi-Agent Timeout & UI Breakdown (Windows)**  
   Parallel sub-agents hard-fail after a 45s timeout on Windows 11, often coupled with severe UI layout corruption. (3 comments)

3. **[#1806](https://github.com/Hmbown/CodeWhale/issues/1806) – Sub-Agent 120s API Timeout**  
   All sub-agents fail identically with a 120s timeout when processing large documents, breaking the core parallel offload promise. (3 comments)

4. **[#2574](https://github.com/Hmbown/CodeWhale/issues/2574) – Provider Fallback Chain**  
   Highly requested: automatic fallback to backup providers on 401/429/5xx errors, eliminating the need for manual `/provider` switching. (3 comments)

5. **[#2989](https://github.com/Hmbown/CodeWhale/issues/2989) – False "Completed" Status with Ollama/Qwen**  
   Dangerous behavior: the agent stops mid-task but reports task status as "completed" when using local models like `qwen3-coder:30b`. (1 comment)

6. **[#2893](https://github.com/Hmbown/CodeWhale/issues/2893) – SiliconFlow Provider Config Duplication**  
   Users must duplicate identical config values into both `[providers.siliconflow]` and `[providers.siliconflow-CN]` for the provider to work at all. (2 comments)

7. **[#3004](https://github.com/Hmbown/CodeWhale/issues/3004) – Dynamic API Key from Script**  
   Security-focused request to source `api_key` from external commands (e.g., KeepassXC) instead of plaintext in `.env` or `config.toml`. (2 comments)

8. **[#2372](https://github.com/Hmbown/CodeWhale/issues/2372) – `task_shell_start` TTY Mode Broken**  
   `tty: true` does not set a controlling terminal, breaking essential tools like `sshpass` that depend on `/dev/tty`. (2 comments)

9. **[#2934](https://github.com/Hmbown/CodeWhale/issues/2934) – Sidebar Sessions Panel**  
   Request for a persistent, browsable session panel to replace the current `Ctrl+R` popup workflow for session management. (1 comment)

10. **[#3012](https://github.com/Hmbown/CodeWhale/issues/3012) – Global `instructions.md` for Cross-Project Context**  
    User wants `~/.codewhale/instructions.md` auto-loaded as a fallback context layer, mirroring project-level `.codewhale/instructions.md`. (1 comment)

---

### 4. Key PR Progress

1. **[#3034](https://github.com/Hmbown/CodeWhale/pull/3034) – v0.8.58 Foundation PR**  
   The main branch for the next release: YAML-based constitution refactor, Codex/Responses client fixes, and sidebar panel improvements.

2. **[#3053](https://github.com/Hmbown/CodeWhale/pull/3053) – Rebrand Migration Docs**  
   Community PR adding a dedicated “Upgrading from deepseek-tui” section to the README, directly addressing migration confusion.

3. **[#3045](https://github.com/Hmbown/CodeWhale/pull/3045) – Un-hardcode Sub-Agent Model Validation**  
   Fixes `requested_model_for_provider` to accept non-DeepSeek model IDs, enabling Ollama, Moonshot, and OpenAI models as sub-agents.

4. **[#3049](https://github.com/Hmbown/CodeWhale/pull/3049) – Hooks v2**  
   Introduces JSON decision contracts (`deny`/`allow`/`ask` + `updatedInput`), glob matchers, and project-local hooks for deterministic policy enforcement.

5. **[#3042](https://github.com/Hmbown/CodeWhale/pull/3042) – Headless Exec Hardening**  
   Adds `--allowed-tools`, `--disallowed-tools`, `--max-turns`, and `--append-system-prompt` flags to `codewhale exec` for CI/benchmarking.

6. **[#3044](https://github.com/Hmbown/CodeWhale/pull/3044) – Remote Autonomous Loop Infra**  
   Upgrades the DigitalOcean remote-smoke setup with swapfile, `gh` CLI, and agent-session scripts for unattended droplet operation.

7. **[#3037](https://github.com/Hmbown/CodeWhale/pull/3037) – Compact Tool-Call Transcript Rendering**  
   Suppresses low-value boilerplate (`"(no output)"`, sub-second timings) in the default compact/Live transcript view.

8. **[#3051](https://github.com/Hmbown/CodeWhale/pull/3051) – Voice Input via `/voice`**  
   Adds speech-to-text slash commands, reusing the active provider’s chat completions API for inference—inspired by MiMo Code.

9. **[#2579](https://github.com/Hmbown/CodeWhale/pull/2579) – AppendLog Backing Store (Merged)**  
   Completes Phase 4 of the architecture refactor, replacing `Session.messages: Vec<Message>` with an `AppendLog` structure.

10. **[#3040](https://github.com/Hmbown/CodeWhale/pull/3040) – Clickable Sidebar Rows**  
    Adds mouse-click dispatch to Tasks and Agents sidebar panels for immediate action (show/cancel/inspect).

---

### 5. Feature Request Trends

- **Universal Model Support & Provider Neutrality**: The strongest signal is the demand to decouple CodeWhale from DeepSeek internals. Users want native Anthropic API support (#3014), un-hardcoded auto-routing (#3018), provider fallback chains (#2574), and accurate self-identification for non-DeepSeek models in the constitution prompt (#3025).
- **Remote Cloud & CI Deployment**: A deliberate maintainer push, matched by user interest, for a 24/7 remote agent running on cheap US infrastructure (DigitalOcean + Telegram bridge, #2964), coupled with hardened `codewhale exec` flags for unattended CI loops (#3027).
- **Enhanced Session & Context Management**: Persistent, browsable session panels (#2934), global-level instructions (#3012), and structured sidebar inspection for long-running tasks (#2889, #2018) are high-frequency QoL requests.
- **Developer Security & Compliance**: Requests for dynamic API key sourcing (#3004) and the Hooks v2 deterministic policy engine (#3026, #3049) show a maturing user base demanding safe key management and auditable tool execution.

---

### 6. Developer Pain Points

- **Rebranding Migration Fracture**: The transition from `deepseek-tui` to `CodeWhale` is the top friction source. Config paths are fragmented (#2369), the TUI still surfaces legacy DeepSeek paths (#2664), and the update path from the old npm package fails silently without clear instructions (#2960, #3053).
- **Sub-Agent Instability**: The multi-agent subsystem is the most frequently broken feature. Hard timeouts (45s, 120s) on Windows are the norm (#1679, #1806), and the silent false "completed" status with local models (#2989) severely undermines trust in the agent framework.
- **Windows & TTY Gaps**: Windows users bear the brunt of agent timeout bugs. The lack of proper controlling terminal emulation for `task_shell_start` breaks essential devops tooling like `sshpass` (#2372).
- **Misleading Error Diagnostics**: Error messages often misattribute the source of a problem (e.g., blaming a `--provider` flag that the user never passed), wasting debugging time (#3007, #3041).
- **Provider Configuration Quirks**: Minor but persistent configuration friction—such as requiring duplicate SiliconFlow sections (#2893)—creates an impression of incomplete provider abstraction.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*