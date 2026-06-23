# AI CLI Tools Community Digest 2026-06-23

> Generated: 2026-06-23 02:54 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Ecosystem — 2026-06-23

## 1. Ecosystem Overview

The AI CLI tool landscape on June 23, 2026 is navigating a tense inflection point: feature velocity remains high across the board, but community trust is increasingly fragile. Universal adoption of MCP (Model Context Protocol) is accelerating, yet every major tool faces spec compliance gaps or lifecycle management bugs that frustrate power users. The most urgent cross-cutting signal is a backlash against opaque token economics and agent inefficiency — users are demanding cost predictability and visible reasoning, not just raw model capability. Enterprise authentication instability (Gemini CLI, Claude Code) and persistent Windows regressions (Claude Code, OpenAI Codex, OpenCode) further suggest that the ecosystem is still maturing from clever prototypes to production-grade daily drivers. The tools that ship reliable cost controls, strict MCP compliance, and cross-platform stability will define the next stage of this market.

## 2. Activity Comparison

| Tool | Releases (24h) | Highlighted Issues | Highlighted PRs | Dominant Community Signal |
|---|---|---|---|---|
| **Claude Code** | v2.1.186 | 10 | 4 | Self-gating reasoning gaps (#60226, 45 comments), Windows data loss (#53717, #12908) |
| **OpenAI Codex** | rust-v0.142.0 stable, v0.143-alpha | 10 | 10+ | 10–20× cost spike (#28879, 239 👍, 121 comments) |
| **Gemini CLI** | None | 10 | 10 | Enterprise OAuth lockout (#28088), historical thought leakage (#27971) |
| **GitHub Copilot CLI** | v1.0.64-2, v1.0.64-3 | 10 | 0 | MCP init-ignore (#1579), session auth loss (#3596), credit burn on restart (#3886) |
| **Kimi Code CLI** | v1.48.0 | 4 | 3 | MCP auto-discovery lockout (#2457), workspace isolation failure (#2469) |
| **OpenCode** | None | 10 | 10 | 26.8 GiB server memory leak (#33213), silent plugin load failure (#33455) |
| **Pi** | v0.79.10 | 10 | 10 | “Working…” hang syndrome (#4945), local LLM demand (#3357) |
| **Qwen Code** | None | 10 | 10 | Systemic input validation gaps (tt-a1i batch), tool execution loop (#5641) |
| **CodeWhale (DeepSeek)** | v0.8.64 (rebrand) | 10 | 11 | Multi-provider routing regressions (#3382), TUI freeze on mult-agent (#3289) |

*Note: “Highlighted Issues/PRs” reflects the top items curated by each digest, not total tracker volume.*

## 3. Shared Feature Directions

**MCP Lifecycle & Compliance (All tools)**
Every tracked tool is actively integrating MCP, but community friction is nearly universal. Claude Code ships MCP CLI authentication, but Kimi Code suffers auto-discovery lockouts (#2457). OpenCode’s highest-voted request is full MCP client capability (#28567). Copilot CLI ignores server initialization instructions (#1579). The gap between *adding MCP support* and *implementing it robustly* is the ecosystem’s widest execution risk today.

**Agent Efficiency & Token Cost Transparency (Claude Code, OpenAI Codex, Gemini, Copilot, Pi)**
Users are growing acutely sensitive to wasted reasoning. Claude Code’s #70198 (“over-investigates instead of measuring”) and #60226 (“flawed reasoning not gated”) capture this precisely. OpenAI Codex’s rate-limit crisis (#28879) shows what happens when metering breaks. Gemini’s MAX_TURNS-as-success (#22323) and Copilot’s invisible credit burn on restart (#3886) reinforce the same theme: **users will not tolerate opaque cost engines.**

**Enterprise Authentication & Policy Hardening (Gemini, Copilot, Claude Code, OpenAI Codex)**
Enterprise OAuth is the top barrier to organizational adoption. Gemini CLI’s #28088 (forced sign-out, blocked re-auth) is the loudest alarm, but Copilot’s missing Intune docs (#3884) and Claude Code’s team API regressions (#68721) point to a systemic gap. Pro account entitlements are broken for OpenAI Codex subscribers (#28504, #29243). The CLI industry must treat Auth as a first-class product surface, not an afterthought.

**Cross-Platform Stability (Claude Code, OpenAI Codex, OpenCode, Qwen Code)**
Windows remains the blind spot. Claude Code’s blank screens (#51143) and update-borne data loss (#53717) are the highest-severity examples, but OpenCode’s stale project cache (#30697), Qwen Code’s Alacritty cursor (#5713), and Codex’s sandbox module errors (#28982) all confirm that platform parity is not keeping pace with feature development.

**Sub-Agent & Workflow Orchestration (Claude Code, OpenCode, CodeWhale, Gemini)**
The industry is moving beyond single-turn agents. OpenCode’s nested sub-agent stack (#32301), Claude Code’s workflow filtering (#60226), CodeWhale’s Fleet sub-agents, and Gemini’s codebase_investigator all signal a structured move toward multi-agent systems. The friction points are equally shared: turn limits, permission gating, and artifact visibility.

## 4. Differentiation Analysis

| Tool | Core Differentiator | Primary User | Critical Vulnerability |
|---|---|---|---|
| **Claude Code** | Deep reasoning & agentic collaboration | Workflow-heavy prompt engineers | Windows neglect; reasoning token cost without output |
| **OpenAI Codex** | OpenAI platform integration (GPT-5.5, Responses API) | ChatGPT Plus/Pro subscribers | 10–20× cost metering bug; high local resource churn |
| **Gemini CLI** | Enterprise GCP security & evaluation infrastructure | GCP/Workspace enterprise teams | OAuth lockout; agent ignoring user config |
| **Copilot CLI** | GitHub ecosystem leverage & sandboxing | GitHub-native developers | MCP compliance lag; session state fragility |
| **Kimi Code CLI** | Monorepo provider schema strictness | MoonshotAI ecosystem | MCP lifecycle regressions; low engagement volume |
| **OpenCode** | TUI plugin architecture & workflow engine | Customization-seeking power users | Stability regressions (memory leaks, silent crashes) |
| **Pi** | Extension API & multi-provider flexibility | Cost-conscious / local-first tinkerers | “Working…” hang syndrome; module identity bugs |
| **Qwen Code** | Open model ecosystem & community contribution energy | Qwen model users, Alibaba Cloud | Systemic input validation; tool loop brittleness |
| **CodeWhale (DeepSeek)** | Multi-provider routing speed & iteration cadence | Chinese cloud ecosystem, DeepSeek users | Rebranding migration tax; provider config complexity |

## 5. Community Momentum & Maturity

**Fastest Iteration:** **CodeWhale** leads with 11 PRs and aggressive provider fixes in a single day, though its rebranding from `deepseek-tui` introduces transitional friction. **Copilot CLI** shipped two point releases in 24 hours, reflecting efficient patch deployment. **OpenCode** is sustaining high structural ambition with its workflow feature stack (5 PRs on a single engine).

**Deepest Community Engagement:** **OpenAI Codex** has the highest-signal community crisis (239 reactions on the cost spike, 121 comments) — a mature user base that knows how to organize and escalate. **Claude Code** maintains the broadest issue surface, with the JSONC request reaching 87 👍 and reasoning-gap threads drawing 45 comments. These communities are demanding accountability.

**Most Structural Maturity:** **Gemini CLI** is investing heavily in evaluation infrastructure (#24353) and security hardening (SSRF dual fixes). **Pi** is paying down architectural debt (Shrinkwrap fix, compaction events) while expanding its provider surface. Both prioritize long-term reliability over headline features.

**Emerging Contributors:** **Qwen Code** benefits from a high-energy contributor (tt-a1i) filing a systematic batch of ~20 validation bugs, indicating a passionate but engineering-rigor-constrained user base. **Kimi Code** remains the quietest, with only 4 issues and 3 PRs updated — the MCP regressions suggest an early-stage product under active build.

## 6. Trend Signals

**“Reasoning on a Dime” is the defining product challenge of 2026.** The backlash against opaque thinking-token costs (Claude #70198, OpenAI #28879, Copilot #3886, Gemini #22323) is the single strongest signal across the ecosystem. Users expect per-step cost accounting, visible reasoning state, and the ability to terminate wasteful loops. Tools that ship “measure twice, cut once” efficiency will win trust; tools that treat thinking as a commodity input will bleed users.

**MCP is becoming the new LSP — but implementation lags spec.** Every tool is racing to support MCP, but spec compliance gaps (Copilot ignoring init instructions), lifecycle bugs (Kimi Code auto-discovery lockout), and desktop/CLI parity failures (OpenAI Codex #28978) create a quality gap that erodes ecosystem confidence. The next six months will separate tools that *integrate* MCP from tools that *master* MCP.

**Cross-platform neglect is a strategic liability.** The concentration of Windows bugs across Claude Code, OpenCode, and Qwen Code is not an accident — it reflects teams optimizing for macOS/Linux and retrofitting Windows support. As enterprise adoption grows, Windows parity becomes a requirement, not a nice-to-have. The tool that invests in first-class Windows UX will capture a disaffected audience.

**Enterprise auth is the adoption gate.** Gemini’s OAuth crisis (#28088), Copilot’s missing MDM documentation (#3884), and Codex’s plan-tier misclassification (#29243) show that authentication and entitlement management are the largest barriers to organizational deployment. The era of “set an API key and go” is over; compliance-ready auth flows are table stakes.

**Local-first is a resilient niche, not a compromise.** Pi’s DeepSeek auto-router (#5970) and local LLM demand (#3357), CodeWhale’s rapid provider expansion, and Qwen’s Vision Bridge (#5126) demonstrate that users value cost control and data privacy as core differentiators. The API pricing volatility around OpenAI Codex (#28879) only strengthens this trend.

**The structured workflow wave is building.** Multi-turn agents, sub-agent spawning (OpenCode #32301, CodeWhale Fleet), and workflow engines are moving from experimental to expected. The friction points (permission gating, turn limits, failure transparency) are shared across tools, suggesting a structured playbook is emerging. The tool that delivers reliable, inspectable multi-agent orchestration will define the next paradigm.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the anthropics/skills repository, based on your requested analysis.

---

### 1. Top Skills Ranking (Most-Discussed PRs)

The following eight Skills PRs have attracted the most community attention based on discussion volume and engagement. All are currently **Open**.

- **[document-typography (#514)](https://github.com/anthropics/skills/pull/514)** — *Typographic Quality Control for Generated Documents*
  A skill designed to prevent orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. The discussion highlights frustration with Claude’s default document formatting and strong demand for cleaner output.
- **[ODT Skill (#486)](https://github.com/anthropics/skills/pull/486)** — *OpenDocument Text Creation and Parsing*
  Adds robust support for ODF (.odt, .ods) file creation and conversion to HTML. The thread shows significant interest from users in enterprise / LibreOffice ecosystems who need open-format document generation.
- **[frontend-design revision (#210)](https://github.com/anthropics/skills/pull/210)** — *Clarity and Actionability Improvements*
  A deep revision of the existing front-end design skill, refactoring every instruction to be single-turn executable. Discussion consensus was that previous design skills were too abstract; this PR is a model for how to write precise skills.
- **[skill-quality-analyzer & security-analyzer (#83)](https://github.com/anthropics/skills/pull/83)** — *Meta-Skills for Ecosystem Quality*
  Two meta-skills that evaluate other Skills across structure, documentation, and security dimensions. Community feedback centered on the need for self-regulating quality standards as the skill count grows.
- **[SAP-RPT-1-OSS predictor (#181)](https://github.com/anthropics/skills/pull/181)** — *Predictive Analytics on SAP Data*
  Integrates SAP’s open-source tabular foundation model for business data analytics. It generated discussion as the strongest vertical enterprise skill proposal to date.
- **[testing-patterns (#723)](https://github.com/anthropics/skills/pull/723)** — *Comprehensive Testing Strategy Skill*
  Covers the Testing Trophy model (Vitest, Playwright, Testing Library) with strong opinions on what to test. The discussion reflects high developer demand for Claude to write reliable tests according to defined patterns.
- **[ServiceNow Platform (#568)](https://github.com/anthropics/skills/pull/568)** — *ITSM, ITOM, SecOps, and IntegrationHub Skill*
  A broad enterprise platform assistant. Discussion focused on scope management and how to cover a massive platform like ServiceNow without context overflow.
- **[AURELION Suite (#444)](https://github.com/anthropics/skills/pull/444)** — *Structured Cognitive and Memory Framework*
  Four skills (kernel, advisor, agent, memory) implementing a professional knowledge management system. Discussion highlights strong community interest in structured agent cognition over generic prompting.

---

### 2. Community Demand Trends (From Issues)

The most concentrated demand trends emerging from the issue tracker are:

- **Skill Development Tooling (The “0% Recall” Blocking Bug)**
  Issues [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169), and [#1061](https://github.com/anthropics/skills/issues/1061) all report that `run_eval.py` consistently returns 0% recall, making the entire description-optimization loop unusable. This is the single loudest technical demand on the repository.
- **Enterprise Distribution and Trust**
  Issue [#228](https://github.com/anthropics/skills/issues/228) (org-wide skill sharing) and [#492](https://github.com/anthropics/skills/issues/492) (namespace security / trust boundary abuse) show the community moving beyond single-user workflows to ask for organizational governance and secure distribution.
- **Agent Governance and Safety**
  Issue [#412](https://github.com/anthropics/skills/issues/412) (proposing an agent-governance skill) and the security discussions in [#1175](https://github.com/anthropics/skills/issues/1175) indicate a growing desire to constrain agent behavior in enterprise contexts.
- **Cross-Platform and Interoperability**
  Persistent Windows compatibility issues ([#1061](https://github.com/anthropics/skills/issues/1061)), interest in Bedrock deployment ([#29](https://github.com/anthropics/skills/issues/29)), and calls to expose Skills as MCP servers ([#16](https://github.com/anthropics/skills/issues/16)) point to demand for wider runtime support.
- **Persistent Memory Systems**
  Proposals like compact-memory ([#1329](https://github.com/anthropics/skills/issues/1329)) and the discussion around PR [#154](https://github.com/anthropics/skills/pull/154) show strong interest in structured memory across conversations.

---

### 3. High-Potential Pending Skills (Likely to Land Soon)

These open PRs target critical infrastructure gaps or high-consensus quality-of-life improvements:

- **[Fix run_eval 0% recall (#1298)](https://github.com/anthropics/skills/pull/1298)** — Directly unblocks the entire skill optimization loop. The most critical pending PR based on community pain.
- **[Windows Subprocess & Encoding Fixes (#1099, #1050)](https://github.com/anthropics/skills/pull/1099)** — Resolve the `[WinError 2]` and cp1252 blocking bugs. Multiple replicators in the issue tracker.
- **[YAML Frontmatter Validation (#361, #539)](https://github.com/anthropics/skills/pull/361)** — Prevents silent truncation of descriptions containing `:` or special characters. Cheap, high-impact fix.
- **[Add CONTRIBUTING.md (#509)](https://github.com/anthropics/skills/pull/509)** — Addresses the 25% GitHub community health score. Clear scope and broad consensus.
- **[Fix PDF Case Sensitivity (#538)](https://github.com/anthropics/skills/pull/538)** — Corrects 8 broken file references blocking the PDF skill on case-sensitive filesystems.

---

### 4. Skills Ecosystem Insight

**The community’s most concentrated demand is shifting from purely proposing new Skills to urgently stabilizing the core skill-creation toolchain and securing enterprise distribution channels, reflecting a maturation from prototyping into a production-grade ecosystem.**

---

# Claude Code Community Digest — 2026-06-23

## Today's Highlights
v2.1.186 lands with practical CLI ergonomics for MCP server authentication and workflow filtering, but the community is wrestling with deeper issues. A highly active thread on self-gating model logic (45 comments) points to fundamental questions about how Claude evaluates the correctness of its own reasoning, while sustained frustration over Windows stability (blank screens, data loss, Defender races) continues to dominate the issue tracker.

## Releases
**[v2.1.186](https://github.com/anthropics/claude-code/releases/...)**  
- **CLI MCP Authentication:** `claude mcp login <name>` and `claude mcp logout <name>` let users authenticate MCP servers without entering the interactive `/mcp` menu. The `--no-browser` flag supports stdin redirect workflows over SSH, a clear win for headless and remote setups.  
- **Workflow Filtering:** The `/workflows` agent view now supports status filtering via the `f` key, bringing basic list ergonomics to a growing surface area of the tool.

## Hot Issues

**[#60226](https://github.com/anthropics/claude-code/issues/60226) — Self-identified reasoning gaps do not gate output** (45 comments)  
*Why it matters:* This is the most commented issue in the 24h window for good reason. The model will explicitly state that its current analysis is unfounded, then proceed to complete that analysis in the same response. The community is actively dissecting whether this is a system prompt failure, a decoding artifact, or something deeper. Users report this pattern confuses workflows requiring reliable self-verification.

**[#68721](https://github.com/anthropics/claude-code/issues/68721) — Regression: native TeamCreate / TeamDelete tools surface in 2.1.177, gone in 2.1.178** (17 comments, 5 👍)  
*Why it matters:* A clean regression affecting the team collaboration layer. Having a core API for team management silently disappear between patch versions erodes confidence in the release process, especially given the tool now actively markets agentic collaboration.

**[#51143](https://github.com/anthropics/claude-code/issues/51143) — Windows Desktop: persistent blank/white screen** (15 comments, 12 👍)  
*Why it matters:* The highest-reacted Windows bug. The Claude Desktop app becomes entirely unusable (Cowork sessions inaccessible), and multiple reinstalls have no effect. For a tool that markets itself as cross-platform, this kind of persistent rendering failure is a significant trust issue.

**[#53717](https://github.com/anthropics/claude-code/issues/53717) — Windows: message content lost after auto-update** (10 comments, 4 👍)  
*Why it matters:* Data loss is the hardest class of bug to recover user trust from. Sessions appear in the sidebar but the JSONL storage files are empty. The auto-update path is particularly dangerous because users have no opportunity to back up before the migration runs.

**[#12908](https://github.com/anthropics/claude-code/issues/12908) — macOS: Conversation history disappears after update** (14 comments, 18 👍)  
*Why it matters:* The macOS counterpart to the Windows data loss issue, but with even stronger community reaction. Conversation history vanishing post-update is one of the most disruptive failure modes for daily users.

**[#17968](https://github.com/anthropics/claude-code/issues/17968) — [FEATURE] Support JSONC for settings files** (16 comments, 87 👍)  
*Why it matters:* The highest-voted open issue by a wide margin. Developers are accustomed to commenting their configuration (VS Code, TypeScript configs), and the lack of comment support in `settings.json` forces workarounds like `_comment` keys. This has massive latent demand.

**[#39975](https://github.com/anthropics/claude-code/issues/39975) — [FEATURE] `/unclear` command / undo for `/clear`** (5 comments, 31 👍)  
*Why it matters:* A simple but highly requested quality-of-life feature. `/clear` is irreversible today, and losing context accidentally means losing a session state. 31 👍 on a closed issue suggests users still strongly want this.

**[#70165](https://github.com/anthropics/claude-code/issues/70165) — iOS: hard-crash on Remote Control session open** (2 comments, new today)  
*Why it matters:* A stack overflow in Swift KeyPath metadata crashes the app on main thread. This is a regression in the latest iOS build (1.260618.0) and blocks the entire mobile remote-control workflow.

**[#67021](https://github.com/anthropics/claude-code/issues/67021) — Bundled ugrep OOM on Linux: bounded `{0,N}` intervals explode DFA compilation** (1 comment, 1 👍)  
*Why it matters:* A niche but severe performance bug. Sending a specific regex pattern to the bundled `ugrep` can consume multiple GB of RSS during DFA construction. This is a landmine for users running `grep`-heavy workflows or linters in CI.

**[#70198](https://github.com/anthropics/claude-code/issues/70198) — Agent over-investigates solo instead of taking a cheap measurement** (1 comment, new today)  
*Why it matters:* A sharp user observation about agent efficiency. When debugging a numeric display defect, the agent spun through multiple turns of internal reasoning about competing theories instead of running a single trivial measurement that would have resolved the ambiguity instantly. This captures a real user-facing cost of "thinking" tokens.

## Key PR Progress

*(4 PRs updated in the last 24 hours)*

**[#70173](https://github.com/anthropics/claude-code/pull/70173) — fix(commit-commands): detect `[gone]` branches with `git branch -vv`**  
*Analysis:* A sharp catch. The `clean_gone` command was piping `git branch -v` (single `-v`) into `grep '[gone]'`, but `git branch -v` only shows commit hashes—it never prints `[gone]`. Without the second `-v`, the command silently no-ops. This fix switches to `-vv` and also fixes the sed/awk parsing for noisy branch names.

**[#63686](https://github.com/anthropics/claude-code/pull/63686) — Bump stale and autoclose timeouts from 14 to 90 days**  
*Analysis:* A lifecycle policy PR aiming to reduce the churn of automatically closing issues after only two weeks of inactivity. While still open, it signals community pushback against aggressive issue gardening that can bury real bugs before triage.

**[#70074](https://github.com/anthropics/claude-code/pull/70074) — docs: fix stale marketplace name in plugin-dev README**  
*Analysis:* The marketplace was renamed from `claude-code-marketplace` to `claude-code-plugins`, but the plugin development docs still referenced the old name. Necessary housekeeping for plugin authors.

**[#70066](https://github.com/anthropics/claude-code/pull/70066) — docs(plugin-dev): update marketplace install instructions**  
*Analysis:* Complements #70074 by updating the actual install flow examples to use `claude --plugin-dir` instead of `cc --plugin-dir` and points contributors to the correct repository for plugin contributions.

## Feature Request Trends

- **Configurability & JSONC:** The demand for JSONC support (#17968, 87 👍) overwhelmingly dominates. Users want to document their `settings.json` with comments. Relatedly, requests are emerging for configurable git polling intervals (#70186) and the ability to intercept and edit a proposed file write in `$EDITOR` before acceptance (#70188).
- **Session UX Recovery:** The `/unclear` command (#39975, 31 👍) has strong demand. It points to a broader desire for session state management that extends beyond just clearing history.
- **Agent Behavior Tuning:** A new class of requests is emerging around making the agent *more direct*. Users want less token waste from over-investigation (#70198), better gating when the model detects its own reasoning is flawed (#60226), and more reliable tool call parsing (#70196).

## Developer Pain Points

- **Windows as a Second-Class Platform:** This is the dominant pain point in the tracker. The combination of persistent blank screens (#51143), data loss during updates (#53717), `EBUSY` rename races with Windows Defender (#67595), cross-device link errors with WSL (#66159), and un-reaped agent process trees (#68394) paints a picture of a platform where core OS integration assumptions are repeatedly violated.
- **Release Stability:** The regression cycle is too tight for some users. The loss of TeamCreate/TeamDelete between 2.1.177 and 2.1.178 (#68721) suggests insufficient regression coverage on the collaboration path. Data loss bugs tied to auto-update (#53717, #12908) compound this.
- **Agent Efficiency Overhead:** Users are growing sensitive to the cost of "thinking" tokens that produce no output. Tool call parse failures that loop (#70196) and multi-turn internal monologues debating trivial decisions (#70198) generate noise and cost without progressing the task. The community is looking for more "measure twice, cut once" reliability from the agent loop rather than "reason indefinitely, act eventually."

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest — 2026-06-23**

---

### 1. Today's Highlights

The community is intensely focused on a severe rate-limit cost regression in Codex `gpt-5.5` ([Issue #28879](https://github.com/openai/codex/issues/28879)), where the per-token cost appears to have jumped 10–20x since June 16, collapsing the 5-hour budget to just 2–3 prompts. Urgent PRs (`#29514`, `#29520`) are in flight to correct the rollout budget prefill and token accounting logic that likely underpins the bug. On a positive note, the infamous 640 TB/yr SQLite logging issue ([Issue #28224](https://github.com/openai/codex/issues/28224)) was resolved with a confirmed 85% reduction in feedback log writes, a major win for SSD endurance and overall system responsiveness.

---

### 2. Releases

| Version | Key Highlights |
|:---|:---|
| **rust-v0.142.0** | Stable release. **New Features:** Redesigned `/usage` interface for viewing and redeeming usage-limit reset credits (with confirmation and retry support, PRs #28154, #28793). Redesigned `/plugins` view that organizes remote plugins into "OpenAI Curated", "Workspace", and "Shared with me" sections. |
| **rust-v0.143.0-alpha.1 / alpha.2** | Cutting-edge alpha builds laying the groundwork for the next stable release. |

---

### 3. Hot Issues

1. **[Issue #28879 (OPEN)](https://github.com/openai/codex/issues/28879) — Rate-limit cost per token jumped ~10-20x**
   *Comments: 121 | Reactions: 👍 239*\
   **Why it matters:** The defining fire of the week. Users on ChatGPT Plus / `gpt-5.5` report the 5-hour budget vanishing in 2–3 prompts with no model or plan change. Session logs show `limit-% consumed per token` spiking dramatically since June 16.

2. **[Issue #28224 (CLOSED)](https://github.com/openai/codex/issues/28224) — SQLite feedback logs can write ~640 TB/year**
   *Comments: 39 | Reactions: 👍 265*\
   **Why it matters:** Merged PRs (#29432, #29457) cut feedback log volume by ~85%, addressing a critical performance and SSD endurance concern. The author closed the issue with thanks to the fix team.

3. **[Issue #28982 (OPEN)](https://github.com/openai/codex/issues/28982) — Windows sandbox setup helper fails**
   *Comments: 29 | Reactions: 👍 9*\
   **Why it matters:** Windows app `26.616.3309.0` cannot launch the native sandbox; the setup helper crashes with “The specified module could not be found”. The issue affects sandbox isolation for Windows Plus users.

4. **[Issue #28978 (OPEN)](https://github.com/openai/codex/issues/28978) — Desktop app MCP error: missing `inputSchema`**
   *Comments: 20 | Reactions: 👍 24*\
   **Why it matters:** Post-update, new Desktop conversations fail immediately with a JSON-RPC validation error, while the CLI with the same config works fine. Indicates a critical Desktop vs. CLI parity bug in MCP server advertisement.

5. **[Issue #28823 (OPEN)](https://github.com/openai/codex/issues/28823) — 5-hour usage meter consuming faster than historical usage**
   *Comments: 16*\
   **Why it matters:** Reinforces the regression reported in #28879. Local telemetry doesn't match the server-side consumption meter, suggesting a backend quota calculation change.

6. **[Issue #25921 (OPEN)](https://github.com/openai/codex/issues/25921) — Crashpad pending dumps growing +5 GB/day**
   *Comments: 13 | Reactions: 👍 3*\
   **Why it matters:** Desktop continuously generates Crashpad dump files (`~/Library/Application Support/com.openai.codex/web/Crashpad/pending`) without bound. One user reported ~50k files growing at 4.9 GB/day.

7. **[Issue #28504 (OPEN)](https://github.com/openai/codex/issues/28504) — Pro account missing reset bank entitlements**
   *Comments: 6 | Reactions: 👍 6*\
   **Why it matters:** Pro ($200/mo) subscribers cannot see or redeem usage-limit reset credits or referral entitlements, making the new `/usage` feature non-functional for a high-value segment.

8. **[Issue #29243 (OPEN)](https://github.com/openai/codex/issues/29243) — Pro $100 plan rate-limited as "Plus"**
   *Comments: 5*\
   **Why it matters:** The 5x $100 Pro tier is misclassified as `plus` in the desktop app (`plan_type=prolite` vs. response header `X-Codex-Plan-Type=plus`), potentially denying users their entitled budget tier.

9. **[Issue #29532 (OPEN)](https://github.com/openai/codex/issues/29532) — Persistent SQLite TRACE churn after v0.142.0**
   *Comments: 2*\
   **Why it matters:** The partial fix (#29432) reduced `responses_websocket` logging, but `#29457` did not fully resolve the issue on macOS. `~/.codex/logs_2.sqlite` continues to grow during normal use.

10. **[Issue #29439 (OPEN)](https://github.com/openai/codex/issues/29439) — CLI continues executing tool calls after SIGINT**
    *Comments: 2*\
    **Why it matters:** SIGINT cancellation does not reliably stop tool execution; the CLI proceeds to run further tool calls. This is a reliability and user-control concern for automation workflows.

---

### 4. Key PR Progress

1. **[PR #29514 (OPEN)](https://github.com/openai/codex/pull/29514) — Skip initial rollout budget prefill**
   **Impact:** Directly addresses the budget drain crisis. Stops charging the initial prompt prefill for each rollout-budget thread, charging only sampled output on the first response, which should significantly reduce the per-turn cost spike.

2. **[PR #29520 (OPEN)](https://github.com/openai/codex/pull/29520) — Scope token-budget accounting to body-after-prefix window**
   **Impact:** Tightens budget accounting to only charge token growth against the configured body budget, respecting the model context window as a safety cap instead of deriving remaining tokens from total active context.

3. **[PR #24092 (OPEN)](https://github.com/openai/codex/pull/24092) — Reject unlowered PowerShell AST regions**
   **Impact:** Critical Windows security fix. Prevents Codex from incorrectly whitelisting PowerShell commands that are disguised via casing tricks in AST syntax (e.g., `EndBlock.Statements`).

4. **[PR #28598 (OPEN)](https://github.com/openai/codex/pull/28598) — Bazel: right-size Rust test targets**
   **Impact:** Developer experience improvement. Defaults generated test targets to `small`, adds per-target size overrides, and eliminates noisy timeout warnings that obscure real test failures.

5. **[PR #27466 (OPEN)](https://github.com/openai/codex/pull/27466) — Trace exec-server JSON-RPC requests**
   **Impact:** Observability upgrade. Propagates W3C trace context across JSON-RPC boundaries, making it possible to correlate client and server work when diagnosing latency or failures in remote exec-server calls.

6. **[PR #29473 (CLOSED)](https://github.com/openai/codex/pull/29473) — Propagate safety buffering treatment metadata**
   **Impact:** New safety infrastructure. Reads request-scoped safety-buffering treatment from HTTP/WS headers, combining it with Responses API signals to expose `showBufferingUi` and `fasterModel` flags through the frontend.

7. **[PR #29527 (OPEN)](https://github.com/openai/codex/pull/29527) — Keep compaction world state aligned with context**
   **Impact:** Fixes a subtle mid-turn compaction bug where replaced context from one environment snapshot could be paired with a stale `WorldState` baseline, preventing deferred environment data from persisting correctly.

8. **[PR #28271 (OPEN)](https://github.com/openai/codex/pull/28271) — Flatten MCP namespace tools for unsupported providers**
   **Impact:** Interoperability fix for non-OpenAI Responses API providers. Proprietary `type: "namespace"` tool wrappers are now flattened based on provider capability, fixing MCP function visibility for third-party providers.

9. **[PR #26705 (OPEN)](https://github.com/openai/codex/pull/26705) — TUI Plugin Sharing 5: Polish remote plugin catalog rows**
   **Impact:** The final PR in the plugin sharing stack. Polish for remote plugin display: admin-disabled plugins appear as read-only, admin-installed plugins sort correctly, and navigation respects catalog sections.

10. **[PR #29155 (OPEN)](https://github.com/openai/codex/pull/29155) — Expose service tier and reasoning effort in OTEL**
    **Impact:** Adds `service_tier` and `model_reasoning_effort` fields to the OTEL `response.completed` event, enabling NVIDIA (and others) to measure Fast mode usage and reasoning effort from CLI telemetry logs.

---

### 5. Feature Request Trends

- **Budget Transparency & Fairness:** Driven by the rate-limit regression, there is heavy demand for predictable, auditable token metering ([#28879](https://github.com/openai/codex/issues/28879), [#28823](https://github.com/openai/codex/issues/28823)), visible plan-tier mapping ([#29243](https://github.com/openai/codex/issues/29243)), and functioning usage-reset credits ([#28504](https://github.com/openai/codex/issues/28504)).
- **Subagent Orchestration:** Users want status-checking APIs and parent-child wait mechanisms so long-running subagents don't get preempted by parent threads ([#16900](https://github.com/openai/codex/issues/16900)).
- **MCP & Plugin Consistency:** Repeated requests for CLI/GUI parity in MCP server handling (CWD resolution, tool advertisement) and local plugin path resolution fixes ([#14449](https://github.com/openai/codex/issues/14449), [#28978](https://github.com/openai/codex/issues/28978)).
- **Windows App Stability:** Sandbox setup, module dependency handling, and PowerShell command classification need hardening for Windows users ([#28982](https://github.com/openai/codex/issues/28982), [#24092](https://github.com/openai/codex/issues/24092)).

---

### 6. Developer Pain Points

- **Rate Limit Cost Spikes:** The single greatest source of friction. Unexpected 10-20x cost-per-token increases make daily allowances unpredictable and effectively break heavy users' workflows ([#28879](https://github.com/openai/codex/issues/28879), [#28886](https://github.com/openai/codex/issues/28886)).
- **Excessive Disk & CPU Overhead:** Crashpad dump accumulation (+5 GB/day) ([#25921](https://github.com/openai/codex/issues/25921)), SQLite log churn ([#29532](https://github.com/openai/codex/issues/29532)), and high idle GPU/CPU activity on Windows ([#29281](https://github.com/openai/codex/issues/29281)) create a significant resource tax for developers running Codex long-term.
- **GUI/CLI Parity Gaps:** The desktop and CLI regularly diverge in behavior (MCP tool visibility, cwd handling, sandbox setup). Workflows that bridge the two often break due to these inconsistencies ([#28978](https://github.com/openai/codex/issues/28978), [#14449](https://github.com/openai/codex/issues/14449)).
- **Cancellation Reliability:** SIGINT handling is unreliable; tool execution can continue even after the user requests termination, creating confusion and potential unintended file system mutations ([#29439](https://github.com/openai/codex/issues/29439)).
- **Crash / Reconnect Loops:** Desktop users face persistent reconnect loops when starting or resuming conversations, accompanied by invisible internal state that resists standard cache-clearing remediations ([#21167](https://github.com/openai/codex/issues/21167)).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-23

## Today's Highlights

Enterprise authentication stability dominates this week's digest: `[#28088](https://github.com/google-gemini/gemini-cli/issues/28088)` reports licensed organization accounts being forcibly signed out with OAuth blocking them entirely, generating the highest community engagement. On the infrastructure side, a cluster of high-impact PRs landed to close SSRF bypass vectors in `web_fetch` (`[#27744](https://github.com/google-gemini/gemini-cli/pull/27744)`, `[#27739](https://github.com/google-gemini/gemini-cli/pull/27739)`) and fix a Node.js 24 OAuth socket reuse regression (`[#28103](https://github.com/google-gemini/gemini-cli/pull/28103)`). Agent behavior quality remains a hot topic, with notable merges addressing thought leakage in history scrubbing (`[#27971](https://github.com/google-gemini/gemini-cli/pull/27971)`) and race conditions in SIGINT cancellation (`[#28096](https://github.com/google-gemini/gemini-cli/pull/28096)`).

## Releases

*None in the last 24 hours.*

## Hot Issues

1. **[#28088 — Enterprise OAuth session failure](https://github.com/google-gemini/gemini-cli/issues/28088)** (P2, Bug, Bot-Triaged)
   The most active issue today. Users with Google Workspace Gemini Code Assist licenses are being abruptly signed out and the CLI then reports the authorized organization account as "unauthorized" during re-authentication. 8 comments and 4 reactions confirm this is a critical blocker for enterprise teams.

2. **[#25166 — Shell execution sticks on "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, Bug)
   A persistent frustration: Gemini executes a simple CLI command, the command finishes, but the UI retains it as active and hangs. 3 reactions underscore the disruption to automated shell workflows. A maintainer-only issue with medium effort estimate.

3. **[#22323 — Subagent MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, Bug)
   The `codebase_investigator` subagent hits its turn limit without completing analysis, yet surfaces `status: "success"` and `Termination Reason: "GOAL"`. This erodes trust in agent evaluation metrics and requires retesting.

4. **[#28101 — Unable to log in to Gemini CLI normally](https://github.com/google-gemini/gemini-cli/issues/28101)** (P2, Bug, Need-Info)
   A fresh report with screenshots showing a complete login failure. Paired with #28088, auth stability is clearly the community's biggest pain point today.

5. **[#27741 — CLI ignores existing architectural patterns and deletes working code](https://github.com/google-gemini/gemini-cli/issues/27741)** (P2, Bug)
   A developer reports two systematic issues: the model introduces parallel structures instead of extending existing ones, and it silently deletes working code (e.g., route handlers). Closed by bot but revealing of trust gaps in autonomous editing.

6. **[#26525 & #26522 — Auto Memory redaction, logging, and retry loops](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, Bugs)
   Twin security/stability issues from the same author. Secrets flow into model context *before* the redaction prompt applies, and low-signal sessions are retried indefinitely because the extraction agent never marks them as processed.

7. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, Epic, AIQ/Eval Infra)
   A major roadmap item growing the behavioral eval suite from 76 tests toward structured component-level evals. Signals the team's increased focus on measurable agent quality.

8. **[#24246 — 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, Bug)
   Users hitting API limits when tool counts exceed 128. Community wants smarter automatic tool scoping rather than imposing arbitrary limits.

9. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (P2, Bug, Maintainer-Only)
   A concerning config trust regression: users who explicitly set Agents to "disabled" found subagents executing autonomously after a CLI update. Needs retesting.

10. **[#27740 — Code generation inserts parameters in the middle of signatures](https://github.com/google-gemini/gemini-cli/issues/27740)** (P2, Bug)
    A smaller but high-friction pattern: when asked to add a parameter, the model inserts it between existing positional arguments instead of appending it, breaking all callers. Highlights a fundamental gap in code generation precision.

## Key PR Progress

1. **[#28103 — Fix OAuth keep-alive socket reuse for Node.js 24](https://github.com/google-gemini/gemini-cli/pull/28103)** (P2, Security)
   Lands urgently to fix a Node.js `http.Agent` socket-reuse regression (`>=24.17.0`) causing `ERR_STREAM_PREMATURE_CLOSE` during "Sign in with Google". Directly addresses the auth crisis.

2. **[#28000 — Fix Jupyter Notebook and JSON corruption in write_file](https://github.com/google-gemini/gemini-cli/pull/28000)** (Size/M, Closed)
   Merged fix for a critical bug where `write_file` silently corrupted `.ipynb` and `.json` files, rendering them unparseable. High impact for data science and configuration workflows.

3. **[#28096 — Drop late tool calls following SIGINT cancellation](https://github.com/google-gemini/gemini-cli/pull/28096)** (Area/Agent, Size/M)
   Closes a race condition where Ctrl+C fails to stop tool execution side effects. The standalone `ToolExecutor` now respects cancellation signals properly.

4. **[#27971 — Strip internal thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)** (Size/M, Open)
   Resolves an insidious "thought leakage" bug where model monologues leak into plain-text history, confusing subsequent turns and causing infinite loop emulation. Critical for long-running session stability.

5. **[#28053 — Defensive path resolution for @-prefixed files](https://github.com/google-gemini/gemini-cli/pull/28053)** (Size/XL, Open)
   Comprehensive fix for the `read_file`/`write_file` failures when the model encounters paths like `@policies/new-policies.txt`. Includes macOS test fixes.

6. **[#27739 & #27744 — Comprehensive SSRF guard for web_fetch](https://github.com/google-gemini/gemini-cli/pull/27739)** (Size/M-L, Closed)
   Dual-fix closing gaps where DNS hostnames (e.g., `127.0.0.1.nip.io`) and redirects could bypass `isPrivateIp()` checks. Significant security hardening for the tooling surface.

7. **[#27915 — Trust dialog discloses correct hook shape](https://github.com/google-gemini/gemini-cli/pull/27915)** (P1, Security, Open)
   Fixes a dangerous inverse display bug: the dialog showed the opposite of the hooks that will actually run. Closes a potential social engineering / arbitrary execution vector.

8. **[#27936 & #28100 — VS Code companion Disposable registration fixes](https://github.com/google-gemini/gemini-cli/pull/27936)** (P2, Core)
   Twin PRs fixing JavaScript comma-operator bugs in `context.subscriptions.push()` that leaked the first Disposable of each pair, causing improper cleanup on deactivation.

9. **[#28094 — Deep-merge user and workspace settings in A2A server](https://github.com/google-gemini/gemini-cli/pull/28094)** (P2, Core)
   Resolves a configuration landmine where nested sections (`tools`, `telemetry`, `experimental`) defined in workspace settings completely overwrote user settings instead of merging.

10. **[#28015 — Cloud Run webhook ingestion service for Caretaker](https://github.com/google-gemini/gemini-cli/pull/28015)** (Size/L, Open)
    Infrastructure PR establishing a formal GitHub webhook pipeline using Cloud Run and Pub/Sub. Indicates maturation of the project's automated issue triage infrastructure.

## Feature Request Trends

- **Structured Evaluation Infrastructure**: The push for component-level evals (`#24353`) continues, driven by the desire to catch logic bugs like the MAX_TURNS false success (`#22323`) before they reach users.
- **AST-Aware Code Intelligence**: Multiple epics (`#22745`, `#22746`) request AST-aware file reading, search, and codebase mapping to reduce token waste and improve edit precision (e.g., not breaking callers when adding params, #27740).
- **Agent Trust & Safety Controls**: Recurring themes around the agent respecting system boundaries—avoiding destructive commands (`#22672`), adhering strictly to user configuration (`#22093`, `#22267`), and not deleting working code (`#27741`).
- **Deterministic Auto Memory**: The community wants a memory system that doesn't leak secrets (`#26525`), loops on low-quality content (`#26522`), or silently drops invalid patches (`#26523`).
- **Usability & Debuggability**: Subagent trajectory visibility (`#22598`), comprehensive bug reports including subagent context (`#21763`), and CLI self-awareness of its own flags/hotkeys (`#21432`) are consistently requested quality-of-life improvements.

## Developer Pain Points

- **Enterprise Authentication Instability**: The sudden sign-out and blocked OAuth for licensed accounts (`#28088`) combined with general login failures (`#28101`) represents the loudest immediate blocker, threatening enterprise adoption.
- **Agent Autonomy vs. User Configuration**: Users frequently report agents ignoring explicit settings (permissions, `#22093`; settings overrides, `#22267`; custom skills, `#21968`), creating a persistent trust deficit.
- **Code Corruption and Lack of Awareness**: Silent code deletion (`#27741`), breaking function signatures (`#27740`), and file format corruption (`#28000`) severely undermine confidence in AI-generated edits.
- **Shell Execution Friction**: The "Waiting input" hang (`#25166`) and getting stuck on interactive prompts (`#22465`) remain high-frequency breaks in terminal-native workflows.
- **Scale and Performance Constraints**: Hitting 400 errors with large tool sets (`#24246`) and terminal resize performance issues (`#21924`) suggest the architecture needs refinement for power users.
- **Operational Opacity**: "Successful" subagent runs hiding MAX_TURNS interruptions (`#22323`) and history polluted by internal model thoughts (`#27971`) make debugging agent behavior extremely difficult.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — June 23, 2026**

---

### 1. Today’s Highlights
The team shipped two rapid releases today (v1.0.64-2 and v1.0.64-3), packing UX improvements like inline image rendering and HTTP(S) proxy configuration, alongside fixes for Windows scrolling and session resume behavior. However, the community is sounding alarms over major MCP compliance gaps—specifically ignoring server initialization instructions—and opaque AI credit consumption triggered by session restarts. The dominant feature demand remains execution transparency, with a cluster of timer-related tickets gaining significant traction.

---

### 2. Releases
Two minor versions landed today, reflecting high iteration cadence on terminal UX and enterprise configuration:

**v1.0.64-3**
- **Added:** Custom HTTP(S) proxy setting via user config.
- **Fixed:** Session resumption by name when names contain spaces. Hides unsupported slash commands in remote-hosted sessions.

**v1.0.64-2**
- **Added:** Setting to hide the conversation scrollbar. Inline image rendering in the terminal. Argument-hint frontmatter support for skills. OpenTelemetry tagging for compacted chat spans now carries `gen_ai.conversation.compacted=true`.

---

### 3. Hot Issues

1. **[#1632] Support subfolders for skills** (👍20)
   The highest-voted open feature request. Users with 10+ custom skills are forced into a flat folder structure and want hierarchical organization.
   [Issue #1632](https://github.com/github/copilot-cli/issues/1632)

2. **[#3596] Error loading model list: Not authenticated** (👍11)
   Resuming a specific session drops auth state for the `/model` command. New sessions work fine, making this a sharp pain point for session-heavy workflows.
   [Issue #3596](https://github.com/github/copilot-cli/issues/3596)

3. **[#1579] Copilot CLI ignores MCP server “instructions”** (👍3)
   MCP servers return initialization instructions to guide the LLM, but the CLI discards them entirely. A root-cause issue for many downstream tool misbehaviors.
   [Issue #1579](https://github.com/github/copilot-cli/issues/1579)

4. **[#3886] Restarting copilot uses AI credits** (New)
   `/restart` and `/resume` appear to burn a fixed ~174 credits, drawing sharp user concern about unintentional consumption without productive work.
   [Issue #3886](https://github.com/github/copilot-cli/issues/3886)

5. **[#3888] Expose extended thinking independent of reasoning effort** (New)
   Power users of Anthropic models want first-class control over extended thinking instead of having it coupled to the effort slider.
   [Issue #3888](https://github.com/github/copilot-cli/issues/3888)

6. **[#1944] Windows: Mouse wheel captured by input box** (Closed)
   A painful regression that blocked conversation history scrolling on Windows. Resolved in the v1.0.64 line, but highlighted fragility in terminal input interception.
   [Issue #1944](https://github.com/github/copilot-cli/issues/1944)

7. **[#3885] Long text not scrolling inside the input** (New)
   Overflow text in the prompt textarea can’t be scrolled with the mouse. The scroll event leaks to the outer chat view, making multi-line editing difficult.
   [Issue #3885](https://github.com/github/copilot-cli/issues/3885)

8. **[#3884] No documentation for enterprise policy enforcement for local sandbox** (New)
   Enterprises cannot deploy the local sandbox under compliance policies because Intune/MDM integration docs are missing. An active adoption blocker.
   [Issue #3884](https://github.com/github/copilot-cli/issues/3884)

9. **[#3278] Display per-response elapsed time** (👍1)
   Part of a cluster of three timer tickets (#3111, #3055, #3278). Users consistently request visibility into how long the agent has been thinking or running shell commands, especially in autopilot mode.
   [Issue #3278](https://github.com/github/copilot-cli/issues/3278)

10. **[#3883] i18n support for top 10 most-spoken languages** (New, 👍1)
    A proposal to localize menus, prompts, errors, and help text. Reflects broadening global adoption and accessibility needs.
    [Issue #3883](https://github.com/github/copilot-cli/issues/3883)

---

### 4. Key PR Progress
**There were no pull requests updated in the last 24 hours.** Development activity over this window has been concentrated exclusively on point releases (v1.0.64-2/3) and triaging the large influx of new issues. Community contributions are currently dormant.

---

### 5. Feature Request Trends

- **Timers & Execution Observability**  
  A persistent cluster of tickets (#3278, #3055, #3111) asking for thinking-time and shell-execution timers. Users want to know how long the agent has been working.

- **MCP Ecosystem Maturation**  
  Requests are pushing beyond basic connectivity: ignored lifecycle instructions (#1579), registry variable interpolation (#3887), and inter-process sharing with VS Code agent windows (#3638) are all flagged as missing.

- **Skills Organization**  
  Users are building enough custom skills that the flat folder structure is becoming a bottleneck. Hierarchical subfolder support (#1632) is the most-upvoted open feature.

- **Localization**  
  i18n support (#3883) suggests the user base is expanding beyond English-speaking markets.

- **Advanced Model Controls**  
  Decoupling extended thinking from reasoning effort (#3888) signals a sophisticated user base wanting fine-grained access to model-specific capabilities.

---

### 6. Developer Pain Points

- **Session State Fragility**  
  Auth loss on resume (#3596) combined with surprise credit billing on restart (#3886) creates a high-tension user experience. Session lifecycle is currently the top reliability pain point.

- **MCP Spec Compliance Gaps**  
  The CLI’s MCP integration lags behind the spec. Ignoring server initialization instructions (#1579) significantly degrades the value of third-party MCP tools and erodes trust in the feature.

- **Terminal UX Regressions**  
  The mouse wheel leak (#1944, now fixed) and the textarea scroll bug (#3885) are low-level friction points that break flow state during prompt editing.

- **Enterprise Documentation Voids**  
  Missing documentation on local sandbox policy enforcement (#3884) directly blocks enterprise rollouts via Intune or MDM.

- **Verbose Permission Prompts**  
  Despite recent fixes, permission requests for redirected streams and nonexistent paths (#1110, #2693) continue to interrupt workflows, suggesting the sandbox heuristics still need refinement.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-06-23**, generated strictly from the provided GitHub data.

---

## 1. Today’s Highlights

Kimi CLI **v1.48.0** landed with a fix for empty reasoning content in `kosong` and stronger agent-loop detection in `soul`. However, the community’s attention is fixed on a spate of MCP lifecycle regressions—specifically an auto-discovery lock-out bug (#2457) and workspace-path isolation failures in `kimi web` (#2469)—alongside a provider schema violation in `OpenAILegacy` (#2465). A new `Monitor` tool PR (#2471) signals growing demand for streaming stdout from long-running tools.

## 2. Releases

- **Kimi Code CLI v1.48.0 / Kosong v0.54.0**  
  *Release PR: https://github.com/MoonshotAI/kimi-cli/pull/2467*  

  - `fix(kosong)` — Properly round-trips empty reasoning content.
  - `feat(soul)` — Escalates repeated-tool-call reminders through three tiers (r1/r2/r3); force-stops the turn when a dead-end streak is detected.
  - Internal version bumps and chore alignment across the `kosong[contrib]` and `kimi-code` wrapper pins.

## 3. Hot Issues

*Only 4 issues were updated in the last 24 hours. Despite the low volume, the signal is highly critical.*

1. **[#2457] MCP server auto-discovers after deletion, causing unfixable 400 errors**  
   *Author: xavier2sy8827-cmyk | Updated: 2026-06-22*  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2457  
   *Why it matters:* The CLI forcibly reinstates a deleted MCP server without user consent, making the resulting 400 error impossible to resolve through normal UI/CLI commands. Represents a severe loss of configuration agency.

2. **[#2469] `kimi web` launches MCP servers from CLI install directory, breaking workspace-relative tools**  
   *Author: Zehee | Updated: 2026-06-22*  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2469  
   *Why it matters:* Any tool configuration relying on workspace-relative paths silently fails under `kimi web`. Breaks the fundamental tenet of project-local MCP isolation.

3. **[#2468] CLI hangs after detached child-process tool call**  
   *Author: N0zoM1z0 | Updated: 2026-06-22*  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2468  
   *Why it matters:* Testing against local API-compatible mocks is a standard development workflow. The hang makes local provider iteration impractical on Linux.

4. **[#2465] `kosong`: `OpenAILegacy` emits `reasoning_effort: null` for thinking "off"**  
   *Author: 0xbentang | Updated: 2026-06-22*  
   📎 https://github.com/MoonshotAI/kimi-cli/issues/2465  
   *Why it matters:* `null` is not a valid value in the OpenAI chat-completions schema; the field must be absent or a valid enum. This causes rejection by strict API endpoints and fails to actually disable thinking.

## 4. Key PR Progress

*Only 3 PRs were updated in the last 24 hours. All are summarized below.*

1. **[#2471] feat(tools): add Monitor tool for per-line stdout streaming** (Open)  
   *Author: Nitjsefnie*  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2471  
   *Description:* Introduces a streaming counterpart to the existing background tool. Allows real-time, per-line inspection of a long-running tool’s stdout.  
   *Why it matters:* Addresses the common pain point of Opaque tool execution—developers can now observe progress without waiting for task completion.

2. **[#2467] chore(release): bump kimi-cli to 1.48.0 and kosong to 0.54.0** (Merged/Closed)  
   *Author: sailist*  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2467  
   *Description:* Handles the release engineering for v1.48.0, including `version_tag.py` validation and pin syncing.  
   *Why it matters:* Ensures version consistency across the monorepo with automated checks.

3. **[#2466] feat(soul): escalate repeated-tool-call reminders and force-stop on dead-end streak** (Merged/Closed)  
   *Author: jackfish212*  
   📎 https://github.com/MoonshotAI/kimi-cli/pull/2466  
   *Description:* Ports the repeated-tool-call handling from `kimi-code`. After 3+ consecutive identical tool calls, escalating reminders are injected; the turn is force-stopped when a dead-end streak is detected.  
   *Why it matters:* Directly mitigates token waste and UI noise from agentic infinite loops.

## 5. Feature Request Trends

- **MCP Lifecycle Management:** Users strongly demand explicit control over MCP server discovery, deletion persistence, and execution context boundaries (workspace vs. installation directory).
- **Provider Schema Strictness:** Growing pressure for internal providers (primarily `kosong`) to strictly match external API schemas (e.g., OpenAI) to prevent silent compatibility failures.
- **Streaming Tool Observability:** The `Monitor` tool proposal indicates a push for richer operational visibility into long-running background tools.

## 6. Developer Pain Points

- **Loss of Configuration Agency:** MCP servers being forcibly reinstated after deletion (#2457) strips users of local control over their tooling graph.
- **Workspace Isolation Failures:** `kimi web` ignoring the workspace boundary for MCP paths (#2469) breaks standard development isolation patterns.
- **Schema Contract Breaches:** `OpenAILegacy` sending invalid `null` values (#2465) causes opaque rejections at the API layer.
- **Stability Regressions with External Providers:** The hang on child-process tool calls (#2468) blocks the critical local development and testing loop.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the OpenCode community digest for **2026-06-23**, based on the supplied GitHub metrics.

---

## 1. Today’s Highlights

The community is heavily engaged in reviewing the massive **workflow feature stack** (PRs #32390–#32394), which has been dismantled into reviewable pieces by mguttmann and is progressing through the pipeline. Meanwhile, critical **stability and performance regressions** dominate issue discussion, including a server-mode memory leak hitting 26.8GiB (#33213), random CPU lockups (#33399), and a silent plugin loading breakage since v1.17.0 (#33455). Users are also loudly pushing for full **MCP protocol compliance** (#28567) and richer TUI plugin APIs (#18969), signaling a maturing community demanding a more reliable and extensible platform.

---

## 2. Releases

No new versions of OpenCode were published in the last 24 hours.

---

## 3. Hot Issues

| # | Issue | Why It Matters & Community Reaction |
|---|-------|--------------------------------------|
| **#32832** | [MCP tool can no longer return image attachments](https://github.com/anomalyco/opencode/issue/32832) (Closed) | A sharp regression from v1.17.5 that broke all visual MCP tool outputs. 22 comments and a rapid fix were needed, as this blocked a core MCP workflow. |
| **#28567** | [Feature: Full MCP client capabilities](https://github.com/anomalyco/opencode/issue/28567) (Open) | The most upvoted feature request this period (👍24). Users are demanding streaming, roots, and sampling support to match the latest MCP standard. |
| **#4489** | [Ephemeral one‑off sessions for `opencode run`](https://github.com/anomalyco/opencode/issue/4489) (Open) | Strong desire (👍12) for stateless, non-persisted sessions. The author offers to implement the feature if UX is agreed upon, highlighting community contributor energy. |
| **#18969** | [tui.footer.items plugin hook for persistent status](https://github.com/anomalyco/opencode/issue/18969) (Open) | Plugin developers are hitting the ceiling of the TUI API, forced to use disruptive toasts for persistent data (token counts, TPS). A dedicated footer API is a top extensibility request. |
| **#30697** | [Move project folder breaks navigation](https://github.com/anomalyco/opencode/issue/30697) (Open) | A persistent Windows UX bug where the app caches old/deleted project paths. Frustrates users who reorganize directories. |
| **#32694** | [Worker has been terminated crash](https://github.com/anomalyco/opencode/issue/32694) (Closed) | A show-stopping crash (👍4) on the first AI interaction. The high reaction count indicates widespread impact, now addressed in close coordination with the TUI worker fix (#33448). |
| **#33213** | [Server mode massive JS heap/swap accumulation](https://github.com/anomalyco/opencode/issue/33213) (Open) | A production ops nightmare: `opencode serve` grows to 26.8GiB cgroup peak in ~1.5 days. Blocks any serious server-side deployment. |
| **#33399** | [Random 99-100% CPU utilization](https://github.com/anomalyco/opencode/issue/33399) (Open) | Intermittent fan-spinning freezes that make the CLI/TUI completely unresponsive. A top concern for everyday development reliability. |
| **#33455** | [Plugins silently not loaded since v1.17.0](https://github.com/anomalyco/opencode/issue/33455) (Closed) | A trust-eroding regression: all external plugins (npm or local paths) fail to load without a single error or log entry. Burned users relying on custom workflows. |
| **#33447** | [Pre-migration sessions stranded after event-sourcing migration](https://github.com/anomalyco/opencode/issue/33447) (Open) | A data migration headache: sessions created before the event-sourcing migration exist in the DB but are invisible and non-resumable. |

---

## 4. Key PR Progress

| # | PR | Description |
|---|----|-------------|
| **#32394** | [feat(workflow): web app + desktop (4/6)](https://github.com/anomalyco/opencode/pull/32394) | Adds the workflow web dashboard with prompt-input wiring and i18n, split from the oversized monolith #29789. |
| **#32393** | [feat(workflow): TUI workflow dialogs (3/6)](https://github.com/anomalyco/opencode/pull/32393) | Implements the TUI run/approval/question dialogs and `<name>` workflow autocomplete. |
| **#32392** | [feat(workflow): server routes + SDK (2/6)](https://github.com/anomalyco/opencode/pull/32392) | Provides the HTTP API route group and regenerated SDK client/types for the workflow engine. |
| **#32390** | [feat(workflow): engine-core (1/6)](https://github.com/anomalyco/opencode/pull/32390) | Modularized workflow engine core, laying the foundation for multi-step structured interactions. |
| **#33310** | [feat(opencode): run bash commands in background](https://github.com/anomalyco/opencode/pull/33310) | An opt-in `run_in_background: true` flag for the bash tool (Closes #1970). Enables long-running processes without blocking the agent loop. |
| **#32301** | [Nested sub-agent spawning (up to 5 levels)](https://github.com/anomalyco/opencode/pull/32301) | Enables deep agentic hierarchies by allowing sub-agents to spawn their own sub-agents, fixing critical bugs blocking the 2→3 level transition. |
| **#33281** | [Standalone V2 session flow](https://github.com/anomalyco/opencode/pull/33281) | Reworks the CLI session architecture to run an authenticated private server child process, creating sessions through the V2 API. |
| **#33448** | [fix(tui): preserve worker rejection handling](https://github.com/anomalyco/opencode/pull/33448) | Fixes the root cause behind several “Worker has been terminated” crashes by properly logging unhandled rejections instead of letting Bun kill the process. |
| **#30685** | [fix(app): ignore stale project roots when navigating](https://github.com/anomalyco/opencode/pull/30685) | Provides the fix for #30697, ensuring moved/deleted project paths don’t break the desktop app navigation (e.g., OneDrive scenarios). |
| **#28828** | [feat(vcs): add git commit/push/pull/stage/unstage/log API endpoints](https://github.com/anomalyco/opencode/pull/28828) | Lays the backend bedrock for a native Git UI panel, adding six new VCS API routes. |

---

## 5. Feature Request Trends

*   **MCP Standard Compliance:** The highest-signal trend. Users are explicitly requesting full Model Context Protocol support (streaming, roots, sampling) to match competitor offerings (#28567).
*   **TUI Extensibility:** The community wants more than just `toast` notifications. Dedicated plugin hooks for status bars/footers (#18969), middleware for rate limiting (#33459), and service-level plugin contracts are increasingly requested.
*   **Flexible Session Management:** Requests for ephemeral/one-off sessions (#4489), cross-project session pickers (#31932), and session sharing/reverting (#33281) show frustration with the current all-or-nothing persistence model.
*   **Native Git Integration:** The long-standing demand for an in-app Git UI panel (#15886, #26558) is finally seeing backend movement with the VCS API PRs (#28828).
*   **Deeper Agentic Capabilities:** The desire for more autonomous workflows is clear: background tool execution (#33310 / #1970), nested sub-agents (#32301), and structured workflow loops (the entire #29789 stack).

---

## 6. Developer Pain Points

*   **Application Stability & Crashes:** “Worker has been terminated” (#32694), renderer freezes (#32046), and high CPU lockups (#33399) are eroding user trust in recent releases.
*   **Production Reliability Blocks:** The massive server-mode memory leak (#33213) makes running OpenCode as a backend service untenable for teams.
*   **Silent Failures and Data Trust:** The silent plugin loading failure (#33455) and stranded migration sessions (#33447) create a “trust gap” where users are afraid to update or rely on migration paths.
*   **Regression Fatigue:** The v1.17.x cycle (from `1.17.4` to `1.17.9`) has introduced multiple regressions (MCP images, tool timing #32574, plugin loading), making developers hesitant to upgrade for new features.
*   **Cross-Platform UX Friction:** Issues like stale Windows project paths (#30697) and the GNU `screen` clipboard incompatibility (#28590) highlight lingering platform-specific rough edges.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-23

### 1. Today’s Highlights
The Pi ecosystem landed **v0.79.10**, enriching compaction events with explicit reason and retry metadata, a direct community-driven fix for a long-standing blind spot in session management. Concurrently, the community rallied around **stream reliability** (OpenAI Codex hangs, agent loop wedging) and **provider configuration UX** (auth modes, model aliases, dynamic model lists), signaling a maturing project where deep architectural debt is actively being repaid alongside user-facing polish.

---

### 2. Releases

**v0.79.10** — [earendil-works/pi Releases](https://github.com/earendil-works/pi/releases/tag/v0.79.10)
- **Feature:** Extension compaction event context.
- `session_before_compact` and `session_compact` now carry `reason` (`"manual" | "threshold" | "overflow"`) and `willRetry`.
- Extensions can finally distinguish explicit `/compact` commands from automatic threshold triggers and overflow recovery flows, unlocking smarter context management logic in third-party extensions.
- Closes [#5217](https://github.com/earendil-works/pi/issues/5217) and builds on work from [#5962](https://github.com/earendil-works/pi/pull/5962) / [#5941](https://github.com/earendil-works/pi/pull/5941).

---

### 3. Hot Issues

1. **[#4945 — OpenAI Codex Connection Reliability](https://github.com/earendil-works/pi/issues/4945)**  
   *64 comments | 30 👍*  
   **Why it matters:** The top-voted open issue. `gpt-5.5` sessions silently freeze on "Working..." with no error or stream output. The only recovery is an Escape interrupt, leaving users frustrated and distrusting of long-running sessions with OpenAI models.

2. **[#3357 — Official Local LLM Provider](https://github.com/earendil-works/pi/issues/3357)**  
   *27 comments | 36 👍*  
   **Why it matters:** Highest 👍 count. A persistent call for dynamic model-fetching from `{baseUrl}/models` for ollama/llama.cpp/LM Studio. The community deeply wants a zero-config "point at local host" experience.

3. **[#5653 — Move off Shrinkwrap](https://github.com/earendil-works/pi/issues/5653)**  
   *15 comments*  
   **Why it matters:** A structural blocker for the ecosystem. Duplicate `pi-ai` instances from nested `node_modules` break the global provider registry. Anyone running multiple extensions feels this pain as a silent, hard-to-debug module identity crisis.

4. **[#5916 — Support provider extensions with model aliases](https://github.com/earendil-works/pi/issues/5916)**  
   *11 comments*  
   **Why it matters:** Power users juggling OpenRouter or multi-provider setups have no UI to configure model overrides. Hardcoded `models.json` patches are the only workaround, screaming for a proper provider configuration layer.

5. **[#5571 — `pi -p` hangs on non-TTY pipe](https://github.com/earendil-works/pi/issues/5571)**  
   *10 comments*  
   **Why it matters:** A blocking bug for CI/CD. If stdin is a pipe and the provider has no credentials, Pi hangs for minutes instead of fast-failing. Automation use cases are effectively broken without this fix.

6. **[#5778 — Agent loop hangs on unresponsive streams](https://github.com/earendil-works/pi/issues/5778)**  
   *8 comments*  
   **Why it matters:** Core architecture vulnerability. Dangling promises from dropped streams or unresolved tool `execute()` calls wedge the entire agent loop. A critical reliability target for v0.80+.

7. **[#5291 — Sessions hang on "Working" with Anthropic](https://github.com/earendil-works/pi/issues/5291)**  
   *6 comments | 2 👍*  
   **Why it matters:** Provider-specific deadlock. Anthropic Enterprise subscriptions experiencing concurrent hang events, suggesting timeout handling or OAuth token refresh flow gaps.

8. **[#4748 — TUI keybindings singleton broken by extension imports](https://github.com/earendil-works/pi/issues/4748)**  
   *5 comments | 2 👍*  
   **Why it matters:** A monorepo packaging edge case that frustrates extension authors. The `getKeybindings()` module-level singleton breaks when extensions resolve their own `@earendil-works/pi-tui` copy.

9. **[#5871 — Hardcoded Anthropic OAuth detection](https://github.com/earendil-works/pi/issues/5871)**  
   *4 comments*  
   **Why it matters:** The fragile `sk-ant-oat` substring check blocks enterprise auth flows. The community wants explicit `authMode` flags, which PR [#5977](https://github.com/earendil-works/pi/pull/5977) has now begun to deliver.

10. **[#5978 — Plain URLs lose clickability after TUI wrapping](https://github.com/earendil-works/pi/issues/5978)**  
    *3 comments*  
    **Why it matters:** Small surface, big UX impact. OAuth callback (e.g., MCP auth-flow) URLs break on soft-wrapping in the TUI, making authenticated flows a gamble. PR [#5981](https://github.com/earendil-works/pi/pull/5981) provides a direct fix with OSC 8 linking.

---

### 4. Key PR Progress

1. **[#5526 — Require terminal events for OpenAI Response streams](https://github.com/earendil-works/pi/pull/5526)** [OPEN]  
   Targets the root cause of borked context counters and random halts by enforcing RFC-compliant termination signals on OpenAI streams.

2. **[#5987 — Fix `--session` resolution by agent name](https://github.com/earendil-works/pi/pull/5987)** [CLOSED]  
   Bridges the pi-agent-identity daemon with core routing, allowing user-friendly agent names (e.g., `lucid-gecko-24`) instead of raw file paths for session targeting.

3. **[#5859 — Send OpenAI Responses prompts as `instructions`](https://github.com/earendil-works/pi/pull/5859)** [CLOSED]  
   Correctly maps `context.systemPrompt` to the top-level `instructions` field of the Responses API, aligning Pi with OpenAI spec and fixing system message injection.

4. **[#5985 — Add Merge Gateway provider](https://github.com/earendil-works/pi/pull/5985)** [CLOSED]  
   Single-key access to 40+ models via Merge Gateway. Mirrors the existing OpenRouter pattern, drastically lowering the barrier for model variety.

5. **[#5981 — Linkify plain URLs in Text output](https://github.com/earendil-works/pi/pull/5981)** [CLOSED]  
   Immediate fix for [#5978](https://github.com/earendil-works/pi/issues/5978). Adds OSC 8 hyperlink support with smart avoidance of double-wrapping existing links.

6. **[#5977 — Explicit Anthropic `authMode` overrides](https://github.com/earendil-works/pi/pull/5977)** [CLOSED]  
   Introduces a configurable `authMode` flag, replacing the brittle `sk-ant-oat` substring check. A model-level compatibility setting that future-proofs provider config.

7. **[#5262 — Add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262)** [OPEN]  
   Builds a thin `AnthropicVertex` adapter targeting GCP customers. Reuses the entire Anthropic streaming path, minimizing maintenance surface.

8. **[#5970 — DeepSeek auto-router extension](https://github.com/earendil-works/pi/pull/5970)** [CLOSED]  
   A clever community extension that inspects prompt complexity to route between DeepSeek V4 Flash (simple) and Pro (complex), claiming 60–70% API cost reduction.

9. **[#5962 — Compaction reason and `willRetry` events](https://github.com/earendil-works/pi/pull/5962)** [CLOSED]  
   Core of the v0.79.10 release. Exposes `reason` / `willRetry` on `session_before_compact` / `session_compact`, matching the existing RPC protocol.

10. **[#5963 — Reject malformed final tool call arguments](https://github.com/earendil-works/pi/pull/5963)** [CLOSED]  
    Validates final streamed tool-call JSON in the shared AI path. Converts silent data corruption into a clean `stopReason: "error"` state, protecting downstream extensions.

---

### 5. Feature Request Trends

**1. Richer Extension API surface**  
A clear consensus: extensions need lifecycle control. Repeated requests for `navigateTree()` on `ExtensionContext` ([#5932](https://github.com/earendil-works/pi/issues/5932)), session replacement APIs ([#5952](https://github.com/earendil-works/pi/issues/5952)), programmatic session switching ([#5912](https://github.com/earendil-works/pi/issues/5912)), and RPC access to session entries/tree ([#5810](https://github.com/earendil-works/pi/issues/5810)) signal a community ready to build on top of Pi, not just inside it.

**2. Provider Flexibility & Configuration**  
Users are tired of hardcoding provider logic. Feature requests center on:
- **Dynamic model discovery** (`{baseUrl}/models`, [#3357](https://github.com/earendil-works/pi/issues/3357))
- **Explicit auth modes** ([#5871](https://github.com/earendil-works/pi/issues/5871))
- **Unified provider/model strings** (`--model provider/model`, [#5972](https://github.com/earendil-works/pi/issues/5972))
- **New provider support** (Merge Gateway, Neuralwatt, Vertex, [#5914](https://github.com/earendil-works/pi/issues/5914), [#5262](https://github.com/earendil-works/pi/pull/5262), [#5985](https://github.com/earendil-works/pi/pull/5985))

**3. Self-hosted & local-first**  
Local LLM integration ([#3357](https://github.com/earendil-works/pi/issues/3357)) still dominates raw 👍, and the fast uptake of tools like the DeepSeek auto-router suggests the community actively seeks cost-optimized, user-controlled infrastructure.

---

### 6. Developer Pain Points

**1. "Working..." Hang Syndrome**  
The single most reported class of bugs. Issues [#4945](https://github.com/earendil-works/pi/issues/4945), [#5291](https://github.com/earendil-works/pi/issues/5291), [#5571](https://github.com/earendil-works/pi/issues/5571), and [#5778](https://github.com/earendil-works/pi/issues/5778) all describe variations of the same symptom: the agent enters a non-responsive state with "Working..." and no escape except manual interruption. Stream drops, unclosed iterators, and lingering promises are the suspected culprits, and this erodes confidence for both interactive and automated use.

**2. Module Duplication / Packaging Fractures**  
The monorepo transition has surfaced painful packaging bugs. Duplicate `pi-ai` and `pi-tui` instances ([#5653](https://github.com/earendil-works/pi/issues/5653), [#4748](https://github.com/earendil-works/pi/issues/4748)) break global state and keybindings, forcing developers to debug problems that feel wholly infrastructure-caused rather than logic-caused.

**3. Silent Data Corruption / Missing Errors**  
Errors being swallowed ([#2188](https://github.com/earendil-works/pi/issues/2188)), Promises not returned ([#5751](https://github.com/earendil-works/pi/issues/5751)), or model overrides occurring silently ([#5976](https://github.com/earendil-works/pi/issues/5976))—developers are flagging that Pi is too quiet when things go wrong. The "fail fast, fail loud" principle is a strongly requested design goal going forward.

**4. CI/CD and Automation Immaturity**  
Non-TTY hang bugs ([#5571](https://github.com/earendil-works/pi/issues/5571)), unawaited sendMessage promises ([#5751](https://github.com/earendil-works/pi/issues/5751)), and unresolved tool promises ([#5778](https://github.com/earendil-works/pi/issues/5778)) collectively make Pi difficult to productize as a reliable backend service today, though the community is actively working through these blockers.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-23

## Today's Highlights
The community is navigating a day of deep cleanup and high-impact feature work. Contributor **tt-a1i** filed a sweeping batch of ~20 validation bugs across the CLI, LSP, tools, and core modules, exposing a systemic weakness in numeric input sanitization. Meanwhile, critical issues like the shell tool execution loop (`#5641`) and a stalled release pipeline (`#5686`) are demanding immediate attention from maintainers. On the development front, ambitious PRs for a resizable desktop file preview (`#5730`), MCP server hot-reload (`#5561`), and a Vision Bridge for text-only models (`#5126`) signal strong forward momentum.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (Top 10)

**#5641 — Shell Tool Result Repetition [P2 / OPEN]**  
A deterministic OpenAI-compatible provider can cause Qwen Code to submit the result for a completed shell tool call repeatedly after it has already been returned. A standalone reproducer confirms this against the current npm `@qwen-code/qwen-code` package. This is a core loop reliability blocker.  
[Issue #5641](https://github.com/QwenLM/qwen-code/issues/5641)

**#5634 — Autofix Tier-1 Trust Bypass [P2 / Security / OPEN]**  
The `status/ready-for-agent` label, which can be influenced by untrusted issue text, unlocks a fast-track automation path that skips the human-engagement filter. This is a social engineering vector for the autofix CI pipeline.  
[Issue #5634](https://github.com/QwenLM/qwen-code/issues/5634)

**#5734 — Fork Subagent Permission Gates Silently Denied [P2 / OPEN]**  
Detached fork subagents (`FORK_AGENT`) silently auto-deny tool calls that require user confirmation instead of bubbling them to the parent session's Background UI. Forks are effectively broken for permission-gated workflows.  
[Issue #5734](https://github.com/QwenLM/qwen-code/issues/5734)

**#5611 — web_fetch Cannot Access JSON APIs [P2 / OPEN]**  
The tool only sends `text/*` Accept headers, causing HTTP 415 errors on REST endpoints like the GitHub API. This blocks a large class of useful server-side tool use cases. The community has responded with a targeted fix in PR #5660.  
[Issue #5611](https://github.com/QwenLM/qwen-code/issues/5611)

**#5686 — v0.19.0-preview.0 Release Pipeline Failure [OPEN]**  
The release workflow failed on the `integration_none` job, blocking the delivery of all fixes and features queued for this preview.  
[Issue #5686](https://github.com/QwenLM/qwen-code/issues/5686)

**#5710 — VSCode openFile Accepts Zero/Invalid Line/Col [P2 / CLOSED]**  
The webview `openFile` handler parsed paths like `src/app.ts:0`, subtracting 1 and creating negative `vscode.Position` values. This crashed the VS Code companion view. Closed with a fix.  
[Issue #5710](https://github.com/QwenLM/qwen-code/issues/5710)

**#5713 — Semi-Invisible Cursor in Alacritty [P3 / Linux / OPEN]**  
The cursor is barely visible in the Alacritty terminal emulator on Linux. While lower priority, this affects a highly technical segment of users and degrades the first-run experience.  
[Issue #5713](https://github.com/QwenLM/qwen-code/issues/5713)

**#3877 — OPENCODE_GO_API_KEY in .env Not Respected [OPEN]**  
A long-running configuration friction point. Qwen Code forces authentication selection on startup even when `OPENCODE_GO_API_KEY` is correctly set in `~/.qwen/.env`. High 👍 count signals significant user frustration.  
[Issue #3877](https://github.com/QwenLM/qwen-code/issues/3877)

**#5683 — Subagent Token Counting Way Off [P2 / OPEN]**  
Token consumption for subagents is being over-reported by orders of magnitude (e.g., 29xx k tokens reported when well under limit). This breaks session budgeting and confuses users about model utilization.  
[Issue #5683](https://github.com/QwenLM/qwen-code/issues/5683)

**#5656 — Move Tool-Use Summaries to Loading Indicator [Feature Request / P3 / OPEN]**  
A well-discussed proposal (5 comments) asking for semantic tool labels (e.g., "Fixed NPE in UserService") to be moved out of the conversation history and into the loading indicator to reduce visual noise. This theme is echoed in PR #5661.  
[Issue #5656](https://github.com/QwenLM/qwen-code/issues/5656)

---

## Key PR Progress (Top 10)

**#5730 — Desktop Resizable Side Panel for File Previews [CLOSED]**  
Replaces the fullscreen overlay file viewer with a docked, resizable right panel, keeping the conversation and file tree visible. A significant UX upgrade aligning with modern IDE patterns.  
[PR #5730](https://github.com/QwenLM/qwen-code/pull/5730)

**#5732 — CI: Harden Required Test Check [OPEN]**  
Pins `actions/checkout` to the PR head SHA and cleans up concurrency to fix stalling required `Test` checks that were blocking merges. Core maintainer infrastructure fix.  
[PR #5732](https://github.com/QwenLM/qwen-code/pull/5732)

**#5661 — TUI Unified Tool Output with Semantic Summaries [OPEN]**  
Implements the feature sentiment from #5656 by replacing raw tool outputs with concise, AI-generated summaries (e.g., "Read 3 files, edited 2 files"). Past and progressive tense summaries are supported.  
[PR #5661](https://github.com/QwenLM/qwen-code/pull/5661)

**#5126 — Vision Bridge: Image Transcription for Text-Only Models [OPEN]**  
Automatically forwards referenced images to an image-capable model on the same provider, transcribing them into text for the primary text-only model. Expands model compatibility significantly.  
[PR #5126](https://github.com/QwenLM/qwen-code/pull/5126)

**#5660 — Fix web_fetch JSON Accept Fallback [OPEN]**  
Directly addresses the HTTP 415 bug by appending a low-priority `*/*;q=0.1` to the Accept header, enabling access to JSON REST APIs.  
[PR #5660](https://github.com/QwenLM/qwen-code/pull/5660)

**#5561 — MCP Server Runtime Hot-Reload on Settings Change [OPEN]**  
Implements live connection/disconnection of MCP servers when `mcpServers` in `settings.json` changes. Eliminates the need for full restarts during MCP configuration iteration.  
[PR #5561](https://github.com/QwenLM/qwen-code/pull/5561)

**#5616 — User Confirmation for Auto-Generated Skills [OPEN]**  
Resolves #5263 by requiring user approval before background-agent-generated skills are persisted. Gives users control over their skill library without blocking automation.  
[PR #5616](https://github.com/QwenLM/qwen-code/pull/5616)

**#5657 — Stop Repeated Duplicate Provider Tool Responses [OPEN]**  
Attempts to fix the tool-looping behavior seen in #5641. Injects a synthetic error on the first duplicate and blocks subsequent repeats, preventing infinite loops.  
[PR #5657](https://github.com/QwenLM/qwen-code/pull/5657)

**#5727 — Docs Audit: Vertex AI Auth, Missing Commands [OPEN]**  
High-impact documentation refresh adding missing entries for `vertex-ai` authentication, new CLI commands, and updating stale references across six doc files.  
[PR #5727](https://github.com/QwenLM/qwen-code/pull/5727)

**#5589 — Docs Alignment with Current CLI Behavior [OPEN]**  
A companion clean-up refreshing user and developer docs to match actual MCP management, extension, theme, and Qwen OAuth CLI behavior.  
[PR #5589](https://github.com/QwenLM/qwen-code/pull/5589)

---

## Feature Request Trends

**Smarter, Less Noisy Output**
The community is strongly pushing for AI-summarized tool output that replaces raw dumps. Proposals include moving labels to loading indicators (#5656) and unifying output modes into semantic summaries (PR #5661).

**Provider & MCP Flexibility**
There is a clear demand for custom provider identity decoupling from SDK protocol enums (#5090), easier model management for custom providers (#4814), and dynamic MCP server lifecycle without restarts (PR #5561).

**Agent Transparency & Control**
Users want to review and approve background-agent actions (auto-generated skills, PR #5616) rather than having them silently committed. Permission-gated tool calls in subagents should be visible and actionable, not silently denied (#5734).

**Vision & Cross-Model Compatibility**
The Vision Bridge (PR #5126) addresses a major pain point for users of text-only models, ensuring image references in prompts don't break the agent.

---

## Developer Pain Points

**Systemic Input Validation Gap**
The single largest signal today is the relentless batch of bugs from `tt-a1i`. Fractional values are accepted everywhere—timeouts, retry counts, positions, limits, byte limits, and env configs. This indicates a broad neglect of integer/safe-integer validation in JSON schemas, CLI argument coerce functions, and env-var parsers. It is the top refactoring tax on maintainers.

**Core Tool Loop Brittleness**
The tool execution lifecycle is under stress. Duplicate responses (#5641), silent auto-denials (#5734), repeated responses (#5657), and web tool HTTP failures (#5611) create an unpredictable development experience for anyone building complex autonomous workflows.

**Environment & Configuration Friction**
The unresolved `.env` detection issue (#3877) continues to generate negative sentiment. New users expect standard environment variables to be discovered automatically; the current behavior forces manual interaction on every startup.

**CI/CD Instability**
A failed release pipeline (#5686) and flaky required test checks (#5732) are wasting maintainer cycles. Debugging CI is displacing feature work and delaying delivery of fixes.

**Platform Parity Gaps**
Minor but persistent issues on non-primary platforms (Windows tilde path expansion `#5245`, Alacritty rendering `#5713`) suggest that while the core product on Linux/macOS is advancing rapidly, the ecosystem compatibility layer requires dedicated stewardship.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**DeepSeek TUI Community Digest – 2026-06-23 (CodeWhale v0.8.64+)**

---

### 1. Today's Highlights

Today saw an intense consolidation cycle with 11 pull requests opened by the core team, driving the v0.8.65 provider-route architecture toward stability. The primary focus was fixing multi-provider routing regressions — Together DeepSeek routes, SiliconFlow tool-call parsing, and Alibaba DashScope compatibility — while adding first-class support for Baidu Qianfan and a configured SearXNG backend for agent web search. The community contributed a WeCom bridge and an official sub-agent configuration toggle.

### 2. Releases

- **v0.8.64 (CodeWhale):** This release finalizes the full rebranding from `deepseek-tui` to **CodeWhale** as the canonical project name, CLI command, and npm package. The legacy `deepseek-tui` npm package is deprecated and will receive no further updates. Users on v0.8.x are directed to `docs/REBRAND.md` for migration steps.

---

### 3. Hot Issues

1. **#3405 [Setup: provider/model step with catalog, auth, picker, and live health checks]**
   Identifies provider/model setup as the "highest-friction first-run path." Proposes a full wizard overhaul using the v0.8.65 provider architecture. High community impact due to onboarding friction.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3405)

2. **#3383 [Provider-scoped model candidates for /model, picker, and slash completions]**
   Aims to stop accidental provider switching: "a naked model string should never silently imply a provider switch." Directly drives the TUI fix in PR #3428. Core to the v0.8.65 UX contract.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3383)

3. **#3382 [Hosted provider offering validation regression for Together DeepSeek routes]**
   Documents a live regression where switching to Together errored with *"Model is a DeepSeek model and is not available on Together."* Addressed today by PR #3426. Illustrates how hardcoded model identities break multi-provider setups.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3382)

4. **#3289 [Regression fixture for fanout, Fleet workers, and TUI freeze resilience]**
   Tracks a critical reliability bug: spawning multiple Fleet/sub-agent workers freezes the TUI input, render, and cancel subsystems. Community reporter @bruce6135 flagged this as a blocker for multi-agent workflows.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3289)

5. **#2900 [DSML tool-call streaming regression for SiliconFlow DeepSeek route]**
   Windows-specific bug where DSML tool-call markup is streamed as ordinary text instead of being parsed correctly. Preserved as a regression fixture in PR #3431. Community reporter @zslingy.
   [Link](https://github.com/Hmbown/CodeWhale/issues/2900)

6. **#3357 [Baidu Qianfan custom/first-class provider route fixture]**
   Community request from @CaiWeibo to support the Baidu Qianfan coding plan with tools. Requires custom provider URL, API key, and model name. Resolved today by PR #3425.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3357)

7. **#3320 [Alibaba Bailian API key and provider onboarding fixture]**
   Community report from @maomaochong998 that Alibaba Cloud Bailian API key integration is completely missing, making calls impossible. Addressed today by PR #3424.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3320)

8. **#2989 [Ollama/qwen premature completed-state regression fixture]**
   A local-model reliability issue where stream termination is falsely treated as successful task completion. Highlights the need to distinguish "provider stop" from "true completion." Community reporter @and7ey.
   [Link](https://github.com/Hmbown/CodeWhale/issues/2989)

9. **#3079 [Make web_search reliable with a SearXNG JSON backend, health checks, and visible agent status]**
   Core trust issue: `web_search` is described as unreliable and opaque. The fix (PR #3430) adds a self-hosted SearXNG backend with explicit health checks. High community sentiment for agent transparency.
   [Link](https://github.com/Hmbown/CodeWhale/issues/3079)

10. **#1978 [OpenRouter-compatible base_url fixture for reasoning/cache/custom routing]**
    An enhancement request from May 2026 to officially support OpenRouter gateways. The documentation and config example land today in PR #3423, providing route-level validation.
    [Link](https://github.com/Hmbown/CodeWhale/issues/1978)

---

### 4. Key PR Progress

1. **#3428 [fix(tui): scope model candidates to active provider]**
   Core UX fix: the `/model` picker and slash completions now show only models for the active provider, preventing silent provider switching.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3428)

2. **#3425 [feat(provider): add Qianfan route fixture]**
   Adds Baidu Qianfan as a first-class OpenAI-compatible provider with `QIANFAN_*` env vars and wire mapping. Resolves #3357.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3425)

3. **#3430 [Add configured SearXNG web_search backend]**
   Implements #3079 with a JSON-based SearXNG backend, configurable CA, and health checks. Allows users to point CodeWhale at a trusted self-hosted instance.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3430)

4. **#3426 [fix(tui): accept Together-owned DeepSeek routes]**
   Fixes the offer validation regression in #3382, allowing Together to correctly route `deepseek-ai/DeepSeek-V4-Pro` and Flash models.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3426)

5. **#3431 [Pin SiliconFlow DSML regression fixtures]**
   Preserves the #2900 Windows/SiliconFlow tool-call bug as explicit test fixtures to prevent re-regression.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3431)

6. **#3427 [test(provider): pin SiliconFlow TokenHub route diagnostics]**
   Adds config resolver proofs that SiliconFlow-CN remains first-class and TokenHub gateways work under the generic OpenAI route.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3427)

7. **#3422 [test(tui): cover Codex Responses retry edges]**
   Strengthens the Codex/Responses reliability path (#3019) by adding transient 503 retry test coverage.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3422)

8. **#3423 [docs(provider): document OpenRouter-compatible base URLs]**
   Finalizes #1978 by documenting the `provider = "openrouter"` + `base_url` pattern and adding examples to `config.example.toml`.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3423)

9. **#3432 [Extract shared bridge core helpers]**
   Refactors duplicated logic from Telegram, Feishu, WeCom, and Weixin bridges into a shared `integrations/bridge-core` package.
   [Link](https://github.com/Hmbown/CodeWhale/pull/3432)

10. **#3327 [Add first-class sub-agent toggle] (Community PR by @BovmantH)**
    Adds `/config subagents on|off` as a first-class control with full session persistence and TUI wiring.
    [Link](https://github.com/Hmbown/CodeWhale/pull/3327)

---

### 5. Feature Request Trends

The overwhelming demand signal from the issue tracker is a **provider routing overhaul (v0.8.65)**. The community wants a clean separation of provider identity, model identity, offerings, and wire-protocol routes instead of the current DeepSeek-centric lookup table. This is visible in:

- **Multi-provider universality:** Requests for Baidu Qianfan (#3357), Alibaba Bailian (#3320), Xiaomi MiMo (#2621), SiliconFlow/TokenHub (#2629), and OpenRouter (#1978).
- **Architectural decoupling:** The EPIC issue #2608 ("Separate provider facts, model facts, offerings, and route resolution") is the structural centerpiece of this trend.
- **Better onboarding:** The `/provider` readiness dashboard (#3083) and the provider/model setup wizard (#3405) aim to lower the high barrier to entry for non-DeepSeek users.
- **Agent execution maturity:** The "Fleet" subsystem (#3154, #3167) and WhaleFlow reduce pass (#3230) point to a strong desire for structured multi-agent workflows beyond simple sub-agent spawning.
- **Secret management:** Provider-scoped API keys from external vaults/commands (#3004) reflects a growing need for production security hygiene.

---

### 6. Developer Pain Points

- **Provider routing confusion:** Hardcoded model identities cause frustrating runtime errors (e.g., Together Rejection #3382). The team is explicitly addressing this with the v0.8.65 route architecture.
- **Chinese cloud provider incompatibility:** Multiple reports of broken auth and tool-calling on Alibaba Bailian, Baidu Qianfan, and SiliconFlow. These are being actively resolved this week.
- **Onboarding friction:** The "DeepSeek-first" API key screen is a major barrier for users wanting to use other providers. The lack of a unified setup wizard is the top reported UX pain point (#3405).
- **Sub-agent instability:** TUI freezes and input lag when spawning multiple Fleet workers (#3289) remains a high-severity blocker for heavy users of the sub-agent feature.
- **Rebranding migration tax:** The transition from `deepseek-tui` to `codewhale` (v0.8.64) creates a messy upgrade path requiring manual config migration, documented explicitly in `REBRAND.md`.
- **Tool execution visibility:** `web_search` failures (#3079) embody a broader frustration — agents appear to act but produce no visible output or error state, making the TUI feel unreliable.
- **Local model behavioral quirks:** Ollama models falsely reporting task completion (#2989) undermines trust in local execution paths, especially for agent workflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*