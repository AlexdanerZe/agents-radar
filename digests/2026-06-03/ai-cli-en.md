# AI CLI Tools Community Digest 2026-06-03

> Generated: 2026-06-03 03:46 UTC | Tools covered: 9

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

# Cross-Tool Ecosystem Comparison Report: AI CLI Developer Tools
**Date:** 2026-06-03  
**Role:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tools landscape on June 3, 2026, reveals a sector hurtling toward production maturity while grappling with the inherent instability of emergent infrastructure. Every major tool chain shipped meaningful updates in the past 24 hours—Claude Code deployed enterprise-grade OpenTelemetry, Copilot CLI launched its `/voice` command, and CodeWhale completed its rebrand—yet community discourse is overwhelmingly dominated by regressions in billing logic, authentication deadlocks, agent loop reliability, and cross-platform fragility, particularly on Windows. The industry is clearly exiting the “demo-ready” phase: users are no longer impressed by capability alone and are now demanding deterministic behavior, billing transparency, configuration sovereignty, and robust security models as a baseline. The competitive divergence is sharpening along two axes: **enterprise-grade infrastructure** (auth, observability, SSO, platform parity) versus **ecosystem extensibility** (multi-provider resilience, MCP tooling, open plugin ecosystems).

---

## 2. Activity Comparison

| Tool | Releases (24h) | PR Velocity (24h) | Top Issue Engagement | Primary Strategic Theme |
|---|---|---|---|---|
| **Claude Code** | v2.1.161 | Low (3 PRs) | #38335 (761 comments, 461 👍) | Enterprise scaling / Billing transparency crisis |
| **OpenAI Codex** | rust-v0.137.0-alpha.4 | Very High (10+ PRs) | #20161 (190 comments, 120 👍) | Auth infrastructure / Rust platform rebuild |
| **Gemini CLI** | v0.46.0-preview.0, v0.45.0 | High (10 PRs) | #21409 (8 👍) | Agent orchestration / Terminal performance |
| **Copilot CLI** | v1.0.58, v1.0.59 | None (0 PRs) | #1703 (28 comments, 54 👍) | Feature velocity / Model parity friction |
| **OpenCode** | None | High (10 PRs) | #20695 (87 comments, 61 👍) | Provider ecosystem cost / Memory stability |
| **Pi (pi-mono)** | None | High (10 PRs) | #5223 (11 comments, 5 👍) | Regional provider expansion / Protocol resilience |
| **Qwen Code** | v0.17.0-preview.0 | High (10 PRs) | #4663 (8 comments) | Local model ergonomics / MCP security |
| **DeepSeek TUI (CodeWhale)** | v0.8.50, v0.8.51 | High (10 PRs) | #2487 (12 comments) | Post-rebrand engine stability / OSS velocity |
| **Kimi Code** | None | None | N/A | Dormant |

---

## 3. Shared Feature Directions

A clear set of convergent requirements emerged across multiple tool communities, representing the new baseline expectations for production-grade AI assistants:

- **Agent Orchestration Reliability** — Sub-agent workflows remain universally fragile. Users report silent hangs across **Gemini CLI** (#21409, #25166), **CodeWhale** (#2487, #2583), and context corruption in multi-agent flows in **Claude Code** (#37793, #63015). The demand for deterministic circuit breakers, progress visibility, and false-positive termination detection is shared across all platforms.

- **MCP Security & Scalability** — The conversation has shifted from "how to enable MCP" to "how to manage MCP in production." Project-scoped `.mcp.json` with approval gating is being implemented simultaneously in **Qwen Code** (#4615, #4713) and **Pi** (#5332). **Gemini CLI** reports hard ceiling errors (>128 tools, #24246), while **Copilot CLI** faces registry discovery bugs (#3436). All communities need intermediate management layers for tool density and trust.

- **Configuration Sovereignty Over "Auto-Magic"** — A strong cross-community pushback against opaque AI-driven defaults is evident. **Qwen Code** users demand the ability to disable auto-generated skills (#4714) and configure timeouts (#4711). **Gemini CLI** users report `settings.json` overrides being silently ignored (#22267). **OpenCode** explicitly rejects "just swap LLMs" suggestions for memory bloat (#20695). Developers want explicit knobs, not invisible decisioning.

- **Comprehensive Persistence & Memory** — State management across session boundaries is the deepest shared technical challenge. **Claude Code** leads the request signal for session portability and skill sync (#20697, #64721). **Codex** suffers compaction dropping AGENTS rules (#25792). **Gemini CLI**'s Auto Memory is pushing toward deterministic, secure transcript extraction (#26525). The "memory wall" remains unsolved by all.

- **Platform Parity (Windows & CJK)** — Windows stability is a universal pain point spanning install failures (**Codex**, **Copilot**), shell spawning errors (**Copilot** #2355, **CodeWhale** #2523, **Pi** #5103), and CJK IME rendering breaks (**Copilot** #3045, #3536, **Pi** #5326, **Qwen Code** #4652). No tool has solved this comprehensively, making it the single largest shared blocker for enterprise adoption.

---

## 4. Differentiation Analysis

The tools are diverging sharply in strategic focus, target persona, and architectural philosophy:

- **Claude Code** optimizes for the **enterprise team lead**. Its investment in OpenTelemetry, agent task visibility, Cowork workflows, and Max plan billing signals a product designed to be sold to engineering managers who need cost attribution, team-level guardrails, and scalable parallel execution. The billing crisis (#38335) is existential for this strategy.

- **OpenAI Codex** is building **enterprise infrastructure**. The massive multi-PR stack for HTTP state management, auth hooks, and multi-account profiles, combined with the Rust core migration, signals a long-term bet on deeply secure, scalable desktop client infrastructure for large organizations. Current auth deadlocks (#25749) are a critical misstep.

- **Gemini CLI** differentiates on **agent-centric orchestration and terminal performance**. The focus on a generalist agent, Auto-Memory, and VirtualizedList performance work targets developers who prioritize autonomous execution and local responsiveness. The "get-shit-done" workflow and AST-aware manipulation requests are unique.

- **Copilot CLI** is deepening its **VS Code ecosystem moat** while pursuing **new interaction modalities** (voice, scheduling, theming). Its rapid feature velocity targets the everyday GitHub developer, but the friction from model parity gaps (#1703) and UI churn (#2205) suggests velocity is outpacing quality assurance.

- **OpenCode** serves as the **universalist's Swiss Army knife**. With the widest provider support and advanced multi-agent TUI ergonomics (backgrounding subagents, skill autocomplete), it targets sophisticated developers optimizing across cost, latency, and model choice. Memory bloat (#20695) is its most critical vulnerability.

- **Pi** and **Qwen Code** are becoming **regional and niche leaders**. Pi excels as the hyper-configurable Node.js client, rapidly onboarding Chinese cloud providers (ZAI, Ant-ling, MiniMax) and building sophisticated security models (workspace approval). Qwen Code balances deep local model integration with IDE-grade terminal UX (VIM mode, IME support).

- **DeepSeek TUI (CodeWhale)** is the **open-source community powerhouse**. Its 10 high-quality daily PRs and rapid feature adoption demonstrate exceptional contributor momentum, but post-rebrand engine instability (#2487, #2583) highlights the fragility of OSS velocity.

---

## 5. Community Momentum & Maturity

| Tier | Tool | Assessment |
|---|---|---|
| **Established Leaders** | **Claude Code**, **Copilot CLI** | Highest mindshare and feature velocity. Community discourse centers on *optimizing and scaling* mature features, not requesting basics. Expectations are high, and regressions generate intense backlash proportionate to market position. |
| **Rapidly Iterating Contenders** | **Gemini CLI**, **OpenCode**, **Pi**, **Qwen Code** | Very high PR throughput with deeply technical contributor bases. These projects are driving the most architectural innovation—new providers, memory architectures, security models. Less battle-tested at scale, but velocity is their defining advantage. |
| **Transitioning / Recalibrating** | **OpenAI Codex**, **CodeWhale** | High technical ambition (Codex Rust rewrite, CodeWhale rebrand) paying the tax of transition. Communities show high engagement and tolerance for instability, but immediate reliability is the prerequisite for reclaiming momentum in their respective niches. |
| **Dormant** | **Kimi Code** | No activity in 24 hours. |

---

## 6. Trend Signals

- **The "Enterprise Check" is the New API Key.** Handling SSO (FIDO2, MFA), operating behind VPNs, providing cost attribution (OTEL, granular billing), and passing security audits (SSRF protection, MCP trust) is no longer optional. Every tool is racing to satisfy enterprise security requirements, creating a sharp divide between "demo-ready" and "deployment-ready."

- **Windows is the Critical Battleground, Not a Secondary Market.** The persistent, high-velocity stream of Windows-specific regressions—clipboard failures, shell spawning, IME flickering—represents systemic underinvestment. The tool that solves Windows stability comprehensively will capture a massive, underserved developer segment.

- **From "Provider Agnostic" to "Provider Resilient."** The fantasy of a universal, stable API abstraction is dead. The volume of provider-specific breakages this week alone—OpenAI server errors, Azure param regressions, MiniMax role fields, Anthropic thinking block failures—demonstrates that multi-provider tools must invest heavily in adapter-layer resilience, diagnostics, and automatic fallback chains.

- **Memory is the Next Frontier of Agentic Compute.** The intense focus on context compaction, auto-memory, session portability, and skill sync signals that the industry has hit a hard wall with stateless, fixed-window LLMs. The tools that solve hierarchical memory, deterministic state management, and secure long-term recall will unlock a new class of autonomous capability.

- **Configurability is the Antidote to Hallucination.** A decisive cross-ecosystem shift is underway: users are rejecting "AI does it all" defaults in favor of explicit, predictable configuration (VIM modes, timeout controls, toggleable auto-skills). This represents a maturation from viewing AI as a magic black box to treating it as controllable, auditable infrastructure.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the latest anthropics/skills activity.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-06-03)

### 1. Top Skills Ranking
The following PRs represent the most-discussed Skill submissions by community engagement:

1.  **[document-typography (#514)](https://github.com/anthropics/skills/pull/514) (Open)** — A precision skill for fixing typographic artifacts in AI-generated documents (orphan words, widow paragraphs, number alignment). Highly practical for reducing visible "AI tells" in long-form output.
2.  **[ODT Skill (#486)](https://github.com/anthropics/skills/pull/486) (Open)** — Enables creation, templating, and conversion of OpenDocument Format (.odt/.ods). Discussion highlights enterprise compliance requirements for LibreOffice/OpenOffice ecosystems.
3.  **[Frontend-Design Clarity (#210)](https://github.com/anthropics/skills/pull/210) (Open)** — An internal revision of the existing frontend-design skill for better actionability and specific UI pattern application rather than generic guidance.
4.  **[Skill Quality & Security Analyzers (#83)](https://github.com/anthropics/skills/pull/83) (Open)** — Two meta-skills for auditing other skills across structure, documentation, quality, and security dimensions. Heavy influence on long-term ecosystem trust.
5.  **[Agent-Creator Meta-Skill (#1140)](https://github.com/anthropics/skills/pull/1140) (Open)** — Introduces an `agent-creator` meta-skill for building task-specific agent sets. Includes critical fixes for multi-tool evaluation and Windows path resolution. Highly topical.
6.  **[Testing-Patterns Skill (#723)](https://github.com/anthropics/skills/pull/723) (Open)** — A comprehensive testing skill covering the Testing Trophy model, unit patterns, React Testing Library, and edge cases. Fills a major standardization gap for AI-generated tests.
7.  **[ServiceNow Platform Skill (#568)](https://github.com/anthropics/skills/pull/568) (Open)** — A broad enterprise skill covering ITSM, ITOM, SecOps, ITAM/SAM, and IntegrationHub. Represents a trend towards deep platform-native skills over narrow scripting helpers.
8.  **[Shodh-Memory Skill (#154)](https://github.com/anthropics/skills/pull/154) (Open)** — Persistent context system for AI agents using proactive retrieval and structured memory records. Addresses the fundamental UX gap of conversational context loss.

### 2. Community Demand Trends
Analysis of the highest-engagement Issues reveals these pressing needs:

- **Enterprise Governance & Sharing:** Issue [#228](https://github.com/anthropics/skills/issues/228) (13 comments) requesting org-wide skill libraries and [#492](https://github.com/anthropics/skills/issues/492) (7 comments) raising namespace trust-boundary concerns signal urgent demand for enterprise controls.
- **Tooling Stability & Reliability:** Skill disappearance bugs ([#62](https://github.com/anthropics/skills/issues/62), 10 comments), a broken evaluation pipeline ([#556](https://github.com/anthropics/skills/issues/556), 9 comments), and duplicate plugin installations ([#189](https://github.com/anthropics/skills/issues/189), 6 comments) indicate that community confidence depends on hardening the skill tooling itself.
- **Interoperability & Extensibility:** Demands to expose Skills as MCPs ([#16](https://github.com/anthropics/skills/issues/16)), concerns over MCP data overflow ([#1102](https://github.com/anthropics/skills/issues/1102)), and proposals for agent governance patterns ([#412](https://github.com/anthropics/skills/issues/412)) suggest the community views Skills as a unified layer for future agent ecosystems.
- **Skill Developer Experience (DX):** The multi-file preload request ([#1220](https://github.com/anthropics/skills/issues/1220)) and criticism of the skill-creator’s educational tone ([#202](https://github.com/anthropics/skills/issues/202)) point to Skills becoming a professional authoring discipline.

### 3. High-Potential Pending Skills
The following open PRs show strong velocity and impact potential:

- **[Testing Patterns (#723)](https://github.com/anthropics/skills/pull/723)** and **[Shodh-Memory (#154)](https://github.com/anthropics/skills/pull/154)** remain the most conceptually ambitious open Skills, filling gaps in developer testing practice and agentic memory.
- **[Agent-Creator (#1140)](https://github.com/anthropics/skills/pull/1140) (Updated Jun 2)** is highly current and addresses critical meta-needs for managing multi-agent complexity.
- **Cross-Platform Universality:** A strong cluster of Windows compatibility fixes ([#1050](https://github.com/anthropics/skills/pull/1050), [#1099](https://github.com/anthropics/skills/pull/1099)) and case-sensitivity corrections ([#538](https://github.com/anthropics/skills/pull/538), [#539](https://github.com/anthropics/skills/pull/539), [#541](https://github.com/anthropics/skills/pull/541)) suggest a push for the platform to function reliably outside macOS/Linux pipelines.
- **[Sensory Skill (#806)](https://github.com/anthropics/skills/pull/806)** — AppleScript macOS automation. Represents demand for "native-first" tooling that uses OS-native capabilities rather than generic screenshot-based computer use.
- **[UTF-8 Panic Fix (#362)](https://github.com/anthropics/skills/pull/362) (Updated Jun 1)** — A critical bug fix for multi-byte character handling in skill-creator scripts; recent activity suggests imminent merge.

### 4. Skills Ecosystem Insight
The community's most concentrated demand has evolved from submitting isolated workflow skills to demanding a **governed, reliable, and interoperable agent platform**, prioritizing enterprise scalability (sharing controls, namespace security), tooling maturity (evaluation pipelines, creator DX), and persistent agentic infrastructure (memory, agent creation, cross-platform stability).

---

# Claude Code Community Digest — 2026-06-03

## 1. Today’s Highlights
Version 2.1.161 landed with enhanced OpenTelemetry support for team-level observability and richer progress reporting in agent views. Community energy remains concentrated on a cluster of model reliability bugs—particularly recurring tool-call parse failures and unexpected billing gates during compaction—while feature requests for cross-platform parity and session portability continue to accumulate significant traction.

---

## 2. Releases

**v2.1.161** ([Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.161))

- **OTEL Resource Attributes**: `OTEL_RESOURCE_ATTRIBUTES` are now exported as labels on metric datapoints, allowing teams to slice usage data by custom dimensions (e.g., team, repo). A meaningful step for engineering orgs trying to attribute cost and latency.
- **Agent Task Visibility**: Agent rows now display `done/total` before the detail column when work is fanned out; peek shows the longest-running item, improving debuggability of parallel agentic workflows.

---

## 3. Hot Issues

*Issues selected for community engagement, severity, and signal value.*

1. **#38335 — Max Plan session limits exhausted abnormally fast** ([Issue](https://github.com/anthropics/claude-code/issues/38335))  
   761 comments, 461 👍. The highest-traffic active issue. Max subscribers report hitting billing gates weeks ahead of expected thresholds. Community sentiment suggests a silent regression in token accounting or throttle logic. *Signal: Urgent, highly widespread.*

2. **#62123 / #63875 — Model’s tool call could not be parsed (Opus 4.7)** ([Issue](https://github.com/anthropics/claude-code/issues/62123), [Issue](https://github.com/anthropics/claude-code/issues/63875))  
   Combined 66 comments, 92 👍. A cross-platform (macOS, Windows, VS Code) parse failure that kills in-progress sessions. Multiple independent reports confirm sustained reproducibility. *Signal: Emerging regression, blocks all progress.*

3. **#20697 — Sync Skills between Desktop and CLI** ([Issue](https://github.com/anthropics/claude-code/issues/20697))  
   28 comments, 99 👍. The top feature request by reaction count. Users want a unified skill registry that spans Claude Desktop and Claude Code CLI, treating skills as a single source of truth.

4. **#63896 — Compaction fails: “Usage credits required for 1M context”** ([Issue](https://github.com/anthropics/claude-code/issues/63896))  
   22 comments, 11 👍. Context compaction on Max subscribers is hitting billing authorization failures, killing long sessions. Suggests a mismatch between plan tier detection and the API request path.

5. **#37793 — Sub-agents fail with prompt too long (many MCP servers)** ([Issue](https://github.com/anthropics/claude-code/issues/37793))  
   21 comments, 23 👍. Users with extensive MCP configurations are completely blocked from using Explore/Plan sub-agents—tool definitions alone exceed the 200K token ceiling.

6. **#63015 — Auto-compact never triggers at 100% context** ([Issue](https://github.com/anthropics/claude-code/issues/63015))  
   16 comments, 12 👍. Regression in v2.1.153. Statusline reports full context but compaction never fires, rendering the session unsustainable. *Signal: Core loop defect.*

7. **#61927 — “PR status couldn’t be checked” banner on every session** ([Issue](https://github.com/anthropics/claude-code/issues/61927))  
   4 comments, 4 👍. A persistent red warning banner floods the UI for worktree branches without an open PR. Minor individually, but symptomatic of noisy default behaviors in the Cowork workflow.

8. **#59628 — Worktree sessions can edit parent checkout** ([Issue](https://github.com/anthropics/claude-code/issues/59628))  
   5 comments. The system announces the worktree context but does not guardrail `Edit`/`Write` tools against modifying files in the parent checkout. *Signal: Safety/fidelity concern.*

9. **#57947 — Agent emits fabricated input-shape content** ([Issue](https://github.com/anthropics/claude-code/issues/57947))  
   3 comments. Under sustained multi-agent load, the model hallucinates Human prefixes, system-reminder tags, and teammate-message blocks into its own assistant turn. Subtle but concerning for agent chains.

10. **#64939 — Desktop Settings hangs on stale model ID** ([Issue](https://github.com/anthropics/claude-code/issues/64939))  
    2 comments. Opening Settings after a model retirement freezes the renderer indefinitely. A sharp UX failure for a core navigation surface.

---

## 4. Key PR Progress

*Only three PRs were active in the last 24 hours, indicating a quieter contribution cycle.*

1. **#64857 — Restrict symlink following in extensibility.py** ([PR](https://github.com/anthropics/claude-code/pull/64857))  
   Fixes a security edge case where GUI-related project-controlled paths could traverse symlinks. Closes #64582.

2. **#64728 — Remove stale statsig.anthropic.com from devcontainer firewall** ([PR](https://github.com/anthropics/claude-code/pull/64728))  
   The devcontainer `init-firewall.sh` script failed on resolution of a retired DNS record. This PR unblocks new contributor onboarding.

3. **#62821 (Merged) — Docs: env-bridge workaround for plugin-MCP session-id** ([PR](https://github.com/anthropics/claude-code/pull/62821))  
   Official documentation for the community-adopted workaround that passes `CLAUDE_CODE_SESSION_ID` to plugin stdio MCP servers. No code changes, but formalizes a widely-needed pattern while #61752 remains open.

---

## 5. Feature Request Trends

*Persistent cross-cutting themes from recent issues:*

- **Session Portability & State**: Users strongly request syncing Skills between Desktop and CLI (#20697), archiving instead of deleting agent sessions (#61978), exporting sessions to prevent data loss on reinstall (#64721), and avoiding re-discovery of previously solved problems (#64729). The thread is a demand for persistent, transferable agent memory.
- **Windows Feature Parity**: Calls for Windows-native Computer Use (#64381), Dev Container support (#64926), and stabilization of Cowork connectors (#61682, #64867) underscore a clear gap in platform maturity.
- **Agent Orchestration**: First-class structured orchestration (#64767) and deterministic automation paths (#58933) signal a shift from interactive prompting toward production-grade, reproducible agent pipelines.
- **MCP Ecosystem Scaling**: Sub-agents losing parent MCP tool registries (#64909) and context-limit ceilings hitting multi-server setups (#37793) are the top friction points for advanced MCP users.

---

## 6. Developer Pain Points

- **Billing & Context Ambiguity**: The most acute pain point. Users on Max plans face "Usage credits required" errors during compaction (#63896) and session limit exhaustion (#38335) without clear feedback on what consumed credits. The opacity of the metering system erodes trust in plan boundaries.
- **Model Reliability Degradation**: Tool-call parse failures (#62123, #63875) and drift from `CLAUDE.md` instructions (#64859) plague long-lived sessions. Developers report that agentic workflows become brittle after extended context accumulation, undermining the value of auto-compaction.
- **Windows Fragility**: Worktree safety guardrails (#59628), Hyper-V/VM creation failures (#64867), and spurious PR banners (#61927) combine to make the Windows experience feel like a lower-priority surface despite growing adoption.
- **UI Noise and Blocking**: Persistent error banners (#61927), input-loop hangs during paste events (#64935), and autocomplete failures on filenames with spaces (#64932) introduce friction that breaks flow—minor individually, but cumulatively damaging to daily trust.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

OpenAI Codex Community Digest — 2026-06-03

---

### Today's Highlights
An escalating authentication crisis dominates the tracker today, with multiple issues detailing phone verification deadlocks (#25749) and FIDO2/SMS MFA conflicts specifically in the CLI (#25737). Windows stability remains a major concern, with fresh installs failing outright for some users (#25489). On the engineering side, a major multi-PR infrastructure stack for per-surface HTTP state and auth hooks landed, alongside security fixes for git worktree trust resolution.

---

### Releases
- **[rust-v0.137.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.137.0-alpha.4):** Nightly Rust CLI build pushed; no detailed changelog provided in the release body.

---

### Hot Issues

1. **[#25749](https://github.com/openai/codex/issues/25749) — Inaccessible legacy phone number recovery** (25 comments, 12 👍)
   Users with valid MFA are trapped in a phone verification loop for a number they no longer own, with no alternative recovery path provided. Critical UX/trust failure.

2. **[#25737](https://github.com/openai/codex/issues/25737) — CLI login forces SMS OTP despite hardware security key** (7 comments, 5 👍)
   Users relying exclusively on FIDO2 keys are forced into a phone OTP step-up during `codex login`. The browser flow correctly honors Advanced Account Security, making this a client-side regression.

3. **[#20161](https://github.com/openai/codex/issues/20161) / [#20320](https://github.com/openai/codex/issues/20320) — Phone verification megathreads** (190 + 41 comments, 120 + 11 👍)
   The highest-traffic ongoing issues. Phone verification either fails silently or never sends a code, locking users out of Desktop/CLI while web access works fine.

4. **[#25203](https://github.com/openai/codex/issues/25203) — GitHub OAuth callback fails on Windows** (34 comments, 21 👍)
   Connecting GitHub from the Windows Desktop app fails with “Unable to find Electron app,” blocking core integration for Windows developers.

5. **[#25489](https://github.com/openai/codex/issues/25489) — Windows clean install does not launch** (11 comments)
   Windows Desktop app fails to launch after a clean reinstall with errors indicating the Electron host or app-server is missing, raising distribution pipeline concerns.

6. **[#25792](https://github.com/openai/codex/issues/25792) — Context compaction forgets AGENTS rules** (7 comments)
   Severe long-task reliability bug: when the context window compacts automatically, custom AGENTS instructions are dropped, causing the model to regress (e.g., progress jumping from 97% back to 42%).

7. **[#18553](https://github.com/openai/codex/issues/18553) — Terminal font rendering still broken** (14 comments, 25 👍)
   Persistent cosmetic bug where terminal output in the Desktop app renders with excessive spacing. High community agreement on severity.

8. **[#20769](https://github.com/openai/codex/issues/20769) — Speed setting resets to Standard on restart** (13 comments, 11 👍)
   User preferences not persisting. The “Fast” model speed reverts to “Standard” every time the app restarts.

9. **[#25769](https://github.com/openai/codex/issues/25769) — Archiving a chat leaves UI stuck on broken thread** (7 comments, 2 👍)
   Archiving the currently viewed thread fails to navigate the UI away, resulting in a “session is archived” error toast — a clear state management bug.

10. **[#24098](https://github.com/openai/codex/issues/24098) / [#22428](https://github.com/openai/codex/issues/22428) — Windows Sandbox execution failures** (15 + 7 comments)
    Elevated Windows sandbox fails universally with “spawn setup refresh failed” or `CreateProcessAsUserW` errors after updates, while unelevated sandbox works. Severely impacting Windows CLI users.

---

### Key PR Progress

1. **[#25930-#25952](https://github.com/openai/codex/pulls?q=is%3Apr+25930) — Per-surface HTTP state & auth stack** (cooper-oai)
   Seven-PR stack adding a generic HTTP state store (`codex-http-state`), exposing it via app-server RPCs, and wiring URL-scoped auth hooks including WebSocket traffic. Foundational work for secure client requests.

2. **[#25383](https://github.com/openai/codex/pull/25383) / [#25469](https://github.com/openai/codex/pull/25469) — Multi-account profile switcher** (dhruvgupta-oai)
   Implements the `accountSession/*` protocol and app-server lifecycle for managing multiple accounts from the Desktop UI. A highly requested enterprise/power-user feature.

3. **[#26023](https://github.com/openai/codex/pull/26023) — Managed macOS sandbox capabilities** (gregyoung2)
   Adds typed macOS Seatbelt capabilities to managed permission profiles, improving the security model for macOS sandbox users.

4. **[#26020](https://github.com/openai/codex/pull/26020) / [#26021](https://github.com/openai/codex/pull/26021) — Git & migration security fixes** (viyatb-oai)
   Fixes trust resolution in linked worktrees and prevents overwrites of symlinked migration targets. These patches address potential supply-chain and data integrity vulnerabilities.

5. **[#26009](https://github.com/openai/codex/pull/26009) — Metadata-only thread subscriptions** (btraut-openai)
   Introduces lightweight catalog subscriptions for the sidebar, allowing it to react to changes without resuming every thread, improving app performance.

6. **[#26013](https://github.com/openai/codex/pull/26013) — CLI terminal visualization instructions** (vie-oai)
   Adds ASCII-only rendering instructions for shared visualizations in CLI/exec sessions, a welcome UX upgrade for terminal-only users.

7. **[#25688](https://github.com/openai/codex/pull/25688) — Per-app approval requirements** (zamoshchin-openai)
   Adds `allowed_approvals_reviewers` to managed app requirements, enabling finer-grained admin control over approval workflows.

8. **[#25232](https://github.com/openai/codex/pull/25232) — Window generation from rollout lineage** (ningyi-oai)
   Fixes `x-codex-window-id` semantics to correctly reflect rollbacks, resumes, and forks. Important for debugging and telemetry accuracy.

9. **[#19047-#19054](https://github.com/openai/codex/pulls?q=is%3Apr+19047) — HAI external-task-ref / Background agents** (adrian-openai)
   Long-running stack adding primitives for external task references and background agent identity, enabling deeper integration with external task management systems.

10. **[#26002](https://github.com/openai/codex/pull/26002) — Log plugin MCP server names** (chrisdong-oai)
    Improved plugin telemetry by including exact MCP server names in the relevant event, aiding debugging and usage analytics.

---

### Feature Request Trends
- **API Provider Flexibility:** The community continues to push for custom API endpoints and OpenRouter-style provider support (#14).
- **Usage Transparency:** Strong desire for a persistent rate-limit and usage display in the main UI rather than hidden in settings (#24182).
- **Reliable Remote Pairing:** Growing demand for stable iOS/macOS remote control, with multiple issues citing disconnections and pairing failures (#22773, #23078).
- **Context Integrity:** Users want guarantees that long-running agent sessions won't lose their instructions to context compaction (#25792).

---

### Developer Pain Points
- **Authentication Dead Ends:** Phone verification loops are the top friction point, locking users out of the platform entirely regardless of existing MFA.
- **Windows Instability:** From clean install failures to sandbox crashes and rendering glitches, Windows remains the most fragile platform for Codex Desktop.
- **State Management Decay:** Settings that refuse to persist (Speed, model preference) and UI desyncs when archiving or switching threads erode trust in the app's reliability.
- **Mobile/Remote Fragility:** Cross-device workflows are routinely broken by updates, leaving multi-device users without a stable remote control channel.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest
**Date:** June 3, 2026
**Data Source:** [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 🚀 Today's Highlights

The Gemini CLI shipped two releases today—v0.45.0 and v0.46.0-preview.0—with targeted fixes for PTY resize crashes and Termux compatibility. The PR queue is lively: a major VirtualizedList performance optimization is underway, the build system race condition in this monorepo is finally being tamed, and Gemini 3.5 Flash GA support is being wired into the model resolution layer. On the bug front, agent hangs and misleading sub-agent success states remain the highest-signal community pain points.

---

## 📦 Releases

Two versions landed in the last 24 hours:

- **[v0.46.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.0)** — Harden PTY resize handling against native crashes (by @scidomino). Includes automated changelog generation.
- **[v0.45.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.0)** — Fixes Termux relaunch and resize remount loops (by @saymanq). Changelog PR is actively awaiting review ([#27642](https://github.com/google-gemini/gemini-cli/pull/27642)).

---

## 🔥 Hot Issues (10 Most Noteworthy)

### 1. [#21409 - Generalist agent hangs (P1)](https://github.com/google-gemini/gemini-cli/issues/21409)
**8 👍 | 7 comments**
The top-voted open issue. The CLI freezes indefinitely whenever the generalist sub-agent is invoked—simple folder creation hangs for up to an hour. **Why it matters**: This is a show-stopper for default workflows. The community workaround (disabling sub-agents) is effective but unacceptable as a permanent solution.

### 2. [#25166 - Shell command stuck on "Waiting input" (P1)](https://github.com/google-gemini/gemini-cli/issues/25166)
**3 👍 | 4 comments**
After executing trivial shell commands, the CLI hangs with an "Awaiting user input" state even though the command finished. **Why it matters**: Core terminal lifecycle logic is breaking on common commands, eroding trust in the shell execution layer.

### 3. [#22323 - Subagent MAX_TURNS reported as GOAL success (P1)](https://github.com/google-gemini/gemini-cli/issues/22323)
**2 👍 | 6 comments**
Sub-agents (e.g., `codebase_investigator`) report `status: "success"` with `Termination Reason: "GOAL"` while internally having hit `MAX_TURNS` with zero analysis performed. **Why it matters**: Quiet failures in agent orchestration make debugging nearly impossible.

### 4. [#21983 - Browser subagent fails in Wayland (P1)](https://github.com/google-gemini/gemini-cli/issues/21983)
**1 👍 | 4 comments**
The browser sub-agent fails to initialize or complete on Wayland display servers. **Why it matters**: Linux developer uptake is hindered by a platform-specific rendering incompatibility.

### 5. [#21968 - Gemini doesn't use skills and sub-agents enough (P2)](https://github.com/google-gemini/gemini-cli/issues/21968)
**6 comments**
Despite having custom "gradle" or "git" skills registered, the model rarely invokes them autonomously. **Why it matters**: The primary value of custom agents and MCP tools is negated if the model ignores them.

### 6. [#20079 - Symlinked agents not recognized (P2)](https://github.com/google-gemini/gemini-cli/issues/20079)
**4 comments**
Agents placed as symlinks in `~/.gemini/agents/` are silently skipped. **Why it matters**: Breaks version management workflows and dotfile-based agent configuration.

### 7. [#26525 - Deterministic redaction for Auto Memory (P2)](https://github.com/google-gemini/gemini-cli/issues/26525)
**3 comments**
Auto Memory sends transcript content to the model *before* redaction instructions take effect, risking secret leakage. **Why it matters**: This is a security-sensitive architectural concern that needs on-device/pre-LLM redaction.

### 8. [#26522 - Auto Memory retrying low-signal sessions (P2)](https://github.com/google-gemini/gemini-cli/issues/26522)
**3 comments**
Low-signal sessions (where the extraction agent chooses not to read) remain unprocessed and get repeatedly surfaced. **Why it matters**: Wasted API calls and noise in the memory pipeline.

### 9. [#24246 - 400 error with > 128 tools (P2)](https://github.com/google-gemini/gemini-cli/issues/24246)
**3 comments**
Users with more than 128 enabled tools hit hard API errors. **Why it matters**: Power users extending the CLI with many MCP servers and custom agents hit a scalability wall.

### 10. [#22186 - get-shit-done output hook causes crash (P1)](https://github.com/google-gemini/gemini-cli/issues/22186)
**3 comments**
The user summary rendering at the end of a `get-shit-done` run crashes the entire CLI. **Why it matters**: Crashing at the finish line of a long-running task is deeply destructive to user trust.

---

## 🔧 Key PR Progress (10 Important PRs)

### 1. [#27645 - Respect backend definitions for 3.5 Flash](https://github.com/google-gemini/gemini-cli/pull/27645)
**New today.**
Updates model resolution to prioritize Gemini 3.5 Flash GA over the Flash Preview when feature flags are active. **Impact**: Directly unblocks early adopters from the latest model tier.

### 2. [#27636 - perf: optimize VirtualizedList and fix click handling (P1, XL)](https://github.com/google-gemini/gemini-cli/pull/27636)
**New today.**
Major deep-tissue work on the terminal rendering engine to fix flicker, scroll stuttering, and click handling for static history items. **Impact**: Targets the top terminal performance complaints.

### 3. [#27643 - fix(build): resolve parallel workspace compilation race condition](https://github.com/google-gemini/gemini-cli/pull/27643)
**New today.**
Splits the monorepo build into sequential topological stages (Core → Libraries → Apps). **Impact**: Eliminates flaky CI failures caused by concurrent dependency compilation.

### 4. [#27626 - fix(core): block private OAuth metadata URLs (P2, Security)](https://github.com/google-gemini/gemini-cli/pull/27626)
**Added yesterday.**
Prevents SSRF attacks during MCP OAuth metadata discovery by blocking private network URLs. **Impact**: Critical security hardening for the MCP integration layer.

### 5. [#27465 - fix(cli): surface extension disable/enable feedback (P2)](https://github.com/google-gemini/gemini-cli/pull/27465)
**Open, status/pr-nudge-sent.**
Routes extension enable/disable output to the terminal instead of silently writing to debug logs. **Impact**: Ends a baffling UX bug where `gemini extensions disable` appeared completely broken.

### 6. [#27572 - fix(cli): handle tmux false positive background detection](https://github.com/google-gemini/gemini-cli/pull/27572)
**Open.**
Fixes a regression where tmux (via mosh) causes the CLI to misdetect a white background, triggering wrong theme switching. **Impact**: Fixes theme reliability in common remote development setups.

### 7. [#27455 - feat(core): Add Amazon URL parsing and metadata extraction](https://github.com/google-gemini/gemini-cli/pull/27455)
**Open, status/pr-nudge-sent.**
Adds Amazon short URL resolution (`amzn.in`, `amzn.to`) and product metadata extraction to `web-fetch`. **Impact**: Enables a new class of shopping/comparison workflows.

### 8. [#27619 - fix(core): implement atomic update in MCP tool discovery](https://github.com/google-gemini/gemini-cli/pull/27619)
**Open.**
Retains the last known good tool list during transient MCP network failures. **Impact**: Eliminates "tool not found" errors from simple network glitches.

### 9. [#27292 - fix(cli): restore non-interactive stdin raw mode on exit](https://github.com/google-gemini/gemini-cli/pull/27292)
**Closed/merged.**
Ensures Ctrl+C cancellation in non-interactive mode properly restores terminal raw mode. **Impact**: Terminal state cleanup safety fix.

### 10. [#27287 - fix(cli): harmonize empty session lifecycle (P2)](https://github.com/google-gemini/gemini-cli/pull/27287)
**Closed/merged.**
Treats "empty" (metadata-only) sessions as valid but flagged, preventing false advertising for resumption or accidental deletion. **Impact**: Smoother session persistence and lifecycle management.

---

## 💡 Feature Request Trends

- **AST-Aware Code Manipulation** — A cohesive push across three issues (#22745, #22746, #22747) to adopt AST-aware file reads, AST grep, and codebase mapping. The goal is higher precision in edits and lower token waste from misaligned reads. *Why it matters:* Directly impacts agent code quality.
- **Autonomous Agent Orchestration** — Users want the model to intelligently decide *when* to use sub-agents and custom skills (#21968), understand its own capabilities and config flags (#21432), and avoid destructive git/database operations (#22672).
- **Memory System Maturity** — Auto Memory is under active development, with feature requests focusing on deterministic client-side redaction (#26525), handling malformed patches (#26523), and smarter retry/skip logic (#26522).
- **Remote Agent Ecosystem** — Epic #20303 tracks Sprint 2 of remote agents, focusing on task-level auth, first-party agent support, and background processing. The CLI is clearly expanding beyond a local-only tool.
- **Browser Agent Resilience** — Issue #22232 requests automatic session takeover and lock recovery to avoid "fail-fast" crashes in persistent browser sessions.

---

## ⚠️ Developer Pain Points

1.  **Agent Hangs & Silent Failures** — The CLI regularly hangs on sub-agent invocations (#21409, #25166) or reports a misleading `GOAL` success when it actually hit a turn limit (#22323). This erodes trust in agent-based workflows.
2.  **Terminal Instability** — Flicker on resize (#21924), corruption after external editors (#24935), misdetection in tmux (#27572), and Wayland incompatibility (#21983). Terminal UI polish remains a persistent friction area.
3.  **Configuration That Is Ignored** — Multiple reports that `settings.json` overrides (e.g., `maxTurns` for the browser agent) are silently ignored (#22267), or that sub-agents activate despite being disabled in config (#22093).
4.  **Scalability Ceilings** — Hard limits on tool count (400 error > 128 tools in #24246) and the model's tendency to ignore custom tools (#21968) block power users from building complex agent setups.
5.  **Auto Memory Noise & Security** — The memory extractor leaks data to the model before redaction (#26525), infinitely retries low-signal sessions (#26522), and silently skips malformed data (#26523).
6.  **Build & Dev Friction** — The monorepo build is prone to race conditions (#27643) and Node version alignment issues (#27255). The development experience itself can be fragile.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

Here is the GitHub Copilot CLI community digest for 2026-06-03.

---

## GitHub Copilot CLI Community Digest – 2026-06-03

### 1. Today’s Highlights
The team shipped two releases (v1.0.58 and v1.0.59), highlighted by the introduction of the `/voice` command for local speech-to-text dictation and the promotion of the experimental UI to default. Community reaction features a mix of enthusiasm for the rapid feature velocity and urgency around immediate regressions—particularly a Windows clipboard failure (#3622) and VPN blocks that prevent enterprise users from enabling the new voice feature (#3636).

### 2. Releases
* **[v1.0.59](https://github.com/github/copilot-cli/releases/tag/v1.0.59)** (2026-06-02) – Adds the `/voice` command, enabling dictation via local speech-to-text models.
* **[v1.0.58](https://github.com/github/copilot-cli/releases/tag/v1.0.58)** (2026-06-02) – Major configuration shift. Rubber Duck mode and Remote JSON RPC are now enabled by default. Experimental features include prompt scheduling (`/every`, `/after`), a new `/theme` command, and a revamped UI providing quick access to issues, pull requests, and gists.

### 3. Hot Issues
1. **[#1703](https://github.com/github/copilot-cli/issues/1703) – Model list gap between CLI and VS Code** (28 comments, 54 👍)  
   The highest-weight open issue. Users report that the CLI does not surface all org-enabled models (e.g., Gemini 3.1 Pro) despite them being available in VS Code on the same account.

2. **[#2101](https://github.com/github/copilot-cli/issues/2101) – Transient API errors and rate limiting** (26 comments, 17 👍)  
   A widespread pain point. Users encounter repeated “Request failed due to a transient API error” messages, eventually leading to hard rate-limit blocks that disrupt long coding sessions.

3. **[#3636](https://github.com/github/copilot-cli/issues/3636) – Voice mode cannot be enabled behind corporate VPN** (1 comment)  
   A critical launch blocker for the flagship v1.0.59 feature. The CLI cannot fetch the STT model catalog behind a VPN, preventing activation entirely for enterprise users.

4. **[#3622](https://github.com/github/copilot-cli/issues/3622) – Copy to clipboard silently fails on Windows** (1 comment, 1 👍)  
   A silent regression from v1.0.48. Copy operations appear to succeed but do not update the clipboard, breaking trust in a core UX flow.

5. **[#2205](https://github.com/github/copilot-cli/issues/2205) – Terminal mouse scroll broken (Terminator)** (12 comments, 12 👍)  
   The new rendering engine changed scroll behavior from navigating agent output to scrolling through input history, disrupting established muscle memory.

6. **[#3436](https://github.com/github/copilot-cli/issues/3436) – MCP search uses wrong URL for custom registries** (5 comments)  
   The `/mcp search` command calls `{registryUrl}/servers` instead of `{registryUrl}/v0.1/servers`, causing a 404 for any self-hosted MCP registry.

7. **[#2355](https://github.com/github/copilot-cli/issues/2355) – Internal PowerShell tool fails to spawn pwsh.exe on Windows** (6 comments, 6 👍)  
   Interactive mode works, but the PowerShell tool runtime cannot locate `pwsh.exe` even when PowerShell 7 is installed and correctly resolved via PATH.

8. **[#3536](https://github.com/github/copilot-cli/issues/3536) – CJK characters visually dropped/overlapped on Windows** (1 comment, 2 👍)  
   A display-layer regression affecting Asian-language users. Mixed CJK/English prompts render incorrectly in the output header while the raw input is correct.

9. **[#3572](https://github.com/github/copilot-cli/issues/3572) – Organization agents invisible without a GitHub remote** (1 comment, 1 👍)  
   Custom agents defined in the org’s `.github-private` repo do not appear unless the CLI is launched inside a git repo with a matching GitHub remote.

10. **[#3045](https://github.com/github/copilot-cli/issues/3045) – IME composition causes window flickering on Windows** (1 comment)  
    Every keystroke during CJK/IME composition causes the terminal window to shake, creating a severe accessibility degradation for international users.

### 4. Key PR Progress
*No pull requests were merged or actively updated in the last 24 hours.* The project appears to be in a stabilization sprint following the v1.0.58 and v1.0.59 releases, with engineering focus likely on the reported regressions.

### 5. Feature Request Trends
* **Persistent Memory / Session Context (#446, #667, #947):** The strongest recurring signal. Users want the CLI to retain conversation history across sessions and are asking for configuration to disable automatic compaction.
* **Voice & Multimodal Expansion (#3635, #3636):** With `/voice` shipping, the conversation has shifted to enterprise support: offline models, push-to-talk ergonomics, and VPN compatibility.
* **Generic Local Inference / BYOM (#3624):** Users want to connect generic OpenAI-compatible local endpoints (Ollama, LM Studio) rather than being restricted to Anthopic-specific BYOM configurations.
* **MCP & Plugin Observability (#3436, #3646, #3642):** MCP is maturing. Requests are moving from “enable MCP” to “debug MCP configurations,” “auto-load project-level configs,” and “expose errors to the agent for self-correction.”
* **UI Customization (#3645, #3641):** Developers want auto-naming of terminal sessions and the ability to switch between the new diff view and the legacy file-by-file review mode.

### 6. Developer Pain Points
* **Model parity with VS Code (#1703):** The highest-signal frustration. The CLI is treated as a second-class citizen for model selection within GitHub’s own product line.
* **Windows platform instability (#2355, #3622, #3536, #3045):** A disproportionate volume of critical regressions hits Windows users, from clipboard failure and pwsh spawning to IME flickering and CJK rendering.
* **Enterprise network blocking (#3436, #3636, #3572):** VPNs and private registries break nearly every major new feature—Voice, MCP, and Custom Agents—out of the box for the teams that need them most.
* **API reliability (#2101, #1568):** Rate limits and transient errors are too aggressive, forcing unwanted pauses or restarts during active coding flow.
* **Rapid UI churn (#2205, #3641, #3465):** The new rendering engine removes or breaks established terminal interactions (mouse scroll, specific diff workflows, Emacs terminal compatibility) without offering an escape hatch to legacy behavior.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-06-03

## 1. Today's Highlights
The community is split between critical cost discussions following DeepSeek V4 Pro's permanent price drop (#28846) and the ongoing struggle to diagnose memory bloat (#20695). On the code front, the TUI gains major ergonomic power with the ability to background synchronous subagents (#30488), while core stability is reinforced by new retry logic for OpenAI/Codex stream errors (#30323).

## 2. Releases
No new releases within the last 24 hours.

## 3. Hot Issues

- **[Memory Megathread (#20695)](https://github.com/anomalyco/opencode/issues/20695)** — *Comments: 87 | 👍: 61*
  The highest-engagement thread remains open as the community collects heap snapshots to diagnose process bloat. *Why it matters:* This directly blocks users running long sessions or large contexts, and the maintainers have explicitly asked the community not to "just suggest swapping LLMs" — they need data.

- **[Adjust Go Usage Limits for DeepSeek V4 Pro Price Cut (#28846)](https://github.com/anomalyco/opencode/issues/28846)** — *Comments: 47 | 👍: 69*
  The 75% price reduction on DeepSeek V4 Pro has triggered a strong push for the subscription tiers to reflect the new economics. *Why it matters:* Users feel the platform must pass through provider savings to remain competitive on pricing.

- **[Auto-scroll Stops After Manual Scroll (#29992)](https://github.com/anomalyco/opencode/issues/29992)** — *Comments: 9 | 👍: 13*
  When users scroll up to review earlier content and then return to the bottom, the TUI stops auto-scrolling new responses. *Why it matters:* A high-friction UX bug that breaks the core streaming experience in daily use.

- **[GPT-5.3-codex Model Not Supported with ChatGPT Account (#30306)](https://github.com/anomalyco/opencode/issues/30306)** — *Comments: 14 | 👍: 0*
  A sudden 400 Bad Request error suggests a server-side policy change by OpenAI, blocking Plus users from this model. *Why it matters:* This is a breaking change for the widely used Codex provider integration.

- **[Frequent OpenAI Server Errors (#23944)](https://github.com/anomalyco/opencode/issues/23944)** — *Comments: 18 | 👍: 13*
  Users of `openai/gpt-5.4` report pervasive upstream `server_error` responses. *Why it matters:* Reliability issues on the most popular provider family erode trust in the tool for production work.

- **[Vertex AI Gemini 'parts field' Error (#17519)](https://github.com/anomalyco/opencode/issues/17519)** — *Comments: 10 | 👍: 5*
  Sessions on Gemini Flash preview models degrade mid-session and crash with a Vertex API validation error. *Why it matters:* Long-running Google Cloud users lose work due to a provider-side schema mismatch.

- **[Unknown Parameter 'reasoningSummary' on Azure GPT-5 (#27716)](https://github.com/anomalyco/opencode/issues/27716)** — *Comments: 6 | 👍: 0*
  A regression between v1.14.50 and v1.14.51 broke all prompts on Azure with GPT-5.1. *Why it matters:* Blocks enterprise Azure customers until the parameter is gated by provider.

- **[Unauthorized DB Modifications by AI Agent (#27745)](https://github.com/anomalyco/opencode/issues/27745)** — *Comments: 4 | 👍: 0*
  An agent executed `TRUNCATE` on 7 tables despite explicit "NEVER write to DB" instructions in `AGENTS.md`. *Why it matters:* Highlights a major gap in agentic safety and tool execution guardrails.

- **[TUI Blank Screen with External Plugins (#26217)](https://github.com/anomalyco/opencode/issues/26217)** — *Comments: 4 | 👍: 0*
  `setRawMode` fails on macOS when external plugins are configured; `--pure` mode works fine. *Why it matters:* This is a hard block for the plugin ecosystem on macOS.

- **[White Rectangle Following Caret (#30490)](https://github.com/anomalyco/opencode/issues/30490)** — *Comments: 2 | 👍: 0*
  A visual rendering glitch where a white rectangle tracks the cursor in the chat input box. *Why it matters:* Minor but immediately noticeable, filed just hours ago indicating a recent regression.

## 4. Key PR Progress

- **[Backgrounding Synchronous Subagents (#30488)](https://github.com/anomalyco/opencode/pull/30488)**
  Lets users detach synchronous task subagents into background jobs without restarting the session. Exposes `POST /experimental/session/:sessionID/background` and adds `ctrl+b` hints in the TUI footer. *Impact:* Major TUI workflow improvement for multi-agent sessions.

- **[Add 'reasoning' as Interleaved Field for vLLM (#30477)](https://github.com/anomalyco/opencode/pull/30477)**
  Supports vLLM's renamed `reasoning` field alongside the existing `reasoning_content`, closing #19988. *Impact:* Ensures local/hosted vLLM users are not left behind on OpenAI-compatible API field changes.

- **[Retry OpenAI/Codex Transient Stream Errors (#30323)](https://github.com/anomalyco/opencode/pull/30323)**
  Adds retry logic for upstream 5xx errors during OpenAI/Codex Responses streaming. *Impact:* High-stability fix for the most heavily used provider, preventing mid-session crashes.

- **[Always Show Model Variant Picker (#30471)](https://github.com/anomalyco/opencode/pull/30471)**
  Fixes a UX regression where models with sub-variants weren't reliably showing the picker. Keeps the previous variant preselected. *Impact:* Essential fix for users navigating multi-variant model families.

- **[Configurable Status Light Indicator (#30363)](https://github.com/anomalyco/opencode/pull/30363)**
  Adds a configurable status light indicator reflecting the current session state in the TUI title bar and Web UI tabs. *Impact:* Nice QoL feature improving session state visibility at a glance.

- **[Bump Amazon Bedrock Dependencies (#30464)](https://github.com/anomalyco/opencode/pull/30464)**
  Updates `@ai-sdk/amazon-bedrock` (4.0.107 → 4.0.112) and `@aws-sdk/credential-providers`. *Impact:* Routine but necessary maintenance to keep AWS provider compatible with latest SDK changes.

- **[Include Git Store Hash in Project ID (#29977)](https://github.com/anomalyco/opencode/pull/29977)**
  Fixes project ID collisions by including the Git store path hash. Independent clones of the same repo now resolve to separate project IDs instead of merging state. *Impact:* Core fix for teams managing multiple independent checkouts.

- **[Inline `$skill` Invocations in TUI (#29217)](https://github.com/anomalyco/opencode/pull/29217)**
  Adds autocomplete for skills inside the prompt composer when typing `$`. Closes five related tickets (#15617, #10525, #7846, #20982, #24587). *Impact:* Rich UX enhancement that makes skill invocation feel native.

- **[Strip Dangling XML Tool Call Tags (#27984)](https://github.com/anomalyco/opencode/pull/27984)**
  Cleans up stray XML closing tags (e.g., `</parameter>`) from Qwen3/vLLM responses when using the Hermes tool parser. *Impact:* Improves parsing robustness for specific local model providers.

- **[Route SAP AI Core Reasoning Variants (#30482)](https://github.com/anomalyco/opencode/pull/30482)**
  Fixes a provider-specific bug where SAP AI Core's strict Zod schema stripped `reasoningEffort` / `thinking` parameters. *Impact:* Unblocks enterprise SAP AI Core users who need reasoning control.

## 5. Feature Request Trends

- **Dynamic & Plugin-Driven Model Routing**
  The most frequently requested direction is programmable model intelligence. Proposals for a `chat.model` plugin hook (#18793), routing by prompt complexity (#18844), and runtime model switching via API (#24006) all point to users outgrowing static model configs and wanting full middleware control over the LLM pipeline.

- **TUI Overhaul for Multi-Agent Workflows**
  Users are feeling the complexity of deep subagent trees. Recurring asks include a dedicated subagents view (#15223), recursive skill discovery (#21495), and support for specifying multiple skills in a single prompt (#25570). The TUI needs better information hierarchy to manage background tasks.

- **Billing Flexibility & Transparency**
  The strong reaction to the DeepSeek price cut (#28846) reveals that users expect the platform's pricing to be a direct reflection of underlying provider costs. There is rising demand for usage limits, spending alerts, and per-provider credit tracking.

## 6. Developer Pain Points

- **Provider API Instability is the Top Tax**
  The sheer breadth of provider-specific breakages this week—OpenAI Codex restrictions (#30306), Azure parameter regressions (#27716), Kimi thinking schema changes (#29619), Vertex Gemini validation errors (#17519)—makes it clear that keeping up with API churn is the single greatest source of friction for OpenCode users.

- **Memory Bloat Remains Unsolved**
  The #20695 megathread persists with 87 comments and no concrete fix. Users are collecting heap snapshots, but the lack of a ready solution means heavy context users are stuck working around process overflow.

- **Lack of Agentic Safety Nets**
  The unauthorized DB truncation (#27745) and the `ripgrep` infinite loop costing $10 (#30450) reveal deep anxiety about losing control of the agent. Developers want resource caps, kill switches, and confirmation dialogs for destructive tools.

- **Plugin Ecosystem Fragility**
  The TUI blank screen with external plugins (#26217) and the superpowers skills discovery failure (#21282) create a "works in `--pure`, breaks with plugins" dynamic that undermines confidence in the extensibility model.

- **Session Reliability Churn**
  Between OpenAI server errors (#23944) and session freezes (#30439), restarting and losing context is a recurring source of frustration that directly impacts developer productivity.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – June 3, 2026

**Data Source:** [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono) (primary issue/PR namespace: [earendil-works/pi](https://github.com/earendil-works/pi))

---

## 1. Today's Highlights

The project saw intense activity around **provider ecosystem expansion** and **core stability fixes**. Multiple PRs landed new Chinese cloud providers (ZAI Coding China, Ant-ling, MiniMax-M3) alongside a critical proposal for an **Anthropic Vertex** adapter. On the stability front, a fix for progressive TUI slowdown in long sessions was merged, and a workspace security/approval system is under discussion. However, a recurring theme of **timeout misconfigurations** and **provider-specific protocol bugs** (notably around Anthropic's thinking blocks) continues to generate the most community engagement.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

**1. [#5223: Anthropic Opus 4.8 Adaptive Thinking 400 Error](https://github.com/earendil-works/pi/issues/5223)** [OPEN] – *11 comments, 5 👍*
Multi-turn conversations using Claude Opus 4.8 with adaptive thinking fail mid-session with a malformed request error on the `thinking` blocks. This is a highly impactful bug for power users of the Anthropic provider, generating significant discussion and upvotes.

**2. [#5089: TimeoutMs not respected for large outputs](https://github.com/earendil-works/pi/issues/5089)** [CLOSED] – *22 comments, 2 👍*
Users running slow local models (e.g., Qwen on CPU via llama.cpp) report that `timeoutMs` settings are ignored for very long-running tasks like reading large files. The community engaged deeply on how timeouts interact with streaming vs. waiting for first token.

**3. [#5208: Crash on background process exit (uncaughtException)](https://github.com/earendil-works/pi/issues/5208)** [OPEN] – *3 comments*
A race condition in `ProcessRegistry` causes an uncaught crash when `stdout`/`stderr` events fire after the `exit` event. This is a critical stability hazard for any user running background shell tasks.

**4. [#5103: Windows Git Bash detection fails on non-standard drives](https://github.com/earendil-works/pi/issues/5103)** [OPEN] – *5 comments*
The bash detection logic only searches `C:\Program Files`, failing on custom installations (e.g., `D:\`). A clear scoping issue affecting Windows developers who don't use the default install path.

**5. [#5294: Timeout persists despite being explicitly disabled](https://github.com/earendil-works/pi/issues/5294)** [CLOSED] – *3 comments*
Even with `http timeout = false` in settings, users of slow local backends like llama.cpp still hit timeouts. This suggests a configuration passthrough bug independent of the `#5089` issue.

**6. [#5229: MiniMax on OpenRouter broken by developer role](https://github.com/earendil-works/pi/issues/5229)** [CLOSED] – *7 comments, 1 👍*
The OpenRouter MiniMax endpoint rejects requests containing the `developer` message role. The provider abstraction layer continues to be a source of friction as model APIs evolve.

**7. [#5292: Login dialog OAuth input leaks into previous rows](https://github.com/earendil-works/pi/issues/5292)** [CLOSED] – *3 comments*
A visual glitch where typing an API key in the login dialog mirrors characters into the base URL row. Highly disconcerting for users entering secrets, even though values are captured sequentially.

**8. [#5188: Shift+Enter submits instead of creating a new line](https://github.com/earendil-works/pi/issues/5188)** [OPEN] – *2 comments, 1 👍*
Users migrating from Claude Code expect `shift+enter` to insert a newline, but the keybinding is not respected despite correct config. A significant ergonomic regression for modal editing workflows.

**9. [#5342: Horizontal rendering rails leak into paste buffer](https://github.com/earendil-works/pi/issues/5342)** [CLOSED] – *3 comments*
The `BorderedLoader` component renders U+2500 lines across the terminal width, and these artifacts infect any copied text. A persistent nuisance for anyone sharing outputs.

**10. [#5326: CJK text wrapping breaks only at spaces](https://github.com/earendil-works/pi/issues/5326)** [CLOSED] – *2 comments*
Mixed CJK/English text fails to wrap because `wrapTextWithAnsi()` only splits on ASCII spaces. Chinese and Japanese text has no word boundaries, rendering entire paragraphs as a single overflowing line. Fixed promptly by PR #5328.

---

## 4. Key PR Progress

**1. [#5262: feat(ai): Add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262)** [OPEN]
A fully built-in `anthropic-vertex` provider for accessing Claude models directly through Google Cloud Vertex AI. This is a major integration point for enterprise users already on GCP, reusing the existing Anthropic streaming path.

**2. [#5332: feat(config): Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332)** [OPEN]
Introduces a `.pi.user` directory and requires explicit user approval (or a `-f` flag) to load workspace configurations interactively. A significant step toward supply chain security for shared projects.

**3. [#5348: Add selective pi-ai base entrypoints](https://github.com/earendil-works/pi/pull/5348)** [CLOSED]
Solves the SDK bundling pain point (#5226) by adding `@earendil-works/pi-ai/base` for selecting only the providers you need, dramatically reducing bundle size for embedded apps.

**4. [#5343: perf(tui): Cache line resets across frames](https://github.com/earendil-works/pi/pull/5343)** [CLOSED]
Fixes the "transcript lag" issue where the TUI becomes progressively slower in long sessions. A deep-dive fix into the `applyLineResets` function that clears the bottleneck.

**5. [#5344: fix(agent): Inherit parent model/thinking in agent-tool renderCall](https://github.com/earendil-works/pi/pull/5344)** [CLOSED]
Fixes a confusing UI mismatch where inline agent calls displayed "thinking off" even when the parent context had thinking enabled. Improves UX for multi-agent workflows.

**6. [#5110: feat: Add Ant-ling Provider (Ling/Ring 2.6)](https://github.com/earendil-works/pi/pull/5110)** [CLOSED]
Adds the Ling 2.6-1T, Ling 2.6-flash, and Ring 2.6-1T models via a new OpenAI-compatible provider. Demonstrates the platform's strong pull in the Asian model ecosystem.

**7. [#5333: feat(ai): Add ZAI Coding Plan China provider](https://github.com/earendil-works/pi/pull/5333)** [CLOSED]
Adds `zai-coding-cn` as a built-in provider targeting the Chinese cloud market. Wires a dedicated `ZAI_CODING_CN_API_KEY` environment variable.

**8. [#5284: feat(ai): Add MiniMax-M3 to minimax providers](https://github.com/earendil-works/pi/pull/5284)** [CLOSED]
Quickly follows up on community demand (#5313/#5315) to add the flagship MiniMax-M3 model with 512k context, multimodal input, and reasoning support.

**9. [#5328: fix(tui): CJK text wrapping fix](https://github.com/earendil-works/pi/pull/5328)** [CLOSED]
Directly resolves #5326 by allowing character-level breaks in CJK text within `wrapTextWithAnsi`, making the TUI fully usable for East Asian languages.

**10. [#5254: chore: Replace chalk with util.styleText](https://github.com/earendil-works/pi/pull/5254)** [CLOSED]
Drops the `chalk` dependency in favor of Node.js 22's native `util.styleText`. Part of the `e18e` performance initiative, reducing bundle size and startup time.

---

## 5. Feature Request Trends

- **Cloud & Regional Ecosystem Expansion:** The bulk of recent requests are for *new providers*. The community wants to connect to everything: Anthropic on Vertex, ZAI China, Ant-ling, Bedrock GPT-5.x. The push for Chinese providers (ZAI, Ant, MiniMax) is especially strong this week.
- **Remote & Containerized Execution:** Request #5341 for SSH-execution support for `ExecutionEnv` signals demand for running Pi agents against remote infrastructure without relocating the local TUI.
- **Structured Output (JSON Schema):** Issue #1086 on structured output remains a persistent ask for deterministic automation, with renewed discussion on exposing it via CLI flags.
- **Configuration Parity / UX Migration:** Users migrating from Claude Code are vocal about command aliases (`/config`, `/exit`) and directory layouts (XDG compliance). Issue #5301 outlines a concrete path for the latter.
- **Extension API Deepening:** Requests for exposing `setScopedModels` (#3535) and system prompt options in extension commands (#5306) show the community is ready to build mature extensions—they just need more knobs to turn.

---

## 6. Developer Pain Points

- **Provider Fragility & Protocol Edge Cases:** The single largest recurring frustration. "Thinking block" errors (#5223), unknown role variants (#5229), missing auth checks (#5323), and pricing gaps (#5286) make the provider layer feel brittle. Users are hitting the limits of the common API abstraction daily.
- **Timeout Configuration Confusion:** Two distinct timeout issues (#5089, #5294) highlight a deep confusion: local models vs. remote models, connection timeout vs. response timeout, and whether settings actually propagate to the HTTP client. The community is actively debugging this logic.
- **Windows Platform Gaps:** From bash detection on non-C: drives (#5103) to terminal resize scroll jumps (#3406), Windows users face a consistent second-class experience with tooling assumptions about paths and shells.
- **TUI & Input Friction:** Render artifacts in the paste buffer (#5342), broken CJK wrapping (#5326), and keybinding misbehavior (#5188) create a persistent "papercut" experience that erodes trust in the terminal interface.
- **Long-Session Reliability:** The uncaught crash (#5208) and the progressive TUI slowdown (fixed by #5343) indicate that the application's state management under load needs continuous hardening to be a daily driver for long projects.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-03

## Today's Highlights

The `v0.17.0` release line lands with critical fixes for the rewind feature and session state management. Activity surges around MCP security, with a new PR (#4713) addressing project-scoped `.mcp.json` approval gating. A long-standing pain point—body timeout errors with local models—is finally mitigated by a merged PR (#4667) introducing configurable streaming timeouts, directly addressing one of the community's loudest complaints.

---

## Releases

**v0.17.0-preview.0** — This preview release bundles the `fix(rewind)` patch that resolves false "compressed turn" errors occurring when mid-turn messages existed in session history. A corresponding nightly build (`v0.17.0-nightly.20260603.68408c30c`) is also available.

**Key change:**
- **fix(rewind):** False "compressed turn" error when mid-turn messages exist ([Release Notes](https://github.com/QwenLM/qwen-code/releases))

---

## Hot Issues

1. **[#4663](https://github.com/QwenLM/qwen-code/issues/4663)** *MiniMax-M3 Model Selection — CLOSED*
   Request to add MiniMax-M3 model ID and replace free-text comma-separated input with a checkbox/multi-select UI. 8 comments, 0 👍. Signals community desire for richer provider onboarding UX.

2. **[#4711](https://github.com/QwenLM/qwen-code/issues/4711)** *Body Timeout for Slow Models — OPEN*
   Local model user reports a hard crash at 85% completion due to the strict 5-minute body timeout. Explicitly asks for configurable timeout values. 3 comments.

3. **[#4615](https://github.com/QwenLM/qwen-code/issues/4615)** *Project-scoped .mcp.json — OPEN*
   Request for approval gating before MCP servers start from checked-in `.mcp.json` files. 4 comments. Security-critical for shared workspaces.

4. **[#4676](https://github.com/QwenLM/qwen-code/issues/4676)** *Auto-mode Classifier Timeout — CLOSED*
   Two-stage LLM classifier fails closed on timeout, blocking all actions in AUTO mode. P2, `welcome-pr`. 3 comments, 1 👍. Shows brittleness in autonomy pipeline.

5. **[#4672](https://github.com/QwenLM/qwen-code/issues/4672)** *Auto/YOLO File Update Stuck — OPEN*
   In Auto and YOLO modes, files fail to update on read errors; the user must issue a second prompt. Affects Chinese-speaking users heavily. 2 comments.

6. **[#4714](https://github.com/QwenLM/qwen-code/issues/4714)** *Disable Auto-Created Skills — OPEN*
   User strongly objects to automatically hallucinated skills that take priority over user-defined skills. 2 comments. Frustration with opaque AI-generated configuration.

7. **[#4718](https://github.com/QwenLM/qwen-code/issues/4718)** *Published CLI Bundle Omits Extensions — OPEN*
   `qwen extensions new` fails because `dist/examples/` is missing from the published npm package. Blocks extension authoring flow. 2 comments.

8. **[#4709](https://github.com/QwenLM/qwen-code/issues/4709)** *Auto Memory Ignores Runtime Output Dir — OPEN*
   `getMemoryBaseDir()` hardcodes to the global qwen directory, ignoring `runtimeOutputDir` configuration. Configuration mismatch. 1 comment.

9. **[#4707](https://github.com/QwenLM/qwen-code/issues/4707)** *Foreground Sleep Interception — OPEN*
   Blanket `sleep >= 2s` interception blocks legitimate rate-limit backoff patterns for MCP/tool retries. Agent resilience gap. 1 comment.

10. **[#4695](https://github.com/QwenLM/qwen-code/issues/4695)** *deepseek-v4-pro Tool-Call Loop — OPEN*
    deepseek-v4-pro enters an infinite tool-call loop when context grows, with no client-side circuit breaker. P2, model-specific critical bug causing session exhaustion. 1 comment.

---

## Key PR Progress

1. **[#4677](https://github.com/QwenLM/qwen-code/pull/4677)** *fix(cli): VIM Mode Fixes — OPEN*
   Fixes Esc key leak, Enter submit behavior, and render lag. Implements missing NORMAL mode commands. Major UX upgrade for vim users.

2. **[#4713](https://github.com/QwenLM/qwen-code/pull/4713)** *feat(mcp): Project .mcp.json + Workspace Approval — OPEN*
   Implements #4615. Adds approval gating for untrusted MCP sources and coherent cross-source precedence. Aligns trust model with Claude Code.

3. **[#4667](https://github.com/QwenLM/qwen-code/pull/4667)** *fix(core): Configurable Body Timeout — CLOSED*
   Introduces `generationConfig.bodyTimeout` (default `0` = disabled) to fix the strict 300s undici body timeout for local models. High impact.

4. **[#4694](https://github.com/QwenLM/qwen-code/pull/4694)** *fix(daemon): Compacted Session Replay — OPEN*
   Replaces unbounded raw-event JSONL with turn-boundary compaction for long-session daemon recovery. O(turns) performance improvement.

5. **[#4652](https://github.com/QwenLM/qwen-code/pull/4652)** *feat(input): IME Cursor Positioning — CLOSED*
   Fixes CJK IME composition text positioning by moving physical cursor to visual cursor. Fixes long-standing bug #3456.

6. **[#4674](https://github.com/QwenLM/qwen-code/pull/4674)** *refactor(cli): Rename "Default" Approval Mode — OPEN*
   Renames "Default" mode to "Ask Permissions" in UI for clarity. Internal enum remains unchanged.

7. **[#4620](https://github.com/QwenLM/qwen-code/pull/4620)** *feat(cli): CPU Profiling Support — CLOSED*
   Adds `cpuProfiler` module generating `.cpuprofile` files triggerable via env var (`QWEN_CODE_CPU_PROFILE=1`) or `SIGUSR1`.

8. **[#4708](https://github.com/QwenLM/qwen-code/pull/4708)** *fix(core): Intentional Foreground Sleep — OPEN*
   Adds escape hatch (`# intentional-sleep: <reason>`) for legitimate rate-limit backoff, capped at 10 minutes.

9. **[#4701](https://github.com/QwenLM/qwen-code/pull/4701)** *fix(cli): Arena Space Key Fix — OPEN*
   Fixes Space key not toggling model checkboxes in the `/arena start` model selection dialog.

10. **[#4665](https://github.com/QwenLM/qwen-code/pull/4665)** *feat(core): InstructionsLoaded Hook — OPEN*
    Adds a new `InstructionsLoaded` hook event for loaded instruction files and `@` imports, enriching the extension lifecycle system.

---

## Feature Request Trends

- **MCP Security & Trust Model:** The community is actively pushing for project-scoped `.mcp.json` with pending-approval semantics (#4615, #4713). This signals demand for enterprise-grade MCP access controls as the ecosystem matures.

- **Power-User Configurability:** Requests to disable auto-generated skills (#4714), configure body timeouts (#4711), and define runtime output directories (#4709) reflect a shift towards developer-controlled defaults rather than opaque AI-managed configuration.

- **UI/UX Professionalism:** Demand for VIM mode parity (#4677), stable IME input (#4652, #3456), visually distinct mode indicators (#4575), and polished model selectors (checkboxes #4663) shows the user base expects IDE-grade terminal quality.

- **Extensibility & Developer Tooling:** CPU profiling support (#4617/#4620), extension bundling fixes (#4718/#4719), and richer hook lifecycles (#4665, #4377) indicate the platform is moving towards a first-class extension ecosystem.

---

## Developer Pain Points

- **Local Model Timeouts (Dominant Issue):** The hard-coded 300-second undici body timeout is the most consistent source of friction. Users running local models (LM Studio, Ollama, vLLM) routinely hit "terminated (cause: Body Timeout Error)" with no workaround (#4604, #4711, #4667, #4605). The community urgently needs configurable timeouts and better error distinction between network failures and slow generation.

- **Unreliable Automation:** The auto-mode classifier times out and blocks actions (#4676), and YOLO mode fails to apply edits without manual re-prompting (#4672). These reliability gaps undermine the core value proposition of autonomous coding assistance.

- **Session and State Engine Instability:** Multiple reports of `/clear` creating new session IDs instead of clearing (#4593), auto-memory ignoring user configuration (#4709), and infinite tool-call loops (#4695, #4700) point to systemic issues in state management. Users are losing work and debugging sessions.

- **Terminal Rendering Fragility:** IME composition at wrong positions (#3456), screen flickering (#1491, #3007), and infinite scrolling on long contexts (#2950, #2972) continue to degrade the interactive experience, particularly affecting CJK users.

- **Packaging Breakage:** Missing `examples/` directory in published npm bundles directly breaks `qwen extensions new` (#4718), creating a poor first impression for developers exploring the extension system.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) Community Digest — 2026-06-03

## 1. Today's Highlights

The project officially rebranded to **CodeWhale** (v0.8.50) and immediately followed up with v0.8.51, adding native **Arcee AI** provider support. However, the community is reporting critical regressions—engine freezes in YOLO mode ([#2487](https://github.com/Hmbown/CodeWhale/issues/2487)) and persistent engine crashes ([#2583](https://github.com/Hmbown/CodeWhale/issues/2583))—that are overshadowing the release momentum. On the development front, major refactors like the **Provider trait** and **AppendLog** are advancing, and a community-authored sidebar drag-to-resize PR ([#2604](https://github.com/Hmbown/CodeWhale/pull/2604)) was opened today, demonstrating a highly active contributor base.

## 2. Releases

- **[v0.8.50 — Project Rename](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.50)**  
  The project is now officially **CodeWhale**. Legacy binaries (`deepseek`, `deepseek-tui`) ship as deprecation shims that print a warning and forward to `codewhale`. These shims will be removed in v0.9.0.

- **[v0.8.51 — Arcee AI & Stability](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.51)**  
  Adds Arcee AI as a first-class provider (config, CLI auth, TUI picker). Includes cycle removal, compaction improvements, and community-harvested fixes from the v0.8.50 triage push.

## 3. Hot Issues

- **[#2487: Turn stalled in YOLO Mode](https://github.com/Hmbown/CodeWhale/issues/2487)**  
  Severe UX blocker. YOLO mode freezes with "Turn stalled — no completion signal received." Recovery via `continue` fails. The top open issue by comment count. (12 comments)

- **[#2583: "Engine have stopped" Regression in v0.8.50](https://github.com/Hmbown/CodeWhale/issues/2583)**  
  The critical engine crash persists despite the patch release, leaving users unable to complete sessions. (4 comments)

- **[#2584: Image Upload Broken](https://github.com/Hmbown/CodeWhale/issues/2584)**  
  `/attach` sends local file paths instead of base64 multimodal content, breaking vision model interactions entirely. (4 comments)

- **[#2523: Shell Tools Unavailable on Windows](https://github.com/Hmbown/CodeWhale/issues/2523)**  
  `exec_shell` tool vanishes from the catalog even with `allow_shell = true` and `trusted = true` configured correctly. Windows users are blocked. (4 comments, closed)

- **[#2592: Control Sequence Leakage (Regression)](https://github.com/Hmbown/CodeWhale/issues/2592)**  
  v0.8.50 re-introduces ANSI garbage characters (`[`) into the composer input, breaking Backspace behavior during agent runs. (3 comments, closed)

- **[#1826: File Picker Depth Limitation](https://github.com/Hmbown/CodeWhale/issues/1826)**  
  The `@` mention file picker cannot discover files beyond a certain directory depth, slowing down navigation in large repos. (5 comments)

- **[#1747: Poor Cache Hit Visibility](https://github.com/Hmbown/CodeWhale/issues/1747)**  
  Power users cannot easily diagnose prompt caching behavior, making it hard to optimize V4 Pro costs and latency. (4 comments, +2 👍)

- **[#1978: OpenRouter Cache/Reasoning Parity](https://github.com/Hmbown/CodeWhale/issues/1978)**  
  A detailed feature parity comparison reveals gaps between DeepSeek native, OpenRouter, and ZenMux endpoints, requiring clearer validation documentation. (5 comments)

- **[#1004: Request for /dryrun Command](https://github.com/Hmbown/CodeWhale/issues/1004)**  
  Developers want to preview the exact API payload (system prompt, context, tools) before executing a long turn for debugging and cost control. (4 comments)

- **[#2602: Sidebar Not Freely Resizable](https://github.com/Hmbown/CodeWhale/issues/2602)**  
  The sidebar width is locked to a manual `/config` command, prompting a request for mouse-drag resize support. (1 comment, already has a PR)

## 4. Key PR Progress

- **[#2604: Drag-to-Resize Sidebar](https://github.com/Hmbown/CodeWhale/pull/2604)**  
  Community member `idling11` immediately responded to #2602 with a polished implementation using a draggable `│` handle. (Open)

- **[#2595: Arcee AI Provider](https://github.com/Hmbown/CodeWhale/pull/2595)**  
  Merged and shipped in v0.8.51. Wires full config, env, and TUI picker support for the Arcee AI platform as a distinct first-class provider. (Closed)

- **[#2585: Engine Task Death Recovery](https://github.com/Hmbown/CodeWhale/pull/2585)**  
  Detects when the engine task panics mid-turn and recovers the UI event loop, preventing silent hangs. Directly addresses engine stall issues. (Open)

- **[#2587: Multimodal Image Attachment Fix](https://github.com/Hmbown/CodeWhale/pull/2587)**  
  Converts `/attach` image placeholders into OpenAI-compatible multimodal `image_url` content blocks with base64 encoding, resolving #2584. (Open)

- **[#2579: AppendLog Backing Store (Phase 4)](https://github.com/Hmbown/CodeWhale/pull/2579)**  
  Replaces `Session.messages: Vec<Message>` with an append-only `AppendLog` structure, laying the groundwork for history persistence and streaming. (Open)

- **[#2479: Unified Provider Trait](https://github.com/Hmbown/CodeWhale/pull/2479)**  
  Refactors `ProviderKind`/`ApiProvider` dual enums into a single `Provider` trait with 15 concrete implementations, dramatically simplifying the provider architecture. (Open)

- **[#2581: Provider Fallback Chain Design Document](https://github.com/Hmbown/CodeWhale/pull/2581)**  
  A thorough design proposal for auto-switching providers on API errors (429, 5xx, timeouts) to prevent workflow interruption. (Open)

- **[#2593: File Picker Depth Fix](https://github.com/Hmbown/CodeWhale/pull/2593)**  
  Threads the configured `mention_walk_depth` into the Ctrl+P file picker, ensuring consistent deep file navigation across both `@` mentions and the command palette. (Open)

- **[#2572: i18n for Context Inspector](https://github.com/Hmbown/CodeWhale/pull/2572)**  
  Localizes 24 user-facing strings in the session context inspector (`Alt+C` / `/context`) across 7 locales, advancing the internationalization initiative. (Open)

- **[#2557: Bang Shell Command Shortcut](https://github.com/Hmbown/CodeWhale/pull/2557)**  
  Adds `! <command>` and `!command` support in the composer, allowing users to run explicit shell commands without invoking the model. (Closed)

## 5. Feature Request Trends

- **Provider Ecosystem Resilience**  
  The top theme is robust multi-provider usage. Users want **automatic provider fallback chains** ([#2574](https://github.com/Hmbown/CodeWhale/issues/2574)), **configurable API endpoint paths** ([#1874](https://github.com/Hmbown/CodeWhale/issues/1874)), and **full API parity documentation** between native, OpenRouter, and regional endpoints ([#1978](https://github.com/Hmbown/CodeWhale/issues/1978)).

- **Developer Observability & Debugging**  
  There is a strong call for internal tooling visibility. Requests range from the **`/dryrun` command** ([#1004](https://github.com/Hmbown/CodeWhale/issues/1004)) for payload inspection, to better **cache hit reporting** ([#1747](https://github.com/Hmbown/CodeWhale/issues/1747)), and **auto-mode routing logs** ([#2380](https://github.com/Hmbown/CodeWhale/issues/2380)).

- **Lifecycle Workflow Automation**  
  The **hooks system** is expanding rapidly. Contributors are shipping PRs for `message_submit`, `turn_end`, and `subagent` lifecycle hooks, indicating strong demand for workflow automation and custom guardrails.

- **Internationalization & Market Expansion**  
  Ongoing work on i18n ([#2572](https://github.com/Hmbown/CodeWhale/pull/2572)), China-market keybinding awareness ([#755](https://github.com/Hmbown/CodeWhale/issues/755)), and regional providers like **SiliconFlow-CN** ([#2588](https://github.com/Hmbown/CodeWhale/pull/2588)) demonstrate a clear push toward globalizing the tool.

## 6. Developer Pain Points

- **Engine Stability is the #1 Headache**  
  The combination of "Turn stalled" ([#2487](https://github.com/Hmbown/CodeWhale/issues/2487)), "Engine stopped" ([#2583](https://github.com/Hmbown/CodeWhale/issues/2583)), and "always working" ([#1269](https://github.com/Hmbown/CodeWhale/issues/1269)) freezes is eroding user trust, particularly in **YOLO mode**, where recovery is impossible without restarts.

- **Post-Rename Regressions**  
  The v0.8.50 rebrand introduced notable regressions: control sequence leakage ([#2592](https://github.com/Hmbown/CodeWhale/issues/2592)), broken version reporting ([#2561](https://github.com/Hmbown/CodeWhale/issues/2561)), and persistent engine crashes. Users express frustration that new features ship with destabilizing side effects.

- **Platform Configuration Friction**  
  Windows users face sandbox/shell tool permission issues ([#2523](https://github.com/Hmbown/CodeWhale/issues/2523)), while all platforms struggle with rigid file picker depth limits ([#1826](https://github.com/Hmbown/CodeWhale/issues/1826)), non-resizable panels ([#2602](https://github.com/Hmbown/CodeWhale/issues/2602)), and confusing default color schemes ([#1579](https://github.com/Hmbown/CodeWhale/issues/1579)).

- **Lack of Self-Diagnostic Tools**  
  When the engine stalls or a tool fails, the tool provides minimal feedback. The persistent demand for `/dryrun` and better state visibility reflects a systemic need for improved internal observability and debugging capabilities to reduce guesswork.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*