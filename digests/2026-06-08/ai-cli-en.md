# AI CLI Tools Community Digest 2026-06-08

> Generated: 2026-06-08 03:40 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-08

---

## 1. Ecosystem Overview

The AI CLI development ecosystem is simultaneously maturing and fracturing. A clear push for protocol standardization (MCP/ACP) and deeper agentic workflows is underway, but the user experience is dominated by billing friction, model regression, and state management failures—the gap between "capable agent" and "trustworthy tool" is the week's dominant theme. Communities are polarizing: high-iteration consumer tools face a trust deficit from opaque pricing and regressions, while enterprise-oriented tools build governance infrastructure that lags in raw agent intelligence. The "cost wall" has arrived, and tools that solve cache efficiency, compaction, and quota transparency will define the next wave of adoption.

---

## 2. Activity Comparison

| Tool | High-Heat Issues | Active PRs (24h) | Release Today | Ecosystem Signal |
|---|---|---|---|---|
| **Claude Code** | #16157 (Billing crisis, 691👍), #65697 (Linux client, 316👍) | ~0 (stalled) | None | Billing and regression fatigue eroding trust |
| **OpenAI Codex** | #26892 (gpt-5.5 404), #24050 (Windows sandbox, 12👍) | 10 | None | Infrastructure refactoring; UI/API catalog desync |
| **Gemini CLI** | #21409 (Agent hangs), #22323 (False success) | 10 | None | Systematic quality investment; agent trust deficit |
| **GitHub Copilot** | #333 (SSL inspection), #3216 (Infinite loop) | 1 (draft) | None | Enterprise networking blockers; stability crisis |
| **Kimi Code** | #2437 (Migration quality), #2438 (Agent unknown) | 1 | None | Post-fork identity crisis; community trust dropping |
| **OpenCode** | #2242 (Sandboxing, 51👍), #21470 (CPU-bound, 10👍) | 10 | None | Orchestration performance ceiling; security push |
| **Pi** | #5478 (CWD bridge), #5485 (Day hallucination) | 8 | None | Fastest iteration; strong extension/performance focus |
| **Qwen Code** | #4550 (LAN blocked), #4514 (Daemon gaps) | 10 | Nightly v0.17.1 | ACP protocol maturation; strategic system features |
| **DeepSeek TUI** | #1177 (Cache low), #743 (Token explosion) | 20 | None | Cost explosion crisis; massive defect cleanup |

---

## 3. Shared Feature Directions

**Requirements appearing across at least three tool communities:**

