# AI CLI Tools Community Digest 2026-05-30

> Generated: 2026-05-30 02:47 UTC | Tools covered: 9

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

| **Tool** | **Releases (24h)** | **Notable Hot Issues** | **Key PRs Updated** |
|---|---|---|---|---|
| **Claude Code** | 2 (v2.1.157/158) | Opus 4.8 quality degradation, 1M billing bugs, TUI data loss | 3 (credential guard, docs, lifecycle) |
| **OpenAI Codex** | 0 | Windows crashes, history loss, App reconnection loop | 10 (multi-agent overlay, cloud config, prompts refactor) |
| **Gemini CLI** | 2 (v0.45.0 nightlies) | `@filename:` hang, model capacity, false sub-agent success | 10 (7 merged: PTY fix, rollback, sandbox stdin) |
| **Copilot CLI** | 2 (v1.0.57 hotfixes) | Context bloat (73% tools), MCP timeouts, enterprise perms | 0 (stabilization focus) |
| **Kimi Code CLI** | 1 (v1.46.0) | Rate limiting fraud (60 vs 1200), agent ignores skills | 3 (error UX, dependency pins, release pipeline) |
| **OpenCode** | 0 | MCP server duplication, GPT latency, clipboard broken | 10 (Workspace v2, LiteLLM, inline `$skill`) |
| **Pi (mono)** | 1 (v0.78.0) | Codex/Codex hangs, EPIPE crash, Qwen integration broken | 10 (SambaNova provider, VCS extensibility, CJK IME fix) |
| **Qwen Code** | 1 (v0.17.0) | OOM on `--resume`, Anthropic compat, MCP security | 10 (DaemonWorkspace refactor, massive OTEL telemetry) |
| **CodeWhale (DeepSeek)** | 0 | Config fragmentation, MCP serve panic, Plan/Agent mode mismatch | 10 (CJK IME fix, TLS verify, sub-agent stop behavior) |

---

### 3. Shared Feature Directions

Requirements appearing across multiple tool communities reveal a convergence around a few critical pain points:

- **Context Window Transparency & Management:** Copilot CLI (#3539 – 73% tool bloat), Codex (#23591 – lost indicator), and Claude Code (#7111 – token counters) are all demanding visibility into context consumption. The current “auto-compaction” black box is eroding trust across the board. The ecosystem wants configurable limits, usage audits, and explicit compaction control.

- **MCP Ecosystem Maturity & Security:** Copilot CLI (timeouts ignored, policy false positives), Qwen Code (#4615 – approval-gated MCP), CodeWhale (#2362 – sub-agent MCP inheritance), and Claude Code (#51798 – sandbox regression) are all hitting serious stability and security gaps. The community is moving from “let me connect MCP” to “let me secure and audit my MCP connections.”

- **Workflow Orchestration & Sub-Agent Control:** Codex (#25155 – multi-agent system overlay), OpenCode (#29447 – task model override), Claude Code (#63843 – workflow amnesia), and CodeWhale (#2354 – stop-on-failure) demonstrate a consistent push beyond simple chat towards structured, multi-step agentic workflows with bounded execution and observability.

- **Cross-Platform & Internationalization (I18n):** Every tool with a heavy CLI/TUI surface is suffering. CodeWhale (CJK fix, Vietnamese locale), Claude Code (CJK IME #63824), Qwen Code (CJK #3456), Pi (IME positioning #5200), and Gemini (Wayland browser agent #21983) show that terminal emulator diversity and non-English input are critical failure modes, not nice-to-haves.

- **Enterprise Policy & Billing Guardrails:** Copilot CLI (#223 – org token permissions), Codex (#24969 – enterprise network blocks), and Gemini (#27115 – Vertex AI model identification) highlight enterprise adoption friction. Simultaneously, Kimi Code (#1994/#2123 – billing fraud) and Claude Code (#45390 – 1M context billing) expose that pricing transparency is the fastest way to destroy user trust.

---

### 4. Differentiation Analysis

- **Claude Code** is the most “agent-native” of the major vendors, investing heavily in its local plugin ecosystem (`.claude/skills`) and hook-based security (credential guard). Its primary vulnerability is its dependency on model quality—the Opus 4.8 regression is a systemic risk to its core value proposition.

- **OpenAI Codex** is leaning hardest into a **Desktop App + CLI hybrid architecture**, with the app-server v2 protocol and remote pairing. The multi-agent overlay and massive prompt extraction refactor signal a move towards a platform play, but Windows ecosystem gaps and session data trust issues are its biggest headwinds.

- **Gemini CLI** is executing with the highest velocity on raw bug fixes (7 merged PRs in 24h). Its tight coupling to Google’s model garden (Vertex AI, Workspace) is a strength for Google Cloud enterprises, but a weakness for the broader LLM community. The persistent model capacity errors and agent self-control issues (runaway searches) undermine its reliability story.

- **GitHub Copilot CLI** is playing a conservative, enterprise-focused game. The zero PR activity in 24h signals a team in full stabilization mode. The “73% context bloat” issue (#3539) is a ticking time bomb for its complex tooling ecosystem. Its differentiation lies in deep GitHub ecosystem integration (tokens, policies).

- **Kimi Code CLI** is in a **trust crisis and strategic pivot**. The “Kimi Code successor” announcement suggests a fundamental rebranding, but the reported ratio of 60 requests vs. 1200 advertised is a severe consumer protection risk. Engineering focus on unifying “provider error UX” (#2245) explicitly acknowledges this.

- **OpenCode** is the most **community-innovating open-core project** in the cohort. Workspace v2, LiteLLM integration, and inline `$skill` invocations show a feature velocity that outpaces many vendors. Its main weakness is systemic performance and memory regressions in its rapid release cycle.

- **Pi (mono)** is the **“universal client” contender**, aggressively adding providers (SambaNova, custom Bedrock headers) and extensibility hooks (VcsProvider, CLI parser export). It treats terminal diversity and provider fragility as a first-class engineering problem, which is its core differentiator.

- **Qwen Code** is undergoing a **deep architectural cleanup** (14 structural issues in #4063, DaemonWorkspace extraction). Massive OpenTelemetry instrumentation suggests an enterprise observability play. It uniquely addresses the “billing” complaint with PR #4614, indicating responsiveness to the power-user pricing gap.

- **CodeWhale (DeepSeek TUI)** has the strongest **externally contributed developer community**. The sheer volume of localization, config, and UX fixes from non-core contributors (CJK IME, Vietnamese, TLS verification) indicates a project that is resonating with a global, technically adept user base that values deep configurability.

---

### 5. Community Momentum & Maturity

**Tier 1: Major Vendor Stability (Mature, Enterprise-Ready)**
- **Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI:** These tools have massive corporate backing and the largest install bases. Their activity is characterized by rapid patch cycles reacting to regressions, strong process management (issue lifecycle PRs), and deep platform integration.
- **Key Signal:** High volume of “user trust” issues (billing, data loss, policy enforcement) indicates they are hitting enterprise security and compliance walls.

**Tier 2: High-Velocity Open-Source Architecture (Rapidly Iterating)**
- **OpenCode, Pi:** These projects are actively rewriting their architectural cores (Workspace v2, Provider overlays, Extension APIs). They are shipping at the highest feature velocity, driven by strong open-source communities.
- **Key Signal:** PRs tackling deep architectural debt (memory management, config loading, workspace handling) show they are maturing rapidly under the hood.

**Tier 3: Ecosystem Expansion & Refactoring (Strategic Investment)**
- **Qwen Code, CodeWhale (DeepSeek TUI):** These tools are investing heavily in telemetry, localization, and developer experience to expand beyond their initial user base. Qwen Code is aggressively refactoring its daemon architecture, while CodeWhale has the highest external contributor rate.
- **Key Signal:** Feature requests and PRs are heavily skewed towards platform agnosticism and config centralization.

**Tier 4: Pivot / Crisis (Critical Inflection Point)**
- **Kimi Code CLI:** The combination of a “successor project” announcement, a severe billing trust crisis (#2123), and a core agent regression (#2399) puts it at a crossroads. User sentiment is defensive, not growth-oriented.

---

### 6. Trend Signals

Several industry-wide signals emerge from this cross-tool analysis:

- **The Model is the Risk Vector:** Opus 4.8, Gemini Flash, and Qwen 3.7 Max all landed this week with severe quality or capacity issues. The ecosystem’s health is directly tied to model rollout quality. Tool providers must build model version pinning, A/B testing, and graceful degradation into their core architecture—or risk losing user trust with every model update.

- **The “Black Box” Context Window is the #1 UX Debt:** Users are demanding to see, audit, and control their context window usage. Auto-compaction without explanation is a major source of frustration. Expect all major tools to ship context explorers, token counters, and configurable compaction strategies in the coming months.

- **Billing is a UX Problem, Not Just a Finance Problem:** Kimi Code’s severe backlash and Claude Code’s 1M context confusion prove that opaque consumption models are a product liability. Transparent, real-time usage dashboards with predictable costing (e.g., fixed-rate quotas) will become a competitive differentiator.

- **MCP is the New Plugin API, But the Security Model is Immature:** Every tool is investing in MCP, but the community is uniformly hitting configuration fragility, process management, and security boundary issues. The “MCP Security Model” (approval gating, credential scanning, policy enforcement) is an emergent product category.

- **Sub-Agent Workflows are Going Mainstream:** The shift from “chat with a coding agent” to “delegate tasks to a managed sub-agent workforce” is evident across every digest. The community wants task-specific models, bounded execution, observable failure modes, and inherit contexts.

- **Globalization is a First-Class Engineering Problem:** CJK IME fixes, Vietnamese localizations, and terminal emulator compatibility issues are appearing in every digest. The AI developer tool market is genuinely global, and tools that ignore terminal diversity or non-English input will see adoption capped.

- **Open Source Tooling Drives Ecosystem Standards:** Pi, OpenCode, and CodeWhale are shipping features (inline skills, custom VCS providers, OSC 8 hyperlinks) that the major vendors haven’t prioritized. These grassroots innovations are shaping user expectations and will likely be adopted upstream by Claude Code and Codex.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Claude Code Skills Community Highlights Report**  
*Data snapshot: 2026-05-30 | Source: github.com/anthropics/skills*

---

### 1. Top Skills Ranking
*Ranked by community engagement signals from the top-20 most-discussed PRs.*

**1. Document Typography Skill (`#514`)**  
[anthropics/skills/pull/514](https://github.com/anthropics/skills/pull/514)  
**Functionality:** Enforces print-quality typography in AI-generated documents—eliminating orphan words, widow paragraphs, and numbering misalignment.  
**Discussion highlights:** Recognizes a universal weakness in LLM output formatting. Debate centers on balancing strict rule enforcement with genre-specific formatting (e.g., academic papers vs. business memos).  
**Status:** Open

**2. ODT Skill (`#486`)**  
[anthropics/skills/pull/486](https://github.com/anthropics/skills/pull/486)  
**Functionality:** Creates, fills, reads, and converts OpenDocument (.odt, .ods) files. Essential for LibreOffice/OpenOffice users in government and enterprise.  
**Discussion highlights:** Strong signal from organizations with ODF mandates. Conversations cover handling of embedded media, styles, and template substitution.  
**Status:** Open

**3. Skill Quality & Security Analyzers (`#83`)**  
[anthropics/skills/pull/83](https://github.com/anthropics/skills/pull/83)  
**Functionality:** Meta-skills that audit other Skills across five dimensions (Structure & Documentation, Security, Clarity, etc.).  
**Discussion highlights:** Community debate on rubric weighting—whether security checks should block a skill outright or just flag risks. Seen as critical for a trusted marketplace.  
**Status:** Open

**4. Frontend-Design Skill Improvement (`#210`)**  
[anthropics/skills/pull/210](https://github.com/anthropics/skills/pull/210)  
**Functionality:** Rewrites the existing `frontend-design` skill for maximum actionability and minimal conversational drift.  
**Discussion highlights:** Serves as a case study in skill design itself. Contributors argue over executable verb count vs. explanatory background.  
**Status:** Open

**5. SAP RPT-1-OSS Predictor (`#181`)**  
[anthropics/skills/pull/181](https://github.com/anthropics/skills/pull/181)  
**Functionality:** Integrates with SAP’s open-source tabular foundation model for predictive analytics directly inside Claude Code.  
**Discussion highlights:** First major enterprise model integration. Discussion centers on prompt strategies for exposing model predictions to non-technical users.  
**Status:** Open

**6. ServiceNow Platform Skill (`#568`)**  
[anthropics/skills/pull/568](https://github.com/anthropics/skills/pull/568)  
**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, SecOps, ITAM/SAM, CSDM, and IntegrationHub.  
**Discussion highlights:** Largest single-platform skill submitted. Active debate on scope management—whether a skill covering “the whole platform” dilutes reliability.  
**Status:** Open

**7. Testing Patterns Skill (`#723`)**  
[anthropics/skills/pull/723](https://github.com/anthropics/skills/pull/723)  
**Functionality:** Comprehensive testing stack coverage: unit (AAA pattern), React Testing Library, integration, and the Testing Trophy philosophy.  
**Discussion highlights:** High demand for consistent code quality enforcement. Discussion specific to mocking strategy recommendations and framework preferences.  
**Status:** Open

**8. AURELION Skill Suite (`#444`)**  
[anthropics/skills/pull/444](https://github.com/anthropics/skills/pull/444)  
**Functionality:** A five-floor cognitive framework (kernel, advisor, agent, memory) for structured professional knowledge management.  
**Discussion highlights:** Most architecturally ambitious submission. Long conversation thread on the ergonomics of the memory module and long-context retrieval strategies.  
**Status:** Open

---

### 2. Community Demand Trends
*Synthesized from the most-commented Issues.*

- **Enterprise collaboration & skill sharing** – Issue [#228](https://github.com/anthropics/skills/issues/228) (13 comments) demands org-wide skill libraries and direct sharing links, reflecting frustration with manual `.skill` file distribution.
- **Robust developer tooling** – Issues [#556](https://github.com/anthropics/skills/issues/556), [#202](https://github.com/anthropics/skills/issues/202), and [#189](https://github.com/anthropics/skills/issues/189) together surface a clear call for a polished `skill-creator` experience: predictable evaluation, duplicate prevention, and Windows compatibility.
- **Security & trust boundaries** – Issue [#492](https://github.com/anthropics/skills/issues/492) (6 comments) names the impulse-trust risk of community skills living under the `anthropic/` namespace. Issue [#412](https://github.com/anthropics/skills/issues/412) formally proposes an agent-governance skill.
- **Platform portability** – Issue [#29](https://github.com/anthropics/skills/issues/29) asks for AWS Bedrock support; Issue [#16](https://github.com/anthropics/skills/issues/16) requests Skills be exposable as MCP tools.

---

### 3. High-Potential Pending Skills
*Active PRs with recent updates, likely to land soon.*

- **n8n Builder & Debugger (`#190`)** – [PR link](https://github.com/anthropics/skills/pull/190)  
  Last updated 2026-05-18. Fills the highest-demand workflow automation gap. Two skills: workflow construction and runtime debugging.

- **Codebase Inventory Audit (`#147`)** – [PR link](https://github.com/anthropics/skills/pull/147)  
  Last updated 2026-02-04. 10-step workflow for identifying orphaned code, unused dependencies, and documentation debt. Heavy enterprise maintenance appeal.

- **Masonry Image / Video Generation (`#335`)** – [PR link](https://github.com/anthropics/skills/pull/335)  
  Last updated 2026-03-14. Integrates Claude with Imagen 3.0 and Veo 3.1 for managed media generation jobs.

- **Shodh Memory (`#154`)** – [PR link](https://github.com/anthropics/skills/pull/154)  
  Last updated 2026-03-03. Persistent cross-session memory for AI agents. Discussion on memory durability and recall precision continues.

- **Windows Compatibility Fixes (`#1099`, `#1050`)** – [PR #1099](https://github.com/anthropics/skills/pull/1099) / [PR #1050](https://github.com/anthropics/skills/pull/1050)  
  Last updated 2026-05-24. Critical unblockers for the Windows developer base (subprocess encoding, `PATHEXT` handling).

---

### 4. Skills Ecosystem Insight

The community’s most concentrated demand is a single shift: **from skills as simple prompts toward skills as reliable, auditable, and platform-specialized production modules**—with the strongest pull coming from document integrity, enterprise system integration (SAP, ServiceNow), rigorous quality/security verification, and professional developer tooling for the skill creation pipeline itself.

---

**Claude Code Community Digest – 2026-05-30**

---

### 1. Today's Highlights

Two rapid-fire patch releases (v2.1.157–158) landed, shipping local plugin auto-loading from `.claude/skills` and extending Auto Mode to Opus 4.7/4.8 on Bedrock, Vertex, and Foundry. However, the community is contending with a sharp regression wave: Opus 4.8 is showing widespread quality and reliability problems, while a cluster of billing bugs around 1M context and persistent TUI input issues are eroding developer trust.

---

### 2. Releases

- **v2.1.158**: Auto mode is now available on Bedrock, Vertex AI, and Amazon Foundry for Opus 4.7 and Opus 4.8. Opt in by setting `CLAUDE_CODE_ENABLE_AUTO_MODE=1`.
- **v2.1.157**: Plugins in `.claude/skills` directories are now automatically loaded, removing the need for a marketplace dependency. Added `claude plugin init <name>` to scaffold new local plugins. Tab-completion added for `/plugin` subcommands.

---

### 3. Hot Issues

Top 10 noteworthy issues by community impact and signal:

- **[[#45390]](https://github.com/anthropics/claude-code/issues/45390) 1M context incorrectly charges Max plan users** (30 comments, 26 👍)  
  A high-severity billing bug where Max plan users are erroneously prompted for extra usage fees when selecting Opus 4.6 (1M context). Heavy community outcry.

- **[[#51798]](https://github.com/anthropics/claude-code/issues/51798) PreToolUse `permissionDecision: "allow"` no longer suppresses sandbox prompts** (27 comments)  
  A v2.1.116+ regression breaks automated pipelines by ignoring hook-based approvals for unsandboxed Bash commands.

- **[[#6275]](https://github.com/anthropics/claude-code/issues/6275) Up arrow key erases entire prompt text** (25 comments, 41 👍)  
  A long-standing UX bug—one errant keystroke silently wipes multi-line prompts. The single most-upvoted complaint in this batch.

- **[[#63797]](https://github.com/anthropics/claude-code/issues/63797) Bash/Read tools intermittently return empty results on Linux** (5 comments)  
  A subtle concurrency race where successful commands (exit 0) return empty tool output, breaking long session context.

- **[[#63479]](https://github.com/anthropics/claude-code/issues/63479) `CLAUDE_CODE_DISABLE_1M_CONTEXT` env var ignored in 2.1.156** (4 comments)  
  Regression: users who explicitly block 1M context find the setting silently overridden, forcing unintended model switching.

- **[[#63304]](https://github.com/anthropics/claude-code/issues/63304) VSCode Chrome integration silently fails** (4 comments)  
  Three distinct bugs cause `mcp__claude-in-chrome__*` tools to fail without any user-facing error, making browser context invisible.

- **[[#63795]](https://github.com/anthropics/claude-code/issues/63795) Opus 4.8: excessive latency with degraded quality** (1 comment)  
  Users report Opus 4.8 is slower than 4.7 on simple tasks while producing lower-quality reasoning, described as "a step backwards."

- **[[#63451]](https://github.com/anthropics/claude-code/issues/63451) Opus 4.8 ignores MCP tool definitions, hallucinates parameters** (1 comment)  
  Rather than loading MCP schemas, Opus 4.8 guesses parameter names and enters long debugging loops, breaking all MCP-dependent workflows.

- **[[#63824]](https://github.com/anthropics/claude-code/issues/63824) Korean/CJK IME preedit broken in `claude agents` view** (1 comment)  
  IME composition text renders at the terminal's parked cursor (bottom-left) instead of the input caret; `CLAUDE_CODE_NATIVE_CURSOR=1` is ignored.

- **[[#63833]](https://github.com/anthropics/claude-code/issues/63833) `claude plugin list --json --available` truncates stdout at 64KB** (2 comments)  
  `process.exit` fires before the pipe drains, cutting off plugin data when piped to other commands—a critical DX bug for plugin builders.

---

### 4. Key PR Progress

Only 3 PRs were updated in the last 24 hours, suggesting a triage-heavy cycle. Analysis of each:

- **[[#62099]](https://github.com/anthropics/claude-code/pull/62099) Add credential-guard plugin for hardcoded secret detection**  
  A PreToolUse hook that scans Write, Edit, MultiEdit, and Bash (redirect/heredoc) calls for 20+ credential patterns before content is written. Directly addresses a major security gap for teams running Claude Code on sensitive repositories.

- **[[#63686]](https://github.com/anthropics/claude-code/pull/63686) Bump stale and autoclose timeouts from 14 to 90 days**  
  A process PR adjusting the issue lifecycle script—likely a response to community pushback against aggressive auto-closing of valid bugs.

- **[[#63467]](https://github.com/anthropics/claude-code/pull/63467) Docs: add Windows gh CLI install instruction in commit-commands README**  
  Documentation fix adding `winget install --id GitHub.cli` to the `/commit-push-pr` workflow README, improving Windows onboarding.

---

### 5. Feature Request Trends

The tracker reveals several strong emerging themes:

- **Deeper IDE Ecosystem**: Calls for a native JetBrains plugin ([#47166](https://github.com/anthropics/claude-code/issues/47166)) are intensifying. VS Code–only support is a growing adoption barrier for enterprise teams standardized on JetBrains.

- **Observability & Cost Visibility**: Users want time-elapsed indicators, token counters, and context usage displays restored or added ([#7111](https://github.com/anthropics/claude-code/issues/7111)). The 1M context billing confusion is amplifying this demand.

- **TUI Keyboard Modernization**: Requests for consistent Readline/Emacs keybindings ([#63823](https://github.com/anthropics/claude-code/issues/63823)) and proper CJK IME support ([#63824](https://github.com/anthropics/claude-code/issues/63824)) highlight that the terminal prompt needs to match modern IDE editing standards.

- **Agent Workflow Persistence**: A sophisticated proposal ([#63843](https://github.com/anthropics/claude-code/issues/63843)) advocates for native MCP integration to prevent "workflow amnesia"—context loss between long-running agent chains and sub-agents.

- **Platform Expansion**: Increasing noise for iOS/iPadOS support ([#63826](https://github.com/anthropics/claude-code/issues/63826), [#63493](https://github.com/anthropics/claude-code/issues/63493)) and native FreeBSD packaging ([#61313](https://github.com/anthropics/claude-code/issues/61313)) shows users want a universal agent experience.

---

### 6. Developer Pain Points

The current bug tracker paints a clear picture of where developers are struggling most:

- **Opus 4.8 Quality Regression** – This is the dominant concern. Ignored MCP schemas ([#63451](https://github.com/anthropics/claude-code/issues/63451)), malformed tool calls ([#63604](https://github.com/anthropics/claude-code/issues/63604)), and excessive latency ([#63795](https://github.com/anthropics/claude-code/issues/63795)) make the latest model feel unstable for agentic use.

- **1M Context Billing Confusion** – A perfect storm of bugs ([#45390](https://github.com/anthropics/claude-code/issues/45390), [#63761](https://github.com/anthropics/claude-code/issues/63761), [#63479](https://github.com/anthropics/claude-code/issues/63479)) where users are wrongly charged, cannot disable 1M context, or are blocked by incorrect API errors. Erodes trust in billing.

- **Sandbox & Permission Flakiness** – Recurring regressions in the hook/sandbox system ([#51798](https://github.com/anthropics/claude-code/issues/51798)) break CI/CD and automation pipelines where silent `allow` decisions are required.

- **TUI Input Fragility** – Data loss on arrow keys ([#6275](https://github.com/anthropics/claude-code/issues/6275)), hijacked cursor movement ([#62736](https://github.com/anthropics/claude-code/issues/62736)), and broken IME ([#63824](https://github.com/anthropics/claude-code/issues/63824)) create a high-friction editing experience for a terminal-native tool.

- **Plugin/Skill Builder DX** – Despite the v2.1.157 improvements, bugs like stdout truncation ([#63833](https://github.com/anthropics/claude-code/issues/63833)) and skill-vs-plugin registration confusion ([#63844](https://github.com/anthropics/claude-code/issues/63844)) show the local tool-building path is still rough.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-30

## Today's Highlights
No new releases landed today, but community activity remained high. The conversation is dominated by **Windows ecosystem friction** (startup crashes, enterprise network policy blocks, and rendering bugs) and **data integrity concerns** around disappearing session history. On the engineering side, significant architectural work is brewing in the PR queue, including a multi-agent system overlay, dedicated prompt extraction, and enterprise cloud config support signaling a broader platform maturity push.

## Releases
No new releases were published in the last 24 hours. The latest versions in active community discussion include Codex CLI `0.133.0` and Desktop App build `26.527.30818`.

---

## Hot Issues

**#12564** [Allow renaming task/thread titles] — *68 Comments, 110 👍*
Closed today after months of community advocacy. The ability to rename threads for better history navigation was the single most heavily requested UX feature in this dataset. A long-standing organizational pain point finally addressed.
[openai/codex#12564](https://github.com/openai/codex/issues/12564)

**#14297** [App reconnects 5 times before responding] — *42 Comments*
A persistent connectivity regression where the Codex App enters a “Reconnecting…” loop multiple times before serving a response. Closed today, likely resolved via a backend or client-side fix.
[openai/codex#14297](https://github.com/openai/codex/issues/14297)

**#22715** [Waiting for desktop despite app being authorized] — *25 Comments, 27 👍*
A critical remote development blocker. Plus users report an infinite “Waiting for desktop” state even when the remote/desktop pairing is properly authorized. Severely impacts the CLI ↔ Desktop remote workflow.
[openai/codex#22715](https://github.com/openai/codex/issues/22715)

**#19811** [Windows 10 workspace dependency repair fails] — *16 Comments*
A frustrating catch-22: the Desktop app detects broken dependencies and prompts a repair, but the repair action immediately fails because Windows 10 is flagged as unsupported by the dependency installer.
[openai/codex#19811](https://github.com/openai/codex/issues/19811)

**#23672** [Windows App fails to start: websocket closed] — *15 Comments*
Startup crash on Windows 11 25H2 producing an opaque `app-server` websocket error (code `3221225501`). Highlights ongoing platform compatibility work needed for the Windows Desktop App.
[openai/codex#23672](https://github.com/openai/codex/issues/23672)

**#23979** [Local project conversation history missing after update] — *8 Comments*
A high-severity data issue on macOS. Threads disappeared from the UI after a May 22 update, despite underlying SQLite data remaining intact in `~/.codex`. A serious trust erosion for users relying on local session durability.
[openai/codex#23979](https://github.com/openai/codex/issues/23979)

**#24969** [Windows Store Codex Browser Use blocked by enterprise policy] — *8 Comments*
A major enterprise adoption blocker. The in-app browser (IAB) automatically enforces network restrictions, and the Chrome extension backend is not selectable as a fallback. Makes the Browser Use feature non-functional in managed environments.
[openai/codex#24969](https://github.com/openai/codex/issues/24969)

**#20884** [Phone number requirement blocking multiple accounts] — *13 Comments*
Heated discussion around mandatory SMS verification. Power users with legitimate Plus subscriptions report being locked out of their accounts by administrative auth policies.
[openai/codex#20884](https://github.com/openai/codex/issues/20884)

**#23591** [Reimplement visible context/token usage indicator] — *34 👍, Closed*
The community strongly rallied around this regression. The loss of the visible context window indicator was a significant blow to power users who rely on token budgeting for complex agentic loops. Reimplementation is a clear win.
[openai/codex#23591](https://github.com/openai/codex/issues/23591)

**#25144** [Disable automatic conversion of long pasted prompts into .txt attachments] — *5 Comments*
A subtle but disruptive UX change. Structured prompts are silently transformed into file attachments, breaking direct editing workflows. Users want a configuration toggle to opt out.
[openai/codex#25144](https://github.com/openai/codex/issues/25144)

---

## Key PR Progress

**#25155** [Add model multi-agent system overlay] — *Open*
Introduces `multi_agent_version` to `ModelInfo` and a constrained catalog selector for root threads. This is the architectural foundation for a managed multi-agent orchestration layer.
[openai/codex#25155](https://github.com/openai/codex/pull/25155)

**#25195** [Suggest plugins from remote vertical catalog] — *Open*
Shifts plugin discovery from local persistence to a remote catalog, improving the out-of-box experience by suggesting relevant connectors (e.g., Databricks) without manual setup.
[openai/codex#25195](https://github.com/openai/codex/pull/25195)

**#24987** [feat(tui): hide background MCP startup status] — *Open*
Addresses TUI clutter during startup by hiding MCP initialization sequences. A necessary UX polish for workflows with slow or numerous MCP servers.
[openai/codex#24987](https://github.com/openai/codex/pull/24987)

**#24989** [feat(app-server): add remote control pairing start] — *Open*
Implements the `remoteControl/pairing/start` method for the app-server v2 protocol, enabling more robust desktop-side pairing for remote development scenarios.
[openai/codex#24989](https://github.com/openai/codex/pull/24989)

**#25151** [Extract prompts from codex-core] — *Open*
A significant refactor that moves all prompt text into a dedicated `codex-prompts` crate. Improves maintainability and ownership isolation for the growing core codebase.
[openai/codex#25151](https://github.com/openai/codex/pull/25151)

**#24696** [Support Library uploads for Codex Apps] — *Open*
Adds a `save_to_openai_library` requirement to file upload tools, with user-facing approval visibility for durable storage. Balances convenience with transparency.
[openai/codex#24696](https://github.com/openai/codex/pull/24696)

**#22668** [Wire managed MITM CA trust into child env] — *Open*
Ensures child processes trust Codex's managed MITM CA, critical for HTTPS inspection and limited mode to function reliably across spawned tools and scripts.
[openai/codex#22668](https://github.com/openai/codex/pull/22668)

**#24620** [Add cloud-managed config layer support] — *Open*
Part of a 5-PR stack introducing enterprise-managed cloud configuration. Allows organizations to push config layers that persist through loading, diagnostics, and protocol surfaces.
[openai/codex#24620](https://github.com/openai/codex/pull/24620)

**#25171** [fix: Bedrock API key region fallback] — *Closed*
Fixes a bug where the `AWS_BEARER_TOKEN_BEDROCK` environment variable path failed because Codex only checked the nested config key for region. Unblocks standard AWS credential flows.
[openai/codex#25171](https://github.com/openai/codex/pull/25171)

**#25184** [Propagate Codex installation id in Responses headers] — *Closed*
Unifies telemetry by adding `x-codex-installation-id` to standard `/responses` HTTP and WebSocket requests, matching what `/responses/compact` already sends.
[openai/codex#25184](https://github.com/openai/codex/pull/25184)

---

## Feature Request Trends

- **Thread & History Management:** Heavy demand for organizational features. The closure of #12564 (thread renaming) validates that navigating long agentic sessions is a top community priority.
- **Context Window Visibility:** The 34 upvotes on #23591 make it clear that power users view the token usage indicator as non-negotiable for managing long-running tasks.
- **Plugin/MCP Ecosystem Maturity:** Users want better plugin discovery (#25195), inline MCP App UIs (#21019), and cleaner startup experiences (#24987). The ecosystem is growing, but polish is lacking.
- **Prompt Control:** A rising desire to stop Codex from silently transforming user input, specifically disabling the long-paste-to-attachment conversion (#25144).
- **Remote Development Reliability:** Features like remote pairing (#24989) are nascent, but existing bugs (#22715) signal this is a high-value, high-friction frontier.

---

## Developer Pain Points

- **Windows Second-Class Experience:** This is the dominant negative theme. Installation failures (#19811), startup crashes (#23672), rendering glitches (#24904, #25160, #25196), notification errors (#25197), and enterprise network blocks (#24969) combine to make the Windows experience feel fragile and unsupported.
- **Session Data Trust:** Losing access to local history (#23979) is a major breach of trust. Even if SQLite data is recoverable, UI disappearance causes panic and severe workflow disruption.
- **Enterprise Network Friction:** Browser Use is neutered by corporate policy (#24969), and the Chrome extension workaround is poorly integrated on Windows (#24040). Large organizations will struggle to adopt Codex under these conditions.
- **Subagent UI Inconsistencies:** Display bugs showing UUIDs instead of nicknames (#23588) chip away at the perceived polish of the multi-agent system.
- **Auth as a Gatekeeper:** Phone verification (#20884, #25185) continues to generate friction for legitimate, paid users, creating unnecessary support overhead.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-30

The Gemini CLI team closed a large batch of stability fixes today, landing critical patches for extension rollback safety, sandbox stdin duplication, and hook context consistency. Simultaneously, a suite of high-priority (P1) PRs were pushed targeting PTY crash bugs on `--resume` and Vertex AI model identification. Community frustration remains high around `gemini-3-flash-preview` capacity limits and a persistent CLI hang triggered by `@filename:line` syntax, underscoring that agent reliability and model access are the community's top friction points.

## Releases

- **[v0.45.0-nightly.20260530.g013914071](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.0-nightly.20260530.g013914071)** – Resolves a crash loop when `preferredEditor` is misconfigured and adds minor UI improvements.
- **[v0.45.0-nightly.20260529.gc82e2b597](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.0-nightly.20260529.gc82e2b597)** – Hardens PTY resize logic against native crashes in the core engine.

## Hot Issues

1. **[#19985](https://github.com/google-gemini/gemini-cli/issues/19985)** – CLI hangs/freezes when using `@filename:line` or `@filename:range` syntax. 16 comments. A core bug with no fix yet, forcing affected users to force-quit regularly.

2. **[#19883](https://github.com/google-gemini/gemini-cli/issues/19883)** – Persistent "No capacity available for model gemini-3-flash-preview" errors. 12 comments, 8 👍. Users report `gemini-2.5-lite` and `gemini-3-pro` work, while Flash remains unreachable.

3. **[#23838](https://github.com/google-gemini/gemini-cli/issues/23838)** – Gemini 3.1 Pro unavailable to Google AI Plus subscribers despite clear subscription tier access. 11 comments, 10 👍. Closed, but generated significant heat around backend provisioning.

4. **[#18811](https://github.com/google-gemini/gemini-cli/issues/18811)** – Generic "Request contains an invalid argument" API error blocking updates. 14 comments, 5 👍. Affects users across v0.27.4 onward with no clear root cause published.

5. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** – Shell command execution stuck on "Waiting input" indefinitely after command completes. P1, 4 comments, 3 👍. Major workflow blocker for automation use cases.

6. **[#17448](https://github.com/google-gemini/gemini-cli/issues/17448)** – Agent repeatedly runs overly broad searches (e.g., searching 'Gmail' in `./`), pulling thousands of matches and causing massive context overflow. 9 comments. Widespread agent behavior issue.

7. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** – Subagent recovery after `MAX_TURNS` falsely reports `status: "success"` with `Termination Reason: "GOAL"`, hiding interruptions. 6 comments, 2 👍. Dangerous misrepresentation in autonomous workflows.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)** – Browser subagent fails on Wayland. P1, 4 comments, 1 👍. Blocks users on Linux environments using Wayland compositors.

9. **[#27052](https://github.com/google-gemini/gemini-cli/issues/27052)** – Cannot paste images from clipboard in Windows Terminal / Vim mode. Root cause identified as bracketed paste mode. Closed after diagnosis.

10. **[#26516 / #26522 / #26523 / #26525](https://github.com/google-gemini/gemini-cli/issues/26516)** – Cluster of Auto Memory bugs: indefinite retries on low-signal sessions, silent skipping of invalid patches, and secret redaction happening only *after* content is in model context. 9 combined comments. Security and data quality concern.

## Key PR Progress

1. **[#27574](https://github.com/google-gemini/gemini-cli/pull/27574)** – Automated nightly version bump for v0.45.0. (OPEN)
2. **[#27115](https://github.com/google-gemini/gemini-cli/pull/27115)** – **fix(cli): restore extension after failed update**. Adds backup and rollback logic for extensions that fail to load post-install. A major plugin reliability win. (MERGED)
3. **[#27123](https://github.com/google-gemini/gemini-cli/pull/27123)** – **fix(core): make keychain credential deletion idempotent**. Prevents crash when credentials are already deleted, smoothing the login flow. (MERGED)
4. **[#27127](https://github.com/google-gemini/gemini-cli/pull/27127)** – **fix(cli): avoid sandbox stdin duplication**. Fixes double message injection when sandbox mode relays stdin. (MERGED)
5. **[#27134](https://github.com/google-gemini/gemini-cli/pull/27134)** – **fix(core): skip hook context for tool continuations**. Eliminates hook-related glitches in pure function response agent loops. (MERGED)
6. **[#27375](https://github.com/google-gemini/gemini-cli/pull/27375)** – **fix(core): correctly identify Gemini 3 models with Vertex AI resource IDs**. P1 fix restoring tool access (web_search, activate_skill) for Vertex AI users on Gemini 3.1. (OPEN)
7. **[#27371](https://github.com/google-gemini/gemini-cli/pull/27371)** – **fix(core): handle EBADF when PTY fd is stale on session resume**. Fixes a crash on `gemini --resume` with stale file descriptors. (OPEN)
8. **[#27369](https://github.com/google-gemini/gemini-cli/pull/27369)** – **fix(core): prevent `--resume` from injecting session context into metadata**. Critical UI fix preventing chat sessions from permanently disappearing from the session browser. (OPEN)
9. **[#27383](https://github.com/google-gemini/gemini-cli/pull/27383)** – **fix(mcp-client): prevent eager tool wipe on network timeout**. Atomic refresh for MCP tools retains existing tools during transient network drops. (OPEN)
10. **[#27365](https://github.com/google-gemini/gemini-cli/pull/27365)** – **Add ephemeral session mode (`--ephemeral`)**. Community-driven feature for headless/data annotation workflows to avoid flooding session logs with disposable agent runs. (OPEN)

## Feature Request Trends

Three signal streams dominate the current feature landscape:

- **Smarter Agent Tools**: Users and internal teams are pushing hard for **AST-aware code navigation** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) to replace wasteful raw-text searches, and better **tool selection heuristics** ([#17448](https://github.com/google-gemini/gemini-cli/issues/17448)) to prevent context-wasting broad searches.

- **Memory System Maturity**: A dedicated cluster of issues ([#26516](https://github.com/google-gemini/gemini-cli/issues/26516) etc.) signals a serious push to harden the **Auto Memory** feature, targeting deterministic pre-emptive secret redaction, patch validation, and graceful handling of low-signal sessions.

- **Agent Lifecycle Control**: There is rising demand for **ephemeral sessions** ([#27365](https://github.com/google-gemini/gemini-cli/pull/27365)), **fine-grained sub-agent configuration overrides** ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and **permission gating** to prevent sub-agent execution when disabled ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)).

## Developer Pain Points

- **Agent Unpredictability**: The CLI agent frequently exhibits unwanted autonomous behavior—hanging on simple text references ([#19985](https://github.com/google-gemini/gemini-cli/issues/19985)), flooding context with overly broad searches ([#17448](https://github.com/google-gemini/gemini-cli/issues/17448)), and running sub-agents without authorization ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)). The false "GOAL" success reports ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) erode trust in automated pipelines.

- **Model Access & Authentication Friction**: Despite valid subscriptions, users routinely hit opaque "Capacity not available" ([#19883](https://github.com/google-gemini/gemini-cli/issues/19883)) and "Invalid argument" ([#18811](https://github.com/google-gemini/gemini-cli/issues/18811)) errors. The Gemini 3.1 Pro Plus subscription bug ([#23838](https://github.com/google-gemini/gemini-cli/issues/23838)) highlights a fragile gap between user entitlements and backend provisioning.

- **Cross-Platform Terminal Issues**: The CLI struggles with terminal emulator diversity. Wayland users are blocked from using the browser agent ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), tmux users face false background detection ([#27572](https://github.com/google-gemini/gemini-cli/pull/27572)), and Windows Terminal users lose clipboard image functionality ([#27052](https://github.com/google-gemini/gemini-cli/issues/27052)).

- **Extension & Integration Fragility**: VS Code extension detection often fails ([#18961](https://github.com/google-gemini/gemini-cli/issues/18961)), Google Workspace extension updates error out ([#18884](https://github.com/google-gemini/gemini-cli/issues/18884)), and, until today's patch, extension updates could permanently break plugins without rollback ([#27115](https://github.com/google-gemini/gemini-cli/pull/27115)). Plugin ecosystem stability remains a recurring frustration for developers building on top of the CLI.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for May 30, 2026.

---

## GitHub Copilot CLI Community Digest — 2026-05-30

### 1. Today’s Highlights
The Copilot CLI team shipped two quick patch releases (`v1.0.57-0` and `v1.0.57-1`) that fix a notoriously cryptic SDK auth error and give users an option to silence startup tips. Meanwhile, the community is rallying around a systemic context-window concern—tools and plugins consuming 73% of the available context before the first user message—and enterprise admins continue to push for full policy parity in the CLI.

---

### 2. Releases
Two patch releases arrived in the past 24 hours, building on the larger feature update (`v1.0.56`) that shipped yesterday.

- **v1.0.57-0:** A highly visible fix: authentication failures (e.g. GitHub API rate limits, invalid tokens) are now surfaced directly to the user instead of the opaque `"Session was not created with authentication info or custom provider"` error. Additionally, `/diff` now defaults to branch-level comparison when there are no local unstaged changes.
- **v1.0.57-1:** Adds the `showTipsOnStartup` setting, letting users disable the startup tip display—a small but clear quality-of-life win.

*Previous (v1.0.56 / v1.0.56-2): Introduced the `rubberDuck` built-in agent, opened the model picker for Free/Student users, redesigned the diff view with continuous scroll, and improved the `web_fetch` tool to prefer markdown content.*

---

### 3. Hot Issues

1. **[#223 – Enterprise Permissions for org-owned tokens](https://github.com/github/copilot-cli/issues/223)** (28 comments, 👍74)  
   The “Copilot Requests” permission scope is missing from the UI when creating org-owned fine-grained tokens. This forces enterprises to use individual PATs—a clear governance blocker. The highest-reaction open issue.

2. **[#700 – List supported models from the CLI](https://github.com/github/copilot-cli/issues/700)** (13 comments)  
   A simple but loud request for a `copilot --list-models` command to discover available models and their context multipliers without digging through menus.

3. **[#172 – MCP Timeouts ignored (CLOSED)](https://github.com/github/copilot-cli/issues/172)** (10 comments)  
   A critical MCP bug where the `timeout` field in `mcp-config.json` was completely bypassed by the runtime, causing all long-running tools to fail. The closure signals a direct compliance fix.

4. **[#3439 – TUI rendering lag inside tmux on mintty/Cygwin](https://github.com/github/copilot-cli/issues/3439)** (8 comments)  
   A painful regression starting in v1.0.49: the TUI becomes “stuck until keypress” inside tmux on Windows emulators. Users report v1.0.48 was stable.

5. **[#98 – Integrate prompts/*.md](https://github.com/github/copilot-cli/issues/98)** (6 comments, 👍28)  
   A high-upvote feature request asking Copilot CLI to natively load `.github/prompts/*.md` files, enabling team-wide system prompts stored alongside the codebase.

6. **[#3162 – Custom MCP servers falsely reported as “blocked by policy”](https://github.com/github/copilot-cli/issues/3162)** (6 comments)  
   Registry-listed MCP servers are incorrectly flagged as blocked by policy due to a false-negative in the CLI’s validation matching logic.

7. **[#3539 – Context window bloat: tools consume 73% of window](https://github.com/github/copilot-cli/issues/3539)** (4 comments)  
   A systemic issue: with ~10 MCP servers and plugins, the System/Tools preamble consumes 146k of 200k tokens, triggering automatic compaction before the user sends their first message. No current tooling exists to audit this.

8. **[#3575 – Hooks do not fire when resuming a session (CLOSED)](https://github.com/github/copilot-cli/issues/3575)** (1 comment)  
   Hooks (`agentStop`, `notification`) worked perfectly in new sessions but failed entirely on `/resume` or `--continue`. Swiftly closed, suggesting a targeted hotfix.

9. **[#3456 – Concurrent OAuth refresh kills token chain](https://github.com/github/copilot-cli/issues/3456)** (1 comment)  
   When concurrent MCP tool calls expire simultaneously, the CLI fans out parallel refresh-token requests, causing rotation conflicts on servers with strict reuse detection. A subtle but destructive auth bug.

10. **[#3547 – Background sub-agent hangs at turn zero](https://github.com/github/copilot-cli/issues/3547)** (1 comment)  
    Dispatched background sub-agents report success but then sit at `status: running, total_turns: 0` indefinitely. A major reliability blocker for multi-agent workflows.

---

### 4. Key PR Progress
No pull requests were updated in the last 24 hours. The current commit activity suggests the team is fully focused on stabilization and cutting hotfix releases (v1.0.57 train) rather than introducing new framework features. Expect the next wave of PRs to target the high-volume MCP and persistence bugs listed above.

---

### 5. Feature Request Trends

- **Enterprise Policy Enforcement:** The most heavily upvoted requests (#223, #2470) all demand that the CLI respect org-level policies for model visibility, token permissions, and authentication. Enterprise admins want CLI parity with the GitHub UI.
- **API & Extensibility Transparency:** Developers are asking for native model catalog listing (#700) and prompt file integration (#98). The goal is to codify, share, and audit AI configurations across teams without relying on UI clicks.
- **Agent Orchestration Maturity:** Requests for parallel sub-agent execution (#3568), custom sub-agent prompts (#3574), and local session logs (#3581) signal a shift from simple chat to structured multi-agent workflows that need observability and concurrency control.

---

### 6. Developer Pain Points

- **MCP Reliability:** The Model Context Protocol is the single largest source of friction this week. Issues range from configuration-level bugs (timeouts ignored, `disabled` flag not respected) to deep protocol-level problems (OAuth race conditions, dropped content fields, policy false-positives). The ecosystem is powerful, but implementation maturity lags behind the core CLI.
- **Context Window Management (Dark UX):** Issue #3539 crystallizes a design blind spot: users have no way to audit how many tokens their tools consume *before* a conversation begins. Auto-compaction feels random and destructive, eroding trust in model behavior.
- **State Persistence Regressions:** A recurring pattern of state loss (model selection reverts, `contextTier` not restored, session-store columns empty, hooks failing on resume). These issues (#1869, #2655, #3557, #3575) make the CLI feel less stateful than competing terminal-based AI tools, breaking developer flow on restart or resume.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-30

---

## 1. Today's Highlights
The release of **v1.46.0** publicly signals the project's transition towards a "Kimi Code successor," marking a major strategic inflection point. Despite this forward-looking move, community sentiment remains heavily fixated on cloud service friction—opaque billing calculations and severe rate limiting are eroding trust among paying subscribers (Issues #1994, #2123). Simultaneously, a newly filed critical bug shows the v1.46.0 agent failing to auto-trigger installed skills (#2399), raising questions about the readiness of the autonomous coding feature set.

---

## 2. Releases
**v1.46.0** ([View Release](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.46.0))
- **Strategic Shift:** Documentation now explicitly announces an "evolution to the Kimi Code successor project," hinting at a rebranding or platform expansion.
- **Router Fix:** Resolved auto-language redirect behavior.
- **Onboarding Polish:** Updated welcome tip links to point to `kimi.com`, streamlining the ecosystem entry point.

---

## 3. Hot Issues
*Six issues were updated in the last 24 hours. They cluster tightly around subscription trust, API reliability, and core agent functionality.*

1. **#1994 — Usage Calculation Dispute** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/1994))  
   *High community validation (👍6).* Users report K2.6's chain-of-thought consumes entire 2-hour quotas in just 2 tasks, contradicting the "300–1200 requests per 5 hours" marketing. Core ask is a shift from token-based to request-based billing transparency.

2. **#2123 — Severe Rate Limiting & Quota Depletion** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/2123))  
   *Critical trust issue.* A paid subscriber measured ~60 requests in 5 hours vs. the advertised 300–1200. User has escalated to a refund request under consumer protection law, exposing legal/compliance risk.

3. **#778 — Persistent API 400 Error** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/778))  
   *Long-running bug (18 comments)* affecting Windows users on the Claude Sonnet model. Remains unmerged, indicating a stubborn cloud-side integration issue.

4. **#2399 — Agent Ignores Installed Skills** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/2399))  
   *Fresh v1.46.0 regression.* The agent fails to auto-trigger available skills, falling back to raw shell commands. Severely undermines the "Kimi Code" autonomous promise.

5. **#2397 — Basic Shell Command Discoverability** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/2397))  
   *Signals an onboarding failure.* A user resorted to filing a bug report just to ask "how to execute a shell command," highlighting a major gap in help documentation and first-run experience.

6. **#247 — Onboarding Key Rejection (Resurfaced)** ([Link](https://github.com/MoonshotAI/kimi-cli/issues/247))  
   *Closed but recently updated.* Old issue (v0.52) about API key acceptance failure. Its revival suggests new users migrating to the latest version are hitting the same wall.

---

## 4. Key PR Progress
*Only 3 PRs were updated in the last 24 hours, but they reveal the team's engineering focus: ecosystem compatibility, error UX, and release hygiene.*

1. **#2398 — Relax OpenAI & FastMCP Dependency Pins** ([Link](https://github.com/MoonshotAI/kimi-cli/pull/2398))  
   Loosens SDK constraints to prevent downstream breakage (e.g., Kosong). Signals a push towards a more modular, plugin-friendly Kimi Code ecosystem.

2. **#2245 — Unify Provider Error UX Across 429 Surfaces** ([Link](https://github.com/MoonshotAI/kimi-cli/pull/2245))  
   Directly addresses the pain points from Issues #1994 and #2123. Centralizes error formatting to replace raw tracebacks with human-readable messages for rate limits and quota exhaustion.

3. **#2391 — v1.46.0 Release Pipeline Validation** ([Link](https://github.com/MoonshotAI/kimi-cli/pull/2391))  
   Automated version tag consistency checks between `kimi-cli` and `kimi-code` wrappers. Essential hygiene for maintaining the integrity of the rebranding effort.

---

## 5. Feature Request Trends
- **Billing Model Reform:** The overwhelming community demand is a move from opaque token-based costing to transparent request-based metering with a real-time usage dashboard.
- **Autonomous Agent Skill Execution:** Users expect the agent to dynamically discover and auto-trigger installed skills. The regression in #2399 reflects a deep desire for deterministic, hands-off tool use.
- **Rate Limit Visibility:** Developers want explicit `Retry-After` headers and consumption forecasts, not silent quota draining.

---

## 6. Developer Pain Points
- **Trust Deficit in Cloud Quotas:** The stark gap between the marketed "300–1200 requests per 5 hours" and the measured ~60 requests is the single largest source of user frustration and threatens subscriber retention.
- **Agent Unpredictability:** The agent falling back to raw shell commands instead of using defined skills (#2399) removes the core value proposition of an intelligent coding assistant.
- **API Error Opacity:** Generic 400 errors with no actionable debugging paths leave users guessing whether the fault lies in their prompt, subscription, or the cloud backend.
- **Onboarding Gaps:** Filing a bug to ask "how to run a shell command" indicates that the CLI's help system and initial user experience are not keeping pace with feature complexity.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-30

## Today's Highlights
The community is confronting critical performance and stability regressions, with major threads on GPT latency (`#29079`) and general slowdowns in the latest release (`#27106`). A significant desktop bug causing MCP server duplication (`#29939`) threatens workflow reliability, while core UX bugs like a non-functional clipboard (`#4283`) see intense continued discussion. On the development front, impactful PRs have landed proposing system prompt cache stability (`#29949`), a workspace v2 overhaul (`#29938`), and inline skill invocations (`#29217`).

## Releases
No official tagged releases were published in the last 24 hours. The latest reported stable versions in issues are `1.14.48` / `1.15.10`, with users reporting regressions in recent builds.

## Hot Issues

*   **[#29079] GPT Models takes too long to respond** (48 👍 | 109 comments)  
    Simple prompts sometimes take minutes to resolve. Users report variable latency spikes with specific model variants (e.g., GPT 5.4 with `xhigh`). Performance team likely investigating provider context caching or throttling.  
    [Link](https://github.com/anomalyco/opencode/issues/29079)

*   **[#4283] Copy To Clipboard is not working** (89 👍 | 101 comments)  
    A persistent, high-impact UI bug described across multiple OS versions. The high 👍 count signals this is a significant daily workflow blocker for many developers.  
    [Link](https://github.com/anomalyco/opencode/issues/4283)

*   **[#20695] Memory Megathread** (60 👍 | 82 comments)  
    Central tracking issue for scattered memory leak reports. The team requests heap snapshots rather than LLM-suggested fixes, indicating a systemic architecture issue under sustained use.  
    [Link](https://github.com/anomalyco/opencode/issues/20695)

*   **[#27530] Error: 4 of 5 requests failed: Unexpected server error** (10 👍 | 21 comments)  
    Startup crashes due to backend provider connection failures. Suggests a brittle service discovery or timeout issue in the modular plugin architecture.  
    [Link](https://github.com/anomalyco/opencode/issues/27530)

*   **[#27106] The latest version is terribly slow** (3 👍 | 7 comments)  
    Users report v1.14.48 is "practically unusable." Correlates with the `#29079` complaints and suggests a regression in the core LLM request handling or UI rendering pipeline.  
    [Link](https://github.com/anomalyco/opencode/issues/27106)

*   **[#19604] Write tool fails silently on large files (~1000+ lines)** (6 👍 | 7 comments)  
    A critical bug for codebase refactoring. The tool executes but returns no error, leaving developers unaware of failure. Raises questions about stream handling for large file writes.  
    [Link](https://github.com/anomalyco/opencode/issues/19604)

*   **[#25168] Jinja template error after compaction** (1 👍 | 14 comments)  
    Auto-compaction breaks LM Studio connections with a `No user query found` Jinja error. Highlights fragility in sidecar/local model context management.  
    [Link](https://github.com/anomalyco/opencode/issues/25168)

*   **[#29939] MCP servers spawn duplicate processes per session** (0 👍 | 3 comments)  
    Emerging critical bug. Spawning 8+ instances per project leads to crashes. Directly impacts the MCP ecosystem that many developers rely on for extensibility.  
    [Link](https://github.com/anomalyco/opencode/issues/29939)

*   **[#29923] Security: Docker supply chain — curl|sh without hash** (0 👍 | 3 comments)  
    A compliance-focused issue highlighting `curl | bash` with no hash verification and root containers. Raises trust and pipeline integrity concerns for deployment.  
    [Link](https://github.com/anomalyco/opencode/issues/29923)

*   **[#17765] Windows Desktop loses all session history after restart** (1 👍 | 6 comments)  
    Persistent UX bug. Sessions exist in `opencode.db` but the UI fails to load them. Affects Windows users specifically, pointing to a possible file path or deserialization issue in the Electron shell.  
    [Link](https://github.com/anomalyco/opencode/issues/17765)

---

## Key PR Progress

*   **[#29217] feat(TUI): Add inline `$skill` invocations**  
    A major UX enhancement. Adds autocomplete for `$skill` commands directly in the prompt composer. Closes five linked issues, signaling a significant improvement to command discoverability and flow.  
    [Link](https://github.com/anomalyco/opencode/pull/29217)

*   **[#29949] fix(session): move env block to tail of system prompt for cache stability**  
    Clever systems engineering. Rearranges the system prompt to make the static prefix cacheable across sessions, directly addressing prompt caching efficiency (Closes `#20110`, `#5224`).  
    [Link](https://github.com/anomalyco/opencode/pull/29949)

*   **[#29938] workspace v2**  
    A vague but potentially massive foundational PR from a core contributor (`jlongster`). Likely a ground-up refactor of how workspaces/projects are managed. Deserves close attention from the community.  
    [Link](https://github.com/anomalyco/opencode/pull/29938)

*   **[#29858] feat(ui): add collapsible reasoning summaries**  
    UI polish for "reasoning" output. Implements collapsible "Reasoning" sections matching existing "Explored" UI patterns, improving readability of long chain-of-thought traces.  
    [Link](https://github.com/anomalyco/opencode/pull/29858)

*   **[#29928] fix(desktop): collapse full-context git diffs**  
    Fixes a critical rendering bug where Git diff views in the Desktop app were loading full-file context, causing performance issues and jarring UX in code reviews.  
    [Link](https://github.com/anomalyco/opencode/pull/29928)

*   **[#29625] feat(core): add location-scoped config loading**  
    Introduces hierarchical config discovery (global → project → `.opencode`). Crucial for monorepo support and environment-specific provider/model overrides.  
    [Link](https://github.com/anomalyco/opencode/pull/29625)

*   **[#12633] feat(tui): add auto-accept mode for permission requests**  
    A long-running PR finally moving forward. Introduces an "autoedit" toggle (`shift+tab`) to auto-accept edit permissions with a 'once' reply, streamlining the edit loop while keeping other permissions manual.  
    [Link](https://github.com/anomalyco/opencode/pull/12633)

*   **[#29937] feat(opencode): add LiteLLM provider integration**  
    Opens up the ecosystem to the full set of LiteLLM-supported providers. A massive boon for users wanting enterprise or niche model backends without manual provider coding.  
    [Link](https://github.com/anomalyco/opencode/pull/29937)

*   **[#28943] fix(provider): expose reasoning effort variants for Kimi K2.6 and Qwen 3.6**  
    Corrects a blanket filtering bug in `transform.ts` that was hiding reasoning effort options for these models. Important for users relying on distilled reasoning variants.  
    [Link](https://github.com/anomalyco/opencode/pull/28943)

*   **[#29447] feat(opencode): add task model override**  
    Empowers primary agents to define which model a subagent uses for delegation. Critical for building agentic workflows where cost/performance split is required (e.g., planner uses Opus, coder uses Sonnet).  
    [Link](https://github.com/anomalyco/opencode/pull/29447)

---

## Feature Request Trends

*   **Agentic Delegation & Control:** Strong demand for better subagent management (`#29954`) and runtime task model overriding (`#29447`), indicating users are building complex multi-agent systems that need granular delegation controls.
*   **Visual & Context Richness:** Persistent requests for displaying images in chat results (`#21227`, `#29956`). The `$skill` and collapsible reasoning PRs show the team is actively closing this UX gap.
*   **Workspace & Identity:** Increased sophistication in workspace handling, with requests for fixing multiple clone identity (`#17940`) and introducing scoped configs (`#29625`) to support monorepo workflows.
*   **IDE Deep Integration:** Issues like `#4240` (Zed native review) and the various ACP fixes show users want OpenCode to feel like a native extension in editors rather than an external tool.
*   **Ecosystem Extensibility:** The influx of provider PRs (LiteLLM, Cloudflare) and the `opencode-balancer` plugin (`#29945`) reflects a thriving ecosystem where users demand broad backend support and community plugins.

---

## Developer Pain Points

*   **Performance & Latency Regressions:** The dominant theme. GPT response times (`#29079`) and complaints that the "latest version is slow" (`#27106`) are generating significant frustration and blocking productivity.
*   **Memory Overhead & Resource Leaks:** The memory megathread (`#20695`), MCP process duplication (`#29939`), and `ReadableStreamDefaultController` crashes (`#29941`) point to systemic resource management issues in the client.
*   **Unreliable Core Tools:** The `write` tool silent failures (`#19604`, `#15675`) and session history bugs (`#17765`) erode fundamental trust in the tool's basic read/write operations.
*   **Configuration & Compatibility Friction:** Users are struggling with ACP integration (`#6002`, `#24481`, `#25836`), custom template errors (`#25168`), and pipeline security concerns (`#29923`).
*   **Sub-agent Reliability:** When a sub-agent or API call fails, it can block or crash the parent session (`#29952`), creating a fragile experience for complex agent delegations.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest | 2026-05-30

*Data source: [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)*

---

## 1. Today's Highlights

**v0.78.0** shipped with two long-awaited quality-of-life features: **named startup sessions** (`--name`/`-n`) and **clickable file paths** via OSC 8 hyperlinks in tool titles. The community is intensely focused on stabilizing provider integrations, with urgent contributions flowing to fix regressions in **Kimi K2.6** and **Qwen 3.7 Max**, while several critical crash bugs (EPIPE on `edit` calls, ANSI stack overflow, compaction on assistant-tailed contexts) saw rapid remediation. **SambaNova Cloud** was accepted as a new built-in provider, signaling continued demand for first-class support across the model ecosystem.

---

## 2. Releases

**v0.78.0** — Two headline additions:

- **Named startup sessions** (`--name` / `-n`): Set a session display name before starting in interactive, print, JSON, or RPC modes. Improves session identification for users running multiple concurrent agents.
- **Clickable file tool paths**: File paths in `read`/`write`/`edit`/`ls` tool titles are now wrapped in OSC 8 hyperlinks, making them Ctrl-clickable directly from the TUI.

---

## 3. Hot Issues

| # | Status | Title | Signal | Why It Matters |
|---|--------|-------|--------|----------------|
| [#4945](https://github.com/earendil-works/pi/issues/4945) | **OPEN** | **openai-codex hangs on "Working..." with zero-usage aborted turns** | 48 💬 · 22 👍 | Most active issue. TUI freezes silently with `gpt-5.5`, forcing users to abort. Core reliability crater. |
| [#5117](https://github.com/earendil-works/pi/issues/5117) | **OPEN** | **Qwen 3.7 Max on OpenRouter is broken** | 5 💬 | `"developer is not one of ['system', 'assistant', 'user']"`. Popular model gated by a role check. |
| [#5098](https://github.com/earendil-works/pi/issues/5098) | **OPEN** | **Inline images and arrow keys broken inside tmux** | 3 💬 | `detectCapabilities()` disables images when `$TMUX` is set. Blocks power users in the most common terminal multiplexer. |
| [#4984](https://github.com/earendil-works/pi/issues/4984) | **OPEN** | **Interactive mode crash on transient terminal EPIPE** | 11 💬 | Uncaught `EPIPE` in `edit` tool calls brings down the whole process. Painful for anyone in pipe-heavy workflows. |
| [#5177](https://github.com/earendil-works/pi/issues/5177) | **CLOSED** | **Unable to stop model by pressing Escape or Ctrl-C** | 4 💬 | "Operation aborted" appeared seconds late. Loss of control is a top-tier UX regression. |
| [#5129](https://github.com/earendil-works/pi/issues/5129) | **OPEN** | **`ctx.ui.custom(factory)` without `overlay:true` bricks open sibling overlays** | 4 💬 | Extension API landmine. Critical for anyone building composable TUI overlays. |
| [#5200](https://github.com/earendil-works/pi/issues/5200) | **CLOSED** | **IME candidate window stuck at right edge in WezTerm** | 2 💬 | Hardware cursor not tracking input focus. Blocks CJK-language users on WezTerm. |
| [#5185](https://github.com/earendil-works/pi/issues/5185) | **CLOSED** | **Stack overflow on unrecognized ANSI control sequences** | 3 💬 | `RangeError: Maximum call stack size exceeded` in text rendering. Fragile parser under low-control inputs. |
| [#5209](https://github.com/earendil-works/pi/issues/5209) | **CLOSED** | **Custom tools always rendered as success, even with `result.isError: true`** | 2 💬 | Misleading UI. Failed extensions appear green, masking errors from agent and user. |
| [#5040](https://github.com/earendil-works/pi/issues/5040) | **CLOSED** | **`PI_CODING_AGENT_SESSION_DIR` forces flat storage** | 5 💬 | Environment variable bypasses per-project folder scoping, breaking `/resume` session filtering. |

---

## 4. Key PR Progress

| PR | State | Focus | Impact |
|----|-------|-------|--------|
| [#5197](https://github.com/earendil-works/pi/pull/5197) | **CLOSED** | **fix(coding-agent): guard compaction `continue()` on assistant-tailed context** | Prevents crash `"Cannot continue from message role: assistant"` after auto-compaction. Solves a subtle session continuity bug. |
| [#5196](https://github.com/earendil-works/pi/pull/5196) | **CLOSED** | **fix(ai): handle OpenCode reasoning params** | Direct fix for Kimi K2.6 regression on Opencode (closes #5169). Properly routes thinking mode parameters. |
| [#5189](https://github.com/earendil-works/pi/pull/5189) | **CLOSED** | **OSC 8 hyperlinks for file paths in tool titles** | Foundation of the "clickable file paths" feature in v0.78.0. Ergonomics improvement for reviewing agent output. |
| [#5206](https://github.com/earendil-works/pi/pull/5206) | **CLOSED** | **ai: add SambaNova as a built-in provider** | Ships with Llama 4 Scout/Raptor and DeepSeek V3 models. Expands first-class provider coverage. |
| [#5190](https://github.com/earendil-works/pi/pull/5190) | **CLOSED** | **coding-agent: make VCS detection extensible via `VcsProvider`** | Extension API enhancement enabling custom VCS support (e.g. `jj`). Non-blocking `detectAsync` for watch-triggered refreshes. |
| [#5195](https://github.com/earendil-works/pi/pull/5195) | **CLOSED** | **fix(coding-agent): buffer early input before prompt loop** | Fixes a race where text typed while the session starts is silently cleared. Smooths the startup UX. |
| [#5183](https://github.com/earendil-works/pi/pull/5183) | **CLOSED** | **fix: prevent stdout EPIPE from crashing the process** | Fixes the uncaught exception in #4984. Wraps `WriteWrap` errors gracefully. |
| [#5198](https://github.com/earendil-works/pi/pull/5198) | **CLOSED** | **fix(tui): default `showHardwareCursor` to true for IME support** | Switches to opt-out for hardware cursor. Directly fixes #5200 (IME positioning in WezTerm). |
| [#5202](https://github.com/earendil-works/pi/pull/5202) | **CLOSED** | **feat(coding-agent): Export CLI argument parser** | Allows extensions to reuse Pi's CLI parsing. Strengthens the SDK surface for tool developers. |
| [#5178](https://github.com/earendil-works/pi/pull/5178) | **CLOSED** | **ai: add custom-header support to Bedrock provider** | Closes the last gap on corporate proxy support by forwarding `StreamOptions.headers` through Bedrock. |

---

## 5. Feature Request Trends

**1. Provider Ecosystem Expansion**  
Users are demanding Pi be the universal client for every frontier model. Rapid community reaction to broken integrations (Kimi K2.6, Qwen 3.7 Max) and contributions like the new SambaNova provider signal that provider agility is the single highest-value axis.

**2. Session & Scripting Control**  
Growing appetite for CLI-first operations: `--session-id` flags, explicit context window sizing, and custom fetch hooks. The `--name` feature in v0.78.0 aligns with this trend, but users clearly want to script, resume, and parameterize sessions programmatically.

**3. Mature Extensibility / SDK**  
The `VcsProvider` interface and CLI parser export show a developer base building on top of Pi. Issues around `ctx.ui.custom` contracts and autocomplete typing safety show the API is powerful but has sharp edges the team is now forced to smooth.

**4. Terminal Portability**  
tmux is broken. WezTerm IME is broken. Soft-wrapped URLs break Ctrl-click. WSL has slash issues. There's a clear expectation that Pi should work flawlessly across *all* popular terminal environments, not just the primary dev machine.

---

## 6. Developer Pain Points

- **Provider Fragility is the #1 cause of churn.** Models change API contracts (roles, headers, reasoning params) faster than the client adapts. Every model release cycle brings a wave of "X is broken" issues.
- **Hangs and crashes dominate negative sentiment.** The silent hang in #4945 and the uncaught EPIPE crash in #4984 represent total UX failure states. Users cannot recover without killing the process.
- **Loss of control is deeply frustrating.** #5177 (failed abort) and #5195 (lost input) show that when the TUI doesn't respond to user actions, trust erodes quickly.
- **Terminal-specific regressions are a constant tax.** Each terminal (tmux, WezTerm, Windows CMD) has unique quirks that break core features (images, cursors, URLs). These affect power users disproportionately.
- **Extension API has rough edges.** The overlay bricking bug (#5129) and tool error styling bug (#5209) show that extension authors are actively building but encountering non-obvious API contracts that should be hardened.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for **2026-05-30**, based on the latest GitHub activity.

---

## Qwen Code Community Digest – 2026-05-30

### 1. Today’s Highlights
Qwen Code **v0.17.0** dropped today, bringing CLI startup-warning surfacing and telemetry bridge fixes. However, the community is buzzing about critical memory instability—a severe OOM bug in `qwen --resume` (#4624) is top-of-mind, while a massive architecture review (#4063) cataloging 14 structural issues is driving internal debate. On the PR front, OpenTelemetry coverage is exploding across the daemon and ACP paths, accompanied by a major refactor extracting the `DaemonWorkspaceService` to untangle the session bridge.

### 2. Releases
**v0.17.0** and **v0.17.0-nightly.20260530** have been published.
- **v0.17.0** ([Release link](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0)):
  - `fix(cli)`: Startup warnings now render on stderr before the TUI initializes (#4461).
  - `fix(telemetry)`: Improved error resilience in the `LogToSpan` bridge.
- **v0.17.0-nightly** ([Release link](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0-nightly.20260530.c699738f9)): Standard nightly tracking the `release/v0.17.0` branch.

### 3. Hot Issues
*Pick of 10 noteworthy issues from recent activity.*

1. **#4624 – `qwen --resume` sub-process memory leak / OOM**  
   A critical bug where child process memory grows hundreds of MB per operation and never releases, eventually crashing. Community members are demanding context compression that actually purges tool results from RAM.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4624) | 👍: 1

2. **#4609 – "Value of this must be DOMException" with local models (Ollama)**  
   Users connecting to local Qwen models via Ollama hit a total blocker. The error surfaces in the context-length classifier helper. PR #4632 is already out to fix it.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4609) | Comments: 4

3. **#4063 – Core + CLI Architecture Review (14 Structural Issues)**  
   A comprehensive audit identifies that `@google/genai` types infect 136 files, and several P0 architecture-level problems are flagged. This issue is acting as the roadmap for the ongoing refactoring wave.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4063) | 👍: 1

4. **#4616 – Qwen3.7-Max unavailable in model list, `/model` fails**  
   Windows 11 users cannot access qwen3.7-max via the standard OpenAI auth path. The issue highlights confusion around provider-specific model availability and configuration.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4616) | Comments: 2

5. **#4627 – macOS auto-update fails with EACCES (npm global prefix)**  
   `sudo npm install -g` followed by auto-update breaks because the updater lacks permissions for `/usr/local`. A classic Node.js deployment pain point.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4627)

6. **#4619 – Anthropic API `tool_result` adjacency errors**  
   When forwarding messages to Anthropic-compatible proxies, orphaned `tool_result` blocks cause API rejections. The fix (#4622) cleans up non-adjacent tool results.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4619)

7. **#4615 – Project-scoped `.mcp.json` with pending approval**  
   Users want MCP servers defined in the workspace to require explicit approval before connecting. A strong signal that the community is serious about credential security in MCP workflows.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4615)

8. **#3456 – CJK IME composition text at wrong position**  
   A long-standing UI bug where pinyin/candidate characters render on an extra line at the bottom of the terminal instead of at the cursor. High friction for East Asian users.  
   [Link](https://github.com/QwenLM/qwen-code/issues/3456) | Comments: 2

9. **#4586 – Ctrl+C behavior regression in PyCharm terminal**  
   After an upgrade, single Ctrl+C now exits the agent instead of requiring two presses. Esc key fails to interrupt, breaking the normal editing loop.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4586)

10. **#4614 – Pricing complaints: Qwen3.7-Max token consumption too fast**  
    A user explicitly requests a ¥400–500 “all-you-can-eat” bundle, comparing unfavorably to GPT/Claude pricing schemes. Indicates demand for power-user tiers.  
    [Link](https://github.com/QwenLM/qwen-code/issues/4614)

### 4. Key PR Progress
*Top 10 significant pull requests updated in the last 24 hours.*

1. **#4563 – `refactor(serve)`: Extract DaemonWorkspaceService**  
   A major piece of the ongoing server architecture cleanup. Pulls workspace-scoped logic out of the `AcpSessionBridge` into a proper service facade, paving the way for cleaner session management.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4563)

2. **#4632 – `fix(core)`: Harden context error text collection**  
   Directly fixes #4609. Catches `DOMException` accessor throws in provider error objects that were crashing the context-length classifier helper.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4632)

3. **#4622 – `fix(core)`: Enforce adjacent tool results**  
   Fixes #4619. Makes `cleanOrphanedToolCalls()` drop non-contiguous `tool_result` blocks, solving Anthropic API rejection errors.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4622)

4. **#4587 – `fix(core)`: Remove proactive subagent system-reminder injection**  
   A highly visible change that removes the "proactively use Agent tool" prompt from every turn. Reduces aggressive subagent spawning, giving the model less bias toward delegation. Marked for discussion.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4587)

5. **#4552 – `feat(serve)`: Runtime MCP server add/remove**  
   Implements HTTP routes (`POST /workspace/mcp/servers`) to mutate the MCP registry without a daemon restart. Covers T2.8 from the #4514 roadmap.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4552)

6. **#4629 – `feat(cli)`: Standalone auto-update support**  
   Adds self-update logic for non-npm standalone installations, including SHA256 verification and atomic replacement. Will resolve the EACCES pain from #4627 for standalone users.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4629)

7. **#4628 / #4630 – `feat(telemetry)`: Tool spans and session.id**  
   A massive expansion of OpenTelemetry coverage. Adds `session.id`, `client_id`, tool spans, and permission route spans across the daemon and ACP path. Makes daemon spans queryable in ARMS.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4628) | [Link](https://github.com/QwenLM/qwen-code/pull/4630)

8. **#4560 – `feat(cli)`: Settings JSON corrupted warning dialog**  
   Adds a fault-tolerant mechanism for corrupt `settings.json`, showing a UI warning dialog and recovering from backup. Addresses a silent failure mode.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4560)

9. **#4613 – `feat(daemon)`: Keep model & approval state consistent across clients**  
   Fixes race conditions where model and approval-mode changes were duplicated or lost when multiple clients (chat, IDE, terminal) share the same daemon session.  
   [Link](https://github.com/QwenLM/qwen-code/pull/4613)

10. **#4618 – `fix(core)`: Scope boolean coercion to boolean-typed fields**  
    Tool parameter validation was coercing `"true"` strings to booleans regardless of schema type. This fix constrains coercion to fields explicitly typed as boolean.  
    [Link](https://github.com/QwenLM/qwen-code/pull/4618)

### 5. Feature Request Trends

- **Observability & Diagnostics:** OpenTelemetry is the dominant theme this week. Users and maintainers are aggressively instrumenting every daemon path, MCP lifecycle, and permission check. Requests for CPU profiling (#4617) and heap snapshots (#4183) signal a desire for Chrome DevTools-grade debugging.
- **MCP Security & Manageability:** The community is pushing for runtime, approval-gated, and project-scoped MCP server configuration (#4615, #4552). This is a clear response to the security surface area MCP introduces.
- **Context & Memory Strategy Overhaul:** The existing "preserve tail" compaction is seen as broken. Users want a "summarize+restore" model (#4592) combined with aggressive memory cleanup to prevent the OOMs seen in #4624.
- **Pricing Flexibility:** High-end model consumption costs are a growing pain point, with explicit calls for large fixed-reset bundles or regional pricing adjustments.

### 6. Developer Pain Points

- **Memory Leaks:** The `--resume` OOM crash (#4624) is the most critical open stability issue. Tool execution history and session records are never released from RAM.
- **API Compatibility & Protocol Strictness:** Non-Qwen providers (Ollama, Anthropic) expose brittleness in error handling and message formatting. The `DOMException` crash (#4609) and `tool_result` adjacency errors (#4619) break workflows for users in mixed-provider environments.
- **Installation Footguns:** `sudo npm install -g` leading to `EACCES` on auto-update (#4627) is a classic Node.js pain point that the standalone auto-update PR (#4629) is only now addressing.
- **Terminal/IDE UX Regressions:** Changes in Ctrl+C handling (#4586) and persistent CJK IME rendering bugs (#3456) are causing daily friction for users in non-standard terminal environments.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# CodeWhale (DeepSeek TUI) Community Digest — 2026-05-30

---

## 1. Today's Highlights

The CodeWhale community was highly active today with 20 open issues and 20 pull requests updated. The primary focus areas were fixing critical stability bugs in the MCP server, addressing deep configuration fragmentation across platforms, and improving agentic AI behavior across mode switches. Notable contributions include a complete fix for CJK IME input handling, a new Vietnamese localization, and the long-demanded configuration for TLS certificate verification.

---

## 2. Releases

No new versions were released in the last 24 hours.

---

## 3. Hot Issues

*Selected 10 noteworthy issues based on community discussion frequency and impact on workflows.*

1. **[#2369 – Config Paths Fragmented Across OS and Cygwin](https://github.com/Hmbown/CodeWhale/issues/2369)** by *buko* — A deep infrastructure bug causing configuration files to be resolved inconsistently across Linux, macOS, and Cygwin, leading to silent data migration issues.

2. **[#2362 – Sub-agents lack MCP tools](https://github.com/Hmbown/CodeWhale/issues/2362)** by *buko* — Critical for multi-agent workflows: spawned sub-agents via `agent_open` cannot access the host session's configured MCP servers (Brave Search, Tavily).

3. **[#2353 – Memory config flag ignored](https://github.com/Hmbown/CodeWhale/issues/2353)** by *why37281* — High-frustration bug where explicit `[memory] enabled = true` in `config.toml` is silently ignored by the runtime, despite user following documentation exactly.

4. **[#2346 – AI Agent unresponsive to mode switching](https://github.com/Hmbown/CodeWhale/issues/2346)** by *DracheTek* — Detailed breakdown of wasted tokens: agents attempt write operations in "Plan" mode and fail to adapt when switching to "Agent" mode.

5. **[#2361 – Local LLM outputs JSON instead of executing tools](https://github.com/Hmbown/CodeWhale/issues/2361)** by *jillsoft-com* — Highlights a major interoperability gap where local models echo function signatures back as text rather than executing the tool calls.

6. **[#2352 – MCP serve panics on shutdown/disconnect](https://github.com/Hmbown/CodeWhale/issues/2352)** by *Neo-millunnium* — A blocking stability issue where `codewhale-tui serve --mcp` crashes immediately with a Tokio runtime panic ("Cannot drop a runtime in a context where blocking is not allowed").

7. **[#2247 – Support Custom DeepSeek-Compatible Providers](https://github.com/Hmbown/CodeWhale/issues/2247)** by *hatakes* — Persistent top-requested feature for API flexibility, allowing configuration of third-party or local DeepSeek-compatible endpoints.

8. **[#2339 – Tool search default cap buries MCP tools](https://github.com/Hmbown/CodeWhale/issues/2339)** by *T-Phuong-Nguyen* — The hardcoded `max_results=5` for tool discovery actively hinders discoverability when multiple MCP servers share keywords.

9. **[#2365 – Make Stream Timeout Configurable](https://github.com/Hmbown/CodeWhale/issues/2365)** by *mserrano11* — Users with slower or locally-deployed models (e.g., DeepSeek V4 Pro on a Mac Studio) require adjustable timeout thresholds to prevent premature disconnection.

10. **[#2310 – Cannot start message with `/`](https://github.com/Hmbown/CodeWhale/issues/2310)** by *zhyuzhyu* — A fundamental UX quirk with no escape mechanism for typing plain text messages that begin with a slash.

---

## 4. Key PR Progress

*Selected 10 important pull requests representing bug fixes, new features, and community infrastructure improvements.*

1. **[#2366 – Fix provider name in help text](https://github.com/Hmbown/CodeWhale/pull/2366)** by *reidliu41* — Corrects branding confusion where `/provider` help text listed "codewhale" instead of "deepseek" (Fixes #2363).

2. **[#2357 – Fix nested runtime panic on MCP shutdown](https://github.com/Hmbown/CodeWhale/pull/2357)** by *reidliu41* — Solves the blocking panic from #2352 by safely handling Tokio runtime drops in the CLI entrypoint.

3. **[#2367 – Add default Java and Vue LSP mappings](https://github.com/Hmbown/CodeWhale/pull/2367)** by *hufanexplore* — Extends default LSP support to enterprise ecosystems, mapping Java to Eclipse JDT LS and Vue to `vue-language-server --stdio`.

4. **[#2347 – Show Git branch in default footer](https://github.com/Hmbown/CodeWhale/pull/2347)** by *nightt5879* — Implements the feature requested in #2341, giving immediate branch visibility without requiring manual `/statusline` configuration.

5. **[#2344 – Raise tool search default results to 20](https://github.com/Hmbown/CodeWhale/pull/2344)** by *nightt5879* — Responds to #2339 by increasing `max_results` from 5 to 20 (capped at 100), significantly improving MCP tool discoverability.

6. **[#2330 – Route IME Chinese characters to composer](https://github.com/Hmbown/CodeWhale/pull/2330)** by *donglovejava* — Fixes a critical internationalization bug where Chinese input method committed characters were silently consumed by the paste-burst heuristic.

7. **[#2340 – Treat `/` followed by space as text](https://github.com/Hmbown/CodeWhale/pull/2340)** by *nightt5879* — Clean UX fix for #2310, allowing messages starting with `/` then a space to pass through as regular text without command dispatch.

8. **[#2358 – Add Vietnamese localization](https://github.com/Hmbown/CodeWhale/pull/2358)** by *hoclaptrinh33* — A full `vi` locale addition covering UI text, configuration, and a new `README.vi.md`.

9. **[#1893 – Make TLS verification configurable](https://github.com/Hmbown/CodeWhale/pull/1893)** by *wavezhang* — Adds `insecure_skip_tls_verify` configuration (config file + `DEEPSEEK_INSECURE_SKIP_TLS_VERIFY` env var) for users behind corporate proxies.

10. **[#2354 – Sub-agent bounded effort / stop-on-failure](https://github.com/Hmbown/CodeWhale/pull/2354)** by *h3c-hexin* — Enhances agent intro prompts to include stop-on-failure guidance, preventing costly retry loops on unreachable or rate-limited external APIs.

---

## 5. Feature Request Trends

*Distilled from issues, PRs, and community discussion patterns.*

- **Provider Agnosticism & Universal Gateway:** Users are demanding robust support for custom DeepSeek-compatible APIs, generic OpenAI-compatible endpoints, Atlas Cloud integration, and proxy configuration for web tools. The project is actively evolving from a dedicated DeepSeek client into a universal LLM TUI.
- **Configuration Centralization:** A dominant theme is the requirement for complete control over hardcoded limits. The community wants every UX threshold (stream timeout, walk depth, mention menu limits, result caps, tool search defaults) moved into `settings.toml`.
- **Agentic Workflow Maturation:** Developers are pushing for a fully context-aware agent. This includes sub-agent MCP inheritance, distinct behavioral modes (Plan vs. Agent), bounded retries, and deterministic file browsing for the `@`-mention menu.
- **Globalization & Accessibility:** Active localization efforts (Vietnamese) and critical input method fixes (CJK IME) highlight the user base's global diversity and the need for non-English developer workflow support.

---

## 6. Developer Pain Points

*Recurring high-friction areas observed across the issue tracker.*

- **Configuration Fragility & Inconsistency:** The highest friction area involves configs failing silently or producing unexpected behavior. The Memory toggle being ignored (#2353), platform-dependent config path resolution causing data loss (#2369), and branded naming confusion ("codewhale" vs. "deepseek") erode user trust.
- **Model–UI Disconnect:** A significant operational gap exists between the TUI's capabilities and the AI model's behavior. Agents fail to perceive mode switches (#2346), and local models struggle with basic function calling (#2361), forcing users into a confused "two-brain" workflow.
- **Stability in Server Mode:** The `serve --mcp` panic (#2352) and stream timeout issues (#2365) represent critical reliability barriers for IDE integrations, pointing to underlying resource management issues in the IPC and async runtime layers.
- **Arbitrary Hardcoded Constraints:** Several interface elements hit low ceiling limits (5 result tool search, 6-entry mention menu, 6-level walk depth) that actively punish users with deeper project structures or complex multi-server MCP setups.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*