# AI CLI Tools Community Digest 2026-06-02

> Generated: 2026-06-02 03:39 UTC | Tools covered: 9

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

**Cross-Tool Ecosystem Report: AI CLI Developer Tools**
**Date:** 2026-06-02

---

### 1. Ecosystem Overview

The AI CLI development tool landscape on June 2, 2026, is defined by a fundamental tension between the pace of agent feature innovation and the operational reliability required for production use. Across the ecosystem, communities are paying significant API costs for upstream bugs—from Opus 4.7 parsing failures in Claude Code to streaming body timeouts in Qwen Code and silent hangs in Pi—eroding trust in autonomous agent workflows. A clear bifurcation is emerging between tightly integrated, first-party model ecosystems (Claude Code, OpenAI Codex, GitHub Copilot) and open, extensible platform plays (OpenCode, Pi, Gemini CLI, CodeWhale) that prioritize local model support and deep customization via MCP, skills, and hooks. Platform parity on Windows and Linux remains a persistent secondary crisis, while context window management and token cost observability have become the defining reliability metrics for long-running user sessions across every tool surveyed.

---

### 2. Activity Comparison

| Tool | Community Issues (Key Signal) | PR Velocity (Today's Signal) | Release Today |
|---|---|---|---|
| **Claude Code** | Very High (Opus parsing regression crisis, Rewind UX backlash) | Moderate (Docs fixes, stale policy) | **Yes** (v2.1.160) |
| **OpenAI Codex** | High (Linux Desktop App demand, Windows OAuth failures, Gmail security incident) | High (PAT auth, symlink hardening, Desktop handoff) | **Yes** (rust-v0.136.0) |
| **Gemini CLI** | High (Generalist agent hangs, Sub-agent false SUCCESS reports) | **Very High** (Notebook tool, /model command, ripgrep port merged) | **Yes** (v0.45.0-nightly) |
| **GitHub Copilot CLI** | Moderate (Clipboard regression, MCP governance, memory loops) | Low (Internal triage focus) | **Yes** (v1.0.57) |
| **Kimi Code CLI** | Low (Text wrapping bug, Zoo Code API whitelist request) | Moderate (OAuth rollback logic, /copy command) | No |
| **OpenCode** | **Very High** (Pricing API debate at 61👍, Desktop MCP blank-state, Permission system unreliability) | **Very High** (PermissionV2 rewrite, Core accounts refactor) | No |
| **Pi** | High (TimeoutMs ignored, Ghostty flicker, Provider stream hangs) | **Very High** (Tool call sanitization for local models, CJK/TUI fixes, keybindings) | No |
| **Qwen Code** | High (Local LLM config hell, Body timeouts, Memory leak in --resume) | **Very High** (Auto-update infrastructure, CPU profiling, Telemetry Phase 3) | **Yes** (v0.17.0-nightly) |
| **DeepSeek/CodeWhale** | High (Token explosion at 400M tokens, low cache hits, YOLO mode stalls) | **Very High** (NSIS Windows installer, i18n wave across 7 locales, configurable API paths) | **Yes** (v0.8.49 Rebrand) |

---

### 3. Shared Feature Directions

Several critical requirements are surfacing simultaneously across multiple communities, indicating strong market consensus:

- **MCP/Plugin Governance & Granular Sandboxing:** Communities across the board are demanding fine-grained, reliable permission systems beyond binary allow/deny.
  - *Evidence:* Copilot CLI (#768 disable-by-default, #3028 granular perms), OpenCode (PermissionV2 PR #30287, subagent MCP perms #30085), Claude Code (auth deadlocks #64397), CodeWhale (typed execution policies #1186).

- **Platform Parity (Windows & Linux):** A universal pain point. Every tool faces active, unresolved bugs on non-macOS platforms.
  - *Evidence:* Claude (ARM64 VM freeze #40198), Codex (Linux Desktop #11023 at 389👍, WSL perf #25715), Pi (CJK/WSL fixes #5264, #5295), Qwen (Windows token doubling #4420), CodeWhale (Win11 freeze #1812, NSIS installer #2045).

- **Context Window & Memory Maturation:** Long agent sessions are hitting hard ceilings—tools that cannot efficiently manage context or persist memory are actively rejected by power users.
  - *Evidence:* Claude (compaction fails #63896, agent state loss #23620), Copilot (infinite compaction loops #3621), CodeWhale (no cross-session memory #2492), Gemini (AST-grounded tools to reduce token noise #22745), OpenCode (manual context controls #1990).

- **Local & Private Model Integration:** The “Ollama configuration” problem is a top complaint. Robust local fallback is a key retention driver.
  - *Evidence:* Qwen Code (#3384 config failure, #4604 body timeout, PR #4667 configurable timeout), Pi (tool call validation for Qwen/Llama #5307, timeout respect #5089), CodeWhale (configurable API path suffix #2508), Copilot (BYOM endpoint request #3624).

- **Cost-to-Output Transparency & Efficiency:** Users are acutely sensitive to tokens wasted on retries, bugs, and inefficient agent loops.
  - *Evidence:* CodeWhale (#743 400M tokens in 6hrs, #1177 low cache hits), Claude (paying for image failures #60334), Codex (retry logic for streamable HTTP #25147), OpenCode (real-time pricing API demand #28846 at 61👍).

---

### 4. Differentiation Analysis

| Tool | Core Philosophy | Target User & Technical Approach | Competitive Vulnerability |
|---|---|---|---|
| **Claude Code** | High-end managed agent tightly coupled to Opus | Pro devs seeking turnkey agentic autonomy. TypeScript. | Opus regression blunts all value. Vulnerable to model lock-in. |
| **OpenAI Codex** | Desktop-centric IDE companion with Computer Use | Developers within the OpenAI/Apple ecosystem. Rust. | Platform instability (Windows, Linux). Auth fragmentation. |
| **Gemini CLI** | Agent framework with evaluation-driven quality | Technical platform builders. TypeScript, sub-agents, skills. | General reliability lags feature velocity. Tool limits (128 tools). |
| **GitHub Copilot** | Integrated workflow tool for the GitHub universe | Enterprise devs on GitHub. Go. MCP ecosystem. | Model parity gap with VS Code. Context stability. Lower open-source velocity. |
| **OpenCode** | Extensible open-core platform | Plugin developers and customization enthusiasts. TypeScript, statecharts, PermissionV2. | MCP panel broke in latest Desktop. Permission system unreliability. |
| **Pi** | Performance-first, local-model champion | Power users across terminals. Rust, fast provider updates. | TUI cross-emulator fragmentation. Local model timeout tuning. |
| **Qwen Code** | Infrastructure-mature dual cloud/local agent | Devs needing robust auto-update, telemetry, and profiling. TypeScript. | Memory leaks, Windows render quality. Local config friction. |
| **CodeWhale** | Community chameleon, shedding DeepSeek identity | Globalized user base (7 locales). TypeScript, strong Windows focus. | Token cost perception. Migration uncertainty from rebrand. |

---

### 5. Community Momentum & Maturity

- **Highest Raw Feature Velocity:** **Gemini CLI** (Notebook, ripgrep, /model landed in one 24h window), **OpenCode** (PermissionV2 and core accounts refactor active), **Pi** (MiniMax M3 support immediately, deep local model forensics), and **CodeWhale** (external i18n contributors, NSIS installer) show the strongest development cadence.

- **Highest Community Engagement / Voice:** **OpenCode** is seeing the most heated cross-tool debate (pricing API, permissions), while **Claude Code** has the highest-urgency signals due to a critical regression. **Codex**’s Linux Desktop request sits at 389 upvotes—a massive latent demand signal.

- **Stability Crisis Mode:** **Claude Code** is in a trust-damaging reliability crisis with the Opus 4.7 parsing bug. **CodeWhale** faces a brand-level cost perception crisis (400M tokens). **Gemini CLI** is actively fighting its own agent’s reliability.

- **Lower Open-Source Velocity:** **GitHub Copilot CLI** and **Kimi Code CLI** show minimal PR activity, suggesting internal development cycles or smaller open-source contribution ecosystems relative to their user bases.

---

### 6. Trend Signals

1. **The “Agent Reliability Cliff” is the Ecosystem’s Largest Risk:** The combination of Opus parsing failures, agent hangs, silent success lies, and paying for failures creates a strong headwind against “set and forget” agent adoption. The next 30–60 days of stability patches will determine whether the category plateaus or accelerates.

2. **Open Ecosystems are Winning the Feature Race:** Tools embracing MCP, custom skills, and extensible APIs (Pi, OpenCode, Gemini CLI, CodeWhale) are landing major features faster than proprietary tools. Extensibility is becoming table stakes.

3. **Platform Neglect Represents a Structural Gap:** The consistent failure to support Windows ARM64, Linux ARM (musl), Wayland, and non-standard shells is leaving a significant underserved market. The tools that solve this (CodeWhale’s NSIS push, Codex’s Linux Desktop demand) will capture share.

4. **Cost Observability is the Next Battleground:** Beyond latency, users demand transparency into token consumption per task. Tools that surface per-call cost, compression efficiency, and cache hit ratios (CodeWhale cache hit complaints, OpenCode pricing API requests) will win the trust of price-sensitive developer power users.

5. **Observability and Debugging are Moving from Nice-to-Have to Table Stakes:** Qwen’s CPU profiling, Pi’s `ctx.isInteractive`, Codex’s `CodexErr` analytics, and OpenCode’s LLM header exposure signal that users want to *debug their agents* as easily as they debug their code. The quality of internal tooling that tool vendors build for themselves will soon be a customer-facing differentiator.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Claude Code Skills Ecosystem Community Highlights**
*Analysis of `github.com/anthropics/skills` Activity | Data as of 2026-06-02*

---

### 1. Top Skills Ranking

The following Pull Requests represent the most-discussed and highest-impact Skill submissions currently active in the repository.

1.  **Document Typography** ([PR #514 – Open](https://github.com/anthropics/skills/pull/514))
    *   **Functionality:** Automated quality control for generated documents, fixing orphan word wrap, widow paragraphs, and numbering misalignment.
    *   **Discussion Highlights:** The top-ranked PR by engagement. Community consensus that typographic polish is a critical gap in AI-generated long-form content.

2.  **ODT Skill** ([PR #486 – Open](https://github.com/anthropics/skills/pull/486))
    *   **Functionality:** Native creation, template filling, and parsing of OpenDocument Format (.odt, .ods) files for the LibreOffice / ISO-standard ecosystem.
    *   **Discussion Highlights:** Strong demand from users needing to bridge Claude Code with open-source office suites and enterprise document pipelines.

3.  **Testing Patterns Skill** ([PR #723 – Open](https://github.com/anthropics/skills/pull/723))
    *   **Functionality:** Full-stack testing methodology covering unit testing (AAA pattern), React Testing Library, E2E patterns, and the Testing Trophy model.
    *   **Discussion Highlights:** Addresses the quality ceiling of generated code—teaching Claude *how* to test rather than just what to build.

4.  **SAP RPT-1-OSS Predictor** ([PR #181 – Open](https://github.com/anthropics/skills/pull/181))
    *   **Functionality:** Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data directly into coding workflows.
    *   **Discussion Highlights:** A high-profile enterprise integration. Demonstrates demand for Claude orchestrating specialized third-party models.

5.  **ServiceNow Platform Skill** ([PR #568 – Open](https://github.com/anthropics/skills/pull/568))
    *   **Functionality:** Broad platform coverage across ITSM, ITOM, SecOps, ITAM/SAM, CSDM, and IntegrationHub.
    *   **Discussion Highlights:** Signals a shift from narrow utility skills to expansive "platform-assistant" skills that cover entire enterprise tool ecosystems.

6.  **AURELION Skill Suite** ([PR #444 – Open](https://github.com/anthropics/skills/pull/444))
    *   **Functionality:** Four-skill suite introducing a structured cognitive framework (5-floor kernel), an advisor, an agent, and a professional memory system.
    *   **Discussion Highlights:** Represents the "Skills-as-Framework" trend, where a single submission teaches a complete methodology rather than a single task.

7.  **Shodh Memory Skill** ([PR #154 – Open](https://github.com/anthropics/skills/pull/154))
    *   **Functionality:** Persistent context system for AI agents using proactive memory retrieval and structured content storage across conversations.
    *   **Discussion Highlights:** Long-standing community demand for true persistent memory surfaces here with a production-ready implementation.

8.  **Meta-Skills: Quality & Security Analyzers** ([PR #83 – Open](https://github.com/anthropics/skills/pull/83))
    *   **Functionality:** Two evaluator skills that analyze other skills across five dimensions (structure, documentation, security, etc.).
    *   **Discussion Highlights:** The ecosystem is self-organizing around quality standards—a key indicator of platform maturation.

---

### 2. Community Demand Trends

The most significant themes emerging from Issues data:

- **Enterprise Readiness & Governance:** The highest-signal issues cluster around organizational features. [Issue #228](https://github.com/anthropics/skills/issues/228) (org-wide sharing, 13 comments) and [Issue #492](https://github.com/anthropics/skills/issues/492) (trust boundary abuse, 7 comments) show urgent demand for managed distribution, permissions, and security namespacing.

- **Developer Tooling Reliability:** Critical infrastructure pain persists. [Issue #556](https://github.com/anthropics/skills/issues/556) (run_eval.py 0% trigger rate, 9 comments) and [Issue #202](https://github.com/anthropics/skills/issues/202) (skill-creator overhaul, 8 comments) highlight that the skill *development* experience is a bottleneck to ecosystem growth.

- **Plugin & Distribution Integrity:** [Issue #189](https://github.com/anthropics/skills/issues/189) (plugin deduplication, 6 comments, 8 👍) and [Issue #1087](https://github.com/anthropics/skills/issues/1087) (incorrect plugin loading) reveal confusion around how skills are packaged and delivered.

- **Cross-Platform Interoperability:** [Issue #16](https://github.com/anthropics/skills/issues/16) (Skills as MCPs) and [Issue #29](https://github.com/anthropics/skills/issues/29) (Bedrock support) remain recurring foundational requests.

- **Skill Complexity Ceiling:** [Issue #1220](https://github.com/anthropics/skills/issues/1220) (multi-file preload) and [Issue #1102](https://github.com/anthropics/skills/issues/1102) (MCP data overflow) indicate skills are hitting architectural limits as they grow in sophistication.

---

### 3. High-Potential Pending Skills

These active PRs address critical ecosystem gaps, maintain strong discussion momentum, and are likely to merge soon:

- **YAML Special Character Validation** ([PR #361 – Updated 2026-06-01](https://github.com/anthropics/skills/pull/361)). Silently corrupted `description` fields are a blocker for every skill creator. Very recent updates suggest imminent merge.

- **Document Skill Bugfixes** ([PR #538](https://github.com/anthropics/skills/pull/538) – PDF case-sensitivity, [PR #541](https://github.com/anthropics/skills/pull/541) – DOCX `w:id` collisions). Core reliability fixes for two of the most-used skill families.

- **Frontend Design Skill Overhaul** ([PR #210 – Updated 2026-03-07](https://github.com/anthropics/skills/pull/210)). A substantial rewrite for actionability and context-awareness. Sets the template for how foundational skills are being upgraded to meet higher quality standards.

- **Workflow Automation Skills** ([PR #190 – Updated 2026-05-18](https://github.com/anthropics/skills/pull/190)). Adds production-tested `n8n-builder`, `n8n-debugger`, and `faf-expert` skills. Automation remains the community's consistently highest-velocity topic.

- **Windows Compatibility Layer** ([PR #1099](https://github.com/anthropics/skills/pull/1099) & [PR #1050](https://github.com/anthropics/skills/pull/1050) – Both Updated 2026-05-24). Fixes subprocess spawning and encoding issues that currently make the skill-creator tools inoperable on Windows. High impact for expanding the contributor base.

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand is the professionalization of the Skills ecosystem—moving from experimental agentic prompts toward a secure, governance-aware, and rigorously validated application platform, with an intense focus on document fidelity, enterprise platform integration, and reliable developer tooling.

---

# Claude Code Community Digest // 2026-06-02

## 1. Today's Highlights

The Claude Code team has shipped **v2.1.160** with critical safety guardrails, addressing long-standing consent gaps by prompting before writing to shell startup files and build-tool configs. However, the dominant story on the issue tracker is a **severe Opus 4.7 tool call parsing regression** ([#62123](https://github.com/anthropics/claude-code/issues/62123), [#63875](https://github.com/anthropics/claude-code/issues/63875)) that is bricking sessions mid-task. Meanwhile, the unsafe default behavior of `/rewind` silently reverting code ([#64615](https://github.com/anthropics/claude-code/issues/64615)) continues to attract strong community backlash.

## 2. Releases

**v2.1.160** — Focus on consent and security:

- **Shell startup file protection:** Claude Code now prompts for confirmation before writing to `.zshenv`, `.zlogin`, `.bash_login`, or `~/.config/git/`. This closes a dangerous attack vector where unintended modifications could lead to automatic command execution on shell start.
- **`acceptEdits` build-tool guard:** Writing to `.npmrc` and similar config files that grant code execution now requires explicit approval, even in `acceptEdits` mode.

This release addresses a genuine trust deficit in the tool's permission model and is a welcome step toward safer agentic behavior.

---

## 3. Hot Issues

**1. [#62123 – Opus 4.7 tool call parsing failure](https://github.com/anthropics/claude-code/issues/62123)** [56 👍, 36 comments]
The most urgent open bug. Opus 4.7 sessions are killed mid-task with `The model's tool call could not be parsed (retry also failed)`. Users report this occurring *repeatedly* across sessions, effectively blocking work. High velocity (created May 25, massive engagement in 8 days).

**2. [#63875 – Recurring tool parse error (duplicate signal)](https://github.com/anthropics/claude-code/issues/63875)** [19 👍, 20 comments]
Confirms the scope of the parsing crisis — affecting users on multiple platforms and sessions. The duplicates alone indicate a top-priority reliability regression.

**3. [#49747 – Opus 4.7 mixes legacy XML format into JSON tool calls](https://github.com/anthropics/claude-code/issues/49747)** [13 👍, 20 comments]
The most technically informative report. On longer payloads, Opus 4.7 reverts to legacy XML tool-use format inside JSON calls, crashing the parser. Identified as a *regression* — this was previously stable.

**4. [#40198 – Cowork VM fails on Windows ARM64](https://github.com/anthropics/claude-code/issues/40198)** [7 👍, 53 comments]
A marathon thread (since March 2026). Cowork environments fail to start on Snapdragon X / Galaxy Book4 Edge. High comment count signals deep frustration with a lack of resolution on ARM64 Windows.

**5. [#60334 – Image processing errors burning token budgets](https://github.com/anthropics/claude-code/issues/60334)** [13 👍, 41 comments]
Users report losing ~70% of their 5-hour usage window to image processing failures — paying full cost for zero output. Closed, but the underlying cost-due-to-bugs pattern is a recurring theme.

**6. [#64615 – `/rewind` silently reverts code without confirmation](https://github.com/anthropics/claude-code/issues/64615)** [3 👍, 2 comments]
Created today, but tapping into a long stream of prior frustration ([#27387](https://github.com/anthropics/claude-code/issues/27387), [#50897](https://github.com/anthropics/claude-code/issues/50897)). The default `Restore code and conversation` option is destructive and has no confirmation dialog.

**7. [#23620 – Agent team configuration lost on context compaction](https://github.com/anthropics/claude-code/issues/23620)** [10 👍, 16 comments]
During long sessions, context compaction wipes the multi-agent team setup. A structural problem for power users relying on agent teams.

**8. [#53922 – Parallel sessions rate-limited after window reset](https://github.com/anthropics/claude-code/issues/53922)** [1 👍, 10 comments]
Bulk-spawning sessions right after the 5-hour API window resets triggers aggressive rate limiting. A workflow blocker for users managing multiple concurrent tasks.

**9. [#64202 – Regression: `claude -p` hangs on Termux/Android](https://github.com/anthropics/claude-code/issues/64202)** [0 👍, 5 comments]
Introduced in 2.1.158, `claude -p "hello"` blocks indefinitely waiting for stdin EOF. Previously working in 2.1.157. Platform regression.

**10. [#63896 – Compaction fails: demands 1M context credits](https://github.com/anthropics/claude-code/issues/63896)** [5 👍, 10 comments]
Context compaction errors out with `Usage credits required for 1M context`, forcing users to enable paid credits—even within standard context limits. Feels like an aggressive billing gate to users.

---

## 4. Key PR Progress

The PR queue was light today (9 updated, several trivial/spam). The substantive contributions:

**1. [#64607 – [Docs Fix] Plugin `.mcp.json` example format correction](https://github.com/anthropics/claude-code/pull/64607)**
A clean documentation fix. The `.mcp.json` plugin examples incorrectly used the `mcpServers` wrapper syntax (which belongs in `plugin.json`). The flat format was corrected, preventing MCP configuration errors for plugin developers.

**2. [#63686 – [Policy] Stale/autoclose timeouts: 14 → 90 days](https://github.com/anthropics/claude-code/pull/63686)**
A repo health improvement bumping both stale marking and auto-close durations from 14 to 90 days. This rightly gives more time for community issues to gain traction before being swept.

**3. [#63467 – [Docs] Add Windows `gh` install instructions for `/commit-push-pr`](https://github.com/anthropics/claude-code/pull/63467)**
The troubleshooting section only listed `brew install gh` (macOS). This adds the `winget` equivalent for Windows, closing a documentation parity gap.

**4. [#63872 – [Docs] README capitalization and grammar fixes](https://github.com/anthropics/claude-code/pull/63872)**
Minor polish: standardizing `GitHub`, `macOS`, and improving introductory sentence punctuation.

*Note: No PRs are open yet addressing the Opus 4.7 parsing regression or the Rewind UX, suggesting the team remains in triage or internal development on these high-severity items.*

---

## 5. Feature Request Trends

- **Rich Terminal Editing:** The most upvoted features demand a proper TUI text experience — click-to-position cursor, text selection, standard editing keys ([#27561](https://github.com/anthropics/claude-code/issues/27561), 39 👍) and per-message timestamps for session context ([#2441](https://github.com/anthropics/claude-code/issues/2441), 48 👍).

- **Deeper VCS Integration:** Users want diff comparison against any branch, not just `main` ([#23626](https://github.com/anthropics/claude-code/issues/23626), 47 👍), and awareness of concurrent sessions to prevent silent branch collisions ([#60295](https://github.com/anthropics/claude-code/issues/60295)).

- **Windows Platform Parity:** The top platform feature demand is Computer Use support on Windows ([#64381](https://github.com/anthropics/claude-code/issues/64381)). Combined with the ongoing ARM64 VM issues, Windows users are feeling like second-class citizens.

- **Safer Defaults:** A clear trend from the Rewind backlash: users want destructive actions to require confirmation, and they want configuration to persist across sessions.

---

## 6. Developer Pain Points

**1. Model Stability Crisis (Critical)**
The Opus 4.7 tool call parsing regression is the #1 reliability issue. Sessions fail mid-task, retries fail, and developers lose time and money. The root cause (XML/JSON format mixing on long payloads, [#49747](https://github.com/anthropics/claude-code/issues/49747)) suggests a model-side regression that may require a hotfix or rollback.

**2. Paying for Failures**
API errors (image processing, parse failures, compaction failures) burn through usage credits and 5-hour windows without delivering results ([#60334](https://github.com/anthropics/claude-code/issues/60334), [#64034](https://github.com/anthropics/claude-code/issues/64034)). The billing model punishes users for upstream errors.

**3. Context Management Fragility**
Long-running sessions are breaking in multiple ways: context compaction loses agent state ([#23620](https://github.com/anthropics/claude-code/issues/23620)), compaction fails entirely demanding credits ([#63896](https://github.com/anthropics/claude-code/issues/63896)), and the rewind feature silently destroys uncommitted code ([#64615](https://github.com/anthropics/claude-code/issues/64615)).

**4. Terminal / Cross-Platform Incompatibility**
Claude Code remains fragile outside its primary macOS/Linux x86_64 sweet spot. Users on Windows ARM64 (VMs freezing), Linux via `tmux` (rendering corruption), Android/Termux (stdin hang), and WSL2 (OAuth failures) all face distinct, unresolved issues.

**5. Permission Dialog Jank**
Interactive trust configuration is unreliable: number key selection in permission dialogs fails ~40% of the time ([#64629](https://github.com/anthropics/claude-code/issues/64629)), and MCP authorization flows can deadlock when permission prompts overlap ([#64397](https://github.com/anthropics/claude-code/issues/64397)). This erodes confidence in the agent's safety controls.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-02

## 1. Today's Highlights
The `rust-v0.136.0` release landed with TUI quality-of-life improvements including clickable markdown links and automatic table reformatting, alongside a new session archival feature. Windows users continue to face the brunt of OAuth authentication failures and stability issues, while the demand for a native Linux Desktop app remains the dominant community force. A key security concern surfaced around `ambient_suggestions` accessing Gmail without an explicit user request.

---

## 2. Releases
**rust-v0.136.0** focuses on improving the Terminal UI and session management:  
- Markdown content now renders web links with OSC 8 metadata for cross-terminal clickability (#24472, #24636, #24825)  
- Cramped tables automatically degrade to readable key/value records without losing link targets  
- Sessions can now be archived via the `/archive` TUI command or `codex archive` from the CLI

[View full release](https://github.com/openai/codex/releases/tag/rust-v0.136.0)

---

## 3. Hot Issues

1. **[Issue #11023 — Linux Desktop App](https://github.com/openai/codex/issues/11023)**  
   *73 comments · 389 👍*  
   The single most upvoted open request. Users are frustrated that the Mac app is nearly unusable due to a linked power issue and want native Linux support for their desktop environments.

2. **[Issue #25144 — Disable Long Paste Conversion](https://github.com/openai/codex/issues/25144)**  
   *29 comments · 40 👍*  
   Structured prompts are silently turned into `.txt` attachments when pasted. The community is asking for a simple toggle to disable this behavior.

3. **[Issue #18993 — VS Code Extension History Unreachable](https://github.com/openai/codex/issues/18993)**  
   *28 comments · 48 👍*  
   A regression preventing users from opening past conversation history inside the VS Code extension. Heavily upvoted and impacting daily IDE workflows.

4. **[Issue #25203 / Issue #25157 — Windows OAuth Callback Failures](https://github.com/openai/codex/issues/25203)**  
   *29 + 18 comments · 14 + 16 👍*  
   Multiple reports of GitHub OAuth on Windows failing with "Unable to find Electron app" or opening Electron error dialogs instead of completing the callback. A critical blocker for Windows-based development.

5. **[Issue #22898 — Mobile Shows Desktop Offline](https://github.com/openai/codex/issues/22898)**  
   *11 comments · 35 👍*  
   The Desktop app appears offline in the iOS ChatGPT app, and the Reconnect button does nothing — no loading state, retry, or error feedback. Undermines the remote/paired-device experience.

6. **[Issue #21128 — Project History Culled After 50 Conversations](https://github.com/openai/codex/issues/21128)**  
   *18 comments · 16 👍*  
   The Desktop app silently hides conversations outside the global recent-50 window. Users report this makes the app unreliable as working memory for real projects.

7. **[Issue #18341 — Mac Persistent Blurred Overlay](https://github.com/openai/codex/issues/18341)**  
   *35 comments · 18 👍*  
   A persistent graphical glitch where a blurred/translucent overlay renders below the composer on macOS Darwin. Remains open for over a month.

8. **[Issue #24433 — Ambient Suggestions Opened Gmail Without User Request](https://github.com/openai/codex/issues/24433)**  
   *3 comments*  
   A serious security/privacy report: the Desktop's `ambient_suggestions` workflow used Computer Use to open a real Chrome profile and access Gmail without an explicit user task. Raises questions about sandbox boundaries and audit trails.

9. **[Issue #25715 — WSL Environment Unusably Slow](https://github.com/openai/codex/issues/25715)**  
   *3 comments · 7 👍*  
   Routine agent turns become painfully slow when the WSL2 environment is selected as the agent runtime on Windows. A platform parity concern.

10. **[Issue #25737 — CLI Forces SMS OTP on Security-Key-Only Accounts](https://github.com/openai/codex/issues/25737)**  
    *3 comments · 1 👍*  
    Users with FIDO2/WebAuthn-only accounts pass browser auth with their hardware key only to be redirected to a phone OTP screen in the CLI. Indicates the CLI auth flow doesn't fully respect Advanced Account Security settings.

---

## 4. Key PR Progress

1. **[PR #25731 — v2 Personal Access Token Support](https://github.com/openai/codex/pull/25731)**  
   Adds `codex login --with-access-token` and `CODEX_ACCESS_TOKEN` support, classifying `at-` tokens separately from legacy JWTs and hydrating account metadata through the AuthAPI.

2. **[PR #25638 — `/app` Desktop Handoff Command](https://github.com/openai/codex/pull/25638)**  
   Lets users open their current CLI thread directly in Codex Desktop via `/app`, matching the existing `codex app <path>` entry point.

3. **[PR #25739 — Permission Profile Inheritance Fix](https://github.com/openai/codex/pull/25739)**  
   Fixes profile inheritance so that extending `:workspace` properly merges parent defaults before applying child overrides, rather than seeding from an empty policy.

4. **[PR #25738 — Code Review Rules into AGENTS.md](https://github.com/openai/codex/pull/25738)**  
   Moves repository-specific review rules into `AGENTS.md`, making review guidance available alongside the code while keeping local review skills intact.

5. **[PR #25147 — Streamable HTTP Retry Logic](https://github.com/openai/codex/pull/25147)**  
   Retries transient streamable HTTP failures during RMCP startup and the read-only `tools/list` operation — a resilience improvement for MCP connections.

6. **[PR #24812 — Enterprise Credit Limits in `/status`](https://github.com/openai/codex/pull/24812)**  
   Adds the `spend_control.individual_limit` field to the rate-limit snapshot, giving enterprise users visibility into their monthly credit limits.

7. **[PR #25736 — App-Bundled Internal Plugin Hooks](https://github.com/openai/codex/pull/25736)**  
   Allows first-party desktop plugins to ship automatically enabled hooks without appearing in user-facing settings, while failing closed on tampered caches.

8. **[PR #15730 — Symlink Hardening](https://github.com/openai/codex/pull/15730)**  
   Rejects symlinked `--output-last-message` paths and project config files before parsing, preventing symlink-based sandbox escapes.

9. **[PR #25675 — Remote Control Pairing RPC](https://github.com/openai/codex/pull/25675)**  
   Exposes a narrow pairing RPC for remote control enrollment, allowing clients to mint short-lived controller artifacts without exposing the backend `serverId`.

10. **[PR #25707 — `CodexErr` Analytics](https://github.com/openai/codex/pull/25707)**  
    Adds rich error telemetry to `codex_turn_event`, emitting granular `codex_error_*` fields for downstream analytics without altering existing error paths.

---

## 5. Feature Request Trends

- **Linux Desktop App:** The consistently highest-voted open request (#11023) remains a dominant signal. Users are calling for native Linux support to escape Mac power issues and bring Codex to their primary development machines.
- **Input Handling UX Control:** There is a strong desire for explicit user control over how input is preprocessed. The request to disable automatic long-paste-to-attachment conversion (#25144) reflects broader demand for the app to stay out of the way of structured data.
- **Session History & Project Continuity:** The recent-50 conversation limit (#21128) is a recurring friction point. Users want project-scoped history persistence, robust search, and better archival (the new `/archive` feature directly addresses this).
- **Enterprise Observability:** Enterprise subscribers are pushing for better visibility into usage and budget data (#24812), signaling growing adoption in organizational settings.
- **Proactive Agent Transparency:** After the Gmail access incident (#24433), there is mounting interest in stricter permission boundaries, audit logs, and opt-in mechanisms for ambient/proactive agent behaviors like `ambient_suggestions`.

---

## 6. Developer Pain Points

- **Windows Platform Instability:** This is the most acute pain point. OAuth callbacks fail (#25203, #25157), WSL performance is crippling (#25715), Computer Use sandbox fails to bootstrap (#25391), and the app crashes on clean reinstall (#25489, #25501). Windows users face a fragmented, unreliable experience.
- **Authentication Fragility:** From phone verification loops (#20320) to FIDO2-incompatible CLI flows (#25737), the authentication pathway remains brittle for power users and those with strict security requirements.
- **Workflow Breaks Due to Data Access:** The inability to open past conversations in the VS Code extension (#18993) and the silent culling of project history in the Desktop app (#21128) directly break developer continuity and trust.
- **Sandbox and Permission Inconsistencies:** Environments silently change context (#24638), Full Access threads get downgraded mid-continuation (#24300), and agent autonomy slips past user intent (#24433). Developers are struggling to build confidence in the sandbox's predictability for long-running tasks.
- **Mobile/Desktop Integration Gaps:** The offline-Desktop illusion in the iOS app (#22898) and stale connection state undermine the promise of a seamless remote-enhanced development workflow.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-02

---

## 1. Today’s Highlights

Agent reliability dominates the discussion today, with highly upvoted bugs around generalist agent hangs and sub-agents masking `MAX_TURNS` failures drawing continued community attention. On the development side, a new nightly release kicks off the transition to a Flash GA model behind an experiment flag, while significant closed PRs from the past 24 hours show major feature landings—including a native Notebook Editor tool, a `/model` slash command, and a `ripgrep` port—that had been in review for some time.

## 2. Releases

**v0.45.0-nightly.20260602.g665228e98** was released today.

**What’s Changed:**
- Transition to Flash GA model when experiment flag is present.
  — [@DavidAPierce in PR #27570](https://github.com/google-gemini/gemini-cli/pull/27570)

Full Changelog: [v0.45.0-nightly.20260530...v0.45.0-nightly.20260602](https://github.com/google-gemini/gemini-cli/compare/v0.45.0-nightly.20260530.g013914071...v0.45.0-nightly.20260602.g66522)

---

## 3. Hot Issues

### 1. [#24353 — Robust Component Level Evaluations (P1, EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)
Tracks the expansion of behavioral eval tests beyond the initial 76. This is the internal quality foundation that underpins every agent feature shipping today. Active triage continues.
> *7 comments | Updated today*

### 2. [#21409 — Generalist Agent Hangs (P1, Bug)](https://github.com/google-gemini/gemini-cli/issues/21409)
**Community Top Pain Point (8 👍).** Users report the CLI hangs indefinitely when the generalist agent is invoked for simple tasks (folder creation). Workaround: explicitly instruct the model to avoid sub-agent delegation.
> *7 comments | Updated today*

### 3. [#22323 — Subagent Recovery After MAX_TURNS Reported as SUCCESS (P1, Bug)](https://github.com/google-gemini/gemini-cli/issues/22323)
The `codebase_investigator` sub-agent reports `status: "success"` even when it hits `MAX_TURNS` and performed no real analysis. This is a critical trust/reporting bug in the agent loop.
> *6 comments | Updated today*

### 4. [#25166 — Shell Command Execution Gets Stuck on “Waiting input” (P1, Bug)](https://github.com/google-gemini/gemini-cli/issues/25166)
Simple shell commands (even those that never ask for stdin) leave the CLI in a stuck “awaiting user input” state. High impact on daily script execution workflows.
> *4 comments (3 👍) | Updated today*

### 5. [#21983 — Browser Subagent Fails in Wayland (P1, Bug)](https://github.com/google-gemini/gemini-cli/issues/21983)
Termination Reason: `GOAL` is reported, but the browser agent fails silently on Wayland compositors. Blocks browser-automation use cases on modern Linux.
> *4 comments (1 👍) | Updated today*

### 6. [#26525 — Add Deterministic Redaction and Reduce Auto Memory Logging (P2, Security)](https://github.com/google-gemini/gemini-cli/issues/26525)
Auto Memory sends local transcripts to models; secrets are redacted only *after* hitting model context, and skills can be logged. This is a high-sensitivity privacy/security hardening item.
> *3 comments | Updated today*

### 7. [#26522 — Stop Auto Memory from Retrying Low-Signal Sessions Indefinitely (P2, Bug)](https://github.com/google-gemini/gemini-cli/issues/26522)
The extraction agent skips low-signal transcripts but never marks them as processed, causing infinite retries. A resource-waste bug that also clogs the inbox.
> *3 comments | Updated today*

### 8. [#21968 — Gemini Does Not Use Skills and Sub-Agents Enough (P2, Bug)](https://github.com/google-gemini/gemini-cli/issues/21968)
Users have configured custom skills (Gradle, Git) with explicit descriptions, but the model ignores them unless instructed directly. Points to a systemic invocation heuristic gap.
> *6 comments | Updated today*

### 9. [#22672 — Agent Should Stop/Discourage Destructive Behavior (P2, Customer Issue)](https://github.com/google-gemini/gemini-cli/issues/22672)
The model readily uses `git reset`, `--force`, and aggressive resource management commands. Community requesting built-in safe-guards/safety prompting for risky operations.
> *2 comments (1 👍) | Updated today*

### 10. [#22745 — Assess Impact of AST-Aware File Reads, Search, and Mapping (P2, EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)
An EPIC tracking whether AST-grounded tools can reduce token noise and align reads more precisely. Spawning three sub-tasks (#22746, #22747). Extremely high potential for improving context efficiency.
> *7 comments (1 👍) | Updated today*

---

## 4. Key PR Progress

### 1. [#8943 — Notebook Tool Implementation (Size: XL)](https://github.com/google-gemini/gemini-cli/pull/8943)
**Closed.** Adds a built-in `NotebookEditTool` for safe `.ipynb` editing—add, edit, delete, move cells, and clear outputs without JSON corruption. Resolves [#6930](https://github.com/google-gemini/gemini-cli/issues/6930). Major UX win for data science users.

### 2. [#8938 — Message Bus Integration for Tool Confirmation (Size: L)](https://github.com/google-gemini/gemini-cli/pull/8938)
**Closed.** Introduces the `enableMessageBusIntegration` flag, allowing external confirmation of tool calls via a message bus. Architectural groundwork for more complex approval workflows.

### 3. [#8940 — Add `/model` Command for Interactive Model Selection (Size: L)](https://github.com/google-gemini/gemini-cli/pull/8940)
**Closed.** Adds a full-screen slash command dialog for switching between Auto, Pro, Flash, and Flash-Lite models mid-session without restarting the CLI.

### 4. [#8935 / #8933 — Reapply "Port `get-ripgrep`" (Size: L)](https://github.com/google-gemini/gemini-cli/pull/8935)
**Closed.** Reverts a previous revert and brings native ripgrep into the CLI toolchain, enabling extremely fast local file search directly from agent tools.

### 5. [#8964 — Releasing: Version Management (Size: L)](https://github.com/google-gemini/gemini-cli/pull/8964)
**Closed.** Enhances the release pipeline with semantic-versioning rollback detection and conflict management across release channels. CI infrastructure hardening.

### 6. [#9003 — Fix tools executing silently without model response (Size: S)](https://github.com/google-gemini/gemini-cli/pull/9003)
**Closed.** Fixes a silent failure mode where tools (e.g., ReadManyFiles) execute but the model never generates a follow-up response, leaving the CLI hanging with no feedback.

### 7. [#8986 — Fix `useSlashCompletion` Flickering During `@` Completions (Size: M)](https://github.com/google-gemini/gemini-cli/pull/8986)
**Closed.** Resolves UI flickering introduced by fuzzy matching. The `useSlashCompletion` effect was interfering with `useAtCompletion`'s anti-flicker mechanism.

### 8. [#8934 — Security: Pin `wrap-ansi` to 9.0.2 (Size: M)](https://github.com/google-gemini/gemini-cli/pull/8934)
**Closed.** Proactive supply chain security. Forces an update away from the compromised `9.0.1` release to `9.0.2`.

### 9. [#8929 — feat(ci): Add a "Verify Release" Action (Size: M)](https://github.com/google-gemini/gemini-cli/pull/8929)
**Closed.** Adds a release pipeline step that pulls the published npm package and verifies the binary returns the expected version. Baseline for future release validation.

### 10. [#8930 — Fix(metrics): Add Exit Hook for Optl SDK Cleanup (Size: XS)](https://github.com/google-gemini/gemini-cli/pull/8930)
**Closed.** Ensures the OpenTelemetry SDK properly cleans up and flushes metrics on process exit, preventing data loss and zombie processes.

---

## 5. Feature Request Trends

- **AST-Grounded Tools:** A strong, multi-issue push (#22745, #22746, #22747) toward AST-aware reading, searching, and codebase mapping. The goal is fewer inference turns, smaller context, and more precise edits for large repos.
- **Agent Self-Awareness & Safety:** Users want models that understand their own configuration flags, hotkeys, and destructive potential (#21432, #22672). This includes respecting `settings.json` overrides reliably (#22267).
- **Memory and Context Maturation:** Auto Memory is under active rework for determinism, security redaction, and avoidance of infinite retries (#26525, #26522, #26523). Expect a more robust memory pipeline soon.
- **Remote Agent Infrastructure:** The Remote Agents EPIC (#20303) is advancing with task-level auth and background operation support, pointing to a server-side agent architecture.
- **Evaluation Driven Development:** Multiple issues (#24353, #23166, #23313) show the team is investing heavily in behavioral and steering evals to prevent regressions.

---

## 6. Developer Pain Points

- **Agent Loop Unreliability:** The top theme. The generalist agent hangs (#21409), sub-agents lie about success (#22323), and the shell executor deadlocks on basic commands (#25166). This erodes trust in autonomous mode.
- **Configuration & Customization Ignored:** Users are frustrated that custom skills are ignored (#21968) and that `settings.json` overrides are silently dropped (#22267). The regression where sub-agents ran with `agents: disabled` (#22093) was a notable violation of user intent.
- **Context / Tool Scaling Limits:** The model throws a 400 error when more than 128 tools are available (#24246). For power users building large custom toolkits, this is a hard wall.
- **UI and Terminal Hygiene:** Lingering issues with terminal resize performance (#21924), screen corruption after external editors (#24935), and `\n` escape mangling (#22466) degrade the interactive experience.
- **Memory Pipeline Inefficiency:** The background extraction agent retries low-signal sessions forever (#26522), silently drops invalid patches (#26523), and logs sensitive content before redaction (#26525). This consumes user API quota and trust.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for June 2, 2026.

---

## GitHub Copilot CLI Community Digest – 2026-06-02

### 1. Today’s Highlights
- **v1.0.57** shipped yesterday with better error messages for rate limits and live feedback for plugin commands, though a wave of clipboard and input bugs from the prior v1.0.56 release is drawing significant community attention.
- MCP server governance is a hot topic: users are running into false policy blocks and requesting granular permissions, signaling that the plugin/MCP ecosystem is actively being put through its paces in production.
- The most-upvoted open issue (53 👍) highlights a persistent model-parity gap between Copilot CLI and VS Code, with Gemini 3.1 Pro notably missing from the CLI model list.

---

### 2. Releases
Two versions landed in the last 24 hours:

- **v1.0.57** – Actionable error messages now shown when `copilot update` hits the GitHub API rate limit. Plugin slash commands (`/plugin install`, `/plugin marketplace`, etc.) display immediate progress feedback. Added the ability to cancel a running shell command.
- **v1.0.57-5** – Minor fixes and stability improvements.

---

### 3. Hot Issues (10 Noteworthy)

| Issue | Why It Matters | Community Signal |
|---|---|---|
| [#1703 – Model list missing Gemini 3.1 Pro](https://github.com/github/copilot-cli/issues/1703) | Org-enabled models available in VS Code are invisible in CLI. Breaks parity. | 53 👍, 27 comments. Highest engagement. |
| [#1707 – 3rd-party MCP servers falsely blocked](https://github.com/github/copilot-cli/issues/1707) | Policy error shown even when org policy explicitly allows them. Downgrade needed to unblock. | 8 comments, closed as regression in 0.0.418. |
| [#768 – Option to disable MCP servers by default](https://github.com/github/copilot-cli/issues/768) | Users want to save tokens by keeping MCP servers off until explicitly needed. | 36 👍, 6 comments. Strong demand for token efficiency. |
| [#3609 / #3622 – Copy to clipboard silently fails](https://github.com/github/copilot-cli/issues/3609) | "Copied to clipboard" message shown but clipboard unchanged. Regression in v1.0.56. | Two reports from different platforms in 24h. High urgency. |
| [#2060 – Exec format error on aarch64 Linux](https://github.com/github/copilot-cli/issues/2060) | The installer fetches an ARM64 binary that cannot execute on Oracle/RHEL ARM systems. | 3 comments, no workaround yet. |
| [#3028 – MCP Permissions system](https://github.com/github/copilot-cli/issues/3028) | No way to restrict which MCP tools the model can invoke. | 5 comments, 4 👍. Privacy/control concern. |
| [#3623 – Context loss with Claude Sonnet 4.6](https://github.com/github/copilot-cli/issues/3623) | Model forgets instructions after just a few exchanges in a session. | Newly filed (June 1). Core memory stability issue. |
| [#3596 – Auth error on session resume](https://github.com/github/copilot-cli/issues/3596) | `/model` fails with "Not authenticated" when resuming a specific session. | Breaks long-running workflows. |
| [#3621 – Auto-compaction loops on large instruction files](https://github.com/github/copilot-cli/issues/3621) | Large `.copilot-instructions.md` files cause infinite compaction, wiping memory every turn. | New. Blocks multi-step tasks for teams with rich docs. |
| [#3619 – Bash tool incompatible with fish shell](https://github.com/github/copilot-cli/issues/3619) | Exit-code sentinel uses `$?` syntax, which fish does not support. | Ecosystem compatibility gap. |

---

### 4. Key PR Progress
PR activity was minimal over the last 24 hours, with only 1 item recorded.

- **[#3473 (OPEN)](https://github.com/github/copilot-cli/pull/3473)** – Appears to be spam/phishing content unrelated to the codebase.
- **Analysis:** The lack of substantial PRs likely reflects a period of internal stabilization and team focus following the `v1.0.57` drop. The surge in newly filed clipboard, shell-compatibility, and memory bugs suggests the next wave of fixes is being triaged.

---

### 5. Feature Request Trends
Three major directional themes are emerging from the issue tracker:

- **MCM / Plugin Governance Maturity** – The bulk of feature requests center on controlling MCP behavior: granular permissions per-tool ([#3028](https://github.com/github/copilot-cli/issues/3028)), toggling servers on/off to manage token spend ([#768](https://github.com/github/copilot-cli/issues/768)), and support for generic local inference endpoints (BYOM) beyond Anthropic ([#3624](https://github.com/github/copilot-cli/issues/3624)).
- **Smarter Session & Context Management** – Users want natural-language session lookup (`--resume "<query>"` – [#3615](https://github.com/github/copilot-cli/issues/3615)), shorthand flags for common operations ([#1914](https://github.com/github/copilot-cli/issues/1914)), and the ability to hide intermediate tool-call noise during streaming ([#3614](https://github.com/github/copilot-cli/issues/3614)).
- **Plugin Ecosystem UX** – With over 10+ custom skills being common, developers are requesting organizational features like subfolder support for the skills directory ([#1632](https://github.com/github/copilot-cli/issues/1632)) and better path handling on Windows ([#1547](https://github.com/github/copilot-cli/issues/1547)).

---

### 6. Developer Pain Points

1. **Clipboard & Input Handling Regressions** – The silent clipboard failure in v1.0.56 ([#3609](https://github.com/github/copilot-cli/issues/3609), [#3622](https://github.com/github/copilot-cli/issues/3622)) and the overloaded `Ctrl+C` behavior ([#3620](https://github.com/github/copilot-cli/issues/3620)) are breaking the fundamental terminal feedback loop for power users.

2. **Memory & Context Stability** – The auto-compaction loop triggered by large instruction files ([#3621](https://github.com/github/copilot-cli/issues/3621)) and rapid context loss with specific models ([#3623](https://github.com/github/copilot-cli/issues/3623)) are creating hard ceilings for complex, multi-step agent tasks.

3. **Cross-Environment Fragility** – Recurring issues with architecture mismatches (aarch64 [#2060](https://github.com/github/copilot-cli/issues/2060)), locale stripping (LC_CTYPE [#3601](https://github.com/github/copilot-cli/issues/3601)), and non-bash shell syntax (fish [#3619](https://github.com/github/copilot-cli/issues/3619)) suggest hardening across diverse dev environments is still maturing.

4. **Authentication & Session Flakiness** – Resuming sessions can silently break authentication ([#3596](https://github.com/github/copilot-cli/issues/3596)), and meta-repo workspace shapes trigger remote control regressions ([#3457](https://github.com/github/copilot-cli/issues/3457)), which undermines reliability for users who rely on persistent agent sessions.

5. **Model Parity with VS Code** – Repeated reports of the CLI showing a reduced model list compared to VS Code on the same account ([#1703](https://github.com/github/copilot-cli/issues/1703)) erodes trust and forces users to context-switch to VS Code to access preferred models.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI Community Digest — 2026-06-02

### Today’s Highlights

No new releases landed today. Two freshly filed issues highlight friction around terminal display quality (#2417) and third-party agent API access (#2416). On the pull request side, a critical authentication fix (#2414) that adds rollback logic for OAuth config validation was opened, alongside a long-standing `/copy` command feature (#1741).

---

### Releases

No new releases in the last 24 hours. The latest available version remains **v1.46.0**.

---

### Hot Issues (3 active today)

**#2417 — [Bug] Text wrapping cuts words mid-word when exceeding line length**
- *Author: ysntony | Model: Kimi-k2.6 | Platform: Darwin*
- Text in the terminal is being split at non-word boundaries, severely degrading readability of long outputs and code blocks. No community discussion yet (0 comments), but this is a high-touch UX regression that will likely draw quick attention.
- [MoonshotAI/kimi-cli Issue #2417](https://github.com/MoonshotAI/kimi-cli/issues/2417)

**#2416 — [Enhancement] Add Zoo Code to the third-party coding agent API whitelist**
- *Author: zimmshane*
- Zoo Code, the active community successor to Roo Code, is currently receiving a `403` error from the Kimi Code API. Since Roo Code was previously whitelisted, this reveals a maintenance gap in the third-party agent compatibility list.
- [MoonshotAI/kimi-cli Issue #2416](https://github.com/MoonshotAI/kimi-cli/issues/2416)

**#1914 — [Bug] Installation fails in regions where GitHub is unreachable [CLOSED]**
- *Author: warku123*
- Users in network-restricted environments could not install the CLI because the `uv` installer pulled dependencies directly from GitHub Releases. Now resolved, reflecting a successful effort to fix a fundamental distribution bottleneck.
- [MoonshotAI/kimi-cli Issue #1914](https://github.com/MoonshotAI/kimi-cli/issues/1914)

---

### Key PR Progress (4 active today)

**#1741 — feat: add `/copy` command for latest assistant response [OPEN]**
- Adds a shell-level `/copy` slash command to copy the most recent assistant response to the system clipboard. A straightforward quality-of-life improvement for terminal-heavy workflows.
- [MoonshotAI/kimi-cli PR #1741](https://github.com/MoonshotAI/kimi-cli/pull/1741)

**#2414 — fix(auth): avoid persisting OAuth token before config validation [OPEN]**
- Prevents OAuth credentials from being saved until the model list and default model are fully validated. Includes a rollback mechanism if config saving fails, protecting users from corrupted auth state.
- [MoonshotAI/kimi-cli PR #2414](https://github.com/MoonshotAI/kimi-cli/pull/2414)

**#2386 — fix(session): map undo wire turns to context turns [OPEN]**
- Resolves a bug where `/undo` and fork operations failed on local slash-command turns because they incorrectly referenced wire-log indices instead of context-log indices.
- [MoonshotAI/kimi-cli PR #2386](https://github.com/MoonshotAI/kimi-cli/pull/2386)

**#2389 — fix(tools): include trailing output in error briefs and render brief as plain text [CLOSED]**
- Improves error messaging from shell tool failures by capturing trailing stdout/stderr in the error brief and rendering it as plain text. Merged.
- [MoonshotAI/kimi-cli PR #2389](https://github.com/MoonshotAI/kimi-cli/pull/2389)

---

### Feature Request Trends

The dominant feature signal is **third-party coding agent interoperability**. The request to whitelist Zoo Code (Issue #2416) underscores that the community expects Kimi Code API to seamlessly integrate with actively maintained open-source agent forks. Separately, the long-dormant `/copy` feature (PR #1741) continues to represent a demand for better **terminal session ergonomics**, allowing users to extract outputs without external clipboard utilities.

---

### Developer Pain Points

- **Geographical Distribution Barriers:** Issue #1914 highlights a critical availability gap—relying exclusively on GitHub Releases for installation locks out developers in restricted regions.
- **Terminal UI Quality:** The mid-word wrapping bug (#2417) exposes a lack of polish in the basic text rendering pipeline, directly impacting daily read-ability of the tool’s output.
- **Configuration Brittleness:** The careful OAuth rollback logic introduced in PR #2414 implies that state corruption during authentication or config file operations is a recognized and painful failure mode for users.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode Community Digest — 2026-06-02

### 1. Today's Highlights
The v1.15.13 Desktop update introduced a severe UX regression where the MCP panel shows "No MCPs configured" while the CLI backend works perfectly, prompting several targeted fixes. The announcement of a permanent 75% reduction in DeepSeek V4 Pro pricing has also ignited a high-engagement discussion around adjusting OpenCode Go subscription limits. On the core development front, a substantial rewrite of the permission system (`PermissionV2`) and account service refactor are moving through the pipeline, signaling a push toward more reliable configuration and broader extensibility.

### 2. Releases
No releases in the last 24 hours.

### 3. Hot Issues
*(10 noteworthy issues, linked and contextualized)*

1. **[#28846 – Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)** (43 comments, 61 👍)  
   *Community Reaction:* The highest engagement of the day. Users are demanding subscription quotas be dynamically adjusted to reflect real-time upstream API cost changes.  
   *Why it matters:* Pricing parity is a core UX concern; ignoring such a dramatic shift erodes trust in the value of the Go plan.

2. **[#16331 – Permissions ignored](https://github.com/anomalyco/opencode/issues/16331)** (40 comments, 8 👍)  
   *Community Reaction:* A classic pain point that refuses to die. Explicit `deny` rules (e.g., `*.env`) are routinely bypassed.  
   *Why it matters:* This is a security issue, not just a convenience bug. It undermines the entire sandboxing promise of the permission model.

3. **[#27589 – TUI fails on Alpine Linux (musl): getcontext symbol not found](https://github.com/anomalyco/opencode/issues/27589)** (24 comments, 12 👍)  
   *Community Reaction:* A clean regression from v1.14.48 to v1.14.50. Linux users on musl-based distros are completely blocked from using the TUI.  
   *Why it matters:* Blocks a non-trivial slice of the Linux user base, raising concerns about the TUI's portability.

4. **[#1990 – [Feature Request] User Controls for Context Management](https://github.com/anomalyco/opencode/issues/1990)** (19 comments, 37 👍)  
   *Community Reaction:* Continues to receive strong support as the community's top UX feature request.  
   *Why it matters:* Directly addresses the tension between "AI pair programming" (need small context) and open-ended chat (need large context).

5. **[#8832 – opencode not respecting permissions](https://github.com/anomalyco/opencode/issues/8832)** (15 comments, 7 👍)  
   *Community Reaction:* Another instance of the permission checker failing, specifically around `bash` commands like `find` and `grep`.  
   *Why it matters:* Shows the problem is systemic, not limited to file-read patterns.

6. **[#11529 – Kimi K2.5 via NanoGPT: tool loops, reasoning bugs](https://github.com/anomalyco/opencode/issues/11529)** (8 comments, 7 👍)  
   *Community Reaction:* Users trying latest frontier models (Kimi K2.5, DeepSeek 3.2) hit immediate roadblocks with tool calling and reasoning parsing.  
   *Why it matters:* Frontier-model adoption is a key driver of OpenCode growth; rough edges here drive users away.

7. **[#30104 – Desktop app MCP tab shows 'No MCPs configured' (CLI works fine)](https://github.com/anomalyco/opencode/issues/30104)** (8 comments, 9 👍)  
   *Community Reaction:* The flagship bug of the v1.15.13 release. Multiple duplicates exist (#30070, #30265, #30130, etc.).  
   *Why it matters:* Makes the Desktop app effectively unusable for MCP management, forcing CLI fallback.

8. **[#29992 – Auto-scroll stops working after manually scrolling and returning to bottom](https://github.com/anomalyco/opencode/issues/29992)** (8 comments, 12 👍)  
   *Community Reaction:* A simple but maddening UX regression during streaming responses.  
   *Why it matters:* Breaks the core reading experience during generation.

9. **[#30306 – gpt-5.3-codex model is not supported when using Codex with a ChatGPT account](https://github.com/anomalyco/opencode/issues/30306)** (7 comments)  
   *Community Reaction:* Sudden breakage for Codex plugin users. Emergency workaround/quick fix was provided (see #30316).  
   *Why it matters:* Highlights the fragility of depending on specific upstream model IDs that can be sunsetted without warning.

10. **[#30126 – High CPU and Memory usage on macOS ARM64](https://github.com/anomalyco/opencode/issues/30126)** (3 comments)  
    *Community Reaction:* New report. OpenCode consumes 100% CPU and ~2.5GB RAM on Apple Silicon.  
    *Why it matters:* Performance regressions on the primary developer platform (macOS) are a high-priority concern.

### 4. Key PR Progress
*(10 important PRs shaping the codebase)*

1. **[#30316 – Remove sunsetted gpt-5.2 and gpt-5.3-codex](https://github.com/anomalyco/opencode/pull/30316)**  
   *Impact:* Emergency fix for Codex users. Removes models from the allowed list to align with upstream API availability. Closes #30306.

2. **[#30220 – Restore deferred MCP status updates](https://github.com/anomalyco/opencode/pull/30220)**  
   *Impact:* Directly targets the v1.15.13 Desktop MCP blank-state regression. Fixes a Solid Query destructuring bug where lazily enabled MCP queries lost their state.

3. **[#30085 – Grant MCP tool permissions in subagent sessions](https://github.com/anomalyco/opencode/pull/30085)**  
   *Impact:* Closes #16491. Subagents spawned via the Task tool can now actually *execute* MCP tools instead of just seeing them in the registry. A major workflow unlock.

4. **[#30287 – Add location-based permission service (PermissionV2)](https://github.com/anomalyco/opencode/pull/30287)**  
   *Impact:* A core architecture revamp. Introduces a schema-driven, location-scoped permission model with normalized project grants. Replaces the legacy ad-hoc system. Aims to solve the systemic reliability issues highlighted by #16331 and #8832.

5. **[#30309 – Refactor core: migrate accounts and load file agents](https://github.com/anomalyco/opencode/pull/30309)**  
   *Impact:* Big internal cleanup. Moves account/OAuth logic into `@opencode-ai/core` and enables loading agents from Markdown files (`{agent,agents}/**/*.md`), paving the way for a more extensible agent system.

6. **[#5020 – Add layout system for TUI](https://github.com/anomalyco/opencode/pull/5020)** (CLOSED)  
   *Impact:* Addresses several accessibility and customization tickets (#2750, #1107, #3547). Introduces an extensible layout system to create more vertical space and improve UI customization in the TUI.

7. **[#30300 – Preserve live parts during TUI session hydration](https://github.com/anomalyco/opencode/pull/30300)**  
   *Impact:* Fixes a race condition where live streaming messages were overwritten by older HTTP snapshot data during initial TUI session load.

8. **[#29977 – Include git store hash in project ID](https://github.com/anomalyco/opencode/pull/29977)**  
   *Impact:* Resolves a confusing bug where independent clones of the same repository shared a project ID, causing state merging and data loss.

9. **[#30314 – Avoid suspending on pending child path](https://github.com/anomalyco/opencode/pull/30314)**  
   *Impact:* Fixes a Solid Query suspension bug that caused UI freezes, improving overall app stability (follow-up to #30167 and #30220).

10. **[#26090 – Expose LLM response headers on assistant messages](https://github.com/anomalyco/opencode/pull/26090)**  
    *Impact:* Enhances debugging and transparency by surfacing upstream provider response headers (e.g., `x-litellm-model`). Critical for users routing through proxies.

### 5. Feature Request Trends
Trends distilled from the day's activity:

1. **Pricing API & Quota Agility (#28846):** The community expects subscription quotas to be dynamically linked to real-time upstream API pricing. A permanent price cut of 75% is seen as a trigger for immediately adjusting Go plan limits.
2. **Permission System Maturity (#16331, #8832, #27436, PR #30287):** The sheer volume of "Permission ignored" bugs is driving the core team to build a completely new permission service. The community is demanding a predictable, secure, and auditable sandbox.
3. **Extensibility & Debugging (#30307, #26090, #30303, #30317):** Users want to build custom controllers (reflection hooks), inspect internal state (session dumps, LLM headers), and integrate deeply with their shell.
4. **Context Control (#1990):** Powerful, evergreen demand for manual context window management to balance cost, latency, and reliability in extended sessions.

### 6. Developer Pain Points
Recurring frustrations and high-frequency requests observed in the data:

- **v1.15.13 Desktop MCP UI Regression:** The most acute pain point. The MCP panel is broken out of the box for Desktop users, forcing a CLI dependency for a core feature. Multiple duplicate issues and hotfix PRs highlight the disruption.
- **Permission System Unreliability:** The number one source of long-term friction. Configuration is routinely ignored, UI permission dialogs get stuck in infinite loops, and subagent permission inheritance is broken. This directly impacts trust in the tool's security model.
- **TUI Stability on Linux:** From `getcontext` errors on musl to full terminal session crashes, the TUI experience on Linux remains fragile and a recurring source of blocking regressions.
- **Frontier Model Integration Friction:** Adopting new models (Kimi K2.5/2.6, DeepSeek 3.2) is a gamble. Users frequently encounter tool call failures, reasoning text parsing errors, and sudden model sunsetting (GPT-5.3-codex), creating a poor experience for early adopters.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-02

**Data Source:** `github.com/earendil-works/pi`

---

## 1. Today's Highlights

The community reacted swiftly to the **MiniMax M3** release, with multiple feature requests and a provider update landing within hours. On the stability front, significant patches were merged to address **local model tool-call validation errors** and **TUI rendering regressions** (Kitty images in WezTerm, CJK IME support, and screen flickering). A critical root-cause analysis of silent provider stream hangs also generated strong discussion, pointing toward a much-needed reliability overhaul.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

### 1. [#5089] `timeoutMs` not respected for slow operations
**URL:** `earendil-works/pi` Issue #5089  
**Why it matters:** With 22 comments, this is the highest-engagement bug this week. Users running large local models (Qwen 3.6 27B) on CPU or underpowered hardware find that the `timeoutMs` setting is ignored past a certain threshold, causing forced disconnections. Community reaction is highly frustrated.

### 2. [#5291] Sessions hang on "Working..." with Anthropic subscription
**URL:** `earendil-works/pi` Issue #5291  
**Why it matters:** An Enterprise Anthropic subscriber reports that sessions freeze on "Working..." simultaneously. Requires manual "Interrupt / stop and resume" cycles. This represents a top-tier reliability concern for paying users of managed providers.

### 3. [#5294] Llama.cpp backend timeout despite `http timeout = false`
**URL:** `earendil-works/pi` Issue #5294  
**Why it matters:** Directly related to #5089 but specifically scoped to the popular `llama.cpp` backend. The user disabled HTTP timeouts via `/settings` but still receives timeouts on slow models, suggesting a secondary or hardcoded timeout layer.

### 4. [#5229] MiniMax on OpenRouter broken (`developer` role)
**URL:** `earendil-works/pi` Issue #5229  
**Why it matters:** Coincides with the M3 release hype. Pi sends a `developer` role message which OpenRouter's MiniMax schema does not accept, causing a `400` error. Immediate blocker for anyone trying MiniMax models on the OpenRouter provider.

### 5. [#5293] Page auto-scrolls to first message on edit task
**URL:** `earendil-works/pi` Issue #5293  
**Why it matters:** A jarring UX regression. Triggering an edit task on a message re-executes "soft selection" from the very first message in the chat history, causing unexpected and highly disruptive scrolling in long sessions.

### 6. [#4877] Session folder collision
**URL:** `earendil-works/pi` Issue #4877  
**Why it matters:** An architectural technical debt bug. The session hashing logic uses path flattening (`--a-b-c-d--`) that can collide for different paths (e.g., `/a/b/c/d` vs `/a-b/c-d`). Well-documented and could surprise users with data leakage.

### 7. [#5290] Silent hang on provider stream errors
**URL:** `earendil-works/pi` Issue #5290  
**Why it matters:** A root-cause deep dive shows `forwardStream()` in `register-builtins.ts` lacks error handling around its `for await` loop. If the provider stream throws, `target.end()` is never called and the rejection is silently swallowed. This is likely a root cause for many mysterious "hang" states.

### 8. [#5311] Screen flicker when extension dialog appears during streaming
**URL:** `earendil-works/pi` Issue #5311  
**Why it matters:** `ctx.ui.confirm()` and `ctx.ui.select()` replace the entire editor element in the TUI, causing visible flickering. This is especially pronounced when the agent is actively streaming output, making the TUI feel unstable.

### 9. [#5271] / [#5272] MiniMax M3 Support requests
**URL:** `earendil-works/pi` Issue #5271  
**Why it matters:** High community demand for the newly released MiniMax M3, which boasts 1M-context MSA and Native Multimodality. Two users filed requests within hours of release. (Addressed in PR #5284).

### 10. [#5307] Local models produce invalid tool call args
**URL:** `earendil-works/pi` Issue #5307  
**Why it matters:** An excellent forensic analysis of why local models like Qwen3.6-35B fail tool calls. Two root causes identified: YAML frontmatter leakage into tool arguments, and malformed JSON from the model. Directly explains the high failure rate of `edit` tool calls in local-only setups.

---

## 4. Key PR Progress

### 1. [#5308] `fix: sanitize local model artifacts in tool prepareArguments`
**URL:** `earendil-works/pi` PR #5308  
**Why it matters:** High impact. Directly addresses the pain of local model validation failures. Strips YAML frontmatter and repairs malformed JSON before TypeBox validation, dramatically improving local model reliability for structured tool calls.

### 2. [#5296] `fix(tui): keep Kitty images visible in WezTerm`
**URL:** `earendil-works/pi` PR #5296  
**Why it matters:** Fixes a bad regression where inline images rendered as empty reserved blocks in WezTerm. Uses targeted `C=1` placement logic instead of the global revert attempted in #5233, preserving the fix for tall images from #4461.

### 3. [#5284] `feat(ai): add MiniMax-M3 to minimax and minimax-cn`
**URL:** `earendil-works/pi` PR #5284  
**Why it matters:** Fast turnaround on a feature request. Adds the model with full specs: 512K context, 128K max output, native multimodal input, and reasoning support. Covers both overseas and China endpoints.

### 4. [#5295] `fix(tui): overlay CJK before-segment strict wide-char boundary`
**URL:** `earendil-works/pi` PR #5295  
**Why it matters:** Prevents TUI layout corruption when overlays land in the middle of wide graphemes. Critical for CJK language support and general text rendering correctness.

### 5. [#5283] `fix(tui): keep hardware cursor marker during slash-command autocomplete`
**URL:** `earendil-works/pi` PR #5283  
**Why it matters:** Another CJK-focused fix. Removes the `!autocompleteState` guard so the `CURSOR_MARKER` is emitted while the slash-command menu is active, fixing IME candidate-window placement for CJK input methods.

### 6. [#5288] `fix(coding-agent): don't decode non-image binary files as UTF-8 in the read tool`
**URL:** `earendil-works/pi` PR #5288  
**Why it matters:** Robustness fix. The `read` tool blindly called `buffer.toString()` on non-image files, which would corrupt binary files. Now skips decoding for non-text, non-image MIME types.

### 7. [#5269] `feat(coding-agent): add ctx.isInteractive to distinguish TUI from RPC mode`
**URL:** `earendil-works/pi` PR #5269  
**Why it matters:** Fixes a regression where `hasUI` returned `true` in RPC mode. Provides a clean, reliable API for extensions to check if a TUI is attached before rendering UI elements or interacting with the user.

### 8. [#5221] `fix: Fix OpenRouter reasoning instruction role`
**URL:** `earendil-works/pi` PR #5221  
**Why it matters:** Restores compatibility with OpenRouter reasoning models. Pi now sends `system` messages for system prompts on OpenRouter (instead of `developer`), aligning with their schema, while preserving `developer` role for native OpenAI.

### 9. [#5281] `feat(coding-agent): Support keybindings for all commands`
**URL:** `earendil-works/pi` PR #5281  
**Why it matters:** Major UX enhancement. Unifies built-in and extension commands under a `cmd.<name>` keybinding convention, allowing users to configure custom shortcuts for any registered command for the first time.

### 10. [#5264] `fix(coding-agent): refresh branch in footer on WSL /mnt repos`
**URL:** `earendil-works/pi` PR #5264  
**Why it matters:** Squashes a WSL-specific annoyance. The footer branch label was not updating after `!git switch` on Windows-backed mounts (`/mnt/c/...`). Adds a narrow polling window to catch the change.

---

## 5. Feature Request Trends

- **Zero-Day Provider Updates:** The community expects immediate model support upon release. The parallel requests for MiniMax M3 and Gemini 3.5 Flash indicate an expectation that Pi's provider catalog stays current with the model release cycle.
- **Extension System Maturation:** A clear pattern of requests for deeper integration APIs is emerging: `ui_prompt_start/end` events (#5302), `ctx.isInteractive` to detect TUI vs RPC (#5269), and customizable keybindings for all commands (#5281). This signals the extension ecosystem is ready for prime-time features.
- **Multimodal CLI Support:** Issue #5279 explicitly requests image attachment via the CLI (not just the TUI), highlighting a need for remote/SSH use cases to leverage vision capabilities (e.g., Gemma 4).
- **Session Management Ergonomics:** The addition of session naming to `/new`, `/clone`, and `/fork` in PR #5256 points to a growing desire for better session organization and workflow control.

---

## 6. Developer Pain Points

- **Unreliable Local Model Execution:** The largest recurring pain point. Local models (Qwen, Llama, DeepSeek) suffer from arbitrary timeouts (#5089, #5294), produce broken structured tool calls (#5307), and cause silent hangs (#5290). This is the single biggest barrier to a smooth local-first experience.
- **TUI Fragility Across Terminal Emulators:** The TUI remains a high-maintenance surface. Flickering dialogs (#5311), WezTerm image breakage (#5296), and CJK IME cursor issues (#5283) demonstrate the difficulty of building a robust terminal application that works uniformly across all emulators.
- **Provider API Incompatibility Churn:** Provider-side schema changes create immediate breakage. The MiniMax/OpenRouter `developer` role mismatch (#5229) and Bedrock Converse API empty-text block restrictions (#4975) create a constant game of catch-up for core compatibility.
- **Silent Failure States:** Several high-comment issues trace mysterious "Working..." hangs to unhandled rejections and missing error propagation (#5290, #5278, #5291). The community is actively pushing for better error surfacing and explicit failure modes.
- **Cross-Platform Gaps (Windows/WSL):** Issues like the `nul` file creation on Windows (#5304) and stale branch footers in WSL (#5264) indicate that cross-platform testing has been a blind spot in recent releases.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for **June 2, 2026**.

---

## Qwen Code Community Digest – 2026-06-02

### 1. Today's Highlights
Streaming reliability remains the dominant community concern this week, particularly for users running local models via Ollama and VLLM. The team has pushed a specific fix for SSE `bodyTimeout` (PR #4667) to mitigate the 300-second default that kills slow local connections. On the development side, **AUTO mode stability** is a clear priority, with simultaneous hardening of the permission classifier (PR #4680, PR #4572) to prevent false-positive blocks and runaway retries. Infrastructure maturity continues to advance with the addition of standalone auto-update support and Chrome DevTools CPU profiling.

### 2. Releases
- **[v0.17.0-nightly.20260602.cea15a118](https://github.com/QwenLM/qwen-code/releases/v0.17.0-nightly.20260602.cea15a118)** published in the last 24 hours. The release notes include a fix for a false *"compressed turn"* error that occurred during session rewind operations, improving the robustness of the conversation compression pipeline.

### 3. Hot Issues
1.  **[#3384 – Unable to add OpenAI-compatible local LLM](https://github.com/QwenLM/qwen-code/issues/3384)** *(11 comments)*: A long-standing config issue that continues to attract discussion. Users report that following the official documentation for VLLM endpoints doesn’t work with the latest npm package (v0.14.5). This is a core pain point for local-first users.
2.  **[#4657 – Using Qwen Code + Ollama: cannot complete tasks](https://github.com/QwenLM/qwen-code/issues/4657)** *(6 comments)*: Users of Qwen3.6-35B-A3B via Ollama report task execution hangs in v0.17.0, likely related to the streaming timeout issues addressed by PR #4667.
3.  **[#4604 – API Error: terminated (cause: Body Timeout Error)](https://github.com/QwenLM/qwen-code/issues/4604)** *(5 comments)*: A persistent Web page processing bug that manifests as a body timeout. The community is actively linking this to the same root cause as #4657.
4.  **[#4420 – UI bug causing token doubling on Windows](https://github.com/QwenLM/qwen-code/issues/4420)** *(5 comments, priority/P1)*: A critical regression in v0.16.0 where the CLI UI renders garbled text in Git Bash, leading to a doubled token consumption rate.
5.  **[#4686 – Bug: Qwen3.7-max streaming repetitive garbage](https://github.com/QwenLM/qwen-code/issues/4686)** *(1 comment)*: Qwen Code v0.17.0 against Qwen3-Max with thinking enabled falls into an infinite repetition loop. Highly disruptive for production workflows.
6.  **[#4676 – Auto-mode classifier times out too easily](https://github.com/QwenLM/qwen-code/issues/4676)** *(1 comment, 1 👍)*: A core infrastructure bug in the AUTO mode permission system. The classifier fails *closed* on timeout, meaning any transient network blip blocks an action as an infrastructure failure. The community strongly supports the proposed fix in PR #4680.
7.  **[#4624 – qwen --resume: child process memory leak leading to OOM](https://github.com/QwenLM/qwen-code/issues/4624)** *(2 comments, 2 👍)*: A documented memory growth issue in resumed daemon sessions. Users report hundreds of MB of unbounded growth per operation, leading to eventual crashes.
8.  **[#4687 – Daemon: subAgent text chunks interleave in transcript](https://github.com/QwenLM/qwen-code/issues/4687)** *(0 comments)*: A newly filed, highly technical bug. During `/review` commands, parallel sub-agent text chunks merge into a single block in the WebShell transcript, causing garbled output.
9.  **[#4675 – Vim INSERT mode Esc key leak and mode indicator lag](https://github.com/QwenLM/qwen-code/issues/4675)** *(1 comment)*: Two specific Vim-mode bugs affecting power users. The Esc key press leaks to the AppContainer handler, and the NORMAL/INSERT mode indicator lags.
10. **[#4672 – Auto/YOLO mode: file edits not applying on first read error](https://github.com/QwenLM/qwen-code/issues/4672)** *(1 comment)*: In automatic editing modes, a transient read error causes the tool to skip the file update entirely, requiring the user to re-prompt. Affects workflow efficiency significantly.

### 4. Key PR Progress
1.  **[#4680 – Loosen auto-mode classifier timeouts](https://github.com/QwenLM/qwen-code/pull/4680)** *(Closes #4676)*: A targeted hotfix to increase stage timeouts and disable thinking in the second stage of the AUTO permission classifier. This prevents the system from arbitrarily blocking actions on network jitter.
2.  **[#4572 – Harden auto mode self-modification checks](https://github.com/QwenLM/qwen-code/pull/4572)** *(Open)*: A major security hardening pass. This PR prevents the classifier from being bypassed by workspace-edit fast-paths when modifying Qwen Code’s own configuration, hooks, or MCP settings.
3.  **[#4667 – Configurable bodyTimeout for local model streaming](https://github.com/QwenLM/qwen-code/pull/4667)** *(Open)*: Implements a `generationConfig.bodyTimeout` field to replace the default 300-second hard limit on SSE idle connections. Directly addresses the core issue behind #4604 and #4657.
4.  **[#4629 – Standalone auto-update support](https://github.com/QwenLM/qwen-code/pull/4629)** *(Open)*: Adds SHA256-verified, atomic self-updates for non-npm installations, downloading directly from OSS/GitHub. A major DX upgrade for standalone users.
5.  **[#4620 – CPU profiling for Chrome DevTools](https://github.com/QwenLM/qwen-code/pull/4620)** *(Open)*: Introduces a `.cpuprofile` recording module triggered via environment variable or SIGUSR1 signal. Valuable for debugging performance regressions in long-running sessions.
6.  **[#4577 – Triage skill for GitHub issue/PR gatekeeping](https://github.com/QwenLM/qwen-code/pull/4577)** *(Open)*: A new `/triage` project skill designed for CI/GitHub Actions. It automates issue classification and PR admission review with staged bilingual comments.
7.  **[#4520 – Truncate model-facing tool output](https://github.com/QwenLM/qwen-code/pull/4520)** *(Open)*: Moves string truncation into `CoreToolScheduler` so all tool outputs are bounded before entering the conversation history, a key defense against context window overflow.
8.  **[#4524 – Bound foreground shell output capture](https://github.com/QwenLM/qwen-code/pull/4524)** *(Open)*: Implements a memory cap on foreground stdout/stderr retention. Prevents sessions from becoming unstable when processing very large shell outputs.
9.  **[#4526 – Bound hard rescue compression retries](https://github.com/QwenLM/qwen-code/pull/4526)** *(Open)*: Adds an upper limit to the compression retry loop, preventing infinite rescue attempts when the request remains too large.
10. **[#4410 – Telemetry Phase 3: subagent spans](https://github.com/QwenLM/qwen-code/pull/4410)** *(Open)*: Adds `qwen-code.subagent` spans for concurrent sub-agent isolation. Without this, telemetry traces from parallel sub-agents interleave destructively under the parent span.

### 5. Feature Request Trends
Several clear directions are emerging from the latest issue surge:

- **UI/UX Customization**: Users are demanding deeper control over the terminal interface. This includes replacing comma-separated text inputs with checkbox/multi-select UIs for model selection ([#4663](https://github.com/QwenLM/qwen-code/issues/4663)), preserving ANSI color codes in status lines ([#4669](https://github.com/QwenLM/qwen-code/issues/4669)), a general TUI optimization epic to reduce visual noise ([#4588](https://github.com/QwenLM/qwen-code/issues/4588)), and improved hierarchy displays for hook configurations ([#4536](https://github.com/QwenLM/qwen-code/issues/4536)).
- **SDK & Integration Maturity**: Developers are requesting explicit API support for advanced session management, such as a first-class `resume` method that doesn’t require injecting synthetic "continue" prompts ([#4679](https://github.com/QwenLM/qwen-code/issues/4679)). There is also strong demand for project-scoped `.mcp.json` with explicit approval semantics ([#4615](https://github.com/QwenLM/qwen-code/issues/4615)).
- **Observability**: Beyond the CPU profiling added in PR #4620, users want non-blocking daemon endpoints so that HTTP triggers can decouple submission from completion [#4582](https://github.com/QwenLM/qwen-code/issues/4582).

### 6. Developer Pain Points
- **Local Model Configuration Hell**: The most frequently recurring frustration is the unreliability of connecting to local LLM providers (Ollama, VLLM). Issues [#3384](https://github.com/QwenLM/qwen-code/issues/3384) and [#4657](https://github.com/QwenLM/qwen-code/issues/4657) describe configs failing silently or timeouts occurring despite correct setup. The configurable `bodyTimeout` (#4667) is the direct community-requested fix.
- **Memory Instability**: The memory leak in `--resume` mode ([#4624](https://github.com/QwenLM/qwen-code/issues/4624)) is a critical stability blocker for developers running daemon sessions. Unbounded growth requiring hard resets makes long-running agents unreliable.
- **UI Regressions on Windows**: The token-doubling bug ([#4420](https://github.com/QwenLM/qwen-code/issues/4420)) is a high-priority financial and usability regression. Combined with various terminal render glitches, Windows users face a consistently poorer experience.
- **Session Reliability**: A general theme of trust issues emerges from bugs like AUTOMODE false blocks ([#4676](https://github.com/QwenLM/qwen-code/issues/4676)), generation loops ([#4686](https://github.com/QwenLM/qwen-code/issues/4686)), trashed parallel transcripts ([#4687](https://github.com/QwenLM/qwen-code/issues/4687)), and Vim mode input leaks ([#4675](https://github.com/QwenLM/qwen-code/issues/4675)). These degrade the *trust* required for autonomous agent usage.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest — 2026-06-02

## 1. Today's Highlights
The most significant event is the project's official identity shift. The **v0.8.49 release renames the project to CodeWhale**, with legacy `deepseek` and `deepseek-tui` binaries reduced to deprecation shims that will be fully removed in v0.9.0. Beyond the rebranding, the community is actively building out **internationalization (7 locales)**, **Windows packaging**, and **new speech tools**, while simultaneously escalating pressure over **exploding token costs** and **agent mode reliability**.

---

## 2. Releases

**[v0.8.49 — The "CodeWhale" Release](https://github.com/Hmbown/CodeWhale/releases)**
This is a hard fork in naming. The `deepseek` and `deepseek-tui` binaries now print a deprecation warning before forwarding to `codewhale` / `codewhale-tui`. Users relying on automation or CI scripts should update their invocations immediately. Full migration details and asset preservation guidance are documented in `docs/REBRAND.md`. The deprecation shims will be cut entirely in the v0.9.0 release cycle.

---

## 3. Hot Issues

1. **[#1177 — Input cache hit rate critically low](https://github.com/Hmbown/CodeWhale/issues/1177) (25 comments)**
   Users report the input cache hit ratio lags far behind DeepSeek-Reasonix (~95%+). This is a major performance and cost concern, as every miss forces a full context recompute. High priority tag applied by the community.

2. **[#743 — Token consumption increased dramatically](https://github.com/Hmbown/CodeWhale/issues/743) (14 comments)**
   A single user reported consuming **400 million tokens** in half a day. The issue calls for urgent investigation into request density and dialog overhead. This signals a systemic inefficiency in how the agent manages context windows during long-running sessions.

3. **[#2487 — YOLO mode freezes ("Turn stalled")](https://github.com/Hmbown/CodeWhale/issues/2487) (11 comments)**
   When using `yolo` mode, the tool stalls with "Turn stalled — no completion signal received." The `continue` command cannot recover the state. This is a severe stability regression for users depending on autonomous agent execution.

4. **[#1969 — Will sessions and skills survive the rebranding?](https://github.com/Hmbown/CodeWhale/issues/1969) (9 comments)**
   A critical migration question: users have invested heavily in custom sessions and skills and are looking for clear guidance on how (or if) these assets transfer from `.deepseek` to `.codewhale`. REBRAND.md apparently needs stronger migration details.

5. **[#2492 — No cross-session memory](https://github.com/Hmbown/CodeWhale/issues/2492) (6 comments)**
   The agent resets completely on restart. Even forcing a memory write fails to trigger a read on boot. This is a foundational gap for anyone expecting persistent agent behavior, and it was raised with clear repro steps.

6. **[#2328 / #2523 — `exec_shell` tool unavailable in Agent mode](https://github.com/Hmbown/CodeWhale/issues/2328) (4 comments each)**
   An active configuration of `allow_shell = true` plus `trusted = true` still leaves `exec_shell` blocked in Agent mode, while it works fine in YOLO mode. This breaks a core workflow for power users and contradicts the documentation.

7. **[#1556 — macOS Ghostty screen flickering](https://github.com/Hmbown/CodeWhale/issues/1556) (5 comments)**
   The TUI flickers constantly inside the Ghostty emulator. Points to a likely rendering incompatibility with Ghostty's specific terminal implementation, impacting the growing macOS user base on modern terminal emulators.

8. **[#1812 — Windows 11 TUI freeze](https://github.com/Hmbown/CodeWhale/issues/1812) (5 comments)**
   Intermittent complete UI lockups on Windows 11. The process remains alive, but no input or screen updates are processed. `crossterm-poll` is under suspicion. Two separate events with logs and thread-state analysis have been captured.

9. **[#1186 — Typed persistent permission rules](https://github.com/Hmbown/CodeWhale/issues/1186) (8 comments)**
   An enhancement proposing a formal execution policy layer (`allow`, `deny`, `ask`) scoped by tool name, command prefix, and workspace-relative path. Shows strong community interest in granular security controls for agent actions.

10. **[#1357 — Input box overlaps with runtime prompt](https://github.com/Hmbown/CodeWhale/issues/1357) (4 comments)**
    A clear UI rendering defect where runtime prompt text covers the user's input area, making typed text partially or fully invisible in certain terminal states.

---

## 4. Key PR Progress

1. **[#2504 — v0.8.50 triage harvest](https://github.com/Hmbown/CodeWhale/pull/2504)**
   Maintainer Hmbown is preparing the next release. This branch bundles fixes for Windows installer docs (#1987) and miscellaneous stewardship cleanups from v0.8.48/v0.8.49.

2. **[#2565 — Contribution gate workflows](https://github.com/Hmbown/CodeWhale/pull/2565)**
   A formal `APPROVED_CONTRIBUTORS` allowlist plus automated gates for PRs and issues. Signals the project is scaling and actively managing external contribution quality.

3. **[#2045 — NSIS Windows installer](https://github.com/Hmbown/CodeWhale/pull/2045)**
   Submitted by ZhulongNT, this delivers a proper Windows `.exe` installer and a classroom deployment checklist, directly fulfilling a top community request.

4. **[#2508 / #2558 — Configurable API path suffix](https://github.com/Hmbown/CodeWhale/pull/2508)**
   Two community PRs addressing a major interoperability gap: many OpenAI-compatible endpoints don't serve on `/v1/chat/completions`. Users can now set `path_suffix` to `/v2` or `/chat/completions` directly.

5. **[#2562 — Fix npm binary version reporting](https://github.com/Hmbown/CodeWhale/pull/2562)**
   Fixes a subtle UX bug where `codew -V` could report the older npm wrapper version instead of the newer installed binary version, reducing user confusion during updates.

6. **[#2559 — Report legacy config migration](https://github.com/Hmbown/CodeWhale/pull/2559)**
   Instead of silently copying `~/.deepseek/config.toml` to `~/.codewhale/config.toml`, the tool now explicitly surfaces the migration event, preventing confusion over which config file is active.

7. **[#2560 — Xiaomi MiMo speech support](https://github.com/Hmbown/CodeWhale/pull/2560)**
   Adds a new speech tool and configuration wiring for Xiaomi's MiMo platform. An interesting expansion of the tool ecosystem beyond pure code generation into multi-modal input.

8. **[#2569 — Atlas Cloud validated model pool expansion](https://github.com/Hmbown/CodeWhale/pull/2569)**
   Extends CodeWhale's static model registry for Atlas Cloud from a legacy 2-model fallback to the validated chat model pool, keeping existing `deepseek-v4-*` aliases intact.

9. **[#2572 / #2568 / #2566 — i18n localization wave](https://github.com/Hmbown/CodeWhale/pull/2572)**
   A concerted push from contributor gordonlu. Localizes the context inspector panel, queue commands, and fanout card across English, Japanese, Simplified Chinese, Vietnamese, Portuguese, and Spanish.

10. **[#2563 — Session timestamps in listings](https://github.com/Hmbown/CodeWhale/pull/2563)**
    Fixes a basic discoverability issue: session lists will now show absolute timestamps instead of just relative ages ("2 days ago"), making it significantly easier to locate specific historical sessions.

---

## 5. Feature Request Trends

| Theme | Evidence |
|---|---|
| **Globalization / i18n** | The strongest active trend. Multiple PRs by gordonlu targeting 7 locales including Ja, ZhHans, Vi, PtBr, Es419. The project is visibly committing to a broad international user base. |
| **Windows parity** | From NSIS installers (#2045, #1987) to fixing freezes (#1812), Windows is a strategic investment area. |
| **Persistent agent memory** | Users want stateful agents (#2492). The current stateless approach combined with token bloat (#743) creates a design tension that needs resolving. |
| **Self-hosting & API interop** | Configurable API paths (#2508), local LLM integration (#2361), and provider abstraction all suggest users want CodeWhale to be a universal agent frontend, not just a DeepSeek client. |
| **Security & policy controls** | The typed permission rules proposal (#1186) indicates demand for granular trust/safety layers suitable for enterprise or shared environments. |

---

## 6. Developer Pain Points

- **Runaway token costs:** The #1 financial complaint. Low cache hits (#1177) and dense request generation (#743) are making heavy agentic workflows prohibitively expensive.
- **Fragile agent autonomy:** YOLO mode stalls (#2487) and inconsistent tool execution (#2328) undermine trust in autonomous task completion, forcing users to babysit the agent.
- **Terminal ecosystem fragmentation:** A cluster of platform-specific bugs — Windows 11 freeze (#1812), macOS Ghostty flash (#1556), iTerm2 UX friction (#2494), Wayland clipboard failure (#1920) — suggests the TUI rendering layer carries a heavy cross-platform maintenance burden.
- **Tool call inconsistency:** `exec_shell` works in YOLO but breaks in Agent mode (#2328, #2523). Local LLM tool calls fail completely (#2361). Workflows built in one mode or backend cannot be trusted to work in another without significant debugging.
- **Migration uncertainty:** The rebranding, while strategically sound, has exposed gaps in documentation and asset migration paths, creating friction for existing invested users (#1969).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*