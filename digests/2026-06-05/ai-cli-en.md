# AI CLI Tools Community Digest 2026-06-05

> Generated: 2026-06-05 03:29 UTC | Tools covered: 9

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

## Cross-Tool AI CLI Ecosystem Comparison Report: June 5, 2026

### 1. Ecosystem Overview

The AI CLI tools landscape is undergoing a painful but necessary transition from the "capability race" into the "reliability and trust era." While providers continue shipping rapid feature releases—managed version gating, daemon architectures, native desktop apps, and expanded plugin ecosystems—the dominant signal from every major community this cycle is a crisis of confidence. Data integrity regressions (silent truncation, session data loss), agent loop failures (indefinite hangs, false success reports), and cross-platform instability (macOS daemon loops, Windows sandbox breaks, WSL friction) are eroding fundamental user trust. A clear strategic divergence is emerging: incumbent tools are being tested on enterprise governance and operational stability, while challengers race on provider flexibility, protocol unification, and extensibility to capture users frustrated by walled gardens. The overall ecosystem is maturing, but the engineering complexity of maintaining reliable agentic systems at scale is proving to be the defining challenge of 2026.

---

### 2. Activity Comparison (as of 2026-06-05)

| Tool | Latest Release | Hot Issue Severity | PR Landscape | Dominant Signal |
|---|---|---|---|---|
| **Claude Code** | v2.1.163 (Managed gating, `/plugin list`) | Critical (Auth blocker, data truncation, auto-compact failure) | High (Session persistence fix merged, triage tooling) | Mature ecosystem straining under reliability regressions |
| **OpenAI Codex** | v0.138.0-alpha.1–4 (4 Rust alphas) | Critical (macOS syspolicyd exhaustion, Win sandbox failures, context loss) | High (Remote pairing RPC, sticky environments, Responses Lite) | Fastest release cadence; system-level stability risks |
| **Gemini CLI** | v0.45.1 hotfix / v0.47.0 nightly | High (Generalist agent hangs, subagent false success) | Very High (SSRF fix, EBADF fix, WSL bypass, 34 PRs updated) | Strong engineering velocity; core agent loop P1s open |
| **GitHub Copilot CLI** | v1.0.60-0 (Vim diff nav, billing topic) | Medium (Rate-limit retry loop, auth on resume, Linux copy regression) | Very Low (No actionable community PRs) | Ecosystem-embedded; low development churn |
| **Kimi Code CLI** | None (v0.9.0–v1.46.0 range) | Critical (403 auth blocking all functionality) | Medium (Terminal scroll fix, session resilience patches) | Early-stage; existential auth bug stunting growth |
| **OpenCode** | v1.16.0 (Workspace cloning, Bedrock support, session mobility) | High (Memory leaks, MCP breakage, prompt injection, subagent retry loops) | Very High (Snowflake provider, Native Effect API, compaction fixes) | Extremely high feature velocity; corresponding regression rate |
| **Pi (badlogic)** | v0.78.1 (NVIDIA NIM, MiniMax-M3, extension context) | High (openai-codex hang, provider API fragmentation, phantom prompts) | Very High (Vertex provider, workspace approval system, keybinding unification) | Steady enterprise-oriented feature shipping |
| **Qwen Code** | v0.17.1-nightly | Medium (Prompt cache busting, headless Linux crash, model ID display) | Very High (Daemon merge +115k LOC, ACP/REST parity, fork agent, stats dashboard) | Major architectural leap toward daemon/standardized protocol |
| **DeepSeek TUI / CodeWhale** | Stabilizing for v0.9.0 | Medium (Session freezes, fragile MCP naming, TUI ergonomics) | High (Auth rollback, multi-tab system, performance optimization series) | Community-driven stabilization focused on quality gating |

---

### 3. Shared Feature Directions

