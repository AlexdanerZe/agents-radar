# AI CLI Tools Community Digest 2026-06-16

> Generated: 2026-06-16 03:44 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Ecosystem – 2026-06-16

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem has entered a high-stakes "stability vs. autonomy" phase. While the market has converged on a common architecture (MCP integration, sandboxed execution, multi-agent loops, extensible hooks), every major tool is simultaneously racing to ship autonomous background features while battling severe platform-specific reliability regressions—from macOS kernel panics (Codex, Claude) to Windows WSL path breakage (Codex, Copilot) and agentic loop hangs (Gemini, DeepSeek TUI). A clear bifurcation is emerging between platform-captive tools (Claude Code, OpenAI Codex, Copilot CLI) that leverage first-party model ecosystems, and independent/niche agents (Qwen Code, Gemini CLI, Pi, OpenCode, DeepSeek TUI, Kimi Code) competing on model flexibility, security controls, and targeted automation. The dominant competitive tension is that autonomous feature velocity is outpacing foundational reliability, creating an opening for disciplined engineering teams to differentiate on stability.

---

## 2. Activity Comparison

| Tool | Release Status (24h) | Digest-Highlighted Issues | Digest-Highlighted PRs | Community Stability Pulse |
|---|---|---|---|---|
| **Claude Code** | **Released** v2.1.178 | 10 | 10 | Moderate – ENOSPC false positives, VM leaks persist |
| **OpenAI Codex** | **Released** v0.140.0 | 10 | 10 | Critical – macOS `syspolicyd` runaway, WSL path regression |
| **Gemini CLI** | Static | 10 | 10 | Low – P1 agent hangs, shell completion stalling |
| **Copilot CLI** | **Released** v1.0.63 | 10 | 0 | Low – Regression whiplash (ARM panic, plugin breakage) |
| **Kimi Code CLI** | Static | 4 | 2 | Moderate – Targeted session/hooks fixes, small team |
| **OpenCode** | Static | 10 | 10 | Critical – Billing activation trust crisis, memory leaks |
| **Pi** | **Released** v0.79.4 | 10 | 10 | Moderate – Provider streaming gaps, SDK packaging flaw |
| **Qwen Code** | **Released** v0.18.1 | 10 | 10 | Strong – OOM fixes, proactive `/loop` roadmap execution |
| **DeepSeek TUI** | Static | 10 | 10 | Critical – YOLO mode "Turn stalled" blocking power users |

---

## 3. Shared Feature Directions

The following requirements are emerging as consensus demands across multiple tool communities:

