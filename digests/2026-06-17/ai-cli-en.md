# AI CLI Tools Community Digest 2026-06-17

> Generated: 2026-06-17 03:46 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Development Ecosystem
**Date:** 2026-06-17

---

## 1. Ecosystem Overview

The AI CLI tools landscape on June 17, 2026 marks a decisive transition from single-session chat copilots to persistent, multi-agent runtime platforms. Across nine major projects, there is deep convergence on the Model Context Protocol (MCP) as the standard for tool interoperability, while session cost management and agent lifecycle reliability emerge as the dominant shared challenges. The ecosystem is simultaneously grappling with a pervasive cross-platform stability deficit—particularly on Windows—and a universal dependence on upstream model quality that exposes every tool to supply-chain risk. Despite these growing pains, feature velocity is accelerating across multiple projects, signaling that the market is still rapidly expanding its definition of what an AI CLI is capable of.

---

## 2. Activity Comparison

| Tool | Issue Heat (24h) | Top Engagement Signal | PR Activity (24h) | Release Status |
|---|---|---|---|---|
| **Claude Code** | Very High | #42776: 87c, 31👍 (Windows lock) | 10 Mixed (Shell inj fix, Symlink guard) | v2.1.179 |
| **OpenAI Codex** | Very High | #25749: 46c, 30👍 (MFA lockout) | 10 Mixed (Token budgets, Credential broker) | 2x Alpha |
| **Gemini CLI** | Moderate | #27973: P0 CI pipeline failure | 10 Mixed (Thought stripping, MCP OAuth fix) | ❌ Blocked |
| **GitHub Copilot CLI** | High | #3687: Windows ARM64 crash (BEX64) | 0 (Release triage focus) | v1.0.64-0 |
| **Kimi Code CLI** | Low | #2457: MCP server ghost state | 1 Open (API stringify fix) | ❌ None |
| **OpenCode** | High | #27167: 88👍 (/goal feature), #2940: 39c (hangs) | 10 Mixed (PowerShell UTF-8, LAN discovery) | ❌ None |
| **Pi (badlogic)** | Very High | #4945: 59c, 30👍 (streaming hang) | 10 Merged (HTTP error bodies, timing metrics) | v0.79.5 / v0.79.6 |
| **Qwen Code** | Very High | #3203: 136c (OAuth free tier reduction) | 10 Mixed (E2E tests merged, /loop engine) | ❌ Blocked |
| **CodeWhale** | Moderate | #2487: 14c (recurring stall bug) | 10 Mixed (Workrooms P1, musl build) | v0.8.61 (Rebrand) |

*Legend: c = comments, 👍 = reactions, P0 = highest severity*

---

## 3. Shared Feature Directions

