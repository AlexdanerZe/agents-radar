# AI CLI Tools Community Digest 2026-06-26

> Generated: 2026-06-26 03:23 UTC | Tools covered: 9

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

**Cross-Tool Comparison Report: AI CLI Ecosystem**
June 26, 2026

---

### 1. Ecosystem Overview
The AI CLI tool landscape is navigating a critical inflection point. While agentic capabilities and MCP/plugin infrastructures are maturing rapidly, community sentiment is dominated by a profound reliability and transparency reckoning. Unpredictable token consumption, session data loss, platform instability (particularly Windows/Linux), and orchestration failures have shifted user focus from raw capability to a demanding need for cost control, observability, and deterministic state management. The ecosystem is polarized between a few high-velocity platforms investing heavily in infrastructure and several flagship tools facing community trust crises due to low engineering responsiveness to acute bugs.

---

### 2. Activity Comparison

| Tool | Hot Issues (Today) | Key PRs (Today) | Release Today | Dominant Signal |
|---|---|---|---|---|
| Claude Code | 10 | 1 | Yes (v2.1.193) | Trust erosion: cost shock, model regression, transcript loss |
| OpenAI Codex | 10 | 10 | Yes (v0.142.2, alphas) | Token accounting crisis + heavy MCP platform investment |
| Gemini CLI | 10 | 10 | Yes (v0.51.0, v0.50.0, v0.49.0) | Pervasive agent hangs & false sub-goal success |
| GitHub Copilot CLI | 10 | 1 | Yes (v1.0.66-0) | Session/auth instability & autopilot regression |
| Kimi Code CLI | 2 | 0 | No | MCP scaling ceiling (~200 tools); Linux TUI flicker |
| OpenCode | 10 | 10 | Yes (v1.17.11) | Windows segfault crisis + session snapshots |
| Pi | 10 | 10 | No | TUI viewport instability; daemon architecture (orchestrator PR) |
| Qwen Code | 10 | 10 | No | Windows OOM crash; CI pipeline cross-contamination |
| CodeWhale (prev. DeepSeek TUI) | 10 | 10 | Yes (v0.8.65) | Approval flow overreach; active rebranding |

---

### 3. Shared Feature Directions
Requirements appearing across multiple tool communities:

- **Session Durability & Rollback:** Every major tool faces heat for data loss or context corruption (Claude transcript drop, Codex auto-compaction damage, Copilot session list loss, OpenCode Windows crash). Demand for explicit undo/rollback and reliable resume is universal.
- **Cost Transparency & Token Control:** Claude and Codex lead the backlash against silent model upgrades and 10–20× token accounting jumps. Copilot and CodeWhale respond with budget controls and prompt slimming. Gemini and Qwen explore AST tooling to reduce token waste.
- **MCP Ecosystem Scaling & Lifecycle:** Kimi crashes at ~200 tools. Copilot struggles with OAuth token refresh. OpenCode and Codex invest in service scaffolding. Claude reports raw XML tool output. The protocol is standardizing, but lifecycle, auth, and performance guarantees are immature.
- **Cross-Platform Parity:** Windows and Linux remain second-class citizens. OpenCode (Bun segfault), Qwen (PowerShell OOM), Codex (sandbox dialog loops), Gemini (Wayland lockout), and Kimi (TUI flicker) all expose significant gaps that erode trust outside the macOS bubble.
- **Agent Observability & Mode Discipline:** False positive goal reporting (Gemini), mode confusion (CodeWhale, Claude), and lack of sub-agent trajectory data in debugging tools are universal gaps. Users cannot debug agent orchestration failures.

---

### 4. Differentiation Analysis

