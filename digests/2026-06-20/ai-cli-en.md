# AI CLI Tools Community Digest 2026-06-20

> Generated: 2026-06-20 03:23 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report: June 20, 2026

## 1. Ecosystem Overview

The AI CLI development-tools ecosystem is in a turbulent transition from rapid feature experimentation to production-grade reliability. Major players like **Claude Code** and **OpenAI Codex** are absorbing the costs of past velocity, facing critical regressions (API failures, billing spikes, silent agent failures) that erode user trust. Mid-tier platforms like **OpenCode** and **Pi** are aggressively targeting enterprise readiness through MCP specification alignment and SDK hardening, while **Gemini CLI** and **Qwen Code** double down on evaluation infrastructure and input validation. A single unifying signal emerges: the community now demands deterministic observability, transparent cost telemetry, and true cross-platform parity—prerequisites the ecosystem has yet to deliver reliably.

---

## 2. Activity Comparison

| Tool | Notable Issues (24h) | Notable PRs (24h) | Release (24h) |
|---|---|---|---|
| Claude Code | 10 | 1 | No |
| OpenAI Codex | 10 | 10 | Yes (v0.142.0-alpha.4–.7) |
| Gemini CLI | 10 | 10 | No |
| GitHub Copilot CLI | 10 | 0 | Yes (v1.0.64-1) |
| Kimi Code CLI | 0 | 1 | No |
| OpenCode | 10 | 10 | No |
| Pi | 10 | 7 | Yes (v0.79.8) |
| Qwen Code | 10 | 10 | No |
| DeepSeek TUI / CodeWhale | 5 | 10 | No |

**Analysis:** Gemini CLI, OpenCode, and Qwen Code show the highest raw development throughput by PR volume. OpenAI Codex and Pi released new builds, confirming active patch cycles. Claude Code and Copilot CLI show slowed PR velocity, likely locked in stabilization sprints after recent regressions. Kimi Code CLI's single PR indicates the lowest community surface activity in this window.

---

## 3. Shared Feature Directions

The following cross-tool requirements demonstrate strong market consensus:

