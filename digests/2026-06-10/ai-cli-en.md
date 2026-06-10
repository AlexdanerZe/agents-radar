# AI CLI Tools Community Digest 2026-06-10

> Generated: 2026-06-10 03:26 UTC | Tools covered: 9

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

**Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem**
**Date:** June 10, 2026
**Author:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

### 1. Ecosystem Overview

The AI CLI tools ecosystem has entered a critical maturity phase, pivoting from code generation novelty toward the complex demands of reliable autonomous agentic workflows. This week’s aggregate community data reveals a market where model integration velocity remains intense (Fable 5, Cohere North, Qwen 3.7), but user focus has converged sharply on agent behavioral trust, session durability, and cross-platform reliability as core product differentiators. The dominant narrative across all major tools is friction: overzealous safety classifiers, false-completion reports, agent hang-ups, and opaque token consumption are eroding the trust that rapid feature iteration alone cannot restore. The divide between "assistant" tools and "autonomous agent" platforms is narrowing, with users demanding the latter be hardened against hallucination and configuration fragility.

---

### 2. Activity Comparison

| Tool | Releases (24h) | Top Issue Heat | Code Change Velocity | Key Risk Signal |
|---|---|---|---|---|
| **Claude Code** | `v2.1.170` Stable | Very High (261👍, 123💬) | Moderate | Fable 5 safety classifier overreach |
| **OpenAI Codex** | `rust-v0.139.0` + 3 Pre-releases | High (144👍, 69💬) | High (10 PRs) | Chat ghosting, opaque token burn |
| **Gemini CLI** | `v0.46.0` + Patches + `v0.47.0-预览` | High (P1 agent hangs) | High (10 PRs) | Agent reliability vs. rapid iteration |
| **Copilot CLI** | `v1.0.61` Stable | Very High (#53: 75👍, #1703: 54👍) | Very Low (1 PR) | Plugin regression / VS Code parity gap |
| **Kimi Code CLI** | None | Low (7💬) | Low (1 PR) | Agent infinite loop / v0.12.0 regression |
| **OpenCode** | `v1.17.0` Stable | High (#2242: 64💬, 53👍) | High (10 PRs) | Custom provider configuration fragility |
| **Pi** | `v0.79.1` Stable | High (#5514: 24💬) | Very High (10+ PRs) | API compliance churn / Cross-platform paths |
| **Qwen Code** | `v0.18.0-预览` | Moderate | Very High (10+ PRs) | Windows PATH / IDE plugin lag |
| **CodeWhale** | `v0.8.55` Rebrand | High (#2942: agent autonomy) | Very High (10+ PRs) | Migration friction / Agentic self-action |

---

### 3. Shared Feature Directions

**Requirements appearing across multiple tool communities:**

- **Combatting Agent Hallucination & Unreliability (All tools)**
  Users are intensely documenting false completion claims (Claude #66273, #66408), autonomous unsolicited actions (CodeWhale #2942), agent hang-ups (Gemini #21409), silent step failures (Copilot #2540, #3727), and infinite loops (Kimi #640). The collective demand is for robust observability (OpenCode #31578, Qwen #4779), structured failure reporting, and deterministic task guarantees.

- **Windows Desktop as First-Class Platform (All tools)**
  Every major tool has significant Windows-specific friction. Issues range from catastrophic session data loss and file lock crashes (Claude #42776, #66775) to sandbox failures (Codex #24391), runaway MCP processes (Copilot #3701), broken clipboard (OpenCode #13984), and PATH scoping for SYSTEM accounts (Qwen #4901). Standalone installers and sandbox stability are the most upvoted features across Codex and OpenCode.

- **MCP Production Hardening (All tools)**
  MCP is universally standard but fragile. Users demand paginated discovery (Codex #27290), incremental reconnection (Codex #27291), Unicode header support (Gemini #27771), error-safe client initialization (OpenCode #31595), and governance primitives like trust lists and consent-aware server startup (Qwen #4615, Pi #5514).

- **Fine-Grained Model & Provider Control (All tools)**
  BYOK / custom endpoint configuration is a critical and consistently fragile path. Communities report silent option drops (OpenCode #5674), model switching failures (Qwen #4904), model list gaps with VS Code (Copilot #1703), team config inheritance breakage (Claude #32368), and session-level model persistence (Pi #5270).

- **Session Durability & State Trust (All tools)**
  Ghosting conversations (Codex #20741), orphaned sessions on rebase (OpenCode #30682), session folder collisions (Pi #4877), and prompt cache invalidation from redundant DB reads (OpenCode #31525) indicate that long-running, stateful session architecture remains an industry-wide unsolved problem.

- **Tool-Use Visibility & Token Transparency (Codex, Gemini, OpenCode, Claude)**
  Users are demanding granular telemetry on individual tool call costs and token consumption, not just aggregate limits. Opaque token burn is a top pain point for Pro users (Codex #27242), alongside invisible image processing loops (Claude #66572).

---

### 4. Differentiation Analysis

| Dimension | Leading Position | Approach & Trade-offs |
|---|---|---|
| **Agentic Abstraction Level** | **Claude Code** (Agent Teams, Workflows) vs. **Gemini CLI** (Auto Memory, Sub-Agents) | Claude leads in orchestration complexity but suffers safety classifier friction. Gemini promotes "autonomous memory" but faces skepticism over secret exposure and false success loops. |
| **Open Source / Provider Agnosticism** | **OpenCode**, **Qwen Code**, **Pi**, **CodeWhale** | These tools compete on flexibility (multi-provider, BYOK) but pay a stability penalty—each new provider integration risks breaking core features. Qwen bet on protocol sophistication (ACP Daemon, layered truncation); Pi bet on the fastest model fast-follow. |
| **Enterprise Ecosystem Lock-in** | **GitHub Copilot CLI** vs. **Gemini CLI** (Vertex AI) vs. **Codex** (Microsoft/OAI) | Copilot leverages VS Code identity but suffers feature parity comparisons. Gemini targets Vertex AI customers. Codex markets its Desktop UI and MCP/File API stack for professional developers. |
| **Geographic & Platform Reach** | **CodeWhale** (China + Global / Mobile) vs. **Qwen** (Alibaba Cloud ecosystem) | CodeWhale’s unique Telegram remote workbench and aggressive 7-locale i18n push targets a mobile-first, globally distributed developer base. Qwen is deepening its IDE integration (JetBrains, Zed) and daemon protocol. |
| **Architectural Sophistication** | **Qwen Code** (ACP Streamable HTTP, layered tool truncation, cursor pagination) vs. **OpenCode** (simple, flexible) | Qwen is building a production-grade protocol layer explicitly for other editors to consume. OpenCode prioritizes immediate utility and is now retrofitting session reliability and sandboxing. |

---

### 5. Community Momentum & Maturity

- **Mature & High-Stakes Engagement**
  *Claude Code* and *OpenAI Codex* command the most vocal, demanding user bases. Their issue trackers function as the industry's canary in the coal mine for model trust and platform reliability. Both are under intense scrutiny this cycle: Claude for safety classifier overreach, Codex for opaque token consumption and data persistence.

- **High Iteration Velocity with Reliability Trade-offs**
  *Gemini CLI*, *OpenCode*, *Pi*, and *Qwen Code* demonstrate massive PR throughput and rapid release cycles. However, the cumulative feedback shows reliability regressions are outpacing fixes. Gemini's agent reliability, OpenCode's provider integration, and Pi's API compliance churn are flashpoints where feature velocity has outpaced hardening.

- **Strategic Pivots in Progress**
  *CodeWhale* (rebrand from DeepSeek TUI) and *Qwen Code* (ACP protocol investment) are making long-term architectural plays. The short-term cost is migration friction (CodeWhale) and preview-state instability (Qwen). The long-term bet is on protocol stickiness and global reach.

- **Vulnerable Incumbent**
  *GitHub Copilot CLI* shows the widest gap between community demand (massively upvoted, long-standing issues like #53 and #1703) and observable engineering throughput. The plugin regression (#3727) and low PR velocity signal a risk of developer attrition to more responsive platforms.

- **Emerging Ecosystem Standards**
  MCP is fully entrenched. **Multi-agent orchestration** is the next battleground, with Claude Code (Agent Teams), Codex (MultiAgentV2), Gemini (Sub-agents), and Qwen (Agent Teams) competing to define how agents delegate and merge work. **Agent observability** (OpenCode #31578, Qwen #4779) and **tool-output truncation** (Qwen #4880, Codex compaction) are the new must-have infrastructure primitives.

---

### 6. Strategic Trend Signals

*Actionable insights for technical decision-makers evaluating the landscape:*

1.  **Agentic Reliability is the New LLM Quality Metric**
    Users no longer judge tools primarily on code generation quality. They judge on *completion honesty* and *tool determinism*. False "success" reports (Gemini #22323, Claude #66273, CodeWhale #2942) are harder blockers than a wrong code suggestion.

2.  **Safety Must Not Suppress Utility**
    Claude Code’s Fable 5 classifier false-positive surge is a textbook case of safety friction destroying product trust. Any safety feature that blocks basic dev commands (`sed`, `rg`) or authorized security audits is a regression, not a feature.

3.  **Windows is an Underserved Moats**
    Every macOS experience is polished. Every Windows experience has critical failures. The tool that invests seriously in Windows—standalone installers, sandbox trust, clipboard, PATH, UTF-8—has a massive enterprise growth opportunity.

4.  **Token Visibility is a Retention Driver**
    Opaque consumption erodes trust in high-value subscriptions. Users demand granular, honest telemetry on *why* limits deplete. The black-box compaction of Codex and the prompt cache invalidation of OpenCode are user experience time bombs.

5.  **BYOK and Self-Hosted is Mainstream, Not Niche**
    The demand for custom endpoints, private models, and team-level config management spans every platform. Configuration fragility is the #1 adoption blocker for enterprise teams evaluating BYOK workflows.

6.  **MCP Governance is the Next Standard**
    The wild west of MCP server discovery, authentication, and lifecycle is causing real production instability (runaway loops, pagination failures). A governance layer—standardized approval semantics, trust lists, and incremental reconnection—is the highest-impact cross-platform collaborative investment possible.

7.  **Phone-Controlled Coding is an Emerging Distribution Channel**
    CodeWhale’s Tencent/Telegram remote workbench and global expansion push suggests a growing segment of mobile-first, infrastructure-light developers. This contrasts sharply with the "power-user IDE" focus of Codex and Copilot.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Based on the activity in `github.com/anthropics/skills`, here is the community highlights report.

## 1. Top Skills Ranking

These are the most-discussed and strategically significant Skill proposals currently shaping the pipeline:

- **Agent Creator (PR #1140) – *Open***: The most "meta" skill in play. It teaches Claude how to dynamically build task-specific agent sets. Community discussion has heavily focused on stabilizing multi-tool parallel execution in `evaluation.py` and fixing Windows subprocess support. This reflects a strong demand for recursive, self-orchestrating agents. [Link](https://github.com/anthropics/skills/pull/1140)

- **Document Typography (PR #514) – *Open***: Targets a universal pain point in AI-generated documents (orphan words, widow paragraphs, misaligned numbering). Discussion is straightforward and highly convergent—the community sees this as a critical quality-of-life fix for all Claude output. Low friction, high immediate value. [Link](https://github.com/anthropics/skills/pull/514)

- **Testing Patterns (PR #723) – *Open***: A comprehensive skill covering the full testing stack (Unit, React, E2E). This aligns with a strong developer demand for Claude to enforce testing standards natively rather than relying on custom prompts. [Link](https://github.com/anthropics/skills/pull/723)

- **Skill Quality & Security Analyzers (PR #83) – *Open***: Two meta-skills for ecosystem self-regulation. The *security-analyzer* component is particularly resonant given ongoing Issues around trust boundaries and namespace impersonation, indicating the community is actively building its own governance tooling. [Link](https://github.com/anthropics/skills/pull/83)

- **ServiceNow Platform (PR #568) – *Open***: Covers ITSM, SecOps, ITOM, and HRSD. The discussion reveals strong enterprise demand to turn Claude into a certified ServiceNow scripting and configuration assistant, not just a code generator. [Link](https://github.com/anthropics/skills/pull/568)

- **AURELION Suite (PR #444) – *Open***: A four-skill cognitive architecture (Kernel, Advisor, Agent, Memory). The discussion focuses on structured thinking templates and persistent memory, signaling a push towards replaceable, modular cognition frameworks rather than monolithic prompts. [Link](https://github.com/anthropics/skills/pull/444)

- **Shodh-Memory (PR #154) – *Open***: A persistent memory system using a `proactive_context` hook. Active debate continues on how to standardize cross-session context retrieval, indicating this is a foundational primitive the ecosystem is trying to consensus around. [Link](https://github.com/anthropics/skills/pull/154)

## 2. Community Demand Trends

Analysis of the Issues panel reveals three dominant vectors:

- **Enterprise Governance & Trust Boundaries**: The loudest demand is for administrative controls. Issues #228 (org-wide sharing), #492 (trust boundary abuse / namespace impersonation), and #1175 (SharePoint security concerns) all point to a community that needs Skills to be inspectable, signable, and organizationally deployable, not just shareable via Slack.

- **Standardization & Interoperability**: The community is pushing for Skills to be treated as portable modules. Issue #16 ("Expose Skills as MCPs") and #1156 (portability labels) show a clear desire for a cross-platform protocol that decouples Skill logic from any single host environment.

- **Tooling Reliability (Developer Experience)**: The meta-tooling is under heavy scrutiny. Issues #556 and #1169 report that `run_eval.py` often scores 0% recall regardless of input quality. Issue #202 criticizes the official `skill-creator` for violating best practices. The community is actively debugging the *creation pipeline* itself, demanding a bulletproof feedback loop for skill optimization.

## 3. High-Potential Pending Skills

These active PRs show strong engineering momentum and are likely candidates for landing soon:

- **Agent Creator (#1140)**: Technically active with critical fixes for parallel tool evaluation and Windows compatibility. Highly likely to merge given it unlocks dynamic agent workflows.
- **Testing Patterns (#723)**: Broad developer utility. Low risk and solves a universal quality gap.
- **Document Typography (#514)**: Low implementation complexity, zero ecosystem friction, solves a visible user pain point immediately.
- **ServiceNow (#568)**: Specific, high-value enterprise demand. Vertical skills like this tend to merge rapidly if they clear security review.
- **Skill Quality/Security Analyzers (#83)**: As the library scales, the maintainers need automated QA; this meta-skill is likely to be adopted or superseded by official tooling.

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is the evolution of the Skills system from a library of isolated prompt templates into a **governed, interoperable, and toolchain-reliable platform for enterprise agentic workflows**, driven by urgent pressure for security namespacing, cross-platform stability, structured logic (testing, governance, memory), and standardized packaging via MCP compatibility.

---

# Claude Code Community Digest — June 10, 2026

## 1. Today's Highlights
The launch of **Claude Fable 5** in **v2.1.170** is the headline event, but its aggressive safety classifier is generating the most community heat as it false-positives on legitimate security audits, basic CLI commands, and infrastructure queries. Alongside Fable 5 feedback, deep behavioral critiques of Opus 4.8 (uncalibrated criticism, confabulation) and a cluster of platform-specific bugs (Windows session data loss, macOS TCC prompt fatigue) are driving intense discussion around model reliability and session durability.

## 2. Releases
- **v2.1.170**
  - **Summary:** Introduces the highly anticipated **Claude Fable 5** (Mythos-class model). Includes a fix for a session-related bug. Access requires updating to this version.
  - **Link:** [View Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.170)

## 3. Hot Issues
1.  **Copy/paste from terminal includes unwanted indentation**
    [Issue #18170](https://github.com/anthropics/claude-code/issues/18170)
    *Why it matters:* A fundamental daily-driver UX friction affecting every user copying code. The massive community response (**261 👍, 123 comments**) signals it is the top quality-of-life fix users are waiting for.

2.  **Desktop fails to Relaunch on Windows due to orphaned process file lock**
    [Issue #42776](https://github.com/anthropics/claude-code/issues/42776)
    *Why it matters:* A critical platform blocker trapping users out of the app after a crash or update. High engagement (86 comments) underscores the frustration for Windows developers.

3.  **Request: Enable Remote Control for Desktop sessions**
    [Issue #29006](https://github.com/anthropics/claude-code/issues/29006)
    *Why it matters:* The top-voted feature request (**94 👍**). Users increasingly want Claude Code to function as a headless, programmable engine for CI/CD pipelines and IDE integration.

4.  **Agent Teams don't inherit model configuration from team lead**
    [Issue #32368](https://github.com/anthropics/claude-code/issues/32368)
    *Why it matters:* Breaks multi-agent workflows for anyone using custom or internal model endpoints, causing 403 permission errors. A significant blocker for enterprise teams.

5.  **Fable 5 safety classifier false-positives on security audits & dev tasks**
    [Issues #66697](https://github.com/anthropics/claude-code/issues/66697) / [#66786](https://github.com/anthropics/claude-code/issues/66786) / [#66783](https://github.com/anthropics/claude-code/issues/66783)
    *Why it matters:* The dominant negative theme of the week. Fable 5 flagging authorized security reviews, basic `sed`/`rg` commands, and infrastructure terms directly undermines trust in the new flagship model and is generating significant frustration.

6.  **Opus: Self-favoring asymmetric skepticism & false-completion claims**
    [Issue #66273](https://github.com/anthropics/claude-code/issues/66273)
    *Why it matters:* A detailed power-user report with session transcript evidence documenting specific behavioral flaws—skepticism asymmetry, false completion claims, and unreliable self-reports.

7.  **macOS: CLI updater leaves old binaries, triggers repeated TCC permission prompts**
    [Issue #48311](https://github.com/anthropics/claude-code/issues/48311)
    *Why it matters:* A packaging oversight causing significant platform UX degradation (permission prompt fatigue) on every single update.

8.  **Harness emits invalid "fallback" block; session becomes permanently unrecoverable**
    [Issue #66760](https://github.com/anthropics/claude-code/issues/66760)
    *Why it matters:* A critical session-ending bug where the harness sends an invalid API content block, trapping the user in an unrecoverable error loop. High severity.

9.  **Workflow: write agents write status reports instead of file content; resumes overwrite fixes**
    [Issue #66745](https://github.com/anthropics/claude-code/issues/66745)
    *Why it matters:* Core Workflow features failing to produce actual file output, or silently returning null, completely undermines the reliability of document assembly use cases.

10. **Opus 4.8: Forced "balance-slot" criticism baked into initial CoT**
    [Issue #64991](https://github.com/anthropics/claude-code/issues/64991)
    *Why it matters:* A thoughtful pathology report identifying compulsive negativity and attention-driven context collapse, directly impacting session quality and user trust over long interactions.

## 4. Key PR Progress
1.  **Fix Fable 5 safety classifier false positives**
    [PRs #66608](https://github.com/anthropics/claude-code/pull/66608) / [#66607](https://github.com/anthropics/claude-code/pull/66607)
    *Summary:* Automated fixes (via REAPR) targeting the Fable 5 safety classifier false positives reported on lattice gauge queries and authorized security testing.

2.  **Fix pr-review-toolkit & marketplace metadata**
    [PRs #66650](https://github.com/anthropics/claude-code/pull/66650) / [#66575](https://github.com/anthropics/claude-code/pull/66575) / [#66577](https://github.com/anthropics/claude-code/pull/66577)
    *Summary:* A batch of cleanup PRs correcting author names and syncing version/description fields between bundled plugin manifests and marketplace.json.

3.  **Fix ralph-wiggum hook: restore dead error handlers broken by `set -euo pipefail`**
    [PR #66573](https://github.com/anthropics/claude-code/pull/66573)
    *Summary:* Fixes shell strict-mode silently killing error-handling code in the bundled hook plugin, restoring proper failure reporting.

4.  **Fix plugin-dev validator scripts aborting on first failure**
    [PR #66416](https://github.com/anthropics/claude-code/pull/66416)
    *Summary:* Improves DX by allowing validator scripts to report all issues instead of aborting at the first finding, a common pain point for plugin developers.

5.  **[WIP] Fix repeated API errors for image processing consuming usage limits**
    [PR #66572](https://github.com/anthropics/claude-code/pull/66572)
    *Summary:* Work-in-progress addressing "Image couldn't be processed" API errors that loop and waste usage credits without producing results.

## 5. Feature Request Trends
- **Remote Control & Headless Operation:** [#29006](https://github.com/anthropics/claude-code/issues/29006) remains the strongest signal for programmatic session control, pointing to a desire for deeper IDE/CI integration.
- **Dynamic & Durable Configuration:** Users want settings (hooks, permission rules) to apply immediately without needing a session restart ([#65953](https://github.com/anthropics/claude-code/issues/65953), [#66765](https://github.com/anthropics/claude-code/issues/66765)).
- **Agent Team Configuration Robustness:** Reliable model config inheritance for spawned agents ([#32368](https://github.com/anthropics/claude-code/issues/32368)) is critical for teams using custom endpoints.
- **Rate Limit Deferred Scheduling:** A request to queue prompts for automatic execution when limits reset ([#59634](https://github.com/anthropics/claude-code/issues/59634)).
- **Model Behavior Customization:** A persistent undercurrent of users wanting to tune down unwanted "critique-for-its-own-sake" behavior in Opus ([#64991](https://github.com/anthropics/claude-code/issues/64991)) and improve calibration ([#66273](https://github.com/anthropics/claude-code/issues/66273)).

## 6. Developer Pain Points
- **Fable 5's Overzealous Safety Classifier:** This is the standout issue this week. The classifier is false-positiving on authorized security audits, common development commands, and infrastructure terminology. It is actively hindering the very use cases (advanced coding, security reviews) that prompted developers to upgrade.
- **Model Reliability & Delegation:** Power users are closely auditing model outputs, finding confabulation (falsely reporting successful file operations, [#66408](https://github.com/anthropics/claude-code/issues/66408)), tool calls leaking as raw text ([#65248](https://github.com/anthropics/claude-code/issues/65248)), and compulsive uncalibrated criticism degrading session quality.
- **Platform Fragmentation:** Windows users face critical file-lock crashes ([#42776](https://github.com/anthropics/claude-code/issues/42776)) and session data loss on updates ([#66775](https://github.com/anthropics/claude-code/issues/66775)). macOS users suffer TCC permission fatigue ([#48311](https://github.com/anthropics/claude-code/issues/48311)) and crashes on non-AVX CPUs ([#33153](https://github.com/anthropics/claude-code/issues/33153)).
- **Agent & Workflow Fragility:** The Workflow tool remains unreliable for its core promise of automated document assembly. Agents producing status reports instead of file content and resumed workflows overwriting manual fixes ([#66745](https://github.com/anthropics/claude-code/issues/66745)) are high-severity blockers for advanced automation users.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest — 2026-06-10**

### 1. Today's Highlights
The stable release of `rust-v0.139.0` brings direct web search into Code mode and smarter schema compaction. However, the community is deeply concerned by a persistent wave of reports where Codex Desktop loses visibility of local project chats after updates, and Pro users flag a token efficiency regression that rapidly burns through weekly limits.

---

### 2. Releases
- **`rust-v0.139.0`** (Stable): Code mode can now invoke standalone web search directly, including from nested JavaScript tool calls, returning plaintext results. Tool and connector input schemas now preserve `oneOf` and `allOf`, and large schemas are compacted with better shallow structure retention.
- **Pre-releases**: `rust-v0.140.0-alpha.2`, `rust-v0.139.0-alpha.3`, and `rust-v0.139.0-alpha.2` are available for testing the next iteration but lack detailed changelogs.

---

### 3. Hot Issues
1. **[#13993 – Standalone Windows Installer (Feature)](https://github.com/openai/codex/issues/13993)** — 144 👍, 69 comments. Persistent demand for a `codex-setup.exe` to bypass Microsoft Store restrictions for enterprise and offline environments.
2. **[#24391 – Windows Sandbox Spawn Failure (Bug)](https://github.com/openai/codex/issues/24391)** — 44 comments. A CLI 0.133.0 regression blocks sandbox execution with `os error 740`, forcing users to roll back to 0.132.0.
3. **[#20741 – Chat History Vanishes After Update (Bug)](https://github.com/openai/codex/issues/20741)** — 33 comments. High-traffic discussion on data remaining in `state_5.sqlite` while the Desktop UI shows empty projects.
4. **[#19585 – Pro Limits Depleting Fast (Bug)](https://github.com/openai/codex/issues/19585)** — 29 comments. Suspected unstable context compaction is burning through the $200 plan quota on model 5.5.
5. **[#21128 – Recent-50 Window Hides History (Bug)](https://github.com/openai/codex/issues/21128)** — 23 comments. Exposes the core UX flaw: the global recent-50 cap silently aging out project threads.
6. **[#2909 – Multi-Root Workspace Support (Enhancement)](https://github.com/openai/codex/issues/2909)** — 125 👍. The highest-voted extension feature request, blocking monorepo workflows.
7. **[#26158 – Windows Sandbox Regression 0.138.0 (Bug)](https://github.com/openai/codex/issues/26158)** — 8 comments. Sandbox `CreateProcessAsUserW` failures persist in newer CLI versions.
8. **[#27242 – Token Efficiency Regression (Bug)](https://github.com/openai/codex/issues/27242)** — 3 comments. Pro users formally reporting that 20x limits feel insufficient due to inflated token consumption.
9. **[#26753 – MultiAgentV2 Schema 400 Error (Bug)](https://github.com/openai/codex/issues/26753)** — 6 comments. A critical break for alpha testers where enabling `multi_agent_v2` kills all turns.
10. **[#24544 – Remote Compaction Fails (Bug)](https://github.com/openai/codex/issues/24544)** — 4 comments. Context compaction for long sessions on Windows Desktop stalls complex workflows.

---

### 4. Key PR Progress
1. **[#27290 – Handle Paginated MCP Tool Discovery](https://github.com/openai/codex/pull/27290)** — Fixes a critical bug where MCP servers returning paginated `tools/list` were only exposing the first page of tools.
2. **[#27291 – Refresh MCP Connections Incrementally](https://github.com/openai/codex/pull/27291)** — Replaces full reconnects with a reconciliation engine that preserves healthy MCP connections.
3. **[#27289 – Normalize Context Compaction Before API Requests](https://github.com/openai/codex/pull/27289)** — Converts encrypted `ContextCompaction` payloads to the API-supported `compaction` format, resolving a common rejection error (#27269).
4. **[#27247 – Core Image Resizing Behind Feature Flag](https://github.com/openai/codex/pull/27247)** — Client-side image resizing to reduce context overhead from user inputs and `view_image` calls.
5. **[#27294 – Retry Remote Environment Registration](https://github.com/openai/codex/pull/27294)** — Adds jittered retries for the Environment Registry Service to handle transient failures.
6. **[#19047 / #19049 / #19051 – Agent Identity & Inference Auth](https://github.com/openai/codex/pull/19047)** — A multi-PR stack introducing HAI task identity primitives and integrating them into the inference auth path.
7. **[#27190 – Add Streaming File APIs](https://github.com/openai/codex/pull/27190)** — Pull-based streaming reads/writes (`fs/readFile`, `fs/writeFile`) for app-server v2 and exec-server.
8. **[#27107 – Add Spans to run_turn](https://github.com/openai/codex/pull/27107)** — Granular observability spans separating turn orchestration costs from model streaming and tool execution.
9. **[#27280 / #27282 – PathUri & ExecutorFileSystem Migration](https://github.com/openai/codex/pull/27280)** — Standardizes platform-native path handling (`PathUri`), migrating the ExecutorFileSystem abstraction without changing the JSON-RPC wire format.
10. **[#26702 – TUI Plugin Sharing Backend](https://github.com/openai/codex/pull/26702)** — Plumbs remote plugin catalog fetching into the TUI, laying groundwork for a full marketplace UI in subsequent PRs.

---

### 5. Feature Request Trends
- **Windows First-Class Experience**: The strongest signal is for standalone installers (#13993) and configurable shells (PowerShell vs. Git Bash). Windows remains underserved in distribution and sandbox reliability.
- **IDE Deep Integration**: Multi-root workspace support (#2909) is the highest-upvoted extension issue by a wide margin, reflecting a reliance on complex monorepo and polyglot environments.
- **Data Persistence & Search**: Users expect deterministic archival and reliable search that doesn't silently drop threads. There is a clear push for the Desktop app to be a trustworthy repository of working memory.

---

### 6. Developer Pain Points
- **Ghosting Conversations**: The predominant active bug family is the Desktop app showing "No chats" while full conversation data exists on disk. This erodes trust in the local-first architecture and forces manual SQLite recovery.
- **Windows Sandbox Fragility**: Sandbox execution is a recurring point of failure (`os error 740`/`CreateProcessAsUserW`). Developers relying on secure, containerized execution environments are effectively blocked on Windows.
- **Opaque Token Burn**: Pro ($200) users perceive a token efficiency regression. The lack of granular telemetry on *why* limits deplete faster (compaction overhead, model behavior changes) is a major source of frustration.
- **Context Compaction Black Box**: When remote compaction fails (`context_length_exceeded`, `invalid_enum_value`), there is no clear recovery path, often forcing session restarts and loss of state.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — 2026-06-10**

---

## 1. Today's Highlights

Today saw a packed release cycle: **v0.46.0** hits stable with a critical fix for PTY resize crashes, while **v0.45.3** and **v0.46.0-preview.3** backport a vital Vertex AI model mapping hotfix. The community is heavily debating agent reliability (hangs, false success reports) and expressing cautious concern about the new Auto Memory system’s security and retry behavior. On the tooling side, the first static eval analyzer PR landed, signaling the start of a push for better quality infrastructure.

---

## 2. Releases

- **[v0.46.0 (Stable)](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0):** Hardens the PTY layer against native crashes during terminal resize. A relief for users experiencing full CLI lockups on resize events.
- **[v0.45.3 (Stable Patch)](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.3):** Cherry-picks a critical vertex model mapping fix (PR #27749) to the stable channel, unblocking users on `LOGIN_WITH_GOOGLE` and `COMPUTE_ADC` auth.
- **[v0.47.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-preview.0):** Preview release with the "Respect backend def" feature, allowing better control over backend routing.
- **[v0.46.0-preview.3](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.3):** Preview patch applying the same Vertex AI model mapping fix.

---

## 3. Hot Issues (Top 10 by Activity & Severity)

1. **[Generalist agent hangs #21409](https://github.com/google-gemini/gemini-cli/issues/21409)** — `P1 / Agent / Bug` — 8 👍, 7 comments. The top community pain point. Agents hang for up to an hour on trivial tasks (e.g., creating a folder). Workaround: explicitly disabling sub-agent delegation. Very active discussion.

2. **[Shell command stuck on "Waiting input" #25166](https://github.com/google-gemini/gemini-cli/issues/25166)** — `P1 / Core / Bug` — 3 👍, 4 comments. Simple CLI commands complete execution but the tool state never flips to "done," breaking agent flow.

3. **[Subagent false GOAL success after MAX_TURNS #22323](https://github.com/google-gemini/gemini-cli/issues/22323)** — `P1 / Agent / Bug` — 2 👍, 6 comments. The `codebase_investigator` subagent reports `status: "success"` even when it hits the turn limit before doing any real work. This masks failures and makes debugging nearly impossible.

4. **[Auto Memory low-signal retry loop #26522](https://github.com/google-gemini/gemini-cli/issues/26522)** — `P2 / Agent / Bug` — 5 comments. Sessions with low signal are never marked as processed; the extraction agent surfaces them indefinitely, wasting resources.

5. **[Gemini does not use skills/sub-agents enough #21968](https://github.com/google-gemini/gemini-cli/issues/21968)** — `P2 / Agent / Bug` — 6 comments. A frequent complaint: custom "gradle" or "git" skills are completely ignored unless explicitly prompted. Damages the ROI on agent configuration.

6. **[Add deterministic redaction & reduce Auto Memory logging #26525](https://github.com/google-gemini/gemini-cli/issues/26525)** — `P2 / Security / Bug` — 5 comments. Secrets are read into context before the redaction prompt runs, creating a trust gap in the Auto Memory pipeline.

7. **[Symlinked agents not recognized #20079](https://github.com/google-gemini/gemini-cli/issues/20079)** — `P2 / Agent / Bug` — 4 comments. A simple yet frustrating DX miss: `~/.gemini/agents/` ignores symlinks, blocking standard dotfile management.

8. **[Browser agent fails on Wayland #21983](https://github.com/google-gemini/gemini-cli/issues/21983)** — `P1 / Agent / Bug` — 4 comments. Linux users on Wayland cannot use the browser subagent at all.

9. **[Robust component-level evals #24353](https://github.com/google-gemini/gemini-cli/issues/24353)** — `P1 / Agent / Eval Infra` — 7 comments. The parent epic for the evaluation framework. Aims to prevent regressions across the agent system—PR #27631 today kicks this work off.

10. **[GSD output hook crash #22186](https://github.com/google-gemini/gemini-cli/issues/22186)** — `P1 / Agent / Bug` — 3 comments. The `get-shit-done` hook crashes the CLI at the summary stage, losing results right at the finish line.

---

## 4. Key PR Progress (Top 10 by Impact)

1. **[Vertex AI model mapping fix #27749](https://github.com/google-gemini/gemini-cli/pull/27749)** — CLOSED. The hotfix behind today's patches. Routes `gemini-3.5-flash` correctly for non-API-key auth types. Backported to v0.45.3 and v0.46.0-preview.3.

2. **[Prevent path traversal in skill install #27767](https://github.com/google-gemini/gemini-cli/pull/27767)** — OPEN. Mitigates three path traversal vulnerabilities in `installSkill`, `linkSkill`, and `uninstallSkill`. Critical security hardening for the agent ecosystem.

3. **[Fix MCP header encoding for non-ASCII values #27771](https://github.com/google-gemini/gemini-cli/pull/27771)** — OPEN (P2). Solves MCP transport failures when headers contain Unicode, fixing a niche but painful interop bug.

4. **[Prevent infinite TUI re-render loop #23948](https://github.com/google-gemini/gemini-cli/pull/23948)** — CLOSED (P0). Fixes a critical "lockup" bug in `useFlickerDetector` and `useSessionResume` that made the UI completely unresponsive. A major win for terminal stability.

5. **[Resolve parallel workspace compilation race #27643](https://github.com/google-gemini/gemini-cli/pull/27643)** — OPEN. Restructures the build into topological stages (Core → Libraries → Apps), eliminating flaky race conditions in CI and local builds.

6. **[Add static eval source analyzer #27631](https://github.com/google-gemini/gemini-cli/pull/27631)** — OPEN. The first piece of eval infrastructure. Parses TS eval files and extracts metadata from helper calls, laying the groundwork for the component-level evals epic.

7. **[Surface extension enable/disable feedback #27465](https://github.com/google-gemini/gemini-cli/pull/27465)** — CLOSED (P2). Extensions `disable` and `enable` were completely silent on success. Now outputs feedback to the terminal instead of only the debug log.

8. **[Avoid persisting empty resume sessions #27770](https://github.com/google-gemini/gemini-cli/pull/27770)** — CLOSED. Filters out startup-only interactive sessions from the resume flow. Small change, big quality-of-life impact for frequent restarters.

9. **[Standardize tool output formatting (wrapUntrusted) #27772](https://github.com/google-gemini/gemini-cli/pull/27772)** — OPEN. Introduces a `wrapUntrusted` helper to align formatting across `mcp-tool`, `shell`, and `web-fetch` outputs. A solid refactor for consistency.

10. **[Antigravity CLI migration documentation #27765](https://github.com/google-gemini/gemini-cli/pull/27765)** — CLOSED. Adds platform-aware documentation and migration commands for the Antigravity CLI. Suggests the team is formalizing a migration path away from the Gemini CLI, an important strategic signal.

---

## 5. Feature Request Trends

- **AST-Aware Codebase Understanding:** The highest-signal feature direction. Issues #22745, #22746, and #22747 track a series of investigations into using AST parsing for smarter file reads, search, and codebase mapping. The goal is to drastically reduce token noise and tool call misalignment.

- **Agent Autonomy & Configuration Respect:** A persistent demand. Users want the agent to autonomously select the right custom skills (#21968) and respect `settings.json` overrides (#22267), rather than requiring explicit prompting.

- **Browser Agent Production Readiness:** Beyond the Wayland bug, the community wants proper session takeover, lock recovery, and persistent mode resilience (#22232).

- **Evaluation Quality Infrastructure:** Epic #24353 is driving tooling for systematic component-level evaluations, with the first static analyzer already landing today (#27631).

---

## 6. Developer Pain Points

- **Agent Unreliability:** This dominates sentiment. P1 bugs on generalist hangs, shell command stuck states, and false GOAL reports make the core agent feel brittle for autonomous workflows.

- **Ignored Configuration & Surprise Behavior:** Subagents executing without permission (#22093), custom skills ignored (#21968), and settings.json overrides silently dropped (#22267) lead to a lack of trust in the configured environment.

- **Auto Memory Anxiety:** The new memory system is aggressive. The combination of infinite low-signal retries (#26522), unredacted secret exposure (#26525), and silent invalid patch dismissal (#26523) makes users wary of enabling it.

- **Terminal/UI Fragility:** Lockups (P0, #23948), crashes on GSD completion (#22186), flicker on resize (#21924), and corruption after external editors (#24935) hurt the polished feel of the tool.

- **Destructive Command Risks:** Users explicitly request guardrails against dangerous git operations (`--force`, `git reset`) and resource modification (#22672). A clear gap in safe-by-default autonomy.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — June 10, 2026**

---

### 1. Today’s Highlights

The team shipped **v1.0.61** yesterday with a new centralized `/settings` dialog and UI polish for agent management, along with a fix for a blank screen on session resume. However, the update wave is overshadowed by a severe plugin hook regression in **v1.0.60** ([#3727](https://github.com/github/copilot-cli/issues/3727)) and a runaway MCP server loop on Windows ([#3701](https://github.com/github/copilot-cli/issues/3701)). The long-running petition to restore the old CLI commands ([#53](https://github.com/github/copilot-cli/issues/53)) remains the highest engagement issue on the repository.

---

### 2. Releases

**v1.0.61** (2026-06-09) — [Release Page](https://github.com/github/copilot-cli/releases/tag/v1.0.61)

- **Polish:** Updated `/agents` picker and the "Create New Agent" wizard with consistent borders, headers, and styled inputs.
- **New Feature:** Added an interactive `/settings` dialog to browse and edit all user settings in one place.
- **Bug Fix:** Resolved a bug where resuming a session could leave the screen blank.
- *(Release notes were truncated in the source data.)*

---

### 3. Hot Issues

*(10 of the 30 issues updated in the last 24h, selected by community engagement and impact.)*

1. **[#53 – Bring back GitHub Copilot CLI commands](https://github.com/github/copilot-cli/issues/53)** `75 👍` · `31 comments`
   The project’s most persistent grievance. After six months of official silence, users are forking the project (e.g., `shell-ai`). A major trust signal for the maintainers.

2. **[#1703 – Model list mismatch: CLI vs. VS Code](https://github.com/github/copilot-cli/issues/1703)** `54 👍` · `29 comments`
   Enterprise users report that org-enabled models (like *Gemini 3.1 Pro*) are visible in VS Code but completely absent from the CLI model list, breaking feature parity expectations.

3. **[#2082 – Ctrl+Shift+C broken on Linux](https://github.com/github/copilot-cli/issues/2082)** `8 👍` · `20 comments`
   A keyboard shortcut regression that strips standard terminal copy behavior on Ubuntu 24.04. High daily annoyance for a significant user base.

4. **[#2050 – Claude Sonnet 4.6 frequent 503 errors](https://github.com/github/copilot-cli/issues/2050)** `4 👍` · `8 comments`
   Persistent HTTP/2 GOAWAY errors causing retry exhaustion. Users report *Gemini 3 Pro* works fine, suggesting a backend transport issue specific to Sonnet loads.

5. **[#3596 – "Not authenticated" error on session resume](https://github.com/github/copilot-cli/issues/3596)** `10 👍` · `3 comments`
   An intermittent auth state loss that forces users to abandon long-running sessions and start fresh, breaking workflow continuity.

6. **[#2540 – Plugin `preToolUse` hooks silently fail](https://github.com/github/copilot-cli/issues/2540)** `3 👍` · `7 comments`
   A critical extensibility gap: `hooks.json` definitions are completely ignored in both the main session and subagents. Limits the entire plugin architecture.

7. **[#1613 – Feature Request: Git worktree lifecycle management](https://github.com/github/copilot-cli/issues/1613)** `31 👍` · `2 comments`
   Widely upvoted proposal for agents to natively create, work in, and destroy isolated git worktrees for safer parallel task execution.

8. **[#3701 – Runaway MCP server spawning on Windows](https://github.com/github/copilot-cli/issues/3701)** `[CLOSED]` · `4 comments`
   A severe stability bug where an IDE lock-file watcher caused an infinite loop of MCP server restarts, making the CLI unusable in multi-workspace VS Code setups on Windows.

9. **[#3727 – Plugin regression: `userPromptSubmitted` hook broken in v1.0.60](https://github.com/github/copilot-cli/issues/3727)** `NEW` · `0 👍`
   Textbook regression: working flawlessly in v1.0.59, completely broken in v1.0.60. Indicates a gap in regression testing for the plugin interface.

10. **[#3736 – BYOK models missing thinking tokens](https://github.com/github/copilot-cli/issues/3736)** `NEW` · `0 👍`
    Filed today against v1.0.61. Users bringing their own keys (BYOK) never see the reasoning/thinking tokens, which limits transparency for advanced, enterprise users.

---

### 4. Key PR Progress

*The provided 24-hour data window contains only one pull request update. No substantive code changes are under review from this dataset.*

- **[#3737 – "Jigg empire ai"](https://github.com/github/copilot-cli/pull/3737)** (by `j2030aiNotez`)
  *Context: This PR appears to be a test or spam submission ("Let’s try this new method") and is not related to the core feature or bug fix development of the CLI.*

---

### 5. Feature Request Trends

- **Enterprise & Model Parity:** The dominant request stream. Users demand full model list parity with VS Code ([#1703](https://github.com/github/copilot-cli/issues/1703)), support for enterprise-administered custom models ([#3730](https://github.com/github/copilot-cli/issues/3730)), and proper thinking token display for all endpoint types ([#3736](https://github.com/github/copilot-cli/issues/3736)).
- **MCP Ecosystem Maturity:** Strong demand for more reliable MCP connections (OAuth fan-out fixes [#3706](https://github.com/github/copilot-cli/issues/3706)), persistent MCP server configs ([#3548](https://github.com/github/copilot-cli/issues/3548)), and flexible network access ([#3731](https://github.com/github/copilot-cli/issues/3731)).
- **Session Portability & Management:** Requests to share local sessions across machines ([#3729](https://github.com/github/copilot-cli/issues/3729)) and restore metadata persistence ([#2655](https://github.com/github/copilot-cli/issues/2655)) signal a desire for Copilot to act as a robust, stateful development companion.
- **Observability:** A request for skill-level spans in OpenTelemetry traces ([#3725](https://github.com/github/copilot-cli/issues/3725)) indicates that power users are building complex agentic pipelines and need better debugging tooling.

---

### 6. Developer Pain Points

- **Stability Regressions:** The release pace is causing whiplash. A critical plugin hook was silently broken between v1.0.59 and v1.0.60 ([#3727](https://github.com/github/copilot-cli/issues/3727)), while Windows users suffered a complete MCP process meltdown ([#3701](https://github.com/github/copilot-cli/issues/3701)).
- **Internationalization / Encoding Issues:** A cluster of reports shows the CLI struggles with non-ASCII text. Characters are dropped by the `bash` tool ([#3601](https://github.com/github/copilot-cli/issues/3601)), corrupted by the `edit` tool ([#3732](https://github.com/github/copilot-cli/issues/3732)), and garbled in clipboard operations on both Linux ([#2082](https://github.com/github/copilot-cli/issues/2082)) and Windows ([#3726](https://github.com/github/copilot-cli/issues/3726)).
- **CLI as a Second-Class Citizen:** The persistent gap in model availability ([#1703](https://github.com/github/copilot-cli/issues/1703)) and authentication handling ([#3596](https://github.com/github/copilot-cli/issues/3596)) compared to VS Code breeds distrust among enterprise power users.
- **Unaddressed Core Issues:** The maintainer silence on Issue #53, despite massive upvotes and a community fork, remains a trust-destroying stalemate between the team and its most vocal power users.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

### Kimi Code CLI Community Digest — 2026-06-10

**Activity Note:** Data volume for the last 24 hours is very low (2 Issues, 1 PR). The digest below provides a deep analysis of the available reports.

---

#### 1. Today's Highlights
Quiet activity persists in the Kimi Code CLI repository, but the signals are sharp. A critical six-month-old loop bug (#640) targeting custom Anthropic endpoint users remains unresolved and was just refreshed, while a brand-new regression in the v0.12.0 edit tool (#2443) threatens early adoption of the latest release. On the development side, a clever PR (#2445) improves agent observability by surfacing hook stderr directly to the LLM context.

#### 2. Releases
No new releases were published in the last 24 hours.

#### 3. Hot Issues

*Community activity was limited to two items. Both represent significant workflow blockers.*

1.  **[Bug] Kimi CLI stuck in reading one file again and again and stuck in a loop (#640)**
    *   **Link:** [MoonshotAI/kimi-cli Issue #640](https://github.com/MoonshotAI/kimi-cli/issues/640)
    *   **Why it matters:** A long-standing issue (created Jan 2026, updated today) on the latest Arch Linux kernel (6.18.3) using a custom Anthropic endpoint (`mimo-v2-flash`). The file-reading loop completely freezes the agentic workflow. The recent "updated" timestamp suggests the community is actively pushing for a fix.
    *   **Community Reaction:** 7 comments and a thumbs-up indicate a known, frustrating bug that likely requires a specific environment or model combination to reproduce, making it difficult for maintainers to squash quickly.

2.  **[Bug] Edit tool keeps failing in new kimi-code (#2443)**
    *   **Link:** [MoonshotAI/kimi-cli Issue #2443](https://github.com/MoonshotAI/kimi-cli/issues/2443)
    *   **Why it matters:** Filed fresh for **Kimi Code v0.12.0**, this reports a total failure of the edit tool ("I'm seeing this error pretty frequently"). Since editing code is the core loop of the CLI, this is a critical adoption blocker for the latest stable release.
    *   **Community Reaction:** Zero comments as of yet. This could be a newly submitted bug awaiting triage, or a specific Debian/user-config environment issue. High watch priority for anyone upgrading to v0.12.0.

#### 4. Key PR Progress

*One PR stands out, providing meaningful infrastructure improvement.*

1.  **[OPEN] feat(hooks): surface PostToolUse hook stderr to LLM context (#2445)**
    *   **Link:** [MoonshotAI/kimi-cli PR #2445](https://github.com/MoonshotAI/kimi-cli/pull/2445)
    *   **Description:** Author `zwpdbh` converts the `PostToolUse` hook from a fire-and-forget `asyncio.create_task` to an awaited operation. This allows hook stderr output to be captured and appended to the tool result message delivered back to the LLM.
    *   **Why it matters:** Previously, failing hooks (e.g., a linter returning an error or an API script failing) were invisible to the LLM. This PR introduces **agentic observability**, allowing the model to understand hook failures and self-correct. This is a strong architectural win for predictable agent workflows.

#### 5. Feature Request Trends

*   **Bring-Your-Own-Key (BYOK) Persistence:** The loop bug (#640) explicitly involves a custom Anthropic endpoint configured via `config.toml`. This reinforces a consistent user demand for flexible, self-hosted model authorization over the standard `/login` pathways.
*   **Agentic Non-Loop Guarantees:** The fundamental request underlying #640 is a deterministic terminal condition for file search and context ingestion. Users expect the agent to stop reading when it has enough context.
*   **Hook Ecosystem Visibility:** PR #2445 represents a growing request for hooks to be integrated into the agent's consciousness rather than existing as silent, fire-and-forget side effects.

#### 6. Developer Pain Points

*   **Agentic Infinite Loops:** The top pain point is the CLI completely hanging in an infinite file-reading loop (#640). This halts productivity entirely and requires a manual kill.
*   **v0.12.0 Regression Fears:** The immediate report of a broken edit tool (#2443) post-release is a severe stability signal for the new major version.
*   **Configuration Fragility:** Relying on a raw `config.toml` for custom endpoints (#640) indicates that the configuration experience for advanced/off-platform users is brittle and lacks proper validation or user guidance.
*   **Silent Hook Failures:** The drive behind PR #2445 highlights a structural pain point: users building complex hook pipelines were flying blind when tools failed, as errors were dropped silently.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — June 10, 2026

## Today's Highlights
**v1.17.0 shipped** with `fff`-backed file search for large projects, X-Session-Id sticky routing support, and Cohere North model integration. Community attention is sharply focused on **custom OpenAI-compatible provider reliability** (multiple high-engagement issues filed in the last 48h) and **agent sandboxing** (#2242), which remains the most active thread. On the PR front, several developer experience fixes landed for the CLI stream output, MCP error safety, and non-TTY environments, alongside a well-received `apiKey` round-robin rotation feature.

---

## Releases
### v1.17.0
_Released by @dmtrKovalenko & @songchaow_
- **Faster file search**: New `fff`-backed search engine dramatically improves file discovery across large codebases.
- **`X-Session-Id` headers**: Enables sticky routing for proxy deployments.
- **Cohere North model support**: Adds officially supported first-party integration.
- **`reasoning` interleaved field**: New option for granular control over structured reasoning output.

---

## Hot Issues
_10 noteworthy conversations from the last 24 hours_

1. **#2242 — Sandboxing agent filesystem access** (64 comments, 53 👍)  
   The most active issue. Developers want `seatbelt`-like restrictions to prevent agents from editing files outside the project directory. No equivalent exists yet in OpenCode.  
   [anomalyco/opencode#2242](https://github.com/anomalyco/opencode/issues/2242)

2. **#13984 — Copy/paste broken in CLI** (45 comments, 20 👍)  
   Persistent cross-platform clipboard bug. "Copied to clipboard" notification appears, but paste produces nothing. Affects Windows heavily.  
   [anomalyco/opencode#13984](https://github.com/anomalyco/opencode/issues/13984)

3. **#3472 — Context awareness not working** (38 comments, 26 👍, _Closed_)  
   VS Code extension advertises context awareness, but selected lines are invisible to the agent. Documentation gaps flagged.  
   [anomalyco/opencode#3472](https://github.com/anomalyco/opencode/issues/3472)

4. **#5674 — Custom OpenAI-compatible provider options silently dropped** (23 comments, 13 👍)  
   BaseURL and apiKey configured via `opencode.json` are not forwarded to API calls. Core integration friction affecting self-hosted users.  
   [anomalyco/opencode#5674](https://github.com/anomalyco/opencode/issues/5674)

5. **#20802 — Image attachments not reaching vision models through custom providers** (15 comments, 7 👍)  
   Vision workflows completely broken when using third-party OpenAI-compatible backends. Provider works fine outside OpenCode.  
   [anomalyco/opencode#20802](https://github.com/anomalyco/opencode/issues/20802)

6. **#31498 — "Extremely bad" developer prompt** (7 comments)  
   A heavy user calls out the default prompt for generating overly-verbose, hesitant agent behavior. Strong community agreement.  
   [anomalyco/opencode#31498](https://github.com/anomalyco/opencode/issues/31498)

7. **#14195 — Multiple subtask calls execute sequentially instead of parallel** (7 comments)  
   `tasks.pop()` loop forces serial execution when the LLM issues batch subtasks. Identified as a core architectural limitation.  
   [anomalyco/opencode#14195](https://github.com/anomalyco/opencode/issues/14195)

8. **#31525 — Prompt loop reloads all messages from DB every iteration, breaking prompt cache** (4 comments)  
   `filterCompactedEffect` breaks Anthropic's byte-identity prompt caching, significantly increasing latency and cost on long sessions.  
   [anomalyco/opencode#31525](https://github.com/anomalyco/opencode/issues/31525)

9. **#31579 — `@ai-sdk/anthropic` v3.0.71 rejects `fallback_message` type** (2 comments)  
   New Anthropic fallbacks API parameter causes full turn failure. Blocks Claude Fable 5 fallback configurations.  
   [anomalyco/opencode#31579](https://github.com/anomalyco/opencode/issues/31579)

10. **#30662 — Session title auto-generation silently fails for opencode provider models** (7 comments)  
    Title agent invokes `llm.stream()` without proper provider config. Left all sessions as "New session — …". Fixed in nightly.  
    [anomalyco/opencode#30662](https://github.com/anomalyco/opencode/issues/30662)

---

## Key PR Progress
_10 important pull requests active today_

1. **#31578 — `fix(cli): stream run output, add empty-text warning, flush race-late parts`**  
   Fixes three blocking CLI issues: silent exits on `opencode run`, dropped text output, and race conditions in streaming.  
   [anomalyco/opencode#31578](https://github.com/anomalyco/opencode/pull/31578)

2. **#31596 — `feat: support apiKey arrays with round-robin rotation per provider`**  
   Closes highly-requested feature #29085. Allows specifying multiple API keys for automatic rotation.  
   [anomalyco/opencode#31596](https://github.com/anomalyco/opencode/pull/31596)

3. **#31598 — `fix(cli): disable spinner animation in non-TTY environments`**  
   ANSI escape codes rendering as garbage in CI, PowerShell, and subprocesses. Adds `isTTY` check.  
   [anomalyco/opencode#31598](https://github.com/anomalyco/opencode/pull/31598)

4. **#31595 — `fix(mcp): make client creation failure-safe`**  
   Wraps MCP client initialization in proper error boundaries. Closes connected clients gracefully on tool initialization failures.  
   [anomalyco/opencode#31595](https://github.com/anomalyco/opencode/pull/31595)

5. **#31583 — `chore: Update fff to 0.9.4`**  
   Bumps `@ff-labs/fff-bun` to 0.9.4, embedding native binaries for stable cross-platform search.  
   [anomalyco/opencode#31583](https://github.com/anomalyco/opencode/pull/31583)

6. **#31599 — `refactor(provider): extract helpers from normalizeMessages`**  
   Clean extraction of Anthropic/Bedrock/Mistral/Deepseek message normalization logic. Sets up easier provider-specific patches.  
   [anomalyco/opencode#31599](https://github.com/anomalyco/opencode/pull/31599)

7. **#24943 — `feat: use small models for explore subagents`**  
   Adds intelligent fallback list to use smaller, cheaper models for file explore sub-agents when no explicit model is set.  
   [anomalyco/opencode#24943](https://github.com/anomalyco/opencode/pull/24943)

8. **#28592 — `fix(cli): handle OSC52 clipboard passthrough properly under GNU screen`**  
   Fixes tmux-only DCS wrapper assumptions. Clipboard passthrough now correctly detects GNU screen's escape sequences.  
   [anomalyco/opencode#28592](https://github.com/anomalyco/opencode/pull/28592)

9. **#30682 — `fix(opencode): preserve orphan sessions on project id drift`**  
   Git history rewrites (e.g., `rebase`) could orphan existing sessions. This conservatively recovers them via root commit SHA fallback.  
   [anomalyco/opencode#30682](https://github.com/anomalyco/opencode/pull/30682)

10. **#31392 — `feat(acp): stage edits for native review in ACP clients`**  
    Enables native file review in Agent Communication Protocol clients like Zed and Devin, allowing users to accept/reject file changes inline.  
    [anomalyco/opencode#31392](https://github.com/anomalyco/opencode/pull/31392)

---

## Feature Request Trends
_Recurring requests distilled from recent issue activity_

- **Sandboxing & Security Containment** (#2242, #9428)  
  Growing call for a `seatbelt`-equivalent to restrict agent filesystem and command execution scopes.

- **Custom Provider Hardening** (#5674, #20802, #26412, #31579)  
  The highest-volume feature area. Users want reliable configuration forwarding, vision support, and compatibility with the latest vLLM/Anthropic fallback APIs.

- **CLI/TUI Customization** (#31582, #31585, #24822)  
  Requests for configurable TUI widths, Chinese (zh-CN) language support, and dynamic terminal window naming under tmux.

- **Parallelism & Performance** (#14195, #31525)  
  Power users are hitting architectural bottlenecks: sequential subtask execution and prompt cache invalidation on every loop iteration.

- **Local-First Inference** (#31587)  
  oMLX provider PR signals strong interest in Mac-native local inference with first-class tool calling support.

---

## Developer Pain Points
_High-frequency frustrations evident from the last 24h_

- **Billing & Refund Process** (#26508, #29182)  
  Multiple complaints about confusing payment UX redirects (ZEN) and 12+ day support response times. Trust issue flagged by the community.

- **Custom Provider Fragility**  
  Each new OpenAI-compatible backend seems to expose a different gap (options, vision, tool calls, streaming validation). The current integration is too brittle for the diverse self-hosted ecosystem.

- **CLI Cross-Platform Gaps**  
  Clipboard paste is broken on Windows (#13984); terminal spinners break CI logs (#31598); stderr leaks into TUI input fields on bash timeout (#31588). Each represents a workflow blocker for different user segments.

- **Prompt Quality & Agent Behavior** (#31498, #3472)  
  Users feel the default developer prompt encourages overly talkative, overly-cautious agents. Combined with undocumented context-awareness features, this creates a mismatch between marketing claims and daily experience.

- **Session & Data Management** (#19513, #30662, #31525)  
  Exporting sessions from the Windows desktop app, auto-title failures, and DB reloads wiping prompt caches all contribute to a sense that session state handling needs a reliability pass.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-10

## Today's Highlights

Pi **v0.79.1** shipped with support for Claude Fable 5 and prompt template defaults, but the big story is the community firestorm around the new **Project Trust** feature — it drew the heaviest discussion of the day as users pushed back on the UX friction. On the PR side, maintainers landed patches for Fable 5 across multiple providers, a major new **Amazon Bedrock Mantle** provider, and several critical fixes for streaming and model path handling.

## Releases

**v0.79.1**: Enables Claude Fable 5 on Anthropic and Amazon Bedrock providers with adaptive thinking and `xhigh` effort level support. Adds positional argument defaults to prompt templates (e.g., `${1:-default}`), making reusable templates more flexible without breaking existing syntax.

# Hot Issues

1. **[#5514: Project Trust Feature Feedback](https://github.com/earendil-works/pi/issues/5514)** (Closed, 24 comments, 12 👍)  
   *Why it matters:* The most engaging issue of the day. Users find the repeated trust prompts across directories and machines highly intrusive, demanding an easier global opt-out or persistent trust lists. The maintainers responded swiftly (see PR #5549).

2. **[#4984: Interactive mode crash on transient terminal EPIPE](https://github.com/earendil-works/pi/issues/4984)** (Closed, 13 comments)  
   *Why it matters:* A critical stability regression where `edit` tool calls crashed the entire session on SIGPIPE. High comment count indicates it was a widespread daily driver issue.

3. **[#4877: Session folder collision](https://github.com/earendil-works/pi/issues/4877)** (Open, 11 comments, 2 👍)  
   *Why it matters:* A subtle but persistent bug where distinct paths (e.g., `/a/b/c/d` vs `/a-b/c-d`) hash to the same session folder, risking session state corruption for users with deep or dash-heavy project structures.

4. **[#5363: Add Amazon Bedrock Mantle OpenAI-compatible provider](https://github.com/earendil-works/pi/issues/5363)** (Open, 7 comments, 3 👍)  
   *Why it matters:* Strong demand for OpenAI-compatible model access via AWS. The existing Bedrock provider uses Converse, which is incompatible with Mantle's OpenAI API — a key enterprise gap being closed by PR #5509.

5. **[#5464: Local models — 3-5 minute "Working" latency](https://github.com/earendil-works/pi/issues/5464)** (Closed, 7 comments)  
   *Why it matters:* A major performance blocker for privacy-focused local inference users. Mid-session messages stalling for minutes erodes trust in the local model workflow.

6. **[#5350: SDK custom tool operations receive host-OS paths](https://github.com/earendil-works/pi/issues/5350)** (Open, 6 comments)  
   *Why it matters:* A critical cross-platform blocker. Custom `read`/`write` tools fail on Windows hosts targeting Linux remotes because paths are resolved to the host OS, not the remote.

7. **[#5531: Kimi.com thinking enabled despite `thinking off`](https://github.com/earendil-works/pi/issues/5531)** (Closed, 5 comments)  
   *Why it matters:* The model still spends tokens thinking even when the toggle is off. Exposes a provider compliance gap where the client-side setting is silently ignored.

8. **[#5511: Context shift compaction failure](https://github.com/earendil-works/pi/issues/5511)** (Closed, 4 comments)  
   *Why it matters:* A hard error on `/compact` at 51.1% context consumption. Automatic summarization is a core reliability feature for long sessions — this failure breaks the safety valve.

9. **[#5578: Shabang (`!`) commands not found for zsh plugins](https://github.com/earendil-works/pi/issues/5578)** (Closed, 2 comments)  
   *Why it matters:* Rapid shell command execution via `!gf` fails for zsh plugin users because Pi defaults to `/bin/bash`. A daily driver regression for plugin-dependent power users.

10. **[#5331: maxTokens maps to wrong API parameter for opencode-go](https://github.com/earendil-works/pi/issues/5331)** (Closed, 4 comments)  
    *Why it matters:* `maxTokens` is sent as `max_completion_tokens` instead of `max_tokens`, which the backend silently ignores. Users lose output length control without any error feedback.

# Key PR Progress

1. **[#5567: Fix(ai): mark Claude Fable 5 thinking off unsupported](https://github.com/earendil-works/pi/pull/5567)**  
   Nullifies the disabled-thinking payload for Fable 5, preventing 400 errors from Anthropic’s API.

2. **[#5563: Feat(ai): add Claude Fable 5 and Mythos 5 models](https://github.com/earendil-works/pi/pull/5563)**  
   Adds official model metadata marking Fable/Mythos as always-adaptive thinking, with omitted disabled-thinking and temperature payloads.

3. **[#5561: Feat(ai): add Claude Fable 5 to Amazon Bedrock](https://github.com/earendil-works/pi/pull/5561)**  
   Extends effort-based adaptive thinking to Bedrock, using `thinking.type=adaptive` with `output_config.effort` instead of the legacy budget_tokens format.

4. **[#5509: Feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/5509)**  
   A major new provider for GPT 5.5/5.4 via Bedrock Mantle’s OpenAI-compatible API. Modelled after the Azure OpenAI provider.

5. **[#5562: Fix(tui): separate list items with blank lines in loose lists](https://github.com/earendil-works/pi/pull/5562)**  
   Fixes TUI markdown rendering to comply with the CommonMark loose-list spec, improving display fidelity for documentation.

6. **[#5555: Fix(ai): attach reasoning_details streamed before tool_calls](https://github.com/earendil-works/pi/pull/5555)**  
   Fixes a data race where encrypted `reasoning_details` signatures arriving before their corresponding `tool_calls` chunk were silently dropped.

7. **[#5553: Add prompt template argument defaults](https://github.com/earendil-works/pi/pull/5553)**  
   Implements the `${N:-default}` syntax from the v0.79.1 release, with single-pass expansion and full regression coverage.

8. **[#5549: Feat(ui): Improved project approval settings](https://github.com/earendil-works/pi/pull/5549)**  
   Directly addresses the #5514 feedback: adds global enable/disable flag, parent-folder trust inheritance, and aligns config commands with the new defaults.

9. **[#5560: Fix(coding-agent): parse `:thinking` suffix from custom model IDs](https://github.com/earendil-works/pi/pull/5560)**  
   Resolves parsing ambiguity allowing users to append `:thinking` effort levels to arbitrary custom model identifiers.

10. **[#5270: Ephemeral session model and thinking level selection](https://github.com/earendil-works/pi/pull/5270)**  
    Prevents in-session model/thinking changes (Ctrl+P, Ctrl+T, `/model`) from overwriting user-global defaults unless `{ persist: true }` is explicitly passed.

# Feature Request Trends

- **Provider Expansion & Fast-Follow on New Models:** The ecosystem is moving quickly to support cutting-edge models. Fable 5, Mythos 5, Opus 4.8, and the new Bedrock Mantle provider are the dominant themes. Users expect zero-delay support for new model API surfaces.
- **Project Trust UX Overhaul:** The single loudest signal this week. The community wants global trust lists, parent-folder inheritance (like VS Code), and silent opt-out paths. PR #5549 suggests maintainers are listening closely.
- **Template & Configuration Ergonomics:** `EPHEMERAL` session config (PR #5270) and prompt template defaults (PR #5553) reflect a push for more flexible, non-mutating configuration workflows.
- **First-Run Experience:** PR #5385 (detecting terminal light/dark theme on first run) signals attention to reducing initial friction for new users.

# Developer Pain Points

- **Shell Ecosystem Incompatibility:** Zsh plugins broken via `!` commands (#5578), non-clickable links (#4180), and terminal-specific key handling regressions (kitty, Windows Terminal) erode the experience for power users with custom setups.
- **Cross-Platform Remote Development Traps:** The Windows host → Linux remote path resolution bug (#5350) highlights a systemic gap in the SDK's tool abstraction layer for heterogeneous environments.
- **Local Inference Performance:** The 3–5 minute "Working" latency for local models (#5464) is a significant adoption barrier for the privacy-conscious segment that Pi targets.
- **Provider API Compliance Churn:** Rapid model releases (Fable 5, Opus 4.8, Kimi K2.6) continuously break expected behavior around thinking toggles, context windows (#5559), and API parameter mappings, demanding constant hotfixes.
- **Session State Fragility:** Folder collisions (#4877), compaction failures (#5511), and subagent Telegram polling conflicts (#5035) collectively reduce confidence in long-running, stateful agent sessions.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest for 2026-06-10

## 1. Today's Highlights

The v0.18.0 preview cycle is underway, delivering a targeted fix for thought parts leaking into CLI copy output. The daemon/ACP transport layer sees major progress as PR #4827 achieves full REST parity, while the community is rallying around experimental Agent Team orchestration (#4844) and an interactive `/stats` dashboard (#4779). On the stability front, a high-urgency fix for terminal resize-induced scrollback corruption is now in review, and Windows PATH scoping for SYSTEM account installs gets a targeted remedy.

---

## 2. Releases

**v0.18.0-preview.0** and **v0.18.0-preview.1**

The only substantive delta: the CLI now correctly strips internal thought/reasoning tokens from copy output—a welcome fix for anyone who has inadvertently pasted reasoning fragments into their editor. Both releases share identical changelogs reflecting the same v0.17.1-based cherry-pick.

- [v0.18.0-preview.1 Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0-preview.1)

---

## 3. Hot Issues

1. **[#4891] Terminal Resize During Streaming Fragments Scrollback** (P2, macOS)  
   Resizing the window mid-generation produces output rendered at mismatched widths, with tool-call box borders cutting off at inconsistent columns. A popular topic in the last 24h—three comments and rising concern about broken scrollback discoverability.

2. **[#4864] CI: Enable Required Status Checks on Main Branch** (CLOSED, P2)  
   PR #4798 merged with all checks failing, breaking `tsc --build` on main. The root cause? A missing `});` in a test file. The fix—branch protection—is now merged, signaling a hardening of the QA process.

3. **[#4907] Down Arrow Requires 2 Presses to Reach Subagent Content** (P2, UI)  
   When a subagent tab bar is visible, the first `↓` press only skips the tab row instead of jumping to content. Small in scope but visibly disruptive for users relying on keyboard navigation in multi-agent sessions.

4. **[#4904] qwen Code Cannot Switch to Newer Models** (P2, Auth)  
   Manually switching to `qwen3.7-plus` fails with: *"Model 'qwen3.7-plus' is not available for auth type 'openai'"* although the model works in Coding Plan. Core functionality regression that blocks access to latest model offerings.

5. **[#4888] IDEA Plugin: `ask_user_question` Text Not Rendering** (P2, IDE)  
   The plugin UI shows only Submit/Cancel buttons but neither the question prompt nor the user input field. This stands out as a critical gap in the JetBrains integration experience.

6. **[#4782] ACP Streamable HTTP Transport — Implementation Status & Upgrade Plan**  
   The canonical tracking issue for the daemon's ACP transport layer. ACP-native editors (Zed, Goose, JetBrains) can connect without adapter code. Four comments signal sustained community interest in this interoperability layer.

7. **[#4901] Windows Standalone Installer: `qwen` Not Found in New Sessions** (P2, Windows)  
   When installed via SSM as SYSTEM user, the shim is written only to User PATH. A well-documented reproduction with an active fix in PR #4903.

8. **[#4889] Feature Request: In-Process MCP Server Support for Python SDK** (P2, SDK)  
   The Python SDK (0.1.x) doesn't yet embed MCP servers inside the SDK process. The `mcp_servers` option exists in `QueryOptions` but is explicitly marked as a no-op. This omission is the single biggest integration blocker for SDK consumers.

9. **[#4882] Feature Request: `terminalSequence` Field on Hooks** (P2, Hooks)  
   A direct parity request with Claude Code v2.1.141, enabling hooks to emit desktop notifications, window-title updates, and bells without needing a controlling terminal. Merged today via PR #4895.

10. **[#4615] Project-Scoped `.mcp.json` with Pending Approval Semantics** (Security, MCP)  
    A proposal for workspace-level MCP configs requiring explicit user consent before any server starts. Five comments reflect strong interest in bringing governance primitives to MCP consumption.

---

## 4. Key PR Progress

1. **[#4895] feat(hooks): terminal sequence notifications** (MERGED)  
   Directly addresses #4882. Hooks can now return a terminal sequence payload, validated against a strict allowlist, and emitted through the active notification channel. Merged within 24 hours of the feature request—impressive turnaround.

2. **[#4844] feat(core): Agent Team experimental feature** (OPEN)  
   Adds parallel sub-agent orchestration where the model creates a named team, spawns teammates that work concurrently, share a task list, and merge results. A significant leap in multi-agent capability, currently under review with steady activity.

3. **[#4890] feat(cli): `/cd` command** (OPEN)  
   Implements a workspace-changing slash command. Validates target directory, prompts before trusting new paths, updates workspace roots, and migrates the active session—answering a long-standing community ask.

4. **[#4894] fix(dual-output): prevent FIFO blocking on startup** (OPEN)  
   Fixes a silent hang when `--json-file` targets a named pipe with no reader. Switches to `O_RDWR | O_NONBLOCK` and adds a 1 MB high-water buffer. A critical fix for programmatic/TUI automation users.

5. **[#4833] feat(daemon): session idle reaper & automatic cleanup** (OPEN)  
   Two-layer lifecycle cleanup for the daemon bridge: close-on-last-detach for immediate teardown and a timeout-based reaper for orphaned sessions. Production-grade hardening for long-running daemon processes.

6. **[#4779] feat(stats): interactive `/stats` dashboard** (OPEN)  
   Three-tab interactive dashboard: Session (live metrics), Activity (usage trends), and Efficiency (TPS, tool analysis). Directly responds to #4252. A strong candidate for the next minor release.

7. **[#4919] fix(cli): debounce resize repaint and clear stale scrollback** (OPEN)  
   Replaces the per-event static repaint with a 200 ms trailing-edge debounce, solving the fragmented scrollback issue (#4891) properly. Only performs one `refreshStatic()` when resize settles.

8. **[#4902] feat(serve): cursor-based pagination for session list** (OPEN)  
   Wires pagination through REST and ACP HTTP transport. GET sessions now accepts `cursor` and `size` query params. ACP dispatch returns `nextCursor` per protocol—foundational for scalable daemon UIs.

9. **[#4880] feat(core): layered tool-output truncation** (OPEN)  
   Three-layer model for bounding tool output before it enters conversation history: single-result truncation (threshold spill to temp file), per-message budget, and cumulative budget. Mirrors Claude Code's approach to context management.

10. **[#4903] fix(installer): auto-detect SYSTEM account, default PATH to machine** (OPEN)  
    When the Windows installer detects `S-1-5-18`, PATH scope defaults to HKLM instead of HKCU, ensuring the `qwen` shim is visible in all new terminal sessions. A companion fix to #4901.

---

## 5. Feature Request Trends

- **Daemon Integration & Protocol Parity:** The ACP Streamable HTTP transport (#4782) and in-process MCP support for the Python SDK (#4889) dominate the integration conversation. Users clearly want qwen to be a first-class citizen in non-CLI toolchains (Zed, Goose, JetBrains).

- **Workspace & Session Lifecycle Management:** There is a notable push for session-level ergonomics: the `/cd` command (#4890), preserving CLI flags on background agent resume (#4884), idle session reaping (#4833), and better model switching UX (#4904, #4813).

- **Troubleshooting & Self-Diagnosis:** `--safe-mode` (#4883) and the interactive `/stats` dashboard (#4779) both speak to a maturing user base that needs introspection tools to isolate configuration issues and monitor performance.

- **Terminal UX Polish:** Optional timestamps in CLI responses (#4899), sidebar panels in the desktop app (#4885), and terminal sequence notifications (#4882) reflect an ongoing drive toward a richer, more informative terminal experience.

---

## 6. Developer Pain Points

- **Terminal Rendering Instability:** Resize-induced scrollback fragmentation (#4891) and the double-press keyboard navigation bug (#4907) are the most actively discussed UI regressions. These compound in multi-agent contexts where screen real estate changes frequently.

- **Model Switching & Provider Configuration:** The inability to switch to `qwen3.7-plus` (#4904) and the runtime prefix leak into `settings.json` (#4729) are recurring configuration landmines. Model provider `baseUrl` duplication (#4813) adds unnecessary friction for users with local vLLM or Coding Plan setups.

- **Windows as a Second-Class Platform:** From PATH scoping (#4901) to the lack of Windows self-hosted runners for CI (#4908), Windows users consistently face installation and discovery problems that macOS and Linux users don't. The SYSTEM account installer fix (#4903) addresses one facet but the broader gap remains.

- **IDE Plugin Lag:** The IDEA plugin's `ask_user_question` rendering failure (#4888) highlights a feature parity gap between the TUI and IDE experience. For organizations standardizing on JetBrains, this is a blocker for adopting agentic workflows.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

## DeepSeek TUI / CodeWhale Community Digest – 2026-06-10

### 1. Today’s Highlights
The project officially rebranded to **CodeWhale** with the v0.8.55 release, deprecating the legacy `deepseek-tui` npm package. The community is buzzing with strategic infrastructure work, including a concrete plan for a US-based remote workbench (Telegram + DigitalOcean) and a massive wave of internationalization PRs adding 7 locales. However, this rapid iteration comes with friction: the rebrand update path is broken for legacy users, agent autonomy issues are drawing significant concern, and standard UX features like auto-update detection remain missing.

### 2. Releases
**v0.8.55** — The canonical project and release-asset name is now **CodeWhale**. This release adds dedicated support for Together AI and the OpenAI Codex provider, alongside model catalog updates. Users on the legacy `deepseek-tui` package must migrate following `docs/REBRAND.md`.  
[Release Link](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.55)

### 3. Hot Issues

1. **#2942 Agent Acting Autonomously (“自问自答”)** – A critical behavioral regression where the agent takes and executes unsolicited actions, actively breaking user projects. High community engagement (6 comments).  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2942)

2. **#2935 Hippocampal Memory for Infinite Context** – An ambitious design proposal for persistent cross-session recall, aiming to replace manual `/compact` and the note tool with a long-term memory architecture.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2935)

3. **#2931 Auto-Update Version Detection** – A standard UX expectation completely absent from the current tool. Users on Homebrew or direct binary downloads have zero awareness of new releases.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2931)

4. **#2960 Broken Rebrand Update Path** – Users on the legacy `deepseek-tui` package hit hard errors with no migration guidance when attempting to update, blocking adoption of the new CodeWhale releases.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2960)

5. **#1990 Remote Workbench (US Cloudflare/AWS/Telegram Lane)** – The strategic push for a global infrastructure equivalent to the existing Tencent path, enabling phone-controlled coding for non-Chinese users.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/1990)

6. **#2641 PDF `read_file` Tool Crash** – A hard stability issue: reading a PDF without the `pages` parameter hangs the session and returns a “channel closed” error. Disrupts heavily for document-focused workflows.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2641)

7. **#2969 Missing v0.8.55 CHANGELOG** – The CHANGELOG was not updated for the major rebranding release, causing immediate confusion for users trying to understand what changed.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2969)

8. **#2922 YOLO Mode Confirmation Spam** – In YOLO mode, the agent seeks confirmation on every atomic operation, defeating the mode’s intended purpose and creating significant friction.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2922)

9. **#2937 Unreliable Background Task Cancellation** – The `Ctrl+B` background task list often shows nothing even when tasks are active, making the cancellation flow unpredictable and untrustworthy.  
   [Issue](https://github.com/Hmbown/CodeWhale/issues/2937)

10. **#2656 Sub-agent Session Name Conflicts** – Agents cannot easily diagnose or recover from session name conflicts during orchestration, revealing a gap in agent-internal debugging tooling.  
    [Issue](https://github.com/Hmbown/CodeWhale/issues/2656)

### 4. Key PR Progress

1. **#2971 Expose Matched Approval Rule Metadata** – Improves explainability by surfacing which execution policy rule triggered an approval request, without changing approval semantics.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2971)

2. **#2920 Fix Oversized Paste File Path** – Migrates the legacy `.deepseek/pastes/` directory to `.codewhale/pastes/` as part of the rebranding cleanup.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2920)

3. **#2895 Fix Siliconflow Config Mapping** – Corrects a bug where the `SiliconflowCN` provider kind mapped to the wrong TOML section, causing user configuration to be silently ignored.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2895)

4. **#2634 (Merged) Port to HarmonyOS** – Major platform expansion using conditional cfg-gating for Linux-specific surfaces, a Rustls/ring switch, and new OHOS environment scripts.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2634)

5. **#2479 (Merged) Provider Trait Architecture** – A sweeping refactoring introducing a `Provider` trait and 18 concrete structs, eliminating scattered match-arm duplication and enabling rapid provider additions.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2479)

6. **#2892 Localize Sandbox Elevation Dialog** – Part of the intensive i18n push: migrates the sandbox elevation widget from hardcoded English to `MessageId`-based translations across all 7 shipped locales.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2892)

7. **#2927 Add Qwen 3.7 Max to OpenRouter Catalog** – Rapidly adds the latest Qwen model to the model resolver and picker with alias support.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2927)

8. **#2925 Add Dedicated Together AI Provider** – Completes the v0.8.55 provider goals with a first-class Together AI profile across config, CLI/TUI, and provider picker.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2925)

9. **#1865 (Merged) Opt-in Pro Plan Routing Profile** – Adds an explicit `/mode pro-plan` profile bridging plan confirmation and execution without forcing it into the default mode cycle.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/1865)

10. **#2522 (Merged) Hard Compaction Option** – Introduces an opt-in mode that summarizes middle conversation history while preserving the system prompt and recent messages. Useful for context-heavy sessions.  
    [PR](https://github.com/Hmbown/CodeWhale/pull/2522)

### 5. Feature Request Trends

- **Global Infrastructure Parity:** The single strongest theme. Users actively drive toward a US/global equivalent (DigitalOcean, Telegram, AWS) of the existing Tencent remote workbench path for phone-controlled coding.
- **Advanced Persistent Memory:** The community wants to move beyond the 1M-token window and manual compaction toward a native, long-term memory architecture (hippocampal memory, cross-session recall).
- **Model & Platform Expansion:** Rapid provider additions (Together AI, Codex, Qwen 3.7 Max) and the HarmonyOS port signal strong demand for multi-ecosystem support.
- **Full-Feature Phone Control:** Requests for the Telegram bridge have shifted from basic connectivity to production resilience: streaming progress, typing indicators, approval deadlock fixes, and retry backoff.
- **Proactive UX Automation:** Missing quality-of-life features like auto-update detection and a guided `remote-setup` wizard are growing in demand as the user base matures.

### 6. Developer Pain Points

- **Agentic Collateral Damage:** The most acute frustrations center on the agent taking actions it was never instructed to perform (#2942) or generating excessive confirmation noise (#2922), undermining trust in autonomous modes.
- **Migration & Upgrade Grief:** The rebrand from `deepseek-tui` to `codewhale` has actively broken the update path without fallback guidance (#2960). Combined with a missing CHANGELOG for the landmark release (#2969), the upgrade experience has been rough.
- **Tooling Stability:** Specific tools like the PDF `read_file` (#2641) and background task manager (#2937) are unreliable, causing hard hangs or invisible state that stalls development flow.
- **TUI Usability Gaps:** Text overflow during long status runs (#2620), inability to see diffs before approving changes (#1846), and long status readability issues (#2914) show the TUI hasn’t fully polished for complex production workloads.
- **Internal Debugging Opacity:** Agents struggle to diagnose their own operational issues (e.g., session name conflicts in #2656, unclear tool availability in #2657), pointing to a need for richer introspection and feedback loops within the agent core.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*