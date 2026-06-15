# AI CLI Tools Community Digest 2026-06-15

> Generated: 2026-06-15 03:56 UTC | Tools covered: 9

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
**Date:** 2026-06-15  
**Focus:** Community sentiment, stability, feature direction

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem on June 15, 2026, is marked by an acute tension between rapid infrastructure investment and escalating stability and cost-control crises. While OpenAI Codex ships async hooks runtimes and Qwen Code lands session-persistence features, the dominant community signals across tools like Claude Code and Gemin CLI are uncontrolled agent costs, platform-specific regressions, and sandbox security failures. The ecosystem is bifurcating: first-party tools (Claude Code, Codex, CodeWhale) are grappling with scaling pain from adoption velocity, while extensibility-focused tools (Pi, OpenCode) are building deep plugin and provider architectures. Windows remains the ecosystem's persistent weak link, with six of eight major tools reporting platform-specific breakage in this cycle.

---

## 2. Activity Comparison

| Tool | Notable Issues | Notable PRs | Release (Last 24h) | Dominant Activity Theme |
|---|---|---|---|---|
| Claude Code | 10 | 5 | None | Cost and reliability crisis (subagent recursion, billing errors, kernel leaks) |
| OpenAI Codex | 10 | 10+ | None | Infrastructure shipping (async hooks, MCP timeouts, rate-limit APIs) |
| Gemini CLI | 10 | 10 | None | Dependency modernization (53 packages, Puppeteer v25, GenAI SDK v2) |
| Copilot CLI | 6 | 0 | None | Triage and stability consolidation |
| Kimi Code | 3 | 4 | None | Service credibility defense (rate limiting, feature gaps) |
| OpenCode | 10 | 10 | v1.17.7 *(Yesterday)* | Post-release regression firefighting (EditBuffer, terminal freeze) |
| Pi | 10 | 10 | None | Contributor pipeline thriving (extension APIs, profiling, Grok auth) |
| Qwen Code | 10 | 10 | None | Security hardening and session persistence |
| CodeWhale | 10 | 10 | v0.8.60 *(Recent)* | Rebrand turbulence, pre-stabilization tension |

*Note: Issue and PR counts reflect noteworthy items curated in each digest, not absolute repository volume.*

---

## 3. Shared Feature Directions