**MCP Lifecycle Maturation (All nine tools)**
Every project is actively wrestling with MCP process lifecycle, credential rotation, server discovery, and transport reliability. Common pain points include leaked child processes (Claude #68933, Pi #5687), cached server config persisting after deletion (Kimi #2457), eager vs. deferred tool exposure (OpenCode #32621), and OAuth token refresh races (Codex #28647, Gemini #27664). The consensus is that MCP is the accepted standard, but standard lifecycle semantics are not yet settled.

**Agent Loop Budgets & Autonomy (Claude, Codex, Gemini, OpenCode, Pi, Qwen, CodeWhale)**
Universal demand for programmable agent budgets, step limits, and scope controls. Features emerging across projects: `/goal` commands (Claude, OpenCode), shared session token budgets spanning sub-agents (Codex #28494), background `/loop` wakeup engines (Qwen #5182/5197), multi-agent session switching (Pi #5700), and durable threaded "workrooms" (CodeWhale #3209/3277).

**Cost Observability & Guardrails (Claude, Codex, OpenCode, Qwen, Pi)**
"Hidden cost explosions" are the top sentiment risk. Specific vectors include 9.3M-token system prompts in WSL (Claude #65429), compaction deadlocks draining fresh quotas (Claude #68973), infinite clarification loops (OpenCode #32615), CPU-bound overhead (OpenCode #21470), and automated memory systems retrying low-signal sessions indefinitely (Gemini #26522).

**Cross-Platform Parity (All, especially Windows)**
Windows is the primary friction surface: process file locks preventing relaunch (Claude #42776), non-ASCII path crashes (Codex #27506), ARM64 BEX64 aborts (Copilot #3687), proxy tool gaps (CodeWhale #3273), and UTF-8 encoding bugs (OpenCode #31985). macOS exhibits resource leaks (Codex #27536, #25243), while Linux suffers glibc version mismatches (CodeWhale #3238, Qwen #5206).

**Security Hardening (Claude, Copilot, Gemini, Codex, Qwen)**
A clear shift toward supply-chain security: symlink escape guards (Claude #68689), shell injection fixes (Claude #68786), credential broker architectures (Codex #28034), CI audit trail validation (Gemini #27753), deterministic secret redaction before memory ingestion (Gemini #26525), and encrypted file-based secret storage (Qwen #5221).

**Observability & Diagnostics (Copilot, Pi, Gemini, OpenCode)**
Growing demand for transparency into internal agent state. Copilot ships dedicated `/diagnose` command (v1.0.64), Pi adds duration/TTFT metrics (PR #5809), Gemini builds component-level behavioral evaluations (epic #24353), and OpenCode debates tool exposure timing to understand context consumption (#32621).

---

## 4. Differentiation Analysis

- **Claude Code (Feature-Rich Incumbent):** Deepest feature surface (hooks, workflows, plugin system) but paying the tax of complexity with Opus 4.8 model regression and Windows bloat. The ecosystem has the most third-party PRs and the most vocal community around core quality.

- **OpenAI Codex (Enterprise Anchored):** Strongest focus on managed configuration, shared token budgets, and server-side exec infrastructure. The highest-stakes UX problem — complete MFA lockout (#25749) — exposes a governance gap that enterprise security teams will scrutinize.

- **Gemini CLI (Architecture Centric):** Leading in cognitive architecture safety (thought stripping via PR #27971, AST-aware methods, behavioral evals). Smallest community but highest signal-to-noise on fundamental agent behavior and safety infrastructure.

- **GitHub Copilot CLI (Ecosystem Lock-in):** Deepest GitHub platform integration (MCP registry, Security Review GA). Permissions model is under fire (coarse `--allow-all` wedge, authorization fatigue), but networking effects from the ecosystem are strong.

- **Kimi Code CLI (Minimalist Guardian):** Lowest activity and engagement. Focused on basic API spec compliance. Community signal suggests a smaller user base with limited voice.

- **OpenCode (Parity Chaser):** Ambitious multi-provider parity with Codex/Claude. Provider abstraction layer is both the primary differentiator and the primary liability — every major provider has a recently reported critical bug (DeepSeek #31849, Gemini #32625, MiniMax #32608).

- **Pi (High-Velocity Innovator):** Highest feature velocity of any project this week. Emphasis on TUI ergonomics, provider flexibility (auth scopes, proxy config), and streaming reliability. A strong bellwether for community demands.

- **Qwen Code (Automation & Cross-Ecosystem Bridge):** Unique strengths in background automation (Loop alignment) and Eastern ecosystem integration (QQ Bot adapter, Moonshot). CI/CD pipeline fragility and platform policy uncertainty (OAuth free tier reduction) are the primary drags.

- **CodeWhale (Ambitious Architect):** Betting on architectural leaps (Hippocampal Memory v2, Workrooms) but paying the toll of rebranding friction and a persistent core stall bug (#2487). High architectural ambition with execution fragility.

---

## 5. Community Momentum & Maturity

**High Velocity** — Pi, Qwen Code, OpenCode show the highest feature velocity and community churn, suggesting rapidly scaling user bases with demanding expectations for iteration speed.

**Established Heavyweights** — Claude Code and OpenAI Codex have the largest installed base and most complex institutional problems (enterprise lock-in, cost governance). Their communities surface the widest array of edge cases.

**Solidifying Core** — Gemini CLI and GitHub Copilot CLI have focused communities. Gemini trades breadth for architectural depth; Copilot leverages platform lock-in for stability but faces foundational permission model problems.

**Transitioning / Fragile** — CodeWhale shows strong architectural ambition (Workrooms, Memory v2) but is most vulnerable to core stability regressions. Kimi Code CLI has minimal community gravity, signaling either a niche use case or a stalled adoption curve.

---

## 6. Trend Signals

**1. MCP as the Universal Connector — Lifecycle is the Hidden Tax**
MCP is the uncontested standard, but server lifecycle management (spawning, OAuth refresh, crash recovery, teardown on session end) is the ecosystem's largest uncoordinated engineering burden. Every project is solving the same problem independently.

**2. The Agent Loop is the Product**
"Turn stalled," "silent hangs," and "infinite wait" are existential threats to user trust. Stream handling, tool execution resilience, and graceful error recovery are now the primary product differentiators — outpacing raw model capability in community discourse.

**3. Token Economy is UX**
Users actively monitor CPU, token, and dollar costs. Tools that lack hard budgets, transparent pricing, and compaction visibility are losing trust. The "hidden cost explosion" sentiment is the strongest negative signal across the entire ecosystem.

**4. Windows is the Frontier of Stability**
Every tool is failing on Windows in a critical dimension — crashes, encoding, process management, or proxies. A tool that solves Windows/WSL parity holistically will capture significant market share from an underserved majority.

**5. Multi-Provider Support is Mandatory but Fragile**
The era of single-model fidelity is over. The abstraction tax is heavy: DeepSeek V4 thinking quirks, MiniMax 400 errors, Moonshot schema rejections, Gemini thinking budget overrides. Provider abstraction layers require constant maintenance that strains engineering teams.

**6. Observability is the New Moat**
Dedicated diagnostic commands, latency metrics, reasoning transparency, and evaluation suites are moving from "nice-to-have" to table stakes for enterprise adoption. Trust requires knowing *why* the agent acted, spent tokens, or chose a tool.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-17 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking (by Community Attention)

*Note: The source data lists PRs sorted by comments* (50 total) *but renders comment counts as "undefined" in this snapshot. The following ordering reflects implied community engagement.*

| Rank | Skill PR | Function | Status |
|------|----------|----------|--------|
| 1 | **[document-typography](https://github.com/anthropics/skills/pull/514)** | Prevents orphan text, widowed paragraphs, and numbering misalignment in AI-generated documents—a universal quality-of-life fix for every document Claude produces. | **Open** (Created Mar 4) |
| 2 | **[ODT Skill](https://github.com/anthropics/skills/pull/486)** | OpenDocument text creation, template filling, and ODT-to-HTML conversion—directly addressing enterprise/public-sector interoperability requirements on ISO-standard formats. | **Open** (Created Mar 1) |
| 3 | **[skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** | Meta-skills evaluating structure, documentation, security, and actionability across five dimensions—foreshadows the trust-boundary governance debate in Issue #492. | **Open** (Created Nov 2025) |
| 4 | **[run_eval.py 0% recall fix](https://github.com/anthropics/skills/pull/1298)** | Solves the critical bug where `run_eval.py` reports 0% recall on every description. Directly resolves Issue #556 (12 comments)—the most-discussed bug in the repository. | **Open** (Created Jun 10) |
| 5 | **[testing-patterns](https://github.com/anthropics/skills/pull/723)** | Comprehensive skill covering testing philosophy (Testing Trophy model), unit testing patterns, React Testing Library, and end-to-end workflows. | **Open** (Created Mar 22) |
| 6 | **[ServiceNow Platform Skill](https://github.com/anthropics/skills/pull/568)** | Broad enterprise platform coverage spanning ITSM, ITOM, ITAM, SecOps, FSM, SPM, and IntegrationHub. The largest platform-specific skill submission. | **Open** (Created Mar 8) |
| 7 | **[shodh-memory](https://github.com/anthropics/skills/pull/154)** | Persistent cross-conversation memory system enabling AI agents to maintain context and structure rich memories across discontinuous sessions. | **Open** (Created Dec 2025) |
| 8 | **[AURELION Suite](https://github.com/anthropics/skills/pull/444)** | A bundled cognitive framework (kernel, advisor, agent, memory) for structured thinking and professional knowledge management—pushing beyond task skills toward agent architectures. | **Open** (Created Feb 21) |

---

## 2. Community Demand Trends

Trends extracted from the top Issues (sorted by comments, 50 total, top 15 shown):

| Theme | Evidence | Implication |
|-------|----------|-------------|
| **Stabilize the Toolchain** | Issue #556 (12 comments), #1169 (3 comments), #1061 (3 comments) all converge on `run_eval.py` reporting 0% recall and Windows subprocess failures. | Highest-priority blocker; the community cannot trust the evaluation loop, making skill optimization non-deterministic. |
| **Enterprise Sharing & Governance** | Issue #228 (14 comments) requesting org-wide skill sharing is the single most popular feature. Issue #492 (7 comments) on trust-boundary abuse and Issue #189 (6 comments) on plugin duplicates reinforce this. | Users want mature distribution channels and security validation before scaling skills across teams. |
| **Platform Interoperability** | Issue #29 (4 comments, Bedrock) and Issue #16 (4 comments, MCP protocol) ask for Skills beyond the Claude Code client. | The community treats Skills as a protocol, not an app-specific feature. |
| **Security & Compliance Patterns** | Issue #412 (6 comments, Agent Governance proposal) and Issue #1175 (4 comments, SPO access control) show demand for first-class security guardrails. | Safety patterns need to become *Skills themselves* rather than ad-hoc instructions. |
| **Agent Memory** | Implicitly validated by PR #154 (shodh-memory) and PR #444 (AURELION memory module). Issue #412 also touches on audit trails. | Persistent context is the next frontier for agent sophistication. |

---

## 3. High-Potential Pending Skills

All PRs examined are **Open**. The following have the highest likelihood of landing soon based on scope clarity and community overlap:

| Skill | PR | Estimated Impact | Key Differentiator |
|-------|----|------------------|---------------------|
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | **Universal**—every document user benefits | Solves a UX defect inherent to AI generation |
| **ODT Skill** | [#486](https://github.com/anthropics/skills/pull/486) | **Enterprise**—public sector compliance | ISO-standard format strategy |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | **Developer**—fills a clear domain gap | Aligns with modern trophy testing philosophy |
| **ServiceNow** | [#568](https://github.com/anthropics/skills/pull/568) | **Enterprise**—largest ITSM platform | Multi-domain agent coverage |
| **shodh-memory** | [#154](https://github.com/anthropics/skills/pull/154) | **Infrastructure**—cross-session persistence | Enables long-running agent identity |
| **skill-quality/security analyzers** | [#83](https://github.com/anthropics/skills/pull/83) | **Meta-level**—community governance enabler | Automated quality gating for the marketplace |
| **Masonry AI (Image/Video)** | [#335](https://github.com/anthropics/skills/pull/335) | **Creative AI**—multimodal generation | Text-to-image/video via Imagen/Veo |

Additionally, a **coordinated patch bundle** addressing platform and parsing issues (PRs [#538](https://github.com/anthropics/skills/pull/538), [#539](https://github.com/anthropics/skills/pull/539), [#541](https://github.com/anthropics/skills/pull/541), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050), [#361](https://github.com/anthropics/skills/pull/361), [#362](https://github.com/anthropics/skills/pull/362)) is running in parallel—fixing case sensitivity, Windows subprocess handling, UTF-8 panics, and YAML parsing. These are lower feature visibility but critical to infrastructure health.

---

## 4. Skills Ecosystem Insight

**One-sentence summary:**
> The community's most concentrated demand is a dual imperative—**urgently stabilize the core evaluation toolchain** (repairing `run_eval.py` 0% recall and Windows compatibility) while simultaneously **expanding into enterprise governance, platform-specific integrations (ODT, ServiceNow), secure agent memory, and org-wide distribution** to unlock professional-grade skill ecosystems beyond individual developer sandboxes.

---

# Claude Code Community Digest — 2026-06-17

## 1. Today’s Highlights
Release [v2.1.179](https://github.com/anthropics/claude-code/releases/tag/v2.1.179) lands with critical fixes for mid-stream connection drops and a WSL2 mouse-wheel scrolling regression, offering immediate relief for terminal and VS Code users. Meanwhile, the community is grappling with significant Opus 4.8 reliability issues and alarming token-cost surprises, while a large batch of open PRs from a single contributor targets Windows path normalization, plugin security, and hook development hardening.

---

## 2. Releases

- **[v2.1.179](https://github.com/anthropics/claude-code/releases/tag/v2.1.179)**
  - **Mid-stream connection drops:** Partial responses are now preserved instead of showing a raw error, and the spinner no longer gets stuck at "running tool."
  - **WSL2 mouse-wheel scrolling:** Fixed a regression from v2.1.172 affecting Windows Terminal and VS Code.
  - **Sandbox fix:** Partial fix noted for `sandbox denyR` restrictions.

---

## 3. Hot Issues

1. **[#42776](https://github.com/anthropics/claude-code/issues/42776) – Desktop Relaunch Lock (Windows)** *(87 comments, 31 👍)*  
   A persistent orphaned process file lock prevents the Claude Code desktop app from relaunching on Windows. The extreme engagement suggests this is a widespread platform-level blocker.

2. **[#65514](https://github.com/anthropics/claude-code/issues/65514) – Pro Plan Blocked for 1M Context** *(17 comments, 2 👍)*  
   Pro-plan users report being blocked from using the 1M context window despite only 17% usage, exposing friction in the new variable-cost credit model.

3. **[#63604](https://github.com/anthropics/claude-code/issues/63604) – Opus 4.8 Malformed Tool Calls** *(10 comments, 12 👍)*  
   Opus 4.8 repeatedly emits malformed `tool_use` blocks, causing entire responses to be discarded. Users report Opus 4.7 works fine, making this a high-severity model regression.

4. **[#42417](https://github.com/anthropics/claude-code/issues/42417) – Japanese Text Mojibake (Windows)** *(9 comments, 9 👍, CLOSED)*  
   The flicker-free renderer (`CLAUDE_CODE_NO_FLICKER=1`) caused UTF-8 clipboard copies in the terminal to be interpreted as CP932. Closed as fixed, a win for CJK users.

5. **[#65429](https://github.com/anthropics/claude-code/issues/65429) – 9.3M Token System Prompt Bloat (WSL/MCP)** *(9 comments)*  
   Installing the Claude Desktop app on Windows triggers a ~9.3 million token system prompt on every WSL session. A critical cost and performance issue for hybrid OS users.

6. **[#68933](https://github.com/anthropics/claude-code/issues/68933) – Skill-Creator MCP Process Leak (macOS)** *(4 comments)*  
   The `skill-creator` plugin’s eval harness shells out to headless `claude -p` processes, which boot MCP servers that never terminate, exhausting memory and forcing hard reboots.

7. **[#64235](https://github.com/anthropics/claude-code/issues/64235) – Intermittent Tool Parse Failures (macOS)** *(5 comments, 2 👍)*  
   A regression since May 29 causes "tool call was malformed" errors on valid tool_use turns. Users report the agent appears to "think for a while and then silently do nothing."

8. **[#68973](https://github.com/anthropics/claude-code/issues/68973) – Quota Drain on First Request After Reset** *(2 comments)*  
   Prompt cache expiry combined with a compaction deadlock burns 30–40% of a fresh Pro quota on the first request. Top-of-mind cost concern.

9. **[#68969](https://github.com/anthropics/claude-code/issues/68969) – Workflow Tool: Args Stringified, No Hot-Reload (Windows)** *(2 comments)*  
   Custom saved workflows receive `args` as a JSON-encoded string rather than an object, and edits do not hot-reload mid-session. Direct friction for plugin developers.

10. **[#68982](https://github.com/anthropics/claude-code/issues/68982) – Cloud Session Message Dropped (Web)** *(2 comments)*  
    A message entered an indefinite "running" state with no token consumption. After a hard refresh, the message was gone from history—indicating a server-side persistence failure.

---

## 4. Key PR Progress

1. **[#46351](https://github.com/anthropics/claude-code/pull/46351) – PowerShell Tool on macOS/Linux (CLOSED)**  
   Enables the PowerShell tool on non-Windows platforms when `pwsh` is detected, resolving a long-standing cross-platform scripting gap.

2. **[#68786](https://github.com/anthropics/claude-code/pull/68786) – Shell Injection Fix in `test-hook.sh` (OPEN)**  
   Replaces unsafe inline string interpolation with stdin redirection to prevent shell injection in the plugin-dev test harness.

3. **[#68785](https://github.com/anthropics/claude-code/pull/68785) – Hook Example Bugs (OPEN)**  
   Fixes three reference hook scripts: hook responses incorrectly written to stderr and JSON injection in examples.

4. **[#68678](https://github.com/anthropics/claude-code/pull/68678) – Triage: Don't Mark Desktop Issues Invalid (OPEN)**  
   Prevents the triage bot from auto-closing Claude Desktop issues, improving the issue intake process.

5. **[#68689](https://github.com/anthropics/claude-code/pull/68689) – Symlink Escape Guard (OPEN)**  
   Blocks symlink escape attacks in extensibility config reads, strengthening the plugin security posture.

6. **[#68694](https://github.com/anthropics/claude-code/pull/68694) – Windows Path Normalization (OPEN)**  
   Normalizes `CLAUDE_PLUGIN_ROOT` path separators on Windows, a prerequisite for reliable cross-platform plugin development.

7. **[#68699](https://github.com/anthropics/claude-code/pull/68699) – Python Wrapper & Windows Plugin Roots (OPEN)**  
   Adds a Python wrapper for hooks and normalizes plugin root paths, targeting Windows execution quirks.

8. **[#68701](https://github.com/anthropics/claude-code/pull/68701) – CRLF Strip in Python Version Probe (OPEN)**  
   Fixes a Windows-only bug where `\r` characters corrupted Python version detection in the security guidance module.

9. **[#68702](https://github.com/anthropics/claude-code/pull/68702) – Bash 3.x Compatibility (macOS) (OPEN)**  
   Guards against a `set -u` expansion error, ensuring compatibility with the legacy Bash 3.x shipped on macOS.

10. **[#68707](https://github.com/anthropics/claude-code/pull/68707) – `/bug` Command (OPEN)**  
    Introduces a new `/bug` slash command to file GitHub issues directly from the terminal, streamlining the community feedback loop.

---

## 5. Feature Request Trends

- **MCP Lifecycle & Reliability:** Users are pushing for better MCP process lifecycle management to prevent memory leaks (especially in eval harnesses), clearer stdio troubleshooting documentation, and proper server shutdown semantics.
- **Cost Visibility & Controls:** Recurring requests for hard usage caps, optional non-streaming output ([#37569](https://github.com/anthropics/claude-code/issues/37569)), and smarter agent loop limits to prevent runaway API consumption.
- **TUI Maturity:** The community wants configurable rendering modes, robust multi-byte character support (Cyrillic, CJK, emoji), and seamless keyboard protocol handling through terminal multiplexers like tmux.
- **Cross-Platform Parity:** Windows and WSL remain the top targets for feature parity requests, including file system reliability, terminal rendering, and scripting tool availability.

---

## 6. Developer Pain Points

- **Opus 4.8 Degradation:** The flagship model is generating significant frustration through malformed tool calls, slow response times, and general unreliability—eroding confidence in the core product.
- **Hidden Cost Explosions:** Developers are being blindsided by massive token-saturated system prompts, compaction deadlocks that burn fresh quotas, and agent loops that spiral out of control with no clear cost guardrails.
- **Windows & WSL Instability:** Windows continues to deliver the roughest experience: orphaned process file locks blocking relaunch, TUI text corruption for non-Latin scripts, scrolling regressions, and fragile path handling.
- **Extensibility Friction:** Plugin and workflow developers face subtle bugs (stringified arguments, shell injection vectors, broken example scripts) that slow down ecosystem growth and erode trust in the hooks system.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

Here is the OpenAI Codex community digest for June 17, 2026, based on the provided GitHub data.

---

## OpenAI Codex Community Digest | 2026-06-17

### 1. Today's Highlights
Multi-platform stability remains the dominant theme, with critical Windows crashes (non-ASCII paths, VCPkgSrv, Computer Use bootstrap) and macOS resource leaks (`code_sign_clone`, `syspolicyd` exhaustion) dominating community discussion. On the development front, the team is advancing the TUI plugin catalog, introducing shared session token budgets for agent workflows, and hardening configuration management for enterprise deployments.

### 2. Releases
Two new alpha releases were published in the last 24 hours: `rust-v0.141.0-alpha.3` and `rust-v0.141.0-alpha.4`. Changelogs were not included in the available data.

### 3. Hot Issues

1.  **Issue #25749 – Auth Recovery Blockade (46 💬, 30 👍)**
    Users with legacy phone-based MFA are completely locked out of Codex with no recovery or replacement path. This is the highest-engagement issue and represents a critical user-management failure.
    [Issue #25749](https://github.com/openai/codex/issues/25749)

2.  **Issue #25243 – macOS `syspolicyd` Exhaustion (33 💬)**
    The macOS app enters a relaunch loop that drains system file descriptors, blocking all new application launches. A critical stability bug.
    [Issue #25243](https://github.com/openai/codex/issues/25243)

3.  **Issue #21128 – Silent Conversation Hiding (27 💬, 17 👍)**
    Project conversations are silently removed from the UI once they fall outside the 50-thread window, making the Desktop app unreliable as long-term project memory.
    [Issue #21128](https://github.com/openai/codex/issues/21128)

4.  **Issue #27536 – macOS `code_sign_clone` Disk Leak (5 💬)**
    The auto-updater leaks 62GB+ into a `code_sign_clone` temp directory without cleanup.
    [Issue #27536](https://github.com/openai/codex/issues/27536)

5.  **Issue #27287 – Windows Computer Use Bootstrap Failure (9 💬, 9 👍)**
    Computer Use on Windows is broken due to a missing `@oai/sky` internal subpath export. Related issues #28121 and #28275 highlight a systemic problem with this feature on Windows.
    [Issue #27287](https://github.com/openai/codex/issues/27287)

6.  **Issue #25865 – Freeze on JSON Stack Trace Paste (9 💬, 7 👍)**
    Pasting medium-sized JSON stack traces with escaped backslashes freezes the Desktop app (Enterprise reporter). Directly impacts debugging workflows.
    [Issue #25865](https://github.com/openai/codex/issues/25865)

7.  **Issue #27506 – Windows Non-ASCII Path Crash (9 💬, 6 👍)**
    User profiles containing Korean characters crash the app on launch. A core localization bug for international users.
    [Issue #27506](https://github.com/openai/codex/issues/27506)

8.  **Issue #28095 – Archived Chat Delete Non-functional (12 💬)**
    Archived chats display a Delete button, but the action silently fails.
    [Issue #28095](https://github.com/openai/codex/issues/28095)

9.  **Issue #20567 – Windows Git Command Spam (9 💬, 1 👍)**
    The app spawns ~1000 `git` commands per minute, causing significant system load (Enterprise reporter).
    [Issue #20567](https://github.com/openai/codex/issues/20567)

10. **Issue #18052 – Context Window Exhaustion (10 💬)**
    Users are frequently hitting context limits, forcing them to clear history or start new threads. A fundamental UX friction point.
    [Issue #18052](https://github.com/openai/codex/issues/18052)

---

### 4. Key PR Progress

1.  **PR #28632 – Rollout Format Safety**
    Adds guardrails to prevent the path-types skill from accidentally modifying the internal rollout format.
    [PR #28632](https://github.com/openai/codex/pull/28632)

2.  **PR #28651 – Exec-Server Payloads Exposed**
    Makes environment registry payloads public to support external services proxying the exec-server.
    [PR #28651](https://github.com/openai/codex/pull/28651)

3.  **PR #28647 – MCP OAuth Refresh Coordination**
    Prevents race conditions when multiple clients attempt to refresh the same MCP provider token simultaneously.
    [PR #28647](https://github.com/openai/codex/pull/28647)

4.  **PR #28494 – Shared Session Token Budgets**
    Introduces an opt-in token budget spanning a root agent thread and all its descendants for predictable cost management.
    [PR #28494](https://github.com/openai/codex/pull/28494)

5.  **PR #28219 / #28189 – Tool Namespace Canonicalization**
    Core infrastructure to prevent namespace collisions among tools and establish search identity for extensions.
    [PR #28219](https://github.com/openai/codex/pull/28219) / [PR #28189](https://github.com/openai/codex/pull/28189)

6.  **PR #26703 - #26705 – TUI Plugin Catalog Rendering (Stack)**
    A three-PR stack bringing remote and shared plugin browsing to the TUI catalog, moving marketplace inventory into the main UI flow.
    [PR #26703](https://github.com/openai/codex/pull/26703)

7.  **PR #27946 – Responses Lite Tool Integration**
    Migrates tools to use `additional_tools` and developer items for compliance with the updated Responses API.
    [PR #27946](https://github.com/openai/codex/pull/27946)

8.  **PR #28409 – Managed Config Hardening**
    Enforces exact values for enterprise-managed configuration fields (e.g., `sqlite_home`, `log_dir`) to prevent drift.
    [PR #28409](https://github.com/openai/codex/pull/28409)

9.  **PR #28034 – Experimental Local Credential Broker**
    Moves credentials behind a managed network proxy to prevent exfiltration by child processes. An important step toward a more secure architecture.
    [PR #28034](https://github.com/openai/codex/pull/28034)

10. **PR #28638 – TurnContext Cleanup**
    Removes redundant and dead fields from `TurnContext` to eliminate split-brain states between config and metadata.
    [PR #28638](https://github.com/openai/codex/pull/28638)

---

### 5. Feature Request Trends
Developer demand strongly favors **workflow continuity and workspace flexibility**:
- **TUI Agility:** Strong support for a `/cwd` slash command to switch working directories without restarting the TUI session (#12464, 21 👍).
- **Workspace Defaults:** Configurable default parent folder for "Start from scratch" projects (#19913, 26 👍).
- **Remote Workspaces:** First-class SSH remote workspace support within Codex Desktop, rather than relying on a manual CLI workaround (#21509).
- **IDE Extensibility:** The ability to open Codex chat sessions in a separate VS Code window (#16615, 12 👍).

---

### 6. Developer Pain Points
The recurring high-friction issues highlight **fragile cross-platform stability and unreliable session management**:
- **Windows Instability:** A confluence of launch crashes (non-ASCII paths, VCPkgSrv), persistent Computer Use failures, and runaway background processes creates a brittle experience for Windows users.
- **macOS Resource Exhaustion:** The app fails to clean up after itself, consuming excessive disk space (`code_sign_clone`) and file descriptors (`syspolicyd`).
- **Session & UI Unreliability:** Conversations are silently dropped from the sidebar, archive management is broken, and history replays are incomplete.
- **Authentication Dead Ends:** The complete lack of a recovery path for legacy phone MFA (#25749) is the single highest-stakes UX problem, threatening total platform access for affected users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-17

## 1. Today's Highlights
The nightly release workflow is down ([#27973](https://github.com/google-gemini/gemini-cli/issues/27973) / P0), blocking all automated builds for `v0.48.0-nightly`. On the quality front, a surgical fix for **thought leakage** ([PR #27971](https://github.com/google-gemini/gemini-cli/pull/27971)) lands to stop the model's internal monologue from spilling into conversation history, which has been causing confusion loops. Agent reliability remains the community's loudest concern — the top-voted open issue ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409), 8 👍) still reports agents hanging indefinitely on simple tasks.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues

1. **[#27973](https://github.com/google-gemini/gemini-cli/issues/27973) — Nightly Release Failed (P0)**  
   The `v0.48.0-nightly.20260617` pipeline is broken. Blocks all downstream testing and integration. Zero community engagement yet (bot-reported), but this is the team's top priority today.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever (P1)**  
   Users report `gemini-cli` hangs indefinitely when deferring to sub-agents. 8 👍 — the highest community reaction on the board. Workaround is to disable sub-agents entirely.

3. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery falsely reports "GOAL success" (P1)**  
   `codebase_investigator` returns a success status even when MAX_TURNS cuts it off before doing any work. Erodes trust in agent results.

4. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command execution gets stuck on "Waiting input" (P1)**  
   3 👍. A simple CLI tool executes successfully but the UI shows the command as still active. Frequent enough to be a common workflow breaker.

5. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component level evaluations (P1 / Epic)**  
   Tracks the growth of behavioral evaluation tests (76 tests, 6 models). The team is formalizing quality gates for the agent system. Strategic importance is high even with low public commentary.

6. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping (P2 / Epic)**  
   Proposes replacing naive file reads with AST-grounded tools to reduce token waste and improve method-boundary accuracy. Signals a major architectural direction.

7. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini does not use skills/sub-agents autonomously (P2)**  
   Users can define skills, but the model ignores them unless explicitly instructed. Undermines the core customization promise of the platform.

8. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Add deterministic redaction to Auto Memory (P2)**  
   Privacy concern: local transcripts are sent to the extraction model *before* redaction. Community will watch this closely for security responses.

9. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely (P2)**  
   The background extractor revisits skipped sessions forever because they aren't marked as processed unless a `read_file` succeeds. Inefficient and resource-wasteful.

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior (P2)**  
    Users report the model using `git reset --force` when safer alternatives exist. 1 👍. Raises safety flags for production data integrity.

## 4. Key PR Progress

1. **[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) — Strip thoughts from scrubbed history turns**  
   A critical cognitive architecture fix. Internal reasoning monologues were leaking into plaintext history, confusing the model and causing infinite loops. Closed.

2. **[#27966](https://github.com/google-gemini/gemini-cli/pull/27966) — Case-insensitive sensitive path blocklist**  
   Hardens the blocklist for `.git`, `.env`, `node_modules` against prompt injection via case-manipulation. Production-grade security fix.

3. **[#27948](https://github.com/google-gemini/gemini-cli/pull/27948) — Pin dependencies and enforce 14-day update cooldown**  
   Supply chain hardening. Stops `^` ranges and mandates a 14-day wait on automated updates. Will reduce regression risk from aggressively auto-updated deps.

4. **[#27964](https://github.com/google-gemini/gemini-cli/pull/27964) — Scope MCP resource resolution**  
   Prevents cross-server URI shadowing. If two MCP servers expose the same URI, resolution now fails closed instead of silently routing to the wrong server.

5. **[#27643](https://github.com/google-gemini/gemini-cli/pull/27643) — Fix parallel workspace build race condition**  
   Splits the monorepo build into sequential topological stages (Core → Libraries → Apps). Eliminates nondeterministic CI failures. Closed.

6. **[#27753](https://github.com/google-gemini/gemini-cli/pull/27753) — Validate `workflow_run` origin in CI**  
   Blocks the `trigger_e2e.yml` fork artifact poisoning attack vector. Repository secrets were at risk. Still open.

7. **[#27664](https://github.com/google-gemini/gemini-cli/pull/27664) — Write MCP OAuth tokens atomically**  
   Uses a temp-file + atomic rename pattern to prevent token corruption from partial writes. Closes a data-integrity gap in MCP auth flows.

8. **[#27889](https://github.com/google-gemini/gemini-cli/pull/27889) — Refresh MCP OAuth with stored client ID**  
   Fixes the `/mcp auth` refresh path for auto-discovered servers where `clientId` isn't in static config. Stops silent auth failures.

9. **[#27763](https://github.com/google-gemini/gemini-cli/pull/27763) — Document `read_file` 20MB limit**  
   Addresses recurring user confusion with official docs for the file size cap. Small but high-impact for DX.

10. **[#27771](https://github.com/google-gemini/gemini-cli/pull/27771) — Fix MCP header encoding for non-ASCII values**  
    MCP HTTP transport now handles Unicode header values (e.g., `mąka`) via proper `ByteString` encoding. Clears a cross-region localization bug.

## 5. Feature Request Trends

- **AST-Aware Tooling**  
  A dedicated epic ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) calls for replacing naïve file reads and searches with syntax-tree aware tools. The goal is sharper method-boundary reads, less wasted context, and more structured codebase mapping.

- **Agent Self-Awareness & Control**  
  [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) asks that the agent understand its own CLI flags, hotkeys, and execution mechanics so it can serve as its own expert guide.

- **Proactive Safety Guardrails**  
  Multiple requests ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672), [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)) want the agent to automatically avoid dangerous commands (`git reset --force`, risky DB mutations) and prefer safe alternatives.

- **Evaluation Infrastructure Maturity**  
  The drive for reliable eval tests is loud ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353), [#23166](https://github.com/google-gemini/gemini-cli/issues/23166), [#23313](https://github.com/google-gemini/gemini-cli/issues/23313)). The team is building component-level behavioral evals to prevent regressions across the 6 supported models.

- **Memory System User Agency**  
  Users want control over what Auto Memory ingests, how invalid patches are surfaced (not silently skipped), and deterministic pre-redaction of secrets ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).

## 6. Developer Pain Points

- **Agent Hangs and Freezes**  
  The #1 pain point by community votes (8 👍 on [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)). Agents freeze indefinitely on trivial tasks. The standard workaround — disabling sub-agents — defeats the product's main value prop.

- **False Positive Reporting**  
  [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) highlights a UX trust crisis: an agent hitting MAX_TURNS reports "GOAL success," hiding the interruption.

- **Unexpected Subagent Activation**  
  [#22093](https://github.com/google-gemini/gemini-cli/issues/22093) reports a `v0.33.0` regression where sub-agents activate without user permission. Violates configuration expectations and safety boundaries.

- **Shell Command Flakiness**  
  [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) shows commands finishing but the UI hanging on "Awaiting user input." Common enough to be a consistent source of developer frustration.

- **Secrets Exposure Before Redaction**  
  [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) describes how Auto Memory sends unredacted content to the extraction model — privacy teams will flag this aggressively.

- **Scenario Bloat & Tool Limits**  
  [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) exceeds the API limit (>128 tools → 400 error). The model lacks built-in scoping over its own available toolkit.

- **Scratchpad & Monologue Contamination**  
  Addressed by [PR #27971](https://github.com/google-gemini/gemini-cli/pull/27971), but this cognitive leakage has been silently degrading conversation quality for many users. Expect relief once the fix ships.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-17

**1. Today’s Highlights**
Release v1.0.64-0 went out today, bringing the new `/diagnose` command, GA of `/security-review`, and deeper MCP integration (registry support, plugin discovery, CSV output). Despite this progress, the issue tracker is unusually active with severity bugs: a debilitating Windows ARM64 crash under load (#3687), a regression isolating subagents from MCP tools (#3812), and a permission-scope leak that can wedge the entire TUI (#3825) have all been reported or updated in the last 24 hours.

**2. Releases**
**v1.0.64‑0** — *released 2026‑06‑17*

- **New `/diagnose`** command for collecting and analyzing session logs.
- **MCP expansion:**
  - `/mcp registry` installation for browsing and installing MCP servers.
  - Installed plugins automatically expose their MCP servers.
  - CSV output support for MCP tools.
- **GA:** `/security-review` is now available to all users without `--experimental`.
[Release](https://github.com/github/copilot-cli/releases/tag/v1.0.64-0)

**3. Hot Issues**
*10 notable items with the highest community impact or severity.*

- **[#3687](https://github.com/github/copilot-cli/issues/3687)** — `copilot.exe` hard‑aborts (BEX64 / 0xc0000409) on Windows ARM64 under load. Most reproducible during multi‑session restore with memory pressure. *Community reaction:* 5 comments, high urgency, persists across 1.0.57 and 1.0.60.
- **[#3828](https://github.com/github/copilot-cli/issues/3828)** — `ContentExclusionFilter.isExcluded` crashes with `TypeError: Cannot read properties of undefined`. Blocks non‑interactive / tool pipelines. *Community reaction:* 1 comment, flagged as a critical blocking crash.
- **[#3812](https://github.com/github/copilot-cli/issues/3812)** — Subagents can no longer access MCP tools. Previously working regression; downgrading does not restore it. *Community reaction:* User filed explicit regression report.
- **[#3825](https://github.com/github/copilot-cli/issues/3825)** — `--allow-all` read permissions leak to the UI dispatcher, wedging the TUI on `-i` / `--resume` startup (no input box). *Community reaction:* Detailed bug report, critical blocker for non‑interactive sessions.
- **[#1168](https://github.com/github/copilot-cli/issues/1168)** — Excessive authorization prompts per high‑level request (“authorization fatigue”). One request triggered over a dozen pop‑ups. *Community reaction:* Long‑standing issue (Jan 2026), highly frustrating for daily users.
- **[#3824](https://github.com/github/copilot-cli/issues/3824)** — Sub‑agents silently run a different model than the configured session model via agent‑type defaults or experiment overrides. *Community reaction:* No surfacing mechanism, erodes trust in the tool’s transparency.
- **[#3823](https://github.com/github/copilot-cli/issues/3823)** — Reasoning effort `xhigh` silently downgrades to `medium` (instead of clamping to `max`) on models that don’t support the level. *Community reaction:* Users cannot detect the silent fallback.
- **[#3821](https://github.com/github/copilot-cli/issues/3821)** — Running `/update` from a resumed session leaves conflicting `--session-id` and `-r` flags, preventing the session from resuming after update. *Community reaction:* Reproducible, breaks the update flow for long‑running sessions.
- **[#3826](https://github.com/github/copilot-cli/issues/3826)** — “Operation cancelled by user” is re‑injected as a new user message after cancelling a turn, confusing the agent. *Community reaction:* Disrupts the core conversation loop.
- **[#3730](https://github.com/github/copilot-cli/issues/3730)** — Enterprise‑managed custom models are available in VS Code but invisible in Copilot CLI. *Community reaction:* 4 👍, blocks wider enterprise adoption.

**4. Key PR Progress**
No pull requests were merged or updated in the last 24 hours. Project activity over this window has focused entirely on the v1.0.64‑0 release cut and heavy triage of the newly filed bug reports above.

**5. Feature Request Trends**
- **MCP ecosystem management:** Strong demand for automation of plugin maintenance—users want a single command to update all installed plugins at once (#3830) and asynchronous execution for read‑only queries like `/mcp show` (#3829). The protocol detection gap for HTTP‑type MCP servers (misidentified as SSE) also remains unresolved (#2790).
- **Session lifecycle controls:** Users are asking for the ability to unarchive/restore accidentally archived project sessions (#3518), indicating sessions are treated as long‑lived assets that need safer state management.
- **Enterprise parity:** The inability to use centrally configured custom models in the CLI (#3730) is a recurring theme, alongside requests for repository‑level configuration of `skillDirectories` (#3822).
- **Model transparency:** A clear pattern of users demanding *explicit* surfacing of which model/reasoning‑effort is being used by sub‑agents or after fallback (#3824, #3823).

**6. Developer Pain Points**
- **Windows ARM64 Instability:** A fatal, reproducible crash under load (#3687) is the most critical stability issue on the board for users on that architecture.
- **Permission‑Scope Leaks:** The `--allow-all` wedge bug (#3825) and the chronic authorization‑fatigue pattern (#1168) point to a permission model that is too coarse and too noisy.
- **Hidden Behavior / No Observability:** Silent model downgrades, sub‑agent model mismatches, and permission leaks without any user‑visible warning (#3824, #3823, #3825) create deep distrust in the tool’s predictability.
- **Cancellation UX:** “Operation cancelled by user” being treated as a user message (#3826) breaks the fundamental interactive loop in a confusing way.
- **Plugin Update Friction:** Updating plugins one‑at‑a‑time is a recurring chore that developers want eliminated (#3830).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for 2026-06-17, synthesized strictly from the provided repository activity.

---

# Kimi Code CLI Community Digest — 2026-06-17

## 1. Today’s Highlights
Activity on the `MoonshotAI/kimi-cli` repository was narrowly focused today, but the signal-to-noise ratio was high. No releases landed, but a critical API compatibility PR (#1771) aims to resolve a persistent 400 error for tool users, while two new issues (#2456, #2457) reveal sharp pain points in onboarding and MCP state management. The long-dormant discussion on agent step limits (#1327) also resurfaced, hinting that users are outgrowing the CLI’s default autonomy guardrails.

## 2. Releases
No new releases were published in the last 24 hours. The latest stable channel remains the version users are currently running (v0.15.0 referenced in #2457, v1.47.x referenced in #2456).

## 3. Hot Issues
*Only 4 issues were updated in the last 24 hours. Below is a deep dive into each, as they represent the entire set of community friction surfacing today.*

- **#1327 — More Steps per Turn By Default**  
  *Link:* [Issue #1327](https://github.com/MoonshotAI/kimi-cli/issues/1327)  
  *Why it matters:* The default limit of 100 steps often terminates agent loops while memory is still underutilized (user reports 34.5% context usage at cutoff). This is a recurring wedge between ambitious agent workflows and out-of-box defaults. The lack of recent upvotes (0 👍) suggests it’s a simmering annoyance rather than a daily crisis for most, but high-context users are clearly hitting the ceiling.  
  *Community Reaction:* 3 comments, no new ones today—stale but still relevant.

- **#1632 (CLOSED) — Option to Hide Thinking Content**  
  *Link:* [Issue #1632](https://github.com/MoonshotAI/kimi-cli/issues/1632)  
  *Why it matters:* This feature request was closed today. Users want the ability to suppress the “Thinking...” spinner and grey italic chain-of-thought text when using models like `kimi-k2-thinking-turbo`. The closure without a visible public resolution is notable—the team may be deprioritizing it or solving it via a different mechanism.  
  *Community Reaction:* 3 👍 indicate moderate desire. The close may cause some friction if users feel silenced, but the issue has no open debate today.

- **#2457 — Auto-Discovery of Deleted MCP Servers Causing 400 Errors**  
  *Link:* [Issue #2457](https://github.com/MoonshotAI/kimi-cli/issues/2457)  
  *Why it matters:* A critical state management bug. After a user deletes an MCP server configuration, the CLI continues to auto-discover and contact it, resulting in permanent, unfixable 400 errors. For a tool where agentic capability depends on reliable MCP toolchains, this is a show-stopping defect that can break complex sessions until a workaround is found.  
  *Community Reaction:* Brand new issue, 0 comments yet. Expect high engagement once maintainers pick it up, as MCP lifecycle is a hot topic for dev tool agents.

- **#2456 — Fresh Install “LLM not set” with No Guidance**  
  *Link:* [Issue #2456](https://github.com/MoonshotAI/kimi-cli/issues/2456)  
  *Why it matters:* A pure onboarding regression. `brew install kimi-cli` followed by any command (e.g., `kimi --print`) fails with the opaque error `LLM not set`. The CLI offers no hint to run `kimi login` or similar setup. This is a high-friction first-run experience that can cause immediate churn.  
  *Community Reaction:* Very new, no comments. Likely to gather quick traction as an obvious UX fix.

## 4. Key PR Progress
*Only 1 pull request was updated in the last 24 hours. It is a high-value maintenance fix.*

- **#1771 — fix: always stringify tool message content in Chat Completions provider**  
  *Link:* [PR #1771](https://github.com/MoonshotAI/kimi-cli/pull/1771)  
  *Author:* he-yufeng  
  *Status:* Open  
  *Why it matters:* Fixes a compliance bug with the OpenAI Chat Completions API. When tool outputs contain multiple `ContentPart`s (e.g., a system reminder alongside the actual text), the API rejects the message with a `400: Fail...` because `content` must be a **string** for `role: "tool"`. This PR ensures the tool result is always stringified, unblocking users who rely on complex tool chains.  
  *Community Reaction:* No comments, but it directly resolves issue #1762 (a blocker for high-frequency tool users). It’s a “plumbing” fix that will improve reliability for everyone using agents with tool loops.

## 5. Feature Request Trends
Drawing from today’s issue activity, three clear community desires stand out:

- **Deeper Agent Autonomy (#1327):** Users are pushing the CLI beyond its default 100-step limit. The core request is for smarter defaults—limiting by context window usage or output quality rather than a hard step floor.
- **UI/UX Verbosity Controls (#1632):** There is a latent demand to toggle reasoning model outputs. While this specific request was closed, the underlying need (configurable display of chain-of-thought) remains unaddressed at scale.
- **Better Out-of-Box Onboarding (#2456):** The `LLM not set` error is a failure of DX. The community expects guided setup (a la `gh auth login` or `wandb login`), where the CLI detects an unauthenticated state and prompts the user, rather than dumping an abstract error.

## 6. Developer Pain Points
- **MCP Server State Mismanagement (#2457):** Deleting a server config doesn’t actually stop the CLI from using it, rendering the MCP system unreliable in dynamic environments. This is a top-tier reliability issue for power users.
- **Opaque First-Run Errors (#2456):** Cryptographic error messages (`LLM not set`) destroy trust and increase support burden.
- **Conservative Step Defaults (#1327):** The 100-step cap feels arbitrary and forces users to edit config files before they can complete complex tasks, disrupting flow state.
- **Upstream API Strictness (#1771):** Non-string `content` fields in tool messages trigger silent or confusing 400 errors, making debugging tool loops much harder than necessary.

---
*Digest generated from the last 24 hours of activity on the `MoonshotAI/kimi-cli` repository. Overall volume was low, but the issues surfaced represent genuine, high-impact friction points for the developer community.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest (2026-06-17)

**Data Source:** [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## 1. Today's Highlights

- A major push for Codex CLI parity is underway, with critical fixes landing for the OpenAI OAuth context flattening bug ([#32505](https://github.com/anomalyco/opencode/issues/32505) / [#32592](https://github.com/anomalyco/opencode/pull/32592)) and an ongoing discussion about MCP tool exposure timing ([#32621](https://github.com/anomalyco/opencode/issues/32621)).
- Provider integration remains a hot topic as users report bugs with MiniMax M3 rejecting tool history ([#32608](https://github.com/anomalyco/opencode/issues/32608)), Gemini thinking budgets ([#32625](https://github.com/anomalyco/opencode/issues/32625)), and DeepSeek edit tool failures ([#31849](https://github.com/anomalyco/opencode/issues/31849)).
- User frustration is mounting around client stability (hanging [#2940](https://github.com/anomalyco/opencode/issues/2940)), cost control (CPU-bound [#21470](https://github.com/anomalyco/opencode/issues/21470)), and basic UX regressions (clipboard [#7048](https://github.com/anomalyco/opencode/issues/7048), image reading [#25832](https://github.com/anomalyco/opencode/issues/25832)).

## 2. Releases

No new releases in the last 24 hours.

## 3. Hot Issues

Top 10 issues by community engagement in the last 24 hours:

1. **[#27167](https://github.com/anomalyco/opencode/issues/27167) [Feature] Add native session goals with `/goal`**  
   *Why it matters:* The highest-requested feature this week (88 👍), aiming to replace verbose prompts with a persistent lifecycle command for managing model intent. Very positive community reception.

2. **[#2940](https://github.com/anomalyco/opencode/issues/2940) [Bug] OpenCode hangs randomly after receiving instructions**  
   *Why it matters:* A critical stability crisis (39 comments) requiring force restarts. The `/compact` command only sometimes helps. Top stability concern for Laravel-based projects.

3. **[#7048](https://github.com/anomalyco/opencode/issues/7048) [Bug] Copy text clipboard functionality broken**  
   *Why it matters:* Standard UX on Linux/GhostTTY is broken—users cannot copy from input or output windows despite the "Copied to clipboard" toast appearing.

4. **[#25832](https://github.com/anomalyco/opencode/issues/25832) [Bug] Cannot read images anymore**  
   *Why it matters:* A regression in vision capabilities broke established workflows for analyzing images to modify HTML/CSS. Affects anyone relying on multimodal features.

5. **[#21470](https://github.com/anomalyco/opencode/issues/21470) [Bug] OpenCode is heavily CPU-bound**  
   *Why it matters:* Financial and performance implications. User reports 1.5 million CPU ticks versus $8.30 in token costs, indicating significant local processing overhead.

6. **[#22129](https://github.com/anomalyco/opencode/issues/22129) [Bug] Skills missing from TUI autocomplete**  
   *Why it matters:* Platform parity bug. Skills are a central feature but invisible in the TUI, undermining the skill workflow for terminal users. 12 👍, exact code location identified.

7. **[#31849](https://github.com/anomalyco/opencode/issues/31849) [Bug] DeepSeek edit tool fails frequently**  
   *Why it matters:* Provider-specific integration issue where the `edit` tool fails to invoke for DeepSeek model users. Reported with detailed error screenshots.

8. **[#32625](https://github.com/anomalyco/opencode/issues/32625) [Bug] Gemini 3.5 Flash locked to minimal thinking budget**  
   *Why it matters:* Bug in the thinking effort resolution logic locks Gemini users out of higher reasoning budgets. Filed with a specific code-level fix suggestion.

9. **[#32615](https://github.com/anomalyco/opencode/issues/32615) [Bug] Infinite clarification/compaction loop on empty git repo**  
   *Why it matters:* Cost-control bug. On a project with only `.git/`, OpenCode enters an infinite clarification loop burning tokens. Filed as both a correctness and cost bug.

10. **[#32621](https://github.com/anomalyco/opencode/issues/32621) [Bug] OpenCode eagerly exposes MCP tools unlike Codex**  
    *Why it matters:* Architectural parity issue. Eagerly exposing all connected MCP tools at turn-construction time increases visible context compared to Codex's deferred approach. Filed by a developer tracking host-runtime parity.

## 4. Key PR Progress

10 important pull requests updated in the last 24 hours:

1. **[#31985](https://github.com/anomalyco/opencode/pull/31985) fix(shell): PowerShell UTF-8 command wrapper on Windows**  
   Closes 5 Windows-specific encoding issues. A massive UX win for Windows developers.

2. **[#32592](https://github.com/anomalyco/opencode/pull/32592) fix(opencode): structured system messages on OAuth path**  
   Directly addresses the critical code path divergence in #32505. Ensures consistent system context handling between OAuth and non-OAuth requests.

3. **[#32609](https://github.com/anomalyco/opencode/pull/32609) fix(provider): stub orphan MiniMax tool results**  
   Hotfix for the MiniMax session rejection issue (#32608). Stubs orphan tool call results to prevent 400 errors on model switch.

4. **[#32624](https://github.com/anomalyco/opencode/pull/32624) fix(shell): external_directory check for redirect targets**  
   Security hardening. Ensures shell redirects (`>`, `>>`) respect the `external_directory` permission boundary.

5. **[#31848](https://github.com/anomalyco/opencode/pull/31848) fix(desktop): server-side picker for HTTP connections**  
   Fixes `directoryPickerKind` logic to correctly use the server-side file picker over HTTP connections.

6. **[#32604](https://github.com/anomalyco/opencode/pull/32604) fix(session): preserve reasoning part type on model switch**  
   Prevents heavy cache invalidation delays caused by differing reasoning part types between models.

7. **[#26861](https://github.com/anomalyco/opencode/pull/26861) fix(tui): old messages disappearing in long sessions**  
   Implements lazy-loading scrollback to prevent message loss in long TUI sessions.

8. **[#23501](https://github.com/anomalyco/opencode/pull/23501) fix: OpenAI-compatible provider improvements**  
   Long-standing PR unifying system messages, image support, and stream interruption fixes for Ollama and local models.

9. **[#27554](https://github.com/anomalyco/opencode/pull/27554) feat(opencode): local LAN provider discovery**  
   Major feature adding mDNS-based server discovery in the `/connect` flow, greatly simplifying local LLM setup.

10. **[#7756](https://github.com/anomalyco/opencode/pull/7756) feat(task): subagent-to-subagent delegation**  
    Ambitious architectural feature enabling nested agent sessions with token budgets, persistence, and hierarchical session navigation. Closes 3 related issues.

## 5. Feature Request Trends

The following high-level feature directions are consistently requested across recent issues:

- **Agentic Workflow Commands:** Strong demand for native lifecycle commands like `/goal` ([#27167](https://github.com/anomalyco/opencode/issues/27167)) and `/loop` ([#18001](https://github.com/anomalyco/opencode/issues/18001)) to manage task scope and iterative execution without verbose prompting.
- **Plugin & Skill Ecosystem Depth:** Requests for a middleware-style plugin pipeline ([#5148](https://github.com/anomalyco/opencode/issues/5148)) and better TUI skill management—specifically recursive discovery and multi-skill selection ([#21495](https://github.com/anomalyco/opencode/issues/21495)).
- **Desktop & IDE Deepening:** A push for more integrated IDE features, such as reliable "Context Awareness" in VSCode ([#22235](https://github.com/anomalyco/opencode/issues/22235)) and configurable panel layouts in the desktop app ([#16349](https://github.com/anomalyco/opencode/issues/16349)).
- **Pricing Tier Flexibility:** Go-tier users are hitting monthly caps and requesting premium add-ons or structured Pro plans with discount options ([#24879](https://github.com/anomalyco/opencode/issues/24879), [#32605](https://github.com/anomalyco/opencode/issues/32605)).

## 6. Developer Pain Points

Recurring frustrations derived from high-frequency and high-engagement issues:

- **Client Stability (Hanging/Unresponsive):** The highest-comment bug this week ([#2940](https://github.com/anomalyco/opencode/issues/2940), 39 comments) describes random hangs requiring forceful termination—a critical blocker with no universal fix.
- **Provider Integration Fragility:** Every major provider has a critical recently-reported bug (DeepSeek [#31849](https://github.com/anomalyco/opencode/issues/31849), Gemini [#32625](https://github.com/anomalyco/opencode/issues/32625), MiniMax [#32608](https://github.com/anomalyco/opencode/issues/32608), LM Studio [#2047](https://github.com/anomalyco/opencode/issues/2047), Llama.cpp [#11286](https://github.com/anomalyco/opencode/issues/11286)). This indicates a high maintenance tax on the provider abstraction layer.
- **Performance & Cost Bleed:** Users actively monitor resource consumption, reporting high CPU overhead ([#21470](https://github.com/anomalyco/opencode/issues/21470)), infinite loops burning tokens ([#32615](https://github.com/anomalyco/opencode/issues/32615)), and prompt cache misses caused by daily date strings ([#32622](https://github.com/anomalyco/opencode/issues/32622)).
- **TUI/Desktop Regression Risk:** Basic UI mechanics frequently break—clipboard ([#7048](https://github.com/anomalyco/opencode/issues/7048)), illegal instruction startup ([#8345](https://github.com/anomalyco/opencode/issues/8345)), file watchers on system roots ([#32610](https://github.com/anomalyco/opencode/pull/32610)), and project path persistence ([#30697](https://github.com/anomalyco/opencode/issues/30697))—eroding trust in client reliability.
- **Architectural Parity Anxiety:** Divergence between OpenCode's native stack and the Codex CLI parity path (eager MCP tools [#32621](https://github.com/anomalyco/opencode/issues/32621), OAuth context flattening [#32505](https://github.com/anomalyco/opencode/issues/32505)) raises concerns about maintaining two subtly different execution stacks.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-17

*Data source: [`github.com/badlogic/pi-mono`](https://github.com/badlogic/pi-mono)*

---

## 1. Today's Highlights
Pi shipped two releases (v0.79.5, v0.79.6) today, bringing provider-scoped environment overrides to `auth.json` and fixing HTTP dispatcher/DeepSeek V4 thinking configurations. The community is laser-focused on streaming reliability—the top issue ([#4945](https://github.com/earendil-works/pi/issues/4945)) describing persistent "Working..." hangs has 30 👍 and 59 comments. A welcome fix for raw HTTP error body preservation ([#5820](https://github.com/earendil-works/pi/pull/5820)) merged today promises to vastly improve proxy/gateway debugging.

---

## 2. Releases

- **v0.79.5** – Feature release. API key entries in `auth.json` can now include an `env` object for provider-specific overrides (Cloudflare, Azure OpenAI, Vertex, Bedrock, cache retention, proxy) without touching the project shell.
- **v0.79.6** – Bug fix release. Corrected the HTTP dispatcher to respect a caller's deliberate `fetch` override instead of silently reinstalling the undici global. Fixed inherited DeepSeek V4 thinking-off requests so they properly send `thinking: { type: "disabled" }`.

---

## 3. Hot Issues

1. **[#4945 – openai-codex Connection Reliability](https://github.com/earendil-works/pi/issues/4945)**
   *59 comments, 30 👍*
   The hottest thread right now. `openai-codex`/`gpt-5.5` leaves the TUI stuck on "Working..." with no streamed text, no tool call, no visible error. Recovery requires pressing Escape to abort the turn. Regular occurrences over several days.

2. **[#4877 – Session folder collision](https://github.com/earendil-works/pi/issues/4877)**
   *19 comments*
   Paths with hyphens collide in session storage (e.g., `/a/b/c/d` vs. `/a-b/c-d` end up in the same folder). A ticking time bomb for users with deeply nested or specially named repos.

3. **[#5687 – pi list and pi update hang with MCP extensions](https://github.com/earendil-works/pi/issues/5687)**
   *8 comments*
   Package subcommands finish output but never exit when an installed extension runs a long-lived MCP server. `handlePackageCommand` loads extensions, but their child processes aren't cleaned up.

4. **[#5816 – `search` tool systematically fails](https://github.com/earendil-works/pi/issues/5816)**
   *7 comments*
   Core regression on v0.79.4. The agent tries to use the `search` tool for codebase navigation but consistently gets `Tool search not found`.

5. **[#5571 – `pi -p` hangs with non-TTY stdin](https://github.com/earendil-works/pi/issues/5571)**
   *7 comments*
   A scripting/CI blocker. `pi -p "..."` hangs indefinitely when the resolved provider has no credentials instead of failing fast.

6. **[#5790 – httpProxy in settings.json](https://github.com/earendil-works/pi/issues/5790)**
   *7 comments*
   Request to allow fixed HTTP proxy configuration in `settings.json` so `EnvHttpProxyAgent` can route without environment variables.

7. **[#5700 – Multiple live agent sessions with TUI switching](https://github.com/earendil-works/pi/issues/5700)**
   *5 comments*
   Highly requested power feature. `switchSession` currently tears down the live session. Users want background agents they can switch between in the TUI.

8. **[#5778 – Agent-core hangs on unresponsive streams](https://github.com/earendil-works/pi/issues/5778)**
   *5 comments*
   Documents a critical flaw in the agent loop: `for await (...) {}` wedges if the LLM stream drops silently or a tool `execute()` fails to resolve.

9. **[#5670 – Tab completion grabs first item](https://github.com/earendil-works/pi/issues/5670)**
   *5 comments*
   Editor friction: typing to narrow a completion menu then pressing Tab applies the first item instead of keeping the menu open.

10. **[#5763 – Providers swallow HTTP error bodies](https://github.com/earendil-works/pi/issues/5763)**
    *4 comments*
    Behind a proxy/gateway, non-standard error responses return unreadable `UnknownError` or `403 status code (no body)` because providers drop the payload.

---

## 4. Key PR Progress

1. **[#5807 – Provider-scoped environment overrides](https://github.com/earendil-works/pi/pull/5807) (Merged)**
   Auth credentials in `auth.json` can now carry an `env` object for provider-specific configuration—account IDs, gateway IDs, and custom headers—without shell-level env vars.

2. **[#5820 – Preserve raw HTTP error bodies](https://github.com/earendil-works/pi/pull/5820) (Merged, fixes #5763)**
   A shared error-formatting helper that surfaces HTTP status and raw bodies from proxy/gateway non-2xx responses. Ends the guessing game around cloud gateway errors.

3. **[#5809 – Duration and time-to-first-token metrics](https://github.com/earendil-works/pi/pull/5809) (Merged)**
   Adds `durationMs` and `timeToFirstTokenMs` to the `Usage` interface and exposes tokens/second in the TUI footer.

4. **[#5812 – Protect pipe chars inside markdown tables](https://github.com/earendil-works/pi/pull/5812) (Merged)**
   Fixes a rendering bug where inline code containing `|` inside table cells broke column alignment and truncated content.

5. **[#5803 – Reject malformed OpenAI tool calls](https://github.com/earendil-works/pi/pull/5803) (Merged)**
   Prevents streamed tool calls missing `id` or `function.name` from being persisted into session history and corrupting future turns.

6. **[#5801 – Nixify pi](https://github.com/earendil-works/pi/pull/5801) (Merged)**
   Adds a Nix flake for building and running Pi (`nix build`, `nix run`), expanding the packaging matrix.

7. **[#5789 – Restore cursorUp line-start behavior](https://github.com/earendil-works/pi/pull/5789) (Merged)**
   Fixes a TUI regression where pressing Up on an input's first line immediately entered history mode instead of jumping to the line start.

8. **[#5798 – Vercel AI Gateway attribution headers](https://github.com/earendil-works/pi/pull/5798) (Merged)**
   Adds `http-referer` and `x-title` headers for identification in Vercel AI Gateway-managed deployments.

9. **[#5796 – Bump TS target to ES2024](https://github.com/earendil-works/pi/pull/5796) (Open)**
   Modernizes the TypeScript lib target and replaces hand-rolled Promise resolvers with native `Promise.withResolvers()`.

---

## 5. Feature Request Trends

- **Multi-agent orchestration** – The community strongly wants Pi to function as an agent platform, supporting concurrent background sessions managed through the TUI ([#5700](https://github.com/earendil-works/pi/issues/5700)) and RPC commands for session inspection ([#5810](https://github.com/earendil-works/pi/issues/5810)).
- **Flexible provider configuration** – Users consistently ask to decouple provider setup from shell environments: richer `auth.json` schemas ([#5728](https://github.com/earendil-works/pi/issues/5728)), in-app proxy settings ([#5790](https://github.com/earendil-works/pi/issues/5790)), and better gateway error surfacing ([#5763](https://github.com/earendil-works/pi/issues/5763)).
- **Broader model compatibility** – Active work to add ZhipuAI ([#2345](https://github.com/earendil-works/pi/issues/2345)), fix Moonshot/Kimi schema validation ([#5822](https://github.com/earendil-works/pi/issues/5822)), and support Anthropic OAuth subscriptions ([#5821](https://github.com/earendil-works/pi/issues/5821)).
- **Performance telemetry** – The newly merged timing metrics ([#5809](https://github.com/earendil-works/pi/pull/5809)) signal growing demand for latency and throughput observability in agent responses.

---

## 6. Developer Pain Points

- **Streaming and agent-loop fragility** – This is the dominant pain point. Stalled streams ([#4945](https://github.com/earendil-works/pi/issues/4945)), silent hangs in non-TTY mode ([#5571](https://github.com/earendil-works/pi/issues/5571)), indefinite agent loop wedges ([#5778](https://github.com/earendil-works/pi/issues/5778)), and MCP lifecycle blocking ([#5687](https://github.com/earendil-works/pi/issues/5687)) dominate the support queue.
- **Provider API incompatibilities** – A steady stream of issues around model-specific quirks: DeepSeek V4 thinking/tool replay conflicts ([#5811](https://github.com/earendil-works/pi/issues/5811), [#5818](https://github.com/earendil-works/pi/issues/5818)), Moonshot schema rejections ([#5822](https://github.com/earendil-works/pi/issues/5822)), and OpenAI responses streaming drops ([#5819](https://github.com/earendil-works/pi/issues/5819)).
- **TUI quality-of-life regressions** – Scroll-jacking during streaming ([#5825](https://github.com/earendil-works/pi/issues/5825), [#5576](https://github.com/earendil-works/pi/issues/5576)), confusing tab completion behavior ([#5670](https://github.com/earendil-works/pi/issues/5670)), and terminal-specific input bugs (Kitty double keys [#5407](https://github.com/earendil-works/pi/issues/5407), Warp URL rendering [#5783](https://github.com/earendil-works/pi/issues/5783)).
- **Invisible errors** – Providers silently dropping error bodies ([#5763](https://github.com/earendil-works/pi/issues/5763)) makes debugging gateway and proxy configurations nearly impossible—partially addressed by today's merge in [#5820](https://github.com/earendil-works/pi/pull/5820).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest · 2026-06-17

## Today's Highlights
The community is grappling with **stability and infrastructure challenges** this week. Multiple release workflow failures (v0.18.1-preview.1, nightly builds) coupled with a critical CI gap—integration tests don't run on PRs—are causing silent regressions and blocking releases. On a positive front, major technical work is landing for **background automation** (self-paced `/loop`), a new **vision bridge** for text-only models, and ecosystem expansion via a community-built **QQ Bot channel adapter**. The proposed **OAuth free tier reduction** remains a highly polarizing topic with 136 comments.

---

## Releases
No new releases published in the last 24 hours. The team is actively investigating pipeline failures affecting the v0.18.1 train (see Hot Issues).

---

## Hot Issues (10 Notable Items)

1. **[Release Pipeline Collapse](https://github.com/QwenLM/qwen-code/issues/5222), [5221](https://github.com/QwenLM/qwen-code/issues/5215), [#5150](https://github.com/QwenLM/qwen-code/issues/5150)**
   > Three separate release attempts (v0.18.1, v0.18.1-preview.1, nightly) have failed in two days. This is the team's highest-urgency operational issue and directly surfaces the broader CI testing deficit.

2. **[Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)**
   > 136 comments — the week's most debated issue. Proposes reducing daily free quota from 1,000 to 100 requests and eventually shuttering the free OAuth entry point. Community reaction has been intense.

3. **[Trojan:JS False Positive in VSIX](https://github.com/QwenLM/qwen-code/issues/5055)**
   > *Priority P1, Security.* Windows Defender flags the official v0.18.0 VSIX as `Trojan:JS/ShaiWorm.DBA!MTB`. Significant trust impact on the Windows developer contingent; needs urgent triage and code-signing investigation.

4. **[CI Integration Tests Don't Run on PRs](https://github.com/QwenLM/qwen-code/issues/5219)**
   > Root cause of many regressions. E2E tests only execute in the nightly Release pipeline, so breaking PRs merge green and remain undetected until release time. A fix is in flight via PR #5211.

5. **[OOM After /quit with Auto-Memory](https://github.com/QwenLM/qwen-code/issues/5147)**
   > Managed auto-memory triggers a V8 heap OOM on session quit with large text histories, despite prior fixes (#4644/#4717). Users see the /quit summary render before the crash, making the error particularly jarring.

6. **[ExitPlanMode Stuck for Hours](https://github.com/QwenLM/qwen-code/issues/5210)**
   > Users report the model (qwen3.7-max) gets trapped in ExitPlanMode for 7+ hours, unable to transition to YOLO mode. A recent behavioral regression that is blocking active users of the plan workflow.

7. **[Stale .qwen-session Blocks Worktree Cleanup](https://github.com/QwenLM/qwen-code/issues/5208)**
   > The `exit_worktree` tool erroneously refuses to clean up worktrees created by previous sessions. Forces manual git worktree management and breaks session lifecycle hygiene.

8. **[Auto-Update Fails on Older glibc (CentOS 7)](https://github.com/QwenLM/qwen-code/issues/5206)**
   > Auto-update silently migrates npm-installed binaries to the standalone installer, which bundles Node 22 requiring `glibc >= 2.28`. Breaks updates on CentOS 7 and other enterprise Linux hosts.

9. **[Discontinued OAuth Model in /model Selector](https://github.com/QwenLM/qwen-code/issues/5160)**
   > The `/model` CLI command still shows the discontinued `[qwen-oauth] coder-model` as the first selectable entry even when OAuth isn't configured. Confusing UX, especially given the free tier uncertainty.

10. **[Demand for Porting Dynamic Workflows](https://github.com/QwenLM/qwen-code/issues/4721)**
    > Strong community push for feature parity with Claude Code 2.1.160's Dynamic Workflows / Ultracode. This dovetails with the ongoing `/loop` alignment work as a multi-agent execution tier complementary to `/swarm`.

---

## Key PR Progress (10 Important Contributions)

1. **[Run E2E Tests on Every PR](https://github.com/QwenLM/qwen-code/pull/5211) — *MERGED***
   > Directly fixes the CI gap (#5219). Adds `daemon_status` to the capabilities baseline and activates integration tests on pull requests. The single most impactful infrastructure improvement this week.

2. **[Encrypted-File Fallback for Extension Secrets](https://github.com/QwenLM/qwen-code/pull/5221) — *OPEN***
   > Implements `SecretStorage` via AES-256-GCM encrypted files when the OS keychain is unavailable. Critical for headless/container environments and credential portability.

3. **[Fix sudo npm install Auto-Update](https://github.com/QwenLM/qwen-code/pull/5207) — *CLOSED / MERGED***
   > Prevents forced migration from npm to the standalone installer when the global prefix requires sudo. Resolves the glibc dependency regression from #4629.

4. **[Vision Bridge for Text-Only Models](https://github.com/QwenLM/qwen-code/pull/5126) — *OPEN***
   > A substantial feature: when a text-only primary model receives an image, it delegates to a configured multimodal model for transcription. Disabled by default. Bridges the largest modality gap.

5. **[QQ Bot Channel Adapter](https://github.com/QwenLM/qwen-code/pull/5202) — *OPEN***
   > Community contribution adding `@qwen-code/channel-qqbot` with WebSocket Gateway, HELLO/HEARTBEAT/DISPATCH/RECONNECT support. Expands the China-side channel ecosystem.

6. **[Background Loop Wakeup Engine (Step 1)](https://github.com/QwenLM/qwen-code/pull/5182) & [Step 2: Wire /loop](https://github.com/QwenLM/qwen-code/pull/5197) — *OPEN***
   > The foundation of `/loop` alignment with Claude Code. A second-resolution session wakeup engine (`CronScheduler`) enabling self-paced background automation without fixed recurring schedules.

7. **[Remember Selected Model Provider](https://github.com/QwenLM/qwen-code/pull/5179) — *OPEN***
   > Fixes a silent UX bug where the model picker forgets your provider choice when multiple providers share a model ID. `baseUrl` is now persisted with the model selection.

8. **[Localize Remaining Hardcoded UI Strings](https://github.com/QwenLM/qwen-code/pull/5189) — *OPEN***
   > Community i18n PR routing close-button tooltips and other hardcoded English strings through the existing `useI18n` system. Adds English and Simplified Chinese entries.

9. **[Track Safe sed Edits in File History](https://github.com/QwenLM/qwen-code/pull/5141) — *OPEN***
   > Treats safe `sed -i` substitution commands as confirmed file edits instead of opaque shell executions. Adds diff preview, file history tracking, and preserves undo semantics.

10. **[Stop After Cancelled ask_user_question](https://github.com/QwenLM/qwen-code/pull/5218) — *OPEN***
    > Fixes ACP tool execution flow so cancelled user questions halt gracefully—including nested agent cases—instead of cascading into skipped follow-up tool errors.

---

## Feature Request Trends

- **Background Automation & Loop Alignment**: The dominant trend. Requests for Dynamic Workflows (#4721), the `/loop` alignment work package (#5124, #5156, #5184), and self-paced wakeup primitives show the community strongly wants "fire-and-forget" agent capabilities mirroring Claude Code.
- **Internationalization (i18n)**: Multiple PRs and issues (#5186, #5189, #5220) targeting hardcoded English strings in both the TUI and web-shell, signalling a growing non-English user base demanding full localization.
- **Security & Credential Infrastructure**: MCP credential scoping (#4615), encrypted secret storage (#5221), and keychain fallbacks are a recurring theme as the tool extends into enterprise and daemon-mode usage.
- **Ecosystem Channel Expansion**: The addition of a QQ Bot adapter (#5201/5202) alongside existing Telegram/WeChat/DingTalk/Feishu channels indicates active investment in developer touchpoint diversity.
- **Model Provider UX**: Issues around provider selection, OAuth model visibility, and vendor-locking perception (#5160, #5179) suggest users want a more model-agnostic, transparent provider selection experience.

---

## Developer Pain Points

- **CI/CD Instability & Regressions**: The #1 pain point. Repeated release pipeline failures (#5222, #5150) combined with the admission that integration tests never run on PRs (#5219) has severely damaged confidence in the release process and branch stability.
- **Platform Compatibility Friction**: Windows users face antivirus false positives (#5055), while Linux users on older distributions (CentOS 7) get locked out of auto-updates due to glibc bundling in the standalone installer (#5206).
- **Core Flow Blocking Bugs**: Session management bugs (OOM on `/quit`, stale worktree markers) and state machine issues (stuck in ExitPlanMode for hours, terminal corrupted by SGR mouse mode) are directly halting daily coding workflows.
- **Service & Policy Uncertainty**: The proposed OAuth free tier reduction from 1000→100 requests/day (#3203), combined with API connectivity failures on Qwen 3.6 (#3050), creates a sense of service fragility among free-tier and indie developers.
- **Testing Gaps Exposed**: The "merge green, fail at release" pattern reveals that the existing PR test suite is insufficient to catch behavioral regressions, especially in plan mode, session lifecycle, and auto-memory paths.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# CodeWhale Community Digest
**Date:** 2026-06-17  
**Project:** Hmbown/CodeWhale (formerly Hmbown/DeepSeek-TUI)

---

## Today's Highlights

The `deepseek-tui` project officially rebrands to **CodeWhale** with the v0.8.61 release, deprecating the legacy npm package. Beyond the rename, execution on the v0.9.0 roadmap is accelerating: a Phase 1 implementation of the "Workrooms" threaded-agent architecture ([#3277](https://github.com/Hmbown/CodeWhale/pull/3277)) has been submitted alongside continued work on the ambitious Hippocampal Memory v2 system ([#2933](https://github.com/Hmbown/CodeWhale/pull/2933)). Stability remains the community's loudest concern, with multiple open threads on the "Turn stalled" freeze error ([#2487](https://github.com/Hmbown/CodeWhale/issues/2487)).

---

## Releases

### v0.8.61
The project completes its official rebrand from `deepseek-tui` to **CodeWhale**. The canonical project, CLI command, npm package, and release assets now use the `codewhale` name. Users on legacy v0.8.x (`deepseek` / `deepseek-tui`) should follow the migration guide in `docs/REBRAND.md`. No other feature changes are packged with this release.

---

## Hot Issues

The following 10 issues represent the most significant active and recently resolved discussions in the community.

### 1. [#2487 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/2487) – Frequent "Turn stalled – no completion signal received" error in `yolo` mode
**Author:** yahayao | **14 comments**  
The most active thread this period. Operations in `yolo` mode freeze with a stall prompt; `continue` fails to recover the session. This is a recurring multi-version stability bug that directly impacts user trust.

### 2. [#3275 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3275) – Agent over-extends scope, enters self-questioning loop  
**Author:** yekern  
Users report that CodeWhale consistently deviates from user intent, proposing and executing work without confirmation. Tagged as a regression from [#3061](https://github.com/Hmbown/CodeWhale/issues/3061), this is a critical agent alignment concern.

### 3. [#3209 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3209) – EPIC: Chat-native workrooms for threaded, shareable agent work  
**Author:** Hmbown  
Flagship v0.9.0 feature proposal. Lays out a vision for moving beyond the terminal session to threads, channels, shareable links, and multi-model collaboration. Already has a Phase 1 PR open ([#3277](https://github.com/Hmbown/CodeWhale/pull/3277)).

### 4. [#2870 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/2870) – EPIC: Staged command-boundary refactor  
**Author:** aboimpinto  
Tracks the decomposition of a major architecture refactor into mergeable chunks for v0.9.0. Aims to land infrastructure without blocking the mainline with a monolithic proof branch.

### 5. [#2739 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/2739) – Task execution freezes and enters infinite wait  
**Author:** zoomtint  
Another freeze report (Chinese locale). The user notes this has persisted since v0.8.51 and that the 300-second subprocess cancellation timeout has not resolved the root cause.

### 6. [#3264 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3264) – Feature request: Restrict skill scanning to `~/.codewhale/skills/` only  
**Author:** Yunqing2022  
Requests a scoped configuration option to limit skill autodiscovery, preventing unwanted directory traversal or performance overhead.

### 7. [#3238 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3238) – Fails to install on Ubuntu 22.04 LTS due to glibc mismatch  
**Author:** thahmidul-islam-nafi  
`npm install -g codewhale` fails on an older but widely used LTS release. Highlights ongoing Linux distribution friction. The musl static build PR ([#3274](https://github.com/Hmbown/CodeWhale/pull/3274)) is a direct response.

### 8. [#3240 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3240) – Legacy `~/.deepseek` config directory still created on Windows  
**Author:** Final527  
Despite the rebrand, CodeWhale still initializes the old `.deepseek` directory in addition to the new `.codewhale` directory. Users want a clean break.

### 9. [#3273 [OPEN]](https://github.com/Hmbown/CodeWhale/issues/3273) – `js_execution` tool does not honor proxy config on Windows  
**Author:** lordwedggie  
The shell tools work through a VPN/proxy, but the built-in JavaScript execution tool times out. A significant blocker for corporate or enterprise Windows environments.

### 10. [#3265 [CLOSED]](https://github.com/Hmbown/CodeWhale/issues/3265) – Moonshot/Kimi API rejects requests due to missing `parameters.type: "object"`  
**Author:** jghwwnq  
Every request to the Moonshot provider failed with HTTP 400 because the tool definitions omitted the required `type: "object"` field. Demonstrates the ongoing challenge of maintaining strict spec compliance across diverse API providers.

---

## Key PR Progress

### 1. [#3277 [OPEN]](https://github.com/Hmbown/CodeWhale/pull/3277) – Workrooms Phase 1
**Author:** idling11  
Foundation layer for v0.9.0 Workrooms: RFC, data model, API endpoints, and CLI integration for durable, threaded agent conversations. This is a major structural addition to the project.

### 2. [#3274 [OPEN]](https://github.com/Hmbown/CodeWhale/pull/3274) – Static Linux x64 musl builds
**Author:** wavezhang  
Switches GitHub Actions release builds to `x86_64-unknown-linux-musl` for glibc-independent static binaries. Companion to the CNB pipeline change in [#2903](https://github.com/Hmbown/CodeWhale/pull/2903). Directly addresses the Ubuntu 22.04 install failures.

### 3. [#3270 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/3270) – Document Linux build-time deps for `cargo install`
**Author:** zlh124  
Adds `libdbus-1-dev` and `pkg-config` to the install guide. A small but critical fix that removes friction for developers building from source on Ubuntu 24.04.

### 4. [#3269 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/3269) – Expose slash commands as hotbar actions
**Author:** reidliu41  
Allows binding slash commands (`/mode`, `/task`, `/rename`) to hotbar slots. Ergonomics improvement for power users who want keyboard-driven workflows.

### 5. [#3267 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/3267) – Keep oversized pastes inline with truncation and auto-expand
**Author:** idling11  
Fixes a UX regression where pasting large text silently replaced the composer content with a file mention. Now preserves the full editability of pasted content.

### 6. [#3236 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/3236) – Add DeepInfra provider support
**Author:** nightt5879  
Comprehensive DeepInfra integration covering runtime, TUI, CLI, and TOML configuration wiring. Expands the provider ecosystem for users outside the standard OpenAI/Azure sphere.

### 7. [#3271 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/3271) – Add Ponytail personality to project instructions
**Author:** ousamabenyounes  
Documents the third-party Ponytail personality in the official project guides, contingent on upstream listing. Signals growing ecosystem maturity.

### 8. [#2933 [OPEN]](https://github.com/Hmbown/CodeWhale/pull/2933) – Hippocampal Memory v2
**Author:** cy2311  
Massive upgrade to the cross-session memory layer: namespaces, rollback, auto-inject, background daemon, and schema migration. Still open and awaiting comprehensive review. This is the highest-stakes architecture PR in flight.

### 9. [#2998 [CLOSED]](https://github.com/Hmbown/CodeWhale/pull/2998) – Bump Tailwind CSS from v3.4.19 to v4.3.1
**Author:** dependabot[bot]  
Dependency bump for the web marketing site. Keeping the stack on a modern major release.

### 10. [#3276 [OPEN]](https://github.com/Hmbown/CodeWhale/pull/3276) – Migrate `/web` marketing site from Tailwind v3 to v4
**Author:** Hmbown  
A proactive migration by the maintainer to close the gap created by Dependabot bumps, ensuring the web presence stays current with Tailwind v4 features.

---

## Feature Request Trends

*   **Multi-Agent Persistence (Workrooms):** The clearest signal for v0.9.0 is a move from ephemeral chat to persistent, threaded, shareable agent containers ([#3209](https://github.com/Hmbown/CodeWhale/issues/3209), [#2007](https://github.com/Hmbown/CodeWhale/issues/2007)).
*   **Long-Term Memory:** The Hippocampal v2 system ([#2933](https://github.com/Hmbown/CodeWhale/pull/2933)) reflects a strong user demand for agents that remember context across sessions without manual injection.
*   **Dynamic Model & Provider Metadata:** Users and maintainers alike want a hydrated model registry instead of scattered hardcoded lists ([#3071](https://github.com/Hmbown/CodeWhale/issues/3071), [#3072](https://github.com/Hmbown/CodeWhale/issues/3072), [#3073](https://github.com/Hmbown/CodeWhale/issues/3073)).
*   **Clarifying Questions:** There is a growing expectation for agents to explicitly ask users questions ([#3102](https://github.com/Hmbown/CodeWhale/issues/3102)) rather than silently making incorrect assumptions during execution.
*   **Configurable Security Scope:** Users want finer-grained control over skill discovery ([#3264](https://github.com/Hmbown/CodeWhale/issues/3264)) and network proxy behavior ([#3273](https://github.com/Hmbown/CodeWhale/issues/3273)).

---

## Developer Pain Points

*   **Turn Stalls and Hard Freezes:** The persistent "Turn stalled" error ([#2487](https://github.com/Hmbown/CodeWhale/issues/2487)) and indefinite execution hangs ([#2739](https://github.com/Hmbown/CodeWhale/issues/2739)) are the most frequently reported stability issues, damaging confidence in long-running autonomous workflows.
*   **Linux Installation Friction:** Users on Ubuntu (22.04 and 24.04) face significant friction, from glibc version mismatches ([#3238](https://github.com/Hmbown/CodeWhale/issues/3238)) to missing system build dependencies ([#3270](https://github.com/Hmbown/CodeWhale/pull/3270)). The move to musl static builds is a positive but still-in-progress response.
*   **Rebranding Cleanup:** The incomplete transition from `deepseek` to `codewhale` has left orphaned config directories ([#3240](https://github.com/Hmbown/CodeWhale/issues/3240)), causing confusion and breaking automated setups.
*   **TUI Input Regressions:** Recent hotbar changes have introduced regressions in basic text input, such as digit keys being intercepted ([#3243](https://github.com/Hmbown/CodeWhale/issues/3243)) and large pastes being hidden behind file references ([#3263](https://github.com/Hmbown/CodeWhale/issues/3263)).
*   **Windows and Proxy Gaps:** Provider tools and execution engines that ignore system proxy settings ([#3273](https://github.com/Hmbown/CodeWhale/issues/3273)) remain a significant blocker for corporate and VPN-restricted developers, limiting the tool's enterprise adoption.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*