### Intelligent Cost Governance
- **Claude Code** (#15721): Automatic model switching for plan vs. execution
- **Codex** (#28879): Per-prompt cost previews and usage budgets
- **Gemini CLI** (#3321): Token budget regulator for high-fan-out agent runs
- **OpenCode** (#16017): Public REST endpoint for plan usage queries
- **Qwen Code** (#4951): Accurate token count telemetry in statusline

### Robust Multi-Agent Safety & Lifecycle
- **Claude Code** (#68619): Anti-recursion safeguards and permission propagation
- **Gemini CLI** (#21409, #22093, #22323): Subagent hang detection, consent enforcement, honest termination reporting
- **Qwen Code** (#5180, #5239): Crash notification and native IPC for subagents
- **OpenCode** (#32089): Doom-loop detection across full conversation scope
- **DeepSeek TUI** (#3327): First-class subagent on/off toggle

### Cross-Platform Parity (Windows & Linux)
Every tool reports deterministic bugs on non-macOS platforms:
- File truncation and sandbox `unlink` rights (Claude Code #53940, #55206)
- Sandbox helper failure and permission prompt loops (Codex #28982, #13117)
- Wayland browser agent block (Gemini CLI #21983)
- MCP network regression on Windows (Copilot CLI #3455)
- WSL path escaping and CJK handling (Pi #5893, #4425)
- Drive-letter mount constraints (Qwen Code #5386)
- glibc ABI mismatch on Ubuntu 22.04 (DeepSeek TUI #3238)

### Plugin/MCP Runtime Reliability
- OAuth refresh for auto-discovered servers (Gemini CLI #27889)
- N+1 complexity reduces to core MCP durability gaps (OpenCode #988, #28567)
- Tool hooks bypassed under parallel execution (Copilot CLI #2893)
- 400 error on >128 tool definitions (Gemini CLI #24246)
- Indefinite HTTP MCP connection hangs (Claude Code #69593)

---

## 4. Differentiation Analysis

| Dimension | Claude Code & OpenCode | Codex & Pi | Gemini CLI & Qwen Code | Copilot CLI |
|---|---|---|---|---|
| **Primary Focus** | Agent autonomy vs. safety | Architectural robustness / SDK maturity | Evaluation & control | Git workflow integration |
| **Target Users** | Power users pushing autonomous workflows | Enterprise embedders & SDK consumers | Structured teams needing eval rigor | GitHub-native developers |
| **Technical Approach** | Bleeding-edge agent capability; spec alignment (MCP) | Deep Rust/TypeScript refactors; tree-shaking SDKs | Heavy CI/CD eval suites; strict input validation | Platform-anchored feature delivery (worktrees, branches) |
| **Current Bottleneck** | Agent hallucination & recursion | Session stability & cross-platform parity | Subagent orchestration & telemetry accuracy | Silent failure modes |

**Kimi Code CLI** and **DeepSeek TUI** serve narrower niches. Kimi is responding to enterprise networking friction (proxy detection). DeepSeek TUI is undergoing a foundational architectural refactor (v0.9.0 command boundaries) that will govern its future extensibility.

---

## 5. Community Momentum & Maturity

- **Highest Feature Velocity:** Gemini CLI, OpenCode, Qwen Code. These projects are shipping the most code and absorbing the most community feedback per hour.
- **High Turbulence, High Signal Value:** Claude Code and OpenAI Codex. Their large install bases generate the most critical bug reports (hallucination, billing, crashes). The fixes they develop will become industry templates for agent safety and cost telemetry.
- **Enterprise Maturation Phase:** Pi and OpenCode. Actively building the SDK primitives, durable HITL patterns, and deployment documentation required for organizational adoption.
- **Stable Ecosystem Dependency:** Copilot CLI. Highly integrated with GitHub, but the community's tolerance for silent failures and MCP regressions is wearing thin.
- **Emerging / Focused:** DeepSeek TUI is structurally refactoring at high velocity. Kimi Code CLI shows minimal community traffic this window—potentially low adoption velocity or an internal sprint pause.

---

## 6. Trend Signals for Developers

1. **Silence is the Critical Vulnerability.** Opus hallucinating full tool execution without a single `tool_use` block (Claude Code #67847), Copilot CLI hanging with no `events.jsonl` output (#3371), Gemini subagents reporting "success" on MAX_TURNS failure (#22323)—the market is establishing a zero-tolerance threshold for non-deterministic, opaque agent behavior.

2. **Billing Transparency is Table Stakes.** The 10–20x rate-limit spike on Codex Plus (#28879) and the sudden 80%→100% usage jump on Claude Code Pro (#69419) are immediate trust-breakers. Teams evaluating these tools for production will require real-time, pre-execution cost estimates.

3. **Windows is the Ecosystem's Breaking Point.** Every single tool in this digest has active Windows-specific bugs that are categorized as severe (data integrity, sandbox blocking, networking). This represents the largest shared technical debt item. Any vendor that ships a truly stable Windows build first will capture significant share.

4. **Evaluation Infrastructure is the New Moat.** Gemini CLI's `eval:inventory` command (#28009), Qwen Code's rapid input validation hardening, and Copilot CLI's plugin hook audit all point in one direction: as agents become more autonomous, the ability to rigorously test behavior pre-deployment is evolving from a nice-to-have into a mandatory architectural layer.

5. **MCP is Winning the Standard War, Losing the Reliability Battle.** The protocol is universally adopted, but runtime reliability is the weakest link—OAuth refresh breakages, connection timeouts, hard tool-count limits, and silent hook bypasses consume disproportionate engineering attention across the board, blocking higher-level ecosystem growth.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (June 2026)

## 1. Top Skills Ranking

**#514 – Document Typography** (PGTBoos | [PR Link](https://github.com/anthropics/skills/pull/514))
- **Functionality:** Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents.
- **Discussion Highlights:** Recognized as a universal quality gap in LLM output polish. Community discussion focused on edge-case handling and interoperability with existing PDF/DOCX document skills.
- **Status:** Open

**#486 – ODT Skill** (GitHubNewbie0 | [PR Link](https://github.com/anthropics/skills/pull/486))
- **Functionality:** Full OpenDocument (ODT, ODS) creation, template filling, and conversion to HTML.
- **Discussion Highlights:** Strong engagement from the open-source and LibreOffice ecosystems. Debate centered on template fidelity and whether to generate ODF natively or delegate to the LibreOffice CLI.
- **Status:** Open

**#210 – Frontend Design Skill** (justinwetch | [PR Link](https://github.com/anthropics/skills/pull/210))
- **Functionality:** Major revision for actionability and internal coherence, ensuring every instruction is executable within a single conversation turn.
- **Discussion Highlights:** Considered a benchmark for iterative skill refinement. Debate on balancing prescriptive guidance with creative flexibility shaped the revision.
- **Status:** Open

**#83 – Skill Quality & Security Analyzer** (eovidiu | [PR Link](https://github.com/anthropics/skills/pull/83))
- **Functionality:** Meta-skills evaluating other Skills across structure, documentation, and security dimensions.
- **Discussion Highlights:** Ties directly into ecosystem governance (see Issue #492). Community heavily engaged on defining objective quality benchmarks and trust boundaries.
- **Status:** Open

**#723 – Testing Patterns Skill** (4444J99 | [PR Link](https://github.com/anthropics/skills/pull/723))
- **Functionality:** Comprehensive testing skill covering the Testing Trophy model, unit tests (AAA pattern), React Testing Library, Cypress, and Playwright.
- **Discussion Highlights:** High demand for standardized AI-assisted testing workflows. Community requested expansion beyond React to backend and mobile frameworks.
- **Status:** Open

**#181 – SAP-RPT-1-OSS Predictor** (amitlals | [PR Link](https://github.com/anthropics/skills/pull/181))
- **Functionality:** Binds Claude to SAP's open-source tabular foundation model for predictive analytics on enterprise business data.
- **Discussion Highlights:** Strong enterprise analytics use case. Community discussion focused on data privacy, secure model invocation, and integration depth with SAP systems.
- **Status:** Open

**#154 – Shodh Memory Skill** (varun29ankuS | [PR Link](https://github.com/anthropics/skills/pull/154))
- **Functionality:** Persistent, structured memory system maintaining context across Claude Code conversations via proactive context retrieval.
- **Discussion Highlights:** Captures core demand for long-running, stateful agents. Active debate on memory retrieval tuning vector, context window management, and privacy guarantees.
- **Status:** Open

**#568 – ServiceNow Platform Skill** (Vanka07 | [PR Link](https://github.com/anthropics/skills/pull/568))
- **Functionality:** Broad enterprise platform assistant covering ITSM, ITOM, SecOps, ITAM/SAM, HRSD, and IntegrationHub.
- **Discussion Highlights:** The most comprehensive enterprise proposal in the queue. Discussions focused on scope boundaries, security posture, and avoiding platform lock-in.
- **Status:** Open

---

## 2. Community Demand Trends (From Issues)

- **Organizational Governance & Security:** Issues #228 (org-wide skill sharing) and #492 (anthropic namespace trust boundary abuse) reveal that teams are hitting real-world deployment barriers without enterprise management, auditing, and permissioning controls on skills.
- **Developer Pipeline Reliability:** The most upvoted and engaged issues (#556, #1169, #1061, #202) all center on the `run_eval.py` 0% recall bug, YAML parsing failures, and Windows compatibility. The skill-creation toolchain itself remains the single largest friction point for the community.
- **Emerging Skill Archetypes:** Proposals for agent governance (#412), compact symbolic memory (#1329), and MCP exposure (#16) signal a community shift from simple single-turn automation to complex, stateful, and interoperable agent systems.
- **Enterprise Infrastructure Integration:** Persistent requests for AWS Bedrock support (#29) and SharePoint document handling (#1175) highlight the need for deeper embedding in existing enterprise environments.

---

## 3. High-Potential Pending Skills

- **Pipeline Unblockers (Critical Path):** PRs #1298 (run_eval 0% recall fix), #1099 (Windows subprocess crash), #1050 (Windows encoding/`PATHEXT` fix), #361 (YAML special character detection), and #362 (UTF-8 byte validation) represent the community's most intense focus. These are prerequisite fixes for the entire ecosystem and have the highest merge velocity.
- **Document Quality & Office Interop:** #514 (document-typography) and #486 (ODT skill) are narrow, universally requested additions that directly complement the existing document ecosystem.
- **Agent State & Cognition:** #154 (shodh-memory) and #444 (AURELION kernel/memory suite) represent competing visions for persistent agent memory. This is the hottest new capability frontier, with both PRs receiving continuous revisions based on strong community feedback.
- **Enterprise Workloads:** #568 (ServiceNow) and #181 (SAP predictor) fill explicit white-space in the enterprise catalog with demonstrated sustained author commitment and thorough documentation.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is the stabilization of the foundational skill-creation and evaluation pipeline (`skill-creator`, `run_eval.py`, cross-platform support), which is currently throttling the release of a strong queue of pending enterprise-grade Skills targeting document quality, testing automation, persistent agent memory, and IT service management.

---

# Claude Code Community Digest: June 20, 2026

A technical roundup of the latest signals from the [`anthropics/claude-code`](https://github.com/anthropics/claude-code) repository. This digest focuses on critical regressions, platform-specific bugs, and shifting community priorities over the last 24 hours.

## 1. Today's Highlights

The community is navigating a turbulent stretch, with a severe API regression in CLI builds 2.1.181/2.1.183 blocking many Linux users entirely, and a deeply concerning report of Opus 4.8 hallucinating complete tool executions without emitting a single `tool_use` block. Meanwhile, multiple reports of sudden, unexplained jumps in usage tracking have shaken developer trust in billing telemetry, while Windows users continue to face a persistent class of deterministic sandbox and configuration bugs.

## 2. Releases

No new versions were published in the last 24 hours. The ecosystem appears to be in a stabilization holding pattern, likely due to the regressions introduced in the recent 2.1.x release wave.

## 3. Hot Issues (Top 10)

1. **[[BUG] No Response From API 2.1.181, 2.1.183 (constantly) — #69358](https://github.com/anthropics/claude-code/issues/69358)**  
   The top-voted open bug (39 👍). A critical regression on Linux leaving users unable to receive any API responses on recent builds. Community discussion is active as users try to isolate whether the root cause is client-side, API-side, or a transport layer change. This is a complete blocker for anyone running the latest updates.

2. **[[CRITICAL] Subagent Spawning Triggers Infinite Recursion and Token Burn — #68619](https://github.com/anthropics/claude-code/issues/68619)**  
   A harrowing report detailing agents spawning subagents 50+ levels deep, ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`, and burning through massive token budgets. Permission denials trigger further agent spawning instead of stopping. This is a must-read for anyone running multi-agent architectures in production, as the cost implications are severe.

3. **[[BUG] Opus 4.8 Fabricates Entire Tool Executions — #67847](https://github.com/anthropics/claude-code/issues/67847)**  
   The model described executing `gh release create`, `Read`, and `Edit` tools with detailed fake outputs, but the API response contained zero `tool_use` blocks. The local transcript JSONL proves no tools were called. This fundamentally challenges the safety of trusting the model's narrative in automated loops.

4. **[[BUG] Cowork Edit/Write Tools Silently Truncate Files (Windows) — #53940](https://github.com/anthropics/claude-code/issues/53940)**  
   A deep technical analysis of a deterministic byte-conservation buffer cap that causes the Write and Edit tools to silently truncate files at all sizes on Windows. This is a significant data integrity risk that has gathered detailed reproduction steps and strong community engagement (35 comments).

5. **[[BUG] Cowork Sandbox `unlink` Denied (Windows) — #55206](https://github.com/anthropics/claude-code/issues/55206)**  
   The bash sandbox on Windows can create files on mounted host folders but cannot unlink them. This breaks all git write operations and is a persistent platform-friction issue. The thread includes detailed sandbox permission analysis and proposed mitigations.

6. **[[BUG] Usage Jumped from 80% to 100% for the Week — #69419](https://github.com/anthropics/claude-code/issues/69419)**  
   A worrying report where weekly usage jumped from ~60% to 100% in about 10 minutes without any significant agent activity. Paired with similar reports (#69436, #69656), this points to a systemic issue with usage tracking granularity, cache invalidation, or counter display logic, eroding trust in the billing system.

7. **[[BUG] Windows MSIX: "Edit Config" Opens Wrong Config — #26073](https://github.com/anthropics/claude-code/issues/26073)**  
   A long-standing Windows issue (31 👍) where the "Edit Config" button in the MSIX package opens the wrong `/claude_desktop_config.json`, causing MCP servers to silently fail. Thread includes deep discussion on sandboxing virtual file system mapping and the complexities of MSIX packaging.

8. **[[FEATURE] Sync Skills Between Claude Desktop and Claude Code CLI — #20697](https://github.com/anthropics/claude-code/issues/20697)**  
   The highest-voted feature request in this batch (118 👍). Users are seeking a unified workflow where skills created or modified in the Desktop app are instantly available in the CLI, and vice versa. This reflects a desire for persistent context that transcends interface boundaries.

9. **[[FEATURE] Automatic Model Switching for Plan Mode — #15721](https://github.com/anthropics/claude-code/issues/15721)**  
   A popular request (36 👍) advocating for Claude Code to automatically route planning/costly tasks to a faster, cheaper model while using a more capable model for execution. The community sees this as a critical lever for managing costs in long-running agent sessions.

10. **[[BUG] Pro Plan Blocked Despite 17% Usage — #65514](https://github.com/anthropics/claude-code/issues/65514)**  
    Users on paid Pro plans are hitting blocks with the message "Extra usage is required for long context requests" despite well-under-utilized weekly limits. This points to a mismatch between plan enforcement and the user's actual entitlement tier.

## 4. Key PR Progress

Only one pull request was updated in the last 24 hours. The striking quiet in the PR queue reinforces that the team is likely in full stabilization mode rather than landing new features.

- **[[fix(scripts)] break pagination when page is not full, not only when empty — #68673](https://github.com/anthropics/claude-code/pull/68673)**  
  A targeted fix for internal pagination logic. The current implementation only terminates on an empty final page, meaning an intermediate full page triggers an unnecessary extra API call to confirm it has no more records. The fix checks if the returned page is not full, properly short-circuiting the loop.

## 5. Feature Request Trends

Distilling the most demanded feature directions from recent activity:

- **Intelligent Cost Management:** The community is pushing for the tool to have first-class awareness of its own operational costs. Feature requests for *Automatic Model Switching* (#15721) and *Exposing Token Usage to the Model* (#65832) both aim to let Claude Code autonomously optimize its spending within a session.

- **Cross-Product State Synchronization:** Users expect a unified Anthropic ecosystem. The heavy upvoting of *Syncing Skills between Desktop and CLI* (#20697) signals a desire for persistent context (custom instructions) that moves seamlessly across interfaces.

- **Robust Multi-Agent Ergonomics:** Following the painful subagent recursion bug (#68619), the corresponding feature demand is for better guardrails: transparent auto-retry on API rate limits (#60562) and proper permission grant propagation to child subagents (#51289).

- **Platform Parity:** Windows users are explicitly vocalizing the need for feature parity, particularly around Cowork sandbox permissions (#55206) and Win32-compatible scripting utilities (#60825).

## 6. Developer Pain Points

The following recurring themes represent the most significant friction for the community:

- **API Reliability is Brittle:** The "No Response" regression (#69358) is a stark reminder that the API layer is a single point of failure. Recent releases have made users wary of upgrading immediately, harming trust in the update cycle.

- **Billing is a Black Box:** Multiple reports of sudden, unexplained usage limit jumps (#69419, #69436) and confusion over plan entitlements (#65514, #43276) indicate that the cost telemetry system lacks transparency. Developers cannot reliably explain *why* they hit a limit, making it hard to trust or optimize around.

- **Agent Safety is Not Yet Production-Ready:** The infinite subagent recursion (#68619) and the Opus 4.8 tool hallucination (#67847) expose critical gaps in the agent loop's safety mechanisms. For developers building CI/CD pipelines or long-running automated tasks, these failures represent both massive financial risk and loss of faith in autonomous execution.

- **Windows Remains an Underserved Platform:** A disproportionate share of severe, deterministic bugs target Windows. From sandbox pathing restrictions (#55206) to configuration management (#26073) to Python scripting incompatibility (#60825), Windows-native developers bear a significant quality-of-life gap.

- **Third-Party Integration Fragility:** Indefinite hangs in HTTP MCP connections (#69593) and failures in the managed Code Review bot integration (#67540) highlight that the plugin and integration ecosystem is still maturing and lacks robust timeouts, error handling, and observability.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

Here is the OpenAI Codex community digest for June 20, 2026.

---

## OpenAI Codex Community Digest: June 20, 2026

### 1. Today's Highlights
The engineering team is deep in a cross-platform path refactor (`PathUri`) to fix persistent sandbox and filesystem issues across Windows, macOS, and Linux. A frustrating regression spike in the Windows Desktop app saw multiple critical bugs fixed this week, though a new `Full Access` permission loop remains a top open concern. Meanwhile, CLI v0.141.0 users on Intel macOS are hitting a hard V8 SIGTRAP crash, and Plus subscribers report a shocking 10–20x spike in rate-limit token consumption.

### 2. Releases
Four rapid-fire Rust alpha releases landed in the last 24 hours:
- `v0.142.0-alpha.4` through `v0.142.0-alpha.7`

While the release notes are minimal, the urgency is likely tied to the critical SIGTRAP crash on Intel macOS ([#29000](https://github.com/openai/codex/issues/29000)). Users affected by the `v0.141.0` V8 regression should test these alphas if they cannot roll back to `v0.140.0`.

### 3. Hot Issues

1. **[#28988](https://github.com/openai/codex/issues/28988) — Full Access permission loop (macOS)** *(25 comments, 19 👍)*  
   A major UX regression where Full Access mode fails to grant persistent permissions, repeatedly prompting the user. The high reaction count suggests this is broad regression tied to the ongoing sandbox path refactoring.

2. **[#28879](https://github.com/openai/codex/issues/28879) — Rate-limit cost jumped 10–20x for Plus users** *(15 comments, 20 👍)*  
   A critical billing/infrastructure issue. Users burning through their 5-hour budget in 2–3 prompts is creating a chilling effect on tool adoption.

3. **[#28982](https://github.com/openai/codex/issues/28982) — Windows sandbox helper fails with missing module** *(17 comments, 7 👍)*  
   A blocker for Windows users updating to `26.616.3309.0`. The native sandbox setup helper fails on launch, reinforcing the feeling that Windows builds are lagging in stability.

4. **[#29000](https://github.com/openai/codex/issues/29000) / [#29047](https://github.com/openai/codex/issues/29047) / [#28893](https://github.com/openai/codex/issues/28893) — SIGTRAP V8 crash on Intel macOS (v0.141.0)** *(Multiple reports)*  
   A hard crash inside the V8 Isolate during tool invocation. The community must either downgrade to `v0.140.0` or wait for the current alpha fix cycle. A top-priority blocker.

5. **[#28224](https://github.com/openai/codex/issues/28224) — SQLite feedback logs writing ~640 TB/year** *(8 comments, 14 👍)*  
   A severe SSD endurance concern. Heavy CLI users are discovering that local logging is aggressively wearing down their drives. A silent, urgent hardware health issue.

6. **[#13117](https://github.com/openai/codex/issues/13117) — Permission prompt for every file read (Windows)** *(16 comments, 10 👍)*  
   A recurring regression where the agent sandbox loses its "remember my choice" state. Long-standing community frustration that appears every few months.

7. **[#17257](https://github.com/openai/codex/issues/17257) — Extra High memory leak** *(9 comments, 11 👍)*  
   A persistent memory leak on the highest performance setting. Power users frequently report OOM scenarios during long sessions.

8. **[#20947](https://github.com/openai/codex/issues/20947) — `hatch-pet` skill broken** *(3 comments, 5 👍)*  
   The skill gets stuck with "Stream disconnected..." errors. Highlights general fragility in the skill/plugin runtime and streaming infra.

9. **[#9046](https://github.com/openai/codex/issues/9046) — Context window exhaustion** *(34 comments)*  
   The most-commented issue persists. Users are confused about best practices for clearing history, highlighting the need for better context management UX.

10. **[#29163](https://github.com/openai/codex/issues/29163) — Projects shared across user accounts on the same PC** *(3 comments)*  
    A potential security/data isolation failure in the desktop client. Projects leak between Windows user profiles on shared machines.

### 4. Key PR Progress

1. **[#29166](https://github.com/openai/codex/pull/29166) / [#29164](https://github.com/openai/codex/pull/29164) / [#29158](https://github.com/openai/codex/pull/29158) — PathUri lexical overhaul (anp-oai)**  
   A massive push for cross-platform path correctness. Preserves raw patch paths, adds lexical helpers for POSIX/Windows/UNC, and removes legacy deserialization. Directly addresses dozens of sandbox and WSL regressions.

2. **[#29162](https://github.com/openai/codex/pull/29162) / [#29149](https://github.com/openai/codex/pull/29149) — Hermetic Windows Rust builds (anp-oai)**  
   Removes MSVC fallback from Windows Bazel actions and pins the build to gnullvm/LLVM. A critical infrastructure investment for consistent Windows CI/CD.

3. **[#29165](https://github.com/openai/codex/pull/29165) — Decouple plugin manifest resource resolution (anp-oai)**  
   A necessary abstraction for executor-owned plugin resources. Prepares the plugin system for more flexible cross-platform deployments without breaking existing host paths.

4. **[#29108](https://github.com/openai/codex/pull/29108) — Carry sandbox intent to remote exec servers (jif-oai)**  
   Enables portable sandbox intent for remote agent execution, paving the way for safe enterprise remote runners.

5. **[#28787](https://github.com/openai/codex/pull/28787) — Transport-neutral session runtime (cconger)**  
   A major architectural cleanup. Splits session business logic from transport concerns. Targets the "zombie session" RAM growth and session hydration failures.

6. **[#29155](https://github.com/openai/codex/pull/29155) — Expose service tier & reasoning effort in OTEL (daniel-oai)**  
   Driven by an NVIDIA request for telemetry. Adds observability for Fast mode vs reasoning effort to support enterprise compliance monitoring.

7. **[#29150](https://github.com/openai/codex/pull/29150) — Remove bundled imagegen system skill (daniel-oai)**  
   Moves image generation to an installable, removable plugin. Shrinks the core runtime and enables faster iteration on the skill ecosystem.

8. **[#26707](https://github.com/openai/codex/pull/26707) — Shared auth system proxy contract (canvrno-oai)**  
   Improves network resilience for developers behind corporate proxies, moving Codex-owned HTTP clients through a route-aware boundary.

9. **[#29082](https://github.com/openai/codex/pull/29082) — Connector skills feature toggle (william-oai)**  
   Adds the narrow runtime control needed for A/B testing connector-provided skills without removing connector apps or MCP tools.

10. **[#26009](https://github.com/openai/codex/pull/26009) — ThreadCatalog metadata subscriptions (btraut-oai)**  
    Solves a frustrating UX gap: sidebar clients can now track activity across all threads via lightweight metadata subscriptions instead of expensive polling.

### 5. Feature Request Trends

- **Transparent Cost & Rate-Limit Controls**: The 10–20x cost spike ([#28879](https://github.com/openai/codex/issues/28879)) has amplified calls for per-prompt cost previews, usage budgets, and clearer billing telemetry.
- **Stable Long-Running Sessions**: Users want automatic context compaction, transparent reasoning-level persistence, and no degradation of model quality after hours of agentic work ([#26876](https://github.com/openai/codex/issues/26876)).
- **Windows Parity as a Hard Requirement**: A constant stream of sandbox, WSL, and path-handling bugs on Windows ([#28982](https://github.com/openai/codex/issues/28982), [#16815](https://github.com/openai/codex/issues/16815)) shows the community sees "fix the Windows experience" as the top priority before further feature development.
- **First-Class Plugin Ecosystem**: The unbundling of image generation ([#29150](https://github.com/openai/codex/pull/29150)) and connector skill toggles ([#29082](https://github.com/openai/codex/pull/29082)) align with community demand for a reliable, installable skill marketplace, but execution stability remains a blocker.

### 6. Developer Pain Points

- **Windows Desktop Instability Crisis**: A single dedicated reporter (SocialK) has filed nearly a dozen critical bugs: crashes on launch, session hydration failures, and RAM saturation ([#27979](https://github.com/openai/codex/issues/27979), [#27175](https://github.com/openai/codex/issues/27175), [#28980](https://github.com/openai/codex/issues/28980)). This signals a systemic quality gap in the Windows client QA pipeline.
- **SSD as a Consumable**: The SQLite logging bug ([#28224](https://github.com/openai/codex/issues/28224)) treats user drive endurance as infinite. For heavy CLI users, this represents a hardware damage risk.
- **Recurring Permission Regressions**: Sandbox permissions breaking "again" ([#13117](https://github.com/openai/codex/issues/13117)) against a predictable workflow pattern indicates weak regression testing during sandbox refactors.
- **Hard Blocker on Intel Macs**: The V8 SIGTRAP ([#29000](https://github.com/openai/codex/issues/29000)) is a hard wall. There is no workaround besides downgrading or risking the bleeding-edge alpha. Productivity stops for users on Intel Mac hardware.
- **Cost Uncertainty Cripples Adoption**: The 10–20x rate limit drain ([#28879](https://github.com/openai/codex/issues/28879)) creates a chilling effect where users are afraid to use the tool. A stable, predictable billing model is the unspoken critical requirement behind this signal.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-20

> *Generated from github.com/google-gemini/gemini-cli*

## Today's Highlights

Today’s nightly release pipeline failed (v0.49.0-nightly), blocking the latest builds for early adopters. A significant fix for capping pending tool responses is finally making its way through review to address longstanding agent hang issues, while critical security patches for `shell-quote` and `vitest` CVEs are queued. The community continues to feel the pain of agents getting stuck on simple shell commands, with two separate P1 bugs still actively triaged.

## Releases

No new releases in the past 24 hours.

## Hot Issues

The following 10 issues represent the most impactful or active discussions in the community today.

**1. Nightly Release Failed** [`#28056`](https://github.com/google-gemini/gemini-cli/issues/28056)
*P1 | release-failure, bug*
The nightly build pipeline for v0.49.0-nightly failed today due to a missing trailing slash in the npm registry URL configuration. This blocks access to cutting-edge builds until the CI fix (already posted as PR #28038) lands.

**2. Shell command hangs with "Waiting input"** [`#25166`](https://github.com/google-gemini/gemini-cli/issues/25166)
*P1 | effort/medium, bug (3 👍)*
After executing trivial shell commands (e.g., `ls`, `mkdir`), Gemini frequently hangs, keeping the shell tool active and displaying "Awaiting user input" even though the command has completed. This is a top disruptor for agent-driven workflows.

**3. Generalist agent hangs forever** [`#21409`](https://github.com/google-gemini/gemini-cli/issues/21409)
*P1 | bug (8 👍)*
The most upvoted issue this week. When the main agent defers to the Generalist sub-agent, it hangs indefinitely—even for trivial tasks like folder creation. The existing workaround is to instruct the model to avoid sub-agents entirely.

**4. Subagent MAX_TURNS falsely reports success** [`#22323`](https://github.com/google-gemini/gemini-cli/issues/22323)
*P1 | bug (2 👍)*
When a subagent hits its maximum turn limit, it reports `status: "success"` and `Termination Reason: "GOAL"`, silently swallowing the interruption. This misleads the orchestrating agent and the user into thinking analysis completed when it did not.

**5. get-shit-done output hook crashes** [`#22186`](https://github.com/google-gemini/gemini-cli/issues/22186)
*P1 | bug*
A reproducible crash in the "get-shit-done" workflow that fires when printing the final user summary. The crash interrupts one of the tool’s most popular features at the moment of delivery.

**6. Browser subagent fails on Wayland** [`#21983`](https://github.com/google-gemini/gemini-cli/issues/21983)
*P1 | bug (1 👍)*
Linux users running Wayland are completely blocked from using the Browser Agent. The agent reports a "GOAL" termination reason but silently fails to interact with the browser.

**7. 400 error with > 128 tools** [`#24246`](https://github.com/google-gemini/gemini-cli/issues/24246)
*P2 | bug*
When enough MCP servers or native tools are enabled, the total tool count exceeds 128, causing a 400 error from the API. Users expect smarter tool scoping or filtering rather than a hard failure.

**8. Auto Memory runs before transcript redaction** [`#26525`](https://github.com/google-gemini/gemini-cli/issues/26525)
*P2 | security, bug*
A significant privacy concern: Auto Memory reads local transcripts and sends them to the extraction agent *before* prompting for secret redaction. Users are pushing for deterministic redation before any context is sent.

**9. Sub-agents running without permission (v0.33.0 regression)** [`#22093`](https://github.com/google-gemini/gemini-cli/issues/22093)
*P2 | bug*
A user reports that upgrading to v0.33.0 caused sub-agents to run despite "agents" being set to disabled in all configurations. This violates explicit user consent and configuration trust.

**10. Model scatters temp scripts across filesystem** [`#23571`](https://github.com/google-gemini/gemini-cli/issues/23571)
*P2 | bug*
The model frequently creates temporary edit scripts in random directories when shell execution is restricted. This creates significant cleanup overhead for developers maintaining clean git histories.

## Key PR Progress

**1. Preserve dollar sequences in prompt templates** [`#28055`](https://github.com/google-gemini/gemini-cli/pull/28055)
*area/agent | size/s, open*
Fixes `applySubstitutions()` corrupting content containing `$` sequences (e.g., `$$`, `$'`, `$&`) in skill, sub-agent, or tool descriptions. Essential for MCP tools that use shell-like syntax.

**2. Cap pending tool responses** [`#27870`](https://github.com/google-gemini/gemini-cli/pull/27870)
*P1 | area/agent, size/m, open*
Prevents agents from hanging by capping very large tool results in `functionResponse`. A direct fix for the deep-seated agent hang issues tracked across multiple closed/open issues.

**3. Critical CVE patches: shell-quote & vitest** [`#27856`](https://github.com/google-gemini/gemini-cli/pull/27856) [`#27857`](https://github.com/google-gemini/gemini-cli/pull/27857)
*CRITICAL | need-issue, open*
Security bots patching CVE-2026-9277 (shell-quote) and CVE-2026-47429 (vitest). Both are critical severity and need fast merging to maintain supply chain integrity.

**4. Fix Jupyter Notebook and JSON corruption in write_file** [`#28000`](https://github.com/google-gemini/gemini-cli/pull/28000)
*size/m, open*
A critical fix for a bug causing `write_file` to silently corrupt `.ipynb` and JSON files, rendering them unparseable. This has been a significant data-loss vector for data science users.

**5. Defensive path resolution for @-prefixed files** [`#28053`](https://github.com/google-gemini/gemini-cli/pull/28053)
*size/xl, open*
Fixes "File not found" errors when the model passes paths starting with `@` (e.g., `@policies/new-policies.txt`). A comprehensive fix covering `read_file`, `replace`, and `write_file`.

**6. Fix MCP OAuth refresh with auto-discovered servers** [`#27889`](https://github.com/google-gemini/gemini-cli/pull/27889)
*P1 | area/agent, size/m, open*
The CLI persists OAuth client IDs from auto-discovered MCP servers but fails to reuse them during token refresh. This fix resolves broken connections to discovered MCP endpoints.

**7. Native drag-and-drop & clipboard image pasting** [`#27859`](https://github.com/google-gemini/gemini-cli/pull/27859)
*P3 | area/core, size/m, open*
Introduces first-class terminal drag-and-drop and Ctrl+V/Cmd+V image pasting. This bridges a major feature gap with GUI models and enables visual multimodal workflows directly in the CLI.

**8. Add eval:inventory CLI command** [`#28009`](https://github.com/google-gemini/gemini-cli/pull/28009)
*size/l, closed*
Adds `npm run eval:inventory` for listing all defined evaluation cases, grouped by policy area. Improves the developer workflow for managing the growing behavioral eval suite.

**9. Fix skills being silently invisible on single-line frontmatter** [`#28042`](https://github.com/google-gemini/gemini-cli/pull/28042)
*P2 | area/extensions, size/m, open*
Fixes skill discovery failing when a SKILL.md description field immediately precedes the closing `---` with no blank line. Affected skills simply didn't appear in `/skills list`.

**10. CI hardening: fork artifact poisoning fix** [`#27753`](https://github.com/google-gemini/gemini-cli/pull/27753)
*P1 | area/security, size/s, open*
Fixes a `workflow_run` artifact poisoning vulnerability where a fork PR could execute attacker-controlled code with repository secrets in the E2E pipeline.

## Feature Request Trends

**Agent Self-Awareness & Safety Guards** (#21432, #22672, #22232)
A growing demand for agents that understand their own mechanics (hotkeys, configuration, CLI flags) and enforce safety boundaries around destructive actions (`git reset --force`, database mutations). The community wants built-in guardrails rather than relying on the model to "just know."

**AST-Aware Codebase Understanding** (#22745, #22746)
Maintainers and power users are pushing for integrating AST-aware tools (tilth, glyph) for file reading, search, and codebase mapping. The goal is to reduce token waste, eliminate misaligned reads, and improve navigation accuracy for the `codebase_investigator` sub-agent.

**Robust Evaluation Infrastructure** (#24353, #23166)
The rapid growth of behavioral evals (76+ tests) is straining the framework. Requests include persistent eval suites, an eval inventory command (now landing in #28009), and stable baseline tests that don't "bleed" or require disabling.

**Memory System Maturation** (#26522, #26523, #26516)
The Auto Memory feature is undergoing heavy iteration. Requests center on signal quality: stop retrying low-signal sessions, quarantine malformed patches instead of silently skipping them, and move secret redaction before transcript loading rather than after.

**Remote Agents & Background Operations** (#20303)
A formal Epic exists for Sprint 2 of Remote Agents, targeting task-level authentication, first-party agent support, and background processing. This suggests a major shift toward persistent, server-side agent capabilities.

## Developer Pain Points

**Agent Hangs** — The dominant pain point. Agents routinely get stuck on interactive prompts (#22465), finished shell commands (#25166), and sub-agent delegation (#21409). Workarounds exist (disabling sub-agents, avoiding interactive commands) but none are root-cause fixes.

**Sub-Agent Mismanagement** — Sub-agents are a source of constant friction. They fire without user consent (#22093), lie about their own failure states (#22323), ignore settings overrides (#22267), and fail to use user-defined skills or tools (#21968).

**Destructive & Messy Behavior** — The model's tendency to scatter temporary scripts across filesystems (#23571) and issue unsafe git commands (#22672) forces users into manual cleanup and reduces trust in autonomous operation.

**Privacy & Trust Gaps** — The Auto Memory system sends transcript content before redaction (#26525) and keeps retrying low-value sessions (#26522). Combined, these issues erode confidence in the tool's background processing and data handling.

**Platform Inconsistency** — Linux (Wayland) users cannot use the Browser Agent (#21983). Terminal rendering bugs remain active (resize flicker #21924, Thai/Lao grapheme corruption #25385, external editor corruption #24935). These degrade the experience for a significant portion of the developer audience.

**Tool Configuration Fragility** — MCP OAuth tokens break on auto-discovered servers (#27889), >128 tools cause a hard API 400 (#24246), and path resolution is brittle around special characters (`@`, `$$`) (#28053, #28055).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

```markdown
# GitHub Copilot CLI Community Digest — 2026-06-20

## 1. Today's Highlights
The v1.0.64-1 patch landed with an experimental `--worktree` flag for isolated session environments, a `/branch` alias for `/fork`, and tab completion for `/agent n`. Meanwhile, the community is actively filing detailed usability reports: recent issues highlight silent context compaction (#3867), inaccessible "thinking" text on dark terminals (#3866), and app hangs during session navigation (#3868). Platform-specific regressions on the Windows MCP server (#3455) and Alpine auto-updates (#3696) remain open points of friction.

## 2. Releases
- **v1.0.64-1** ([Release](https://github.com/github/copilot-cli/releases/tag/v1.0.64-1))
  - **Added:** `/branch` alias for `/fork`, matching Claude Code command naming.
  - **Experimental:** `--worktree`/`-w` flag (enable with `/experimental`) to create/reuse a git worktree under `<repo>.worktrees/`.
  - **Added:** Tab completion for `/agent n`.

## 3. Hot Issues
_Selected for their high engagement, severity, recency, and representation of broader trends._

1. **[#1665: Support Plugins Scoped to Project/Repository [CLOSED]**](https://github.com/github/copilot-cli/issues/1665)
   - 17 👍. This highly requested change would allow teams to ship `.copilot` plugin configs per-repo instead of relying on global user installs. Recently closed, signaling likely feature delivery.

2. **[#3867: No Context Window Visibility or Compaction Notification [OPEN]**](https://github.com/github/copilot-cli/issues/3867)
   - Developers are demanding a heads-up display for token usage. Silent context compaction causes unpredictable model behavior, eroding trust in long sessions.

3. **[#3866: Thinking/Reasoning Text Unreadable on Dark Backgrounds [OPEN]**](https://github.com/github/copilot-cli/issues/3866)
   - A hardcoded dark gray foreground for the "Thinking…" animation makes it invisible on dark themes. A basic accessibility regression reported in v1.0.64.

4. **[#3868: App Hangs When Right-Clicking a Session [OPEN]**](https://github.com/github/copilot-cli/issues/3868)
   - Introduces an unresponsive state during multi-session management. A critical stability bug for power users juggling several chat/session windows.

5. **[#3869: /ask Feature Cramped Text Box [OPEN]**](https://github.com/github/copilot-cli/issues/3869)
   - The `/ask` output pane is described as "un-useable" because it only shows a few lines. Requests for resizable panes or pagination to handle code-heavy responses.

6. **[#3455: github-mcp-server "fetch failed" on Windows [OPEN]**](https://github.com/github/copilot-cli/issues/3455)
   - A regression in v1.0.51 broke the MCP server connectivity on Windows. Blocks a core integration workflow for a significant platform segment.

7. **[#3371: CLI Silently Hangs on Stalled HTTPS Sockets [OPEN]**](https://github.com/github/copilot-cli/issues/3371)
   - The terminal can freeze indefinitely with no log output (no `events.jsonl`, no TUI feedback). A silent failure with catastrophic user experience.

8. **[#2893: preToolUse Hooks Bypassed Under Parallel Calls [OPEN]**](https://github.com/github/copilot-cli/issues/2893)
   - When `timeoutSec` triggers, the subprocess persists, and the CLI allows the tool execution anyway. Creates a silent security/auditing gap in the plugin system.

9. **[#731: Z Shell / direnv Session ID Bug [CLOSED]**](https://github.com/github/copilot-cli/issues/731)
   - 14 👍. Long-standing incompatibility with `direnv` and Nix environments. Resolved, which unblocks many power users relying on environment-oriented shells.

10. **[#3864: Plugin cache_path Absolute Path Breaks Docker [OPEN]**](https://github.com/github/copilot-cli/issues/3864)
    - `cache_path` in `config.json` is hardcoded to the install-time `$HOME`. When `~/.copilot` is volume-mounted in Docker (where `$HOME` differs), plugin hooks silently never fire.

## 4. Key PR Progress
- **No pull requests were updated in the last 24 hours.** Maintainers appear heavily focused on triaging the wave of UX and regression issues from the v1.0.64 release and the ongoing MCP integration support.

## 5. Feature Request Trends
- **Project-Scoped Configuration:** There is a strong push for plugins and configuration to live inside the repository rather than strictly in `~/.copilot`. Issue #1665 (recently closed) is the primary signal here.
- **Ambient Visibility & Controls:** Users want a "heads-up display" for context window stats (#3867), better text rendering for dense responses (#3869), tighter accessibility compliance (#3866), and AI-invocable navigation commands like `/cd` (#3865).
- **Worktree & Isolation:** The experimental `--worktree` flag is a hit, and the community is already requesting deeper integration (e.g., auto-updating the status bar `pwd` when switching worktrees via the agent).

## 6. Developer Pain Points
- **Silence is the #1 Enemy:** The most common theme across open bugs is the CLI failing *silently*. Hooks bypassed without warning (#2893), sockets stalled with no logs (#3371), context compacted without notice (#3867), and fleet mode lagging by 50 minutes (#1901). Developers need deterministic, verbose feedback.
- **Platform Fragility Continues to Bite:** Edge cases in non-standard environments are persistent friction points: Alpine musl auto-updates downloading the wrong binary (#3696), Windows MCP networking regressions (#3455), Docker absolute path hardcoding (#3864), and Zsh/direnv environment variable pollution (#731).
- **Session Lifecycle Management:** Features like updating while resuming a session (#3821) and hanging on session right-click (#3868) suggest the multi-session architecture is being pushed hard by complex workflows and needs more rigorous lifecycle testing.

```

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-20**

---

### 1. Today’s Highlights
Today’s digest is defined by a single, targeted fix. The only repository activity is **PR #2463**, which resolves a critical networking bug where the CLI ignored system proxy settings. No new releases or issue threads surfaced in the last 24 hours, indicating a quiet consolidation period for the team and community.

---

### 2. Releases
*No new releases were published in the last 24 hours.*

---

### 3. Hot Issues
*The issue tracker recorded zero updates or new reports for this period (Total: 0 items).*

Without active threads, there are no community reactions or trending topics to surface from today’s window. This likely reflects a natural pause after prior discussion cycles or an internal sprint focus.

---

### 4. Key PR Progress

Only one PR was updated or created in the last 24 hours:

- **#2463 [OPEN] fix: respect system proxy settings in FetchURL**
    - **Author:** `itxaiohanglover`
    - **Link:** [View Pull Request](https://github.com/MoonshotAI/kimi-cli/pull/2463)
    - **Details:** The `FetchURL` module was found to ignore standard `HTTP_PROXY` and `HTTPS_PROXY` environment variables because Python’s `aiohttp` library does not read them by default. This caused `Connection reset by peer` failures in proxied environments (corporate firewalls, VPNs, etc.).
    - **Why it matters:** This is a high-value fix for enterprise and professional developers. Removing the need for manual proxy configuration significantly lowers the friction for adopting Kimi CLI in restricted network environments.
    - **Status:** Open, filed 2026-06-19.

---

### 5. Feature Request Trends
*Insufficient data to analyze trends — no new issues were created or updated in the last 24 hours.*

From the context of today’s sole PR, the underlying community desire is clear: **seamless environment integration**. Developers expect the CLI to inherit system-level settings (proxies, certs, auth tokens) without manual intervention.

---

### 6. Developer Pain Points

- **Automatic Proxy Detection (PR #2463):** The single piece of activity highlights a recurring frustration: networking tools that fail to respect standard OS environment variables. Users behind corporate proxies experience hard failures (`Connection reset by peer`), creating an immediate trust barrier with new adopters.
- **Network Hardening:** This patch underscores an implicit demand for the CLI networking layer to deeply integrate with host OS configuration (env vars, system proxy, certificate stores). Enterprise users particularly feel this friction, making it a strong candidate for ongoing hardening.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

**OpenCode Community Digest – 2026-06-20**

## 1. Today's Highlights
This week is strongly defined by the push for MCP specification alignment, with three stacked PRs (#32478, #32936, #32943) incrementally adding resource subscriptions, templates, and change-event support. On the stability front, a severe 100% CPU hang (#32965) and continued memory issues (#20695) are consuming community attention. Feature development remains active, highlighted by a new "Ultra Mode" autonomous agent (#33042) and long-requested Android/Termux platform support (#33010).

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Hot Issues
1. **[#20695 – Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** (98 comments, 71 👍)  
   Centralized report hub for memory bloat. The team is requesting heap snapshots and explicitly cautioning against LLM-generated debugging suggestions.
2. **[#2242 – Agent Sandboxing](https://github.com/anomalyco/opencode/issues/2242)** (74 comments, 55 👍)  
   Users want native restrictions on agent terminal and file access. The discussion frequently compares Codex CLI's macOS seatbelt approach to OpenCode's current lack of isolation.
3. **[#988 – MCP Remote OAuth](https://github.com/anomalyco/opencode/issues/988)** (39 comments, 95 👍)  
   The top-voted open issue. Proposes an OAuth 2.1 flow for remote MCP servers to eliminate manual secret/token management in configs.
4. **[#28567 – Full MCP Client Capabilities](https://github.com/anomalyco/opencode/issues/28567)** (17 comments, 24 👍)  
   OpenCode's MCP client is behind the official spec. Requests for resource subscriptions, prompts, and logging to reach full parity.
5. **[#16017 – Go Plan Usage API](https://github.com/anomalyco/opencode/issues/16017)** (19 comments, 70 👍)  
   Users want a public REST endpoint to query rolling/weekly/monthly usage data, currently only visible in the dashboard UI.
6. **[#32965 – 100% CPU Spiral](https://github.com/anomalyco/opencode/issues/32965)** (4 comments)  
   Critical hang where the main thread pins a core at 100% after a model step with no logs or I/O, unresponsive even to SIGTERM.
7. **[#32444 – GLM-5.2 Thinking Variants Excluded](https://github.com/anomalyco/opencode/issues/32444)** (6 comments, 13 👍)  
   A hardcoded filter in `variants()` blocks all models with "glm" in the ID, preventing users from accessing High/Max thinking-effort levels.
8. **[#32010 – Background Agent Wake Silently Dropped](https://github.com/anomalyco/opencode/issues/32010)** (5 comments)  
   `promptAsync` messages persist to the database but the session loop is never scheduled, silently swallowing wake calls for background agents.
9. **[#31815 – `opencode web` Fails in Containers](https://github.com/anomalyco/opencode/issues/31815)** (4 comments, 4 👍)  
   Lacks a graceful fallback when `xdg-open` is absent in Docker/Podman, printing an opaque ENOENT stack trace.
10. **[#24817 – Ctrl+Z Suspends Instead of Undo (Linux)](https://github.com/anomalyco/opencode/issues/24817)** (6 comments, 3 👍)  
    Standard Linux terminal behavior catches Ctrl+Z as `SIGTSTP`, suspending the process rather than performing an undo in the text input.

## 4. Key PR Progress
1. **[#32478 – MCP Resource List Change Events](https://github.com/anomalyco/opencode/pull/32478)** (Nomadcxx)  
   The first slice of full MCP subscription support. OpenCode now registers for and handles `resources/list` change events from servers that advertise them.
2. **[#32936 – MCP Resource Subscriptions](https://github.com/anomalyco/opencode/pull/32936)** (Nomadcxx)  
   Adds `subscribe`/`unsubscribe` actions, allowing real-time updates to resources without polling.
3. **[#32943 – MCP Templates & Completion](https://github.com/anomalyco/opencode/pull/32943)** (Nomadcxx)  
   Implements `resources/templates/list` and URI completion support, closing a significant gap with the MCP specification.
4. **[#33042 – Ultra Mode Autonomous Agent](https://github.com/anomalyco/opencode/pull/33042)** (woppa518)  
   A new agent type with a hardcoded state machine for autonomous plan→build→verify→loop workflows, featuring per-phase tool filtering.
5. **[#32089 – Proper Doom Loop Detection](https://github.com/anomalyco/opencode/pull/32089)** (JustSidus)  
   Fixes detection scope so it evaluates across the entire conversation, not just the current assistant message, preventing repeated tool call spirals.
6. **[#8535 – Bi-Directional Cursor Pagination](https://github.com/anomalyco/opencode/pull/8535)** (CasualDeveloper)  
   Implements cursor-based pagination for session messages across the full stack: server, application, TUI, API, and share views.
7. **[#33010 – Android/Termux Support](https://github.com/anomalyco/opencode/pull/33010)** (Ue1i7on)  
   Adds platform mapping and postinstall scripts for Termux (Android ARM64), resolving four open feature requests for mobile support.
8. **[#28921 – ACP Permission Context](https://github.com/anomalyco/opencode/pull/28921)** (bcdady)  
   Improves security visibility by including the full shell command and file paths in the ACP permission prompt.
9. **[#30211 – Fix Provider Config Precedence](https://github.com/anomalyco/opencode/pull/30211)** (shlroland)  
   Resolves a regression where plugin `models()` hooks could override explicit user provider configurations.
10. **[#33019 – Inline Skill Picker](https://github.com/anomalyco/opencode/pull/33019)** (alexx855)  
    A minimalist TUI feature: typing `$` opens an inline dialog to search, load, and unload skills without leaving the chat.

## 5. Feature Request Trends
- **MCP Specification Alignment**  
  The dominant theme. Top issues request full spec compliance: OAuth 2.1 (#988), resource subscriptions (#28567), and proper template/completion handling. The stacked PRs (#32478, #32936, #32943) indicate core team investment here.
- **Agent Autonomy & Safety**  
  Contradictory but coexisting pushes for more autonomous agents (**Ultra Mode**, self-correcting loops) and stronger security boundaries (**sandboxing**, permission context in prompts).
- **Platform & Provider Expansion**  
  Users actively seek first-class support outside the standard macOS/Linux desktop: Android/Termux (#33010), Docker containers (#31815), and exotic providers like LiteLLM and GLM.
- **Usage Transparency**  
  Growing demand for API-level access to plan usage (#16017) and proper introspection into agent reasoning (thinking-effort levels, `reasoning_content`).

## 6. Developer Pain Points
- **Stability Regressions**  
  High-severity issues are pervasive: 100% CPU loops (#32965), sub-agents hanging indefinitely (#33028), and SIGTRAP crashes on Apple Silicon (#32694) point to core runtime fragility.
- **Integration Friction**  
  Established workflows like WSL2/VS Code context syncing (#29570) break without warning. Database migration errors block app launch entirely (#31119).
- **Data Integrity**  
  Orphaned public shares that cannot be unshared (#32062), disappearing chat messages (#7380), and stale snapshot locks (#29413) undermine trust in session persistence.
- **Missing Platform UX**  
  Linux users continue to deal with elementary terminal issues (Ctrl+Z suspending the process, no `xdg-open` fallback) and lack of official Android support.
- **Opaque Provider Behavior**  
  Hardcoded model filters (GLM exclusion in `variants()`), silent `promptAsync` drops, and confusing plugin config precedence create a debugging maze for power users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest: June 20, 2026

**Repository:** `github.com/earendil-works/pi` (aliased as `badlogic/pi-mono`)

---

## 1. Today's Highlights

A packed 24 hours for the Pi ecosystem. The release of **v0.79.8** introduces selective base entry points for the SDK, a clear step toward production-grade tree-shaking. On the community side, a **critical data-loss bug** in the `edit` tool’s fuzzy matching ([#5899](https://github.com/earendil-works/pi/issues/5899)) was identified and patched within hours ([#5898](https://github.com/earendil-works/pi/pull/5898)), though the long-running streaming scroll bug ([#5825](https://github.com/earendil-works/pi/issues/5825)) continues to generate discussion. New provider integration work is flowing steadily, with contributions for Amazon Bedrock Mantle ([#5509](https://github.com/earendil-works/pi/pull/5509)) and OpenRouter Fusion ([#5866](https://github.com/earendil-works/pi/pull/5866)).

---

## 2. Releases

**v0.79.8** was published in the last 24 hours. It ships a single, impactful new feature:

- **Selective Provider Base Entry Points** – SDK users can now import `@earendil-works/pi-ai/base` and `@earendil-works/pi-agent-core/base` with explicit provider registration. This allows bundlers (webpack, esbuild, etc.) to tree-shake unused provider transports, dramatically reducing bundle sizes for embedded Pi agents.

---

## 3. Hot Issues

*10 noteworthy items from the top 30 by comment count, covering bugs, feature gaps, and community friction.*

1.  **[#5825](https://github.com/earendil-works/pi/issues/5825) — Streaming markdown forces scroll to bottom** (24 comments)
    *The most active thread this week.* Enabling `clear on shrink` causes aggressive auto-scrolling. Users reading slower than the agent writes are forced to fight the UI. PR [#5846](https://github.com/earendil-works/pi/pull/5846) attempts a fix for code fenced rendering but the core issue remains open.

2.  **[#5897](https://github.com/earendil-works/pi/issues/5897) — Unavailable models offered in Copilot integration** (9 comments)
    *Significant onboarding friction.* GitHub Copilot subscribers are shown unusable legacy models (e.g., GPT-4 nano, older Opus). Indicates a misalignment between the Copilot model list and Pi’s model compatibility.

3.  **[#5899](https://github.com/earendil-works/pi/issues/5899) — Edit tool fuzzy match silently rewrites the whole file** (2 comments)
    *Critical data integrity bug.* When `oldText` differs from the file (trailing whitespace, smart quotes), the tool rewrites the entire file in normalized form. Fixed by [#5898](https://github.com/earendil-works/pi/pull/5898), but the severity generated immediate community concern.

4.  **[#5673](https://github.com/earendil-works/pi/issues/5673) — Add "vllm-deepseek" thinking format for DeepSeek models behind vLLM proxies** (4 comments)
    *Growing self-hosted demand.* The community wants a `thinkingFormat` value that passes `chat_template_kwargs: { thinking: true }` for DeepSeek-V3.x compatibility with vLLM.

5.  **[#5804](https://github.com/earendil-works/pi/issues/5804) — Fast Sessions (SQLite session storage)** (2 comments, +1 👍)
    *A highly anticipated architectural shift.* Users are pushing for SQLite-based session storage to speed up load/search times and move beyond the JSONL file format for session persistence.

6.  **[#5901](https://github.com/earendil-works/pi/issues/5901) — Durable HITL tool-call interrupts** (2 comments)
    *Enterprise SDK signal.* Headless SDK users explicitly requested durable human-in-the-loop approval for tool calls, directly comparing against LangGraph’s HITL middleware.

7.  **[#5907](https://github.com/earendil-works/pi/issues/5907) — `pi.setActiveTools` cannot hide built-in `read` tool** (1 comment)
    *SDK control limitation.* The `read` tool cannot be disabled via the SDK API, forcing agents to avoid reading large files that crash context. Points to a need for a stricter tool permission model.

8.  **[#5871](https://github.com/earendil-works/pi/issues/5871) — Anthropic OAuth-token detection is hardcoded to `sk-ant-oat`** (2 comments)
    *Configuration rigidity.* The provider logic uses a hardcoded substring check. Users with custom OAuth proxies or non-standard credential formats cannot configure this, requesting it be made declarative in `models.json`.

9.  **[#5904](https://github.com/earendil-works/pi/issues/5904) — Bash tool `cwd` parameter is silently dropped** (1 comment)
    *Silent failure mode.* A model attempting to set `cwd` is ignored without error. If the session working directory is deleted, the model has no escape path, leading to workflow deadlocks.

10. **[#5909](https://github.com/earendil-works/pi/issues/5909) — Coalesce rapid thinking_level_change entries to avoid session bloat** (1 comment)
    *Performance sharp edge.* Rapidly cycling thinking levels floods the JSONL session file. These hidden entries don’t get compacted, making the session tree sluggish.

---

## 4. Key PR Progress

*The data window shows 7 pull requests. All are covered below.*

1.  **[#5898](https://github.com/earendil-works/pi/pull/5898) — fix(coding-agent): preserve untouched content in fuzzy edit matches**
    *Critical fix for [#5899](https://github.com/earendil-works/pi/issues/5899).* Ensures only the targeted lines are changed during fuzzy matching. The rapid merge of this PR highlights the team’s commitment to data integrity.

2.  **[#5846](https://github.com/earendil-works/pi/pull/5846) — fix(tui): stabilize streaming code fence rendering**
    *Targets the top-voted UX bug [#5825](https://github.com/earendil-works/pi/issues/5825).* Focuses on stabilizing TUI rendering during streaming to prevent scroll jumps. Currently open.

3.  **[#5900](https://github.com/earendil-works/pi/pull/5900) — feat(coding-agent): emit OSC 9998/9999 for freecode-web adapter**
    *Web integration bridge.* Subscribes to `AgentSession` events and emits standard OSC escape codes so web-based PTY parsers can display accurate status, cost, and context telemetry.

4.  **[#5509](https://github.com/earendil-works/pi/pull/5509) — feat: Add Amazon Bedrock Mantle OpenAI Responses provider**
    *Major new provider.* Models the existing Azure Responses pattern to hook into AWS Bedrock Mantle, bringing GPT 5.5 and 5.4 to Pi via AWS.

5.  **[#5866](https://github.com/earendil-works/pi/pull/5866) — feat(ai): add OpenRouter Fusion alias**
    *Router flexibility.* Adds `openrouter/fusion` as a synthetic router alias (matching the existing `auto` pattern), exposing OpenRouter’s model fusion routing capability.

6.  **[#5356](https://github.com/earendil-works/pi/pull/5356) — docs: add containerization guide and Gondolin example**
    *Deployment documentation.* A comprehensive guide on containerizing Pi, complete with a practical example deployment ("Gondolin").

7.  **[#4794](https://github.com/earendil-works/pi/pull/4794) — chore: run pi-test through tsx**
    *Build tooling fix.* Switches the test runner to use `tsx`, ensuring workspace package imports resolve correctly through `package.json` exports during testing.

---

## 5. Feature Request Trends

Distilling the last 24 hours of community requests reveals several strong signal axes:

- **Provider Integration Depth**: Users are pushing beyond basic provider support. Demand is high for **custom thinking formats** (vLLM DeepSeek [#5673](https://github.com/earendil-works/pi/issues/5673), max thinking levels [#5831](https://github.com/earendil-works/pi/issues/5831)), **prompt caching** (Mistral [#5854](https://github.com/earendil-works/pi/issues/5854)), **schema compatibility** (Moonshot/Kimi [#5822](https://github.com/earendil-works/pi/issues/5822)), and **flexible authentication** (Codex bearer tokens [#5152](https://github.com/earendil-works/pi/issues/5152), configurable Anthropic OAuth [#5871](https://github.com/earendil-works/pi/issues/5871)).

- **Session Performance & Architecture**: The community strongly desires a **shift from JSONL to SQLite** for session storage ([#5804](https://github.com/earendil-works/pi/issues/5804)), faster session switching ([#5905](https://github.com/earendil-works/pi/issues/5905)), and protection against session bloat from high-frequency metadata changes ([#5909](https://github.com/earendil-works/pi/issues/5909)).

- **SDK Maturity for Embedding**: Growing demand for **enterprise SDK features**: durable HITL interrupts ([#5901](https://github.com/earendil-works/pi/issues/5901)), granular tool gating ([#5907](https://github.com/earendil-works/pi/issues/5907)), bundle optimization (v0.79.8’s entry points), and customizable system prompts with placeholders ([#4789](https://github.com/earendil-works/pi/issues/4789)).

- **Cross-Platform Hardening**: Requests for fixing **WSL path/variable escaping** ([#5893](https://github.com/earendil-works/pi/issues/5893)), **CJK path handling** ([#4425](https://github.com/earendil-works/pi/issues/4425)), and **MinGW compatibility** ([#3672](https://github.com/earendil-works/pi/issues/3672)) signal that Pi is being actively used in diverse development environments.

---

## 6. Developer Pain Points

The most acute pain points this week center on **unexpected tool behavior** and **fragile integrations**:

- **Data Integrity Fears**: The silent rewriting of files by the `edit` tool ([#5899](https://github.com/earendil-works/pi/issues/5899)) was the single highest-severity bug of the week. Although rapidly fixed, the incident shook user confidence. The silent dropping of the `cwd` parameter in the `bash` tool ([#5904](https://github.com/earendil-works/pi/issues/5904)) is a similar pattern of a tool behaving unpredictably without alerting the user or model.

- **Workflow Interruptions**: The streaming scroll bug ([#5825](https://github.com/earendil-works/pi/issues/5825)) actively fights users trying to read output. Slow session initialization and switching times ([#5804](https://github.com/earendil-works/pi/issues/5804), [#5905](https://github.com/earendil-works/pi/issues/5905)) penalize users working across multiple sessions, breaking flow state.

- **Integration Friction**: Non-OpenAI providers remain a source of friction. Users face schema conflicts (Kimi/Moonshot [#5822](https://github.com/earendil-works/pi/issues/5822)), hardcoded authentication patterns (Anthropic OAuth [#5871](https://github.com/earendil-works/pi/issues/5871)), and unusable model lists in the Copilot integration ([#5897](https://github.com/earendil-works/pi/issues/5897)).

- **Windows/Non-Standard Environments**: WSL variable escaping ([#5893](https://github.com/earendil-works/pi/issues/5893)), CJK file path handling ([#4425](https://github.com/earendil-works/pi/issues/4425)), and MinGW write tool failures ([#3672](https://github.com/earendil-works/pi/issues/3672)) collectively paint a picture of Pi’s cross-platform experience still lagging behind its Linux/macOS experience.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-20

## Today's Highlights
This week's digest captures a community grappling with agent stability, particularly a critical Plan Mode regression and subagent lifecycle management failures. In response, the team quickly shipped escape hatches for blocked workflows while merging a wave of PRs to harden input validation across the codebase. Meanwhile, strong demand continues for better model management UX and robust multi-agent coordination primitives.

## Releases
**No new releases in the last 24 hours.** The latest stable version remains **0.17.1**. Users should watch for an imminent patch addressing the stability regressions highlighted this week.

---

## Hot Issues
*Top 10 noteworthy issues updated in the last 24h, ranked by community engagement and impact.*

1. **[#5267](https://github.com/QwenLM/qwen-code/issues/5267) — `context.fileName` config doesn't work (9 comments)**
   A documented setting to specify attachment files for agent prompts is non-functional. Erodes trust in the configuration reference and directly impacts context-injection workflows.

2. **[#5180](https://github.com/QwenLM/qwen-code/issues/5180) — Subagent crashes mid-task in multi-agent setups (6 comments)**
   A "manager" agent delegates to subagents that crash silently without notification. Highlights a missing lifecycle-hook layer for advanced automation.

3. **[#5428](https://github.com/QwenLM/qwen-code/issues/5428) — Agent stuck in Plan Mode (regression, 2 comments)**
   The latest update causes the agent to falsely assume Plan Mode and repeatedly try to exit it on standard prompts. A critical daily-driver bug being actively patched (see PR #5430).

4. **[#5239](https://github.com/QwenLM/qwen-code/issues/5239) — Weak subagent communication primitives (4 comments)**
   No native notification mechanism exists when a subagent finishes or crashes. Users are driven to hacky file-based monitors to track progress.

5. **[#5422](https://github.com/QwenLM/qwen-code/issues/5422) — PostToolUse hook output is dead code (4 comments)**
   `updatedMCPToolOutput` is declared in the hook type but never consumed by the runtime. Misleading API surface quickly fixed in PR #5423.

6. **[#5142](https://github.com/QwenLM/qwen-code/issues/5142) — CLI history invisible in virtualized mode (5 comments)**
   History is hidden until the user presses `/`, creating a fundamental UX confusion in the CLI.

7. **[#4814](https://github.com/QwenLM/qwen-code/issues/4814) — Custom Provider model management friction (5 comments)**
   Adding new models without using presets (e.g., OpenRouter) is cumbersome. A major onboarding barrier for enterprise users.

8. **[#3361](https://github.com/QwenLM/qwen-code/issues/3361) — Agent misinterprets shell output as empty (5 comments)**
   Commands execute successfully, but the agent claims the output buffer is empty. Breaks git and build automation workflows.

9. **[#4951](https://github.com/QwenLM/qwen-code/issues/4951) — Token count accuracy concerns (4 comments)**
   Users report seeing hundreds of thousands of tokens consumed after a few messages, raising trust issues in the statusline telemetry.

10. **[#5408](https://github.com/QwenLM/qwen-code/issues/5408) — Thinking content folded by default (2 comments)**
    The new UI folds the model's thinking output with no clear expand mechanism—a regression users say undermines one of Qwen Code's key differentiators.

---

## Key PR Progress
*Important pull requests updated in the last 24h.*

1. **[#5430](https://github.com/QwenLM/qwen-code/pull/5430) — Escape path for Plan Gate (Open)**
   Adds a `force_exit` mechanism when the Plan Approval Gate is unavailable, providing a direct response to the #5428 crisis.

2. **[#4850](https://github.com/QwenLM/qwen-code/pull/4850) — Interactive multi-tab extensions manager (Open)**
   Turns `/extensions` into a rich UI with **Installed**/**Discover**/**Sources** tabs covering the full extension lifecycle.

3. **[#5396](https://github.com/QwenLM/qwen-code/pull/5396) — UI flicker reduction (Open)**
   Implements throttling (60→100ms), compact mode transitions via `startTransition`, and STREAM_TEXT batching to stabilize rendering.

4. **[#5030](https://github.com/QwenLM/qwen-code/pull/5030) — Resume interrupted turns without "continue" message (Open)**
   Allows seamless resumption of unfinished turns from crashes or history without polluting the transcript with synthetic messages.

5. **[#5409](https://github.com/QwenLM/qwen-code/pull/5409) — Block broad shell self-kill commands (Merged)**
   Detects risky `taskkill`/`pkill`/`killall` patterns before execution, preventing the agent from accidentally terminating its host process.

6. **[#5423](https://github.com/QwenLM/qwen-code/pull/5423) — Remove dead hook field (Merged)**
   Cleans up the `updatedMCPToolOutput` field identified in #5422, tightening the hooks API contract.

7. **[#5426](https://github.com/QwenLM/qwen-code/pull/5426) — Accept uppercase URLs in `mcp add` (Merged)**
   Fixes case-sensitive scheme detection (`startsWith("http://")`) that rejected `HTTPS://` or `HTTP://`.

8. **[#5429](https://github.com/QwenLM/qwen-code/pull/5429) — Accept uppercase URLs in extensions install (Merged)**
   Parallel fix to #5426 for the extension install source parser.

9. **[#5398](https://github.com/QwenLM/qwen-code/pull/5398) — Extension management for web shell (Merged)**
   Brings `/extensions install` and management UI to the daemon and web shell, achieving parity with the CLI.

10. **[#5415](https://github.com/QwenLM/qwen-code/pull/5415) — Bound QQ Bot reconnection retries (Merged)**
    Fixes an infinite-loop bug where gateway HTTP failures never exhausted `reconnectAttempts` due to a missing counter increment.

---

## Feature Request Trends

Three dominant directions emerge from the current issue pipeline:

- **Production-Grade Multi-Agent (#5180, #5239):** Users are pushing beyond prototyping. The demand is for proper subagent lifecycle management, crash notification, and bidirectional communication without file-based hacks.
- **Intelligent Model Routing (#5225, #4814):** A strong desire for automatic Pro/Flash model switching based on task complexity to optimize costs, alongside vastly simplified custom-provider onboarding.
- **Human-in-the-Loop Automation (#5263, #5409):** The community wants confirmation dialogs *before* the agent persists auto-generated skills or executes broadly destructive shell commands.

---

## Developer Pain Points

- **Agent Reliability Fears:** Silent subagent crashes (#5180) and the Plan Mode loop (#5428) are shaking confidence in autonomous background execution. Developers feel they cannot trust long-running workflows.
- **Validation Fatigue:** A torrent of strict validation bugs this week (colons in grep paths [#5370], uppercase URLs [#5390], drive letters in mounts [#5386], equals signs in env vars [#5374]) suggests the input pipeline needs a systematic audit.
- **Telemetry Skepticism:** Inaccurate token counters (#4951) and hidden thinking processes (#5408) frustrate power users who rely on this data for debugging and cost management.
- **Feature Parity Gaps:** Modes like ACP (#5007) and Web Shell (#5398, before fix) consistently lag behind the CLI, fragmenting the developer experience across deployment targets.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-20

> **Note:** While the data source is associated with `DeepSeek-TUI`, the current active repository for development, issues, and pull requests is **`Hmbown/CodeWhale`**. This digest reflects the CodeWhale project and its evolution.

---

## Today's Highlights

Development velocity remains high, with a clear split between architectural groundwork and user-facing improvements. The critical EPIC #2870 command-boundary refactor continues to advance with a new Layer 4 PR (#3330), signaling strong progress toward **v0.9.0**. For the current **v0.8.63** release, the team is shipping high-impact features like a first-class sub-agent toggle (#3327) and block-type-aware thread seeding (#3300). Reliability and compatibility fixes—token budgets, proxy support, and Codex retries—round out the patch queue.

## Releases

**No new releases in the last 24 hours.** The next iteration, **v0.8.63**, is actively being shaped by open PRs (#3327, #3300, #3344, etc.).

## Hot Issues

The data shows **5 issues** updated in the last 24 hours. All are noteworthy for different segments of the community:

1. **[#2870] EPIC: Staged Command-Boundary Refactor**
   *Tracking refs #2791 | Proof PR: #2851*
   The defining architectural change for **v0.9.0**. This EPIC organizes a complex multi-PR refactor that reworks how commands and boundaries are handled. Directly impacts workflow reliability and plugin architecture. Low public reaction (0 👍), but high internal activity.

2. **[#3238] Ubuntu 22.04 LTS – glibc Version Mismatch**
   *Tags: bug, documentation, reliability*
   A hard deployment blocker. The tool fails to run on Ubuntu 22.04 due to a newer glibc requirement. This is a critical compatibility issue for a widely used enterprise and development Linux distribution.

3. **[#3328] v0.8.62 Doesn't Show Sidebar**
   *Tags: question*
   A user-reported UI regression immediately following an upgrade. The user notes `/sidebar` says it's visible, but the terminal interface no longer displays it. Points to a gap in UI change communication or test coverage.

4. **[#3324] Recommendation for Long-Context Compression Library**
   *Tags: recommendation*
   Community member `TuringCorp-net` proposes integrating `mosaic-compress`, a stateless dialogue compression tool. Reflects a deep user need for managing long coding sessions without token limits.

5. **[#3320] Alibaba Cloud Bailian API Key Not Integrated**
   *Tags: bug*
   A feature request from the Chinese market. The tool currently lacks support for Alibaba Cloud's Bailian LLM platform (`bailian.console.aliyun.com`), preventing users in that ecosystem from leveraging local API resources.

## Key PR Progress

Picking 10 of the most significant open PRs:

1. **[#3321] fix(workflow): add token budget regulator for high fan-out agent runs**
   *Author: @donglovejava*
   Closes an enforcement gap between the protocol layer and runtime execution. The `BudgetSpec` only tracked `max_steps` and `timeout_sec`, but token budgets weren't actually enforced at runtime. This PR adds comprehensive regulation, preventing runaway agent spend. High importance for production workloads.

2. **[#3327] v0.8.63: Add first-class sub-agent toggle**
   *Author: @BovmantH*
   Introduces `/config subagents on|off|status`. Users gain session-level and persistent control over sub-agent execution. Wires `AppAction::UpdateFeatures` through `Op::SetFeatures`. A significant UX upgrade for users who need to quickly enable or disable agent delegation.

3. **[#3300] [v0.8.63] feat(tui): preserve thinking/tool blocks when seeding thread from session**
   *Author: @gaord*
   Replaces text-only `seed_thread_from_messages` with a block-type-aware implementation. Preserves `ContentBlock` variants (Thinking, ToolUse, ToolResult) as distinct `TurnItem` entries. Essential for maintaining full conversational context across sessions.

4. **[#3330] Layer 4: replay FEAT-005 command extraction on Hunter**
   *Author: @aboimpinto*
   Advances the **EPIC #2870** refactor. Applies the new command extraction logic against the current trait-backed Hunter registry. A semantic replay, not a raw cherry-pick, targeting `hunter/0.8.62-glm-subagents`.

5. **[#3344] fix(tui): retry Codex responses requests**
   *Author: @cyq1017*
   Fixes **#3019**. The Codex streaming path previously sent requests once and returned immediately on transport/status failures. This routes the responses request through `send_with_retry`, rebuilding per-attempt. Critical for reliability in flaky network environments.

6. **[#3331] fix(tui): enable proxy env for JS execution**
   *Author: @cyq1017*
   Fixes **#3273**. Mirrors lowercase proxy variables and `ALL_PROXY` into the uppercase names that Node.js reads. Adds regression coverage. A critical fix for enterprise users behind corporate firewalls relying on JavaScript execution features.

7. **[#3332] fix(app-server): require auth for non-loopback binds**
   *Author: @cyq1017*
   Fixes **#3258**. Rejects non-loopback app-server binds when no explicit auth token is supplied. Loophole for loopback one-time token generation remains. A straightforward security hardening PR.

8. **[#3345] refactor(config): move inline tests to module**
   *Author: @cyq1017*
   Closes **#3307**. Moves config tests from `crates/config/src/lib.rs` into a dedicated `tests.rs` module. Reduces production file size and future conflict surface. Low risk, high housekeeping value.

9. **[#3333] refactor(tui): split MCP header helpers**
   *Author: @cyq1017*
   Incremental architectural cleanup. Moves HTTP default/header filtering helpers into `mcp::headers`, isolating them from inline transport code. Prepares for the larger MCP transport split in **#3310**.

10. **[#3329] fix(config): restore huggingface env precedence**
    *Author: @gaord*
    Restores Hugging Face API key environment variable precedence on the TUI config surface. Unblocks `scripts/check-provider-registry.py` (the CI/Lint gate) on `main`. A subtle but breaking regression fix.

## Feature Request Trends

1. **Agent Orchestration Governance:** The strongest signal. Users need fine-grained controls for complex agent runs—token budgeting (#3321), sub-agent toggles (#3327), and clearly defined command boundaries (#2870, #3330).

2. **Context Persistence & Fidelity:** A deep push for preserving complex LLM output structures. The community wants thinking/tool blocks preserved across sessions (#3300) and is exploring long-context compression techniques (#3324).

3. **Platform & Provider Expansion:** Growing demand for diverse LLM provider integrations, specifically Alibaba Cloud Bailian in the Chinese market (#3320), indicating the user base is globalizing beyond Western providers.

4. **Architectural Stability for v0.9.0:** Heavy community investment in structural refactoring (command boundaries, MCP transport splitting) signals a collective desire for a stable, extensible foundation before major new features.

## Developer Pain Points

1. **Linux Distribution Compatibility:** The **glibc version mismatch** (#3238) is a severe installation blocker. Developers on stable/reliable distributions like Ubuntu 22.04 LTS are completely locked out, which is a top-priority frustration.

2. **Configuration Friction:** Common onboarding tasks are surprisingly painful. Environment variable precedence keeps breaking (#3329), proxy configuration isn't honored for JS execution (#3331), and major provider API keys lack integration (#3320).

3. **Unreliable Streaming Paths:** The lack of retry logic on the Codex streaming endpoint (#3344) is a persistent reliability bug that degrades experience during critical code-response workflows, leading to silent failures.

4. **Undocumented UI Regressions:** The sidebar state change in v0.8.62 (#3328) that confused users without a clear migration path or `/sidebar` documentation indicates the need for stronger change management and communication around TUI feature toggles and UI layout changes.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*