# AI CLI Tools Community Digest 2026-06-28

> Generated: 2026-06-28 03:30 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Ecosystem (2026-06-28)

---

## 1. Ecosystem Overview

The AI CLI development tools landscape on June 28, 2026 is defined by an acute tension between **capability ambition** and **operational maturity**. While projects push aggressively into extended reasoning (Claude Code), high-speed generation (Codex), and multi-agent collaboration (Qwen Code), the collective user base is revolting against unpredictability in cost, behavior, and security. A clear bifurcation is emerging between "platform" tools (Pi, OpenCode, DeepSeek TUI) investing heavily in extensibility and "product" tools (Claude Code, Copilot CLI) struggling to stabilize their core promises. Across the board, **cost governance, context management, and cross-platform reliability** have overtaken model quality as the primary competitive differentiators.

---

## 2. Activity Comparison

| Tool | Community Pulse | Issues Volume (Hot 10) | PR Velocity (24h) | Releases (24h) | Key Signal |
|---|---|---|---|---|---|
| **Claude Code** | Frustrated / High Engagement | Very High (150+ combined 👍) | Low (2 PRs) | None | Bug gridlock eroding trust |
| **OpenAI Codex** | **Crisis Mode** | Critical (334 👍, 186 comments on #28879) | Very High (10+ PRs) | 3 Alphas | Rapid response to cost backlash |
| **Gemini CLI** | Cautious / Security-Focused | Moderate (8 comments max) | High (10 PRs) | 1 Nightly | Accelerating security hardening |
| **Copilot CLI** | Negative / Regression Fatigue | Moderate (20 👍 top) | Low (3 PRs) | None | TUI quality churn |
| **Kimi Code CLI** | **Inactive** | None | None | None | Project idle |
| **OpenCode** | Engaged / Velocity | High (34 👍 top) | Very High (10+ PRs) | None | Strong WSL/stability focus |
| **Pi** | Platform-Building | High (34 comments top) | High (8 PRs) | None | Extension API maturation |
| **Qwen Code** | Technically Focused | Moderate (4 comments avg) | High (10 PRs) | 1 Nightly | Collaborative features advancing |
| **DeepSeek TUI** | Cost-Sensitive / Active | High (24 comments top) | Very High (10+ PRs) | None (Gated) | Cache/token optimization push |

---

## 3. Shared Feature Directions

**Cost Governance & Budget Transparency**
A universal demand for predictable spending. **OpenAI Codex** users report 10–20× cost spikes draining Plus plans in 2–3 prompts (#28879, #29955). **DeepSeek TUI** users cite 400M tokens burned in half a day (#743) and poor cache hit ratios vs. competitors (#1177). **Qwen Code** faces backlash over silent model upgrades draining credits (#5819) and Anthropic prompt-cache misses (#5942). **Pi** responds with a native `reportUsage()` extension API for sub-agent cost tracking (#6119).

**Context & Memory Management as Competitive Moats**
**DeepSeek TUI** primes the space with its "Cache-Maximal Context Mode" (PR #3697, Issue #528), re-reading active files instead of summarizing. **Pi** introduces `excludeFromContext` to persist UI data without polluting the LLM window (#5678). **Qwen Code** pushes Git-shared team memory (#5867) and project-local todos (#5836). **Claude Code** sees speculative requests for reactive memory systems (#71937).

**Multi-Agent & Collaborative Workflows**
**Qwen Code**'s `qwen tag` (PR #5888) establishes channel-resident multiplayer agents. **Claude Code** users demand explicit Cowork compaction controls (#65114). **DeepSeek TUI** fixes daemon permission voting across connections (#5912) for team-based approval. The single-user model is clearly being pressured toward team integration.

**Security Hardening & File Hygiene**
**Gemini CLI** leads with SSRF DNS rebinding fixes (#28181), CI env-var leak patches (#28179), and symlink traversal blocking (#28180). **OpenAI Codex** faces sustained demand for `.codexignore` to block sensitive paths (#2847, 414 👍). **Copilot CLI** has a non-functional `preToolUse` hook (#3874). **OpenCode** addresses WSL UNC path injection (#19473). A clear industry-wide audit is underway.

**Plugin/MCP Ecosystem Maturity**
**OpenAI Codex** invests heavily in MCP OAuth serialization (PR stack #30292–#30296). **Gemini CLI** fixes MCP OAuth token refresh (#27889) and MIME type sniffing (#27878). **DeepSeek TUI** lands a formal plugin system with TOML manifests and registry lifecycle (#3710). **Pi** builds a fully extensible agent API around tools, cost reporting, and context management (#6119, #6121, #5678).

---

## 4. Differentiation Analysis

**Claude Code — The Thinking Pioneer**
Competes on the quality of extended reasoning (Opus 4.7). The current "thinking summary saga" (#49268, #49322, 150+ combined 👍) demonstrates the operational cost of this differentiation: a critical UX pipeline broken for weeks with no fix. The community's patience is thinning despite the brand's strong reasoning reputation.

**OpenAI Codex — The Power Layer**
Differentiates on raw model strength and execution speed (GPT-5.5). The current cost crisis (#28879) exposes a high-risk pricing model where unbounded potential meets unbounded cost. Users love the power but cannot trust the bill. The team's rapid PR response (10+ PRs, 3 alphas) suggests organizational muscle, but the transparency gap is damaging.

**Gemini CLI — The Security-First Enterprise Tool**
Uniquely positioned as the AI CLI that prioritizes safety over feature velocity. Today's security PRs are not reactive patches but a systematic hardening strategy: SSRF, env-var leaks, symlinks, shell parameter expansion controls (#28175). This is a direct bid for regulated enterprise adoption, sacrificing consumer buzz for architectural trust.

**GitHub Copilot CLI — The Ecosystem Integrator**
Relies on deep GitHub integration and a massive installed base. The current TUI regression crisis (alt-screen backlash #1799, ghost characters #3959, broken copy #3964) shows a product struggling to balance feature expansion with core UX quality. Risk of becoming ubiquitous but unloved as competitors refine their experience.

**OpenCode — The Provider-Agnostic Universal Client**
Competes on running anywhere with any model (WSL, Windows ARM, Linux, Copilot Enterprise, NVIDIA NIM). Cross-platform stability is the product. The high PR velocity (10+ fixes) addresses a real gap: many teams have heterogeneous environments that "macOS-first" tools ignore.

**Pi — The Extensible Platform**
The extension API is the primary product. Rapid movement on `reportUsage()`, `excludeFromContext`, safe reload deferral (#5735), and tool execution (#6121) shows Pi building an agent operating system. Targets developers who want to build custom AI workflows, not just use a CLI.

**Qwen Code — The Collaborative Agent**
Differentiates on multi-user, cross-device state. `qwen tag` (#5888), team memory tiers (#5867), and durable task files for `/loop` (#5889) are unique in the landscape. Targeting team leads and DevOps who need persistent, shared agent infrastructure.

**DeepSeek TUI / CodeWhale — The Cost Optimizer**
Differentiates on engineering efficiency. Cache-maximal mode, formal release scorecards (#3707), and the plugin system are designed for power users hitting hard token budget constraints. Extremely community-responsive to technical debt around caching and compaction.

---

## 5. Community Momentum & Maturity

**Highest Momentum / Rapid Iteration**
- **OpenAI Codex:** Despite a cost crisis, the PR velocity (3 alphas, 10+ PRs in 24h) and unified organizational response show a maturing engineering team capable of rapid crisis management.
- **DeepSeek TUI:** Very high technical velocity with a strong bilingual (Chinese/English) community. Active development of plugin systems, cache optimization, and formal release gating signal a project approaching production readiness.
- **OpenCode:** Sustained high PR output solving deep platform integration issues. Provider agnosticism and WSL support are resonating with enterprise users.

**High Engagement / Trust Volatility**
- **Claude Code:** Massively engaged community (150+ upvotes on thinking bugs) but low patch velocity. The disconnect between user expectations and delivery is widening.
- **Copilot CLI:** Negative momentum. High user count but mounting frustration over unaddressed regressions across rendering, Windows, and authentication.

**Strategic Platform Builders**
- **Pi:** Developer-centric community building on the extension API. Lower end-user volume but high developer intensity.
- **Gemini CLI:** Smaller, quieter community but clear strategic direction. Engineers are methodically closing security gaps rather than chasing features.

**At Risk**
- **Kimi Code CLI:** Complete inactivity. The project is dormant in a rapidly moving market.

---

## 6. Trend Signals

**1. Deterministic Cost is the New Competitive Moat**
The Codex and DeepSeek TUI crises signal a market limit: users will not adopt autonomous agents for wide-scale tasks without guaranteed cost caps and cache efficiency. "Budget as a Feature" is emerging—tools that provide hard constraints, transparent dashboards, and predictable token consumption will capture enterprise trust.

**2. Security is Becoming a Terminal Failure Mode**
The volume of SSRF, symlink, env-var leak, and prompt injection fixes in a single digest cycle (Gemini alone: 3 security PRs) suggests real-world exploitation is accelerating. A security incident could be a terminal brand event for a closed-source AI CLI tool. Security-first positioning (Gemini's strategy) is becoming a competitive advantage, not a constraint.

**3. Context Window Management Defines the Platform Tier**
The differentiating factor is shifting from "which model can write better code?" to "which tool can manage context, state, cost, and tools most reliably?" DeepSeek TUI's Cache-Maximal Mode, Pi's `excludeFromContext`, and Qwen's memory tiers are platform-level innovations that matter more than incremental model accuracy improvements.

**4. Cross-Platform Investment is the Untapped Gold Mine**
Consistent macOS-first development is leaving Windows and Linux users as second-class citizens. OpenCode's WSL fixes, Copilot's Windows batch failures (#3958), and Gemini's Wayland browser issues (#21983) all point to a massive underserved TAM. The tool that invests seriously in cross-platform QA will win heterogeneous enterprise environments decisively.

**5. The "Cowork" Paradigm is Inevitable but Immature**
Qwen Code's `qwen tag` and Claude Code's Cowork sessions signal an industry push toward persistent, multi-user, multi-agent collaboration. The current state (hangs, opaque compaction, permission loops) is fragile. The first tool to make collaborative AI agent sessions reliable, transparent, and state-persistent across user sessions will define the category for the next 12 months.

**6. Extensibility is Becoming Table Stakes**
The simultaneous investment in plugin systems (DeepSeek TUI), extension APIs (Pi), and MCP/OAuth stacks (Codex, Gemini) signals that the "walled garden" approach is dying. Developers are demanding the ability to customize, extend, and integrate. Tools that offer rich extension surfaces will capture developer mindshare; tools that are closed will be outrun by their ecosystems.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills Community Highlights Report

**Source:** `github.com/anthropics/skills` | **As of:** 2026-06-28

---

### 1. Top Skills Ranking

The following represent the most-watched Skill proposals by community engagement, covering a broad arc from quality-of-life improvements to enterprise integration.

**1. [document-typography](https://github.com/anthropics/skills/pull/514) (PR #514) — Author: PGTBoos | Status: Open**
- *Functionality:* Enforces professional typographic standards (orphan/widow control, heading isolation, numbering alignment) in generated documents.
- *Discussion Highlights:* A near-universal pain point in AI-generated output. Discussion centered on edge cases for multi-column layouts and whether to expose discretionary hyphen controls.
- *Status:* Open.

**2. [testing-patterns](https://github.com/anthropics/skills/pull/723) (PR #723) — Author: 4444J99 | Status: Open**
- *Functionality:* Comprehensive testing skill covering the Testing Trophy model, unit tests (AAA pattern), and React component testing with Testing Library.
- *Discussion Highlights:* One of the most-requested developer workflow skills. Debate focused on balancing verbosity vs. actionable specificity for test-generation patterns.
- *Status:* Open.

**3. [codebase-inventory-audit](https://github.com/anthropics/skills/pull/147) (PR #147) — Author: p19dixon | Status: Open**
- *Functionality:* Systematic 10-step audit workflow to identify orphaned code, unused files, documentation gaps, and infrastructure bloat.
- *Discussion Highlights:* Valued for its practical, structured approach to tackling technical debt directly in Claude Code. Reviewers requested clearer output formatting for integration with `CODEBASE-STATUS.md`.
- *Status:* Open.

**4. [shodh-memory](https://github.com/anthropics/skills/pull/154) (PR #154) — Author: varun29ankuS | Status: Open**
- *Functionality:* Persistent cross-session memory system enabling agents to surface relevant context via structured `proactive_context` calls.
- *Discussion Highlights:* Touches the core challenge of long-running agentic workflows. Discussion focused on memory eviction strategies and cost awareness for growing context stores.
- *Status:* Open.

**5. [skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83) (PR #83) — Author: eovidiu | Status: Open**
- *Functionality:* Meta-skills evaluating skills across 5 quality dimensions (Structure, Clarity, Examples) and a dedicated security posture scan.
- *Discussion Highlights:* Directly responds to the trust gap from Issue #492 (namespace impersonation). Community discussion centered on adding a trust-score rubric.
- *Status:* Open.

**6. [appdeploy](https://github.com/anthropics/skills/pull/360) (PR #360) — Author: avimak | Status: Open**
- *Functionality:* Enables full-stack web app deployment and lifecycle management (status checks, versioning, rollbacks) directly from Claude.
- *Discussion Highlights:* Significant interest in bridging code generation to production deployment. Reviewers explored auth token scoping and multi-environment support.
- *Status:* Open.

**7. [odt](https://github.com/anthropics/skills/pull/486) (PR #486) — Author: GitHubNewbie0 | Status: Open**
- *Functionality:* Create, read, fill, and convert OpenDocument Format files (.odt, .ods) to HTML, with LibreOffice/ISO standard compatibility.
- *Discussion Highlights:* Strong enterprise demand. Discussion focused on handling inline images and complex table structures within the ODF schema.
- *Status:* Open.

**8. [SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181) (PR #181) — Author: amitlals | Status: Open**
- *Functionality:* Leverages SAP's open-source tabular foundation model for predictive analytics on enterprise business data.
- *Discussion Highlights:* Signals demand for ERP data science integration. Reviewers discussed model serving patterns and data privacy when using local vs. remote inference.
- *Status:* Open.

---

### 2. Community Demand Trends

Extracted from top-voted and most-commented Issues, four dominant demand vectors emerge:

1. **Infrastructure Reliability (Critical Blockade):** Issues [#556](https://github.com/anthropics/skills/issues/556) and [#1169](https://github.com/anthropics/skills/issues/1169) report that `run_eval.py` consistently scores **0% recall on every iteration**, rendering the entire `skill-creator` optimization loop (run_loop.py, improve_description.py) effectively broken. This is the community's single most acute bottleneck. Issue [#1061](https://github.com/anthropics/skills/issues/1061) adds that the pipeline is entirely unusable on Windows due to subprocess and encoding assumptions.

2. **Security, Trust, and Governance:** Issue [#492](https://github.com/anthropics/skills/issues/492) alerts that community skills distributed under the official `anthropic/` namespace create a **trust boundary vulnerability**, enabling privilege escalation. Proposals for an [agent-governance](https://github.com/anthropics/skills/issues/412) safety skill and SPO security concerns ([#1175](https://github.com/anthropics/skills/issues/1175)) show the community is demanding rigorous access-control models.

3. **Distribution and Collaboration Infrastructure:** Issue [#228](https://github.com/anthropics/skills/issues/228) requests org-wide skill sharing without manual `.skill` file transfers. Issue [#184](https://github.com/anthropics/skills/issues/184) reports `agentskills.io` is down with a redirect loop, hampering ecosystem discovery. The demand for MCP interop ([#16](https://github.com/anthropics/skills/issues/16)) suggests users want skills to expose programmable APIs.

4. **Advanced Agentic Capabilities:** Beyond simple prompt skills, the community is proposing **persistent memory** ([#1329](https://github.com/anthropics/skills/issues/1329), compact-memory), **full-stack testing** ([#723](https://github.com/anthropics/skills/pull/723)), and **best-practice metacognition** for skill creators ([#202](https://github.com/anthropics/skills/issues/202)). This indicates a shift toward complex, stateful, and self-improving agents.

---

### 3. High-Potential Pending Skills

These open PRs carry the most community momentum and are likely to merge in the near term:

**Critical Infrastructure Fixes (Blockers)**
1. **[#1298 (MartinCajiao)](https://github.com/anthropics/skills/pull/1298)** — The primary fix for the `run_eval.py` 0% recall bug, addressing eval artifact installation, Windows stream reading, and trigger detection. Unblocks the entire optimization loop.
2. **[#1323 (Polluelo978)](https://github.com/anthropics/skills/pull/1323)** — Closes the root cause of trigger-detection failure in `run_single_query`. Highly complementary to #1298.
3. **[#1099 (joshuawowk)](https://github.com/anthropics/skills/pull/1099) / [#1050 (gstreet-ops)](https://github.com/anthropics/skills/pull/1050)** — Windows compatibility patches for subprocess PATHEXT resolution, cp1252 encoding, and pipe selection.

**High-Impact Skill Submissions**
4. **[#210 (justinwetch)](https://github.com/anthropics/skills/pull/210)** — Major rewrite of the `frontend-design` skill for clarity and actionability.
5. **[#723 (4444J99)](https://github.com/anthropics/skills/pull/723)** — `testing-patterns` skill, directly serving the top developer workflow demand.
6. **[#514 (PGTBoos)](https://github.com/anthropics/skills/pull/514)** — `document-typography` skill, addressing a universal output-quality gap.
7. **[#83 (eovidiu)](https://github.com/anthropics/skills/pull/83)** — `skill-quality-analyzer` and `skill-security-analyzer` meta-skills, enabling community-driven trust verification.

---

### 4. Skills Ecosystem Insight

The Claude Code Skills community is currently **blocked on a foundational reliability gap** (the broken 0% recall evaluation loop and unresolved namespace trust abuse), yet the underlying demand trajectory strongly points toward a **secure, stateful, and enterprise-grade agentic infrastructure**—prioritizing trusted governance, cross-session memory, and robust quality meta-validation over simpler content-generation prompts.

---

# Claude Code Community Digest – 2026-06-28

## Today's Highlights
The community remains tightly focused on the **Opus 4.7 thinking summary saga**, with issues [#49268](https://github.com/anthropics/claude-code/issues/49268) and [#49322](https://github.com/anthropics/claude-code/issues/49322) leading active discussion as the root cause becomes better understood (a missing `display: "summarized"` header in the harness). Separately, a controversial new clickable permission prompt (#70622) and a partial safety classifier outage (#69950) are causing acute workflow friction. No new releases were cut on the main branch this weekend, and pull request activity was minimal.

## Releases
No new versions of Claude Code were published in the last 24 hours.

## Hot Issues
*10 selected by community engagement, impact, and urgency.*

1. **[#49268 – Opus 4.7 Thinking Summaries Root Cause](https://github.com/anthropics/claude-code/issues/49268)**  
   *Comments: 46 | 👍: 75*  
   The community's most-upvoted open bug. User `yusufmo1` identified that the core CLI harness fails to set `display: "summarized"` in the API call, causing Opus 4.7 to omit thinking summaries entirely. A weeks-long issue with immense community interest.

2. **[#49322 – VS Code Extension Rendering Failure](https://github.com/anthropics/claude-code/issues/49322)**  
   *Comments: 47 | 👍: 41*  
   The downstream VS Code extension cannot render thinking summaries even when the API returns them. A close companion to #49268, leaving users with a blank thinking panel.

3. **[#39636 – Cowork VM ARM64 Boot Failure (Snapdragon X Plus)](https://github.com/anthropics/claude-code/issues/39636)**  
   *Comments: 32 | 👍: 9*  
   A long-standing blocker for Windows-on-ARM users. The Cowork virtual machine guest kernel fails to boot, timing out every connection attempt. Open since March with no resolution.

4. **[#70622 – Clickable Yes/No Prompts Backlash](https://github.com/anthropics/claude-code/issues/70622)**  
   *Comments: 8 | 👍: 24*  
   A strong UX backlash against the new clickable permission buttons in the terminal. Users report accidentally approving dangerous commands or cancelling actions by clicking in empty terminal space. Demand is high for a keyboard-only configuration toggle.

5. **[#69950 – Safety Classifier Outage](https://github.com/anthropics/claude-code/issues/69950)**  
   *Comments: 2 | 👍: 0*  
   An external safety service failure completely blocked bash and MCP tools for an extended period, exposing a hard dependency with no offline fallback and creating a full stop for users in auto-approval mode.

6. **[#57102 – Stale .git/index.lock in Worktrees](https://github.com/anthropics/claude-code/issues/57102)**  
   *Comments: 5 | 👍: 0*  
   Normal CLI operations are leaking Git lock files in worktree environments on macOS, requiring manual cleanup before subsequent commands can proceed.

7. **[#43474 – MCP Instructions Silently Truncated](https://github.com/anthropics/claude-code/issues/43474)**  
   *Comments: 3 | 👍: 2*  
   When multiple MCP servers are configured, the last server's instructions are silently cut off in the system prompt. A serious reliability concern for the MCP ecosystem.

8. **[#65114 – Request for Manual Cowork Compaction](https://github.com/anthropics/claude-code/issues/65114)**  
   *Comments: 5 | 👍: 1*  
   Users want an explicit `/compact` command during Cowork sessions. The current automatic-only compaction schedule is perceived as opaque and unpredictable.

9. **[#57230 – VSCode Native System Notifications](https://github.com/anthropics/claude-code/issues/57230)**  
   *Comments: 4 | 👍: 14*  
   High enthusiasm for OS-native toast notifications when Claude needs user attention. The current colored-dot indicator system is easy to miss when the window is not focused.

10. **[#71945 – Repetitive Thinking Token Loop](https://github.com/anthropics/claude-code/issues/71945)**  
    *Comments: 1 | 👍: 0*  
    A new and expensive bug: the thinking phase enters a repetitive generation loop, wasting ~2.3k tokens on repeated phrases before completing.

## Key PR Progress
*Only 2 pull requests were updated in the last 24 hours. Neither represents a major feature merge, but the open PR is a welcome refinement to the project's own tooling.*

1. **[#68787 – Fix(scripts): Add error message to edit-issue-labels.sh](https://github.com/anthropics/claude-code/pull/68787)**  
   *Status: OPEN*  
   A small but meaningful fix for the repository's own CI tooling. The `edit-issue-labels.sh` script previously exited silently with code 1 when called without arguments. This PR adds proper error reporting to stderr, improving debugging for maintainers.

2. **[#71798 – Closed PR (Title: ".")](https://github.com/anthropics/claude-code/pull/71798)**  
   *Status: CLOSED*  
   A closed pull request with no substantive description, likely a test, merge commit cleanup, or accidental submission.

## Feature Request Trends
Several clear directional themes emerge from the current issue queue:

- **Multi-Channel Notifications:** A strong push for a proper notification system spanning native OS toasts ([Windows #67220](https://github.com/anthropics/claude-code/issues/67220)), VSCode system notifications ([#57230](https://github.com/anthropics/claude-code/issues/57230), [#65241](https://github.com/anthropics/claude-code/issues/65241)), and mobile push for remote permission approval ([#62458](https://github.com/anthropics/claude-code/issues/62458)).
- **Cowork Control & Feedback:** Users want explicit compaction controls (manual `[#compact, #65114](https://github.com/anthropics/claude-code/issues/65114)` and agent-invokable [#71803](https://github.com/anthropics/claude-code/issues/71803)), alongside better feedback channels and feature parity across Claude surfaces ([#71941](https://github.com/anthropics/claude-code/issues/71941)).
- **MCP Stability & Correctness:** The ecosystem is growing, and users are demanding better handling of MCP server instructions (no truncation [#43474](https://github.com/anthropics/claude-code/issues/43474)), reliable environment variable propagation ([#71924](https://github.com/anthropics/claude-code/issues/71924)), and ecosystem compatibility ([#71943](https://github.com/anthropics/claude-code/issues/71943)).
- **Reactive Memory System:** A speculative but ambitious request ([#71937](https://github.com/anthropics/claude-code/issues/71937)) proposes that Claude should self-signal learning events, proactively updating its memory without requiring explicit user correction.

## Developer Pain Points
The most acute frustrations evident in this week's data:

- **Opus 4.7 Thinking Visibility Gridlock:** The combination of a harness API header bug and an extension rendering failure has completely broken thinking summaries for everyone using Opus 4.7 outside the standard CLI. Over 150 combined upvotes and weeks of silence have generated sustained community frustration.
- **Permission UI Regressions:** The clickable prompt change ([#70622](https://github.com/anthropics/claude-code/issues/70622)) has created a classic "dangerous UX" scenario where an attempt to streamline workflows accidentally enables destructive actions, with no easy way to disable it.
- **Fragile External Dependencies:** The safety classifier outage ([#69950](https://github.com/anthropics/claude-code/issues/69950)) paralyzed the entire tool for users in safe/auto mode. The lack of a local fallback or degraded mode is a major architectural pain point.
- **Cross-Platform Fragmentation:** Windows ARM users remain locked out of Cowork entirely ([#39636](https://github.com/anthropics/claude-code/issues/39636)). Windows desktop users lack native notifications ([#67220](https://github.com/anthropics/claude-code/issues/67220)). WSL2 users hit the VSCode thinking rendering bug ([#49902](https://github.com/anthropics/claude-code/issues/49902)). The platform experience feels inconsistent.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**Codex Community Digest — 2026-06-28**

---

### 1. Today's Highlights
The Codex community is in an uproar over a suspected 10-20× cost increase on GPT-5.5 rate limits (Issue #28879), draining Plus and Pro budgets in just 2-3 prompts. On a positive note, the critical SSD-endurance bug caused by runaway SQLite feedback logs (Issue #28224) has been largely resolved thanks to merged PRs #29432 and #29457, cutting writes by ~85%. The engineering team shipped three rapid Rust client alphas (v0.143.0-alpha.27-29) and advanced a major coordinated stack of PRs to stabilize MCP OAuth token handling.

---

### 2. Releases
| Version | Summary |
|---|---|
| **rust-v0.143.0-alpha.27** | Alpha release |
| **rust-v0.143.0-alpha.28** | Alpha release |
| **rust-v0.143.0-alpha.29** | Alpha release |

The three rapid-fire alphas of the Rust CLI client were published in the last 24 hours. No detailed changelogs accompanied the releases, suggesting hotfix iteration, likely related to the ongoing logging and rate-limit improvements in the v0.142.0 line.

---

### 3. Hot Issues (Top 10)

1. **[#28879] Budget Drain on GPT-5.5 (Plus Plan)** [OPEN]  
   The defining issue of the day with 186 comments and 334 👍. Users report a 10-20× increase in rate-limit token consumption since June 16, draining the 5-hour budget in 2-3 prompts. No official response yet.  
   *[openai/codex Issue #28879]*

2. **[#11023] Linux Desktop App Request** [OPEN]  
   The single most popular feature request (130 comments, 650 👍). The lack of a native Linux app is a critical blocker for Linux-native development teams.  
   *[openai/codex Issue #11023]*

3. **[#28224] SQLite 640TB/Year Write Bloat (Resolved)** [CLOSED]  
   The author confirmed this is fixed. PRs #29432 and #29457 (merged in v0.142.0) cut log volume by ~85%, saving industry-wide SSD endurance.  
   *[openai/codex Issue #28224]*

4. **[#2847] .codexignore / Sensitive File Exclusion** [OPEN]  
   79 comments, 414 👍. The demand for a mechanism to prevent the agent from reading sensitive paths (e.g., `.env`, `node_modules`) at both repo and global levels is a top security priority.  
   *[openai/codex Issue #2847]*

5. **[#29532] Persistent Log Churn Post-v0.142.0 (macOS)** [OPEN]  
   The fix for #28224 was partial. macOS users still see churn from `task-runner` and `feedback` SQLite targets, indicating a remaining debt in the logging pipeline.  
   *[openai/codex Issue #29532]*

6. **[#25744] Computer Use / MCP Zombie Process Leak (macOS)** [OPEN]  
   Long-running sessions accumulate unreaped helper processes, causing HID lag and WindowServer/TCC stalls. A critical system stability leak.  
   *[openai/codex Issue #25744]*

7. **[#29955] Instant 100-Credit Drain (Pro Plan)** [OPEN]  
   Confirms the scope of the #28879 issue. The author's 100 Pro credits vanished after a single message, immediately resetting the 5-hour limit to 0%.  
   *[openai/codex Issue #29955]*

8. **[#26984] MCP stdio FD Leaks (EMFILE)** [OPEN]  
   Pipe file descriptors and orphan child processes accumulate, eventually hitting OS "Too many open files" limits. A hard barrier for long-running MCP workflows.  
   *[openai/codex Issue #26984]*

9. **[#30390] Ambient Suggestions Silently Burning Tokens (Windows)** [OPEN]  
   The background suggestion feature consumed ~70k tokens without user interaction on Windows Desktop. Erodes trust in background resource accounting.  
   *[openai/codex Issue #30390]*

10. **[#20570] Windows Sandbox Startup Failure** [OPEN]  
    A persistent bug across multiple versions (`0.128.0` to `0.133.0+`) where the sandbox runner fails with `CreateProcessAsUserW failed: 1920`.  
    *[openai/codex Issue #20570]*

---

### 4. Key PR Progress (Top 10)

1. **[#30292 – #30296] MCP OAuth Serialization & Recovery Stack** [OPEN]  
   A coordinated 5-PR effort by `stevenlee-oai` covering shared credential store serialization, login/logout transactions, refresh ownership, and drift detection. The most significant engineering push in the current pipeline.  
   *[openai/codex PR #30292]*

2. **[#30395] Show Usage-Limit Reset Expiry** [OPEN]  
   Directly addresses the transparency crisis. Fetches reset-credit details so clients can show exact expiry dates. Pairs with Issue #29618.  
   *[openai/codex PR #30395]*

3. **[#30334] Structured Tool & Inference Timing Events** [OPEN]  
   Adds critical observability for app-server operators, distinguishing dispatch/queue time from handler time. Useful for diagnosing rate-limit and latency bottlenecks.  
   *[openai/codex PR #30334]*

4. **[#30269] Disable Nagle on Rendezvous WebSockets** [OPEN]  
   A low-latency fix for remote execution connections, disabling Nagle's algorithm to reduce network buffering for exec-server traffic.  
   *[openai/codex PR #30269]*

5. **[#29691] Enforce Marketplace Source Policy at Runtime** [CLOSED]  
   Merged. Enterprise admins can now enforce plugin allow/block policies, making blocked marketplace plugins inactive at the application level.  
   *[openai/codex PR #29691]*

6. **[#30327] Stabilize Synthesized Call Output IDs** [CLOSED]  
   A correctness fix ensuring stable conversation identity during prompt projection, preventing retries and edits from breaking context.  
   *[openai/codex PR #30327]*

7. **[#30291] Expose Environment Info RPC** [CLOSED]  
   Allows clients to query a remote execution environment’s shell and working directory before selection, improving multi-architecture workflows.  
   *[openai/codex PR #30291]*

8. **[#30089] Test MCP OAuth Concurrency and Recovery** [OPEN]  
   A comprehensive test suite for the new MCP OAuth stack, covering concurrent access, crash recovery, and token refresh races.  
   *[openai/codex PR #30089]*

9. **[#29432 / #29457] SQLite Log Write Reduction** [MERGED]  
   The hotfixes that cut 640TB/year write projections by ~85%. A major victory for platform reliability.  
   *[openai/codex PR #29432]*

10. **[#30384] Increase `currentTime/read` Timeout** [CLOSED]  
    A simple operational safety net, doubling the external time-read request timeout from 5s to 10s to prevent spurious failures.  
    *[openai/codex PR #30384]*

---

### 5. Feature Request Trends

- **Context Security & Hygiene**: The `.codexignore` / `.aiignore` request (#2847, #24993) is the dominant recurring theme. Developers explicitly want control over what the agent reads to prevent secrets leaking and context window bloat.

- **Platform Equity**: The persistent high demand for a Linux Desktop app (#11023) remains the largest platform gap, significantly limiting adoption in Linux-first environments.

- **Usage Transparency & Budgeting**: Following the rate-limit cost spike, users are demanding detailed breakdowns of token consumption, reset credit expiry (#29618, PR #30395), and background task costs.

- **User Agency & Permission Granularity**: A clear trend toward opt-in execution modes, including "ask before every edit" (#24325), non-blocking orchestration (#30399), and explicit confirmation for automation.

- **MCP Ecosystem Maturity**: The massive PR stack on OAuth stability signals strong community pressure for MCP to become a reliable, production-grade protocol rather than a brittle experimental feature.

---

### 6. Developer Pain Points

- **Opaque & Drastic Cost Increases (#28879, #29955)**: The single biggest pain point. Undocumented 10-20× jumps in token consumption destroy budget predictability and erode trust in the pricing model.

- **Silent Resource & Quota Leaks (#30390, #29532)**: Features operating in the background (ambient suggestions, log churn, MCP zombie processes) consume user resources without explicit consent or visibility.

- **MCP & Subagent Unreliability (#25744, #26984, #30407)**: Zombie process accumulation, file descriptor leaks, and subagents ignoring configured speed settings make the agent untrustworthy for hands-off workflows.

- **Windows as a High-Friction Platform (#20570, #21863, #29408)**: A chronic pattern of sandbox failures, blank editor panels, and resource-exhausting `git.exe` polling processes marks Windows as an unreliable platform for Codex Desktop.

- **Lack of Granular Permission Controls (#2847, #24325)**: The inability to easily exclude files, enforce edit confirmations, or set strict agent boundaries limits the tool's adoption in security-sensitive and enterprise codebases.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — June 28, 2026

## Today’s Highlights
Today's activity is defined by a major security hardening push, headlined by the **v0.51.0-nightly** release which enforces case-insensitive path blocklisting and VS Code human-in-the-loop (HITL) enforcement. A wave of critical PRs targets SSRF bypasses, CI environment variable leaks, and symlink-based path traversal vulnerabilities. Meanwhile, agent reliability remains a top concern, with patches merging to prevent silent scope expansion and to normalize MCP tool schemas for strict API compatibility.

---

## Releases
- **[v0.51.0-nightly.20260628.gae0a3aa7b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260628.gae0a3aa7b)**
  - **Security fix:** Enforces case-insensitive sensitive path blocklist and VS Code HITL validation (`#27966`). This closes a gap where mixed-case paths could bypass the blocklist and ensures human oversight in critical IDE operations.

---

## Hot Issues
1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** — **Subagent false success on MAX_TURNS (Bug, P1)**
   The `codebase_investigator` subagent reports `status: "success"` and termination reason `"GOAL"` even when it was interrupted by hitting the turn limit. This undermines trust in agent task completion. Active community discussion (8 comments) suggests this is a high-priority fix.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** — **Generalist agent hangs indefinitely (Bug, P1)**
   Simple tasks like folder creation cause the generalist agent to hang for up to an hour. The workaround—disabling sub-agent deferral—points to an orchestration deadlock. 8 upvotes reflect widespread developer frustration.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** — **Shell command stuck on "Waiting input" after completion (Bug, P1)**
   Commands finish normally but the UI retains a pending state. This degrades the core UX of the CLI, causing developers to repeatedly cancel and retry. 3 upvotes, heavily discussed in community chat.

4. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)** — **Zero-Dependency OS Sandboxing for bash affinity (Enhancement, P2)**
   Proposes leveraging the model's native bash expertise via local sandboxing instead of restricting it. This is a strategic feature request that could radically improve execution safety without sacrificing capability.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** — **AST-aware file reads, search, and mapping (Feature, P2)**
   An EPIC exploring AST-level intelligence to read precise method bounds, reducing token waste and misaligned tool calls. Directly addresses the "reads the whole file" pain point.

6. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)** — **Low sub-agent / skill utilization (Bug, P2)**
   Users report the model rarely invokes custom skills or sub-agents unless explicitly instructed. This limits the extensibility platform promise and leads to repetitive manual prompting.

7. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)** — **Deterministic redaction and Auto Memory logging (Bug, P2)**
   Auto Memory sends transcripts to the model before redacting secrets. This is a privacy concern: extraction happens in-context, and logs can persist skill data and transcripts without sanitization.

8. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)** — **Agent destructive behavior (Safety, P2)**
   Models occasionally use `git reset`, `--force`, or unsafe SQL operations when safer alternatives exist. The community is requesting built-in guardrails and risk awareness prompts.

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)** — **Browser subagent fails on Wayland (Bug, P1)**
   The browser agent crashes on startup in Wayland environments. Wayland adoption is growing, and this blocks an entire class of Linux developers from using the browser agent.

10. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)** — **400 error with >128 tools (Bug, P2)**
    Enabling too many tools triggers a 400 API error. The agent lacks tool-scoping intelligence, creating a scalability bottleneck for power users with rich MCP ecosystems.

---

## Key PR Progress
1. **[#28181](https://github.com/google-gemini/gemini-cli/pull/28181)** — **SSRF DNS rebinding fix (Security)**
   Replaces synchronous hostname string checking with proper DNS resolution in `web_fetch`. Closes a vulnerability class that could have allowed internal network probing.

2. **[#28179](https://github.com/google-gemini/gemini-cli/pull/28179)** — **Remove ISSUE_BODY / ISSUE_TITLE from allowed env vars (Security)**
   These variables bypassed sanitization, allowing prompt injection or data leakage in CI contexts. This is a proactive hardening for agent-in-the-loop workflows.

3. **[#28180](https://github.com/google-gemini/gemini-cli/pull/28180)** — **Restore defensive path resolution for @-reference files (Security)**
   Re-applies the symlink traversal fix from `#27943` that was previously reverted. Prevents `read_file`/`write_file`/`edit` tools from following malicious symlinks.

4. **[#27878](https://github.com/google-gemini/gemini-cli/pull/27878)** — **MCP image MIME type sniffing 🟢 Merged**
   Fixes Figma MCP integration where WebP images were mislabeled as PNG. Uses binary signature sniffing to prevent HTTP 400 errors. Directly unblocks design-to-code workflows.

5. **[#27889](https://github.com/google-gemini/gemini-cli/pull/27889)** — **MCP OAuth refresh with stored client ID 🟢 Merged**
   Fixes token refresh for auto-discovered MCP servers where `clientId` wasn't statically configured. Critical for long-running MCP sessions.

6. **[#27886](https://github.com/google-gemini/gemini-cli/pull/27886)** — **Respect .gitignore and .geminiignore in session context 🟢 Merged**
   Ensures `<session_context>` directory tree follows project ignore rules instead of pushing noise (like `node_modules`) into the agent’s context window.

7. **[#28172](https://github.com/google-gemini/gemini-cli/pull/28172)** — **Prevent silent scope expansion on task failure (Agent)**
   Fixes the `mandateConfirm` function to explicitly block the agent from running scripts or reading full files when asked for a localized code review. A direct quality-of-trust fix.

8. **[#28178](https://github.com/google-gemini/gemini-cli/pull/28178)** — **Require approved bot patch artifacts (CI Security)**
   Adds an explicit approval marker before the Gemini CLI bot's publish job consumes patch artifacts. Closes the reasoning-to-publish boundary against stale or malicious patches.

9. **[#28175](https://github.com/google-gemini/gemini-cli/pull/28175)** — **Require confirmation for shell parameter expansion (Policy)**
   Downgrades allow-listed commands containing `${...}` expansions to require confirmation in interactive mode and denies them entirely in `YOLO` / non-interactive mode.

10. **[#28169](https://github.com/google-gemini/gemini-cli/pull/28169)** — **Eval coverage report command (DevX)**
    Adds an `eval:coverage` command that cross-references eval test targets with the tool registry. Improves visibility into test gaps for maintainers and contributors.

---

## Feature Request Trends
- **Safety-first agent orchestration:** The community consistently asks for built-in destructive action detection, sandboxed execution, and scope-restricted task handling. The volume of security PRs today strongly correlates with these requests.
- **Memory system maturity:** Users want transparent, validated, and privacy-respecting memory. Specifically: deterministic redaction, quarantine for invalid patches, and opt-out mechanisms for low-signal session recording.
- **Intelligent context management:** AST-aware tools are the top "capability" request. Developers want the agent to understand code structure natively—reading only the relevant method or function instead of the whole file.
- **Reliable skill utilization:** A common complaint is that agents ignore custom tools and skills. The feature ask is for the model to proactively match task descriptions to registered skills without explicit prompting.
- **MCP ecosystem hardening:** As MCP adoption grows, so do requests for robust schema validation, OAuth lifecycle management, and resilience against misconfigured servers.

---

## Developer Pain Points
- **Agent reliability is the #1 trust blocker:** Hanging agents, false success reports, and stuck terminal processes are the most upvoted and discussed issues. Developers cannot rely on the CLI for unattended workflows.
- **Security friction slows adoption:** The constant tension between agent autonomy and safety is forcing users to choose between productivity and security. Sandboxing is the most requested solution, but the current state of symlink handling, env-var leaks, and SSRF exposure shows the gap is still wide.
- **Configuration feels fragile:** Broken themes, ignored `settings.json` overrides, unreadable `.env` files breaking extensions, and symlink-based agent files not being recognized all create a "death by a thousand cuts" experience for power users.
- **MCP integration is powerful but immature:** Strict schema validations, OAuth token refresh failures, and MIME type mismatches indicate the MCP integration layer needs hardening to match the excitement around the ecosystem.
- **Platform gaps are blocking Linux users:** The Wayland browser agent failure and terminal corruption on editor exit leave a segment of the developer community unable to use core features.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-28

## 1. Today's Highlights
Community sentiment is trending negative as a wave of terminal rendering regressions and platform-specific bugs dominate the discourse. The absence of a toggle to disable the new alt‑screen view is pushing power users away, while simultaneous failures on Windows (MCP server launches, clipboard operations, debugging paths) reveal significant quality assurance gaps. Adding to the frustration, the long-standing Ubuntu keychain bug remains unresolved despite heavy community demand.

## 2. Releases
No new releases were published in the last 24 hours. The latest active versions, **v1.0.65** and **v1.0.66**, are currently the subjects of the most severe community bug reports.

## 3. Hot Issues

| # | Issue | Why It Matters & Community Reaction |
|---|-------|--------------------------------------|
| 1 | **[#2165 – Ubuntu Keychain Support is Broken](https://github.com/github/copilot-cli/issues/2165)** (👍 20) | High-engagement authentication failure. The official documentation’s suggested workaround is incorrect, preventing Ubuntu users from persisting credentials. The community is demanding a reliable fix. |
| 2 | **[#1799 – How to Turn Off Alt-Screen Views](https://github.com/github/copilot-cli/issues/1799)** (👍 7) | Strong pushback against the forced alt‑screen rendering. Users want a simple `gh copilot config` toggle to revert to inline output, citing conflicts with terminal multiplexers and personal workflows. |
| 3 | **[#3964 – Copying Soft-Wrapped Output Drops Space](https://github.com/github/copilot-cli/issues/3964)** | A textbook regression. Issue #3666 was closed as fixed in v1.0.49, but the bug is back. This erodes trust in the release process and directly impacts the core workflow of copying generated code. |
| 4 | **[#3958 – Windows v1.0.66 MCP Server .bat/.cmd Failure](https://github.com/github/copilot-cli/issues/3958)** | Critical Windows regression. Any stdio MCP server launched via a `.bat` or `.cmd` script with arguments instantly crashes, effectively disabling MCP-based tooling for a large segment of Windows agent users. |
| 5 | **[#3949 – Windows 11 Copy Fails, Clipboard Empty](https://github.com/github/copilot-cli/issues/3949)** | The agent falsely reports content as “copied to clipboard” while nothing is actually stored. This breaks the fundamental user interaction loop and reduces trust in the agent’s feedback. |
| 6 | **[#3959 – Visual “Ghost” Characters in TUI](https://github.com/github/copilot-cli/issues/3959)** | Deleting text leaves visual artifacts on screen. Points to a flawed terminal cell redraw logic introduced in recent releases, resulting in a messy and unprofessional visual experience. |
| 7 | **[#3957 – MBP Trackpad Scrolling Broken](https://github.com/github/copilot-cli/issues/3957)** | A frustrating input regression where two‑finger scrolling on the MacBook Pro triggers prompt selection instead of scroll, likely caused by conflicing event handlers. |
| 8 | **[#3960 – Custom Model Provider Still Drains AI Quota](https://github.com/github/copilot-cli/issues/3960)** | User expectations clash with implementation. When a custom provider is set, users reasonably expect their own API endpoint to handle quota, not still count against their GitHub Copilot cap. |
| 9 | **[#3874 – VS Code `preToolUse` Hook Denial is a No‑Op](https://github.com/github/copilot-cli/issues/3874)** | Security‑governance regression. The agent hook system meant to deny specific commands is completely non-functional, nullifying team safety policies for VS Code agent users. |
| 10 | **[#3815 – Windows Debug Log Path Missing Backslash](https://github.com/github/copilot-cli/issues/3815)** | Minor but symbolic. The displayed path is malformed (e.g., `C:Usersuser`), adding friction to the debugging process and indicating a gap in Windows path normalization. |

## 4. Key PR Progress
*Note: PR velocity is low this cycle, with only three pull requests surfacing in the window.*

- **[#3928 – Add .gitignore and settings configuration](https://github.com/github/copilot-cli/pull/3928)** (Open)  
  A proposal to improve default project scaffolding. Addresses a real gap in generated projects but has not yet received maintainer feedback.

- **[#570 – [WIP] Add macOS installation instructions to README.md](https://github.com/github/copilot-cli/pull/570)** (Closed)  
  A long-standing PR created by the Copilot agent itself. Its recent closure signals the documentation effort has been completed or absorbed into a separate initiative.

- **[#3737 – Jigg empire ai](https://github.com/github/copilot-cli/pull/3737)** (Open)  
  A PR with no meaningful description and no comments. Appears to be a test or spam submission, contributing to low signal-to-noise in the queue.

## 5. Feature Request Trends

- **Contextual “Interrupt” Commands**  
  Inspired by Claude Code’s `/btw`, users want the ability to ask short contextual questions without corrupting the active session context ([#2778](https://github.com/github/copilot-cli/issues/2778)).
- **Granular Terminal Controls**  
  The alt‑screen toggle request is part of a larger desire for full control over CLI output rendering, session histories, and status bars ([#1799](https://github.com/github/copilot-cli/issues/1799), [#3963](https://github.com/github/copilot-cli/issues/3963)).
- **Transparent Usage & Quota Tracking**  
  Developers want visibility into session expiration and strict quota isolation when bringing their own AI model endpoints ([#3963](https://github.com/github/copilot-cli/issues/3963), [#3960](https://github.com/github/copilot-cli/issues/3960)).
- **Low-Code/No-Code Actions**  
  A minor but persistent signal for rigid high-level commands (e.g., “generate an iPhone app”) remains, though the broader community is far more focused on agentic flexibility ([#2824](https://github.com/github/copilot-cli/issues/2824)).

## 6. Developer Pain Points

- **TUI Regression Crisis**  
  The highest concentration of pain lives in the terminal user interface. Issues across rendering, input handling, and copying (##3959, #3957, #3964, #1799) suggest the recent UI investment needs urgent stabilization.

- **Windows Quality Chasm**  
  Three distinct critical bugs break core workflows on Windows (##3949, #3958, #3815). This signals a lack of platform-specific testing before general release, alienating a substantial portion of the developer ecosystem.

- **Release Reliability Fatigue**  
  The community is showing signs of burnout over recurring regressions. The incomplete fix of the copy-wrap issue (#3964, a regression of #3666) and the immediate breakage of MCP servers in a patch release (#3958) indicate stress in the QA process.

- **Authentication Fragmentation**  
  Linux users remain blocked on credential persistence (#2165), forcing them into a sub-optimal interactive login flow. The lack of progress on this high-👍 issue is a notable blind spot for the Linux user base.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — June 28, 2026

## 1. Today's Highlights
No new releases landed today, but the development and community activity was intense. The top themes are **cross‑platform stability** (WSL path corruption, memory leaks in server mode, platform‑specific TUI crashes) and **provider compatibility** (enterprise Copilot, NVIDIA NIM, GLM models). A wave of high‑value pull requests was opened, addressing the long‑standing WSL path bug, piped‑stdin breakage, empty‑content crashes, and introducing V2 session undo/redo and rename.

## 2. Releases
No updates published in the last 24 hours.

## 3. Hot Issues

**10 notable issues selected from the top 30 by community engagement:**

| Issue | Why it matters | Community reaction |
|---|---|---|
| **[#8816](https://github.com/anomalyco/opencode/issues/8816) — `llms.txt` & docs as Markdown** | Strong demand for making OpenCode’s documentation directly parseable by LLMs. | 34 👍 · 15 comments. Multiple users asking for an official convention. |
| **[#23153](https://github.com/anomalyco/opencode/issues/23153) — Pay‑Go with crypto** | Requests for cryptocurrency payment support reflect a non‑trivial user segment seeking alternative billing. | 24 👍 · 13 comments. Active discussion on feasibility. |
| **[#22422](https://github.com/anomalyco/opencode/issues/22422) — Memory Leak Warning** | `MaxListenersExceededWarning` is a recurring symptom of event‑handler accumulation, especially on Windows. | 7 comments. Linked to similar reports like #28492. |
| **[#19473](https://github.com/anomalyco/opencode/issues/19473) — Desktop sends UNC paths to WSL** | Windows Desktop app converts WSL paths to `\\wsl.localhost\…` format, breaking every bash tool call. | 7 comments. High friction for WSL users; a top platform pain point. |
| **[#12219](https://github.com/anomalyco/opencode/issues/12219) — OpenRouter credit / token limit** | Users of free or cheap models (e.g., Kimi 2.5) hit hard token caps when credits are too low, with a confusing error. | 7 comments · 6 👍. Provider cost UX friction. |
| **[#19130](https://github.com/anomalyco/opencode/issues/19130) — Windows ARM64 TUI fails** | Native ARM64 binary runs CLI but the TUI panics on `bun:ffi`/TinyCC. Growing user base for WinARM. | 6 comments · 5 👍. |
| **[#33890](https://github.com/anomalyco/opencode/issues/33890) — Bun 1.3.14 segfault (SIGILL) on Linux** | TUI crashes on AMD EPYC (Zen4, AVX‑512). Critical stability issue for high‑end servers. | 6 comments · 5 👍. Upstream Bun / WASM dependency. |
| **[#33213](https://github.com/anomalyco/opencode/issues/33213) — Server mode heap/swap accumulation** | `opencode serve` grows to 26.8 GiB cgroup peak over ~1.5 days. Requires restart. | 5 comments. Major concern for production server deployments. |
| **[#34228](https://github.com/anomalyco/opencode/issues/34228) — Inconsistent project skills exposure** | Agent sees a different subset of 35 configured skills between sessions. Undermines agent reliability. | 5 comments. Fresh report, likely to see more traction. |
| **[#34030](https://github.com/anomalyco/opencode/issues/34030) — Can't invoke enterprise Copilot third‑party models** | Enterprise GitHub Copilot accounts add custom models, but OpenCode can't discover or use them. | 4 comments. Enterprise readiness gap. |

## 4. Key PR Progress

| PR | Description | Impact |
|---|---|---|
| **[#34273](https://github.com/anomalyco/opencode/pull/34273)** | `feat(tools): add agent tools` — adds git, format, diagnostics, memory/history, LSP rename + TUI spinner fix (Angelo17123) | Major extension of agent native capabilities. |
| **[#33202](https://github.com/anomalyco/opencode/pull/33202)** | `fix(agent): skip parseModel when model is "inherit"` — unblocks custom `.md` subagents (yjlc‑pc) | Closes **five** open issues (#17890, #31141, #5623, #8896, #23908). |
| **[#34272](https://github.com/anomalyco/opencode/pull/34272)** | `fix: add final empty-content guard in message() pipeline` (Oxygen56) | Provider‑agnostic fix for empty‑content crashes (#23260, #26320). |
| **[#34242](https://github.com/anomalyco/opencode/pull/34242)** | `fix(tui): prevent piped stdin from breaking UI and keyboard input` (LordMikkel) | Closes four long‑standing bugs (#28538, #24195, #3871, #6220). |
| **[#34256](https://github.com/anomalyco/opencode/pull/34256)** | `fix(server): reject foreign directory hints before instance lookup` (romanilyin) | Directly addresses the WSL path breakage (#34255, #30895, #19473). |
| **[#34234](https://github.com/anomalyco/opencode/pull/34234)** | `fix: preserve attachment file paths` (jparradog) | Agents can now access pasted files via filesystem path (#23801, #17488). |
| **[#34233](https://github.com/anomalyco/opencode/pull/34233)** | `feat(app): v2 wsl ui` (arvsrn) | Dedicated WSL UI for the desktop app, including new loader components. |
| **[#34227](https://github.com/anomalyco/opencode/pull/34227)** | `fix(console): account for partial Zen refunds` (opencode-agent[bot]) | Improves billing accuracy by tracking actual refund amounts. |
| **[#34263 / #34264](https://github.com/anomalyco/opencode/pull/34263)** | `feat(tui): undo/redo/revert + session rename` (thdxr) | Wires V2 staged‑revert API into TUI; adds session renaming end‑to‑end. |
| **[#29881](https://github.com/anomalyco/opencode/pull/29881)** | `fix(tui): add wl-paste text read for Wayland systems` (zackslash) | Fixes Ctrl+V on Wayland by adding `wl-paste` support. |

## 5. Feature Request Trends

- **LLM‑ready documentation**: The `llms.txt` request ([#8816](https://github.com/anomalyco/opencode/issues/8816)) is the top‑voted open feature. Users want to feed OpenCode’s own docs directly into their coding workflows.
- **Payment flexibility**: Multiple users (24 👍) are asking for cryptocurrency payments ([#23153](https://github.com/anomalyco/opencode/issues/23153)), indicating an expectation of decentralized billing.
- **Enterprise & alternative providers**: Issues about enterprise Copilot accounts ([#34030](https://github.com/anomalyco/opencode/issues/34030)) and NVIDIA NIM model gaps ([#34177](https://github.com/anomalyco/opencode/issues/34177), [#34026](https://github.com/anomalyco/opencode/issues/34026)) show demand for total provider freedom.
- **Deeper agent tooling**: The community wants richer built‑in agent tools (git, diagnostics, LSP). PR [#34273](https://github.com/anomalyco/opencode/pull/34273) aligns with this trend.
- **Desktop UX polish**: Requests for sticky session headers, configurable tool output, and dedicated WSL UIs show the desktop app is a major focus area.

## 6. Developer Pain Points

- **❯ WSL / Windows path instability**: The desktop app sending UNC paths to WSL hosts ([#19473](https://github.com/anomalyco/opencode/issues/19473), [#30895](https://github.com/anomalyco/opencode/issues/30895)) remains the single biggest platform friction point. Fixes are in progress (#34256).
- **❯ Memory leaks & long‑session degradation**: `MaxListenersExceededWarning` ([#22422](https://github.com/anomalyco/opencode/issues/22422)), server‑mode 26 GiB heap accumulation ([#33213](https://github.com/anomalyco/opencode/issues/33213)), and mid‑session freezes ([#34214](https://github.com/anomalyco/opencode/issues/34214)) are recurring pain points for power users.
- **❯ Provider & model brittleness**: Sessions break when the agent triggers image input on a non‑vision model ([#34113](https://github.com/anomalyco/opencode/issues/34113)), NVIDIA NIM requests hang ([#34026](https://github.com/anomalyco/opencode/issues/34026)), and prompt cache drops to 0 on GLM‑5.1 ([#31348](https://github.com/anomalyco/opencode/issues/31348)). Provider‑agnostic robustness is lacking.
- **❯ Agent inconsistency**: The silent model‑selection revert ([#34207](https://github.com/anomalyco/opencode/issues/34207)) and unstable skills exposure ([#34228](https://github.com/anomalyco/opencode/issues/34228)) erode user trust in the agent’s operational determinism.
- **❯ Cross‑platform edge cases**: ARM64 TUI crash ([#19130](https://github.com/anomalyco/opencode/issues/19130)), Wayland paste ([#29881](https://github.com/anomalyco/opencode/issues/29881)), and macOS NFS kernel messages leaking into the TUI ([#34146](https://github.com/anomalyco/opencode/issues/34146)) highlight the difficulty of supporting every platform flawlessly.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-28

## Today's Highlights
The Pi ecosystem saw a heavy day of extension API maturation and TUI bug squashing. On the extension side, critical gaps were closed with the landing of `reportUsage()` for cost tracking, a safe `ctx.reload()` deferral mechanism, and a new setting for external editor paths. The TUI received attention on multiple fronts, with fixes landing for screen flicker on parallel tool calls and Devnagri text breaking the layout, while a highly active discussion (34 comments) continues around streaming markdown forced-scrolling. The model landscape remains volatile: Together.ai deprecations land in two weeks, Azure model names were corrected, and the community flagged a malicious package in the nascent extension marketplace.

---

## Releases
**No new core releases in the last 24 hours.**

---

## Hot Issues — 10 Noteworthy Items

### 1. [#5825 — Streaming markdown forces scroll to bottom](earendil-works/pi Issue #5825) [OPEN]
**Situation:** While streaming markdown output, Pi forces the viewport to scroll to the bottom if `clear on shrink` is enabled, preventing users from reading earlier output as the model responds.
**Signal:** 34 comments — the most active issue today. A clear UX regression that frustrates users who read faster than the model types.
**Tags:** `bug`, high engagement

### 2. [#5763 — Providers swallow the HTTP error body](earendil-works/pi Issue #5763) [OPEN]
**Situation:** Behind a proxy/gateway, non-2xx error bodies are dropped by most providers, turning descriptive errors into opaque messages like `UnknownError` or `403 status code (no body)`.
**Signal:** Actively tracked alongside PR #5832. Enterprise user pain point.
**Tags:** `bug`, `inprogress`

### 3. [#6131 — Full screen redraw (flicker) on simultaneous tool calls](earendil-works/pi Issue #6131) [CLOSED]
**Situation:** When the model returns multiple tool calls in one turn, the TUI clears and redraws the entire screen, worsening as more tool call blocks accumulate.
**Signal:** Closed with a fix. Visual flicker is a high-urgency cosmetic defect for a TUI-first product.
**Tags:** `bug`, `untriaged`

### 4. [#6129 — Malicious Package Report: @hypabolic/pi-hypa](earendil-works/pi Issue #6129) [CLOSED]
**Situation:** Community report flagging a package that "gamed the system" with artificial install counts. The reporter noted that even without active malware, the exploitation of the install mechanism is unacceptable.
**Signal:** A critical signal for Pi's extension marketplace governance and trust-building.
**Tags:** `package-report`, ecosystem security

### 5. [#6130 — renderCall/renderResult silently ignore exceptions](earendil-works/pi Issue #6130) [CLOSED]
**Situation:** Custom renderers fail silently, causing developers to waste hours debugging hallucinated imports or logic errors. The reporter explicitly implored: *"please don't ignore exceptions"*.
**Signal:** Highlights a core expectation for extension developers: hard failures must be visible.
**Tags:** `bug`, extension DX

### 6. [#6124 — Devnagri words breaking the Pi harness](earendil-works/pi Issue #6124) [CLOSED]
**Situation:** Typing Devnagari script (e.g., `नेटवर्क`) completely breaks the TUI layout.
**Signal:** Closed with a fix. A critical i18n/unidirectional text rendering bug.
**Tags:** `bug`, internationalization

### 7. [#6127 — `--append-system-prompt` can't override default coding-agent identity](earendil-works/pi Issue #6127) [CLOSED]
**Situation:** Users running `pi --mode rpc` as a backend for custom agents cannot override the built-in coding-agent identity, even when passing a full identity via `--append-system-prompt`.
**Signal:** Blocks advanced use cases where Pi acts as a backend, not the frontend agent.
**Tags:** RPC, identity, configuration

### 8. [#6120 / #6119 — Extension API: reportUsage() to feed subagent costs into session footer](earendil-works/pi Issue #6120, PR #6119) [CLOSED]
**Situation:** Sub-agent extensions (like review agents) track token/cost usage internally but cannot report that data back to the main session footer.
**Signal:** Merged. A critical enabler for cost transparency when building complex agent chains.
**Tags:** `extension-api`, cost tracking

### 9. [#6121 — Allow extensions to execute registered tools](earendil-works/pi Issue #6121) [CLOSED]
**Situation:** Feature request from the author of a "codemode" extension (`pi-eval`) to allow TypeScript scripts in extensions to call Pi's registered tools.
**Signal:** Closed with implementation. Unlocks powerful meta-agent and automation patterns.
**Tags:** `extension-api`, tool execution

### 10. [#6105 — User messages get incorrectly escaped](earendil-works/pi Issue #6105) [CLOSED]
**Situation:** Typing a backslash `\` causes it to render as `"`, a basic text processing defect.
**Signal:** Reproducible with `pi --no-extensions`, indicating a core parsing issue.
**Tags:** `bug`, core parsing

---

## Key PR Progress — 8 PRs Analyzed

### 1. [#5735 — fix(coding-agent): defer extension reload requests safely](earendil-works/pi PR #5735) [OPEN]
**What:** Makes `ctx.reload()` safe for use from any extension context by deferring reloads to safe lifecycle boundaries via `AgentSession` coordination.
**Why it matters:** Extension stability. Prevents race conditions and crashes during self-reload.
**Tags:** `extension-api`, stability

### 2. [#5678 — Add excludeFromContext for custom messages](earendil-works/pi PR #5678) [OPEN]
**What:** Allows custom messages to be persisted and rendered in the UI but excluded from LLM context during conversion, compaction, and summarization.
**Why it matters:** Powerful new primitive. Extensions can display information without polluting the model's window.
**Tags:** `extension-api`, context management

### 3. [#5832 — fix(ai): surface provider HTTP error body instead of opaque SDK message](earendil-works/pi PR #5832) [OPEN]
**What:** Fixes #5763. Passes through the raw HTTP error body from proxy/gateway responses instead of dropping it.
**Why it matters:** Enterprise debugging. Turns "UnknownError" into actionable error messages.
**Tags:** `providers`, debugging

### 4. [#6123 — feat(coding-agent): add externalEditor setting for Ctrl+G](earendil-works/pi PR #6123) [CLOSED/MERGED]
**What:** Adds a `settings.json` option for the external editor path (`externalEditor`), bypassing locked `$VISUAL`/`$EDITOR` env vars on Windows/Git Bash.
**Why it matters:** Fixes a specific, long-standing Windows pain point. Restores Ctrl+G functionality.
**Tags:** `settings`, windows, DX

### 5. [#6119 — feat: add reportUsage API for extensions to contribute session cost](earendil-works/pi PR #6119) [CLOSED/MERGED]
**What:** Implements `pi.reportUsage(input)` to allow extensions to push token/cost data into the session footer and `/session` view.
**Why it matters:** Closes a major extension API gap. Enables accurate billing for multi-model agent pipelines.
**Tags:** `extension-api`, cost tracking

### 6. [#6115 — feat(coding-agent): add configurable chat padding](earendil-works/pi PR #6115) [OPEN, to-discuss]
**What:** A draft PR to add settings that control TUI padding, a frequent community request from Discord.
**Why it matters:** Signals maintainers are listening to TUI customization demand, while noting architectural complexity.
**Tags:** `tui`, customization

### 7. [#6099 — Rename Azure model key from 'gpt-5.2-chat-latest' to 'gpt-5.2-chat'](earendil-works/pi PR #6099) [CLOSED/MERGED]
**What:** Corrects the Azure OpenAI model key where `gpt-5.2-chat-latest` does not exist as a deployment option.
**Why it matters:** Prevents Azure users from hitting immediate "model not found" errors.
**Tags:** `providers`, `azure`, model mapping

### 8. [#6111 — fix(coding-agent): report settings write failures in install/remove](earendil-works/pi PR #6111) [CLOSED/MERGED]
**What:** Fixes #6112. `pi install` now surfaces a proper error and non-zero exit code when `settings.json` is read-only, instead of silently succeeding.
**Why it matters:** Eliminates a confusing silent failure that led users to believe extensions were active when they weren't.
**Tags:** `bug`, extension install, DX

---

## Feature Request Trends

**1. Extension API as Platform**
A coordinated push is underway to make Pi's extension system a first-class development platform. The cluster of issues and PRs around tool execution (#6121), cost reporting (#6120), stable session imports (#6117), and safe reload (#5735) all point to developers building complex, production-grade extensions that demand deep API access.

**2. Deep Configuration & Customization**
Users are demanding file-based configuration over environment variables. The `externalEditor` setting (#6122), `npmInstallArgs`/`npmUpdateArgs` (#6125, #6126), and chat padding configuration (#6115) all reflect a community that wants deterministic, portable, and shared config files over shell-dependent env vars.

**3. Model Agility**
The rapid churn of model issues (Together.ai deprecations #6132, Azure naming #6114, OpenCode thinking #6116, DiffusionGemma #6128, Qwen3.5 definitions #4106) indicates a highly engaged user base jumping on the latest models the day they drop. This creates a support burden for maintainers but also signals strong product-market fit for power users.

**4. Internationalization & Unicode**
The Devnagri bug (#6124) was closed quickly, but its very existence emphasizes the need for proper Unicode handling across the TUI stack as the user base globalizes.

---

## Developer Pain Points

**Silent Failures Dominate**
The loudest complaint this week is silencing. `renderCall/renderResult` swallowing exceptions (#6130), `pi install` silently skipping registration when `settings.json` is read-only (#6112), providers eating HTTP error bodies (#5763), and user messages being mangled (#6105). Each case robbed developers of hours. The community is clear: *prefer crash over silence.*

**TUI Jank and Responsiveness**
Multiple bugs hit the core user interface simultaneously: forced autoscroll (#5825), full-screen flicker on tool calls (#6131), and a total layout break on non-Latin input (#6124). For a TUI-native product, these issues erode confidence and professional polish quickly.

**Ecosystem Trust & Safety**
The @hypabolic/pi-hypa report (#6129) is a reminder that the extension marketplace is not immune to manipulation. With extension installs gamed and potential supply chain risk, the community is watching how Pi's curation and moderation evolves.

**Provider Integration Opacity**
Behind-the-scenes provider behavior remains a persistent debugging thicket. Models ignoring thinking settings (#6116), proxies swallowing errors (#5763), and incorrect model definitions (#4106, #6132) all force users to cross-reference multiple sources to understand failure modes. Surface-level error messages are still not trusted.

**Identity Management for RPC Users**
Using Pi as a backend for custom agents has a strong blocking issue: `--append-system-prompt` cannot reliably override the built-in coding identity (#6127). This limits architectural flexibility for teams wanting to embed Pi in custom agent frameworks.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code Community Digest for June 28, 2026.

---

## Qwen Code Community Digest — 2026-06-28

### 1. Today's Highlights
The project shipped `v0.19.2-nightly` with a `web_fetch` robustness fix, but the dominant community conversations center on **cost governance** and **session reliability**. A sharp uptick in discussions around silent model upgrades and prompt cache inefficiency signals growing user backlash against expensive default behaviors. On the development side, the `qwen tag` multiplayer agent feature and revamped daemon permissions signal a strong strategic push towards collaborative workflows.

### 2. Releases
- **[v0.19.2-nightly.20260628.714513df2](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.2-nightly.20260628.714513df2)**
  A minor nightly release anchored by a single core fix. The `web_fetch` tool now has a JSON fallback mode, improving compatibility when scraping endpoints that don't return traditional HTML. This is a targeted fix for developers relying on automated data fetching in their agentic workflows.

### 3. Hot Issues
1. **[#5942](https://github.com/QwenLM/qwen-code/issues/5942) – Anthropic Provider Prompt-Cache Misses** 🤯 *Cost*
   A deep-dive analysis reveals Qwen Code suffers avoidable cache misses on Anthropic endpoints where Claude Code does not. This directly inflates API costs per turn. *Why it matters:* A hard blocker for cost-sensitive teams. *Reaction:* 2 comments, but the technical depth from `xiaoliu10` has put the comparison with Claude Code on the roadmap.
2. **[#5819](https://github.com/QwenLM/qwen-code/issues/5819) – Model Auto-Upgrade Drains Credits** 💸 *Trust*
   User `aspnmy` reported that a silent upgrade switched their low-cost model to a premium tier, exhausting prepaid funds. *Why it matters:* A severe breach of user trust and a financial risk. *Reaction:* 4 comments, highly critical; the community is demanding explicit consent for billing-affecting config changes.
3. **[#5922](https://github.com/QwenLM/qwen-code/issues/5922) – `cua-driver.exe` High CPU on Idle** 🔥 *Windows Perf*
   The computer-use tool driver maintains high CPU usage even after the agent finishes. *Why it matters:* A significant platform-specific regression for Windows users that gives the tool the appearance of bloatware. *Reaction:* 3 comments, flagged as `P2`, `welcome-pr` open.
4. **[#5920](https://github.com/QwenLM/qwen-code/issues/5920) – `/rewind` Records Have Null `parentUuid`** 💥 *Data Integrity*
   The conversation history collapsed on resume because parent UIDs were serialized as null. *Why it matters:* Completely breaks session context, a critical core regression. *Reaction:* 3 comments; community member `KangHaiYue` quickly diagnosed the serialization flaw.
5. **[#5836](https://github.com/QwenLM/qwen-code/issues/5836) – Project-Local Todo & Memory Sync** 🔄 *Workflow*
   User `liyujiang-gzu` requests todos and memories be persistable inside the project directory for Git-based cross-device syncing. *Why it matters:* A top friction point for developers who switch machines. *Reaction:* 4 comments, strong consensus on blocking the feature gap.
6. **[#5941](https://github.com/QwenLM/qwen-code/issues/5941) – Scroll Jump During Streaming** 🖱️ *UX*
   Scrolling up while the model is generating content immediately jumps to the top of the output. *Why it matters:* A jarring UI regression that breaks the reading experience. *Reaction:* 2 comments, reported on Windows.
7. **[#5756](https://github.com/QwenLM/qwen-code/issues/5756) – Default 8K Output Cap Truncates Large Writes** ✂️ *Cost/Loops*
   The hard 8K cap forces the model into expensive retry loops when generating large files (e.g., wikis). *Why it matters:* Creates a "tax" on large output tasks. *Reaction:* 3 comments; directly contributed to the creation of fix PRs like [#5939](https://github.com/QwenLM/qwen-code/pull/5939).
8. **[#5889](https://github.com/QwenLM/qwen-code/issues/5889) – `.qwen/loop.md` Task File Injection** 🤖 *Automation*
   A proposal for a durable task file injected at fire time for `/loop`, allowing the user to edit long-running agent instructions mid-cycle. *Why it matters:* Essential for production-grade background automation. *Reaction:* 3 comments, seen as a necessary evolution of the cron/loop system.
9. **[#5867](https://github.com/QwenLM/qwen-code/issues/5867) – Git-Shared "Team" Tier for Auto-Memory** 👥 *Collaboration*
   Introduces a third tier of memory (USER / PROJECT / **TEAM**) that is git-shared for persistent team knowledge. *Why it matters:* A cornerstone for multi-developer adoption. *Reaction:* 3 comments, aligns with the strategic `qwen tag` direction.
10. **[#5909](https://github.com/QwenLM/qwen-code/issues/5909) – Harden Slug-to-Path Call Sites** 🛡️ *Security*
    Defense-in-depth audit for all remaining untrusted-name-to-filesystem-path conversions. *Why it matters:* Proactive security hardening prevents potential path traversal vulnerabilities. *Reaction:* 3 comments, part of a persistent security effort by `VectorPeak`.

### 4. Key PR Progress
1. **[#5888](https://github.com/QwenLM/qwen-code/pull/5888) – `feat(channels): qwen tag — Phase 0`** *(OPEN)*
   The headline architectural move. Introduces a channel-resident, multiplayer agent ("qwen tag") built on the existing daemon. This is the foundation for group-based AI workflows (DingTalk-first).
2. **[#5946](https://github.com/QwenLM/qwen-code/pull/5946) – `fix(core): Anthropic SDK abort listener leak`** *(CLOSED)*
   Critical stability fix. Wraps abort signals in per-request child controllers to prevent a growing listener leak that could cause memory bloat and erratic abort behavior.
3. **[#5944](https://github.com/QwenLM/qwen-code/pull/5944) – `fix(core): halt repeated shell inspection variants`** *(OPEN)*
   Directly addresses the "stuck agent" loop. Adds an always-on loop guard that detects repetitive read-only shell commands (e.g., `git status`, `git diff`) and halts the run.
4. **[#5856](https://github.com/QwenLM/qwen-code/pull/5856) – `feat(desktop): voice dictation`** *(OPEN)*
   Brings the `/voice` dictation feature to the desktop app, adding a microphone button with waveform visualization and recording controls, achieving full parity with the CLI and Web Shell.
5. **[#5912](https://github.com/QwenLM/qwen-code/pull/5912) – `fix(daemon): ACP permission votes across connections`** *(OPEN)*
   Fixes a core blocker for team use. Permission requests in the daemon were tied to single connections; this PR namespaces them so votes can be processed across different users/sessions.
6. **[#5868](https://github.com/QwenLM/qwen-code/pull/5868) – `feat(core): configurable auto-compact threshold`** *(OPEN)*
   Gives users control over the context window by allowing configuration of auto-compaction thresholds and Stop hook context usage. A direct response to context window frustration.
7. **[#5795](https://github.com/QwenLM/qwen-code/pull/5795) – `feat(core): enrich subagent crash notifications`** *(OPEN)*
   Improves agent resilience. When a sub-agent crashes, the parent agent now receives structured partial results and recent activity logs instead of a generic failure.
8. **[#5928](https://github.com/QwenLM/qwen-code/pull/5928) – `feat(config): todosDirectory setting`** *(OPEN)*
   Directly addresses feature request [#5836](https://github.com/QwenLM/qwen-code/issues/5836). Adds a `todosDirectory` setting allowing users to store task state inside the project directory for Git synchronization.
9. **[#5943](https://github.com/QwenLM/qwen-code/pull/5943) – `feat(web-shell): add error boundaries`** *(CLOSED)*
   Adds multiple layers of React error boundaries (generic, message-item, code-block) to the web-shell, ensuring a single render crash doesn't white-screen the entire embedded UI.
10. **[#5848](https://github.com/QwenLM/qwen-code/pull/5848) – `feat(ui): ui.history.collapsePreviewCount`** *(OPEN)*
    UX quality-of-life improvement. When resuming a collapsed session, users can now keep the most recent N turns visible, solving the "lost context" feeling on resume.

### 5. Feature Request Trends
- **Multi-User & Cross-Device State**: The strongest signal from the community is the demand for persistent, sharable state. Requests for git-shared team memory ([#5867](https://github.com/QwenLM/qwen-code/issues/5867)), project-local todos ([#5836](https://github.com/QwenLM/qwen-code/issues/5836)), and channel-resident agents ([#5888](https://github.com/QwenLM/qwen-code/pull/5888)) paint a clear picture: the community is ready to move from single-user tools to collaborative intelligence.
- **Cost-Control Infrastructure**: Users are done with passive cost management. They want hard constraints: vision model fallbacks ([#5597](https://github.com/QwenLM/qwen-code/issues/5597)), fixed model locking against upgrades ([#5819](https://github.com/QwenLM/qwen-code/issues/5819)), and observability into agent spending.
- **Background Automation Maturity**: The `/loop` and cron systems are hitting limitations. Users want durable task files that survive restarts ([#5889](https://github.com/QwenLM/qwen-code/issues/5889)) and the ability to see, edit, and cancel their scheduled tasks ([#5823](https://github.com/QwenLM/qwen-code/issues/5823)).
- **Ecosystem Parity**: Significant interest in Telegram bot completion ([#5907](https://github.com/QwenLM/qwen-code/issues/5907)) and a revival of the Chrome extension using the new daemon architecture ([#5936](https://github.com/QwenLM/qwen-code/issues/5936)), indicating users want Qwen Code everywhere they work.

### 6. Developer Pain Points
1. **Silent Cost Escalation (Trust Crisis)** 🚨
   The most acute pain point is the tool making decisions that silently increase billing. The model auto-upgrade bug ([#5819](https://github.com/QwenLM/qwen-code/issues/5819)) and broken prompt caching ([#5942](https://github.com/QwenLM/qwen-code/issues/5942)) have created a trust deficit regarding automated behaviors.
2. **The Looping Agent Problem** 🔄
   Despite existing guards, agents still frequently get stuck in tool loops—either from explicit `write_file` retries due to token caps ([#5756](https://github.com/QwenLM/qwen-code/issues/5756)) or implicit repeated shell inspections ([#5944](https://github.com/QwenLM/qwen-code/issues/5944)). Each loop wastes significant time and tokens.
3. **State Serialization Fragility** 💾
   The `/rewind` null UUID bug ([#5920](https://github.com/QwenLM/qwen-code/issues/5920)) exposed a low tolerance for state machine errors. Developers rely heavily on perfect session history; any data corruption is viewed as a critical incident.
4. **Windows Performance Gaps** 🪟
   Persistent reports of high CPU usage from the `cua-driver` ([#5922](https://github.com/QwenLM/qwen-code/issues/5922)) and clipping UI elements ([#5933](https://github.com/QwenLM/qwen-code/issues/5933)) suggest Windows is consistently under-served by the quality assurance process.
5. **Configuration Surprises** ⚙️
   Users expect deterministic configuration. Non-standard env parsing ([#5929](https://github.com/QwenLM/qwen-code/issues/5929)) and settings that silently change on upgrade ([#5819](https://github.com/QwenLM/qwen-code/issues/5819)) undermine the confidence developers need to rely on the tool in production.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest — 2026-06-28

**Source:** github.com/Hmbown/CodeWhale

---

## 1. Today's Highlights
The maintainers shipped a significant wave of infrastructure PRs—landing a **lightweight plugin system**, a **cache-maximal context mode**, and critical **ACP streaming/cancel fixes** for editor integrations. Simultaneously, the **v0.8.66 release ledger** ([#3707](https://github.com/Hmbown/CodeWhale/pull/3707)) was merged, formalizing the token/cache/context discipline targets that must be met before the release ships. Community pain over high token burn and low cache hit ratios remains intense (issues #1177, #1120, #743), but the volume of engine reliability fixes suggests the team is methodically closing the gap.

---

## 2. Releases
**None in the last 24 hours.** The v0.8.66 milestone is actively gated behind a scorecard tracked in the new release ledger. An official bin or npm release should not be expected until the maintainers are satisfied with the cache-hit and input-token benchmarks.

---

## 3. Hot Issues

1.  **[#1177 – 输入缓存命中率太低了 (Input cache hit ratio is too low)](https://github.com/Hmbown/CodeWhale/issues/1177)**
    *   **Why it matters:** Users report a “night and day” gap vs. competing tools that hit 95%+ cache rates. This directly drives API costs and is the top community complaint. *24 comments.*

2.  **[#1120 – There still seems to be some problems with cache hits](https://github.com/Hmbown/CodeWhale/issues/1120)**
    *   **Why it matters:** Bilingual report confirming cache misses persist despite earlier patch claims. Users are skeptical that the issue is fully understood. *21 comments.*

3.  **[#743 – token消耗增大了很多 (Token consumption has increased significantly)](https://github.com/Hmbown/CodeWhale/issues/743)**
    *   **Why it matters:** Reports of 400 million tokens burned in half a day. Points to excessive context re-injection and agent chattiness. *13 comments.*

4.  **[#3275 – CodeWhale is overly involved in making modifications, engaging in self-questioning and self-answering](https://github.com/Hmbown/CodeWhale/issues/3275)**
    *   **Why it matters:** A **critical trust regression**. The agent enters self-driven loops without user confirmation, deviating from the original request. Flagged as a regression from #3061. *12 comments.*

5.  **[#3568 – Plan and agent mode mixed up YET AGAIN](https://github.com/Hmbown/CodeWhale/issues/3568)**
    *   **Why it matters:** High-frustration recurrence—the agent ignores Plan mode and executes autonomously, breaking an MMR (Mode-Mixed Reaction) workflow. *6 comments, 1 👍.*

6.  **[#3495 – Adopt Moraine as CodeWhale's memory backend](https://github.com/Hmbown/CodeWhale/issues/3495)**
    *   **Why it matters:** Proposed architectural shift to a dedicated long-term memory layer (Moraine) with MCP recall tools, moving towards persistent, searchable agent memory.

7.  **[#3541 – Feature Request: Rust-based native runtime / desktop client](https://github.com/Hmbown/CodeWhale/issues/3541)**
    *   **Why it matters:** Represents community desire to shed Node.js overhead for lower latency and cold-start performance, a signal that platform maturity is expected.

8.  **[#1641 – Agent mode: add fallback strategy when tool calls fail](https://github.com/Hmbown/CodeWhale/issues/1641)**
    *   **Why it matters:** The agent currently retries failing external tools endlessly until total failure. Users need graceful degradation or alternative tool switching. *3 comments.*

9.  **[#528 – Cache-maximal context mode: re-read active files instead of summarizing](https://github.com/Hmbown/CodeWhale/issues/528)**
    *   **Why it matters:** Core principle shift—leverage cheap V4 caching to keep full file context instead of compressing/forgetting. The PR (#3697) just landed, making this a high-interest tracking issue.

10. **[#3638 – Exposed main prompt for broader use cases (e.g., creative writing)](https://github.com/Hmbown/CodeWhale/issues/3638)**
    *   **Why it matters:** Signals expansion of the user base beyond software engineering. The PR (#3696) just merged, allowing system prompt overrides from config.

---

## 4. Key PR Progress

1.  **[#3710 / #3708 / #3699 / #3692 – Plugin System Infrastructure](https://github.com/Hmbown/CodeWhale/pull/3710)**
    *   **What:** A layered rollout of a modular plugin system: TOML manifest parsing, filesystem discovery, registry lifecycle, and prompt injection. Includes a built-in `rust-toolkit` example.

2.  **[#3696 – Allow overriding the base prompt from the config directory](https://github.com/Hmbown/CodeWhale/pull/3696)**
    *   **What:** Closes the core of #3638. Users can now swap the base/constitutional system prompt from a config file, unblocking non-coding use cases (writing, document review).

3.  **[#3702 – Stream session/prompt deltas as session/update chunks](https://github.com/Hmbown/CodeWhale/pull/3702)**
    *   **What:** Fixes ACP buffering for editors (Zed). Agents now stream output incrementally instead of waiting for the full turn to complete.

4.  **[#3698 – Cancel in-flight session/prompt on session/cancel](https://github.com/Hmbown/CodeWhale/pull/3698)**
    *   **What:** Critical fix for the ACP protocol. The read loop no longer blocks on a provider turn, allowing cancellation signals to be processed immediately.

5.  **[#3697 – Cache-maximal context mode: materialize active file contents](https://github.com/Hmbown/CodeWhale/pull/3697)**
    *   **What:** Implements the core architecture of #528. An opt-in mode now injects full file contents for the top active paths into the context, reducing tool-call overhead.

6.  **[#3705 / #3703 / #3701 – Engine fallback strategies for failed tool calls](https://github.com/Hmbown/CodeWhale/pull/3705)**
    *   **What:** Addresses #1641 across three PRs. Adds model-visible fallback hints for transient errors, repeated search failures, and generic timeouts.

7.  **[#3700 – Emit hunt verdict mapping for verifier](https://github.com/Hmbown/CodeWhale/pull/3700)**
    *   **What:** Wires the verifier to structured output: `pass/partial/fail → hunted/wounded/escaped`. Adds trophy metadata enforcement and audit details.

8.  **[#3707 – Add v0.8.66 release ledger](https://github.com/Hmbown/CodeWhale/pull/3707)**
    *   **What:** Registers the formal release scorecard: token/cache benchmarks, ACP registry status, and changelog updates. Acts as the gate document for the next release.

9.  **[#3607 – Reactivate stale issue cleanup](https://github.com/Hmbown/CodeWhale/pull/3607)**
    *   **What:** Re-establishes an automated stale policy for `bug` + `needs-info` issues, preventing the backlog from growing unbounded.

10. **[#3704 / #3684 – CI hardening and docs fixes](https://github.com/Hmbown/CodeWhale/pull/3704)**
    *   **What:** Ensures required CI checks (`Lint`, `Test`, `Smoke`) run even on docs-only PRs, and fixes stale file paths in contribution guides to prevent onboarding friction.

---

## 5. Feature Request Trends

- **Plugin & MCP Ecosystem:** The community is strongly aligned behind a formal plugin system and MCP (Model Context Protocol) integration. The rapid landing of the plugin system suggests the maintainers agree this is a critical extensibility vector. Requests for ACP Registry listing ([#3192](https://github.com/Hmbown/CodeWhale/issues/3192)) and Moraine-backed memory ([#3495](https://github.com/Hmbown/CodeWhale/issues/3495)) fall under this umbrella.

- **Cache-Maximal & Token Discipline:** Users are begging for smarter context handling. The "Cache-maximal context mode" (#528) is now implemented, but requests for **shell-only benchmark profiles** ([#2954](https://github.com/Hmbown/CodeWhale/issues/2954)), **prompt slimming** ([#2953](https://github.com/Hmbown/CodeWhale/issues/2953)), and **reduced transcript repetition** ([#2956](https://github.com/Hmbown/CodeWhale/issues/2956)) show this is the single biggest community-wide concern.

- **Non-Coding & Custom Workflows:** A clear cohort wants to repurpose CodeWhale for generative writing, roleplaying, or document analysis. The merged prompt-override PR (#3696) is a direct response to this demand. Chinese-language skill optimization ([#3354](https://github.com/Hmbown/CodeWhale/issues/3354)) is a specific sub-request.

- **Native Performance:** A vocal minority is asking for a **Rust-native desktop client** ([#3541](https://github.com/Hmbown/CodeWhale/issues/3541)) to eliminate the Node.js startup and memory overhead, signaling that some users see the TS/Node runtime as a scaling bottleneck for long-running agent sessions.

---

## 6. Developer Pain Points

- **Exorbitant Token Consumption:** The #1 source of frustration. Users report burning through huge token budgets due to verbose agent loops, excessive context re-injection, and a lack of compaction. Issues #743 (400M tokens / half day) and #1818 are the most extreme examples of a widespread problem.

- **Poor Cache Hit Ratios:** Directly tied to costs. The community has benchmarked competitors at 95%+ cache hit rates and is losing patience with CodeWhale's performance (issues #1177, #1120, #1747). This feels like a solved problem elsewhere.

- **Agent Autonomy Violations:** Users do not trust the agent to stay in its lane. The self-dialogue loops in #3275 and the persistent Plan/Agent mode confusion in #3568 are making developers reluctant to let the agent run unattended, defeating the purpose of an autonomous TUI.

- **Lack of Graceful Error Recovery:** When external tools (web search, API calls) fail, the agent spins its wheels until task failure. The community wants intelligent fallback chains or degradation paths, not raw error text or infinite retries (issue #1641).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*