- **Claude Code (Anthropic):** Premium agentic depth + safety classifiers. Suffering most acutely from trust regime breakdown. Architecture prioritizes hard reasoning and safety middlewares, but community engagement (380 👍 on feature issue) contrasts dangerously with low engineering output (1 PR today).
- **OpenAI Codex:** Platform and MCP play. Highest strategic infrastructure investment (virtual MCP servers, npm plugins, Rust core). Token accounting crisis is the primary existential threat to its Pro model. Target user: plugin developers and power users seeking extensibility.
- **Gemini CLI (Google):** Structured orchestration (sub-agents, skills) + AST codebase intelligence. Strongest prioritization process (P1/P2 labels, Epics). Differentiates on multi-agent patterns and Vertex AI enterprise routing. Target user: GCP enterprises and ML-heavy teams.
- **GitHub Copilot CLI:** Enterprise governance (managed settings, MCP policy enforcement) + IDE-native workflows. Strongest session/auth reliability pressure. Autopilot regression is a direct hit to its core value proposition. Target user: GitHub shop / managed org deployments.
- **Kimi Code CLI (MoonshotAI):** Low community volume today. Tight coupled to "K2.7 Code" thinking model. Early stage, fragile at scale. MCP 200-tool crash and TUI flicker indicate a small team still finding its footing.
- **OpenCode (AnomalyCo):** Multi-provider broker with strong open-source culture. Highest practical innovation velocity (snapshots, SDK-next, copy-on-select). Windows crisis managed proactively (canary switch). Target user: provider-agnostic power users and SDK integrators.
- **Pi (Earendil Works):** Terminal-crafted engine with extension architecture. Strong theoretical rigor (RPC, viewport lifecycle, orchestrator daemon). Deepest work on TUI stability. Target user: tinkerers, extension developers, and terminal purists.
- **Qwen Code (QwenLM / Alibaba):** CI/CD integration + JetBrains ecosystem. Unique focus on extension creation tools and daemon-based resume (SSE). CI pipeline contamination and Windows OOM are acute growing pains. Target user: JetBrains developers and CI pipeline engineers.
- **CodeWhale (Hmbown):** Token efficiency + approval granularity champions. Rebranding from DeepSeek signals independence. Approval flow overreach is its biggest friction point; persistent rule persistence (#1186) is the designated fix. Target user: token-sensitivity-conscious freelancers and automation-heavy teams.

---

### 5. Community Momentum & Maturity

**High Development Velocity** (10+ PRs, releases, infrastructure bets):
- OpenCode, Pi, Gemini CLI, OpenAI Codex, CodeWhale. These tools demonstrate sustained commit velocity and clear roadmap execution. They are absorbing critical feedback and shipping experimental infrastructure (MCP services, orchestrator daemons, session snapshots).

**Moderate / Stabilizing:**
- GitHub Copilot CLI: Released v1.0.66-0 but low visible PR engineering. Stable but not aggressively experimental.
- Qwen Code: Good feature PRs (10) but CI/QA contamination and Windows instability signal process immaturity. The velocity is there, the quality gate is not.
- Claude Code: **Highest risk divergence.** Community engagement is the highest in the ecosystem, but PR velocity is the lowest among major tools (1 PR). This gap between user pain and engineering response is a leading indicator of sustained trust decay for a premium product.

**Low Signal / Early Stage:**
- Kimi Code CLI: 0 PRs, 0 releases, 2 bugs. Insufficient data to assess trajectory, but the MCP scaling limit is a structural issue that needs solving before adoption scales.

---

### 6. Trend Signals

1.  **The Token Accountability Crisis:** Unpredictable billing is the #1 existential threat to premium AI tools. Silent model upgrades, 10× rate-limit jumps, and background token waste are creating a "transactional trust" gap. Tools offering hard budgets, real-time burn rates, and explicit cost consent (Copilot's experimental budgets, CodeWhale's prompt slimming) will win the pricing trust battle.

2.  **Reliability is the New Frontier:** The market has internalized that agents break in predictable ways (hangs, false success, context loss). The demand has shifted from "what can it do?" to "can I trust it to finish without loss?" Demand for rollback, durable HITL, session recovery, and deterministic mode boundaries is overwhelming.

3.  **MCP Lifecycle is the New Differentiator:** MCP is winning as the interop standard. The battle is now about who handles auth refresh, tool count scaling, and error policy gracefully. Kimi's 200-tool crash and Codex's OAuth refresh failures are cautionary tales for everyone.

4.  **Windows/Linux Tax is Growing:** The macOS-first development model is actively limiting TAM and enterprise trust. Segfaults, OOM, terminal flicker, and sandbox loops on non-macOS platforms are no longer acceptable for professional tools. The ecosystem must treat cross-platform as a first-class requirement.

5.  **Sub-Agent Observability is a Universal Gap:** Every agent orchestration platform lacks debug-ability for sub-agents. The demand for trajectory logs, failure event feeds, and structured debugging (OpenCode SDK events, Gemini bug report context, Pi lifecycle hooks) defines the next UX frontier.

6.  **Streaming Rendering is a Specialized Discipline:** High-speed reasoning models break standard terminal assumptions. Flicker, scroll jumps, and rendering overhead are requiring investment in virtual DÖM diffing, debouncing, and syntax streaming. Polish here is a direct proxy for user-perceived quality.

7.  **CI/CD Self-Cannibalization Risk:** AI-generated PRs that miss integration tests (Qwen #5665) and CI pipeline cross-contamination (#5882) highlight a chicken-and-egg reality: if the tool generating code degrades the engineering process that tests its own output, it erodes the fundamental value proposition of adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Community Highlights Report: anthropics/skills
**Date**: 2026-06-26 | **Source**: github.com/anthropics/skills

---

## 1. Top Skills Ranking (by PR Attention)

| Rank | Skill | Functionality | Discussion Highlights | Status |
|---|---|---|---|---|
| 1 | **run_eval.py Fix (Skill-Creator Core)** [PR #1298](anthropics/skills PR #1298) | Fixes the critical "0% recall" bug that makes the description-optimization loop (`run_loop.py`, `improve_description.py`) optimize against noise. Addresses Windows stream reading and trigger detection. | The top-discussed PR. "10+ independent reproductions" confirm the universal recall bug. This fix is a prerequisite for any skill-creator workflow. | Open |
| 2 | **Document Typography** [PR #514](anthropics/skills PR #514) | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. | Solves a universal quality-of-life issue in Claude document output. Highly anticipated QoL skill. | Open |
| 3 | **ODT/ODS Creation** [PR #486](anthropics/skills PR #486) | Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods) for LibreOffice and ISO-standard workflows. | Fills a prominent format interoperability gap. Demand from open-source document users. | Open |
| 4 | **Frontend Design Clarity** [PR #210](anthropics/skills PR #210) | Revises the frontend-design skill for better actionability, internal coherence, and single-conversation executability. | Reflects community emphasis on precise, executable instructions over educational prose. | Open |
| 5 | **Skill Quality & Security Analyzer** [PR #83](anthropics/skills PR #83) | Meta-skills evaluating other Skills across structure/documentation (20%), correctness, and security dimensions. | Indicates growing demand for governance, quality control, and security auditing within the skill ecosystem. | Open |
| 6 | **SAP Predictive Analytics (RPT-1-OSS)** [PR #181](anthropics/skills PR #181) | Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data. | Shows enterprise appetite for specialized domain-model integration via Skills. | Open |
| 7 | **Testing Patterns** [PR #723](anthropics/skills PR #723) | Comprehensive Testing Trophy skill covering unit testing (AAA), React Testing Library, and E2E patterns. | Broad developer demand for standardized, opinionated testing guidance embedded in the agent. | Open |
| 8 | **Codebase Inventory Audit** [PR #147](anthropics/skills PR #147) | Systematic 10-step workflow identifying orphaned code, unused files, documentation gaps, and infrastructure bloat. | Concrete, well-structured tooling for codebase maintenance. Outputs a single source of truth (CODEBASE-STATUS.md). | Open |
| 9 | **AppDeploy** [PR #360](anthropics/skills PR #360) | Deploys and manages full-stack web apps to a public URL via AppDeploy.ai, including lifecycle management. | Extends Claude's reach into DevOps pipelines. Enables deploy-from-conversation workflows. | Open |

---

## 2. Community Demand Trends (from Issues)

- **Pipeline Reliability & Cross-Platform Parity** (*Highest Signal*): Issues #556 (12 comments), #1169 (3 comments), #1061 (3 comments) converge on the same pain point — the `skill-creator` evaluation pipeline is broken on Windows and universally returns 0% recall, rendering the optimization loop non-functional.
- **Trust & Security Boundaries**: Issue #492 (19 comments, 2 👍) is the highest-engagement issue overall, warning that community skills distributed under the `anthropic/` namespace create a dangerous trust-boundary vulnerability for privilege escalation.
- **Enterprise Sharing & Distribution**: Issue #228 (14 comments, 7 👍) demands org-wide skill libraries and direct sharing links, highlighting friction in team adoption.
- **Agent Memory & Persistence**: Issue #1329 (compact-memory proposal) and PR #154 (shodh-memory) reflect a strong trend toward long-running agent state management and context persistence.
- **Platform Expansion**: Requests to expose Skills as MCPs (Issue #16) and support AWS Bedrock (Issue #29) signal demand for Skills to operate beyond the desktop client.
- **Decluttering & Plugin Hygiene**: Issue #189 (6 comments, 9 👍) reports duplicate skills across `document-skills` and `example-skills` plugins, indicating demand for better content organization.

---

## 3. High-Potential Pending Skills

These open PRs combine active community discussion with clear utility, making them strong candidates for merge:

1. **Skill-Creator Reliability Fixes** (`#1298`, `#1099`, `#1050`, `#1323`) — These fixes unblock the entire skill development workflow. Highest priority pending changes in the repository.
2. **Testing Patterns** (`#723`) — Broad appeal across all developer types; covers a universally needed domain.
3. **Document Typography** (`#514`) — Low complexity, high impact on user-facing document quality.
4. **ODT/ODS Skill** (`#486`) — Fills a clear documented gap in format support.
5. **SAP RPT-1-OSS** (`#181`) — Targeted at a specific high-value enterprise use case with strong signals.
6. **AppDeploy** (`#360`) — Enables cloud deployment workflows directly from conversation.
7. **Shodh-Memory** (`#154`) / **Compact-Memory** (`#1329`) — Address the growing need for persistent agent state in long-running sessions.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a stable, cross-platform skill-creation foundation** (fixing the systemic `run_eval.py` recall bug and Windows compatibility) capable of reliably producing, governing, and distributing **enterprise-grade skills** spanning document engineering, testing, analytics, and persistent agent memory — all within a clearly governed trust boundary.

---

Here is the Claude Code community digest for June 26, 2026, based on the latest repository activity.

---

## Claude Code Community Digest — 2026-06-26

### 1. Today’s Highlights

Community sentiment today is dominated by model performance trust issues, unexpected billing shocks, and data integrity scares. A fresh release (v2.1.193) extends the auto-mode classifier’s reach and denial reporting, but users are loudly focused on Opus 4.8 regression, a critical memory leak, and a session persistence bug that silently dropped transcripts for days.

### 2. Releases

**v2.1.193**
- **New Setting:** `autoMode.classifyAllShell` — routes *all* Bash/PowerShell commands through the auto-mode classifier, not just arbitrary-code-execution patterns.
- **Improved Feedback:** Auto-mode denial reasons are now surfaced in the transcript, the denial toast, and the `/permissions` recent denials view.

### 3. Hot Issues

*Pick of 10 noteworthy issues from today’s activity.*

1. **[#36151 Multi-account switching in Claude Mobile app](https://github.com/anthropics/claude-code/issues/36151)** — Dominates the engagement charts with 110 comments and 380 👍. Users want to switch accounts without shared email. **Why it matters:** Reflects growing demand for multi-tenancy in Claude workflows. **Community reaction:** Overwhelmingly positive, but the conversation is split on whether this belongs in claude-code or the mobile client.

2. **[#71481 Silent default model upgrade to Opus 4.7 caused $506 in unexpected charges](https://github.com/anthropics/claude-code/issues/71481)** — User reports auto-recharges after the tool silently swapped from Sonnet to Opus. **Why it matters:** Unconsented model escalation directly drains wallets. **Community reaction:** Outrage; users are demanding granular control and explicit notification on pricing-tier changes.

3. **[#68780 Opus 4.8 reasoning degradation and speed regression](https://github.com/anthropics/claude-code/issues/68780)** — Users claim severe reasoning failures on “Max” effort. **Why it matters:** Erodes confidence in the premium model tier. **Community reaction:** Heated; some users mention legal action under EU consumer protection.

4. **[#71493 Extreme memory leak (348,766 MB/hour growth rate)](https://github.com/anthropics/claude-code/issues/71493)** — Identified via `/heapdump`. **Why it matters:** Makes long-lived sessions impractical. **Community reaction:** Alarmed; users are calling for an immediate patch.

5. **[#71496 Session transcript persistence silently disabled server-side](https://github.com/anthropics/claude-code/issues/71496)** — Transcripts stopped writing for five days; sessions vanished from `--resume`. **Why it matters:** Data loss is the highest-urgency class of bug for developer tools. **Community reaction:** Anxious; users are questioning server-side reliability.

6. **[#63687 “tool_use malformed” client errors on Opus 4.8 1M context](https://github.com/anthropics/claude-code/issues/63687) — mirrored by [#68354 stray “court” token](https://github.com/anthropics/claude-code/issues/68354)** — Tool calls emit raw XML or stray tokens instead of executing. **Why it matters:** Breaks MCP, agentic loops, and all automation. **Community reaction:** Frustrated; these reports have been building for weeks.

7. **[#71482 Safety block halts authorized mesh-agent enrollment](https://github.com/anthropics/claude-code/issues/71482)** — Auto-mode classifier misreads loopback admin tasks as security weakening. **Why it matters:** Highlights tension between safety classifiers and legitimate devops workflows. **Community reaction:** Users want explicit override lists.

8. **[#71478 VS Code extension resumes huge sessions without warning, exhausts Max usage](https://github.com/anthropics/claude-code/issues/71478)** — A resumed session triggers massive API consumption. **Why it matters:** Cost UX failure in the IDE. **Community reaction:** Users want a confirmation prompt before heavy session loads.

9. **[#29017 Conversation history lost in VSCode extension](https://github.com/anthropics/claude-code/issues/29017)** — Open since February 2026. **Why it matters:** Long-standing IDE unreliability. **Community reaction:** Steady frustration; the thread keeps gaining traction.

10. **[#61415 Bypass Permissions mode can’t be enabled on macOS](https://github.com/anthropics/claude-code/issues/61415)** — Setting reverts instantly to “Accept Edits.” **Why it matters:** Breaks an entire trust workflow. **Community reaction:** Users stuck in elevated-permission limbo.

### 4. Key PR Progress

Only one pull request was updated in the last 24 hours, making for a light PR day.

- **[#63686 Bump stale and autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)** — Merged by @caseyWebb. This process change significantly extends issue lifecycles before automated closure, giving maintainers and reporters more time to reproduce and resolve complex bugs. **Why it matters:** Provides breathing room for deep-dive debugging of the issues dominating today’s digest.

### 5. Feature Request Trends

The most popular enhancement signals from the issue tracker coalesce around four directions:

- **Multi-Account & Session Management** — #36151 leads total engagement (380 👍). Users want to switch accounts freely and manage multiple simultaneous identities.
- **Input Editing & UX Control** — #3412 (view/edit pasted text blocks, 269 👍) remains the longest-running top-voted feature request. Power users want agency over what enters the context window.
- **Developer Hooks & Middleware** — #9516 (User Interrupt Hook, 43 👍) signals demand for custom logic during agent pauses. The community wants to extend the agent’s control flow.
- **Granular Sandboxing & Permissions** — #44180 (Unix socket support for Linux/bwrap) and the uproar around auto-mode false positives indicate a need for configurable security models that don’t block legitimate admin work.

### 6. Developer Pain Points

Recurring themes from today’s activity:

- **Unexpected Cost Escalation** — The strongest theme today. Silent model upgrades (#71481) and automatic large-session resumption (#71478) are generating genuine financial trust crises.
- **Data Integrity & Session Durability** — Server-side transcript loss (#71496) and VSCode history disappearance (#29017) hit the highest note of urgency: losing your work.
- **Model Performance & Tool-Use Reliability** — Opus 4.8 regression (#68780) and tool-call malformation (#63687, #68354) undermine the tool’s autonomy promise.
- **Authentication & Authorization Friction** — Missing OAuth scopes (#71490), broken proxy startup ordering (#71177), and invalidated SSH tokens (#54179) create repetitive setup headaches.
- **Safety/UX False Positives** — The auto-mode classifier blocking mesh-agent enrollment (#71482) and Git commands (#30832) frustrates expert developers who need tighter control over their security posture.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-26

## Today's Highlights

The primary community concern this week centers on severe rate-limit and token accounting instability, with Issue #28879 reporting a 10–20× jump in per-token costs that drains the 5-hour Pro budget in just 2–3 prompts, while Issue #30002 demonstrates quota over-reporting after resets. On the infrastructure side, the massive SQLite logging volume tracked in #28224 (estimated ∼640 TB/year) has been partially mitigated in the 0.142.0 release, though several users report the fix isn't fully effective. On the development front, the roadmap is heavily investing in plugin and MCP infrastructure, highlighted by PRs adding npm marketplace support (#29375), sandbox network ingress (#29263), and a prototype treating Codex Apps as virtual HTTP MCP servers (#30000).

## Releases

- **`rust-v0.142.2`** — MCP tools now use tool search by default when supported, improving discovery. macOS authentication clients can honor system proxy, PAC, and WPAD settings with `respect_system_proxy` enabled.
- **`rust-v0.143.0-alpha.16 / .21 / .22 / .25`** — Multiple alpha releases pushing toward the v0.143.0 stable release; changelogs show active iteration on the session and agent stack.
- **`codex-zsh-v0.1.0`** — Initial release of a dedicated Zsh plugin for Codex CLI integration.

## Hot Issues

1. **[#28879 — Rate-limit cost per token jumped ∼10–20×](https://github.com/openai/codex/issues/28879)** 🔥 *304 👍, 152 comments*
   Users on the Plus plan report their 5-hour budget draining in 2-3 prompts on `gpt-5.5`. Session logs show per-token limit consumption grew an order of magnitude starting around June 16 with no change to model/plan/app. The most critical issue on the tracker right now.

2. **[#28224 — SQLite feedback logs can write ∼640 TB/year](https://github.com/openai/codex/issues/28224)** 🔥 *385 👍, 86 comments*
   A staggering disk-endurance concern. Three merged PRs (parts of 0.142.0) avoid ∼85% of the log volume according to the reporter, earning a planned closure. Remains a cautionary tale about verbose telemetry.

3. **[#9203 — Please make `/undo` back](https://github.com/openai/codex/issues/9203)** *297 👍, 51 comments*
   A long-standing feature request. Users report data loss when Codex modifies untracked files, and the removed `/undo` command provided a critical safety net. High community demand.

4. **[#30002 — Pro 5h limit burned in ∼41 minutes after reset](https://github.com/openai/codex/issues/30002)** *25 comments*
   Server-side quota accounting over-reports consumption. A Pro account used ∼1.35M tokens before hitting the limit, while the same account earlier needed ∼156M tokens for a full window. Points to a stateful accounting bug on the server side.

5. **[#25749 — Inaccessible legacy phone number blocks access](https://github.com/openai/codex/issues/25749)** *64 comments*
   Users logged in via Google OAuth with MFA can still get locked out when Codex demands verification via a defunct legacy phone number, with no recovery or replacement path. A significant auth UX failure.

6. **[#5957 — Auto-compaction causes GPT-5-Codex to lose the plot](https://github.com/openai/codex/issues/5957)** *31 comments*
   Enterprise users report that auto-compaction causes the model to forget it is mid-task, which files it edited, and stops producing useful output. Inversely correlated session quality vs. length.

7. **[#30008 — "Selected model is at capacity"](https://github.com/openai/codex/issues/30008)** *22 comments*
   Widespread reports of capacity errors hitting Pro and Pro-20 users across both the desktop app and CLI, suggesting provisioning shortfalls or hard rollover limits.

8. **[#13733 — Background process polling burns tokens](https://github.com/openai/codex/issues/13733)** *30 comments*
   Each status check on a background process (e.g. `cargo build`) triggers a full API round trip with the entire conversation history. Token cost scales linearly with history size × poll count.

9. **[#17265 — MCP OAuth tokens are not auto-refreshed](https://github.com/openai/codex/issues/17265)** *19 comments*
   Codex persists a `refresh_token` in `~/.codex/.credentials.json` but never uses it, causing MCP tool calls to fail with auth errors until manual intervention.

10. **[#29200 — Windows sandbox setup dialog on every `apply_patch`](https://github.com/openai/codex/issues/29200)** *17 comments*
    After the 26.616 update, every `apply_patch` invocation triggers a `codex-windows-sandbox-setup.exe` dialog on Windows, even on success. Prompting Windows-specific stability concerns.

## Key PR Progress

1. **[#30000 — Prototype Codex Apps as virtual HTTP MCP servers](https://github.com/openai/codex/pull/30000)**
   Establishes a `codex-apps` crate that snapshots upstream Apps and serves authenticated loopback Streamable HTTP MCP endpoints per connector. A foundational shift toward unifying Apps and the MCP ecosystem.

2. **[#29375 — Support npm marketplace plugin sources](https://github.com/openai/codex/pull/29375)**
   Fixes a deserialization issue where `{"source":"npm"}` was treated as unsupported, preventing npm-backed plugins from appearing in `plugin list --available` and `plugin add`.

3. **[#30164 — Make new-thread model defaults scope-aware](https://github.com/openai/codex/pull/30164)**
   Allows Codex to load distinct model defaults for "Work" vs. "Coding" scopes in one config bundle, selecting the right defaults on thread creation without reloading.

4. **[#30148 — Reuse MCP runtimes when selected availability changes nothing](https://github.com/openai/codex/pull/30148)**
   Previously, any ready selected-capability environment triggered a full MCP runtime swap. This PR keys reuse by whether the environment actually contributes MCP servers or connectors, avoiding unnecessary teardowns.

5. **[#30144 — Fix terminal rollout event durability](https://github.com/openai/codex/pull/30144)**
   Session code now flushes the thread store after appending `TurnComplete`/`TurnAborted` events. Fixes a latent durability gap for buffered thread stores.

6. **[#29263 — Expose sandbox ingress to host](https://github.com/openai/codex/pull/29263)**
   Adds an opt-in Unix `ingress` exec parameter carrying a TCP port, enabling callers outside the sandbox network namespace to reach sandboxed servers. Crucial for networked tool execution.

7. **[#30154 — Preserve status for evicted V2 agents](https://github.com/openai/codex/pull/30154)**
   V2 residency previously consulted only the ThreadManager for agent status. After LRU eviction, completed/errored agents became `NotFound`. This PR binds final status in `AgentMetadata` before eviction.

8. **[#28582 — Route preview traffic to plugin service](https://github.com/openai/codex/pull/28582)**
   Adds `features.plugin_service_preview` flag to route traffic through Codex's new plugin service stack, shared with the employee-only preview for Codex Apps.

9. **[#30156 — Fall back when remote filesystem walk is unavailable](https://github.com/openai/codex/pull/30156)**
   Provides graceful degradation when a newer Codex client connects to an exec-server that doesn't expose the optimized `fs/walk` RPC, preventing "method not found" hard failures.

10. **[#29909 — Allow CCA image generation and web search extensions](https://github.com/openai/codex/pull/29909)**
    Extends the actor-authorized provider shape used by CCA to enable standalone image generation and web search, while preserving existing flows for older models.

## Feature Request Trends

- **Session Recovery / Safety Net (`/undo`)** — Issue #9203 (297 👍) remains the top enhancement request. Users are demanding a robust undo or session rollback mechanism, especially for untracked local file changes made by the model.
- **Plugin & MCP Ecosystem Growth** — The volumes of PRs around npm plugin sourcing (#29375), virtual MCP apps (#30000), and App identity in MCP context (#29934) indicate the community and team are pushing toward a fully extensible tool platform. App/MCP unification is the clear architectural direction.
- **Scope-Aware Configuration** — PRs #30164 and #29683 are pushing for distinct model/reasoning defaults per use case (Coding vs. Work), surfacing that developers want smarter defaults that don't require manual toggling.
- **Binary File Handling** — Issue #4867 (27 comments) asks for binary file support in PR creation. As Codex is applied to more complex codebases (assets, compiled artifacts), this is becoming a practical blocker.

## Developer Pain Points

- **Unpredictable Token Accounting** — The cluster of rate-limit bugs (#28879, #30002, #13733) paints a picture of a quota system that is unreliable by an order of magnitude. This is eroding trust in the Pro billing model and making cost budgeting impossible.
- **Aggressive Background Disk Usage** — The SQLite logging saga (#28224 fix partially shipped, but #29532 & #29814 persist) raises concerns about SSD endurance and hidden system resource drain, even when users are idle.
- **Windows Desktop Stability** — Windows-specific crashes and dialogs (#29200, #27828, #29544, #29782) are frequent and severe, from GPU crashes on Cloudflare Turnstile to blocking sandbox setup popups. The overall quality of the Windows desktop experience appears to lag significantly behind macOS.
- **Auth Flow Dead Ends** — Stale MCP tokens (#17265) and inaccessible phone verification (#25749) create hard blockers. Any auth path that requires user intervention outside the tool's lifecycle is a fragility point for CI/automation.
- **Context Loss in Long Sessions** — Auto-compaction actively sabotaging long-running tasks (#5957) is a significant problem for Enterprise users doing complex refactoring or multi-step builds. Losing the model's awareness of its own edits is a critical bug.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — 2026-06-26**

---

### 1. Today's Highlights
Today's activity focused heavily on shoring up the CI/CD pipeline for release quality and patching critical agent reliability bugs. The release of `v0.50.0-preview.1` introduces a Tool Registry Dependency Injection refactor, while several high-priority issues surrounding agent hangs, false "GOAL" success from sub-agents, and OAuth token security drew significant attention. Community momentum continues around AST-aware codebase tooling and the need for deterministic secret redaction in the Auto Memory system.

---

### 2. Releases
Three versions were published today:
- **v0.51.0-nightly.20260626** — Hardens the release CI to prevent bad NPM releases and promote job crashes.
- **v0.50.0-preview.1** — Further release verification hardening and a new `Feat/tool registry di` for internal architecture improvements.
- **v0.49.0** — Stable release with dependabot cooldown period configuration and changelog automation.

---

### 3. Hot Issues

1.  **#21409 [P1] Generalist Agent Hangs** — The agent hangs indefinitely on simple tasks like folder creation. Users report that explicitly disabling sub-agents works around the issue. (👍 8)
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21409)

2.  **#25166 [P1] Shell Command Hangs ("Awaiting input")** — A recurring blocking issue where shell commands complete but the tool remains stuck in an "Awaiting user input" state, breaking the core terminal workflow. (👍 3)
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/25166)

3.  **#22323 [P1] Subagent False GOAL Success** — The `codebase_investigator` subagent reports `status: "success"` even when it hits the `MAX_TURNS` limit before performing any analysis, masking critical failures.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/22323)

4.  **#21763 [P1] Bugreport Lacks Subagent Context** — The `/bug` command only captures the main session without subagent trajectories, severely limiting debugging capability.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21763)

5.  **#21983 [P1] Browser Subagent Fails on Wayland** — The browser agent cannot launch or operate correctly on Wayland display servers, blocking Linux users.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21983)

6.  **#24353 [P1] Component Level Evaluations** — An EPIC tracking the expansion of behavioral evals to cover 6 Gemini model variants, aiming to prevent regressions in agent behavior.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/24353)

7.  **#21968 [P2] Skills and Sub-agents Ignored** — The model rarely autonomously triggers custom skills or sub-agents, even when tasks match their descriptions, undermining agent extensibility.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/21968)

8.  **#19873 [P2] Leverage Bash Affinity via Zero-Dependency Sandboxing** — A proposal to deeply integrate the model's native POSIX tool chaining within a secure sandbox, balancing safety with execution capability. (👍 1)
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/19873)

9.  **#26525 [P2] Auto Memory Redaction & Logging** — Highlights that secrets sent for redaction are already in model context before filtering, and the service may log sensitive skill content. Requests deterministic pre-context redaction.
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/26525)

10. **#22745 [P2] AST-Aware File Tools** — An EPIC investigating whether AST-aware method reading and codebase mapping can reduce token usage, noise, and tool call turns compared to line-based tools. (👍 1)
    [Issue Link](https://github.com/google-gemini/gemini-cli/issues/22745)

---

### 4. Key PR Progress

1.  **#28103** — **OAuth Keep-Alive Fix**. Prevents socket reuse that causes token exchange failures on Node.js versions shipping the CVE-2026-48931 fix (24.17.0, 22.23.0, 26.3.0).
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/28103)

2.  **#27850** — **MCP Image MIME Sniffing**. Corrects MCP image payloads with wrong MIME types by sniffing the actual bytes (PNG, JPEG, GIF, WebP). Fixes #27731. (Closed)
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27850)

3.  **#27845** — **Folder Trust Before Auth**. Re-orders startup to prompt for workspace trust before authentication, ensuring local configs and secrets are handled correctly. (Closed)
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27845)

4.  **#28013** — **Prompt $ Pattern Corruption Fix**. Fixes a critical bug where `$`-prefixed patterns in skill descriptions could corrupt prompt strings via `String.prototype.replace`.
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/28013)

5.  **#27971** — **Thought Leakage Fix**. Strips model scratchpad/thoughts from scrubbed history turns to prevent infinite loops and context confusion.
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27971)

6.  **#27979** — **MCP Untrusted Output Wrapping**. Wraps `read_mcp_resource` output with `wrapUntrusted()` for security consistency with MCP tools. Resolves #27983.
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27979)

7.  **#27848** — **`gemini models` Command**. Adds a long-requested CLI command to list available models, context windows, and tiers with JSON output support. (Closed)
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27848)

8.  **#28149** — **Skill .gitignore/.geminiignore Respect**. Ensures skill resource listings respect ignore files instead of sharing irrelevant project files with the model.
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/28149)

9.  **#27461** — **PTY Resize EBADF Suppression**. Backports an upstream `node-pty` fix to prevent crashes when resizing exiting PTY sessions, exacerbated by recent UI layout changes. (Closed)
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/27461)

10. **#28145** — **Vertex Endpoint Routing**. Routes traffic to official Representative Endpoints (REP) for Vertex AI multi-region configurations (`us`, `eu`). (Closed)
    [PR Link](https://github.com/google-gemini/gemini-cli/pull/28145)

---

### 5. Feature Request Trends

- **Agentic Observability & Control:** Strong demand for transparency into subagent operations (trajectories in bug reports, shareable via `/chat share`) and stricter controls over agent permissions and tool scoping.
- **Structured Codebase Intelligence:** Multiple requests converge on AST-aware tooling for reading method bounds and mapping codebases to reduce token waste and improve edit precision.
- **Security-First Execution Layer:** A growing push for sandboxing native bash execution, pre-context secret redaction in Auto Memory, and hardened MCPI/O boundaries against malformed server data.
- **Tool Registry Flexibility:** The `Feat/tool registry di` in the latest preview release suggests the team is investing in modular tool loading, likely to address issues with tool count limits and dynamic tool scoping.

---

### 6. Developer Pain Points

- **Pervasive Hangs:** The most frequent blocker involves the agent freezing on shell commands or during sub-agent delegation, requiring manual cancellation.
- **False Positive Reporting:** Sub-agents reporting "GOAL" success while hitting turn limits or crashing erodes trust in the tool's diagnostic output.
- **Orchestration Gaps:** Custom skills and sub-agents are rarely used autonomously by the model, rendering user investment in them largely ineffective without explicit prompting.
- **Destructive Tendencies:** The agent overuses `--force` flags, `git reset`, and generates temp scripts in random directories, creating cleanup overhead and risk for version-controlled workspaces.
- **Configuration Ignorance:** Settings like `maxTurns` for sub-agents are silently ignored, symlinked agent files won't load, and `settings.json` overrides are frequently missed by sub-agent systems like the browser agent.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – June 26, 2026**

---

### 1. Today's Highlights

- **v1.0.66-0 launches** with highly requested MCP lifecycle toggles and experimental response budget controls, directly responding to long-standing community feedback [#2956](https://github.com/github/copilot-cli/issues/2956) and [#3564](https://github.com/github/copilot-cli/issues/3564).  
- **Session stability is the week's hottest cluster**: users report resumed sessions losing model access (#3596), autopilot mode breaking after a single request (#3933), and sessions disappearing from the resume list (#3931).  
- **Hotfixes are flowing** for recent regressions: closed issues include Linux AppImage library leaks (#3925), mouse tracking corruption on exit (#3876), and an observability gap in `/tasks` (#3937).

---

### 2. Releases

**v1.0.66-0**

- **MCP Toggle:** Enable/disable MCP servers directly from the interactive `/mcp show` menu instead of requiring manual commands.
- **Budget Controls:** New experimental "response budget" settings added to the CLI settings menu (likely token/spend limits).
- **Observability:** Managed settings can now push OpenTelemetry export configuration to local installs.
- **Resilience:** MCP tools running on OAuth-authenticated remote servers now recover automatically after a mid-session token refresh.

---

### 3. Hot Issues

1. **[#3596 – Error loading model list: Not authenticated (11 👍)](https://github.com/github/copilot-cli/issues/3596)**  
   *Why it matters:* Resuming a session breaks the `/model` command entirely, blocking model switching and forcing full restarts. A core session regression.

2. **[#3933 – Drops out of autopilot after each request](https://github.com/github/copilot-cli/issues/3933)**  
   *Why it matters:* Persistent autopilot mode is a key differentiator. The regression forces developers to re-enable autopilot after every single prompt, breaking multi-step agentic workflows.

3. **[#700 – Provide a way to list all models (14 comments)](https://github.com/github/copilot-cli/issues/700)**  
   *Why it matters:* The most commented open feature request. Users want a `--list-models` command showing model names, capabilities, and multipliers for informed cost/quality trade-offs.

4. **[#2643 – Silent command rewrite blocked by confirmation dialog (12 comments)](https://github.com/github/copilot-cli/issues/2643)**  
   *Why it matters:* Plugin developers expected `preToolUse` with `permissionDecision: allow` to enable silent automation. An unavoidable confirmation dialog kills advanced scripting and skill workflows.

5. **[#3636 – Voice mode blocked on corporate VPN (5 👍)](https://github.com/github/copilot-cli/issues/3636)**  
   *Why it matters:* Voice mode cannot fetch its catalog on locked-down networks, rendering the feature entirely unusable for a wide segment of enterprise users.

6. **[#3935 – VS Code Terminal ignores user theme (new)](https://github.com/github/copilot-cli/issues/3935)**  
   *Why it matters:* Since v1.0.64, the CLI forces a light theme inside VS Code terminals regardless of user settings—a highly visible accessibility and UX regression.

7. **[#3501 – Scroll bar makes text unalign on Windows (9 👍)](https://github.com/github/copilot-cli/issues/3501)**  
   *Why it matters:* The new vertical scroll bar in Windows Terminal and Console Host causes persistent text misalignment, a distracting visual bug on a primary platform.

8. **[#3934 – MCP server 'blocked by policy' (new)](https://github.com/github/copilot-cli/issues/3934)**  
   *Why it matters:* Correct MCP configs working in VS Code/IntelliJ are blocked in the CLI with an opaque error. Enterprise policy enforcement needs transparent debugging.

9. **[#3909 – Enterprise server-managed settings for local CLI](https://github.com/github/copilot-cli/issues/3909)**  
   *Why it matters:* Org admins cannot centrally push config (env vars, policies) to local CLI installs—a critical gap that blocks wide enterprise rollout.

10. **[#3931 – Recent sessions missing from resume list (new)](https://github.com/github/copilot-cli/issues/3931)**  
    *Why it matters:* Users are losing entire conversation histories. Combined with #3596, session management is the biggest pain point for daily drivers.

---

### 4. Pull Requests in Flight

Only one pull request saw activity today, suggesting the team is focused on stabilization patches for v1.0.66-0.

- **[#3928 – Add .gitignore and settings configuration](https://github.com/github/copilot-cli/pull/3928)**  
  A routine project hygiene PR adding standard `.gitignore` and settings config templates.

---

### 5. Feature Request Trends

- **Model Discovery & Quotas:** Users increasingly demand CLI-native model listing ([#700](https://github.com/github/copilot-cli/issues/700)) and monthly AIC usage visibility ([#3932](https://github.com/github/copilot-cli/issues/3932)).
- **MCP UX Maturation:** The community wants MCP to feel like a core platform, not an afterthought: async read-only commands ([#3829](https://github.com/github/copilot-cli/issues/3829)), Azure DevOps integration ([#3794](https://github.com/github/copilot-cli/issues/3794)), and respecting server "instructions" ([#1579](https://github.com/github/copilot-cli/issues/1579)).
- **Enterprise Governance:** Strong push for server-pushed managed settings ([#3909](https://github.com/github/copilot-cli/issues/3909)) and clear MCP policy error messaging ([#3934](https://github.com/github/copilot-cli/issues/3934)).
- **Theming & Accessibility:** Calls for fine-grained per-element theming ([#2123](https://github.com/github/copilot-cli/issues/2123)) are getting louder following recent visual regressions.

---

### 6. Developer Pain Points

- **Session / Auth Instability:** The loudest cluster of bugs. Resuming sessions loses model auth (#3596, #3680), sessions vanish from the list (#3931), and autopilot disengages every turn (#3933).  
- **Network & Environment Friction:** Corporate VPNs block voice mode (#3636), WSL2 users can't use `/copy` (#3534), and Linux AppImages leak library paths (#3925, closed).  
- **UI Regressions:** Windows scroll bar alignment (#3501) and forced light themes in VS Code (#3935) are breaking daily developer comfort at high visibility.  
- **Plugin/Skill Fragility:** Developers hit walls with silent hook execution (#2643), lost migrated Claude Code skills on update (#3938), and confusing `argument-hint` validation errors (#3929).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for **2026-06-26**, based strictly on the provided GitHub data.

---

## Kimi Code CLI Community Digest — 2026-06-26

### 1. Today’s Highlights
The repository had a quiet day with **no new releases or pull requests**. All attention is focused on two critical bug reports filed today against the current `v0.19.2` release that highlight major pain points in stability and scalability: a violent Linux TUI flickering when using the `K2.7 Code thinking` model, and a hard crash when an MCP server exposes more than 200 tools.

### 2. Releases
**None.** The latest stable build remains `v0.19.2`. No release artifacts or changelogs were published in the last 24 hours.

### 3. Hot Issues
*Exactly two issues were updated in the last 24 hours. Despite the low volume, both are high-signal defects.*

**1. Issue #2475: [bug] MCP tools crash with large tool sets**
- **Author:** [ptyll](https://github.com/ptyll)
- **Link:** [MoonshotAI/kimi-cli Issue #2475](https://github.com/MoonshotAI/kimi-cli/issues/2475)
- **Summary:** An MCP server providing 212 tools with descriptions causes the CLI to fail entirely.
- **Why it matters:** This reveals a hard ceiling in the MCP adapter’s initialization logic. As agent tooling matures, power users frequently operate servers with hundreds of tools. A crash at ~200 tools is a critical scalability blocker that limits the practicality of Kimi’s MCP integration for enterprise workflows.
- **Community Reaction:** New (0 comments, 0 upvotes). Expected to gather significant traction if replicated.

**2. Issue #2474: [bug] Complete UI re-render loop / shaking on Linux**
- **Author:** [yudichimiantiao](https://github.com/yudichimiantiao)
- **Link:** [MoonshotAI/kimi-cli Issue #2474](https://github.com/MoonshotAI/kimi-cli/issues/2474)
- **Summary:** The entire terminal conversation view constantly flickers and resets from scratch when using the `K2.7 Code thinking` model on Linux.
- **Why it matters:** Terminal UI stability is a basic usability requirement. The specificity to the “Code thinking” mode suggests the TUI framework is failing to handle high-throughput streaming reasoning tokens, likely due to a missing virtual DOM diffing or debouncing mechanism. This directly impacts the flagship selling feature of the CLI.
- **Community Reaction:** New (0 comments, 0 upvotes). High potential for disruption across the Linux developer base.

### 4. Key PR Progress
**None.** No pull requests were created, opened, or updated in the last 24 hours. Development velocity appears focused on internal tracking or stabilization.

### 5. Feature Request Trends
No explicit feature requests were opened today, but the bugs strongly imply the following community demands:
- **Fault-Tolerant MCP Registration:** A clear need for MCP tool loading to handle very large manifests (200+ tools) without choking. Users implicitly request a soft-warning or lazy-loading pattern instead of a hard crash.
- **Stable TUI During Streaming:** Users need virtualized or diff-based terminal rendering that can handle rapid, long-thinking model outputs without page-ripping flicker.

### 6. Developer Pain Points
- **MCP Scaling Ceiling:** The 200-tool hard failure is an immediate dealbreaker for advanced agent builders. It erodes trust in the MCP protocol implementation for serious production use.
- **Linux TUI Instability:** The most prominent friction point for the core developer audience (Linux users) is the broken rendering loop. Making a “Code thinking” feature that breaks the terminal makes the tool feel unpolished at the point of highest value.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: June 26, 2026

## 1. Today's Highlights

- **v1.17.11 launched** with session snapshots for message-level rollback, directly tackling long-standing state management concerns.
- **Windows stability crisis deepens:** the v1.17.10 Bun segfault (#33742) forces widespread downgrades, prompting a strategic CI switch to Bun canary builds.
- **Long-standing UX victory:** the `tui.copy_on_select` setting finally ships (PR #4793), resolving the most-voted configuration request. The `sdk-next` ecosystem also advances rapidly with active session exposure and MCP service scaffolding.

## 2. Releases

**v1.17.11**
- **Core:** Session snapshots and revert controls allow granular rollback to earlier messages, including associated file changes.
- **Bugfix:** MCP OAuth URL is now always printed to stdout, ensuring manual sign-in works when the browser auto-open flow fails.
- **Desktop:** Chrome-styled... *[data truncated in source]*

---

## 3. Hot Issues

*(10 noteworthy issues from the past 24 hours)*

1. **[#33742] Windows Segfault on v1.17.10**
   *45 comments, 42 👍*
   A native Bun segmentation fault makes v1.17.10 completely unusable on Windows. v1.17.9 is confirmed stable under identical configurations. The leading community concern.
   [Issue 33742](https://github.com/anomalyco/opencode/issues/33742)

2. **[#30360] Agent Picker Missing in v2 Layout**
   *3 comments, 5 👍*
   The build/plan agent picker is hidden when "New layout and designs" is enabled. Gated incorrectly in `prompt-input.tsx`. A fix is submitted in PR #30352.
   [Issue 30360](https://github.com/anomalyco/opencode/issues/30360)

3. **[#32821] GLM-5.2 Content Validation Error**
   *8 comments*
   OpenCode serializes message content as a `[{text:"..."}]` array, which the GLM-5.2 API rejects with a 400 error. The model expects a plain string, exposing provider-specific formatting gaps.
   [Issue 32821](https://github.com/anomalyco/opencode/issues/32821)

4. **[#28656] Blank Code Blocks in CentOS 7 TUI**
   *4 comments*
   All LLM-output code blocks render as invisible blank space. Users must copy/paste into external editors to view code. Likely a terminal detection or renderer edge case.
   [Issue 28656](https://github.com/anomalyco/opencode/issues/28656)

5. **[#33866] Old Skills Config Syntax Breaks Loading**
   *3 comments*
   The build agent incorrectly writes the legacy array-based `skills` config syntax instead of the current object-based format, causing silent load failures.
   [Issue 33866](https://github.com/anomalyco/opencode/issues/33866)

6. **[#33815] Severe Slowdown on v1.17.10**
   *3 comments*
   Post-upgrade, responses take "years" and return "Internal server error retrying." Makes the update effectively broken, increasing pressure on the v1.17.11 rollout.
   [Issue 33815](https://github.com/anomalyco/opencode/issues/33815)

7. **[#33903] Effect.tryPromise Startup Crash on Windows**
   *2 comments*
   A secondary crash pattern on Windows that persists even after downgrading from v1.17.10. PR #33996 directly addresses this by preserving native init errors instead of using a generic fallback.
   [Issue 33903](https://github.com/anomalyco/opencode/issues/33903)

8. **[#13102] Tool Execution Aborted on Truncated Call**
   *5 comments*
   Agentic workflows break silently when a tool call is issued with empty or truncated input. The generic "Tool aborted" error provides no diagnostic path, causing significant downstream failures.
   [Issue 13102](https://github.com/anomalyco/opencode/issues/13102)

9. **[#34004] Anthropic Custom Provider UX Gap**
   *1 comment (opened today)*
   Despite backend support for an `Anthropic-compatible` provider type (#11692), configuring it on Desktop requires undocumented manual `opencode.jsonc` edits rather than UI-based setup.
   [Issue 34004](https://github.com/anomalyco/opencode/issues/34004)

10. **[#34003] sdk-next Needs Durable Failure Events**
    *1 comment (opened today)*
    Embedded SDK hosts cannot surface terminal diagnostic events when a session drain fails, leaving the host stuck in a "Working" state indefinitely. A critical lifecycle gap.
    [Issue 34003](https://github.com/anomalyco/opencode/issues/34003)

---

## 4. Key PR Progress

*(10 impactful pull requests updated in the last 24 hours)*

1. **[#30352] Show build/plan agent picker in v2 layout** (@xohmai)
   Fixes the gating in `prompt-input.tsx` so `settings.general.showCustomAgents()` is respected in the new layout.
   [PR 30352](https://github.com/anomalyco/opencode/pull/30352)

2. **[#29281] Fix `process.exit()` killing parent terminal on Windows** (@LifeJiggy)
   Prevents `ExitProcess()` from sending `CTRL_CLOSE_EVENT` to the parent PowerShell/cmd console group on close.
   [PR 29281](https://github.com/anomalyco/opencode/pull/29281)

3. **[#33892] Bound session diff summary payload** (@ponponon)
   Caps diffs before generation and persistence to prevent pathological workspace bloat from corrupting session summaries. Closes #33106.
   [PR 33892](https://github.com/anomalyco/opencode/pull/33892)

4. **[#33996] Preserve TUI renderer initialization errors** (@Hona)
   Replaces a generic `Effect.tryPromise` wrapper with the underlying OpenTUI error, enabling proper debugging of startup crashes. Addresses #33903 and #32706.
   [PR 33996](https://github.com/anomalyco/opencode/pull/33996)

5. **[#33822] Use Bun canary for beta channel** (@Hona)
   Strategic CI change to leverage the Rust-rewritten Bun canary builds, directly mitigating the Windows segfault issue (#33742).
   [PR 33822](https://github.com/anomalyco/opencode/pull/33822)

6. **[#33988] Scaffold core MCP Service** (@opencode-agent[bot])
   Introduces a Location-scoped `MCP.Service` with layered V2 config, timeout handling, and full connect/disconnect lifecycle wiring via child scopes.
   [PR 33988](https://github.com/anomalyco/opencode/pull/33988)

7. **[#4793] Add `tui.copy_on_select` setting** (@ariane-emory)
   Resolves the heavily upvoted #4751 (24 comments, 18 👍). Adds a config boolean to disable clipboard pollution on text selection. A major UX quality-of-life improvement.
   [PR 4793](https://github.com/anomalyco/opencode/pull/4793)

8. **[#33994] Auto-approve permissions per server** (@opencode-agent[bot])
   Moves Desktop auto-approval from session-scoped to server-scoped granularity, significantly reducing repetitive approval prompts.
   [PR 33994](https://github.com/anomalyco/opencode/pull/33994)

9. **[#34000] Enable mentioning of hidden files** (@iputuanggak)
   Adds `hidden: true` to file search configuration, fixing the inability to `@`-mention dot-prefixed files.
   [PR 34000](https://github.com/anomalyco/opencode/pull/34000)

10. **[#33991] Expose active sessions via SDK** (@kitlangton)
    Adds `client.sessions.active()` returning `{ [sessionID]: { type: "running" } }` for TUI bootstrap and external monitor coordination.
    [PR 33991](https://github.com/anomalyco/opencode/pull/33991)

---

## 5. Feature Request Trends

- **Compaction Configuration (Highest upvote cluster):** Configurable thresholds (#11314, #11930) and silent/background compaction (#13033) represent the most persistent gap. Users want granular control over when and how compaction triggers, and the ability to stream summaries invisibly.
- **Provider Parity & Flexibility:** Strong demand for feature matching between direct-auth and GitHub Copilot models (#12504), robust handling of non-standard API payload formats (GLM arrays #32821, Vertex Gemini #31879), and first-class UI for custom provider types (#34004).
- **Embedded SDK Lifecycle (sdk-next):** The embedded community is pushing hard for production-grade lifecycle events: durable failure reporting (#34003), session metadata support (#33964), and host config injection (#33963).
- **Multi-Agent Observability:** A growing UX cluster around sub-agents—sidebar panels (#12463), agent type/session ID in task tool calls (#16287), and timestamps in session pickers (#16341)—signals a need for better orchestration debugging.

---

## 6. Developer Pain Points

- **Windows Runtime Instability (Crisis Level):** The v1.17.10 Bun segfault (#33742) and secondary `Effect.tryPromise` crashes (#33903) make Windows the most fragile platform. The CI switch to Bun canary (#33822) is an explicit admission that upstream runtime issues are blocking stability.
- **Configuration Schema Migration Fatigue:** Silent failures from syntax changes (`skills`: array → object in #33866) and undocumented provider config fields (#34004) force users into trial-and-error debugging, eroding trust in config stability.
- **Terminal Compatibility Tax:** Low-level rendering bugs (CentOS blank blocks #28656, iTerm2 mouse reporting conflicts #24046) and process propagation issues (parent shell termination on Windows close #29281) create a steady background drain on developer trust across platforms.
- **Agent Workflow Blind Spots:** Broken tool execution on truncated calls (#13102) and no durable failure reporting in the embedded SDK (#34003) leave autonomous agent loops without proper error boundaries or diagnostic paths.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-26

## Today's Highlights
Today's activity centers on critical reliability patches for the coding agent's RPC client (removing the hardcoded 60-second timeout) and continued community friction with TUI viewport instability during streaming and rendering. The experimental `pi orchestrator` PR signals a push toward multi-instance management, while a flurry of requests for session introspection APIs and single-binary packaging reflects a maturing platform ecosystem.

## Releases
No new releases published in the last 24 hours.

## Hot Issues
*Top 10 noteworthy issues by community engagement and impact.*

1.  **[#4945](https://github.com/earendil-works/pi/issues/4945) – OpenAI Codex Connection Reliability Issues *[inprogress]***  
    The highest-engagement open thread. The interactive TUI hangs on "Working..." with no streaming, tool calls, or error recovery. Only Escape works, recording an aborted turn.  
    *Reaction:* 71 comments, 30 👍 — indicates a critical, widespread UX failure with the default provider integration.

2.  **[#5825](https://github.com/earendil-works/pi/issues/5825) – Streaming markdown forces scroll to bottom *[bug]***  
    Fast streaming output forces constant viewport jumps to the bottom, specifically triggered by the `clear on shrink` setting, making reading nearly impossible.  
    *Reaction:* 31 comments.

3.  **[#6050](https://github.com/earendil-works/pi/issues/6050) – TUI full redraw clears terminal scrollback *[untriaged]***  
    Destructive full redraws during active rendering cause the terminal scrollbar to jump to the start of the chat, disrupting focus and losing visual context.  
    *Reaction:* 10 comments.

4.  **[#5595](https://github.com/earendil-works/pi/issues/5595) – maxTokens not passing through *[to-discuss]***  
    Blocks usage of reasoning models like DeepSeek v4pro on Together.ai by failing to respect user output token limits, causing premature truncation.  
    *Reaction:* 8 comments, 2 👍.

5.  **[#5671](https://github.com/earendil-works/pi/issues/5671) – `~/.pi` and `cwd/.pi` overlap *[bug]***  
    Identified by mitsuhiko. The shared `.pi` namespace for global and project settings creates scoping ambiguity and potential conflicts in `$HOME`.  
    *Reaction:* 6 comments, 5 👍.

6.  **[#4290](https://github.com/earendil-works/pi/issues/4290) – Messages aborted for length treated as regular stops *[bug]***  
    The TUI fails to visually distinguish between a complete response and a cut-off model ("length finish"), making turn truncation invisible to the user.  
    *Reaction:* 6 comments, 1 👍.

7.  **[#5886](https://github.com/earendil-works/pi/issues/5886) – AgentSession settlement/continuation lifecycle bugs *[pkg:agent, pkg:coding-agent]***  
    Meta-issue by mitsuhiko documenting a class of deep bugs where post-run logic tries to continue an agent from an invalid assistant transcript tail.  
    *Reaction:* 3 comments, 2 👍.

8.  **[#6002](https://github.com/earendil-works/pi/issues/6002) – `SessionManager.open()` silently truncates files *[bug]***  
    High-severity data loss bug. Pointing the session CLI at a non-session file (e.g. NDJSON) silently destroys it, replacing it with a small session header.  
    *Reaction:* 4 comments.

9.  **[#6060](https://github.com/earendil-works/pi/issues/6060) – TypeError in footer rendering token stats *[untriaged]***  
    Uncaught exception crashes the TUI entirely when rendering context usage stats for sessions with tool-call-only assistant messages.  
    *Reaction:* 4 comments.

10. **[#5901](https://github.com/earendil-works/pi/issues/5901) – Durable HITL tool-call interrupts *[no-action]***  
    Highlights headless/enterprise use cases lacking proper human-in-the-loop approval for tool calls, a gap compared to LangGraph/LangChain.  
    *Reaction:* 3 comments.

## Key PR Progress
*Top 10 impactful pull requests updated in the last 24 hours.*

1.  **[#6087](https://github.com/earendil-works/pi/pull/6087) – fix(coding-agent): remove hardcoded RPC wait timeout *[Closed]***  
    The `RpcClient` had a hardcoded 60s cap in `waitForIdle()` and `collectEvents()`, causing long-running tool sessions to fail silently. Makes timeout configurable and adds exit cleanup.

2.  **[#6084](https://github.com/earendil-works/pi/pull/6084) – fix(tui): preserve custom widget render order on background refreshes *[Closed]***  
    Extension widgets were reordering during high-frequency TUI refreshes due to `Map.delete/set` cycles. Fixes flickering and layout jumps in complex extension-built UIs.

3.  **[#6081](https://github.com/earendil-works/pi/pull/6081) – feat: add #RRGGBBAA alpha support for theme colors *[Closed]***  
    Extends the theme system for 8-digit hex colors. Alpha values are pre-blended with background colors at load time for terminal ANSI compatibility.

4.  **[#6078](https://github.com/earendil-works/pi/pull/6078) – feat(coding-agent): add get_entries and get_tree RPC commands *[Open]***  
    Exposes read-only RPC endpoints mirroring `SessionManager` internals with cursor-based pagination. Unlocks deep programmatic session introspection for external tools and UIs.

5.  **[#6064](https://github.com/earendil-works/pi/pull/6064) – feat(experimental): pi orchestrator *[Open]***  
    Major architectural PR adding a Unix-socket-based daemon for lifecycle management of multiple Pi instances (start, list, stop). Signals multi-instance orchestration roadmap.

6.  **[#6074](https://github.com/earendil-works/pi/pull/6074) – fix(coding-agent): avoid pre-prompt compaction continue *[Open]***  
    Prevents premature compaction of the pre-prompt context that could strip critical system instructions during long-running, context-bound sessions.

7.  **[#6067](https://github.com/earendil-works/pi/pull/6067) – fix(prompt): add overeager scope-discipline rule *[Closed]***  
    Single-line system prompt addition (inspired by Aider's `overeager_prompt`) instructing the agent to stay strictly within the scope of the user's request.

8.  **[#5832](https://github.com/earendil-works/pi/pull/5832) – fix(ai): surface provider HTTP error body *[Open]***  
    For providers behind a gateway/proxy, non-2xx responses with unparseable bodies now surface the raw HTTP error text instead of generic SDK messages.

9.  **[#5270](https://github.com/earendil-works/pi/pull/5270) – Ephemeral session model and thinking level selection *[Closed]***  
    Defaults `/model` and `/think` changes to session-only mode unless `{ persist: true }` is passed. Stops in-session configuration from leaking into global defaults.

10. **[#6063](https://github.com/earendil-works/pi/pull/6063) – Extension stats & benchmark cleanup *[Closed]***  
    Fixes OSC garbage printed to the terminal after running benchmark/timing diagnostics, improving the developer experience for performance tuning.

## Feature Request Trends
- **Programmatic Session Control:** A strong, repeated signal for deep session API access. Developers want `get_entries`/`get_tree` RPC endpoints ([#5810](https://github.com/earendil-works/pi/issues/5810), [#6078](https://github.com/earendil-works/pi/pull/6078)), deterministic in-memory session IDs ([#6070](https://github.com/earendil-works/pi/issues/6070)), and durable HITL middleware for tool calls ([#5901](https://github.com/earendil-works/pi/issues/5901)).
- **Terminal UI Polish & Customization:** The community is demanding robust viewport stability (scroll, redraw, tmux jumps) while simultaneously requesting deeper customization like alpha color support ([#6081](https://github.com/earendil-works/pi/pull/6081)) and shell autocompletion for Pi commands ([#6086](https://github.com/earendil-works/pi/issues/6086)).
- **Deployment & Infrastructure Maturation:** Requests for single-binary packaging ([#6065](https://github.com/earendil-works/pi/issues/6065)), daemon-based orchestration ([#6064](https://github.com/earendil-works/pi/pull/6064)), and provider payload transforms ([#6089](https://github.com/earendil-works/pi/issues/6089)) indicate a shift from a single-user TUI tool toward a robust, deployable platform.

## Developer Pain Points
- **Connectivity Instability:** The "Working..." hang with OpenAI-shaped providers ([#4945](https://github.com/earendil-works/pi/issues/4945)) combined with a total lack of feedback for invisible "length finish" truncations ([#4290](https://github.com/earendil-works/pi/issues/4290)) is the most painful recurring pattern.
- **Terminal Viewport Instability:** Viewport jumping during streaming, rendering, and tool output expands across tmux and non-tmux sessions ([#5825](https://github.com/earendil-works/pi/issues/5825), [#6050](https://github.com/earendil-works/pi/issues/6050), [#6073](https://github.com/earendil-works/pi/issues/6073)). This is the top friction point for deep focus workflows.
- **Silent Data Loss and Unexpected Crashes:** Uncaught TypeErrors crashing the TUI ([#6060](https://github.com/earendil-works/pi/issues/6060)), silent file truncation by `SessionManager.open()` ([#6002](https://github.com/earendil-works/pi/issues/6002)), and extensions breaking on update ([#5989](https://github.com/earendil-works/pi/issues/5989)) erode confidence in stability.
- **Configuration and Scoping Fragility:** Ambiguity between global and project configs ([#5671](https://github.com/earendil-works/pi/issues/5671)), global setting leaks from in-session changes ([#5270](https://github.com/earendil-works/pi/issues/5270)), and hardcoded internal timeouts ([#6088](https://github.com/earendil-works/pi/issues/6088)) create a high configuration tax.
- **Cross-Platform and Headless Gaps:** Issues with Git Bash detection on Windows ([#5103](https://github.com/earendil-works/pi/issues/5103)), Node version dependencies ([#6065](https://github.com/earendil-works/pi/issues/6065)), and lack of durable HITL ([#5901](https://github.com/earendil-works/pi/issues/5901)) highlight friction for non-macOS users and enterprise integrations.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the **Qwen Code Community Digest** for **2026-06-26**, based on the latest GitHub activity from `QwenLM/qwen-code`.

---

## Qwen Code Community Digest – 2026-06-26

### 1. Today's Highlights
The most critical signal today is a **major Windows stability regression** ([Issue #5873](QwenLM/qwen-code Issue #5873)) where every tool call spawns a non-closing PowerShell process, leading to an OOM crash. On the infrastructure side, **CI/CD pipeline integrity** took center stage: a triage agent was found cross-contaminating PR reviews ([Issue #5882](QwenLM/qwen-code Issue #5882)), and several PRs focus on hardening the release process. On a positive note, the ecosystem is growing—a new **bundled Extension Creator skill** ([PR #5828](QwenLM/qwen-code PR #5828)) aims to make building extensions frictionless, and the team is converging on a **resumable session architecture** ([PR #5030](QwenLM/qwen-code PR #5030), [PR #5852](QwenLM/qwen-code PR #5852)).

### 2. Releases
**No new releases in the last 24 hours.** The latest stable version remains **v0.19.2**, although the automated release workflow for this version experienced a failed publish job ([Issue #5831](QwenLM/qwen-code Issue #5831)).

### 3. Hot Issues (Top 10)

1.  **[#5873] Windows PowerShell OOM Bug (P1, OPEN)**
    - **What:** Every tool call spawns a new `powershell.exe` process that is never terminated, causing memory exhaustion. The author describes it as a critical regression in v0.19.2.
    - **Why it matters:** This is the most severe open bug. It renders the tool unusable on Windows and has generated strong community frustration.
    - [QwenLM/qwen-code Issue #5873]

2.  **[#5882] CI Cross-PR State Contamination (P1, OPEN)**
    - **What:** The `qwen-triage` workflow posted comments belonging to PR #5872 onto the completely separate PR #5874, indicating a failure of runner isolation.
    - **Why it matters:** A critical failure of the automated review pipeline. If state bleeds between jobs, the risk of incorrect merges increases significantly.
    - [QwenLM/qwen-code Issue #5882]

3.  **[#239] Streaming Setup Timeout (CLOSED)**
    - **What:** A persistent hard 64-second timeout on streaming setup, requiring users to reduce input length or increase `contentGenerator.timeout`.
    - **Why it matters:** High engagement (16 comments, 8 👍). Represents a common class of networking/resource issues that impacts users with large contexts.
    - [QwenLM/qwen-code Issue #239]

4.  **[#535] Qwen3 30B Tool Call Failure (CLOSED)**
    - **What:** Edit/write file tools consistently fail with `params/... must be string` errors when using the Qwen3 30b model.
    - **Why it matters:** Highlights compatibility friction between the Qwen Code agent framework and specific open-weight models.
    - [QwenLM/qwen-code Issue #535]

5.  **[#4493] JetBrains Rider OAuth Login Loop (CLOSED)**
    - **What:** Users on Rider are stuck in an OAuth redirect loop and cannot access cloud token plans.
    - **Why it matters:** A complete login blocker for JetBrains users, a key demographic for the IDE plugin.
    - [QLM/qwen-code Issue #4493]

6.  **[#5055] Trojan:JS False Positive (CLOSED)**
    - **What:** Windows Defender flagged the VSIX installer as a trojan.
    - **Why it matters:** Even though it is a false positive, this destroys trust and is a massive barrier for enterprise security teams.
    - [QwenLM/qwen-code Issue #5055]

7.  **[#2724] IntelliJ 2026.1 + Ollama Not Working (CLOSED)**
    - **What:** The agent forces a cloud login attempt even when configured for a local Ollama instance, working correctly in Rider/WebStorm but not IntelliJ.
    - **Why it matters:** Shows significant fragmentation in JetBrains plugin support, frustrating local-first users.
    - [QwenLM/qwen-code Issue #2724]

8.  **[#1002] Connection Error & Streaming Timeout Tracking (CLOSED)**
    - **What:** A meta-issue consolidating hard-to-reproduce reports of `connection error` and `streaming timeout`.
    - **Why it matters:** Represents a systemic weakness in network handling that is difficult for the team to diagnose without better telemetry.
    - [QwenLM/qwen-code Issue #1002]

9.  **[#5831] Release v0.19.2 Workflow Failure (CLOSED)**
    - **What:** The automated "publish" job failed during the release pipeline.
    - **Why it matters:** Ops transparency is high here, but repeated workflow failures damage developer confidence in the delivery pipeline.
    - [QwenLM/qwen-code Issue #5831]

10. **[#5665] AI PRs Missing Integration Tests (CLOSED)**
    - **What:** AI-generated PRs consistently update unit tests but miss integration tests, causing failures to surface only during releases.
    - **Why it matters:** Highlights a specific blind spot in the current agent capability regarding cross-repository context.
    - [QwenLM/qwen-code Issue #5665]

### 4. Key PR Progress (Top 10)

1.  **[#5828] Bundled Extension Creator Skill (OPEN)**
    - **Feature:** Adds a skill that automatically scaffolds, customizes, and tests Qwen Code extensions using the `qwen extensions new` template.
    - **Impact:** Lowers the barrier to entry for plugin developers significantly. A major ecosystem growth play.
    - [QwenLM/qwen-code PR #5828]

2.  **[#5030] Resume Interrupted Turn Without "Continue" (OPEN)**
    - **Feature:** Allows SDK callers to seamlessly resume an interrupted assistant turn without injecting a synthetic "continue" user message into the transcript.
    - **Impact:** A fundamental UX improvement for session reliability and long-running agentic tasks.
    - [QwenLM/qwen-code PR #5030]

3.  **[#5778] `/model --vision` Fallback (OPEN)**
    - **Feature:** Lets users configure a dedicated vision model that the system automatically uses when the main text model receives an image.
    - **Impact:** Solves the "I want vision but don't want to switch models" problem elegantly.
    - [QwenLM/qwen-code PR #5778]

4.  **[#5780] `qwen update` & `/update` Commands (OPEN)**
    - **Feature:** Adds CLI and in-chat commands to check for and install new versions, supporting npm and standalone distributions.
    - **Impact:** Eliminates a major friction point in the update workflow for non-VSIX users.
    - [QwenLM/qwen-code PR #5780]

5.  **[#5869] Stream-Highlight Code Blocks in Web Shell (OPEN)**
    - **Feature:** Implements live syntax highlighting while streaming code blocks and fixes language alias detection.
    - **Impact:** Eliminates flickering between plain text and highlighted views during streaming, vastly improving web shell readability.
    - [QwenLM/qwen-code PR #5869]

6.  **[#5852] Resume /acp Session Stream via SSE (OPEN)**
    - **Feature:** Implements standard SSE `Last-Event-ID` for the daemon's event stream, allowing reliable reconnection.
    - **Impact:** Core infrastructure hardening for the daemon architecture, preventing data loss on network drops.
    - [QwenLM/qwen-code PR #5852]

7.  **[#5777] Revive Chrome Extension (Daemon-Direct) (OPEN)**
    - **Feature:** Rebuilds the Chrome extension as a direct HTTP+SSE client of the local `qwen serve` daemon.
    - **Impact:** Brings back the Chrome platform with a vastly cleaner architecture compared to the previous Native Messaging approach.
    - [QwenLM/qwen-code PR #5777]

8.  **[#5847] Runtime Context Injection (OPEN)**
    - **Feature:** Adds a per-session key-value store that external callers can inject as `<system-reminder>` blocks on every turn.
    - **Impact:** Decouples dynamic context from static system prompts, enabling new patterns for SDK integrations.
    - [QwenLM/qwen-code PR #5847]

9.  **[#5878] Fix Standalone Archive Packaging (OPEN)**
    - **Feature:** Prevents the packaging script from aborting if a stale `dist/node_modules` directory exists.
    - **Impact:** Blocks a specific release-breaking bug, ensuring standalone builds can complete successfully.
    - [QwenLM/qwen-code PR #5878]

10. **[#5666] Ctrl+O Transcript View Design (OPEN)**
    - **Feature:** Proposes eliminating the compact/detailed mode toggle in favor of a single concise view with a frozen full-detail transcript on `Ctrl+O`.
    - **Impact:** A strong simplification of the terminal UX, reducing cognitive overhead for the user.
    - [QwenLM/qwen-code PR #5666]

### 5. Feature Request Trends

- **Agent Team Collaboration ([#1815](QwenLM/qwen-code Issue #1815)):** The highest-voted feature request (8 👍) asks for a "multi-agent team" mode where a lead agent coordinates sub-agents for parallel work. This indicates a desire for more complex, autonomous planning.
- **Reliability Set-Undo ([#2342](QwenLM/qwen-code Issue #2342), [#4204](QwenLM/qwen-code Issue #4204)):** The community continues to prioritize `/undo` and persistent file history. Users want a safety net for unexpected AI behavior.
- **Plan Approval Gates ([#5881](QwenLM/qwen-code Issue #5881)):** A new proposal extends the existing model-initiated plan review to user-initiated entries into plan mode. Users want more control and safety checkpoints before the agent executes changes.
- **CI/CD Process Maturity:** Internal and external contributors are pushing for stricter CI policies, including merge queues ([#4805](QwenLM/qwen-code Issue #4805)) and faster PR pipelines ([#5027](QwenLM/qwen-code Issue #5027)). This reflects a focus on professionalizing the development process as the project scales.
- **Better Multi-Modal UX:** Users want to drag-and-drop images or paste base64 data directly ([#3518](QwenLM/qwen-code Issue #3518)), not just rely on clipboard paste, which is currently broken on macOS.

### 6. Developer Pain Points

- **Windows Stability Crisis:** The #1 pain point today. The OOM bug ([#5873](QwenLM/qwen-code Issue #5873)) is a showstopper, compounded by known issues with background processes ([#481](QwenLM/qwen-code Issue #481)) and false positive antivirus alerts ([#5055](QwenLM/qwen-code Issue #5055)).
- **Streaming and Connection Reliability:** Recurring issues like "connection error", "streaming timeout" ([#239](QwenLM/qwen-code Issue #239), [#1002](QwenLM/qwen-code Issue #1002), [#1111](QwenLM/qwen-code Issue #1111)) remain the most persistent source of friction for remote API users.
- **JetBrains Second-Class Citizenship:** Users consistently report problems exclusive to JetBrains IDEs, particularly around authentication and local model detection ([#4493](QwenLM/qwen-code Issue #4493), [#2724](QwenLM/qwen-code Issue #2724)). The plugin experience is clearly lagging behind VS Code.
- **Context Management Confusion:** Power users are frustrated by broken context window limits and useless compression ([#1924](QwenLM/qwen-code Issue #1924)) and by UI bugs where messages vanish or the stop button fails ([#2678](QwenLM/qwen-code Issue #2678)).
- **AI Blind Spots in PRs:** Developers are noticing that the AI generates code and unit tests effectively but consistently misses related integration tests ([#5665](QwenLM/qwen-code Issue #5665)), forcing manual review to catch regressions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-26

**Note:** The project officially rebranded to **CodeWhale** starting from v0.8.65. The legacy `deepseek-tui` npm package is deprecated. This digest covers the renamed repository (`Hmbown/CodeWhale`).

---

## 1. Today's Highlights

CodeWhale crosses a major branding milestone with v0.8.65 formally deprecating the `deepseek-tui` name, while maintainers intensify efforts on production hardening and user-facing UX refinement. The community is sharply focused on two axes: taming the aggressive new approval flow that broke existing YOLO workflows, and closing the token-efficiency gap with Codex CLI through prompt slimming and better telemetry. A flurry of merged PRs today tackled stale sub-agent reconciliation, approval diff previews, and localization infrastructure, signaling a sprint toward the v0.8.66 stabilization milestone.

---

## 2. Releases

**v0.8.65 (CodeWhale Rebrand)**
The canonical project name is now `CodeWhale`. The legacy npm package `deepseek-tui` is officially deprecated and will receive no further releases. Users migrating from v0.8.x legacy trains (`deepseek` / `deepseek-tui`) should consult `docs/REBRAND.md`. This release also ships the TUI mouse-report input leak fix and various runtime safety improvements.

[View Release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.65)

---

## 3. Hot Issues

**#3568 — [BUG] Plan and Agent mode mixed up yet again**  
A recurring regression where the AI fails to respect mode switching. The attached trace shows the agent attempting file modification methods while in Plan mode. Community reaction is frustrated, as this is the second notable occurrence. [+1 👍, 5 comments]  
[Issue #3568](https://github.com/Hmbown/CodeWhale/issues/3568)

**#3606 — [BUG] Agent asks for confirmation in YOLO mode**  
Post-upgrade regression: YOLO mode, intended to be fully automatic, now blocks on permission prompts. Users expected `/mode YOLO` combined with `approval_mode AUTO` to suppress all confirmations.  
[Issue #3606](https://github.com/Hmbown/CodeWhale/issues/3606)

**#3466 — [CLOSED] Approval modal cancellation semantics**  
A top friction point. Users dislike the new "destructive approval every time" behavior introduced in 0.8.64. The thread requests a toggle or return to the original "no confirmation" default.  
[Issue #3466](https://github.com/Hmbown/CodeWhale/issues/3466)

**#1186 — [OPEN] Typed persistent permission rules**  
A long-running feature request (10 comments) to implement `allow/deny/ask` rules scoped by tool name, command prefix, and workspace path. This is the designated solution to the approval fatigue seen in #3466.  
[Issue #1186](https://github.com/Hmbown/CodeWhale/issues/1186)

**#1679 — [CLOSED] SSE multi-agent parallel timeout on Windows 11**  
Multi-agent execution on Windows reliably hits 45s SSE timeouts and UI corruption. Users are forced to fall back to solo serial execution. Platform-specific blocking bug.  
[Issue #1679](https://github.com/Hmbown/CodeWhale/issues/1679)

**#3205 — [OPEN] Fleet model classes, loadout auto, and semantic route roles**  
Architectural saga for the Fleet compute abstraction. The goal is to resolve full loadouts for roles/slots, not just model strings. Impacts TUI, CLI, sub-agents, and Fleet workers.  
[Issue #3205](https://github.com/Hmbown/CodeWhale/issues/3205)

**#861 — [CLOSED] Thinking collapse (multiple root causes)**  
A critical UX defect family where reasoning blocks freeze, truncate silently, or drop `reasoning_content`. Referenced frequently as a benchmark for prompt/streaming reliability.  
[Issue #861](https://github.com/Hmbown/CodeWhale/issues/861)

**#3541 — [OPEN] Rust-based native runtime / desktop client**  
A community proposal to replace the Node.js/TypeScript TUI with a Rust native client. Motivation includes cold-start latency, memory footprint, and event-loop stalls during long agent sessions. Sparks architectural debate.  
[Issue #3541](https://github.com/Hmbown/CodeWhale/issues/3541)

**#2953 — [OPEN] Slim default prompt toward Codex-parity input tokens**  
Strategic effort to reduce the base prompt footprint. CodeWhale's static prompt is measurably larger than Codex CLI's, contributing to token waste before any work begins.  
[Issue #2953](https://github.com/Hmbown/CodeWhale/issues/2953)

**#2300 — [OPEN] Multi-model compatibility, provider docs, and automatic Fleet loadout**  
A user-facing acceptance fixture for provider/model routing. Requests clearer documentation distinguishing `provider = vllm` vs `provider = openai` when using local endpoints.  
[Issue #2300](https://github.com/Hmbown/CodeWhale/issues/2300)

---

## 4. Key PR Progress

**#3633 — [OPEN] fix(release): gate registry publish on fresh assets**  
Adds `verify-release-assets.sh` to compare local/remote tag SHAs before publishing, preventing stale packages from reaching the registry.  
[PR #3633](https://github.com/Hmbown/CodeWhale/pull/3633)

**#3632 — [CLOSED] feat(tui): save apply_patch ask rules from validated touched files**  
Implements the "S" save shortcut in approval modals for `apply_patch`. Persists exact `tool = "apply_patch" + path = ...` ask rules upon successful preflight. Directly addresses #1186.  
[PR #3632](https://github.com/Hmbown/CodeWhale/pull/3632)

**#3631 — [CLOSED] test(tui): lock approval key badges**  
Adds render-test assertions for approval modal key badges (approve once, always, deny, abort) to lock the UX contract for #3380.  
[PR #3631](https://github.com/Hmbown/CodeWhale/pull/3631)

**#3629 — [CLOSED] perf(prompt): slim default static prompt**  
Compacts prose-heavy sections in `constitution.md` (RLM, thinking-budget, toolbox). Adds a regression test for the composed static prompt size. Targets Codex parity (#2953).  
[PR #3629](https://github.com/Hmbown/CodeWhale/pull/3629)

**#3622 — [CLOSED] fix(tui): harden approval change previews**  
Bounded `apply_patch` changes-array previews, counts skipped patch context lines, localizes preview sublabels for zh-Hans users. Follow-up on #3619.  
[PR #3622](https://github.com/Hmbown/CodeWhale/pull/3622)

**#3628 — [CLOSED] feat(exec): report prompt input composition**  
Adds `input_analysis` to `stream-json` metadata, breaking down token estimates by request/message/system/framing text and tool-use composition. Refs #2956.  
[PR #3628](https://github.com/Hmbown/CodeWhale/pull/3628)

**#3620 — [CLOSED] fix(tui): reconcile stale subagents before status**  
Critical reliability fix: cleans up heartbeat-expired sub-agents before state capture, preventing dead child agents from injecting stale "running" state into the next turn.  
[PR #3620](https://github.com/Hmbown/CodeWhale/pull/3620)

**#3619 — [CLOSED] fix(tui): show proposed file changes in approvals**  
Closes the highly-requested #1846. Renders bounded previews inside expanded approval cards for `write_file`, `edit_file`, and `apply_patch`.  
[PR #3619](https://github.com/Hmbown/CodeWhale/pull/3619)

**#3618 — [CLOSED] fix(tui): reuse live auto approval for follow-up paths**  
Completes the live auto-approval wiring from #3613. Routes sandbox elevation retry and queued task creation through `app_auto_approve_enabled`. Keeps YOLO and explicit `auto` modes aligned.  
[PR #3618](https://github.com/Hmbown/CodeWhale/pull/3618)

**#3583 — [OPEN] refactor(localization): extract hardcoded texts into JSON**  
Foundation work for i18n. Moves hardcoded strings from `crates/tui/src/localization.rs` to JSON locale files using the `rust-i18n` crate. Sets stage for multi-language support.  
[PR #3583](https://github.com/Hmbown/CodeWhale/pull/3583)

---

## 5. Feature Request Trends

**Persistent Security Policies**  
The dominant ask this cycle. Developers want to codify `allow/deny/ask` rules that persist across sessions rather than repeatedly approving destructive actions (#1186, #3466). The `S` save shortcut in #3632 is the first concrete step.

**Codex-Level Token Efficiency**  
Multiple issues (#2953, #2956, #2957, #2954) push for prompt slimming, transcript deduplication, and benchmark mode discipline. The community wants CodeWhale to match Codex CLI's input/output token footprint.

**Automated Agent Scaling ("Fleet")**  
Interest is growing in Fleet loadout auto-resolution (#3205) and provider-agnostic model selection (#2300). Users want one configuration that works across TUI, CLI, and multi-agent runs.

**Desktop Class Performance**  
The Rust native runtime proposal (#3541) reflects weariness with Node.js overhead. Expect more discussion around memory and cold-start profiles, especially for agent-heavy workloads.

**Localized Tooling**  
The localization PR (#3583) and zh-Hans preview sublabels in #3622 signal growing international contributor momentum.

---

## 6. Developer Pain Points

**Approval Flow Overreach**  
The post-0.8.64 security model is the #1 pain point. Users in YOLO mode or high-automation scripting find the new prompts intrusive (#3606, #3466). The rush to add persistent rules (#1186) confirms the default UX was too strong.

**Agent Mode Instability**  
Plan/Agent mode confusion (#3568) is a high-severity cognitive friction. When the AI violates mode constraints, users lose trust and must wipe conversation context to recover.

**Windows Platform Gaps**  
SSE timeouts and UI corruption under parallel sub-agents (#1679) remain unresolved, limiting Windows users to degraded (solo/serial) workflows. A growing concern as multi-agent use scales.

**Installation Friction**  
The `install.sh` endpoint returning HTML (#3582) and the complexity of distinguishing `vllm` vs `openai` providers (#2300) create onboarding hurdles that frustrate new evaluators.

**Model-Level Reliability**  
"Thinking collapse" (#861) and provider-specific concurrency limits (#3496) cause non-deterministic failures that are hard to reproduce, making triage slow.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*