**Cost Control & Usage Transparency** *(6 tools)*
- **Claude Code** (#68430, #32544): Subagent recursion costing unbounded tokens, billing errors
- **OpenAI Codex** (#15281): CLI `/status` lacks token counts, model names, reset windows
- **OpenCode** (#9545, #28846): Unified OAuth usage tracking, demand for DeepSeek price pass-through
- **Pi** (#5722, #5738): Per-model compaction limits, Anthropic cache pricing fix
- **Qwen Code** (#5118, #4564): Per-task token breakdowns, `/stats` cost command
- **CodeWhale** (#3066): Cost tracking broken for all non-DeepSeek models

**Agent Observability & Steering** *(6 tools)*
- **CodeWhale** (#3102, #2666): Agents need formal clarification questions, resource budget visibility
- **Claude Code** (#68430): Uninterruptible subagent spawning
- **Gemini CLI** (#22323, #21409): False success reports, agent hangs
- **Kimi Code** (#2451): System prompt overrides user instructions
- **Pi** (#5687): CLI functions hang on MCP extensions
- **Qwen Code** (#4943): Safe mode `--safe-mode` flag being added

**Platform Stability & Parity** *(6 tools)*
- **Windows:** OpenAI Codex (#27979, #28103, crash loops/WSL binary), Pi (#5103, Git bash detection), Kimi Code (#2018, Alt+V paste), Qwen Code (#4218, MCP tools), CodeWhale (#1812, TUI freeze)
- **macOS:** Claude Code (#66020, kernel zone leak), OpenAI Codex (#27536, `code_sign_clone` 62GB+ leak)
- **Linux:** CodeWhale (#1067, glibc 2.39 incompatibility)

**Project-Level Context Automation** *(4 tools)*
- **Kimi Code** (#850, closed without implementation): Auto-load `AGENTS.md` / `.cursorrules`
- **Claude Code** (implied by `CLAUDE.md` ecosystem)
- **Qwen Code** (`QWEN.md` always-loaded warnings, #5073)

**MCP Standardization & Security** *(4 tools)*
- **OpenCode** (#28567, #31778): Full spec demand (Roots, Sampling), env leak prevention
- **OpenAI Codex** (#28234): MCP timeout increases (120s → 300s)
- **Pi** (#5687): CLI hang on MCP-infused extensions
- **Gemini CLI** (#27730): JSON array compliance in `structuredContent`

---

## 4. Differentiation Analysis

| Tool | Core Competitive Angle | Current Weakness |
|---|---|---|
| **Claude Code** | Highest raw coding competency perception | Cost predictability crisis, macOS kernel instability |
| **OpenAI Codex** | Enterprise infrastructure investment (hooks, rate-limit API, managed settings) | Windows update regressions, session corruption |
| **Gemini CLI** | Evaluation quality focus, AST-aware code manipulation | Sub-agent reliability, danger-prone model behavior |
| **Copilot CLI** | Native GitHub/Azure DevOps integration | Stale feature pipeline, session poisoning vulnerability |
| **Kimi Code** | Project-context loading, service simplicity | Trust deficit (rate limiting), competitive parity gaps |
| **OpenCode** | Universal provider/MCP client, session management | Release stability regression, plugin env safety |
| **Pi** | Extensibility platform (extension APIs, profiling, safe reload) | Windows host fragility, dependency duplication |
| **Qwen Code** | Security sandbox rigor, session persistence, CI maturity | Context window exhaustion, provider configuration confusion |
| **CodeWhale** | Multi-agent orchestration vision (WhaleFlow) | Stability crisis, rebrand migration friction |

---

## 5. Community Momentum & Maturity

**Rapid Iteration / High Engagement**
- **Claude Code**: Despite the cost/security crisis, the bounty program ($29–$200 per fix) and PR throughput indicate a deeply invested user base. Highest-urgency issue volume.
- **OpenCode**: v1.17.7 released yesterday; regressions are reported and developers are jumping on them (PRs for terminal reset, OAuth cleanup, subagent context). Fast feedback loop.
- **Pi**: The strongest contributor pipeline. High-quality architectural PRs (extension guidelines API #5711, safe reload #5735, Grok OAuth #5714, profiling #5731) confirmed in a single day cycle.

**Infrastructure & Enterprise Maturity**
- **OpenAI Codex**: Largest cross-platform investment; shipping managed workspace features, MCP infra, and async hooks. Enterprise adoption signals strongest here.
- **Gemini CLI**: Deep infrastructure focus (dependency hygiene, evaluation, auto-memory hardening). Slower feature velocity but lower technical debt buildup.
- **Qwen Code**: Security-first engineering (safe mode, contract probes, CI pipeline fixes). Strong session persistence investment.

**Struggling / Consolidating**
- **Kimi Code**: Smallest issue volume, weakest community signal. Rate-limit trust gap (#2123) and outdated feature set (#850 closed without implementation) suggest risk of user attrition.
- **Copilot CLI**: No code changes today. Critical session poisoning bug (#3791) suggests deep stability work, but the ecosystem feels quiet relative to peers.
- **CodeWhale**: Rebrand turbulence (DeepSeek → CodeWhale). High vulnerability (stability crisis, Linux distro lockout). Users "abandoning the tool" per digest quotes.

---

## 6. Trend Signals

1. **Autonomous Agent Cost Control is the Defining Challenge**  
   Uncontrollable token burn from recursive subagent spawning (Claude Code #68430, #68110) and task loops (Qwen Code #3184) is the ecosystem's most urgent unsolved problem. The community is demanding explicit depth limits, kill-switches, and per-task cost dashboards. Tools that deliver robust cost governance will capture professional trust.

2. **Windows Parity is a Market Opportunity**  
   Every major tool except Copilot CLI has a Windows-specific breaking bug or missing feature in this digest cycle. The ecosystem is leaving significant market share on the table. The first tool to deliver first-class Windows support (WSL deep integration, native clipboard, TUI stability) gains a structural advantage.

3. **MCP is the Standard, But Security Lags**  
   MCP adoption is accelerating across Codex, OpenCode, Pi, and Gemini CLI, but best practices for subprocess isolation, credential management, and OAuth resource release are still catching up. Environment variable leakage (OpenCode #31778) and hung CLI processes (Pi #5687) indicate the spec is ahead of secure implementations.

4. **Context Management Moves From Unlimited to Intelligent**  
   The community is shifting from demanding larger context windows to demanding smarter context utilization: AST-aware file operations (Gemini CLI #22745), external context querying (OpenCode RLM #11829), `excludeFromContext` flags (Pi #5654), and prompt guideline APIs (Pi #5710). Tools ignoring context hygiene are seeing "max_tokens" errors dominate their bug trackers.

5. **Multi-Provider Economics Drive Architectur**  
   The DeepSeek price reduction catalyzed community pressure on OpenCode (#28846), while Pi, CodeWhale, and Kimi Code are all adding non-standard providers. Users want OAuth-based, BYOK-ready, auto-failover provider chains. Vendor lock-in is actively resisted by the professional community.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the Claude Code Skills ecosystem based on the anthropics/skills repository activity as of 2026-06-15.

---

## Top Skills Ranking

**Based on community discussion levels and implied engagement velocity:**

### 1. Agent-Creator Meta-Skill (PR #1140)
- **Status:** Open | Author: `SyedaQurratAI`
- **Functionality:** Generates task-specific agent sets. Critically bundles the fix for multi-tool parallel evaluation crashes and Windows `%APPDATA%` compatibility.
- **Discussion:** This PR has absorbed the highest volume of traffic due to its role as a vehicle for fixing the `run_eval` pipeline (addressing Issue #1120). The community sees agent bootstrapping as the next logical step for the ecosystem.
- [View PR #1140](https://github.com/anthropics/skills/pull/1140)

### 2. Document Typography (PR #514)
- **Status:** Open | Author: `PGTBoos`
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and list numbering misalignment in AI-generated documents.
- **Discussion:** Unusually broad appeal because this flaw is visible in every long-form Claude document. The skill is popular as a "set it and forget it" quality layer for all document generation.
- [View PR #514](https://github.com/anthropics/skills/pull/514)

### 3. ODT Skill (PR #486)
- **Status:** Open | Author: `GitHubNewbie0`
- **Functionality:** Full lifecycle management for OpenDocument Format (.odt, .ods)—creation, template filling, conversion to HTML.
- **Discussion:** Addresses a hard enterprise barrier. European public sector and LibreOffice-heavy organizations explicitly require ISO-standard ODF support. High strategic value for team onboarding.
- [View PR #486](https://github.com/anthropics/skills/pull/486)

### 4. Meta-Skill Analyzers (PR #83)
- **Status:** Open | Author: `eovidiu`
- **Functionality:** Two meta-skills (`skill-quality-analyzer` and `skill-security-analyzer`) that evaluate other skills across structure, documentation, resources, clarity, and security dimensions.
- **Discussion:** Represents the ecosystem's self-regulation impulse. Directly ties into the security concerns raised in Issue #492 regarding namespace trust and malicious skill detection. High signal as a marketplace maturity milestone.
- [View PR #83](https://github.com/anthropics/skills/pull/83)

### 5. Testing Patterns (PR #723)
- **Status:** Open | Author: `4444J99`
- **Functionality:** Comprehensive testing skill covering unit testing (AAA pattern), React component testing, and end-to-end flow philosophy.
- **Discussion:** Universally applicable skill bridging code generation and production-quality QA. The community has independently validated this as a daily-driver skill that covers a persistent gap in LLM coding workflows.
- [View PR #723](https://github.com/anthropics/skills/pull/723)

### 6. SAP-RPT-1-OSS Predictor (PR #181)
- **Status:** Open | Author: `amitlals`
- **Functionality:** Steers SAP's open-source tabular foundation model for predictive analytics on business data.
- **Discussion:** Signals demand for domain-specific, locally-inferred models orchestrated by Claude. Appeals to the enterprise analytics cohort and demonstrates a pattern for other enterprise LLM integrations.
- [View PR #181](https://github.com/anthropics/skills/pull/181)

### 7. Codebase Inventory Audit (PR #147)
- **Status:** Open | Author: `p19dixon`
- **Functionality:** Systematic 10-step workflow scanning for orphaned code, unused files, documentation gaps, and infrastructure bloat; outputting a `CODEBASE-STATUS.md`.
- **Discussion:** Widely praised for its structured approach. Validated as an effective pattern for complex, multi-step skill design. Resonates strongly with teams managing legacy systems and technical debt.
- [View PR #147](https://github.com/anthropics/skills/pull/147)

### 8. Shodh-Memory (PR #154) / AURELION Suite (PR #444)
- **Status:** Open | Authors: `varun29ankuS`, `Chase-Key`
- **Functionality:** Persistent context systems. Shodh-Memory provides proactive memory retrieval across conversations. AURELION provides a structured 5-floor cognitive architecture for professional knowledge management.
- **Discussion:** Represents the frontier of skill complexity—introducing statefulness and architectural layering. The community is actively debating appropriate scope for individual skills, but the demand for durable agentic memory is unambiguous.
- [View PR #154](https://github.com/anthropics/skills/pull/154) | [View PR #444](https://github.com/anthropics/skills/pull/444)

---

## Community Demand Trends

*Derived from the top commented Issues:*

1. **Enterprise Distribution and Fleet Management**
   - Issue #228 (*14 comments, 7 👍*) is the single highest-comment issue. The community is frustrated by the manual "download, Slack/Teams, upload" workflow for skill sharing. There is an urgent demand for org-wide libraries or direct sharing links. This is paired with security concerns (#492, #1175) about namespace trust and permission boundaries.

2. **Critical `skill-creator` Pipeline Breakdown**
   - Issues #556 and #1169 report that `run_eval.py` consistently logs 0% recall across all queries, rendering the description optimization loop (used by `run_loop.py` and `improve_description.py`) completely non-functional. This is the ecosystem's most urgent operational bug. Windows compatibility (#1061) compounds this for a significant user segment.

3. **Security and Trust Boundary**
   - Issue #492 raised a critical alert: community skills are distributed under the `anthropic/` namespace, creating a trust boundary vulnerability where users might grant elevated permissions to unofficial skills. The community is actively demanding marketplace governance and clear brand separation.

4. **Platform Portability**
   - Issues #29 (AWS Bedrock support) and #16 (Expose Skills as MCPs) show the community wants skills to escape the Claude Desktop/CLI container. MCP exposure is seen as the protocol-level path to wider interoperability.

5. **Stability and Durability**
   - Issues #62 and #61 report skills arbitrarily disappearing or returning 404 errors. These substack-level stability issues erode confidence in the skill storage layer and are a prerequisite complaint for any adoption beyond early adopter phase.

---

## High-Potential Pending Skills

*These Skill PRs have active development momentum or broad community support and are positioned to land soon:*

- **Agent-Creator (PR #1140):** High priority because it unblocks the meta-agent workflow and fixes the multi-tool eval crash.
- **Document Typography (PR #514):** Universally applicable; lowest friction for merging given broad pain point consensus.
- **ODT Skill (PR #486):** Fills a hard enterprise requirement gap. Expected to be fast-tracked for partnered deployments.
- **Testing Patterns (PR #723):** Cleanly architected; high immediate utility for the core engineering audience.
- **Codebase Inventory Audit (PR #147):** Mature workflow proposal; well-structured for acceptance.
- **Meta-Skill Analyzers (PR #83):** Strategically important for ecosystem governance and security self-policing.

---

## Skills Ecosystem Insight

The community's most concentrated demand is simultaneously infrastructural—urgently requiring a reliable, cross-platform developer toolchain and enterprise-grade distribution, security, and governance—and aspirational, pushing toward durable agentic architectures (memory systems, cognitive frameworks) and professional-grade output quality (typography, testing, formal document standards) that move skills from experiments to production assets.

---

**Claude Code Community Digest — 2026-06-15**

---

### 1. Today's Highlights
This week’s digest is dominated by urgent stability and cost-control regressions. Critical bugs involving unbounded recursive subagent spawning and macOS kernel resource leaks have sparked widespread concern, while a long-standing feature request for India-specific pricing continues to dominate community engagement. No new releases are available yet to address these issues, leaving developers in a watch-and-wait stance.

---

### 2. Releases
No new releases were published in the last 24 hours.

---

### 3. Hot Issues

1. **[#53940: Cowork Edit/Write tools silently truncate files](https://github.com/anthropics/claude-code/issues/53940)** — A deterministic data-loss bug where a byte-conservation buffer cap silently truncates files of any size. The community has provided full reproduction steps, making this a high-severity integrity risk for agent-driven edits.

2. **[#17432: Feature Request—India-Specific Pricing Plans (INR)](https://github.com/anthropics/claude-code/issues/17432)** — The single most upvoted issue (442 👍, 194 comments). Users are demanding parity with OpenAI and Google, who already offer local-currency pricing. This is shaping up as a major market-access blocker for the Indian developer ecosystem.

3. **[#41458: `cleanupPeriodDays: 99999` ignored—490 sessions deleted](https://github.com/anthropics/claude-code/issues/41458)** — A regression where explicit retention settings are silently overridden, causing large-scale session loss. Users are rightly concerned about configuration reliability.

4. **[#32544: Extra charges despite available plan capacity](https://github.com/anthropics/claude-code/issues/32544)** — Reports of over-billing paired with false rate-limit errors. Trust in the cost model is being actively eroded, especially for heavy users depending on predictable subscription pricing.

5. **[#68430: CRITICAL—Subagents recursively spawn 50+ levels deep](https://github.com/anthropics/claude-code/issues/68430)** — Agents ignore `CLAUDE_CODE_FORK_SUBAGENT=0`, trigger infinite recursion, and burn tokens catastrophically. Permission denials trigger further agent spawning instead of halting. This is a critical cost and resource control failure.

6. **[#68110: General-purpose sub-agents cause exponential fan-out](https://github.com/anthropics/claude-code/issues/68110)** — Complements #68430 by isolating the `general-purpose` agent type as a danger vector. Without depth or count limits, a single task can cascade into massive unbilled token consumption.

7. **[#66020: macOS kernel zone leak (`data.kalloc.1024`) from CLI](https://github.com/anthropics/claude-code/issues/66020)** — A deep system-level bug. The CLI leaks kernel memory at a rate of up to 1,027/sec under load, eventually causing OS panics at ~20 GB. Developers are calling this a reliability blocker for macOS as a host platform.

8. **[#63870: Bash tool calls emitted as raw `<invoke>` text](https://github.com/anthropics/claude-code/issues/63870)** — Tool calls are being printed as plaintext instead of executed. The result is a completely non-functional agent in affected sessions.

9. **[#59823: Billing confusion around `remote-control` June 15th deadline](https://github.com/anthropics/claude-code/issues/59823)** — A documentation issue with financial stakes: unclear classification of `claude remote-control` usage under the new subscription plans taking effect today.

10. **[#66192: Copy-paste broken on macOS TUI](https://github.com/anthropics/claude-code/issues/66192)** — A fundamental usability regression. Copy-paste is a minimal expectation for command-line tooling, and its breakage is causing measurable friction for macOS users.

---

### 4. Key PR Progress

1. **[#43598: Add upstream issue sync workflow](https://github.com/anthropics/claude-code/pull/43598) (CLOSED)** — Merged a script to fetch and normalize upstream issues, improving cross-repository issue management.

2. **[#68423: Fix sweep script—don't auto-close assigned issues](https://github.com/anthropics/claude-code/pull/68423) (OPEN)** — Addresses a workflow logic gap where `markStale` correctly skips assigned issues but `closeExpired` still closes them. Important for maintainer workflow integrity.

3. **[#67699: Fix—Claude autonomously ran background scripts calling paid external API](https://github.com/anthropics/claude-code/pull/67699) (OPEN)** — A community-submitted bounty fix ($29) for a critical security/cost bug (#67654). Highlights the value of the bounty program for catching costly regressions.

4. **[#67409: Fix—Account downgraded due to billing error](https://github.com/anthropics/claude-code/pull/67409) (OPEN)** — Another bounty-driven fix ($200) addressing a billing logic bug that incorrectly downgraded user accounts. Reflects community urgency around payment reliability.

5. **[#67722: Claude dedupe issues workflow](https://github.com/anthropics/claude-code/pull/67722) (CLOSED)** — Adds a GitHub Actions workflow to automatically detect and manage duplicate issues, a practical response to the growing volume of incoming reports.

---

### 5. Feature Request Trends

- **Regional Pricing & Payment Flexibility:** The overwhelming signal is the demand for India-specific INR pricing (#17432). The community expects global pricing parity with OpenAI and Google.
- **Granular Agent and Cost Control:** Users want per-message model selection (#68165), explicit subagent depth limits (implied by the #68430 crisis), and the ability to set working directories for subagents (#12748).
- **Rich Desktop Integration:** Inspired by OpenAI Codex's "Appshots," users are requesting full-window text capture via macOS accessibility APIs (#68498) to provide richer context without manual copying.
- **Localization & UX Polish:** Requests for respecting the user's timezone (#64988) and scoping the main screen to the current project directory (#68495) show a desire for mature, context-aware local behavior.
- **Model Provider Flexibility:** Users relying on third-party API providers are seeing auto-compact breakage (#65585), and agent teams ignore configured models (#68411), pointing to a need for better multi-provider and model-override support.

---

### 6. Developer Pain Points

- **Uncontrolled Agent Costs:** This is the dominant theme. Recursive subagent spawning (#68430, #68110) and billing errors (#32544) are creating acute financial anxiety. Developers urgently need kill-switches, depth limits, and better cost visibility.
- **Data Integrity Failures:** Silent file truncation (#53940), session deletion despite config overrides (#41458), and missing tool results (#68457) are severely eroding trust in the tool’s reliability.
- **System-Level Instability on macOS:** Kernel zone leaks (#66020) and pty exhaustion (#66434, #65995) make Claude Code a system crash risk on macOS, a primary development platform.
- **Configuration Silently Ignored:** There is a strong cross-cutting pattern of settings being overridden—retention policies, agent environment variables, model choices. Developers feel locked out of control over their own tools.
- **Core Workflow Fragmentation:** Broken clipboard operations (#66192), blank screens on Windows (#51143), and malformed Bash invocations (#63870) show that fundamental daily workflows remain fragile across platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-15

---

## Today's Highlights
The Codex community is contending with significant Windows app instability following the latest update (v26.609.4994.0), with multiple reports of crash loops and broken WSL workflows. On the development side, the team is shipping major infrastructure including an async hooks runtime, expanded MCP timeouts, and rate-limit credit redemption in the TUI. Notably, the highly-requested thread renaming feature (#12564) has been closed after intense community engagement, signaling a planned implementation.

---

## Releases
No new releases were published in the last 24 hours.

---

## Hot Issues
*10 noteworthy issues from the community tracker*

**1. Windows desktop app crash after June 12 update**
*Issue #27979* — The Codex Desktop app (26.609.4994.0) no longer opens for many Windows users after the latest auto-update. With 21 comments, this is the most critical active regression, blocking all desktop usage on affected systems.
[#27979](https://github.com/openai/codex/issues/27979)

**2. Thread/chat renaming feature (Closed)**
*Issue #12564* — This enhancement to allow users to rename task and thread titles accumulated 80 comments and 111 👍 before being closed. Capturing a long-held community desire for better history navigation and organization.
[#12564](https://github.com/openai/codex/issues/12564)

**3. Project sidebar showing "No chats" incorrectly**
*Issue #25500* — Projects with active, non-archived conversations show an empty state in the Codex Desktop sidebar. 18 comments indicate a reproducible UI state mismatch that undermines workspace management.
[#25500](https://github.com/openai/codex/issues/25500)

**4. Project chat history disappeared after update**
*Issue #27353* — A severe data integrity issue where an macOS user's entire project history vanished post-update. Complements the other session state bugs and points to a wider state persistence problem.
[#27353](https://github.com/openai/codex/issues/27353)

**5. Missing Linux binary in MSIX breaks "Run agent in WSL"**
*Issue #28103* — The Microsoft Store build of v26.609.4994.0 ships without the Linux `codex` binary, causing the WSL "Run agent" feature to fail immediately. Critical for the Windows developer audience.
[#28103](https://github.com/openai/codex/issues/28103)

**6. macOS `code_sign_clone` consumes 62GB+ disk space**
*Issue #27536* — An unbounded disk leak in the macOS Electron app. The `code_sign_clone` directory in system temp grows massively across auto-updates, threatening storage on developer machines.
[#27536](https://github.com/openai/codex/issues/27536)

**7. CLI /status command lacks full usage data**
*Issue #15281* — A long-standing request (since March) for `codex /status` to expose accurate model names, reset windows, and token counts. The community wants full rate-limit transparency.
[#15281](https://github.com/openai/codex/issues/15281)

**8. Computer Use MCP initialize times out**
*Issue #23840* — The bundled Computer Use MCP handshake fails in the desktop app while the terminal works fine, blocking the primary Computer Use workflow for affected users.
[#23840](https://github.com/openai/codex/issues/23840)

**9. No toggle for spellchecking in app settings**
*Issue #25431* — Users are requesting an accessible on/off switch for the built-in spellchecker. Received 14 👍 quickly, highlighting a desire for greater editor-level customization.
[#25431](https://github.com/openai/codex/issues/25431)

**10. Windows sandbox fails after power outage**
*Issue #28248* — After a system interruption, all sandbox read operations fail due to corrupted ACLs. Indicates a fragility in the sandbox filesystem layer during unexpected termination.
[#28248](https://github.com/openai/codex/issues/28248)

---

## Key PR Progress
*10 important pull requests driving the codebase forward*

**1. Rate-limit credit API and TUI redemption**
*PRs #28143 & #28154* — Introduces the backend `account/rateLimits/read` API with a nullable `resetCredits` field and a TUI `/usage` flow to view and redeem personal reset credits. Directly addresses the community's desire for usage transparency.
[#28143](https://github.com/openai/codex/pull/28143) | [#28154](https://github.com/openai/codex/pull/28154)

**2. Increase default MCP tool timeout to 300s**
*PR #28234* — A tactical fix for the pervasive MCP timeout issues. Raising the limit from 120s to 300s targets the Computer Use initialization failures reported in #23840 and similar bugs.
[#28234](https://github.com/openai/codex/pull/28234)

**3. Auto-resolution timer for user input**
*PR #28235* — Adds a 60s hidden grace period and 60s visible countdown for `request_user_input` prompts in the TUI. Automatically submits an empty response if the user does not interact, preventing stalled sessions.
[#28235](https://github.com/openai/codex/pull/28235)

**4. Async hooks runtime (Stacked PRs)**
*PRs #27771, #27452, #27772* — Builds a bounded runtime for async hooks, allowing them to finish independently of the launching operation. Adds execution mode visibility to app-server and TUI. A major architectural expansion for Codex extensibility.
[#27771](https://github.com/openai/codex/pull/27771) | [#27452](https://github.com/openai/codex/pull/27452) | [#27772](https://github.com/openai/codex/pull/27772)

**5. Terminal resize reflow becomes stable**
*PR #27794* — Removes all feature flag gates for `terminal_resize_reflow`, making it always-on behavior. Core terminal ergonomics are now fully stable.
[#27794](https://github.com/openai/codex/pull/27794)

**6. Multi-tool install requests**
*PR #27640* — Expands `request_plugin_install` from single targets to flat lists or categorized groups. Lays the foundation for a richer, bulk plugin management system.
[#27640](https://github.com/openai/codex/pull/27640)

**7. External agent import accounting & telemetry**
*PRs #28008 & #28009* — Introduces stable import IDs and progress notifications for external agent imports. Provides the client with the correlation and artifact accounting needed for reliable import workflows.
[#28008](https://github.com/openai/codex/pull/28008) | [#28009](https://github.com/openai/codex/pull/28009)

**8. Managed child MITM CA infrastructure**
*PRs #25888, #26315* — Implements per-sandbox MITM CA bundle management. Tracks startup state and materializes immutable child-selected CA material, strengthening the security and isolation model for sandboxed environments.
[#25888](https://github.com/openai/codex/pull/25888) | [#26315](https://github.com/openai/codex/pull/26315)

**9. Enterprise workspace headline in statusline**
*PR #28232* — Adds a `workspace-headline` status line item for Enterprise ChatGPT/Codex accounts, displaying workspace messages refreshed every 10s. Signals continued investment in managed/enterprise features.
[#28232](https://github.com/openai/codex/pull/28232)

**10. Managed field support for requirements.toml**
*PR #27666* — Extends `requirements.toml` enforcement to managed authentication, storage, telemetry, and shell settings. Strengthens the configuration policy framework for organizational deployments.
[#27666](https://github.com/openai/codex/pull/27666)

---

## Feature Request Trends

- **History & Session Management:** Renaming threads (#12564), fixing sidebar sync (#25500), and preventing history loss (#27353) remain the dominant themes. Users are demanding durable, searchable, and navigable session archives.
- **Rate-Limit Visibility:** Transparent access to usage data (quota windows, token counts, model names) in both the CLI (#15281) and app is the loudest community voice for feature improvements.
- **UI/UX Customization:** Requests for toggling spellcheck (#25431), TUI scrolling (#23280), and shell environment consistency (#16551) show the user base is maturing and focusing on ergonomics.
- **Platform Parity & Reliability:** Windows users are vocalizing WSL integration needs (#28103) and sandbox resilience (#28248), while macOS users are impacted by resource leaks (#27536). Stability and feature parity across all platforms is a rising expectation.

---

## Developer Pain Points

- **Update Regressions:** The June 12 Windows update is a severe quality regression, causing crash loops and breaking WSL workflows (triggered by #27979, #28103, #27367).
- **Session State Corruption:** A cluster of bugs around projects and threads losing their state, showing empty states incorrectly, or disappearing entirely is eroding trust in session persistence.
- **Resource Management:** Unbounded disk consumption on macOS (`code_sign_clone`, 62GB+) points to systemic resource cleanup gaps that affect long-running users.
- **MCP & Computer Use Instability:** Recurring MCP initialization timeouts and "app-server exited" errors are making the Computer Use feature unreliable for a significant subset of users.
- **Transparency Gap:** The lack of detailed rate-limit data in the CLI and app creates confusion and anxiety around plan limits, pushing users to cobble together their own monitoring.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — Monday, June 15, 2026**

### 1. Today’s Highlights
Infrastructure saw heavy churn today as a massive 53-package dependency update landed, pulling in major version bumps for Puppeteer, the GenAI SDK, Undici, and Yargs. On the stability front, P1 bugs around agent hangs and false-success reporting continue to generate discussion, while several high-quality community patches for MCP compliance and telemetry reliability are waiting for review. The Auto Memory system remains the focal point of a dedicated quality workstream, with multiple open issues tracking redaction gaps and indefinite retries.

---

### 2. Releases
No new versions of the Gemini CLI were published in the last 24 hours.

---

### 3. Hot Issues
*Notable open issues sorted by community impact and severity.*

1. **Generalist Agent Hangs on Simple Tasks**
   [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) *(P1, 8 👍)* — The agent freezes indefinitely when deferring to the generalist sub-agent for trivial operations. Instructing the model not to use sub-agents is the only current workaround. Highest community upvotes in this batch.

2. **Sub-Agent Reports False Success After MAX_TURNS**
   [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) *(P1, 2 👍)* — Sub-agents that hit the turn limit report `Termination Reason: "GOAL"` and `status: "success"`, masking real failures. Especially dangerous for automated CI/CD pipelines.

3. **Shell Commands Get Stuck in “Awaiting Input”**
   [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) *(P1, 3 👍, effort/medium)* — Simple CLI commands finish executing but the shell remains in a waiting state, blocking further workflow progress.

4. **Browser Sub-Agent Fails on Wayland**
   [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) *(P1, 1 👍)* — The browser agent is broken on display servers using Wayland, preventing a whole segment of Linux users from leveraging browsing capabilities.

5. **`get-shit-done` Crashes During Summary**
   [#22186](https://github.com/google-gemini/gemini-cli/issues/22186) *(P1)* — A crash bug occurring during the user summary phase of the `get-shit-done` workflow, causing data loss.

6. **Custom Skills and Sub-Agents Rarely Used Autonomously**
   [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) *(P2)* — The model largely ignores user-defined custom skills and sub-agents unless explicitly told to use them, undermining the value of the extension system.

7. **Safety: Agent Resorts to Destructive Commands**
   [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) *(P2, 1 👍)* — The model frequently uses `git reset`, `--force`, and other destructive operations when safer alternatives exist. Community requests stronger guardrails and risk awareness.

8. **Auto Memory System Reliability Trio**
   [#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) *(P2)* — A collection of bugs covering indefinite retries on low-signal sessions, silent skipping of invalid memory patches, and the need for deterministic secret redaction before data reaches model context.

9. **400 Error When Exposing >128 Tools**
   [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) *(P2)* — The CLI hard-fails with a 400 error when too many tools are active. Community expectations call for smarter automatic tool pruning before submission.

10. **AST-Aware File Operations Investigation**
    [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) *(P2, 1 👍)* — An active epic tracking whether AST-aware file reads and searches can reduce token consumption and improve editing precision by understanding method and syntax boundaries.

---

### 4. Key PR Progress

1. **Fix MCP JSON Arrays in structuredContent**
   [#27730](https://github.com/google-gemini/gemini-cli/pull/27730) *(Open, he-yufeng)* — Prevents `McpComplianceTransport` from copying JSON arrays into `structuredContent`, fixing broken calendar-style tool responses. Includes regression tests.

2. **Telemetry Metric Attribute Truncation**
   [#27729](https://github.com/google-gemini/gemini-cli/pull/27729) *(Open, imsrnfo)* — Truncates telemetry attributes to 1024 characters to stop GCP Monitoring export error floods when using `--format json`.

3. **Fix Auto Model Visibility Without Preview Access**
   [#27718](https://github.com/google-gemini/gemini-cli/pull/27718) *(Open, he-yufeng)* — Prevents the `auto` model alias from disappearing from `/model` when dynamic model configuration is enabled and preview access is restricted.

4. **New Interactive Policies Dialog**
   [#22456](https://github.com/google-gemini/gemini-cli/pull/22456) *(Closed)* — Replaces the plain-text `/policies` output with a searchable, tabbed UI that categorizes rules by decision type (Allow, Ask, Deny).

5. **Non-Invasive UX Journey Testing Framework**
   [#23030](https://github.com/google-gemini/gemini-cli/pull/23030) *(Closed)* — Landed a white-box testing framework to verify React component presence and visual state in the terminal, enabling better end-to-end UI testing.

6. **Massive 53-Package Dependency Update**
   [#27925](https://github.com/google-gemini/gemini-cli/pull/27925) *(Closed)* — Batch merge of the `npm-dependencies` group, including `@agentclientprotocol/sdk` (0.16.1 → 0.25.0), `@octokit/rest`, and dozens of minor runtime updates.

7. **Puppeteer v24 → v25**
   [#27931](https://github.com/google-gemini/gemini-cli/pull/27931) *(Closed)* — Major version jump for the browser automation core, bringing new bug fixes and API stability for the Browser Agent.

8. **GenAI SDK v1 → v2**
   [#27929](https://github.com/google-gemini/gemini-cli/pull/27929) *(Closed)* — Upgrade to the next major version of the foundational `@google/genai` client library.

9. **Markdown Parser: marked v15 → v18**
   [#27934](https://github.com/google-gemini/gemini-cli/pull/27934) *(Closed)* — Three major version jumps for the CLI’s markdown rendering, likely closing several edge-case parsing bugs.

10. **CLI Framework: yargs v17 → v18**
    [#27933](https://github.com/google-gemini/gemini-cli/pull/27933) *(Closed)* — Core CLI argument parser updated to the latest major release.

---

### 5. Feature Request Trends

- **Agent Autonomy & Self-Awareness:** There is a strong demand for the agent to proactively use its full toolset—skills, sub-agents, and CLI self-knowledge—without requiring explicit user prompting ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968), [#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **AST-Aware Code Manipulation:** Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) are exploring syntax-aware reads and searches to reduce token waste and improve the precision of edits and codebase mapping.
- **Memory System Hardening:** The Auto Memory feature is shifting from “functional” to “reliable,” with requests focusing on deterministic redaction, scrubbing low-signal sessions, and transparent error reporting ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)).
- **Evaluation Infrastructure Maturity:** The majority of the day’s highest-comment issues touch on building robust component-level or project-level evaluation systems to catch regressions before they ship ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353), [#23166](https://github.com/google-gemini/gemini-cli/issues/23166)).

---

### 6. Developer Pain Points

- **Agent Reliability & False Reporting:** Hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), crashes ([#22186](https://github.com/google-gemini/gemini-cli/issues/22186)), and false success states ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) erode trust in autonomous workflows. Blocking issues remain open for months.
- **Configuration & Permission Ignorance:** Sub-agents often ignore `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), run without permission ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), or fail to recognize symlinks in agent directories ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)).
- **Workspace Hygiene & Safety:** The model frequently scatters temporary scripts across the file system ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) and opts for destructive `--force` flags over safer alternatives ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Tool Limit Crashing:** A hard 400 error when tool counts exceed 128 ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) without graceful degradation or automatic tool pruning is a frequent frustration for power users with many MCP or custom tools configured.
- **Terminal UI Regressions:** Corruption after exiting external editors ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)) and poor resize performance ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)) degrade the interactive terminal experience.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-15

## 1. Today's Highlights
The Copilot CLI ecosystem was quiet in terms of code changes, with no new releases or pull requests. The issue tracker, however, revealed critical stability concerns: a newly reported session-poisoning vulnerability (#3791) where a malformed attachment permanently breaks all subsequent turns, and a highly-upvoted duplicate item error (#3558) continues to block workflows at scale. On the feature front, developers are requesting automatic model discovery for BYOK setups (#3795) and deeper Azure DevOps integration (#3794).

## 2. Releases
No new versions of `github/copilot-cli` were published in the last 24 hours.

## 3. Hot Issues
*Note: 8 issues were updated in the period; 2 were spam/invalid. The 6 meaningful reports are covered below.*

**[area:agents] #956 – Agent skills scripts executed in wrong folder**
*Why it matters:* A 5-month-old bug where `SKILLS.md` script references fail because the CLI runs them from an unexpected working directory. This directly undermines the reliability of the Agent Skills ecosystem.
*Community reaction:* Low upvotes (+2) but sustained discussion (6 comments), indicating a vocal base of skill authors hitting this.
[GitHub Link](https://github.com/github/copilot-cli/issues/956)

**[area:context-memory, area:models] #3558 – Duplicate Item Errors**
*Why it matters:* A disruptive execution failure (`Duplicate item found with id ...`) during initial processing that completely halts the session. Highest-impact bug in the batch.
*Community reaction:* Strongest signal with +7 upvotes and 4 comments, confirming wide impact across user workflows.
[GitHub Link](https://github.com/github/copilot-cli/issues/3558)

**[triage] #3791 – Malformed attachment poisons session**
*Why it matters:* The most critical stability finding today. A password-protected `.xlsx` triggers a CAPI 400 that persists through all subsequent turns in the same session, effectively destroying the session’s usability.
*Community reaction:* Fresh report, no comments yet, but represents a severe UX regression.
[GitHub Link](https://github.com/github/copilot-cli/issues/3791)

**[triage] #3797 – Inconsistent prompt box layout in cmd tabs**
*Why it matters:* A visual inconsistency where the prompt UI renders differently across terminal tabs within the same window. While non-functional, it erodes the polish of the developer experience.
*Community reaction:* Just filed (1 comment), no upvotes yet.
[GitHub Link](https://github.com/github/copilot-cli/issues/3797)

**[triage] #3795 – Feature request: opt-in model discovery for BYOK / custom providers**
*Why it matters:* Users working with custom providers must manually set `COPILOT_MODEL`. This request asks the CLI to automatically discover provider models, reducing configuration overhead for enterprise deployments.
[GitHub Link](https://github.com/github/copilot-cli/issues/3795)

**[triage] #3794 – Add Azure DevOps work items to Up next**
*Why it matters:* The "Up next" panel remains empty for teams using Azure DevOps repos, even though ADO is already a supported project type. This is a clear integration gap that breaks the unified workflow promise.
[GitHub Link](https://github.com/github/copilot-cli/issues/3794)

*Also noted:* Two reports (#3793 and #3796) were closed as invalid/spam, reflecting ongoing triage efforts to maintain issue quality.

## 4. Key PR Progress
No pull requests were merged or updated in the last 24 hours. This lull may indicate the maintainer team is prioritizing triage and deep investigation of the session stability bugs (#3791, #3558) rather than pushing new features.

## 5. Feature Request Trends
- **Custom Model / BYOK Ergonomics (#3795):** The community is pushing for the CLI to abstract away manual configuration steps when using custom providers, requesting automatic model discovery as a quality-of-life improvement for enterprise users.
- **Cross-Platform Backlog Unification (#3794):** Users want the "Up next" panel to aggregate work items from external tools, beginning with Azure DevOps. This aligns with a broader theme of treating Copilot CLI as a universal developer inbox rather than a purely GitHub-native tool.
- **Agent Skill Determinism (#956):** The ongoing discussion around script execution paths signals that developers building agent skills need stronger guarantees about the runtime environment.

## 6. Developer Pain Points
- **Session Poisoning Risk (#3791):** A single malformed input can permanently corrupt a CLI session with no recovery path. This exposes a critical lack of error isolation or session state rollback.
- **Non-Actionable Execution Blockers (#3558):** The "Duplicate item" error stops progress entirely with no clear remediation, frustrating users who must restart sessions from scratch.
- **Agent Script Execution Divergence (#956):** Skill authors cannot reliably predict the working directory for their scripts, breaking spec-compliant skill definitions and reducing confidence in the skills platform.
- **UI Consistency Gaps (#3797):** Even minor terminal UI layout differences generate tickets, highlighting the high polish bar the developer community expects from a professional CLI tool.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-15**

### 1. Today’s Highlights
No new releases landed, but the community engaged deeply with critical service quality and agent control issues. The most intense discussion centers on a user reporting that the paid Code Plan’s actual throughput (~60+ requests/5h) falls far short of advertised figures of 300–1200 requests/5h (#2123). Meanwhile, the closure of the long-standing request for automatic project context loading (#850) and a new report of system–prompt conflicts (#2451) underscore a growing demand for deeper user steering and parity with tools like Claude Code.

### 2. Releases
No new versions or releases were published in the last 24 hours.

### 3. Hot Issues
*While the 24-hour update window contained only three issues, each reveals deep community concerns.*

* **#2123 (OPEN) — Severe Rate Limiting on Code Plan**  
  **Significance:** User `littlePoBoy` documents a massive discrepancy between advertised and actual rate limits on the paid plan. The vague percentage-based quota display is described as a “service black box,” and a denied refund request has escalated trust concerns. This is the highest-severity service complaint currently on the board.  
  **Link:** [MoonshotAI/kimi-cli Issue #2123](https://github.com/MoonshotAI/kimi-cli/issues/2123)

* **#850 (CLOSED) — Auto-load Project Context/Rules (AGENTS.md, .cursorrules)**  
  **Significance:** Proposed by `Al4ric`, this feature requested automatic ingestion of project-level rules files at session start—a standard behavior in Claude Code (`CLAUDE.md`). The closure of this request without implementation remains a prominent feature gap and a specific migration friction point.  
  **Link:** [MoonshotAI/kimi-cli Issue #850](https://github.com/MoonshotAI/kimi-cli/issues/850)

* **#2451 (OPEN) — System Prompt Conflicts with User Workflow**  
  **Significance:** User `iaindooley` on v0.12.0 reports that the hardcoded system prompt overrides strict custom guidelines supplied via API key. For advanced users requiring precise, deterministic agent steering, this lack of prompt-layer control renders custom workflows unreliable.  
  **Link:** [MoonshotAI/kimi-cli Issue #2451](https://github.com/MoonshotAI/kimi-cli/issues/2451)

### 4. Key PR Progress
*Four pull requests moved this cycle, spanning cross-platform fixes and core reliability hardening.*

* **#2452 (OPEN) — StrReplaceFile Multi-Edit Hunk Integrity**  
  **Fix:** Currently the tool applies all edits sequentially and only errors out if the *entire* result is unchanged, allowing unmatched hunks to cause cascading failures. This PR fails fast on the first unmatched hunk.  
  **Why it matters:** Critical hardening for code editing; prevents silent partial corruption during multi-hunk modifications.  
  **Link:** [MoonshotAI/kimi-cli PR #2452](https://github.com/MoonshotAI/kimi-cli/pull/2452)

* **#2018 (CLOSED) — Alt+V Paste for Windows Terminal**  
  **Fix:** Adds `Alt+V` as a fallback paste binding because Windows Terminal intercepts `Ctrl+V`.  
  **Why it matters:** Essential ergonomic patch for Windows developers needing reliable clipboard integration.  
  **Link:** [MoonshotAI/kimi-cli PR #2018](https://github.com/MoonshotAI/kimi-cli/pull/2018)

* **#2020 (CLOSED) — Per-Process Log Filenames**  
  **Fix:** Solves `loguru` rotation `PermissionError` on Windows by using `kimi.{pid}.log` files.  
  **Why it matters:** Eliminates a common race condition when developers run multiple concurrent CLI sessions.  
  **Link:** [MoonshotAI/kimi-cli PR #2020](https://github.com/MoonshotAI/kimi-cli/pull/2020)

* **#839 (CLOSED) — Configurable Shell Support for Windows**  
  **Fix:** Adds explicit configuration for the CLI shell in Windows environments.  
  **Why it matters:** Closes a long-standing platform parity gap, enabling seamless integration with preferred Windows terminals.  
  **Link:** [MoonshotAI/kimi-cli PR #839](https://github.com/MoonshotAI/kimi-cli/pull/839)

### 5. Feature Request Trends
*Distilling the most requested directions from recent community activity.*

* **Project-Level Context Loading:** The persistent demand for automatic detection and loading of project rules files (`.cursorrules`, `AGENTS.md`) is the community’s clearest signal. It is widely considered a table-stakes feature and a specific barrier for users migrating from Claude Code (`CLAUDE.md`).
* **Granular Prompt Composability:** Users want a layered prompt model where their custom instructions take precedence over the base system prompt. Issue #2451 highlights a fundamental desire for the agent to remain strictly subservient to user-defined strictures.

### 6. Developer Pain Points
*Recurring frustrations that are impacting user retention and workflow adoption.*

* **Service Credibility (The Trust Gap):** The severe rate-limiting and opaque quota display documented in #2123 represent a critical trust deficit. When actual throughput is ~5% of advertised capacity and refunds are disputed, the foundation of a paid developer tool is directly challenged.
* **Loss of Workflow Control:** The inability to reliably enforce custom instructions against the system prompt (#2451) introduces unpredictability. Power users require deterministic steering, and any ambiguity here undermines the tool’s utility for structured development workflows.
* **Competitive Parity Gaps:** The absence of auto-context loading (#850) adds significant friction compared to competitors. Users are forced into repetitive manual setup, negating the efficiency gains that an AI coding agent is meant to provide.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

**OpenCode Community Digest — June 15, 2026**

---

### 1. Today's Highlights
The v1.17.7 release landed yesterday with important plugin/ACP fixes and MCP improvements, but is already drawing heat for stability regressions including terminal freeze (#32376) and `EditBuffer` crashes (#32348). Meanwhile, the community is healthily contentious over DeepSeek V4 Pro pricing (#28846) pushing for full MCP standards compliance (#28567). On the PR front, major work is progressing on unified usage tracking (#9545) and clean subagent context inheritance (#32302).

---

### 2. Releases
**v1.17.7** — [Full Changelog](anomalyco/opencode)
- *Bugfixes:* Plugin client requests now reuse the active server (no longer assume default local port). ACP shell tool calls display command and working directory from invocation. Plugin-defined shell environment variables are now correctly applied to PTY sessions.
- *Improvements:* General MCP subsystem hardening.
- *⚠️ Known Regressions:* Users reporting `EditBuffer is destroyed` guard failures (#32348) and complete terminal unresponsiveness requiring process kill (#32376).

---

### 3. Hot Issues

1.  **[#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](anomalyco/opencode Issue #28846)** *(CLOSED)*  
    **77 comments | 79 👍** — The community overwhelmingly demanded that cost savings from DeepSeek's price cut be passed to subscribers. Now closed, presumably implemented or planned.

2.  **[#13984 — cannot copy and paste in opencode CLI](anomalyco/opencode Issue #13984)** *(OPEN)*  
    **48 comments** — A long-standing terminal compatibility issue. Clipboard operations report success but paste yields nothing. OS and emulator dependent, high frustration level.

3.  **[#28567 — Full MCP client capabilities](anomalyco/opencode Issue #28567)** *(OPEN)*  
    **11 comments | 21 👍** — OpenCode's MCP client is lagging behind the spec (Roots, Sampling, Streaming). Users want parity to keep the plugin ecosystem competitive.

4.  **[#32172 — Add GLM-5.2 model support for Z.AI provider](anomalyco/opencode Issue #32172)** *(OPEN)*  
    **7 comments** — Z.AI dropped GLM-5.2, a new reasoning model. The community wants it wired in immediately.

5.  **[#11829 — Recursive Language Model Context Management](anomalyco/opencode Issue #11829)** *(OPEN)*  
    **6 comments | 11 👍** — Proposes treating context as an *external environment* queried programmatically (RLM paradigm from MIT). A sophisticated alternative to compaction/sliding windows.

6.  **[#30763 — TUI: Statuses via "flags" in current Session view](anomalyco/opencode Issue #30763)** *(OPEN)*  
    **4 comments** — Users want user-defined lightweight tags (todo, doing, done) on sessions, directly in the TUI, to improve workflow management.

7.  **[#32348 — EditBuffer Destroyed consistently popping after upgrading to 1.17.7](anomalyco/opencode Issue #32348)** *(OPEN)*  
    **3 comments** — Critical regression. `clearAllHighlights` guard fails repeatedly after the upgrade, rendering sessions unstable.

8.  **[#31778 — MCP server subprocess receives full process.env (API keys leaked)](anomalyco/opencode Issue #31778)** *(OPEN)*  
    **2 comments** — Security concern: entire environment is passed to local MCP server subprocesses, exposing keys, tokens, and credentials.

9.  **[#32366 — UI stuck on 'thinking' indefinitely after stream error](anomalyco/opencode Issue #32366)** *(OPEN)*  
    **2 comments** — Stream errors (e.g., socket close) leave the UI in an unrecoverable "thinking…" state with no error display. Requires full restart.

10. **[#32376 — v1.17.7 terminal is completely frozen and unable to send messages](anomalyco/opencode Issue #32376)** *(OPEN)*  
    **2 comments** — Another v1.17.7 regression; terminal becomes completely unresponsive. No workaround other than killing the process.

---

### 4. Key PR Progress

1.  **[#32364 — fix: reset terminal modes on tui shutdown](anomalyco/opencode PR #32364)**  
    Closes #20458. Ensures terminal state (title, modes) is fully restored on TUI exit, preventing shell corruption.

2.  **[#32377 — fix(acp): clean up session mcp servers](anomalyco/opencode PR #32377)**  
    Closes #32371. ACP sessions that register MCP servers now properly tear them down on close, preventing resource leaks.

3.  **[#32373 — feat(opencode): support models.dev reasoning options](anomalyco/opencode PR #32373)**  
    Adds shared `ReasoningVariants` handling for the new `reasoning_options` fields on `models.dev` catalog models.

4.  **[#32302 — fix(opencode): forward parent attachments to subagents](anomalyco/opencode PR #32302)**  
    Closes #25553. Fixes a bug where `@mention` subagents in the `task` path lost parent context attachments, breaking critical context handoffs.

5.  **[#32245 — fix(mcp): stop idle OAuth callback server](anomalyco/opencode PR #32245)**  
    Properly releases the OAuth callback port on success, error, cancellation, or timeout. Clean resource management for MCP auth flows.

6.  **[#32241 — fix(tui): render move errors inline](anomalyco/opencode PR #32241)**  
    Improves error resilience in session dialogs by keeping loading, success, error, and empty states inside the same shell, preventing crashes.

7.  **[#9545 — feat(usage): unified usage tracking with auth refresh](anomalyco/opencode PR #9545)**  
    Major backend feature: centralized usage tracking for OAuth providers (Anthropic, GitHub Copilot, OpenAI). Adds GET /usage and SDK regeneration.

8.  **[#31993 — fix(app): restore desktop open menu](anomalyco/opencode PR #31993)**  
    Fixes two overlapping regressions that broke the "Open in" control in the desktop session header.

9.  **[#32370 / #29967 — Linux clipboard selection (PRIMARY buffer)](anomalyco/opencode PR #32370)**  
    New `linux_clipboard_selection` config for PRIMARY buffer support. A definitive fix for copy/paste on Linux terminals.

10. **[#31132 — fix(tui): load root sessions safely in dialogs](anomalyco/opencode PR #31132)**  
    Closes #16270, #31125. Resolves long-standing session dialog crashes by improving root session loading and list construction. Supersedes several prior attempts.

---

### 5. Feature Request Trends

- **MCP Standards Alignment** — The loudest feature vector. Users demand full specification support (Roots, Sampling, Streaming) and improved security boundaries (#28567, #31778). The plugin ecosystem is straining against the current client limits.
- **Session & Workspace Organization** — A growing need for better TUI-native project management: session flags/statuses (#30763), session renaming (#32375), SSH remote references (#31901), and bidirectional cursor pagination (#8535/PR).
- **Economic Optimization** — The DeepSeek pricing firestorm (#28846) plus rapid asks for new models (GLM-5.2 #32172, Grok Composer 2.5 #31475) reveal a user base actively chasing best-cost inference.
- **Context Engineering** — Advanced users are pushing beyond compaction toward fully externalized context environments (RLM #11829), coupled with demands for reliable subagent context inheritance (#30355, #32302/PR).

---

### 6. Developer Pain Points

- **Release Stability** — The v1.17.7 regressions (#32348, #32376, #32366) are the top acute pain point. Stream state recovery and render guard logic need hardening.
- **Plugin System Fragility** — Async prompt overlaps (#28202), silent permission drops (#28037), and environment variable leaks (#31778) indicate the plugin/MCP layer is stressed by real-world concurrent usage.
- **Terminal Ecosystem Friction** — Linux copy/paste (#13984), terminal reset on exit (#32364), and PRIMARY buffer quirks (#32370) remain persistent, OS-specific maintenance sinks.
- **Free Tier UX** — Confusion around "free usage exceeded" (#15585) points to a need for clearer rate limit communication and error messaging rather than silent blocks.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi community digest for June 15, 2026.

---

## Today's Highlights

The community is intensely focused on a critical **Escape key interrupt regression** affecting both main tasks and subagents (#5736, #5685), alongside a deep architectural debate on **dependency duplication** caused by Shrinkwrap (#5653). On the positive side, the contributor pipeline is thriving, with a flurry of high-quality implementations landing, including a first-party **xAI Grok OAuth integration** (#5714), a **safe extension reload mechanism** (#5735), and a formal **extension prompt-guidelines API** (#5710/#5711).

## Releases

No new releases were cut in the last 24 hours.

## Hot Issues

1.  **[#5103] Windows bash detector fails when Git Bash is on PATH but not under C:\Program Files** (18 comments)
    A major blocker for Windows developers on non-standard drives. The built-in detection is hardcoded to search `C:\Program Files\Git`, ignoring the user's PATH. High community frustration as it breaks local agent execution on the most common alternative Windows setup.
    *Link:* [earendil-works/pi Issue #5103](https://github.com/earendil-works/pi/issues/5103)

2.  **[#5653] Move off Shrinkwrap** (9 comments)
    Installing both `pi-ai` and `pi-coding-agent` as direct deps results in duplicate module copies on disk, causing a hard-to-debug runtime state split (e.g., API provider registries). The core team is actively debating full deduplication strategies.
    *Link:* [earendil-works/pi Issue #5653](https://github.com/earendil-works/pi/issues/5653)

3.  **[#5702] `prompt_cache_retention` request failure & maintainability in `generate-models.ts`** (6 comments)
    A deep technical report from a power user (devasur) identifies a 400 error caused by sending unsupported `cache_control` fields to specific providers—but the real bombshell is the analysis of the monolithic `generate-models.ts` file. The ensuing discussion led directly to a draft refactor PR (#5743).
    *Link:* [earendil-works/pi Issue #5702](https://github.com/earendil-works/pi/issues/5702)

4.  **[#5736] Escape no longer interrupts active interactive task** (6 comments)
    A highly alarming regression. The UI advertises `Escape` as the cancel key, but pressing it during an active run can leave the agent running. The root cause appears related to sub-agent lifecycle management.
    *Link:* [earendil-works/pi Issue #5736](https://github.com/earendil-works/pi/issues/5736)

5.  **[#5654] Add `excludeFromContext` to custom messages** (6 comments, 1 👍)
    A strong community push to let extension-injected messages (e.g., `/status` pings) skip LLM context entirely, mirroring the existing flag on bash-execution messages. This is a highly sought-after ergonomic improvement for instrumentation extensions.
    *Link:* [earendil-works/pi Issue #5654](https://github.com/earendil-works/pi/issues/5654)

6.  **[#5687] `pi list` and `pi update` never exit when an extension runs an MCP server** (6 comments)
    Core CLI utilities hang indefinitely. The root cause is that `handlePackageCommand` loads extensions, which in turn start long-lived MCP servers. This blocks users from running admin commands without manually killing the process.
    *Link:* [earendil-works/pi Issue #5687](https://github.com/earendil-works/pi/issues/5687)

7.  **[#5671] `~/.pi` and `cwd/.pi` overlap** (5 comments, 3 👍)
    Authored by project veteran mitsuhiko, this issue questions the design of using `.pi` for both global settings and project-local settings. While currently mitigated by storing global data in `.pi/agent`, the naming collision is a persistent source of confusion for new users.
    *Link:* [earendil-works/pi Issue #5671](https://github.com/earendil-works/pi/issues/5671)

8.  **[#5706] Task hangs indefinitely at "waiting for summary approval" when using local LLM backend** (5 comments)
    A critical blocker for the local-model user segment. Tasks using OpenAI-compatible local backends (e.g., Ollama, vLLM) get stuck at the summary approval step. Cloud providers (DeepSeek, OpenAI) work fine, suggesting a serialisation or timeout mismatch in the approval flow.
    *Link:* [earendil-works/pi Issue #5706](https://github.com/earendil-works/pi/issues/5706)

9.  **[#5303] Bash tool truncates command output when a child holds stdout past exit** (3 comments)
    A painful silent data loss bug. The `waitForChildProcess` function destroys the output accumulator 100ms after the parent process exits, but children (e.g., pre-commit hooks spawned by `git commit`) can still emit data. The model receives truncated results.
    *Link:* [earendil-works/pi Issue #5303](https://github.com/earendil-works/pi/issues/5303)

10. **[#5710] A way to add extension-level prompt guidelines** (4 comments)
    A well-formed feature proposal introducing `pi.setPromptGuidelines()`. It aims to let extensions inject project-wide rules (e.g., "Prefer existing terminology") without monkey-patching system prompts.
    *Link:* [earendil-works/pi Issue #5710](https://github.com/earendil-works/pi/issues/5710)

## Key PR Progress

1.  **[[DRAFT] #5743] Refactor `generate-models.ts` into a data-driven generator**
    A direct follow-up to the technical debt raised in #5702. Devasur proposes splitting the monolithic provider config file into a data-driven pipeline. Strong signal of mature community engineering contributing back upstream.
    *Link:* [earendil-works/pi PR #5743](https://github.com/earendil-works/pi/pull/5743)

2.  **[#5738] Fix pricing for Anthropic 1h cache writes at 2x input**
    Corrects a significant cost undercount. The provider aggregates `cache_creation_input_tokens`, losing the 5m/1h split. The PR reads the `ephemeral_1h_input_tokens` field to charge 1h writes at the correct 2x base rate instead of the 5m rate.
    *Link:* [earendil-works/pi PR #5738](https://github.com/earendil-works/pi/pull/5738)

3.  **[#5678] Add `excludeFromContext` for custom messages**
    Implements the popular #5654 feature request. mitsuhiko ensures the flag is respected by compaction, branch summarization, and the core `convertToLlm` serialization, preventing flagged messages from entering model context without sacrificing persistence.
    *Link:* [earendil-works/pi PR #5678](https://github.com/earendil-works/pi/pull/5678)

4.  **[#5735] Fix: defer extension reload requests safely**
    Addresses the long-standing danger of reloading extensions from within hooks. Makes `ctx.reload()` safe by deferring the actual reload until the next safe boundary in the agent loop.
    *Link:* [earendil-works/pi PR #5735](https://github.com/earendil-works/pi/pull/5735)

5.  **[#5732] Support `allowCommands` option in `sendUserMessage`**
    Enables slash commands (e.g., session reset, connection triggers) from extension-injected user messages by allowing prompt template expansion to be toggled on.
    *Link:* [earendil-works/pi PR #5732](https://github.com/earendil-works/pi/pull/5732)

6.  **[#5731] Add tool instrumentation for execution profiling**
    A new layer of telemetry within the tool execution engine, allowing developers to trace and profile tool performance directly from within the agent.
    *Link:* [earendil-works/pi PR #5731](https://github.com/earendil-works/pi/pull/5731)

7.  **[#5726] Fix test model IDs across providers**
    CI stability fix. Updates hardcoded test model IDs to match current Anthropic, OpenRouter, and other provider naming conventions.
    *Link:* [earendil-works/pi PR #5726](https://github.com/earendil-works/pi/pull/5726)

8.  **[#5714] Add xAI Grok account OAuth login**
    A major integration from hyiiiii. Adds a built-in OAuth provider for xAI using OIDC discovery and device-code login, plus Grok subscription models backed by the Grok CLI proxy. Surfaced in the `/login` flow.
    *Link:* [earendil-works/pi PR #5714](https://github.com/earendil-works/pi/pull/5714)

9.  **[#5711] Add extension prompt guideline API**
    Implements #5710. Provides `pi.setPromptGuidelines()` on the `ExtensionAPI` object, allowing extensions to contribute to the system prompt without raw string manipulation.
    *Link:* [earendil-works/pi PR #5711](https://github.com/earendil-works/pi/pull/5711)

10. **[#5385] Detect first-run terminal theme (light/dark)**
    Automatically queries the terminal via OSC to detect the system theme on first launch, persisting the choice to settings. Solves the mismatch where Pi defaults to a dark theme on a light terminal.
    *Link:* [earendil-works/pi PR #5385](https://github.com/earendil-works/pi/pull/5385)

## Feature Request Trends

- **Context Budgeting & Garbage Collection:** The loudest trend is fighting context bloat. Proposals for `excludeFromContext` (#5654), `allowCommands`/template expansion (#5733), and model-specific compaction limits (#5722) all aim to keep the LLM focused on meaningful tokens.
- **Multi-Agent Concurrency:** Users increasingly want to manage multiple live agent sessions without teardown (#5700), driven by workflows that manage parallel background agents.
- **Provider Ecosystem Depth:** Requests are shifting from "add more providers" to "make each provider work better." This includes flexible `auth.json` config (#5728), dedicated provider models (Grok/GLM/Kimi), and raw payload exposure in hooks (#5730).
- **Extension API as a Platform:** The community is treating the extension system as a first-class development platform, requesting formal APIs for prompt guidelines (#5710), safe reloading (#5735), and execution profiling (#5731).

## Developer Pain Points

- **Windows Experience is Fragile:** The top recurring frustration is Windows support. The bash detection bug (#5103), broken SIGTERM cleanup (#5724), WezTerm rendering issues (#5618), and streaming scroll jumps (#5576) signal a significant quality gap on the platform.
- **Output Loss and Reliability:** Silent data loss from the bash tool (#5303) and crashes from background processes (#5208) erode trust in the agent’s ability to provide correct command output.
- **Talk Interruption is Broken:** The Escape key regression (#5736, #5685) is the highest-urgency UX bug right now. Users expect a hard abort and are getting stuck subagents.
- **CLI Hang on MCP Extensions:** The inability to run basic `pi list` or `pi update` commands when MCP servers are active (#5687) creates a poor developer experience for anyone using the server ecosystem.
- **Dependency Duplication:** The Shrinkwrap issue (#5653) highlights a broader frustration with Node.js dependency management in monorepo-like tooling, causing real runtime isolation bugs.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

**Qwen Code Community Digest**
*Date: 2026-06-15*
*Source: github.com/QwenLM/qwen-code*

---

### Today’s Highlights
Security and reliability dominate the conversation today. A critical report (#5102) demonstrates that the agent can execute provider-requested side effects during permission-contract probes, sparking immediate discussion on trust boundaries. Meanwhile, a false-positive Trojan detection in the VSIX package (#5055) continues to impact Windows users. On the infrastructure front, a major CI flaw was exposed where the PR review job exits with code zero on API errors, silently reporting green success while posting no review comments (#5052). Positively, the community is rallying around feature PRs that enhance cost visibility, context safety, and session persistence.

---

### Releases
No new releases in the last 24 hours.

---

### Hot Issues

1. **[#5102 – Security contract side effect execution](https://github.com/QwenLM/qwen-code/issues/5102)** *(Critical)*
   A deterministic local verification run confirms Qwen Code executed a provider-requested shell command that wrote a file during the permission-contract probe, despite the probe contract prohibiting such actions. This challenges the fundamental security model of the agent sandbox.

2. **[#5052 – CI false green on API errors](https://github.com/QwenLM/qwen-code/issues/5052)** *(Priority P2)*
   The `qwen-code-pr-review.yml` pipeline reports a green checkmark when the API connection drops mid-review. The job exits code 0, leaving the PR completely unreviewed with no indication of failure. Over 5 comments, the community has called for proper exit-on-error handling.

3. **[#5055 – Trojan false positive in VSIX package](https://github.com/QwenLM/qwen-code/issues/5055)** *(Priority P1, Bug)*
   Windows Defender flags the 0.18.0 VSIX extension as `Trojan:JS/ShaiWorm.DBA!MTB`. This is generating significant friction for the Windows user base and demands an urgent signing or packaging review from the maintainers.

4. **[#5080 – API Key / Token Plan configuration conflict](https://github.com/QwenLM/qwen-code/issues/5080)** *(Priority P2, Bug)*
   Users configuring Alibaba Bailian via `qwen config` experience 401 errors when switching between Standard API Key (`sk-xxx`) and Token Plan provider endpoints. The configuration matrix does not properly isolate these connection types, causing interference.

5. **[#5101 – Repeated large tool results overflow context](https://github.com/QwenLM/qwen-code/issues/5101)** *(Priority P1, Bug)*
   When a provider repeatedly asks for a command that emits large output, Qwen Code carries every duplicate result back through provider history. This accelerates context window exhaustion and represents the specific mechanism behind many "max_tokens" truncation errors.

6. **[#5114 – Daemon segfault on Ubuntu 24.04](https://github.com/QwenLM/qwen-code/issues/5114)** *(Bug)*
   A fresh install of the daemon module on Ubuntu 24.04 triggers a SIGSEGV at startup. The stack trace points to a native dependency issue, blocking users who rely on the daemon for background persistent sessions.

7. **[#5119 – No method to allow sudo commands](https://github.com/QwenLM/qwen-code/issues/5119)** *(Feature Request)*
   When an agent attempts a `sudo` command, it fails ungracefully and forces the user into a copy-paste loop. The community is requesting a persistence layer in the permission dialogue to remember sudo approval for a session.

8. **[#4218 – MCP filesystem tools not available to model](https://github.com/QwenLM/qwen-code/issues/4218)** *(Bug)*
   A persistent Windows MCP bug: the UI shows `server-filesystem` as connected, but the AI model receives no tool definitions and cannot invoke read/write operations. This remains a critical gap for Windows MCP users.

9. **[#3203 – OAuth free tier policy adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** *(Feature Request)*
   The proposal to reduce the free tier from 1,000 to 100 requests/day has generated 135 comments. The community is highly vocal about the impact on existing workflows, and Pro plan availability remains a secondary complaint.

10. **[#5124 – Align `/loop` baseline coverage](https://github.com/QwenLM/qwen-code/issues/5124)** *(Feature Request)*
    A formal request to lock down the cron-backed loop behavior with tests and expose a proper command surface. This signals growing production use of scheduled/background automation within Qwen Code.

---

### Key PR Progress

1. **[#5118 – Per-task token & time detail in web-shell](https://github.com/QwenLM/qwen-code/pull/5118)**
   Expands completed todo items in the web-shell UI to show start/end time, elapsed duration, token breakdowns (input/output/cached), and API time. Directly addresses the demand for cost and resource transparency.

2. **[#4943 – `--safe-mode` CLI flag](https://github.com/QwenLM/qwen-code/pull/4943)**
   Adds a troubleshooting-first flag that disables all user customizations: QWEN.md, hooks, extensions, skills, MCP servers, subagents, and conditional rules. Essential for debugging agent misbehavior.

3. **[#5030 – Resume interrupted turn without "continue"](https://github.com/QwenLM/qwen-code/pull/5030)**
   Introduces a first-class mechanism to resume an unfinished assistant turn after a crash or interruption. Eliminates the need for a synthetic "continue" user message, a major session persistence improvement.

4. **[#5094 – Dynamic Workflows P4a (extractAndStripMeta)](https://github.com/QwenLM/qwen-code/pull/5094)**
   Implements the first half of Phase 4 of the Dynamic Workflows port. Separates the meta-extraction step from the main workflow loop, laying plumbing for richer workflow orchestration.

5. **[#4564 – Token usage stats & cost visibility](https://github.com/QwenLM/qwen-code/pull/4564)**
   Adds persisted token-usage accounting. The new `/stats` command provides daily/monthly breakdowns by model and auth type, with CSV/JSON export. Coordination boundaries with existing stats are documented.

6. **[#5073 – Warn on oversized context instructions](https://github.com/QwenLM/qwen-code/pull/5073)**
   Adds a startup warning when the always-loaded QWEN.md exceeds 15% of the active model’s context window. A proactive guard against silent context starvation.

7. **[#4866 – Split PR triage into 4-job pipeline](https://github.com/QwenLM/qwen-code/pull/4866)**
   Replaces the monolithic `/triage` skill with a staged `qwen-pr-triage.yml` pipeline (resolve → product-decision → review → check). Aims to reduce CI false positives and improve maintainability.

8. **[#5001 – Optional `[HH:MM:SS]` timestamps in CLI](https://github.com/QwenLM/qwen-code/pull/5001)**
   Adds an `output.showTimestamps` setting that renders a timestamp before each assistant turn. The same timestamp appears immediately when output starts, not after completion.

9. **[#4520 – Centralized model-facing tool output truncation](https://github.com/QwenLM/qwen-code/pull/4520)**
   Moves truncation logic from the shell tool into `CoreToolScheduler`. This ensures any tool returning string content is bounded before being injected into conversation history, preventing context overflow.

10. **[#5120 – Fix daemon auto-title generation on empty history](https://github.com/QwenLM/qwen-code/pull/5120)**
    Adds a guard to skip automatic session title generation when the history contains no user message. Fixes a regression where daemon-created sessions triggered title generation prematurely.

---

### Feature Request Trends

- **Cost & Usage Visibility:** The strongest signal this week. Users want granular access to token counts, API times, and per-task costs. PRs #5118 and #4564 directly target this, while #5101 frames the absence of this data as a bug.
- **Security Model Maturation:** The expectation for enterprise-grade guardrails is rising. Requests for proper sudo support (#5119), contract-respecting probe execution (#5102), and a safe mode (#4943) indicate the tool is being evaluated for sensitive production environments.
- **Session & UI Persistence:** Developers want persistent preferences (history collapse #4085, active model display #5104) and reliable long-running sessions (turn resumes #5030, daemon stability #5114).
- **Observation-Based Attention:** A growing need for the agent to handle real-time feedback from tools without repeating the same failing action, highlighted by requests to improve the `/loop` command (#5124) and break infinite edit loops (#3184).

---

### Developer Pain Points

- **Context Window Exhaustion:** This is the most frustrating recurring issue. Agents regularly fail due to `max_tokens` limits, repeated injection of large tool outputs (#5101), and overly verbose history management, leaving users stuck mid-task without clear recovery paths.
- **Looping & Non-Termination:** The agent frequently enters repetitive edit-debug-fail loops (#3184, #5100) with no built-in break mechanism. This erodes trust in autonomous mode and forces constant manual intervention.
- **Authentication & Plan Volatility:** Constant friction around free tier throttling (#3203), unavailability of the Pro plan (#3272), and confusing API key configuration (#5080) creates a poor onboarding experience.
- **Windows & Cross-Platform Parity:** Windows users remain second-class citizens with MCP tool connection failures (#4218), antivirus false positives (#5055), and packaging issues that degrade the overall experience compared to macOS/Linux.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# CodeWhale (formerly DeepSeek TUI) Community Digest — 2026-06-15

---

## 1. Today's Highlights

The rename to **CodeWhale** is now official in the v0.8.60 release, with the canonical project name, CLI, npm package, and release assets fully transitioned. The community is impatiently awaiting the v0.8.61 stabilization release ([PR #3225](https://github.com/Hmbown/CodeWhale/pull/3225)), which promises to fix the critical Windows TUI freeze and seed the WhaleFlow orchestration layer. Developer sentiment this week focuses heavily on reliability gaps—persistent sub-agent timeouts, missing provider failover, and agent telemetry deficits—which remain the most significant barriers to professional daily driving.

---

## 2. Releases

**No new releases today.** The most recent release is **v0.8.60**, which formalizes the CodeWhale rebrand. The canonical project name, npm package, and release artifacts are now `codewhale`. The legacy `deepseek-tui` npm package is fully deprecated. Migration instructions are in `docs/REBRAND.md`.

---

## 3. Hot Issues

1. **[Issue #3102](https://github.com/Hmbown/CodeWhale/issues/3102): v0.8.62 — Add first-class clarification question requests for agents**  
   *Author: Hmbown | 💬 3 | Tags: enhancement, ux, reliability*  
   A foundational UX gap: agents currently can only emit standard chat messages when they need input rather than using a formal harness-level request. This blocks modal interactions for secrets, permissions, and ambiguous queries.

2. **[Issue #2487](https://github.com/Hmbown/CodeWhale/issues/2487): Frequent error — Turn stalled / no completion signal received**  
   *Author: yahayao | 💬 12 | 👍 1 | Tags: bug, v0.8.61*  
   The most active bug thread. YOLO mode freezes entirely with a "Turn stalled" prompt; `continue` cannot recover the session. Strongly impacts automated workflow reliability.

3. **[Issue #1806](https://github.com/Hmbown/CodeWhale/issues/1806): Sub-agent 120s API timeout renders `agent_open` nearly unusable**  
   *Author: qiyuanlicn | 💬 4 | Tags: bug, v0.8.39*  
   Parallel sub-agents share a hard 120-second API ceiling, causing all child tasks to fail identically. Community members report this defeats the advertised parallel offload use case.

4. **[Issue #1812](https://github.com/Hmbown/CodeWhale/issues/1812): TUI freeze on Windows (crossterm poll)**  
   *Author: aboimpinto | 💬 5 | Tags: bug, tui, reliability, Windows*  
   UI becomes completely unresponsive without crashing. Two confirmed events with logs captured. The pending v0.8.61 release targets this as a primary bugfix.

5. **[Issue #2574](https://github.com/Hmbown/CodeWhale/issues/2574): Provider fallback chain — auto-switch on API failure**  
   *Author: hsdbeebou | 💬 3 | Tags: enhancement, v0.8.61*  
   Users must manually run `/provider` when quotas or API errors interrupt work. A dormant config slice was merged in [PR #2779](https://github.com/Hmbown/CodeWhale/pull/2779), but runtime failover is still missing.

6. **[Issue #2666](https://github.com/Hmbown/CodeWhale/issues/2666): Telemetry — agents need visible token context and resource usage**  
   *Author: Hmbown | 💬 2 | Tags: bug, v0.8.61, v0.8.64*  
   During long-running or multi-agent tasks, agents have no visibility into token budgets, context pressure, elapsed time, or child-agent status. This blind-spot can cause agents to run out of capacity without warning.

7. **[Issue #3222](https://github.com/Hmbown/CodeWhale/issues/3222): Add `reasoning_style` override for inline-tag thinking blocks**  
   *Author: buko | 💬 2 | Tags: bug, enhancement, documentation*  
   Parsing of reasoning content from MiniMax M3 and similar models using inline XML-style thinking blocks is broken. Third-party model support remains a recurrent pain point.

8. **[Issue #3232](https://github.com/Hmbown/CodeWhale/issues/3232): Native updater fragile behind proxies**  
   *Author: zhyuzhyu | 💬 1 | Tags: bug, enhancement*  
   `codewhale update` fails on networks behind corporate proxies due to GitHub API rate limiting and missing retry logic for EOF errors. A clear enterprise adoption blocker.

9. **[Issue #1067 / #3207](https://github.com/Hmbown/CodeWhale/issues/3207): glibc 2.39 dependency — incompatible with Ubuntu 22.04 / RHEL**  
   *Authors: RAIN-LOJK / eipiem1 | 💬 3 / 2 | Tags: bug, v0.8.61*  
   Pre-built Linux binaries require glibc 2.39, locking out users on stable distributions. Multiple calls for supporting both `glibc 2.35` and `2.39` targets in releases.

10. **[Issue #3066](https://github.com/Hmbown/CodeWhale/issues/3066): Cost tracking is dead for all non-DeepSeek models**  
    *Author: Hmbown | 💬 1 | Tags: enhancement, tui, model-lab*  
    `pricing.rs` only maps costs for `deepseek*` and Xiaomi MiMo. Users of Kimi, Qwen, GLM, MiniMax, OpenAI, or OpenRouter models see zero cost data, cache savings, or accrual.

---

## 4. Key PR Progress

1. **[PR #3225](https://github.com/Hmbown/CodeWhale/pull/3225) (Draft): v0.8.61 — Freeze fix + WhaleFlow foundation**  
   *28 commits over main*  
   The major pending release. Fixes the Windows crossterm-poll freeze and introduces the WhaleFlow orchestration substrate. Draft state, flagged as launch-blocker critical.

2. **[PR #3051](https://github.com/Hmbown/CodeWhale/pull/3051) (Closed): Voice slash command (`/voice`)**  
   Adds speech-to-text input to the TUI, reusing the active provider's chat completions API for transcription. Inspired by MiMo Code's voice UX.

3. **[PR #3197](https://github.com/Hmbown/CodeWhale/pull/3197) (Closed): Rename DeepSeek blue consumers to whale accent**  
   Completes the visual rebrand by migrating all `DEEPSEEK_BLUE` palette references to `WHALE_ACCENT_PRIMARY`. Deprecated aliases retained for compatibility.

4. **[PR #2771](https://github.com/Hmbown/CodeWhale/pull/2771) (Closed): LLM-guided AGENTS.md init**  
   The `/init` command now delegates `AGENTS.md` generation to the LLM based on gathered project context, replacing the previous static template approach.

5. **[PR #2779](https://github.com/Hmbown/CodeWhale/pull/2779) (Closed): Dormant provider fallback chain config**  
   Adds `fallback_providers = [...]` parsing to the config model with a dormant `ProviderChain` helper. No runtime effect yet, but builds the data layer for Issue #2574.

6. **[PR #2802](https://github.com/Hmbown/CodeWhale/pull/2802) (Closed): Hugging Face MCP helpers**  
   Introduces `/hf mcp status`, `/hf mcp setup`, and `/hf concepts` slash commands to manage settings-driven MCP agents, bridging CodeWhale with the broader MCP ecosystem.

7. **[PR #2797](https://github.com/Hmbown/CodeWhale/pull/2797) (Closed): Sofya search provider**  
   Adds a new web search backend to the agent toolchain, expanding the agent's ability to gather real-time information from indexed sources.

8. **[PR #2795](https://github.com/Hmbown/CodeWhale/pull/2795) (Closed): Enrich auth errors with request context**  
   Auth error messages now include provider, base URL authority, model, key source, key type, and a redacted key fingerprint—significantly improving debug-ability.

9. **[PR #2102](https://github.com/Hmbown/CodeWhale/pull/2102) (Closed): Defer low-value native tools by default**  
   Performance optimization: tools outside the core catalog are now materialized on-demand rather than loaded at startup. An `always_load` config escape hatch is provided.

10. **[PR #2804](https://github.com/Hmbown/CodeWhale/pull/2804) (Closed): Surface subagent branch status**  
    Observability fix: the parent workspace branch/status chip refreshes when a sub-agent completes a shell tool call. Sub-agent workspace paths are now persisted across reloads.

---

## 5. Feature Request Trends

The community's direction coalesces around four major thrusts:

- **WhaleFlow Multi-Agent Orchestration**: The project's own vision documents (Issues #3230, #3229) point toward a full swarm/reduce pattern with fleet-ledger shared task lists, heterogeneous model workers, and synthesis passes. Users are asking for the promised orchestration layer to materialize.

- **Hardened Professional Workflows**: Developer sentiment strongly favors reliability features over novelty: automatic provider failover (#2574), proxy-aware networking (#3232), global config overlays (#3012), and accurate cost tracking across all providers (#3066) are all blockers for enterprise adoption.

- **Agent Transparency and Interactivity**: Users want agents to be more observable and interactive. Top requests include first-class clarification questions (#3102), explicit telemetry for token/context/resource budgets (#2666), and voice-based interaction (#3051). Agents operating as black boxes is increasingly seen as unacceptable for complex tasks.

- **Cross Provider/Platform Compatibility**: The tool's expansion beyond DeepSeek models is being hamstrung by specific incompatibilities: broken reasoning block parsing on MiniMax M3 bodies (#3222), unsupported providers like DeepInfra (#3231), and binary incompatibility on older Linux distributions (#1067, #3207).

---

## 6. Developer Pain Points

- **Stability Crisis**: The combination of the Windows TUI freeze (#1812), the YOLO "Turn stalled" error (#2487), and generic task hangs (#2739) is the single loudest complaint category. Multiple users explicitly state they are "abandoning the tool" or "unable to use it" due to freezing behavior.

- **Core Feature Unusability**: Key advertised capabilities remain broken for many. Sub-agent parallelism is gated by a 120-second hard timeout (#1806). Non-DeepSeek cost tracking returns `None` values (#3066). MCP-based workflows are haltingly unreliable on Windows (#1679).

- **Painful Migration Experience**: The `deepseek-tui` → `codewhale` transition has created significant friction: `deepseek update` silently breaks the PATH (#2917), `npm update` fails silently (#2924), and the release asset names are confusing (#3208).

- **Linux Distribution Lockout**: The mandatory glibc 2.39 dependency shuts out a large segment of the Linux user base on LTS distributions. Community members explicitly request builds for both glibc 2.35 (Ubuntu 22.04) and 2.39 (Ubuntu 24.04) to unblock deployment on servers and CI runners.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*