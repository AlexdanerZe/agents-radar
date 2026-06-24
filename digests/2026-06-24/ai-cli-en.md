# AI CLI Tools Community Digest 2026-06-24

> Generated: 2026-06-24 02:54 UTC | Tools covered: 9

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

# Cross-Tool Ecosystem Comparison Report: 2026-06-24

## 1. Ecosystem Overview

The AI CLI tools landscape is undergoing an intense phase of competitive maturation, defined by convergent priorities around agent reliability, MCP security standardization, and cost transparency. The primary battleground has shifted from raw model access to the determinism of autonomous execution—every major tool logged high-severity issues this week involving agent stalls, silent failures, or runaway token consumption. A clear bifurcation is emerging between deeply engineered "platform plays" (OpenAI Codex, Qwen Code) and highly iterative community-driven tools (Pi, DeepSeek TUI), while enterprise governance and cross-platform stability are proving to be universal pain points. Developers across the ecosystem are increasingly vocal: they trust the models but do not yet fully trust the agents, and they demand the tooling maturity to audit, control, and predict what their AI CLI does.

## 2. Activity Comparison

| Tool | Issues (Notable Activity) | PRs (Updated 24h) | Releases (24h) |
|---|---|---|---|
| **Claude Code** | High: 10 hot topics (#50270 51👍 Termux, #70165 iOS crash) | 1 (#20448) | v2.1.187 |
| **OpenAI Codex** | Highest: #28224 (333👍 logging), #25243 (46 comments macOS crash) | 10+ (#29736–#29767) | Rust-v0.143.0-alpha.3–12 |
| **Gemini CLI** | Moderate: #22323 false GOAL, #21409 hangs, #27635 SSRF | 10 (#27753–#28113) | None |
| **GitHub Copilot CLI** | High: #3892 FD leak, #3881 billing, #3901 WSL breakage | 1 (#3873) | v1.0.64 |
| **Kimi Code CLI** | Low: 1 issue updated (#2448 YOLO mode broken, 2 weeks open) | 0 | None |
| **OpenCode** | High: #4714 (35👍 TUI search), #19604 (Write silent fail) | 10 (#33571–#33281) | None |
| **Pi** | Highest: #5825 (30 comments scroll-lock), provider regressions | 10 (#6026–#6030) | v0.80.0 / .1 / .2 |
| **Qwen Code** | Highest: 37 issues updated, 50 active PRs | 10+ (#5788–#5550) | v0.19.1, v0.19.0 |
| **DeepSeek TUI** | High: #2487 turn stalled, #3461 MCP duplicates | 10 (#3521–#3533) | None |

## 3. Shared Feature Directions

The following requirements appear across **four or more** tool communities, indicating strong industry consensus:

- **Safe & Deterministic Autonomous Execution:** Configurable safety policies, subagent resource caps, and structured review gates (e.g., `git reset --force` guards, secret disclosure mandates, review policies). *Observed in: Claude Code, Qwen Code, Gemini CLI, DeepSeek TUI, GitHub Copilot CLI, Kimi Code CLI.*

- **Robust Cross-Platform & Mobile Support:** Demand for equal stability on Windows, macOS, Linux, WSL, ARM64 (Snapdragon/Apple Silicon), and mobile (Android Termux, iOS). *Observed in: Claude Code, OpenAI Codex, GitHub Copilot CLI, OpenCode, Pi.*

- **Cost & Token Inefficiency Resolution:** Real-time context estimates, efficient cache reuse (KV cache, prompt caching), prevention of runaway subagent token burn, and transparent logging discipline. *Observed in: Claude Code, OpenAI Codex, Qwen Code, Pi, Gemini CLI.*

- **MCP Security & Lifecycle Standardization:** Formal SSRF protections, credential isolation, cross-server resource scoping, and lifecycle management (no duplicate processes, clean teardown). *Observed in: Gemini CLI, DeepSeek TUI, Claude Code, Qwen Code, GitHub Copilot CLI.*

- **TUI/UX Professionalization:** Native session search, accessibility (a11y/contrast), internationalization (i18n), stable streaming layouts, and consistent input handling. *Observed in: OpenCode, Pi, Qwen Code, DeepSeek TUI, Claude Code, GitHub Copilot CLI.*

## 4. Differentiation Analysis

**Platform Layer vs. Application Tool.** OpenAI Codex and Qwen Code are investing heavily in architectural decoupling—extracting local graph stores, credential brokers, and marketplace governance layers. They are building platforms to host agent ecosystems. In contrast, Pi, DeepSeek TUI, and OpenCode focus on the terminal experience, session ergonomics, and multi-agent orchestration, competing on immediate developer delight rather than infrastructure breadth.

**Enterprise Governance Depth.** Claude Code and GitHub Copilot CLI lead on enterprise contracts: org-level model restrictions, sandbox credentials, EMU identity resolution, and usage analytics (despite outages). Their communities are raising issues about billing correctness and quota transparency, reflecting a paying-user base with sharp expectations. Gemini CLI competes here on security posture (SSRF hardening, CI/CD supply chain validation) rather than billing features.

**Engineering Velocity vs. Stability.** Pi shipped three releases in 24 hours to patch provider regressions, while DeepSeek TUI committed architectural enforcement for route resolution and MCP lifecycle. OpenAI Codex and Qwen Code maintain the highest sustained PR throughput (10+ architectural PRs daily). Kimi Code CLI shows the lowest velocity, with a critical YOLO mode regression open for two weeks and no PRs—a jarring contrast in a space where competitors ship multiple patches per week.

**Philosophical Stance on Autonomous Mode.** Some tools treat autonomy as a continuum needing review policies (DeepSeek TUI `#3144`, Qwen Code `#5550`), while others have suffered trust breakdowns from hard-coded YOLO promises (Kimi Code `#2448`). Claude Code and Gemini CLI are grappling with subagent orchestration failures—context bleed and false GOAL reports—that undermine the "delegation" model entirely.

## 5. Community Momentum & Maturity

- **Highest Engineering Velocity:** OpenAI Codex (10+ architectural PRs/day, credential broker, marketplace governance) and Qwen Code (50 active PRs, daemon platformization, safety hardening). Both are executing at a scale that widens their feature lead weekly.

- **Highest Iterative Responsiveness:** Pi rapidly addressed the v0.80.x provider regression crisis with three releases in hours, but the patch cycle points to a fragile core abstraction (`streamSimpleOpenAICompletions`). This speed is valued but tests user patience with instability.

- **Most Structured Governance:** Qwen Code (formal P2/P3 labeling, clear release branches, auto-publish to VS Code) and DeepSeek TUI (harvest merge policy, architectural enforcement gates) demonstrate mature open-source project management.

- **Strongest Enterprise Maturity Signals:** Claude Code (advanced org controls, detailed cost analysis discussions) and GitHub Copilot CLI (billing, EMU, identity management). Their communities are willing to pay but demand SLA-level reliability and transparent metering.

- **At-Risk Momentum:** Kimi Code CLI registers near-zero activity. A core feature regression (`--yolo`) open for 14+ days without a hotfix or PR signals stalled maintenance velocity.

- **Growing Architectural Sophistication:** OpenCode (shared schema extraction, ACP bridging), Gemini CLI (tool registry for evals), and Codex (local agent graph store, credential broker) are investing in the abstractions needed to make their tools extensible and testable at scale.

## 6. Trend Signals for Developers

- **Reliability is the New Feature.** The most-upvoted issues across the ecosystem are not feature gaps—they are agents stalling (`#2487`, `#21409`), burning tokens silently (`#65500`, `#28224`), or failing without feedback (`#19604`). Production trust is the defining competitive moat in 2026.

- **Autonomous Mode Requires Contracts, Not Just Permissions.** The community is rejecting simple "approve/deny" prompts in favor of review policies (`#3144`), subagent context caps (`#5734`), deterministic guardrails (`#5749`), and audit trails (`#20448`, `#3521`). Tools that cannot offer structured autonomous safety will lose professional users.

- **MCP Maturation is Accelerating. Watch the Security Backlash.** Gemini CLI's SSRF patch (`#28112`) and DeepSeek TUI's lifecycle fix (`#3524`) signal a shift from "connect anything" to "securely govern everything." Relying on unsecured MCP connections will be seen as negligent by late 2026.

- **Cross-Platform Rupture Remains an Unforced Error.** macOS system integrity crises (Codex `#25243`), WSL boot failures (Copilot `#3901`), Termux breakage (Claude Code `#50270`), and Desktop path mangling (OpenCode `#30895`) show that platform quality differentials are the fastest way to bleed user trust. Heterogeneous teams should test rigorously before committing.

- **Cost Control is a Competitive Moat.** Transparent context budgets (Pi `#6018`), efficient caching (Qwen `#5760`), and disciplined logging (Codex `#28224`) are table stakes. Tools that obscure cost telemetry or suffer silent token burn will lose the "run in production" vote.

- **Terminal as a Platform is the Next Frontier.** The push for daemonization (Qwen serve, Codex app-server), background session management (Pi Swarm, DeepSeek Fleet), and voice dictation (Qwen `#5755`) indicates the CLI is evolving into a persistent runtime. Developers evaluating tools should consider not just the session experience but the architecture for background operations, API extensibility, and long-running workflow resilience.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills Community Highlights Report, based on the `anthropics/skills` activity data.

---

## Claude Code Skills Community Highlights Report
**Data as of 2026-06-24 | Source:** `github.com/anthropics/skills`

### 1. Top Skills Ranking (Most-Attended Pull Requests)

The most-discussed Skill submissions reflect a community moving beyond proof-of-concept work into enterprise integration, developer tooling, and agentic memory.

1.  **Meta-Skills for Quality & Security ([PR #83](https://github.com/anthropics/skills/pull/83))**  
    *Author: eovidiu | Status: Open*  
    **Functionality:** Adds two evaluator skills—*skill-quality-analyzer* and *skill-security-analyzer*—to assess Skills across structure, documentation, and security dimensions.  
    **Discussion:** A maturing ecosystem signal; the community is actively building tooling to validate other tools rather than just submitting individual skills.

2.  **Document Typography Control ([PR #514](https://github.com/anthropics/skills/pull/514))**  
    *Author: PGTBoos | Status: Open*  
    **Functionality:** Prevents orphaned words, widow paragraphs, and numbering misalignment in AI-generated documents.  
    **Discussion:** High engagement because typographic issues affect virtually every generated document. Represents a universal quality-of-life request.

3.  **ODT / OpenDocument Format Skill ([PR #486](https://github.com/anthropics/skills/pull/486))**  
    *Author: GitHubNewbie0 | Status: Open*  
    **Functionality:** Full lifecycle support for .odt and .ods files—creation, template filling, and conversion.  
    **Discussion:** Addresses strong demand from the LibreOffice and open-standard ecosystem, which is underrepresented in the official skill set.

4.  **Frontend-Design Overhaul ([PR #210](https://github.com/anthropics/skills/pull/210))**  
    *Author: justinwetch | Status: Open*  
    **Functionality:** Revises the existing frontend-design skill for clarity and single-conversation actionability.  
    **Discussion:** Implicit critique of existing skills being too verbose or human-readable; the discussion pushes for operational precision rather than documentation-style text.

5.  **SAP-RPT-1-OSS Predictor ([PR #181](https://github.com/anthropics/skills/pull/181))**  
    *Author: amitlals | Status: Open*  
    **Functionality:** Integrates SAP’s open-source tabular foundation model for predictive analytics on ERP data.  
    **Discussion:** A clear enterprise demand signal, bridging LLM agents directly into SAP business data workflows.

6.  **Testing-Patterns Skill ([PR #723](https://github.com/anthropics/skills/pull/723))**  
    *Author: 4444J99 | Status: Open*  
    **Functionality:** Covers the full testing stack—Testing Trophy model, unit tests, React Testing Library, and E2E.  
    **Discussion:** One of the highest-commented skill additions; developer workflow automation is a core unmet need in the current collection.

7.  **Shodh-Memory (Persistent Context) ([PR #154](https://github.com/anthropics/skills/pull/154))**  
    *Author: varun29ankuS | Status: Open*  
    **Functionality:** Implements persistent memory across conversations via `proactive_context` calls and structured memory stores.  
    **Discussion:** Taps into the widespread desire for agentic state management without external infrastructure.

8.  **AppDeploy ([PR #360](https://github.com/anthropics/skills/pull/360))**  
    *Author: avimak | Status: Open*  
    **Functionality:** Deploys and manages full-stack web applications to a public URL directly from Claude.  
    **Discussion:** Represents the "agent-as-deployer" use case, bridging chat interfaces directly to production workflows.

---

### 2. Community Demand Trends (From Issues)

The top Issues by engagement reveal three converging demand vectors:

- **Toolchain Stability & Accuracy:** Issues [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169), and [#1061](https://github.com/anthropics/skills/issues/1061) all document the same critical blocker: `run_eval.py` returning `recall=0%` on every iteration, making the description optimizer unusable. Windows compatibility remains a recurring and vocal pain point.
- **Enterprise-Grade Security & Governance:** Issue [#492](https://github.com/anthropics/skills/issues/492) (trust boundary abuse via the `anthropic/` namespace) and Issue [#412](https://github.com/anthropics/skills/issues/412) (proposing an `agent-governance` skill) signal strong demand for safety patterns, permission models, and namespace integrity.
- **Org-Wide Sharing & Interoperability:** Issue [#228](https://github.com/anthropics/skills/issues/228) (enterprise skill sharing) and Issue [#16](https://github.com/anthropics/skills/issues/16) (exposing Skills as MCPs) show the community wants to break out of the single-user file-upload model and integrate Skills into standard enterprise infrastructure.
- **Memory & Context Management:** Issue [#1329](https://github.com/anthropics/skills/issues/1329) proposes a `compact-memory` skill using symbolic notation, mirroring the strong PR interest in persistent agent memory.

---

### 3. High-Potential Pending Skills

These active-comment PRs are likely to land soon and have the highest impact on ecosystem health:

- **Critical Optimization Engine Fixes ([PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1323](https://github.com/anthropics/skills/pull/1323)):** The 0% recall bug in `run_eval.py` is the #1 blocker for the entire skill development workflow. PR #1298 provides a multi-layered fix (artifact installation, Windows stream reading, trigger detection). PR #1323 specifically targets the trigger detection logic. These are the highest-value pending contributions.
- **Windows Platform Unlocks ([PR #1050](https://github.com/anthropics/skills/pull/1050), [PR #1099](https://github.com/anthropics/skills/pull/1099)):** These PRs fix subprocess hunting (`PATHEXT`) and pipe-reading crashes (`WinError 10038`) that make the toolchain inoperable on Windows. Merging them would unblock a significant portion of the developer base.
- **Testing-Patterns Skill ([PR #723](https://github.com/anthropics/skills/pull/723)):** A comprehensive, ready-to-merge skill filling a major gap in developer workflow capabilities.
- **Shodh-Memory Skill ([PR #154](https://github.com/anthropics/skills/pull/154)):** Persistent memory is the most conceptually ambitious pending skill, with strong community engagement around its implementation strategy.

---

### 4. Skills Ecosystem Insight

The community’s most concentrated demand is **resolving the fundamental `run_eval.py` feedback loop** to enable functional skill optimization, while simultaneously pushing for **enterprise-grade security, persistent agent memory, and cross-platform stability** to transform Skills from a promising concept into a robust, production-ready developer platform.

---

**Claude Code Community Digest | 2026-06-24**

---

### Today's Highlights
Anthropic pushed **v2.1.187** with enhanced enterprise security controls (`sandbox.credentials` and org model restrictions). However, the community is sounding alarms over a **critical iOS Remote Control crash regression** (#70165, #70382) that insta-crashes the app on session open. Meanwhile, the **Termux/Android breakage** (#50270) remains the most upvoted and discussed open issue, signaling deep frustration with the dropped glibc compatibility.

---

### Releases
**v2.1.187** was released in the last 24 hours.

- **`sandbox.credentials` setting**: Sandboxed commands are now blocked from reading credential files and secret environment variables.
- **Org-configured model restrictions**: Administrators can enforce model availability in the model picker, `--model`/`/model` flags, and the `ANTHROPIC_MODEL` environment variable.

---

### Hot Issues
1. **#50270 – v2.1.113+ broken on Termux/Android** (59 comments, 51 👍)
   A native glibc binary removed the working JS fallback. This is the single most upvoted and discussed issue in the tracker, and it continues to dominate conversation as unresolved.

2. **#70165 – iOS app hard-crashes opening Remote Control** (9 comments)
   Part of a major regression cluster with multiple duplicates (#70262, #70288, #70382, #70359). Tapping a session in the Code tab instantly crashes the app. Complete blocker for mobile Remote Control.

3. **#69238 – No response from API when Advisor is triggered** (19 comments, 33 👍)
   High upvotes. The Advisor pattern is a core differentiation for Claude Code; failing here erodes trust in the built-in "ask for help" escalation path.

4. **#50674 – Cowork fails on ARM64 (Snapdragon X) Windows** (26 comments)
   Passes readiness check but fails at runtime. A growing problem as ARM Windows laptops enter the developer hardware mix.

5. **#65500 – deep-research workflow aborts entire run, burning millions of tokens** (5 comments)
   A zero-output failure after consuming ~3.5M tokens. Schema-bound StructuredOutput failures in subagents abort the entire pipeline. Critical cost and productivity sink.

6. **#57751 – Subagents inherit parent prompt cache (~150K tokens) causing plan-mode bleed** (2 comments)
   Subagents cloning parent context leads to hallucinations and self-poisoning. A core architectural flaw in the agent dispatch model.

7. **#70459 – Auto-compaction: two compounding cost bugs** (2 comments, 2 👍)
   Technical deep-dive: stale precompute bloats conversations, and the prefix is repeatedly cache-created instead of cache-read, silently inflating token costs.

8. **#43255 – Chrome MCP tools domain navigation error** (16 comments, 8 👍)
   "Navigation to this domain is not allowed" error on all domains. Long-standing regression since v1.0.66 blocking MCP-based browsing.

9. **#11791 – Browser automation tools incompatible with web sandbox proxy** (8 comments, 14 👍)
   Playwright, Puppeteer, and Selenium cannot run inside the web sandbox due to missing HTTPS CONNECT tunneling support. Fundamental architectural limitation.

10. **#64503 – Claude Code Analytics not updated since May 12** (4 comments, 6 👍)
    A month-long analytics outage preventing cost tracking for teams. Significant for org-level usage monitoring.

---

### Key PR Progress
*Note: Only 1 pull request received updates in the last 24 hours.*

- **#20448 (OPEN) – Add web4-governance plugin for AI governance with R6 workflow**
  Proposes a plugin implementing T3 trust tensors, entity witnessing, and R6 audit trails for cryptographic provenance of agent actions. Currently has no community discussion (0 comments), but represents an exploration into verifiable accountability layers for the CLI.

---

### Feature Request Trends
1. **Mermaid Diagram Support (#14375):** The top-voted feature request (38 👍). Developers want native terminal rendering of flowcharts and diagrams without leaving the TUI.
2. **Internationalization (i18n):** A unified meta-issue (#70490) consolidates 5+ language-specific requests (Spanish, Chinese, Japanese, Korean, Portuguese). Strong community demand for non-English locale support.
3. **Accessibility (#70425):** An expert audit from a blind accessibility architect requesting audio cues, heading discipline, and screen-reader hooks. Detailed, actionable proposal.
4. **Bidirectional Hook API (#65179):** Advanced proposal to let hooks trigger session operations (like compaction) via a local server and per-invocation UUID, transforming hooks from read-only observers to active session participants.

---

### Developer Pain Points
- **Mobile & Cross-Platform Gaps:** The Termux/Android breakage (#50270) and the new iOS Remote Control crash regression (#70165) are the loudest unresolved issues. ARM Windows support (#50674) remains fragile.
- **Cost & Token Inefficiency:** Deep research aborting with zero output (#65500), auto-compaction bugs generating extra cache reads (#70459), and subagent context bleed (#57751) are eroding user trust in cost management.
- **UI/UX Regressions:** File delivery chips rendering as empty and unclickable across macOS, Windows, and Desktop app (#65677, #69780, #69279) is a recurring theme hurting the core user experience.
- **Core Workflow Reliability:** API errors on Advisor (#69238), raw `<invoke>` XML printed to terminal on Windows (#66160), and the Chrome MCP block (#43255) indicate testing gaps in critical user-facing paths.
- **Analytics Blindness:** The month-long analytics outage (#64503) is a significant pain point for teams managing and justifying Claude Code spend.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

OpenAI Codex Community Digest – 2026-06-24

---

### 1. Today's Highlights

The pipeline is churning hard with a dense wave of `rust-v0.143.0-alpha` releases, signaling active stabilization of the Rust middleware layer. The community is sharply focused on two critical tensions: a **macOS system integrity crisis** where Codex desktop is repeatedly exhausting `syspolicyd`, and persistent **SSD-destroying SQLite log churn** despite a significant hotfix that mitigated ~85% of writes. On the engineering front, OpenAI merged critical infrastructure for **plugin marketplace governance** and began landing the **experimental credential broker** for managed network proxies.

---

### 2. Releases

A rapid sequence of `rust-v0.143.0-alpha` builds (alpha.3 through alpha.12) were published within the last 24 hours. While individual changelogs for these alpha tags are sparse in the release notes, the high iteration cadence points to tight integration testing and rapid patching of the core Rust crates following the larger `v0.142.0` drop.

**Link:** [OpenAI Codex Releases](https://github.com/openai/codex/releases)

---

### 3. Hot Issues

**#1 — #28224 [OPEN]: SQLite feedback logs can write ~640 TB/year**
(*333 👍, 72 comments*)
The community’s highest-voted issue. The reporter updated the thread noting three PRs (#29432, #29457) have been merged, cutting logs by 85%. Still, the remaining baseline churn worries users running Codex on consumer SSDs.
[Issue #28224](https://github.com/openai/codex/issues/28224)

**#2 — #26892 [CLOSED]: GPT-5.5 listed as available but returns 404**
(*28 👍, 84 comments*)
A critical model-routing bug that lasted over two weeks. Local metadata claimed `gpt-5.5` was ready, but all backend API calls failed with `Model not found`. The closure implies a server-side fix.
[Issue #26892](https://github.com/openai/codex/issues/26892)

**#3 — #25243 [OPEN]: macOS relaunch loop exhausts syspolicyd file descriptors**
(*3 👍, 46 comments*)
A severe macOS issue where Codex enters an infinite relaunch cycle, locking up `syspolicyd` and preventing any app from launching until reboot. Wide user concern over system stability.
[Issue #25243](https://github.com/openai/codex/issues/25243)

**#4 — #16767 [OPEN]: Desktop triggers sustained syspolicyd/trustd CPU spikes**
(*26 👍, 19 comments*)
This issue tracks a separate but related macOS problem: just having Codex open pegs Apple’s security services indefinitely, drowning the CPU. High reaction count signals broad impact.
[Issue #16767](https://github.com/openai/codex/issues/16767)

**#5 — #28515 [OPEN]: "Model is at capacity. Please try a different model"**
(*3 👍, 7 comments*)
Paid users on `gpt-5.5 xhigh` frequently hitting hard capacity caps. Growing frustration that premium subscriptions are being throttled by backend capacity, breaking automation and long sessions.
[Issue #28515](https://github.com/openai/codex/issues/28515)

**#6 — #29532 [OPEN]: Persistent SQLite TRACE churn after `rust-v0.142.0`**
(*7 👍, 10 comments*)
A follow-up report on the logging problem. The user confirms `responses_websocket` logging dropped (good), but other TRACE targets continue to write heavily. Drafting a second wave of fixes.
[Issue #29532](https://github.com/openai/codex/issues/29532)

**#7 — #26011 [OPEN]: Windows stale MCP paths after auto-update**
(*0 👍, 6 comments*)
After Codex auto-updates on Windows, `config.toml` retains paths to old bin directories. This breaks the `node_repl` MCP server with `os error 3`. Demonstrates a brittle update mechanism.
[Issue #26011](https://github.com/openai/codex/issues/26011)

**#8 — #29374 [OPEN]: High CPU usage and overheating on Apple Silicon**
(*0 👍, 3 comments*)
Users on Darwin 25.5.0 arm64 report abnormally high CPU usage after launching Codex Desktop, leading to thermal throttling on Macs. Mirrors general performance regression reports.
[Issue #29374](https://github.com/openai/codex/issues/29374)

**#9 — #24445 [OPEN]: "You're out of Codex messages" despite 99% usage remaining**
(*0 👍, 3 comments*)
Business plan users hitting a hard false-positive rate-limit banner. Locking users out of the service completely despite having nearly full quota. Eroding trust in usage telemetry.
[Issue #24445](https://github.com/openai/codex/issues/24445)

**#10 — #15752 [OPEN]: Codex app crashes during task execution (Regression)**
(*1 👍, 6 comments*)
A previously fixed silent crash (#11016) has regressed in version `26.323.20928`. Users are wary of applying updates without clear regression test coverage on the core execution loop.
[Issue #15752](https://github.com/openai/codex/issues/15752)

---

### 4. Key PR Progress

**#1 — #29736: Inject agent graph store into ThreadManager**
(`wiltzius-openai`)
Moves lifecycle operations (spawn, close, resume, feedback) into an explicit `LocalAgentGraphStore` abstraction. This decouples the thread runtime from direct SQLite access and sets the stage for alternative backends.
[PR #29736](https://github.com/openai/codex/pull/29736)

**#2 — #29690 / #29753 / #29691: Marketplace source admission policy**
(`xl-openai`)
A multi-PR chain implementing TOML-driven marketplace source requirements. Prevents plugins from disallowed sources from being installed, listed, or refreshed across CLI, app-server, and migration flows. Core enterprise governance feature.
[PR #29690](https://github.com/openai/codex/pull/29690)

**#3 — #28034 / #29752: Experimental local credential broker**
(`winston-openai`, `viyatb-oai`)
A major security slice that moves injectable credentials behind the managed network proxy. Child processes can no longer read raw credentials directly; integration removes proxy-scoped dummy values when leaving network containment.
[PR #28034](https://github.com/openai/codex/pull/28034)

**#4 — #29758: Fix token-budget compaction baselines**
(`bolinfest`)
P2 review comments from the #29743 merge exposed a bug where pre-turn compaction captured context from the wrong model state under token-budget pressure. Fix ensures correct baselines are always used before model changes.
[PR #29758](https://github.com/openai/codex/pull/29758)

**#5 — #29762: Reuse compacted history for new context windows**
(`pakrym-oai`)
Fixes a consistency gap where `start_new_context_window` bypassed the centralized compacted-history path, missing critical item ID assignments. This prevents history corruption on fresh context windows.
[PR #29762](https://github.com/openai/codex/pull/29762)

**#6 — #29767: Assign response item IDs in forked history**
(`pakrym-oai`)
Fork-specific response items (like subagent usage hints) were appended directly, bypassing the `ItemIds` feature path. This PR ensures they get proper IDs, enabling correct reconstruction and persistence of forked conversations.
[PR #29767](https://github.com/openai/codex/pull/29767)

**#7 — #29778: Ensure app-server listener before proxying**
(`efrazer-oai`)
Introduces `--ensure-listener` mode for robust daemon lifecycle management. Uses Unix-socket probes and operation locking to guarantee the listener is ready before stdio proxy attaches.
[PR #29778](https://github.com/openai/codex/pull/29778)

**#8 — #29697: Attribute network requests to the exact exec on Linux**
(`jif-oai`)
Enhances observability by linking managed proxy connections back to the specific `exec` call that opened them. Crucial for debugging concurrent agent executions sharing the same proxy port.
[PR #29697](https://github.com/openai/codex/pull/29697)

**#9 — #29765: Ignore local curated plugins when remote catalog is active**
(`xl-openai`)
Suppresses conflicting `openai-curated` plugins when a remote catalog is active. Stops duplicate/incompatible plugins loading system-wide. Connects plugin load decisions to the Auth backend type.
[PR #29765](https://github.com/openai/codex/pull/29765)

**#10 — #29722 / #29721 / #29723: Domain type ownership migration**
(`anp-oai`)
A trio of clean-up PRs moving `ConfigLayer`/`AuthMode`/`ConnectorMetadata` types out of the app-server wire DTOs into their respective crates (`codex-config`, `codex-protocol`, `codex-connectors`). Reduces coupling and clarifies dependency direction.
[PR #29722](https://github.com/openai/codex/pull/29722)

---

### 5. Feature Request Trends

**Composer & Session UX:**
Users are requesting the ability to explicitly close "steers" (composer sessions) via an `X` button (#16015) and a simpler `Cmd+Enter` keybinding to submit messages (#16111). There is friction around the current modal UI for session management.

**Plugin & Skill Governance:**
Demand is rising for better plugin controls. The top requests include the ability to disable built-in features like the `@` chat search (#29231) and stable config pathing to prevent MCP breaks after auto-updates (#26011).

**Enterprise-Grade Git Workflows:**
A consistently highly-upvoted feature is a configurable `base_branch` in `environment.toml` (#15768, 7 👍). Teams working on `develop` or release branches want to avoid the hard-coded `main` default for worktrees.

**Model Interaction Discipline:**
A notable philosophical request (#29032) asks for Codex to enforce contract-first release discipline in long sessions, moving towards trustworthy, auditable autonomous coding rather than rapid prototyping defaults.

---

### 6. Developer Pain Points

**macOS System Integrity at Risk:**
This is the single loudest theme across the issue tracker. Codex Desktop is repeatedly triggering bugs in `syspolicyd` and `trustd` that result in relaunch loops (#25243), high CPU spikes (#16767), file descriptor exhaustion (#28071, #27662), and broken Gatekeeper (`spctl Too many open files`). These aren't just app crashes; they break the entire OS security model until a reboot.

**SSD-Destroying Disk I/O:**
The 640 TB/year SQLite log estimate (#28224) captured the community’s nightmare, but the reality is that even after the 85% fix, persistent low-level TRACE logging (#29532) continues to wear down drives. Developers are actively monitoring their disk usage as a Codex health metric.

**Brittle Update Mechanisms:**
Auto-updates consistently break user configurations. Windows users face broken MCP paths (#26011), mojibake in temporary directories (#28258), and plugin sync failures (#26792) after every MS Store update. This creates a systemic distrust of automatic update installation.

**Premium Service Unavailability:**
Paying users face a trifecta of reliability problems: model not found errors (#26892), hard "at capacity" restrictions (#28515), and false-positive out-of-messages banners (#24445). For a tool that's sold as a paid productivity multiplier, simply accessing the service reliably is a recurring daily battle.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

## Gemini CLI Community Digest — June 24, 2026

### 1. Today's Highlights
Security hardening dominates the commit log this week, with high-priority patches closing critical MCP SSRF vulnerabilities and a CI/CD supply chain attack vector. On the reliability front, a deeply concerning logic flaw was uncovered where sub-agents falsely report "GOAL" success after being abruptly terminated by turn limits (#22323). Finally, the model demonstrated impressive self-diagnosis capabilities when it identified and patched a ~90-second Windows startup delay caused by an eager `execSync` (#28106).

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Hot Issues
1. **#22323 Subagent recovery after MAX_TURNS reported as GOAL success** (P1, Bug, 8 comments) — A critical orchestration bug: when a sub-agent hits its maximum turn limit, the system wraps the result as `status: "success"` / `Termination Reason: "GOAL"`, silently masking the interruption. This deeply undermines agent reliability reporting.
2. **#21409 Generalist agent hangs** (P1, Bug, 8 👍) — Top-voted reliability blocker. Deferring to the generalist agent causes indefinite hangs even for trivial tasks like folder creation. The only workaround is disabling sub-agents entirely.
3. **#27635 SSRF via attacker-controlled OAuth metadata URLs** (P2, Security, Closed) — Critical security finding: `oauth-utils.ts` fetches URLs from MCP server responses without SSRF validation, allowing malicious servers to probe private networks. Drove a wave of follow-on MCP security PRs.
4. **#28106 Massive 50s+ startup delay on Windows** (P2, Bug) — An eager `execSync` in `EditorSettingsManager` during ESM import causes 90-second Windows startups. Notably, the model itself diagnosed and patched this, but it's a jarring UX out of the box.
5. **#25166 Shell command execution sticks on "Waiting input"** (P1, Bug, 3 👍) — High-frequency workflow killer: after a shell command finishes, the CLI hangs, falsely displaying `Awaiting user input`. Breaks iterative development flow.
6. **#21968 Gemini ignores skills and sub-agents** (P2, Bug, 6 comments) — A persistent capability gap. Custom skills (Gradle, Git, etc.) are almost never auto-selected; users must explicitly command the model to use them, severely limiting the extensibility feature's value.
7. **#26525 Add deterministic redaction & reduce Auto Memory logging** (P2, Security) — Architectural privacy concern: Auto Memory sends full local transcripts to the extraction model **before** any secrets redaction, meaning sensitive data enters model context regardless of the redaction prompt.
8. **#22093 Subagents running without permission since v0.33.0** (P2, Bug) — A configuration regression. An update caused sub-agents to run despite being disabled in all configs, frustrating users relying strictly on MCP.
9. **#22672 Agent should discourage destructive behavior** (P2, Feature, 1 👍) — Safety UX request: the model uses `git reset --force` or similar when safer alternatives exist. Community wants nudge/confirmation for high-risk operations.
10. **#27748 Shell awaiting input visual inconsistency** (P3, Bug) — Minor UX issue where the terminal shows `Shell awaiting input` while the action bar simultaneously reads `Action Required`, creating ambiguity about session state.

### 4. Key PR Progress
1. **#27753 CI: Validate workflow_run origin** (P1, Security, Closed) — High-severity supply chain fix. The E2E pipeline was vulnerable to fork-based artifact poisoning. Now strictly validates `workflow_run` context to prevent unauthorized code execution with repo secrets.
2. **#27971 Fix core: Strip thoughts from scrubbed history turns** (Security, Open) — Resolves "Thought Leakage" where the model's internal reasoning leaks into plain-text history, causing recursive monologues in future turns. A fundamental fix for context hygiene.
3. **#28103 Fix core: Avoid keep-alive socket reuse during OAuth** (P2, Security, Open) — Fixes a Node.js >= 24.17.0 regression that breaks "Sign in with Google" due to socket reuse throwing `ERR_STREAM_PREMATURE_CLOSE`.
4. **#27966 Fix security: Enforce case-insensitive sensitive path blocklist** (Medium, Open) — Solves a prompt-injection bypass by enforcing case-insensitive blocklisting for `.git`, `.env`, and `node_modules` to prevent path traversal attacks.
5. **#27964 Fix MCP: Scope resource resolution to prevent cross-server URI confusion** (Medium, Open) — Closes an MCP security gap where a malicious server could shadow a trusted server's URI due to an unscoped resolution fallback. Now fails closed on URI collisions.
6. **#28112 Fix MCP: Add SSRF protection to OAuth metadata discovery** (Large, Open) — Directly addresses #27635 by porting SSRF protections (`isLoopbackHost`, DNS validation) from the main web-fetch utility into the MCP OAuth flow.
7. **#27914 Fix CLI: Don't offer to resume unsaved sessions** (P2, Open) — Quality-of-life fix: when an `ENOSPC` error prevents saving, the exit prompt no longer incorrectly offers to `--resume` the unsaved session.
8. **#28113 Feat/tool registry discovery** (Large, Open) — Infrastructure for evals. Creates a formal registry of built-in tools and enables AST extraction of tool names in assertions, improving evaluation fidelity.
9. **#28099 Fix CLI: Show descriptive sandbox label in footer** (P2, Open) — macOS UX improvement: the footer now displays the specific seatbelt profile name instead of the generic "current process" string.
10. **#27771 Fix MCP header encoding for non-ASCII values** (P2, Closed) — Critical for international users. MCP discovery now correctly encodes headers with Unicode characters (e.g., `mąka`) as `ByteString` values, preventing connection failures.

### 5. Feature Request Trends
- **Self-Aware Agent Infrastructure (#21432, #22598, #22745):** A strong push for the agent to understand its own mechanics—accurately reporting its flags, hotkeys, and internal tooling. There is specific demand for AST-aware code manipulation to reduce token waste and for subagent trajectory sharing to improve debugging and evaluation.
- **Professionalized Evaluation & Testing (#24353, #23313, #28113):** The team is scaling up "behavioral eval" infrastructure. Requests for a formal tool registry and robust, repeatable steering tests indicate a move toward CI-native quality gates for agent behavior.
- **Secure & Non-Spammy Memory Layer (#26522, #26523, #26525):** Auto Memory is being hardened from experiment to production. Core requests include guaranteeing secrets never enter model context, preventing infinite retries on low-signal data, and transparent handling of corrupted memory patches.
- **Third-Party Integration Safety (MCP) (#27635, #27964, #22232):** As MCP usage grows, so does security focus. Users want explicit SSRF protection, strict resource isolation between servers, and resilience features like automatic session lock recovery for the browser agent.

### 6. Developer Pain Points
- **Agent Freezes & Silent Failures:** The loudest complaint remains the agent getting stuck—whether the generalist hangs, sub-agents silently hit turn limits, or shell commands falsely report "awaiting input." These stalls directly kill developer productivity and trust.
- **Configuration Is Ignored:** A profound trust deficit. Skills are rarely auto-used, agent permissions are overridden after updates, and `settings.json` overrides are silently ignored by sub-agents. Users feel they cannot effectively constrain the tool.
- **Terminal & Windows Roughness:** Windows users experience ~90-second startup delays. General terminal flickering on resize and corruption after external editor usage points to a rendering layer needing better performance and statelessness.
- **Destructiveness & Cleanup:** The model's tendency to randomly script files across the workspace and use `--force` flags is a major nuisance. Developers want sandboxing or undo mechanisms before the tool alters critical files.
- **Debugging Black Holes:** When things go wrong (e.g., agent hang, false GOAL report), the `/bug` report lacks subagent context. The lack of visibility into internal agent decision-making is a recurring frustration.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — June 24, 2026

## Today's Highlights
The v1.0.64 release landed yesterday with welcome improvements to path access transparency (symlink resolution) and pay-as-you-go budget UX. However, the update appears to have introduced regressions, most notably a complete launch failure on WSL ([#3901](#)) and a UI-thread freeze caused by synchronous secret scanning ([#3900](#)). Meanwhile, a critical resource leak in session-state management ([#3892](#)) and a potential billing miscalculation ([#3881](#)) have raised serious concerns among power users. The community is closely watching how the team responds to these stability and correctness issues.

---

## Releases
**v1.0.64** — *June 23, 2026*

- **Path access prompts now show resolved symlink targets**, giving users full visibility into exactly which paths are being granted access. This is a meaningful security/transparency improvement for agentic workflows.
- **Pay-as-you-go budget UI enhancements**: the additional usage budget is now shown on launch, refreshes after a request is rejected for hitting the spend limit, and displays a friendly message when the limit is reached. A nice polish for billing UX.

*No other releases in the last 24 hours.*

---

## Hot Issues
Top 10 noteworthy issues from the last 24 hours, with context and community reaction.

**1. [#3892 — Copilot CLI never prunes `~/.copilot/session-state`, causing EMFILE / file-descriptor exhaustion (crashes VS Code Copilot Chat)](https://github.com/github/copilot-cli/issues/3892)**
A critical resource leak. Session state accumulates unboundedly and can crash VS Code Copilot Chat on heavily used machines. *No comments yet, but this is a top-tier stability concern for daily users.*

**2. [#3881 — Billing bug: charged 5% instead of 2% (6x multiplier incorrectly applied)](https://github.com/github/copilot-cli/issues/3881)**
User reports quota decreased by 5% for a single request with a 6x multiplier model, when it should have been 2%. Direct financial impact on paying users. *High urgency, developer explicitly asking for a 3% refund.*

**3. [#3901 — Copilot cannot launch from WSL after upgrading to v1.0.64](https://github.com/github/copilot-cli/issues/3901)**
Freshly filed, zero comments, but a full breakage on WSL for an entire user segment makes this a hot candidate for immediate triage. *Breaking change regression.*

**4. [#3900 — Secret filtering can block the CLI UI thread](https://github.com/github/copilot-cli/issues/3900)**
Synchronous secret scanning on large response objects causes the TUI to freeze. The author notes single-threaded scanning with recursive parsing is the root cause. *Performance regression in a security feature.*

**5. [#3501 — Scroll bar makes text unalign on Windows](https://github.com/github/copilot-cli/issues/3501)**
Ongoing Windows rendering regression introduced with the vertical scroll bar. **9 upvotes** across the community, demonstrating broad frustration. *Platform-specific UX regression.*

**6. [#3866 — Thinking/reasoning text is unreadable on dark backgrounds](https://github.com/github/copilot-cli/issues/3866)**
Hardcoded dark gray foreground used for "Thinking..." reasoning text is invisible against dark terminal themes. An **accessibility** and theming regression affecting a significant subset of users.

**7. [#3897 — Copilot CLI incorrectly selects the wrong authenticated GitHub account](https://github.com/github/copilot-cli/issues/3897)**
Multi-account (EMU + personal) users face 403 push failures because the CLI picks the wrong identity. Enterprise customers are heavily impacted.

**8. [#3894 — `agentStop` triggering on subagent turns causes `/review` to never finish](https://github.com/github/copilot-cli/issues/3894)**
A custom hook registered on `agentStop` is re-triggered on subagent termination, causing the parent `/review` command to hang indefinitely. *Breaks advanced agent orchestration.*

**9. [#3731 — Allow option to restore `web_fetch` access to private networks](https://github.com/github/copilot-cli/issues/3731)**
v1.0.60 blocked agents from fetching internal corporate URLs. Enterprise users are asking for a controlled opt-in. *Ongoing discussion, enterprise blocker.*

**10. [#2590 — Plugins installed via a Marketplace aren't available via ACP](https://github.com/github/copilot-cli/issues/2590)**
Feature parity gap between the CLI and Agent Client Protocol. MCP servers and agents work in the CLI but are invisible to ACP-connected clients. *3 upvotes, community wants a unified plugin model.*

---

## Key PR Progress
PR activity was light in the last 24 hours, with only one pull surfacing in the update window.

**1. [#3873 — Add initial console log for greeting](https://github.com/github/copilot-cli/pull/3873)**
*Author: EverydayEvertime | Status: Open | Comments: 0*
A very thin PR adding a basic console log greeting. No discussion or review activity yet. This does not appear to be a major feature or fix and likely requires further refinement from the author.

*Note: No other pull requests received an update in the last 24 hours. Most active development work appears to be happening on the issue triage and release stabilization front.*

---

## Feature Request Trends
Distilled from all issues, the community is pushing hard on several recurring directions:

- **Scheduling & Automation (#2056):** Recurring/scheduled prompts for agentic workflows. Users want the agent to act without waiting for manual "send message" triggers.
- **MCP & Plugin Ecosystem Maturity (#3893, #3889, #2590):**
    - Collision warnings when MCP servers share names across plugins.
    - stdio transport support in ACP mode (protocol compliance gap).
    - Full plugin parity between CLI and ACP.
- **Enterprise Controls (#3731, #3712, #3897):**
    - Restoring private network `web_fetch` access with safe opt-ins.
    - Correct multi-account identity resolution.
    - Documentation for sandbox/ReFS limitations on Windows.
- **Accessibility & Theming (#3866, #3898):** Far more attention is being paid to terminal color contrast and custom background support. This is becoming a recurring friction point.
- **Voice & Dictation UX (#3896):** Push-to-talk is gaining adoption, but edge cases around typing during transcription finalization are driving feature requests for better input state management.

---

## Developer Pain Points
Recurring frustrations and high-frequency bugs visible in the current data:

- **Post-Update Regressions:** v1.0.64 broke WSL launches for some users (#3901), introduced secret-scanning UI freezes (#3900), and existing issues with Windows scroll bar alignment persist. The community is wary of the release cadence stability.
- **Resource Leaks:** The session-state folder explosion (#3892) is a textbook unbounded growth issue that can take down co-processes.
- **Billing & Quota Correctness:** The 5% vs. 2% billing bug (#3881) erodes trust in metering accuracy, a highly sensitive topic for paying subscribers.
- **Identity & Configuration Confusion:** Multi-account push failures (#3897) and silent drops of BYOK model overrides on subagents (#3891) frustrate advanced and enterprise users seeking deterministic behavior.
- **Cross-Platform Gaps:** Windows has a disproportionate share of rendering and filesystem (ReFS, Dev Drive) issues. WSL, while powerful, remains fragile across updates.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-24**

**1. Today’s Highlights**
Activity in the `MoonshotAI/kimi-cli` repository was sparse today, with no new releases or pull requests recorded in the last 24 hours. The single noteworthy signal is an unresolved regression in v0.12.0 (Issue #2448) where the `--yolo` autonomous mode fails to suppress approval prompts, directly breaking unattended workflows for power users.

**2. Releases**
*None.* No new version tags or release artifacts were published in the last 24 hours.

**3. Hot Issues**
*The provided data snapshot for the last 24 hours contains one updated issue. It is analyzed below.*

1. **[[Bug] Kimi CLI is prompting for approval in yolo mode (#2448)](https://github.com/MoonshotAI/kimi-cli/issues/2448)**
   - **Author:** iaindooley
   - **Status:** Open | Created: 2026-06-10 | Updated: 2026-06-23
   - **Environment:** Debian, API Key, Model `k2.6`, Kimi Code v0.12.0
   - **Why it matters:** `--yolo` mode is the core feature for agentic and CI/CD integrations. A bug that causes the CLI to halt for confirmation despite being in autonomous mode directly negates the value of the feature and blocks scripting use cases. The bug has persisted for two weeks, suggesting the fix may involve a non-trivial change in how execution safety prompts are gated.
   - **Community reaction:** Public discussion is minimal (1 comment, 0 reactions). This may indicate a narrow reproduction scenario or that the broader user base has not yet stress-tested YOLO mode. The absence of noise does not reduce the severity for affected pipelines.

**4. Key PR Progress**
*No pull requests were updated, opened, or merged in the repository within the 24-hour window.* The project may be in a stabilization phase or undergoing internal refactoring with limited external visibility.

**5. Feature Request Trends**
The dominant implicit request from the available signal is a demand for **hardened, unconditional autonomous execution**. The `--yolo` contract must be ironclad—approval prompts should be completely suppressible regardless of the underlying model, system environment, or requested operation. Beyond the fix itself, developers would benefit from a clearly documented guarantee of which safety prompts YOLO mode overrides and which (if any) are always non-negotiable.

**6. Developer Pain Points**
- **Broken Automation Contracts:** The primary frustration is the unreliability of `--yolo`. Users integrating the CLI into automated systems cannot trust a flag that advertises zero interaction but still halts on approval requests.
- **Patch Velocity Concerns:** An open, high-severity bug since June 10th without a hotfix release raises questions about the triage speed for regressions in core execution modes.
- **Quality Verification Gap:** The existence of this regression in a stable release (v0.12.0) suggests a gap in testing autonomous flag edge cases across different platforms (Debian in this case) and authentication methods (API key vs. web login).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — June 24, 2026

## 1. Today’s Highlights
A significant architectural clean-up landed today with the extraction of shared public schemas (`@opencode-ai/schema`) and the removal of several schema-forwarding facades. On the bug-fix front, the long-running ACP `question` tool hang has been patched, and the desktop app received multiple UX fixes for tab stability and notification state. The community is rallying hard around TUI search capabilities, session recovery after sleep, and rising alarm over the `Write` tool's silent failure on large files.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues

**#4714 — [FEATURE] TUI Search for string in session buffer**  
The top-voted issue (35 👍, 28 comments). Users are demanding a native `find` command equivalent to what you get in a text editor. This is the single biggest UX gap for the TUI right now.  
[Link](https://github.com/anomalyco/opencode/issues/4714)

**#19604 — Write tool fails silently on ~1000+ line files**  
A high-severity reliability bug. The `Write` tool returns a failure with zero error messages on large files. Users report multiple retries produce the same result. Trust in file operations is at stake.  
[Link](https://github.com/anomalyco/opencode/issues/19604)

**#14212 — Support more DBMS for state storage**  
Strong demand (21 👍) for Postgres and other databases. The Drizzle migration opened the door, and power-users are eager to run OpenCode against centralized state backends rather than SQLite only.  
[Link](https://github.com/anomalyco/opencode/issues/14212)

**#32747 — @ file mentions don't include files created after startup**  
A daily workflow blocker: newly created files are invisible to the `@` picker until a full restart. The submitter traced it to stale search state in the TUI.  
[Link](https://github.com/anomalyco/opencode/issues/32747)

**#15431 — macOS lock screen freezes session**  
Long-running tasks appear "In Progress" but are completely frozen after the user unlocks. No further output is received. A critical pain point for anyone treating OpenCode as a daemon.  
[Link](https://github.com/anomalyco/opencode/issues/15431)

**#17173 — OpenCode Go performance is abysmal**  
Users report extreme latency starting agents and executing tool calls. The performance degradation appears systemic on certain provider routes (e.g., GLM).  
[Link](https://github.com/anomalyco/opencode/issues/17173)

**#30895 — Desktop v1.16.0 converts WSL `/mnt/c/` paths to Windows paths**  
A regression specific to the desktop app when connecting to a WSL server. Correct WSL paths are mangled into Windows `C:\` paths, breaking file access and session lists entirely.  
[Link](https://github.com/anomalyco/opencode/issues/30895)

**#33568 — [FEATURE] CMD+Send to submit (Mac)**  
Small but telling: Mac users want standard `CMD+Enter` to send, with plain `Enter` for newlines. High-frequency ergonomics request.  
[Link](https://github.com/anomalyco/opencode/issues/33568)

**#31453 — Add `/export` to Desktop app**  
The TUI has it, the Desktop app does not. Feature parity gap blocking session portability for desktop users.  
[Link](https://github.com/anomalyco/opencode/issues/31453)

**#23287 — Recovery of agentic workflow after system wakeup**  
Reinforces the lock-screen freeze theme. Users want the Desktop app to gracefully recover or resume tasks after a laptop wakes from sleep, not just sit frozen.  
[Link](https://github.com/anomalyco/opencode/issues/23287)

## 4. Key PR Progress

**#33571 — Extract shared public schemas**  
Creates a private `@opencode-ai/schema` package housing canonical public types (Agent, Session, Provider, etc.). Replaces `Schema.Class` with `Schema.Struct` for better construction and decoration. Major step toward a stable API boundary. [Link](https://github.com/anomalyco/opencode/pull/33571)

**#33577 — Remove schema forwarding facades**  
Companion cleanup that drops indirect filesystem, integration, and permission schema modules in favor of direct canonical imports. Preserves behavior-bearing domain APIs while removing indirection. [Link](https://github.com/anomalyco/opencode/pull/33577)

**#33569 — Make session navigation stable and fast**  
Keeps the previous coherent session painted until destination placement is ready—no loading screen flash. Reuses bounded server/session placement and preloads adjacent tabs. [Link](https://github.com/anomalyco/opencode/pull/33569)

**#33576 — Throttle directory tree loading**  
Limits Open Project tree listings to three concurrent requests. Prioritizes newly opened folders over eager preloads and skips stale queued work after navigation. [Link](https://github.com/anomalyco/opencode/pull/33576)

**#33566 — Keep prompt state in tabs**  
Adds non-persisted lifecycle-managed state per titlebar tab so prompt text doesn't vanish when switching sessions in the new layout. [Link](https://github.com/anomalyco/opencode/pull/33566)

**#33482 — Bridge ACP question prompts via extMethod**  
Fixes the `question` tool hanging forever in ACP mode. The `Deferred` was waiting for an answer that never arrived; this PR routes it through the ACP client correctly. Closes #17920 and #13752. [Link](https://github.com/anomalyco/opencode/pull/33482)

**#33560 — Simplify OpenCode connection flow**  
Routes onboarding directly to the OpenCode Console URL, auto-selects the first organization alphabetically, and renames auth methods ("OpenCode Console account" vs. "API key (service account)") for clarity. [Link](https://github.com/anomalyco/opencode/pull/33560)

**#33562 — Map providers to integrations**  
Wires an optional `integration_id` to provider metadata so catalog availability and LLM credentials resolve through the mapped integration. Infrastructure for a more modular identity layer. [Link](https://github.com/anomalyco/opencode/pull/33562)

**#32370 — Linux clipboard selection**  
Implements native Linux copy-on-select / middle-click-to-paste behavior, fixing #29963. Long-standing platform gap finally closed. [Link](https://github.com/anomalyco/opencode/pull/32370)

**#33281 — Standalone v2 session flow in CLI**  
Adds `--standalone` mode that spawns an authenticated private server child process for the TUI. Creates sessions through the v2 API and loads state via `DataProvider`. Significant investment in the CLI experience. [Link](https://github.com/anomalyco/opencode/pull/33281)

## 5. Feature Request Trends

- **Session Resilience & Recovery**: The cluster of login-lock-screen freezes (#15431), wake-from-sleep hangs (#23287), and "Worker terminated" crashes (#32694) makes clear the community wants OpenCode to behave like a robust long-running daemon, not a fragile REPL.
- **Search & Retrieval**: Issue #4714 (TUI search) dominates the voting. Users need to search agent output, not just file names. This is the top unmet UX need.
- **Desktop / TUI Parity**: `/export` (#31453), keybind customization (#33568), and session persistence differences continue to surface. The Desktop app is catching up but has not reached full feature parity.
- **Enterprise / Team Scope**: Requests for Postgres storage (#14212), granular per-agent tool permissions (#17607), hierarchical plans (#13928), and plugin API stability (#24065) signal a maturing user base that needs governance and scale.
- **Context Freshness**: Stale file mentions (#32747) point to a broader desire for live, reactive context that stays in sync with the filesystem without manual restarts.

## 6. Developer Pain Points

- **Silent Failures Wear Down Trust**: The `Write` tool returning no error on large file writes (#19604) is the loudest example, but the pattern appears elsewhere (ACP hangs, provider errors swallowed). Debugging these "ghost" failures is a major time sink.
- **Session State Is Too Fragile**: Losing sessions on terminal close (#26505), getting frozen output on screen lock (#15431), and hard crashes (#32694) make long agent sessions feel risky rather than reliable.
- **Performance Not Keeping Pace**: "Abysmal" (their words) performance on OpenCode Go (#17173) and lag in directory navigation (#33576's driver) highlight backend/ network bottlenecks that directly impact the developer's flow state.
- **Cross-Platform WSL Pain**: The v1.16.0 path regression (#30895) is just the latest in a string of WSL-specific bugs (#7297, #9776). WSL users feel like second-class citizens after every major release.
- **Provider & Plugin Configuration Friction**: Custom headers not applying (#15306), sub-agent model errors (#21615), and undocumented but functional plugin API internals (#24065) show the configuration surface has grown faster than its documentation.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

## Pi Community Digest – 2026-06-24: Patch Cycle Hits Hard, Multi-Agent Focus Intensifies

---

### 1. Today's Highlights
The Pi project shipped **v0.80.2** just hours after v0.80.1, fixing provider-regression chaos that broke Nvidia, DeepSeek, and Cloudflare Workers integrations. A major TUI streaming scroll-lock bug (#5825) is drawing the most community heat (30 comments) with a dedicated fix already in review (#6026). Meanwhile, the community is rapidly converging on multi-agent orchestration as the next pillar feature, with multiple issues and PRs targeting AgentSwarm UX, naming conventions, and real-time status visualization.

---

### 2. Releases
Three releases landed within the last 24 hours under the v0.80.x line:

- **v0.80.2** (Latest): Changed the inherited `pi-ai` `ApiKeyCredential` discriminator to `"api_key"` with provider-scoped env values for full `auth.json` compatibility. Renamed the inherited agent-core shell execution option type.
- **v0.80.1**: Fixed Amazon Bedrock `AWS_PROFILE` endpoint resolution, Fireworks Anthropic-compatible session-affinity defaults, and Together AI compatibility.
- **v0.80.0**: Added `Ctrl+J` default newline binding, renamed `zai` provider label to "ZAI Coding Plan (Global)", and overhauled the `pi-ai` global API (`stream`/`complete`/`completeSimple`).

[View releases](https://github.com/earendil-works/pi/releases)

---

### 3. Hot Issues (10 of 30 updated in last 24h)

1. **#5825 – Streaming markdown forces scroll to bottom (OPEN, 30 comments)**
   A controversial TUI regression where Pi hard-scrolls to the bottom during streaming if `clear on shrink` is enabled. Users report it makes reading previous context essentially impossible while a response is in flight. A dedicated fix PR (#6026) is already in review.
   [earendil-works/pi#5825](https://github.com/earendil-works/pi/issues/5825)

2. **#6020 – DeepSeek provider not working in 0.80 (CLOSED, 11 comments)**
   DeepSeek fails with a deserialization error: messages with a `developer` role are sent to an API that only accepts `system`, `user`, or `assistant`. A rapid iteration upstream invalidated the role assumption.
   [earendil-works/pi#6020](https://github.com/earendil-works/pi/issues/6020)

3. **#6016 / #6017 – Nvidia & local models broken (CLOSED, 7+3 comments)**
   A critical shared error — `streamSimpleOpenAICompletions is not a function` — affecting Nvidia plugin users and local model runners (Ollama/LM Studio) on 0.80.1. Forced rollbacks to 0.79.10 across the community.
   [earendil-works/pi#6016](https://github.com/earendil-works/pi/issues/6016) | [#6017](https://github.com/earendil-works/pi/issues/6017)

4. **#6002 – SessionManager.open() silently truncates non-session files (OPEN, 2 comments)**
   A data-safety critical bug: pointing `--session` at a large NDJSON log file silently truncates it to a 133-byte session header with no warning, error, or backup. Heavy community concern about trust in session handling.
   [earendil-works/pi#6002](https://github.com/earendil-works/pi/issues/6002)

5. **#5700 – Support multiple live agent sessions with TUI switching (CLOSED, 8 comments)**
   A highly-requested capability for background/parallel agent sessions. Users want `switchSession` to preserve state instead of tearing down, enabling concurrent workflows without losing context.
   [earendil-works/pi#5700](https://github.com/earendil-works/pi/issues/5700)

6. **#5989 – Extension pi-lovely-codex broken by update (CLOSED, 6 comments)**
   A community extension that was working hours earlier fails completely after a core update. Highlights the fragility of the extension ecosystem when core APIs shift without migration notices.
   [earendil-works/pi#5989](https://github.com/earendil-works/pi/issues/5989)

7. **#5730 – Expose raw provider responses in hooks (CLOSED, 4 comments)**
   Developers want `after_provider_response` to expose the full raw body, not just status/headers. Essential for debugging proxy issues and building advanced extension logic.
   [earendil-works/pi#5730](https://github.com/earendil-works/pi/issues/5730)

8. **#6021 – Cloudflare Workers.AI 404 on 0.80.1 (CLOSED, 1 comment)**
   Endpoints fail because `{CLOUDFLARE_ACCOUNT_ID}` in the base URL is being passed as a literal string instead of being interpolated.
   [earendil-works/pi#6021](https://github.com/earendil-works/pi/issues/6021)

9. **#5996 – Footer rendering breaks when session name contains newlines (CLOSED, 4 comments)**
   LLM-generated session names with `\n` characters cause the TUI footer to render across multiple terminal rows, leaking content outside the editor box. Fixed in PR #5999.
   [earendil-works/pi#5996](https://github.com/earendil-works/pi/issues/5996)

10. **#5976 – /model replaces defaultModel silently (CLOSED, 2 comments)**
    The `/model` command mutates the persistent `defaultModel` setting rather than the active session model only. Users report losing their default configuration without realizing it.
    [earendil-works/pi#5976](https://github.com/earendil-works/pi/issues/5976)

---

### 4. Key PR Progress (10 of 12 updated in last 24h)

1. **#6026 – fix(tui): stabilize working status row (OPEN)**
   Directly addresses the #5825 scroll-lock regression by stabilizing the TUI status row rendering during streaming. A high-priority fix for the UX regression of the week.
   [earendil-works/pi#6026](https://github.com/earendil-works/pi/pull/6026)

2. **#5262 – feat(ai): add Anthropic Vertex provider (OPEN)**
   A major new built-in provider integrating Claude on GCP Vertex AI using `AnthropicVertex` SDK. Reuses the existing Anthropic Messages streaming path. Significant scope, still open for review.
   [earendil-works/pi#5262](https://github.com/earendil-works/pi/pull/5262)

3. **#5832 – fix(ai): surface provider HTTP error body (OPEN)**
   Ensures error bodies from proxies/gateways are passed to the user rather than suppressed into opaque SDK messages. Fixes #5763 and dramatically improves debugability for enterprise/proxy setups.
   [earendil-works/pi#5832](https://github.com/earendil-works/pi/pull/5832)

4. **#6018 – feature(coding-agent): show context estimates in session tree (OPEN)**
   Adds a context usage estimate column to the Session Tree view. Helps users quickly identify heavy entries and understand where their context window budget is going.
   [earendil-works/pi#6018](https://github.com/earendil-works/pi/pull/6018)

5. **#5999 – fix(coding-agent): normalize session names (CLOSED)**
   Sanitizes newlines from LLM-generated session names, resolving the TUI footer layout breakage described in #5996.
   [earendil-works/pi#5999](https://github.com/earendil-works/pi/pull/5999)

6. **#5784 – fix(coding-agent): sort threaded sessions by latest activity (CLOSED)**
   Threaded mode now sorts sessions by the most recent message in the entire subtree rather than the root session modification date. Much more practical for long-running forked workflows.
   [earendil-works/pi#5784](https://github.com/earendil-works/pi/pull/5784)

7. **#5526 – Require terminal events for OpenAI Responses streams (CLOSED)**
   Fixes random stream stalling in OpenAI responses by strictly requiring terminal response events before considering a stream complete. Resolves persistent "continue" typing issues.
   [earendil-works/pi#5526](https://github.com/earendil-works/pi/pull/5526)

8. **#6004 – feat: Normalize modern Microsoft Foundry endpoints (CLOSED)**
   Updates URL normalization to handle modern `*.ai.azure.com` style Foundry endpoints, fixing base endpoint compatibility issues.
   [earendil-works/pi#6004](https://github.com/earendil-works/pi/pull/6004)

9. **#5994 – fix(ai): route OpenCode Go models through Anthropic (CLOSED)**
   Corrects model routing for OpenCode endpoints exposing Anthropic-compatible metadata (e.g., `minimax-m2.7`) so they use the Anthropic Messages API instead of the OpenAI compatibility path.
   [earendil-works/pi#5994](https://github.com/earendil-works/pi/pull/5994)

10. **#6030 – fix(coding-agent): print benchmark timings after TUI stop (OPEN)**
    Prevents benchmark output from overlapping with the TUI rendering by flushing timing stats to stdout after the TUI shuts down cleanly. Developer tooling improvement.
    [earendil-works/pi#6030](https://github.com/earendil-works/pi/pull/6030)

---

### 5. Feature Request Trends

- **Multi-Agent Swarm as First-Class UX**: The highest volume of new feature discussion centers on making `AgentSwarm`/`AgentTeam` accessible from the default workflow. Specific proposals include dedicated slash commands (`/swarm`, `/swarm-team`), real-time TUI agent-state visualization, and consistent brand naming (e.g., `SwarmTeam`) — see issues #6011, #6012, #6013, #6014.
- **Provider Expansion & Intelligent Routing**: Strong demand for additional built-in providers (Merge Gateway, Anthropic Vertex, MiniMax) combined with smarter automatic selection of API protocol (Anthropic vs OpenAI) based on model metadata, not manual configuration.
- **Deep Extension Hooks**: Users continuously request full raw HTTP response access in lifecycle hooks (#5730) to build richer MCP integrations, custom logging, and proxy debugging.
- **Session Visibility & Protection**: Features improving session tree display (context estimates, threaded sort by activity) and protecting against accidental data destruction (#6002) are gaining traction as the tool handles more complex long-running workflows.

---

### 6. Developer Pain Points

- **Provider Regression Cycle**: The v0.80.x line has been particularly unstable. DeepSeek, Nvidia, Cloudflare, Fireworks, Together, and local providers have all broken across the last three patches. The shared `streamSimpleOpenAICompletions` abstraction appears to be a single point of failure affecting multiple providers simultaneously.
- **Data Loss Exposure**: The `SessionManager.open()` silent truncation bug (#6002) is a critical trust issue, especially for users who pipe NDJSON data into pi. Even though isolated to CLI usage, it raises broader concerns about session ingestion robustness.
- **Extension Ecosystem Fragility**: Community extensions breaking between minor patches (#5989) creates maintenance burden and user frustration. The lack of a formal API stability guarantee or migration notice in changelogs is a recurring complaint.
- **TUI Polish Gaps Beyond the Major Bug**: Persistent annoyances like brittle footer rendering, unwanted mutation of persistent settings, lack of hardware cursor management on terminal blur, and broken long-URL clickability collectively erode the "premium terminal app" experience.
- **Enterprise/Proxy Debugging**: Error bodies from gateways and proxies are frequently swallowed as opaque SDK messages, making the tool difficult to troubleshoot in corporate network environments (#5832).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-24

### 1. Today’s Highlights
The project shipped v0.19.1 stable, adding MCP resource completions and server discovery, while the community kept up intense velocity with 37 Issue updates and 50 active PRs. Three clear themes dominate the conversation: **hardening autonomous agent safety** (destructive git guards, secret disclosure mandates), **polishing the Terminal UX** (default status line, virtualized history, Unicode consistency), and **platformizing the `qwen serve` daemon** (voice dictation, workspace APIs, cron scheduling discussions).

---

### 2. Releases
Four releases landed in the past 24 hours, with two stable tags and two preview/nightly builds:

- **[v0.19.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.1)** (Stable) — `feat(cli): match MCP resource completions by name and discover servers` by @wenshao
- **[v0.19.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.0)** (Stable) — `ci(release): Auto-publish VSCode companion after stable releases` by @yiliang114
- **[v0.19.1-nightly.20260624](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.1-nightly.20260624.a234860a4)** — Backports `feat(serve): Add remote LSP status route` by @doudouOUC
- **[v0.18.5-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.5-preview.0)** — Also includes the remote LSP status route

---

### 3. Hot Issues (10 noteworthy)

1. **[#5758 — Protocol / AuthType Decoupling](https://github.com/QwenLM/qwen-code/issues/5758)** [OPEN] [P2]
   *Community discussion on config compatibility. `modelId` + `baseUrl` works in CLI only, while ACP/VSCode pass `providerId + modelId`. Needs a protocol mapping to decouple identity from SDK routing. 5 comments, strongly engaged.*

2. **[#5736 — More Full Prompt Reprocessing](https://github.com/QwenLM/qwen-code/issues/5736)** [OPEN]
   *A consistent pain point for local LLM users. After recent updates, continuing a conversation triggers full re-prefill on llama.cpp instead of incremental cache reuse. 4 comments, user attached server console logs.*

3. **[#5761 — Model Selector Shows Two Checked Items](https://github.com/QwenLM/qwen-code/issues/5761)** [CLOSED] [P2]
   *Desktop UI regression: selecting `[ModelStudio Coding Plan] qwen3.7-plus` also highlights `[ModelStudio Standard] qwen3.7-plus`. Status bar shows the wrong plan. 3 comments, confirmed as duplicate.*

4. **[#5790 — Smart Conditional `node_modules` Symlink](https://github.com/QwenLM/qwen-code/issues/5790)** [OPEN] [P3]
   *Features request for worktree support. Current `symlinkDirectories` is all-or-nothing; the proposal makes it conditional on dependency changes to save disk space without risking stale modules. 2 comments.*

5. **[#5789 — Enable Status Line Preset by Default](https://github.com/QwenLM/qwen-code/issues/5789)** [OPEN] [P3]
   *New users never see the built-in status line until they discover `/statusline`. Proposal to enable it by default showing model, git branch, context usage. Low cost, high onboarding value. 2 comments.*

6. **[#5782 — WebFetch Should Reject URLs Containing Userinfo](https://github.com/QwenLM/qwen-code/issues/5782)** [OPEN] [P3]
   *Security hardening: `WebFetch` currently accepts embedded credentials before the host, potentially exposing secrets in UI/diagnostics. The community wants `user:pass@host` URLs rejected. 2 comments.*

7. **[#5749 — Deterministic Guards Against Destructive Git Commands](https://github.com/QwenLM/qwen-code/issues/5749)** [CLOSED] [P2]
   *Request to block `git reset --hard`, `git clean -fd`, etc., in auto mode even when the user didn't explicitly discard work. Shows demand for safety rails in autonomous workflows. 2 comments.*

8. **[#5734 — Fork Subagent Hardening](https://github.com/QwenLM/qwen-code/issues/5734)** [CLOSED] [P2]
   *Two gaps: forks have no turn cap (unbounded token burn) and permission-gated tool calls are silently auto-denied without inline UI feedback. Community flagged this as a runaway cost risk. 2 comments.*

9. **[#5760 — Use KV Cache Save/Restore Instead of Text Compression](https://github.com/QwenLM/qwen-code/issues/5760)** [OPEN] [P2]
   *High-performance request to use llama.cpp slot state save/restore to avoid re-prefill during context compression. Would eliminate cache misses from summary-generated token sequences. 2 comments.*

10. **[#5763 — Multi-Session `/context-usage` Returns Global Token Count](https://github.com/QwenLM/qwen-code/issues/5763)** [CLOSED] [P2]
    *Process-global singleton leak in the daemon: all sessions report the same token count from the most recently active session. Critical bug for anyone running multiple serve sessions. 1 comment, flagged as `daemon`.*

---

### 4. Key PR Progress (10 important)

1. **[#5788 — Replace Emoji with Unicode Text Symbols in TUI](https://github.com/QwenLM/qwen-code/pull/5788)** [CLOSED]
   *Addresses the long-standing inconsistency where some UI states used emoji, others used text glyphs. Moves entirely to fixed-width Unicode (`✦`, `●`, `✓`, `◐`), cleaning up cross-terminal rendering.*

2. **[#5792 — Enable Built-in Status Line Preset by Default](https://github.com/QwenLM/qwen-code/pull/5792)** [OPEN]
   *Implements the requested default status line. New users see model name, git status, and context usage immediately. Simple config toggle for existing users.*

3. **[#5738 — Default to Virtualized Terminal History](https://github.com/QwenLM/qwen-code/pull/5738)** [OPEN]
   *Turns on in-app scrollable history by default. Users who prefer host scrollback can opt out via `ui.useTerminalBuffer`. A major UX default change.*

4. **[#5785 — Optimize Serve Daemon Startup](https://github.com/QwenLM/qwen-code/pull/5785)** [OPEN]
   *Makes `qwen serve` reach the HTTP listener earlier by deferring React/Ink, web-shell, and ACP setup until after the listener is ready. Adds startup observability.*

5. **[#5755 — Voice Dictation Over the Daemon for Web Shell](https://github.com/QwenLM/qwen-code/pull/5755)** [OPEN]
   *Browser captures microphone, streams PCM to a new `/voice/stream` WebSocket, daemon transcribes server-side. Expands the daemon as a platform layer.*

6. **[#5783 — Reject Userinfo URLs in WebFetch Validation](https://github.com/QwenLM/qwen-code/pull/5783)** [OPEN]
   *Implements the security fix requested in #5782. Rejects `http(s)://user:pass@` before the tool invocation proceeds.*

7. **[#5794 — Refine ASR Transcripts with Fast Model](https://github.com/QwenLM/qwen-code/pull/5794)** [OPEN]
   *After voice dictation, raw transcripts are cleaned up by a fast LLM to remove filler words and fix disfluencies before inserting into the prompt.*

8. **[#5654 — Restore Custom Model IDs When Re-entering Auth Wizard](https://github.com/QwenLM/qwen-code/pull/5654)** [CLOSED]
   *Fixes #5636. The `/auth` Model IDs step now loads previously saved custom IDs instead of resetting to defaults. Small fix, high user impact.*

9. **[#5793 — Map Provider ID to SDK Protocol (`providerProtocol`)](https://github.com/QwenLM/qwen-code/pull/5793)** [OPEN]
   *Implements Approach A from the #5758 discussion. Adds a new optional `providerProtocol` dictionary to decouple provider identity from SDK routing backward-compatibly.*

10. **[#5550 — Secret Disclosure Mandate for Broad File Tasks](https://github.com/QwenLM/qwen-code/pull/5550)** [OPEN]
    *Prevents sweeping file tasks (copy, sync, mirror) from exposing secrets (`.env`, private keys) into public destinations. A Keeper of the Rules pattern applied to autonomous agent behavior.*

---

### 5. Feature Request Trends

**Daemon as a Persistent Runtime Platform**
The community is pushing `qwen serve` beyond a simple HTTP server toward a full-fledged background daemon. Requests include system service registration (`#5768`), revived browser extensions via daemon+WebUI (`#5626`), and rich daemon-hosted features like voice APIs (`#5755`, `#5765`). This signals a strategic appetite for a persistent, long-running host process that separates the agent runtime from the interactive terminal.

**Safety-First Autonomous Mode**
A strong theme is preventing catastrophic agent actions. PRs like the **Secret Disclosure Mandate** (`#5550`) and **Destructive Git Guards** (`#5749`) coexist with requests for subagent resource limits (`#5734`). Developers are treating autonomous mode as a production system that needs deterministic safety rails, not just permission prompts.

**Universal Terminal Polish (TUI Professionalism)**
Pervasive interest in making the CLI feel like a high-quality terminal application: default status lines (`#5789`), virtualized history (`#5738`), consistent Unicode glyphs over emoji (`#5788`), proper box-drawing across terminals (`#5771`, `#5562`). The `/model --vision` flag (`#5597`) fits here — users want model management to feel equally polished.

**Enterprise Configuration & Model Management**
Complex deployment scenarios are driving requests for decoupled provider/SDK routing (`#5758`), `/config key=value` for quick settings (`#5748`), and KV cache optimization for local models (`#5760`). The project is being stretched to support multi-provider, multi-session enterprise workflows.

---

### 6. Developer Pain Points

- **Configuration Setup Friction**: Auth wizards that lose custom model IDs (`#5636`), persistent JetBrains 401 errors (`#3757`), and environment variables being silently ignored (`#3877`) create high early-exit frustration. New users hit walls before they ever run a successful prompt.

- **Local LLM Performance Unpredictability**: Full prompt reprocessing on conversation continuation (`#5736`) and lack of KV cache slot save/restore (`#5760`) make local models feel sluggish, undermining the key value prop for privacy-conscious developers.

- **TUI Cross-Terminal Fragility**: Background colors don't render consistently (`#5562`, `#5771`), cursors become invisible in Alacritty (`#5713`). The visual polish degrades dramatically depending on terminal emulator and theme choice, breaking the professional impression.

- **Background Process Opacity**: The `fork` subagent silently burns tokens with no turn cap (`#5734`), and daemon multi-session state leaks mean `/context-usage` reports garbage data (`#5763`). Developers running background automations feel a lack of visibility and control over resource consumption.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

## DeepSeek TUI Community Digest — June 24, 2026
*Generated from Hmbown/CodeWhale*

---

### 1. Today’s Highlights
Today’s activity converged on two fronts: the **Fleet execution subsystem** moved from design to deliverable with a wave of PRs adding agent profile loading, a loadout setup view, worker runtime exposure, and gated route resolution. Concurrently, a **critical MCP lifecycle bug** (#3461) causing duplicate server processes was rapidly diagnosed and patched. Maintainers also formalized a **harvest merge policy** (#3533, #3517) to ensure contributor attribution survives rebase and merge.

---

### 2. Releases
No new releases were published in the last 24 hours. The project remains in high-velocity feature development targeting the v0.8.65 milestone, primarily focused on the Fleet architecture, provider routing overhaul, and workspace agent profiles.

---

### 3. Hot Issues

1. **#2487 – Turn stalled – no completion signal received**  
   The most active issue by comment volume (17). YOLO mode repeatedly freezes permanently, forcing full restarts. Deep frustration with autonomous execution reliability.
   [Hmbown/CodeWhale#2487](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **#3275 – Self-questioning and self-answering loops**  
   A behavioral regression from #3061. The agent extends scope without user confirmation, undermining trust in delegation.
   [Hmbown/CodeWhale#3275](https://github.com/Hmbown/CodeWhale/issues/3275)

3. **#3144 – Natural-language auto-review policy & pre-push gate**  
   A Cursor-inspired request for a programmable review middle-ground between “always ask” and “unchecked run”.
   [Hmbown/CodeWhale#3144](https://github.com/Hmbown/CodeWhale/issues/3144)

4. **#3461 – MCP duplicate server instance lifecycle**  
   Spawns two MCP processes per config entry, wasting RAM and breaking pipes. Immediately actionable and sparked the day’s PRs.
   [Hmbown/CodeWhale#3461](https://github.com/Hmbown/CodeWhale/issues/3461)

5. **#2766 – UI refactor needed**  
   Long-running UX pain: output hard to copy, confirmation pop-ups hide the interface, info density poor.
   [Hmbown/CodeWhale#2766](https://github.com/Hmbown/CodeWhale/issues/2766)

6. **#1812 – TUI freeze on Windows (crossterm poll)**  
   Persistent cross-platform bug. Windows 11 TUI becomes completely unresponsive while the process stays alive.
   [Hmbown/CodeWhale#1812](https://github.com/Hmbown/CodeWhale/issues/1812)

7. **#3222 – Inline `<think>...</think>` reasoning blocks**  
   Compatibility patch for OpenAI-compatible gateways. Essential for multi-provider rendering fidelity.
   [Hmbown/CodeWhale#3222](https://github.com/Hmbown/CodeWhale/issues/3222)

8. **#3474 – Low text contrast in model/session pickers on macOS**  
   Clear UI bug (now closed) that underscored testing gaps on non-Linux terminals.
   [Hmbown/CodeWhale#3474](https://github.com/Hmbown/CodeWhale/issues/3474)

9. **#3384 – Atomic provider/model switching via *ReadyRouteCandidate***  
   Architectural work to ensure state mutation only occurs after a complete route candidate is resolved.
   [Hmbown/CodeWhale#3384](https://github.com/Hmbown/CodeWhale/issues/3384)

10. **#2492 – Lack of cross-session memory**  
    Each restart loses context; memory must be explicitly re-read. A critical gap for persistent agent workflows.
    [Hmbown/CodeWhale#2492](https://github.com/Hmbown/CodeWhale/issues/2492)

---

### 4. Key PR Progress

1. **#3521 – Gate runtime switches on RouteResolver**  
   Architectural enforcement: provider/model changes flow through route resolution before state mutation.
   [Hmbown/CodeWhale#3521](https://github.com/Hmbown/CodeWhale/pull/3521)

2. **#3524 / #3529 – Make MCP connection drops explicit**  
   Centralizes MCP lifecycle with logging, directly addressing the duplicate MCP process bug.
   [Hmbown/CodeWhale#3524](https://github.com/Hmbown/CodeWhale/pull/3524)

3. **#3532 – Reuse shared McpPool across HTTP API calls**  
   Eliminates redundant pool creation in the HTTP API path, eliminating the root cause of resource duplication.
   [Hmbown/CodeWhale#3532](https://github.com/Hmbown/CodeWhale/pull/3532)

4. **#3513 – Load workspace agent profiles**  
   Fleet kernel: discovers and normalizes `.codewhale/agents/*.toml` into `FleetProfile` vocabulary.
   [Hmbown/CodeWhale#3513](https://github.com/Hmbown/CodeWhale/pull/3513)

5. **#3516 – Fleet setup loadout view (TUI)**  
   Lets users configure roles, profiles, loadouts, and recursion policies in a visual left-to-right planner.
   [Hmbown/CodeWhale#3516](https://github.com/Hmbown/CodeWhale/pull/3516)

6. **#3523 – Feed route limits into context budgets**  
   Connects resolved `RouteLimits` to dynamic context windows, compaction thresholds, and pressure readouts.
   [Hmbown/CodeWhale#3523](https://github.com/Hmbown/CodeWhale/pull/3523)

7. **#3519 – Mouse-wheel scrolling + provider type-ahead**  
   Two high-demand picker UX features landed across model, session, provider, and theme pickers.
   [Hmbown/CodeWhale#3519](https://github.com/Hmbown/CodeWhale/pull/3519)

8. **#3500 – Harden picker selection contrast**  
   Fixes the contrast regression reported in #3474, improving accessibility across `/model` and `/sessions`.
   [Hmbown/CodeWhale#3500](https://github.com/Hmbown/CodeWhale/pull/3500)

9. **#3530 – Localize /mode picker and composer Vim indicator**  
   Harvested contributor PR (#2239) bringing i18n wiring to the mode system.
   [Hmbown/CodeWhale#3530](https://github.com/Hmbown/CodeWhale/pull/3530)

10. **#3533 – Require rebase/merge-commit (not squash) for harvested PRs**  
    Standardizes attribution policy so `Co-authored-by` lines survive the merge process.
    [Hmbown/CodeWhale#3533](https://github.com/Hmbown/CodeWhale/pull/3533)

---

### 5. Feature Request Trends

- **Multi-Provider Fleet Architecture**  
  The dominant signal: decoupling from a single model. Specific requests include provider-owned live model catalogs (#3385), capability-aware fallback chains (#2574), cross-provider model search (#3075), and direct provider integration (GLM-5.2, #3439).

- **Safe, Observable Autonomous Execution**  
  Strong community interest in controlled agent autonomy: natural-language review policies (#3144), visual inspection artifacts for browser/UI tasks (#3145), and Fleet permission/delegation policies (#3167).

- **Agent Context & Memory**  
  Developers consistently request persistent cross-session memory (#2492) and real-time telemetry for token budget, context pressure, and cost during long-running tasks (#2666).

- **Platform & UX Maturity**  
  i18n (#3530), accessibility (contrast #3474, scrolling #3519), and modal usability (#2766) indicate the user base is pushing for production-grade fit and finish.

---

### 6. Developer Pain Points

- **Execution Loop Fragility**  
  The highest-severity cluster: “Turn stalled” freezes (#2487) and self-questioning loops (#3275) directly erode trust in autonomous modes.

- **Resource Management & Stability**  
  Duplicate MCP processes (#3461) wasting RAM and causing pipeline breakage is a concrete systems-level headache. Windows-specific TUI locks (#1812) remain unresolved.

- **Core UX Friction**  
  Inability to copy output cleanly (#2766), low text contrast (#3474), and poor discoverability of configuration knobs (#3303) consistently surface as daily-use irritants.

- **Configuration Complexity**  
  Lack of a unified TUI for editing runtime config (#3303) and confusion between provider/model selection (#2300) make onboarding and tuning more difficult than necessary.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*