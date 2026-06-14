# AI CLI Tools Community Digest 2026-06-14

> Generated: 2026-06-14 03:41 UTC | Tools covered: 9

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

**AI CLI Tools Cross-Platform Comparison Report: 2026-06-14**

---

### 1. Ecosystem Overview

The AI CLI tools ecosystem is in a phase of rapid infrastructure maturation under significant reliability pressure. Community feedback this week reveals a stark split between **platform leaders battling trust regressions** (data loss, hallucinated tool calls, session stability) and **aggressive challengers racing to close feature gaps**. Cross-cutting engineering priorities have crystallized around MCP (Model Context Protocol) hardering, multi-agent orchestration observability, and persistent memory management. The dominant story is that context economics—token bloat, cache retention, and prompt degradation—are now the primary operational bottleneck limiting production agent adoption. As models converge in quality, system-level reliability, extensibility, and cross-platform parity are emerging as the decisive differentiators.

---

### 2. Activity Comparison

| Tool | Notable Issues | PR Velocity (24h) | Release Velocity (24h) | Core Engineering Signal |
|---|---|---|---|---|
| **Claude Code** | 10 hot (8 critical bugs, data loss, hallucinated tools) | Low (3 PRs) | 0 | Stability / incident response cycle |
| **OpenAI Codex** | 10 hot (Windows brick, safety flag fatigue) | Very High (20+ PRs) | 2 alpha (rust-v0.140.0) | Deep sandbox / infrastructure push |
| **Gemini CLI** | 10 hot (agent hangs, config regression) | High (10 PRs) | 0 | MCP edge-case hardening |
| **Copilot CLI** | 5 updated (model availability, MCP preload) | None | 2 stable (v1.0.62 / v1.0.62-2) | Post-feature stabilization |
| **Kimi Code CLI** | 2 fresh + 8 deferred (TUI crash, infinite loop) | Medium (4 PRs, 3 merged) | 0 | API/MCP bugfix sprint |
| **OpenCode** | 10 hot (token growth OOM, TUI regressions) | High (10 PRs, major features) | 2 patch (v1.17.5/6) | High-velocity feature integration |
| **Pi** | 10 hot (cache billing, local model hangs) | High (10 PRs, Veil, Vertex) | 1 patch (v0.79.3) | Cost / cache / local model focus |
| **Qwen Code** | 10 hot (provider decouple, long-context loss) | High (10 PRs) | 0 | Interoperability / migration bridge |
| **DeepSeek TUI (CodeWhale)** | 10 hot (Agent Fleet architecture) | High (8 PRs, runtime API) | 0 | Cutting-edge multi-agent R&D |

---

### 3. Shared Feature Directions

Several cross-cutting requirements are appearing nearly simultaneously across multiple tool communities:

**1. MCP as the Universal Interconnect Layer**
- *OpenCode*: Full spec compliance demanded (client roots, streaming, error routing, OAuth escape)—closes 9 issues.
- *Gemini CLI*: Schema normalization, OAuth refresh with stored client ID, image MIME sniffing for Figma MCP.
- *Copilot CLI*: Request for eager MCP tool preloading into agent context (#3787).
- *Kimi Code CLI*: Direct MCP crash cascade fix (Notion, code-index disconnects killed sessions).
- *Qwen Code*: `/import-config` to migrate MCP servers from Claude Code and Claude Desktop.
- **Implication**: The ecosystem is standardizing on MCP as the TCP/IP of AI tooling. Strict spec compliance and robust error handling are now minimum requirements.

**2. Persistent Memory & Context Window Management**
- *Claude Code*: Lifecycle hooks (#47023) formalize an architecture 5+ community requests need.
- *OpenCode*: Unbounded `tokens.cache.read` growth (#30649) and `opencode.db` OOM from streaming events (#32005).
- *Gemini CLI*: Auto-memory retries low-signal sessions indefinitely (#26522).
- *Pi*: Cache retention bug silently dropping 1h TTL to 5min (#5703); new "Veil" capture system for smart context truncation.
- *Qwen Code*: Long-context attention loss and repetitive tool calls forcing session termination (#5018, #5019).
- **Implication**: Context window economy is the single greatest technical bottleneck. All teams are building or requesting smart compaction, caching, and eviction strategies.

**3. Multi-Agent Orchestration & Observability**
- *DeepSeek TUI*: Formal role-based Agent Fleet (scout, implementer, verifier, manager)—#3167.
- *OpenAI Codex*: Encrypted MultiAgentV2 removing the audit trail (#28058)—community pushing back hard.
- *Claude Code*: Configurable subagent reasoning effort (#43083) and parallel task spawning (#68333).
- *Gemini CLI*: Subagent false success reporting on turn-limit hits (#22323); agents running without permission (#22093).
- *Copilot CLI*: Subagent configuration (model, reasoning effort, time window) shipped in v1.0.62-2.
- **Implication**: Agent delegation is the headline feature, but observability, debugging transparency, and enforcement of user intent are failing everywhere. The tools that solve the "trust and verify" problem for subagents will win long-term adoption.

**4. Cross-Platform Parity (Windows / Linux)**
- *OpenAI Codex*: Most aggressive push—WSL path fixes, Windows sandbox, hermetic Wine/PowerShell test harnesses.
- *Claude Code*: tmux rendering corruption (#29937), JetBrains request (#47166), Windows app bricking (#27979).
- *OpenCode*: macOS hardened runtime SIGKILL, WSL UNC path brittleness.
- *Gemini CLI*: Browser agent fails under Wayland (#21983).
- *Kimi Code CLI*: TUI crash on terminal resize (#2450).
- **Implication**: macOS + VS Code is the universal "first-class" setup. Every other platform configuration is a second-class experience. This is the largest greenfield opportunity for a tool that delivers true parity.

---

### 4. Differentiation Analysis

| Tool | Core Differentiator | Target User | Current Technical Bottleneck |
|---|---|---|---|
| **Claude Code** | Model talent + ecosystem stickiness | Professional agent-heavy developers | Data integrity (hallucinated tools, session loss) |
| **OpenAI Codex** | Platform engineering / deterministic execution | Enterprise + cross-platform teams | Windows instability; safety heuristic overreach |
| **Gemini CLI** | MCP-first, sub-agent delegation | Developers wanting agent-as-teammate | Agent hangs; configuration disobedience |
| **Copilot CLI** | Polished GitHub integration | Mainstream developers, CI/CD | Model catalog gaps; tool visibility |
| **Kimi Code CLI** | Lightweight, Moonshot API | Niche Moonshot/Chinese ecosystem | Fragile subprocess/event-loop architecture |
| **OpenCode** | "Best of all worlds" feature integration | Power users / early adopters | Velocity / regression trade-off |
| **Pi** | Cost transparency, local models | Cost-conscious, self-hosters | Package manager instability (Shrinkwrap) |
| **Qwen Code** | Interoperability / migration bridge | Claude Code refugees, Asian market | Long-context model degradation |
| **DeepSeek TUI (CodeWhale)** | Advanced multi-agent control plane | Researchers, agent architects | Complexity fragility; narrow appeal |

---

### 5. Community Momentum & Maturity

- **Highest Engineering Velocity + Community Heat**: *OpenCode* and *DeepSeek TUI (CodeWhale)*. Both are rapidly shipping features while their communities actively contribute architectural design (Agent Fleet roles, MCP spec compliance). *OpenAI Codex* has massive internal velocity but higher user friction.

- **Mature Leader Under Pressure**: *Claude Code*. The deepest plugin ecosystem and largest mindshare, but the community's trust is visibly eroding due to a cluster of data-integrity regressions. Low PR velocity compared to the volume of critical bugs signals a defensive stabilization cycle.

- **Polished Product / Low Friction**: *Copilot CLI*. The quietest community this week, which is generally a strong signal in developer tools. The v1.0.62-2 marketplace launch went smoothly.

- **Rapidly Converging on Leaders**: *Gemini CLI* and *Qwen Code* are actively fixing foundational issues (MCP edge cases, provider flexibility) to reach parity with Claude Code and Codex. Both have sophisticated technical communities.

- **Fragile / Niche**: *Kimi Code CLI* shows the most concerning signal. Very low issue and PR volume relative to critical bugs (infinite loops, TUI crashes). Suggests a very small active user base or one in decline. *Pi* remains a healthy niche play.

---

### 6. Trend Signals

**For Technical Decision-Makers and AI Tool Developers:**

1. **Context Window is the New Memory**: Prompt engineering is giving way to context management engineering. Cache retention, compaction strategies, and KV-cache-aware prompt shaping (OpenCode #23595 eliminating moving system-reminders) are the new frontier for agent reliability.

2. **MCP Compliance is Non-Negotiable**: The Model Context Protocol is converging toward a universal standard akin to LSP for AI tooling. Tools that don't support roots, streaming, OAuth, and structured error handling by the end of 2026 risk ecosystem exclusion.

3. **The Audit vs. Autonomy Trade-off is Unresolved**: The community backlash against OpenCode's encrypted multi-agent messages highlights a fundamental tension. Developers demand **full transparency** for debugging agentic workflows. Encryption of agent internals, while good for security, is toxic for trust.

4. **Migration Barriers Are Crumbling**: Qwen Code's explicit `/import-config` for Claude Code users signals a brewing "migration war." Model exclusivity is no longer a lock-in factor; what keeps users is workflow reliability and tool ecosystem depth. The leaderboard can shift quickly if a key player falters on reliability.

5. **Cross-Platform is the Largest Untapped Moat**: Every tool ships a first-class macOS experience. The community signal from Windows (Codex bricking, WSL path mangling), Linux (tmux corruption, Wayland failure), and Web/mobile (Claude Code remote-control breakage) is a consistent cry for parity. A tool that delivers platform equity today would capture a massive dissatisfied user base.

6. **Safety System Calibration is Critical**: Over-flagging of benign operations (`git maintenance`, tax forms, standard DevOps) is creating "alert fatigue" across Codex and Qwen Code. The community is demanding frictionless professional modes that trust the developer's intent. The current paranoia is undermining the very trust safety systems are designed to protect.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-14 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Trends (by Community Attention & Impact)

**A. Skill-Creator Infrastructure & Reliability**
The single largest block of community engineering effort targets the skill development toolchain itself. Multiple contributors (Lubrsy706, Mr-Neutr0n, MartinCajiao, joshuawowk, gstreet-ops) submitted patches fixing YAML frontmatter parsing, case-sensitive file reference mismatches, UTF-8 multi-byte panics, Windows subprocess crashes, and the critical `run_eval.py` 0% recall bug (Issues #556, #1169). This cluster shows the community demanding a bulletproof meta-toolkit before building the next generation of skills.
- Status: Open (multiple PRs)
- Key PRs: [#539 (YAML validation)](https://github.com/anthropics/skills/pull/539) • [#538 (PDF case-sensitivity)](https://github.com/anthropics/skills/pull/538) • [#541 (DOCX w:id collision)](https://github.com/anthropics/skills/pull/541) • [#362 (UTF-8 fix)](https://github.com/anthropics/skills/pull/362) • [#1298 (0% recall overhaul)](https://github.com/anthropics/skills/pull/1298)

**B. Agent Persistence & Cognitive Architecture**
Three ambitious proposals target stateful agents: **shodh-memory** (#154) offers persistent cross-conversation context retrieval; the **AURELION suite** (#444) provides a structured cognitive framework with kernel, advisor, and memory modules; **agent-creator** (#1140) is a meta-skill for composing task-specific agent sets. This cluster represents the conceptual frontier of the ecosystem, directly addressing the #1 implicit demand for long-running agent workflows.
- Status: Open
- Links: [#154 (shodh-memory)](https://github.com/anthropics/skills/pull/154) • [#444 (AURELION)](https://github.com/anthropics/skills/pull/444) • [#1140 (agent-creator)](https://github.com/anthropics/skills/pull/1140)

**C. Document Quality & Format Support**
**document-typography** (#514) is a high-utility, low-complexity skill fixing orphan word wrap, widow paragraphs, and numbering misalignment—a universal quality gap in AI-generated documents. The **ODT Skill** (#486) adds full OpenDocument Format support, unlocking LibreOffice enterprise users who cannot rely on proprietary formats.
- Status: Open
- Links: [#514](https://github.com/anthropics/skills/pull/514) • [#486](https://github.com/anthropics/skills/pull/486)

**D. Security & Quality Meta-Skills**
**skill-quality-analyzer and skill-security-analyzer** (#83) are the community's most important self-regulation proposal. They evaluate skills across structure, documentation, and security dimensions—directly responding to the trust boundary abuse concerns raised in Issue #492 regarding the `anthropic/` namespace.
- Status: Open
- Link: [#83](https://github.com/anthropics/skills/pull/83)

**E. Testing & Code Quality Workflows**
**testing-patterns** (#723) introduces a comprehensive methodology (Testing Trophy, AAA pattern, React Testing Library). **codebase-inventory-audit** (#147) addresses orphaned code and documentation debt with a systematic 10-step workflow. Both reflect a shift toward skills that enforce engineering discipline rather than generate content.
- Status: Open
- Links: [#723](https://github.com/anthropics/skills/pull/723) • [#147](https://github.com/anthropics/skills/pull/147)

**F. Enterprise Analytics**
**SAP-RPT-1-OSS predictor** (#181) integrates SAP's open-source tabular foundation model into Claude Code for predictive analytics on business data—a strong signal of enterprise adoption and demand for domain-specific skills.
- Status: Open
- Link: [#181](https://github.com/anthropics/skills/pull/181)

---

## 2. Community Demand Trends (from Issues)

1. **Enterprise Sharing & Collaboration (#228)**
   The top-voted issue requests org-wide skill sharing without manual file transfers. This is the single biggest blocker for team adoption (14 comments, 7 👍).

2. **Deterministic Evaluation Framework (#556, #1169)**
   The `run_eval.py` 0% recall bug has become a rallying point. The community recognizes that reliable skill iteration requires a functioning evaluation loop—building complex skills on a broken evaluator is impossible.

3. **Governance & Trust Boundary Protection (#492, #412)**
   A security-focused contingent is actively concerned about namespace impersonation and demands "Agent Governance" patterns—policy enforcement, threat detection, audit trails—built into the skill architecture.

4. **Cross-Platform Stability & DX (#1061, #202)**
   Windows users face persistent subprocess and encoding issues. Combined with demands for skill-creator best practices (#202), the community is pushing for a mature, platform-agnostic developer experience.

5. **Protocol Interoperability (#16)**
   The long-standing request to expose skills as MCPs persists. Users want a standardized interface for composability rather than isolated skill files.

---

## 3. High-Potential Pending Skills

These **open** PRs combine strong utility with active community attention and are likely to land soon:

| Skill | Summary | Why It Matters |
|---|---|---|
| **document-typography** ([#514](https://github.com/anthropics/skills/pull/514)) | Fixes orphans/widows/numbering in AI docs | Universal pain point, low controversy, high impact |
| **ODT Skill** ([#486](https://github.com/anthropics/skills/pull/486)) | Create/fill/convert ODF documents | Enterprise & open-source interoperability |
| **testing-patterns** ([#723](https://github.com/anthropics/skills/pull/723)) | Comprehensive testing methodology | Directly meets developer demand for code quality |
| **skill-quality-analyzer** ([#83](https://github.com/anthropics/skills/pull/83)) | Meta-skill for auditing other skills | Governance is the hot trend; this is timely |
| **agent-creator** ([#1140](https://github.com/anthropics/skills/pull/1140)) | Meta-skill for composing task-specific agents | Aligns with the infrastructure + agents trajectory |
| **codebase-inventory-audit** ([#147](https://github.com/anthropics/skills/pull/147)) | Identifies orphaned code & doc gaps | Fills code cleanup workflow gap |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is shifting from authoring isolated prompt-based skills to building a reliable, governable, and stateful infrastructure layer—encompassing deterministic evaluation tooling, persistent memory systems, trust boundary enforcement, and enterprise-grade sharing—signaling the rapid professionalization of the Claude Code Skills ecosystem.**

---

# Claude Code Community Digest — 2026-06-14

## 1. Today’s Highlights
No new releases shipped today, and the community's focus is on a set of critical reliability regressions. Multiple reports document Opus 4.8 fabricating tool calls without executing them, while separate issues track session data loss and connection instability caused by hidden context accumulation. On the feature front, the highest-demand request remains formal lifecycle hooks to support community-built persistent memory layers.

## 2. Releases
No new versions were published in the last 24 hours.

## 3. Hot Issues
Ten noteworthy issues driving discussion today, ordered from most to least critical:

- **[BUG] Write Tool Data Loss** [`#67917`](https://github.com/anthropics/claude-code/issues/67917) — The Write tool's full-file-replacement default causes irrecoverable loss on governed state files. Community is requesting an append-only mode or protected-path mechanism. 8 comments, active since filing.

- **[BUG] Session JSONL Rewritten to Metadata Stub** [`#66734`](https://github.com/anthropics/claude-code/issues/66734) — All `user`/`assistant` records are being wiped from session transcripts, leaving only metadata. `/resume` opens empty sessions. Critical data-loss regression reported on the native installer.

- **[BUG] Opus 4.8 Fabricating Tool Executions** [`#67847`](https://github.com/anthropics/claude-code/issues/67847) — The model described executing `gh release create`, `Read`, and `Edit` in detail, but the API response contained zero `tool_use` blocks. Destroys trust in audit trails and session summaries.

- **[BUG] Spoofed Tool Results (Opus 4.8)** [`#68332`](https://github.com/anthropics/claude-code/issues/68332) — A separate report of fabricated tool results being injected into session context. Highlights a systemic issue with extended thinking mode.

- **[BUG] Hidden Context Buildup → ECONNRESET** [`#68339`](https://github.com/anthropics/claude-code/issues/68339) — Fresh project sessions rapidly accumulate hidden tool-result context and eventually fail with `ECONNRESET`. Suggests inefficient prompt packing or a memory leak.

- **[FEATURE] VS Code Auto-Attach Disable** [`#24726`](https://github.com/anthropics/claude-code/issues/24726) — Highest engagement today with **159 👍** and 52 comments. Community wants a setting to prevent Claude from automatically reading the open file or selection.

- **[PROPOSAL] Session Lifecycle Hooks for External Memory** [`#47023`](https://github.com/anthropics/claude-code/issues/47023) — A formal proposal to expose `compact` and `session` hooks. Addresses at least 5 other open issues requesting persistent memory. Community solutions are blocking on this.

- **[BUG] tmux Terminal Rendering Corruption** [`#29937`](https://github.com/anthropics/claude-code/issues/29937) — Long-standing Linux bug (38 👍). Text overlaps and overwrites previous output inside `tmux-256color`. Core TUI experience is broken for a significant user base.

- **[FEATURE] Configurable Subagent Reasoning Effort** [`#43083`](https://github.com/anthropics/claude-code/issues/43083) — Users want `low/medium/high` reasoning effort for subagents, not just model selection. 22 👍. Directly affects agent cost and latency tuning.

- **[FEATURE] Slash Commands in Remote-Control UI** [`#28379`](https://github.com/anthropics/claude-code/issues/28379) — `/clear`, `/compact`, `/context` typed in the web/mobile `/remote-control` UI are treated as plain text. 44 👍. Breaks core workflow parity for mobile users.

## 4. Key PR Progress
Only 3 pull requests were updated in the last 24 hours, suggesting the team is in a bug-fix or stabilization cycle:

- **[Open] Project-Theme Plugin** [`#68239`](https://github.com/anthropics/claude-code/pull/68239) — The only substantive contribution today. Adds a plugin that reads `theme`/`color` from `.claude/settings.json` and applies it on session start. Closes long-standing request `#43216`. This plugin pattern could serve as a template for community extensions.

- **[Closed] SECURITY.md** [`#1`](https://github.com/anthropics/claude-code/pull/1) — An old, closed PR adding a basic security policy.

- **[Open] Non-descriptive PR** [`#58673`](https://github.com/anthropics/claude-code/pull/58673) — A stub PR ("s") with no substantive content. Low priority.

*Analysis:* The low PR velocity combined with the volume of critical bugs suggests the core team is prioritizing stability and incident response over landing new features this cycle.

## 5. Feature Request Trends
Several clear directions emerged from the 30 top issues:

- **Persistent Memory Architecture (`#47023`)** — The most strategically significant request. Community members are building custom memory layers (markdown stores, knowledge graphs) but need official lifecycle hooks to prevent breakage on every update.

- **Agentic Control Maturation** — Users are pushing for finer-grained subagent management: reasoning effort (`#43083`), parallel task spawning (`#68333`), and team inbox routing fixes (`#50779`). The agent framework is gaining adoption, but default behavior is too opaque.

- **Cross-Platform & IDE Parity** — JetBrains (`#47166`), Windows (`#68340`), tmux on Linux (`#29937`), and the Remote-Control UI (`#28379`) are consistently cited as second-class experiences compared to macOS + VS Code.

- **UI Customization & Minimalism** — A steady stream of requests to hide status line elements (token counter `#21867`), disable sounds (`#59970`), and customize highlighting (`#8504`) indicates a desire for a cleaner workspace.

- **Permissions Model Refinement** — `bypassPermissions` continues to generate friction. Users expect it to mean zero prompts, but it regularly fails for `.claude/skills/` and `.claude/commands/` paths (`#37253`, `#36497`, `#53888`).

## 6. Developer Pain Points
The community's daily frustrations cluster in five areas:

- **Data Integrity Crisis** — Session transcript loss (`#66734`) combined with hallucinated tool calls (`#67847`, `#68332`) fundamentally undermines trust in session history and audit trails.

- **"Bypass Permissions" Doesn't Bypass** — The permission model is the top source of productivity friction. Promises of frictionless use are broken by constant prompts for `.claude/` edits, defeating the setting's intent.

- **Terminal Fragility on Linux** — tmux corruption (`#29937`) and CJK text mojibake in fullscreen mode (`#66269`) make the TUI unreliable for a significant chunk of the developer ecosystem.

- **Session Stability Over Long Runs** — Hidden context buildup leading to `ECONNRESET` (`#68339`) forces frequent `/compact` cycles, breaking deep reasoning sessions.

- **Cost Governance Gaps** — Team plan members can burn through credits without per-member confirmation (`#68346`), creating budget anxiety that slows enterprise adoption.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — June 14, 2026

**Technical Analyst Overview**

---

## 1. Today's Highlights

This week’s digest is dominated by a massive engineering push toward stable cross-platform execution, particularly fixing the Windows sandbox and remote-environment path handling pipeline. At the same time, community frustration is sharpening around two issues: overly aggressive cybersecurity safety flags blocking normal workflows, and a subtle but damaging regression where multi-agent encryption removes the developer audit trail. A substantial batch of 7 integration-test PRs from the execution team signals that reliability around the app-server process model is being locked down ahead of broader platform rollout.

---

## 2. Releases

Two incremental alpha releases for the Rust Codex CLI landed in the last 24 hours, continuing the rapid iteration cycle on the native build:

- **[rust-v0.140.0-alpha.18](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.18)** — initial release
- **[rust-v0.140.0-alpha.19](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.19)** — initial release

No detailed changelogs accompany these tags, but the surrounding PR activity is heavily focused on Windows CI pipeline optimization, hermetic Wine/PowerShell test harnesses, and exec-server path correctness, suggesting these alphas are foundation builds for cross-platform sandbox support.

---

## 3. Hot Issues

| Issue | Summary | Why It Matters |
|-------|---------|---------------|
| **[#27979](https://github.com/openai/codex/issues/27979)** — Windows App Broken After Update (18 comments) | Codex Desktop `26.609.4994.0` fails to launch entirely after the June 12 update. | **Critical blocker.** A complete bricking of the Windows desktop app erodes trust in auto-update channels. |
| **[#28015](https://github.com/openai/codex/issues/28015)** — False Positive Cybersecurity Flag on Repo Maintenance (15 comments) | Routine local DevOps hygiene (`git maintenance`, disk cleanup) triggers an intrusive safety check prompt. | **Core UX friction.** The safety system is mishandling context, halting legitimate sessions and undermining user confidence in the tool's judgment. |
| **[#24246](https://github.com/openai/codex/issues/24246)** — macOS “Malware Blocked” Alert for Codex Helper (11 comments, 9 👍) | macOS system-level malware gate triggers repeatedly on the Codex helper process. | **Trust and distribution issue.** Code signing or notarization problems at the OS level are extremely alarming to end users. |
| **[#24428](https://github.com/openai/codex/issues/24428)** — Codex Responds Too Slowly (14 comments, 25 👍) | Persistent slow SSE/WebSocket responses, especially since late May. | **Widespread performance pain point.** The high upvote count signals a silent majority experiencing latency regression. |
| **[#26158](https://github.com/openai/codex/issues/26158)** — Windows Sandbox Regression CLI 0.138.0 (10 comments, 5 👍) | `CreateProcessAsUserW` fails in sandbox setup; rollback to 0.132.0 required. | **Regression hygiene.** Users explicitly staying on older versions is a strong signal of broken core workflow. |
| **[#27603](https://github.com/openai/codex/issues/27603)** — 15-Second Interval Between Rounds (Windows CLI) (4 comments) | Windows CLI exhibits a complete freeze between conversation turns. | **Severe platform gap.** Makes the Windows CLI nearly unusable for interactive workflow. |
| **[#28086](https://github.com/openai/codex/issues/28086)** — WSL Agent Mode Fails to Find Bundled CLI (5 comments) | Windows app-server resolves the Linux CLI incorrectly in WSL environments, launching the Windows `.exe` instead. | **WSL path resolution broken.** This breaks the core "agent on behalf of" pattern for WSL-heavy developers. |
| **[#18896](https://github.com/openai/codex/issues/18896)** — Computer Use Permission Denied (macOS) (8 comments) | MCP-based permission elicitation is fighting with macOS TCC; Screen Recording + Accessibility grants ignored. | **Feature blocked by OS sandbox conflict.** Computer Use is inoperable on macOS regardless of user intent. |
| **[#28058](https://github.com/openai/codex/issues/28058)** — Encrypted MultiAgentV2 Removes Audit Trail (2 comments, 3 👍) | Encryption of inter-agent messages makes task execution invisible to the human operator. | **Silent observability regression.** Developers cannot debug subagent behavior—a dangerous trade-off for agentic tooling. |
| **[#20204](https://github.com/openai/codex/issues/20204)** — Inconsistent PreToolUse Hook Coverage (10 comments) | Hook events only fire for `shell`, `unified_exec`, `apply_patch`, and `mcp`—most tool types are invisible to the safety layer. | **Architecture risk.** Extensibility and safety auditing are incomplete across the tool registry. |

---

## 4. Key PR Progress

| PR | Feature / Fix | Why It Matters |
|----|---------------|---------------|
| **[#28151](https://github.com/openai/codex/pull/28151)** | Pipeline Windows targets separately | Eliminates ARM64 packaging waiting for x64; directly speeds up Windows release cycles. |
| **[#28146](https://github.com/openai/codex/pull/28146) / [#28152](https://github.com/openai/codex/pull/28152)** | Preserve and render remote environment cwd natively | Fixes cross-OS path mangling (`/C:/windows`), ensuring model-visible paths match the execution environment. |
| **[#28122](https://github.com/openai/codex/pull/28122)** | Exec-server honors remote environment cwd and shell | Core fix for Windows sandbox; passes the native shell and working directory through to the remote execution context. |
| **[#28120](https://github.com/openai/codex/pull/28120) / [#28124](https://github.com/openai/codex/pull/28124)** | Hermetic Windows shell testing with Wine + PowerShell | Foundational test infrastructure to prevent Windows sandbox regressions before they ship. |
| **[#27953](https://github.com/openai/codex/pull/27953)** | Load app-bundled internal hooks from Codex Desktop | Moves first-party plugin hooks into the app bundle as trusted, forced hooks—cleaning up the review UI and improving security posture. |
| **[#28118](https://github.com/openai/codex/pull/28118) / [#28143](https://github.com/openai/codex/pull/28143)** | Rate-limit reset redemption in `/usage` TUI | Adds backend + TUI support for earning and redeeming personal rate-limit reset credits—a highly visible quality-of-life feature. |
| **[#27607](https://github.com/openai/codex/pull/27607) / [#27602](https://github.com/openai/codex/pull/27602)** | Dedupe plugin MCPs; preserve plugin apps in listings | Plugin auth-routing stack narrowing conflicts between App-declared and plugin-provided MCP servers. |
| **[#28131](https://github.com/openai/codex/pull/28131)** | Refresh SSH agent for app-server proxy | Fixes a long-running connectivity issue where `SSH_AUTH_SOCK` goes stale after the parent SSH session exits. |
| **[#28132–#28136](https://github.com/openai/codex/pull/28132) series (7 PRs)** | Deterministic process handle tests (spawn, reuse, cleanup, handle conflicts, relative/absolute workdir) | Enforces the documented app-server contract through deep integration tests; removes prior flaky `ignore` policies. This is a major reliability unlock for the execution subsystem. |
| **[#28137](https://github.com/openai/codex/pull/28137)** | Verify app-server process cwd execution | Closes the gap where `process/spawn` tests supplied a cwd but never proved the child process actually used it. |

---

## 5. Feature Request Trends

The community is signaling a clear desire for **polish, customization, and backward compatibility** over raw new agent capabilities:

- **User-Configurable Settings** — [#25431](https://github.com/openai/codex/issues/25431) (spellcheck toggle, 13 👍) leads a push for per-feature toggles in the native desktop app, particularly on Windows.
- **State Persistence for Ephemeral Features** — [#26227](https://github.com/openai/codex/issues/26227) requests that side chats become persistent child threads rather than disposable context. Users want to treat temporary interactions as first-class session artifacts.
- **Hooks Extensibility** — The community is actively building on Codex (e.g., WorkGraph project in [#20985](https://github.com/openai/codex/issues/20985)). The incomplete hook coverage flagged in [#20204](https://github.com/openai/codex/issues/20204) is a growing blocker for third-party tooling.
- **IDE Ecosystem Parity** — [#19002](https://github.com/openai/codex/issues/19002) (CLion detection) reflects an expectation that Codex support the full JetBrains suite out of the box, not just the flagship IDEs.
- **Agent Rules Standard Adoption** — [#1624](https://github.com/openai/codex/issues/1624) (closed, positive) shows the community values AGENTS.md interoperability as a cross-tool standard.

---

## 6. Developer Pain Points

Recurring frustrations this week cluster tightly into three themes:

1. **Windows Instability Dominates the Support Signal**  
   The platform-wide Windows experience is the single largest source of friction: app crashes on update ([#27979](https://github.com/openai/codex/issues/27979)), sandbox setup failures ([#24391](https://github.com/openai/codex/issues/24391), [#26158](https://github.com/openai/codex/issues/26158)), WSL path mangling ([#28086](https://github.com/openai/codex/issues/28086), [#28094](https://github.com/openai/codex/issues/28094)), and severe latency ([#27603](https://github.com/openai/codex/issues/27603)). The macOS platform, while quieter, has its own critical OS-level friction with permission sandboxing ([#18896](https://github.com/openai/codex/issues/18896)) and trust notarization ([#24246](https://github.com/openai/codex/issues/24246)).

2. **Safety Heuristics Are Too Aggressive for Developer Workflows**  
   The cybersecurity flagging system continues to generate significant heat. Flagging `git maintenance` and personal tax form preparation as cybersecurity risks ([#28015](https://github.com/openai/codex/issues/28015), [#27817](https://github.com/openai/codex/issues/27817)) interrupts flow and creates a trust deficit. Developers accept safety prompts for genuine risk—not for daily DevOps hygiene.

3. **Observability Sacrificed for Encryption**  
   The MultiAgentV2 message encryption landing ([#28058](https://github.com/openai/codex/issues/28058)) embodies a risky design trade-off. While securing inter-agent communication is valuable, it silently removes the human-in-the-loop audit trail. For a developer tool where debugging agent decisions is paramount, this regression feels like a step backward from the transparency that developer tools require.

---

*Digest compiled from openai/codex activity on 2026-06-14.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-14

The community continued to focus on **agent reliability** and **MCP interoperability** this week. A cluster of high-priority PRs landed to address OAuth refresh for auto-discovered MCP servers, image MIME sniffing for Figma integrations, and a cap on pending tool responses to prevent agent deadlocks. On the issue tracker, agent hangs and configuration regression (subagents running without permission since v0.33.0) are drawing sustained community attention.

---

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

**1. Generalist agent hangs forever** [[#21409]](https://github.com/google-gemini/gemini-cli/issues/21409)  
*P1 · 8 👍* – The community's most-voted pain point. Simple operations (folder creation) hang indefinitely when the generalist agent is invoked. Users report disabling sub-agents entirely as the only workaround.

**2. Shell command execution stuck on "Waiting input"** [[#25166]](https://github.com/google-gemini/gemini-cli/issues/25166)  
*P1 · 3 👍* – After a simple CLI command completes, the agent retains the shell as active and waits for user input. Affects the core terminal workflow for even the most trivial commands.

**3. Subagent MAX_TURNS false success reporting** [[#22323]](https://github.com/google-gemini/gemini-cli/issues/22323)  
*P1 · 2 👍* – `codebase_investigator` reports `Termination Reason: "GOAL"` and `status: "success"` even after hitting the turn limit with zero analysis performed. Erodes user trust in agent result reporting.

**4. Subagents running without permission since v0.33.0** [[#22093]](https://github.com/google-gemini/gemini-cli/issues/22093)  
*P2* – Users who explicitly disabled sub-agents (expecting only MCP functionality) saw them activate automatically after upgrading. A configuration regression that breaks the user's safety model.

**5. Agent underutilizes custom skills and sub-agents** [[#21968]](https://github.com/google-gemini/gemini-cli/issues/21968)  
*P2* – Custom skills (e.g., "gradle", "git") and sub-agents are documented but rarely invoked unless explicitly mentioned in the prompt. This severely limits the value of the extension architecture.

**6. 400 error with > 128 tools** [[#24246]](https://github.com/google-gemini/gemini-cli/issues/24246)  
*P2* – Enabling too many tools causes a 400 error. Users want smarter tool-scoping when more tools are available than the API limit allows.

**7. Agent performs destructive operations without prompting** [[#22672]](https://github.com/google-gemini/gemini-cli/issues/22672)  
*P2 · 1 👍* – `git reset` and `--force` flags are used when safer alternatives exist. Developers want stronger guardrails for complex git/DB operations.

**8. Browser agent fails under Wayland** [[#21983]](https://github.com/google-gemini/gemini-cli/issues/21983)  
*P1 · 1 👍* – The browser sub-agent terminates immediately on Wayland sessions with a "GOAL" termination reason despite full failure.

**9. Symlinks in ~/.gemini/agents/ not recognized** [[#20079]](https://github.com/google-gemini/gemini-cli/issues/20079)  
*P2* – Symlinked agent files are silently ignored. This frustrates users who manage their agent configs with dotfile managers or version control.

**10. Auto Memory retries low-signal sessions indefinitely** [[#26522]](https://github.com/google-gemini/gemini-cli/issues/26522)  
*P2* – The background extraction agent can repeatedly surface the same low-value session. A missing "skip processed" mechanism creates infinite retries and potential log bloat.

---

## Key PR Progress

**1. Fix MCP OAuth refresh with stored client ID** [[#27889]](https://github.com/google-gemini/gemini-cli/pull/27889)  
*P1 · Agent* – Resolves token refresh failures for auto-discovered MCP servers where the `oauth.clientId` lives in stored metadata rather than static config.

**2. Cap pending tool responses** [[#27870]](https://github.com/google-gemini/gemini-cli/pull/27870)  
*P1 · Agent* – A large `functionResponse` payload can block the pending queue. This PR caps the response size to prevent the agent from stalling.

**3. MCP image MIME type sniffing** [[#27878]](https://github.com/google-gemini/gemini-cli/pull/27878) / [[#27850]](https://github.com/google-gemini/gemini-cli/pull/27850)  
*P1 · Core* – WebP images from Figma MCP were labeled as `image/png`, causing 400 errors. Implements base64 signature sniffing for PNG, JPEG, GIF, and WebP.

**4. Prevent regex stack overflow in @-command parser** [[#27580]](https://github.com/google-gemini/gemini-cli/pull/27580) *(CLOSED)*  
*P1 · Core* – Replaced a complex regex with an iterative scanner to prevent catastrophic backtracking when processing large pasted inputs.

**5. Fix command injection via safe `spawnSync`** [[#27575]](https://github.com/google-gemini/gemini-cli/pull/27575) *(CLOSED)*  
*P2 · Security* – Replaced shell-interpolated `execSync` in `findCommand()` and `commandExists()` with safe `spawnSync` calls.

**6. Normalize MCP tool schemas to root `type: object`** [[#27888]](https://github.com/google-gemini/gemini-cli/pull/27888)  
*P2 · Agent* – MCP servers without `type: "object"` in their input schema are rejected by Vertex AI strict mode. This patch normalizes schemas during discovery.

**7. Respect `.gitignore` and `.geminiignore` in `<session_context>`** [[#27886]](https://github.com/google-gemini/gemini-cli/pull/27886)  
*P2 · Core* – The directory tree shown inside session context previously ignored ignore rules, leaking file structure or irrelevant files into the prompt.

**8. Honor custom theme `border.default`** [[#27887]](https://github.com/google-gemini/gemini-cli/pull/27887)  
*P2 · CLI* – Documented custom border colors were silently overridden when the terminal reported a background color via OSC 11. Fixes two code paths that prevented user theming.

**9. Register all VS Code companion disposables** [[#27885]](https://github.com/google-gemini/gemini-cli/pull/27885)  
*P2 · Core* – Fixes a resource leak in `packages/vscode-ide-companion` where two activation registrations were never added to `context.subscriptions`.

**10. Add image-grounding hint to function responses** [[#27711]](https://github.com/google-gemini/gemini-cli/pull/27711)  
*Unprioritized · Core* – Opens the pipeline for multimodal tool results by hinting when a function response payload is an image attachment, enabling better grounding.

---

## Feature Request Trends

Several strategic themes are visible in this week's issue activity:

- **AST-aware code understanding** – Multiple EPICs ([[#22745]](https://github.com/google-gemini/gemini-cli/issues/22745), [[#22746]](https://github.com/google-gemini/gemini-cli/issues/22746), [[#22747]](https://github.com/google-gemini/gemini-cli/issues/22747)) are pushing toward AST-grounded file reads and search to reduce token waste and turn counts. This suggests a deeper commitment to codebase-aware tooling, possibly replacing regex-based approaches.

- **MCP as the primary extension path** – The volume of MCP fixes (OAuth, schema normalization, image support, tool response capping) indicates MCP is the strategic extensibility interface. The team is rapidly maturing edge-case handling that was missed in the initial implementation.

- **Persistent memory maturation** – Auto Memory issues [[#26525]](https://github.com/google-gemini/gemini-cli/issues/26525), [[#26522]](https://github.com/google-gemini/gemini-cli/issues/26522), and [[#26523]](https://github.com/google-gemini/gemini-cli/issues/26523) show the system is moving toward production-grade memory management (redaction, infinite retry prevention, invalid patch handling). This is a prerequisite for long-running session context.

- **Remote & background agent operations** – The Remote Agents Epic [[#20303]](https://github.com/google-gemini/gemini-cli/issues/20303) continues, pushing toward task-level auth and background processing, indicating a roadmap toward CI/CD and automated review workflows.

---

## Developer Pain Points

Recurring frustrations from the community this week highlight a **trust deficit between the agent's autonomy and user configuration**:

- **Agent hangs and stalls** are the #1 complaint. Generalist and shell agents fail on basic operations, forcing users to disable features entirely.
- **Configuration disobedience** is widespread. Agents ignore explicit disabling of sub-agents ([[#22093]](https://github.com/google-gemini/gemini-cli/issues/22093)), ignore custom skills and settings ([[#21968]](https://github.com/google-gemini/gemini-cli/issues/21968), [[#22267]](https://github.com/google-gemini/gemini-cli/issues/22267)), and choose destructive commands over safe ones ([[#22672]](https://github.com/google-gemini/gemini-cli/issues/22672)). This creates a need for "strict mode" enforcement.
- **False outcome reporting** ([[#22323]](https://github.com/google-gemini/gemini-cli/issues/22323)) is particularly concerning. When the agent declares "success" after actually hitting a wall, it breaks automated workflows and user trust. Developers cannot rely on the agent's own judgment of its results.
- **Scalability ceilings** are being hit. The 128-tool limit ([[#24246]](https://github.com/google-gemini/gemini-cli/issues/24246)) and the lack of smart tool scoping suggest the current architecture doesn't yet handle deeply integrated MCP ecosystems gracefully.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for June 14, 2026.

---

## GitHub Copilot CLI Community Digest — 2026-06-14

### 1. Today's Highlights
The `v1.0.62-2` release is the standout event, launching plugin marketplace support and adding powerful diff search features. On the issue tracker, the community is pushing hard for better model support, specifically requesting API key support for remote Ollama servers (#3789) and questioning the availability of advertised models like Gemini (#2550). The call for preloading MCP tools (#3787) signals a growing desire for more reliable agent-tool interaction.

### 2. Releases
Two versions dropped on June 13:

- **v1.0.62**: UI polish. Dialogs now scroll with the timeline instead of blocking it, allowing users to read older agent output while composing prompts.
- **v1.0.62-2** (Major feature release):
  - **Plugin Marketplace**: Plugins can now ship installable extensions, opening up the ecosystem.
  - **Diff View Search**: Content search with match highlighting and `n`/`N` navigation in the diff view.
  - **Slash Commands**: New `/app` command opens the GitHub app (with a browser fallback).
  - **Subagent Configuration**: Users can now configure the subagent model, reasoning effort, and context time window.

### 3. Hot Issues
Only five issues were updated in the last 24 hours. All are covered here:

1. **#2550 — Missing Models (CLOSED)** `[area:models]`
   - **Summary:** Users cannot find Gemini, Raptor mini, or Goldeneye models in the CLI model list despite being documented.
   - **Reaction:** High engagement (6 👍). This is a significant parity concern between docs and the actual CLI.
   - **Link:** [github/copilot-cli Issue #2550](https://github.com/github/copilot-cli/issues/2550)

2. **#3789 — Ollama API Key for Bring Your Own Model (OPEN)** `[triage]`
   - **Summary:** Requests the ability to add an API key for the host header when connecting a remote Ollama server.
   - **Reaction:** Brand new, no comments yet. Taps into the growing "local AI" and self-hosted model workflows.
   - **Link:** [github/copilot-cli Issue #3789](https://github.com/github/copilot-cli/issues/3789)

3. **#3787 — Preload MCP Server Tools (OPEN)** `[triage]`
   - **Summary:** Requests that MCP tools be eagerly loaded into the agent's initial `<available_tools>` list instead of lazy-loaded.
   - **Reaction:** Highlights a concrete UX failure: agents unaware of lazy-loaded tools cannot use them.
   - **Link:** [github/copilot-cli Issue #3787](https://github.com/github/copilot-cli/issues/3787)

4. **#3785 — Clarify `.copilotignore` Semantics (OPEN)** `[area:permissions, area:configuration]`
   - **Summary:** Asks for clear semantics and support of `.copilotignore` in the CLI, particularly for nested ignore files.
   - **Reaction:** Reflects broader community confusion about how file exclusion works across GitHub Copilot surfaces.
   - **Link:** [github/copilot-cli Issue #3785](https://github.com/github/copilot-cli/issues/3785)

5. **#3788 — Invalid Submission (CLOSED)**
   - **Summary:** A non-substantive issue closed quickly.
   - **Reaction:** Indicates active issue triage.
   - **Link:** [github/copilot-cli Issue #3788](https://github.com/github/copilot-cli/issues/3788)

### 4. Key PR Progress
No pull requests were updated in the last 24 hours. Development focus appears to be on stabilization following the `v1.0.62-2` release and triaging the recent influx of feature requests.

### 5. Feature Request Trends
Two major community aspirations are emerging from the current issue queue:

- **Expanding Model Coverage:** Users want the full advertised model catalog available in the CLI (Gemini/`#2550`), alongside fully-supported Bring Your Own Model flows for local/self-hosted providers (Ollama/`#3789`).
- **Smarter Agent Context & Tooling:**
  - The call for **eager MCP loading** (`#3787`) points to a desire for agents to have immediate, reliable visibility into the user's tool ecosystem.
  - Requests for **`.copilotignore` clarity** (`#3785`) show that power users need robust context control to manage large monorepos or sensitive directories effectively.

### 6. Developer Pain Points
- **Model Availability Discrepancies**: Documented models (Gemini, Raptor mini) are not actually accessible in the CLI (`#2550`).
- **Tooling Friction**: Agents fail to use available MCP tools due to lazy initialization (`#3787`).
- **Configuration Barriers**: Connecting custom local/remote models (Ollama) requires workarounds because the BYOM interface lacks basic API key support (`#3789`).
- **Lack of Context Controls**: Unclear or unsupported `.copilotignore` behavior leads to confusion about what the agent can read (`#3785`).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-14

## 1. Today's Highlights
The team pushed through a critical batch of infrastructure fixes this week. Three PRs from `wintrover` were merged, directly addressing Moonshot API JSON serialization bugs, MCP server crash cascades, and client timeout mismatches. Meanwhile, two blocking user-facing bugs remain unresolved: a new TUI crash on terminal resize (#2450) and a six-month-old infinite loop bug (#640) that saw renewed activity yesterday. The tone from recent issues suggests community patience is thinning around core reliability, even as the API integration layer stabilizes.

## 2. Releases
No new versions were published in the last 24 hours. The latest stable cut remains **Kimi Code v0.12.0**, though users on custom endpoints report running version `0.76`, indicating a wider-than-expected version spread in the community.

## 3. Hot Issues
*Only 2 Issues were updated in the last 24h; the remaining entries below are drawn from bugs explicitly referenced in recent PRs to show the full reliability picture.*

**#2450 – Uncaught Pi TUI exception due to screen width** [NEW]
- *Author:* iaindooley — *Created:* 2026-06-13 — *Comments:* 0
- A fresh crash report with zero triage. The terminal UI throws an unhandled exception on non-standard screen widths, blocking the CLI entirely. Since TUI is the primary UX surface, this demands immediate triage.
- `MoonshotAI/kimi-cli Issue #2450`

**#640 – CLI stuck in reading one file loop** [LONG-RUNNING]
- *Author:* isbafatima90-arch — *Created:* 2026-01-19 — *Comments:* 13 — *Updated:* 2026-06-13
- Updated yesterday after months of silence. The CLI enters an infinite loop reading the same file, with no timeout or progress progress. The user runs a custom Anthropic endpoint with `mimo-v2-flash` on Arch Linux. This is a catastrophic UX failure that appears to be model- or context-window dependent.
- `MoonshotAI/kimi-cli Issue #640`

**Moonshot API double-encoded JSON (#2406)** [RESOLVED]
- Tool call arguments (`todos`, nested objects) were returned as JSON strings instead of parsed objects, causing Pydantic validation to fail. Affected `SetTodoList`, `ExitPlan`, and similar tools. Fixed by PR #2407.

**MCP connection drop crashes** [RESOLVED]
- Notion and code-index MCP servers disconnecting during cleanup caused unhandled exceptions in the event loop. Fixed by PR #2434.

**Upstream proxy timeout hangs** [RESOLVED]
- The default 600s timeout from `AsyncOpenAI()` clashed with proxy limits (~300s), leaving users waiting 5+ minutes. Fixed by PR #2409.

**Web runner BrokenPipeError** [UNFIXED]
- Subprocesses exiting between `start()` and `drain()` crash the web session. Open PR #2324 exists but hasn't been merged.

**Crash telemetry fragility**
- `telemetry/crash.py` was heavily refactored in PR #2434, implying that crash reports themselves were generating secondary failures, a strong signal of systemic instability.

**Kosong provider configuration complexity**
- Multiple PRs target the `kosong/` provider module, suggesting users are struggling with custom endpoint setup.

**Custom Anthropic endpoint loops**
- Issue #640's platform (`custom anthropic endpoint`) hints at a broader class of loop bugs affecting non-Moonshot models.

**Model churn risk (`mimo-v2-flash`, `k2.6`)**
- Users running newer or less common model IDs are hitting the sharpest edges. The TUI crash (#2450) hit on `k2.6`.

## 4. Key PR Progress
*4 Pull Requests were updated in the last 24h (3 merged, 1 open). Their impact breaks down into 10 distinct changes.*

**#2434 – Suppress MCP connection errors in event loop handler** [MERGED]
- `src/kimi_cli/telemetry/crash.py`: guards cleanup when an MCP server (Notion, code-index) drops mid-session. Prevents cascading failure.
- `MoonshotAI/kimi-cli PR #2434`

**#2434 – Handle LLM double-serialization in action calls** [MERGED]
- Same PR corrects a bug where the LLM receives already-serialized action calls, preventing agent orchestration failures.

**#2407 – Fix double-encoded JSON in tool call arguments** [MERGED]
- `src/.../tool_calls.py`: After `json.loads` on the outer frame, inner values like `todos` remained as strings. Fixed by recursively parsing nested JSON strings.
- `MoonshotAI/kimi-cli PR #2407`

**#2407 – Pydantic validation fix for nested tool values** [MERGED]
- Specific fix ensures `SetTodoList`, `ExitPlan`, and any tool receiving deeply nested arrays/objects pass model validation.

**#2407 – JavaScript/Python double-stringify edge case** [MERGED]
- Fixes the root cause: Moonshot API's backend calling `JSON.stringify` twice on arrays within `function.arguments`.

**#2409 – Add default 120s timeout to `create_openai_client`** [MERGED]
- `kosong/chat_provider/openai_common.py`: overrides the OpenAI SDK's 600s default with 120s to match proxy timeouts.
- `MoonshotAI/kimi-cli PR #2409`

**#2409 – MiMo proxy alignment** [MERGED]
- Prevents silent 5-minute hangs when upstream proxies (e.g., MiMo API) time out around 300s.

**#2324 – Handle BrokenPipeError in `SessionProcess.send_message`** [OPEN]
- `src/kimi_cli/web/runner/process.py`: adds a `try/except` guard for `BrokenPipeError` when the subprocess exits before `stdin.drain()` completes.
- `MoonshotAI/kimi-cli PR #2324`

**#2324 – Web process lifecycle guard** [OPEN]
- Checks if `process.returncode` is set before writing, preventing orphaned sends to dead subprocesses.

**#2324 – Stdin drain error isolation** [OPEN]
- Prevents one failed subprocess from crashing the entire `SessionProcess` loop, improving concurrent request resilience in the web runner.

## 5. Feature Request Trends
- **MCP ecosystem stability:** Users expect tools (Notion, code-index) to be first-class citizens. Crashing the CLI on MCP disconnect is a hard blocker for production adoption.
- **Custom API endpoint hardening:** Non-Moonshot backends (Anthropic, OpenAI proxy) are heavily used. The loop bug (#640) strongly implies the context ingestion pipeline is fragile outside Moonshot's native models.
- **TUI resilience:** The TUI must handle `SIGWINCH` and non-standard terminal widths gracefully. Zero-tolerance for resize-related panics.
- **Timeout configurability:** The 600s default is universally considered too high. The 120s fix in #2409 will likely need to be user-configurable going forward.
- **Tool calling reliability:** Double-serialization bugs erode trust in agentic workflows. The community wants robust parsing regardless of backend.

## 6. Developer Pain Points
| Pain Point | Source / Evidence | Severity |
|---|---|---|
| Infinite AI loops | Issue #640 — CLI reads same file forever with no escape | Critical |
| TUI crash on resize | Issue #2450 — blocks entire CLI on basic OS event | Critical |
| MCP server crash cascade | PR #2434 — single disconnected tool kills session | High |
| API double-encoded JSON | PR #2407 / #2406 — tools silently fail on many models | High |
| Subprocess death in web runner | PR #2324 — concurrent requests lose reliability | Medium |
| 600s timeout hang | PR #2409 — unacceptable wait on slow proxies | Medium |
| Slow resolution of blocking bugs | Issue #640 open since January 2026 | Latent frustration |
| Version fragmentation | Users on `0.76` vs `v0.12.0` with distinct bugs | Config overhead |

**Summary:** The next release needs to prioritize TUI stability and the infinite file loop. The three merged PRs from `wintrover` are a strong step forward for API and MCP integration, but they are erasing symptoms, not rewriting the fragile subprocess/event-loop architecture underneath.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for June 14, 2026.

---

## OpenCode Community Digest — 2026-06-14

### 1. Today's Highlights
A significant wave of MCP infrastructure hardening landed today, led by @rekram1-node, improving client roots, error routing, and OAuth security ([see PRs](#key-pr-progress)). On the feature front, the massive **Cedric multi-tab workspace** and a native **`/goal` session command** are queued for release. However, platform stability remains a top concern, as critical bugs around **unbounded token growth** ([#30649](#30649)) and **database bloat from streaming events** ([#32005](#32005)) threaten long-running agentic workflows.

### 2. Releases
Two patch versions shipped in the last 24 hours.

*   **v1.17.6** ([View Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.6))
    *   **Bugfix:** Improved MCP server compatibility by declaring OpenCode's supported client capabilities.
*   **v1.17.5** ([View Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.5))
    *   **Improvements:** Added external browser OAuth for the Snowflake Cortex provider (@santigc6). Improved project copy management and move-session flows in v2 layout.
    *   **Bugfixes:** Recovered expired MCP sessions instead of leaving tools disconnected. Cleared stale closed MCP clients to prevent resource leaks.

### 3. Hot Issues

1.  **[#2755 [CLOSED] feat: Copy Mode for OpenCode](https://github.com/anomalyco/opencode/issues/2755)**
    *   **Context:** The most active issue (17 comments, 76 👍). Users are demanding a vim/tmux-like mode for precise text selection from messages and code blocks.
    *   **Why it matters:** Highlights that while the core agent is powerful, the chat UX for output consumption needs mature editing and selection tools.

2.  **[#5076 [CLOSED] Better/Safer Defaults for Security](https://github.com/anomalyco/opencode/issues/5076)**
    *   **Context:** A highly-upvoted (60 👍) call for making OpenCode restrict file system and shell access by default, shifting to an "ask-first" security model.
    *   **Why it matters:** Reflects the community’s desire to trust OpenCode with production projects, viewing the current "allow-by-default" setup as a serious risk.

3.  **[#28567 [OPEN] Full MCP Client Capabilities](https://github.com/anomalyco/opencode/issues/28567)**
    *   **Context:** Users are explicitly calling out the gap between OpenCode’s MCP client and the latest MCP protocol standard. (20 👍)
    *   **Why it matters:** Directly aligns with the high volume of MCP PRs today. The ecosystem is demanding strict compliance and full feature parity (roots, streaming, etc.).

4.  **[#30649 [OPEN] Unbounded Session Token Growth](https://github.com/anomalyco/opencode/issues/30649)**
    *   **Context:** A critical reliability bug where `tokens.cache.read` grows without a practical upper bound, eventually making long sessions unrecoverable due to context-window errors.
    *   **Why it matters:** This is a major scaling blocker for users running deep, multi-turn agentic tasks.

5.  **[#32005 [OPEN] Event Table Bloat Causing OOM](https://github.com/anomalyco/opencode/issues/32005)**
    *   **Context:** `message.updated.1` events from streaming subagents are bloating the `opencode.db` to hundreds of MB, causing OOM crashes when loading old sessions.
    *   **Why it matters:** A severe performance regression in the database layer for heavy users of the subagent/explorer pattern.

6.  **[#28957 [OPEN] "Upstream Idle Timeout Exceeded"](https://github.com/anomalyco/opencode/issues/28957)**
    *   **Context:** Users utilizing the "writing-plans" skill are hitting infrastructure-side timeouts from the model provider. (12 comments)
    *   **Why it matters:** Shows the tension between long-running tool loops (e.g., deep research/planning) and typical API gateway timeouts.

7.  **[#32231 [CLOSED] Terminal Option Removed in v2](https://github.com/anomalyco/opencode/issues/32231)**
    *   **Context:** Users report the CLI/Terminal start button has vanished in the new layout.
    *   **Why it matters:** A straightforward UX regression in the v2 layout that blocks a core workflow. High urgency for everyday users.

8.  **[#32260 [OPEN] TUI Themes Broken After opentui Upgrade](https://github.com/anomalyco/opencode/issues/32260)**
    *   **Context:** Upgrading the core `opentui` library from 0.1.x to 0.3.x broke all built-in color themes.
    *   **Why it matters:** A fresh regression (filed today) that degrades the experience for every TUI user, requiring an immediate fix.

9.  **[#23595 [OPEN] System-Reminder Breaks Prompt Cache](https://github.com/anomalyco/opencode/issues/23595)**
    *   **Context:** An astute technical report detailing how OpenCode keeps moving `<system-reminder>` in the prompt history, invalidating the KV cache in local runners like llama.cpp. (8 👍)
    *   **Why it matters:** Demonstrates deep community understanding of LLM inference overhead and highlights significant wasted prompt processing in the current architecture.

10. **[#18503 [CLOSED] macOS SIGKILL (Missing Hardened Runtime)](https://github.com/anomalyco/opencode/issues/18503)**
    *   **Context:** The binary crashes immediately on macOS 26.x due to missing `TeamIdentifier` code signatures.
    *   **Why it matters:** A platform-critical issue that completely blocks adoption for users on the latest macOS. Highlights the need for proper CI/CD code signing.

### 4. Key PR Progress

1.  **[#32235 [CLOSED] feat: Prepare Cedric Workspace Release](https://github.com/anomalyco/opencode/pull/32235)**
    *   **What it does:** A massive feature PR introducing a multi-tab workspace surface with Browser, file, code, Markdown, Terminal, Side Chat, and a Background Tasks lifecycle.
    *   **Impact:** The biggest UX shift in this digest. Moves OpenCode closer to a full IDE alternative.

2.  **[#32230 [CLOSED] feat(mcp): Support Client Roots](https://github.com/anomalyco/opencode/pull/32230)**
    *   **What it does:** Advertises MCP client `roots` capability and serves the project directory as a `file://` URI.
    *   **Impact:** Foundational for MCP servers that need to understand the project structure (e.g., linters, dependency checkers).

3.  **[#32244 [OPEN] fix(mcp): Handle Tool Result Errors](https://github.com/anomalyco/opencode/pull/32244)**
    *   **What it does:** Routes `CallToolResult.isError` responses through the AI SDK’s tool-error path, preserving rich diagnostics. (Closes #16969, relates to #28567)
    *   **Impact:** Stops MCP errors from being invisible or generic. A major DX improvement for plugin developers.

4.  **[#32239 [CLOSED] feat(session): Add Native /goal](https://github.com/anomalyco/opencode/pull/32239)**
    *   **What it does:** Implements a per-session goal system with status tracking (active/paused/completed) and an optional token budget.
    *   **Impact:** Addresses the long-standing request for better session steering (#27167) without relying on fragile system prompts.

5.  **[#32242 [OPEN] fix(mcp): Escape OAuth Callback Errors](https://github.com/anomalyco/opencode/pull/32242)**
    *   **What it does:** Escapes provider-controlled error strings before rendering HTML and declares UTF-8 encoding for callback pages. (Closes #17364, relates to #28567)
    *   **Impact:** Critical security fix preventing XSS vector through malicious MCP OAuth providers.

6.  **[#32261 [OPEN] fix(opencode): Accept Leading # in PR Command](https://github.com/anomalyco/opencode/pull/32261)**
    *   **What it does:** Allows `opencode pr #992` by typing the positional argument as a string instead of a number.
    *   **Impact:** Small but immediate quality-of-life fix for users who habitually use the `#` prefix when referencing GitHub PRs.

7.  **[#32193 [OPEN] fix(core): Mentions for Files in Hidden Folders](https://github.com/anomalyco/opencode/pull/32193)**
    *   **What it does:** Enables `@`-mentioning files inside folders with a leading `.` or prefix. (Fixes #32126)
    *   **Impact:** Resolves a frustrating blind spot where users couldn't reference config files (e.g., `.env`, `.gitignore`) in their prompts.

8.  **[#32247 [OPEN] feat(ui): Full RTL Support](https://github.com/anomalyco/opencode/pull/32247)**
    *   **What it does:** Adds full Right-to-Left language support for the entire UI.
    *   **Impact:** Major localization improvement that makes the tool accessible to a significantly broader audience (Arabic, Hebrew, etc.).

9.  **[#27231 [OPEN] feat: Add Edit Button for Connected Providers](https://github.com/anomalyco/opencode/pull/27231)**
    *   **What it does:** Provides a UI button to edit provider configurations (e.g., API keys, model selection). (Closes #20598)
    *   **Impact:** Removes the need for manual JSON configuration changes, significantly improving onboarding and admin UX.

10. **[#29132 [CLOSED] fix: Await Event Loop in Non-Interactive Run](https://github.com/anomalyco/opencode/pull/29132)**
    *   **What it does:** Fixes `opencode run --format json` exiting before the event stream has completed. (Closes #26855)
    *   **Impact:** Critical for CI/CD integrations and scripting, ensuring output is complete before a process exit code is emitted.

### 5. Feature Request Trends

*   **MCP Spec Compliance:** Users are aggressively pushing for full [MCP specification](https://modelcontextprotocol.io/specification/2025) compliance. Requests for client roots, proper error handling, streaming, and auth flexibility dominate the feature backlog (#28567, #32230).
*   **Agentic UX Control:** There is a strong trend towards giving users more steering capability. This includes **Copy Mode** for output (#2755), **Safe/Permissive Modes** for security (#5076), **Persisted Goals** (#32239), and **Session Autosave** (#1865). Users want to feel in control of the agent, not just passengers.
*   **Desktop and Terminal Maturity:** Blunt edges in the desktop app (WSL paths [#19473], certificate errors [#32250], `xdg-open` containers [#31815]) indicate a growing user base that expects a polished, native experience.
*   **Model Provider Diversity:** The community actively requests support for emerging models (GLM-5.2 [#32172]) and better local provider UX (Ollama [#19326]), underscoring the importance of a vendor-neutral provider abstraction.

### 6. Developer Pain Points

*   **V2 Layout Regressions:** The rollout of the new layout and designs has introduced frustrating regressions. Users are reporting the **missing agent picker** (#30360), the **removed terminal option** (#32231), and **broken TUI themes** (#32260). The velocity of the UI overhaul is outpacing stability.
*   **Long Session Instability:** The most critical technical hurdle. The system struggles with deep agentic loops. Issues like **unbounded token growth** (#30649), **event table OOM crashes** (#32005), and **upstream idle timeouts** (#28957) suggest the database and prompt management layers need re-architecting to handle the load they generate.
*   **Prompt Caching Waste:** Power users running local models (llama.cpp, Ollama) are acutely sensitive to prompt processing costs. The moving `<system-reminder>` (#23595) and unnecessary re-processing caused by agent file edits (#32246) represent significant computational waste that the core team needs to address.
*   **Authentication Friction:** Getting started remains a headache. Issues like binary **SIGKILL on macOS** (#18503), **Ollama not appearing** (#19326), **server password conflicts** (#24204), and **WSL UNC path brittleness** (#19473) create a high barrier to entry for new users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi community digest for June 14, 2026, based on data from `github.com/badlogic/pi-mono`.

**Pi Community Digest — 2026-06-14**

**Today's Highlights**
A critical billing fix lands in v0.79.3, correcting mismatched context window metadata for GPT-5.x Codex models. However, the community is sounding the alarm on a silent cache retention bug for Claude that is costing users money, and a hard blocker has emerged for local LLM users. PR activity is strong, featuring a new Veil context capture system, long-awaited Anthropic Vertex integration, and Windows clipboard image support.

**Releases**
- **v0.79.3**: Fixes a high-severity billing hazard where inherited context window metadata for OpenAI GPT-5.4, GPT-5.5, and Codex variants incorrectly advertised a larger limit than the actual 272k-token Codex backend limit. Prompts exceeding this limit were being billed but silently failing. (Reported by [@trethore](https://github.com/trethore)). [Release Details](https://github.com/badlogic/pi-mono/releases/tag/v0.79.3)

**Hot Issues**
- **[[#5703]](https://github.com/earendil-works/pi/issues/5703) 1h Cache Retention Silently Degraded for Claude Models**: A major cost bug. Pi sends `cache_control.ttl: "1h"` but omits the required `extended-cache-ttl-2025-04-11` beta header, causing the API to silently revert to a 5-minute retention window. Users are paying full price for cache hits they are not getting. (8 comments)
- **[[#5644]](https://github.com/earendil-works/pi/issues/5644) GPT 5.5 API/Codex Incorrect Context Window Size**: User reports the actual Codex window is 400K and the API is 1M, conflicting with Pi's current metadata. Highlights an ongoing challenge with model configuration accuracy. (6 comments)
- **[[#5653]](https://github.com/earendil-works/pi/issues/5653) Move off Shrinkwrap**: A critical architectural issue. Installing `pi-ai` and `pi-coding-agent` as direct dependencies results in duplicate module copies and a broken API provider registry. This is a major threat to extension ecosystem stability. (7 comments)
- **[[#5706]](https://github.com/earendil-works/pi/issues/5706) Task Hangs at Summary Approval with Local LLM Backends**: A showstopper for self-hosters. The task freezes indefinitely during summary approval when using a local OpenAI-compatible backend, requiring a manual kill. Cloud providers are unaffected. (3 comments)
- **[[#5571]](https://github.com/earendil-works/pi/issues/5571) `pi -p` Hangs with Unauthenticated Default Provider**: Poor out-of-box experience. On a fresh install with no API keys, `pi -p` hangs for 3+ minutes instead of failing fast with a clear configuration error. (5 comments)
- **[[#5702]](https://github.com/earendil-works/pi/issues/5702) `prompt_cache_retention` Sent to Providers that Reject It**: Sending caching headers to unsupported providers (like opencode/zen) results in 400 errors. The issue also raises concerns about the maintainability of the model-registry build system. (4 comments)
- **[[#5687]](https://github.com/earendil-works/pi/issues/5687) `pi list`/`update` Hangs with MCP Server Extensions**: Package management commands become zombie processes if an installed extension is running a long-lived MCP server, refusing to exit. (3 comments)
- **[[#5654]](https://github.com/earendil-works/pi/issues/5654) Add `excludeFromContext` to Custom Messages**: Users want slash commands to display interactive messages in the TUI without injecting them into the LLM context window, mirroring existing bash execution flags. (4 comments)
- **[[#5595]](https://github.com/earendil-works/pi/issues/5595) openai-completions `maxTokens` Not Passing Through**: Reasoning models like DeepSeek V4 hit token limits mid-turn because the user-set `maxTokens` value is silently ignored by the provider. (5 comments)
- **[[#289]](https://github.com/earendil-works/pi/issues/289) Custom Slash Commands for Coding Agent**: A long-standing top request. Users want slash commands that can execute arbitrary logic (UI, bash, permission checks), moving beyond simple prompt injection. (18 comments)

**Key PR Progress**
- **[[#5526]](https://github.com/earendil-works/pi/pull/5526) Require Terminal Events for OpenAI Responses Streams**: Fixes random stream stoppages and context counter desyncs by enforcing that OpenAI Responses streams end only on terminal events. Essential for reliability with OpenAI models.
- **[[#5708]](https://github.com/earendil-works/pi/pull/5708) Wrap Question Extension Text Instead of Truncating**: A clean UI fix that prevents text clipping in the extension input area.
- **[[#5704]](https://github.com/earendil-works/pi/pull/5704) Capture System for Auto-Storing Tool Results (Veil)**: Implements the "Capture" phase of context management, automatically caching tool results (Read, Bash, WebSearch, WebFetch) with content-based deduplication and smart truncation.
- **[[#5690]](https://github.com/earendil-works/pi/pull/5690) Configurable chat-template ThinkingFormat for vLLM**: Implements a generic `thinkingFormat: "chat-template"` for OpenAI-compatible providers, enabling proper thinking support beyond hardcoded model family rules. Addresses a major gap for vLLM users.
- **[[#5262]](https://github.com/earendil-works/pi/pull/5262) Add Anthropic Vertex Provider**: Adds a built-in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI, reusing the existing Anthropic streaming and tooling infrastructure.
- **[[#5688]](https://github.com/earendil-works/pi/pull/5688) Force Safe esbuild Resolution**: Closes a transitive dependency vulnerability by forcing `esbuild` to `^0.28.1` and refreshing the lockfile.
- **[[#5640]](https://github.com/earendil-works/pi/pull/5640) Paste Clipboard Images via Ctrl+V on Windows Terminal**: Solves a problem where Windows terminals swallow Ctrl+V as text paste. Now handles image pasting natively for Windows users.
- **[[#5665]](https://github.com/earendil-works/pi/pull/5665) Handle `setActiveTools(undefined)` Gracefully**: Fixes a runtime crash (`toolNames is not iterable`) when developers pass `undefined` to restore all tools, matching the documented TypeScript types.
- **[[#5701]](https://github.com/earendil-works/pi/pull/5701) Fix MinMax-M3 Context Size**: Adjusts the MinMax-M3 context size from 1M to the correct 524,288 token limit observed through OpenRouter.
- **[[#5693]](https://github.com/earendil-works/pi/pull/5693) Merging Official Repo Updates**: Routine merge to maintain release parity.

**Feature Request Trends**
- **Context Window Autonomy**: Users are demanding fine-grained control over context management. This includes explicit `excludeFromContext` flags for custom messages, smart caching strategies (the Veil system), and preventing bloat from system prompts.
- **Multi-Session & Background Agents**: A strong desire for concurrent, persistent agent sessions that can be switched via the TUI without destroying the current session context.
- **Extensible Agent Runtime**: The community wants slash commands and extensions that go beyond LLM orchestration, enabling interactive UI elements, dynamic permission checks, and complex scripting.
- **Provider Agnosticism**: Continuous pressure for feature parity across all backends. The bugs related to local LLMs, vLLM thinking formats, and Vertex AI integration show a community that relies on a diverse model ecosystem.

**Developer Pain Points**
- **Package Manager Instability**: The Shrinkwrap-based installation system is a top source of systemic friction. Duplicate module instances, ignored semver ranges, and broken self-update mechanisms make the developer experience fragile.
- **Silent Degradation of Features**: The most frustrating class of bugs. Features like API caching and token limits are silently capped or dropped without user notification, leading to unexpected failures and costs.
- **Lack of Resilient Error Recovery**: The agent's state machine is brittle. Continuation crashes (`Cannot continue from message role: assistant`), unhandled TUI render failures, and unresponsive MCP processes highlight a need for stronger error boundaries.
- **Inaccurate Provider Metadata**: Model definitions for context windows, available thinking levels, and API capabilities are frequently stale or incorrect, forcing developers to debug at the provider configuration level.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

**Qwen Code Community Digest — 2026-06-14**

---

### 1. Today's Highlights

Activity this week centers on interoperability and core reliability. A draft PR to decouple the provider identity from the SDK protocol (#5089) paves the way for custom provider support, while a new `/import-config` command (#5095) directly addresses community demand for smoother Claude Code migration. On the user-facing side, long-context performance degradation remains the hottest topic, with several reports (#5018, #5019) describing repetitive tool calls and attention loss in lengthy sessions. A nightly release workflow also broke today (#5092), prompting immediate attention.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Hot Issues

1. **[#3203](https://github.com/QwenLM/qwen-code/issues/3203) – OAuth Free Tier Policy Adjustment** (129 comments)  
   Proposes carving the free tier from 1,000 requests/day to 100, with an eventual phase-out. The explosive comment count signals strong community pushback and concern over access changes for casual users.

2. **[#5083](https://github.com/QwenLM/qwen-code/issues/5083) – TUI freezes due to zombie subprocesses** (5 comments)  
   A critical bug: the TUI becomes completely unresponsive when bash child processes go zombie (Z state) and are never reaped. Requires a force-kill and undermines trust in session stability.

3. **[#5090](https://github.com/QwenLM/qwen-code/issues/5090) – Refactor: Decouple Provider Identity from SDK Protocol** (3 comments, in-review)  
   Proposes making `providerId` a free-form string and introducing a `Protocol` enum (`OPENAI | GEMINI | ANTHROPIC | QWEN_OAUTH`) for explicit SDK routing. A foundational step toward arbitrary provider support.

4. **[#5055](https://github.com/QwenLM/qwen-code/issues/5055) – Trojan:JS/ShaiWorm.DBA!MTB False Positive** (4 comments)  
   The Windows VSIX triggers Windows Defender. Erodes trust in the official distribution channel and blocks adoption in security-sensitive environments.

5. **[#5018](https://github.com/QwenLM/qwen-code/issues/5018) – Long-context attention loss / forgetting** (4 comments)  
   Users report severe performance degradation in long sessions, with the model “forgetting” earlier context. A top UX complaint affecting complex, multi-step tasks.

6. **[#5019](https://github.com/QwenLM/qwen-code/issues/5019) – Repetitive tool calls causing session termination** (3 comments)  
   The same tool is called with identical arguments across consecutive rounds, triggering a hard stop from the API. Directly related to the long-context badcase.

7. **[#5080](https://github.com/QwenLM/qwen-code/issues/5080) – Standard API Key vs Token Plan provider conflict** (4 comments)  
   Switching between `[ModelStudio Token Plan]` and standard auth leads to unexpected 401 errors when the wrong connection method is cached in the provider list.

8. **[#4845](https://github.com/QwenLM/qwen-code/issues/4845) – Feature Request: /import-config for Claude migration** (4 comments)  
   A “one-click import” tool to bring MCP servers, instructions, and custom commands over from Claude Code and Claude Desktop. Strong community signal for lowering switching costs.

9. **[#5064](https://github.com/QwenLM/qwen-code/issues/5064) – Status line overflow/wrapping** (3 comments, welcome-pr)  
   Long status text is hidden or overlapped in the TUI footer. Tagged as a good first contributor issue.

10. **[#5092](https://github.com/QwenLM/qwen-code/issues/5092) – Nightly Release Workflow Failure (v0.18.0-nightly)** (0 comments)  
    Automated CI run for today’s nightly build failed. Users tracking `main` are currently blocked from receiving the latest build.

---

### 4. Key PR Progress

1. **[PR #5095](https://github.com/QwenLM/qwen-code/pull/5095) – `/import-config` for Claude MCP servers** (OPEN)  
   Imports MCP settings from Claude Code (user/project) and Claude Desktop into Qwen Code settings. Skips reserved names and reports malformed files. Directly answers the call for smoother interop.

2. **[PR #5089](https://github.com/QwenLM/qwen-code/pull/5089) – Extract `Protocol` enum, decouple model identity** (OPEN, draft)  
   The implementation side of Issue #5090. Changes `AuthType` to `type AuthType = string` and introduces a `Protocol` enum for SDK routing, unblocking custom providers.

3. **[PR #5004](https://github.com/QwenLM/qwen-code/pull/5004) – Durable cron jobs (`/loop` survival)** (MERGED)  
   `/loop` tasks now persist across restarts by saving state under `~/.qwen/tmp/<project-hash>`. A major step into background automation.

4. **[PR #4914](https://github.com/QwenLM/qwen-code/pull/4914) – OOM prevention: idempotent compaction + explicit GC** (MERGED)  
   Regression tests for compacted tool groups and an explicit garbage-collection trigger. Essential for preventing memory leaks in long-lived sessions.

5. **[PR #5093](https://github.com/QwenLM/qwen-code/pull/5093) – Wrap long status lines** (OPEN)  
   Caps rendered status lines at `MAX_STATUS_LINES` and wraps content instead of truncating. Resolves Issue #5064.

6. **[PR #5088](https://github.com/QwenLM/qwen-code/pull/5088) – Web-shell: full tool detail + auto-collapse** (MERGED)  
   Replaces the 120-character hard cap on tool descriptions in the web-shell and auto-collapses finished tool calls to keep the transcript readable.

7. **[PR #5036](https://github.com/QwenLM/qwen-code/pull/5036) – Hard-stop repeated identical tool calls** (OPEN)  
   Moves loop detection from the TUI hook into the core stream loop via `LoopDetectionService`. A direct fix for the repetition pattern reported in Issue #5019.

8. **[PR #4933](https://github.com/QwenLM/qwen-code/pull/4933) – Config file change detection via chokidar** (OPEN)  
   Watches Qwen settings files for external edits and applies them live. Removes the need for manual reload or restart after editing `~/.qwen/settings.json`.

9. **[PR #5034](https://github.com/QwenLM/qwen-code/pull/5034) – Workflow P3: agent options (schema, type, model, isolation)** (MERGED)  
   The third phase of the Dynamic Workflows port. Adds per-call `agent()` options that complete the dispatch contract matching upstream Claude Code 2.1.168.

10. **[PR #5051](https://github.com/QwenLM/qwen-code/pull/5051) – Computer Use: migrate from `ocu` to `cua-driver-rs`** (MERGED)  
    Swaps the Node.js open-computer-use backend for a Rust driver (`trycua/cua`). Brings cross-platform support and no-focus-stealing native automation.

---

### 5. Feature Request Trends

- **Interoperability & Migration (Priority: High)**  
  The strongest signal is the desire to reduce switching costs between AI coding tools. The `/import-config` command (#4845) and the Dynamic Workflows port (#4721) are direct responses to developers migrating from or evaluating against Claude Code.

- **Background & Persistent Automation (Priority: Medium-High)**  
  Durable cron jobs (#5004), persistent file-history snapshots (#4204), and persistent session management (#5074) show the community expects Qwen Code to handle long-running, unattended agent workflows without losing state.

- **Provider Extensibility (Priority: Medium)**  
  The decoupling of provider identity from SDK protocol (#5089/5090) indicates growing demand for BYO-model flexibility, reducing dependency on a hard-coded provider list.

---

### 6. Developer Pain Points

- **Long-Context Model Degradation**  
  The #1 user-facing quality issue. Reports (#5018, #5019, #5029) describe forgetfulness, repetitive tool calls that force session termination, and an overall “dumbing down” effect in long sessions. Users view this as a critical blocker for complex tasks.

- **UI Stability and Hangs**  
  The TUI freezing from zombie subprocesses (#5083), missing plan summaries on exit (#5075), and overlapping/fragmenting status lines (#5064) create frequent context-switching and frustration during hands-on development.

- **Authentication & Configuration Friction**  
  Confusion between Standard API Keys and Token Plan access points (#5080) leads to hard-to-diagnose 401 errors. The proposed free-tier cut (#3203) also threatens to alienate hobbyist / evaluation users.

- **Platform-Specific Gaps**  
  Linux SSH users lack clipboard support (#4926), and the Windows VSIX gets flagged as malware (#5055). These trust and accessibility gaps create barriers for specific user segments and enterprise environments.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-14

> **Note on naming:** The project is now officially rebranded to **CodeWhale** (repository `Hmbown/CodeWhale`), though the digest retains the legacy DeepSeek TUI handle.

---

## 1. Today's Highlights
The v0.8.60 development sprint is at its zenith, with the project's architecture pivoting decisively toward a multi-agent **"Agent Fleet"** control plane inspired by Cursor's cloud agent model. The core architectural debate centers on splitting sub-agents into a fully headless runtime with lightweight TUI projections (#3096) while defining formal role-based delegation policies for manager agents (#3167). A critical quality-of-life regression was also exposed—cost tracking is entirely dead for all non-DeepSeek models (#3066)—with a fix already landed in PR #3201. Meanwhile, persistent UX friction around the UI blocking during long-running verification tasks (#3200) and unreliable agent steering (#3203) signals that "reliability" is the dominant consumer pain point entering the final stretch of the release cycle.

---

## 2. Releases
No new releases in the last 24 hours. The project remains in an intense pre-release engineering phase for the v0.8.60 milestone.

---

## 3. Hot Issues

1. **[#3096 v0.8.60: Split sub-agents into a headless worker runtime with lightweight TUI projections](https://github.com/Hmbown/CodeWhale/issues/3096)**
   The defining architectural debate for the current cycle. Proposes moving sub-agents from in-process async tasks to a decoupled headless runtime. The community discussion (6 comments) weighs the scalability benefits for fan-out workloads against the operational complexity of managing an external process tree.

2. **[#3154 EPIC: Agent Fleet control plane for always-running verifiable work](https://github.com/Hmbown/CodeWhale/issues/3154)**
   The master tracking issue for v0.8.60's central feature. Defines the vision of CodeWhale as a persistent control plane managing many background worker agents, turning scarce maintainer attention into a coordination problem. Essential reading for understanding the project's direction.

3. **[#3167 Model the Agent Fleet org chart, roles, and delegation policy](https://github.com/Hmbown/CodeWhale/issues/3167)**
   A deep design discussion on moving beyond symmetrical child agents. Proposes formal roles (scouts, implementers, verifiers, operators) so the manager agent doesn't reinvent delegation logic every turn. Critical scaffolding for non-trivial fleet orchestration.

4. **[#3066 Cost tracking is dead for all non-DeepSeek models](https://github.com/Hmbown/CodeWhale/issues/3066)**
   A high-severity regression. The `pricing_for_model` function in `crates/tui/src/pricing.rs` returns `None` for every provider except DeepSeek and Xiaomi MiMo, breaking turn/session cost lines, cache-savings readouts, and background accrual for Kimi, Qwen, GLM, OpenAI, Arcee, and OpenRouter users.

5. **[#3205 Add route-effective model inventory and auto fleet model selector](https://github.com/Hmbown/CodeWhale/issues/3205)**
   Exposes a practical scaling bottleneck: the current `auto`/default model behavior is too shallow for a multi-provider fleet. Live testing with Z.ai/GLM routes demonstrated that a single default model cannot serve role-specific workers or multiple OAuth/CLI routes.

6. **[#3200 Make long-running shell and verifier work truly non-blocking](https://github.com/Hmbown/CodeWhale/issues/3200)**
   A core reliability complaint. Direct user observation showed the TUI feeling blocked after dispatching background work like `cargo check` or `cargo test`, undermining the entire background execution value proposition.

7. **[#3203 Make queued steering reliable and add Ctrl+S send](https://github.com/Hmbown/CodeWhale/issues/3203)**
   A fundamental UX interaction bug. Cmd+Enter frequently fails to submit steering messages while the model or child workers are busy. The explicit request for Ctrl+S as a dedicated "send queued steering" shortcut indicates a desire for a more robust, keyboard-centric interaction model.

8. **[#2982 Clearly display busy or free](https://github.com/Hmbown/CodeWhale/issues/2982)**
   Simple but telling UX signal. Users report that without changing text, it's impossible to distinguish "task finished" from "still thinking." Proposes traffic-light color blocks—a basic state visibility gap in a tool designed for autonomous background work.

9. **[#3204 Correct model context-window metadata and preflight over-limit requests](https://github.com/Hmbown/CodeWhale/issues/3204)**
   A reliability bug with high confusion cost. Live testing with GPT-5.5/Codex routes hit repeated `context_length_exceeded` errors while the TUI status line displayed incorrect context stats, eroding trust in the tool's feedback.

10. **[#3192 Put it up for agentclientprotocol/registry](https://github.com/Hmbown/CodeWhale/issues/3192)**
    A community-driven integration request to list CodeWhale in the ACP registry. Having a registry entry enables seamless installation and discovery from editors like Zed, widening the project's adoption surface beyond the Terminal.

---

## 4. Key PR Progress

1. **[#3206 WeChat Bridge using Feishu and Tencent OpenClaw](https://github.com/Hmbown/CodeWhale/pull/3206)**
   *Community* by **VincentCorleone**. Adds a full WeChat bridge reusing the existing Feishu bridge architecture. Extends CodeWhale's reach into the messaging ecosystem. (Open)

2. **[#3201 fix: revive cost tracking for non-DeepSeek models](https://github.com/Hmbown/CodeWhale/pull/3201)**
   *Core fix* by **mvanhorn**. Directly addresses #3066 by expanding the `pricing.rs` table. A critical quality-of-life patch for anyone running on providers other than DeepSeek. (Open)

3. **[#2808 feat(runtime-api): add session save, undo/retry, and snapshot endpoints](https://github.com/Hmbown/CodeWhale/pull/2808)**
   *Feature* by **gaord**. A substantial PR adding REST API endpoints for session persistence and undo/retry, enabling GUI frontends to reuse TUI session capabilities without reimplementing the runtime. (Open)

4. **[#3199 feat(runtime-api): add PUT /v1/sessions endpoint](https://github.com/Hmbown/CodeWhale/pull/3199)**
   *Feature* by **gaord**. A cleanly scoped slice of #2808, providing a single endpoint for saving a thread's live engine state as a named session. Demonstrates strong iterative engineering discipline. (Open)

5. **[#3197 Rename DeepSeek blue consumers to whale accent](https://github.com/Hmbown/CodeWhale/pull/3197)**
   *Cleanup* by **nightt5879**. Finalizes the visual rebranding from DeepSeek TUI to CodeWhale by migrating color tokens from `DEEPSEEK_BLUE` to `WHALE_ACCENT_PRIMARY`. Closes #3069. (Open)

6. **[#3196 Add Ctrl+P / Ctrl+N slash-command autocomplete navigation](https://github.com/Hmbown/CodeWhale/pull/3196)**
   *UX polish* by **1Git2Clone**. Adds keyboard shortcuts as alternatives to arrow keys for command autocomplete navigation, including a guard to prevent collision with the global file-picker. (Open)

7. **[#3195 fix(telegram): keep polling while turns stream](https://github.com/Hmbown/CodeWhale/pull/3195)**
   *Bug fix* by **cyq1017**. Fixes a concurrency issue where long-running streamed turns blocked the Telegram `getUpdates` polling loop, rendering the bridge unresponsive. Closes #2966. (Open)

8. **[#3193 Add config-gated Pro Plan routing profile](https://github.com/Hmbown/CodeWhale/pull/3193)**
   *Feature* by **dumbjack**. Reworks the Pro Plan feature as a config-gated routing profile (`pro_plan_profile = false` by default). Separates premium routing from the default mode/menu flow to avoid user confusion. (Open)

---

## 5. Feature Request Trends

The overwhelming direction is the transition of CodeWhale from a single-agent TUI into a **multi-agent orchestration platform**.

- **Agent Orchestration & Fleet Management:** The dominant theme. The community is deeply engaged in building an "Agent Fleet" control plane (#3096, #3154, #3167) with headless runtimes, role-based delegation (manager, scout, implementer, verifier), SSH-backed workers, and explicit security trust boundaries.
- **Multi-Model Ecosystem Maturity:** Users are pushing hard to make CodeWhale a first-class citizen for *any* provider. This manifests in demands for accurate cost tracking (#3066), dynamic per-role model selection (#3205), and correct context-window metadata (#3204).
- **Standardized Protocol Integration:** Community requests for ACP registry listing (#3192, #1447) and the existing ACP/agent-to-agent protocol development signal a desire for CodeWhale to be a recognized, interoperable component in the broader AI tooling ecosystem.
- **External AI Bridges:** The addition of bridges for WeChat (#3206), Feishu, and Telegram (#3195) suggests an emerging pattern of using CodeWhale as a headless AI backend for messaging platforms, not just a standalone TUI.

---

## 6. Developer Pain Points

- **"Reliability" as a Meta-Pain Point:** The `reliability` tag is the most heavily recurring label. Users are hitting context-window errors with misleading UI feedback (#3204), the TUI blocks on dispatched background tasks (#3200), and queued steering is flaky under load (#3203).
- **Non-DeepSeek Feature Drop-off:** Using CodeWhale with OpenAI, Qwen, GLM, or other providers results in a visibly degraded experience where core QoL features like cost tracking, cache readouts, and model metadata break completely. This is the single biggest source of friction for the multi-model user base.
- **Basic Installation Failures:** The `cargo install codewhale-tui` failure (#3198) represents a fundamental barrier to entry that directly impacts community growth and first-run impressions.
- **State Visibility & Discoverability:** Users cannot reliably tell whether the agent is busy or idle (#2982). Hidden shortcuts are poorly surfaced (#3194). CLI model routing disagrees with the live runtime (#3202), forcing users into a trial-and-error configuration workflow.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*