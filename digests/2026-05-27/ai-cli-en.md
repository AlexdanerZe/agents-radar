# AI CLI Tools Community Digest 2026-05-27

> Generated: 2026-05-27 03:30 UTC | Tools covered: 9

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

# Multi-Platform AI CLI Developer Tool Analysis
**Date:** 2026-05-27  
**Role:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape on May 27, 2026 reflects a market in hyper-competitive adolescence. While core code-generation capability is largely commoditized, the battlefront has shifted decisively to **platform parity, agent autonomy, and enterprise readiness**. A clear architectural divide is emerging between tools optimized for single-user interactive coding (Claude Code, Codex CLI, CodeWhale) and those building multi-agent server infrastructure (Gemini CLI, Qwen Code, Kimi Code). The dominant theme across all communities is "regression fatigue vs. architectural ambition"—established tools are paying for rapid past feature churn with stabilization crises, while newer entrants race to build robust daemonized workflows. The MCP ecosystem is universally recognized as the defining plugin standard, yet OAuth friction, blacklist bypass vulnerabilities, and runtime configuration gaps are slowing grassroots adoption.

---

## 2. Activity Comparison

| Tool | Releases (24h) | Hot Issues | Key PRs | Top Issue | Community Health Signal |
|---|---|---|---|---|---|
| **Claude Code** | 1 (v2.1.152) | 10 | 10 | **GitLab Integration** (94 👍) | Stable, rapid iteration |
| **OpenAI Codex** | 1 (v0.134.0) | 10 | 10 | **OAuth NoneType crash** (#24665) | 🔴 **Critical** (broken Linux x64 binary) |
| **Gemini CLI** | 0 | 10 | 10 | **Agent Hangs** (8 👍, #21409) | Stable, high architectural velocity |
| **GitHub Copilot CLI** | 1 (v1.0.55-1) | 10 | 0 | **IME Submit Key** (46 👍, #1972) | 🟡 **Fragile** (regression fatigue peak) |
| **Kimi Code CLI** | 1 (v1.45.0) | 7 | 6 | **API Key Rate Limit** (#2368) | Stable, active scaling engineering |
| **OpenCode** | 0 (v1.15.11 pending) | 10 | 10 | **Agent Sandboxing** (47 👍, #2242) | Stabilizing, high bug-fix throughput |
| **Pi** | 0 | 10 (mostly closed) | 10 | **Local LLM Provider** (31 👍, #3357) | Mature, terminal-compatibility focus |
| **Qwen Code** | 2 (v0.16.1 preview) | 10 | 10 | **OOM in Long Sessions** (#4149) | Strong architectural velocity (Daemon mode) |
| **CodeWhale** (fka DeepSeek TUI) | 3 (v0.8.45–47) | 10 | 10 | **Docker Encoding** (190 comments, #1615) | 🟡 **Migrating** (rebranding friction) |

**Key Takeaway:** OpenAI Codex and GitHub Copilot CLI carry the highest near-term user risk due to broken builds and regression accumulation, respectively. Qwen Code and Kimi Code are delivering the most significant architectural innovations. CodeWhale and OpenCode lead in raw community engagement volume relative to project scale.

---

## 3. Shared Feature Directions

Multiple independent communities are converging on identical requirements—strong evidence of genuine developer need rather than vendor-driven priorities.

### 3.1 Git Platform Parity & Workflow Integration
- **GitLab integration** dominates as the top open feature request for Claude Code (#12346, 94 👍) and recurs across Gemini CLI (MR reviews) and OpenCode.
- **PR review reliability** is a common pain point across Claude Code (now shipping `--fix`), Copilot CLI (#3529 generic review errors), and Gemini CLI.
- **Remote session management** appears in Copilot CLI (#3442 false-positive warnings) and Pi (#5018 session naming).

### 3.2 MCP Ecosystem Maturity & Security
- **OAuth/authentication granularity**: Claude Code (#61376 401s), OpenAI Codex (#24665 `NoneType` crash), Qwen Code (#4317 SSO 504s), and Pi (#4911 device code login) all have active auth issues. Strict RFC compliance is demanded.
- **Dynamic MCP server configuration**: Qwen Code (#4552 runtime add/remove), Claude Code (skills `disallowed-tools`), and Copilot CLI (#3436 registry URL bugs) point toward immutable-config frustration.
- **Security hardening**: Gemini CLI patched an MCP blacklist bypass RCE (#27377). Claude Code shipped a security-guidance plugin. CodeWhale and OpenCode are building formal typed permission systems.

### 3.3 Terminal & Clipboard Ergonomics (The "Professional Polish" Tier)
- **Clipboard fidelity**: CodeWhale (#1920 Wayland silent failure), Claude Code (#62682 macOS TUI formatting loss), Copilot CLI (#3534 WSL ARM64 clipboard broken).
- **URL handling & wrapping**: Claude Code (#62678 Windows wrapping), Copilot CLI (#3395 Linux paste).
- **Input method (IME) support**: Copilot CLI (#1972 top open feature at 46 👍) for CJK users; CodeWhale (#2165) and Pi (Intl.Segmenter, #5022) actively fixing CJK boundary panics.
- **Output truncation / full content access**: Claude Code (#26954, long-standing), OpenCode (#29363 32K silent cap), Pi (#4945 "Working..." hang).

### 3.4 Enterprise & Headless Workflows
- **Non-interactive / silent modes**: Pi (#5031 piped mode silent failure), Gemini CLI (#27365 `--ephemeral`), Codex (#21567 `CODEX_NON_INTERACTIVE`), Claude Code (explicit requests).
- **Persistent environment hooks**: Codex (#24650 `CODEX_ENV_FILE`), Copilot CLI (#3508 lifecycle hooks broken), Claude Code (WorktreeCreate hooks #29716).
- **Audit & cost observability**: Qwen Code (#4564 token usage stats), OpenCode (#28846 DeepSeek V4 pricing), Kimi Code (#2368 rate limiting), Codex (#2916 API tier config).

### 3.5 Agent Safety & Permission Architecture
- All major tools are building or have shipped some form of persistent permission system: OpenCode (#2242 agent sandboxing), CodeWhale (#2242 typed allow/deny/ask), Gemini CLI (#27377 blacklist fix), Claude Code (`disallowed-tools` in Skills), Codex (permissions overhaul in v0.134.0).

---

## 4. Differentiation Analysis

The tools are diverging sharply on architecture, target user, and strategic priority.

| Strategic Archetype | Representative Tools | Core Differentiator | Primary Weakness |
|---|---|---|---|
| **Senior Dev Assistant** | Claude Code | Review pipelines, lifecycle hooks, rich plugin ecosystem | Desktop-mode stability, documentation lag |
| **AGI Terminal** | OpenAI Codex | Deepest OpenAI model integration | Auth fragility, unexplained regressions, build artifacts |
| **Enterprise Gateway** | GitHub Copilot CLI | Zero-friction GitHub workflow lock-in | Regression fatigue, stagnant feature velocity |
| **Research Autonomy Platform** | Gemini CLI | Multi-agent sub-agents, AST understanding, formal evals | Agent loop brittleness (hangs, false success) |
| **Scaling Engine** | Kimi Code CLI | Multi-agent concurrency (API Key Pool), provider pragmatism | VSCode extension UX, low community visibility |
| **Open-Source BYOK Power Tool** | OpenCode | Maximum provider flexibility (local + cloud), high contributor churn | Reliability under heavy load, tool-call fragility |
| **Terminal Engineer's Stable Choice** | Pi | Terminal mux/hardware compatibility, local-first SaaS bypass | Feature velocity vs. incumbent alternatives |
| **Agent Server Infrastructure** | Qwen Code | Daemon mode (ACP/MCP bridges), server-first architecture | Memory pressure in long sessions, IDE parity |
| **International Swiss-Army Blade** | CodeWhale | Provider diversity (Xiaomi, OpenRouter), heavy i18n | Rebranding migration pain, Windows stability |

**Strategic Observations:**
- **Qwen Code** is the only tool anticipating a future where the CLI is not a session client but a long-running server process. Its ACP/MCP bridges (#4472, #4555) represent the most architecturally advanced bet in the entire landscape.
- **Gemini CLI** and **Kimi Code** are investing hardest in autonomous multi-agent workflows, directly attacking the "agent loop" scaling ceiling that constrains the entire category.
- **Pi** holds a unique position as the tool least concerned with the "AI hype cycle" and most focused on raw terminal engineering excellence and local model sovereignty.
- The **OpenCode** community bug-fix throughput (the YOMXXX wave merging a dozen patches today) demonstrates the resilience of truly open governance, but it also produces instability.

---

## 5. Community Momentum & Maturity

### Highest Maturity (Established User Base, High Expectations)
- **Claude Code**: Most sophisticated feature requests and bug reporting. Community expects enterprise-grade stability. GitLab parity is the #1 litmus test of platform commitment.
- **GitHub Copilot CLI**: Largest installed base due to GitHub distribution. The 1.0.49 regression cluster (WSL, TUI, clipboard, mouse scroll) has meaningfully damaged trust. The next 2–3 releases are critical retention windows.
- **Pi**: Smallest but most technically discerning community. Terminal mux compatibility is treated as a first-class requirement. Low drama, high signal-to-noise ratio in issue tracking.

### Highest Velocity (Shipping Architecture, Accepting Instability)
- **Qwen Code**: Most ambitious engineering output of any tool in this window. The Daemon workspace refactor (#4563), MCP serve bridge (#4555), and telemetry infrastructure (#4565) are enterprise-grade deliverables in an early-stage product.
- **Kimi Code CLI**: Very responsive to core bottlenecks. The API Key Pool PR (#2369) directly addresses the community's top scaling blocker. Demonstrates tight feedback loop.
- **CodeWhale**: Fastest release cadence (3 releases today). Rebranding from DeepSeek to CodeWhale introduces friction but signals commercial ambition. i18n investment (#2239, 47 files) is unmatched.

### Highest Risk Profile
- **OpenAI Codex**: A broken Linux x64 build artifact (#24672), a complete OAuth crash (#24665), and widespread quality regressions (#24649) form a dangerous trifecta. Users have alternatives (Claude Code, Gemini CLI) and may switch if these aren't resolved urgently. The "GPT-5.5 1M context cancelled" debacle (#24031) also signals communication culture issues.
- **GitHub Copilot CLI**: Enterprise users are a captive audience but will escalate internally if the "1.0.49 was good, 1.0.51 is bad" pattern continues. Zero new feature PRs today signals an internal stabilization crunch.

### Fragmentation Risk
- **Windows and Linux parity** remain the weakest link across the entire landscape. No tool offers a truly "first-class" experience on all three major platforms simultaneously. WSL2 ARM64 clipboard (Copilot CLI #3534), Windows Bash `EEXIST` (Claude Code #56593), Wayland browser agent failures (Gemini CLI #21983), and Windows TUI freezes (CodeWhale #1812) fragment the user base and force platform lock-in.

---

## 6. Trend Signals — Implications for Decision-Makers

### 6.1 The "Agent Server" has Arrived (Qwen Code, Gemini CLI)
The single strongest architectural signal is the shift from session-based CLI to long-running daemon processes. Qwen Code's `qwen serve` (Mode B) with ACP/MCP bridges is the most mature implementation, but Gemini CLI's `--ephemeral` mode and Claude Code's Desktop hooks point in the same direction.
**Implication:** Tools without a robust daemon/server architecture by Q4 2026 will be locked out of enterprise CI/CD, IDE integration, and remote development use cases. Evaluate tools on their headless and server-side capabilities, not just interactive TUI polish.

### 6.2 Silent Failure is the Most Dangerous Bug Class
Across every community, the highest-sentiment issues involve tools that silently lie: sub-agents reporting "success" when maxed out (Gemini CLI #22323), clipboard writes dropping data (CodeWhale #1920), status showing "Working..." while hung (Pi #4945), autosave reporting completion while history is lost (Codex #23979).
**Implication:** When evaluating tools, strict error hygiene and observability (structured logs, explicit state transitions) should be weighted more heavily than feature lists. A tool that fails loudly is more trustworthy than one that fails quietly.

### 6.3 MCP Security is the New Supply Chain Risk
The Gemini CLI MCP blacklist bypass RCE fix (#27377) and Claude Code's OAuth gap (#61376) are early warnings. MCP servers are quickly becoming the "npm of 2026"—a proliferating ecosystem with minimal security governance. Malicious workspace `.mcp.json` files or compromised plugins represent a direct supply chain attack vector.
**Implication:** Enterprises must mandate tool-specific security guidance (Claude Code's approach), typed permission systems (CodeWhale, OpenCode), and allowlisted MCP endpoints. The next high-profile breach will be via an MCP server, not a browser extension.

### 6.4 Developer Experience Parity is the Competitive Moat
No tool is delivering an excellent experience across all platforms and input methods. CJK IME support (Copilot CLI #1972), Wayland clipboard (CodeWhale #1920), ARM64 WSL (Copilot CLI #3534), and JetBrains IDE integration (Qwen Code #4493) all represent table-stakes gaps that erode user trust.
**Implication:** Organizations with diverse hardware/OS environments (typical in enterprise) should evaluate tools explicitly for the weakest platform in their fleet. A tool that works perfectly on macOS but fails on WSL2 has a hard ceiling on adoption.

### 6.5 Multi-Provider is the Ultimate Hedge
The ecosystem is fracturing between tool-specific model lock-in (Codex ~ OpenAI, Copilot ~ GitHub Models) and tools aggressively pursuing multi-provider flexibility (OpenCode, Kimi Code, CodeWhale, Pi). CodeWhale's Xiaomi MiMo integration (#2240) signals that geo-political and pricing pressures will drive further diversification.
**Implication:** Standardizing on a tool architecture that supports multiple backends reduces vendor risk and allows teams to optimize for cost, latency, and model performance independently. Tools designed as model-agnostic runtimes (Pi, OpenCode, CodeWhale) have a structural long-term advantage over tight integration plays.

### 6.6 Autonomy Scaling Ceilings are Real
The community is hitting concrete infrastructure bottlenecks: the 128-tool MCP API limit (Gemini CLI #24246), single-API-key throttling for concurrent sub-agents (Kimi Code #2368), and OOM crashes in long sessions (Qwen Code #4149). Solving these (dynamic tool loading, key pooling, memory pressure monitoring) is the next frontier.
**Implication:** Any team planning to deploy AI CLI tools for autonomous, multi-hour tasks must understand the memory and rate-limit profiles of their chosen tool. These infrastructure details will separate production-ready agents from prototypes.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Community Highlights Report for the `anthropics/skills` repository based on the most-watched pull requests and community issues as of May 27, 2026.

---

## 1. Top Skills Ranking

*The following 8 Pull Requests represent the highest-discussion Skill proposals, covering significant new capabilities and major platform integrations.*

**1. AURELION Skill Suite (PR #444)** | [Open](https://github.com/anthropics/skills/pull/444)
A structured cognitive framework introducing four skills: *aurelion-kernel* (5-floor thinking templates), *advisor* (context injection), *agent* (meta-prompts), and *memory* (persistent context). Discussion focuses on its density as a full agentic operating system for Claude. **Status: OPEN.**

**2. ServiceNow Platform Skill (PR #568)** | [Open](https://github.com/anthropics/skills/pull/568)
A broad enterprise skill covering ITSM, ITOM, SecOps, ITAM/SAM, FSM, SPM, CSDM, and IntegrationHub. Positions Claude as a full platform assistant rather than a narrow scripting helper. **Status: OPEN.**

**3. Add testing-patterns skill (PR #723)** | [Open](https://github.com/anthropics/skills/pull/723)
Comprehensive testing methodology covering the Testing Trophy model, AAA unit patterns, React Testing Library, and E2E strategies. Directly addresses the core developer workflow of quality assurance. **Status: OPEN.**

**4. n8n Builder & Debugger (PR #190)** | [Open](https://github.com/anthropics/skills/pull/190)
Adds four production-tested community skills including *n8n-builder* and *n8n-debugger* for building and troubleshooting workflows. Represents the “automation-as-code” pattern the community heavily gravitates toward. **Status: OPEN.**

**5. ODT Skill (PR #486)** | [Open](https://github.com/anthropics/skills/pull/486)
Adds OpenDocument Format creation, template filling, and ODT-to-HTML conversion. This closes a critical document-format gap for public sector and European enterprise users. **Status: OPEN.**

**6. SAP-RPT-1-OSS Predictor (PR #181)** | [Open](https://github.com/anthropics/skills/pull/181)
Integrates SAP’s open-source tabular foundation model for predictive analytics directly inside Claude Code. A niche but powerful enterprise skill bridging SAP data with LLM orchestration. **Status: OPEN.**

**7. Document Typography Skill (PR #514)** | [Open](https://github.com/anthropics/skills/pull/514)
Solves persistent AI-writing quality issues: orphans, widows, numbering misalignment. While narrow in scope, it addresses a universal UX frustration in generated documents. **Status: OPEN.**

**8. Codebase Inventory Audit (PR #147)** | [Open](https://github.com/anthropics/skills/pull/147)
A systematic 10-step workflow for identifying orphaned code, unused files, and documentation gaps. Acts as a “meta” skill for large-scale codebase hygiene. **Status: OPEN.**

---

## 2. Community Demand Trends

*Analysis of the top commented Issues reveals where the community is actively hitting friction or requesting new infrastructure:*

**Skill Distribution & Management (#228, #189, #1087)**
The loudest demand is for mature distribution. Users are frustrated with manual `.skill` file sharing via Slack (#228), plugin systems installing duplicates (#189), and plugins loading all repository skills instead of declared sets (#1087).

**Tooling Reliability (#556, #202, #184)**
The evaluation framework (`run_eval.py`) is widely broken—queries never trigger skills (#556). The `skill-creator` itself is flagged as educational rather than operational, and the `agentskills.io` reference site suffered redirect errors (#184).

**Security & Trust Boundaries (#492, #1175, #412)**
Trust is a rising theme. Community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability (#492). Users propose an *agent-governance* skill for policy enforcement and audit trails (#412). Enterprise concerns are emerging around embedding access control logic in SKILL.md for SharePoint Online (#1175).

**Platform Interoperability (#29, #16, #1102)**
Demand is growing to run Skills on AWS Bedrock (#29), expose Skills as MCP servers (#16), and address context bloat when MCP returns excess database data (#1102).

---

## 3. High-Potential Pending Skills

*These open PRs show strong momentum and are likely candidates for merging in the near term:*

| Skill | PR# | Rationale |
|-------|-----|-----------|
| **AURELION Suite** | [#444](https://github.com/anthropics/skills/pull/444) | High-complexity cognitive framework; deep community interest. |
| **ServiceNow Platform** | [#568](https://github.com/anthropics/skills/pull/568) | Major enterprise vertical; covers 10+ IT domains. |
| **Testing Patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Universal developer workflow; high surface area. |
| **ODT Skill** | [#486](https://github.com/anthropics/skills/pull/486) | Addresses a clear format gap (OpenDocument). |
| **n8n Builder/Debugger** | [#190](https://github.com/anthropics/skills/pull/190) | Strong workflow automation use case. |
| **Masonry AI (Image/Video)** | [#335](https://github.com/anthropics/skills/pull/335) | Brings Imagen/Veo generation to Claude Code. |
| **Document Typography** | [#514](https://github.com/anthropics/skills/pull/514) | Solves a subtle but universally felt quality problem. |

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is shifting from skill creation to skill management and enterprise hardening—governance, distribution infrastructure, platform security, and tooling reliability are now the critical bottlenecks over raw new functionality.**

---

# Claude Code Community Digest — 2026-05-27

## Today's Highlights
v2.1.152 ships a significant workflow upgrade: `/code-review --fix` now applies suggestions directly to the working tree, and `/simplify` delegates to this unified pipeline. The community is loudly signaling GitLab integration (94 👍) as the top missing feature, while a wave of documentation issues filed today suggests the docs are struggling to keep pace with rapid feature shipping. Desktop-mode reliability (macOS permissions, hook fidelity) remains a sore spot for power users.

---

## Releases
**v2.1.152** ([Release Link](https://github.com/anthropics/claude-code/releases/tag/v2.1.152))

- **`/code-review --fix`**: Code review is no longer purely advisory. The `--fix` flag directly applies findings (reuse, simplification, efficiency suggestions) to the working tree after analysis. `/simplify` has been rerouted to trigger this review pipeline, unifying the code improvement flow.
- **Skills `disallowed-tools`**: Skill and slash command authors can now define `disallowed-tools` in frontmatter for surgical tool restriction, moving beyond broader `allow`/`deny` patterns.

---

## Hot Issues

1. **#61415 — [BUG] Desktop: Bypass Permissions mode can't be enabled on macOS** (👍12, 💬43)
   A critical permissions flow is broken on macOS Desktop. Bypass Permissions reverts silently to Accept Edits with a "Permission mode couldn't be changed" error. Major blocker for Desktop adopters. The high comment count reflects numerous failed workaround attempts.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/61415)

2. **#12346 — [FEATURE] GitLab Integration (Repository Connection, MRs, Mobile Access)** (👍94, 💬36)
   The most upvoted open feature request by a wide margin. Users want full GitLab parity with the existing GitHub integration—repository linking, MR reviews, and mobile access.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/12346)

3. **#29716 — [BUG] WorktreeCreate / Remove hooks not called in Claude Desktop** (👍21, 💬17)
   Worktree lifecycle hooks are a core automation primitive. Their silent failure in Desktop breaks git-worktree workflows, forcing users back to the CLI.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/29716)

4. **#26954 — [BUG] Bash output truncated: ctrl+o/ctrl+e don't fully expand output** (👍22, 💬12)
   A long-standing UX friction point. Terminal output expansion commands can't reveal full content, consistently breaking log-inspection workflows.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/26954)

5. **#56593 — [BUG] Bash tool permanently fails with EEXIST on session-env mkdir (Windows)** (👍2, 💬3)
   The Bash tool becomes permanently broken mid-session on Windows due to a race condition in session-env directory creation, triggering spontaneously or after context compression.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/56593)

6. **#62678 — [BUG] Long URLs break when ctrl-clicked/copied due to line wrapping (Windows)** (👍0, 💬2)
   A terminal wrapping regression on Windows. Wrapped URLs are truncated, making links un-clickable and un-copyable.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/62678)

7. **#61376 — [BUG] MCP server 401 without RFC 9728 hint surfaces as 'Failed to connect'** (👍0, 💬3)
   Non-standard OAuth `WWW-Authenticate` headers cause a generic connection error instead of triggering the proper OAuth dance, complicating MCP server development and adoption.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/61376)

8. **#62679 — [BUG] hookify plugin: internal `from hookify.*` imports fail** (👍0, 💬1)
   A cautionary tale for plugin ecosystem maturity: the `hookify` plugin (v0.1.0) ships its code at the plugin root with no `hookify/` subdirectory, breaking every hook invocation at import time.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/62679)

9. **#58733 — [FEATURE] Add `/reload-skills` command to refresh skill discovery mid-session** (👍0, 💬5)
   Users developing or iterating on skills must currently restart the entire session to pick up changes. A dynamic reload command would significantly improve the development loop.  
   [Issue Link](https://github.com/anthropics/claude-code/issues/58733)

10. **#62682 — [FEATURE] Copy/paste loses rich formatting on macOS TUI** (👍0, 💬0)
    A core editing regression. Copying from the fullscreen TUI drops code formatting, breaking a fundamental developer workflow for moving code between environments.  
    [Issue Link](https://github.com/anthropics/claude-code/issues/62682)

---

## Key PR Progress

1. **#62586 — [CLOSED] Update security-guidance plugin**  
   Ships the latest version of the automated security reviewer, catching common vulnerabilities (injection, path traversal) at code-generation time rather than downstream.  
   [PR Link](https://github.com/anthropics/claude-code/pull/62586)

2. **#61742 — [OPEN] Document Agent View TUI working directory limitation**  
   Codifies a known constraint: agents spawned from the TUI inherit the parent's working directory. Documents the workaround (separate terminals/tmux panes). Closes #61546.  
   [PR Link](https://github.com/anthropics/claude-code/pull/61742)

3. **#62597 — [OPEN] fix: resolve 10 CI/script bugs**  
   A sweeping hardening of the project's CI pipeline: replaces hardcoded repo names with `GITHUB_REPOSITORY` env var fallbacks, adds safe event handling for scheduled workflows, and improves error output in label/edit scripts.  
   [PR Link](https://github.com/anthropics/claude-code/pull/62597)

4. **#62264 — [OPEN] feat: add block-build-commands hook example**  
   Introduces a `PreToolUse` hook template that serves as a hard execution guardrail. Blocks `cmake`, `make`, `cargo build`, `npm run build`, and other compilation commands from executing in the Bash tool.  
   [PR Link](https://github.com/anthropics/claude-code/pull/62264)

5. **#4943 — [OPEN] feat: add shell completions (bash, zsh, fish)**  
   A major quality-of-life PR open since August 2025. Provides static completion scripts for tab-autocompleting commands, flags, and arguments. Still pending, indicating internal deliberation or technical debt.  
   [PR Link](https://github.com/anthropics/claude-code/pull/4943)

6. **#60732 — [OPEN] polish plugins README wording**  
   Improves the introductory description of the plugin ecosystem for readability and clarity.  
   [PR Link](https://github.com/anthropics/claude-code/pull/60732)

7. **#60427 — [OPEN] docs: use standard GitHub capitalization in README**  
   Minor brand consistency fix.  
   [PR Link](https://github.com/anthropics/claude-code/pull/60427)

8. **#62622 — [CLOSED] fix: resolve 10 CI/script bugs (duplicate)**  
   Closed in favor of #62597.  
   [PR Link](https://github.com/anthropics/claude-code/pull/62622)

9. **#62592 — [CLOSED] Update security-guidance plugin README**  
   Companion documentation update for the security plugin.  
   [PR Link](https://github.com/anthropics/claude-code/pull/62592)

10. **#58673 — [OPEN] s**  
    Stub PR with a minimal single-character title; likely a test or incomplete submission.  
    [PR Link](https://github.com/anthropics/claude-code/pull/58673)

---

## Feature Request Trends

The community is coalescing around several key directions:

- **Platform Parity**: GitLab integration (#12346) dominates by raw reaction count, but requests for full feature parity between Desktop and CLI (hooks, permissions, panels) form a strong undercurrent.
- **Plugin API Maturation**: Users want richer skills/plugins—dynamic reloading (`/reload-skills`, #58733), configurable defaults (`default` field in `userConfig`, #46477), and stable packaging guidelines (hookify bugs #62679, #62683).
- **Terminal Ergonomics**: A push for professional-grade terminal behavior: clickable URLs (#62678), rich clipboard support (#62682), proper screen clearing discipline (#62681), and configurable sound effects (#59970).
- **Protocol & Standards Compliance**: The MCP OAuth issue (#61376) signals users expect strict RFC compliance for third-party integrations rather than opaque error handling.
- **Documentation Completeness**: A single user (`coygeek`) filed five documentation issues today alone (#62673–#62677), covering gaps in monitoring, fullscreen, fallback models, MCP deduplication, and turn duration settings. Docs are clearly lagging behind feature velocity.

---

## Developer Pain Points

- **Desktop Mode Instability**: macOS permissions (#61415) and hook fidelity (#29716) create a reliability gap between CLI and Desktop that frustrates desktop-first workflows.
- **Windows TUI & Bash Stability**: The Bash tool's `EEXIST` crash (#56593) and terminal wrapping issues (#62678) make the Windows experience fraught with blocking errors.
- **Plugin Ecosystem Brittleness**: The hookify packaging bug (#62679) perfectly illustrates the early-stage fragility of the plugin system. Lack of `default` fields (#46477), missing `reload-skills` (#58733), and unclear scoping rules (#62683) add daily friction.
- **Terminal Output Reliability**: The long-standing `ctrl+e` / full output issue (#26954) remains a persistent pain point for anyone reviewing lengthy command output or logs.
- **MCP Debugging Opacity**: Generic "Failed to connect" errors for non-standard OAuth (#61376) make debugging MCP server integrations unnecessarily difficult, slowing adoption.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-27

## 1. Today's Highlights
Codex CLI v0.134.0 shipped with an eagerly awaited local conversation history search, but a missing Linux x64 binary artifact is blocking adoption for a significant portion of the user base. A critical OAuth breakdown (`NoneType` error) is disrupting team workflows, while a widespread quality and speed regression continues to generate heat. The community also showed strong positive reaction to infrastructure PRs addressing SQLite migration safety and environment hook persistence.

## 2. Releases

**Codex CLI v0.134.0 (rust-v0.134.0)**
- **Local History Search**: Implements search across conversation history with case-insensitive matching and result previews. (#23519, #23921)
- **Profile Overhaul**: The `--profile` flag is now the primary mechanism for selecting profiles across CLI, TUI, sandbox, and permissions. Legacy profile configs are rejected automatically.
- **⚠️ Caveat**: A release-blocking issue (#24672) reports that the Linux x64 build artifact is missing from npm, causing the CLI to exit on startup.

## 3. Hot Issues

1. **#24665 — Hermes Agent OAuth Broken (`NoneType` error)**
   Multiple team members unable to authenticate. Core login flow is completely broken. 
   [View Issue](https://github.com/openai/codex/issues/24665)

2. **#24672 — Linux x64 v0.134.0 Install Failure**
   The latest CLI release cannot run on standard Linux x64 systems due to a missing platform binary.
   [View Issue](https://github.com/openai/codex/issues/24672)

3. **#20161 — Phone Verification Loop on SSO (Closed)**
   Previously widespread pain (169 comments, 104 👍) where SSO users were forced into phone verification. Closed but highlights deep auth friction.
   [View Issue](https://github.com/openai/codex/issues/20161)

4. **#13993 — Standalone Windows Installer Request**
   120 👍. Top feature request blocking corporate and offline Windows users who cannot use the Microsoft Store.
   [View Issue](https://github.com/openai/codex/issues/13993)

5. **#24649 — Widespread Slowdown and Quality Degradation**
   Users objectively reporting slower task completion and lower response quality over the last week. High sentiment risk.
   [View Issue](https://github.com/openai/codex/issues/24649)

6. **#24510 — Desktop High CPU from Metadata Bloat**
   Sustained high CPU usage due to unbounded processing of thread metadata (`title`, `preview`). Performance issue for heavy users.
   [View Issue](https://github.com/openai/codex/issues/24510)

7. **#24031 — GPT-5.5 1M Context Window Delayed/Closed**
   Community frustration over a promised feature (1M context for GPT-5.5) being abruptly closed without delivery or detailed communication.
   [View Issue](https://github.com/openai/codex/issues/24031)

8. **#24098 — Windows Elevated Sandbox Fails**
   `spawn setup refresh` error when running CLI as admin. Core Windows execution path is flaky.
   [View Issue](https://github.com/openai/codex/issues/24098)

9. **#2916 — API Service Tier Configuration**
   38 👍. Power users demanding control over OpenAI API service tiers for cost vs. latency optimization.
   [View Issue](https://github.com/openai/codex/issues/2916)

10. **#23979 — Conversation History Missing After Update**
    Critical data reliability concern. History disappears from UI post-update, though underlying SQLite data persists.
    [View Issue](https://github.com/openai/codex/issues/23979)

## 4. Key PR Progress

1. **#24690 — Revert Bedrock Mantle GovCloud Support**
   OpenAI walks back GovCloud support shortly after merging it, citing internal policy. Signals strict compliance boundaries.
   [View PR](https://github.com/openai/codex/pull/24690)

2. **#24684 — Rust Toolchain 1.95.0 Uprev**
   Standard infrastructure upgrade to leverage new Rust compiler features across the entire build pipeline.
   [View PR](https://github.com/openai/codex/pull/24684)

3. **#24650 — CODEX_ENV_FILE Hook Persistence**
   Brings Codex CLI to parity with Claude Code for environment management. Allows `SessionStart` hooks to persist `PATH` and virtualenv changes.
   [View PR](https://github.com/openai/codex/pull/24650)

4. **#24673 — Start Idle Turns Without Reservations**
   Refactors the goal continuation flow to avoid a "partial active" turn state, improving reliability of background task scheduling.
   [View PR](https://github.com/openai/codex/pull/24673)

5. **#24663 / #23546 — ChatGPT Token Refresh Serialization**
   Prevents auth failures during long requests by serializing refresh-token redemption across processes and proactively refreshing near-expiry tokens.
   [View PR](https://github.com/openai/codex/pull/24663)

6. **#21567 — Noninteractive Install Script Mode**
   Addresses a long-standing enterprise gap. The `CODEX_NON_INTERACTIVE` env var allows for automated deployment and CI/CD integration.
   [View PR](https://github.com/openai/codex/pull/21567)

7. **#24616 — Wrap SQLite Migrations in Transactions**
   Critically improves data safety during upgrades. Ensures migration failures trigger a full rollback instead of partial corruption.
   [View PR](https://github.com/openai/codex/pull/24616)

8. **#23950 / #24683 — Slash Command Draft Preservation**
   Excellent UX improvement. Users can now draft text, move the cursor, and type a slash command (e.g., `/review`) without losing the drafted text.
   [View PR](https://github.com/openai/codex/pull/23950)

9. **#24368 — Compaction Metadata in Turn Headers**
   Adds `request_kind` values to distinguish compaction, prewarm, and foreground turns. Improves observability for debugging context window issues.
   [View PR](https://github.com/openai/codex/pull/24368)

10. **#24669 / #24660 / #24693 — Standalone Web Search Refinements**
    Iterative improvement of the standalone `web.run` tool. Fixes schema budget stripping and adds progress feedback for extension-hosted searches.
    [View PR](https://github.com/openai/codex/pull/24669)

## 5. Feature Request Trends

- **Windows Platform Parity**: The demand for a standalone Windows `.exe` installer (#13993) is the single most upvoted open feature request. This is part of a broader pattern of Windows-specific sandbox and permission bugs (#22428, #24098) that suggest the Windows port lags significantly behind macOS/Linux.
- **IDE Deep Integration (VS Code/Cursor)**: Users are pushing for richer session management inside the IDE, specifically requesting tabbed chat interfaces (#12098) and persistent session lists that stay visible alongside active chats (#24594).
- **Cost Control & Observability**: There is a strong undercurrent of demand for API service tier configuration (#2916) and better quota transparency (#20153). Users want to optimize cost for heavy workloads and feel blindsided by rapid quota consumption.
- **Enterprise Readiness**: Features like `CODEX_NON_INTERACTIVE` installs (#21567), environment variable hooks (#24650), and MCP configuration fixes (#22105) point to growing enterprise adoption and a need for robust, automatable, and policy-compliant setups.

## 6. Developer Pain Points

- **Authentication & Authorization Friction**: This is the most painful recurring theme. OAuth `NoneType` crashes (#24665), SSO phone loops (#20161), and remote control auth failures (#22696) destroy trust in the foundational login flow.
- **Data Persistence Anxiety**: Users are uneasy about local state management. Issues regarding conversation history disappearing after updates (#23979), compaction failures (#20931), and high CPU usage from metadata bloat (#24510) suggest the local database model is under strain.
- **Unexplained Performance Regressions**: The sudden, widespread slowdown (#24649) and reports of quotas "draining like crazy" (#20153) indicate a lack of transparency when backend model configurations or throttling policies change. This generates significant community backlash.
- **Cross-Device Synchronization Gaps**: The Remote Control feature is generating friction. Devices can get stuck in an "authorized but unusable" state (#23865), and Locked Computer Use breaks on specific hardware (#24086). The multi-device story feels brittle.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest — May 27, 2026**

---

### 1. Today’s Highlights
Agent stability and security hardening dominated the conversation today, with a high-severity PR merging to fix an MCP blacklist bypass RCE vulnerability. While no new releases shipped, the P1 hang and subagent false-success bugs continue to generate significant community attention, and the strategic push toward AST-aware file operations (tracked across three workstream issues) signals a major upcoming shift in agent code comprehension. The Auto Memory subsystem also saw a batch of targeted quality and privacy fixes from the same author.

**No new releases in the last 24 hours.**

---

### 2. Hot Issues

##### [#24353] Robust Component Level Evaluations (P1, Epic)
**Link:** google-gemini/gemini-cli Issue #24353
Why it matters: This epic formalizes the behavioral eval framework, which now encompasses 76+ tests across 6 models. It is the linchpin for ensuring agent changes don't regress quality, and its progress directly impacts community trust in new releases.

##### [#22745] AST-Aware File Reads, Search & Mapping (P2, Strategic Epic)
**Link:** google-gemini/gemini-cli Issue #22745
Why it matters: The community strongly supports shifting from text-based grep to AST-aware methods for reading method bounds and searching syntax. If successful, this workstream promises sharp reductions in token waste and agent turn counts.

##### [#21409] Generalist Agent Hangs (P1, 8👍)
**Link:** google-gemini/gemini-cli Issue #21409
Why it matters: The top-voted pain point. Users report the agent hangs indefinitely when deferring to sub-agents for simple tasks like folder creation. The lone workaround—forcing the agent to never use sub-agents—defeats the tool’s core architecture.

##### [#22323] Subagent Recovery Reports False “Success” (P1)
**Link:** google-gemini/gemini-cli Issue #22323
Why it matters: A deceptive UX bug where hitting `MAX_TURNS` inside a sub-agent is reported externally as `status: “success”`. Misleading outcome reporting is dangerous in an autonomous coding context, as users may trust a result that was never delivered.

##### [#25166] Shell Command Execution Gets Stuck on “Awaiting Input” (P1, 3👍)
**Link:** google-gemini/gemini-cli Issue #25166
Why it matters: Commands complete successfully but the UI state remains “Waiting input”, blocking all downstream work. This is a critical workflow deadlock that has frustrated multiple users with reproducible cases.

##### [#21968] Model Ignores Custom Skills & Sub-Agents (P2)
**Link:** google-gemini/gemini-cli Issue #21968
Why it matters: Undermines the extensibility promise. Users report that the agent ignores custom “gradle” or “git” skills unless explicitly instructed, reducing the value of a significant community investment.

##### [#26525 / #26522 / #26523] Auto Memory Quality & Privacy Backlog (P2)
**Link:** google-gemini/gemini-cli Issues #26522 / #26523 / #26525
Why it matters: A focused push from a single author to fix three interconnected Auto Memory issues: (1) infinite retries on low-signal sessions, (2) silently skipping malformed patches instead of surfacing them, and (3) needing deterministic secret redaction before transcript content reaches model context.

##### [#21983] Browser Subagent Fails on Wayland (P1)
**Link:** google-gemini/gemini-cli Issue #21983
Why it matters: A platform blocker for modern Linux users. The browser agent is a marquee feature, and Wayland incompatibility prevents a significant Linux segment from using it at all.

##### [#24246] 400 Error with > 128 Tools (P2)
**Link:** google-gemini/gemini-cli Issue #24246
Why it matters: As the MCP ecosystem expands, power users regularly exceed the tool count limit, resulting in a hard API error. This is a scalability ceiling that needs addressing for the agent to support rich plugin setups.

##### [#25436] Unexpected “Request Cancelled” (P2, Closed as Duplicate)
**Link:** google-gemini/gemini-cli Issue #25436
Why it matters: Users report the agent cancels itself mid-task without any user input. The inherent trust hit from spontaneous cancellations makes this a high-sentiment issue even after triage.

---

### 3. Key PR Progress

##### [#27377] Fix MCP Blacklist Bypass (RCE)
**Link:** google-gemini/gemini-cli PR #27377
Impact: Closes a critical vulnerability where malicious workspace MCP servers could bypass `mcp.excluded` and `mcp.allowed` lists to start local processes. Security-critical patch.

##### [#27467] Fix Multi-line Escaped Quotes in Shell Wrapper
**Link:** google-gemini/gemini-cli PR #27467
Impact: Adopts `shell-quote` for parsing, fixing cases where `stripShellWrapper` failed on commands like `bash -c "hg commit -m \"title\n\nbody\""`.

##### [#27463] Preserve refresh_token in File-Based Credential Cache
**Link:** google-gemini/gemini-cli PR #27463
Impact: Addresses persistent auth invalidation for the default OAuth storage path, ensuring sessions don’t break due to dropped `refresh_token` fields.

##### [#27292] Restore Non-Interactive Stdin Raw Mode on Exit
**Link:** google-gemini/gemini-cli PR #27292
Impact: Ensures safe terminal cleanup in headless/CI modes when a Ctrl+C cancellation path is hit, preventing a broken TTY state.

##### [#27461] Suppress PTY Resize EBADF Crashes
**Link:** google-gemini/gemini-cli PR #27461
Impact: Prevents crashes when the terminal is resized while a PTY is exiting. This was exacerbated by recent UI layout changes that increased resize polling frequency.

##### [#27371] Handle EBADF on `gemini --resume`
**Link:** google-gemini/gemini-cli PR #27371
Impact: A P1 fix for session resume crashes caused by stale PTY file descriptors. Ensures long-lived sessions can be reliably restored.

##### [#27453] Re-seed Metadata on Mid-Session File Recreation
**Link:** google-gemini/gemini-cli PR #27453
Impact: Fixes a session corruption path where external cleanup deleting the conversation file mid-session would leave the file unparseable.

##### [#27365] Add `--ephemeral` Session Mode
**Link:** google-gemini/gemini-cli PR #27365
Impact: Community-driven feature for CI/CD and data annotation workflows, preventing headless task logs from flooding the user’s session history.

##### [#27054] Windows Image Pasting & Clipboard Styling
**Link:** google-gemini/gemini-cli PR #27054
Impact: Fixes Windows Terminal pasting and adds a clean UI for paste events, closing a long-standing platform parity gap.

##### [#27465] Surface Extension Enable/Disable Feedback
**Link:** google-gemini/gemini-cli PR #27465
Impact: Fixes a silent-fail UX issue where `gemini extensions disable` logged success only to a debug file, leaving users thinking the command was broken.

---

### 4. Feature Request Trends

- **AST-Aware Code Understanding (Dominant Theme):** The three-issue workstream (#22745, #22746, #22747) is the single most ambitious strategic direction surfacing right now. The community strongly desires replacing line-based grep and full-file reads with syntax-aware tooling to reduce latency and token costs.
- **Agent Self-Awareness & Safety:** Users want the agent to know its own flags, hotkeys, and limits (#21432) and to default to safe operations over destructive git or DB commands (#22672). This reflects a desire for the CLI to act as an expert peer, not a reckless assistant.
- **Backgroundable Sub-Agents:** Requests to background sub-agents with Ctrl+B (#22741) signal users increasingly treat the CLI as a multitasking development environment.
- **Server-Driven Configuration:** The epic for remote model routing (#20878) implies frustration with static local config and a desire for the CLI to dynamically adapt to backend model availability.

---

### 5. Developer Pain Points

- **Agent Loop Brittleness:** The top pain cluster. Hangs (#21409), deadlocks on shell commands (#25166), and false “success” reports from sub-agents (#22323) erode confidence in autonomous operation.
- **Configuration is Ignored:** Users report that settings.json values (maxTurns, permissions) (#22267) and disallowed agent modes (#22093) are silently overridden by the model, forcing users into constant supervision.
- **Terminal Crashes & Platform Gaps:** PTY crashes on resize (#27461, #27371) hit a raw nerve with multiplexer users. Wayland browser failures (#21983) and Windows keybinding gaps (#26088) continue to fractionalize the user base.
- **Opaque Errors & Silent Failures:** Spontaneous “Request Cancelled” (#25436) and extension commands with no terminal feedback (#27465) leave users debugging ghosts rather than working.
- **Memory System Complexity:** Auto Memory’s value is acknowledged, but its current fragility with patch validation (#26523), infinite low-signal retries (#26522), and privacy redaction gaps (#26525) generate a steady stream of nuance bugs.
- **Ecosystem Scalability Ceilings:** The 128-tool API limit (#24246) constrains power users who integrate deeply with the MCP ecosystem, blocking adoption for complex workflows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — 2026-05-27**

---

### 1. Today’s Highlights
A new patch release (`v1.0.55-1`) shipped today, bundling fixes for the disruptive Linux clipboard regressions introduced in 1.0.49 and improving the `/env` command. The community remains deeply engaged with enterprise rollout friction (MCP registry URLs, Remote Sessions) and long-standing input accessibility gaps. The highest-upvoted open issue—configurable IME submission keys—remains a critical unmet need for CJK-language developers.

---

### 2. Releases

**[Released] v1.0.55-1**
The team shipped a minor patch primarily focused on terminal UI polish and immediate regression fixes.

**Improvements**
- Increased selection background contrast across all color themes for better visibility.
- `/env` now displays loaded extensions with their status and source, addressing a long-standing environment visibility gap.

**Fixes**
- Terminal bell no longer sounds on turn completion unless explicitly enabled via config.
- Cleaned up placeholder text ("bla") in the `/resume` picker.

---

### 3. Hot Issues
*Selected for community reaction, platform coverage, and escalation status.*

1. **[#3385] [Bug] Can't run Copilot CLI 1.0.49 on WSL after upgrade**  
   *13 comments, 9 👍*
   Users on WSL 2 report the CLI stalls at startup. The issue has been open since May 19 without a resolution, leaving a large segment of Linux-adjacent developers pinned on older versions.  
   *Link: `github/copilot-cli Issue #3385`*

2. **[#2205] [Bug] Mouse scroll regression in terminal (Terminator)**  
   *10 comments, 12 👍*
   Since the 1.0.49 TUI rewrite, mouse scroll cycles through input history instead of navigating agent output. A severe UX regression for interactive users.  
   *Link: `github/copilot-cli Issue #2205`*

3. **[#3439] [Bug] 1.0.49 regression: TUI rendering lag inside tmux on mintty/Cygwin**  
   *7 comments*
   Burst rendering and spinner stutter under tmux on Windows, explicitly not present in 1.0.43 or 1.0.48. Points to a core terminal frame-handling defect.  
   *Link: `github/copilot-cli Issue #3439`*

4. **[#3442] [Bug] v1.0.51 — Remote sessions are not enabled**  
   *5 comments, 10 👍 (Closed)*
   A widespread false-positive warning for Enterprise users. Generated significant internal pressure before being resolved, but highlighted fragility in feature-flag propagation.  
   *Link: `github/copilot-cli Issue #3442`*

5. **[#3436] [Bug] /mcp search constructs wrong URL for custom MCP registries (/v0.1/ segment missing)**  
   *5 comments, 1 👍*
   Completely blocks MCP tool discovery for organizations running self-hosted registries. Requires manual URL patching to work around.  
   *Link: `github/copilot-cli Issue #3436`*

6. **[#1972] [Feature] Allow users to configure submit key (e.g., Ctrl+Enter) to prevent accidental IME submission**  
   *3 comments, 46 👍*
   The single most upvoted open issue. Users of CJK languages are forced to choose between their IME workflow and the CLI’s Enter-to-submit default.  
   *Link: `github/copilot-cli Issue #1972`*

7. **[#3534] [Bug] WSL2 (ARM64): /copy fails with clip.exe exit code 1 in 1.0.55**  
   *1 comment*
   A fresh regression in today’s patch: clipboard writes break on ARM64 WSL due to `cmd.exe` quoting issues. Indicates incomplete platform coverage in the clipboard rework.  
   *Link: `github/copilot-cli Issue #3534`*

8. **[#3508] [Bug] Extension lifecycle hooks receive empty workingDirectory since CLI ~1.0.51**  
   *2 comments (Closed)*
   A silent breaking change to the plugin API. Hooks like `onSessionStart` lose their working directory context, forcing extension authors to vendor workarounds.  
   *Link: `github/copilot-cli Issue #3508`*

9. **[#3529] [Bug] Copilot encountered an error and was unable to review this pull request**  
   *2 comments*
   A generic, opaque error for the PR Review feature. Users receive no actionable recovery path, eroding trust in the core review workflow.  
   *Link: `github/copilot-cli Issue #3529`*

10. **[#3459] [Bug] Copilot CLI auto-update check makes unauthenticated API request, causing rate limit errors in shared-NAT environments**  
    *1 comment (Support Escalation)*
    The automatic version check can poison GitHub API rate limits for entire teams behind a shared egress IP. A classic enterprise rollout landmine.  
    *Link: `github/copilot-cli Issue #3459`*

---

### 4. Key PR Progress
No pull requests were created or updated in the last 24 hours, indicating a stabilization cycle following the `v1.0.55-1` release. The most impactful contributions landed implicitly through this release, which resolved:
- **Linux Clipboard/Input Stability**: A cluster of Wayland and GNOME Terminal copy/paste regressions from 1.0.49 were closed (#3414, #3483, #3395, #3467).
- **Environment Visibility**: The new `/env` behavior directly ships the functionality requested in #3479.
- **Agent Profile Frontmatter**: Support for `skills:` lists in custom agent profiles (#3532) was merged and released, allowing richer prompt preloading.

---

### 5. Feature Request Trends

1. **Customizable Input Handling**: The dominance of the IME submit key request (#1972) reflects a growing international user base whose core workflow is broken by hardcoded keybindings. There is also a steady stream of requests to respect OS cursor and clipboard defaults (#2507).

2. **Programmatic & Non-Interactive Sessions**: Users increasingly want to script the CLI. Requests for flags to start sessions without the TUI (#3525) and persistent cross-session audit logs (#1791) both point to a desire for CI/CD and SDK integration.

3. **Agent Profile Extensibility**: The newly shipped `skills:` frontmatter (#3532) has validated the appetite for richer agent definitions. The community is looking for dynamic context injection, preloaded tools, and private agent registries.

4. **Enterprise-Grade MCP & Auth**: Beyond bug fixes (#3436), users are actively requesting Managed Identity support for Azure Foundry (#2705) and clearer MCP tool visibility for custom agents (#3337). The platform is being evaluated as an enterprise standard, and these gaps block adoption.

---

### 6. Developer Pain Points

1. **"1.0.49 Regression Fatigue"**: The most common pattern across complaints is "worked in 1.0.48, broken in 1.0.49"—affecting TUI rendering (#3439), Linux paste (#3414), WSL execution (#3385), and mouse scroll (#2205). Trust in the update cycle has been noticeably damaged.

2. **Plugin Ecosystem Instability**: Extension authors are absorbing breaking changes rapidly. Lifecycle hooks losing context (#3508) and unlisted extensions in `/env` (#3479) force plugin maintainers to constantly adapt or lose functionality.

3. **Opaque Error Handling**: Generic messages like "Copilot encountered an error" (#3529) or "Execution failed: CAPIError" (#2147) provide no actionable recovery path, forcing users to search or abandon workflows.

4. **Edge Case Fragmentation**: ARM64 WSL (#3534), Cygwin tmux (#3439), and GNOME Wayland (#3467) all experience platform-specific failures that stall for days or weeks. Developers on non-standard setups feel chronically deprioritized.

5. **Enterprise Rollout Friction**: The combination of auto-update rate limiting (#3459), MCP registry path errors (#3436), and false-positive Remote Sessions warnings (#3442) creates a hostile environment for organizational deployment and policy enforcement.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

### Kimi Code CLI Community Digest — 2026-05-27

---

#### 1. Today's Highlights
The Kimi Code CLI ecosystem is pivoting heavily toward **scalability and interoperability**. The v1.45.0 release bundles error handling cleanup and smarter AI loop deduplication, while the community’s loudest pain point—subagent API key rate limiting on concurrent tasks—has been met with an immediate architectural solution in the form of a new API Key Pool PR (#2369). The backlog is also seeing cleanup, with the long-standing `@mention` file path bug finally closed (#1774).

---

#### 2. Releases
While the formal releases tab shows no update, **v1.45.0** was published via merged PR (#2373) on May 26, bundling several recent quality and reliability patches:
- **Tool deduplication with "sparse reminders"** (#2372) to reduce token waste and avoid redundant model loops.
- **Fix for misleading "Quota exceeded" prefix** on generic 403 errors (#2342), cleaning up a major UX frustration.
- **Kill ring system clipboard config** (#2260) for terminal editor customization.
- **Logging improvements for hook task exceptions** (#1852) to replace silently swallowed errors with visible logs.

👉 [#2373 [Release PR]](MoonshotAI/kimi-cli PR #2373)

---

#### 3. Hot Issues
*7 items updated in the last 24 hours, analyzed below.*

1. **#2368 [OPEN] Foreground subagents exhaust API key rate limit**
   *Why it matters:* The top scaling blocker. Running 3–4 concurrent `coder` or `explore` agents hits a hard 429 ceiling, preventing the community from using Kimi Code’s multi-agent architecture effectively. Zero comments on the issue, but a targeted PR (#2369) landed instantly, reflecting high internal/community alignment on its severity.
   👉 [#2368](MoonshotAI/kimi-cli Issue #2368)

2. **#2208 [OPEN] OpenAI-compatible API endpoint**
   *Why it matters:* A strategic “platform” request to let Kimi models serve as drop-in replacements in Cursor, Continue.dev, and Windsurf. High strategic value, though reaction volume is low (0 👍) as the vocal power-user base seems to be waiting for action.
   👉 [#2208](MoonshotAI/kimi-cli Issue #2208)

3. **#2367 [OPEN] ReadMediaFile returns 400 error**
   *Why it matters:* A fundamental I/O function (`favicon.ico` read) failing with a generic 400 error undermines trust in the provider stack. Attracts 1 👍 from other users hitting similar opaque errors.
   👉 [#2367](MoonshotAI/kimi-cli Issue #2367)

4. **#2141 [OPEN] DeepSeek V4 `reasoning_content` multi-turn tool call failure**
   *Why it matters:* Strict protocol adherence is required for “thinking” models. Multi-turn conversations with tool calls fail entirely. The author demonstrates deep spec knowledge, showing the user base is technically demanding.
   👉 [#2141](MoonshotAI/kimi-cli Issue #2141)

5. **#2317 [OPEN] VSCode extension: plan mode file path not clickable**
   *Why it matters:* Table-stakes IDE UX is missing. Clickable file paths in chat webview are required for production-grade extensions. No fix PR attached yet.
   👉 [#2317](MoonshotAI/kimi-cli Issue #2317)

6. **#2370 [OPEN] Steer (⚡) button for Web UI queue**
   *Why it matters:* The community wants the `kimi web` interface to act as a heavy-duty agent workstation, not a simple chat. Queue prioritization is a mature UX request.
   👉 [#2370](MoonshotAI/kimi-cli Issue #2370)

7. **#1774 [CLOSED] @mention file path error (home directory resolution)**
   *Why it matters:* This fix closes a long-standing bug (opened April 7) on Darwin systems where `~` in `@mention` paths failed. Demonstrates healthy backlog cleanup.
   👉 [#1774](MoonshotAI/kimi-cli Issue #1774)

---

#### 4. Key PR Progress
*6 items updated, all directly tied to the community’s top concerns.*

1. **#2369 [OPEN] feat: API Key Pool for parallel subagent execution**
   *Analysis:* The most significant PR in this window. Introduces `llm_key_pool.py` with a round-robin allocator to distribute requests across multiple API keys, directly solving #2368. If merged, this unblocks practical concurrent multi-agent workflows.
   👉 [#2369](MoonshotAI/kimi-cli PR #2369)

2. **#2372 [CLOSED] feat: Tool dedup with sparse reminders and canonical args**
   *Analysis:* A smart core optimization. After a tool is used, subsequent calls get a short reminder instead of the full tool spec, saving significant context. Also makes `/clear` a true alias for `/new`.
   *Status:* Merged into v1.45.0.
   👉 [#2372](MoonshotAI/kimi-cli PR #2372)

3. **#2373 [CLOSED] chore: bump to v1.45.0**
   *Analysis:* Standard release housekeeping—version bump, changelog sync, wrapper pinning.
   👉 [#2373](MoonshotAI/kimi-cli PR #2373)

4. **#2342 [CLOSED] fix: Remove misleading "Quota exceeded" prefix from all 403 errors**
   *Analysis:* Targeted shell UX fix. The previous implementation slapped a quota warning on every 403, regardless of the real cause (auth, region, etc.). Good developer hygiene.
   *Status:* Merged into v1.45.0.
   👉 [#2342](MoonshotAI/kimi-cli PR #2342)

5. **#2260 [CLOSED] feat: `kill_ring_system_clipboard` config option**
   *Analysis:* Community-driven terminal customization. Shows the maintainers are responsive to power-user editor workflows.
   *Status:* Merged into v1.45.0.
   👉 [#2260](MoonshotAI/kimi-cli PR #2260)

6. **#1852 [CLOSED] fix: Log hook task exceptions instead of silently discarding**
   *Analysis:* Crucial for observability. Previously, failures in `PreToolUse`, `PostLLM`, and `SubagentStop` callbacks were swallowed with `lambda t: t.exception() if not t.cancelled() else None`. Now properly logged, greatly aiding plugin and extension debugging.
   *Status:* Merged.
   👉 [#1852](MoonshotAI/kimi-cli PR #1852)

---

#### 5. Feature Request Trends
The last 24 hours crystallize four clear community-demand vectors:

- **Ecosystem Interoperability:** The OpenAI-compatible API request (#2208) is the single highest-leverage feature—it would transform Kimi Code from a standalone CLI into infrastructure for the existing IDE ecosystem.
- **Agent Scaling Infrastructure:** Power users are hitting hard architectural ceilings with concurrent subagents (#2368). Feature requests are shifting from “how to use” to “how to scale.”
- **Web UI as Power Tool:** Users expect granular task queue management (Steer button, #2370), moving the Web UI beyond simple chat.
- **Strict Provider Compatibility:** DeepSeek’s `reasoning_content` spec adherence (#2141) shows users expect rigorous implementation of provider protocols, not loose approximations.

---

#### 6. Developer Pain Points
- **Opaque API Errors:** Non-specific 400 (#2367) and misleading 403 (#2342) messages create significant debugging overhead. The shell UX fix is a welcome step, but a general push for lower-level error surfacing is visible.
- **Concurrency Ceilings:** The single-API-key rate limit for subagents (#2368) forces power users into sequential workflows or requires hacky manual key rotation. This is the #1 friction point for advanced developers.
- **Extension UX Gaps:** The VSCode extension (#2317) still lacks basic expected features (clickable file paths), creating a perception of immaturity versus the polished CLI.
- **Hybrid Workflow Friction:** Mixing providers (e.g., Kimi + DeepSeek) reveals incompatibilities (#2141) that slow down experimental multi-model routing.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode Community Digest — 2026-05-27

### 1. Today's Highlights
A major wave of stability patches landed today, with contributor **YOMXXX** merging over a dozen critical fixes targeting process management, task-tool fallbacks, shell output draining, and session prompt loops. The community remains highly vocal about OpenAI provider reliability, as issues #29129 and #29079 together crossed 100 reactions, with users reporting streaming freezes and multi-minute latency on simple prompts. On the feature side, the long-awaited `/goal` plugin PR (#28610) was submitted, reflecting strong demand for native session lifecycle management.

### 2. Releases
No releases were published in the last 24 hours. Given the high volume of merged bug-fix PRs, a point release (likely v1.15.11) is expected soon to deliver the accumulated improvements.

### 3. Hot Issues

1. **OpenAI Streaming Freeze (#29129)**  
   OpenCode intermittently enters a "working" state with high CPU usage and no output. 45 👍 indicate this is the community's top reliability concern.  
   [View Issue](https://github.com/anomalyco/opencode/issues/29129)

2. **GPT Models Response Latency (#29079)**  
   Users report simple commands taking minutes with GPT 5.4. High frustration reflected in 40 👍 and 58 comments.  
   [View Issue](https://github.com/anomalyco/opencode/issues/29079)

3. **Agent Sandboxing (#2242)**  
   47 👍 and 37 comments, the top unaddressed security feature. Users want to restrict agent file/terminal access to the current directory.  
   [View Issue](https://github.com/anomalyco/opencode/issues/2242)

4. **Native Session Goals / `/goal` (#27167)**  
   36 👍, now gaining momentum as a PR (#28610) has been opened. Users want persistent, multi-turn session goals.  
   [View Issue](https://github.com/anomalyco/opencode/issues/27167)

5. **Free Model Usage Confusion (#15585)**  
   43 comments. Users hitting "free usage exceed" errors on truly free models seek clarity on limits.  
   [View Issue](https://github.com/anomalyco/opencode/issues/15585)

6. **Adjust Go Limits Post DeepSeek V4 Price Cut (#28846)**  
   32 👍. Community pushing OpenCode to reflect DeepSeek's 75% price reduction in subscription usage tiers.  
   [View Issue](https://github.com/anomalyco/opencode/issues/28846)

7. **Tool Name Parsing Bug (#4279)**  
   Models such as Kimi K2 call tools with a leading space (e.g. `" bash"` instead of `"bash"`), causing loops and wasted quota.  
   [View Issue](https://github.com/anomalyco/opencode/issues/4279)

8. **Skill Library Overload (#29462)**  
   The `skill` tool has no upper bound on skill injection into the system prompt, risking major token waste in large repos.  
   [View Issue](https://github.com/anomalyco/opencode/issues/29462)

9. **Subagents Require Billing (#28362)**  
   Users with fully external/local providers are blocked by `task()` requiring OpenCode workspace billing.  
   [View Issue](https://github.com/anomalyco/opencode/issues/28362)

10. **Output Token Cap Silent Limit (#29363)**  
    `limit.output` is silently capped at 32K. The only escape hatch is an experimental env var, frustrating DeepSeek/Llama users.  
    [View Issue](https://github.com/anomalyco/opencode/issues/29363)

### 4. Key PR Progress

1. **feat: add /goal plugin (#28610)** — NathanKong76  
   Implements the native session goal feature, directly closing the top community feature request #27167.  
   [View PR](https://github.com/anomalyco/opencode/pull/28610)

2. **fix: fail task on empty subagent output (#29239)** — YOMXXX  
   Ensures empty task results correctly trigger model fallbacks instead of silently returning nothing.  
   [View PR](https://github.com/anomalyco/opencode/pull/29239)

3. **fix: report process exit before stdio close (#29476)** — YOMXXX  
   Resolves a background child process hang where detached descendants prevented proper exit tracking.  
   [View PR](https://github.com/anomalyco/opencode/pull/29476)

4. **fix: wait for shell output drain (#29230)** — YOMXXX  
   Fixes a race condition where `ShellTool.run` could return before the output reader finishes reading.  
   [View PR](https://github.com/anomalyco/opencode/pull/29230)

5. **fix(acp): flush updated text chunks (#29492)** — YOMXXX  
   Directly addresses the JetBrains ACP DeepSeek V4 truncation issue (#29488) that left streaming output incomplete.  
   [View PR](https://github.com/anomalyco/opencode/pull/29492)

6. **fix: stop prompt loop by assistant parent (#29480)** — YOMXXX  
   Kills an infinite prompt loop caused by flawed last-message detection in session state.  
   [View PR](https://github.com/anomalyco/opencode/pull/29480)

7. **fix: recover stale snapshot index locks (#29415)** — YOMXXX  
   Introduces recovery for corrupted git index locks, preventing crashes after an unclean shutdown.  
   [View PR](https://github.com/anomalyco/opencode/pull/29415)

8. **fix: resolve spawn on exit (#29108)** — divitkashyap  
   Stops cross-spawn from stalling on shutdown by not waiting for detached child stdio to close.  
   [View PR](https://github.com/anomalyco/opencode/pull/29108)

9. **fix: resolve absolute glob roots (#29466)** — YOMXXX  
   Corrects the Glob tool's handling of absolute patterns so they search from the project root correctly.  
   [View PR](https://github.com/anomalyco/opencode/pull/29466)

10. **fix: require read before write overwrite (#29467)** — YOMXXX  
    Enforces the documented contract that Write tool cannot overwrite files that haven't been read first.  
    [View PR](https://github.com/anomalyco/opencode/pull/29467)

### 5. Feature Request Trends

- **Session Lifecycle Management** is the dominant request cluster. Users want persistent goals (`/goal` #27167), visual session trees (`/tree` #22067), and the ability to disable editor context auto-attachment for multi-window isolation (#24270).
- **Security Controls** continue to grow in demand, with agent sandboxing (#2242) leading the pack. Users also want enforceable permission rule objects for web tools.
- **Provider Economics** are under scrutiny. The community is pressuring for usage tiers that track API price cuts (#28846) and removal of billing friction for fully local/BYOK setups (#28362).
- **UI Polish** remains steady: default expanded reasoning blocks (#29456), global language settings (#9610), and ACP/IDE feature parity (#29488) are all recurring themes.

### 6. Developer Pain Points

- **Fallback System Unreliability:** The fallback chain fails silently on empty task output (#29054) and infinite socket hangs (#29470, #29129), leaving users stranded without error feedback.
- **Configuration Surprises:** The 32K output token cap (#29363), unexpected billing checks for subagents (#28362), and user-info crashes in containers (#29292) erode trust in defaults.
- **OpenAI Provider Degradation:** A significant segment of users reports BigPickle outperforming the native OpenAI provider in speed and stability (#29312, #29079), creating churn risk.
- **Terminal & CI Hardening:** Multiplexer support (zellij/tmux notifications, #29099) and container compatibility issues point to a need for better headless/embedded environments.
- **Tool-Call Fragility:** Simple parsing errors (e.g. leading space in tool names, #4279) cascade into session derailment, highlighting fragility in LLM-tool interface hygiene.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi community digest for 2026-05-27.

---

## Pi Community Digest — 2026-05-27

### 1. Today's Highlights
The Pi community is seeing intense focus on reliability and terminal compatibility today. Critical patches land for the `openai-codex` hang and silent provider retry loops, directly addressing major user disruptions. Simultaneously, keyboard negotiation overhauls resolve long-standing Zellij conflicts, while progress on device code login and stream timeouts pushes Pi towards more robust headless and resilient workflows.

### 2. Releases
No new package versions were published in the last 24 hours.

### 3. Hot Issues

1. **#4945 (Open): openai-codex can hang on Working...** – The most active issue. Users report the TUI silently freezing on "Working..." after aborted turns or stream failures, requiring manual Escape intervention. High community engagement (28 comments, 16 👍). (earendil-works/pi Issue #4945)

2. **#3357 (Open): Official local LLM provider extension** – The top-voted feature request (31 👍). Users strongly desire dynamic model list fetching from `{baseUrl}/models` for seamless integration with llama.cpp, ollama, and LM Studio. (earendil-works/pi Issue #3357)

3. **#4990 (Closed): Edits failing** – A critical regression post-update where the `edit` tool fails validation with "must have required properties edits." The author explicitly regrets updating, highlighting the community’s stabilization phase. (earendil-works/pi Issue #4990)

4. **#5031 (Closed): pi -p prints nothing when piped** – Non-interactive text mode fails to write the assistant response to stdout when the prompt is piped via stdin. Exit code is 0, making it a silent blocker for CI/CD and script integrations. (earendil-works/pi Issue #5031)

5. **#4943 (Closed): OpenRouter context overflow not detected** – OpenRouter providers returning input length exceeded errors are not recognized, causing expensive infinite retry loops instead of triggering automatic compaction. (earendil-works/pi Issue #4943)

6. **#4927 (Closed): Cyrillic display name ByteString crash** – Header encoding bug blocks users with non-ASCII ChatGPT OAuth profile names. Highlights internationalization gaps in the Codex HTTP client layer. (earendil-works/pi Issue #4927)

7. **#5033 (Closed): Keyboard broken in Zellij** – False-positive detection of full Kitty keyboard protocol inside the Zellij mux kills native Alt and Shift+Enter bindings. A classic terminal compatibility challenge. (earendil-works/pi Issue #5033)

8. **#5035 (Closed): Telegram getUpdates polling conflicts** – Background sub-agents inherit parent environment variables, leading to conflicting Telegram Bot API long-polling sessions. Highlights emergent complexity in multi-agent architectures. (earendil-works/pi Issue #5035)

9. **#5018 (Closed): Deterministic named session resumption** – Users running multiple Pi instances in tmux/cmux request predictable, nameable sessions for workflow orchestration. Current behavior is described as "all broken." (earendil-works/pi Issue #5018)

10. **#5009 (Closed): kimi-code ban due to Pi usage** – A concerning data point where users report being banned from third-party API subscriptions. Raises awareness about the risks of aggressive API usage patterns and provider dependency. (earendil-works/pi Issue #5009)

### 4. Key PR Progress

1. **#5050 (Merged): Propagate runtime state to running agent loops** – Extensions calling `setModel()` etc. from tool result handlers now apply changes immediately instead of waiting for the next user turn. Essential for dynamic workflow extensions. (earendil-works/pi PR #5050)

2. **#5022 (Merged): Intl.Segmenter Unicode word boundaries** – A quality-of-life fix for the editor, leveraging the Web API for correct Unicode text selection and movement. Addresses long-standing TUI frustrations for international users. (earendil-works/pi PR #5022)

3. **#4979 (Open): Codex websocket timeouts** – Implements connection idle and connect timeouts for Codex, specifically targeting the "Working..." hang by ensuring stale connections eventually fail cleanly. (earendil-works/pi PR #4979)

4. **#4991 (Merged): Disable hidden provider 429 retries** – Stops trusting the `retry-after` header blindly from providers. Prevents infinite loops on quota exhaustion (e.g., Codex overage measured in days). Directly improves core stability. (earendil-works/pi PR #4991)

5. **#5037 (Open): JetBrains terminal capabilities** – Declares true color support for Pi running inside JetBrains IDEs, expanding the supported terminal ecosystem. (earendil-works/pi PR #5037)

6. **#5036 (Merged): Raw prompt template arguments** – Adds `$RAW_ARGUMENTS` support for prompt templates, allowing multi-line pasted text to be preserved without quoting. A powerful new tool for skill/prompt template authors. (earendil-works/pi PR #5036)

7. **#5032 (Merged): Progressive keyboard negotiation** – Fixes the Zellij keyboard conflict by correctly querying the terminal level and only enabling full Kitty protocol when the terminal directly supports it, not just any `CSI ? u` reply. (earendil-works/pi PR #5032)

8. **#5030 (Merged): Stream idle timeout watchdog** – Adds configurable idle timeouts for provider streams, preventing silent hangs during inference. (earendil-works/pi PR #5030)

9. **#5029 (Open): Abort in-flight LLM call on AgentSession.dispose()** – Prevents abandoned token generation and orphaned HTTP requests when users switch or fork sessions mid-stream. Critical for cost efficiency and agent loop hygiene. (earendil-works/pi PR #5029)

10. **#4911 (Open): Codex device code login** – Implements the highly requested device flow authentication for Codex, unlocking Pi for use in headless SSH environments without a local browser callback. (earendil-works/pi PR #4911)

### 5. Feature Request Trends
- **Local Model Sovereignty:** The #1 single issue by votes is seamless local LLM integration ([#3357](earendil-works/pi Issue #3357)), driven by cost, privacy, and offline deployment needs.
- **Extension API Maturation:** A surge in requests for deeper extension APIs (runtime state access, background processes [#4850](earendil-works/pi Issue #4850), typed settings schemas [#4981](earendil-works/pi Issue #4981)) signals an active plugin ecosystem pushing core boundaries.
- **Terminal Ecosystem Expansion:** Users are demanding first-class support for diverse terminals (Zellij [##5033](earendil-works/pi Issue #5033), JetBrains [##5037]), moving beyond macOS Terminal/iTerm2 assumptions.
- **Session Management Control:** Deterministic naming ([#5018](earendil-works/pi Issue #5018)) and settings scoping ([#5046](earendil-works/pi Issue #5046)) reflect power-user needs for orchestrating complex, multi-session workflows.

### 6. Developer Pain Points
- **Post-Update Regressions:** Users are wary of updates ([#4990](earendil-works/pi Issue #4990)), signalling that Pi is in a stabilization phase where disruption to the core `edit` workflow is a critical trust-breaker.
- **Non-Interactive Mode Reliability:** Silent failures in `pi -p` piped mode ([#5031](earendil-works/pi Issue #5031)) block CI/CD adoption, a key growth area for any CLI developer tool.
- **Terminal Fragility:** Native keyboard shortcuts breaking in popular multiplexers like Zellij ([#5033](earendil-works/pi Issue #5033)) creates deep daily friction. Graphical rendering issues ([#4883](earendil-works/pi Issue #4883)) compound terminal chaos.
- **Internationalization Gaps:** Encoding crashes with non-ASCII characters ([#4927](earendil-works/pi Issue #4927)) show I18n coverage is still nascent in critical web-facing HTTP/header layers.
- **Settings Architecture Confusion:** Unclear setting precedence ([#5046](earendil-works/pi Issue #5046)) and unintuitive version update logic ([#4929](earendil-works/pi Issue #4929)) indicate the configuration system needs clearer user-facing design.
- **Provider Dependency Risks:** The kimi-code ban reports ([#5009](earendil-works/pi Issue #5009)) serve as a stark reminder of the third-party API dependency risk inherent in AI tools, prompting community discussions around failover and moderation of request patterns.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date:** 2026-05-27

## 1. Today's Highlights
The "Mode B" daemon (`qwen serve`) ecosystem is maturing rapidly, with significant architectural pushes including ACP/MCP bridge protocols and a formal L2 capability layering refactor. Memory pressure in long sessions remains the community's top pain point, but the team is responding with proactive monitoring (`#4403`) and telemetry infrastructure (`#4565`). Build stability also gets attention with a targeted TS5055 fix in the v0.16.1 preview release.

## 2. Releases

- **[v0.16.1-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.16.1-preview.0) / [v0.16.1-nightly.20260527](https://github.com/QwenLM/qwen-code/releases/tag/v0.16.1-nightly.20260527):** Patch releases fixing a TypeScript build issue (`TS5055`—stale outputs causing compilation failures). Includes only build tooling and chore commits. Previews the upcoming v0.16.1 stable.

- **[sdk-typescript-v0.1.8-preview.0/1](https://github.com/QwenLM/qwen-code/releases):** SDK releases bundling CLI version 0.16.1 for integration consumers. No functional SDK changes flagged beyond the updated CLI dependency.

## 3. Hot Issues

1. **[#4175 — Mode B Feature Roadmap (40 comments)](https://github.com/QwenLM/qwen-code/issues/4175)**  
   The central tracking issue for producing a stable `qwen serve`. Covers the HTTP/SSE surface, auth defenses, and session multiplexing. Active community alignment on priorities for F1–F5 milestones.

2. **[#3803 — Daemon Design Proposal (25 comments)](https://github.com/QwenLM/qwen-code/issues/3803)**  
   The foundational 6-chapter design series (by wenshao) guiding the daemon architecture. Continues to serve as the decision record for protocol choices and workspace lifecycle.

3. **[#4514 — Daemon Capability Gaps (10 comments)](https://github.com/QwenLM/qwen-code/issues/4514)**  
   Tracks remaining gaps in the HTTP/SSE surface for remote clients beyond the existing slash-command passthrough. Driving concrete PRs (see `#4552`, `#4563`). High-priority for remote agent workflows.

4. **[#4149 — OOM in Long Sessions (12 comments)](https://github.com/QwenLM/qwen-code/issues/4149)**  
   "Ineffective mark-compacts near heap limit" crashes. Reproduced across multiple model providers. Community suspects large diffs, tool outputs, and `/compress` cycles as triggers. Opened by Aleks-0.

5. **[#4317 — Auth 504 Gateway Time-out (4 comments)](https://github.com/QwenLM/qwen-code/issues/4317)**  
   OAuth device token polling fails with HTTP 504, blocking user login. Affects Google SSO path specifically. Critical UX blocker for impacted users.

6. **[#4326 — MCP Spring AI Incompatibility (2 comments)](https://github.com/QwenLM/qwen-code/issues/4326)**  
   MCP client fails to maintain stable connections with Spring AI Streamable HTTP servers due to unsupported GET methods. Tagged `welcome-pr`—a clear opportunity for external contributors.

7. **[#2922 — Notification Hooks (3 comments)](https://github.com/QwenLM/qwen-code/issues/2922)**  
   Long-running feature request for sound/callback hooks on task completion and approval requests. Community signals strong interest in non-blocking workflow awareness.

8. **[#4493 — JetBrains Rider Login Failure (3 comments)](https://github.com/QwenLM/qwen-code/issues/4493)**  
   Users on JetBrains IDEs (Rider) report stuck OAuth redirects that cannot reach the Aliyun token plan. Indicates gaps in IDE companion parity vs VSCode.

9. **[#4361 — Global Hooks Ignored (3 comments)](https://github.com/QwenLM/qwen-code/issues/4361)**  
   Hooks placed in `~/.qwen/hooks` are silently bypassed. Root cause under investigation. Erodes confidence in the extensibility story for power users.

10. **[#4562 — Windows Shell Execution (2 comments)](https://github.com/QwenLM/qwen-code/issues/4562)**  
    User reports `!` commands fail under cmd.exe and asks for PowerShell by default. Platform-specific friction point for Windows developers.

## 4. Key PR Progress

1. **[!4563 — Refactor DaemonWorkspaceService](https://github.com/QwenLM/qwen-code/pull/4563)**  
   Extracts workspace-scoped capabilities (File/Auth/Agents/Memory) from `AcpSessionBridge` into a new `DaemonWorkspaceService` facade. Implements the L2 layering strategy proposed in `#4542`. By @doudouOUC.

2. **[!4555 — Serve-Bridge MCP Server](https://github.com/QwenLM/qwen-code/pull/4555)**  
   Introduces `qwen-serve-bridge`, enabling any MCP-compatible client (Claude Desktop, Cursor, Qoder) to interact with the Qwen daemon via stdio. Major unlock for ecosystem integration. By @jifeng.

3. **[!4472 — ACP Streamable HTTP Transport](https://github.com/QwenLM/qwen-code/pull/4472)**  
   Implements Agent Client Protocol (RFD #721) as a second northbound daemon path at `/acp`. Shares workspace scoping with the existing REST API. By @chiga0.

4. **[!4403 — Memory Pressure Monitor](https://github.com/QwenLM/qwen-code/pull/4403)**  
   Adds proactive runtime memory handling: container-aware limits, conservative cache cleanup, and diagnostic events for stalled GC cycles. Directly targets the OOM plague. By @ZevGit.

5. **[!4565 — Telemetry Foundation for RT Optimization](https://github.com/QwenLM/qwen-code/pull/4565)**  
   Lays data collection groundwork for agent loop response-time improvements. Zero performance impact initially—designed for P1.5 data-driven tuning. By @gwinthis.

6. **[!4559 — Daemon File Logger](https://github.com/QwenLM/qwen-code/pull/4559)**  
   Adds configurable per-process debug logging to `~/.qwen/debug/daemon/`. Essential for diagnosing daemon lifecycle issues in production deployments. By @doudouOUC.

7. **[!4552 — Runtime MCP Server Add/Remove](https://github.com/QwenLM/qwen-code/pull/4552)**  
   Closes daemon capability gap T2.8 from `#4514`. Adds HTTP endpoints for adding/replacing MCP servers without daemon restart. By @doudouOUC.

8. **[!4564 — Token Usage Stats](https://github.com/QwenLM/qwen-code/pull/4564)**  
   Persists daily/monthly token consumption with model and auth-type breakdowns. Exportable as CSV/JSON via `/stats`. Addresses growing cost-visibility demand. By @shenyankm.

9. **[!4533 — `/skills` Picker Dialog](https://github.com/QwenLM/qwen-code/pull/4533)**  
   Transforms bare `/skills` into an interactive dialog for browsing, searching, and toggling skills. Adds workspace-scoped `skills.disabled` config. UX polish for a core workflow. By @callmeYe.

10. **[!4544 — Auto-prepend @ for Multi-file Paste/Drop](https://github.com/QwenLM/qwen-code/pull/4544)**  
    Fixes a long-standing UX inconsistency where multi-file drag-and-drop did not automatically add the `@` prefix, while single-file operations did. By @MikeWang0316tw.

## 5. Feature Request Trends

**Daemon / Server Mode (Mode B) Domination:** The overwhelming direction of new feature work is making `qwen serve` production-ready: protocol standardization (ACP, MCP bridges), dynamic configuration, and lifecycle management. The community actively participates in shaping the roadmap through `#4175` and `#4514`.

**Observability as a First-Class Feature:** Users increasingly demand cost and performance visibility. Token usage tracking (`#4564`) and telemetry infrastructure (`#4565`) are the leading edge of a shift toward data-driven workflow optimization.

**Extensibility via MCP:** The PRs adding MCP server bridges signal strong intent to let users plug custom tools and data sources into the daemon without modifying core code. "Runtime MCP add/remove" (`#4552`) points toward a dynamic plugin ecosystem.

**Memory Management Transitioning to Feature Work:** Once purely a bug category, OOM handling is now spawning dedicated engineering work (pressure monitors, telemetry). This reflects a commitment to supporting long-running, context-heavy sessions.

## 6. Developer Pain Points

**Memory Exhaustion (OOM):** The single largest source of friction. Multiple reports this week alone (`#4149`, `#4276`, `#4351`, `#4399`) confirm that heap limits are routinely hit in long sessions with large tool outputs. Users resort to launching with increased `--max-old-space-size` as a fragile workaround.

**Authentication Fragility:** Flaky OAuth token polling (504 errors, `#4317`) and IDE-specific login flow breaks (Rider, `#4493`) cause frequent workflow interruptions. The auth surface lacks the resilience needed for daily professional use.

**IDE Ecosystem Parity:** JetBrains users continue to report gaps in plugin support vs VSCode—most critically in authentication and feature discovery. This risks platform lock-in for teams with mixed IDE preferences.

**Configuration Reliability:** Silent failures (global hooks ignored, `#4361`) and settings JSON corruption erode trust in the extensibility layer. Power users rely on these knobs but report unpredictable behavior.

**Platform-Specific Rough Edges:** Windows developers face shell execution issues (cmd vs PowerShell, `#4562`) and multi-file input handling quirks. While the team is addressing these incrementally, the experience remains less polished than on macOS/Linux.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-05-27

## Today's Highlights

The project **officially rebranded to CodeWhale**, shipping deprecation shims in v0.8.45/v0.8.46. A wave of stability fixes landed in the v0.8.47 rollup (PR #2233), addressing critical deadlocks and paste handling bugs. Meanwhile, a major typed permission system (PR #2242) and a Xiaomi MiMo provider integration (PR #2240) signal the ecosystem's expansion beyond the original DeepSeek-first identity. Community velocity remains high, but platform stability issues on Windows and Wayland continue to dominate developer pain points.

## Releases

- **v0.8.45 / v0.8.46** — Project renamed to **CodeWhale**. Legacy `deepseek` and `deepseek-tui` binaries ship as deprecation shims, printing a one-line warning and forwarding to `codewhale` / `codewhale-tui`. These shims will be removed in v0.9.0.
- **v0.8.47** (PR #2233) — Composed of 9 community PRs. Key changes include the critical RwLock→Semaphore deadlock fix in tool runtime, composer text selection with copy/cut, project context tracing, and session load auto-model restoration.

## Hot Issues

1. **[#1615] Docker Encoding Ruins Experience** ([Issue](https://github.com/Hmbown/CodeWhale/issues/1615))
   - *Status:* Closed | *Comments:* 190
   - User reports immediate garbled text (`乱码`) when running the official Docker image despite following instructions precisely. Extremely high emotional engagement, requiring a Linux server restart. Highlights a broken onboarding path for non-English environments.

2. **[#2165] CJK Character Boundary Panic** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2165))
   - *Status:* Closed | *Comments:* 3
   - Critical crash at `ui.rs:1492` when rendering long strings containing Chinese characters on Windows with UTF-8 encoding. Byte-index truncation in DataFrame headers triggers the panic. Fixed in a recent patch, but remains a stark reminder of TUI rendering race conditions for i18n.

3. **[#2104] Homebrew Distribution Shim Failure** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2104))
   - *Status:* Closed | *Comments:* 4
   - After `brew upgrade`, the `deepseek` deprecation shim fails to locate the `codewhale` binary on PATH, producing a binary-not-found error. A concrete rebranding migration pain point.

4. **[#2134] Paste Triggers Unintended Send** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2134))
   - *Status:* Closed | *Comments:* 2
   - Pasting table data (e.g. from VS Code error list) auto-submits the form because embedded Tab characters bypass the `burst_window_until` Enter suppression. Only the first line is sent. Fixed in PR #2174 by preserving the suppression window.

5. **[#1806] Sub-agent 120s API Timeout** ([Issue](https://github.com/Hmbown/CodeWhale/issues/1806))
   - *Status:* Open | *Comments:* 3
   - All 5 sub-agents in a parallel `agent_open` task failed with identical 120-second timeout errors, rendering the parallel offloading feature nearly unusable for heavy workloads. Community requests strongly favor configurable timeout thresholds.

6. **[#1812] Windows TUI Intermittent Freeze** ([Issue](https://github.com/Hmbown/CodeWhale/issues/1812))
   - *Status:* Open | *Comments:* 3
   - Complete UI unresponsiveness on Windows 11 without a process crash. Two confirmed events with thread-state analysis point to the `crossterm` poll loop. Remains an unresolved stability risk for Windows users.

7. **[#2156] Global `~/.agents/AGENTS.md` Support** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2156))
   - *Status:* Open | *Comments:* 2
   - Request to automatically load global instructions from `~/.agents/AGENTS.md` as a vendor-neutral fallback, eliminating repetitive system prompt setup per project. Multiple parallel PRs indicate high community alignment.

8. **[#1920] Wayland Clipboard Silent Failure** ([Issue](https://github.com/Hmbown/CodeWhale/issues/1920))
   - *Status:* Open | *Comments:* 2
   - Copying text inside the TUI on non-wlroots Wayland compositors (e.g. niri) writes nothing to the system clipboard. The mouse selection popup appears to work but silently drops the data.

9. **[#2244] Footer Overlays Long Output** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2244))
   - *Status:* Open | *Comments:* 1
   - When model output exceeds terminal height, the status line covers the bottom of the transcript. The scroll boundary does not properly account for the footer, making long code blocks or tables unreadable without workarounds.

10. **[#2231] Config Directory Migration Confusion** ([Issue](https://github.com/Hmbown/CodeWhale/issues/2231))
    - *Status:* Closed | *Comments:* 1
    - Post-rebrand, users find dual configuration directories (`~/.deepseek` vs `~/.codewhale`) confusing. The maintainer acknowledges the issue and formalizes the migration path and legacy fallback mechanism.

## Key PR Progress

1. **[#2242] Typed Persistent Permission System** ([PR](https://github.com/Hmbown/CodeWhale/pull/2242))
   - *Status:* Open
   - End-to-end typed tool permission rules (`allow` / `deny` / `ask`) scoped by tool name, command prefix, and workspace-relative path. Supersedes earlier split `execpolicy` PRs and integrates the TUI persistence UI. A major architectural maturing of the agent tool safety layer.

2. **[#2245] Fix Bing HTML Entity Decoding** ([PR](https://github.com/Hmbown/CodeWhale/pull/2245))
   - *Status:* Open
   - Critical fix for the default Bing search backend returning 0 results. URL click-tracking redirects encode separators as HTML entities (`&amp;`), causing parse failure in `normalize_bing_url`.

3. **[#2240] Xiaomi MiMo Provider Support** ([PR](https://github.com/Hmbown/CodeWhale/pull/2240))
   - *Status:* Open
   - First-class integration of the Xiaomi MiMo API supporting `mimo-v2.5-pro` (reasoning flagship) and `mimo-v2.5` models. Implements MiMo-specific thinking toggle and model list retrieval from the token-plan endpoint.

4. **[#2235] `/new` Session Command** ([PR](https://github.com/Hmbown/CodeWhale/pull/2235))
   - *Status:* Closed
   - Introduces `/new [--force]` as an explicit command to start a fresh saved session, fixing the ambiguous lifecycle where `/clear` reset state without proper session management.

5. **[#2239] i18n Phase 1-4b Wiring** ([PR](https://github.com/Hmbown/CodeWhale/pull/2239))
   - *Status:* Open
   - Massive localization effort rebasing and wiring MessageId translations across 47 files (+1059 lines). Fixes 109 compile errors from the upstream rebase. Supersedes the stalled PR #812.

6. **[#2133] External GUI Runtime Bridge** ([PR](https://github.com/Hmbown/CodeWhale/pull/2133))
   - *Status:* Open
   - Architectural plumbing to propagate `EngineEvent::UserInputRequired` to external runtime consumers (VSCode extensions, custom GUIs). Exposes `submit_user_input` / `cancel_user_input` on the runtime handle.

7. **[#2236] Global `~/.agents/AGENTS.md` Fallback** ([PR](https://github.com/Hmbown/CodeWhale/pull/2236))
   - *Status:* Open
   - Fulfills the top feature request (#2156): reads global agent instructions from `~/.agents/AGENTS.md` as a vendor-neutral fallback when `~/.claude/CLAUDE.md` is absent.

8. **[#2233] v0.8.47 Release Build** ([PR](https://github.com/Hmbown/CodeWhale/pull/2233))
   - *Status:* Closed
   - Roll-up of 9 community PRs into a single release. Includes the RwLock→Semaphore deadlock fix, composer text selection, copy/cut support, project context tracing, and session load improvements.

9. **[#2228] Composer Text Selection & Copy/Cut** ([PR](https://github.com/Hmbown/CodeWhale/pull/2228))
   - *Status:* Closed
   - Adds mouse drag selection and keyboard-driven text selection (Shift+arrows) to the input box. Ctrl+C/X for copy/cut with word-jump on macOS. A significant UX enhancement requested across multiple issues.

10. **[#1856] Tool Call Runtime Deadlock Fix** ([PR](https://github.com/Hmbown/CodeWhale/pull/1856))
    - *Status:* Closed
    - Replaces `Arc<RwLock<()>>` with `Arc<Semaphore>` in `ToolCallRuntime` to eliminate tool re-entrancy deadlocks. Serial tools hold a permit for full execution duration; parallel tools no longer block on read-lock contention.

## Feature Request Trends

- **Global Context & Config Inheritance:** Strong demand for loading global `AGENTS.md` rules from `~/.agents/` and smoothing the config migration from `~/.deepseek` to `~/.codewhale`. Users expect project-level instructions to be prioritized automatically without manual `/anchor` commands.
- **Typed Permission Systems:** The ecosystem is maturing toward enterprise-safe tool use. Requests for persistent, typed rules (allow/deny/ask) per tool and command pattern dominate the enhancements category.
- **i18n & Locale Polish:** Beyond CJK character rendering, users want full UI translations and locale-aware cost displays (CNY vs USD). The 47-file i18n PR (#2239) reflects the scale of this demand.
- **External IDE Integration:** A clear bridge from the TUI engine to external consumers (VSCode extensions, custom frontends) is taking shape through runtime event plumbing.
- **Provider Diversity:** The community actively contributes provider backends (Xiaomi MiMo, OpenRouter parity, vLLM reasoning parameters), signaling demand for a genuinely vendor-neutral AI terminal experience.

## Developer Pain Points

- **Cross-Platform Stability:** Windows freezes (#1812), Apple macOS notarization blocks (#2052), and Wayland clipboard failures (#1920) remain the most disruptive platform-specific blockers. These undermine confidence in the TUI for daily professional use.
- **Rebranding Migration Friction:** The `deepseek → codewhale` binary migration caused Homebrew shim bugs (#2104), config directory confusion (#2231), and slow download mirror issues in China (#2222).
- **Agent Workflow Fragility:** Hard-coded 120s sub-agent timeouts (#1806) and tool call deadlocks (#2157) make parallel agent features feel experimental. Users cannot trust `agent_open` for production pipeline tasks.
- **Edge-Case UI Regressions:** Paste-triggered sends (#2134), footer overlay on long output (#2244), and CJK boundary panics (#2165) indicate that the TUI layout and input handling have persistent edge cases under non-English inputs.
- **Build & Distribution Friction:** Nix builds fail in CI (#2221, #2223), Apple quarantines standalone binaries, and npm updates lag behind GitHub releases (#1914) — all contributing to significant install friction for new users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*