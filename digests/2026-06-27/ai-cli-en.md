# AI CLI Tools Community Digest 2026-06-27

> Generated: 2026-06-27 02:49 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report: June 27, 2026

## 1. Ecosystem Overview

The AI CLI developer tools landscape has reached a critical inflection point where raw capability is no longer the primary differentiator—trust, cost predictability, and deterministic behavior dominate community discourse across all major projects. The ecosystem is bifurcating between high-cost, deep-reasoning platforms (Claude Code, OpenAI Codex, Copilot CLI) and agile, infrastructure-focused contenders (Qwen Code, Gemini CLI, Pi) that are pushing multi-agent orchestration and structural code awareness. A universal "trust crisis" is unfolding around opaque billing mechanisms, memory data leakage across contexts, and uncontrollable agent looping—issues that collectively represent the industry's most urgent unsolved problems. The signal from the developer community is unmistakable: excitement about *what* these tools can do is being overtaken by demands for reliability, transparency, and predictable behavior.

---

## 2. Activity Comparison

| Tool | Hot Issues (Last 24h) | Key PRs (Last 24h) | Release Today |
|---|---|---|---|
| **Claude Code** | Very High (10+, with duplicates) | Low (2) | ✅ v2.1.195 |
| **OpenAI Codex** | Very High (10) | Very High (10) | ✅ rust-v0.142.3 |
| **Gemini CLI** | Very High (10) | Very High (10) | ❌ None |
| **GitHub Copilot CLI** | High (10) | Very Low (1) | ✅ v1.0.66-1 |
| **Kimi Code CLI** | Low (3) | Low (2) | ❌ None |
| **OpenCode** | Very High (10) | Very High (10) | ❌ None |
| **Pi (pi-mono)** | High (10) | High (7) | ❌ None |
| **Qwen Code** | Very High (10) | Very High (10) | ✅ v0.19.2-nightly |
| **CodeWhale** | High (10) | High (10) | ❌ None |

**Interpretation:**
- **Highest Development Velocity:** OpenAI Codex, Gemini CLI, OpenCode, and Qwen Code maintained the most intense engineering cadence, each processing double-digit PRs while managing high issue load.
- **Stabilization Mode:** Claude Code and Copilot CLI show disproportionately low PR volume relative to their issue severity (billing lockout, data loss, memory leaks), suggesting deeper root-cause remediation efforts are underway.
- **Niche/Emerging:** Kimi Code remains nascent; Pi and CodeWhale demonstrate healthy community contribution rates (externally authored PRs) that belie their smaller user bases.

---

## 3. Shared Feature Directions

*Requirements independently emerging across multiple projects, indicating strong market pull:*

