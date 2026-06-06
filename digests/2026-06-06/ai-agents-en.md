# OpenClaw Ecosystem Digest 2026-06-06

> Issues: 469 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-06 02:50 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-06

## 1. Today's Overview
The OpenClaw project is operating at an extremely high velocity, with **469 issues** and **500 pull requests** receiving updates in the last 24 hours. Maintainers are keeping pace, successfully closing 132 issues and merging/landing 137 PRs today. However, the activity reveals a project under significant stabilization pressure, as a large portion of community submissions revolve around regressions introduced in the recent v5.x and v6.x release chains. No new releases were cut today, suggesting the team is focused on a hotfix cycle for the 2026.6.1 release, balancing rapid feature development around MCP security and multi-agent scenarios with the stability demands of a mission-critical AI agent platform.

## 2. Releases
*No new releases were published today.*

## 3. Project Progress
The ClawSweeper automation framework has been central to accelerating the merge pipeline today, auto-merging critical patches to keep the main branch healthy.

**Stability Fixes Landed:**
- **macOS node-mode reconnection loop** — PR [#90815](https://github.com/openclaw/openclaw/pull/90815) and [#90736](https://github.com/openclaw/openclaw/pull/90736) address a TLS-pinning WebSocket session rebuild loop (#90668) in healthy direct gateway sessions.
- **Memory status identity check** — PR [#90816](https://github.com/openclaw/openclaw/pull/90816) and [#90748](https://github.com/openclaw/openclaw/pull/90748) fix the `memory status` command always printing a blank "expected" model field, making `memory_search` tool calls fail after a successful `memory index --force`.
- **Auto-compaction race condition** — PR [#90773](https://github.com/openclaw/openclaw/pull/90773) resolves an owned-write publication gap in the embedded prompt-lock path when `SessionManager` appends session JSONL entries during provider streaming.

**Feature Foundation:**
- **Sub-agent tool allowlist** — PR [#78441](https://github.com/openclaw/openclaw/pull/78441) (size L, ready for maintainer review) adds optional `toolsAllow` to `sessions_spawn`, enabling native embedded sub-agent tool isolation without overexposing the full tool catalog.

**Diagnostics Improvements:**
- Memory pressure logs are now operator-actionable with units, percentage thresholds, and guidance ([#90797](https://github.com/openclaw/openclaw/pull/90797)).
- Codex completion timeout diagnostics now surface structured failure details ([#90820](https://github.com/openclaw/openclaw/pull/90820)).
- The TUI `/models` command now emits "loading models" feedback before the slow catalog discovery resolves ([#90826](https://github.com/openclaw/openclaw/pull/90826)).

## 4. Community Hot Topics
The most active discussions reveal a community deeply engaged with both urgent regressions and strategic feature design.

- **Regression anxiety remains the top concern.** The issue "[Bug]: Coding Agent never completes anything" ([#62505](https://github.com/openclaw/openclaw/issues/62505), 14 comments) remains a P1 functional breakdown for a core use case since 2026.4.2. The "High CPU, extreme control-plane RPC latency" issue ([#76562](https://github.com/openclaw/openclaw/issues/76562), 13 comments, 5 👍) indicates systemic performance problems introduced in the 2026.4.29/2026.5.2 release chain. A fix is in progress via PR [#90819](https://github.com/openclaw/openclaw/pull/90819).

- **OpenAI provider friction is a recurring theme.** The upgrade to 2026.6.1 broke OpenAI ChatGPT Responses for `gpt-5.4/gpt-5.5` ([#90083](https://github.com/openclaw/openclaw/issues/90083), 12 comments, 3 👍, P1), while native replay sessions fail with `invalid_encrypted_content` on subsequent turns ([#90093](https://github.com/openclaw/openclaw/issues/90093), 8 comments).

- **MCP consent envelopes** — Feature request [#78308](https://github.com/openclaw/openclaw/issues/78308) (12 comments, 1 👍) continues to gather momentum, asking for the same `/approve <id>` pipeline that gates shell-exec to be extended to MCP tool calls. This signals a strong user demand for security-by-design in tool execution.

- **Per-agent knowledge isolation** — Issue [#63829](https://github.com/openclaw/openclaw/issues/63829) (9 comments, 9 👍) remains the highest-voted open feature request. Users need separate memory-wiki vaults per agent in multi-agent setups rather than a single global vault.

- **Matrix channel dispatch broken on v2026.6.1** — The crash reported in [#90325](https://github.com/openclaw/openclaw/issues/90325) (5 comments, 2 👍) is drawing attention as a regression confirmed across versions 2026.5.27 through 2026.6.1.

## 5. Bugs & Stability
Stability dominates today's data, with a heavy concentration of P1 regressions and data integrity issues.

**Critical Regressions (P1/P0):**

| Issue | Summary | Status |
|---|---|---|
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent never completes anything (Regression post-2026.4.2) | OPEN |
| [#90083](https://github.com/openclaw/openclaw/issues/90083) | OpenAI ChatGPT Responses transport fails `invalid_provider_content_type` for gpt-5.4/5.5 on 2026.6.1 | OPEN |
| [#90325](https://github.com/openclaw/openclaw/issues/90325) | Matrix channel handler crashes with `TypeError: Cannot read properties of undefined` on 2026.6.1 | OPEN |
| [#87756](https://github.com/openclaw/openclaw/issues/87756) | Prompt-launched Lobster workflow hangs on nested `/tools/invoke` (Regression) | OPEN |
| [#77012](https://github.com/openclaw/openclaw/issues/77012) | WebChat session transcript overwritten every turn (5.2 regression — SessionManager removal) | OPEN |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) | High CPU, extreme control-plane RPC latency (2026.4.29/5.2 regression) — Fix PR #90819 open | OPEN |
| [#90072](https://github.com/openclaw/openclaw/issues/90072) | Cron state silently wiped during SQLite migration on upgrade to 2026.6.1 | CLOSED |

**Data Integrity & State Corruption:**
- **Memory-core dreaming** is sourcing session-corpus files from deleted `.jsonl.deleted.*` paths, and the narrative phase writes placeholder fallbacks despite valid prose responses ([#90466](https://github.com/openclaw/openclaw/issues/90466)).
- **In-progress replies swallowed** by heartbeat/system events in Telegram topic sessions ([#64810](https://github.com/openclaw/openclaw/issues/64810)).
- **Recovery chain fragility** — Aborted runs leave unstable next-turn state ([#62322](https://github.com/openclaw/openclaw/issues/62322)), and sub-agent timeout recovery creates duplicate API posts ([#37446](https://github.com/openclaw/openclaw/issues/37446)).

**Channel & Platform Bugs:**
- **Feishu:** Streaming card truncated to last character with abnormal typewriter effect ([#88929](https://github.com/openclaw/openclaw/issues/88929)); config validation fails on upgrade from v4.5 to v4.8 ([#63101](https://github.com/openclaw/openclaw/issues/63101)).
- **macOS:** launchd plist `StandardErrorPath` hardcoded to `/dev/null`, hiding all gateway stderr since 5.28 ([#90711](https://github.com/openclaw/openclaw/issues/90711)).
- **Inbound reactions not triggering agent turns** on Telegram despite `triggerAgentTurn: true` ([#64752](https://github.com/openclaw/openclaw/issues/64752), CLOSED).

**Security & Auth:**
- **Codex OAuth refresh lockdown** can wedge agents for hours without clear alerting or profile rotation ([#86215](https://github.com/openclaw/openclaw/issues/86215)).
- **Agent internal thinking exposed** to end users across multiple models ([#64267](https://github.com/openclaw/openclaw/issues/64267)).
- **`message.send` schema overexposure** causing GPT models to auto-populate poll/components/modal fields, leading to runtime validation failures ([#43015](https://github.com/openclaw/openclaw/issues/43015)).

## 6. Feature Requests & Roadmap Signals

**Likely Imminent (Next Release Cycle):**
- **MCP Consent Envelopes** ([#78308](https://github.com/openclaw/openclaw/issues/78308)) — The momentum behind channel-mediated approval for MCP tool calls is the strongest signal in the feature pipeline. Current Codex and shell-exec approval patterns provide a clear implementation path.
- **Sub-agent Tool Isolation** — PR [#78441](https://github.com/openclaw/openclaw/pull/78441) directly implements `toolsAllow` forwarding to `sessions_spawn`. This addresses the critical gap where MCP tools are not injected into subagent sessions ([#85030](https://github.com/openclaw/openclaw/issues/85030), [#45269](https://github.com/openclaw/openclaw/issues/45269)).

**Medium-Term Roadmap Signals:**
- **Context Window Economy** — The "Tiered bootstrap file loading" proposal ([#22438](https://github.com/openclaw/openclaw/issues/22438)) and the "Reduce tool schema token overhead" task ([#14785](https://github.com/openclaw/openclaw/issues/14785)) signal a strategic push to enable power users with large workspaces to manage token budgets efficiently.
- **Session Governance** — Demand for hard session limits (`maxDurationMinutes`, `maxTokensPerSession`, [#64463](https://github.com/openclaw/openclaw/issues/64463)) and raw message retention that survives compaction/resets ([#58818](https://github.com/openclaw/openclaw/issues/58818)) indicates users need circuit breakers and continuity guarantees for production deployments.
- **Model Fallback Chains** — The discovery that fallback chains are not triggered on provider-wide quota exhaustion ([#85103](https://github.com/openclaw/openclaw/issues/85103)) will likely drive improvements to the provider resilience layer.

**Stalled Features Pending Decision:**
- **Per-agent memory-wiki vaults** ([#63829](https://github.com/openclaw/openclaw/issues/63829), 9 👍) — The highest-voted feature request remains in limbo awaiting product decision and security review.
- **Discord permission overhaul** ([#69748](https://github.com/openclaw/openclaw/issues/69748)) — Proposal for role-based bypass/mention/deny lists with per-channel overrides has been awaiting triage since April.
- **WebChat UI customization** ([#90246](https://github.com/openclaw/openclaw/issues/90246)) — Users want the ability to hide/collapse the Workspace/Files rail; only 1 day old but already has 2 👍.

## 7. User Feedback Summary

**Upgrade Fatigue Is Tangible.** The consistent emergence of regressions with minor version bumps (2026.4.2 → 4.15 → 5.2 → 6.1) is eroding user confidence. The silent wiping of 44/45 cron jobs during SQLite migration ([#90072](https://github.com/openclaw/openclaw/issues/90072)) was particularly damaging to trust in the migration process.

**"Just Works" Expectations vs. Reality.** Users express frustration that the platform requires constant monitoring to maintain core functionality:
- Provider auth failures (Codex OAuth wedges, [#86215](https://github.com/openclaw/openclaw/issues/86215)) require operator intervention.
- Media understanding models are guessed rather than exposed as runtime telemetry ([#62924](https://github.com/openclaw/openclaw/issues/62924)), reducing transparency.
- Model fallback chains fail silently on provider quota exhaustion ([#85103](https://github.com/openclaw/openclaw/issues/85103)).

**Channel Parity Gaps.** Users on non-core platforms (Matrix, Feishu, Synology Chat) feel their experience is degraded. Matrix crashes on v2026.6.1 ([#90325](https://github.com/openclaw/openclaw/issues/90325)), Feishu streaming is broken ([#88929](https://github.com/openclaw/openclaw/issues/88929)), and basic features like voice messages on Matrix ([#78016](https://github.com/openclaw/openclaw/issues/78016), CLOSED) are lagging.

**Maturing Community Expectations.** The user base is evolving from individual hobbyists to power users and operators deploying multi-agent systems. They are requesting:
- Per-agent isolation (vaults, tool allowlists, memory separation)
- Session cost controls and circuit breakers
- Secure, auditable tool execution pipelines
- Transparent, diagnosable provider failure modes

## 8. Backlog Watch
Several high-value features and fixes remain open despite their strategic importance to the project's roadmap:

| Issue | Priority | Age | Reason for Stalling |
|---|---|---|---|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) — Per-agent memory-wiki vault | P1 | 2026-04-09 (2 months) | Awaiting product decision + security review. Highest-voted open feature (9 👍). |
| [#14785](https://github.com/openclaw/openclaw/issues/14785) — Reduce tool schema token overhead (~3,500 tok/session) | P2 | 2026-02-12 (4 months) | Awaiting maintainer review + product decision. Affects every single session. |
| [#58730](https://github.com/openclaw/openclaw/issues/58730) — exec() sandbox isolation and tool permission model | P1 | 2026-04-01 (2 months) | Needs maintainer review, product decision, and security review despite being inspired by a real information leak. |
| [#58818](https://github.com/openclaw/openclaw/issues/58818) — Guarantee last N raw messages in agent context | P2 | 2026-04-01 (2 months) | Needs product decision + security review. Solves the fundamental problem of agents losing context after compaction/reset. |
| [#69748](https://github.com/openclaw/openclaw/issues/69748) — Discord permission overhaul (roles, deny/allow lists) | P2 | 2026-04-21 (6 weeks) | Needs product decision + security review. Long-standing pain point for Discord users. |
| [#61009](https://github.com/openclaw/openclaw/issues/61009) — docs/tools/exec contradicts runtime behavior on `host=node` | P2 | 2026-04-04 (2 months) | Stale; needs security review + linked PR attention. Documentation vs. implementation mismatch. |

The concentration of `clawsweeper:needs-product-decision` and `clawsweeper:needs-maintainer-review` labels on these items suggests that while the automation pipeline for merging simple fixes is strong, the strategic product decision-making loop for larger features and security redesigns is a bottleneck in the project's throughput.

---

## Cross-Ecosystem Comparison

## Cross-Project Ecosystem Comparison Report — 2026-06-06

### 1. Ecosystem Overview

The personal AI agent open-source landscape demonstrated exceptional velocity on June 6, 2026, but with a stark divergence between feature expansion and platform stability. The ecosystem is undergoing an adolescent growth phase: the largest projects (OpenClaw, IronClaw, ZeroClaw) are deep in architectural migrations and grappling with regression fatigue, while emerging contenders (Hermes Agent, NanoBot, LobsterAI) are capturing users by combining responsive development with higher baseline reliability. A universal pivot toward enterprise-grade concerns—multi-agent isolation, MCP-level security governance, provider resilience, and cost management—dominates the roadmap signals across every actively developed project. Meanwhile, the CJK market has emerged as a primary driver, with i18n quality and domestic channel integration (WeCom, DingTalk, Feishu, Yuanbao) acting as barometers of project maturity rather than differentiators.

---

### 2. Activity Comparison Table

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score & Signal |
|---|---|---|---|---|
| **OpenClaw** | 469 | 500 | Hotfix cycle (no release) | **Fair** — Unmatched volume, but P1 regressions eroding trust (v5.x/v6.x chains). |
| **NanoBot** | 11 | 28 | No release | **Excellent** — Rapid bug turnaround, high community PR quality, responsive maintainers. |
| **Hermes Agent** | 50 | 50 | v0.16.0 “The Surface” (Jun 5) | **Good** — Strong post-launch stabilization; CJK UX pain points remain. |
| **PicoClaw** | 6 | 22 | v0.2.9-nightly | **Excellent** — Panic-grade bugs resolved same-day. Stability-first execution. |
| **NanoClaw** | 0 | 3 (2 merged) | No releases | **Stable** — Clean backlog, focused incremental hardening. |
| **NullClaw** | 0 | 1 (open) | No releases | **Dormant** — Single provider PR, zero defect activity. |
| **IronClaw** | 13 | 50 | Stalled (PR #3708, 21 days) | **Fair (High Risk)** — Massive Reborn churn; CI broken for 10 days blind spot. |
| **LobsterAI** | 3 (stale) | 12 (all merged) | v2026.6.5 | **Excellent** — Feature output + critical security patches landed cleanly. |
| **Moltis** | 4 | 5 | No release | **Good** — Measured iteration; 48-hour fix cycle for Telegram regression. |
| **CoPaw (QwenPaw)** | 20 | 16 | No release | **Fair (Concerning)** — Active community undermined by P0 memory leaks and agent loops. |
| **TinyClaw** | 0 | 0 | — | **Dormant** — No activity. |
| **ZeptoClaw** | 0 | 0 | — | **Dormant** — No activity. |
| **ZeroClaw** | 50 | 50 | No release (v0.9.0 prep) | **Good (Scaling)** — Strong RFC-driven roadmap; triage bottleneck on community contributions. |

---

### 3. OpenClaw’s Position

OpenClaw remains the gravitational center of the ecosystem, operating at a volume (469 issues, 500 PRs daily) that dwarfs every other project by an order of magnitude. Its primary advantage is **ecosystem completeness**—deepest MCP integration, largest contributor pipeline, and broadest platform support. The ClawSweeper automation pipeline enables an unparalleled merge velocity.

However, this scale comes with a structural vulnerability: **regression opacity**. The consistent emergence of P1 breakages across minor version bumps (2026.4.2 → 6.1) has created a trust deficit among power users. Competitors are explicitly benefiting from this—NanoBot’s responsive bug turnaround and Hermes Agent’s polished v0.16.0 launch offer “just works” alternatives.

Technically, OpenClaw’s monolith architecture contrasts with ZeroClaw’s pluggable security model and IronClaw’s Rust/backend microservices approach. The community size comparison is lopsided: OpenClaw’s daily issue count exceeds the combined total of the next five most active projects. The key bottleneck is not engineering throughput but **product decision latency**—strategic requests like per-agent vaults (#63829) and tool schema optimization (#14785) have stalled for months despite broad consensus.

---

### 4. Shared Technical Focus Areas

**Security & Tool Governance** (Universal)
- **MCP consent envelopes:** OpenClaw (#78308), PicoClaw (exec guard, #1042), ZeroClaw (shell confirmation tiers, #7155)
- **Permission isolation:** OpenClaw (sub-agent allowlist, #78441), IronClaw (cross-tenant leakage fix), ZeroClaw (allowed_tools enforcement, #6914), CoPaw (WriteFileOverwriteGuardian)
- **Secret redaction/audit:** Hermes Agent (#40139), ZeroClaw (nested secret redaction, #7261), LobsterAI (IPC allowlist, #1535)

**Multi-Agent & Session Architecture**
- **Cross-agent communication:** NanoBot (PR #3992 — cross-agent message bus), Hermes Agent (ToolCallStormBreaker, #35573)
- **Memory/context isolation:** OpenClaw (per-agent vaults, #63829), ZeroClaw (routing control, #6969), PicoClaw (context compression display, #2968)
- **Session governance & circuit breakers:** OpenClaw (maxDurationMinutes, #64463), Moltis (tool result caps, #1089)

**CJK Platform Parity**
- **i18n desktop UI:** Hermes Agent (Japanese/Traditional Chinese desktop, #40114), LobsterAI (implicit)
- **Messaging channel integration:** CoPaw (Yuanbao fixes), IronClaw (WeCom group approval, #4502), OpenClaw (Feishu streaming, #88929), Moltis (Telegram streaming)
- **Provider compatibility:** CoPaw (DeepSeek thinking block, #4962), Hermes Agent (Anthropic dots→hyphens, #22196)

**Reliability Engineering**
- **Memory/data integrity:** OpenClaw (dreaming sourcing deleted paths, #90466), NanoBot (session message drop, #4203), PicoClaw (JSONL metadata crash consistency, #2907)
- **Provider resilience:** IronClaw (budget governance misclassification, #4311), NanoClaw (5xx silent failures, #2692), OpenClaw (fallback chains on quota exhaustion, #85103)

---

### 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | NanoBot | IronClaw | ZeroClaw | LobsterAI | CoPaw |
|---|---|---|---|---|---|---|---|
| **Target User** | Enterprise Ops / Platform Teams | Power Users / Developers | Developers / Enthusiasts | Enterprise Backend | Enterprise Sec/Ops | Consumer Desktop | AI Workbench Users |
| **Architecture** | Node.js Monolith + SDKs | Electron / Rust / Python | Python SDK-first | Rust / Microservices | Pluggable Provider Model | Electron / React (Desktop) | Python / Tauri |
| **Core Innovation** | MCP ecosystem, Sub-agent orchestration | Agent learning loop (Skill+Memory+Search) | Cross-agent bus, Desktop shell polish | Hook framework, Reborn API facade | Pluggable Security & Observability | Artifacts workspace, Monetization engine | Browser automation, Cron execution |
| **Primary Vulnerability** | Regression fatigue from high velocity | CJK input gaps, Intel Mac lockout | Small team relative to ambition | CI blind spot during Reborn | Triage bottleneck on community RFCs | Stale UX bug backlog (2 months) | P0 memory leaks, infinite loops |

**Key insight:** The ecosystem is bifurcating into two distinct markets. **Enterprise Orchestrators** (OpenClaw, IronClaw, ZeroClaw) compete on RBAC, governance, gateway resilience, and API compatibility. **Desktop AI Apps** (Hermes Agent, LobsterAI, CoPaw) compete on UX polish, artifact workflows, i18n quality, and local execution. NanoBot and Moltis occupy a middle ground, prioritizing modularity and self-hosting flexibility.

---

### 6. Community Momentum & Maturity

**Tier 1: Sprinting with Structural Strain**
- **OpenClaw** — Largest community by far, but regression anxiety is the dominant sentiment. Users explicitly express upgrade fatigue and trust erosion (e.g., silent cron state wipe, #90072).
- **IronClaw** — Immense architectural velocity (Reborn) with significant operational risk. 10 days of broken nightly CI represents a critical quality blind spot. The stalled release PR (#3708, 21 days) suggests internal disagreement about readiness.
- **ZeroClaw** — RFC-driven growth with heavy engagement on governance (#6808) and security (#7142). Triage capacity is trailing contribution volume, risking contributor churn.

**Tier 2: High-Velocity, Productive Iteration**
- **Hermes Agent** — Post-launch stabilization phase is going well. 20 PRs merged/closed today. The “skill + memory + session_search” design is generating genuine user delight (#40251). CJK pain points are the primary friction vector.
- **NanoBot** — Exceptional community health. Maintainers closed bugs on the day of filing (#4200, #4197). 28 PRs updated, high first-time contributor quality. Cross-agent bus (#3992) is the most ambitious roadmap item.
- **LobsterAI** — Strong security posture (rapid patching of API proxy leaks, IPC exposure). 12 PRs merged cleanly. Stable UX bugs (draft persistence, #1471/#1472) are the main drag on an otherwise healthy project.

**Tier 3: Niche Stability Setters**
- **PicoClaw** — Best-in-class stability SLA. Multiple panic-grade bugs patched in a single day. Excellent for users who prioritize reliability over breadth.
- **Moltis** — Measured, healthy iteration. 48-hour Telegram fix turnaround is best-in-class for channel responsiveness. Container sandboxing focus is a clear differentiator.
- **NanoClaw** — Cleanest backlog in the ecosystem. Zero open issues. Focused on incremental hardening. Ideal for SDK-level usage.

**Tier 4: Dormant**
- **NullClaw, TinyClaw, ZeptoClaw** — No meaningful community activity. May represent maintained tools or personal projects without active adoption.

---

### 7. Trend Signals

**1. Security is the decisive competitive axis.** The universal demand for MCP consent envelopes, tool allowlists, secret redaction, and audit trails is the clearest signal for the second half of 2026. Projects that fail to ship robust permission models (OpenClaw’s stalled #78308, IronClaw’s hook framework maturity) will lose enterprise traction to those that do (ZeroClaw’s Pluggable Security Provider, LobsterAI’s IPC hardening).

**2. Multi-agent isolation is table stakes.** Users deploying multi-agent setups demand per-agent memory vaults (OpenClaw #63829 is the highest-voted open feature), tool isolation (OpenClaw #78441), and context circuit breakers. NanoBot’s cross-agent bus (#3992) and Hermes’ ToolCallStormBreaker (#35573) signal that this is the next major architectural battleground.

**3. CJK market is a primary adoption driver, not an afterthought.** i18n quality, domestic LLM compatibility (DeepSeek, Yuanbao, Volcengine), and messaging platform support (WeCom, Feishu, QQ, DingTalk) are core requirements for sustained growth. Hermes Agent and CoPaw are making strategic investments here; OpenClaw’s regressions on Matrix/Feishu are bleeding community trust.

**4. Provider aggregation is commoditizing. Resilience is the new differentiator.** All major projects support OpenAI-compatible endpoints. The value is shifting to *how* the system fails: intelligent fallback chains (IronClaw #4311, OpenClaw #85103), graceful degradation on quota exhaustion (PicoClaw #2905), and transparent failure diagnostics (NanoClaw #2692).

**5. Desktop and IDE integration is the new growth vector.** Requests for XCode MCP bridges (ZeroClaw #6065), embedded WebUIs (ZeroClaw, Hermes Agent), and artifact/workspace systems (LobsterAI #2114, CoPaw) indicate that the chat window is no longer sufficient. The AI agent is becoming a persistent operating system layer, not a conversational tool.

**6. The “Two-Market” hypothesis is validating.** *Enterprise Orchestrators* will win on governance, audit, and API gateways (IronClaw, ZeroClaw, OpenClaw). *Desktop AI Apps* will win on design, i18n, and local-first experiences (Hermes Agent, LobsterAI, CoPaw). NanoBot and Moltis are positioned to bridge both if they maintain their modularity and reliability advantages.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 6, 2026.

---

## NanoBot Project Digest — 2026-06-06

### 1. Today’s Overview

NanoBot is experiencing a surge of community-driven development today. While no new official release was tagged, the repository saw an exceptional volume of activity: **11 issues** and **28 pull requests** were updated in the last 24 hours. The maintainers and contributors are focusing on two major fronts simultaneously—shoring up stability (SDK shutdown lifecycle, session message integrity, provider compatibility) and landing transformative features (cross-agent messaging, a polished desktop shell, new search providers). The velocity and quality of submissions indicate a project in a very healthy state with a growing ecosystem of power users and enterprise adopters.

### 2. Releases

**None.** No new versions were released today.

### 3. Project Progress

A total of **11 PRs** were merged or closed today. The completed work includes a mix of urgent fixes and quality-of-life features:

- **Fixed:** Desktop restart token and WebSocket replay gaps (PR #4210).
- **Fixed:** DM pairing regression on Weixin and Telegram channels (PR #4197).
- **Feature:** New `/skill` slash command that lists only enabled skills, addressing the confusion reported in Issue #3959 (PR #3968).

*Notable newly opened PRs (submitted today, not yet merged):*

- **SDK stability fix** for MCP connection shutdown errors (PR #4216, fixing #4211).
- **Session integrity fix** for orphan tool results discarding all messages (PR #4215, fixing #4203).
- **New search provider:** Added support for Exa as a web search backend (PR #4213).
- **Desktop shell** polish with shared WebUI surfaces, gateway APIs for file preview, and automation (PR #4195).
- **Cross-agent message bus** enabling multiple NanoBot instances to communicate via a shared protocol (PR #3992).
- **WebUI UX:** “fork-from-here” support with per-chat composer prefill isolation (PR #4208).
- **Tool-call validation hardening:** Near-miss tool names now explicitly error instead of silently guessing (PR #4190).
- **Drop of Python 3.11/3.12 support** to align CI with actual testing on 3.13/3.14 (PR #4207).

### 4. Community Hot Topics

The most active and reacted-to items reveal a community that deeply cares about provider interoperability and session reliability.

- **GitHub Copilot Login Failure (#2573) — 9 👍, 4 comments**  
  This closed issue received the strongest reaction of any item today. Users identified a regression after switching from `litellm` to a direct OpenAI client. The high reaction count signals that GitHub Copilot integration is a heavily desired provider path.  
  *URL: HKUDS/nanobot Issue #2573*

- **`/skill` listing disabled skills (#3959) — 4 comments**  
  A straightforward bug where the original `/skill` command didn’t respect the `disabledSkills` config. The discussion led directly to a dedicated slash command (PR #3968), showing the maintainers’ responsive approach to UX feedback.  
  *URL: HKUDS/nanobot Issue #3959*

- **History reinforcement as broad facts (#4212) — detailed technical analysis**  
  A new, deeply considered issue from an advanced user analyzing how the consolidator and summarizer loop back into the system prompt, potentially reinforcing unconfirmed inferences. This demonstrates a sophisticated user base engaging directly with the project’s core memory architecture.  
  *URL: HKUDS/nanobot Issue #4212*

### 5. Bugs & Stability

**Critical**

- **SDK MCP connection leak (#4211)** — Using the SDK with a stdio MCP server triggers a `RuntimeError: Attempted to exit cancel scope in a different task` at shutdown. Immediately addressed by PR #4216.  
  *URL: HKUDS/nanobot Issue #4211*

- **Session message silent drop (#4203)** — The `find_legal_message_start` function contains a logic flaw where an orphan tool result after a user message causes the entire message window to be discarded. A precise fix is proposed in PR #4215.  
  *URL: HKUDS/nanobot Issue #4203*

**High**

- **Browser refresh message loss (#4200)** — A regression causing user message loss on WebUI refresh was reported and already closed today.  
  *URL: HKUDS/nanobot Issue #4200*

- **Weixin/Telegram DM broken (#4197)** — Denied private senders were not properly routed through the pairing flow. Fix merged today.  
  *URL: HKUDS/nanobot PR #4197*

**Medium / Long-standing**

- **Matrix test error on `main` (#1946)** — Open since March, this test failure continues to affect developers branching from main. No fix has materialized.  
  *URL: HKUDS/nanobot Issue #1946*

- **Tool-call validation weakness (PR #4190)** — A submitted fix aims to prevent silent execution of near-miss tool names, changing the behavior to explicit errors with suggestions.

### 6. Feature Requests & Roadmap Signals

Today’s PRs and issues offer a clear view of the upcoming roadmap:

- **Multi-agent architecture** is the headline story. PR #3992 (cross-agent message bus) is the largest structural change in the queue and suggests the project is preparing for agent-to-agent communication workflows.
- **Desktop as a first-class surface** is close to landing. PR #4195 adds a desktop host, shared WebUI chat and settings surfaces, and the gateway APIs needed for a self-contained desktop experience.
- **Extensibility** is a dominant community theme:
    - Custom image generation providers (issues #4132, #4196)
    - Configurable subagent error handling (`fail_on_tool_error` context config, issue #4198)
    - `extra_query` parameter injection on provider configs to support Azure/enterprise gateways (issue #4204)
- **Enterprise channels** continue to mature. Support for DingTalk group allowlists (PR #4206) and IMAP post-actions for email (PR #4170) are both in active review.

**Prediction for next release:** Expect the inclusion of the Exa search provider (#4213), the `/skill` command (#3968), the fork-from-here UX feature (#4208), and the critical session/SDK stability fixes (#4215, #4216). The cross-agent and desktop PRs may require another round of review before merging.

### 7. User Feedback Summary

- **Pain Points:**  
  - Configuration and debugging of provider connections continues to be a hurdle, particularly for non-OpenAI-compatible endpoints (Volcengine, Copilot, Azure).  
  - Session history quirks (message loss, orphan tool state) are the most commonly reported operational bugs, and users are closely watching the fix PRs.

- **Use Cases:**  
  - Enterprise/devops users are pushing for gateway support (`api-version` params, custom providers).  
  - Chinese-language users are actively requesting better support for Volcengine and other domestic model providers (Issue #4196).  
  - Advanced power users are engaging directly with the agent’s internal memory pipeline (Issue #4212).

- **Satisfaction Indicators:**  
  - The rapid turnaround on bug reports (e.g., #4200, #4197 closed on the same day they were filed) demonstrates high maintainer responsiveness.  
  - The volume of high-quality community PRs (+28 today) suggests strong developer satisfaction with the project’s codebase and contributing experience.

### 8. Backlog Watch

Several important items remain open for extended periods and may need maintainer attention:

- **Matrix test failure (#1946)** — Open since **March 2026**. This prevents new contributors from cleanly testing on `main` and has acquired no proposed fix.  
  *URL: HKUDS/nanobot Issue #1946*

- **CI Pipeline PRs** — Two foundational CI improvement PRs sit idle:
  - `#1408` (unit-test workflow with coverage gate, open since March)
  - `#1284` (full CI/CD with quality checks, open since February)  
  The recent decision to drop old Python 3.11/3.12 support (PR #4207) renders some of this CI work more urgent to align testing with reality.  
  *URL: HKUDS/nanobot PR #1408* / *PR #1284*

- **Gateway CLI management (#3538)** — Adds `start`, `stop`, `restart`, and `status` commands for the gateway runtime. Open since late April with no recent activity from reviewers.  
  *URL: HKUDS/nanobot PR #3538*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-06

---

## 1. Today's Overview
Hermes Agent shows exceptional post-launch velocity, with **50 issues and 50 PRs updated** in the 24 hours following the massive **v0.16.0 "The Surface Release"** (v2026.6.5). The project is in a high-activity stabilization and localization phase: 20 PRs were merged or closed today, and a wave of community bugs is being met with rapid fix PRs. Overall project health is strong, though CJK input quality, Intel Mac support, and platform-adapter reconnection logic remain notable friction points. Internationalization (i18n) is clearly the dominant theme driving both feature requests and bug reports.

---

## 2. Releases
- **v2026.6.5 / Hermes Agent v0.16.0 — "The Surface Release"** *(June 5, 2026)*
  This is a landmark release, incorporating **874 commits** since v0.15.2, **542 merged PRs**, and **1,962 file changes**. The project closed **399 issues** (2 P0, 62 P1, 16 security-tagged) with help from **170 community contributors**.
  
  **What it means:** The release name "The Surface" implies deep rework of the Desktop app, TUI, and i18n layers. No explicit migration guide was included in the data, but given the scale, users running custom UI integrations or platform plugins should verify compatibility. The heavy focus on i18n in surrounding issues suggests major changes to locale handling.

---

## 3. Project Progress
### Merged / Closed Today
- **#40254** — `[codex] Add profile builder web flow`  
  Delivers a multi-step dashboard profile builder (model, MCP servers, skills, review).
- **#32297** — `fix(vision): don't retry non-retryable 4xx image downloads`  
  Eliminates wasteful retries of fixed 404/403 URLs in vision tools.

### Active Feature & Fix PRs in Flight
- **Internationalization:** Major i18n merge for Chinese CLI/TUI (#35277) and desktop language switching for Japanese/Traditional Chinese (#40114).
- **Critical Fixes:** Post-compression evidence fabrication (#40260), Anthropic model normalization (#40261), desktop OSC escape input leak (#40262), and ACP OAuth bearer forwarding (#40257).
- **Runtime Refinements:** Context compression re-fire prevention (#40246), async-safe URL validation across five platform adapters (#40255), and user-interrupt gateways (#39813).

---

## 4. Community Hot Topics
| Issue | Type | Comments | Core Need |
|-------|------|----------|-----------|
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | Bug (P3) | 5 | Intel Mac support — official DMG is arm64-only, blocking x86_64 users |
| [#40219](https://github.com/NousResearch/hermes-agent/issues/40219) | Feature (P3) | 4 | Japanese i18n / localization for UI and system messages |
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | Bug (P2) | 4 | QQ Bot WebSocket enters silent loop on reconnect failure |
| [#38227](https://github.com/NousResearch/hermes-agent/issues/38227) | Bug (P3) | 2 | Duplicate of #37505 — Intel Mac support confusion |
| [#40146](https://github.com/NousResearch/hermes-agent/issues/40146) | Bug (P3) | 3 | Chinese IME: voice button fails to switch to send button mid-composition |
| [#40251](https://github.com/NousResearch/hermes-agent/issues/40251) | Feedback | 0 | **User love letter:** Chinese user praises the `skill + memory + session_search` learning loop as "genius-level design" |

**Analysis:** The community is pushing hard for broader language support and fixing CJK UX pain points. The emotional engagement in #40251 indicates that the core architectural vision (skill/memory learning loop) is resonating deeply with power users.

---

## 5. Bugs & Stability
Ranked by severity; fix PRs noted where available.

**P1 (Critical)**
- **[#39886](https://github.com/NousResearch/hermes-agent/issues/39886)** — Cron scheduler context bleed into concurrent jobs. No fix PR yet.
- **[#40201](https://github.com/NousResearch/hermes-agent/issues/40201)** — Post-compression final synthesis fabricates source-backed findings. → **Fix PR [#40260](https://github.com/NousResearch/hermes-agent/pull/40260)** (adds CRITICAL EVIDENCE GUARD).

**P2 (High)**
- **[#31101](https://github.com/NousResearch/hermes-agent/issues/31101)** — QQ Bot adapter: silent loop after reconnect failure. Not yet fixed.
- **[#22196](https://github.com/NousResearch/hermes-agent/issues/22196)** — Anthropic provider normalizes dots→hyphens for *all* models, breaking third-party APIs (Xiaomi MiMo). → **Fix PR [#40261](https://github.com/NousResearch/hermes-agent/pull/40261)**.
- **[#38412](https://github.com/NousResearch/hermes-agent/issues/38412)** — Desktop Remote gateway: WebSocket always rejected (4403) for packaged Electron.
- **[#38488](https://github.com/NousResearch/hermes-agent/issues/38488)** — MCP server permanently gives up after transient backend outage.
- **[#40176](https://github.com/NousResearch/hermes-agent/issues/40176)** — Pinned Python deps with known CVEs (`urllib3 2.6.3`, `PyJWT 2.12.1`, etc.).
- **[#40139](https://github.com/NousResearch/hermes-agent/issues/40139)** — Secret redaction actively alters command execution, not just display masking.
- **[#40225](https://github.com/NousResearch/hermes-agent/issues/40225)** — Feishu card approval buttons use wrong auth gate, rejecting all DM users.
- **[#38963](https://github.com/NousResearch/hermes-agent/issues/38963)** — Desktop fails with "no git???" error on startup.

**P3 (Medium/Low)**
- [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) — Intel Mac binary missing.
- [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) — Terminal escape sequences leak into output, silently consuming first 1–3 characters.
- [#40227](https://github.com/NousResearch/hermes-agent/issues/40227) — Hindsight plugin API mismatch with `hindsight_embed` package.
- [#40226](https://github.com/NousResearch/hermes-agent/issues/40226) — Chinese IME breaks composer entirely (no submit, truncated text).

---

## 6. Feature Requests & Roadmap Signals
### Likely Landing in v0.16.1
- **Full Portuguese (pt-BR) support** ([#40239](https://github.com/NousResearch/hermes-agent/issues/40239)) — backend translations already ship.
- **Desktop Remote File Browsing** ([#40258](https://github.com/NousResearch/hermes-agent/pull/40258)) — pick and upload to remote gateway filesystem.
- **ACP OAuth Forwarding** ([#40256](https://github.com/NousResearch/hermes-agent/issues/40256), [#40257](https://github.com/NousResearch/hermes-agent/pull/40257)) — pass per-user bearer to upstream LLM providers.
- **ToolCallStormBreaker** ([#35573](https://github.com/NousResearch/hermes-agent/issues/35573)) — suppress repeated tool-call loops (RFC stage, strong design signal).

### Platform & UX Enhancements
- **Telegram clarify UX** ([#40259](https://github.com/NousResearch/hermes-agent/issues/40259)) — render choice text on buttons vs. bare numbers.
- **Gateway health exposure** ([#40199](https://github.com/NousResearch/hermes-agent/issues/40199)) — surface platform adapter health and auto-remediate stale adapters.
- **Ambient temporal awareness** ([#40252](https://github.com/NousResearch/hermes-agent/pull/40252)) — inject wall-clock time via ephemeral system prompt for time-aware agent behavior.
- **`/approvals` slash command** ([#39425](https://github.com/NousResearch/hermes-agent/issues/39425)) — full approval mode selection (`manual` / `smart` / `off`) mid-chat.

---

## 7. User Feedback Summary
### Gratitude & Growing Adoption
- **#40251**: A highly articulate Chinese user describes Hermes as "the most genius AI agent design" they have seen, specifically praising the `skill + memory + session_search` learning loop for enabling a "gradually accumulated construction" workflow. This is a strong signal that the architecture is delivering on its long-term vision.

### Key Pain Points (Requiring Priority)
- **Intel Mac Lockout**: Users on x86_64 Macs feel abandoned (#37505, #38227). This is a repeated topic with no fix PR visible.
- **CJK Input Broken**: Multiple users report Chinese IME completely breaking the desktop composer (#40145, #40146, #40226). Text truncation, missing send button, and Enter key failure create a poor experience for the entire Chinese-speaking community.
- **Remote Gateway Frustration**: Users connecting Desktop to remote backends face a gauntlet of WS rejection and config errors (#38412, #40215), making a flagship feature difficult to rely on.
- **"My agent died" scenarios**: QQ Bot and MCP users report permanent disconnect states with no recovery short of a full restart (#31101, #38488).

---

## 8. Backlog Watch
*Long-unanswered or high-impact items needing maintainer attention.*

| Issue | Created | Status | Why It Matters |
|-------|---------|--------|----------------|
| [#9553](https://github.com/NousResearch/hermes-agent/issues/9553) | Apr 14 | ✅ Open, P3 Docs | Documentation references a non-existent file in `grpo-rl-training/`. Newcomers hit this. |
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | May 23 | 🟠 Open, P2 Bug | QQ Bot platform adapter enters a silent infinite loop. No fix PR despite high severity. |
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | Jun 2 | 🔴 Open, P3 Bug | Intel Mac support request (duplicate of #38227). No response from maintainers on fallback plan. |
| [#38488](https://github.com/NousResearch/hermes-agent/issues/38488) | Jun 3 | 🔴 Open, P2 Bug | MCP server permanently disconnects after transient outage. Requires gateway resilience work. |
| [#35573](https://github.com/NousResearch/hermes-agent/issues/35573) | May 30 | 📘 Open, RFC | ToolCallStormBreaker RFC — high community interest but no implementation path yet. |

---

**Summary:** A massive release has landed, and the community is actively stress-testing its edges. The core team is responsive (fix PRs live for multiple P1/P2 bugs within hours), but long-standing platform reliability issues (QQ Bot, MCP) and the Intel Mac gap remain concerning. Internationalization is clearly the dominant vector for the next patch cycle.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-06

## 1. Today's Overview
PicoClaw saw an exceptionally active 24 hours on June 6th, with **22 Pull Requests** updated and **6 Issues** touched. The project maintainers aggressively closed out work, merging or closing **20 PRs** and **4 Issues** during this window. Activity was heavily weighted toward stability and correctness: multiple panic-grade type assertion bugs were patched, a critical OneBot message routing error was fixed, and a data-corruption edge case in the JSONL memory store was resolved. A new nightly build (`v0.2.9-nightly.20260606`) was also published. Overall project health is solid, with rapid response to incoming bug reports and a clear focus on hardening the agent runtime.

## 2. Releases
**Nightly Build: `v0.2.9-nightly.20260606.89ee8f1b`**
An automated nightly build was cut from `main` today. As is standard for nightly releases, stability is not guaranteed. No breaking changes or migration notes accompany this release. The full diff against the latest stable tag can be inspected [here](https://github.com/sipeed/picoclaw/compare/v0.2.9...main). No stable release occurred.

## 3. Project Progress
Today’s project progress was overwhelmingly driven by bug fixes and infrastructure hardening:

**Bug Fixes**
- **OneBot Group Routing Fix:** Resolved the `send_private_msg` / `send_group_msg` confusion that broke group chat replies. (PR [#3009](https://github.com/sipeed/picoclaw/pull/3009), closing Issue [#3002](https://github.com/sipeed/picoclaw/issues/3002))
- **Panic Prevention (Channels & Agent):** Added safe `ok`-checked type assertions in `toChannelHashes` and `UnsubscribeEvents` to prevent crash-on-bad-config scenarios. (PRs [#3010](https://github.com/sipeed/picoclaw/pull/3010), [#3011](https://github.com/sipeed/picoclaw/pull/3011))
- **Context Transparency:** Patched `/context` to display both the soft summarization trigger and the hard compression budget, ending user confusion reported in Issue [#2968](https://github.com/sipeed/picoclaw/issues/2968). (PR [#2985](https://github.com/sipeed/picoclaw/pull/2985))
- **JSONL Data Integrity:** Fixed a crash-consistency gap where the memory store could lose metadata state after an abrupt process termination. (PR [#2907](https://github.com/sipeed/picoclaw/pull/2907))
- **JSONL Performance Hot Path:** Eliminated costly full-index cloning on every cache hit in `ResolveSessionKey`. (PR [#2913](https://github.com/sipeed/picoclaw/pull/2913))
- **Fallback Chain:** Ensured expired request contexts stop the provider fallback chain immediately instead of wasting time on dead candidates. (PR [#2905](https://github.com/sipeed/picoclaw/pull/2905))
- **Skill-Creator Docs:** Removed references to missing helper scripts in the skill-creator guide. (PR [#3013](https://github.com/sipeed/picoclaw/pull/3013))

**Features & Improvements**
- **MiMo Provider Update:** Added `CommonModels` configuration for the MiMo provider, fixing WebUI model recommendations for multimodal workflows. (PR [#2915](https://github.com/sipeed/picoclaw/pull/2915))
- **Anthropic SDK Upgrade:** A massive dependency bump from `anthropic-sdk-go` v1.26.0 → v1.46.0, unlocking the latest Anthropic API capabilities. (PR [#2962](https://github.com/sipeed/picoclaw/pull/2962))
- **Web UI Security Hardening:** Shipped CSRF protection, path traversal validation, and security headers for the web backend. (PR [#2900](https://github.com/sipeed/picoclaw/pull/2900))
- **Provider Logo Fallbacks:** Restored logo rendering on the models config page after a prior refactor. (PR [#2908](https://github.com/sipeed/picoclaw/pull/2908))
- **Dependency Housekeeping:** Frontend deps (React, TanStack Router/Query, shadcn, Tabler Icons) and Go deps (`go.mau.fi/util`) were all bumped by Dependabot and merged.

## 4. Community Hot Topics
**Most Active Issues & Discussions**

- **[BUG] exec tool `guardCommand` false positives (Issue #1042)** — *Closed, 15 comments, 2 👍*
  *Link:* https://github.com/sipeed/picoclaw/issues/1042
  *Analysis:* The most active discussion revolves around the safety guard in the `exec` tool flagging legitimate network commands (e.g., `curl wttr.in/Beijing`) as path traversal attacks. The underlying need is clear: users want robust safety without breaking standard shell workflows. The issue was closed today, which may signal either a fix was accepted or a design decision was communicated.

- **[BUG] `/context` shows only compression threshold (Issue #2968)** — *Closed, 5 comments*
  *Link:* https://github.com/sipeed/picoclaw/issues/2968
  *Analysis:* Users configuring context windows were misled by the `/context` command, which omitted the summarization trigger threshold. The rapid resolution (resolved by PR [#2985](https://github.com/sipeed/picoclaw/pull/2985) on the same day the fix was approved) demonstrates strong maintainer responsiveness to UX feedback.

- **[BUG] Evolution Mode token drain (Issue #3012)** — *Open, 1 comment*
  *Link:* https://github.com/sipeed/picoclaw/issues/3012
  *Analysis:* Filed just today, this fresh report of continuous token consumption with Evolution Mode enabled is likely the community’s highest-priority concern. The feature is still maturing, and this runtime cost leak threatens user trust if not patched quickly.

- **[TASK] Skill-Creator audit (Issue #652)** — *Open, 3 comments*
  *Link:* https://github.com/sipeed/picoclaw/issues/652
  *Analysis:* A long-running task (opened in February) about the broken skill-creator onboarding experience. Today’s doc patch (PR [#3013](https://github.com/sipeed/picoclaw/pull/3013)) addresses the documentation side, but the underlying missing scripts and full workflow restoration remain open. New contributors are the most affected demographic.

## 5. Bugs & Stability
Ranked by severity (★ = Critical, ● = High, ◆ = Medium)

| Severity | Issue | Description | Status |
|---|---|---|---|
| ★ | #3012 | Evolution Mode consumes tokens every minute when enabled. Direct API cost impact to users. | **Open — No fix PR yet** |
| ● | #3010 / #3011 | Unchecked type assertions in channels and agent could panic on unexpected config types. | **Fixed** |
| ● | #3002 | OneBot group messages used `send_private_msg` API, breaking group chat. | **Fixed** in #3009 |
| ● | #2907 | JSONL metadata drift after crash → potential session corruption. | **Fixed** |
| ◆ | #2968 | `/context` displayed incomplete compression info, omitting summarization threshold. | **Fixed** in #2985 |
| ◆ | #2905 | Expired request contexts wasted time in fallback chain. | **Fixed** |
| ◆ | #2900 | Missing CSRF protection and path traversal validation in web backend. | **Fixed** (Hardened) |
| ◆ | #1042 | `exec` tool’s `guardCommand` regex flagged `curl` URL arguments as path traversal. | **Closed** |

**Takeaway:** The project’s stability posture improved dramatically today. Four potential panics or data-corruption vectors were eliminated. However, the **Evolution token drain (Issue #3012)** is an active critical bug that should be the maintainers’ top immediate priority.

## 6. Feature Requests & Roadmap Signals
**Strong Signals for Next Stable Release**

- **Image Input Compression (PR [#2964](https://github.com/sipeed/picoclaw/pull/2964)):** *Open / Draft.* A proposed `image_compression` pipeline to limit inbound vision payloads before model inference. Highly useful for users on token budgets or slow networks. Watch this PR for merging—it would be a natural inclusion in a v0.3.0 target.

- **Channel Identity Refactor (PR [#2551](https://github.com/sipeed/picoclaw/pull/2551)):** *Open since April.* Decouples channel names from provider types to allow multi-instance deployments of the same provider (e.g., two Slack bots). A necessary architectural evolution for enterprise-scale users, though it has gone stale.

- **Evolution Mode Refinements:** The token drain bug (#3012) signals that Evolution Mode is under heavy real-world testing. Expect imminent hotfixes or config tunables around the polling/drafting cycle.

- **Multi-Modal Momentum:** The MiMo provider update (PR [#2915](https://github.com/sipeed/picoclaw/pull/2915)) and Anthropic SDK jump (PR [#2962](https://github.com/sipeed/picoclaw/pull/2962)) strongly suggest the project is investing in first-class vision and multi-modal support. Image compression (#2964) fits this roadmap perfectly.

## 7. User Feedback Summary
**Satisfaction Drivers**
- **Rapid Bug Response:** The OneBot fix (filed Jun 4, fixed Jun 5) and context display fix (filed May 30, resolved Jun 5) demonstrate a strong SLA on reported regressions.

**Pain Points & Dissatisfaction**
- **Evolution Mode Cost Risk (Issue #3012):** Unpredictable token burn undermines trust in the new Evolution feature, which is crucial for “always-on” personal assistant use cases.
- **Skill Onboarding Friction (Issue #652):** The skill-creator has been nominally broken for four months. While docs were patched today, the missing tooling is a persistent barrier for new community developers.
- **Exec Guard Overreach (Issue #1042):** Users who write custom skills involving web requests are hit by safety guard false positives, forcing them to disable guards or work around the tool.

**Underlying Use Cases Expressed**
- Multi-modal chat (MiMo / Anthropic vision).
- Group chat integration (OneBot, likely connecting to QQ/NapCat on FreeBSD).
- Persistent AI agents via Evolution Mode.
- Custom skill development from community contributors.

## 8. Backlog Watch
Items requiring maintainer attention or decision:

1. **#2551 — Channel Identification Refactor**
   - *Opened:* Apr 16, 2026 | *Status:* Open, Stale
   - *Link:* https://github.com/sipeed/picoclaw/pull/2551
   - *Why it matters:* Critical for running multiple instances of the same channel type (e.g., multiple Slack workspaces). The longer this sits, the more the codebase diverges, making merge harder.

2. **#652 — Skill-Creator Audit & Restoration**
   - *Opened:* Feb 22, 2026 | *Status:* Open (partially addressed by #3013)
   - *Link:* https://github.com/sipeed/picoclaw/issues/652
   - *Why it matters:* First impressions matter. A broken onboarding path for skill developers has been the top open task for 3.5 months. The recent doc fix is a good start, but the checklist item (“restore missing scripts”) remains unchecked.

3. **#2964 — Image Input Compression**
   - *Opened:* May 28, 2026 | *Status:* Open / Draft
   - *Link:* https://github.com/sipeed/picoclaw/pull/2964
   - *Why it matters:* High user value in the growing multi-modal use case. Needs a maintainer review to move out of draft and into the merge queue.

4. **#3012 — Evolution Mode Token Drain**
   - *Opened:* Jun 5, 2026 | *Status:* Open
   - *Link:* https://github.com/sipeed/picoclaw/issues/3012
   - *Why it matters:* Though brand new, this is the most impactful active bug. Immediate investigation is warranted to prevent user churn and API cost surprises.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-06-06

**1. Today's Overview**
NanoClaw saw moderate PR activity on June 5th, with three pull requests updated and two merged. No new issues were filed, and no releases were published. The team concentrated on improving the onboarding flow and addressing a known gap in API error resilience. Project health appears stable, supported by an empty issue backlog and targeted progress on reliability enhancements.

**2. Releases**
No new releases were published on this date. The repository currently has no tagged releases to report.

**3. Project Progress**
Two housekeeping and feature pull requests were successfully merged today:

- **#2691 (Closed – Merged):** Improves the missing-credential flow by dynamically detecting the correct OneCLI setup URL from the gateway error body, removing hardcoded URLs.
  ([nanocoai/nanoclaw PR #2691](nanocoai/nanoclaw PR #2691))

- **#2690 (Closed – Merged):** Simplifies HF token setup by aligning the default secret mode for auto-created agents with the actual SDK behavior (`all` instead of `selective`) and correcting the associated documentation.
  ([nanocoai/nanoclaw PR #2690](nanocoai/nanoclaw PR #2690))

**4. Community Hot Topics**
Discussion volumes were effectively zero across the repository in the last 24 hours, with no comments or reactions recorded on any PRs or issues. The primary topic drawing attention is the open reliability fix in **PR #2692**, which addresses the poll-loop error-handling gap. While engagement is low, the subject is technically significant for users running long-lived agent workflows.

**5. Bugs & Stability**
One stability-related pull request is currently open. No crash reports or regressions were filed as direct issues today.

- **Severity: Medium-High** – [nanocoai/nanoclaw PR #2692](nanocoai/nanoclaw PR #2692) (Open) targets a silent failure scenario where the Claude Agent SDK reports transient HTTP 5xx errors (e.g., `529 Overloaded`) as a terminal `result` message instead of throwing an exception, leading to silent failures in the poll loop. The fix implements local retry logic with user notification upon exhaustion.

**6. Feature Requests & Roadmap Signals**
The merged PRs signal a deliberate focus on reducing setup friction (#2690, #2691). The active PR #2692 points to an emerging roadmap theme of hardening execution infrastructure against upstream API instability. These improvements are strong candidates for inclusion in the next minor release.

**7. User Feedback Summary**
Direct user feedback (comments, reactions) was absent in this session. However, the rationale behind PR #2691 (dynamic URL detection) and PR #2690 (fixing misaligned defaults) implies that the team identified user friction during onboarding and credential setup. The quick iteration suggests a responsive maintainer approach to recent pain points.

**8. Backlog Watch**
The project maintains an exceptionally clean backlog. There are **zero open issues** awaiting triage. The only open item pending maintainer action is **PR #2692** (the 5xx retry fix), which remains open for review. No long-unanswered community threads exist.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest – 2026-06-06**

---

### 1. Today's Overview
NullClaw is currently in a quiet, stable phase. No new issues were filed or resolved in the last 24 hours, and no releases were published. The sole locus of development activity is a single open Pull Request (#947) proposing a new provider integration. The lack of bug reports and the targeted nature of the pending feature suggest a healthy, low-maintenance project period focused on ecosystem expansion rather than fire-fighting.

### 2. Releases
No releases were published today.

### 3. Project Progress
No Pull Requests were merged or closed today. Development progress is confined entirely to the outstanding PR #947.

### 4. Community Hot Topics
The only community activity is **PR #947: feat(providers): add Evolink as an OpenAI-compatible provider** ([View](https://github.com/nullclaw/nullclaw/pull/947)). Submitted by the Evolink team, this PR is a first-party contribution to add their multi-model gateway as a native provider. It has not yet garnered community discussion (0 comments, 0 reactions), but the underlying user need is clear: developers want a frictionless way to access a variety of frontier models (GPT-5, Gemini, DeepSeek, etc.) through a single, widely-supported OpenAI-compatible interface without manual API management.

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The codebase remains stable with zero open issues.

### 6. Feature Requests & Roadmap Signals
PR #947 is the strongest roadmap signal this period. It indicates a steady push toward flexible provider aggregation. If merged, NullClaw will pivot further toward acting as a universal client for "provider-of-provider" gateways. Given the structure of the PR, the next release version is likely to include Evolink as a first-class provider. This trend suggests users want to load-balance or failover across several high-end LLMs without manually hardcoding multiple endpoints.

### 7. User Feedback Summary
No direct user pain points or satisfaction signals were recorded in Issues today. The only indirect feedback is the Evolink contribution itself, which implies a desire for native support for popular multi-model gateways. The zero-defect count suggests overall user satisfaction or low usage volume in the tracked period.

### 8. Backlog Watch
The backlog is clear. The only outstanding ticket is the newly opened **PR #947** ([View](https://github.com/nullclaw/nullclaw/pull/947)), which requires a maintainer review. It is not yet stale, but it represents the single most important action item for the project maintainers to address for the next development cycle.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-06-06.

---

## 1. Today's Overview

Today marks one of the most intense development cycles in recent IronClaw history. A staggering **50 pull requests** were updated, and **13 issues** received attention, with the overwhelming majority of activity driven by the **"Reborn" architecture migration**. A massive wave of backend infrastructure—spanning durable state backends (Postgres, LibSQL), the production activation of the hook framework, and API restructuring—dominated the merge queue. Simultaneously, community validation of the **WeCom (WeChat Work)** channel revealed several rough edges in the v0.29.1 release. No formal release was cut today, but the churn signals a major release is imminent once the Reborn surface stabilizes.

## 2. Releases

**None.** No releases were published on 2026-06-06. The project remains at **v0.29.1** (Staging). An open release PR ([#3708](nearai/ironclaw PR #3708)) has been stalled since May 16, detailing pending breaking changes in `ironclaw_common` and `ironclaw_skills`.

## 3. Project Progress

**22 pull requests were merged or closed today**, reflecting major milestones in the Reborn architecture.

- **Hook Framework Production Landing (Massive Merge Wave):** The hooks system has moved from substrate to live activation. Core contributor `zmanian` landed a series of XL-sized PRs resolving the primary hook tracking issue ([#3934](nearai/ironclaw Issue #3934)). Key landed PRs include:
  - **Backend Implementation:** `PostgresPredicateStateBackend` ([#3933](nearai/ironclaw PR #3933)) and `LibSqlPredicateStateBackend` ([#3936](nearai/ironclaw PR #3936)).
  - **Production Gate:** Activation behind a default-OFF `HOOKS_ENABLED` flag ([#3938](nearai/ironclaw PR #3938)).
  - **Third-Party Extensions:** Support for hook-only extensions with containment gating ([#3951](nearai/ironclaw PR #3951)).
  - **Security Hardening:** Critical patches for cross-tenant leakage, replay attacks, and provider spoofing ([#3931](nearai/ironclaw PR #3931)).
  - **Auditing & Testing:** Wiring of `SecurityAuditSink` ([#3922](nearai/ironclaw PR #3922)), cross-backend adversarial parity suite ([#3937](nearai/ironclaw PR #3937)).

- **Skills System Refactor:** PR [#2904](nearai/ironclaw PR #2904) was closed, representing a major security-first refactor that ripped out 11 WASM API-proxy tools in favor of 10 skill-based HTTP declarations, keeping the `http` tool as the single execution engine.

- **Architecture Splitting:** Work began on splitting the `ProductWorkflow` into explicit `submit`/`read`/`subscribe` doors ([#4488](nearai/ironclaw Issue #4488), [#4506](nearai/ironclaw PR #4506)) to cleanly support the upcoming OpenAI-compatible API wiring.

- **WeCom Fixes:** Two user-reported sub-issues were closed: fix for merged group/DM conversations ([#4194](nearai/ironclaw Issue #4194)) and unclear owner visibility ([#4198](nearai/ironclaw Issue #4198)).

## 4. Community Hot Topics

The most active discussions revolved around deep architectural decisions and critical logic flaws.

- **[Issue #4311: Reborn model gateway collapses budget governance failures into context-overflow recovery](nearai/ironclaw Issue #4311)**
  - *Comments: 2*
  - *Analysis:* This is the hottest technical thread. The core issue is that the `HostManagedModelErrorKind::BudgetExceeded` error is being incorrectly mapped to `ContextOverflow` in the agent loop. The underlying need is strictly correct error differentiation: budget governance failures should trigger a different recovery path than context window overflows. Misclassification risks silent failures or incorrect agent behavior.
- **[Issue #4488: Split ProductWorkflow into explicit submit/read/subscribe doors](nearai/ironclaw Issue #4488)**
  - *Comments: 2*
  - *Analysis:* This architectural planning issue reflects the intense preparation for OpenAI API compatibility. The community is discussing the cleanest effect-boundary patterns for the Reborn facade.
- **Dependabot Activity:** PRs [#4503](nearai/ironclaw PR #4503) (38 dependency updates) and [#4002](nearai/ironclaw PR #4002) (16 CI action updates) represent signal that the dependency surface is being heavily refreshed, which introduces risk of subtle breakages alongside the security improvements.

## 5. Bugs & Stability

Several significant bugs were reported or remain active. The WeCom channel faces the highest number of user-facing regressions.

| Severity | Issue | Summary | Status |
| :--- | :--- | :--- | :--- |
| **Critical** | [#4311](nearai/ironclaw Issue #4311) | Budget governance failures misclassified as context overflow in Reborn gateway. | Open |
| **High** | [#4512](nearai/ironclaw Issue #4512) | Concurrent sandbox `job_semaphore` is defined but never acquired, rendering concurrency controls inert. | Open |
| **High** | [#4108](nearai/ironclaw Issue #4108) | Nightly E2E test suite has been failing since May 27 (10+ days) with no maintainer response. | Open |
| **Medium** | [#4502](nearai/ironclaw Issue #4502) | WeCom group chat approval replies (`y`/`yes`) do not work, blocking tool approval. | Open |
| **Medium** | [#4500](nearai/ironclaw Issue #4500) | Channel onboarding system events written to wrong user conversations (WeCom & Telegram). | Open |
| **Medium** | [#4505](nearai/ironclaw Issue #4505) | WeCom group conversation titles not distinguishable in Web UI sidebar. | Open |
| **Resolved** | [#4194](nearai/ironclaw Issue #4194) | Group/Private DM conversations were merged; fix has landed. | Closed |
| **Resolved** | [#3931](nearai/ironclaw PR #3931) | Cross-tenant leakage & replay fixed in hook framework. | Closed |

## 6. Feature Requests & Roadmap Signals

The roadmap is rapidly crystallizing around the "Reborn" API surface and enhanced channel capabilities.

- **OpenAI-Compatible API Gateway:** The foundational work is underway. Splitting the `ProductWorkflow` ([#4488](nearai/ironclaw Issue #4488)) and hardening the submit/projection boundary ([#4483](nearai/ironclaw Issue #4483)) are explicitly paving the way for an OpenAI-compatible endpoint. This is the highest-signal roadmap item.
- **Slack as a First-Class Channel:** Multiple PRs from `serrrfirat` aggressively target Slack:
  - Streaming feedback (delete "Ironclaw is thinking...") ([#4491](nearai/ironclaw Issue #4491)).
  - Durable stores for host-beta state ([#4463](nearai/ironclaw PR #4463)).
  - Channel route admin wiring ([#4510](nearai/ironclaw PR #4510)).
- **Extension Ecosystem (IronHub):** The port of the IronHub install flow to Reborn ([#4479](nearai/ironclaw PR #4479)) with signed catalogs and provenance checking signals a move toward a secure, official extension marketplace.
- **Runtime-Aware Approval Gates:** PR [#4390](nearai/ironclaw PR #4390) wires runtime profiles into approval gates, allowing local-dev bypass decisions versus strict production policies.

## 7. User Feedback Summary

Real user feedback comes predominantly from community member **`sunglow666`**, who performed a deep validation pass of the WeCom channel (summarized in [#4191](nearai/ironclaw Issue #4191)).

- **Satisfaction:** Core text messaging, pairing/reconnection, markdown rendering, emoji, and multilingual support are all working well.
- **Dissatisfaction/Pain Points:**
  - **Core Workflow Blocked:** Tool approval is completely broken in WeCom group chats ([#4502](nearai/ironclaw Issue #4502)). The bot keeps asking for approval even after the correct reply.
  - **Data Integrity:** Onboarding events and conversation routing are unreliable, writing system messages to the wrong conversation ([#4500](nearai/ironclaw Issue #4500)).
  - **UX Degradation:** Multiple group chats are indistinguishable in the Web UI, making the sidebar unusable for users with several groups ([#4505](nearai/ironclaw Issue #4505)).

## 8. Backlog Watch

These issues require urgent maintainer attention or are blocking the release pipeline.

- **[Issue #4108: Nightly E2E failed](nearai/ironclaw Issue #4108)** — *Age: 10 days | Status: Open (No Comments)*
  - **Watch Risk: High.** The nightly E2E suite has been failing since May 27. With the massive volume of development merges in the last 24 hours (Postgres/LibSQL backends, hook framework), a stale CI failure is a significant blind spot. If the CI gate is broken, bugs from the entire hooks merge wave could go undetected. Maintainers should prioritize reconciliation of this run.
- **[PR #3708: chore: release](nearai/ironclaw PR #3708)** — *Age: 21 days | Status: Open*
  - **Watch Risk: High.** This release PR has been open for three weeks. It details API breaking changes in `ironclaw_common` and `ironclaw_skills`. The delay suggests unresolved internal debates about release readiness or migration paths. The accumulation of work since May 16 means the next release will be a blockbuster, but it is currently blocked.
- **[Issue #4512: Concurrent sandbox job_semaphore is never acquired](nearai/ironclaw Issue #4512)** — *Age: 0 days (Reported today)*
  - **Watch Risk: Medium.** A concurrency guard that is defined but never acquired is a bug of omission. It doesn't crash, but long-running concurrent jobs may face resource starvation or race conditions depending on the runtime environment. Because it was reported today, it hasn't been triaged yet.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — June 6, 2026

---

## 1. Today's Overview

LobsterAI demonstrated exceptional development velocity today, with **12 pull requests merged** and a **new release published (v2026.6.5)**. Activity spanned features across Cowork, Artifacts, Voice Input, and Settings, accompanied by two critical security patches. The open issue queue remains stable at **3 items**, all carrying "stale" labels. Overall, the project shows strong forward momentum with healthy attention to both user-facing features and internal hardening, though several long-standing UX bugs in the Cowork module continue to await resolution.

---

## 2. Releases

### LobsterAI 2026.6.5 — Released June 5

**What's Changed:**
- **Cowork**: Improved channel session synchronization and cleanup logic ([PR #2108](https://github.com/netease-youdao/LobsterAI/pull/2108))
- **Shortcuts**: Complete overhaul of keyboard shortcuts with expanded actions and improved UX ([PR #2108](https://github.com/netease-youdao/LobsterAI/pull/2108))

**Breaking Changes / Migration Notes:**
- No breaking changes or migration notes were documented in this release.
- Users with custom shortcut configurations should review their settings post-update, as the action mapping has been significantly restructured.

---

## 3. Project Progress

The following features and fixes advanced to the `main` branch today:

### Cowork & Chat UX
- **PR #2118** ([link](https://github.com/netease-youdao/LobsterAI/pull/2118)): Robust clipboard copy with a graceful fallback chain (Electron → Clipboard API → textarea execCommand). Prompts login/subscribe when no accessible model is available.
- **PR #2116** ([link](https://github.com/netease-youdao/LobsterAI/pull/2116)): Classification of LobsterAI free-quota exhaustion errors with upgrade links; deduplication of consecutive stream errors within a 10s window; install guide for empty expert kits state.
- **PR #2115** ([link](https://github.com/netease-youdao/LobsterAI/pull/2115)): IM reply handler now correctly assembles replies from current-turn messages only, fixing a context contamination bug.

### Artifacts
- **PR #2114** ([link](https://github.com/netease-youdao/LobsterAI/pull/2114)): Significant enhancement to file preview functionality. Office zoom, preview/source switching collapsed into "More" menus. Fixes for Word pagination, PDF/Office scaling, Excel column width, row overlap, and PPT scroll scaling in expanded panel view. Added HTML file browser preview and expandable panel support.

### Voice Input
- **PR #2113** ([link](https://github.com/netease-youdao/LobsterAI/pull/2113)): Added macOS microphone usage metadata and audio-input entitlement. Registered trusted renderer media permission policy. Refactored permission helpers out of `main.ts`. Added ASR request diagnostics for uploaded audio.

### Subscription & Model Management
- **PR #2112** ([link](https://github.com/netease-youdao/LobsterAI/pull/2112)): Locked plan models now show a login/subscribe prompt on click instead of being silently disabled. Restricted fallback behavior for locked models in default/agent selection. Added OpenClaw repair flow.

### Configuration & Migration
- **PR #2117** ([link](https://github.com/netease-youdao/LobsterAI/pull/2117)): Tracked provider model migration versions to prevent duplicate injection. Preserved user-deleted provider models across app restarts. Added regression tests for all affected providers.

### Settings & UI Polish
- **PR #1531** ([link](https://github.com/netease-youdao/LobsterAI/pull/1531)): Replaced the multi-card theme color grid with a compact diagonal-gradient circle selector. Light/dark theme adaptation. (Stale PR merged after ~2 months).
- **PR #1533** ([link](https://github.com/netease-youdao/LobsterAI/pull/1533)): New local session usage statistics panel in Settings → General. Displays total sessions/messages, today/this week metrics, and average messages per session via SQLite.

### Security Hardening
- **PR #1534** ([link](https://github.com/netease-youdao/LobsterAI/pull/1534)): Sanitized API proxy logs — URLs now omit query/hash, request/response details log only metadata (header count, byte size) instead of full bodies and tokens. (Stale PR merged after ~2 months).
- **PR #1535** ([link](https://github.com/netease-youdao/LobsterAI/pull/1535)): Restricted renderer process KV store IPC (`store:get`/`set`/`remove`) to a defined allowlist of safe keys, preventing exposure of `auth_tokens`, `enterprise_config`, and other sensitive data. (Stale PR merged after ~2 months).

### Release Management
- **PR #2119** ([link](https://github.com/netease-youdao/LobsterAI/pull/2119)): Release 2026.6.4 cut, bundling features across Cowork, Voice Input, Artifacts, Shortcuts, and Update modules.

---

## 4. Community Hot Topics

### Most Active Issues

| Issue | Author | Created | Updated | Comments | Summary |
|---|---|---|---|---|---|
| [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | 54huige | Apr 5 | Jun 5 | 2 | Python script execution fails in Cowork sessions but works in Claude Code CLI |
| [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | MaoQianTu | Apr 4 | Jun 5 | 1 | Draft content lost due to debounce on session/view switch |
| [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | MaoQianTu | Apr 4 | Jun 5 | 1 | Re-editing history message overwrites unsent draft without confirmation |

**Analysis:**

**Issue #1487** highlights a meaningful feature gap for power users running local models (30B). The user reports that Python tool-calling works correctly in the standard Claude Code CLI but fails within Lobster's Cowork interface. This suggests a possible difference in how the application translates user intents or orchestrates tool calls compared to the reference CLI implementation. The underlying need is **strict feature parity with the official client**, especially for developers experimenting with local models.

**Issues #1471 and #1472**, both filed by user **MaoQianTu**, point to a fragile state management system in the Cowork input area. Together, they paint a picture of an editor where user data can easily be lost through normal workflow actions (switching views, editing history). While the maintainers merged related Cowork UX improvements today (PR #2116, #2118), these specific persistence bugs remain open.

---

## 5. Bugs & Stability

### Critical/High Severity (Resolved)
| Bug | Fix PR | Severity | Notes |
|---|---|---|---|
| API Proxy Log Leaks ([#1534](https://github.com/netease-youdao/LobsterAI/pull/1534)) | Merged | Critical | Full request URLs, headers, and response bodies were logged at `info` level, exposing API keys, Bearer tokens, and conversation content |
| Renderer KV Store Exposure ([#1535](https://github.com/netease-youdao/LobsterAI/pull/1535)) | Merged | Critical | Renderer process had unrestricted access to sensitive KV keys (`auth_tokens`, `github_copilot_github_token`, `enterprise_config`) |

### Medium Severity (Resolved)
| Bug | Fix PR | Notes |
|---|---|---|
| macOS Voice Input Microphone Access ([#2113](https://github.com/netease-youdao/LobsterAI/pull/2113)) | Merged | Missing entitlement and permission request flow blocked ASR |
| Config Migration Removes Deleted Models ([#2117](https://github.com/netease-youdao/LobsterAI/pull/2117)) | Merged | User-deleted provider models were re-added on app restart |
| IM Reply Context Assembly ([#2115](https://github.com/netease-youdao/LobsterAI/pull/2115)) | Merged | Reply handler used all history instead of current-turn messages only |
| Clipboard Copy Failures ([#2118](https://github.com/netease-youdao/LobsterAI/pull/2118)) | Merged | No graceful fallback chain for electron/copy board operations |

### Low Severity / Unresolved
| Bug | Issue | Status | Pain Level |
|---|---|---|---|
| Cowork Draft Persistence | [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | Open, stale | High |
| Cowork Re-edit Overwrite | [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | Open, stale | High |
| Python Script Compatibility | [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | Open, stale | Medium (power users) |

---

## 6. Feature Requests & Roadmap Signals

### Recently Fulfilled Requests
- **Local session usage statistics** (implied by [#1532](https://github.com/netease-youdao/LobsterAI/issues/1532)): Fulfilled by PR [#1533](https://github.com/netease-youdao/LobsterAI/pull/1533) (merged today).
- **Compact theme color selector**: Fulfilled by PR [#1531](https://github.com/netease-youdao/LobsterAI/pull/1531) (merged today, filed April 7).

### Active Roadmap Signals
- **Voice Input (ASR)**: Multiple PRs today (especially [#2113](https://github.com/netease-youdao/LobsterAI/pull/2113)) focus on microphone permission infrastructure, entitlement configuration, and diagnostic tooling. This suggests Voice Input is approaching a general release milestone.
- **Artifacts Expansion**: PR [#2114](https://github.com/netease-youdao/LobsterAI/pull/2114) represents a major iteration on the artifacts workspace. Office file preview, HTML browser preview, and expandable panel support indicate that LobsterAI is positioning Artifacts as a fully featured alternative to standalone IDE previews.
- **Monetization & Tier Management**: PR [#2112](https://github.com/netease-youdao/LobsterAI/pull/2112) (subscribe prompts, locked model indicators) and PR [#2116](https://github.com/netease-youdao/LobsterAI/pull/2116) (free-quota exhaustion handling) show active implementation of the subscription and plan system.

### Prediction for v2026.6.6
- Resolution of the Cowork input persistence bugs ([#1471](https://github.com/netease-youdao/LobsterAI/issues/1471), [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472))
- General release flag for Voice Input
- Continued Artifacts stabilization following the large PR [#2114](https://github.com/netease-youdao/LobsterAI/pull/2114) changes
- Potential fix for Python script compatibility gap ([#1487](https://github.com/netease-youdao/LobsterAI/issues/1487))

---

## 7. User Feedback Summary

### Sources of Satisfaction
- **High development velocity**: Users see a massive merge batch (12 PRs) clearing a long tail of bugs and feature items simultaneously.
- **Security responsiveness**: The rapid landing of two security patches (log sanitization, IPC allowlist) signals responsible stewardship.
- **Requested features delivered**: Session stats and theme selector requests were fulfilled today.

### Sources of Frustration / Pain Points
- **Data integrity anxiety** ([#1471](https://github.com/netease-youdao/LobsterAI/issues/1471), [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472)): Losing unsent draft content or having it silently overwritten is the highest-impact UX complaint currently open. These issues have been active for **two months** without a merged fix.
- **CLI feature parity gap** ([#1487](https://github.com/netease-youdao/LobsterAI/issues/1487)): For users running local models (e.g., 30B class), Python script execution breaks in Lobster's Cowork while working in the official Claude Code CLI. This undermines trust for the power-user segment.
- **Security exposure window**: While fixed, the log and IPC vulnerabilities (PRs [#1534](https://github.com/netease-youdao/LobsterAI/pull/1534), [#1535](https://github.com/netease-youdao/LobsterAI/pull/1535)) existed in prior releases. Users running pre-patch builds may have had sensitive data exposed in logs or accessible from the renderer process.

---

## 8. Backlog Watch

### Issues at Risk of Stagnation

| Issue | Author | Age | Last Updated | Comments | Current Status |
|---|---|---|---|---|---|
| [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) — Python script fails in Cowork | 54huige | ~62 days | Jun 5 | 2 | No maintainer action or assignment visible |
| [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) — Cowork draft loss on navigation | MaoQianTu | ~63 days | Jun 5 | 1 | No maintainer action or assignment visible |
| [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) — Cowork re-edit overwrite | MaoQianTu | ~63 days | Jun 5 | 1 | No maintainer action or assignment visible |

### Assessment
The maintainers made excellent progress today clearing the **stale PR backlog** — four PRs dating to early April were merged ([#1531](https://github.com/netease-youdao/LobsterAI/pull/1531), [#1533](https://github.com/netease-youdao/LobsterAI/pull/1533), [#1534](https://github.com/netease-youdao/LobsterAI/pull/1534), [#1535](https://github.com/netease-youdao/LobsterAI/pull/1535)). However, the **three open issues** remain untouched and carry "stale" labels. While the overall velocity explains this prioritization (heavy feature delivery), the ongoing lack of acknowledgment or milestone assignment for these issues risks community trust erosion. Users filing detailed, reproducible UX bug reports deserve a status signal — even a pinned "planned for next iteration" comment would significantly improve perception of maintainer attentiveness.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-06

**Project:** [moltis-org/moltis](https://github.com/moltis-org/moltis)

---

## 1. Today's Overview

Moltis shows measured but meaningful development activity today. Contributors processed four issues and five pull requests, delivering one critical fix for the Telegram integration while advancing infrastructure work on container sandboxing and model configuration. While no new releases were cut, the project demonstrates healthy iteration velocity: a significant bug reported on June 3rd was merged as a fix by June 5th. Activity is balanced between squashing regressions (Docker filesystem fallback, model preference persistence) and hardening core execution environments (Podman support, session history tool result limits).

---

## 2. Releases

No new releases published in this window. The last stable version remains current.

---

## 3. Project Progress

**Merged / Closed:**
- **[PR #1099](https://github.com/moltis-org/moltis/pull/1099)** (by s-salamatov) — *Separate Telegram progress stream from final replies.* Fixed a critical regression where Telegram's edit-in-place streaming was mixing intermediate progress updates into the final answer. The solution sends a silent progress message, throttles edits, and deletes it on completion so the canonical reply arrives cleanly. This resolves **[Issue #1097](https://github.com/moltis-org/moltis/issues/1097)** (reported June 3, fixed June 5 — excellent response time).

**Open PRs Under Active Development:**
- **[PR #1089](https://github.com/moltis-org/moltis/pull/1089)** (s-salamatov) — Caps persisted tool/tool_result content during session rehydration. A wide-reaching change affecting normal chat, streaming, compaction, prompt inspection, and silent memory turns.
- **[PR #1104](https://github.com/moltis-org/moltis/pull/1104)** (penso) — Allows users to replace or clear saved preferred provider models from the UI, with backend and Playwright regression coverage.
- **[PR #1105](https://github.com/moltis-org/moltis/pull/1105)** (penso) — Adds robust fallback from translated Docker host paths to container copy when the gateway process cannot access the host mount. Includes regression tests for sandboxed file operations.
- **[PR #1106](https://github.com/moltis-org/moltis/pull/1106)** (penso) — Opt-in Podman escape hatches for host socket passthrough and privileged nested Podman, plus improved diagnostics for rootless Podman `cannot clone` failures.

---

## 4. Community Hot Topics

**Telegram Streaming Reliability**
The most active topic by engagement was the Telegram output corruption bug. **[Issue #1097](https://github.com/moltis-org/moltis/issues/1097)** (1 comment) and its rapid resolution via **[PR #1099](https://github.com/moltis-org/moltis/pull/1099)** signal that streaming stability on messaging integrations is a high priority for both maintainers and the user base.

**Container Sandboxing Push**
Three PRs from penso ([#1104](https://github.com/moltis-org/moltis/pull/1104), [#1105](https://github.com/moltis-org/moltis/pull/1105), [#1106](https://github.com/moltis-org/moltis/pull/1106)) represent a coordinated effort to harden the execution sandbox across Docker and Podman. This is the day's dominant infrastructure theme.

**Usability Polish from a Power User**
User IlyaBizyaev filed three focused UX issues on June 5th:
- [#1107](https://github.com/moltis-org/moltis/issues/1107) — Multiline text input for mobile web UI
- [#1108](https://github.com/moltis-org/moltis/issues/1108) — Session list shows times but not dates for past sessions
- [#1109](https://github.com/moltis-org/moltis/issues/1109) — Update banner doesn't account for Docker installs

While none have comments yet, filing multiple detailed, non-blocking issues in a single day indicates a deeply engaged user actively testing the edges of the web experience. Prompt triaging here would reinforce positive contributor momentum.

---

## 5. Bugs & Stability

| Severity | Issue | Status |
|----------|-------|--------|
| **High** | **Telegram streaming leaks progress into final reply** ([#1097](https://github.com/moltis-org/moltis/issues/1097)) | **CLOSED** — Fixed by [#1099](https://github.com/moltis-org/moltis/pull/1099) |
| **Medium** | **Update banner fires incorrectly on Docker installs** ([#1109](https://github.com/moltis-org/moltis/issues/1109)) | OPEN, no fix PR yet |
| **Medium** | **Session list omits dates for past-day sessions** ([#1108](https://github.com/moltis-org/moltis/issues/1108)) | OPEN, no fix PR yet |
| **Low** | **Docker sandbox filesystem tool fails when host mount is inaccessible** (PR [#1105](https://github.com/moltis-org/moltis/pull/1105)) | Fix PR OPEN |
| **Low** | **Rootless Podman failure diagnostics need improvement** (PR [#1106](https://github.com/moltis-org/moltis/pull/1106)) | Fix PR OPEN |
| **Low** | **Tool result bloat can break session rehydration** (PR [#1089](https://github.com/moltis-org/moltis/pull/1089)) | Fix PR OPEN |

No crashes or data loss reports were filed in this window. The most severe bug (Telegram streaming) was turned around in ~48 hours.

---

## 6. Feature Requests & Roadmap Signals

Looking at active PRs and fresh feature requests, the next release cycle appears focused on:

- **Container Ecosystem Flexibility** — Podman escape hatches ([#1106](https://github.com/moltis-org/moltis/pull/1106)) and Docker sandbox fallbacks ([#1105](https://github.com/moltis-org/moltis/pull/1105)) suggest a strong push toward supporting alternative container runtimes beyond basic Docker.
- **Model Configuration** — Allowing users to explicitly replace or clear preferred models ([#1104](https://github.com/moltis-org/moltis/pull/1104)) is a quality-of-life improvement for providers with many model options.
- **Web UI Mobile & Usability** — Multiline text input ([#1107](https://github.com/moltis-org/moltis/issues/1107)) and date display in session lists ([#1108](https://github.com/moltis-org/moltis/issues/1108)) point to a polishing phase for the web interface, targeting mobile power users.
- **Session Robustness** — Capping tool results before rehydration ([#1089](https://github.com/moltis-org/moltis/pull/1089)) is a preventative measure against session history corruption, a strong candidate for inclusion in a stability-oriented patch.

**Prediction:** The next release will likely include the Podman and Docker filesystem fixes (PR [#1105](https://github.com/moltis-org/moltis/pull/1105), [#1106](https://github.com/moltis-org/moltis/pull/1106)) and the model preference UI fix ([#1104](https://github.com/moltis-org/moltis/pull/1104)), possibly packaged as a minor version bump.

---

## 7. User Feedback Summary

**Pain Points:**
- **Telegram Integration Defect** (now fixed): Streaming was corrupting final replies — a severe operational issue for chat-first users.
- **Docker Update UX Bug:** The update banner does not distinguish between source-installed and Docker-installed instances ([#1109](https://github.com/moltis-org/moltis/issues/1109)), creating noise for container users.
- **Mobile Web Limitations:** Lack of multi-line input on mobile ([#1107](https://github.com/moltis-org/moltis/issues/1107)) hinders power users on phones and tablets.
- **Session History Context:** The web session list drops date context after 24 hours ([#1108](https://github.com/moltis-org/moltis/issues/1108)), making navigation difficult for heavy users.

**Use Cases Observed:**
- Heavy reliance on Telegram as a primary interface.
- Self-hosting via Docker (and growing interest in Podman).
- Web UI used both as primary desktop interface and mobile companion.

**Satisfaction Signal:** The rapid turnaround on the Telegram streaming bug (48 hours from report to fix) indicates high maintainer responsiveness, which generally reflects a responsive project culture.

---

## 8. Backlog Watch

**[PR #1089](https://github.com/moltis-org/moltis/pull/1089)** — *Cap persisted tool results before rehydration* (s-salamatov, opened June 1)
This is the oldest open PR without a merge. It touches session history across the entire chat stack (normal chat, streaming, compaction, silent memory, prompt inspection). Its stalled status at 5 days with no comments or review activity may indicate it needs broader architectural discussion or is awaiting a difficult design review.

**[Issues #1107](https://github.com/moltis-org/moltis/issues/1107), [#1108](https://github.com/moltis-org/moltis/issues/1108), [#1109](https://github.com/moltis-org/moltis/issues/1109)** (IlyaBizyaev, opened June 5)
All three remain untriaged — no labels, no assignees, no comments. While fresh, maintaining responsiveness here will sustain the contributor's engagement.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-06

**Project:** CoPaw / QwenPaw (`agentscope-ai/QwenPaw`)  
**Analysis Date:** 2026-06-06  
**Data Window:** Last 24 hours


## 1. Today's Overview

The CoPaw (QwenPaw) project is seeing intense community activity, with **20 issues** and **16 pull requests** updated in the past day, signaling strong user engagement paired with significant stability challenges. No new releases were published, but the development team is actively reviewing substantial fix PRs targeting critical bugs in browser automation, channel integration (Yuanbao), and the desktop experience. User sentiment appears divided: the community is deeply engaged and filing high-quality, detailed bug reports, but several blocking defects—particularly agent infinite loops and memory leaks—are causing significant friction for real-world usage. The rapid response with companion fix PRs for several of these issues suggests a focused stabilization push.


## 2. Releases

**None.** The current latest available version remains **v1.1.10**. No release artifacts or changelogs were published today.


## 3. Project Progress

Several notable fixes and features reached a resolved state today, reflecting active work across browser automation, security, UI polish, and test coverage.

**Browser & Desktop Stability:**
- **PR #4944** (closed, [`agentscope-ai/QwenPaw/pull/4944`](agentscope-ai/QwenPaw/pull/4944)) — Resolved CDP timeout failures and added browser-specific user data directories (`user_data_chrome`, `user_data_edge`) to prevent profile format conflicts when switching between Chrome and Edge. This directly fixes the issues reported in #4919.
- **PR #4905** (closed, [`agentscope-ai/QwenPaw/pull/4905`](agentscope-ai/QwenPaw/pull/4905)) — Added coordinate-based mouse click support (`page_x`/`page_y`) to the `browser_control` skill.

**New Integrations:**
- **PR #4934** (closed, [`agentscope-ai/QwenPaw/pull/4934`](agentscope-ai/QwenPaw/pull/4934)) — First-time contributor contribution adding an **OpenSandbox** plugin (`plugins/tool/opensandbox/`), enabling agents to execute shell commands in an isolated sandbox environment without modifying core shell tooling.

**UI & Console Fixes:**
- **PR #4972** (closed, [`agentscope-ai/QwenPaw/pull/4972`](agentscope-ai/QwenPaw/pull/4972)) — Fixed LaTeX math formula rendering by installing KaTeX dependencies and integrating the LaTeX plugin into the Markdown renderer. Fixes #4756.
- **PR #4765 / #4766** (closed, first-time contributor @SnowTQ) — Centered the shield icon on the security page and removed hover `transform` on environment variable rows to eliminate scrollbar flickering.

**Security:**
- **PR #4026** (closed, [`agentscope-ai/QwenPaw/pull/4026`](agentscope-ai/QwenPaw/pull/4026)) — Added `WriteFileOverwriteGuardian` to prevent the `write_file` tool from silently overwriting non-empty files.

**Testing:**
- **PR #4973** (open, [`agentscope-ai/QwenPaw/pull/4973`](agentscope-ai/QwenPaw/pull/4973)) — New contributor @EaveLuo submitted **129 test cases across 1,374 lines** expanding coverage for `local_models`, `providers`, `tunnel`, and `utils` modules.

**Yuanbao Channel Fixes (Open PRs):**
The team has opened a coordinated set of fix PRs today for the Yuanbao channel:
- **PR #4983** — Store `connectId` from `AuthBindRsp`
- **PR #4982** — Fix streaming replies silently dropped when `streaming_enabled=True`
- **PR #4981** — Restrict file preview to `WORKING_DIR` and block sensitive paths


## 4. Community Hot Topics

The following items generated the most discussion activity (comments) in the last 24 hours:

**Most Active Issues:**

1.  **#4754** — [CLOSED] *[Question]: 打包方式 (Packaging method)*  
    *7 comments* — A user asked about the difference between the Windows Desktop client and the Tauri version for creating `.exe` packages. The thread reflects widespread community interest in packaging and distribution.  
    [`agentscope-ai/QwenPaw/issues/4754`](agentscope-ai/QwenPaw/issues/4754)

2.  **#4919** — [CLOSED] *[Bug]: browser_use CDP timeout / Chrome/Edge crash*  
    *6 comments* — Several users confirmed the same failure patterns with browser automation. The thorough debugging (Playwright versions, npm CLI fallback) provided valuable troubleshooting data for the team.  
    [`agentscope-ai/QwenPaw/issues/4919`](agentscope-ai/QwenPaw/issues/4919)

3.  **#4770** — [OPEN] *[Feature]: Session list column order adjustment*  
    *5 comments* — Strong user consensus that "update by time" should be leftmost and that session ID columns have no value for end users. This has now been implemented in **PR #4975**.  
    [`agentscope-ai/QwenPaw/issues/4770`](agentscope-ai/QwenPaw/issues/4770)

4.  **#4967** — [OPEN] *[Bug]: Infinite execution loop, cannot exit*  
    *4 comments* — High urgency thread where users describe agents trapped in a loop. The lack of a documented kill switch for such states is a clear user pain point.  
    [`agentscope-ai/QwenPaw/issues/4967`](agentscope-ai/QwenPaw/issues/4967)

5.  **#4963** — [OPEN] *[Feature]: Cron direct script/shell execution*  
    *3 comments* — A power-user request to bypass the AI agent for pure scheduled script execution. The discussion reveals a clear pattern of users running system commands via Cron.  
    [`agentscope-ai/QwenPaw/issues/4963`](agentscope-ai/QwenPaw/issues/4963)

**Underlying Needs Analysis:** The community is demanding **stability** (loop handling, memory management) and **flexibility** (cron without AI, custom column views, sandboxing). There is a clear split between users wanting a polished desktop appliance and those building programmable agent workflows.


## 5. Bugs & Stability

**Critical (Agent Blocking / Data Loss Risk):**

| Issue | Title | Impact | Fix Status |
|---|---|---|---|
| [#4967](agentscope-ai/QwenPaw/issues/4967) | [Bug]: 执行过程陷入死循环，无法退出 (Agent trapped in infinite loop) | Server-side process hang requiring force kill | No fix PR yet |
| [#4968](agentscope-ai/QwenPaw/issues/4968) | [Bug]: Subprocess fork fails "Cannot allocate memory" due to virtual memory leak | Service crashes, OOM scenarios | No fix PR yet |
| [#4970](agentscope-ai/QwenPaw/issues/4970) | [Bug]: Corrupted `loop_config.json` / `prd.json` crashes entire session | Complete loss of agent interaction | No fix PR yet |

**High (Severely Degraded Experience):**

| Issue | Title | Impact | Fix Status |
|---|---|---|---|
| [#4962](agentscope-ai/QwenPaw/issues/4962) | [Bug]: DeepSeek API replies folded into thinking block | Reply hidden behind expand toggle | No fix PR yet |
| [#4976-4980](agentscope-ai/QwenPaw/issues/4976-4980) | [Bug]: Yuanbao channel – missing proto files, protobuf compat, streaming drop, auth failure | Channel integration effectively broken | **PRs #4981, #4982, #4983 open** |
| [#4832](agentscope-ai/QwenPaw/issues/4832) | [Bug]: Shell subprocess missing `CREATE_NO_WINDOW` flag | cmd.exe window flashes on every Windows shell call | Fix proposed in **PR #4900** (open) |

**Medium (Annoyance):**

| Issue | Title | Status |
|---|---|---|
| [#4959](agentscope-ai/QwenPaw/issues/4959) | [Bug]: Abnormal LaTeX display | **Fixed in PR #4972** |
| [#4770](agentscope-ai/QwenPaw/issues/4770) | [Bug/Feature]: Session column order poor | **Fixed in PR #4975** |

**Key Observation:** The severity of issues #4967 and #4968 is a major **health signal concern**. An agent that cannot be interrupted or a process that leaks memory to the point of `fork()` failure are fundamental reliability problems. The community is filing these with good reproduction data, and the speed of maintainer response (e.g., Yuanbao channel fixes having PRs up the same day) is commendable, but these root causes need urgent resolution.


## 6. Feature Requests & Roadmap Signals

Based on community demand and PR activity, the following features are strong candidates for inclusion in the next point release (v1.1.11) or the next minor release:

- **High Priority:**
    - **Cron Direct Script Execution (#4963):** Users are explicitly asking for a `shell` task type in Cron. This is a clean addition that doesn't require AI agent involvement and has clear user utility. Likely target: **v1.1.11**.
    - **Session Sidebar / Quick Switcher (#4971):** A user request for one-click session switching, citing the current interface as cumbersome. Combined with the column order fix (#4975), a session UI overhaul seems imminent.

- **Medium Priority:**
    - **Per-Agent Avatars (#4974):** Requests to upload avatar URLs or images for visual differentiation in management lists and chat windows. Cosmetic but highly requested.
    - **LAN Console Access (#4960):** A user is blocked from mobile browser access on LAN and has exhausted firewall debugging. Likely a missing HTTP host binding or documentation gap.

- **Nice-to-Have (Backlog):**
    - **macOS Intel Tauri Support (#4744):** Question about whether the Tauri client supports Intel Macs. Maintainers have not yet responded. This may simply require a build target update.


## 7. User Feedback Summary

**Positive Signals:**
- Users are actively using advanced features (Mission Mode, Cron, browser automation, Yuanbao channel).
- Community provides high-quality, multi-attempt debugging logs (see #4919, #4968).
- First-time-contributor PRs are being accepted and merged (PRs #4934, #4972, #4973).
- The user filing #4971 explicitly says the project has potential but the session UX needs work.

**Critical Pain Points:**
1.  **Reliability:** "Agent trapped in a loop", "cannot exit", "crashes the entire agent" – these are the loudest complaints. Users expect a robust kill switch and error recovery.
2.  **Desktop Experience:** CMD flashing (#4832) is a consistent complaint for Windows desktop app users, making the tool feel unpolished.
3.  **Integration Friction:** The Yuanbao channel is generating a cluster of bugs (#4976-#4980), creating a negative experience for users of that platform.
4.  **AI Rendering:** The DeepSeek thinking/reply folding bug (#4962) affects the core interaction loop, hiding the actual AI response.

**User Sentiment Trend:** Cautiously optimistic. Users are putting in the work to report bugs but are frustrated by fundamental stability issues. The rapid closing of some issues (e.g., #4919) is a positive signal, but the unresolved critical bugs (#4967, #4968, #4970) overshadow the progress.


## 8. Backlog Watch

The following issues and PRs require maintainer attention due to age, lack of response, or importance to the community:

**Unanswered Issues:**

| Issue | Date Created | Summary | Days Waiting |
|---|---|---|---|
| [#4744](agentscope-ai/QwenPaw/issues/4744) | 2026-05-28 | macOS Tauri Intel chip support query | 9 days |
| [#4960](agentscope-ai/QwenPaw/issues/4960) | 2026-06-04 | LAN console access failure (user exhausted all troubleshooting) | 2 days |
| [#4832](agentscope-ai/QwenPaw/issues/4832) | 2026-05-31 | CMD window flash on Windows shell command | 6 days |

**Stale PRs Awaiting Review / Merge:**

| PR | Updated | Description | Risk / Impact |
|---|---|---|---|
| [#4822](agentscope-ai/QwenPaw/pull/4822) | 2026-06-05 | Fix cron agent tasks producing empty traces (#4818) | **High** – Affects reliability of Cron agent responses. |
| [#4884](agentscope-ai/QwenPaw/pull/4884) | 2026-06-05 | Stop old channel before starting new in `replace_channel` | **Medium** – Channel lifecycle race condition. |
| [#4900](agentscope-ai/QwenPaw/pull/4900) | 2026-06-05 | Decouple plugin loader; fix Windows console window flash | **High** – Directly fixes #4832 and enables plugin loading in frozen environments. |
| [#4973](agentscope-ai/QwenPaw/pull/4973) | 2026-06-05 | New contributor: 129 test cases for Phase 5 modules | **Low risk, high value** – Code coverage improvement. |

**Risk Assessment:** The most critical item in the backlog is **PR #4900** (plugin loader decoupling and `CREATE_NO_WINDOW` flag). This PR resolves both the long-standing Windows cmd flash complaint (#4832) and enables crucial functionality for Tauri/PyInstaller builds. Its prolonged open state (since June 2) is a bottleneck for the desktop experience. **Issue #4960** (LAN console access) is also growing stale and the user has explicitly signaled they have exhausted their own debugging—a direct response from maintainers is warranted.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 6, 2026.

---

### 1. Today's Overview
ZeroClaw recorded a peak activity day on June 6, 2026, with 50 issues and 50 pull requests updated in the last 24 hours. With 43 open issues, 38 open PRs, and 12 merged/closed actions, the project demonstrates a robust development velocity. Activity is heavily weighted toward a coordinated batch of architectural RFCs (Security, Observability, Connectivity), a massive expansion of the provider and channel ecosystem, and a parallel sprint to squash critical bugs. The project is clearly in a high-cycle build-up phase targeting a significant **v0.9.0** milestone.

### 2. Releases
No new releases were published today.

### 3. Project Progress
The merge/close rate today (12 items) reflects active feature integration and issue resolution. Notable closures include:
- **Bug Fixes Integrated:** The critical onboarding redirect bug impacting Codex users (zeroclaw-labs/zeroclaw Issue #6120) was resolved and closed. The `providers.fallback` configuration hook (zeroclaw-labs/zeroclaw Issue #6295) has been wired into the runtime provider resolution engine, closing out a long-standing schema-to-runtime gap.
- **Feature Pipeline (Open PRs):** A massive wave of PRs is under review. This includes the introduction of **7 new OpenAI-compatible model providers** (zeroclaw-labs/zeroclaw PR #7260) and the addition of **9 new communication channels** (Twilio, Plivo, Telnyx, Sinch, Vonage, Mastodon, Rocket.Chat, Zulip, Lemmy) under the schema v3 architecture (zeroclaw-labs/zeroclaw PR #7265, #7270). The web UI is also seeing a major update with dedicated management dashboards for MCP, Skills, and Plugins (zeroclaw-labs/zeroclaw PR #7229) and per-field editing for MCP servers (zeroclaw-labs/zeroclaw PR #7267).

### 4. Community Hot Topics
The community is deeply engaged in shaping the project’s core architecture and governance:
- **Project Governance:** Issue #6808 (zeroclaw-labs/zeroclaw Issue #6808, 9 comments) remains the most discussed item, proposing formal “Work Lanes, Board Automation, and Label Cleanup” to manage the project’s scaling complexity.
- **Core Agent UX:** Issue #6969 (zeroclaw-labs/zeroclaw Issue #6969, 7 comments) reveals a strong user pain point around the regression of “output routing” (controlling where and how replies are sent), critical for users migrating from other agent frameworks like Letta.
- **Security Architecture:** Authors **singlerider** and **Audacity88** are driving intense discussion on the v0.9.0 roadmap. Tracking issues for a Pluggable Security Provider (zeroclaw-labs/zeroclaw Issue #7142), OIDC Authentication (zeroclaw-labs/zeroclaw Issue #7141), and Air-gapped execution (zeroclaw-labs/zeroclaw Issue #6293) represent the heavy architectural discussions underway.

### 5. Bugs & Stability
A coordinated bug-fixing sprint is evident, with high-severity reports receiving immediate PRs:
- **Critical/Severity S2:**
    - Credential/URL fallback in the Channel Orchestrator (zeroclaw-labs/zeroclaw Issue #7059, P1/S2) could lead to incorrect provider routing. No fix PR is listed yet.
- **High Risk / Panics:**
    - UTF-8 char-boundary panics in text truncation for dashboards and social channels (zeroclaw-labs/zeroclaw PR #7123).
    - Malformed JSON from LLM tool calls for file writes causing parsing failures (zeroclaw-labs/zeroclaw PR #7244).
- **High Risk / Security:**
    - Nested secrets in config objects failing to redact properly (zeroclaw-labs/zeroclaw PR #7261).
    - Leaking `<think>` block content in the streaming agent loop (zeroclaw-labs/zeroclaw PR #7254).
    - `paired_tokens` drift detection producing false positives (zeroclaw-labs/zeroclaw PR #7247).
    - Killed ACP sessions being silently revivable (zeroclaw-labs/zeroclaw PR #7258).
- These issues are largely authored by core contributors who have also submitted their respective fix PRs, indicating a highly responsive engineering team.

### 6. Feature Requests & Roadmap Signals
The strongest roadmapping signal today is the intense focus on **v0.9.0**, which is shaping up to be an **Enterprise & Security Release**:
- **Enterprise Security Suite:** Tracking issues for Pluggable Security Providers (zeroclaw-labs/zeroclaw Issue #7142) and OIDC Authentication (zeroclaw-labs/zeroclaw Issue #7141) are the anchors of this release. The addition of a per-execution shell command confirmation tier (zeroclaw-labs/zeroclaw Issue #7155) and process memory limits on subprocesses (zeroclaw-labs/zeroclaw Issue #6916) suggests a focus on safe multi-tenancy and compliance.
- **Connectivity Expansion:** The batch addition of 7 providers and 9 channels signals a strategic push to become an agnostic hub for all AI traffic.
- **User-Driven Requests:** Users continue to ask strongly for **OAuth support** for subscription providers (zeroclaw-labs/zeroclaw Issue #5601), a **Lighter Core** that delegates tools to skills (zeroclaw-labs/zeroclaw Issue #6165), and a **Per-model capability config** for vision and context windows (zeroclaw-labs/zeroclaw Issue #7100).

### 7. User Feedback Summary
User feedback captured today highlights specific friction points and desired workflows:
- **Migration Pain:** A user migrating from Letta highlights a critical UX regression in controlling message delivery preferences, stating the old behavior **“is gone”** (zeroclaw-labs/zeroclaw Issue #6969). This is a high-signal feature gap for power users.
- **Integration Desires:** Users express a pain point in bridging their AI conversations with their coding environments. The request for a ZeroClaw MCP to XCode bridge (zeroclaw-labs/zeroclaw Issue #6065) reflects a demand for deeper IDE integration, while the office document parsing WASM plugin request (zeroclaw-labs/zeroclaw Issue #7024) signals a need for enhanced data ingestion capabilities.
- **Quality of Life:** The high false-positive rate of the “remote markdown link” skill audit (zeroclaw-labs/zeroclaw Issue #6714) is causing friction for skill developers, and a user explicitly flagged the clutter of 200+ stale merged branches in the repository (zeroclaw-labs/zeroclaw Issue #6715).

### 8. Backlog Watch
A significant backlog of `status:blocked` and `needs-maintainer-review` items is apparent. These issues represent unmet contributor expectations and potential bottlenecks:
- **Dormant Features:** The “Subscription-native OAuth” (zeroclaw-labs/zeroclaw Issue #5601, Apr 10) and “Lighter ZeroClaw core” (zeroclaw-labs/zeroclaw Issue #6165, Apr 27) RFCs have been blocked for over a month without maintainer direction.
- **Blocked Security Enhancements:** Detailed RFCs for `allowed_tools` enforcement (zeroclaw-labs/zeroclaw Issue #6914), Skill-scoped tool activation (zeroclaw-labs/zeroclaw Issue #6915), and Composio action filters (zeroclaw-labs/zeroclaw Issue #6917) remain in limbo despite having clear technical specifications.
- **Project Hygiene:** An explicit request to clean up stale branches (zeroclaw-labs/zeroclaw Issue #6715) and a call to establish a standardized CI/CD container build pipeline (zeroclaw-labs/zeroclaw Issue #5908) are stalled. Addressing these could significantly lower the barrier to entry for new contributors.
- **Risk Assessment:** While the core team is highly productive on the v0.9.0 roadmap, the growing list of `needs-maintainer-review` items suggests that community contributions are outpacing triage capacity, creating a latent risk of contributor frustration if left unaddressed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*