| Demand Pattern | Manifesting In | Specific Needs Observed |
|---|---|---|
| **Persistent Memory & Shared State** | Claude, Gemini, OpenCode | Team Memory (#38536), Auto Memory reliability (#26522), Session Goals / context persistence (#27167) |
| **Autonomous Background Execution** | Qwen, DeepSeek, OpenCode, Claude | `/loop` automation (#5124), Goal Mode (#3096), `/goal` session objective command (#27167) |
| **Granular Security & Permission Policies** | Claude, Codex, Gemini, OpenCode, DeepSeek, Copilot | `Tool(param:value)` syntax (v2.1.178), seatbelt sandboxing (#2242), SSRF web fetch protection (#27739), typed persistent permission rules (#1186) |
| **MCP Lifecycle & Schema Stability** | Claude, Copilot, OpenCode, Qwen, Gemini | Unbounded server spawn prevention (#64366), schema string coercion fixes (#4966), resource download handling (#28466) |
| **Session Lifecycle Durability** | Kimi, Claude, OpenCode, DeepSeek | Reliable `--continue` (#2222), lifecycle hooks (#47023), archive/delete and session recovery (#32499) |
| **BYOK / Multi-Provider Flexibility** | Copilot, Pi, Qwen, OpenCode, DeepSeek | Multiple model support (#3282), provider registry refactoring (#3005), model picker disambiguation (#5173) |
| **Cross-Platform Parity** | Codex, Copilot, OpenCode, DeepSeek, Pi, Claude | WSL path rewriting (#28094), UTF-8 mojibake on Windows (#3776, #30869), Wayland browser agent crashes (#21983) |

---

## 4. Differentiation Analysis

- **Claude Code (Anthropic)** – The most permission-rich agent ecosystem with the new `Tool(param:value)` engine. Strategically tied to Anthropic model capabilities (Opus thinking blocks). Main vulnerability: Desktop VM resource governance and spurious filesystem errors eroding daily driver trust.

- **OpenAI Codex** – The most heavily productionized tool with Guardian safety system, app-server architecture, and built-in `/usage` analytics. Strong enterprise policy controls (`default_tools_approval_mode`). Vulnerable to macOS platform instability (`syspolicyd` runaway) and over-aggressive safety classifiers.

- **Gemini CLI (Google)** – Stands out for its security-first engineering culture (SSRF-focused patches, strict dependency pinning with 14-day cooldown). Deep Google Cloud enterprise integration (GDC air-gapped auth). Core agent loop reliability (hangs, misreported success) lags behind its safety commitment.

- **Copilot CLI (GitHub)** – Leverages deepest GitHub ecosystem integration. Struggling with `v1.0.6x` regression whiplash. The community demand for BYOK (#3282) directly challenges its captive model proposition. Enterprise OAuth scoping (#953) is a long-unmet governance need.

- **Kimi Code CLI (MoonshotAI)** – Targeted regional player. Small team executing focused bug fixes on core primitives (session resume, hook system). Emerging system proxy bug (#2455) is a critical blocker for enterprise network environments.

- **OpenCode** – Most ambitious MCP compliance story with active spec tracking (instructions, schema sanitization, resource downloads). Strongest community desire for agent sandboxing and session goals. Currently facing an existential trust crisis over billing activation failures (#32420, #32482) and memory stability (#20695).

- **Pi** – Unique agent ecosystem play via extensible DP extension API and aggressive provider proliferation (Amazon Bedrock Mantle, ZAI-CN). SDK architecture debt from Shrinkwrap module duplication (#5653) limits platform growth. Strong TUI UX focus but suffers rendering paper cuts.

- **Qwen Code – The most disciplined engineering roadmap tracked in this digest. Systematic rollout of autonomous `/loop` primitives (wakeup tool, task files, workflow phases). Proactive OOM crash fixes and model provider disambiguation. Strongest momentum in background automation and production stability.

- **DeepSeek TUI** – Technologically bold (i18n spanning 47 files, data-driven provider registry refactor eliminating 100+ match arms). The definitive "high autonomy" YOLO mode tool. Core stability issues ("Turn stalled" #2487, Windows UI freeze #1812) represent the highest risk of user exodus for power users.

---

## 5. Community Momentum & Maturity

**Mature Leaders (Sustaining Innovation, High Bug Burden)**
Claude Code and OpenAI Codex command the largest user bases and most complex feature surfaces. Their maturity is a double-edged sword: users tolerate bugs for capability, but data loss (Claude Desktop sessions wiped) and platform lockups (Codex macOS freezes) actively erode trust.

**Disciplined Fast Followers (Executing on Roadmaps)**
Qwen Code shows the strongest signal-to-noise ratio with systematic `/loop` execution, OOM fixes, and stable releases. Gemini CLI demonstrates rigorous process in security patches and infrastructure PRs, though agentic loop reliability remains a gap. Both are engineering-driven, not hype-driven.

**High-Risk, High-Reward (Ambitious Architecture, Volatile Base)**
DeepSeek TUI and OpenCode have the most fanatical user bases and the most ambitious technical goals (headless subagent runtime, full MCP compliance). However, their stability problems ("Turn stalled", billing trust crisis) are severe enough to cap growth unless immediately addressed.

**Incumbent Under Pressure**
Copilot CLI has the distribution advantage of GitHub but is hemorrhaging trust through the `v1.0.6x` regression cycle. ARM panic, broken plugins, and failed requests consuming AIC (#3814) make the current experience hard to defend.

**Platform / Niche Players**
Pi serves a loyal extension developer audience with its unique SDK approach. Kimi Code CLI serves a specific regional market. Both face scalability challenges but are stable within their current scope.

---

## 6. Trend Signals

**Autonomous Sessions are the New Product**
The competitive arena has shifted from "best response quality" to "longest reliable agent run". Session durability, context resumption, and background task management (Qwen `/loop`, OpenCode `/goal`, DeepSeek Goal Mode) are the defining features of 2026.

**The Safety Backlash is Real**
False positives (Codex blocking `git status`, Claude spurious ENOSPC, Kimi opaque "High Risk" compaction) are eroding user trust in automated systems. The market is demanding deterministic, user-controllable permission models (Claude `Tool(param:value)`, DeepSeek typed rules) over black-box classifiers.

**MCP is Infrastructure, Not a Feature**
Standardizing on MCP is table stakes; the quality of integration is the differentiator. Unbounded process spawning (#64366), schema incompatibilities (#4966), SSRF bypasses (#27739), and missing resource/prompt capabilities create systemic reliability gaps that require dedicated engineering investment.

**BYOK is the Escape Hatch from Ecosystem Lock-In**
The demand for multi-model support (Copilot #3282), provider registries (DeepSeek #3005), and fallback chains (Pi #4945) signals strong market rejection of single-model captivity. Users want to route their tool to the best model for the task, not be locked into a single vendor's ecosystem.

**Cross-Platform Parity is an Urgent Gap**
Every digest highlights painful non-macOS regressions. Hardcoded UTF-8 assumptions (OpenCode, Copilot), WSL path rewriting (Codex), Wayland browser agent crashes (DeepSeek, Gemini), and ARM64 panics (Copilot) reveal systemic under-investment in cross-platform testing. Tools that continue treating non-macOS platforms as secondary will bleed market share.

**Observability Becomes Non-Negotiable**
As agents run longer and consume more tokens, visibility into usage (Codex `/usage`), cost (Qwen `/stats`), and performance (OpenCode tokens/second request) is becoming critical for the professional developer segment. Tools that fail to provide this will lose the power user demographic.

**The "Second System" Effect is Biting**
Tools are adding complex features (loops, MCP, security rules, skills) on unstable foundations. DeepSeek TUI's YOLO mode, Claude's Desktop VM leaks, and Gemini's agent hangs all suggest a "move fast and break everything" pace that is hitting a wall as systems grow complex. The next competitive advantage is disciplined, reliable engineering—not feature count.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the data from the `anthropics/skills` repository.

---

### 1. Top Skills Ranking

The following Pull Requests represent the most actively discussed new Skill submissions, ranked by community comment activity:

**#514: [Document Typography Skill](https://github.com/anthropics/skills/issues/514)** *(Open)*
- **Functionality:** A quality-control skill that prevents common AI-generated document flaws, including orphan/widow text, misaligned numbering, and stranded section headers.
- **Discussion Highlights:** High community consensus around a universal pain point in generated documents. The proposal is praised for addressing a problem every user encounters but rarely requests directly.
- **Status:** Open, with ongoing refinement.

**#486: [ODT Skill](https://github.com/anthropics/skills/issues/486)** *(Open)*
- **Functionality:** Comprehensive support for the OpenDocument Format (.odt, .ods) including creation, template filling, and conversion to HTML.
- **Discussion Highlights:** Strong demand from enterprise and public-sector users who rely on LibreOffice. The discussion focuses heavily on the need for ISO-standard document interoperability beyond Microsoft formats.
- **Status:** Open.

**#1140: [Agent Creator & Multi-Tool Eval Fix](https://github.com/anthropics/skills/issues/1140)** *(Open)*
- **Functionality:** A meta-skill for composing task-specific agent sets from the existing library, bundled with critical fixes for parallel tool-call evaluation and Windows path handling.
- **Discussion Highlights:** Represents the community’s growing interest in *orchestration and composition* over single-skill usage. The evaluation fix is treated as a blocker for reliable agent workflows.
- **Status:** Open.

**#444: [AURELION Skill Suite](https://github.com/anthropics/skills/issues/444)** *(Open)*
- **Functionality:** A four-skill suite (Kernel, Advisor, Agent, Memory) implementing a structured 5-floor cognitive framework for professional knowledge management and AI collaboration.
- **Discussion Highlights:** Signals maturing architectural ambition in the ecosystem. The conversation explores how multi-skill frameworks can manage complex, stateful reasoning tasks.
- **Status:** Open.

**#83: [Skill Quality & Security Analyzers](https://github.com/anthropics/skills/issues/83)** *(Open)*
- **Functionality:** Meta-skills that evaluate other Skills across five quality dimensions (Structure, Documentation, Security, Robustness, Actionability).
- **Discussion Highlights:** The community is proactively demanding governance tooling. This PR is central to conversations about setting quality gates for the rapidly expanding marketplace.
- **Status:** Open.

**#181: [SAP-RPT-1-OSS Predictor Skill](https://github.com/anthropics/skills/issues/181)** *(Open)*
- **Functionality:** Integrates SAP’s open-source tabular foundation model for predictive analytics directly into Claude Code workflows.
- **Discussion Highlights:** Niche but intensely engaged audience of enterprise SAP developers. Demonstrates demand for domain-specific ML models to be callable as Skills.
- **Status:** Open.

**#210: [Frontend Design Skill Clarity Revamp](https://github.com/anthropics/skills/issues/210)** *(Open)*
- **Functionality:** A comprehensive revision of the existing frontend-design skill to improve instruction actionability and internal coherence.
- **Discussion Highlights:** Represents a shift from "what can a Skill do" to "how should a well-written Skill behave." The community is actively debating quality standards for skill authoring.
- **Status:** Open.

---

### 2. Community Demand Trends

Analysis of the most commented-on Issues reveals three dominant demand vectors:

- **Development Pipeline Reliability (Critical Mass):** Issues **#556** and **#1169** describe a catastrophic bug in `run_eval.py` where recall is stuck at 0%, making the optimization loop unusable. Issues **#1061** and **#1099** highlight persistent cross-platform failures (Windows encoding, subprocess pipes). The community’s single loudest demand is "make the skill-authoring tools work reliably everywhere."

- **Enterprise Infrastructure & Governance:** Issue **#228** (Org-wide skill sharing) and Issue **#492** (Security/trust boundary abuse) show a clear demand for administrative control, distribution channels, and authorship verification. Issue **#1175** raises security concerns around enterprise data handling within skills. The ecosystem is outgrowing its single-user origins.

- **Standardization & Interoperability:** Issue **#16** (Expose Skills as MCPs) and Issue **#1220** (Multi-file preload for skill references) reflect a desire for Skills to integrate cleanly with external tools and work as composable, modular units.

---

### 3. High-Potential Pending Skills

These open PRs have active discussion and address clear gaps, making them strong candidates for near-term landing:

- **#514: Document Typography** — Solves a universal quality flaw in generated documents.
- **#486: ODT Skill** — Covers the crucial LibreOffice/OpenDocument interoperability gap.
- **#723: [Testing Patterns Skill](https://github.com/anthropics/skills/issues/723)** — A comprehensive testing stack skill (Unit, React, E2E) highly requested by engineering teams.
- **#147: [Codebase Inventory Audit](https://github.com/anthropics/skills/issues/147)** — Systematically identifies orphaned code, unused files, and documentation gaps.
- **#154: [Shodh-Memory Skill](https://github.com/anthropics/skills/issues/154)** — Provides persistent, cross-conversation memory for AI agents.
- **#1140: Agent Creator Skill** — Enables dynamic, task-specific agent composition as a meta-skill.

---

### 4. Skills Ecosystem Insight

**The community’s most concentrated demand is a dual-track evolution: urgently stabilizing the cross-platform skill development pipeline (fixing evaluation reliability and Windows parity) while simultaneously authoring deeply specialized, enterprise-grade skills (ODT, SAP, Agent Orchestration, Typography) to transform Claude Code from a generalist assistant into a production-ready, domain-optimized platform.**

---

Here is the Claude Code community digest for June 16, 2026, synthesized from the latest GitHub activity.

---

# Claude Code Community Digest — 2026-06-16

### 1. Today’s Highlights

v2.1.178 ships with a highly anticipated `Tool(param:value)` syntax for permission rules and fixes for nested skill discovery. The community is actively wrestling with stability issues, however—especially a rash of spurious macOS ENOSPC errors and critical resource leaks in the Desktop app. A single prolific contributor (`AZERDSQ131`) has been particularly active, contributing a sweeping set of fixes across plugin infrastructure, Windows compatibility, and workflow automation.

### 2. Releases

**Latest:** `v2.1.178`

- **`Tool(param:value)` Permission Syntax:** Rules can now match specific tool parameters using wildcards, e.g., `Agent(model:opus)` to block expensive subagents. This gives power users much finer control over agent orchestration without blanket deny rules.
- **Nested Skills Loading:** Skills in nested `.claude/skills` directories now load correctly when working on files in those subtrees. Naming conflicts resolve in favor of the most deeply nested skill.

### 3. Hot Issues

1. **[#24726](https://github.com/anthropics/claude-code/issues/24726) – VS Code: Setting to disable auto-attach of open file/selection.** The most voted open issue (`👍 163`). Developers want explicit opt-in for context rather than automatic file attachment. A clear sign the current context injection model frustrates power users.

2. **[#64366](https://github.com/anthropics/claude-code/issues/64366) – Unbounded MCP server fan-out causing kernel panics.** Cowork and Agent sessions spawn MCP servers that are never reclaimed. Results in RAM exhaustion and kernel panics (M2 Max / 32 GB). Highlights a severe lifecycle management hole in the agent runtime.

3. **[#29045](https://github.com/anthropics/claude-code/issues/29045) – Desktop app spawns 1.8 GB Hyper-V VM for chat-only use.** Users are confused by the heavy overhead for simple interactions. Strong sentiment that this should be lazy-loaded or deferred.

4. **[#48334](https://github.com/anthropics/claude-code/issues/48334) – Desktop update deletes session history.** A high-severity data loss bug: `sessions-index.json` and `.jsonl` files are wiped during upgrades. Erodes user trust in the Desktop app’s persistence layer.

5. **[#63909](https://github.com/anthropics/claude-code/issues/63909) / [#65166](https://github.com/anthropics/claude-code/issues/65166) – Spurious macOS ENOSPC “temp filesystem full” errors.** The single largest bug cluster. A false positive in disk space checking (`statfs().bsize=0` on x86_64) causes the Bash tool to abort commands. Extremely disruptive to daily workflows.

6. **[#47023](https://github.com/anthropics/claude-code/issues/47023) – Expose compact/session lifecycle hooks for external memory.** A well-scoped proposal backed by 22 comments. The community is building custom memory layers and desperately needs official hook points for transcript access and compaction interception.

7. **[#50267](https://github.com/anthropics/claude-code/issues/50267) – Subagents can’t write to `permissions.allow` paths (regression 2.1.114).** Blocks agentic workflows. Subagents performing file I/O are denied even when the parent session has explicitly allowed the paths.

8. **[#63358](https://github.com/anthropics/claude-code/issues/63358) – Opus 4.8 returns empty thinking blocks.** Extended thinking for the flagship model is broken (empty `thinking` field). Blocks thinking-dependent workflows and mirrors a prior regression in Opus 4.7.

9. **[#38536](https://github.com/anthropics/claude-code/issues/38536) – Feature Request: Shared Team Memory.** High-value enterprise signal. The current individual-only memory model is a bottleneck for team handoffs and collaborative investigations.

10. **[#65577](https://github.com/anthropics/claude-code/issues/65577) – Desktop VM disk grows unboundedly.** The `rootfs.img` for the local microVM sandbox is never reclaimed, silently filling the disk. Pairs with #64366 to paint a concerning picture of Desktop resource governance.

### 4. Key PR Progress

A massive cleanup wave landed over the past 24 hours, mostly from a single contributor tackling long-standing tech debt.

1. **[#68678](https://github.com/anthropics/claude-code/pull/68678) – Fix triage bot marking Desktop issues as invalid.** Corrects `triage-issue.md` which was incorrectly filtering out Claude Desktop bug reports from the main repo.

2. **[#68707](https://github.com/anthropics/claude-code/pull/68707) – Add `/bug` command for in-terminal issue filing.** A new plugin that lets users file structured GitHub bug reports without leaving the terminal, auto-collecting environment info.

3. **[#68699](https://github.com/anthropics/claude-code/pull/68699) – Fix Hookify on Windows (Python wrapper + path normalization).** Prevents silent hook failures on Windows by wrapping Python calls and normalizing `CLAUDE_PLUGIN_ROOT` backslashes for bash.

4. **[#68700](https://github.com/anthropics/claude-code/pull/68700) – Fix plugin execution path normalization for Windows.** Ensures plugin hooks can execute scripts with properly formed paths on Windows.

5. **[#68672](https://github.com/anthropics/claude-code/pull/68672) – Fix Hookify rule loading for unknown tools.** Corrects a bug where `event` remained `None` for unhandled tools. Now correctly loads `event:all` rules as a fallback.

6. **[#68671](https://github.com/anthropics/claude-code/pull/68671) – Fix PostToolUse permission decision.** Allows PostToolUse hooks to properly return `permissionDecision: "deny"`, which was previously ignored.

7. **[#68689](https://github.com/anthropics/claude-code/pull/68689) – Block symlink escape in security-guidance config reads.** Security hardening: prevents malicious symlinks from hijacking `.claude/security-patterns.yaml` reads.

8. **[#68681](https://github.com/anthropics/claude-code/pull/68681) – Fix workflow pagination break conditions.** Critical fix for `lock-closed-issues.yml` where pagination stopped prematurely (checking `length === 0` instead of `length < 100`).

9. **[#68693](https://github.com/anthropics/claude-code/pull/68693) – Fix additive duplicate label assignment.** Prevents the `closeIssueAsDuplicate()` function from overwriting existing issue labels when applying the `duplicate` label.

10. **[#68679](https://github.com/anthropics/claude-code/pull/68679) – Fix ralph-wiggum promise detection against control characters.** Fixes the Ralph loop stop hook misinterpreting terminal escape sequences, ensuring `<promise>` tokens are correctly detected in transcripts.

### 5. Feature Request Trends

- **Persistent & Shared Memory:** The strongest product signal. Users are hitting hard limits with the current stateless, single-user memory model. Requests span lifecycle hooks (`#47023`), shared team memory (`#38536`), and structured memory layers.
- **Context Management Precision:** Developers want surgical control over context injection. The top-voted issue is for a VS Code auto-attach toggle (`#24726`), closely followed by requests for incremental multi-selection (`#33058`).
- **Permission System Evolution:** The new `Tool(param:value)` release directly answers demand for fine-grained agent orchestration. The community is already experimenting with blocking expensive models in subagents and parameterized rule matching.
- **Desktop Session Lifecycle:** Users are requesting archive/delete functionality (`#65615`) alongside fixes for sidebar state, indicating a need for mature session management.

### 6. Developer Pain Points

- **Spurious macOS ENOSPC:** The top friction point. False positive “disk full” errors break subprocess execution unpredictably across multiple Apple Silicon and Intel configurations. Duplicate reports keep surfacing, suggesting the fix is non-trivial.
- **Desktop App Reliability:** A cluster of critical bugs—kernel panics (#64366), data loss on updates (#48334), and unbounded VM disk growth (#65577)—are actively eroding trust in the Desktop application as a stable daily driver.
- **Plugin Development Fragility:** The wave of PRs fixing Windows path separators, shell edge cases, and rule engine bugs suggests the plugin SDK has significant platform quality gaps and needs hardened testing.
- **Agent Loop Instability:** Building agentic systems involves systemic friction: subagent permission regressions (`#50267`), premature loop termination (`#68735`), tool call parsing failures (`#64235`), and model-level thinking block regressions (`#63358`) create a fragmented experience for power users.
- **API / Model Regression Churn:** Frequent regressions in model selection parsing, API error codes, and thinking block rendering indicate the integration layer lacks sufficient regression test coverage against the broader Anthropic API surface.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-16

**Analysis by OpenAI Developer Tools Team**

---

## 1. Today's Highlights

OpenAI shipped **Codex CLI `v0.140.0`** with long-requested `/usage` analytics and `/goal` enhancements for oversized text and image attachments. The community conversation, however, is dominated by **platform stability regressions** (macOS `syspolicyd` runaway, Windows launch crashes) and a cluster of **false-positive cybersecurity flags** blocking everyday developer workflows. On the engineering front, PRs advancing the sandbox credential broker, plugin recommendation caching, and Guardian retry logic signal a strong push toward production hardening.

---

## 2. Releases

### [rust-v0.140.0](https://github.com/openai/codex/releases/tag/rust-v0.140.0)
*Stable channel release*

- **`/usage` views**: new commands for daily, weekly, and cumulative account-level token activity tracking. (#27925)
- **`/goal` enhancements**: now preserves oversized text, large pasted blocks, and image attachments, including across remote app-server sessions. (#27508, #27509, #27510)
- **Permanent session deletion**: full support for hard-deleting sessions through the app-server API.

### Alpha Channel
`rust-v0.140.0-alpha.{20,21,22}` and `rust-v0.141.0-alpha.{1,2}` published in the last 24 hours. No changelog details provided for these builds.

---

## 3. Hot Issues

*10 noteworthy items selected from the top 30 by comment activity.*

### 1. [#11023](https://github.com/openai/codex/issues/11023) — Linux Desktop App *(Enhancement / App)*
- **Comments:** 113 | **👍:** 583
- **Why it matters:** The single highest-demand feature on the board. A native Linux desktop client is strongly requested, driven partly by critical macOS performance issues (#10432) that make the current app “almost unusable” on Mac hardware for some users.

### 2. [#25719](https://github.com/openai/codex/issues/25719) — macOS `syspolicyd` / `trustd` CPU & Memory Runaway *(Bug / Performance)*
- **Comments:** 26 | **👍:** 33
- **Why it matters:** Codex Desktop repeatedly triggers system security daemons into uncontrolled CPU and memory consumption, effectively freezing the user’s machine. Represents a **top-priority stability blocker** for macOS power users.

### 3. [#28015](https://github.com/openai/codex/issues/28015) — False-Positive Cybersecurity Check Blocking Local Repo Maintenance *(Bug / CLI / Safety)*
- **Comments:** 18 | **👍:** 0
- **Why it matters:** Normal DevOps tasks (checking git status, running local hygiene commands) are being flagged as cybersecurity risks, interrupting paid sessions. Duplicates the pattern from [#27817](https://github.com/openai/codex/issues/27817) (finance/tax work flagged), indicating a systemic over-sensitivity in the safety classifier.

### 4. [#28094](https://github.com/openai/codex/issues/28094) — WSL Path Rewriting `/home` → `C:\home` *(Bug / Windows / Session)*
- **Comments:** 13 | **👍:** 1
- **Why it matters:** The Desktop App rewrites Linux `/home/project` paths to `C:\home\project`, breaking project–chat associations and reporting valid WSL directories as missing. A severe regression for the Windows + WSL development workflow.

### 5. [#21527](https://github.com/openai/codex/issues/21527) — General Slowness *(Bug / Performance)*
- **Comments:** 32 | **👍:** 17
- **Why it matters:** A broad, high-signal complaint: “Codex is really too slow, whether it's the VS Code plugin or the Codex app.” Captures latent frustration with model response latency across the entire product surface.

### 6. [#12661](https://github.com/openai/codex/issues/12661) — `file://` Links Open in Edge Instead of VS Code *(Bug / Windows / Extension)*
- **Comments:** 47 | **👍:** 43
- **Why it matters:** A strict DX regression on Windows. Markdown responses containing local file links (`file:///C:/...`) redirect to the system browser instead of the VS Code editor, breaking a core developer reference workflow.

### 7. [#27331](https://github.com/openai/codex/issues/27331) — `multi_agent_v2` Flag Breaks Every Turn *(Bug / Regression / Config)*
- **Comments:** 4 | **👍:** 5
- **Why it matters:** Enabling `features.multi_agent_v2` in `config.toml` causes every API turn to fail with an encrypted-tools 400 error before the model even executes. A complete functional regression for early feature testers.

### 8. [#28442](https://github.com/openai/codex/issues/28442) — Windows Desktop Crash on Launch *(Bug / Windows / App)*
- **Comments:** 2 | **👍:** 0
- **Why it matters:** Version `26.609.9530.0` fails to open any window after launch. The app becomes completely unavailable for affected Windows users, requiring a rollback to `26.602.9276.0`.

### 9. [#28190](https://github.com/openai/codex/issues/28190) — `rg` (ripgrep) Blocked by macOS *(Bug / CLI / Sandbox)*
- **Comments:** 9 | **👍:** 8
- **Why it matters:** The system sandbox is blocking the `rg` binary, preventing the CLI agent from performing file searches. Highlights frictions in the sandbox tooling whitelist for common developer utilities.

### 10. [#3355](https://github.com/openai/codex/issues/3355) — Connection Break After MacBook Sleep *(Bug / Connectivity)*
- **Comments:** 37 | **👍:** 19
- **Why it matters:** Long-running tasks disconnect when the laptop lid closes without a graceful session resume path. A persistent workflow-breaking behavior for mobile developers.

---

## 4. Key PR Progress

*10 impactful pull requests updated in the last 24 hours.*

### 1. [#28396](https://github.com/openai/codex/pull/28396) — Record External Agent Import Results
*Status: Open | Author: charlesgong-openai*
Persists completed external-agent config import results in the state DB, including granular success/failure details for config, AGENTS.md, and skill files. Foundational for reliable plugin and agent import auditing.

### 2. [#28307](https://github.com/openai/codex/pull/28307) — Queue TUI Follow-Ups Through App-Server
*Status: Open | Author: efrazer-oai*
Adds durable queuing for TUI follow-ups via the app-server. Prevents message loss on client crash and is the proof-of-concept for the User Message Queue feature.

### 3. [#28399](https://github.com/openai/codex/pull/28399) — Add Recommended Plugin Endpoint Cache [1/3]
*Status: Open | Author: adaley-openai*
Authenticated caching for `/ps/plugins/suggested?scope=GLOBAL`. Deduplicates concurrent cache misses and warms recommendations by backend/account identity. Reduces cold-start latency for plugin discovery.

### 4. [#27965](https://github.com/openai/codex/pull/27965) — Support `default_tools_approval_mode`
*Status: Open | Author: zamoshchin-openai*
Exposes `default_tools_approval_mode` in `[apps._default]` config. Applies after managed/per-tool settings and before the built-in `auto` fallback. Essential for enterprise policy controls.

### 5. [#27704](https://github.com/openai/codex/pull/27704) — Activate Endpoint Plugin Recommendations [3/3]
*Status: Open | Author: adaley-openai*
Final integration: snapshots and filters endpoint candidates per turn, resolving first-turn cache races and enforcing exact install validation. Closes the plugin recommendation pipeline.

### 6. [#28163](https://github.com/openai/codex/pull/28163) — Use Local Environment for User Shell Commands
*Status: Open | Author: pakrym-oai*
Fixes shell commands to use the correct selected turn environment instead of the legacy session cwd. Critical for multi-device remote setups where a remote environment lacks local escape paths.

### 7. [#28034](https://github.com/openai/codex/pull/28034) — Add Local Credential Broker
*Status: Open | Author: winston-openai*
Introduces a credential broker behind `features.network_proxy`. Keeps real GitHub/OpenAI credentials out of child-process tokens, injecting them only at the MITM proxy layer. A significant sandbox hardening improvement.

### 8. [#27982](https://github.com/openai/codex/pull/27982) — Start Guardian Child Session at Parent Start
*Status: Open | Author: jgershen-oai*
Pre-warms the Guardian child session during parent initialization instead of creating it on-demand for the first auto-review. Reduces latency for the initial safety check at session start.

### 9. [#28429](https://github.com/openai/codex/pull/28429) — Add Interruptible Sleep Tool
*Status: Open | Author: pakrym-oai*
A built-in `sleep` tool behind the `sleep_tool` feature flag. Allows models to pause for external work without blocking a shell process, resuming gracefully when new turn input arrives. A smart primitive for autonomous agent loops.

### 10. [#26334](https://github.com/openai/codex/pull/26334) — Retry Transient Guardian Reviewer Failures *(CLOSED)*
*Status: Merged | Author: viyatb-oai*
Transient failures (timeouts, rate limits, transport errors) in Guardian reviews are now retried instead of being treated as hard denials. Prevents infrastructure blips from blocking operations, a critical safety-system reliability fix.

---

## 5. Feature Request Trends

*Directions emerging from the cumulative issue signal.*

- **Linux Desktop Client (#11023):** Unquestionably the top community feature request by reaction count (583 👍). Developers explicitly cite macOS performance issues and power management concerns as drivers for needing a native Linux app.
- **Performance Optimization (Multiple Issues):** Underpinning many top issues is a demand for lower model response latency, reduced CPU/memory footprint (especially on macOS), and faster WSL-agent round trips. Users want a lighter, faster runtime across all platforms.
- **Platform Parity (Windows + WSL):** Issues around WSL path mapping (#28094), Windows sandbox elevation (#28107), and missing Computer Use support (#28435) indicate a strong and vocal Windows power-user base feeling friction relative to the macOS experience.
- **Sandbox & Policy Refinements:** Users are requesting finer-grained control over safety classifiers and tool approval modes. The false-positive theme (#27817, #28015) is driving a need for context-aware, per-tool permission policies rather than broad content flags.
- **Session Lifecycle Flexibility:** Requests for predictable session resume (`/goal` visibility, #28263), working archive deletion (#28095), and graceful sleep recovery (#3355) show developers expect the agent to handle long-lived, interrupted workflows reliably.

---

## 6. Developer Pain Points

*Recurring frustrations observed across the top issues.*

- **Over-aggressive Cybersecurity Classifiers:** The most acute friction. Standard workflows (git maintenance, API calls, tax preparation) are falsely flagged, interrupting sessions and breaking autonomous agent trust. The pattern is broad enough to be a top stability/safety experience concern.
- **macOS Resource Exhaustion:** The `syspolicyd`/`trustd` runaway bug (#25719, #28071) makes the Desktop App a system-wide risk on macOS. Combined with sleep-disconnect (#3355), the experience feels unstable for mobile/laptop developers.
- **Windows WSL Integration Instability:** Basic path mapping failures (#28094), helper executable regressions (#27125), and persistent elevation bugs (#28107) make the WSL agent environment feel like a second-class integration, despite being a core developer setup.
- **General Platform Performance:** Across App, Extension, and CLI, the consistent signal is "too slow" (#21527, #27240). High latency per turn and UI sluggishness are eroding daily development velocity.
- **Feature-Gate Regressions:** The `multi_agent_v2` issue (#27331) breaking all API calls highlights the danger of config-flag experiments leaking into production reliability. Users expect feature flags to be safe to toggle.
- **Session Lifecycle Unpredictability:** Sessions disappearing from resume (#28263), archive deletion failing silently (#28095), and misleading credit limits (#23258) create an inconsistent session-management experience that undermines developer trust in state durability.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-16

## 1. Today's Highlights
Security hardening dominated yesterday's PR activity, with multiple patches landed to block SSRF vectors in the web-fetch tool and MCP OAuth metadata discovery. On the reliability front, several P1 bugs around agent hangs and subagent turn misreporting continue to attract community attention, while the project took a significant engineering hygiene step by introducing strict dependency pinning with a 14-day update cooldown. No new releases were published in the last 24 hours.

## 2. Releases
No new releases. The latest stable release remains unchanged.

---

## 3. Hot Issues

1. **Generalist agent hangs** — `#21409` (P1, 8 👍, 7 comments)
   The CLI freezes indefinitely when deferring to the generalist subagent, even for trivial tasks like folder creation. Users report workarounds (disabling sub-agents), but this remains a critical reliability blocker.
   [Issue #21409](google-gemini/gemini-cli Issue #21409)

2. **Subagent misreports MAX_TURNS as success** — `#22323` (P1, 2 👍, 6 comments)
   A logical bug where `codebase_investigator` hits its turn limit but reports `status: "GOAL"`. This erodes trust in agentic task completion and has high severity due to the silent failure mode.
   [Issue #22323](google-gemini/gemini-cli Issue #22323)

3. **Shell command hangs after completion** — `#25166` (P1, 3 👍, 4 comments)
   Executed CLI commands remain in "Awaiting user input" state despite having finished. A top-priority UX regression in the core execution loop.
   [Issue #25166](google-gemini/gemini-cli Issue #25166)

4. **Robust component-level evaluations** — `#24353` (EPIC, P1)
   An EPIC tracking the expansion of behavioral eval infrastructure from 76 tests to a comprehensive framework covering 6 Gemini models. Signals a major QA maturation push.
   [Issue #24353](google-gemini/gemini-cli Issue #24353)

5. **Model ignores custom skills and sub-agents** — `#21968` (P2, 6 comments)
   Users report the agent fails to autonomously leverage user-defined skills and sub-agents despite relevant descriptions. Declared effective only under explicit instruction, undermining the core value proposition of customization.
   [Issue #21968](google-gemini/gemini-cli Issue #21968)

6. **400 error with >128 tools** — `#24246` (P2, 3 comments)
   A hard scaling limit: when too many tools are enabled, the API returns a 400 error. Users want smarter tool scoping to avoid this ceiling.
   [Issue #24246](google-gemini/gemini-cli Issue #24246)

7. **Auto Memory bug cluster** — `#26522` / `#26525` / `#26523` (P2, 5/5/3 comments)
   A cluster of issues around the Auto Memory feature: infinite retrying of low-signal sessions, pre-redaction secret logging, and silent skipping of invalid `.patch` files. Suggests the feature needs a focused reliability pass.
   [Issue #26522](google-gemini/gemini-cli Issue #26522) | [#26525](google-gemini/gemini-cli Issue #26525) | [#26523](google-gemini/gemini-cli Issue #26523)

8. **Browser agent fails on Wayland** — `#21983` (P1, 1 👍, 4 comments)
   The browser subagent crashes on Wayland display servers, blocking Linux users on modern compositors from using a core agent capability.
   [Issue #21983](google-gemini/gemini-cli Issue #21983)

9. **Agent should discourage destructive behaviors** — `#22672` (P2, 1 👍, 3 comments)
   The model's tendency to use `git reset --force` or `--force` flags when safer alternatives exist raises safety concerns for production environments.
   [Issue #22672](google-gemini/gemini-cli Issue #22672)

10. **Symlinks not recognized as agents** — `#20079` (P2, 4 comments)
    Symlinked `.md` files in `~/.gemini/agents/` are silently ignored. A straightforward filesystem compatibility gap.
    [Issue #20079](google-gemini/gemini-cli Issue #20079)

---

## 4. Key PR Progress

1. **SSRF protection for web fetch (DNS + redirects)** — `#27739` / `#27744` (OPEN)
   Two complementary PRs fixing private IP bypasses in `isBlockedHost` via wildcard DNS services and redirect resolution. Critical security hardening.
   [PR #27739](google-gemini/gemini-cli PR #27739) | [PR #27744](google-gemini/gemini-cli PR #27744)

2. **Block private OAuth metadata URLs** — `#27626` (CLOSED, P2)
   Prevents SSRF via MCP server OAuth discovery by validating metadata URLs against private IP ranges before fetching.
   [PR #27626](google-gemini/gemini-cli PR #27626)

3. **Consolidated MCP server lists** — `#27605` (CLOSED)
   Fixes a policy bypass where workspace-scoped MCP allow/block lists could override user/system settings. Now correctly unions excluded lists and intersects allowed lists across scopes.
   [PR #27605](google-gemini/gemini-cli PR #27605)

4. **Platform-aware shell guidance** — `#27603` (CLOSED)
   Windows UX improvement: the operational prompt now includes `win32`-specific inspection commands instead of Unix-only examples.
   [PR #27603](google-gemini/gemini-cli PR #27603)

5. **Fix pending tools and trust overrides** — `#27854` (CLOSED)
   Prevents premature state progression while awaiting user tool approvals and forces sequential file writes to eliminate race conditions in the agent loop.
   [PR #27854](google-gemini/gemini-cli PR #27854)

6. **Path resolution for @-reference files** — `#27943` (OPEN)
   Fixes a "File not found" error when the model tries to read files originally referenced via the CLI's `@` mention syntax.
   [PR #27943](google-gemini/gemini-cli PR #27943)

7. **Top-level `/reload` command** — `#24478` (CLOSED)
   Consolidates all reload subcommands into a single `/reload` action, re-syncing agents, skills, MCP servers, memory, and settings.
   [PR #24478](google-gemini/gemini-cli PR #24478)

8. **Pin dependencies + 14-day update cooldown** — `#27948` (OPEN)
   A major dependency management policy change: strips all `^`/`~` ranges and enforces a cooldown on automated updates to prevent churn-induced breakage.
   [PR #27948](google-gemini/gemini-cli PR #27948)

9. **Fix nightly release workflow** — `#27939` (CLOSED, P1)
   Nightly releases were stalling because scheduled cron runs defaulted to the `prod` environment requiring manual approval. Now uses an unprotected environment.
   [PR #27939](google-gemini/gemini-cli PR #27939)

10. **GDC air-gapped service identity** — `#27956` (OPEN)
    Adds support for token exchange in air-gapped environments following an upstream `google-auth-library` update. Expands enterprise deployment scenarios.
    [PR #27956](google-gemini/gemini-cli PR #27956)

---

## 5. Feature Request Trends

- **AST-Aware Code Intelligence**: Epics `#22745`, `#22746`, and `#22747` explore using AST-aware tools (e.g., `tilth`, `glyph`, AST grep) for file reads, search, and codebase mapping. The goal is to reduce turns from misaligned reads and lower noise in tokens — a strong vote for semantic over lexical tooling.

- **Autonomous Skill Utilization**: Issues like `#21968` and `#21432` both highlight a desire for the agent to natively understand and leverage its own capabilities (skills, sub-agents, hotkeys, flags) without explicit user prompting. The emphasis is on *autonomous self-awareness*.

- **Remote & Background Operations**: Epic `#20303` (Remote Agents Sprint 2) drives toward task-level auth, 1P agent support, and background processing — enabling unattended, long-running agent workflows.

- **Evaluation Infrastructure**: `#24353` and `#23166` show strong internal investment in making component-level and project-level evaluations reliable, non-flaky, and actionable. A bottom-up push for engineering rigor.

---

## 6. Developer Pain Points

- **Agent Unreliability**: The top recurring frustration. Issues like generalist agent hangs (`#21409`), shell command stalling (`#25166`), false success reports (`#22323`), and ignored settings (`#22267`, `#22093`) undermine confidence in autonomous mode.

- **Memory System Friction**: The Auto Memory feature cluster (`#26516`, `#26522`, `#26523`, `#26525`) reveals multiple pain points: secret exposure risk, infinite retries on low-signal data, and silent failure on malformed patches. Users need a trustworthy, auditable memory subsystem.

- **Filesystem Tooling Bugs**: Small but frequent sharp edges: symlinks not recognized (`#20079`), temp file littering (`#23571`), `\n` escape misbehavior (`#22466`), parallel write conflicts (`#24429` PR), and broken `@`-reference resolution (`#27943` PR).

- **Security & Safety Anxiety**: The SSRF patches (`#27739`, `#27744`, `#27626`) and requests for destructive command prevention (`#22672`) indicate users are actively concerned about the blast radius of agentic actions.

- **Platform Compatibility**: Wayland (`#21983`), tmux (`#27572`), and terminal corruption after external editors (`#24935`) point to gaps in cross-platform testing that directly impact daily workflows on Linux and inside terminal multiplexers.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – June 16, 2026**

---

## 1. Today's Highlights
The team shipped **v1.0.63** to address recent regressions and improve provider reliability. A new `deferTools` option for MCP server configuration gives developers finer control over tool availability. Despite the patch, the community is still navigating fallout from v1.0.60 and v1.0.61, including a critical ARM64 panic and persistent cross-platform encoding bugs. Interest remains high in multi-model BYOK support and richer session management features.

---

## 2. Releases
- **v1.0.63 / v1.0.63-0** (June 15)
  - **Image Handling:** Blocked image attachments now surface clear guidance on enabling vision or switching models, replacing the previous cryptic 400 error (directly addresses Issue #3781).
  - **MCP Configuration:** Added a `deferTools` option to MCP server config, keeping a server’s tools available even when agentic tool search is enabled.
  - **Provider Reliability:** Improved request reliability for OpenAI, Anthropic, and Azure OpenAI endpoints.
  - **UX:** `--help` options are now alphabetized. Pressing `w` in `/diff` toggles whitespace-only changes.
  - **Experimental:** Improved `/rewind` behavior.

---

## 3. Hot Issues (Top 10 Noteworthy)
1. **#953 – Granular OAuth Scopes (Enterprise)**
   Long-standing demand to scope authentication to specific repos instead of blanket read/write access. The single permission model is a barrier for organizational adoption.
   [Issue #953](https://github.com/github/copilot-cli/issues/953) | 7 comments | 👍 3

2. **#3727 – Plugin Hook Regression in v1.0.60**
   The `userPromptSubmitted` hook’s `additionalContext` payload no longer reaches the planner. Plugin authors must freeze at v1.0.59 to maintain compatibility.
   [Issue #3727](https://github.com/github/copilot-cli/issues/3727) | 4 comments

3. **#3781 – Image Pasting Bricks Sessions (Now Patched)**
   Pasting an image without a multimodal model caused an unrecoverable 400 loop. *Closed as resolved in v1.0.63*, but the fragility of session state during these errors raised broader concerns.
   [Issue #3781](https://github.com/github/copilot-cli/issues/3781) | 3 comments

4. **#3282 – Multiple BYOK Model Support**
   Top-voted open feature. Users want the ability to switch between multiple BYOK models without killing the session and re-setting environment variables.
   [Issue #3282](https://github.com/github/copilot-cli/issues/3282) | 👍 8

5. **#3784 – Linux ARM64 Panic (v1.0.62-1)**
   A Tokio reactor crash immediately after the first prompt blocks the CLI on ARM64 hardware (e.g., Raspberry Pi). High severity for users on non-x86 platforms.
   [Issue #3784](https://github.com/github/copilot-cli/issues/3784) | 2 comments

6. **#3769 – Agency Mode Output Mangling**
   Streaming responses in Agency mode exhibit character duplication and layout corruption until the response finishes. Disrupts the agentic workflow experience.
   [Issue #3769](https://github.com/github/copilot-cli/issues/3769) | 2 comments | 👍 3

7. **#3756 – Third-Party MCP Blocked by Policy**
   Enterprise users are locked out of third-party MCP servers by organization policy, leaving only built-in tools available. A recurring point of friction for managed environments.
   [Issue #3756](https://github.com/github/copilot-cli/issues/3756) | 3 comments

8. **#3782 – MCP Server Unbounded Tight Loop (v1.0.61)**
   A stdio MCP server was spawned thousands of times without backoff or a max-retry cap. A significant reliability incident for users with custom MCP servers.
   [Issue #3782](https://github.com/github/copilot-cli/issues/3782) | 1 comment

9. **#3776 / #3813 – UTF-8 Mojibake on Windows Copy/Paste**
   Text displays correctly in the terminal but pastes as garbled characters in Windows applications. Affects WSL, Ubuntu on WSL, and VS Code Terminal. A daily workflow blocker for non-English locales.
   [Issue #3776](https://github.com/github/copilot-cli/issues/3776) | 2 comments

10. **#3814 – Failed Requests Still Consume AIC**
    A user reported persistent transient API errors draining their allocation without successful output. Raises concerns about cost control and retry policies for metered plans.
    [Issue #3814](https://github.com/github/copilot-cli/issues/3814) | 👍 1

---

## 4. Key PR Progress
No substantive community or core pull requests were merged or updated in the last 24 hours. The single PR (#3817) appears to be non-functional or spam content. Development activity is currently concentrated on stabilizing the v1.0.6x line through patches rather than integrating new contributions.

---

## 5. Feature Request Trends
- **BYOK & Model Flexibility:** The strongest signal from the community is the need for multi-model BYOK support (#3282), custom HTTP headers for private deployments (#3399), and provider-specific optimizations like Anthropic prompt caching (#3808).
- **Session Intelligence:** Power users are outgrowing linear sessions. There is increasing demand for concurrent session management (#2966), full-text search of session history (#3807), and merging IDE (VS Code) chat history into the CLI `/chronicle` view (#3816).
- **Enterprise Hardening:** Requests for granular OAuth permission scoping (#953) and better visibility into policy-blocked features (#3756) are frequent from organizational users.

---

## 6. Developer Pain Points
- **Regression Whiplash:** The v1.0.6x cycle has been unusually volatile. Plugins broke in .60, MCP servers crashed in .61, and ARM64 panicked in .62-1. Users consistently express frustration over having to pin versions to maintain stability.
- **Fragile Session State:** Sessions can be permanently wedged by oversized attachments, model mismatches, or transient API errors, often requiring manual `.jsonl` editing for recovery. The v1.0.63 image handling fix is a step forward, but broader resilience is needed.
- **Cross-Platform Gaps:** Between the ARM64 crash (#3784), Windows installation EPERM errors (#3810), and unresolved UTF-8 paste corruption (#3776, #3813), non-standard platforms continue to feel like second-class experiences.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-06-16**, based on the GitHub activity snapshot of `MoonshotAI/kimi-cli`.

---

## 1. Today’s Highlights
The day’s activity is driven by contributor **logicwu0**, who submitted two targeted PRs—`#2453` and `#2454`—to fix long-standing failures in session persistence and the hooks system, directly addressing two of the hottest open bugs (`#2222` and `#2303`). On the downside, a critical new **system proxy bug (`#2455`)** was filed regarding `FetchURL` ignoring environment configuration, which impacts users behind firewalls or on WSL2. Meanwhile, the “high risk” compaction error (`#2402`) saw its discussion thread updated today but remains an open blocker with no official resolution.

## 2. Releases
- **None.** No new releases were published in the last 24 hours.

## 3. Hot Issues
_4 active issues were identified in the snapshot. Each is detailed below with context and community impact._

**#2455 [NEW] FetchURL Ignores System Proxy**
- **Author:** KuangYin-Z
- **Why it matters:** The `FetchURL` tool bypasses the system proxy configuration, breaking all external network calls for users in restricted environments (corporate firewalls, China, WSL2). The report stresses that `Shell` and `curl` work fine, exposing a hard bug that severely limits the CLI's portability.
- **Community reaction:** Freshly filed, no comments yet—this is likely to become a high-traffic issue for enterprise users.
- **Link:** [Issue #2455](https://github.com/MoonshotAI/kimi-cli/issues/2455)

**#2402 [RESURFACED] High Risk Compaction Error (`400 APIStatusError`)**
- **Author:** thoughtworld
- **Why it matters:** The compaction pipeline failed with an opaque "high risk" rejection. This blocks conversation management entirely for the affected model (`kimi-k2.6`). The issue was updated today but remains unresolved, indicating backend-side investigation is ongoing.
- **Community reaction:** Low commentary (2 replies), suggesting users are waiting on official guidance or a patch. The vague "high risk" label makes self-diagnosis difficult.
- **Link:** [Issue #2402](https://github.com/MoonshotAI/kimi-cli/issues/2402)

**#2303 [FIX INCOMING] UserPromptSubmit Hook Receives Empty Prompt in Shell UI**
- **Author:** AkaCoder404
- **Why it matters:** The hook system is the primary extensibility mechanism. Getting an empty prompt string when using the interactive CLI shell breaks custom regex-based workflows, pre-processing pipelines, and security validators. This makes the hook API unreliable for daily use.
- **Community reaction:** Addressed directly by PR `#2454`. The root cause was identified as a variable sourcing error in `KimiSoul._turn`.
- **Link:** [Issue #2303](https://github.com/MoonshotAI/kimi-cli/issues/2303)

**#2222 [FIX INCOMING] `--continue` Reports “No Previous Session Found”**
- **Author:** LiPingFeel
- **Why it matters:** The `--continue` flag is a core workflow primitive. Its inconsistent behavior—failing on one invocation but working on another in the same directory—erodes user trust in session management. This is a high-frequency frustration.
- **Community reaction:** Addressed by PR `#2453`. The fix introduces a fallback to the latest session when the specific `last_session_id` metadata is missing.
- **Link:** [Issue #2222](https://github.com/MoonshotAI/kimi-cli/issues/2222)

## 4. Key PR Progress
_2 pull requests were active in the snapshot. Both are high-quality, targeted fixes from contributor logicwu0._

**#2454 fix(hooks): pass prompt text to UserPromptSubmit from structured input**
- **Feature/Fix:** Resolves #2303. The hook system now correctly passes the user’s typed text to `UserPromptSubmit` when the input comes from the interactive shell (not just the `-p` flag).
- **Technical detail:** The PR identified that `text_input` was being derived from the wrong variable path in `KimiSoul._turn`. The fix ensures the raw prompt string is accessible for regex matching and hook logic.
- **Community impact:** Unblocks all custom hooks and third-party integrations that rely on this event.
- **Link:** [PR #2454](https://github.com/MoonshotAI/kimi-cli/pull/2454)

**#2453 fix(session): resume latest session when `last_session_id` is missing**
- **Feature/Fix:** Resolves #2222. Implements a graceful fallback in `Session.continue_`. When the specific `last_session_id` key is missing from the session metadata, the system now selects the most recent session from the working directory instead of failing immediately.
- **Technical detail:** Previously, the logic strictly required `work_dir + last_session_id` matching. The PR relaxes this to a "best effort" resume when metadata is incomplete.
- **Community impact:** Restores reliable `--continue` behavior across different file system states and OS platforms (Windows, macOS, Linux).
- **Link:** [PR #2453](https://github.com/MoonshotAI/kimi-cli/pull/2453)

## 5. Feature Request Trends
Distilling the signals from the current open issues:
- **System Proxy & Network Compliance (Implicit):** The `#2455` bug highlights a strong demand for full system-level network configuration respect. Users expect the CLI to inherit proxy, VPN, and TLS settings without manual environment flags.
- **Reliable Session Continuity:** The `#2222` fix is popular because sessions are the backbone of iterative AI-assisted coding. Users want guaranteed context resumption, even after crashes or directory switches.
- **Mature Hook API:** The `#2303` bug demonstrates that the community is actively trying to build automation on top of the CLI. There is a clear demand for a stable, well-documented hook system that works uniformly across CLI modes.
- **Transparent Error Handling:** The "high risk" error in `#2402` points to a need for better logging and user-facing status messages when internal API policies block a request.

## 6. Developer Pain Points
- **Environmental Context Blindness:** The CLI occasionally fails to inherit the host environment—specifically proxy settings (`#2455`) and file system state (`#2222`). This forces developers to debug issues that are purely environmental rather than code-related.
- **Inconsistent Core Commands:** Core invariants like `--continue` and the interaction shell hooks behave differently based on input mode or metadata state. This lack of uniformity reduces predictability for daily power users.
- **Opaque API Rejection:** The "high risk" compaction error is a prime example of a poor developer experience—a non-actionable status code with no retry path, suggestion, or timeout explanation.
- **Fragile State Management:** Session metadata and compaction states appear to be fragile. Users hitting edge cases (missing IDs, corruption, API rejections) face hard failures rather than graceful degradation.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for June 16, 2026.

---

### OpenCode Community Digest – June 16, 2026

#### 1. Today’s Highlights
The community is vibrating around critical memory stability (#20695) and a long-running demand for agent sandboxing (#2242), while a highly-upvoted proposal for native session goals (`/goal`) is gaining rapid momentum (#27167). On the development side, MCP compliance is seeing a strong push with several PRs landing for schema sanitization and server instructions. However, a spate of unremediated billing activation failures (#32420, #32482) is creating a serious trust emergency that needs immediate operational attention.

#### 2. Releases
No new releases in the last 24 hours.

---

#### 3. Hot Issues

**#20695 – Memory Megathread (97 Comments, 65 👍)**
The highest-traffic item in the tracker. Scattered memory leak reports have consolidated. Maintainers are pleading for heap snapshots rather than AI-generated solutions. This is the single biggest stability blocker right now.
[Issue Link](https://github.com/anomalyco/opencode/issues/20695)

**#2242 – Agent Sandboxing (69 Comments, 53 👍)**
A long-standing security feature request. Users want a `seatbelt`-like restriction on file access and command execution (similar to Codex CLI or Gemini CLI). This is a major adoption barrier for security-conscious teams.
[Issue Link](https://github.com/anomalyco/opencode/issues/2242)

**#6930 – Anthropic OAuth Violation & Ban (22 Comments, 14 👍)**
Alarming report of account bans triggered by OpenCode’s OAuth flow. If using the recommended login path, users risk losing their Anthropic account. This requires an urgent communication or provider clarification.
[Issue Link](https://github.com/anomalyco/opencode/issues/6930)

**#27167 – Native Session Goals / `/goal` (49 Comments, 84 👍)**
Strongest feature signal of the week. The proposal for persistent, declarative session goals (e.g., `/goal refactor auth module`) is overwhelmingly popular. It would solve the "repeat myself every prompt" frustration.
[Issue Link](https://github.com/anomalyco/opencode/issues/27167)

**#27906 – Bun Install Broken (18 Comments, 13 👍)**
v1.15.1+ introduced a hard requirement for postinstall lifecycle scripts, which Bun blocks globally by default. A breaking change that is disrupting the Bun developer workflow.
[Issue Link](https://github.com/anomalyco/opencode/issues/27906)

**#5374 – Show Tokens/Second (17 Comments, 81 👍)**
A consistent high-upvote feature request for real-time performance metrics. Essential for power users comparing providers and models.
[Issue Link](https://github.com/anomalyco/opencode/issues/5374)

**#28567 – Full MCP Client Capabilities (14 Comments, 22 👍)**
Users are comparing OpenCode to the latest MCP spec and finding gaps in streaming, resources, and prompts. This is the driving force behind several active PRs.
[Issue Link](https://github.com/anomalyco/opencode/issues/28567)

**#32420 / #32482 – Billing Activation Failures (5+ Reports)**
Multiple users report being charged for "OpenCode Go" with no workspace activation and zero support response. One user explicitly flags the process as a "scam." A critical retention and trust issue.
[Issue #32420](https://github.com/anomalyco/opencode/issues/32420) | [Issue #32482](https://github.com/anomalyco/opencode/issues/32482)

**#32484 – Build Agent Much Worse than Subagents (3 Comments)**
A compelling user report claiming the "build" agent is consistently outperformed by general or explore agents. If true, this indicates a regression in agent specialization that weakens the core product promise.
[Issue Link](https://github.com/anomalyco/opencode/issues/32484)

**#30869 – Hardcoded UTF-8 Decoding Breaks CJK Windows (5 Comments)**
`bash.ts` hardcodes `stdout.toString("utf8")`, causing garbled output on non-UTF-8 systems (e.g., Chinese GBK). A small fix with a huge impact on Windows accessibility.
[Issue Link](https://github.com/anomalyco/opencode/issues/30869)

---

#### 4. Key PR Progress

**#31985 – Fix Windows Shell Encoding**
Closes 5 issues. Uses PowerShell `EncodedCommand` for reliable UTF-8 output on Windows. The single most impactful cross-platform fix in the queue.
[PR Link](https://github.com/anomalyco/opencode/pull/31985)

**#29150 – Break Infinite Auto-Compact Loop**
Fixes a dangerous bug where context overflow detection fires forever when the provided model limit is smaller than the actual provider limit.
[PR Link](https://github.com/anomalyco/opencode/pull/29150)

**#32490 – Append MCP Server Instructions to Context**
Implements `InitializeResult.instructions` from the MCP spec. A core part of the ongoing MCP feature push. References #28567.
[PR Link](https://github.com/anomalyco/opencode/pull/32490)

**#32489 – Sanitize MCP Tool Schemas for OpenAI**
Fixes a hard crash when MCP tools emit JSON Schema keywords unsupported by OpenAI. Necessary for broad MCP compatibility.
[PR Link](https://github.com/anomalyco/opencode/pull/32489)

**#31645 – Progress Feedback for `opencode upgrade`**
Closes #31623. Adds real-time progress to the upgrade command, solving the "is it hung?" UX problem.
[PR Link](https://github.com/anomalyco/opencode/pull/31645)

**#31644 – Register `/compact` and `/summarize` Commands**
Fixes #31636. These advanced commands were silently missing from autocomplete and `/help`. Important for power-users leveraging compression.
[PR Link](https://github.com/anomalyco/opencode/pull/31644)

**#32487 – Configurable Cost Display Currency**
Closes #32485. Adds `display.currency` and `display.currency_rate` configuration options. A nice quality-of-life addition for the global user base.
[PR Link](https://github.com/anomalyco/opencode/pull/32487)

**#32499 – Allow Clearing Session Archive Time**
Closes #24153. Finally allows users to un-archive a session. A small but frequently requested UX fix.
[PR Link](https://github.com/anomalyco/opencode/pull/32499)

**#28466 – Ignore MCP Resource File Downloads**
Closes #14753 and others. Critical for MCP stability. Prevents the client from crashing or misbehaving when handling resource file downloads from MCP servers.
[PR Link](https://github.com/anomalyco/opencode/pull/28466)

**#32494 – Include PR Identity in GitHub Context**
Fixes #32233. Adds `pr_number` and `pr_url` to the context for `opencode github run`, improving the quality of automated PR reviews.
[PR Link](https://github.com/anomalyco/opencode/pull/32494)

---

#### 5. Feature Request Trends

**🛡️ Agent Sandboxing (Strongest Demand)**
Requests for filesystem and network restrictions (#2242, #16914) are persistent. Users want a clear "chroot" or "seatbelt" mode for the agent’s terminal.

**🎯 Session Goals & Lifecycle**
The proposal for a native `/goal` command (#27167) and agent-scoped skill loading (#19344) signals a strong desire for persistent, manageable state across interactions without context bloat.

**📊 Performance Visibility**
The demand for a `tokens/second` display (#5374) remains a top-voted request. Power users want to benchmark and debug provider speed easily.

**🔌 Full MCP Compliance**
Users are tracking the MCP spec closely. They want streaming, resource management, prompts, and proper schema handling (#28567). This is the most active development focus.

**✂️ Token Efficiency**
Developers are proactively profiling their sessions. Moving git/PR instructions out of the bash tool description (#21345) to save ~1.7K tokens per request is a clever, data-driven feature request.

---

#### 6. Developer Pain Points

**🚩 Billing & Support Black Hole**
The most acute pain point. Multiple users report being charged for a subscription that never activates, with zero response from the support email. This is actively eroding trust in the project's monetization model (#32420, #32482, #32466).

**🪟 Windows as a Second-Class Platform**
Windows users are disproportionately affected by hardcoded UTF-8 assumptions (#30869), broken Bun installs (#27906), terminal blocking in Playwright/Gradle (#22767, #22154), and UI renderer crashes (#32452). Build quality on Windows lags significantly.

**🌀 Agent Quality Inconsistency**
The explicit report that the "build" agent is worse than general subagents (#32484) suggests a core design or regression issue. If specialized agents aren't reliably better, the entire agent framework loses credibility.

**⏱️ Provider Idle Timeouts**
"Upstream idle timeout exceeded" errors (#28957, #31456) are a recurring frustration, particularly with longer planning skills or slow models. This breaks the user's flow hard.

**⚙️ Custom Provider Configuration Friction**
Users struggle with defining custom providers or newly released models (`kimi-k2.7-code-highspeed`, `deepseek-v4-flash`). Issues around default `max_tokens` (#1735) and missing input modalities (#26103, #32493) make flexibility feel brittle.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

## pi Community Digest - 2026-06-16

### 1. Today's Highlights
Version v0.79.4 ships with automatic first-run theme detection that reads your terminal background. The community is heavily focused on an `openai-codex` connection reliability bug (#4945) and a critical architectural issue around Shrinkwrap causing module duplication (#5653). Core PRs this cycle targeted long-running process hangs and stabilized the extension API for `print` mode users.

### 2. Releases
**v0.79.4** ([Release](https://github.com/earendil-works/pi/releases/tag/v0.79.4))
- **Automatic first-run theme selection:** pi now detects the terminal background color on first launch and automatically defaults to the `dark` or `light` theme.

### 3. Hot Issues

1. [#4945](https://github.com/earendil-works/pi/issues/4945) **[OPEN] `openai-codex` Connection Reliability Issues** (57 Comments, 30 👍)
   The top issue by engagement. Users report the interactive TUI gets stuck on `Working...` with no streamed text or error when using `openai-codex` / `gpt-5.5`. The only recovery is pressing Escape. Reproducible over several days.

2. [#5103](https://github.com/earendil-works/pi/issues/5103) **[OPEN] Windows Git-Bash Detection** (21 Comments, 0 👍)
   A persistent Windows pain point. The prebuilt binary fails to detect git-bash from PATH, breaking the built-in bash tool for Windows users.

3. [#5653](https://github.com/earendil-works/pi/issues/5653) **[OPEN] Move off Shrinkwrap** (10 Comments, 0 👍)
   Installing both `pi-ai` and `pi-coding-agent` as direct dependencies places two copies of `pi-ai` on disk, creating separate API provider registries via duplicated module-level `Map` instances. This is a critical SDK packaging flaw.

4. [#5702](https://github.com/earendil-works/pi/issues/5702) **[CLOSED] `prompt_cache_retention` Sent to Incompatible Providers** (8 Comments, 0 👍)
   Request failure caused by `generate-models.ts` not filtering `promptCacheRetention` for providers like OpenCode/Zen. Exposes a deeper maintainability concern in the model-registry build system.

5. [#5687](https://github.com/earendil-works/pi/issues/5687) **[CLOSED] `pi list` / `pi update` Hang with MCP Servers** (7 Comments, 0 👍)
   Package subcommands finish their work but never exit when an installed extension runs a long-lived MCP server. Forces users to Ctrl-C.

6. [#4877](https://github.com/earendil-works/pi/issues/4877) **[OPEN] Session Folder Collision** (15 Comments, 2 👍)
   Due to how sessions are stored, paths like `/a/b/c/d` and `/a-b/c-d` collide into the same session folder. Minor but surprising.

7. [#5728](https://github.com/earendil-works/pi/issues/5728) **[OPEN] Provider-Specific Config in `auth.json`** (6 Comments, 0 👍)
   Users want `auth.json` to carry provider-specific fields (e.g., `accountId`, `gatewayId`) instead of relying solely on environment variables.

8. [#5463](https://github.com/earendil-works/pi/issues/5463) **[OPEN] Auto-Compaction After Final Turn Throws Error** (2 Comments, 5 👍)
   Compaction after a normal assistant turn causes an unhandled error because the agent tries to `continue()` from the `assistant` role.

9. [#5773](https://github.com/earendil-works/pi/issues/5773) **[CLOSED] TUI Crashes on Long Extension Status Lines** (2 Comments, 0 👍)
   TUI crashes at startup if combined extension status text exceeds the terminal width.

10. [#5785](https://github.com/earendil-works/pi/issues/5785) **[CLOSED] Security Concern Over `--min-release-age=0` npm Flag** (2 Comments, 0 👍)
    A sharp debate over pi overriding the user's npm age-of-release protection during updates, arguing it undermines supply chain security.

### 4. Key PR Progress

1. [#5587](https://github.com/earendil-works/pi/pull/5587) **feat(coding-agent): experimental first-time setup flow** (CLOSED)
   The implementation behind v0.79.4's auto-theme. Behind `PI_EXPERIMENTAL=1`, shows the light/dark choice with live preview.

2. [#5675](https://github.com/earendil-works/pi/pull/5675) **fix: stabilize compaction after reload** (CLOSED)
   Preserves previous compaction token boundaries and fixes queued message delivery after agent reload. High stability impact.

3. [#5752](https://github.com/earendil-works/pi/pull/5752) **fix: `pi.sendUserMessage`/`sendMessage` return Promise** (CLOSED)
   Fixes a major extension API bug where `await` resolved immediately instead of waiting for the agent to finish processing the message.

4. [#5753](https://github.com/earendil-works/pi/pull/5753) **fix: drain stdout before resolving when child holds the pipe** (CLOSED)
   Fixes #5303. Resolves the long-standing hang where pi waits on a child process that holds stdout open past exit.

5. [#5758](https://github.com/earendil-works/pi/pull/5758) **fix(coding-agent): diagnose when a child holds stdio open** (CLOSED)
   Follow-up to #5753 that adds active diagnosis so pi doesn't have to wait for the full bash timeout.

6. [#5765](https://github.com/earendil-works/pi/pull/5765) **feat(d-pi): split `createDPiExtension`** (CLOSED)
   Decomposes the monolithic DP extension into `multi-agent-extension` and `remote-executor-extension` for better composability.

7. [#5509](https://github.com/earendil-works/pi/pull/5509) **feat: Add Amazon Bedrock Mantle OpenAI Responses provider** (OPEN)
   Major new provider for AWS users, supporting GPT 5.5/5.4 via Bedrock Mantle's OpenAI-compatible Responses API.

8. [#5762](https://github.com/earendil-works/pi/pull/5762) **Add ZAI-CN (bigmodel.cn) provider** (CLOSED)
   Expands support for the Chinese market with a dedicated built-in provider for BigModel's API.

9. [#5779](https://github.com/earendil-works/pi/pull/5779) **feat(coding-agent): XML-structured `/review` prompt responses** (CLOSED)
   Converts the `/review` command to use XML-structured instructions, enforcing a coverage-aware workflow and improving parsing.

10. [#5784](https://github.com/earendil-works/pi/pull/5784) **fix(coding-agent): sort threaded sessions by subtree activity** (OPEN)
    Improves the threaded session selector to sort by the most recent activity in the session subtree, not the root creation date.

### 5. Feature Request Trends
Three major vectors are driving enhancement requests:

- **Provider Proliferation:** Users are aggressively pushing for new LLM backends, including region-specific providers like ZAI China (`zai-cn`), cloud-native gateways like Amazon Bedrock Mantle, and latest models like Gemini 3.5 Flash in Vertex.
- **Configuration Hardening:** A strong desire to move config out of environment variables and hardcoded constants. This includes scoped provider config in `auth.json` (#5728), environment variables for truncation options (#5759), and SHA256 integrity files for binary releases (#5739).
- **Extension API Expansion:** The extension ecosystem is maturing. Requests to expose `edit-diff` for extensions (#5756), add prompt guideline APIs (#5711), and port focused tools (like the 4R review agents from gentle-ai, #5771) show users building deeper integrations.

### 6. Developer Pain Points

- **LLM Provider Instability:** The streaming layer remains the top support burden. The `openai-codex` "stuck on Working..." bug (#4945) garnered 30 reactions, while separate issues with MiniMax (#5777) and Z.AI (#845) highlight systemic fragility in the provider interface.
- **CLI & Process Management:** Package commands hanging when MCP servers are active (#5687) and child processes holding stdout open (#5753) create constant friction. The response to the `--min-release-age=0` flag (#5785) shows the community is highly sensitive to supply chain security.
- **Cross-Platform Consistency:** Windows support continues to lag, with the git-bash detection issue (#5103) remaining unresolved.
- **TUI Rendering and UX:** The TUI has accumulating paper-cuts: crashes on long status lines (#5773), markdown backticks rendered as raw text (#5766), and session selector idiosyncrasies (#5747). Low severity but high frequency of complaints.
- **SDK Architecture Debt:** The Shrinkwrap module duplication (#5653) stands out as a deep architectural issue affecting anyone building on `pi-ai` or `pi-coding-agent`. The model registry build system complexity was also flagged in #5702 as a maintainability risk.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-16

## 1. Today's Highlights
The project shipped **v0.18.1** and **desktop-v0.0.4** with stability fixes for daemon session gating and MCP persistence, alongside broad documentation corrections. A major engineering push on the `/loop` background automation roadmap is executing in parallel, with foundational PRs landing for a session wakeup primitive (#5182) and task-file support (#5148). Critical patches for OOM crashes on `/quit` (#5181) and model provider disambiguation (#5179) are moving through review, signaling strong attention to core reliability.

## 2. Releases
- **[v0.18.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1)**: General availability release. Close: includes a fix for oversized context instruction warnings (`he-yufeng`), gates direct session shell in the daemon behind explicit opt-in (`doudouOUC`), and resolves stale defaults in CLI docs.
- **[desktop-v0.0.4](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.0.4)**: Desktop app update that persists MCP server removals (`Jerry2003826`) and refreshes raw model-derived defaults.
- **Nightly/Preview**: `v0.18.1-preview.0` and `v0.18.1-nightly.20260616` are available for early testing of the ongoing loop and reliability work.

## 3. Hot Issues
1. **[#5055 — Trojan:JS false positive on VSIX](https://github.com/QwenLM/qwen-code/issues/5055)**  
   P1 security concern. The `v0.18.0` VSIX for Windows is flagged by Windows Defender (`Trojan:JS/ShaiWorm.DBA!MTB`). Community members have flagged this as a critical blocker. Status: `need-information`.

2. **[#5180 — Subagent crashes mid-task](https://github.com/QwenLM/qwen-code/issues/5180)**  
   A high-impact multi-agent bug where a subagent processing a delegated task fails mid-execution with heap issues. Logs from a 12-hour session are being analyzed. Status: `open`, P2.

3. **[#5147 — OOM crash after /quit](https://github.com/QwenLM/qwen-code/issues/5147)**  
   V8 heap exhaustion in `buildTranscriptMessages()` during auto-memory extraction even on short sessions. A targeted fix is already in PR #5181.

4. **[#5173 — Model provider selection does not persist](https://github.com/QwenLM/qwen-code/issues/5173)**  
   When multiple `modelProviders` entries share the same model `id` (e.g., `qwen3.7-max`) but different `baseUrl` values, the picker selection is lost on relaunch. High friction for complex routing setups.

5. **[#4966 — MCP schema string coercion breaks strict tools](https://github.com/QwenLM/qwen-code/issues/4966)**  
   LLMs emit numeric parameters as strings (`"depth": "3"`), which strict MCP servers reject. Reproducible with Playwright. Community interest is high.

6. **[#5160 — Discontinued OAuth model shown in picker](https://github.com/QwenLM/qwen-code/issues/5160)**  
   Running `/model` shows the discontinued `qwen-oauth` coder-model as selectable even when OAuth is not configured, confusing users about available features.

7. **[#5159 — Tmux trackpad hijacks history navigation](https://github.com/QwenLM/qwen-code/issues/5159)**  
   macOS users inside tmux sessions cannot scroll the conversation view; trackpad gestures cycle the prompt history instead. Input regression.

8. **[#5142 — Virtualized CLI history invisible](https://github.com/QwenLM/qwen-code/issues/5142)**  
   The new virtualized history mode renders the input box at the top and history is invisible; it only appears when the `/` key is pressed. Screenshots provided. Status: `welcome-pr`.

9. **[#5101 — Repeated large tool results bloat context](https://github.com/QwenLM/qwen-code/issues/5101)**  
   Deterministic local providers cause repeated large tool-result records to be resent through provider history, rapidly exhausting the context window. P1 impact.

10. **[#5177 — `exit_plan_mode` fails with empty plan](https://github.com/QwenLM/qwen-code/issues/5177)**  
    Calling `exit_plan_mode` with an empty `plan` parameter triggers a validation error, wasting API turns. Community interest with a `welcome-pr` label.

## 4. Key PR Progress
1. **[PR #5182 — `loop_wakeup` primitive](https://github.com/QwenLM/qwen-code/pull/5182)**  
   Foundation for self-paced `/loop` iterations. Adds a session-scoped one-shot wakeup tool. Does not yet change current `/loop` behavior.

2. **[PR #5181 — Fix OOM on /quit](https://github.com/QwenLM/qwen-code/pull/5181)**  
   Fixes `FATAL ERROR: Reached heap limit` in auto-memory by optimizing `buildTranscriptMessages()` to avoid regex flattening of large histories.

3. **[PR #5179 — Fix model provider disambiguation](https://github.com/QwenLM/qwen-code/pull/5179)**  
   Persists the selected provider's `baseUrl` alongside the model name, resolving the selection-loss issue in #5173.

4. **[PR #5175 — Mid-turn web-shell messages](https://github.com/QwenLM/qwen-code/pull/5175)**  
   Allows user messages typed while a turn is running to be drained into the active turn between tool batches, dramatically improving interactive flow.

5. **[PR #5171 — Auto-retry stream transport errors](https://github.com/QwenLM/qwen-code/pull/5171)**  
   Adds bounded automatic retry for transport-level stream drops before the first chunk, reducing transient network failures.

6. **[PR #5155 — Explicit subagent forking](https://github.com/QwenLM/qwen-code/pull/5155)**  
   Makes forking an explicit `subagent_type: "fork"` choice, preventing the model from unintentionally detaching when it needs results.

7. **[PR #5148 — `/loop` command surface & task files](https://github.com/QwenLM/qwen-code/pull/5148)**  
   Aligns the loop command surface, adds `/proactive` alias, and implements a project-level task-file reader for declarative loop behavior.

8. **[PR #5094 — Workflow P4: meta + `/workflows`](https://github.com/QwenLM/qwen-code/pull/5094)**  
   Phase 4 of the Dynamic Workflows port. Adds meta extraction and phase-tree visualization, building toward a full structured workflow engine.

9. **[PR #4943 — `--safe-mode` CLI flag](https://github.com/QwenLM/qwen-code/pull/4943)**  
   Disables all user customizations (hooks, MCP, skills, context files) for clean-slate troubleshooting. High demand from the community.

10. **[PR #4564 — Token usage stats & cost visibility](https://github.com/QwenLM/qwen-code/pull/4564)**  
    Implements persisted token accounting with daily/monthly breakdowns and CSV/JSON export in `/stats`. Addresses a long-standing feature request.

## 5. Feature Request Trends
- **Background automation & loops**: The `/loop` feature ecosystem is the dominant trend. Users want self-paced wakeups, task-file definitions, cancellation, and status feedback for long-running autonomous agents. Multiple focused child issues in [#5124](https://github.com/QwenLM/qwen-code/issues/5124) are carving this up into small, mergeable slices.
- **Diagnostic tooling**: Strong demand for `--safe-mode`, detailed token accounting, and proper model provider disambiguation reflects a maturing user base that needs production observability and troubleshooting.
- **Agentic control**: Requests for expanded hook interfaces (`toolCallId`, `terminalSequence`), explicit subagent forking, and improved permission/sudo dialogues show users want fine-grained control over autonomous behavior.
- **Desktop app parity**: Feature requests are migrating from core CLI to desktop app polish, including git branch display and interactive extension managers.

## 6. Developer Pain Points
- **Memory stability**: OOM crashes, especially during session exit with auto-memory enabled, are the most severe reliability issue. Community logs confirm V8 heap exhaustion even on moderate session sizes.
- **Shell and input friction**: Windows users struggle with `cmd` vs `pwsh` default environments, macOS users hit trackpad/tmux conflicts, and Ghostty terminal flickering in plan mode remains unresolved.
- **Integration edge cases**: Strict MCP schema validation (numeric string coercion), sudo command handling, and `exit_plan_mode` empty-parameter failures create recurring workflow interruptions.
- **Configuration drift**: Stale default values, discontinued models appearing in pickers, and non-persisting provider selections indicate a need for stricter configuration lifecycle management and migration paths.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-16

*Sourced from the `github.com/Hmbown/CodeWhale` issue tracker.*

## 1. Today's Highlights
The past 24 hours brought substantial infrastructure merges, including a profound refactor of the provider system into a data-driven registry ([#3005](https://github.com/Hmbown/CodeWhale/pull/3005)) and the foundation for atomic security policy persistence ([#3233](https://github.com/Hmbown/CodeWhale/pull/3233)). Despite this engineering progress, the community's attention remains fixed on several critical reliability blockers—most notably the "Turn stalled" error in YOLO mode ([#2487](https://github.com/Hmbown/CodeWhale/issues/2487)) and intermittent TUI freezes on Windows ([#1812](https://github.com/Hmbown/CodeWhale/issues/1812)). These issues continue to generate the highest levels of engagement and frustration.

## 2. Releases
No new releases were published in the last 24 hours. The project remains in a stabilization phase following the v0.8.59 release cycle, which addressed the macOS mouse-report input leak and cleared the main issue/PR queue.

## 3. Hot Issues

1. **[#2487 – "Turn stalled" error in YOLO mode](https://github.com/Hmbown/CodeWhale/issues/2487)** (OPEN, Bug, 13 comments)  
The UI becomes completely unresponsive mid-operation, and sending `continue` fails to recover the session. This is the most active open issue and represents a core stability crisis for the full-autonomy workflow.

2. **[#3063 – v0.8.59 Release Tracker](https://github.com/Hmbown/CodeWhale/issues/3063)** (CLOSED, Tracker, 11 comments)  
Shipped the TUI mouse-report input leak fix on macOS and a full maintainer queue triage. Demonstrates the project's structured approach to stabilization releases.

3. **[#3096 – Headless Sub-agent Worker Runtime](https://github.com/Hmbown/CodeWhale/issues/3096)** (CLOSED, Enhancement, 8 comments)  
Proposes decoupling sub-agent execution from the main TUI process entirely, moving from in-process async tasks to a lightweight headless runtime. This directly addresses the "too UI-shaped" criticism of the current fan-out architecture.

4. **[#1812 – TUI Freezes on Windows 11](https://github.com/Hmbown/CodeWhale/issues/1812)** (OPEN, Bug, 6 comments)  
Complete UI lockups under load, confirmed with logs and thread-state analysis. The process stays alive but the UI becomes a zombie. Unusable for Windows users in the current state.

5. **[#2739 – Task Execution Hangs / Context Loss](https://github.com/Hmbown/CodeWhale/issues/2739)** (OPEN, Bug, 3 comments)  
Stuck in infinite wait loops. Escaping yields connection timeout. Using `--continue` wipes the entire session context. The user explicitly states this "frequent issue cannot be tolerated" and has persisted across multiple versions (0.8.51+).

6. **[#2574 – Provider Fallback Chain](https://github.com/Hmbown/CodeWhale/issues/2574)** (OPEN, Enhancement, 4 comments)  
Request for automatic provider failover on 401/429/5xx errors. Currently requires manual `/provider` commands, destroying workflow momentum.

7. **[#2629 – SiliconFlow & TokenHub 401 Errors](https://github.com/Hmbown/CodeWhale/issues/2629)** (OPEN, Bug, 4 comments)  
Persistent `invalid api key` failures on two popular Chinese cloud platforms despite correct config. Suggests a narrow protocol mismatch in the provider layer.

8. **[#3192 – Agent Client Protocol Registry](https://github.com/Hmbown/CodeWhale/issues/3192)** (OPEN, Enhancement, 6 comments)  
Request to list CodeWhale in the ACP registry for seamless Zed installation. Signals growing strategic interest in CodeWhale as a universal, editor-agnostic agent backend.

9. **[#1186 – Typed Persistent Permission Rules](https://github.com/Hmbown/CodeWhale/issues/1186)** (OPEN, Enhancement, 9 comments)  
Scopes `allow/deny/ask` rules by tool name, command prefix, and workspace path. A foundational security feature for making high-autonomy modes viable in production environments.

10. **[#3102 – First-Class Clarification Questions](https://github.com/Hmbown/CodeWhale/issues/3102)** (OPEN, Enhancement, 4 comments)  
Proposes a dedicated modal UI for agents to ask the user clarifying questions instead of emitting plain chat messages. Directly addresses UX friction for secret entry and parameter gathering.

## 4. Key PR Progress

1. **[#3005 – Provider Metadata Data-Driven Registry](https://github.com/Hmbown/CodeWhale/pull/3005)** (MERGED)  
Eliminates ~100 hand-maintained match arms across two crates. A `Provider` trait backed by a static `PROVIDER_REGISTRY` now powers provider config. This is the architectural bedrock for dynamic provider fallback and easier third-party provider contributions.

2. **[#3235 – DeepInfra Provider Support](https://github.com/Hmbown/CodeWhale/pull/3235)** (MERGED)  
Adds DeepInfra, an OpenAI-compatible inference cloud hosting 100+ open models. Directly addresses community demand for provider diversity.

3. **[#3233 – Atomic Ask-Only Permission Persistence](https://github.com/Hmbown/CodeWhale/pull/3233)** (MERGED)  
Implements the config store backend for the typed permission rules system. Writes are atomic, ensuring config safety without yet adding the approval UI layer.

4. **[#3241 – Dollar Skill Aliases (`$skill-name`)](https://github.com/Hmbown/CodeWhale/pull/3241)** (MERGED)  
Introduces `$` prefix as a direct composer alias alongside existing `/skill` syntax. A small UX tweak with high power-user impact.

5. **[#3244 – Retry Release Lookups and Downloads](https://github.com/Hmbown/CodeWhale/pull/3244)** (MERGED)  
Adds retry logic for transient GitHub release metadata and asset-download failures. Strengthens the reliability of the update mechanism.

6. **[#3206 – WeChat Bridge via Feishu / Tencent OpenClaw](https://github.com/Hmbown/CodeWhale/pull/3206)** (MERGED)  
Community contribution enabling CodeWhale access from within WeChat by leveraging the existing Feishu bridge. Strong signal of organic ecosystem growth.

7. **[#3257 – App-Server Canonical Runtime Entrypoint](https://github.com/Hmbown/CodeWhale/pull/3257)** (MERGED)  
Consolidates the server-mode architecture by delegating `app-server –http/–mobile` to the existing `serve` runtime path. A clean architectural consolidation.

8. **[#2239 – i18n Phase 1-4b Wiring](https://github.com/Hmbown/CodeWhale/pull/2239)** (OPEN)  
Massive effort (+1059 lines, 47 files) integrating translations into the actual UI layer. Fixes 109 rebase compile errors. Demonstrates deep commitment to global adoption despite significant merge complexity.

9. **[#3242 – `workspace_follow_symlinks` Setting](https://github.com/Hmbown/CodeWhale/pull/3242)** (OPEN)  
Adds symlink-aware directory traversal for walk-based tools. A direct fix for workflow limitations with linked directories.

10. **[#2986 – Harvest-Credit Close Template](https://github.com/Hmbown/CodeWhale/pull/2986)** (MERGED)  
Formalizes the process for crediting contributors when their PR content is harvested. An important community governance and trust document.

## 5. Feature Request Trends

**Provider Ecosystem Resilience**  
Users want CodeWhale to function as an intelligent, resilient gateway. The strongest signals are for automatic provider failover chains, scriptable/dynamic API key retrieval, and a move toward the Agent Client Protocol for editor integration. The provider layer must handle backends failing silently.

**Long-Horizon Autonomous Agents ("Goal Mode")**  
The demand for persistent, multi-turn agent objectives remains high. Users want checkpointed sub-agents, resource usage telemetry, and an LLM-as-judge loop that continues work across turns until a goal is met. The current serial todo-list model is seen as too fragile for complex multi-file tasks.

**Security & Execution Policy**  
A clear shift toward making full autonomy viable. The typed persistent permission rules system is the keystone: allowing users to define granular `allow/deny/ask` policies scoped to paths, commands, and tools. This is the path to making YOLO modes safe for production codebases.

**Better Agent-Human Interaction**  
Dedicated UI for agent clarification requests and the ability to interrupt an agent mid-todo-list are the top UX requests. Users want to save time and tokens by redirecting an agent in-flight, not waiting for all scheduled tasks to complete.

## 6. Developer Pain Points

**Core Stability is the #1 Exit Driver**  
The "Turn stalled" bug, Windows freezes, and general task hangs are actively driving users away. The strong language in comments ("unbearable", "实在无法忍受", "cannot be tolerated") signals that no amount of new features will retain users if the foundation remains brittle.

**Sub-Agent Parallelism is Unreliable in Practice**  
Advertised parallel capabilities break under real load. Hard 120-second API ceilings, clipped output that the model hallucinates into complete evidence, and UI corruption during SSE streaming make `agent_open`/`agent_eval` workflows high-risk for long-running tasks.

**Provider Integration is a Trial-and-Error Nightmare**  
OpenAI API compatibility is not universal. Platforms like SiliconFlow and Moonshot fail with opaque errors. Without clear protocol mismatch diagnostics, users are left debugging with zero feedback from the provider layer.

**Session Context is Too Volatile**  
Losing a long-running session's context due to a hang or corruption is a killer. The inability to reliably resume a complex task without losing all state severely damages trust, especially for migrations or multi-file refactors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*