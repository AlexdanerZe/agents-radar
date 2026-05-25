# AI CLI Tools Community Digest 2026-05-25

> Generated: 2026-05-25 09:58 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report
**Date:** 2026-05-25  
**Prepared for:** Technical leadership and developer ecosystem analysis

---

## 1. Ecosystem Overview

The AI CLI tools landscape is undergoing a rapid maturation cycle characterized by intense competition across three vectors: agentic autonomy, platform integration, and cost transparency. Today’s cross-tool data reveals a shared struggle to deliver reliable autonomous execution while maintaining user trust through robust security models and predictable cost structures. The ecosystem is bifurcating between open-source challengers that prioritize provider flexibility and terminal power-user experiences (Pi, OpenCode, CodeWhale) and platform incumbents balancing ecosystem depth with security and reliability regressions (Claude Code, Copilot CLI, OpenAI Codex). An emerging “economic efficiency” wave, catalyzed by DeepSeek’s 75% price reduction, is pressuring proprietary tools to adopt multi-provider architectures or face user migration to more cost-transparent alternatives. Across all tools, the gap between ambitious agentic feature sets and daily-driver reliability remains the single largest friction point.

---

## 2. Activity Comparison (2026-05-24 to 2026-05-25)

| Tool | Hot Issues Tracked | PRs in Digest | Releases (24h) | Primary Activity Character |
|---|---|---|---|---|
| **Claude Code** (Anthropic) | 10 | 6 | 0 | Security/data-loss crisis; plugin ecosystem expansion |
| **OpenAI Codex** | 10 | 10 | 0 | Agent reliability fixes; major TUI feature work (Vim, Review Story) |
| **Gemini CLI** (Google) | 10 | 10 | 0 | Deep agent orchestration bug fixes; configurable routing |
| **GitHub Copilot CLI** | 10 | 0 | 3 (v1.0.53–55-0) | Rendering regression triage; hotfix stabilization cycle |
| **Kimi Code CLI** (MoonshotAI) | 3 | 7 | 0 | ACP protocol compliance; architectural rewrite debate |
| **OpenCode** (anomalyco) | 10 | 10 | 0 | Stability regression (v1.15.10); MCP/MQ hardening |
| **Pi** (earendil-works) | 10 | 10 | 0 | XDG compliance landed; stability/resilience patches |
| **Qwen Code** (QwenLM) | 10 | 10 | 1 (nightly) | Mode B daemon roadmap integration; telemetry/safety work |
| **CodeWhale** (Hmbown) | 10 | 10 | 3 (v0.8.43/44/45 RC) | Rebranding migration; Control Plane release preparation |

---

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities independently, indicating genuine market demand:

### Agent Reliability & Determinism
- **Tools affected:** OpenAI Codex, Gemini CLI, Claude Code, Pi, OpenCode, Copilot CLI
- **Specific needs:**
  - Elimination of non-responsive hangs (Pi #4945, Gemini #21409, OpenCode #29129)
  - Honest agent status reporting instead of false “success” on timeout (Gemini #22323)
  - Interruptible/recoverable agent runs (CodeWhale PR #2118, Claude Code #62168)
  - Deterministic tool execution without deadlocks (Codex #24407, Gemini #25166)

### Multi-Provider & Model Flexibility
- **Tools affected:** Copilot CLI, OpenCode, Pi, CodeWhale, Gemini CLI
- **Specific needs:**
  - Explicit `--model` flags for selecting inference backends (Copilot #2854)
  - Proportional Go/quota adjustments following DeepSeek price cuts (OpenCode #28846, #29151)
  - New provider integrations: DashScope (Pi #4964), Kiro/AWS (OpenCode #20491), Groq/Cerebras (CodeWhale #2087)
  - Configurable routing rules for model-to-task mapping (Gemini #27406)

### Security & Execution Sandboxing
- **Tools affected:** Claude Code, OpenCode, CodeWhale, Qwen Code
- **Specific needs:**
  - Filesystem write restriction enforcement across all tools (Claude Code #52325)
  - Full agent sandboxing as highest-voted feature request (OpenCode #2242, 46 👍)
  - Typed, persistent permission rules for tool operations (CodeWhale #1186)
  - Runaway protection and denial caps for headless/autonomous modes (Qwen Code #4502, #4476)

### Context, Cost & Memory Transparency
- **Tools affected:** Claude Code, OpenAI Codex, Pi, Qwen Code, Gemini CLI
- **Specific needs:**
  - Visible context window usage indicators (Codex #24272 cluster)
  - Per-session token consumption counters (Qwen Code #4479)
  - Reliable session compaction without data loss (Pi #4046, Codex #14425)
  - Subagent prompt cache hit rates (Claude Code #54006)
  - Persistent cost display instead of per-turn resets (CodeWhale #2038)

### Cross-Platform & IDE Parity
- **Tools affected:** Copilot CLI, Gemini CLI, CodeWhale, Claude Code, Qwen Code
- **Specific needs:**
  - Fixes for Linux/Wayland, Windows Terminal, and WSL2-specific rendering issues
  - Mobile session management (Copilot #3498, Codex iOS/Android issues)
  - IDE extension compatibility with modern editor versions (Qwen Code #4488)
  - SSH/remote image paste support (Claude Code #5277)

---

## 4. Differentiation Analysis

### Ecosystem Depth & Extensibility
- **Claude Code** leads with its plugin architecture (`credential-guard` plugin, `.claude/rules` integration), but pays a complexity tax visible in MCP integration friction and plugin auth failures.
- **CodeWhale** and **OpenCode** invest heavily in open extension APIs and skill systems, prioritizing community-driven contributions.

### Agentic Autonomy & Hierarchy
- **Gemini CLI** has the most sophisticated agent hierarchy (generalist, subagents, browser agent) but suffers the highest rate of “stuck agent” reports, exposing the gap between architecture and execution reliability.
- **OpenAI Codex** pushes autonomy features (`/Goal`, `/Review Story`) and TUI power tools (Vim bindings, transcript search), positioning itself as the “terminal-first agentic IDE.”
- **Kimi Code** hesitates at a protocol level (ACP), while its Python-to-TypeScript rewrite debate signals underlying architectural uncertainty.

### Provider Agnosticism & Cost Transparency
- **Pi** and **OpenCode** are the most responsive to provider market shifts, rapidly integrating new backends (DashScope, Kiro) and adjusting quota models for DeepSeek’s price cut. This economic flexibility is a strategic differentiator.
- **Copilot CLI** and **Claude Code** face the strongest “walled garden” accusations from their communities, with explicit demands for Gemini and multi-model support.

### Enterprise Readiness & Safety
- **Qwen Code** and **Claude Code** are the most focused on enterprise patterns: daemon architectures, telemetry instrumentation, headless guardrails, and session management APIs.
- **GitHub Copilot CLI** relies on GitHub platform integration but struggles with shell environment hostility (history truncation, `PS0`/`PROMPT_COMMAND` conflicts).

### Terminal UX Maturity
- **OpenAI Codex** and **CodeWhale** are racing to transform the terminal into a full-featured IDE (independent scroll regions, vim keybindings, model-level diff narratives).
- **Pi** prioritizes output cleanliness and Linux best practices (XDG, markdown rendering, file output collapse).
- **Copilot CLI** demonstrates the risks of this race: rapid TUI innovation has introduced widespread rendering regressions (IME misplacement, scrollbar alignment, output clipping).

---

## 5. Community Momentum & Maturity

| Category | Tools | Characterization |
|---|---|---|
| **Rapidly Iterating / High Momentum** | Qwen Code, CodeWhale, Pi, OpenCode | Open-source projects with high PR velocity, responsive to niche community needs (provider expansion, terminal ergonomics, cost tracking). Safe experimentation platforms. |
| **Managing Scale / Mature, High Scrutiny** | Claude Code, OpenAI Codex, GitHub Copilot CLI | Largest user bases, highest expectations. Regressions are immediately visible and heavily criticized. Innovation is balanced against stability. |
| **Strong Architecture, Reliability Gap** | Gemini CLI | Most ambitious agent architecture (subagents, routing, skills). Most acute reliability issues (hangs, false success, configuration ignored). Bridges gap, it becomes a serious contender. |
| **Strategic Crossroads** | Kimi Code CLI | Lowest observable issue/PR activity. Architectural rewrite proposal reflects deeper product direction uncertainty. |

**Velocity metrics:** OpenCode, Pi, and CodeWhale average 10+ substantive PRs per observed cycle. Copilot CLI shipped 3 releases in 24 hours for hotfix triage. Claude Code and Codex are producing high-quality feature PRs alongside heavy bug-fix loads, indicating engineering teams operating at capacity.

---

## 6. Trend Signals

1. **The Reliability Ceiling is the Bottleneck.** The collective community voice across all nine tools points to agent reliability (hangs, deadlocks, false success reports, config being ignored) as the primary obstacle to daily professional use. *Tool-level insight: Gemini CLI and OpenAI Codex face the steepest trust erosion here; Pi and CodeWhale invest heavily in deterministic error recovery.*

2. **Economic Efficiency Drives Architecture.** DeepSeek’s permanent 75% V4 Pro price cut is the defining external shock this cycle. Tools that facilitate multi-provider routing and cost transparency (Pi, OpenCode) strengthen their competitive position. *Tool-level insight: Copilot CLI and Claude Code face direct pressure to open their model selection layers.*

3. **Memory Management is the New Context Window.** The conversation has shifted from “how large is the context window” to “how efficiently is my session memory managed, and how much does it cost?” Compaction reliability, prompt caching, and token counters are now first-class requirements. *Tool-level insight: Qwen Code’s token counter (#4479) and Claude’s cache TTL issues (#54006) are early indicators of a lasting trend.*

4. **The Terminal is Being Rebuilt as a Full IDE.** OpenAI Codex (Review Story, Vim bindings, transcript search) and CodeWhale (independent scroll regions, Control Plane) are aggressively adding desktop-grade UI capabilities to the terminal. This suggests a strategic belief that the terminal, not the desktop app, is the primary developer surface. *Tool-level insight: Copilot CLI’s rendering regressions demonstrate how quickly UI changes can erode trust in this strategy.*

5. **Security-as-a-Feature is a Dealbreaker.** Agent sandboxing, credential guards, persistent permission rules, and runaway protection are no longer “nice to have.” The Claude Code sandbox bypass (#52325) will be a widely referenced cautionary case. *Tool-level insight: OpenCode’s #2242 (Sandbox the Agent) with 46 votes is the single highest-reaction open issue across all digests.*

6. **Open Source Affords a Trust Advantage.** OpenCode, Pi, and CodeWhale users can fix what bothers them (provider configs, path handling, UI quirks) directly or through fast-cycle community PRs. This creates a resilience that closed-source tools must match with rapid response to community feedback.

---

### Key Takeaway

The AI CLI tool ecosystem is past the “demo or novelty” phase. Developers are integrating these tools deeply into daily workflows and demanding enterprise-grade reliability, cost transparency, and security. The tools that will win the next six months are those that can execute core agentic features *deterministically*, offer genuine provider flexibility, and surface cost/memory economics clearly to the user.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills: Community Highlights Report (Data as of 2026-05-25)

### 1. Top Skills Ranking

**1. [Add document-typography skill (#514)](https://github.com/anthropics/skills/pull/514)** — *Status: Open*
Automatically prevents orphan/widow text, stranded section headers, and numbering alignment issues in generated documents. The most discussed PR in the repository, highlighting a universal frustration with AI document formatting quality. The discussion focuses on the frequency of these errors in Claude’s output and the skill’s broad applicability.

**2. [Add ODT skill (#486)](https://github.com/anthropics/skills/pull/486)** — *Status: Open*
Provides full OpenDocument Format support (.odt, .ods) including creation, template filling, and conversion to HTML. Driven by enterprise users needing LibreOffice/ISO-standard document generation. The high engagement reflects a clear gap in the current skillset for open-source office formats.

**3. [Add testing-patterns skill (#723)](https://github.com/anthropics/skills/pull/723)** — *Status: Open*
Covers the full testing stack from philosophy (Testing Trophy model) through unit, React component, and end-to-end patterns. The broad scope and prescriptive structure have generated sustained discussion around testing standards and what a default testing skill should contain.

**4. [Add AURELION skill suite (#444)](https://github.com/anthropics/skills/pull/444)** — *Status: Open*
A four-skill cognitive framework (kernel, advisor, agent, memory) for structured reasoning and persistent context. The most architecturally ambitious submission in the top rankings, drawing attention for its production memory management patterns.

**5. [Add ServiceNow platform skill (#568)](https://github.com/anthropics/skills/pull/568)** — *Status: Open*
A broad ServiceNow assistant covering ITSM, ITOM, SecOps, ITAM, SPM, and IntegrationHub. Signals strong enterprise demand for Claude Code integration with major IT service management platforms.

**6. [Add skill-quality-analyzer and skill-security-analyzer (#83)](https://github.com/anthropics/skills/pull/83)** — *Status: Open*
Meta-skills that evaluate other skills across structure, documentation, and security dimensions. The timing aligns perfectly with the community’s growing security concerns and desire for skill quality standards.

**7. [Add codebase-inventory-audit skill (#147)](https://github.com/anthropics/skills/pull/147)** — *Status: Open*
A 10-step workflow for identifying orphaned code, documentation gaps, and infrastructure bloat. The systematic approach to codebase hygiene has resonated strongly with teams managing legacy codebases.

---

### 2. Community Demand Trends

**Document Fidelity & Standards Compliance**
Issues and PRs consistently call for output that matches enterprise document standards. The community directly links Claude’s value to its ability to produce production-ready, properly formatted documents (ODT, typography, tracked changes), rather than disposable drafts.

**Security & Trust Boundary Management**
Issue [#492](https://github.com/anthropics/skills/issues/492) (trust boundary abuse under the anthropic/ namespace) and Issue [#412](https://github.com/anthropics/skills/issues/412) (agent governance proposals) indicate sharpening awareness of supply-chain risks. The community is asking for permission models, security analyzers, and audit trails, not just new features.

**Quality Assurance Infrastructure**
There is a clear push to professionalize the skill development lifecycle itself. Issue [#556](https://github.com/anthropics/skills/issues/556) (run_eval.py trigger failures) and Issue [#202](https://github.com/anthropics/skills/issues/202) (skill-creator best practices) reveal that contributors want reliable tooling to test and validate skills before distribution.

**Cross-Platform Portability & Sharing**
Issue [#228](https://github.com/anthropics/skills/issues/228) (org-wide skill sharing), Issue [#189](https://github.com/anthropics/skills/issues/189) / [#1087](https://github.com/anthropics/skills/issues/1087) (duplicate plugin installations), and Issue [#29](https://github.com/anthropics/skills/issues/29) (Bedrock support) collectively show a community straining against manual distribution pipelines and seeking a mature plugin registry.

**Automation & Workflow Engineering**
PRs for n8n, SAP predictive models, and memory systems reveal demand for Claude acting as an automation orchestrator, not just an inline assistant.

---

### 3. High-Potential Pending Skills

These open PRs maintain active discussion and are likely to land soon:

- **[document-typography (#514)](https://github.com/anthropics/skills/pull/514)** — The most-discussed skill overall. Addresses the single most visible pain point in AI document generation. Likely to merge once orphan/widow edge cases are fully specified.
- **[ODT skill (#486)](https://github.com/anthropics/skills/pull/486)** — Strong enterprise push. The OpenDocument gap is widely acknowledged; discussion centers on template handling rather than core functionality.
- **[testing-patterns (#723)](https://github.com/anthropics/skills/pull/723)** — Broad consensus on the need, with refinement ongoing around React-specific vs. general patterns.
- **[skill-quality-analyzer + skill-security-analyzer (#83)](https://github.com/anthropics/skills/pull/83)** — Directly addresses the security and quality concerns raised in Issues. The meta-skill pattern itself is novel and likely to influence future contributions.
- **[shodh-memory (#154)](https://github.com/anthropics/skills/pull/154)** — Persistent memory across conversations. Discussion is active around memory structuring and proactive context retrieval.

---

### 4. Skills Ecosystem Insight

**The community’s most concentrated demand is elevating Claude Code from a conversational copilot into a production-grade enterprise forge**, requiring rigorous document fidelity (typography, ODT, tracked changes), layered testing infrastructure, and secure, governed platform integrations (ServiceNow, n8n, SAP) that match organizational deployment expectations.

---

# Claude Code Community Digest
**Date:** 2026-05-25  
**Source:** `github.com/anthropics/claude-code`

---

## 1. Today’s Highlights
Activity today is dominated by critical security and reliability reports. A sandbox bypass where the Write tool ignores filesystem restrictions enforced by the Bash tool ([#52325](https://github.com/anthropics/claude-code/issues/52325)) was raised alongside a data-loss regression in session cleanup logic ([#41458](https://github.com/anthropics/claude-code/issues/41458)). Multiple users report a coordinated spike in API socket disconnects and “Elevated errors” across both Claude Code and Claude Desktop, suggesting a backend incident cascade on 2026-05-24 ([#62146](https://github.com/anthropics/claude-code/issues/62146)). On the feature front, a community PR for a `credential-guard` plugin ([#62099](https://github.com/anthropics/claude-code/pull/62099)) and a CLI–Desktop sync proposal ([#61969](https://github.com/anthropics/claude-code/pull/61969)) highlight strong ecosystem-building momentum.

---

## 2. Releases
No new releases in the last 24 hours.

---

## 3. Hot Issues

1. **[#14200 — Add rules support to Plugins](https://github.com/anthropics/claude-code/issues/14200)**  
   The most upvoted open feature request (76 👍), asking for `.claude/rules` integration within plugins. Community sentiment is strongly in favor of composable, shareable rule sets.

2. **[#37323 — Support `/btw` command in VS Code extension](https://github.com/anthropics/claude-code/issues/37323)**  
   A parity gap with 62 👍. Users want the lightweight side-question flow available in the terminal CLI ported to the IDE extension.

3. **[#49268 — Thinking summaries missing on Opus 4.7](https://github.com/anthropics/claude-code/issues/49268)**  
   A highly active bug (57 👍, 34 comments). The harness fails to set `display: "summarized"`, causing extended thinking summaries not to render after the model switch.

4. **[#18009 — Slack plugin fails to authenticate](https://github.com/anthropics/claude-code/issues/18009)**  
   A core integration blocking users, with 48 👍 and 18 comments. The “does not support dynamic client registration” error suggests a protocol mismatch.

5. **[#5277 — Image paste in SSH/sftp](https://github.com/anthropics/claude-code/issues/5277)**  
   A 10-month-old request (30 👍) that continues to get traction. Users running Claude on remote servers want inline image context without needing desktop app integrations.

6. **[#28729 — Link source control repo for organization skills](https://github.com/anthropics/claude-code/issues/28729)**  
   Enterprise demand for version-controlled, git-backed skills distribution. 30 👍.

7. **[#41458 — `cleanupPeriodDays: 99999` ignored, 490 sessions silently deleted](https://github.com/anthropics/claude-code/issues/41458)**  
   Tagged `data-loss` and `regression`. A misconfiguration in the cleanup logic overrode explicit user settings, destroying long session histories.

8. **[#52325 — Write tool bypasses sandbox filesystem write restrictions](https://github.com/anthropics/claude-code/issues/52325)**  
   A high-severity security gap. The Write tool can write outside the sandbox directory, while the Bash tool correctly enforces the restriction.

9. **[#54006 — Agent team subagents do not honor 1-hour prompt cache TTL](https://github.com/anthropics/claude-code/issues/54006)**  
   Cost-critical bug for agent teams: the root session shows 100% cache hits, but every spawned agent session gets 0%, dramatically increasing API costs.

10. **[#62146 / #62181 — Elevated error rates and socket disconnects](https://github.com/anthropics/claude-code/issues/62146)**  
    Multiple users report `ECONNREFUSED` errors, a spike on 2026-05-24, and a cross-client cascade affecting both Claude Code and Claude Desktop simultaneously.

---

## 4. Key PR Progress

1. **[#62099 — Add credential-guard plugin](https://github.com/anthropics/claude-code/pull/62099)**  
   New plugin using `PreToolUse` hooks to scan 20+ credential patterns in `Write`, `Edit`, `MultiEdit`, and `Bash` tool calls, preventing hardcoded secrets from being committed.

2. **[#61969 — CLI–Desktop conversation sync (proposal)](https://github.com/anthropics/claude-code/pull/61969)**  
   Opens the door for browsing terminal CLI sessions in the Claude desktop UI, unifying the session review experience across surfaces.

3. **[#62023 — Fix word-boundary @claude trigger in workflows](https://github.com/anthropics/claude-code/pull/62023)**  
   Closed fix. Prevents false positives when GitHub workflows match `@claude` in plugin marketplace names like `@claude-plugins-official`.

4. **[#61968 — Troubleshooting for AskUserQuestion rewind checkpoint gap](https://github.com/anthropics/claude-code/pull/61968)**  
   Documents the root cause: rewind is keyed to user-message boundaries, but `AskUserQuestion` answers arrive as `tool_result` blocks inside assistant turns. Proposes an echo-back workaround.

5. **[#61478 / #58673](https://github.com/anthropics/claude-code/pull/61478)**  
   Low-quality or spam submissions. No substantive changes to report.

---

## 5. Feature Request Trends

- **Plugin & Rules Convergence** — The highest-voted open request ([#14200](https://github.com/anthropics/claude-code/issues/14200)) alongside a new request for per-project `enabledPlugins` in `.claude/settings.json` ([#62174](https://github.com/anthropics/claude-code/issues/62174)) signals strong demand for granular, composable plugin configuration.

- **Extended Context Presets** — Users want a dedicated `opusplan[1m]` preset to unlock Sonnet 4.6’s 1M context window for the non-planning phase ([#53987](https://github.com/anthropics/claude-code/issues/53987)).

- **Remote Development** — Image paste support in SSH/sftp sessions ([#5277](https://github.com/anthropics/claude-code/issues/5277)) remains the most enduring request for developers working on remote or headless machines.

- **Version-Controlled Skills** — Linking source control repositories as the source for organization skills ([#28729](https://github.com/anthropics/claude-code/issues/28729)) would enable PR-driven skill updates and approval workflows.

- **IDE Feature Parity** — The `/btw` command gap ([#37323](https://github.com/anthropics/claude-code/issues/37323)) and the ability to hide inline diffs ([#37951](https://github.com/anthropics/claude-code/issues/37951)) reflect a community pushing for a consistent experience across CLI and VS Code.

---

## 6. Developer Pain Points

- **Sandbox Security Model Gaps** — The Write tool completely bypassing sandbox filesystem restrictions ([#52325](https://github.com/anthropics/claude-code/issues/52325)) and the `autoAllowBashIfSandboxed` feature flagging on safe `key=value` shell arguments ([#58214](https://github.com/anthropics/claude-code/issues/58214)) erode trust in the sandbox boundary.

- **Agent Autonomy & Communication** — Multiple reports of agents proceeding with multi-step changes before the user has responded to a clarifying question ([#62168](https://github.com/anthropics/claude-code/issues/62168)). Intermittently missing `Co-Authored-By` trailer in git commits ([#58033](https://github.com/anthropics/claude-code/issues/58033)) adds collaboration friction.

- **Windows & WSL Reliability** — Distinct pain points for the Windows platform persist: flaky auth flows that revert instantly ([#44585](https://github.com/anthropics/claude-code/issues/44585)), sandbox environment leaks breaking JVM Gradle and MCP servers ([#44857](https://github.com/anthropics/claude-code/issues/44857)), and the VS Code extension occasionally rendering a blank page ([#61140](https://github.com/anthropics/claude-code/issues/61140)).

- **MCP Integration Friction** — The Slack plugin is fully broken ([#18009](https://github.com/anthropics/claude-code/issues/18009)), hosted Google MCP endpoints return 404 ([#55474](https://github.com/anthropics/claude-code/issues/55474)), MCP timeouts beyond 60s are ignored ([#16837](https://github.com/anthropics/claude-code/issues/16837)), and validation feedback for MCP settings is absent ([#62176](https://github.com/anthropics/claude-code/issues/62176)).

- **Cost Unpredictability** — Subagents missing the prompt cache entirely ([#54006](https://github.com/anthropics/claude-code/issues/54006)) and the desktop app falsely reporting “Usage Limit Reached” ([#61673](https://github.com/anthropics/claude-code/issues/61673)) create unnecessary billing anxiety and friction for heavy users.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

Here is the OpenAI Codex community digest for 2026-05-25.

---

## OpenAI Codex Community Digest — 2026-05-25

## 1. Today's Highlights
Today’s digest surfaces widespread user backlash over a missing context window usage indicator across platforms following recent app updates, along with critical work landing to harden agent stability and improve the TUI editing experience. Performance regressions in GPT-5.5 Fast are drawing significant attention, while the team is proactively shipping transcript search, Vim parity, and an ambitious new Review Story feature for inline code review.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Hot Issues
1. **[Issue #20161](https://github.com/openai/codex/issues/20161) (CLOSED) – Phone number verification failure.** Highly engaged issue (161 comments, 102 👍) detailing an auth flow breakage when moving between devices; users are prompted unexpectedly for a phone number despite none being on file.
2. **[Issue #23195](https://github.com/openai/codex/issues/23195) (OPEN) – macOS flags Codex Desktop as malware.** A sudden in-session macOS security warning is interrupting business and Pro users, causing alarm and requiring manual overrides to continue working.
3. **[Issue #24422](https://github.com/openai/codex/issues/24422) (OPEN) – GPT-5.5 Fast performance regression.** Users report the Fast model has slowed to match Standard tier speeds, with simple tasks escalating to 10–20 minute completion times.
4. **[Issue #24272](https://github.com/openai/codex/issues/24272) (OPEN) – Context window usage indicator missing.** A high-visibility regression where the context bar disappeared from the composer (closely related to #24044, #24015, #24071, #24029, #24066 across Windows and macOS).
5. **[Issue #21076](https://github.com/openai/codex/issues/21076) (OPEN) – Desktop conversation history hidden/stale.** Recent threads are not surfaced despite existing in the local SQLite database, a serious data visibility bug for active developers.
6. **[Issue #20805](https://github.com/openai/codex/issues/20805) (OPEN) – Image-heavy chats cause reconnection loops.** Threads with numerous attached images trigger repeated reconnections and severe slowdown, blocking visual and design workflows.
7. **[Issue #24269](https://github.com/openai/codex/issues/24269) (OPEN) – /Goal command universally failing.** The new autonomous goal feature consistently fails, preventing users from delegating complex multi-step tasks to Codex.
8. **[Issue #14425](https://github.com/openai/codex/issues/14425) (OPEN) – Compaction hangs indefinitely below 16%.** A long-standing blocker that freezes sessions entirely, blocking any further progress in long-running threads.
9. **[Issue #13891](https://github.com/openai/codex/issues/13891) (OPEN) – MCP login OAuth resource indicator missing.** A critical security gap for MCP server integration where the protected resource indicator is omitted from the authorize request, resulting in incorrect token audiences.
10. **[Issue #24407](https://github.com/openai/codex/issues/24407) (OPEN) – `apply_patch` tool non-deterministic deadlock.** The `file_change` tool deadlocks on file mutations across CLI versions 0.125 to 0.133, preventing `turn.completed` events from firing and breaking automated execution pipelines.

## 4. Key PR Progress
1. **[PR #23585](https://github.com/openai/codex/pull/23585) – Auto-compaction death-loop guard.** Prevents infinite cycles where successful compaction leaves the context above the auto-compact trigger, a critical agent-stability fix for autonomous turns.
2. **[PR #24169](https://github.com/openai/codex/pull/24169) / PR #23829 – Sanitize invalid image history.** Replaces poisoned image payloads (malformed base64, download failures) with model-visible feedback instead of rolling back turns or breaking thread resume.
3. **[PR #24420](https://github.com/openai/codex/pull/24420) – Show remote connection details in `/status`.** Exposes transport type and server version in the TUI status command to improve debugging for remote and daemon sessions.
4. **[PR #24317](https://github.com/openai/codex/pull/24317) – Respect hook trust bypass on TUI startup.** Fixes a regression where `--dangerously-bypass-hook-trust` was ignored in the TUI, breaking automated and headless workflows.
5. **[PR #23539](https://github.com/openai/codex/pull/23539) – Transcript search for TUI.** Adds Ctrl+F search to the transcript overlay, dramatically improving navigation through long sessions.
6. **[PR #24382](https://github.com/openai/codex/pull/24382) – Vim text object bindings (TUI).** Implements `ciw`, `daw`, `di(`, and bracket variants in the composer, delivering long-awaited Vim parity for power users.
7. **[PR #24350](https://github.com/openai/codex/pull/24350) – Review Story API (TUI).** A new feature generating model-authored, ordered narratives for diffs, designed to guide reviewers through coherent logical steps rather than flat alphabetical changes.
8. **[PR #24368](https://github.com/openai/codex/pull/24368) – Compaction metadata in turn headers.** Adds `request_kind` and `window_id` observability to turn headers, enabling better debugging of compaction behavior and context management.
9. **[PR #24305](https://github.com/openai/codex/pull/24305) – Doctor thread inventory audit.** Adds a `codex doctor` command to detect missing desktop sessions by comparing the SQLite state DB against the on-disk JSONL rollout files.
10. **[PR #24356](https://github.com/openai/codex/pull/24356) – Nudge users toward auto-compaction.** Addresses backlash over hidden context controls by introducing gentle reminders that the auto-compaction system is working as intended.

## 5. Feature Request Trends
- **Unified Session Management:** There is strong demand for visibility across Codex surfaces. [Issue #24197](https://github.com/openai/codex/issues/24197) specifically requests showing local CLI/TUI sessions inside the Desktop app, reflecting a need for a single pane of glass regardless of access method.
- **MCP & Extension Parity:** [Issue #2901](https://github.com/openai/codex/issues/2901) (64 👍) requests that the VSCode extension support the same MCP management system used by GitHub Copilot, signaling a strong desire for a standardized protocol interface across all environments.
- **Terminal as Full IDE:** The volume of TUI-focused PRs (transcript search, Vim text objects, Review Story) indicates the team is prioritizing the terminal as a primary editing and review environment, aligning with power-user expectations for a first-class terminal experience.

## 6. Developer Pain Points
- **Context Management Opacity:** The disappearance of the context usage indicator across platforms (Issues #24272, #24044, et al.) is the single most acute pain point today. Developers feel blind entering long threads without knowledge of their context buffer state.
- **Agent Reliability:** The combination of failing `/Goal` commands, `apply_patch` deadlocks (#24407), and compaction hangs (#14425) is severely undermining trust in autonomous agentic workflows.
- **Model Performance Instability:** The regression of GPT-5.5 Fast (#24422) highlights how dependent daily workflow cadence is on consistent model speed, and any degradation immediately breaks developer trust in fast iteration.
- **Cross-Platform Inconsistency:** A persistent pattern of platform-specific bugs (Windows UI freezes #24251, Android remote history #22762, iOS remote flakiness #24424, macOS malware warnings #23195) suggests macOS remains the primary development target, with other environments frequently receiving delayed attention.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

Here is the **Gemini CLI Community Digest** for **2026-05-25**, based on the latest GitHub activity across issues and pull requests.

---

## 1. Today's Highlights
While no new releases shipped in the last 24 hours, the project saw high-impact activity around agent stability and configurability. Critical fixes landed for session resume crashes (`EBADF` handling) and multi-line paste support on Windows, while the community pushed hard for configurable routing and tool-call timeouts. A long tail of Auto Memory reliability bugs and workspace pollution issues dominated the issue tracker, signaling strong demand for more predictable agent behavior.

---

## 2. Releases
No new releases were published in the last 24 hours.

---

## 3. Hot Issues (Top 10)

1.  **[#21409 – Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** – P1, 8 👍. The most upvoted open issue. The generalist agent hangs indefinitely on simple tasks (e.g., folder creation). Users note that explicitly disabling sub-agents avoids the hang, pointing to a deep agent orchestration bug.
2.  **[#25166 – Shell command stuck "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** – P1, 3 👍. A major workflow blocker: the CLI shows an active shell prompt even after the command finishes. Actively affecting daily use.
3.  **[#22323 – Subagent false success on MAX_TURNS](https://github.com/google-gemini/gemini-cli/issues/22323)** – P1, 2 👍. The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hits the turn limit without analyzing anything. This erodes trust in agent reporting.
4.  **[#21983 – Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** – P1, 1 👍. The browser agent crashes on Linux under Wayland. A critical gap for Linux users.
5.  **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** – P1 Epic. The backbone of quality assurance for the agent system. Tracks the expansion and hardening of the behavioral eval suite.
6.  **[#26516 / #26522 / #26523 / #26525 – Auto Memory bug cluster](https://github.com/google-gemini/gemini-cli/issues/26516)** – P2. A coordinated set of fixes targeting the Auto Memory system: indefinite retries on low-signal sessions, silent skipping of invalid patches, and deterministic secret redaction. Indicates the feature is still stabilizing.
7.  **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** – P2. The model ignores user-defined skills unless explicitly told to use them. Undermines the extensibility promise of the platform.
8.  **[#23571 – Model creates tmp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)** – P2. The agent frequently generates temporary edit scripts in arbitrary directories, creating major workspace cleanup overhead for users.
9.  **[#24246 – 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** – P2. The CLI hits a hard crash when the tool count exceeds the model limit. The agent lacks the ability to dynamically scope tool availability.
10. **[#22672 – Agent should discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** – P2, 1 👍. Users want safer defaults for commands like `git reset --force`, reflecting a desire for the agent to be "self-aware" of potential risks.

---

## 4. Key PR Progress (Top 10)

1.  **[#27429 – fix(core): handle EBADF in resizePty](https://github.com/google-gemini/gemini-cli/pull/27429)** – P1. A critical fix for `gemini --resume` crashes. Treats stale PTY file descriptors (EBADF) gracefully instead of crashing. *Related PR [#27371](https://github.com/google-gemini/gemini-cli/pull/27371) covers the same ground.*
2.  **[#26905 – fix(cli): synthesize bracketed-paste markers](https://github.com/google-gemini/gemini-cli/pull/26905)** – P1. Solves a major UX pain point on Windows/PowerShell/WSL2 where multi-line pastes were submitted prematurely.
3.  **[#27406 – feat(routing): configurable numeric routing rules](https://github.com/google-gemini/gemini-cli/pull/27406)** – P2 (community). Allows users to define custom complexity-score-to-model mappings in `settings.json`. Moves away from a hardcoded binary Pro/Flash threshold.
4.  **[#26914 – fix(core): include flash-lite in fallback chain](https://github.com/google-gemini/gemini-cli/pull/26914)** – P1. Ensures free-tier users fall back to `gemini-2.5-flash-lite` (1000 RPD) instead of erroring out when Pro and Flash quotas are exhausted.
5.  **[#26930 – fix(cli): restore previous extension on failed update](https://github.com/google-gemini/gemini-cli/pull/26930)** – P1. Prevents "update bricking" where a failed extension update leaves users without a working extension.
6.  **[#27418 – feat(core): non-interactive shell respects `enableInteractiveShell: false`](https://github.com/google-gemini/gemini-cli/pull/27418)** – P1. Closes a configuration adherence gap for headless/automated workflows.
7.  **[#27348 – fix: wrap Ajv validate() in try/catch (malformed schemas)](https://github.com/google-gemini/gemini-cli/pull/27348)** – P1. Prevents hard crashes when the LLM sends unexpected parameter shapes during tool validation.
8.  **[#27423 – feat(core): configurable per-tool-call timeout](https://github.com/google-gemini/gemini-cli/pull/27423)** – P3 (community). Adds a long-requested safety valve (`tools.callTimeout`) to cap unbounded tool execution.
9.  **[#27349 – fix: strip CJK characters from model thought output](https://github.com/google-gemini/gemini-cli/pull/27349)** – P2. Fixes an internationalization bug where the model leaked non-English thinking (Chinese/Japanese/Korean) into the user's terminal.
10. **[#26932 – fix(cli): handle refreshAuth rejection](https://github.com/google-gemini/gemini-cli/pull/26932)** – P1. Stops unhandled promise rejections during non-interactive OAuth flows, preventing auth crashes.

---

## 5. Feature Request Trends

- **Configurable Agent Autonomy:** The strongest signal is the demand for agents that respect user boundaries. This includes configurable routing rules (PR #27406), per-tool timeouts (PR #27423), server-driven model selection (#20878), and safer defaults for destructive operations (#22672).
- **Memory System Maturity:** The flurry of issues (cluster #26516) around Auto Memory indicates it is a flagship feature still fighting reliability issues. Users want deterministic redaction, safe handling of corrupt patches, and an end to infinite processing loops.
- **AST-Aware Code Analysis:** The investigation track (#22745, #22746, #22747) represents a forward-looking desire for deeper code understanding. The community and maintainers are actively evaluating if AST-aware tools can reduce token waste and improve codebase mapping precision.
- **Background & Parallel Execution:** Requests for backgroundable sub-agents (Ctrl+B) and advanced remote agent capabilities (#20303, #22741) imply users want the CLI to act as a persistent, multitasking AI engineer rather than a single-threaded assistant.

---

## 6. Developer Pain Points

- **Stuck Processes & Silent Failures:** The #1 frustration is the agent getting "stuck" without clear feedback. Issues like the generalist agent hanging ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands freezing ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and subagents lying about success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) indicate a systemic reliability gap in the execution loop.
- **Configuration Being Ignored:** Users repeatedly report that the agent ignores explicit configuration. The Browser Agent ignoring `settings.json` ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) and sub-agents running without permission ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) are prime examples that erode user trust.
- **Cross-Platform/Environment Woes:** Linux users on Wayland ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)) and Windows users fighting terminal buffering ([#26905](https://github.com/google-gemini/gemini-cli/pull/26905)) face experience gaps. The high volume of PTY/stale-fd fixes ([#27429](https://github.com/google-gemini/gemini-cli/pull/27429)) shows session management is brittle.
- **Workspace Littering:** The agent's habit of scattering temp scripts in the user's working directory ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) breaks standard git and CI hygiene workflows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest — 2026-05-25**

---

### 1. Today’s Highlights
The maintainers shipped three releases in the last 24 hours (v1.0.53, v1.0.54, v1.0.55-0), finally squashing the long-standing Bash shell hang caused by `PS0`/`PROMPT_COMMAND` and fixing the `/skills picker` to respect `--config-dir`. However, the community is grappling with a wave of input and rendering regressions: Chinese IME preedit text is accumulating at the bottom-right corner on macOS, paste is broken on GNOME Wayland, and clip/reflow issues are making output scroll unreachable. Interest in model pluralism remains intense, with Google Gemini support holding the highest upvote count of any open feature request.

---

### 2. Releases
Three releases landed in the past day, all focused on bug fixes:

- **v1.0.55-0** — Extensions now launch correctly when the CLI is packaged as a single-executable application (SEA).
- **v1.0.54** (2026-05-24) — General fixes and changes.
- **v1.0.53** (2026-05-24) — Three fixes:
  - Multiline prompts render fully without clipping or selection offset.
  - `/skills picker` now correctly honors the `--config-dir` flag (closes [#2926](https://github.com/github/copilot-cli/issues/2926)).
  - Bash shell sessions no longer hang when `PS0` or `PROMPT_COMMAND` is set in the environment (closes [#2350](https://github.com/github/copilot-cli/issues/2350)).

---

### 3. Hot Issues
*(10 noteworthy issues updated in the last 24 hours)*

1. **[#3502](https://github.com/github/copilot-cli/issues/3502) — Chinese Zhuyin IME preedit text rendered at bottom-right on macOS** *[NEW] [input-keyboard] [terminal-rendering]*  
   **(👍 29)** The community’s most-reacted issue. Composition text no longer follows the cursor. A clear accessibility/UX regression for East Asian-language users.

2. **[#2854](https://github.com/github/copilot-cli/issues/2854) — Google Gemini not available in Copilot CLI** *[OPEN] [models]*  
   **(👍 15)** The top-voted feature request. Users explicitly want a `--model` flag or backend toggle to use Gemini. Signals strong demand for model-agnostic support.

3. **[#3414](https://github.com/github/copilot-cli/issues/3414) — Paste regression on GNOME Wayland (1.0.49+)** *[OPEN] [platform-linux] [input-keyboard]*  
   **(👍 1)** Paste inside the prompt stopped working after upgrade. Works on the same machine in 1.0.48. A specific Linux desktop regression.

4. **[#3497](https://github.com/github/copilot-cli/issues/3497) — Terminal output clipped after resize/reflow** *[NEW] [terminal-rendering]*  
   **(👍 8)** Long responses are partially invisible and unreachable via the scrollbar. Points to a logic error in the recent terminal reflow rendering.

5. **[#3501](https://github.com/github/copilot-cli/issues/3501) — Scroll bar makes text unaligned on Windows** *[NEW] [platform-windows]*  
   **(👍 7)** The new vertical scrollbar introduced around v1.0.50 causes text alignment issues on Windows Console Host and Windows Terminal.

6. **[#2317](https://github.com/github/copilot-cli/issues/2317) — `~/.bash_history` truncated after Copilot executes a command** *[OPEN] [tools]*  
   **(👍 8, fresh comments)** Users report the fix from [#501](https://github.com/github/copilot-cli/issues/501) is incomplete. `HISTFILESIZE`/`HISTSIZE` are still ignored.

7. **[#3333](https://github.com/github/copilot-cli/issues/3333) — Android/Termux support broken in v1.0.48+ (glibc requirement)** *[OPEN] [platform-linux] [installation]*  
   **(👍 1, 5 comments)** A native Rust addon (`runtime.node`) compiled against glibc breaks usage on Termux (Bionic libc). Portability regression.

8. **[#3494](https://github.com/github/copilot-cli/issues/3494) — SKILL.md files with `description > 1024 chars` silently dropped from skills list** *[NEW] [plugins]*  
   **(👍 0)** No warning or error is raised when a skill description exceeds the 1024-char spec limit. Extension developers hit silent failures.

9. **[#3508](https://github.com/github/copilot-cli/issues/3508) — Extension lifecycle hooks receive empty `workingDirectory`** *[NEW] [plugins]*  
   **(👍 0)** Since v1.0.51, hooks like `onSessionStart` and `onPreToolUse` get `""` for `workingDirectory` instead of the actual directory. Breaks path-dependent extensions.

10. **[#3514](https://github.com/github/copilot-cli/issues/3514) — `list_agents` returns empty while background agents are visibly running** *[NEW] [agents] [context-memory]*  
   **(👍 0)** UI shows 7 active agents, but the `list_agents` tool returns `<no background agents>`. A state synchronization or caching bug.

---

### 4. Key PR Progress
No pull requests were updated in the last 24 hours. The bulk of engineering activity this cycle is concentrated on hotfix point releases rather than merging new feature pull requests.

---

### 5. Feature Request Trends
Aggregating signals from the last 24 hours presents three clear themes:

- **Model Pluralism & Configuration Overlays:** The highest-energy feature request by upvotes is direct Gemini support ([#2854](https://github.com/github/copilot-cli/issues/2854)). Issues like [#3507](https://github.com/github/copilot-cli/issues/3507) ("COPILOT_CUSTOM_INSTRUCTIONS_DIRS only half-honored") show users are already trying to use `CLAUDE.md` / `GEMINI.md` files, implying they want an agnostic CLI that works across providers.

- **Agent Ecosystem Scaling:** The demand for extensibility is accelerating. Requests for multiple agent directories ([#3505](https://github.com/github/copilot-cli/issues/3505)), built-in `/create-*` wizards ([#3503](https://github.com/github/copilot-cli/issues/3503)), and proper sub-agent tool provisioning ([#3506](https://github.com/github/copilot-cli/issues/3506)) all point to the community wanting a first-class agent marketplace rather than a single monolithic agent.

- **Remote & Mobile Parity:** Remote sessions via GitHub Mobile are gaining traction, but the experience is rough. Users need push notifications when an agent is blocked ([#3512](https://github.com/github/copilot-cli/issues/3512)), and the Android UI often renders nothing ([#3498](https://github.com/github/copilot-cli/issues/3498)).

---

### 6. Developer Pain Points
Three friction clusters dominate the current conversation:

- **The Rendering Tax:** The sharpest pain point. Recent rendering changes have introduced widespread visual regressions—scrollbars breaking layouts ([#3501](https://github.com/github/copilot-cli/issues/3501)), output going missing beyond the viewport ([#3497](https://github.com/github/copilot-cli/issues/3497)), IME text rendered in the wrong location ([#3502](https://github.com/github/copilot-cli/issues/3502)), and “steering” messages failing to appear until a huge delay ([#3500](https://github.com/github/copilot-cli/issues/3500)). Developer trust in the terminal renderer’s stability is eroding.

- **Extension & Plugin Instability:** A recurring pattern of silent failures is eroding confidence in the extension API. Skills created with long descriptions vanish without warning ([#3494](https://github.com/github/copilot-cli/issues/3494)), lifecycle hooks suddenly return empty data ([#3508](https://github.com/github/copilot-cli/issues/3508)), and specifications like `tools:` in agent frontmatter are ignored by sub-agents ([#3506](https://github.com/github/copilot-cli/issues/3506)).

- **Shell History and Environment Hostility:** A long-standing issue ([#2317](https://github.com/github/copilot-cli/issues/2317)) with truncated `~/.bash_history` is receiving renewed attention, indicating that proposed fixes are incomplete. Together with the recently patched `PS0`/`PROMPT_COMMAND` hang, it suggests Copilot’s shell integration still has deep friction with user shell configuration.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest | 2026-05-25

*Curated from public GitHub activity on MoonshotAI/kimi-cli*

---

## 1. Today's Highlights

Two major technical currents define today's landscape. First, a controversial, full-scale rewrite proposal swapping the Python CLI for Bun/TypeScript (PR #1707) continues to spark debate about the project’s architectural future. Second, a coordinated push around Agent Communication Protocol (ACP) compliance (PRs #2359, #2363, #2364) signals a strategic focus on multi-agent interoperability. On the stability front, a critical hang bug in the WebSocket API’s `Shell` tool was filed (Issue #2365), posing an immediate blocker for headless and remote-control use cases.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

Given the low volume of recent issue activity (3 items updated), the entire set of active discussions is covered below. Each represents a distinct and pressing theme.

**1. [Issue #2365] `kimi-code-worker` hangs on `Shell` tool via WebSocket API**
- **Significance:** Highly critical. Complete hang on the `Shell` tool blocks all remote execution patterns and automated pipelines relying on the WebSocket interface.
- **Community Reaction:** Brand new (posted today, 0 comments so far), but the severity places it at the top of the urgent-fix list for any headless or CI/CD use case.
- [Issue #2365](MoonshotAI/kimi-cli Issue #2365)

**2. [Issue #2232] Background tasks need to be able to adjust timeout**
- **Significance:** Recurring workflow disruption. Kimi’s optimistic timeout estimation frequently kills complex or long-running background tasks mid-execution, forcing destructive restarts with manual timing adjustments.
- **Community Reaction:** Growing consensus. The request is precise and actionable: expose knobs for background timeout configuration rather than enforcing rigid defaults.
- [Issue #2232](MoonshotAI/kimi-cli Issue #2232)

**3. [Issue #1894] Kimi CLI cannot recursively load nested skill directories**
- **Significance:** Ecosystem friction. Codex supports recursive skill hierarchies (e.g., `.agents/skills/cloudlive/skills/…`), but Kimi does not. This creates a real portability barrier for teams with complex, multi-level skill structures.
- **Community Reaction:** Well-documented with a concrete example. The four comments underscore a desire for parity with Codex’s loading strategy and cleaner repository layouts.
- [Issue #1894](MoonshotAI/kimi-cli Issue #1894)

---

## 4. Key PR Progress

**1. [PR #1707] refactor: rewrite from Python to Bun + TypeScript + React Ink**
- **Summary:** A massive draft refactor (~32k lines, 166 TSX files) proposing a complete rewrite of the CLI. The PR title ("kimi cli 用python是彻底的失败") expresses strong architectural dissatisfaction. React Ink replaces the current Python terminal UI.
- **Why It Matters:** Signals a significant contributor divide regarding DX and performance. If adopted, this would fundamentally reshape the project’s contribution model and dependency footprint.
- [PR #1707](MoonshotAI/kimi-cli PR #1707)

**2. [PR #2359] fix(acp): assign message ids to streamed content**
- **Summary:** Adds proper `messageId` values to streamed ACP content. Built to support integration with third-party agent platforms (e.g., PwrAgent).
- **Why It Matters:** A blocking requirement for reliable ACP-based multi-agent coordination and event tracking.
- [PR #2359](MoonshotAI/kimi-cli PR #2359)

**3. [PR #2363] fix(acp): replay loaded session history**
- **Summary:** Ensures restored ACP sessions correctly replay the full conversation and tool call history. Stacked on PR #2359.
- **Why It Matters:** Session resume is a core feature for long-running, interactive agent collaborations; the previous implementation lost history on load.
- [PR #2363](MoonshotAI/kimi-cli PR #2363)

**4. [PR #2364] feat(acp): support permission mode switching**
- **Summary:** Adds protocol-level dynamic permission switching to ACP sessions. Resolves Issue #1414.
- **Why It Matters:** Enables secure, context-aware escalation patterns — a must for enterprise deployments needing varying authorization levels during a session.
- [PR #2364](MoonshotAI/kimi-cli PR #2364)

**5. [PR #2362] fix: retain original line break style and fix cross-platform CRLF/LF issues**
- **Summary:** Root-caused the corruption to Python’s `readtext()` universal newlines mode. Fixes `StrReplaceFile` and `WriteFile` to respect the original line-ending style.
- **Why It Matters:** A cross-platform "paper cut" that silently breaks file integrity for Windows developers. Resolves Issues #1952 and #2191.
- [PR #2362](MoonshotAI/kimi-cli PR #2362)

**6. [PR #2361] [codex] docs: clarify hooks notification example**
- **Summary:** Replaces non-functional `permission_prompt` examples in the hooks documentation with real background-task notification types.
- **Why It Matters:** Fixes documentation that actively misled developers building automated approval workflows.
- [PR #2361](MoonshotAI/kimi-cli PR #2361)

**7. [PR #2335] docs: fix Notification hook matcher example**
- **Summary:** Updates hook config fixtures and clarifies that `Notification` matchers use notification types, not sink names.
- **Why It Matters:** Complements PR #2361; together they address a documentation blind spot that caused frequent config errors.
- [PR #2335](MoonshotAI/kimi-cli PR #2335)

---

## 5. Feature Request Trends

Four distinct directional signals emerge from today’s data:

- **ACP Interoperability:** The most concentrated effort. Multiple stacked PRs target message IDs, session history replay, and dynamic permission switching — all aimed at making Kimi a first-class node in the agent protocol ecosystem.
- **Codex Feature Parity:** The inability to load recursive skill directories (Issue #1894) remains the single most prominent compatibility gap. There is clear demand for Kimi to match Codex’s configuration and skill discovery patterns.
- **User-Controllable Execution Lifecycles:** The call for adjustable background timeouts (Issue #2232) reflects a broader desire for escape hatches from the CLI’s aggressive scheduling heuristics.
- **Developer Documentation Quality:** The repeated fixes to hook/matcher documentation (PRs #2335, #2361) suggest a recurring blind spot that actively wastes developer time.

---

## 6. Developer Pain Points

- **Architectural Churn / Language Bet:** The Python-to-TypeScript rewrite proposal (PR #1707) is not merely a refactor — it forces the community to choose sides on the project’s technological foundation. Such debates can stall feature development on the current codebase.
- **Unforgiving Timeouts:** Background tasks are killed with no user recourse. The rigid timeout model destroys trust for non-interactive, batch, or pipeline-based workflows. Issue #2232 captures a deeply felt frustration.
- **Stability at the Edges:** The WebSocket API hang (Issue #2365) and the cross-platform line-ending corruption (PR #2362) are high-friction bugs that erode confidence in the tool’s remote execution and cross-platform compatibility.
- **Documentation Friction:** Hooks and matchers are a powerful feature, but the recent flurry of corrections to their documentation (PRs #2335, #2361) suggests the barrier to entry is higher than it should be. Correct documentation is a prerequisite for adoption.
- **Ecosystem Lock-Out:** The flat skill directory limitation (Issue #1894) directly penalizes users who adopt advanced directory organization patterns — pushing them back to Codex or forcing unnatural repository structures.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-25

## Today's Highlights
The community is actively discussing the implications of DeepSeek V4 Pro’s permanent 75% price cut on OpenCode Go quotas, while developers grapple with acute stability issues in the v1.15.10 release, including streaming freezes and TUI boot hangs. On the development front, several high-impact PRs are landing, focusing on session visibility, subagent reliability, and MCP connection robustness.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

[#29079](https://github.com/anomalyco/opencode/issues/29079) **GPT Models Takes Too Long to Respond** (40 comments, 17 👍)  
One of the most active threads this week. Users report severe intermittent latency on GPT 5.4/xhigh for simple tasks like updating `graphify`. The issue points toward a potential request orchestration bottleneck rather than provider speed. The volume of community engagement indicates this is a top-tier performance concern.

[#15585](https://github.com/anomalyco/opencode/issues/15585) **"Free usage exceed" error on free models** (38 comments, 10 👍)  
A persistent source of user confusion dating back months. Users believe free models should be genuinely unlimited; the 38-comment thread reveals a significant documentation and metering transparency gap.

[#2242](https://github.com/anomalyco/opencode/issues/2242) **Sandbox the Agent** (35 comments, 46 👍)  
The highest-reaction issue this cycle. Users are demanding strict file-system sandboxing similar to Gemini CLI or Codex CLI seatbelts. With 46 upvotes, this is the single most requested security feature.

[#28846](https://github.com/anomalyco/opencode/issues/28846) **Adjust Go usage limits after DeepSeek V4 Pro price cut** (10 comments, 11 👍)  
A pragmatic financial feature request: DeepSeek permanently dropped V4 Pro API pricing by 75%, and subscribers want Go quotas proportionally increased. Closely tied to [#29151](https://github.com/anomalyco/opencode/issues/29151) which asks the same question.

[#29129](https://github.com/anomalyco/opencode/issues/29129) **OpenAI stream intermittently freezes with high CPU** (8 comments)  
A critical stability bug. During streaming responses, OpenCode enters a working state with zero visible output while burning CPU indefinitely until the process is killed. The user provided a detailed tcpdump analysis showing idle HTTPS sockets.

[#29134](https://github.com/anomalyco/opencode/issues/29134) **TUI hangs after session creation — v1.15.10** (4 comments, 2 👍)  
A v1.15.10 regression on macOS Apple Silicon. Both `opencode` TUI and `opencode run` hang after session creation. The build call never completes, effectively breaking the terminal workflow for affected users.

[#22020](https://github.com/anomalyco/opencode/issues/22020) **Global AGENTS.md silently ignored when project file exists** (9 comments)  
A configuration layering bug. The documentation promises global rules merge with project-level rules, but the current behavior silently drops the global file. The discrepancy between docs and behavior has frustrated power users.

[#29187](https://github.com/anomalyco/opencode/issues/29187) **gpt-5.5 unexpected EOF on custom providers** (3 comments)  
An interoperability bug. A custom OpenAI-compatible endpoint works fine with gpt-5.4 and DeepSeek, and works for gpt-5.5 in Codex, but fails in OpenCode with an `unexpected EOF`. Points to fragile streaming response parsing.

[#29190](https://github.com/anomalyco/opencode/issues/29190) **MCP remote connections silently die** (2 comments)  
A thorough root-cause analysis. Remote HTTP/SSE MCP connections drop after idle periods with no `onclose`/`onerror` handling, no reconnection logic, and no heartbeat. The status falsely shows "connected" while all tool calls fail with "Not connected".

[#29195](https://github.com/anomalyco/opencode/issues/29195) **Zen Payment SCAM warning** (6 comments)  
A critical community safety notice. Users report a fake GO subscription payment redirect to "OpenCode ZEN". The thread advises initiating chargebacks with banks and preserving screenshots.

---

## Key PR Progress

[#29193](https://github.com/anomalyco/opencode/pull/29193) **feat(skill): add hidden frontmatter field**  
Merges feature parity with `AgentConfig.hidden`, allowing users to hide unused skills from the TUI skill picker. A clean UX improvement requested by power users with large skill libraries.

[#29176](https://github.com/anomalyco/opencode/pull/29176) **fix(task): surface non-text subagent results**  
Closes [#24447](https://github.com/anomalyco/opencode/issues/24447). Fixes a critical bug where reasoning models (e.g., GPT OSS 120B) produce empty `<task_result>` when they complete without a final text block. The fix preserves whatever content the subagent generated.

[#29174](https://github.com/anomalyco/opencode/pull/29174) **fix(tui): show direct child sessions as subagents**  
Closes [#29175](https://github.com/anomalyco/opencode/issues/29175). Plugin-created child sessions (`session.create(parentID)`) were invisible in the parent TUI because discovery relied solely on native `task` metadata. Fixes this gap for the plugin ecosystem.

[#29130](https://github.com/anomalyco/opencode/pull/29130) **fix(tui): open external editor in worktree cwd**  
The `/editor` command now launches the editor with an explicit working directory matching the project worktree, fixing a UX bug where editors inherited the TUI process directory.

[#26861](https://github.com/anomalyco/opencode/pull/26861) **fix(tui): Old messages disappearing during long sessions**  
Implements lazy-scroll loading (50 older messages on scroll-up). Fixes the long-standing [#7380](https://github.com/anomalyco/opencode/issues/7380) where conversation history silently dropped off in extended sessions.

[#26580](https://github.com/anomalyco/opencode/pull/26580) **fix: normalize Windows desktop session paths**  
Closes [#17765](https://github.com/anomalyco/opencode/issues/17765). A critical Windows fix where all session history vanished on every app restart due to path normalization issues.

[#29173](https://github.com/anomalyco/opencode/pull/29173) **feat(opencode): add question ask and wait endpoints**  
Adds `POST /question` and `GET /question/:requestID/wait` endpoints, enabling external clients to interact with the session question flow without managing internal event bus state.

[#27802](https://github.com/anomalyco/opencode/pull/27802) **feat(opencode): fff search tools**  
Implements `fzf`-style fuzzy finders for file search, content search, and directory search. Brings fast interactive search directly into the TUI.

[#20491](https://github.com/anomalyco/opencode/pull/20491) **feat(opencode): add Kiro provider**  
A community contribution adding Kiro (AWS) as a first-class provider option, expanding the provider ecosystem for users in the AWS ecosystem.

[#27785](https://github.com/anomalyco/opencode/pull/27785) **fix(mcp): handle OAuth flows that connect without tokens**  
Closes [#5953](https://github.com/anomalyco/opencode/issues/5953). Fixes a subtle MCP OAuth path where a remote server completes transport setup without persisting OAuth credentials.

---

## Feature Request Trends

**Agent Sandboxing & Safety**  
Issue #2242 dominates the requests this week. The community wants rigorous file-system and network sandboxing before agents can be truly trusted for autonomous execution.

**Cost Optimization Alignment**  
The DeepSeek V4 Pro permanent 75% price cut has energized users to demand proportional quota increases on the Go subscription tier (#28846, #29151). This correlates with a broader push for provider pricing transparency.

**Remote & Mobile Development**  
A strong undercurrent for WebSocket-based ACP (#13388), SSH file editing (#29152), and mobile control workflows (#29121). Users want OpenCode as a remote development terminal.

**Session Management Overhaul**  
Page-based history navigation (#26327), archived session views (#15250), and close confirmation / minimize-to-tray (#27463) all point to growing maturity demands around session lifecycle.

**Provider & Plugin Ecosystem Growth**  
New provider requests (CommandCode #26338, Kiro #20491) and inline skill invocation (#22666) indicate a thriving ecosystem pull.

---

## Developer Pain Points

**Stability & Performance Regressions**  
The v1.15.10 release introduced concerning hangs (#29134) and streaming freezes (#29129), eroding confidence in the release cycle. Combined with slow GPT responses (#29079) and Windows memory bloat (#7827), stability is the community’s top unaddressed theme.

**Model Interoperability Fragility**  
A recurring pattern of model-specific edge cases: GPT-5.5 EOF errors (#29187), GPT OSS 120B subagent truncation (#27210), and orphaned tools causing `model does not support assistant message prefill` errors (#26177). Response parsing and state cleanup logic need hardening.

**Configuration Friction**  
Silent failures remain the most frustrating bug class. Global `AGENTS.md` layering breaks (#22020) and config changes requiring full app restarts (#10899) interrupt deep workflow states.

**Infrastructure Gaps**  
MCP connections dying without heartbeat or reconnection (#29190), hard 5-minute timeouts on local providers (#26602), and broken Nix flake builds since v1.4.11 (#23719) highlight gaps in the supporting infrastructure layer.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest: 2026-05-25

## 1. Today's Highlights
A major infrastructure improvement lands today as XDG Base Directory compliance ([PR #256](https://github.com/earendil-works/pi/pull/256)) is finally merged after months of community demand, promising an auto-migration from `~/.pi/` to standardised paths. The new Alibaba DashScope provider ([PR #4964](https://github.com/earendil-works/pi/pull/4964)) is now available, bringing 22 Qwen models including the highly capable Qwen 3.7 Max. On the reliability front, a critical report of `openai-codex` sessions permanently hanging on "Working…" ([Issue #4945](https://github.com/earendil-works/pi/issues/4945)) has the community on edge, while a large cumulative patch bundle including rollback fixes and auto-memory RPC ([PR #4974](https://github.com/earendil-works/pi/pull/4974)) was merged to stabilise the codebase.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Hot Issues

- **[Issue #4945](https://github.com/earendil-works/pi/issues/4945) – openai-codex hangs on "Working…"** (13 comments, 👍5)  
  A top-priority bug where `gpt-5.5` sessions get stuck with no streaming output, tool calls, or error messages. Users can only recover via Escape, which records an aborted turn. No confirmed fix yet; this is displacing user workflow trust.

- **[Issue #2870](https://github.com/earendil-works/pi/issues/2870) – Follow XDG Base Directory** (14 comments, 👍26)  
  The definitive feature request for Linux configuration hygiene. With 26 thumbs up it was the most popular open request; the companion PR (#256) has now been merged.

- **[Issue #4916](https://github.com/earendil-works/pi/issues/4916) – Collapse file read output** (19 comments)  
  A highly requested UX setting to truncate verbose file reads to a single line in the CLI, similar to the existing "hide thinking" toggle. Strong community demand for terminal output cleanliness.

- **[Issue #4897](https://github.com/earendil-works/pi/issues/4897) – RPC mode "write ENOBUFS"** (13 comments)  
  A stability crash affecting users driving Pi programmatically via JSONL over stdout. High-volume streaming causes the process to exit non-zero. Backpressure fixes in PR #4950 aim to alleviate this.

- **[Issue #4946](https://github.com/earendil-works/pi/issues/4946) – TUI crash on long tool output** (6 comments)  
  A hard crash when tool output exceeds terminal width. Severely impacts users with narrow terminals or verbose tool outputs. Closed with a fix already applied.

- **[Issue #4707](https://github.com/earendil-works/pi/issues/4707) – Agent hangs on 429 rate limits** (4 comments, 👍3)  
  A regression introduced by the Undici fetch implementation causing permanent hangs during provider rate limits. The community is eager for the HTTP idle timeout configuration in PR #4759.

- **[Issue #4046](https://github.com/earendil-works/pi/issues/4046) – Compaction deletes everything** (8 comments)  
  A terrifying data-loss issue where session compaction blanks all history. Root cause (a race condition on `AbortController.signal`) is being fixed in PR #4958.

- **[Issue #4801](https://github.com/earendil-works/pi/issues/4801) – DeepSeek v4 reasoning_effort validation** (5 comments)  
  Configuration friction where OpenRouter rejects valid `xhigh` effort values. Highlights the broader challenge of normalising provider-specific parameters.

- **[Issue #4923](https://github.com/earendil-works/pi/issues/4923) – Long URLs break at hyphens** (3 comments)  
  A rendering bug where word-wrapping splits URLs at hyphens, breaking clickability. Closed with a tokenisation fix merged.

- **[Issue #4953](https://github.com/earendil-works/pi/issues/4953) – Installer modifies PATH unnecessarily with asdf** (2 comments)  
  Installer experience bug where Pi tries to modify PATH even when an `asdf` shim correctly resolves the binary.

## 4. Key PR Progress

- **[PR #256](https://github.com/earendil-works/pi/pull/256) (Merged)** – Implements XDG Base Directory compliance with auto-migration from legacy `~/.pi/` paths. This was the clear #1 community request by votes and has been in the works since December 2025.

- **[PR #4974](https://github.com/earendil-works/pi/pull/4974) (Merged)** – Large cumulative patch bundling rollback bug fixes, a change review UI redesign, hooks compatibility improvements, and an auto-memory RPC addition. Represents a major stabilization and feature pass.

- **[PR #4964](https://github.com/earendil-works/pi/pull/4964) (Merged)** – Adds the DashScope provider (Alibaba Bailian) with 22 Qwen models, unlocking Qwen 3.7 Max via an OpenAI-compatible Chat Completions endpoint with first-class thinking support.

- **[PR #4958](https://github.com/earendil-works/pi/pull/4958) (Merged)** – Fixes a compaction abort controller race condition guarding `.signal` access across async boundaries. Directly addresses the data-loss crash in Issue #4046.

- **[PR #4965](https://github.com/earendil-works/pi/pull/4965) (Merged)** – Disables Kitty keyboard protocol flag 2 to prevent VS Code integrated terminal viewport reset on focus regain. A quality-of-life fix for daily VS Code users.

- **[PR #4962](https://github.com/earendil-works/pi/pull/4962) (Merged)** – Polishes terminal markdown rendering. Headings and code blocks now render natively instead of showing raw `#` markers, improving visual hierarchy.

- **[PR #4950](https://github.com/earendil-works/pi/pull/4950) (Merged)** – Fixes backpressure retry aborts in the RPC layer. Critical for the stability of programmatic users hit by the "write ENOBUFS" crash (Issue #4897).

- **[PR #4911](https://github.com/earendil-works/pi/pull/4911) (Open)** – Adds device code login for Codex, providing a second authentication screen alternative to the default OAuth flow. Closes Issue #3424.

- **[PR #4954](https://github.com/earendil-works/pi/pull/4954) (Open)** – Exposes `getToolDefinition` to the command context. Aimed at extension authors who need runtime introspection of tool schemas for dynamic tool user interfaces.

- **[PR #4651](https://github.com/earendil-works/pi/pull/4651) (Draft/Open)** – Experimentally fetches a portable Git Bash for Windows. While the ~350MB footprint is controversial, it signals strong intent to improve the native Windows developer experience.

## 5. Feature Request Trends

- **Terminal UI Maturity** – The community is intensely focused on making the terminal output cleaner and more professional. Requests for collapsible file read blocks ([Issue #4916](https://github.com/earendil-works/pi/issues/4916)), sticky bottom layouts ([Issue #3146](https://github.com/earendil-works/pi/issues/3146)), better markdown rendering, and accessibility via screen reader support ([Issue #4687](https://github.com/earendil-works/pi/issues/4687)) dominate. The TUI is graduating from a proof-of-concept to a polished daily-driver.

- **Config & Data Portability** – There is a strong push for Linux best practices and robust path handling. The XDG Base Directive compliance ([PR #256](https://github.com/earendil-works/pi/pull/256)) was the pinnacle of this, but related requests for respecting `PI_CONFIG_DIR` ([Issue #2390](https://github.com/earendil-works/pi/issues/2390)), fixing session folder collisions ([Issue #4877](https://github.com/earendil-works/pi/issues/4877)), and hiding sensitive env vars ([related discussions]) show a deep desire for robust filesystem and configuration behaviour.

- **Provider Agnosticism & Expansion** – Users want access to the best models from any backend. The DashScope provider ([PR #4964](https://github.com/earendil-works/pi/pull/4964)) and the DeepSeek `reasoning_effort` configuration friction ([Issue #4801](https://github.com/earendil-works/pi/issues/4801)) highlight demand for both new backends and fluid parameter passing. The proposal for "provider-hosted tools" ([Issue #4955](https://github.com/earendil-works/pi/issues/4955)) points toward a future where the local tool executor is not the only path.

- **Stability & Resilience** – Recurring themes of "never fail silently". Issues #4945 (hang on Working...), #4707 (hang on 429), and #4046 (data loss during compaction) indicate the community values deterministic error recovery just as much as feature velocity.

## 6. Developer Pain Points

- **The "Working…" Hang ([Issue #4945](https://github.com/earendil-works/pi/issues/4945))** – The single most pressing issue. Zero-usage aborted turns leave users stranded with no feedback. The only escape is a destructive abort, which directly destroys workflow trust.

- **Data Integrity Scares ([Issue #4046](https://github.com/earendil-works/pi/issues/4046), [#4877](https://github.com/earendil-works/pi/issues/4877), [#4919](https://github.com/earendil-works/pi/issues/4919))** – Compaction deleting everything, session folder collisions, and stale auth locks causing "No API key found" errors erode confidence in local state management. Users fear losing context or configuration on crash.

- **Terminal UX Regressions ([Issue #4946](https://github.com/earendil-works/pi/issues/4946), [#4923](https://github.com/earendil-works/pi/issues/4923), [#4918](https://github.com/earendil-works/pi/issues/4918))** – Crashing on long lines, breaking URL clickability at word-wrap boundaries, and `Shift+Enter` not inserting newlines are frustrating daily-driver bugs that break flow state.

- **Package Management & Installer Friction ([Issue #4953](https://github.com/earendil-works/pi/issues/4953), [#4842](https://github.com/earendil-works/pi/issues/4842), [#4929](https://github.com/earendil-works/pi/issues/4929))** – Conflicts with `asdf` shims, undeclared transitive dependencies that break under `pnpm`/Yarn PnP, and confusing `minimumReleaseAge` update logic suggest the shipping and packaging layer needs more investment.

- **API Key & Authentication Hiccups ([Issue #4919](https://github.com/earendil-works/pi/issues/4919), [#4801](https://github.com/earendil-works/pi/issues/4801))** – Stale file locks and provider-specific parameter validation (e.g. DeepSeek `reasoning_effort` on OpenRouter) waste significant debugging time for users who simply want to code.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

**Qwen Code Community Digest — 2026-05-25**

---

### Today's Highlights
The **Mode B (daemon) roadmap** continues to dominate activity: the large integration merge [#4490](https://github.com/QwenLM/qwen-code/pull/4490) pulls F1–F5 features into `main`, while new endpoints like `POST /session/:id/recap` ([#4504](https://github.com/QwenLM/qwen-code/pull/4504)) and cross-client real-time sync ([#4484](https://github.com/QwenLM/qwen-code/pull/4484)) round out the serve story. On the telemetry side, a cluster of fixes address broken trace IDs and LogToSpan bridge reliability. Security work continues with runaway-protection guardrails for headless mode ([#4502](https://github.com/QwenLM/qwen-code/pull/4502)) and better denial observability for AUTO mode ([#4476](https://github.com/QwenLM/qwen-code/pull/4476)).

---

### Releases
- **v0.16.1-nightly.20260525.84f408017**
  - Fix: Clean stale outputs before `tsc --build` to prevent **TS5055** errors.
  - Chore: Nightly release bump.

---

### Hot Issues
1.  [#4175 — proposal(serve): Mode B feature-priority roadmap toward v0.16 production-ready](https://github.com/QwenLM/qwen-code/issues/4175)
    *38 comments.* The central coordination issue for the daemon architecture. Stage 1 (single daemon per workspace) is live; this issue tracks the remaining work (F1–F5). Active collaboration from multiple core contributors. **Strategic importance: defining the v0.16 release scope.**

2.  [#4488 — qwen code插件(v0.16.0)在vscode左侧栏不显示](https://github.com/QwenLM/qwen-code/issues/4488)
    *6 comments.* The VS Code extension fails to render in the sidebar on VS Code ≥ 1.120.0. A significant UX regression—the plugin flashes and disappears. High urgency for IDE users.

3.  [#4276 — oom-crash](https://github.com/QwenLM/qwen-code/issues/4276)
    *8 comments.* Detailed OOM logs from scavenge cycles. Likely related to large context windows. Needs triage for memory management improvements.

4.  [#4501 — bug(provider/dashscope): side-query thinking disable doesn't reach qwen3 series](https://github.com/QwenLM/qwen-code/issues/4501)
   *New issue from core dev.* The `enable_thinking` field is only rewritten when it already exists on the request body. For OpenAI-compatible providers (including DashScope), it is never pre-populated, so the user’s choice to disable thinking is silently ignored.

5.  [#4486 — bug(telemetry): qwen-code.interaction span has wrong trace id](https://github.com/QwenLM/qwen-code/issues/4486)
   *New, filed by core dev.* `startInteractionSpan` misses the parent `ctx` argument, creating orphan spans. Immediately fixed in [#4499](https://github.com/QwenLM/qwen-code/pull/4499).

6.  [#4493 — rider无法登录qwen code](https://github.com/QwenLM/qwen-code/issues/4493)
   *2 comments.* JetBrains Rider login redirect loops if the user is already authenticated in the browser, blocking access to Aliyun token plans. **IDE integration blocker.**

7.  [#4479 — 需要一个功能统计Qwen Code每日消耗的Token数量](https://github.com/QwenLM/qwen-code/issues/4479)
   *3 comments.* A user discovered a single session burned 30M tokens and requests a daily token consumption counter. The feature request is labeled with `scope/analytics` and `welcome-pr`, indicating a good opportunity for external contributions.

8.  [#4494 — Side queries ignore the user's configured output language](https://github.com/QwenLM/qwen-code/issues/4494)
   *1 comment.* `recap`, `title`, `tool-use summary`, and `suggestions` don't respect the `output-language.md` configuration. Undermines the multilingual UX promise.

9.  [#4442 — BUG UI/UX](https://github.com/QwenLM/qwen-code/issues/4442)
   *1 comment.* Reports UI freezing during bulk file edits and conversation jank on long threads, requiring manual terminal deletion. Likely tied to rendering bottlenecks in the interactive terminal.

10. [#4421 — feat(diagnostics): 本地问题诊断框架 — ring buffer + diagnostic ID + /bug collect bundle](https://github.com/QwenLM/qwen-code/issues/4421)
    *3 comments.* Proposes a local-first diagnostic framework (ring buffer, diagnostic IDs, `/bug collect`). Addresses the pain of debugging API/SSE failures without pre-enabled debug mode. Strong UX and support orientation.

---

### Key PR Progress
1.  [#4490 — chore(integration): merge daemon_mode_b_main into main — F1/F2/F3/F4-prereq + F5 alpha docs batch](https://github.com/QwenLM/qwen-code/pull/4490)
    *Massive batch merge.* Pulls the first five features of the Mode B roadmap into `main`. A key synchronization point for the serve architecture.

2.  [#4504 — feat(serve): add POST /session/:id/recap](https://github.com/QwenLM/qwen-code/pull/4504)
    Exposes `generateSessionRecap` over HTTP/SSE. Allows daemon clients (SDK, Web UI, IDE plugins) to fetch a one-sentence "where did I leave off" summary without a full prompt turn.

3.  [#4502 — feat(cli): headless / non-interactive runaway-protection guardrails](https://github.com/QwenLM/qwen-code/pull/4502)
    Phased implementation of `--max-wall-time` and `--max-tool-calls` for headless mode. Closes the widely-requested [#4103](https://github.com/QwenLM/qwen-code/issues/4103). Essential for production-grade CLI usage.

4.  [#4484 — feat(daemon+sdk): cross-client real-time sync completeness](https://github.com/QwenLM/qwen-code/pull/4484)
    Closes eight sync gaps where actions on one SSE client failed to propagate to others on the same session. Core infrastructure for multi-client daemon sessions.

5.  [#4495 — Enable Token Plan cache control](https://github.com/QwenLM/qwen-code/pull/4495)
    Routes Token Plan endpoints through the DashScope-compatible path to enable cache-control metadata. Directly addresses the missing cache metrics reported in [#4444](https://github.com/QwenLM/qwen-code/issues/4444).

6.  [#4499 — fix(telemetry): attach interaction span to session root context](https://github.com/QwenLM/qwen-code/pull/4499)
    *Fixes #4486.* The missing `ctx` argument in `startInteractionSpan` was splitting the interaction span into an orphan trace. Now properly parented under the session root.

7.  [#4161 — feat(cli): add auto-improve command](https://github.com/QwenLM/qwen-code/pull/4161)
    Adds a `/auto-improve` slash command for session-scoped, continuously verifying improvement loops. Supports scheduled ticks and local state tracking. New tool for CI-like workflows inside the agent.

8.  [#4491 — fix(sdk): honor canUseTool timeout in CLI control requests](https://github.com/QwenLM/qwen-code/pull/4491)
    Tool permission prompts were falling back to a shorter generic timeout instead of the SDK’s configured `canUseTool` timeout. Fixes a real-world UX race where user approval expired prematurely.

9.  [#4476 — Add AUTO mode denial observability and caps](https://github.com/QwenLM/qwen-code/pull/4476)
    Adds structured denial boundaries and a cumulative denial cap for AUTO mode, alongside hooks for classifier visibility. Strengthens the safety contract for autonomous execution.

10. [#4410 — feat(telemetry): Phase 3 — qwen-code.subagent span with concurrent isolation](https://github.com/QwenLM/qwen-code/pull/4410)
    Wraps subagent invocations in their own span, preventing LLM/tool spans from interleaving across concurrent siblings. Critical for observability of parallel subtask execution.

---

### Feature Request Trends
- **Daemon / Mode B Progression:** The community and core team are highly aligned on shipping Mode B to production. Requests for session management APIs ([#4503](https://github.com/QwenLM/qwen-code/issues/4503) — Message ID in ACP) and real-time sync are rising as the daemon matures.
- **Telemetry & Observability:** A strong wave of requests for better local diagnostics ([#4421](https://github.com/QwenLM/qwen-code/issues/4421)), token usage dashboards ([#4479](https://github.com/QwenLM/qwen-code/issues/4479)), and cache visibility ([#4444](https://github.com/QwenLM/qwen-code/issues/4444)) suggests users need more tools to understand agent behavior and cost.
- **Safety and Guardrails:** Headless runaway protection ([#4103](https://github.com/QwenLM/qwen-code/issues/4103) → [#4502](https://github.com/QwenLM/qwen-code/pull/4502)) and AUTO mode denial observability ([#4476](https://github.com/QwenLM/qwen-code/pull/4476)) dominate safety discussions. Credential security in extensions ([#4425](https://github.com/QwenLM/qwen-code/issues/4425)) underscores a focus on supply chain risk.
- **Project-Level Configuration:** Requests for `QWEN.local.md` ([#4091](https://github.com/QwenLM/qwen-code/issues/4091)) and better handling of invalid `settings.json` ([#4448](https://github.com/QwenLM/qwen-code/issues/4448)) show demand for robust, per-project runtime customization.

---

### Developer Pain Points
- **IDE Compatibility across versions:** VS Code 1.120.0 breaks the extension sidebar ([#4488](https://github.com/QwenLM/qwen-code/issues/4488)); JetBrains Rider has a redirect-loop login failure ([#4493](https://github.com/QwenLM/qwen-code/issues/4493)). These issues directly block daily users on modern editors.
- **Stability under load:** OOM crashes ([#4276](https://github.com/QwenLM/qwen-code/issues/4276)) and UI freezes during bulk file edits ([#4442](https://github.com/QwenLM/qwen-code/issues/4442)) indicate memory management and rendering bottlenecks that hurt user trust for complex tasks.
- **Silent configuration failures:** An invalid `.qwen/settings.json` is silently ignored, falling back to first-time setup ([#4448](https://github.com/QwenLM/qwen-code/issues/4448)). Side queries ignoring the user’s configured output language ([#4494](https://github.com/QwenLM/qwen-code/issues/4494)) erodes the customization contract.
- **Telemetry gaps for cost awareness:** Users cannot audit their token consumption without external tools ([#4479](https://github.com/QwenLM/qwen-code/issues/4479)), and cache effectiveness metrics are missing from `/stats model` for Token Plan users ([#4444](https://github.com/QwenLM/qwen-code/issues/4444)).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-05-25

> **Project Rebrand Note:** The repository previously known as `DeepSeek-TUI` has formally rebranded to **CodeWhale** as of v0.8.43/v0.8.44. The community digest retains the "DeepSeek TUI" title context per the initiative's origin, but all development now lives under the CodeWhale identity.

---

## 1. Today's Highlights

The CodeWhale project accelerated its rebranding with v0.8.43 and v0.8.44 shipping as a coordinated rename batch, introducing deprecation shims for the legacy `deepseek` / `deepseek-tui` binaries. Meanwhile, the v0.8.45 **"Control Plane"** release is in its final preparation ([PR #2118](Hmbown/CodeWhale PR #2118)), aiming to make agentic terminal work **interruptible and recoverable**. The community is simultaneously rallying around a cross-provider model catalog, persistent cost visibility, and a new voice input prototype that was deliberately descoped from v0.8.45 to v0.8.46 for cross-platform hardening.

---

## 2. Releases

- **v0.8.43 / v0.8.44 — The Rebranding Batch**  
  The project officially renames from DeepSeek TUI to **CodeWhale**. Legacy binaries (`deepseek`, `deepseek-tui`) are now deprecation shims that print a one-line warning and forward execution to `codewhale` / `codewhale-tui`. These shims will be removed entirely in v0.9.0. See `docs/REBRAND.md` for the migration guide.

- **v0.8.45 (Release Candidate In Progress)**  
  The upcoming release emphasizes **interruptibility and recovery**: RLM session objects, cancellable directory/search tools, deterministic whale-species sub-agent naming, the `/balance` billing scaffold, test verifier preview wiring, and contributor credit updates. Voice input prototypes were completed but pulled from the release branch and deferred to v0.8.46.

---

## 3. Hot Issues

*Data source: [Hmbown/CodeWhale Issues](Hmbown/CodeWhale Issue #...)*

1. **[#1615 — Docker garbled output](Hmbown/CodeWhale Issue #1615)**  
   *188 comments / CLOSED*  
   Users running via Docker experience irresolvable garbled terminal output. Despite being closed, this issue generated the highest community engagement in the tracker, revealing significant friction in the containerized setup path.

2. **[#2104 — Homebrew distribution fails: `codewhale` not found](Hmbown/CodeWhale Issue #2104)**  
   *2 comments / OPEN*  
   A direct rebranding casualty: the Homebrew formula installs the legacy shim but not the primary `codewhale` binary, breaking `brew upgrade` workflows for macOS users.

3. **[#2114 — Provider config silently overridden by environment variables](Hmbown/CodeWhale Issue #2114)**  
   *0 comments / OPEN*  
   Using `/profile` to switch configurations is ignored when a conflicting `$DEEPSEEK_API_KEY` or `$DEEPSEEK_PROVIDER` env var is set. A dangerous silent override for multi-provider power users.

4. **[#2109 — Model name forced to lowercase](Hmbown/CodeWhale Issue #2109)**  
   *0 comments / OPEN*  
   Inputting `DeepSeek-V4-Flash` is silently lowercased to `deepseek-v4-flash`, rendering the model unusable for providers that enforce exact casing. A trust-eroding transparency bug.

5. **[#1773 — TUI hangs on WSL2 without X server](Hmbown/CodeWhale Issue #1773)**  
   *0 comments / CLOSED*  
   The `arboard` clipboard crate blocks on a Unix socket indefinitely when no X11 server is running (headless / WSL2 without WSLg). Users face a completely blank TUI with no error path.

6. **[#1186 — Typed persistent permission rules](Hmbown/CodeWhale Issue #1186)**  
   *3 comments / OPEN*  
   A community-proposed enhancement to extend the execution policy layer with scoped, typed rules (`allow`, `deny`, `ask`) based on tool name, command prefix, or workspace path. High-value security UX.

7. **[#2038 — Cost and timing display resets aggressively](Hmbown/CodeWhale Issue #2038)**  
   *2 comments / CLOSED*  
   Users cannot track cumulative session cost or confirm that prefix caching is working. The per-turn reset undermines usage visibility.

8. **[#2039 — Shell execution causes UI freeze](Hmbown/CodeWhale Issue #2039)**  
   *1 comment / CLOSED*  
   During long builds or test suites, the TUI lacks any progress indicator or heartbeat, leaving users "anxious and pressing keys they shouldn't."

9. **[#2018 — Low-information rows should be inspectable/clickable](Hmbown/CodeWhale Issue #2018)**  
   *2 comments / OPEN*  
   Agent and task panels truncate critical information without affordances to expand. A core UX refinement for v0.8.45.

10. **[#2089 — Configurable path suffix for OpenAI-compatible endpoints](Hmbown/CodeWhale Issue #2089)**  
    *0 comments / OPEN*  
    Third-party proxies often reject `/v1/chat/completions` and require `/chat/completions`. Adding a configurable `path_suffix` unblocks self-hosted and lightweight gateway setups.

---

## 4. Key PR Progress

*Data source: [Hmbown/CodeWhale Pull Requests](Hmbown/CodeWhale PR #...)*

1. **[#2118 — Prepare v0.8.45 release](Hmbown/CodeWhale PR #2118)**  
   The main release preparation branch, gathering RLM recovery sessions, the `/balance` command, cancellable tools, and deterministic whale-species naming for sub-agents.

2. **[#2105 — Fix Homebrew binaries for rebrand](Hmbown/CodeWhale PR #2105)**  
   Directly addresses #2104 by ensuring the `codewhale` binary is properly installed by the Homebrew formula alongside the legacy forwarding shims.

3. **[#1790 — Wrap `file_search` in `spawn_blocking` with 30s timeout](Hmbown/CodeWhale PR #1790)** *(Closed)*  
   Prevents the synchronous directory walker from blocking the engine loop entirely, keeping cancellation responsive during deep directory searches.

4. **[#1686 — Preserve all tool_calls in OpenAI batch streaming responses](Hmbown/CodeWhale PR #1686)** *(Closed)*  
   Fixes a critical bug where multiple tool calls in a single streaming response from OpenAI-compatible backends (vLLM, Ollama, Together) would silently drop all but the final call.

5. **[#1856 — Replace `RwLock` with `Semaphore` in tool runtime](Hmbown/CodeWhale PR #1856)**  
   Eliminates a re-entrant deadlock scenario in `ToolCallRuntime` where serial tools block parallel tools, while preventing tools from deadlocking on themselves.

6. **[#2062 — Persist permission rules from approval prompts](Hmbown/CodeWhale PR #2062)**  
   A highly anticipated community feature: users can now save typed `allow` / `deny` rules directly from tool approval dialogs, with a preview of the rule that will be written to user config.

7. **[#2113 — Independent scroll regions for conversation and tool output](Hmbown/CodeWhale PR #2113)**  
   Splits the chat area into two scroll zones (transcript and tool output) with independent state, mouse wheel support, and separate caches. A major UX upgrade.

8. **[#2111 — Embed user prompt in snapshot labels for readable `/restore`](Hmbown/CodeWhale PR #2111)**  
   Resubmitted from #1798. Replaces opaque `pre-turn:1` snapshot labels with the first line of the user prompt (truncated). Makes session recovery navigable.

9. **[#2102 — Defer low-value native tools by default](Hmbown/CodeWhale PR #2102)**  
   Native tools outside the core catalog are now deferred until explicitly referenced. Adds `[tools] always_load` config for opt-in, reducing startup latency.

10. **[#2101 — Model family identity palettes](Hmbown/CodeWhale PR #2101)**  
    Adds deterministic, exported `ModelFamily` APIs and family-specific color palettes (DeepSeek, Anthropic, OpenAI, Google, etc.) visible in the TUI header model label.

---

## 5. Feature Request Trends

Across all open and closed issues, the community is driving CodeWhale unmistakably toward becoming a **multi-provider, cross-platform agentic IDE**:

- **Agentic Control & Recovery**  
  The "Control Plane" / "Hunt" vocabulary dominates (#1879, #2092, #2093, #2094). Users want interruptible, rewinding agent runs with formal verdict states (`hunting`, `hunted`, `escaped`). This is the single most coordinated feature direction.

- **Multi-Provider & Model Catalogs**  
  A sustained push for a **cross-provider model registry** (`codewhale models --all`), a provider-hardening pack adding Groq/Cerebras/Together/DeepInfra (#2087), flexible endpoint path suffixes (#2089), and per-provider billing queries (#2019).

- **Localization & Language Access**  
  The new "Whale-school" initiative (#2090, #2091) is the fastest-growing feature set. Proposals include hover translation cards for sub-agent names, pinned vocabulary drill panels, and full UI localization. Indicates a strong non-English / polyglot user base.

- **Voice Input**  
  Prototyped in v0.8.45 but pulled. Issues #2115 and #2116 track the full cross-platform, terminal-safe design for v0.8.46, acknowledging that Cmd-K is commonly captured by terminal emulators.

- **Session Context & Persistence**  
  Demand is emerging for non-linear session trees (`parent_entry_id` on the message table, #2082), engine-level turn budgeting (#2083), and meaningful snapshot metadata (#2111).

---

## 6. Developer Pain Points

- **Rebranding Migration Friction**  
  The rename to CodeWhale shipped with incomplete Homebrew formula updates (#2104) and binary path confusion. Several cycles were needed to stabilize the basic `brew upgrade` path. User trust in "update and it just works" took a measurable hit.

- **Configuration Transparency Failures**  
  Two "silent override" bugs—environment variables bypassing profile configurations (#2114) and model names being lowercased without warning (#2109)—are eroding confidence in the config layer. These were called out as "trust-eroding" by community members.

- **Long-Running Command UX**  
  The TUI lacks any progress heartbeat during long-running shell operations (#2039). Users repeatedly report "idle" or "frozen" states during builds, test suites, or deployments. This is the single most reproducible daily-driver frustration.

- **Cross-Platform Gaps**  
  WSL2 headless hangs (#1773) and Windows terminal mouse capture interference (#2103) highlight that the terminal layer still has gaps outside macOS/Linux with desktop environments.

- **Cost & Resource Anxiety**  
  The aggressive resetting of cost and timing displays (#2038) actively prevents users from developing good usage habits or monitoring spending. Users want persistent telemetry, not per-turn resets.

- **Docker Onboarding Instability**  
  The garbled output issue (#1615) accumulated 188 comments, making it the largest single discussion thread in the tracker. This indicates the container-first onboarding experience needs fundamental re-architecture, not just patch fixes.

---

*Stay up to date at [github.com/Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*