| Need | Affected Tools | Core Community Pain |
|---|---|---|
| **Native Linux Desktop Client** | Claude Code (#65697, 316👍), OpenAI Codex (#11023, 510👍), GitHub Copilot (#2294) | Non-negotiable for server-side/enterprise developers. Mac-first window is closing. |
| **Billing Transparency & Fairness** | Claude Code (#16157), OpenAI Codex (#12299, #26512), OpenCode (#15585, #29182), DeepSeek TUI (#1177) | Users hit false limits, passive drain, opaque quotas. Trust in metering is broken. |
| **Session Reliability & State Management** | OpenAI Codex (#7808, context death), Pi (#5478, CWD leak), Gemini CLI (#25166, shell hang), DeepSeek TUI (#2739, freeze) | Losing hours of work. Hard context window death or subtle state corruption is fatal for long sessions. |
| **Plugin/MCP Ecosystem Stability** | Claude Code (Windows/Arch MCP), OpenAI Codex (#25809, plugin loss), Pi (#5487, tool conflict), OpenCode (#2242, sandbox) | Plugins are the future, but setup friction, state loss, and lack of isolation block adoption. |
| **Provider/Local Model Flexibility** | Kimi Code (#2439, Ollama fails), OpenCode (#20995, Gemma 4), Gemini CLI (#24246, 128-tool limit), Pi (#5456, role mismatch) | Users run heterogeneous backends. Bugs are specific and blocking, eroding the value of agnosticism. |
| **Agent Trust & Guardrails** | Gemini CLI (#22323, false success, #22672, destructive), GitHub Copilot (#3216, loop), Qwen Code (#4538, self-modification) | "Doesn't hang" and "doesn't destroy" are more valued than "smarter". |
| **Session Mobility / Renaming** | Kimi Code (#2269), OpenCode (#25848), DeepSeek TUI (#2492) | Sessions are valuable artifacts but cannot be labeled, searched, or moved between machines. |

---

## 4. Differentiation Analysis

**How each tool's strategic bets define its community pain and future trajectory:**

| Tool | Strategic Bet | Biggest Weakness This Week |
|---|---|---|
| **Claude Code** | Deep agentic workflows with fine-grained hooks | Opus 4.8 regression (#63604, #64991) and Max billing crisis (#16157) |
| **OpenAI Codex** | Plugin infrastructure, global instructions API, stable SDK primitives | gpt-5.5 UI/API mismatch (#26892), Windows sandbox fragility (#24050) |
| **Gemini CLI** | Systematic quality (Robust Evals #24353), AST-aware code intelligence (#22745) | Generalist agent hangs (#21409), sub-agent false success (#22323) |
| **GitHub Copilot** | Enterprise compliance, GitHub-native CI/CD integration | SSL inspection (#333), infinite budget loops (#3216), licensing ambiguity (#2294) |
| **Kimi Code** | *Undefined post-fork.* Transitioning from `kimi-cli` to `kimi-code` without clear differentiation. | Migration breakdown (#2437), agent unknown status (#2438), closed community debate (#2381) |
| **OpenCode** | Maximum customizability via orchestration logic | CPU-bound internal loop (#21470), provider fragility across every release |
| **Pi** | Clean MCP/extensions API, performance-first design, fast bug turnaround | Provider transport timeouts (#5427), local model latency (#5464), cold start (#5402) |
| **Qwen Code** | ACP protocol dominance, daemon-as-server model, system-level features (sleep inhibit, reaper, OOM) | Enterprise air-gap block (#4550), submodule completions (#4568) |
| **DeepSeek TUI** | Low-cost fast inference model access | Token cost is destroying the value prop (#743, #1177); mode inconsistency (#2328, #2346) |

---

## 5. Community Momentum & Maturity

**Engineering Velocity (PRs 24h):**
- **Hyperactive:** DeepSeek TUI (20 PRs, massive bug-fix sprint)
- **Very Active:** OpenAI Codex, Gemini CLI, OpenCode, Pi, Qwen Code (8–10 PRs each)
- **Stalled:** Claude Code, GitHub Copilot, Kimi Code (0–1 PRs each)

**Community Heat vs. Health:**
- **Claude Code** and **OpenAI Codex** have the highest raw engagement but negative sentiment (billing crises, regressions). High risk of user flight.
- **Pi** has the best ratio of constructive feedback to rapid resolution. Most mature extension API iteration.
- **Gemini CLI** and **OpenCode** show high-signal, constructive bug reporting from sophisticated user bases. Good community health despite serious bugs.
- **Kimi Code** and **DeepSeek TUI** are in negative sentiment territory: strategic confusion and cost crises, respectively.

**Maturity Assessment:**
- **Systematic / Stabilizing:** Gemini CLI (robust eval framework), OpenAI Codex (plugin architecture refactor)
- **Fast-Growth / Unstable:** Pi, OpenCode, Qwen Code, DeepSeek TUI (high velocity, but sharp edges)
- **Trust Vulnerable:** Claude Code (billing), Kimi Code (identity), DeepSeek TUI (cost)
- **Niche / Quiet:** GitHub Copilot (enterprise barriers limiting growth)

---

## 6. Trend Signals

**Key takeaways for technical decision-makers:**

1. **Cost Transparency is the #1 Competitive Moat.** Token burn, false rate limits, and passive quota drain dominate the most upvoted threads. Tools that cannot instrument and display real-time cost per action will lose enterprise adoption. Caching strategy (DeepSeek #1177) is as important as model intelligence.

2. **"Trustworthy Agent" > "Smart Agent".** Hangs, false successes, and destructive operations are more damaging than a wrong answer. The winning tools will invest in guardrails, sandboxing, and deterministic state tracking (OpenCode #2242, Gemini #22323, GitHub Copilot #3216).

3. **Protocol Interoperability is the New Platform Battle.** MCP is table stakes. ACP (Qwen Code #4514, #4782) is the emerging differentiator. The CLI tool that becomes the best *orchestrator of services*—rather than the best monolith—wins the platform war.

4. **Linux Desktop is a Gap, Not a Niche.** 500+ 👍 for a Linux build on two separate tools (OpenAI Codex, Claude Code) signals that the professional server-side developer is neglected. Tools without a Linux GUI are actively capping their TAM.

5. **Internal Tool Performance Matters.** OpenCode's CPU-bound orchestration loop (#21470) and Pi's cold start (#5402) reveal that users are sensitive to *tool overhead*, not just model latency. Developers are profiling the tool.

6. **Session State is a First-Class Asset.** The lack of session naming, cross-machine portability, and crash recovery are universal pain points. The tool that makes sessions persistent, searchable, and restorable will capture the "deep work" use case.

7. **Debugging the Agent is the New UX Frontier.** Communities are asking for transparent mode switching (DeepSeek #2346), filtered transcripts (OpenCode #31294), and exportable traces. The tool that makes agent decisioning inspectable will build the most trust.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Claude Code Skills Ecosystem: Community Highlights Report**  
*Data as of 2026-06-08 | Source: github.com/anthropics/skills*

---

### 1. Top Skills Ranking

**Most Attention via Pull Requests** (function, discussion highlights, status)

- **Document Typography ([#514](https://github.com/anthropics/skills/pull/514))**  
  *Function:* Auto-corrects orphans, widows, and numbering misalignment in AI-generated documents.  
  *Discussion:* Addresses a universal output-quality pain point; highly practical for anyone publishing Claude-generated content.  
  *Status:* Open

- **Frontend-Design Clarity ([#210](https://github.com/anthropics/skills/pull/210))**  
  *Function:* Revises the existing `frontend-design` skill so every instruction is directly actionable by Claude within a single conversation.  
  *Discussion:* Signals the community’s growing emphasis on *skill quality over quantity* and specific, behavior-shaping guidance.  
  *Status:* Open

- **Meta Skills: Quality & Security Analyzers ([#83](https://github.com/anthropics/skills/pull/83))**  
  *Function:* Two meta-skills that evaluate other skills across structure, documentation, and security dimensions.  
  *Discussion:* Seen as foundational for ecosystem trust and quality control; sparked debate on self-assessment tooling.  
  *Status:* Open

- **Infrastructure Fixes (Lubrsy706 series: [#538](https://github.com/anthropics/skills/pull/538), [#539](https://github.com/anthropics/skills/pull/539), [#541](https://github.com/anthropics/skills/pull/541))**  
  *Function:* Fixes case-sensitive file references, YAML frontmatter parsing, and DOCX tracked-change ID collisions.  
  *Discussion:* Reflects ecosystem maturation; community contributors are actively hardening the repo’s core infrastructure.  
  *Status:* Open

- **ServiceNow Platform Skill ([#568](https://github.com/anthropics/skills/pull/568))**  
  *Function:* Broad coverage of ITSM, ITOM, SecOps, ITAM, FSM, SPM, CSDM, and IntegrationHub.  
  *Discussion:* The largest enterprise-platform skill submission to date; ambitious scope has attracted sustained commentary.  
  *Status:* Open

- **Windows Subprocess & Encoding Fixes ([#1050](https://github.com/anthropics/skills/pull/1050), [#1099](https://github.com/anthropics/skills/pull/1099))**  
  *Function:* Resolves `run_eval.py` and `run_loop.py` crashes on Windows due to `PATHEXT` handling and pipe encoding.  
  *Discussion:* Massive blocker for non-macOS users; repeated community engagement underscores cross-platform demand.  
  *Status:* Open

- **Agent Creator Meta-Skill ([#1140](https://github.com/anthropics/skills/pull/1140))**  
  *Function:* Creates task-specific agent sets; fixes parallel multi-tool evaluation and adds Windows `recalc.py` support.  
  *Discussion:* Directly addresses the need for dynamic agent composition and reliable tool orchestration.  
  *Status:* Open (Fixes #1120)

- **n8n Builder & Debugger ([#190](https://github.com/anthropics/skills/pull/190))**  
  *Function:* Guides Claude through building and debugging n8n automation workflows from scratch.  
  *Discussion:* High engagement from the automation community; workflow integration is a clear priority area.  
  *Status:* Open

---

### 2. Community Demand Trends

**Most-Anticipated Skill Directions (from Issues)**

- **Enterprise Governance & Sharing**  
  [Issue #228](https://github.com/anthropics/skills/issues/228) (13 comments, 7 👍) calls for org-wide skill sharing without manual file transfers.  
  [Issue #492](https://github.com/anthropics/skills/issues/492) (7 comments, 2 👍) raises trust-boundary and namespace impersonation risks.

- **Reliable Evaluation & Optimization Tooling**  
  [Issue #556](https://github.com/anthropics/skills/issues/556) (11 comments, 7 👍) and [Issue #1169](https://github.com/anthropics/skills/issues/1169) document that `run_eval.py` and `run_loop.py` yield 0% recall across all queries, blocking skill iteration.

- **Platform Stability & Architecture**  
  [Issue #62](https://github.com/anthropics/skills/issues/62) and [#61](https://github.com/anthropics/skills/issues/61) report disappearing skills and 404 errors.  
  [Issue #1220](https://github.com/anthropics/skills/issues/1220) requests multi-file reference bundling.  
  [Issue #16](https://github.com/anthropics/skills/issues/16) advocates exposing Skills as MCP tools for protocol-native consumption.

---

### 3. High-Potential Pending Skills

**Active PRs likely to merge soon, based on community momentum:**

| PR | Skill | Why It’s Watchlisted |
|---|---|---|
| [#1140](https://github.com/anthropics/skills/pull/1140) | Agent Creator Meta-Skill | Unlocks dynamic agent composition; directly fixes multi-tool eval |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing Patterns Skill | Covers testing trophy, React, integration, E2E; high developer demand |
| [#444](https://github.com/anthropics/skills/pull/444) | AURELION Suite (4 skills) | Structured cognitive + memory framework for professional KM |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow Platform Skill | Most comprehensive enterprise platform skill submitted to date |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP Predictive Analytics Skill | Direct enterprise analytics use case using SAP-RPT-1-OSS |
| [#514](https://github.com/anthropics/skills/pull/514) | Document Typography Skill | Universal document quality fix; low friction to merge |

---

### 4. Skills Ecosystem Insight

*The community’s most concentrated demand has shifted away from narrow functional skills toward the **reliability, governance, and platform infrastructure**—evaluation tooling, cross-platform parity, enterprise distribution, and security—required to make the Skills ecosystem trustworthy and scalable.*

---

# Claude Code Community Digest — 2026-06-08

## 1. Today's Highlights
The community remains focused on a critical usage-limit crisis affecting Max subscribers (Issue #16157), while the call for a native Linux Desktop build continues to gain momentum with 316 👍 (Issue #65697). Recent regressions in the TUI scroll behavior (v2.1.150) and malformed tool calls from Opus 4.8 are eroding confidence in release stability. The pull request queue is inactive, suggesting engineering bandwidth is concentrated on internal stabilization work.

## 2. Releases
No new releases were tagged in the last 24 hours.

## 3. Hot Issues

**[#16157 – Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/issues/16157)**
*Comments: 1476 | 👍: 691*
The highest-engagement issue on the board by a wide margin. Max-plan subscribers report burning through their usage budget within minutes of starting a session. The sheer volume of comments (1476) suggests an ongoing billing/capacity crisis that is severely impacting developer trust in paid tiers.

**[#65697 – Official Claude Desktop build for Linux](https://github.com/anthropics/claude-code/issues/65697)**
*Comments: 24 | 👍: 316*
The demand for a native Linux Desktop build (Ubuntu LTS / Debian) is the strongest single feature signal this week. While `claude code` works as a CLI on Linux, the community is explicitly asking for desktop-quality GUI integration.

**[#45937 – Dispatch main conversation permanently offline despite working Cowork tasks](https://github.com/anthropics/claude-code/issues/45937)**
*Comments: 33 | 👍: 12*
A confusing state bug where Cowork task execution succeeds but the main Dispatch thread never appears online in mobile clients. Points to a potential session routing or sync issue in the Cowork architecture.

**[#25128 – Drag and drop not working in VS Code extension chat panel](https://github.com/anthropics/claude-code/issues/25128)**
*Comments: 19 | 👍: 39*
An orphaned regression dating back to v2.1.6 (still broken as of v2.1.39). A basic IDE interaction that works in the terminal CLI but fails in the VS Code panel. Long resolution time is generating frustration.

**[#62466 – Repeated "Image couldn't be processed" API errors consuming usage limit](https://github.com/anthropics/claude-code/issues/62466)**
*Comments: 18 | 👍: 16*
Failed image processing calls are still counting against API usage, causing unexpected cost spikes for developers working with visual inputs. This is both a reliability and a billing fairness issue.

**[#63604 – Opus 4.8 repeatedly emits malformed tool_use blocks](https://github.com/anthropics/claude-code/issues/63604)**
*Comments: 4 | 👍: 8*
Raw `<invoke>` XML leaking into terminal output, forcing session hangs until the user sends a manual message. This is a clear regression from Opus 4.7 and is blocking teams who rely on accurate function calling.

**[#65833 – v2.1.150: scroll wheel no longer scrolls conversation (sends arrow keys instead)](https://github.com/anthropics/claude-code/issues/65833)**
*Comments: 3 | 👍: 1*
A TUI regression where the mouse scroll wheel now cycles input history instead of panning the conversation view. A frustrating UX regression for terminal-heavy users.

**[#16001 – Allow for updated input in PermissionRequest:ExitPlanTool:Approve hook](https://github.com/anthropics/claude-code/issues/16001)**
*Comments: 13 | 👍: 26*
High-value workflow feature. Developers want to validate and modify tool exit plans directly within the approval hook, rather than going through the full async feedback cycle.

**[#65863 – Agent() spawn fails with "thinking options type cannot be disabled" on DeepSeek endpoint](https://github.com/anthropics/claude-code/issues/65863)**
*Comments: 3 | 👍: 0*
Conflicting parameter handling between `thinking` and `reasoning_effort` breaks Agent mode when using third-party Anthropic-compatible providers. Signals that provider abstraction layer needs better parameter normalization.

**[#64991 – Opus 4.8: forced balance-slot criticism, critique-for-its-own-sake, and attention-driven context collapse](https://github.com/anthropics/claude-code/issues/64991)**
*Comments: 1 | 👍: 1*
A thorough behavioral pathology report on Opus 4.8, cataloging 71 sub-issues. The author identifies a tendency for forced "balance-slot" criticism baked into the model's chain-of-thought. Validates subtle quality complaints heard elsewhere in the community.

## 4. Key PR Progress
The pull request queue is effectively inactive. The only updated PR, [#58673](https://github.com/anthropics/claude-code/pull/58673), is a trivial placeholder ("s") and does not represent meaningful code motion. With no merges to `main` in the last 24 hours, the community is awaiting hotfix releases for the v2.1.168 regressions.

## 5. Feature Request Trends
- **Linux Desktop Client:** A native GUI build for Debian/Ubuntu (Issue #65697) is the #1 platform request, accumulating 316 👍 in just three days.
- **Workflow Hooks & Customization:** Developers are pushing for programmable permission hooks (Issue #16001), settings to disable automatic file attachment in VS Code (Issue #66162), and global session history across projects (Issue #49095).
- **Accessibility:** Text-to-speech readback and voice mode for Remote Control sessions (Issue #42700) is gaining support, indicating expanding use cases beyond the traditional developer terminal.
- **Third-Party Provider Parity:** Requests for better context window detection for non-Anthropic APIs (Issue #46416) and general provider compatibility fixes remain a steady background signal.

## 6. Developer Pain Points
- **Billing & Quota Reliability:** The Max subscription usage-limit bug (#16157) is the most active thread on the board. Trust in the billing model is suffering when paying users cannot maintain a productive session.
- **Opus 4.8 Regressions:** The latest model is introducing tool-call corruption (#63604) and unwanted behavioral patterns (#64991), forcing teams to pin older models or accept degraded output.
- **Image Handling Costs:** "Image couldn't be processed" errors still consume usage budgets (#62466) and poison future image interactions in the same session (#66141). This creates a direct cost penalty for developers using multimodal features.
- **Regression Stability:** Frequent regressions in basic features (TUI scrolling #65833, VSCode DnD #25128) indicate testing gaps. The community is sensitive to losing established functionality in patches.
- **MCP & Plugin Setup Friction:** MCP servers fail silently on Windows (`spawn ENOENT` #58510), Arch Linux sandboxes are broken (#64799), and the `/doctor` diagnostic command fails to detect configuration errors (#64768). This makes plugin adoption a trial-and-error process.
- **Cross-Platform Gaps:** Windows and Linux users experience a regular stream of OS-specific auth (#65725), shell-detection (#62113), and sandbox issues, reinforcing a perception of macOS as a first-class platform.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-08

## Today's Highlights
The rollout of **`gpt-5.5`** has hit a wall: users report the model is selectable in both the Desktop app and CLI but returns a 404 on execution (#26892, #26910). **Windows sandbox stability** remains the most disruptive broad issue, with multiple distinct workflows (WSL, Computer Use, `node_repl`) all failing with `os error 740` (#24050, #25362, #25419). On the engineering side, OpenAI is investing heavily in **plugin infrastructure and global instructions** (#26831, #26934) to lock down the architecture ahead of the next stable release.

## Releases
*No new versions in the last 24 hours.*

## Hot Issues

1. **[#11023 — Codex Desktop App for Linux](https://github.com/openai/codex/issues/11023)** *(Enhancement, 100 comments, 510 👍)*  
   The most‑voted open issue by a wide margin. Linux developers cite unmanageable power consumption on macOS and the inability to run the app on their primary development machines. Community reaction is overwhelmingly positive but clearly growing impatient for a roadmap commitment.

2. **[#26892 — gpt-5.5 Is Listed but Requests Fail with 404](https://github.com/openai/codex/issues/26892)** *(Bug, 21 comments)*  
   A critical regression. Local model metadata advertises `gpt-5.5` as available, but every request to the responses endpoint returns `"Model not found"`. Users are forced to downgrade to `gpt-5.4`. A companion closed issue (#26910) flagged the same problem across the Mac app and CLI.

3. **[#24050 — Windows Sandbox Setup Triggers OS Error 740](https://github.com/openai/codex/issues/24050)** *(Bug, 7 comments, 12 👍)*  
   The root cause of a cascading set of Windows failures. Non‑elevated sandboxed tool execution (even `rg --version`) is blocked by Windows UAC/installer detection before the command runs. This single systemic issue is being echoed in #25362, #25419, and #26929.

4. **[#25715 — WSL2 Agent Environment Unusably Slow](https://github.com/openai/codex/issues/25715)** *(Bug, 36 comments)*  
   Routine “turns” are critically slow when the app targets a WSL2 Linux distro. The thread has become a gathering point for Windows developers who rely on native Linux tooling, strongly upvoting any proposed WSL‑specific optimizations.

5. **[#11881 — GitHub Action Auth Fails Despite Connected Account](https://github.com/openai/codex/issues/11881)** *(Bug, 16 comments, 28 👍)*  
   Invoking `@codex review` in a PR repeatedly asks users to connect GitHub even when the connector shows as active in the dashboard. CI/CD teams are blocked, creating high urgency for a fix.

6. **[#12299 — “You’ve Hit Your Usage Limit” Despite 90% Remaining](https://github.com/openai/codex/issues/12299)** *(Bug, 19 comments)*  
   Plus subscribers report a false rate‑limit hit early in the billing cycle. The heuristic behind usage accounting appears to have a race condition or stale cache, causing frustration and unnecessary throttling.

7. **[#25809 — Desktop Plugins Disappear After Restart](https://github.com/openai/codex/issues/25809)** *(Bug, 6 comments)*  
   The Chrome native messaging host and Computer‑Use MCP plugin repeatedly lose their connection after a restart. Re‑installing the bundled plugins temporarily fixes the state but the root cause (manifest creation/attachment) remains unresolved.

8. **[#26512 — Pro 5x Quota Dropped and Drains Passively](https://github.com/openai/codex/issues/26512)** *(Bug, 4 comments)*  
   High‑tier ($100/mo) subscribers report their weekly limits were silently reduced on June 1, and the quota continues to drain even when Codex is idle. Billing and telemetry transparency is a hot topic in the thread.

9. **[#23131 — TypeScript SDK JSONL Parser Breaks on Multiline MCP Results](https://github.com/openai/codex/issues/23131)** *(Bug, 11 comments)*  
   The SDK fails to parse tool results that contain multiline data, effectively breaking MCP tool‑calling workflows. A community patch is attached, signaling that the official SDK needs a stricter JSONL compliance pass.

10. **[#7808 — Context Window Exhaustion Is Immediately Fatal](https://github.com/openai/codex/issues/7808)** *(Bug, 9 comments, 8 👍)*  
    Running out of context window kills the entire conversation thread with no graceful compaction or summarization. Long‑session users consider this the single biggest QoL issue in the product today.

## Key PR Progress

1. **[#26937 — Test Windows Managed Deny‑Read Enforcement](https://github.com/openai/codex/pull/26937)** *(Open)*  
   Closes a security gap where a Python subprocess inside the Windows sandbox could bypass `permissions.filesystem.deny_read`. Adds integration coverage for enterprise compliance.

2. **[#26831/#26830 — Global Instructions Contributor API & Lifecycle Characterization](https://github.com/openai/codex/pull/26831)** *(Open)*  
   A substantial architectural refactor. Moves global instructions out of core `Config` into an explicit extension point, paired with exhaustive E2E tests covering forks, subagents, compaction, and resume to prevent data loss.

3. **[#26639 — Scope MCP Startup Status by Thread](https://github.com/openai/codex/pull/26639)** *(Closed)*  
   Fixes a UX pollution bug where MCP startup failures from spawned subagents were rendered in the parent thread transcript. Now scoped correctly to the originating child thread.

4. **[#26934 — Prune Stale Curated Plugin Caches](https://github.com/openai/codex/pull/26934)** *(Open)*  
   The first step in automated plugin lifecycle management. Cached plugins whose names no longer appear in the curated marketplace are pruned, preventing stale or dropped plugins from loading silently.

5. **[#26932 — Use Cached Remote Plugin Catalog for Plugin List](https://github.com/openai/codex/pull/26932)** *(Open)*  
   Loads the remote plugin marketplace catalog from the local disk cache when available, significantly speeding up `plugin/list` responses.

6. **[#26920 — Add Python SDK Goal Turns](https://github.com/openai/codex/pull/26920)** *(Open)*  
   Exposes persistent “goal” turns in both synchronous and asynchronous Python contexts. Goals are started atomically, assigned stable IDs, and support rollover‑aware control—a building block for persistent background agents.

7. **[#25976 — Use Stable Item IDs for Responses API Calls](https://github.com/openai/codex/pull/25976)** *(Open)*  
   Infrastructure change to pass stable client‑side item IDs when round‑tripping with the Responses API, enabling robust state tracking across remote compaction sessions.

8. **[#24982 — Honor Parent Approvals for Intercepted Execs](https://github.com/openai/codex/pull/24982)** *(Open)*  
   Fixes a major friction point in the unified‑exec path: approved sandbox overrides in a parent ZSH session no longer require re‑approval for forked child processes.

9. **[#26918 — Address Newly Reported Rust Advisories](https://github.com/openai/codex/pull/26918)** *(Open)*  
   Security maintenance bumping `rand` 0.8.5 → 0.8.6 (RUSTSEC-2026-0097) and flagging a transient `proc-macro-error2` advisory until upstream `i18n-embed-fl` updates.

10. **[#21612 — Bump Zip from 2.4.2 to 8.6.0](https://github.com/openai/codex/pull/21612)** *(Open)*  
    A massive version jump resolving multiple security advisories. The long‑running Dependabot PR is under review for API breakage across the `codex-rs` crate.

## Feature Request Trends

- **Native Linux Desktop App (#11023, 510 👍):** By far the single most requested addition. The macOS power consumption issue (#10432) is actively driving users to demand a Linux build.
- **General User Mode for Domain Experts (#26556):** A nascent but notable shift. Users want a simplified interface that hides diffs, logs, and implementation details, allowing non‑programmers to leverage Codex agents safely.
- **Client Version Rollback (#26914):** Trust in auto‑update is eroding. Paid subscribers want a way to pin or roll back the Desktop app version when a release breaks their workflow.
- **Plugin Ecosystem Stability:** Users consistently request that bundled plugins (Chrome, Computer‑Use) survive app restarts and that git‑sourced plugins support rich metadata before installation.

## Developer Pain Points

- **Windows Sandbox `os error 740`:** The single highest‑frequency distress signal. It blocks WSL, Computer Use, `node_repl`, and basic command execution. Despite multiple tickets, the sandbox initialization path on Windows remains fragile.
- **Model Backend/UI Desync:** `gpt-5.5` being listed but returning 404 exposes a dangerous disconnect between the client model catalog and the server. Developers lose trust when the UI says “available” but the API says “not found.”
- **Plugin State Loss:** Plugins that disappear after restart or fail to re‑establish native messaging hosts are a recurring theme. The extension system needs reliable lifecycle hooks and state persistence.
- **Rate Limit Opacity:** False‑positive limits (#12299) combined with passive quota drainage (#26512) create a perception of opaque billing. Users want per‑request telemetry and real‑time remaining quota dashboards.
- **Fatal Context Window Exhaustion (#7808):** The hard death of a thread upon hitting the context limit continues to be the top usability complaint for anyone running long‑lived agent sessions, with no compaction or summarization fallback in sight.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

## Gemini CLI Community Digest — 2026-06-08

While no new release landed in the last 24 hours, the repository saw intense activity around high-severity agent reliability issues and strategic quality investments. The community is feeling the friction of agent hangs and false-success states, while the maintainer team is pushing forward with MCP compliance fixes, memory system quality improvements, and the foundational work for AST-aware code understanding.

### Releases
**No new releases** in the last 24 hours. The latest update remains **v0.33.0**, which introduced the sub-agent feature that is generating significant discussion and several related bugs.

---

### Hot Issues

1. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist Agent Hangs [P1]**
   *8 upvotes.* The most upvoted issue this week. The CLI completely freezes when deferring to the generalist agent, even for trivial tasks like folder creation. Users report having to cancel after an hour. A notable community workaround is emerging: explicitly instructing the model not to use sub-agents.

2. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust Component Level Evaluations [P1]**
   A major P1 epic tracking the expansion of the behavioral eval framework (originally from #15300). With 76 behavioral tests already written across 6 Gemini models, this epic signals a major investment in systematic regression protection.

3. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent Reports "GOAL Success" After MAX_TURNS [P1]**
   A deeply deceptive bug where the `codebase_investigator` sub-agent reports `status: "success"` and `Termination Reason: "GOAL"` even though it hit its turn limit before doing any real analysis. This undermines trust in agent output.

4. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell Command Hangs Awaiting Input [P1]**
   *3 upvotes.* After executing simple shell commands, the CLI shows the command as "active" and "awaiting user input" even though the command finished. A core UX regression given the agent's heavy reliance on shell execution.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-Aware File Reads, Search, and Mapping [P2]**
   A strategic investigation epic into whether AST-aware tools can reduce token waste, eliminate misaligned reads, and improve navigation. Could be a major leap in agent precision and cost efficiency if successful.

6. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini Does Not Use Custom Skills and Sub-Agents [P2]**
   Despite having properly configured "gradle" and "git" skills with clear descriptions, the model rarely uses them autonomously. The model only defaults to custom agents when explicitly instructed, largely defeating the purpose of role-based customization.

7. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) / [#26516](https://github.com/google-gemini/gemini-cli/issues/26516) — Auto Memory Redaction & Quality [P2]**
   A cluster of memory-system bugs (see also #26522, #26523). Secrets are sent to model context before redaction, low-signal sessions are retried indefinitely, and invalid inbox patches are silently skipped. The security and reliability implications are driving a batch of focused fixes.

8. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 Error with >128 Tools [P2]**
   A practical scaling ceiling. When a project exceeds 128 tools, the API returns a hard 400 error. The community expects smarter tool scoping rather than a hard crash.

9. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent Destructive Behavior [P2]**
   *1 upvote.* The model occasionally resorts to `git reset` or `--force` flags when safer alternatives exist. Users want built-in guardrails to prevent destructive operations on repositories and databases.

10. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser Subagent Fails on Wayland [P1]**
    *1 upvote.* The `browser_agent` is completely non-functional on Wayland displays. A blocker for Linux desktop users running modern Fedora/Ubuntu.

---

### Key PR Progress

1. **[#27418](https://github.com/google-gemini/gemini-cli/pull/27418) — Respect `enableInteractiveShell: false` + Native Bridge Stability [CLOSED, P1]**
   Fixes shell execution service to properly respect the `enableInteractiveShell` flag and handles non-UTF-8 bytes in the string serialization layer. Critical for CI/CD and headless operation.

2. **[#27412](https://github.com/google-gemini/gemini-cli/pull/27412) — Prevent Model Fabrication on Binary Read [CLOSED, P2]**
   A major hallucination fix. When `read_file` processes a PDF (or other binary), the output was a bare descriptive string, causing the model to fabricate analysis. Now properly detects and signals binary content to avoid model confusion.

3. **[#27730](https://github.com/google-gemini/gemini-cli/pull/27730) — Keep Array Tool Results Out of `structuredContent` [OPEN, P1]**
   Fixes regression #27725 where JSON array payloads (e.g., from calendar tools) were incorrectly copied into `structuredContent`. Preserves text content for array tool results, improving MCP compliance.

4. **[#27733](https://github.com/google-gemini/gemini-cli/pull/27733) — Sniff MCP Image MIME Types [CLOSED]**
   Magic-byte detection for image payloads before sending MCP image/resource inline data to the model. Corrects misreported WebP/PNG/JPEG/GIF MIME types in the scheduler-facing `inlineData`.

5. **[#27729](https://github.com/google-gemini/gemini-cli/pull/27729) — Truncate Telemetry Attributes [OPEN, P2]**
   Fixes the terminal flood of Node.js stack traces during telemetry export by truncating metric attributes to 1024 characters, matching GCP Monitoring limits. High impact for enterprise users.

6. **[#27718](https://github.com/google-gemini/gemini-cli/pull/27718) — Keep `auto` Visible Without Preview Access [OPEN, P2]**
   Marks the top-level `auto` alias as non-preview so it remains visible in `/model` for dynamic model configuration, while keeping preview-only auto aliases filtered.

7. **[#27409](https://github.com/google-gemini/gemini-cli/pull/27409) — Fix Performance Test Timeout [CLOSED, P1]**
   Infrastructure fix to stabilize the performance test suite, which had been flaking under load. Maintains CI confidence.

8. **[#23647](https://github.com/google-gemini/gemini-cli/pull/23647) — Open Plugin Agent Support [CLOSED]**
   Implements automatic discovery, namespacing, and variable expansion for sub-agents defined in an Open Plugin's `agents/` directory. A key extensibility feature closing out.

9. **[#22586](https://github.com/google-gemini/gemini-cli/pull/22586) — Programmatic Extension Search [CLOSED]**
   Adds `/extensions search <query>` to both ACP and interactive UI. Preserves the visual gallery while enabling CLI-first discovery.

10. **[#22585](https://github.com/google-gemini/gemini-cli/pull/22585) — `/teleport` Command for Session Mobility [CLOSED]**
    Allows moving active AI engineering sessions between machines (e.g., local laptop to remote server). Unlike `/resume share`, this handles full session portability.

---

### Feature Request Trends

Three overlapping strategic directions are clear from recent requests:

- **Next-Level Code Intelligence:** The investigation into **AST-aware tools** (`#22745`, `#22746`, `#22747`) is the most impactful potential feature set in flight. The community wants the agent to operate on a syntactic level—precise method-bound reads, AST-grep for structural queries—rather than just text-based line numbers.

- **Proactive Safety & Governance:** Users are demanding that the agent recognize and avoid dangerous operations (`#22672`), actually use its configured skills without prompting (`#21968`), and understand its own mechanics to act as its own expert guide (`#21432`).

- **Memory & Privacy Maturation:** The Auto Memory system (`#26525`, `#26522`) is generating significant scrutiny. The requests for **deterministic redaction**, **session quality filtering**, and **patch validation** represent a maturation of the feature from a helpful "memory" layer into a system that must meet privacy and reliability bars.

---

### Developer Pain Points

1. **Reliability Friction is Dominating**
   The most acute frustration is agent reliability: the CLI hangs on generalist agent deferral (`#21409`), completed shell commands still show as "awaiting input" (`#25166`), and sub-agents report false "GOAL" successes after failing (`#22323`). These create a trust deficit that forces users to babysit interactions.

2. **Platform & Integration Gaps**
   Linux desktop users are blocked by **Wayland browser agent failures** (`#21983`). The inability to use **symlinks** for agent files (`#20079`) and **terminal corruption** after exiting external editors (`#24935`) are smaller but recurring friction points that fragment the experience across environments.

3. **Model Governance is Unpredictable**
   The P1 shell hang (`#25166`) apart, the top behavioral pain point is that the model refuses to use well-configured custom agents and skills without explicit instruction (`#21968`). Conversely, the model will generate messy temp scripts in random directories (`#23571`) and resort to destructive `git --force` operations (`#22672`), creating cleanup overhead and safety anxiety.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the **GitHub Copilot CLI Community Digest** for **2026-06-08**, based exclusively on repository activity from the last 24 hours.

---

### 1. Today’s Highlights
The past 24 hours produced no new release, but community attention is sharply focused on a critical session stability bug and persistent enterprise onboarding friction. A disturbing infinite-loop issue in long-running sessions has drawn financial loss concerns and a refund request from an affected user. Meanwhile, corporate users continue to hit hard walls with SSL inspection proxies and limited OTel authentication options, signaling that enterprise readiness remains the community’s top unmet need.

---

### 2. Releases
No new releases were published in the last 24 hours.

---

### 3. Hot Issues
All 10 recently active Issues are covered below.

**#333 – Enterprise SSL Inspection Failure** [OPEN, 4 👍]
- **Summary:** CLI fails with “fetch failed” behind MITM proxies even when corporate CAs are installed in the system keychain.
- **Why it matters:** This is a critical blocker for any corporate deployment using SSL inspection. The lack of a custom CA bundle or environment variable to trust internal certificates stalls enterprise rollout entirely.
- [github/copilot-cli #333](https://github.com/github/copilot-cli/pull/333)

**#3216 – Infinite Loop / Compaction Bug** [OPEN, 0 👍]
- **Summary:** After ~136 turns near the context limit, the agent entered an infinite loop of directory listing and memory compaction overnight, burning API calls. User explicitly requested a refund.
- **Why it matters:** A severe stability bug that undermines trust in unattended sessions. The direct financial cost to users makes this the highest-urgency open issue for the core team to address.
- [github/copilot-cli #3216](https://github.com/github/copilot-cli/pull/3216)

**#3477 – Enterprise OTel Auth (mTLS & Dynamic Headers)** [OPEN, 0 👍]
- **Summary:** Requests parity with Claude Code for mTLS and dynamic auth-token refresh on the OTLP exporter.
- **Why it matters:** Enterprise observability pipelines require more than static headers. Without this, production telemetry integrations remain impossible for security-conscious teams.
- [github/copilot-cli #3477](https://github.com/github/copilot-cli/pull/3477)

**#3709 – BYOK Model Switching** [OPEN, 0 👍]
- **Summary:** The `/model` picker only shows GitHub-hosted models. Users cannot select or switch to local/BYOK models mid-session.
- **Why it matters:** Power users running local models want the same session-level flexibility as hosted models. This is a UX gap that limits the utility of the BYOK feature.
- [github/copilot-cli #3709](https://github.com/github/copilot-cli/pull/3709)

**#2294 – Linux Distro Packaging License (Arch Linux)** [OPEN, 2 👍]
- **Summary:** Arch Linux maintainers seek permission to package the CLI. License Section 2 language around commercial use is causing confusion for non-commercial distro repos.
- **Why it matters:** Official Linux distro packaging is a major vector for adoption. Clarifying the license to explicitly allow this would remove a key community friction point.
- [github/copilot-cli #2294](https://github.com/github/copilot-cli/pull/2294)

**#2828 – Rate Limit Messaging Improvement** [CLOSED, 2 👍]
- **Summary:** Proposed that the CLI should suggest next steps when a weekly rate limit is hit, rather than just presenting a dead-end error.
- **Why it matters:** This was closed recently, suggesting a fix or documentation change was deployed. It highlights a broader desire for helpful, actionable error messages.
- [github/copilot-cli #2828](https://github.com/github/copilot-cli/pull/2828)

**#3710 – FreeBSD Install Script Bug** [OPEN, 0 👍]
- **Summary:** The `curl ... | bash` installer at `gh.io/copilot-install` misidentifies FreeBSD as Windows and fails.
- **Why it matters:** Completely blocks evaluation on FreeBSD. A simple platform detection fix would unlock an entire BSD user base.
- [github/copilot-cli #3710](https://github.com/github/copilot-cli/pull/3710)

**#3712 – Windows ReFS / Dev Drive Limitation** [OPEN, 0 👍]
- **Summary:** A user politely reports that the local sandbox may have limitations on Windows Dev Drive (ReFS), requesting better documentation rather than a fix.
- **Why it matters:** Highlights a platform-specific blind spot. Clear documentation would prevent wasted debugging time for Windows power users.
- [github/copilot-cli #3712](https://github.com/github/copilot-cli/pull/3712)

**#3711 – Windows Registry Version Mismatch** [OPEN, 0 👍]
- **Summary:** Running `/update` to v1.0.60 does not update the corresponding Windows Registry entry.
- **Why it matters:** This breaks external tooling and inventory scripts that rely on the registry for version detection.
- [github/copilot-cli #3711](https://github.com/github/copilot-cli/pull/3711)

**#3396 – GITHUB_TOKEN CI/CD Confusion** [CLOSED, 0 👍]
- **Summary:** In GitHub Actions, the CLI silently picks up `GITHUB_TOKEN` and forwards it to the backend, causing a confusing authorization error.
- **Why it matters:** A silent failure mode in CI/CD. The closure suggests a fix was applied (likely a better error message or token detection logic).
- [github/copilot-cli #3396](https://github.com/github/copilot-cli/pull/3396)

---

### 4. Key PR Progress
PR activity was minimal, with only one open pull request in the last 24 hours:

**#3708 – Add files via upload** [OPEN]
- **Author:** panchofrancisco1987-ui. This PR lacks a descriptive summary and appears to be an early or experimental draft. It requires triage and review from the maintainers before it can be considered for merge.
- [github/copilot-cli #3708](https://github.com/github/copilot-cli/pull/3708)

*Note: No other PRs were updated or submitted in this window.*

---

### 5. Feature Request Trends
The following high-level themes emerge from the active Issues:

1. **Enterprise Networking & Security:**
   The strongest signal is for deeper enterprise integration. Users need custom CA support for SSL inspection (#333) and mTLS/auto-refreshing tokens for OpenTelemetry (#3477). These are non-negotiable features for regulated or large-scale corporate deployments.

2. **Model Flexibility & Visibility:**
   Users want the `/model` picker to expose local/BYOK models, allowing seamless switching within a single session (#3709). This reflects a desire for the CLI to be model-agnostic, treating local providers as first-class citizens.

3. **Platform Inclusivity:**
   There is clear demand for official Linux distribution packaging (#2294) and fixing the installer for non-Linux Unix systems like FreeBSD (#3710).

4. **Session Stability & Cost Guardrails:**
   The infinite-loop bug (#3216) has ignited discussion around session termination policies, cost caps, and better memory management for long-running agents.

---

### 6. Developer Pain Points

- **Financial Risk from Agent Loops:** Issue #3216 perfectly articulates the fear of running long headless sessions. The infinite directory-listing and compaction loop leads to uncontrolled API consumption and an explicit refund request, indicating a serious lack of trust in session stability.

- **Enterprise Proxy Hell:** The SSL inspection issue (#333) remains one of the highest-friction points for corporate adoption. The absence of environment variables for custom CAs or certificate bundles forces many enterprise users to abandon the CLI.

- **CI/CD Integration Pitfalls:** The silent failure when `GITHUB_TOKEN` is present (#3396) demonstrates that the CLI is not yet optimized for the GitHub Actions environment. Even though it is closed, it highlights a broader need for robust CI/CD detection and error messaging.

- **Platform Parity Gaps:** Users on FreeBSD are completely blocked by a simple installer bug (#3710). Windows users face undocumented sandbox restrictions (#3712) and version management issues (#3711). Linux distro maintainers are blocked by licensing ambiguity (#2294). Each of these is a small but sharp wall preventing wider community contribution and adoption.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-08

**Key Theme:** The `kimi-cli` → `kimi-code` transition hit a flashpoint today, with six fresh bug reports and a closed community backlash issue fueling concerns about stability, agent reliability, and strategic direction.

---

## 1. Today's Highlights

The migration from `kimi-cli` to `kimi-code` is producing notable friction, with a wave of critical bugs around agent session states, installation conflicts, and local Ollama integration. A strongly worded community challenge to the product split (#2381) was closed without a visible public response, adding to trust concerns. No new releases were cut, though a long-standing build fix (PR #774) was finally merged.

---

## 2. Releases

No new releases for `kimi-cli` or `kimi-code` were published in the last 24 hours.

---

## 3. Hot Issues

Activity was concentrated in **7 issues**, all reviewed below due to their relevance to the ongoing transition.

**#2437 — Migration Feedback: unclear state, quota confusion, and possible agent quality regression**
- **Who:** `865x44` (Fedora Linux, migrated from `kimi-cli v1.47.0` → `kimi-code v0.11.0`)
- **Why it matters:** A detailed, clinical post-migration report covering version history, quota attribution problems, and suspected LLM quality regression. This is the highest-signal bug report of the day.
- [MoonshotAI/kimi-cli Issue #2437](https://github.com/MoonshotAI/kimi-cli/issues/2437)

**#2436 — Installation failed: "Kimi can't seem to make up her mind"**
- **Who:** `pleabargain`
- **Why it matters:** Reports a split-brain state where old and new binaries interfere with each other. Indicates a critical flaw in the tooling coexistence logic.
- [MoonshotAI/kimi-cli Issue #2436](https://github.com/MoonshotAI/kimi-cli/issues/2436)

**#2381 — Why abandon kimi-cli and redo kimi code? [CLOSED]**
- **Who:** `QuantumLiu`
- **Why it matters:** A strongly worded objection to the strategic fork, including a subscription cancellation threat. The issue was closed without a visible roadmap explanation, which may deepen community dissatisfaction.
- [MoonshotAI/kimi-cli Issue #2381](https://github.com/MoonshotAI/kimi-cli/issues/2381)

**#2438 — Agent status unknown; cannot dive into agentic session**
- **Who:** `dmorsin` (kimi-code user)
- **Why it matters:** The core "agentic session" feature returns an opaque "unknown" status, making the feature completely unusable. A blocking bug for the tool's main value proposition.
- [MoonshotAI/kimi-cli Issue #2438](https://github.com/MoonshotAI/kimi-cli/issues/2438)

**#2439 — `compaction.unable` error when using local Ollama model**
- **Who:** `regul8or` (Linux, local Ollama)
- **Why it matters:** Local model support is a key differentiator. This `compaction.unable` error breaks the entire offline/self-hosted workflow.
- [MoonshotAI/kimi-cli Issue #2439](https://github.com/MoonshotAI/kimi-cli/issues/2439)

**#2440 — Clickable symbol / line references in Kimi Code chat panel**
- **Who:** `ElPrg`
- **Why it matters:** A clean UX enhancement request: inline-code symbols (functions, classes) should be clickable to navigate to definitions. Represents a broader user expectation for IDE-grade terminal interaction.
- [MoonshotAI/kimi-cli Issue #2440](https://github.com/MoonshotAI/kimi-cli/issues/2440)

**#2269 — Remote Control / Multi-Device Session Handoff**
- **Who:** `lucianaluma777`
- **Why it matters:** A long-standing feature request (May 13) with 5 comments. Users want seamless session continuity across laptop, web, and mobile — a major workflow unlock.
- [MoonshotAI/kimi-cli Issue #2269](https://github.com/MoonshotAI/kimi-cli/issues/2269)

---

## 4. Key PR Progress

Only **1 PR** was touched in the last 24 hours.

**#774 — fix: correct module-name type in `pyproject.toml` [CLOSED]**
- **Who:** `sherlockGH-coder`
- **What it does:** Resolves a TOML parse error where `module-name` was incorrectly defined as an array instead of a string, which broke `make prepare` for local development builds.
- **Why it matters:** While a small fix, its closure after 4 months (since January 29) signals a backlog cleanup effort. It directly unblocks developers trying to build from source.
- [MoonshotAI/kimi-cli PR #774](https://github.com/MoonshotAI/kimi-cli/pull/774)

---

## 5. Feature Request Trends

The signal-to-noise ratio is heavily skewed toward **stability and recovery** right now, but two clear feature themes are emerging:

- **Seamless Multi-Device Workflows (#2269):** Users expect sessions to follow them across devices. This has sustained interest since May and is the most engaged feature request.
- **IDE-Grade Terminal UX (#2440):** The request for clickable symbol definitions suggests users want `kimi-code` to feel like an intelligent editor, not just a REPL. Deep linking and inline code intelligence are becoming baseline expectations.

---

## 6. Developer Pain Points

1. **Migration Breakdown:** The coexistence of `kimi-cli` and `kimi-code` is actively breaking environments (#2436). Users feel forced into a new tool without a clean migration path.
2. **Agentic Feature Unreliability:** The "agent status unknown" error (#2438) blocks the marquee feature. Combined with suspected regression (#2437), trust in the agent layer is eroding.
3. **Local Model Integration Friction:** The Ollama `compaction.unable` error (#2439) damages credibility with the privacy-conscious / cost-sensitive developer segment.
4. **Trust and Communication Deficit:** The closure of the community challenge (#2381) without a visible public roadmap or apology is a red flag for developer relations. Users interpreting the silence as dismissal is a growing risk.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

**OpenCode Community Digest – June 8, 2026**

---

### 1. Today's Highlights
- The community is heavily rallying around **Gemma 4 tool-calling failures** ([#20995](https://github.com/anomalyco/opencode/issues/20995), [#21034](https://github.com/anomalyco/opencode/issues/21034)) and the urgent need for **agent sandboxing** ([#2242](https://github.com/anomalyco/opencode/issues/2242)), signaling a shift toward production reliability and security.
- A critical performance discussion has emerged: a user reports that OpenCode itself is **heavily CPU-bound** ([#21470](https://github.com/anomalyco/opencode/issues/21470)), consuming 1.5 million internal tokens against just $8.30 in model costs, raising questions about the efficiency of the orchestration loop.
- The PR queue is strong, with high-impact fixes landing for **WSL stability** ([#31095](https://github.com/anomalyco/opencode/pull/31095)), **MCP server capability detection** ([#31271](https://github.com/anomalyco/opencode/pull/31271)), and a major **TUI transcript filtering experiment** from core contributor `antfu` ([#31294](https://github.com/anomalyco/opencode/pull/31294)).

---

### 2. Releases
No new releases in the last 24 hours.

---

### 3. Hot Issues

1. **[#2242](https://github.com/anomalyco/opencode/issues/2242) – Sandboxing the Agent** *(63 comments, 51 👍)*
   The highest-engagement open issue. Users want macOS-style seatbelt restrictions to prevent the agent from accessing files outside the current directory. This reflects a strong demand for enterprise-grade security controls.

2. **[#20995](https://github.com/anomalyco/opencode/issues/20995) – Gemma 4 (e4b) Tool Calls Not Recognized via Ollama** *(26 comments, 47 👍)*
   The model returns valid `tool_calls`, but OpenCode fails to parse them from the streaming OpenAI-compatible API response. Blocking a major new model family for local users.

3. **[#21034](https://github.com/anomalyco/opencode/issues/21034) – Gemma-4 Interaction Loops/Failures** *(18 comments, 19 👍)*
   Related to #20995 but broader: even with the latest LM Studio and llama.cpp engine fixes, Gemma 4 models remain unusable in OpenCode due to tool loop failures.

4. **[#21470](https://github.com/anomalyco/opencode/issues/21470) – OpenCode is Heavily CPU-Bound** *(10 comments, 10 👍)*
   A deep-dive report showing OpenCode consumes more compute time internally than waiting on model API calls. The session spent $8.30 on model tokens but 1.5 million tokens internally. A critical performance red flag.

5. **[#15585](https://github.com/anomalyco/opencode/issues/15585) – "Free Usage Exceeded" Despite Free Models** *(47 comments, 12 👍)*
   Users hitting rate limits on supposedly "free" models. Confusion persists around OpenCode's actual free tier policy versus advertised model pricing.

6. **[#22132](https://github.com/anomalyco/opencode/issues/22132) – OpenCode Hangs with Local Ollama Provider** *(9 comments)*
   Even simple prompts like `ci` cause OpenCode to freeze when using Ollama via the `@ai-sdk/openai-compatible` bridge, while direct API calls work fine.

7. **[#31147](https://github.com/anomalyco/opencode/issues/31147) – AWS Bedrock SSO Regression in 1.16** *(7 comments)*
   A recent update broke AWS credential resolution for SSO users, crashing with a cryptic `Symbol` error. Highlights fragile provider integrations.

8. **[#29182](https://github.com/anomalyco/opencode/issues/29182) – Refund Request Unanswered for 12 Days** *(7 comments)*
   A user reports complete radio silence from support on a $5 refund, eroding trust in billing operations. Related to broader billing confusion in the community.

9. **[#30807](https://github.com/anomalyco/opencode/issues/30807) – Prune Bugs: Instruction Re-attachment & Early-Exit** *(4 comments)*
   Two subtle but critical bugs in the pruning mechanism: pruning can re-attach stale instruction files and skip older prunable tools, degrading agent behavior over long sessions.

10. **[#25848](https://github.com/anomalyco/opencode/issues/25848) – [Feature] Session Renaming** *(7 comments)*
    A persistent UX request. Users want `/rename` or CLI commands to manually label sessions, which is currently lacking.

---

### 4. Key PR Progress

1. **[#31294](https://github.com/anomalyco/opencode/pull/31294) – feat(tui): web-style transcript filtering** *(antfu)*
   Merged experimental filtering for the TUI that hides internal steps, tool states, and patches in the transcript. A significant UX improvement for power users.

2. **[#31297](https://github.com/anomalyco/opencode/pull/31297) – fix(shell): force UTF-8 for PowerShell** *(duofuwang)*
   Finally fixes garbled Chinese/Unicode output on Windows. Closes three separate issues (#23636, #31187, #30205).

3. **[#31299](https://github.com/anomalyco/opencode/pull/31299) – fix(task): propagate subagent errors** *(iloli-25)*
   Prevents agents from hanging indefinitely when a subagent fails, using a race between error events and a 120s timeout. Closes #5204.

4. **[#31271](https://github.com/anomalyco/opencode/pull/31271) – fix(opencode): respect MCP server capabilities** *(rekram1-node)*
   Stops OpenCode from forcibly requesting `tools/list` from prompt-only MCP servers. Keeps prompt/resource-only servers connected.

5. **[#25649](https://github.com/anomalyco/opencode/pull/25649) – fix: increase LSP initialize timeout for JDTLS/KotlinLS** *(norbu35)*
   Raises the hardcoded 20s LSP timeout to handle slow JVM-based project syncs. Critical for Java/Kotlin users with large Gradle projects.

6. **[#31095](https://github.com/anomalyco/opencode/pull/31095) – fix(desktop): few WSL bugs** *(neriousy)*
   Fixes `distroReady` initialization errors, broken sidebar server removal, and stale WSL distro detection.

7. **[#31283](https://github.com/anomalyco/opencode/pull/31283) – fix(desktop): stabilize snapshot sidecar lifecycle** *(Hona)*
   Prevents snapshot capture from blocking on stale Git index locks and desktop server crashes from late pipe errors.

8. **[#31211](https://github.com/anomalyco/opencode/pull/31211) – fix(tui): replace scheduled with manual debounce** *(malventano)*
   Removes a Node.js compatibility regression from `@solid-primitives/scheduled` that broke the TUI under certain build conditions.

9. **[#30849](https://github.com/anomalyco/opencode/pull/30849) – fix(opencode): strip MiniMax trailing tool_call leak suffix** *(ulises-jeremias)*
   Targeted sanitizer for a MiniMax artifact where assistant text leaks a tool-call marker. Highlights the ongoing battle with model-provider quirks.

10. **[#26167](https://github.com/anomalyco/opencode/pull/26167) – fix(session): retry empty stream truncations** *(edevil)*
    When providers end a stream without a proper `stop_reason`, OpenCode now discards the truncated part and retries, preventing silent session corruption.

---

### 5. Feature Request Trends

- **Security & Compliance**: The #2242 sandboxing discussion is the loudest signal yet that users want restricted execution contexts (file access, network, git operations) for production deployments.
- **Provider Depth**: Users are no longer satisfied with basic API compatibility. Demands are rising for specific variant support (MiniMax M3 thinking modes [#31180](https://github.com/anomalyco/opencode/issues/31180)), better local model integration, and smoother SSO/credential flows.
- **Quality of Life / UX**: Session renaming ([#25848](https://github.com/anomalyco/opencode/issues/25848)), LaTeX rendering in the web UI ([#24426](https://github.com/anomalyco/opencode/issues/24426)), and improved TUI navigation (word-by-word [#3090](https://github.com/anomalyco/opencode/issues/3090), paragraph copy [#3091](https://github.com/anomalyco/opencode/issues/3091)) are small changes with broad appeal.

---

### 6. Developer Pain Points

1. **Provider Fragility & Regressions**
   Every release risks breaking a provider integration. The AWS Bedrock SSO regression ([#31147](https://github.com/anomalyco/opencode/issues/31147)) and Ollama hangs ([#22132](https://github.com/anomalyco/opencode/issues/22132)) demonstrate how fragile the provider layer is, forcing constant churn.

2. **Model Tool-Calling Unreliability**
   Gemma 4 and MiniMax are repeatedly failing on tool calls. Issues like the MiniMax leak ([#30849](https://github.com/anomalyco/opencode/issues/30849)) and Gemma parse failures ([#20995](https://github.com/anomalyco/opencode/issues/20995)) require model-specific sanitizers, which don't scale.

3. **High Internal Resource Consumption**
   The CPU-bound report ([#21470](https://github.com/anomalyco/opencode/issues/21470)) exposes a core tension: OpenCode's orchestration loop is often the bottleneck, not the LLM. This directly impacts cost and speed for users.

4. **Billing Confusion & Support Friction**
   Free tier limits ([#15585](https://github.com/anomalyco/opencode/issues/15585), [#14273](https://github.com/anomalyco/opencode/issues/14273)), double charges ([#29248](https://github.com/anomalyco/opencode/issues/29248)), and unresponsive refund support ([#29182](https://github.com/anomalyco/opencode/issues/29182)) are eroding community trust.

5. **Context Window Management Bugs**
   Subtle bugs in pruning ([#30807](https://github.com/anomalyco/opencode/issues/30807)) and context compaction leakage ([#28355](https://github.com/anomalyco/opencode/issues/28355)) cause agents to "forget" rules or re-attach stale instructions, breaking long-running sessions.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest
**June 8, 2026**

## 1. Today's Highlights
The community maintains a blistering pace, closing significant issues around provider compatibility and session state management. A critical bug where shell directory changes (`cd`) were captured but never propagated to the session has been identified, alongside rapid fixes for model hallucination of days of the week in the system prompt. Performance receives strong attention, with PRs optimizing session switching and improving context estimation accuracy after compaction.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues

**#5427 — OpenAI Codex Transport Issues (Active)** – Users of OpenAI Codex models via ChatGPT subscriptions are encountering persistent `SSE response headers timed out after 10000ms` errors mid-conversation, making sessions unusable. The only active open issue in this selection, signaling rough edges with OpenAI's streaming infrastructure.
- *Link:* [earendil-works/pi Issue #5427](https://github.com/earendil-works/pi/issues/5427)

**#5464 — Local Model "Working" Latency** – Running local models via Ollama introduces a 3–5 minute "Working" status delay on even simple messages. This severely degrades the local-first use case and has drawn community attention.
- *Link:* [earendil-works/pi Issue #5464](https://github.com/earendil-works/pi/issues/5464)

**#5485 — Day of Week Hallucinations** – `YYYY-MM-DD` injection in the system prompt causes smaller models (e.g., GLM-5.1) to hallucinate the day of the week. A fix was shipped almost immediately (PR #5486) showing strong maintainer responsiveness.
- *Link:* [earendil-works/pi Issue #5485](https://github.com/earendil-works/pi/issues/5485)

**#5469 — MCP Tool Result Collapse Request** – Heavy MCP users are requesting default collapsible output blocks to reduce terminal noise from tools like `fetch` and `brave_search`. The desire for a `settings.json` opt-out signals a need for configurable output density.
- *Link:* [earendil-works/pi Issue #5469](https://github.com/earendil-works/pi/issues/5469)

**#5478 — CWD Bridge Propagation Failure (Critical)** – Pi captures the working directory after `bash` tool execution but never reads the captured value back. Commands like `cd` silently succeed in the shell but fail to update the session, tools, or footer. A fundamental state management bug.
- *Link:* [earendil-works/pi Issue #5478](https://github.com/earendil-works/pi/issues/5478)

**#5428 — Plan Mode Refine Error** – Refining a plan generated by the example `plan-mode` extension triggers an `Agent is already processing` error. The root cause is traced to extension-triggered message queuing (related to #5062), affecting workflow users.
- *Link:* [earendil-works/pi Issue #5428](https://github.com/earendil-works/pi/issues/5428)

**#5402 — Slow Cold Start** – Startup adds ~2.4 seconds purely from Node.js loading 138MB of provider SDK dependencies at import time. With `--no-extensions`, this remains the dominant contributor to slow cold starts, indicating need for lazy loading.
- *Link:* [earendil-works/pi Issue #5402](https://github.com/earendil-works/pi/issues/5402)

**#5456 — `openai-responses` Developer Role Ignored** – The `openai-responses` provider forces `role: "developer"` when reasoning is enabled, ignoring `compat.supportsDeveloperRole: false`. Breaks providers that only accept the `system` role.
- *Link:* [earendil-works/pi Issue #5456](https://github.com/earendil-works/pi/issues/5456)

**#5438 — Clipboard Image Paste Failure** – In interactive mode, pasting an image inserts the temp file path into the editor but the actual image bytes are never attached to the model request. Model and provider independent — the bug is in the editor integration layer.
- *Link:* [earendil-works/pi Issue #5438](https://github.com/earendil-works/pi/issues/5438)

**#5487 — SSH Extension Tool Conflict** – Loading the SSH example extension prevents other extensions from overriding core tools (`bash`, `edit`). A tool routing isolation gap in the extension system, limiting composability.
- *Link:* [earendil-works/pi Issue #5487](https://github.com/earendil-works/pi/issues/5487)

## 4. Key PR Progress

**#5486 — fix: include day of week in Current date** – Rapid fix for Issue #5485. Modifies system prompt injection to include the full day name alongside the date. Landed same day as the bug report.
- *Link:* [earendil-works/pi PR #5486](https://github.com/earendil-works/pi/pull/5486)

**#5479 — perf: reuse services on same-cwd session switch** – Significant optimization. Session switches in the same working directory now reuse existing services (settings, models, auth) instead of calling `createRuntime()`. Reduces overhead for multi-session workflows.
- *Link:* [earendil-works/pi PR #5479](https://github.com/earendil-works/pi/pull/5479)

**#5481 — feat: require bash descriptions and default timeout** – Enforces a required `description` field on bash tool calls and adds a default timeout. Improves log readability by forcing explainable commands and prevents hanging shells.
- *Link:* [earendil-works/pi PR #5481](https://github.com/earendil-works/pi/pull/5481)

**#5480 — fix: estimate context usage after compaction** – Prevents footer showing `?/200k` post-compaction. Estimates token count from compressed state rather than returning null, providing continuous context feedback.
- *Link:* [earendil-works/pi PR #5480](https://github.com/earendil-works/pi/pull/5480)

**#5472 — feat: add Requesty as native provider** – Integrates Requesty.ai as a first-class provider in `packages/ai`. `requesty/...` model identifiers now work out of the box without custom endpoint configuration.
- *Link:* [earendil-works/pi PR #5472](https://github.com/earendil-works/pi/pull/5472)

**#5471 — fix: don't unconditionally continue after compaction** – Fixes Issue #5463. Threshold-based auto-compaction was triggering `agent.continue()` even without queued messages, causing an illegal state assertion. Prevents a class of mid-session crashes.
- *Link:* [earendil-works/pi PR #5471](https://github.com/earendil-works/pi/pull/5471)

**#5467 — Include models.json path in migration parse errors** – Developer experience improvement. Parse errors during `models.json` migrations now report the absolute file path, drastically simplifying debugging of malformed user configs.
- *Link:* [earendil-works/pi PR #5467](https://github.com/earendil-works/pi/pull/5467)

**#5465 — feat: add mineru document-parsing skill** – New community skill under `.pi/skills/mineru/`. Provides a CLI wrapper for Mineru's document parsing API with URL/local file upload, polling, and extraction support.
- *Link:* [earendil-works/pi PR #5465](https://github.com/earendil-works/pi/pull/5465)

## 5. Feature Request Trends
The community is heavily focused on **extending the public API surface** of Pi. Multiple requests target exposing internal components (`RpcExtensionUIRequest`, `runAgentSession`, `ExtensionContext` methods) to enable more powerful third-party extensions and programmatic control. There is a steady demand for **improved UX configuration**, specifically around controlling output clutter (collapsible MCP tool results, configurable clipboard image storage paths). **Provider flexibility** remains a priority, with requests for dynamic model list updates from OpenRouter and the ability to opt out of specific built-in sandbox tools.

## 6. Developer Pain Points
The most significant friction stems from **provider API instability and compatibility**. Issues with Anthropic's thinking blocks (Opus 4.8), OpenAI Codex transport timeouts, and the forced `developer` role type mismatch dominate the bug reports. **Performance regressions** are a recurring annoyance, highlighted by the ~2.4s cold start cost from eager provider imports and multi-minute latency on local models. The **extension system's lack of isolation** (tool name conflicts between extensions) and **state management bugs** (CWD not propagating, compacted context showing `null`) are creating friction for developers building on top of the platform.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

**Qwen Code Community Digest — 2026-06-08**

### 1. Today’s Highlights
The development velocity around the Qwen Code daemon and ACP protocol integration is at an all-time high, with new WebSocket transport, session reaping, and runtime language switching PRs landing alongside critical stability patches. A nightly `v0.17.1` fixes a long-standing UX annoyance—clipping internal reasoning tokens from copied output—while the community continues to push for declarative agent definitions and dynamic model fallbacks to match the extensibility of competing tools. Long-running session memory management received focused attention, with a targeted OOM fix entering review.

### 2. Releases
No stable release today. The team published **`v0.17.1-nightly.20260608.aea34fa2c`**. The only changelog entry is a UX fix: `fix(cli): skip thought parts in copy output by @he-yufeng`. This ensures that internal thinking/speculative tokens no longer flood the clipboard when copying AI responses, a notable quality-of-life improvement for users of prompt-caching or reasoning-heavy models.

### 3. Hot Issues
*(10 noteworthy issues from the 15 updated in the last 24h)*

1. **[#4514](https://github.com/QwenLM/qwen-code/issues/4514) – Tracking: Daemon Capability Gaps (doudouOUC)** – The most active issue right now (13 comments). Tracks the remaining gaps in `qwen serve` HTTP/SSE surface for full ACP compatibility post-v0.16-alpha. A strategic roadmap item.

2. **[#4821](https://github.com/QwenLM/qwen-code/issues/4821) – Declarative Agent Definitions (qqqys)** – Proposes defining custom agents via Markdown files with YAML frontmatter, directly modeled on Claude Code’s `.claude/agents` pattern. High community engagement (5 comments) and strong ecosystem leverage.

3. **[#4782](https://github.com/QwenLM/qwen-code/issues/4782) – ACP Streamable HTTP Transport Tracking (chiga0)** – Closely related to the daemon maturation thread. Documents the status of native ACP transport, which would allow editors like Zed, Goose, and JetBrains to connect without adapters.

4. **[#4550](https://github.com/QwenLM/qwen-code/issues/4550) – LAN Startup Blocked (sotex)** – Critical blocker for enterprise adoption. Users in air-gapped internal networks report being stuck on the initialization step indefinitely. Requesting a flag to skip connectivity checks.

5. **[#1206](https://github.com/QwenLM/qwen-code/issues/1206) – Dynamic Multi-Model Switching (benzntech)** – Long-standing feature request (since Dec 2025) for dynamically fetching and switching models from OpenAI-compatible endpoints. Only 1 comment today but high strategic value for hybrid deployments.

6. **[#4538](https://github.com/QwenLM/qwen-code/issues/4538) – Harden AUTO Mode Against Self-Modification (qqqys)** – Safety-focused feature request for policy guardrails around agent configuration file modifications and denial-bypass attempts. Receives a 👍 for urgency.

7. **[#4830](https://github.com/QwenLM/qwen-code/issues/4830) – Fallback Model Support (qqqys)** – Quickly closed as duplicate/discussion-needed, but signals strong developer demand for resilient long-running sessions that don't hard-fail on transient provider errors.

8. **[#4257](https://github.com/QwenLM/qwen-code/issues/4257) – System Sleep Prevention (fantasyz)** – A classic pain point: the agent loses progress when the OS sleeps during long tasks. Now resolved by the merged PR #4434.

9. **[#4568](https://github.com/QwenLM/qwen-code/issues/4568) – Submodule `@` File Completion (undici77)** – Bug impacting monorepo workflows: the file picker (`@`) shows submodule directories but lists zero files inside them.

10. **[#4744](https://github.com/QwenLM/qwen-code/issues/4744) – `/copy N` Support (huww98)** – Simple but highly practical quality-of-life request for the terminal UI: extending `/copy` to accept a numeric argument to copy older messages.

### 4. Key PR Progress
*(10 important PRs representing major features or critical fixes)*

1. **[#4773](https://github.com/QwenLM/qwen-code/pull/4773) – ACP WebSocket Transport (chiga0)** – Adds WebSocket adapter for the daemon, coexisting with SSE. A significant leap toward real-time, full-duplex daemon communication. Depends on #4827.

2. **[#4732](https://github.com/QwenLM/qwen-code/pull/4732) – Workflow Tool P1: `node:vm` Sandbox (LaZzyMan)** – Implements a minimal JavaScript sandbox with `agent()` sequential call support. The foundational piece for the previously requested "Ultracode" dynamic workflow system.

3. **[#4824](https://github.com/QwenLM/qwen-code/pull/4824) – OOM Prevention via History Compaction (zzhenyao)** – Three targeted fixes to prevent old-space exhaustion in long sessions: microcompaction on Hook messages, memory-pressure-triggered compaction, and removing en-dash characters from API history to reduce token waste.

4. **[#4713](https://github.com/QwenLM/qwen-code/pull/4713) – MCP Project Config Approval Gating (qqqys)** – Considers project-level `.mcp.json` as untrusted-until-approved, establishing a coherent precedence model for MCP server sources. Addresses a core safety concern (#4615).

5. **[#4810](https://github.com/QwenLM/qwen-code/pull/4810) – OpenAI SDK Abort Listener Leak Fix (yiliang114)** – Wraps the `AbortSignal` in per-request child controllers to isolate the SDK’s internal listener leak. Critical for avoiding memory creep in long-running agent loops.

6. **[#4833](https://github.com/QwenLM/qwen-code/pull/4833) – Session Idle Reaper (chiga0)** – Adds a background reaper that tears down daemon sessions with no SSE subscribers, no active prompts, and an expired heartbeat (default 30 min TTL).

7. **[#4795](https://github.com/QwenLM/qwen-code/pull/4795) – TUI Screen Flash Elimination (zzhenyao)** – Fixes the full-screen flash that occurs in compact mode by preventing cross-group tool data-level merges when `useTerminalBuffer` is false.

8. **[#4705](https://github.com/QwenLM/qwen-code/pull/4705) – Runtime Language Switching (chiga0)** – Adds `POST /session/:id/language` for switching both UI language and LLM output language mid-session without polluting the transcript. Follows the same pattern as the approval-mode bridge.

9. **[#4704](https://github.com/QwenLM/qwen-code/pull/4704) – Honor Skill `allowedTools` (tanzhenxin)** – Finally makes the `allowedTools` field functional by auto-approving declared tools for the session. Lowers friction for skill authors and enhances the autonomy of the skill system.

10. **[#4434](https://github.com/QwenLM/qwen-code/pull/4434) – System Sleep Inhibitor (DragonnZhang)** – *Merged.* Adds a runtime sleep inhibitor (platform-specific) so long-running agent tasks do not get interrupted by the OS power manager. Directly closes the high-pain issue #4257.

### 5. Feature Request Trends

- **Daemon as a First-Class ACP Host**: The strongest trend. Multiple tracking issues and PRs (#4514, #4782, #4773, #4833) are converging to make `qwen serve` a robust protocol server for external editors, moving beyond a simple CLI flag.
- **Declarative Configuration for Agents & Skills**: The community is aggressively pursuing code-free extensibility. Patterned after Claude Code’s frontmatter agents (#4821) and the new `allowedTools` auto-approval (#4704), the goal is to let users define custom behaviors without forking TypeScript.
- **Production Safety & Reliability**: Safety features are in high demand: hardened AUTO mode (#4538), MCP trust gating (#4713), and fallback model routing (#4830). Users increasingly want to run agents unattended and are building feedback loops that demand resilience.
- **Multimodal & Model Flexibility**: Repeated calls for dynamic model switching (#1206) and correct model detection for multimodal support (#4802) signal that the community is using Qwen Code across diverse backends (local, cloud, proxy) and expects seamless modality handling.

### 6. Developer Pain Points

- **Enterprise Network Blockers**: The most concrete operational pain point is the initialization failure in air-gapped environments (#4550). Hitting a hard wall requiring a workaround to skip connectivity checks.
- **Long-Running Session Instability**: Memory leaks in the OpenAI SDK wrapper (#4810) and unbounded history growth (#4824) are the top “silent dealbreaker” issues, killing sessions that should run for hours.
- **Terminal UX Friction**: Despite steady improvements, terminal pain points crop up frequently: submodule `@` completions showing empty directories (#4568), screen flashes on tool completions (#4795), and limited copy commands (#4744).
- **Multimodal Integration Fragility**: Clipboard image paste silently failing (#3517, fixed by #4647) and model modality fingerprints falling through regex detection rules (#4802) highlight that common visual workflows can feel like edge cases.
- **Lack of Model Provider Resilience**: The inability to specify fallback models or dynamically change providers mid-session forces manual restarts when API rate limits or outages occur (#4830, #1206).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) Community Digest – June 8, 2026

---

## 1. Today's Highlights

The community is laser-focused on **cost efficiency and reliability**, with token consumption and cache hit rates dominating discussions. A massive contribution from HUQIANTAO delivered **five pull requests fixing 30+ critical bugs** spanning security, concurrency, error handling, and tools (PRs #2880–#2884). Meanwhile, LeoAlex0’s cache optimization PRs (#2874, #2877) directly target the runaway token usage reported in #1177 and #743. The **v0.9.0 stewardship branch** (#2762) is actively consolidating these changes, signaling a major release on the horizon. Internationalization also saw strong momentum, with Gordon Lu localizing dialog surfaces across seven locales.

---

## 2. Releases

**No official releases in the last 24 hours.** The latest stable version remains v0.8.52. The maintainer is actively integrating contributions into the `codex/v0.9.0-stewardship` branch (#2762). Note: the npm wrapper version (v0.8.47) continues to lag behind the binary version (v0.8.49+), causing update confusion (ref. Issue #2561).

---

## 3. Hot Issues (10 of 30)

1. **[Hmbown/CodeWhale Issue #1177](https://github.com/Hmbown/CodeWhale/issues/1177) – Input cache hit rate too low**  
   A direct comparison against DeepSeek-Reasonix (95%+ hit rate) flags a serious cost gap. High community resonance with 24 comments demanding better caching strategy.

2. **[Hmbown/CodeWhale Issue #743](https://github.com/Hmbown/CodeWhale/issues/743) – Token consumption explosion (4B tokens in half a day)**  
   User reports extreme API burn, explicitly requesting optimization of request density and dialogue interaction volume. Urgent cost concern.

3. **[Hmbown/CodeWhale Issue #1969](https://github.com/Hmbown/CodeWhale/issues/1969) – Migration anxiety after rename to CodeWhale**  
   Users fear loss of sessions and skills. Documentation gap identified for migration without manual download.

4. **[Hmbown/CodeWhale Issue #2328](https://github.com/Hmbown/CodeWhale/issues/2328) – `exec_shell` tool mode inconsistency**  
   Works in YOLO mode but fails in Agent mode, contradicting documentation. Blocks tool-dependent workflows.

5. **[Hmbown/CodeWhale Issue #1620](https://github.com/Hmbown/CodeWhale/issues/1620) – Extremely slow thinking process**  
   Character-by-character output is reported as “one word per half day,” raising concerns about streaming or rendering bottlenecks.

6. **[Hmbown/CodeWhale Issue #2620](https://github.com/Hmbown/CodeWhale/issues/2620) – Freeze and text overflow on refactoring task (v0.8.50)**  
   UI becomes completely unresponsive; text spills outside terminal bounds. Blocking for development workflows.

7. **[Hmbown/CodeWhale Issue #2739](https://github.com/Hmbown/CodeWhale/issues/2739) – Stuck in infinite wait loop**  
   Time-out recovery loses session context. User reports abandoning the tool after repeated frustration in v0.8.51/0.8.52.

8. **[Hmbown/CodeWhale Issue #2261](https://github.com/Hmbown/CodeWhale/issues/2261) – TUI crash leaks input to PowerShell**  
   Critical UX defect: lost keyboard focus causes typed input to be executed by the parent shell verbatim.

9. **[Hmbown/CodeWhale Issue #1425](https://github.com/Hmbown/CodeWhale/issues/1425) – Multi-agent deadlock on large text processing**  
   Analyzing a 3-million-word novel fails due to `agent_wait` timeouts. Highlights scalability limits in the agent scheduler.

10. **[Hmbown/CodeWhale Issue #2346](https://github.com/Hmbown/CodeWhale/issues/2346) – AI agent unresponsive to mode switching**  
    Agent ignores Plan/Agent state changes, wasting tokens retrying rejected tool calls. Mode transparency is a high-priority UX request.

---

## 4. Key PR Progress (10 of 20)

1. **[Hmbown/CodeWhale PR #2892](https://github.com/Hmbown/CodeWhale/pull/2892) – feat(i18n): Localize sandbox elevation dialog (7 locales)**  
   Gordon Lu extends i18n coverage for elevation prompts across En, Ja, ZhHans, ZhHant, PtBr, Es419, and Vi.

2. **[Hmbown/CodeWhale PR #2874](https://github.com/Hmbown/CodeWhale/pull/2874) – feat(cache): Slim runtime_prompt for cache stability**  
   LeoAlex0 moves dynamic policy text out of the system prompt into transient messages, directly addressing the cache invalidation problem behind #1177.

3. **[Hmbown/CodeWhale PR #2888](https://github.com/Hmbown/CodeWhale/pull/2888) – refactor(commands): Extract registry and parser helpers**  
   Layer 3 of the staged command-boundary refactor (aboimpinto), decoupling command logic and preparing a cleaner CLI surface.

4. **[Hmbown/CodeWhale PR #2236](https://github.com/Hmbown/CodeWhale/pull/2236) – feat: Vendor-neutral AGENTS.md from ~/.agents/**  
   mvanhorn adds cross-tool compatibility, reading global agent instructions as a fallback for improved interoperability.

5. **[Hmbown/CodeWhale PR #2882](https://github.com/Hmbown/CodeWhale/pull/2882) – fix: Security bugs**  
   HUQIANTAO patches an execution policy bypass via whitespace normalization and fixes approval mapping vulnerabilities.

6. **[Hmbown/CodeWhale PR #2881](https://github.com/Hmbown/CodeWhale/pull/2881) – fix: Error handling (11 bugs)**  
   Silently discarded errors (config persistence, logging) are corrected, preventing masked data loss and improving debuggability.

7. **[Hmbown/CodeWhale PR #2883](https://github.com/Hmbown/CodeWhale/pull/2883) – fix: Concurrency bugs (5 bugs)**  
   Mutex poisoning, thread exhaustion, and Windows compilation failures are resolved, improving runtime stability.

8. **[Hmbown/CodeWhale PR #2869](https://github.com/Hmbown/CodeWhale/pull/2869) – fix(tui): List all provider models in /model picker**  
   ousamabenyounes fixes a high-friction UX bug where custom models saved under a non-active provider were invisible.

9. **[Hmbown/CodeWhale PR #2873](https://github.com/Hmbown/CodeWhale/pull/2873) – feat(config): Hotbar slot persistence (slots 1–8)**  
   reidliu41 lays the config foundation for customizable hotbars, moving toward user-defined key bindings.

10. **[Hmbown/CodeWhale PR #2887](https://github.com/Hmbown/CodeWhale/pull/2887) – test: Gherkin acceptance E2E harness**  
    aboimpinto adds structured BDD-style tests for the command/tool lifecycle, a long-term investment in release quality.

---

## 5. Feature Request Trends

- **Aggressive Caching & Cost Reduction**: The #1 request is fixing the input cache hit rate (target: 95%+). Users are desperate to stop the “token burn” that makes the tool economically unviable for heavy use.
- **Persistent Session Memory**: Cross-session memory is a major blocker for complex tasks. Users expect the agent to remember context from previous sessions without explicit file-level state management (#2492).
- **Mode-Agnostic Tool Behavior**: The community wants tool availability (e.g., `exec_shell`) to be consistent across YOLO, Agent, and Plan modes, removing the cognitive load and token waste of mode-specific restrictions (#2328, #2346).
- **Full Internationalization**: Active PRs localizing sandbox and approval dialogs across seven locales reveal a strong global user base demanding native language support beyond English and Chinese.
- **Custom Workflow Integration**: Requests for user-configurable hotbars, vendor-neutral agent instructions, and per-project agent configuration signal a push toward highly personalized engineering workflows.

---

## 6. Developer Pain Points

- **Runaway API Costs**: The dominant pain point is uncontrollable token expenditure. Users report feeling penalized by verbose context repackaging and ineffective retry loops, wiping out the benefits of fast inference.
- **Session Fragility & Progress Loss**: Frequent freezes, crashes, and unrecoverable timeouts cause developers to lose hours of work. The inability to reliably resume a crashed session is a critical deal-breaker for daily use.
- **Migration & Update Fatigue**: The rename from DeepSeek TUI to CodeWhale created significant confusion about session/skill migration. Discrepancies between package versions (npm vs. binary) further erode trust in the update mechanism.
- **Terminal-Specific Instability**: Developers using niche terminals (Ghostty) or environments (WSL, macOS) face exclusive bugs that are hard to reproduce on primary dev setups, creating a fragmented user experience.
- **Input Handling & UI Glitches**: Persistent minor defects—pasting text triggering execution, overlapping UI elements, broken scrolling—collectively degrade the daily coding loop, adding friction to otherwise productive sessions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*