| Requirement | Affected Tools | Community Specifics |
|---|---|---|
| **Deterministic Memory & Context Isolation** | Copilot CLI (#3945, #3946), Gemini CLI (#26525), Claude Code (#71671), Codex (#30299) | Cross-repo memory leakage and pre-redaction secret exposure are the most urgent privacy defects. Users demand per-project isolation, audit trails, and CLI commands for memory inspection. |
| **Multi-Agent Orchestration & Team Collaboration** | Qwen Code (#5887), Gemini CLI (#21409, #22323), Claude Code (#69691), OpenCode (#34135), Pi (#6064) | The market is moving beyond single-turn agents toward persistent team-based agents (Qwen Tag), background loop tasks, and supervised sub-agent workflows. |
| **Non-Blocking, Ocularly Stable Terminal UI** | Pi (#5825, #6050), OpenCode (#28956), Claude Code (#71726), Qwen Code (#5869) | Forced scroll-jumps, destructive full redraws, and non-dismissable overlays are actively harming productivity. The TUI is becoming a live IDE canvas, not just a conversation log. |
| **Cost & Usage Billing Transparency** | OpenAI Codex (#28879), Claude Code (#5088), OpenCode (#28846) | The largest cross-cutting trust issue. Opaque budget consumption, silent model swaps (Qwen #5819), and unresolvable billing lockouts are driving the loudest community frustration. |
| **Cross-Platform Parity (Windows/ARM)** | Copilot CLI (#2082, #3949), Claude Code (#39636), Codex (#30265), OpenCode (#29281), Pi (#6104) | Windows clipboard, WSL path translation, ARM64 VM crashes, and `process.exit()` killing parent terminals are recurring platform-specific regressions. |
| **Security Hardening & Sandboxing** | Claude Code (#70684), Codex (#29933), Gemini CLI (#27966), Qwen Code (#5834, #5055) | Path traversal vulnerabilities, destructive plugin actions, Trojan false positives, and broken proxy support highlight the gap between feature surface and security maturity. |

---

## 4. Differentiation Analysis

### Strategic Positioning

| Tool | Core Identity | Target User | Primary Weakness |
|---|---|---|---|
| **Claude Code** | Enterprise deep-reasoning engine | Professional developers on Max plans | Over-reliance on single high-tier model (Opus 4.8); vulnerable to provider-side regressions |
| **OpenAI Codex** | Plugin ecosystem platform | Power users, MCP ecosystem adopters | Plugin lifecycle trust deficit; billing opacity erodes core value proposition |
| **Gemini CLI** | Structured safety & evaluation leader | Advanced agentic users, eval-centric teams | Over-engineering for safety; sub-agents can be overly cautious or fail to utilize configured tools |
| **Copilot CLI** | Integrated GitHub workflow tool | Broad enterprise developer base | Identity crisis between standalone CLI and platform component; context isolation bugs |
| **OpenCode** | Cost-optimized multi-provider agent | Cost-conscious, BYO-model developers | Downstream API fragility; reliability varies wildly across providers |
| **Pi (pi-mono)** | TUI-first embeddable runtime | Rust ecosystem, library embedding, terminal purists | Smallest ecosystem; breaking changes common as architecture stabilizes |
| **Qwen Code** | Multi-instance team agent infrastructure | China-market, team collaboration, daemon-mode workflows | Complex architecture creates process lifecycle bugs (zombie processes, OOM) |
| **CodeWhale** | DeepSeek-native reasoning TUI | CJK developers, DeepSeek ecosystem | Reasoning model streaming fragility; narrow provider focus |

### Technical Approach Divergence

- **Agent Architecture:** Gemini CLI is investing heavily in **AST-aware structural code understanding** (#22745) and behavioral eval suites (#24353), aiming for tool correctness over raw throughput. Qwen Code is pushing **daemon-mode persistent agents** with resumable SSE streams (#5852) and **multiplayer channel agents** (#5887)—treating the CLI as infrastructure. Pi is architecting for **library embedding**, decoupling the agent runtime from the TUI process lifecycle.
- **Plugin/Provider Strategy:** OpenAI Codex is enabling **remote plugins by default** (#30297) and enforcing **marketplace source policies** (#29691), betting on a curated but massively extensible ecosystem. OpenCode is pursuing **maximum provider flexibility**, absorbing the complexity cost of supporting diverse API spec deviations.
- **Safety & Governance:** Copilot CLI's v1.0.66-1 introduced **subagent concurrency limits** and a **`/chronicle skills review`** workflow—formalizing enterprise governance as a feature. Gemini CLI is enforcing **case-insensitive sensitive path blocklists** (#27966) and **recursive reasoning caps** (#28164) as architectural invariants.

---

## 5. Community Momentum & Maturity

### Highest Development Velocity
**Qwen Code** and **Gemini CLI** are shipping the most impactful architectural changes daily (multiplayer agents, daemon resumability, AST evals, reasoning caps) while simultaneously managing high-severity bug loads. This indicates strong internal investment and engineering capacity.

### Highest Expectations & Pressure
**Claude Code** and **OpenAI Codex**. Their user bases are deeply invested power users who are highly sensitive to regressions. The simultaneous billing trust crises in both (#5088, #28879) combined with model quality regressions (Opus 4.8 malformed calls, disappearing 1M context) represent material attrition risk. Community blowback is loudest here.

### Trust on the Line
**GitHub Copilot CLI**. The memory/instruction leakage defects (#3945, #3946) represent a fundamental breach of contextual integrity for a tool deeply woven into the development lifecycle. The near-zero PR throughput (1 PR) suggests the team is prioritizing a difficult root-cause fix, but the silence is notable.

### Rapidly Maturing Niche
**Pi (pi-mono)** and **CodeWhale**. Both show high community contribution ratios (externally authored provider support, documentation). If they can resolve their core stability blockers (TUI viewport, editor freezes, extension isolation), they are well-positioned to capture specific developer segments (Rust/Pi, DeepSeek/CodeWhale).

---

## 6. Trend Signals for Developers

### 1. Agent Loops Are the Industry's "Memory Corruption"
Infinite loops, stuck tool calls, and false success reports (Gemini #22323, Qwen #27852, Claude #63604) are the new core stability bug. Tools implementing **deterministic exit conditions**, **recursive reasoning caps**, and **user-editable loop task files** (Gemini, Qwen) are setting the reliability standard. Any tool lacking these guarantees will face increasing community rejection as users burn API credits on runaway agents.

### 2. BYO Model Complexity is a Cost Center
The operational burden of maintaining consistent behavior across 8+ provider APIs (OpenAI, Anthropic, Bedrock, DeepSeek, Qwen, GLM, Friendli, OpenRouter) is immense. OpenCode's 100+ issue backlog includes a steady stream of provider-specific fragility (Bedrock empty responses, Qwen malformed calls). The market is splitting into **single-provider premium experiences** (Claude Code, Copilot CLI) and **multi-provider cost optimization** (OpenCode, CodeWhale)—rarely do tools excel at both.

### 3. The Terminal is Competing with the IDE
The intense focus on TUI quality (Pi scroll stabilization, OpenCode modal fixes, Qwen web-shell live syntax highlighting, Claude Code mouse-disable env var) signals that the terminal is being reimagined as a **live IDE surface**. Ocular stability, non-blocking interaction patterns, and responsive streaming are table stakes. A tool that makes the terminal feel junior to VS Code will lose the terminal-native user.

### 4. Memory is the Next Privacy Battlefield
Cross-repo context pollution (Copilot), pre-redaction data exposure (Gemini), silent history loss (Claude #71729), and unredacted session logs (Qwen) represent the top security concern. Enterprise compliance teams will increasingly block tools that cannot offer **strict project isolation**, **auditable memory delete**, and **configurable redaction** before model ingestion. The MCP-backed external memory stores (CodeWhale Moraine, Qwen Tag) suggest the market is actively searching for the right architecture.

### 5. Cost Dynamics are Externally Imposed
The largest cost events (DeepSeek price cuts, Opus 1M context removal, Codex rate-limit changes) are entirely outside tool providers' control. The most resilient tools will be those offering **granular per-model cost controls** (OpenCode), **credit alerts** (Qwen), and **high deterministic value generation**—i.e., fixing loops and truncation errors that waste tokens on fruitless retries.

### 6. The "Multi-Agent Stack" is Emerging as a Product Category
Qwen Tag, Pi Orchestrator, Copilot Subagents, and OpenCode Child Agent Pickers point toward an architectural pattern where the CLI manages **long-lived, shared agent instances** rather than ephemeral single-session conversations. This has profound implications for state management, permissions, and team workflow—expect this to be the defining architectural debate of late 2026.

---

## Bottom Line

The AI CLI market has passed the "show me what it can do" phase. Developers now ask: *"Will it burn my budget? Will it leak my secrets? Will it spin forever?"* The tools that win the next 12 months will be those that solve for **deterministic execution, transparent economics, and strict context isolation**—not those with the flashiest new agent capability. The current landscape reveals a market that has glimpsed the future and is deeply frustrated by the present's unreliability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the `anthropics/skills` repository activity (data as of 2026-06-27).

---

## Claude Code Skills Community Highlights Report

### 1. Top Skills Ranking

The following eight pull requests represent the highest-engagement Skill proposals and critical infrastructure fixes on the repository. (All remain **Open**.)

1.  **Skill-Creator Scoring Fix** ([#1298](https://github.com/anthropics/skills/pull/1298))
    - **Functionality**: Fixes the `run_eval.py` script that reports 0% recall on every description, breaking the `run_loop.py` optimization pipeline. The fix installs the eval artifact as a real skill and corrects Windows stream reading.
    - **Discussion**: Directly addresses Issue #556 (10+ independent reproductions). The community identified this as the single greatest blocker for iterative skill development.
    - **Status**: **Open**

2.  **Document Typography** ([#514](https://github.com/anthropics/skills/pull/514))
    - **Functionality**: Prevents orphan words, widow paragraphs, and numbering misalignment in generated documents.
    - **Discussion**: Highly practical, filling a quality-control gap that users say affects virtually every document Claude generates.
    - **Status**: **Open**

3.  **ODT / OpenDocument Skill** ([#486](https://github.com/anthropics/skills/pull/486))
    - **Functionality**: Enables creation, reading, filling, and conversion of `.odt`/`.ods` files, triggered by terms like “LibreOffice,” “ODF,” or “ISO standard document.”
    - **Discussion**: Strong demand from government and open-source-standards users. Highlights the community’s push for robust office-format parity.
    - **Status**: **Open**

4.  **Frontend Design Revamp** ([#210](https://github.com/anthropics/skills/pull/210))
    - **Functionality**: Complete rewrite of the existing `frontend-design` skill to make every instruction actionable within a single conversation session.
    - **Discussion**: The original skill was criticized for an educational, developer-documentation tone. This PR serves as a bellwether for the “skill-creator best practices” demanded in Issue #202.
    - **Status**: **Open**

5.  **Quality & Security Meta-Skills** ([#83](https://github.com/anthropics/skills/pull/83))
    - **Functionality**: Introduces two meta-skills—`skill-quality-analyzer` and `skill-security-analyzer`—evaluating skills across five weighted dimensions.
    - **Discussion**: Timely given the trust boundary vulnerability raised in Issue #492. Represents the ecosystem’s first step toward self-governance.
    - **Status**: **Open**

6.  **SAP-RPT-1-OSS Predictor** ([#181](https://github.com/anthropics/skills/pull/181))
    - **Functionality**: Skill for interacting with SAP’s open-source tabular foundation model for predictive analytics on business data.
    - **Discussion**: Bridges enterprise AI and the open-source community. The SAP TechEd 2025 release made this highly relevant for large-org teams.
    - **Status**: **Open**

7.  **Testing Patterns** ([#723](https://github.com/anthropics/skills/pull/723))
    - **Functionality**: Comprehensive testing skill covering the Testing Trophy model, unit tests, React components, and E2E.
    - **Discussion**: Addresses a deeply felt need for structured, opinionated testing guidance. Expected to standardize how Claude generates test suites in codebases.
    - **Status**: **Open**

8.  **Shodh-Memory** ([#154](https://github.com/anthropics/skills/pull/154))
    - **Functionality**: Persistent context system for AI agents using proactive retrieval across sessions.
    - **Discussion**: One of the most conceptually ambitious skills submitted. The community is watching closely for how agent-state management evolves.
    - **Status**: **Open**

---

### 2. Community Demand Trends

Analysis of the highest-engagement Issues reveals three concentrated demand vectors:

- **Security & Trust Infrastructure**: Issue #492 (21 comments) flags that community skills under the `anthropic/` namespace enable impersonation and trust boundary abuse. The community demands verified publisher badges or namespace isolation.
- **Org-Wide Sharing & Library Management**: Issue #228 (14 comments, 7 👍) calls for native skill sharing within organizations, moving beyond the current manual download/upload workflow that scales poorly for teams.
- **Skill-Creator Reliability**: Issues #556 and #1169 (combined 15 comments) document a broken core loop where `run_eval.py` never detects triggers. The community’s patience with 0% recall is clearly exhausted; this is the unblocker for all power users.

---

### 3. High-Potential Pending Skills

Beyond the top eight, several active PRs with strong structural foundations are likely to merge soon:

- **AppDeploy** ([#360](https://github.com/anthropics/skills/pull/360)): Enables Claude to deploy and manage full-stack webapps to a public URL. High potential for prototyping workflows.
- **Codebase Inventory Audit** ([#147](https://github.com/anthropics/skills/pull/147)): A systematic 10-step orphan code and documentation-bloat detection workflow. Directly addresses large-codebase maintenance friction.
- **Additional Skill-Creator Bugfixes** ([#1323](https://github.com/anthropics/skills/pull/1323), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050)): Multiple Windows-compatibility and trigger-detection fixes are queued, signaling the maintainers are actively stabilizing the optimizer pipeline.

---

### 4. Skills Ecosystem Insight

The community’s most concentrated demand is for a dual-layer evolution: fixing the bedrock reliability of the skill-creation infrastructure (the scoring and validation pipeline) while simultaneously rushing toward a suite of rigorous developer workflow skills—testing, deployment, audit, and typography—that require Claude to function as an autonomous engineering peer rather than a conversational assistant.

---

Here is the community digest for June 27, 2026.

---

## Claude Code Community Digest: 2026-06-27

### 1. Today's Highlights

Release **v2.1.195** lands with a crucial fix for hook matchers (exact matching for hyphenated names) and a new env var to disable mouse interactions. A wave of reports continues around the **Opus 4.8 1M context window disappearing** from the model picker, alongside persistent **Cowork failures on Windows ARM (Snapdragon X)** . A fresh, high-severity report details **silent conversation history loss** in the Desktop `</> Code` tab, demanding immediate attention.

### 2. Releases

**v2.1.195** ([Link](https://github.com/anthropics/claude-code/releases))

- **New:** Added `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` environment variable to disable mouse click/drag/hover in fullscreen mode while retaining wheel scroll (useful for terminal multiplexers and accessibility).
- **Fix:** Hook matchers with hyphenated identifiers (e.g., `code-reviewer`, `mcp__brave-search`) now perform **exact-string matching** instead of substring matching. This prevents accidental activation of hooks sharing common prefixes.

### 3. Hot Issues

*Top 10 most active or critical discussions from the last 24 hours:*

1. **Billing Lockout Crisis** ([#5088](https://github.com/anthropics/claude-code/issues/5088))
   *177 comments, 58 👍.* A critical `oncall`/`area:cost` bug where users are immediately locked out of Claude Code after paying for a Max 5x plan. High community frustration around support responsiveness.

2. **Cowork Dead on ARM64** ([#39636](https://github.com/anthropics/claude-code/issues/39636))
   *31 comments, 9 👍.* Cowork VM kernel never boots on Snapdragon X Plus. A related issue ([#50674](https://github.com/anthropics/claude-code/issues/50674)) confirms failures persist even when the readiness check passes. Blocking Windows-on-ARM adopters entirely.

3. **Opus 4.8 Malformed Tool Calls** ([#63604](https://github.com/anthropics/claude-code/issues/63604))
   *11 comments, 14 👍.* A model regression where Opus 4.8 emits broken `tool_use` blocks, causing the entire response to be discarded. Downvoting heavily impacts user trust. No workaround confirmed.

4. **1M Context Disappeared from Desktop Picker** ([#36351](https://github.com/anthropics/claude-code/issues/36351))
   *17 comments, 11 👍.* Duplicate reports ([#68287](https://github.com/anthropics/claude-code/issues/68287), [#69109](https://github.com/anthropics/claude-code/issues/69109), [#69444](https://github.com/anthropics/claude-code/issues/69444)) confirm that the 1M context option for Opus 4.8 is absent for many Max plan users after the latest Desktop update.

5. **Auto-Compact Regression for 3rd Party APIs** ([#65585](https://github.com/anthropics/claude-code/issues/65585))
   *6 comments, 4 👍.* Since v2.1.161, auto-compact has stopped working for third-party API providers. A painful regression for users relying on their own API keys to manage costs.

6. **Sandbox Breaks SSH Git Operations** ([#70684](https://github.com/anthropics/claude-code/issues/70684))
   *3 comments, 12 👍.* The sandbox injects SOCKS5 proxy settings that use BSD `nc`, which cannot negotiate authentication. This breaks `git push`/`fetch` for teams using authenticated proxies.

7. **Desktop Conversation History Lost on Restart** ([#71729](https://github.com/anthropics/claude-code/issues/71729))
   *6 comments.* Fresh bug: The `</> Code` embedded terminal in Claude Desktop silently drops all conversation history after a restart, with no warning or error logged.

8. **Claude-in-Chrome Blocks Business Domains** ([#40173](https://github.com/anthropics/claude-code/issues/40173))
   *11 comments, 7 👍.* Hardcoded server-side blocking prevents automation on financial/enterprise domains (e.g., Wells Fargo, Schwab). Users want a configurable allowlist feature.

9. **Issues Auto-Closed Without Review** ([#30407](https://github.com/anthropics/claude-code/issues/30407))
   *16 comments, 4 👍.* A growing concern about project maintainability. Community members report legitimate triaged issues being closed by bots without a maintainer response, impacting trust in the feedback loop.

10. **Model Ignores Memory/Instructions** ([#71671](https://github.com/anthropics/claude-code/issues/71671))
    *2 comments.* A user reports the model ignoring its own saved memory and scripts across multiple sessions, leading to repeated production data loss. Raises fundamental questions about memory reliability.

### 4. Key PR Progress

*PR activity was light today (only 2 items):*

1. **Docs: Sandbox Host Scope Clarified** ([#71627](https://github.com/anthropics/claude-code/pull/71627)) — **Open**
   A documentation improvement for `examples/settings/README.md`. It adds a bullet clarifying that hosts approved at prompt-time in the sandbox are **session-scoped** and lost on restart. Critical for teams relying on `sandbox.network.allowedDomains`.

2. **Stale External Fork Merge** ([#71530](https://github.com/anthropics/claude-code/pull/71530)) — **Closed**
   A simple sync PR from an external fork. Low significance, merged without discussion.

### 5. Feature Request Trends

- **Context Window Parity:** The overwhelming demand is for restoring the **full 1M context window for Opus 4.8** on the Max plan. Users view this as a core feature, not a nice-to-have.
- **Agent Control & Determinism:** Requests for **synchronous sub-agent execution** ([#69691](https://github.com/anthropics/claude-code/issues/69691)) and **mid-turn message injection in Desktop** ([#71726](https://github.com/anthropics/claude-code/issues/71726)) point to a desire for finer-grained orchestration.
- **Accessibility & Input Maturity:** Users want **custom voice dictation vocabularies** for technical jargon ([#71721](https://github.com/anthropics/claude-code/issues/71721)) and the ability to **disable prompt suggestions** in the web interface ([#66117](https://github.com/anthropics/claude-code/issues/66117)).
- **Remote Session Management:** A clear push for fully **remote session control** without requiring physical local approval ([#71731](https://github.com/anthropics/claude-code/issues/71731)).

### 6. Developer Pain Points

1. **Model Quality Regressions:** The Opus 4.8 1M context disappearance combined with the malformed tool call bug creates a trust deficit around the primary high-tier model.
2. **Windows ARM Readiness:** Cowork on Snapdragon X is a hard blocker. Passing a readiness check but failing to boot the VM ([#50674](https://github.com/anthropics/claude-code/issues/50674)) is a poor user experience.
3. **Silent Data Loss:** Reports of conversations disappearing ([#71729](https://github.com/anthropics/claude-code/issues/71729)) and GitHub issues failing to log errors ([#71733](https://github.com/anthropics/claude-code/issues/71733)) represent the highest severity class of defects.
4. **Sandbox Networking:** The SOCKS5 `nc` incompatibility ([#70684](https://github.com/anthropics/claude-code/issues/70684)) makes the sandbox unusable in many enterprise proxy environments.
5. **Configuration Portability:** Hardcoded absolute paths in plugins ([#31388](https://github.com/anthropics/claude-code/issues/31388)) continue to break setups shared across Linux/WSL and containerized environments.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest — 2026-06-27**

---

### 1. Today's Highlights
Rate-limit billing remains a flashpoint this week: Issue #28879 has exploded past 175 comments, with users claiming cost-per-token jumped ~10-20x since mid-June on the Plus plan. On the engineering side, the team is pushing forward major infrastructure improvements, overlapping critical-path latency (PR #30286) and enabling remote plugins by default (PR #30297). Meanwhile, a steady stream of Windows- and macOS-specific bugs around plugins, sandboxes, and resource leaks continues to challenge developer workflows.

---

### 2. Releases
- **`rust-v0.142.3`** – Maintenance-only patch; no user-facing changes since 0.142.2 ([Compare](https://github.com/openai/codex/compare/rust-v0.142.2...rust-v0.142.3)).
- **`rust-v0.143.0-alpha.26`** – Next pre-release milestone; no detailed changelog provided.

---

### 3. Hot Issues

1. **[BUG] Rate-limit cost per token jumped ~10-20x** (`#28879`)
   - **What:** Users report their 5-hour Plus budget draining in 2-3 prompts instead of 20+. Session logs show `limit-% consumed per token` increased dramatically around June 16.
   - **Why it matters:** The top-voted and most active issue (326 👍). Directly threatens the core value proposition for paying developers.
   - **[Link](https://github.com/openai/codex/issues/28879)**

2. **[BUG] 5-hour allowance consumed in ~1 hour** (`#30212`)
   - **What:** Pro (20x) users experiencing abnormal budget depletion, mirroring symptoms from #28879.
   - **Why it matters:** Indicates a systemic rate-limit or metering bug affecting multiple tiers.
   - **[Link](https://github.com/openai/codex/issues/30212)**

3. **[BUG] MCP stdio servers leak pipe FDs → EMFILE** (`#26984`)
   - **What:** stdio transport for MCP servers leaks file descriptors and orphans child processes, leading to `"Too many open files"` errors.
   - **Why it matters:** Directly impacts MCP reliability, a core differentiator for Codex CLI power users.
   - **[Link](https://github.com/openai/codex/issues/26984)**

4. **[BUG] `code_sign_clone` grows unbounded (62 GB+) on macOS** (`#27536`)
   - **What:** The Electron app accumulates a massive temp directory across updates.
   - **Why it matters:** Severe disk-resource leak. Highlights systemic update-pipeline cleanup issues.
   - **[Link](https://github.com/openai/codex/issues/27536)**

5. **[BUG] `curated-plugin sync` runs `git reset --hard` on user repos** (`#29933`)
   - **What:** Plugin sync performs a destructive `git reset --hard` on the user’s working tree.
   - **Why it matters:** High-severity safety issue with risk of data loss; erodes trust in plugin lifecycle management.
   - **[Link](https://github.com/openai/codex/issues/29933)**

6. **[BUG] Prompt textarea disabled after several prompts (macOS)** (`#30263`)
   - **What:** Text input area becomes unresponsive, requiring app restarts.
   - **Why it matters:** High-friction UI bug blocking the primary interaction path.
   - **[Link](https://github.com/openai/codex/issues/30263)**

7. **[ENHANCEMENT] Official CLI for memory inspect/prune/delete** (`#30299`)
   - **What:** Request for a command-line surface to manage the experimental `memories` feature.
   - **Why it matters:** Growing demand for transparency and control over agent persistent state.
   - **[Link](https://github.com/openai/codex/issues/30299)**

8. **[BUG] Chrome control broken in WSL-agent mode** (`#30265`)
   - **What:** Native-messaging host manifest paths use un-translated `/mnt/c/` paths, preventing browser control.
   - **Why it matters:** Blocks a flagship feature for the large WSL developer segment on Windows.
   - **[Link](https://github.com/openai/codex/issues/30265)**

9. **[BUG] Bundled plugins disappear after Windows app updates** (`#30270`)
   - **What:** Browser/Chrome/Computer Use plugins vanish post-update due to stale marketplace paths.
   - **Why it matters:** Highly disruptive to Windows workflows; undermines update reliability.
   - **[Link](https://github.com/openai/codex/issues/30270)**

10. **[BUG] TRACE logs written despite `RUST_LOG=warn`** (`#30236`)
    - **What:** App ignores the `RUST_LOG` env var, flooding `logs_2.sqlite` with verbose trace output.
    - **Why it matters:** Broken configuration layer causing unnecessary disk I/O and performance degradation.
    - **[Link](https://github.com/openai/codex/issues/30236)**

---

### 4. Key PR Progress

1. **`feat(rollout): persist canonical items for paginated threads`** (`#30188`)
   - The final persistence layer for the new `TurnItem` lifecycle. Moves away from legacy parallel item events.
   - **[Link](https://github.com/openai/codex/pull/30188)**

2. **`core: overlap diff root discovery with world state`** (`#30286`)
   - Parallelizes remote diff-root discovery with world-state construction to reduce thread-cold turn latency.
   - **[Link](https://github.com/openai/codex/pull/30286)**

3. **`[codex] Enable remote plugins by default`** (`#30297`)
   - Promotes remote plugins to stable, greatly expanding the plugin ecosystem while preserving an opt-out.
   - **[Link](https://github.com/openai/codex/pull/30297)**

4. **`[plugins] Enforce marketplace source policy at runtime`** (`#29691`)
   - Implements runtime enforcement of enterprise source policies, blocking or filtering plugins based on config.
   - **[Link](https://github.com/openai/codex/pull/29691)**

5. **`Add generated token auth to app-server WebSockets`** (`#30315`)
   - Generates a 256-bit token for WebSocket listeners when `--ws-auth` is not set, improving local security.
   - **[Link](https://github.com/openai/codex/pull/30315)**

6. **`core: persist unmatched call output repairs`** (`#30327`)
   - Ensures durable identity for synthesized “aborted” outputs during prompt repairs, fixing conversation history consistency.
   - **[Link](https://github.com/openai/codex/pull/30327)**

7. **`fix(remote-control): avoid server token refresh retry storms`** (`#30201`)
   - Prevents repeated failed refresh attempts from overwhelming the server during transient outages.
   - **[Link](https://github.com/openai/codex/pull/30201)**

8. **`Preserve namespaces on custom tool calls`** (`#30302`)
   - Passes optional tool namespaces through the entire pipeline, preventing collisions in streaming and dispatch.
   - **[Link](https://github.com/openai/codex/pull/30302)**

9. **`Add retired model compaction repro`** (`#30319`)
   - Integration test for model-switch compaction when a previous model slug is retired, ensuring graceful deprecation.
   - **[Link](https://github.com/openai/codex/pull/30319)**

10. **`core-skills: cache snapshots before root discovery`** (`#30281`)
    - Aligns skill snapshot caching with root discovery to avoid redundant metadata probes on remote filesystems.
    - **[Link](https://github.com/openai/codex/pull/30281)**

---

### 5. Feature Request Trends
- **Configurability & Extensibility:** Developers are pushing for more user-side control: configurable API base URLs for alternative providers (e.g., Bedrock), and native CLI commands to manage agent memory.
- **Event-Driven Agent Capabilities:** The `monitor` tool request (#29922) signals a desire for Codex to support background event-driven workflows (log watches, file changes, CI triggers) rather than purely turn-based interaction.
- **Plugin Lifecycle Stability:** As remote plugins are enabled by default, users are requesting predictable update behavior, version pinning, and strict runtime policy enforcement to prevent silent breakage.

---

### 6. Developer Pain Points
- **Rate Limit Transparency:** The #1 recurring frustration is opaque and volatile usage billing. Multiple high-engagement issues (#28879, #30212, #30310) point to a systemic loss of trust in how consumption is calculated and communicated.
- **Windows Platform Instability:** A disproportionately high volume of severe bugs target Windows—WSL agent mode, browser control, sandbox elevation, and plugin removal on update. This is a significant weak spot for the user experience.
- **Plugin Ecosystem Trust:** Destructive actions (e.g., `git reset --hard` in #29933) and brittle update paths (#30270) generate widespread caution about plugin safety, a critical issue as the remote plugin model expands.
- **Configuration & Debugging Dissonance:** Ignored environment variables (`RUST_LOG`) and unbounded resource leaks (`code_sign_clone`, TRACE logs) erode confidence in runtime fundamentals and developer tooling hygiene.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-27

## Today’s Highlights
The project saw no new releases today, but a heavy wave of core reliability patches landed in review. Key efforts focus on **eliminating agent loops and hangs** (pending tool response caps, recursive reasoning limits, thought leakage cleanup) and **hardening MCP and path resolution** to fix "File not found" bugs and broken server routing. On the infrastructure side, the **Caretaker automation system** is rapidly materializing with multiple Cloud Run PRs for webhook ingestion, triage, and egress — a strong signal that the team is dogfooding their own tooling for project maintenance.

## Releases
**No new releases** in the last 24 hours.

---

## Hot Issues
*Pick of 10 most noteworthy open / recently updated issues.*

### 1. [#22323 Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)
- **Priority:** P1 · **Area:** Agent · **Comments:** 8 · **👍:** 2
- **What it is:** A `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit the max turn limit before doing any actual work.
- **Why it matters:** This is a critical logic flaw that masks agent failures, misleading users and auto-eval pipelines into thinking analysis completed successfully. Top community concern this week.

### 2. [#21409 Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)
- **Priority:** P1 · **Area:** Agent · **Comments:** 7 · **👍:** 8
- **What it is:** The CLI hangs indefinitely when deferring to the generalist agent, even for simple tasks like folder creation. Instructing the model to skip sub-agents works around it.
- **Why it matters:** Highest community engagement this period (8 👍). Completely blocks users from relying on sub-agent delegation. A top-priority investigation.

### 3. [#25166 Shell command stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)
- **Priority:** P1 · **Area:** Core · **Comments:** 4 · **👍:** 3
- **What it is:** After executing a simple shell command that successfully finishes, the CLI remains in a "Waiting input" state indefinitely.
- **Why it matters:** Pervasive UX-breaking bug that turns the CLI into a dangling process. Very high frustration signal in the community.

### 4. [#26525 Secrets / Auto Memory redaction](https://github.com/google-gemini/gemini-cli/issues/26525)
- **Priority:** P2 · **Area:** Security · **Comments:** 5
- **What it is:** Auto Memory sends local transcript content to the model *before* redaction; secrets remain in model context and logs.
- **Why it matters:** Raises fundamental security and privacy concerns about the memory extraction pipeline. Community is watching the resolution closely.

### 5. [#24353 Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)
- **Priority:** P1 · **Area:** Agent · **Comments:** 7
- **What it is:** An epic building on 76 behavioral eval tests across 6 Gemini models. Aims for broader automated testing to prevent regressions.
- **Why it matters:** The backbone of quality assurance for the agent system. Signals the team is investing heavily in preventing the class of bugs described above.

### 6. [#21968 Gemini doesn’t use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)
- **Priority:** P2 · **Area:** Agent · **Comments:** 6
- **What it is:** Users report the model rarely uses custom skills (e.g., Gradle, Git) or sub-agents unless explicitly prompted to do so, even for closely related tasks.
- **Why it matters:** A core value proposition of Gemini CLI is extensibility; this points to a fundamental gap in how the model discovers and selects tools.

### 7. [#22745 AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)
- **Priority:** P2 · **Area:** Agent · **Comments:** 7 · **👍:** 1
- **What it is:** An epic investigating whether AST-aware tools reduce turn count, token waste, and misaligned reads by understanding code structure.
- **Why it matters:** Points the direction for the next generation of the coding agent: structural understanding over raw text processing. Closely related to codebase mapping improvements (#22746).

### 8. [#27852 Weird infinite loop](https://github.com/google-gemini/gemini-cli/issues/27852)
- **Priority:** P2 · **Area:** Agent · **Comments:** 3 · **Status:** Closed (needs info)
- **What it is:** A barebones implementation request sent the CLI into an execution loop.
- **Why it matters:** Despite being closed for more information, this represents a widespread class of regressions where simple prompts trigger runaway agent behavior.

### 9. [#22267 Browser Agent ignores settings.json overrides](https://github.com/google-gemini/gemini-cli/issues/22267)
- **Priority:** P2 · **Area:** Agent · **Comments:** 3
- **What it is:** The Browser Agent completely disregards `maxTurns` and other settings from user configuration.
- **Why it matters:** Breaks the trust contract in the configuration system. Users cannot control agent behavior through the documented pathways.

### 10. [#22093 Sub-agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)
- **Priority:** P2 · **Area:** Agent · **Comments:** 2
- **What it is:** Sub-agents (e.g., generalist) execute even when all agent modes are explicitly set to disabled, surprising users who only expected MCP functionality.
- **Why it matters:** A critical configuration trust issue — users who deliberately disable features should not have them silently re-enabled by the agent.

---

## Key PR Progress
*Pick of 10 impactful PRs updated in the last 24h.*

### 1. [#27870 Cap pending tool responses (Merged)](https://github.com/google-gemini/gemini-cli/pull/27870)
- **Area:** Agent · **Size:** M
- **What it does:** Prevents crashes by limiting the size/volume of pending `functionResponse` payloads.
- **Why it matters:** Fixes a high-frequency crash (fixes #27738). Directly addresses the "stuck tool response" class of bugs.

### 2. [#28164 Limit recursive reasoning turns](https://github.com/google-gemini/gemini-cli/pull/28164)
- **Area:** Core · **Size:** M
- **What it does:** Enforces a strict 15-turn cap on recursive reasoning per single user request (configurable via `maxSessionTurns`).
- **Why it matters:** Directly protects local CPU resources and API quotas from the infinite loop problems highlighted in #27852 and others.

### 3. [#28053 Defensive path resolution for `@`-prefixed files](https://github.com/google-gemini/gemini-cli/pull/28053)
- **Area:** Core Tools · **Size:** XL
- **What it does:** Fixes "File not found" errors when the model passes `@`-prefixed paths (e.g., `@policies/new-policies.txt`) to filesystem tools. Also fixes macOS tests.
- **Why it matters:** A common source of broken workflows when the model generates file paths with `@` references.

### 4. [#27971 Strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)
- **Area:** Core · **Size:** M/L
- **What it does:** Surgically removes model internal monologue ("thoughts") from history turns to prevent "thought leakage" that confuses subsequent reasoning.
- **Why it matters:** Targets a root cause of loop cascades and incoherent agent behavior in long sessions.

### 5. [#28055 Preserve dollar sequences in prompt templates](https://github.com/google-gemini/gemini-cli/pull/28055)
- **Area:** Agent · **Size:** S/M
- **What it does:** Fixes `applySubstitutions()` from corrupting `$` sequences (e.g., `$$`, `$'`, `$&`) in skill, sub-agent, and tool descriptions.
- **Why it matters:** Prevents silent prompt corruption that can break skill definitions or inject unintended behavior.

### 6. [#28033 MCP longest-prefix matching for server names](https://github.com/google-gemini/gemini-cli/pull/28033)
- **Area:** MCP · **Size:** M
- **What it does:** Adds longest-prefix matching to `parseMcpToolName` to correctly route tools when MCP server names contain underscores. Fixes #27981.
- **Why it matters:** MCP ecosystem growth depends on robust server name parsing. This fixes incorrect tool routing for a significant subset of MCP servers.

### 7. [#27966 Case-insensitive sensitive path blocklist (Merged)](https://github.com/google-gemini/gemini-cli/pull/27966)
- **Area:** Security · **Size:** M
- **What it does:** Enforces case-insensitive matching for the `.git`, `.env`, `node_modules` blocklist to bypass prompt injection attempts.
- **Why it matters:** A critical security fix — simple case swaps could previously bypass access controls on sensitive files.

### 8. [#28059 Unreadable .env doesn’t break extension loading](https://github.com/google-gemini/gemini-cli/pull/28059)
- **Area:** Extensions · **Size:** M
- **What it does:** Ensures an EACCES error on a workspace `.env` file doesn't cascade into a complete extension loading failure.
- **Why it matters:** Resolves a brittle failure mode for sandboxed environments (fixes #27894) where a permission issue kills all extension functionality.

### 9. [#27915 Trust dialog shows correct hook shape](https://github.com/google-gemini/gemini-cli/pull/27915)
- **Area:** Security · **Size:** M
- **What it does:** Corrects the workspace-trust dialog to display the *actual* hooks that will execute rather than the inverse. Fixes #27901.
- **Why it matters:** Prevents a security UX bug where a dangerous `SessionStart` hook runs silently while the dialog shows nothing to the user.

### 10. [#28012 Sync footer branch name on WSL/macOS](https://github.com/google-gemini/gemini-cli/pull/28012)
- **Area:** Core · **Size:** M
- **What it does:** Refreshes the footer Branch indicator after `git checkout` on filesystems that don't fire `fs.watch` events (WSL mounts, network shares).
- **Why it matters:** Everyday UX polish — the stale branch indicator on WSL was a persistent visual bug for a large segment of users.

---

## Feature Request Trends

- **Agent Observability & Evals:** The community strongly desires visibility into sub-agent trajectories ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)). The team is investing heavily in component-level evals ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353)) and steering tests ([#23313](https://github.com/google-gemini/gemini-cli/issues/23313)) to catch regressions early.

- **Structural Code Understanding (AST):** A clear push to move beyond text-based tools toward AST-aware reading, searching, and mapping ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)) to reduce token waste and improve tool accuracy.

- **Memory System Maturity:** The Auto Memory system is evolving fast. Users want deterministic redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), quarantine for invalid patches ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and intelligent filtering of low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)).

- **Safety & Destructive Action Prevention:** Growing calls for the agent to detect and discourage dangerous operations (`git reset --force`, destructive DB commands) before executing them ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).

- **Automated Project Stewardship (Caretaker):** The "Caretaker" suite of Cloud Run services ([#28167](https://github.com/google-gemini/gemini-cli/pull/28167), [#28015](https://github.com/google-gemini/gemini-cli/pull/28015), [#28163](https://github.com/google-gemini/gemini-cli/pull/28163)) represents a meta-feature: using Gemini CLI to manage Gemini CLI’s own issue triage and release process.

---

## Developer Pain Points

- **Agent Loops, Hangs, and Stuck States:** The single largest source of frustration this period. Infinite loops ([#27852](https://github.com/google-gemini/gemini-cli/issues/27852)), shell commands hanging on input ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and generalist agent freezes ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)) erode user trust heavily.

- **Sub-Agent Mismanagement:** Multiple reports of agents running sub-agents without permission ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), failing to use perfectly configured skills ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), and masking critical failures as successes ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)).

- **Context Pollution & Token Waste:** "Thought leakage" confusing the model across turns ([#27971](https://github.com/google-gemini/gemini-cli/pull/27971)), the model creating random temporary script files ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), and a lack of structural code awareness all contribute to excessive token burn.

- **Cross-Platform & Terminal Friction:** Browser agent failures on Wayland ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), stale branch indicators on WSL mounts ([#28012](https://github.com/google-gemini/gemini-cli/pull/28012)), terminal corruption on resize ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)), and incorrect `\n` escape behavior ([#22466](https://github.com/google-gemini/gemini-cli/issues/22466)).

- **Configuration & Integration Breakage:** MCP tool routing broken by underscore server names ([#28033](https://github.com/google-gemini/gemini-cli/pull/28033)), Browser Agent ignoring `settings.json` entirely ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and `.env` permission errors cascading into full extension system failures ([#28059](https://github.com/google-gemini/gemini-cli/pull/28059)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – June 27, 2026

## Today’s Highlights
This week’s `v1.0.66-1` release focuses on enterprise governance, introducing subagent concurrency limits, a `/chronicle skills review` workflow, and desktop notifications. However, the community is raising alarms over critical privacy bugs involving memory and instruction leakage between repositories (#3945, #3946), as well as recurring clipboard regressions on both Linux and Windows (#2082, #3949). The signal is clear: users deeply value the extensibility gains, but fundamental system integrity issues are top of mind.

## Releases
### v1.0.66-1
- **Subagent Concurrency & Depth Limits:** Usage-based billing users can now configure these in `/settings`, directly addressing performance concerns from bloated subagent session exports.
- **`/chronicle skills review`:** A formal review workflow for skill drafts, supporting accept, reject, or defer actions.
- **Desktop Notifications:** Native alerts for attention prompts and idle session timeouts.

## Hot Issues (Top 10)

1. **[#2082](https://github.com/github/copilot-cli/issues/2082) – Clipboard broken on Linux (`ctrl+shift+c`)** – *Open, 11 👍*
   A long-standing regression since `v1.0.4` breaking a core terminal UX pattern. 22 comments indicate broad impact and frustration across Ubuntu 24.04 users.

2. **[#3949](https://github.com/github/copilot-cli/issues/3949) – Copy does not work on Windows 11** – *Open*
   Mirroring the Linux issue, the CLI confirms a copy action occurred despite nothing landing on the clipboard. Erodes trust in the tool’s feedback loop.

3. **[#3945](https://github.com/github/copilot-cli/issues/3945) – Memories leaking between repositories** – *Open, Critical*
   A highly alarming context isolation bug. “Facts” from one repo contaminate brand-new, unrelated repos. Privacy and correctness implications are severe.

4. **[#3946](https://github.com/github/copilot-cli/issues/3946) – Custom instructions leak into repository analysis** – *Open*
   A companion to #3945; local `.copilot-instructions` from one project bleed into the analysis of others, causing hallucinated project structures and recommendations.

5. **[#3944](https://github.com/github/copilot-cli/issues/3944) – Subagent transcripts inlined verbatim in session exports** – *Open*
   Session logs become unmanageably large with uncapped subagent tool-call dumps. The new concurrency limits in `v1.0.66` align directly with this pain point.

6. **[#3954](https://github.com/github/copilot-cli/issues/3954) – `explore` tool hardcodes `gpt-5.4-mini` ignoring custom config** – *Open*
   Breaks Bring-Your-Own-Model workflows. Users configuring DeepSeek or other endpoints are blocked when the agent invokes the `explore` tool.

7. **[#3947](https://github.com/github/copilot-cli/issues/3947) – Theme system regression in 1.0.64** – *Closed*
   All five theme options override the terminal background, breaking transparency. Quickly closed, suggesting either a pending fix or a designed trade-off.

8. **[#3955](https://github.com/github/copilot-cli/issues/3955) – Drag-and-drop file attachment broken on macOS app** – *Open, Regression*
   A recent regression in the Copilot desktop app. Dropping files into the prompt composer no longer attaches anything—a critical context workflow blocker.

9. **[#3942](https://github.com/github/copilot-cli/issues/3942) – `--acp` does not work with `--agent`** – *Open*
   Blocks CI/CD automation with custom agents. Users cannot script their specialized agent workflows non-interactively.

10. **[#3948](https://github.com/github/copilot-cli/issues/3948) – `web_fetch` returns `TypeError: fetch failed`** – *Open*
    The `web_fetch` tool is completely broken despite correct proxy/env configuration. Limits agent access to real-time documentation and web context.

## Key PR Progress
Only a single pull request was updated in the last 24 hours, indicating the team is currently focused on stabilization and release management over new feature merges:

- **[#570](https://github.com/github/copilot-cli/pull/570) – [WIP] Add macOS installation instructions to README.md** *(Closed)*
  An automated PR from the Copilot bot itself. Updated but remains closed. This reflects background maintenance work rather than active feature development. The low PR volume reinforces that the immediate cycle is dedicated to addressing the regression flood and hardening `v1.0.66-1`.

## Feature Request Trends

- **Custom Agent & Skill Scoping (#3940, #3951):** Users want a `skills` field in custom agent definitions to restrict which skills are preloaded into context. The goal is creating tightly-scoped agents (e.g., a .NET/C# specialist) without irrelevant tool noise.
- **Session Pause & Resume (#1928):** A recurring request for the ability to pause an active session, inject additional instructions, and resume without losing state.
- **Platform-Native Shell Support (#3951):** A strong push for native PowerShell cmdlets on Windows instead of wrapping a generic CLI. Indicates the tool is transitioning from a utility to a platform-integrated tool.
- **Governance & Audit (#3947, #3906):** Users are requesting formal theme accessibility standards, CVE tracking for security reports, and better diagnostics when configurations fail silently.

## Developer Pain Points

- **Cross-Platform Clipboard Instability (#2082, #3949):** The #1 immediate UX friction. Copy/paste is not negotiable, and its failure on both Linux and Windows is the loudest complaint this cycle.
- **Context & Memory Contamination (#3945, #3946):** The highest severity concern. Leaking memories and instructions between repositories fundamentally breaks the promise of contextual awareness. This actively misleads users about their projects and is a must-fix.
- **Configuration Ignorance (#3954, #3948):** Users who invest time in custom models or proxies find their settings silently ignored by internal tools like `explore` and `web_fetch`. This destroys predictability.
- **Automation Roadblocks (#3942):** The inability to combine non-interactive mode (`--acp`) with custom agents (`--agent`) blocks the CLI’s value in CI/CD pipelines—a key audience for a CLI tool.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-06-27**

**1. Today's Highlights**
Today's activity on the `kimi-cli` repository was focused on stability and documentation quality. The long-running 403 authentication issue (#2425) surrounding `kimi-for-coding` agent access was closed, providing clarity on tiered model licensing. A critical state management bug was opened for Plan mode (#2478), where the agent remains stuck due to a mismatch between the system prompt and command recognition. Additionally, two active PRs landed covering developer onboarding docs and stricter OpenAI API interoperability.

---

**2. Releases**
No new releases were published in the last 24 hours.

---

**3. Hot Issues**
*(The dataset for this period contained 3 active issues. All are analyzed below.)*

- **#2478 [Bug] ExitPlanMode reports "Not in plan mode" while system reminder claims plan mode is active**
  *Author: proccl | Updated: 2026-06-26 | Comments: 1*
  **Why it matters:** This is a high-severity "stuck state" bug. The system persists a plan file path and explicitly states "Plan mode is active," but calling `ExitPlanMode` fails because the internal state machine believes it is already out of plan mode. This creates a deadlock for the agent workflow where the user cannot cleanly exit planning. Community reaction is immediate concern, as it directly blocks structured planning sessions.
  **Link:** MoonshotAI/kimi-cli Issue #2478

- **#2425 [CLOSED] [bug] 403 Kimi For Coding is currently only available for Coding Agents**
  *Author: zhongyr | Updated: 2026-06-26 | Comments: 10 | 👍: 3*
  **Why it matters:** The highest-engagement item of the batch. The user received a blanket 403 error when using the `kimi-for-coding` model via the CLI. The 10 comments and 3 upvotes suggest a widespread confusion around API access tiers. The closure implies the team provided a resolution—likely clarifying that the model requires a specific plan or agent license—highlighting a need for better upfront error messaging.
  **Link:** MoonshotAI/kimi-cli Issue #2425

- **#2477 [bug] Kimi CLI Bug Report — Double Enter Key & `/sessions` Feedback Loss**
  *Author: iqre8 | Updated: 2026-06-26 | Comments: 0*
  **Why it matters:** A Linux-specific (Ubuntu 24.04) terminal interaction bug. The "double enter" behavior points to an event handler that isn't properly consuming the first key press, while the loss of `/sessions` feedback suggests stdout is being swallowed or buffered incorrectly. This degrades the interactive TUI experience for Linux developers.
  **Link:** MoonshotAI/kimi-cli Issue #2477

---

**4. Key PR Progress**
*(The dataset for this period contained 2 active PRs. Both are analyzed below.)*

- **#2287 [OPEN] docs(readme): add prerequisites list to Development section**
  *Author: ktwu01 | Updated: 2026-06-26*
  **Feature/Fix:** Documentation improvement. Adds a `### Prerequisites` block to the README's Development section.
  **Why it matters:** This addresses a common contributor onboarding pain point (#2274). New developers previously hit errors running `make prepare` without knowing the required runtime dependencies. This PR lowers the barrier to entry for open-source contributions by clearly listing the toolchain upfront.
  **Link:** MoonshotAI/kimi-cli PR #2287

- **#2476 [OPEN] fix(kosong): omit reasoning_effort instead of sending null when thinking is off**
  *Author: logicwu0 | Updated: 2026-06-26*
  **Feature/Fix:** Interoperability fix for the `OpenAILegacy` adapter. When `thinking` is disabled, the adapter was passing `reasoning_effort=None` to the SDK, which serializes as `"reasoning_effort": null`. Strict OpenAI-compatible SDKs reject this field. The fix ensures the key is fully omitted.
  **Why it matters:** A technically precise fix that shows attention to API specification compliance. Users relying on OpenAI-compatible proxies or older SDKs will stop seeing parameter validation errors.
  **Link:** MoonshotAI/kimi-cli PR #2476

---

**5. Feature Request Trends**
- **Transparent Model Access/Error Messaging** – The 403 authentication confusion (#2425) points to a strong demand for clearer tiered licensing signals. The community wants the CLI to distinguish between "invalid key" and "key valid but model requires a different agent tier" in error messages.
- **Robust Plan Mode State Machine** – The inconsistency in #2478 implies developers are heavily relying on structured planning. There is a clear request for deterministic state transitions, including a "forced exit" override command for when the internal state gets out of sync.
- **Terminal Input Hygiene** – The double-keypress bug (#2477) reflects a general frustration with input event handling. A request for better Linux tty integration and explicit stdout flushing is implicit in this report.

---

**6. Developer Pain Points**
- **State Machine Deadlocks** – (#2478) The Plan mode inconsistency creates a "Catch-22" where the system reminds the agent it is in a mode, but the exit command is rejected. This is a critical workflow blocker that undermines user trust in agentic modes.
- **Opaque Authorization Failures** – (#2425) Gateway errors (HTTP 403) are reported without enough context to self-diagnose. Developers must open a bug report and engage in a 10-comment thread to understand basic licensing restrictions.
- **Unreliable Terminal Event Handlers** – (#2477) On Linux, raw input events are not being consumed correctly, and command output is lost. This degrades the interactive development experience significantly, especially for power users running custom shell environments.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest based on the latest GitHub activity.

---

# OpenCode Community Digest • 2026-06-27

## 1. Today's Highlights
The community is heavily engaged around pricing equity following DeepSeek's latest price cuts, with Issue [#28846](https://github.com/anomalyco/opencode/issues/28846) ballooning to 85 comments demanding subscription limit adjustments. On the UX front, a sweeping fix for the much-criticized Question Tool overlay has landed in PR [#34116](https://github.com/anomalyco/opencode/pull/34116), closing six long-standing issues in one patch. Infrastructure reliability remains a focus, with a wave of automated PRs merging to harden stream handling, retry backoffs, and Windows process management.

## 2. Releases
**No new releases in the last 24 hours.** The project remains on its current stable track.

## 3. Hot Issues

1. **[#28846 – Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)** *— 85 comments, 82 👍*
   The hottest topic by far. Users argue that the DeepSeek pricing collapse must be reflected in subscription usage tiers to maintain fair value.

2. **[#23153 – Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)** *— 12 comments, 23 👍*
   Persistent demand for cryptocurrency payment options alongside standard fiat for OpenCode Go subscriptions.

3. **[#18108 – Truncated tool calls are misclassified and unrecoverable](https://github.com/anomalyco/opencode/issues/18108)** *— 7 comments, 2 👍*
   A critical bug where models hit `maxOutputTokens` mid-tool-call, generating truncated JSON that traps the agent in an unrecoverable retry loop.

4. **[#32149 – Opencode Stops Processing Requests Without Response](https://github.com/anomalyco/opencode/issues/32149)** *— 6 comments, 2 👍*
   The desktop app silently stops producing output after the "thinking" phase, leaving no error message. A significant reliability concern.

5. **[#28956 – Question prompt overlay blocks response text with no minimize/close option](https://github.com/anomalyco/opencode/issues/28956)** *— 5 comments*
   A specific instance of the overarching Question Tool UI problem, highlighting the lack of any dismiss functionality.

6. **[#31430 – Bedrock Mantle for GPT 5.5 can return empty successful responses](https://github.com/anomalyco/opencode/issues/31430)** *— 5 comments*
   A provider-specific trap: HTTP 200 responses with empty bodies are treated as success, silently aborting the agent's current task.

7. **[#17797 – TUI: Modified files are no longer shown](https://github.com/anomalyco/opencode/issues/17797)** *— 4 comments*
   A regression report indicating the "diff stats" panel in the TUI sidebar has disappeared after a recent update.

8. **[#17873 – Preserve Model Selection Per Chat](https://github.com/anomalyco/opencode/issues/17873)** *— 4 comments*
   A quality-of-life request asking for model choices to be isolated to individual chat sessions rather than overwritten globally.

9. **[#33618 – Qwen 3.7 Plus/Max (via OpenRouter) unknown/invalid tool calls](https://github.com/anomalyco/opencode/issues/33618)** *— 3 comments*
   Sporadic failures showing empty tool call names (`✗ "" failed`), causing repeated aborts with newer Qwen frontier models.

10. **[#34087 – Opencode not returning responses (v1.16.2)](https://github.com/anomalyco/opencode/issues/34087)** *— 3 comments*
    A fresh report of the silent no-response bug on the latest desktop version, suggesting a potential regression.

## 4. Key PR Progress

1. **[#34116 – fix(app): question UI fixes and UX improvements](https://github.com/anomalyco/opencode/pull/34116)** *by eXamadeus*
   **Biggest win of the day.** Closes six issues (#14924, #32791, #15896, #15353, #19400, #28956) addressing the blocking Question Tool dialog, making it collapsible and non-obtrusive.

2. **[#34135 – feat(tui): add child agent picker](https://github.com/anomalyco/opencode/pull/34135)** *by opencode-agent[bot]*
   Replaces the parent composer with an on-demand child-agent picker in the TUI, sorted by running state and recency.

3. **[#34138 – feat(tui): open provider auth URL](https://github.com/anomalyco/opencode/pull/34138)** *by opencode-agent[bot]*
   Adds an `o` shortcut to V2 provider authorization dialogs to directly open the URL in the default browser.

4. **[#29281 – fix(opencode): prevent process.exit() from killing parent terminal on Windows](https://github.com/anomalyco/opencode/pull/29281)** *by LifeJiggy*
   Critical Windows fix where `process.exit()` was sending `CTRL_CLOSE_EVENT` and forcibly terminating the parent shell.

5. **[#33547 – fix(go): filter models list to only show oa-compat supported models](https://github.com/anomalyco/opencode/pull/33547)** *by devinoldenburg*
   Fixes the Go API endpoint returning models in the catalog that are not compatible with the Go inference path.

6. **[#34137 – fix(desktop): handle moved projects and deleted paths](https://github.com/anomalyco/opencode/pull/34137)** *by opencode-agent[bot]*
   Improves project detection when directories are renamed or deleted, preventing the desktop app from redirecting to stale locations.

7. **[#29457 – fix(plan): don't carry plan model into build agent on plan_exit](https://github.com/anomalyco/opencode/pull/29457)** *by fmb4910-ops*
   Resolves a subtle agent corruption where the planning model configuration leaked into the execution/build agent.

8. **[#29412 – fix(opencode): repair common tool-input shape failures before retry](https://github.com/anomalyco/opencode/pull/29412)** *by paymog*
   Adds a validation-and-repair layer that attempts to fix malformed tool-call JSON before failing or retrying.

9. **[#29446 – fix(opencode): bound codex stream stalls](https://github.com/anomalyco/opencode/pull/29446)** *by avilabss*
   Introduces timeouts for ChatGPT/Codex OAuth streams to prevent infinite hangs when the upstream stalls.

10. **[#29404 – fix(core): handle JSON parse failure gracefully in models-dev](https://github.com/anomalyco/opencode/pull/29404)** *by levgiorg*
    Wraps a `JSON.parse()` in a try/catch to prevent a hard crash on startup when blocked networks return HTML instead of JSON.

## 5. Feature Request Trends

- **Pricing Flexibility:** The dominant theme is demanding proportionality—users want subscription usage limits and tiers to dynamically reflect the cratering cost of frontier API inference (DeepSeek). This is coupled with sustained pressure for cryptocurrency payment support.
- **Non-Blocking Agent UI:** The single highest-volume UI request is making the "Question Tool" dialog non-modal. Users need to minimize, collapse, or scroll behind the overlay to review conversation context before providing answers.
- **Session State Isolation:** Multiple requests ask for model selection, context windows, and session titles to be strictly isolated per chat. Users are frustrated by memory contexts polluting session titles and model choices leaking between chats.
- **Configuration Hardening:** There is a growing demand for explicit configuration flags to be strictly enforced by the runtime, stemming from bugs where `auto: false` and environment variables are silently ignored.

## 6. Developer Pain Points

- **Unrecoverable Agent Errors:** The "doom loop" pattern—truncated tool calls, stalled streams, or silent empty responses—is the top technical pain point. These issues break the fundamental promise of autonomous agentic coding and waste substantial developer time in debugging non-deterministic failures.
- **UI Locking Conversation Context:** The Question Tool overlay blocking the conversation history is not merely cosmetic; it directly degrades the quality of agent collaboration by preventing users from verifying context before responding.
- **Provider-Specific Fragility:** A steady stream of issues specific to individual providers (Bedrock empty responses, Qwen malformed calls, GLM image failures, Copilot 403s) highlights the immense complexity of maintaining consistent behavior across the rapidly diversifying LLM ecosystem.
- **Windows Stability Gap:** From `process.exit()` killing the terminal to app launches failing silently, Windows users continue to bear the brunt of platform-related stability regressions.
- **Silent No-Response States:** Reports of the desktop app entering a "thinking" state and producing zero output—without error messages—are deeply concerning for a tool that developers rely on for productivity.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

**Pi Community Digest — 2026-06-27**

---

### 1. Today’s Highlights

TUI/terminal stability commanded developer attention this cycle as multiple high‑comment reports detailed forced scroll‑to‑bottom behavior and scrollback‑clearing redraws, with a targeted fix already open in the PR pipeline ([#6026](https://github.com/earendil-works/pi/pull/6026)). Provider extensibility continued to gain momentum with community contributions adding Friendli and Amazon Bedrock Mantle support, while a flurry of embedded‑library issues revealed hard architectural blockers for programmatic use of the coding agent. Finally, an experimental pi‑orchestrator daemon previews a future where Pi can manage multiple agent instances over a Unix socket.

---

### 2. Releases

**No new releases** were published in the last 24 hours.

---

### 3. Hot Issues

*10 noteworthy issues selected from 31 active items.*

- **[#5825 – Streaming markdown forces scroll to bottom](https://github.com/earendil-works/pi/issues/5825)**
  *33 comments, 0 👍*  
  The most‑active bug today. When `clear on shrink` is enabled, reading ahead in streaming markdown output is impossible because Pi forces the terminal scroll position to the bottom every few seconds. Community consensus marks it as a critical UX regression.

- **[#4877 – Session folder collision](https://github.com/earendil-works/pi/issues/4877)**
  *19 comments, 2 👍*  
  Path normalization can map distinct working directories (e.g., `/a/b/c/d` vs `/a-b/c-d`) to the same session storage folder. Low probability but a data‑integrity landmine waiting for a user.

- **[#5363 – Add amazon-bedrock-mantle provider](https://github.com/earendil-works/pi/issues/5363)**
  *15 comments, 4 👍*  
  The existing Bedrock provider uses the Converse API; Bedrock Mantle models require an OpenAI‑compatible endpoint. High upvote count reflects strong enterprise demand for flexible AWS routing.

- **[#6050 – TUI full redraw clears terminal scrollback](https://github.com/earendil-works/pi/issues/6050)**
  *11 comments, 0 👍*  
  During active agent rendering, the TUI issues destructive full redraws that flush the terminal scrollback buffer entirely, destroying the user’s audit trail.

- **[#5871 – Anthropic OAuth‑token detection hardcoded to sk-ant-oat](https://github.com/earendil-works/pi/issues/5871)**
  *6 comments, 0 👍*  
  The provider relies on a brittle substring check to detect OAuth tokens. Enterprises using custom credential stores or SSO cannot configure the detection logic.

- **[#5992 – Pi crashes due to “value.startsWith is not a function”](https://github.com/earendil-works/pi/issues/5992)**
  *4 comments, 0 👍*  
  Reloading a long session triggers an uncaught `TypeError` in `CustomEditor.getBestAutocompleteMatch`, killing the process and destroying unsaved context.

- **[#6093 – Scoped Anthropic API keys need necessary request params](https://github.com/earendil-works/pi/issues/6093)**
  *3 comments, 0 👍*  
  Claude Code scoped keys (`sk-ant-api03-…`) are indistinguishable from regular keys, leading to mismatched auth headers. Complements the OAuth–detection issue above.

- **[#6101 – Embedded library: shared extension runtime poisoned across sessions](https://github.com/earendil-works/pi/issues/6101)**
  *1 comment, 0 👍*  
  Creating multiple `AgentSession` objects in a single process throws “This extension ctx is stale” on the second session. A critical blocker for embedding Pi as a library.

- **[#6102 – Embedded library: theme Proxy throws “Theme not initialized”](https://github.com/earendil-works/pi/issues/6102)**
  *1 comment, 0 👍*  
  When Pi runs without the TUI, the global `theme` object is a throwing proxy because `initTheme()` is never called. Every extension or core path touching the theme immediately fails.

- **[#6104 – `find` drops first path‑segment character on Windows](https://github.com/earendil-works/pi/issues/6104)**
  *1 comment, 0 👍*  
  Path‑concatenation logic breaks when searching from a bare drive root (e.g., `C:\`), producing corrupted relative paths like `I/…` with doubled trailing slashes.

---

### 4. Key PR Progress

*7 pull requests were updated in the last 24 hours.*

- **[#6026 – fix(tui): stabilize working status row](https://github.com/earendil-works/pi/pull/6026) *(open)***  
  Directly targets the streaming‑scroll bug (#5825). Prevents the working indicator from triggering destructive re‑renders that steal terminal focus.

- **[#6109 – fix(coding-agent): preserve dependency cache on extension reload](https://github.com/earendil-works/pi/pull/6109) *(closed/merged)***  
  Fixes #6108 where release binaries re‑evaluated dependency module side effects on `/reload`. Theme registrations and other side‑effect corruption are now avoided on reload.

- **[#6064 – feat(experimental): pi orchestrator](https://github.com/earendil-works/pi/pull/6064) *(closed)***  
  A substantial experimental package adding a local daemon (`@earendil‑works/pi‑orchestrator`) that manages Pi instance lifecycles over a Unix socket. Opens the door to multi‑instance workflows and persistent background agents.

- **[#6090 – feat(ai): add Friendli provider](https://github.com/earendil-works/pi/pull/6090) *(closed/merged)***  
  Community contribution adding Friendli as a built‑in OpenAI‑compatible provider (`FRIENDLI_API_KEY` auth, default model `zai‑org/GLM‑5.2`).

- **[#6087 – fix(coding-agent): remove hardcoded RPC wait timeout](https://github.com/earendil-works/pi/pull/6087) *(closed/merged)***  
  Removes the 60‑second hard cap in `RpcClient` wait methods. Long‑running MCP tool sessions can now complete without premature failure.

- **[#6099 – Rename model key from gpt-5.2-chat-latest to gpt-5.2-chat](https://github.com/earendil-works/pi/pull/6099) *(closed/merged)***  
  Corrects an erroneous model identifier. The model `gpt‑5.2‑chat‑latest` does not exist; available models are `gpt‑5.2`, `gpt‑5.2‑chat`, and `gpt‑5.2‑codex`.

- **[#6092 – draft: hosted websearch](https://github.com/earendil-works/pi/pull/6092) *(closed)***  
  A draft PR enabling a persistent hosted search tool in the agent loop. Author notes it is not intended for merge but serves as a reference for the hosted‑tooling pattern.

---

### 5. Feature Request Trends

- **Provider Ecosystem Expansion**  
  Demand for natively supported providers is accelerating. Requests for Amazon Bedrock Mantle, Friendli, and configurable Anthropic credential handling show that enterprise teams want to route Pi through their existing AI gateways without relying solely on the custom‑provider escape hatch.

- **TUI Redraw / Viewport Reform**  
  The cluster of scroll‑jank and scrollback‑destruction bugs signals a deep desire for “ocular stability.” Developers want the terminal viewport to behave predictably—no forced scrolls, no erased history.

- **Library Embedding Mode**  
  The multi‑issue flurry from a single developer (wloonis) around `@earendil‑works/pi‑coding‑agent` as a library indicates the community is integrating Pi directly into IDEs and custom toolchains. The current architecture assumes TUI ownership of the process lifecycle, which breaks programmatic usage.

- **Multi‑Session / Orchestration**  
  The experimental orchestrator PR (#6064) is the architectural expression of a desire for running multiple Pi instances, background agent tasks, or daemonized workflows.

---

### 6. Developer Pain Points

1. **Viewport Instability (highest volume)**  
   The combination of forced streamed scroll (#5825) and destructive full redraws (#6050, #6073) is the most disruptive daily irritation. Developers rely on terminal scrollback as their natural log, and Pi keeps erasing or jumping past it.

2. **Extension Isolation & Idempotency**  
   Extensions and their dependencies can register side effects (themes, global state) that are fragile on `/reload`. The ecosystem lacks a sandbox contract for extensions, leading to stale‑context errors (#6101) and double‑evaluation side effects (#6108/#6109).

3. **Authentication Assumptions**  
   Hardcoded token‑prefix checks for Anthropic OAuth (#5871) and the inability to distinguish scoped keys from regular keys (#6093) create friction for enterprise adoption. Auth should be fully configurable and declarative.

4. **Embedded Library Gaps**  
   Using Pi outside the TUI exposes missing initialization paths. The global `theme` object and extension context management are tightly coupled to the interactive app lifecycle, making reliable embedding deeply challenging (#6101, #6102).

5. **Tool Loop Timeouts**  
   Long‑running tools can be silently killed by hardcoded client‑side timeouts in the RPC layer (#6088), and post‑completion hangs persist even after earlier `streamTimeout` fixes (#5944). The tool execution lifecycle is not yet fully hardened.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-27

## Today's Highlights

The v0.19.2 nightly cycle continues with a strong security focus, shipping multiple defense-in-depth patches for source slug validation and credential cache paths. On the platform reliability front, the daemon receives a critical fix for cross-connection ACP permission votes and a resumable session stream, while the community RFC for "qwen tag" (a persistent multiplayer channel agent) has already yielded a Phase 0 implementation. The biggest operational fire this week—a Windows PowerShell OOM regression where every tool call leaked an unclosed process—has been triaged and closed.

---

## Releases

- **[`v0.19.2-nightly.20260627.d93bec905`](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.2-nightly.20260627.d93bec905)**: Includes `fix(core): allow web_fetch JSON fallback` and standard release housekeeping.
- **[`cua-driver-rs-v0.6.8`](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.6.8)**: Updated prebuilt binaries vendored under `packages/cua-driver`. macOS now ships code-signed and notarized universal binary + `.app`. Linux (x86_64 + arm64, glibc 2.31+) and Windows (x86_64 + arm64) remain unsigned. Enables the **relative-coordinate** fork.

---

## Hot Issues

1. **[#5873 — Windows: every tool call spawns a PowerShell process that never closes, causing OOM](https://github.com/QwenLM/qwen-code/issues/5873) (Closed, P1)**
   A high-severity regression: on Windows, every tool invocation opened a new `powershell` process with no cleanup, leading to guaranteed memory exhaustion. Community frustration peaked ("I really want to swear"). Marked as ready for agent and closed.

2. **[#5083 — TUI freezes due to zombie bash child processes](https://github.com/QwenLM/qwen-code/issues/5083) (Open, P2)**
   Users report the CLI TUI becoming completely unresponsive during sessions on Linux. Diagnosis points to an unreaped zombie `bash` process (PID 255709) persisting for ~4 minutes, blocking UI input. Points to a gap in subprocess lifecycle management.

3. **[#5819 — Auto-upgrade silently swaps model to higher cost tier](https://github.com/QwenLM/qwen-code/issues/5819) (Open, P2)**
   After auto-upgrading from v0.18.3 to v0.19.x, `settings.json` was modified without user consent to switch from `DeepSeek-4 flash` to a premium model, exhausting prepaid credits until SMS alerts fired. A major trust issue with the self-update mechanism.

4. **[#5756 — Default 8K output cap truncates large `write_file` calls](https://github.com/QwenLM/qwen-code/issues/5756) (Open, P2)**
   `CAPPED_DEFAULT_MAX_TOKENS=8000` overrides the model's real output limit, causing repeated truncation failures when generating large files (e.g., wikis). The model enters expensive retry loops, wasting tokens and time.

5. **[#5894 — Edit tool result summary appended to every subsequent response](https://github.com/QwenLM/qwen-code/issues/5894) (Open, P2)**
   After using the edit tool, the "File changed" diff block is persistently re-appended to all future replies, polluting the context window and confusing the model across turns.

6. **[#5823 — Silent `/loop` cron tasks with no visibility or kill mechanism](https://github.com/QwenLM/qwen-code/issues/5823) (Open, P2)**
   A user discovered old scheduled tasks auto-executing in fresh sessions days later, with no UI to list, inspect, or terminate active loops. Background automation running without the user's knowledge is a serious UX trust breaker.

7. **[#5055 — VSIX flagged as Trojan by Windows Defender](https://github.com/QwenLM/qwen-code/issues/5055) (Closed, P1)**
   The v0.18.0 VSIX triggered `Trojan:JS/ShaiWorm.DBA!MTB` alerts on Windows 11. This false positive created significant friction and trust concerns for enterprise users.

8. **[#5834 — Source deletion accepts path traversal slugs](https://github.com/QwenLM/qwen-code/issues/5834) (Closed, P1)**
   A crafted `sourceSlug` containing `../` could escape the workspace `sources` directory during deletion. Promptly fixed via a stricter slug guard (PR #5829).

9. **[#4175 — Mode B (`qwen serve`) production readiness roadmap](https://github.com/QwenLM/qwen-code/issues/4175) (Open)**
   The strategic tracking issue for making the daemon production-grade. Stage 1 HTTP/SSE routes, auth, and same-workspace multiplexing are live; remaining work covers command gap analysis and session durability.

10. **[#5887 — "qwen tag": Multiplayer channel-resident agent (DingTalk-first)](https://github.com/QwenLM/qwen-code/issues/5887) (Open, P3)**
    A highly-upvoted proposal for a persistent shared agent living in chat groups, enabling multi-user collaboration within a single session. Inspired by Claude Tags. An RFC + Phase 0 PR (#5888) landed same-day.

---

## Key PR Progress

1. **[#5915 — fix(core): silence unknown schema format warnings](https://github.com/QwenLM/qwen-code/pull/5915)**
   Suppresses the Ajv `unknown format "uint64" ignored in schema` warnings that were polluting the CLI startup output. Small change, high visible impact.

2. **[#5914 — fix(desktop): harden remaining source path validation](https://github.com/QwenLM/qwen-code/pull/5914)**
   Rolls up remaining defense-in-depth for source slug-to-path edges (session MCP server resolution, cache paths) without loosening the core guard from #5829.

3. **[#5911 — fix(desktop): normalize source slug validation errors](https://github.com/QwenLM/qwen-code/pull/5911)**
   Refactors `config_validate` fallback paths and slug error handling to return structured validation results instead of uncaught generic failures.

4. **[#5912 — fix(daemon): resolve ACP permission votes across connections](https://github.com/QwenLM/qwen-code/pull/5912)**
   Fixes a fundamental daemon design flaw where ACP permission requests were scoped to the single streaming connection, breaking multi-connection permission workflows.

5. **[#5890 — feat(loop): inject `.qwen/loop.md` task file at fire time](https://github.com/QwenLM/qwen-code/pull/5890)**
   Implements the feature from #5889: long-running loops can carry a durable, user-editable task file. The model opts in via a sentinel prompt, enabling mid-run task editing without restarts.

6. **[#5888 — feat(channels): qwen tag — RFC + Phase 0](https://github.com/QwenLM/qwen-code/pull/5888)**
   The initial implementation of the multiplayer channel-resident agent. Built on existing channel adapters and the `qwen serve` daemon rather than a separate service. Works via distributed session locking and a shared tag registry.

7. **[#5869 — feat(web-shell): stream-highlight code blocks](https://github.com/QwenLM/qwen-code/pull/5869)**
   Eliminates the flickering between plain and highlighted code during streaming in the web shell. Re-tokenizes incrementally so highlighting is smooth and immediate.

8. **[#5852 — feat(daemon,sdk): resumable `/acp` session stream](https://github.com/QwenLM/qwen-code/pull/5852)**
   Wires standard SSE `id:` lines into session events so reconnecting clients can use `Last-Event-ID` to resume from where they left off. Also exports SDK transports.

9. **[#5829 — fix(desktop): reject unsafe source slugs before deletion (Merged)](https://github.com/QwenLM/qwen-code/pull/5829)**
   Closes the CWE-22 path traversal vulnerability from #5834. Invalid source identifiers are rejected before the delete path is resolved.

10. **[#5778 — feat(cli): add `/model --vision` for fallback vision model](https://github.com/QwenLM/qwen-code/pull/5778)**
    Introduces a `visionModel` setting and CLI command so image-capable models can be configured as fallbacks when the main text-only model receives an image input.

---

## Feature Request Trends

- **Multiplayer / Persistent Channel Agents:** The strongest signal this week is the community's desire for shared-agent workspaces in chat platforms. The "qwen tag" proposal (#5887) addresses the pain point that current sessions are siloed per-user, blocking team collaboration. Expect this to be a major 2026 theme.
- **Transparent Background Automation:** Users want `/loop` to be durable, inspectable, and editable without restarting. The `.qwen/loop.md` PR (#5890) and Plan Approval Gate proposals (#5881) reflect demand for safe, visible autonomous execution.
- **Daemon Production Hardening (Mode B):** The relentless push for `qwen serve` stability is the dominant infra-level theme: resumable streams (#5852), cross-connection permissions (#5912), and complete command coverage (#4175, #5677).
- **Multimodal / Vision Integration:** The `/model --vision` PR (#5778) signals growing demand for native image handling within the code agent workflow, beyond simple file references.
- **Hot-Reload Everything:** Issue #3696 for comprehensive runtime hot-reload of skills, extensions, and MCP configurations remains a long-standing quality-of-life ask for power users.

---

## Developer Pain Points

- **Uncontrolled Process Proliferation:** The Windows OOM bug (#5873) and Linux zombie process issue (#5083) expose a recurring pattern: tool execution spawning persistent OS processes without reliable teardown. This is the single most impactful reliability gap.
- **Auto-Updates Undermining User Autonomy:** The unauthorized model swap bug (#5819) highlights deep anxiety about the self-update system. Users demand explicit consent and notification before changes that affect billing or default model tiers.
- **Hidden Background Execution:** The silent cron issue (#5823) is a trust breaker. Background automation that runs invisibly with no user interface for listing, pausing, or killing tasks creates dangerous "black box" behavior.
- **Context Pollution from Tool Results:** The edit tool summary being repeatedly appended (#5894) and the 8K cap truncation (#5756) both contribute to "context decay"—the model's effective working memory fills up with garbage, degrading performance while still burning tokens.
- **Security Confidence Gap:** The Trojan false positive (#5055) and the path traversal vulnerability (#5834) underscore the community's sensitivity to security. Even false positives cause significant friction, especially for enterprise adopters.
- **CI/CD Friction for Contributors:** Cross-PR test contamination (#5882) and stale CI green checks (#4805) create a frustrating contribution experience where reviewers cannot trust CI results, wasting time on environment-specific failures.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest — 2026-06-27

## 1. Today's Highlights

The CodeWhale project had an intense 24 hours of integration, stabilization, and community grooming. The maintainer harvested two significant community contributions—the OpenModel provider and the WeCom Bridge documentation—while closing the v0.8.59 release tracker which fixes the macOS mouse-report leak. A simultaneous batch of dependency upgrades (rusqlite, sha2, Docker actions) and the reactivation of stale-issue automation signal a strong push for codebase hygiene ahead of the v0.9 architecture work.

## 2. Releases

No new releases were tagged in the last 24 hours. The next expected stable release is the v0.8.59 stabilization train, which resolves the mouse-report leak and clears the current maintainer queue.

## 3. Hot Issues

* **#3063 — v0.8.59 Release Tracker (CLOSED):** The stabilization release is finalized, including the macOS TUI mouse-report input leak fix and a full triage of the current issue/PR queue.  
  [Hmbown/CodeWhale#3063](https://github.com/Hmbown/CodeWhale/issues/3063)

* **#861 — Thinking Collapse Fix (CLOSED):** A milestone for reasoning model users. The four root causes of frozen spinners, silent truncation, and dropped `reasoning_content` (which caused HTTP 400 on subsequent turns) have been audited and resolved via #3016.  
  [Hmbown/CodeWhale#861](https://github.com/Hmbown/CodeWhale/issues/861)

* **#3657 — Editor Freeze (OPEN):** A critical UX defect where activating the editor in draft mode hard-locks the entire application, requiring `kill -9`. High community urgency.  
  [Hmbown/CodeWhale#3657](https://github.com/Hmbown/CodeWhale/issues/3657)

* **#3582 — Install.sh HTML Regression (CLOSED):** A critical onboarding blocker where the curl endpoint served a Next.js HTML page instead of the shell script. Resolved.  
  [Hmbown/CodeWhale#3582](https://github.com/Hmbown/CodeWhale/issues/3582)

* **#1186 — Typed Persistent Permissions (OPEN):** A highly-discussed enhancement to the exec policy layer proposing structured `allow/deny/ask` rules scoped by tool name, command prefix, or workspace path.  
  [Hmbown/CodeWhale#1186](https://github.com/Hmbown/CodeWhale/issues/1186)

* **#3537 — i18n Library Overhaul (CLOSED):** The 5,000+ line `localization.rs` is being replaced with a dedicated i18n library to improve compilation speed and translation toolchain integration.  
  [Hmbown/CodeWhale#3537](https://github.com/Hmbown/CodeWhale/issues/3537)

* **#2953 — Slimming Default Prompts (OPEN):** A key performance initiative targeting Codex token parity by profiling and reducing the static prompt footprint.  
  [Hmbown/CodeWhale#2953](https://github.com/Hmbown/CodeWhale/issues/2953)

* **#2870 — EPIC: Command-Boundary Refactor (OPEN):** An architectural epic tracking the breaking of a major refactor into staged, mergeable chunks to avoid destabilizing the codebase.  
  [Hmbown/CodeWhale#2870](https://github.com/Hmbown/CodeWhale/issues/2870)

* **#3638 — Exposed Main Prompt (OPEN):** Community member @DracheTek requests configurable core prompts (Constitution/Personality) for non-engineering use cases like creative writing.  
  [Hmbown/CodeWhale#3638](https://github.com/Hmbown/CodeWhale/issues/3638)

* **#3401 — Hotbar QA Gate (CLOSED):** A release QA matrix for v0.8.66 proving the complex interplay of config, key input, sidebars, and MCP commands works end-to-end.  
  [Hmbown/CodeWhale#3401](https://github.com/Hmbown/CodeWhale/issues/3401)

## 4. Key PR Progress

* **#3677 / #3585 — OpenModel Provider (Merged):** Authored by @noaft, harvested by the maintainer. OpenModel is now a first-class Anthropic Messages provider defaulting to `deepseek-v4-flash`.  
  [Hmbown/CodeWhale#3677](https://github.com/Hmbown/CodeWhale/pull/3677)

* **#3678 / #3640 — WeCom Bridge Docs (Merged):** Authored by @pkeging. Adds a full deployment guide and security section for the WeCom bridge integration.  
  [Hmbown/CodeWhale#3678](https://github.com/Hmbown/CodeWhale/pull/3678)

* **#3575 — Moraine MCP Recall Tool (Open):** Wires `moraine-mcp` as a default recall tool source, enabling session search, file attention, and session history for agents via MCP.  
  [Hmbown/CodeWhale#3575](https://github.com/Hmbown/CodeWhale/pull/3575)

* **#3674 — Runtime Auth Refactor (Merged):** @cyq1017 extracted auth/token/cookie helpers into `runtime_api/auth.rs`, improving code organization without changing auth behavior.  
  [Hmbown/CodeWhale#3674](https://github.com/Hmbown/CodeWhale/pull/3674)

* **#3679 — CI OHOS Resilience (Merged):** The release drift workflow now retries the OHOS `cargo tree` probe before failing, reducing flaky CI failures while preserving real error reporting.  
  [Hmbown/CodeWhale#3679](https://github.com/Hmbown/CodeWhale/pull/3679)

* **#3673 / #3672 — sha2 0.11 Upgrade (Merged):** Handled the breaking `LowerHex` formatting change while maintaining hash stability across CLI, TUI, Fleet, and tool receipts.  
  [Hmbown/CodeWhale#3673](https://github.com/Hmbown/CodeWhale/pull/3673)

* **#3675 — rusqlite Bump (Merged):** Upgraded to 0.39.0, carefully avoiding a 0.40.1 vendor build regression caused by `unstable cfg_select!` usage.  
  [Hmbown/CodeWhale#3675](https://github.com/Hmbown/CodeWhale/pull/3675)

* **#3680 — Fix Stale Doc Paths (Open):** @findshan fixes broken file paths in `CONTRIBUTING.md` PR exemplars, improving the new contributor experience.  
  [Hmbown/CodeWhale#3680](https://github.com/Hmbown/CodeWhale/pull/3680)

* **#3607 — Stale Issue Automation (Open):** Re-activates GitHub Actions stale management with specific policies (e.g., `bug + needs-info` ages out unless it carries a `release-blocker` label).  
  [Hmbown/CodeWhale#3607](https://github.com/Hmbown/CodeWhale/pull/3607)

* **#3676 / #3621 — Provider Links Fix (Merged):** Also by @noaft. Fixes the fallback docs URL and adds a Qianfan-specific documentation link.  
  [Hmbown/CodeWhale#3676](https://github.com/Hmbown/CodeWhale/pull/3676)

## 5. Feature Request Trends

* **Memory & Execution Governance:** A consistent push for "stateful agents" that remember permissions (typed allow/deny/ask rules) and session history (MCP-backed Moraine recall tools).  
* **Provider & Behavior Customization:** Users want deep control over model behavior—configurable core prompts for non-engineering domains and first-class support for alternative providers like OpenModel.  
* **Token Economy (Codex Parity):** Strong community sentiment that CodeWhale is burning too many tokens. Issues specifically target the base prompt size and repeated tool output in transcripts to match Codex CLI efficiency.  
* **CJK & Internationalization:** A heavy i18n investment is underway, driven by a strong Asian developer base. IME composition UI bugs and the 5,000-line localization file are top priorities.

## 6. Developer Pain Points

* **Fragile Onboarding:** The `install.sh` HTML regression (#3582) underscores how easily the first-user experience breaks due to routing changes, creating immediate friction for new adopters.  
* **TUI Critical Stability:** The Editor Freeze (#3657) is a high-severity showstopper that completely halts the primary coding workflow.  
* **Reasoning Model Fragility:** The "thinking collapse" bugs highlight a deep, cross-cutting challenge in streaming reasoning content correctly across different model providers and edge cases.  
* **CI/CD Flakiness:** False-positive failures from OHOS network probes and Nightly cross-target build regressions erode trust in the CI pipeline and slow down release velocity.  
* **Codebase Maintainability:** A 5,000+ line localization file and significant dead-code inventory create high cognitive load for both contributors and maintainers trying to make focused changes.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*