| Pattern | Tools Involved | Specific User Needs |
|---|---|---|
| **Automatic, Trustworthy Context Management** | Claude Code, OpenAI Codex, Copilot CLI, OpenCode, Pi, Qwen Code | Seamless compaction that doesn't silently truncate or lose data. Predictable behavior at 1M+ context windows. Universal demand for "set and forget" context handling. |
| **Persistent & Resumable Session State** | Claude Code, OpenAI Codex, Copilot CLI, Kimi Code CLI, OpenCode | Sessions must survive restarts, upgrades, and network interruptions without losing history or authentication. Session resume is breaking auth state across multiple tools. |
| **Granular, Configurable Permission Models** | Claude Code, Copilot CLI, Pi, CodeWhale, Gemini CLI | `allow once` / config-driven approval policies to eliminate permission fatigue. Subagent prompts lack context for evaluating safety (Copilot CLI #3684). |
| **Agent Loop Reliability & Determinism** | Gemini CLI, OpenCode, Pi, Claude Code | Agent loops that hang indefinitely, falsely report success on MAX_TURNS, or generate phantom follow-up prompts are the highest-severity trust killers. |
| **Cross-Platform First-Class Support** | All tools | macOS-dominant development creates systemic friction. Linux terminal regressions (Wayland, musl, copy-paste), Windows sandbox failures, and WSL performance gaps are universal. |
| **Provider & Model Flexibility** | OpenCode, Pi, Qwen Code, Kimi Code CLI, Claude Code | Users demand seamless switching between Anthropic, OpenAI, Google, DeepSeek, open-weight models, and cloud providers (Bedrock, Vertex). Auth conflicts between subscriptions and API keys (Claude Code #8327) are a hard blocker. |
| **MCP / Plugin Ecosystem Maturation** | Claude Code, DeepSeek TUI, Qwen Code, Copilot CLI, OpenAI Codex | Fragile naming conventions (`split_once('_')` failures), deferred loading busting prompt caches, manifest quality, and missing diagnostics are universal pain points. |

---

### 4. Differentiation Analysis

**Anthropic (Claude Code)** positions as the **enterprise-grade market leader**, actively shipping managed version enforcement and plugin infrastructure. However, the same maturity is straining under critical data-integrity regressions (silent file truncation, auto-compact failure) and a **unified auth model conflict** between subscriptions and API keys that remains an onboarding trust blocker after 9 months.

**OpenAI (Codex)** is the most **aggressive feature shipper** (4 Rust alphas in a day) with strong bets on the **Desktop App** and **Computer Use** paradigms. The relentless velocity is producing severe **macOS system-level instability** (`syspolicyd` FDs exhaustion, `trustd` CPU runaway) and **Windows sandbox fragility**, suggesting QA infrastructure hasn't scaled with release cadence.

**Google (Gemini CLI)** shows the deepest investment in **agent orchestration architecture** (generalist + specialized sub-agents) and **safety/evaluation infrastructure** (component-level evals, Auto Memory). The trade-off is that the agent loop complexity produces the most dramatic **loop hygiene** failures—false success on MAX_TURNS and indefinite hangs are the cohort's most visible agent reliability issues.

**GitHub (Copilot CLI)** takes a deliberately **conservative, embedded approach**. It is the most tightly integrated with existing developer workflows (GitHub, VS Code) but has the **narrowest feature surface** and lowest open-source PR activity. The community's pain points (rate-limit retry exhaustion, session resume authentication loss) reflect a robust but friction-prone core.

**MoonshotAI (Kimi Code CLI)** is an **emerging player** whose growth is severely blocked by a **403 authorization gatekeeping bug** that halts all functionality. The small team shows responsive PR turnaround for terminal UI fixes, but session resilience, feature parity (VS Code), and version fragmentation reveal a tool still maturing its foundations.

**OpenCode** is the **most feature-dense challenger**, aggressively adding providers (Snowflake, Bedrock), a native Effect API, and complex session management. The velocity is extraordinary—but so is the **regression frequency**. MCP service detection breaks between point releases, and the subagent infinite retry loop (`$15+/invocation`) represents real operational risk for power users.

**Pi (badlogic)** functions as the **Swiss Army knife of providers**, prioritizing enterprise cloud connectivity (Vertex AI, AWS Bedrock Mantle, NVIDIA NIM) and extensibility (workspace approval systems, universal keybinding conventions). The trade-off is visible **provider API fragmentation**—`max_tokens` vs `max_completion_tokens` mapping, `developer`/`system` role aliases, and proxied connection regressions create constant minor incompatibilities.

**Qwen Code (QwenLM)** is taking the most **architecturally distinct path**: a daemon-native ACP server model enabling headless operation and third-party editor integration without adapter shims. The massive `+115k LOC` daemon merge signals a strategic bet on **protocol unification** and CI/CD-agnostic workflows. Suffers from similar prompt caching and UI issues, but the architecture is genuinely differentiated.

**DeepSeek TUI / CodeWhale** stands out for its **community-driven development model** ("harvest" merges from contributors) and rigorous **performance optimization** focus (memoized token estimation, cached serialization). The explicit `v0.9.0 stabilization gate` demonstrates mature engineering governance. Cross-tab collaboration and multi-session workspace features indicate strong grassroots innovation in TUI UX.

---

### 5. Community Momentum & Maturity

**High Volume, High Expectations (Established but Strained):**

- **Claude Code** commands the largest professional user base. The community is mature and vocal, but the volume of *critical* reliability regressions—silent truncation, session data loss, auto-compact broken—suggests maintenance burden scaling faster than quality assurance capacity. Enterprise users are deeply engaged but increasingly frustrated.
- **OpenAI Codex** has exceptionally high community engagement driven by rapid product updates and strong brand pull. The system-level macOS issues and Windows sandbox regressions are creating a vocal, powerful user cohort starting to push back against release velocity.

**Rapidly Iterating with Architectural Ambition (High Churn, High Growth):**

- **Qwen Code** is executing the largest architectural migration in the cohort. The daemon/ACP model, combined with active community contribution on performance, positions it well for Linux-first, infrastructure-minded developers. Growth likely to accelerate as the protocol unification bet pays off.
- **OpenCode** ships features faster than any other open-core tool. The "Memory Megathread" (#20695, 90 comments) demonstrates active community co-debugging. The primary risk is that regression velocity fractures the user base across incompatible versions.
- **Pi** demonstrates mature, steady feature shipping with deep understanding of enterprise deployment realities (cloud providers, path separators, approval workflows). Less flashy than competitors, but the issue tracker shows strong prioritization of real-world blocking issues.

**Stabilizing or in Catch-Up Mode:**

- **DeepSeek TUI / CodeWhale** shows strong community health with multiple merged community PRs (`HUQIANTAO`, `Implementist`, `Lively7385`). The explicit stabilization gate signals responsible engineering governance. Momentum depends on successful delivery of v0.9.0 without introducing new regressions.
- **Kimi Code CLI** has the weakest community signal. The 403 auth bug is an existential growth blocker. The team is responsive (auto-scroll fix within 24 hours), but version fragmentation and feature gaps vs. VS Code extension weaken retention.

**Steady State / Platform Embedded:**

- **GitHub Copilot CLI** has low open-source activity, but its user base is massive by platform default (GitHub customers). Issues like rate-limit retry loops and auth-on-resume failures are highly impactful but do not threaten the tool's existence. The team appears to be developing largely internally.

---

### 6. Trend Signals for Technical Decision-Makers

1. **Trust is the New Differentiator.** Across every tool, the highest-severity issues involve data loss, silent corruption, false agent success reports, or unjustified failures. **Evaluate a tool on its "Reliability" and "Data Integrity" issue track record, not its feature list.** A tool that silently truncates files or loses a 2-hour session history carries a higher total cost than one missing a minor feature.

2. **The Agent Loop is the Single Hardest Engineering Problem.** Hangs, infinite retries, false success on turn limits, and phantom follow-up prompts are the cohort's most erosive bugs. Teams should demand evidence of robust backpressure, deterministic state machines, and visible agent telemetry (token budgets, execution context). Tools that ship "agents" without loop hygiene are shipping incomplete products.

3. **Cross-Platform Parity is a Hard Requirement, Not a "Nice to Have."** The volume of Linux/WSL/macOS-specific regressions is staggering. If your team operates predominantly on Linux or Windows, deeply audit the tool's platform-specific issue tracker. "Mac-first" development is creating systemic friction for the majority of professional developers.

4. **Enterprise Security Models are Immature and Often Counterproductive.** Managed version gating, safety classifiers, and auth models are creating as many problems as they solve. A safety classifier that flags `/compact` as an attack (Claude Code #63499) or permission prompts that hide executed commands (Copilot CLI #3684) are broken by design. Evaluate enterprise controls for practical usability, not just feature checkboxes.

5. **Provider Flexibility is Becoming Table Stakes.** The rise of OpenCode, Pi, and Qwen Code is directly fueled by users' desire to benchmark and switch between Anthropic, OpenAI, Google, DeepSeek, Ollama, and cloud providers. Claude Code's 9-month-old auth conflict (#8327) perfectly illustrates the future failure point of rigid provider models. **Choose a tool that treats provider configuration as a first-class, swappable component.**

6. **MCP/Plugin Standardization is at a Critical Inflection Point.** Every tool is building a plugin ecosystem, and early adopters are hitting identical problems: deferred loading busting prompt caches, fragile naming conventions, permission fatigue, and manifest quality gaps. The industry urgently needs a robust, standardized SDK or protocol. The next 6 months will be decisive for ecosystem consolidation—monitor which approaches (ACP, MCP, custom) gain critical mass.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the `anthropics/skills` repository activity as of **2026-06-05**.

---

## 1. Top Skills Ranking (Most Discussed Pull Requests)

The following PRs represent the most commented-on Skill submissions, reflecting intense community scrutiny and interest.

**1. Agent Creator Meta-Skill ([#1140](https://github.com/anthropics/skills/pull/1140))**
- **Functionality:** Introduces an `agent-creator` meta-skill for constructing task-specific agent sets. Also fixes critical evaluation pipeline bugs and adds Windows support.
- **Discussion Highlights:** The community focused heavily on the parallel tool-calling fix in `evaluation.py` and the practical implications of composable agent arsenals.
- **Status:** Open (Updated Jun 2, 2026)

**2. Skill Quality & Security Analyzers ([#83](https://github.com/anthropics/skills/pull/83))**
- **Functionality:** Adds meta-skills to evaluate Skills across five dimensions: Structure, Documentation, Security, Reliability, and Extensibility.
- **Discussion Highlights:** Strong consensus on the need for community-wide quality gatekeeping. The security analyzer dimension generated the most debate regarding trust boundaries.
- **Status:** Open

**3. Document Typography ([#514](https://github.com/anthropics/skills/pull/514))**
- **Functionality:** Prevents common typographic issues in AI-generated documents (orphans, widows, numbering misalignment).
- **Discussion Highlights:** Broad agreement that these formatting flaws affect every document Claude generates. Users appreciate a skill targeting this "invisible" quality dimension.
- **Status:** Open

**4. Testing Patterns ([#723](https://github.com/anthropics/skills/pull/723))**
- **Functionality:** Comprehensive skill covering the Testing Trophy model, unit testing patterns, and React Testing Library best practices.
- **Discussion Highlights:** Debate centered on prescriptive vs. configurable testing setups. High demand for "what NOT to test" guidance.
- **Status:** Open

**5. SAP Predictive Analytics ([#181](https://github.com/anthropics/skills/pull/181))**
- **Functionality:** Leverages SAP's open-source RPT-1-OSS tabular foundation model for predictive analytics on business data.
- **Discussion Highlights:** Enterprise users engaged heavily on data security and API integration patterns. Signals growing enterprise appetite for vertical-specific skills.
- **Status:** Open

**6. ServiceNow Platform ([#568](https://github.com/anthropics/skills/pull/568))**
- **Functionality:** Broad platform assistant covering ITSM, ITOM, SecOps, ITAM, and CSDM.
- **Discussion Highlights:** High praise for the breadth, but concerns raised about context window saturation given the copious domain surface area.
- **Status:** Open

**7. Shodh-Memory ([#154](https://github.com/anthropics/skills/pull/154))**
- **Functionality:** Persistent memory system that maintains context across conversations via structured memory records.
- **Discussion Highlights:** Central discussion point: the trade-off between memory utility and token costs, and how to avoid "memory bloat."
- **Status:** Open

**8. OpenDocument Format (ODT) ([#486](https://github.com/anthropics/skills/pull/486))**
- **Functionality:** Full read/write/convert support for OpenDocument (.odt, .ods), template filling, and HTML parsing.
- **Discussion Highlights:** Strong demand from LibreOffice and open-source document workflow users. Template filling was the most requested sub-feature.
- **Status:** Open

---

## 2. Community Demand Trends (From Issues)

Analysis of the top 15 most-commented Issues reveals the community's most anticipated improvements:

- **Enterprise Governance & Sharing:** The top-voted issue ([#228](https://github.com/anthropics/skills/issues/228)) demands org-wide skill libraries. Issues [#492](https://github.com/anthropics/skills/issues/492) (namespace trust) and [#412](https://github.com/anthropics/skills/issues/412) (agent governance) reflect a strong push toward formal security and policy models.
- **Platform Portability & Reliability:** Recurring demands for cross-platform compatibility: Bedrock support ([#29](https://github.com/anthropics/skills/issues/29)), MCP interoperability ([#16](https://github.com/anthropics/skills/issues/16), [#1102](https://github.com/anthropics/skills/issues/1102)), and data persistence stability ([#62](https://github.com/anthropics/skills/issues/62)).
- **Developer Tooling & Evaluation Quality:** Issue [#556](https://github.com/anthropics/skills/issues/556) (eval pipeline failures) and [#202](https://github.com/anthropics/skills/issues/202) (skill-creator quality) highlight a critical bottleneck: the community is demanding better tools for building tools.
- **Skill Architecture:** Advanced users are pushing for multi-file bundling ([#1220](https://github.com/anthropics/skills/issues/1220)) and standardized portability labels ([#1156](https://github.com/anthropics/skills/issues/1156)) to manage context windows and distribution.

---

## 3. High-Potential Pending Skills

These active PRs show strong recent momentum and are likely to land soon:

- **Agent Creator Meta-Skill ([#1140](https://github.com/anthropics/skills/pull/1140))** — Updated June 2. The most recent substantial feature addition. Directly addresses the "multi-agent workflow" gap.
- **Feature-Dev Workflow Fix ([#363](https://github.com/anthropics/skills/pull/363))** — Updated June 3. Solves a critical `TodoWrite` overwrite bug that silently skips quality review phases. High operational impact.
- **Windows Compatibility Drive ([#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050))** — Ongoing effort to fix `run_eval.py` crashes and subprocess encoding. Unblocking the Windows user base is a key priority.
- **n8n Builder & Debugger Suite ([#190](https://github.com/anthropics/skills/pull/190))** — Updated May 18. Four production-tested skills (n8n, faf-expert). Strong candidate for merging as it addresses automation and persistent context.
- **Testing Patterns ([#723](https://github.com/anthropics/skills/pull/723))** — Sustained interest in a complete testing stack skill makes this a high-probability merge candidate.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is a fundamental shift from building narrow utility skills to establishing a **governed, portable, and persistent enterprise agent platform**, with the biggest friction point being the immaturity of the meta-tooling (evaluation, security, and packaging infrastructure) needed to sustain that vision.**

---

**Claude Code Community Digest — 2026-06-05**

---

### 1. Today's Highlights
Anthropic shipped **Claude Code v2.1.163** with managed version enforcement and a new `/plugin list` command, signaling tightening enterprise controls and maturing plugin infrastructure. However, the community's attention remains fixed on critical reliability regressions: silent file truncation in Cowork tools and auto-compact failures. A long-running **authentication subscription conflict** (Issue #8327, 116 comments) continues to dominate discussion. On the maintenance side, a critical fix for session persistence data loss was merged, and contributors are actively shipping better triage tooling.

---

### 2. Releases
**v2.1.163** was published today.
- **Managed Version Gating:** New `requiredMinimumVersion` and `requiredMaximumVersion` managed settings allow admins to enforce specific tool versions. Claude Code will refuse to launch outside the configured range and direct users to an approved version.
- **Plugin Command:** A new `/plugin list` command exposes enabled/disabled plugin states via `--enabled` / `--disabled` flags.

[View Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.163)

---

### 3. Hot Issues (10 selected by community engagement & severity)

1. **#8327 — [Bug] 'Organization has been disabled' when ANTHROPIC_API_KEY overrides Max/Pro subscription** *(116 comments)*
   The most active issue. Users with valid subscriptions hit this error when an API key is also present. Remains a major onboarding and trust blocker, active since Sep 2025.
   [Issue Link](https://github.com/anthropics/claude-code/issues/8327)

2. **#63060 — [Bug] API Error: Usage credits required for 1M context** *(66 comments)*
   High friction around the 1M context window. Users must manually run `/usage-credits` or switch models. Strong demand for automatic handling.
   [Issue Link](https://github.com/anthropics/claude-code/issues/63060)

3. **#61869 — [Bug] Usage credits required for 1M context window (CLOSED as duplicate)** *(57 comments)*
   Closed as duplicate of #63060, confirming the scale of user impact for this context credit friction.
   [Issue Link](https://github.com/anthropics/claude-code/issues/61869)

4. **#53940 — [Bug] Cowork Edit/Write tools silently truncate files via byte-conservation buffer cap** *(23 comments)*
   A severe data integrity bug. Files are deterministically truncated at all sizes with no warning. Debugging sessions are exposing silent corruption.
   [Issue Link](https://github.com/anthropics/claude-code/issues/53940)

5. **#63015 — [Bug] Auto-compact never triggers despite statusline reporting '100% context used'** *(20 comments)*
   Regression on v2.1.153. The compaction mechanism entirely fails to fire, forcing manual context management. Max subscription, 200K mode.
   [Issue Link](https://github.com/anthropics/claude-code/issues/63015)

6. **#63499 — [Bug] `/compact` fails with cyber safeguards false positive during defensive security session** *(4 comments)*
   The context compaction command itself is re-classified as a security violation. Suggests an overly aggressive safety classifier intercepting legitimate operations.
   [Issue Link](https://github.com/anthropics/claude-code/issues/63499)

7. **#25434 — [Docs] Session docs missing nested-Claude launch guard behavior** *(9 comments)*
   No documented behavior for launching Claude Code inside another session. Increasingly relevant as users adopt parallel worktree sessions.
   [Issue Link](https://github.com/anthropics/claude-code/issues/25434)

8. **#18061 — [Docs] Contradiction regarding WSL support for Chrome integration** *(8 comments)*
   Documentation and changelog disagree on whether WSL is supported for the browser integration. Platform friction for Linux-on-Windows developers.
   [Issue Link](https://github.com/anthropics/claude-code/issues/18061)

9. **#19426 — [Docs] Undocumented 'Clear Context' transition options in Plan Mode** *(8 comments)*
   Plan Mode contains UI behavior for clearing context that is entirely undocumented, limiting user workflow awareness.
   [Issue Link](https://github.com/anthropics/claude-code/issues/19426)

10. **#25456 — [Docs] @-mention anchor fragment syntax (@file.md#section) is undocumented** *(6 comments)*
    Power users frequently request this fine-grained context injection feature be officially documented.
    [Issue Link](https://github.com/anthropics/claude-code/issues/25456)

---

### 4. Key PR Progress (5 PRs updated in last 24h)

1. **#44742 [CLOSED] — Fix: diagnostic tool + root cause analysis for session persistence data loss**
   *Critical bug fix.* Addresses a silent data loss issue affecting 12+ duplicate reports since Dec 2025 where VS Code extension conversations vanish on restart. Adds `scripts/diagnose-session-persistence.ts` for users to validate setup. **Merged.**
   [PR Link](https://github.com/anthropics/claude-code/pull/44742)

2. **#65344 [OPEN] — Fix(scripts): correct premature return in `markStale` and add `--debug` flag**
   Fixes a logic bug in paginated issue processing for `scripts/sweep.ts`. Improves automated stale-issue handling for maintainers.
   [PR Link](https://github.com/anthropics/claude-code/pull/65344)

3. **#65286 [OPEN] — Fix(plugins): add missing `plugin.json` manifest for `plugin-dev`**
   Adds the required `.claude-plugin/plugin.json` manifest to the developer plugin, fixing installation and discovery through normal plugin channels. Important for ecosystem contributors.
   [PR Link](https://github.com/anthropics/claude-code/pull/65286)

4. **#65314 [OPEN] — Scripts: add `detect-theme-color-issues` triage tool**
   Community-driven triage script that auto-labels and groups issues related to invisible text on light terminal themes (`color7`/`color0` collision family). Reduces manual triage burden.
   [PR Link](https://github.com/anthropics/claude-code/pull/65314)

5. **#58673 [OPEN] — s**
   Placeholder/test PR. Minimal substantive activity on heavy code changes today, likely reflecting focus on the release and critical bug triage.
   [PR Link](https://github.com/anthropics/claude-code/pull/58673)

---

### 5. Feature Request Trends

- **Reliable Context Compaction:** The dominant request is for automatic, seamless context management. Users want the 1M context window to be *transparently handled*, not gated behind manual commands or credits.
- **Plugin Ecosystem Depth:** With `/plugin list` now live, the community expects better scoping, validation, and discovery. Demand is growing for plugin-provided MCP server deduplication and stable documentation.
- **Unified Auth Model:** The sustained heat on Issue #8327 signals an urgent request to merge API key and subscription authentication paths without conflicts.
- **Session & State Transparency:** Multiple docs issues ask for a centralized reference of all files, settings, and state directories. Users want a clear map of how Claude Code manages local state (sessions, configs, managed overrides).
- **MCP & Agent UX Indicators:** Users want explicit UI feedback for MCP "Queried {server}" calls and safe interruption/result retrieval from background sub-agents.

---

### 6. Developer Pain Points

- **Data Integrity & Trust:** Silent truncation (#53940) and session data loss (#44742) erode fundamental trust. These are the highest-severity items for professional developers relying on the tool for production work.
- **Context Window Friction:** Hitting the 1M credit gate or a broken auto-compactor mid-session creates sudden workflow breakdowns. Developers are forced into manual recovery.
- **Documentation Gaps:** The extensive documentation debt (predominantly filed by a single power user, `coygeek`) highlights a gap between feature releases and usable developer guides. This increases the support burden directly.
- **Configuration Sprawl:** Confusion between managed settings, environment variables (`ANTHROPIC_API_KEY` vs subscription), local settings (`settings.local.json`), and plugin scopes is a consistent source of hard-to-debug errors.
- **Platform Support Friction:** WSL contradictions, Linux glibc minimums, and terminal theme collisions show that the macOS experience is significantly smoother than Linux/Windows, creating barriers for a diverse developer tool audience.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – June 5, 2026

## 1. Today’s Highlights
Today saw a burst of infrastructure work with four rapid-fire Rust alpha releases (`v0.138.0-alpha.1` through `v0.138.0-alpha.4`), signaling active engineering churn on the CLI/app-server runtime. On the community side, the top discussion threads centered on severe macOS stability issues involving `syspolicyd` resource exhaustion, while the request for a native Linux desktop client continued to gather overwhelming momentum (477 👍).

## 2. Releases
A series of alpha releases for the Codex Rust runtime were published within the last 24 hours:

- **[`rust-v0.138.0-alpha.1`](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.1)** through **[`rust-v0.138.0-alpha.4`](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.4)**

While specific changelogs are not surfaced in this snapshot, the rapid iteration cycle (four alpha tags in a single day) suggests active development addressing upstream fixes or deploying incremental features in the core runtime. Developers on the cutting edge should update and watch for behavioral changes in sandboxing and context management.

## 3. Hot Issues
*(10 noteworthy items from the last 24h)*

- **[Issue #11023](https://github.com/openai/codex/issues/11023) – Codex desktop app for Linux**  
  *Enhancement, App* | 97 comments | 477 👍  
  The single most-liked open feature request. Users report the Mac app is power-prohibitive for long-running local workloads and are pushing hard for a native Linux build.

- **[Issue #20741](https://github.com/openai/codex/issues/20741) – Project chat histories disappeared after update**  
  *Bug, App, Session* | 26 comments  
  A severe data-loss incident on macOS Tahoe. Multiple users confirm project histories vanishing after upgrading, eroding trust in persistent state.

- **[Issue #25882](https://github.com/openai/codex/issues/25882) – macOS app relaunches in tight loop, exhausting syspolicyd FDs**  
  *Bug, App, Performance* | 12 comments  
  A critical system-level failure. Codex respawns its own binary in a loop until `syspolicyd` exhausts file descriptors, freezing all app launches system-wide.

- **[Issue #25719](https://github.com/openai/codex/issues/25719) – syspolicyd/trustd CPU and memory runaway**  
  *Bug, App, Computer Use, Performance* | 15 comments  
  A closely related macOS issue where Codex triggers persistent high CPU usage in system security daemons, significantly degrading machine performance.

- **[Issue #24391](https://github.com/openai/codex/issues/24391) – Windows sandbox spawn setup refresh fails on CLI 0.133.0**  
  *Bug, Windows OS, Sandbox, CLI* | 23 comments  
  A widely-reproduced Windows regression. The sandbox fails to initialize after updating, breaking shell commands and Node REPL for many users.

- **[Issue #25715](https://github.com/openai/codex/issues/25715) – Codex App Unusable Slow with WSL as Agent Environment**  
  *Bug, Windows OS, App, Performance* | 21 comments  
  Developers relying on WSL report severe performance degradation, with routine operations taking excessive time. A top hindrance for Windows-based coding workflows.

- **[Issue #25220](https://github.com/openai/codex/issues/25220) – Bundled plugins unavailable on EFS-encrypted WindowsApps**  
  *Bug, Windows OS, App, Skills, Computer Use, Browser* | 12 comments  
  Enterprise users are blocked by filesystem permission issues. Windows AppX installations with EFS encryption cause plugin copyfile failures.

- **[Issue #22802](https://github.com/openai/codex/issues/22802) – Mobile remote setup fails with “Secure setup failed”**  
  *Bug, App, Remote* | 17 comments  
  Remote pairing between the ChatGPT mobile app and Codex Desktop fails for certain configurations. High engagement signals strong demand for reliable remote access.

- **[Issue #26493](https://github.com/openai/codex/issues/26493) – Context compaction fails with `invalid_enum_value`**  
  *Bug, Windows OS, Context, App, App-Server* | 5 comments (opened today)  
  A very fresh bug affecting context management, possibly linked to the new alpha releases. The `invalid_enum_value` error suggests a serialization mismatch in the compaction stack.

- **[Issue #21073](https://github.com/openai/codex/issues/21073) – Auto-resume CLI session when usage limit resets**  
  *Enhancement, Rate Limits, Enterprise* | 6 comments | 9 👍  
  A smart quality-of-life request. Users want the CLI to automatically resume tasks after hitting usage limits rather than discarding work.

## 4. Key PR Progress
*(10 important pull requests)*

- **[PR #26449](https://github.com/openai/codex/pull/26449) / [PR #26450](https://github.com/openai/codex/pull/26450) – Remote control pairing status transport & RPC**  
  Adds backend transport and app-server RPC support for checking pairing status. Lays groundwork for more reliable mobile-to-desktop connection handling.

- **[PR #26505](https://github.com/openai/codex/pull/26505) – Make turn environments sticky**  
  A significant UX improvement. Environment selections (cwd, tool configs) now persist across turns, removing the need for repetitive per-turn reconfiguration.

- **[PR #26500](https://github.com/openai/codex/pull/26500) – Open Windows app workspaces via deep link**  
  Fixes a gap in the Windows CLI where `codex app PATH` printed manual instructions instead of directly opening the workspace in the Desktop app via `codex://` deep links.

- **[PR #26490](https://github.com/openai/codex/pull/26490) – Use standalone tools for Responses Lite**  
  Architecturally significant: enables a lightweight model execution path by routing web search and image generation through Codex-owned executors instead of hosted backends.

- **[PR #26202](https://github.com/openai/codex/pull/26202) – Restore release symbol artifacts with line tables**  
  Developer tooling win. Restores release symbol archives using `line-tables-only` debuginfo, balancing small archive size with accurate stack traces for debugging Codex itself.

- **[PR #26479](https://github.com/openai/codex/pull/26479) – Speed up local nextest runs**  
  Internally-focused productivity PR that introduces bounded parallelism for local test runs, drastically reducing `just test` times without changing CI behavior.

- **[PR #26181](https://github.com/openai/codex/pull/26181) – fix(tui): Windows composer background**  
  Fixes the TUI composer shading on Windows terminals that support OSC 10/11 default color queries, improving terminal visual consistency.

- **[PR #26259](https://github.com/openai/codex/pull/26259) – Add advisory Interrupt hooks for interrupted turns**  
  Safety and observability improvement. Allows handlers to emit system messages on interruption without blocking the interrupt path.

- **[PR #25829](https://github.com/openai/codex/pull/25829) – Add product defaults for plugin sharing**  
  Enterprise unlock. Moves plugin sharing configuration from an internal feature flag toward customer/admin-controlled settings.

- **[PR #25147](https://github.com/openai/codex/pull/25147) – Retry streamable HTTP initialize failures**  
  Resilience boost. Transient failures during RMCP startup and `tools/list` will now be automatically retried, reducing flaky connection drops.

## 5. Feature Request Trends
Three major directions are emerging from recent issues:

1. **Native Linux Client** – Issue [#11023](https://github.com/openai/codex/issues/11023) dominates with 477 👍. The community sees a native Linux app as the solution to power limitations on macOS and inconsistent WSL performance on Windows.

2. **Remote & Mobile Workflow Reliability** – Issues [#22802](https://github.com/openai/codex/issues/22802) and [#22851](https://github.com/openai/codex/issues/22851) highlight friction in mobile-to-desktop pairing. Developers want seamless “anywhere” access that just works.

3. **Enterprise Readiness** – Requests for custom plugin sharing defaults ([PR #25829](https://github.com/openai/codex/pull/25829)), enterprise network policy compliance ([#24814](https://github.com/openai/codex/issues/24814)), and EFS filesystem support ([#25220](https://github.com/openai/codex/issues/25220)) indicate the tool is penetrating deeper into corporate environments. Auto-resume on usage limits ([#21073](https://github.com/openai/codex/issues/21073)) also fits this trend.

## 6. Developer Pain Points
Recurring themes from the last 24 hours of issue activity:

- **Windows Sandbox Fragility** – The `spawn setup refresh` error ([#24391](https://github.com/openai/codex/issues/24391), [#25362](https://github.com/openai/codex/issues/25362)) is the single most disruptive Windows bug, cascading into Node REPL, Browser, and Computer Use tool failures.

- **macOS System Instability** – The `syspolicyd` / `trustd` related loops ([#25719](https://github.com/openai/codex/issues/25719), [#25882](https://github.com/openai/codex/issues/25882), [#25243](https://github.com/openai/codex/issues/25243)) are causing system-wide app launch freezes and resource exhaustion. This is a top-tier reliability emergency.

- **State and Context Loss** – Users are burned by disappearing chat histories ([#20741](https://github.com/openai/codex/issues/20741)) and context compaction failures ([#20931](https://github.com/openai/codex/issues/20931), [#26493](https://github.com/openai/codex/issues/26493)). Confidence in long-running sessions is at risk.

- **Cross-Platform Parity Gaps** – Mac, Windows, WSL, and Linux each have distinct showstoppers (WSL slowness, EFS plugin failure, missing native Linux app, macOS daemon thrash), fragmenting the developer experience across platforms.

- **Plugin/Tool Diagnostics Fragility** – Errors like “unknown variant vertical” ([#25418](https://github.com/openai/codex/issues/25418)), Computer Use screenshot failures ([#25178](https://github.com/openai/codex/issues/25178)), and MCP handshake timeouts ([#23840](https://github.com/openai/codex/issues/23840)) suggest the plugin system lacks robust error surfacing and environment validation.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-05

## Today's Highlights

The team shipped **v0.45.1** as a hotfix on the `v0.45.0` release line while the nightly pipeline (`v0.47.0`) gets a CI reliability overhaul. More notably, a concentrated wave of high-priority **terminal stability** and **agent loop** patches landed in the last 24 hours, addressing the community's most painful crash patterns (PTY resize errors, WSL interop, and 400 errors on function calls). Agent orchestration reliability remains the hottest topic, with the false-success-on-MAX_TURNS bug (#22323) and generalist agent hangs (#21409) still unresolved.

---

## Releases

### [v0.45.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.1) (Hotfix)
- Cherry-pick `665228e` from `release/v0.45.0-pr-27570`
- Patches a critical issue in the v0.45.0 release line

### [v0.47.0-nightly.20260604.g4196596f7](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-nightly.20260604.g4196596f7)
- CI: Optimized PR size labeler and batch workflows
- CI: Fixed `pull_request_target` trigger to grant write access on fork PRs

---

## Hot Issues (10 of 50 updated in last 24h)

1. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs** [P1, Bug]
   Highest community engagement this week (👍 8). The agent hangs indefinitely on simple tasks (folder creation). Users report the only workaround is explicitly instructing the model not to delegate to sub-agents. No fix committed yet.

2. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent MAX_TURNS falsely reported as GOAL success** [P1, Bug]
   A design flaw in agent orchestration: the `codebase_investigator` subagent returns `status: "success"` even when it hit its turn limit before performing any analysis. Masks costly timeouts and stalls debugging.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell commands stuck "Waiting input" after completion** [P1, Bug]
   Repeatedly reported. Trivial CLI commands complete but the PTY state machine never releases them. Continues to block the agent loop.

4. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component-level evaluations** [P1, Epic]
   Follow-up to the behavioral eval framework. Currently has 76 tests across 6 Gemini models. Community-impacting because this directly gates model quality improvements.

5. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser agent fails on Wayland** [P1, Bug]
   Linux users on Wayland (default on Fedora, modern Ubuntu) cannot use the browser subagent. Forces X11 workaround or avoidance.

6. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools** [P2, Bug]
   The agent hits API limits when tool declarations exceed the threshold. Expected behavior is smarter tool selection; current behavior is a hard crash.

7. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Agent doesn't use custom skills/sub-agents proactively** [P2, Bug]
   Users invest in custom skills (git, gradle) but the model ignores them unless explicitly prompted. Reduces ROI on custom agent setup.

8. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) / [#26523](https://github.com/google-gemini/gemini-cli/issues/26523) / [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory reliability** [P2, Bug Trio]
   Three issues filed by SandyTao520 expose security/reliability gaps: secrets leak before redaction, indefinite retries of low-signal sessions, and silent drops of invalid memory patches. Pending internal review.

9. **[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) — Subagents run without permission since v0.33.0** [P2, Bug]
   Configuration trust broken. Agents set to "disabled" across all configs are ignored after the update. Erodes confidence in settings governance.

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior** [P2, Feature/Bug]
    Users want safety rails for dangerous operations (git reset, `--force` flags, database mutations). The model currently does not distinguish between safe and destructive alternatives.

---

## Key PR Progress (10 of 34 updated in last 24h)

1. **[#27348](https://github.com/google-gemini/gemini-cli/pull/27348) — Wrap Ajv validate() in try/catch** [P1, CLOSED]
   Critical crash fix. Malformed schemas from the LLM (`Cannot read properties of undefined (reading 'type')`) were crashing `write_file`/`replace` tools. Merged.

2. **[#27335](https://github.com/google-gemini/gemini-cli/pull/27335) — Prevent SSRF via open redirect in web-fetch** [CLOSED]
   Security: The `fetchWithTimeout` utility followed redirects blindly. A public host could redirect the tool to `http://169.254.169.254/` (cloud metadata). Redirect chain now validated.

3. **[#27354](https://github.com/google-gemini/gemini-cli/pull/27354) — Bypass node-pty on WSL for Windows executables** [P2, CLOSED]
   Major UX win for WSL users. Windows `.exe` files run inside a Linux PTY had interop issues. Falls back to standard `child_process` automatically.

4. **[#27341](https://github.com/google-gemini/gemini-cli/pull/27341) — Strip functionCall.id before API call** [P2, CLOSED]
   Fixes the persistent "400 Unknown name 'id'" error on tool-calling turns. Internal IDs for ACP IDE rendering were leaking into the API payload.

5. **[#27329](https://github.com/google-gemini/gemini-cli/pull/27329) — Skip missing includeDirectories instead of crashing** [P1, CLOSED]
   One bad path in `settings.json` (`context.includeDirectories`) aborted CLI startup entirely. Now gracefully skips missing directories.

6. **[#27347](https://github.com/google-gemini/gemini-cli/pull/27347) — Validate commands to prevent NL saved as shell commands** [P2, CLOSED]
   Natural language input like "mostrar diretório" was being silently saved into command history via `/statusline`. Now validates input is a real command.

7. **[#27505](https://github.com/google-gemini/gemini-cli/pull/27505) — Fix extra spaces on width-0 CJK continuation cells** [P2, OPEN]
   Terminal rendering bug affecting international users: spurious whitespace injected between CJK characters in shell output. Important for copy-paste accuracy.

8. **[#27529](https://github.com/google-gemini/gemini-cli/pull/27529) — Handle EBADF errors in ShellExecutionService** [P2, OPEN]
   Directly addresses the crash in PTY resizing loops. Catches the Bad File Descriptor error gracefully instead of taking down the process.

9. **[#27524](https://github.com/google-gemini/gemini-cli/pull/27524) — Read bootstrap settings from correct path when GEMINI_CLI_HOME set** [P1, OPEN]
   Fixes a configuration bootstrap race condition for users setting a custom home directory.

10. **[#27331](https://github.com/google-gemini/gemini-cli/pull/27331) — Clarify settings.json path for GEMINI_CLI_HOME** [P3, CLOSED]
    Documentation fix resolving [#23622](https://github.com/google-gemini/gemini-cli/issues/23622). Explicitly notes user state path is `$GEMINI_CLI_HOME/.gemini/settings.json`.

---

## Feature Request Trends

- **Smarter Codebase Understanding:** The **AST-aware tools** initiative ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) is the most strategically significant feature request. Users want the agent to read method bounds and search syntax by shape rather than text, reducing turn counts and token waste.

- **Safety & Destructive Action Guardrails:** Recurring demand ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)) for the model to distinguish safe vs. destructive operations (git reset, force flags, DB writes). Users expect intelligent defaults and warnings.

- **Agent Configuration & Self-Awareness:** [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) captures a broader desire: the agent should know its own flags, hotkeys, and settings well enough to act as its own expert guide. [#22093](https://github.com/google-gemini/gemini-cli/issues/22093) reinforces that user settings must be strictly honored.

- **Remote/Enterprise Agent Infrastructure:** [#20303](https://github.com/google-gemini/gemini-cli/issues/20303) (Sprint 2 – Advanced Auth & Background Operations) signals heavy investment in enterprise-grade agent support, including task-level auth and 1P agent integration.

- **Evaluation & Quality Infrastructure:** Epics like [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) (component level evals) and [#23166](https://github.com/google-gemini/gemini-cli/issues/23166) (stabilizing internal evals) are internally driven but directly affect community trust in model quality.

---

## Developer Pain Points

1. **Agent Loop Hangs & False Successes**
   The #1 erosive issue. The generalist agent hangs indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), subagents report fake success on MAX_TURNS ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), and completed shell commands stay stuck in "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)). These break the core "gemini do X" workflow for a significant subset of users.

2. **Terminal/PTY Subsystem Instability**
   A cluster of high-priority PRs (*amitesh0303*, *samuelgirmametaferia*) are all targeting the same root cause: crashes on PTY resize events (`EBADF`), flicker on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)), and corruption after external editor exits ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)). This subsystem needs hardening.

3. **LLM Output Sanitization Gaps**
   The model regularly emits CJK characters in thought streams ([#27349](https://github.com/google-gemini/gemini-cli/pull/27349)), natural language in command slots ([#27347](https://github.com/google-gemini/gemini-cli/pull/27347)), and malformed schemas that crash tools ([#27348](https://github.com/google-gemini/gemini-cli/pull/27348)). These are handled by downstream patches but indicate a persistent LLM behavior problem.

4. **Browser Agent Environmental Fragility**
   Wayland incompatibility ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), ignored `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and profile lock contention ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)) make the browser agent unreliable across environments.

5. **Memory System Data Integrity**
   The Auto Memory feature is shipping with significant trust deficits: content leaks to the model before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), invalid patches are silently dropped ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and low-signal sessions are retried infinitely ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-05

## Today's Highlights
A busy day on the tracker as **v1.0.60-0** rolled out, bringing `/diff` vim navigation, a `billing` help topic, and a `-r` shorthand for `--resume`. Meanwhile, a long-running rate-limit saga (**#2101**) continues to dominate community discussion (27 comments, 17 👍), and a fresh regression report (**#3659**) shows that plugin hooks are blocking CLI startup for some Windows users. On the safety front, **#3684** raises a legitimate concern about subagent permission prompts lacking command context.

## Releases
### v1.0.60-0
- **New:** `billing` help topic providing an overview of AI credit usage features
- **Navigation:** Vim-style keys (`g`, `G`, `Ctrl+D`, `Ctrl+U`) added to the `/diff` view
- **Session Info:** Displays Mission Control sharing status for synced sessions
- **Shorthand:** `-r` is now available as an alias for `--resume`
- **Other:** LSP server configuration updates

---

## Hot Issues
*(Top 10 noteworthy issues from the last 24h, selected by community engagement and impact)*

#### #2101 — [area:models] Transient API error retry loop → hard rate limit
- **Comments:** 27 | **👍:** 17
- **Summary:** Users are hitting repeated `Request failed due to a transient API error. Retrying...` messages that ultimately end in a 60-second Copilot rate limit. The high comment count and strong reactions suggest this is a widespread backend stability concern affecting every session type.
- **Link:** [github/copilot-cli Issue #2101](https://github.com/github/copilot-cli/issues/2101)

#### #2082 — [area:platform-linux, area:input-keyboard] `ctrl+shift+c` no longer copies to clipboard on Linux
- **Comments:** 19 | **👍:** 8
- **Summary:** A regression dating to v1.0.4 has broken one of the most basic terminal copy actions on Ubuntu 24.04. Users note that `ctrl+c` and right-click still work, but the muscle-memory `ctrl+shift+c` path is non-functional in the Copilot context.
- **Link:** [github/copilot-cli Issue #2082](https://github.com/github/copilot-cli/issues/2082)

#### #3596 — [area:authentication, area:sessions, area:models] Session resume breaks `/model` authentication
- **Comments:** 2 | **👍:** 8
- **Summary:** Resuming a session with `--resume` causes `/model` to fail with `Error loading model list: Error: Not authenticated`. All other session commands work fine. The high 👍 count suggests many users rely on resumed sessions and hit this hard.
- **Link:** [github/copilot-cli Issue #3596](https://github.com/github/copilot-cli/issues/3596)

#### #2398 — [area:permissions, area:configuration] Support a default config file for permissions
- **Comments:** 3 | **👍:** 10
- **Summary:** A highly-upvoted feature request asking for a way to pre-approve access patterns (file read, tool execution) via a config file rather than approving every session. Permission fatigue is clearly a real UX blocker for power users.
- **Link:** [github/copilot-cli Issue #2398](https://github.com/github/copilot-cli/issues/2398)

#### #3666 — [area:input-keyboard, area:terminal-rendering] Copying wrapped output loses spaces (CLOSED)
- **Comments:** 3 | **👍:** 0
- **Summary:** A curious terminal rendering bug where copying wrapped code fragments from the CLI strips spaces — e.g., `var c = "";` becomes `varc`. Though closed, it signals lingering issues in the terminal output layer that affect developer productivity.
- **Link:** [github/copilot-cli Issue #3666](https://github.com/github/copilot-cli/issues/3666)

#### #3677 — [area:context-memory, area:models] Long context compaction triggers at 18% instead of ~91%
- **Comments:** 1 | **👍:** 0
- **Summary:** A deep technical bug: when using `claude-opus-4.7-1m-internal`, the CLI fetches model capabilities from two sources and uses the smaller (non-long-context) blob for capacity checks. This forces compaction and summarization at 18% of the true 936K context window. Significant for anyone pushing long-context boundaries.
- **Link:** [github/copilot-cli Issue #3677](https://github.com/github/copilot-cli/issues/3677)

#### #3659 — [area:platform-windows, area:plugins] Plugin hooks fail with PowerShell argument errors
- **Comments:** 3 | **👍:** 0
- **Summary:** v1.0.57 introduced a hard blocker for Windows users with plugins: all preToolUse hooks fail because `.ps1` arguments are passed incorrectly, making the CLI unusable until the hook system is bypassed. A high-impact regression for enterprise setups.
- **Link:** [github/copilot-cli Issue #3659](https://github.com/github/copilot-cli/issues/3659)

#### #3529 — [triage] Copilot PR review fails entirely across CLI and UI
- **Comments:** 3 | **👍:** 3
- **Summary:** Users report `Copilot encountered an error and was unable to review this pull request` with no clear resolution path. The failure spans both the CLI and GitHub UI, suggesting a service-side issue affecting an entire workflow path.
- **Link:** [github/copilot-cli Issue #3529](https://github.com/github/copilot-cli/issues/3529)

#### #3636 — [area:networking, area:models] Voice mode fails on corporate VPN
- **Comments:** 2 | **👍:** 3
- **Summary:** Enabling `/voice` fails because the CLI cannot reach the speech-to-text model catalog. This blocks anyone behind a corporate proxy or VPN from using the new voice features. Highlights a need for configurable catalog endpoints or fallback mechanisms.
- **Link:** [github/copilot-cli Issue #3636](https://github.com/github/copilot-cli/issues/3636)

#### #3684 — [area:permissions, area:agents] Subagent permissions lack command context
- **Comments:** 0 | **👍:** 0
- **Summary:** A fresh safety concern: subagent permission prompts only show `"/"` as the target directory without revealing the exact shell command to be run. This makes it impossible to evaluate whether the action is safe. Community signal is low (just filed), but the UX and security implications are significant.
- **Link:** [github/copilot-cli Issue #3684](https://github.com/github/copilot-cli/issues/3684)

---

## Key PR Progress
Pull request activity was very quiet in the last 24 hours. The two surfaced items are low quality / spam, and no community or bot-driven feature PRs were merged.

- **#3651** — "Create xcopilotcli" (OP: suspicious content)
- **#3473** — Spam commit (contains promotional link unrelated to the codebase)

No actionable PR progress to report from the open data. Development signal remains concentrated in the Issues tracker.

---

## Feature Request Trends
*Requests distilled across all recent issues*

1. **Permission Workflow Optimization** — The desire for persistent, configurable permissions (#2398) and clearer subagent tool context (#3684) is the strongest recurring theme. Users want "allow once" or config-driven models to avoid approval fatigue.
2. **Session Resume Reliability** — Multiple tickets (#3596, #3680) ask for resumed sessions to fully restore authentication state, including access to the model picker.
3. **Security Hardening for Integrations** — Requests for encrypted OAuth token storage on disk (#2783) and the ability to refresh BYOK credentials without a process restart (#3682).
4. **Extended Configuration Surface** — Custom slash commands at the machine level (#3343), agent-level `effort` / `context length` parameters (#3678), and configurable session worktrees (#3675).
5. **Localization / Accessibility** — A first request for Spanish localization of slash command descriptions (#3681), indicating a growing non-English user base.

---

## Developer Pain Points
*Recurring frustrations and high-frequency complaints*

- **Authentication State Loss on Resume** — A pattern is clear: resuming sessions can break model selection, credential awareness, and the `/model` command. This forces restarts and wastes time.
- **Copy/Paste Fragility** — The Linux `ctrl+shift+c` regression (#2082) has been open since March. Combined with SSH-tmux edge cases (#3260) and wrapped-text corruption (#3666), clipboard behavior is a persistent friction point.
- **Plugin / Hook System Regressions** — v1.0.57 broke hook execution on Windows (#3659), showing that the plugin infrastructure lacks effective cross-platform testing in the release pipeline.
- **Rate Limiting & Retry Logic Gaps** — Both generic transient API errors (#2101) and Azure OpenAI 429 throttling (#3679) exhaust their retry budget far too quickly due to insufficient backoff. Users are hitting hard timeouts.
- **Agent Context Breakdowns** — Sub-agents losing connection to the orchestrator (#2923), background agents silently hanging at `total_turns=0` (#3547), and premature context compaction (#3677) all point to the agent framework still maturing under real workloads.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** June 5, 2026

---

## 1. Today's Highlights

A core authorization bug is dominating community discussion this cycle, with two separate reports ([#2425](https://github.com/MoonshotAI/kimi-cli/issues/2425), [#2427](https://github.com/MoonshotAI/kimi-cli/issues/2427)) detailing persistent `403` errors blocking all functionality on the `kimi-for-coding` and `k2.6` models. On the development front, contributor `GH-ytym` responded rapidly with a fix for the Linux terminal auto-scroll bug ([#2429](https://github.com/MoonshotAI/kimi-cli/pull/2429)), while maintainer `Pluviobyte` has a substantial queue of session-reliability and data-integrity fixes awaiting merge or review.

---

## 2. Releases

No new releases were published in the last 24 hours. Active discussion spans versions `0.9.0` through `1.46.0`, indicating a fast-moving project.

---

## 3. Hot Issues

*5 issues were active in the last 24 hours. All are covered below.*

1. **[#2425] 403 Authorization Error (`kimi-for-coding`)** — *Open, 10 comments, 3 👍*
   The most impactful issue today. Users running version `0.9.0` receive a `403` on every message with the message "Kimi For Coding is currently only available for Coding Agents such as Kimi CLI, Claude Code, Roo Code, Kilo Code…". The high engagement suggests a widespread platform-level restriction or auth misconfiguration.
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2425)

2. **[#2427] Duplicate 403 Error (`k2.6`)** — *Open, 2 comments*
   A similar report targeting the `k2.6` model on Debian (WSL2), confirming the auth issue is not limited to a single model or macOS.
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2427)

3. **[#2422] Auto-scroll to Bottom on Output** — *Open, 1 comment*
   Users on Linux cannot scroll up to review completed conversation output because the terminal automatically jumps back to the bottom roughly every second. A significant UX regression for anyone reviewing long responses.
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2422)

4. **[#2430] Auto Logout Mid-Task** — *Closed*
   After leaving a task idle, the user returned to find themselves logged out. Disrupts long-running background workflows. Marked as closed, but the root cause warrants attention.
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2430)

5. **[#2428] `/title` Command Missing from VS Code Extension** — *Open*
   The `/title` command works in the standalone CLI but is unavailable in the VS Code extension, highlighting a feature parity gap between the two interfaces.
   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2428)

---

## 4. Key PR Progress

*6 pull requests are open or were updated in this cycle.*

1. **[#2429] Fix: Prevent Linux Terminal Auto-Scroll** — `GH-ytym`
   A direct fix for [#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422). Stops the idle cursor blink from forcing a viewport scroll to the bottom. Notable for its rapid turnaround (issue and fix on consecutive days).
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2429)

2. **[#2388] Fix: Persist Pasted Text Placeholders** — `Pluviobyte`
   Long pasted text is folded into `[Pasted text #N]` placeholders. This fix ensures those placeholders survive prompt recall and session history replay, preventing data loss.
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2388)

3. **[#2387] Fix: Preserve Shell Command Headlines** — `Pluviobyte`
   Addresses aggressive truncation of `Used Shell (...)` command headlines. Improves readability of terminal output during tool-using workflows.
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2387)

4. **[#2386] Fix: Map Undo Wire Turns to Context Turns** — `Pluviobyte`
   Critical fix for `/undo` and fork behavior. Previously, local slash-command turns could break the context index, leading to corrupt state on undo. Correctly maps wire turns to context turns.
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2386)

5. **[#2383] Fix: Repair Orphan `tool_calls` on History Replay** — `Pluviobyte`
   If a session is killed mid-turn (OOM, terminal close, `kill -9`), the persisted `context.jsonl` can contain orphan `tool_calls`. This fix repairs state on replay, preventing crashes during recovery.
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2383)

6. **[#2382] Fix: Convert Unsupported Image Formats to PNG** — `Pluviobyte`
   Providers (Kimi, Anthropic, Google) support limited image formats. This adds automatic conversion (e.g., `.ico` → `.png`) in `ReadMediaFile` to prevent failures on unusual file types.
   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2382)

---

## 5. Feature Request Trends

Although the current cycle is heavy on bug reports, several distinct user needs can be inferred from the data:

- **Transparent and Resilient Authentication**: The `403` authorization errors ([#2425](https://github.com/MoonshotAI/kimi-cli/issues/2425), [#2427](https://github.com/MoonshotAI/kimi-cli/issues/2427)) suggest users strongly desire a clear, non-blocking authentication flow. Automatic re-authentication or session refresh is likely a high-priority unspoken request.
- **CLI–Editor Feature Parity**: The missing `/title` command in VS Code ([#2428](https://github.com/MoonshotAI/kimi-cli/issues/2428)) implies users expect all CLI commands to work seamlessly within editor extensions.
- **Robust Session Resilience**: Implicit in issues like [#2430](https://github.com/MoonshotAI/kimi-cli/issues/2430) (auto-logout) and PRs like [#2383](https://github.com/MoonshotAI/kimi-cli/pull/2383) (crash recovery) is a clear demand for long-running, crash-resistant sessions.
- **Cross-Platform UI Polish**: The Linux-specific terminal rendering bug ([#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422)) and command truncation ([#2387](https://github.com/MoonshotAI/kimi-cli/pull/2387)) indicate a need for dedicated TTY optimization beyond macOS.

---

## 6. Developer Pain Points

- **Authorization Gatekeeping Is Paralyzing**: The `403` error is the single biggest frustration this cycle. It is a hard block that completely halts all user workflows and dominates community discussion (10 comments on one issue in 24 hours).
- **Session and History Unreliability**: Mid-task logouts ([#2430](https://github.com/MoonshotAI/kimi-cli/issues/2430)) and crash-related data corruption ([#2383](https://github.com/MoonshotAI/kimi-cli/pull/2383)) severely erode trust in the tool for complex or long-running tasks.
- **Terminal UI Friction**: The auto-scroll bug ([#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422)) makes reviewing LLM output nearly impossible on Linux, directly undermining the core CLI value proposition.
- **Version Fragmentation**: Users reporting bugs across versions `0.9.0`, `1.36.0`, and `1.46.0` suggests a rapid release cadence where fixes either don't propagate or new regressions emerge quickly.
- **Editor Extension as a Second-Class Citizen**: The feature gap between the standalone CLI and the VS Code extension ([#2428](https://github.com/MoonshotAI/kimi-cli/issues/2428)) forces developers to context-switch between environments.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for June 5, 2026, covering the latest releases, active discussions, and code contributions.

---

## OpenCode Community Digest: 2026-06-05

### 1. Today’s Highlights
v1.16.0 shipped with managed workspace cloning, session mobility between workspaces, and native Bedrock support for OpenAI models, signaling a strong focus on infrastructure robustness. Community attention is split between a centralized **Memory Megathread** (#20695) and a suite of deeply technical bug reports from user `LifetimeVip` that expose critical vulnerabilities in compaction and context management. The ongoing debate over adjusting subscription limits to match DeepSeek V4’s price cut (#28846) remains the hottest economic topic.

---

### 2. Releases

**v1.16.0** — [View Release](https://github.com/anomalyco/opencode/releases/tag/v1.16.0)

- **Core Improvements:**
  - Added **managed workspace cloning** that preserves dirty and untracked files.
  - Added support for **moving sessions between workspaces and directories**.
  - Added proper **OpenAI model support through AWS Bedrock**.
  - Added **skill discovery and file-based agent loading**.
  - Updated **GitHub Copilot usage** integration.

---

### 3. Hot Issues

Picked from the top 30 most-commented issues updated in the last 24 hours.

1.  **#20695 – Memory Megathread** (90 💬, 63 👍)
    A central hub for collecting heap snapshots to debug widespread memory leaks. The team explicitly warns against LLM-generated "solutions."
    [Issue Link](https://github.com/anomalyco/opencode/issues/20695)

2.  **#28846 – DeepSeek V4 Permanent 75% Price Reduction** (69 💬, 74 👍)
    Community demands OpenCode Go subscription limits reflect the API price cut. Indicates high user sensitivity to provider economics.
    [Issue Link](https://github.com/anomalyco/opencode/issues/28846)

3.  **#27589 – Alpine Linux (musl) TUI Regression** (27 💬, 12 👍)
    v1.14.50 breaks the TUI render library on musl-based systems (`getcontext` symbol not found). Blocks users on Alpine.
    [Issue Link](https://github.com/anomalyco/opencode/issues/27589)

4.  **#30811 – Compaction Loses Context; No Verification** (6 💬)
    A critical five-point analysis of code quality degradation in long conversations. Highlights that compaction throws away crucial context.
    [Issue Link](https://github.com/anomalyco/opencode/issues/30811)

5.  **#1168 – Feature Request: Clickable Links** (6 💬, 91 👍)
    The highest upvoted item this cycle. Users want `Ctrl+Click` URL support in the TUI for better workflow integration.
    [Issue Link](https://github.com/anomalyco/opencode/issues/1168)

6.  **#17169 – Subagent Infinite Retry Loop** (4 💬)
    Subagents enter an unbounded retry loop on tool failure, burning $15+ per invocation. A significant operational cost risk.
    [Issue Link](https://github.com/anomalyco/opencode/issues/17169)

7.  **#30839 – 0 MCP Services After Upgrade** (2 💬, 1 👍)
    v1.15.13 breaks MCP service detection. Users are forced to downgrade to v1.15.12.
    [Issue Link](https://github.com/anomalyco/opencode/issues/30839)

8.  **#30799 – Prompt Injection via `<system-reminder>` Tags** (3 💬)
    File content is not sanitized for system-reminder tags, allowing users to override system prompts via the `read` tool.
    [Issue Link](https://github.com/anomalyco/opencode/issues/30799)

9.  **#12789 – "Model not supported" for Copilot Claude** (16 💬)
    Copilot provider works for Gemini but fails for Claude models. Widespread confusion about provider support.
    [Issue Link](https://github.com/anomalyco/opencode/issues/12789)

10. **#30831 – `opencode completion` is Truncated** (2 💬)
    The generated Zsh script is cut mid-string, producing an unparseable completion file.
    [Issue Link](https://github.com/anomalyco/opencode/issues/30831)

---

### 4. Key PR Progress

Picked from the top 20 PRs updated in the last 24 hours.

1.  **#30789 – Persist V2 Session Context Epochs** (`kitlangton`)
    [Merged] Stores immutable baseline context with structured source snapshots, ensuring context integrity across restarts.
    [PR Link](https://github.com/anomalyco/opencode/pull/30789)

2.  **#30820 – Bedrock OpenAI Model URLs** (`PershingSquare`)
    [Merged] Adds URL variable substitution for AWS Bedrock Mantle endpoints. Closes #30819.
    [PR Link](https://github.com/anomalyco/opencode/pull/30820)

3.  **#29901 – Snowflake Cortex Provider** (`kameshsampath`)
    [Merged] Adds a new major enterprise provider to the ecosystem.
    [PR Link](https://github.com/anomalyco/opencode/pull/29901)

4.  **#30678 – Desktop Multi-Server Support** (`Hona`)
    [Open] Introduces server isolation, filtered session lists, and project scope headers for the desktop home screen.
    [PR Link](https://github.com/anomalyco/opencode/pull/30678)

5.  **#30224 – Clearer Tool Schema Error Messages** (`nikhilkulkarni1755`)
    [Open] Improves local model debugging by printing expected vs. received JSON keys on tool call errors.
    [PR Link](https://github.com/anomalyco/opencode/pull/30224)

6.  **#30836 – Fix Errored Compaction Summaries** (`ShamirSecret`)
    [Open] Prevents compaction from leaving ghost `finish` errors when the summarization LLM call fails.
    [PR Link](https://github.com/anomalyco/opencode/pull/30836)

7.  **#30837 – Optimize First-Time `snapshot.track`** (`ayubun`)
    [Open] Eliminates per-blob duplication contributing to snapshot directory bloat. Addresses three related issues.
    [PR Link](https://github.com/anomalyco/opencode/pull/30837)

8.  **#24962 – Apply Agent Variant at Runtime** (`21pounder`)
    [Open] Fixes #21632 where subagent model variants were parsed but silently ignored during execution.
    [PR Link](https://github.com/anomalyco/opencode/pull/24962)

9.  **#30824 – Color Themes for Desktop App** (`arvsrn`)
    [Merged] Adds `resolveThemeVariantV2` for runtime palette resolution and v2 semantic token mapping.
    [PR Link](https://github.com/anomalyco/opencode/pull/30824)

10. **#30828 – Public Native Effect API** (`kitlangton`)
    [Merged] Exports `@opencode-ai/core/public` as the official embedding API for native Effect applications.
    [PR Link](https://github.com/anomalyco/opencode/pull/30828)

---

### 5. Feature Request Trends

1. **Provider Economics & Flexibility**
   - Users are aggressively price-sensitive, demanding automatic usage limit adjustments for provider price cuts (DeepSeek V4) and quick support for new model tiers (AWS Bedrock GPT-5.5/5.4).

2. **Session State Management**
   - High demand for `--resume <session>` CLI flags, local-time log filenames, and robust session history persistence (non-destructive deletion).

3. **Extensibility & Embedding**
   - A clear push towards first-class plugin integrations (Systematic) and embedding OpenCode into custom Effect apps via the new public Native API.

4. **TUI/Desktop QoL**
   - "Clickable Links" broke 91 upvotes. Users also want color themes, proper terminal signal handling (no SIGTSTP on Ctrl+Z), and notifications inside tmux/zellij.

---

### 6. Developer Pain Points

- **Regression Frequency:** Multiple reports (Alpine musl, MCP services, Windows Ctrl+C/Exit) indicate point-releases are introducing hard breakages, eroding trust in safe upgrades.
- **Operational Cost Risks:** The subagent infinite retry loop (#17169) remains a significant financial liability for users running multi-step workflows, highlighting a gap in retry budgets.
- **Local Model Friction:** Persistent issues with vLLM compatibility, Ollama file writes, and schema mismatches (wrong JSON keys) dominate the local-model user experience.
- **Context Window Fragility:** The wave of reports from `LifetimeVip` (#30791, #30795, #30799, #30805, #30811) reveals poorly enforced invariants in read-before-edit checks, compaction overflow thresholds, and prompt injection sanitization.
- **State Corruption:** Race conditions in session deletion and SQLite pragma failures suggest underlying concurrency and database migration issues remain unaddressed.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi community digest for June 5, 2026.

---

### 1. Today’s Highlights

**Release v0.78.1** expands provider support with NVIDIA NIM and MiniMax-M3, and gives extensions richer access to the system runtime. The community remains laser-focused on the critical `openai-codex` hang bug ([#4945](https://github.com/earendil-works/pi/issues/4945)), which dominates discussion. On the infrastructure front, significant work is progressing on a dedicated Anthropic Vertex provider ([#5262](https://github.com/earendil-works/pi/pull/5262)) and a new workspace approval system ([#5332](https://github.com/earendil-works/pi/pull/5332)), signaling a strong push toward enterprise readiness and security.

---

### 2. Releases

**Version 0.78.1** is now available ([release](https://github.com/badlogic/pi-mono/releases/tag/v0.78.1)).

- **New Providers:** Added Ant Ling and NVIDIA NIM setup. MiniMax-M3 support added for direct MiniMax providers.
- **Extension Context:** Extensions can now leverage `ctx.mode` and `ctx.getSystemPromptOptions()` for more context-aware tooling and configuration reading.

---

### 3. Hot Issues

**10 noteworthy issues currently driving community discussion:**

1. **[#4945](https://github.com/earendil-works/pi/issues/4945) — `openai-codex` hang on “Working…”**  
   The top-voted open issue (52 comments, 27 👍). The TUI freezes with no feedback, forcing an abort. Currently labeled `inprogress`.

2. **[#5386](https://github.com/earendil-works/pi/issues/5386) — Crash in `getSessionStats()` with Ollama**  
   A hard crash surfaces when an assistant message is missing the `usage` field. A critical papercut for local-model users.

3. **[#5373](https://github.com/earendil-works/pi/issues/5373) — High idle CPU on large sessions**  
   Users report ~24% CPU usage on 150k+ token sessions at rest. The report includes excellent `strace` data for debugging.

4. **[#5188](https://github.com/earendil-works/pi/issues/5188) — Shift+Enter submits instead of newline**  
   A common terminal convention broken in the TUI. Conflicts with user keybindings and degrades the editing experience.

5. **[#5363](https://github.com/earendil-works/pi/issues/5363) — Request: `amazon-bedrock-mantle` provider**  
   A new provider requested to support Bedrock’s OpenAI-compatible Mantle models, separate from the existing Converse API provider.

6. **[#5350](https://github.com/earendil-works/pi/issues/5350) — Windows paths break Linux remote tools**  
   A serious extensibility blocker: custom file operations pass host-OS resolved paths (Windows `\`) to remote Linux targets, breaking cross-platform remote workflows.

7. **[#5384](https://github.com/earendil-works/pi/issues/5384) — DeepSeek “developer” role regression via proxies**  
   The `detectCompat` fix from #1048 doesn’t cover proxied connections (e.g., OpenRouter), causing repeated 400 errors.

8. **[#5368](https://github.com/earendil-works/pi/issues/5368) — Phantom follow-up prompts**  
   The agent hallucinates a second, unrelated request from the user immediately after completing a task, eroding trust in deterministic behavior.

9. **[#5389](https://github.com/earendil-works/pi/issues/5389) — Mac Speech-to-Text freezes Pi**  
   Activating macOS STT while Pi is processing locks the TUI completely until the process is killed.

10. **[#5331](https://github.com/earendil-works/pi/issues/5331) — `maxTokens` ignored for OpenCode Go**  
    The API parameter `max_completion_tokens` is sent instead of `max_tokens`, which the backend ignores. (Now fixed by PR #5400).

---

### 4. Key PR Progress

**10 important pull requests that landed or made progress today:**

1. **[#5262](https://github.com/earendil-works/pi/pull/5262) — feat(ai): Add Anthropic Vertex provider**  
   Opens the enterprise GCP market by adding native support for Claude on Vertex AI, reusing the existing Anthropic streaming pipeline.

2. **[#5332](https://github.com/earendil-works/pi/pull/5332) — feat(config): Approval system for workspaces**  
   Introduces a `.pi.user` directory and interactive approval mode to prevent untrusted workspace configurations from executing without consent.

3. **[#5281](https://github.com/earendil-works/pi/pull/5281) — feat(coding-agent): Keybindings for all commands**  
   Unifies built-in and extension commands under a `cmd.<name>` keybinding convention, giving power users full control over shortcuts.

4. **[#5400](https://github.com/earendil-works/pi/pull/5400) — fix(ai): Map `maxTokens` to `max_tokens` for OpenCode**  
   Directly fixes #5331, correcting the parameter mapping for OpenCode and OpenCode Go providers.

5. **[#5410](https://github.com/earendil-works/pi/pull/5410) — fix: Persist restored session model as default**  
   Solves the UX issue where `pi -c` would restore a session but reset the default model, making new model selection feel arbitrary.

6. **[#5399](https://github.com/earendil-works/pi/pull/5399) — fix(extensions): Surface deferred-extension commands**  
   Fixes a race condition where commands from deferred-load extensions were missing from TUI autocomplete.

7. **[#5379](https://github.com/earendil-works/pi/pull/5379) — fix: Absolute paths for user-scoped packages**  
   Improves config portability by storing user-scoped local package installs as absolute paths instead of relative ones.

8. **[#5385](https://github.com/earendil-works/pi/pull/5385) — feat(coding-agent): First-run terminal theme detection**  
   Adds a polished onboarding UX by querying the terminal’s color scheme via OSC to automatically set a matching light or dark theme.

9. **[#5397](https://github.com/earendil-works/pi/pull/5397) — fix: Alt+Delete word deletion on Mac**  
   Adds native Mac text editing behavior (word-level delete) to the TUI input field, matching OS-level conventions.

10. **[#5371](https://github.com/earendil-works/pi/pull/5371) — fix(coding-agent): Space between skill and user messages**  
    A small but highly visible UI polish fix: `/skill` messages are no longer concatenated directly with the user’s follow-up text.

---

### 5. Feature Request Trends

The community’s signal is converging on four key themes:

- **Enterprise & Multi-Cloud Depth:** A clear push for native providers on major clouds (GCP Vertex AI, AWS Bedrock Mantle) and dedicated hardware providers (NVIDIA NIM).
- **Remote-First Development:** Features enabling agents to operate on remote machines (SSH execution, remote containers, cross-platform file systems) are in high demand, evolving Pi from a local tool into a distributed control plane.
- **Extensible Agent Infrastructure:** Developers want deeper SDK hooks: programmatic slash command execution, MCP structured content, custom UI loaders, and configurable tool execution commands.
- **Model Compatibility Automation:** The community is asking for smarter automatic detection of provider-specific API quirks (parameter naming, role aliases, streaming behavior) to reduce reliance on manual `compat` configuration.

---

### 6. Developer Pain Points

- **Provider API Fragmentation:** Mapping `max_tokens`, `max_completion_tokens`, `developer`/`system` roles, and thinking levels across dozens of providers remains the single largest source of issue reports. Each new provider (OpenCode, Fireworks, Bedrock Mantle) introduces minor but breaking API differences.
- **Stability Regressions:** Long-running issues like the `openai-codex` hang (#4945) and crashes on missing data fields (#5386) are eroding confidence in the core agent loop.
- **Cross-Platform Inconsistency:** Mac-specific freezes (STT, #5389), Windows path separators leaking into remote operations (#5350), and non-standard keybindings (#5188, #5397) create a fragmented UX that demands platform-specific workarounds.
- **Unpredictable Agent Behavior:** Hallucinated follow-up prompts (#5368) and silent configuration mutations (#5355) introduce a trust deficit, making an agentic tool feel less deterministic than developers expect.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-05

## Today’s Highlights
The daemon-mode initiative continues its push toward ACP/REST parity, with a 24-method extension batch and a comprehensive RFD alignment tracking issue now open. On the stability front, critical patches landed for prompt cache busting caused by MCP deferred tool listings and background auto-updates breaking cross-provider model switching. Community energy is concentrated on persistent memory systems, enhanced usage analytics, and headless Linux compatibility.

## Releases
- **[v0.17.1-nightly.20260605.715266537](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260605.715266537)** — Routine nightly release. Includes a fix from @he-yufeng for the `/copy` command skipping internal thought blocks in copied output, ensuring only user-facing content is captured.

---

## Hot Issues

1. **[#4782 — ACP Streamable HTTP Transport Implementation Status & RFD Alignment](https://github.com/QwenLM/qwen-code/issues/4782)**  
   Daemon now speaks `agent-client-protocol` natively. Editors like Zed, Goose, and JetBrains can connect without adapter shims. This is the key interoperability milestone for the `qwen serve` path.

2. **[#4777 — Deferred-Tools Listing in System Prompt Busts Prompt Cache](https://github.com/QwenLM/qwen-code/issues/4777)**  
   A significant performance concern flagged by @qqqys: every MCP progressive discovery or tool reveal via `ToolSearch` invalidates the cached system prompt, incurring a full cache miss on subsequent turns.

3. **[#4758 — Background Auto-Update Replaces Chunks Mid-Session, Breaking Model Switching](https://github.com/QwenLM/qwen-code/issues/4758)**  
   When `npm install -g` runs in the background, content-hash filenames in `chunks/` change. Dynamic `import()` by `authType` fails for providers not yet loaded — a critical runtime bug for users switching between OpenAI/Anthropic providers mid-session.

4. **[#4722 — Statusline Shows Model ID Instead of Human-Readable Name](https://github.com/QwenLM/qwen-code/issues/4722)**  
   `ui.currentModel` or `cfg.getModel()` returns raw IDs like `qwen3-coder-plus` rather than `Qwen3 Coder Plus`. Affects multi-model setups where the raw ID is used as a unique key.

5. **[#4754 — `/model` Should Not Persist to Settings by Default](https://github.com/QwenLM/qwen-code/issues/4754)**  
   Running `/model qwen-plus` writes the selection to `settings.json` via `persistSetting()`, making temporary session switches survive restarts. Community consensus favors explicit opt-in to persist.

6. **[#4747 — Global User-Level Auto-Memory at `~/.qwen/memories/`](https://github.com/QwenLM/qwen-code/issues/4747)**  
   Currently auto-memory is scoped per-project. This request for cross-project user memory (preferences, working style) mirrors Claude’s user memory feature and received strong community traction.

7. **[#4597 — Enhanced `/stats` with Cross-Session Dashboard](https://github.com/QwenLM/qwen-code/issues/4597)**  
   Community-requested feature to match Claude Code’s stats experience. Proposes persistent usage history in `~/.qwen/usage-history.json` and an interactive full-screen dashboard with Session/Activity/Efficiency tabs.

8. **[#4723 — Does Qwen Code Support a Rule System?](https://github.com/QwenLM/qwen-code/issues/4723)**  
   A frequently asked question distinguishing "rules" (Claude Code, Copilot Instructions) from skills. High demand for language-style and cross-session guidance without requiring custom skill definitions.

9. **[#4769 — Display Git Branch Prominently in Desktop UI](https://github.com/QwenLM/qwen-code/issues/4769)**  
   Git branch info is currently buried in a tooltip. Users want it visible in the main toolbar when the working directory is a git repository.

10. **[#4712 — `/bug`, `/docs`, `/insight` Crash with `spawn xdg-open ENOENT` on Headless Linux](https://github.com/QwenLM/qwen-code/issues/4712)**  
    Containers, SSH sessions, and minimal installs crash the process when UI commands try to spawn a desktop opener. Blocks developers operating in remote/CI environments.

---

## Key PR Progress

1. **[#4490 — Merge Daemon-Mode Feature Batch into Main](https://github.com/QwenLM/qwen-code/pull/4490)**  
   A massive integration merge (46 commits, 386 files, +115k/−12k LOC) from `daemon_mode_b_main`. Covers the core daemon feature set for v0.16-alpha, including workspaces, ACP bridge, and lifecycle management.

2. **[#4736 — ACP/REST Parity Wave 1 (24 Extension Methods)](https://github.com/QwenLM/qwen-code/pull/4736)**  
   Adds `_qwen/*` extensions to the ACP HTTP dispatch: session extensions, memory operations, file I/O, and auth — achieving near-complete functional parity between REST and ACP transports.

3. **[#4781 — Keep Deferred-Tools Listing Out of Cached System Prompt](https://github.com/QwenLM/qwen-code/pull/4781)**  
   Direct fix for #4777. Moves the MCP deferred tool listing from the cached system prompt into a per-turn `<system-reminder>`, preserving prompt cache validity across tool reveals.

4. **[#4760 — Handle Background Auto-Update Breaking Model Switching](https://github.com/QwenLM/qwen-code/pull/4760)**  
   Fixes the `Cannot find module` error in #4758 by eagerly loading generator modules and locking chunk references during auto-update.

5. **[#4780 — Add `/fork` Background-Agent Command](https://github.com/QwenLM/qwen-code/pull/4780)**  
   Implements a true background fork agent that inherits the full conversation context (system prompt, history, tools) and runs a directive without blocking the main conversation.

6. **[#4779 — Interactive `/stats` Dashboard with Cross-Session Tracking](https://github.com/QwenLM/qwen-code/pull/4779)**  
   Community contribution implementing three-tab dashboard (Session, Activity, Efficiency) with persistent usage history. Directly addresses the requested feature in #4597.

7. **[#4677 — Vim Mode Fixes: Esc Leak, Enter Submit, Render Lag](https://github.com/QwenLM/qwen-code/pull/4677)**  
   Three critical vim mode fixes: prevents Esc from triggering AppContainer's handler in INSERT mode, fixes Enter submission, and adds missing NORMAL-mode commands.

8. **[#4572 — Harden Auto Mode Self-Modification Checks](https://github.com/QwenLM/qwen-code/pull/4572)**  
   Prevents auto-mode LLM writes from bypassing the classifier on config files, hooks, commands, and MCP configuration. Splits classifier permissions for safer autonomous operation.

9. **[#4766 — Preserve Non-ASCII Git Paths in File Crawler](https://github.com/QwenLM/qwen-code/pull/4766)**  
   Disables Git's octal path quoting in the file crawler so non-ASCII tracked filenames return as proper UTF-8. Includes regression tests against repos with Git path quoting enabled.

10. **[#4719 — Bundle Extension Examples in `dist/`](https://github.com/QwenLM/qwen-code/pull/4719)**  
    Fixes the packaging pipeline so built-in extension example templates are included in the distributed package, resolving a long-standing issue where examples were missing post-install.

---

## Feature Request Trends

- **Protocol Unification (ACP/REST):** The largest architectural trend is the daemon becoming an ACP-native server. The new Streamable HTTP transport (#4782) positions Qwen Code as a drop-in backend for third-party editors, driving requests for full parity and stable interop APIs.
- **Persistent Intelligence Across Sessions:** Three complementary requests dominate: a proper rule system (#4723) for language/style guidance, global user memory (#4747) for cross-project preferences, and persistent usage analytics (#4597) for cost/efficiency tracking. The community clearly wants the tool to "remember" at every layer.
- **Agent Orchestration Depth:** Users are pushing beyond single-turn auto-mode. Background fork agents (#4757), configurable sub-agent concurrency (#3568), and non-LLM context compression (#4264) indicate demand for sophisticated multi-agent workflows.
- **Local-First Diagnostics:** The diagnostic framework proposal (#4421) — providing a ring buffer, diagnostic IDs, and `/bug collect bundle` — reflects a desire for self-service debugging without requiring debug mode or tracing infrastructure.

---

## Developer Pain Points

- **Prompt Cache Instability:** The deferred MCP tools busting the system prompt cache (#4777) is the most technically painful issue this week. For users leveraging MCP tool ecosystems, this degrades every turn into a cold-cache request, directly impacting latency and cost.
- **Installation & Runtime Environment:** Headless Linux remains underserved (#4712) — commands that assume a desktop environment crash hard. Auto-update mechanisms continue to fight with system permissions and module loading (#4758, #4627), creating a brittle upgrade path for `npm -g` users.
- **UI Configuration Surprises:** The `/model` persistence issue (#4754) exemplifies a recurring tension between temporary commands and permanent settings. Combined with the raw model ID display (#4722), configuration state management in the CLI creates ongoing cognitive friction.
- **Core UX Regressions:** Desktop app input handling (#4772) and vim mode Escape key leaks (#4677) are the kind of flow-breaking bugs that erode daily trust in the interface, even when the backend engine is stable.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest
**Date:** 2026-06-05  
**Project:** CodeWhale (the DeepSeek TUI platform under `Hmbown/CodeWhale`)

---

## 1. Today's Highlights

The project entered a formal stabilization push for **v0.9.0** ([#2721](https://github.com/Hmbown/CodeWhale/issues/2721)), establishing a dedicated gate to resolve long-standing Windows, large-repo, and subagent blockers before the feature drop. Maintainers actively merged several community-harvested PRs, most notably **provider auth rollback** ([#2769](https://github.com/Hmbown/CodeWhale/pull/2769)) to prevent IDE lockouts and **custom search endpoints** ([#2767](https://github.com/Hmbown/CodeWhale/pull/2767)) for private API users. A substantial community PR ([#2753](https://github.com/Hmbown/CodeWhale/pull/2753)) introducing a **multi-tab system with cross-tab collaboration** signals strong grassroots interest in richer workspace management inside the TUI itself.

---

## 2. Releases

No releases in the last 24 hours.

---

## 3. Hot Issues (10 Noteworthy)

### [#2766 UI Refactor needed](https://github.com/Hmbown/CodeWhale/issues/2766)
by *mo-vic* — Direct user feedback on core TUI friction: output is difficult to copy, and confirmation popups obscure the main interface while showing mostly useless information. A raw signal that the TUI layer needs ergonomic investment.

### [#2721 v0.9.0 Stabilization gate](https://github.com/Hmbown/CodeWhale/issues/2721)
by *Hmbown* — Release-blocker meta-issue explicitly calling out Windows, large-repo, subagent, and live-state blockers. This is the maintainer’s roadmap signal for the next major version.

### [#2758 Wrong resume command in sessions footer](https://github.com/Hmbown/CodeWhale/issues/2758)
by *sximelon* — The CLI’s own help text prints `codewhale --resume <session-id>`, but `--resume` is not a valid top-level flag. A simple but trust-eroding documentation bug in the dispatcher.

### [#2739 Task freezes, connection timeouts, session loss](https://github.com/Hmbown/CodeWhale/issues/2739)
by *zoomtint* — User reports tasks freezing into infinite waits, ESC failing to recover, and sessions fully lost on `--continue`. Explicitly states this has been a recurring issue across versions (0.8.51 → 0.8.52), making it a high-urgency reliability regression.

### [#2648 Deferred tool hydration renders as completed run](https://github.com/Hmbown/CodeWhale/issues/2648)
by *Hmbown* — Deferred tool schemas are displayed as a finished run in the live transcript, showing `run done` even though the tool was merely loaded, not executed. A correctness/trust issue for agent visibility.

### [#2744 MCP tool name parsing breaks with underscores](https://github.com/Hmbown/CodeWhale/issues/2744)
by *lioryx* — `McpPool::parse_prefixed_name` uses `split_once('_')` to decompose `mcp_{server}_{tool}` names. Any server name containing an underscore (e.g., `my_db`) splits at the wrong boundary, routing calls to a nonexistent server. A fragile protocol implementation.

### [#2666 Telemetry: agents need visible token/context usage](https://github.com/Hmbown/CodeWhale/issues/2666)
by *Hmbown* — During long multi-agent tasks, agents have no visibility into token budget, context window pressure, or elapsed time. A deep UX gap for agentic workflows.

### [#2752 Run Trace Export for WhaleFlow/Model Lab](https://github.com/Hmbown/CodeWhale/issues/2752)
by *nayar-900* — Requests a structured way to export run traces including model config, outputs, and token usage. Without this, multi-model evaluations lack audit trails.

### [#2743 Adapt Claude Code skills ecosystem](https://github.com/Hmbown/CodeWhale/issues/2743)
by *AiurArtanis* — Strategic request to make CodeWhale a consumer of the broader Claude Code skill library. Acknowledges the “transpilation” complexity but highlights interest in breaking provider lock-in while accessing existing skill ecosystems.

### [#2749 Project-level .codewhale/mcp.json auto-merge](https://github.com/Hmbown/CodeWhale/issues/2749)
by *yekern* — Documentation states project MCP server config is supported, but the binary only loads from user-level config. A request for intuitive merging semantics rather than replacement.

---

## 4. Key PR Progress (10 Important)

### [#2769 / #2755 Provider auth rollback](https://github.com/Hmbown/CodeWhale/pull/2769) (Merged)
by *Hmbown* (harvest from *cyq1017*) — Snapshots provider state before first request; on auth failure (e.g., Kimi/Moonshot), restores the previous provider, model, and runtime config. Fixes the lock-out scenario reported in [#2754](https://github.com/Hmbown/CodeWhale/issues/2754).

### [#2768 Custom completion sound files](https://github.com/Hmbown/CodeWhale/pull/2768) (Merged)
by *Hmbown* (harvest from *cyq1017*) — Adds `completion_sound = "file"` and `[notifications].sound_file` config, using native Windows `PlaySoundW` for async WAV playback. Fulfills [#2484](https://github.com/Hmbown/CodeWhale/issues/2484).

### [#2767 Custom DuckDuckGo search endpoint](https://github.com/Hmbown/CodeWhale/pull/2767) (Merged)
by *Hmbown* (harvest from *cyq1017*) — Adds `[search].base_url` for DuckDuckGo-compatible private search endpoints, gating network policy on the configured host. Closes [#2436](https://github.com/Hmbown/CodeWhale/issues/2436).

### [#2764 Gate shell child kill helper off Windows](https://github.com/Hmbown/CodeWhale/pull/2764) (Merged)
by *Hmbown* — Fixes a Windows CI `-D warnings` build failure by compiling `ShellChild::kill` only on non-Windows. Keeps Windows on existing job-object cleanup paths.

### [#2763 Refresh branch status after shell changes](https://github.com/Hmbown/CodeWhale/pull/2763) (Merged)
by *Hmbown* — Immediately refreshes cached workspace branch/status after shell-family tool completions, with async redraw support. Improves project mode DX after git operations.

### [#2745 / #2759 LLM-powered codebase analysis for AGENTS.md](https://github.com/Hmbown/CodeWhale/pull/2745) (Merged / Superseded)
by *punkcanyang* / *HUQIANTAO* — Replaces the template-based `/init` command with deep LLM project analysis. Gathers rich Rust context, then delegates generation to the agent. The follow-up [#2759](https://github.com/Hmbown/CodeWhale/pull/2759) patches credential leakage from git remotes and formatting.

### [#2753 Multi-tab system with cross-tab collaboration](https://github.com/Hmbown/CodeWhale/pull/2753) (Open)
by *ljm3790865* — Major community contribution. Introduces `TabManager` with per-tab chat history, session persistence across restarts, tab cycling (`Ctrl+\``, `Ctrl+Tab`), and cross-tab primitives for task delegation via mentions/`TaskDelegator`.

### [#2687 Project mode prompts per request](https://github.com/Hmbown/CodeWhale/pull/2687) (Open)
by *LeoAlex0* — Architectural refactor. Moves mode instructions, tool taxonomy, and approval policy from mutating `message[0]` into transient request-time runtime metadata. Aims to keep the base system prompt byte-stable.

### [#2631–#2635 Performance optimization series](https://github.com/Hmbown/CodeWhale/pull/2631) (Merged)
by *HUQIANTAO* — Systematic per-turn latency reduction: memoizes token estimation, caches tool catalog JSON serialization, collapses reverse message scans to a single pass, and caches history row calculations. Significantly reduces overhead on every turn.

### [#2623 Scroll support for plan prompt modal](https://github.com/Hmbown/CodeWhale/pull/2623) (Merged)
by *Implementist* — The `PlanPromptView` lacked scrolling, causing long plans to overflow the popup and clip bottom action options. Adds scrolling to prevent clipped off-screen content.

---

## 5. Feature Request Trends

**Extensibility & Interoperability:** A strong push to reduce platform lock-in. Users demand custom endpoints (search [#2767](https://github.com/Hmbown/CodeWhale/pull/2767), API providers [#2769](https://github.com/Hmbown/CodeWhale/pull/2769)), flexible MCP server configurations ([#2744](https://github.com/Hmbown/CodeWhale/issues/2744), [#2749](https://github.com/Hmbown/CodeWhale/issues/2749)), and even bridging into the Claude Code skill ecosystem ([#2743](https://github.com/Hmbown/CodeWhale/issues/2743)).

**Observability & Control:** Users increasingly want *in-band* telemetry. Requests for visible token budgets ([#2666](https://github.com/Hmbown/CodeWhale/issues/2666)), structured run traces ([#2752](https://github.com/Hmbown/CodeWhale/issues/2752)), and configurable notifications ([#2768](https://github.com/Hmbown/CodeWhale/pull/2768)) reflect a maturing user base running complex, long-lived agent tasks.

**Workspace-Aware Agents:** The shift from chat to agent is driving demand for deep project understanding. The LLM-powered init ([#2745](https://github.com/Hmbown/CodeWhale/pull/2745)), context-aware MCP merging ([#2749](https://github.com/Hmbown/CodeWhale/issues/2749)), and live branch/status refresh ([#2763](https://github.com/Hmbown/CodeWhale/pull/2763)) all point to a need for tools that understand the *codebase*, not just the *cursor*.

---

## 6. Developer Pain Points

**Session Reliability & Trust:** This remains the most acute pain point. Users report task freezes with no recovery path ([#2739](https://github.com/Hmbown/CodeWhale/issues/2739)), auth failures that lock the entire IDE ([#2754](https://github.com/Hmbown/CodeWhale/issues/2754)), and misleading UI states where deferred tools appear as completed runs ([#2648](https://github.com/Hmbown/CodeWhale/issues/2648)). Each incident directly erodes trust in the agentic core.

**Platform Fragmentation:** Windows requires specific CI patches and test-window widening to stay functional ([#2764](https://github.com/Hmbown/CodeWhale/pull/2764), [#2765](https://github.com/Hmbown/CodeWhale/pull/2765) via [#2528](https://github.com/Hmbown/CodeWhale/pull/2528)). Wayland users face silent clipboard failures on non-wlroots compositors ([#1920](https://github.com/Hmbown/CodeWhale/issues/1920)). Linux and Windows remain second-tier deployment targets.

**Configuration Rigidity:** Simple parsing decisions create cascading failures. The `split_once('_')` in MCP name parsing ([#2744](https://github.com/Hmbown/CodeWhale/issues/2744)) is a canonical example of a fragile implementation that breaks silently. Incorrect CLI hints ([#2758](https://github.com/Hmbown/CodeWhale/issues/2758)) and non-merging project configs ([#2749](https://github.com/Hmbown/CodeWhale/issues/2749)) add constant cognitive overhead.

**TUI Ergonomics:** Beyond the feature requests, bare usability issues like popups obscuring the main interface and difficulty copying output ([#2766](https://github.com/Hmbown/CodeWhale/issues/2766)) suggest the TUI’s information architecture has not kept pace with the feature set. The stabilization gate ([#2721](https://github.com/Hmbown/CodeWhale/issues/2721)) explicitly acknowledges that old correctness and usability bugs cannot ship under a larger feature release.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*