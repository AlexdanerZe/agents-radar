# OpenClaw Ecosystem Digest 2026-06-01

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-01 03:42 UTC

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

Here is a structured project digest for OpenClaw based on the provided data for 2026-06-01.

---

## OpenClaw Project Digest | 2026-06-01

### 1. Today’s Overview
OpenClaw saw an extremely high volume of activity in the last 24 hours, with **500 Issues** and **500 Pull Requests** updated. The core team shipped an aggressive hotfix cycle, releasing **four beta versions** (v2026.5.31-beta.1 through beta.4) all concentrating on the same resilience and recovery issues. While the triage throughput is impressive—over 220 issues closed and 280 PRs merged/closed in a single day—the identical release notes across the four betas suggest a specific, stubborn stability bug cluster that required multiple deployment attempts to fully resolve. The overall project health is strong, but the project is clearly in an intense stabilization phase following the deployment of Codex and Active Memory features.

### 2. Releases
**Four new releases today:** `v2026.5.31-beta.1`, `beta.2`, `beta.3`, and `beta.4`.

All four releases share identical highlights:
- **Agents & CLI Runtimes:** Improved recovery from interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries. (Refs: #88129, #88136, #88141, #88162, #88182)
- **Channels:** Steadier delivery across Telegram, WhatsApp, iMessage, and Slack.

**Assessment:** The unified highlight text across four distinct builds implies a rolling hotfix cycle where the team iterated rapidly on the same regressions without introducing discrete new features. Users on the `2026.5.22` stable release should pay close attention to this patch series if they are experiencing Codex or channel delivery issues.

### 3. Project Progress
In the last 24 hours, **283 PRs were merged/closed** and **224 Issues were resolved**. Notable fixes and progressions include:

- **Subagent Regression Fixed:** The major subagent regression introduced in `2026.5.7` has been resolved ([Issue #81214](https://github.com/openclaw/openclaw/issues/81214)).
- **Anthropic Thinking Signature Crash Patched:** A hard session failure caused by expired `thinking block` signatures has been closed ([Issue #88020](https://github.com/openclaw/openclaw/issues/88020)).
- **Gateway Restart Bug Closed:** The critical bug where an `auth.cooldowns` config change forced a full gateway restart (dropping in-flight CLI runs) was addressed ([Issue #88443](https://github.com/openclaw/openclaw/issues/88443)).
- **Azure/Mattermost Fixes Merged:** PRs resolving `non_deliverable_terminal_turn` errors on Azure Responses ([#88893](https://github.com/openclaw/openclaw/pull/88893)) and fixing attachment handling for Mattermost ([#88859](https://github.com/openclaw/openclaw/pull/88859)) have been closed.
- **Tool Schema & Null Handling:** The `fix(agents)` PR series advanced, improving how nullable and literal-union tool schemas are projected to providers ([#88880](https://github.com/openclaw/openclaw/pull/88880)).
- **Documentation Push:** A significant documentation effort covers markdown rendering contracts ([#88875](https://github.com/openclaw/openclaw/pull/88875)), recovery cards for subagents ([#88886](https://github.com/openclaw/openclaw/pull/88886)), and Feishu raw-mode card fallbacks ([#88894](https://github.com/openclaw/openclaw/pull/88894)).

### 4. Community Hot Topics
- **Nextcloud Talk & Codex Plugin Approval Stalls ([Issue #86047](https://github.com/openclaw/openclaw/issues/86047)):** A high-engagement P1 regression on `2026.5.22` where Codex app-server approvals stall causes interrupted turns. Filed by an AI agent after the user rolled back. (3👍, 7 comments)
- **Matrix Thread Replies Broken ([Issue #87307](https://github.com/openclaw/openclaw/issues/87307)):** Users are highly active (11 comments) debugging why bot replies are sent as normal messages instead of thread replies after upgrading to `2026.5.22`.
- **Feishu Group Messaging Broken ([Issue #77666](https://github.com/openclaw/openclaw/issues/77666)):** The highest-reacted open issue (4👍). Group messages are received but replies are 0 after upgrading to `2026.5.3`. A deep frustration for the Asian user base.
- **Pre-Response Enforcement Hooks ([Issue #13583](https://github.com/openclaw/openclaw/issues/13583)):** This long-standing feature request for "hard gates" on tool calls continues to attract attention (11 comments, 2👍), driven by demand from high-stakes operations workflows.
- **MCP Channel-Mediated Approval ([Issue #78308](https://github.com/openclaw/openclaw/issues/78308)):** A key roadmap item with high community desire for standardizing approval envelopes for MCP tool calls.

### 5. Bugs & Stability
**Critical / P1 Remaining:**
- **Codex App-Server Stability:** The Codex runtime remains the primary source of critical bugs. Issues #83959 (retry exhaustion), #85251 (silent turn completion), and #86996 (latency + hook timeouts) are all unresolved P1s directly impacting user workflows.
- **Session Context Confusion ([Issue #32296](https://github.com/openclaw/openclaw/issues/32296)):** A long-standing P1 (13 comments) where agents reply to previous messages. Updated today, indicating no fix is imminent.
- **Auth Router & Cooldowns:** Issue #67423 reveals the auth router ignores provider `apiKey` fields, and #87616 shows timeouts with local LM Studio are sharp (3s) despite extended configs.

**Regressions & Recent Introductions:**
- **Matrix Threads:** P1 regression still open ([#87307](https://github.com/openclaw/openclaw/issues/87307)).
- **OpenAI Responses 404:** Fixed today ([#88499](https://github.com/openclaw/openclaw/issues/88499)).
- **Telegram Group Reply Routing:** Users report replies sent to DM chat_ids instead of groups ([#79308](https://github.com/openclaw/openclaw/issues/79308)).
- **Slack Event Loop Blocking:** A high-severity Windows issue where Slack startup blocks the gateway for 5+ minutes is noted as stale but unclosed ([#78435](https://github.com/openclaw/openclaw/issues/78435)).

**Fix PRs in Flight:**
- `fix(feishu): restore full-text streaming` ([#88597](https://github.com/openclaw/openclaw/pull/88597)) — P1, maintainer look.
- `fix(codex): quarantine unreadable dynamic tools` ([#88774](https://github.com/openclaw/openclaw/pull/88774)) — Prevents malformed plugins from crashing the turn.

### 6. Feature Requests & Roadmap Signals
- **Policy & Compliance Framework:** The "policy" series of PRs (#87056, #87074, #87081) by maintainer `giodl73-repo` is maturing. Data handling conformance checks and strict key validation indicate a major push towards enterprise governance capabilities.
- **Cost Telemetry ([PR #86029](https://github.com/openclaw/openclaw/pull/86029)):** An active PR surfaces `costUsd`, `provider`, and `model` in the `agent.wait` response. This is a strong signal that financial observability is entering the stable roadmap.
- **Tiered Bootstrap Loading ([PR #22439](https://github.com/openclaw/openclaw/pull/22439)):** This massive PR, open since February, addresses the top user complaint of context window waste. It was updated today and is in the "needs proof" stage. It is a likely candidate for the next minor release.
- **Voice-as-IO for Discord ([Issue #73699](https://github.com/openclaw/openclaw/issues/73699)):** A closed feature request for bridging Discord voice to text channels signals that multimodal/QoL features are being reviewed, even if not immediately scheduled.
- **I18n for Slash Commands ([Issue #79458](https://github.com/openclaw/openclaw/issues/79458)):** A strongly-upvoted community need for localized slash command descriptions (specifically for Chinese-speaking users).

### 7. User Feedback Summary
- **Pain Points:**
    - **High Latency on Codex:** Users report trivial turns taking 25.9s on the Codex native runtime ([Issue #78947](https://github.com/openclaw/openclaw/issues/78947)).
    - **Plugin Debugging Hell:** Plugin loaders silently failing on invalid contracts costs users "hours of debugging" ([Issue #78301](https://github.com/openclaw/openclaw/issues/78301)).
    - **Browser Plugin Fragility:** The `chrome-mcp` browser plugin frequently fails with `targetId mismatch` and `AbortError` during cron runs ([Issue #78602](https://github.com/openclaw/openclaw/issues/78602)).
    - **Configuration Schema Churn:** The GHCR image rejecting `channels.discord.streaming.progress.commentary` despite source support ([Issue #88788](https://github.com/openclaw/openclaw/issues/88788)) is a frustrating deployment hurdle.
- **Desires:**
    - **Stability Over New Features:** The nature of the conversation (rollbacks, regressions, identical hotfix betas) suggests a strong user desire for a hardened "Long Term Support" release.
    - **Tool Call Control:** High demand for sub-agent tool allowlists (featured in #78441) and hard enforcement gates (#13583).

### 8. Backlog Watch
- **[feat(workspace): Tiered Bootstrap Loading (PR #22439)](https://github.com/openclaw/openclaw/pull/22439):** Open since Feb 21. A massive, critical feature that directly tackles context window pressure. Updated today but still flagged as "needs proof". High risk, high reward for the next major release.
- **[Feature: Pre-response Enforcement Hooks (Issue #13583)](https://github.com/openclaw/openclaw/issues/13583):** Open since Feb 10. Requires a product decision. This feature unlocks enterprise use-cases (quant/finance/security) but is blocked on design consensus.
- **[Feature: MCP Consent Envelope (Issue #78308)](https://github.com/openclaw/openclaw/issues/78308):** Open since May 6, stale. A massive security improvement for MCP tool calls that has been sitting without a fix PR for nearly a month.
- **[Bug: Gateway fail-fast on missing probe auth (PR #68280)](https://github.com/openclaw/openclaw/pull/68280):** Open since Apr 17. A security hardening PR that has not received maintainer approval.
- **[Bug: Plugin Loader Silent Failures (Issue #78301)](https://github.com/openclaw/openclaw/issues/78301):** Open (stale). This issue has high developer experience impact but lacks a linked fix PR.

---

*Generated by an analyst in training based on public GitHub metadata from OpenClaw.*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest data for June 1, 2026.

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem on June 1, 2026, is operating at an unprecedented scale, characterized by a clear "barbell" effect. At one end, massive projects like OpenClaw are grinding through post-feature-launch stabilization with intense hotfix cycles; at the other, a wave of niche and platform-specific projects (CoPaw, NanoClaw, PicoClaw) are rapidly adding enterprise capabilities, channels, and extensions. The universal community demand has shifted decisively from feature velocity to production-grade reliability, with MCP scaling, autonomous execution trust, and provider parity emerging as the defining competitive benchmarks. Projects that can bridge the gap between rapid iteration and enterprise hardening are the ones generating the strongest community retention signals.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Today | Ecosystem Health Signal |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 4x Beta | Hyper-scale stabilization / Firefighting |
| **Hermes Agent** | 50 | 50 | None | High-velocity stabilization sprint |
| **ZeroClaw** | 30 | 50 | None | Strong, balanced feature/stability |
| **CoPaw** | 27 | 11 | None | Scaling pains, high engagement |
| **IronClaw** | 3 | 26 | None | Strong, heavy architectural rebuild |
| **NanoBot** | 6 | 19 | None | Strong, security & hardening focus |
| **NanoClaw** | 3 | 8 | None | Moderate, operational hardening |
| **PicoClaw** | 6 | 10 | Nightly | Strong, community-driven fixes |
| **LobsterAI** | 1 | 2 | None | Low activity, billing friction |
| **Moltis** | 0 | 1 | None | Stable, quiet internal hardening |
| **NullClaw** | 2 | 0 | None | Low cadence, critical bugs |
| **ZeptoClaw** | 1 | 0 | None | Stable, quiet security audit |
| **TinyClaw** | 0 | 0 | None | Dormant |

---

## 3. OpenClaw's Position

OpenClaw retains its role as the undisputed reference implementation and largest community anchor, processing an order of magnitude more daily activity than any peer (500 Issues/PRs alone). Its technical approach is the most aggressive in the ecosystem, simultaneously pushing Polymorphic Channels, a custom Codex native runtime, and a maturing Policy-as-Code framework for enterprise governance. This breadth is double-edged: it gives OpenClaw the widest surface area and fastest triage, but the identical release notes across four beta builds signals a project navigating stubborn stability regressions under the weight of its own ambition. The strong community demand for a hardened "LTS" release contrasts sharply with the "move fast and fix things" velocity of peers like ZeroClaw and NanoBot, who are shipping more focused, stable builds in the same window. OpenClaw’s community is the deepest, but its complexity cost is the highest.

---

## 4. Shared Technical Focus Areas

Several critical requirements are emerging across multiple projects simultaneously, representing the ecosystem’s current technical consensus on what matters most:

- **MCP Infrastructure Scaling (ALL Major Projects):** This is the universal pain point. CoPaw (process explosion, SharedMCPPool), NanoClaw (HTTP/SSE transport diversification), IronClaw (stdio activation bugs), and ZeroClaw (resource/prompt support) are all finding that the first generation of MCP integrations doesn't scale to multi-agent, production deployments. **Security approval envelopes** (OpenClaw, CoPaw) are a rapidly emerging sub-theme.

- **Codex & Provider Reliability (OpenClaw, Hermes, PicoClaw):** Keeping pace with the rapidly iterating OpenAI API (gpt-5.5, OAuth changes, streaming edge cases) is a shared burden. Hermes Agent explicitly bypasses the OpenAI SDK for SSE streaming; PicoClaw overhauls OAuth response handling; OpenClaw patches thinking block signatures. Single-provider fragility is a stark risk.

- **Autonomous Execution Trust (NullClaw, CoPaw, ZeroClaw, NanoBot):** The reliability of scheduled agent tasks ("cron") is the ecosystem's current benchmark for trust. Silent failures—NullClaw subprocesses not spawning, CoPaw producing empty execution traces, ZeroClaw failing to route cron output—are the highest-severity bugs being reported. The community wants "set-and-forget," and every project is struggling to deliver it.

- **Enterprise Security & Auth (NanoBot, IronClaw, ZeroClaw, OpenClaw):** SSO integrations (Azure AAD in NanoBot, GitHub GSuite in IronClaw) and Role-Based Access Control (ZeroClaw, OpenClaw) are becoming baseline requirements. The volume of security hardening PRs (WebSocket auth, path traversal, SSRF guards) across the board signals that production deployments are now the norm.

- **Platform Parity, Especially Windows (CoPaw, Hermes, ZeroClaw):** Windows-specific regressions—CMD window flashes, silent gateway failures, pip upgrade ghost files—consistently create high-friction UX gaps for deployed agents. This remains a strong signal that the ecosystem's testing infrastructure is developer-macOS-heavy.

---

## 5. Differentiation Analysis

The landscape reveals sharp architectural and demographic fault lines:

- **Language & Performance Layer:**
  - **Rust-native** (ZeroClaw, IronClaw, ZeptoClaw) prioritize performance, binary portability, and system-level reliability.
  - **Python-heavy** (NanoBot) lead in ML-native integrations (RAG, ASR, heavy data science).
  - **TypeScript/Node.js** (NanoClaw) favor MCP ecosystem velocity and rapid prototyping.

- **Target User Profiles:**
  - **OpenClaw:** The "general operating system" for agents. Broadest channel and plugin coverage. Caters to power users willing to tolerate complexity.
  - **ZeroClaw / IronClaw:** Developer-centric, performance-sensitive, enterprise infrastructure. Rust gives them a distinct edge in hardware integration (ESP32) and low-latency trigger architecture.
  - **CoPaw:** Deep ecosystem play for the Chinese enterprise/cross-platform market (WeWork, QQ, DingTalk, Feishu). Agentscope 2.0 migration is a bet on multi-agent scaffolding.
  - **Hermes Agent:** Multi-platform creator focus (Discord video, Feishu streaming, Telegram). High emphasis on media modality parity.
  - **NanoBot:** Researcher / personal knowledge management. Strongest signal on memory persistence (RAG) and goal execution.
  - **PicoClaw / NanoClaw:** Lightweight, mobile, or developer companion tools (Termux, Claude Code integration, local models).

- **Architectural Velocity:**
  - **Ground-up Rebuild:** IronClaw ("Reborn" architecture).
  - **Foundation Refactoring:** CoPaw (Agentscope 2.0), NanoBot (Gateway refactor).
  - **Feature Layer Focused:** ZeroClaw (Skills UX, Integration Pipelines).
  - **Stabilization / Firefighting:** OpenClaw, Hermes Agent.

---

## 6. Community Momentum & Maturity

The ecosystem divides into four clear momentum tiers:

- **Tier 1: Hyper-Scale Stabilization**
  - **OpenClaw** is navigating post-feature launch turbulence with unmatched volume. The identical beta release notes signal a project in a brute-force hotfix cycle. Its community is the largest, but its satisfaction metrics are the most volatile (rollbacks, identical patches).

- **Tier 2: High-Velocity Feature + Stability**
  - **ZeroClaw, Hermes Agent, CoPaw, IronClaw, NanoBot** are adding significant new subsystems (MCP transport, channel adapters, authentication frameworks) while maintaining rapid closure of critical bugs. These projects are in a "build and lock down" cadence. CoPaw is under the most visible scaling strain (MCP process explosion), but its community engagement is exceptionally high.

- **Tier 3: Steady / Targeted Iteration**
  - **PicoClaw, Moltis, LobsterAI** are adding targeted features and fixes without the heavy firefighting of Tier 1. These are building stable bases in their respective niches.

- **Tier 4: Low Cadence / Specialized**
  - **NullClaw, ZeptoClaw, TinyClaw** show minimal development throughput. ZeptoClaw is executing on internal security audits; NullClaw is reacting to specific critical bugs. These risk falling behind on ecosystem interoperability standards (MCP, Codex compatibility) without an infusion of development velocity.

---

## 7. Trend Signals

The aggregated community feedback across all projects reveals several strong, actionable industry trends for AI agent developers:

1.  **The "Set-and-Forget" Reliability Threshold is the New Table Stakes:**
    The single highest-value signal is the demand for trust in autonomous schedules. The projects that effectively communicate and close silent failure modes (NullClaw #941, CoPaw #4818, ZeroClaw #6647) will win the production deployment battle. Developers must invest heavily in heartbeat monitoring, delivery confirmation chains, and self-healing infrastructure before adding new channels or features.

2.  **MCP is the Integration Standard, but Scaling it is the Next Frontier:**
    MCP adoption is universal, but the conversation has shifted from "how to connect" to "how to pool, secure, and scale MCP processes across hundreds of agents." Security envelopes (consent, approval), transport diversity (stdio vs. HTTP/SSE), and process deduplication (CoPaw's SharedMCPPool) are the critical battlegrounds for the next release cycle.

3.  **Enterprise Security is Being Baked into the Core API, Not Bolted On:**
    The volume of PRs hardening WS auth, path traversal, SSRF, and MCP consent indicates that the agent platform "toy" phase is over. RBAC, audit logging, and SSO (ZeroClaw #5982, NanoBot #4126, IronClaw #4229) are becoming baseline requirements for the enterprise adoption wave. Developers who delay this will face a painful retrofit.

4.  **Provider Fragmentation is a Structural Risk that Requires Active Mitigation:**
    Single-point-of-failure in API providers is a recurring pain point. The community demands robust fallback, multi-provider parity gates, and local model support as a hedge against API instability and cost volatility. Projects investing in provider abstraction layers (ZeroClaw #5937) are building a durable competitive moat.

5.  **Context Management is Over; Persistent Memory is the New Benchmark:**
    The industry has clearly moved past simple context window management. "Active Memory" (OpenClaw), "RAG for Memory" (NanoBot), and session size capping (Moltis) are shifting from differentiators to infrastructure requirements for managing long-running, context-intensive agent interactions.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot Project Digest — 2026-06-01

### 1. Today’s Overview

NanoBot saw a highly productive day with **19 PRs updated** (12 open, 7 merged/closed) and **6 Issues updated** (4 closed, 2 open), indicating strong developer velocity and rapid triage. The majority of activity centered on **security hardening** (WebSocket auth, symlink escapes, SSRF guards, heartbeat fail-closed logic), **WebUI reliability** (fixing a white-screen crash), and **enterprise-readiness** (Azure AAD auth, RAG memory). The breadth of contributions—from refactors of core internals to audio transcription support—signals a project maturing rapidly across infrastructure, user experience, and compliance. Community engagement remains high, with several feature PRs visibly moving toward merge.

### 2. Releases

No new releases were published in the last 24 hours. The project is in a dense feature iteration cycle between formal version tags.

### 3. Project Progress (Merged/Closed PRs)

Seven PRs were closed or merged today, spanning three focus areas:

- **Security & Reliability**
  - PR [#4127](https://github.com/HKUDS/nanobot/pull/4127) (`fix(agent): extend sustained goal iteration budget`): Improves `/goal` workflow robustness by allowing continuation past the normal tool-call iteration budget.
  - PR [#4112](https://github.com/HKUDS/nanobot/pull/4112) / [#4114](https://github.com/HKUDS/nanobot/pull/4114) (`fix(heartbeat)`): Heartbeat task now fails closed, suppressing false “All clear.” deliveries and skipping empty HEARTBEAT.md files. Closes issue [#4111](https://github.com/HKUDS/nanobot/issues/4111).
  - PR [#4103](https://github.com/HKUDS/nanobot/pull/4103) (`Require auth for WebSocket token issuance`): Prevents unauthenticated minting of short-lived WS tokens when a static token is configured. Closes security issue [#4077](https://github.com/HKUDS/nanobot/issues/4077).

- **WebUI**
  - PR [#4121](https://github.com/HKUDS/nanobot/pull/4121) (`feat(webui): polish chat rendering and host runtime`): Stabilizes streamed assistant output, reasoning delta blocks, and file edit actions.
  - PR [#4117](https://github.com/HKUDS/nanobot/pull/4117) (`fix(webui): handle undefined language in code blocks`): Fixes white-screen crash on code blocks without a language specifier. Closes [#4116](https://github.com/HKUDS/nanobot/issues/4116).

- **Other**
  - PR [#4118](https://github.com/HKUDS/nanobot/pull/4118) (test push, closed).

### 4. Community Hot Topics

The most conversation-driving items reflect **enterprise integration** and **user control over agent autonomy**:

- **[Issue #4120](https://github.com/HKUDS/nanobot/issues/4120) (Closed)** — *Vest MCP Integration / Monetization Angle*: The only issue with explicit replies; an external vendor proposed a tool-recommendation integration atop NanoBot’s MCP framework. This signals growing commercial interest in the ecosystem and a potential partner channel.
- **[PR #1443](https://github.com/HKUDS/nanobot/pull/1443) (Open, 3 months old)** — *Decouple heartbeat reasoning from notification*: Continues to receive updates and attention. It captures a long-running community desire to quiet the agent’s autonomous heartbeat to avoid unwanted message delivery.
- **[Issue #4125](https://github.com/HKUDS/nanobot/issues/4125) / [PR #4126](https://github.com/HKUDS/nanobot/pull/4126)** — *Azure AAD Authentication*: The linked pair shows strong demand for enterprise-grade auth, a must-have for MS ecosystem deployments.

**Underlying need**: Users are pushing beyond single-user toy scenarios into secure, compliant, federated team deployments where the agent must be both autonomous and unobtrusive.

### 5. Bugs & Stability

Bugs reported today span a range of severities, with several already accompanied by fix PRs:

| Severity | Issue | Summary | Fix Status |
|----------|-------|---------|------------|
| **High** | [#4128](https://github.com/HKUDS/nanobot/issues/4128) | `retain_recent_legal_suffix` causes duplicate user message archiving and inconsistent LLM context | PR [#4129](https://github.com/HKUDS/nanobot/pull/4129) (open) |
| **Medium** | [#4111](https://github.com/HKUDS/nanobot/issues/4111) | Heartbeat cron falsely sends “All clear.” to Feishu when no task is present | Fixed in [#4112](https://github.com/HKUDS/nanobot/pull/4112) / [#4114](https://github.com/HKUDS/nanobot/pull/4114) |
| **High** | [#4116](https://github.com/HKUDS/nanobot/issues/4116) | WebUI white-screen crash on code blocks without language specifier | Fixed in [#4117](https://github.com/HKUDS/nanobot/pull/4117) |
| **Medium** | [#4124](https://github.com/HKUDS/nanobot/issues/4124) | XML tool calls from non-standard models (mimo, glm) leak raw XML to chat channels | PR [#4124](https://github.com/HKUDS/nanobot/pull/4124) (open) |
| **High (Security)** | [#4077](https://github.com/HKUDS/nanobot/issues/4077) | Unauthenticated WebSocket token issuance | Fixed in [#4103](https://github.com/HKUDS/nanobot/pull/4103) |

Contributors are actively working on the remaining open bugs (#4124, #4128), maintaining the project’s pattern of same-day or next-day patch coverage.

### 6. Feature Requests & Roadmap Signals

Several open PRs reveal the direction of the next release:

- **Memory/Intelligence**: PR [#4109](https://github.com/HKUDS/nanobot/pull/4109) *(feat: Add lightweight RAG for memory retrieval)* is a high-impact feature likely to land soon, moving beyond context-window-only memory to persistent, retrieval-augmented knowledge.
- **Enterprise Auth**: PR [#4126](https://github.com/HKUDS/nanobot/pull/4126) adds Azure AAD/Azure Identity–based auth for the OpenAI provider, responding to strict subscription policies.
- **Multimodal / UX**: PR [#4122](https://github.com/HKUDS/nanobot/pull/4122) brings voice recording and local ASR (FunASR) to the WebUI composer.
- **Architecture**: PR [#4115](https://github.com/HKUDS/nanobot/pull/4115) extracts `GatewayHTTPHandler` from WebSocket channels, a prerequisite for hot-reload and cleaner agent-loop decoupling. PR [#3990](https://github.com/HKUDS/nanobot/pull/3990) refactors the Dream module away from a heavy two-phase class.

**Prediction**: The next minor release will likely bundle the RAG memory backend, Azure AAD auth, and the Gateway refactor—collectively shifting NanoBot substantially toward production-level team/enterprise use.

### 7. User Feedback Summary

User signals from the data reveal a **sophisticated, deployment-focused community**:

- **Pain Points**: Enterprise identity constraints (Azure AAD missing), insufficient control over autonomous agent chatter (Heartbeat), context management bugs, and edge-case WebUI hangs are the primary friction points.
- **Satisfaction Indicators**: High confidence in maintainer response—crashes are fixed within hours, security reports are merged same-day. The willingness to file detailed bug reports (including Chinese-language architecture analysis in #4128) implies deep user investment.
- **Use Cases**: MCP tool chaining, persistent goal execution (`/goal`), headless Telegram/Feishu operation, and heavy filesystem interaction all feature prominently.

**Overall**: Users are pushing NanoBot into demanding production roles and are generally satisfied with the project’s velocity and transparency, even as they encounter the inevitable rough edges of rapid development.

### 8. Backlog Watch

A few items stand out as needing maintainer attention or strategic decision:

- **[PR #1443](https://github.com/HKUDS/nanobot/pull/1443)** — *Decouple heartbeat reasoning from notification* (Opened 2026-03-02, ~3 months old). A mature feature PR that conflicts philosophically with the newly merged “fail-closed” heartbeat fixes. The maintainers should decide whether to merge it, close it, or reframe its approach.
- **[PR #3990](https://github.com/HKUDS/nanobot/pull/3990)** — *Refactor Dream class to cron + process_direct* (Opened 2026-05-24, ~1 week old). A substantial refactor that strips ~315 lines. Needs review sign-off to avoid bitrotting while other features land.
- **Security PR Cluster**: [#4099](https://github.com/HKUDS/nanobot/pull/4099) (read-only extra roots), [#4101](https://github.com/HKUDS/nanobot/pull/4101) (Dream skill ownership), [#4119](https://github.com/HKUDS/nanobot/pull/4119) (symlink escapes), and [#4123](https://github.com/HKUDS/nanobot/pull/4123) (MCP SSRF guard) are all open and awaiting merge. Closing this cluster would provide a strong security baseline for the next release.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-01

## Today’s Overview
Hermes Agent saw intense activity today with **50 issues and 50 pull requests updated**, signaling a project in a high-velocity stabilization sprint following the v0.14.0 release. No new version was tagged, but six PRs were merged, mainly around Docker infrastructure improvements for the s6-overlay migration. The community and maintainers remain deeply focused on resolving OpenAI Codex/gpt-5.5 reliability gaps and first-party API compatibility (Anthropic, Bedrock). At the same time, several critical regressions — a dashboard update button destroying cron jobs, CLI terminal freezes, and a Windows gateway restart failure — indicate that the update/migration path is currently a pain point. The project is clearly scaling its platform coverage (Discord, Feishu, Windows) but is navigating a phase of elevated churn.

## Releases
None

## Project Progress *(Merged/Closed PRs Today)*
Six PRs were merged or closed today, with heavy emphasis on Docker infrastructure and configuration hardening:
- **[#34382](NousResearch/hermes-agent PR #34382)** – `fix(docker): add /usr/bin/tini compatibility shim for legacy wrappers`. Resolves the Hostinger VPS migration crash (`#34192`) caused by the switch from tini to s6-overlay.
- **[#34268](NousResearch/hermes-agent PR #34268)** – `fix(config): chown ensure_hermes_home dirs to HERMES_UID/GID in Docker`. Prevents permission errors on subdirectories created at runtime for profile namespaces.
- **[#34554](NousResearch/hermes-agent Issue #34554)** – *CLOSED* – P1 bug for Claude Opus 4.8 schema changes (`thinking.type.enabled` rejection).
- **[#32423](NousResearch/hermes-agent Issue #32423)** – *CLOSED* – Context window regression after interrupted compaction.
- **[#34339](NousResearch/hermes-agent Issue #34339)** – *CLOSED* – Gateway auto-start failure after tini-to-s6 image upgrade.
- **[#35025](NousResearch/hermes-agent Issue #35025)** – *CLOSED* – Docker excessive `chown` on every boot when using non-default UID.

## Community Hot Topics
- **OpenAI Codex/gpt-5.5 Unreliability (Top Issue)**
  – **[#33075](NousResearch/hermes-agent Issue #33075)** (CLOSED today, 14 comments, 11 👍): Users report that Hermes v0.14.0 with `openai-codex` / `gpt-5.5` hits `APIConnectionError`/TTFB timeouts repeatedly while the official Codex CLI works fine. A direct follow-up fix PR was opened today: **[#36217](NousResearch/hermes-agent PR #36217)** ("Fix Codex gpt-5.5 stream stalls"), which bypasses the OpenAI SDK stream wrapper and consumes SSE directly via `httpx`. Long-running issue **[#13834](NousResearch/hermes-agent Issue #13834)** (8 comments) underscores the community frustration: the same machine/network that works with the official CLI fails with Hermes.
  *Underlying Need:* Strict behavior parity with the official Codex CLI and robust SSE/stream handling.

- **Agent-Native Task Relay RFC**
  – **[#31392](NousResearch/hermes-agent Issue #31392)** (7 comments): An RFC by *leavedrop* proposing auto-forking subagents with async human approval gates. This reflects a power-user desire for more complex, supervised, parallel task orchestration beyond the current delegation model.

- **Cross-Device Cloud Sync**
  – **[#20510](NousResearch/hermes-agent Issue #20510)** (4 comments, 9 👍): Strong demand for syncing config, profiles, memory, and cron jobs across devices. This is consistently one of the most upvoted open features.

## Bugs & Stability
**Critical / High Impact (P1)**
- **Bedrock Opus 4.8 Sampling Params**
  – **[#36151](NousResearch/hermes-agent Issue #36151)** (reported today, 3 comments): Opus 4.7/4.8 on Bedrock Converse rejects `temperature`/`top_p`. The `_forbids_sampling_params` guard from `anthropic_adapter.py` was never applied to the Bedrock path. No fix PR yet.
- **Anthropic 15-Minute Stream Hang**
  – **[#33855](NousResearch/hermes-agent PR #33855)** (PR open, P1): A stuck streaming response on the Anthropic-native path hangs the worker for ~900s. The proposed fix skips the primary OpenAI client swap on stale stream retry.
- **Dashboard Update Destroys Cron Jobs**
  – **[#25281](NousResearch/hermes-agent Issue #25281)** (P1, OPEN): Pressing "Update Hermes" in the dashboard completely wipes all scheduled cron jobs. Major platform reliability issue.

**Major / Moderate Impact (P2)**
- **Windows Gateway Restart Failure**
  – **[#36213](NousResearch/hermes-agent Issue #36213)** (reported today) / PR fix **[#36223](NousResearch/hermes-agent PR #36223)** (by *Pluviobyte*): Gateway restart on Windows does not verify old process termination, causing silent port-binding failure.
- **CLI Freeze on Slash Commands**
  – **[#33961](NousResearch/hermes-agent Issue #33961)** (5 comments): `/new`, `/clear`, and `/reset` freeze the terminal, requiring a full process kill.
- **Agent Session HOME Path Points to Profile**
  – **[#36144](NousResearch/hermes-agent Issue #36144)** (reported today): Tools resolve `~` to the Hermes profile directory instead of the user's actual home, breaking file tools and CLIs.
- **Cron API Endpoint Mismatch (UI Broken)**
  – **[#36149](NousResearch/hermes-agent Issue #36149)** (reported today): Frontend requests `GET /api/cron/jobs`; backend defines `GET /api/jobs`. The Schedules UI component is non-functional.
- **Docker: `hermes update` Fails Inside Container**
  – **[#35835](NousResearch/hermes-agent Issue #35835)** (OPEN): Update command does not work in non-published containers.
- **Discord Tool-Using Responses Dropped**
  – **[#33842](NousResearch/hermes-agent PR #33842)** (PR open): Tool-using replies (`api_calls >= 2`) were silently dropped on Discord.

**Minor / Edge Case (P3)**
- **[#31263](NousResearch/hermes-agent Issue #31263)**: Holographic memory context injection never fires (2 comments).
- **[#31144](NousResearch/hermes-agent Issue #31144)**: `.env` loading path disagrees with `hermes config show` on Windows.

## Feature Requests & Roadmap Signals
- **Likely for v0.15.0:**
  - **Video Analysis Support**
    – **[#36224](NousResearch/hermes-agent PR #36224)** (opened today): Adds `video_analyze` support for Discord and all platforms. Fixes triple-point video dropping in the Discord pipeline. A major modality expansion.
  - **Context Compression Memory Ledger**
    – **[#36222](NousResearch/hermes-agent PR #36222)** (by *KeyArgo*): Opt-in compression memory persistence on top of segment summaries. Hardens provider, gateway, and session-scope edge cases.
  - **Feishu Streaming Cards**
    – **[#36202](NousResearch/hermes-agent PR #36202)** (by *Mxin-9527*): Migrates Feishu bot responses from full PATCH updates to CardKit native streaming, eliminating "edited" badges and rate limits.
  - **MiniMax-M3 Provider Support**
    – **[#36212](NousResearch/hermes-agent PR #36212)** (opened today): Adds M3 and highspeed variants to the direct MiniMax provider list.

- **High Community Demand (Timeline Unclear):**
  - **Cloud Sync** ([#20510](NousResearch/hermes-agent Issue #20510), 9 👍).
  - **Auto-discover Models** from custom endpoints ([#10011](NousResearch/hermes-agent Issue #10011), 3 👍).
  - **Multi-Profile Dashboard** to surface cron jobs across all profiles ([#20622](NousResearch/hermes-agent Issue #20622)).
  - **Native Mobile App** for iOS & Android with voice calling ([#11911](NousResearch/hermes-agent Issue #11911)).

## User Feedback Summary
**Satisfaction Indicators:**
- The community is actively contributing complex upstream features — *leavedrop*’s task relay RFC and *Mxin-9527*’s Feishu streaming cards signal deep engagement from technically sophisticated users.
- Multi-platform parity (Discord video, Feishu streaming, Windows fixes) is being aggressively pursued, matching explicit user asks.

**Pain Points / Dissatisfaction:**
- **OpenAI Codex Gap:** The persistent gap between Hermes' Codex support and the official CLI is the most commented-on issue. Users explicitly compare the two, eroding confidence in Hermes as a primary Codex client.
- **Upgrade Regressions:** The cron-deletion-on-update bug (#25281) and Docker s6 migration breakage (#34339, #35835) suggest the update pipeline lacks sufficient integration testing.
- **Environment & Config Friction:** Users on Windows and macOS are hitting confusing divergences between `.env` loading, `HOME` resolution, and config display.
- **Session Reliability:** Issues around background cancellation (#36184), memory injection not firing (#31263), and context window changes (#32423) indicate that long-running session state management still has rough edges.

## Backlog Watch
- **Bedrock CachePoint Injection (P1, 45 days open)**
  – **[#11970](NousResearch/hermes-agent Issue #11970)** (by *aws-yz*): The Bedrock Converse path never sends `cachePoint` markers, so prompt caching is silently disabled. Users on Bedrock pay full input-token cost every turn. No fix PR exists.
- **Bedrock Bearer Token Auth (P2, 20 days, PR waiting)**
  – **[#24507](NousResearch/hermes-agent PR #24507)** (by *JustinOhms*): Claude requests fail with `Could not resolve credentials from session` when using `AWS_BEARER_TOKEN_BEDROCK`. A fix PR has been open since May 12 without being merged.
- **Auto-Discover Models (Feature, 47 days stale)**
  – **[#10011](NousResearch/hermes-agent Issue #10011)** (3 👍, 3 comments): Feature request to auto-discover models from custom provider endpoints. No maintainer response.
- **Holographic Memory Not Firing (P3, 8 days)**
  – **[#31263](NousResearch/hermes-agent Issue #31263)** (by *ea98989*): Reported for v0.14.0 with detailed environment info. No triage response yet.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for June 1, 2026.

---

## 1. Today’s Overview
PicoClaw remains in an active development cycle, with 6 issues and 10 pull requests updated in the last 24 hours. A new nightly build was released, and the team merged a critical fix for the OpenAI Codex OAuth provider that was heavily impacting users. Concurrently, the community submitted several high-quality feature PRs around the `cron` tool, Telegram channel integration, and Anthropic provider compatibility. While provider stability is the dominant theme today, the volume of new contributions suggests a healthy balance between bug fixing and feature expansion.

## 2. Releases
A single new release was tagged today:
- **`v0.2.9-nightly.20260601.ba806592`**: An automated nightly build from the `main` branch. The release notes warn that this build "may be unstable" and should be used with caution.
- **Changelog**: Compare with the previous stable (`v0.2.9`) at [GitHub Comparison](https://github.com/sipeed/picoclaw/compare/v0.2.9...main).
- **Breaking Changes / Migration Notes**: None explicitly published for this nightly.

## 3. Project Progress
Three PRs were merged or closed in the last 24 hours, advancing both platform stability and agent capabilities:

- **[Fix] Codex OAuth Response Handling (PR #2967 — Closed)**: This is the major win of the day. The provider now accumulates `response.output_text.delta` events instead of waiting for a nullable final `response.output` object. This resolves the persistent "empty response" issue for ChatGPT backend users.
- **[Feature] Rich Media Delivery (PR #2856 — Closed)**: The `message` tool has been extended to support media attachments and channel-aware rich delivery (starting with Telegram). This closes Issue #2855 and eliminates the need for agents to split text and file sends.
- **[Chore] Repository Hygiene (PR #2980 — Closed)**: Debug output files have been added to `.gitignore`.

New features submitted for review today include:
- **`cron` tool expansion** ([PR #2977](https://github.com/sipeed/picoclaw/pull/2977)): Adding `get` and `update` actions to prevent destructive rescheduling flows.
- **Telegram group reply detection** ([PR #2975](https://github.com/sipeed/picoclaw/pull/2975)): Replying to a bot message now counts as a mention in group chats.
- **Anthropic SDK v1.46.0 support** ([PR #2979](https://github.com/sipeed/picoclaw/pull/2979)): Fixing the deprecated `NewThinkingConfigAdaptiveParam` helper.

## 4. Community Hot Topics
- **Most Discussed — LM Studio Integration (Issue #28, 21 comments — Closed/Stale)**: Despite being closed months ago, this issue continues to draw traction from users wanting simpler local provider setup. The underlying need is a lower barrier to entry for connecting to local LLMs, an area the project may need to formally address soon.
- **Highest Impact — Codex OAuth Empty Response (Issue #2674, 4 👍 / 7 comments)**: This was the community’s primary pain point. A sophisticated analysis by contributors identified that streamed `output_text.delta` events were being ignored. The fix in PR #2967 was well-received and closes the loop started by reporter `@livinghorror` in Issue #2953.
- **New Thread — OmniRoute Provider Request (Issue #2978)**: A fresh, zero-comment feature request signaling the community’s desire for a third-party routing adapter. This aligns with the broader trend of provider extensibility.
- **Platform Expansion — Android Termux Guide (PR #2902)**: A stale PR that was updated today. The demand for mobile deployment is rising, and this PR would fill a significant documentation gap for ARM64 users.

## 5. Bugs & Stability
- **Critical (Fixed)**: The OpenAI Codex OAuth provider returning empty responses ([#2674](https://github.com/sipeed/picoclaw/issues/2674)). **Fix merged** in [#2967](https://github.com/sipeed/picoclaw/pull/2967). A targeted test for this streaming edge case would be recommended to prevent regression.
- **High (Open Fix)**: Anthropic provider broken by the SDK bump to v1.46.0 ([#2979](https://github.com/sipeed/picoclaw/pull/2979)). A one-line fix is awaiting maintainer merge.
- **Medium (Open)**: The `/context` command always showing a static "Compress at: 76800 tokens" value ([#2968](https://github.com/sipeed/picoclaw/issues/2968)). This is a display bug that may mislead users about actual token usage, specifically reported on FreeBSD with MiniMax.
- **Low (Closed)**: Debug output files polluting the repository ([#2980](https://github.com/sipeed/picoclaw/pull/2980)).

## 6. Feature Requests & Roadmap Signals
- **Next Release Candidates**:
  - The `cron` tool `get`/`update` actions ([PR #2977](https://github.com/sipeed/picoclaw/pull/2977)) are a strong candidate for the next stable release, as they directly improve agent operational autonomy.
  - Telegram reply-as-mention ([PR #2975](https://github.com/sipeed/picoclaw/pull/2975)) is low-risk, high-utility UX improvement that will likely land quickly.
- **Provider Layer Evolution**: The request for OmniRoute ([Issue #2978](https://github.com/sipeed/picoclaw/issues/2978)) and the lingering demand for LM Studio ([Issue #28](https://github.com/sipeed/picoclaw/issues/28)) indicate the user base expects a more formalized provider plugin system or "connectivity wizards" in the next roadmap cycle.
- **Core Architecture**: PRs [#2906](https://github.com/sipeed/picoclaw/pull/2906) (bus backpressure) and [#2904](https://github.com/sipeed/picoclaw/pull/2904) (agent loop stability) remain open. These are foundational changes that would significantly boost runtime reliability but require careful review before landing.

## 7. User Feedback Summary
- **Pain Points**: Provider connectivity remains the top source of user frustration. The Codex OAuth bug created a week-long window where a core backend silently failed, eroding trust. Users running on non-standard environments (FreeBSD, mobile) report display and compatibility edge cases.
- **Desired Use Cases**: The community wants PicoClaw to run everywhere — from high-end desktops connecting to ChatGPT backend to low-power ARM64 mobile devices via Termux. Agent operators are also demanding richer native tooling (media delivery, cron introspection).
- **Satisfaction**: The rapid triage and community-driven fix for Issue #2674 (from bug report to merged fix in ~6 days) demonstrates a responsive OSS culture. The quality of user-submitted bug reports (including detailed root cause analysis in #2953) shows a deeply engaged technical user base.

## 8. Backlog Watch
Several important items require maintainer attention to avoid stagnation:

- **Architectural PRs by SiYue-Zo** (PRs [#2906](https://github.com/sipeed/picoclaw/pull/2906) & [#2904](https://github.com/sipeed/picoclaw/pull/2904)): These address message bus backpressure and agent panic recovery. They have been open for 11+ days. Without explicit maintainer feedback, they risk becoming stale and requiring painful rebases.
- **Skill Reliability Check** ([PR #2936](https://github.com/sipeed/picoclaw/pull/2936)): This PR prevents agents from advertising skills whose required binaries are missing. It directly addresses a common runtime failure mode for cloud vs. edge deployments. Open for 7 days with no comment from maintainers.
- **LM Studio Expectations** ([Issue #28](https://github.com/sipeed/picoclaw/issues/28)): Although closed as stale, this is the most active issue in the project's history. The maintainers should consider publishing a formal stance or "good first issue" label for this feature to manage community expectations, rather than allowing it to remain a silent point of frustration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest | June 1, 2026

**Repository:** [github.com/nanocoai/nanoclaw](https://github.com/nanocoai/nanoclaw)

---

## 1. Today's Overview

NanoClaw showed high development velocity over the past 24 hours, with **8 pull requests** updated and **3 new issues** filed by 4 unique authors. The activity balance leans heavily toward operational hardening and developer experience, with critical reports surfacing around file-descriptor exhaustion, single-threaded host freezes, and silent container leaks. Community contributions are strong: `GiladShoham` contributed a coordinated batch of three PRs enhancing MCP transport and skill mounting, while `mshirel` opened three detailed stability reports. No official releases were cut in this window, but the volume of merged and active fix PRs suggests a stability-focused release is accumulating fast. Overall project health is active but mid-correction, as real-world scaling reveals architectural debt that the community is actively addressing.

---

## 2. Releases

No new releases published in the last 24 hours. The latest available versions remain unchanged.

---

## 3. Project Progress

### Merged / Closed

- **[#2648](https://github.com/nanocoai/nanoclaw/pull/2648) (CLOSED)** — `gavrielc`: Added a `/upload-trace` utility skill for uploading session traces to Hugging Face. A clean feature addition to the skills ecosystem.
- **[#2658](https://github.com/nanocoai/nanoclaw/pull/2658) (CLOSED)** — `cyber-chris`: Deployment configuration changes merged.

### Active Feature Development

- **[#2662](https://github.com/nanocoai/nanoclaw/pull/2662)** — `GiladShoham`: Extends `McpServerConfig` from a single stdio interface to a union type supporting **HTTP and SSE transports**, opening NanoClaw to hosted and remote MCP servers.
- **[#2661](https://github.com/nanocoai/nanoclaw/pull/2661)** — `GiladShoham`: Per-group skills placed in `groups/<folder>/skills/` are now wired into Claude Code's slash command discovery directory at spawn time.
- **[#2660](https://github.com/nanocoai/nanoclaw/pull/2660)** — `GiladShoham`: Mounts external symlink targets inside the container, resolving a failure mode where per-group skills pointing to shared host libraries failed silently.
- **[#2664](https://github.com/nanocoai/nanoclaw/pull/2664)** — `whahnize`: Runs the browser scraping sidecar inside the v2 container entrypoint. Bakes in web-fetch, NotebookLM, Mer audio, and Paris rental skills. Adds Discord v2 raw-text delivery.

### Stabilization Fixes (Active PRs)

- **[#2659](https://github.com/nanocoai/nanoclaw/pull/2659)** — `GiladShoham`: Reaps containers via host PID when `docker stop`/`kill` returns permission denied (common on unprivileged LXC/VMs).
- **[#2656](https://github.com/nanocoai/nanoclaw/pull/2656)** — `MoonCaves`: Moves `mnemon setup` from `entrypoint.sh` (which is overridden at spawn time) into the application `main()` to ensure hooks register correctly.

---

## 4. Community Hot Topics

No comments or reactions have been recorded yet on the items in this window (all are freshly submitted), but the *thematic weight* of contributions highlights community priorities:

- **MCP Protocol Expansion** — [#2662](https://github.com/nanocoai/nanoclaw/pull/2662) (HTTP/SSE support) is the single most architecturally significant PR of the day. Extending beyond stdio MCP is a consistent pain point for users aiming to connect managed or remote MCP servers.
- **Skill Usability** — [#2661](https://github.com/nanocoai/nanoclaw/pull/2661) and [#2660](https://github.com/nanocoai/nanoclaw/pull/2660) tackle a real workflow friction: skills were mountable but not discoverable or linkable. The three-PR cluster from `GiladShoham` represents a coordinated push that will noticeably improve the skill developer experience.

---

## 5. Bugs & Stability

**Ranked by severity:**

### Critical
- **[#2655](https://github.com/nanocoai/nanoclaw/issues/2655) — OneCLI Gateway FD Exhaustion:** The credential gateway runs with the default 1024 file-descriptor soft limit. Under burst load, it hard-exits with `os error 24 (No file descriptors available)`, causing a **silent total agent outage**. No fix PR exists yet. This is the highest-urgency item in the backlog.
- **[#2665](https://github.com/nanocoai/nanoclaw/issues/2665) — Host Freeze on Blocking Ops:** The single Node event loop driving the host can be frozen entirely by unbounded `await` (e.g., `channel.deliver()`, `execSync` image build). The `/health` endpoint cannot detect this condition, providing zero diagnostic signal during outages.

### High
- **[#2657](https://github.com/nanocoai/nanoclaw/issues/2657) — Self-Healing Gap:** Docker marks one-click gateway containers as `unhealthy` but fires no restart. Agent containers do not fail fast when the gateway connection drops. This creates persistent, silent failure states in production deployments.
- **[#2659](https://github.com/nanocoai/nanoclaw/pull/2659) — Container Leak (Fix PR exists):** On unprivileged hosts (LXC/VMs), `docker stop` returns permission denied. The in-memory `activeContainers` map is lost on host restart, causing orphans to leak and keep polling. **Fix PR open** by `GiladShoham`.

### Medium
- **[#2656](https://github.com/nanocoai/nanoclaw/pull/2656) — Mnemon Setup Silent Failure (Fix PR exists):** The `entrypoint.sh` override skips `mnemon setup` entirely, leaving hooks unregistered. **Fix PR open** by `MoonCaves`.

---

## 6. Feature Requests & Roadmap Signals

Several items point strongly to the direction of the next release:

- **MCP Multi-Transport (Imminent):** [#2662](https://github.com/nanocoai/nanoclaw/pull/2662) strongly signals that **HTTP and SSE MCP support** will land in the next version, making NanoClaw compatible with the rapidly expanding hosted-MCP ecosystem.
- **v2 Container Runtime (In Progress):** [#2664](https://github.com/nanocoai/nanoclaw/pull/2664) continues building out the "v2" container architecture with a browser scraping sidecar and new adapters. This indicates a significant container image overhaul in the pipeline.
- **Skill Ecosystem Maturation:** [#2660](https://github.com/nanocoai/nanoclaw/pull/2660) (external symlinks) and [#2661](https://github.com/nanocoai/nanoclaw/pull/2661) (slash commands) show the roadmap moving toward enterprise-grade skill management with shared libraries and instant discoverability.
- **Autonomous Operations:** [#2657](https://github.com/nanocoai/nanoclaw/issues/2657) (self-healing) and [#2655](https://github.com/nanocoai/nanoclaw/issues/2655) (fd exhaustion) are defensive signals. The community is demanding true "set and forget" production reliability, and the volume of fix PRs suggests the maintainers are listening closely.

---

## 7. User Feedback Summary

Direct upvotes or comments are absent from this snapshot (all items are too fresh), but the bug reports and PRs serve as explicit proxies for user experience:

- **Pain Point — Silent Outages Under Load:** Users are hitting hard resource limits (FD exhaustion, thread-blocking operations) with zero diagnostic pathway ([#2655](https://github.com/nanocoai/nanoclaw/issues/2655), [#2665](https://github.com/nanocoai/nanoclaw/issues/2665)).
- **Pain Point — Fragile Container Management:** Deployments on restrictive hosts (LXC/VMs) leak orphan containers ([#2659](https://github.com/nanocoai/nanoclaw/pull/2659)). Docker health checks are configured but not acted upon ([#2657](https://github.com/nanocoai/nanoclaw/issues/2657)).
- **Pain Point — Skill Development Friction:** Skills using symlinks break silently, and per-group skills are invisible as slash commands ([#2660](https://github.com/nanocoai/nanoclaw/pull/2660), [#2661](https://github.com/nanocoai/nanoclaw/pull/2661), [#2656](https://github.com/nanocoai/nanoclaw/pull/2656)).
- **Positive Signal — Responsive Contributor Base:** The rapid turnaround of fix PRs from community members (`GiladShoham`, `MoonCaves`) alongside these reports indicates a healthy, invested contributor base that ships solutions, not just complaints.

---

## 8. Backlog Watch

All three new issues ([#2665](https://github.com/nanocoai/nanoclaw/issues/2665), [#2657](https://github.com/nanocoai/nanoclaw/issues/2657), [#2655](https://github.com/nanocoai/nanoclaw/issues/2655)) were created on **May 31, 2026** and carry **zero comments, zero reactions, and no assignees**. While there are no "long-standing" unanswered items visible in this 24-hour window, the silence on these critical stability reports is notable.

**Recommendation:** These three issues require immediate triage and assignment. The lack of community discussion may indicate that the problems are self-evident to the core team, but from a project-health perspective, labeling and acknowledging them publicly would set a strong ownership precedent for the upcoming stabilization release.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-01

**Data Snapshot:** Last 24 hours (May 31–Jun 1, 2026)
- Issues Updated: 2 (both open)
- PRs Updated: 0
- New Releases: 0
- Active Commenters: 1 (`weissfl`)

**Project Health Assessment:** Quiet development cycle with zero code merges or releases, but active user engagement through two newly filed, well-defined bug reports. The reports uncover regressions and gaps in the Telegram integration and the agent scheduler—core components that demand urgent maintainer attention.

---

## 1. Today's Overview

NullClaw enters June with a quiet development cadence; no pull requests were updated and no releases were cut in the last 24 hours. At the same time, power user `weissfl` filed two substantive bug reports targeting the Telegram interface and the scheduled agent execution pipeline. The most critical issue (#941) reveals that agent-type cron jobs silently fail to spawn a subprocess, breaking automated delivery entirely. While code churn is low, the specificity and severity of these reports signal an engaged user base encountering real pain points in production use cases. The project would benefit strongly from a targeted bugfix sprint focusing on the scheduler backend and Telegram callback UX.

---

## 2. Releases

No new releases were published in the monitored period.

---

## 3. Project Progress

**No pull requests were merged or closed in the last 24 hours.**

---

## 4. Community Hot Topics

Two new issues constitute the entirety of community activity. Although they have no comments or reactions yet, their content drives the current conversation forward.

**Issue #941: Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens**
- Author: `weissfl`
- [View Issue #941](https://github.com/nullclaw/nullclaw/issues/941)
- *Underlying Need:* Users depend on scheduled autonomous agents for offline/unattended workflows. This bug violates the core promise of a "set-and-forget" agent system. The underlying demand is for **reliable, auditable autonomous execution** with clear success/failure signals.

**Issue #942: Telegram — missing typing indicator when pressing inline buttons (callback_query)**
- Author: `weissfl`
- [View Issue #942](https://github.com/nullclaw/nullclaw/issues/942)
- *Underlying Need:* Users expect **consistent, pro-grade UX** across all interaction modalities. The typing indicator provides crucial real-time feedback that processing has begun. The gap between text-based and callback-based interactions reveals a need for unified event lifecycle handling in the Telegram driver.

---

## 5. Bugs & Stability

Two bugs were reported, distinct in severity and component.

| Severity | Issue | Component | Description | Fix PR Exists? |
|-----------|-------|-----------|-------------|----------------|
| **High** | [#941](https://github.com/nullclaw/nullclaw/issues/941) | Scheduler / Agent Runner | `agent`-type cron jobs marked as complete without spawning the subprocess; no Telegram message delivered despite correct `delivery_mode` and `delivery_channel` config. | No |
| **Low-Medium** | [#942](https://github.com/nullclaw/nullclaw/issues/942) | Telegram Integration (UI/UX) | `callback_query` presses (e.g., `nc_choices`) do not trigger the "typing…" indicator that text messages reliably show. | No |

**Analysis:** Issue #941 is a critical functional regression. If this is not an isolated environment issue, it breaks scheduled agent workflows entirely. #942 is a UX degradation that lowers perceived responsiveness during interactive sessions.

---

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. However, the bug reports provide strong roadmap signals:

- **Scheduling Reliability Overhaul:** Issue #941 suggests the subprocess spawning logic in the cron/agent dispatch loop has a structural flaw. A future release (likely a patch or minor version) should prioritize a deeper refactor of the job runner's subprocess lifecycle and delivery confirmation chain.
- **Telegram Interaction Parity:** Issue #942 signals that inline button interactions lack the same event-handling pipeline as text messages. A maintenance release unifying the input processing flow—ensuring `send_chat_action("typing")` fires consistently—is a natural next step.

**Next-Release Prediction:** A hotfix (v0.x.1+) targeting #941 is the most probable immediate release, given the high severity of the cron execution bug. A UX patch for #942 may follow closely behind.

---

## 7. User Feedback Summary

- **Identified Pain Points:**
  1. **Silent Scheduled Failures:** Agent tasks configured with `job_type: "agent"`, `delivery_mode: "always"`, and `delivery_channel: "telegram"` fail silently—no message sent, no subprocess spawned, job marked complete. This erodes trust in autonomous functionality.
  2. **Inconsistent Telegram UX:** The absence of the typing indicator on callback queries versus text messages creates a jarring user experience where interactive button presses feel unresponsive or broken.

- **Use Cases Evidenced:**
  - Scheduled Telegram-based agent tasks (report generation, daily digests)
  - Interactive inline button workflows (choice selection via `nc_choices`)

- **Satisfaction Signals:**
  - The author `weissfl` is filing specific, well-structured bug reports with expected vs. actual behavior clearly documented—indicating a technically sophisticated user deeply invested in making the tool work correctly, rather than a casual user abandoning it.

---

## 8. Backlog Watch

**Status:** No long-unanswered issues or PRs are present in the current 24-hour snapshot.

The two reported items (## 941, 942) were opened less than 24 hours ago and remain uncommented by maintainers. While they do not yet qualify as "backlog," they represent the most pressing items on the project's active radar and require a prompt maintainer response, especially the critical #941 scheduler issue. A broader audit of issues outside this 24-hour window is recommended to identify any deeper backlog items needing attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest based on the provided GitHub data for June 1, 2026.

---

## 1. Today's Overview
IronClaw development remains extremely active, with 26 PRs updated in the past 24 hours and a strong focus on the foundational "Reborn" architecture. Core contributors drove the majority of the change, merging three large feature PRs covering triggers, outbound communications, and product auth. Issue activity was quiet overall (only three issues updated), but a long-running MCP transport bug and a nightly E2E failure represent significant stability risks. No new releases were cut today.

## 2. Releases
**None.** No new versions of IronClaw were published in this period.

## 3. Project Progress
Seven pull requests were merged or closed today, advancing several key architectural pillars:

- **[Triggers] libSQL Repository ([PR #4263](https://github.com/nearai/ironclaw/pull/4263)):** henrypark133 landed the first durable backend for the Reborn trigger system using libSQL. This backend is scoped intentionally to a single repository, with a Postgres counterpart waiting in the stack.
- **[Outbound] Resolution Engine ([PR #4262](https://github.com/nearai/ironclaw/pull/4262)):** The P0 outbound communication resolution engine was merged by henrypark133, providing candidate selection logic for delivery without yet integrating validation or transport.
- **[Auth] AuthPromptView & WebUI OAuth Wiring ([PR #4257](https://github.com/nearai/ironclaw/pull/4257)):** A significant feature by serrrfirat that wires the Rust-side challenge enrichment into the WebUI v2 for GSuite OAuth, Notion MCP OAuth, and GitHub PAT flows.
- **[Dependencies] Bulk Updates:** Dependabot closures brought in multiple ecosystem updates, including the Tokio stack (1.50.0 → 1.52.3, [PR #4001](https://github.com/nearai/ironclaw/pull/4001)) and Serde JSON ([PR #4000](https://github.com/nearai/ironclaw/pull/4000)).

## 4. Community Hot Topics
The most active discussions continue to revolve around core stability and large new integrations:

- **[Issue #2923: stdio MCP Activation Bug](https://github.com/nearai/ironclaw/issues/2923) (4 comments, 1 👍):** The hottest community topic. A user re-filed this after it was closed in error by a non-maintainer, insisting the stdio transport *is* wired end-to-end but the activation pre-flight is broken. This signals a strong desire for MCP tool support and frustration with the process around the issue.
- **[PR #4178: Feishu WebSocket Event Intake](https://github.com/nearai/ironclaw/pull/4178) (XL, core contributor):** A complex new channel integration adding full Feishu/Lark support via binary protobuf websockets and webhook fallback. This large PR is under heavy review.
- **[PR #4035 / #4272: Slack Reborn Adapter](https://github.com/nearai/ironclaw/pull/4035) (Stacked PRs, regular contributor):** The first reviewable slices of Slack moving into the Reborn architecture. These are foundational for better Slack stability and features.
- **[PR #4229: Native GitHub SSO Surface](https://github.com/nearai/ironclaw/pull/4229) (XL, experienced contributor):** Implements GitHub OAuth for WebChat v2, a high-value feature for community deployments.

## 5. Bugs & Stability
- **🔴 CRITICAL — CI Failure ([Issue #4108](https://github.com/nearai/ironclaw/issues/4108)):** The Nightly E2E suite is failing. This is an unattended automated report (updated 2026-05-31, zero comments) that requires immediate triage to unblock integration testing.
- **🟠 HIGH — MCP Transport Activation ([Issue #2923](https://github.com/nearai/ironclaw/issues/2923)):** Users cannot activate stdio-based MCP servers due to a "Failed to discover authorization endpoints" error. The user claims this is a regression in v0.25.0 and was mishandled by community moderation. No linked fix PR is currently visible in the activity.
- **🟡 MEDIUM — `capability_info` Error Handling ([PR #4266](https://github.com/nearai/ironclaw/pull/4266)):** A fix in progress by serrrfirat addresses a stability issue where unknown `capability_info` targets cause terminal driver errors instead of graceful model-facing `InvalidInput` failures. This is under active review.

## 6. Feature Requests & Roadmap Signals
The data strongly signals that the next major version will be the **Reborn architectural release**. Several large features are being built simultaneously:

- **Reborn Triggers:** Merged libSQL backend ([#4263](https://github.com/nearai/ironclaw/pull/4263)) with Postgres parity in the stack ([#4270](https://github.com/nearai/ironclaw/pull/4270)).
- **Reborn Outbound:** The resolution engine is merged ([#4262](https://github.com/nearai/ironclaw/pull/4262)); an outbound validation bridge is now open for review ([#4271](https://github.com/nearai/ironclaw/pull/4271)).
- **New Platform Integrations:** Live PRs for **Slack** ([#4035](https://github.com/nearai/ironclaw/pull/4035), [#4272](https://github.com/nearai/ironclaw/pull/4272)), **Feishu/Lark** ([#4178](https://github.com/nearai/ironclaw/pull/4178)), and **GitHub SSO** ([#4229](https://github.com/nearai/ironclaw/pull/4229)) suggest an aggressive channel and auth expansion strategy.
- **Product Auth UX:** A multi-PR effort ([#4239](https://github.com/nearai/ironclaw/pull/4239), [#4269](https://github.com/nearai/ironclaw/pull/4269), [#4257](https://github.com/nearai/ironclaw/pull/4257)) is modernizing credential management, OAuth, and auth-prompt logic for the Reborn web UI.

*Prediction:* The next release will focus heavily on Reborn stability for core integrations (Triggers, Outbound, Auth) and debut the new Slack/Feishu channel adapters.

## 7. User Feedback Summary
Direct user feedback is limited but pointed.

- **Pain Points:** The stdio MCP bug ([#2923](https://github.com/nearai/ironclaw/issues/2923)) is the clearest source of user dissatisfaction. The author explicitly stated the issue was "closed in error," implying a process gap where non-maintainers can close legitimate bugs. This needs direct maintainer attention to restore trust.
- **Satisfaction:** The sheer velocity (26 PRs updated) suggests a healthy, fast-moving project. Users looking for Slack and Feishu integration, as well as better GitHub SSO, have concrete reason for optimism given the active PRs.
- **Use Cases:** The current work is heavily oriented toward enterprise and developer-platform use cases requiring complex authentication chains (OAuth, SSO, MCP) and multi-channel delivery (Slack, Feishu, WebUI).

## 8. Backlog Watch
- **[Issue #2923: stdio MCP Activation Bug](https://github.com/nearai/ironclaw/issues/2923) (Open since April 24):** This is the single highest-priority item in the backlog. It has been open for over a month, was mishandled by process, and directly impacts tool usage. A maintainer should explicitly label and prioritize this.
- **[PR #4002: Dependabot Actions Update (16 updates)](https://github.com/nearai/ironclaw/pull/4002) (Open since May 24):** Stale dependency update for GitHub Actions. With the nightly E2E currently failing, unmerged CI dependency updates are a risk. This should be triaged promptly.
- **[PR #4001: Tokio Ecosystem Update](https://github.com/nearai/ironclaw/pull/4001) (Open since May 24):** Unmerged update for the Tokio stack, which powers the entire async runtime. Staleness here increases the risk of drift from upstream fixes.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI Project Digest – 2026-06-01

---

### 1. Today's Overview
LobsterAI registered low activity on June 1st, with only one new issue and two updated pull requests, and no new release. The single new issue reveals a severe user complaint about the subscription credit rollover policy, posing a direct retention risk. On the development side, a UI optimization PR was merged, signaling ongoing frontend polish. However, a critical two-month-old fix for ghost scheduled tasks remains stale in the backlog.

---

### 2. Releases
No new releases were published on this date or in the immediate period leading up to the digest cut-off.

---

### 3. Project Progress
One pull request was merged today:

- **PR #2080 (Merged)** – [area: renderer, area: docs, area: main, area: cowork] chore: optimize kits and upload file ui  
  Submitted by **fisherdaddy**, this PR delivers a UI/UX polish pass across multiple modules, optimizing the kits panel and file upload interface.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/2080)

---

### 4. Community Hot Topics
Community engagement today is concentrated on a single high-stakes billing issue:

- **Issue #2081 (Open)** – **Subscription Credit Expiry Complaint**  
  Filed by **zjk648491625**, this issue expresses strong anger (“来搞笑的吧???”) over 5,500 unused subscription credits being reset at month-end. The underlying need is for a fair rollover policy or explicit expiry warnings. This represents a direct threat to paid-tier trust and retention.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/2081)

No other issue or PR generated discussion today.

---

### 5. Bugs & Stability
- **No new bugs were reported today.**

- **Recurring Bug (Medium Severity)** – **Ghost Scheduled Tasks**  
  PR #1465 provides a root-cause fix for Issue #1359: deleting a scheduled task fails to clean up its associated local SQLite session, causing the deleted task to reappear as an empty ghost session on restart. The fix has been sitting stale since May 31 and awaits maintainer review.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1465)

---

### 6. Feature Requests & Roadmap Signals
- **Subscription Policy Change (Implicit from Issue #2081)**  
  The community is clearly requesting fairer quota management — either a monthly rollover of unused credits or proactive expiry notifications. This may become a high-priority roadmap item to stem user dissatisfaction.

- **UI Polish Direction (Evidenced by PR #2080)**  
  The merged optimization of the kits and file upload UI suggests the team is refining core user workflows, possibly preparing these surfaces for more stable feature expansion.

---

### 7. User Feedback Summary
- **Satisfaction**: The primary sentiment captured today is severe dissatisfaction tied directly to the monetization model.
- **Pain Points**: Users feel their purchase was devalued when bulk credits were silently cleared.
- **Use Cases**: The feedback highlights a critical gap in the subscriber lifecycle — the system failed to help the user track or use their allocated paid quota effectively.
- **Risk Assessment**: The tone of Issue #2081 represents a clear escalation risk. An official response and/or policy adjustment is strongly recommended.

---

### 8. Backlog Watch
- **[PRIORITY: HIGH] Issue #2081** – Subscription credit rollover complaint. At least one paying user is actively waiting for a response. Any delay may amplify churn risk.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/2081)

- **[PRIORITY: MEDIUM] PR #1465** – Fix for ghost scheduled tasks. Labeled as stale for ~2 months despite having a clear root cause and proposed fix. Requires code review and merge to resolve a persistent data-consistency bug.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1465)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest: 2026-06-01**

**1. Today's Overview**
The Moltis repository saw minimal activity on June 1st, 2026, with no new issues filed and no new releases published. Project activity was limited to the opening of a single pull request targeting session history management. The absence of user-reported bugs or feature requests combined with the quiet PR queue suggests a stable period focused on internal reliability improvements. Overall project health appears sound, with maintainers proactively addressing infrastructure concerns rather than reacting to community disruption.

**2. Releases**
No new releases were published on this date.

**3. Project Progress**
No pull requests were merged or closed today. The single active work item is:
- **[PR #1089 [OPEN] Cap persisted tool results before rehydration](https://github.com/moltis-org/moltis/pull/1089)** (Author: [s-salamatov](https://github.com/s-salamatov))
  - Limits the size of `tool` and `tool_result` content when session history is restored into provider-bound `ChatMessage`s.
  - Applies this capping across all execution paths: normal chat, streaming, retry-after-compaction, prompt inspection, silent memory turns, and LLM-backed compaction prompts.
  - Still open and pending review.

**4. Community Hot Topics**
Engagement metrics were flat today—zero comments across all issues and PRs. The sole open discussion center is **[PR #1089](https://github.com/moltis-org/moltis/pull/1089)**, which attracted no reactions or discussion yet. The underlying need is clear: large tool call outputs can easily bloat a session's rehydrated context, risking token overruns and increased costs in long-running agent loops. This PR is a proactive safeguard for heavy tool users, even if the community has not yet voiced concern.

**5. Bugs & Stability**
No explicit bugs or regressions were reported today. However, **[PR #1089](https://github.com/moltis-org/moltis/pull/1089)** strongly implies an internal recognition of a stability vulnerability: unconstrained tool-result bloat during rehydration. While not a user-filed crash, this fix preemptively addresses a latent class of context overflow issues that could silently degrade session reliability. No new fixes for user-reported crashes exist.

**6. Feature Requests & Roadmap Signals**
No user-facing feature requests were filed today. The only roadmap signal is the reliability-focused nature of **[PR #1089](https://github.com/moltis-org/moltis/pull/1089)**. This points toward the next version leaning into hardening session and memory management rather than adding flashy new features. It is reasonable to predict that the upcoming release will include session size throttling and more robust compaction logic.

**7. User Feedback Summary**
There is no direct user feedback to report for this date. The combination of zero new issues and zero comments on the day's only PR suggests a lull in community activity rather than rapid satisfaction or dissatisfaction.

**8. Backlog Watch**
The project backlog is exceptionally clean. There are no unresolved older issues, no stalled PRs from prior dates, and no long-dormant discussions awaiting maintainer input. The only open item ([PR #1089](https://github.com/moltis-org/moltis/pull/1089)) was submitted today and is actively progressing through review. No items currently demand maintainer triage attention.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw / QwenPaw Project Digest | June 1, 2026

## 1. Today's Overview

June 1st reveals a project under heavy strain from rapid adoption, with **27 issues** and **11 pull requests** updated in the last 24 hours. Community engagement is at a fever pitch, driven largely by MCP resource exhaustion at scale, Windows-specific regressions, and a notable v1.1.9 reliability regression where agents default to a system-level fallback message. While no formal release was cut today, the development team is actively responding with targeted PRs, including a critical `SharedMCPPool` for multi-agent deployments and a significant WIP to migrate the underlying `agentscope` dependency to version 2.0. The overall tone is constructive but urgent—users are pushing the platform hard and discovering its current scaling limits.

---

## 2. Releases

No releases today.

---

## 3. Project Progress

**Merged / Closed PRs:**
- **[[CLOSED] feat(console): improve chat slash skill suggestions**](https://github.com/agentscope-ai/QwenPaw/pull/4810) (#4810) — The only closed PR today, improving slash-command skill discovery in the chat UI with better filtering and pagination.

**Key Active PRs under Review / Development:**

| PR | Status | Description |
|---|---|---|
| [#4849 perf(mcp): add SharedMCPPool](https://github.com/agentscope-ai/QwenPaw/pull/4849) | **Open** | Direct fix for the MCP process explosion bug (#4842), pooling server connections across agents. **Top priority.** |
| [#4846 refactor: migrate agentscope 1.x to 2.0](https://github.com/agentscope-ai/QwenPaw/pull/4846) | **WIP Open** | Major architecture upgrade to agentscope 2.0. Signals long-term structural investment. |
| [#4847 fix(skill): preserve user config during update](https://github.com/agentscope-ai/QwenPaw/pull/4847) | **Open** | Stops workspace skill downloads from overwriting user tags and channel settings. |
| [#4820 fix(context): normalize inline source URLs during compaction](https://github.com/agentscope-ai/QwenPaw/pull/4820) | **Open** | Fixes memory compaction crash (#4811) when media blocks contain raw URL strings. |
| [#4822 fix(crons): fix share_session cron tasks producing empty traces](https://github.com/agentscope-ai/QwenPaw/pull/4822) | **Open** | Resolves cron agents reporting success but executing no actions (#4818). |
| [#4821 feat(feishu): add group session sharing mode](https://github.com/agentscope-ai/QwenPaw/pull/4821) | **Open** | Adds group session isolation control to the Feishu channel. |
| [#4848 feat(channels): add QR code authorization for QQ](https://github.com/agentscope-ai/QwenPaw/pull/4848) | **Open** | QR-based credential retrieval matching the DingTalk pattern. |
| [#4737 feat(telegram): add tool_guard interactive approval](https://github.com/agentscope-ai/QwenPaw/pull/4737) | **Open (Under Review)** | Inline keyboard approval for tool execution in Telegram. |

---

## 4. Community Hot Topics

The most active discussions reveal deep power-user engagement and escalating demands.

**[#4845 — WeWork channel lacks memory isolation (Security)](https://github.com/agentscope-ai/QwenPaw/issues/4845)**
A user reports that prompt injection on the WeWork channel can leak other users' chat histories. This is the most sensitive active issue—there is currently no fix PR linked.

**[#4837 — v1.1.9 system-level fallback flooding](https://github.com/agentscope-ai/QwenPaw/issues/4837)**
Multiple users are hitting a regression where agents return a canned "cannot process your request" message instead of their real response. This is undermining trust in the latest stable version.

**[#4842 / #4834 — MCP server process explosions](https://github.com/agentscope-ai/QwenPaw/issues/4842)**
A user running 300+ agents describes how each agent spawns its own MCP server process, creating hundreds of concurrent processes that persist across restarts. PR #4849 is the direct response and is the community's most-watched fix.

**[#4789 — Conversation rollback and deletion (Closed)](https://github.com/agentscope-ai/QwenPaw/issues/4789)**
A heavily upvoted feature request asking for Trae-like per-conversation rollback with file history management. Although closed, the 8 comments and reaction signal strong latent demand for workspace versioning.

**[#4808 — Agent "person_stat_skill" not exists](https://github.com/agentscope-ai/QwenPaw/issues/4808)**
A user struggles with SKILL.md configuration, hitting a cryptic error. With 7 comments, this highlights the community's need for better skill onboarding tooling.

---

## 5. Bugs & Stability

The project is actively managing a bug surge, with Windows and MCP reliability dominating the severity landscape.

### Critical

| Issue | Impact | Status |
|---|---|---|
| [#4845 WeWork memory isolation leak](https://github.com/agentscope-ai/QwenPaw/issues/4845) | Security — prompt injection leaks cross-user chat history | Open, no fix PR |
| [#4842 MCP process explosion (300+ agents)](https://github.com/agentscope-ai/QwenPaw/issues/4842) | Resource exhaustion, system crashes | Fix inbound (#4849) |
| [#4834 MCP processes persist across restarts](https://github.com/agentscope-ai/QwenPaw/issues/4834) | Process accumulation, slow console loading | Open |
| [#4837 v1.1.9 system fallback flooding](https://github.com/agentscope-ai/QwenPaw/issues/4837) | Agent returns "cannot process" instead of reasoning | Open |
| [#4844 Browser process/temp dir locks on Windows](https://github.com/agentscope-ai/QwenPaw/issues/4844) | Locks prevent backups, cascade to other failures | Open |

### High

| Issue | Impact | Status |
|---|---|---|
| [#4835 Single invalid job fails entire workspace](https://github.com/agentscope-ai/QwenPaw/issues/4835) | Total workspace crash on `jobs.json` validation error | Open |
| [#4818 Cron share_session tasks empty traces](https://github.com/agentscope-ai/QwenPaw/issues/4818) | Cron reports success but executes no actions | Fix inbound (#4822) |
| [#4649 / #4653 Orphaned / interrupted cron jobs](https://github.com/agentscope-ai/QwenPaw/issues/4649) | Ghost tasks from stale configs, user messages interrupt cron | Closed, deeper fix needed? |
| [#4829 / #4832 CMD window flash on tool execution (Windows)](https://github.com/agentscope-ai/QwenPaw/issues/4829) | Annoying UX — cmd.exe window appears on every shell tool call | Closed (#4829), New (#4832) |
| [#4839 Windows pip upgrade ghost skill dirs](https://github.com/agentscope-ai/QwenPaw/issues/4839) | `~`-prefixed stale skill directories pollute pool | Open |

### Medium

| Issue | Impact | Status |
|---|---|---|
| [#4811 Compaction crash on inline source URL](https://github.com/agentscope-ai/QwenPaw/issues/4811) | `AttributeError` crash during context compaction | Fix inbound (#4820) |
| [#4666 Model config lost on new session](https://github.com/agentscope-ai/QwenPaw/issues/4666) | "Load failed" on Models page, requires restart | Open since May 25 |
| [#4824 ACP protocol mismatch with Claude Code](https://github.com/agentscope-ai/QwenPaw/issues/4824) | Version format mismatch, internal errors | Open |
| [#4819 Coding mode conversation switching breaks](https://github.com/agentscope-ai/QwenPaw/issues/4819) | Global refresh + jump back on chat switch | Open |

---

## 6. Feature Requests & Roadmap Signals

### Near-Term (Likely v1.2.0)

- **MCP Process Pooling** ([PR #4849](https://github.com/agentscope-ai/QwenPaw/pull/4849)) — The leading candidate for the next patch release; solves the critical scaling bottleneck.
- **Tool Definition Lazy Loading** ([#4836](https://github.com/agentscope-ai/QwenPaw/issues/4836)) — Proposes reducing initial context token overhead by **55–65%** for tools-rich environments (45+ tools). Extremely practical for heavy deployments.
- **Configurable Chat Modes** ([#4843](https://github.com/agentscope-ai/QwenPaw/issues/4843)) — Interrupt, Queue, and Insert modes for concurrent message handling. Addresses the cron-interruption complaints and power-user concurrency needs.

### Medium-Term

- **Thinking Effort UI Selector** ([#4840](https://github.com/agentscope-ai/QwenPaw/issues/4840)) — Moving reasoning configuration out of config files into the chat window UI.
- **Multi-Turn Tool Output Suppression** ([#4838](https://github.com/agentscope-ai/QwenPaw/issues/4838)) — Channel-level option to suppress agent text after tool calls for "silent" tool execution.
- **Conversation Workspace Versioning** ([#4789](https://github.com/agentscope-ai/QwenPaw/issues/4789)) — Per-conversation file and state rollback. High community demand.
- **Desktop UX: Clickable File Paths** ([#4830](https://github.com/agentscope-ai/QwenPaw/issues/4830)) — Auto-detect and render local paths as clickable links in chat output.
- **Docker Dependency Pre-Install** ([#4831](https://github.com/agentscope-ai/QwenPaw/issues/4831)) — Pre-install `psycopg2-binary`, `pytz`, `mootdx` to avoid container rebuild failures.

### Long-Term / Architecture

- **Agentscope 2.0 Migration** ([PR #4846](https://github.com/agentscope-ai/QwenPaw/pull/4846)) — A foundational refactor that will unlock significant downstream improvements but carries integration risk.
- **GPT-5.5 `reasoning_effort: xhigh` Support** ([#4814](https://github.com/agentscope-ai/QwenPaw/issues/4814)) — User requesting clear documentation and `extra_body` passthrough for advanced reasoning tiers.

---

## 7. User Feedback Summary

### Primary Pain Points

- **Windows as a Second-Class Platform:**
  The CMD window flash (#4829, #4832), pip upgrade ghost files (#4839), and browser temp locks (#4844) consistently make the Windows experience feel incomplete. For a desktop Tauri app, these are high-friction issues.

- **v1.1.9 Regressions Erode Trust:**
  The system-level fallback flooding (#4837) is the most alarming current issue. Users trusted an upgrade and got silent failures.

- **Enterprise Scaling Walls:**
  Users deploying 100–300+ agents hit hard resource limits. MCP process explosion is the headline issue, but the broader pattern (cron ghosting, config brittleness, session isolation gaps) suggests the architecture wasn't stress-tested at this scale.

- **Config and State Fragility:**
  A single malformed `jobs.json` entry kills the entire workspace (#4835). Model configs vanish on new session (#4666). Small state management errors have outsized consequences.

### Positive Signals

- **Highly Technical Community:** The level of detail in bug reports (logs, reproduction steps, root cause analysis) reflects a sophisticated user base willing to invest in the project's success.
- **Channel Diversity is Valued:** The rapid expansion across WeWork, QQ, Feishu, DingTalk, and Telegram is clearly meeting a real multi-platform need.
- **Responsive Maintainers:** The community sees developers opening targeted fix PRs within hours or days of critical reports (MCP pooling, cron traces, compaction crash).

---

## 8. Backlog Watch

Several important items risk stalling without maintainer attention.

| Item | Days Waiting | Risk |
|---|---|---|
| [PR #4433 — Token usage badge / per-turn UI](https://github.com/agentscope-ai/QwenPaw/pull/4433) | **17 days** (Under Review) | High-community-value feature languishing despite being "Under Review" since May 15. Decision or revision request overdue. |
| [PR #4737 — Telegram tool_guard inline keyboard](https://github.com/agentscope-ai/QwenPaw/pull/4737) | **4 days** (Under Review) | Well-structured PR adding critical safety UX to Telegram. Needs final approval. |
| [Issue #4666 — Models config lost on new session](https://github.com/agentscope-ai/QwenPaw/issues/4666) | **7 days** (Open) | Data loss bug with no linked fix PR, no maintainer comment. Affects core usability. |
| [Issue #4808 — SKILL.md "not exists" error](https://github.com/agentscope-ai/QwenPaw/issues/4808) | **3 days** (Open) | Recurring configuration friction suggests a need for better error messages, a diagnostic CLI command, or manifest validation. |
| [Issue #4653 / #4649 — Cron reliability](https://github.com/agentscope-ai/QwenPaw/issues/4653) | **8 days** (Closed) | Closed, but the new crop of cron bugs (#4818, #4835) suggests the underlying root cause may not be fully resolved. |

---

*End of digest. Data reflects the project state as of June 1, 2026.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

Here is the structured ZeptoClaw project digest based on the provided GitHub data for 2026-06-01.

---

### ZeptoClaw Project Digest — 2026-06-01

**1. Today's Overview**
Project activity over the last 24 hours was minimal in terms of raw volume but carried significant weight in terms of security posture. The sole development action was the closure of a repository-wide Codex Security scan specifically targeting the webhook identity routing flow. No pull requests were merged and no new releases were published. While public contribution velocity was low, the completion of this audit chore signals a strong internal focus on infrastructure security and access control hardening. The overall project health appears stable, with a proactive stance on vulnerability prevention.

**2. Releases**
No new releases were published in the reporting window.

**3. Project Progress**
The only completed work item was a closed maintenance issue:
- **Security Hardening:** The project successfully closed a security chore focused on webhook identity routing. This work implies the completion of a deep code analysis pass on the authentication and admission pipeline, reducing potential attack surface in a critical path.
  - *Details:* [qhkm/zeptoclaw Issue #609 – chore(security): repository-wide Codex Security scan for webhook identity routing](https://github.com/qhkm/zeptoclaw/issues/609)

**4. Community Hot Topics**
Community discussion was limited to the single active issue. While it generated only one comment and zero reactions, its content is notable for the broader project ecosystem.
- **Issue #609 (Closed):** The chore specifically requested a "repository-wide Codex Security scan" with an emphasis on webhook request identity flow.
  - *Link:* [qhkm/zeptoclaw Issue #609](https://github.com/qhkm/zeptoclaw/issues/609)
  - *Analysis:* The author is associated with the `oai` GitHub organization, suggesting an ongoing security vetting process tied directly to OpenAI infrastructure. The underlying need driving this activity is the hardening of identity-based admission and routing, likely a prerequisite for broader production deployment or integration with enterprise identity providers. The lack of public discussion does not signal a lack of interest; it suggests the work is primarily driven by institutional security requirements rather than community feature requests at this time.

**5. Bugs & Stability**
No new bugs, crashes, or regressions were reported in the last 24 hours. The security scan conducted in Issue #609 is inherently a proactive bug-prevention activity, targeting logical flaws in the identity routing layer. The absence of open stability issues in the window suggests a healthy baseline, though analysts should watch for any follow-up patches generated by this scan.

**6. Feature Requests & Roadmap Signals**
No explicit user feature requests were logged today. However, the roadmap signal is clearly visible through the lens of the security chore:
- **Identity & Routing Focus:** The deep prioritization of webhook identity routing suggests that ZeptoClaw is preparing for multi-tenant enterprise hosting, federated authentication, or complex agent chaining where identity integrity across hops is critical.
- **Predictions:** Future releases will likely see improvements to authentication middleware, webhook validation libraries, or configuration schemas for identity mapping based on findings from this scan.

**7. User Feedback Summary**
No explicit user feedback (pain points or praise) was captured in the issue tracker within the reporting period. The quietness of the tracker could imply stability and satisfaction among active users, or it could reflect a currently low volume of public user engagement. The data sample is insufficient to draw strong conclusions on sentiment.

**8. Backlog Watch**
- **No Long-Standing Neglected Items:** No outdated issues or idle pull requests were touched in the last 24 hours. The dataset does not reveal any items demanding immediate maintainer attention.
- **Watch Item:** While not strictly backlogged, the *results* of the Codex Security scan in Issue #609 should be tracked. If the scan uncovered architectural debt or specific vulnerabilities, corresponding issues will likely be filed in the coming days. Maintaining velocity on these follow-ups will be critical to preserving the security gains made today.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-01

## 1. Today's Overview

ZeroClaw is experiencing a sustained high-velocity development period. Over the last 24 hours, the project saw updates on **30 issues** and **50 pull requests**, indicating a heavy push toward upcoming milestones tracked in the `v0.7.6` (skills UX) and `v0.8.1` (integration/channel/provider/tool) release cycles. While no formal releases were cut today, the team successfully closed **12 issues** and integrated **10 PRs**, striking a balance between landing new feature work (email OAuth2, hardware simulator, TTS transcoding, multi-tenant channels) and closing critical bug reports from the community. Activity is broad, spanning core architecture, provider unification, new TUI client stability, and physical computing use cases. The project's overall health is strong, though several S1 (workflow-blocked) bugs remain open, warranting continued focus on runtime reliability.

---

## 2. Releases

No new releases were published in the last 24 hours. The active trackers **#6253 (v0.7.6 — skills)** and **#6970 (v0.8.1 — integration queue)** suggest pre-release candidates are likely to materialize soon.

---

## 3. Project Progress

The last 24 hours saw **10 PRs merged or closed** and **12 issues closed**, with notable developments across infrastructure, bug fixes, and channel improvements:

- **Infrastructure & CI:**
  - **PR #7023** introduces a versioned documentation deployment system with a version selector, allowing users to browse docs specific to their release.
  - **PR #7044** refactored Cargo dependency management by extracting a `channels-all` aggregate feature, reducing complexity in the dependency graph.

- **Core & Configuration:**
  - **PR #7028** fixed `zeroclaw config set` to properly materialize typed provider aliases from the config set, resolving a configuration integrity bug.
  - **Issue #5843** (Model-wise reasoning configuration) was closed, indicating per-provider reasoning settings are now supported.

- **Channel & Platform Fixes:**
  - **Issue #7033** (Media pipeline omitting inline image data for vision providers) — closed.
  - **Issue #7032** (WhatsApp Web `mention_only` missing LID JID mentions) — closed.
  - **Issue #6999** (Telegram voice transcription always failing) — closed, resolving a major Telegram workflow block.
  - **Issue #6965** (Canvas page never receiving frames from web-UI chat) — closed.
  - **Issue #6647** (Cron job output not routed to configured channels) — closed.

- **Long-Standing Fixes Landed:**
  - **Issue #4842** (aarch64 download of wrong architecture on Raspberry Pi) — closed.
  - **Issue #5289** (Bedrock provider sending erroneous `x-api-key` header causing 403) — closed.

---

## 4. Community Hot Topics

The community is most engaged around architecture scaling, new client interfaces, and channel extensibility:

- **Most Discussed Open Issue:**
  - **[#5982: Per-sender RBAC for multi-tenant deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982)** (8 comments) — Demand for isolated workspaces, tool sets, and rate limits is a clear signal of enterprise interest.
  - **[#5937: Refactor providers architecture](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)** (9 comments) — The most-commented issue, reflecting strong community alignment on the need to unify reqwest client management and reduce code duplication across providers.

- **Highest Reaction Counts:**
  - **[#4467: Add MCP resource and prompt support](https://github.com/zeroclaw-labs/zeroclaw/issues/4467)** (4 👍) — Strong user desire for MCP beyond tool-only client mode.
  - **[#3100: Mattermost oncall mode](https://github.com/zeroclaw-labs/zeroclaw/issues/3100)** (2 👍) — Persistent request for broader channel listening capabilities.
  - **[#4879: Gemini CLI OAuth failure](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)** (2 👍) — User frustration with a key provider workflow remains high.

- **ZeroCode TUI Introduced:**
  - **[PR #6848: zerocode TUI + RPC socket transport](https://github.com/zeroclaw-labs/zeroclaw/pull/6848)** — The largest active PR, representing a major new client interface. Seeking first-round feedback before a `v0.8.0-beta-2` tag.

- **Hardware Integration Buzz:**
  - A series of PRs from contributor `Rhoahndur` (**[#7045](https://github.com/zeroclaw-labs/zeroclaw/pull/7045), [#7046](https://github.com/zeroclaw-labs/zeroclaw/pull/7046), [#7047](https://github.com/zeroclaw-labs/zeroclaw/pull/7047), [#7048](https://github.com/zeroclaw-labs/zeroclaw/pull/7048)**), extracted from the ESP32 hackathon demo, are introducing smart-room named-device tools, a simulator, and serial allowlist features, signaling growing community interest in physical computing with ZeroClaw.

---

## 5. Bugs & Stability

The project resolved several high-impact bugs today, but a cluster of S1 (workflow-blocked) issues remains open.

- **Resolved in Last 24h:**
  - **S1 (Workflow Blocked):** Telegram voice transcription (#6999), Canvas streaming (#6965), Cron output routing (#6647) — all closed.
  - **S2 (Major Feature Broken):** Media pipeline annotations (#7033), WhatsApp Web LID JID handling (#7032) — closed.
  - **Architecture-specific:** aarch64 update command (#4842) — closed.

- **Open S1 & High-Severity Bugs:**
  - **[#7043: zerocode TUI never reconnects after daemon close](https://github.com/zeroclaw-labs/zeroclaw/issues/7043)** (S1) — The new TUI becomes permanently unresponsive after daemon restart; a critical UX blocker ahead of the TUI's general availability.
  - **[#7042: Daemon IPC crash on file-descriptor exhaustion (EMFILE)](https://github.com/zeroclaw-labs/zeroclaw/issues/7042)** (S1) — A runtime reliability risk under sustained load.
  - **[#7038: `zeroclaw check` 11/11 websocket 401 despite valid auth](https://github.com/zeroclaw-labs/zeroclaw/issues/7038)** (S1) — Health check tool fully failing with valid credentials.
  - **[#5962: Ollama Provider call failure when tools are needed](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)** (S1, P2) — Blocks all subsequent messages in a session.
  - **[#4879: Gemini CLI OAuth broken](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)** (P1, S1) — Long-standing provider integration failure.
  - **[#5866: Telegram bot ignores replies on its messages with `mention_only=true`](https://github.com/zeroclaw-labs/zeroclaw/issues/5866)** (S1, P2) — Group chat UX regression.
  - **[#5155: Delegate agents ignore `prompt_injection_mode`](https://github.com/zeroclaw-labs/zeroclaw/issues/5155)** (P1, S1) — Delegates always inject full skills regardless of global compact mode setting.

- **Security-Related Bug of Note:**
  - **[#5122: web_fetch `allowed_private_hosts` bypass for DNS names resolving to private IPs](https://github.com/zeroclaw-labs/zeroclaw/issues/5122)** (P1, S2) — Security feature remains partially broken; accepted and in-progress with no fix merged yet.

- **Minor Issues:**
  - **[#7037: Discord invite link in README is invalid](https://github.com/zeroclaw-labs/zeroclaw/issues/7037)** (S3) — Affects community onboarding.

---

## 6. Feature Requests & Roadmap Signals

The project's trajectory is clearly visible through open trackers and active PR themes:

- **Short-Term (v0.7.6 — Skills Focus):**
  - The **[#6253 tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)** (P1) is coordinating improvements across CLI, loader, audit, install paths, sandbox, and skill authoring tools.

- **Near-Term (v0.8.1 — Integration Push):**
  - **[#6970: v0.8.1 integration queue](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)** (P2) is routing additive channels, providers, and tools through the pipeline.
  - Actively landing: **Multi-tenant Linq channel** ([#7041](https://github.com/zeroclaw-labs/zeroclaw/pull/7041)), **Email IMAP channel with XOAUTH2** ([#7021](https://github.com/zeroclaw-labs/zeroclaw/pull/7021)), **Twilio SMS** ([#6429](https://github.com/zeroclaw-labs/zeroclaw/pull/6429)), **OGG/Opus TTS transcoding** ([#7050](https://github.com/zeroclaw-labs/zeroclaw/pull/7050)), **Static output modality preference** ([#7020](https://github.com/zeroclaw-labs/zeroclaw/pull/7020)).

- **Medium-to-Long-Term Signals:**
  - **Enterprise Multi-Tenancy:** [#5982 (RBAC)](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) and [#5937 (Architecture Refactor)](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) are foundational requirements for multi-user deployments.
  - **MCP Expansion:** [#4467 (MCP resources/prompts)](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) signals a push beyond tool-only MCP integration.
  - **Hardware & IoT:** The stream of PRs from the ESP32 demo (#6148 series) suggests an emerging IoT/edge compute use case.
  - **Release Infrastructure:** [#6822 (zerocode in build matrix)](https://github.com/zeroclaw-labs/zeroclaw/issues/6822) is a prerequisite for the TUI client to ship alongside the main binary.

- **Notable Config Fix Landed:**
  - Model-wise reasoning configuration (closed #5843) is now supported after community request.

---

## 7. User Feedback Summary

- **Pain Points — Stability & UX:**
  - **Telegram reliability** has been a recurring theme. Voice transcription (#6999) and group reply handling (#5866) are areas users have found frustrating.
  - **TUI robustness** shows early adopter friction: the daemon disconnect handling (#7043) and crash-on-fd-exhaustion (#7042) are blocking users who adopt the new interface.
  - **Provider friction:** Ollama tool calls (#5962), Gemini OAuth (#4879), and the Bedrock header issue (#5289, now closed) show that provider diversity comes with integration maintenance costs.
  - **Community access:** The invalid Discord invite (#7037) is a small but meaningful signal of documentation upkeep friction.

- **Positive Signals:**
  - The **high volume of repeat contributors** (`Audacity88`, `singlerider`, `Rhoahndur`, `mov-xound-glitch`, `yijunyu`) indicates a healthy and invested development community.
  - The **rapid closure of reported S1 bugs** (#6999, #6965, #6647) demonstrates maintainers are responsive to critical workflow blocks.
  - **Active pre-release development** (v0.7.6, v0.8.1, v0.8.0-beta-2) shows momentum and transparent planning.

---

## 8. Backlog Watch

Several important items are lingering and may require maintainer attention:

- **PRs Needing Action:**
  - **[#6148: ESP32 hardware demo](https://github.com/zeroclaw-labs/zeroclaw/pull/6148)** (and its extracted children #7046, #7047, #7048) — The largest feature branch in flight. Broken down for review but maintainer bandwidth is a constraint.
  - **[#6429: Twilio SMS channel](https://github.com/zeroclaw-labs/zeroclaw/pull/6429)** — Flagged `needs-author-action`; pending contributor response.

- **Long-Standing High-Impact Open Issues:**
  - **[#4879: Gemini CLI OAuth](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)** (P1, since March 28) — Still blocking an entire provider path for a significant user segment.
  - **[#5122: web_fetch security bypass](https://github.com/zeroclaw-labs/zeroclaw/issues/5122)** (P1, since March 29) — A security feature that remains partially broken for over two months.
  - **[#4467: MCP resource/prompt support](https://github.com/zeroclaw-labs/zeroclaw/issues/4467)** (P2, since March 24) — Despite being the most-upvoted issue (4 👍), progression toward a solution appears stalled.

- **Codebase Integrity Watch:**
  - **[#6074: Audit of 153 commits lost in bulk revert](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)** (P2) — An open issue documenting that a single commit reverted 153 commits. While it was a necessary rollback, the lost fixes, features, and improvements have no recovery plan visible in the thread. This warrants long-term monitoring.
  - **[#6720: `context_aware_tools` dead code](https://github.com/zeroclaw-labs/zeroclaw/issues/6720)** (P2) — A config field that parses cleanly but is never read. Community users enabling this field expecting functionality will hit a silent failure. Maintainers should either wire the feature or remove the config option with a deprecation notice.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/AlexdanerZe/agents-radar).*